---
title: "使用 Azure CLI 將 VM 移轉至 Resource Manager | Microsoft Docs"
description: "這篇文章提供使用 Azure CLI 進行平台支援之資源移轉 (從傳統移轉至 Azure Resource Manager) 的逐步解說"
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
ms.openlocfilehash: a63d758570b09b37b8e51c639267f729521d9ae0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="migrate-iaas-resources-from-classic-to-azure-resource-manager-by-using-azure-cli"></a><span data-ttu-id="ba39f-103">使用 Azure CLI 將 IaaS 資源從傳統移轉至 Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ba39f-103">Migrate IaaS resources from classic to Azure Resource Manager by using Azure CLI</span></span>
<span data-ttu-id="ba39f-104">以下步驟說明如何使用 Azure 命令列介面 (CLI) 命令，將基礎結構即服務 (IaaS) 資源從傳統部署模型移轉至 Azure Resource Manager 部署模型。</span><span class="sxs-lookup"><span data-stu-id="ba39f-104">These steps show you how to use Azure command-line interface (CLI) commands to migrate infrastructure as a service (IaaS) resources from the classic deployment model to the Azure Resource Manager deployment model.</span></span> <span data-ttu-id="ba39f-105">本文需要 [Azure CLI](../../cli-install-nodejs.md)。</span><span class="sxs-lookup"><span data-stu-id="ba39f-105">The article requires the [Azure CLI](../../cli-install-nodejs.md).</span></span>

> [!NOTE]
> <span data-ttu-id="ba39f-106">下述所有作業都是等冪的。</span><span class="sxs-lookup"><span data-stu-id="ba39f-106">All the operations described here are idempotent.</span></span> <span data-ttu-id="ba39f-107">如果您有不支援的功能或組態錯誤以外的任何問題，建議您重新嘗試準備、中止或認可作業。</span><span class="sxs-lookup"><span data-stu-id="ba39f-107">If you have a problem other than an unsupported feature or a configuration error, we recommend that you retry the prepare, abort, or commit operation.</span></span> <span data-ttu-id="ba39f-108">如此，平台就會重新嘗試該動作。</span><span class="sxs-lookup"><span data-stu-id="ba39f-108">The platform will then try the action again.</span></span>
> 
> 

<br>
<span data-ttu-id="ba39f-109">下列流程圖會識別在移轉程序期間執行步驟所需的順序</span><span class="sxs-lookup"><span data-stu-id="ba39f-109">Here is a flowchart to identify the order in which steps need to be executed during a migration process</span></span>

![Screenshot that shows the migration steps](../windows/media/migration-classic-resource-manager/migration-flow.png)

## <a name="step-1-prepare-for-migration"></a><span data-ttu-id="ba39f-111">步驟 1︰為移轉做準備</span><span class="sxs-lookup"><span data-stu-id="ba39f-111">Step 1: Prepare for migration</span></span>
<span data-ttu-id="ba39f-112">以下是您評估將 IaaS 資源從傳統移轉至 Resource Manager 時，我們所建議的一些最佳做法：</span><span class="sxs-lookup"><span data-stu-id="ba39f-112">Here are a few best practices that we recommend as you evaluate migrating IaaS resources from classic to Resource Manager:</span></span>

* <span data-ttu-id="ba39f-113">將 [不支援的組態或功能清單](../windows/migration-classic-resource-manager-overview.md)看一遍。</span><span class="sxs-lookup"><span data-stu-id="ba39f-113">Read through the [list of unsupported configurations or features](../windows/migration-classic-resource-manager-overview.md).</span></span> <span data-ttu-id="ba39f-114">如果您的虛擬機器使用不支援的組態或功能，建議您等到宣布支援該功能/組態之後，再進行移轉。</span><span class="sxs-lookup"><span data-stu-id="ba39f-114">If you have virtual machines that use unsupported configurations or features, we recommend that you wait for the feature/configuration support to be announced.</span></span> <span data-ttu-id="ba39f-115">或者，您可以移除該功能或移出該組態，以利移轉進行 (如果這麼做符合您的需求)。</span><span class="sxs-lookup"><span data-stu-id="ba39f-115">Alternatively, you can remove that feature or move out of that configuration to enable migration if it suits your needs.</span></span>
* <span data-ttu-id="ba39f-116">如果您是使用自動化指令碼來部署現今的基礎結構和應用程式，請使用這些指令碼來嘗試建立相似的測試設定以進行移轉。</span><span class="sxs-lookup"><span data-stu-id="ba39f-116">If you have automated scripts that deploy your infrastructure and applications today, try to create a similar test setup by using those scripts for migration.</span></span> <span data-ttu-id="ba39f-117">或者，您也可以使用 Azure 入口網站來設定範例環境。</span><span class="sxs-lookup"><span data-stu-id="ba39f-117">Alternatively, you can set up sample environments by using the Azure portal.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ba39f-118">目前不支援將應用程式閘道從傳統環境移轉至 Resource Manager。</span><span class="sxs-lookup"><span data-stu-id="ba39f-118">Application Gateways are not currently supported for migration from classic to Resource Manager.</span></span> <span data-ttu-id="ba39f-119">若要使用應用程式閘道來移轉傳統虛擬網路，請先移除閘道，再執行「準備」作業來移動網路。</span><span class="sxs-lookup"><span data-stu-id="ba39f-119">To migrate a classic virtual network with an Application gateway, remove the gateway before running a Prepare operation to move the network.</span></span> <span data-ttu-id="ba39f-120">在完成移轉之後，於 Azure Resource Manager 中重新連接閘道。</span><span class="sxs-lookup"><span data-stu-id="ba39f-120">After you complete the migration, reconnect the gateway in Azure Resource Manager.</span></span> 
>
><span data-ttu-id="ba39f-121">如果 ExpressRoute 閘道連線至另一個訂用帳戶中的 ExpressRoute 線路，則無法自動移轉。</span><span class="sxs-lookup"><span data-stu-id="ba39f-121">ExpressRoute gateways connecting to ExpressRoute circuits in another subscription cannot be migrated automatically.</span></span> <span data-ttu-id="ba39f-122">在這種情況下，請移除 ExpressRoute 閘道，移轉虛擬網路，然後重新建立閘道。</span><span class="sxs-lookup"><span data-stu-id="ba39f-122">In such cases, remove the ExpressRoute gateway, migrate the virtual network and recreate the gateway.</span></span> <span data-ttu-id="ba39f-123">如需相關步驟和詳細資訊，請參閱[將 ExpressRoute 線路和相關聯的虛擬網路從傳統部署模型移轉至 Resource Manager 部署模型](../../expressroute/expressroute-migration-classic-resource-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="ba39f-123">Please see [Migrate ExpressRoute circuits and associated virtual networks from the classic to the Resource Manager deployment model](../../expressroute/expressroute-migration-classic-resource-manager.md) for more information.</span></span>
> 
> 

## <a name="step-2-set-your-subscription-and-register-the-provider"></a><span data-ttu-id="ba39f-124">步驟 2︰設定您的訂用帳戶並註冊提供者</span><span class="sxs-lookup"><span data-stu-id="ba39f-124">Step 2: Set your subscription and register the provider</span></span>
<span data-ttu-id="ba39f-125">針對移轉案例，您必須為傳統和 Resource Manager 模型設定您的環境。</span><span class="sxs-lookup"><span data-stu-id="ba39f-125">For migration scenarios, you need to set up your environment for both classic and Resource Manager.</span></span> <span data-ttu-id="ba39f-126">[安裝 Azure CLI](../../cli-install-nodejs.md) 並[選取您的訂用帳戶](../../xplat-cli-connect.md)。</span><span class="sxs-lookup"><span data-stu-id="ba39f-126">[Install Azure CLI](../../cli-install-nodejs.md) and [select your subscription](../../xplat-cli-connect.md).</span></span>

<span data-ttu-id="ba39f-127">登入您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="ba39f-127">Sign-in to your account.</span></span>

    azure login

<span data-ttu-id="ba39f-128">使用下列命令來選取 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="ba39f-128">Select the Azure subscription by using the following command.</span></span>

    azure account set "<azure-subscription-name>"

> [!NOTE]
> <span data-ttu-id="ba39f-129">註冊是一次性步驟，但必須在嘗試移轉之前完成。</span><span class="sxs-lookup"><span data-stu-id="ba39f-129">Registration is a one time step but it needs to be done once before attempting migration.</span></span> <span data-ttu-id="ba39f-130">如果不註冊，您會看到下列錯誤訊息</span><span class="sxs-lookup"><span data-stu-id="ba39f-130">Without registering you'll see the following error message</span></span> 
> 
> <span data-ttu-id="ba39f-131">*不正確的要求︰訂用帳戶未針對移轉進行註冊。*</span><span class="sxs-lookup"><span data-stu-id="ba39f-131">*BadRequest : Subscription is not registered for migration.*</span></span> 
> 
> 

<span data-ttu-id="ba39f-132">請使用下列命令向移轉資源提供者註冊。</span><span class="sxs-lookup"><span data-stu-id="ba39f-132">Register with the migration resource provider by using the following command.</span></span> <span data-ttu-id="ba39f-133">請注意，在某些情況下，此命令會逾時。</span><span class="sxs-lookup"><span data-stu-id="ba39f-133">Note that in some cases, this command times out.</span></span> <span data-ttu-id="ba39f-134">不過，註冊將會成功。</span><span class="sxs-lookup"><span data-stu-id="ba39f-134">However, the registration will be successful.</span></span>

    azure provider register Microsoft.ClassicInfrastructureMigrate

<span data-ttu-id="ba39f-135">請等候 5 分鐘讓註冊完成。</span><span class="sxs-lookup"><span data-stu-id="ba39f-135">Please wait five minutes for the registration to finish.</span></span> <span data-ttu-id="ba39f-136">您可以使用下列命令來檢查核准狀態。</span><span class="sxs-lookup"><span data-stu-id="ba39f-136">You can check the status of the approval by using the following command.</span></span> <span data-ttu-id="ba39f-137">請先確定 RegistrationState 是 `Registered` ，再繼續進行。</span><span class="sxs-lookup"><span data-stu-id="ba39f-137">Make sure that RegistrationState is `Registered` before you proceed.</span></span>

    azure provider show Microsoft.ClassicInfrastructureMigrate

<span data-ttu-id="ba39f-138">現在，請將 CLI 切換至 `asm` 模式。</span><span class="sxs-lookup"><span data-stu-id="ba39f-138">Now switch CLI to the `asm` mode.</span></span>

    azure config mode asm

## <a name="step-3-make-sure-you-have-enough-azure-resource-manager-virtual-machine-cores-in-the-azure-region-of-your-current-deployment-or-vnet"></a><span data-ttu-id="ba39f-139">步驟 3︰確定您目前的部署或 VNET 的 Azure 區域中有足夠的 Azure Resource Manager 虛擬機器核心</span><span class="sxs-lookup"><span data-stu-id="ba39f-139">Step 3: Make sure you have enough Azure Resource Manager Virtual Machine cores in the Azure region of your current deployment or VNET</span></span>
<span data-ttu-id="ba39f-140">針對這個步驟，您將需要切換到 `arm` 模式。</span><span class="sxs-lookup"><span data-stu-id="ba39f-140">For this step you'll need to switch to `arm` mode.</span></span> <span data-ttu-id="ba39f-141">請使用下列命令來執行此操作。</span><span class="sxs-lookup"><span data-stu-id="ba39f-141">Do this with the following command.</span></span>

```
azure config mode arm
```

<span data-ttu-id="ba39f-142">您可以使用下列 CLI 命令來檢查您目前在 Azure Resource Manager 中擁有的核心數量。</span><span class="sxs-lookup"><span data-stu-id="ba39f-142">You can use the following CLI command to check the current amount of cores you have in Azure Resource Manager.</span></span> <span data-ttu-id="ba39f-143">若要深入了解核心配額，請參閱 [限制和 Azure Resource Manager](../../azure-subscription-service-limits.md#limits-and-the-azure-resource-manager)</span><span class="sxs-lookup"><span data-stu-id="ba39f-143">To learn more about core quotas, see [Limits and the Azure Resource Manager](../../azure-subscription-service-limits.md#limits-and-the-azure-resource-manager)</span></span>

```
azure vm list-usage -l "<Your VNET or Deployment's Azure region"
```

<span data-ttu-id="ba39f-144">完成這個步驟的確認之後，您可以切換回 `asm` 模式。</span><span class="sxs-lookup"><span data-stu-id="ba39f-144">Once you're done verifying this step, you can switch back to `asm` mode.</span></span>

    azure config mode asm


## <a name="step-4-option-1---migrate-virtual-machines-in-a-cloud-service"></a><span data-ttu-id="ba39f-145">步驟 4：選項 1 - 移轉雲端服務中的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="ba39f-145">Step 4: Option 1 - Migrate virtual machines in a cloud service</span></span>
<span data-ttu-id="ba39f-146">使用下列命令來取得雲端服務清單，然後選擇您想要移轉的雲端服務。</span><span class="sxs-lookup"><span data-stu-id="ba39f-146">Get the list of cloud services by using the following command, and then pick the cloud service that you want to migrate.</span></span> <span data-ttu-id="ba39f-147">請注意，如果雲端服務中的 VM 是在虛擬網路中，或是具有 Web/背景工作角色，您將會收到錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="ba39f-147">Note that if the VMs in the cloud service are in a virtual network or if they have web/worker roles, you will get an error message.</span></span>

    azure service list

<span data-ttu-id="ba39f-148">執行下列命令，以從詳細資訊輸出中獲得雲端服務的部署名稱。</span><span class="sxs-lookup"><span data-stu-id="ba39f-148">Run the following command to get the deployment name for the cloud service from the verbose output.</span></span> <span data-ttu-id="ba39f-149">在大部分情況下，部署名稱和雲端服務名稱相同。</span><span class="sxs-lookup"><span data-stu-id="ba39f-149">In most cases, the deployment name is the same as the cloud service name.</span></span>

    azure service show <serviceName> -vv

<span data-ttu-id="ba39f-150">首先，請使用下列命令來驗證您是否可以移轉雲端服務︰</span><span class="sxs-lookup"><span data-stu-id="ba39f-150">First, validate if you can migrate the cloud service using the following commands:</span></span>

```shell
azure service deployment validate-migration <serviceName> <deploymentName> new "" "" ""
```

<span data-ttu-id="ba39f-151">準備好雲端服務中的虛擬機器以進行移轉。</span><span class="sxs-lookup"><span data-stu-id="ba39f-151">Prepare the virtual machines in the cloud service for migration.</span></span> <span data-ttu-id="ba39f-152">有兩個選項可供您選擇。</span><span class="sxs-lookup"><span data-stu-id="ba39f-152">You have two options to choose from.</span></span>

<span data-ttu-id="ba39f-153">如果您想要將 VM 移轉至平台建立的虛擬網路，請使用下列命令。</span><span class="sxs-lookup"><span data-stu-id="ba39f-153">If you want to migrate the VMs to a platform-created virtual network, use the following command.</span></span>

    azure service deployment prepare-migration <serviceName> <deploymentName> new "" "" ""

<span data-ttu-id="ba39f-154">如果您想要移轉至 Resource Manager 部署模型中的現有虛擬網路，請使用下列命令。</span><span class="sxs-lookup"><span data-stu-id="ba39f-154">If you want to migrate to an existing virtual network in the Resource Manager deployment model, use the following command.</span></span>

    azure service deployment prepare-migration <serviceName> <deploymentName> existing <destinationVNETResourceGroupName> <subnetName> <vnetName>

<span data-ttu-id="ba39f-155">準備作業成功之後，您可以瀏覽詳細資訊輸出，以取得 VM 的移轉狀態並確保 VM 處於 `Prepared` 狀態。</span><span class="sxs-lookup"><span data-stu-id="ba39f-155">After the prepare operation is successful, you can look through the verbose output to get the migration state of the VMs and ensure that they are in the `Prepared` state.</span></span>

    azure vm show <vmName> -vv

<span data-ttu-id="ba39f-156">使用 CLI 或 Azure 入口網站來檢查已備妥之資源的組態。</span><span class="sxs-lookup"><span data-stu-id="ba39f-156">Check the configuration for the prepared resources by using either CLI or the Azure portal.</span></span> <span data-ttu-id="ba39f-157">如果您尚未準備好進行移轉，而想要回到舊狀態，請使用下列命令。</span><span class="sxs-lookup"><span data-stu-id="ba39f-157">If you are not ready for migration and you want to go back to the old state, use the following command.</span></span>

    azure service deployment abort-migration <serviceName> <deploymentName>

<span data-ttu-id="ba39f-158">如果備妥的組態看起來沒問題，您就可以繼續進行並使用下列命令來認可資源。</span><span class="sxs-lookup"><span data-stu-id="ba39f-158">If the prepared configuration looks good, you can move forward and commit the resources by using the following command.</span></span>

    azure service deployment commit-migration <serviceName> <deploymentName>



## <a name="step-4-option-2----migrate-virtual-machines-in-a-virtual-network"></a><span data-ttu-id="ba39f-159">步驟 4：選項 2 - 移轉虛擬網路中的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="ba39f-159">Step 4: Option 2 -  Migrate virtual machines in a virtual network</span></span>
<span data-ttu-id="ba39f-160">選取您想要移轉的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="ba39f-160">Pick the virtual network that you want to migrate.</span></span> <span data-ttu-id="ba39f-161">請注意，如果虛擬網路包含 Web/背景工作角色，或有具備不支援之組態的 VM，您將會收到驗證錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="ba39f-161">Note that if the virtual network contains web/worker roles or VMs with unsupported configurations, you will get a validation error message.</span></span>

<span data-ttu-id="ba39f-162">使用下列命令來取得訂用帳戶中的所有虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="ba39f-162">Get all the virtual networks in the subscription by using the following command.</span></span>

    azure network vnet list

<span data-ttu-id="ba39f-163">輸出會看起來類似這樣：</span><span class="sxs-lookup"><span data-stu-id="ba39f-163">The output will look something like this:</span></span>

![將整個虛擬網路名稱醒目提示的命令列螢幕擷取畫面。](../media/virtual-machines-linux-cli-migration-classic-resource-manager/vnet.png)

<span data-ttu-id="ba39f-165">在上述範例中，**virtualNetworkName** 是 **"Group classicubuntu16 classicubuntu16"** 這整個名稱。</span><span class="sxs-lookup"><span data-stu-id="ba39f-165">In the above example, the **virtualNetworkName** is the entire name **"Group classicubuntu16 classicubuntu16"**.</span></span>

<span data-ttu-id="ba39f-166">首先，請使用下列命令來驗證您是否可以移轉虛擬網路︰</span><span class="sxs-lookup"><span data-stu-id="ba39f-166">First, validate if you can migrate the virtual network using the following command:</span></span>

```shell
azure network vnet validate-migration <virtualNetworkName>
```

<span data-ttu-id="ba39f-167">使用下列命令來準備您所選擇的虛擬網路以進行移轉。</span><span class="sxs-lookup"><span data-stu-id="ba39f-167">Prepare the virtual network of your choice for migration by using the following command.</span></span>

    azure network vnet prepare-migration <virtualNetworkName>

<span data-ttu-id="ba39f-168">使用 CLI 或 Azure 入口網站來檢查已備妥之虛擬機器的組態。</span><span class="sxs-lookup"><span data-stu-id="ba39f-168">Check the configuration for the prepared virtual machines by using either CLI or the Azure portal.</span></span> <span data-ttu-id="ba39f-169">如果您尚未準備好進行移轉，而想要回到舊狀態，請使用下列命令。</span><span class="sxs-lookup"><span data-stu-id="ba39f-169">If you are not ready for migration and you want to go back to the old state, use the following command.</span></span>

    azure network vnet abort-migration <virtualNetworkName>

<span data-ttu-id="ba39f-170">如果備妥的組態看起來沒問題，您就可以繼續進行並使用下列命令來認可資源。</span><span class="sxs-lookup"><span data-stu-id="ba39f-170">If the prepared configuration looks good, you can move forward and commit the resources by using the following command.</span></span>

    azure network vnet commit-migration <virtualNetworkName>

## <a name="step-5-migrate-a-storage-account"></a><span data-ttu-id="ba39f-171">步驟 5：移轉儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="ba39f-171">Step 5: Migrate a storage account</span></span>
<span data-ttu-id="ba39f-172">完成虛擬機器移轉之後，我們建議您將移轉儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="ba39f-172">Once you're done migrating the virtual machines, we recommend you migrate the storage account.</span></span>

<span data-ttu-id="ba39f-173">使用下列命令來準備儲存體帳戶以進行移轉</span><span class="sxs-lookup"><span data-stu-id="ba39f-173">Prepare the storage account for migration by using the following command</span></span>

    azure storage account prepare-migration <storageAccountName>

<span data-ttu-id="ba39f-174">使用 CLI 或 Azure 入口網站來檢查已備妥之儲存體帳戶的設定。</span><span class="sxs-lookup"><span data-stu-id="ba39f-174">Check the configuration for the prepared storage account by using either CLI or the Azure portal.</span></span> <span data-ttu-id="ba39f-175">如果您尚未準備好進行移轉，而想要回到舊狀態，請使用下列命令。</span><span class="sxs-lookup"><span data-stu-id="ba39f-175">If you are not ready for migration and you want to go back to the old state, use the following command.</span></span>

    azure storage account abort-migration <storageAccountName>

<span data-ttu-id="ba39f-176">如果備妥的組態看起來沒問題，您就可以繼續進行並使用下列命令來認可資源。</span><span class="sxs-lookup"><span data-stu-id="ba39f-176">If the prepared configuration looks good, you can move forward and commit the resources by using the following command.</span></span>

    azure storage account commit-migration <storageAccountName>

## <a name="next-steps"></a><span data-ttu-id="ba39f-177">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ba39f-177">Next steps</span></span>

* [<span data-ttu-id="ba39f-178">平台支援的 IaaS 資源移轉 (從傳統移轉至 Azure Resource Manager) 的概觀</span><span class="sxs-lookup"><span data-stu-id="ba39f-178">Overview of platform-supported migration of IaaS resources from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="ba39f-179">平台支援的從傳統移轉至 Azure Resource Manager 的技術深入探討</span><span class="sxs-lookup"><span data-stu-id="ba39f-179">Technical deep dive on platform-supported migration from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="ba39f-180">將 IaaS 資源從傳統移轉至 Azure Resource Manager 的規劃</span><span class="sxs-lookup"><span data-stu-id="ba39f-180">Planning for migration of IaaS resources from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="ba39f-181">使用 PowerShell 將 IaaS 資源從傳統移轉至 Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ba39f-181">Use PowerShell to migrate IaaS resources from classic to Azure Resource Manager</span></span>](../windows/migration-classic-resource-manager-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="ba39f-182">用於協助將 IaaS 資源從傳統移轉至 Azure Resource Manager 的社群工具</span><span class="sxs-lookup"><span data-stu-id="ba39f-182">Community tools for assisting with migration of IaaS resources from classic to Azure Resource Manager</span></span>](../windows/migration-classic-resource-manager-community-tools.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="ba39f-183">檢閱最常見的移轉錯誤</span><span class="sxs-lookup"><span data-stu-id="ba39f-183">Review most common migration errors</span></span>](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="ba39f-184">檢閱有關將 IaaS 資源從傳統移轉至 Azure Resource Manager 的常見問題集</span><span class="sxs-lookup"><span data-stu-id="ba39f-184">Review the most frequently asked questions about migrating IaaS resources from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
