---
title: "aaaTroubleshoot 網路安全性群組-PowerShell |Microsoft 文件"
description: "了解如何在 hello Azure Resource Manager 部署 tootroubleshoot 網路安全性群組的相關模型使用 Azure PowerShell。"
services: virtual-network
documentationcenter: na
author: AnithaAdusumilli
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: 4c732bb7-5cb1-40af-9e6d-a2a307c2a9c4
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/23/2016
ms.author: anithaa
ms.openlocfilehash: 95fd60fa72cf6d17fa990e3c3eb7d980878f7c15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-network-security-groups-using-azure-powershell"></a>使用 Azure PowerShell 為網路安全性群組疑難排解
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

## <a name="detailed-troubleshooting-steps"></a>詳細的疑難排解步驟
完成下列步驟 tootroubleshoot Nsg vm 的 hello:

1. 啟動 Azure PowerShell 工作階段與登入 tooAzure。 如果您不熟悉使用 Azure PowerShell，請參閱 hello[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)發行項。
2. 輸入下列命令 tooreturn 所有 NSG 規則都套用 tooa NIC 名為 hello *VM1 NIC1* hello 資源群組中*RG1*:
   
        Get-AzureRmEffectiveNetworkSecurityGroup -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1
   
   > [!TIP]
   > 如果您不知道 NIC hello 名稱，請輸入下列命令 tooretrieve hello 名稱的資源群組中的所有 Nic 的 hello: 
   > 
   > `Get-AzureRmNetworkInterface -ResourceGroupName RG1 | Format-Table Name`
   > 
   > 
   
    hello 下列文字是針對 hello 傳回 hello 有效的規則輸出的範例*VM1 NIC1* NIC:
   
        NetworkSecurityGroup   : {
                                   "Id": "/subscriptions/[Subscription ID]/resourceGroups/RG1/providers/Microsoft.Network/networkSecurityGroups/VM1-NIC1-NSG"
                                 }
        Association            : {
                                   "NetworkInterface": {
                                     "Id": "/subscriptions/[Subscription ID]/resourceGroups/RG1/providers/Microsoft.Network/networkInterfaces/VM1-NIC1"
                                   }
                                 }
        EffectiveSecurityRules : [
                                 {
                                 "Name": "securityRules/allowRDP",
                                 "Protocol": "Tcp",
                                 "SourcePortRange": "0-65535",
                                 "DestinationPortRange": "3389-3389",
                                 "SourceAddressPrefix": "Internet",
                                 "DestinationAddressPrefix": "0.0.0.0/0",
                                 "ExpandedSourceAddressPrefix": [… ],
                                 "ExpandedDestinationAddressPrefix": [],
                                 "Access": "Allow",
                                 "Priority": 1000,
                                 "Direction": "Inbound"
                                 },
                                 {
                                 "Name": "defaultSecurityRules/AllowVnetInBound",
                                 "Protocol": "All",
                                 "SourcePortRange": "0-65535",
                                 "DestinationPortRange": "0-65535",
                                 "SourceAddressPrefix": "VirtualNetwork",
                                 "DestinationAddressPrefix": "VirtualNetwork",
                                 "ExpandedSourceAddressPrefix": [
                                  "10.9.0.0/16",
                                  "168.63.129.16/32",
                                  "10.0.0.0/16",
                                  "10.1.0.0/16"
                                  ],
                                 "ExpandedDestinationAddressPrefix": [
                                  "10.9.0.0/16",
                                  "168.63.129.16/32",
                                  "10.0.0.0/16",
                                  "10.1.0.0/16"
                                  ],
                                  "Access": "Allow",
                                  "Priority": 65000,
                                  "Direction": "Inbound"
                                  },…
                         ]
   
        NetworkSecurityGroup   : {
                                   "Id": 
                                 "/subscriptions/[Subscription ID]/resourceGroups/RG1/providers/Microsoft.Network/networkSecurityGroups/Subnet1-NSG"
                                 }
        Association            : {
                                   "Subnet": {
                                     "Id": 
                                 "/subscriptions/[Subscription ID]/resourceGroups/RG1/providers/Microsoft.Network/virtualNetworks/WestUS-VNet1/subnets/Subnet1"
                                 }
                                 }
        EffectiveSecurityRules : [
                                 {
                                "Name": "securityRules/denyRDP",
                                "Protocol": "Tcp",
                                "SourcePortRange": "0-65535",
                                "DestinationPortRange": "3389-3389",
                                "SourceAddressPrefix": "Internet",
                                "DestinationAddressPrefix": "0.0.0.0/0",
                                "ExpandedSourceAddressPrefix": [
                                   ... ],
                                "ExpandedDestinationAddressPrefix": [],
                                "Access": "Deny",
                                "Priority": 1000,
                                "Direction": "Inbound"
                                },
                                {
                                "Name": "defaultSecurityRules/AllowVnetInBound",
                                "Protocol": "All",
                                "SourcePortRange": "0-65535",
                                "DestinationPortRange": "0-65535",
                                "SourceAddressPrefix": "VirtualNetwork",
                                "DestinationAddressPrefix": "VirtualNetwork",
                                "ExpandedSourceAddressPrefix": [
                                "10.9.0.0/16",
                                "168.63.129.16/32",
                                "10.0.0.0/16",
                                "10.1.0.0/16"
                                ],
                                "ExpandedDestinationAddressPrefix": [
                                "10.9.0.0/16",
                                "168.63.129.16/32",
                                "10.0.0.0/16",
                                "10.1.0.0/16"
                                ],
                                "Access": "Allow",
                                "Priority": 65000,
                                "Direction": "Inbound"
                                },...
                                ]
   
    請注意下列資訊 hello 輸出中的 hello:
   
   * 有兩個 **NetworkSecurityGroup** 區段︰一個與子網路 (*Subnet1*) 相關聯，一個與 NIC (*VM1-NIC1*) 相關聯。 在此範例中，NSG 已套用的 tooeach。
   * **關聯**顯示 hello 資源 （子網路或 NIC） 指定的 NSG 與相關聯。 如果 hello NSG 資源移動/解除關聯執行此命令之前，您可能需要 toowait 幾秒鐘的時間以 hello 變更 tooreflect hello 命令輸出中。 
   * hello 做為開頭的規則名稱*defaultSecurityRules*： 當 NSG 會建立，在其中建立數個預設安全性規則。 預設規則無法移除，但是可以較高優先順序的規則覆寫。
     讀取 hello [NSG 概觀](virtual-networks-nsg.md#default-rules)深入了解 NSG 文章 toolearn 預設安全性規則。
   * **ExpandedAddressPrefix**展開 NSG 預設標記的 hello 位址首碼。 標籤代表多個位址首碼。 從特定位址前置詞的 VM 連線進行疑難排解時，擴充的 hello 標記很有用。 例如，具有對等互連的 VNET，VIRTUAL_NETWORK 標記會展開 tooshow 所以 VNet hello 上述輸出中的前置詞。
     
     > [!NOTE]
     > NSG 相關聯的子網路、 NIC，或兩者是否 hello 命令只會顯示有效的規則。 一個 VM 可能有多個 NIC 分別套用不同的 NSG。 進行疑難排解時，執行每個 NIC hello 命令
     > 
     > 
3. tooease 覆寫較大的數字的 NSG 規則篩選輸入下列命令 tootroubleshoot 進一步 hello: 
   
        $NSGs = Get-AzureRmEffectiveNetworkSecurityGroup -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1
        $NSGs.EffectiveSecurityRules | Sort-Object Direction, Access, Priority | Out-GridView
   
    RDP 流量 （TCP 連接埠 3389），篩選條件是套用 toohello 方格檢視中，hello 下列圖片所示：
   
    ![規則清單](./media/virtual-network-nsg-troubleshoot-powershell/rules.png)
4. 您可以看到 hello 方格檢視中，有同時允許與拒絕 rdp 的規則。 hello 步驟 2 中的輸出會顯示該 hello *DenyRDP*規則是在 hello NSG 套用 toohello 子網路。 對於輸入規則，會先處理 Nsg 套用 toohello 子網路。 如果找到相符項目，不會處理 hello NSG 套用 toohello 網路介面。 在此情況下，hello *DenyRDP*從 hello 子網路的規則會封鎖 RDP toohello VM (**VM1**)。
   
   > [!NOTE]
   > VM 可能會有多個 Nic 附加的 tooit。 每個可能是連線的 tooa 不同的子網路。 因為在 hello 先前步驟中的 hello 命令會針對 NIC 執行，很重要您指定的 tooensure hello 的 NIC 遇到 hello 連線失敗。 如果您不確定，您就可以針對每個連結 NIC toohello VM，一律執行 hello 命令。
   > 
   > 
5. 到 VM1，變更 hello tooRDP*拒絕 RDP (為 3389)*太規則*允許 RDP(3389)*在 hello **Subnet1 NSG** NSG。 確認開啟 RDP 連線 toohello VM，或使用 hello PsPing 工具開啟 TCP 連接埠 3389。 您可以進一步了解 PsPing 讀取 hello [PsPing 下載頁面](https://technet.microsoft.com/sysinternals/psping.aspx)
   
    您可以使用或移除規則從 NSG hello 資訊在 hello 輸出 hello 下列命令：
   
        Get-Help *-AzureRmNetworkSecurityRuleConfig

## <a name="considerations"></a>考量
請考慮 hello 疑難排解連線問題時，下列點：

* 預設 NSG 規則將會封鎖從 hello 對內的存取網際網路和允許 VNet 輸入流量。 規則應該明確加入 tooallow 輸入視需要從網際網路存取。
* 如果沒有造成 VM 的網路連線 toofail NSG 安全性規則，hello 問題可能是因為：
  * Hello VM 作業系統內執行的防火牆軟體
  * 為虛擬設備或內部部署流量設定的路由。 網際網路流量可以透過強制通道的重新導向的 tooon 單位。 RDP/SSH 連線從 hello 網際網路 tooyour VM 可能不適用於此設定，根據 hello 在內部部署網路硬體如何處理這個流量。 讀取 hello[疑難排解路由](virtual-network-routes-troubleshoot-powershell.md)文章 toolearn 如何 toodiagnose 路由問題，可能索性 hello 和出的流量傳送 hello VM。 
* 如果您有所以 Vnet，根據預設，hello VIRTUAL_NETWORK 標記會自動擴展 tooinclude 前置詞所以 vnet。 您可以檢視這些前置詞中 hello **ExpandedAddressPrefix**清單，tootroubleshoot 對等互連連線問題相關 tooVNet。 
* 有效的安全性規則只會顯示於是否有與 hello VM NIC 和或子網路的 NSG 相關聯。 
* 如果沒有相關聯 hello NIC 的 Nsg 或子網路，而且您有指派 tooyour VM 的公用 IP 位址，所有連接埠將會開啟以供對內及對外存取。 如果 hello VM 的公用 IP 位址，強烈建議套用 Nsg toohello NIC 或子網路。  

