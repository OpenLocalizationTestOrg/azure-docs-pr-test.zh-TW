---
title: "aaaTroubleshoot 路由-PowerShell |Microsoft 文件"
description: "了解 tootroubleshoot 會路由傳送嗨使用 Azure PowerShell 的 Azure Resource Manager 部署模型中。"
services: virtual-network
documentationcenter: na
author: AnithaAdusumilli
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: bf7dc5e7-9399-460e-8e0d-8992dbed98a6
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/23/2016
ms.author: anithaa
ms.openlocfilehash: 7a07806df5c1d0caee921187e6ad29f6755ab535
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-routes-using-azure-powershell"></a><span data-ttu-id="7557f-103">使用 Azure PowerShell 對路由進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="7557f-103">Troubleshoot routes using Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7557f-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="7557f-104">Azure Portal</span></span>](virtual-network-routes-troubleshoot-portal.md)
> * [<span data-ttu-id="7557f-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7557f-105">PowerShell</span></span>](virtual-network-routes-troubleshoot-powershell.md)
> 
> 

<span data-ttu-id="7557f-106">如果您遇到網路連線問題 tooor 您 Azure 虛擬機器 (VM)，路由可能影響您 VM 的流量。</span><span class="sxs-lookup"><span data-stu-id="7557f-106">If you are experiencing network connectivity issues tooor from your Azure Virtual Machine (VM), routes may be impacting your VM traffic flows.</span></span> <span data-ttu-id="7557f-107">本文章提供的路由 toohelp 進一步的疑難排解的診斷功能的概觀。</span><span class="sxs-lookup"><span data-stu-id="7557f-107">This article provides an overview of diagnostics capabilities for routes toohelp troubleshoot further.</span></span>

<span data-ttu-id="7557f-108">路由表與子網路相關聯，在該子網路中的所有網路介面 (NIC) 上都有效。</span><span class="sxs-lookup"><span data-stu-id="7557f-108">Route tables are associated with subnets and are effective on all network interfaces (NIC) in that subnet.</span></span> <span data-ttu-id="7557f-109">hello 下列類型的路由可以是套用的 tooeach 網路介面：</span><span class="sxs-lookup"><span data-stu-id="7557f-109">hello following types of routes can be applied tooeach network interface:</span></span>

* <span data-ttu-id="7557f-110">**系統路由︰** 在 Azure 虛擬網路 (VNet) 中建立的每個子網路預設都有系統路由表，允許本機 VNet 流量、透過 VPN 閘道的內部部署流量以及網際網路流量。</span><span class="sxs-lookup"><span data-stu-id="7557f-110">**System routes:** By default, every subnet created in an Azure Virtual Network (VNet) has system route tables that allow local VNet traffic, on-premises traffic via VPN gateways, and Internet traffic.</span></span> <span data-ttu-id="7557f-111">對等互連的 VNet 也有系統路由。</span><span class="sxs-lookup"><span data-stu-id="7557f-111">System routes also exist for peered VNets.</span></span>
* <span data-ttu-id="7557f-112">**BGP 路由：**傳播 toonetwork 介面透過 ExpressRoute 或站台對站 VPN 連線。</span><span class="sxs-lookup"><span data-stu-id="7557f-112">**BGP routes:** Propagated toonetwork interfaces through ExpressRoute or site-to-site VPN connections.</span></span> <span data-ttu-id="7557f-113">深入了解 BGP 路由閱讀 hello[與 VPN 閘道的 BGP](../vpn-gateway/vpn-gateway-bgp-overview.md)和[ExpressRoute 概觀](../expressroute/expressroute-introduction.md)文件。</span><span class="sxs-lookup"><span data-stu-id="7557f-113">Learn more about BGP routing by reading hello [BGP with VPN gateways](../vpn-gateway/vpn-gateway-bgp-overview.md) and [ExpressRoute overview](../expressroute/expressroute-introduction.md) articles.</span></span>
* <span data-ttu-id="7557f-114">**使用者定義的路由 (UDR):**如果您使用網路虛擬裝置，或會強制通道流量 tooan 透過站對站 VPN 的內部部署網路，您可能需要使用者定義的路由 (UDRs) 與子網路路由表相關聯。</span><span class="sxs-lookup"><span data-stu-id="7557f-114">**User-defined routes (UDR):** If you are using network virtual appliances or are forced-tunneling traffic tooan on-premises network via a site-to-site VPN, you may have user-defined routes (UDRs) associated with your subnet route table.</span></span> <span data-ttu-id="7557f-115">如果您不熟悉 UDRs，讀取 hello[使用者定義的路由](virtual-networks-udr-overview.md#user-defined-routes)發行項。</span><span class="sxs-lookup"><span data-stu-id="7557f-115">If you're not familiar with UDRs, read hello [user-defined routes](virtual-networks-udr-overview.md#user-defined-routes) article.</span></span>

<span data-ttu-id="7557f-116">以 hello 各種路由可以是套用的 tooa 網路介面，它可以是難以 toodetermine 為有效的彙總的路由。</span><span class="sxs-lookup"><span data-stu-id="7557f-116">With hello various routes that can be applied tooa network interface, it can be difficult toodetermine which aggregate routes are effective.</span></span> <span data-ttu-id="7557f-117">toohelp VM 網路連線問題疑難排解，您可以檢視所有的 hello 有效路由的網路介面在 hello Azure Resource Manager 部署模型。</span><span class="sxs-lookup"><span data-stu-id="7557f-117">toohelp troubleshoot VM network connectivity, you can view all hello effective routes for a network interface in hello Azure Resource Manager deployment model.</span></span>

## <a name="using-effective-routes-tootroubleshoot-vm-traffic-flow"></a><span data-ttu-id="7557f-118">使用有效路由 tootroubleshoot VM 流量</span><span class="sxs-lookup"><span data-stu-id="7557f-118">Using Effective Routes tootroubleshoot VM traffic flow</span></span>
<span data-ttu-id="7557f-119">本文使用 hello tootroubleshoot hello 有效會路由傳送網路介面的範例 tooillustrate 為下列案例：</span><span class="sxs-lookup"><span data-stu-id="7557f-119">This article uses hello following scenario as an example tooillustrate how tootroubleshoot hello effective routes for a network interface:</span></span>

<span data-ttu-id="7557f-120">VM (*VM1*) 連接 toohello VNet (*VNet1*，前置詞： 10.9.0.0/16) 失敗 tooconnect tooa VM(VM3) 新 peered VNet 中 (*VNet3*，前置詞 10.10.0.0/16)。</span><span class="sxs-lookup"><span data-stu-id="7557f-120">A VM (*VM1*) connected toohello VNet (*VNet1*, prefix: 10.9.0.0/16) fails tooconnect tooa VM(VM3) in a newly peered VNet (*VNet3*, prefix 10.10.0.0/16).</span></span> <span data-ttu-id="7557f-121">有沒有 UDRs 或 BGP 路由套用的 tooVM1 NIC1 網路連線介面 toohello VM，只有系統路由會套用。</span><span class="sxs-lookup"><span data-stu-id="7557f-121">There are no UDRs or BGP routes applied tooVM1-NIC1 network interface connected toohello VM, only system routes are applied.</span></span>

<span data-ttu-id="7557f-122">本文說明如何 toodetermine hello 原因 hello 連線失敗，使用 Azure 資源管理部署模型中的有效路由的功能。</span><span class="sxs-lookup"><span data-stu-id="7557f-122">This article explains how toodetermine hello cause of hello connection failure, using effective routes capability in Azure Resource Management deployment model.</span></span>
<span data-ttu-id="7557f-123">雖然 hello 範例會使用只有系統路由，hello 相同的步驟可以使用的 toodetermine 透過任何路由類型是傳入和傳出的連線失敗。</span><span class="sxs-lookup"><span data-stu-id="7557f-123">While hello example uses only system routes, hello same steps can be used toodetermine inbound and outbound connection failures over any route type.</span></span>

> [!NOTE]
> <span data-ttu-id="7557f-124">如果您的 VM 有連結的多個 NIC，請針對每個 hello Nic toodiagnose 網路連線問題 tooand 從 VM 檢查有效的路由。</span><span class="sxs-lookup"><span data-stu-id="7557f-124">If your VM has more than one NIC attached, check effective routes for each of hello NICs toodiagnose network connectivity issues tooand from a VM.</span></span>
> 
> 

### <a name="view-effective-routes-for-a-virtual-machine"></a><span data-ttu-id="7557f-125">檢視虛擬機器的有效路由</span><span class="sxs-lookup"><span data-stu-id="7557f-125">View effective routes for a virtual machine</span></span>
<span data-ttu-id="7557f-126">toosee hello 彙總路由的套用的 tooa VM，完成下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="7557f-126">toosee hello aggregate routes that are applied tooa VM, complete hello following steps:</span></span>

### <a name="view-effective-routes-for-a-network-interface"></a><span data-ttu-id="7557f-127">檢視網路介面的有效路由</span><span class="sxs-lookup"><span data-stu-id="7557f-127">View effective routes for a network interface</span></span>
<span data-ttu-id="7557f-128">toosee hello 彙總路由的套用的 tooa 網路介面，完成下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="7557f-128">toosee hello aggregate routes that are applied tooa network interface, complete hello following steps:</span></span>

1. <span data-ttu-id="7557f-129">啟動 Azure PowerShell 工作階段與登入 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="7557f-129">Start an Azure PowerShell session and login tooAzure.</span></span> <span data-ttu-id="7557f-130">如果您不熟悉 Azure PowerShell，請參閱 hello[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)發行項。</span><span class="sxs-lookup"><span data-stu-id="7557f-130">If you’re not familiar with Azure PowerShell, read hello [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) article.</span></span>
2. <span data-ttu-id="7557f-131">hello 下列命令會傳回名為所有的路由套用 tooa 網路介面*VM1 NIC1* hello 資源群組中*RG1*。</span><span class="sxs-lookup"><span data-stu-id="7557f-131">hello following command returns all routes applied tooa network interface named *VM1-NIC1* in hello resource group *RG1*.</span></span>
   
       Get-AzureRmEffectiveRouteTable -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1
   
   > [!TIP]
   > <span data-ttu-id="7557f-132">如果您不知道 hello 的網路介面的名稱，輸入下列命令 tooretrieve hello 名稱的所有網路介面卡中資源 group.* hello</span><span class="sxs-lookup"><span data-stu-id="7557f-132">If you don’t know hello name of a network interface, type hello following command tooretrieve hello names of all network interfaces in a resource group.*</span></span>
   > 
   > 
   
       Get-AzureRmNetworkInterface -ResourceGroupName RG1 | Format-Table Name
   
   <span data-ttu-id="7557f-133">hello 下列輸出看起來類似 toohello 輸出 NIC 連線到每個路由套用 toohello 子網路 hello:</span><span class="sxs-lookup"><span data-stu-id="7557f-133">hello following output looks similar toohello output for each route applied toohello subnet hello NIC is connected to:</span></span>
   
       Name :
       State : Active
       AddressPrefix : {10.9.0.0/16}
       NextHopType : VNetLocal
       NextHopIpAddress : {}
   
       Name :
       State : Active
       AddressPrefix : {0.0.0.0/16}
       NextHopType : Internet
       NextHopIpAddress : {}
   
   <span data-ttu-id="7557f-134">請注意 hello 輸出中的 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="7557f-134">Notice hello following in hello output:</span></span>
   
   * <span data-ttu-id="7557f-135">**名稱**: hello 有效路由的名稱可能是空的除非明確指定的使用者定義的路由。</span><span class="sxs-lookup"><span data-stu-id="7557f-135">**Name**: Name of hello effective route may be empty, unless explicitly specified, for user-defined routes.</span></span> 
   * <span data-ttu-id="7557f-136">**狀態**： 表示 hello 有效路由的狀態。</span><span class="sxs-lookup"><span data-stu-id="7557f-136">**State**: Indicates state of hello effective route.</span></span> <span data-ttu-id="7557f-137">可能的值為 "Active" 或 "Invalid"</span><span class="sxs-lookup"><span data-stu-id="7557f-137">Possible values are "Active" or "Invalid"</span></span>
   * <span data-ttu-id="7557f-138">**AddressPrefixes**： 以 CIDR 標記法指定有效路由的 hello hello 位址前置詞。</span><span class="sxs-lookup"><span data-stu-id="7557f-138">**AddressPrefixes**: Specifies hello address prefix of hello effective route in CIDR notation.</span></span> 
   * <span data-ttu-id="7557f-139">**nextHopType**： 指出 hello hello 指定路由的下一個躍點。</span><span class="sxs-lookup"><span data-stu-id="7557f-139">**nextHopType**: Indicates hello next hop for hello given route.</span></span> <span data-ttu-id="7557f-140">可能的值為 *VirtualAppliance*、*Internet*、*VNetLocal*、*VNetPeering* 或 *Null*。</span><span class="sxs-lookup"><span data-stu-id="7557f-140">Possible values are *VirtualAppliance*, *Internet*, *VNetLocal*, *VNetPeering*, or *Null*.</span></span> <span data-ttu-id="7557f-141">UDR 中 *nextHopType* 的值為 **Null** 可能表示是無效路由。</span><span class="sxs-lookup"><span data-stu-id="7557f-141">A value of *Null* for **nextHopType** in a UDR may indicate an invalid route.</span></span> <span data-ttu-id="7557f-142">例如，如果**nextHopType**是*VirtualAppliance*與 hello 網路虛擬設備 VM 並未處於執行佈建狀態。</span><span class="sxs-lookup"><span data-stu-id="7557f-142">For example, if **nextHopType** is *VirtualAppliance* and hello network virtual appliance VM is not in a provisioned/running state.</span></span> <span data-ttu-id="7557f-143">如果**nextHopType**是*VPNGateway*且沒有任何閘道佈建/執行中指定的 VNet 的 hello，hello 路由可能會變成無效。</span><span class="sxs-lookup"><span data-stu-id="7557f-143">If **nextHopType** is *VPNGateway* and there is no gateway provisioned/running in hello given VNet, hello route may become invalid.</span></span>
   * <span data-ttu-id="7557f-144">**NextHopIpAddress**： 指定 hello hello hello 有效路由的下一個躍點 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="7557f-144">**NextHopIpAddress**: Specifies hello IP address of hello next hop of hello effective route.</span></span>
   
   <span data-ttu-id="7557f-145">hello 下列命令會傳回 hello 路由更容易的 tooview 資料表中：</span><span class="sxs-lookup"><span data-stu-id="7557f-145">hello following command returns hello routes in an easier tooview table:</span></span>
   
       Get-AzureRmEffectiveRouteTable -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1 | Format-Table
   
   <span data-ttu-id="7557f-146">hello 以下輸出適某些 hello 輸出收到 hello 先前所述的案例：</span><span class="sxs-lookup"><span data-stu-id="7557f-146">hello following output is some of hello output received for hello scenario described previously:</span></span>
   
       Name State AddressPrefix NextHopType NextHopIpAddress
       ---- ----- ------------- ----------- ----------------
       Active {10.9.0.0/16} VnetLocal {}
       Active {0.0.0.0/0} Internet {}
3. <span data-ttu-id="7557f-147">沒有任何所列的路由 toohello *Uswest VNet3* VNet (前置詞從 10.10.0.0/16)** *Uswest VNet1* （首碼 10.9.0.0/16） hello 先前步驟中的 hello 輸出中。</span><span class="sxs-lookup"><span data-stu-id="7557f-147">There is no route listed toohello *WestUS-VNet3* VNet (Prefix 10.10.0.0/16)** from *WestUS-VNet1* (Prefix 10.9.0.0/16) in hello output from hello previous step.</span></span> <span data-ttu-id="7557f-148">Hello 下列圖片所示，hello VNet 對等的連結以 hello *Uswest VNet3* VNet 處於 hello *Disconnected*狀態。</span><span class="sxs-lookup"><span data-stu-id="7557f-148">As shown in hello following picture, hello VNet peering link with hello *WestUS-VNet3* VNet is in hello *Disconnected* state.</span></span>
   
    ![](./media/virtual-network-routes-troubleshoot-portal/image4.png)
   
    <span data-ttu-id="7557f-149">hello 雙向連結的 hello 對等互連已損毀，其中說明為什麼 VM1 無法連接在 hello tooVM3 *Uswest VNet3* VNet。</span><span class="sxs-lookup"><span data-stu-id="7557f-149">hello bi-directional link for hello peering is broken, which explains why VM1 could not connect tooVM3 in hello *WestUS-VNet3* VNet.</span></span> <span data-ttu-id="7557f-150">為 *WestUS-VNet1* 和 *WestUS-VNet3* VNet 再次設定雙向對等互連連結。</span><span class="sxs-lookup"><span data-stu-id="7557f-150">Setup a bi-directional VNet peering link again for *WestUS-VNet1* and *WestUS-VNet3* VNets.</span></span> <span data-ttu-id="7557f-151">hello hello VNet 對等互連已正確建立連結之後，傳回的輸出如下：</span><span class="sxs-lookup"><span data-stu-id="7557f-151">hello output returned after hello VNet peering link is correctly established follows:</span></span>
   
        Name State AddressPrefix NextHopType NextHopIpAddress
        ---- ----- ------------- ----------- ----------------
        Active {10.9.0.0/16} VnetLocal {}
        Active {10.10.0.0/16} VNetPeering {}
        Active {0.0.0.0/0} Internet {}
   
    <span data-ttu-id="7557f-152">一旦決定 hello 問題，您可以新增、 移除或變更路由及路由表。</span><span class="sxs-lookup"><span data-stu-id="7557f-152">Once you determine hello issue, you can add, remove, or change routes and route tables.</span></span> <span data-ttu-id="7557f-153">下列命令 toosee hello 命令的清單類型 hello 因此使用 toodo:</span><span class="sxs-lookup"><span data-stu-id="7557f-153">Type hello following command toosee a list of hello commands used toodo so:</span></span>
   
        Get-Help *-AzureRmRouteConfig

## <a name="considerations"></a><span data-ttu-id="7557f-154">考量</span><span class="sxs-lookup"><span data-stu-id="7557f-154">Considerations</span></span>
<span data-ttu-id="7557f-155">檢閱 hello 的路由清單時，請注意幾件事 tookeep 傳回：</span><span class="sxs-lookup"><span data-stu-id="7557f-155">A few things tookeep in mind when reviewing hello list of routes returned:</span></span>

* <span data-ttu-id="7557f-156">路由是根據 UDR、BGP 和系統路由之間的最長首碼比對 (LPM)。</span><span class="sxs-lookup"><span data-stu-id="7557f-156">Routing is based on Longest Prefix Match (LPM) among UDRs, BGP and system routes.</span></span> <span data-ttu-id="7557f-157">如果有多個路由 hello 相同 LPM 相符，然後根據 hello 順序的源頭選取路由：</span><span class="sxs-lookup"><span data-stu-id="7557f-157">If there is more than one route with hello same LPM match, then a route is selected based on its origin in hello following order:</span></span>
  
  * <span data-ttu-id="7557f-158">使用者定義路由</span><span class="sxs-lookup"><span data-stu-id="7557f-158">User-defined route</span></span>
  * <span data-ttu-id="7557f-159">BGP 路由</span><span class="sxs-lookup"><span data-stu-id="7557f-159">BGP route</span></span>
  * <span data-ttu-id="7557f-160">系統 (預設) 路由</span><span class="sxs-lookup"><span data-stu-id="7557f-160">System (Default) route</span></span>
    
    <span data-ttu-id="7557f-161">使用有效的路由，您只能看到有效路由的 LPM 根據所有 hello 了路由的相符項目。</span><span class="sxs-lookup"><span data-stu-id="7557f-161">With effective routes, you can only see effective routes that are LPM match based on all hello availble routes.</span></span> <span data-ttu-id="7557f-162">顯示 hello 路由以給定的 nic 如何評估，這讓您輕鬆 tootroubleshoot 特定路由且可能影響從您的 VM 的連線。</span><span class="sxs-lookup"><span data-stu-id="7557f-162">By showing how hello routes are actually evaluated for a given NIC, this makes it a lot easier tootroubleshoot specific routes that may be impacting connectivity to/from your VM.</span></span>
* <span data-ttu-id="7557f-163">如果您有 UDRs 並傳送流量 tooa 網路的虛擬設備 (NVA)，與*VirtualAppliance*為**nextHopType**，確定已啟用 IP 轉送 hello NVA 接收 hello 流量或捨棄的封包。</span><span class="sxs-lookup"><span data-stu-id="7557f-163">If you have UDRs and are sending traffic tooa network virtual appliance (NVA), with *VirtualAppliance* as **nextHopType**, ensure that IP forwarding is enabled on hello NVA receiving hello traffic or packets are dropped.</span></span> 
* <span data-ttu-id="7557f-164">如果已啟用強制通道，所有傳出網際網路流量會路由的 tooon 內部。</span><span class="sxs-lookup"><span data-stu-id="7557f-164">If Forced tunneling is enabled, all outbound Internet traffic will be routed tooon-premises.</span></span> <span data-ttu-id="7557f-165">RDP/SSH 從網際網路 tooyour VM 可能不適用於此設定，根據如何 hello 內部處理這個流量。</span><span class="sxs-lookup"><span data-stu-id="7557f-165">RDP/SSH from Internet tooyour VM may not work with this setting, depending on how hello on-premises handles this traffic.</span></span> 
  <span data-ttu-id="7557f-166">符合下列其中一個條件時，可以啟用強制通道︰</span><span class="sxs-lookup"><span data-stu-id="7557f-166">Forced-tunneling can be enabled:</span></span>
  * <span data-ttu-id="7557f-167">使用站台對站台 VPN 時，將使用者定義路由 (UDR) 的 nextHopType 設定為 VPNGateway</span><span class="sxs-lookup"><span data-stu-id="7557f-167">If using site-to-site VPN, by setting a user-defined route (UDR) with nextHopType as VPN Gateway</span></span>
  * <span data-ttu-id="7557f-168">透過 BGP 公告預設路由</span><span class="sxs-lookup"><span data-stu-id="7557f-168">If a default route is advertised over BGP</span></span>
* <span data-ttu-id="7557f-169">Vnet 對等互連流量 toowork 正確的系統路由**nextHopType** *VNetPeering*的 hello 所以 VNet 的前置詞的範圍必須存在。</span><span class="sxs-lookup"><span data-stu-id="7557f-169">For VNet peering traffic toowork correctly, a system route with **nextHopType** *VNetPeering* must exist for hello peered VNet’s prefix range.</span></span> <span data-ttu-id="7557f-170">如果這類的路由不存在，而且 hello 對等互連的 VNet 連結正確無誤：</span><span class="sxs-lookup"><span data-stu-id="7557f-170">If such a route doesn’t exist and hello VNet peering link looks OK:</span></span>
  * <span data-ttu-id="7557f-171">如果是新建立的對等互連連結，請等候幾秒鐘並重試。</span><span class="sxs-lookup"><span data-stu-id="7557f-171">Wait a few seconds and retry if it's a newly established peering link.</span></span> <span data-ttu-id="7557f-172">它有時會接受路途 toopropagate tooall hello 網路介面的子網路。</span><span class="sxs-lookup"><span data-stu-id="7557f-172">It occasionally takes longer toopropagate routes tooall hello network interfaces in a subnet.</span></span>
  * <span data-ttu-id="7557f-173">Hello 流量可能影響網路安全性群組 (NSG) 規則。</span><span class="sxs-lookup"><span data-stu-id="7557f-173">Network Security Group (NSG) rules may be impacting hello traffic flows.</span></span> <span data-ttu-id="7557f-174">如需詳細資訊，請參閱 hello[疑難排解網路安全性群組](virtual-network-nsg-troubleshoot-powershell.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="7557f-174">For more information, see hello [Troubleshoot Network Security Groups](virtual-network-nsg-troubleshoot-powershell.md) article.</span></span>

