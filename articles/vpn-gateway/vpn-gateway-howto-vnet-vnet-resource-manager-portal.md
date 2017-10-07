---
title: "連接 Azure 虛擬網路 tooanother VNet： 入口網站 |Microsoft 文件"
description: "建立 Vnet 使用資源管理員之間的 VPN 閘道連線，並 hello Azure 入口網站。"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: a7015cfc-764b-46a1-bfac-043d30a275df
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/02/2017
ms.author: cherylmc
ms.openlocfilehash: a529f90d976bee0f50403947d06e9da8a6c05349
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-vnet-to-vnet-vpn-gateway-connection-using-hello-azure-portal"></a><span data-ttu-id="9c858-103">設定 VNet 對 VNet VPN 閘道連線使用 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="9c858-103">Configure a VNet-to-VNet VPN gateway connection using hello Azure portal</span></span>

<span data-ttu-id="9c858-104">本文章將示範如何 toocreate 虛擬網路之間的 VPN 閘道連線。</span><span class="sxs-lookup"><span data-stu-id="9c858-104">This article shows you how toocreate a VPN gateway connection between virtual networks.</span></span> <span data-ttu-id="9c858-105">hello 虛擬網路可在 hello 相同或不同區域，並從 hello 相同或不同的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="9c858-105">hello virtual networks can be in hello same or different regions, and from hello same or different subscriptions.</span></span> <span data-ttu-id="9c858-106">當連接的 Vnet，從不同的訂用帳戶，hello 訂用帳戶不需要與相關聯的 toobe hello 相同的 Active Directory 租用戶。</span><span class="sxs-lookup"><span data-stu-id="9c858-106">When connecting VNets from different subscriptions, hello subscriptions do not need toobe associated with hello same Active Directory tenant.</span></span> 

<span data-ttu-id="9c858-107">這篇文章中的 hello 步驟套用 toohello Resource Manager 部署模型，並使用 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="9c858-107">hello steps in this article apply toohello Resource Manager deployment model and use hello Azure portal.</span></span> <span data-ttu-id="9c858-108">您也可以建立此組態使用不同的部署工具或部署模型，從下列清單中的 hello 選取不同的選項：</span><span class="sxs-lookup"><span data-stu-id="9c858-108">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="9c858-109">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="9c858-109">Azure portal</span></span>](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)
> * [<span data-ttu-id="9c858-110">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9c858-110">PowerShell</span></span>](vpn-gateway-vnet-vnet-rm-ps.md)
> * [<span data-ttu-id="9c858-111">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="9c858-111">Azure CLI</span></span>](vpn-gateway-howto-vnet-vnet-cli.md)
> * [<span data-ttu-id="9c858-112">Azure 入口網站 (傳統)</span><span class="sxs-lookup"><span data-stu-id="9c858-112">Azure portal (classic)</span></span>](vpn-gateway-howto-vnet-vnet-portal-classic.md)
> * [<span data-ttu-id="9c858-113">連線不同的部署模型 - Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="9c858-113">Connect different deployment models - Azure portal</span></span>](vpn-gateway-connect-different-deployment-models-portal.md)
> * [<span data-ttu-id="9c858-114">連線不同的部署模型 - PowerShell</span><span class="sxs-lookup"><span data-stu-id="9c858-114">Connect different deployment models - PowerShell</span></span>](vpn-gateway-connect-different-deployment-models-powershell.md)
>
>

![v2v 圖表](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/v2vrmps.png)

<span data-ttu-id="9c858-116">連接虛擬網路 tooanother 虛擬網路 (VNet 對 VNet) 是類似 tooconnecting VNet tooan 在內部部署站台位置。</span><span class="sxs-lookup"><span data-stu-id="9c858-116">Connecting a virtual network tooanother virtual network (VNet-to-VNet) is similar tooconnecting a VNet tooan on-premises site location.</span></span> <span data-ttu-id="9c858-117">這兩種連線類型使用的 VPN 閘道 tooprovide 採用 IPsec/IKE 的安全通道。</span><span class="sxs-lookup"><span data-stu-id="9c858-117">Both connectivity types use a VPN gateway tooprovide a secure tunnel using IPsec/IKE.</span></span> <span data-ttu-id="9c858-118">如果您的 Vnet hello 中相同的區域，您可能會想 tooconsider 它們使用對等互連的 VNet 連接。</span><span class="sxs-lookup"><span data-stu-id="9c858-118">If your VNets are in hello same region, you may want tooconsider connecting them using VNet Peering.</span></span> <span data-ttu-id="9c858-119">VNet 對等互連不會使用 VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="9c858-119">VNet peering does not use a VPN gateway.</span></span> <span data-ttu-id="9c858-120">如需詳細資訊，請參閱 [VNet 對等互連](../virtual-network/virtual-network-peering-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="9c858-120">For more information, see [VNet peering](../virtual-network/virtual-network-peering-overview.md).</span></span>

<span data-ttu-id="9c858-121">您可以將 VNet 對 VNet 通訊與多站台組態結合。</span><span class="sxs-lookup"><span data-stu-id="9c858-121">VNet-to-VNet communication can be combined with multi-site configurations.</span></span> <span data-ttu-id="9c858-122">這可讓您建立結合內部虛擬網路連線使用跨單位連線的網路拓樸 hello 下列圖表所示：</span><span class="sxs-lookup"><span data-stu-id="9c858-122">This lets you establish network topologies that combine cross-premises connectivity with inter-virtual network connectivity, as shown in hello following diagram:</span></span>

<span data-ttu-id="9c858-123">![關於連接](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/aboutconnections.png "關於連接")</span><span class="sxs-lookup"><span data-stu-id="9c858-123">![About connections](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/aboutconnections.png "About connections")</span></span>

### <a name="why-connect-virtual-networks"></a><span data-ttu-id="9c858-124">為什麼要連接虛擬網路？</span><span class="sxs-lookup"><span data-stu-id="9c858-124">Why connect virtual networks?</span></span>

<span data-ttu-id="9c858-125">您可以遵循原因 hello tooconnect 虛擬網路：</span><span class="sxs-lookup"><span data-stu-id="9c858-125">You may want tooconnect virtual networks for hello following reasons:</span></span>

* <span data-ttu-id="9c858-126">**跨區域的異地備援和異地目前狀態**</span><span class="sxs-lookup"><span data-stu-id="9c858-126">**Cross region geo-redundancy and geo-presence**</span></span>
  
  * <span data-ttu-id="9c858-127">您可以使用安全連線設定自己的異地複寫或同步處理，而不用查看網際網路對向端點。</span><span class="sxs-lookup"><span data-stu-id="9c858-127">You can set up your own geo-replication or synchronization with secure connectivity without going over Internet-facing endpoints.</span></span>
  * <span data-ttu-id="9c858-128">您可以使用 Azure 流量管理員和負載平衡器，利用異地備援跨多個 Azure 區域設定高度可用的工作負載。</span><span class="sxs-lookup"><span data-stu-id="9c858-128">With Azure Traffic Manager and Load Balancer, you can set up highly available workload with geo-redundancy across multiple Azure regions.</span></span> <span data-ttu-id="9c858-129">重要的一個例子是 tooset 設定 SQL Always On 與分配到多個 Azure 區域的可用性群組。</span><span class="sxs-lookup"><span data-stu-id="9c858-129">One important example is tooset up SQL Always On with Availability Groups spreading across multiple Azure regions.</span></span>
* <span data-ttu-id="9c858-130">**具有隔離或管理界限的區域性多層式應用程式**</span><span class="sxs-lookup"><span data-stu-id="9c858-130">**Regional multi-tier applications with isolation or administrative boundary**</span></span>
  
  * <span data-ttu-id="9c858-131">在 hello 相同區域中，您可以設定多層應用程式與多個虛擬網路連接在一起，因為 tooisolation 或系統管理需求。</span><span class="sxs-lookup"><span data-stu-id="9c858-131">Within hello same region, you can set up multi-tier applications with multiple virtual networks connected together due tooisolation or administrative requirements.</span></span>

<span data-ttu-id="9c858-132">如需 VNet 對 VNet 連線的詳細資訊，請參閱 hello [VNet 對 VNet 常見問題集](#faq)hello 本文結尾處。</span><span class="sxs-lookup"><span data-stu-id="9c858-132">For more information about VNet-to-VNet connections, see hello [VNet-to-VNet FAQ](#faq) at hello end of this article.</span></span> <span data-ttu-id="9c858-133">請注意，是否您的 Vnet 不同訂用帳戶中，您無法建立 hello 連接 hello 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="9c858-133">Note that if your VNets are in different subscriptions, you can't create hello connection in hello portal.</span></span> <span data-ttu-id="9c858-134">您可以使用 [PowerShell](vpn-gateway-vnet-vnet-rm-ps.md) 或 [CLI](vpn-gateway-howto-vnet-vnet-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="9c858-134">You can use [PowerShell](vpn-gateway-vnet-vnet-rm-ps.md) or [CLI](vpn-gateway-howto-vnet-vnet-cli.md).</span></span>

### <span data-ttu-id="9c858-135"><a name="values"></a>設定範例</span><span class="sxs-lookup"><span data-stu-id="9c858-135"><a name="values"></a>Example settings</span></span>

<span data-ttu-id="9c858-136">當使用這些步驟，做為練習，您可以使用 hello 範例設定值。</span><span class="sxs-lookup"><span data-stu-id="9c858-136">When using these steps as an exercise, you can use hello example settings values.</span></span> <span data-ttu-id="9c858-137">為了舉例說明，我們對每個 VNet 使用多個位址空間。</span><span class="sxs-lookup"><span data-stu-id="9c858-137">For example purposes, we use multiple address spaces for each VNet.</span></span> <span data-ttu-id="9c858-138">不過，VNet 對 VNet 組態不需要多個位址空間。</span><span class="sxs-lookup"><span data-stu-id="9c858-138">However, VNet-to-VNet configurations don't require multiple address spaces.</span></span>

<span data-ttu-id="9c858-139">**TestVNet1 的值︰**</span><span class="sxs-lookup"><span data-stu-id="9c858-139">**Values for TestVNet1:**</span></span>

* <span data-ttu-id="9c858-140">VNet 名稱︰TestVNet1</span><span class="sxs-lookup"><span data-stu-id="9c858-140">VNet Name: TestVNet1</span></span>
* <span data-ttu-id="9c858-141">位址空間︰10.11.0.0/16</span><span class="sxs-lookup"><span data-stu-id="9c858-141">Address space: 10.11.0.0/16</span></span>
  * <span data-ttu-id="9c858-142">子網路名稱：FrontEnd</span><span class="sxs-lookup"><span data-stu-id="9c858-142">Subnet name: FrontEnd</span></span>
  * <span data-ttu-id="9c858-143">子網路位址範圍：10.11.0.0/24</span><span class="sxs-lookup"><span data-stu-id="9c858-143">Subnet address range: 10.11.0.0/24</span></span>
* <span data-ttu-id="9c858-144">資源群組︰TestRG1</span><span class="sxs-lookup"><span data-stu-id="9c858-144">Resource Group: TestRG1</span></span>
* <span data-ttu-id="9c858-145">位置：美國東部</span><span class="sxs-lookup"><span data-stu-id="9c858-145">Location: East US</span></span>
* <span data-ttu-id="9c858-146">位址空間︰10.12.0.0/16</span><span class="sxs-lookup"><span data-stu-id="9c858-146">Address Space: 10.12.0.0/16</span></span>
  * <span data-ttu-id="9c858-147">子網路名稱：BackEnd</span><span class="sxs-lookup"><span data-stu-id="9c858-147">Subnet name: BackEnd</span></span>
  * <span data-ttu-id="9c858-148">子網路位址範圍︰10.12.0.0/24</span><span class="sxs-lookup"><span data-stu-id="9c858-148">Subnet address range: 10.12.0.0/24</span></span>
* <span data-ttu-id="9c858-149">閘道子網路名稱： GatewaySubnet （如此便會自動填滿 hello 入口網站中）</span><span class="sxs-lookup"><span data-stu-id="9c858-149">Gateway Subnet name: GatewaySubnet (this will auto-fill in hello portal)</span></span>
  * <span data-ttu-id="9c858-150">閘道子網路位址範圍︰10.11.255.0/27</span><span class="sxs-lookup"><span data-stu-id="9c858-150">Gateway Subnet address range: 10.11.255.0/27</span></span>
* <span data-ttu-id="9c858-151">DNS 伺服器： 使用您的 DNS 伺服器 hello IP 位址</span><span class="sxs-lookup"><span data-stu-id="9c858-151">DNS Server: Use hello IP address of your DNS Server</span></span>
* <span data-ttu-id="9c858-152">虛擬網路閘道名稱︰TestVNet1GW</span><span class="sxs-lookup"><span data-stu-id="9c858-152">Virtual Network Gateway Name: TestVNet1GW</span></span>
* <span data-ttu-id="9c858-153">閘道類型：VPN</span><span class="sxs-lookup"><span data-stu-id="9c858-153">Gateway Type: VPN</span></span>
* <span data-ttu-id="9c858-154">VPN 類型：路由式</span><span class="sxs-lookup"><span data-stu-id="9c858-154">VPN type: Route-based</span></span>
* <span data-ttu-id="9c858-155">SKU： 選取您想要 toouse 的閘道 SKU hello</span><span class="sxs-lookup"><span data-stu-id="9c858-155">SKU: Select hello Gateway SKU you want toouse</span></span>
* <span data-ttu-id="9c858-156">公用 IP 位址名稱︰TestVNet1GWIP</span><span class="sxs-lookup"><span data-stu-id="9c858-156">Public IP address name: TestVNet1GWIP</span></span>
* <span data-ttu-id="9c858-157">連接值︰</span><span class="sxs-lookup"><span data-stu-id="9c858-157">Connection values:</span></span>
  * <span data-ttu-id="9c858-158">名稱︰TestVNet1toTestVNet4</span><span class="sxs-lookup"><span data-stu-id="9c858-158">Name: TestVNet1toTestVNet4</span></span>
  * <span data-ttu-id="9c858-159">共用的金鑰： 您可以自行建立 hello 共用的金鑰。</span><span class="sxs-lookup"><span data-stu-id="9c858-159">Shared key: You can create hello shared key yourself.</span></span> <span data-ttu-id="9c858-160">此範例中，我們將使用 abc123。</span><span class="sxs-lookup"><span data-stu-id="9c858-160">For this example, we'll use abc123.</span></span> <span data-ttu-id="9c858-161">hello 重點是，當您建立 hello hello Vnet 之間的連線，必須符合 hello 值。</span><span class="sxs-lookup"><span data-stu-id="9c858-161">hello important thing is that when you create hello connection between hello VNets, hello value must match.</span></span>

<span data-ttu-id="9c858-162">**TestVNet4 的值︰**</span><span class="sxs-lookup"><span data-stu-id="9c858-162">**Values for TestVNet4:**</span></span>

* <span data-ttu-id="9c858-163">VNet 名稱︰TestVNet4</span><span class="sxs-lookup"><span data-stu-id="9c858-163">VNet Name: TestVNet4</span></span>
* <span data-ttu-id="9c858-164">位址空間︰10.41.0.0/16</span><span class="sxs-lookup"><span data-stu-id="9c858-164">Address space: 10.41.0.0/16</span></span>
  * <span data-ttu-id="9c858-165">子網路名稱：FrontEnd</span><span class="sxs-lookup"><span data-stu-id="9c858-165">Subnet name: FrontEnd</span></span>
  * <span data-ttu-id="9c858-166">子網路位址範圍︰10.41.0.0/24</span><span class="sxs-lookup"><span data-stu-id="9c858-166">Subnet address range: 10.41.0.0/24</span></span>
* <span data-ttu-id="9c858-167">資源群組︰TestRG1</span><span class="sxs-lookup"><span data-stu-id="9c858-167">Resource Group: TestRG1</span></span>
* <span data-ttu-id="9c858-168">位置：美國西部</span><span class="sxs-lookup"><span data-stu-id="9c858-168">Location: West US</span></span>
* <span data-ttu-id="9c858-169">位址空間︰10.42.0.0/16</span><span class="sxs-lookup"><span data-stu-id="9c858-169">Address Space: 10.42.0.0/16</span></span>
  * <span data-ttu-id="9c858-170">子網路名稱：BackEnd</span><span class="sxs-lookup"><span data-stu-id="9c858-170">Subnet name: BackEnd</span></span>
  * <span data-ttu-id="9c858-171">子網路位址範圍︰10.42.0.0/24</span><span class="sxs-lookup"><span data-stu-id="9c858-171">Subnet address range: 10.42.0.0/24</span></span>
* <span data-ttu-id="9c858-172">GatewaySubnet 名稱： GatewaySubnet （如此便會自動填滿 hello 入口網站中）</span><span class="sxs-lookup"><span data-stu-id="9c858-172">GatewaySubnet name: GatewaySubnet (this will auto-fill in hello portal)</span></span>
  * <span data-ttu-id="9c858-173">閘道子網路位址範圍︰10.41.255.0/27</span><span class="sxs-lookup"><span data-stu-id="9c858-173">GatewaySubnet address range: 10.41.255.0/27</span></span>
* <span data-ttu-id="9c858-174">DNS 伺服器： 使用您的 DNS 伺服器 hello IP 位址</span><span class="sxs-lookup"><span data-stu-id="9c858-174">DNS Server: Use hello IP address of your DNS Server</span></span>
* <span data-ttu-id="9c858-175">虛擬網路閘道名稱︰TestVNet4GW</span><span class="sxs-lookup"><span data-stu-id="9c858-175">Virtual Network Gateway Name: TestVNet4GW</span></span>
* <span data-ttu-id="9c858-176">閘道類型：VPN</span><span class="sxs-lookup"><span data-stu-id="9c858-176">Gateway Type: VPN</span></span>
* <span data-ttu-id="9c858-177">VPN 類型：路由式</span><span class="sxs-lookup"><span data-stu-id="9c858-177">VPN type: Route-based</span></span>
* <span data-ttu-id="9c858-178">SKU： 選取您想要 toouse 的閘道 SKU hello</span><span class="sxs-lookup"><span data-stu-id="9c858-178">SKU: Select hello Gateway SKU you want toouse</span></span>
* <span data-ttu-id="9c858-179">公用 IP 位址名稱︰TestVNet4GWIP</span><span class="sxs-lookup"><span data-stu-id="9c858-179">Public IP address name: TestVNet4GWIP</span></span>
* <span data-ttu-id="9c858-180">連接值︰</span><span class="sxs-lookup"><span data-stu-id="9c858-180">Connection values:</span></span>
  * <span data-ttu-id="9c858-181">名稱︰TestVNet4toTestVNet1</span><span class="sxs-lookup"><span data-stu-id="9c858-181">Name: TestVNet4toTestVNet1</span></span>
  * <span data-ttu-id="9c858-182">共用的金鑰： 您可以自行建立 hello 共用的金鑰。</span><span class="sxs-lookup"><span data-stu-id="9c858-182">Shared key: You can create hello shared key yourself.</span></span> <span data-ttu-id="9c858-183">此範例中，我們將使用 abc123。</span><span class="sxs-lookup"><span data-stu-id="9c858-183">For this example, we'll use abc123.</span></span> <span data-ttu-id="9c858-184">hello 重點是，當您建立 hello hello Vnet 之間的連線，必須符合 hello 值。</span><span class="sxs-lookup"><span data-stu-id="9c858-184">hello important thing is that when you create hello connection between hello VNets, hello value must match.</span></span>

## <span data-ttu-id="9c858-185"><a name="CreatVNet"></a>1.建立及設定 TestVNet1</span><span class="sxs-lookup"><span data-stu-id="9c858-185"><a name="CreatVNet"></a>1. Create and configure TestVNet1</span></span>
<span data-ttu-id="9c858-186">如果您沒有 VNet，請確認 hello 設定與您的 VPN 閘道設計相容。</span><span class="sxs-lookup"><span data-stu-id="9c858-186">If you already have a VNet, verify that hello settings are compatible with your VPN gateway design.</span></span> <span data-ttu-id="9c858-187">請特別注意 tooany 的子網路，可能會與其他網路重疊。</span><span class="sxs-lookup"><span data-stu-id="9c858-187">Pay particular attention tooany subnets that may overlap with other networks.</span></span> <span data-ttu-id="9c858-188">如果有重疊的子網路，您的連線便無法正常運作。</span><span class="sxs-lookup"><span data-stu-id="9c858-188">If you have overlapping subnets, your connection won't work properly.</span></span> <span data-ttu-id="9c858-189">如果您的 VNet 設定的 hello 正確的設定，就可以開始在 hello hello 步驟[指定 DNS 伺服器](#dns)> 一節。</span><span class="sxs-lookup"><span data-stu-id="9c858-189">If your VNet is configured with hello correct settings, you can begin hello steps in hello [Specify a DNS server](#dns) section.</span></span>

### <a name="toocreate-a-virtual-network"></a><span data-ttu-id="9c858-190">toocreate 虛擬網路</span><span class="sxs-lookup"><span data-stu-id="9c858-190">toocreate a virtual network</span></span>
[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-basic-vnet-rm-portal-include.md)]

## <span data-ttu-id="9c858-191"><a name="subnets"></a>2.新增其他位址空間和建立子網路</span><span class="sxs-lookup"><span data-stu-id="9c858-191"><a name="subnets"></a>2. Add additional address space and create subnets</span></span>
<span data-ttu-id="9c858-192">建立 VNet 之後，您可以新增其他位址空間和建立子網路。</span><span class="sxs-lookup"><span data-stu-id="9c858-192">You can add additional address space and create subnets once your VNet has been created.</span></span>

[!INCLUDE [vpn-gateway-additional-address-space](../../includes/vpn-gateway-additional-address-space-include.md)]

## <span data-ttu-id="9c858-193"><a name="gatewaysubnet"></a>3.建立閘道子網路</span><span class="sxs-lookup"><span data-stu-id="9c858-193"><a name="gatewaysubnet"></a>3. Create a gateway subnet</span></span>
<span data-ttu-id="9c858-194">連接您的虛擬網路 tooa 閘道之前，您首先需要 toocreate hello 閘道子網路要為 hello 虛擬網路 toowhich tooconnect。</span><span class="sxs-lookup"><span data-stu-id="9c858-194">Before connecting your virtual network tooa gateway, you first need toocreate hello gateway subnet for hello virtual network toowhich you want tooconnect.</span></span> <span data-ttu-id="9c858-195">可能的話，它是最佳 toocreate 閘道子網路中順序 tooprovide 使用 CIDR 區塊/28 或 /27 足夠的 IP 位址 tooaccommodate 額外設定需求。</span><span class="sxs-lookup"><span data-stu-id="9c858-195">If possible, it's best toocreate a gateway subnet using a CIDR block of /28 or /27 in order tooprovide enough IP addresses tooaccommodate additional future configuration requirements.</span></span>

<span data-ttu-id="9c858-196">如果您要建立此設定做為練習，請參閱 toothese[範例設定](#values)時建立您的閘道子網路。</span><span class="sxs-lookup"><span data-stu-id="9c858-196">If you are creating this configuration as an exercise, refer toothese [Example settings](#values) when creating your gateway subnet.</span></span>

[!INCLUDE [vpn-gateway-no-nsg](../../includes/vpn-gateway-no-nsg-include.md)]

### <a name="toocreate-a-gateway-subnet"></a><span data-ttu-id="9c858-197">toocreate 閘道子網路</span><span class="sxs-lookup"><span data-stu-id="9c858-197">toocreate a gateway subnet</span></span>
[!INCLUDE [vpn-gateway-add-gwsubnet-rm-portal](../../includes/vpn-gateway-add-gwsubnet-rm-portal-include.md)]

## <span data-ttu-id="9c858-198"><a name="dns"></a>4.指定 DNS 伺服器 (選擇性)</span><span class="sxs-lookup"><span data-stu-id="9c858-198"><a name="dns"></a>4. Specify a DNS server (optional)</span></span>
<span data-ttu-id="9c858-199">VNet 對 VNet 連線不需要 DNS。</span><span class="sxs-lookup"><span data-stu-id="9c858-199">DNS is not required for VNet-to-VNet connections.</span></span> <span data-ttu-id="9c858-200">不過，如果您想要部署的 tooyour 虛擬網路的資源 toohave 名稱解析，您應該指定 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="9c858-200">However, if you want toohave name resolution for resources that are deployed tooyour virtual network, you should specify a DNS server.</span></span> <span data-ttu-id="9c858-201">此設定可讓您指定 hello toouse 需為此虛擬網路的名稱解析的 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="9c858-201">This setting lets you specify hello DNS server that you want toouse for name resolution for this virtual network.</span></span> <span data-ttu-id="9c858-202">它不會建立 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="9c858-202">It does not create a DNS server.</span></span>

[!INCLUDE [vpn-gateway-add-dns-rm-portal](../../includes/vpn-gateway-add-dns-rm-portal-include.md)]

## <span data-ttu-id="9c858-203"><a name="VNetGateway"></a>5.建立虛擬網路閘道</span><span class="sxs-lookup"><span data-stu-id="9c858-203"><a name="VNetGateway"></a>5. Create a virtual network gateway</span></span>
<span data-ttu-id="9c858-204">在此步驟中，您可以建立 hello 虛擬網路閘道的 VNet。</span><span class="sxs-lookup"><span data-stu-id="9c858-204">In this step, you create hello virtual network gateway for your VNet.</span></span> <span data-ttu-id="9c858-205">建立閘道可以通常要花費 45 分鐘以上，視 hello 選取的閘道 SKU。</span><span class="sxs-lookup"><span data-stu-id="9c858-205">Creating a gateway can often take 45 minutes or more, depending on hello selected gateway SKU.</span></span> <span data-ttu-id="9c858-206">如果您要建立此設定做為練習，您可以參考 toohello[範例設定](#values)。</span><span class="sxs-lookup"><span data-stu-id="9c858-206">If you are creating this configuration as an exercise, you can refer toohello [Example settings](#values).</span></span>

### <a name="toocreate-a-virtual-network-gateway"></a><span data-ttu-id="9c858-207">toocreate 虛擬網路閘道</span><span class="sxs-lookup"><span data-stu-id="9c858-207">toocreate a virtual network gateway</span></span>
[!INCLUDE [vpn-gateway-add-gw-rm-portal](../../includes/vpn-gateway-add-gw-rm-portal-include.md)]

## <span data-ttu-id="9c858-208"><a name="CreateTestVNet4"></a>6.建立及設定 TestVNet4</span><span class="sxs-lookup"><span data-stu-id="9c858-208"><a name="CreateTestVNet4"></a>6. Create and configure TestVNet4</span></span>
<span data-ttu-id="9c858-209">當您設定 TestVNet1 之後時，請重複 hello 先前步驟中，取代這些 TestVNet4 hello 值建立 TestVNet4。</span><span class="sxs-lookup"><span data-stu-id="9c858-209">Once you've configured TestVNet1, create TestVNet4 by repeating hello previous steps, replacing hello values with those of TestVNet4.</span></span> <span data-ttu-id="9c858-210">您無須 toowait TestVNet1 hello 虛擬網路閘道後才設定 TestVNet4 之前建立。</span><span class="sxs-lookup"><span data-stu-id="9c858-210">You don't need toowait until hello virtual network gateway for TestVNet1 has finished creating before configuring TestVNet4.</span></span> <span data-ttu-id="9c858-211">如果您使用您自己的值，請確定 hello 位址空間不與任何 hello 您想要 tooconnect 的 Vnet 重疊。</span><span class="sxs-lookup"><span data-stu-id="9c858-211">If you are using your own values, make sure that hello address spaces don't overlap with any of hello VNets that you want tooconnect to.</span></span>

## <span data-ttu-id="9c858-212"><a name="TestVNet1Connection"></a>7.設定 hello TestVNet1 連線</span><span class="sxs-lookup"><span data-stu-id="9c858-212"><a name="TestVNet1Connection"></a>7. Configure hello TestVNet1 connection</span></span>
<span data-ttu-id="9c858-213">當完成 TestVNet1 和 TestVNet4 hello 虛擬網路閘道時，您可以建立虛擬網路閘道連線。</span><span class="sxs-lookup"><span data-stu-id="9c858-213">When hello virtual network gateways for both TestVNet1 and TestVNet4 have completed, you can create your virtual network gateway connections.</span></span> <span data-ttu-id="9c858-214">在本節中，您將從 VNet1 tooVNet4 建立連接。</span><span class="sxs-lookup"><span data-stu-id="9c858-214">In this section, you will create a connection from VNet1 tooVNet4.</span></span> <span data-ttu-id="9c858-215">這些步驟只適用於 hello 的 Vnet 相同訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="9c858-215">These steps work only for VNets in hello same subscription.</span></span> <span data-ttu-id="9c858-216">如果您的 Vnet 不同訂用帳戶中，您必須使用 PowerShell toomake hello 連接。</span><span class="sxs-lookup"><span data-stu-id="9c858-216">If your VNets are in different subscriptions, you must use PowerShell toomake hello connection.</span></span> <span data-ttu-id="9c858-217">請參閱 hello [PowerShell](vpn-gateway-vnet-vnet-rm-ps.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="9c858-217">See hello [PowerShell](vpn-gateway-vnet-vnet-rm-ps.md) article.</span></span>

1. <span data-ttu-id="9c858-218">在**所有資源**，瀏覽您的 VNet toohello 虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="9c858-218">In **All resources**, navigate toohello virtual network gateway for your VNet.</span></span> <span data-ttu-id="9c858-219">例如，**TestVNet1GW**。</span><span class="sxs-lookup"><span data-stu-id="9c858-219">For example, **TestVNet1GW**.</span></span> <span data-ttu-id="9c858-220">按一下**TestVNet1GW** tooopen hello 虛擬網路閘道刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="9c858-220">Click **TestVNet1GW** tooopen hello virtual network gateway blade.</span></span>
   
    <span data-ttu-id="9c858-221">![連接刀鋒視窗](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/settings_connection.png "連接刀鋒視窗e")</span><span class="sxs-lookup"><span data-stu-id="9c858-221">![Connections blade](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/settings_connection.png "Connections blade")</span></span>
2. <span data-ttu-id="9c858-222">按一下**+ 加**tooopen hello**加入連接**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="9c858-222">Click **+Add** tooopen hello **Add connection** blade.</span></span>
3. <span data-ttu-id="9c858-223">在 hello**加入連接**刀鋒視窗中，在 hello 名稱欄位中，輸入您的連線的名稱。</span><span class="sxs-lookup"><span data-stu-id="9c858-223">On hello **Add connection** blade, in hello name field, type a name for your connection.</span></span> <span data-ttu-id="9c858-224">例如，**TestVNet1toTestVNet4**。</span><span class="sxs-lookup"><span data-stu-id="9c858-224">For example, **TestVNet1toTestVNet4**.</span></span>
   
    <span data-ttu-id="9c858-225">![連接名稱](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/v1tov4.png "連接名稱")</span><span class="sxs-lookup"><span data-stu-id="9c858-225">![Connection name](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/v1tov4.png "Connection name")</span></span>
4. <span data-ttu-id="9c858-226">在 [連線類型] 中，</span><span class="sxs-lookup"><span data-stu-id="9c858-226">For **Connection type**.</span></span> <span data-ttu-id="9c858-227">選取**VNet 對 VNet**從 hello 下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="9c858-227">select **VNet-to-VNet** from hello dropdown.</span></span>
5. <span data-ttu-id="9c858-228">hello**第一個虛擬網路閘道**因為您正在建立此連線從 hello 指定的虛擬網路閘道，自動填入欄位值。</span><span class="sxs-lookup"><span data-stu-id="9c858-228">hello **First virtual network gateway** field value is automatically filled in because you are creating this connection from hello specified virtual network gateway.</span></span>
6. <span data-ttu-id="9c858-229">hello**第二個虛擬網路閘道**欄位是 hello 的 hello VNet 的虛擬網路閘道的 toocreate 的連接。</span><span class="sxs-lookup"><span data-stu-id="9c858-229">hello **Second virtual network gateway** field is hello virtual network gateway of hello VNet that you want toocreate a connection to.</span></span> <span data-ttu-id="9c858-230">按一下**選擇另一個虛擬網路閘道**tooopen hello**選擇虛擬網路閘道**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="9c858-230">Click **Choose another virtual network gateway** tooopen hello **Choose virtual network gateway** blade.</span></span>
   
    <span data-ttu-id="9c858-231">![新增連接](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/add_connection.png "新增連接")</span><span class="sxs-lookup"><span data-stu-id="9c858-231">![Add connection](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/add_connection.png "Add a connection")</span></span>
7. <span data-ttu-id="9c858-232">列出此刀鋒視窗檢視 hello 虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="9c858-232">View hello virtual network gateways that are listed on this blade.</span></span> <span data-ttu-id="9c858-233">請注意，只會列出您的訂用帳戶中的虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="9c858-233">Notice that only virtual network gateways that are in your subscription are listed.</span></span> <span data-ttu-id="9c858-234">如果您希望您的訂用帳戶的 tooconnect tooa 虛擬網路閘道，請使用 hello [PowerShell 文章](vpn-gateway-vnet-vnet-rm-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="9c858-234">If you want tooconnect tooa virtual network gateway that is not in your subscription, please use hello [PowerShell article](vpn-gateway-vnet-vnet-rm-ps.md).</span></span> 
8. <span data-ttu-id="9c858-235">按一下您想要 tooconnect hello 虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="9c858-235">Click hello virtual network gateway that you want tooconnect to.</span></span>
9. <span data-ttu-id="9c858-236">在 hello**共用金鑰**欄位中，輸入您的連線的共用的金鑰。</span><span class="sxs-lookup"><span data-stu-id="9c858-236">In hello **Shared key** field, type a shared key for your connection.</span></span> <span data-ttu-id="9c858-237">您可以產生此金鑰，或自行建立此金鑰。</span><span class="sxs-lookup"><span data-stu-id="9c858-237">You can generate or create this key yourself.</span></span> <span data-ttu-id="9c858-238">在 站對站連接 hello 您使用的索引鍵會是完全 hello 相同的內部部署裝置和虛擬網路閘道連接。</span><span class="sxs-lookup"><span data-stu-id="9c858-238">In a site-to-site connection, hello key you use would be exactly hello same for your on-premises device and your virtual network gateway connection.</span></span> <span data-ttu-id="9c858-239">hello 概念很類似，不同處在於連線 tooa VPN 裝置，而您要連接 tooanother 虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="9c858-239">hello concept is similar here, except that rather than connecting tooa VPN device, you are connecting tooanother virtual network gateway.</span></span>
   
    <span data-ttu-id="9c858-240">![共用金鑰](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/sharedkey.png "共用金鑰")</span><span class="sxs-lookup"><span data-stu-id="9c858-240">![Shared key](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/sharedkey.png "Shared key")</span></span>
10. <span data-ttu-id="9c858-241">按一下**確定**在 hello hello 刀鋒視窗 toosave 底部 您的變更。</span><span class="sxs-lookup"><span data-stu-id="9c858-241">Click **OK** at hello bottom of hello blade toosave your changes.</span></span>

## <span data-ttu-id="9c858-242"><a name="TestVNet4Connection"></a>8.設定 hello TestVNet4 連線</span><span class="sxs-lookup"><span data-stu-id="9c858-242"><a name="TestVNet4Connection"></a>8. Configure hello TestVNet4 connection</span></span>
<span data-ttu-id="9c858-243">接下來，從 TestVNet4 tooTestVNet1 建立連接。</span><span class="sxs-lookup"><span data-stu-id="9c858-243">Next, create a connection from TestVNet4 tooTestVNet1.</span></span> <span data-ttu-id="9c858-244">使用 hello 相同您使用從 TestVNet1 tooTestVNet4 toocreate hello 連接方法。</span><span class="sxs-lookup"><span data-stu-id="9c858-244">Use hello same method that you used toocreate hello connection from TestVNet1 tooTestVNet4.</span></span> <span data-ttu-id="9c858-245">請確定您使用 hello 相同的共用金鑰。</span><span class="sxs-lookup"><span data-stu-id="9c858-245">Make sure that you use hello same shared key.</span></span>

## <span data-ttu-id="9c858-246"><a name="VerifyConnection"></a>9.確認您的連接</span><span class="sxs-lookup"><span data-stu-id="9c858-246"><a name="VerifyConnection"></a>9. Verify your connection</span></span>
<span data-ttu-id="9c858-247">請確認 hello 連線。</span><span class="sxs-lookup"><span data-stu-id="9c858-247">Verify hello connection.</span></span> <span data-ttu-id="9c858-248">每個虛擬網路閘道，請勿 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="9c858-248">For each virtual network gateway, do hello following:</span></span>

1. <span data-ttu-id="9c858-249">找出 hello 虛擬網路閘道的 hello 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="9c858-249">Locate hello blade for hello virtual network gateway.</span></span> <span data-ttu-id="9c858-250">例如，**TestVNet4GW**。</span><span class="sxs-lookup"><span data-stu-id="9c858-250">For example, **TestVNet4GW**.</span></span> 
2. <span data-ttu-id="9c858-251">在 hello 虛擬網路閘道刀鋒視窗中，按一下 **連線**hello 虛擬網路閘道的 tooview hello 連線刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="9c858-251">On hello virtual network gateway blade, click **Connections** tooview hello connections blade for hello virtual network gateway.</span></span>

<span data-ttu-id="9c858-252">檢視 hello 連線，並確認 hello 狀態。</span><span class="sxs-lookup"><span data-stu-id="9c858-252">View hello connections and verify hello status.</span></span> <span data-ttu-id="9c858-253">Hello 連線建立之後，您會看到**Succeeded**和**Connected** hello 狀態值為。</span><span class="sxs-lookup"><span data-stu-id="9c858-253">Once hello connection is created, you will see **Succeeded** and **Connected** as hello Status values.</span></span>

<span data-ttu-id="9c858-254">![已成功](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/connected.png "已成功")</span><span class="sxs-lookup"><span data-stu-id="9c858-254">![Succeeded](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/connected.png "Succeeded")</span></span>

<span data-ttu-id="9c858-255">您可以按兩下每個連接，個別 tooview hello 連線的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="9c858-255">You can double-click each connection separately tooview more information about hello connection.</span></span>

<span data-ttu-id="9c858-256">![程式集](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/essentials.png "程式集")</span><span class="sxs-lookup"><span data-stu-id="9c858-256">![Essentials](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/essentials.png "Essentials")</span></span>

## <span data-ttu-id="9c858-257"><a name="faq"></a>VNet 對 VNet 常見問題集</span><span class="sxs-lookup"><span data-stu-id="9c858-257"><a name="faq"></a>VNet-to-VNet FAQ</span></span>
<span data-ttu-id="9c858-258">檢視 VNet 對 VNet 連線的其他資訊的 hello 常見問題集詳細資料。</span><span class="sxs-lookup"><span data-stu-id="9c858-258">View hello FAQ details for additional information about VNet-to-VNet connections.</span></span>

[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

## <a name="next-steps"></a><span data-ttu-id="9c858-259">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9c858-259">Next steps</span></span>
<span data-ttu-id="9c858-260">一旦完成您的連線，您可以將虛擬機器 tooyour 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="9c858-260">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="9c858-261">請參閱 hello[虛擬機器文件](https://docs.microsoft.com/azure/#pivot=services&panel=Compute)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="9c858-261">See hello [Virtual Machines documentation](https://docs.microsoft.com/azure/#pivot=services&panel=Compute) for more information.</span></span>
