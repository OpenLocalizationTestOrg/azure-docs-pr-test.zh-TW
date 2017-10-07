---
title: "aaaRun Hadoop 作業使用 Azure Cosmos DB 和 HDInsight |Microsoft 文件"
description: "了解 toorun 簡單 Hive、 Pig 和 MapReduce 如何與 Azure Cosmos DB Azure HDInsight 工作。"
services: cosmos-db
author: dennyglee
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: 06f0ea9d-07cb-4593-a9c5-ab912b62ac42
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 06/08/2017
ms.author: denlee
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2e27499f2c4ba951af9a1ade1bcc9c1b6d298fcd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="Azure Cosmos DB-HDInsight"></a>使用 Azure Cosmos DB 和 HDInsight 執行 Apache Hive、Pig 或 Hadoop 作業
本教學課程示範如何 toorun [Apache Hive][apache-hive]， [Apache Pig][apache-pig]，和[Apache Hadoop] [apache-hadoop] Cosmos DB Hadoop 連接器與 Azure HDInsight 上的 MapReduce 工作。 Cosmos DB 的 Hadoop 連接器可讓您為來源和接收器 Hive、 Pig 和 MapReduce 工作的 Cosmos DB tooact。 本教學課程將使用 Cosmos DB 作為 hello 資料來源和目的地 Hadoop 工作。

完成本教學課程之後，您會無法 tooanswer hello 下列問題：

* 如何使用 Hive、Pig 或 MapReduce 作業從 Cosmos DB 載入資料？
* 如何使用 Hive、Pig 或 MapReduce 作業在 Cosmos DB 中儲存資料？

我們建議您藉由監看下列影片，我們透過使用 Cosmos DB 與 HDInsight Hive 工作執行所在的 hello 開始使用。

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Use-Azure-DocumentDB-Hadoop-Connector-with-Azure-HDInsight/player]
>
>

然後，傳回 toothis 發行項，您會在此收到 hello 上如何的 Cosmos DB 資料執行分析工作的完整詳細資料。

> [!TIP]
> 本教學課程假設您先前已有使用 Apache Hadoop、Hive 和/或 Pig 的經驗。 如果您是新 tooApache Hadoop、 Hive 和 Pig，我們建議您造訪 hello [Apache Hadoop 文件][apache-hadoop-doc]。 本教學課程也假設您先前已有使用 Cosmos DB 的經驗，且擁有 Cosmos DB 帳戶。 如果您是新 tooCosmos DB，或是您沒有 Cosmos DB 帳戶，請查看我們[入門][ getting-started]頁面。
>
>

沒有時間 toocomplete hello 教學課程和 Hive、 Pig 和 MapReduce 只要 tooget hello 完整的範例 PowerShell 指令碼嗎？ 沒問題，您可以在[這裡][hdinsight-samples]取得。 hello 下載也包含對這些範例的 hello hql、 pig 和 java 檔案。

## <a name="NewestVersion"></a>最新版本
<table border='1'>
    <tr><th>Hadoop 連接器版本</th>
        <td>1.2.0</td></tr>
    <tr><th>指令碼 URI</th>
        <td>https://portalcontent.blob.core.windows.net/scriptaction/documentdb-hadoop-installer-v04.ps1</td></tr>
    <tr><th>修改日期</th>
        <td>2016 年 4 月 26 日</td></tr>
    <tr><th>支援的 HDInsight 版本</th>
        <td>3.1、3.2</td></tr>
    <tr><th>變更記錄檔</th>
        <td>更新 Azure Cosmos DB Java SDK too1.6.0</br>
            將已分割的集合支援同時加入為來源和接收</br>
        </td></tr>
</table>

## <a name="Prerequisites"></a>必要條件
之前遵循 hello 指示在本教學課程，請確定您擁有 hello 下列：

* Cosmos DB 帳戶、資料庫和包含文件的集合。 如需詳細資訊，請參閱[開始使用 Azure Cosmos DB][getting-started]。 範例資料匯入您的 Cosmos DB 帳戶以 hello [Cosmos DB 匯入工具][import-data]。
* 輸送量。 從 HDInsight 讀取和寫入將會計入您的集合的配置要求單位。
* 每個輸出集合額內額外預存程序的容量。 hello 預存程序可用來傳送產生的文件。
* 產生的文件 hello hello Hive、 Pig 或 MapReduce 工作的容量。
* [*選擇性*] 額外集合的容量。

> [!WARNING]
> 順序 tooavoid hello 建立新的集合，在任何 hello 工作期間，您可以列印 hello 結果 toostdout、 儲存 hello 輸出 tooyour WASB 容器，或指定現有的集合。 在指定的現有集合的 hello 情況下，會建立新文件 hello 集合內的與中的衝突時，只會影響現有的文件*識別碼*。 **hello 連接器將會自動覆寫現有的文件識別碼衝突**。 您可以藉由設定 hello upsert 選項 toofalse 來關閉這項功能。 如果 upsert 為 false，就會發生衝突，hello Hadoop 工作將會失敗。報告發生 id 衝突錯誤。
>
>

## <a name="ProvisionHDInsight"></a>步驟 1︰建立新的 HDInsight 叢集
本教學課程會使用指令碼動作 hello Azure 入口網站 toocustomize 從您的 HDInsight 叢集。 在本教學課程中，我們將使用 hello Azure 入口網站 toocreate 您的 HDInsight 叢集。 如需有關如何 toouse PowerShell cmdlet 或 hello HDInsight.NET SDK，請參閱指示[自訂 HDInsight 叢集使用指令碼動作][ hdinsight-custom-provision]發行項。

1. 登入 toohello [Azure 入口網站][azure-portal]。
2. 按一下**+ 新增**hello hello 左瀏覽頂端，在搜尋**HDInsight** hello 新刀鋒視窗上的 hello 頂端搜尋列中。
3. **HDInsight**所發行**Microsoft**頂端 hello hello 結果會出現。 對它按一下，然後按一下 [建立] 。
4. Hello 新的 HDInsight 叢集上建立刀鋒視窗中，輸入您**叢集名稱**和選取 hello**訂用帳戶**tooprovision 您想在此資源。

    <table border='1'>
        <tr><td>叢集名稱</td><td>名稱 hello 叢集。<br/>
DNS 名稱的開頭與結尾都必須是英數字元，且可包含連字號。<br/>
hello 欄位必須是介於 3 到 63 個字元之間的字串。</td></tr>
        <tr><td>訂用帳戶名稱</td>
            <td>如果您有多個 Azure 訂用帳戶，請選取 hello 訂用帳戶裝載 HDInsight 叢集。 </td></tr>
    </table>
5.按一下**選取叢集類型**和下列屬性 toohello 組 hello 指定值。

    <table border='1'>
        <tr><td>叢集類型</td><td><strong>Hadoop</strong></td></tr>
        <tr><td>叢集層</td><td><strong>標準</strong></td></tr>
        <tr><td>作業系統</td><td><strong>Windows</strong></td></tr>
        <tr><td>版本</td><td>最新版本</td></tr>
    </table>

    現在，按一下 [選取] 。

    ![提供 Hadoop HDInsight 初始叢集詳細資料][image-customprovision-page1]
6. 按一下**認證**tooset 您登入及遠端存取認證。 選擇 [叢集登入使用者名稱] 和 [叢集登入密碼]。

    如果您想 tooremote 到您的叢集，請選取*是*在 hello hello 刀鋒視窗的底部，並提供使用者名稱和密碼。
7. 按一下**資料來源**tooset 您主要資料的位置存取。 選擇 hello**選取方法**並指定現有的儲存體帳戶或另外新建一個。
8. 在 hello 相同刀鋒視窗中，指定**預設容器**和**位置**。 然後，按一下 [選取] 。

   > [!NOTE]
   > 選取位置關閉 tooyour Cosmos DB 帳戶區域，以提升效能
   >
   >
9. 按一下**定價**tooselect hello 的節點數目和類型。 稍後可以保留 hello 預設組態及背景工作節點的小數位數 hello 數。
10. 按一下**選擇性組態**，然後**指令碼動作**hello 選擇性組態刀鋒視窗中。

     在指令碼動作] 中，輸入下列資訊 toocustomize hello 您的 HDInsight 叢集。

     <table border='1'>
         <tr><th>屬性</th><th>值</th></tr>
         <tr><td>名稱</td>
             <td>指定 hello 指令碼動作的名稱。</td></tr>
         <tr><td>指令碼 URI</td>
             <td>指定 hello URI toohello 指令碼會叫用的 toocustomize hello 叢集。</br></br>
請輸入： </br> <strong>https://portalcontent.blob.core.windows.net/scriptaction/documentdb-hadoop-installer-v04.ps1</strong>.</td></tr>
         <tr><td>前端</td>
             <td>按一下 [hello] 核取方塊 toorun hello hello 前端節點上的 PowerShell 指令碼。</br></br>
             <strong>勾選此核取方塊</strong>。</td></tr>
         <tr><td>背景工作</td>
             <td>按一下 [hello] 核取方塊 toorun hello PowerShell 指令碼到 hello 背景工作節點上。</br></br>
             <strong>勾選此核取方塊</strong>。</td></tr>
         <tr><td>Zookeeper</td>
             <td>按一下 [hello] 核取方塊 toorun hello PowerShell 指令碼到 hello 動物園管理員。</br></br>
             <strong>不需要</strong>。
             </td></tr>
         <tr><td>參數</td>
             <td>指定 hello 參數，如果 hello 指令碼所需。</br></br>
             <strong>不需要參數</strong>。</td></tr>
     </table>
11. 建立新的**資源群組**或使用 Azure 訂用帳戶下的現有資源群組。
12. 現在，檢查**Pin toodashboard** tootrack 其部署和按一下**建立**！

## <a name="InstallCmdlets"></a>步驟 2：安裝並設定 Azure PowerShell
1. 安裝 Azure PowerShell。 您可以在[這裡][powershell-install-configure]找到指示。

   > [!NOTE]
   > 或者，您可以使用 HDInsight 的線上 Hive 編輯器 (僅限 Hive 查詢)。 toodo，登入 toohello [Azure 入口網站][azure-portal]，按一下 [ **HDInsight**在 hello 左的窗格 tooview 一份您的 HDInsight 叢集。 按一下您想 toorun Hive 查詢，然後再按一下 hello 叢集**查詢主控台**。
   >
   >
2. 開啟 Azure PowerShell 整合式指令碼環境的 hello:

   * 在執行 Windows 8 或 Windows Server 2012 或以上版本的電腦，您可以使用 hello 內建搜尋。 從 hello [開始] 畫面，輸入**powershell ise**按一下**Enter**。
   * 在執行版本早於 Windows 8 或 Windows Server 2012 的電腦，使用 hello [開始] 功能表。 從 hello [開始] 功能表中，輸入**命令提示字元**hello 搜尋方塊中，然後在 [hello 結果清單中，按一下**命令提示字元**。 在 [hello 命令提示字元，輸入**powershell_ise**按一下**Enter**。
3. 新增您的 Azure 帳戶。

   1. 在 [hello 主控台窗格中，輸入**Add-azureaccount**按一下**Enter**。
   2. 輸入您 Azure 訂用帳戶相關聯的 hello 電子郵件地址，然後按一下**繼續**。
   3. 輸入 hello Azure 訂用帳戶的密碼。
   4. 按一下 [ **登入**]。
4. 下列圖表中的 hello 識別您的 Azure PowerShell 指令碼環境的 hello 重要部分。

    ![Azure PowerShell 的圖表][azure-powershell-diagram]

## <a name="RunHive"></a>步驟 3：使用 Cosmos DB 和 HDInsight 執行 Hive 作業
> [!IMPORTANT]
> 以 < > 表示的所有變數都必須使用組態設定進行填寫。
>
>

1. 下列 PowerShell 指令碼窗格中的變數集 hello。

        # Provide Azure subscription name, hello Azure Storage account and container that is used for hello default HDInsight file system.
        $subscriptionName = "<SubscriptionName>"
        $storageAccountName = "<AzureStorageAccountName>"
        $containerName = "<AzureStorageContainerName>"

        # Provide hello HDInsight cluster name where you want toorun hello Hive job.
        $clusterName = "<HDInsightClusterName>"
2. <p>首先我們要建構查詢字串。 我們會撰寫 Hive 查詢會接受所有文件產生的系統時間戳記 (_ts) 和 Azure Cosmos DB 集合中的唯一識別碼 (_rid)、 計算所有文件以 hello 分鐘，然後儲存 hello 結果回新的 Azure Cosmos DB 集合。</p>

    <p>首先，我們要在 Azure Cosmos DB 集合中建立 Hive 資料表。 新增下列程式碼片段 toohello PowerShell 指令碼窗格中的 hello<strong>之後</strong>hello # 1 的程式碼片段。 請確定您包含 hello 選擇性 DocumentDB.query 參數 t 修剪我們的文件 toojust _ts 和 _rid。</p>

   > [!NOTE]
   > **命名 DocumentDB.inputCollections 是正確的選擇。** 沒錯，我們允許在一筆輸入中加入多個集合： </br>
   >
   >

        '*DocumentDB.inputCollections*' = '*\<DocumentDB Input Collection Name 1\>*,*\<DocumentDB Input Collection Name 2\>*' A1A</br> hello collection names are separated without spaces, using only a single comma.

        # Create a Hive table using data from DocumentDB. Pass DocumentDB hello query toofilter transferred data too_rid and _ts.
        $queryStringPart1 = "drop table DocumentDB_timestamps; "  +
                            "create external table DocumentDB_timestamps(id string, ts BIGINT) "  +
                            "stored by 'com.microsoft.azure.documentdb.hive.DocumentDBStorageHandler' "  +
                            "tblproperties ( " +
                                "'DocumentDB.endpoint' = '<DocumentDB Endpoint>', " +
                                "'DocumentDB.key' = '<DocumentDB Primary Key>', " +
                                "'DocumentDB.db' = '<DocumentDB Database Name>', " +
                                "'DocumentDB.inputCollections' = '<DocumentDB Input Collection Name>', " +
                                "'DocumentDB.query' = 'SELECT r._rid AS id, r._ts AS ts FROM root r' ); "

1. 接下來，讓我們來建立 hello 輸出集合的 Hive 資料表。 hello 輸出文件屬性將 hello 月、 日、 時、 分、 hello 總次數。

   > [!NOTE]
   > **再重申一次，命名 DocumentDB.outputCollections 是正確的選擇。** 沒錯，我們允許在一筆輸出中加入多個集合： </br>
   > '*DocumentDB.outputCollections*' = '*\<DocumentDB 輸出集合名稱 1\>*,*\<DocumentDB 輸出集合名稱 2\>*' </br> hello 集合名稱不含空格，使用單一逗號分隔。 </br></br>
   > 文件將會是跨多個集合的分散式循環配置資源。 批次的文件會儲存在一個集合，然後第二個批次的文件會儲存在 hello 下一次回收，依此類推。
   >
   >

       # Create a Hive table for hello output data tooDocumentDB.
       $queryStringPart2 = "drop table DocumentDB_analytics; " +
                             "create external table DocumentDB_analytics(Month INT, Day INT, Hour INT, Minute INT, Total INT) " +
                             "stored by 'com.microsoft.azure.documentdb.hive.DocumentDBStorageHandler' " +
                             "tblproperties ( " +
                                 "'DocumentDB.endpoint' = '<DocumentDB Endpoint>', " +
                                 "'DocumentDB.key' = '<DocumentDB Primary Key>', " +  
                                 "'DocumentDB.db' = '<DocumentDB Database Name>', " +
                                 "'DocumentDB.outputCollections' = '<DocumentDB Output Collection Name>' ); "
2. 最後，讓我們依月、 日、 小時和分鐘，而且插入 hello 結果回 hello 票數 hello 文件輸出 Hive 資料表。

        # GROUP BY minute, COUNT entries for each, INSERT INTO output Hive table.
        $queryStringPart3 = "INSERT INTO table DocumentDB_analytics " +
                              "SELECT month(from_unixtime(ts)) as Month, day(from_unixtime(ts)) as Day, " +
                              "hour(from_unixtime(ts)) as Hour, minute(from_unixtime(ts)) as Minute, " +
                              "COUNT(*) AS Total " +
                              "FROM DocumentDB_timestamps " +
                              "GROUP BY month(from_unixtime(ts)), day(from_unixtime(ts)), " +
                              "hour(from_unixtime(ts)) , minute(from_unixtime(ts)); "
3. 新增 hello hello 上一個查詢中的下列指令碼程式碼片段 toocreate Hive 工作定義。

        # Create a Hive job definition.
        $queryString = $queryStringPart1 + $queryStringPart2 + $queryStringPart3
        $hiveJobDefinition = New-AzureHDInsightHiveJobDefinition -Query $queryString

    您也可以使用 hello-檔案切換 toospecify HDFS 上的下列 HiveQL 指令碼檔案。
4. 新增下列程式碼片段 toosave hello 開始時間的 hello 和送出 hello Hive 工作。

        # Save hello start time and submit hello job toohello cluster.
        $startTime = Get-Date
        Select-AzureSubscription $subscriptionName
        $hiveJob = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $hiveJobDefinition
5. 新增下列 hello Hive 工作 toocomplete 的 toowait hello。

        # Wait for hello Hive job toocomplete.
        Wait-AzureHDInsightJob -Job $hiveJob -WaitTimeoutInSeconds 3600
6. 新增 hello 遵循 tooprint hello 標準輸出和 hello 開始和結束時間。

        # Print hello standard error, hello standard output of hello Hive job, and hello start and end time.
        $endTime = Get-Date
        Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $hiveJob.JobId -StandardOutput
        Write-Host "Start: " $startTime ", End: " $endTime -ForegroundColor Green
7. **執行** 新的指令碼！ **按一下**hello 綠色執行] 按鈕。
8. 檢查 hello 結果。 登入 hello [Azure 入口網站][azure-portal]。

   1. 按一下<strong>瀏覽</strong>hello 左側面板上。 </br>
   2. 按一下<strong>一切</strong>在 hello 的右上方 hello 瀏覽面板。 </br>
   3. 尋找並按一下 [Azure Cosmos DB 帳戶]<strong></strong>。 </br>
   4. 接下來，尋找您<strong>Azure Cosmos DB 帳戶</strong>，然後<strong>Azure Cosmos DB Database</strong>和您<strong>Azure Cosmos DB 集合</strong>hello 輸出集合中指定相關聯Hive 查詢。</br>
   5. 最後，按一下 [<strong>開發人員工具</strong>] 底下的 <strong>Document Explorer</strong>。</br></p>

   您會看到 hello 的 Hive 查詢的結果。

   ![Hive 查詢結果][image-hive-query-results]

## <a name="RunPig"></a>步驟 4：使用 Cosmos DB 和 HDInsight 執行 Pig 作業
> [!IMPORTANT]
> 以 < > 表示的所有變數都必須使用組態設定進行填寫。
>
>

1. 下列 PowerShell 指令碼窗格中的變數集 hello。

        # Provide Azure subscription name.
        $subscriptionName = "Azure Subscription Name"

        # Provide HDInsight cluster name where you want toorun hello Pig job.
        $clusterName = "Azure HDInsight Cluster Name"
2. <p>首先我們要建構查詢字串。 我們會撰寫 Pig 查詢會接受所有文件產生的系統時間戳記 (_ts) 和 Azure Cosmos DB 集合中的唯一識別碼 (_rid)、 計算所有文件以 hello 分鐘，然後儲存 hello 結果回新的 Azure Cosmos DB 集合。</p>
    <p>首先，將文件從 Cosmos DB 載入 HDInsight。 新增下列程式碼片段 toohello PowerShell 指令碼窗格中的 hello<strong>之後</strong>hello # 1 的程式碼片段。 請確定 tooadd DocumentDB 查詢 toohello 選擇性 DocumentDB 查詢參數 tootrim，我們的文件 toojust _ts 和 _rid。</p>

   > [!NOTE]
   > 沒錯，我們允許在一筆輸入中加入多個集合： </br>
   > '*\<DocumentDB 輸入集合名稱 1\>*,*\<DocumentDB 輸入集合名稱 2\>*'</br> hello 集合名稱不含空格，使用單一逗號分隔。 </b>
   >
   >

    文件將會是跨多個集合的分散式循環配置資源。 批次的文件會儲存在一個集合，然後第二個批次的文件會儲存在 hello 下一次回收，依此類推。

        # Load data from Cosmos DB. Pass DocumentDB query toofilter transferred data too_rid and _ts.
        $queryStringPart1 = "DocumentDB_timestamps = LOAD '<DocumentDB Endpoint>' USING com.microsoft.azure.documentdb.pig.DocumentDBLoader( " +
                                                        "'<DocumentDB Primary Key>', " +
                                                        "'<DocumentDB Database Name>', " +
                                                        "'<DocumentDB Input Collection Name>', " +
                                                        "'SELECT r._rid AS id, r._ts AS ts FROM root r' ); "
3. 接下來，讓我們清點 hello 文件的 hello 月、 日、 時、 分、 hello 總次數。

       # GROUP BY minute and COUNT entries for each.
       $queryStringPart2 = "timestamp_record = FOREACH DocumentDB_timestamps GENERATE `$0#'id' as id:int, ToDate((long)(`$0#'ts') * 1000) as timestamp:datetime; " +
                           "by_minute = GROUP timestamp_record BY (GetYear(timestamp), GetMonth(timestamp), GetDay(timestamp), GetHour(timestamp), GetMinute(timestamp)); " +
                           "by_minute_count = FOREACH by_minute GENERATE FLATTEN(group) as (Year:int, Month:int, Day:int, Hour:int, Minute:int), COUNT(timestamp_record) as Total:int; "
4. 最後，讓我們 hello 結果儲存至新輸出集合。

   > [!NOTE]
   > 沒錯，我們允許在一筆輸出中加入多個集合： </br>
   > '\<DocumentDB 輸出集合名稱 1\>,\<DocumentDB 輸出集合名稱 2\>'</br> hello 集合名稱不含空格，使用單一逗號分隔。</br>
   > 文件將會是分散式的循環配置資源的 hello 多個集合。 批次的文件會儲存在一個集合，然後第二個批次的文件會儲存在 hello 下一次回收，依此類推。
   >
   >

        # Store output data tooCosmos DB.
        $queryStringPart3 = "STORE by_minute_count INTO '<DocumentDB Endpoint>' " +
                            "USING com.microsoft.azure.documentdb.pig.DocumentDBStorage( " +
                                "'<DocumentDB Primary Key>', " +
                                "'<DocumentDB Database Name>', " +
                                "'<DocumentDB Output Collection Name>'); "
5. 新增 hello hello 上一個查詢中的下列指令碼程式碼片段 toocreate Pig 工作定義。

        # Create a Pig job definition.
        $queryString = $queryStringPart1 + $queryStringPart2 + $queryStringPart3
        $pigJobDefinition = New-AzureHDInsightPigJobDefinition -Query $queryString -StatusFolder $statusFolder

    您也可以使用 hello-檔案切換 toospecify HDFS 上的 Pig 指令碼檔案。
6. 新增下列程式碼片段 toosave hello 開始時間的 hello 和送出 hello Pig 工作。

        # Save hello start time and submit hello job toohello cluster.
        $startTime = Get-Date
        Select-AzureSubscription $subscriptionName
        $pigJob = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $pigJobDefinition
7. 新增下列 hello Pig 工作 toocomplete 的 toowait hello。

        # Wait for hello Pig job toocomplete.
        Wait-AzureHDInsightJob -Job $pigJob -WaitTimeoutInSeconds 3600
8. 新增 hello 遵循 tooprint hello 標準輸出和 hello 開始和結束時間。

        # Print hello standard error, hello standard output of hello Hive job, and hello start and end time.
        $endTime = Get-Date
        Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $pigJob.JobId -StandardOutput
        Write-Host "Start: " $startTime ", End: " $endTime -ForegroundColor Green
9. **執行** 新的指令碼！ **按一下**hello 綠色執行] 按鈕。
10. 檢查 hello 結果。 登入 hello [Azure 入口網站][azure-portal]。

    1. 按一下<strong>瀏覽</strong>hello 左側面板上。 </br>
    2. 按一下<strong>一切</strong>在 hello 的右上方 hello 瀏覽面板。 </br>
    3. 尋找並按一下 [Azure Cosmos DB 帳戶]<strong></strong>。 </br>
    4. 接下來，尋找您<strong>Azure Cosmos DB 帳戶</strong>，然後<strong>Azure Cosmos DB Database</strong>和您<strong>Azure Cosmos DB 集合</strong>hello 輸出集合中指定相關聯Pig 查詢。</br>
    5. 最後，按一下 [<strong>開發人員工具</strong>] 底下的 <strong>Document Explorer</strong>。</br></p>

    您會看到 hello Pig 查詢結果。

    ![Pig 查詢結果][image-pig-query-results]

## <a name="RunMapReduce"></a>步驟 5：使用 Azure Cosmos DB 和 HDInsight 執行 MapReduce 作業
1. 下列 PowerShell 指令碼窗格中的變數集 hello。

        $subscriptionName = "<SubscriptionName>"   # Azure subscription name
        $clusterName = "<ClusterName>"             # HDInsight cluster name
2. 我們會執行 MapReduce 工作，計算 hello Azure Cosmos DB 集合中每個文件屬性的項目數目。 新增此指令碼程式碼片段**之後**hello 程式碼片段上方。

        # Define hello MapReduce job.
        $TallyPropertiesJobDefinition = New-AzureHDInsightMapReduceJobDefinition -JarFile "wasb:///example/jars/TallyProperties-v01.jar" -ClassName "TallyProperties" -Arguments "<DocumentDB Endpoint>","<DocumentDB Primary Key>", "<DocumentDB Database Name>","<DocumentDB Input Collection Name>","<DocumentDB Output Collection Name>","<[Optional] DocumentDB Query>"

   > [!NOTE]
   > TallyProperties v01.jar 隨附的 hello Cosmos DB Hadoop 連接器 hello 自訂安裝。
   >
   >
3. 新增下列命令 toosubmit hello MapReduce 工作的 hello。

        # Save hello start time and submit hello job.
        $startTime = Get-Date
        Select-AzureSubscription $subscriptionName
        $TallyPropertiesJob = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $TallyPropertiesJobDefinition | Wait-AzureHDInsightJob -WaitTimeoutInSeconds 3600  

    此外 toohello MapReduce 工作定義，您也提供您想 toorun hello MapReduce 工作，以及 hello 認證 hello HDInsight 叢集名稱。 hello Start-azurehdinsightjob 是非同步的呼叫。 hello 作業，使用 hello toocheck hello 完成*Wait-azurehdinsightjob* cmdlet。
4. 加入下列命令 toocheck hello 執行 hello MapReduce 工作的任何錯誤。

        # Get hello job output and print hello start and end time.
        $endTime = Get-Date
        Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $TallyPropertiesJob.JobId -StandardError
        Write-Host "Start: " $startTime ", End: " $endTime -ForegroundColor Green
5. **執行** 新的指令碼！ **按一下**hello 綠色執行] 按鈕。
6. 檢查 hello 結果。 登入 hello [Azure 入口網站][azure-portal]。

   1. 按一下<strong>瀏覽</strong>hello 左側面板上。
   2. 按一下<strong>一切</strong>在 hello 的右上方 hello 瀏覽面板。
   3. 尋找並按一下 [Azure Cosmos DB 帳戶]<strong></strong>。
   4. 接下來，尋找您<strong>Azure Cosmos DB 帳戶</strong>，然後<strong>Azure Cosmos DB Database</strong>和您<strong>Azure Cosmos DB 集合</strong>hello 輸出集合中指定相關聯MapReduce 工作。
   5. 最後，按一下 [<strong>開發人員工具</strong>] 底下的 <strong>Document Explorer</strong>。

      您會看到 hello 的 MapReduce 工作的結果。

      ![MapReduce 查詢結果][image-mapreduce-query-results]

## <a name="NextSteps"></a>後續步驟
恭喜！ 您剛剛使用 Azure Cosmos DB 和 HDInsight 執行您的第一個 Hive、Pig 和 MapReduce 作業。

我們已開放 Hadoop 連接器的原始碼。 如果您有興趣，您可以在 [GitHub][github] 上發表意見。

toolearn 詳細資訊，請參閱下列文章 hello:

* [使用 Documentdb 開發 Java 應用程式][documentdb-java-application]
* [在 HDInsight 上開發 Hadoop 的 Java MapReduce 程式][hdinsight-develop-deploy-java-mapreduce]
* [開始使用登錄區中的 Hadoop，HDInsight tooanalyze 行動話筒使用中][hdinsight-get-started]
* [搭配 HDInsight 使用 MapReduce][hdinsight-use-mapreduce]
* [搭配 HDInsight 使用 Hivet][hdinsight-use-hive]
* [搭配 HDInsight 使用 Pig][hdinsight-use-pig]
* [使用指令碼動作來自訂 HDInsight 叢集][hdinsight-hadoop-customize-cluster]

[apache-hadoop]: http://hadoop.apache.org/
[apache-hadoop-doc]: http://hadoop.apache.org/docs/current/
[apache-hive]: http://hive.apache.org/
[apache-pig]: http://pig.apache.org/
[getting-started]: documentdb-get-started.md

[azure-portal]: https://portal.azure.com/
[azure-powershell-diagram]: ./media/run-hadoop-with-hdinsight/azurepowershell-diagram-med.png

[hdinsight-samples]: http://portalcontent.blob.core.windows.net/samples/documentdb-hdinsight-samples.zip
[github]: https://github.com/Azure/azure-documentdb-hadoop
[documentdb-java-application]: documentdb-java-application.md
[import-data]: import-data.md

[hdinsight-custom-provision]: ../hdinsight/hdinsight-provision-clusters.md
[hdinsight-develop-deploy-java-mapreduce]: ../hdinsight/hdinsight-develop-deploy-java-mapreduce-linux.md
[hdinsight-hadoop-customize-cluster]: ../hdinsight/hdinsight-hadoop-customize-cluster.md
[hdinsight-get-started]: ../hdinsight/hdinsight-hadoop-tutorial-get-started-windows.md
[hdinsight-storage]: ../hdinsight/hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-hive]: ../hdinsight/hdinsight-use-hive.md
[hdinsight-use-mapreduce]: ../hdinsight/hdinsight-use-mapreduce.md
[hdinsight-use-pig]: ../hdinsight/hdinsight-use-pig.md

[image-customprovision-page1]: ./media/run-hadoop-with-hdinsight/customprovision-page1.png
[image-hive-query-results]: ./media/run-hadoop-with-hdinsight/hivequeryresults.PNG
[image-mapreduce-query-results]: ./media/run-hadoop-with-hdinsight/mapreducequeryresults.PNG
[image-pig-query-results]: ./media/run-hadoop-with-hdinsight/pigqueryresults.PNG

[powershell-install-configure]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0
