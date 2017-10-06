---
title: "aaaUse Hadoop Hive 和 HDInsight 的 Azure 中的遠端桌面 |Microsoft 文件"
description: "了解如何 tooconnect tooHadoop HDInsight 中使用叢集的遠端桌面，並使用 hello hive 控制檔的命令列介面，以執行 Hive 查詢。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 8c228e35-d58a-4f22-917a-1d20c9da89b4
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/12/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: f86ffc1be33a8b0b2346d1a1388e5dfa6d0f8777
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hive-with-hadoop-on-hdinsight-with-remote-desktop"></a>利用遠端桌面搭配使用 Hive 與 HDInsight 上的 Hadoop
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

在本文中，您將學習如何 tooconnect tooan HDInsight 叢集使用遠端桌面，然後再執行 Hive 查詢使用 hello hive 控制檔的命令列介面 (CLI)。

> [!IMPORTANT]
> 只有在使用 Windows 做為 hello 作業系統的 HDInsight 叢集上使用遠端桌面。 Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。 如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。
>
> HDInsight 3.4 或更高，請參閱[使用 Hive 與 HDInsight Beeline](hdinsight-hadoop-use-hive-beeline.md)直接在 hello 叢集上執行 Hive 查詢，從命令列上的資訊。

## <a id="prereq"></a>必要條件
toocomplete hello 本文中的步驟，您需要下列 hello:

* Windows 型 HDInsight (HDInsight 上的 Hadoop) 叢集
* 執行 Windows 10、Windows 8 或 Windows 7 的用戶端電腦

## <a id="connect"></a>使用遠端桌面連線
Hello HDInsight 叢集，啟用遠端桌面，然後依照指示 hello 連接 tooit[連接使用 RDP tooHDInsight 叢集](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)。

## <a id="hive"></a>使用 hello Hive 命令
當您有連接 toohello 桌面 hello HDInsight 叢集時，使用下列步驟 toowork Hive 與 hello:

1. 從 hello HDInsight 桌面啟動 hello **Hadoop 命令列**。
2. 輸入下列命令 toostart hello Hive CLI hello:

        %hive_home%\bin\hive

    Hello CLI 啟動之後，您會看到 hello Hive CLI 提示： `hive>`。
3. 使用 hello CLI 中，輸入下列陳述式 toocreate 名為的新資料表的 hello **log4jLogs**使用範例資料：

        set hive.execution.engine=tez;
        DROP TABLE log4jLogs;
        CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
        STORED AS TEXTFILE LOCATION 'wasb:///example/data/';
        SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

    這些陳述式會執行下列動作的 hello:

   * **DROP TABLE**: hello 資料表已存在時刪除 hello 資料表與 hello 資料檔。
   * **CREATE EXTERNAL TABLE**：在 Hive 中建立新的「外部」資料表。 外部資料表 (資料會保留在 hello 原始位置中的 hello) 登錄區中儲存只有 hello 資料表定義。

     > [!NOTE]
     > 當您預期 hello 基礎資料 toobe 更新由外部來源 （例如自動化的資料上傳程序中） 或另一項 MapReduce 作業，但是您通常想要登錄區查詢 toouse hello 最新的資料，應該使用外部資料表。
     >
     > 卸除的外部資料表沒有**不**刪除 hello 資料、 hello 資料表定義。
     >
     >
   * **資料列格式**: hello 資料格式化的方式會告知 hive 控制檔。 在此情況下，每個記錄檔中的 hello 欄位會以空格分隔。
   * **儲存為文字檔位置**： 告訴 Hive 其中 hello 資料是儲存 （hello 範例/資料目錄），則會儲存為文字。
   * **選取**： 選取所有資料列計數其中資料行**t4**包含 hello 值**[錯誤]**。 這應該會傳回值 **3** ，因為有三個資料列包含此值。
   * **INPUT__FILE__NAME LIKE '%.log'** - 告訴 Hive 我們只應該從檔名以 log 結尾的檔案中傳回資料。 這會限制 hello 搜尋 toohello sample.log 檔案，其中包含 hello 資料，並防止從其他範例與 hello 我們所定義的結構描述不相符的資料檔案傳回資料。
4. 下列陳述式 toocreate 名為 'internal' 新的資料表使用 hello**錯誤記錄檔**:

        CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
        INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log';

    這些陳述式會執行下列動作的 hello:

   * **CREATE TABLE IF NOT EXISTS**：建立資料表 (如果不存在)。 因為 hello**外部**關鍵字不是，這是內部的資料表，hello Hive 資料倉儲中所儲存且受完全登錄區。

     > [!NOTE]
     > 不同於**外部**資料表，卸除內部資料表也會刪除基礎資料的 hello。
     >
     >
   * **儲存 AS ORC**: hello 資料儲存最佳化的資料列單欄式 (ORC) 格式。 這是高度最佳化且有效率的 Hive 資料儲存格式。
   * **INSERT OVERWRITE ...選取**： 選取資料列從 hello **log4jLogs**包含資料表**[錯誤]**，然後插入到 hello hello 資料**錯誤記錄檔**資料表。

     只有資料列的 tooverify 包含**[錯誤]**資料行 t4 是預存的 toohello**錯誤記錄檔**資料表，請使用下列陳述式 tooreturn 所有 hello 中的資料列的 hello**錯誤記錄檔**:

       SELECT * from errorLogs;

     應該傳回三個資料列，且在資料行 t4 中全部包含 **[ERROR]** 。

## <a id="summary"></a>摘要
如您所見，hello hello Hive 命令提供的 HDInsight 叢集上執行 Hive 查詢輕鬆 toointeractively，監視 hello 工作的狀態，和擷取 hello 輸出。

## <a id="nextsteps"></a>接續步驟
如需 HDInsight 中 Hive 的一般資訊：

* [搭配使用 Hive 與 HDInsight 上的 Hadoop](hdinsight-use-hive.md)

如需您可以在 HDInsight 上使用 Hadoop 之其他方式的詳細資訊：

* [搭配使用 Pig 與 HDInsight 上的 Hadoop](hdinsight-use-pig.md)
* [搭配使用 MapReduce 與 HDInsight 上的 Hadoop](hdinsight-use-mapreduce.md)

如果您正在使用 Hive Tez，請參閱下列文件的偵錯資訊的 hello:

* [使用 Windows 為基礎的 HDInsight 上的 hello Tez UI](hdinsight-debug-tez-ui.md)
* [使用 hello Ambari Tez 以 Linux 為基礎的 HDInsight 上的檢視](hdinsight-debug-ambari-tez-view.md)

[1]: ../HDInsight/hdinsight-hadoop-visual-studio-tools-get-started.md

[hdinsight-sdk-documentation]: http://msdnstage.redmond.corp.microsoft.com/library/dn479185.aspx

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[apache-tez]: http://tez.apache.org
[apache-hive]: http://hive.apache.org/
[apache-log4j]: http://en.wikipedia.org/wiki/Log4j
[hive-on-tez-wiki]: https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez
[import-to-excel]: http://azure.microsoft.com/documentation/articles/hdinsight-connect-excel-power-query/


[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md





[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md


[Powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx
