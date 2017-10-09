---
title: "aaaTroubleshoot 網路安全性群組-入口網站 |Microsoft 文件"
description: "了解如何在 hello Azure Resource Manager 部署 tootroubleshoot 網路安全性群組的相關模型使用 hello Azure 入口網站。"
services: virtual-network
documentationcenter: na
author: AnithaAdusumilli
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: a54feccf-0123-4e49-a743-eb8d0bdd1ebc
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/23/2016
ms.author: anithaa
ms.openlocfilehash: 0d3d2110fe1507f36e3b933de924a0876db2747a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-network-security-groups-using-hello-azure-portal"></a>疑難排解使用 hello Azure 入口網站的網路安全性群組
> [!div class="op_single_selector"]
> * [Azure 入口網站](virtual-network-nsg-troubleshoot-portal.md)
> * [PowerShell](virtual-network-nsg-troubleshoot-powershell.md)
> 
> 

如果您在虛擬機器 (VM) 上設定網路安全性群組 (Nsg)，而遭遇 VM 連線問題，這篇文章會提供的 Nsg toohelp 進一步的疑難排解診斷功能的概觀。

Nsg 可讓您 toocontrol hello 類型的流量進出虛擬機器 (Vm) 的流程。 Nsg 可以套用的 toosubnets Azure 虛擬網路 (VNet)、 網路介面 (NIC)，或兩者。 hello 套用有效的規則 tooa NIC 是存在於 hello Nsg 套用 tooa NIC 和 hello 它連接至子網路中的 hello 規則的彙總。 這些 NSG 的規則有時候會互相衝突，影響 VM 的網路連線。  

套用您的 VM Nic 上，您可以檢視 Nsg，從所有 hello 有效的安全性規則。 本文示範如何使用這些規則在 tootroubleshoot VM 連線問題 hello Azure Resource Manager 部署模型。 如果您不熟悉 VNet 和 NSG 的概念，請參閱 hello[虛擬網路](virtual-networks-overview.md)和[網路安全性群組](virtual-networks-nsg.md)概觀文件。

## <a name="using-effective-security-rules-tootroubleshoot-vm-traffic-flow"></a>使用有效的安全性規則 tootroubleshoot VM 流量
常見的連接問題的範例，則 hello 案例所示：

一個名為 *VM1* 的 VM 位於 *WestUS-VNet1* VNet 內的 *Subnet1* 子網路。 嘗試 tooconnect toohello 透過 TCP 連接埠 3389 使用 RDP 的 VM 會失敗。 在這兩個 hello NIC 套用 Nsg *VM1 NIC1* hello 子網路和*Subnet1*。 Hello hello 網路介面相關聯的 NSG 中允許流量 tooTCP 連接埠 3389 *VM1 NIC1*，不過 TCP ping tooVM1 的連接埠 3389 失敗。

雖然這個範例會使用 TCP 連接埠 3389，hello 下列步驟可以使用的 toodetermine 透過任何連接埠是傳入和傳出的連線失敗。

### <a name="vm"></a>檢視虛擬機器的有效安全性規則
完成下列步驟 tootroubleshoot Nsg vm 的 hello:

您可以從 hello VM 本身的 NIC 上檢視 hello 有效的安全性規則的完整的清單。 您也可以新增、 修改及刪除 hello 有效的規則刀鋒視窗中，從子網路和 NIC 的 NSG 規則，如果您有權限 tooperform 這些作業。

1. 登入 toohello https://portal.azure.com 在 Azure 入口網站。
2. 按一下**更多服務**，然後按一下 **虛擬機器**hello 的清單中，會出現。
3. 從出現的 hello 清單中選取 VM tootroubleshoot 和選項的 VM 刀鋒視窗隨即出現。
4. 按一下 [診斷並解決問題]，然後選取常見的問題。 例如，**我無法連線 toomy Windows VM**已選取。 
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image1.png)
5. Hello 下列圖片所示步驟就會出現在 hello 問題： 
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image2.png)
   
    按一下*有效安全性群組規則*在 hello 清單中的建議步驟。
6. hello**取得有效的安全性規則**刀鋒視窗隨即出現，如 hello 下列圖片所示：
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image3.png)
   
    請注意下列各節 hello 圖片的 hello:
   
   * **範圍：**設定得*VM1*，hello 在步驟 3 中選取的 VM。
   * **網路介面︰** *VM1-NIC1* 。 一個 VM 可以有多個網路介面 (NIC)。 每個 NIC 只能有唯一的有效安全性規則。 進行疑難排解時，您可能需要 tooview hello 有效的安全性規則的每個 nic。
   * **關聯 Nsg:** Nsg 可以套用的 tooboth hello NIC 和 hello 子網路 hello NIC 連線到。 Hello 圖片中 NSG 已套用的 tooboth hello NIC 和 hello 它連接至子網路。 您可以按一下 hello NSG 名稱 toodirectly 修改 hello Nsg 中的規則。
   * **VM1 nsg 索引標籤：** hello hello 圖片中顯示的規則清單是 hello NSG 套用 toohello nic。 每當建立一個 NSG 時，Azure 就會建立幾個預設的規則。 您無法移除 hello 預設規則，但您可以使用較高優先順序的規則覆寫它們。 深入了解預設規則，讀取 hello toolearn [NSG 概觀](virtual-networks-nsg.md#default-rules)發行項。
   * **目的地資料行：**一些 hello 規則有文字 hello 資料行中，而有些則擁有位址前置詞。 hello 文字時建立 hello 預設標籤套用 toohello 安全性規則名稱。 hello 標記是系統提供的識別碼，代表多個前置詞。 選取的規則與標記，例如*AllowInternetOutBound*，列出在 hello hello 前置詞**位址首碼**刀鋒視窗。
   * **下載：** hello 的規則清單中可能會很長。 您可以按一下來下載.csv 檔案的 hello 規則進行離線分析**下載**和儲存 hello 檔案。
   * **AllowRDP**輸入的規則： 這個規則允許 RDP 連線 toohello VM。
7. 按一下 hello **Subnet1 NSG** hello NSG 中的索引標籤 tooview hello 有效規則套用 toohello 子網路，hello 下列圖片所示： 
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image4.png)
   
    請注意 hello *denyRDP* **輸入**規則。 在 hello 網路介面套用的規則之前，會評估輸入的規則套用於 hello 子網路。 Hello 拒絕規則套 hello 子網路，因為 hello 要求 tooconnect tooTCP 3389 會失敗，因為 hello 允許規則在 hello NIC 不會加以評估。 
   
    hello *denyRDP*規則是 hello 原因 hello RDP 連線失敗的原因。 將它移除，應該解決 hello 問題。
   
   > [!NOTE]
   > 如果關聯的 hello VM hello 與 NIC 不是處於執行中狀態，或 Nsg 未套用的 toohello NIC 或子網路，會顯示任何規則。
   > 
   > 
8. tooedit NSG 規則中，按一下  *Subnet1 NSG*在 hello**關聯 Nsg** > 一節。
   這會開啟 hello **Subnet1 NSG**刀鋒視窗。 您可以直接編輯 hello 規則上的 **輸入安全性規則**。
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image7.png)
9. 移除 hello 之後*denyRDP* hello 中的輸入的規則**Subnet1 NSG**並加入*allowRDP*規則 hello 有效的規則清單看起來像下列圖片的 hello:
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image8.png)
   
    確認開啟 RDP 連線 toohello VM，或使用 hello PsPing 工具開啟 TCP 連接埠 3389。 您可以進一步了解 PsPing 讀取 hello [PsPing 下載頁面](https://technet.microsoft.com/sysinternals/psping.aspx)。

### <a name="nic"></a>檢視網路介面的有效安全性規則
如果您 VM 的流量會影響特定 nic，您可以藉由完成下列步驟的 hello 檢視 hello 從 hello 網路介面內容 hello NIC 的有效規則的完整清單：

1. 登入 toohello https://portal.azure.com 在 Azure 入口網站。
2. 按一下**更多服務**，然後按一下 **網路介面**hello 的清單中，會出現。
3. 選取某個網路介面。 在下列圖片 hello，NIC 命名為*VM1 NIC1*已選取。
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image5.png)
   
    請注意該 hello**範圍**toohello 選取的網路介面設定。 深入了解 toolearn hello 額外的資訊顯示，讀取 hello 的步驟 6**疑難排解 Nsg vm**本文一節。
   
   > [!NOTE]
   > 從網路介面移除 NSG，hello 子網路的 nsg 關聯仍然有效上指定 NIC 的 hello 在此情況下，hello 輸出只會顯示 hello 子網路 NSG 的規則。 規則只會顯示 hello NIC 是否附加的 tooa VM。
   > 
   > 
4. 您可以直接編輯與 NIC 和子網路相關聯之 NSG 的規則。 toolearn 作法，請閱讀步驟 8 的 hello**檢視虛擬機器的有效的安全性規則**本文一節。

## <a name="nsg"></a>檢視網路安全性群組 (NSG) 的有效安全性規則
當修改 NSG 規則，您可能想 tooreview hello 影響的特定 VM 上的 hello 規則。 您可以檢視所有 hello Nic 給定的 NSG 套用 hello 有效的安全性規則的完整清單而不需要從給定 NSG 刀鋒視窗中的 hello tooswitch 內容。 tootroubleshoot NSG，完成下列步驟的 hello 內的有效規則：

1. 登入 toohello https://portal.azure.com 在 Azure 入口網站。
2. 按一下**更多服務**，然後按一下 **網路安全性群組**hello 的清單中，會出現。
3. 選取某個 NSG。 在下列圖片 hello，選取名為 VM1 nsg NSG。
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image6.png)
   
    請注意下列各節的 hello 上一張圖片的 hello:
   
   * **範圍：**設定 toohello 選取 NSG。
   * **虛擬機器：**當 NSG 是套用的 tooa 子網路，而是套用的 tooall 介面附加的 tooall Vm 連接的 toohello 子網路。 此清單顯示套用此 NSG 的所有 VM。 您可以從 hello 清單中選取任何 VM。
     
     > [!NOTE]
     > 如果 NSG 套用的 tooonly 空白的子網路，不會列 Vm。 如果 NSG 套用的 tooa NIC 不是與 VM 相關聯，這些 Nic 也不會列。 
     > 
     > 
   * **網路介面：**一個 VM 可以有多個網路介面。 您可以選取網路介面附加的 toohello 選取 VM。
   * **AssociatedNSGs:**最 tootwo 多處理能力的 NIC 可以有任何時候，有效 Nsg，一個套用 toohello NIC，hello 其他 toohello 子網路。 雖然 hello 範圍當做 VM1 nsg，如果 hello NIC 具有有效的子網路 NSG，hello 輸出會顯示這兩個 Nsg。
4. 您可以直接編輯與 NIC 或子網路相關聯之 NSG 的規則。 toolearn 作法，請閱讀步驟 8 的 hello**檢視虛擬機器的有效的安全性規則**本文一節。

深入了解 toolearn hello 額外的資訊顯示，讀取 hello 的步驟 6**檢視虛擬機器的有效的安全性規則**本文一節。

> [!NOTE]
> 雖然子網路和 NIC 各有一個 NSG 套用 toothem，NSG 可以關聯的 toomultiple Nic 和多重子網路。
> 
> 

## <a name="considerations"></a>考量
請考慮 hello 疑難排解連線問題時，下列點：

* 預設 NSG 規則將會封鎖從 hello 對內的存取網際網路和允許 VNet 輸入流量。 規則應該明確加入 tooallow 輸入視需要從網際網路存取。
* 如果沒有造成 VM 的網路連線 toofail NSG 安全性規則，hello 問題可能是因為：
  * Hello VM 作業系統內執行的防火牆軟體
  * 為虛擬設備或內部部署流量設定的路由。 網際網路流量可以透過強制通道的重新導向的 tooon 單位。 RDP/SSH 連線從 hello 網際網路 tooyour VM 可能不適用於此設定，根據 hello 在內部部署網路硬體如何處理這個流量。 讀取 hello[疑難排解路由](virtual-network-routes-troubleshoot-powershell.md)文章 toolearn 如何 toodiagnose 路由問題，可能索性 hello 和出的流量傳送 hello VM。 
* 如果您有所以 Vnet，根據預設，hello VIRTUAL_NETWORK 標記會自動擴展 tooinclude 前置詞所以 vnet。 您可以檢視這些前置詞中 hello **ExpandedAddressPrefix**清單，tootroubleshoot 對等互連連線問題相關 tooVNet。 
* 有效的安全性規則只會顯示於是否有與 hello VM NIC 和或子網路的 NSG 相關聯。 
* 如果沒有相關聯 hello NIC 的 Nsg 或子網路，而且您有指派 tooyour VM 的公用 IP 位址，所有連接埠將會開啟以供對內及對外存取。 如果 hello VM 的公用 IP 位址，強烈建議套用 Nsg toohello NIC 或子網路。

