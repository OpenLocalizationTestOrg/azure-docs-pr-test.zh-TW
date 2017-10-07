---
title: "HDInsight 的 Azure 中的 Hadoop aaaAnalyze 飛行延遲資料 |Microsoft 文件"
description: "了解如何 toouse 一個 Windows PowerShell 指令碼 toocreate 的 HDInsight 叢集，執行 Hive 工作，執行 Sqoop 工作，並刪除 hello 叢集。"
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 00e26aa9-82fb-4dbe-b87d-ffe8e39a5412
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 6ebaee65d9b270e5dc2141dd1265011d372f497d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-flight-delay-data-by-using-hive-in-hdinsight"></a>在 HDInsight 上使用 Hadoop 分析航班延誤資料
Hive 可透過一種類似 SQL 的指令碼語言 (稱為 *[HiveQL][hadoop-hiveql]*) 來執行 Hadoop MapReduce 作業，可用來彙總、查詢和分析大量資料。

> [!IMPORTANT]
> hello 本文件中的步驟需要 Windows 為基礎的 HDInsight 叢集。 Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。 如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。 如需與 Linux 叢集搭配使用的步驟，請參閱 [在 HDInsight (Linux) 中使用 Hive 分析航班延誤資料](hdinsight-analyze-flight-delay-data-linux.md)。

其中一個 Azure HDInsight hello 主要優點是 hello 分隔資料儲存和計算。 HDInsight 使用 Azure Blob 儲存體來儲存資料。 典型的工作包含三個部分：

1. **將資料儲存在 Azure Blob 儲存體中。**  例如，將天氣資料、感應器資料、Web 記錄，以及此案例中的航班延誤資料儲存到 Azure Blob 儲存體中。
2. **執行工作。** 時間 tooprocess hello 資料時，執行 Windows PowerShell 指令碼 （或用戶端應用程式） toocreate 的 HDInsight 叢集，執行作業，並刪除 hello 叢集。 輸出資料 tooAzure Blob 儲存體儲存 hello 作業。 即使在刪除 hello 叢集之後，會保留 hello 輸出資料。 因此，您只需要對已耗用的部分付費。
3. **從 Azure Blob 儲存體擷取 hello 輸出**，或在本教學課程中，匯出 hello 資料 tooan Azure SQL database。

hello 下列圖表說明 hello 案例和本教學課程的 hello 結構：

![HDI.FlightDelays.flow][img-hdi-flightdelays-flow]

請注意 hello hello 圖表中的數字對應 toohello 章節標題。 **M**代表 hello 主要處理序。 **A**代表 hello 附錄中的 hello 內容。

hello hello 教學課程的主要部分會顯示影響 toouse 一個 Windows PowerShell 指令碼 tooperform hello 下列工作：

* 建立 HDInsight 叢集。
* 在機場，hello 叢集 toocalculate 平均延遲上執行 Hive 工作。 hello 飛行延遲資料會儲存在 Azure Blob 儲存體帳戶。
* 執行 Sqoop 作業 tooexport hello Hive 工作輸出 tooan Azure SQL 資料庫。
* 刪除 hello HDInsight 叢集。

在 hello 附錄中，您可以找到 hello 指示將飛行延遲資料上傳、 建立/上傳 Hive 查詢字串，與 hello Azure SQL database 準備 hello Sqoop 工作。

> [!NOTE]
> 本文件中的 hello 步驟是特定 tooWindows 為基礎的 HDInsight 叢集。 如需與 Linux 叢集搭配使用的步驟，請參閱[在 HDInsight (Linux) 中使用 Hive 分析航班延誤資料](hdinsight-analyze-flight-delay-data-linux.md)

### <a name="prerequisites"></a>必要條件
開始本教學課程之前，您必須具備下列項目 hello:

* **Azure 訂用帳戶**。 請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)。
* **具有 Azure PowerShell 的工作站**。

    > [!IMPORTANT]
    > 使用 Azure Service Manager 管理 HDInsight 資源的 Azure PowerShell 支援已**被取代**，並已在 2017 年 1 月 1 日移除。 此文件使用 hello 新 HDInsight 的 cmdlet 可與 Azure 資源管理員中的步驟 hello。
    >
    > 請依照中的 hello 步驟[安裝和設定 Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall hello 最新版的 Azure PowerShell。 如果您有指令碼的需要 toobe 修改 toouse hello 新的 cmdlet 可與 Azure 資源管理員，請參閱[移轉 tooAzure 資源管理員為基礎的開發工具的 HDInsight 叢集](hdinsight-hadoop-development-using-azure-resource-manager.md)如需詳細資訊。

**本教學課程中使用的檔案**

本教學課程使用 airline 飛行資料從 hello 時間上效能[研究及創新技術管理、 局所免費提供的運輸統計資料或 RITA][rita-website]。
一份 hello 資料已經上傳 tooan Azure Blob 儲存體容器具有 hello 公用 Blob 的存取權限。
PowerShell 指令碼部分會複製 hello 資料從 hello 公用 blob 容器 toohello 預設 blob 容器的叢集。 hello HiveQL 指令碼也會複製 toohello 相同的 Blob 容器。
如果您想 toolearn 如何上傳 tooget/hello 資料 tooyour 擁有儲存體帳戶，以及如何上傳 toocreate/hello 下列 HiveQL 指令碼檔案，請參閱[附錄 A](#appendix-a)和[附錄 B](#appendix-b)。

hello 下表列出本教學課程所用的 hello 檔案：

<table border="1">
<tr><th>檔案</th><th>說明</th></tr>
<tr><td>wasb://flightdelay@hditutorialdata.blob.core.windows.net/flightdelays.hql</td><td>hello Hive 工作由 hello 下列 HiveQL 指令碼檔案。 此指令碼已上傳的 tooan hello 公用存取 Azure Blob 儲存體帳戶。 <a href="#appendix-b">附錄 B</a>的準備和上傳這個檔案 tooyour 自己 Azure Blob 儲存體帳戶的指示。</td></tr>
<tr><td>wasb://flightdelay@hditutorialdata.blob.core.windows.net/2013Data</td><td>Hello Hive 工作的輸入的資料。 hello 資料已上傳的 tooan hello 公用存取 Azure Blob 儲存體帳戶。 <a href="#appendix-a">附錄 A</a>的指示，取得 hello 資料，並上傳 hello 資料 tooyour 自己 Azure Blob 儲存體帳戶。</td></tr>
<tr><td>\tutorials\flightdelays\output</td><td>hello hello Hive 工作的輸出路徑。 hello 預設容器用來儲存 hello 輸出資料。</td></tr>
<tr><td>\tutorials\flightdelays\jobstatus</td><td>hello Hive 工作狀態上，資料夾 hello 預設容器。</td></tr>
</table>

## <a name="create-cluster-and-run-hivesqoop-jobs"></a>建立叢集和執行 Hive/Sqoop 工作
Hadoop MapReduce 是批次處理。 hello 大部分符合成本效益的方式 toorun Hive 工作是 toocreate 叢集 hello 作業並 hello 工作完成之後刪除 hello 工作。 hello 下列指令碼包含 hello 整個程序。
如需有關建立 HDInsight 叢集和執行 Hive 工作的詳細資訊，請參閱[在 HDInsight 中建立 Hadoop 叢集][hdinsight-provision]和[搭配 HDInsight 使用 Hive][hdinsight-use-hive]。

**Azure powershell toorun hello Hive 查詢**

1. 使用中的 hello 指示建立 hello Sqoop 作業輸出的 Azure SQL 資料庫與 hello 資料表[旓紵 C](#appendix-c)。
2. 開啟 Windows PowerShell ISE，然後執行下列指令碼的 hello:

    ```powershell
    $subscriptionID = "<Azure Subscription ID>"
    $nameToken = "<Enter an Alias>"

    ###########################################
    # You must configure hello follwing variables
    # for an existing Azure SQL Database
    ###########################################
    $existingSqlDatabaseServerName = "<Azure SQL Database Server>"
    $existingSqlDatabaseLogin = "<Azure SQL Database Server Login>"
    $existingSqlDatabasePassword = "<Azure SQL Database Server login password>"
    $existingSqlDatabaseName = "<Azure SQL Database name>"

    $localFolder = "E:\Tutorials\Downloads\" # A temp location for copying files.
    $azcopyPath = "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy" # depends on hello version, hello folder can be different

    ###########################################
    # (Optional) configure hello following variables
    ###########################################

    $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")

    $resourceGroupName = $namePrefix + "rg"
    $location = "EAST US 2"

    $HDInsightClusterName = $namePrefix + "hdi"
    $httpUserName = "admin"
    $httpPassword = "<Enter hello Password>"

    $defaultStorageAccountName = $namePrefix + "store"
    $defaultBlobContainerName = $HDInsightClusterName # use hello cluster name

    $existingSqlDatabaseTableName = "AvgDelays"
    $sqlDatabaseConnectionString = "jdbc:sqlserver://$existingSqlDatabaseServerName.database.windows.net;user=$existingSqlDatabaseLogin@$existingSqlDatabaseServerName;password=$existingSqlDatabaseLogin;database=$existingSqlDatabaseName"

    $hqlScriptFile = "/tutorials/flightdelays/flightdelays.hql"

    $jobStatusFolder = "/tutorials/flightdelays/jobstatus"

    ###########################################
    # Login
    ###########################################
    try{
        $acct = Get-AzureRmSubscription
    }
    catch{
        Login-AzureRmAccount
    }
    Select-AzureRmSubscription -SubscriptionID $subscriptionID

    ###########################################
    # Create a new HDInsight cluster
    ###########################################

    # Create ARM group
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $location

    # Create hello default storage account
    New-AzureRmStorageAccount -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName -Location $location -Type Standard_LRS

    # Create hello default Blob container
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccountName -StorageAccountKey $defaultStorageAccountKey
    New-AzureStorageContainer -Name $defaultBlobContainerName -Context $defaultStorageAccountContext

    # Create hello HDInsight cluster
    $pw = ConvertTo-SecureString -String $httpPassword -AsPlainText -Force
    $httpCredential = New-Object System.Management.Automation.PSCredential($httpUserName,$pw)

    New-AzureRmHDInsightCluster `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $HDInsightClusterName `
        -Location $location `
        -ClusterType Hadoop `
        -OSType Windows `
        -ClusterSizeInNodes 2 `
        -HttpCredential $httpCredential `
        -DefaultStorageAccountName "$defaultStorageAccountName.blob.core.windows.net" `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultStorageContainer $existingDefaultBlobContainerName

    ###########################################
    # Prepare hello HiveQL script and source data
    ###########################################

    # Create hello temp location
    New-Item -Path $localFolder -ItemType Directory -Force

    # Download hello sample file from Azure Blob storage
    $context = New-AzureStorageContext -StorageAccountName "hditutorialdata" -Anonymous
    $blobs = Get-AzureStorageBlob -Container "flightdelay" -Context $context
    #$blobs | Get-AzureStorageBlobContent -Context $context -Destination $localFolder

    # Upload data toodefault container

    $azcopycmd = "cmd.exe /C '$azcopyPath\azcopy.exe' /S /Source:'$localFolder' /Dest:'https://$defaultStorageAccountName.blob.core.windows.net/$defaultBlobContainerName/tutorials/flightdelays' /DestKey:$defaultStorageAccountKey"

    Invoke-Expression -Command:$azcopycmd

    ###########################################
    # Submit hello Hive job
    ###########################################
    Use-AzureRmHDInsightCluster -ClusterName $HDInsightClusterName -HttpCredential $httpCredential
    $response = Invoke-AzureRmHDInsightHiveJob `
                    -Files $hqlScriptFile `
                    -DefaultContainer $defaultBlobContainerName `
                    -DefaultStorageAccountName $defaultStorageAccountName `
                    -DefaultStorageAccountKey $defaultStorageAccountKey `
                    -StatusFolder $jobStatusFolder

    write-Host $response

    ###########################################
    # Submit hello Sqoop job
    ###########################################
    $exportDir = "wasb://$defaultBlobContainerName@$defaultStorageAccountName.blob.core.windows.net/tutorials/flightdelays/output"

    $sqoopDef = New-AzureRmHDInsightSqoopJobDefinition `
                    -Command "export --connect $sqlDatabaseConnectionString --table $sqlDatabaseTableName --export-dir $exportDir --fields-terminated-by \001 "
    $sqoopJob = Start-AzureRmHDInsightJob `
                    -ResourceGroupName $resourceGroupName `
                    -ClusterName $hdinsightClusterName `
                    -HttpCredential $httpCredential `
                    -JobDefinition $sqoopDef #-Debug -Verbose

    Wait-AzureRmHDInsightJob `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $HDInsightClusterName `
        -HttpCredential $httpCredential `
        -WaitTimeoutInSeconds 3600 `
        -Job $sqoopJob.JobId

    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -HttpCredential $httpCredential `
        -DefaultContainer $existingDefaultBlobContainerName `
        -DefaultStorageAccountName $defaultStorageAccountName `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -JobId $sqoopJob.JobId `
        -DisplayOutputType StandardError

    ###########################################
    # Delete hello cluster
    ###########################################
    Remove-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $hdinsightClusterName
    ```
3. 連接 tooyour SQL 資料庫，並依城市 hello AvgDelays 資料表中的平均航班延誤請參閱：

    ![HDI.FlightDelays.AvgDelays.Dataset][image-hdi-flightdelays-avgdelays-dataset]

- - -

## <a id="appendix-a"></a>附錄 A-上傳飛行延遲資料 tooAzure Blob 儲存體
上傳 hello 資料檔和 hello 下列 HiveQL 指令碼檔案 (請參閱[附錄 B](#appendix-b)) 需要一些規劃。 hello 概念是 toostore hello 資料檔案和 hello HiveQL 檔案之前建立的 HDInsight 叢集和執行 hello Hive 工作。 您有兩個選擇：

* **使用 hello 相同 hello HDInsight 叢集將會使用為 hello 預設檔案系統的 Azure 儲存體帳戶。** Hello HDInsight 叢集將具有 hello 儲存體帳戶存取金鑰，因為您不需要 toomake 任何其他變更。
* **使用不同的 Azure 儲存體帳戶，從 hello HDInsight 叢集預設的檔案系統。** 在 hello 情況下，您必須修改 hello 建立組件的 Windows PowerShell 指令碼中找到 hello[建立 HDInsight 叢集和執行的 Hive/Sqoop 工作](#runjob)toolink hello 與額外的儲存體帳戶的儲存體帳戶。 如需指示，請參閱[在 HDInsight 中建立 Hadoop 叢集][hdinsight-provision]。 hello HDInsight 叢集就會知道 hello hello 儲存體帳戶的存取金鑰。

> [!NOTE]
> hello 的 hello 資料檔是硬式編碼 hello 下列 HiveQL 指令碼檔案中的 Blob 儲存體路徑。 您必須據以更新。

**toodownload hello 飛行資料**

1. 瀏覽過[研究和創新的技術管理、 運輸局所免費提供統計][rita-website]。
2. 在 hello 頁面上，選取下列值的 hello:

    <table border="1">
    <tr><th>名稱</th><th>值</th></tr>
    <tr><td>篩選年份</td><td>2013 </td></tr>
    <tr><td>篩選期間</td><td>一月</td></tr>
    <tr><td>欄位</td><td>*Year*、*FlightDate*、*UniqueCarrier*、*Carrier*、*FlightNum*、*OriginAirportID*、*Origin*、*OriginCityName*、*OriginState*、*DestAirportID*、*Dest*、*DestCityName*、*DestState*、*DepDelayMinutes*、*ArrDelay*、*ArrDelayMinutes*、*CarrierDelay*、*WeatherDelay*、*NASDelay*、*SecurityDelay*、*LateAircraftDelay* (請清除其餘所有欄位)</td></tr>
    </table>
3. 按一下 **下載**。
4. 解壓縮 hello 檔案 toohello **C:\Tutorials\FlightDelay\2013Data**資料夾。 每個檔案皆為 CSV 檔案，大小約為 60 GB。
5. 它包含資料的 hello 月份 hello 檔案 toohello 名稱重新命名。 例如，包含 hello 年 1 月資料的 hello 檔案會命名為*January.csv*。
6. 針對每個 hello 2013 中的 12 個月重複執行步驟 2 和 5 toodownload 檔案。 您必須至少有一個檔案 toorun hello 教學課程。

**tooupload hello 飛行延遲資料 tooAzure Blob 儲存體**

1. 準備 hello 參數：

    <table border="1">
    <tr><th>變數名稱</th><th>注意事項</th></tr>
    <tr><td>$storageAccountName</td><td>hello tooupload hello 資料所在的 Azure 儲存體帳戶。</td></tr>
    <tr><td>$blobContainerName</td><td>您想要 tooupload hello 資料 hello Blob 容器。</td></tr>
    </table>
2. 開啟 Azure PowerShell ISE。
3. 貼上下列指令碼到 hello 指令碼窗格中的 hello:

    ```powershell
    [CmdletBinding()]
    Param(

        [Parameter(Mandatory=$True,
                    HelpMessage="Enter hello Azure storage account name for creating a new HDInsight cluster. If hello account doesn't exist, hello script will create one.")]
        [String]$storageAccountName,

        [Parameter(Mandatory=$True,
                    HelpMessage="Enter hello Azure blob container name for creating a new HDInsight cluster. If not specified, hello HDInsight cluster name will be used.")]
        [String]$blobContainerName
    )

    #Region - Variables
    $localFolder = "C:\Tutorials\FlightDelay\2013Data"  # hello source folder
    $destFolder = "tutorials/flightdelay/2013data"     #hello blob name prefix for hello files toobe uploaded
    #EndRegion

    #Region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #EndRegion

    #Region - Validate user input
    Write-Host "`nValidating hello Azure Storage account and hello Blob container..." -ForegroundColor Green
    # Validate hello Storage account
    if (-not (Get-AzureRmStorageAccount|Where-Object{$_.StorageAccountName -eq $storageAccountName}))
    {
        Write-Host "hello storage account, $storageAccountName, doesn't exist." -ForegroundColor Red
        exit
    }
    else{
        $resourceGroupName = (Get-AzureRmStorageAccount|Where-Object{$_.StorageAccountName -eq $storageAccountName}).ResourceGroupName
    }

    # Validate hello container
    $storageAccountKey = (Get-AzureRmStorageAccountKey -StorageAccountName $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    if (-not (Get-AzureStorageContainer -Context $storageContext |Where-Object{$_.Name -eq $blobContainerName}))
    {
        Write-Host "hello Blob container, $blobContainerName, doesn't exist" -ForegroundColor Red
        Exit
    }
    #EngRegion

    #Region - Copy hello file from local workstation tooAzure Blob storage
    if (test-path -Path $localFolder)
    {
        foreach ($item in Get-ChildItem -Path $localFolder){
            $fileName = "$localFolder\$item"
            $blobName = "$destFolder/$item"

            Write-Host "Copying $fileName too$blobName" -ForegroundColor Green

            Set-AzureStorageBlobContent -File $fileName -Container $blobContainerName -Blob $blobName -Context $storageContext
        }
    }
    else
    {
        Write-Host "hello source folder on hello workstation doesn't exist" -ForegroundColor Red
    }

    # List hello uploaded files on HDInsight
    Get-AzureStorageBlob -Container $blobContainerName  -Context $storageContext -Prefix $destFolder
    #EndRegion
    ```
4. 按**F5** toorun hello 指令碼。

如果您選擇 toouse hello 檔案上傳不同的方法，請確定 hello 檔案路徑是教學課程/flightdelay 資料。 hello 存取 hello 檔案的語法為：

    wasb://<ContainerName>@<StorageAccountName>.blob.core.windows.net/tutorials/flightdelay/data

hello 路徑教學課程/flightdelay/資料是 hello hello 檔案上傳時所建立的虛擬資料夾。 請確認共有 12 個檔案，每個月份各一個。

> [!NOTE]
> 您必須更新 hello Hive 查詢 tooread 從 hello 新位置。
>
> 您必須設定 hello 容器存取權限 toobe 公用，或繫結 hello 儲存體帳戶 toohello HDInsight 叢集。 否則，hello Hive 查詢字串不會無法 tooaccess hello 資料檔案。

- - -

## <a id="appendix-b"></a>附錄 B - 建立及上傳 HiveQL 指令碼
使用 Azure PowerShell，您可以執行多個下列 HiveQL 陳述式一次，或封裝 hello HiveQL 陳述式到指令碼檔案。 本節說明如何 toocreate 下列 HiveQL 指令碼和上傳 hello 編寫指令碼 tooAzure Blob 儲存體使用 Azure PowerShell。 Hive 需要 Azure Blob 儲存體中的 hello 下列 HiveQL 指令碼 toobe。

hello 下列 HiveQL 指令碼將會執行下列 hello:

1. **卸除 hello delays_raw 資料表**，以防 hello 資料表已經存在。
2. **建立 hello delays_raw 外部的 Hive 資料表**hello 飛行延遲檔案以指出 toohello Blob 儲存體位置。 此查詢會指定欄位將以 "," 分隔，且每一行都會以 "\n" 結尾。 這會造成問題，當欄位值包含逗號，因為登錄區無法分辨是欄位分隔符號逗號和一個屬於欄位值 (這是來源的欄位值中的 hello 案例\_縣 （市)\_名稱和目的地\_縣 （市)\_名稱)。 tooaddress hello，查詢會建立暫存資料行未正確分割成資料行的 toohold 資料。
3. **卸除 hello 延遲資料表**，以防 hello 資料表已經存在。
4. **建立 hello 延遲資料表**。 很有幫助 tooclean hello 資料再進一步處理。 此查詢建立新的資料表，*延遲*，hello delays_raw 資料表中。 請注意，不會複製 hello 暫存資料行 （如先前所述），以及該 hello **substring**函式是從 hello 資料使用的 tooremove 引號。
5. **計算 hello 平均天氣延遲和群組 hello 結果依城市名稱。** 它也會輸出 hello 結果 tooBlob 儲存體。 請注意該 hello 查詢將會從 hello 資料移除所有格符號，並且排除 hello 其中值的資料列**weather_delay**為 null。 這是必要動作，因為 Sqoop (稍後使用於本教學課程) 預設不會正常處理這些值。

Hello HiveQL 命令的完整清單，請參閱[hive 控制檔的資料定義語言][hadoop-hiveql]。 每個 HiveQL 命令都必須以分號結尾。

**toocreate 下列 HiveQL 指令碼檔案**

1. 準備 hello 參數：

    <table border="1">
    <tr><th>變數名稱</th><th>注意事項</th></tr>
    <tr><td>$storageAccountName</td><td>hello tooupload hello 下列 HiveQL 指令碼所在的 Azure 儲存體帳戶。</td></tr>
    <tr><td>$blobContainerName</td><td>您想要 tooupload hello 下列 HiveQL 指令碼，以 hello Blob 容器。</td></tr>
    </table>
2. 開啟 Azure PowerShell ISE。
3. 複製並貼上下列指令碼到 hello 指令碼窗格中的 hello:

    ```powershell
    [CmdletBinding()]
    Param(

        # Azure Blob storage variables
        [Parameter(Mandatory=$True,
                    HelpMessage="Enter hello Azure storage account name for creating a new HDInsight cluster. If hello account doesn't exist, hello script will create one.")]
        [String]$storageAccountName,

        [Parameter(Mandatory=$True,
                    HelpMessage="Enter hello Azure blob container name for creating a new HDInsight cluster. If not specified, hello HDInsight cluster name will be used.")]
        [String]$blobContainerName
    )

    #region - Define variables
    # Treat all errors as terminating
    $ErrorActionPreference = "Stop"

    # hello HiveQL script file is exported as this file before it's uploaded tooBlob storage
    $hqlLocalFileName = "e:\tutorials\flightdelay\flightdelays.hql"

    # hello HiveQL script file will be uploaded tooBlob storage as this blob name
    $hqlBlobName = "tutorials/flightdelay/flightdelays.hql"

    # These two constants are used by hello HiveQL script file
    #$srcDataFolder = "tutorials/flightdelay/data"
    $dstDataFolder = "/tutorials/flightdelay/output"
    #endregion

    #Region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #EndRegion

    #Region - Validate user input
    Write-Host "`nValidating hello Azure Storage account and hello Blob container..." -ForegroundColor Green
    # Validate hello Storage account
    if (-not (Get-AzureRmStorageAccount|Where-Object{$_.StorageAccountName -eq $storageAccountName}))
    {
        Write-Host "hello storage account, $storageAccountName, doesn't exist." -ForegroundColor Red
        exit
    }
    else{
        $resourceGroupName = (Get-AzureRmStorageAccount|Where-Object{$_.StorageAccountName -eq $storageAccountName}).ResourceGroupName
    }

    # Validate hello container
    $storageAccountKey = (Get-AzureRmStorageAccountKey -StorageAccountName $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    if (-not (Get-AzureStorageContainer -Context $storageContext |Where-Object{$_.Name -eq $blobContainerName}))
    {
        Write-Host "hello Blob container, $blobContainerName, doesn't exist" -ForegroundColor Red
        Exit
    }
    #EngRegion

    #region - Validate hello file and file path

    # Check if a file with hello same file name already exists on hello workstation
    Write-Host "`nvalidating hello folder structure on hello workstation for saving hello HQL script file ..."  -ForegroundColor Green
    if (test-path $hqlLocalFileName){

        $isDelete = Read-Host 'hello file, ' $hqlLocalFileName ', exists.  Do you want toooverwirte it? (Y/N)'

        if ($isDelete.ToLower() -ne "y")
        {
            Exit
        }
    }

    # Create hello folder if it doesn't exist
    $folder = split-path $hqlLocalFileName
    if (-not (test-path $folder))
    {
        Write-Host "`nCreating folder, $folder ..." -ForegroundColor Green

        new-item $folder -ItemType directory
    }
    #end region

    #region - Write hello Hive script into a local file
    Write-Host "`nWriting hello Hive script into a file on your workstation ..." `
                -ForegroundColor Green

    $hqlDropDelaysRaw = "DROP TABLE delays_raw;"

    $hqlCreateDelaysRaw = "CREATE EXTERNAL TABLE delays_raw (" +
            "YEAR string, " +
            "FL_DATE string, " +
            "UNIQUE_CARRIER string, " +
            "CARRIER string, " +
            "FL_NUM string, " +
            "ORIGIN_AIRPORT_ID string, " +
            "ORIGIN string, " +
            "ORIGIN_CITY_NAME string, " +
            "ORIGIN_CITY_NAME_TEMP string, " +
            "ORIGIN_STATE_ABR string, " +
            "DEST_AIRPORT_ID string, " +
            "DEST string, " +
            "DEST_CITY_NAME string, " +
            "DEST_CITY_NAME_TEMP string, " +
            "DEST_STATE_ABR string, " +
            "DEP_DELAY_NEW float, " +
            "ARR_DELAY_NEW float, " +
            "CARRIER_DELAY float, " +
            "WEATHER_DELAY float, " +
            "NAS_DELAY float, " +
            "SECURITY_DELAY float, " +
            "LATE_AIRCRAFT_DELAY float) " +
        "ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' " +
        "LINES TERMINATED BY '\n' " +
        "STORED AS TEXTFILE " +
        "LOCATION 'wasb://flightdelay@hditutorialdata.blob.core.windows.net/2013Data';"

    $hqlDropDelays = "DROP TABLE delays;"

    $hqlCreateDelays = "CREATE TABLE delays AS " +
        "SELECT YEAR AS year, " +
            "FL_DATE AS flight_date, " +
            "substring(UNIQUE_CARRIER, 2, length(UNIQUE_CARRIER) -1) AS unique_carrier, " +
            "substring(CARRIER, 2, length(CARRIER) -1) AS carrier, " +
            "substring(FL_NUM, 2, length(FL_NUM) -1) AS flight_num, " +
            "ORIGIN_AIRPORT_ID AS origin_airport_id, " +
            "substring(ORIGIN, 2, length(ORIGIN) -1) AS origin_airport_code, " +
            "substring(ORIGIN_CITY_NAME, 2) AS origin_city_name, " +
            "substring(ORIGIN_STATE_ABR, 2, length(ORIGIN_STATE_ABR) -1)  AS origin_state_abr, " +
            "DEST_AIRPORT_ID AS dest_airport_id, " +
            "substring(DEST, 2, length(DEST) -1) AS dest_airport_code, " +
            "substring(DEST_CITY_NAME,2) AS dest_city_name, " +
            "substring(DEST_STATE_ABR, 2, length(DEST_STATE_ABR) -1) AS dest_state_abr, " +
            "DEP_DELAY_NEW AS dep_delay_new, " +
            "ARR_DELAY_NEW AS arr_delay_new, " +
            "CARRIER_DELAY AS carrier_delay, " +
            "WEATHER_DELAY AS weather_delay, " +
            "NAS_DELAY AS nas_delay, " +
            "SECURITY_DELAY AS security_delay, " +
            "LATE_AIRCRAFT_DELAY AS late_aircraft_delay " +
        "FROM delays_raw;"

    $hqlInsertLocal = "INSERT OVERWRITE DIRECTORY '$dstDataFolder' " +
        "SELECT regexp_replace(origin_city_name, '''', ''), " +
            "avg(weather_delay) " +
        "FROM delays " +
        "WHERE weather_delay IS NOT NULL " +
        "GROUP BY origin_city_name;"

    $hqlScript = $hqlDropDelaysRaw + $hqlCreateDelaysRaw + $hqlDropDelays + $hqlCreateDelays + $hqlInsertLocal

    $hqlScript | Out-File $hqlLocalFileName -Encoding ascii -Force
    #endregion

    #region - Upload hello Hive script toohello default Blob container
    Write-Host "`nUploading hello Hive script toohello default Blob container ..." -ForegroundColor Green

    # Create a storage context object
    $storageAccountKey = (Get-AzureRmStorageAccountKey -StorageAccountName $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
    $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    # Upload hello file from local workstation tooBlob storage
    Set-AzureStorageBlobContent -File $hqlLocalFileName -Container $blobContainerName -Blob $hqlBlobName -Context $destContext
    #endregion

    Write-host "`nEnd of hello PowerShell script" -ForegroundColor Green
    ```

    以下是使用 hello 指令碼中的 hello 變數：

   * **$hqlLocalFileName** -hello 指令碼 hello HiveQL 指令碼會將檔案儲存在本機之前將它上傳 tooBlob 儲存體。 這是 hello 檔案名稱。 hello 預設值是<u>C:\tutorials\flightdelay\flightdelays.hql</u>。
   * **$hqlBlobName** -這是 hello 下列 HiveQL 指令碼檔案 blob 名稱 hello Azure Blob 儲存體中使用。 hello 預設值為 tutorials/flightdelay/flightdelays.hql。 Hello 檔會寫入直接 tooAzure Blob 儲存體，因為沒有"/"開頭 hello hello blob 名稱。 如果您想 tooaccess hello 檔案從 Blob 儲存體，您需要 tooadd"/"開頭 hello hello 檔案名稱。
   * **$srcDataFolder** 和 **$dstDataFolder** - = "tutorials/flightdelay/data" = "tutorials/flightdelay/output"

- - -
## <a id="appendix-c"></a>附錄 C-將 Azure SQL database 準備 hello Sqoop 作業輸出
**tooprepare hello SQL 資料庫 （這與合併 hello Sqoop 指令碼）**

1. 準備 hello 參數：

    <table border="1">
    <tr><th>變數名稱</th><th>注意事項</th></tr>
    <tr><td>$sqlDatabaseServerName</td><td>hello hello Azure SQL database 伺服器名稱。 輸入任何 toocreate 新的伺服器。</td></tr>
    <tr><td>$sqlDatabaseUsername</td><td>hello hello Azure SQL database 伺服器的登入名稱。 如果 $sqlDatabaseServerName 是現有的伺服器，hello 登入和登入密碼。 使用的 tooauthenticate 與 hello 伺服器 否則，它們會使用的 toocreate 新的伺服器。</td></tr>
    <tr><td>$sqlDatabasePassword</td><td>hello hello Azure SQL database 伺服器的登入密碼。</td></tr>
    <tr><td>$sqlDatabaseLocation</td><td>只有在建立新的 Azure 資料庫伺服器時才會使用此值。</td></tr>
    <tr><td>$sqlDatabaseName</td><td>hello SQL database 會將 toocreate hello AvgDelays 資料表用於 hello Sqoop 工作。 保留空白會建立名為 HDISqoop 的資料庫。 hello Sqoop 作業輸出的 hello 資料表名稱是 AvgDelays。 </td></tr>
    </table>
2. 開啟 Azure PowerShell ISE。
3. 複製並貼上下列指令碼到 hello 指令碼窗格中的 hello:

    ```powershell
    [CmdletBinding()]
    Param(

        # Azure Resource group variables
        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello Azure resource group name. It will be created if it doesn't exist.")]
        [String]$resourceGroupName,

        # SQL database server variables
        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello Azure SQL Database Server Name. It will be created if it doesn't exist.")]
        [String]$sqlDatabaseServer,

        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello Azure SQL Database admin user.")]
        [String]$sqlDatabaseLogin,

        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello Azure SQL Database admin user password.")]
        [String]$sqlDatabasePassword,

        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello region toocreate hello Database in.")]
        [String]$sqlDatabaseLocation,   #For example, West US.

        # SQL database variables
        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello database name. It will be created if it doesn't exist.")]
        [String]$sqlDatabaseName # specify hello database name if you have one created. Otherwise use "" toohave hello script create one for you.
    )

    # Treat all errors as terminating
    $ErrorActionPreference = "Stop"

    #region - Constants and variables

    # IP address REST service used for retrieving external IP address and creating firewall rules
    [String]$ipAddressRestService = "http://bot.whatismyipaddress.com"
    [String]$fireWallRuleName = "FlightDelay"

    # SQL database variables
    [String]$sqlDatabaseMaxSizeGB = 10

    #SQL query string for creating AvgDelays table
    [String]$sqlDatabaseTableName = "AvgDelays"
    [String]$sqlCreateAvgDelaysTable = " CREATE TABLE [dbo].[$sqlDatabaseTableName](
                [origin_city_name] [nvarchar](50) NOT NULL,
                [weather_delay] float,
            CONSTRAINT [PK_$sqlDatabaseTableName] PRIMARY KEY CLUSTERED
            (
                [origin_city_name] ASC
            )
            )"
    #endregion

    #Region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #EndRegion

    #region - Create and validate Azure resouce group
    try{
        Get-AzureRmResourceGroup -Name $resourceGroupName
    }
    catch{
        New-AzureRmResourceGroup -Name $resourceGroupName -Location $sqlDatabaseLocation
    }

    #EndRegion

    #region - Create and validate Azure SQL database server
    try{
        Get-AzureRmSqlServer -ServerName $sqlDatabaseServer -ResourceGroupName $resourceGroupName}
    catch{
        Write-Host "`nCreating SQL Database server ..."  -ForegroundColor Green

        $sqlDatabasePW = ConvertTo-SecureString -String $sqlDatabasePassword -AsPlainText -Force
        $credential = New-Object System.Management.Automation.PSCredential($sqlDatabaseLogin,$sqlDatabasePW)

        $sqlDatabaseServer = (New-AzureRmSqlServer -ResourceGroupName $resourceGroupName -ServerName $sqlDatabaseServer -SqlAdministratorCredentials $credential -Location $sqlDatabaseLocation).ServerName
        Write-Host "`tThe new SQL database server name is $sqlDatabaseServer." -ForegroundColor Cyan

        Write-Host "`nCreating firewall rule, $fireWallRuleName ..." -ForegroundColor Green
        $workstationIPAddress = Invoke-RestMethod $ipAddressRestService
        New-AzureRmSqlServerFirewallRule -ResourceGroupName $resourceGroupName -ServerName $sqlDatabaseServer -FirewallRuleName "$fireWallRuleName-workstation" -StartIpAddress $workstationIPAddress -EndIpAddress $workstationIPAddress

        #tooallow other Azure services tooaccess hello server add a firewall rule and set both hello StartIpAddress and EndIpAddress too0.0.0.0. Note that this allows Azure traffic from any Azure subscription tooaccess hello server.
        New-AzureRmSqlServerFirewallRule -ResourceGroupName $resourceGroupName -ServerName $sqlDatabaseServer -FirewallRuleName "$fireWallRuleName-Azureservices" -StartIpAddress "0.0.0.0" -EndIpAddress "0.0.0.0"
    }

    #endregion

    #region - Create and validate Azure SQL database

    try {
        Get-AzureRmSqlDatabase -ResourceGroupName $resourceGroupName -ServerName $sqlDatabaseServer -DatabaseName $sqlDatabaseName
    }
    catch {
        Write-Host "`nCreating SQL Database, $sqlDatabaseName ..."  -ForegroundColor Green
        New-AzureRMSqlDatabase -ResourceGroupName $resourceGroupName -ServerName $sqlDatabaseServer -DatabaseName $sqlDatabaseName -Edition "Standard" -RequestedServiceObjectiveName "S1"
    }

    #endregion

    #region -  Execute an SQL command toocreate hello AvgDelays table

    Write-Host "`nCreating SQL Database table ..."  -ForegroundColor Green
    $conn = New-Object System.Data.SqlClient.SqlConnection
    $conn.ConnectionString = "Data Source=$sqlDatabaseServer.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabasePassword;Encrypt=true;Trusted_Connection=false;"
    $conn.open()
    $cmd = New-Object System.Data.SqlClient.SqlCommand
    $cmd.connection = $conn
    $cmd.commandtext = $sqlCreateAvgDelaysTable
    $cmd.executenonquery()

    $conn.close()

    Write-host "`nEnd of hello PowerShell script" -ForegroundColor Green
    ```

   > [!NOTE]
   > hello 指令碼會使用具像狀態傳輸 (REST) 服務、 http://bot.whatismyipaddress.com、 tooretrieve 外部的 IP 位址。 hello IP 位址用來建立 SQL 資料庫伺服器的防火牆規則。

    以下是一些 hello 指令碼中使用的變數：

   * **$ipAddressRestService** -hello 預設值是 http://bot.whatismyipaddress.com。這是用來取得外部 IP 位址的公用 IP 位址 REST 服務。 想要的話，您可以使用其他服務。 hello hello 服務透過擷取外部 IP 位址將會使用的 toocreate Azure SQL 資料庫伺服器的防火牆規則，以便您可以從您的工作站存取 hello 資料庫 （透過使用 Windows PowerShell 指令碼）。
   * **$fireWallRuleName** -這是 hello hello 防火牆規則 hello Azure SQL 資料庫伺服器名稱。 hello 預設名稱是<u>FlightDelay</u>。 想要的話，您可以將它重新命名。
   * **$sqlDatabaseMaxSizeGB** - 只有在建立新的 Azure SQL Database 伺服器時才會使用此值。 hello 預設值為 10 GB。 10GB 足夠供本教學課程使用。
   * **$sqlDatabaseName** - 只有在建立新的 Azure SQL Database 時才會使用此值。 hello 預設值為 HDISqoop。 如果您將它重新命名時，您必須跟著更新 hello Sqoop Windows PowerShell 指令碼。
4. 按**F5** toorun hello 指令碼。
5. 驗證 hello 指令碼輸出。 請確定 hello 指令碼已順利執行。

## <a id="nextsteps"></a> 後續步驟
現在您已了解如何 tooupload 檔案 tooAzure Blob 儲存體，如何使用 Azure Blob 儲存體中的 hello 資料 toopopulate Hive 資料表如何 toorun Hive 查詢，以及如何 toouse Sqoop tooexport 資料從 HDFS tooan Azure SQL database。 toolearn 詳細資訊，請參閱下列文章 hello:

* [開始使用 HDInsight][hdinsight-get-started]
* [搭配 HDInsight 使用 Hivet][hdinsight-use-hive]
* [搭配 HDInsight 使用 Oozie][hdinsight-use-oozie]
* [搭配 HDInsight 使用 Sqoop][hdinsight-use-sqoop]
* [搭配 HDInsight 使用 Pig][hdinsight-use-pig]
* [開發 HDInsight 的 Java MapReduce 程式][hdinsight-develop-mapreduce]

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[rita-website]: http://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236&DB_Short_Name=On-Time
[powershell-install-configure]: /powershell/azureps-cmdlets-docs

[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-develop-mapreduce]: hdinsight-develop-deploy-java-mapreduce-linux.md

[hadoop-hiveql]: https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DDL
[hadoop-shell-commands]: http://hadoop.apache.org/docs/r0.18.3/hdfs_shell.html

[technetwiki-hive-error]: http://social.technet.microsoft.com/wiki/contents/articles/23047.hdinsight-hive-error-unable-to-rename.aspx

[image-hdi-flightdelays-avgdelays-dataset]: ./media/hdinsight-analyze-flight-delay-data/HDI.FlightDelays.AvgDelays.DataSet.png
[img-hdi-flightdelays-run-hive-job-output]: ./media/hdinsight-analyze-flight-delay-data/HDI.FlightDelays.RunHiveJob.Output.png
[img-hdi-flightdelays-flow]: ./media/hdinsight-analyze-flight-delay-data/HDI.FlightDelays.Flow.png
