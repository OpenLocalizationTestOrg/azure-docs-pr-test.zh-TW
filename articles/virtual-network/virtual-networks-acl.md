---
title: "aaaWhat 是 Azure 網路存取控制清單？"
description: "了解 Azure 中的存取控制清單"
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 83d66c84-8f6b-4388-8767-cd2de3e72d76
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.openlocfilehash: a2681af035d162362771e6df9864bbe838f16352
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-an-endpoint-access-control-list"></a>什麼是端點存取控制清單？

> [!IMPORTANT]
> Azure 有兩種不同的[部署模型](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json)來建立和使用資源：Resource Manager 和傳統。 本文說明如何使用 hello 傳統部署模型。 Microsoft 建議最新的部署使用 hello Resource Manager 部署模型。 

端點存取控制清單 (ACL) 是可供您的 Azure 部署使用的安全性增強功能。 ACL 提供 hello 能力 tooselectively 允許或拒絕虛擬機器端點的流量。 此封包篩選功能提供了一層額外的安全性。 您可以僅針對端點指定網路 ACL。 您無法針對虛擬網路或是包含在虛擬網路中的特定子網路指定 ACL。 建議 toouse 網路安全性群組 (Nsg) 而不是盡可能的 Acl。 toolearn 深入了解 Nsg，請參閱[網路安全性群組概觀](virtual-networks-nsg.md)

可以使用 PowerShell 或 hello Azure 入口網站中設定 Acl。 tooconfigure 網路 ACL 使用 PowerShell，請參閱[端點使用 PowerShell 管理存取控制清單](virtual-networks-acl-powershell.md)。 使用網路 ACL tooconfigure hello Azure 入口網站，請參閱[如何端點 tooa 虛擬機器 tooset](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)。

使用網路 Acl，您可以執行下列 hello:

* 選擇性地允許或拒絕根據遠端子網路 IPv4 位址範圍 tooa 虛擬機器輸入端點的連入流量。
* 將 IP 位址加入黑名單
* 為每個虛擬機器端點建立多個規則
* 使用規則順序 tooensure hello 正確指定的虛擬機器端點 (最低 toohighest) 上套用的規則集
* 為特定遠端子網路 IPv4 位址指定 ACL。

請參閱 hello [Azure 限制](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#networking-limits)ACL 限制的發行項。

## <a name="how-acls-work"></a>ACL 的運作方式
ACL 是包含規則清單的物件。 當您建立 ACL，並將它套用 tooa 虛擬機器端點時，封包篩選會在您的 VM hello 主機節點進行。 這表示 hello 來自遠端 IP 位址的流量篩選，而不是比對的 ACL 規則，在您的 VM 上的 hello 主機節點。 如此您的 VM 免於耗費珍貴 CPU 循環 hello 封包篩選。

建立虛擬機器時，一份預設 ACL 置於位置 tooblock 所有連入流量。 不過，如果 （連接埠 3389） 所建立的端點，然後 hello 預設 ACL 被修改 tooallow 為該端點的所有傳入的流量。 從任何遠端子網路的傳入的流量將獲允許 toothat 端點和沒有防火牆佈建是必要的。 除非建立那些連接埠的端點，否則會封鎖所有其他連接埠則的輸入流量。 預設為允許輸出流量。

**範例預設 ACL 資料表**

| **規則編號** | **遠端子網路** | **端點** | **允許/拒絕** |
| --- | --- | --- | --- |
| 100 |0.0.0.0/0 |3389 |允許 |

## <a name="permit-and-deny"></a>允許和拒絕
您可以透過建立指定「允許」或「拒絕」的規則，選擇性允許或拒絕虛擬機器輸入端點的網路流量。 根據預設，當建立端點時，所有流量都允許的 toohello 端點的重要 toonote 它。 基於這個原因，是重要 toounderstand 如何 toocreate 允許/拒絕規則，並將它們放在 hello 正確順序的優先順序，如果您想要更精確地控制 hello 網路流量，您可以選擇 tooallow tooreach hello 虛擬機器端點。

點 tooconsider:

1. **無 ACL –**預設建立端點時，將允許所有流量 hello 端點。
2. **允許 -** 當您新增一個或多個「允許」範圍時，將預設為拒絕所有其他範圍。 從允許的 IP 範圍的 hello 的封包將會無法 toocommunicate 與 hello 虛擬機器端點。
3. **拒絕 -** 當您新增一個或多個「拒絕」範圍時，將預設為允許所有其他範圍。
4. **允許和拒絕層的組合**您可以使用組合的 「 允許 」 和 「 拒絕 」 時想 toocarve 出特定的 IP 範圍 toobe 允許或拒絕。

## <a name="rules-and-rule-precedence"></a>規則和規則優先順序
網路 ACL 可以在特定的虛擬機器端點上進行設定。 例如，您可以針對在虛擬機器上建立的 RDP 端點指定網路 ACL，以便鎖定特定 IP 位址的存取權。 hello 下表顯示方式 toogrant 存取 toopublic 的特定範圍 toopermit 存取 RDP 的虛擬 Ip (Vip)。 所有其他遠端 IP 會遭到拒絕。 我們遵循 *最低優先* 的規則順序。

### <a name="multiple-rules"></a>多個規則
在 hello 面範例中，如果您想 tooallow 存取 toohello RDP 端點只能從兩個公用 IPv4 位址範圍 （65.0.0.0/8 和 159.0.0.0/8），您可以達到這個目的藉由指定兩個*允許*規則。 在此情況下，由於虛擬機器預設會建立 RDP，您可能需要 toolock 下對遠端子網路為基礎的存取 toohello RDP 連接埠。 hello 以下範例顯示的方式 toogrant 存取 toopublic 的特定範圍 toopermit 存取 RDP 的虛擬 Ip (Vip)。 所有其他遠端 IP 會遭到拒絕。 這是因為網路 ACL 可以針對特定虛擬機器端點進行設定，且預設為拒絕存取。

**範例 – 多個規則**

| **規則編號** | **遠端子網路** | **端點** | **允許/拒絕** |
| --- | --- | --- | --- |
| 100 |65.0.0.0/8 |3389 |允許 |
| 200 |159.0.0.0/8 |3389 |允許 |

### <a name="rule-order"></a>規則順序
為端點時，可以指定多個規則，因為中必須有方式 tooorganize 規則順序 toodetermine 規則的優先順序。 hello 規則順序即是指定優先順序。 網路 ACL 遵循 *最低優先* 的規則順序。 在 hello 下列範例中，連接埠 80 上的 hello 端點選擇性地授與存取 tooonly 特定 IP 位址範圍。 tooconfigure，我們有拒絕規則 (規則\#100) hello 175.1.0.1/24 空間中的位址。 第二個規則則被指定優先順序 200 允許存取 tooall 175.0.0.0/8 底下其他地址。

**範例 – 規則優先順序**

| **規則編號** | **遠端子網路** | **端點** | **允許/拒絕** |
| --- | --- | --- | --- |
| 100 |175.1.0.1/24 |80 |拒絕 |
| 200 |175.0.0.0/8 |80 |允許 |

## <a name="network-acls-and-load-balanced-sets"></a>網路 ACL 和負載平衡集合
您可以在負載平衡集端點上指定網路 ACL。 如果負載平衡集指定 ACL，hello 的網路 ACL 是套用的 tooall 中的虛擬機器負載平衡的集。 例如，如果使用 「 連接埠 80 」 所建立的負載平衡集，而且 hello 負載平衡集包含 3 個 Vm，hello 網路 ACL 建立端點的其中一個 VM 會自動的 「 連接埠 80 」 套用 toohello 其他 Vm。

![網路 ACL 和負載平衡集合](./media/virtual-networks-acl/IC674733.png)

## <a name="next-steps"></a>後續步驟
[使用 PowerShell 來管理端點的存取控制清單](virtual-networks-acl-powershell.md)

