---
title: "aaaTroubleshoot 路由-入口網站 |Microsoft 文件"
description: "了解如何在 hello Azure Resource Manager 部署模型使用 tootroubleshoot 路由 hello Azure 入口網站。"
services: virtual-network
documentationcenter: na
author: AnithaAdusumilli
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: bdd8b6dc-02fb-4057-bb23-8289caa9de89
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/23/2016
ms.author: anithaa
ms.openlocfilehash: 579bae91ef3200852032b3953d3cc5d26deada86
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-routes-using-hello-azure-portal"></a>疑難排解使用 hello Azure 入口網站的路由
> [!div class="op_single_selector"]
> * [Azure 入口網站](virtual-network-routes-troubleshoot-portal.md)
> * [PowerShell](virtual-network-routes-troubleshoot-powershell.md)
>
>

如果您遇到網路連線問題 tooor 您 Azure 虛擬機器 (VM)，路由可能影響您 VM 的流量。 本文章提供的路由 toohelp 進一步的疑難排解的診斷功能的概觀。

路由表與子網路相關聯，在該子網路中的所有網路介面 (NIC) 上都有效。 hello 下列類型的路由可以是套用的 tooeach 網路介面：

* **系統路由︰** 在 Azure 虛擬網路 (VNet) 中建立的每個子網路預設都有系統路由表，允許本機 VNet 流量、透過 VPN 閘道的內部部署流量以及網際網路流量。 對等互連的 VNet 也有系統路由。
* **BGP 路由：**傳播 toonetwork 介面透過 ExpressRoute 或站台對站 VPN 連線。 深入了解 BGP 路由閱讀 hello[與 VPN 閘道的 BGP](../vpn-gateway/vpn-gateway-bgp-overview.md)和[ExpressRoute 概觀](../expressroute/expressroute-introduction.md)文件。
* **使用者定義的路由 (UDR):**如果您使用網路虛擬裝置，或會強制通道流量 tooan 透過站對站 VPN 的內部部署網路，您可能需要使用者定義的路由 (UDRs) 與子網路路由表相關聯。 如果您不熟悉 UDRs，讀取 hello[使用者定義的路由](virtual-networks-udr-overview.md#user-defined-routes)發行項。

以 hello 各種路由可以是套用的 tooa 網路介面，它可以是難以 toodetermine 為有效的彙總的路由。 toohelp VM 網路連線問題疑難排解，您可以檢視所有的 hello 有效路由的網路介面在 hello Azure Resource Manager 部署模型。

## <a name="using-effective-routes-tootroubleshoot-vm-traffic-flow"></a>使用有效路由 tootroubleshoot VM 流量
本文使用 hello tootroubleshoot hello 有效會路由傳送網路介面的範例 tooillustrate 為下列案例：

VM (*VM1*) 連接 toohello VNet (*VNet1*，前置詞： 10.9.0.0/16) 失敗 tooconnect tooa VM(VM3) 新 peered VNet 中 (*VNet3*，前置詞 10.10.0.0/16)。 有沒有 UDRs 或 BGP 路由套用的 tooVM1 NIC1 網路連線介面 toohello VM，只有系統路由會套用。

本文說明如何 toodetermine hello 原因 hello 連線失敗，使用 Azure 資源管理部署模型中的有效路由的功能。
雖然 hello 範例會使用只有系統路由，hello 相同的步驟可以使用的 toodetermine 透過任何路由類型是傳入和傳出的連線失敗。

> [!NOTE]
> 如果您的 VM 有連結的多個 NIC，請針對每個 hello Nic toodiagnose 網路連線問題 tooand 從 VM 檢查有效的路由。
>
>

### <a name="view-effective-routes-for-a-virtual-machine"></a>檢視虛擬機器的有效路由
toosee hello 彙總路由的套用的 tooa VM，完成下列步驟的 hello:

1. 登入 toohello https://portal.azure.com 在 Azure 入口網站。
2. 按一下**更多服務**，然後按一下 **虛擬機器**hello 的清單中，會出現。
3. 從出現的 hello 清單中選取 VM tootroubleshoot 和選項的 VM 刀鋒視窗隨即出現。
4. 按一下 [診斷並解決問題]，然後選取常見的問題。 例如，**我無法連線 toomy Windows VM**已選取。

    ![](./media/virtual-network-routes-troubleshoot-portal/image1.png)
5. Hello 下列圖片所示步驟就會出現在 hello 問題：

    ![](./media/virtual-network-routes-troubleshoot-portal/image2.png)

    按一下*有效路由*在 hello 清單中的建議步驟。
6. hello**有效路由**刀鋒視窗隨即出現，如 hello 下列圖片所示：

    ![](./media/virtual-network-routes-troubleshoot-portal/image3.png)

    如果您的 VM 只有一個 NIC，預設會選取它。 如果您有多個 NIC，選取您想要的 tooview hello 有效路由的 hello NIC。

   > [!NOTE]
   > 如果 hello VM 相關聯 hello NIC 不是處於執行中狀態，將不會顯示有效的路由。 只有 hello 前 200 個有效的路由中會顯示 hello 入口網站。 Hello 完整清單，請按一下**下載**。 您可以進一步篩選 hello 結果從 hello 下載的.csv 檔案。
   >
   >

    請注意 hello 輸出中的 hello 下列：

   * **來源**： 指出 hello 路由類型。 系統路由會顯示為 *Default*，UDR 會顯示為 *User*，閘道路由 (靜態或 BGP) 則會顯示為 *VPNGateway*。
   * **狀態**： 表示 hello 有效路由的狀態。 可能的值為 *Active* 或 *Invalid*。
   * **AddressPrefixes**： 以 CIDR 標記法指定有效路由的 hello hello 位址前置詞。
   * **nextHopType**： 指出 hello hello 指定路由的下一個躍點。 可能的值為 *VirtualAppliance*、*Internet*、*VNetLocal*、*VNetPeering* 或 *Null*。 UDR 中 *nextHopType* 的值為 **Null** 可能表示是無效路由。 例如，如果**nextHopType**是*VirtualAppliance*與 hello 網路虛擬設備 VM 並未處於執行佈建狀態。 如果**nextHopType**是*VPNGateway*且沒有任何閘道佈建/執行中指定的 VNet 的 hello，hello 路由可能會變成無效。
7. 沒有任何所列的路由 toohello *Uswest VNET3* VNet (前置詞 10.10.0.0/16) 與 hello *Uswest VNet1* （首碼 10.9.0.0/16） hello 上一個步驟中的 hello 圖片中。 在下列圖片 hello，hello 對等互連連結將處於 hello *Disconnected*狀態：

    ![](./media/virtual-network-routes-troubleshoot-portal/image4.png)

    hello 雙向連結的 hello 對等互連已損毀，其中說明為什麼 VM1 無法連接在 hello tooVM3 *Uswest VNet3* VNet。
8. hello 下圖顯示 hello 路由之後建立 hello 雙向對等互連連結：

    ![](./media/virtual-network-routes-troubleshoot-portal/image5.png)

強制通道和路由評估更多疑難排解的情況下，讀取 hello[考量](virtual-network-routes-troubleshoot-portal.md#considerations)本文一節。

### <a name="view-effective-routes-for-a-network-interface"></a>檢視網路介面的有效路由
如果網路流量流程受到特定網路介面 (NIC) 影響，您可以直接在 NIC 上檢視有效路由的完整清單。 toosee hello 彙總路由的套用的 tooa NIC，完成下列步驟的 hello:

1. 登入 toohello https://portal.azure.com 在 Azure 入口網站。
2. 按一下 [更多服務]，然後按一下 [網路介面]
3. Hello NIC，hello 名稱清單中搜尋，或從出現的 hello 清單中選取。 在此範例中選取了 [VM1-NIC1]  。
4. 選取**有效路由**在 hello**網路介面**刀鋒視窗中，hello 下列圖片所示：

       ![](./media/virtual-network-routes-troubleshoot-portal/image6.png)

    hello**範圍**選取預設值 toohello 網路介面。

      ![](./media/virtual-network-routes-troubleshoot-portal/image7.png)

### <a name="view-effective-routes-for-a-route-table"></a>檢視路由表的有效路由
當路由表中修改使用者定義的路由 (UDRs)，您可能想 tooreview hello 影響的特定 VM 上的 hello 路由。 路由表可以與任意數目的子網路產生關聯。 您現在可以檢視所有 hello 有效路由，針對所有 hello Nic 套用指定的路由表，而不需要從指定的路由表刀鋒視窗中的 hello tooswitch 內容。

在此範例中，路由表 (*UDRouteTable*) 中指定了 UDR (*UDRoute*)。 此路由傳送來自的所有網際網路流量*Subnet1*在 hello *Uswest VNet1* VNet，透過網路的虛擬設備 (NVA)，在*Subnet2*的 hello 相同的 VNet。 hello 路由以 hello 下列圖片所示：

![](./media/virtual-network-routes-troubleshoot-portal/image8.png)

toosee hello 彙總的路由的路由表，完成下列步驟的 hello:

1. 登入 toohello https://portal.azure.com 在 Azure 入口網站。
2. 按一下 [更多服務]，然後按一下 [路由表]
3. Hello 路由表的搜尋 hello 清單想 toosee 彙總的路由並加以選取。 在此範例中選取了 **UDRouteTable** 。 選取的 hello 路由表的刀鋒視窗隨即出現，hello 下列圖片所示：

    ![](./media/virtual-network-routes-troubleshoot-portal/image9.png)
4. 選取**有效路由**在 hello**路由表**刀鋒視窗。 hello**範圍**設定 toohello 您選取的路由表。
5. 路由表可以套用的 toomultiple 子網路。 選取 hello**子網路**想 tooreview 從 hello 清單。 在此範例中選取了 [Subnet1]  。
6. 選取 [網路介面] 。 列出所有 Nic 已連線的 toohello 選取子網路。 在此範例中選取了 [VM1-NIC1]  。

    ![](./media/virtual-network-routes-troubleshoot-portal/image10.png)

   > [!NOTE]
   > 如果不與執行中的 VM 關聯 hello NIC，則會顯示沒有有效的路由。
   >
   >

## <a name="considerations"></a>考量
檢閱 hello 的路由清單時，請注意幾件事 tookeep 傳回：

* 路由是根據 UDR、BGP 和系統路由之間的最長首碼比對 (LPM)。 如果有多個路由 hello 相同 LPM 相符，然後根據 hello 順序的源頭選取路由：

  * 使用者定義路由
  * BGP 路由
  * 系統 (預設) 路由

    使用有效的路由，您只能看到有效路由的 LPM 根據所有 hello 了路由的相符項目。 顯示 hello 路由以給定的 nic 如何評估，這讓您輕鬆 tootroubleshoot 特定路由且可能影響從您的 VM 的連線。
* 如果您有 UDRs 並傳送流量 tooa 網路的虛擬設備 (NVA)，與*VirtualAppliance*為**nextHopType**，確定已啟用 IP 轉送 hello NVA 接收 hello 流量或捨棄的封包。
* 如果已啟用強制通道，所有傳出網際網路流量會路由的 tooon 內部。 RDP/SSH 從網際網路 tooyour VM 可能不適用於此設定，根據如何 hello 內部處理這個流量。
  符合下列其中一個條件時，可以啟用強制通道︰
  * 使用站台對站台 VPN 時，將使用者定義路由 (UDR) 的 nextHopType 設定為 VPNGateway
  * 透過 BGP 公告預設路由
* Vnet 對等互連流量 toowork 正確的系統路由**nextHopType** *VNetPeering*的 hello 所以 VNet 的前置詞的範圍必須存在。 如果這類的路由不存在，而且 hello 對等互連的 VNet 連結正確無誤：
  * 如果是新建立的對等互連連結，請等候幾秒鐘並重試。 它有時會接受路途 toopropagate tooall hello 網路介面的子網路。
  * Hello 流量可能影響網路安全性群組 (NSG) 規則。 如需詳細資訊，請參閱 hello[疑難排解網路安全性群組](virtual-network-nsg-troubleshoot-portal.md)發行項。
