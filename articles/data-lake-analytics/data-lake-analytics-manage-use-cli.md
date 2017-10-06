---
title: "使用 Azure 命令列介面的 Azure Data Lake Analytics aaaManage |Microsoft 文件"
description: "了解如何 toomanage Data Lake Analytics 帳戶，資料來源、 工作和使用者使用 Azure CLI"
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
ms.openlocfilehash: 0af1f89080739b39f6980989b7694734cc135715
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-data-lake-analytics-using-azure-command-line-interface-cli"></a><span data-ttu-id="47e48-103">使用 Azure 命令列介面 (CLI) 管理 Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="47e48-103">Manage Azure Data Lake Analytics using Azure Command-line Interface (CLI)</span></span>
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

<span data-ttu-id="47e48-104">了解 toomanage Azure Data Lake Analytics 帳戶、 資料來源、 使用者和工作使用 hello Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="47e48-104">Learn how toomanage Azure Data Lake Analytics accounts, data sources, users, and jobs using hello Azure CLI.</span></span> <span data-ttu-id="47e48-105">toosee 管理主題使用其他工具中，按一下 [hello] 索引標籤選取上述。</span><span class="sxs-lookup"><span data-stu-id="47e48-105">toosee management topics using other tools, click hello tab select above.</span></span>


<span data-ttu-id="47e48-106">**必要條件**</span><span class="sxs-lookup"><span data-stu-id="47e48-106">**Prerequisites**</span></span>

<span data-ttu-id="47e48-107">開始本教學課程之前，您必須擁有 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="47e48-107">Before you begin this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="47e48-108">**Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="47e48-108">**An Azure subscription**.</span></span> <span data-ttu-id="47e48-109">請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="47e48-109">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="47e48-110">**Azure CLI**。</span><span class="sxs-lookup"><span data-stu-id="47e48-110">**Azure CLI**.</span></span> <span data-ttu-id="47e48-111">請參閱 [安裝和設定 Azure CLI](../cli-install-nodejs.md)。</span><span class="sxs-lookup"><span data-stu-id="47e48-111">See [Install and configure Azure CLI](../cli-install-nodejs.md).</span></span>
  * <span data-ttu-id="47e48-112">下載並安裝 hello**發行前版本** [Azure CLI 工具](https://github.com/MicrosoftBigData/AzureDataLake/releases)中排序 toocomplete 此示範。</span><span class="sxs-lookup"><span data-stu-id="47e48-112">Download and install hello **pre-release** [Azure CLI tools](https://github.com/MicrosoftBigData/AzureDataLake/releases) in order toocomplete this demo.</span></span>
* <span data-ttu-id="47e48-113">**驗證**，並使用下列命令 hello:</span><span class="sxs-lookup"><span data-stu-id="47e48-113">**Authentication**, using hello following command:</span></span>
  
        azure login
    <span data-ttu-id="47e48-114">如需有關如何使用工作或學校帳戶驗證的詳細資訊，請參閱[tooan Azure 訂用帳戶連線從 hello Azure CLI](../xplat-cli-connect.md)。</span><span class="sxs-lookup"><span data-stu-id="47e48-114">For more information on authenticating using a work or school account, see [Connect tooan Azure subscription from hello Azure CLI](../xplat-cli-connect.md).</span></span>
* <span data-ttu-id="47e48-115">**交換器 toohello Azure Resource Manager 模式**，並使用下列命令 hello:</span><span class="sxs-lookup"><span data-stu-id="47e48-115">**Switch toohello Azure Resource Manager mode**, using hello following command:</span></span>
  
        azure config mode arm

<span data-ttu-id="47e48-116">**toolist hello 資料湖存放區和 Data Lake Analytics 命令：**</span><span class="sxs-lookup"><span data-stu-id="47e48-116">**toolist hello Data Lake Store and Data Lake Analytics commands:**</span></span>

    azure datalake store
    azure datalake analytics

<!-- ################################ -->
<!-- ################################ -->
## <a name="manage-accounts"></a><span data-ttu-id="47e48-117">管理帳戶</span><span class="sxs-lookup"><span data-stu-id="47e48-117">Manage accounts</span></span>
<span data-ttu-id="47e48-118">您必須擁有 Data Lake Analytics 帳戶，才能執行任何 Data Lake Analytics 工作。</span><span class="sxs-lookup"><span data-stu-id="47e48-118">Before running any Data Lake Analytics jobs, you must have a Data Lake Analytics account.</span></span> <span data-ttu-id="47e48-119">與 Azure HDInsight 不同的是，分析帳戶未執行工作時，您無需支付該帳戶的費用。</span><span class="sxs-lookup"><span data-stu-id="47e48-119">Unlike Azure HDInsight, you don't pay for an Analytics account when it is not running a job.</span></span>  <span data-ttu-id="47e48-120">您只需支付 hello 時間執行作業時。</span><span class="sxs-lookup"><span data-stu-id="47e48-120">You only pay for hello time when it is running a job.</span></span>  <span data-ttu-id="47e48-121">如需詳細資訊，請參閱 [Azure Data Lake Analytics 概觀](data-lake-analytics-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="47e48-121">For more information, see [Azure Data Lake Analytics Overview](data-lake-analytics-overview.md).</span></span>  

### <a name="create-accounts"></a><span data-ttu-id="47e48-122">建立帳戶</span><span class="sxs-lookup"><span data-stu-id="47e48-122">Create accounts</span></span>
      azure datalake analytics account create "<Data Lake Analytics Account Name>" "<Azure Location>" "<Resource Group Name>" "<Default Data Lake Account Name>"


### <a name="update-accounts"></a><span data-ttu-id="47e48-123">更新帳戶</span><span class="sxs-lookup"><span data-stu-id="47e48-123">Update accounts</span></span>
<span data-ttu-id="47e48-124">hello 下列命令會更新現有的資料湖分析帳戶 hello 屬性</span><span class="sxs-lookup"><span data-stu-id="47e48-124">hello following command updates hello properties of an existing Data Lake Analytics Account</span></span>

    azure datalake analytics account set "<Data Lake Analytics Account Name>"


### <a name="list-accounts"></a><span data-ttu-id="47e48-125">列出帳戶</span><span class="sxs-lookup"><span data-stu-id="47e48-125">List accounts</span></span>
<span data-ttu-id="47e48-126">列出 Data Lake Analytics 帳戶</span><span class="sxs-lookup"><span data-stu-id="47e48-126">List Data Lake Analytics accounts</span></span> 

    azure datalake analytics account list

<span data-ttu-id="47e48-127">列出特定資源群組內的 Data Lake Analytics 帳戶</span><span class="sxs-lookup"><span data-stu-id="47e48-127">List Data Lake Analytics accounts within a specific resource group</span></span>

    azure datalake analytics account list -g "<Azure Resource Group Name>"

<span data-ttu-id="47e48-128">取得特定 Data Lake Analytics 帳戶的詳細資料</span><span class="sxs-lookup"><span data-stu-id="47e48-128">Get details of a specific Data Lake Analytics account</span></span>

    azure datalake analytics account show -g "<Azure Resource Group Name>" -n "<Data Lake Analytics Account Name>"

### <a name="delete-data-lake-analytics-accounts"></a><span data-ttu-id="47e48-129">刪除 Data Lake Analytics 帳戶</span><span class="sxs-lookup"><span data-stu-id="47e48-129">Delete Data Lake Analytics accounts</span></span>
      azure datalake analytics account delete "<Data Lake Analytics Account Name>"


<!-- ################################ -->
<!-- ################################ -->
## <a name="manage-account-data-sources"></a><span data-ttu-id="47e48-130">管理帳戶資料來源</span><span class="sxs-lookup"><span data-stu-id="47e48-130">Manage account data sources</span></span>
<span data-ttu-id="47e48-131">Data Lake Analytics 目前支援下列資料來源的 hello:</span><span class="sxs-lookup"><span data-stu-id="47e48-131">Data Lake Analytics currently supports hello following data sources:</span></span>

* [<span data-ttu-id="47e48-132">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="47e48-132">Azure Data Lake Store</span></span>](../data-lake-store/data-lake-store-overview.md)
* [<span data-ttu-id="47e48-133">Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="47e48-133">Azure Storage</span></span>](../storage/common/storage-introduction.md)

<span data-ttu-id="47e48-134">當您建立 Analytics 帳戶時，您必須指定的 Azure 資料湖存放區帳戶 toobe hello 預設儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="47e48-134">When you create an Analytics account, you must designate an Azure Data Lake Storage account toobe hello default storage account.</span></span> <span data-ttu-id="47e48-135">hello ADL 存放裝置會使用預設帳戶 toostore 工作中繼資料和作業的稽核記錄檔。</span><span class="sxs-lookup"><span data-stu-id="47e48-135">hello default ADL storage account is used toostore job metadata and job audit logs.</span></span> <span data-ttu-id="47e48-136">建立分析帳戶後，就可以新增其他 Azure Data Lake 儲存體帳戶和/或 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="47e48-136">After you have created an Analytics account, you can add additional Data Lake Storage accounts and/or Azure Storage account.</span></span> 

### <a name="find-hello-default-adl-storage-account"></a><span data-ttu-id="47e48-137">找不到 hello 預設 ADL 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="47e48-137">Find hello default ADL storage account</span></span>
    azure datalake analytics account show "<Data Lake Analytics Account Name>"

<span data-ttu-id="47e48-138">hello 值都會列在屬性： datalakeStoreAccount:name。</span><span class="sxs-lookup"><span data-stu-id="47e48-138">hello value is listed under properties:datalakeStoreAccount:name.</span></span>

### <a name="add-additional-azure-blob-storage-accounts"></a><span data-ttu-id="47e48-139">新增其他的 Azure Blob 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="47e48-139">Add additional Azure Blob storage accounts</span></span>
      azure datalake analytics account datasource add -n "<Data Lake Analytics Account Name>" -b "<Azure Blob Storage Account Short Name>" -k "<Azure Storage Account Key>"

> [!NOTE]
> <span data-ttu-id="47e48-140">僅支援 Blob 儲存體簡短名稱。</span><span class="sxs-lookup"><span data-stu-id="47e48-140">Only Blob storage short names are supported.</span></span>  <span data-ttu-id="47e48-141">請勿使用 FQDN，例如 "myblob.blob.core.windows.net"。</span><span class="sxs-lookup"><span data-stu-id="47e48-141">Don't use FQDN, for example "myblob.blob.core.windows.net".</span></span>
> 
> 

### <a name="add-additional-data-lake-store-accounts"></a><span data-ttu-id="47e48-142">新增其他的 Data Lake Store 帳戶</span><span class="sxs-lookup"><span data-stu-id="47e48-142">Add additional Data Lake Store accounts</span></span>
      azure datalake analytics account datasource add -n "<Data Lake Analytics Account Name>" -l "<Data Lake Store Account Name>" [-d]

<span data-ttu-id="47e48-143">[-d] 是選擇性參數 tooindicate hello 所加入的資料湖是否 hello 預設資料湖帳戶。</span><span class="sxs-lookup"><span data-stu-id="47e48-143">[-d] is an optional switch tooindicate whether hello Data Lake being added is hello default Data Lake account.</span></span> 

### <a name="update-existing-data-source"></a><span data-ttu-id="47e48-144">更新現有的資料來源</span><span class="sxs-lookup"><span data-stu-id="47e48-144">Update existing data source</span></span>
<span data-ttu-id="47e48-145">tooset 現有 Data Lake Store 帳戶 toobe hello 預設值：</span><span class="sxs-lookup"><span data-stu-id="47e48-145">tooset an existing Data Lake Store account toobe hello default:</span></span>

      azure datalake analytics account datasource set -n "<Data Lake Analytics Account Name>" -l "<Azure Data Lake Store Account Name>" -d

<span data-ttu-id="47e48-146">tooupdate 現有的 Blob 儲存體帳戶金鑰：</span><span class="sxs-lookup"><span data-stu-id="47e48-146">tooupdate an existing Blob storage account key:</span></span>

      azure datalake analytics account datasource set -n "<Data Lake Analytics Account Name>" -b "<Blob Storage Account Name>" -k "<New Blob Storage Account Key>"

### <a name="list-data-sources"></a><span data-ttu-id="47e48-147">列出資料來源：</span><span class="sxs-lookup"><span data-stu-id="47e48-147">List data sources:</span></span>
    azure datalake analytics account show "<Data Lake Analytics Account Name>"

![Data Lake Analytics 會列出資料來源](./media/data-lake-analytics-manage-use-cli/data-lake-analytics-list-data-source.png)

### <a name="delete-data-sources"></a><span data-ttu-id="47e48-149">刪除資料來源：</span><span class="sxs-lookup"><span data-stu-id="47e48-149">Delete data sources:</span></span>
<span data-ttu-id="47e48-150">toodelete Data Lake Store 帳戶：</span><span class="sxs-lookup"><span data-stu-id="47e48-150">toodelete a Data Lake Store account:</span></span>

      azure datalake analytics account datasource delete "<Data Lake Analytics Account Name>" "<Azure Data Lake Store Account Name>"

<span data-ttu-id="47e48-151">toodelete Blob 儲存體帳戶：</span><span class="sxs-lookup"><span data-stu-id="47e48-151">toodelete a Blob storage account:</span></span>

      azure datalake analytics account datasource delete "<Data Lake Analytics Account Name>" "<Blob Storage Account Name>"

## <a name="manage-jobs"></a><span data-ttu-id="47e48-152">管理工作</span><span class="sxs-lookup"><span data-stu-id="47e48-152">Manage jobs</span></span>
<span data-ttu-id="47e48-153">您必須擁有 Data Lake Analytics 帳戶，才能建立工作。</span><span class="sxs-lookup"><span data-stu-id="47e48-153">You must have a Data Lake Analytics account before you can create a job.</span></span>  <span data-ttu-id="47e48-154">如需詳細資訊，請參閱 [管理 Data Lake Analytics 帳戶](#manage-accounts)。</span><span class="sxs-lookup"><span data-stu-id="47e48-154">For more information, see [Manage Data Lake Analytics accounts](#manage-accounts).</span></span>

### <a name="list-jobs"></a><span data-ttu-id="47e48-155">列出工作</span><span class="sxs-lookup"><span data-stu-id="47e48-155">List jobs</span></span>
      azure datalake analytics job list -n "<Data Lake Analytics Account Name>"

![Data Lake Analytics 會列出資料來源](./media/data-lake-analytics-manage-use-cli/data-lake-analytics-list-jobs.png)

### <a name="get-job-details"></a><span data-ttu-id="47e48-157">取得工作詳細資料</span><span class="sxs-lookup"><span data-stu-id="47e48-157">Get job details</span></span>
      azure datalake analytics job show -n "<Data Lake Analytics Account Name>" -j "<Job ID>"

### <a name="submit-jobs"></a><span data-ttu-id="47e48-158">提交工作</span><span class="sxs-lookup"><span data-stu-id="47e48-158">Submit jobs</span></span>
> [!NOTE]
> <span data-ttu-id="47e48-159">工作的 hello 預設優先權為 1000，和工作平行處理原則的 hello 預設程度為 1。</span><span class="sxs-lookup"><span data-stu-id="47e48-159">hello default priority of a job is 1000, and hello default degree of parallelism for a job is 1.</span></span>
> 
> 

    azure datalake analytics job create  "<Data Lake Analytics Account Name>" "<Job Name>" "<Script>"

### <a name="cancel-jobs"></a><span data-ttu-id="47e48-160">取消工作</span><span class="sxs-lookup"><span data-stu-id="47e48-160">Cancel jobs</span></span>
<span data-ttu-id="47e48-161">使用 hello 清單命令 toofind hello 作業識別碼，然後再使用 [取消] 5d; toocancel hello 作業。</span><span class="sxs-lookup"><span data-stu-id="47e48-161">Use hello list command toofind hello job id, and then use cancel toocancel hello job.</span></span>

      azure datalake analytics job list -n "<Data Lake Analytics Account Name>"
      azure datalake analytics job cancel "<Data Lake Analytics Account Name>" "<Job ID>"

## <a name="manage-catalog"></a><span data-ttu-id="47e48-162">管理目錄</span><span class="sxs-lookup"><span data-stu-id="47e48-162">Manage catalog</span></span>
<span data-ttu-id="47e48-163">hello U-SQL 目錄會是使用的 toostructure 資料和程式碼，因此它們可以共用 U-SQL 指令碼。</span><span class="sxs-lookup"><span data-stu-id="47e48-163">hello U-SQL catalog is used toostructure data and code so they can be shared by U-SQL scripts.</span></span> <span data-ttu-id="47e48-164">hello 類別目錄可讓 hello Azure Data Lake 中的資料可能的最大效能。</span><span class="sxs-lookup"><span data-stu-id="47e48-164">hello catalog enables hello highest performance possible with data in Azure Data Lake.</span></span> <span data-ttu-id="47e48-165">如需詳細資訊，請參閱 [使用 U-SQL 目錄](data-lake-analytics-use-u-sql-catalog.md)。</span><span class="sxs-lookup"><span data-stu-id="47e48-165">For more information, see [Use U-SQL catalog](data-lake-analytics-use-u-sql-catalog.md).</span></span>

### <a name="list-catalog-items"></a><span data-ttu-id="47e48-166">列出目錄項目</span><span class="sxs-lookup"><span data-stu-id="47e48-166">List catalog items</span></span>
    #List databases
    azure datalake analytics catalog list -n "<Data Lake Analytics Account Name>" -t database

    #List tables
    azure datalake analytics catalog list -n "<Data Lake Analytics Account Name>" -t table

<span data-ttu-id="47e48-167">hello 類型包括資料庫、 結構描述、 組件、 外部資料來源、 資料表、 資料表值函式或資料表統計資料。</span><span class="sxs-lookup"><span data-stu-id="47e48-167">hello types include database, schema, assembly, external data source, table, table valued function or table statistics.</span></span>

<!-- ################################ -->
<!-- ################################ -->
## <a name="use-arm-groups"></a><span data-ttu-id="47e48-168">使用 ARM 群組</span><span class="sxs-lookup"><span data-stu-id="47e48-168">Use ARM groups</span></span>
<span data-ttu-id="47e48-169">應用程式通常由許多元件組成，例如，Web 應用程式、資料庫、資料庫伺服器、儲存體和協力廠商服務。</span><span class="sxs-lookup"><span data-stu-id="47e48-169">Applications are typically made up of many components, for example a web app, database, database server, storage, and 3rd party services.</span></span> <span data-ttu-id="47e48-170">Azure 資源管理員 (ARM) 可讓您與您的應用程式，為群組參照 tooas Azure 資源群組中的 hello 資源 toowork。</span><span class="sxs-lookup"><span data-stu-id="47e48-170">Azure Resource Manager (ARM) enables you toowork with hello resources in your application as a group, referred tooas an Azure Resource Group.</span></span> <span data-ttu-id="47e48-171">您可以部署、 更新、 監視或刪除所有 hello 資源應用程式在單一、 協調作業。</span><span class="sxs-lookup"><span data-stu-id="47e48-171">You can deploy, update, monitor or delete all of hello resources for your application in a single, coordinated operation.</span></span> <span data-ttu-id="47e48-172">您會使用部署的範本，且該範本可以用於不同的環境，例如測試、預備和生產環境。</span><span class="sxs-lookup"><span data-stu-id="47e48-172">You use a template for deployment and that template can work for different environments such as testing, staging and production.</span></span> <span data-ttu-id="47e48-173">您可以藉由檢視 hello hello 整個群組的彙總成本，計費釐清為您的組織。</span><span class="sxs-lookup"><span data-stu-id="47e48-173">You can clarify billing for your organization by viewing hello rolled-up costs for hello entire group.</span></span> <span data-ttu-id="47e48-174">如需詳細資訊，請參閱 [Azure 資源管理員概觀](../azure-resource-manager/resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="47e48-174">For more information, see [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md).</span></span> 

<span data-ttu-id="47e48-175">資料湖分析服務可包含下列元件的 hello:</span><span class="sxs-lookup"><span data-stu-id="47e48-175">A Data Lake Analytics service can include hello following components:</span></span>

* <span data-ttu-id="47e48-176">Azure Data Lake Analytics 帳戶</span><span class="sxs-lookup"><span data-stu-id="47e48-176">Azure Data Lake Analytics account</span></span>
* <span data-ttu-id="47e48-177">必要的預設 Azure Data Lake 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="47e48-177">Required default Azure Data Lake Storage account</span></span>
* <span data-ttu-id="47e48-178">其他 Azure Data Lake 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="47e48-178">Additional Azure Data Lake Storage accounts</span></span>
* <span data-ttu-id="47e48-179">其他 Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="47e48-179">Additional Azure Storage accounts</span></span>

<span data-ttu-id="47e48-180">您可以建立一個 ARM 群組 toomake 底下的所有這些元件它們更容易 toomanage。</span><span class="sxs-lookup"><span data-stu-id="47e48-180">You can create all these components under one ARM group toomake them easier toomanage.</span></span>

![Azure Data Lake Analytics 帳戶與儲存體](./media/data-lake-analytics-manage-use-portal/data-lake-analytics-arm-structure.png)

<span data-ttu-id="47e48-182">Data Lake Analytics 帳戶和 hello 相依的儲存體帳戶必須放置在 hello 相同 Azure 資料中心。</span><span class="sxs-lookup"><span data-stu-id="47e48-182">A Data Lake Analytics account and hello dependent storage accounts must be placed in hello same Azure data center.</span></span>
<span data-ttu-id="47e48-183">hello ARM 群組不過可以位於不同的資料中心。</span><span class="sxs-lookup"><span data-stu-id="47e48-183">hello ARM group however can be located in a different data center.</span></span>  

## <a name="see-also"></a><span data-ttu-id="47e48-184">另請參閱</span><span class="sxs-lookup"><span data-stu-id="47e48-184">See also</span></span>
* [<span data-ttu-id="47e48-185">Microsoft Azure Data Lake Analytics 概觀</span><span class="sxs-lookup"><span data-stu-id="47e48-185">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="47e48-186">使用 Azure 入口網站開始使用 Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="47e48-186">Get started with Data Lake Analytics using Azure Portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="47e48-187">使用 Azure 入口網站管理 Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="47e48-187">Manage Azure Data Lake Analytics using Azure Portal</span></span>](data-lake-analytics-manage-use-portal.md)
* [<span data-ttu-id="47e48-188">使用 Azure 入口網站監視和疑難排解 Azure Data Lake Analytics 工作</span><span class="sxs-lookup"><span data-stu-id="47e48-188">Monitor and troubleshoot Azure Data Lake Analytics jobs using Azure Portal</span></span>](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)

