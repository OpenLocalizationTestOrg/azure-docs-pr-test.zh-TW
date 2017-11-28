---
title: "虛擬網路 tooan ExpressRoute 電路的連結： Azure 入口網站 |Microsoft 文件"
description: "本文件提供如何 toolink 虛擬網路 (Vnet) tooExpressRoute 電路的概觀。"
services: expressroute
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f5cb5441-2fba-46d9-99a5-d1d586e7bda4
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: cherylmc
ms.openlocfilehash: 8bedcb11df7e30281fd439afdfb76cc67626a8f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-virtual-network-tooan-expressroute-circuit"></a><span data-ttu-id="563c0-103">連接虛擬網路 tooan ExpressRoute 電路</span><span class="sxs-lookup"><span data-stu-id="563c0-103">Connect a virtual network tooan ExpressRoute circuit</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="563c0-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="563c0-104">Azure portal</span></span>](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [<span data-ttu-id="563c0-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="563c0-105">PowerShell</span></span>](expressroute-howto-linkvnet-arm.md)
> * [<span data-ttu-id="563c0-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="563c0-106">Azure CLI</span></span>](howto-linkvnet-cli.md)
> * [<span data-ttu-id="563c0-107">影片 - Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="563c0-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [<span data-ttu-id="563c0-108">PowerShell (傳統)</span><span class="sxs-lookup"><span data-stu-id="563c0-108">PowerShell (classic)</span></span>](expressroute-howto-linkvnet-classic.md)
> 

<span data-ttu-id="563c0-109">這篇文章可協助您將虛擬網路 (Vnet) tooAzure ExpressRoute 電路連結使用 hello Resource Manager 部署模型並 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="563c0-109">This article helps you link virtual networks (VNets) tooAzure ExpressRoute circuits by using hello Resource Manager deployment model and hello Azure portal.</span></span> <span data-ttu-id="563c0-110">虛擬網路可以在 hello 相同的訂用帳戶，或它們可以是另一個訂用帳戶的一部分。</span><span class="sxs-lookup"><span data-stu-id="563c0-110">Virtual networks can either be in hello same subscription, or they can be part of another subscription.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="563c0-111">開始之前</span><span class="sxs-lookup"><span data-stu-id="563c0-111">Before you begin</span></span>
* <span data-ttu-id="563c0-112">檢閱 hello[必要條件](expressroute-prerequisites.md)，[路由需求](expressroute-routing.md)，和[工作流程](expressroute-workflows.md)開始設定之前。</span><span class="sxs-lookup"><span data-stu-id="563c0-112">Review hello [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="563c0-113">您必須擁有作用中的 ExpressRoute 線路。</span><span class="sxs-lookup"><span data-stu-id="563c0-113">You must have an active ExpressRoute circuit.</span></span>
  
  * <span data-ttu-id="563c0-114">請依照下列指示 hello 太[建立 ExpressRoute 電路](expressroute-howto-circuit-portal-resource-manager.md)和已啟用連線提供者的 hello 循環。</span><span class="sxs-lookup"><span data-stu-id="563c0-114">Follow hello instructions too[create an ExpressRoute circuit](expressroute-howto-circuit-portal-resource-manager.md) and have hello circuit enabled by your connectivity provider.</span></span>
  * <span data-ttu-id="563c0-115">確定您已針對循環設定了 Azure 私用對等。</span><span class="sxs-lookup"><span data-stu-id="563c0-115">Ensure that you have Azure private peering configured for your circuit.</span></span> <span data-ttu-id="563c0-116">請參閱 hello[設定路由](expressroute-howto-routing-portal-resource-manager.md)路由指示的發行項。</span><span class="sxs-lookup"><span data-stu-id="563c0-116">See hello [Configure routing](expressroute-howto-routing-portal-resource-manager.md) article for routing instructions.</span></span>
  * <span data-ttu-id="563c0-117">請確認 Azure 私用對等設定，且 hello BGP 對等互連網路與 Microsoft 之間，以便您可以啟用端對端連線已啟動。</span><span class="sxs-lookup"><span data-stu-id="563c0-117">Ensure that Azure private peering is configured and hello BGP peering between your network and Microsoft is up so that you can enable end-to-end connectivity.</span></span>
  * <span data-ttu-id="563c0-118">請確定您有已建立且完整佈建的虛擬網路和虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="563c0-118">Ensure that you have a virtual network and a virtual network gateway created and fully provisioned.</span></span> <span data-ttu-id="563c0-119">請依照下列指示 hello 太[建立 expressroute 的虛擬網路閘道](expressroute-howto-add-gateway-resource-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="563c0-119">Follow hello instructions too[create a virtual network gateway for ExpressRoute](expressroute-howto-add-gateway-resource-manager.md).</span></span> <span data-ttu-id="563c0-120">Expressroute 的虛擬網路閘道使用 hello gatewaytype 的授權 'ExpressRoute'，不是 VPN。</span><span class="sxs-lookup"><span data-stu-id="563c0-120">A virtual network gateway for ExpressRoute uses hello GatewayType 'ExpressRoute', not VPN.</span></span>

* <span data-ttu-id="563c0-121">您可以連結 too10 虛擬網路 tooa 標準 ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="563c0-121">You can link up too10 virtual networks tooa standard ExpressRoute circuit.</span></span> <span data-ttu-id="563c0-122">所有虛擬網路必須位於 hello 相同地理政治區域時使用標準的 ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="563c0-122">All virtual networks must be in hello same geopolitical region when using a standard ExpressRoute circuit.</span></span> 
* <span data-ttu-id="563c0-123">您可以連結以外的 hello ExpressRoute 電路的 hello 地緣政治區域虛擬網路或連線較大的虛擬網路 tooyour ExpressRoute 循環數目，如果啟用 hello ExpressRoute premium 附加元件。</span><span class="sxs-lookup"><span data-stu-id="563c0-123">You can link a virtual network outside of hello geopolitical region of hello ExpressRoute circuit, or connect a larger number of virtual networks tooyour ExpressRoute circuit if you enabled hello ExpressRoute premium add-on.</span></span> <span data-ttu-id="563c0-124">檢查 hello[常見問題集](expressroute-faqs.md)如需有關 hello premium 附加元件。</span><span class="sxs-lookup"><span data-stu-id="563c0-124">Check hello [FAQ](expressroute-faqs.md) for more details on hello premium add-on.</span></span>
* <span data-ttu-id="563c0-125">您可以[觀賞視訊](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)開頭 toobetter 了解 hello 步驟之前。</span><span class="sxs-lookup"><span data-stu-id="563c0-125">You can [view a video](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit) before beginning toobetter understand hello steps.</span></span>

## <a name="connect-a-virtual-network-in-hello-same-subscription-tooa-circuit"></a><span data-ttu-id="563c0-126">連接 hello 中的虛擬網路相同的訂用帳戶 tooa 電路</span><span class="sxs-lookup"><span data-stu-id="563c0-126">Connect a virtual network in hello same subscription tooa circuit</span></span>

### <a name="toocreate-a-connection"></a><span data-ttu-id="563c0-127">toocreate 連接</span><span class="sxs-lookup"><span data-stu-id="563c0-127">toocreate a connection</span></span>

> [!NOTE]
> <span data-ttu-id="563c0-128">BGP 組態資訊不會顯示 hello 第 3 層提供者是否設定您的對等互連。</span><span class="sxs-lookup"><span data-stu-id="563c0-128">BGP configuration information will not show up if hello layer 3 provider configured your peerings.</span></span> <span data-ttu-id="563c0-129">如果您的電路位於佈建狀態，您應該能夠 toocreate 連線。</span><span class="sxs-lookup"><span data-stu-id="563c0-129">If your circuit is in a provisioned state, you should be able toocreate connections.</span></span>
>

1. <span data-ttu-id="563c0-130">確認正確設定您的 ExpressRoute 電路和 Azure 私人對等互連。</span><span class="sxs-lookup"><span data-stu-id="563c0-130">Ensure that your ExpressRoute circuit and Azure private peering have been configured successfully.</span></span> <span data-ttu-id="563c0-131">請依照下列中的 hello 指示[建立 ExpressRoute 電路](expressroute-howto-circuit-arm.md)和[設定路由](expressroute-howto-routing-arm.md)。</span><span class="sxs-lookup"><span data-stu-id="563c0-131">Follow hello instructions in [Create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and [Configure routing](expressroute-howto-routing-arm.md).</span></span> <span data-ttu-id="563c0-132">ExpressRoute 電路應該看起來像下列映像的 hello:</span><span class="sxs-lookup"><span data-stu-id="563c0-132">Your ExpressRoute circuit should look like hello following image:</span></span>

    ![刪除 ExpressRoute 線路螢幕擷取畫面](./media/expressroute-howto-linkvnet-portal-resource-manager/routing1.png)
   
2. <span data-ttu-id="563c0-134">您現在可以開始佈建連線 toolink 您虛擬網路閘道 tooyour ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="563c0-134">You can now start provisioning a connection toolink your virtual network gateway tooyour ExpressRoute circuit.</span></span> <span data-ttu-id="563c0-135">按一下**連接** > **新增**tooopen hello**加入連接**刀鋒視窗中，然後設定 hello 值。</span><span class="sxs-lookup"><span data-stu-id="563c0-135">Click **Connection** > **Add** tooopen hello **Add connection** blade, and then configure hello values.</span></span>

    ![新增連線螢幕擷取畫面](./media/expressroute-howto-linkvnet-portal-resource-manager/samesub1.png)  

3. <span data-ttu-id="563c0-137">已成功設定您的連線之後，連線物件會顯示 hello hello 連接資訊。</span><span class="sxs-lookup"><span data-stu-id="563c0-137">After your connection has been successfully configured, your connection object will show hello information for hello connection.</span></span>

     ![連線物件螢幕擷取畫面](./media/expressroute-howto-linkvnet-portal-resource-manager/samesub2.png)

### <a name="toodelete-a-connection"></a><span data-ttu-id="563c0-139">toodelete 連接</span><span class="sxs-lookup"><span data-stu-id="563c0-139">toodelete a connection</span></span>
<span data-ttu-id="563c0-140">您可以刪除的連線，藉由選取 hello**刪除**連線 hello 刀鋒視窗上的圖示。</span><span class="sxs-lookup"><span data-stu-id="563c0-140">You can delete a connection by selecting hello **Delete** icon on hello blade for your connection.</span></span>

## <a name="connect-a-virtual-network-in-a-different-subscription-tooa-circuit"></a><span data-ttu-id="563c0-141">在不同的訂用帳戶 tooa 電路的虛擬網路連線</span><span class="sxs-lookup"><span data-stu-id="563c0-141">Connect a virtual network in a different subscription tooa circuit</span></span>
<span data-ttu-id="563c0-142">您可以讓多個訂用帳戶共用 ExpressRoute 線路。</span><span class="sxs-lookup"><span data-stu-id="563c0-142">You can share an ExpressRoute circuit across multiple subscriptions.</span></span> <span data-ttu-id="563c0-143">hello 下圖顯示簡單圖解如何共用 ExpressRoute 電路的運作方式跨多個訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="563c0-143">hello figure below shows a simple schematic of how sharing works for ExpressRoute circuits across multiple subscriptions.</span></span>

![跨訂用帳戶的連線能力](./media/expressroute-howto-linkvnet-portal-resource-manager/cross-subscription.png)

- <span data-ttu-id="563c0-145">Hello hello 大型雲端內的小型雲端都屬於 toodifferent 部門組織內使用的 toorepresent 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="563c0-145">Each of hello smaller clouds within hello large cloud is used toorepresent subscriptions that belong toodifferent departments within an organization.</span></span>
- <span data-ttu-id="563c0-146">Hello 部門 hello 組織內的每個可以使用自己的訂用帳戶來部署其服務，但它們可以共用單一 ExpressRoute 電路 tooconnect 後 tooyour 在內部部署網路。</span><span class="sxs-lookup"><span data-stu-id="563c0-146">Each of hello departments within hello organization can use their own subscription for deploying their services, but they can share a single ExpressRoute circuit tooconnect back tooyour on-premises network.</span></span>
- <span data-ttu-id="563c0-147">單一部門 (在此範例中： IT) 可以擁有 hello ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="563c0-147">A single department (in this example: IT) can own hello ExpressRoute circuit.</span></span> <span data-ttu-id="563c0-148">Hello 組織內其他訂用帳戶可以使用 hello ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="563c0-148">Other subscriptions within hello organization can use hello ExpressRoute circuit.</span></span>

    > [!NOTE]
    > <span data-ttu-id="563c0-149">Hello 專用循環的連線和頻寬費用將會套用的 toohello ExpressRoute 電路擁有者。</span><span class="sxs-lookup"><span data-stu-id="563c0-149">Connectivity and bandwidth charges for hello dedicated circuit will be applied toohello ExpressRoute circuit owner.</span></span> <span data-ttu-id="563c0-150">所有虛擬網路共用 hello 相同的頻寬。</span><span class="sxs-lookup"><span data-stu-id="563c0-150">All virtual networks share hello same bandwidth.</span></span>
    > 
    >

### <a name="administration---circuit-owners-and-circuit-users"></a><span data-ttu-id="563c0-151">系統管理 - 線路擁有者和線路使用者</span><span class="sxs-lookup"><span data-stu-id="563c0-151">Administration - circuit owners and circuit users</span></span>

<span data-ttu-id="563c0-152">hello '電路擁有者' 是授權的 Power hello ExpressRoute 電路資源的使用者。</span><span class="sxs-lookup"><span data-stu-id="563c0-152">hello 'circuit owner' is an authorized Power User of hello ExpressRoute circuit resource.</span></span> <span data-ttu-id="563c0-153">hello 電路擁有者可以建立可以兌換的 「 循環的使用者 」 的授權。</span><span class="sxs-lookup"><span data-stu-id="563c0-153">hello circuit owner can create authorizations that can be redeemed by 'circuit users'.</span></span> <span data-ttu-id="563c0-154">循環使用者是擁有者的虛擬網路閘道，不在 hello 相同訂用帳戶，因為 hello ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="563c0-154">Circuit users are owners of virtual network gateways that are not within hello same subscription as hello ExpressRoute circuit.</span></span> <span data-ttu-id="563c0-155">電路使用者可以兌換授權 (每個虛擬網路一個授權)。</span><span class="sxs-lookup"><span data-stu-id="563c0-155">Circuit users can redeem authorizations (one authorization per virtual network).</span></span>

<span data-ttu-id="563c0-156">hello 電路擁有者隨時都有 hello 電源 toomodify 和撤銷授權。</span><span class="sxs-lookup"><span data-stu-id="563c0-156">hello circuit owner has hello power toomodify and revoke authorizations at any time.</span></span> <span data-ttu-id="563c0-157">撤銷授權會導致從已撤銷其存取權的 hello 訂用帳戶中刪除所有連結連線。</span><span class="sxs-lookup"><span data-stu-id="563c0-157">Revoking an authorization results in all link connections being deleted from hello subscription whose access was revoked.</span></span>

### <a name="circuit-owner-operations"></a><span data-ttu-id="563c0-158">循環擁有者作業</span><span class="sxs-lookup"><span data-stu-id="563c0-158">Circuit owner operations</span></span>

<span data-ttu-id="563c0-159">**toocreate 連線授權**</span><span class="sxs-lookup"><span data-stu-id="563c0-159">**toocreate a connection authorization**</span></span>

<span data-ttu-id="563c0-160">hello 電路擁有者建立的授權。</span><span class="sxs-lookup"><span data-stu-id="563c0-160">hello circuit owner creates an authorization.</span></span> <span data-ttu-id="563c0-161">這會導致 hello 建立的授權金鑰可以使用循環使用者 tooconnect 其虛擬網路閘道 toohello ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="563c0-161">This results in hello creation of an authorization key that can be used by a circuit user tooconnect their virtual network gateways toohello ExpressRoute circuit.</span></span> <span data-ttu-id="563c0-162">一個授權僅適用於一個連線。</span><span class="sxs-lookup"><span data-stu-id="563c0-162">An authorization is valid for only one connection.</span></span>

1. <span data-ttu-id="563c0-163">在 hello ExpressRoute 刀鋒視窗中，按一下 **授權**，然後輸入**名稱**hello 授權，然後按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="563c0-163">In hello ExpressRoute blade, Click **Authorizations** and then type a **name** for hello authorization and click **Save**.</span></span>

    ![授權](./media/expressroute-howto-linkvnet-portal-resource-manager/authorization.png)

2. <span data-ttu-id="563c0-165">Hello 組態儲存之後，複製 hello**資源識別碼**和 hello**授權金鑰**。</span><span class="sxs-lookup"><span data-stu-id="563c0-165">Once hello configuration is saved, copy hello **Resource ID** and hello **Authorization Key**.</span></span>

    ![授權金鑰](./media/expressroute-howto-linkvnet-portal-resource-manager/authkey.png)

<span data-ttu-id="563c0-167">**toodelete 連線授權**</span><span class="sxs-lookup"><span data-stu-id="563c0-167">**toodelete a connection authorization**</span></span>

<span data-ttu-id="563c0-168">您可以刪除的連線，藉由選取 hello**刪除**連線 hello 刀鋒視窗上的圖示。</span><span class="sxs-lookup"><span data-stu-id="563c0-168">You can delete a connection by selecting hello **Delete** icon on hello blade for your connection.</span></span>

### <a name="circuit-user-operations"></a><span data-ttu-id="563c0-169">循環使用者作業</span><span class="sxs-lookup"><span data-stu-id="563c0-169">Circuit user operations</span></span>

<span data-ttu-id="563c0-170">hello 電路使用者需要 hello 資源 ID，以及從 hello 電路擁有者授權金鑰。</span><span class="sxs-lookup"><span data-stu-id="563c0-170">hello circuit user needs hello resource ID and an authorization key from hello circuit owner.</span></span> 

<span data-ttu-id="563c0-171">**tooredeem 連線授權**</span><span class="sxs-lookup"><span data-stu-id="563c0-171">**tooredeem a connection authorization**</span></span>

1.  <span data-ttu-id="563c0-172">按一下 hello **+ 新增** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="563c0-172">Click hello **+New** button.</span></span>

    ![Click New](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection1.png)

2.  <span data-ttu-id="563c0-174">搜尋**「 連線 」** hello Marketplace，在選取它，然後按一下**建立**。</span><span class="sxs-lookup"><span data-stu-id="563c0-174">Search for **"Connection"** in hello Marketplace, select it, and click **Create**.</span></span>

    ![搜尋連線](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection2.png)

3.  <span data-ttu-id="563c0-176">請確定 hello**連線類型**設定得"ExpressRoute"。</span><span class="sxs-lookup"><span data-stu-id="563c0-176">Make sure hello **Connection type** is set too"ExpressRoute".</span></span>


4.  <span data-ttu-id="563c0-177">填入 hello 詳細資料，然後按一下 **確定**hello 基本概念刀鋒視窗中。</span><span class="sxs-lookup"><span data-stu-id="563c0-177">Fill in hello details, then click **OK** in hello Basics blade.</span></span>

    ![基本概念刀鋒視窗](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection3.png)

5.  <span data-ttu-id="563c0-179">在 hello**設定**刀鋒視窗中，選取 hello**虛擬網路閘道**並檢查 hello**兌換授權**核取方塊。</span><span class="sxs-lookup"><span data-stu-id="563c0-179">In hello **Settings** blade, Select hello **Virtual network gateway** and check hello **Redeem authorization** check box.</span></span>

6.  <span data-ttu-id="563c0-180">輸入 hello**授權金鑰**和 hello**對等電路 URI**並提供 hello 連接名稱。</span><span class="sxs-lookup"><span data-stu-id="563c0-180">Enter hello **Authorization key** and hello **Peer circuit URI** and give hello connection a name.</span></span> <span data-ttu-id="563c0-181">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="563c0-181">Click **OK**.</span></span>

    ![設定刀鋒視窗](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection4.png)

7. <span data-ttu-id="563c0-183">檢閱在 hello hello 資訊**摘要**刀鋒視窗，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="563c0-183">Review hello information in hello **Summary** blade and click **OK**.</span></span>


<span data-ttu-id="563c0-184">**toorelease 連線授權**</span><span class="sxs-lookup"><span data-stu-id="563c0-184">**toorelease a connection authorization**</span></span>

<span data-ttu-id="563c0-185">您可以藉由刪除連結 hello ExpressRoute 電路 toohello 虛擬網路的 hello 連接釋放授權。</span><span class="sxs-lookup"><span data-stu-id="563c0-185">You can release an authorization by deleting hello connection that links hello ExpressRoute circuit toohello virtual network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="563c0-186">後續步驟</span><span class="sxs-lookup"><span data-stu-id="563c0-186">Next steps</span></span>
<span data-ttu-id="563c0-187">如需 ExpressRoute 的詳細資訊，請參閱 hello [ExpressRoute 常見問題集](expressroute-faqs.md)。</span><span class="sxs-lookup"><span data-stu-id="563c0-187">For more information about ExpressRoute, see hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>
