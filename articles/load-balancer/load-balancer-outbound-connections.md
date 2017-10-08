---
title: "在 Azure 中的 aaaUnderstanding 輸出連線 |Microsoft 文件"
description: "本文說明如何 Azure 可讓 Vm toocommunicate 具有公用網際網路服務。"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
ms.assetid: 5f666f2a-3a63-405a-abcd-b2e34d40e001
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 5/31/2017
ms.author: kumud
ms.openlocfilehash: ffe59971b934a16c9f6f78e3b15869a0072320d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-outbound-connections-in-azure"></a>了解 Azure 中的輸出連線

Azure 中的虛擬機器 (VM) 可在公用 IP 位址空間中與 Azure 外部的端點進行通訊。 當 VM 啟動公用 IP 位址空間中的輸出流量 tooa 目的地時，則 Azure hello VM 的私用 IP 位址 tooa 公用 IP 位址，對應，並允許返回流量 tooreach hello VM。

Azure 提供三種不同方法 tooachieve 的傳出連線。 每個方法都有自己的功能和條件約束。 請仔細檢閱每個方法 toochoose 哪一個符合您的需求。

| 案例 | 方法 | 注意 |
| --- | --- | --- |
| 獨立 VM (無負載平衡器，無執行個體層級公用 IP 位址) |預設 SNAT |Azure 關聯 SNAT 的公用 IP 位址 |
| 負載平衡的 VM (無 VM 上的執行個體層級公用 IP 位址) |SNAT 使用 hello 負載平衡器 |Azure 的 hello 負載平衡器的公用 IP 位址用於 SNAT |
| 具有執行個體層級公用 IP 位址的 VM (無論是否有負載平衡器) |未使用 SNAT |Azure 會使用 hello 分派 toohello VM 的公用 IP |

如果您不想 VM toocommunicate 具有外部公用 IP 位址空間中的 Azure 端點，您可以使用網路安全性群組群組 (NSG) tooblock 存取。 [防止公用連線](#preventing-public-connectivity)中會更詳細地討論使用 NSG。

## <a name="standalone-vm-with-no-instance-level-public-ip-address"></a>無執行個體層級公用 IP 位址的獨立 VM

在此案例中，hello VM 不是 Azure 負載平衡器集區的一部分，而且沒有指派 tooit 的執行個體層級公用 IP (ILPIP) 位址。 當 hello VM 建立輸出的資料流程時，Azure 將轉譯 hello 輸出流量 tooa 公用的來源 IP 位址的 hello 私用的來源 IP 的位址。 hello 這個輸出流程使用公用 IP 位址是不可設定的並不會計算 hello 訂用帳戶的公用 IP 資源限制。 Azure 會使用來源網路位址轉譯 (SNAT) tooperform 此函式。 Hello 公用 IP 位址的臨時連接埠會使用的 toodistinguish 個別源自 hello VM 的流量。 建立流程時，SNAT 會動態配置暫時連接埠。 在此內容中，用於 SNAT hello 臨時連接埠是參照的 tooas SNAT 連接埠。

SNAT 連接埠是可能會耗盡的有限資源。 使用方式的重要 toounderstand 它。 一個 SNAT 連接埠被取用每一個流程 tooa 單一目的地 IP 位址。 針對多個流程 toohello 相同的目的地 IP 位址，每個流程取用單一 SNAT 連接埠。 這可確保 hello 流程唯一時，源自 hello 相同公用 IP 位址 toohello 相同的目的地 IP 位址。 多個流程，每個 tooa 不同的目的地 IP 位址使用單一 SNAT 連接埠，每個目的地。 hello 目的地 IP 位址的特點 hello 流程。

您可以使用[負載平衡器的記錄分析](load-balancer-monitor-log.md)和[SNAT 連接埠耗盡訊息的警示的事件記錄檔 toomonitor](load-balancer-monitor-log.md#alert-event-log)。 當 SNAT 連接埠資源耗盡時，輸出流程失敗，直到現有流程釋放 SNAT 連接埠為止。 負載平衡器會使用 4 分鐘閒置逾時以收回 SNAT 連接埠。

## <a name="load-balanced-vm-with-no-instance-level-public-ip-address"></a>無執行個體層級公用 IP 位址的負載平衡 VM

在此案例中，hello VM 是 Azure 負載平衡器集區的一部分。  hello VM 沒有指派 tooit 公用 IP 位址。 hello 負載平衡器資源必須使用規則 toolink hello 公用 IP 前端與 hello 後端集區設定。  如果您沒有完成這項設定，hello 行為是 hello 前一節，如中所述[獨立虛擬機器沒有執行個體層級公用 IP 與](load-balancer-outbound-connections.md#standalone-vm-with-no-instance-level-public-ip-address)。

Hello 負載平衡的 VM 建立輸出的資料流程，Azure 會轉譯 hello 輸出流量 toohello 公用 IP 位址的 hello 公用負載平衡器前端的 hello 私用的來源 IP 位址。 Azure 會使用來源網路位址轉譯 (SNAT) tooperform 此函式。 Hello 負載平衡器的公用 IP 位址的臨時連接埠會使用的 toodistinguish 個別源自 hello VM 的流量。 建立輸出流程時，SNAT 會動態配置暫時連接埠。 在此內容中，用於 SNAT hello 臨時連接埠是參照的 tooas SNAT 連接埠。

SNAT 連接埠是可能會耗盡的有限資源。 使用方式的重要 toounderstand 它。 一個 SNAT 連接埠被取用每一個流程 tooa 單一目的地 IP 位址。 針對多個流程 toohello 相同的目的地 IP 位址，每個流程取用單一 SNAT 連接埠。 這可確保 hello 流程唯一時，源自 hello 相同公用 IP 位址 toohello 相同的目的地 IP 位址。 多個流程，每個 tooa 不同的目的地 IP 位址使用單一 SNAT 連接埠，每個目的地。 hello 目的地 IP 位址的特點 hello 流程。

您可以使用[負載平衡器的記錄分析](load-balancer-monitor-log.md)和[SNAT 連接埠耗盡訊息的警示的事件記錄檔 toomonitor](load-balancer-monitor-log.md#alert-event-log)。 當 SNAT 連接埠資源耗盡時，輸出流程失敗，直到現有流程釋放 SNAT 連接埠為止。 負載平衡器會使用 4 分鐘閒置逾時以收回 SNAT 連接埠。

## <a name="vm-with-an-instance-level-public-ip-address-with-or-without-load-balancer"></a>具有執行個體層級公用 IP 位址的 VM (無論是否有負載平衡器)

在此案例中，hello VM 會有執行個體層級公用 IP (ILPIP) 指派 tooit。 並不重要 hello VM 是否負載平衡與否。 使用 ILPIP 時，不會使用來源網路位址轉譯 (SNAT)。 hello VM 使用 hello ILPIP 所有輸出流量的。 如果您的應用程式起始許多輸出流量，而且您遇到 SNAT 耗盡，您應該考慮指派 ILPIP tooavoid SNAT 條件約束。

## <a name="discovering-hello-public-ip-used-by-a-given-vm"></a>指定的 VM 所使用的探索 hello 公用 IP

有很多種 toodetermine hello 公用來源的輸出連線的 IP 位址。 OpenDNS 提供的服務，可以顯示 hello VM 的公用 IP 位址。 使用 hello nslookup 命令時，您可以傳送 DNS 查詢 hello 名稱 myip.opendns.com toohello OpenDNS 解析程式。 hello 服務會傳回已使用的 toosend hello 查詢的 hello 來源 IP 位址。 當您執行您的 VM 中的下列查詢的 hello 時，hello 回應會是公用 IP 用於該 VM 的 hello。

    nslookup myip.opendns.com resolver1.opendns.com

## <a name="preventing-public-connectivity"></a>防止公用連線

有時是讓人困擾的 VM toobe 允許 toocreate 輸出流量，或可能有哪些目的地可以達到與輸出流量需求 toomanage。 在此情況下，您使用[網路安全性群組群組 (NSG)](../virtual-network/virtual-networks-nsg.md) toomanage hello 目的地 VM 可以連線到該 hello。 當您將套用 NSG tooa 負載平衡 VM，您需要 toopay 注意 toohello[預設標記](../virtual-network/virtual-networks-nsg.md#default-tags)和[預設規則](../virtual-network/virtual-networks-nsg.md#default-rules)。

您必須確定該 hello VM 可以接收來自 Azure 負載平衡器的健全狀況探查要求。 如果 NSG 區塊健全狀況探查要求從 hello AZURE_LOADBALANCER 預設標籤，您 VM 的健全狀況探查失敗，hello VM 被標示為離線。 負載平衡器會停止傳送新的流程 toothat VM。

## <a name="limitations"></a>限制

若[多個 (公用) IP 位址與負載平衡器關聯](load-balancer-multivip-overview.md)這些公用 IP 位址中的任一位址都可以是輸出流程的候選項。

Azure 會使用演算法 toodetermine hello SNAT 連接埠數目可根據 hello hello 集區大小。  目前無法進行設定。

請務必 toorememember hello SNAT 連接埠數目，不會轉譯直接 toonumber 的連線。 請參閱上述詳細資料何時及如何 SNAT 連接埠配置及如何 toomanage 此 exhaustible 資源。
