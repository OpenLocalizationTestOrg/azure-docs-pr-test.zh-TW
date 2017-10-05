---
title: "對路由進行疑難排解 - 入口網站 | Microsoft Docs"
description: "了解如何使用 Azure 入口網站對 Azure Resource Manager 部署模型中的路由進行疑難排解。"
services: virtual-network
documentationcenter: na
author: AnithaAdusumilli
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: bdd8b6dc-02fb-4057-bb23-8289caa9de89
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/23/2016
ms.author: anithaa
ms.openlocfilehash: dad415936280b4af916b8c46df46f6c51ac0bca4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-routes-using-the-azure-portal"></a><span data-ttu-id="ba0dc-103">使用 Azure 入口網站對路由進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="ba0dc-103">Troubleshoot routes using the Azure Portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ba0dc-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="ba0dc-104">Azure Portal</span></span>](virtual-network-routes-troubleshoot-portal.md)
> * [<span data-ttu-id="ba0dc-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ba0dc-105">PowerShell</span></span>](virtual-network-routes-troubleshoot-powershell.md)
>
>

<span data-ttu-id="ba0dc-106">如果您和 Azure 虛擬機器 (VM) 之間遇到網路連線問題，路由可能會影響 VM 的流量流程。</span><span class="sxs-lookup"><span data-stu-id="ba0dc-106">If you are experiencing network connectivity issues to or from your Azure Virtual Machine (VM), routes may be impacting your VM traffic flows.</span></span> <span data-ttu-id="ba0dc-107">本文提供協助診斷路由功能的概觀以進一步進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="ba0dc-107">This article provides an overview of diagnostics capabilities for routes to help troubleshoot further.</span></span>

<span data-ttu-id="ba0dc-108">路由表與子網路相關聯，在該子網路中的所有網路介面 (NIC) 上都有效。</span><span class="sxs-lookup"><span data-stu-id="ba0dc-108">Route tables are associated with subnets and are effective on all network interfaces (NIC) in that subnet.</span></span> <span data-ttu-id="ba0dc-109">下列類型的路由可以套用到每個網路介面︰</span><span class="sxs-lookup"><span data-stu-id="ba0dc-109">The following types of routes can be applied to each network interface:</span></span>

* <span data-ttu-id="ba0dc-110">**系統路由︰** 在 Azure 虛擬網路 (VNet) 中建立的每個子網路預設都有系統路由表，允許本機 VNet 流量、透過 VPN 閘道的內部部署流量以及網際網路流量。</span><span class="sxs-lookup"><span data-stu-id="ba0dc-110">**System routes:** By default, every subnet created in an Azure Virtual Network (VNet) has system route tables that allow local VNet traffic, on-premises traffic via VPN gateways, and Internet traffic.</span></span> <span data-ttu-id="ba0dc-111">對等互連的 VNet 也有系統路由。</span><span class="sxs-lookup"><span data-stu-id="ba0dc-111">System routes also exist for peered VNets.</span></span>
* <span data-ttu-id="ba0dc-112">**BGP 路由︰** 透過 ExpressRoute 或站台對站台 VPN 連線傳播到網路介面。</span><span class="sxs-lookup"><span data-stu-id="ba0dc-112">**BGP routes:** Propagated to network interfaces through ExpressRoute or site-to-site VPN connections.</span></span> <span data-ttu-id="ba0dc-113">閱讀 [BGP 與 VPN 閘道](../vpn-gateway/vpn-gateway-bgp-overview.md)和 [ExpressRoute 概觀](../expressroute/expressroute-introduction.md)文章深入了解 BGP 路由。</span><span class="sxs-lookup"><span data-stu-id="ba0dc-113">Learn more about BGP routing by reading the [BGP with VPN gateways](../vpn-gateway/vpn-gateway-bgp-overview.md) and [ExpressRoute overview](../expressroute/expressroute-introduction.md) articles.</span></span>
* <span data-ttu-id="ba0dc-114">**使用者定義路由 (UDR)：** 如果您使用網路虛擬設備或透過站台對站台 VPN 強制將流量導向內部部署網路，您可能會有與子網路路由表相關聯的使用者定義路由 (UDR)。</span><span class="sxs-lookup"><span data-stu-id="ba0dc-114">**User-defined routes (UDR):** If you are using network virtual appliances or are forced-tunneling traffic to an on-premises network via a site-to-site VPN, you may have user-defined routes (UDRs) associated with your subnet route table.</span></span> <span data-ttu-id="ba0dc-115">如果您不熟悉 UDR，請閱讀 [使用者定義路由](virtual-networks-udr-overview.md#user-defined-routes) 文章。</span><span class="sxs-lookup"><span data-stu-id="ba0dc-115">If you're not familiar with UDRs, read the [user-defined routes](virtual-networks-udr-overview.md#user-defined-routes) article.</span></span>

<span data-ttu-id="ba0dc-116">因為有各種路由可套用至網路介面，所以可能會很難判斷哪些彙總路由是有效的。</span><span class="sxs-lookup"><span data-stu-id="ba0dc-116">With the various routes that can be applied to a network interface, it can be difficult to determine which aggregate routes are effective.</span></span> <span data-ttu-id="ba0dc-117">為了協助對 VM 網路連線進行疑難排解，您可以檢視 Azure Resource Manager 部署模型中某個網路介面的所有有效路由。</span><span class="sxs-lookup"><span data-stu-id="ba0dc-117">To help troubleshoot VM network connectivity, you can view all the effective routes for a network interface in the Azure Resource Manager deployment model.</span></span>

## <a name="using-effective-routes-to-troubleshoot-vm-traffic-flow"></a><span data-ttu-id="ba0dc-118">使用有效路由對 VM 流量流程進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="ba0dc-118">Using Effective Routes to troubleshoot VM traffic flow</span></span>
<span data-ttu-id="ba0dc-119">本文使用下列案例做為範例，說明如何對網路介面的有效路由進行疑難排解︰</span><span class="sxs-lookup"><span data-stu-id="ba0dc-119">This article uses the following scenario as an example to illustrate how to troubleshoot the effective routes for a network interface:</span></span>

<span data-ttu-id="ba0dc-120">某個連接到 VNet (*VNet1*，首碼︰10.9.0.0/16) 的 VM (*VM1*) 無法連線到新對等互連的 VNet (*VNet3*，首碼 10.10.0.0/16) 中的 VM (VM3)。</span><span class="sxs-lookup"><span data-stu-id="ba0dc-120">A VM (*VM1*) connected to the VNet (*VNet1*, prefix: 10.9.0.0/16) fails to connect to a VM(VM3) in a newly peered VNet (*VNet3*, prefix 10.10.0.0/16).</span></span> <span data-ttu-id="ba0dc-121">連線到 VM 的 VM1-NIC1 網路介面沒有套用 UDR 或 BGP 路由，只有套用系統路由。</span><span class="sxs-lookup"><span data-stu-id="ba0dc-121">There are no UDRs or BGP routes applied to VM1-NIC1 network interface connected to the VM, only system routes are applied.</span></span>

<span data-ttu-id="ba0dc-122">本文說明如何使用 Azure Resource Manager 部署模型中的有效路由功能判斷連線失敗的原因。</span><span class="sxs-lookup"><span data-stu-id="ba0dc-122">This article explains how to determine the cause of the connection failure, using effective routes capability in Azure Resource Management deployment model.</span></span>
<span data-ttu-id="ba0dc-123">雖然此範例只使用系統路由，但是可以使用相同的步驟判斷透過任何路由類型的輸入和輸出連線失敗。</span><span class="sxs-lookup"><span data-stu-id="ba0dc-123">While the example uses only system routes, the same steps can be used to determine inbound and outbound connection failures over any route type.</span></span>

> [!NOTE]
> <span data-ttu-id="ba0dc-124">如果您的 VM 附加了多個 NIC，請檢查每個 NIC 的有效路由以診斷和 VM 之間的網路連線問題。</span><span class="sxs-lookup"><span data-stu-id="ba0dc-124">If your VM has more than one NIC attached, check effective routes for each of the NICs to diagnose network connectivity issues to and from a VM.</span></span>
>
>

### <a name="view-effective-routes-for-a-virtual-machine"></a><span data-ttu-id="ba0dc-125">檢視虛擬機器的有效路由</span><span class="sxs-lookup"><span data-stu-id="ba0dc-125">View effective routes for a virtual machine</span></span>
<span data-ttu-id="ba0dc-126">若要查看套用到 VM 的彙總路由，請完成下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="ba0dc-126">To see the aggregate routes that are applied to a VM, complete the following steps:</span></span>

1. <span data-ttu-id="ba0dc-127">登入 Azure 入口網站，位址是 https://portal.azure.com。</span><span class="sxs-lookup"><span data-stu-id="ba0dc-127">Login to the Azure portal at https://portal.azure.com.</span></span>
2. <span data-ttu-id="ba0dc-128">按一下 [更多服務]，然後在出現的清單中按一下 [虛擬機器]。</span><span class="sxs-lookup"><span data-stu-id="ba0dc-128">Click **More services**, then click **Virtual machines** in the list that appears.</span></span>
3. <span data-ttu-id="ba0dc-129">從出現的清單中選取要進行疑難排解的 VM，此時會出現一個有選項的 VM 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="ba0dc-129">Select a VM to troubleshoot from the list that appears and a VM blade with options appears.</span></span>
4. <span data-ttu-id="ba0dc-130">按一下 [診斷並解決問題]，然後選取常見的問題。</span><span class="sxs-lookup"><span data-stu-id="ba0dc-130">Click **Diagnose & solve problems** and then select a common problem.</span></span> <span data-ttu-id="ba0dc-131">例如選取了 [我無法連接到我的 Windows VM]  。</span><span class="sxs-lookup"><span data-stu-id="ba0dc-131">For this example, **I can’t connect to my Windows VM** is selected.</span></span>

    ![](./media/virtual-network-routes-troubleshoot-portal/image1.png)
5. <span data-ttu-id="ba0dc-132">在問題下方會出現步驟，如下圖所示︰</span><span class="sxs-lookup"><span data-stu-id="ba0dc-132">Steps appear under the problem, as shown in the following picture:</span></span>

    ![](./media/virtual-network-routes-troubleshoot-portal/image2.png)

    <span data-ttu-id="ba0dc-133">按一下建議步驟清單中的 [有效路由]  。</span><span class="sxs-lookup"><span data-stu-id="ba0dc-133">Click *effective routes* in the list of recommended steps.</span></span>
6. <span data-ttu-id="ba0dc-134">[有效路由]  刀鋒視窗隨即會出現，如下圖所示︰</span><span class="sxs-lookup"><span data-stu-id="ba0dc-134">The **Effective routes** blade appears, as shown in the following picture:</span></span>

    ![](./media/virtual-network-routes-troubleshoot-portal/image3.png)

    <span data-ttu-id="ba0dc-135">如果您的 VM 只有一個 NIC，預設會選取它。</span><span class="sxs-lookup"><span data-stu-id="ba0dc-135">If your VM has only one NIC, it is selected by default.</span></span> <span data-ttu-id="ba0dc-136">如果您有多個 NIC，請選取您想要檢視有效路由的 NIC。</span><span class="sxs-lookup"><span data-stu-id="ba0dc-136">If you have more than one NIC, select the NIC for which you want to view the effective routes.</span></span>

   > [!NOTE]
   > <span data-ttu-id="ba0dc-137">如果與 NIC 相關聯的 VM 不是處於執行中狀態，就不會顯示有效路由。</span><span class="sxs-lookup"><span data-stu-id="ba0dc-137">If the VM associated with the NIC is not in a running state, effective routes will not be shown.</span></span> <span data-ttu-id="ba0dc-138">入口網站中只會顯示前 200 個有效路由。</span><span class="sxs-lookup"><span data-stu-id="ba0dc-138">Only the first 200 effective routes are shown in the portal.</span></span> <span data-ttu-id="ba0dc-139">如需完整的清單，請按一下 [下載] 。</span><span class="sxs-lookup"><span data-stu-id="ba0dc-139">For the full list, click **Download**.</span></span> <span data-ttu-id="ba0dc-140">您可以從下載的 .csv 檔案進一步篩選結果。</span><span class="sxs-lookup"><span data-stu-id="ba0dc-140">You can further filter on the results from the downloaded .csv file.</span></span>
   >
   >

    <span data-ttu-id="ba0dc-141">請注意輸出的下列項目：</span><span class="sxs-lookup"><span data-stu-id="ba0dc-141">Notice the following in the output:</span></span>

   * <span data-ttu-id="ba0dc-142">**Source**︰表示路由的類型。</span><span class="sxs-lookup"><span data-stu-id="ba0dc-142">**Source**: Indicates the type of route.</span></span> <span data-ttu-id="ba0dc-143">系統路由會顯示為 *Default*，UDR 會顯示為 *User*，閘道路由 (靜態或 BGP) 則會顯示為 *VPNGateway*。</span><span class="sxs-lookup"><span data-stu-id="ba0dc-143">System routes are shown as *Default*, UDRs are shown as *User* and gateway routes (static or BGP) are shown as *VPNGateway*.</span></span>
   * <span data-ttu-id="ba0dc-144">**State**︰表示有效路由的狀態。</span><span class="sxs-lookup"><span data-stu-id="ba0dc-144">**State**: Indicates state of the effective route.</span></span> <span data-ttu-id="ba0dc-145">可能的值為 *Active* 或 *Invalid*。</span><span class="sxs-lookup"><span data-stu-id="ba0dc-145">Possible values are *Active* or *Invalid*.</span></span>
   * <span data-ttu-id="ba0dc-146">**AddressPrefixes**︰以 CIDR 標記法指定有效路由的位址首碼。</span><span class="sxs-lookup"><span data-stu-id="ba0dc-146">**AddressPrefixes**: Specifies the address prefix of the effective route in CIDR notation.</span></span>
   * <span data-ttu-id="ba0dc-147">**nextHopType**︰表示指定路由的下一個躍點。</span><span class="sxs-lookup"><span data-stu-id="ba0dc-147">**nextHopType**: Indicates the next hop for the given route.</span></span> <span data-ttu-id="ba0dc-148">可能的值為 *VirtualAppliance*、*Internet*、*VNetLocal*、*VNetPeering* 或 *Null*。</span><span class="sxs-lookup"><span data-stu-id="ba0dc-148">Possible values are *VirtualAppliance*, *Internet*, *VNetLocal*, *VNetPeering*, or *Null*.</span></span> <span data-ttu-id="ba0dc-149">UDR 中 *nextHopType* 的值為 **Null** 可能表示是無效路由。</span><span class="sxs-lookup"><span data-stu-id="ba0dc-149">A value of *Null* for **nextHopType** in a UDR may indicate an invalid route.</span></span> <span data-ttu-id="ba0dc-150">例如，如果 **nextHopType** 是 *VirtualAppliance* ，但是網路虛擬設備 VM 不是處於已佈建/執行中狀態。</span><span class="sxs-lookup"><span data-stu-id="ba0dc-150">For example, if **nextHopType** is *VirtualAppliance* and the network virtual appliance VM is not in a provisioned/running state.</span></span> <span data-ttu-id="ba0dc-151">如果 **nextHopType** 是 *VPNGateway* ，但是指定 VNet 中沒有任何閘道已佈建/執行中，路由可能會變成無效。</span><span class="sxs-lookup"><span data-stu-id="ba0dc-151">If **nextHopType** is *VPNGateway* and there is no gateway provisioned/running in the given VNet, the route may become invalid.</span></span>
7. <span data-ttu-id="ba0dc-152">上一個步驟的圖片中沒有列出從 *WestUS-VNet1* (首碼 10.9.0.0/16) 到 *WestUS-VNET3* VNet (首碼 10.10.0.0/16) 的路由。</span><span class="sxs-lookup"><span data-stu-id="ba0dc-152">There is no route listed to the *WestUS-VNET3* VNet (Prefix 10.10.0.0/16) from the *WestUS-VNet1* (Prefix 10.9.0.0/16) in the picture in the previous step.</span></span> <span data-ttu-id="ba0dc-153">在下圖中，對等互連連結處於 *Disconnected* 狀態︰</span><span class="sxs-lookup"><span data-stu-id="ba0dc-153">In the following picture, the peering link is in the *Disconnected* state:</span></span>

    ![](./media/virtual-network-routes-troubleshoot-portal/image4.png)

    <span data-ttu-id="ba0dc-154">對等互連的雙向連結已中斷，這說明為什麼 VM1 無法連線到 *WestUS-VNet3* VNet 中的 VM3。</span><span class="sxs-lookup"><span data-stu-id="ba0dc-154">The bi-directional link for the peering is broken, which explains why VM1 could not connect to VM3 in the *WestUS-VNet3* VNet.</span></span>
8. <span data-ttu-id="ba0dc-155">下圖顯示建立雙向對等互連連結之後的路由︰</span><span class="sxs-lookup"><span data-stu-id="ba0dc-155">The following picture shows the routes after establishing the bi-directional peering link:</span></span>

    ![](./media/virtual-network-routes-troubleshoot-portal/image5.png)

<span data-ttu-id="ba0dc-156">如需更多強制通道和路由評估的疑難排解情況，請閱讀本文的 [考量](virtual-network-routes-troubleshoot-portal.md#considerations) 一節。</span><span class="sxs-lookup"><span data-stu-id="ba0dc-156">For more troubleshooting scenarios for forced-tunneling and route evaluation, read the [Considerations](virtual-network-routes-troubleshoot-portal.md#considerations) section of this article.</span></span>

### <a name="view-effective-routes-for-a-network-interface"></a><span data-ttu-id="ba0dc-157">檢視網路介面的有效路由</span><span class="sxs-lookup"><span data-stu-id="ba0dc-157">View effective routes for a network interface</span></span>
<span data-ttu-id="ba0dc-158">如果網路流量流程受到特定網路介面 (NIC) 影響，您可以直接在 NIC 上檢視有效路由的完整清單。</span><span class="sxs-lookup"><span data-stu-id="ba0dc-158">If network traffic flow is impacted for a particular network interface (NIC), you can view a full list of effective routes on a NIC directly.</span></span> <span data-ttu-id="ba0dc-159">若要查看套用到 NIC 的彙總路由，請完成下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="ba0dc-159">To see the aggregate routes that are applied to a NIC, complete the following steps:</span></span>

1. <span data-ttu-id="ba0dc-160">登入 Azure 入口網站，位址是 https://portal.azure.com。</span><span class="sxs-lookup"><span data-stu-id="ba0dc-160">Login to the Azure portal at https://portal.azure.com.</span></span>
2. <span data-ttu-id="ba0dc-161">按一下 [更多服務]，然後按一下 [網路介面]</span><span class="sxs-lookup"><span data-stu-id="ba0dc-161">Click **More services**, then click **Network interfaces**</span></span>
3. <span data-ttu-id="ba0dc-162">搜尋清單找出 NIC 的名稱，或從出現的清單中選取。</span><span class="sxs-lookup"><span data-stu-id="ba0dc-162">Search the list for the name of a NIC, or select it from the list that appears.</span></span> <span data-ttu-id="ba0dc-163">在此範例中選取了 [VM1-NIC1]  。</span><span class="sxs-lookup"><span data-stu-id="ba0dc-163">In this example, **VM1-NIC1** is selected.</span></span>
4. <span data-ttu-id="ba0dc-164">在 [網路介面] 刀鋒視窗中選取 [有效路由]，如下圖所示︰</span><span class="sxs-lookup"><span data-stu-id="ba0dc-164">Select **Effective routes** in the **Network interface** blade, as shown in the following picture:</span></span>

       ![](./media/virtual-network-routes-troubleshoot-portal/image6.png)

    <span data-ttu-id="ba0dc-165">[範圍]  預設為選取的網路介面。</span><span class="sxs-lookup"><span data-stu-id="ba0dc-165">The **Scope** defaults to the network interface selected.</span></span>

      ![](./media/virtual-network-routes-troubleshoot-portal/image7.png)

### <a name="view-effective-routes-for-a-route-table"></a><span data-ttu-id="ba0dc-166">檢視路由表的有效路由</span><span class="sxs-lookup"><span data-stu-id="ba0dc-166">View effective routes for a route table</span></span>
<span data-ttu-id="ba0dc-167">在路由表中修改使用者定義路由 (UDR) 時，可以檢閱在特定 VM 上新增路由的影響。</span><span class="sxs-lookup"><span data-stu-id="ba0dc-167">When modifying user-defined routes (UDRs) in a route table, you may want to review the impact of the routes being added on a particular VM.</span></span> <span data-ttu-id="ba0dc-168">路由表可以與任意數目的子網路產生關聯。</span><span class="sxs-lookup"><span data-stu-id="ba0dc-168">A route table can be associated with any number of subnets.</span></span> <span data-ttu-id="ba0dc-169">您現在可以檢視套用指定路由表之所有 NIC 的所有有效路由，而不必從指定路由表刀鋒視窗切換內容。</span><span class="sxs-lookup"><span data-stu-id="ba0dc-169">You can now view all the effective routes for all the NICs that a given route table is applied to, without having to switch context from the given route table blade.</span></span>

<span data-ttu-id="ba0dc-170">在此範例中，路由表 (*UDRouteTable*) 中指定了 UDR (*UDRoute*)。</span><span class="sxs-lookup"><span data-stu-id="ba0dc-170">For this example, a UDR (*UDRoute*) is specified in a route table (*UDRouteTable*).</span></span> <span data-ttu-id="ba0dc-171">此路由會透過網路虛擬設備 (NVA) 將 *WestUS-VNet1* VNet 中來自 *Subnet1* 的所有網際網路流量傳入同一個 VNet 的 *Subnet2*。</span><span class="sxs-lookup"><span data-stu-id="ba0dc-171">This route sends all Internet traffic from *Subnet1* in the *WestUS-VNet1* VNet, through a network virtual appliance (NVA), in *Subnet2* of the same VNet.</span></span> <span data-ttu-id="ba0dc-172">路由如下圖所示：</span><span class="sxs-lookup"><span data-stu-id="ba0dc-172">The route is shown in the following picture:</span></span>

![](./media/virtual-network-routes-troubleshoot-portal/image8.png)

<span data-ttu-id="ba0dc-173">若要查看路由表的彙總路由，請完成下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="ba0dc-173">To see the aggregate routes for a route table, complete the following steps:</span></span>

1. <span data-ttu-id="ba0dc-174">登入 Azure 入口網站，位址是 https://portal.azure.com。</span><span class="sxs-lookup"><span data-stu-id="ba0dc-174">Login to the Azure portal at https://portal.azure.com.</span></span>
2. <span data-ttu-id="ba0dc-175">按一下 [更多服務]，然後按一下 [路由表]</span><span class="sxs-lookup"><span data-stu-id="ba0dc-175">Click **More services**, then click **Route tables**</span></span>
3. <span data-ttu-id="ba0dc-176">搜尋清單找出您想要查看彙總路由的路由表，然後選取它。</span><span class="sxs-lookup"><span data-stu-id="ba0dc-176">Search the list for the route table you want to see aggregate routes for and select it.</span></span> <span data-ttu-id="ba0dc-177">在此範例中選取了 **UDRouteTable** 。</span><span class="sxs-lookup"><span data-stu-id="ba0dc-177">In this example, **UDRouteTable** is selected.</span></span> <span data-ttu-id="ba0dc-178">選取路由表的刀鋒視窗會隨即出現，如下圖所示︰</span><span class="sxs-lookup"><span data-stu-id="ba0dc-178">A blade for the selected route table appears, as shown in the following picture:</span></span>

    ![](./media/virtual-network-routes-troubleshoot-portal/image9.png)
4. <span data-ttu-id="ba0dc-179">在 [路由表] 刀鋒視窗中選取 [有效路由]。</span><span class="sxs-lookup"><span data-stu-id="ba0dc-179">Select **Effective Routes** in the **Route table** blade.</span></span> <span data-ttu-id="ba0dc-180">[範圍]  會設為您所選取的路由表。</span><span class="sxs-lookup"><span data-stu-id="ba0dc-180">The **Scope** is set to the route table you selected.</span></span>
5. <span data-ttu-id="ba0dc-181">路由表可以套用到多個子網路。</span><span class="sxs-lookup"><span data-stu-id="ba0dc-181">A route table can be applied to multiple subnets.</span></span> <span data-ttu-id="ba0dc-182">從清單中選取您想要檢閱 [子網路]  。</span><span class="sxs-lookup"><span data-stu-id="ba0dc-182">Select the **Subnet** you want to review from the list.</span></span> <span data-ttu-id="ba0dc-183">在此範例中選取了 [Subnet1]  。</span><span class="sxs-lookup"><span data-stu-id="ba0dc-183">In this example, **Subnet1** is selected.</span></span>
6. <span data-ttu-id="ba0dc-184">選取 [網路介面] 。</span><span class="sxs-lookup"><span data-stu-id="ba0dc-184">Select a **Network Interface**.</span></span> <span data-ttu-id="ba0dc-185">此時會列出連線到選取子網路的所有 NIC。</span><span class="sxs-lookup"><span data-stu-id="ba0dc-185">All NICs connected to the selected subnet are listed.</span></span> <span data-ttu-id="ba0dc-186">在此範例中選取了 [VM1-NIC1]  。</span><span class="sxs-lookup"><span data-stu-id="ba0dc-186">In this example, **VM1-NIC1** is selected.</span></span>

    ![](./media/virtual-network-routes-troubleshoot-portal/image10.png)

   > [!NOTE]
   > <span data-ttu-id="ba0dc-187">如果 NIC 沒有與執行中的 VM 相關聯，則不會顯示任何有效路由。</span><span class="sxs-lookup"><span data-stu-id="ba0dc-187">If the NIC is not associated with a running VM, no effective routes are shown.</span></span>
   >
   >

## <a name="considerations"></a><span data-ttu-id="ba0dc-188">考量</span><span class="sxs-lookup"><span data-stu-id="ba0dc-188">Considerations</span></span>
<span data-ttu-id="ba0dc-189">檢閱傳回的路由清單時，請記住下列幾點事項︰</span><span class="sxs-lookup"><span data-stu-id="ba0dc-189">A few things to keep in mind when reviewing the list of routes returned:</span></span>

* <span data-ttu-id="ba0dc-190">路由是根據 UDR、BGP 和系統路由之間的最長首碼比對 (LPM)。</span><span class="sxs-lookup"><span data-stu-id="ba0dc-190">Routing is based on Longest Prefix Match (LPM) among UDRs, BGP and system routes.</span></span> <span data-ttu-id="ba0dc-191">如果有多個符合相同 LPM 的路由，則會根據其來源，以下列順序選取路由：</span><span class="sxs-lookup"><span data-stu-id="ba0dc-191">If there is more than one route with the same LPM match, then a route is selected based on its origin in the following order:</span></span>

  * <span data-ttu-id="ba0dc-192">使用者定義路由</span><span class="sxs-lookup"><span data-stu-id="ba0dc-192">User-defined route</span></span>
  * <span data-ttu-id="ba0dc-193">BGP 路由</span><span class="sxs-lookup"><span data-stu-id="ba0dc-193">BGP route</span></span>
  * <span data-ttu-id="ba0dc-194">系統 (預設) 路由</span><span class="sxs-lookup"><span data-stu-id="ba0dc-194">System (Default) route</span></span>

    <span data-ttu-id="ba0dc-195">如果有有效路由，您就只會看到根據所有可用路由符合 LPM 的有效路由。</span><span class="sxs-lookup"><span data-stu-id="ba0dc-195">With effective routes, you can only see effective routes that are LPM match based on all the availble routes.</span></span> <span data-ttu-id="ba0dc-196">透過示範如何針對指定 NIC 實際評估路由，這樣可以更方便對可能會影響 VM 連線的特定路由進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="ba0dc-196">By showing how the routes are actually evaluated for a given NIC, this makes it a lot easier to troubleshoot specific routes that may be impacting connectivity to/from your VM.</span></span>
* <span data-ttu-id="ba0dc-197">如果您有 UDR，要將流量傳送到網路虛擬設備 (NVA)，且 *VirtualAppliance* 為 **nextHopType**，請確定接收流量的 NVA 已啟用 IP 轉送，否則封包會被捨棄。</span><span class="sxs-lookup"><span data-stu-id="ba0dc-197">If you have UDRs and are sending traffic to a network virtual appliance (NVA), with *VirtualAppliance* as **nextHopType**, ensure that IP forwarding is enabled on the NVA receiving the traffic or packets are dropped.</span></span>
* <span data-ttu-id="ba0dc-198">如果已啟用強制通道，所有輸出的網際網路流量就會路由到內部部署。</span><span class="sxs-lookup"><span data-stu-id="ba0dc-198">If Forced tunneling is enabled, all outbound Internet traffic will be routed to on-premises.</span></span> <span data-ttu-id="ba0dc-199">使用此設定時，根據內部部署處理此流量的方式，從網際網路可能無法 RDP/SSH 到您的 VM。</span><span class="sxs-lookup"><span data-stu-id="ba0dc-199">RDP/SSH from Internet to your VM may not work with this setting, depending on how the on-premises handles this traffic.</span></span>
  <span data-ttu-id="ba0dc-200">符合下列其中一個條件時，可以啟用強制通道︰</span><span class="sxs-lookup"><span data-stu-id="ba0dc-200">Forced-tunneling can be enabled:</span></span>
  * <span data-ttu-id="ba0dc-201">使用站台對站台 VPN 時，將使用者定義路由 (UDR) 的 nextHopType 設定為 VPNGateway</span><span class="sxs-lookup"><span data-stu-id="ba0dc-201">If using site-to-site VPN, by setting a user-defined route (UDR) with nextHopType as VPN Gateway</span></span>
  * <span data-ttu-id="ba0dc-202">透過 BGP 公告預設路由</span><span class="sxs-lookup"><span data-stu-id="ba0dc-202">If a default route is advertised over BGP</span></span>
* <span data-ttu-id="ba0dc-203">要讓 VNet 對等互連流量正確運作，對等互連的 VNet 的首碼範圍必須有 **nextHopType** *VNetPeering* 的系統路由。</span><span class="sxs-lookup"><span data-stu-id="ba0dc-203">For VNet peering traffic to work correctly, a system route with **nextHopType** *VNetPeering* must exist for the peered VNet’s prefix range.</span></span> <span data-ttu-id="ba0dc-204">如果沒有此類路由，且 VNet 對等互連連結看起來正常︰</span><span class="sxs-lookup"><span data-stu-id="ba0dc-204">If such a route doesn’t exist and the VNet peering link looks OK:</span></span>
  * <span data-ttu-id="ba0dc-205">如果是新建立的對等互連連結，請等候幾秒鐘並重試。</span><span class="sxs-lookup"><span data-stu-id="ba0dc-205">Wait a few seconds and retry if it's a newly established peering link.</span></span> <span data-ttu-id="ba0dc-206">有時候需要花比較長的時間才能將路由傳播到子網路中的所有網路介面。</span><span class="sxs-lookup"><span data-stu-id="ba0dc-206">It occasionally takes longer to propagate routes to all the network interfaces in a subnet.</span></span>
  * <span data-ttu-id="ba0dc-207">網路安全性群組 (NSG) 規則可能會影響流量流程。</span><span class="sxs-lookup"><span data-stu-id="ba0dc-207">Network Security Group (NSG) rules may be impacting the traffic flows.</span></span> <span data-ttu-id="ba0dc-208">如需詳細資訊，請參閱 [為網路安全性群組疑難排解](virtual-network-nsg-troubleshoot-portal.md) 文章。</span><span class="sxs-lookup"><span data-stu-id="ba0dc-208">For more information, see the [Troubleshoot Network Security Groups](virtual-network-nsg-troubleshoot-portal.md) article.</span></span>
