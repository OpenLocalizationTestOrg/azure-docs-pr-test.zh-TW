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
# <a name="create-a-site-to-site-connection-in-hello-azure-portal"></a>Hello Azure 入口網站中建立站對站連接

本文章將示範如何 toouse 會 hello Azure 入口網站 toocreate 站對站 VPN 閘道連線從您的內部部署網路 toohello VNet。 本文章中的 hello 步驟適用於 toohello Resource Manager 部署模型。 您也可以建立此組態使用不同的部署工具或部署模型，從下列清單中的 hello 選取不同的選項：

> [!div class="op_single_selector"]
> * [Azure 入口網站](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [CLI](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [Azure 入口網站 (傳統)](vpn-gateway-howto-site-to-site-classic-portal.md)
> 
>

站對站 VPN 閘道連線是使用的 tooconnect 您內部網路 tooan Azure 虛擬網路透過 VPN IPsec/IKE （IKEv1 或 IKEv2） 通道。 這種類型的連線需要 VPN 裝置位於內部部署具有對外開放的公用 IP 位址指派 tooit。 如需 VPN 閘道的詳細資訊，請參閱[關於 VPN 閘道](vpn-gateway-about-vpngateways.md)。

![站對站 VPN 閘道跨單位連線圖表](./media/vpn-gateway-howto-site-to-site-resource-manager-portal/site-to-site-diagram.png)

## <a name="before-you-begin"></a>開始之前

請確認您已符合下列準則，開始您的組態之前 hello:

* 請確定您擁有相容的 VPN 裝置和人能夠 tooconfigure 它。 如需相容 VPN 裝置和裝置組態的詳細資訊，請參閱[關於 VPN 裝置](vpn-gateway-about-vpn-devices.md)。
* 確認您的 VPN 裝置有對外開放的公用 IPv4 位址。 此 IP 位址不能位於 NAT 後方。
* 如果您不熟悉 hello IP 位址範圍位於內部網路組態，您需要 toocoordinate 的人可以為您提供這些詳細資料。 當您建立此設定時，您必須指定 hello IP 位址範圍前置詞，則 Azure 會路由傳送 tooyour 在內部部署位置。 無 hello 的內部部署網路的子網路可以透過圈具有您想要 tooconnect hello 虛擬網路子網路。 

### <a name="values"></a>範例值

本文章中的 hello 範例會使用下列值的 hello。 您可以使用這些值 toocreate 測試環境中，或參閱 toothem toobetter 了解這篇文章中的 hello 範例。

* **VNet 名稱︰**TestVNet1
* **位址空間：** 
  * 10.11.0.0/16
  * 10.12.0.0/16 (對此練習是選擇性的)
* **子網路：**
  * FrontEnd：10.11.0.0/24
  * BackEnd：10.12.0.0/24 (對此練習是選擇性的)
* **GatewaySubnet：**10.11.255.0/27
* **資源群組︰**TestRG1
* **位置：**美國東部
* **DNS 伺服器：**選擇性。 hello DNS 伺服器的 IP 位址。
* **虛擬網路閘道名稱：**VNet1GW
* **公用 IP：**VNet1GWIP
* **VPN 類型：**路由式
* **連線類型︰**網站間 (IPsec)
* **閘道類型：**VPN
* **區域網路閘道名稱：**Site2
* **連線名稱︰**VNet1toSite2

## <a name="CreatVNet"></a>1.建立虛擬網路

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-basic-vnet-s2s-rm-portal-include.md)]

## <a name="dns"></a>2.指定 DNS 伺服器

DNS 是不必要的 toocreate 網站-站台連線。 不過，如果您想要部署的 tooyour 虛擬網路的資源 toohave 名稱解析，您應該指定 DNS 伺服器。 此設定可讓您指定 hello toouse 需為此虛擬網路的名稱解析的 DNS 伺服器。 它不會建立 DNS 伺服器。 如需名稱解析的詳細資訊，請參閱 [VM 和角色執行個體的名稱解析](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md)。

[!INCLUDE [vpn-gateway-add-dns-rm-portal](../../includes/vpn-gateway-add-dns-rm-portal-include.md)]

## <a name="gatewaysubnet"></a>3.建立 hello 閘道子網路

[!INCLUDE [vpn-gateway-aboutgwsubnet](../../includes/vpn-gateway-about-gwsubnet-include.md)]

[!INCLUDE [vpn-gateway-add-gwsubnet-rm-portal](../../includes/vpn-gateway-add-gwsubnet-s2s-rm-portal-include.md)]

## <a name="VNetGateway"></a>4.建立 hello VPN 閘道

[!INCLUDE [vpn-gateway-add-gw-s2s-rm-portal](../../includes/vpn-gateway-add-gw-s2s-rm-portal-include.md)]

## <a name="LocalNetworkGateway"></a>5.建立 hello 區域網路閘道

hello 區域網路閘道通常是指 tooyour 在內部部署位置。 您提供 hello 站台的名稱之 Azure 可以參考 tooit，然後指定 hello IP 位址的 hello 在內部部署 VPN 裝置 toowhich 中，您將建立連接。 您也指定 hello 而必須路由傳送透過 hello VPN 閘道 toohello VPN 裝置 IP 位址首碼。 您指定的 hello 位址前置詞是在內部部署網路上的 hello 前置詞。 如果您在內部部署網路的變更，或需要 toochange hello 公用 IP 位址的 hello VPN 裝置，您可以輕鬆地 hello 值稍後更新。

[!INCLUDE [Add local network gateway](../../includes/vpn-gateway-add-lng-s2s-rm-portal-include.md)]

## <a name="VPNDevice"></a>6.設定 VPN 裝置

站台對站連線 tooan 在內部部署網路需要 VPN 裝置。 在此步驟中，設定 VPN 裝置。 當設定 VPN 裝置，您會需要 hello 下列：

- 共用金鑰。 這是共用相同 hello 建立您的站對站 VPN 連線時所指定的索引鍵。 在我們的範例中，我們會使用基本的共用金鑰。 我們建議您產生更複雜金鑰 toouse。
- hello 的虛擬網路閘道的公用 IP 位址。 您可以使用 hello Azure 入口網站、 PowerShell 或 CLI 檢視 hello 公用 IP 位址。 toofind hello 公用 IP 位址的 VPN 閘道使用 hello Azure 入口網站，瀏覽過**虛擬網路閘道**，然後按一下您的閘道 hello 名稱。

[!INCLUDE [Configure a VPN device](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]

## <a name="CreateConnection"></a>7.建立 hello VPN 連線

建立虛擬網路閘道與內部部署 VPN 裝置之間的 hello 站對站 VPN 連線。

[!INCLUDE [Add connections](../../includes/vpn-gateway-add-site-to-site-connection-s2s-rm-portal-include.md)]

## <a name="VerifyConnection"></a>8.確認 hello VPN 連線

[!INCLUDE [Verify - Azure portal](../../includes/vpn-gateway-verify-connection-portal-rm-include.md)]

## <a name="connectVM"></a>tooconnect tooa 虛擬機器

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-s2s-include.md)]

## <a name="reset"></a>如何 tooreset VPN 閘道

如果您遺失一或多個站對站 VPN 通道上的跨單位 VPN 連線，重設 Azure VPN 閘道會很有幫助。 在此情況下，您在內部部署 VPN 裝置是所有運作正常，但您不能 tooestablish 與 hello Azure VPN 閘道 IPsec 通道。 如需相關步驟，請參閱[重設 VPN 閘道](vpn-gateway-resetgw-classic.md)。

## <a name="resize"></a>如何 toochange 閘道 SKU （調整大小的閘道）

Hello 步驟 toochange 閘道 SKU，請參閱[閘道 Sku](vpn-gateway-about-vpn-gateway-settings.md#gwsku)。

## <a name="next-steps"></a>後續步驟

* BGP 的相關資訊，請參閱 hello [BGP 概觀](vpn-gateway-bgp-overview.md)和[如何 tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md)。
* 如需強制通道的相關資訊，請參閱[關於強制通道](vpn-gateway-forced-tunneling-rm.md)。
* 如需高可用性主動-主動連線的相關資訊，請參閱[高可用性跨單位和 VNet 對 VNet 連線能力](vpn-gateway-highlyavailable.md)。
