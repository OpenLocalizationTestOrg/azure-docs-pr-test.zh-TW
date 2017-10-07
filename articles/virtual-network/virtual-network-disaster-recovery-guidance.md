---
title: "在 hello 事件影響到 Azure 虛擬網路的 Azure 服務中斷的 aaaWhat toodo |Microsoft 文件"
description: "了解哪些 toodo hello 影響到 Azure 虛擬網路的 Azure 服務中斷事件中。"
services: virtual-network
documentationcenter: 
author: NarayanAnnamalai
manager: jefco
editor: 
ms.assetid: ad260ab9-d873-43b3-8896-f9a1db9858a5
ms.service: virtual-network
ms.workload: virtual-network
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2016
ms.author: narayan;aglick
ms.openlocfilehash: db022d2a042d255cf8ec6afb68cd8436aeecfe08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="virtual-network--business-continuity"></a>虛擬網路 – 商務持續性
## <a name="overview"></a>概觀
虛擬網路 (VNet) 是網路的您 hello 雲端中的邏輯表示法。 它可讓您 toodefine 自己私用 IP 位址空間與區段 hello 網路至子網路。 Vnet 做為信任界限 toohost 您的計算資源，例如 Azure 虛擬機器和雲端服務 （web/背景工作角色）。 VNet 可讓您直接裝載於它的 hello 資源之間的私用 IP 通訊。 虛擬網路也可以透過下列其中一 hello 混合式選項，例如 VPN 閘道或 ExpressRoute 連結的 tooan 在內部部署網路。

VNet 建立區域的 hello 範圍內。 您可以使用相同的位址空間中兩個不同區域建立 Vnet (也就是美國東部和美國西部但無法連接它們 tooone 直接另一個)。 

## <a name="business-continuity"></a>商務持續性
可能有數種不同的方式會讓您的應用程式中斷。 給定的區域可能會被切斷到期 tooa 天然災害或由於多個裝置/伺服器 tooa 失敗部分損毀。 hello 對影響 hello VNet 服務會在每種情況不同。

**問： 該怎麼辦的中斷 tooan 整個地區的 hello 事件中？亦即，如果區域是完全截止 tooa 天然災害到期？發生什麼事的 toohello hello 區域中裝載的虛擬網路？**

答： hello 虛擬網路和 hello 資源 hello 受影響區域會維持為 hello 服務中斷的 hello 期間無法存取。

![簡單的虛擬網路圖表](./media/virtual-network-disaster-recovery-guidance/vnet.png)

**問： 我可以 toodo 重新建立 hello 不同區域中的相同虛擬網路？**

答︰「虛擬網路」(VNet) 是非常輕量型的資源。 您可以叫用 Azure Api toocreate VNet 與 hello 相同位址不同的區域中的空間。 toore-建立 hello 相同的環境的 hello 在受影響的區域，您必須 toomake API 呼叫 toore-部署雲端服務 （web/背景工作角色） 和您所擁有的虛擬機器。 您也必須 toospin VPN 閘道及 tooyour 在內部部署網路連線，如果您已在內部部署連線 （例如，在混合式部署）。

找到 hello 相關指示，來建立 VNet[這裡](virtual-networks-create-vnet-arm-pportal.md)。 

**問︰是否可以事先在另一個區域中重新建立指定區域中的 VNet 複本？**

答: [是]，您可以建立兩個 Vnet 使用 hello 相同的私人 IP 位址空間和時間之前有兩個不同區域中的資源。 如果客戶已裝載網際網路對向 hello VNet 中的服務，它們可能已設定為使用中的 Traffic Manager toogeo 路由流量 toohello 區域。 不過，客戶無法連接兩個 Vnet 與 hello 相同位址空間 tootheir 在內部部署網路將會造成路由問題。 客戶可以在 hello 發生災害時，在某個區域 VNet 遺失連接 hello hello 與相符的位址空間 tootheir 在內部部署網路的可用區域中的其他 VNet。

找到 hello 相關指示，來建立 VNet[這裡](virtual-networks-create-vnet-arm-pportal.md)。

