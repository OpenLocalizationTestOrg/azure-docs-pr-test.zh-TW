---
title: "在 Azure Log Analytics aaaUnderstanding 警示 |Microsoft 文件"
description: "警示記錄分析中的識別您的 OMS 儲存機制中的重要資訊和可以主動通知您的問題或叫用動作 tooattempt toocorrect 它們。  本文說明 hello 各種不同的警示規則和定義的方式。"
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 6cfd2a46-b6a2-4f79-a67b-08ce488f9a91
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/26/2017
ms.author: bwren
ms.openlocfilehash: bfa0a5aaeca81674e79a6d647f36d937efeeb439
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-alerts-in-log-analytics"></a>了解 Log Analytics 中的警示

Log Analytics 中的警示會識別您的 Log Analytics 儲存機制中的重要資訊。  本文提供中記錄分析工作如何警示規則的詳細資料，並描述 hello 不同類型的警示規則的差異。

建立警示規則的 hello 程序，請參閱下列文章的 hello:

- 使用 [Azure 入口網站](log-analytics-alerts-creating.md)建立警示規則
- 使用 [Resource Manager 範本](../operations-management-suite/operations-management-suite-solutions-resources-searches-alerts.md)建立叢集規則
- 使用 [REST API](log-analytics-api-alerts.md) 建立警示規則


## <a name="alert-rules"></a>警示規則

警示會由自動定期執行記錄搜尋的警示規則所建立。  如果 hello hello 記錄搜尋結果符合特定準則，則會建立警示的記錄。  hello 規則然後就可以自動執行一個或多個動作 tooproactively 通知您 hello 警示，或叫用另一個處理序。  不同類型的警示規則會使用不同的邏輯 tooperform 這項分析。

![Log Analytics 警示](media/log-analytics-alerts/overview.png)

警示規則的定義方式 hello 下列詳細資料：

- **記錄搜尋**。  hello 每次引發 hello 警示規則會執行的查詢。  此查詢所傳回的 hello 記錄是使用的 toodetermine 是否建立警示。
- **時間範圍**。  指定 hello hello 查詢的時間範圍。  hello 查詢會傳回目前時間的 hello 這個範圍內所建立的記錄。  可以是介於 5 分鐘與 24 小時之間的任何值。 例如，如果 hello too60 分鐘和 hello 查詢設定 視窗的時間執行於 1:15 PM，會傳回 1:15 PM 12:15 PM 之間建立的記錄。
- **頻率**。  指定頻率 hello 應該執行查詢。 可以是介於 5 分鐘與 24 小時之間的任何值。 應該是等於 tooor 小於 hello 時間間隔。  如果 hello 值大於 hello 的時段，然後可能會遺漏的記錄。<br>例如，請考慮 30 分鐘的時間範圍，以及 60 分鐘的頻率。  如果 hello 查詢 1:00 執行，它會傳回 12:30 下午 1:00 之間的記錄。  hello hello 查詢就會執行下一次為 2:00 時，它就會傳回 1:30 到 2:00 之間的記錄。  1:00 和 1:30 之間建立的任何記錄一律不會評估。
- **閾值**。  hello hello 記錄搜尋結果會評估的 toodetermine 是否應該建立警示。  hello 臨界值是不同的 hello 不同類型警示的規則。

Log Analytics 中的各個警示規則是兩種類型其中之一。  Hello 以下各節中詳細說明每個類型。

- **[結果數目](#number-of-results-alert-rules)**。 建立 hello 數字的記錄傳回 hello 記錄搜尋時的單一警示超過指定數字。
- **[計量測量](#metric-measurement-alert-rules)**。  Hello hello 超過指定臨界值的值的記錄搜尋結果中每個物件已建立警示。

hello 警示規則類型之間的差異如下所示。

- **結果數目**警示規則永遠會建立單一警示時**度量的度量**警示規則建立的每個物件已經超過 hello 臨界值警示。
- **結果數目**hello 閾值超過一次時，警示規則建立警示。 **度量的度量**警示規則超過 hello 臨界值時，可以建立警示特定數目的一段特定時間間隔的時間。

## <a name="number-of-results-alert-rules"></a>結果數目警示規則
**結果數目**hello hello 搜尋查詢所傳回的記錄數目超過 hello 指定的臨界值時，警示規則會建立單一警示。

### <a name="threshold"></a>閾值
hello 閾值**的結果數目**警示規則是只是大於或小於特定值。  如果 hello hello 記錄搜尋所傳回的記錄數目符合此準則，則會建立警示。

### <a name="scenarios"></a>案例

#### <a name="events"></a>事件
這種類型的警示規則適用於處理例如 Windows 事件記錄、Syslog 和自訂記錄的事件。  取得建立特定的錯誤事件，或特定的時間間隔內建立多個錯誤事件時，您可能想 toocreate 警示。

單一事件，hello 數目比 0，而 hello 頻率和時間視窗 too5 分鐘結果 toogreater tooalert。  每隔 5 分鐘到 hello 次出現的單一事件，因為已執行 hello 最後一次時間 hello 查詢所建立的檢查執行 hello 查詢。  較長的頻率可能會延遲 hello hello 事件所收集到 hello 警示建立時間。

有些應用程式可能會記錄不一定會產生警示的偶發錯誤。  比方說，hello 應用程式可能會重試建立 hello 錯誤事件的 hello 程序，然後成功 hello 下一次。  在此情況下，您可能不想 toocreate hello 警示除非特定的時間間隔內建立多個事件。  

在某些情況下，您可能想 toocreate 警示，在 hello 事件不存在。  例如，處理程序可能會記錄它可以正常運作的一般事件 tooindicate。  如果它不在特定的時間範圍內記錄一個事件，則應建立警示。  在此情況下您會設定 hello 閾值太**小於 1**。

#### <a name="performance-alerts"></a>效能警示
[效能資料](log-analytics-data-sources-performance-counters.md)儲存為 hello tooevents 類似的 OMS 儲存機制中的記錄。  如果您想 tooalert 效能計數器超過特定閾值時，該臨界值應該包含在 hello 查詢中。

例如，如果您想 tooalert 時 hello 處理器會執行一段 90%，您會使用 hello hello hello 警示規則的臨界值與下列類似的查詢**大於 0**。

    Type=Perf ObjectName=Processor CounterName="% Processor Time" CounterValue>90

如果您想 tooalert hello 處理器的平均值超過特定時段的 90%時，您會使用查詢，使用 hello[測量命令](log-analytics-search-reference.md#commands)像 hello hello 警示規則的臨界值與 hello 面**大於 0**.

    Type=Perf ObjectName=Processor CounterName="% Processor Time" | measure avg(CounterValue) by Computer | where AggregatedValue>90

>[!NOTE]
> 如果您的工作區已升級的 toohello[新的記錄分析查詢語言](log-analytics-log-search-upgrade.md)，然後 hello 上述查詢會變更 toohello 下列：`Perf | where ObjectName=="Processor" and CounterName=="% Processor Time" and CounterValue>90`
> `Perf | where ObjectName=="Processor" and CounterName=="% Processor Time" | summarize avg(CounterValue) by Computer | where CounterValue>90`


## <a name="metric-measurement-alert-rules"></a>公制度量單位的警示規則

>[!NOTE]
> 計量測量警示規則目前處於公開預覽狀態。

**計量測量**警示規則會針對查詢中其值超過指定閾值的每個物件建立警示。  它們有遵循不同的差異，從 hello**的結果數目**警示規則。

#### <a name="log-search"></a>記錄搜尋
雖然您可以使用任何查詢**的結果數目**警示規則，有特定需求 hello 查詢度量的度量的警示規則。  它必須包括[測量命令](log-analytics-search-reference.md#commands)toogroup hello 結果上的特定欄位。 此命令必須包含下列項目 hello。

- **彙總函式**。  判斷執行 hello 計算，以及可能數字欄位 tooaggregate。  例如， **count （)**會在 hello 查詢中，傳回記錄的 hello 數目**avg(CounterValue)**會傳回 hello 平均 hello CounterValue 欄位的一段 hello 間隔。
- **群組欄位**。  系統會為這個欄位中的每個執行個體建立帶有彙總值的記錄，而且每個執行個體都可產生警示。  例如，如果您想 toogenerate 警示每一部電腦，您會使用**電腦**。   
- **間隔**。  定義 hello hello 資料彙總經過的時間間隔。  例如，如果您指定**5**，會建立一則記錄，每隔 5 分鐘時段彙總 hello hello 警示指定 hello 群組欄位的每個執行個體。

#### <a name="threshold"></a>閾值
hello 度量的度量的警示規則的臨界值是由彙總的值和定義的。  如果在 hello 記錄搜尋中任何資料點超過此值，其會被視為有入侵。  如果 hello 漏洞 hello 結果中的任何物件的數目超過 hello 指定的值，然後建立該物件的警示。

#### <a name="example"></a>範例
假設您想要在任何電腦於過去 30 分鐘內發生三次處理器使用率超過 90% 時收到警示。  您會建立警示規則，以 hello 下列詳細資料。  

**查詢：**Type=Perf ObjectName=Processor CounterName="% Processor Time" | measure avg(CounterValue) by Computer Interval 5minute<br>
**時間範圍︰**30 分鐘<br>
**警示頻率︰**5 分鐘<br>
**彙總值︰**大於 90<br>
**警示觸發依據︰**違規總數大於 5<br>

hello 查詢會建立每一部電腦的平均值在 5 分鐘的時間間隔。  此查詢會執行收集的資料每隔 5 分鐘透過 hello 前 30 分鐘。  三部電腦的資料範例如下所示。

![查詢結果範例](media/log-analytics-alerts/metrics-measurement-sample-graph.png)

在此範例中，個別的警示會建立 srv02 和 srv03 因為它們透過 hello 時段違反 hello 90%閾值 3 次。  如果 hello**警示觸發程序為基礎：**已變更過**Consecutive**則會僅針對 srv03 建立警示，因為它違反 hello 3 個連續取樣閾值。

## <a name="alert-records"></a>警示記錄
在 Log Analytics 中由警示規則建立的警示記錄，**Type** 為 **Alert**，**SourceSystem** 為 **OMS**。  所以在下表中的 hello 有 hello 屬性。

| 屬性 | 說明 |
|:--- |:--- |
| 類型 |*警示* |
| SourceSystem |*OMS* |
| *Object*  | [度量的度量警示](#metric-measurement-alert-rules)都會有 hello 群組欄位的屬性。  比方說，如果 hello 記錄搜尋群組的電腦，hello 警示記錄有電腦 hello hello 電腦名稱做為 hello 值。
| AlertName |Hello 警示名稱。 |
| AlertSeverity |Hello 警示的嚴重性層級。 |
| LinkToSearchResults |連結 tooLog 分析記錄搜尋，傳回從建立 hello 警示的 hello 查詢 hello 記錄。 |
| 查詢 |已執行的 hello 查詢的文字。 |
| QueryExecutionEndTime |Hello hello 查詢的時間範圍的結尾。 |
| QueryExecutionStartTime |Hello hello 查詢的時間範圍的開頭。 |
| ThresholdOperator | Hello 警示規則所使用的運算子。 |
| ThresholdValue | Hello 警示規則所使用的值。 |
| TimeGenerated |建立日期和時間的 hello 警示。 |

有其他種類的 hello 所建立的警示記錄[警示管理解決方案](log-analytics-solution-alert-management.md)和[Power BI 會將匯出](log-analytics-powerbi.md)。  這些記錄的 **Type** 均為 **Alert**，但依其 **SourceSystem** 區分。


## <a name="next-steps"></a>後續步驟
* 安裝 hello[警示管理解決方案](log-analytics-solution-alert-management.md)從 System Center Operations Manager 收集 tooanalyze 警示與警示一起建立記錄分析中。
* 深入了解可產生警示的 [記錄檔搜尋](log-analytics-log-searches.md) 。
* 完成 [設定 Webook](log-analytics-alerts-webhooks.md) 和警示規則的逐步解說。  
* 深入了解如何 toowrite [Azure 自動化中的 runbook](https://azure.microsoft.com/documentation/services/automation) tooremediate 警示所識別的問題。
