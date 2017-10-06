---
title: "aaaAzure 虛擬網路對等互連 |Microsoft 文件"
description: "了解 Azure 中的虛擬網路對等互連。"
services: virtual-network
documentationcenter: na
author: NarayanAnnamalai
manager: jefco
editor: tysonn
ms.assetid: eb0ba07d-5fee-4db0-b1cb-a569b7060d2a
ms.service: virtual-network
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/17/2017
ms.author: narayan
ms.openlocfilehash: 46a14b416a7d4389f79a3cd7c55e388b5d312577
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="virtual-network-peering"></a>虛擬網路對等互連
虛擬網路對等互連可讓您 tooconnect 兩個虛擬網路中的 hello 透過同一個地區 hello Azure 骨幹網路。 所以，一旦 hello 兩個虛擬網路會顯示為一個連線之用。 hello 兩個虛擬網路仍會視為不同的資源，來管理，但 hello，所以虛擬網路可在虛擬機器彼此直接通訊，使用私人 IP 位址。

hello hello 在虛擬機器之間的流量所以虛擬網路透過 hello Azure 基礎結構，方式一樣流量路由傳送嗨在虛擬機器之間路由傳送相同的虛擬網路。 使用 虛擬網路對等互連的 hello 優點包括：

* 不同虛擬網路的資源之間具有低延遲、高頻寬連線。
* hello 能力 toouse 資源，例如網路應用裝置和 VPN 閘道 peered 虛擬網路中的轉送點。
* hello 能力 toopeer 兩個虛擬網路建立透過 hello Azure Resource Manager 部署模型或一個 toopeer 透過資源管理員 tooa 透過 hello 傳統部署模型所建立的虛擬網路建立虛擬網路。 讀取 hello[了解 Azure 部署模型](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json)文章 toolearn 更多關於 hello hello 兩個 Azure 部署模型之間的差異。

## <a name="requirements-constraints"></a>需求和限制

* hello 所以虛擬網路必須存在於 hello 相同 Azure 區域。 您可以使用 [VPN 閘道](../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fvirtual-network%2ftoc.json#V2V)，與不同 Azure 區域中的虛擬網路連線。
* hello 所以虛擬網路必須具有非重疊的 IP 位址空間。
* 一旦虛擬網路與另一個虛擬網路對等互連，便無法在虛擬網路中新增或刪除位址空間。
* 虛擬網路對等互連是介於兩個虛擬網路之間。 沒有衍生跨對等項目的可轉移關聯性。 例如，如果 virtualNetworkA 與 virtualNetworkB，所以，virtualNetworkB 所以與 virtualNetworkC virtualNetworkA 是*不*所以 toovirtualNetworkC。
* 您可以對等長的特殊權限的使用者身分存在於兩個不同的訂閱的虛擬網路 (請參閱[特定權限](create-peering-different-deployment-models-subscriptions.md#permissions)) 兩者的訂用帳戶授權 hello 對等互連，而且 hello 訂用帳戶相關聯的 toohello 相同Azure Active Directory 租用戶。 您可以使用[VPN 閘道](../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fvirtual-network%2ftoc.json#V2V)tooconnect 訂用帳戶中的虛擬網路相關聯 toodifferent Active Directory 租用戶。
* 虛擬網路可以所以，如果建立這兩種透過 hello Resource Manager 部署模型，或透過 hello Resource Manager 部署模型建立一個虛擬網路和其他 hello 建立透過 hello 傳統部署模型。 透過 hello 傳統部署模型所建立的兩個虛擬網路不能所以 tooeach 其他，不過。 您可以使用[VPN 閘道](../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fvirtual-network%2ftoc.json#V2V)tooconnect 兩個透過 hello 傳統部署模型所建立的虛擬網路。
* Hello 通訊，所以虛擬網路中的虛擬機器之間不有任何額外的頻寬限制，但沒有 hello 仍然適用的虛擬機器大小而定的最大網路頻寬。 深入了解不同的虛擬機器大小，讀取 hello 的最大網路頻寬 toolearn [Windows](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json)或[Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json)虛擬機器大小的發行項。
* Azure 提供的虛擬機器內部 DNS 名稱解析無法在對等互連虛擬網路中運作。 虛擬機器已是可解析只在 hello 區域虛擬網路內的內部 DNS 名稱。 不過，您可以為虛擬網路的 DNS 伺服器設定連接的虛擬機器 toopeered 虛擬網路。 如需詳細資訊，請閱讀 hello[使用您自己的 DNS 伺服器的名稱解析](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server)發行項。

![基本虛擬網路對等互連](./media/virtual-networks-peering-overview/figure01.png)

## <a name="connectivity"></a>連線能力
對等兩個虛擬網路之後，可能是虛擬網路中的資源可以直接連接 hello 所以虛擬網路中的資源。 hello 兩個虛擬網路具有完整的 IP 層級的連線。

hello 網路延遲為兩部虛擬機器，所以虛擬網路之間的往返 hello 相同與單一虛擬網路內的往返。 hello 網路輸送量根據所允許的 hello 虛擬機器大小成正比 tooits hello 頻寬。 沒有任何額外的限制內 hello 對等互連的頻寬。

直接透過 hello Azure 後端基礎結構，不能透過閘道路由傳送 hello 流量，所以虛擬網路中的虛擬機器之間。

虛擬機器連線的 tooa 虛擬網路可以存取 hello 內部負載平衡的端點 hello 所以虛擬網路中。 如有需要，可以套用網路安全性群組的相關虛擬網路 tooblock 存取 tooother 虛擬網路或子網路中。

在設定虛擬網路對等互連時，您可以開啟或關閉 hello 網路安全性群組規則 hello 虛擬網路之間。 如果您開啟完整所以的虛擬網路 （也就是 hello 預設選項） 之間的連線，您可以套用網路安全性群組 toospecific 子網路或虛擬機器 tooblock 或拒絕特定存取。 深入了解 toolearn 網路安全性群組，讀取 hello[網路安全性群組概觀](virtual-networks-nsg.md)發行項。

## <a name="service-chaining"></a>服務鏈結
您可以設定使用者定義的路由點 toovirtual 電腦的所以虛擬網路中為 hello"下個躍點 」 IP 位址 tooenable 服務鏈結。 服務鏈結可讓您 toodirect 流量從一個虛擬網路 tooa 虛擬應用裝置中透過使用者定義的路由 peered 虛擬網路。

您可以也可以有效地建立中樞和支點類型環境的 hello 集線器可以裝載基礎結構元件，例如網路虛擬應用裝置。 所有 hello 支點虛擬網路可以接著都互連與 hello 中樞虛擬網路。 流量可以透過網路執行 hello 中樞虛擬網路中的虛擬裝置。 簡單地說，虛擬網路對等互連，可讓 hello 下一個躍點 IP 位址在使用者定義的 hello 路由 toobe hello IP 位址的 hello 所以虛擬網路中的虛擬機器。 更多關於使用者定義的路由，讀取 hello toolearn[使用者定義的路由概觀](virtual-networks-udr-overview.md)發行項。

## <a name="gateways-and-on-premises-connectivity"></a>閘道及內部部署連線能力
每個虛擬網路，無論是否有另一個虛擬網路，所以它仍然可以有它自己的閘道，並使用該 tooconnect tooan 在內部部署網路。 您也可以設定[虛擬網路對虛擬網路連線](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md?toc=%2fazure%2fvirtual-network%2ftoc.json)使用閘道，即使 hello 虛擬網路是否對等。

當為虛擬網路互連這兩個選項的設定時，hello hello 虛擬網路之間的流量流經 hello 對等組態 (也就是透過 hello Azure 骨幹)。

當虛擬網路對等時，您也可以做為傳輸點 tooan 內部網路設定 hello 所以虛擬網路中 hello 閘道。 在此情況下，hello 虛擬網路正在使用遠端閘道不能有自己的閘道。 虛擬網路只能擁有一個閘道。 hello 閘道可以是本機或遠端閘道 （hello 所以虛擬網路），如 hello 下列圖片所示：

![VNet 對等互連傳輸](./media/virtual-networks-peering-overview/figure02.png)

Hello 透過不同的部署模型建立的虛擬網路之間的對等關聯性中不支援閘道傳輸。 Hello 對等關聯性中的這兩個虛擬網路必須已建立資源管理員透過閘道傳送 toowork。

當 hello 共用單一 Azure ExpressRoute 連線的虛擬網路是否對等時，hello 它們之間的流量會透過 hello 對等關聯性 (也就是透過 hello Azure 骨幹網路)。 您仍然可以使用本機閘道中每個虛擬網路 tooconnect toohello 內部 expressroute 電路。 此外，您也可以使用共用閘道並設定內部部署連線的傳輸。

## <a name="provisioning"></a>佈建
虛擬網路對等互連是需要權限的作業。 它是個別的函式 hello VirtualNetworks 命名空間之下。 使用者可以被授與特定權限 tooauthorize 對等互連。 具有讀寫存取 toohello 虛擬網路的使用者會自動繼承這些權限。

系統管理員的使用者或是 hello 對等功能的特殊權限的使用者，可以起始另一個虛擬網路對等作業。 如果沒有相符的要求上對等互連 hello 另一端，並且符合其他需求時，如果建立 hello 對等互連。

## <a name="limits"></a>限制
會有單一虛擬網路所允許的對等互連的 hello 數目限制。 如需詳細資訊，請檢閱 hello [Azure 網路限制](../azure-subscription-service-limits.md#networking-limits)。

## <a name="pricing"></a>價格
我們會針對使用虛擬網路對等互連的輸入和輸出流量收取少許費用。 如需詳細資訊，請參閱 hello[定價頁面](https://azure.microsoft.com/pricing/details/virtual-network)。

## <a name="next-steps"></a>接續步驟

* 完成虛擬網路對等互連教學課程。 透過建立 hello 相同，虛擬網路之間建立的虛擬網路對等互連，或存在於不同的部署模型 hello 相同，或不同的訂用帳戶。 完成其中一個 hello 下列案例的教學課程：
 
    |Azure 部署模型  | 訂用帳戶  |
    |---------|---------|
    |兩者皆使用 Resource Manager |[相同](virtual-network-create-peering.md)|
    | |[不同](create-peering-different-subscriptions.md)|
    |一個使用 Resource Manager、一個使用傳統部署模型     |[相同](create-peering-different-deployment-models.md)|
    | |[不同](create-peering-different-deployment-models-subscriptions.md)|

* 深入了解如何 toocreate[中樞和支點網路拓撲](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) 
* 了解所有[虛擬網路對等設定以及如何 toochange 它們](virtual-network-manage-peering.md)
