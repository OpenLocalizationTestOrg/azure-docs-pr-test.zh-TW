---
title: "aaaTroubleshoot 路由-PowerShell |Microsoft 文件"
description: "了解 tootroubleshoot 會路由傳送嗨使用 Azure PowerShell 的 Azure Resource Manager 部署模型中。"
services: virtual-network
documentationcenter: na
author: AnithaAdusumilli
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: bf7dc5e7-9399-460e-8e0d-8992dbed98a6
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/23/2016
ms.author: anithaa
ms.openlocfilehash: 7a07806df5c1d0caee921187e6ad29f6755ab535
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-routes-using-azure-powershell"></a>使用 Azure PowerShell 對路由進行疑難排解
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

### <a name="view-effective-routes-for-a-network-interface"></a>檢視網路介面的有效路由
toosee hello 彙總路由的套用的 tooa 網路介面，完成下列步驟的 hello:

1. 啟動 Azure PowerShell 工作階段與登入 tooAzure。 如果您不熟悉 Azure PowerShell，請參閱 hello[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)發行項。
2. hello 下列命令會傳回名為所有的路由套用 tooa 網路介面*VM1 NIC1* hello 資源群組中*RG1*。
   
       Get-AzureRmEffectiveRouteTable -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1
   
   > [!TIP]
   > 如果您不知道 hello 的網路介面的名稱，輸入下列命令 tooretrieve hello 名稱的所有網路介面卡中資源 group.* hello
   > 
   > 
   
       Get-AzureRmNetworkInterface -ResourceGroupName RG1 | Format-Table Name
   
   hello 下列輸出看起來類似 toohello 輸出 NIC 連線到每個路由套用 toohello 子網路 hello:
   
       Name :
       State : Active
       AddressPrefix : {10.9.0.0/16}
       NextHopType : VNetLocal
       NextHopIpAddress : {}
   
       Name :
       State : Active
       AddressPrefix : {0.0.0.0/16}
       NextHopType : Internet
       NextHopIpAddress : {}
   
   請注意 hello 輸出中的 hello 下列：
   
   * **名稱**: hello 有效路由的名稱可能是空的除非明確指定的使用者定義的路由。 
   * **狀態**： 表示 hello 有效路由的狀態。 可能的值為 "Active" 或 "Invalid"
   * **AddressPrefixes**： 以 CIDR 標記法指定有效路由的 hello hello 位址前置詞。 
   * **nextHopType**： 指出 hello hello 指定路由的下一個躍點。 可能的值為 *VirtualAppliance*、*Internet*、*VNetLocal*、*VNetPeering* 或 *Null*。 UDR 中 *nextHopType* 的值為 **Null** 可能表示是無效路由。 例如，如果**nextHopType**是*VirtualAppliance*與 hello 網路虛擬設備 VM 並未處於執行佈建狀態。 如果**nextHopType**是*VPNGateway*且沒有任何閘道佈建/執行中指定的 VNet 的 hello，hello 路由可能會變成無效。
   * **NextHopIpAddress**： 指定 hello hello hello 有效路由的下一個躍點 IP 位址。
   
   hello 下列命令會傳回 hello 路由更容易的 tooview 資料表中：
   
       Get-AzureRmEffectiveRouteTable -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1 | Format-Table
   
   hello 以下輸出適某些 hello 輸出收到 hello 先前所述的案例：
   
       Name State AddressPrefix NextHopType NextHopIpAddress
       ---- ----- ------------- ----------- ----------------
       Active {10.9.0.0/16} VnetLocal {}
       Active {0.0.0.0/0} Internet {}
3. 沒有任何所列的路由 toohello *Uswest VNet3* VNet (前置詞從 10.10.0.0/16)** *Uswest VNet1* （首碼 10.9.0.0/16） hello 先前步驟中的 hello 輸出中。 Hello 下列圖片所示，hello VNet 對等的連結以 hello *Uswest VNet3* VNet 處於 hello *Disconnected*狀態。
   
    ![](./media/virtual-network-routes-troubleshoot-portal/image4.png)
   
    hello 雙向連結的 hello 對等互連已損毀，其中說明為什麼 VM1 無法連接在 hello tooVM3 *Uswest VNet3* VNet。 為 *WestUS-VNet1* 和 *WestUS-VNet3* VNet 再次設定雙向對等互連連結。 hello hello VNet 對等互連已正確建立連結之後，傳回的輸出如下：
   
        Name State AddressPrefix NextHopType NextHopIpAddress
        ---- ----- ------------- ----------- ----------------
        Active {10.9.0.0/16} VnetLocal {}
        Active {10.10.0.0/16} VNetPeering {}
        Active {0.0.0.0/0} Internet {}
   
    一旦決定 hello 問題，您可以新增、 移除或變更路由及路由表。 下列命令 toosee hello 命令的清單類型 hello 因此使用 toodo:
   
        Get-Help *-AzureRmRouteConfig

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
  * Hello 流量可能影響網路安全性群組 (NSG) 規則。 如需詳細資訊，請參閱 hello[疑難排解網路安全性群組](virtual-network-nsg-troubleshoot-powershell.md)發行項。

