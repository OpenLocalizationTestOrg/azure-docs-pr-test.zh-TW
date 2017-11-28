---
title: "建立和修改 ExpressRoute 線路︰PowerShell：Azure 傳統| Microsoft Docs"
description: "這篇文章會引導您完成建立及佈建 ExpressRoute 循環的 hello 步驟。 本文也會顯示 toocheck hello 狀態如何更新或刪除和取消佈建您的電路。"
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 0134d242-6459-4dec-a2f1-4657c3bc8b23
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/21/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: 9897c88776a2153ba22aa9ff328becb9f12b660b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-an-expressroute-circuit-using-powershell-classic"></a><span data-ttu-id="9f18c-104">使用 PowerShell 建立和修改 ExpressRoute 線路 (傳統)</span><span class="sxs-lookup"><span data-stu-id="9f18c-104">Create and modify an ExpressRoute circuit using PowerShell (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9f18c-105">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="9f18c-105">Azure portal</span></span>](expressroute-howto-circuit-portal-resource-manager.md)
> * [<span data-ttu-id="9f18c-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9f18c-106">PowerShell</span></span>](expressroute-howto-circuit-arm.md)
> * [<span data-ttu-id="9f18c-107">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="9f18c-107">Azure CLI</span></span>](howto-circuit-cli.md)
> * [<span data-ttu-id="9f18c-108">影片 - Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="9f18c-108">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [<span data-ttu-id="9f18c-109">PowerShell (傳統)</span><span class="sxs-lookup"><span data-stu-id="9f18c-109">PowerShell (classic)</span></span>](expressroute-howto-circuit-classic.md)
>

<span data-ttu-id="9f18c-110">這篇文章會引導您透過 hello 步驟 toocreate Azure ExpressRoute 循環使用 PowerShell cmdlet 和 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="9f18c-110">This article walks you through hello steps toocreate an Azure ExpressRoute circuit by using PowerShell cmdlets and hello classic deployment model.</span></span> <span data-ttu-id="9f18c-111">本文也會顯示 toocheck hello 狀態如何更新或刪除和取消佈建 ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="9f18c-111">This article also shows you how toocheck hello status, update, or delete and deprovision an ExpressRoute circuit.</span></span>

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]


<span data-ttu-id="9f18c-112">**關於 Azure 部署模型**</span><span class="sxs-lookup"><span data-stu-id="9f18c-112">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="before-you-begin"></a><span data-ttu-id="9f18c-113">開始之前</span><span class="sxs-lookup"><span data-stu-id="9f18c-113">Before you begin</span></span>
### <a name="step-1-review-hello-prerequisites-and-workflow-articles"></a><span data-ttu-id="9f18c-114">步驟 1.</span><span class="sxs-lookup"><span data-stu-id="9f18c-114">Step 1.</span></span> <span data-ttu-id="9f18c-115">檢閱 hello 必要條件和工作流程發行項</span><span class="sxs-lookup"><span data-stu-id="9f18c-115">Review hello prerequisites and workflow articles</span></span>
<span data-ttu-id="9f18c-116">請確定您已經檢閱 hello[必要條件](expressroute-prerequisites.md)和[工作流程](expressroute-workflows.md)開始設定之前。</span><span class="sxs-lookup"><span data-stu-id="9f18c-116">Make sure that you have reviewed hello [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>  

### <a name="step-2-install-hello-latest-versions-of-hello-azure-service-management-sm-powershell-modules"></a><span data-ttu-id="9f18c-117">步驟 2.</span><span class="sxs-lookup"><span data-stu-id="9f18c-117">Step 2.</span></span> <span data-ttu-id="9f18c-118">安裝 hello hello Azure 服務管理 (SM) PowerShell 模組最新版本</span><span class="sxs-lookup"><span data-stu-id="9f18c-118">Install hello latest versions of hello Azure Service Management (SM) PowerShell modules</span></span>
<span data-ttu-id="9f18c-119">請依照下列中的 hello 指示[開始使用 Azure PowerShell 指令程式](/powershell/azure/overview)的逐步指示如何 tooconfigure 電腦 toouse hello Azure PowerShell 模組。</span><span class="sxs-lookup"><span data-stu-id="9f18c-119">Follow hello instructions in [Getting started with Azure PowerShell cmdlets](/powershell/azure/overview) for step-by-step guidance on how tooconfigure your computer toouse hello Azure PowerShell modules.</span></span>

### <a name="step-3-log-in-tooyour-azure-account-and-select-a-subscription"></a><span data-ttu-id="9f18c-120">步驟 3.</span><span class="sxs-lookup"><span data-stu-id="9f18c-120">Step 3.</span></span> <span data-ttu-id="9f18c-121">登入 tooyour Azure 帳戶，然後選取訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="9f18c-121">Log in tooyour Azure account and select a subscription</span></span>
1. <span data-ttu-id="9f18c-122">使用提高的權限開啟 PowerShell 主控台和 tooyour 帳戶連接。</span><span class="sxs-lookup"><span data-stu-id="9f18c-122">Open your PowerShell console with elevated rights and connect tooyour account.</span></span> <span data-ttu-id="9f18c-123">使用下列範例 toohelp 您連接的 hello:</span><span class="sxs-lookup"><span data-stu-id="9f18c-123">Use hello following example toohelp you connect:</span></span>

        Login-AzureRmAccount

2. <span data-ttu-id="9f18c-124">請檢查 hello hello 帳戶的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="9f18c-124">Check hello subscriptions for hello account.</span></span>

        Get-AzureRmSubscription

3. <span data-ttu-id="9f18c-125">如果您有多個訂閱，選取您想 toouse hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="9f18c-125">If you have more than one subscription, select hello subscription that you want toouse.</span></span>

        Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"

4. <span data-ttu-id="9f18c-126">接下來，使用下列 cmdlet tooadd hello Azure 訂用帳戶 tooPowerShell hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="9f18c-126">Next, use hello following cmdlet tooadd your Azure subscription tooPowerShell for hello classic deployment model.</span></span>

        Add-AzureAccount

## <a name="create-and-provision-an-expressroute-circuit"></a><span data-ttu-id="9f18c-127">建立和佈建 ExpressRoute 線路</span><span class="sxs-lookup"><span data-stu-id="9f18c-127">Create and provision an ExpressRoute circuit</span></span>
### <a name="step-1-import-hello-powershell-modules-for-expressroute"></a><span data-ttu-id="9f18c-128">步驟 1.</span><span class="sxs-lookup"><span data-stu-id="9f18c-128">Step 1.</span></span> <span data-ttu-id="9f18c-129">Hello PowerShell 模組匯入 expressroute</span><span class="sxs-lookup"><span data-stu-id="9f18c-129">Import hello PowerShell modules for ExpressRoute</span></span>
 <span data-ttu-id="9f18c-130">如果您尚未這樣做，必須以 hello PowerShell 工作階段中使用 hello ExpressRoute cmdlet 的順序 toostart 匯 hello Azure 和 ExpressRoute 模組。</span><span class="sxs-lookup"><span data-stu-id="9f18c-130">If you have not already done so, you must import hello Azure and ExpressRoute modules into hello PowerShell session in order toostart using hello ExpressRoute cmdlets.</span></span> <span data-ttu-id="9f18c-131">您匯入 hello 模組 hello 從它們的位置安裝 tooon 本機電腦。</span><span class="sxs-lookup"><span data-stu-id="9f18c-131">You import hello modules from hello location that they were installed tooon your local computer.</span></span> <span data-ttu-id="9f18c-132">您可以根據 hello 方法使用 tooinstall hello 模組，可能不同於下列範例所示的 hello hello 位置。</span><span class="sxs-lookup"><span data-stu-id="9f18c-132">Depending on hello method you used tooinstall hello modules, hello location may be different than hello following example shows.</span></span> <span data-ttu-id="9f18c-133">如有必要，請修改 hello 範例。</span><span class="sxs-lookup"><span data-stu-id="9f18c-133">Modify hello example if necessary.</span></span>  

    Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
    Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'

### <a name="step-2-get-hello-list-of-supported-providers-locations-and-bandwidths"></a><span data-ttu-id="9f18c-134">步驟 2.</span><span class="sxs-lookup"><span data-stu-id="9f18c-134">Step 2.</span></span> <span data-ttu-id="9f18c-135">取得支援的提供者、 位置及頻寬 hello 清單</span><span class="sxs-lookup"><span data-stu-id="9f18c-135">Get hello list of supported providers, locations, and bandwidths</span></span>
<span data-ttu-id="9f18c-136">建立 ExpressRoute 電路之前，您需要支援的連線提供者、 位置及頻寬選項的 hello 清單。</span><span class="sxs-lookup"><span data-stu-id="9f18c-136">Before you create an ExpressRoute circuit, you need hello list of supported connectivity providers, locations, and bandwidth options.</span></span>

<span data-ttu-id="9f18c-137">hello PowerShell cmdlet`Get-AzureDedicatedCircuitServiceProvider`傳回這項資訊在稍後步驟中，您將使用：</span><span class="sxs-lookup"><span data-stu-id="9f18c-137">hello PowerShell cmdlet `Get-AzureDedicatedCircuitServiceProvider` returns this information, which you’ll use in later steps:</span></span>

    Get-AzureDedicatedCircuitServiceProvider

<span data-ttu-id="9f18c-138">請檢查 toosee，如果您連線服務提供者已列於此處。</span><span class="sxs-lookup"><span data-stu-id="9f18c-138">Check toosee if your connectivity provider is listed there.</span></span> <span data-ttu-id="9f18c-139">請記下的下列資訊，因為您將需要它稍後建立電路的 hello:</span><span class="sxs-lookup"><span data-stu-id="9f18c-139">Make a note of hello following information because you'll need it later when you create a circuit:</span></span>

* <span data-ttu-id="9f18c-140">名稱</span><span class="sxs-lookup"><span data-stu-id="9f18c-140">Name</span></span>
* <span data-ttu-id="9f18c-141">PeeringLocations</span><span class="sxs-lookup"><span data-stu-id="9f18c-141">PeeringLocations</span></span>
* <span data-ttu-id="9f18c-142">BandwidthsOffered</span><span class="sxs-lookup"><span data-stu-id="9f18c-142">BandwidthsOffered</span></span>

<span data-ttu-id="9f18c-143">您現在準備好 toocreate ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="9f18c-143">You're now ready toocreate an ExpressRoute circuit.</span></span>         

### <a name="step-3-create-an-expressroute-circuit"></a><span data-ttu-id="9f18c-144">步驟 3.</span><span class="sxs-lookup"><span data-stu-id="9f18c-144">Step 3.</span></span> <span data-ttu-id="9f18c-145">建立 ExpressRoute 線路</span><span class="sxs-lookup"><span data-stu-id="9f18c-145">Create an ExpressRoute circuit</span></span>
<span data-ttu-id="9f18c-146">hello 下列範例示範透過在美國矽谷 Equinix toocreate 200 Mbps ExpressRoute 電路的方式。</span><span class="sxs-lookup"><span data-stu-id="9f18c-146">hello following example shows how toocreate a 200-Mbps ExpressRoute circuit through Equinix in Silicon Valley.</span></span> <span data-ttu-id="9f18c-147">如果您使用不同的提供者和不同的設定，請在您提出要求時替換成該資訊。</span><span class="sxs-lookup"><span data-stu-id="9f18c-147">If you're using a different provider and different settings, substitute that information when you make your request.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9f18c-148">ExpressRoute 電路將計費 hello 發出服務金鑰的時間。</span><span class="sxs-lookup"><span data-stu-id="9f18c-148">Your ExpressRoute circuit will be billed from hello moment a service key is issued.</span></span> <span data-ttu-id="9f18c-149">請確定您執行此作業，準備好 tooprovision hello 電路 hello 連線服務提供者時。</span><span class="sxs-lookup"><span data-stu-id="9f18c-149">Ensure that you perform this operation when hello connectivity provider is ready tooprovision hello circuit.</span></span>
> 
> 

<span data-ttu-id="9f18c-150">hello 下面是新的服務金鑰的要求範例：</span><span class="sxs-lookup"><span data-stu-id="9f18c-150">hello following is an example request for a new service key:</span></span>

    $Bandwidth = 200
    $CircuitName = "MyTestCircuit"
    $ServiceProvider = "Equinix"
    $Location = "Silicon Valley"

    New-AzureDedicatedCircuit -CircuitName $CircuitName -ServiceProviderName $ServiceProvider -Bandwidth $Bandwidth -Location $Location -sku Standard -BillingType MeteredData

<span data-ttu-id="9f18c-151">或者，如果您想 toocreate ExpressRoute 電路 hello 高階的附加元件，使用 hello 下列範例。</span><span class="sxs-lookup"><span data-stu-id="9f18c-151">Or, if you want toocreate an ExpressRoute circuit with hello premium add-on, use hello following example.</span></span> <span data-ttu-id="9f18c-152">請參閱 toohello [ExpressRoute 常見問題集](expressroute-faqs.md)如需詳細資訊 hello premium 附加元件。</span><span class="sxs-lookup"><span data-stu-id="9f18c-152">Refer toohello [ExpressRoute FAQ](expressroute-faqs.md) for more details about hello premium add-on.</span></span>

    New-AzureDedicatedCircuit -CircuitName $CircuitName -ServiceProviderName $ServiceProvider -Bandwidth $Bandwidth -Location $Location -sku Premium - BillingType MeteredData


<span data-ttu-id="9f18c-153">hello 回應會包含 hello 服務金鑰。</span><span class="sxs-lookup"><span data-stu-id="9f18c-153">hello response will contain hello service key.</span></span> <span data-ttu-id="9f18c-154">您可以取得所有 hello 參數的詳細的描述執行 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="9f18c-154">You can get detailed descriptions of all hello parameters by running hello following:</span></span>

    get-help new-azurededicatedcircuit -detailed

### <a name="step-4-list-all-hello-expressroute-circuits"></a><span data-ttu-id="9f18c-155">步驟 4.</span><span class="sxs-lookup"><span data-stu-id="9f18c-155">Step 4.</span></span> <span data-ttu-id="9f18c-156">列出所有的 hello ExpressRoute 電路</span><span class="sxs-lookup"><span data-stu-id="9f18c-156">List all hello ExpressRoute circuits</span></span>
<span data-ttu-id="9f18c-157">您可以執行 hello `Get-AzureDedicatedCircuit` tooget 所有清單 hello 您建立 ExpressRoute 電路的命令：</span><span class="sxs-lookup"><span data-stu-id="9f18c-157">You can run hello `Get-AzureDedicatedCircuit` command tooget a list of all hello ExpressRoute circuits that you created:</span></span>

    Get-AzureDedicatedCircuit

<span data-ttu-id="9f18c-158">hello 回應將類似下列範例的 toohello:</span><span class="sxs-lookup"><span data-stu-id="9f18c-158">hello response will be something similar toohello following example:</span></span>

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : NotProvisioned
    Sku                              : Standard
    Status                           : Enabled

<span data-ttu-id="9f18c-159">您可以擷取這項資訊在任何時候使用 hello `Get-AzureDedicatedCircuit` cmdlet。</span><span class="sxs-lookup"><span data-stu-id="9f18c-159">You can retrieve this information at any time by using hello `Get-AzureDedicatedCircuit` cmdlet.</span></span> <span data-ttu-id="9f18c-160">進行呼叫不含任何參數的 hello 列出 hello 的所有電路。</span><span class="sxs-lookup"><span data-stu-id="9f18c-160">Making hello call without any parameters lists all hello circuits.</span></span> <span data-ttu-id="9f18c-161">您的服務金鑰將會列在 hello *ServiceKey*欄位。</span><span class="sxs-lookup"><span data-stu-id="9f18c-161">Your service key will be listed in hello *ServiceKey* field.</span></span>

    Get-AzureDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : NotProvisioned
    Sku                              : Standard
    Status                           : Enabled

<span data-ttu-id="9f18c-162">您可以取得所有 hello 參數的詳細的描述執行 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="9f18c-162">You can get detailed descriptions of all hello parameters by running hello following:</span></span>

    get-help get-azurededicatedcircuit -detailed

### <a name="step-5-send-hello-service-key-tooyour-connectivity-provider-for-provisioning"></a><span data-ttu-id="9f18c-163">步驟 5。</span><span class="sxs-lookup"><span data-stu-id="9f18c-163">Step 5.</span></span> <span data-ttu-id="9f18c-164">佈建傳送嗨服務金鑰 tooyour 連線服務提供者</span><span class="sxs-lookup"><span data-stu-id="9f18c-164">Send hello service key tooyour connectivity provider for provisioning</span></span>
<span data-ttu-id="9f18c-165">*ServiceProviderProvisioningState*提供 hello 的佈建 hello 服務提供者端的目前狀態的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="9f18c-165">*ServiceProviderProvisioningState* provides information on hello current state of provisioning on hello service-provider side.</span></span> <span data-ttu-id="9f18c-166">*狀態*hello Microsoft 側邊提供 hello 狀態。</span><span class="sxs-lookup"><span data-stu-id="9f18c-166">*Status* provides hello state on hello Microsoft side.</span></span> <span data-ttu-id="9f18c-167">如需循環的佈建狀態的詳細資訊，請參閱 hello[工作流程](expressroute-workflows.md#expressroute-circuit-provisioning-states)發行項。</span><span class="sxs-lookup"><span data-stu-id="9f18c-167">For more information about circuit provisioning states, see hello [Workflows](expressroute-workflows.md#expressroute-circuit-provisioning-states) article.</span></span>

<span data-ttu-id="9f18c-168">當您建立新的 ExpressRoute 電路時，hello 電路將處於下列狀態的 hello:</span><span class="sxs-lookup"><span data-stu-id="9f18c-168">When you create a new ExpressRoute circuit, hello circuit will be in hello following state:</span></span>

    ServiceProviderProvisioningState : NotProvisioned
    Status                           : Enabled


<span data-ttu-id="9f18c-169">hello 電路將會移 toohello hello 連線服務提供者會在您啟用的 hello 程序中時，下列狀態：</span><span class="sxs-lookup"><span data-stu-id="9f18c-169">hello circuit will go toohello following state when hello connectivity provider is in hello process of enabling it for you:</span></span>

    ServiceProviderProvisioningState : Provisioning
    Status                           : Enabled

<span data-ttu-id="9f18c-170">ExpressRoute 電路必須遵循您 toobe 無法 toouse 狀態 hello 它：</span><span class="sxs-lookup"><span data-stu-id="9f18c-170">An ExpressRoute circuit must be in hello following state for you toobe able toouse it:</span></span>

    ServiceProviderProvisioningState : Provisioned
    Status                           : Enabled


### <a name="step-6-periodically-check-hello-status-and-hello-state-of-hello-circuit-key"></a><span data-ttu-id="9f18c-171">步驟 6.</span><span class="sxs-lookup"><span data-stu-id="9f18c-171">Step 6.</span></span> <span data-ttu-id="9f18c-172">定期檢查 hello 狀態和 hello 循環索引鍵 hello 狀態</span><span class="sxs-lookup"><span data-stu-id="9f18c-172">Periodically check hello status and hello state of hello circuit key</span></span>
<span data-ttu-id="9f18c-173">這樣可讓您知道提供者何時已啟用您的線路。</span><span class="sxs-lookup"><span data-stu-id="9f18c-173">This lets you know when your provider has enabled your circuit.</span></span> <span data-ttu-id="9f18c-174">在設定 hello 循環之後， *ServiceProviderProvisioningState*將會顯示為*已佈建*hello 下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="9f18c-174">After hello circuit has been configured, *ServiceProviderProvisioningState* will display as *Provisioned* as shown in hello following example:</span></span>

    Get-AzureDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

### <a name="step-7-create-your-routing-configuration"></a><span data-ttu-id="9f18c-175">步驟 7.</span><span class="sxs-lookup"><span data-stu-id="9f18c-175">Step 7.</span></span> <span data-ttu-id="9f18c-176">建立路由組態</span><span class="sxs-lookup"><span data-stu-id="9f18c-176">Create your routing configuration</span></span>
<span data-ttu-id="9f18c-177">請參閱 toohello [ExpressRoute 電路的路由組態 （建立和修改電路的互連）](expressroute-howto-routing-classic.md)文件以取得逐步指示。</span><span class="sxs-lookup"><span data-stu-id="9f18c-177">Refer toohello [ExpressRoute circuit routing configuration (create and modify circuit peerings)](expressroute-howto-routing-classic.md) article for step-by-step instructions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9f18c-178">這些說明僅適用於 toocircuits 與提供層級 2 連線服務的服務提供者所建立。</span><span class="sxs-lookup"><span data-stu-id="9f18c-178">These instructions only apply toocircuits that are created with service providers that offer layer 2 connectivity services.</span></span> <span data-ttu-id="9f18c-179">如果您使用的服務提供者是提供受管理的第 3 層服務 (通常是 IP VPN，如 MPLS)，您的連線提供者會為您設定和管理路由。</span><span class="sxs-lookup"><span data-stu-id="9f18c-179">If you're using a service provider that offers managed layer 3 services (typically an IP VPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>
> 
> 

### <a name="step-8-link-a-virtual-network-tooan-expressroute-circuit"></a><span data-ttu-id="9f18c-180">步驟 8。</span><span class="sxs-lookup"><span data-stu-id="9f18c-180">Step 8.</span></span> <span data-ttu-id="9f18c-181">連結虛擬網路 tooan ExpressRoute 電路</span><span class="sxs-lookup"><span data-stu-id="9f18c-181">Link a virtual network tooan ExpressRoute circuit</span></span>
<span data-ttu-id="9f18c-182">接下來，將虛擬網路 tooyour ExpressRoute 電路的連結。</span><span class="sxs-lookup"><span data-stu-id="9f18c-182">Next, link a virtual network tooyour ExpressRoute circuit.</span></span> <span data-ttu-id="9f18c-183">請參閱太[連結 ExpressRoute 電路 toovirtual 網路](expressroute-howto-linkvnet-classic.md)如需逐步指示。</span><span class="sxs-lookup"><span data-stu-id="9f18c-183">Refer too[Linking ExpressRoute circuits toovirtual networks](expressroute-howto-linkvnet-classic.md) for step-by-step instructions.</span></span> <span data-ttu-id="9f18c-184">如果您需要 toocreate hello 傳統部署模型使用 expressroute 的虛擬網路，請參閱[建立 expressroute 的虛擬網路](expressroute-howto-vnet-portal-classic.md)。</span><span class="sxs-lookup"><span data-stu-id="9f18c-184">If you need toocreate a virtual network using hello classic deployment model for ExpressRoute, see [Create a virtual network for ExpressRoute](expressroute-howto-vnet-portal-classic.md).</span></span>

## <a name="getting-hello-status-of-an-expressroute-circuit"></a><span data-ttu-id="9f18c-185">取得 hello 狀態的 ExpressRoute 電路</span><span class="sxs-lookup"><span data-stu-id="9f18c-185">Getting hello status of an ExpressRoute circuit</span></span>
<span data-ttu-id="9f18c-186">您可以擷取這項資訊在任何時候使用 hello `Get-AzureCircuit` cmdlet。</span><span class="sxs-lookup"><span data-stu-id="9f18c-186">You can retrieve this information at any time by using hello `Get-AzureCircuit` cmdlet.</span></span> <span data-ttu-id="9f18c-187">進行呼叫不含任何參數的 hello 列出 hello 的所有電路。</span><span class="sxs-lookup"><span data-stu-id="9f18c-187">Making hello call without any parameters lists all hello circuits.</span></span>

    Get-AzureDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

    Bandwidth                        : 1000
    CircuitName                      : MyAsiaCircuit
    Location                         : Singapore
    ServiceKey                       : #################################
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

<span data-ttu-id="9f18c-188">您可以傳遞做為參數 toohello 呼叫 hello 服務金鑰，以取得特定的 ExpressRoute 電路的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="9f18c-188">You can get information on a specific ExpressRoute circuit by passing hello service key as a parameter toohello call.</span></span>

    Get-AzureDedicatedCircuit -ServiceKey "*********************************"

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled


<span data-ttu-id="9f18c-189">您可以藉由執行下列範例中的 hello 取得所有 hello 參數的詳細的說明：</span><span class="sxs-lookup"><span data-stu-id="9f18c-189">You can get detailed descriptions of all hello parameters by running hello following example:</span></span>

    get-help get-azurededicatedcircuit -detailed

## <a name="modifying-an-expressroute-circuit"></a><span data-ttu-id="9f18c-190">修改 ExpressRoute 線路</span><span class="sxs-lookup"><span data-stu-id="9f18c-190">Modifying an ExpressRoute circuit</span></span>
<span data-ttu-id="9f18c-191">您可以修改 ExpressRoute 線路的某些屬性，而不會影響連線。</span><span class="sxs-lookup"><span data-stu-id="9f18c-191">You can modify certain properties of an ExpressRoute circuit without impacting connectivity.</span></span>

<span data-ttu-id="9f18c-192">您可以 hello 遵循不中斷的情況：</span><span class="sxs-lookup"><span data-stu-id="9f18c-192">You can do hello following with no downtime:</span></span>

* <span data-ttu-id="9f18c-193">啟用或停用 ExpressRoute 線路的 ExpressRoute 進階附加元件。</span><span class="sxs-lookup"><span data-stu-id="9f18c-193">Enable or disable an ExpressRoute premium add-on for your ExpressRoute circuit.</span></span>
* <span data-ttu-id="9f18c-194">增加 hello 頻寬的 ExpressRoute 電路提供 hello 連接埠的容量不足。</span><span class="sxs-lookup"><span data-stu-id="9f18c-194">Increase hello bandwidth of your ExpressRoute circuit provided there is capacity available on hello port.</span></span> <span data-ttu-id="9f18c-195">請注意，不支援降級 hello 電路頻寬。</span><span class="sxs-lookup"><span data-stu-id="9f18c-195">Note that downgrading hello bandwidth of a circuit is not supported.</span></span> 
* <span data-ttu-id="9f18c-196">變更計量計劃的計量資料 tooUnlimited 資料 hello。</span><span class="sxs-lookup"><span data-stu-id="9f18c-196">Change hello metering plan from Metered Data tooUnlimited Data.</span></span> <span data-ttu-id="9f18c-197">請注意該變更 hello 計量計劃從無限制的資料 tooMetered 不支援資料。</span><span class="sxs-lookup"><span data-stu-id="9f18c-197">Note that changing hello metering plan from Unlimited Data tooMetered Data is not supported.</span></span>
* <span data-ttu-id="9f18c-198">您可以啟用和停用 [允許傳統作業]。</span><span class="sxs-lookup"><span data-stu-id="9f18c-198">You can enable and disable *Allow Classic Operations*.</span></span>

<span data-ttu-id="9f18c-199">請參閱 toohello [ExpressRoute 常見問題集](expressroute-faqs.md)如需有關限制和限制。</span><span class="sxs-lookup"><span data-stu-id="9f18c-199">Refer toohello [ExpressRoute FAQ](expressroute-faqs.md) for more information on limits and limitations.</span></span>

### <a name="tooenable-hello-expressroute-premium-add-on"></a><span data-ttu-id="9f18c-200">tooenable hello ExpressRoute 高階的附加元件</span><span class="sxs-lookup"><span data-stu-id="9f18c-200">tooenable hello ExpressRoute premium add-on</span></span>
<span data-ttu-id="9f18c-201">您可以使用下列 PowerShell cmdlet 的 hello，為您現有的電路啟用 hello ExpressRoute premium add-on:</span><span class="sxs-lookup"><span data-stu-id="9f18c-201">You can enable hello ExpressRoute premium add-on for your existing circuit by using hello following PowerShell cmdlet:</span></span>

    Set-AzureDedicatedCircuitProperties -ServiceKey "*********************************" -Sku Premium

    Bandwidth                        : 1000
    CircuitName                      : TestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Premium
    Status                           : Enabled

<span data-ttu-id="9f18c-202">您的電路現在會有 hello ExpressRoute 高階附加元件功能已啟用。</span><span class="sxs-lookup"><span data-stu-id="9f18c-202">Your circuit will now have hello ExpressRoute premium add-on features enabled.</span></span> <span data-ttu-id="9f18c-203">請注意，我們就會啟動 hello 命令已順利執行完成後，只要您計費 hello premium 附加元件的功能。</span><span class="sxs-lookup"><span data-stu-id="9f18c-203">Note that we will start billing you for hello premium add-on capability as soon as hello command has successfully run.</span></span>

### <a name="toodisable-hello-expressroute-premium-add-on"></a><span data-ttu-id="9f18c-204">toodisable hello ExpressRoute 高階的附加元件</span><span class="sxs-lookup"><span data-stu-id="9f18c-204">toodisable hello ExpressRoute premium add-on</span></span>
> [!IMPORTANT]
> <span data-ttu-id="9f18c-205">如果您使用大於 hello 標準循環所允許的資源，這項作業可能會失敗。</span><span class="sxs-lookup"><span data-stu-id="9f18c-205">This operation can fail if you're using resources that are greater than what is permitted for hello standard circuit.</span></span>
> 
> 

#### <a name="considerations"></a><span data-ttu-id="9f18c-206">考量</span><span class="sxs-lookup"><span data-stu-id="9f18c-206">Considerations</span></span>

* <span data-ttu-id="9f18c-207">您必須確定虛擬網路連結的 toohello 循環的 hello 數目小於 10 之前您從 premium toostandard 降級。</span><span class="sxs-lookup"><span data-stu-id="9f18c-207">You must ensure that hello number of virtual networks linked toohello circuit is less than 10 before you downgrade from premium toostandard.</span></span> <span data-ttu-id="9f18c-208">如果不這麼做，您的更新要求會失敗，，您可以使用票據的 hello 高階費率。</span><span class="sxs-lookup"><span data-stu-id="9f18c-208">If you don't do this, your update request will fail, and you'll be billed hello premium rates.</span></span>
* <span data-ttu-id="9f18c-209">您必須取消連結其他地理政治區域中的所有虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="9f18c-209">You must unlink all virtual networks in other geopolitical regions.</span></span> <span data-ttu-id="9f18c-210">如果不這麼做，您的更新要求會失敗，，您可以使用票據的 hello 高階費率。</span><span class="sxs-lookup"><span data-stu-id="9f18c-210">If you don't do this, your update request will fail, and you'll be billed hello premium rates.</span></span>
* <span data-ttu-id="9f18c-211">就私用對等設定而言，路由表必須少於 4000 個路由。</span><span class="sxs-lookup"><span data-stu-id="9f18c-211">Your route table must be less than 4,000 routes for private peering.</span></span> <span data-ttu-id="9f18c-212">如果您的路由表的大小大於 4000 路由，hello BGP 工作階段會卸除，並不會重新啟用，直到 hello 公告的首碼數目，低於 4000。</span><span class="sxs-lookup"><span data-stu-id="9f18c-212">If your route table size is greater than 4,000 routes, hello BGP session will drop and won't be reenabled until hello number of advertised prefixes goes below 4,000.</span></span>

#### <a name="disable-hello-premium-add-on"></a><span data-ttu-id="9f18c-213">停用 hello premium 附加元件</span><span class="sxs-lookup"><span data-stu-id="9f18c-213">Disable hello premium add-on</span></span>
<span data-ttu-id="9f18c-214">您可以使用下列 PowerShell cmdlet 的 hello 停用 hello ExpressRoute premium add-on 您現有的循環：</span><span class="sxs-lookup"><span data-stu-id="9f18c-214">You can disable hello ExpressRoute premium add-on for your existing circuit by using hello following PowerShell cmdlet:</span></span>

    Set-AzureDedicatedCircuitProperties -ServiceKey "*********************************" -Sku Standard

    Bandwidth                        : 1000
    CircuitName                      : TestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled



### <a name="tooupdate-hello-expressroute-circuit-bandwidth"></a><span data-ttu-id="9f18c-215">tooupdate hello ExpressRoute 電路頻寬</span><span class="sxs-lookup"><span data-stu-id="9f18c-215">tooupdate hello ExpressRoute circuit bandwidth</span></span>
<span data-ttu-id="9f18c-216">檢查 hello [ExpressRoute 常見問題集](expressroute-faqs.md)支援您的提供者的頻寬選項。</span><span class="sxs-lookup"><span data-stu-id="9f18c-216">Check hello [ExpressRoute FAQ](expressroute-faqs.md) for supported bandwidth options for your provider.</span></span> <span data-ttu-id="9f18c-217">您可以選擇大於您現有的循環 hello 大小，只要 hello （您的電路建立所在） 的實體連接埠可讓任何規模。</span><span class="sxs-lookup"><span data-stu-id="9f18c-217">You can pick any size that is greater than hello size of your existing circuit as long as hello physical port (on which your circuit is created) allows.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9f18c-218">如果 hello 現有的連接埠上有足夠的容量，您可能必須 toorecreate hello ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="9f18c-218">You may have toorecreate hello ExpressRoute circuit if there is inadequate capacity on hello existing port.</span></span> <span data-ttu-id="9f18c-219">如果沒有任何額外的容量可在該位置，您無法升級 hello 循環。</span><span class="sxs-lookup"><span data-stu-id="9f18c-219">You cannot upgrade hello circuit if there is no additional capacity available at that location.</span></span>
>
> <span data-ttu-id="9f18c-220">您無法減少 hello 頻寬的 ExpressRoute 電路不會中斷。</span><span class="sxs-lookup"><span data-stu-id="9f18c-220">You cannot reduce hello bandwidth of an ExpressRoute circuit without disruption.</span></span> <span data-ttu-id="9f18c-221">降級頻寬 toodeprovision hello ExpressRoute 循環會要求您，並再重新佈建新增的 ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="9f18c-221">Downgrading bandwidth requires you toodeprovision hello ExpressRoute circuit and then reprovision a new ExpressRoute circuit.</span></span>
> 
> 

#### <a name="resize-a-circuit"></a><span data-ttu-id="9f18c-222">調整電路大小</span><span class="sxs-lookup"><span data-stu-id="9f18c-222">Resize a circuit</span></span>

<span data-ttu-id="9f18c-223">決定您需要的大小之後，您可以使用下列命令 tooresize hello 您的循環：</span><span class="sxs-lookup"><span data-stu-id="9f18c-223">After you decide what size you need, you can use hello following command tooresize your circuit:</span></span>

    Set-AzureDedicatedCircuitProperties -ServiceKey ********************************* -Bandwidth 1000

    Bandwidth                        : 1000
    CircuitName                      : TestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

<span data-ttu-id="9f18c-224">您的電路將具有已調整大小 hello Microsoft 一邊。</span><span class="sxs-lookup"><span data-stu-id="9f18c-224">Your circuit will have been sized up on hello Microsoft side.</span></span> <span data-ttu-id="9f18c-225">您必須連絡其端 toomatch 您連接的提供者 tooupdate 設定這項變更。</span><span class="sxs-lookup"><span data-stu-id="9f18c-225">You must contact your connectivity provider tooupdate configurations on their side toomatch this change.</span></span> <span data-ttu-id="9f18c-226">請注意，我們將會開始計費您 hello 更新從這個點的頻寬選項上。</span><span class="sxs-lookup"><span data-stu-id="9f18c-226">Note that we will start billing you for hello updated bandwidth option from this point on.</span></span>

<span data-ttu-id="9f18c-227">如果您看到下列錯誤，當增加 hello 電路頻寬的 hello，這表示那里 hello 您現有的電路建立所在的實體連接埠上保留足夠的頻寬。</span><span class="sxs-lookup"><span data-stu-id="9f18c-227">If you see hello following error when increasing hello circuit bandwidth, it means there is no sufficient bandwidth left on hello physical port where your existing circuit is created.</span></span> <span data-ttu-id="9f18c-228">您有 toodelete 這個循環，並建立新的循環，您需要的 hello 大小。</span><span class="sxs-lookup"><span data-stu-id="9f18c-228">You have toodelete this circuit and create a new circuit of hello size you need.</span></span> 

    Set-AzureDedicatedCircuitProperties : InvalidOperation : Insufficient bandwidth available tooperform this circuit
    update operation
    At line:1 char:1
    + Set-AzureDedicatedCircuitProperties -ServiceKey ********************* ...
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : CloseError: (:) [Set-AzureDedicatedCircuitProperties], CloudException
        + FullyQualifiedErrorId : Microsoft.WindowsAzure.Commands.ExpressRoute.SetAzureDedicatedCircuitPropertiesCommand


## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a><span data-ttu-id="9f18c-229">取消佈建和刪除 ExpressRoute 線路</span><span class="sxs-lookup"><span data-stu-id="9f18c-229">Deprovisioning and deleting an ExpressRoute circuit</span></span>

### <a name="considerations"></a><span data-ttu-id="9f18c-230">考量</span><span class="sxs-lookup"><span data-stu-id="9f18c-230">Considerations</span></span>

* <span data-ttu-id="9f18c-231">您必須取消連結從 hello 這個作業 toosucceed 的 ExpressRoute 電路的所有虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="9f18c-231">You must unlink all virtual networks from hello ExpressRoute circuit for this operation toosucceed.</span></span> <span data-ttu-id="9f18c-232">請檢查 toosee，如果您有任何虛擬網路連結 toohello 循環，如果此作業會失敗。</span><span class="sxs-lookup"><span data-stu-id="9f18c-232">Check toosee if you have any virtual networks that are linked toohello circuit if this operation fails.</span></span>
* <span data-ttu-id="9f18c-233">如果 hello ExpressRoute 電路服務提供者佈建狀態為**佈建**或**已佈建**您必須使用您的服務提供者 toodeprovision hello 電路邊。</span><span class="sxs-lookup"><span data-stu-id="9f18c-233">If hello ExpressRoute circuit service provider provisioning state is **Provisioning** or **Provisioned** you must work with your service provider toodeprovision hello circuit on their side.</span></span> <span data-ttu-id="9f18c-234">我們將繼續 tooreserve 資源，並向您收取費用，直到完成取消佈建 hello 電路 hello 服務提供者，並通知我們。</span><span class="sxs-lookup"><span data-stu-id="9f18c-234">We will continue tooreserve resources and bill you until hello service provider completes deprovisioning hello circuit and notifies us.</span></span>
* <span data-ttu-id="9f18c-235">如果 hello 服務提供者已解除佈建 hello 循環 (hello 佈建狀態的服務提供者設定得**未佈建**) 可接著刪除 hello 循環。</span><span class="sxs-lookup"><span data-stu-id="9f18c-235">If hello service provider has deprovisioned hello circuit (hello service provider provisioning state is set too**Not provisioned**) you can then delete hello circuit.</span></span> <span data-ttu-id="9f18c-236">這樣會停止計費 hello 循環。</span><span class="sxs-lookup"><span data-stu-id="9f18c-236">This will stop billing for hello circuit.</span></span>

#### <a name="delete-a-circuit"></a><span data-ttu-id="9f18c-237">刪除電路</span><span class="sxs-lookup"><span data-stu-id="9f18c-237">Delete a circuit</span></span>

<span data-ttu-id="9f18c-238">若要刪除 ExpressRoute 電路，您可以執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="9f18c-238">You can delete your ExpressRoute circuit by running hello following command:</span></span>

    Remove-AzureDedicatedCircuit -ServiceKey "*********************************"



## <a name="next-steps"></a><span data-ttu-id="9f18c-239">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9f18c-239">Next steps</span></span>
<span data-ttu-id="9f18c-240">建立您的循環之後，請確定您執行 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="9f18c-240">After you create your circuit, make sure that you do hello following:</span></span>

* [<span data-ttu-id="9f18c-241">建立和修改 ExpressRoute 線路的路由</span><span class="sxs-lookup"><span data-stu-id="9f18c-241">Create and modify routing for your ExpressRoute circuit</span></span>](expressroute-howto-routing-classic.md)
* [<span data-ttu-id="9f18c-242">連結您的虛擬網路 tooyour ExpressRoute 電路</span><span class="sxs-lookup"><span data-stu-id="9f18c-242">Link your virtual network tooyour ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-classic.md)

