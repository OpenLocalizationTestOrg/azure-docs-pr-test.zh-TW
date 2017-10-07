---
title: "aaaAzure 虛擬網路 |Microsoft 文件"
description: "了解 Azure 虛擬網路概念和功能。"
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 9633de4b-a867-4ddf-be3c-a332edf02e24
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/23/2017
ms.author: jdial
ms.openlocfilehash: 55ae6a131d882ad893aeffcaa4127bc47beda552
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-network"></a>Azure 虛擬網路

hello Azure 虛擬網路服務可讓您 toosecurely 連接的 Azure 資源 tooeach 其他與虛擬網路 (Vnet)。 VNet 是網路的您自己 hello 雲端中的表示法。 VNet 是 hello 的隔離的邏輯專用的 Azure 雲端 tooyour 訂用帳戶。 您也可以連接的 Vnet tooyour 在內部部署網路。 hello 下列圖片顯示 hello Azure 虛擬網路服務的 hello 功能：

![網路圖表](./media/virtual-networks-overview/virtual-network-overview.png)

深入了解下列 Azure 虛擬網路功能的 hello toolearn 按一下 hello 功能：
- **[隔離︰](#isolation)**VNet 會彼此隔離。 您可以建立個別的開發、 測試和生產環境的 Vnet 該使用 hello 相同的 CIDR 位址區塊。 相反地，您可以建立多個使用不同 CIDR 位址區塊的 VNet 並將這些網路連接在一起。 您可以將 VNet 分成多個子網路。 Azure 提供的內部名稱解析的 Vm 和雲端服務角色執行個體連接 tooa VNet。 您可以選擇性地設定 VNet toouse 您自己的 DNS 伺服器，而不是使用 Azure 的內部名稱解析。
- **[網際網路連線：](#internet)** 連接的 tooa VNet 擁有的所有 Azure 虛擬機器 (VM) 和雲端服務角色執行個體存取 toohello 網際網路，根據預設。 視需要您也可以啟用輸入的存取 toospecific 資源。
- **[Azure 資源連接：](#within-vnet)**  Azure 資源，例如雲端服務和 Vm 可以連接的 toohello 相同的 VNet。 hello 資源可以連接 tooeach 其他使用私人 IP 位址，即使它們位於不同子網路。 Azure 預設之間提供路由子網路、 Vnet，與在內部部署網路，因此您不需要 tooconfigure，管理路由。
- **[VNet 連線：](#connect-vnets)**  Vnet 可以是其他連接的 tooeach，讓資源連線 tooany VNet toocommunicate 與任何其他 VNet 上的任何資源。
- **[在內部部署連線：](#connect-on-premises)**  Vnet 必須透過網路與 Azure 之間的私人網路連線或透過站對站 VPN 連線的連線的 tooon 內部網路是透過網際網路 hello。
- **[流量篩選︰](#filtering)**可以依照來源 IP 位址和連接埠、目的地 IP 位址和連接埠以及通訊協定的輸入和輸出，篩選 VM 和雲端服務角色執行個體網路流量。
- **[路由︰](#routing)**您可以設定您自己的路由，或使用透過網路閘道的 BGP 路由，選擇性地覆寫 Azure 的預設路由。

## <a name = "isolation"></a>網路隔離和分割

您可以在每個 Azure [訂用帳戶](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription)和 Azure [區域](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#region)內實作多個 VNet。 每個 VNet 會與其他 VNet 隔離。 對於每個 VNet，您可以︰
- 使用公用和私人 (RFC 1918) 位址指定自訂私人 IP 位址空間。 Azure 資源連接的 toohello VNet 私人 IP 位址會從指派 hello 您指派的位址空間。
- 區段 hello VNet 到一個或多個子網路，並配置 hello VNet 位址空間 tooeach 子網路的一部分。
- 使用 Azure 提供名稱解析，或指定您自己的 DNS 伺服器以供資源連接 tooa VNet。 深入了解讀取 hello 的 Vnet 中的名稱解析 toolearn [Vm 和雲端服務的名稱解析](virtual-networks-name-resolution-for-vms-and-role-instances.md)發行項。

## <a name = "internet"></a>連接 toohello 網際網路
所有資源連線的 tooa VNet 都有預設的傳出連線 toohello 網際網路。 hello 資源的 hello 私用 IP 位址是來源網路位址轉譯 (SNAT) tooa 公用 IP 位址的 hello Azure 基礎結構。 深入了解輸出的網際網路連線，讀取 hello toolearn[了解 Azure 中的輸出連線](..\load-balancer\load-balancer-outbound-connections.md?toc=%2fazure%2fvirtual-network%2ftoc.json#standalone-vm-with-no-instance-level-public-ip-address)發行項。 您可以透過實作自訂路由和流量篩選變更 hello 預設連線。

toocommunicate 輸入網際網路而不需要 SNAT，資源必須指派的公用 IP 位址的 hello 網際網路或 toocommunicate 輸出的 toohello tooAzure 資源。 更多關於公用 IP 位址，讀取 hello toolearn[公用 IP 位址](virtual-network-public-ip-address.md)發行項。

## <a name="within-vnet"></a>連線 Azure 資源
您可以連接數個 Azure 資源 tooa VNet，例如虛擬機器 (VM)、 雲端服務、 應用程式服務環境和虛擬機器規模集。 Vm 連接 tooa VNet 中的子網路的網路介面 (NIC)。 深入了解 Nic，讀取 hello toolearn[網路介面](virtual-network-network-interface.md)發行項。

## <a name="connect-vnets"></a>連線虛擬網路

您可以連接的 Vnet tooeach 其他，啟用資源彼此連接 tooeither VNet toocommunicate 跨 Vnet。 您可以使用一個或兩個下列選項 tooconnect Vnet tooeach 其他 hello:
- **對等互連：**可讓資源連線 toodifferent Azure Vnet hello 內相同的 Azure 位置 toocommunicate 彼此。 hello 頻寬和延遲在 hello Vnet 是 hello 相同好像 hello 資源連線的 toohello 相同的 VNet。 深入了解對等互連，toolearn 讀取 hello[虛擬網路對等互連](virtual-network-peering-overview.md)發行項。
- **VNet 對 VNet 連線：**可讓資源連線 toodifferent Azure VNet 內 hello 相同，或不同的 Azure 位置。 不同於對等互連，VNet 之間的頻寬有限，因為流量必須通過 Azure VPN 閘道。 深入了解 Vnet 連線 VNet 對 VNet 連線後，讀取 hello toolearn[設定 VNet 對 VNet 連線](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json)發行項。

## <a name="connect-on-premises"></a>Tooan 在內部部署網路連線

您可以連接您在內部部署網路 tooa VNet hello 下列選項的任意組合：
- **點對站虛擬私人網路 (VPN):**單一的電腦已連線的 tooyour 網路與 hello VNet 之間建立。 這種連接類型是如果您剛開始使用 Azure 或開發人員，很好的因為您需要少量或沒有變更 tooyour 現有的網路。 hello 連線會使用透過 hello 網際網路 hello PC 與 hello VNet 之間 hello SSTP 通訊協定 tooprovide 加密通訊。 點對站 VPN 的 hello 延遲是無法預測的因為 hello 流量會周遊 hello 網際網路。
- **站對站 VPN：**建立於 VPN 裝置與 Azure VPN 閘道之間。 這種連接類型可讓您授權 tooaccess VNet 任何內部部署資源。 hello 連接是透過 hello 網際網路在內部部署裝置與 hello Azure VPN 閘道之間提供加密的通訊的 IPSec/IKE VPN。 站對站連線的 hello 延遲是無法預測的因為 hello 流量會周遊 hello 網際網路。
- **Azure ExpressRoute：**透過 ExpressRoute 合作夥伴，建立於您的網路與 Azure 之間。 此連線是私人連線。 流量不會周遊 hello 網際網路。 ExpressRoute 連線的 hello 延遲是可預測，，因為流量不會周遊 hello 網際網路。

深入了解所有 hello 先前連線的選項，讀取 hello toolearn[連線拓撲圖表](../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fvirtual-network%2ftoc.json#diagrams)發行項。

## <a name="filtering"></a>篩選網路流量
您可以篩選使用 hello 下列選項之一或兩者的子網路之間的網路流量：
- **網路安全性群組 (NSG):**每個 NSG 可以包含多個傳入和傳出的安全性規則可讓您依來源和目的地 IP 位址、 連接埠和通訊協定的 toofilter 流量。 您可以套用 NSG tooeach NIC 的 VM 中。 您也可以套用 NSG toohello 子網路的 NIC，或其他 Azure 資源，連線到。 深入了解 Nsg，讀取 hello toolearn[網路安全性群組](virtual-networks-nsg.md)發行項。
- **網路虛擬裝置 (NVA)：**NVA 是可執行以下軟體的 VM：執行防火牆等網路功能的軟體。 檢視可用 NVAs 清單在 hello [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/category/networking?page=1&subcategories=appliances)。 此外，也可取得提供 WAN 最佳化和其他網路流量功能的 NVA。 NVA 通常使用於使用者定義或 BGP 路由。 您也可以使用 Vnet 之間 NVA toofilter 流量。

## <a name="routing"></a>路由網路流量

Azure 會建立可讓資源連線的 tooany 子網路中任何 VNet toocommunicate 彼此，預設路由表。 您可以實作，或這兩個下列選項 toooverride hello hello Azure 建立的預設路由：
- **使用者定義的路由：**您可以建立自訂的路由表控制流量所在 toofor 路由的路由與每個子網路。 更多關於使用者定義的路由，讀取 hello toolearn[使用者定義的路由](virtual-networks-udr-overview.md)發行項。
- **BGP 路由：**如果您使用 Azure VPN 閘道或 ExpressRoute 連接的 VNet tooyour 在內部部署網路連接，您可以將傳播 BGP 路由 tooyour Vnet。

## <a name="pricing"></a>價格

虛擬網路、子網路、路由表或網路安全性群組均免費。 輸出網際網路頻寬使用量、公用 IP 位址、虛擬網路對等互連、VPN 閘道和 ExpressRoute 都有各自的價格結構。 檢視 hello[虛擬網路](https://azure.microsoft.com/pricing/details/virtual-network)， [VPN 閘道](https://azure.microsoft.com/pricing/details/vpn-gateway)，和[ExpressRoute](https://azure.microsoft.com/pricing/details/expressroute)定價的詳細資訊的頁面。

## <a name="faq"></a>常見問題集

tooreview 常見問題集關於虛擬網路，請參閱 hello[虛擬網路常見問題集](virtual-networks-faq.md)發行項。


## <a name="next-steps"></a>接續步驟

- 建立第一個 VNet 和 hello hello 中的步驟，以連接少數的 Vm tooit[建立第一個虛擬網路](virtual-network-get-started-vnet-subnet.md)發行項。
- 完成在 hello hello 步驟建立點對站連線 tooa VNet[設定點對站連線](../vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json)發行項。
- 深入了解一些 hello 另一個索引鍵[網路功能](../networking/networking-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json)的 Azure。
