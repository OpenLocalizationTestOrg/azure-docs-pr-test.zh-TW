---
title: "aaaUse HDInsight 中的，以時間為基礎 Hadoop Oozie coordinator |Microsoft 文件"
description: "在 HDInsight 上使用以時間為基礎的 Hadoop Oozie 協調器：一項巨量資料服務。 深入了解如何 toodefine Oozie 工作流程和協調，並提交工作。"
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 00c3a395-d51a-44ff-af2d-1f116c4b1c83
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: aecbb5ee94a4234d1a7768bdb6de2a33508b1e4c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-time-based-oozie-coordinator-with-hadoop-in-hdinsight-toodefine-workflows-and-coordinate-jobs"></a>以時間為基礎的 Oozie 協調器使用 HDInsight toodefine 工作流程中的 Hadoop 和協調工作
在本文中，您將學習如何 toodefine 工作流程及協調員，和如何 tootrigger hello 協調器工作，根據時間。 它是透過有幫助 toogo[與 HDInsight 的使用 Oozie] [ hdinsight-use-oozie]閱讀本文之前。 此外 tooOozie，您也可以排定工作，使用 Azure Data Factory。 toolearn Azure Data Factory，請參閱[搭配使用 Pig 和 Hive 與 Data Factory](../data-factory/data-factory-data-transformation-activities.md)。

> [!NOTE]
> 本文章需有以 Windows 為基礎的 HDInsight 叢集。 如需使用 Oozie，包括以時間為基礎的工作，在以 Linux 為基礎的叢集上，請參閱[Hadoop toodefine 與執行工作流程以 Linux 為基礎的 HDInsight 上使用 Oozie](hdinsight-use-oozie-linux-mac.md)

## <a name="what-is-oozie"></a>什麼是 Oozie
Apache Oozie 是可管理 Hadoop 工作的工作流程/協調系統。 Hello Hadoop 堆疊，與整合，並支援 Apache MapReduce、 Apache Pig、 Apache Hive，和 Apache Sqoop Hadoop 工作。 它也可以使用的 tooschedule 作業的特定 tooa 系統，例如 Java 程式或殼層指令碼。

hello 下列影像顯示 hello 工作流程將實作：

![Workflow diagram][img-workflow-diagram]

hello 工作流程包含兩個動作：

1. 登錄區動作會執行下列 HiveQL 指令碼 toocount hello 每個記錄層級類型的發生 log4j 記錄檔中。 每個 log4j 記錄檔所組成，其中包含 [記錄層級] 欄位 tooshow hello 類型和 hello 嚴重性，例如欄位一行：

        2012-02-03 18:35:34 SampleClass6 [INFO] everything normal for id 577725851
        2012-02-03 18:35:34 SampleClass4 [FATAL] system problem at id 1991281254
        2012-02-03 18:35:34 SampleClass3 [DEBUG] detail for id 1304807656
        ...

    hello Hive 指令碼輸出如下：

        [DEBUG] 434
        [ERROR] 3
        [FATAL] 1
        [INFO]  96
        [TRACE] 816
        [WARN]  4

    如需 Hive 的詳細資訊，請參閱[在 HDInsight 上使用 Hive][hdinsight-use-hive]。
2. Sqoop 動作匯出 hello HiveQL 動作輸出 tooa 資料表在 Azure SQL 資料庫。 如需 Sqoop 的詳細資訊，請參閱[搭配 HDInsight 使用 Sqoop][hdinsight-use-sqoop]。

> [!NOTE]
> HDInsight 叢集上支援 Oozie 版本，請參閱[HDInsight 所提供的 hello 叢集版本中最新消息？][hdinsight-versions].
>
>

## <a name="prerequisites"></a>必要條件
開始本教學課程之前，您必須擁有 hello 下列：

* **具有 Azure PowerShell 的工作站**。

    > [!IMPORTANT]
    > 使用 Azure Service Manager 管理 HDInsight 資源的 Azure PowerShell 支援已**被取代**，將會在 2017 年 1 月 1 日前移除。 此文件使用 hello 新 HDInsight 的 cmdlet 可與 Azure 資源管理員中的步驟 hello。
    >
    > 請依照中的 hello 步驟[安裝和設定 Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall hello 最新版的 Azure PowerShell。 如果您有指令碼的需要 toobe 修改 toouse hello 新的 cmdlet 可與 Azure 資源管理員，請參閱[移轉 tooAzure 資源管理員為基礎的開發工具的 HDInsight 叢集](hdinsight-hadoop-development-using-azure-resource-manager.md)如需詳細資訊。

* **HDInsight 叢集**。 如需關於建立 HDInsight 叢集的詳細資訊，請參閱[建立 HDInsight 叢集][hdinsight-provision]或[開始使用 HDInsight][hdinsight-get-started]。 您需要下列資料 toogo hello 教學課程的 hello:

    <table border = "1">
    <tr><th>叢集屬性</th><th>Windows PowerShell 變數名稱</th><th>值</th><th>說明</th></tr>
    <tr><td>HDInsight 叢集名稱</td><td>$clusterName</td><td></td><td>您會在其執行本教學課程中的 hello HDInsight 叢集。</td></tr>
    <tr><td>HDInsight 叢集使用者名稱</td><td>$clusterUsername</td><td></td><td>hello HDInsight 叢集使用者名稱。 </td></tr>
    <tr><td>HDInsight 叢集使用者的密碼 </td><td>$clusterPassword</td><td></td><td>hello HDInsight 叢集的使用者密碼。</td></tr>
    <tr><td>Azure 儲存體帳戶名稱</td><td>$storageAccountName</td><td></td><td>Azure 儲存體帳戶可用 toohello HDInsight 叢集。 此教學課程中，使用 hello hello 叢集佈建程序期間所指定預設儲存體帳戶。</td></tr>
    <tr><td>Azure Blob 容器名稱</td><td>$containerName</td><td></td><td>此範例中，使用適用於 hello 預設 HDInsight 叢集檔案系統的 hello Azure Blob 儲存體容器。 根據預設，它有名稱為 hello HDInsight 叢集相同的 hello。</td></tr>
    </table>
* **Azure SQL Database**。 您必須從您的工作站設定 hello SQL Database 伺服器 tooallow 存取的防火牆規則。 如需有關建立 Azure SQL database 和 hello 防火牆設定的指示，請參閱 [開始使用 Azure SQL database] [sql database-get-已啟動]。 本文章提供 Windows PowerShell 指令碼來建立您需要在此教學課程的 hello Azure SQL 資料庫資料表。

    <table border = "1">
    <tr><th>SQL Database 屬性</th><th>Windows PowerShell 變數名稱</th><th>值</th><th>說明</th></tr>
    <tr><td>SQL Database 伺服器名稱</td><td>$sqlDatabaseServer</td><td></td><td>hello SQL 資料庫伺服器 toowhich Sqoop 會將資料匯出。 </td></tr>
    <tr><td>SQL Database 登入名稱</td><td>$sqlDatabaseLogin</td><td></td><td>SQL Database 登入名稱。</td></tr>
    <tr><td>SQL Database 登入密碼</td><td>$sqlDatabaseLoginPassword</td><td></td><td>SQL Database 登入密碼。</td></tr>
    <tr><td>SQL Database 名稱</td><td>$sqlDatabaseName</td><td></td><td>hello Azure SQL database toowhich Sqoop 會將資料匯出。 </td></tr>
    </table>

  > [!NOTE]
  > 根據預設，Azure SQL Database 接受來自 Azure 服務 (例如 Azure HDInsight) 的連線。 如果防火牆已停用此設定，您必須從 hello Azure 入口網站來啟用它。 如需關於建立 SQL Database 和設定防火牆規則的指示，請參閱[建立和設定 SQL Database][sqldatabase-get-started]。

> [!NOTE]
> 填入 hello hello 資料表中的值。 這將有助於本教學課程的執行。

## <a name="define-oozie-workflow-and-hello-related-hiveql-script"></a>定義 Oozie 工作流程和 hello 相關的下列 HiveQL 指令碼
Oozie 工作流程定義會以 hPDL 撰寫 (一種 XML 程序定義語言)。 hello 預設工作流程檔案名稱是*workflow.xml*。  您將 hello 工作流程在本機儲存檔案，然後再部署它 toohello HDInsight 叢集稍後在本教學課程使用 Azure PowerShell。

hello hello 工作流程中的登錄區動作呼叫下列 HiveQL 指令碼檔案。 此指令碼檔案包含三個 HiveQL 陳述式：

1. **DROP TABLE 陳述式 hello**刪除 hello log4j Hive 資料表，如果存在的話。
2. **hello CREATE TABLE 陳述式**建立 log4j Hive 外部資料表，指向 toohello hello log4j 記錄檔的位置。
3. **hello hello log4j 記錄檔的位置**。 hello 欄位分隔符號是"，"。 hello 預設列的分隔符號是"\n"。 Hive 外部資料表是要移除 hello 原始位置，從使用的 tooavoid hello 資料檔，萬一您想要讓 toorun hello Oozie 流程多次。
4. **hello 插入覆寫陳述式**計算 hello 出現從每個記錄層級型別 hello log4j Hive 資料表，並將儲存 hello 輸出 tooan Azure Blob 儲存體位置。

> [!NOTE]
> Hive 路徑有已知問題。 此問題會在您提交 Oozie 工作時發生。 hello 修正 hello 問題可以找到 hello TechNet Wiki 上的指示： [HDInsight Hive 錯誤： 無法 toorename][technetwiki-hive-error]。

**toodefine hello 下列 HiveQL 指令碼檔案 toobe 呼叫 hello 工作流程**

1. 建立以下列的 hello 文字檔案內容：

        DROP TABLE ${hiveTableName};
        CREATE EXTERNAL TABLE ${hiveTableName}(t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) ROW FORMAT DELIMITED FIELDS TERMINATED BY ' ' STORED AS TEXTFILE LOCATION '${hiveDataFolder}';
        INSERT OVERWRITE DIRECTORY '${hiveOutputFolder}' SELECT t4 AS sev, COUNT(*) AS cnt FROM ${hiveTableName} WHERE t4 LIKE '[%' GROUP BY t4;

    有三個 hello 指令碼中使用的變數：

   * ${hiveTableName}
   * ${hiveDataFolder}
   * ${hiveOutputFolder}

     hello 工作流程定義檔 (在本教學課程 workflow.xml) 會在執行階段傳遞這些值 toothis 下列 HiveQL 指令碼。
2. 將 hello 檔案儲存為**C:\Tutorials\UseOozie\useooziewf.hql**使用 ANSI (ASCII) 的編碼方式。 (如果您的文字編輯器沒有此選項，請使用「記事本」)。此指令碼檔案會在 hello 教學課程稍後部署的 toohello HDInsight 叢集。

**toodefine 工作流程**

1. 建立以下列的 hello 文字檔案內容：

    ```xml
    <workflow-app name="useooziewf" xmlns="uri:oozie:workflow:0.2">
        <start too= "RunHiveScript"/>

        <action name="RunHiveScript">
            <hive xmlns="uri:oozie:hive-action:0.2">
                <job-tracker>${jobTracker}</job-tracker>
                <name-node>${nameNode}</name-node>
                <configuration>
                    <property>
                        <name>mapred.job.queue.name</name>
                        <value>${queueName}</value>
                    </property>
                </configuration>
                <script>${hiveScript}</script>
                <param>hiveTableName=${hiveTableName}</param>
                <param>hiveDataFolder=${hiveDataFolder}</param>
                <param>hiveOutputFolder=${hiveOutputFolder}</param>
            </hive>
            <ok to="RunSqoopExport"/>
            <error to="fail"/>
        </action>

        <action name="RunSqoopExport">
            <sqoop xmlns="uri:oozie:sqoop-action:0.2">
                <job-tracker>${jobTracker}</job-tracker>
                <name-node>${nameNode}</name-node>
                <configuration>
                    <property>
                        <name>mapred.compress.map.output</name>
                        <value>true</value>
                    </property>
                </configuration>
            <arg>export</arg>
            <arg>--connect</arg>
            <arg>${sqlDatabaseConnectionString}</arg>
            <arg>--table</arg>
            <arg>${sqlDatabaseTableName}</arg>
            <arg>--export-dir</arg>
            <arg>${hiveOutputFolder}</arg>
            <arg>-m</arg>
            <arg>1</arg>
            <arg>--input-fields-terminated-by</arg>
            <arg>"\001"</arg>
            </sqoop>
            <ok to="end"/>
            <error to="fail"/>
        </action>

        <kill name="fail">
            <message>Job failed, error message[${wf:errorMessage(wf:lastErrorNode())}] </message>
        </kill>

        <end name="end"/>
    </workflow-app>
    ```

    有兩個 hello 工作流程中定義的動作。 hello 開始 tooaction 是*RunHiveScript*。 如果 hello 動作執行*確定*，hello 下一個動作是*RunSqoopExport*。

    hello RunHiveScript 有數個變數。 當您使用 Azure PowerShell 提交從工作站 hello Oozie 作業時，您將會傳遞 hello 值。

    工作流程變數

    <table border = "1">
    <tr><th>工作流程變數</th><th>說明</th></tr>
    <tr><td>${jobTracker}</td><td>指定 hello URL hello Hadoop 作業追蹤程式。 請在 HDInsight 叢集 3.0 和 2.0 版上使用 <strong>jobtrackerhost:9010</strong>。</td></tr>
    <tr><td>${nameNode}</td><td>指定 hello Hadoop 名稱節點 hello URL。 使用 hello 預設檔案系統 wasb: / / 位址，例如<i>wasb: / /&lt;containerName&gt;@&lt;storageAccountName&gt;。 account>.blob.core.windows.net</i>。</td></tr>
    <tr><td>${queueName}</td><td>指定要送往 hello hello 工作的佇列名稱。 使用<strong>預設值</strong>。</td></tr>
    </table>

    Hive 動作變數

    <table border = "1">
    <tr><th>Hive 動作變數</th><th>說明</th></tr>
    <tr><td>${hiveDataFolder}</td><td>hello hello Hive Create Table 命令的來源目錄。</td></tr>
    <tr><td>${hiveOutputFolder}</td><td>hello hello 插入覆寫陳述式的輸出資料夾。</td></tr>
    <tr><td>${hiveTableName}</td><td>hello hello Hive 資料表參考 hello log4j 資料檔案的名稱。</td></tr>
    </table>

    Sqoop 動作變數

    <table border = "1">
    <tr><th>Sqoop 動作變數</th><th>說明</th></tr>
    <tr><td>${sqlDatabaseConnectionString}</td><td>SQL Database 連接字串。</td></tr>
    <tr><td>${sqlDatabaseTableName}</td><td>將匯出 hello Azure SQL 資料庫資料表 toowhere hello 資料。</td></tr>
    <tr><td>${hiveOutputFolder}</td><td>hello hello hive 控制檔插入覆寫陳述式的輸出資料夾。 這是 hello hello Sqoop 匯出 (匯出 dir) 相同的資料夾。</td></tr>
    </table>

    如需 Oozie 工作流程，並使用 hello 工作流程動作的詳細資訊，請參閱[Apache Oozie 4.0 版文件][ apache-oozie-400] （適用於 HDInsight 叢集版本 3.0） 或[Apache Oozie 3.3.2文件][ apache-oozie-332] （適用於 HDInsight 叢集版本 2.1）。

1. 將 hello 檔案儲存為**C:\Tutorials\UseOozie\workflow.xml**使用 ANSI (ASCII) 的編碼方式。 (如果您的文字編輯器沒有此選項，請使用「記事本」)。

**toodefine 協調器**

1. 建立以下列的 hello 文字檔案內容：

    ```xml
    <coordinator-app name="my_coord_app" frequency="${coordFrequency}" start="${coordStart}" end="${coordEnd}" timezone="${coordTimezone}" xmlns="uri:oozie:coordinator:0.4">
        <action>
            <workflow>
                <app-path>${wfPath}</app-path>
            </workflow>
        </action>
    </coordinator-app>
    ```

    有五個 hello 定義檔中所使用的變數：

   | 變數 | 說明 |
   | --- | --- |
   | ${coordFrequency} |工作暫停時間。 頻率一律以分鐘表示。 |
   | ${coordStart} |工作開始時間。 |
   | ${coordEnd} |工作結束時間。 |
   | ${coordTimezone} |Oozie 在固定時區處理協調器工作，不受日光節約時間影響 (通常使用 UTC 表示)。 這個時區稱為 hello"Oozie 處理 timezone。 」 |
   | ${wfPath} |hello workflow.xml hello 路徑。  如果 hello 工作流程檔案名稱不是 hello 預設檔名 (workflow.xml)，您必須指定它。 |
2. 將 hello 檔案儲存為**C:\Tutorials\UseOozie\coordinator.xml**使用 hello ANSI (ASCII) 的編碼方式。 (如果您的文字編輯器沒有此選項，請使用「記事本」)。

## <a name="deploy-hello-oozie-project-and-prepare-hello-tutorial"></a>部署 hello Oozie 專案，並準備 hello 教學課程
您將會執行 Azure PowerShell 指令碼 tooperform hello 下列：

* 複製 hello 下列 HiveQL 指令碼 (useoozie.hql) tooAzure Blob 儲存體，wasb:///tutorials/useoozie/useoozie.hql。
* 將複製 workflow.xml toowasb:///tutorials/useoozie/workflow.xml。
* 將複製 coordinator.xml toowasb:///tutorials/useoozie/coordinator.xml。
* 複製 hello 資料檔 (/ example/data/sample.log) toowasb:///tutorials/useoozie/data/sample.log。
* 建立用於儲存 Sqoop 匯出資料的 Azure SQL Database 資料表。 hello 資料表名稱是*log4jLogCount*。

**了解 HDInsight 儲存體**

HDInsight 使用 Azure Blob 儲存體來儲存資料。 wasb: / / 是 Microsoft 的 hello Hadoop 分散式檔案系統 (HDFS) Azure Blob 儲存體中的實作。 如需詳細資訊，請參閱[搭配 HDInsight 使用 Azure Blob 儲存體][hdinsight-storage]。

當您佈建的 HDInsight 叢集時，Azure Blob 儲存體帳戶和特定的容器，從該帳戶指定為 hello 預設的檔案系統，例如 HDFS 中。 此外 toothis 儲存體帳戶，您可以加入額外的儲存體帳戶從 hello 相同 Azure 訂用帳戶或從不同的 Azure 訂閱 hello 佈建程序期間。 如需關於新增其他儲存體帳戶的指示，請參閱[佈建 HDInsight 叢集][hdinsight-provision]。 toosimplify hello Azure PowerShell 指令碼用在此教學課程中，所有的檔案儲存在 hello 預設檔案系統容器中的 hello 位於*/教學課程/useoozie*。 根據預設，此容器擁有的 hello 名稱做為 hello HDInsight 叢集名稱相同。
hello 語法為：

    wasb[s]://<ContainerName>@<StorageAccountName>.blob.core.windows.net/<path>/<filename>

> [!NOTE]
> 只有 hello *wasb: / /*在 HDInsight 叢集版本 3.0 支援語法。 較舊的 hello *asv: / /*語法支援 HDInsight 2.1 和 1.6 的叢集，但它不支援 HDInsight 3.0 叢集。
>
> hello wasb: / / 是虛擬路徑。 如需詳細資訊，請參閱[搭配 HDInsight 使用 Azure Blob 儲存體][hdinsight-storage]。

可以使用任何 hello 下列的 Uri （我使用 workflow.xml 做為範例），從 HDInsight 存取儲存在 hello 預設檔案系統容器中的檔案：

    wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie/workflow.xml
    wasb:///tutorials/useoozie/workflow.xml
    /tutorials/useoozie/workflow.xml

如果您想直接從 hello 儲存體帳戶的 tooaccess hello 檔案，hello hello 檔案的 blob 名稱是：

    tutorials/useoozie/workflow.xml

**了解 Hive 內部和外部資料表**

有幾件事，您需要 tooknow Hive 內部和外部資料表的相關：

* hello CREATE TABLE 命令會建立內部資料表中，也稱為受管理的資料表。 hello 資料檔必須位於 hello 預設容器。
* hello CREATE TABLE 命令移動 hello 資料檔案toohello/hive/倉儲/<TableName> hello 預設容器中的資料夾。
* hello CREATE EXTERNAL TABLE 命令會建立外部資料表。 hello 資料檔案可以位於外部 hello 預設容器。
* hello CREATE EXTERNAL TABLE 命令不會移動 hello 資料檔案。
* hello CREATE EXTERNAL TABLE 命令不允許 hello 位置子句中指定的 hello 資料夾下的任何子資料夾。 這是為什麼 hello 教學課程會建立一份 hello sample.log 檔案 hello 原因。

如需詳細資訊，請參閱 [HDInsight：Hive 內部和外部資料表簡介][cindygross-hive-tables]。

**tooprepare hello 教學課程**

1. 開啟 hello Windows PowerShell ISE (在 hello Windows 8 開始 畫面中，輸入**PowerShell_ISE**，然後按一下 **Windows PowerShell ISE**。 如需詳細資訊，請參閱[在 Windows 8 和 Windows 上啟動 Windows PowerShell][powershell-start])。
2. 在 hello 底部窗格中，執行下列命令 tooconnect tooyour Azure 訂用帳戶的 hello:

    ```powershell
    Add-AzureAccount
    ```

    您將會提示的 tooenter 您的 Azure 帳戶的認證。 此方法加入訂用帳戶連接的逾時和 12 小時之後，您就會再次具有 toorun hello cmdlet。

   > [!NOTE]
   > 如果您有多個 Azure 訂閱 hello 預設訂用帳戶不是您想要 toouse hello，請使用 hello <strong>Select-azuresubscription</strong> cmdlet tooselect 訂用帳戶。

3. 複製 hello 到 hello 指令碼窗格中，下列指令碼，然後設定 hello 前六個變數：

    ```powershell
    # WASB variables
    $storageAccountName = "<StorageAccountName>"
    $containerName = "<BlobStorageContainerName>"

    # SQL database variables
    $sqlDatabaseServer = "<SQLDatabaseServerName>"
    $sqlDatabaseLogin = "<SQLDatabaseLoginName>"
    $sqlDatabaseLoginPassword = "SQLDatabaseLoginPassword>"
    $sqlDatabaseName = "<SQLDatabaseName>"
    $sqlDatabaseTableName = "log4jLogsCount"

    # Oozie files for hello tutorial
    $hiveQLScript = "C:\Tutorials\UseOozie\useooziewf.hql"
    $workflowDefinition = "C:\Tutorials\UseOozie\workflow.xml"
    $coordDefinition =  "C:\Tutorials\UseOozie\coordinator.xml"

    # WASB folder for storing hello Oozie tutorial files.
    $destFolder = "tutorials/useoozie"  # Do NOT use hello long path here
    ```

    如需 hello 變數的詳細描述，請參閱 hello[必要條件](#prerequisites)在本教學課程 > 一節。

4. 附加 hello 遵循 toohello hello 指令碼窗格中的指令碼：

    ```powershell
    # Create a storage context object
    $storageaccountkey = get-azurestoragekey $storageAccountName | %{$_.Primary}
    $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageaccountkey

    function uploadOozieFiles()
    {
        Write-Host "Copy HiveQL script, workflow definition and coordinator definition ..." -ForegroundColor Green
        Set-AzureStorageBlobContent -File $hiveQLScript -Container $containerName -Blob "$destFolder/useooziewf.hql" -Context $destContext
        Set-AzureStorageBlobContent -File $workflowDefinition -Container $containerName -Blob "$destFolder/workflow.xml" -Context $destContext
        Set-AzureStorageBlobContent -File $coordDefinition -Container $containerName -Blob "$destFolder/coordinator.xml" -Context $destContext
    }

    function prepareHiveDataFile()
    {
        Write-Host "Make a copy of hello sample.log file ... " -ForegroundColor Green
        Start-CopyAzureStorageBlob -SrcContainer $containerName -SrcBlob "example/data/sample.log" -Context $destContext -DestContainer $containerName -destBlob "$destFolder/data/sample.log" -DestContext $destContext
    }

    function prepareSQLDatabase()
    {
        # SQL query string for creating log4jLogsCount table
        $cmdCreateLog4jCountTable = " CREATE TABLE [dbo].[$sqlDatabaseTableName](
                [Level] [nvarchar](10) NOT NULL,
                [Total] float,
            CONSTRAINT [PK_$sqlDatabaseTableName] PRIMARY KEY CLUSTERED
            (
            [Level] ASC
            )
            )"

        #Create hello log4jLogsCount table
        Write-Host "Create Log4jLogsCount table ..." -ForegroundColor Green
        $conn = New-Object System.Data.SqlClient.SqlConnection
        $conn.ConnectionString = "Data Source=$sqlDatabaseServer.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabaseLoginPassword;Encrypt=true;Trusted_Connection=false;"
        $conn.open()
        $cmd = New-Object System.Data.SqlClient.SqlCommand
        $cmd.connection = $conn
        $cmd.commandtext = $cmdCreateLog4jCountTable
        $cmd.executenonquery()

        $conn.close()
    }

    # upload workflow.xml, coordinator.xml, and ooziewf.hql
    uploadOozieFiles;

    # make a copy of example/data/sample.log tooexample/data/log4j/sample.log
    prepareHiveDataFile;

    # create log4jlogsCount table on SQL database
    prepareSQLDatabase;
    ```

5. 按一下**執行指令碼**或按**F5** toorun hello 指令碼。 hello 輸出將會類似於：

    ![Tutorial preparation output][img-preparation-output]

## <a name="run-hello-oozie-project"></a>執行 hello Oozie 專案
Azure PowerShell 目前並未提供任何用以定義 Oozie 工作的 Cmdlet。 您可以使用 hello **Invoke-restmethod** cmdlet tooinvoke Oozie web 服務。 hello Oozie web 服務應用程式開發介面是 HTTP REST JSON API。 如需 hello Oozie web 服務應用程式開發介面的詳細資訊，請參閱[Apache Oozie 4.0 版文件][ apache-oozie-400] （適用於 HDInsight 叢集版本 3.0） 或[Apache Oozie 3.3.2 文件] [ apache-oozie-332] （適用於 HDInsight 叢集版本 2.1）。

**toosubmit Oozie 工作**

1. 開啟 hello Windows PowerShell ISE (在 Windows 8 [開始] 畫面中，輸入**PowerShell_ISE**，然後按一下 **Windows PowerShell ISE**。 如需詳細資訊，請參閱[在 Windows 8 和 Windows 上啟動 Windows PowerShell][powershell-start])。
2. 複製 hello 下列指令碼到 hello 指令碼窗格中，並設定然後 hello 先 14 個變數 (不過，請略過**$storageUri**)。

    ```powershell
    #HDInsight cluster variables
    $clusterName = "<HDInsightClusterName>"
    $clusterUsername = "<HDInsightClusterUsername>"
    $clusterPassword = "<HDInsightClusterUserPassword>"

    #Azure Blob storage (WASB) variables
    $storageAccountName = "<StorageAccountName>"
    $storageContainerName = "<BlobContainerName>"
    $storageUri="wasb://$storageContainerName@$storageAccountName.blob.core.windows.net"

    #Azure SQL database variables
    $sqlDatabaseServer = "<SQLDatabaseServerName>"
    $sqlDatabaseLogin = "<SQLDatabaseLoginName>"
    $sqlDatabaseLoginPassword = "<SQLDatabaseloginPassword>"
    $sqlDatabaseName = "<SQLDatabaseName>"

    #Oozie WF/coordinator variables
    $coordStart = "2014-03-21T13:45Z"
    $coordEnd = "2014-03-21T13:45Z"
    $coordFrequency = "1440"    # in minutes, 24h x 60m = 1440m
    $coordTimezone = "UTC"    #UTC/GMT

    $oozieWFPath="$storageUri/tutorials/useoozie"  # hello default name is workflow.xml. And you don't need toospecify hello file name.
    $waitTimeBetweenOozieJobStatusCheck=10

    #Hive action variables
    $hiveScript = "$storageUri/tutorials/useoozie/useooziewf.hql"
    $hiveTableName = "log4jlogs"
    $hiveDataFolder = "$storageUri/tutorials/useoozie/data"
    $hiveOutputFolder = "$storageUri/tutorials/useoozie/output"

    #Sqoop action variables
    $sqlDatabaseConnectionString = "jdbc:sqlserver://$sqlDatabaseServer.database.windows.net;user=$sqlDatabaseLogin@$sqlDatabaseServer;password=$sqlDatabaseLoginPassword;database=$sqlDatabaseName"
    $sqlDatabaseTableName = "log4jLogsCount"

    $passwd = ConvertTo-SecureString $clusterPassword -AsPlainText -Force
    $creds = New-Object System.Management.Automation.PSCredential ($clusterUsername, $passwd)
    ```

    如需 hello 變數的詳細描述，請參閱 hello[必要條件](#prerequisites)在本教學課程 > 一節。

    $coordstart 和 $coordend 是 hello 工作流程開始和結束時間。 toofind hello UTC/GMT 時間，搜尋 bing.com 的 「 utc 時間 」。hello $coordFrequency 頻率為您想要讓 toorun hello 流程分鐘。
3. 附加 hello 遵循 toohello 指令碼。 此組件定義 hello Oozie 裝載：

    ```powershell
    #OoziePayload used for Oozie web service submission
    $OoziePayload =  @"
    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>

        <property>
            <name>nameNode</name>
            <value>$storageUrI</value>
        </property>

        <property>
            <name>jobTracker</name>
            <value>jobtrackerhost:9010</value>
        </property>

        <property>
            <name>queueName</name>
            <value>default</value>
        </property>

        <property>
            <name>oozie.use.system.libpath</name>
            <value>true</value>
        </property>

        <property>
            <name>oozie.coord.application.path</name>
            <value>$oozieWFPath</value>
        </property>

        <property>
            <name>wfPath</name>
            <value>$oozieWFPath</value>
        </property>

        <property>
            <name>coordStart</name>
            <value>$coordStart</value>
        </property>

        <property>
            <name>coordEnd</name>
            <value>$coordEnd</value>
        </property>

        <property>
            <name>coordFrequency</name>
            <value>$coordFrequency</value>
        </property>

        <property>
            <name>coordTimezone</name>
            <value>$coordTimezone</value>
        </property>

        <property>
            <name>hiveScript</name>
            <value>$hiveScript</value>
        </property>

        <property>
            <name>hiveTableName</name>
            <value>$hiveTableName</value>
        </property>

        <property>
            <name>hiveDataFolder</name>
            <value>$hiveDataFolder</value>
        </property>

        <property>
            <name>hiveOutputFolder</name>
            <value>$hiveOutputFolder</value>
        </property>

        <property>
            <name>sqlDatabaseConnectionString</name>
            <value>&quot;$sqlDatabaseConnectionString&quot;</value>
        </property>

        <property>
            <name>sqlDatabaseTableName</name>
            <value>$SQLDatabaseTableName</value>
        </property>

        <property>
            <name>user.name</name>
            <value>admin</value>
        </property>

    </configuration>
    "@
    ```

   > [!NOTE]
   > hello 主要的差異比較 toohello 工作流程提交裝載檔案是 hello 變數**oozie.coord.application.path**。 提交工作流程工作時，您必須改用 **oozie.wf.application.path** 。

4. 附加 hello 遵循 toohello 指令碼。 此組件會檢查 hello Oozie web 服務狀態：

    ```powershell
    function checkOozieServerStatus()
    {
        Write-Host "Checking Oozie server status..." -ForegroundColor Green
        $clusterUriStatus = "https://$clusterName.azurehdinsight.net:443/oozie/v2/admin/status"
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriStatus -Credential $creds -OutVariable $OozieServerStatus

        $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
        $oozieServerSatus = $jsonResponse[0].("systemMode")
        Write-Host "Oozie server status is $oozieServerSatus..."

        if($oozieServerSatus -notmatch "NORMAL")
        {
            Write-Host "Oozie server status is $oozieServerSatus...cannot submit Oozie jobs. Check hello server status and re-run hello job."
            exit 1
        }
    }
    ```

5. 附加 hello 遵循 toohello 指令碼。 這部分會建立 Oozie 工作：

    ```powershell
    function createOozieJob()
    {
        # create Oozie job
        Write-Host "Sending hello following Payload toohello cluster:" -ForegroundColor Green
        Write-Host "`n--------`n$OoziePayload`n--------"
        $clusterUriCreateJob = "https://$clusterName.azurehdinsight.net:443/oozie/v2/jobs"
        $response = Invoke-RestMethod -Method Post -Uri $clusterUriCreateJob -Credential $creds -Body $OoziePayload -ContentType "application/xml" -OutVariable $OozieJobName -debug -Verbose

        $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
        $oozieJobId = $jsonResponse[0].("id")
        Write-Host "Oozie job id is $oozieJobId..."

        return $oozieJobId
    }
    ```

   > [!NOTE]
   > 當您提交的工作流程工作時，您必須在 hello 工作建立之後，進行另一個 web 服務呼叫 toostart hello 工作。 在此情況下，依時間觸發 hello 協調器工作。 hello 作業將自動啟動。

6. 附加 hello 遵循 toohello 指令碼。 此組件會檢查 hello Oozie 工作狀態：

    ```powershell
    function checkOozieJobStatus($oozieJobId)
    {
        # get job status
        Write-Host "Sleeping for $waitTimeBetweenOozieJobStatusCheck seconds until hello job metadata is populated in hello Oozie metastore..." -ForegroundColor Green
        Start-Sleep -Seconds $waitTimeBetweenOozieJobStatusCheck

        Write-Host "Getting job status and waiting for hello job toocomplete..." -ForegroundColor Green
        $clusterUriGetJobStatus = "https://$clusterName.azurehdinsight.net:443/oozie/v2/job/" + $oozieJobId + "?show=info"
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriGetJobStatus -Credential $creds
        $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
        $JobStatus = $jsonResponse[0].("status")

        while($JobStatus -notmatch "SUCCEEDED|KILLED")
        {
            Write-Host "$(Get-Date -format 'G'): $oozieJobId is in $JobStatus state...waiting $waitTimeBetweenOozieJobStatusCheck seconds for hello job toocomplete..."
            Start-Sleep -Seconds $waitTimeBetweenOozieJobStatusCheck
            $response = Invoke-RestMethod -Method Get -Uri $clusterUriGetJobStatus -Credential $creds
            $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
            $JobStatus = $jsonResponse[0].("status")
        }

        Write-Host "$(Get-Date -format 'G'): $oozieJobId is in $JobStatus state!"
        if($JobStatus -notmatch "SUCCEEDED")
        {
            Write-Host "Check logs at http://headnode0:9014/cluster for detais."
            exit -1
        }
    }
    ```

7. （選擇性）附加 hello 遵循 toohello 指令碼。

    ```powershell
    function listOozieJobs()
    {
        Write-Host "Listing Oozie jobs..." -ForegroundColor Green
        $clusterUriStatus = "https://$clusterName.azurehdinsight.net:443/oozie/v2/jobs"
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriStatus -Credential $creds

        write-host "Job ID                                   App Name        Status      Started                         Ended"
        write-host "----------------------------------------------------------------------------------------------------------------------------------"
        foreach($job in $response.workflows)
        {
            Write-Host $job.id "`t" $job.appName "`t" $job.status "`t" $job.startTime "`t" $job.endTime
        }
    }

    function ShowOozieJobLog($oozieJobId)
    {
        Write-Host "Showing Oozie job info..." -ForegroundColor Green
        $clusterUriStatus = "https://$clusterName.azurehdinsight.net:443/oozie/v2/job/$oozieJobId" + "?show=log"
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriStatus -Credential $creds
        write-host $response
    }

    function killOozieJob($oozieJobId)
    {
        Write-Host "Killing hello Oozie job $oozieJobId..." -ForegroundColor Green
        $clusterUriStartJob = "https://$clusterName.azurehdinsight.net:443/oozie/v2/job/" + $oozieJobId + "?action=kill" #Valid values for hello 'action' parameter are 'start', 'suspend', 'resume', 'kill', 'dryrun', 'rerun', and 'change'.
        $response = Invoke-RestMethod -Method Put -Uri $clusterUriStartJob -Credential $creds | Format-Table -HideTableHeaders -debug
    }
    ```

8. 附加 hello 遵循 toohello 指令碼：

    ```powershell
    checkOozieServerStatus
    # listOozieJobs
    $oozieJobId = createOozieJob($oozieJobId)
    checkOozieJobStatus($oozieJobId)
    # ShowOozieJobLog($oozieJobId)
    # killOozieJob($oozieJobId)
    ```

    如果您想 toorun hello 其他函式，請移除 hello # 符號。
9. 如果您的 HDinsight 叢集是 2.1 版，請將 "https://$clusterName.azurehdinsight.net:443/oozie/v2/" 取代為 "https://$clusterName.azurehdinsight.net:443/oozie/v1/"。 HDInsight 叢集版本 2.1 並不支援第 2 版的 hello web 服務。
10. 按一下**執行指令碼**或按**F5** toorun hello 指令碼。 hello 輸出將會類似於：

     ![Tutorial run workflow output][img-runworkflow-output]
11. 連接 tooyour SQL Database toosee hello 匯出資料。

**toocheck hello 作業錯誤記錄檔**

tootroubleshoot 工作流程，hello Oozie 記錄檔可以在找到 C:\apps\dist\oozie-3.3.2.1.3.2.0-05\oozie-win-distro\logs\Oozie.log 從 hello 叢集前端節點。 如需 RDP 資訊，請參閱[管理 HDInsight 叢集使用 hello Azure 入口網站][hdinsight-admin-portal]。

**toorerun hello 教學課程**

toorerun hello 工作流程，您必須執行下列工作的 hello:

* 刪除 hello Hive 指令碼輸出檔。
* 刪除 hello hello log4jLogsCount 資料表中的資料。

以下是您可使用的範例 Windows PowerShell 指令碼：

```powershell
$storageAccountName = "<AzureStorageAccountName>"
$containerName = "<ContainerName>"

#SQL database variables
$sqlDatabaseServer = "<SQLDatabaseServerName>"
$sqlDatabaseLogin = "<SQLDatabaseLoginName>"
$sqlDatabaseLoginPassword = "<SQLDatabaseLoginPassword>"
$sqlDatabaseName = "<SQLDatabaseName>"
$sqlDatabaseTableName = "log4jLogsCount"

Write-host "Delete hello Hive script output file ..." -ForegroundColor Green
$storageaccountkey = get-azurestoragekey $storageAccountName | %{$_.Primary}
$destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageaccountkey
Remove-AzureStorageBlob -Context $destContext -Blob "tutorials/useoozie/output/000000_0" -Container $containerName

Write-host "Delete all hello records from hello log4jLogsCount table ..." -ForegroundColor Green
$conn = New-Object System.Data.SqlClient.SqlConnection
$conn.ConnectionString = "Data Source=$sqlDatabaseServer.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabaseLoginPassword;Encrypt=true;Trusted_Connection=false;"
$conn.open()
$cmd = New-Object System.Data.SqlClient.SqlCommand
$cmd.connection = $conn
$cmd.commandtext = "delete from $sqlDatabaseTableName"
$cmd.executenonquery()

$conn.close()
```

## <a name="next-steps"></a>後續步驟
在本教學課程中，您學到如何 toodefine Oozie 工作流程和 Oozie 協調器，以及使用 Azure PowerShell toorun Oozie 協調者作業的方式。 toolearn 詳細資訊，請參閱下列文章 hello:

* [開始使用 HDInsight][hdinsight-get-started]
* [搭配 HDInsight 使用 Azure Blob 儲存體][hdinsight-storage]
* [使用 Azure PowerShell 管理 HDInsight][hdinsight-admin-powershell]
* [上傳資料 tooHDInsight][hdinsight-upload-data]
* [搭配 HDInsight 使用 Sqoop][hdinsight-use-sqoop]
* [搭配 HDInsight 使用 Hivet][hdinsight-use-hive]
* [搭配 HDInsight 使用 Pig][hdinsight-use-pig]
* [開發 HDInsight 的 Java MapReduce 程式][hdinsight-develop-java-mapreduce]

[hdinsight-cmdlets-download]: http://go.microsoft.com/fwlink/?LinkID=325563

[hdinsight-versions]:  hdinsight-component-versioning.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md

[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-develop-java-mapreduce]: hdinsight-develop-deploy-java-mapreduce-linux.md
[hdinsight-use-oozie]: hdinsight-use-oozie.md

[sqldatabase-get-started]: ../sql-database/sql-database-get-started.md

[azure-management-portal]: https://portal.azure.com/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md

[apache-hadoop]: http://hadoop.apache.org/
[apache-oozie-400]: http://oozie.apache.org/docs/4.0.0/
[apache-oozie-332]: http://oozie.apache.org/docs/3.3.2/

[powershell-download]: http://azure.microsoft.com/downloads/
[powershell-about-profiles]: http://go.microsoft.com/fwlink/?LinkID=113729
[powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx
[powershell-script]: http://technet.microsoft.com/library/ee176949.aspx

[cindygross-hive-tables]: http://blogs.msdn.com/b/cindygross/archive/2013/02/06/hdinsight-hive-internal-and-external-tables-intro.aspx

[img-workflow-diagram]: ./media/hdinsight-use-oozie-coordinator-time/HDI.UseOozie.Workflow.Diagram.png
[img-preparation-output]: ./media/hdinsight-use-oozie-coordinator-time/HDI.UseOozie.Preparation.Output1.png
[img-runworkflow-output]: ./media/hdinsight-use-oozie-coordinator-time/HDI.UseOozie.RunCoord.Output.png

[technetwiki-hive-error]: http://social.technet.microsoft.com/wiki/contents/articles/23047.hdinsight-hive-error-unable-to-rename.aspx
