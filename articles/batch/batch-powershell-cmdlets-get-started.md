---
title: "Azure 批次開始使用 PowerShell aaaGet |Microsoft 文件"
description: "快速介紹 toohello Azure PowerShell cmdlet，您可以使用 toomanage 批次的資源。"
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
ms.openlocfilehash: 3e4d12e9c1e52a5b2db2dd44346edda93b7ef92b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-batch-resources-with-powershell-cmdlets"></a><span data-ttu-id="b8238-103">使用 PowerShell Cmdlet 管理 Batch 資源</span><span class="sxs-lookup"><span data-stu-id="b8238-103">Manage Batch resources with PowerShell cmdlets</span></span>

<span data-ttu-id="b8238-104">以 hello Azure 批次的 PowerShell cmdlet，您可以執行，並編寫指令碼的 hello 許多相同的工作，當您執行以 hello 批次 Api hello Azure 入口網站和 hello Azure 命令列介面 (CLI)。</span><span class="sxs-lookup"><span data-stu-id="b8238-104">With hello Azure Batch PowerShell cmdlets, you can perform and script many of hello same tasks you carry out with hello Batch APIs, hello Azure portal, and hello Azure Command-Line Interface (CLI).</span></span> <span data-ttu-id="b8238-105">這是您可以使用 toomanage 批次帳戶，並使用您的批次資源，例如集區、 工作和工作的快速簡介 toohello cmdlet。</span><span class="sxs-lookup"><span data-stu-id="b8238-105">This is a quick introduction toohello cmdlets you can use toomanage your Batch accounts and work with your Batch resources such as pools, jobs, and tasks.</span></span>

<span data-ttu-id="b8238-106">如需的批次 cmdlet，以及詳細的 cmdlet 語法的完整清單，請參閱 hello [Azure 批次指令程式參考](/powershell/module/azurerm.batch/#batch)。</span><span class="sxs-lookup"><span data-stu-id="b8238-106">For a complete list of Batch cmdlets and detailed cmdlet syntax, see hello [Azure Batch cmdlet reference](/powershell/module/azurerm.batch/#batch).</span></span>

<span data-ttu-id="b8238-107">本文是根據 Azure PowerShell 3.0.0 版中的 Cmdlet 所撰寫。</span><span class="sxs-lookup"><span data-stu-id="b8238-107">This article is based on cmdlets in Azure PowerShell version 3.0.0.</span></span> <span data-ttu-id="b8238-108">我們建議您更新您的 Azure PowerShell 經常 tootake 的服務更新和增強功能的優點。</span><span class="sxs-lookup"><span data-stu-id="b8238-108">We recommend that you update your Azure PowerShell frequently tootake advantage of service updates and enhancements.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b8238-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="b8238-109">Prerequisites</span></span>
<span data-ttu-id="b8238-110">執行下列作業 toouse Azure PowerShell toomanage hello 批次資源。</span><span class="sxs-lookup"><span data-stu-id="b8238-110">Perform hello following operations toouse Azure PowerShell toomanage your Batch resources.</span></span>

* [<span data-ttu-id="b8238-111">安裝並設定 Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b8238-111">Install and configure Azure PowerShell</span></span>](/powershell/azure/overview)
* <span data-ttu-id="b8238-112">執行 hello**登入 AzureRmAccount** cmdlet tooconnect tooyour 訂用帳戶 (hello hello Azure Resource Manager 模組中的 Azure 批次 cmdlet 出貨):</span><span class="sxs-lookup"><span data-stu-id="b8238-112">Run hello **Login-AzureRmAccount** cmdlet tooconnect tooyour subscription (hello Azure Batch cmdlets ship in hello Azure Resource Manager module):</span></span>
  
    `Login-AzureRmAccount`
* <span data-ttu-id="b8238-113">**向 hello 批次提供者命名空間**。</span><span class="sxs-lookup"><span data-stu-id="b8238-113">**Register with hello Batch provider namespace**.</span></span> <span data-ttu-id="b8238-114">這項作業只需要執行 toobe**每個訂閱一次**。</span><span class="sxs-lookup"><span data-stu-id="b8238-114">This operation only needs toobe performed **once per subscription**.</span></span>
  
    `Register-AzureRMResourceProvider -ProviderNamespace Microsoft.Batch`

## <a name="manage-batch-accounts-and-keys"></a><span data-ttu-id="b8238-115">管理 Batch 帳戶和金鑰</span><span class="sxs-lookup"><span data-stu-id="b8238-115">Manage Batch accounts and keys</span></span>
### <a name="create-a-batch-account"></a><span data-ttu-id="b8238-116">建立批次帳戶：</span><span class="sxs-lookup"><span data-stu-id="b8238-116">Create a Batch account</span></span>
<span data-ttu-id="b8238-117">**New-AzureRmBatchAccount** 會在指定的資源群組中建立 Batch 帳戶。</span><span class="sxs-lookup"><span data-stu-id="b8238-117">**New-AzureRmBatchAccount** creates a Batch account in a specified resource group.</span></span> <span data-ttu-id="b8238-118">如果您還沒有資源群組，建立一個執行 hello[新增 AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="b8238-118">If you don't already have a resource group, create one by running hello [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet.</span></span> <span data-ttu-id="b8238-119">指定一個 hello Azure 區域中 hello**位置**參數，例如"Central US"。</span><span class="sxs-lookup"><span data-stu-id="b8238-119">Specify one of hello Azure regions in hello **Location** parameter, such as "Central US".</span></span> <span data-ttu-id="b8238-120">例如：</span><span class="sxs-lookup"><span data-stu-id="b8238-120">For example:</span></span>

    New-AzureRmResourceGroup –Name MyBatchResourceGroup –location "Central US"

<span data-ttu-id="b8238-121">然後，在 hello 資源群組中，指定在 hello 帳戶的名稱建立 Batch 帳戶 <*account_name*> hello 位置和資源群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="b8238-121">Then, create a Batch account in hello resource group, specifying a name for hello account in <*account_name*> and hello location and name of your resource group.</span></span> <span data-ttu-id="b8238-122">建立 hello 批次帳戶可能需要一些時間 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="b8238-122">Creating hello Batch account can take some time toocomplete.</span></span> <span data-ttu-id="b8238-123">例如：</span><span class="sxs-lookup"><span data-stu-id="b8238-123">For example:</span></span>

    New-AzureRmBatchAccount –AccountName <account_name> –Location "Central US" –ResourceGroupName <res_group_name>

> [!NOTE]
> <span data-ttu-id="b8238-124">hello 批次帳戶名稱必須是唯一 toohello hello 資源群組，Azure 地區介於 3 到 24 個字元，並使用小寫字母和數字只。</span><span class="sxs-lookup"><span data-stu-id="b8238-124">hello Batch account name must be unique toohello Azure region for hello resource group, contain between 3 and 24 characters, and use lowercase letters and numbers only.</span></span>
> 
> 

### <a name="get-account-access-keys"></a><span data-ttu-id="b8238-125">取得帳戶存取金鑰</span><span class="sxs-lookup"><span data-stu-id="b8238-125">Get account access keys</span></span>
<span data-ttu-id="b8238-126">**Get AzureRmBatchAccountKeys**顯示 hello Azure Batch 帳戶相關聯的存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="b8238-126">**Get-AzureRmBatchAccountKeys** shows hello access keys associated with an Azure Batch account.</span></span> <span data-ttu-id="b8238-127">例如，執行下列 tooget hello 主要和次要金鑰建立 hello 帳戶 hello。</span><span class="sxs-lookup"><span data-stu-id="b8238-127">For example, run hello following tooget hello primary and secondary keys of hello account you created.</span></span>

    $Account = Get-AzureRmBatchAccountKeys –AccountName <account_name>

    $Account.PrimaryAccountKey

    $Account.SecondaryAccountKey

### <a name="generate-a-new-access-key"></a><span data-ttu-id="b8238-128">產生新的存取金鑰</span><span class="sxs-lookup"><span data-stu-id="b8238-128">Generate a new access key</span></span>
<span data-ttu-id="b8238-129">**New-AzureRmBatchAccountKey** 將為 Azure Batch 帳戶產生新的主要或次要帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="b8238-129">**New-AzureRmBatchAccountKey** generates a new primary or secondary account key for an Azure Batch account.</span></span> <span data-ttu-id="b8238-130">例如，您的 Batch 帳戶的新主索引鍵 toogenerate 輸入：</span><span class="sxs-lookup"><span data-stu-id="b8238-130">For example, toogenerate a new primary key for your Batch account, type:</span></span>

    New-AzureRmBatchAccountKey -AccountName <account_name> -KeyType Primary

> [!NOTE]
> <span data-ttu-id="b8238-131">toogenerate 新的次要金鑰，指定 「 次要 」 hello **KeyType**參數。</span><span class="sxs-lookup"><span data-stu-id="b8238-131">toogenerate a new secondary key, specify "Secondary" for hello **KeyType** parameter.</span></span> <span data-ttu-id="b8238-132">您可以分別有 tooregenerate hello 主要和次要金鑰。</span><span class="sxs-lookup"><span data-stu-id="b8238-132">You have tooregenerate hello primary and secondary keys separately.</span></span>
> 
> 

### <a name="delete-a-batch-account"></a><span data-ttu-id="b8238-133">刪除 Batch 帳戶</span><span class="sxs-lookup"><span data-stu-id="b8238-133">Delete a Batch account</span></span>
<span data-ttu-id="b8238-134">**Remove-AzureRmBatchAccount** 將刪除 Batch 帳戶。</span><span class="sxs-lookup"><span data-stu-id="b8238-134">**Remove-AzureRmBatchAccount** deletes a Batch account.</span></span> <span data-ttu-id="b8238-135">例如：</span><span class="sxs-lookup"><span data-stu-id="b8238-135">For example:</span></span>

    Remove-AzureRmBatchAccount -AccountName <account_name>

<span data-ttu-id="b8238-136">出現提示時，請確認您要讓 tooremove hello 帳戶。</span><span class="sxs-lookup"><span data-stu-id="b8238-136">When prompted, confirm you want tooremove hello account.</span></span> <span data-ttu-id="b8238-137">移除帳戶可能需要一些時間 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="b8238-137">Account removal can take some time toocomplete.</span></span>

## <a name="create-a-batchaccountcontext-object"></a><span data-ttu-id="b8238-138">建立 BatchAccountContext 物件</span><span class="sxs-lookup"><span data-stu-id="b8238-138">Create a BatchAccountContext object</span></span>
<span data-ttu-id="b8238-139">當您建立和管理批次集區、 工作、 工作和其他資源，請先建立 BatchAccountContext 物件 toostore，您的帳戶名稱和金鑰時，使用 tooauthenticate hello 批次的 PowerShell cmdlet:</span><span class="sxs-lookup"><span data-stu-id="b8238-139">tooauthenticate using hello Batch PowerShell cmdlets when you create and manage Batch pools, jobs, tasks, and other resources, first create a BatchAccountContext object toostore your account name and keys:</span></span>

    $context = Get-AzureRmBatchAccountKeys -AccountName <account_name>

<span data-ttu-id="b8238-140">您 hello BatchAccountContext 將物件傳遞至指令程式，使用 hello **BatchContext**參數。</span><span class="sxs-lookup"><span data-stu-id="b8238-140">You pass hello BatchAccountContext object into cmdlets that use hello **BatchContext** parameter.</span></span>

> [!NOTE]
> <span data-ttu-id="b8238-141">根據預設，hello 帳戶的主索引鍵用於驗證，但是您可以藉由變更 BatchAccountContext 物件的明確地選取 hello 金鑰 toouse **KeyInUse**屬性： `$context.KeyInUse = "Secondary"`。</span><span class="sxs-lookup"><span data-stu-id="b8238-141">By default, hello account's primary key is used for authentication, but you can explicitly select hello key toouse by changing your BatchAccountContext object’s **KeyInUse** property: `$context.KeyInUse = "Secondary"`.</span></span>
> 
> 

## <a name="create-and-modify-batch-resources"></a><span data-ttu-id="b8238-142">建立和修改批次資源</span><span class="sxs-lookup"><span data-stu-id="b8238-142">Create and modify Batch resources</span></span>
<span data-ttu-id="b8238-143">使用 cmdlet，例如**新增 AzureBatchPool**，**新增 AzureBatchJob**，和**新增 AzureBatchTask** toocreate 批次帳戶下的資源。</span><span class="sxs-lookup"><span data-stu-id="b8238-143">Use cmdlets such as **New-AzureBatchPool**, **New-AzureBatchJob**, and **New-AzureBatchTask** toocreate resources under a Batch account.</span></span> <span data-ttu-id="b8238-144">都那里對應**Get-**和**Set-** cmdlet tooupdate hello 屬性，現有的資源和**移除-** cmdlet tooremove 資源，批次帳戶下的。</span><span class="sxs-lookup"><span data-stu-id="b8238-144">There are corresponding **Get-** and **Set-** cmdlets tooupdate hello properties of existing resources, and  **Remove-** cmdlets tooremove resources under a Batch account.</span></span>

<span data-ttu-id="b8238-145">許多這些 cmdlet，在中使用時增加 toopassing BatchContext 物件，您需要 toocreate，或傳遞物件，其中包含詳細的資源設定，如 hello 下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="b8238-145">When using many of these cmdlets, in addition toopassing a BatchContext object, you need toocreate or pass objects that contain detailed resource settings, as shown in hello following example.</span></span> <span data-ttu-id="b8238-146">請參閱 hello 詳細說明每個 cmdlet，如需其他範例。</span><span class="sxs-lookup"><span data-stu-id="b8238-146">See hello detailed help for each cmdlet for additional examples.</span></span>

### <a name="create-a-batch-pool"></a><span data-ttu-id="b8238-147">建立 Batch 集區</span><span class="sxs-lookup"><span data-stu-id="b8238-147">Create a Batch pool</span></span>
<span data-ttu-id="b8238-148">當建立或更新的批次集區，您選取 hello 雲端服務組態或 hello 虛擬機器組態的 hello hello 上作業系統的計算節點 (請參閱[批次功能概觀](batch-api-basics.md#pool))。</span><span class="sxs-lookup"><span data-stu-id="b8238-148">When creating or updating a Batch pool, you select either hello cloud service configuration or hello virtual machine configuration for hello operating system on hello compute nodes (see [Batch feature overview](batch-api-basics.md#pool)).</span></span> <span data-ttu-id="b8238-149">如果您指定 hello 雲端服務組態，其中包含一個 hello 處理計算節點[Azure 客體 OS 版本](../cloud-services/cloud-services-guestos-update-matrix.md#releases)。</span><span class="sxs-lookup"><span data-stu-id="b8238-149">If you specify hello cloud service configuration, your compute nodes are imaged with one of hello [Azure Guest OS releases](../cloud-services/cloud-services-guestos-update-matrix.md#releases).</span></span> <span data-ttu-id="b8238-150">如果您指定 hello 虛擬機器組態，您可以指定 hello 的其中一個支援的 Linux 或 Windows VM 映像中所列的 hello [Azure 虛擬機器 Marketplace][vm_marketplace]，或提供自訂您已經備妥的映像。</span><span class="sxs-lookup"><span data-stu-id="b8238-150">If you specify hello virtual machine configuration, you can either specify one of hello supported Linux or Windows VM images listed in hello [Azure Virtual Machines Marketplace][vm_marketplace], or provide a custom image that you have prepared.</span></span>

<span data-ttu-id="b8238-151">當您執行**新增 AzureBatchPool**，傳遞 PSCloudServiceConfiguration 或 PSVirtualMachineConfiguration 物件中的 hello 作業系統設定。</span><span class="sxs-lookup"><span data-stu-id="b8238-151">When you run **New-AzureBatchPool**, pass hello operating system settings in a PSCloudServiceConfiguration or PSVirtualMachineConfiguration object.</span></span> <span data-ttu-id="b8238-152">例如，hello 下列 cmdlet 會建立新的批次集區大小小型運算中的節點 hello 雲端服務組態，建立映像與 hello 最新作業系統版本系列 3 (Windows Server 2012)。</span><span class="sxs-lookup"><span data-stu-id="b8238-152">For example, hello following cmdlet creates a new Batch pool with size Small compute nodes in hello cloud service configuration, imaged with hello latest operating system version of family 3 (Windows Server 2012).</span></span> <span data-ttu-id="b8238-153">在這裡，hello **CloudServiceConfiguration**參數會指定 hello *$configuration*變數作為 hello PSCloudServiceConfiguration 物件。</span><span class="sxs-lookup"><span data-stu-id="b8238-153">Here, hello **CloudServiceConfiguration** parameter specifies hello *$configuration* variable as hello PSCloudServiceConfiguration object.</span></span> <span data-ttu-id="b8238-154">hello **BatchContext**參數會指定先前定義的變數*$context*為 hello BatchAccountContext 物件。</span><span class="sxs-lookup"><span data-stu-id="b8238-154">hello **BatchContext** parameter specifies a previously defined variable *$context* as hello BatchAccountContext object.</span></span>

    $configuration = New-Object -TypeName "Microsoft.Azure.Commands.Batch.Models.PSCloudServiceConfiguration" -ArgumentList @(4,"*")

    New-AzureBatchPool -Id "AutoScalePool" -VirtualMachineSize "Small" -CloudServiceConfiguration $configuration -AutoScaleFormula '$TargetDedicated=4;' -BatchContext $context

<span data-ttu-id="b8238-155">計算節點 hello 新集區中的 hello 目標數目取決於自動調整公式。</span><span class="sxs-lookup"><span data-stu-id="b8238-155">hello target number of compute nodes in hello new pool is determined by an autoscaling formula.</span></span> <span data-ttu-id="b8238-156">Hello 公式在此情況下，只是**$TargetDedicated = 4**，指出 hello hello 集區中的運算節點數目最多為 4。</span><span class="sxs-lookup"><span data-stu-id="b8238-156">In this case, hello formula is simply **$TargetDedicated=4**, indicating hello number of compute nodes in hello pool is 4 at most.</span></span>

## <a name="query-for-pools-jobs-tasks-and-other-details"></a><span data-ttu-id="b8238-157">查詢集區、作業、工作及其他詳細資料</span><span class="sxs-lookup"><span data-stu-id="b8238-157">Query for pools, jobs, tasks, and other details</span></span>
<span data-ttu-id="b8238-158">使用 cmdlet，例如**Get AzureBatchPool**， **Get AzureBatchJob**，和**Get AzureBatchTask** tooquery 批次帳戶下建立的實體。</span><span class="sxs-lookup"><span data-stu-id="b8238-158">Use cmdlets such as **Get-AzureBatchPool**, **Get-AzureBatchJob**, and **Get-AzureBatchTask** tooquery for entities created under a Batch account.</span></span>

### <a name="query-for-data"></a><span data-ttu-id="b8238-159">查詢資料</span><span class="sxs-lookup"><span data-stu-id="b8238-159">Query for data</span></span>
<span data-ttu-id="b8238-160">例如，使用**Get AzureBatchPools** toofind 程式集區。</span><span class="sxs-lookup"><span data-stu-id="b8238-160">As an example, use **Get-AzureBatchPools** toofind your pools.</span></span> <span data-ttu-id="b8238-161">根據預設，此查詢在您的帳戶下的所有集區，假設您已經儲存中的 hello BatchAccountContext 物件*$context*:</span><span class="sxs-lookup"><span data-stu-id="b8238-161">By default this queries for all pools under your account, assuming you already stored hello BatchAccountContext object in *$context*:</span></span>

    Get-AzureBatchPool -BatchContext $context

### <a name="use-an-odata-filter"></a><span data-ttu-id="b8238-162">使用 OData 篩選</span><span class="sxs-lookup"><span data-stu-id="b8238-162">Use an OData filter</span></span>
<span data-ttu-id="b8238-163">您可以提供的 OData 篩選器使用 hello**篩選**參數 toofind 只 hello 您感興趣的物件。</span><span class="sxs-lookup"><span data-stu-id="b8238-163">You can supply an OData filter using hello **Filter** parameter toofind only hello objects you’re interested in.</span></span> <span data-ttu-id="b8238-164">例如，您可以找到識別碼以 “myPool” 開頭的所有集區：</span><span class="sxs-lookup"><span data-stu-id="b8238-164">For example, you can find all pools with ids starting with “myPool”:</span></span>

    $filter = "startswith(id,'myPool')"

    Get-AzureBatchPool -Filter $filter -BatchContext $context

<span data-ttu-id="b8238-165">雖然這個方法比在本機管線中使用 “Where-Object” 較不具有彈性，</span><span class="sxs-lookup"><span data-stu-id="b8238-165">This method is not as flexible as using “Where-Object” in a local pipeline.</span></span> <span data-ttu-id="b8238-166">不過，hello 查詢取得 toohello 批次服務直接傳送，讓所有的篩選發生在 hello 伺服器端，儲存的網際網路頻寬。</span><span class="sxs-lookup"><span data-stu-id="b8238-166">However, hello query gets sent toohello Batch service directly so that all filtering happens on hello server side, saving Internet bandwidth.</span></span>

### <a name="use-hello-id-parameter"></a><span data-ttu-id="b8238-167">使用 hello Id 參數</span><span class="sxs-lookup"><span data-stu-id="b8238-167">Use hello Id parameter</span></span>
<span data-ttu-id="b8238-168">替代 tooan OData 篩選器為 toouse hello**識別碼**參數。</span><span class="sxs-lookup"><span data-stu-id="b8238-168">An alternative tooan OData filter is toouse hello **Id** parameter.</span></span> <span data-ttu-id="b8238-169">識別碼"myPool 」 的特定集區的 tooquery:</span><span class="sxs-lookup"><span data-stu-id="b8238-169">tooquery for a specific pool with id "myPool":</span></span>

    Get-AzureBatchPool -Id "myPool" -BatchContext $context

<span data-ttu-id="b8238-170">hello**識別碼**參數僅支援完整識別碼搜尋，不使用萬用字元或 OData 樣式篩選器。</span><span class="sxs-lookup"><span data-stu-id="b8238-170">hello **Id** parameter supports only full-id search, not wildcards or OData-style filters.</span></span>

### <a name="use-hello-maxcount-parameter"></a><span data-ttu-id="b8238-171">使用 hello MaxCount 參數</span><span class="sxs-lookup"><span data-stu-id="b8238-171">Use hello MaxCount parameter</span></span>
<span data-ttu-id="b8238-172">依預設，每個 Cmdlet 最多傳回 1000 個物件。</span><span class="sxs-lookup"><span data-stu-id="b8238-172">By default, each cmdlet returns a maximum of 1000 objects.</span></span> <span data-ttu-id="b8238-173">如果達到此限制，請精簡篩選 toobring 回較少的物件，或明確地設定最多使用 hello **MaxCount**參數。</span><span class="sxs-lookup"><span data-stu-id="b8238-173">If you reach this limit, either refine your filter toobring back fewer objects, or explicitly set a maximum using hello **MaxCount** parameter.</span></span> <span data-ttu-id="b8238-174">例如：</span><span class="sxs-lookup"><span data-stu-id="b8238-174">For example:</span></span>

    Get-AzureBatchTask -MaxCount 2500 -BatchContext $context

<span data-ttu-id="b8238-175">tooremove hello 上限設定**MaxCount** too0 或更少。</span><span class="sxs-lookup"><span data-stu-id="b8238-175">tooremove hello upper bound, set **MaxCount** too0 or less.</span></span>

### <a name="use-hello-powershell-pipeline"></a><span data-ttu-id="b8238-176">使用 hello PowerShell 管線</span><span class="sxs-lookup"><span data-stu-id="b8238-176">Use hello PowerShell pipeline</span></span>
<span data-ttu-id="b8238-177">批次指令程式可以利用 hello PowerShell 管線 toosend 資料之間的指令程式。</span><span class="sxs-lookup"><span data-stu-id="b8238-177">Batch cmdlets can leverage hello PowerShell pipeline toosend data between cmdlets.</span></span> <span data-ttu-id="b8238-178">這會有相同效果與指定的參數，但具有多個實體工作的 hello。</span><span class="sxs-lookup"><span data-stu-id="b8238-178">This has hello same effect as specifying a parameter, but makes working with multiple entities easier.</span></span>

<span data-ttu-id="b8238-179">例如，尋找和顯示您帳戶下的所有作業：</span><span class="sxs-lookup"><span data-stu-id="b8238-179">For example, find and display all tasks under your account:</span></span>

    Get-AzureBatchJob -BatchContext $context | Get-AzureBatchTask -BatchContext $context

<span data-ttu-id="b8238-180">重新啟動集區中的每個計算節點︰</span><span class="sxs-lookup"><span data-stu-id="b8238-180">Restart (reboot) every compute node in a pool:</span></span>

    Get-AzureBatchComputeNode -PoolId "myPool" -BatchContext $context | Restart-AzureBatchComputeNode -BatchContext $context

## <a name="application-package-management"></a><span data-ttu-id="b8238-181">應用程式封裝管理</span><span class="sxs-lookup"><span data-stu-id="b8238-181">Application package management</span></span>
<span data-ttu-id="b8238-182">應用程式套件提供一個簡化的方式 toodeploy 應用程式 toohello 計算您的集區中的節點。</span><span class="sxs-lookup"><span data-stu-id="b8238-182">Application packages provide a simplified way toodeploy applications toohello compute nodes in your pools.</span></span> <span data-ttu-id="b8238-183">以 hello 批次的 PowerShell cmdlet，您可以上傳和管理您的 Batch 帳戶中的應用程式封裝及部署封裝版本 toocompute 節點。</span><span class="sxs-lookup"><span data-stu-id="b8238-183">With hello Batch PowerShell cmdlets, you can upload and manage application packages in your Batch account, and deploy package versions toocompute nodes.</span></span>

<span data-ttu-id="b8238-184">**建立** 應用程式：</span><span class="sxs-lookup"><span data-stu-id="b8238-184">**Create** an application:</span></span>

    New-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication"

<span data-ttu-id="b8238-185">**新增** 應用程式封裝︰</span><span class="sxs-lookup"><span data-stu-id="b8238-185">**Add** an application package:</span></span>

    New-AzureRmBatchApplicationPackage -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication" -ApplicationVersion "1.0" -Format zip -FilePath package001.zip

<span data-ttu-id="b8238-186">設定 hello**預設版本**hello 應用程式：</span><span class="sxs-lookup"><span data-stu-id="b8238-186">Set hello **default version** for hello application:</span></span>

    Set-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication" -DefaultVersion "1.0"

<span data-ttu-id="b8238-187">**列出**應用程式的套件</span><span class="sxs-lookup"><span data-stu-id="b8238-187">**List** an application's packages</span></span>

    $application = Get-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication"

    $application.ApplicationPackages

<span data-ttu-id="b8238-188">**刪除**應用程式套件</span><span class="sxs-lookup"><span data-stu-id="b8238-188">**Delete** an application package</span></span>

    Remove-AzureRmBatchApplicationPackage -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication" -ApplicationVersion "1.0"

<span data-ttu-id="b8238-189">**刪除**應用程式</span><span class="sxs-lookup"><span data-stu-id="b8238-189">**Delete** an application</span></span>

    Remove-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication"

> [!NOTE]
> <span data-ttu-id="b8238-190">您必須先刪除所有應用程式的應用程式封裝版本，然後再刪除 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b8238-190">You must delete all of an application's application package versions before you delete hello application.</span></span> <span data-ttu-id="b8238-191">如果您嘗試 toodelete 目前具有應用程式封裝的應用程式，您會收到 '衝突' 錯誤。</span><span class="sxs-lookup"><span data-stu-id="b8238-191">You will receive a 'Conflict' error if you try toodelete an application that currently has application packages.</span></span>
> 
> 

### <a name="deploy-an-application-package"></a><span data-ttu-id="b8238-192">部署應用程式封裝</span><span class="sxs-lookup"><span data-stu-id="b8238-192">Deploy an application package</span></span>
<span data-ttu-id="b8238-193">您可以在建立集區時，指定一或多個應用程式套件以供部署。</span><span class="sxs-lookup"><span data-stu-id="b8238-193">You can specify one or more application packages for deployment when you create a pool.</span></span> <span data-ttu-id="b8238-194">當您在集區建立期間指定套件時，它是已部署的 tooeach 節點 hello 節點聯結集區。</span><span class="sxs-lookup"><span data-stu-id="b8238-194">When you specify a package at pool creation time, it is deployed tooeach node as hello node joins pool.</span></span> <span data-ttu-id="b8238-195">重新啟動或重新安裝映像節點時，也會部署套件。</span><span class="sxs-lookup"><span data-stu-id="b8238-195">Packages are also deployed when a node is rebooted or reimaged.</span></span>

<span data-ttu-id="b8238-196">指定 hello`-ApplicationPackageReference`選項加入 hello 集區的應用程式封裝 toohello 集區的節點建立集區 toodeploy 時。</span><span class="sxs-lookup"><span data-stu-id="b8238-196">Specify hello `-ApplicationPackageReference` option when creating a pool toodeploy an application package toohello pool's nodes as they join hello pool.</span></span> <span data-ttu-id="b8238-197">首先，建立**PSApplicationPackageReference**物件，並將它設定 hello 應用程式識別碼和封裝版本想 toodeploy toohello 集區的計算節點：</span><span class="sxs-lookup"><span data-stu-id="b8238-197">First, create a **PSApplicationPackageReference** object, and configure it with hello application Id and package version you want toodeploy toohello pool's compute nodes:</span></span>

    $appPackageReference = New-Object Microsoft.Azure.Commands.Batch.Models.PSApplicationPackageReference

    $appPackageReference.ApplicationId = "MyBatchApplication"

    $appPackageReference.Version = "1.0"

<span data-ttu-id="b8238-198">現在建立 hello 集區，並指定 hello 封裝參考物件，如 hello 引數 toohello`ApplicationPackageReferences`選項：</span><span class="sxs-lookup"><span data-stu-id="b8238-198">Now create hello pool, and specify hello package reference object as hello argument toohello `ApplicationPackageReferences` option:</span></span>

    New-AzureBatchPool -Id "PoolWithAppPackage" -VirtualMachineSize "Small" -CloudServiceConfiguration $configuration -BatchContext $context -ApplicationPackageReferences $appPackageReference

<span data-ttu-id="b8238-199">您可以找到更多有關應用程式封裝中[部署與批次應用程式套件的應用程式 toocompute 節點](batch-application-packages.md)。</span><span class="sxs-lookup"><span data-stu-id="b8238-199">You can find more information on application packages in [Deploy applications toocompute nodes with Batch application packages](batch-application-packages.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b8238-200">您必須[Azure 儲存體帳戶連結](#linked-storage-account-autostorage)tooyour 批次帳戶 toouse 應用程式封裝。</span><span class="sxs-lookup"><span data-stu-id="b8238-200">You must [link an Azure Storage account](#linked-storage-account-autostorage) tooyour Batch account toouse application packages.</span></span>
> 
> 

### <a name="update-a-pools-application-packages"></a><span data-ttu-id="b8238-201">更新集區的應用程式封裝</span><span class="sxs-lookup"><span data-stu-id="b8238-201">Update a pool's application packages</span></span>
<span data-ttu-id="b8238-202">指派 tooan 現有集區的 tooupdate hello 應用程式首先會建立 PSApplicationPackageReference 物件具有所需的 hello 屬性 （應用程式識別碼和封裝版本）：</span><span class="sxs-lookup"><span data-stu-id="b8238-202">tooupdate hello applications assigned tooan existing pool, first create a PSApplicationPackageReference object with hello desired properties (application Id and package version):</span></span>

    $appPackageReference = New-Object Microsoft.Azure.Commands.Batch.Models.PSApplicationPackageReference

    $appPackageReference.ApplicationId = "MyBatchApplication"

    $appPackageReference.Version = "2.0"

<span data-ttu-id="b8238-203">接下來，批次中收到 hello 集區、 清除任何現有的封裝、 加入我們新的封裝參考，和 hello 批次服務更新的 hello 新集區設定：</span><span class="sxs-lookup"><span data-stu-id="b8238-203">Next, get hello pool from Batch, clear out any existing packages, add our new package reference, and update hello Batch service with hello new pool settings:</span></span>

    $pool = Get-AzureBatchPool -BatchContext $context -Id "PoolWithAppPackage"

    $pool.ApplicationPackageReferences.Clear()

    $pool.ApplicationPackageReferences.Add($appPackageReference)

    Set-AzureBatchPool -BatchContext $context -Pool $pool

<span data-ttu-id="b8238-204">您現在已更新 hello 批次服務中的 hello 集區的屬性。</span><span class="sxs-lookup"><span data-stu-id="b8238-204">You've now updated hello pool's properties in hello Batch service.</span></span> <span data-ttu-id="b8238-205">tooactually 部署 hello 新應用程式封裝 toocompute 節點 hello 集區中的，不過，您必須重新啟動或重新安裝映像的那些節點。</span><span class="sxs-lookup"><span data-stu-id="b8238-205">tooactually deploy hello new application package toocompute nodes in hello pool, however, you must restart or reimage those nodes.</span></span> <span data-ttu-id="b8238-206">您可以使用此命令重新啟動集區中的每個節點︰</span><span class="sxs-lookup"><span data-stu-id="b8238-206">You can restart every node in a pool with this command:</span></span>

    Get-AzureBatchComputeNode -PoolId "PoolWithAppPackage" -BatchContext $context | Restart-AzureBatchComputeNode -BatchContext $context

> [!TIP]
> <span data-ttu-id="b8238-207">您可以部署多個應用程式封裝 toohello 計算節點集區中。</span><span class="sxs-lookup"><span data-stu-id="b8238-207">You can deploy multiple application packages toohello compute nodes in a pool.</span></span> <span data-ttu-id="b8238-208">如果您希望太*新增*應用程式封裝，而不是取代目前部署的 hello 封裝省略 hello`$pool.ApplicationPackageReferences.Clear()`上述列。</span><span class="sxs-lookup"><span data-stu-id="b8238-208">If you'd like too*add* an application package instead of replacing hello currently deployed packages, omit hello `$pool.ApplicationPackageReferences.Clear()` line above.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="b8238-209">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b8238-209">Next steps</span></span>
* <span data-ttu-id="b8238-210">如需詳細的 Cmdlet 語法和範例，請參閱 [Azure Batch Cmdlet 參考資料](/powershell/module/azurerm.batch/#batch)。</span><span class="sxs-lookup"><span data-stu-id="b8238-210">For detailed cmdlet syntax and examples, see [Azure Batch cmdlet reference](/powershell/module/azurerm.batch/#batch).</span></span>
* <span data-ttu-id="b8238-211">如需應用程式和批次中的應用程式套件的詳細資訊，請參閱[部署與批次應用程式套件的應用程式 toocompute 節點](batch-application-packages.md)。</span><span class="sxs-lookup"><span data-stu-id="b8238-211">For more information about applications and application packages in Batch, see [Deploy applications toocompute nodes with Batch application packages](batch-application-packages.md).</span></span>

[vm_marketplace]: https://azure.microsoft.com/marketplace/virtual-machines/