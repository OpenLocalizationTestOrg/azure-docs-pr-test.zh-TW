---
title: "aaaInternal 負載平衡器概觀 |Microsoft 文件"
description: "內部負載平衡器和其功能的概觀。Azure 和可能的案例 tooconfigure 內部端點的負載平衡器的運作方式"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: tysonn
ms.assetid: 36065bfe-0ef1-46f9-a9e1-80b229105c85
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: 9a901aad224d8821c154e130e142699d57282b25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="internal-load-balancer-overview"></a>內部負載平衡器概觀

不同於 hello 網際網路對向負載平衡器，hello 內部負載平衡器 (ILB) 會指示流量只有 tooresources hello 雲端服務，或使用 VPN tooaccess hello Azure 基礎結構內。 hello 基礎結構會限制存取 toohello 負載平衡虛擬 IP 位址 (Vip 的雲端服務或虛擬網路)，讓它們絕對不會直接公開的 tooan 網際網路端點。 這可讓在 Azure 中的企業營運 (LOB) 應用程式 toorun 內部一行，並從 hello 雲端內或從存取資源的內部。

## <a name="why-you-may-need-an-internal-load-balancer"></a>為何需要內部負載平衡器

Azure 內部負載平衡 (ILB) 可在位於雲端服務或虛擬網路 (具有區域範圍) 中的虛擬機器之間提供負載平衡。 如需使用 hello 和具有區域範圍的虛擬網路的組態資訊，請參閱[地區虛擬網路](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/)在 hello Azure 部落格。 已針對同質群組設定的現有虛擬網路無法使用 ILB。

ILB 能夠達到下列類型的負載平衡的 hello:

* 在雲端服務中，從虛擬機器 tooa 集位於 hello 內的虛擬機器的相同雲端服務 （請參閱圖 1）。
* 虛擬網路內的虛擬機器位於 hello hello 虛擬網路 tooa 集合中的虛擬機器從相同雲端服務的 hello 虛擬網路 （請參閱圖 2）。
* 跨單位虛擬網路中，從內部部署電腦 tooa 組位於 hello 內的虛擬機器的相同雲端服務的 hello 虛擬網路 （請參閱圖 3）。
* 網際網路對向、 多層式應用程式中 hello 後端層並非網際網路對向，但需要的負載平衡流量從 hello 網際網路對向層。
* 在不需要額外負載平衡器硬體或軟體的情況下，針對裝載於 Azure 中的 LOB 應用程式進行負載平衡。 在內部部署伺服器納入 hello 的一組電腦的流量進行負載平衡。

## <a name="internet-facing-multi-tier-applications"></a>網際網路面向的多層式應用程式

hello web 層有網際網路用戶端的網際網路對向端點，而且是一組負載平衡的一部分。 hello 負載平衡器會將連入流量的 TCP 連接埠 443 (HTTPS) toohello 網頁伺服器的 web 用戶端。

hello 資料庫伺服器位於 ILB 端點 hello 網頁伺服器用於儲存體。 此資料庫服務的負載平衡的端點的流量進行負載平衡到 hello ILB 集合中的 hello 的資料庫伺服器。

下列影像顯示 hello hello 網際網路對向多層式應用程式內 hello 相同雲端服務。

![單一雲端服務的內部負載平衡](./media/load-balancer-internal-overview/IC736321.png)

圖 1 - 網際網路面向的多層式應用程式

Hello ILB 部署 tooa 不同雲端服務，比 hello hello ILB 取用一個 hello 服務時的多層式應用程式的另一個可能的使用。

雲端服務使用相同的虛擬網路將會有的 hello 存取 toohello ILB 端點。 下列影像顯示前端 web 伺服器位於不同雲端服務從 hello 資料庫後端，並使用 hello hello hello 中的只剩下 ILB 端點相同虛擬網路。

![雲端服務之間的內部負載平衡](./media/load-balancer-internal-overview/IC744147.png)

圖 2 - 位於不同雲端服務的前端伺服器

## <a name="intranet-line-of-business-applications"></a>內部網路企業營運應用程式

從用戶端 hello 與內部網路上的流量達到負載平衡的 LOB 伺服器使用 VPN 連線 tooAzure 網路 hello 組。

hello 用戶端電腦會從 Azure VPN 服務使用點 toosite VPN 存取 tooan IP 位址。 它可讓 hello 使用 hello hello ILB 端點之後託管的 LOB 應用程式。

![內部負載平衡使用點 toosite VPN](./media/load-balancer-internal-overview/IC744148.png)

圖 3: hello LB 端點之後託管的 LOB 應用程式

Hello LOB 的另一個案例是 toohave 站 toosite VPN toohello 虛擬網路已 hello ILB 端點。 這可讓內部網路流量路由傳送 toobe toohello ILB 端點。

![內部負載平衡使用站台 toosite VPN](./media/load-balancer-internal-overview/IC744150.png)

圖 4-在內部部署網路流量路由傳送 toohello ILB 端點

## <a name="limitations"></a>限制

內部負載平衡器組態不支援 SNAT。 在 hello 本文內容，SNAT 是指 tooport 偽裝來源網路位址轉譯。  這適用於的 tooscenarios 負載平衡器集區中的 VM 需要 tooreach hello 個別內部負載平衡器的前端 IP 位址的地方。 內部負載平衡器不支援這種情況。 負載平衡 toohello 引發 hello 流程 VM hello 流程時，會發生連接失敗。 對於這類情況，您必須使用 Proxy 形式負載平衡器。

## <a name="next-steps"></a>後續步驟

[Azure Resource Manager 的 Azure Load Balancer 支援](load-balancer-arm.md)

[開始設定網際網路面向的負載平衡器](load-balancer-get-started-internet-arm-ps.md)

[開始設定內部負載平衡器](load-balancer-get-started-ilb-arm-ps.md)

[設定負載平衡器分配模式](load-balancer-distribution-mode.md)

[設定負載平衡器的閒置 TCP 逾時設定](load-balancer-tcp-idle-timeout.md)
