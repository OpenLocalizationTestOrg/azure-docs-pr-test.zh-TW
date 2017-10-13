---
title: "使用 ExpressRoute 將 Azure Stack 連線至 Azure"
description: "如何使用 ExpressRoute 將 Azure Stack 中的虛擬網路連線至 Azure 中的虛擬網路。"
services: azure-stack
documentationcenter: 
author: victorar
manager: 
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 9/25/2017
ms.author: victorh
ms.openlocfilehash: aa6973939c6cfe0688f5781fdcea5d39670249df
ms.sourcegitcommit: 90e2cced6a773b1b52f999ba73cd8877305d270b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/13/2017
---
# <a name="connect-azure-stack-to-azure-using-expressroute"></a><span data-ttu-id="2df1b-103">使用 ExpressRoute 將 Azure Stack 連線至 Azure</span><span class="sxs-lookup"><span data-stu-id="2df1b-103">Connect Azure Stack to Azure using ExpressRoute</span></span>

<span data-ttu-id="2df1b-104">「適用於：Azure Stack 整合系統和 Azure Stack 開發套件」</span><span class="sxs-lookup"><span data-stu-id="2df1b-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="2df1b-105">支援兩種方法將 Azure Stack 中的虛擬網路連線至 Azure 中的虛擬網路：</span><span class="sxs-lookup"><span data-stu-id="2df1b-105">There are two supported methods to connect virtual networks in Azure Stack to virtual networks in Azure:</span></span>
   * <span data-ttu-id="2df1b-106">**網站間**</span><span class="sxs-lookup"><span data-stu-id="2df1b-106">**Site-to-Site**</span></span>

     <span data-ttu-id="2df1b-107">透過 IPsec (IKE v1 和 IKE v2) 的 VPN 連線。</span><span class="sxs-lookup"><span data-stu-id="2df1b-107">A VPN connection over IPsec (IKE v1 and IKE v2).</span></span> <span data-ttu-id="2df1b-108">此類型的連線需要 VPN 裝置或 RRAS。</span><span class="sxs-lookup"><span data-stu-id="2df1b-108">This type of connection requires a VPN device or RRAS.</span></span> <span data-ttu-id="2df1b-109">如需詳細資訊，請參閱[使用 VPN 將 Azure Stack 連線至 Azure](azure-stack-connect-vpn.md)。</span><span class="sxs-lookup"><span data-stu-id="2df1b-109">For more information, see [Connect Azure Stack to Azure using VPN](azure-stack-connect-vpn.md).</span></span>
   * <span data-ttu-id="2df1b-110">**ExpressRoute**</span><span class="sxs-lookup"><span data-stu-id="2df1b-110">**ExpressRoute**</span></span>

     <span data-ttu-id="2df1b-111">從 Azure Stack 部署直接連線至 Azure。</span><span class="sxs-lookup"><span data-stu-id="2df1b-111">A direct connection to Azure from your Azure Stack deployment.</span></span> <span data-ttu-id="2df1b-112">ExpressRoute **不是**透過公用網際網路的 VPN 連線。</span><span class="sxs-lookup"><span data-stu-id="2df1b-112">ExpressRoute is **not** a VPN connection over the public Internet.</span></span> <span data-ttu-id="2df1b-113">如需 Azure ExpressRoute 的詳細資訊，請參閱 [ExpressRoute 概觀](../expressroute/expressroute-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="2df1b-113">For more information about Azure ExpressRoute, see [ExpressRoute overview](../expressroute/expressroute-introduction.md).</span></span>

<span data-ttu-id="2df1b-114">本文將示範如何使用 ExpressRoute 將 Azure Stack 連線至 Azure。</span><span class="sxs-lookup"><span data-stu-id="2df1b-114">This article shows an example using ExpressRoute to connect Azure Stack to Azure.</span></span>
## <a name="requirements"></a><span data-ttu-id="2df1b-115">需求</span><span class="sxs-lookup"><span data-stu-id="2df1b-115">Requirements</span></span>
<span data-ttu-id="2df1b-116">使用 ExpressRoute 來連線 Azure Stack 和 Azure 時的特定需求如下：</span><span class="sxs-lookup"><span data-stu-id="2df1b-116">The following are specific requirements to connect Azure Stack and Azure using ExpressRoute:</span></span>
* <span data-ttu-id="2df1b-117">Azure 訂用帳戶，用於 Azure 中建立 ExpressRoute 線路和 VNet。</span><span class="sxs-lookup"><span data-stu-id="2df1b-117">An Azure subscription to create an ExpressRoute circuit and VNets in Azure.</span></span>
* <span data-ttu-id="2df1b-118">透過[連線提供者](../expressroute/expressroute-locations.md)佈建的 ExpressRoute 線路。</span><span class="sxs-lookup"><span data-stu-id="2df1b-118">A provisioned ExpressRoute circuit through a [connectivity provider](../expressroute/expressroute-locations.md).</span></span>
* <span data-ttu-id="2df1b-119">路由器，ExpressRoute 線路會連線至其 WAN 連接埠。</span><span class="sxs-lookup"><span data-stu-id="2df1b-119">A router that has the ExpressRoute circuit connected to its WAN ports.</span></span>
* <span data-ttu-id="2df1b-120">路由器的 LAN 端會連結至 Azure Stack 多組織用戶共享閘道。</span><span class="sxs-lookup"><span data-stu-id="2df1b-120">The LAN side of the router is linked to the Azure Stack Multitenant Gateway.</span></span>
* <span data-ttu-id="2df1b-121">路由器在其 LAN 介面和 Azure Stack 多組織用戶共享閘道之間，必須支援站對站 VPN 連線。</span><span class="sxs-lookup"><span data-stu-id="2df1b-121">The router must support Site-to-Site VPN connections between its LAN interface and Azure Stack Multitenant Gateway.</span></span>
* <span data-ttu-id="2df1b-122">如果您的 Azure Stack 部署中新增多個租用戶，路由器必須能夠建立多個 VRF (虛擬路由和轉送)。</span><span class="sxs-lookup"><span data-stu-id="2df1b-122">If more than one tenant is added in your Azure Stack deployment, the router must be able to create multiple VRFs (Virtual Routing and Forwarding).</span></span>

<span data-ttu-id="2df1b-123">下圖顯示完成設定之後的概念性網路服務檢視：</span><span class="sxs-lookup"><span data-stu-id="2df1b-123">The following diagram shows a conceptual networking view after you complete the configuration:</span></span>

![概念圖表](media/azure-stack-connect-expressroute/Conceptual.png)

<span data-ttu-id="2df1b-125">**圖表 1**</span><span class="sxs-lookup"><span data-stu-id="2df1b-125">**Diagram 1**</span></span>

<span data-ttu-id="2df1b-126">下列架構圖表顯示多個租用戶如何從 Azure Stack 基礎結構，透過 ExpressRoute 路由器，連線至 Microsoft Edge 的 Azure：</span><span class="sxs-lookup"><span data-stu-id="2df1b-126">The following architecture diagram shows how multiple tenants connect from the Azure Stack infrastructure through the ExpressRoute router to Azure at the Microsoft edge:</span></span>

![架構圖表](media/azure-stack-connect-expressroute/Architecture.png)

<span data-ttu-id="2df1b-128">**圖表 2**</span><span class="sxs-lookup"><span data-stu-id="2df1b-128">**Diagram 2**</span></span>

<span data-ttu-id="2df1b-129">本文中顯示的範例使用相同的架構，以透過 ExpressRoute 私用對等互連來連線至 Azure。</span><span class="sxs-lookup"><span data-stu-id="2df1b-129">The example shown in this article uses the same architecture to connect to Azure via ExpressRoute private peering.</span></span> <span data-ttu-id="2df1b-130">在作法上是使用站對站 VPN 連線，從 Azure Stack 中的虛擬網路閘道連線至 ExpressRoute 路由器。</span><span class="sxs-lookup"><span data-stu-id="2df1b-130">It is done using a Site-to-Site VPN connection from the virtual network gateway in Azure Stack to an ExpressRoute router.</span></span> <span data-ttu-id="2df1b-131">在本文中，下列步驟說明如何在兩個 VNet 之間建立端對端連線：從 Azure Stack 中的不同租用戶到它們在 Azure 中各自的 VNet。</span><span class="sxs-lookup"><span data-stu-id="2df1b-131">The following steps in this article show how to create an end-to-end connection between two VNets from two different tenants in Azure Stack to their respective VNets in Azure.</span></span> <span data-ttu-id="2df1b-132">您可以選擇新增更多個租用戶 VNet，並對每個租用戶重複同樣的步驟，或使用此範例而只部署單一租用戶 VNet。</span><span class="sxs-lookup"><span data-stu-id="2df1b-132">You can choose to add as many tenant VNets and replicate the steps for each tenant or use this example to deploy just a single tenant VNet.</span></span>

## <a name="configure-azure-stack"></a><span data-ttu-id="2df1b-133">設定 Azure Stack</span><span class="sxs-lookup"><span data-stu-id="2df1b-133">Configure Azure Stack</span></span>
<span data-ttu-id="2df1b-134">現在，請建立您需要的資源，以將 Azure Stack 環境設定為租用戶。</span><span class="sxs-lookup"><span data-stu-id="2df1b-134">Now you create the resources you need to set up your Azure Stack environment as a tenant.</span></span> <span data-ttu-id="2df1b-135">下列步驟說明您需要怎麼做。</span><span class="sxs-lookup"><span data-stu-id="2df1b-135">The following steps illustrate what you need to do.</span></span> <span data-ttu-id="2df1b-136">以下指示說明如何使用 Azure Stack 入口網站來建立資源，但您也可以使用 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="2df1b-136">These instructions show how to create resources using the Azure Stack portal, but you can also use PowerShell.</span></span>

![網路資源步驟](media/azure-stack-connect-expressroute/image2.png)
### <a name="before-you-begin"></a><span data-ttu-id="2df1b-138">開始之前</span><span class="sxs-lookup"><span data-stu-id="2df1b-138">Before you begin</span></span>
<span data-ttu-id="2df1b-139">在開始設定之前，您需要：</span><span class="sxs-lookup"><span data-stu-id="2df1b-139">Before you start the configuration, you need:</span></span>
* <span data-ttu-id="2df1b-140">Azure Stack 部署。</span><span class="sxs-lookup"><span data-stu-id="2df1b-140">An Azure Stack deployment.</span></span>

   <span data-ttu-id="2df1b-141">如需有關部署 Azure Stack 開發套件的資訊，請參閱 [Azure Stack 開發套件部署快速入門](azure-stack-deploy-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="2df1b-141">For information about deploying Azure Stack Development Kit, see [Azure Stack Development Kit deployment quickstart](azure-stack-deploy-overview.md).</span></span>
* <span data-ttu-id="2df1b-142">Azure Stack 上可供使用者訂閱的供應項目。</span><span class="sxs-lookup"><span data-stu-id="2df1b-142">An offer on Azure Stack that your user can subscribe to.</span></span>

  <span data-ttu-id="2df1b-143">如需指示，請參閱[將虛擬機器提供給您的 Azure Stack 使用者](azure-stack-tutorial-tenant-vm.md)。</span><span class="sxs-lookup"><span data-stu-id="2df1b-143">For instructions, see [Make virtual machines available to your Azure Stack users](azure-stack-tutorial-tenant-vm.md).</span></span>

### <a name="create-network-resources-in-azure-stack"></a><span data-ttu-id="2df1b-144">在 Azure Stack 中建立網路資源</span><span class="sxs-lookup"><span data-stu-id="2df1b-144">Create network resources in Azure Stack</span></span>

<span data-ttu-id="2df1b-145">請使用下列程序在 Azure Stack 中建立每個租用戶所需的網路資源：</span><span class="sxs-lookup"><span data-stu-id="2df1b-145">Use the following procedures to create the required network resources in Azure Stack for each tenant:</span></span>

#### <a name="create-the-virtual-network-and-vm-subnet"></a><span data-ttu-id="2df1b-146">建立虛擬網路和 VM 子網路</span><span class="sxs-lookup"><span data-stu-id="2df1b-146">Create the virtual network and VM subnet</span></span>
1. <span data-ttu-id="2df1b-147">以使用者 (租用戶) 帳戶來登入使用者入口網站。</span><span class="sxs-lookup"><span data-stu-id="2df1b-147">Sign in the user portal with a user (tenant) account.</span></span>

2. <span data-ttu-id="2df1b-148">在入口網站中，按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="2df1b-148">In the portal, click **New**.</span></span>

   ![](media/azure-stack-connect-expressroute/MAS-new.png)

3. <span data-ttu-id="2df1b-149">從 Marketplace 功能表中選取 [網路]。</span><span class="sxs-lookup"><span data-stu-id="2df1b-149">Select **Networking** from the Marketplace menu.</span></span>

4. <span data-ttu-id="2df1b-150">按一下功能表上的 [虛擬網路]。</span><span class="sxs-lookup"><span data-stu-id="2df1b-150">Click **Virtual network** on the menu.</span></span>

5. <span data-ttu-id="2df1b-151">根據下表，在適當欄位中輸入值：</span><span class="sxs-lookup"><span data-stu-id="2df1b-151">Type the values into the appropriate fields using the following table:</span></span>

   |<span data-ttu-id="2df1b-152">欄位</span><span class="sxs-lookup"><span data-stu-id="2df1b-152">Field</span></span>  |<span data-ttu-id="2df1b-153">值</span><span class="sxs-lookup"><span data-stu-id="2df1b-153">Value</span></span>  |
   |---------|---------|
   |<span data-ttu-id="2df1b-154">名稱</span><span class="sxs-lookup"><span data-stu-id="2df1b-154">Name</span></span>     |<span data-ttu-id="2df1b-155">Tenant1VNet1</span><span class="sxs-lookup"><span data-stu-id="2df1b-155">Tenant1VNet1</span></span>         |
   |<span data-ttu-id="2df1b-156">位址空間</span><span class="sxs-lookup"><span data-stu-id="2df1b-156">Address space</span></span>     |<span data-ttu-id="2df1b-157">10.1.0.0/16</span><span class="sxs-lookup"><span data-stu-id="2df1b-157">10.1.0.0/16</span></span>|
   |<span data-ttu-id="2df1b-158">子網路名稱</span><span class="sxs-lookup"><span data-stu-id="2df1b-158">Subnet name</span></span>     |<span data-ttu-id="2df1b-159">Tenant1-Sub1</span><span class="sxs-lookup"><span data-stu-id="2df1b-159">Tenant1-Sub1</span></span>|
   |<span data-ttu-id="2df1b-160">子網路位址範圍</span><span class="sxs-lookup"><span data-stu-id="2df1b-160">Subnet address range</span></span>     |<span data-ttu-id="2df1b-161">10.1.1.0/24</span><span class="sxs-lookup"><span data-stu-id="2df1b-161">10.1.1.0/24</span></span>|

6. <span data-ttu-id="2df1b-162">您應會看到稍早建立的訂用帳戶填入 [訂用帳戶] 欄位中。</span><span class="sxs-lookup"><span data-stu-id="2df1b-162">You should see the Subscription you created earlier populated in the **Subscription** field.</span></span>

    <span data-ttu-id="2df1b-163">a.</span><span class="sxs-lookup"><span data-stu-id="2df1b-163">a.</span></span> <span data-ttu-id="2df1b-164">針對 [資源群組]，您可以建立資源群組，如果您已經有資源群組，請選取 [使用現有的]。</span><span class="sxs-lookup"><span data-stu-id="2df1b-164">For Resource Group, you can either create a Resource Group or if you already have one, select **Use existing**.</span></span>

    <span data-ttu-id="2df1b-165">b.</span><span class="sxs-lookup"><span data-stu-id="2df1b-165">b.</span></span> <span data-ttu-id="2df1b-166">驗證預設位置。</span><span class="sxs-lookup"><span data-stu-id="2df1b-166">Verify the default location.</span></span>

    <span data-ttu-id="2df1b-167">c.</span><span class="sxs-lookup"><span data-stu-id="2df1b-167">c.</span></span> <span data-ttu-id="2df1b-168">按一下 [釘選到儀表板]。</span><span class="sxs-lookup"><span data-stu-id="2df1b-168">Click **Pin to dashboard**.</span></span>

    <span data-ttu-id="2df1b-169">d.</span><span class="sxs-lookup"><span data-stu-id="2df1b-169">d.</span></span> <span data-ttu-id="2df1b-170">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="2df1b-170">Click **Create**.</span></span>



#### <a name="create-the-gateway-subnet"></a><span data-ttu-id="2df1b-171">建立閘道子網路</span><span class="sxs-lookup"><span data-stu-id="2df1b-171">Create the gateway subnet</span></span>
1. <span data-ttu-id="2df1b-172">從儀表板開啟您建立的虛擬網路資源 (Tenant1VNet1)。</span><span class="sxs-lookup"><span data-stu-id="2df1b-172">Open the Virtual Network resource you created (Tenant1VNet1) from the dashboard.</span></span>
2. <span data-ttu-id="2df1b-173">在 [設定] 區段上，選取 [子網路]。</span><span class="sxs-lookup"><span data-stu-id="2df1b-173">On the Settings section, select **Subnets**.</span></span>
3. <span data-ttu-id="2df1b-174">按一下 [閘道子網路]﹐將閘道子網路新增至虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="2df1b-174">Click **Gateway Subnet** to add a gateway subnet to the virtual network.</span></span>
   
    ![](media/azure-stack-connect-expressroute/gatewaysubnet.png)
4. <span data-ttu-id="2df1b-175">子網路名稱預設為 **GatewaySubnet**。</span><span class="sxs-lookup"><span data-stu-id="2df1b-175">The name of the subnet is set to **GatewaySubnet** by default.</span></span>
   <span data-ttu-id="2df1b-176">閘道子網路很特別﹐必須具有此特定名稱，才能正常運作。</span><span class="sxs-lookup"><span data-stu-id="2df1b-176">Gateway subnets are special and must have this specific name to function properly.</span></span>
5. <span data-ttu-id="2df1b-177">在 [位址範圍] 欄位中，確認位址是 **10.1.0.0/24**。</span><span class="sxs-lookup"><span data-stu-id="2df1b-177">In the **Address range** field, verify the address is **10.1.0.0/24**.</span></span>
6. <span data-ttu-id="2df1b-178">按一下 [確定] 以建立閘道子網路。</span><span class="sxs-lookup"><span data-stu-id="2df1b-178">Click **OK** to create the gateway subnet.</span></span>

#### <a name="create-the-virtual-network-gateway"></a><span data-ttu-id="2df1b-179">建立虛擬網路閘道</span><span class="sxs-lookup"><span data-stu-id="2df1b-179">Create the virtual network gateway</span></span>
1. <span data-ttu-id="2df1b-180">在 Azure Stack 使用者入口網站中，按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="2df1b-180">In the Azure Stack user portal, click **New**.</span></span>
   
2. <span data-ttu-id="2df1b-181">從 Marketplace 功能表中選取 [網路]。</span><span class="sxs-lookup"><span data-stu-id="2df1b-181">Select **Networking** from the Marketplace menu.</span></span>
3. <span data-ttu-id="2df1b-182">從網路資源清單中選取 [虛擬網路閘道]。</span><span class="sxs-lookup"><span data-stu-id="2df1b-182">Select **Virtual network gateway** from the list of network resources.</span></span>
4. <span data-ttu-id="2df1b-183">在 [名稱] 欄位中輸入 **GW1**。</span><span class="sxs-lookup"><span data-stu-id="2df1b-183">In the **Name** field type **GW1**.</span></span>
5. <span data-ttu-id="2df1b-184">按一下 [虛擬網路] 項目以選擇虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="2df1b-184">Click the **Virtual network** item to choose a virtual network.</span></span>
   <span data-ttu-id="2df1b-185">從清單中選取 [Tenant1VNet1]。</span><span class="sxs-lookup"><span data-stu-id="2df1b-185">Select **Tenant1VNet1** from the list.</span></span>
6. <span data-ttu-id="2df1b-186">按一下 [公用 IP 位址] 功能表項目。</span><span class="sxs-lookup"><span data-stu-id="2df1b-186">Click the **Public IP address** menu item.</span></span> <span data-ttu-id="2df1b-187">當 [選擇公用 IP 位址] 區段開啟時﹐按一下 [新建]。</span><span class="sxs-lookup"><span data-stu-id="2df1b-187">When the **Choose public IP address** section opens click **Create new**.</span></span>
7. <span data-ttu-id="2df1b-188">在 [名稱] 欄位中，輸入 **GW1-PiP**﹐然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="2df1b-188">In the **Name** field, type **GW1-PiP** and click **OK**.</span></span>
8. <span data-ttu-id="2df1b-189">[VPN 類型] 預設應選取 [路由式]。</span><span class="sxs-lookup"><span data-stu-id="2df1b-189">The **VPN type** should have **Route-based** selected by default.</span></span>
    <span data-ttu-id="2df1b-190">保留此設定。</span><span class="sxs-lookup"><span data-stu-id="2df1b-190">Keep this setting.</span></span>
9. <span data-ttu-id="2df1b-191">確認 [訂用帳戶] 和 [位置] 均正確無誤。</span><span class="sxs-lookup"><span data-stu-id="2df1b-191">Verify that **Subscription** and **Location** are correct.</span></span> <span data-ttu-id="2df1b-192">想要的話，您可以將資源釘選到儀表板。</span><span class="sxs-lookup"><span data-stu-id="2df1b-192">You can pin the resource to the Dashboard if you want.</span></span> <span data-ttu-id="2df1b-193">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="2df1b-193">Click **Create**.</span></span>

#### <a name="create-the-local-network-gateway"></a><span data-ttu-id="2df1b-194">建立區域網路閘道</span><span class="sxs-lookup"><span data-stu-id="2df1b-194">Create the local network gateway</span></span>

<span data-ttu-id="2df1b-195">區域網路閘道資源的目的是指出 VPN 連線另一端的遠端閘道。</span><span class="sxs-lookup"><span data-stu-id="2df1b-195">The purpose of the Local network gateway resource is to indicate the remote gateway at the other end of the VPN connection.</span></span> <span data-ttu-id="2df1b-196">在此範例中，遠端是 ExpressRoute 路由器的 LAN 子介面。</span><span class="sxs-lookup"><span data-stu-id="2df1b-196">For this example, the remote side is the LAN subinterface of the ExpressRoute router.</span></span> <span data-ttu-id="2df1b-197">對於此範例中的租用戶 1，遠端位址是 10.60.3.255，如圖 2 所示。</span><span class="sxs-lookup"><span data-stu-id="2df1b-197">For Tenant 1 in this example, the remote address is 10.60.3.255 as shown in Diagram 2.</span></span>

1. <span data-ttu-id="2df1b-198">登入 Azure Stack 實體機器。</span><span class="sxs-lookup"><span data-stu-id="2df1b-198">Log in to the Azure Stack physical machine.</span></span>
2. <span data-ttu-id="2df1b-199">以您的使用者帳戶登入使用者入口網站，然後按一下新增。</span><span class="sxs-lookup"><span data-stu-id="2df1b-199">Sign in to the user portal with your user account and click **New**.</span></span>
3. <span data-ttu-id="2df1b-200">從 Marketplace 功能表中選取 [網路]。</span><span class="sxs-lookup"><span data-stu-id="2df1b-200">Select **Networking** from the Marketplace menu.</span></span>
4. <span data-ttu-id="2df1b-201">從資源清單中選取 [區域網路閘道]。</span><span class="sxs-lookup"><span data-stu-id="2df1b-201">Select **local network gateway** from the list of resources.</span></span>
5. <span data-ttu-id="2df1b-202">在 [名稱] 欄位中輸入 **ER-Router-GW**。</span><span class="sxs-lookup"><span data-stu-id="2df1b-202">In the **Name** field type **ER-Router-GW**.</span></span>
6. <span data-ttu-id="2df1b-203">關於 [IP 位址] 欄位，請參閱圖 2。</span><span class="sxs-lookup"><span data-stu-id="2df1b-203">For the **IP address** field, refer to Diagram 2.</span></span> <span data-ttu-id="2df1b-204">對於租用戶 1，ExpressRoute 路由器的 LAN 子介面 IP 位址是 10.60.3.255。</span><span class="sxs-lookup"><span data-stu-id="2df1b-204">The IP address of the ExpressRoute router's LAN subinterface for Tenant 1 is 10.60.3.255.</span></span> <span data-ttu-id="2df1b-205">根據您自己的環境，輸入路由器相對應介面的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="2df1b-205">For your own environment, type the IP address of your router's corresponding interface.</span></span>
7. <span data-ttu-id="2df1b-206">在 [位址空間] 欄位中，輸入您想要連線至 Azure 中之 VNet 的位址空間。</span><span class="sxs-lookup"><span data-stu-id="2df1b-206">In the **Address Space** field, type the address space of the VNets that you want to connect to in Azure.</span></span> <span data-ttu-id="2df1b-207">關於此範例，請參閱圖 2。</span><span class="sxs-lookup"><span data-stu-id="2df1b-207">For this example, refer to Diagram 2.</span></span> <span data-ttu-id="2df1b-208">對於租用戶 1，請注意，必要的子網路是 **192.168.2.0/24** (這是 Azure 中的中樞 VNet) 和 **10.100.0.0/16** (這是 Azure 中的輪輻 VNet)。</span><span class="sxs-lookup"><span data-stu-id="2df1b-208">For Tenant 1, notice that the required subnets are **192.168.2.0/24** (this is the Hub Vnet in Azure) and **10.100.0.0/16** (this is the Spoke VNet in Azure).</span></span> <span data-ttu-id="2df1b-209">根據您自己的環境，輸入相對應的子網路。</span><span class="sxs-lookup"><span data-stu-id="2df1b-209">Type the corresponding subnets for your own environment.</span></span>
   > [!IMPORTANT]
   > <span data-ttu-id="2df1b-210">對於 Azure Stack 閘道和 ExpressRoute 路由器之間的站對站 VPN 連線，這個範例假設您使用靜態路由。</span><span class="sxs-lookup"><span data-stu-id="2df1b-210">This example assumes you are using static routes for the Site-to-Site VPN connection between the Azure Stack gateway and the ExpressRoute router.</span></span>

8. <span data-ttu-id="2df1b-211">確認您的 [訂用帳戶]、[資源群組] 和 [位置] 都正確無誤，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="2df1b-211">Verify that your **Subscription**, **Resource Group**, and **Location** are all correct and click **Create**.</span></span>

#### <a name="create-the-connection"></a><span data-ttu-id="2df1b-212">建立連線</span><span class="sxs-lookup"><span data-stu-id="2df1b-212">Create the connection</span></span>
1. <span data-ttu-id="2df1b-213">在 Azure Stack 使用者入口網站中，按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="2df1b-213">In the Azure Stack user portal, click **New**.</span></span>
2. <span data-ttu-id="2df1b-214">從 Marketplace 功能表中選取 [網路]。</span><span class="sxs-lookup"><span data-stu-id="2df1b-214">Select **Networking** from the Marketplace menu.</span></span>
3. <span data-ttu-id="2df1b-215">從資源清單中選取 [連線]。</span><span class="sxs-lookup"><span data-stu-id="2df1b-215">Select **Connection** from the list of resources.</span></span>
4. <span data-ttu-id="2df1b-216">在 [基本] 設定區段中，選擇 [站對站 (IPSec)] 作為 [連線類型]。</span><span class="sxs-lookup"><span data-stu-id="2df1b-216">In the **Basics** settings section, choose **Site-to-site (IPSec)** as the **Connection type**.</span></span>
5. <span data-ttu-id="2df1b-217">選取 [訂用帳戶]、[資源群組] 和 [位置]﹐然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="2df1b-217">Select the **Subscription**, **Resource Group**, and **Location** and click **OK**.</span></span>
6. <span data-ttu-id="2df1b-218">在 [設定] 區段中，按一下 [虛擬網路閘道]，然後按一下 [GW1]。</span><span class="sxs-lookup"><span data-stu-id="2df1b-218">In the **Settings** section,  click **Virtual network gateway** click **GW1**.</span></span>
7. <span data-ttu-id="2df1b-219">按一下 [區域網路閘道]，然後按一下 [ER 路由器 GW]。</span><span class="sxs-lookup"><span data-stu-id="2df1b-219">Click **Local network gateway**, and click **ER Router GW**.</span></span>
8. <span data-ttu-id="2df1b-220">在 [連線名稱] 欄位中，輸入 **ConnectToAzure**。</span><span class="sxs-lookup"><span data-stu-id="2df1b-220">In the **Connection Name** field, type **ConnectToAzure**.</span></span>
9. <span data-ttu-id="2df1b-221">在 [共用金鑰 (PSK)] 欄位中輸入 **abc123**﹐然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="2df1b-221">In the **Shared key (PSK)** field, type **abc123** and click **OK**.</span></span>
10. <span data-ttu-id="2df1b-222">在 [摘要] 區段上，按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="2df1b-222">On the **Summary** section, click **OK**.</span></span>

    <span data-ttu-id="2df1b-223">建立連線之後，您就可以看到虛擬網路閘道所使用的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="2df1b-223">After the connection is created, you can see the public IP address used by the virtual network gateway.</span></span> <span data-ttu-id="2df1b-224">若要在 Azure Stack 入口網站中找出位址，請瀏覽至您的虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="2df1b-224">To find the address in the Azure Stack portal, browse to your Virtual network gateway.</span></span> <span data-ttu-id="2df1b-225">在 [概觀] 中，尋找 [公用 IP 位址]。</span><span class="sxs-lookup"><span data-stu-id="2df1b-225">In **Overview**, find the **Public IP address**.</span></span> <span data-ttu-id="2df1b-226">請記下這個位址。下一節會將它用作「內部 IP 位址」(如果適用於您的部署)。</span><span class="sxs-lookup"><span data-stu-id="2df1b-226">Note this address; you will use it as the *Internal IP address* in the next section (if applicable for your deployment).</span></span>

    ![](media/azure-stack-connect-expressroute/GWPublicIP.png)

#### <a name="create-a-virtual-machine"></a><span data-ttu-id="2df1b-227">建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="2df1b-227">Create a virtual machine</span></span>
<span data-ttu-id="2df1b-228">若要驗證透過 VPN 連線傳輸的資料，您需要虛擬機器在 Azure Stack Vnet 中傳送和接收資料。</span><span class="sxs-lookup"><span data-stu-id="2df1b-228">To validate data traveling through the VPN Connection, you need virtual machines to send and receive data in the Azure Stack Vnet.</span></span> <span data-ttu-id="2df1b-229">現在，請建立虛擬機器，並將它放在您的虛擬網路中的 VM 子網路上。</span><span class="sxs-lookup"><span data-stu-id="2df1b-229">Create a virtual machine now and put it in your VM subnet in your virtual network.</span></span>

1. <span data-ttu-id="2df1b-230">在 Azure Stack 使用者入口網站中，按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="2df1b-230">In the Azure Stack user portal, click **New**.</span></span>
2. <span data-ttu-id="2df1b-231">從 Marketplace 功能表選取 [虛擬機器]。</span><span class="sxs-lookup"><span data-stu-id="2df1b-231">Select **Virtual Machines** from the Marketplace menu.</span></span>
3. <span data-ttu-id="2df1b-232">在虛擬機器映像清單中，選取 [Windows Server 2016 Datacenter 評估版] 映像，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="2df1b-232">In the list of virtual machine images, select the **Windows Server 2016 Datacenter Eval** image and click **Create**.</span></span>
4. <span data-ttu-id="2df1b-233">在 [基本] 區段的 [名稱] 欄位中，輸入 **VM01**。</span><span class="sxs-lookup"><span data-stu-id="2df1b-233">On the **Basics** section, in the **Name** field type **VM01**.</span></span>
5. <span data-ttu-id="2df1b-234">輸入有效的使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="2df1b-234">Type a valid user name and password.</span></span> <span data-ttu-id="2df1b-235">建立 VM 之後﹐您將使用此帳戶來登入 VM。</span><span class="sxs-lookup"><span data-stu-id="2df1b-235">You’ll use this account to log in to the VM after it has been created.</span></span>
6. <span data-ttu-id="2df1b-236">提供 訂用帳戶、資源群組 和 位置﹐然後按一下確定。</span><span class="sxs-lookup"><span data-stu-id="2df1b-236">Provide a **Subscription**, **Resource Group**, and **Location** and then click **OK**.</span></span>
7. <span data-ttu-id="2df1b-237">在 大小 區段上，按一下此執行個體的虛擬機器大小，然後按一下選取。</span><span class="sxs-lookup"><span data-stu-id="2df1b-237">On the **Size** section, click a virtual machine size for this instance and then click **Select**.</span></span>
8. <span data-ttu-id="2df1b-238">在 [設定] 區段上，您可以接受預設值。</span><span class="sxs-lookup"><span data-stu-id="2df1b-238">On the **Settings** section, you can accept the defaults.</span></span> <span data-ttu-id="2df1b-239">但請確定選取的虛擬網路是 **Tenant1VNet1**，而子網路設定為 **10.1.1.0/24**。</span><span class="sxs-lookup"><span data-stu-id="2df1b-239">But ensure the virtual network selected is **Tenant1VNet1** and the subnet is set to **10.1.1.0/24**.</span></span> <span data-ttu-id="2df1b-240">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="2df1b-240">Click **OK**.</span></span>
9. <span data-ttu-id="2df1b-241">檢閱 [摘要] 區段上的設定，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="2df1b-241">Review the settings on the **Summary** section and click **OK**.</span></span>

<span data-ttu-id="2df1b-242">針對您想要連線的每個租用戶 VNet，重複執行從**建立虛擬網路和 VM 子網路**到**建立虛擬機器**各節的步驟。</span><span class="sxs-lookup"><span data-stu-id="2df1b-242">For each tenant VNet you want to connect, repeat the previous steps from **Create the virtual network and VM subnet** through **Create a virtual machine** sections.</span></span>

### <a name="configure-the-nat-virtual-machine-for-gateway-traversal"></a><span data-ttu-id="2df1b-243">設定用於閘道周遊的 NAT 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="2df1b-243">Configure the NAT virtual machine for gateway traversal</span></span>
> [!IMPORTANT]
> <span data-ttu-id="2df1b-244">本節僅適用於 Azure Stack 開發套件部署。</span><span class="sxs-lookup"><span data-stu-id="2df1b-244">This section is for Azure Stack Development Kit deployments only.</span></span> <span data-ttu-id="2df1b-245">多重節點部署不需要 NAT。</span><span class="sxs-lookup"><span data-stu-id="2df1b-245">The NAT is not needed for multi-node deployments.</span></span>

<span data-ttu-id="2df1b-246">Azure Stack 開發套件是獨立的，而且與部署實體主機的網路隔離。</span><span class="sxs-lookup"><span data-stu-id="2df1b-246">The Azure Stack Development Kit is self-contained and isolated from the network on which the physical host is deployed.</span></span> <span data-ttu-id="2df1b-247">因此，閘道所連線的「外部」VIP 網路不是在外部，而是隱藏在執行網路位址轉譯 (NAT) 的路由器背後。</span><span class="sxs-lookup"><span data-stu-id="2df1b-247">So, the “External” VIP network that the gateways are connected to is not external, but instead is hidden behind a router doing Network Address Translation (NAT).</span></span>
 
<span data-ttu-id="2df1b-248">路由器是 Windows Server 虛擬機器 (**AzS-BGPNAT01**)，在 Azure Stack 開發套件基礎結構中扮演「路由及遠端存取服務」(RRAS) 角色。</span><span class="sxs-lookup"><span data-stu-id="2df1b-248">The router is a Windows Server virtual machine (**AzS-BGPNAT01**) running the Routing and Remote Access Services (RRAS) role in the Azure Stack Development Kit infrastructure.</span></span> <span data-ttu-id="2df1b-249">您必須在 AzS-BGPNAT01 虛擬機器上設定 NAT，允許以站對站 VPN 連線來連線兩端。</span><span class="sxs-lookup"><span data-stu-id="2df1b-249">You must configure NAT on the AzS-BGPNAT01 virtual machine to allow the Site-to-Site VPN Connection to connect on both ends.</span></span>

#### <a name="configure-the-nat"></a><span data-ttu-id="2df1b-250">設定 NAT</span><span class="sxs-lookup"><span data-stu-id="2df1b-250">Configure the NAT</span></span>

1. <span data-ttu-id="2df1b-251">以您的系統管理員帳戶登入 Azure Stack 實體機器。</span><span class="sxs-lookup"><span data-stu-id="2df1b-251">Log in to the Azure Stack physical machine with your administrator account.</span></span>
2. <span data-ttu-id="2df1b-252">複製和編輯下列 PowerShell 指令碼，然後在提升權限的 Windows PowerShell ISE 中執行。</span><span class="sxs-lookup"><span data-stu-id="2df1b-252">Copy and edit the following PowerShell script and run in an elevated Windows PowerShell ISE.</span></span> <span data-ttu-id="2df1b-253">取代您的系統管理員密碼。</span><span class="sxs-lookup"><span data-stu-id="2df1b-253">Replace your administrator password.</span></span> <span data-ttu-id="2df1b-254">傳回的位址是您的「外部 BGPNAT 位址」。</span><span class="sxs-lookup"><span data-stu-id="2df1b-254">The address returned is your *External BGPNAT address*.</span></span>

   ```
   cd \AzureStack-Tools-master\connect
   Import-Module .\AzureStack.Connect.psm1
   $Password = ConvertTo-SecureString "<your administrator password>" `
    -AsPlainText `
    -Force
   Get-AzureStackNatServerAddress `
    -HostComputer "azs-bgpnat01" `
    -Password $Password
   ```
4. <span data-ttu-id="2df1b-255">若要設定 NAT，請複製和編輯下列 PowerShell 指令碼，然後在提升權限的 Windows PowerShell ISE 中執行。</span><span class="sxs-lookup"><span data-stu-id="2df1b-255">To configure the NAT, copy and edit the following PowerShell script and run in an elevated Windows PowerShell ISE.</span></span> <span data-ttu-id="2df1b-256">編輯指令碼來取代「外部 BGPNAT 位址」和「內部 IP 位址」(您先前在**建立連線**一節中記下的值)。</span><span class="sxs-lookup"><span data-stu-id="2df1b-256">Edit the script to replace the *External BGPNAT address* and *Internal IP address* (which you noted previously in the **Create the Connection** section).</span></span>

   <span data-ttu-id="2df1b-257">在範例圖表中，「外部 BGPNAT 位址」是 10.10.0.62，「內部 IP 位址」是 192.168.102.1。</span><span class="sxs-lookup"><span data-stu-id="2df1b-257">In the example diagrams, the *External BGPNAT address* is 10.10.0.62 and the *Internal IP address* is 192.168.102.1.</span></span>

   ```
   # Designate the external NAT address for the ports that use the IKE authentication.
   Invoke-Command `
    -ComputerName azs-bgpnat01 `
     {Add-NetNatExternalAddress `
      -NatName BGPNAT `
      -IPAddress <External BGPNAT address> `
      -PortStart 499 `
      -PortEnd 501}
   Invoke-Command `
    -ComputerName azs-bgpnat01 `
     {Add-NetNatExternalAddress `
      -NatName BGPNAT `
      -IPAddress <External BGPNAT address> `
      -PortStart 4499 `
      -PortEnd 4501}
   # create a static NAT mapping to map the external address to the Gateway
   # Public IP Address to map the ISAKMP port 500 for PHASE 1 of the IPSEC tunnel
   Invoke-Command `
    -ComputerName azs-bgpnat01 `
     {Add-NetNatStaticMapping `
      -NatName BGPNAT `
      -Protocol UDP `
      -ExternalIPAddress <External BGPNAT address> `
      -InternalIPAddress <Internal IP address> `
      -ExternalPort 500 `
      -InternalPort 500}
   # Finally, configure NAT traversal which uses port 4500 to
   # successfully establish the complete IPSEC tunnel over NAT devices
   Invoke-Command `
    -ComputerName azs-bgpnat01 `
     {Add-NetNatStaticMapping `
      -NatName BGPNAT `
      -Protocol UDP `
      -ExternalIPAddress <External BGPNAT address> `
      -InternalIPAddress <Internal IP address> `
      -ExternalPort 4500 `
      -InternalPort 4500}
   ```

## <a name="configure-azure"></a><span data-ttu-id="2df1b-258">設定 Azure</span><span class="sxs-lookup"><span data-stu-id="2df1b-258">Configure Azure</span></span>
<span data-ttu-id="2df1b-259">既然您已完成 Azure Stack 設定，再來可以部署一些 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="2df1b-259">Now that you have completed the Azure Stack configuration, you can deploy some Azure resources.</span></span> <span data-ttu-id="2df1b-260">下圖顯示 Azure 中的範例租用戶虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="2df1b-260">The following diagram shows a sample tenant virtual network in Azure.</span></span> <span data-ttu-id="2df1b-261">針對您在 Azure 中的 VNet，您可以使用任何名稱和定址配置。</span><span class="sxs-lookup"><span data-stu-id="2df1b-261">You can use any name and addressing scheme for your VNet in Azure.</span></span> <span data-ttu-id="2df1b-262">不過，在 Azure 和 Azure Stack 中，VNet 的位址範圍必須是唯一的，而且不重疊。</span><span class="sxs-lookup"><span data-stu-id="2df1b-262">However, the address range of the VNets in Azure and Azure Stack must be unique and not overlap.</span></span>

![Azure Vnet](media/azure-stack-connect-expressroute/AzureArchitecture.png)

<span data-ttu-id="2df1b-264">**圖表 3**</span><span class="sxs-lookup"><span data-stu-id="2df1b-264">**Diagram 3**</span></span>

<span data-ttu-id="2df1b-265">您在 Azure 中部署的資源，類似於您在 Azure Stack 中部署的資源。</span><span class="sxs-lookup"><span data-stu-id="2df1b-265">The resources you deploy in Azure are similar to the resources you deployed in Azure Stack.</span></span> <span data-ttu-id="2df1b-266">同樣地，您需要部署：</span><span class="sxs-lookup"><span data-stu-id="2df1b-266">Similarly, you deploy:</span></span>
* <span data-ttu-id="2df1b-267">虛擬網路和子網路</span><span class="sxs-lookup"><span data-stu-id="2df1b-267">Virtual networks and subnets</span></span>
* <span data-ttu-id="2df1b-268">閘道子網路</span><span class="sxs-lookup"><span data-stu-id="2df1b-268">A gateway subnet</span></span>
* <span data-ttu-id="2df1b-269">虛擬網路閘道</span><span class="sxs-lookup"><span data-stu-id="2df1b-269">A virtual network gateway</span></span>
* <span data-ttu-id="2df1b-270">連線</span><span class="sxs-lookup"><span data-stu-id="2df1b-270">A connection</span></span>
* <span data-ttu-id="2df1b-271">ExpressRoute 線路</span><span class="sxs-lookup"><span data-stu-id="2df1b-271">An ExpressRoute circuit</span></span>

<span data-ttu-id="2df1b-272">範例 Azure 網路基礎結構的設定方式如下：</span><span class="sxs-lookup"><span data-stu-id="2df1b-272">The example Azure network infrastructure is configured in the following way:</span></span>
* <span data-ttu-id="2df1b-273">使用標準中樞 (192.168.2.0/24) 和輪輻 (10.100.0.0./16) VNet 模型。</span><span class="sxs-lookup"><span data-stu-id="2df1b-273">A standard hub (192.168.2.0/24) and spoke (10.100.0.0./16) VNet model is used.</span></span>
* <span data-ttu-id="2df1b-274">工作負載部署在輪輻 Vnet 中，而 ExpressRoute 線路連線至中樞 VNet。</span><span class="sxs-lookup"><span data-stu-id="2df1b-274">The workloads are deployed in the spoke Vnet and the ExpressRoute circuit is connected to the hub VNet.</span></span>
* <span data-ttu-id="2df1b-275">透過 VNet 對等互連功能來連結這兩個 VNet。</span><span class="sxs-lookup"><span data-stu-id="2df1b-275">The two VNets are linked using the VNet peering feature.</span></span>

### <a name="configure-vnets"></a><span data-ttu-id="2df1b-276">設定 Vnet</span><span class="sxs-lookup"><span data-stu-id="2df1b-276">Configure Vnets</span></span>
1. <span data-ttu-id="2df1b-277">使用您的 Azure 認證登入 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="2df1b-277">Sign in to the Azure portal with your Azure credentials.</span></span>
2. <span data-ttu-id="2df1b-278">使用 192.168.2.0/24 位址空間建立中樞 VNet。</span><span class="sxs-lookup"><span data-stu-id="2df1b-278">Create the hub VNet using the 192.168.2.0/24 address space.</span></span> <span data-ttu-id="2df1b-279">使用 192.168.2.0/25 位址範圍建立子網路，並使用 192.168.2.128/27 位址範圍新增閘道子網路。</span><span class="sxs-lookup"><span data-stu-id="2df1b-279">Create a subnet using the 192.168.2.0/25 address range, and add a gateway subnet using the 192.168.2.128/27 address range.</span></span>
3. <span data-ttu-id="2df1b-280">使用 10.100.0.0/16 位址範圍建立輪輻 VNet 和子網路。</span><span class="sxs-lookup"><span data-stu-id="2df1b-280">Create the spoke VNet and subnet using the 10.100.0.0/16 address range.</span></span>


<span data-ttu-id="2df1b-281">如需有關在 Azure 中建立虛擬網路的詳細資訊，請參閱[建立有多個子網路的虛擬網路](../virtual-network/virtual-networks-create-vnet-arm-pportal.md)。</span><span class="sxs-lookup"><span data-stu-id="2df1b-281">For more information about creating virtual networks in Azure, see [Create a virtual network with multiple subnets](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span></span>

### <a name="configure-an-expressroute-circuit"></a><span data-ttu-id="2df1b-282">設定 ExpressRoute 線路</span><span class="sxs-lookup"><span data-stu-id="2df1b-282">Configure an ExpressRoute circuit</span></span>

1. <span data-ttu-id="2df1b-283">檢閱 [ExpressRoute 必要條件和檢查清單](../expressroute/expressroute-prerequisites.md)中的 ExpressRoute 必要條件。</span><span class="sxs-lookup"><span data-stu-id="2df1b-283">Review the ExpressRoute prerequisites in [ExpressRoute prerequisites & checklist](../expressroute/expressroute-prerequisites.md).</span></span>
2. <span data-ttu-id="2df1b-284">請依照[建立和修改 ExpressRoute 線路](../expressroute/expressroute-howto-circuit-portal-resource-manager.md)中的步驟，使用您的 Azure 訂用帳戶建立 ExpressRoute 線路。</span><span class="sxs-lookup"><span data-stu-id="2df1b-284">Follow the steps in [Create and modify an ExpressRoute circuit](../expressroute/expressroute-howto-circuit-portal-resource-manager.md) to create an ExpressRoute circuit using your Azure subscription.</span></span>
3. <span data-ttu-id="2df1b-285">將上一個步驟中的服務金鑰分享給主機服務提供者，以便在他們那一端佈建您的 ExpressRoute 線路。</span><span class="sxs-lookup"><span data-stu-id="2df1b-285">Share the service key from the previous step with your hoster/provider to provision your ExpressRoute circuit at their end.</span></span>
4. <span data-ttu-id="2df1b-286">請依照[建立和修改 ExpressRoute 線路的對等互連](../expressroute/expressroute-howto-routing-portal-resource-manager.md)中的步驟，在 ExpressRoute 線路上設定私用對等互連。</span><span class="sxs-lookup"><span data-stu-id="2df1b-286">Follow the steps in [Create and modify peering for an ExpressRoute circuit](../expressroute/expressroute-howto-routing-portal-resource-manager.md) to configure private peering on the ExpressRoute circuit.</span></span>

### <a name="create-the-virtual-network-gateway"></a><span data-ttu-id="2df1b-287">建立虛擬網路閘道</span><span class="sxs-lookup"><span data-stu-id="2df1b-287">Create the virtual network gateway</span></span>

* <span data-ttu-id="2df1b-288">請依照[使用 PowerShell 為 ExpressRoute 設定虛擬網路閘道](../expressroute/expressroute-howto-add-gateway-resource-manager.md)中的步驟，在中樞 VNet 中為 ExpressRoute 建立虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="2df1b-288">Follow the steps in [Configure a virtual network gateway for ExpressRoute using PowerShell](../expressroute/expressroute-howto-add-gateway-resource-manager.md) to create a virtual network gateway for ExpressRoute in the hub VNet.</span></span>

### <a name="create-the-connection"></a><span data-ttu-id="2df1b-289">建立連線</span><span class="sxs-lookup"><span data-stu-id="2df1b-289">Create the connection</span></span>

* <span data-ttu-id="2df1b-290">若要將 ExpressRoute 線路連結至中樞 VNet，請依照[將虛擬網路連線至 ExpressRoute 線路](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md)中的步驟。</span><span class="sxs-lookup"><span data-stu-id="2df1b-290">To link the ExpressRoute circuit to the hub VNet, follow the steps in [Connect a virtual network to an ExpressRoute circuit](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md).</span></span>

### <a name="peer-the-vnets"></a><span data-ttu-id="2df1b-291">將 Vnet 對等互連</span><span class="sxs-lookup"><span data-stu-id="2df1b-291">Peer the Vnets</span></span>

* <span data-ttu-id="2df1b-292">依照[使用 Azure 入口網站建立虛擬網路對等互連](../virtual-network/virtual-networks-create-vnetpeering-arm-portal.md)中的步驟，將中樞和輪輻 VNet 對等互連。</span><span class="sxs-lookup"><span data-stu-id="2df1b-292">Peer the Hub and Spoke VNets using the steps in [Create a virtual network peering using the Azure portal](../virtual-network/virtual-networks-create-vnetpeering-arm-portal.md).</span></span> <span data-ttu-id="2df1b-293">設定 VNet 對等互連時，務必選取下列選項：</span><span class="sxs-lookup"><span data-stu-id="2df1b-293">When configuring VNet peering, ensure you select the following options:</span></span>
   * <span data-ttu-id="2df1b-294">從中樞至輪輻：**允許閘道傳輸**</span><span class="sxs-lookup"><span data-stu-id="2df1b-294">From hub to spoke: **Allow gateway transit**</span></span>
   * <span data-ttu-id="2df1b-295">從輪輻至中樞：**使用遠端閘道**</span><span class="sxs-lookup"><span data-stu-id="2df1b-295">From spoke to hub: **Use remote gateway**</span></span>

### <a name="create-a-virtual-machine"></a><span data-ttu-id="2df1b-296">建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="2df1b-296">Create a virtual machine</span></span>

* <span data-ttu-id="2df1b-297">將工作負載虛擬機器部署至輪輻 VNet。</span><span class="sxs-lookup"><span data-stu-id="2df1b-297">Deploy your workload virtual machines into the spoke VNet.</span></span>

<span data-ttu-id="2df1b-298">對於您在 Azure 中想要透過各自 ExpressRoute 線路來連線的其他任何租用戶 VNet，重複這些步驟。</span><span class="sxs-lookup"><span data-stu-id="2df1b-298">Repeat these steps for any additional tenant VNets you want to connect in Azure through their respective ExpressRoute circuits.</span></span>

## <a name="configure-the-router"></a><span data-ttu-id="2df1b-299">設定路由器</span><span class="sxs-lookup"><span data-stu-id="2df1b-299">Configure the router</span></span>

<span data-ttu-id="2df1b-300">您可以參考下列端對端基礎結構圖表，以指引您設定 ExpressRoute 路由器。</span><span class="sxs-lookup"><span data-stu-id="2df1b-300">You can use the following end-to-end infrastructure diagram to guide the configuration of your ExpressRoute Router.</span></span> <span data-ttu-id="2df1b-301">這個圖表顯示兩個租用戶 (租用戶 1 和租用戶 2)，有各自的 Express Route 線路。</span><span class="sxs-lookup"><span data-stu-id="2df1b-301">This diagram shows two tenants (Tenant 1 and Tenant 2) with their respective Express Route circuits.</span></span> <span data-ttu-id="2df1b-302">每個都連結至各自在 ExpressRoute 路由器 LAN 和 WAN 端的 VRF (虛擬路由和轉送)，以確保兩個租用戶之間的端對端隔離。</span><span class="sxs-lookup"><span data-stu-id="2df1b-302">Each is linked to their own VRF (Virtual Routing and Forwarding) in the LAN and WAN side of the ExpressRoute router to ensure end-to-end isolation between the two tenants.</span></span> <span data-ttu-id="2df1b-303">隨著您進行範例設定，請記下路由器介面中使用的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="2df1b-303">Note the IP addresses used in the router interfaces as you follow the sample configuration.</span></span>

![端對端圖表](media/azure-stack-connect-expressroute/EndToEnd.png)

<span data-ttu-id="2df1b-305">**圖表 4**</span><span class="sxs-lookup"><span data-stu-id="2df1b-305">**Diagram 4**</span></span>

<span data-ttu-id="2df1b-306">您可以使用任何支援 IKEv2 VPN 和 BGP 的路由器，以終止 Azure Stack 的站對站 VPN 連線。</span><span class="sxs-lookup"><span data-stu-id="2df1b-306">You can use any router that supports IKEv2 VPN and BGP to terminate the Site-to-Site VPN connection from Azure Stack.</span></span> <span data-ttu-id="2df1b-307">相同的路由器用於透過 ExpressRoute 線路來連線至 Azure。</span><span class="sxs-lookup"><span data-stu-id="2df1b-307">The same router is used to connect to Azure using an ExpressRoute circuit.</span></span> 

<span data-ttu-id="2df1b-308">以下是 Cisco ASR 1000 的範例設定，支援圖表 4 所示的網路基礎結構：</span><span class="sxs-lookup"><span data-stu-id="2df1b-308">Here is a sample configuration from a Cisco ASR 1000 that supports the network infrastructure shown in Diagram 4:</span></span>

```
ip vrf Tenant 1
 description Routing Domain for PRIVATE peering to Azure for Tenant 1
 rd 1:1
!
ip vrf Tenant 2
 description Routing Domain for PRIVATE peering to Azure for Tenant 2
 rd 1:5
!
crypto ikev2 proposal V2-PROPOSAL2 
description IKEv2 proposal for Tenant 1 
encryption aes-cbc-256
 integrity sha256
 group 2
crypto ikev2 proposal V4-PROPOSAL2 
description IKEv2 proposal for Tenant 2 
encryption aes-cbc-256
 integrity sha256
 group 2
!
crypto ikev2 policy V2-POLICY2 
description IKEv2 Policy for Tenant 1 
match fvrf Tenant 1
 match address local 10.60.3.255
 proposal V2-PROPOSAL2
description IKEv2 Policy for Tenant 2
crypto ikev2 policy V4-POLICY2 
 match fvrf Tenant 2
 match address local 10.60.3.251
 proposal V4-PROPOSAL2
!
crypto ikev2 profile V2-PROFILE
description IKEv2 profile for Tenant 1 
match fvrf Tenant 1
 match address local 10.60.3.255
 match identity remote any
 authentication remote pre-share key abc123
 authentication local pre-share key abc123
 ivrf Tenant 1
!
crypto ikev2 profile V4-PROFILE
description IKEv2 profile for Tenant 2
 match fvrf Tenant 2
 match address local 10.60.3.251
 match identity remote any
 authentication remote pre-share key abc123
 authentication local pre-share key abc123
 ivrf Tenant 2
!
crypto ipsec transform-set V2-TRANSFORM2 esp-gcm 256 
 mode tunnel
crypto ipsec transform-set V4-TRANSFORM2 esp-gcm 256 
 mode tunnel
!
crypto ipsec profile V2-PROFILE
 set transform-set V2-TRANSFORM2 
 set ikev2-profile V2-PROFILE
!
crypto ipsec profile V4-PROFILE
 set transform-set V4-TRANSFORM2 
 set ikev2-profile V4-PROFILE
!
interface Tunnel10
description S2S VPN Tunnel for Tenant 1
 ip vrf forwarding Tenant 1
 ip address 11.0.0.2 255.255.255.252
 ip tcp adjust-mss 1350
 tunnel source TenGigabitEthernet0/1/0.211
 tunnel mode ipsec ipv4
 tunnel destination 10.10.0.62
 tunnel vrf Tenant 1
 tunnel protection ipsec profile V2-PROFILE
!
interface Tunnel20
description S2S VPN Tunnel for Tenant 2
 ip vrf forwarding Tenant 2
 ip address 11.0.0.2 255.255.255.252
 ip tcp adjust-mss 1350
 tunnel source TenGigabitEthernet0/1/0.213
 tunnel mode ipsec ipv4
 tunnel destination 10.10.0.62
 tunnel vrf VNET3
 tunnel protection ipsec profile V4-PROFILE
!
interface GigabitEthernet0/0/1
 description PRIMARY Express Route Link to AZURE over Equinix
 no ip address
 negotiation auto
!
interface GigabitEthernet0/0/1.100
description Primary WAN interface of Tenant 1
 description PRIMARY ER link supporting Tenant 1 to Azure
 encapsulation dot1Q 101
 ip vrf forwarding Tenant 1
 ip address 192.168.1.1 255.255.255.252
!
interface GigabitEthernet0/0/1.102
description Primary WAN interface of Tenant 2
 description PRIMARY ER link supporting Tenant 2 to Azure
 encapsulation dot1Q 102
 ip vrf forwarding Tenant 2
 ip address 192.168.1.17 255.255.255.252
!
interface GigabitEthernet0/0/2
 description BACKUP Express Route Link to AZURE over Equinix
 no ip address
 negotiation auto
!
interface GigabitEthernet0/0/2.100
description Secondary WAN interface of Tenant 1
 description BACKUP ER link supporting Tenant 1 to Azure
 encapsulation dot1Q 101
 ip vrf forwarding Tenant 1
 ip address 192.168.1.5 255.255.255.252
!
interface GigabitEthernet0/0/2.102
description Secondary WAN interface of Tenant 2 
description BACKUP ER link supporting Tenant 2 to Azure
 encapsulation dot1Q 102
 ip vrf forwarding Tenant 2
 ip address 192.168.1.21 255.255.255.252
!
interface TenGigabitEthernet0/1/0
 description Downlink to ---Port 1/47
 no ip address
!
interface TenGigabitEthernet0/1/0.211
 description LAN interface of Tenant 1
description Downlink to --- Port 1/47.211
 encapsulation dot1Q 211
 ip vrf forwarding Tenant 1
 ip address 10.60.3.255 255.255.255.254
!
interface TenGigabitEthernet0/1/0.213
description LAN interface of Tenant 2
 description Downlink to --- Port 1/47.213
 encapsulation dot1Q 213
 ip vrf forwarding Tenant 2
 ip address 10.60.3.251 255.255.255.254
!
router bgp 65530
 bgp router-id <removed>
 bgp log-neighbor-changes
 description BGP neighbor config and route advertisement for Tenant 1 VRF 
 address-family ipv4 vrf Tenant 1
  network 10.1.0.0 mask 255.255.0.0
  network 10.60.3.254 mask 255.255.255.254
  network 192.168.1.0 mask 255.255.255.252
  network 192.168.1.4 mask 255.255.255.252
  neighbor 10.10.0.62 remote-as 65100
  neighbor 10.10.0.62 description VPN-BGP-PEER-for-Tenant 1
  neighbor 10.10.0.62 ebgp-multihop 5
  neighbor 10.10.0.62 activate
  neighbor 10.60.3.254 remote-as 4232570301
  neighbor 10.60.3.254 description LAN peer for CPEC:INET:2112 VRF
  neighbor 10.60.3.254 activate
  neighbor 10.60.3.254 route-map BLOCK-ALL out
  neighbor 192.168.1.2 remote-as 12076
  neighbor 192.168.1.2 description PRIMARY ER peer for Tenant 1 to Azure
  neighbor 192.168.1.2 ebgp-multihop 5
  neighbor 192.168.1.2 activate
  neighbor 192.168.1.2 soft-reconfiguration inbound
  neighbor 192.168.1.2 route-map Tenant 1-ONLY out
  neighbor 192.168.1.6 remote-as 12076
  neighbor 192.168.1.6 description BACKUP ER peer for Tenant 1 to Azure
  neighbor 192.168.1.6 ebgp-multihop 5
  neighbor 192.168.1.6 activate
  neighbor 192.168.1.6 soft-reconfiguration inbound
  neighbor 192.168.1.6 route-map Tenant 1-ONLY out
  maximum-paths 8
 exit-address-family
 !
description BGP neighbor config and route advertisement for Tenant 2 VRF 
address-family ipv4 vrf Tenant 2
  network 10.1.0.0 mask 255.255.0.0
  network 10.60.3.250 mask 255.255.255.254
  network 192.168.1.16 mask 255.255.255.252
  network 192.168.1.20 mask 255.255.255.252
  neighbor 10.10.0.62 remote-as 65300
  neighbor 10.10.0.62 description VPN-BGP-PEER-for-Tenant 2
  neighbor 10.10.0.62 ebgp-multihop 5
  neighbor 10.10.0.62 activate
  neighbor 10.60.3.250 remote-as 4232570301
  neighbor 10.60.3.250 description LAN peer for CPEC:INET:2112 VRF
  neighbor 10.60.3.250 activate
  neighbor 10.60.3.250 route-map BLOCK-ALL out
  neighbor 192.168.1.18 remote-as 12076
  neighbor 192.168.1.18 description PRIMARY ER peer for Tenant 2 to Azure
  neighbor 192.168.1.18 ebgp-multihop 5
  neighbor 192.168.1.18 activate
  neighbor 192.168.1.18 soft-reconfiguration inbound
  neighbor 192.168.1.18 route-map VNET-ONLY out
  neighbor 192.168.1.22 remote-as 12076
  neighbor 192.168.1.22 description BACKUP ER peer for Tenant 2 to Azure
  neighbor 192.168.1.22 ebgp-multihop 5
  neighbor 192.168.1.22 activate
  neighbor 192.168.1.22 soft-reconfiguration inbound
  neighbor 192.168.1.22 route-map VNET-ONLY out
  maximum-paths 8
 exit-address-family
!
ip forward-protocol nd
!
ip as-path access-list 1 permit ^$
ip route vrf Tenant 1 10.1.0.0 255.255.0.0 Tunnel10
ip route vrf Tenant 2 10.1.0.0 255.255.0.0 Tunnel20
!
ip prefix-list BLOCK-ALL seq 5 deny 0.0.0.0/0 le 32
!
route-map BLOCK-ALL permit 10
 match ip address prefix-list BLOCK-ALL
!
route-map VNET-ONLY permit 10
 match as-path 1
!
```

## <a name="test-the-connection"></a><span data-ttu-id="2df1b-309">測試連線</span><span class="sxs-lookup"><span data-stu-id="2df1b-309">Test the connection</span></span>

<span data-ttu-id="2df1b-310">建立站對站連線和 ExpressRoute 線路之後測試連線。</span><span class="sxs-lookup"><span data-stu-id="2df1b-310">Test your connection after establishing the Site-to-Site connection and the ExpressRoute circuit.</span></span> <span data-ttu-id="2df1b-311">這項工作很簡單。</span><span class="sxs-lookup"><span data-stu-id="2df1b-311">This task is simple.</span></span>  <span data-ttu-id="2df1b-312">登入您在 Azure VNet 中建立的其中一個虛擬機器，然後偵測您在 Azure Stack 環境中建立的虛擬機器，反之亦然。</span><span class="sxs-lookup"><span data-stu-id="2df1b-312">Log on to one of the virtual machines you created in your Azure VNet and ping the virtual machine you created in the Azure Stack environment, or vice versa.</span></span> 

<span data-ttu-id="2df1b-313">為了確定是透過站對站和 ExpressRoute 連線來傳送流量，您必須在兩端都偵測虛擬機器的固定 IP (DIP) 位址，而不是虛擬機器的 VIP 位址。</span><span class="sxs-lookup"><span data-stu-id="2df1b-313">To ensure you are sending the traffic through the Site-to-Site and ExpressRoute connections, you must ping the dedicated IP (DIP) address of the virtual machine at both ends and not the VIP address of the virtual machine.</span></span> <span data-ttu-id="2df1b-314">因此，您必須找出並記下連線另一端的位址。</span><span class="sxs-lookup"><span data-stu-id="2df1b-314">So, you must find and note the address on the other end of the connection.</span></span>

### <a name="allow-icmp-in-through-the-firewall"></a><span data-ttu-id="2df1b-315">允許 ICMP 通過防火牆</span><span class="sxs-lookup"><span data-stu-id="2df1b-315">Allow ICMP in through the firewall</span></span>
<span data-ttu-id="2df1b-316">根據預設，Windows Server 2016 不允許 ICMP 封包中通過防火牆。</span><span class="sxs-lookup"><span data-stu-id="2df1b-316">By default, Windows Server 2016 does not allow ICMP packets in through the firewall.</span></span> <span data-ttu-id="2df1b-317">因此，針對您在測試中使用的每個虛擬機器，請在提升權限的 PowerShell 視窗中執行下列 Cmdlet：</span><span class="sxs-lookup"><span data-stu-id="2df1b-317">So, for every virtual machine you use in the test, run the following cmdlet in an elevated PowerShell window:</span></span>


   ```
   New-NetFirewallRule `
    –DisplayName “Allow ICMPv4-In” `
    –Protocol ICMPv4
   ```

### <a name="ping-the-azure-stack-virtual-machine"></a><span data-ttu-id="2df1b-318">偵測 Azure Stack 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="2df1b-318">Ping the Azure Stack virtual machine</span></span>

1. <span data-ttu-id="2df1b-319">使用租用戶帳戶登入 Azure Stack 使用者入口網站。</span><span class="sxs-lookup"><span data-stu-id="2df1b-319">Sign in to the Azure Stack user portal using a tenant account.</span></span>
2. <span data-ttu-id="2df1b-320">按一下左側導覽中的 [虛擬機器]。</span><span class="sxs-lookup"><span data-stu-id="2df1b-320">Click **Virtual Machines** in the left navigation bar.</span></span>
3. <span data-ttu-id="2df1b-321">尋找並按一下您先前建立的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="2df1b-321">Find the virtual machine that you previously created and click it.</span></span>
4. <span data-ttu-id="2df1b-322">在虛擬機器的區段上，按一下 [連線]。</span><span class="sxs-lookup"><span data-stu-id="2df1b-322">On the section for the virtual machine, click **Connect**.</span></span>
5. <span data-ttu-id="2df1b-323">開啟提高權限的 PowerShell 視窗，然後輸入 **ipconfig /all**。</span><span class="sxs-lookup"><span data-stu-id="2df1b-323">Open an elevated PowerShell window, and type **ipconfig /all**.</span></span>
6. <span data-ttu-id="2df1b-324">在輸出中尋找並記下 IPv4 位址。</span><span class="sxs-lookup"><span data-stu-id="2df1b-324">Find the IPv4 Address in the output and note it.</span></span> <span data-ttu-id="2df1b-325">從 Azure VNet 中的虛擬機器偵測此位址。</span><span class="sxs-lookup"><span data-stu-id="2df1b-325">Ping this address from the virtual machine in the Azure VNet.</span></span> <span data-ttu-id="2df1b-326">在範例環境中，此位址來自 10.1.1.x/24 子網路。</span><span class="sxs-lookup"><span data-stu-id="2df1b-326">In the example environment, the address is from the 10.1.1.x/24 subnet.</span></span> <span data-ttu-id="2df1b-327">在您的環境中，此位址可能不同。</span><span class="sxs-lookup"><span data-stu-id="2df1b-327">In your environment, the address might be different.</span></span> <span data-ttu-id="2df1b-328">但應該會在您為租用戶 VNet 子網路建立的子網路內。</span><span class="sxs-lookup"><span data-stu-id="2df1b-328">However, it should be within the subnet you created for the Tenant VNet subnet.</span></span>


### <a name="view-data-transfer-statistics"></a><span data-ttu-id="2df1b-329">檢視資料轉送統計資料</span><span class="sxs-lookup"><span data-stu-id="2df1b-329">View data transfer statistics</span></span>

<span data-ttu-id="2df1b-330">如果想要知道有多少流量通過您的連線，您可以在 Azure Stack 使用者入口網站的 [連線] 區段上找到此資訊。</span><span class="sxs-lookup"><span data-stu-id="2df1b-330">If you want to know how much traffic is passing through your connection, you can find this information on the Connection section in the Azure Stack user portal.</span></span> <span data-ttu-id="2df1b-331">此資訊也很適合用來確認您剛傳送的 Ping，真的通過 VPN 和 ExpressRoute 連線。</span><span class="sxs-lookup"><span data-stu-id="2df1b-331">This information is also another good way to verify that the ping you just sent actually went through the VPN and ExpressRoute connections.</span></span>

1. <span data-ttu-id="2df1b-332">使用租用戶帳戶登入 Microsoft Azure Stack 使用者入口網站。</span><span class="sxs-lookup"><span data-stu-id="2df1b-332">Sign in to the Microsoft Azure Stack user portal using your tenant account.</span></span>
2. <span data-ttu-id="2df1b-333">瀏覽至已建立 VPN 閘道的資源群組，然後選取 [連線] 物件類型。</span><span class="sxs-lookup"><span data-stu-id="2df1b-333">Navigate to the resource group where your VPN Gateway was created and select the **Connections** object type.</span></span>
3. <span data-ttu-id="2df1b-334">按一下清單中的 [ConnectToAzure]連線。</span><span class="sxs-lookup"><span data-stu-id="2df1b-334">Click the **ConnectToAzure** connection in the list.</span></span>
4. <span data-ttu-id="2df1b-335">在 [連線] 區段上，您可以看到 [資料輸入] 和 [資料輸出] 的統計資料。您應該會看到一些非零值。</span><span class="sxs-lookup"><span data-stu-id="2df1b-335">On the **Connection** section, you can see statistics for **Data in** and **Data out**. You should see some non-zero values there.</span></span>

   ![資料輸入、資料輸出](media/azure-stack-connect-expressroute/DataInDataOut.png)

## <a name="next-steps"></a><span data-ttu-id="2df1b-337">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2df1b-337">Next steps</span></span>
[<span data-ttu-id="2df1b-338">將應用程式部署到 Azure 和 Azure Stack</span><span class="sxs-lookup"><span data-stu-id="2df1b-338">Deploy apps to Azure and Azure Stack</span></span>](azure-stack-solution-pipeline.md)