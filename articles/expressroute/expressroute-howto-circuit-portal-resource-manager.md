---
title: "建立與修改 ExpressRoute 線路：Azure 入口網站 | Microsoft Docs"
description: "本文說明如何建立、佈建、驗證、更新、刪除和取消佈建 ExpressRoute 線路。"
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 68d59d59-ed4d-482f-9cbc-534ebb090613
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/07/2017
ms.author: cherylmc;ganesr
ms.openlocfilehash: e3721cd3c031622788f553e71a6555b844f3f7dc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="create-and-modify-an-expressroute-circuit"></a><span data-ttu-id="af17f-103">建立和修改 ExpressRoute 線路</span><span class="sxs-lookup"><span data-stu-id="af17f-103">Create and modify an ExpressRoute circuit</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="af17f-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="af17f-104">Azure portal</span></span>](expressroute-howto-circuit-portal-resource-manager.md)
> * [<span data-ttu-id="af17f-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="af17f-105">PowerShell</span></span>](expressroute-howto-circuit-arm.md)
> * [<span data-ttu-id="af17f-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="af17f-106">Azure CLI</span></span>](howto-circuit-cli.md)
> * [<span data-ttu-id="af17f-107">影片 - Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="af17f-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [<span data-ttu-id="af17f-108">PowerShell (傳統)</span><span class="sxs-lookup"><span data-stu-id="af17f-108">PowerShell (classic)</span></span>](expressroute-howto-circuit-classic.md)
>

<span data-ttu-id="af17f-109">此文章說明如何使用 Azure 入口網站和 Azure Resource Manager 部署模型建立 Azure ExpressRoute 線路。</span><span class="sxs-lookup"><span data-stu-id="af17f-109">This article describes how to create an Azure ExpressRoute circuit by using the Azure portal and the Azure Resource Manager deployment model.</span></span> <span data-ttu-id="af17f-110">下列步驟也會示範如何檢查線路的狀態、對它進行更新，或是對它進行刪除及取消佈建。</span><span class="sxs-lookup"><span data-stu-id="af17f-110">The following steps also show you how to check the status of the circuit, update it, or delete and deprovision it.</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="af17f-111">開始之前</span><span class="sxs-lookup"><span data-stu-id="af17f-111">Before you begin</span></span>
* <span data-ttu-id="af17f-112">開始設定之前，請檢閱[必要條件](expressroute-prerequisites.md)和[工作流程](expressroute-workflows.md)。</span><span class="sxs-lookup"><span data-stu-id="af17f-112">Review the [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="af17f-113">確定您可以存取 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="af17f-113">Ensure that you have access to the [Azure portal](https://portal.azure.com).</span></span>
* <span data-ttu-id="af17f-114">確定您具有建立新網路資源的權限。</span><span class="sxs-lookup"><span data-stu-id="af17f-114">Ensure that you have permissions to create new networking resources.</span></span> <span data-ttu-id="af17f-115">如果您沒有正確的權限，請連絡您的帳戶管理員。</span><span class="sxs-lookup"><span data-stu-id="af17f-115">Contact your account administrator if you do not have the right permissions.</span></span>
* <span data-ttu-id="af17f-116">您可以在開始前先[觀賞影片](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)，以便更加了解步驟。</span><span class="sxs-lookup"><span data-stu-id="af17f-116">You can [view a video](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit) before beginning in order to better understand the steps.</span></span>

## <a name="create-and-provision-an-expressroute-circuit"></a><span data-ttu-id="af17f-117">建立和佈建 ExpressRoute 線路</span><span class="sxs-lookup"><span data-stu-id="af17f-117">Create and provision an ExpressRoute circuit</span></span>
### <a name="1-sign-in-to-the-azure-portal"></a><span data-ttu-id="af17f-118">1.登入 Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="af17f-118">1. Sign in to the Azure portal</span></span>
<span data-ttu-id="af17f-119">透過瀏覽器瀏覽至 [Azure 入口網站](http://portal.azure.com) ，並使用您的 Azure 帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="af17f-119">From a browser, navigate to the [Azure portal](http://portal.azure.com) and sign in with your Azure account.</span></span>

### <a name="2-create-a-new-expressroute-circuit"></a><span data-ttu-id="af17f-120">2.建立新的 ExpressRoute 線路</span><span class="sxs-lookup"><span data-stu-id="af17f-120">2. Create a new ExpressRoute circuit</span></span>
> [!IMPORTANT]
> <span data-ttu-id="af17f-121">ExpressRoute 線路將會從發出服務金鑰時開始收費。</span><span class="sxs-lookup"><span data-stu-id="af17f-121">Your ExpressRoute circuit will be billed from the moment a service key is issued.</span></span> <span data-ttu-id="af17f-122">請確定在連線提供者準備好佈建線路之後，再執行此作業。</span><span class="sxs-lookup"><span data-stu-id="af17f-122">Ensure that you perform this operation when the connectivity provider is ready to provision the circuit.</span></span>
> 
> 

1. <span data-ttu-id="af17f-123">您可以選取建立新資源的選項來建立 ExpressRoute 線路。</span><span class="sxs-lookup"><span data-stu-id="af17f-123">You can create an ExpressRoute circuit by selecting the option to create a new resource.</span></span> <span data-ttu-id="af17f-124">按一下 [新增] > [網路] > [ExpressRoute]，如下圖所示：</span><span class="sxs-lookup"><span data-stu-id="af17f-124">Click **New** > **Networking** > **ExpressRoute**, as shown in the following image:</span></span>
   
    ![建立 ExpressRoute 線路](./media/expressroute-howto-circuit-portal-resource-manager/createcircuit1.png)
2. <span data-ttu-id="af17f-126">按一下 [ExpressRoute] 之後，將會看到 [建立 ExpressRoute 線路] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="af17f-126">After you click **ExpressRoute**, you'll see the **Create ExpressRoute circuit** blade.</span></span> <span data-ttu-id="af17f-127">填寫此刀鋒視窗上的值時，請確定您指定正確的 SKU 層和資料計量。</span><span class="sxs-lookup"><span data-stu-id="af17f-127">When you're filling in the values on this blade, make sure that you specify the correct SKU tier and data metering.</span></span>
   
   * <span data-ttu-id="af17f-128"> 決定要啟用 ExpressRoute 標準或 ExpressRoute 進階附加元件。</span><span class="sxs-lookup"><span data-stu-id="af17f-128">**Tier** determines whether an ExpressRoute standard or an ExpressRoute premium add-on is enabled.</span></span> <span data-ttu-id="af17f-129">您可以指定 [標準] 來取得標準 SKU，或指定 [進階] 來取得進階附加元件。</span><span class="sxs-lookup"><span data-stu-id="af17f-129">You can specify **Standard** to get the standard SKU or **Premium** for the premium add-on.</span></span>
   * <span data-ttu-id="af17f-130"> 決定計費類型。</span><span class="sxs-lookup"><span data-stu-id="af17f-130">**Data metering** determines the billing type.</span></span> <span data-ttu-id="af17f-131">您可以指定 [計量付費] 以採用計量付費數據傳輸方案，選取 [無限制] 以採用無限制的資料方案。</span><span class="sxs-lookup"><span data-stu-id="af17f-131">You can specify **Metered** for a metered data plan and **Unlimited** for an unlimited data plan.</span></span> <span data-ttu-id="af17f-132">請注意，您可以將計費類型從 [計量付費] 變更為 [無限制]，但無法從 [無限制] 變更為 [計量付費]。</span><span class="sxs-lookup"><span data-stu-id="af17f-132">Note that you can change the billing type from **Metered** to **Unlimited**, but you can't change the type from **Unlimited** to **Metered**.</span></span>
     
     ![設定 SKU 層和資料計量](./media/expressroute-howto-circuit-portal-resource-manager/createcircuit2.png)

> [!IMPORTANT]
> <span data-ttu-id="af17f-134">請留意「對等位置」表示您與 Microsoft 對等互連的[實體位置](expressroute-locations.md) 。</span><span class="sxs-lookup"><span data-stu-id="af17f-134">Please be aware that the Peering Location indicates the [physical location](expressroute-locations.md) where you are peering with Microsoft.</span></span> <span data-ttu-id="af17f-135">這**不會**連結到「位置」屬性，這是指 Azure 網路資源提供者所在的地理位置。</span><span class="sxs-lookup"><span data-stu-id="af17f-135">This is **not** linked to "Location" property, which refers to the geography where the Azure Network Resource Provider is located.</span></span> <span data-ttu-id="af17f-136">儘管它們並無關聯，但最好還是選擇地理位置靠近線路對等位置的網路資源提供者。</span><span class="sxs-lookup"><span data-stu-id="af17f-136">While they are not related, it is a good practice to choose a Network Resource Provider geographically close to the Peering Location of the circuit.</span></span> 
> 
> 

### <a name="3-view-the-circuits-and-properties"></a><span data-ttu-id="af17f-137">3.檢視線路和屬性</span><span class="sxs-lookup"><span data-stu-id="af17f-137">3. View the circuits and properties</span></span>
<span data-ttu-id="af17f-138">**檢視所有線路**</span><span class="sxs-lookup"><span data-stu-id="af17f-138">**View all the circuits**</span></span>

<span data-ttu-id="af17f-139">您可以選取左側功能表上的 [所有資源] 來檢視您建立的所有線路。</span><span class="sxs-lookup"><span data-stu-id="af17f-139">You can view all the circuits that you created by selecting **All resources** on the left-side menu.</span></span>

![檢視線路](./media/expressroute-howto-circuit-portal-resource-manager/listresource.png)

<span data-ttu-id="af17f-141">**檢視屬性**</span><span class="sxs-lookup"><span data-stu-id="af17f-141">**View the properties**</span></span>

    You can view the properties of the circuit by selecting it. On this blade, note the service key for the circuit. You must copy the circuit key for your circuit and pass it down to the service provider to complete the provisioning process. The circuit key is specific to your circuit.

![檢視屬性](./media/expressroute-howto-circuit-portal-resource-manager/listproperties1.png)

### <a name="4-send-the-service-key-to-your-connectivity-provider-for-provisioning"></a><span data-ttu-id="af17f-143">4.將服務金鑰傳送給連線提供者以進行佈建</span><span class="sxs-lookup"><span data-stu-id="af17f-143">4. Send the service key to your connectivity provider for provisioning</span></span>
<span data-ttu-id="af17f-144">在此刀鋒視窗上，[提供者狀態] 提供服務提供者端目前的佈建狀態相關資訊。</span><span class="sxs-lookup"><span data-stu-id="af17f-144">On this blade, **Provider status** provides information on the current state of provisioning on the service-provider side.</span></span> <span data-ttu-id="af17f-145">[線路狀態] 提供 Microsoft 端的狀態。</span><span class="sxs-lookup"><span data-stu-id="af17f-145">**Circuit status** provides the state on the Microsoft side.</span></span> <span data-ttu-id="af17f-146">如需線路佈建狀態的詳細資訊，請參閱[工作流程](expressroute-workflows.md#expressroute-circuit-provisioning-states)文章。</span><span class="sxs-lookup"><span data-stu-id="af17f-146">For more information about circuit provisioning states, see the [Workflows](expressroute-workflows.md#expressroute-circuit-provisioning-states) article.</span></span>

<span data-ttu-id="af17f-147">當您建立新的 ExpressRoute 線路時，線路會是下列狀態：</span><span class="sxs-lookup"><span data-stu-id="af17f-147">When you create a new ExpressRoute circuit, the circuit will be in the following state:</span></span>

<span data-ttu-id="af17f-148">提供者狀態︰未佈建</span><span class="sxs-lookup"><span data-stu-id="af17f-148">Provider status: Not provisioned</span></span><BR>
<span data-ttu-id="af17f-149">線路狀態：已啟用</span><span class="sxs-lookup"><span data-stu-id="af17f-149">Circuit status: Enabled</span></span>

![起始佈建程序](./media/expressroute-howto-circuit-portal-resource-manager/viewstatus.png)

<span data-ttu-id="af17f-151">當連線提供者正在為您啟用線路時，線路會變更為下列狀態：</span><span class="sxs-lookup"><span data-stu-id="af17f-151">The circuit will change to the following state when the connectivity provider is in the process of enabling it for you:</span></span>

<span data-ttu-id="af17f-152">提供者狀態︰正在佈建</span><span class="sxs-lookup"><span data-stu-id="af17f-152">Provider status: Provisioning</span></span><BR>
<span data-ttu-id="af17f-153">線路狀態：已啟用</span><span class="sxs-lookup"><span data-stu-id="af17f-153">Circuit status: Enabled</span></span>

<span data-ttu-id="af17f-154">若要能夠使用 ExpressRoute 線路，它必須處於下列狀態：</span><span class="sxs-lookup"><span data-stu-id="af17f-154">For you to be able to use an ExpressRoute circuit, it must be in the following state:</span></span>

<span data-ttu-id="af17f-155">提供者狀態︰已佈建</span><span class="sxs-lookup"><span data-stu-id="af17f-155">Provider status: Provisioned</span></span><BR>
<span data-ttu-id="af17f-156">線路狀態：已啟用</span><span class="sxs-lookup"><span data-stu-id="af17f-156">Circuit status: Enabled</span></span>

### <a name="5-periodically-check-the-status-and-the-state-of-the-circuit-key"></a><span data-ttu-id="af17f-157">5.定期檢查線路金鑰的狀態與狀況</span><span class="sxs-lookup"><span data-stu-id="af17f-157">5. Periodically check the status and the state of the circuit key</span></span>
<span data-ttu-id="af17f-158">選取感興趣的線路，即可檢視該線路的屬性。</span><span class="sxs-lookup"><span data-stu-id="af17f-158">You can view the properties of the circuit that you're interested in by selecting it.</span></span> <span data-ttu-id="af17f-159">檢查 [提供者狀態]，確定它已變成 [已佈建] 再繼續。</span><span class="sxs-lookup"><span data-stu-id="af17f-159">Check the **Provider status** and ensure that it has moved to **Provisioned** before you continue.</span></span>

![線路和提供者狀態](./media/expressroute-howto-circuit-portal-resource-manager/viewstatusprovisioned.png)

### <a name="6-create-your-routing-configuration"></a><span data-ttu-id="af17f-161">6.建立路由組態</span><span class="sxs-lookup"><span data-stu-id="af17f-161">6. Create your routing configuration</span></span>
<span data-ttu-id="af17f-162">如需逐步指示，請參閱 [ExpressRoute 線路路由組態](expressroute-howto-routing-portal-resource-manager.md)一文以建立和修改線路對等。</span><span class="sxs-lookup"><span data-stu-id="af17f-162">For step-by-step instructions, refer to the [ExpressRoute circuit routing configuration](expressroute-howto-routing-portal-resource-manager.md) article to create and modify circuit peerings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="af17f-163">這些指示只適用於由提供第 2 層連線服務的服務提供者所建立的線路。</span><span class="sxs-lookup"><span data-stu-id="af17f-163">These instructions only apply to circuits that are created with service providers that offer layer 2 connectivity services.</span></span> <span data-ttu-id="af17f-164">如果您使用的服務提供者是提供受管理的第 3 層服務 (通常是 IP VPN，如 MPLS)，您的連線提供者會為您設定和管理路由。</span><span class="sxs-lookup"><span data-stu-id="af17f-164">If you're using a service provider that offers managed layer 3 services (typically an IP VPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>
> 
> 

### <a name="7-link-a-virtual-network-to-an-expressroute-circuit"></a><span data-ttu-id="af17f-165">7.將虛擬網路連結到 ExpressRoute 線路</span><span class="sxs-lookup"><span data-stu-id="af17f-165">7. Link a virtual network to an ExpressRoute circuit</span></span>
<span data-ttu-id="af17f-166">接下來，將虛擬網路連結到 ExpressRoute 線路。</span><span class="sxs-lookup"><span data-stu-id="af17f-166">Next, link a virtual network to your ExpressRoute circuit.</span></span> <span data-ttu-id="af17f-167">當使用 Resource Manager 部署模型時，使用[將虛擬網路連結到 ExpressRoute 線路](expressroute-howto-linkvnet-arm.md)文章。</span><span class="sxs-lookup"><span data-stu-id="af17f-167">Use the [Linking virtual networks to ExpressRoute circuits](expressroute-howto-linkvnet-arm.md) article when you work with the Resource Manager deployment model.</span></span>

## <a name="getting-the-status-of-an-expressroute-circuit"></a><span data-ttu-id="af17f-168">取得 ExpressRoute 線路的狀態</span><span class="sxs-lookup"><span data-stu-id="af17f-168">Getting the status of an ExpressRoute circuit</span></span>
<span data-ttu-id="af17f-169">選取線路，即可檢視該線路的狀態。</span><span class="sxs-lookup"><span data-stu-id="af17f-169">You can view the status of a circuit by selecting it.</span></span> 

![ExpressRoute 線路的狀態](./media/expressroute-howto-circuit-portal-resource-manager/listproperties1.png)

## <a name="modifying-an-expressroute-circuit"></a><span data-ttu-id="af17f-171">修改 ExpressRoute 線路</span><span class="sxs-lookup"><span data-stu-id="af17f-171">Modifying an ExpressRoute circuit</span></span>
<span data-ttu-id="af17f-172">您可以修改 ExpressRoute 線路的某些屬性，而不會影響連線。</span><span class="sxs-lookup"><span data-stu-id="af17f-172">You can modify certain properties of an ExpressRoute circuit without impacting connectivity.</span></span>

<span data-ttu-id="af17f-173">您可以執行下列工作，而無需中途停機：</span><span class="sxs-lookup"><span data-stu-id="af17f-173">You can do the following with no downtime:</span></span>

* <span data-ttu-id="af17f-174">啟用或停用 ExpressRoute 線路的 ExpressRoute 進階附加元件。</span><span class="sxs-lookup"><span data-stu-id="af17f-174">Enable or disable an ExpressRoute premium add-on for your ExpressRoute circuit.</span></span>
* <span data-ttu-id="af17f-175">只要連接埠有可用的容量，就增加 ExpressRoute 線路的頻寬。</span><span class="sxs-lookup"><span data-stu-id="af17f-175">Increase the bandwidth of your ExpressRoute circuit provided there is capacity available on the port.</span></span> <span data-ttu-id="af17f-176">請注意，不支援將線路的頻寬降級。</span><span class="sxs-lookup"><span data-stu-id="af17f-176">Note that downgrading the bandwidth of a circuit is not supported.</span></span> 
* <span data-ttu-id="af17f-177">將計量方案從 [計量付費] 變更為 [無限制]。</span><span class="sxs-lookup"><span data-stu-id="af17f-177">Change the metering plan from Metered Data to Unlimited Data.</span></span> <span data-ttu-id="af17f-178">請注意，不支援將計量方案從 [無限制] 變更為 [計量付費]。</span><span class="sxs-lookup"><span data-stu-id="af17f-178">Note that changing the metering plan from Unlimited Data to Metered Data is not supported.</span></span>
* <span data-ttu-id="af17f-179">您可以啟用和停用 [允許傳統作業]。</span><span class="sxs-lookup"><span data-stu-id="af17f-179">You can enable and disable *Allow Classic Operations*.</span></span>

<span data-ttu-id="af17f-180">如需限制的詳細資訊，請參閱 [ExpressRoute 常見問題集](expressroute-faqs.md)。</span><span class="sxs-lookup"><span data-stu-id="af17f-180">For more information on limits and limitations, refer to the [ExpressRoute FAQ](expressroute-faqs.md).</span></span>

<span data-ttu-id="af17f-181">若要修改 ExpressRoute 線路，請按一下 [設定]，如下圖所示。</span><span class="sxs-lookup"><span data-stu-id="af17f-181">To modify an ExpressRoute circuit, click on the **Configuration** as shown in the figure below.</span></span>

![修改線路](./media/expressroute-howto-circuit-portal-resource-manager/modifycircuit.png)

<span data-ttu-id="af17f-183">您可以在 [設定] 刀鋒視窗中修改頻寬、SKU、計費模型並允許傳統作業。</span><span class="sxs-lookup"><span data-stu-id="af17f-183">You can modify the bandwidth, SKU, billing model and allow classic operations within the configuration blade.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="af17f-184">如果現有的連接埠上沒有足夠的容量，您可能必須重新建立 ExpressRoute 線路。</span><span class="sxs-lookup"><span data-stu-id="af17f-184">You may have to recreate the ExpressRoute circuit if there is inadequate capacity on the existing port.</span></span> <span data-ttu-id="af17f-185">如果該位置已無額外的容量，您無法升級線路。</span><span class="sxs-lookup"><span data-stu-id="af17f-185">You cannot upgrade the circuit if there is no additional capacity available at that location.</span></span>
>
> <span data-ttu-id="af17f-186">降低 ExpressRoute 線路的頻寬時必須中斷運作。</span><span class="sxs-lookup"><span data-stu-id="af17f-186">You cannot reduce the bandwidth of an ExpressRoute circuit without disruption.</span></span> <span data-ttu-id="af17f-187">頻寬降級需要取消佈建 ExpressRoute 線路，然後重新佈建新的 ExpressRoute 線路。</span><span class="sxs-lookup"><span data-stu-id="af17f-187">Downgrading bandwidth requires you to deprovision the ExpressRoute circuit and then reprovision a new ExpressRoute circuit.</span></span>
> 
> <span data-ttu-id="af17f-188">如果您使用的資源超出標準線路所允許的數量，停用進階附加元件作業可能會失敗。</span><span class="sxs-lookup"><span data-stu-id="af17f-188">Disable premium add-on operation can fail if you're using resources that are greater than what is permitted for the standard circuit.</span></span>
> 
> 

## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a><span data-ttu-id="af17f-189">取消佈建和刪除 ExpressRoute 線路</span><span class="sxs-lookup"><span data-stu-id="af17f-189">Deprovisioning and deleting an ExpressRoute circuit</span></span>
<span data-ttu-id="af17f-190">您可以選取**刪除**圖示，刪除 ExpressRoute 線路。</span><span class="sxs-lookup"><span data-stu-id="af17f-190">You can delete your ExpressRoute circuit by selecting the **delete** icon.</span></span> <span data-ttu-id="af17f-191">請注意：</span><span class="sxs-lookup"><span data-stu-id="af17f-191">Note the following:</span></span>

* <span data-ttu-id="af17f-192">您必須取消連結 ExpressRoute 線路的所有虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="af17f-192">You must unlink all virtual networks from the ExpressRoute circuit.</span></span> <span data-ttu-id="af17f-193">如果此操作失敗，請檢查您是否有任何虛擬網路連結至線路。</span><span class="sxs-lookup"><span data-stu-id="af17f-193">If this operation fails, check whether any virtual networks are linked to the circuit.</span></span>
* <span data-ttu-id="af17f-194">如果 ExpressRoute 線路服務提供者佈建狀態為「正在佈建」或「已佈建」，您就必須與服務提供者一起合作，取消佈建他們那邊的線路。</span><span class="sxs-lookup"><span data-stu-id="af17f-194">If the ExpressRoute circuit service provider provisioning state is **Provisioning** or **Provisioned** you must work with your service provider to deprovision the circuit on their side.</span></span> <span data-ttu-id="af17f-195">我們將繼續保留資源並向您收取費用，直到線路服務提供者完成取消佈建並通知我們。</span><span class="sxs-lookup"><span data-stu-id="af17f-195">We will continue to reserve resources and bill you until the service provider completes deprovisioning the circuit and notifies us.</span></span>
* <span data-ttu-id="af17f-196">若服務提供者已取消佈建線路 (服務提供者佈建狀態設定為 [NotProvisioned] )，則您可以刪除線路。</span><span class="sxs-lookup"><span data-stu-id="af17f-196">If the service provider has deprovisioned the circuit (the service provider provisioning state is set to **Not provisioned**) you can then delete the circuit.</span></span> <span data-ttu-id="af17f-197">這樣將會停止針對線路計費</span><span class="sxs-lookup"><span data-stu-id="af17f-197">This will stop billing for the circuit</span></span>

## <a name="next-steps"></a><span data-ttu-id="af17f-198">後續步驟</span><span class="sxs-lookup"><span data-stu-id="af17f-198">Next steps</span></span>
<span data-ttu-id="af17f-199">建立好線路後，請務必執行下列作業：</span><span class="sxs-lookup"><span data-stu-id="af17f-199">After you create your circuit, make sure that you do the following:</span></span>

* [<span data-ttu-id="af17f-200">建立和修改 ExpressRoute 線路的路由</span><span class="sxs-lookup"><span data-stu-id="af17f-200">Create and modify routing for your ExpressRoute circuit</span></span>](expressroute-howto-routing-portal-resource-manager.md)
* [<span data-ttu-id="af17f-201">將虛擬網路連結至 ExpressRoute 線路</span><span class="sxs-lookup"><span data-stu-id="af17f-201">Link your virtual network to your ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-arm.md)

