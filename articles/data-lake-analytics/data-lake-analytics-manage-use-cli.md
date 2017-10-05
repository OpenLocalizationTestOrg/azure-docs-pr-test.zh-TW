---
title: "使用 Azure 命令列介面管理 Azure Data Lake Analytics | Microsoft Docs"
description: "了解如何使用 Azure CLI 管理 Data Lake Analytics 帳戶、資料來源、工作和使用者"
services: data-lake-analytics
documentationcenter: 
author: edmacauley
manager: jhubbard
editor: cgronlun
ms.assetid: 4e5a3a0a-6d7f-43ed-aeb5-c3b3979a1e0a
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: f90bada3572c0ed40b07d76ec02c1b499bbd1428
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="manage-azure-data-lake-analytics-using-azure-command-line-interface-cli"></a><span data-ttu-id="8ca5d-103">使用 Azure 命令列介面 (CLI) 管理 Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="8ca5d-103">Manage Azure Data Lake Analytics using Azure Command-line Interface (CLI)</span></span>
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

<span data-ttu-id="8ca5d-104">了解如何使用 Azure CLI 管理 Azure Data Lake Analytics 帳戶、資料來源、使用者和工作。</span><span class="sxs-lookup"><span data-stu-id="8ca5d-104">Learn how to manage Azure Data Lake Analytics accounts, data sources, users, and jobs using the Azure CLI.</span></span> <span data-ttu-id="8ca5d-105">若要使用其他工具查看管理主題，請按一下上方的索引標籤選取器。</span><span class="sxs-lookup"><span data-stu-id="8ca5d-105">To see management topics using other tools, click the tab select above.</span></span>


<span data-ttu-id="8ca5d-106">**必要條件**</span><span class="sxs-lookup"><span data-stu-id="8ca5d-106">**Prerequisites**</span></span>

<span data-ttu-id="8ca5d-107">開始進行本教學課程之前，您必須具備下列條件：</span><span class="sxs-lookup"><span data-stu-id="8ca5d-107">Before you begin this tutorial, you must have the following:</span></span>

* <span data-ttu-id="8ca5d-108">**Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="8ca5d-108">**An Azure subscription**.</span></span> <span data-ttu-id="8ca5d-109">請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="8ca5d-109">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="8ca5d-110">**Azure CLI**。</span><span class="sxs-lookup"><span data-stu-id="8ca5d-110">**Azure CLI**.</span></span> <span data-ttu-id="8ca5d-111">請參閱 [安裝和設定 Azure CLI](../cli-install-nodejs.md)。</span><span class="sxs-lookup"><span data-stu-id="8ca5d-111">See [Install and configure Azure CLI](../cli-install-nodejs.md).</span></span>
  * <span data-ttu-id="8ca5d-112">下載並安裝 **Azure CLI 工具** [發行前版本](https://github.com/MicrosoftBigData/AzureDataLake/releases) ，才能完成這個示範。</span><span class="sxs-lookup"><span data-stu-id="8ca5d-112">Download and install the **pre-release** [Azure CLI tools](https://github.com/MicrosoftBigData/AzureDataLake/releases) in order to complete this demo.</span></span>
* <span data-ttu-id="8ca5d-113">使用下列命令進行**驗證**：</span><span class="sxs-lookup"><span data-stu-id="8ca5d-113">**Authentication**, using the following command:</span></span>
  
        azure login
    <span data-ttu-id="8ca5d-114">如需使用公司或學校帳戶驗證的詳細資訊，請參閱 [從 Azure CLI 連線至 Azure 訂用帳戶](../xplat-cli-connect.md)。</span><span class="sxs-lookup"><span data-stu-id="8ca5d-114">For more information on authenticating using a work or school account, see [Connect to an Azure subscription from the Azure CLI](../xplat-cli-connect.md).</span></span>
* <span data-ttu-id="8ca5d-115">使用下列命令，**切換至 Azure 資源管理員模式**：</span><span class="sxs-lookup"><span data-stu-id="8ca5d-115">**Switch to the Azure Resource Manager mode**, using the following command:</span></span>
  
        azure config mode arm

<span data-ttu-id="8ca5d-116">**若要列出 Data Lake Store 和 Data Lake Analytics 命令：**</span><span class="sxs-lookup"><span data-stu-id="8ca5d-116">**To list the Data Lake Store and Data Lake Analytics commands:**</span></span>

    azure datalake store
    azure datalake analytics

<!-- ################################ -->
<!-- ################################ -->
## <a name="manage-accounts"></a><span data-ttu-id="8ca5d-117">管理帳戶</span><span class="sxs-lookup"><span data-stu-id="8ca5d-117">Manage accounts</span></span>
<span data-ttu-id="8ca5d-118">您必須擁有 Data Lake Analytics 帳戶，才能執行任何 Data Lake Analytics 工作。</span><span class="sxs-lookup"><span data-stu-id="8ca5d-118">Before running any Data Lake Analytics jobs, you must have a Data Lake Analytics account.</span></span> <span data-ttu-id="8ca5d-119">與 Azure HDInsight 不同的是，分析帳戶未執行工作時，您無需支付該帳戶的費用。</span><span class="sxs-lookup"><span data-stu-id="8ca5d-119">Unlike Azure HDInsight, you don't pay for an Analytics account when it is not running a job.</span></span>  <span data-ttu-id="8ca5d-120">您只需支付執行工作時的費用。</span><span class="sxs-lookup"><span data-stu-id="8ca5d-120">You only pay for the time when it is running a job.</span></span>  <span data-ttu-id="8ca5d-121">如需詳細資訊，請參閱 [Azure Data Lake Analytics 概觀](data-lake-analytics-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="8ca5d-121">For more information, see [Azure Data Lake Analytics Overview](data-lake-analytics-overview.md).</span></span>  

### <a name="create-accounts"></a><span data-ttu-id="8ca5d-122">建立帳戶</span><span class="sxs-lookup"><span data-stu-id="8ca5d-122">Create accounts</span></span>
      azure datalake analytics account create "<Data Lake Analytics Account Name>" "<Azure Location>" "<Resource Group Name>" "<Default Data Lake Account Name>"


### <a name="update-accounts"></a><span data-ttu-id="8ca5d-123">更新帳戶</span><span class="sxs-lookup"><span data-stu-id="8ca5d-123">Update accounts</span></span>
<span data-ttu-id="8ca5d-124">下列命令會更新現有 Data Lake Analytics 帳戶的屬性</span><span class="sxs-lookup"><span data-stu-id="8ca5d-124">The following command updates the properties of an existing Data Lake Analytics Account</span></span>

    azure datalake analytics account set "<Data Lake Analytics Account Name>"


### <a name="list-accounts"></a><span data-ttu-id="8ca5d-125">列出帳戶</span><span class="sxs-lookup"><span data-stu-id="8ca5d-125">List accounts</span></span>
<span data-ttu-id="8ca5d-126">列出 Data Lake Analytics 帳戶</span><span class="sxs-lookup"><span data-stu-id="8ca5d-126">List Data Lake Analytics accounts</span></span> 

    azure datalake analytics account list

<span data-ttu-id="8ca5d-127">列出特定資源群組內的 Data Lake Analytics 帳戶</span><span class="sxs-lookup"><span data-stu-id="8ca5d-127">List Data Lake Analytics accounts within a specific resource group</span></span>

    azure datalake analytics account list -g "<Azure Resource Group Name>"

<span data-ttu-id="8ca5d-128">取得特定 Data Lake Analytics 帳戶的詳細資料</span><span class="sxs-lookup"><span data-stu-id="8ca5d-128">Get details of a specific Data Lake Analytics account</span></span>

    azure datalake analytics account show -g "<Azure Resource Group Name>" -n "<Data Lake Analytics Account Name>"

### <a name="delete-data-lake-analytics-accounts"></a><span data-ttu-id="8ca5d-129">刪除 Data Lake Analytics 帳戶</span><span class="sxs-lookup"><span data-stu-id="8ca5d-129">Delete Data Lake Analytics accounts</span></span>
      azure datalake analytics account delete "<Data Lake Analytics Account Name>"


<!-- ################################ -->
<!-- ################################ -->
## <a name="manage-account-data-sources"></a><span data-ttu-id="8ca5d-130">管理帳戶資料來源</span><span class="sxs-lookup"><span data-stu-id="8ca5d-130">Manage account data sources</span></span>
<span data-ttu-id="8ca5d-131">Data Lake Analytics 目前支援下列資料來源：</span><span class="sxs-lookup"><span data-stu-id="8ca5d-131">Data Lake Analytics currently supports the following data sources:</span></span>

* [<span data-ttu-id="8ca5d-132">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="8ca5d-132">Azure Data Lake Store</span></span>](../data-lake-store/data-lake-store-overview.md)
* [<span data-ttu-id="8ca5d-133">Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="8ca5d-133">Azure Storage</span></span>](../storage/common/storage-introduction.md)

<span data-ttu-id="8ca5d-134">當您建立分析帳戶時，必須指定 Azure Data Lake 儲存體帳戶作為預設的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="8ca5d-134">When you create an Analytics account, you must designate an Azure Data Lake Storage account to be the default storage account.</span></span> <span data-ttu-id="8ca5d-135">預設的 ADL 儲存體帳戶是用來儲存工作中繼資料與工作稽核記錄。</span><span class="sxs-lookup"><span data-stu-id="8ca5d-135">The default ADL storage account is used to store job metadata and job audit logs.</span></span> <span data-ttu-id="8ca5d-136">建立分析帳戶後，就可以新增其他 Azure Data Lake 儲存體帳戶和/或 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="8ca5d-136">After you have created an Analytics account, you can add additional Data Lake Storage accounts and/or Azure Storage account.</span></span> 

### <a name="find-the-default-adl-storage-account"></a><span data-ttu-id="8ca5d-137">尋找預設的 ADL 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="8ca5d-137">Find the default ADL storage account</span></span>
    azure datalake analytics account show "<Data Lake Analytics Account Name>"

<span data-ttu-id="8ca5d-138">值會列在 properties:datalakeStoreAccount:name 下方。</span><span class="sxs-lookup"><span data-stu-id="8ca5d-138">The value is listed under properties:datalakeStoreAccount:name.</span></span>

### <a name="add-additional-azure-blob-storage-accounts"></a><span data-ttu-id="8ca5d-139">新增其他的 Azure Blob 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="8ca5d-139">Add additional Azure Blob storage accounts</span></span>
      azure datalake analytics account datasource add -n "<Data Lake Analytics Account Name>" -b "<Azure Blob Storage Account Short Name>" -k "<Azure Storage Account Key>"

> [!NOTE]
> <span data-ttu-id="8ca5d-140">僅支援 Blob 儲存體簡短名稱。</span><span class="sxs-lookup"><span data-stu-id="8ca5d-140">Only Blob storage short names are supported.</span></span>  <span data-ttu-id="8ca5d-141">請勿使用 FQDN，例如 "myblob.blob.core.windows.net"。</span><span class="sxs-lookup"><span data-stu-id="8ca5d-141">Don't use FQDN, for example "myblob.blob.core.windows.net".</span></span>
> 
> 

### <a name="add-additional-data-lake-store-accounts"></a><span data-ttu-id="8ca5d-142">新增其他的 Data Lake Store 帳戶</span><span class="sxs-lookup"><span data-stu-id="8ca5d-142">Add additional Data Lake Store accounts</span></span>
      azure datalake analytics account datasource add -n "<Data Lake Analytics Account Name>" -l "<Data Lake Store Account Name>" [-d]

<span data-ttu-id="8ca5d-143">[-d] 是選用參數，指出所新增的 Data Lake 是預設的 Data Lake 帳戶。</span><span class="sxs-lookup"><span data-stu-id="8ca5d-143">[-d] is an optional switch to indicate whether the Data Lake being added is the default Data Lake account.</span></span> 

### <a name="update-existing-data-source"></a><span data-ttu-id="8ca5d-144">更新現有的資料來源</span><span class="sxs-lookup"><span data-stu-id="8ca5d-144">Update existing data source</span></span>
<span data-ttu-id="8ca5d-145">若要將現有的 Data Lake Store 帳戶設為預設值：</span><span class="sxs-lookup"><span data-stu-id="8ca5d-145">To set an existing Data Lake Store account to be the default:</span></span>

      azure datalake analytics account datasource set -n "<Data Lake Analytics Account Name>" -l "<Azure Data Lake Store Account Name>" -d

<span data-ttu-id="8ca5d-146">若要更新現有的 Blob 儲存體帳戶金鑰：</span><span class="sxs-lookup"><span data-stu-id="8ca5d-146">To update an existing Blob storage account key:</span></span>

      azure datalake analytics account datasource set -n "<Data Lake Analytics Account Name>" -b "<Blob Storage Account Name>" -k "<New Blob Storage Account Key>"

### <a name="list-data-sources"></a><span data-ttu-id="8ca5d-147">列出資料來源：</span><span class="sxs-lookup"><span data-stu-id="8ca5d-147">List data sources:</span></span>
    azure datalake analytics account show "<Data Lake Analytics Account Name>"

![Data Lake Analytics 會列出資料來源](./media/data-lake-analytics-manage-use-cli/data-lake-analytics-list-data-source.png)

### <a name="delete-data-sources"></a><span data-ttu-id="8ca5d-149">刪除資料來源：</span><span class="sxs-lookup"><span data-stu-id="8ca5d-149">Delete data sources:</span></span>
<span data-ttu-id="8ca5d-150">刪除 Data Lake Store 帳戶：</span><span class="sxs-lookup"><span data-stu-id="8ca5d-150">To delete a Data Lake Store account:</span></span>

      azure datalake analytics account datasource delete "<Data Lake Analytics Account Name>" "<Azure Data Lake Store Account Name>"

<span data-ttu-id="8ca5d-151">刪除 Blob 儲存體帳戶：</span><span class="sxs-lookup"><span data-stu-id="8ca5d-151">To delete a Blob storage account:</span></span>

      azure datalake analytics account datasource delete "<Data Lake Analytics Account Name>" "<Blob Storage Account Name>"

## <a name="manage-jobs"></a><span data-ttu-id="8ca5d-152">管理工作</span><span class="sxs-lookup"><span data-stu-id="8ca5d-152">Manage jobs</span></span>
<span data-ttu-id="8ca5d-153">您必須擁有 Data Lake Analytics 帳戶，才能建立工作。</span><span class="sxs-lookup"><span data-stu-id="8ca5d-153">You must have a Data Lake Analytics account before you can create a job.</span></span>  <span data-ttu-id="8ca5d-154">如需詳細資訊，請參閱 [管理 Data Lake Analytics 帳戶](#manage-accounts)。</span><span class="sxs-lookup"><span data-stu-id="8ca5d-154">For more information, see [Manage Data Lake Analytics accounts](#manage-accounts).</span></span>

### <a name="list-jobs"></a><span data-ttu-id="8ca5d-155">列出工作</span><span class="sxs-lookup"><span data-stu-id="8ca5d-155">List jobs</span></span>
      azure datalake analytics job list -n "<Data Lake Analytics Account Name>"

![Data Lake Analytics 會列出資料來源](./media/data-lake-analytics-manage-use-cli/data-lake-analytics-list-jobs.png)

### <a name="get-job-details"></a><span data-ttu-id="8ca5d-157">取得工作詳細資料</span><span class="sxs-lookup"><span data-stu-id="8ca5d-157">Get job details</span></span>
      azure datalake analytics job show -n "<Data Lake Analytics Account Name>" -j "<Job ID>"

### <a name="submit-jobs"></a><span data-ttu-id="8ca5d-158">提交工作</span><span class="sxs-lookup"><span data-stu-id="8ca5d-158">Submit jobs</span></span>
> [!NOTE]
> <span data-ttu-id="8ca5d-159">工作的預設優先順序為 1000，工作的平行處理原則預設程度是 1。</span><span class="sxs-lookup"><span data-stu-id="8ca5d-159">The default priority of a job is 1000, and the default degree of parallelism for a job is 1.</span></span>
> 
> 

    azure datalake analytics job create  "<Data Lake Analytics Account Name>" "<Job Name>" "<Script>"

### <a name="cancel-jobs"></a><span data-ttu-id="8ca5d-160">取消工作</span><span class="sxs-lookup"><span data-stu-id="8ca5d-160">Cancel jobs</span></span>
<span data-ttu-id="8ca5d-161">使用 list 命令來尋找工作識別碼，然後使用 cancel 來取消工作。</span><span class="sxs-lookup"><span data-stu-id="8ca5d-161">Use the list command to find the job id, and then use cancel to cancel the job.</span></span>

      azure datalake analytics job list -n "<Data Lake Analytics Account Name>"
      azure datalake analytics job cancel "<Data Lake Analytics Account Name>" "<Job ID>"

## <a name="manage-catalog"></a><span data-ttu-id="8ca5d-162">管理目錄</span><span class="sxs-lookup"><span data-stu-id="8ca5d-162">Manage catalog</span></span>
<span data-ttu-id="8ca5d-163">U-SQL 目錄是用來建構資料和程式碼，讓 U-SQL 指令碼可以共用它們。</span><span class="sxs-lookup"><span data-stu-id="8ca5d-163">The U-SQL catalog is used to structure data and code so they can be shared by U-SQL scripts.</span></span> <span data-ttu-id="8ca5d-164">目錄可以讓 Azure Data Lake 中的資料具有可能的最高效能。</span><span class="sxs-lookup"><span data-stu-id="8ca5d-164">The catalog enables the highest performance possible with data in Azure Data Lake.</span></span> <span data-ttu-id="8ca5d-165">如需詳細資訊，請參閱 [使用 U-SQL 目錄](data-lake-analytics-use-u-sql-catalog.md)。</span><span class="sxs-lookup"><span data-stu-id="8ca5d-165">For more information, see [Use U-SQL catalog](data-lake-analytics-use-u-sql-catalog.md).</span></span>

### <a name="list-catalog-items"></a><span data-ttu-id="8ca5d-166">列出目錄項目</span><span class="sxs-lookup"><span data-stu-id="8ca5d-166">List catalog items</span></span>
    #List databases
    azure datalake analytics catalog list -n "<Data Lake Analytics Account Name>" -t database

    #List tables
    azure datalake analytics catalog list -n "<Data Lake Analytics Account Name>" -t table

<span data-ttu-id="8ca5d-167">類型包括資料庫、結構描述、組件、外部資料來源、資料表、資料表值函數或資料表統計資料。</span><span class="sxs-lookup"><span data-stu-id="8ca5d-167">The types include database, schema, assembly, external data source, table, table valued function or table statistics.</span></span>

<!-- ################################ -->
<!-- ################################ -->
## <a name="use-arm-groups"></a><span data-ttu-id="8ca5d-168">使用 ARM 群組</span><span class="sxs-lookup"><span data-stu-id="8ca5d-168">Use ARM groups</span></span>
<span data-ttu-id="8ca5d-169">應用程式通常由許多元件組成，例如，Web 應用程式、資料庫、資料庫伺服器、儲存體和協力廠商服務。</span><span class="sxs-lookup"><span data-stu-id="8ca5d-169">Applications are typically made up of many components, for example a web app, database, database server, storage, and 3rd party services.</span></span> <span data-ttu-id="8ca5d-170">Azure 資源管理員 (ARM) 可讓您將應用程式中的資源做為群組使用，稱為 Azure 資源群組。</span><span class="sxs-lookup"><span data-stu-id="8ca5d-170">Azure Resource Manager (ARM) enables you to work with the resources in your application as a group, referred to as an Azure Resource Group.</span></span> <span data-ttu-id="8ca5d-171">您可以透過單一、協調的作業來部署、更新、監視或刪除應用程式的所有資源。</span><span class="sxs-lookup"><span data-stu-id="8ca5d-171">You can deploy, update, monitor or delete all of the resources for your application in a single, coordinated operation.</span></span> <span data-ttu-id="8ca5d-172">您會使用部署的範本，且該範本可以用於不同的環境，例如測試、預備和生產環境。</span><span class="sxs-lookup"><span data-stu-id="8ca5d-172">You use a template for deployment and that template can work for different environments such as testing, staging and production.</span></span> <span data-ttu-id="8ca5d-173">您可以檢視整個群組的彙總成本，為您的組織釐清計費。</span><span class="sxs-lookup"><span data-stu-id="8ca5d-173">You can clarify billing for your organization by viewing the rolled-up costs for the entire group.</span></span> <span data-ttu-id="8ca5d-174">如需詳細資訊，請參閱 [Azure 資源管理員概觀](../azure-resource-manager/resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="8ca5d-174">For more information, see [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md).</span></span> 

<span data-ttu-id="8ca5d-175">Data Lake Analytics 服務可包含下列元件：</span><span class="sxs-lookup"><span data-stu-id="8ca5d-175">A Data Lake Analytics service can include the following components:</span></span>

* <span data-ttu-id="8ca5d-176">Azure Data Lake Analytics 帳戶</span><span class="sxs-lookup"><span data-stu-id="8ca5d-176">Azure Data Lake Analytics account</span></span>
* <span data-ttu-id="8ca5d-177">必要的預設 Azure Data Lake 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="8ca5d-177">Required default Azure Data Lake Storage account</span></span>
* <span data-ttu-id="8ca5d-178">其他 Azure Data Lake 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="8ca5d-178">Additional Azure Data Lake Storage accounts</span></span>
* <span data-ttu-id="8ca5d-179">其他 Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="8ca5d-179">Additional Azure Storage accounts</span></span>

<span data-ttu-id="8ca5d-180">您可以在某個 ARM 群組下建立上述所有元件，這樣更容易管理。</span><span class="sxs-lookup"><span data-stu-id="8ca5d-180">You can create all these components under one ARM group to make them easier to manage.</span></span>

![Azure Data Lake Analytics 帳戶與儲存體](./media/data-lake-analytics-manage-use-portal/data-lake-analytics-arm-structure.png)

<span data-ttu-id="8ca5d-182">Data Lake Analytics 帳戶和相依的儲存體帳戶必須位於相同的 Azure 資料中心。</span><span class="sxs-lookup"><span data-stu-id="8ca5d-182">A Data Lake Analytics account and the dependent storage accounts must be placed in the same Azure data center.</span></span>
<span data-ttu-id="8ca5d-183">但 ARM 群組可位在不同的資料中心內。</span><span class="sxs-lookup"><span data-stu-id="8ca5d-183">The ARM group however can be located in a different data center.</span></span>  

## <a name="see-also"></a><span data-ttu-id="8ca5d-184">另請參閱</span><span class="sxs-lookup"><span data-stu-id="8ca5d-184">See also</span></span>
* [<span data-ttu-id="8ca5d-185">Microsoft Azure Data Lake Analytics 概觀</span><span class="sxs-lookup"><span data-stu-id="8ca5d-185">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="8ca5d-186">使用 Azure 入口網站開始使用 Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="8ca5d-186">Get started with Data Lake Analytics using Azure Portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="8ca5d-187">使用 Azure 入口網站管理 Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="8ca5d-187">Manage Azure Data Lake Analytics using Azure Portal</span></span>](data-lake-analytics-manage-use-portal.md)
* [<span data-ttu-id="8ca5d-188">使用 Azure 入口網站監視和疑難排解 Azure Data Lake Analytics 工作</span><span class="sxs-lookup"><span data-stu-id="8ca5d-188">Monitor and troubleshoot Azure Data Lake Analytics jobs using Azure Portal</span></span>](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)

