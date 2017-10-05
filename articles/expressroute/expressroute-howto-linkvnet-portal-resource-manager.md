---
title: "將虛擬網路連結到 ExpressRoute 電路：Azure 入口網站 | Microsoft Docs"
description: "本文件提供如何將虛擬網路 (Vnet) 連結到 ExpressRoute 循環的概觀。"
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
ms.openlocfilehash: 595c30ab5d9adc6061ad753d952adf894ba80b2f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="connect-a-virtual-network-to-an-expressroute-circuit"></a><span data-ttu-id="04f76-103">將虛擬網路連線到 ExpressRoute 電路</span><span class="sxs-lookup"><span data-stu-id="04f76-103">Connect a virtual network to an ExpressRoute circuit</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="04f76-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="04f76-104">Azure portal</span></span>](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [<span data-ttu-id="04f76-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="04f76-105">PowerShell</span></span>](expressroute-howto-linkvnet-arm.md)
> * [<span data-ttu-id="04f76-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="04f76-106">Azure CLI</span></span>](howto-linkvnet-cli.md)
> * [<span data-ttu-id="04f76-107">影片 - Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="04f76-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [<span data-ttu-id="04f76-108">PowerShell (傳統)</span><span class="sxs-lookup"><span data-stu-id="04f76-108">PowerShell (classic)</span></span>](expressroute-howto-linkvnet-classic.md)
> 

<span data-ttu-id="04f76-109">本文會協助您使用 Resource Manager 部署模型和 Azure 入口網站將虛擬網路 (VNet) 連結到 Azure ExpressRoute 線路。</span><span class="sxs-lookup"><span data-stu-id="04f76-109">This article helps you link virtual networks (VNets) to Azure ExpressRoute circuits by using the Resource Manager deployment model and the Azure portal.</span></span> <span data-ttu-id="04f76-110">虛擬網路可以位於相同的訂用帳戶中，或屬於另一個訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="04f76-110">Virtual networks can either be in the same subscription, or they can be part of another subscription.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="04f76-111">開始之前</span><span class="sxs-lookup"><span data-stu-id="04f76-111">Before you begin</span></span>
* <span data-ttu-id="04f76-112">開始設定之前，請先檢閱[必要條件](expressroute-prerequisites.md)、[路由需求](expressroute-routing.md)及[工作流程](expressroute-workflows.md)。</span><span class="sxs-lookup"><span data-stu-id="04f76-112">Review the [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="04f76-113">您必須擁有作用中的 ExpressRoute 線路。</span><span class="sxs-lookup"><span data-stu-id="04f76-113">You must have an active ExpressRoute circuit.</span></span>
  
  * <span data-ttu-id="04f76-114">遵循指示來 [建立 ExpressRoute 線路](expressroute-howto-circuit-portal-resource-manager.md) ，並由您的連線提供者來啟用該線路。</span><span class="sxs-lookup"><span data-stu-id="04f76-114">Follow the instructions to [create an ExpressRoute circuit](expressroute-howto-circuit-portal-resource-manager.md) and have the circuit enabled by your connectivity provider.</span></span>
  * <span data-ttu-id="04f76-115">確定您已針對循環設定了 Azure 私用對等。</span><span class="sxs-lookup"><span data-stu-id="04f76-115">Ensure that you have Azure private peering configured for your circuit.</span></span> <span data-ttu-id="04f76-116">請參閱 [設定路由](expressroute-howto-routing-portal-resource-manager.md) 一文，以取得路由指示。</span><span class="sxs-lookup"><span data-stu-id="04f76-116">See the [Configure routing](expressroute-howto-routing-portal-resource-manager.md) article for routing instructions.</span></span>
  * <span data-ttu-id="04f76-117">請確定已設定 Azure 私用對等，且已開啟您的網路與 Microsoft 之間的 BGP 對等，讓您可以啟用端對端連線。</span><span class="sxs-lookup"><span data-stu-id="04f76-117">Ensure that Azure private peering is configured and the BGP peering between your network and Microsoft is up so that you can enable end-to-end connectivity.</span></span>
  * <span data-ttu-id="04f76-118">請確定您有已建立且完整佈建的虛擬網路和虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="04f76-118">Ensure that you have a virtual network and a virtual network gateway created and fully provisioned.</span></span> <span data-ttu-id="04f76-119">請依照指示[為 ExpressRoute 建立虛擬網路閘道](expressroute-howto-add-gateway-resource-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="04f76-119">Follow the instructions to [create a virtual network gateway for ExpressRoute](expressroute-howto-add-gateway-resource-manager.md).</span></span> <span data-ttu-id="04f76-120">ExpressRoute 的虛擬網路閘道會使用 GatewayType 'ExpressRoute'，而不是 VPN。</span><span class="sxs-lookup"><span data-stu-id="04f76-120">A virtual network gateway for ExpressRoute uses the GatewayType 'ExpressRoute', not VPN.</span></span>

* <span data-ttu-id="04f76-121">您最多可以將 10 個虛擬網路連結至標準 ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="04f76-121">You can link up to 10 virtual networks to a standard ExpressRoute circuit.</span></span> <span data-ttu-id="04f76-122">在使用標準 ExpressRoute 電路時，所有虛擬網路都必須位於相同的地理政治區域內。</span><span class="sxs-lookup"><span data-stu-id="04f76-122">All virtual networks must be in the same geopolitical region when using a standard ExpressRoute circuit.</span></span> 
* <span data-ttu-id="04f76-123">如果您已啟用 ExpressRoute 高階附加元件，則可連結 ExpressRoute 電路的地理政治區域以外的虛擬網路，或是將大量的虛擬網路連線到 ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="04f76-123">You can link a virtual network outside of the geopolitical region of the ExpressRoute circuit, or connect a larger number of virtual networks to your ExpressRoute circuit if you enabled the ExpressRoute premium add-on.</span></span> <span data-ttu-id="04f76-124">如需高階附加元件的詳細資訊，請參閱 [常見問題集](expressroute-faqs.md) 。</span><span class="sxs-lookup"><span data-stu-id="04f76-124">Check the [FAQ](expressroute-faqs.md) for more details on the premium add-on.</span></span>
* <span data-ttu-id="04f76-125">您可以在開始前先[觀看影片](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)來進一步了解步驟。</span><span class="sxs-lookup"><span data-stu-id="04f76-125">You can [view a video](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit) before beginning to better understand the steps.</span></span>

## <a name="connect-a-virtual-network-in-the-same-subscription-to-a-circuit"></a><span data-ttu-id="04f76-126">將相同訂用帳戶中的虛擬網路連接到線路</span><span class="sxs-lookup"><span data-stu-id="04f76-126">Connect a virtual network in the same subscription to a circuit</span></span>

### <a name="to-create-a-connection"></a><span data-ttu-id="04f76-127">建立連線</span><span class="sxs-lookup"><span data-stu-id="04f76-127">To create a connection</span></span>

> [!NOTE]
> <span data-ttu-id="04f76-128">如果您的對等互連是由第 3 層提供者設定，就不會顯示 BGP 組態資訊。</span><span class="sxs-lookup"><span data-stu-id="04f76-128">BGP configuration information will not show up if the layer 3 provider configured your peerings.</span></span> <span data-ttu-id="04f76-129">如果線路處於佈建狀態，您應該能夠建立連線。</span><span class="sxs-lookup"><span data-stu-id="04f76-129">If your circuit is in a provisioned state, you should be able to create connections.</span></span>
>

1. <span data-ttu-id="04f76-130">確認正確設定您的 ExpressRoute 電路和 Azure 私人對等互連。</span><span class="sxs-lookup"><span data-stu-id="04f76-130">Ensure that your ExpressRoute circuit and Azure private peering have been configured successfully.</span></span> <span data-ttu-id="04f76-131">請遵循[建立 ExpressRoute 線路](expressroute-howto-circuit-arm.md)和[設定路由](expressroute-howto-routing-arm.md)中的指示。</span><span class="sxs-lookup"><span data-stu-id="04f76-131">Follow the instructions in [Create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and [Configure routing](expressroute-howto-routing-arm.md).</span></span> <span data-ttu-id="04f76-132">ExpressRoute 線路看起來應該像下圖：</span><span class="sxs-lookup"><span data-stu-id="04f76-132">Your ExpressRoute circuit should look like the following image:</span></span>

    ![刪除 ExpressRoute 線路螢幕擷取畫面](./media/expressroute-howto-linkvnet-portal-resource-manager/routing1.png)
   
2. <span data-ttu-id="04f76-134">您現在可以開始佈建將虛擬網路閘道連結至 ExpressRoute 線路的連線。</span><span class="sxs-lookup"><span data-stu-id="04f76-134">You can now start provisioning a connection to link your virtual network gateway to your ExpressRoute circuit.</span></span> <span data-ttu-id="04f76-135">按一下 [連接] > [新增] 開啟 [新增連線] 刀鋒視窗，然後設定各值。</span><span class="sxs-lookup"><span data-stu-id="04f76-135">Click **Connection** > **Add** to open the **Add connection** blade, and then configure the values.</span></span>

    ![新增連線螢幕擷取畫面](./media/expressroute-howto-linkvnet-portal-resource-manager/samesub1.png)  

3. <span data-ttu-id="04f76-137">順利設定連線後，您的連線物件就會顯示連接資訊。</span><span class="sxs-lookup"><span data-stu-id="04f76-137">After your connection has been successfully configured, your connection object will show the information for the connection.</span></span>

     ![連線物件螢幕擷取畫面](./media/expressroute-howto-linkvnet-portal-resource-manager/samesub2.png)

### <a name="to-delete-a-connection"></a><span data-ttu-id="04f76-139">刪除連接</span><span class="sxs-lookup"><span data-stu-id="04f76-139">To delete a connection</span></span>
<span data-ttu-id="04f76-140">您可以選取連接刀鋒視窗上的 **刪除** 圖示來刪除連接。</span><span class="sxs-lookup"><span data-stu-id="04f76-140">You can delete a connection by selecting the **Delete** icon on the blade for your connection.</span></span>

## <a name="connect-a-virtual-network-in-a-different-subscription-to-a-circuit"></a><span data-ttu-id="04f76-141">將不同訂用帳戶中的虛擬網路連接到線路</span><span class="sxs-lookup"><span data-stu-id="04f76-141">Connect a virtual network in a different subscription to a circuit</span></span>
<span data-ttu-id="04f76-142">您可以讓多個訂用帳戶共用 ExpressRoute 線路。</span><span class="sxs-lookup"><span data-stu-id="04f76-142">You can share an ExpressRoute circuit across multiple subscriptions.</span></span> <span data-ttu-id="04f76-143">下圖顯示簡單的圖解，示範多個訂用帳戶共用 ExpressRoute 線路的方式。</span><span class="sxs-lookup"><span data-stu-id="04f76-143">The figure below shows a simple schematic of how sharing works for ExpressRoute circuits across multiple subscriptions.</span></span>

![跨訂用帳戶的連線能力](./media/expressroute-howto-linkvnet-portal-resource-manager/cross-subscription.png)

- <span data-ttu-id="04f76-145">大型雲端內的每個較小型雲端，會用來代表屬於組織內不同部門的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="04f76-145">Each of the smaller clouds within the large cloud is used to represent subscriptions that belong to different departments within an organization.</span></span>
- <span data-ttu-id="04f76-146">組織內的每個部門都可以使用自己的訂用帳戶來部署它們的服務，但可共用單一 ExpressRoute 線路，以連線回內部部署網路。</span><span class="sxs-lookup"><span data-stu-id="04f76-146">Each of the departments within the organization can use their own subscription for deploying their services, but they can share a single ExpressRoute circuit to connect back to your on-premises network.</span></span>
- <span data-ttu-id="04f76-147">單一部門 (在此範例中：IT) 可以擁有 ExpressRoute 循環。</span><span class="sxs-lookup"><span data-stu-id="04f76-147">A single department (in this example: IT) can own the ExpressRoute circuit.</span></span> <span data-ttu-id="04f76-148">組織內的其他訂用帳戶可以使用 ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="04f76-148">Other subscriptions within the organization can use the ExpressRoute circuit.</span></span>

    > [!NOTE]
    > <span data-ttu-id="04f76-149">ExpressRoute 循環擁有者需支付專用循環的連線和頻寬費用。</span><span class="sxs-lookup"><span data-stu-id="04f76-149">Connectivity and bandwidth charges for the dedicated circuit will be applied to the ExpressRoute circuit owner.</span></span> <span data-ttu-id="04f76-150">所有虛擬網路都會共用相同的頻寬。</span><span class="sxs-lookup"><span data-stu-id="04f76-150">All virtual networks share the same bandwidth.</span></span>
    > 
    >

### <a name="administration---circuit-owners-and-circuit-users"></a><span data-ttu-id="04f76-151">系統管理 - 線路擁有者和線路使用者</span><span class="sxs-lookup"><span data-stu-id="04f76-151">Administration - circuit owners and circuit users</span></span>

<span data-ttu-id="04f76-152">「線路擁有者」是 ExpressRoute 線路資源的已授權「進階使用者」。</span><span class="sxs-lookup"><span data-stu-id="04f76-152">The 'circuit owner' is an authorized Power User of the ExpressRoute circuit resource.</span></span> <span data-ttu-id="04f76-153">電路擁有者能夠建立可由「電路使用者」兌換的授權。</span><span class="sxs-lookup"><span data-stu-id="04f76-153">The circuit owner can create authorizations that can be redeemed by 'circuit users'.</span></span> <span data-ttu-id="04f76-154">線路使用者是虛擬網路閘道的擁有者，與 ExpressRoute 線路位於不同的訂用帳戶內。</span><span class="sxs-lookup"><span data-stu-id="04f76-154">Circuit users are owners of virtual network gateways that are not within the same subscription as the ExpressRoute circuit.</span></span> <span data-ttu-id="04f76-155">電路使用者可以兌換授權 (每個虛擬網路一個授權)。</span><span class="sxs-lookup"><span data-stu-id="04f76-155">Circuit users can redeem authorizations (one authorization per virtual network).</span></span>

<span data-ttu-id="04f76-156">電路擁有者能夠隨時修改及撤銷授權。</span><span class="sxs-lookup"><span data-stu-id="04f76-156">The circuit owner has the power to modify and revoke authorizations at any time.</span></span> <span data-ttu-id="04f76-157">如果撤銷授權，則在存取權遭撤銷的訂用帳戶中，所有連結連線均會被刪除。</span><span class="sxs-lookup"><span data-stu-id="04f76-157">Revoking an authorization results in all link connections being deleted from the subscription whose access was revoked.</span></span>

### <a name="circuit-owner-operations"></a><span data-ttu-id="04f76-158">循環擁有者作業</span><span class="sxs-lookup"><span data-stu-id="04f76-158">Circuit owner operations</span></span>

<span data-ttu-id="04f76-159">**建立連線授權**</span><span class="sxs-lookup"><span data-stu-id="04f76-159">**To create a connection authorization**</span></span>

<span data-ttu-id="04f76-160">電路擁有者會建立授權。</span><span class="sxs-lookup"><span data-stu-id="04f76-160">The circuit owner creates an authorization.</span></span> <span data-ttu-id="04f76-161">這樣即會建立授權金鑰，讓電路使用者可用來將其虛擬網路閘道連接到 ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="04f76-161">This results in the creation of an authorization key that can be used by a circuit user to connect their virtual network gateways to the ExpressRoute circuit.</span></span> <span data-ttu-id="04f76-162">一個授權僅適用於一個連線。</span><span class="sxs-lookup"><span data-stu-id="04f76-162">An authorization is valid for only one connection.</span></span>

1. <span data-ttu-id="04f76-163">在 [ExpressRoute] 刀鋒視窗中，按一下 [授權]，然後輸入授權的**名稱**並按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="04f76-163">In the ExpressRoute blade, Click **Authorizations** and then type a **name** for the authorization and click **Save**.</span></span>

    ![授權](./media/expressroute-howto-linkvnet-portal-resource-manager/authorization.png)

2. <span data-ttu-id="04f76-165">儲存組態之後，複製**資源識別碼**和**授權金鑰**。</span><span class="sxs-lookup"><span data-stu-id="04f76-165">Once the configuration is saved, copy the **Resource ID** and the **Authorization Key**.</span></span>

    ![授權金鑰](./media/expressroute-howto-linkvnet-portal-resource-manager/authkey.png)

<span data-ttu-id="04f76-167">**刪除連線授權**</span><span class="sxs-lookup"><span data-stu-id="04f76-167">**To delete a connection authorization**</span></span>

<span data-ttu-id="04f76-168">您可以選取連接刀鋒視窗上的 **刪除** 圖示來刪除連接。</span><span class="sxs-lookup"><span data-stu-id="04f76-168">You can delete a connection by selecting the **Delete** icon on the blade for your connection.</span></span>

### <a name="circuit-user-operations"></a><span data-ttu-id="04f76-169">循環使用者作業</span><span class="sxs-lookup"><span data-stu-id="04f76-169">Circuit user operations</span></span>

<span data-ttu-id="04f76-170">線路使用者需要具備資源識別碼，以及線路擁有者所提供的授權金鑰。</span><span class="sxs-lookup"><span data-stu-id="04f76-170">The circuit user needs the resource ID and an authorization key from the circuit owner.</span></span> 

<span data-ttu-id="04f76-171">**兌換連線授權**</span><span class="sxs-lookup"><span data-stu-id="04f76-171">**To redeem a connection authorization**</span></span>

1.  <span data-ttu-id="04f76-172">按一下 [+新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="04f76-172">Click the **+New** button.</span></span>

    ![Click New](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection1.png)

2.  <span data-ttu-id="04f76-174">在 Marketplace 中搜尋**連線**、選取它，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="04f76-174">Search for **"Connection"** in the Marketplace, select it, and click **Create**.</span></span>

    ![搜尋連線](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection2.png)

3.  <span data-ttu-id="04f76-176">確定 [連線類型] 設定為 [ExpressRoute]。</span><span class="sxs-lookup"><span data-stu-id="04f76-176">Make sure the **Connection type** is set to "ExpressRoute".</span></span>


4.  <span data-ttu-id="04f76-177">填入詳細資料，然後在 [基本] 刀鋒視窗中按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="04f76-177">Fill in the details, then click **OK** in the Basics blade.</span></span>

    ![基本概念刀鋒視窗](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection3.png)

5.  <span data-ttu-id="04f76-179">在 [設定] 刀鋒視窗中選取 [虛擬網路閘道]，並選取 [兌換授權] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="04f76-179">In the **Settings** blade, Select the **Virtual network gateway** and check the **Redeem authorization** check box.</span></span>

6.  <span data-ttu-id="04f76-180">輸入**授權金鑰**和**對等線路 URI**，並提供連線名稱。</span><span class="sxs-lookup"><span data-stu-id="04f76-180">Enter the **Authorization key** and the **Peer circuit URI** and give the connection a name.</span></span> <span data-ttu-id="04f76-181">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="04f76-181">Click **OK**.</span></span>

    ![設定刀鋒視窗](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection4.png)

7. <span data-ttu-id="04f76-183">在 [摘要] 刀鋒視窗中檢閱資訊，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="04f76-183">Review the information in the **Summary** blade and click **OK**.</span></span>


<span data-ttu-id="04f76-184">**釋出連線授權**</span><span class="sxs-lookup"><span data-stu-id="04f76-184">**To release a connection authorization**</span></span>

<span data-ttu-id="04f76-185">您可以藉由刪除將 ExpressRoute 線路連結到虛擬網路的連線來釋出授權。</span><span class="sxs-lookup"><span data-stu-id="04f76-185">You can release an authorization by deleting the connection that links the ExpressRoute circuit to the virtual network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="04f76-186">後續步驟</span><span class="sxs-lookup"><span data-stu-id="04f76-186">Next steps</span></span>
<span data-ttu-id="04f76-187">如需有關 ExpressRoute 的詳細資訊，請參閱 [ExpressRoute 常見問題集](expressroute-faqs.md)。</span><span class="sxs-lookup"><span data-stu-id="04f76-187">For more information about ExpressRoute, see the [ExpressRoute FAQ](expressroute-faqs.md).</span></span>
