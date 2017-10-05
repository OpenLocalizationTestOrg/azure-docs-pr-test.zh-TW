---
title: "將內部部署網路連接至 Azure 虛擬網路：站對站 VPN：入口網站 | Microsoft Docs"
description: "透過公用網際網路建立從內部部署網路至 Azure 虛擬網路之 IPsec 連線的步驟。 這些步驟可協助您使用入口網站建立跨單位的站對站 VPN 閘道連線。"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 827a4db7-7fa5-4eaf-b7e1-e1518c51c815
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/02/2017
ms.author: cherylmc
ms.openlocfilehash: 0dec0d3744f76a06313928197f3a5229290ba32b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-site-to-site-connection-in-the-azure-portal"></a><span data-ttu-id="ca136-104">在 Azure 入口網站中建立站對站連線</span><span class="sxs-lookup"><span data-stu-id="ca136-104">Create a Site-to-Site connection in the Azure portal</span></span>

<span data-ttu-id="ca136-105">本文說明如何使用 Azure 入口網站來建立從內部部署網路到 VNet 的站對站 VPN 閘道連線。</span><span class="sxs-lookup"><span data-stu-id="ca136-105">This article shows you how to use the Azure portal to create a Site-to-Site VPN gateway connection from your on-premises network to the VNet.</span></span> <span data-ttu-id="ca136-106">本文中的步驟適用於 Resource Manager 部署模型。</span><span class="sxs-lookup"><span data-stu-id="ca136-106">The steps in this article apply to the Resource Manager deployment model.</span></span> <span data-ttu-id="ca136-107">您也可從下列清單中選取不同的選項，以使用不同的部署工具或部署模型來建立此組態：</span><span class="sxs-lookup"><span data-stu-id="ca136-107">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="ca136-108">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="ca136-108">Azure portal</span></span>](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="ca136-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ca136-109">PowerShell</span></span>](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [<span data-ttu-id="ca136-110">CLI</span><span class="sxs-lookup"><span data-stu-id="ca136-110">CLI</span></span>](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [<span data-ttu-id="ca136-111">Azure 入口網站 (傳統)</span><span class="sxs-lookup"><span data-stu-id="ca136-111">Azure portal (classic)</span></span>](vpn-gateway-howto-site-to-site-classic-portal.md)
> 
>

<span data-ttu-id="ca136-112">站對站 VPN 閘道連線可用來透過 IPsec/IKE (IKEv1 或 IKEv2) VPN 通道，將內部部署網路連線到 Azure 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="ca136-112">A Site-to-Site VPN gateway connection is used to connect your on-premises network to an Azure virtual network over an IPsec/IKE (IKEv1 or IKEv2) VPN tunnel.</span></span> <span data-ttu-id="ca136-113">此類型的連線需要位於內部部署的 VPN 裝置，且您已對該裝置指派對外開放的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="ca136-113">This type of connection requires a VPN device located on-premises that has an externally facing public IP address assigned to it.</span></span> <span data-ttu-id="ca136-114">如需 VPN 閘道的詳細資訊，請參閱[關於 VPN 閘道](vpn-gateway-about-vpngateways.md)。</span><span class="sxs-lookup"><span data-stu-id="ca136-114">For more information about VPN gateways, see [About VPN gateway](vpn-gateway-about-vpngateways.md).</span></span>

![站對站 VPN 閘道跨單位連線圖表](./media/vpn-gateway-howto-site-to-site-resource-manager-portal/site-to-site-diagram.png)

## <a name="before-you-begin"></a><span data-ttu-id="ca136-116">開始之前</span><span class="sxs-lookup"><span data-stu-id="ca136-116">Before you begin</span></span>

<span data-ttu-id="ca136-117">在開始設定之前，請確認您已符合下列條件：</span><span class="sxs-lookup"><span data-stu-id="ca136-117">Verify that you have met the following criteria before beginning your configuration:</span></span>

* <span data-ttu-id="ca136-118">確定您有相容的 VPN 裝置以及能夠對其進行設定的人員。</span><span class="sxs-lookup"><span data-stu-id="ca136-118">Make sure you have a compatible VPN device and someone who is able to configure it.</span></span> <span data-ttu-id="ca136-119">如需相容 VPN 裝置和裝置組態的詳細資訊，請參閱[關於 VPN 裝置](vpn-gateway-about-vpn-devices.md)。</span><span class="sxs-lookup"><span data-stu-id="ca136-119">For more information about compatible VPN devices and device configuration, see [About VPN Devices](vpn-gateway-about-vpn-devices.md).</span></span>
* <span data-ttu-id="ca136-120">確認您的 VPN 裝置有對外開放的公用 IPv4 位址。</span><span class="sxs-lookup"><span data-stu-id="ca136-120">Verify that you have an externally facing public IPv4 address for your VPN device.</span></span> <span data-ttu-id="ca136-121">此 IP 位址不能位於 NAT 後方。</span><span class="sxs-lookup"><span data-stu-id="ca136-121">This IP address cannot be located behind a NAT.</span></span>
* <span data-ttu-id="ca136-122">如果您不熟悉位於內部部署網路組態的 IP 位址範圍，您需要與能夠提供那些詳細資料的人協調。</span><span class="sxs-lookup"><span data-stu-id="ca136-122">If you are unfamiliar with the IP address ranges located in your on-premises network configuration, you need to coordinate with someone who can provide those details for you.</span></span> <span data-ttu-id="ca136-123">當您建立此組態時，您必須指定 IP 位址範圍的首碼，以供 Azure 路由傳送至您的內部部署位置。</span><span class="sxs-lookup"><span data-stu-id="ca136-123">When you create this configuration, you must specify the IP address range prefixes that Azure will route to your on-premises location.</span></span> <span data-ttu-id="ca136-124">內部部署網路的子網路皆不得與您所要連線的虛擬網路子網路重疊。</span><span class="sxs-lookup"><span data-stu-id="ca136-124">None of the subnets of your on-premises network can over lap with the virtual network subnets that you want to connect to.</span></span> 

### <span data-ttu-id="ca136-125"><a name="values"></a>範例值</span><span class="sxs-lookup"><span data-stu-id="ca136-125"><a name="values"></a>Example values</span></span>

<span data-ttu-id="ca136-126">本文的範例使用下列值。</span><span class="sxs-lookup"><span data-stu-id="ca136-126">The examples in this article use the following values.</span></span> <span data-ttu-id="ca136-127">您可以使用這些值來建立測試環境，或參考這些值，進一步了解本文中的範例。</span><span class="sxs-lookup"><span data-stu-id="ca136-127">You can use these values to create a test environment, or refer to them to better understand the examples in this article.</span></span>

* <span data-ttu-id="ca136-128">**VNet 名稱︰**TestVNet1</span><span class="sxs-lookup"><span data-stu-id="ca136-128">**VNet Name:** TestVNet1</span></span>
* <span data-ttu-id="ca136-129">**位址空間：**</span><span class="sxs-lookup"><span data-stu-id="ca136-129">**Address Space:**</span></span> 
  * <span data-ttu-id="ca136-130">10.11.0.0/16</span><span class="sxs-lookup"><span data-stu-id="ca136-130">10.11.0.0/16</span></span>
  * <span data-ttu-id="ca136-131">10.12.0.0/16 (對此練習是選擇性的)</span><span class="sxs-lookup"><span data-stu-id="ca136-131">10.12.0.0/16 (optional for this exercise)</span></span>
* <span data-ttu-id="ca136-132">**子網路：**</span><span class="sxs-lookup"><span data-stu-id="ca136-132">**Subnets:**</span></span>
  * <span data-ttu-id="ca136-133">FrontEnd：10.11.0.0/24</span><span class="sxs-lookup"><span data-stu-id="ca136-133">FrontEnd: 10.11.0.0/24</span></span>
  * <span data-ttu-id="ca136-134">BackEnd：10.12.0.0/24 (對此練習是選擇性的)</span><span class="sxs-lookup"><span data-stu-id="ca136-134">BackEnd: 10.12.0.0/24 (optional for this exercise)</span></span>
* <span data-ttu-id="ca136-135">**GatewaySubnet：**10.11.255.0/27</span><span class="sxs-lookup"><span data-stu-id="ca136-135">**GatewaySubnet:** 10.11.255.0/27</span></span>
* <span data-ttu-id="ca136-136">**資源群組︰**TestRG1</span><span class="sxs-lookup"><span data-stu-id="ca136-136">**Resource Group:** TestRG1</span></span>
* <span data-ttu-id="ca136-137">**位置：**美國東部</span><span class="sxs-lookup"><span data-stu-id="ca136-137">**Location:** East US</span></span>
* <span data-ttu-id="ca136-138">**DNS 伺服器：**選擇性。</span><span class="sxs-lookup"><span data-stu-id="ca136-138">**DNS Server:** Optional.</span></span> <span data-ttu-id="ca136-139">DNS 伺服器的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="ca136-139">The IP address of your DNS server.</span></span>
* <span data-ttu-id="ca136-140">**虛擬網路閘道名稱：**VNet1GW</span><span class="sxs-lookup"><span data-stu-id="ca136-140">**Virtual Network Gateway Name:** VNet1GW</span></span>
* <span data-ttu-id="ca136-141">**公用 IP：**VNet1GWIP</span><span class="sxs-lookup"><span data-stu-id="ca136-141">**Public IP:** VNet1GWIP</span></span>
* <span data-ttu-id="ca136-142">**VPN 類型：**路由式</span><span class="sxs-lookup"><span data-stu-id="ca136-142">**VPN Type:** Route-based</span></span>
* <span data-ttu-id="ca136-143">**連線類型︰**網站間 (IPsec)</span><span class="sxs-lookup"><span data-stu-id="ca136-143">**Connection Type:** Site-to-site (IPsec)</span></span>
* <span data-ttu-id="ca136-144">**閘道類型：**VPN</span><span class="sxs-lookup"><span data-stu-id="ca136-144">**Gateway Type:** VPN</span></span>
* <span data-ttu-id="ca136-145">**區域網路閘道名稱：**Site2</span><span class="sxs-lookup"><span data-stu-id="ca136-145">**Local Network Gateway Name:** Site2</span></span>
* <span data-ttu-id="ca136-146">**連線名稱︰**VNet1toSite2</span><span class="sxs-lookup"><span data-stu-id="ca136-146">**Connection Name:** VNet1toSite2</span></span>

## <span data-ttu-id="ca136-147"><a name="CreatVNet"></a>1.建立虛擬網路</span><span class="sxs-lookup"><span data-stu-id="ca136-147"><a name="CreatVNet"></a>1. Create a virtual network</span></span>

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-basic-vnet-s2s-rm-portal-include.md)]

## <span data-ttu-id="ca136-148"><a name="dns"></a>2.指定 DNS 伺服器</span><span class="sxs-lookup"><span data-stu-id="ca136-148"><a name="dns"></a>2. Specify a DNS server</span></span>

<span data-ttu-id="ca136-149">建立站對站連線時不需要 DNS。</span><span class="sxs-lookup"><span data-stu-id="ca136-149">DNS is not required to create a Site-to-Site connection.</span></span> <span data-ttu-id="ca136-150">不過，如果您想要對部署至虛擬網路的資源進行名稱解析，則應指定 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="ca136-150">However, if you want to have name resolution for resources that are deployed to your virtual network, you should specify a DNS server.</span></span> <span data-ttu-id="ca136-151">此設定可讓您指定要用於此虛擬網路之名稱解析的 DNS 伺服器服務。</span><span class="sxs-lookup"><span data-stu-id="ca136-151">This setting lets you specify the DNS server that you want to use for name resolution for this virtual network.</span></span> <span data-ttu-id="ca136-152">它不會建立 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="ca136-152">It does not create a DNS server.</span></span> <span data-ttu-id="ca136-153">如需名稱解析的詳細資訊，請參閱 [VM 和角色執行個體的名稱解析](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md)。</span><span class="sxs-lookup"><span data-stu-id="ca136-153">For more information about name resolution, see [Name Resolution for VMs and role instances](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span></span>

[!INCLUDE [vpn-gateway-add-dns-rm-portal](../../includes/vpn-gateway-add-dns-rm-portal-include.md)]

## <span data-ttu-id="ca136-154"><a name="gatewaysubnet"></a>3.建立閘道子網路</span><span class="sxs-lookup"><span data-stu-id="ca136-154"><a name="gatewaysubnet"></a>3. Create the gateway subnet</span></span>

[!INCLUDE [vpn-gateway-aboutgwsubnet](../../includes/vpn-gateway-about-gwsubnet-include.md)]

[!INCLUDE [vpn-gateway-add-gwsubnet-rm-portal](../../includes/vpn-gateway-add-gwsubnet-s2s-rm-portal-include.md)]

## <span data-ttu-id="ca136-155"><a name="VNetGateway"></a>4.建立 VPN 閘道</span><span class="sxs-lookup"><span data-stu-id="ca136-155"><a name="VNetGateway"></a>4. Create the VPN gateway</span></span>

[!INCLUDE [vpn-gateway-add-gw-s2s-rm-portal](../../includes/vpn-gateway-add-gw-s2s-rm-portal-include.md)]

## <span data-ttu-id="ca136-156"><a name="LocalNetworkGateway"></a>5.建立區域網路閘道</span><span class="sxs-lookup"><span data-stu-id="ca136-156"><a name="LocalNetworkGateway"></a>5. Create the local network gateway</span></span>

<span data-ttu-id="ca136-157">區域網路閘道通常是指您的內部部署位置。</span><span class="sxs-lookup"><span data-stu-id="ca136-157">The local network gateway typically refers to your on-premises location.</span></span> <span data-ttu-id="ca136-158">請賦予網站可供 Azure 參考的名稱，然後指定您想要與其建立連線之內部部署 VPN 裝置的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="ca136-158">You give the site a name by which Azure can refer to it, then specify the IP address of the on-premises VPN device to which you will create a connection.</span></span> <span data-ttu-id="ca136-159">也請指定 IP 位址首碼，以供系統透過 VPN 閘道路由至 VPN 裝置。</span><span class="sxs-lookup"><span data-stu-id="ca136-159">You also specify the IP address prefixes that will be routed through the VPN gateway to the VPN device.</span></span> <span data-ttu-id="ca136-160">您指定的位址首碼是位於內部部署網路上的首碼。</span><span class="sxs-lookup"><span data-stu-id="ca136-160">The address prefixes you specify are the prefixes located on your on-premises network.</span></span> <span data-ttu-id="ca136-161">如果您的內部部署網路變更，或者您需要變更 VPN 裝置的公用 IP 位址，您稍後可以輕鬆地更新這些值。</span><span class="sxs-lookup"><span data-stu-id="ca136-161">If your on-premises network changes or you need to change the public IP address for the VPN device, you can easily update the values later.</span></span>

[!INCLUDE [Add local network gateway](../../includes/vpn-gateway-add-lng-s2s-rm-portal-include.md)]

## <span data-ttu-id="ca136-162"><a name="VPNDevice"></a>6.設定 VPN 裝置</span><span class="sxs-lookup"><span data-stu-id="ca136-162"><a name="VPNDevice"></a>6. Configure your VPN device</span></span>

<span data-ttu-id="ca136-163">內部部署網路的站對站連線需要 VPN 裝置。</span><span class="sxs-lookup"><span data-stu-id="ca136-163">Site-to-Site connections to an on-premises network require a VPN device.</span></span> <span data-ttu-id="ca136-164">在此步驟中，設定 VPN 裝置。</span><span class="sxs-lookup"><span data-stu-id="ca136-164">In this step, you configure your VPN device.</span></span> <span data-ttu-id="ca136-165">在設定 VPN 裝置時，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="ca136-165">When configuring your VPN device, you need the following:</span></span>

- <span data-ttu-id="ca136-166">共用金鑰。</span><span class="sxs-lookup"><span data-stu-id="ca136-166">A shared key.</span></span> <span data-ttu-id="ca136-167">這個共同金鑰與您建立站對站 VPN 連線時指定的共用金鑰相同。</span><span class="sxs-lookup"><span data-stu-id="ca136-167">This is the same shared key that you specify when creating your Site-to-Site VPN connection.</span></span> <span data-ttu-id="ca136-168">在我們的範例中，我們會使用基本的共用金鑰。</span><span class="sxs-lookup"><span data-stu-id="ca136-168">In our examples, we use a basic shared key.</span></span> <span data-ttu-id="ca136-169">我們建議您產生更複雜的金鑰以供使用。</span><span class="sxs-lookup"><span data-stu-id="ca136-169">We recommend that you generate a more complex key to use.</span></span>
- <span data-ttu-id="ca136-170">虛擬網路閘道的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="ca136-170">The Public IP address of your virtual network gateway.</span></span> <span data-ttu-id="ca136-171">您可以使用 Azure 入口網站、PowerShell 或 CLI 來檢視公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="ca136-171">You can view the public IP address by using the Azure portal, PowerShell, or CLI.</span></span> <span data-ttu-id="ca136-172">若要使用 Azure 入口網站尋找 VPN 閘道的公用 IP 位址，請瀏覽至 [虛擬網路閘道]，然後按一下閘道名稱。</span><span class="sxs-lookup"><span data-stu-id="ca136-172">To find the Public IP address of your VPN gateway using the Azure portal, navigate to **Virtual network gateways**, then click the name of your gateway.</span></span>

[!INCLUDE [Configure a VPN device](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]

## <span data-ttu-id="ca136-173"><a name="CreateConnection"></a>7.建立 VPN 連線</span><span class="sxs-lookup"><span data-stu-id="ca136-173"><a name="CreateConnection"></a>7. Create the VPN connection</span></span>

<span data-ttu-id="ca136-174">您會在虛擬網路閘道與內部部署 VPN 裝置之間建立站對站 VPN 連線。</span><span class="sxs-lookup"><span data-stu-id="ca136-174">Create the Site-to-Site VPN connection between your virtual network gateway and your on-premises VPN device.</span></span>

[!INCLUDE [Add connections](../../includes/vpn-gateway-add-site-to-site-connection-s2s-rm-portal-include.md)]

## <span data-ttu-id="ca136-175"><a name="VerifyConnection"></a>8.驗證 VPN 連線</span><span class="sxs-lookup"><span data-stu-id="ca136-175"><a name="VerifyConnection"></a>8. Verify the VPN connection</span></span>

[!INCLUDE [Verify - Azure portal](../../includes/vpn-gateway-verify-connection-portal-rm-include.md)]

## <span data-ttu-id="ca136-176"><a name="connectVM"></a>連線至虛擬機器</span><span class="sxs-lookup"><span data-stu-id="ca136-176"><a name="connectVM"></a>To connect to a virtual machine</span></span>

[!INCLUDE [Connect to a VM](../../includes/vpn-gateway-connect-vm-s2s-include.md)]

## <span data-ttu-id="ca136-177"><a name="reset"></a>如何重設 VPN 閘道</span><span class="sxs-lookup"><span data-stu-id="ca136-177"><a name="reset"></a>How to reset a VPN gateway</span></span>

<span data-ttu-id="ca136-178">如果您遺失一或多個站對站 VPN 通道上的跨單位 VPN 連線，重設 Azure VPN 閘道會很有幫助。</span><span class="sxs-lookup"><span data-stu-id="ca136-178">Resetting an Azure VPN gateway is helpful if you lose cross-premises VPN connectivity on one or more Site-to-Site VPN tunnels.</span></span> <span data-ttu-id="ca136-179">在此情況下，您的所有內部部署 VPN 裝置都會運作正常，但無法使用 Azure VPN 閘道建立 IPsec 通道。</span><span class="sxs-lookup"><span data-stu-id="ca136-179">In this situation, your on-premises VPN devices are all working correctly, but are not able to establish IPsec tunnels with the Azure VPN gateways.</span></span> <span data-ttu-id="ca136-180">如需相關步驟，請參閱[重設 VPN 閘道](vpn-gateway-resetgw-classic.md)。</span><span class="sxs-lookup"><span data-stu-id="ca136-180">For steps, see [Reset a VPN gateway](vpn-gateway-resetgw-classic.md).</span></span>

## <span data-ttu-id="ca136-181"><a name="resize"></a>如何變更閘道 SKU (調整閘道的大小)</span><span class="sxs-lookup"><span data-stu-id="ca136-181"><a name="resize"></a>How to change a gateway SKU (resize a gateway)</span></span>

<span data-ttu-id="ca136-182">如需變更閘道 SKU 的步驟，請參閱[閘道 SKU](vpn-gateway-about-vpn-gateway-settings.md#gwsku)。</span><span class="sxs-lookup"><span data-stu-id="ca136-182">For the steps to change a gateway SKU, see [Gateway SKUs](vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ca136-183">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ca136-183">Next steps</span></span>

* <span data-ttu-id="ca136-184">如需 BGP 的相關資訊，請參閱 [BGP 概觀](vpn-gateway-bgp-overview.md)和[如何設定 BGP](vpn-gateway-bgp-resource-manager-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="ca136-184">For information about BGP, see the [BGP Overview](vpn-gateway-bgp-overview.md) and [How to configure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span></span>
* <span data-ttu-id="ca136-185">如需強制通道的相關資訊，請參閱[關於強制通道](vpn-gateway-forced-tunneling-rm.md)。</span><span class="sxs-lookup"><span data-stu-id="ca136-185">For information about Forced Tunneling, see [About Forced Tunneling](vpn-gateway-forced-tunneling-rm.md).</span></span>
* <span data-ttu-id="ca136-186">如需高可用性主動-主動連線的相關資訊，請參閱[高可用性跨單位和 VNet 對 VNet 連線能力](vpn-gateway-highlyavailable.md)。</span><span class="sxs-lookup"><span data-stu-id="ca136-186">For information about Highly Available Active-Active connections, see [Highly Available cross-premises and VNet-to-VNet connectivity](vpn-gateway-highlyavailable.md).</span></span>
