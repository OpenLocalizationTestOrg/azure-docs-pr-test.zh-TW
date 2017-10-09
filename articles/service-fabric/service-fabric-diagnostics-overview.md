---
title: "aaaAzure 服務網狀架構監視和診斷的概觀 |Microsoft 文件"
description: "了解如何對 Azure Service Fabric 叢集、應用程式和服務進行監視和診斷。"
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/17/2017
ms.author: dekapur
ms.openlocfilehash: 1ef6419863b056b76d81e915ab78df4facae88bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-and-diagnostics-for-azure-service-fabric"></a>對 Azure Service Fabric 進行監視和診斷

監視和診斷是重大 toodeveloping 測試和任何環境中部署應用程式和服務。 如果您要規劃和實作監視和診斷功能，以協助確保應用程式和服務可在本機開發環境或生產環境中如預期般運作，Service Fabric 解決方案就是理想之選。

hello 主要目標的監視和診斷要：
* 偵測並診斷硬體和基礎結構的問題
* 偵測軟體和應用程式的問題，縮短服務中斷時間
* 了解資源耗用量，以及協助進行磁碟機作業決策
* 最佳化應用程式、服務及基礎結構效能
* 產生商業見解，並找出改善之處


hello 整體的工作流程的監視和診斷包含三個步驟：

1. **事件產生**： 這包括在 hello 基礎結構 （叢集）、 平台和應用程式 / 服務層級的事件記錄檔、 追蹤 （自訂的事件）
2. **事件彙總**： 產生的事件需要 toobe 收集並彙總，然後才能顯示
3. **分析**： 事件必須 toobe 視覺化且可存取某些格式、 tooallow 分析及顯示視需要

多項產品會涵蓋這些三個區域的可用，而且您針對每個可用 toochoose 不同技術。 它是重要 toomake 確定的 hello 各種片段工作一起 toodeliver 的端對端監視您的叢集解決方案。

## <a name="event-generation"></a>事件產生

hello hello 監視和診斷工作流程中的第一個步驟是建立 hello 和產生的事件和記錄檔。 這些事件、 記錄和追蹤會產生兩個層級： hello （包括 hello 叢集、 hello 機器或 Service Fabric 動作） 的平台層或 hello 應用程式層級 （任何檢測會新增部署 toohello 叢集 tooapps 和服務）。 雖然 Service Fabric 預設會提供部分檢測，但這些層級的每個事件皆可自訂。

深入了解[平台層級事件](service-fabric-diagnostics-event-generation-infra.md)和[應用程式層級事件](service-fabric-diagnostics-event-generation-app.md)toounderstand 所提供內容和 tooadd 如何進一步檢測。

Hello 記錄提供者，您想要 toouse 來決定之後, 您需要 toomake 確定您的記錄檔正在彙總，並且正確儲存。

## <a name="event-aggregation"></a>事件彙總

收集 hello 記錄和事件產生應用程式，且您的叢集，我們通常建議使用[Azure 診斷](service-fabric-diagnostics-event-aggregation-wad.md)（比較類似 tooagent 為基礎的記錄檔集合） 或[EventFlow](service-fabric-diagnostics-event-aggregation-eventflow.md)（同處理序記錄檔集合）。

收集使用 Azure 診斷擴充功能的應用程式記錄檔是很適合用於 Service Fabric 服務如果 hello 設定的記錄檔來源和目的地不常變更也有 hello 來源與目的地之間的直接對應。 hello 原因的這就設定 Azure 診斷會發生在 hello 資源管理員層級，所以進行重大變更 toohello 設定需要更新/重新部署 hello 叢集。 此外，若要確保您的記錄檔能更永久儲存在可供各種分析平台存取的位置，這也是最適用的選擇。 這表示，比起採用 EventFlow 這類選項，管線的效率較低。

使用[EventFlow](https://github.com/Azure/diagnostics-eventflow)可讓您 toohave 服務傳送其記錄檔直接 tooan 分析和視覺效果的平台，及/或 toostorage。 其他程式庫 （ILogger、 Serilog 等） 可能會使用 hello 相同目的，但 EventFlow 具有 hello 優點需要同處理序記錄檔收集和 toosupport Service Fabric 服務專用的設計。 這通常會 toohave 數個潛在優點：

* 輕鬆設定及部署
    * 診斷資料收集的 hello 組態只是 hello 服務組態的一部分。 它是簡單 tooalways 保持其 「 同步 」 以 hello 其餘部分的 hello 應用程式
    * 可輕鬆達成個別應用程式或個別服務的設定。
    * 設定資料目的地，透過 EventFlow 只是新增 hello 適當的 NuGet 套件，以及變更 hello *eventFlowConfig.json*檔案
* 彈性
    * hello 應用程式可以傳送 hello 資料每當需要 toogo，只要用戶端程式庫支援 hello 目標資料儲存系統。 您可以視需要新增新的目的地。
    * 可以實作複雜的擷取、篩選和資料彙總規則。
* 存取 toointernal 應用程式資料和內容
    * hello hello 應用程式/服務處理序內執行的診斷子系統擴大範圍與內容資訊一起 hello 追蹤

這兩個選項不會互斥，而是可能 tooget 透過使用其中一種類似工作或其他 hello 時, 無法也更有意義，由這種 tooset 一件事 toonote。 在大部分情況下，使用同處理序的集合合併代理程式可能會導致 tooa 更可靠的監視工作流程。 hello Azure 診斷擴充功能 （代理程式） 可能是您選擇的路徑為平台層級的記錄檔時，您可以使用 EventFlow （內建集合） 您應用程式層級的記錄檔。 一旦您已經了解最適合您，就是您要如何顯示及分析您的資料 toobe 時間 toothink。

## <a name="event-analysis"></a>事件分析

有數個很好的平台 toohello 分析和視覺效果的監視和診斷資料時存在於 hello 市場。 hello 建議的兩個是[OMS](service-fabric-diagnostics-event-analysis-oms.md)和[Application Insights](service-fabric-diagnostics-event-analysis-appinsights.md)到期 tootheir 更佳的整合服務的網狀架構，但您應該也尋找 hello[彈性堆疊](https://www.elastic.co/products)（特別是當您考慮執行叢集離線的環境中）， [Splunk](https://www.splunk.com/)，或您的喜好設定的任何其他平台。

hello 重點您選擇的任何平台應該包含如何舒適您是以 hello 使用者介面和查詢選項，hello 能力 toovisualize 資料和建立簡單易讀的儀表板，並 hello 額外的工具，它們提供 tooenhance 您監視自動向發出警示。

此外您選擇，當您設定 Service Fabric 叢集做為 Azure 資源 toohello 平台，您也可以存取 tooAzure 的方塊外監視的機器，可用於特定的效能及設定監視的度量。

### <a name="azure-monitor"></a>Azure 監視器

您可以使用[Azure 監視器](../monitoring-and-diagnostics/monitoring-overview.md)toomonitor 許多 hello Azure Service Fabric 叢集建立所在的資源。 一組度量 hello[虛擬機器規模集](../monitoring-and-diagnostics/monitoring-supported-metrics.md#microsoftcomputevirtualmachinescalesets)與個別[虛擬機器](../monitoring-and-diagnostics/monitoring-supported-metrics.md#microsoftcomputevirtualmachinescalesetsvirtualmachines)自動收集並顯示 hello Azure 入口網站。 tooview hello 收集資訊，請在 hello Azure 入口網站中，選取 hello 資源群組含有 hello Service Fabric 叢集。 然後，選取 hello 虛擬機器規模集的 tooview。 在 hello**監視**區段中，選取**度量**tooview hello 值的圖表。

![已收集計量資訊的 Azure 入口網站檢視](media/service-fabric-diagnostics-overview/azure-monitoring-metrics.png)

toocustomize hello 圖表，請依照下列中的 hello 指示[Microsoft Azure 中的度量](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md)。 您也可以根據這些計量建立警示，如[在 Azure 監視器中建立 Azure 服務的警示](../monitoring-and-diagnostics/insights-alerts-portal.md)所述。 您可以將警示 tooa 通知服務傳送中所述，使用 web 攔截， [Azure 度量警示上設定的 web 攔截，](../monitoring-and-diagnostics/insights-webhooks-alerts.md)。 Azure 監視器只支援一個訂用帳戶。 如果您需要 toomonitor 多個訂用帳戶，或如果您需要額外的功能，[記錄分析](https://azure.microsoft.com/documentation/services/log-analytics/)、 組件的 Microsoft Operations Management Suite，提供針對在內部部署與雲端架構的整體的 IT 管理解決方案基礎結構。 您可以從 Azure 監視的資料傳送直接 tooLog 分析，以便您可以看到您在單一位置的整個環境度量和記錄檔。

## <a name="next-steps"></a>後續步驟

### <a name="watchdogs"></a>監視程式

監視是不同的服務可以觀賞健全狀況和 hello 健康情況模型階層中的任何項目載入跨服務和報表的健全狀況。 這可協助防止將不會偵測根據 hello 檢視的單一服務的錯誤。 Watchdogs 也是很好的起點 toohost 程式碼執行修復動作，而不需使用者互動 （例如，在特定時間間隔內清除記錄檔儲存體中）。 您可以在[這裡](https://github.com/Azure-Samples/service-fabric-watchdog-service)找到範例監視程式服務實作。

開始使用了解如何將事件和記錄檔產生在 hello[平台層級](service-fabric-diagnostics-event-generation-infra.md)和 hello[應用程式層級](service-fabric-diagnostics-event-generation-app.md)。
