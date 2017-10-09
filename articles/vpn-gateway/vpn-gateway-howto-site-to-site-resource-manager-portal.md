---
title: "連接您在內部部署網路 tooan Azure 虛擬網路： 站對站 VPN： 入口網站 |Microsoft 文件"
description: "IPsec 連線從您內部網路 tooan Azure 虛擬網路上的步驟 toocreate hello 公用網際網路。 這些步驟將協助您建立使用 hello 入口網站的跨單位站對站 VPN 閘道連線。"
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
ms.openlocfilehash: 6f0acbaf1bf016026cefade048a116e94686103d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-site-to-site-connection-in-hello-azure-portal"></a><span data-ttu-id="d17eb-104">Hello Azure 入口網站中建立站對站連接</span><span class="sxs-lookup"><span data-stu-id="d17eb-104">Create a Site-to-Site connection in hello Azure portal</span></span>

<span data-ttu-id="d17eb-105">本文章將示範如何 toouse 會 hello Azure 入口網站 toocreate 站對站 VPN 閘道連線從您的內部部署網路 toohello VNet。</span><span class="sxs-lookup"><span data-stu-id="d17eb-105">This article shows you how toouse hello Azure portal toocreate a Site-to-Site VPN gateway connection from your on-premises network toohello VNet.</span></span> <span data-ttu-id="d17eb-106">本文章中的 hello 步驟適用於 toohello Resource Manager 部署模型。</span><span class="sxs-lookup"><span data-stu-id="d17eb-106">hello steps in this article apply toohello Resource Manager deployment model.</span></span> <span data-ttu-id="d17eb-107">您也可以建立此組態使用不同的部署工具或部署模型，從下列清單中的 hello 選取不同的選項：</span><span class="sxs-lookup"><span data-stu-id="d17eb-107">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="d17eb-108">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="d17eb-108">Azure portal</span></span>](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="d17eb-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d17eb-109">PowerShell</span></span>](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [<span data-ttu-id="d17eb-110">CLI</span><span class="sxs-lookup"><span data-stu-id="d17eb-110">CLI</span></span>](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [<span data-ttu-id="d17eb-111">Azure 入口網站 (傳統)</span><span class="sxs-lookup"><span data-stu-id="d17eb-111">Azure portal (classic)</span></span>](vpn-gateway-howto-site-to-site-classic-portal.md)
> 
>

<span data-ttu-id="d17eb-112">站對站 VPN 閘道連線是使用的 tooconnect 您內部網路 tooan Azure 虛擬網路透過 VPN IPsec/IKE （IKEv1 或 IKEv2） 通道。</span><span class="sxs-lookup"><span data-stu-id="d17eb-112">A Site-to-Site VPN gateway connection is used tooconnect your on-premises network tooan Azure virtual network over an IPsec/IKE (IKEv1 or IKEv2) VPN tunnel.</span></span> <span data-ttu-id="d17eb-113">這種類型的連線需要 VPN 裝置位於內部部署具有對外開放的公用 IP 位址指派 tooit。</span><span class="sxs-lookup"><span data-stu-id="d17eb-113">This type of connection requires a VPN device located on-premises that has an externally facing public IP address assigned tooit.</span></span> <span data-ttu-id="d17eb-114">如需 VPN 閘道的詳細資訊，請參閱[關於 VPN 閘道](vpn-gateway-about-vpngateways.md)。</span><span class="sxs-lookup"><span data-stu-id="d17eb-114">For more information about VPN gateways, see [About VPN gateway](vpn-gateway-about-vpngateways.md).</span></span>

![站對站 VPN 閘道跨單位連線圖表](./media/vpn-gateway-howto-site-to-site-resource-manager-portal/site-to-site-diagram.png)

## <a name="before-you-begin"></a><span data-ttu-id="d17eb-116">開始之前</span><span class="sxs-lookup"><span data-stu-id="d17eb-116">Before you begin</span></span>

<span data-ttu-id="d17eb-117">請確認您已符合下列準則，開始您的組態之前 hello:</span><span class="sxs-lookup"><span data-stu-id="d17eb-117">Verify that you have met hello following criteria before beginning your configuration:</span></span>

* <span data-ttu-id="d17eb-118">請確定您擁有相容的 VPN 裝置和人能夠 tooconfigure 它。</span><span class="sxs-lookup"><span data-stu-id="d17eb-118">Make sure you have a compatible VPN device and someone who is able tooconfigure it.</span></span> <span data-ttu-id="d17eb-119">如需相容 VPN 裝置和裝置組態的詳細資訊，請參閱[關於 VPN 裝置](vpn-gateway-about-vpn-devices.md)。</span><span class="sxs-lookup"><span data-stu-id="d17eb-119">For more information about compatible VPN devices and device configuration, see [About VPN Devices](vpn-gateway-about-vpn-devices.md).</span></span>
* <span data-ttu-id="d17eb-120">確認您的 VPN 裝置有對外開放的公用 IPv4 位址。</span><span class="sxs-lookup"><span data-stu-id="d17eb-120">Verify that you have an externally facing public IPv4 address for your VPN device.</span></span> <span data-ttu-id="d17eb-121">此 IP 位址不能位於 NAT 後方。</span><span class="sxs-lookup"><span data-stu-id="d17eb-121">This IP address cannot be located behind a NAT.</span></span>
* <span data-ttu-id="d17eb-122">如果您不熟悉 hello IP 位址範圍位於內部網路組態，您需要 toocoordinate 的人可以為您提供這些詳細資料。</span><span class="sxs-lookup"><span data-stu-id="d17eb-122">If you are unfamiliar with hello IP address ranges located in your on-premises network configuration, you need toocoordinate with someone who can provide those details for you.</span></span> <span data-ttu-id="d17eb-123">當您建立此設定時，您必須指定 hello IP 位址範圍前置詞，則 Azure 會路由傳送 tooyour 在內部部署位置。</span><span class="sxs-lookup"><span data-stu-id="d17eb-123">When you create this configuration, you must specify hello IP address range prefixes that Azure will route tooyour on-premises location.</span></span> <span data-ttu-id="d17eb-124">無 hello 的內部部署網路的子網路可以透過圈具有您想要 tooconnect hello 虛擬網路子網路。</span><span class="sxs-lookup"><span data-stu-id="d17eb-124">None of hello subnets of your on-premises network can over lap with hello virtual network subnets that you want tooconnect to.</span></span> 

### <span data-ttu-id="d17eb-125"><a name="values"></a>範例值</span><span class="sxs-lookup"><span data-stu-id="d17eb-125"><a name="values"></a>Example values</span></span>

<span data-ttu-id="d17eb-126">本文章中的 hello 範例會使用下列值的 hello。</span><span class="sxs-lookup"><span data-stu-id="d17eb-126">hello examples in this article use hello following values.</span></span> <span data-ttu-id="d17eb-127">您可以使用這些值 toocreate 測試環境中，或參閱 toothem toobetter 了解這篇文章中的 hello 範例。</span><span class="sxs-lookup"><span data-stu-id="d17eb-127">You can use these values toocreate a test environment, or refer toothem toobetter understand hello examples in this article.</span></span>

* <span data-ttu-id="d17eb-128">**VNet 名稱︰**TestVNet1</span><span class="sxs-lookup"><span data-stu-id="d17eb-128">**VNet Name:** TestVNet1</span></span>
* <span data-ttu-id="d17eb-129">**位址空間：**</span><span class="sxs-lookup"><span data-stu-id="d17eb-129">**Address Space:**</span></span> 
  * <span data-ttu-id="d17eb-130">10.11.0.0/16</span><span class="sxs-lookup"><span data-stu-id="d17eb-130">10.11.0.0/16</span></span>
  * <span data-ttu-id="d17eb-131">10.12.0.0/16 (對此練習是選擇性的)</span><span class="sxs-lookup"><span data-stu-id="d17eb-131">10.12.0.0/16 (optional for this exercise)</span></span>
* <span data-ttu-id="d17eb-132">**子網路：**</span><span class="sxs-lookup"><span data-stu-id="d17eb-132">**Subnets:**</span></span>
  * <span data-ttu-id="d17eb-133">FrontEnd：10.11.0.0/24</span><span class="sxs-lookup"><span data-stu-id="d17eb-133">FrontEnd: 10.11.0.0/24</span></span>
  * <span data-ttu-id="d17eb-134">BackEnd：10.12.0.0/24 (對此練習是選擇性的)</span><span class="sxs-lookup"><span data-stu-id="d17eb-134">BackEnd: 10.12.0.0/24 (optional for this exercise)</span></span>
* <span data-ttu-id="d17eb-135">**GatewaySubnet：**10.11.255.0/27</span><span class="sxs-lookup"><span data-stu-id="d17eb-135">**GatewaySubnet:** 10.11.255.0/27</span></span>
* <span data-ttu-id="d17eb-136">**資源群組︰**TestRG1</span><span class="sxs-lookup"><span data-stu-id="d17eb-136">**Resource Group:** TestRG1</span></span>
* <span data-ttu-id="d17eb-137">**位置：**美國東部</span><span class="sxs-lookup"><span data-stu-id="d17eb-137">**Location:** East US</span></span>
* <span data-ttu-id="d17eb-138">**DNS 伺服器：**選擇性。</span><span class="sxs-lookup"><span data-stu-id="d17eb-138">**DNS Server:** Optional.</span></span> <span data-ttu-id="d17eb-139">hello DNS 伺服器的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="d17eb-139">hello IP address of your DNS server.</span></span>
* <span data-ttu-id="d17eb-140">**虛擬網路閘道名稱：**VNet1GW</span><span class="sxs-lookup"><span data-stu-id="d17eb-140">**Virtual Network Gateway Name:** VNet1GW</span></span>
* <span data-ttu-id="d17eb-141">**公用 IP：**VNet1GWIP</span><span class="sxs-lookup"><span data-stu-id="d17eb-141">**Public IP:** VNet1GWIP</span></span>
* <span data-ttu-id="d17eb-142">**VPN 類型：**路由式</span><span class="sxs-lookup"><span data-stu-id="d17eb-142">**VPN Type:** Route-based</span></span>
* <span data-ttu-id="d17eb-143">**連線類型︰**網站間 (IPsec)</span><span class="sxs-lookup"><span data-stu-id="d17eb-143">**Connection Type:** Site-to-site (IPsec)</span></span>
* <span data-ttu-id="d17eb-144">**閘道類型：**VPN</span><span class="sxs-lookup"><span data-stu-id="d17eb-144">**Gateway Type:** VPN</span></span>
* <span data-ttu-id="d17eb-145">**區域網路閘道名稱：**Site2</span><span class="sxs-lookup"><span data-stu-id="d17eb-145">**Local Network Gateway Name:** Site2</span></span>
* <span data-ttu-id="d17eb-146">**連線名稱︰**VNet1toSite2</span><span class="sxs-lookup"><span data-stu-id="d17eb-146">**Connection Name:** VNet1toSite2</span></span>

## <span data-ttu-id="d17eb-147"><a name="CreatVNet"></a>1.建立虛擬網路</span><span class="sxs-lookup"><span data-stu-id="d17eb-147"><a name="CreatVNet"></a>1. Create a virtual network</span></span>

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-basic-vnet-s2s-rm-portal-include.md)]

## <span data-ttu-id="d17eb-148"><a name="dns"></a>2.指定 DNS 伺服器</span><span class="sxs-lookup"><span data-stu-id="d17eb-148"><a name="dns"></a>2. Specify a DNS server</span></span>

<span data-ttu-id="d17eb-149">DNS 是不必要的 toocreate 網站-站台連線。</span><span class="sxs-lookup"><span data-stu-id="d17eb-149">DNS is not required toocreate a Site-to-Site connection.</span></span> <span data-ttu-id="d17eb-150">不過，如果您想要部署的 tooyour 虛擬網路的資源 toohave 名稱解析，您應該指定 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="d17eb-150">However, if you want toohave name resolution for resources that are deployed tooyour virtual network, you should specify a DNS server.</span></span> <span data-ttu-id="d17eb-151">此設定可讓您指定 hello toouse 需為此虛擬網路的名稱解析的 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="d17eb-151">This setting lets you specify hello DNS server that you want toouse for name resolution for this virtual network.</span></span> <span data-ttu-id="d17eb-152">它不會建立 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="d17eb-152">It does not create a DNS server.</span></span> <span data-ttu-id="d17eb-153">如需名稱解析的詳細資訊，請參閱 [VM 和角色執行個體的名稱解析](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md)。</span><span class="sxs-lookup"><span data-stu-id="d17eb-153">For more information about name resolution, see [Name Resolution for VMs and role instances](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span></span>

[!INCLUDE [vpn-gateway-add-dns-rm-portal](../../includes/vpn-gateway-add-dns-rm-portal-include.md)]

## <span data-ttu-id="d17eb-154"><a name="gatewaysubnet"></a>3.建立 hello 閘道子網路</span><span class="sxs-lookup"><span data-stu-id="d17eb-154"><a name="gatewaysubnet"></a>3. Create hello gateway subnet</span></span>

[!INCLUDE [vpn-gateway-aboutgwsubnet](../../includes/vpn-gateway-about-gwsubnet-include.md)]

[!INCLUDE [vpn-gateway-add-gwsubnet-rm-portal](../../includes/vpn-gateway-add-gwsubnet-s2s-rm-portal-include.md)]

## <span data-ttu-id="d17eb-155"><a name="VNetGateway"></a>4.建立 hello VPN 閘道</span><span class="sxs-lookup"><span data-stu-id="d17eb-155"><a name="VNetGateway"></a>4. Create hello VPN gateway</span></span>

[!INCLUDE [vpn-gateway-add-gw-s2s-rm-portal](../../includes/vpn-gateway-add-gw-s2s-rm-portal-include.md)]

## <span data-ttu-id="d17eb-156"><a name="LocalNetworkGateway"></a>5.建立 hello 區域網路閘道</span><span class="sxs-lookup"><span data-stu-id="d17eb-156"><a name="LocalNetworkGateway"></a>5. Create hello local network gateway</span></span>

<span data-ttu-id="d17eb-157">hello 區域網路閘道通常是指 tooyour 在內部部署位置。</span><span class="sxs-lookup"><span data-stu-id="d17eb-157">hello local network gateway typically refers tooyour on-premises location.</span></span> <span data-ttu-id="d17eb-158">您提供 hello 站台的名稱之 Azure 可以參考 tooit，然後指定 hello IP 位址的 hello 在內部部署 VPN 裝置 toowhich 中，您將建立連接。</span><span class="sxs-lookup"><span data-stu-id="d17eb-158">You give hello site a name by which Azure can refer tooit, then specify hello IP address of hello on-premises VPN device toowhich you will create a connection.</span></span> <span data-ttu-id="d17eb-159">您也指定 hello 而必須路由傳送透過 hello VPN 閘道 toohello VPN 裝置 IP 位址首碼。</span><span class="sxs-lookup"><span data-stu-id="d17eb-159">You also specify hello IP address prefixes that will be routed through hello VPN gateway toohello VPN device.</span></span> <span data-ttu-id="d17eb-160">您指定的 hello 位址前置詞是在內部部署網路上的 hello 前置詞。</span><span class="sxs-lookup"><span data-stu-id="d17eb-160">hello address prefixes you specify are hello prefixes located on your on-premises network.</span></span> <span data-ttu-id="d17eb-161">如果您在內部部署網路的變更，或需要 toochange hello 公用 IP 位址的 hello VPN 裝置，您可以輕鬆地 hello 值稍後更新。</span><span class="sxs-lookup"><span data-stu-id="d17eb-161">If your on-premises network changes or you need toochange hello public IP address for hello VPN device, you can easily update hello values later.</span></span>

[!INCLUDE [Add local network gateway](../../includes/vpn-gateway-add-lng-s2s-rm-portal-include.md)]

## <span data-ttu-id="d17eb-162"><a name="VPNDevice"></a>6.設定 VPN 裝置</span><span class="sxs-lookup"><span data-stu-id="d17eb-162"><a name="VPNDevice"></a>6. Configure your VPN device</span></span>

<span data-ttu-id="d17eb-163">站台對站連線 tooan 在內部部署網路需要 VPN 裝置。</span><span class="sxs-lookup"><span data-stu-id="d17eb-163">Site-to-Site connections tooan on-premises network require a VPN device.</span></span> <span data-ttu-id="d17eb-164">在此步驟中，設定 VPN 裝置。</span><span class="sxs-lookup"><span data-stu-id="d17eb-164">In this step, you configure your VPN device.</span></span> <span data-ttu-id="d17eb-165">當設定 VPN 裝置，您會需要 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="d17eb-165">When configuring your VPN device, you need hello following:</span></span>

- <span data-ttu-id="d17eb-166">共用金鑰。</span><span class="sxs-lookup"><span data-stu-id="d17eb-166">A shared key.</span></span> <span data-ttu-id="d17eb-167">這是共用相同 hello 建立您的站對站 VPN 連線時所指定的索引鍵。</span><span class="sxs-lookup"><span data-stu-id="d17eb-167">This is hello same shared key that you specify when creating your Site-to-Site VPN connection.</span></span> <span data-ttu-id="d17eb-168">在我們的範例中，我們會使用基本的共用金鑰。</span><span class="sxs-lookup"><span data-stu-id="d17eb-168">In our examples, we use a basic shared key.</span></span> <span data-ttu-id="d17eb-169">我們建議您產生更複雜金鑰 toouse。</span><span class="sxs-lookup"><span data-stu-id="d17eb-169">We recommend that you generate a more complex key toouse.</span></span>
- <span data-ttu-id="d17eb-170">hello 的虛擬網路閘道的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="d17eb-170">hello Public IP address of your virtual network gateway.</span></span> <span data-ttu-id="d17eb-171">您可以使用 hello Azure 入口網站、 PowerShell 或 CLI 檢視 hello 公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="d17eb-171">You can view hello public IP address by using hello Azure portal, PowerShell, or CLI.</span></span> <span data-ttu-id="d17eb-172">toofind hello 公用 IP 位址的 VPN 閘道使用 hello Azure 入口網站，瀏覽過**虛擬網路閘道**，然後按一下您的閘道 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="d17eb-172">toofind hello Public IP address of your VPN gateway using hello Azure portal, navigate too**Virtual network gateways**, then click hello name of your gateway.</span></span>

[!INCLUDE [Configure a VPN device](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]

## <span data-ttu-id="d17eb-173"><a name="CreateConnection"></a>7.建立 hello VPN 連線</span><span class="sxs-lookup"><span data-stu-id="d17eb-173"><a name="CreateConnection"></a>7. Create hello VPN connection</span></span>

<span data-ttu-id="d17eb-174">建立虛擬網路閘道與內部部署 VPN 裝置之間的 hello 站對站 VPN 連線。</span><span class="sxs-lookup"><span data-stu-id="d17eb-174">Create hello Site-to-Site VPN connection between your virtual network gateway and your on-premises VPN device.</span></span>

[!INCLUDE [Add connections](../../includes/vpn-gateway-add-site-to-site-connection-s2s-rm-portal-include.md)]

## <span data-ttu-id="d17eb-175"><a name="VerifyConnection"></a>8.確認 hello VPN 連線</span><span class="sxs-lookup"><span data-stu-id="d17eb-175"><a name="VerifyConnection"></a>8. Verify hello VPN connection</span></span>

[!INCLUDE [Verify - Azure portal](../../includes/vpn-gateway-verify-connection-portal-rm-include.md)]

## <span data-ttu-id="d17eb-176"><a name="connectVM"></a>tooconnect tooa 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="d17eb-176"><a name="connectVM"></a>tooconnect tooa virtual machine</span></span>

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-s2s-include.md)]

## <span data-ttu-id="d17eb-177"><a name="reset"></a>如何 tooreset VPN 閘道</span><span class="sxs-lookup"><span data-stu-id="d17eb-177"><a name="reset"></a>How tooreset a VPN gateway</span></span>

<span data-ttu-id="d17eb-178">如果您遺失一或多個站對站 VPN 通道上的跨單位 VPN 連線，重設 Azure VPN 閘道會很有幫助。</span><span class="sxs-lookup"><span data-stu-id="d17eb-178">Resetting an Azure VPN gateway is helpful if you lose cross-premises VPN connectivity on one or more Site-to-Site VPN tunnels.</span></span> <span data-ttu-id="d17eb-179">在此情況下，您在內部部署 VPN 裝置是所有運作正常，但您不能 tooestablish 與 hello Azure VPN 閘道 IPsec 通道。</span><span class="sxs-lookup"><span data-stu-id="d17eb-179">In this situation, your on-premises VPN devices are all working correctly, but are not able tooestablish IPsec tunnels with hello Azure VPN gateways.</span></span> <span data-ttu-id="d17eb-180">如需相關步驟，請參閱[重設 VPN 閘道](vpn-gateway-resetgw-classic.md)。</span><span class="sxs-lookup"><span data-stu-id="d17eb-180">For steps, see [Reset a VPN gateway](vpn-gateway-resetgw-classic.md).</span></span>

## <span data-ttu-id="d17eb-181"><a name="resize"></a>如何 toochange 閘道 SKU （調整大小的閘道）</span><span class="sxs-lookup"><span data-stu-id="d17eb-181"><a name="resize"></a>How toochange a gateway SKU (resize a gateway)</span></span>

<span data-ttu-id="d17eb-182">Hello 步驟 toochange 閘道 SKU，請參閱[閘道 Sku](vpn-gateway-about-vpn-gateway-settings.md#gwsku)。</span><span class="sxs-lookup"><span data-stu-id="d17eb-182">For hello steps toochange a gateway SKU, see [Gateway SKUs](vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d17eb-183">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d17eb-183">Next steps</span></span>

* <span data-ttu-id="d17eb-184">BGP 的相關資訊，請參閱 hello [BGP 概觀](vpn-gateway-bgp-overview.md)和[如何 tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="d17eb-184">For information about BGP, see hello [BGP Overview](vpn-gateway-bgp-overview.md) and [How tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span></span>
* <span data-ttu-id="d17eb-185">如需強制通道的相關資訊，請參閱[關於強制通道](vpn-gateway-forced-tunneling-rm.md)。</span><span class="sxs-lookup"><span data-stu-id="d17eb-185">For information about Forced Tunneling, see [About Forced Tunneling](vpn-gateway-forced-tunneling-rm.md).</span></span>
* <span data-ttu-id="d17eb-186">如需高可用性主動-主動連線的相關資訊，請參閱[高可用性跨單位和 VNet 對 VNet 連線能力](vpn-gateway-highlyavailable.md)。</span><span class="sxs-lookup"><span data-stu-id="d17eb-186">For information about Highly Available Active-Active connections, see [Highly Available cross-premises and VNet-to-VNet connectivity](vpn-gateway-highlyavailable.md).</span></span>
