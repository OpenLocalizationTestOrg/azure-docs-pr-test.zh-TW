---
title: "服務網狀架構的平台層級監視 aaaAzure |Microsoft 文件"
description: "深入了解平台層級的事件和記錄檔使用 toomonitor 和診斷 Azure Service Fabric 叢集。"
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
ms.date: 08/24/2017
ms.author: dekapur
ms.openlocfilehash: f8fb1c8b546e05c517ae12c91906acc04cd6eaa6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="platform-level-event-and-log-generation"></a>平台層級事件和記錄產生

## <a name="monitoring-hello-cluster"></a>監視 hello 叢集

它是重要 toomonitor 在 hello 平台層級 toodetermine 不論您的硬體與叢集會如預期般運作。 雖然 Service Fabric 可以保留在硬體故障期間執行的應用程式，但是您仍然需要 toodiagnose 是否發生錯誤的應用程式中或是 hello 基礎結構。 您也應該監視您的叢集 toobetter 規劃容量，協助中新增或移除硬體相關的決策。

Service Fabric 提供五個不同的記錄通道--蜪鎏產生 hello 下列事件：

* 操作通道： 高階 Service Fabric 和 hello 叢集，包括事件節點後面的課程中，新的應用程式部署，所執行的作業或 SF 升級復原等。
* 作業通道 - 詳細：健康情況報告與負載平衡決策
* 資料和通訊通道： 重要的記錄檔和傳訊 (目前僅 hello ReverseProxy) 以及資料路徑 （可靠的服務模型） 所產生的事件
* 資料 （& s） 傳訊通道-詳細： 詳細資訊，其中包含記錄資料和傳訊 （此通道會有極大量的事件） 的 hello 叢集中所有 hello 非關鍵的通道   
* [Reliable Services 事件](service-fabric-reliable-services-diagnostics.md)：程式設計模型特定的事件
* [Reliable Actors 事件](service-fabric-reliable-actors-diagnostics.md)︰程式設計模型特定的事件和效能計數器
* 支援記錄檔： 產生的 Service Fabric 只 toobe 時提供支援，我們所使用的系統記錄檔

這些不同的通道涵蓋大部分 hello 平台層級記錄所建議。 tooimprove 平台層級記錄，請考慮投資更佳了解 hello 健全狀況模型並加入自訂的健康情況報告，以及加入自訂**效能計數器**toobuild 即時的了解 hello 的影響您的服務及 hello 叢集上的應用程式。

### <a name="azure-service-fabric-health-and-load-reporting"></a>Azure Service Fabric 健全狀況和負載報告

Service Fabric 有自己的健全狀況模型，詳述於下列文件：
- [簡介 tooService 網狀架構健全狀況監視](service-fabric-health-introduction.md)
- [回報和檢查服務健全狀況](service-fabric-diagnostics-how-to-report-and-check-service-health.md)
- [新增自訂 Service Fabric 健康狀態報告](service-fabric-report-health.md)
- [檢視 Service Fabric 健康狀態報告](service-fabric-view-entities-aggregated-health.md)

監視健全狀況是重大 toomultiple 層面服務的運作。 當 Service Fabric 執行具名的應用程式升級時，健全狀況監視尤其重要。 Hello 服務的每個升級網域會升級，而是使用 tooyour 客戶之後，hello 升級網域必須通過健全狀況檢查，之後再 hello 部署移 toohello 下一個升級網域。 如果無法達到良好健全狀況狀態，hello 部署會回復，以便 hello 應用程式是在已知的良好狀態。 雖然 hello 服務復原之前，有些客戶可能會受到影響，但大部分的客戶不會發生問題。 此外，較快，而不需要動作從人力運算子 toowait 進行解析。 hello 併入您的程式碼 hello 更有彈性您的服務是 toodeployment 問題的詳細健全狀況檢查。

服務健全狀況的另一個層面會報告從 hello 服務的度量資訊。 度量是在 Service Fabric 中重要的因為它們是使用的 toobalance 資源使用狀況。 計量也可以當做系統健全狀況的指標。 例如，您的應用程式可能有許多服務，而每個執行個體會報告每秒要求數 (RPS) 計量。 如果一項服務使用比另一個服務更多資源，Service Fabric 移動 hello 叢集的服務執行個體 tootry toomaintain 甚至資源使用率。 如需資源耗用量運作方式的詳細說明，請參閱[在 Service Fabric 中使用計量管理資源耗用量和負載](service-fabric-cluster-resource-manager-metrics.md)。

計量也可協助您深入探索服務的運作方式。 經過一段時間，您可以使用標準 toocheck hello 服務作業內預期的參數。 例如，如果趨勢會顯示在上星期一早上 hello 上午 9 點平均 RPS 1000，則您可能設定健康情況報告，提醒您，如果 hello RPS 500 低於或高於 1500。 所有項目可能是最適合的但是可能值得外觀 toobe 確定客戶擁有絕佳的體驗。 您的服務可以定義一組度量，可報告基於健全狀況檢查，但不會影響 hello hello 叢集的資源平衡。 toodo 如此，組 hello 衡量標準權數 toozero。 我們建議您啟動的所有標準的權數各為零，並不增加 hello 加權，直到確定您了解加權 hello 度量資訊會如何影響的叢集資源平衡。

> [!TIP]
> 請勿使用太多的加權計量。 可能很難 toounderstand 為什麼服務執行個體正在移動的平衡。 少數幾個計量就很夠用！

任何資訊指出 hello 健全狀況和應用程式的效能是候選項目的度量和健全狀況報表。 CPU 效能計數器可以告訴您節點的使用情況，但無法讓您知道某個特定服務是否健康，因為可能有多項服務在單一節點上執行。 但是，度量 RPS，處理的項目等所有要求延遲可以都表示特定服務的 hello 健全狀況。

使用程式碼類似 toothis 的 tooreport 健康狀態：

  ```csharp
    if (!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportInstanceHealth(healthInformation);
    }
  ```

tooreport 度量資訊，請使用程式碼類似 toothis:

  ```csharp
    this.Partition.ReportLoad(new List<LoadMetric> { new LoadMetric("MemoryInMb", 1234), new LoadMetric("metric1", 42) });
  ```

### <a name="service-fabric-support-logs"></a>Service Fabric 支援記錄

如果 toocontact Microsoft 技術支援說明需要與 Azure Service Fabric 叢集，則幾乎都需要支援記錄檔。 如果您的叢集裝載於 Azure，建立叢集時會自動設定和收集支援記錄。 hello 記錄會儲存於專用的儲存體帳戶，在您的叢集資源群組中。 hello 儲存體帳戶沒有固定的名稱，但在 hello 帳戶，您會看到 blob 容器和資料表名稱的開頭使用*網狀架構*。 如需有關為獨立叢集設定記錄收集的資訊，請參閱[建立和管理獨立 Azure Service Fabric 叢集](service-fabric-cluster-creation-for-windows-server.md)和[獨立 Windows 叢集的組態設定](service-fabric-cluster-manifest.md)。 獨立 Service Fabric 執行個體，hello 記錄檔應該傳送 tooa 本機檔案共用。 您是**必要**toohave 這些記錄檔中的支援，但是它們不是預期的 toobe 可用 hello Microsoft 客戶支援小組以外的任何人。

## <a name="enabling-diagnostics-for-a-cluster"></a>啟用叢集的診斷

中的這些記錄檔的順序 tootake 優點，強烈建議在叢集建立期間已啟用 「 診斷 」。 藉由開啟診斷]、 [hello 叢集部署時，Windows Azure 診斷無法 tooacknowledge hello 操作、 可靠的服務和 Reliable actors 通道，且儲存 hello 資料將會有說明進一步[彙總的事件Azure 診斷](service-fabric-diagnostics-event-aggregation-wad.md)。

如以上所示，也會選擇性欄位 tooadd 應用程式 Insights (AI) 的檢測金鑰。 如果您選擇的任何事件分析 toouse AI (深入了解相關內容位於[Application Insights 事件分析](service-fabric-diagnostics-event-analysis-appinsights.md))，此處包含 hello AppInsights 資源 instrumentationKey (GUID)。


如果您正在 toodeploy 容器 tooyour 叢集，請加入這個 tooyour"WadCfg > DiagnosticMonitorConfiguration"啟用 WAD toopick 向上 docker 統計資料：

```json
"DockerSources": {
    "Stats": {
        "enabled": true,
        "sampleRate": "PT1M"
    }
},

```

## <a name="measuring-performance"></a>測量效能

叢集的測量效能將協助您了解如何調整您的叢集可以 toohandle 負載和磁碟機決策 (查看更多有關調整叢集[在 Azure 上](service-fabric-cluster-scale-up-down.md)，或[內部](service-fabric-cluster-windows-server-add-remove-nodes.md))。 效能資料也是很有用時，會比較 tooactions 您或您的應用程式和服務可能已執行，當時分析記錄檔中 hello 未來。 

如需使用 Service Fabric 時的效能計數器 toocollect 的清單，請參閱[Service Fabric 中的效能計數器](service-fabric-diagnostics-event-generation-perf.md)

以下是您可以設定收集叢集效能資料的兩個常用方式：

* 使用代理程式： 這是慣用的 hello 方式從電腦收集的效能，因為代理程式通常具有可收集的效能度量的清單，而且它是相當容易的程序 toochoose hello 度量想 toocollect 或加以變更. 閱讀有關[tooconfigure 如何適用於 Service Fabric hello OMS](service-fabric-diagnostics-event-analysis-oms.md)和[hello OMS Windows 代理程式設定](../log-analytics/log-analytics-windows-agents.md)文章 toolearn 更多關於 hello OMS 代理程式，也就是一個可以 toopick 已啟動這類監視代理程式叢集 Vm 和已部署的容器的效能資料。

* 設定診斷 toowrite 效能計數器 tooa 資料表： 在 Azure 上的叢集，這表示從 hello Vm 在叢集中，變更 hello Azure 診斷組態 toopick 向上 hello 適當的效能計數器，並讓它 toopick 向上如果您將會部署任何容器 docker 統計資料。 了解設定[中 WAD 效能計數器](service-fabric-diagnostics-event-aggregation-wad.md)Service Fabric tooset 效能計數器集合中。

## <a name="next-steps"></a>後續步驟

將記錄檔和事件需要 toobe 之前它們可以傳送 tooany 分析平台的彙總資料。 閱讀有關[EventFlow](service-fabric-diagnostics-event-aggregation-eventflow.md)和[WAD](service-fabric-diagnostics-event-aggregation-wad.md) toobetter 了解一些 hello 建議的選項。
