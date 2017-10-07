---
title: "VPN 閘道概觀： 建立跨單位 VPN 連線 tooAzure 虛擬網路 |Microsoft 文件"
description: "此 VPN 閘道概觀說明 hello 方式 tooconnect tooAzure 虛擬網路透過 hello 網際網路使用 VPN 連線。 其中包含基本連接設定的圖表。"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 2358dd5a-cd76-42c3-baf3-2f35aadc64c8
ms.service: vpn-gateway
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/05/2017
ms.author: cherylmc
ms.openlocfilehash: 899270734270632a5b12d56021c924e977725a7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="about-vpn-gateway"></a>關於 VPN 閘道

VPN 閘道是一種虛擬網路閘道傳送加密的流量，跨公用連線 tooan 內部部署位置。 您也可以使用透過 hello Microsoft 網路的 Azure 虛擬網路之間的 VPN 閘道 toosend 加密流量。 Azure 虛擬網路與內部部署網站之間 toosend 加密網路流量，您必須建立虛擬網路的 VPN 閘道。

每個虛擬網路可以有只有一個 VPN 閘道，不過，您可以建立多個連線 toohello 相同的 VPN 閘道。 例如，多站台連線設定。 當您建立多個連線 toohello 相同的 VPN 閘道，所有 VPN 通道，包括點對站 Vpn，適用於 hello 閘道的共用 hello 頻寬。

### <a name="whatis"></a>什麼是虛擬網路閘道？

虛擬網路閘道組成兩個或更多虛擬機器的部署稱為 hello GatewaySubnet tooa 特定子網路。 hello 位於的 hello 時建立 hello 虛擬網路閘道，GatewaySubnet 所建立的 Vm。 虛擬網路閘道的 Vm 是已設定的 toocontain 路由表和閘道服務特定 toohello 閘道。 您無法直接設定 hello 屬於 hello 虛擬網路閘道的 Vm，您絕對不要部署的其他資源 toohello GatewaySubnet。

當您建立虛擬網路閘道使用 hello 'Vpn' 的閘道類型時，它會建立特定類型的加密流量; 的虛擬網路閘道VPN 閘道。 VPN 閘道可能佔用 too45 分鐘 toocreate。 這是因為 hello VPN 閘道的 Vm hello 正在部署的 toohello GatewaySubnet 而設有 hello 您指定的設定。 hello 您選取的閘道 SKU 決定的 vm 的強大功能 hello。

## <a name="gwsku"></a>閘道 SKU

[!INCLUDE [vpn-gateway-gwsku-include](../../includes/vpn-gateway-gwsku-include.md)]

## <a name="configuring"></a>設定 VPN 閘道

VPN 閘道連線需仰賴多個具有特定設定的資源。 大部分的 hello 資源可個別設定，但必須以特定順序，在某些情況下進行設定。

### <a name="settings"></a>設定

您選擇的每個資源的 hello 設定是重大 toocreating 成功的連接。 如需 VPN 閘道個別資源和設定的資訊，請參閱 [關於 VPN 閘道設定](vpn-gateway-about-vpn-gateway-settings.md)。 hello 發行項包含資訊 toohelp 您了解閘道類型、 VPN 類型、 連接類型，閘道子網路、 區域網路閘道，以及各種其他您可能想 tooconsider 的資源設定。

### <a name="tools"></a>部署工具

您可以開始建立及設定使用組態工具，例如 hello Azure 入口網站的資源。 您可以在之後決定 tooswitch tooanother 工具，例如 PowerShell tooconfigure 其他資源，或修改現有的資源時適用。 目前，您無法在 hello Azure 入口網站中設定每個資源和資源設定。 hello 文章中的每個連線的拓撲中的 hello 指示指定的特定組態工具會在需要時。 

### <a name="models"></a>部署模型

當您設定 VPN 閘道時，hello 採取的步驟取決於 hello 部署模型，您使用 toocreate 虛擬網路。 比方說，如果您已建立您的 VNet 使用 hello 傳統部署模型，使用 hello 指導方針與指示 hello 傳統部署模型 toocreate 及設定 VPN 閘道設定。 如需部署模型的詳細資訊，請參閱 [了解 Resource Manager 和傳統部署模型](../azure-resource-manager/resource-manager-deployment-model.md)。

## <a name="diagrams"></a>連線拓撲圖表

有不同的組態可用於 VPN 閘道連線的重要 tooknow 它。 您需要哪些設定最符合您需求的 toodetermine。 在下列 hello 章節，您可以檢視 hello 遵循 VPN 閘道連線的相關資訊和拓撲圖表： hello 下列各節包含的資料表清單：

* 可用的部署模型
* 可用的設定工具
* 帶您連結直接 tooan 文件： 如果有的話

使用 hello 圖表和描述 toohelp 選取 hello 連線拓撲 toomatch 您的需求。 hello 圖表顯示 hello 主要基準拓撲，但可能 toobuild 當做指導方針使用 hello 圖表更複雜的組態。

## <a name="s2smulti"></a>站對站以及多網站 (IPsec/IKE VPN 通道)

### <a name="S2S"></a>站對站

網站間 (S2S) VPN 閘道連線是透過 IPsec/IKE (IKEv1 或 IKEv2) VPN 通道建立的連線。 S2S 連線需要 VPN 裝置位於內部部署具有公用 IP 位址指派 tooit 並不位於 NAT 後方。 S2S 連線可以用於跨單位與混合式組態。   

![Azure VPN 閘道站對站連接範例](./media/vpn-gateway-about-vpngateways/vpngateway-site-to-site-connection-diagram.png)

### <a name="Multi"></a>多站台

此連線類型是 hello 站對站連線的變化。 您可以建立多個 VPN 連線從您的虛擬網路閘道，通常連接 toomultiple 內部部署站台。 處理多重連線時，您必須使用路由式 VPN 類型 (也就是使用傳統 VNet 時的動態閘道)。 因為每個虛擬網路只能有一個 VPN 閘道，則所有透過 hello 閘道的連線共用 hello 可用的頻寬。 這通常稱為「多網站」連線。

![Azure VPN 閘道多網站連接範例](./media/vpn-gateway-about-vpngateways/vpngateway-multisite-connection-diagram.png)

### <a name="deployment-models-and-methods-for-site-to-site-and-multi-site"></a>站對站和多網站的部署模型和方法

[!INCLUDE [vpn-gateway-table-site-to-site](../../includes/vpn-gateway-table-site-to-site-include.md)]

## <a name="P2S"></a>點對站 (透過 SSTP 的 VPN)

點對站 (P2S) VPN 閘道，可讓您建立從個別的用戶端電腦的安全連線 tooyour 虛擬網路。 當您想要 tooconnect tooyour 從遠端位置，例如當您從家裡或會議 telecommuting VNet，點對站 VPN 連線會很有用。 您有只有少數的用戶端需要 tooconnect tooa VNet 時 P2S VPN 也很有用的方案 toouse，而不是站對站 VPN。 

如同 S2S 連線，P2S 連線不需要內部部署公眾對應 IP 位址或 VPN 裝置。 P2S 連接只能使用透過 S2S 連線 hello 相同的 VPN 閘道，只要所有 hello 組態需求的兩個連線都相容。

使用 P2S hello 安全通訊端通道通訊協定 (SSTP)，這是 SSL 型 VPN 通訊協定。 建立之 P2S VPN 連線從 hello 用戶端電腦。

![Azure VPN 閘道點對站連接範例](./media/vpn-gateway-about-vpngateways/vpngateway-point-to-site-connection-diagram.png)

### <a name="deployment-models-and-methods-for-point-to-site"></a>點對站的部署模型和方法

[!INCLUDE [vpn-gateway-table-point-to-site](../../includes/vpn-gateway-table-point-to-site-include.md)]

## <a name="V2V"></a>VNet 對 VNet 連線 (IPsec/IKE VPN 通道)

連接虛擬網路 tooanother 虛擬網路 (VNet 對 VNet) 是類似 tooconnecting VNet tooan 在內部部署站台位置。 這兩種連線類型使用的 VPN 閘道 tooprovide 採用 IPsec/IKE 的安全通道。 您甚至可以將多網站連線組態與 VNet 對 VNet 通訊結合。 這可讓您建立結合了跨單位連線與內部虛擬網路連線的網路拓撲。

可以是您所連接的 Vnet hello:

* 在 hello 相同或不同區域
* 在 hello 相同或不同的訂用帳戶 
* 在 hello 相同或不同的部署模型

![Azure VPN 閘道 VNet tooVNet 連接範例](./media/vpn-gateway-about-vpngateways/vpngateway-vnet-to-vnet-connection-diagram.png)

### <a name="connections-between-deployment-models"></a>部署模型之間的連線

Azure 目前有兩種部署模型：傳統和 Resource Manager。 如果您已使用 Azure 一段時間，則可能具有傳統 VNet 上執行的 Azure VM 和執行個體角色。 較新的 VM 和角色執行個體可能會在 Resource Manager 中建立的 VNet 中執行。 您可以在直接與資源在另一個 VNet toocommunicate 建立 hello Vnet tooallow 之間的連線 hello 資源。

### <a name="vnet-peering"></a>VNet 對等互連

您可能無法 toouse VNet 對等互連 toocreate 您的連接，只要您的虛擬網路會符合特定需求。 VNet 對等互連不會使用虛擬網路閘道。 如需詳細資訊，請參閱 [VNet 對等互連](../virtual-network/virtual-network-peering-overview.md)。

### <a name="deployment-models-and-methods-for-vnet-to-vnet"></a>VNet 對 VNet 的部署模型和方法

[!INCLUDE [vpn-gateway-table-vnet-to-vnet](../../includes/vpn-gateway-table-vnet-to-vnet-include.md)]

## <a name="ExpressRoute"></a>ExpressRoute (專用的私人連線)

Microsoft Azure ExpressRoute 可讓您將您在內部部署網路擴充至 hello Microsoft 雲端中，透過連線服務提供者所提供的專用私人連接。 透過 ExpressRoute，您可以建立連線 tooMicrosoft 雲端服務，例如 Microsoft Azure、 Office 365 和 CRM Online。 從任意點對任意點 (IP VPN) 網路、點對點乙太網路，或在共置設施上透過連線提供者的虛擬交叉連接，都可以進行連線。

ExpressRoute 連線不會經過 hello 公用網際網路。 這可讓 ExpressRoute 連線 toooffer 詳細可靠性、 速度、 延遲更少和較高的安全性比一般連線透過網際網路 hello。

ExpressRoute 連線不會使用 VPN 閘道，但是會以虛擬網路閘道做為其必要組態的一部分。 ExpressRoute 連線，在 hello 虛擬網路閘道被設定為使用 'ExpressRoute'，而不是 'Vpn' hello 閘道類型。 如需 ExpressRoute 的詳細資訊，請參閱 hello [ExpressRoute 技術概觀](../expressroute/expressroute-introduction.md)。

## <a name="coexisting"></a>站對站及 ExpressRoute 並存連線

ExpressRoute 是直接從您的 WAN 專用連線 (不透過 hello 公用網際網路) tooMicrosoft 服務，包括 Azure。 站對站 VPN 流量的傳輸會透過 hello 加密公用網際網路。 要能 tooconfigure 站對站 VPN 和 ExpressRoute 連線 hello 相同虛擬網路有多項優點。

您可以設定站對站 VPN，安全的容錯移轉路徑做為 ExpressRoute，或使用站對站 Vpn tooconnect toosites 不是您網路的一部分，但透過 ExpressRoute 連接。 請注意，此設定需要兩個虛擬網路閘道的 hello 相同虛擬網路，另一個使用 hello 閘道類型 'Vpn' hello 'ExpressRoute' 利用 hello 閘道類型。

![ExpressRoute 和 VPN 閘道並存連接範例](./media/vpn-gateway-about-vpngateways/expressroute-vpngateway-coexisting-connections-diagram.png)

### <a name="deployment-models-and-methods-for-s2s-and-expressroute"></a>S2S 和 ExpressRoute 的部署模型和方法

[!INCLUDE [vpn-gateway-table-coexist](../../includes/vpn-gateway-table-coexist-include.md)]

## <a name="pricing"></a>價格

[!INCLUDE [vpn-gateway-about-pricing-include](../../includes/vpn-gateway-about-pricing-include.md)]

如需 VPN 閘道之閘道 SKU 的詳細資訊，請參閱[閘道 SKU](vpn-gateway-about-vpn-gateway-settings.md#gwsku)。

## <a name="faq"></a>常見問題集

常見問題集疑問 VPN 閘道的詳細資訊，請參閱 hello [VPN 閘道常見問題集](vpn-gateway-vpn-faq.md)。

## <a name="next-steps"></a>後續步驟

- 規劃您的 VPN 閘道設定。 請參閱 [VPN 閘道的規劃與設計](vpn-gateway-plan-design.md)。
- 檢視 hello [VPN 閘道常見問題集](vpn-gateway-vpn-faq.md)如需詳細資訊。
- 檢視 hello[訂用帳戶和服務限制](../azure-subscription-service-limits.md#networking-limits)。
- 深入了解一些 hello 另一個索引鍵[網路功能](../networking/networking-overview.md)的 Azure。
