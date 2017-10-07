---
title: "aaaMigrate tooResource 管理員使用 PowerShell |Microsoft 文件"
description: "本文逐步 hello 平台支援移轉的 IaaS 資源，例如虛擬機器 (Vm)、 虛擬網路 (Vnet) 和儲存體帳戶從傳統 tooAzure 資源管理員 (ARM) 可以使用 Azure PowerShell 命令"
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 2b3dff9b-2e99-4556-acc5-d75ef234af9c
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: kasing
ms.openlocfilehash: b5b2987da292f1c241be71a354b0c2e1a96a07c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-iaas-resources-from-classic-tooazure-resource-manager-by-using-azure-powershell"></a><span data-ttu-id="898df-103">使用 Azure PowerShell，從傳統 tooAzure 資源管理員移轉 IaaS 資源</span><span class="sxs-lookup"><span data-stu-id="898df-103">Migrate IaaS resources from classic tooAzure Resource Manager by using Azure PowerShell</span></span>
<span data-ttu-id="898df-104">這些步驟顯示如何 toouse Azure PowerShell 命令為從 hello 傳統部署模型 toohello Azure Resource Manager 部署模型的服務 (IaaS) 資源的 toomigrate 基礎結構。</span><span class="sxs-lookup"><span data-stu-id="898df-104">These steps show you how toouse Azure PowerShell commands toomigrate infrastructure as a service (IaaS) resources from hello classic deployment model toohello Azure Resource Manager deployment model.</span></span>

<span data-ttu-id="898df-105">如果您想，您也可以移轉的資源使用 hello [Azure 命令列介面 (Azure CLI)](../linux/migration-classic-resource-manager-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="898df-105">If you want, you can also migrate resources by using hello [Azure Command Line Interface (Azure CLI)](../linux/migration-classic-resource-manager-cli.md).</span></span>

* <span data-ttu-id="898df-106">如需有關支援的移轉案例的背景，請參閱[平台支援移轉的 IaaS 資源從資源管理員的傳統 tooAzure](migration-classic-resource-manager-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="898df-106">For background on supported migration scenarios, see [Platform-supported migration of IaaS resources from classic tooAzure Resource Manager](migration-classic-resource-manager-overview.md).</span></span>
* <span data-ttu-id="898df-107">如需詳細的指引和移轉的逐步解說，請參閱[技術的深入剖析平台支援移轉從傳統 tooAzure 資源管理員](migration-classic-resource-manager-deep-dive.md)。</span><span class="sxs-lookup"><span data-stu-id="898df-107">For detailed guidance and a migration walkthrough, see [Technical deep dive on platform-supported migration from classic tooAzure Resource Manager](migration-classic-resource-manager-deep-dive.md).</span></span>
* [<span data-ttu-id="898df-108">檢閱最常見的移轉錯誤</span><span class="sxs-lookup"><span data-stu-id="898df-108">Review most common migration errors</span></span>](migration-classic-resource-manager-errors.md)

<br>
<span data-ttu-id="898df-109">以下是步驟需要執行移轉程序期間 toobe 流程圖 tooidentify hello 順序</span><span class="sxs-lookup"><span data-stu-id="898df-109">Here is a flowchart tooidentify hello order in which steps need toobe executed during a migration process</span></span>

![螢幕擷取畫面顯示 hello 移轉步驟](media/migration-classic-resource-manager/migration-flow.png)

## <a name="step-1-plan-for-migration"></a><span data-ttu-id="898df-111">步驟 1︰為移轉做規劃</span><span class="sxs-lookup"><span data-stu-id="898df-111">Step 1: Plan for migration</span></span>
<span data-ttu-id="898df-112">以下是我們建議您在評估從傳統 tooResource Manager 移轉的 IaaS 資源的一些最佳作法：</span><span class="sxs-lookup"><span data-stu-id="898df-112">Here are a few best practices that we recommend as you evaluate migrating IaaS resources from classic tooResource Manager:</span></span>

* <span data-ttu-id="898df-113">閱讀 hello[支援和不支援的功能和設定](migration-classic-resource-manager-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="898df-113">Read through hello [supported and unsupported features and configurations](migration-classic-resource-manager-overview.md).</span></span> <span data-ttu-id="898df-114">如果您有使用不支援的設定或功能的虛擬機器，我們建議您等候 hello 設定/功能支援 toobe 宣布。</span><span class="sxs-lookup"><span data-stu-id="898df-114">If you have virtual machines that use unsupported configurations or features, we recommend that you wait for hello configuration/feature support toobe announced.</span></span> <span data-ttu-id="898df-115">或者，如果其符合您的需求時，移除該功能，或移出該設定 tooenable 移轉。</span><span class="sxs-lookup"><span data-stu-id="898df-115">Alternatively, if it suits your needs, remove that feature or move out of that configuration tooenable migration.</span></span>
* <span data-ttu-id="898df-116">如果您有自動化部署基礎結構和應用程式目前的指令碼，請使用這些指令碼移轉嘗試 toocreate 類似的測試設定。</span><span class="sxs-lookup"><span data-stu-id="898df-116">If you have automated scripts that deploy your infrastructure and applications today, try toocreate a similar test setup by using those scripts for migration.</span></span> <span data-ttu-id="898df-117">或者，您可以設定範例環境使用 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="898df-117">Alternatively, you can set up sample environments by using hello Azure portal.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="898df-118">從傳統 tooResource Manager 移轉目前不支援應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="898df-118">Application Gateways are not currently supported for migration from classic tooResource Manager.</span></span> <span data-ttu-id="898df-119">toomigrate 傳統虛擬網路與應用程式閘道，執行準備作業 toomove hello 網路之前先移除 hello 閘道。</span><span class="sxs-lookup"><span data-stu-id="898df-119">toomigrate a classic virtual network with an Application gateway, remove hello gateway before running a Prepare operation toomove hello network.</span></span> <span data-ttu-id="898df-120">Hello 移轉完成之後，重新連接 hello 閘道 Azure 資源管理員中。</span><span class="sxs-lookup"><span data-stu-id="898df-120">After you complete hello migration, reconnect hello gateway in Azure Resource Manager.</span></span>
>
><span data-ttu-id="898df-121">ExpressRoute 閘道連接 tooExpressRoute 電路，另一個訂用帳戶中的不會自動移轉。</span><span class="sxs-lookup"><span data-stu-id="898df-121">ExpressRoute gateways connecting tooExpressRoute circuits in another subscription cannot be migrated automatically.</span></span> <span data-ttu-id="898df-122">在這種情況下，移除 hello ExpressRoute 閘道、 hello 虛擬網路移轉並重新建立 hello 閘道。</span><span class="sxs-lookup"><span data-stu-id="898df-122">In such cases, remove hello ExpressRoute gateway, migrate hello virtual network and recreate hello gateway.</span></span> <span data-ttu-id="898df-123">請參閱[移轉 ExpressRoute 電路和相關聯的虛擬網路與 hello 傳統 toohello Resource Manager 部署模型](../../expressroute/expressroute-migration-classic-resource-manager.md)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="898df-123">Please see [Migrate ExpressRoute circuits and associated virtual networks from hello classic toohello Resource Manager deployment model](../../expressroute/expressroute-migration-classic-resource-manager.md) for more information.</span></span>
>
>

## <a name="step-2-install-hello-latest-version-of-azure-powershell"></a><span data-ttu-id="898df-124">步驟 2： 安裝 Azure PowerShell hello 最新版本</span><span class="sxs-lookup"><span data-stu-id="898df-124">Step 2: Install hello latest version of Azure PowerShell</span></span>
<span data-ttu-id="898df-125">有兩個主要選項 tooinstall Azure PowerShell: [PowerShell 資源庫](https://www.powershellgallery.com/profiles/azure-sdk/)或[Web Platform Installer (WebPI)](http://aka.ms/webpi-azps)。</span><span class="sxs-lookup"><span data-stu-id="898df-125">There are two main options tooinstall Azure PowerShell: [PowerShell Gallery](https://www.powershellgallery.com/profiles/azure-sdk/) or [Web Platform Installer (WebPI)](http://aka.ms/webpi-azps).</span></span> <span data-ttu-id="898df-126">WebPI 接收每月更新。</span><span class="sxs-lookup"><span data-stu-id="898df-126">WebPI receives monthly updates.</span></span> <span data-ttu-id="898df-127">PowerShell 資源庫則是持續接收更新。</span><span class="sxs-lookup"><span data-stu-id="898df-127">PowerShell Gallery receives updates on a continuous basis.</span></span> <span data-ttu-id="898df-128">本文是以 Azure PowerShell 2.1.0 為基礎。</span><span class="sxs-lookup"><span data-stu-id="898df-128">This article is based on Azure PowerShell version 2.1.0.</span></span>

<span data-ttu-id="898df-129">如需安裝指示，請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="898df-129">For installation instructions, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<br>

## <a name="step-3-ensure-that-you-are-an-administrator-for-hello-subscription-in-azure-portal"></a><span data-ttu-id="898df-130">步驟 3： 確定您在 Azure 入口網站是 hello 訂用帳戶的系統管理員</span><span class="sxs-lookup"><span data-stu-id="898df-130">Step 3: Ensure that you are an administrator for hello subscription in Azure portal</span></span>
<span data-ttu-id="898df-131">tooperform 這個移轉中，您必須新增為共同管理員的 hello hello 訂用帳戶[Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="898df-131">tooperform this migration, you must be added as a co-administrator for hello subscription in hello [Azure portal](https://portal.azure.com).</span></span>

1. <span data-ttu-id="898df-132">登入 hello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="898df-132">Sign into hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="898df-133">在 hello 中樞功能表中，選取 **訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="898df-133">On hello Hub menu, select **Subscription**.</span></span> <span data-ttu-id="898df-134">如果您沒有看到，請選取 [更多服務]。</span><span class="sxs-lookup"><span data-stu-id="898df-134">If you don't see it, select **More services**.</span></span>
3. <span data-ttu-id="898df-135">尋找 hello 適當的訂閱項目，然後查看 hello **MY ROLE**欄位。</span><span class="sxs-lookup"><span data-stu-id="898df-135">Find hello appropriate subscription entry, then look at hello **MY ROLE** field.</span></span> <span data-ttu-id="898df-136">共同管理員，hello 值應該是_帳戶管理員_。</span><span class="sxs-lookup"><span data-stu-id="898df-136">For a co-administrator, hello value should be _Account admin_.</span></span>

<span data-ttu-id="898df-137">如果您不能 tooadd 共同管理員，請連絡服務管理員或共同管理員的 hello 訂用帳戶 tooget 自行加入。</span><span class="sxs-lookup"><span data-stu-id="898df-137">If you are not able tooadd a co-administrator, then contact a service administrator or co-administrator for hello subscription tooget yourself added.</span></span>   

## <a name="step-4-set-your-subscription-and-sign-up-for-migration"></a><span data-ttu-id="898df-138">步驟 4︰設定您的訂用帳戶並註冊以進行移轉</span><span class="sxs-lookup"><span data-stu-id="898df-138">Step 4: Set your subscription and sign up for migration</span></span>
<span data-ttu-id="898df-139">首先，開啟 PowerShell 提示字元。</span><span class="sxs-lookup"><span data-stu-id="898df-139">First, start a PowerShell prompt.</span></span> <span data-ttu-id="898df-140">進行移轉，您需要的這兩種傳統環境 tooset 和資源管理員。</span><span class="sxs-lookup"><span data-stu-id="898df-140">For migration, you need tooset up your environment for both classic and Resource Manager.</span></span>

<span data-ttu-id="898df-141">登入 tooyour 帳戶 hello 資源管理員的模型。</span><span class="sxs-lookup"><span data-stu-id="898df-141">Sign in tooyour account for hello Resource Manager model.</span></span>

```powershell
    Login-AzureRmAccount
```

<span data-ttu-id="898df-142">使用下列命令的 hello 取得 hello 可用的訂用帳戶：</span><span class="sxs-lookup"><span data-stu-id="898df-142">Get hello available subscriptions by using hello following command:</span></span>

```powershell
    Get-AzureRMSubscription | Sort Name | Select Name
```

<span data-ttu-id="898df-143">設定您的 Azure 訂閱 hello 目前工作階段。</span><span class="sxs-lookup"><span data-stu-id="898df-143">Set your Azure subscription for hello current session.</span></span> <span data-ttu-id="898df-144">此範例中設定 hello 預設訂用帳戶名稱太**我 Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="898df-144">This example sets hello default subscription name too**My Azure Subscription**.</span></span> <span data-ttu-id="898df-145">使用您自己取代 hello 範例訂用帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="898df-145">Replace hello example subscription name with your own.</span></span>

```powershell
    Select-AzureRmSubscription –SubscriptionName "My Azure Subscription"
```

> [!NOTE]
> <span data-ttu-id="898df-146">註冊是一次性步驟，但您必須在嘗試移轉之前完成。</span><span class="sxs-lookup"><span data-stu-id="898df-146">Registration is a one-time step, but you must do it once before attempting migration.</span></span> <span data-ttu-id="898df-147">若未註冊，您會看到下列錯誤訊息的 hello:</span><span class="sxs-lookup"><span data-stu-id="898df-147">Without registering, you see hello following error message:</span></span>
>
> <span data-ttu-id="898df-148">*不正確的要求︰訂用帳戶未針對移轉進行註冊。*</span><span class="sxs-lookup"><span data-stu-id="898df-148">*BadRequest : Subscription is not registered for migration.*</span></span>
>
>

<span data-ttu-id="898df-149">使用下列命令的 hello 註冊與 hello 移轉資源提供者：</span><span class="sxs-lookup"><span data-stu-id="898df-149">Register with hello migration resource provider by using hello following command:</span></span>

```powershell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.ClassicInfrastructureMigrate
```

<span data-ttu-id="898df-150">請等待五分鐘 hello 註冊 toofinish。</span><span class="sxs-lookup"><span data-stu-id="898df-150">Please wait five minutes for hello registration toofinish.</span></span> <span data-ttu-id="898df-151">您可以使用下列命令的 hello 檢查 hello hello 核准狀態：</span><span class="sxs-lookup"><span data-stu-id="898df-151">You can check hello status of hello approval by using hello following command:</span></span>

```powershell
    Get-AzureRmResourceProvider -ProviderNamespace Microsoft.ClassicInfrastructureMigrate
```

<span data-ttu-id="898df-152">請先確定 RegistrationState 是 `Registered` ，再繼續進行。</span><span class="sxs-lookup"><span data-stu-id="898df-152">Make sure that RegistrationState is `Registered` before you proceed.</span></span>

<span data-ttu-id="898df-153">立即登入 tooyour 帳戶 hello 傳統的模型。</span><span class="sxs-lookup"><span data-stu-id="898df-153">Now sign in tooyour account for hello classic model.</span></span>

```powershell
    Add-AzureAccount
```

<span data-ttu-id="898df-154">使用下列命令的 hello 取得 hello 可用的訂用帳戶：</span><span class="sxs-lookup"><span data-stu-id="898df-154">Get hello available subscriptions by using hello following command:</span></span>

```powershell
    Get-AzureSubscription | Sort SubscriptionName | Select SubscriptionName
```

<span data-ttu-id="898df-155">設定您的 Azure 訂閱 hello 目前工作階段。</span><span class="sxs-lookup"><span data-stu-id="898df-155">Set your Azure subscription for hello current session.</span></span> <span data-ttu-id="898df-156">此範例會設定 hello 預設訂用帳戶太**我 Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="898df-156">This example sets hello default subscription too**My Azure Subscription**.</span></span> <span data-ttu-id="898df-157">使用您自己取代 hello 範例訂用帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="898df-157">Replace hello example subscription name with your own.</span></span>

```powershell
    Select-AzureSubscription –SubscriptionName "My Azure Subscription"
```

<br>

## <a name="step-5-make-sure-you-have-enough-azure-resource-manager-virtual-machine-cores-in-hello-azure-region-of-your-current-deployment-or-vnet"></a><span data-ttu-id="898df-158">步驟 5： 請確定您有足夠的 Azure 資源管理員虛擬機器核心 hello 目前的部署或 VNET 的 Azure 區域中</span><span class="sxs-lookup"><span data-stu-id="898df-158">Step 5: Make sure you have enough Azure Resource Manager Virtual Machine cores in hello Azure region of your current deployment or VNET</span></span>
<span data-ttu-id="898df-159">您可以使用下列 PowerShell 命令 toocheck hello 目前的核心數目有 Azure 資源管理員中的 hello。</span><span class="sxs-lookup"><span data-stu-id="898df-159">You can use hello following PowerShell command toocheck hello current number of cores you have in Azure Resource Manager.</span></span> <span data-ttu-id="898df-160">toolearn 進一步了解核心配額，請參閱[限制和 hello Azure Resource Manager](../../azure-subscription-service-limits.md#limits-and-the-azure-resource-manager)。</span><span class="sxs-lookup"><span data-stu-id="898df-160">toolearn more about core quotas, see [Limits and hello Azure Resource Manager](../../azure-subscription-service-limits.md#limits-and-the-azure-resource-manager).</span></span>

<span data-ttu-id="898df-161">這個範例會檢查在 hello hello 可用性**美國西部**區域。</span><span class="sxs-lookup"><span data-stu-id="898df-161">This example checks hello availability in hello **West US** region.</span></span> <span data-ttu-id="898df-162">使用您自己取代 hello 範例區域名稱。</span><span class="sxs-lookup"><span data-stu-id="898df-162">Replace hello example region name with your own.</span></span>

```powershell
Get-AzureRmVMUsage -Location "West US"
```

## <a name="step-6-run-commands-toomigrate-your-iaas-resources"></a><span data-ttu-id="898df-163">步驟 6： 執行命令 toomigrate IaaS 資源</span><span class="sxs-lookup"><span data-stu-id="898df-163">Step 6: Run commands toomigrate your IaaS resources</span></span>
> [!NOTE]
> <span data-ttu-id="898df-164">此處所述的所有 hello 作業都是等冪。</span><span class="sxs-lookup"><span data-stu-id="898df-164">All hello operations described here are idempotent.</span></span> <span data-ttu-id="898df-165">如果您有不支援的功能或設定錯誤以外的問題，我們建議您重試 hello 準備、 中止或認可作業。</span><span class="sxs-lookup"><span data-stu-id="898df-165">If you have a problem other than an unsupported feature or a configuration error, we recommend that you retry hello prepare, abort, or commit operation.</span></span> <span data-ttu-id="898df-166">hello 平台，然後嘗試再次 hello 動作。</span><span class="sxs-lookup"><span data-stu-id="898df-166">hello platform then tries hello action again.</span></span>
>
>

## <a name="step-61-option-1---migrate-virtual-machines-in-a-cloud-service-not-in-a-virtual-network"></a><span data-ttu-id="898df-167">步驟 6.1：選項 1 - 移轉雲端服務中的虛擬機器 (不在虛擬網路中)</span><span class="sxs-lookup"><span data-stu-id="898df-167">Step 6.1: Option 1 - Migrate virtual machines in a cloud service (not in a virtual network)</span></span>
<span data-ttu-id="898df-168">使用下列命令，hello 的雲端服務]，然後按一下 [挑選 hello 雲端服務，而您想 toomigrate 取得 hello 清單。</span><span class="sxs-lookup"><span data-stu-id="898df-168">Get hello list of cloud services by using hello following command, and then pick hello cloud service that you want toomigrate.</span></span> <span data-ttu-id="898df-169">如果 hello 雲端服務中的 hello Vm 虛擬網路中，或他們有 web 或背景工作角色，hello 命令會傳回錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="898df-169">If hello VMs in hello cloud service are in a virtual network or if they have web or worker roles, hello command returns an error message.</span></span>

```powershell
    Get-AzureService | ft Servicename
```

<span data-ttu-id="898df-170">取得 hello hello 雲端服務的部署名稱。</span><span class="sxs-lookup"><span data-stu-id="898df-170">Get hello deployment name for hello cloud service.</span></span> <span data-ttu-id="898df-171">在此範例中，hello 服務名稱是**我的服務**。</span><span class="sxs-lookup"><span data-stu-id="898df-171">In this example, hello service name is **My Service**.</span></span> <span data-ttu-id="898df-172">Hello 範例服務名稱取代成您自己的服務名稱。</span><span class="sxs-lookup"><span data-stu-id="898df-172">Replace hello example service name with your own service name.</span></span>

```powershell
    $serviceName = "My Service"
    $deployment = Get-AzureDeployment -ServiceName $serviceName
    $deploymentName = $deployment.DeploymentName
```

<span data-ttu-id="898df-173">準備移轉的 hello 雲端服務中的 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="898df-173">Prepare hello virtual machines in hello cloud service for migration.</span></span> <span data-ttu-id="898df-174">您必須從兩個選項 toochoose。</span><span class="sxs-lookup"><span data-stu-id="898df-174">You have two options toochoose from.</span></span>

* <span data-ttu-id="898df-175">**選項 1：Hello Vm tooa 平台建立虛擬網路移轉**</span><span class="sxs-lookup"><span data-stu-id="898df-175">**Option 1. Migrate hello VMs tooa platform-created virtual network**</span></span>

    <span data-ttu-id="898df-176">首先，驗證是否可以使用下列命令的 hello hello 雲端服務移轉：</span><span class="sxs-lookup"><span data-stu-id="898df-176">First, validate if you can migrate hello cloud service using hello following commands:</span></span>

    ```powershell
    $validate = Move-AzureService -Validate -ServiceName $serviceName `
        -DeploymentName $deploymentName -CreateNewVirtualNetwork
    $validate.ValidationMessages
    ```

    <span data-ttu-id="898df-177">hello 上述命令會顯示任何警告及封鎖移轉的錯誤。</span><span class="sxs-lookup"><span data-stu-id="898df-177">hello preceding command displays any warnings and errors that block migration.</span></span> <span data-ttu-id="898df-178">如果驗證成功，則可以移 toohello**準備**步驟：</span><span class="sxs-lookup"><span data-stu-id="898df-178">If validation is successful, then you can move on toohello **Prepare** step:</span></span>

    ```powershell
    Move-AzureService -Prepare -ServiceName $serviceName `
        -DeploymentName $deploymentName -CreateNewVirtualNetwork
    ```
* <span data-ttu-id="898df-179">**選項 2：移轉 tooan 現有的虛擬網路中 hello Resource Manager 部署模型**</span><span class="sxs-lookup"><span data-stu-id="898df-179">**Option 2. Migrate tooan existing virtual network in hello Resource Manager deployment model**</span></span>

    <span data-ttu-id="898df-180">此範例中設定 hello 資源群組名稱太**myResourceGroup**，太 hello 虛擬網路名稱**myVirtualNetwork**太 hello 子網路名稱和**mySubNet**。</span><span class="sxs-lookup"><span data-stu-id="898df-180">This example sets hello resource group name too**myResourceGroup**, hello virtual network name too**myVirtualNetwork** and hello subnet name too**mySubNet**.</span></span> <span data-ttu-id="898df-181">取代您自己的資源名稱 hello hello 範例中的 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="898df-181">Replace hello names in hello example with hello names of your own resources.</span></span>

    ```powershell
    $existingVnetRGName = "myResourceGroup"
    $vnetName = "myVirtualNetwork"
    $subnetName = "mySubNet"
    ```

    <span data-ttu-id="898df-182">首先，驗證是否使用下列命令的 hello hello 虛擬網路移轉：</span><span class="sxs-lookup"><span data-stu-id="898df-182">First, validate if you can migrate hello virtual network using hello following command:</span></span>

    ```powershell
    $validate = Move-AzureService -Validate -ServiceName $serviceName `
        -DeploymentName $deploymentName -UseExistingVirtualNetwork -VirtualNetworkResourceGroupName $existingVnetRGName -VirtualNetworkName $vnetName -SubnetName $subnetName
    $validate.ValidationMessages
    ```

    <span data-ttu-id="898df-183">hello 上述命令會顯示任何警告及封鎖移轉的錯誤。</span><span class="sxs-lookup"><span data-stu-id="898df-183">hello preceding command displays any warnings and errors that block migration.</span></span> <span data-ttu-id="898df-184">如果驗證成功，您可以繼續進行下列準備步驟 hello:</span><span class="sxs-lookup"><span data-stu-id="898df-184">If validation is successful, then you can proceed with hello following Prepare step:</span></span>

    ```powershell
        Move-AzureService -Prepare -ServiceName $serviceName -DeploymentName $deploymentName `
        -UseExistingVirtualNetwork -VirtualNetworkResourceGroupName $existingVnetRGName `
        -VirtualNetworkName $vnetName -SubnetName $subnetName
    ```

<span data-ttu-id="898df-185">Hello 上述選項的其中一種成功 hello 「 準備 」 作業之後，查詢 hello Vm hello 移轉的狀態。</span><span class="sxs-lookup"><span data-stu-id="898df-185">After hello Prepare operation succeeds with either of hello preceding options, query hello migration state of hello VMs.</span></span> <span data-ttu-id="898df-186">確保它們處於 hello`Prepared`狀態。</span><span class="sxs-lookup"><span data-stu-id="898df-186">Ensure that they are in hello `Prepared` state.</span></span>

<span data-ttu-id="898df-187">此範例中設定 hello VM 名稱太**myVM**。</span><span class="sxs-lookup"><span data-stu-id="898df-187">This example sets hello VM name too**myVM**.</span></span> <span data-ttu-id="898df-188">Hello 範例名稱取代成您自己的 VM 名稱。</span><span class="sxs-lookup"><span data-stu-id="898df-188">Replace hello example name with your own VM name.</span></span>

```powershell
    $vmName = "myVM"
    $vm = Get-AzureVM -ServiceName $serviceName -Name $vmName
    $vm.VM.MigrationState
```

<span data-ttu-id="898df-189">檢查 hello hello 準備資源使用 PowerShell 或 hello Azure 入口網站的組態。</span><span class="sxs-lookup"><span data-stu-id="898df-189">Check hello configuration for hello prepared resources by using either PowerShell or hello Azure portal.</span></span> <span data-ttu-id="898df-190">如果您不準備好進行移轉，而且您想要讓 toogo 後 toohello 舊狀態，請使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="898df-190">If you are not ready for migration and you want toogo back toohello old state, use hello following command:</span></span>

```powershell
    Move-AzureService -Abort -ServiceName $serviceName -DeploymentName $deploymentName
```

<span data-ttu-id="898df-191">如果 hello 備妥的 configuration 狀況良好，可以向前移動，並使用下列命令的 hello 認可 hello 資源：</span><span class="sxs-lookup"><span data-stu-id="898df-191">If hello prepared configuration looks good, you can move forward and commit hello resources by using hello following command:</span></span>

```powershell
    Move-AzureService -Commit -ServiceName $serviceName -DeploymentName $deploymentName
```

## <a name="step-61-option-2---migrate-virtual-machines-in-a-virtual-network"></a><span data-ttu-id="898df-192">步驟 6.1：選項 2 - 移轉虛擬網路中的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="898df-192">Step 6.1: Option 2 - Migrate virtual machines in a virtual network</span></span>

<span data-ttu-id="898df-193">toomigrate 虛擬機器在虛擬網路中，您可以移轉 hello 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="898df-193">toomigrate virtual machines in a virtual network, you migrate hello virtual network.</span></span> <span data-ttu-id="898df-194">hello 虛擬機器自動移轉與 hello 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="898df-194">hello virtual machines automatically migrate with hello virtual network.</span></span> <span data-ttu-id="898df-195">您想 toomigrate 挑選 hello 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="898df-195">Pick hello virtual network that you want toomigrate.</span></span>
> [!NOTE]
> <span data-ttu-id="898df-196">[將單一傳統的虛擬機器移轉](migrate-single-classic-to-resource-manager.md)藉由使用受管理的磁碟使用 hello VHD （作業系統和資料） 檔案的 hello 虛擬機器建立新的資源管理員虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="898df-196">[Migrate single classic virtual machine](migrate-single-classic-to-resource-manager.md) by creating a new Resource Manager virtual machine with Managed Disks using hello VHD (OS and data) files of hello virtual machine.</span></span>
<br>

> [!NOTE]
> <span data-ttu-id="898df-197">hello 虛擬網路名稱可能不同於所顯示 hello 中新的入口網站。</span><span class="sxs-lookup"><span data-stu-id="898df-197">hello virtual network name might be different from what is shown in hello new Portal.</span></span> <span data-ttu-id="898df-198">hello 新版 Azure 入口網站會顯示 hello 名稱做為`[vnet-name]`但是 hello 實際的虛擬網路名稱必須是型別`Group [resource-group-name] [vnet-name]`。</span><span class="sxs-lookup"><span data-stu-id="898df-198">hello new Azure Portal displays hello name as `[vnet-name]` but hello actual virtual network name is of type `Group [resource-group-name] [vnet-name]`.</span></span> <span data-ttu-id="898df-199">然後再移轉，查閱 hello 實際的虛擬網路名稱使用 hello 命令`Get-AzureVnetSite | Select -Property Name`檢視在 hello 或舊的 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="898df-199">Before migrating, lookup hello actual virtual network name using hello command `Get-AzureVnetSite | Select -Property Name` or view it in hello old Azure Portal.</span></span> 

<span data-ttu-id="898df-200">此範例中設定 hello 虛擬網路名稱太**myVnet**。</span><span class="sxs-lookup"><span data-stu-id="898df-200">This example sets hello virtual network name too**myVnet**.</span></span> <span data-ttu-id="898df-201">Hello 範例虛擬網路名稱取代您自己。</span><span class="sxs-lookup"><span data-stu-id="898df-201">Replace hello example virtual network name with your own.</span></span>

```powershell
    $vnetName = "myVnet"
```

> [!NOTE]
> <span data-ttu-id="898df-202">如果 hello 虛擬網路包含 web 或背景工作角色或 Vm 具有不支援的設定，您會取得驗證錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="898df-202">If hello virtual network contains web or worker roles, or VMs with unsupported configurations, you get a validation error message.</span></span>
>
>

<span data-ttu-id="898df-203">如果您可以使用下列命令的 hello 移轉 hello 虛擬網路，首先，驗證：</span><span class="sxs-lookup"><span data-stu-id="898df-203">First, validate if you can migrate hello virtual network by using hello following command:</span></span>

```powershell
    Move-AzureVirtualNetwork -Validate -VirtualNetworkName $vnetName
```

<span data-ttu-id="898df-204">hello 上述命令會顯示任何警告及封鎖移轉的錯誤。</span><span class="sxs-lookup"><span data-stu-id="898df-204">hello preceding command displays any warnings and errors that block migration.</span></span> <span data-ttu-id="898df-205">如果驗證成功，您可以繼續進行下列準備步驟 hello:</span><span class="sxs-lookup"><span data-stu-id="898df-205">If validation is successful, then you can proceed with hello following Prepare step:</span></span>

```powershell
    Move-AzureVirtualNetwork -Prepare -VirtualNetworkName $vnetName
```

<span data-ttu-id="898df-206">檢查 hello hello 準備使用 Azure PowerShell 或 hello Azure 入口網站的虛擬機器的組態。</span><span class="sxs-lookup"><span data-stu-id="898df-206">Check hello configuration for hello prepared virtual machines by using either Azure PowerShell or hello Azure portal.</span></span> <span data-ttu-id="898df-207">如果您不準備好進行移轉，而且您想要讓 toogo 後 toohello 舊狀態，請使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="898df-207">If you are not ready for migration and you want toogo back toohello old state, use hello following command:</span></span>

```powershell
    Move-AzureVirtualNetwork -Abort -VirtualNetworkName $vnetName
```

<span data-ttu-id="898df-208">如果 hello 備妥的 configuration 狀況良好，可以向前移動，並使用下列命令的 hello 認可 hello 資源：</span><span class="sxs-lookup"><span data-stu-id="898df-208">If hello prepared configuration looks good, you can move forward and commit hello resources by using hello following command:</span></span>

```powershell
    Move-AzureVirtualNetwork -Commit -VirtualNetworkName $vnetName
```

## <a name="step-62-migrate-a-storage-account"></a><span data-ttu-id="898df-209">步驟 6.2：移轉儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="898df-209">Step 6.2 Migrate a storage account</span></span>
<span data-ttu-id="898df-210">一旦您完成移轉 hello 虛擬機器時，我們建議您移轉 hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="898df-210">Once you're done migrating hello virtual machines, we recommend you migrate hello storage accounts.</span></span>

<span data-ttu-id="898df-211">移轉 hello 儲存體帳戶之前，請執行前的必要條件檢查：</span><span class="sxs-lookup"><span data-stu-id="898df-211">Before you migrate hello storage account, please perform preceding prerequisite checks:</span></span>

* <span data-ttu-id="898df-212">**將傳統的磁碟儲存 hello 儲存體帳戶中的虛擬機器移轉**</span><span class="sxs-lookup"><span data-stu-id="898df-212">**Migrate classic virtual machines whose disks are stored in hello storage account**</span></span>

    <span data-ttu-id="898df-213">上述命令傳回 RoleName 和 DiskName 屬性的所有 hello 傳統 VM 磁碟 hello 儲存體帳戶中。</span><span class="sxs-lookup"><span data-stu-id="898df-213">Preceding command returns RoleName and DiskName properties of all hello classic VM disks in hello storage account.</span></span> <span data-ttu-id="898df-214">RoleName 是 hello 磁碟連接的虛擬機器 toowhich hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="898df-214">RoleName is hello name of hello virtual machine toowhich a disk is attached.</span></span> <span data-ttu-id="898df-215">如果上述命令會傳回磁碟，然後確保移轉之前移轉這些磁碟已連接該虛擬機器 toowhich hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="898df-215">If preceding command returns disks then ensure that virtual machines toowhich these disks are attached are migrated before migrating hello storage account.</span></span>
    ```powershell
     $storageAccountName = 'yourStorageAccountName'
      Get-AzureDisk | where-Object {$_.MediaLink.Host.Contains($storageAccountName)} | Select-Object -ExpandProperty AttachedTo -Property `
      DiskName | Format-List -Property RoleName, DiskName

    ```
* <span data-ttu-id="898df-216">**刪除未附加之傳統的 VM 磁碟儲存在 hello 儲存體帳戶**</span><span class="sxs-lookup"><span data-stu-id="898df-216">**Delete unattached classic VM disks stored in hello storage account**</span></span>

    <span data-ttu-id="898df-217">找到未附加之傳統 VM 磁碟在 hello 儲存體帳戶使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="898df-217">Find unattached classic VM disks in hello storage account using following command:</span></span>

    ```powershell
        $storageAccountName = 'yourStorageAccountName'
        Get-AzureDisk | where-Object {$_.MediaLink.Host.Contains($storageAccountName)} | Where-Object -Property AttachedTo -EQ $null | Format-List -Property DiskName  

    ```
    <span data-ttu-id="898df-218">如果上述命令傳回磁碟，則使用下列命令刪除這些磁碟︰</span><span class="sxs-lookup"><span data-stu-id="898df-218">If above command returns disks then delete these disks using following command:</span></span>

    ```powershell
       Remove-AzureDisk -DiskName 'yourDiskName'
    ```
* <span data-ttu-id="898df-219">**刪除 VM 映像儲存在 hello 儲存體帳戶**</span><span class="sxs-lookup"><span data-stu-id="898df-219">**Delete VM images stored in hello storage account**</span></span>

    <span data-ttu-id="898df-220">上述命令會傳回所有 hello VM 映像 hello 儲存體帳戶中儲存的作業系統磁碟。</span><span class="sxs-lookup"><span data-stu-id="898df-220">Preceding command returns all hello VM images with OS disk stored in hello storage account.</span></span>
     ```powershell
        Get-AzureVmImage | Where-Object { $_.OSDiskConfiguration.MediaLink -ne $null -and $_.OSDiskConfiguration.MediaLink.Host.Contains($storageAccountName)`
                                } | Select-Object -Property ImageName, ImageLabel
     ```
     <span data-ttu-id="898df-221">上述命令會傳回所有 hello VM 映像 hello 儲存體帳戶中儲存的資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="898df-221">Preceding command returns all hello VM images with data disks stored in hello storage account.</span></span>
     ```powershell

        Get-AzureVmImage | Where-Object {$_.DataDiskConfigurations -ne $null `
                                         -and ($_.DataDiskConfigurations | Where-Object {$_.MediaLink -ne $null -and $_.MediaLink.Host.Contains($storageAccountName)}).Count -gt 0 `
                                        } | Select-Object -Property ImageName, ImageLabel
     ```
    <span data-ttu-id="898df-222">刪除所有上述使用上述命令的命令所傳回的 hello VM 映像：</span><span class="sxs-lookup"><span data-stu-id="898df-222">Delete all hello VM images returned by above commands using preceding command:</span></span>
    ```powershell
    Remove-AzureVMImage -ImageName 'yourImageName'
    ```

<span data-ttu-id="898df-223">使用下列命令的 hello 驗證移轉的每個儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="898df-223">Validate each storage account for migration by using hello following command.</span></span> <span data-ttu-id="898df-224">此範例中的 hello 儲存體帳戶名稱是**myStorageAccount**。</span><span class="sxs-lookup"><span data-stu-id="898df-224">In this example, hello storage account name is **myStorageAccount**.</span></span> <span data-ttu-id="898df-225">Hello 範例名稱取代 hello 您自己的儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="898df-225">Replace hello example name with hello name of your own storage account.</span></span>

```powershell
    $storageAccountName = "myStorageAccount"
    Move-AzureStorageAccount -Validate -StorageAccountName $storageAccountName
```

<span data-ttu-id="898df-226">下一個步驟是 tooPrepare hello 儲存體帳戶進行移轉</span><span class="sxs-lookup"><span data-stu-id="898df-226">Next step is tooPrepare hello storage account for migration</span></span>

```powershell
    $storageAccountName = "myStorageAccount"
    Move-AzureStorageAccount -Prepare -StorageAccountName $storageAccountName
```

<span data-ttu-id="898df-227">檢查 hello hello 準備使用 Azure PowerShell 或 hello Azure 入口網站的儲存體帳戶的組態。</span><span class="sxs-lookup"><span data-stu-id="898df-227">Check hello configuration for hello prepared storage account by using either Azure PowerShell or hello Azure portal.</span></span> <span data-ttu-id="898df-228">如果您不準備好進行移轉，而且您想要讓 toogo 後 toohello 舊狀態，請使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="898df-228">If you are not ready for migration and you want toogo back toohello old state, use hello following command:</span></span>

```powershell
    Move-AzureStorageAccount -Abort -StorageAccountName $storageAccountName
```

<span data-ttu-id="898df-229">如果 hello 備妥的 configuration 狀況良好，可以向前移動，並使用下列命令的 hello 認可 hello 資源：</span><span class="sxs-lookup"><span data-stu-id="898df-229">If hello prepared configuration looks good, you can move forward and commit hello resources by using hello following command:</span></span>

```powershell
    Move-AzureStorageAccount -Commit -StorageAccountName $storageAccountName
```

## <a name="next-steps"></a><span data-ttu-id="898df-230">後續步驟</span><span class="sxs-lookup"><span data-stu-id="898df-230">Next steps</span></span>
* [<span data-ttu-id="898df-231">平台支援移轉的 IaaS 資源從傳統 tooAzure 資源管理員概觀</span><span class="sxs-lookup"><span data-stu-id="898df-231">Overview of platform-supported migration of IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="898df-232">技術的深入剖析平台支援移轉從傳統 tooAzure 資源管理員</span><span class="sxs-lookup"><span data-stu-id="898df-232">Technical deep dive on platform-supported migration from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="898df-233">規劃移轉的 IaaS 資源從傳統 tooAzure 資源管理員</span><span class="sxs-lookup"><span data-stu-id="898df-233">Planning for migration of IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="898df-234">使用 CLI toomigrate IaaS 資源從傳統 tooAzure 資源管理員</span><span class="sxs-lookup"><span data-stu-id="898df-234">Use CLI toomigrate IaaS resources from classic tooAzure Resource Manager</span></span>](../linux/migration-classic-resource-manager-cli.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="898df-235">社群工具，用以協助移轉的 IaaS 資源從傳統 tooAzure 資源管理員</span><span class="sxs-lookup"><span data-stu-id="898df-235">Community tools for assisting with migration of IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-community-tools.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="898df-236">檢閱最常見的移轉錯誤</span><span class="sxs-lookup"><span data-stu-id="898df-236">Review most common migration errors</span></span>](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="898df-237">檢閱 hello 最常見問題集從傳統 tooAzure 資源管理員移轉的 IaaS 資源</span><span class="sxs-lookup"><span data-stu-id="898df-237">Review hello most frequently asked questions about migrating IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
