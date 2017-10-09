---
title: "與 Azure VPN 閘道的高可用性組態 aaaOverview |Microsoft 文件"
description: "本文提供使用 Azure VPN 閘道的高可用性組態選項概觀。"
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: 
ms.assetid: a8bfc955-de49-4172-95ac-5257e262d7ea
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/24/2016
ms.author: yushwang
ms.openlocfilehash: 316293b9ac79645bf9bb9e89fbc4aa8f3eacd209
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="highly-available-cross-premises-and-vnet-to-vnet-connectivity"></a>高可用性跨單位和 VNet 對 VNet 連線
本文針對使用 Azure VPN 閘道的跨單位和 VNet 對 VNet 連線提供高可用性組態選項的概觀。

## <a name = "activestandby"></a>關於 Azure VPN 閘道備援
每個 Azure VPN 閘道都是由作用中-待命組態中的兩個執行個體組成。 任何已規劃的維修或非計劃的中斷發生 toohello 作用中的執行個體，會自動接管 （容錯移轉） hello 待命執行個體，並將其恢復 hello S2S VPN 或 VNet 對 VNet 連線中。 hello 切換會短暫中斷。 若是計劃性維護，應 10 too15 秒內還原 hello 連線。 未規劃的問題，hello 連接復原將會比較長，關於 1 分鐘 too1 和半分鐘 hello 最壞的情況下。 P2S VPN 用戶端連線 toohello 閘道 hello P2S 連線將會中斷而且 hello 的使用者需要 tooreconnect 從 hello 用戶端電腦。

![作用中-待命](./media/vpn-gateway-highlyavailable/active-standby.png)

## <a name="highly-available-cross-premises-connectivity"></a>高可用性跨單位連線
tooprovide 更佳的可用性，對您的跨內部部署連線，有幾個選項：

* 多個內部部署 VPN 裝置
* 主動-主動 Azure VPN 閘道
* 兩者的組合

### <a name = "activeactiveonprem"></a>多個內部部署 VPN 裝置
Hello 下列圖表所示，您可以從您在內部部署網路 tooconnect tooyour Azure VPN 閘道，使用多個 VPN 裝置：

![多個內部部署 VPN](./media/vpn-gateway-highlyavailable/multiple-onprem-vpns.png)

這個組態可提供多個使用中的通道，從 hello 相同 Azure VPN 閘道 tooyour 在內部部署中的裝置 hello 相同的位置。 有一些需求和限制︰

1. 您需要 toocreate 多 S2S VPN 連線從您的 VPN 裝置 tooAzure。 當您從 hello 連接多個 VPN 裝置相同的內部部署網路 tooAzure，您需要從 Azure VPN 閘道 toohello 區域網路閘道的 toocreate 一個區域網路閘道的每個 VPN 裝置，以及一個連線。
2. 對應 tooyour VPN 裝置 hello 區域網路閘道必須 hello"GatewayIpAddress"屬性中唯一的公用 IP 位址。
3. 此組態需要 BGP。 代表的 VPN 裝置每個區域網路閘道必須擁有 hello"BgpPeerIpAddress"屬性中指定唯一 BGP 對等體 IP 位址。
4. 在每個區域網路閘道的 hello AddressPrefix 屬性欄位不得重疊。 您應該指定 /32 hello"BgpPeerIpAddress"hello AddressPrefix 欄位中，例如 10.200.200.254/32 CIDR 格式。
5. 您應該使用 BGP tooadvertise hello 相同的前置詞的 hello 相同的內部部署網路首碼 tooyour Azure VPN 閘道和 hello 流量會透過轉送這些通道同時。
6. 每個連接納入 hello Azure VPN 閘道，10 Basic 和 Standard Sku 的通道數目上限和 30 HighPerformance sku。 

此設定會 hello Azure VPN 閘道是仍在使用中-待命模式，因此 hello 相同容錯移轉行為以及所述，仍會發生短暫中斷[上方](#activestandby)。 但這項設定可防範內部部署網路和 VPN 裝置發生錯誤或中斷。

### <a name="active-active-azure-vpn-gateway"></a>主動-主動 Azure VPN 閘道
您現在可以建立 Azure VPN 閘道在主動-主動組態中，其中的 hello 閘道 Vm，就會建立 S2S VPN 通道 tooyour 在內部部署 VPN 裝置，為顯示 hello 下列兩個執行個體的圖表：

![主動-主動](./media/vpn-gateway-highlyavailable/active-active.png)

在此組態中，每個 Azure 閘道執行個體都會有唯一的公用 IP 位址，而每個建立的 IPsec/IKE S2S VPN 通道 tooyour 在內部部署 VPN 裝置區域網路閘道與連接中指定。 請注意，這兩個 VPN 通道是實際的部份 hello 相同的連接。 您仍將會需要您在內部部署 VPN 裝置 tooaccept tooconfigure 或建立兩個 S2S VPN 通道 toothose 兩個 Azure VPN 閘道的公用 IP 位址。

由於 hello Azure 閘道器執行個體都在主動-主動組態中，從您的 Azure 虛擬網路 tooyour hello 流量在內部網路將會同時路由傳送透過這兩個通道，即使在內部部署 VPN 裝置可能優先於一個通道hello 其他。 請注意的 hello 相同的 TCP 或 UDP 流量將一律周遊 hello 相同通道或路徑，但除非維護事件發生在其中一個 hello 執行個體。

當已規劃的維修或非計劃的事件發生時 tooone 閘道執行個體時，該執行個體 tooyour hello IPsec 通道內部部署 VPN 裝置將會中斷。 hello 對應路由 VPN 裝置上的應該移除或撤銷自動使 hello 流量將會切換 toohello 透過其他使用中 IPsec 通道。 上 hello Azure 端，透過 hello 參數將會自動從 hello 影響執行個體 toohello 作用中執行個體。

### <a name="dual-redundancy-active-active-vpn-gateways-for-both-azure-and-on-premises-networks"></a>雙重備援︰Azure 和內部部署網路的主動-主動 VPN 閘道
hello 最可靠的方式是 toocombine hello 主動-主動閘道網路與 Azure 上的 hello 如下圖所示。

![雙重備援](./media/vpn-gateway-highlyavailable/dual-redundancy.png)

這裡您建立和設定 hello Azure VPN 閘道在主動-主動組態中，建立兩個區域網路閘道和兩個連線，您的兩個內部部署 VPN 裝置如上面所述。 hello 結果會是 4 的 IPsec 通道，您的 Azure 虛擬網路與內部部署網路之間的完整網狀的連線。

所有的閘道和通道 hello Azure 端從作用中，所以 hello 流量會散佈到所有的 4 通道同時，雖然每個 TCP 或 UDP 流量會再次遵循 hello 相同通道或從路徑 hello Azure 端。 即使所分配 hello 流量，您可能會看到稍微更佳的輸送量，透過 hello IPsec 通道，這項設定的 hello 主要目標是要讓高可用性。 而且很難 tooprovide hello 度量 toohello 本質統計 hello 分配，因為不同的應用程式流量條件將會影響 hello 彙總輸送量。

此拓撲需要兩個區域網路閘道及兩個連線 toosupport hello 對內部部署 VPN 裝置，和 BGP 是必要的 tooallow hello 兩個連線 toohello 相同的內部部署網路。 這些需求都是相同 hello 與 hello[上方](#activeactiveonprem)。 

## <a name="highly-available-vnet-to-vnet-connectivity-through-azure-vpn-gateways"></a>透過 Azure VPN 閘道的高可用性 VNet 對 VNet 連線
hello 相同主動-主動組態也可以套用 tooAzure VNet 對 VNet 連線。 您可以建立兩個虛擬網路，主動-主動 VPN 閘道，並將它們連接在一起的 tooform hello 完整相同 mesh 4 hello 圖表下方的 hello 中所示的兩個 Vnet 之間的通道之連線：

![VNet 對 VNet](./media/vpn-gateway-highlyavailable/vnet-to-vnet.png)

這可確保永遠都會有一組通道 hello 兩個虛擬網路間所有的計劃性的維護事件，提供更好的可用性。 即使 hello 相同的跨單位連線的拓撲需要兩個連接，如上所示的 hello VNet 對 VNet 拓撲將需要每個閘道只能有一個連線。 此外，BGP 是選擇性，除非透過 hello VNet 對 VNet 連線的傳輸路由是必要的。

## <a name="next-steps"></a>後續步驟
請參閱[跨單位和 VNet 對 VNet 連線設定主動-主動 VPN 閘道](vpn-gateway-activeactive-rm-powershell.md)步驟 tooconfigure 主動-主動跨單位和 VNet 對 VNet 連線。

