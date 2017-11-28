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
# <a name="analyze-flight-delay-data-by-using-hive-in-hdinsight"></a><span data-ttu-id="50ef6-103">在 HDInsight 上使用 Hadoop 分析航班延誤資料</span><span class="sxs-lookup"><span data-stu-id="50ef6-103">Analyze flight delay data by using Hive in HDInsight</span></span>
<span data-ttu-id="50ef6-104">Hive 可透過一種類似 SQL 的指令碼語言 (稱為 *[HiveQL][hadoop-hiveql]*) 來執行 Hadoop MapReduce 作業，可用來彙總、查詢和分析大量資料。</span><span class="sxs-lookup"><span data-stu-id="50ef6-104">Hive provides a means of running Hadoop MapReduce jobs through an SQL-like scripting language called *[HiveQL][hadoop-hiveql]*, which can be applied towards summarizing, querying, and analyzing large volumes of data.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="50ef6-105">hello 本文件中的步驟需要 Windows 為基礎的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="50ef6-105">hello steps in this document require a Windows-based HDInsight cluster.</span></span> <span data-ttu-id="50ef6-106">Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。</span><span class="sxs-lookup"><span data-stu-id="50ef6-106">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="50ef6-107">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="50ef6-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="50ef6-108">如需與 Linux 叢集搭配使用的步驟，請參閱 [在 HDInsight (Linux) 中使用 Hive 分析航班延誤資料](hdinsight-analyze-flight-delay-data-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="50ef6-108">For steps that work with a Linux-based cluster, see [Analyze flight delay data by using Hive in HDInsight (Linux)](hdinsight-analyze-flight-delay-data-linux.md).</span></span>

<span data-ttu-id="50ef6-109">其中一個 Azure HDInsight hello 主要優點是 hello 分隔資料儲存和計算。</span><span class="sxs-lookup"><span data-stu-id="50ef6-109">One of hello major benefits of Azure HDInsight is hello separation of data storage and compute.</span></span> <span data-ttu-id="50ef6-110">HDInsight 使用 Azure Blob 儲存體來儲存資料。</span><span class="sxs-lookup"><span data-stu-id="50ef6-110">HDInsight uses Azure Blob storage for data storage.</span></span> <span data-ttu-id="50ef6-111">典型的工作包含三個部分：</span><span class="sxs-lookup"><span data-stu-id="50ef6-111">A typical job involves three parts:</span></span>

1. <span data-ttu-id="50ef6-112">**將資料儲存在 Azure Blob 儲存體中。**</span><span class="sxs-lookup"><span data-stu-id="50ef6-112">**Store data in Azure Blob storage.**</span></span>  <span data-ttu-id="50ef6-113">例如，將天氣資料、感應器資料、Web 記錄，以及此案例中的航班延誤資料儲存到 Azure Blob 儲存體中。</span><span class="sxs-lookup"><span data-stu-id="50ef6-113">For example, weather data, sensor data, web logs, and in this case, flight delay data are saved into Azure Blob storage.</span></span>
2. <span data-ttu-id="50ef6-114">**執行工作。**</span><span class="sxs-lookup"><span data-stu-id="50ef6-114">**Run jobs.**</span></span> <span data-ttu-id="50ef6-115">時間 tooprocess hello 資料時，執行 Windows PowerShell 指令碼 （或用戶端應用程式） toocreate 的 HDInsight 叢集，執行作業，並刪除 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="50ef6-115">When it is time tooprocess hello data, you run a Windows PowerShell script (or a client application) toocreate an HDInsight cluster, run jobs, and delete hello cluster.</span></span> <span data-ttu-id="50ef6-116">輸出資料 tooAzure Blob 儲存體儲存 hello 作業。</span><span class="sxs-lookup"><span data-stu-id="50ef6-116">hello jobs save output data tooAzure Blob storage.</span></span> <span data-ttu-id="50ef6-117">即使在刪除 hello 叢集之後，會保留 hello 輸出資料。</span><span class="sxs-lookup"><span data-stu-id="50ef6-117">hello output data is retained even after hello cluster is deleted.</span></span> <span data-ttu-id="50ef6-118">因此，您只需要對已耗用的部分付費。</span><span class="sxs-lookup"><span data-stu-id="50ef6-118">This way, you pay for only what you have consumed.</span></span>
3. <span data-ttu-id="50ef6-119">**從 Azure Blob 儲存體擷取 hello 輸出**，或在本教學課程中，匯出 hello 資料 tooan Azure SQL database。</span><span class="sxs-lookup"><span data-stu-id="50ef6-119">**Retrieve hello output from Azure Blob storage**, or in this tutorial, export hello data tooan Azure SQL database.</span></span>

<span data-ttu-id="50ef6-120">hello 下列圖表說明 hello 案例和本教學課程的 hello 結構：</span><span class="sxs-lookup"><span data-stu-id="50ef6-120">hello following diagram illustrates hello scenario and hello structure of this tutorial:</span></span>

![HDI.FlightDelays.flow][img-hdi-flightdelays-flow]

<span data-ttu-id="50ef6-122">請注意 hello hello 圖表中的數字對應 toohello 章節標題。</span><span class="sxs-lookup"><span data-stu-id="50ef6-122">Note that hello numbers in hello diagram correspond toohello section titles.</span></span> <span data-ttu-id="50ef6-123">**M**代表 hello 主要處理序。</span><span class="sxs-lookup"><span data-stu-id="50ef6-123">**M** stands for hello main process.</span></span> <span data-ttu-id="50ef6-124">**A**代表 hello 附錄中的 hello 內容。</span><span class="sxs-lookup"><span data-stu-id="50ef6-124">**A** stands for hello content in hello appendix.</span></span>

<span data-ttu-id="50ef6-125">hello hello 教學課程的主要部分會顯示影響 toouse 一個 Windows PowerShell 指令碼 tooperform hello 下列工作：</span><span class="sxs-lookup"><span data-stu-id="50ef6-125">hello main portion of hello tutorial shows you how toouse one Windows PowerShell script tooperform hello following tasks:</span></span>

* <span data-ttu-id="50ef6-126">建立 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="50ef6-126">Create an HDInsight cluster.</span></span>
* <span data-ttu-id="50ef6-127">在機場，hello 叢集 toocalculate 平均延遲上執行 Hive 工作。</span><span class="sxs-lookup"><span data-stu-id="50ef6-127">Run a Hive job on hello cluster toocalculate average delays at airports.</span></span> <span data-ttu-id="50ef6-128">hello 飛行延遲資料會儲存在 Azure Blob 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="50ef6-128">hello flight delay data is stored in an Azure Blob storage account.</span></span>
* <span data-ttu-id="50ef6-129">執行 Sqoop 作業 tooexport hello Hive 工作輸出 tooan Azure SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="50ef6-129">Run a Sqoop job tooexport hello Hive job output tooan Azure SQL database.</span></span>
* <span data-ttu-id="50ef6-130">刪除 hello HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="50ef6-130">Delete hello HDInsight cluster.</span></span>

<span data-ttu-id="50ef6-131">在 hello 附錄中，您可以找到 hello 指示將飛行延遲資料上傳、 建立/上傳 Hive 查詢字串，與 hello Azure SQL database 準備 hello Sqoop 工作。</span><span class="sxs-lookup"><span data-stu-id="50ef6-131">In hello appendixes, you can find hello instructions for uploading flight delay data, creating/uploading a Hive query string, and preparing hello Azure SQL database for hello Sqoop job.</span></span>

> [!NOTE]
> <span data-ttu-id="50ef6-132">本文件中的 hello 步驟是特定 tooWindows 為基礎的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="50ef6-132">hello steps in this document are specific tooWindows-based HDInsight clusters.</span></span> <span data-ttu-id="50ef6-133">如需與 Linux 叢集搭配使用的步驟，請參閱[在 HDInsight (Linux) 中使用 Hive 分析航班延誤資料](hdinsight-analyze-flight-delay-data-linux.md)</span><span class="sxs-lookup"><span data-stu-id="50ef6-133">For steps that work with a Linux-based cluster, see [Analyze flight delay data using Hive in HDInsight (Linux)](hdinsight-analyze-flight-delay-data-linux.md)</span></span>

### <a name="prerequisites"></a><span data-ttu-id="50ef6-134">必要條件</span><span class="sxs-lookup"><span data-stu-id="50ef6-134">Prerequisites</span></span>
<span data-ttu-id="50ef6-135">開始本教學課程之前，您必須具備下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="50ef6-135">Before you begin this tutorial, you must have hello following items:</span></span>

* <span data-ttu-id="50ef6-136">**Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="50ef6-136">**An Azure subscription**.</span></span> <span data-ttu-id="50ef6-137">請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)。</span><span class="sxs-lookup"><span data-stu-id="50ef6-137">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="50ef6-138">**具有 Azure PowerShell 的工作站**。</span><span class="sxs-lookup"><span data-stu-id="50ef6-138">**A workstation with Azure PowerShell**.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="50ef6-139">使用 Azure Service Manager 管理 HDInsight 資源的 Azure PowerShell 支援已**被取代**，並已在 2017 年 1 月 1 日移除。</span><span class="sxs-lookup"><span data-stu-id="50ef6-139">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and was removed on January 1, 2017.</span></span> <span data-ttu-id="50ef6-140">此文件使用 hello 新 HDInsight 的 cmdlet 可與 Azure 資源管理員中的步驟 hello。</span><span class="sxs-lookup"><span data-stu-id="50ef6-140">hello steps in this document use hello new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="50ef6-141">請依照中的 hello 步驟[安裝和設定 Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall hello 最新版的 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="50ef6-141">Please follow hello steps in [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="50ef6-142">如果您有指令碼的需要 toobe 修改 toouse hello 新的 cmdlet 可與 Azure 資源管理員，請參閱[移轉 tooAzure 資源管理員為基礎的開發工具的 HDInsight 叢集](hdinsight-hadoop-development-using-azure-resource-manager.md)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="50ef6-142">If you have scripts that need toobe modified toouse hello new cmdlets that work with Azure Resource Manager, see [Migrating tooAzure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span></span>

<span data-ttu-id="50ef6-143">**本教學課程中使用的檔案**</span><span class="sxs-lookup"><span data-stu-id="50ef6-143">**Files used in this tutorial**</span></span>

<span data-ttu-id="50ef6-144">本教學課程使用 airline 飛行資料從 hello 時間上效能[研究及創新技術管理、 局所免費提供的運輸統計資料或 RITA][rita-website]。</span><span class="sxs-lookup"><span data-stu-id="50ef6-144">This tutorial uses hello on-time performance of airline flight data from [Research and Innovative Technology Administration, Bureau of Transportation Statistics or RITA][rita-website].</span></span>
<span data-ttu-id="50ef6-145">一份 hello 資料已經上傳 tooan Azure Blob 儲存體容器具有 hello 公用 Blob 的存取權限。</span><span class="sxs-lookup"><span data-stu-id="50ef6-145">A copy of hello data has been uploaded tooan Azure Blob storage container with hello Public Blob access permission.</span></span>
<span data-ttu-id="50ef6-146">PowerShell 指令碼部分會複製 hello 資料從 hello 公用 blob 容器 toohello 預設 blob 容器的叢集。</span><span class="sxs-lookup"><span data-stu-id="50ef6-146">A part of your PowerShell script copies hello data from hello public blob container toohello default blob container of your cluster.</span></span> <span data-ttu-id="50ef6-147">hello HiveQL 指令碼也會複製 toohello 相同的 Blob 容器。</span><span class="sxs-lookup"><span data-stu-id="50ef6-147">hello HiveQL script is also copied toohello same Blob container.</span></span>
<span data-ttu-id="50ef6-148">如果您想 toolearn 如何上傳 tooget/hello 資料 tooyour 擁有儲存體帳戶，以及如何上傳 toocreate/hello 下列 HiveQL 指令碼檔案，請參閱[附錄 A](#appendix-a)和[附錄 B](#appendix-b)。</span><span class="sxs-lookup"><span data-stu-id="50ef6-148">If you want toolearn how tooget/upload hello data tooyour own Storage account, and how toocreate/upload hello HiveQL script file, see [Appendix A](#appendix-a) and [Appendix B](#appendix-b).</span></span>

<span data-ttu-id="50ef6-149">hello 下表列出本教學課程所用的 hello 檔案：</span><span class="sxs-lookup"><span data-stu-id="50ef6-149">hello following table lists hello files used in this tutorial:</span></span>

<table border="1">
<tr><th><span data-ttu-id="50ef6-150">檔案</span><span class="sxs-lookup"><span data-stu-id="50ef6-150">Files</span></span></th><th><span data-ttu-id="50ef6-151">說明</span><span class="sxs-lookup"><span data-stu-id="50ef6-151">Description</span></span></th></tr>
<tr><td>wasb://flightdelay@hditutorialdata.blob.core.windows.net/flightdelays.hql</td><td><span data-ttu-id="50ef6-152">hello Hive 工作由 hello 下列 HiveQL 指令碼檔案。</span><span class="sxs-lookup"><span data-stu-id="50ef6-152">hello HiveQL script file used by hello Hive job.</span></span> <span data-ttu-id="50ef6-153">此指令碼已上傳的 tooan hello 公用存取 Azure Blob 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="50ef6-153">This script has been uploaded tooan Azure Blob storage account with hello public access.</span></span> <span data-ttu-id="50ef6-154"><a href="#appendix-b">附錄 B</a>的準備和上傳這個檔案 tooyour 自己 Azure Blob 儲存體帳戶的指示。</span><span class="sxs-lookup"><span data-stu-id="50ef6-154"><a href="#appendix-b">Appendix B</a> has instructions on preparing and uploading this file tooyour own Azure Blob storage account.</span></span></td></tr>
<tr><td>wasb://flightdelay@hditutorialdata.blob.core.windows.net/2013Data</td><td><span data-ttu-id="50ef6-155">Hello Hive 工作的輸入的資料。</span><span class="sxs-lookup"><span data-stu-id="50ef6-155">Input data for hello Hive job.</span></span> <span data-ttu-id="50ef6-156">hello 資料已上傳的 tooan hello 公用存取 Azure Blob 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="50ef6-156">hello data has been uploaded tooan Azure Blob storage account with hello public access.</span></span> <span data-ttu-id="50ef6-157"><a href="#appendix-a">附錄 A</a>的指示，取得 hello 資料，並上傳 hello 資料 tooyour 自己 Azure Blob 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="50ef6-157"><a href="#appendix-a">Appendix A</a> has instructions on getting hello data and uploading hello data tooyour own Azure Blob storage account.</span></span></td></tr>
<tr><td><span data-ttu-id="50ef6-158">\tutorials\flightdelays\output</span><span class="sxs-lookup"><span data-stu-id="50ef6-158">\tutorials\flightdelays\output</span></span></td><td><span data-ttu-id="50ef6-159">hello hello Hive 工作的輸出路徑。</span><span class="sxs-lookup"><span data-stu-id="50ef6-159">hello output path for hello Hive job.</span></span> <span data-ttu-id="50ef6-160">hello 預設容器用來儲存 hello 輸出資料。</span><span class="sxs-lookup"><span data-stu-id="50ef6-160">hello default container is used for storing hello output data.</span></span></td></tr>
<tr><td><span data-ttu-id="50ef6-161">\tutorials\flightdelays\jobstatus</span><span class="sxs-lookup"><span data-stu-id="50ef6-161">\tutorials\flightdelays\jobstatus</span></span></td><td><span data-ttu-id="50ef6-162">hello Hive 工作狀態上，資料夾 hello 預設容器。</span><span class="sxs-lookup"><span data-stu-id="50ef6-162">hello Hive job status folder on hello default container.</span></span></td></tr>
</table>

## <a name="create-cluster-and-run-hivesqoop-jobs"></a><span data-ttu-id="50ef6-163">建立叢集和執行 Hive/Sqoop 工作</span><span class="sxs-lookup"><span data-stu-id="50ef6-163">Create cluster and run Hive/Sqoop jobs</span></span>
<span data-ttu-id="50ef6-164">Hadoop MapReduce 是批次處理。</span><span class="sxs-lookup"><span data-stu-id="50ef6-164">Hadoop MapReduce is batch processing.</span></span> <span data-ttu-id="50ef6-165">hello 大部分符合成本效益的方式 toorun Hive 工作是 toocreate 叢集 hello 作業並 hello 工作完成之後刪除 hello 工作。</span><span class="sxs-lookup"><span data-stu-id="50ef6-165">hello most cost-effective way toorun a Hive job is toocreate a cluster for hello job, and delete hello job after hello job is completed.</span></span> <span data-ttu-id="50ef6-166">hello 下列指令碼包含 hello 整個程序。</span><span class="sxs-lookup"><span data-stu-id="50ef6-166">hello following script covers hello whole process.</span></span>
<span data-ttu-id="50ef6-167">如需有關建立 HDInsight 叢集和執行 Hive 工作的詳細資訊，請參閱[在 HDInsight 中建立 Hadoop 叢集][hdinsight-provision]和[搭配 HDInsight 使用 Hive][hdinsight-use-hive]。</span><span class="sxs-lookup"><span data-stu-id="50ef6-167">For more information on creating an HDInsight cluster and running Hive jobs, see [Create Hadoop clusters in HDInsight][hdinsight-provision] and [Use Hive with HDInsight][hdinsight-use-hive].</span></span>

<span data-ttu-id="50ef6-168">**Azure powershell toorun hello Hive 查詢**</span><span class="sxs-lookup"><span data-stu-id="50ef6-168">**toorun hello Hive queries by Azure PowerShell**</span></span>

1. <span data-ttu-id="50ef6-169">使用中的 hello 指示建立 hello Sqoop 作業輸出的 Azure SQL 資料庫與 hello 資料表[旓紵 C](#appendix-c)。</span><span class="sxs-lookup"><span data-stu-id="50ef6-169">Create an Azure SQL database and hello table for hello Sqoop job output by using hello instructions in [Appendix C](#appendix-c).</span></span>
2. <span data-ttu-id="50ef6-170">開啟 Windows PowerShell ISE，然後執行下列指令碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="50ef6-170">Open Windows PowerShell ISE, and run hello following script:</span></span>

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
3. <span data-ttu-id="50ef6-171">連接 tooyour SQL 資料庫，並依城市 hello AvgDelays 資料表中的平均航班延誤請參閱：</span><span class="sxs-lookup"><span data-stu-id="50ef6-171">Connect tooyour SQL database and see average flight delays by city in hello AvgDelays table:</span></span>

    ![HDI.FlightDelays.AvgDelays.Dataset][image-hdi-flightdelays-avgdelays-dataset]

- - -

## <span data-ttu-id="50ef6-173"><a id="appendix-a"></a>附錄 A-上傳飛行延遲資料 tooAzure Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="50ef6-173"><a id="appendix-a"></a>Appendix A - Upload flight delay data tooAzure Blob storage</span></span>
<span data-ttu-id="50ef6-174">上傳 hello 資料檔和 hello 下列 HiveQL 指令碼檔案 (請參閱[附錄 B](#appendix-b)) 需要一些規劃。</span><span class="sxs-lookup"><span data-stu-id="50ef6-174">Uploading hello data file and hello HiveQL script files (see [Appendix B](#appendix-b)) requires some planning.</span></span> <span data-ttu-id="50ef6-175">hello 概念是 toostore hello 資料檔案和 hello HiveQL 檔案之前建立的 HDInsight 叢集和執行 hello Hive 工作。</span><span class="sxs-lookup"><span data-stu-id="50ef6-175">hello idea is toostore hello data files and hello HiveQL file before creating an HDInsight cluster and running hello Hive job.</span></span> <span data-ttu-id="50ef6-176">您有兩個選擇：</span><span class="sxs-lookup"><span data-stu-id="50ef6-176">You have two options:</span></span>

* <span data-ttu-id="50ef6-177">**使用 hello 相同 hello HDInsight 叢集將會使用為 hello 預設檔案系統的 Azure 儲存體帳戶。**</span><span class="sxs-lookup"><span data-stu-id="50ef6-177">**Use hello same Azure Storage account that will be used by hello HDInsight cluster as hello default file system.**</span></span> <span data-ttu-id="50ef6-178">Hello HDInsight 叢集將具有 hello 儲存體帳戶存取金鑰，因為您不需要 toomake 任何其他變更。</span><span class="sxs-lookup"><span data-stu-id="50ef6-178">Because hello HDInsight cluster will have hello Storage account access key, you don't need toomake any additional changes.</span></span>
* <span data-ttu-id="50ef6-179">**使用不同的 Azure 儲存體帳戶，從 hello HDInsight 叢集預設的檔案系統。**</span><span class="sxs-lookup"><span data-stu-id="50ef6-179">**Use a different Azure Storage account from hello HDInsight cluster default file system.**</span></span> <span data-ttu-id="50ef6-180">在 hello 情況下，您必須修改 hello 建立組件的 Windows PowerShell 指令碼中找到 hello[建立 HDInsight 叢集和執行的 Hive/Sqoop 工作](#runjob)toolink hello 與額外的儲存體帳戶的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="50ef6-180">If this is hello case, you must modify hello creation part of hello Windows PowerShell script found in [Create HDInsight cluster and run Hive/Sqoop jobs](#runjob) toolink hello Storage account as an additional Storage account.</span></span> <span data-ttu-id="50ef6-181">如需指示，請參閱[在 HDInsight 中建立 Hadoop 叢集][hdinsight-provision]。</span><span class="sxs-lookup"><span data-stu-id="50ef6-181">For instructions, see [Create Hadoop clusters in HDInsight][hdinsight-provision].</span></span> <span data-ttu-id="50ef6-182">hello HDInsight 叢集就會知道 hello hello 儲存體帳戶的存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="50ef6-182">hello HDInsight cluster then knows hello access key for hello Storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="50ef6-183">hello 的 hello 資料檔是硬式編碼 hello 下列 HiveQL 指令碼檔案中的 Blob 儲存體路徑。</span><span class="sxs-lookup"><span data-stu-id="50ef6-183">hello Blob storage path for hello data file is hard coded in hello HiveQL script file.</span></span> <span data-ttu-id="50ef6-184">您必須據以更新。</span><span class="sxs-lookup"><span data-stu-id="50ef6-184">You must update it accordingly.</span></span>

<span data-ttu-id="50ef6-185">**toodownload hello 飛行資料**</span><span class="sxs-lookup"><span data-stu-id="50ef6-185">**toodownload hello flight data**</span></span>

1. <span data-ttu-id="50ef6-186">瀏覽過[研究和創新的技術管理、 運輸局所免費提供統計][rita-website]。</span><span class="sxs-lookup"><span data-stu-id="50ef6-186">Browse too[Research and Innovative Technology Administration, Bureau of Transportation Statistics][rita-website].</span></span>
2. <span data-ttu-id="50ef6-187">在 hello 頁面上，選取下列值的 hello:</span><span class="sxs-lookup"><span data-stu-id="50ef6-187">On hello page, select hello following values:</span></span>

    <table border="1">
    <tr><th><span data-ttu-id="50ef6-188">名稱</span><span class="sxs-lookup"><span data-stu-id="50ef6-188">Name</span></span></th><th><span data-ttu-id="50ef6-189">值</span><span class="sxs-lookup"><span data-stu-id="50ef6-189">Value</span></span></th></tr>
    <tr><td><span data-ttu-id="50ef6-190">篩選年份</span><span class="sxs-lookup"><span data-stu-id="50ef6-190">Filter Year</span></span></td><td><span data-ttu-id="50ef6-191">2013</span><span class="sxs-lookup"><span data-stu-id="50ef6-191">2013</span></span> </td></tr>
    <tr><td><span data-ttu-id="50ef6-192">篩選期間</span><span class="sxs-lookup"><span data-stu-id="50ef6-192">Filter Period</span></span></td><td><span data-ttu-id="50ef6-193">一月</span><span class="sxs-lookup"><span data-stu-id="50ef6-193">January</span></span></td></tr>
    <tr><td><span data-ttu-id="50ef6-194">欄位</span><span class="sxs-lookup"><span data-stu-id="50ef6-194">Fields</span></span></td><td><span data-ttu-id="50ef6-195">*Year*、*FlightDate*、*UniqueCarrier*、*Carrier*、*FlightNum*、*OriginAirportID*、*Origin*、*OriginCityName*、*OriginState*、*DestAirportID*、*Dest*、*DestCityName*、*DestState*、*DepDelayMinutes*、*ArrDelay*、*ArrDelayMinutes*、*CarrierDelay*、*WeatherDelay*、*NASDelay*、*SecurityDelay*、*LateAircraftDelay* (請清除其餘所有欄位)</span><span class="sxs-lookup"><span data-stu-id="50ef6-195">*Year*, *FlightDate*, *UniqueCarrier*, *Carrier*, *FlightNum*, *OriginAirportID*, *Origin*, *OriginCityName*, *OriginState*, *DestAirportID*, *Dest*, *DestCityName*, *DestState*, *DepDelayMinutes*, *ArrDelay*, *ArrDelayMinutes*, *CarrierDelay*, *WeatherDelay*, *NASDelay*, *SecurityDelay*, *LateAircraftDelay* (clear all other fields)</span></span></td></tr>
    </table><span data-ttu-id="50ef6-196">
3. 按一下 **下載**。</span><span class="sxs-lookup"><span data-stu-id="50ef6-196">
3. Click **Download**.</span></span>
<span data-ttu-id="50ef6-197">4.</span><span class="sxs-lookup"><span data-stu-id="50ef6-197">4.</span></span> <span data-ttu-id="50ef6-198">解壓縮 hello 檔案 toohello **C:\Tutorials\FlightDelay\2013Data**資料夾。</span><span class="sxs-lookup"><span data-stu-id="50ef6-198">Unzip hello file toohello **C:\Tutorials\FlightDelay\2013Data** folder.</span></span> <span data-ttu-id="50ef6-199">每個檔案皆為 CSV 檔案，大小約為 60 GB。</span><span class="sxs-lookup"><span data-stu-id="50ef6-199">Each file is a CSV file and is approximately 60GB in size.</span></span>
<span data-ttu-id="50ef6-200">5.</span><span class="sxs-lookup"><span data-stu-id="50ef6-200">5.</span></span> <span data-ttu-id="50ef6-201">它包含資料的 hello 月份 hello 檔案 toohello 名稱重新命名。</span><span class="sxs-lookup"><span data-stu-id="50ef6-201">Rename hello file toohello name of hello month that it contains data for.</span></span> <span data-ttu-id="50ef6-202">例如，包含 hello 年 1 月資料的 hello 檔案會命名為*January.csv*。</span><span class="sxs-lookup"><span data-stu-id="50ef6-202">For example, hello file containing hello January data would be named *January.csv*.</span></span>
<span data-ttu-id="50ef6-203">6.</span><span class="sxs-lookup"><span data-stu-id="50ef6-203">6.</span></span> <span data-ttu-id="50ef6-204">針對每個 hello 2013 中的 12 個月重複執行步驟 2 和 5 toodownload 檔案。</span><span class="sxs-lookup"><span data-stu-id="50ef6-204">Repeat steps 2 and 5 toodownload a file for each of hello 12 months in 2013.</span></span> <span data-ttu-id="50ef6-205">您必須至少有一個檔案 toorun hello 教學課程。</span><span class="sxs-lookup"><span data-stu-id="50ef6-205">You will need a minimum of one file toorun hello tutorial.</span></span>

<span data-ttu-id="50ef6-206">**tooupload hello 飛行延遲資料 tooAzure Blob 儲存體**</span><span class="sxs-lookup"><span data-stu-id="50ef6-206">**tooupload hello flight delay data tooAzure Blob storage**</span></span>

1. <span data-ttu-id="50ef6-207">準備 hello 參數：</span><span class="sxs-lookup"><span data-stu-id="50ef6-207">Prepare hello parameters:</span></span>

    <table border="1">
    <tr><th><span data-ttu-id="50ef6-208">變數名稱</span><span class="sxs-lookup"><span data-stu-id="50ef6-208">Variable Name</span></span></th><th><span data-ttu-id="50ef6-209">注意事項</span><span class="sxs-lookup"><span data-stu-id="50ef6-209">Notes</span></span></th></tr>
    <tr><td><span data-ttu-id="50ef6-210">$storageAccountName</span><span class="sxs-lookup"><span data-stu-id="50ef6-210">$storageAccountName</span></span></td><td><span data-ttu-id="50ef6-211">hello tooupload hello 資料所在的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="50ef6-211">hello Azure Storage account where you want tooupload hello data to.</span></span></td></tr>
    <tr><td><span data-ttu-id="50ef6-212">$blobContainerName</span><span class="sxs-lookup"><span data-stu-id="50ef6-212">$blobContainerName</span></span></td><td><span data-ttu-id="50ef6-213">您想要 tooupload hello 資料 hello Blob 容器。</span><span class="sxs-lookup"><span data-stu-id="50ef6-213">hello Blob container where you want tooupload hello data to.</span></span></td></tr>
    </table>
2. <span data-ttu-id="50ef6-214">開啟 Azure PowerShell ISE。</span><span class="sxs-lookup"><span data-stu-id="50ef6-214">Open Azure PowerShell ISE.</span></span>
<span data-ttu-id="50ef6-215">3.</span><span class="sxs-lookup"><span data-stu-id="50ef6-215">3.</span></span> <span data-ttu-id="50ef6-216">貼上下列指令碼到 hello 指令碼窗格中的 hello:</span><span class="sxs-lookup"><span data-stu-id="50ef6-216">Paste hello following script into hello script pane:</span></span>

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
4. <span data-ttu-id="50ef6-217">按**F5** toorun hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="50ef6-217">Press **F5** toorun hello script.</span></span>

<span data-ttu-id="50ef6-218">如果您選擇 toouse hello 檔案上傳不同的方法，請確定 hello 檔案路徑是教學課程/flightdelay 資料。</span><span class="sxs-lookup"><span data-stu-id="50ef6-218">If you choose toouse a different method for uploading hello files, please make sure hello file path is tutorials/flightdelay/data.</span></span> <span data-ttu-id="50ef6-219">hello 存取 hello 檔案的語法為：</span><span class="sxs-lookup"><span data-stu-id="50ef6-219">hello syntax for accessing hello files is:</span></span>

    wasb://<ContainerName>@<StorageAccountName>.blob.core.windows.net/tutorials/flightdelay/data

<span data-ttu-id="50ef6-220">hello 路徑教學課程/flightdelay/資料是 hello hello 檔案上傳時所建立的虛擬資料夾。</span><span class="sxs-lookup"><span data-stu-id="50ef6-220">hello path tutorials/flightdelay/data is hello virtual folder you created when you uploaded hello files.</span></span> <span data-ttu-id="50ef6-221">請確認共有 12 個檔案，每個月份各一個。</span><span class="sxs-lookup"><span data-stu-id="50ef6-221">Verify that there are 12 files, one for each month.</span></span>

> [!NOTE]
> <span data-ttu-id="50ef6-222">您必須更新 hello Hive 查詢 tooread 從 hello 新位置。</span><span class="sxs-lookup"><span data-stu-id="50ef6-222">You must update hello Hive query tooread from hello new location.</span></span>
>
> <span data-ttu-id="50ef6-223">您必須設定 hello 容器存取權限 toobe 公用，或繫結 hello 儲存體帳戶 toohello HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="50ef6-223">You must either configure hello container access permission toobe public or bind hello Storage account toohello HDInsight cluster.</span></span> <span data-ttu-id="50ef6-224">否則，hello Hive 查詢字串不會無法 tooaccess hello 資料檔案。</span><span class="sxs-lookup"><span data-stu-id="50ef6-224">Otherwise, hello Hive query string will not be able tooaccess hello data files.</span></span>

- - -

## <span data-ttu-id="50ef6-225"><a id="appendix-b"></a>附錄 B - 建立及上傳 HiveQL 指令碼</span><span class="sxs-lookup"><span data-stu-id="50ef6-225"><a id="appendix-b"></a>Appendix B - Create and upload a HiveQL script</span></span>
<span data-ttu-id="50ef6-226">使用 Azure PowerShell，您可以執行多個下列 HiveQL 陳述式一次，或封裝 hello HiveQL 陳述式到指令碼檔案。</span><span class="sxs-lookup"><span data-stu-id="50ef6-226">Using Azure PowerShell, you can run multiple HiveQL statements one at a time, or package hello HiveQL statement into a script file.</span></span> <span data-ttu-id="50ef6-227">本節說明如何 toocreate 下列 HiveQL 指令碼和上傳 hello 編寫指令碼 tooAzure Blob 儲存體使用 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="50ef6-227">This section shows you how toocreate a HiveQL script and upload hello script tooAzure Blob storage by using Azure PowerShell.</span></span> <span data-ttu-id="50ef6-228">Hive 需要 Azure Blob 儲存體中的 hello 下列 HiveQL 指令碼 toobe。</span><span class="sxs-lookup"><span data-stu-id="50ef6-228">Hive requires hello HiveQL scripts toobe stored in Azure Blob storage.</span></span>

<span data-ttu-id="50ef6-229">hello 下列 HiveQL 指令碼將會執行下列 hello:</span><span class="sxs-lookup"><span data-stu-id="50ef6-229">hello HiveQL script will perform hello following:</span></span>

1. <span data-ttu-id="50ef6-230">**卸除 hello delays_raw 資料表**，以防 hello 資料表已經存在。</span><span class="sxs-lookup"><span data-stu-id="50ef6-230">**Drop hello delays_raw table**, in case hello table already exists.</span></span>
2. <span data-ttu-id="50ef6-231">**建立 hello delays_raw 外部的 Hive 資料表**hello 飛行延遲檔案以指出 toohello Blob 儲存體位置。</span><span class="sxs-lookup"><span data-stu-id="50ef6-231">**Create hello delays_raw external Hive table** pointing toohello Blob storage location with hello flight delay files.</span></span> <span data-ttu-id="50ef6-232">此查詢會指定欄位將以 "," 分隔，且每一行都會以 "\n" 結尾。</span><span class="sxs-lookup"><span data-stu-id="50ef6-232">This query specifies that fields are delimited by "," and that lines are terminated by "\n".</span></span> <span data-ttu-id="50ef6-233">這會造成問題，當欄位值包含逗號，因為登錄區無法分辨是欄位分隔符號逗號和一個屬於欄位值 (這是來源的欄位值中的 hello 案例\_縣 （市)\_名稱和目的地\_縣 （市)\_名稱)。</span><span class="sxs-lookup"><span data-stu-id="50ef6-233">This poses a problem when field values contain commas because Hive cannot differentiate between a comma that is a field delimiter and a one that is part of a field value (which is hello case in field values for ORIGIN\_CITY\_NAME and DEST\_CITY\_NAME).</span></span> <span data-ttu-id="50ef6-234">tooaddress hello，查詢會建立暫存資料行未正確分割成資料行的 toohold 資料。</span><span class="sxs-lookup"><span data-stu-id="50ef6-234">tooaddress this, hello query creates TEMP columns toohold data that is incorrectly split into columns.</span></span>
3. <span data-ttu-id="50ef6-235">**卸除 hello 延遲資料表**，以防 hello 資料表已經存在。</span><span class="sxs-lookup"><span data-stu-id="50ef6-235">**Drop hello delays table**, in case hello table already exists.</span></span>
4. <span data-ttu-id="50ef6-236">**建立 hello 延遲資料表**。</span><span class="sxs-lookup"><span data-stu-id="50ef6-236">**Create hello delays table**.</span></span> <span data-ttu-id="50ef6-237">很有幫助 tooclean hello 資料再進一步處理。</span><span class="sxs-lookup"><span data-stu-id="50ef6-237">It is helpful tooclean up hello data before further processing.</span></span> <span data-ttu-id="50ef6-238">此查詢建立新的資料表，*延遲*，hello delays_raw 資料表中。</span><span class="sxs-lookup"><span data-stu-id="50ef6-238">This query creates a new table, *delays*, from hello delays_raw table.</span></span> <span data-ttu-id="50ef6-239">請注意，不會複製 hello 暫存資料行 （如先前所述），以及該 hello **substring**函式是從 hello 資料使用的 tooremove 引號。</span><span class="sxs-lookup"><span data-stu-id="50ef6-239">Note that hello TEMP columns (as mentioned previously) are not copied, and that hello **substring** function is used tooremove quotation marks from hello data.</span></span>
5. <span data-ttu-id="50ef6-240">**計算 hello 平均天氣延遲和群組 hello 結果依城市名稱。**</span><span class="sxs-lookup"><span data-stu-id="50ef6-240">**Compute hello average weather delay and groups hello results by city name.**</span></span> <span data-ttu-id="50ef6-241">它也會輸出 hello 結果 tooBlob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="50ef6-241">It will also output hello results tooBlob storage.</span></span> <span data-ttu-id="50ef6-242">請注意該 hello 查詢將會從 hello 資料移除所有格符號，並且排除 hello 其中值的資料列**weather_delay**為 null。</span><span class="sxs-lookup"><span data-stu-id="50ef6-242">Note that hello query will remove apostrophes from hello data and will exclude rows where hello value for **weather_delay** is null.</span></span> <span data-ttu-id="50ef6-243">這是必要動作，因為 Sqoop (稍後使用於本教學課程) 預設不會正常處理這些值。</span><span class="sxs-lookup"><span data-stu-id="50ef6-243">This is necessary because Sqoop, used later in this tutorial, doesn't handle those values gracefully by default.</span></span>

<span data-ttu-id="50ef6-244">Hello HiveQL 命令的完整清單，請參閱[hive 控制檔的資料定義語言][hadoop-hiveql]。</span><span class="sxs-lookup"><span data-stu-id="50ef6-244">For a full list of hello HiveQL commands, see [Hive Data Definition Language][hadoop-hiveql].</span></span> <span data-ttu-id="50ef6-245">每個 HiveQL 命令都必須以分號結尾。</span><span class="sxs-lookup"><span data-stu-id="50ef6-245">Each HiveQL command must terminate with a semicolon.</span></span>

<span data-ttu-id="50ef6-246">**toocreate 下列 HiveQL 指令碼檔案**</span><span class="sxs-lookup"><span data-stu-id="50ef6-246">**toocreate a HiveQL script file**</span></span>

1. <span data-ttu-id="50ef6-247">準備 hello 參數：</span><span class="sxs-lookup"><span data-stu-id="50ef6-247">Prepare hello parameters:</span></span>

    <table border="1">
    <tr><th><span data-ttu-id="50ef6-248">變數名稱</span><span class="sxs-lookup"><span data-stu-id="50ef6-248">Variable Name</span></span></th><th><span data-ttu-id="50ef6-249">注意事項</span><span class="sxs-lookup"><span data-stu-id="50ef6-249">Notes</span></span></th></tr>
    <tr><td><span data-ttu-id="50ef6-250">$storageAccountName</span><span class="sxs-lookup"><span data-stu-id="50ef6-250">$storageAccountName</span></span></td><td><span data-ttu-id="50ef6-251">hello tooupload hello 下列 HiveQL 指令碼所在的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="50ef6-251">hello Azure Storage account where you want tooupload hello HiveQL script to.</span></span></td></tr>
    <tr><td><span data-ttu-id="50ef6-252">$blobContainerName</span><span class="sxs-lookup"><span data-stu-id="50ef6-252">$blobContainerName</span></span></td><td><span data-ttu-id="50ef6-253">您想要 tooupload hello 下列 HiveQL 指令碼，以 hello Blob 容器。</span><span class="sxs-lookup"><span data-stu-id="50ef6-253">hello Blob container where you want tooupload hello HiveQL script to.</span></span></td></tr>
    </table>
2. <span data-ttu-id="50ef6-254">開啟 Azure PowerShell ISE。</span><span class="sxs-lookup"><span data-stu-id="50ef6-254">Open Azure PowerShell ISE.</span></span>
<span data-ttu-id="50ef6-255">3.</span><span class="sxs-lookup"><span data-stu-id="50ef6-255">3.</span></span> <span data-ttu-id="50ef6-256">複製並貼上下列指令碼到 hello 指令碼窗格中的 hello:</span><span class="sxs-lookup"><span data-stu-id="50ef6-256">Copy and paste hello following script into hello script pane:</span></span>

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

    <span data-ttu-id="50ef6-257">以下是使用 hello 指令碼中的 hello 變數：</span><span class="sxs-lookup"><span data-stu-id="50ef6-257">Here are hello variables used in hello script:</span></span>

   * <span data-ttu-id="50ef6-258">**$hqlLocalFileName** -hello 指令碼 hello HiveQL 指令碼會將檔案儲存在本機之前將它上傳 tooBlob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="50ef6-258">**$hqlLocalFileName** - hello script saves hello HiveQL script file locally before uploading it tooBlob storage.</span></span> <span data-ttu-id="50ef6-259">這是 hello 檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="50ef6-259">This is hello file name.</span></span> <span data-ttu-id="50ef6-260">hello 預設值是<u>C:\tutorials\flightdelay\flightdelays.hql</u>。</span><span class="sxs-lookup"><span data-stu-id="50ef6-260">hello default value is <u>C:\tutorials\flightdelay\flightdelays.hql</u>.</span></span>
   * <span data-ttu-id="50ef6-261">**$hqlBlobName** -這是 hello 下列 HiveQL 指令碼檔案 blob 名稱 hello Azure Blob 儲存體中使用。</span><span class="sxs-lookup"><span data-stu-id="50ef6-261">**$hqlBlobName** - This is hello HiveQL script file blob name used in hello Azure Blob storage.</span></span> <span data-ttu-id="50ef6-262">hello 預設值為 tutorials/flightdelay/flightdelays.hql。</span><span class="sxs-lookup"><span data-stu-id="50ef6-262">hello default value is tutorials/flightdelay/flightdelays.hql.</span></span> <span data-ttu-id="50ef6-263">Hello 檔會寫入直接 tooAzure Blob 儲存體，因為沒有"/"開頭 hello hello blob 名稱。</span><span class="sxs-lookup"><span data-stu-id="50ef6-263">Because hello file will be written directly tooAzure Blob storage, there is NOT a "/" at hello beginning of hello blob name.</span></span> <span data-ttu-id="50ef6-264">如果您想 tooaccess hello 檔案從 Blob 儲存體，您需要 tooadd"/"開頭 hello hello 檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="50ef6-264">If you want tooaccess hello file from Blob storage, you will need tooadd a "/" at hello beginning of hello file name.</span></span>
   * <span data-ttu-id="50ef6-265">**$srcDataFolder** 和 **$dstDataFolder** - = "tutorials/flightdelay/data" = "tutorials/flightdelay/output"</span><span class="sxs-lookup"><span data-stu-id="50ef6-265">**$srcDataFolder** and **$dstDataFolder** - = "tutorials/flightdelay/data" = "tutorials/flightdelay/output"</span></span>

- - -
## <span data-ttu-id="50ef6-266"><a id="appendix-c"></a>附錄 C-將 Azure SQL database 準備 hello Sqoop 作業輸出</span><span class="sxs-lookup"><span data-stu-id="50ef6-266"><a id="appendix-c"></a>Appendix C - Prepare an Azure SQL database for hello Sqoop job output</span></span>
<span data-ttu-id="50ef6-267">**tooprepare hello SQL 資料庫 （這與合併 hello Sqoop 指令碼）**</span><span class="sxs-lookup"><span data-stu-id="50ef6-267">**tooprepare hello SQL database (merge this with hello Sqoop script)**</span></span>

1. <span data-ttu-id="50ef6-268">準備 hello 參數：</span><span class="sxs-lookup"><span data-stu-id="50ef6-268">Prepare hello parameters:</span></span>

    <table border="1">
    <tr><th><span data-ttu-id="50ef6-269">變數名稱</span><span class="sxs-lookup"><span data-stu-id="50ef6-269">Variable Name</span></span></th><th><span data-ttu-id="50ef6-270">注意事項</span><span class="sxs-lookup"><span data-stu-id="50ef6-270">Notes</span></span></th></tr>
    <tr><td><span data-ttu-id="50ef6-271">$sqlDatabaseServerName</span><span class="sxs-lookup"><span data-stu-id="50ef6-271">$sqlDatabaseServerName</span></span></td><td><span data-ttu-id="50ef6-272">hello hello Azure SQL database 伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="50ef6-272">hello name of hello Azure SQL database server.</span></span> <span data-ttu-id="50ef6-273">輸入任何 toocreate 新的伺服器。</span><span class="sxs-lookup"><span data-stu-id="50ef6-273">Enter nothing toocreate a new server.</span></span></td></tr>
    <tr><td><span data-ttu-id="50ef6-274">$sqlDatabaseUsername</span><span class="sxs-lookup"><span data-stu-id="50ef6-274">$sqlDatabaseUsername</span></span></td><td><span data-ttu-id="50ef6-275">hello hello Azure SQL database 伺服器的登入名稱。</span><span class="sxs-lookup"><span data-stu-id="50ef6-275">hello login name for hello Azure SQL database server.</span></span> <span data-ttu-id="50ef6-276">如果 $sqlDatabaseServerName 是現有的伺服器，hello 登入和登入密碼。 使用的 tooauthenticate 與 hello 伺服器</span><span class="sxs-lookup"><span data-stu-id="50ef6-276">If $sqlDatabaseServerName is an existing server, hello login and login password are used tooauthenticate with hello server.</span></span> <span data-ttu-id="50ef6-277">否則，它們會使用的 toocreate 新的伺服器。</span><span class="sxs-lookup"><span data-stu-id="50ef6-277">Otherwise they are used toocreate a new server.</span></span></td></tr>
    <tr><td><span data-ttu-id="50ef6-278">$sqlDatabasePassword</span><span class="sxs-lookup"><span data-stu-id="50ef6-278">$sqlDatabasePassword</span></span></td><td><span data-ttu-id="50ef6-279">hello hello Azure SQL database 伺服器的登入密碼。</span><span class="sxs-lookup"><span data-stu-id="50ef6-279">hello login password for hello Azure SQL database server.</span></span></td></tr>
    <tr><td><span data-ttu-id="50ef6-280">$sqlDatabaseLocation</span><span class="sxs-lookup"><span data-stu-id="50ef6-280">$sqlDatabaseLocation</span></span></td><td><span data-ttu-id="50ef6-281">只有在建立新的 Azure 資料庫伺服器時才會使用此值。</span><span class="sxs-lookup"><span data-stu-id="50ef6-281">This value is used only when you're creating a new Azure database server.</span></span></td></tr>
    <tr><td><span data-ttu-id="50ef6-282">$sqlDatabaseName</span><span class="sxs-lookup"><span data-stu-id="50ef6-282">$sqlDatabaseName</span></span></td><td><span data-ttu-id="50ef6-283">hello SQL database 會將 toocreate hello AvgDelays 資料表用於 hello Sqoop 工作。</span><span class="sxs-lookup"><span data-stu-id="50ef6-283">hello SQL database used toocreate hello AvgDelays table for hello Sqoop job.</span></span> <span data-ttu-id="50ef6-284">保留空白會建立名為 HDISqoop 的資料庫。</span><span class="sxs-lookup"><span data-stu-id="50ef6-284">Leaving it blank will create a database called HDISqoop.</span></span> <span data-ttu-id="50ef6-285">hello Sqoop 作業輸出的 hello 資料表名稱是 AvgDelays。</span><span class="sxs-lookup"><span data-stu-id="50ef6-285">hello table name for hello Sqoop job output is AvgDelays.</span></span> </td></tr>
    </table>
2. <span data-ttu-id="50ef6-286">開啟 Azure PowerShell ISE。</span><span class="sxs-lookup"><span data-stu-id="50ef6-286">Open Azure PowerShell ISE.</span></span>
<span data-ttu-id="50ef6-287">3.</span><span class="sxs-lookup"><span data-stu-id="50ef6-287">3.</span></span> <span data-ttu-id="50ef6-288">複製並貼上下列指令碼到 hello 指令碼窗格中的 hello:</span><span class="sxs-lookup"><span data-stu-id="50ef6-288">Copy and paste hello following script into hello script pane:</span></span>

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
   > <span data-ttu-id="50ef6-289">hello 指令碼會使用具像狀態傳輸 (REST) 服務、 http://bot.whatismyipaddress.com、 tooretrieve 外部的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="50ef6-289">hello script uses a representational state transfer (REST) service, http://bot.whatismyipaddress.com, tooretrieve your external IP address.</span></span> <span data-ttu-id="50ef6-290">hello IP 位址用來建立 SQL 資料庫伺服器的防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="50ef6-290">hello IP address is used for creating a firewall rule for your SQL database server.</span></span>

    <span data-ttu-id="50ef6-291">以下是一些 hello 指令碼中使用的變數：</span><span class="sxs-lookup"><span data-stu-id="50ef6-291">Here are some variables used in hello script:</span></span>

   * <span data-ttu-id="50ef6-292">**$ipAddressRestService** -hello 預設值是 http://bot.whatismyipaddress.com。這是用來取得外部 IP 位址的公用 IP 位址 REST 服務。</span><span class="sxs-lookup"><span data-stu-id="50ef6-292">**$ipAddressRestService** - hello default value is http://bot.whatismyipaddress.com. It is a public IP address REST service for getting your external IP address.</span></span> <span data-ttu-id="50ef6-293">想要的話，您可以使用其他服務。</span><span class="sxs-lookup"><span data-stu-id="50ef6-293">You can use other services if you want.</span></span> <span data-ttu-id="50ef6-294">hello hello 服務透過擷取外部 IP 位址將會使用的 toocreate Azure SQL 資料庫伺服器的防火牆規則，以便您可以從您的工作站存取 hello 資料庫 （透過使用 Windows PowerShell 指令碼）。</span><span class="sxs-lookup"><span data-stu-id="50ef6-294">hello external IP address retrieved through hello service will be used toocreate a firewall rule for your Azure SQL database server, so that you can access hello database from your workstation (by using a Windows PowerShell script).</span></span>
   * <span data-ttu-id="50ef6-295">**$fireWallRuleName** -這是 hello hello 防火牆規則 hello Azure SQL 資料庫伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="50ef6-295">**$fireWallRuleName** - This is hello name of hello firewall rule for hello Azure SQL database server.</span></span> <span data-ttu-id="50ef6-296">hello 預設名稱是<u>FlightDelay</u>。</span><span class="sxs-lookup"><span data-stu-id="50ef6-296">hello default name is <u>FlightDelay</u>.</span></span> <span data-ttu-id="50ef6-297">想要的話，您可以將它重新命名。</span><span class="sxs-lookup"><span data-stu-id="50ef6-297">You can rename it if you want.</span></span>
   * <span data-ttu-id="50ef6-298">**$sqlDatabaseMaxSizeGB** - 只有在建立新的 Azure SQL Database 伺服器時才會使用此值。</span><span class="sxs-lookup"><span data-stu-id="50ef6-298">**$sqlDatabaseMaxSizeGB** - This value is used only when you're creating a new Azure SQL database server.</span></span> <span data-ttu-id="50ef6-299">hello 預設值為 10 GB。</span><span class="sxs-lookup"><span data-stu-id="50ef6-299">hello default value is 10GB.</span></span> <span data-ttu-id="50ef6-300">10GB 足夠供本教學課程使用。</span><span class="sxs-lookup"><span data-stu-id="50ef6-300">10GB is sufficient for this tutorial.</span></span>
   * <span data-ttu-id="50ef6-301">**$sqlDatabaseName** - 只有在建立新的 Azure SQL Database 時才會使用此值。</span><span class="sxs-lookup"><span data-stu-id="50ef6-301">**$sqlDatabaseName** - This value is used only when you're creating a new Azure SQL database.</span></span> <span data-ttu-id="50ef6-302">hello 預設值為 HDISqoop。</span><span class="sxs-lookup"><span data-stu-id="50ef6-302">hello default value is HDISqoop.</span></span> <span data-ttu-id="50ef6-303">如果您將它重新命名時，您必須跟著更新 hello Sqoop Windows PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="50ef6-303">If you rename it, you must update hello Sqoop Windows PowerShell script accordingly.</span></span>
4. <span data-ttu-id="50ef6-304">按**F5** toorun hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="50ef6-304">Press **F5** toorun hello script.</span></span>
5. <span data-ttu-id="50ef6-305">驗證 hello 指令碼輸出。</span><span class="sxs-lookup"><span data-stu-id="50ef6-305">Validate hello script output.</span></span> <span data-ttu-id="50ef6-306">請確定 hello 指令碼已順利執行。</span><span class="sxs-lookup"><span data-stu-id="50ef6-306">Make sure hello script ran successfully.</span></span>

## <span data-ttu-id="50ef6-307"><a id="nextsteps"></a> 後續步驟</span><span class="sxs-lookup"><span data-stu-id="50ef6-307"><a id="nextsteps"></a> Next steps</span></span>
<span data-ttu-id="50ef6-308">現在您已了解如何 tooupload 檔案 tooAzure Blob 儲存體，如何使用 Azure Blob 儲存體中的 hello 資料 toopopulate Hive 資料表如何 toorun Hive 查詢，以及如何 toouse Sqoop tooexport 資料從 HDFS tooan Azure SQL database。</span><span class="sxs-lookup"><span data-stu-id="50ef6-308">Now you understand how tooupload a file tooAzure Blob storage, how toopopulate a Hive table by using hello data from Azure Blob storage, how toorun Hive queries, and how toouse Sqoop tooexport data from HDFS tooan Azure SQL database.</span></span> <span data-ttu-id="50ef6-309">toolearn 詳細資訊，請參閱下列文章 hello:</span><span class="sxs-lookup"><span data-stu-id="50ef6-309">toolearn more, see hello following articles:</span></span>

* <span data-ttu-id="50ef6-310">[開始使用 HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="50ef6-310">[Get started with HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="50ef6-311">[搭配 HDInsight 使用 Hivet][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="50ef6-311">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="50ef6-312">[搭配 HDInsight 使用 Oozie][hdinsight-use-oozie]</span><span class="sxs-lookup"><span data-stu-id="50ef6-312">[Use Oozie with HDInsight][hdinsight-use-oozie]</span></span>
* <span data-ttu-id="50ef6-313">[搭配 HDInsight 使用 Sqoop][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="50ef6-313">[Use Sqoop with HDInsight][hdinsight-use-sqoop]</span></span>
* <span data-ttu-id="50ef6-314">[搭配 HDInsight 使用 Pig][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="50ef6-314">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="50ef6-315">[開發 HDInsight 的 Java MapReduce 程式][hdinsight-develop-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="50ef6-315">[Develop Java MapReduce programs for HDInsight][hdinsight-develop-mapreduce]</span></span>

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
