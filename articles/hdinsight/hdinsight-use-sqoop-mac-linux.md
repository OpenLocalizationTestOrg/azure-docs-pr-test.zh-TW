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
# <a name="use-apache-sqoop-tooimport-and-export-data-between-hadoop-on-hdinsight-and-sql-database"></a><span data-ttu-id="42674-104">使用 Apache Sqoop tooimport 和匯出 HDInsight 上的 Hadoop 和 SQL Database 之間的資料</span><span class="sxs-lookup"><span data-stu-id="42674-104">Use Apache Sqoop tooimport and export data between Hadoop on HDInsight and SQL Database</span></span>

[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

<span data-ttu-id="42674-105">了解如何 toouse Apache Sqoop tooimport 匯出之間在 Hadoop 叢集 Azure HDInsight 和 Azure SQL Database 或 Microsoft SQL Server 資料庫。</span><span class="sxs-lookup"><span data-stu-id="42674-105">Learn how toouse Apache Sqoop tooimport and export between a Hadoop cluster in Azure HDInsight and Azure SQL Database or Microsoft SQL Server database.</span></span> <span data-ttu-id="42674-106">在此文件使用 hello 步驟 hello`sqoop`命令直接從 hello hello Hadoop 叢集的前端節點。</span><span class="sxs-lookup"><span data-stu-id="42674-106">hello steps in this document use hello `sqoop` command directly from hello headnode of hello Hadoop cluster.</span></span> <span data-ttu-id="42674-107">您使用 SSH tooconnect toohello 前端節點，並執行這份文件中的 hello 命令。</span><span class="sxs-lookup"><span data-stu-id="42674-107">You use SSH tooconnect toohello head node and run hello commands in this document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="42674-108">hello 本文件中的步驟只適用於使用 Linux 的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="42674-108">hello steps in this document only work with HDInsight clusters that use Linux.</span></span> <span data-ttu-id="42674-109">Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。</span><span class="sxs-lookup"><span data-stu-id="42674-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="42674-110">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="42674-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="install-freetds"></a><span data-ttu-id="42674-111">安裝 FreeTDS</span><span class="sxs-lookup"><span data-stu-id="42674-111">Install FreeTDS</span></span>

1. <span data-ttu-id="42674-112">使用 SSH tooconnect toohello HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="42674-112">Use SSH tooconnect toohello HDInsight cluster.</span></span> <span data-ttu-id="42674-113">例如，下列命令的 hello 連接 toohello 名為叢集的主要前端節點`mycluster`:</span><span class="sxs-lookup"><span data-stu-id="42674-113">For example, hello following command connects toohello primary headnode of a cluster named `mycluster`:</span></span>

    ```bash
    ssh CLUSTERNAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="42674-114">如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="42674-114">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="42674-115">使用下列命令 tooinstall freetds 才能使用 hello:</span><span class="sxs-lookup"><span data-stu-id="42674-115">Use hello following command tooinstall FreeTDS:</span></span>

    ```bash
    sudo apt --assume-yes install freetds-dev freetds-bin
    ```

    <span data-ttu-id="42674-116">在數個步驟 tooconnect tooSQL 資料庫中用於 freetds 才能使用。</span><span class="sxs-lookup"><span data-stu-id="42674-116">FreeTDS is used in several steps tooconnect tooSQL Database.</span></span>

## <a name="create-hello-table-in-sql-database"></a><span data-ttu-id="42674-117">SQL 資料庫中建立 hello 資料表</span><span class="sxs-lookup"><span data-stu-id="42674-117">Create hello table in SQL Database</span></span>

> [!IMPORTANT]
> <span data-ttu-id="42674-118">如果您使用 hello HDInsight 叢集，而且在建立 SQL 資料庫[建立叢集和 SQL database](hdinsight-use-sqoop.md)，略過本節中的 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="42674-118">If you are using hello HDInsight cluster and SQL Database created in [Create cluster and SQL database](hdinsight-use-sqoop.md), skip hello steps in this section.</span></span> <span data-ttu-id="42674-119">hello 資料庫和資料表所建立的 hello 一部分步驟在 hello[建立叢集和 SQL database](hdinsight-use-sqoop.md)文件。</span><span class="sxs-lookup"><span data-stu-id="42674-119">hello database and table were created as part of hello steps in hello [Create cluster and SQL database](hdinsight-use-sqoop.md) document.</span></span>

1. <span data-ttu-id="42674-120">從 hello SSH 工作階段，使用下列命令 tooconnect toohello SQL Database 伺服器 hello。</span><span class="sxs-lookup"><span data-stu-id="42674-120">From hello SSH session, use hello following command tooconnect toohello SQL Database server.</span></span>

        TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D sqooptest

    <span data-ttu-id="42674-121">您收到的輸出類似 toohello 下列文字：</span><span class="sxs-lookup"><span data-stu-id="42674-121">You receive output similar toohello following text:</span></span>

        locale is "en_US.UTF-8"
        locale charset is "UTF-8"
        using default charset "UTF-8"
        Default database being set toosqooptest
        1>

2. <span data-ttu-id="42674-122">在 hello`1>`提示字元中，輸入下列查詢的 hello:</span><span class="sxs-lookup"><span data-stu-id="42674-122">At hello `1>` prompt, enter hello following query:</span></span>

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

    <span data-ttu-id="42674-123">當 hello`GO`輸入陳述式、 評估 hello 前一個陳述式。</span><span class="sxs-lookup"><span data-stu-id="42674-123">When hello `GO` statement is entered, hello previous statements are evaluated.</span></span> <span data-ttu-id="42674-124">首先，hello **mobiledata**建立資料表時，則叢集的索引加入 tooit （需要 SQL Database）。</span><span class="sxs-lookup"><span data-stu-id="42674-124">First, hello **mobiledata** table is created, then a clustered index is added tooit (required by SQL Database.)</span></span>

    <span data-ttu-id="42674-125">已建立下列 hello 資料表的查詢 tooverify 使用 hello:</span><span class="sxs-lookup"><span data-stu-id="42674-125">Use hello following query tooverify that hello table has been created:</span></span>

    ```sql
    SELECT * FROM information_schema.tables
    GO
    ```

    <span data-ttu-id="42674-126">您會看到下列文字的輸出類似 toohello:</span><span class="sxs-lookup"><span data-stu-id="42674-126">You see output similar toohello following text:</span></span>

        TABLE_CATALOG   TABLE_SCHEMA    TABLE_NAME      TABLE_TYPE
        sqooptest       dbo     mobiledata      BASE TABLE

3. <span data-ttu-id="42674-127">輸入`exit`在 hello`1>`提示 tooexit hello tsql 公用程式。</span><span class="sxs-lookup"><span data-stu-id="42674-127">Enter `exit` at hello `1>` prompt tooexit hello tsql utility.</span></span>

## <a name="sqoop-export"></a><span data-ttu-id="42674-128">Sqoop export</span><span class="sxs-lookup"><span data-stu-id="42674-128">Sqoop export</span></span>

1. <span data-ttu-id="42674-129">從 hello SSH 連線 toohello 叢集中，使用下列命令 tooverify Sqoop 可以看到您的 SQL Database 的 hello:</span><span class="sxs-lookup"><span data-stu-id="42674-129">From hello SSH connection toohello cluster, use hello following command tooverify that Sqoop can see your SQL Database:</span></span>

    ```bash
    sqoop list-databases --connect jdbc:sqlserver://<serverName>.database.windows.net:1433 --username <adminLogin> -P
    ```
    <span data-ttu-id="42674-130">出現提示時，輸入 hello 密碼 hello SQL 資料庫登入。</span><span class="sxs-lookup"><span data-stu-id="42674-130">When prompted, enter hello password for hello SQL Database login.</span></span>

    <span data-ttu-id="42674-131">此命令會傳回一份資料庫，包括 hello **sqooptest**您稍早建立的資料庫。</span><span class="sxs-lookup"><span data-stu-id="42674-131">This command returns a list of databases, including hello **sqooptest** database that you created earlier.</span></span>

2. <span data-ttu-id="42674-132">從 tooexport 資料**hivesampletable** toohello **mobiledata**資料表，請使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="42674-132">tooexport data from **hivesampletable** toohello **mobiledata** table, use hello following command:</span></span>

    ```bash
    sqoop export --connect 'jdbc:sqlserver://<serverName>.database.windows.net:1433;database=sqooptest' --username <adminLogin> -P --table 'mobiledata' --export-dir 'wasb:///hive/warehouse/hivesampletable' --fields-terminated-by '\t' -m 1
    ```

    <span data-ttu-id="42674-133">此命令會指示 Sqoop tooconnect toohello **sqooptest**資料庫。</span><span class="sxs-lookup"><span data-stu-id="42674-133">This command instructs Sqoop tooconnect toohello **sqooptest** database.</span></span> <span data-ttu-id="42674-134">Sqoop 再匯出資料**wasb: / hive/倉儲/hivesampletable** toohello **mobiledata**資料表。</span><span class="sxs-lookup"><span data-stu-id="42674-134">Sqoop then exports data from **wasb:///hive/warehouse/hivesampletable** toohello **mobiledata** table.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="42674-135">使用`wasb:///`如果 hello 您叢集的預設儲存體是 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="42674-135">Use `wasb:///` if hello default storage for your cluster is an Azure Storage account.</span></span> <span data-ttu-id="42674-136">如果是 Azure Data Lake Store，請使用 `adl:///`。</span><span class="sxs-lookup"><span data-stu-id="42674-136">Use `adl:///` if it is an Azure Data Lake Store.</span></span>

3. <span data-ttu-id="42674-137">Hello 命令完成之後，使用下列命令 tooconnect toohello 資料庫使用 TSQL hello:</span><span class="sxs-lookup"><span data-stu-id="42674-137">After hello command completes, use hello following command tooconnect toohello database using TSQL:</span></span>

    ```bash
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P -p 1433 -D sqooptest
    ```

    <span data-ttu-id="42674-138">一旦連接之後，使用 hello 遵循 hello 資料的陳述式 tooverify 已匯出的 toohello **mobiledata**資料表：</span><span class="sxs-lookup"><span data-stu-id="42674-138">Once connected, use hello following statements tooverify that hello data was exported toohello **mobiledata** table:</span></span>

    ```sql
    SET ROWCOUNT 50;
    SELECT * FROM mobiledata
    GO
    ```

    <span data-ttu-id="42674-139">您應該會看到 hello 資料表中資料的清單。</span><span class="sxs-lookup"><span data-stu-id="42674-139">You should see a listing of data in hello table.</span></span> <span data-ttu-id="42674-140">型別`exit`tooexit hello tsql 公用程式。</span><span class="sxs-lookup"><span data-stu-id="42674-140">Type `exit` tooexit hello tsql utility.</span></span>

## <a name="sqoop-import"></a><span data-ttu-id="42674-141">Sqoop import</span><span class="sxs-lookup"><span data-stu-id="42674-141">Sqoop import</span></span>

1. <span data-ttu-id="42674-142">使用 hello 下列命令從 hello tooimport 資料**mobiledata** toohello SQL 資料庫中的資料表**wasb: / 教學課程/usesqoop/importeddata** HDInsight 上的目錄：</span><span class="sxs-lookup"><span data-stu-id="42674-142">Use hello following command tooimport data from hello **mobiledata** table in SQL Database, toohello **wasb:///tutorials/usesqoop/importeddata** directory on HDInsight:</span></span>

    ```bash
    sqoop import --connect 'jdbc:sqlserver://<serverName>.database.windows.net:1433;database=sqooptest' --username <adminLogin> --password <adminPassword> --table 'mobiledata' --target-dir 'wasb:///tutorials/usesqoop/importeddata' --fields-terminated-by '\t' --lines-terminated-by '\n' -m 1
    ```

    <span data-ttu-id="42674-143">hello 資料中的 hello 欄位會以定位字元分隔，hello 線條會以新行字元終止。</span><span class="sxs-lookup"><span data-stu-id="42674-143">hello fields in hello data are separated by a tab character, and hello lines are terminated by a new-line character.</span></span>

2. <span data-ttu-id="42674-144">Hello 匯入完成後，請使用下列命令 toolist 出 hello 資料 hello 新目錄中的 hello:</span><span class="sxs-lookup"><span data-stu-id="42674-144">Once hello import has completed, use hello following command toolist out hello data in hello new directory:</span></span>

    ```bash
    hdfs dfs -text /tutorials/usesqoop/importeddata/part-m-00000
    ```

## <a name="using-sql-server"></a><span data-ttu-id="42674-145">使用 SQL Server</span><span class="sxs-lookup"><span data-stu-id="42674-145">Using SQL Server</span></span>

<span data-ttu-id="42674-146">您也可以使用 Sqoop tooimport，並在資料中心或 Azure 中裝載的虛擬機器上，從 SQL Server，匯出資料。</span><span class="sxs-lookup"><span data-stu-id="42674-146">You can also use Sqoop tooimport and export data from SQL Server, either in your data center or on a Virtual Machine hosted in Azure.</span></span> <span data-ttu-id="42674-147">使用 SQL Database 和 SQL Server 的 hello 差異如下：</span><span class="sxs-lookup"><span data-stu-id="42674-147">hello differences between using SQL Database and SQL Server are:</span></span>

* <span data-ttu-id="42674-148">HDInsight 和 SQL Server 必須是在 hello 相同 Azure 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="42674-148">Both HDInsight and SQL Server must be on hello same Azure Virtual Network.</span></span>

    <span data-ttu-id="42674-149">如需範例，請參閱 hello[連接 HDInsight tooyour 在內部部署網路](./connect-on-premises-network.md)文件。</span><span class="sxs-lookup"><span data-stu-id="42674-149">For an example, see hello [Connect HDInsight tooyour on-premises network](./connect-on-premises-network.md) document.</span></span>

    <span data-ttu-id="42674-150">如需有關使用 HDInsight 的 Azure 虛擬網路的詳細資訊，請參閱 hello[擴充具有 Azure 虛擬網路的 HDInsight](hdinsight-extend-hadoop-virtual-network.md)文件。</span><span class="sxs-lookup"><span data-stu-id="42674-150">For more information on using HDInsight with an Azure Virtual Network, see hello [Extend HDInsight with Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md) document.</span></span> <span data-ttu-id="42674-151">如需有關 Azure 虛擬網路的詳細資訊，請參閱 hello[虛擬網路概觀](../virtual-network/virtual-networks-overview.md)文件。</span><span class="sxs-lookup"><span data-stu-id="42674-151">For more information on Azure Virtual Network, see hello [Virtual Network Overview](../virtual-network/virtual-networks-overview.md) document.</span></span>

* <span data-ttu-id="42674-152">SQL Server 必須已設定的 tooallow SQL 驗證。</span><span class="sxs-lookup"><span data-stu-id="42674-152">SQL Server must be configured tooallow SQL authentication.</span></span> <span data-ttu-id="42674-153">如需詳細資訊，請參閱 hello [Choose an Authentication Mode](https://msdn.microsoft.com/ms144284.aspx)文件。</span><span class="sxs-lookup"><span data-stu-id="42674-153">For more information, see hello [Choose an Authentication Mode](https://msdn.microsoft.com/ms144284.aspx) document.</span></span>

* <span data-ttu-id="42674-154">您可能必須 tooconfigure SQL Server tooaccept 遠端連線。</span><span class="sxs-lookup"><span data-stu-id="42674-154">You may have tooconfigure SQL Server tooaccept remote connections.</span></span> <span data-ttu-id="42674-155">如需詳細資訊，請參閱 hello [tootroubleshoot 連接 toohello SQL Server 資料庫引擎](http://social.technet.microsoft.com/wiki/contents/articles/2102.how-to-troubleshoot-connecting-to-the-sql-server-database-engine.aspx)文件。</span><span class="sxs-lookup"><span data-stu-id="42674-155">For more information, see hello [How tootroubleshoot connecting toohello SQL Server database engine](http://social.technet.microsoft.com/wiki/contents/articles/2102.how-to-troubleshoot-connecting-to-the-sql-server-database-engine.aspx) document.</span></span>

* <span data-ttu-id="42674-156">建立 hello **sqooptest**使用公用程式，例如 SQL Server 中的資料庫**SQL Server Management Studio**或**tsql**。</span><span class="sxs-lookup"><span data-stu-id="42674-156">Create hello **sqooptest** database in SQL Server using a utility such as **SQL Server Management Studio** or **tsql**.</span></span> <span data-ttu-id="42674-157">使用 Azure CLI hello hello 步驟只適用於 Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="42674-157">hello steps for using hello Azure CLI only work for Azure SQL Database.</span></span>

    <span data-ttu-id="42674-158">使用下列 TRANSACT-SQL 陳述式 toocreate hello 的 hello **mobiledata**資料表：</span><span class="sxs-lookup"><span data-stu-id="42674-158">Use hello following Transact-SQL statements toocreate hello **mobiledata** table:</span></span>

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

* <span data-ttu-id="42674-159">當從 HDInsight 連線 toohello SQL Server，您可能必須 hello SQL Server toouse hello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="42674-159">When connecting toohello SQL Server from HDInsight, you may have toouse hello IP address of hello SQL Server.</span></span> <span data-ttu-id="42674-160">例如：</span><span class="sxs-lookup"><span data-stu-id="42674-160">For example:</span></span>

    ```bash
    sqoop import --connect 'jdbc:sqlserver://10.0.1.1:1433;database=sqooptest' --username <adminLogin> --password <adminPassword> --table 'mobiledata' --target-dir 'wasb:///tutorials/usesqoop/importeddata' --fields-terminated-by '\t' --lines-terminated-by '\n' -m 1
    ```

## <a name="limitations"></a><span data-ttu-id="42674-161">限制</span><span class="sxs-lookup"><span data-stu-id="42674-161">Limitations</span></span>

* <span data-ttu-id="42674-162">大量匯出的以 Linux 為基礎的 HDInsight、 hello Sqoop 使用連接器 tooexport 資料 tooMicrosoft SQL Server 或 Azure SQL Database 目前不支援大量插入。</span><span class="sxs-lookup"><span data-stu-id="42674-162">Bulk export - With Linux-based HDInsight, hello Sqoop connector used tooexport data tooMicrosoft SQL Server or Azure SQL Database does not currently support bulk inserts.</span></span>

* <span data-ttu-id="42674-163">批次處理-與 linux 的 HDInsight，當使用 hello`-batch`切換時執行插入、 Sqoop 可讓多個插入，而不是批次處理 hello 插入作業。</span><span class="sxs-lookup"><span data-stu-id="42674-163">Batching - With Linux-based HDInsight, When using hello `-batch` switch when performing inserts, Sqoop makes multiple inserts instead of batching hello insert operations.</span></span>

## <a name="next-steps"></a><span data-ttu-id="42674-164">後續步驟</span><span class="sxs-lookup"><span data-stu-id="42674-164">Next steps</span></span>

<span data-ttu-id="42674-165">現在您已經學會如何 toouse Sqoop。</span><span class="sxs-lookup"><span data-stu-id="42674-165">Now you have learned how toouse Sqoop.</span></span> <span data-ttu-id="42674-166">toolearn 詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="42674-166">toolearn more, see:</span></span>

* <span data-ttu-id="42674-167">[搭配 HDInsight 使用 Oozie][hdinsight-use-oozie]：在 Oozie 工作流程中使用 Sqoop 動作。</span><span class="sxs-lookup"><span data-stu-id="42674-167">[Use Oozie with HDInsight][hdinsight-use-oozie]: Use Sqoop action in an Oozie workflow.</span></span>
* <span data-ttu-id="42674-168">[飛行延遲使用分析資料 HDInsight][hdinsight-analyze-flight-data]： 使用 Hive tooanalyze 飛行延遲的資料，然後再使用 Sqoop tooexport 資料 tooan Azure SQL database。</span><span class="sxs-lookup"><span data-stu-id="42674-168">[Analyze flight delay data using HDInsight][hdinsight-analyze-flight-data]: Use Hive tooanalyze flight delay data, and then use Sqoop tooexport data tooan Azure SQL database.</span></span>
* <span data-ttu-id="42674-169">[上傳資料 tooHDInsight][hdinsight-upload-data]： 尋找其他方法上, 傳資料 tooHDInsight/Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="42674-169">[Upload data tooHDInsight][hdinsight-upload-data]: Find other methods for uploading data tooHDInsight/Azure Blob storage.</span></span>

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
