---
title: "在 Azure 堆疊 aaaQuota 類型 |Microsoft 文件"
description: "檢閱 hello 不同的配額類型之服務和 Azure 堆疊中的資源。"
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: byronr
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 8/23/2017
ms.author: erikje
ms.openlocfilehash: e05870603526a3e0e65d536cff98b9033524017d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="quota-types-in-azure-stack"></a>Azure Stack 中的配額類型
[配額](azure-stack-plan-offer-quota-overview.md#plans)定義 hello 使用者訂用帳戶可以佈建或取用之資源的限制。 例如，配額可能允許使用者 toocreate toofive Vm 上。 每個資源都可以有自己的配額類型。

## <a name="compute-quota-types"></a>計算配額類型
| **類型** | **預設值** | **說明** |
| --- | --- | --- |
| 虛擬機器的數目上限 |50 | hello 訂用帳戶可以在這個位置中建立的虛擬機器的數目上限。 |
| 虛擬機器核心的數目上限 |100 | hello 的訂用帳戶可以在這個位置中建立的核心數目上限 （例如，A3 VM 有四個核心）。 |
| 可用性設定組的數目上限 |10 | hello，可以在這個位置建立可用性設定組的數目上限。 |
| 虛擬機器擴展集的數目上限 |100 | hello 可以在這個位置建立的虛擬機器規模集的數目上限。 |

> [!NOTE]
> 此 Technical Preview 中未限制計算配額。
> 
> 

## <a name="storage-quota-types"></a>儲存體配額類型
| **Item** | **預設值** | **說明** |
| --- | --- | --- |
| 最大容量 (GB) |500 |訂用帳戶可以在這個位置取用的總儲存體容量。 |
| 儲存體帳戶的總數 |20 |hello 的訂用帳戶可以在這個位置中建立的儲存體帳戶數目上限。 |

## <a name="network-quota-types"></a>網路配額類型
| **Item** | **預設值** | **說明** |
| --- | --- | --- |
| 公用 IP 的數目上限 |50 |hello 的訂用帳戶可以在這個位置中建立的公用 Ip 數目上限。 |
| 虛擬網路的數目上限 |50 |hello 的訂用帳戶可以在這個位置中建立的虛擬網路的最大數目。 |
| 虛擬網路閘道的數目上限 |1 |hello 訂用帳戶可以在這個位置中建立的虛擬網路閘道 （VPN 閘道） 的數目上限。 |
| 網路連線的數目上限 |2 |hello 訂用帳戶可以建立在這個位置中的所有虛擬網路閘道的網路連線 （點對點或站台對站台） 的數目上限。 |
| 負載平衡器的數目上限 |50 |hello 訂用帳戶可以在這個位置中建立的負載平衡器的數目上限。 |
| 最大 NIC |100 |hello 訂用帳戶可以在這個位置中建立的網路介面的數目上限。 |
| 網路安全性群組的數目上限 |50 |hello 訂用帳戶可以在這個位置中建立的網路安全性群組的數目上限。 |

## <a name="view-an-existing-quota"></a>檢視現有的配額
1. 按一下 [更多服務] > [資源提供者]。
2. 選取您想 tooview hello 配額與 hello 服務。
3. 按一下**配額**，和您想要 tooview 選取 hello 配額。

## <a name="next-steps"></a>後續步驟
[深入了解方案、供應項目與配額。](azure-stack-plan-offer-quota-overview.md)

[建立方案時建立配額。](azure-stack-create-plan.md)
