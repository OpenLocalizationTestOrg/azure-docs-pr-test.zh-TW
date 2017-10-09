---
title: "aaaUser 定義路由，並在 Azure 中的 IP 轉送 |Microsoft 文件"
description: "了解 tooconfigure 使用者定義路由 (UDR) 和 IP 轉送 tooforward 流量 toonetwork 在 Azure 中的虛擬應用裝置。"
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
ms.assetid: c39076c4-11b7-4b46-a904-817503c4b486
ms.service: virtual-network
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f1f1d46166d5a7c776f472b7ade1354d943ece10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="user-defined-routes-and-ip-forwarding"></a>使用者定義的路由和 IP 轉送

當您在 Azure 中新增虛擬機器 (Vm) tooa 虛擬網路 (VNet) 時，您會發現 hello Vm 會自動無法 toocommunicate 彼此 hello 網路上。 您不需要 toospecify 閘道，即使 hello Vm 位於不同的子網路。 hello 也適用於來自 hello Vm toohello 通訊公用網際網路，以及混合式連線從 Azure tooyour 擁有資料中心已存在時，甚至 tooyour 與內部網路。

這個流量可能是通訊的因為 Azure 會使用一系列的系統路由 toodefine IP 流量流動的方式。 系統路由控制 hello hello 下列案例中的通訊流程：

* 從 hello 相同子網路。
* 從 VNet 中的子網路 tooanother。
* 從 Vm toohello 網際網路。
* 從透過 VPN 閘道 VNet tooanother VNet。
* 從 VNet tooanother VNet 透過 VNet 對等 （服務鏈結）。
* 從透過 VPN 閘道的 VNet tooyour 在內部部署網路。

hello 圖顯示簡單的安裝過程中，使用 VNet、 兩個子網路，以及一些 Vm，以及 hello 可讓 IP 流量 tooflow 系統路由。

![Azure 中的系統路由](./media/virtual-networks-udr-overview/Figure1.png)

雖然系統路由 hello 使用有助於流量自動為您的部署，有些情況是您想在其中 toocontrol hello 透過路由傳送封包的虛擬應用裝置。 您可以因此藉由建立使用者定義的路由指定 hello 反而流動 tooa 特定子網路 toogo tooyour 虛擬設備的封包的下一個躍點和啟用 IP 轉送的 hello 執行為虛擬應用裝置 hello VM。

hello 下圖示範使用者定義的路由與 IP 轉送 tooforce 封包透過第三個的子網路上的虛擬應用裝置從另一個 toogo 傳送 tooone 子網路。

![Azure 中的系統路由](./media/virtual-networks-udr-overview/Figure2.png)

> [!IMPORTANT]
> 套用的 tootraffic 離開子網路的任何資源 （例如，網路介面附加 tooVMs） hello 子網路中為使用者定義的路由。 您無法建立路由 toospecify 如何流量輸入子網路 hello 網際網路，從執行個體。 hello 應用裝置會轉寄流量 toocannot 處於 hello 出 hello 流量來源的相同子網路。 請永遠為您的應用裝置建立個別的子網路。 
> 
> 

## <a name="route-resource"></a>路由資源
透過路由表定義在 hello 實體網路上的每個節點上的 TCP/IP 網路路由傳送封包。 路由表是一系列個別的路由使用 toodecide 其中 tooforward 封包根據 hello 目的地 IP 位址。 路由包含 hello 下列：

| 屬性 | 說明 | 條件約束 | 考量 |
| --- | --- | --- | --- |
| 位址首碼 |hello 目的地 CIDR toowhich hello 路由套用，例如 10.1.0.0/16。 |必須是有效的 CIDR 範圍，代表 hello 上的位址公用網際網路、 Azure 虛擬網路或在內部部署資料中心。 |請確定 hello**位址首碼**未包含 hello 的 hello 位址**下個躍點位址**，否則會進入迴圈，從 hello 來源 toohello 下一個躍點會不進入程式封包hello 目的地。 |
| 下一個躍點類型 |Azure 躍點 hello 封包的 hello 類型應該傳送至。 |必須是 hello 的下列值的其中一個： <br/> **虛擬網路**。 代表 hello 區域虛擬網路。 例如，如果您有兩個子網路，10.1.0.0/16 和 10.2.0.0/16 在 hello 相同虛擬網路，hello hello 路由表中的每個子網路的路由會有的下一個躍點值*虛擬網路*。 <br/> **虛擬網路閘道**。 代表 Azure S2S VPN 閘道。 <br/> **網際網路**。 代表 hello hello Azure 基礎結構所提供的預設網際網路閘道。 <br/> **虛擬應用裝置**。 表示加入 tooyour Azure 虛擬網路的虛擬應用裝置。 <br/> **無**。 代表黑洞。 完全不會轉送轉送 tooa 黑洞的封包。 |請考慮使用**虛擬設備**toodirect 流量 tooa VM 或 Azure 負載平衡器的內部 IP 位址。  此類型允許 IP 位址，如下所述的 hello 的規格。 請考慮使用**無**輸入 toostop 封包從流動 tooa 指定目的地。 |
| 下一個躍點位址 |下一個躍點位址 hello 包含 hello 應該要轉送封包的 IP 位址。 下一個躍點值只能用在 hello 下一個躍點類型所在的路由*虛擬設備*。 |必須是可連線到 hello 其中要套用 hello 使用者定義的路由，而不需要透過虛擬網路內的 IP 位址**虛擬網路閘道**。 hello IP 位址有 toobe hello 相同虛擬網路，它會套用，或 peered 虛擬網路上。 |如果 hello IP 位址代表 VM，請確定您已啟用[IP 轉送](#IP-forwarding)hello VM 的 Azure 中。 Hello IP 位址代表 hello 內部 IP 位址的 Azure 負載平衡器，請確定您已符合負載平衡每個連接埠規則，如果您希望 tooload 平衡。|

在 Azure PowerShell 中的某些 hello"NextHopType"值具有不同的名稱：

* 虛擬網路是 VnetLocal
* 虛擬網路閘道是 VirtualNetworkGateway
* 虛擬應用裝置是 VirtualAppliance
* 網際網路是 Internet
* 無是 None

### <a name="system-routes"></a>系統路由
建立虛擬網路中每個子網路會自動關聯於路由表含有下列系統的路由規則的 hello:

* **本機 VNet 規則**：此規則會自動針對虛擬網路中的每個子網路建立。 它會指定在 hello VNet 中的 hello Vm 之間沒有直接的連結，並沒有任何中繼的下一個躍點。
* **在內部部署規則**： 此規則會套用 tooall 流量 toohello 在內部部署位址範圍，並使用做為下一個躍點目的地 hello 的 VPN 閘道。
* **網際網路規則**： 此規則會處理所有流量 toohello 公用網際網路 (位址前置詞 0.0.0.0/0) 和使用 hello 基礎結構網際網路閘道為 hello 下個躍點的所有流量 toohello 網際網路。

### <a name="user-defined-routes"></a>使用者定義的路由
針對大多數環境您只需要已定義 azure 的 hello 系統路由。 不過，您可能需要 toocreate 路由表，並將一個或多個路由在特定情況下，例如：

* 強制通道透過在內部部署網路 toohello 網際網路。
* 在 Azure 環境中使用虛擬應用裝置。

在上述的 hello 案例，您會有 toocreate 路由表，並加入使用者定義的路由 tooit。 您可以有多個路由表，而且 hello 相同的路由表可以是相關聯的 tooone 或更多子網路。 而每個子網路只能關聯的 tooa 單一路由表。 所有 Vm 和子網路中的雲端服務都使用 hello 路由相關聯資料表 toothat 子網路。

子網路會依賴系統路由，直到路由表相關聯的 toohello 子網路。 一旦關聯存在之後，在使用者定義的路由和系統路由之間，就會根據最長前置詞比對 (LPM) 完成。 如果沒有以 hello 相同 LPM 相符，然後選取路由的多個路由會根據其原來 hello 順序中：

1. 使用者定義的路由
2. BGP 路由 (使用 ExpressRoute 時)
3. 系統路由

toolearn 如何 toocreate 使用者定義的路由，請參閱[tooCreate 路由的方式，並啟用 Azure 中的 IP 轉送](virtual-network-create-udr-arm-template.md)。

> [!IMPORTANT]
> 使用者定義的路由會套用的 tooAzure Vm 和雲端服務。 比方說，如果您想 tooadd 您在內部部署網路與 Azure 之間的防火牆虛擬應用裝置，您必須 toocreate 您 Azure 的路由表的使用者定義路由轉送所有流量 toohello 在內部部署位址空間 toohello 虛擬應用裝置。 您也可以加入使用者定義的路由 (UDR) toohello GatewaySubnet tooforward 從內部部署 tooAzure 的所有流量透過 hello 虛擬設備。 這是近期內的新增功能。
> 
> 

### <a name="bgp-routes"></a>BGP 路由
如果您有您在內部部署網路與 Azure 之間 ExpressRoute 連線，您可以從您的內部部署網路 tooAzure 啟用 BGP toopropagate 路由。 這些 BGP 路由會以 hello 與系統路由和使用者的相同方式定義每個 Azure 子網路路由。 如需詳細資訊，請參閱 [ExpressRoute 簡介](../expressroute/expressroute-introduction.md)。

> [!IMPORTANT]
> 您可以設定您 Azure 環境 toouse 強制通道透過在內部部署網路，藉由建立使用者定義的路由為 hello 下一個躍點使用 hello VPN 閘道子網路 0.0.0.0/0。 不過，這只有在您使用的是 VPN 閘道，而不是 ExpressRoute 時，才有作用。 若是 Expressroute，強制通道是透過 BGP 設定。
> 
> 

## <a name="ip-forwarding"></a>IP 轉送
如上所述，hello 主要原因 toocreate 的其中一個使用者定義路由是 tooforward 流量 tooa 虛擬應用裝置。 虛擬應用裝置只是執行以某種方式，例如防火牆或 NAT 裝置的應用程式使用 toohandle 網路流量的 VM。

此 VM 必須是能夠 tooreceive 連入流量的虛擬應用裝置中並未提及 tooitself。 tooallow VM tooreceive 流量定址 tooother 目的地，您必須啟用 IP 轉送 hello VM。 這是 Azure 設定，不是在 hello 客體作業系統設定。

## <a name="next-steps"></a>後續步驟
* 了解如何太[hello Resource Manager 部署模型中建立路由](virtual-network-create-udr-arm-template.md)並 toosubnets 產生關聯。 
* 了解如何太[hello 傳統部署模型中建立路由](virtual-network-create-udr-classic-ps.md)並 toosubnets 產生關聯。

