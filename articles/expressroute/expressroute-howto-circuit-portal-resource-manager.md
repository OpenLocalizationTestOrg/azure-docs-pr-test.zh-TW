---
title: "建立與修改 ExpressRoute 線路：Azure 入口網站 | Microsoft Docs"
description: "本文說明如何 toocreate，佈建、 驗證、 更新、 刪除和取消佈建 ExpressRoute 電路。"
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
ms.openlocfilehash: 200418aed6bdebace43a2f57cf532d1c8d13cb83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-an-expressroute-circuit"></a><span data-ttu-id="d2310-103">建立和修改 ExpressRoute 線路</span><span class="sxs-lookup"><span data-stu-id="d2310-103">Create and modify an ExpressRoute circuit</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d2310-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="d2310-104">Azure portal</span></span>](expressroute-howto-circuit-portal-resource-manager.md)
> * [<span data-ttu-id="d2310-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d2310-105">PowerShell</span></span>](expressroute-howto-circuit-arm.md)
> * [<span data-ttu-id="d2310-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="d2310-106">Azure CLI</span></span>](howto-circuit-cli.md)
> * [<span data-ttu-id="d2310-107">影片 - Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="d2310-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [<span data-ttu-id="d2310-108">PowerShell (傳統)</span><span class="sxs-lookup"><span data-stu-id="d2310-108">PowerShell (classic)</span></span>](expressroute-howto-circuit-classic.md)
>

<span data-ttu-id="d2310-109">本文說明如何使用 Azure ExpressRoute 電路 toocreate hello Azure 入口網站與 hello Azure Resource Manager 部署模型。</span><span class="sxs-lookup"><span data-stu-id="d2310-109">This article describes how toocreate an Azure ExpressRoute circuit by using hello Azure portal and hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="d2310-110">hello 下列步驟也會顯示 hello 電路 toocheck hello 狀態如何更新，或刪除，並取消佈建它。</span><span class="sxs-lookup"><span data-stu-id="d2310-110">hello following steps also show you how toocheck hello status of hello circuit, update it, or delete and deprovision it.</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="d2310-111">開始之前</span><span class="sxs-lookup"><span data-stu-id="d2310-111">Before you begin</span></span>
* <span data-ttu-id="d2310-112">檢閱 hello[必要條件](expressroute-prerequisites.md)和[工作流程](expressroute-workflows.md)開始設定之前。</span><span class="sxs-lookup"><span data-stu-id="d2310-112">Review hello [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="d2310-113">請確定您有存取 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="d2310-113">Ensure that you have access toohello [Azure portal](https://portal.azure.com).</span></span>
* <span data-ttu-id="d2310-114">確定您有權限 toocreate 新網路功能資源。</span><span class="sxs-lookup"><span data-stu-id="d2310-114">Ensure that you have permissions toocreate new networking resources.</span></span> <span data-ttu-id="d2310-115">如果您沒有 hello 正確的權限，請連絡您的帳戶管理員。</span><span class="sxs-lookup"><span data-stu-id="d2310-115">Contact your account administrator if you do not have hello right permissions.</span></span>
* <span data-ttu-id="d2310-116">您可以[觀賞視訊](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)順序的開頭之前 toobetter 了解 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="d2310-116">You can [view a video](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit) before beginning in order toobetter understand hello steps.</span></span>

## <a name="create-and-provision-an-expressroute-circuit"></a><span data-ttu-id="d2310-117">建立和佈建 ExpressRoute 線路</span><span class="sxs-lookup"><span data-stu-id="d2310-117">Create and provision an ExpressRoute circuit</span></span>
### <a name="1-sign-in-toohello-azure-portal"></a><span data-ttu-id="d2310-118">1.登入 toohello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="d2310-118">1. Sign in toohello Azure portal</span></span>
<span data-ttu-id="d2310-119">從瀏覽器中，瀏覽 toohello [Azure 入口網站](http://portal.azure.com)並以您的 Azure 帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="d2310-119">From a browser, navigate toohello [Azure portal](http://portal.azure.com) and sign in with your Azure account.</span></span>

### <a name="2-create-a-new-expressroute-circuit"></a><span data-ttu-id="d2310-120">2.建立新的 ExpressRoute 線路</span><span class="sxs-lookup"><span data-stu-id="d2310-120">2. Create a new ExpressRoute circuit</span></span>
> [!IMPORTANT]
> <span data-ttu-id="d2310-121">ExpressRoute 電路將計費 hello 發出服務金鑰的時間。</span><span class="sxs-lookup"><span data-stu-id="d2310-121">Your ExpressRoute circuit will be billed from hello moment a service key is issued.</span></span> <span data-ttu-id="d2310-122">請確定您執行此作業，準備好 tooprovision hello 電路 hello 連線服務提供者時。</span><span class="sxs-lookup"><span data-stu-id="d2310-122">Ensure that you perform this operation when hello connectivity provider is ready tooprovision hello circuit.</span></span>
> 
> 

1. <span data-ttu-id="d2310-123">您可以藉由選取 hello 選項 toocreate 建立 ExpressRoute 電路，新的資源。</span><span class="sxs-lookup"><span data-stu-id="d2310-123">You can create an ExpressRoute circuit by selecting hello option toocreate a new resource.</span></span> <span data-ttu-id="d2310-124">按一下**新增** > **網路** > **ExpressRoute**hello 下列影像所示：</span><span class="sxs-lookup"><span data-stu-id="d2310-124">Click **New** > **Networking** > **ExpressRoute**, as shown in hello following image:</span></span>
   
    ![建立 ExpressRoute 線路](./media/expressroute-howto-circuit-portal-resource-manager/createcircuit1.png)
2. <span data-ttu-id="d2310-126">按一下 之後**ExpressRoute**，您會看到 hello**建立 ExpressRoute 電路**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="d2310-126">After you click **ExpressRoute**, you'll see hello **Create ExpressRoute circuit** blade.</span></span> <span data-ttu-id="d2310-127">當您要填入此刀鋒視窗上的 hello 值時，請確定您指定 hello 正確 SKU 層和資料計量。</span><span class="sxs-lookup"><span data-stu-id="d2310-127">When you're filling in hello values on this blade, make sure that you specify hello correct SKU tier and data metering.</span></span>
   
   * <span data-ttu-id="d2310-128"> 決定要啟用 ExpressRoute 標準或 ExpressRoute 進階附加元件。</span><span class="sxs-lookup"><span data-stu-id="d2310-128">**Tier** determines whether an ExpressRoute standard or an ExpressRoute premium add-on is enabled.</span></span> <span data-ttu-id="d2310-129">您可以指定**標準**tooget hello 標準 SKU 或**Premium** hello premium 附加元件。</span><span class="sxs-lookup"><span data-stu-id="d2310-129">You can specify **Standard** tooget hello standard SKU or **Premium** for hello premium add-on.</span></span>
   * <span data-ttu-id="d2310-130">**資料計量**決定 hello 計費的型別。</span><span class="sxs-lookup"><span data-stu-id="d2310-130">**Data metering** determines hello billing type.</span></span> <span data-ttu-id="d2310-131">您可以指定 [計量付費] 以採用計量付費數據傳輸方案，選取 [無限制] 以採用無限制的資料方案。</span><span class="sxs-lookup"><span data-stu-id="d2310-131">You can specify **Metered** for a metered data plan and **Unlimited** for an unlimited data plan.</span></span> <span data-ttu-id="d2310-132">請注意，您可以變更從 hello 計費類型**Metered**太**Unlimited**，但您無法變更 hello 類型從**無限制**太**Metered**.</span><span class="sxs-lookup"><span data-stu-id="d2310-132">Note that you can change hello billing type from **Metered** too**Unlimited**, but you can't change hello type from **Unlimited** too**Metered**.</span></span>
     
     ![設定 hello SKU 層和計量資料](./media/expressroute-howto-circuit-portal-resource-manager/createcircuit2.png)

> [!IMPORTANT]
> <span data-ttu-id="d2310-134">請留意對等互連位置該 hello 指出 hello[實體位置](expressroute-locations.md)您與 Microsoft 的互連位置。</span><span class="sxs-lookup"><span data-stu-id="d2310-134">Please be aware that hello Peering Location indicates hello [physical location](expressroute-locations.md) where you are peering with Microsoft.</span></span> <span data-ttu-id="d2310-135">這是**不**太連結 「 位置 」 屬性，是指 toohello hello Azure 網路資源提供者所在的地理位置。</span><span class="sxs-lookup"><span data-stu-id="d2310-135">This is **not** linked too"Location" property, which refers toohello geography where hello Azure Network Resource Provider is located.</span></span> <span data-ttu-id="d2310-136">雖然無關，它是很好的作法 toochoose 網路資源提供者關閉地理 toohello hello 循環的對等互連位置。</span><span class="sxs-lookup"><span data-stu-id="d2310-136">While they are not related, it is a good practice toochoose a Network Resource Provider geographically close toohello Peering Location of hello circuit.</span></span> 
> 
> 

### <a name="3-view-hello-circuits-and-properties"></a><span data-ttu-id="d2310-137">3.檢視 hello 電路和屬性</span><span class="sxs-lookup"><span data-stu-id="d2310-137">3. View hello circuits and properties</span></span>
<span data-ttu-id="d2310-138">**檢視所有 hello 電路**</span><span class="sxs-lookup"><span data-stu-id="d2310-138">**View all hello circuits**</span></span>

<span data-ttu-id="d2310-139">您可以檢視所有您建立選取的 hello 電路**所有資源**hello 左側功能表上。</span><span class="sxs-lookup"><span data-stu-id="d2310-139">You can view all hello circuits that you created by selecting **All resources** on hello left-side menu.</span></span>

![檢視線路](./media/expressroute-howto-circuit-portal-resource-manager/listresource.png)

<span data-ttu-id="d2310-141">**檢視 hello 屬性**</span><span class="sxs-lookup"><span data-stu-id="d2310-141">**View hello properties**</span></span>

    You can view hello properties of hello circuit by selecting it. On this blade, note hello service key for hello circuit. You must copy hello circuit key for your circuit and pass it down toohello service provider toocomplete hello provisioning process. hello circuit key is specific tooyour circuit.

![檢視屬性](./media/expressroute-howto-circuit-portal-resource-manager/listproperties1.png)

### <a name="4-send-hello-service-key-tooyour-connectivity-provider-for-provisioning"></a><span data-ttu-id="d2310-143">4.佈建傳送嗨服務金鑰 tooyour 連線服務提供者</span><span class="sxs-lookup"><span data-stu-id="d2310-143">4. Send hello service key tooyour connectivity provider for provisioning</span></span>
<span data-ttu-id="d2310-144">在這個刀鋒視窗中，**提供者狀態**提供 hello 的佈建 hello 服務提供者端的目前狀態的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="d2310-144">On this blade, **Provider status** provides information on hello current state of provisioning on hello service-provider side.</span></span> <span data-ttu-id="d2310-145">**電路狀態**hello Microsoft 側邊提供 hello 狀態。</span><span class="sxs-lookup"><span data-stu-id="d2310-145">**Circuit status** provides hello state on hello Microsoft side.</span></span> <span data-ttu-id="d2310-146">如需循環的佈建狀態的詳細資訊，請參閱 hello[工作流程](expressroute-workflows.md#expressroute-circuit-provisioning-states)發行項。</span><span class="sxs-lookup"><span data-stu-id="d2310-146">For more information about circuit provisioning states, see hello [Workflows](expressroute-workflows.md#expressroute-circuit-provisioning-states) article.</span></span>

<span data-ttu-id="d2310-147">當您建立新的 ExpressRoute 電路時，hello 電路將處於下列狀態的 hello:</span><span class="sxs-lookup"><span data-stu-id="d2310-147">When you create a new ExpressRoute circuit, hello circuit will be in hello following state:</span></span>

<span data-ttu-id="d2310-148">提供者狀態︰未佈建</span><span class="sxs-lookup"><span data-stu-id="d2310-148">Provider status: Not provisioned</span></span><BR>
<span data-ttu-id="d2310-149">線路狀態：已啟用</span><span class="sxs-lookup"><span data-stu-id="d2310-149">Circuit status: Enabled</span></span>

![起始佈建程序](./media/expressroute-howto-circuit-portal-resource-manager/viewstatus.png)

<span data-ttu-id="d2310-151">hello 循環會變更 toohello hello 連線服務提供者會在您啟用的 hello 程序中時，下列狀態：</span><span class="sxs-lookup"><span data-stu-id="d2310-151">hello circuit will change toohello following state when hello connectivity provider is in hello process of enabling it for you:</span></span>

<span data-ttu-id="d2310-152">提供者狀態︰正在佈建</span><span class="sxs-lookup"><span data-stu-id="d2310-152">Provider status: Provisioning</span></span><BR>
<span data-ttu-id="d2310-153">線路狀態：已啟用</span><span class="sxs-lookup"><span data-stu-id="d2310-153">Circuit status: Enabled</span></span>

<span data-ttu-id="d2310-154">您 toobe 無法 toouse ExpressRoute 電路，它必須處於下列狀態的 hello:</span><span class="sxs-lookup"><span data-stu-id="d2310-154">For you toobe able toouse an ExpressRoute circuit, it must be in hello following state:</span></span>

<span data-ttu-id="d2310-155">提供者狀態︰已佈建</span><span class="sxs-lookup"><span data-stu-id="d2310-155">Provider status: Provisioned</span></span><BR>
<span data-ttu-id="d2310-156">線路狀態：已啟用</span><span class="sxs-lookup"><span data-stu-id="d2310-156">Circuit status: Enabled</span></span>

### <a name="5-periodically-check-hello-status-and-hello-state-of-hello-circuit-key"></a><span data-ttu-id="d2310-157">5.定期檢查 hello 狀態和 hello 循環索引鍵 hello 狀態</span><span class="sxs-lookup"><span data-stu-id="d2310-157">5. Periodically check hello status and hello state of hello circuit key</span></span>
<span data-ttu-id="d2310-158">您可以檢視由選取感興趣的 hello 循環的 hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="d2310-158">You can view hello properties of hello circuit that you're interested in by selecting it.</span></span> <span data-ttu-id="d2310-159">檢查 hello**提供者狀態**，並確定它已移動過**已佈建**繼續進行之前。</span><span class="sxs-lookup"><span data-stu-id="d2310-159">Check hello **Provider status** and ensure that it has moved too**Provisioned** before you continue.</span></span>

![線路和提供者狀態](./media/expressroute-howto-circuit-portal-resource-manager/viewstatusprovisioned.png)

### <a name="6-create-your-routing-configuration"></a><span data-ttu-id="d2310-161">6.建立路由組態</span><span class="sxs-lookup"><span data-stu-id="d2310-161">6. Create your routing configuration</span></span>
<span data-ttu-id="d2310-162">如需逐步指示，請參閱 toohello [ExpressRoute 電路的路由組態](expressroute-howto-routing-portal-resource-manager.md)文章 toocreate 和修改循環的對等互連。</span><span class="sxs-lookup"><span data-stu-id="d2310-162">For step-by-step instructions, refer toohello [ExpressRoute circuit routing configuration](expressroute-howto-routing-portal-resource-manager.md) article toocreate and modify circuit peerings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d2310-163">這些說明僅適用於 toocircuits 與提供層級 2 連線服務的服務提供者所建立。</span><span class="sxs-lookup"><span data-stu-id="d2310-163">These instructions only apply toocircuits that are created with service providers that offer layer 2 connectivity services.</span></span> <span data-ttu-id="d2310-164">如果您使用的服務提供者是提供受管理的第 3 層服務 (通常是 IP VPN，如 MPLS)，您的連線提供者會為您設定和管理路由。</span><span class="sxs-lookup"><span data-stu-id="d2310-164">If you're using a service provider that offers managed layer 3 services (typically an IP VPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>
> 
> 

### <a name="7-link-a-virtual-network-tooan-expressroute-circuit"></a><span data-ttu-id="d2310-165">7.連結虛擬網路 tooan ExpressRoute 電路</span><span class="sxs-lookup"><span data-stu-id="d2310-165">7. Link a virtual network tooan ExpressRoute circuit</span></span>
<span data-ttu-id="d2310-166">接下來，將虛擬網路 tooyour ExpressRoute 電路的連結。</span><span class="sxs-lookup"><span data-stu-id="d2310-166">Next, link a virtual network tooyour ExpressRoute circuit.</span></span> <span data-ttu-id="d2310-167">使用 hello[連結虛擬網路 tooExpressRoute 電路](expressroute-howto-linkvnet-arm.md)處理 hello Resource Manager 部署模型時，發行項。</span><span class="sxs-lookup"><span data-stu-id="d2310-167">Use hello [Linking virtual networks tooExpressRoute circuits](expressroute-howto-linkvnet-arm.md) article when you work with hello Resource Manager deployment model.</span></span>

## <a name="getting-hello-status-of-an-expressroute-circuit"></a><span data-ttu-id="d2310-168">取得 hello 狀態的 ExpressRoute 電路</span><span class="sxs-lookup"><span data-stu-id="d2310-168">Getting hello status of an ExpressRoute circuit</span></span>
<span data-ttu-id="d2310-169">您可以藉由選取檢視 hello 的循環的狀態。</span><span class="sxs-lookup"><span data-stu-id="d2310-169">You can view hello status of a circuit by selecting it.</span></span> 

![ExpressRoute 線路的狀態](./media/expressroute-howto-circuit-portal-resource-manager/listproperties1.png)

## <a name="modifying-an-expressroute-circuit"></a><span data-ttu-id="d2310-171">修改 ExpressRoute 線路</span><span class="sxs-lookup"><span data-stu-id="d2310-171">Modifying an ExpressRoute circuit</span></span>
<span data-ttu-id="d2310-172">您可以修改 ExpressRoute 線路的某些屬性，而不會影響連線。</span><span class="sxs-lookup"><span data-stu-id="d2310-172">You can modify certain properties of an ExpressRoute circuit without impacting connectivity.</span></span>

<span data-ttu-id="d2310-173">您可以 hello 遵循不中斷的情況：</span><span class="sxs-lookup"><span data-stu-id="d2310-173">You can do hello following with no downtime:</span></span>

* <span data-ttu-id="d2310-174">啟用或停用 ExpressRoute 線路的 ExpressRoute 進階附加元件。</span><span class="sxs-lookup"><span data-stu-id="d2310-174">Enable or disable an ExpressRoute premium add-on for your ExpressRoute circuit.</span></span>
* <span data-ttu-id="d2310-175">增加 hello 頻寬的 ExpressRoute 電路提供 hello 連接埠的容量不足。</span><span class="sxs-lookup"><span data-stu-id="d2310-175">Increase hello bandwidth of your ExpressRoute circuit provided there is capacity available on hello port.</span></span> <span data-ttu-id="d2310-176">請注意，不支援降級 hello 電路頻寬。</span><span class="sxs-lookup"><span data-stu-id="d2310-176">Note that downgrading hello bandwidth of a circuit is not supported.</span></span> 
* <span data-ttu-id="d2310-177">變更計量計劃的計量資料 tooUnlimited 資料 hello。</span><span class="sxs-lookup"><span data-stu-id="d2310-177">Change hello metering plan from Metered Data tooUnlimited Data.</span></span> <span data-ttu-id="d2310-178">請注意該變更 hello 計量計劃從無限制的資料 tooMetered 不支援資料。</span><span class="sxs-lookup"><span data-stu-id="d2310-178">Note that changing hello metering plan from Unlimited Data tooMetered Data is not supported.</span></span>
* <span data-ttu-id="d2310-179">您可以啟用和停用 [允許傳統作業]。</span><span class="sxs-lookup"><span data-stu-id="d2310-179">You can enable and disable *Allow Classic Operations*.</span></span>

<span data-ttu-id="d2310-180">如需有關限制和限制的詳細資訊，請參閱 toohello [ExpressRoute 常見問題集](expressroute-faqs.md)。</span><span class="sxs-lookup"><span data-stu-id="d2310-180">For more information on limits and limitations, refer toohello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>

<span data-ttu-id="d2310-181">toomodify ExpressRoute 循環中，按一下 hello**組態**hello 圖所示。</span><span class="sxs-lookup"><span data-stu-id="d2310-181">toomodify an ExpressRoute circuit, click on hello **Configuration** as shown in hello figure below.</span></span>

![修改線路](./media/expressroute-howto-circuit-portal-resource-manager/modifycircuit.png)

<span data-ttu-id="d2310-183">您可以修改 hello 頻寬、 SKU，計費模型，並允許傳統 hello 組態刀鋒視窗中的作業。</span><span class="sxs-lookup"><span data-stu-id="d2310-183">You can modify hello bandwidth, SKU, billing model and allow classic operations within hello configuration blade.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d2310-184">如果 hello 現有的連接埠上有足夠的容量，您可能必須 toorecreate hello ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="d2310-184">You may have toorecreate hello ExpressRoute circuit if there is inadequate capacity on hello existing port.</span></span> <span data-ttu-id="d2310-185">如果沒有任何額外的容量可在該位置，您無法升級 hello 循環。</span><span class="sxs-lookup"><span data-stu-id="d2310-185">You cannot upgrade hello circuit if there is no additional capacity available at that location.</span></span>
>
> <span data-ttu-id="d2310-186">您無法減少 hello 頻寬的 ExpressRoute 電路不會中斷。</span><span class="sxs-lookup"><span data-stu-id="d2310-186">You cannot reduce hello bandwidth of an ExpressRoute circuit without disruption.</span></span> <span data-ttu-id="d2310-187">降級頻寬 toodeprovision hello ExpressRoute 循環會要求您，並再重新佈建新增的 ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="d2310-187">Downgrading bandwidth requires you toodeprovision hello ExpressRoute circuit and then reprovision a new ExpressRoute circuit.</span></span>
> 
> <span data-ttu-id="d2310-188">停用 premium add-on 作業可能會失敗，如果您使用大於 hello 標準循環所允許的資源。</span><span class="sxs-lookup"><span data-stu-id="d2310-188">Disable premium add-on operation can fail if you're using resources that are greater than what is permitted for hello standard circuit.</span></span>
> 
> 

## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a><span data-ttu-id="d2310-189">取消佈建和刪除 ExpressRoute 線路</span><span class="sxs-lookup"><span data-stu-id="d2310-189">Deprovisioning and deleting an ExpressRoute circuit</span></span>
<span data-ttu-id="d2310-190">您可以藉由選取 hello 刪除 ExpressRoute 電路**刪除**圖示。</span><span class="sxs-lookup"><span data-stu-id="d2310-190">You can delete your ExpressRoute circuit by selecting hello **delete** icon.</span></span> <span data-ttu-id="d2310-191">請注意 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="d2310-191">Note hello following:</span></span>

* <span data-ttu-id="d2310-192">您必須取消連結從 hello ExpressRoute 電路的所有虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="d2310-192">You must unlink all virtual networks from hello ExpressRoute circuit.</span></span> <span data-ttu-id="d2310-193">如果此作業失敗，請檢查是否已連結的任何虛擬網路 toohello 循環。</span><span class="sxs-lookup"><span data-stu-id="d2310-193">If this operation fails, check whether any virtual networks are linked toohello circuit.</span></span>
* <span data-ttu-id="d2310-194">如果 hello ExpressRoute 電路服務提供者佈建狀態為**佈建**或**已佈建**您必須使用您的服務提供者 toodeprovision hello 電路邊。</span><span class="sxs-lookup"><span data-stu-id="d2310-194">If hello ExpressRoute circuit service provider provisioning state is **Provisioning** or **Provisioned** you must work with your service provider toodeprovision hello circuit on their side.</span></span> <span data-ttu-id="d2310-195">我們將繼續 tooreserve 資源，並向您收取費用，直到完成取消佈建 hello 電路 hello 服務提供者，並通知我們。</span><span class="sxs-lookup"><span data-stu-id="d2310-195">We will continue tooreserve resources and bill you until hello service provider completes deprovisioning hello circuit and notifies us.</span></span>
* <span data-ttu-id="d2310-196">如果 hello 服務提供者已解除佈建 hello 循環 (hello 佈建狀態的服務提供者設定得**未佈建**) 可接著刪除 hello 循環。</span><span class="sxs-lookup"><span data-stu-id="d2310-196">If hello service provider has deprovisioned hello circuit (hello service provider provisioning state is set too**Not provisioned**) you can then delete hello circuit.</span></span> <span data-ttu-id="d2310-197">這會停止計費 hello 循環</span><span class="sxs-lookup"><span data-stu-id="d2310-197">This will stop billing for hello circuit</span></span>

## <a name="next-steps"></a><span data-ttu-id="d2310-198">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d2310-198">Next steps</span></span>
<span data-ttu-id="d2310-199">建立您的循環之後，請確定您執行 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="d2310-199">After you create your circuit, make sure that you do hello following:</span></span>

* [<span data-ttu-id="d2310-200">建立和修改 ExpressRoute 線路的路由</span><span class="sxs-lookup"><span data-stu-id="d2310-200">Create and modify routing for your ExpressRoute circuit</span></span>](expressroute-howto-routing-portal-resource-manager.md)
* [<span data-ttu-id="d2310-201">連結您的虛擬網路 tooyour ExpressRoute 電路</span><span class="sxs-lookup"><span data-stu-id="d2310-201">Link your virtual network tooyour ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-arm.md)

