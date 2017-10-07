---
title: "aaaMigrate Vm tooResource 管理員使用 Azure CLI |Microsoft 文件"
description: "本文逐步 hello 平台支援移轉的資源從傳統 tooAzure 資源管理員使用 Azure CLI"
services: virtual-machines-linux
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: d6f5a877-05b6-4127-a545-3f5bede4e479
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: kasing
ms.openlocfilehash: 0b11f4bb1b4658b3e88bf7629147ed953b678556
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-iaas-resources-from-classic-tooazure-resource-manager-by-using-azure-cli"></a><span data-ttu-id="abea8-103">從傳統 tooAzure 資源管理員移轉 IaaS 資源，使用 Azure CLI</span><span class="sxs-lookup"><span data-stu-id="abea8-103">Migrate IaaS resources from classic tooAzure Resource Manager by using Azure CLI</span></span>
<span data-ttu-id="abea8-104">這些步驟顯示如何 toouse Azure 命令列介面 (CLI) 的命令 toomigrate 基礎結構為從 hello 傳統部署模型 toohello Azure Resource Manager 部署模型的服務 (IaaS) 資源。</span><span class="sxs-lookup"><span data-stu-id="abea8-104">These steps show you how toouse Azure command-line interface (CLI) commands toomigrate infrastructure as a service (IaaS) resources from hello classic deployment model toohello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="abea8-105">hello 文章需要 hello [Azure CLI](../../cli-install-nodejs.md)。</span><span class="sxs-lookup"><span data-stu-id="abea8-105">hello article requires hello [Azure CLI](../../cli-install-nodejs.md).</span></span>

> [!NOTE]
> <span data-ttu-id="abea8-106">此處所述的所有 hello 作業都是等冪。</span><span class="sxs-lookup"><span data-stu-id="abea8-106">All hello operations described here are idempotent.</span></span> <span data-ttu-id="abea8-107">如果您有不支援的功能或設定錯誤以外的問題，我們建議您重試 hello 準備、 中止或認可作業。</span><span class="sxs-lookup"><span data-stu-id="abea8-107">If you have a problem other than an unsupported feature or a configuration error, we recommend that you retry hello prepare, abort, or commit operation.</span></span> <span data-ttu-id="abea8-108">hello 平台將再重試 hello 的動作。</span><span class="sxs-lookup"><span data-stu-id="abea8-108">hello platform will then try hello action again.</span></span>
> 
> 

<br>
<span data-ttu-id="abea8-109">以下是步驟需要執行移轉程序期間 toobe 流程圖 tooidentify hello 順序</span><span class="sxs-lookup"><span data-stu-id="abea8-109">Here is a flowchart tooidentify hello order in which steps need toobe executed during a migration process</span></span>

![螢幕擷取畫面顯示 hello 移轉步驟](../windows/media/migration-classic-resource-manager/migration-flow.png)

## <a name="step-1-prepare-for-migration"></a><span data-ttu-id="abea8-111">步驟 1︰為移轉做準備</span><span class="sxs-lookup"><span data-stu-id="abea8-111">Step 1: Prepare for migration</span></span>
<span data-ttu-id="abea8-112">以下是我們建議您在評估從傳統 tooResource Manager 移轉的 IaaS 資源的一些最佳作法：</span><span class="sxs-lookup"><span data-stu-id="abea8-112">Here are a few best practices that we recommend as you evaluate migrating IaaS resources from classic tooResource Manager:</span></span>

* <span data-ttu-id="abea8-113">閱讀 hello[不支援的設定或功能的清單](../windows/migration-classic-resource-manager-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="abea8-113">Read through hello [list of unsupported configurations or features](../windows/migration-classic-resource-manager-overview.md).</span></span> <span data-ttu-id="abea8-114">如果您有使用不支援的設定或功能的虛擬機器，我們建議您等待 hello 功能/組態支援 toobe 宣布。</span><span class="sxs-lookup"><span data-stu-id="abea8-114">If you have virtual machines that use unsupported configurations or features, we recommend that you wait for hello feature/configuration support toobe announced.</span></span> <span data-ttu-id="abea8-115">或者，您可以移除該功能，或移出該設定 tooenable 移轉時，如果其符合您的需求。</span><span class="sxs-lookup"><span data-stu-id="abea8-115">Alternatively, you can remove that feature or move out of that configuration tooenable migration if it suits your needs.</span></span>
* <span data-ttu-id="abea8-116">如果您有自動化部署基礎結構和應用程式目前的指令碼，請使用這些指令碼移轉嘗試 toocreate 類似的測試設定。</span><span class="sxs-lookup"><span data-stu-id="abea8-116">If you have automated scripts that deploy your infrastructure and applications today, try toocreate a similar test setup by using those scripts for migration.</span></span> <span data-ttu-id="abea8-117">或者，您可以設定範例環境使用 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="abea8-117">Alternatively, you can set up sample environments by using hello Azure portal.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="abea8-118">從傳統 tooResource Manager 移轉目前不支援應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="abea8-118">Application Gateways are not currently supported for migration from classic tooResource Manager.</span></span> <span data-ttu-id="abea8-119">toomigrate 傳統虛擬網路與應用程式閘道，執行準備作業 toomove hello 網路之前先移除 hello 閘道。</span><span class="sxs-lookup"><span data-stu-id="abea8-119">toomigrate a classic virtual network with an Application gateway, remove hello gateway before running a Prepare operation toomove hello network.</span></span> <span data-ttu-id="abea8-120">Hello 移轉完成之後，重新連接 hello 閘道 Azure 資源管理員中。</span><span class="sxs-lookup"><span data-stu-id="abea8-120">After you complete hello migration, reconnect hello gateway in Azure Resource Manager.</span></span> 
>
><span data-ttu-id="abea8-121">ExpressRoute 閘道連接 tooExpressRoute 電路，另一個訂用帳戶中的不會自動移轉。</span><span class="sxs-lookup"><span data-stu-id="abea8-121">ExpressRoute gateways connecting tooExpressRoute circuits in another subscription cannot be migrated automatically.</span></span> <span data-ttu-id="abea8-122">在這種情況下，移除 hello ExpressRoute 閘道、 hello 虛擬網路移轉並重新建立 hello 閘道。</span><span class="sxs-lookup"><span data-stu-id="abea8-122">In such cases, remove hello ExpressRoute gateway, migrate hello virtual network and recreate hello gateway.</span></span> <span data-ttu-id="abea8-123">請參閱[移轉 ExpressRoute 電路和相關聯的虛擬網路與 hello 傳統 toohello Resource Manager 部署模型](../../expressroute/expressroute-migration-classic-resource-manager.md)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="abea8-123">Please see [Migrate ExpressRoute circuits and associated virtual networks from hello classic toohello Resource Manager deployment model](../../expressroute/expressroute-migration-classic-resource-manager.md) for more information.</span></span>
> 
> 

## <a name="step-2-set-your-subscription-and-register-hello-provider"></a><span data-ttu-id="abea8-124">步驟 2： 設定您的訂用帳戶，並註冊 hello 提供者</span><span class="sxs-lookup"><span data-stu-id="abea8-124">Step 2: Set your subscription and register hello provider</span></span>
<span data-ttu-id="abea8-125">移轉案例中，您需要的這兩種傳統環境 tooset 和資源管理員。</span><span class="sxs-lookup"><span data-stu-id="abea8-125">For migration scenarios, you need tooset up your environment for both classic and Resource Manager.</span></span> <span data-ttu-id="abea8-126">[安裝 Azure CLI](../../cli-install-nodejs.md) 並[選取您的訂用帳戶](../../xplat-cli-connect.md)。</span><span class="sxs-lookup"><span data-stu-id="abea8-126">[Install Azure CLI](../../cli-install-nodejs.md) and [select your subscription](../../xplat-cli-connect.md).</span></span>

<span data-ttu-id="abea8-127">Tooyour 登入帳戶。</span><span class="sxs-lookup"><span data-stu-id="abea8-127">Sign-in tooyour account.</span></span>

    azure login

<span data-ttu-id="abea8-128">使用下列命令的 hello 選取 hello Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="abea8-128">Select hello Azure subscription by using hello following command.</span></span>

    azure account set "<azure-subscription-name>"

> [!NOTE]
> <span data-ttu-id="abea8-129">註冊是一次步驟但它需要 toobe 完成一次嘗試移轉。</span><span class="sxs-lookup"><span data-stu-id="abea8-129">Registration is a one time step but it needs toobe done once before attempting migration.</span></span> <span data-ttu-id="abea8-130">若未註冊，您會看到下列錯誤訊息的 hello</span><span class="sxs-lookup"><span data-stu-id="abea8-130">Without registering you'll see hello following error message</span></span> 
> 
> <span data-ttu-id="abea8-131">*不正確的要求︰訂用帳戶未針對移轉進行註冊。*</span><span class="sxs-lookup"><span data-stu-id="abea8-131">*BadRequest : Subscription is not registered for migration.*</span></span> 
> 
> 

<span data-ttu-id="abea8-132">使用下列命令的 hello 註冊與 hello 移轉資源提供者。</span><span class="sxs-lookup"><span data-stu-id="abea8-132">Register with hello migration resource provider by using hello following command.</span></span> <span data-ttu-id="abea8-133">請注意，在某些情況下，此命令會逾時。不過，hello 註冊才會成功。</span><span class="sxs-lookup"><span data-stu-id="abea8-133">Note that in some cases, this command times out. However, hello registration will be successful.</span></span>

    azure provider register Microsoft.ClassicInfrastructureMigrate

<span data-ttu-id="abea8-134">請等待五分鐘 hello 註冊 toofinish。</span><span class="sxs-lookup"><span data-stu-id="abea8-134">Please wait five minutes for hello registration toofinish.</span></span> <span data-ttu-id="abea8-135">您可以使用下列命令的 hello 檢查 hello hello 核准狀態。</span><span class="sxs-lookup"><span data-stu-id="abea8-135">You can check hello status of hello approval by using hello following command.</span></span> <span data-ttu-id="abea8-136">請先確定 RegistrationState 是 `Registered` ，再繼續進行。</span><span class="sxs-lookup"><span data-stu-id="abea8-136">Make sure that RegistrationState is `Registered` before you proceed.</span></span>

    azure provider show Microsoft.ClassicInfrastructureMigrate

<span data-ttu-id="abea8-137">現在切換 CLI toohello`asm`模式。</span><span class="sxs-lookup"><span data-stu-id="abea8-137">Now switch CLI toohello `asm` mode.</span></span>

    azure config mode asm

## <a name="step-3-make-sure-you-have-enough-azure-resource-manager-virtual-machine-cores-in-hello-azure-region-of-your-current-deployment-or-vnet"></a><span data-ttu-id="abea8-138">步驟 3： 請確定您有足夠的 Azure 資源管理員虛擬機器核心 hello 目前的部署或 VNET 的 Azure 區域中</span><span class="sxs-lookup"><span data-stu-id="abea8-138">Step 3: Make sure you have enough Azure Resource Manager Virtual Machine cores in hello Azure region of your current deployment or VNET</span></span>
<span data-ttu-id="abea8-139">這個步驟您將需要 tooswitch 太`arm`模式。</span><span class="sxs-lookup"><span data-stu-id="abea8-139">For this step you'll need tooswitch too`arm` mode.</span></span> <span data-ttu-id="abea8-140">以下列命令的 hello 這麼做。</span><span class="sxs-lookup"><span data-stu-id="abea8-140">Do this with hello following command.</span></span>

```
azure config mode arm
```

<span data-ttu-id="abea8-141">您可以使用下列 CLI 命令 toocheck hello 目前量核心有 Azure 資源管理員中的 hello。</span><span class="sxs-lookup"><span data-stu-id="abea8-141">You can use hello following CLI command toocheck hello current amount of cores you have in Azure Resource Manager.</span></span> <span data-ttu-id="abea8-142">toolearn 進一步了解核心配額，請參閱[限制和 hello Azure 資源管理員](../../azure-subscription-service-limits.md#limits-and-the-azure-resource-manager)</span><span class="sxs-lookup"><span data-stu-id="abea8-142">toolearn more about core quotas, see [Limits and hello Azure Resource Manager](../../azure-subscription-service-limits.md#limits-and-the-azure-resource-manager)</span></span>

```
azure vm list-usage -l "<Your VNET or Deployment's Azure region"
```

<span data-ttu-id="abea8-143">完成後確認此步驟中，您可以切換回太`asm`模式。</span><span class="sxs-lookup"><span data-stu-id="abea8-143">Once you're done verifying this step, you can switch back too`asm` mode.</span></span>

    azure config mode asm


## <a name="step-4-option-1---migrate-virtual-machines-in-a-cloud-service"></a><span data-ttu-id="abea8-144">步驟 4：選項 1 - 移轉雲端服務中的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="abea8-144">Step 4: Option 1 - Migrate virtual machines in a cloud service</span></span>
<span data-ttu-id="abea8-145">使用下列命令，hello 的雲端服務]，然後按一下 [挑選 hello 雲端服務，而您想 toomigrate 取得 hello 清單。</span><span class="sxs-lookup"><span data-stu-id="abea8-145">Get hello list of cloud services by using hello following command, and then pick hello cloud service that you want toomigrate.</span></span> <span data-ttu-id="abea8-146">請注意如果 hello 雲端服務中的 hello Vm 虛擬網路中，或他們有 web/背景工作角色，您會收到錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="abea8-146">Note that if hello VMs in hello cloud service are in a virtual network or if they have web/worker roles, you will get an error message.</span></span>

    azure service list

<span data-ttu-id="abea8-147">執行 hello hello 詳細資訊輸出中的下列命令 tooget hello 部署 hello 雲端服務名稱。</span><span class="sxs-lookup"><span data-stu-id="abea8-147">Run hello following command tooget hello deployment name for hello cloud service from hello verbose output.</span></span> <span data-ttu-id="abea8-148">在大部分情況下，hello 部署名稱是 hello 與 hello 雲端服務名稱相同。</span><span class="sxs-lookup"><span data-stu-id="abea8-148">In most cases, hello deployment name is hello same as hello cloud service name.</span></span>

    azure service show <serviceName> -vv

<span data-ttu-id="abea8-149">首先，驗證是否可以使用下列命令的 hello hello 雲端服務移轉：</span><span class="sxs-lookup"><span data-stu-id="abea8-149">First, validate if you can migrate hello cloud service using hello following commands:</span></span>

```shell
azure service deployment validate-migration <serviceName> <deploymentName> new "" "" ""
```

<span data-ttu-id="abea8-150">準備移轉的 hello 雲端服務中的 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="abea8-150">Prepare hello virtual machines in hello cloud service for migration.</span></span> <span data-ttu-id="abea8-151">您必須從兩個選項 toochoose。</span><span class="sxs-lookup"><span data-stu-id="abea8-151">You have two options toochoose from.</span></span>

<span data-ttu-id="abea8-152">如果您想 toomigrate hello Vm tooa 平台建立虛擬網路，請使用下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="abea8-152">If you want toomigrate hello VMs tooa platform-created virtual network, use hello following command.</span></span>

    azure service deployment prepare-migration <serviceName> <deploymentName> new "" "" ""

<span data-ttu-id="abea8-153">如果您想 toomigrate tooan 現有 hello Resource Manager 部署模型中的虛擬網路，請使用下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="abea8-153">If you want toomigrate tooan existing virtual network in hello Resource Manager deployment model, use hello following command.</span></span>

    azure service deployment prepare-migration <serviceName> <deploymentName> existing <destinationVNETResourceGroupName> <subnetName> <vnetName>

<span data-ttu-id="abea8-154">Hello 準備之後操作是否成功，您可以查看 hello 詳細資訊輸出 tooget hello 的移轉狀態 hello Vm，並確保它們處於 hello`Prepared`狀態。</span><span class="sxs-lookup"><span data-stu-id="abea8-154">After hello prepare operation is successful, you can look through hello verbose output tooget hello migration state of hello VMs and ensure that they are in hello `Prepared` state.</span></span>

    azure vm show <vmName> -vv

<span data-ttu-id="abea8-155">檢查 hello hello 準備資源使用 CLI 或 hello Azure 入口網站的組態。</span><span class="sxs-lookup"><span data-stu-id="abea8-155">Check hello configuration for hello prepared resources by using either CLI or hello Azure portal.</span></span> <span data-ttu-id="abea8-156">如果您不準備好進行移轉，而且您想要讓 toogo 後 toohello 舊狀態，請使用下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="abea8-156">If you are not ready for migration and you want toogo back toohello old state, use hello following command.</span></span>

    azure service deployment abort-migration <serviceName> <deploymentName>

<span data-ttu-id="abea8-157">如果 hello 備妥的組態看起來不錯，可以向前移動，並使用下列命令的 hello 認可 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="abea8-157">If hello prepared configuration looks good, you can move forward and commit hello resources by using hello following command.</span></span>

    azure service deployment commit-migration <serviceName> <deploymentName>



## <a name="step-4-option-2----migrate-virtual-machines-in-a-virtual-network"></a><span data-ttu-id="abea8-158">步驟 4：選項 2 - 移轉虛擬網路中的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="abea8-158">Step 4: Option 2 -  Migrate virtual machines in a virtual network</span></span>
<span data-ttu-id="abea8-159">您想 toomigrate 挑選 hello 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="abea8-159">Pick hello virtual network that you want toomigrate.</span></span> <span data-ttu-id="abea8-160">請注意，是否 hello 虛擬網路包含 web/背景工作角色或 Vm 具有不支援的設定，您會取得驗證錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="abea8-160">Note that if hello virtual network contains web/worker roles or VMs with unsupported configurations, you will get a validation error message.</span></span>

<span data-ttu-id="abea8-161">使用下列命令的 hello hello 訂用帳戶中取得所有 hello 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="abea8-161">Get all hello virtual networks in hello subscription by using hello following command.</span></span>

    azure network vnet list

<span data-ttu-id="abea8-162">hello 輸出看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="abea8-162">hello output will look something like this:</span></span>

![Hello 與反白顯示的 hello 整個虛擬網路名稱的命令列的螢幕擷取畫面。](../media/virtual-machines-linux-cli-migration-classic-resource-manager/vnet.png)

<span data-ttu-id="abea8-164">在上述範例中的 hello，hello **virtualNetworkName** hello 整個名稱**」 群組 classicubuntu16 classicubuntu16"**。</span><span class="sxs-lookup"><span data-stu-id="abea8-164">In hello above example, hello **virtualNetworkName** is hello entire name **"Group classicubuntu16 classicubuntu16"**.</span></span>

<span data-ttu-id="abea8-165">首先，驗證是否使用下列命令的 hello hello 虛擬網路移轉：</span><span class="sxs-lookup"><span data-stu-id="abea8-165">First, validate if you can migrate hello virtual network using hello following command:</span></span>

```shell
azure network vnet validate-migration <virtualNetworkName>
```

<span data-ttu-id="abea8-166">使用下列命令的 hello 準備移轉您選擇的 hello 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="abea8-166">Prepare hello virtual network of your choice for migration by using hello following command.</span></span>

    azure network vnet prepare-migration <virtualNetworkName>

<span data-ttu-id="abea8-167">檢查 hello hello 備妥使用 CLI 或 hello Azure 入口網站的虛擬機器的組態。</span><span class="sxs-lookup"><span data-stu-id="abea8-167">Check hello configuration for hello prepared virtual machines by using either CLI or hello Azure portal.</span></span> <span data-ttu-id="abea8-168">如果您不準備好進行移轉，而且您想要讓 toogo 後 toohello 舊狀態，請使用下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="abea8-168">If you are not ready for migration and you want toogo back toohello old state, use hello following command.</span></span>

    azure network vnet abort-migration <virtualNetworkName>

<span data-ttu-id="abea8-169">如果 hello 備妥的組態看起來不錯，可以向前移動，並使用下列命令的 hello 認可 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="abea8-169">If hello prepared configuration looks good, you can move forward and commit hello resources by using hello following command.</span></span>

    azure network vnet commit-migration <virtualNetworkName>

## <a name="step-5-migrate-a-storage-account"></a><span data-ttu-id="abea8-170">步驟 5：移轉儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="abea8-170">Step 5: Migrate a storage account</span></span>
<span data-ttu-id="abea8-171">一旦您完成移轉 hello 虛擬機器時，我們建議您移轉 hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="abea8-171">Once you're done migrating hello virtual machines, we recommend you migrate hello storage account.</span></span>

<span data-ttu-id="abea8-172">準備移轉中的 hello 儲存體帳戶，使用下列命令的 hello</span><span class="sxs-lookup"><span data-stu-id="abea8-172">Prepare hello storage account for migration by using hello following command</span></span>

    azure storage account prepare-migration <storageAccountName>

<span data-ttu-id="abea8-173">檢查由使用 CLI 或 hello Azure 入口網站所準備的儲存體帳戶的 hello hello 組態。</span><span class="sxs-lookup"><span data-stu-id="abea8-173">Check hello configuration for hello prepared storage account by using either CLI or hello Azure portal.</span></span> <span data-ttu-id="abea8-174">如果您不準備好進行移轉，而且您想要讓 toogo 後 toohello 舊狀態，請使用下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="abea8-174">If you are not ready for migration and you want toogo back toohello old state, use hello following command.</span></span>

    azure storage account abort-migration <storageAccountName>

<span data-ttu-id="abea8-175">如果 hello 備妥的組態看起來不錯，可以向前移動，並使用下列命令的 hello 認可 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="abea8-175">If hello prepared configuration looks good, you can move forward and commit hello resources by using hello following command.</span></span>

    azure storage account commit-migration <storageAccountName>

## <a name="next-steps"></a><span data-ttu-id="abea8-176">後續步驟</span><span class="sxs-lookup"><span data-stu-id="abea8-176">Next steps</span></span>

* [<span data-ttu-id="abea8-177">平台支援移轉的 IaaS 資源從傳統 tooAzure 資源管理員概觀</span><span class="sxs-lookup"><span data-stu-id="abea8-177">Overview of platform-supported migration of IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="abea8-178">技術的深入剖析平台支援移轉從傳統 tooAzure 資源管理員</span><span class="sxs-lookup"><span data-stu-id="abea8-178">Technical deep dive on platform-supported migration from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="abea8-179">規劃移轉的 IaaS 資源從傳統 tooAzure 資源管理員</span><span class="sxs-lookup"><span data-stu-id="abea8-179">Planning for migration of IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="abea8-180">使用傳統 tooAzure 資源管理員的 PowerShell toomigrate IaaS 資源</span><span class="sxs-lookup"><span data-stu-id="abea8-180">Use PowerShell toomigrate IaaS resources from classic tooAzure Resource Manager</span></span>](../windows/migration-classic-resource-manager-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="abea8-181">社群工具，用以協助移轉的 IaaS 資源從傳統 tooAzure 資源管理員</span><span class="sxs-lookup"><span data-stu-id="abea8-181">Community tools for assisting with migration of IaaS resources from classic tooAzure Resource Manager</span></span>](../windows/migration-classic-resource-manager-community-tools.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="abea8-182">檢閱最常見的移轉錯誤</span><span class="sxs-lookup"><span data-stu-id="abea8-182">Review most common migration errors</span></span>](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="abea8-183">檢閱 hello 最常見問題集從傳統 tooAzure 資源管理員移轉的 IaaS 資源</span><span class="sxs-lookup"><span data-stu-id="abea8-183">Review hello most frequently asked questions about migrating IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
