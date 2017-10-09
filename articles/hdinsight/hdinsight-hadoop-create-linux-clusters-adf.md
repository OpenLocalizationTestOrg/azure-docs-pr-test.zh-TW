---
title: "使用 Data Factory-Azure HDInsight 隨 Hadoop 叢集的 aaaCreate |Microsoft 文件"
description: "了解如何 toocreate 隨 Hadoop 叢集 HDInsight 使用 Azure Data Factory 中。"
services: hdinsight
documentationcenter: 
tags: azure-portal
author: spelluru
manager: jhubbard
editor: cgronlun
ms.assetid: 1f3b3a78-4d16-4d99-ba6e-06f7bb185d6a
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/20/2017
ms.author: spelluru
ms.openlocfilehash: c869776ac270e37dec710b5fc8d2a792d9263129
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-on-demand-hadoop-clusters-in-hdinsight-using-azure-data-factory"></a><span data-ttu-id="e7df7-103">使用 Azure Data Factory 在 HDInsight 中建立隨選 Handooop 叢集</span><span class="sxs-lookup"><span data-stu-id="e7df7-103">Create on-demand Hadoop clusters in HDInsight using Azure Data Factory</span></span>
[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="e7df7-104">[Azure Data Factory](../data-factory/data-factory-introduction.md)是以雲端為基礎的資料整合服務會協調及自動 hello 移動和轉換資料。</span><span class="sxs-lookup"><span data-stu-id="e7df7-104">[Azure Data Factory](../data-factory/data-factory-introduction.md) is a cloud-based data integration service that orchestrates and automates hello movement and transformation of data.</span></span> <span data-ttu-id="e7df7-105">它可建立 HDInsight Hadoop 叢集在 just-in-time tooprocess 輸入的資料配量，及 hello 處理序完成時刪除 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="e7df7-105">It can create a HDInsight Hadoop cluster just-in-time tooprocess an input data slice and delete hello cluster when hello processing is complete.</span></span> <span data-ttu-id="e7df7-106">使用隨 HDInsight Hadoop 叢集的 hello 優點包括：</span><span class="sxs-lookup"><span data-stu-id="e7df7-106">Some of hello benefits of using an on-demand HDInsight Hadoop cluster are:</span></span>

- <span data-ttu-id="e7df7-107">您只有工資 hello 計時器工作執行的 hello HDInsight Hadoop 叢集 （以及簡短的可設定閒置時間）。</span><span class="sxs-lookup"><span data-stu-id="e7df7-107">You only pay for hello time job is running on hello HDInsight Hadoop cluster (plus a brief configurable idle time).</span></span> <span data-ttu-id="e7df7-108">HDInsight 叢集的 hello 計費被一下每分鐘，不論您或不使用它們。</span><span class="sxs-lookup"><span data-stu-id="e7df7-108">hello billing for HDInsight clusters is pro-rated per minute, whether you are using them or not.</span></span> <span data-ttu-id="e7df7-109">當您使用隨 HDInsight 連結服務 Data Factory 中時，視頁面時，會建立 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="e7df7-109">When you use an on-demand HDInsight linked service in Data Factory, hello clusters are created on-demand.</span></span> <span data-ttu-id="e7df7-110">和 hello 叢集 hello 工作都完成之後會自動刪除。</span><span class="sxs-lookup"><span data-stu-id="e7df7-110">And hello clusters are deleted automatically when hello jobs are completed.</span></span> <span data-ttu-id="e7df7-111">因此，您只需支付 hello 作業執行時間和 hello 簡短閒置時間 （存留時間設定）。</span><span class="sxs-lookup"><span data-stu-id="e7df7-111">Therefore, you only pay for hello job running time and hello brief idle time (time-to-live setting).</span></span>
- <span data-ttu-id="e7df7-112">您可以使用 Data Factory 管線建立工作流程。</span><span class="sxs-lookup"><span data-stu-id="e7df7-112">You can create a workflow using a Data Factory pipeline.</span></span> <span data-ttu-id="e7df7-113">例如，您可以從 Azure blob 儲存體，視 HDInsight Hadoop 叢集上執行 Hive 指令碼和 Pig 指令碼處理 hello 資料在內部部署 SQL Server tooan hello 管線 toocopy 資料。</span><span class="sxs-lookup"><span data-stu-id="e7df7-113">For example, you can have hello pipeline toocopy data from an on-premises SQL Server tooan Azure blob storage, process hello data by running a Hive script and a Pig script on an on-demand HDInsight Hadoop cluster.</span></span> <span data-ttu-id="e7df7-114">接著，複製 hello 結果資料 tooan BI 應用程式 tooconsume for Azure SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="e7df7-114">Then, copy hello result data tooan Azure SQL Data Warehouse for BI applications tooconsume.</span></span>
- <span data-ttu-id="e7df7-115">您可以排程 hello 工作流程 toorun 定期 （每小時、 每天、 每週、 每月等）。</span><span class="sxs-lookup"><span data-stu-id="e7df7-115">You can schedule hello workflow toorun periodically (hourly, daily, weekly, monthly, etc.).</span></span>

<span data-ttu-id="e7df7-116">在 Azure Data Factory 中，資料處理站可以有一或多個資料管線。</span><span class="sxs-lookup"><span data-stu-id="e7df7-116">In Azure Data Factory, a data factory can have one or more data pipelines.</span></span> <span data-ttu-id="e7df7-117">資料管線具有一或多個活動。</span><span class="sxs-lookup"><span data-stu-id="e7df7-117">A data pipeline has one or more activities.</span></span> <span data-ttu-id="e7df7-118">兩種活動類型︰[資料移動活動](../data-factory/data-factory-data-movement-activities.md)和[資料轉換活動](../data-factory/data-factory-data-transformation-activities.md)。</span><span class="sxs-lookup"><span data-stu-id="e7df7-118">There are two types of activities: [Data Movement Activities](../data-factory/data-factory-data-movement-activities.md) and [Data Transformation Activities](../data-factory/data-factory-data-transformation-activities.md).</span></span> <span data-ttu-id="e7df7-119">您可以使用資料移動的活動 （目前，只複製活動） toomove 資料來源建立資料存放區 tooa 目的地資料存放區。</span><span class="sxs-lookup"><span data-stu-id="e7df7-119">You use data movement activities (currently, only Copy Activity) toomove data from a source data store tooa destination data store.</span></span> <span data-ttu-id="e7df7-120">您使用資料轉換活動 tootransform/處理序資料。</span><span class="sxs-lookup"><span data-stu-id="e7df7-120">You use data transformation activities tootransform/process data.</span></span> <span data-ttu-id="e7df7-121">HDInsight Hive 活動是其中一個支援的 Data Factory 的 hello 轉換活動。</span><span class="sxs-lookup"><span data-stu-id="e7df7-121">HDInsight Hive Activity is one of hello transformation activities supported by Data Factory.</span></span> <span data-ttu-id="e7df7-122">您在本教學課程使用 hello Hive 轉換活動。</span><span class="sxs-lookup"><span data-stu-id="e7df7-122">You use hello Hive transformation activity in this tutorial.</span></span>

<span data-ttu-id="e7df7-123">您可以設定 hive 活動 toouse HDInsight Hadoop 叢集或隨 HDInsight Hadoop 叢集。</span><span class="sxs-lookup"><span data-stu-id="e7df7-123">You can configure a hive activity toouse your own HDInsight Hadoop cluster or an on-demand HDInsight Hadoop cluster.</span></span> <span data-ttu-id="e7df7-124">在本教學課程，hello hello 資料 factory 管線中的 Hive 活動是已設定的 toouse 隨選 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="e7df7-124">In this tutorial, hello Hive activity in hello data factory pipeline is configured toouse an on-demand HDInsight cluster.</span></span> <span data-ttu-id="e7df7-125">因此，當 hello 活動執行 tooprocess 資料配量時，會發生下列情況：</span><span class="sxs-lookup"><span data-stu-id="e7df7-125">Therefore, when hello activity runs tooprocess a data slice, here is what happens:</span></span>

1. <span data-ttu-id="e7df7-126">HDInsight Hadoop 叢集會自動建立您在 just-in-time tooprocess hello 配量。</span><span class="sxs-lookup"><span data-stu-id="e7df7-126">A HDInsight Hadoop cluster is automatically created for you just-in-time tooprocess hello slice.</span></span>  
2. <span data-ttu-id="e7df7-127">hello 輸入的資料會由 hello 叢集上執行下列 HiveQL 指令碼處理。</span><span class="sxs-lookup"><span data-stu-id="e7df7-127">hello input data is processed by running a HiveQL script on hello cluster.</span></span>
3. <span data-ttu-id="e7df7-128">hello 處理完成，且 hello 叢集的時間 （timeToLive 設定） 設定的 hello 內處於閒置狀態之後，會刪除 hello HDInsight Hadoop 叢集。</span><span class="sxs-lookup"><span data-stu-id="e7df7-128">hello HDInsight Hadoop cluster is deleted after hello processing is complete and hello cluster is idle for hello configured amount of time (timeToLive setting).</span></span> <span data-ttu-id="e7df7-129">如果可用於在 timeToLive 閒置時間與處理 hello 下一個資料配量，hello 相同叢集是使用的 tooprocess hello 配量。</span><span class="sxs-lookup"><span data-stu-id="e7df7-129">If hello next data slice is available for processing with in this timeToLive idle time, hello same cluster is used tooprocess hello slice.</span></span>  

<span data-ttu-id="e7df7-130">在本教學課程，hello 與 hello hive 活動相關聯的下列 HiveQL 指令碼會執行下列動作的 hello:</span><span class="sxs-lookup"><span data-stu-id="e7df7-130">In this tutorial, hello HiveQL script associated with hello hive activity performs hello following actions:</span></span>

1. <span data-ttu-id="e7df7-131">建立參考 hello 原始 web 記錄資料儲存在 Azure Blob 儲存體中的外部資料表。</span><span class="sxs-lookup"><span data-stu-id="e7df7-131">Creates an external table that references hello raw web log data stored in an Azure Blob storage.</span></span>
2. <span data-ttu-id="e7df7-132">資料分割 hello 依據年和月的未經處理資料。</span><span class="sxs-lookup"><span data-stu-id="e7df7-132">Partitions hello raw data by year and month.</span></span>
3. <span data-ttu-id="e7df7-133">存放區 hello hello Azure blob 儲存體中的資料分割的資料。</span><span class="sxs-lookup"><span data-stu-id="e7df7-133">Stores hello partitioned data in hello Azure blob storage.</span></span>

<span data-ttu-id="e7df7-134">在此教學課程中，hello 與 hello hive 活動相關聯的下列 HiveQL 指令碼會建立參考 hello hello Azure Blob 儲存體中儲存的未經處理的 web 記錄資料的外部資料表。</span><span class="sxs-lookup"><span data-stu-id="e7df7-134">In this tutorial, hello HiveQL script associated with hello hive activity creates an external table that references hello raw web log data stored in hello Azure Blob Storage.</span></span> <span data-ttu-id="e7df7-135">以下是每個月 hello 範例資料列 hello 輸入檔中。</span><span class="sxs-lookup"><span data-stu-id="e7df7-135">Here are hello sample rows for each month in hello input file.</span></span>

```
2014-01-01,02:01:09,SAMPLEWEBSITE,GET,/blogposts/mvc4/step2.png,X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,53175,871
2014-02-01,02:01:10,SAMPLEWEBSITE,GET,/blogposts/mvc4/step7.png,X-ARR-LOG-ID=d7472a26-431a-4a4d-99eb-c7b4fda2cf4c,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,30184,871
2014-03-01,02:01:10,SAMPLEWEBSITE,GET,/blogposts/mvc4/step7.png,X-ARR-LOG-ID=d7472a26-431a-4a4d-99eb-c7b4fda2cf4c,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,30184,871
```

<span data-ttu-id="e7df7-136">hello 下列 HiveQL 指令碼會分割 hello 依據年和月的未經處理資料。</span><span class="sxs-lookup"><span data-stu-id="e7df7-136">hello HiveQL script partitions hello raw data by year and month.</span></span> <span data-ttu-id="e7df7-137">它會建立三個 hello 先前的輸入為基礎的輸出資料夾。</span><span class="sxs-lookup"><span data-stu-id="e7df7-137">It creates three output folders based on hello previous input.</span></span> <span data-ttu-id="e7df7-138">每個資料夾都包含一個檔案，內含每個月的項目。</span><span class="sxs-lookup"><span data-stu-id="e7df7-138">Each folder contains a file with entries from each month.</span></span>

```
adfgetstarted/partitioneddata/year=2014/month=1/000000_0
adfgetstarted/partitioneddata/year=2014/month=2/000000_0
adfgetstarted/partitioneddata/year=2014/month=3/000000_0
```

<span data-ttu-id="e7df7-139">如需新增 tooHive 活動中的 Data Factory 資料轉換活動，請參閱[轉換和分析使用 Azure Data Factory](../data-factory/data-factory-data-transformation-activities.md)。</span><span class="sxs-lookup"><span data-stu-id="e7df7-139">For a list of Data Factory data transformation activities in addition tooHive activity, see [Transform and analyze using Azure Data Factory](../data-factory/data-factory-data-transformation-activities.md).</span></span>

> [!NOTE]
> <span data-ttu-id="e7df7-140">目前，您只可以從 Azure Data Factory 建立 HDInsight 叢集 3.2 版。</span><span class="sxs-lookup"><span data-stu-id="e7df7-140">Currently, you can only create HDInsight cluster version 3.2 from Azure Data Factory.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e7df7-141">必要條件</span><span class="sxs-lookup"><span data-stu-id="e7df7-141">Prerequisites</span></span>
<span data-ttu-id="e7df7-142">在開始這篇文章中的 hello 指示之前，您必須擁有 hello 下列項目：</span><span class="sxs-lookup"><span data-stu-id="e7df7-142">Before you begin hello instructions in this article, you must have hello following items:</span></span>

* <span data-ttu-id="e7df7-143">[Azure 訂用帳戶](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)。</span><span class="sxs-lookup"><span data-stu-id="e7df7-143">[Azure subscription](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="e7df7-144">Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="e7df7-144">Azure PowerShell.</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-powershell.md)]

### <a name="prepare-storage-account"></a><span data-ttu-id="e7df7-145">準備儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="e7df7-145">Prepare storage account</span></span>
<span data-ttu-id="e7df7-146">您可以使用向上 toothree 儲存體帳戶，在此案例中：</span><span class="sxs-lookup"><span data-stu-id="e7df7-146">You can use up toothree storage accounts in this scenario:</span></span>

- <span data-ttu-id="e7df7-147">hello HDInsight 叢集的預設儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="e7df7-147">default storage account for hello HDInsight cluster</span></span>
- <span data-ttu-id="e7df7-148">hello 輸入資料的儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="e7df7-148">storage account for hello input data</span></span>
- <span data-ttu-id="e7df7-149">hello 輸出資料的儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="e7df7-149">storage account for hello output data</span></span>

<span data-ttu-id="e7df7-150">toosimplify hello 教學課程中，您可以使用一個儲存體帳戶 tooserve hello 三種用途。</span><span class="sxs-lookup"><span data-stu-id="e7df7-150">toosimplify hello tutorial, you use one storage account tooserve hello three purposes.</span></span> <span data-ttu-id="e7df7-151">本章節的 hello Azure PowerShell 範例指令碼會執行下列工作的 hello:</span><span class="sxs-lookup"><span data-stu-id="e7df7-151">hello Azure PowerShell sample script found in this section performs hello following tasks:</span></span>

1. <span data-ttu-id="e7df7-152">登入 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="e7df7-152">Log in tooAzure.</span></span>
2. <span data-ttu-id="e7df7-153">建立 Azure 資源群組。</span><span class="sxs-lookup"><span data-stu-id="e7df7-153">Create an Azure resource group.</span></span>
3. <span data-ttu-id="e7df7-154">建立 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="e7df7-154">Create an Azure Storage account.</span></span>
4. <span data-ttu-id="e7df7-155">Hello 儲存體帳戶中建立 Blob 容器</span><span class="sxs-lookup"><span data-stu-id="e7df7-155">Create a Blob container in hello storage account</span></span>
5. <span data-ttu-id="e7df7-156">複製下列兩個檔案 toohello Blob 容器的 hello:</span><span class="sxs-lookup"><span data-stu-id="e7df7-156">Copy hello following two files toohello Blob container:</span></span>

   * <span data-ttu-id="e7df7-157">輸入資料檔： [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log)</span><span class="sxs-lookup"><span data-stu-id="e7df7-157">Input data file: [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log)</span></span>
   * <span data-ttu-id="e7df7-158">HiveQL 指令碼： [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql)</span><span class="sxs-lookup"><span data-stu-id="e7df7-158">HiveQL script: [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql)</span></span>

     <span data-ttu-id="e7df7-159">這兩個檔案會儲存在公用 Blob 容器。</span><span class="sxs-lookup"><span data-stu-id="e7df7-159">Both files are stored in a public Blob container.</span></span>


<span data-ttu-id="e7df7-160">**tooprepare hello 儲存體和複製 hello 檔案使用 Azure PowerShell:**</span><span class="sxs-lookup"><span data-stu-id="e7df7-160">**tooprepare hello storage and copy hello files using Azure PowerShell:**</span></span>
> [!IMPORTANT]
> <span data-ttu-id="e7df7-161">指定 hello Azure 資源群組和 hello 將 hello 指令碼所建立的 Azure 儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="e7df7-161">Specify names for hello Azure resource group and hello Azure storage account that will be created by hello script.</span></span>
> <span data-ttu-id="e7df7-162">請記下**資源群組名稱**，**儲存體帳戶名稱**，和**儲存體帳戶金鑰**hello 指令碼輸出。</span><span class="sxs-lookup"><span data-stu-id="e7df7-162">Write down **resource group name**, **storage account name**, and **storage account key** outputted by hello script.</span></span> <span data-ttu-id="e7df7-163">您會需要它們 hello 下一節。</span><span class="sxs-lookup"><span data-stu-id="e7df7-163">You need them in hello next section.</span></span>

```powershell
$resourceGroupName = "<Azure Resource Group Name>"
$storageAccountName = "<Azure Storage Account Name>"
$location = "East US 2"

$sourceStorageAccountName = "hditutorialdata"  
$sourceContainerName = "adfhiveactivity"

$destStorageAccountName = $storageAccountName
$destContainerName = "adfgetstarted" # don't change this value.

####################################
# Connect tooAzure
####################################
#region - Connect tooAzure subscription
Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
try{Get-AzureRmContext}
catch{Login-AzureRmAccount}
#endregion

####################################
# Create a resource group, storage, and container
####################################

#region - create Azure resources
Write-Host "`nCreating resource group, storage account and blob container ..." -ForegroundColor Green

New-AzureRmResourceGroup -Name $resourceGroupName -Location $location
New-AzureRmStorageAccount `
    -ResourceGroupName $resourceGroupName `
    -Name $destStorageAccountName `
    -type Standard_LRS `
    -Location $location

$destStorageAccountKey = (Get-AzureRmStorageAccountKey `
    -ResourceGroupName $resourceGroupName `
    -Name $destStorageAccountName)[0].Value

$sourceContext = New-AzureStorageContext `
    -StorageAccountName $sourceStorageAccountName `
    -Anonymous
$destContext = New-AzureStorageContext `
    -StorageAccountName $destStorageAccountName `
    -StorageAccountKey $destStorageAccountKey

New-AzureStorageContainer -Name $destContainerName -Context $destContext
#endregion

####################################
# Copy files
####################################
#region - copy files
Write-Host "`nCopying files ..." -ForegroundColor Green

$blobs = Get-AzureStorageBlob `
    -Context $sourceContext `
    -Container $sourceContainerName

$blobs|Start-AzureStorageBlobCopy `
    -DestContext $destContext `
    -DestContainer $destContainerName

Write-Host "`nCopied files ..." -ForegroundColor Green
Get-AzureStorageBlob -Context $destContext -Container $destContainerName
#endregion

Write-host "`nYou will use hello following values:" -ForegroundColor Green
write-host "`nResource group name: $resourceGroupName"
Write-host "Storage Account Name: $destStorageAccountName"
write-host "Storage Account Key: $destStorageAccountKey"

Write-host "`nScript completed" -ForegroundColor Green
```

<span data-ttu-id="e7df7-164">如果您需要協助 hello PowerShell 指令碼，請參閱[使用 hello 與 Azure 儲存體的 Azure PowerShell](../storage/common/storage-powershell-guide-full.md)。</span><span class="sxs-lookup"><span data-stu-id="e7df7-164">If you need help with hello PowerShell script, see [Using hello Azure PowerShell with Azure Storage](../storage/common/storage-powershell-guide-full.md).</span></span> <span data-ttu-id="e7df7-165">如果您希望 toouse Azure CLI 相反地，請參閱 hello[附錄](#appendix)hello Azure CLI 指令碼的區段。</span><span class="sxs-lookup"><span data-stu-id="e7df7-165">If you like toouse Azure CLI instead, see hello [Appendix](#appendix) section for hello Azure CLI script.</span></span>

<span data-ttu-id="e7df7-166">**tooexamine hello 儲存體帳戶和 hello 內容**</span><span class="sxs-lookup"><span data-stu-id="e7df7-166">**tooexamine hello storage account and hello contents**</span></span>

1. <span data-ttu-id="e7df7-167">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="e7df7-167">Sign on toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="e7df7-168">按一下**資源群組**hello 左窗格上。</span><span class="sxs-lookup"><span data-stu-id="e7df7-168">Click **Resource groups** on hello left pane.</span></span>
3. <span data-ttu-id="e7df7-169">按兩下您建立 PowerShell 指令碼中的 hello 資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="e7df7-169">Double-click hello resource group name you created in your PowerShell script.</span></span> <span data-ttu-id="e7df7-170">如果您有太多的資源群組列出，請使用 hello 篩選條件。</span><span class="sxs-lookup"><span data-stu-id="e7df7-170">Use hello filter if you have too many resource groups listed.</span></span>
4. <span data-ttu-id="e7df7-171">在 hello**資源**磚中，您應該有一項資源列出，除非您與其他專案共用 hello 資源群組。</span><span class="sxs-lookup"><span data-stu-id="e7df7-171">On hello **Resources** tile, you shall have one resource listed unless you share hello resource group with other projects.</span></span> <span data-ttu-id="e7df7-172">該資源是您稍早指定的 hello 名稱 hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="e7df7-172">That resource is hello storage account with hello name you specified earlier.</span></span> <span data-ttu-id="e7df7-173">按一下 hello 儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="e7df7-173">Click hello storage account name.</span></span>
5. <span data-ttu-id="e7df7-174">按一下 hello **Blob**磚。</span><span class="sxs-lookup"><span data-stu-id="e7df7-174">Click hello **Blobs** tiles.</span></span>
6. <span data-ttu-id="e7df7-175">按一下 hello **adfgetstarted**容器。</span><span class="sxs-lookup"><span data-stu-id="e7df7-175">Click hello **adfgetstarted** container.</span></span> <span data-ttu-id="e7df7-176">您會看到兩個資料夾︰[輸入資料] 和 [指令碼]。</span><span class="sxs-lookup"><span data-stu-id="e7df7-176">You see two folders: **inputdata** and **script**.</span></span>
7. <span data-ttu-id="e7df7-177">開啟 [hello] 資料夾，並檢查 hello 資料夾中的 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="e7df7-177">Open hello folder and check hello files in hello folders.</span></span> <span data-ttu-id="e7df7-178">hello inputdata 包含輸入資料與 hello input.log 檔案而且 hello 指令碼 資料夾包含 hello HiveQL 指令碼檔案。</span><span class="sxs-lookup"><span data-stu-id="e7df7-178">hello inputdata contains hello input.log file with input data and hello script folder contains hello HiveQL script file.</span></span>

## <a name="create-a-data-factory-using-resource-manager-template"></a><span data-ttu-id="e7df7-179">使用 Resource Manager 範本建立資料處理站</span><span class="sxs-lookup"><span data-stu-id="e7df7-179">Create a data factory using Resource Manager template</span></span>
<span data-ttu-id="e7df7-180">Hello 儲存體帳戶、 與 hello 輸入的資料，hello 備妥下列 HiveQL 指令碼，您就準備好 toocreate Azure data factory。</span><span class="sxs-lookup"><span data-stu-id="e7df7-180">With hello storage account, hello input data, and hello HiveQL script prepared, you are ready toocreate an Azure data factory.</span></span> <span data-ttu-id="e7df7-181">有數種方法可建立 Data Factory。</span><span class="sxs-lookup"><span data-stu-id="e7df7-181">There are several methods for creating data factory.</span></span> <span data-ttu-id="e7df7-182">在本教學課程中，您可以建立 data factory 所部署的 Azure Resource Manager 範本使用 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="e7df7-182">In this tutorial, you create a data factory by deploying an Azure Resource Manager template using hello Azure portal.</span></span> <span data-ttu-id="e7df7-183">您也可以使用 [Azure CLI](../azure-resource-manager/resource-group-template-deploy-cli.md) 和 [Azure PowerShell](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template) 部署 Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="e7df7-183">You can also deploy a Resource Manager template by using [Azure CLI](../azure-resource-manager/resource-group-template-deploy-cli.md) and [Azure PowerShell](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template).</span></span> <span data-ttu-id="e7df7-184">如需其他 Data Factory 建立方法，請參閱 [教學課程︰建立您的第一個 Data Factory](../data-factory/data-factory-build-your-first-pipeline.md)。</span><span class="sxs-lookup"><span data-stu-id="e7df7-184">For other data factory creation methods, see [Tutorial: Build your first data factory](../data-factory/data-factory-build-your-first-pipeline.md).</span></span>

1. <span data-ttu-id="e7df7-185">按一下下列 tooAzure 中的映像 toosign 和開啟 hello Resource Manager 範本 hello Azure 入口網站中的 hello。</span><span class="sxs-lookup"><span data-stu-id="e7df7-185">Click hello following image toosign in tooAzure and open hello Resource Manager template in hello Azure portal.</span></span> <span data-ttu-id="e7df7-186">hello 範本位於 https://hditutorialdata.blob.core.windows.net/adfhiveactivity/data-factory-hdinsight-on-demand.json。</span><span class="sxs-lookup"><span data-stu-id="e7df7-186">hello template is located at https://hditutorialdata.blob.core.windows.net/adfhiveactivity/data-factory-hdinsight-on-demand.json.</span></span> <span data-ttu-id="e7df7-187">請參閱 hello [hello 範本中的 Data Factory 實體](#data-factory-entities-in-the-template)hello 範本中定義實體的詳細資訊的區段。</span><span class="sxs-lookup"><span data-stu-id="e7df7-187">See hello [Data Factory entities in hello template](#data-factory-entities-in-the-template) section for detailed information about entities defined in hello template.</span></span> 

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Fadfhiveactivity%2Fdata-factory-hdinsight-on-demand.json" target="_blank"><img src="./media/hdinsight-hadoop-create-linux-clusters-adf/deploy-to-azure.png" alt="Deploy tooAzure"></a>
2. <span data-ttu-id="e7df7-188">選取**使用現有**選項 hello**資源群組**設定，再選取 hello hello hello （使用 PowerShell 指令碼） 的上一個步驟中所建立的資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="e7df7-188">Select **Use existing** option for hello **Resource group** setting, and select hello name of hello resource group you created in hello previous step (using PowerShell script).</span></span>
3. <span data-ttu-id="e7df7-189">輸入 hello data factory 的名稱 (**Data Factory 名稱**)。</span><span class="sxs-lookup"><span data-stu-id="e7df7-189">Enter a name for hello data factory (**Data Factory Name**).</span></span> <span data-ttu-id="e7df7-190">此名稱必須是全域唯一的。</span><span class="sxs-lookup"><span data-stu-id="e7df7-190">This name must be globally unique.</span></span>
4. <span data-ttu-id="e7df7-191">輸入 hello**儲存體帳戶名稱**和**儲存體帳戶金鑰**hello 上一個步驟中記下。</span><span class="sxs-lookup"><span data-stu-id="e7df7-191">Enter hello **storage account name** and **storage account key** you wrote down in hello previous step.</span></span>
5. <span data-ttu-id="e7df7-192">選取**toohello 條款和條件，即表示我同意**閱讀後指定上述**條款和條件**。</span><span class="sxs-lookup"><span data-stu-id="e7df7-192">Select **I agree toohello terms and conditions** stated above after reading through **terms and conditions**.</span></span>
6. <span data-ttu-id="e7df7-193">選取**Pin toodashboard**選項。</span><span class="sxs-lookup"><span data-stu-id="e7df7-193">Select **Pin toodashboard** option.</span></span>
6. <span data-ttu-id="e7df7-194">按一下 [購買/建立]。</span><span class="sxs-lookup"><span data-stu-id="e7df7-194">Click **Purchase/Create**.</span></span> <span data-ttu-id="e7df7-195">您在 hello 呼叫儀表板上看到磚**部署範本部署**。</span><span class="sxs-lookup"><span data-stu-id="e7df7-195">You see a tile on hello Dashboard called **Deploying Template deployment**.</span></span> <span data-ttu-id="e7df7-196">等候直到在 hello**資源群組**資源群組的刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="e7df7-196">Wait until hello **Resource group** blade for your resource group opens.</span></span> <span data-ttu-id="e7df7-197">您也可以按一下 hello 磚的標題會當做您資源群組名稱 tooopen hello 資源群組 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="e7df7-197">You can also click hello tile titled as your resource group name tooopen hello resource group blade.</span></span>
6. <span data-ttu-id="e7df7-198">如果尚未開啟 hello 資源群組 刀鋒視窗，請按一下 hello 磚 tooopen hello 資源群組。</span><span class="sxs-lookup"><span data-stu-id="e7df7-198">Click hello tile tooopen hello resource group if hello resource group blade is not already open.</span></span> <span data-ttu-id="e7df7-199">現在您應該會看到一個詳細資料 factory 資源列出此外 toohello 儲存體帳戶的資源。</span><span class="sxs-lookup"><span data-stu-id="e7df7-199">Now you shall see one more data factory resource listed in addition toohello storage account resource.</span></span>
7. <span data-ttu-id="e7df7-200">按一下您的 data factory hello 名稱 (您指定的 hello 值**Data Factory 名稱**參數)。</span><span class="sxs-lookup"><span data-stu-id="e7df7-200">Click hello name of your data factory (value you specified for hello **Data Factory Name** parameter).</span></span>
8. <span data-ttu-id="e7df7-201">在 hello Data Factory 刀鋒視窗中，按一下 hello**圖表**磚。</span><span class="sxs-lookup"><span data-stu-id="e7df7-201">In hello Data Factory blade, click hello **Diagram** tile.</span></span> <span data-ttu-id="e7df7-202">hello 圖表會顯示與輸入資料集和輸出資料集的一個活動：</span><span class="sxs-lookup"><span data-stu-id="e7df7-202">hello diagram shows one activity with an input dataset, and an output dataset:</span></span>

    ![Azure Data Factory HDInsight 隨選 Hive 活動管線圖](./media/hdinsight-hadoop-create-linux-clusters-adf/hdinsight-adf-pipeline-diagram.png)

    <span data-ttu-id="e7df7-204">hello 名稱定義在 hello Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="e7df7-204">hello names are defined in hello Resource Manager template.</span></span>
9. <span data-ttu-id="e7df7-205">按兩下 [AzureBlobOutput] 。</span><span class="sxs-lookup"><span data-stu-id="e7df7-205">Double-click **AzureBlobOutput**.</span></span>
10. <span data-ttu-id="e7df7-206">在 hello**最近更新配量**，您應該會看到一個扇區。</span><span class="sxs-lookup"><span data-stu-id="e7df7-206">On hello **Recent updated slices**, you shall see one slice.</span></span> <span data-ttu-id="e7df7-207">如果 hello 狀態是**正在**，等候直到變更太**準備**。</span><span class="sxs-lookup"><span data-stu-id="e7df7-207">If hello status is **In progress**, wait until it is changed too**Ready**.</span></span> <span data-ttu-id="e7df7-208">通常，大約需要**20 分鐘**toocreate 的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="e7df7-208">It usually takes about **20 minutes** toocreate an HDInsight cluster.</span></span>

### <a name="check-hello-data-factory-output"></a><span data-ttu-id="e7df7-209">檢查 hello 資料處理站的輸出</span><span class="sxs-lookup"><span data-stu-id="e7df7-209">Check hello data factory output</span></span>

1. <span data-ttu-id="e7df7-210">使用 hello 相同 hello 最後一個工作階段 toocheck hello 容器中的 hello adfgetstarted 容器的程序。</span><span class="sxs-lookup"><span data-stu-id="e7df7-210">Use hello same procedure in hello last session toocheck hello containers of hello adfgetstarted container.</span></span> <span data-ttu-id="e7df7-211">有兩個新的容器此外太**adfgetsarted**:</span><span class="sxs-lookup"><span data-stu-id="e7df7-211">There are two new containers in addition too**adfgetsarted**:</span></span>

   * <span data-ttu-id="e7df7-212">遵循 hello 模式名稱的容器： `adf<yourdatafactoryname>-linkedservicename-datetimestamp`。</span><span class="sxs-lookup"><span data-stu-id="e7df7-212">A container with name that follows hello pattern: `adf<yourdatafactoryname>-linkedservicename-datetimestamp`.</span></span> <span data-ttu-id="e7df7-213">此容器是 hello hello HDInsight 叢集的預設容器。</span><span class="sxs-lookup"><span data-stu-id="e7df7-213">This container is hello default container for hello HDInsight cluster.</span></span>
   * <span data-ttu-id="e7df7-214">adfjobs： 此容器是 hello hello ADF 作業記錄的容器。</span><span class="sxs-lookup"><span data-stu-id="e7df7-214">adfjobs: This container is hello container for hello ADF job logs.</span></span>

     <span data-ttu-id="e7df7-215">hello 資料處理站的輸出會儲存在**afgetstarted**您 hello Resource Manager 範本中的設定。</span><span class="sxs-lookup"><span data-stu-id="e7df7-215">hello data factory output is stored in **afgetstarted** as you configured in hello Resource Manager template.</span></span>
2. <span data-ttu-id="e7df7-216">按一下 [adfgetstarted] 。</span><span class="sxs-lookup"><span data-stu-id="e7df7-216">Click **adfgetstarted**.</span></span>
3. <span data-ttu-id="e7df7-217">按兩下 [partitioneddata] 。</span><span class="sxs-lookup"><span data-stu-id="e7df7-217">Double-click **partitioneddata**.</span></span> <span data-ttu-id="e7df7-218">您會看到**年 = 2014年**資料夾因為所有的 hello web 記錄日期在 2014 年。</span><span class="sxs-lookup"><span data-stu-id="e7df7-218">You see a **year=2014** folder because all hello web logs are dated in year 2014.</span></span>

    ![Azure Data Factory HDInsight 隨選 Hive 活動管線輸出](./media/hdinsight-hadoop-create-linux-clusters-adf/hdinsight-adf-output-year.png)

    <span data-ttu-id="e7df7-220">如果您 hello 清單向下鑽研，您應該會看到一月、 二月和三月的三個資料夾。</span><span class="sxs-lookup"><span data-stu-id="e7df7-220">If you drill down hello list, you shall see three folders for January, February, and March.</span></span> <span data-ttu-id="e7df7-221">而且每個月都有記錄檔。</span><span class="sxs-lookup"><span data-stu-id="e7df7-221">And there is a log for each month.</span></span>

    ![Azure Data Factory HDInsight 隨選 Hive 活動管線輸出](./media/hdinsight-hadoop-create-linux-clusters-adf/hdinsight-adf-output-month.png)

## <a name="data-factory-entities-in-hello-template"></a><span data-ttu-id="e7df7-223">Hello 範本中的 data Factory 實體</span><span class="sxs-lookup"><span data-stu-id="e7df7-223">Data Factory entities in hello template</span></span>
<span data-ttu-id="e7df7-224">以下是如何 data factory hello 最上層資源管理員範本外觀就像：</span><span class="sxs-lookup"><span data-stu-id="e7df7-224">Here is how hello top-level Resource Manager template for a data factory looks like:</span></span>

```json
{
    "contentVersion": "1.0.0.0",
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "parameters": { ...
    },
    "variables": { ...
    },
    "resources": [
        {
            "name": "[parameters('dataFactoryName')]",
            "apiVersion": "[variables('apiVersion')]",
            "type": "Microsoft.DataFactory/datafactories",
            "location": "westus",
            "resources": [
                { ... },
                { ... },
                { ... },
                { ... }
            ]
        }
    ]
}
```

### <a name="define-data-factory"></a><span data-ttu-id="e7df7-225">定義資料處理站</span><span class="sxs-lookup"><span data-stu-id="e7df7-225">Define data factory</span></span>
<span data-ttu-id="e7df7-226">Hello 下列範例所示，您可以定義在 hello Resource Manager 範本中的 data factory:</span><span class="sxs-lookup"><span data-stu-id="e7df7-226">You define a data factory in hello Resource Manager template as shown in hello following sample:</span></span>  

```json
"resources": [
{
    "name": "[parameters('dataFactoryName')]",
    "apiVersion": "[variables('apiVersion')]",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "westus",
}
```
<span data-ttu-id="e7df7-227">hello dataFactoryName 是 hello 部署 hello 範本時，您指定的 hello data factory 名稱。</span><span class="sxs-lookup"><span data-stu-id="e7df7-227">hello dataFactoryName is hello name of hello data factory you specify when you deploy hello template.</span></span> <span data-ttu-id="e7df7-228">Data factory 是目前只支援 hello 美國東部、 美國西部和北歐區域中。</span><span class="sxs-lookup"><span data-stu-id="e7df7-228">Data factory is currently only supported in hello East US, West US, and North Europe regions.</span></span>

### <a name="defining-entities-within-hello-data-factory"></a><span data-ttu-id="e7df7-229">定義 hello 資料處理站內的實體</span><span class="sxs-lookup"><span data-stu-id="e7df7-229">Defining entities within hello data factory</span></span>
<span data-ttu-id="e7df7-230">hello 下列 Data Factory 實體範本中所定義 hello JSON:</span><span class="sxs-lookup"><span data-stu-id="e7df7-230">hello following Data Factory entities are defined in hello JSON template:</span></span>

* [<span data-ttu-id="e7df7-231">Azure 儲存體連結服務</span><span class="sxs-lookup"><span data-stu-id="e7df7-231">Azure Storage linked service</span></span>](#azure-storage-linked-service)
* [<span data-ttu-id="e7df7-232">HDInsight 隨選連結服務</span><span class="sxs-lookup"><span data-stu-id="e7df7-232">HDInsight on-demand linked service</span></span>](#hdinsight-on-demand-linked-service)
* [<span data-ttu-id="e7df7-233">Azure Blob 輸入資料集</span><span class="sxs-lookup"><span data-stu-id="e7df7-233">Azure blob input dataset</span></span>](#azure-blob-input-dataset)
* [<span data-ttu-id="e7df7-234">Azure Blob 輸出資料集</span><span class="sxs-lookup"><span data-stu-id="e7df7-234">Azure blob output dataset</span></span>](#azure-blob-output-dataset)
* [<span data-ttu-id="e7df7-235">具有複製活動的管線</span><span class="sxs-lookup"><span data-stu-id="e7df7-235">Data pipeline with a copy activity</span></span>](#data-pipeline)

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="e7df7-236">Azure 儲存體連結服務</span><span class="sxs-lookup"><span data-stu-id="e7df7-236">Azure Storage linked service</span></span>
<span data-ttu-id="e7df7-237">hello Azure 儲存體連結服務連結您的 Azure 儲存體帳戶 toohello data factory。</span><span class="sxs-lookup"><span data-stu-id="e7df7-237">hello Azure Storage linked service links your Azure storage account toohello data factory.</span></span> <span data-ttu-id="e7df7-238">在此教學課程中，hello 相同儲存體帳戶做為 hello 預設 HDInsight 儲存體帳戶、 輸入的資料存放區和輸出資料存放區。</span><span class="sxs-lookup"><span data-stu-id="e7df7-238">In this tutorial, hello same storage account is used as hello default HDInsight storage account, input data storage, and output data storage.</span></span> <span data-ttu-id="e7df7-239">因此，您只定義一個 Azure 儲存體連結服務。</span><span class="sxs-lookup"><span data-stu-id="e7df7-239">Therefore, you define only one Azure Storage linked service.</span></span> <span data-ttu-id="e7df7-240">在連結的 hello 服務定義中，您可以指定 hello 名稱和您的 Azure 儲存體帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="e7df7-240">In hello linked service definition, you specify hello name and key of your Azure storage account.</span></span> <span data-ttu-id="e7df7-241">請參閱[Azure 儲存體連結服務](../data-factory/data-factory-azure-blob-connector.md#azure-storage-linked-service)如需詳細資訊 JSON 屬性使用 toodefine Azure 儲存體連結服務。</span><span class="sxs-lookup"><span data-stu-id="e7df7-241">See [Azure Storage linked service](../data-factory/data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties used toodefine an Azure Storage linked service.</span></span>

```json
{
    "name": "[variables('storageLinkedServiceName')]",
    "type": "linkedservices",
    "dependsOn": [ "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]" ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "[concat('DefaultEndpointsProtocol=https;AccountName=',parameters('storageAccountName'),';AccountKey=',parameters('storageAccountKey'))]"
        }
    }
}
```
<span data-ttu-id="e7df7-242">hello **connectionString**使用 hello storageAccountName 及 storageAccountKey 參數。</span><span class="sxs-lookup"><span data-stu-id="e7df7-242">hello **connectionString** uses hello storageAccountName and storageAccountKey parameters.</span></span> <span data-ttu-id="e7df7-243">您部署 hello 範本時指定這些參數的值。</span><span class="sxs-lookup"><span data-stu-id="e7df7-243">You specify values for these parameters while deploying hello template.</span></span>  

#### <a name="hdinsight-on-demand-linked-service"></a><span data-ttu-id="e7df7-244">HDInsight 隨選連結服務</span><span class="sxs-lookup"><span data-stu-id="e7df7-244">HDInsight on-demand linked service</span></span>
<span data-ttu-id="e7df7-245">在 hello 隨 HDInsight 連結服務定義中，指定 hello Data Factory 服務 toocreate HDInsight Hadoop 叢集在執行階段所使用的組態參數的值。</span><span class="sxs-lookup"><span data-stu-id="e7df7-245">In hello on-demand HDInsight linked service definition, you specify values for configuration parameters that are used by hello Data Factory service toocreate a HDInsight Hadoop cluster at runtime.</span></span> <span data-ttu-id="e7df7-246">請參閱[計算連結的服務](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service)文件如需詳細資訊 JSON 屬性使用 toodefine HDInsight 視連結的服務。</span><span class="sxs-lookup"><span data-stu-id="e7df7-246">See [Compute linked services](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) article for details about JSON properties used toodefine an HDInsight on-demand linked service.</span></span>  

```json

{
    "type": "linkedservices",
    "name": "[variables('hdInsightOnDemandLinkedServiceName')]",
    "dependsOn": [
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedservices/', variables('storageLinkedServiceName'))]"
    ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "type": "HDInsightOnDemand",
        "typeProperties": {
            "version": "3.5",
            "clusterSize": 1,
            "timeToLive": "00:05:00",
            "osType": "Linux",
            "sshUserName": "myuser",                            
            "sshPassword": "MyPassword!",
            "linkedServiceName": "[variables('storageLinkedServiceName')]"
        }
    }
}
```
<span data-ttu-id="e7df7-247">請注意下列點 hello:</span><span class="sxs-lookup"><span data-stu-id="e7df7-247">Note hello following points:</span></span>

* <span data-ttu-id="e7df7-248">hello Data Factory 建立**linux**為您的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="e7df7-248">hello Data Factory creates a **Linux-based** HDInsight cluster for you.</span></span>
* <span data-ttu-id="e7df7-249">hello HDInsight Hadoop 叢集會建立於 hello 相同 hello 儲存體帳戶與區域。</span><span class="sxs-lookup"><span data-stu-id="e7df7-249">hello HDInsight Hadoop cluster is created in hello same region as hello storage account.</span></span>
* <span data-ttu-id="e7df7-250">請注意 hello *timeToLive*設定。</span><span class="sxs-lookup"><span data-stu-id="e7df7-250">Notice hello *timeToLive* setting.</span></span> <span data-ttu-id="e7df7-251">hello 資料處理站會在 hello 叢集正在閒置 30 分鐘後自動刪除 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="e7df7-251">hello data factory deletes hello cluster automatically after hello cluster is being idle for 30 minutes.</span></span>
* <span data-ttu-id="e7df7-252">hello HDInsight 叢集建立**預設容器**hello hello JSON 中指定的 blob 儲存體中 (**linkedServiceName**)。</span><span class="sxs-lookup"><span data-stu-id="e7df7-252">hello HDInsight cluster creates a **default container** in hello blob storage you specified in hello JSON (**linkedServiceName**).</span></span> <span data-ttu-id="e7df7-253">HDInsight 刪除 hello 叢集時，不會刪除此容器。</span><span class="sxs-lookup"><span data-stu-id="e7df7-253">HDInsight does not delete this container when hello cluster is deleted.</span></span> <span data-ttu-id="e7df7-254">這是設計的行為。</span><span class="sxs-lookup"><span data-stu-id="e7df7-254">This behavior is by design.</span></span> <span data-ttu-id="e7df7-255">HDInsight 叢集隨 HDInsight 連結服務，以建立每次配量需要處理現有的叢集即時除非 toobe (**timeToLive**) 和 hello 處理完成時刪除。</span><span class="sxs-lookup"><span data-stu-id="e7df7-255">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice needs toobe processed unless there is an existing live cluster (**timeToLive**) and is deleted when hello processing is done.</span></span>

<span data-ttu-id="e7df7-256">如需詳細資訊，請參閱 [HDInsight 隨選連結服務](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) 。</span><span class="sxs-lookup"><span data-stu-id="e7df7-256">See [On-demand HDInsight Linked Service](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e7df7-257">隨著處理的配量越來越多，您會在 Azure Blob 儲存體中看到許多容器。</span><span class="sxs-lookup"><span data-stu-id="e7df7-257">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="e7df7-258">如果您不需要它們進行疑難排解的 hello 工作，您可能會想 toodelete 它們 tooreduce hello 儲存體成本。</span><span class="sxs-lookup"><span data-stu-id="e7df7-258">If you do not need them for troubleshooting of hello jobs, you may want toodelete them tooreduce hello storage cost.</span></span> <span data-ttu-id="e7df7-259">這些容器的 hello 名稱遵循模式: 「 adf**yourdatafactoryname**-**linkedservicename**-datetimestamp"。</span><span class="sxs-lookup"><span data-stu-id="e7df7-259">hello names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span></span> <span data-ttu-id="e7df7-260">使用工具，例如[Microsoft 儲存體總管](http://storageexplorer.com/)toodelete 容器，在您的 Azure blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="e7df7-260">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) toodelete containers in your Azure blob storage.</span></span>

#### <a name="azure-blob-input-dataset"></a><span data-ttu-id="e7df7-261">Azure Blob 輸入資料集</span><span class="sxs-lookup"><span data-stu-id="e7df7-261">Azure blob input dataset</span></span>
<span data-ttu-id="e7df7-262">在 hello 輸入資料集定義中，您可以指定 hello blob 容器、 資料夾和檔案名稱，其中包含 hello 輸入的資料。</span><span class="sxs-lookup"><span data-stu-id="e7df7-262">In hello input dataset definition, you specify hello names of blob container, folder, and file that contains hello input data.</span></span> <span data-ttu-id="e7df7-263">請參閱[Azure Blob 資料集屬性](../data-factory/data-factory-azure-blob-connector.md#dataset-properties)如需詳細資訊 JSON 屬性使用 toodefine Azure Blob 資料集。</span><span class="sxs-lookup"><span data-stu-id="e7df7-263">See [Azure Blob dataset properties](../data-factory/data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used toodefine an Azure Blob dataset.</span></span>

```json

{
    "type": "datasets",
    "name": "[variables('blobInputDatasetName')]",
    "dependsOn": [
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedServices/', variables('storageLinkedServiceName'))]"
    ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "[variables('storageLinkedServiceName')]",
        "typeProperties": {
            "fileName": "input.log",
            "folderPath": "adfgetstarted/inputdata",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}

```

<span data-ttu-id="e7df7-264">請注意下列 hello JSON 定義中的特定設定的 hello:</span><span class="sxs-lookup"><span data-stu-id="e7df7-264">Notice hello following specific settings in hello JSON definition:</span></span>

```json
"fileName": "input.log",
"folderPath": "adfgetstarted/inputdata",
```

#### <a name="azure-blob-output-dataset"></a><span data-ttu-id="e7df7-265">Azure Blob 輸出資料集</span><span class="sxs-lookup"><span data-stu-id="e7df7-265">Azure Blob output dataset</span></span>
<span data-ttu-id="e7df7-266">在 hello 輸出資料集定義中，您可以指定 hello 的 blob 容器，並保存 hello 輸出資料之資料夾的名稱。</span><span class="sxs-lookup"><span data-stu-id="e7df7-266">In hello output dataset definition, you specify hello names of blob container and folder that holds hello output data.</span></span> <span data-ttu-id="e7df7-267">請參閱[Azure Blob 資料集屬性](../data-factory/data-factory-azure-blob-connector.md#dataset-properties)如需詳細資訊 JSON 屬性使用 toodefine Azure Blob 資料集。</span><span class="sxs-lookup"><span data-stu-id="e7df7-267">See [Azure Blob dataset properties](../data-factory/data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used toodefine an Azure Blob dataset.</span></span>  

```json

{
    "type": "datasets",
    "name": "[variables('blobOutputDatasetName')]",
    "dependsOn": [
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedServices/', variables('storageLinkedServiceName'))]"
    ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "[variables('storageLinkedServiceName')]",
        "typeProperties": {
            "folderPath": "adfgetstarted/partitioneddata",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1,
            "style": "EndOfInterval"
        }
    }
}
```

<span data-ttu-id="e7df7-268">hello folderPath 指定保存 hello 輸出資料的 hello 路徑 toohello 資料夾：</span><span class="sxs-lookup"><span data-stu-id="e7df7-268">hello folderPath specifies hello path toohello folder that holds hello output data:</span></span>

```json
"folderPath": "adfgetstarted/partitioneddata",
```

<span data-ttu-id="e7df7-269">hello[資料集可用性](../data-factory/data-factory-create-datasets.md#dataset-availability)設定如下所示：</span><span class="sxs-lookup"><span data-stu-id="e7df7-269">hello [dataset availability](../data-factory/data-factory-create-datasets.md#dataset-availability) setting is as follows:</span></span>

```json
"availability": {
    "frequency": "Month",
    "interval": 1,
    "style": "EndOfInterval"
},
```

<span data-ttu-id="e7df7-270">在 Azure Data Factory，輸出資料集可用性磁碟機 hello 管線。</span><span class="sxs-lookup"><span data-stu-id="e7df7-270">In Azure Data Factory, output dataset availability drives hello pipeline.</span></span> <span data-ttu-id="e7df7-271">在此範例中，hello 點產生配量每月 hello (為 EndOfInterval) 當月最後一天。</span><span class="sxs-lookup"><span data-stu-id="e7df7-271">In this example, hello slice is produced monthly on hello last day of month (EndOfInterval).</span></span> <span data-ttu-id="e7df7-272">如需詳細資訊，請參閱 [Data Factory 排程和執行](../data-factory/data-factory-scheduling-and-execution.md)。</span><span class="sxs-lookup"><span data-stu-id="e7df7-272">For more information, see [Data Factory Scheduling and Execution](../data-factory/data-factory-scheduling-and-execution.md).</span></span>

#### <a name="data-pipeline"></a><span data-ttu-id="e7df7-273">Data Pipeline</span><span class="sxs-lookup"><span data-stu-id="e7df7-273">Data pipeline</span></span>
<span data-ttu-id="e7df7-274">您可以定義在隨選 Azure HDInsight 叢集上執行 Hive 指令碼以轉換資料的管線。</span><span class="sxs-lookup"><span data-stu-id="e7df7-274">You define a pipeline that transforms data by running Hive script on an on-demand Azure HDInsight cluster.</span></span> <span data-ttu-id="e7df7-275">請參閱[管線 JSON](../data-factory/data-factory-create-pipelines.md#pipeline-json)如需 JSON 用項目 toodefine 管線，以在此範例的描述。</span><span class="sxs-lookup"><span data-stu-id="e7df7-275">See [Pipeline JSON](../data-factory/data-factory-create-pipelines.md#pipeline-json) for descriptions of JSON elements used toodefine a pipeline in this example.</span></span>

```json
{
    "type": "datapipelines",
    "name": "[parameters('dataFactoryName')]",
    "dependsOn": [
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedServices/', variables('storageLinkedServiceName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedServices/', variables('hdInsightOnDemandLinkedServiceName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/datasets/', variables('blobInputDatasetName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/datasets/', variables('blobOutputDatasetName'))]"
    ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "description": "Azure Data Factory pipeline with an Hadoop Hive activity",
        "activities": [
            {
                "type": "HDInsightHive",
                "typeProperties": {
                    "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                    "scriptLinkedService": "[variables('storageLinkedServiceName')]",
                    "defines": {
                        "inputtable": "[concat('wasb://adfgetstarted@', parameters('storageAccountName'), '.blob.core.windows.net/inputdata')]",
                        "partitionedtable": "[concat('wasb://adfgetstarted@', parameters('storageAccountName'), '.blob.core.windows.net/partitioneddata')]"
                    }
                },
                "inputs": [
                    {
                        "name": "AzureBlobInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutput"
                    }
                ],
                "policy": {
                    "concurrency": 1,
                    "retry": 3
                },
                "name": "RunSampleHiveActivity",
                "linkedServiceName": "HDInsightOnDemandLinkedService"
            }
        ],
        "start": "2016-01-01T00:00:00Z",
        "end": "2016-01-31T00:00:00Z",
        "isPaused": false
    }
}
```

<span data-ttu-id="e7df7-276">hello 管線包含一個活動，HDInsightHive 活動。</span><span class="sxs-lookup"><span data-stu-id="e7df7-276">hello pipeline contains one activity, HDInsightHive activity.</span></span> <span data-ttu-id="e7df7-277">由於開始和結束日期都在 2016 年 1 月，因此只處理一個月的資料 (配量)。</span><span class="sxs-lookup"><span data-stu-id="e7df7-277">As both start and end dates are in January 2016, data for only one month (a slice) is processed.</span></span> <span data-ttu-id="e7df7-278">同時*啟動*和*結束*hello 活動的已過去的日期，因此 hello Data Factory hello 月份立即處理資料。</span><span class="sxs-lookup"><span data-stu-id="e7df7-278">Both *start* and *end* of hello activity have a past date, so hello Data Factory processes data for hello month immediately.</span></span> <span data-ttu-id="e7df7-279">如果 hello 結尾是未來的日期，hello 資料 factory hello 時間時，就會建立另一個配量。</span><span class="sxs-lookup"><span data-stu-id="e7df7-279">If hello end is a future date, hello data factory creates another slice when hello time comes.</span></span> <span data-ttu-id="e7df7-280">如需詳細資訊，請參閱 [Data Factory 排程和執行](../data-factory/data-factory-scheduling-and-execution.md)。</span><span class="sxs-lookup"><span data-stu-id="e7df7-280">For more information, see [Data Factory Scheduling and Execution](../data-factory/data-factory-scheduling-and-execution.md).</span></span>

## <a name="clean-up-hello-tutorial"></a><span data-ttu-id="e7df7-281">清除 hello 教學課程</span><span class="sxs-lookup"><span data-stu-id="e7df7-281">Clean up hello tutorial</span></span>

### <a name="delete-hello-blob-containers-created-by-on-demand-hdinsight-cluster"></a><span data-ttu-id="e7df7-282">刪除 hello 隨選 HDInsight 叢集所建立的 blob 容器</span><span class="sxs-lookup"><span data-stu-id="e7df7-282">Delete hello blob containers created by on-demand HDInsight cluster</span></span>
<span data-ttu-id="e7df7-283">每次配量需要處理現有的即時叢集 (timeToLive); 除非 toobe，HDInsight 叢集建立隨 HDInsight 連結服務而且 hello 叢集 hello 處理完成時刪除。</span><span class="sxs-lookup"><span data-stu-id="e7df7-283">With on-demand HDInsight linked service, an HDInsight cluster is created every time a slice needs toobe processed unless there is an existing live cluster (timeToLive); and hello cluster is deleted when hello processing is done.</span></span> <span data-ttu-id="e7df7-284">針對每個群集，Azure Data Factory，請在 hello 作為 hello 叢集 hello 預設 stroage 帳戶的 Azure blob 儲存體中建立 blob 容器。</span><span class="sxs-lookup"><span data-stu-id="e7df7-284">For each cluster, Azure Data Factory creates a blob container in hello Azure blob storage used as hello default stroage account for hello cluster.</span></span> <span data-ttu-id="e7df7-285">即使已刪除 HDInsight 叢集，hello 預設 blob 儲存體容器和相關聯的 hello 儲存體帳戶不會刪除。</span><span class="sxs-lookup"><span data-stu-id="e7df7-285">Even though HDInsight cluster is deleted, hello default blob storage container and hello associated storage account are not deleted.</span></span> <span data-ttu-id="e7df7-286">這是設計的行為。</span><span class="sxs-lookup"><span data-stu-id="e7df7-286">This behavior is by design.</span></span> <span data-ttu-id="e7df7-287">隨著處理的配量越來越多，您會在 Azure Blob 儲存體中看到許多容器。</span><span class="sxs-lookup"><span data-stu-id="e7df7-287">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="e7df7-288">如果您不需要它們進行疑難排解的 hello 工作，您可能會想 toodelete 它們 tooreduce hello 儲存體成本。</span><span class="sxs-lookup"><span data-stu-id="e7df7-288">If you do not need them for troubleshooting of hello jobs, you may want toodelete them tooreduce hello storage cost.</span></span> <span data-ttu-id="e7df7-289">這些容器的 hello 名稱遵循模式： `adfyourdatafactoryname-linkedservicename-datetimestamp`。</span><span class="sxs-lookup"><span data-stu-id="e7df7-289">hello names of these containers follow a pattern: `adfyourdatafactoryname-linkedservicename-datetimestamp`.</span></span>

<span data-ttu-id="e7df7-290">刪除 hello **adfjobs**和**adfyourdatafactoryname-linkedservicename-datetimestamp**資料夾。</span><span class="sxs-lookup"><span data-stu-id="e7df7-290">Delete hello **adfjobs** and **adfyourdatafactoryname-linkedservicename-datetimestamp** folders.</span></span> <span data-ttu-id="e7df7-291">hello adfjobs 容器包含從 Azure Data Factory 的作業記錄。</span><span class="sxs-lookup"><span data-stu-id="e7df7-291">hello adfjobs container contains job logs from Azure Data Factory.</span></span>

### <a name="delete-hello-resource-group"></a><span data-ttu-id="e7df7-292">刪除 hello 資源群組</span><span class="sxs-lookup"><span data-stu-id="e7df7-292">Delete hello resource group</span></span>
<span data-ttu-id="e7df7-293">[Azure 資源管理員](../azure-resource-manager/resource-group-overview.md)是使用的 toodeploy，管理和監視您的解決方案，為群組。</span><span class="sxs-lookup"><span data-stu-id="e7df7-293">[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) is used toodeploy, manage, and monitor your solution as a group.</span></span>  <span data-ttu-id="e7df7-294">刪除資源群組會刪除所有 hello hello 群組內的元件。</span><span class="sxs-lookup"><span data-stu-id="e7df7-294">Deleting a resource group deletes all hello components inside hello group.</span></span>  

1. <span data-ttu-id="e7df7-295">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="e7df7-295">Sign on toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="e7df7-296">按一下**資源群組**hello 左窗格上。</span><span class="sxs-lookup"><span data-stu-id="e7df7-296">Click **Resource groups** on hello left pane.</span></span>
3. <span data-ttu-id="e7df7-297">按一下您建立 PowerShell 指令碼中的 hello 資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="e7df7-297">Click hello resource group name you created in your PowerShell script.</span></span> <span data-ttu-id="e7df7-298">如果您有太多的資源群組列出，請使用 hello 篩選條件。</span><span class="sxs-lookup"><span data-stu-id="e7df7-298">Use hello filter if you have too many resource groups listed.</span></span> <span data-ttu-id="e7df7-299">會開啟 hello 資源群組的新刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="e7df7-299">It opens hello resource group in a new blade.</span></span>
4. <span data-ttu-id="e7df7-300">在 hello**資源**磚中，您應該擁有 hello 預設儲存體帳戶和 hello 資料處理站所列，除非您與其他專案共用 hello 資源群組。</span><span class="sxs-lookup"><span data-stu-id="e7df7-300">On hello **Resources** tile, you shall have hello default storage account and hello data factory listed unless you share hello resource group with other projects.</span></span>
5. <span data-ttu-id="e7df7-301">按一下**刪除**hello 頂端 hello 刀鋒視窗上。</span><span class="sxs-lookup"><span data-stu-id="e7df7-301">Click **Delete** on hello top of hello blade.</span></span> <span data-ttu-id="e7df7-302">這樣會刪除 hello 儲存體帳戶和儲存在 hello 儲存體帳戶中的 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="e7df7-302">Doing so deletes hello storage account and hello data stored in hello storage account.</span></span>
6. <span data-ttu-id="e7df7-303">輸入 hello 資源群組名稱 tooconfirm 刪除，然後再按一下**刪除**。</span><span class="sxs-lookup"><span data-stu-id="e7df7-303">Enter hello resource group name tooconfirm deletion, and then click **Delete**.</span></span>

<span data-ttu-id="e7df7-304">如果您不想 toodelete hello 儲存體帳戶，當您刪除 hello 資源群組時，請考慮 hello 下列架構藉由分隔 hello 預設儲存體帳戶中的 hello 的商務資料。</span><span class="sxs-lookup"><span data-stu-id="e7df7-304">In case you don't want toodelete hello storage account when you delete hello resource group, consider hello following architecture by separating hello business data from hello default storage account.</span></span> <span data-ttu-id="e7df7-305">在此情況下，您會擁有一個 hello hello 的商務資料的儲存體帳戶的資源群組，並且 hello HDInsight 連結服務與 hello data factory 的 hello 預設儲存體帳戶的其他資源群組。</span><span class="sxs-lookup"><span data-stu-id="e7df7-305">In this case, you have one resource group for hello storage account with hello business data, and hello other resource group for hello default storage account for HDInsight linked service and hello data factory.</span></span> <span data-ttu-id="e7df7-306">當您刪除 hello 第二個資源群組時，它不會影響 hello 商務資料的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="e7df7-306">When you delete hello second resource group, it does not impact hello business data storage account.</span></span> <span data-ttu-id="e7df7-307">toodo 因此：</span><span class="sxs-lookup"><span data-stu-id="e7df7-307">toodo so:</span></span>

* <span data-ttu-id="e7df7-308">新增下列 toohello 最上層資源群組，以及 hello Microsoft.DataFactory/datafactories 資源，資源管理員範本中的 hello。</span><span class="sxs-lookup"><span data-stu-id="e7df7-308">Add hello following toohello top-level resource group along with hello Microsoft.DataFactory/datafactories resource in your Resource Manager template.</span></span> <span data-ttu-id="e7df7-309">它會建立儲存體帳戶：</span><span class="sxs-lookup"><span data-stu-id="e7df7-309">It creates a storage account:</span></span>

    ```json
    {
        "name": "[parameters('defaultStorageAccountName')]",
        "type": "Microsoft.Storage/storageAccounts",
        "location": "[parameters('location')]",
        "apiVersion": "[variables('defaultApiVersion')]",
        "dependsOn": [ ],
        "tags": {

        },
        "properties": {
            "accountType": "Standard_LRS"
        }
    },
    ```
* <span data-ttu-id="e7df7-310">加入新連結的服務點 toohello 新儲存體帳戶：</span><span class="sxs-lookup"><span data-stu-id="e7df7-310">Add a new linked service point toohello new storage account:</span></span>

    ```json
    {
        "dependsOn": [ "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]" ],
        "type": "linkedservices",
        "name": "[variables('defaultStorageLinkedServiceName')]",
        "apiVersion": "[variables('apiVersion')]",
        "properties": {
            "type": "AzureStorage",
            "typeProperties": {
                "connectionString": "[concat('DefaultEndpointsProtocol=https;AccountName=',parameters('defaultStorageAccountName'),';AccountKey=',listKeys(resourceId('Microsoft.Storage/storageAccounts', variables('defaultStorageAccountName')), variables('defaultApiVersion')).key1)]"
            }
        }
    },
    ```
* <span data-ttu-id="e7df7-311">與其他的 dependsOn additionalLinkedServiceNames 設定 hello HDInsight ondemand 連結服務：</span><span class="sxs-lookup"><span data-stu-id="e7df7-311">Configure hello HDInsight ondemand linked service with an additional dependsOn and an additionalLinkedServiceNames:</span></span>

    ```json
    {
        "dependsOn": [
            "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
            "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedservices/', variables('defaultStorageLinkedServiceName'))]",
            "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedservices/', variables('storageLinkedServiceName'))]"

        ],
        "type": "linkedservices",
        "name": "[variables('hdInsightOnDemandLinkedServiceName')]",
        "apiVersion": "[variables('apiVersion')]",
        "properties": {
            "type": "HDInsightOnDemand",
            "typeProperties": {
                "version": "3.5",
                "clusterSize": 1,
                "timeToLive": "00:05:00",
                "osType": "Linux",
                "sshUserName": "myuser",                            
                "sshPassword": "MyPassword!",
                "linkedServiceName": "[variables('storageLinkedServiceName')]",
                "additionalLinkedServiceNames": "[variables('defaultStorageLinkedServiceName')]"
            }
        }
    },            
    ```
## <a name="next-steps"></a><span data-ttu-id="e7df7-312">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e7df7-312">Next steps</span></span>
<span data-ttu-id="e7df7-313">在本文中，您已經學會如何 toouse Azure Data Factory toocreate-隨選 HDInsight 叢集 tooprocess Hive 工作。</span><span class="sxs-lookup"><span data-stu-id="e7df7-313">In this article, you have learned how toouse Azure Data Factory toocreate on-demand HDInsight cluster tooprocess Hive jobs.</span></span> <span data-ttu-id="e7df7-314">多個 tooread:</span><span class="sxs-lookup"><span data-stu-id="e7df7-314">tooread more:</span></span>

* [<span data-ttu-id="e7df7-315">Hadoop 教學課程：開始在 HDInsight 中使用以 Linux 為基礎的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="e7df7-315">Hadoop tutorial: Get started using Linux-based Hadoop in HDInsight</span></span>](hdinsight-hadoop-linux-tutorial-get-started.md)
* [<span data-ttu-id="e7df7-316">在 HDInsight 中建立以 Linux 為基礎的 Hadoop 叢集</span><span class="sxs-lookup"><span data-stu-id="e7df7-316">Create Linux-based Hadoop clusters in HDInsight</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
* [<span data-ttu-id="e7df7-317">HDInsight 文件</span><span class="sxs-lookup"><span data-stu-id="e7df7-317">HDInsight documentation</span></span>](https://azure.microsoft.com/documentation/services/hdinsight/)
* [<span data-ttu-id="e7df7-318">Data Factory 文件</span><span class="sxs-lookup"><span data-stu-id="e7df7-318">Data factory documentation</span></span>](https://azure.microsoft.com/documentation/services/data-factory/)

## <a name="appendix"></a><span data-ttu-id="e7df7-319">附錄</span><span class="sxs-lookup"><span data-stu-id="e7df7-319">Appendix</span></span>

### <a name="azure-cli-script"></a><span data-ttu-id="e7df7-320">Azure CLI 指令碼</span><span class="sxs-lookup"><span data-stu-id="e7df7-320">Azure CLI script</span></span>
<span data-ttu-id="e7df7-321">您可以使用 Azure CLI，而不是使用 Azure PowerShell toodo hello 教學課程。</span><span class="sxs-lookup"><span data-stu-id="e7df7-321">You can use Azure CLI instead of using Azure PowerShell toodo hello tutorial.</span></span> <span data-ttu-id="e7df7-322">toouse Azure CLI 第一次安裝 Azure CLI，依照下列指示的 hello:</span><span class="sxs-lookup"><span data-stu-id="e7df7-322">toouse Azure CLI, first install Azure CLI as per hello following instructions:</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

#### <a name="use-azure-cli-tooprepare-hello-storage-and-copy-hello-files"></a><span data-ttu-id="e7df7-323">使用 Azure CLI tooprepare hello 存放裝置，並將 hello 檔案複製</span><span class="sxs-lookup"><span data-stu-id="e7df7-323">Use Azure CLI tooprepare hello storage and copy hello files</span></span>

```
azure login

azure config mode arm

azure group create --name "<Azure Resource Group Name>" --location "East US 2"

azure storage account create --resource-group "<Azure Resource Group Name>" --location "East US 2" --type "LRS" <Azure Storage Account Name>

azure storage account keys list --resource-group "<Azure Resource Group Name>" "<Azure Storage Account Name>"
azure storage container create "adfgetstarted" --account-name "<Azure Storage AccountName>" --account-key "<Azure Storage Account Key>"

azure storage blob copy start "https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log" --dest-account-name "<Azure Storage Account Name>" --dest-account-key "<Azure Storage Account Key>" --dest-container "adfgetstarted"
azure storage blob copy start "https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql" --dest-account-name "<Azure Storage Account Name>" --dest-account-key "<Azure Storage Account Key>" --dest-container "adfgetstarted"
```

<span data-ttu-id="e7df7-324">hello 的容器名稱*adfgetstarted*。</span><span class="sxs-lookup"><span data-stu-id="e7df7-324">hello container name is *adfgetstarted*.</span></span> <span data-ttu-id="e7df7-325">讓它保持原狀。</span><span class="sxs-lookup"><span data-stu-id="e7df7-325">Keep it as it is.</span></span> <span data-ttu-id="e7df7-326">否則，您必須 tooupdate hello Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="e7df7-326">Otherwise you need tooupdate hello Resource Manager template.</span></span> <span data-ttu-id="e7df7-327">如果您需要此 CLI 指令碼的說明，請參閱[使用 hello 與 Azure 儲存體的 Azure CLI](../storage/common/storage-azure-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="e7df7-327">If you need help with this CLI script, see [Using hello Azure CLI with Azure Storage](../storage/common/storage-azure-cli.md).</span></span>
