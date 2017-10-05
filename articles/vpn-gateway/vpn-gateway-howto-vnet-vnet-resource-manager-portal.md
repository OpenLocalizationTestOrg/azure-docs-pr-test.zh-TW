---
title: "將 Azure 虛擬網路連接至另一個 VNet︰入口網站 | Microsoft Docs"
description: "使用 Resource Manager 和 Azure 入口網站建立 VNet 間的 VPN 閘道連接。"
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
ms.openlocfilehash: 0293495a9cbdab1fc797d9948e4cbb7759b1ba54
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="configure-a-vnet-to-vnet-vpn-gateway-connection-using-the-azure-portal"></a><span data-ttu-id="5d068-103">使用 Azure 入口網站設定 VNet 對 VNet 的 VPN 閘道連線</span><span class="sxs-lookup"><span data-stu-id="5d068-103">Configure a VNet-to-VNet VPN gateway connection using the Azure portal</span></span>

<span data-ttu-id="5d068-104">本文說明如何建立虛擬網路之間的VPN 閘道連線。</span><span class="sxs-lookup"><span data-stu-id="5d068-104">This article shows you how to create a VPN gateway connection between virtual networks.</span></span> <span data-ttu-id="5d068-105">虛擬網路可位於相同或不同的區域，以及來自相同或不同的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="5d068-105">The virtual networks can be in the same or different regions, and from the same or different subscriptions.</span></span> <span data-ttu-id="5d068-106">連線來自不同訂用帳戶的 VNet 時，訂用帳戶不需與相同的 Active Directory 租用戶相關聯。</span><span class="sxs-lookup"><span data-stu-id="5d068-106">When connecting VNets from different subscriptions, the subscriptions do not need to be associated with the same Active Directory tenant.</span></span> 

<span data-ttu-id="5d068-107">本文中的步驟適用於 Resource Manager 部署模型並使用 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="5d068-107">The steps in this article apply to the Resource Manager deployment model and use the Azure portal.</span></span> <span data-ttu-id="5d068-108">您也可從下列清單中選取不同的選項，以使用不同的部署工具或部署模型來建立此組態：</span><span class="sxs-lookup"><span data-stu-id="5d068-108">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="5d068-109">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="5d068-109">Azure portal</span></span>](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)
> * [<span data-ttu-id="5d068-110">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5d068-110">PowerShell</span></span>](vpn-gateway-vnet-vnet-rm-ps.md)
> * [<span data-ttu-id="5d068-111">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="5d068-111">Azure CLI</span></span>](vpn-gateway-howto-vnet-vnet-cli.md)
> * [<span data-ttu-id="5d068-112">Azure 入口網站 (傳統)</span><span class="sxs-lookup"><span data-stu-id="5d068-112">Azure portal (classic)</span></span>](vpn-gateway-howto-vnet-vnet-portal-classic.md)
> * [<span data-ttu-id="5d068-113">連線不同的部署模型 - Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="5d068-113">Connect different deployment models - Azure portal</span></span>](vpn-gateway-connect-different-deployment-models-portal.md)
> * [<span data-ttu-id="5d068-114">連線不同的部署模型 - PowerShell</span><span class="sxs-lookup"><span data-stu-id="5d068-114">Connect different deployment models - PowerShell</span></span>](vpn-gateway-connect-different-deployment-models-powershell.md)
>
>

![v2v 圖表](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/v2vrmps.png)

<span data-ttu-id="5d068-116">將虛擬網路連接至另一個虛擬網路 (VNet 對 VNet)，類似於將 VNet 連接至內部部署網站位置。</span><span class="sxs-lookup"><span data-stu-id="5d068-116">Connecting a virtual network to another virtual network (VNet-to-VNet) is similar to connecting a VNet to an on-premises site location.</span></span> <span data-ttu-id="5d068-117">這兩種連線類型都使用 VPN 閘道提供使用 IPsec/IKE 的安全通道。</span><span class="sxs-lookup"><span data-stu-id="5d068-117">Both connectivity types use a VPN gateway to provide a secure tunnel using IPsec/IKE.</span></span> <span data-ttu-id="5d068-118">如果您的 Vnet 位在相同區域，您可能會考慮使用 VNet 對等互連來進行連線。</span><span class="sxs-lookup"><span data-stu-id="5d068-118">If your VNets are in the same region, you may want to consider connecting them using VNet Peering.</span></span> <span data-ttu-id="5d068-119">VNet 對等互連不會使用 VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="5d068-119">VNet peering does not use a VPN gateway.</span></span> <span data-ttu-id="5d068-120">如需詳細資訊，請參閱 [VNet 對等互連](../virtual-network/virtual-network-peering-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="5d068-120">For more information, see [VNet peering](../virtual-network/virtual-network-peering-overview.md).</span></span>

<span data-ttu-id="5d068-121">您可以將 VNet 對 VNet 通訊與多站台組態結合。</span><span class="sxs-lookup"><span data-stu-id="5d068-121">VNet-to-VNet communication can be combined with multi-site configurations.</span></span> <span data-ttu-id="5d068-122">這可讓您建立使用內部虛擬網路連線結合跨單位連線的網路拓撲，如下圖所示：</span><span class="sxs-lookup"><span data-stu-id="5d068-122">This lets you establish network topologies that combine cross-premises connectivity with inter-virtual network connectivity, as shown in the following diagram:</span></span>

<span data-ttu-id="5d068-123">![關於連接](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/aboutconnections.png "關於連接")</span><span class="sxs-lookup"><span data-stu-id="5d068-123">![About connections](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/aboutconnections.png "About connections")</span></span>

### <a name="why-connect-virtual-networks"></a><span data-ttu-id="5d068-124">為什麼要連接虛擬網路？</span><span class="sxs-lookup"><span data-stu-id="5d068-124">Why connect virtual networks?</span></span>

<span data-ttu-id="5d068-125">針對下列原因，您可能希望連接虛擬網路：</span><span class="sxs-lookup"><span data-stu-id="5d068-125">You may want to connect virtual networks for the following reasons:</span></span>

* <span data-ttu-id="5d068-126">**跨區域的異地備援和異地目前狀態**</span><span class="sxs-lookup"><span data-stu-id="5d068-126">**Cross region geo-redundancy and geo-presence**</span></span>
  
  * <span data-ttu-id="5d068-127">您可以使用安全連線設定自己的異地複寫或同步處理，而不用查看網際網路對向端點。</span><span class="sxs-lookup"><span data-stu-id="5d068-127">You can set up your own geo-replication or synchronization with secure connectivity without going over Internet-facing endpoints.</span></span>
  * <span data-ttu-id="5d068-128">您可以使用 Azure 流量管理員和負載平衡器，利用異地備援跨多個 Azure 區域設定高度可用的工作負載。</span><span class="sxs-lookup"><span data-stu-id="5d068-128">With Azure Traffic Manager and Load Balancer, you can set up highly available workload with geo-redundancy across multiple Azure regions.</span></span> <span data-ttu-id="5d068-129">其中一個重要的範例就是使用分散在多個 Azure 區域的可用性群組來設定 SQL Always On。</span><span class="sxs-lookup"><span data-stu-id="5d068-129">One important example is to set up SQL Always On with Availability Groups spreading across multiple Azure regions.</span></span>
* <span data-ttu-id="5d068-130">**具有隔離或管理界限的區域性多層式應用程式**</span><span class="sxs-lookup"><span data-stu-id="5d068-130">**Regional multi-tier applications with isolation or administrative boundary**</span></span>
  
  * <span data-ttu-id="5d068-131">在相同區域中，您可以因為隔離或管理需求，設定將多層式應用程式與多個虛擬網路連線在一起。</span><span class="sxs-lookup"><span data-stu-id="5d068-131">Within the same region, you can set up multi-tier applications with multiple virtual networks connected together due to isolation or administrative requirements.</span></span>

<span data-ttu-id="5d068-132">如需 VNet 對 VNet 連線的詳細資訊，請參閱本文結尾處的 [VNet 對 VNet 常見問題集](#faq) 。</span><span class="sxs-lookup"><span data-stu-id="5d068-132">For more information about VNet-to-VNet connections, see the [VNet-to-VNet FAQ](#faq) at the end of this article.</span></span> <span data-ttu-id="5d068-133">請注意，如果您的 Vnet 位於不同的訂用帳戶中，就無法在入口網站中建立連線。</span><span class="sxs-lookup"><span data-stu-id="5d068-133">Note that if your VNets are in different subscriptions, you can't create the connection in the portal.</span></span> <span data-ttu-id="5d068-134">您可以使用 [PowerShell](vpn-gateway-vnet-vnet-rm-ps.md) 或 [CLI](vpn-gateway-howto-vnet-vnet-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="5d068-134">You can use [PowerShell](vpn-gateway-vnet-vnet-rm-ps.md) or [CLI](vpn-gateway-howto-vnet-vnet-cli.md).</span></span>

### <span data-ttu-id="5d068-135"><a name="values"></a>設定範例</span><span class="sxs-lookup"><span data-stu-id="5d068-135"><a name="values"></a>Example settings</span></span>

<span data-ttu-id="5d068-136">練習這些步驟時，您可以使用設定值範例。</span><span class="sxs-lookup"><span data-stu-id="5d068-136">When using these steps as an exercise, you can use the example settings values.</span></span> <span data-ttu-id="5d068-137">為了舉例說明，我們對每個 VNet 使用多個位址空間。</span><span class="sxs-lookup"><span data-stu-id="5d068-137">For example purposes, we use multiple address spaces for each VNet.</span></span> <span data-ttu-id="5d068-138">不過，VNet 對 VNet 組態不需要多個位址空間。</span><span class="sxs-lookup"><span data-stu-id="5d068-138">However, VNet-to-VNet configurations don't require multiple address spaces.</span></span>

<span data-ttu-id="5d068-139">**TestVNet1 的值︰**</span><span class="sxs-lookup"><span data-stu-id="5d068-139">**Values for TestVNet1:**</span></span>

* <span data-ttu-id="5d068-140">VNet 名稱︰TestVNet1</span><span class="sxs-lookup"><span data-stu-id="5d068-140">VNet Name: TestVNet1</span></span>
* <span data-ttu-id="5d068-141">位址空間︰10.11.0.0/16</span><span class="sxs-lookup"><span data-stu-id="5d068-141">Address space: 10.11.0.0/16</span></span>
  * <span data-ttu-id="5d068-142">子網路名稱：FrontEnd</span><span class="sxs-lookup"><span data-stu-id="5d068-142">Subnet name: FrontEnd</span></span>
  * <span data-ttu-id="5d068-143">子網路位址範圍：10.11.0.0/24</span><span class="sxs-lookup"><span data-stu-id="5d068-143">Subnet address range: 10.11.0.0/24</span></span>
* <span data-ttu-id="5d068-144">資源群組︰TestRG1</span><span class="sxs-lookup"><span data-stu-id="5d068-144">Resource Group: TestRG1</span></span>
* <span data-ttu-id="5d068-145">位置：美國東部</span><span class="sxs-lookup"><span data-stu-id="5d068-145">Location: East US</span></span>
* <span data-ttu-id="5d068-146">位址空間︰10.12.0.0/16</span><span class="sxs-lookup"><span data-stu-id="5d068-146">Address Space: 10.12.0.0/16</span></span>
  * <span data-ttu-id="5d068-147">子網路名稱：BackEnd</span><span class="sxs-lookup"><span data-stu-id="5d068-147">Subnet name: BackEnd</span></span>
  * <span data-ttu-id="5d068-148">子網路位址範圍︰10.12.0.0/24</span><span class="sxs-lookup"><span data-stu-id="5d068-148">Subnet address range: 10.12.0.0/24</span></span>
* <span data-ttu-id="5d068-149">閘道子網路名稱︰GatewaySubnet (這會在入口網站中自動填入)</span><span class="sxs-lookup"><span data-stu-id="5d068-149">Gateway Subnet name: GatewaySubnet (this will auto-fill in the portal)</span></span>
  * <span data-ttu-id="5d068-150">閘道子網路位址範圍︰10.11.255.0/27</span><span class="sxs-lookup"><span data-stu-id="5d068-150">Gateway Subnet address range: 10.11.255.0/27</span></span>
* <span data-ttu-id="5d068-151">DNS 伺服器︰使用您的 DNS 伺服器的 IP 位址</span><span class="sxs-lookup"><span data-stu-id="5d068-151">DNS Server: Use the IP address of your DNS Server</span></span>
* <span data-ttu-id="5d068-152">虛擬網路閘道名稱︰TestVNet1GW</span><span class="sxs-lookup"><span data-stu-id="5d068-152">Virtual Network Gateway Name: TestVNet1GW</span></span>
* <span data-ttu-id="5d068-153">閘道類型：VPN</span><span class="sxs-lookup"><span data-stu-id="5d068-153">Gateway Type: VPN</span></span>
* <span data-ttu-id="5d068-154">VPN 類型：路由式</span><span class="sxs-lookup"><span data-stu-id="5d068-154">VPN type: Route-based</span></span>
* <span data-ttu-id="5d068-155">SKU︰選取您想要使用的閘道 SKU</span><span class="sxs-lookup"><span data-stu-id="5d068-155">SKU: Select the Gateway SKU you want to use</span></span>
* <span data-ttu-id="5d068-156">公用 IP 位址名稱︰TestVNet1GWIP</span><span class="sxs-lookup"><span data-stu-id="5d068-156">Public IP address name: TestVNet1GWIP</span></span>
* <span data-ttu-id="5d068-157">連接值︰</span><span class="sxs-lookup"><span data-stu-id="5d068-157">Connection values:</span></span>
  * <span data-ttu-id="5d068-158">名稱︰TestVNet1toTestVNet4</span><span class="sxs-lookup"><span data-stu-id="5d068-158">Name: TestVNet1toTestVNet4</span></span>
  * <span data-ttu-id="5d068-159">共用金鑰︰您可以自行建立共用金鑰。</span><span class="sxs-lookup"><span data-stu-id="5d068-159">Shared key: You can create the shared key yourself.</span></span> <span data-ttu-id="5d068-160">此範例中，我們將使用 abc123。</span><span class="sxs-lookup"><span data-stu-id="5d068-160">For this example, we'll use abc123.</span></span> <span data-ttu-id="5d068-161">重點是當您建立 VNet 之間的連接時，此值必須符合。</span><span class="sxs-lookup"><span data-stu-id="5d068-161">The important thing is that when you create the connection between the VNets, the value must match.</span></span>

<span data-ttu-id="5d068-162">**TestVNet4 的值︰**</span><span class="sxs-lookup"><span data-stu-id="5d068-162">**Values for TestVNet4:**</span></span>

* <span data-ttu-id="5d068-163">VNet 名稱︰TestVNet4</span><span class="sxs-lookup"><span data-stu-id="5d068-163">VNet Name: TestVNet4</span></span>
* <span data-ttu-id="5d068-164">位址空間︰10.41.0.0/16</span><span class="sxs-lookup"><span data-stu-id="5d068-164">Address space: 10.41.0.0/16</span></span>
  * <span data-ttu-id="5d068-165">子網路名稱：FrontEnd</span><span class="sxs-lookup"><span data-stu-id="5d068-165">Subnet name: FrontEnd</span></span>
  * <span data-ttu-id="5d068-166">子網路位址範圍︰10.41.0.0/24</span><span class="sxs-lookup"><span data-stu-id="5d068-166">Subnet address range: 10.41.0.0/24</span></span>
* <span data-ttu-id="5d068-167">資源群組︰TestRG1</span><span class="sxs-lookup"><span data-stu-id="5d068-167">Resource Group: TestRG1</span></span>
* <span data-ttu-id="5d068-168">位置：美國西部</span><span class="sxs-lookup"><span data-stu-id="5d068-168">Location: West US</span></span>
* <span data-ttu-id="5d068-169">位址空間︰10.42.0.0/16</span><span class="sxs-lookup"><span data-stu-id="5d068-169">Address Space: 10.42.0.0/16</span></span>
  * <span data-ttu-id="5d068-170">子網路名稱：BackEnd</span><span class="sxs-lookup"><span data-stu-id="5d068-170">Subnet name: BackEnd</span></span>
  * <span data-ttu-id="5d068-171">子網路位址範圍︰10.42.0.0/24</span><span class="sxs-lookup"><span data-stu-id="5d068-171">Subnet address range: 10.42.0.0/24</span></span>
* <span data-ttu-id="5d068-172">閘道子網路名稱︰GatewaySubnet (這會在入口網站中自動填入)</span><span class="sxs-lookup"><span data-stu-id="5d068-172">GatewaySubnet name: GatewaySubnet (this will auto-fill in the portal)</span></span>
  * <span data-ttu-id="5d068-173">閘道子網路位址範圍︰10.41.255.0/27</span><span class="sxs-lookup"><span data-stu-id="5d068-173">GatewaySubnet address range: 10.41.255.0/27</span></span>
* <span data-ttu-id="5d068-174">DNS 伺服器︰使用您的 DNS 伺服器的 IP 位址</span><span class="sxs-lookup"><span data-stu-id="5d068-174">DNS Server: Use the IP address of your DNS Server</span></span>
* <span data-ttu-id="5d068-175">虛擬網路閘道名稱︰TestVNet4GW</span><span class="sxs-lookup"><span data-stu-id="5d068-175">Virtual Network Gateway Name: TestVNet4GW</span></span>
* <span data-ttu-id="5d068-176">閘道類型：VPN</span><span class="sxs-lookup"><span data-stu-id="5d068-176">Gateway Type: VPN</span></span>
* <span data-ttu-id="5d068-177">VPN 類型：路由式</span><span class="sxs-lookup"><span data-stu-id="5d068-177">VPN type: Route-based</span></span>
* <span data-ttu-id="5d068-178">SKU︰選取您想要使用的閘道 SKU</span><span class="sxs-lookup"><span data-stu-id="5d068-178">SKU: Select the Gateway SKU you want to use</span></span>
* <span data-ttu-id="5d068-179">公用 IP 位址名稱︰TestVNet4GWIP</span><span class="sxs-lookup"><span data-stu-id="5d068-179">Public IP address name: TestVNet4GWIP</span></span>
* <span data-ttu-id="5d068-180">連接值︰</span><span class="sxs-lookup"><span data-stu-id="5d068-180">Connection values:</span></span>
  * <span data-ttu-id="5d068-181">名稱︰TestVNet4toTestVNet1</span><span class="sxs-lookup"><span data-stu-id="5d068-181">Name: TestVNet4toTestVNet1</span></span>
  * <span data-ttu-id="5d068-182">共用金鑰︰您可以自行建立共用金鑰。</span><span class="sxs-lookup"><span data-stu-id="5d068-182">Shared key: You can create the shared key yourself.</span></span> <span data-ttu-id="5d068-183">此範例中，我們將使用 abc123。</span><span class="sxs-lookup"><span data-stu-id="5d068-183">For this example, we'll use abc123.</span></span> <span data-ttu-id="5d068-184">重點是當您建立 VNet 之間的連接時，此值必須符合。</span><span class="sxs-lookup"><span data-stu-id="5d068-184">The important thing is that when you create the connection between the VNets, the value must match.</span></span>

## <span data-ttu-id="5d068-185"><a name="CreatVNet"></a>1.建立及設定 TestVNet1</span><span class="sxs-lookup"><span data-stu-id="5d068-185"><a name="CreatVNet"></a>1. Create and configure TestVNet1</span></span>
<span data-ttu-id="5d068-186">如果您已經有 VNet，請驗證設定是否與您的 VPN 閘道設計相容。</span><span class="sxs-lookup"><span data-stu-id="5d068-186">If you already have a VNet, verify that the settings are compatible with your VPN gateway design.</span></span> <span data-ttu-id="5d068-187">請特別注意任何可能與其他網路重疊的子網路。</span><span class="sxs-lookup"><span data-stu-id="5d068-187">Pay particular attention to any subnets that may overlap with other networks.</span></span> <span data-ttu-id="5d068-188">如果有重疊的子網路，您的連線便無法正常運作。</span><span class="sxs-lookup"><span data-stu-id="5d068-188">If you have overlapping subnets, your connection won't work properly.</span></span> <span data-ttu-id="5d068-189">如果您的 VNet 已設定為正確的設定，即可開始執行 [指定 DNS 伺服器](#dns) 一節中的步驟。</span><span class="sxs-lookup"><span data-stu-id="5d068-189">If your VNet is configured with the correct settings, you can begin the steps in the [Specify a DNS server](#dns) section.</span></span>

### <a name="to-create-a-virtual-network"></a><span data-ttu-id="5d068-190">建立虛擬網路</span><span class="sxs-lookup"><span data-stu-id="5d068-190">To create a virtual network</span></span>
[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-basic-vnet-rm-portal-include.md)]

## <span data-ttu-id="5d068-191"><a name="subnets"></a>2.新增其他位址空間和建立子網路</span><span class="sxs-lookup"><span data-stu-id="5d068-191"><a name="subnets"></a>2. Add additional address space and create subnets</span></span>
<span data-ttu-id="5d068-192">建立 VNet 之後，您可以新增其他位址空間和建立子網路。</span><span class="sxs-lookup"><span data-stu-id="5d068-192">You can add additional address space and create subnets once your VNet has been created.</span></span>

[!INCLUDE [vpn-gateway-additional-address-space](../../includes/vpn-gateway-additional-address-space-include.md)]

## <span data-ttu-id="5d068-193"><a name="gatewaysubnet"></a>3.建立閘道子網路</span><span class="sxs-lookup"><span data-stu-id="5d068-193"><a name="gatewaysubnet"></a>3. Create a gateway subnet</span></span>
<span data-ttu-id="5d068-194">將虛擬網路連接到閘道之前，您必須先建立虛擬網路要連接的閘道子網路。</span><span class="sxs-lookup"><span data-stu-id="5d068-194">Before connecting your virtual network to a gateway, you first need to create the gateway subnet for the virtual network to which you want to connect.</span></span> <span data-ttu-id="5d068-195">可能的話，最好使用 /28 或 /27 的 CIDR 區塊建立閘道子網路，以便提供足以容納未來其他組態需求的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="5d068-195">If possible, it's best to create a gateway subnet using a CIDR block of /28 or /27 in order to provide enough IP addresses to accommodate additional future configuration requirements.</span></span>

<span data-ttu-id="5d068-196">如果您要練習建立此組態，請在建立閘道子網路時參考這些[範例值](#values) 。</span><span class="sxs-lookup"><span data-stu-id="5d068-196">If you are creating this configuration as an exercise, refer to these [Example settings](#values) when creating your gateway subnet.</span></span>

[!INCLUDE [vpn-gateway-no-nsg](../../includes/vpn-gateway-no-nsg-include.md)]

### <a name="to-create-a-gateway-subnet"></a><span data-ttu-id="5d068-197">建立閘道子網路</span><span class="sxs-lookup"><span data-stu-id="5d068-197">To create a gateway subnet</span></span>
[!INCLUDE [vpn-gateway-add-gwsubnet-rm-portal](../../includes/vpn-gateway-add-gwsubnet-rm-portal-include.md)]

## <span data-ttu-id="5d068-198"><a name="dns"></a>4.指定 DNS 伺服器 (選擇性)</span><span class="sxs-lookup"><span data-stu-id="5d068-198"><a name="dns"></a>4. Specify a DNS server (optional)</span></span>
<span data-ttu-id="5d068-199">VNet 對 VNet 連線不需要 DNS。</span><span class="sxs-lookup"><span data-stu-id="5d068-199">DNS is not required for VNet-to-VNet connections.</span></span> <span data-ttu-id="5d068-200">不過，如果您想要對部署至虛擬網路的資源進行名稱解析，則應指定 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="5d068-200">However, if you want to have name resolution for resources that are deployed to your virtual network, you should specify a DNS server.</span></span> <span data-ttu-id="5d068-201">此設定可讓您指定要用於此虛擬網路之名稱解析的 DNS 伺服器服務。</span><span class="sxs-lookup"><span data-stu-id="5d068-201">This setting lets you specify the DNS server that you want to use for name resolution for this virtual network.</span></span> <span data-ttu-id="5d068-202">它不會建立 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="5d068-202">It does not create a DNS server.</span></span>

[!INCLUDE [vpn-gateway-add-dns-rm-portal](../../includes/vpn-gateway-add-dns-rm-portal-include.md)]

## <span data-ttu-id="5d068-203"><a name="VNetGateway"></a>5.建立虛擬網路閘道</span><span class="sxs-lookup"><span data-stu-id="5d068-203"><a name="VNetGateway"></a>5. Create a virtual network gateway</span></span>
<span data-ttu-id="5d068-204">此步驟將帶您建立 VNet 的虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="5d068-204">In this step, you create the virtual network gateway for your VNet.</span></span> <span data-ttu-id="5d068-205">建立閘道通常可能需要 45 分鐘或更久，視選取的閘道 SKU 而定。</span><span class="sxs-lookup"><span data-stu-id="5d068-205">Creating a gateway can often take 45 minutes or more, depending on the selected gateway SKU.</span></span> <span data-ttu-id="5d068-206">如果您要練習建立此組態，您可以參考[範例設定](#values)。</span><span class="sxs-lookup"><span data-stu-id="5d068-206">If you are creating this configuration as an exercise, you can refer to the [Example settings](#values).</span></span>

### <a name="to-create-a-virtual-network-gateway"></a><span data-ttu-id="5d068-207">建立虛擬網路閘道</span><span class="sxs-lookup"><span data-stu-id="5d068-207">To create a virtual network gateway</span></span>
[!INCLUDE [vpn-gateway-add-gw-rm-portal](../../includes/vpn-gateway-add-gw-rm-portal-include.md)]

## <span data-ttu-id="5d068-208"><a name="CreateTestVNet4"></a>6.建立及設定 TestVNet4</span><span class="sxs-lookup"><span data-stu-id="5d068-208"><a name="CreateTestVNet4"></a>6. Create and configure TestVNet4</span></span>
<span data-ttu-id="5d068-209">設定 TestVNet1 之後，請重複先前步驟來建立 TestVNet4，並換成 TestVNet4 的值。</span><span class="sxs-lookup"><span data-stu-id="5d068-209">Once you've configured TestVNet1, create TestVNet4 by repeating the previous steps, replacing the values with those of TestVNet4.</span></span> <span data-ttu-id="5d068-210">您不需要等到 TestVNet1 的虛擬網路閘道建立完成後才設定 TestVNet4。</span><span class="sxs-lookup"><span data-stu-id="5d068-210">You don't need to wait until the virtual network gateway for TestVNet1 has finished creating before configuring TestVNet4.</span></span> <span data-ttu-id="5d068-211">如果您使用自己的值，請確定位址空間沒有與任何您想要連接的 VNet 重疊。</span><span class="sxs-lookup"><span data-stu-id="5d068-211">If you are using your own values, make sure that the address spaces don't overlap with any of the VNets that you want to connect to.</span></span>

## <span data-ttu-id="5d068-212"><a name="TestVNet1Connection"></a>7.設定 TestVNet1 連接</span><span class="sxs-lookup"><span data-stu-id="5d068-212"><a name="TestVNet1Connection"></a>7. Configure the TestVNet1 connection</span></span>
<span data-ttu-id="5d068-213">當 TestVNet1 和 TestVNet4 的虛擬網路閘道完成後，您可以建立虛擬網路閘道連接。</span><span class="sxs-lookup"><span data-stu-id="5d068-213">When the virtual network gateways for both TestVNet1 and TestVNet4 have completed, you can create your virtual network gateway connections.</span></span> <span data-ttu-id="5d068-214">本節中，您將建立從 VNet1 到 VNet4 的連接。</span><span class="sxs-lookup"><span data-stu-id="5d068-214">In this section, you will create a connection from VNet1 to VNet4.</span></span> <span data-ttu-id="5d068-215">這些步驟只適用於相同的訂用帳戶中的 VNet。</span><span class="sxs-lookup"><span data-stu-id="5d068-215">These steps work only for VNets in the same subscription.</span></span> <span data-ttu-id="5d068-216">如果您的 VNet 位於不同的訂用帳戶中，則必須使用 PowerShell 來進行連線。</span><span class="sxs-lookup"><span data-stu-id="5d068-216">If your VNets are in different subscriptions, you must use PowerShell to make the connection.</span></span> <span data-ttu-id="5d068-217">請參閱 [PowerShell](vpn-gateway-vnet-vnet-rm-ps.md) 文件。</span><span class="sxs-lookup"><span data-stu-id="5d068-217">See the [PowerShell](vpn-gateway-vnet-vnet-rm-ps.md) article.</span></span>

1. <span data-ttu-id="5d068-218">在 [所有資源] 中，瀏覽至 VNet 的虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="5d068-218">In **All resources**, navigate to the virtual network gateway for your VNet.</span></span> <span data-ttu-id="5d068-219">例如，**TestVNet1GW**。</span><span class="sxs-lookup"><span data-stu-id="5d068-219">For example, **TestVNet1GW**.</span></span> <span data-ttu-id="5d068-220">按一下 [TestVNet1GW] 以開啟 [虛擬網路閘道] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="5d068-220">Click **TestVNet1GW** to open the virtual network gateway blade.</span></span>
   
    <span data-ttu-id="5d068-221">![連接刀鋒視窗](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/settings_connection.png "連接刀鋒視窗e")</span><span class="sxs-lookup"><span data-stu-id="5d068-221">![Connections blade](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/settings_connection.png "Connections blade")</span></span>
2. <span data-ttu-id="5d068-222">按一下 [+新增] 以開啟 [新增連接] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="5d068-222">Click **+Add** to open the **Add connection** blade.</span></span>
3. <span data-ttu-id="5d068-223">在 [新增連接] 刀鋒視窗的 [名稱] 欄位中，輸入連接名稱。</span><span class="sxs-lookup"><span data-stu-id="5d068-223">On the **Add connection** blade, in the name field, type a name for your connection.</span></span> <span data-ttu-id="5d068-224">例如，**TestVNet1toTestVNet4**。</span><span class="sxs-lookup"><span data-stu-id="5d068-224">For example, **TestVNet1toTestVNet4**.</span></span>
   
    <span data-ttu-id="5d068-225">![連接名稱](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/v1tov4.png "連接名稱")</span><span class="sxs-lookup"><span data-stu-id="5d068-225">![Connection name](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/v1tov4.png "Connection name")</span></span>
4. <span data-ttu-id="5d068-226">在 [連線類型] 中，</span><span class="sxs-lookup"><span data-stu-id="5d068-226">For **Connection type**.</span></span> <span data-ttu-id="5d068-227">從下拉式清單選取 [VNet 對 VNet]。</span><span class="sxs-lookup"><span data-stu-id="5d068-227">select **VNet-to-VNet** from the dropdown.</span></span>
5. <span data-ttu-id="5d068-228">因為您是從指定的虛擬網路閘道建立此連接，將會自動填入 [第一個虛擬網路閘道] 欄位值。</span><span class="sxs-lookup"><span data-stu-id="5d068-228">The **First virtual network gateway** field value is automatically filled in because you are creating this connection from the specified virtual network gateway.</span></span>
6. <span data-ttu-id="5d068-229">[第二個虛擬網路閘道] 欄位是您想要建立連接的 VNet 的虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="5d068-229">The **Second virtual network gateway** field is the virtual network gateway of the VNet that you want to create a connection to.</span></span> <span data-ttu-id="5d068-230">按一下 [選擇另一個虛擬網路閘道]，以開啟 [選擇虛擬網路閘道] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="5d068-230">Click **Choose another virtual network gateway** to open the **Choose virtual network gateway** blade.</span></span>
   
    <span data-ttu-id="5d068-231">![新增連接](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/add_connection.png "新增連接")</span><span class="sxs-lookup"><span data-stu-id="5d068-231">![Add connection](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/add_connection.png "Add a connection")</span></span>
7. <span data-ttu-id="5d068-232">檢視此刀鋒視窗上列出的虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="5d068-232">View the virtual network gateways that are listed on this blade.</span></span> <span data-ttu-id="5d068-233">請注意，只會列出您的訂用帳戶中的虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="5d068-233">Notice that only virtual network gateways that are in your subscription are listed.</span></span> <span data-ttu-id="5d068-234">如果想要連接的虛擬網路閘道不在您的訂用帳戶中，請參閱 [PowerShell 文章](vpn-gateway-vnet-vnet-rm-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="5d068-234">If you want to connect to a virtual network gateway that is not in your subscription, please use the [PowerShell article](vpn-gateway-vnet-vnet-rm-ps.md).</span></span> 
8. <span data-ttu-id="5d068-235">按一下您想要連接虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="5d068-235">Click the virtual network gateway that you want to connect to.</span></span>
9. <span data-ttu-id="5d068-236">在 [共用金鑰] 欄位中，輸入連接的共用金鑰。</span><span class="sxs-lookup"><span data-stu-id="5d068-236">In the **Shared key** field, type a shared key for your connection.</span></span> <span data-ttu-id="5d068-237">您可以產生此金鑰，或自行建立此金鑰。</span><span class="sxs-lookup"><span data-stu-id="5d068-237">You can generate or create this key yourself.</span></span> <span data-ttu-id="5d068-238">在網站間連接中，您用於內部部署裝置與虛擬網路閘道連接的金鑰完全相同。</span><span class="sxs-lookup"><span data-stu-id="5d068-238">In a site-to-site connection, the key you use would be exactly the same for your on-premises device and your virtual network gateway connection.</span></span> <span data-ttu-id="5d068-239">此處的概念類似，差別在於是連接到另一個虛擬網路閘道，而不是連接到 VPN 裝置。</span><span class="sxs-lookup"><span data-stu-id="5d068-239">The concept is similar here, except that rather than connecting to a VPN device, you are connecting to another virtual network gateway.</span></span>
   
    <span data-ttu-id="5d068-240">![共用金鑰](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/sharedkey.png "共用金鑰")</span><span class="sxs-lookup"><span data-stu-id="5d068-240">![Shared key](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/sharedkey.png "Shared key")</span></span>
10. <span data-ttu-id="5d068-241">按一下刀鋒視窗底部的 [確定] 以儲存變更。</span><span class="sxs-lookup"><span data-stu-id="5d068-241">Click **OK** at the bottom of the blade to save your changes.</span></span>

## <span data-ttu-id="5d068-242"><a name="TestVNet4Connection"></a>8.設定 TestVNet4 連接</span><span class="sxs-lookup"><span data-stu-id="5d068-242"><a name="TestVNet4Connection"></a>8. Configure the TestVNet4 connection</span></span>
<span data-ttu-id="5d068-243">接下來，建立從 TestVNet4 至 TestVNet1 的連接。</span><span class="sxs-lookup"><span data-stu-id="5d068-243">Next, create a connection from TestVNet4 to TestVNet1.</span></span> <span data-ttu-id="5d068-244">像就您建立從 TestVNet1 至 TestVNet4 的連接一樣，使用相同的方法。</span><span class="sxs-lookup"><span data-stu-id="5d068-244">Use the same method that you used to create the connection from TestVNet1 to TestVNet4.</span></span> <span data-ttu-id="5d068-245">請確定您使用相同的共用金鑰。</span><span class="sxs-lookup"><span data-stu-id="5d068-245">Make sure that you use the same shared key.</span></span>

## <span data-ttu-id="5d068-246"><a name="VerifyConnection"></a>9.確認您的連接</span><span class="sxs-lookup"><span data-stu-id="5d068-246"><a name="VerifyConnection"></a>9. Verify your connection</span></span>
<span data-ttu-id="5d068-247">確認連接。</span><span class="sxs-lookup"><span data-stu-id="5d068-247">Verify the connection.</span></span> <span data-ttu-id="5d068-248">對每個虛擬網路閘道，執行下列作業︰</span><span class="sxs-lookup"><span data-stu-id="5d068-248">For each virtual network gateway, do the following:</span></span>

1. <span data-ttu-id="5d068-249">找出虛擬網路閘道的刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="5d068-249">Locate the blade for the virtual network gateway.</span></span> <span data-ttu-id="5d068-250">例如，**TestVNet4GW**。</span><span class="sxs-lookup"><span data-stu-id="5d068-250">For example, **TestVNet4GW**.</span></span> 
2. <span data-ttu-id="5d068-251">在虛擬網路閘道刀鋒視窗中，按一下 [連接]，以檢視虛擬網路閘道的連接刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="5d068-251">On the virtual network gateway blade, click **Connections** to view the connections blade for the virtual network gateway.</span></span>

<span data-ttu-id="5d068-252">檢視連接並確認狀態。</span><span class="sxs-lookup"><span data-stu-id="5d068-252">View the connections and verify the status.</span></span> <span data-ttu-id="5d068-253">一旦建立連接，您會看到 [狀態] 值為 [成功] 和 [已連接]。</span><span class="sxs-lookup"><span data-stu-id="5d068-253">Once the connection is created, you will see **Succeeded** and **Connected** as the Status values.</span></span>

<span data-ttu-id="5d068-254">![已成功](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/connected.png "已成功")</span><span class="sxs-lookup"><span data-stu-id="5d068-254">![Succeeded](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/connected.png "Succeeded")</span></span>

<span data-ttu-id="5d068-255">您可以分別按兩下每個連接，以檢視該連接的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="5d068-255">You can double-click each connection separately to view more information about the connection.</span></span>

<span data-ttu-id="5d068-256">![程式集](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/essentials.png "程式集")</span><span class="sxs-lookup"><span data-stu-id="5d068-256">![Essentials](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/essentials.png "Essentials")</span></span>

## <span data-ttu-id="5d068-257"><a name="faq"></a>VNet 對 VNet 常見問題集</span><span class="sxs-lookup"><span data-stu-id="5d068-257"><a name="faq"></a>VNet-to-VNet FAQ</span></span>
<span data-ttu-id="5d068-258">檢視常見問題集詳細資料以取得 VNet 對 VNet 連線的其他資訊。</span><span class="sxs-lookup"><span data-stu-id="5d068-258">View the FAQ details for additional information about VNet-to-VNet connections.</span></span>

[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

## <a name="next-steps"></a><span data-ttu-id="5d068-259">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5d068-259">Next steps</span></span>
<span data-ttu-id="5d068-260">一旦完成您的連接，就可以將虛擬機器加入您的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="5d068-260">Once your connection is complete, you can add virtual machines to your virtual networks.</span></span> <span data-ttu-id="5d068-261">如需詳細資訊，請參閱 [虛擬機器文件](https://docs.microsoft.com/azure/#pivot=services&panel=Compute) 。</span><span class="sxs-lookup"><span data-stu-id="5d068-261">See the [Virtual Machines documentation](https://docs.microsoft.com/azure/#pivot=services&panel=Compute) for more information.</span></span>
