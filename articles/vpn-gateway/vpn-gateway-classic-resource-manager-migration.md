---
title: "aaaVPN 閘道傳統 tooResource Manager 移轉 |Microsoft 文件"
description: "此頁面提供 hello 傳統 VPN 閘道 tooResource Manager 移轉的概觀。"
documentationcenter: na
services: vpn-gateway
author: amsriva
manager: rossort
editor: amsriva
ms.assetid: caa8eb19-825a-4031-8b49-18fbf3ebc04e
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/02/2017
ms.author: amsriva
ms.openlocfilehash: c1d84bf5315224c5c8faac53d7957b496ed205ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="vpn-gateway-classic-tooresource-manager-migration"></a>VPN 閘道傳統 tooResource Manager 移轉
VPN 閘道現在可以從傳統 tooResource 管理員部署的模型移轉。 您可以進一步了解 Azure Resource Manager [功能和優點](../azure-resource-manager/resource-group-overview.md)。 我們在本文中詳細說明如何從傳統部署 toonewer 資源管理員 toomigrate 基礎模型。 

VPN 閘道會移轉為傳統 tooResource 管理員從 VNet 移轉的一部分。 此移轉是一次一個 VNet。 沒有其他工具或必要條件 toomigration 方面的需求。 移轉步驟相同 tooexisting VNet 移轉作業，而且會記載於[IaaS 資源移轉頁面](../virtual-machines/windows/migration-classic-resource-manager-ps.md)。 在移轉期間沒有任何資料路徑停機時間，因此現有的工作負載時，會在移轉期間繼續 toofunction 而不會在內部部署連線遺失。 hello 移轉程序期間不會變更 hello hello VPN 閘道與相關聯公用 IP 位址。 這表示，您不需要 tooreconfigure 在內部部署路由器 hello 移轉完成後。  

hello 模型資源管理員 中不同於傳統的模型，並為虛擬網路閘道、 區域網路閘道與連線資源組成。 這些代表 hello VPN 閘道本身，hello 本機站台分別代表在內部部署位址空間和兩個 hello 之間的連線。 移轉完成後，您的閘道不能使用傳統模型，且虛擬網路閘道、區域網路閘道及連線物件上的所有管理作業必須使用 Resource Manager 模式執行。

## <a name="supported-scenarios"></a>支援的案例
最常見的 VPN 連線案例所涵蓋傳統 tooResource Manager 移轉。 支援的 hello 案例包括-

* 點 toosite 連線
* 站台 VPN 閘道 toosite 連線連接 tooon 內部部署位置
* 使用 VPN 閘道的兩個 Vnet 之間的 VNet tooVNet 連線
* 多個 Vnet 連接 toosame 內部部署位置
* 多站台連線能力
* 強制通道已啟用 VNets

不支援的案例包括 -  

* 目前不支援 VNet 隨附 ExpressRoute 閘道與 VPN 閘道。
* 傳輸 VM 擴充功能進行的連線的 tooon 內部部署伺服器案例。 傳輸 VPN 連線能力限制如下所述。

> [!NOTE]
> 資源管理員模型中的 CIDR 驗證是更嚴格的其中一個 hello 比傳統的模型中。 移轉之前請確定指定的傳統的位址範圍開始 hello 移轉之前符合 toovalid CIDR 格式。 CIDR 可以使用任何常見 CIDR 驗證器進行驗證。 移轉時具有無效 CIDR 範圍的 VNet 或本機網站可能會導致失敗的狀態。
> 
> 

## <a name="vnet-toovnet-connectivity-migration"></a>VNet tooVNet 連線移轉
在傳統的 VNet tooVNet 連線藉由建立本機站台 hello 表示法連線 VNet。 客戶都需要的 toocreate 兩個的本機站台代表 hello 需要 toobe 兩個 Vnet 連接在一起。 這些是已則連線的 toohello 對應使用 IPsec 通道 tooestablish 之間連線的 Vnet hello 兩個 Vnet。 此模型會有管理能力的挑戰，因為一個 VNet 中的任何位址範圍變更也必須維持在 hello 對應本機站台的表示法。 Resource Manager 模型中不再需要此因應措施。 hello 的 hello 兩個 Vnet 可以直接使用來達成 'Vnet2Vnet' 連接類型的連接資源之間的連線。 

![螢幕擷取畫面的 VNet tooVNet 移轉。](./media/vpn-gateway-migration/migration1.png)

我們偵測到的 hello 連接的實體 VNet 移轉期間 toocurrent VNet VPN 閘道是另一個 VNet，而確保這兩個 Vnet 移轉完成後，您會不會再看到兩個本機站台代表 hello 另一個 VNet。 已轉換的 tooResource 管理員模型使用兩個 VPN 閘道和 Vnet2Vnet 之類型的兩個連接的兩個 VPN 閘道、 兩個本機站台和它們之間的兩個連線的 hello 傳統模型。

## <a name="transit-vpn-connectivity"></a>傳輸 VPN 連線能力
使用於 VNet 的內部部署連線達成連接 tooanother 直接連接 tooon 內部的 VNet，您可以在拓撲中設定 VPN 閘道。 這是第一個 VNet 中的執行個體的連接的 tooon 內部資源，透過連接是直接連接的 tooon 內部部署的 VNet 中的傳輸 toohello VPN 閘道傳輸 VPN 連線能力。 tooachieve 傳統部署模型中的此設定，您將需要 toocreate 彚代表這兩個連接的 hello VNet 和內部部署位址空間的前置詞的本機站台。 此 representational state transfer 本機站台則接著連接的 toohello VNet tooachieve 傳輸連線。 這個傳統的模型也有類似的管理性挑戰，因為在內部部署位址範圍中的任何變更也必須維持對 hello 本機站台代表的 VNet 和內部部署的 hello 彙總。 在資源管理員支援閘道的 BGP 支援的簡介可簡化管理性，因為 hello 已連線的閘道可以了解在內部部署，而不手動修改 tooprefixes 來自路由。

![傳輸路由案例的螢幕擷取畫面。](./media/vpn-gateway-migration/migration2.png)

因為我們不需要本機站台轉換 VNet tooVNet 連線，hello 傳輸案例將會遺失在內部部署連線間接連線 tooon 內部的 vnet。 hello 的連線中斷，就可以緩解 hello 下列兩種方式，在完成移轉之後- 

* 已連接在一起的 VPN 閘道和 tooon 內部部署上啟用 BGP。 啟用 BGP 還原的連線能力而不需要任何其他組態變更，因為路由是在 VNet 閘道之間了解及通告。 請注意，BGP 選項僅在標準和更高的 SKU 才可使用。
* 建立明確從代表在內部部署位置受影響的 VNet toohello 本機網路閘道連線。 這也可能需要變更 hello 在內部部署路由器 toocreate 上的設定，而且設定 hello IPsec 通道。

## <a name="next-steps"></a>後續步驟
在了解 VPN 閘道移轉支援之後, 請繼續太[平台支援移轉的 IaaS 資源從傳統 tooResource 管理員](../virtual-machines/windows/migration-classic-resource-manager-ps.md)tooget 啟動。

