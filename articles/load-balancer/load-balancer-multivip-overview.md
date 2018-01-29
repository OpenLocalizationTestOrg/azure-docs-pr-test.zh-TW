---
title: "Azure Load Balancer 的多個 VIP | Microsoft Docs"
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
ms.date: 09/25/2017
ms.author: chkuhtz
ms.openlocfilehash: 1045a18f5fd9739a6028198deea129e9e621f127
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/11/2017
---
# <a name="multiple-vips-for-azure-load-balancer"></a>Azure Load Balancer 的多個 VIP

[!INCLUDE [load-balancer-basic-sku-include.md](../../includes/load-balancer-basic-sku-include.md)]

Azure Load Balancer 可讓您平衡在多個連接埠、多個 IP 位址或兩者上的服務負載。 您可以使用公用和內部負載平衡器定義來負載平衡一組 VM 間的流量。

本文說明此功能的基本運用、重要概念和限制。 如果您只想要公開一個 IP 位址上的服務，可以找到[公用](load-balancer-get-started-internet-portal.md)或[內部](load-balancer-get-started-ilb-arm-portal.md)負載平衡器設定的簡易指示。 新增多個 VIP 是對單一 VIP 設定累加設定。 您隨時可以使用本文中的概念擴充簡化的設定。

定義 Azure Load Balancer 時，前端和後端設定會與規則連線。 規則所參考的健全狀況探查是用來判斷新的流程如何傳送至後端集區中的節點。 前端是由虛擬 IP (VIP) 定義，VIP 由 3 項元素組成：IP 位址 (公用或內部)、傳輸通訊協定 (UDP 或 TCP)、連接埠號碼。 DIP 是連接到後端集區中 VM 的 Azure 虛擬 NIC 上的 IP 位址。

下表是一些範例前端設定：

| VIP | IP 位址 | protocol | 連接埠 |
| --- | --- | --- | --- |
| 1 |65.52.0.1 |TCP |80 |
| 2 |65.52.0.1 |TCP |*8080* |
| 3 |65.52.0.1 |*UDP* |80 |
| 4 |*65.52.0.2* |TCP |80 |

表中有四個不同的前端。 #1、#2、#3 前端是具有多個規則的單一 VIP。 使用相同的 IP 位址，但每個前端的連接埠或通訊協定不同。 #1、#4 前端是多 VIP 的範例，在多個 VIP 上重複使用相同的前端通訊協定和連接埠。

Azure Load Balancer 提供定義負載平衡規則的彈性。 規則宣告如何將前端上的位址和連接埠對應至後端上的目的地位址和連接埠。 不同規則是否重複使用後端連接埠，視規則的類型而定。 每種規則類型有特定的需求，會影響主機設定和探查設計的方式。 規則分為兩種：

1. 預設規則，不會重複使用後端連接埠
2. 浮動 IP 規則，會重複使用後端連接埠

Azure Load Balancer 允許您在同一負載平衡器設定上混用兩種規則類型。 負載平衡器可以對指定的 VM同時使用它們，或任何組合，只要您遵守規則的限制。 選擇的規則類型取決於您的應用程式需求以及支援該設定的複雜性。 您應該評估何種規則類型最適合您的案例。

我們將從預設行為開始進一步探討這些案例。

## <a name="rule-type-1-no-backend-port-reuse"></a>規則類型 #1︰不重複使用後端連接埠

![MultiVIP 圖解片](./media/load-balancer-multivip-overview/load-balancer-multivip.png)

在此案例中，前端 VIP 的設定如下︰

| VIP | IP 位址 | protocol | 連接埠 |
| --- | --- | --- | --- |
| ![VIP](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) 1 |65.52.0.1 |TCP |80 |
| ![VIP](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) 2 |*65.52.0.2* |TCP |80 |

DIP 是輸入流量的目的地。 在後端集區中，每個 VM 會公開 DIP 上唯一連接埠上的所需服務。 這項服務是透過規則定義與前端相關聯。

我們定義兩個規則︰

| 規則 | 對應前端 | 至後端集區 |
| --- | --- | --- |
| 1 |![VIP](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) VIP1:80 |![後端](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) DIP1:80, ![後端](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) DIP2:80 |
| 2 |![VIP](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) VIP2:80 |![後端](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) DIP1:81, ![後端](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) DIP2:81 |

現在 Azure Load Balancer 的完整對應如下︰

| 規則 | VIP IP 位址 | protocol | 連接埠 | 目的地 | 連接埠 |
| --- | --- | --- | --- | --- | --- |
| ![規則](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) 1 |65.52.0.1 |TCP |80 |DIP IP 位址 |80 |
| ![規則](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) 2 |65.52.0.2 |TCP |80 |DIP IP 位址 |81 |

每個規則都必須產生具有唯一組合 (目的地 IP 位址和目的地連接埠組合) 的流程。 改變流量的目的地連接埠，多個規則就可以將流量傳送到不同連接埠上的相同 DIP。

健全狀況探查一律會被導向 VM 的 DIP。 您必須確定您的探查會反映 VM 的健全狀況。

## <a name="rule-type-2-backend-port-reuse-by-using-floating-ip"></a>規則類型 #2︰使用浮動 IP 來重複使用後端連接埠

Azure Load Balancer 提供在多個 VIP 重複使用前端連接埠的彈性，不論使用何種規則類型。 此外，在某些應用程式案例中，後端集區中單一 VM 上的多個應用程式執行個體偏好或必須使用相同連接埠。 連接埠重複使用的常見範例包括提供高可用性的叢集、網路虛擬裝置、公開多個不會重新加密的 TLS 端點。

如果您想要在多個規則重複使用後端連接埠，必須啟用規則定義中的浮動 IP。

浮動 IP 是伺服器直接回傳 (DSR) 的一部分。 DSR 包含兩個部分︰流程拓樸和 IP 位址對應配置。 在平台層級，Azure Load Balancer 一律在 DSR 流程拓撲中運作，無論是否已啟用浮動 IP。 這表示流程的輸出部分一律會正確重寫為直接流回原始來源。

使用預設規則類型時，Azure 會公開傳統負載平衡 IP 位址對應配置以利使用的方便性。 啟用浮動 IP 會變更 IP 位址對應配置，以提供更大的彈性，解釋如下。

下圖說明此設定：

![MultiVIP 圖解片](./media/load-balancer-multivip-overview/load-balancer-multivip-dsr.png)

此案例中，後端集區中的每個 VM 有三個網路介面︰

* DIP：與 VM 相關聯的虛擬 NIC (Azure NIC 資源的 IP 組態)
* VIP1︰客體 OS 內的回送介面 (此 OS 已設定了 VIP1 的 IP 位址)
* VIP2︰客體 OS 內的回送介面 (此 OS 已設定了 VIP2 的 IP 位址)

> [!IMPORTANT]
> 邏輯介面的設定是在客體 OS 內進行。 這項設定不是由 Azure 執行或管理。 沒有此設定，規則將無法運作。 健全狀況探查定義使用 VM 的 DIP，而不是邏輯 VIP。 因此，您的服務必須提供 DIP 連接埠的探查回應，以反映邏輯 VIP 上提供之服務的狀態。

讓我們假設前一個案例的相同前端組態︰

| VIP | IP 位址 | protocol | 連接埠 |
| --- | --- | --- | --- |
| ![VIP](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) 1 |65.52.0.1 |TCP |80 |
| ![VIP](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) 2 |*65.52.0.2* |TCP |80 |

我們定義兩個規則︰

| 規則 | 對應前端 | 至後端集區 |
| --- | --- | --- |
| 1 |![規則](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) VIP1:80 |![後端](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) VIP1:80 (在 VM1 和 VM2) |
| 2 |![規則](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) VIP2:80 |![後端](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) VIP2:80 (在 VM1 和 VM2) |

下表顯示負載平衡器的完整對應︰

| 規則 | VIP IP 位址 | protocol | 連接埠 | 目的地 | 連接埠 |
| --- | --- | --- | --- | --- | --- |
| ![VIP](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) 1 |65.52.0.1 |TCP |80 |與 VIP 相同 (65.52.0.1) |與 VIP 相同 (80) |
| ![VIP](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) 2 |65.52.0.2 |TCP |80 |與 VIP 相同 (65.52.0.2) |與 VIP 相同 (80) |

輸入流量的目的地是在 VM 中回送介面上的 VIP 位址。 每個規則都必須產生具有唯一組合 (目的地 IP 位址和目的地連接埠組合) 的流程。 改變流量的目的地 IP 位址，就有可能在相同 VM 上重複使用連接埠。 將您的服務繫結至 VIP 的 IP 位址和個別回送介面的連接埠，即可會向負載平衡器公開服務。

請注意，此範例沒有變更目的地連接埠。 雖然這是浮動 IP 案例，Azure Load Balancer 也支援定義規則來重寫後端的目的地連接埠，使其和前端的目的地連接埠不同。

浮動 IP 規則類型是數種負載平衡器設定模式的基礎。 [具有多個接聽程式的 SQL AlwaysOn](../virtual-machines/windows/sql/virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md) 設定是目前可看到其運用的範例。 經過一段時間，我們會記載更多這類案例。

## <a name="limitations"></a>限制

* 只有 IaaS VM 支援多個 VIP 設定。
* 若使用浮點 IP 規則，您的應用程式必須使用 DIP 輸出流量。 如果您的應用程式繫結至客體 OS 中回送介面上設定的 VIP 位址，就無法使用 SNAT 來重寫輸出流量，流程就會失敗。
* 公用 IP 位址需要費用。 如需詳細資訊，請參閱 [IP 位址定價](https://azure.microsoft.com/pricing/details/ip-addresses/)
* 訂用帳戶有其限制。 如需詳細資訊，請參閱 [服務限制](../azure-subscription-service-limits.md#networking-limits) 的說明。
