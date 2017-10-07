---
title: "Azure 負載平衡器 Vip aaaMultiple |Microsoft 文件"
description: "Azure Load Balancer 上多個 VIP 概觀"
services: load-balancer
documentationcenter: na
author: chkuhtz
manager: narayan
editor: 
ms.assetid: 748e50cd-3087-4c2e-a9e1-ac0ecce4f869
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/11/2016
ms.author: chkuhtz
ms.openlocfilehash: e186e1248e7d187e7efd0668dc3244465ce3e156
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="multiple-vips-for-azure-load-balancer"></a>Azure Load Balancer 的多個 VIP

Azure 負載平衡器可讓您在多個連接埠、 多個 IP 位址，或兩者上的 tooload 平衡服務。 您可以使用公用和內部負載平衡器定義 tooload 平衡流量分配一組的 Vm。

這篇文章會說明這個能力、 重要的概念和條件約束的 hello 基本概念。 如果您只想 tooexpose 服務在一個 IP 位址上，您可以找到簡化的指示[公用](load-balancer-get-started-internet-portal.md)或[內部](load-balancer-get-started-ilb-arm-portal.md)負載平衡器組態。 加入多個 Vip 是累加 tooa 單一 VIP 設定。 使用本文章中的 hello 概念，您可以展開簡化的組態，在任何時間。

定義 Azure Load Balancer 時，前端和後端設定會與規則連線。 hello hello 規則所參考的健全狀況探查是使用的 toodetermine 新流量會傳送 hello 後端集區中的 tooa 節點。 hello 前端定義的虛擬 IP (VIP)，也就是 3-tuple 組成 （公用或內部） 的 IP 位址、 傳輸通訊協定 （UDP 或 TCP） 和連接埠號碼。 DIP 是 Azure 的虛擬 NIC 上的 IP 位址附加 tooa hello 後端集區中的 VM。

hello 下表包含一些範例前端組態：

| VIP | IP 位址 | protocol | 連接埠 |
| --- | --- | --- | --- |
| 1 |65.52.0.1 |TCP |80 |
| 2 |65.52.0.1 |TCP |*8080* |
| 3 |65.52.0.1 |*UDP* |80 |
| 4 |*65.52.0.2* |TCP |80 |

hello 表顯示四個不同的前端。 #1、#2、#3 前端是具有多個規則的單一 VIP。 hello 相同的 IP 位址使用，但 hello 連接埠或通訊協定是每個前端不同。 前端 #1 和 #4，多個 Vip，其中 hello 相同前端通訊協定和連接埠可重複使用跨多個 Vip 的範例。

Azure 負載平衡器提供有彈性地定義 hello 負載平衡規則。 規則宣告如何位址和連接埠 hello 前端上是對應的 toohello 目的地位址與連接埠 hello 後端上。 在規則上重複使用後端連接埠是不論是否取決於 hello hello 規則類型。 每種規則類型有特定的需求，會影響主機設定和探查設計的方式。 規則分為兩種：

1. hello 與任何後端連接埠的預設規則重複使用
2. hello 浮動 IP 規則會在重複使用後端連接埠

Azure 負載平衡器可讓您同時在 規則類型 toomix hello 相同負載平衡器組態。 hello 負載平衡器可以使用它們同時針對指定的 VM 或任何組合中，只要您遵守 hello 的 hello 規則的條件約束。 您選擇哪些規則類型取決於您應用程式和 hello 的複雜度，支援該組態的 hello 需求。 您應該評估何種規則類型最適合您的案例。

我們來探索這些案例進一步開頭 hello 預設行為。

## <a name="rule-type-1-no-backend-port-reuse"></a>規則類型 #1︰不重複使用後端連接埠

![MultiVIP 圖解片](./media/load-balancer-multivip-overview/load-balancer-multivip.png)

在此案例中，hello 前端 Vip 設定，如下所示：

| VIP | IP 位址 | protocol | 連接埠 |
| --- | --- | --- | --- |
| ![VIP](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) 1 |65.52.0.1 |TCP |80 |
| ![VIP](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) 2 |*65.52.0.2* |TCP |80 |

hello DIP 是 hello hello 目的地的輸入流量。 在 hello 後端集區，每個 VM 會公開 hello 預期 DIP 的唯一連接埠上的服務。 此服務是透過規則定義的 hello 前端與相關聯。

我們定義兩個規則︰

| 規則 | 對應前端 | toobackend 集區 |
| --- | --- | --- |
| 1 |![VIP](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) VIP1:80 |![後端](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) DIP1:80, ![後端](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) DIP2:80 |
| 2 |![VIP](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) VIP2:80 |![後端](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) DIP1:81, ![後端](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) DIP2:81 |

Azure 負載平衡器中的 hello 完成對應現在如下所示：

| 規則 | VIP IP 位址 | protocol | 連接埠 | 目的地 | 連接埠 |
| --- | --- | --- | --- | --- | --- |
| ![規則](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) 1 |65.52.0.1 |TCP |80 |DIP IP 位址 |80 |
| ![規則](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) 2 |65.52.0.2 |TCP |80 |DIP IP 位址 |81 |

每個規則都必須產生具有唯一組合 (目的地 IP 位址和目的地連接埠組合) 的流程。 藉由各種 hello 的目的地連接埠 hello 資料流程，多個規則可以提供流程 toohello 不同的連接埠上的相同 DIP。

健全狀況探查一律會導向的 toohello VM 的 DIP。 您必須確定您您探查反映 hello VM hello 健全狀況。

## <a name="rule-type-2-backend-port-reuse-by-using-floating-ip"></a>規則類型 #2︰使用浮動 IP 來重複使用後端連接埠

Azure 負載平衡器提供跨多個 Vip，不論使用的 hello 規則類型 hello 彈性 tooreuse hello 的前端連接埠。 此外，部分應用程式案例偏好或要求相同連接埠 toobe hello 後端集區中之單一 vm 的多個應用程式執行個體所使用的 hello。 連接埠重複使用的常見範例包括提供高可用性的叢集、網路虛擬裝置、公開多個不會重新加密的 TLS 端點。

如果您想 tooreuse hello 後端連接埠跨多個規則，您必須啟用浮動 IP hello 規則定義中。

浮動 IP 是伺服器直接回傳 (DSR) 的一部分。 DSR 包含兩個部分︰流程拓樸和 IP 位址對應配置。 在平台層級，Azure Load Balancer 一律在 DSR 流程拓撲中運作，無論是否已啟用浮動 IP。 這表示 hello 流程一部分輸出永遠是正確重寫的 tooflow 直接後 toohello 原點。

與 hello 預設規則類型，Azure 會公開傳統負載平衡以方便使用的 IP 位址對應配置。 啟用浮動 IP 變更額外的彈性，說明如下所示為 hello IP 位址對應配置 tooallow。

hello 下列圖表將說明這項設定：

![MultiVIP 圖解片](./media/load-balancer-multivip-overview/load-balancer-multivip-dsr.png)

此案例中，針對 hello 後端集區中的每個 VM 會具有三個網路介面：

* DIP: 虛擬 NIC 與 hello VM （Azure 的 NIC 資源的 IP 組態） 相關聯
* VIP1︰客體 OS 內的回送介面 (此 OS 已設定了 VIP1 的 IP 位址)
* VIP2︰客體 OS 內的回送介面 (此 OS 已設定了 VIP2 的 IP 位址)

> [!IMPORTANT]
> hello 組態的 hello 邏輯介面 hello 客體作業系統內執行。 這項設定不是由 Azure 執行或管理。 沒有此設定，hello 規則將無法運作。 健全狀況探查定義使用 hello hello VM 的 DIP，而不是 hello 邏輯的 VIP。 因此，您的服務必須提供所提供的 hello 服務的 hello 狀態反映 hello 邏輯 vip DIP 通訊埠上的探查回應。

讓我們假設 hello 相同的前端組態，如 hello 前一個案例所示：

| VIP | IP 位址 | protocol | 連接埠 |
| --- | --- | --- | --- |
| ![VIP](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) 1 |65.52.0.1 |TCP |80 |
| ![VIP](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) 2 |*65.52.0.2* |TCP |80 |

我們定義兩個規則︰

| 規則 | 對應前端 | toobackend 集區 |
| --- | --- | --- |
| 1 |![規則](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) VIP1:80 |![後端](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) VIP1:80 (在 VM1 和 VM2) |
| 2 |![規則](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) VIP2:80 |![後端](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) VIP2:80 (在 VM1 和 VM2) |

下表中的 hello hello 負載平衡器中顯示 hello 完整的對應：

| 規則 | VIP IP 位址 | protocol | 連接埠 | 目的地 | 連接埠 |
| --- | --- | --- | --- | --- | --- |
| ![VIP](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) 1 |65.52.0.1 |TCP |80 |與 VIP 相同 (65.52.0.1) |與 VIP 相同 (80) |
| ![VIP](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) 2 |65.52.0.2 |TCP |80 |與 VIP 相同 (65.52.0.2) |與 VIP 相同 (80) |

hello 目的地 hello 的輸入的流量沒有受到 hello VM 中的 hello 回送介面上的 hello VIP 位址。 每個規則都必須產生具有唯一組合 (目的地 IP 位址和目的地連接埠組合) 的流程。 依不同 hello 目的地 IP 位址的 hello 流程連接埠重複使用是有可能會在 hello 相同的 VM。 您的服務 toohello VIP 的 IP 位址和連接埠 hello 個別的回送介面將它繫結所公開的 toohello 負載平衡器。

請注意此範例不會變更 hello 目的地連接埠。 雖然這是浮動 IP 的案例，Azure 負載平衡器也支援定義規則 toorewrite hello 後端目的地連接埠和 toomake 它不同於 hello 前端目的地連接埠。

hello 浮動 IP 規則類型是數種負載平衡器組態模式的 hello foundation。 目前可用的其中一個範例是 hello[與多個接聽程式的 SQL AlwaysOn](../virtual-machines/windows/sql/virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md)組態。 經過一段時間，我們會記載更多這類案例。

## <a name="limitations"></a>限制

* 只有 IaaS VM 支援多個 VIP 設定。
* Hello 浮動 IP 規則之後，您的應用程式必須使用輸出流量 hello DIP。 如果您的應用程式將繫結 toohello hello 客體作業系統中的 hello 回送介面上設定的 VIP 位址，則 SNAT 不是使用 toorewrite hello 輸出流量，而 hello 流程失敗。
* 公用 IP 位址需要費用。 如需詳細資訊，請參閱 [IP 位址定價](https://azure.microsoft.com/pricing/details/ip-addresses/)
* 訂用帳戶有其限制。 如需詳細資訊，請參閱 [服務限制](../azure-subscription-service-limits.md#networking-limits) 的說明。
