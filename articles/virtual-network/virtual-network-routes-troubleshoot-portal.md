---
title: "aaaTroubleshoot 路由-入口網站 |Microsoft 文件"
description: "了解如何在 hello Azure Resource Manager 部署模型使用 tootroubleshoot 路由 hello Azure 入口網站。"
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
ms.openlocfilehash: 579bae91ef3200852032b3953d3cc5d26deada86
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-routes-using-hello-azure-portal"></a><span data-ttu-id="ee402-103">疑難排解使用 hello Azure 入口網站的路由</span><span class="sxs-lookup"><span data-stu-id="ee402-103">Troubleshoot routes using hello Azure Portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ee402-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="ee402-104">Azure Portal</span></span>](virtual-network-routes-troubleshoot-portal.md)
> * [<span data-ttu-id="ee402-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ee402-105">PowerShell</span></span>](virtual-network-routes-troubleshoot-powershell.md)
>
>

<span data-ttu-id="ee402-106">如果您遇到網路連線問題 tooor 您 Azure 虛擬機器 (VM)，路由可能影響您 VM 的流量。</span><span class="sxs-lookup"><span data-stu-id="ee402-106">If you are experiencing network connectivity issues tooor from your Azure Virtual Machine (VM), routes may be impacting your VM traffic flows.</span></span> <span data-ttu-id="ee402-107">本文章提供的路由 toohelp 進一步的疑難排解的診斷功能的概觀。</span><span class="sxs-lookup"><span data-stu-id="ee402-107">This article provides an overview of diagnostics capabilities for routes toohelp troubleshoot further.</span></span>

<span data-ttu-id="ee402-108">路由表與子網路相關聯，在該子網路中的所有網路介面 (NIC) 上都有效。</span><span class="sxs-lookup"><span data-stu-id="ee402-108">Route tables are associated with subnets and are effective on all network interfaces (NIC) in that subnet.</span></span> <span data-ttu-id="ee402-109">hello 下列類型的路由可以是套用的 tooeach 網路介面：</span><span class="sxs-lookup"><span data-stu-id="ee402-109">hello following types of routes can be applied tooeach network interface:</span></span>

* <span data-ttu-id="ee402-110">**系統路由︰** 在 Azure 虛擬網路 (VNet) 中建立的每個子網路預設都有系統路由表，允許本機 VNet 流量、透過 VPN 閘道的內部部署流量以及網際網路流量。</span><span class="sxs-lookup"><span data-stu-id="ee402-110">**System routes:** By default, every subnet created in an Azure Virtual Network (VNet) has system route tables that allow local VNet traffic, on-premises traffic via VPN gateways, and Internet traffic.</span></span> <span data-ttu-id="ee402-111">對等互連的 VNet 也有系統路由。</span><span class="sxs-lookup"><span data-stu-id="ee402-111">System routes also exist for peered VNets.</span></span>
* <span data-ttu-id="ee402-112">**BGP 路由：**傳播 toonetwork 介面透過 ExpressRoute 或站台對站 VPN 連線。</span><span class="sxs-lookup"><span data-stu-id="ee402-112">**BGP routes:** Propagated toonetwork interfaces through ExpressRoute or site-to-site VPN connections.</span></span> <span data-ttu-id="ee402-113">深入了解 BGP 路由閱讀 hello[與 VPN 閘道的 BGP](../vpn-gateway/vpn-gateway-bgp-overview.md)和[ExpressRoute 概觀](../expressroute/expressroute-introduction.md)文件。</span><span class="sxs-lookup"><span data-stu-id="ee402-113">Learn more about BGP routing by reading hello [BGP with VPN gateways](../vpn-gateway/vpn-gateway-bgp-overview.md) and [ExpressRoute overview](../expressroute/expressroute-introduction.md) articles.</span></span>
* <span data-ttu-id="ee402-114">**使用者定義的路由 (UDR):**如果您使用網路虛擬裝置，或會強制通道流量 tooan 透過站對站 VPN 的內部部署網路，您可能需要使用者定義的路由 (UDRs) 與子網路路由表相關聯。</span><span class="sxs-lookup"><span data-stu-id="ee402-114">**User-defined routes (UDR):** If you are using network virtual appliances or are forced-tunneling traffic tooan on-premises network via a site-to-site VPN, you may have user-defined routes (UDRs) associated with your subnet route table.</span></span> <span data-ttu-id="ee402-115">如果您不熟悉 UDRs，讀取 hello[使用者定義的路由](virtual-networks-udr-overview.md#user-defined-routes)發行項。</span><span class="sxs-lookup"><span data-stu-id="ee402-115">If you're not familiar with UDRs, read hello [user-defined routes](virtual-networks-udr-overview.md#user-defined-routes) article.</span></span>

<span data-ttu-id="ee402-116">以 hello 各種路由可以是套用的 tooa 網路介面，它可以是難以 toodetermine 為有效的彙總的路由。</span><span class="sxs-lookup"><span data-stu-id="ee402-116">With hello various routes that can be applied tooa network interface, it can be difficult toodetermine which aggregate routes are effective.</span></span> <span data-ttu-id="ee402-117">toohelp VM 網路連線問題疑難排解，您可以檢視所有的 hello 有效路由的網路介面在 hello Azure Resource Manager 部署模型。</span><span class="sxs-lookup"><span data-stu-id="ee402-117">toohelp troubleshoot VM network connectivity, you can view all hello effective routes for a network interface in hello Azure Resource Manager deployment model.</span></span>

## <a name="using-effective-routes-tootroubleshoot-vm-traffic-flow"></a><span data-ttu-id="ee402-118">使用有效路由 tootroubleshoot VM 流量</span><span class="sxs-lookup"><span data-stu-id="ee402-118">Using Effective Routes tootroubleshoot VM traffic flow</span></span>
<span data-ttu-id="ee402-119">本文使用 hello tootroubleshoot hello 有效會路由傳送網路介面的範例 tooillustrate 為下列案例：</span><span class="sxs-lookup"><span data-stu-id="ee402-119">This article uses hello following scenario as an example tooillustrate how tootroubleshoot hello effective routes for a network interface:</span></span>

<span data-ttu-id="ee402-120">VM (*VM1*) 連接 toohello VNet (*VNet1*，前置詞： 10.9.0.0/16) 失敗 tooconnect tooa VM(VM3) 新 peered VNet 中 (*VNet3*，前置詞 10.10.0.0/16)。</span><span class="sxs-lookup"><span data-stu-id="ee402-120">A VM (*VM1*) connected toohello VNet (*VNet1*, prefix: 10.9.0.0/16) fails tooconnect tooa VM(VM3) in a newly peered VNet (*VNet3*, prefix 10.10.0.0/16).</span></span> <span data-ttu-id="ee402-121">有沒有 UDRs 或 BGP 路由套用的 tooVM1 NIC1 網路連線介面 toohello VM，只有系統路由會套用。</span><span class="sxs-lookup"><span data-stu-id="ee402-121">There are no UDRs or BGP routes applied tooVM1-NIC1 network interface connected toohello VM, only system routes are applied.</span></span>

<span data-ttu-id="ee402-122">本文說明如何 toodetermine hello 原因 hello 連線失敗，使用 Azure 資源管理部署模型中的有效路由的功能。</span><span class="sxs-lookup"><span data-stu-id="ee402-122">This article explains how toodetermine hello cause of hello connection failure, using effective routes capability in Azure Resource Management deployment model.</span></span>
<span data-ttu-id="ee402-123">雖然 hello 範例會使用只有系統路由，hello 相同的步驟可以使用的 toodetermine 透過任何路由類型是傳入和傳出的連線失敗。</span><span class="sxs-lookup"><span data-stu-id="ee402-123">While hello example uses only system routes, hello same steps can be used toodetermine inbound and outbound connection failures over any route type.</span></span>

> [!NOTE]
> <span data-ttu-id="ee402-124">如果您的 VM 有連結的多個 NIC，請針對每個 hello Nic toodiagnose 網路連線問題 tooand 從 VM 檢查有效的路由。</span><span class="sxs-lookup"><span data-stu-id="ee402-124">If your VM has more than one NIC attached, check effective routes for each of hello NICs toodiagnose network connectivity issues tooand from a VM.</span></span>
>
>

### <a name="view-effective-routes-for-a-virtual-machine"></a><span data-ttu-id="ee402-125">檢視虛擬機器的有效路由</span><span class="sxs-lookup"><span data-stu-id="ee402-125">View effective routes for a virtual machine</span></span>
<span data-ttu-id="ee402-126">toosee hello 彙總路由的套用的 tooa VM，完成下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="ee402-126">toosee hello aggregate routes that are applied tooa VM, complete hello following steps:</span></span>

1. <span data-ttu-id="ee402-127">登入 toohello https://portal.azure.com 在 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="ee402-127">Login toohello Azure portal at https://portal.azure.com.</span></span>
2. <span data-ttu-id="ee402-128">按一下**更多服務**，然後按一下 **虛擬機器**hello 的清單中，會出現。</span><span class="sxs-lookup"><span data-stu-id="ee402-128">Click **More services**, then click **Virtual machines** in hello list that appears.</span></span>
3. <span data-ttu-id="ee402-129">從出現的 hello 清單中選取 VM tootroubleshoot 和選項的 VM 刀鋒視窗隨即出現。</span><span class="sxs-lookup"><span data-stu-id="ee402-129">Select a VM tootroubleshoot from hello list that appears and a VM blade with options appears.</span></span>
4. <span data-ttu-id="ee402-130">按一下 [診斷並解決問題]，然後選取常見的問題。</span><span class="sxs-lookup"><span data-stu-id="ee402-130">Click **Diagnose & solve problems** and then select a common problem.</span></span> <span data-ttu-id="ee402-131">例如，**我無法連線 toomy Windows VM**已選取。</span><span class="sxs-lookup"><span data-stu-id="ee402-131">For this example, **I can’t connect toomy Windows VM** is selected.</span></span>

    ![](./media/virtual-network-routes-troubleshoot-portal/image1.png)
5. <span data-ttu-id="ee402-132">Hello 下列圖片所示步驟就會出現在 hello 問題：</span><span class="sxs-lookup"><span data-stu-id="ee402-132">Steps appear under hello problem, as shown in hello following picture:</span></span>

    ![](./media/virtual-network-routes-troubleshoot-portal/image2.png)

    <span data-ttu-id="ee402-133">按一下*有效路由*在 hello 清單中的建議步驟。</span><span class="sxs-lookup"><span data-stu-id="ee402-133">Click *effective routes* in hello list of recommended steps.</span></span>
6. <span data-ttu-id="ee402-134">hello**有效路由**刀鋒視窗隨即出現，如 hello 下列圖片所示：</span><span class="sxs-lookup"><span data-stu-id="ee402-134">hello **Effective routes** blade appears, as shown in hello following picture:</span></span>

    ![](./media/virtual-network-routes-troubleshoot-portal/image3.png)

    <span data-ttu-id="ee402-135">如果您的 VM 只有一個 NIC，預設會選取它。</span><span class="sxs-lookup"><span data-stu-id="ee402-135">If your VM has only one NIC, it is selected by default.</span></span> <span data-ttu-id="ee402-136">如果您有多個 NIC，選取您想要的 tooview hello 有效路由的 hello NIC。</span><span class="sxs-lookup"><span data-stu-id="ee402-136">If you have more than one NIC, select hello NIC for which you want tooview hello effective routes.</span></span>

   > [!NOTE]
   > <span data-ttu-id="ee402-137">如果 hello VM 相關聯 hello NIC 不是處於執行中狀態，將不會顯示有效的路由。</span><span class="sxs-lookup"><span data-stu-id="ee402-137">If hello VM associated with hello NIC is not in a running state, effective routes will not be shown.</span></span> <span data-ttu-id="ee402-138">只有 hello 前 200 個有效的路由中會顯示 hello 入口網站。</span><span class="sxs-lookup"><span data-stu-id="ee402-138">Only hello first 200 effective routes are shown in hello portal.</span></span> <span data-ttu-id="ee402-139">Hello 完整清單，請按一下**下載**。</span><span class="sxs-lookup"><span data-stu-id="ee402-139">For hello full list, click **Download**.</span></span> <span data-ttu-id="ee402-140">您可以進一步篩選 hello 結果從 hello 下載的.csv 檔案。</span><span class="sxs-lookup"><span data-stu-id="ee402-140">You can further filter on hello results from hello downloaded .csv file.</span></span>
   >
   >

    <span data-ttu-id="ee402-141">請注意 hello 輸出中的 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="ee402-141">Notice hello following in hello output:</span></span>

   * <span data-ttu-id="ee402-142">**來源**： 指出 hello 路由類型。</span><span class="sxs-lookup"><span data-stu-id="ee402-142">**Source**: Indicates hello type of route.</span></span> <span data-ttu-id="ee402-143">系統路由會顯示為 *Default*，UDR 會顯示為 *User*，閘道路由 (靜態或 BGP) 則會顯示為 *VPNGateway*。</span><span class="sxs-lookup"><span data-stu-id="ee402-143">System routes are shown as *Default*, UDRs are shown as *User* and gateway routes (static or BGP) are shown as *VPNGateway*.</span></span>
   * <span data-ttu-id="ee402-144">**狀態**： 表示 hello 有效路由的狀態。</span><span class="sxs-lookup"><span data-stu-id="ee402-144">**State**: Indicates state of hello effective route.</span></span> <span data-ttu-id="ee402-145">可能的值為 *Active* 或 *Invalid*。</span><span class="sxs-lookup"><span data-stu-id="ee402-145">Possible values are *Active* or *Invalid*.</span></span>
   * <span data-ttu-id="ee402-146">**AddressPrefixes**： 以 CIDR 標記法指定有效路由的 hello hello 位址前置詞。</span><span class="sxs-lookup"><span data-stu-id="ee402-146">**AddressPrefixes**: Specifies hello address prefix of hello effective route in CIDR notation.</span></span>
   * <span data-ttu-id="ee402-147">**nextHopType**： 指出 hello hello 指定路由的下一個躍點。</span><span class="sxs-lookup"><span data-stu-id="ee402-147">**nextHopType**: Indicates hello next hop for hello given route.</span></span> <span data-ttu-id="ee402-148">可能的值為 *VirtualAppliance*、*Internet*、*VNetLocal*、*VNetPeering* 或 *Null*。</span><span class="sxs-lookup"><span data-stu-id="ee402-148">Possible values are *VirtualAppliance*, *Internet*, *VNetLocal*, *VNetPeering*, or *Null*.</span></span> <span data-ttu-id="ee402-149">UDR 中 *nextHopType* 的值為 **Null** 可能表示是無效路由。</span><span class="sxs-lookup"><span data-stu-id="ee402-149">A value of *Null* for **nextHopType** in a UDR may indicate an invalid route.</span></span> <span data-ttu-id="ee402-150">例如，如果**nextHopType**是*VirtualAppliance*與 hello 網路虛擬設備 VM 並未處於執行佈建狀態。</span><span class="sxs-lookup"><span data-stu-id="ee402-150">For example, if **nextHopType** is *VirtualAppliance* and hello network virtual appliance VM is not in a provisioned/running state.</span></span> <span data-ttu-id="ee402-151">如果**nextHopType**是*VPNGateway*且沒有任何閘道佈建/執行中指定的 VNet 的 hello，hello 路由可能會變成無效。</span><span class="sxs-lookup"><span data-stu-id="ee402-151">If **nextHopType** is *VPNGateway* and there is no gateway provisioned/running in hello given VNet, hello route may become invalid.</span></span>
7. <span data-ttu-id="ee402-152">沒有任何所列的路由 toohello *Uswest VNET3* VNet (前置詞 10.10.0.0/16) 與 hello *Uswest VNet1* （首碼 10.9.0.0/16） hello 上一個步驟中的 hello 圖片中。</span><span class="sxs-lookup"><span data-stu-id="ee402-152">There is no route listed toohello *WestUS-VNET3* VNet (Prefix 10.10.0.0/16) from hello *WestUS-VNet1* (Prefix 10.9.0.0/16) in hello picture in hello previous step.</span></span> <span data-ttu-id="ee402-153">在下列圖片 hello，hello 對等互連連結將處於 hello *Disconnected*狀態：</span><span class="sxs-lookup"><span data-stu-id="ee402-153">In hello following picture, hello peering link is in hello *Disconnected* state:</span></span>

    ![](./media/virtual-network-routes-troubleshoot-portal/image4.png)

    <span data-ttu-id="ee402-154">hello 雙向連結的 hello 對等互連已損毀，其中說明為什麼 VM1 無法連接在 hello tooVM3 *Uswest VNet3* VNet。</span><span class="sxs-lookup"><span data-stu-id="ee402-154">hello bi-directional link for hello peering is broken, which explains why VM1 could not connect tooVM3 in hello *WestUS-VNet3* VNet.</span></span>
8. <span data-ttu-id="ee402-155">hello 下圖顯示 hello 路由之後建立 hello 雙向對等互連連結：</span><span class="sxs-lookup"><span data-stu-id="ee402-155">hello following picture shows hello routes after establishing hello bi-directional peering link:</span></span>

    ![](./media/virtual-network-routes-troubleshoot-portal/image5.png)

<span data-ttu-id="ee402-156">強制通道和路由評估更多疑難排解的情況下，讀取 hello[考量](virtual-network-routes-troubleshoot-portal.md#considerations)本文一節。</span><span class="sxs-lookup"><span data-stu-id="ee402-156">For more troubleshooting scenarios for forced-tunneling and route evaluation, read hello [Considerations](virtual-network-routes-troubleshoot-portal.md#considerations) section of this article.</span></span>

### <a name="view-effective-routes-for-a-network-interface"></a><span data-ttu-id="ee402-157">檢視網路介面的有效路由</span><span class="sxs-lookup"><span data-stu-id="ee402-157">View effective routes for a network interface</span></span>
<span data-ttu-id="ee402-158">如果網路流量流程受到特定網路介面 (NIC) 影響，您可以直接在 NIC 上檢視有效路由的完整清單。</span><span class="sxs-lookup"><span data-stu-id="ee402-158">If network traffic flow is impacted for a particular network interface (NIC), you can view a full list of effective routes on a NIC directly.</span></span> <span data-ttu-id="ee402-159">toosee hello 彙總路由的套用的 tooa NIC，完成下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="ee402-159">toosee hello aggregate routes that are applied tooa NIC, complete hello following steps:</span></span>

1. <span data-ttu-id="ee402-160">登入 toohello https://portal.azure.com 在 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="ee402-160">Login toohello Azure portal at https://portal.azure.com.</span></span>
2. <span data-ttu-id="ee402-161">按一下 [更多服務]，然後按一下 [網路介面]</span><span class="sxs-lookup"><span data-stu-id="ee402-161">Click **More services**, then click **Network interfaces**</span></span>
3. <span data-ttu-id="ee402-162">Hello NIC，hello 名稱清單中搜尋，或從出現的 hello 清單中選取。</span><span class="sxs-lookup"><span data-stu-id="ee402-162">Search hello list for hello name of a NIC, or select it from hello list that appears.</span></span> <span data-ttu-id="ee402-163">在此範例中選取了 [VM1-NIC1]  。</span><span class="sxs-lookup"><span data-stu-id="ee402-163">In this example, **VM1-NIC1** is selected.</span></span>
4. <span data-ttu-id="ee402-164">選取**有效路由**在 hello**網路介面**刀鋒視窗中，hello 下列圖片所示：</span><span class="sxs-lookup"><span data-stu-id="ee402-164">Select **Effective routes** in hello **Network interface** blade, as shown in hello following picture:</span></span>

       ![](./media/virtual-network-routes-troubleshoot-portal/image6.png)

    <span data-ttu-id="ee402-165">hello**範圍**選取預設值 toohello 網路介面。</span><span class="sxs-lookup"><span data-stu-id="ee402-165">hello **Scope** defaults toohello network interface selected.</span></span>

      ![](./media/virtual-network-routes-troubleshoot-portal/image7.png)

### <a name="view-effective-routes-for-a-route-table"></a><span data-ttu-id="ee402-166">檢視路由表的有效路由</span><span class="sxs-lookup"><span data-stu-id="ee402-166">View effective routes for a route table</span></span>
<span data-ttu-id="ee402-167">當路由表中修改使用者定義的路由 (UDRs)，您可能想 tooreview hello 影響的特定 VM 上的 hello 路由。</span><span class="sxs-lookup"><span data-stu-id="ee402-167">When modifying user-defined routes (UDRs) in a route table, you may want tooreview hello impact of hello routes being added on a particular VM.</span></span> <span data-ttu-id="ee402-168">路由表可以與任意數目的子網路產生關聯。</span><span class="sxs-lookup"><span data-stu-id="ee402-168">A route table can be associated with any number of subnets.</span></span> <span data-ttu-id="ee402-169">您現在可以檢視所有 hello 有效路由，針對所有 hello Nic 套用指定的路由表，而不需要從指定的路由表刀鋒視窗中的 hello tooswitch 內容。</span><span class="sxs-lookup"><span data-stu-id="ee402-169">You can now view all hello effective routes for all hello NICs that a given route table is applied to, without having tooswitch context from hello given route table blade.</span></span>

<span data-ttu-id="ee402-170">在此範例中，路由表 (*UDRouteTable*) 中指定了 UDR (*UDRoute*)。</span><span class="sxs-lookup"><span data-stu-id="ee402-170">For this example, a UDR (*UDRoute*) is specified in a route table (*UDRouteTable*).</span></span> <span data-ttu-id="ee402-171">此路由傳送來自的所有網際網路流量*Subnet1*在 hello *Uswest VNet1* VNet，透過網路的虛擬設備 (NVA)，在*Subnet2*的 hello 相同的 VNet。</span><span class="sxs-lookup"><span data-stu-id="ee402-171">This route sends all Internet traffic from *Subnet1* in hello *WestUS-VNet1* VNet, through a network virtual appliance (NVA), in *Subnet2* of hello same VNet.</span></span> <span data-ttu-id="ee402-172">hello 路由以 hello 下列圖片所示：</span><span class="sxs-lookup"><span data-stu-id="ee402-172">hello route is shown in hello following picture:</span></span>

![](./media/virtual-network-routes-troubleshoot-portal/image8.png)

<span data-ttu-id="ee402-173">toosee hello 彙總的路由的路由表，完成下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="ee402-173">toosee hello aggregate routes for a route table, complete hello following steps:</span></span>

1. <span data-ttu-id="ee402-174">登入 toohello https://portal.azure.com 在 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="ee402-174">Login toohello Azure portal at https://portal.azure.com.</span></span>
2. <span data-ttu-id="ee402-175">按一下 [更多服務]，然後按一下 [路由表]</span><span class="sxs-lookup"><span data-stu-id="ee402-175">Click **More services**, then click **Route tables**</span></span>
3. <span data-ttu-id="ee402-176">Hello 路由表的搜尋 hello 清單想 toosee 彙總的路由並加以選取。</span><span class="sxs-lookup"><span data-stu-id="ee402-176">Search hello list for hello route table you want toosee aggregate routes for and select it.</span></span> <span data-ttu-id="ee402-177">在此範例中選取了 **UDRouteTable** 。</span><span class="sxs-lookup"><span data-stu-id="ee402-177">In this example, **UDRouteTable** is selected.</span></span> <span data-ttu-id="ee402-178">選取的 hello 路由表的刀鋒視窗隨即出現，hello 下列圖片所示：</span><span class="sxs-lookup"><span data-stu-id="ee402-178">A blade for hello selected route table appears, as shown in hello following picture:</span></span>

    ![](./media/virtual-network-routes-troubleshoot-portal/image9.png)
4. <span data-ttu-id="ee402-179">選取**有效路由**在 hello**路由表**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="ee402-179">Select **Effective Routes** in hello **Route table** blade.</span></span> <span data-ttu-id="ee402-180">hello**範圍**設定 toohello 您選取的路由表。</span><span class="sxs-lookup"><span data-stu-id="ee402-180">hello **Scope** is set toohello route table you selected.</span></span>
5. <span data-ttu-id="ee402-181">路由表可以套用的 toomultiple 子網路。</span><span class="sxs-lookup"><span data-stu-id="ee402-181">A route table can be applied toomultiple subnets.</span></span> <span data-ttu-id="ee402-182">選取 hello**子網路**想 tooreview 從 hello 清單。</span><span class="sxs-lookup"><span data-stu-id="ee402-182">Select hello **Subnet** you want tooreview from hello list.</span></span> <span data-ttu-id="ee402-183">在此範例中選取了 [Subnet1]  。</span><span class="sxs-lookup"><span data-stu-id="ee402-183">In this example, **Subnet1** is selected.</span></span>
6. <span data-ttu-id="ee402-184">選取 [網路介面] 。</span><span class="sxs-lookup"><span data-stu-id="ee402-184">Select a **Network Interface**.</span></span> <span data-ttu-id="ee402-185">列出所有 Nic 已連線的 toohello 選取子網路。</span><span class="sxs-lookup"><span data-stu-id="ee402-185">All NICs connected toohello selected subnet are listed.</span></span> <span data-ttu-id="ee402-186">在此範例中選取了 [VM1-NIC1]  。</span><span class="sxs-lookup"><span data-stu-id="ee402-186">In this example, **VM1-NIC1** is selected.</span></span>

    ![](./media/virtual-network-routes-troubleshoot-portal/image10.png)

   > [!NOTE]
   > <span data-ttu-id="ee402-187">如果不與執行中的 VM 關聯 hello NIC，則會顯示沒有有效的路由。</span><span class="sxs-lookup"><span data-stu-id="ee402-187">If hello NIC is not associated with a running VM, no effective routes are shown.</span></span>
   >
   >

## <a name="considerations"></a><span data-ttu-id="ee402-188">考量</span><span class="sxs-lookup"><span data-stu-id="ee402-188">Considerations</span></span>
<span data-ttu-id="ee402-189">檢閱 hello 的路由清單時，請注意幾件事 tookeep 傳回：</span><span class="sxs-lookup"><span data-stu-id="ee402-189">A few things tookeep in mind when reviewing hello list of routes returned:</span></span>

* <span data-ttu-id="ee402-190">路由是根據 UDR、BGP 和系統路由之間的最長首碼比對 (LPM)。</span><span class="sxs-lookup"><span data-stu-id="ee402-190">Routing is based on Longest Prefix Match (LPM) among UDRs, BGP and system routes.</span></span> <span data-ttu-id="ee402-191">如果有多個路由 hello 相同 LPM 相符，然後根據 hello 順序的源頭選取路由：</span><span class="sxs-lookup"><span data-stu-id="ee402-191">If there is more than one route with hello same LPM match, then a route is selected based on its origin in hello following order:</span></span>

  * <span data-ttu-id="ee402-192">使用者定義路由</span><span class="sxs-lookup"><span data-stu-id="ee402-192">User-defined route</span></span>
  * <span data-ttu-id="ee402-193">BGP 路由</span><span class="sxs-lookup"><span data-stu-id="ee402-193">BGP route</span></span>
  * <span data-ttu-id="ee402-194">系統 (預設) 路由</span><span class="sxs-lookup"><span data-stu-id="ee402-194">System (Default) route</span></span>

    <span data-ttu-id="ee402-195">使用有效的路由，您只能看到有效路由的 LPM 根據所有 hello 了路由的相符項目。</span><span class="sxs-lookup"><span data-stu-id="ee402-195">With effective routes, you can only see effective routes that are LPM match based on all hello availble routes.</span></span> <span data-ttu-id="ee402-196">顯示 hello 路由以給定的 nic 如何評估，這讓您輕鬆 tootroubleshoot 特定路由且可能影響從您的 VM 的連線。</span><span class="sxs-lookup"><span data-stu-id="ee402-196">By showing how hello routes are actually evaluated for a given NIC, this makes it a lot easier tootroubleshoot specific routes that may be impacting connectivity to/from your VM.</span></span>
* <span data-ttu-id="ee402-197">如果您有 UDRs 並傳送流量 tooa 網路的虛擬設備 (NVA)，與*VirtualAppliance*為**nextHopType**，確定已啟用 IP 轉送 hello NVA 接收 hello 流量或捨棄的封包。</span><span class="sxs-lookup"><span data-stu-id="ee402-197">If you have UDRs and are sending traffic tooa network virtual appliance (NVA), with *VirtualAppliance* as **nextHopType**, ensure that IP forwarding is enabled on hello NVA receiving hello traffic or packets are dropped.</span></span>
* <span data-ttu-id="ee402-198">如果已啟用強制通道，所有傳出網際網路流量會路由的 tooon 內部。</span><span class="sxs-lookup"><span data-stu-id="ee402-198">If Forced tunneling is enabled, all outbound Internet traffic will be routed tooon-premises.</span></span> <span data-ttu-id="ee402-199">RDP/SSH 從網際網路 tooyour VM 可能不適用於此設定，根據如何 hello 內部處理這個流量。</span><span class="sxs-lookup"><span data-stu-id="ee402-199">RDP/SSH from Internet tooyour VM may not work with this setting, depending on how hello on-premises handles this traffic.</span></span>
  <span data-ttu-id="ee402-200">符合下列其中一個條件時，可以啟用強制通道︰</span><span class="sxs-lookup"><span data-stu-id="ee402-200">Forced-tunneling can be enabled:</span></span>
  * <span data-ttu-id="ee402-201">使用站台對站台 VPN 時，將使用者定義路由 (UDR) 的 nextHopType 設定為 VPNGateway</span><span class="sxs-lookup"><span data-stu-id="ee402-201">If using site-to-site VPN, by setting a user-defined route (UDR) with nextHopType as VPN Gateway</span></span>
  * <span data-ttu-id="ee402-202">透過 BGP 公告預設路由</span><span class="sxs-lookup"><span data-stu-id="ee402-202">If a default route is advertised over BGP</span></span>
* <span data-ttu-id="ee402-203">Vnet 對等互連流量 toowork 正確的系統路由**nextHopType** *VNetPeering*的 hello 所以 VNet 的前置詞的範圍必須存在。</span><span class="sxs-lookup"><span data-stu-id="ee402-203">For VNet peering traffic toowork correctly, a system route with **nextHopType** *VNetPeering* must exist for hello peered VNet’s prefix range.</span></span> <span data-ttu-id="ee402-204">如果這類的路由不存在，而且 hello 對等互連的 VNet 連結正確無誤：</span><span class="sxs-lookup"><span data-stu-id="ee402-204">If such a route doesn’t exist and hello VNet peering link looks OK:</span></span>
  * <span data-ttu-id="ee402-205">如果是新建立的對等互連連結，請等候幾秒鐘並重試。</span><span class="sxs-lookup"><span data-stu-id="ee402-205">Wait a few seconds and retry if it's a newly established peering link.</span></span> <span data-ttu-id="ee402-206">它有時會接受路途 toopropagate tooall hello 網路介面的子網路。</span><span class="sxs-lookup"><span data-stu-id="ee402-206">It occasionally takes longer toopropagate routes tooall hello network interfaces in a subnet.</span></span>
  * <span data-ttu-id="ee402-207">Hello 流量可能影響網路安全性群組 (NSG) 規則。</span><span class="sxs-lookup"><span data-stu-id="ee402-207">Network Security Group (NSG) rules may be impacting hello traffic flows.</span></span> <span data-ttu-id="ee402-208">如需詳細資訊，請參閱 hello[疑難排解網路安全性群組](virtual-network-nsg-troubleshoot-portal.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="ee402-208">For more information, see hello [Troubleshoot Network Security Groups](virtual-network-nsg-troubleshoot-portal.md) article.</span></span>
