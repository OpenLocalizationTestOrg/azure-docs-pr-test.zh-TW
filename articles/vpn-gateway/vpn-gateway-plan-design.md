---
title: "跨單位連線的規劃和設計：Azure VPN 閘道| Microsoft Docs"
description: "深入了解跨單位、混合式和 VNet 對 VNet 連線的 VPN 閘道規劃與設計"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: d5aaab83-4e74-4484-8bf0-cc465811e757
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/27/2017
ms.author: cherylmc
ms.openlocfilehash: 3d4587ba31d163384212eca88a7e2c0ba8f3b21f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="planning-and-design-for-vpn-gateway"></a>規劃與設計 VPN 閘道

跨單位及 VNet 對 VNet 組態的規劃與設計有可能很簡單，也可能很複雜，需視您的網路需求而定。 本文將逐步引導您完成基本的規劃和設計考量。

## <a name="planning"></a>規劃

### <a name="compare"></a>跨單位連線選項

如果您想 tooconnect 內部網站安全地 tooa 虛擬網路，因此您有三個不同的方式 toodo： 站台間，點對站和 ExpressRoute。 比較 hello 不同的跨單位連線所提供。 hello 您選擇的選項可以根據各種因素而定，例如：

* 您的方案需要哪種輸送量?
* 是否要 toocommunicate hello 透過公用網際網路，透過安全的 VPN 或私人連線嗎？
* 您有公用 IP 位址可用 toouse 嗎？
* 您計劃 toouse VPN 裝置？ 如果是，它相容嗎？
* 您只連線幾台電腦或您想要網站持續連線?
* 都需要哪些類型的 VPN 閘道想 toocreate hello 方案？
* 您應該使用哪一種閘道 SKU？

### <a name="planningtable"></a>規劃表

下表中的 hello 可協助您決定為您的方案 hello 最佳連線選項。

[!INCLUDE [vpn-gateway-cross-premises](../../includes/vpn-gateway-cross-premises-include.md)]

### <a name="gwsku"></a>閘道 SKU

[!INCLUDE [vpn-gateway-table-gwtype-aggtput](../../includes/vpn-gateway-table-gwtype-aggtput-include.md)]

### <a name="wf"></a>工作流程

hello 下列清單會列出 hello 雲端連線。 常見的工作流程：

1. 設計和計劃連線拓撲和清單 hello 位址空間的所有網路您想 tooconnect。
2. 建立 Azure 虛擬網路。 
3. 建立 hello 虛擬網路的 VPN 閘道。
4. 建立並設定連接 tooon 內部部署網路或其他虛擬網路 （如有需要）。
5. 建立並設定 Azure VPN 閘道的點對站連線 (視需要)。

## <a name="design"></a>設計
### <a name="topologies"></a>連線拓撲

先來看看 hello 中的 hello 圖表[有關 VPN 閘道](vpn-gateway-about-vpngateways.md)發行項。 hello 發行項包含基本的圖表，每個拓撲，以及您可以使用 toodeploy 組態 hello 可用的部署工具的 hello 部署模型。

### <a name="designbasics"></a>設計基本概念

hello 下列各節討論 hello VPN 閘道的基本概念。 

#### <a name="servicelimits"></a>網路服務限制

捲動 hello 資料表 tooview[網路服務限制](../azure-subscription-service-limits.md#networking-limits)。 上述的 hello 限制可能會影響您的設計。

#### <a name="subnets"></a>關於子網路

當您建立連線時，必須考量您的子網路範圍。 子網路位址範圍不能重疊。 重疊的子網路時，一個虛擬網路或內部部署位置包含相同 hello 其他位置的位址空間包含的 hello。 這表示的範圍，以針對您 toouse 您本機內部網路 toocarve 需要網路工程師，Azure ip 位址空間/子網路。 您需要不使用 hello 本機內部網路的位址空間。

使用 VNet 對 VNet 連線時，也要注意避免重疊的子網路。 如果您的子網路重疊的 IP 位址存在傳送 hello 和目的地的 Vnet，VNet 對 VNet 連線失敗。 Azure 無法路由傳送 hello 資料 toohello 另一個 VNet 因為 hello 目的地位址是 hello 傳送 VNet 的一部分。

「VPN 閘道」需要名為閘道子網路的特定子網路。 所有的閘道子網路必須命名為 GatewaySubnet toowork 正確。 請務必不 tooname 您不同的閘道子網路名稱，而且不會部署到 Vm 或任何其他 toohello 閘道子網路。 請參閱 [閘道子網路](vpn-gateway-about-vpn-gateway-settings.md#gwsub)。

#### <a name="local"></a>關於區域網路閘道

hello 區域網路閘道通常是指 tooyour 在內部部署位置。 Hello 傳統部署模型，在 hello 區域網路閘道會是參照的 tooas 本機網路站台。 當您設定區域網路閘道時，您會為它命名，指定 hello 公用 IP 位址的 hello 在內部部署 VPN 裝置，以及指定 hello 在內部部署位置中的 hello 位址首碼。 Azure 會查看 hello 目的地位址首碼的網路流量、 參照您所指定的 hello 組態 hello 本機網路閘道，並據以路由傳送封包。 您可以視需要修改 hello 位址前置詞。 如需詳細資訊，請參閱[區域網路閘道](vpn-gateway-about-vpn-gateway-settings.md#lng)。

#### <a name="gwtype"></a>關於閘道類型

選取您的拓撲的 hello 正確的閘道類型相當重要。 如果您選取 hello 類型錯誤，您的閘道器就無法正常運作。 hello 閘道類型指定 hello 閘道本身連接和 hello Resource Manager 部署模型的必要的組態設定的方式。

hello 閘道類型包括：

* Vpn
* ExpressRoute

#### <a name="connectiontype"></a>關於連線類型

每個組態皆需要特定的連線類型。 hello 連線類型如下：

* IPsec
* Vnet2Vnet
* ExpressRoute
* VPNClient

#### <a name="vpntype"></a>關於 VPN 類型

每個組態都需要特定 VPN 類型。 如果您要結合兩個組態，例如建立站對站連接和點對站連線 toohello 相同的 VNet，您必須使用符合這兩個連線需求的 VPN 類型。

[!INCLUDE [vpn-gateway-vpntype](../../includes/vpn-gateway-vpntype-include.md)]

hello 下列表格顯示 hello VPN 類型為它所對應 tooeach 連接組態。 請確定 hello 想 toocreate 您閘道的相符項目 hello 組態的 VPN 類型。 

[!INCLUDE [vpn-gateway-table-vpntype](../../includes/vpn-gateway-table-vpntype-include.md)]

### <a name="devices"></a>站對站連線的 VPN 裝置

tooconfigure 網站-站台連線，不論部署模型，您需要下列項目 hello:

* 與 Azure VPN 閘道相容的 VPN 裝置
* 不在 NAT 後方的公開 IPv4 IP 位址

您需要 toohave 體驗如何設定 VPN 裝置，或別人可為您設定裝置 hello。

[!INCLUDE [vpn-gateway-configure-vpn-device-rm](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]

### <a name="forcedtunnel"></a>考量強制通道路由

對於多數組態，您可以設定強制通道。 強制通道可讓您重新導向或 「 強制 」 所有網際網路繫結流量後 tooyour 在內部部署位置透過站對站 VPN 通道來檢查和稽核。 這是多數企業 IT 原則的重要安全性需求。 

如果沒有強制通道，您在 Azure 中的 Vm 所傳來的網際網路繫結流量將一律周遊出 toohello 網際網路，而 hello 選項 tooallow 不直接的 Azure 網路基礎結構從您 tooinspect 或稽核 hello 流量。 Tooinformation 洩漏或其他類型的安全性漏洞，可能會導致未經授權的網際網路存取。

可以在這兩種部署模型中使用不同的工具，設定強制通道的連線。 如需詳細資訊，請參閱[設定強制通道](vpn-gateway-forced-tunneling-rm.md)。

**強制通道圖表**

![Azure VPN 閘道強制通道圖表](./media/vpn-gateway-plan-design/forced-tunneling-diagram.png)

## <a name="next-steps"></a>後續步驟

請參閱 hello [VPN 閘道常見問題集](vpn-gateway-vpn-faq.md)和[有關 VPN 閘道](vpn-gateway-about-vpngateways.md)文件的詳細資訊 toohelp 您與您的設計。

如需有關特定閘道設定的詳細資訊，請參閱 [關於 VPN 閘道設定](vpn-gateway-about-vpn-gateway-settings.md)。