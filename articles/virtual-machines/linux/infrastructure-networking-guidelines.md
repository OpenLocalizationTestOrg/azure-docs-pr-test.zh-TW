---
title: "網路基礎結構指導方針-Linux aaaAzure |Microsoft 文件"
description: "深入了解 hello 金鑰設計和實作部署的指導方針 Azure 基礎結構服務中的虛擬網路。"
documentationcenter: 
services: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: a7ebd5da-3c62-45e8-ad90-6c73a37ebeb1
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f3f49b135b1f9bca3fd463e9ff27299fb97908c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-networking-infrastructure-guidelines-for-linux-vms"></a>適用於 Linux VM 的 Azure 網路基礎結構指導方針

[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

本文著重在規劃步驟適用於在 Azure 中的虛擬網路和連接現有的內部部署環境之間所需的了解 hello。

## <a name="implementation-guidelines-for-virtual-networks"></a>虛擬網路的實作指導方針
决策：

* 哪種類型的虛擬網路是否需要 toohost 您的 IT 工作負載或基礎結構 (僅限雲端或跨單位)？
* 跨單位虛擬網路，用於多少位址空間您需要 toohost hello 子網路和 Vm 現在和合理擴充 hello 未來嗎？
* 是您 toocreate 集中的虛擬網路，或是建立每個資源群組的個別虛擬網路？

工作：

* 定義建立 hello 虛擬網路 toobe hello 位址空間。
* 定義子網路與 hello 位址空間的每個的 hello 組。
* 跨單位虛擬網路，定義 hello 組 hello Vm hello 虛擬網路需要 tooreach 中的 hello 在內部部署位置的本機網路位址空間。
* 在內部部署網路小組 tooensure hello 適當設定路由，在建立時使用跨單位虛擬網路。
* 建立使用您的命名慣例的 hello 虛擬網路。

## <a name="virtual-networks"></a>虛擬網路
虛擬網路是必要 toosupport 虛擬機器 (Vm) 之間的通訊。 和實體網路一樣，您可以定義子網路、自訂 IP 位址、DNS 設定、安全性篩選，以及負載平衡。 使用[VPN 閘道](../../vpn-gateway/vpn-gateway-about-vpngateways.md)或[Express Route 電路](../../expressroute/expressroute-introduction.md)，您可以將 Azure 虛擬網路 tooyour 在內部部署網路連接。 您可以深入了解 [虛擬網路及其元件](../../virtual-network/virtual-networks-overview.md)。

透過使用資源群組，您便能彈性地設計您的虛擬網路元件。 Vm 可以將自己的資源群組外的 toovirtual 網路連接。 常見的設計方式是包含您的核心網路基礎結構會受到一般小組 toocreate 集中式資源群組。 Vm 和其應用程式部署 tooseparate 資源群組。 這個方法可讓應用程式擁有者存取 toohello 包含其 Vm 而不需要開啟設定存取 toohello hello 廣虛擬網路資源的資源群組。

## <a name="site-connectivity"></a>站台連線能力
### <a name="cloud-only-virtual-networks"></a>僅限雲端虛擬網路
如果在內部部署使用者和電腦不需要持續連線 tooVMs Azure 的虛擬網路中，您的虛擬網路設計是直接的：

![基本僅雲端虛擬網路圖表](./media/infrastructure-networking-guidelines/vnet01.png)

這種方法通常適用於網際網路對應的工作負載，例如，以網際網路為基礎的 Web 伺服器。 您可以使用 SSH 或點對站 VPN 連線來管理這些 VM。

因為它們並未連接 tooyour 在內部部署網路，僅限 Azure 虛擬網路可以使用 hello 私人 IP 位址空間的任何部分。 hello 位址空間可以是 hello 相同的私用空間中使用內部部署。

### <a name="cross-premises-virtual-networks"></a>跨單位虛擬網路
如果在內部部署使用者和電腦需要持續連線 tooVMs Azure 的虛擬網路中，建立跨單位虛擬網路。 Hello 虛擬網路 tooyour 在內部部署網路連線與 ExpressRoute 或站對站 VPN 連線。

![跨部署虛擬網路圖表](./media/infrastructure-networking-guidelines/vnet02.png)

此設定會 hello Azure 虛擬網路是基本上的雲端擴充功能在內部部署網路。

因為它們連接 tooyour 內部網路，跨單位虛擬網路必須使用 hello 位址空間是唯一的組織所使用的一部分。 在 hello 相同方式，不同公司的位置指派特定的 IP 子網路中，當您擴充出您的網路，Azure 會變成另一個位置。

tooallow 封包 tootravel 從跨單位虛擬網路 tooyour 在內部部署網路，您必須設定 hello 組相關的內部部署位址前置詞為 hello hello 虛擬網路的區域網路定義的一部分。 根據 hello 位址空間 hello 虛擬網路和 hello 集相關的內部部署位置，hello 本機網路中可以有多個位址前置詞。

您可以將轉換僅限雲端的虛擬網路 tooa 跨單位虛擬網路，但最有可能需要您 toore IP 您的虛擬網路位址空間和 Azure 資源。 因此，請仔細考慮虛擬網路是否需要 toobe tooyour 連線在內部部署網路，當您指派的 IP 子網路。

## <a name="subnets"></a>子網路
子網路可讓您 tooorganize 相關資源的可能是以邏輯方式 (例如，一個 Vm 子網路相關聯 toohello 相同的應用程式)，或實體 （例如，每個資源群組的一個子網路）。 您也可以採用子網路隔離技術來提高安全性。

針對跨單位虛擬網路，您應該設計以 hello 的子網路用於內部部署資源的相同慣例。 **Azure 會使用一律 hello hello 每個子網路的位址空間的前三個 IP 位址**。 toodetermine hello 數目所需的位址 hello 子網路，啟動透過計算 hello 現在您需要的 Vm 數目。 供未來成長估計，然後使用 hello 下列資料表 toodetermine hello 大小 hello 子網路。

| 所需的 VM 數目 | 所需的主機位元數 | Hello 子網路的大小 |
| --- | --- | --- |
| 1–3 |3 |/29 |
| 4–11 |4 |/28 |
| 12–27 |5 |/27 |
| 28–59 |6 |/26 |
| 60–123 |7 |/25 |

> [!NOTE]
> 一般在內部部署子網路，hello n 主機位元與子網路的主機位址數目上限是 2<sup> n </sup> -2。 Azure 子網路，hello n 主機位元與子網路的主機位址數目上限是 2<sup> n </sup> – 5 （2 及 3，Azure 會使用每個子網路上的 hello 位址）。
> 
> 

如果您選擇的子網路大小太小，您會有 toore IP，並重新部署 hello 子網路中的 hello Vm。

## <a name="network-security-groups"></a>網路安全性群組
您可以套用到您的虛擬網路的流動的篩選規則 toohello 流量使用網路安全性群組。 您可以建立更細微的篩選規則 toosecure 虛擬網路環境，控制傳入和傳出流量，來源和目的地 IP 範圍，允許連接埠等。網路安全性群組可以是虛擬網路或直接指定虛擬網路介面的 tooa 內套用的 toosubnets。 它會建議 toohave 某種程度的篩選您的虛擬網路上的流量的網路安全性群組。 您可以深入了解 [網路安全性群組](../../virtual-network/virtual-networks-nsg.md)。

## <a name="additional-network-components"></a>其他網路元件
和內部部署實體網路基礎結構一樣，Azure 虛擬網路除了子網路和 IP 位址之外，還可以包含更多其他元件。 當您設計您的應用程式基礎結構，您可能會想 tooincorporate 部分這些額外的元件：

* [VPN 閘道](../../vpn-gateway/vpn-gateway-about-vpngateways.md)-連接 Azure 虛擬網路 tooother Azure 虛擬網路，或透過站對站 VPN 連線連線 tooon 內部部署網路。 實作 Express Route 連線以做為專用的安全連線。 您也可以利用點對站 VPN 連線，來提供使用者直接存取。
* [負載平衡器](../../load-balancer/load-balancer-overview.md) - 視需求針對外部和內部流量提供流量負載平衡。
* [應用程式閘道](../../application-gateway/application-gateway-introduction.md)-HTTP hello 應用程式層進行負載平衡，為 web 應用程式提供某些額外的好處，而不要部署 hello Azure 負載平衡器。
* [Traffic Manager](../../traffic-manager/traffic-manager-overview.md) -DNS 架構流量發佈 toodirect 使用者 toohello 最接近可用的應用程式端點，允許您 toohost 超出不同地區的 Azure 資料中心的應用程式。

## <a name="next-steps"></a>後續步驟
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-linux-infrastructure-guidelines-next-steps.md)]

