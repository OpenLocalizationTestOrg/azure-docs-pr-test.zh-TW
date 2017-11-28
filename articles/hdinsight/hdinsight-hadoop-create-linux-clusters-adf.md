---
title: "使用 Data Factory 建立隨選 Hadoop 叢集 - Azure HDInsight | Microsoft Docs"
description: "了解如何使用 Azure Data Factory 在 HDInsight 中建立隨選 Handooop 叢集。"
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
ms.openlocfilehash: e68f1d72965d9516e0552c84d03d234c21739390
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="create-on-demand-hadoop-clusters-in-hdinsight-using-azure-data-factory"></a><span data-ttu-id="bc749-103">使用 Azure Data Factory 在 HDInsight 中建立隨選 Handooop 叢集</span><span class="sxs-lookup"><span data-stu-id="bc749-103">Create on-demand Hadoop clusters in HDInsight using Azure Data Factory</span></span>
[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="bc749-104">[Azure Data Factory](../data-factory/data-factory-introduction.md) 是雲端架構資料整合服務，用來協調以及自動移動和轉換資料。</span><span class="sxs-lookup"><span data-stu-id="bc749-104">[Azure Data Factory](../data-factory/data-factory-introduction.md) is a cloud-based data integration service that orchestrates and automates the movement and transformation of data.</span></span> <span data-ttu-id="bc749-105">它可以建立 HDInsight Hadoop 叢集 Just-in-Time 來處理輸入資料配量並在處理序完成時刪除叢集。</span><span class="sxs-lookup"><span data-stu-id="bc749-105">It can create a HDInsight Hadoop cluster just-in-time to process an input data slice and delete the cluster when the processing is complete.</span></span> <span data-ttu-id="bc749-106">使用隨選 HDInsight Hadoop 叢集的優點包括︰</span><span class="sxs-lookup"><span data-stu-id="bc749-106">Some of the benefits of using an on-demand HDInsight Hadoop cluster are:</span></span>

- <span data-ttu-id="bc749-107">您只需支付作業在 HDInsight Hadoop 叢集上執行的時間 (加上簡短的可設定閒置時間)。</span><span class="sxs-lookup"><span data-stu-id="bc749-107">You only pay for the time job is running on the HDInsight Hadoop cluster (plus a brief configurable idle time).</span></span> <span data-ttu-id="bc749-108">不論使用與否，HDInsight 叢集都是按分鐘計費。</span><span class="sxs-lookup"><span data-stu-id="bc749-108">The billing for HDInsight clusters is pro-rated per minute, whether you are using them or not.</span></span> <span data-ttu-id="bc749-109">當您在 Data Factory 中使用隨選 HDInsight 連結服務時，會隨選建立叢集。</span><span class="sxs-lookup"><span data-stu-id="bc749-109">When you use an on-demand HDInsight linked service in Data Factory, the clusters are created on-demand.</span></span> <span data-ttu-id="bc749-110">而叢集會在作業完成時自動刪除。</span><span class="sxs-lookup"><span data-stu-id="bc749-110">And the clusters are deleted automatically when the jobs are completed.</span></span> <span data-ttu-id="bc749-111">所以您只需對作業執行時間和短暫閒置時間 (存留時間設定) 付費。</span><span class="sxs-lookup"><span data-stu-id="bc749-111">Therefore, you only pay for the job running time and the brief idle time (time-to-live setting).</span></span>
- <span data-ttu-id="bc749-112">您可以使用 Data Factory 管線建立工作流程。</span><span class="sxs-lookup"><span data-stu-id="bc749-112">You can create a workflow using a Data Factory pipeline.</span></span> <span data-ttu-id="bc749-113">例如，您可以用管線將資料從內部部署 SQL Server 複製到 Azure blob 儲存體，在隨選 HDInsight Hadoop 叢集上執行 Hive 指令碼和 Pig 指令碼來處理資料。</span><span class="sxs-lookup"><span data-stu-id="bc749-113">For example, you can have the pipeline to copy data from an on-premises SQL Server to an Azure blob storage, process the data by running a Hive script and a Pig script on an on-demand HDInsight Hadoop cluster.</span></span> <span data-ttu-id="bc749-114">然後，將結果資料複製到 Azure SQL 資料倉儲以供 BI 應用程式使用。</span><span class="sxs-lookup"><span data-stu-id="bc749-114">Then, copy the result data to an Azure SQL Data Warehouse for BI applications to consume.</span></span>
- <span data-ttu-id="bc749-115">您可以排程定期 (每小時、每天、每週、每月等) 執行工作流程。</span><span class="sxs-lookup"><span data-stu-id="bc749-115">You can schedule the workflow to run periodically (hourly, daily, weekly, monthly, etc.).</span></span>

<span data-ttu-id="bc749-116">在 Azure Data Factory 中，資料處理站可以有一或多個資料管線。</span><span class="sxs-lookup"><span data-stu-id="bc749-116">In Azure Data Factory, a data factory can have one or more data pipelines.</span></span> <span data-ttu-id="bc749-117">資料管線具有一或多個活動。</span><span class="sxs-lookup"><span data-stu-id="bc749-117">A data pipeline has one or more activities.</span></span> <span data-ttu-id="bc749-118">兩種活動類型︰[資料移動活動](../data-factory/data-factory-data-movement-activities.md)和[資料轉換活動](../data-factory/data-factory-data-transformation-activities.md)。</span><span class="sxs-lookup"><span data-stu-id="bc749-118">There are two types of activities: [Data Movement Activities](../data-factory/data-factory-data-movement-activities.md) and [Data Transformation Activities](../data-factory/data-factory-data-transformation-activities.md).</span></span> <span data-ttu-id="bc749-119">您可以使用資料移動活動 (目前，只有複製活動)，將資料從來源資料存放區移到目的地資料存放區。</span><span class="sxs-lookup"><span data-stu-id="bc749-119">You use data movement activities (currently, only Copy Activity) to move data from a source data store to a destination data store.</span></span> <span data-ttu-id="bc749-120">使用資料轉換活動以處理/轉換資料。</span><span class="sxs-lookup"><span data-stu-id="bc749-120">You use data transformation activities to transform/process data.</span></span> <span data-ttu-id="bc749-121">HDInsight Hive 活動是 Data Factory 所支援的其中一個轉換活動。</span><span class="sxs-lookup"><span data-stu-id="bc749-121">HDInsight Hive Activity is one of the transformation activities supported by Data Factory.</span></span> <span data-ttu-id="bc749-122">您在本教學課程中使用 Hive 轉換活動。</span><span class="sxs-lookup"><span data-stu-id="bc749-122">You use the Hive transformation activity in this tutorial.</span></span>

<span data-ttu-id="bc749-123">您可以設定 Hive 活動使用您自己的 HDInsight Hadoop 叢集或隨選 HDInsight Hadoop 叢集。</span><span class="sxs-lookup"><span data-stu-id="bc749-123">You can configure a hive activity to use your own HDInsight Hadoop cluster or an on-demand HDInsight Hadoop cluster.</span></span> <span data-ttu-id="bc749-124">在本教學課程中，資料處理站管線中的 Hive 活動會設定為使用隨 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="bc749-124">In this tutorial, the Hive activity in the data factory pipeline is configured to use an on-demand HDInsight cluster.</span></span> <span data-ttu-id="bc749-125">因此，當執行活動以處理資料配量時，以下是會發生的事︰</span><span class="sxs-lookup"><span data-stu-id="bc749-125">Therefore, when the activity runs to process a data slice, here is what happens:</span></span>

1. <span data-ttu-id="bc749-126">會自動建立 HDInsight Hadoop 叢集 just-in-time 以處理配量。</span><span class="sxs-lookup"><span data-stu-id="bc749-126">A HDInsight Hadoop cluster is automatically created for you just-in-time to process the slice.</span></span>  
2. <span data-ttu-id="bc749-127">會在叢集上執行 HiveQL 指令碼以處理輸入資料。</span><span class="sxs-lookup"><span data-stu-id="bc749-127">The input data is processed by running a HiveQL script on the cluster.</span></span>
3. <span data-ttu-id="bc749-128">處理完成後，會刪除 HDInsight Hadoop 叢集，且叢集在設定的一段時間會處於閒置狀態 (timeToLive 設定)。</span><span class="sxs-lookup"><span data-stu-id="bc749-128">The HDInsight Hadoop cluster is deleted after the processing is complete and the cluster is idle for the configured amount of time (timeToLive setting).</span></span> <span data-ttu-id="bc749-129">如果下一個資料配量可用於在此 timeToLive 閒置時間中進行處理，相同的叢集會用來處理配量。</span><span class="sxs-lookup"><span data-stu-id="bc749-129">If the next data slice is available for processing with in this timeToLive idle time, the same cluster is used to process the slice.</span></span>  

<span data-ttu-id="bc749-130">在本教學課程中，與 Hive 活動相關聯的 HiveQL 指令碼會執行下列動作︰</span><span class="sxs-lookup"><span data-stu-id="bc749-130">In this tutorial, the HiveQL script associated with the hive activity performs the following actions:</span></span>

1. <span data-ttu-id="bc749-131">建立參考儲存在 Azure blob 儲存體中未經處理之 Web 記錄資料的外部資料表。</span><span class="sxs-lookup"><span data-stu-id="bc749-131">Creates an external table that references the raw web log data stored in an Azure Blob storage.</span></span>
2. <span data-ttu-id="bc749-132">依年份和月份分割的未經處理資料。</span><span class="sxs-lookup"><span data-stu-id="bc749-132">Partitions the raw data by year and month.</span></span>
3. <span data-ttu-id="bc749-133">Azure blob 儲存體中儲存的分割資料。</span><span class="sxs-lookup"><span data-stu-id="bc749-133">Stores the partitioned data in the Azure blob storage.</span></span>

<span data-ttu-id="bc749-134">在本教學課程中，與 Hive 活動相關聯的 HiveQL 指令碼會建立外部資料表，其會參考 Azure Blob 儲存體中儲存的未經處理 web 記錄資料。</span><span class="sxs-lookup"><span data-stu-id="bc749-134">In this tutorial, the HiveQL script associated with the hive activity creates an external table that references the raw web log data stored in the Azure Blob Storage.</span></span> <span data-ttu-id="bc749-135">這裡是輸入檔中每個月份的資料列範例。</span><span class="sxs-lookup"><span data-stu-id="bc749-135">Here are the sample rows for each month in the input file.</span></span>

```
2014-01-01,02:01:09,SAMPLEWEBSITE,GET,/blogposts/mvc4/step2.png,X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,53175,871
2014-02-01,02:01:10,SAMPLEWEBSITE,GET,/blogposts/mvc4/step7.png,X-ARR-LOG-ID=d7472a26-431a-4a4d-99eb-c7b4fda2cf4c,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,30184,871
2014-03-01,02:01:10,SAMPLEWEBSITE,GET,/blogposts/mvc4/step7.png,X-ARR-LOG-ID=d7472a26-431a-4a4d-99eb-c7b4fda2cf4c,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,30184,871
```

<span data-ttu-id="bc749-136">HiveQL 指令碼會依年份和月份分割未經處理的資料。</span><span class="sxs-lookup"><span data-stu-id="bc749-136">The HiveQL script partitions the raw data by year and month.</span></span> <span data-ttu-id="bc749-137">它會根據先前的輸入建立三個輸出資料夾。</span><span class="sxs-lookup"><span data-stu-id="bc749-137">It creates three output folders based on the previous input.</span></span> <span data-ttu-id="bc749-138">每個資料夾都包含一個檔案，內含每個月的項目。</span><span class="sxs-lookup"><span data-stu-id="bc749-138">Each folder contains a file with entries from each month.</span></span>

```
adfgetstarted/partitioneddata/year=2014/month=1/000000_0
adfgetstarted/partitioneddata/year=2014/month=2/000000_0
adfgetstarted/partitioneddata/year=2014/month=3/000000_0
```

<span data-ttu-id="bc749-139">如需 Data Factory 資料轉換活動 (Hive 活動除外) 的清單，請參閱 [使用 Azure Data Factory 進行轉換和分析](../data-factory/data-factory-data-transformation-activities.md)。</span><span class="sxs-lookup"><span data-stu-id="bc749-139">For a list of Data Factory data transformation activities in addition to Hive activity, see [Transform and analyze using Azure Data Factory](../data-factory/data-factory-data-transformation-activities.md).</span></span>

> [!NOTE]
> <span data-ttu-id="bc749-140">目前，您只可以從 Azure Data Factory 建立 HDInsight 叢集 3.2 版。</span><span class="sxs-lookup"><span data-stu-id="bc749-140">Currently, you can only create HDInsight cluster version 3.2 from Azure Data Factory.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bc749-141">必要條件</span><span class="sxs-lookup"><span data-stu-id="bc749-141">Prerequisites</span></span>
<span data-ttu-id="bc749-142">開始執行本文中的指示之前，您必須擁有以下項目：</span><span class="sxs-lookup"><span data-stu-id="bc749-142">Before you begin the instructions in this article, you must have the following items:</span></span>

* <span data-ttu-id="bc749-143">[Azure 訂用帳戶](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)。</span><span class="sxs-lookup"><span data-stu-id="bc749-143">[Azure subscription](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="bc749-144">Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="bc749-144">Azure PowerShell.</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-powershell.md)]

### <a name="prepare-storage-account"></a><span data-ttu-id="bc749-145">準備儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="bc749-145">Prepare storage account</span></span>
<span data-ttu-id="bc749-146">在此案例中，您最多可以使用三個儲存體帳戶︰</span><span class="sxs-lookup"><span data-stu-id="bc749-146">You can use up to three storage accounts in this scenario:</span></span>

- <span data-ttu-id="bc749-147">HDInsight 叢集的預設儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="bc749-147">default storage account for the HDInsight cluster</span></span>
- <span data-ttu-id="bc749-148">輸入資料的儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="bc749-148">storage account for the input data</span></span>
- <span data-ttu-id="bc749-149">輸出資料的儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="bc749-149">storage account for the output data</span></span>

<span data-ttu-id="bc749-150">為了簡化本教學課程，您會將一個儲存體帳戶用於 3 個用途。</span><span class="sxs-lookup"><span data-stu-id="bc749-150">To simplify the tutorial, you use one storage account to serve the three purposes.</span></span> <span data-ttu-id="bc749-151">本節中找到的 Azure PowerShell 範例指令碼會執行下列工作：</span><span class="sxs-lookup"><span data-stu-id="bc749-151">The Azure PowerShell sample script found in this section performs the following tasks:</span></span>

1. <span data-ttu-id="bc749-152">登入 Azure。</span><span class="sxs-lookup"><span data-stu-id="bc749-152">Log in to Azure.</span></span>
2. <span data-ttu-id="bc749-153">建立 Azure 資源群組。</span><span class="sxs-lookup"><span data-stu-id="bc749-153">Create an Azure resource group.</span></span>
3. <span data-ttu-id="bc749-154">建立 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="bc749-154">Create an Azure Storage account.</span></span>
4. <span data-ttu-id="bc749-155">在儲存體帳戶中建立 Blob 容器</span><span class="sxs-lookup"><span data-stu-id="bc749-155">Create a Blob container in the storage account</span></span>
5. <span data-ttu-id="bc749-156">將下列兩個檔案複製到 Blob 容器︰</span><span class="sxs-lookup"><span data-stu-id="bc749-156">Copy the following two files to the Blob container:</span></span>

   * <span data-ttu-id="bc749-157">輸入資料檔： [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log)</span><span class="sxs-lookup"><span data-stu-id="bc749-157">Input data file: [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log)</span></span>
   * <span data-ttu-id="bc749-158">HiveQL 指令碼： [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql)</span><span class="sxs-lookup"><span data-stu-id="bc749-158">HiveQL script: [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql)</span></span>

     <span data-ttu-id="bc749-159">這兩個檔案會儲存在公用 Blob 容器。</span><span class="sxs-lookup"><span data-stu-id="bc749-159">Both files are stored in a public Blob container.</span></span>


<span data-ttu-id="bc749-160">**使用 Azure PowerShell 準備處存體並複製檔案：**</span><span class="sxs-lookup"><span data-stu-id="bc749-160">**To prepare the storage and copy the files using Azure PowerShell:**</span></span>
> [!IMPORTANT]
> <span data-ttu-id="bc749-161">指定指令碼會建立之 Azure 資源群組和 Azure 儲存體帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="bc749-161">Specify names for the Azure resource group and the Azure storage account that will be created by the script.</span></span>
> <span data-ttu-id="bc749-162">記下指令碼所輸出的**資源群組名稱**、**儲存體帳戶名稱**和**儲存體帳戶金鑰**。</span><span class="sxs-lookup"><span data-stu-id="bc749-162">Write down **resource group name**, **storage account name**, and **storage account key** outputted by the script.</span></span> <span data-ttu-id="bc749-163">您在下一節中需要這些資料。</span><span class="sxs-lookup"><span data-stu-id="bc749-163">You need them in the next section.</span></span>

```powershell
$resourceGroupName = "<Azure Resource Group Name>"
$storageAccountName = "<Azure Storage Account Name>"
$location = "East US 2"

$sourceStorageAccountName = "hditutorialdata"  
$sourceContainerName = "adfhiveactivity"

$destStorageAccountName = $storageAccountName
$destContainerName = "adfgetstarted" # don't change this value.

####################################
# Connect to Azure
####################################
#region - Connect to Azure subscription
Write-Host "`nConnecting to your Azure subscription ..." -ForegroundColor Green
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

Write-host "`nYou will use the following values:" -ForegroundColor Green
write-host "`nResource group name: $resourceGroupName"
Write-host "Storage Account Name: $destStorageAccountName"
write-host "Storage Account Key: $destStorageAccountKey"

Write-host "`nScript completed" -ForegroundColor Green
```

<span data-ttu-id="bc749-164">如需有關此 PowerShell 指定碼的說明，請參閱 [使用 Azure PowerShell 搭配 Azure 儲存體](../storage/common/storage-powershell-guide-full.md)。</span><span class="sxs-lookup"><span data-stu-id="bc749-164">If you need help with the PowerShell script, see [Using the Azure PowerShell with Azure Storage](../storage/common/storage-powershell-guide-full.md).</span></span> <span data-ttu-id="bc749-165">如果您想要改為使用 Azure CLI，請參閱 Azure CLI 指令碼的[附錄](#appendix)區段。</span><span class="sxs-lookup"><span data-stu-id="bc749-165">If you like to use Azure CLI instead, see the [Appendix](#appendix) section for the Azure CLI script.</span></span>

<span data-ttu-id="bc749-166">**檢查儲存體帳戶和內容**</span><span class="sxs-lookup"><span data-stu-id="bc749-166">**To examine the storage account and the contents**</span></span>

1. <span data-ttu-id="bc749-167">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="bc749-167">Sign on to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="bc749-168">按一下左側面板上的 [資源群組]  。</span><span class="sxs-lookup"><span data-stu-id="bc749-168">Click **Resource groups** on the left pane.</span></span>
3. <span data-ttu-id="bc749-169">按兩下您在 PowerShell 指令碼中建立的資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="bc749-169">Double-click the resource group name you created in your PowerShell script.</span></span> <span data-ttu-id="bc749-170">如果列出太多的資源群組，請使用篩選器。</span><span class="sxs-lookup"><span data-stu-id="bc749-170">Use the filter if you have too many resource groups listed.</span></span>
4. <span data-ttu-id="bc749-171">除非您與其他專案共用資源群組，否則 [資源]  圖格應列出一個資源。</span><span class="sxs-lookup"><span data-stu-id="bc749-171">On the **Resources** tile, you shall have one resource listed unless you share the resource group with other projects.</span></span> <span data-ttu-id="bc749-172">該資源是您先前指定名稱的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="bc749-172">That resource is the storage account with the name you specified earlier.</span></span> <span data-ttu-id="bc749-173">按一下儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="bc749-173">Click the storage account name.</span></span>
5. <span data-ttu-id="bc749-174">按一下 [Blob]  圖格。</span><span class="sxs-lookup"><span data-stu-id="bc749-174">Click the **Blobs** tiles.</span></span>
6. <span data-ttu-id="bc749-175">按一下 [adfgetstarted]  容器。</span><span class="sxs-lookup"><span data-stu-id="bc749-175">Click the **adfgetstarted** container.</span></span> <span data-ttu-id="bc749-176">您會看到兩個資料夾︰[輸入資料] 和 [指令碼]。</span><span class="sxs-lookup"><span data-stu-id="bc749-176">You see two folders: **inputdata** and **script**.</span></span>
7. <span data-ttu-id="bc749-177">開啟資料夾並檢查資料夾中的檔案。</span><span class="sxs-lookup"><span data-stu-id="bc749-177">Open the folder and check the files in the folders.</span></span> <span data-ttu-id="bc749-178">Inputdata 包含 input.log 檔案與輸入資料，而指令碼資料夾包含 HiveQL 指令碼檔案。</span><span class="sxs-lookup"><span data-stu-id="bc749-178">The inputdata contains the input.log file with input data and the script folder contains the HiveQL script file.</span></span>

## <a name="create-a-data-factory-using-resource-manager-template"></a><span data-ttu-id="bc749-179">使用 Resource Manager 範本建立資料處理站</span><span class="sxs-lookup"><span data-stu-id="bc749-179">Create a data factory using Resource Manager template</span></span>
<span data-ttu-id="bc749-180">備妥儲存體帳戶、輸入資料和 HiveQL 指令碼，您就準備好建立 Azure Data Factory。</span><span class="sxs-lookup"><span data-stu-id="bc749-180">With the storage account, the input data, and the HiveQL script prepared, you are ready to create an Azure data factory.</span></span> <span data-ttu-id="bc749-181">有數種方法可建立 Data Factory。</span><span class="sxs-lookup"><span data-stu-id="bc749-181">There are several methods for creating data factory.</span></span> <span data-ttu-id="bc749-182">在本教學課程中，您會使用 Azure 入口網站部署 Azure Resource Manager 範本來建立資料處理站。</span><span class="sxs-lookup"><span data-stu-id="bc749-182">In this tutorial, you create a data factory by deploying an Azure Resource Manager template using the Azure portal.</span></span> <span data-ttu-id="bc749-183">您也可以使用 [Azure CLI](../azure-resource-manager/resource-group-template-deploy-cli.md) 和 [Azure PowerShell](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template) 部署 Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="bc749-183">You can also deploy a Resource Manager template by using [Azure CLI](../azure-resource-manager/resource-group-template-deploy-cli.md) and [Azure PowerShell](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template).</span></span> <span data-ttu-id="bc749-184">如需其他 Data Factory 建立方法，請參閱 [教學課程︰建立您的第一個 Data Factory](../data-factory/data-factory-build-your-first-pipeline.md)。</span><span class="sxs-lookup"><span data-stu-id="bc749-184">For other data factory creation methods, see [Tutorial: Build your first data factory](../data-factory/data-factory-build-your-first-pipeline.md).</span></span>

1. <span data-ttu-id="bc749-185">按一下以下影像，在 Azure 入口網站中登入 Azure 並開啟 Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="bc749-185">Click the following image to sign in to Azure and open the Resource Manager template in the Azure portal.</span></span> <span data-ttu-id="bc749-186">範本是位於 https://hditutorialdata.blob.core.windows.net/adfhiveactivity/data-factory-hdinsight-on-demand.json。</span><span class="sxs-lookup"><span data-stu-id="bc749-186">The template is located at https://hditutorialdata.blob.core.windows.net/adfhiveactivity/data-factory-hdinsight-on-demand.json.</span></span> <span data-ttu-id="bc749-187">請參閱[範本中的 Data Factory 實體](#data-factory-entities-in-the-template)一節以取得範本中所定義的實體詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="bc749-187">See the [Data Factory entities in the template](#data-factory-entities-in-the-template) section for detailed information about entities defined in the template.</span></span> 

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Fadfhiveactivity%2Fdata-factory-hdinsight-on-demand.json" target="_blank"><img src="./media/hdinsight-hadoop-create-linux-clusters-adf/deploy-to-azure.png" alt="Deploy to Azure"></a>
2. <span data-ttu-id="bc749-188">針對**資源群組**設定選取 [使用現有] 選項，然後選取您在上一個步驟 (使用 PowerShell 指令碼) 中建立的資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="bc749-188">Select **Use existing** option for the **Resource group** setting, and select the name of the resource group you created in the previous step (using PowerShell script).</span></span>
3. <span data-ttu-id="bc749-189">輸入資料處理站的名稱 (**Data Factory 名稱**)。</span><span class="sxs-lookup"><span data-stu-id="bc749-189">Enter a name for the data factory (**Data Factory Name**).</span></span> <span data-ttu-id="bc749-190">此名稱必須是全域唯一的。</span><span class="sxs-lookup"><span data-stu-id="bc749-190">This name must be globally unique.</span></span>
4. <span data-ttu-id="bc749-191">輸入您在上一個步驟中記下的**儲存體帳戶名稱**和**儲存帳戶金鑰**。</span><span class="sxs-lookup"><span data-stu-id="bc749-191">Enter the **storage account name** and **storage account key** you wrote down in the previous step.</span></span>
5. <span data-ttu-id="bc749-192">閱讀**條款及條件**後，選取 [我同意上方所述的條款及條件]。</span><span class="sxs-lookup"><span data-stu-id="bc749-192">Select **I agree to the terms and conditions** stated above after reading through **terms and conditions**.</span></span>
6. <span data-ttu-id="bc749-193">選取 [釘選到儀表板] 選項。</span><span class="sxs-lookup"><span data-stu-id="bc749-193">Select **Pin to dashboard** option.</span></span>
6. <span data-ttu-id="bc749-194">按一下 [購買/建立]。</span><span class="sxs-lookup"><span data-stu-id="bc749-194">Click **Purchase/Create**.</span></span> <span data-ttu-id="bc749-195">您將會在儀表板上看到名稱為 [進行範本部署] 的圖格。</span><span class="sxs-lookup"><span data-stu-id="bc749-195">You see a tile on the Dashboard called **Deploying Template deployment**.</span></span> <span data-ttu-id="bc749-196">等到您資源群組的 [資源群組] 刀鋒視窗開啟。</span><span class="sxs-lookup"><span data-stu-id="bc749-196">Wait until the **Resource group** blade for your resource group opens.</span></span> <span data-ttu-id="bc749-197">您也可以按一下以您的資源群組名稱為標題的圖格，開啟資源群組刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="bc749-197">You can also click the tile titled as your resource group name to open the resource group blade.</span></span>
6. <span data-ttu-id="bc749-198">如果資源群組刀鋒視窗尚未開啟，按一下圖格以開啟資源群組。</span><span class="sxs-lookup"><span data-stu-id="bc749-198">Click the tile to open the resource group if the resource group blade is not already open.</span></span> <span data-ttu-id="bc749-199">除了儲存體帳戶資源，您現在應該會看到另外列出一個 Data Factory 資源。</span><span class="sxs-lookup"><span data-stu-id="bc749-199">Now you shall see one more data factory resource listed in addition to the storage account resource.</span></span>
7. <span data-ttu-id="bc749-200">按一下您資料處理站的名稱 (您為 **Data Factory 名稱**參數所指定的值)。</span><span class="sxs-lookup"><span data-stu-id="bc749-200">Click the name of your data factory (value you specified for the **Data Factory Name** parameter).</span></span>
8. <span data-ttu-id="bc749-201">在 [Data Factory] 刀鋒視窗中，按一下 [圖表] 圖格。</span><span class="sxs-lookup"><span data-stu-id="bc749-201">In the Data Factory blade, click the **Diagram** tile.</span></span> <span data-ttu-id="bc749-202">此圖顯示一個具有輸入資料集與輸出資料集的活動︰</span><span class="sxs-lookup"><span data-stu-id="bc749-202">The diagram shows one activity with an input dataset, and an output dataset:</span></span>

    ![Azure Data Factory HDInsight 隨選 Hive 活動管線圖](./media/hdinsight-hadoop-create-linux-clusters-adf/hdinsight-adf-pipeline-diagram.png)

    <span data-ttu-id="bc749-204">資源會在 Resource Manager 範本中定義。</span><span class="sxs-lookup"><span data-stu-id="bc749-204">The names are defined in the Resource Manager template.</span></span>
9. <span data-ttu-id="bc749-205">按兩下 [AzureBlobOutput] 。</span><span class="sxs-lookup"><span data-stu-id="bc749-205">Double-click **AzureBlobOutput**.</span></span>
10. <span data-ttu-id="bc749-206">在 [最近更新的配量] 上，您應該會看到一個配量。</span><span class="sxs-lookup"><span data-stu-id="bc749-206">On the **Recent updated slices**, you shall see one slice.</span></span> <span data-ttu-id="bc749-207">如果狀態為 [進行中]，請等到其變更為 [就緒]。</span><span class="sxs-lookup"><span data-stu-id="bc749-207">If the status is **In progress**, wait until it is changed to **Ready**.</span></span> <span data-ttu-id="bc749-208">建立 HDInsight 叢集通常需要大約 **20 分鐘**的時間。</span><span class="sxs-lookup"><span data-stu-id="bc749-208">It usually takes about **20 minutes** to create an HDInsight cluster.</span></span>

### <a name="check-the-data-factory-output"></a><span data-ttu-id="bc749-209">檢查 Data Factory 輸出</span><span class="sxs-lookup"><span data-stu-id="bc749-209">Check the data factory output</span></span>

1. <span data-ttu-id="bc749-210">使用最後一個工作階段中的相同程序來檢查 adfgetstarted 容器的內容。</span><span class="sxs-lookup"><span data-stu-id="bc749-210">Use the same procedure in the last session to check the containers of the adfgetstarted container.</span></span> <span data-ttu-id="bc749-211">除了 adfgetsarted ，有兩個新容器：</span><span class="sxs-lookup"><span data-stu-id="bc749-211">There are two new containers in addition to **adfgetsarted**:</span></span>

   * <span data-ttu-id="bc749-212">具有遵循模式之名稱的容器︰`adf<yourdatafactoryname>-linkedservicename-datetimestamp`。</span><span class="sxs-lookup"><span data-stu-id="bc749-212">A container with name that follows the pattern: `adf<yourdatafactoryname>-linkedservicename-datetimestamp`.</span></span> <span data-ttu-id="bc749-213">此容器是 HDInsight 叢集的預設容器。</span><span class="sxs-lookup"><span data-stu-id="bc749-213">This container is the default container for the HDInsight cluster.</span></span>
   * <span data-ttu-id="bc749-214">adfjobs︰這個容器是 ADF 作業記錄檔的容器。</span><span class="sxs-lookup"><span data-stu-id="bc749-214">adfjobs: This container is the container for the ADF job logs.</span></span>

     <span data-ttu-id="bc749-215">如同您在 Resource Manager 範本中所設定，Data Factory 的輸出會儲存在 **afgetstarted** 中。</span><span class="sxs-lookup"><span data-stu-id="bc749-215">The data factory output is stored in **afgetstarted** as you configured in the Resource Manager template.</span></span>
2. <span data-ttu-id="bc749-216">按一下 [adfgetstarted] 。</span><span class="sxs-lookup"><span data-stu-id="bc749-216">Click **adfgetstarted**.</span></span>
3. <span data-ttu-id="bc749-217">按兩下 [partitioneddata] 。</span><span class="sxs-lookup"><span data-stu-id="bc749-217">Double-click **partitioneddata**.</span></span> <span data-ttu-id="bc749-218">您會看到 **year=2014** 資料夾，因為所有 Web 記錄檔的日期皆為 2014 年。</span><span class="sxs-lookup"><span data-stu-id="bc749-218">You see a **year=2014** folder because all the web logs are dated in year 2014.</span></span>

    ![Azure Data Factory HDInsight 隨選 Hive 活動管線輸出](./media/hdinsight-hadoop-create-linux-clusters-adf/hdinsight-adf-output-year.png)

    <span data-ttu-id="bc749-220">如果您向下鑽研清單，您會看到一月、二月和三月的 3 個資料夾。</span><span class="sxs-lookup"><span data-stu-id="bc749-220">If you drill down the list, you shall see three folders for January, February, and March.</span></span> <span data-ttu-id="bc749-221">而且每個月都有記錄檔。</span><span class="sxs-lookup"><span data-stu-id="bc749-221">And there is a log for each month.</span></span>

    ![Azure Data Factory HDInsight 隨選 Hive 活動管線輸出](./media/hdinsight-hadoop-create-linux-clusters-adf/hdinsight-adf-output-month.png)

## <a name="data-factory-entities-in-the-template"></a><span data-ttu-id="bc749-223">範本中的 Data Factory 實體</span><span class="sxs-lookup"><span data-stu-id="bc749-223">Data Factory entities in the template</span></span>
<span data-ttu-id="bc749-224">用於資料處理站的最上層 Resource Manager 範本看起來如下︰</span><span class="sxs-lookup"><span data-stu-id="bc749-224">Here is how the top-level Resource Manager template for a data factory looks like:</span></span>

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

### <a name="define-data-factory"></a><span data-ttu-id="bc749-225">定義資料處理站</span><span class="sxs-lookup"><span data-stu-id="bc749-225">Define data factory</span></span>
<span data-ttu-id="bc749-226">您可以在 Resource Manager 範本中定義資料處理站，如下列範例所示︰</span><span class="sxs-lookup"><span data-stu-id="bc749-226">You define a data factory in the Resource Manager template as shown in the following sample:</span></span>  

```json
"resources": [
{
    "name": "[parameters('dataFactoryName')]",
    "apiVersion": "[variables('apiVersion')]",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "westus",
}
```
<span data-ttu-id="bc749-227">DataFactoryName 是您在部署範本時指定的資料處理站名稱。</span><span class="sxs-lookup"><span data-stu-id="bc749-227">The dataFactoryName is the name of the data factory you specify when you deploy the template.</span></span> <span data-ttu-id="bc749-228">目前只有美國東部、美國西部和北歐地區支援 Data Factory。</span><span class="sxs-lookup"><span data-stu-id="bc749-228">Data factory is currently only supported in the East US, West US, and North Europe regions.</span></span>

### <a name="defining-entities-within-the-data-factory"></a><span data-ttu-id="bc749-229">在資料處理站內定義實體</span><span class="sxs-lookup"><span data-stu-id="bc749-229">Defining entities within the data factory</span></span>
<span data-ttu-id="bc749-230">下列的 Data Factory 實體定義於 JSON 範本中︰</span><span class="sxs-lookup"><span data-stu-id="bc749-230">The following Data Factory entities are defined in the JSON template:</span></span>

* [<span data-ttu-id="bc749-231">Azure 儲存體連結服務</span><span class="sxs-lookup"><span data-stu-id="bc749-231">Azure Storage linked service</span></span>](#azure-storage-linked-service)
* [<span data-ttu-id="bc749-232">HDInsight 隨選連結服務</span><span class="sxs-lookup"><span data-stu-id="bc749-232">HDInsight on-demand linked service</span></span>](#hdinsight-on-demand-linked-service)
* [<span data-ttu-id="bc749-233">Azure Blob 輸入資料集</span><span class="sxs-lookup"><span data-stu-id="bc749-233">Azure blob input dataset</span></span>](#azure-blob-input-dataset)
* [<span data-ttu-id="bc749-234">Azure Blob 輸出資料集</span><span class="sxs-lookup"><span data-stu-id="bc749-234">Azure blob output dataset</span></span>](#azure-blob-output-dataset)
* [<span data-ttu-id="bc749-235">具有複製活動的管線</span><span class="sxs-lookup"><span data-stu-id="bc749-235">Data pipeline with a copy activity</span></span>](#data-pipeline)

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="bc749-236">Azure 儲存體連結服務</span><span class="sxs-lookup"><span data-stu-id="bc749-236">Azure Storage linked service</span></span>
<span data-ttu-id="bc749-237">Azure 儲存體已連結的服務會連結 Azure 儲存體帳戶至資料處理站。</span><span class="sxs-lookup"><span data-stu-id="bc749-237">The Azure Storage linked service links your Azure storage account to the data factory.</span></span> <span data-ttu-id="bc749-238">在本教學課程中，相同的儲存體帳戶會做為預設 HDInsight 儲存體帳戶、輸入資料儲存體和輸出資料儲存體。</span><span class="sxs-lookup"><span data-stu-id="bc749-238">In this tutorial, the same storage account is used as the default HDInsight storage account, input data storage, and output data storage.</span></span> <span data-ttu-id="bc749-239">因此，您只定義一個 Azure 儲存體連結服務。</span><span class="sxs-lookup"><span data-stu-id="bc749-239">Therefore, you define only one Azure Storage linked service.</span></span> <span data-ttu-id="bc749-240">在連結的服務定義中，您指定 Azure 儲存體帳戶的名稱和金鑰。</span><span class="sxs-lookup"><span data-stu-id="bc749-240">In the linked service definition, you specify the name and key of your Azure storage account.</span></span> <span data-ttu-id="bc749-241">如需用來定義 Azure 儲存體連結服務之 JSON 屬性的詳細資料，請參閱 [Azure 儲存體連結服務](../data-factory/data-factory-azure-blob-connector.md#azure-storage-linked-service)。</span><span class="sxs-lookup"><span data-stu-id="bc749-241">See [Azure Storage linked service](../data-factory/data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties used to define an Azure Storage linked service.</span></span>

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
<span data-ttu-id="bc749-242">**connectionString** 會使用 storageAccountName 和 storageAccountKey 參數。</span><span class="sxs-lookup"><span data-stu-id="bc749-242">The **connectionString** uses the storageAccountName and storageAccountKey parameters.</span></span> <span data-ttu-id="bc749-243">您在部署範本時指定這些參數的值。</span><span class="sxs-lookup"><span data-stu-id="bc749-243">You specify values for these parameters while deploying the template.</span></span>  

#### <a name="hdinsight-on-demand-linked-service"></a><span data-ttu-id="bc749-244">HDInsight 隨選連結服務</span><span class="sxs-lookup"><span data-stu-id="bc749-244">HDInsight on-demand linked service</span></span>
<span data-ttu-id="bc749-245">在隨選 HDInsight 連結服務定義中，您可以指定由 Data Factory 服務用來在執行階段建立 HDInsight Hadoop 叢集的組態參數值。</span><span class="sxs-lookup"><span data-stu-id="bc749-245">In the on-demand HDInsight linked service definition, you specify values for configuration parameters that are used by the Data Factory service to create a HDInsight Hadoop cluster at runtime.</span></span> <span data-ttu-id="bc749-246">請參閱[計算連結服務](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service)文章，以取得關於用來定義 HDInsight 隨選連結服務之 JSON 屬性的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="bc749-246">See [Compute linked services](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) article for details about JSON properties used to define an HDInsight on-demand linked service.</span></span>  

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
<span data-ttu-id="bc749-247">請注意下列幾點：</span><span class="sxs-lookup"><span data-stu-id="bc749-247">Note the following points:</span></span>

* <span data-ttu-id="bc749-248">Data Factory 會為您建立**以 Linux 為基礎的** HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="bc749-248">The Data Factory creates a **Linux-based** HDInsight cluster for you.</span></span>
* <span data-ttu-id="bc749-249">HDInsight Hadoop 叢集會並存於與儲存體帳戶相同的區域中。</span><span class="sxs-lookup"><span data-stu-id="bc749-249">The HDInsight Hadoop cluster is created in the same region as the storage account.</span></span>
* <span data-ttu-id="bc749-250">請注意 timeToLive  設定。</span><span class="sxs-lookup"><span data-stu-id="bc749-250">Notice the *timeToLive* setting.</span></span> <span data-ttu-id="bc749-251">Data Factory 會在叢集閒置 30 分鐘後自動刪除叢集。</span><span class="sxs-lookup"><span data-stu-id="bc749-251">The data factory deletes the cluster automatically after the cluster is being idle for 30 minutes.</span></span>
* <span data-ttu-id="bc749-252">HDInsight 叢集會在您於 JSON 中指定的 Blob 儲存體 (**linkedServiceName**) 建立**預設容器**。</span><span class="sxs-lookup"><span data-stu-id="bc749-252">The HDInsight cluster creates a **default container** in the blob storage you specified in the JSON (**linkedServiceName**).</span></span> <span data-ttu-id="bc749-253">HDInsight 不會在刪除叢集時刪除此容器。</span><span class="sxs-lookup"><span data-stu-id="bc749-253">HDInsight does not delete this container when the cluster is deleted.</span></span> <span data-ttu-id="bc749-254">這是設計的行為。</span><span class="sxs-lookup"><span data-stu-id="bc749-254">This behavior is by design.</span></span> <span data-ttu-id="bc749-255">在使用 HDInsight 隨選連結服務時，除非有現有的即時叢集 (**timeToLive**)，否則每當需要處理配量時，就會建立 HDInsight 叢集，並在處理完成時予以刪除。</span><span class="sxs-lookup"><span data-stu-id="bc749-255">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice needs to be processed unless there is an existing live cluster (**timeToLive**) and is deleted when the processing is done.</span></span>

<span data-ttu-id="bc749-256">如需詳細資訊，請參閱 [HDInsight 隨選連結服務](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) 。</span><span class="sxs-lookup"><span data-stu-id="bc749-256">See [On-demand HDInsight Linked Service](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bc749-257">隨著處理的配量越來越多，您會在 Azure Blob 儲存體中看到許多容器。</span><span class="sxs-lookup"><span data-stu-id="bc749-257">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="bc749-258">如果在疑難排解作業時不需要這些容器，建議您加以刪除以降低儲存成本。</span><span class="sxs-lookup"><span data-stu-id="bc749-258">If you do not need them for troubleshooting of the jobs, you may want to delete them to reduce the storage cost.</span></span> <span data-ttu-id="bc749-259">這些容器的名稱遵循下列模式："adf**yourdatafactoryname**-**linkedservicename**-datetimestamp"。</span><span class="sxs-lookup"><span data-stu-id="bc749-259">The names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span></span> <span data-ttu-id="bc749-260">請使用 [Microsoft 儲存體總管](http://storageexplorer.com/) 之類的工具刪除 Azure Blob 儲存體中的容器。</span><span class="sxs-lookup"><span data-stu-id="bc749-260">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) to delete containers in your Azure blob storage.</span></span>

#### <a name="azure-blob-input-dataset"></a><span data-ttu-id="bc749-261">Azure Blob 輸入資料集</span><span class="sxs-lookup"><span data-stu-id="bc749-261">Azure blob input dataset</span></span>
<span data-ttu-id="bc749-262">在輸入資料集定義中，您可以指定 blob 容器、資料夾和包含輸入資料之檔案的名稱。</span><span class="sxs-lookup"><span data-stu-id="bc749-262">In the input dataset definition, you specify the names of blob container, folder, and file that contains the input data.</span></span> <span data-ttu-id="bc749-263">請參閱 [Azure Blob 資料集屬性](../data-factory/data-factory-azure-blob-connector.md#dataset-properties)，以取得用來定義 Azure Blob 資料集之 JSON 屬性的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="bc749-263">See [Azure Blob dataset properties](../data-factory/data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used to define an Azure Blob dataset.</span></span>

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

<span data-ttu-id="bc749-264">請注意下列在 JSON 定義中的特定設定值︰</span><span class="sxs-lookup"><span data-stu-id="bc749-264">Notice the following specific settings in the JSON definition:</span></span>

```json
"fileName": "input.log",
"folderPath": "adfgetstarted/inputdata",
```

#### <a name="azure-blob-output-dataset"></a><span data-ttu-id="bc749-265">Azure Blob 輸出資料集</span><span class="sxs-lookup"><span data-stu-id="bc749-265">Azure Blob output dataset</span></span>
<span data-ttu-id="bc749-266">在輸出資料集定義中，您可以指定 blob 容器和包含輸出資料之資料夾的名稱。</span><span class="sxs-lookup"><span data-stu-id="bc749-266">In the output dataset definition, you specify the names of blob container and folder that holds the output data.</span></span> <span data-ttu-id="bc749-267">請參閱 [Azure Blob 資料集屬性](../data-factory/data-factory-azure-blob-connector.md#dataset-properties)，以取得用來定義 Azure Blob 資料集之 JSON 屬性的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="bc749-267">See [Azure Blob dataset properties](../data-factory/data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used to define an Azure Blob dataset.</span></span>  

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

<span data-ttu-id="bc749-268">FolderPath 會指定包含輸出資料的資料夾路徑︰</span><span class="sxs-lookup"><span data-stu-id="bc749-268">The folderPath specifies the path to the folder that holds the output data:</span></span>

```json
"folderPath": "adfgetstarted/partitioneddata",
```

<span data-ttu-id="bc749-269">[資料集可用性](../data-factory/data-factory-create-datasets.md#dataset-availability) 設定如下︰</span><span class="sxs-lookup"><span data-stu-id="bc749-269">The [dataset availability](../data-factory/data-factory-create-datasets.md#dataset-availability) setting is as follows:</span></span>

```json
"availability": {
    "frequency": "Month",
    "interval": 1,
    "style": "EndOfInterval"
},
```

<span data-ttu-id="bc749-270">在 Azure Data Factory 中，輸出資料集可用性會推動管線。</span><span class="sxs-lookup"><span data-stu-id="bc749-270">In Azure Data Factory, output dataset availability drives the pipeline.</span></span> <span data-ttu-id="bc749-271">在此範例中，每個月會在當月的最後一天產生配量 (EndOfInterval)。</span><span class="sxs-lookup"><span data-stu-id="bc749-271">In this example, the slice is produced monthly on the last day of month (EndOfInterval).</span></span> <span data-ttu-id="bc749-272">如需詳細資訊，請參閱 [Data Factory 排程和執行](../data-factory/data-factory-scheduling-and-execution.md)。</span><span class="sxs-lookup"><span data-stu-id="bc749-272">For more information, see [Data Factory Scheduling and Execution](../data-factory/data-factory-scheduling-and-execution.md).</span></span>

#### <a name="data-pipeline"></a><span data-ttu-id="bc749-273">Data Pipeline</span><span class="sxs-lookup"><span data-stu-id="bc749-273">Data pipeline</span></span>
<span data-ttu-id="bc749-274">您可以定義在隨選 Azure HDInsight 叢集上執行 Hive 指令碼以轉換資料的管線。</span><span class="sxs-lookup"><span data-stu-id="bc749-274">You define a pipeline that transforms data by running Hive script on an on-demand Azure HDInsight cluster.</span></span> <span data-ttu-id="bc749-275">請參閱[管線 JSON](../data-factory/data-factory-create-pipelines.md#pipeline-json)，以取得用來在此範例中定義管線的 JSON 元素之描述。</span><span class="sxs-lookup"><span data-stu-id="bc749-275">See [Pipeline JSON](../data-factory/data-factory-create-pipelines.md#pipeline-json) for descriptions of JSON elements used to define a pipeline in this example.</span></span>

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

<span data-ttu-id="bc749-276">此管線包含一個活動，HDInsightHive 活動。</span><span class="sxs-lookup"><span data-stu-id="bc749-276">The pipeline contains one activity, HDInsightHive activity.</span></span> <span data-ttu-id="bc749-277">由於開始和結束日期都在 2016 年 1 月，因此只處理一個月的資料 (配量)。</span><span class="sxs-lookup"><span data-stu-id="bc749-277">As both start and end dates are in January 2016, data for only one month (a slice) is processed.</span></span> <span data-ttu-id="bc749-278">活動的開始和結束都擁有過去的日期，因此 Data Factory 會立即處理月份的資料。</span><span class="sxs-lookup"><span data-stu-id="bc749-278">Both *start* and *end* of the activity have a past date, so the Data Factory processes data for the month immediately.</span></span> <span data-ttu-id="bc749-279">如果結束為未來日期，則 Data Factory 屆時會建立另一個配量。</span><span class="sxs-lookup"><span data-stu-id="bc749-279">If the end is a future date, the data factory creates another slice when the time comes.</span></span> <span data-ttu-id="bc749-280">如需詳細資訊，請參閱 [Data Factory 排程和執行](../data-factory/data-factory-scheduling-and-execution.md)。</span><span class="sxs-lookup"><span data-stu-id="bc749-280">For more information, see [Data Factory Scheduling and Execution](../data-factory/data-factory-scheduling-and-execution.md).</span></span>

## <a name="clean-up-the-tutorial"></a><span data-ttu-id="bc749-281">清除教學課程</span><span class="sxs-lookup"><span data-stu-id="bc749-281">Clean up the tutorial</span></span>

### <a name="delete-the-blob-containers-created-by-on-demand-hdinsight-cluster"></a><span data-ttu-id="bc749-282">刪除隨選 HDInsight 叢集所建立的 blob 容器</span><span class="sxs-lookup"><span data-stu-id="bc749-282">Delete the blob containers created by on-demand HDInsight cluster</span></span>
<span data-ttu-id="bc749-283">使用 HDInsight 隨選連結服務時，除非有現有的即時叢集 (timeToLive)，否則每當需要處理配量時，就會建立 HDInsight 叢集，並在處理完成時刪除此叢集。</span><span class="sxs-lookup"><span data-stu-id="bc749-283">With on-demand HDInsight linked service, an HDInsight cluster is created every time a slice needs to be processed unless there is an existing live cluster (timeToLive); and the cluster is deleted when the processing is done.</span></span> <span data-ttu-id="bc749-284">對於每個叢集，Azure Data Factory 會在 Azure Blob 儲存體中建立 blob 容器以做為叢集的預設儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="bc749-284">For each cluster, Azure Data Factory creates a blob container in the Azure blob storage used as the default stroage account for the cluster.</span></span> <span data-ttu-id="bc749-285">即使已刪除 HDInsight 叢集，但不會刪除預設 Blob 儲存體容器和相關聯的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="bc749-285">Even though HDInsight cluster is deleted, the default blob storage container and the associated storage account are not deleted.</span></span> <span data-ttu-id="bc749-286">這是設計的行為。</span><span class="sxs-lookup"><span data-stu-id="bc749-286">This behavior is by design.</span></span> <span data-ttu-id="bc749-287">隨著處理的配量越來越多，您會在 Azure Blob 儲存體中看到許多容器。</span><span class="sxs-lookup"><span data-stu-id="bc749-287">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="bc749-288">如果在疑難排解作業時不需要這些容器，建議您加以刪除以降低儲存成本。</span><span class="sxs-lookup"><span data-stu-id="bc749-288">If you do not need them for troubleshooting of the jobs, you may want to delete them to reduce the storage cost.</span></span> <span data-ttu-id="bc749-289">這些容器的名稱會遵循模式︰`adfyourdatafactoryname-linkedservicename-datetimestamp`。</span><span class="sxs-lookup"><span data-stu-id="bc749-289">The names of these containers follow a pattern: `adfyourdatafactoryname-linkedservicename-datetimestamp`.</span></span>

<span data-ttu-id="bc749-290">刪除 **adfjobs** 和 **adfyourdatafactoryname-linkedservicename-datetimestamp** 資料夾。</span><span class="sxs-lookup"><span data-stu-id="bc749-290">Delete the **adfjobs** and **adfyourdatafactoryname-linkedservicename-datetimestamp** folders.</span></span> <span data-ttu-id="bc749-291">Adfjobs 容器包含來自 Azure Data Factory 的作業記錄。</span><span class="sxs-lookup"><span data-stu-id="bc749-291">The adfjobs container contains job logs from Azure Data Factory.</span></span>

### <a name="delete-the-resource-group"></a><span data-ttu-id="bc749-292">刪除資源群組</span><span class="sxs-lookup"><span data-stu-id="bc749-292">Delete the resource group</span></span>
<span data-ttu-id="bc749-293">[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) 用來以群組方式部署、管理及監視您的解決方案。</span><span class="sxs-lookup"><span data-stu-id="bc749-293">[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) is used to deploy, manage, and monitor your solution as a group.</span></span>  <span data-ttu-id="bc749-294">刪除資源群組將會刪除群組內的所有元件。</span><span class="sxs-lookup"><span data-stu-id="bc749-294">Deleting a resource group deletes all the components inside the group.</span></span>  

1. <span data-ttu-id="bc749-295">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="bc749-295">Sign on to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="bc749-296">按一下左側面板上的 [資源群組]  。</span><span class="sxs-lookup"><span data-stu-id="bc749-296">Click **Resource groups** on the left pane.</span></span>
3. <span data-ttu-id="bc749-297">按一下您在 PowerShell 指令碼中建立的資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="bc749-297">Click the resource group name you created in your PowerShell script.</span></span> <span data-ttu-id="bc749-298">如果列出太多的資源群組，請使用篩選器。</span><span class="sxs-lookup"><span data-stu-id="bc749-298">Use the filter if you have too many resource groups listed.</span></span> <span data-ttu-id="bc749-299">會在新的刀鋒視窗中開啟資源群組。</span><span class="sxs-lookup"><span data-stu-id="bc749-299">It opens the resource group in a new blade.</span></span>
4. <span data-ttu-id="bc749-300">除非您與其他專案共用資源群組，否則 [資源]  圖格應列出預設儲存體帳戶和 Data Factory。</span><span class="sxs-lookup"><span data-stu-id="bc749-300">On the **Resources** tile, you shall have the default storage account and the data factory listed unless you share the resource group with other projects.</span></span>
5. <span data-ttu-id="bc749-301">按一下刀鋒視窗頂端的 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="bc749-301">Click **Delete** on the top of the blade.</span></span> <span data-ttu-id="bc749-302">這麼做會刪除儲存體帳戶和此儲存體帳戶中儲存的資料。</span><span class="sxs-lookup"><span data-stu-id="bc749-302">Doing so deletes the storage account and the data stored in the storage account.</span></span>
6. <span data-ttu-id="bc749-303">輸入資源群組名稱以確認刪除，然後按一下 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="bc749-303">Enter the resource group name to confirm deletion, and then click **Delete**.</span></span>

<span data-ttu-id="bc749-304">如果您不想在刪除資源群組時刪除儲存體帳戶，可以考慮以下區隔商務資料與預設儲存體帳戶的架構。</span><span class="sxs-lookup"><span data-stu-id="bc749-304">In case you don't want to delete the storage account when you delete the resource group, consider the following architecture by separating the business data from the default storage account.</span></span> <span data-ttu-id="bc749-305">在此情況下，您會有一個資源群組用於包含商務資料的儲存體帳戶，而另一個資源群組則用於 HDInsight 連結服務的預設儲存體帳戶和 Data Factory。</span><span class="sxs-lookup"><span data-stu-id="bc749-305">In this case, you have one resource group for the storage account with the business data, and the other resource group for the default storage account for HDInsight linked service and the data factory.</span></span> <span data-ttu-id="bc749-306">當您刪除第二個資源群組時，並不會影響商務資料儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="bc749-306">When you delete the second resource group, it does not impact the business data storage account.</span></span> <span data-ttu-id="bc749-307">若要這樣做：</span><span class="sxs-lookup"><span data-stu-id="bc749-307">To do so:</span></span>

* <span data-ttu-id="bc749-308">將下列程式碼以及 Resource Manager 範本中的 Microsoft.DataFactory/datafactories 資源加入最上層資源群組。</span><span class="sxs-lookup"><span data-stu-id="bc749-308">Add the following to the top-level resource group along with the Microsoft.DataFactory/datafactories resource in your Resource Manager template.</span></span> <span data-ttu-id="bc749-309">它會建立儲存體帳戶：</span><span class="sxs-lookup"><span data-stu-id="bc749-309">It creates a storage account:</span></span>

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
* <span data-ttu-id="bc749-310">將新的連結服務點加入至新的儲存體帳戶︰</span><span class="sxs-lookup"><span data-stu-id="bc749-310">Add a new linked service point to the new storage account:</span></span>

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
* <span data-ttu-id="bc749-311">使用其他 dependsOn 和 additionalLinkedServiceNames 設定 HDInsight 隨選連結服務︰</span><span class="sxs-lookup"><span data-stu-id="bc749-311">Configure the HDInsight ondemand linked service with an additional dependsOn and an additionalLinkedServiceNames:</span></span>

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
## <a name="next-steps"></a><span data-ttu-id="bc749-312">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bc749-312">Next steps</span></span>
<span data-ttu-id="bc749-313">在本文中，您已學會如何使用 Azure Data Factory 來建立隨選 HDInsight 叢集來處理 Hive 作業。</span><span class="sxs-lookup"><span data-stu-id="bc749-313">In this article, you have learned how to use Azure Data Factory to create on-demand HDInsight cluster to process Hive jobs.</span></span> <span data-ttu-id="bc749-314">若要閱讀更多資訊︰</span><span class="sxs-lookup"><span data-stu-id="bc749-314">To read more:</span></span>

* [<span data-ttu-id="bc749-315">Hadoop 教學課程：開始在 HDInsight 中使用以 Linux 為基礎的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="bc749-315">Hadoop tutorial: Get started using Linux-based Hadoop in HDInsight</span></span>](hdinsight-hadoop-linux-tutorial-get-started.md)
* [<span data-ttu-id="bc749-316">在 HDInsight 中建立以 Linux 為基礎的 Hadoop 叢集</span><span class="sxs-lookup"><span data-stu-id="bc749-316">Create Linux-based Hadoop clusters in HDInsight</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
* [<span data-ttu-id="bc749-317">HDInsight 文件</span><span class="sxs-lookup"><span data-stu-id="bc749-317">HDInsight documentation</span></span>](https://azure.microsoft.com/documentation/services/hdinsight/)
* [<span data-ttu-id="bc749-318">Data Factory 文件</span><span class="sxs-lookup"><span data-stu-id="bc749-318">Data factory documentation</span></span>](https://azure.microsoft.com/documentation/services/data-factory/)

## <a name="appendix"></a><span data-ttu-id="bc749-319">附錄</span><span class="sxs-lookup"><span data-stu-id="bc749-319">Appendix</span></span>

### <a name="azure-cli-script"></a><span data-ttu-id="bc749-320">Azure CLI 指令碼</span><span class="sxs-lookup"><span data-stu-id="bc749-320">Azure CLI script</span></span>
<span data-ttu-id="bc749-321">您可以使用 Azure CLI ，而不是使用 Azure PowerShell 來執行教學課程。</span><span class="sxs-lookup"><span data-stu-id="bc749-321">You can use Azure CLI instead of using Azure PowerShell to do the tutorial.</span></span> <span data-ttu-id="bc749-322">若要使用 Azure CLI，先依照下列指示安裝 Azure CLI：</span><span class="sxs-lookup"><span data-stu-id="bc749-322">To use Azure CLI, first install Azure CLI as per the following instructions:</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

#### <a name="use-azure-cli-to-prepare-the-storage-and-copy-the-files"></a><span data-ttu-id="bc749-323">使用 Azure CLI 準備儲存體並複製檔案</span><span class="sxs-lookup"><span data-stu-id="bc749-323">Use Azure CLI to prepare the storage and copy the files</span></span>

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

<span data-ttu-id="bc749-324">容器名稱為 *adfgetstarted*。</span><span class="sxs-lookup"><span data-stu-id="bc749-324">The container name is *adfgetstarted*.</span></span> <span data-ttu-id="bc749-325">讓它保持原狀。</span><span class="sxs-lookup"><span data-stu-id="bc749-325">Keep it as it is.</span></span> <span data-ttu-id="bc749-326">否則，您必須更新 Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="bc749-326">Otherwise you need to update the Resource Manager template.</span></span> <span data-ttu-id="bc749-327">如需有關此 CLI 指定碼的說明，請參閱 [使用 Azure CLI 搭配 Azure 儲存體](../storage/common/storage-azure-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="bc749-327">If you need help with this CLI script, see [Using the Azure CLI with Azure Storage](../storage/common/storage-azure-cli.md).</span></span>
