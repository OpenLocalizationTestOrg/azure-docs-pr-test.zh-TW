---
title: "aaaApache 的 Hadoop-Azure HDInsight Sqoop |Microsoft 文件"
description: "深入了解如何 toouse Apache Sqoop tooimport 和 HDInsight 上的 Hadoop 和 Azure SQL Database 之間的匯出。"
editor: cgronlun
manager: jhubbard
services: hdinsight
documentationcenter: 
author: Blackmist
tags: azure-portal
keywords: hadoop sqoop,sqoop
ms.assetid: 303649a5-4be5-4933-bf1d-4b232083c354
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: larryfr
ms.openlocfilehash: b256285659bbcf18ff05e220ccdf51c21eb8fbf7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-apache-sqoop-tooimport-and-export-data-between-hadoop-on-hdinsight-and-sql-database"></a>使用 Apache Sqoop tooimport 和匯出 HDInsight 上的 Hadoop 和 SQL Database 之間的資料

[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

了解如何 toouse Apache Sqoop tooimport 匯出之間在 Hadoop 叢集 Azure HDInsight 和 Azure SQL Database 或 Microsoft SQL Server 資料庫。 在此文件使用 hello 步驟 hello`sqoop`命令直接從 hello hello Hadoop 叢集的前端節點。 您使用 SSH tooconnect toohello 前端節點，並執行這份文件中的 hello 命令。

> [!IMPORTANT]
> hello 本文件中的步驟只適用於使用 Linux 的 HDInsight 叢集。 Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。 如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。

## <a name="install-freetds"></a>安裝 FreeTDS

1. 使用 SSH tooconnect toohello HDInsight 叢集。 例如，下列命令的 hello 連接 toohello 名為叢集的主要前端節點`mycluster`:

    ```bash
    ssh CLUSTERNAME-ssh.azurehdinsight.net
    ```

    如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。

2. 使用下列命令 tooinstall freetds 才能使用 hello:

    ```bash
    sudo apt --assume-yes install freetds-dev freetds-bin
    ```

    在數個步驟 tooconnect tooSQL 資料庫中用於 freetds 才能使用。

## <a name="create-hello-table-in-sql-database"></a>SQL 資料庫中建立 hello 資料表

> [!IMPORTANT]
> 如果您使用 hello HDInsight 叢集，而且在建立 SQL 資料庫[建立叢集和 SQL database](hdinsight-use-sqoop.md)，略過本節中的 hello 步驟。 hello 資料庫和資料表所建立的 hello 一部分步驟在 hello[建立叢集和 SQL database](hdinsight-use-sqoop.md)文件。

1. 從 hello SSH 工作階段，使用下列命令 tooconnect toohello SQL Database 伺服器 hello。

        TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D sqooptest

    您收到的輸出類似 toohello 下列文字：

        locale is "en_US.UTF-8"
        locale charset is "UTF-8"
        using default charset "UTF-8"
        Default database being set toosqooptest
        1>

2. 在 hello`1>`提示字元中，輸入下列查詢的 hello:

    ```sql
    CREATE TABLE [dbo].[mobiledata](
    [clientid] [nvarchar](50),
    [querytime] [nvarchar](50),
    [market] [nvarchar](50),
    [deviceplatform] [nvarchar](50),
    [devicemake] [nvarchar](50),
    [devicemodel] [nvarchar](50),
    [state] [nvarchar](50),
    [country] [nvarchar](50),
    [querydwelltime] [float],
    [sessionid] [bigint],
    [sessionpagevieworder] [bigint])
    GO
    CREATE CLUSTERED INDEX mobiledata_clustered_index on mobiledata(clientid)
    GO
    ```

    當 hello`GO`輸入陳述式、 評估 hello 前一個陳述式。 首先，hello **mobiledata**建立資料表時，則叢集的索引加入 tooit （需要 SQL Database）。

    已建立下列 hello 資料表的查詢 tooverify 使用 hello:

    ```sql
    SELECT * FROM information_schema.tables
    GO
    ```

    您會看到下列文字的輸出類似 toohello:

        TABLE_CATALOG   TABLE_SCHEMA    TABLE_NAME      TABLE_TYPE
        sqooptest       dbo     mobiledata      BASE TABLE

3. 輸入`exit`在 hello`1>`提示 tooexit hello tsql 公用程式。

## <a name="sqoop-export"></a>Sqoop export

1. 從 hello SSH 連線 toohello 叢集中，使用下列命令 tooverify Sqoop 可以看到您的 SQL Database 的 hello:

    ```bash
    sqoop list-databases --connect jdbc:sqlserver://<serverName>.database.windows.net:1433 --username <adminLogin> -P
    ```
    出現提示時，輸入 hello 密碼 hello SQL 資料庫登入。

    此命令會傳回一份資料庫，包括 hello **sqooptest**您稍早建立的資料庫。

2. 從 tooexport 資料**hivesampletable** toohello **mobiledata**資料表，請使用下列命令的 hello:

    ```bash
    sqoop export --connect 'jdbc:sqlserver://<serverName>.database.windows.net:1433;database=sqooptest' --username <adminLogin> -P --table 'mobiledata' --export-dir 'wasb:///hive/warehouse/hivesampletable' --fields-terminated-by '\t' -m 1
    ```

    此命令會指示 Sqoop tooconnect toohello **sqooptest**資料庫。 Sqoop 再匯出資料**wasb: / hive/倉儲/hivesampletable** toohello **mobiledata**資料表。

    > [!IMPORTANT]
    > 使用`wasb:///`如果 hello 您叢集的預設儲存體是 Azure 儲存體帳戶。 如果是 Azure Data Lake Store，請使用 `adl:///`。

3. Hello 命令完成之後，使用下列命令 tooconnect toohello 資料庫使用 TSQL hello:

    ```bash
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P -p 1433 -D sqooptest
    ```

    一旦連接之後，使用 hello 遵循 hello 資料的陳述式 tooverify 已匯出的 toohello **mobiledata**資料表：

    ```sql
    SET ROWCOUNT 50;
    SELECT * FROM mobiledata
    GO
    ```

    您應該會看到 hello 資料表中資料的清單。 型別`exit`tooexit hello tsql 公用程式。

## <a name="sqoop-import"></a>Sqoop import

1. 使用 hello 下列命令從 hello tooimport 資料**mobiledata** toohello SQL 資料庫中的資料表**wasb: / 教學課程/usesqoop/importeddata** HDInsight 上的目錄：

    ```bash
    sqoop import --connect 'jdbc:sqlserver://<serverName>.database.windows.net:1433;database=sqooptest' --username <adminLogin> --password <adminPassword> --table 'mobiledata' --target-dir 'wasb:///tutorials/usesqoop/importeddata' --fields-terminated-by '\t' --lines-terminated-by '\n' -m 1
    ```

    hello 資料中的 hello 欄位會以定位字元分隔，hello 線條會以新行字元終止。

2. Hello 匯入完成後，請使用下列命令 toolist 出 hello 資料 hello 新目錄中的 hello:

    ```bash
    hdfs dfs -text /tutorials/usesqoop/importeddata/part-m-00000
    ```

## <a name="using-sql-server"></a>使用 SQL Server

您也可以使用 Sqoop tooimport，並在資料中心或 Azure 中裝載的虛擬機器上，從 SQL Server，匯出資料。 使用 SQL Database 和 SQL Server 的 hello 差異如下：

* HDInsight 和 SQL Server 必須是在 hello 相同 Azure 虛擬網路。

    如需範例，請參閱 hello[連接 HDInsight tooyour 在內部部署網路](./connect-on-premises-network.md)文件。

    如需有關使用 HDInsight 的 Azure 虛擬網路的詳細資訊，請參閱 hello[擴充具有 Azure 虛擬網路的 HDInsight](hdinsight-extend-hadoop-virtual-network.md)文件。 如需有關 Azure 虛擬網路的詳細資訊，請參閱 hello[虛擬網路概觀](../virtual-network/virtual-networks-overview.md)文件。

* SQL Server 必須已設定的 tooallow SQL 驗證。 如需詳細資訊，請參閱 hello [Choose an Authentication Mode](https://msdn.microsoft.com/ms144284.aspx)文件。

* 您可能必須 tooconfigure SQL Server tooaccept 遠端連線。 如需詳細資訊，請參閱 hello [tootroubleshoot 連接 toohello SQL Server 資料庫引擎](http://social.technet.microsoft.com/wiki/contents/articles/2102.how-to-troubleshoot-connecting-to-the-sql-server-database-engine.aspx)文件。

* 建立 hello **sqooptest**使用公用程式，例如 SQL Server 中的資料庫**SQL Server Management Studio**或**tsql**。 使用 Azure CLI hello hello 步驟只適用於 Azure SQL Database。

    使用下列 TRANSACT-SQL 陳述式 toocreate hello 的 hello **mobiledata**資料表：

    ```sql
    CREATE TABLE [dbo].[mobiledata](
    [clientid] [nvarchar](50),
    [querytime] [nvarchar](50),
    [market] [nvarchar](50),
    [deviceplatform] [nvarchar](50),
    [devicemake] [nvarchar](50),
    [devicemodel] [nvarchar](50),
    [state] [nvarchar](50),
    [country] [nvarchar](50),
    [querydwelltime] [float],
    [sessionid] [bigint],
    [sessionpagevieworder] [bigint])
    ```

* 當從 HDInsight 連線 toohello SQL Server，您可能必須 hello SQL Server toouse hello IP 位址。 例如：

    ```bash
    sqoop import --connect 'jdbc:sqlserver://10.0.1.1:1433;database=sqooptest' --username <adminLogin> --password <adminPassword> --table 'mobiledata' --target-dir 'wasb:///tutorials/usesqoop/importeddata' --fields-terminated-by '\t' --lines-terminated-by '\n' -m 1
    ```

## <a name="limitations"></a>限制

* 大量匯出的以 Linux 為基礎的 HDInsight、 hello Sqoop 使用連接器 tooexport 資料 tooMicrosoft SQL Server 或 Azure SQL Database 目前不支援大量插入。

* 批次處理-與 linux 的 HDInsight，當使用 hello`-batch`切換時執行插入、 Sqoop 可讓多個插入，而不是批次處理 hello 插入作業。

## <a name="next-steps"></a>後續步驟

現在您已經學會如何 toouse Sqoop。 toolearn 詳細資訊，請參閱：

* [搭配 HDInsight 使用 Oozie][hdinsight-use-oozie]：在 Oozie 工作流程中使用 Sqoop 動作。
* [飛行延遲使用分析資料 HDInsight][hdinsight-analyze-flight-data]： 使用 Hive tooanalyze 飛行延遲的資料，然後再使用 Sqoop tooexport 資料 tooan Azure SQL database。
* [上傳資料 tooHDInsight][hdinsight-upload-data]： 尋找其他方法上, 傳資料 tooHDInsight/Azure Blob 儲存體。

[hdinsight-versions]:  hdinsight-component-versioning.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-storage]: ../hdinsight-hadoop-use-blob-storage.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md

[sqldatabase-get-started]: ../sql-database-get-started.md
[sqldatabase-create-configue]: ../sql-database-create-configure.md

[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx
[powershell-install]: /powershell/azureps-cmdlets-docs
[powershell-script]: http://technet.microsoft.com/library/ee176949.aspx

[sqoop-user-guide-1.4.4]: https://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html
