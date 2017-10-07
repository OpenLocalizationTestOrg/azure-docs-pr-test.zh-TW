---
title: "Azure Stream Analytics： 有效率地最佳化您的工作 toouse 串流單位 |Microsoft 文件"
description: "查詢 Azure 串流分析中關於規模與效能的最佳做法。"
keywords: "串流單位、查詢效能"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: 5ad98b34d625190a879260f54c9eff0294e230cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-your-job-toouse-streaming-units-efficiently"></a>有效率地最佳化您的工作 toouse 串流單位

Azure Stream Analytics 彙總 hello 效能"weight"的資料流處理單位 (SUs) 到執行作業。 SUs 代表 hello 運算資源的取用的 tooexecute 作業。 SUs 提供方式 toodescribe hello 相對事件處理為基礎的混合測量結果的 CPU、 記憶體容量和讀寫率。 這個容量可讓您專注於 hello 查詢邏輯並移除您就不需要 tooknow 儲存層的效能考量，以手動方式，您的工作配置記憶體並及時近似 hello CPU core-所需的計數 toorun 您的工作。

## <a name="how-many-sus-are-required-for-a-job"></a>一個作業需要多少 SU？

選擇的特定作業的必要 SUs 的 hello 數目取決於 hello hello 輸入和 hello 工作內所定義的 hello 查詢的資料分割組態。 hello**標尺**刀鋒視窗可讓您 tooset hello SUs 的權限數目。 它會是最佳作法 tooallocate 比所需的多個 SUs。 延遲及輸送量 hello 成本的配置額外的記憶體最佳化 hello Stream Analytics 處理引擎。

Hello 最佳作法一般是未使用之查詢的 6 sus toostart *PARTITION BY*。 使用您在其中修改 hello SUs 數目後代表性的資料量並檢查 hello SU %使用量度量的試驗方法，然後判斷 hello 成問題。

Azure Stream Analytics 中保留事件視窗中啟動任何處理之前，先呼叫 hello"重新排序緩衝區 」。 事件會依照 hello 重新排列視窗內的時間，和後續作業 hello 暫時排序事件。 依時間排列的事件可確保該 hello 運算子具有入所有資料行的可見性 hello 事件 hello 中的約定的時間範圍內。 它也可讓 hello 運算子執行 hello 必要的處理，以及產生的輸出。 這項機制的副作用是 hello hello 重新排列視窗持續時間會因為延遲處理。 hello hello 作業 （影響 SU 耗用量） 的記憶體耗用量是大小的 hello 數目這個重新排列視窗和 hello 事件包含在它的函式。

> [!NOTE]
> 讀取器的 hello 數目變更時升級作業期間，暫時性的警告會寫入 tooaudit 記錄檔。 串流分析作業會從這些暫時性問題中自動復原。

## <a name="common-high-memory-causes-for-high-su-usage-for-running-jobs"></a>常見的高效能記憶體會需要高 SU 使用率來執行作業

### <a name="high-cardinality-for-group-by"></a>分組依據的高基數

內送事件的 hello 基數規定 hello 作業的記憶體使用量。

例如，在`SELECT count(*) from input group by clustered, tumblingwindow (minutes, 5)`，hello 與相關聯的數字**叢集**是 hello 查詢的 hello 基數。

toomitigate 問題所造成的高基數，藉由增加使用的資料分割延展 hello 查詢**PARTITION BY**。

```
Select count(*) from input
Partition By clusterid
GROUP BY clustered tumblingwindow (minutes, 5)
```

hello 數目*叢集*是 hello 的基數 GROUP BY 這裡。

分割 hello 查詢之後，它是分散在多個節點。 如此一來，hello 進入到每個節點中的事件數目會降低，這又可以降低 hello hello 重新排序緩衝區大小。 您也應該依據 partitionid 分割事件中樞的分割區。

### <a name="high-unmatched-event-count-for-join"></a>JOIN 的高量不相符事件計數

不相符的事件聯結中的 hello 數目會影響 hello 查詢 hello 記憶體使用量。 例如，採用正在尋找的廣告效果 toofind hello 數目，會產生按下的查詢：

```
SELECT id from clicks INNER JOIN,
impressions on impressions.id = clicks.id AND DATEDIFF(hour, impressions, clicks) between 0 AND 10
```

在此案例中，很可能會顯示許多廣告，但只產生少數點擊數。 這類結果需要 hello 作業 tookeep hello 的時間間隔內的所有 hello 事件。 hello 耗用數量是記憶體的成比例 toohello 視窗大小和事件速率。 

toomitigate 此情況下，向外延展藉由增加 hello 查詢分割分割區藉由使用。 

分割 hello 查詢之後，它是分散在多個處理節點。 如此一來，hello 進入到每個節點中的事件數目會降低，這又可以降低 hello hello 重新排序緩衝區大小。

### <a name="large-number-of-out-of-order-events"></a>大量的順序錯亂事件 

大量的大型的時間間隔內的失序的事件會造成較大 hello"重新排序緩衝區"toobe hello 大小。 toomitigate 此情況下，藉由增加小數位數 hello 查詢分割分割區藉由使用。 分割 hello 查詢之後，它是分散在多個節點。 如此一來，hello 進入到每個節點中的事件數目會降低，這又可以降低 hello hello 重新排序緩衝區大小。 


## <a name="get-help"></a>取得說明
如需進一步的協助，請參閱我們的 [Azure Stream Analytics 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)。

## <a name="next-steps"></a>後續步驟
* [簡介 tooAzure 資料流分析](stream-analytics-introduction.md)
* [開始使用 Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [調整 Azure Stream Analytics 工作](stream-analytics-scale-jobs.md)
* [Azure 串流分析查詢語言參考](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure 串流分析管理 REST API 參考](https://msdn.microsoft.com/library/azure/dn835031.aspx)
