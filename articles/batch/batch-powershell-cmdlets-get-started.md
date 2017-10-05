---
title: "開始使用 PowerShell for Azure Batch | Microsoft Docs"
description: "您可以用來管理 Batch 資源的 Azure PowerShell Cmdlet 快速簡介。"
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: f9ad62c5-27bf-4e6b-a5bf-c5f5914e6199
ms.service: batch
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: powershell
ms.workload: big-compute
ms.date: 02/27/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e33be6ed658e00250ea1e80cd7da4d348fb18296
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="manage-batch-resources-with-powershell-cmdlets"></a><span data-ttu-id="a02a2-103">使用 PowerShell Cmdlet 管理 Batch 資源</span><span class="sxs-lookup"><span data-stu-id="a02a2-103">Manage Batch resources with PowerShell cmdlets</span></span>

<span data-ttu-id="a02a2-104">使用 Azure Batch PowerShell Cmdlet，您可以執行與您使用 Batch API、Azure 入口網站和 Azure 命令列介面 (CLI) 執行的許多相同工作並撰寫其指令碼。</span><span class="sxs-lookup"><span data-stu-id="a02a2-104">With the Azure Batch PowerShell cmdlets, you can perform and script many of the same tasks you carry out with the Batch APIs, the Azure portal, and the Azure Command-Line Interface (CLI).</span></span> <span data-ttu-id="a02a2-105">本文會快速介紹可用來管理 Batch 帳戶和使用批次資源 (例如集區、作業和和工作) 的 Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="a02a2-105">This is a quick introduction to the cmdlets you can use to manage your Batch accounts and work with your Batch resources such as pools, jobs, and tasks.</span></span>

<span data-ttu-id="a02a2-106">如需批次 Cmdlet 和詳細 Cmdlet 語法的完整清單，請參閱 [Azure 批次 Cmdlet 參考資料](/powershell/module/azurerm.batch/#batch)。</span><span class="sxs-lookup"><span data-stu-id="a02a2-106">For a complete list of Batch cmdlets and detailed cmdlet syntax, see the [Azure Batch cmdlet reference](/powershell/module/azurerm.batch/#batch).</span></span>

<span data-ttu-id="a02a2-107">本文是根據 Azure PowerShell 3.0.0 版中的 Cmdlet 所撰寫。</span><span class="sxs-lookup"><span data-stu-id="a02a2-107">This article is based on cmdlets in Azure PowerShell version 3.0.0.</span></span> <span data-ttu-id="a02a2-108">建議您經常更新您的 Azure PowerShell 以利用服務更新和增強功能。</span><span class="sxs-lookup"><span data-stu-id="a02a2-108">We recommend that you update your Azure PowerShell frequently to take advantage of service updates and enhancements.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a02a2-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="a02a2-109">Prerequisites</span></span>
<span data-ttu-id="a02a2-110">執行下列作業，以使用 Azure PowerShell 來管理您的 Batch 資源。</span><span class="sxs-lookup"><span data-stu-id="a02a2-110">Perform the following operations to use Azure PowerShell to manage your Batch resources.</span></span>

* [<span data-ttu-id="a02a2-111">安裝並設定 Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="a02a2-111">Install and configure Azure PowerShell</span></span>](/powershell/azure/overview)
* <span data-ttu-id="a02a2-112">執行 **Login-AzureRmAccount** Cmdlet 以連線到訂用帳戶 (Azure Batch Cmdlet 隨附在 Azure Resource Manager 模組中)：</span><span class="sxs-lookup"><span data-stu-id="a02a2-112">Run the **Login-AzureRmAccount** cmdlet to connect to your subscription (the Azure Batch cmdlets ship in the Azure Resource Manager module):</span></span>
  
    `Login-AzureRmAccount`
* <span data-ttu-id="a02a2-113">**註冊 Batch 提供者命名空間**。</span><span class="sxs-lookup"><span data-stu-id="a02a2-113">**Register with the Batch provider namespace**.</span></span> <span data-ttu-id="a02a2-114">每個訂用帳戶只需要執行這項作業**一次**。</span><span class="sxs-lookup"><span data-stu-id="a02a2-114">This operation only needs to be performed **once per subscription**.</span></span>
  
    `Register-AzureRMResourceProvider -ProviderNamespace Microsoft.Batch`

## <a name="manage-batch-accounts-and-keys"></a><span data-ttu-id="a02a2-115">管理 Batch 帳戶和金鑰</span><span class="sxs-lookup"><span data-stu-id="a02a2-115">Manage Batch accounts and keys</span></span>
### <a name="create-a-batch-account"></a><span data-ttu-id="a02a2-116">建立批次帳戶：</span><span class="sxs-lookup"><span data-stu-id="a02a2-116">Create a Batch account</span></span>
<span data-ttu-id="a02a2-117">**New-AzureRmBatchAccount** 會在指定的資源群組中建立 Batch 帳戶。</span><span class="sxs-lookup"><span data-stu-id="a02a2-117">**New-AzureRmBatchAccount** creates a Batch account in a specified resource group.</span></span> <span data-ttu-id="a02a2-118">如果您還沒有資源群組，請執行 [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) Cmdlet 建立一個資源群組。</span><span class="sxs-lookup"><span data-stu-id="a02a2-118">If you don't already have a resource group, create one by running the [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet.</span></span> <span data-ttu-id="a02a2-119">在 **Location** 參數中指定其中一個 Azure 區域，例如 "Central US"。</span><span class="sxs-lookup"><span data-stu-id="a02a2-119">Specify one of the Azure regions in the **Location** parameter, such as "Central US".</span></span> <span data-ttu-id="a02a2-120">例如：</span><span class="sxs-lookup"><span data-stu-id="a02a2-120">For example:</span></span>

    New-AzureRmResourceGroup –Name MyBatchResourceGroup –location "Central US"

<span data-ttu-id="a02a2-121">然後，在資源群組中建立 Batch 帳戶，為 <account_name> 中的帳戶指定名稱，以及指定資源群組的位置和名稱。</span><span class="sxs-lookup"><span data-stu-id="a02a2-121">Then, create a Batch account in the resource group, specifying a name for the account in <*account_name*> and the location and name of your resource group.</span></span> <span data-ttu-id="a02a2-122">建立 Batch 帳戶可能需要一些時間來完成。</span><span class="sxs-lookup"><span data-stu-id="a02a2-122">Creating the Batch account can take some time to complete.</span></span> <span data-ttu-id="a02a2-123">例如：</span><span class="sxs-lookup"><span data-stu-id="a02a2-123">For example:</span></span>

    New-AzureRmBatchAccount –AccountName <account_name> –Location "Central US" –ResourceGroupName <res_group_name>

> [!NOTE]
> <span data-ttu-id="a02a2-124">Batch 帳戶名稱對資源群組的 Azure 區域必須是唯一的、包含 3 到 24 個字元，並只使用小寫字母和數字。</span><span class="sxs-lookup"><span data-stu-id="a02a2-124">The Batch account name must be unique to the Azure region for the resource group, contain between 3 and 24 characters, and use lowercase letters and numbers only.</span></span>
> 
> 

### <a name="get-account-access-keys"></a><span data-ttu-id="a02a2-125">取得帳戶存取金鑰</span><span class="sxs-lookup"><span data-stu-id="a02a2-125">Get account access keys</span></span>
<span data-ttu-id="a02a2-126">**Get-AzureRmBatchAccountKeys** 將顯示與 Azure Batch 帳戶相關聯的存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="a02a2-126">**Get-AzureRmBatchAccountKeys** shows the access keys associated with an Azure Batch account.</span></span> <span data-ttu-id="a02a2-127">例如，執行下列命令以取得您所建立帳戶的主要和次要金鑰。</span><span class="sxs-lookup"><span data-stu-id="a02a2-127">For example, run the following to get the primary and secondary keys of the account you created.</span></span>

    $Account = Get-AzureRmBatchAccountKeys –AccountName <account_name>

    $Account.PrimaryAccountKey

    $Account.SecondaryAccountKey

### <a name="generate-a-new-access-key"></a><span data-ttu-id="a02a2-128">產生新的存取金鑰</span><span class="sxs-lookup"><span data-stu-id="a02a2-128">Generate a new access key</span></span>
<span data-ttu-id="a02a2-129">**New-AzureRmBatchAccountKey** 將為 Azure Batch 帳戶產生新的主要或次要帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="a02a2-129">**New-AzureRmBatchAccountKey** generates a new primary or secondary account key for an Azure Batch account.</span></span> <span data-ttu-id="a02a2-130">例如，若要為您的 Batch 帳戶產生新的主要金鑰，請輸入：</span><span class="sxs-lookup"><span data-stu-id="a02a2-130">For example, to generate a new primary key for your Batch account, type:</span></span>

    New-AzureRmBatchAccountKey -AccountName <account_name> -KeyType Primary

> [!NOTE]
> <span data-ttu-id="a02a2-131">若要產生新的次要金鑰，請將 **KeyType** 參數指定為「次要」。</span><span class="sxs-lookup"><span data-stu-id="a02a2-131">To generate a new secondary key, specify "Secondary" for the **KeyType** parameter.</span></span> <span data-ttu-id="a02a2-132">您必須個別重新產生主要和次要金鑰。</span><span class="sxs-lookup"><span data-stu-id="a02a2-132">You have to regenerate the primary and secondary keys separately.</span></span>
> 
> 

### <a name="delete-a-batch-account"></a><span data-ttu-id="a02a2-133">刪除 Batch 帳戶</span><span class="sxs-lookup"><span data-stu-id="a02a2-133">Delete a Batch account</span></span>
<span data-ttu-id="a02a2-134">**Remove-AzureRmBatchAccount** 將刪除 Batch 帳戶。</span><span class="sxs-lookup"><span data-stu-id="a02a2-134">**Remove-AzureRmBatchAccount** deletes a Batch account.</span></span> <span data-ttu-id="a02a2-135">例如：</span><span class="sxs-lookup"><span data-stu-id="a02a2-135">For example:</span></span>

    Remove-AzureRmBatchAccount -AccountName <account_name>

<span data-ttu-id="a02a2-136">出現提示時，請確認您想要移除的帳戶。</span><span class="sxs-lookup"><span data-stu-id="a02a2-136">When prompted, confirm you want to remove the account.</span></span> <span data-ttu-id="a02a2-137">帳戶移除可能需要一些時間來完成。</span><span class="sxs-lookup"><span data-stu-id="a02a2-137">Account removal can take some time to complete.</span></span>

## <a name="create-a-batchaccountcontext-object"></a><span data-ttu-id="a02a2-138">建立 BatchAccountContext 物件</span><span class="sxs-lookup"><span data-stu-id="a02a2-138">Create a BatchAccountContext object</span></span>
<span data-ttu-id="a02a2-139">若要在建立和管理 Batch 集區、作業、工作和其他資源時使用 Batch PowerShell Cmdlet 來進行驗證，請先建立 BatchAccountContext 物件以儲存帳戶名稱和金鑰：</span><span class="sxs-lookup"><span data-stu-id="a02a2-139">To authenticate using the Batch PowerShell cmdlets when you create and manage Batch pools, jobs, tasks, and other resources, first create a BatchAccountContext object to store your account name and keys:</span></span>

    $context = Get-AzureRmBatchAccountKeys -AccountName <account_name>

<span data-ttu-id="a02a2-140">您必須將 BatchAccountContext 物件傳遞給使用 **BatchContext** 參數的 Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="a02a2-140">You pass the BatchAccountContext object into cmdlets that use the **BatchContext** parameter.</span></span>

> [!NOTE]
> <span data-ttu-id="a02a2-141">依預設，帳戶的主要金鑰用於驗證，但是您可以透過變更 BatchAccountContext 物件的 **KeyInUse** 屬性，明確地選取要使用的金鑰：`$context.KeyInUse = "Secondary"`。</span><span class="sxs-lookup"><span data-stu-id="a02a2-141">By default, the account's primary key is used for authentication, but you can explicitly select the key to use by changing your BatchAccountContext object’s **KeyInUse** property: `$context.KeyInUse = "Secondary"`.</span></span>
> 
> 

## <a name="create-and-modify-batch-resources"></a><span data-ttu-id="a02a2-142">建立和修改批次資源</span><span class="sxs-lookup"><span data-stu-id="a02a2-142">Create and modify Batch resources</span></span>
<span data-ttu-id="a02a2-143">請使用 **New-AzureBatchPool**、**New-AzureBatchJob** 和 **New-AzureBatchTask** 之類的 Cmdlet 在 Batch 帳戶下建立資源。</span><span class="sxs-lookup"><span data-stu-id="a02a2-143">Use cmdlets such as **New-AzureBatchPool**, **New-AzureBatchJob**, and **New-AzureBatchTask** to create resources under a Batch account.</span></span> <span data-ttu-id="a02a2-144">要更新現有資源的屬性，有對應的 **Get-** 和 **Set-** Cmdlet ，要移除 Batch 帳戶下的資源，則有 **Remove-** Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="a02a2-144">There are corresponding **Get-** and **Set-** cmdlets to update the properties of existing resources, and  **Remove-** cmdlets to remove resources under a Batch account.</span></span>

<span data-ttu-id="a02a2-145">使用許多這類 Cmdlet 時，除了傳遞 BatchContext 物件，您還需要建立或傳遞包含詳細資源設定的物件，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="a02a2-145">When using many of these cmdlets, in addition to passing a BatchContext object, you need to create or pass objects that contain detailed resource settings, as shown in the following example.</span></span> <span data-ttu-id="a02a2-146">如需其他範例，請參閱每個 Cmdlet 的詳細說明。</span><span class="sxs-lookup"><span data-stu-id="a02a2-146">See the detailed help for each cmdlet for additional examples.</span></span>

### <a name="create-a-batch-pool"></a><span data-ttu-id="a02a2-147">建立 Batch 集區</span><span class="sxs-lookup"><span data-stu-id="a02a2-147">Create a Batch pool</span></span>
<span data-ttu-id="a02a2-148">建立或更新 Batch 集區時，請為計算節點上的作業系統選取雲端服務設定或虛擬機器設定 (請參閱 [Batch 功能概觀](batch-api-basics.md#pool))。</span><span class="sxs-lookup"><span data-stu-id="a02a2-148">When creating or updating a Batch pool, you select either the cloud service configuration or the virtual machine configuration for the operating system on the compute nodes (see [Batch feature overview](batch-api-basics.md#pool)).</span></span> <span data-ttu-id="a02a2-149">如果您指定雲端服務設定，則會使用其中一個 [Azure 客體 OS 版本](../cloud-services/cloud-services-guestos-update-matrix.md#releases)來製作計算節點的映像。</span><span class="sxs-lookup"><span data-stu-id="a02a2-149">If you specify the cloud service configuration, your compute nodes are imaged with one of the [Azure Guest OS releases](../cloud-services/cloud-services-guestos-update-matrix.md#releases).</span></span> <span data-ttu-id="a02a2-150">如果您指定虛擬機器設定，則可以指定 [Azure 虛擬機器 Marketplace][vm_marketplace] 所列的其中一個支援的 Linux 或 Windows VM 映像，或提供您已準備的自訂映像。</span><span class="sxs-lookup"><span data-stu-id="a02a2-150">If you specify the virtual machine configuration, you can either specify one of the supported Linux or Windows VM images listed in the [Azure Virtual Machines Marketplace][vm_marketplace], or provide a custom image that you have prepared.</span></span>

<span data-ttu-id="a02a2-151">當您執行 **New-AzureBatchPool**時，請在 PSCloudServiceConfiguration 或 PSVirtualMachineConfiguration 物件中傳遞作業系統設定。</span><span class="sxs-lookup"><span data-stu-id="a02a2-151">When you run **New-AzureBatchPool**, pass the operating system settings in a PSCloudServiceConfiguration or PSVirtualMachineConfiguration object.</span></span> <span data-ttu-id="a02a2-152">例如，下列 Cmdlet 會使用雲端服務組態中的小型計算節點建立新的 Batch 集區，並以最新的系列 3 (Windows Server 2012) 作業系統版本製作映像。</span><span class="sxs-lookup"><span data-stu-id="a02a2-152">For example, the following cmdlet creates a new Batch pool with size Small compute nodes in the cloud service configuration, imaged with the latest operating system version of family 3 (Windows Server 2012).</span></span> <span data-ttu-id="a02a2-153">在此，**CloudServiceConfiguration** 參數會指定 $configuration 變數做為 PSCloudServiceConfiguration 物件。</span><span class="sxs-lookup"><span data-stu-id="a02a2-153">Here, the **CloudServiceConfiguration** parameter specifies the *$configuration* variable as the PSCloudServiceConfiguration object.</span></span> <span data-ttu-id="a02a2-154">**BatchContext** 參數會將先前定義的變數 $context 指定為 BatchAccountContext 物件。</span><span class="sxs-lookup"><span data-stu-id="a02a2-154">The **BatchContext** parameter specifies a previously defined variable *$context* as the BatchAccountContext object.</span></span>

    $configuration = New-Object -TypeName "Microsoft.Azure.Commands.Batch.Models.PSCloudServiceConfiguration" -ArgumentList @(4,"*")

    New-AzureBatchPool -Id "AutoScalePool" -VirtualMachineSize "Small" -CloudServiceConfiguration $configuration -AutoScaleFormula '$TargetDedicated=4;' -BatchContext $context

<span data-ttu-id="a02a2-155">新集區中計算節點的目標數目是由自動調整公式決定。</span><span class="sxs-lookup"><span data-stu-id="a02a2-155">The target number of compute nodes in the new pool is determined by an autoscaling formula.</span></span> <span data-ttu-id="a02a2-156">在此案例中，此公式僅僅是 **$TargetDedicated=4**，表示集區中的計算節點數最多為 4 個。</span><span class="sxs-lookup"><span data-stu-id="a02a2-156">In this case, the formula is simply **$TargetDedicated=4**, indicating the number of compute nodes in the pool is 4 at most.</span></span>

## <a name="query-for-pools-jobs-tasks-and-other-details"></a><span data-ttu-id="a02a2-157">查詢集區、作業、工作及其他詳細資料</span><span class="sxs-lookup"><span data-stu-id="a02a2-157">Query for pools, jobs, tasks, and other details</span></span>
<span data-ttu-id="a02a2-158">使用 Cmdelt (例如 **Get-AzureBatchPool**、**Get-AzureBatchJob** 和 **Get-AzureBatchTask**) 查詢在 Batch 帳戶下建立的實體。</span><span class="sxs-lookup"><span data-stu-id="a02a2-158">Use cmdlets such as **Get-AzureBatchPool**, **Get-AzureBatchJob**, and **Get-AzureBatchTask** to query for entities created under a Batch account.</span></span>

### <a name="query-for-data"></a><span data-ttu-id="a02a2-159">查詢資料</span><span class="sxs-lookup"><span data-stu-id="a02a2-159">Query for data</span></span>
<span data-ttu-id="a02a2-160">例如，使用 **Get-AzureBatchPools** 尋找您的集區。</span><span class="sxs-lookup"><span data-stu-id="a02a2-160">As an example, use **Get-AzureBatchPools** to find your pools.</span></span> <span data-ttu-id="a02a2-161">依預設，這將查詢您帳戶下的所有集區，並假設您已經將 BatchAccountContext 物件儲存在 *$context*中：</span><span class="sxs-lookup"><span data-stu-id="a02a2-161">By default this queries for all pools under your account, assuming you already stored the BatchAccountContext object in *$context*:</span></span>

    Get-AzureBatchPool -BatchContext $context

### <a name="use-an-odata-filter"></a><span data-ttu-id="a02a2-162">使用 OData 篩選</span><span class="sxs-lookup"><span data-stu-id="a02a2-162">Use an OData filter</span></span>
<span data-ttu-id="a02a2-163">您可以提供 **篩選** 參數給 OData 篩選，只尋找您感興趣的物件。</span><span class="sxs-lookup"><span data-stu-id="a02a2-163">You can supply an OData filter using the **Filter** parameter to find only the objects you’re interested in.</span></span> <span data-ttu-id="a02a2-164">例如，您可以找到識別碼以 “myPool” 開頭的所有集區：</span><span class="sxs-lookup"><span data-stu-id="a02a2-164">For example, you can find all pools with ids starting with “myPool”:</span></span>

    $filter = "startswith(id,'myPool')"

    Get-AzureBatchPool -Filter $filter -BatchContext $context

<span data-ttu-id="a02a2-165">雖然這個方法比在本機管線中使用 “Where-Object” 較不具有彈性，</span><span class="sxs-lookup"><span data-stu-id="a02a2-165">This method is not as flexible as using “Where-Object” in a local pipeline.</span></span> <span data-ttu-id="a02a2-166">不過查詢將直接傳送進 Batch 服務，讓所有篩選在伺服器端運作，進而省下網際網路頻寬。</span><span class="sxs-lookup"><span data-stu-id="a02a2-166">However, the query gets sent to the Batch service directly so that all filtering happens on the server side, saving Internet bandwidth.</span></span>

### <a name="use-the-id-parameter"></a><span data-ttu-id="a02a2-167">使用識別碼參數</span><span class="sxs-lookup"><span data-stu-id="a02a2-167">Use the Id parameter</span></span>
<span data-ttu-id="a02a2-168">使用 **Id** 參數可做為 OData 篩選器的替代方式。</span><span class="sxs-lookup"><span data-stu-id="a02a2-168">An alternative to an OData filter is to use the **Id** parameter.</span></span> <span data-ttu-id="a02a2-169">若要查詢識別碼為 "myPool" 的特定集區：</span><span class="sxs-lookup"><span data-stu-id="a02a2-169">To query for a specific pool with id "myPool":</span></span>

    Get-AzureBatchPool -Id "myPool" -BatchContext $context

<span data-ttu-id="a02a2-170">**Id** 參數僅支援完整識別碼的搜尋，不能使用萬用字元或 OData 樣式的篩選器。</span><span class="sxs-lookup"><span data-stu-id="a02a2-170">The **Id** parameter supports only full-id search, not wildcards or OData-style filters.</span></span>

### <a name="use-the-maxcount-parameter"></a><span data-ttu-id="a02a2-171">使用 MaxCount 參數</span><span class="sxs-lookup"><span data-stu-id="a02a2-171">Use the MaxCount parameter</span></span>
<span data-ttu-id="a02a2-172">依預設，每個 Cmdlet 最多傳回 1000 個物件。</span><span class="sxs-lookup"><span data-stu-id="a02a2-172">By default, each cmdlet returns a maximum of 1000 objects.</span></span> <span data-ttu-id="a02a2-173">如果到達此限制，請調整您的篩選器以傳回較少的物件，或使用 **MaxCount** 參數明確地設定最大值。</span><span class="sxs-lookup"><span data-stu-id="a02a2-173">If you reach this limit, either refine your filter to bring back fewer objects, or explicitly set a maximum using the **MaxCount** parameter.</span></span> <span data-ttu-id="a02a2-174">例如：</span><span class="sxs-lookup"><span data-stu-id="a02a2-174">For example:</span></span>

    Get-AzureBatchTask -MaxCount 2500 -BatchContext $context

<span data-ttu-id="a02a2-175">若要移除上限，將 **MaxCount** 設定為 0 或更少。</span><span class="sxs-lookup"><span data-stu-id="a02a2-175">To remove the upper bound, set **MaxCount** to 0 or less.</span></span>

### <a name="use-the-powershell-pipeline"></a><span data-ttu-id="a02a2-176">使用 PowerShell 管線</span><span class="sxs-lookup"><span data-stu-id="a02a2-176">Use the PowerShell pipeline</span></span>
<span data-ttu-id="a02a2-177">Batch Cmdlet 可以利用 PowerShell 管線在 Cmdlet 之間傳送資料。</span><span class="sxs-lookup"><span data-stu-id="a02a2-177">Batch cmdlets can leverage the PowerShell pipeline to send data between cmdlets.</span></span> <span data-ttu-id="a02a2-178">這和指定參數有相同的效果，但是讓處理多個實體更容易。</span><span class="sxs-lookup"><span data-stu-id="a02a2-178">This has the same effect as specifying a parameter, but makes working with multiple entities easier.</span></span>

<span data-ttu-id="a02a2-179">例如，尋找和顯示您帳戶下的所有作業：</span><span class="sxs-lookup"><span data-stu-id="a02a2-179">For example, find and display all tasks under your account:</span></span>

    Get-AzureBatchJob -BatchContext $context | Get-AzureBatchTask -BatchContext $context

<span data-ttu-id="a02a2-180">重新啟動集區中的每個計算節點︰</span><span class="sxs-lookup"><span data-stu-id="a02a2-180">Restart (reboot) every compute node in a pool:</span></span>

    Get-AzureBatchComputeNode -PoolId "myPool" -BatchContext $context | Restart-AzureBatchComputeNode -BatchContext $context

## <a name="application-package-management"></a><span data-ttu-id="a02a2-181">應用程式封裝管理</span><span class="sxs-lookup"><span data-stu-id="a02a2-181">Application package management</span></span>
<span data-ttu-id="a02a2-182">應用程式封裝提供了簡化的方式，可將應用程式部署至您集區中的計算節點。</span><span class="sxs-lookup"><span data-stu-id="a02a2-182">Application packages provide a simplified way to deploy applications to the compute nodes in your pools.</span></span> <span data-ttu-id="a02a2-183">利用 Batch PowerShell Cmdlet，您可以上傳和管理 Batch 帳戶中的應用程式套件，並將套件版本部署至計算節點。</span><span class="sxs-lookup"><span data-stu-id="a02a2-183">With the Batch PowerShell cmdlets, you can upload and manage application packages in your Batch account, and deploy package versions to compute nodes.</span></span>

<span data-ttu-id="a02a2-184">**建立** 應用程式：</span><span class="sxs-lookup"><span data-stu-id="a02a2-184">**Create** an application:</span></span>

    New-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication"

<span data-ttu-id="a02a2-185">**新增** 應用程式封裝︰</span><span class="sxs-lookup"><span data-stu-id="a02a2-185">**Add** an application package:</span></span>

    New-AzureRmBatchApplicationPackage -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication" -ApplicationVersion "1.0" -Format zip -FilePath package001.zip

<span data-ttu-id="a02a2-186">設定應用程式的**預設版本**︰</span><span class="sxs-lookup"><span data-stu-id="a02a2-186">Set the **default version** for the application:</span></span>

    Set-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication" -DefaultVersion "1.0"

<span data-ttu-id="a02a2-187">**列出**應用程式的套件</span><span class="sxs-lookup"><span data-stu-id="a02a2-187">**List** an application's packages</span></span>

    $application = Get-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication"

    $application.ApplicationPackages

<span data-ttu-id="a02a2-188">**刪除**應用程式套件</span><span class="sxs-lookup"><span data-stu-id="a02a2-188">**Delete** an application package</span></span>

    Remove-AzureRmBatchApplicationPackage -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication" -ApplicationVersion "1.0"

<span data-ttu-id="a02a2-189">**刪除**應用程式</span><span class="sxs-lookup"><span data-stu-id="a02a2-189">**Delete** an application</span></span>

    Remove-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication"

> [!NOTE]
> <span data-ttu-id="a02a2-190">您必須先刪除所有應用程式的應用程式套件版本，才能刪除應用程式。</span><span class="sxs-lookup"><span data-stu-id="a02a2-190">You must delete all of an application's application package versions before you delete the application.</span></span> <span data-ttu-id="a02a2-191">如果您嘗試刪除目前具有應用程式套件的應用程式，您會收到「衝突」錯誤。</span><span class="sxs-lookup"><span data-stu-id="a02a2-191">You will receive a 'Conflict' error if you try to delete an application that currently has application packages.</span></span>
> 
> 

### <a name="deploy-an-application-package"></a><span data-ttu-id="a02a2-192">部署應用程式封裝</span><span class="sxs-lookup"><span data-stu-id="a02a2-192">Deploy an application package</span></span>
<span data-ttu-id="a02a2-193">您可以在建立集區時，指定一或多個應用程式套件以供部署。</span><span class="sxs-lookup"><span data-stu-id="a02a2-193">You can specify one or more application packages for deployment when you create a pool.</span></span> <span data-ttu-id="a02a2-194">當您在建立集區時指定封裝時，它會在節點加入集區時部署到每個節點。</span><span class="sxs-lookup"><span data-stu-id="a02a2-194">When you specify a package at pool creation time, it is deployed to each node as the node joins pool.</span></span> <span data-ttu-id="a02a2-195">重新啟動或重新安裝映像節點時，也會部署套件。</span><span class="sxs-lookup"><span data-stu-id="a02a2-195">Packages are also deployed when a node is rebooted or reimaged.</span></span>

<span data-ttu-id="a02a2-196">在建立集區時指定 `-ApplicationPackageReference` 選項，以在節點加入集區時將應用程式套件部署到集區的節點。</span><span class="sxs-lookup"><span data-stu-id="a02a2-196">Specify the `-ApplicationPackageReference` option when creating a pool to deploy an application package to the pool's nodes as they join the pool.</span></span> <span data-ttu-id="a02a2-197">首先，建立 **PSApplicationPackageReference** 物件，然後以您要部署至集區中計算節點的應用程式識別碼和套件版本進行設定︰</span><span class="sxs-lookup"><span data-stu-id="a02a2-197">First, create a **PSApplicationPackageReference** object, and configure it with the application Id and package version you want to deploy to the pool's compute nodes:</span></span>

    $appPackageReference = New-Object Microsoft.Azure.Commands.Batch.Models.PSApplicationPackageReference

    $appPackageReference.ApplicationId = "MyBatchApplication"

    $appPackageReference.Version = "1.0"

<span data-ttu-id="a02a2-198">現在建立集區，並指定套件參考物件做為 `ApplicationPackageReferences` 選項的引數︰</span><span class="sxs-lookup"><span data-stu-id="a02a2-198">Now create the pool, and specify the package reference object as the argument to the `ApplicationPackageReferences` option:</span></span>

    New-AzureBatchPool -Id "PoolWithAppPackage" -VirtualMachineSize "Small" -CloudServiceConfiguration $configuration -BatchContext $context -ApplicationPackageReferences $appPackageReference

<span data-ttu-id="a02a2-199">您可以在[使用 Batch 應用程式套件將應用程式部署至計算節點](batch-application-packages.md)中找到應用程式套件的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="a02a2-199">You can find more information on application packages in [Deploy applications to compute nodes with Batch application packages](batch-application-packages.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a02a2-200">您必須先 [連結 Azure 儲存體帳戶](#linked-storage-account-autostorage) 到您的 Batch 帳戶，才能使用應用程式套件。</span><span class="sxs-lookup"><span data-stu-id="a02a2-200">You must [link an Azure Storage account](#linked-storage-account-autostorage) to your Batch account to use application packages.</span></span>
> 
> 

### <a name="update-a-pools-application-packages"></a><span data-ttu-id="a02a2-201">更新集區的應用程式封裝</span><span class="sxs-lookup"><span data-stu-id="a02a2-201">Update a pool's application packages</span></span>
<span data-ttu-id="a02a2-202">若要更新指派給現有集區的應用程式，請先使用所需的屬性 (應用程式識別碼和套件版本) 建立 PSApplicationPackageReference 物件︰</span><span class="sxs-lookup"><span data-stu-id="a02a2-202">To update the applications assigned to an existing pool, first create a PSApplicationPackageReference object with the desired properties (application Id and package version):</span></span>

    $appPackageReference = New-Object Microsoft.Azure.Commands.Batch.Models.PSApplicationPackageReference

    $appPackageReference.ApplicationId = "MyBatchApplication"

    $appPackageReference.Version = "2.0"

<span data-ttu-id="a02a2-203">接下來，從 Batch 取得集區、清除任何現有的套件、新增我們新的套件參考，以及使用新的集區設定更新 Batch 服務︰</span><span class="sxs-lookup"><span data-stu-id="a02a2-203">Next, get the pool from Batch, clear out any existing packages, add our new package reference, and update the Batch service with the new pool settings:</span></span>

    $pool = Get-AzureBatchPool -BatchContext $context -Id "PoolWithAppPackage"

    $pool.ApplicationPackageReferences.Clear()

    $pool.ApplicationPackageReferences.Add($appPackageReference)

    Set-AzureBatchPool -BatchContext $context -Pool $pool

<span data-ttu-id="a02a2-204">您現在已更新 Batch 服務中集區的屬性。</span><span class="sxs-lookup"><span data-stu-id="a02a2-204">You've now updated the pool's properties in the Batch service.</span></span> <span data-ttu-id="a02a2-205">若要將新的應用程式套件實際部署至集區中的計算節點，您必須重新啟動這些節點或重新安裝其映像。</span><span class="sxs-lookup"><span data-stu-id="a02a2-205">To actually deploy the new application package to compute nodes in the pool, however, you must restart or reimage those nodes.</span></span> <span data-ttu-id="a02a2-206">您可以使用此命令重新啟動集區中的每個節點︰</span><span class="sxs-lookup"><span data-stu-id="a02a2-206">You can restart every node in a pool with this command:</span></span>

    Get-AzureBatchComputeNode -PoolId "PoolWithAppPackage" -BatchContext $context | Restart-AzureBatchComputeNode -BatchContext $context

> [!TIP]
> <span data-ttu-id="a02a2-207">您可以將多個應用程式套件部署至集區中的計算節點。</span><span class="sxs-lookup"><span data-stu-id="a02a2-207">You can deploy multiple application packages to the compute nodes in a pool.</span></span> <span data-ttu-id="a02a2-208">如果您想要新增應用程式套件，而非取代目前部署的套件，請省略上面的 `$pool.ApplicationPackageReferences.Clear()` 一行。</span><span class="sxs-lookup"><span data-stu-id="a02a2-208">If you'd like to *add* an application package instead of replacing the currently deployed packages, omit the `$pool.ApplicationPackageReferences.Clear()` line above.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="a02a2-209">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a02a2-209">Next steps</span></span>
* <span data-ttu-id="a02a2-210">如需詳細的 Cmdlet 語法和範例，請參閱 [Azure Batch Cmdlet 參考資料](/powershell/module/azurerm.batch/#batch)。</span><span class="sxs-lookup"><span data-stu-id="a02a2-210">For detailed cmdlet syntax and examples, see [Azure Batch cmdlet reference](/powershell/module/azurerm.batch/#batch).</span></span>
* <span data-ttu-id="a02a2-211">如需 Batch 中應用程式和應用程式套件的詳細資訊，請參閱[使用 Batch 應用程式套件將應用程式部署至計算節點](batch-application-packages.md)。</span><span class="sxs-lookup"><span data-stu-id="a02a2-211">For more information about applications and application packages in Batch, see [Deploy applications to compute nodes with Batch application packages](batch-application-packages.md).</span></span>

[vm_marketplace]: https://azure.microsoft.com/marketplace/virtual-machines/