---
title: "調整串流分析工作以增加輸送量 | Microsoft Docs"
description: "了解如何透過設定輸入資料分割、微調查詢定義，及設定工作串流處理單元來調整串流分析工作。"
keywords: "資料串流處理, 串流資料處理, 微調分析"
services: stream-analytics
documentationcenter: 
author: JSeb225
manager: jhubbard
editor: cgronlun
ms.assetid: 7e857ddb-71dd-4537-b7ab-4524335d7b35
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/22/2017
ms.author: jeanb
ms.openlocfilehash: 781a3b71c35cb48e40202e3b1acc8edbbaf865c4
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/11/2017
---
# <a name="scale-azure-stream-analytics-jobs-to-increase--throughput"></a>調整 Azure 串流分析工作以增加輸送量
本文示範如何調整串流分析查詢，以增加串流分析作業的輸送量。 您可以使用以下指南來調整作業，進而處理更高的負載及利用更多系統資源 (如更多頻寬、更多 CPU 資源、更多記憶體)。
依照必要條件的規定，您需要閱讀以下文章：
-   [了解及調整串流處理單位](stream-analytics-streaming-unit-consumption.md)
-   [建立可平行作業](stream-analytics-parallelization.md)


## <a name="case-1--your-query-is-inherently-fully-parallelizable-across-input-partitions"></a>案例 1 – 查詢在輸入分割區之間原本就完全可平行
如果您的查詢在輸入分割區之間原本就完全可平行，可以遵循以下步驟：
1.  使用 **PARTITION BY** 關鍵字撰寫窘迫平行查詢。 如需詳細資料，請參閱[本頁](stream-analytics-parallelization.md)的「窘迫平行作業」一節。
2.  根據查詢使用的輸出類型，某些輸出可能是不可平行或需要進一步設定才能成為窘迫平行。 例如，SQL、SQL DW 和 Power BI 輸出不可平行。 輸出一律會先合併再傳送到輸出接收。 Blob、資料表、ADLS、服務匯流排和 Azure 函式可自動平行化。 CosmosDB 和事件中樞需要將 PartitionKey 組態設定為與 **PARTITION BY** 欄位相符 (通常是 PartitionId)。 另請特別注意，對事件中樞來說，所有輸入和所有輸出的分割區數目應相符，以避免跨越分割區。 
3.  使用 **6 SU** (單一運算節點的完整容量) 來執行查詢，以測量可達成輸送量的最大值；如果您使用 **GROUP BY**，請測量作業可處理的群組數目 (基數)。 達到系統資源限制的作業會出現如下所示的一般徵兆。
    - SU % 使用率計量超過 80%。 這表示記憶體使用量偏高。 若要了解導致這項計量增加的因素，請參閱[這裡](stream-analytics-streaming-unit-consumption.md)的描述。 
    -   輸出時間戳記落後時鐘時間。 根據您的查詢邏輯，輸出時間戳記與時鐘時間之間可能有邏輯位移。 不過，它們的進行的速度大致上應該相同。 如果輸出時間戳記遠遠落後，代表系統過度使用。 這可能是下游輸出接收節流，或 CPU 使用率過高的結果。 目前我們未提供 CPU 使用量度量，因此您可能會很難區分這兩者。
        - 如果此問題是接收節流所引起的，您可能需要增加輸出分割區的數目 (和輸入分割區的數目，以保留作業的完全可平行能力)，或增加接收的資源數量 (如 CosmosDB 的要求單位數目)。
    - 在作業圖表中，每個輸入都有一個按照分割區區分的待辦項目事件計量。 如果待辦項目事件計量持續增加，也代表系統資源受限 (因為輸出接收節流或 CPU 使用率過高)。
4.  假設您沒有任何讓某個分割區「過熱」的資料扭曲，一旦判斷出 6 SU 作業能達到的限制後，您可以在新增更多 SU 時利用線性方式推測作業的處理容量。
>[!Note]
> 請選擇正確的串流處理單位數目：串流分析會為每個新增的 6 SU 建立處理節點，因此節點數目最好是輸入分割區數目的除數，這樣分割區才能平均分配到各個節點。
> 例如，如果您已測量出 6 SU 作業能達成 4 MB/s 的處理速率，那麼您的輸入分割區計數便是 4。 您可以選擇使用 12 SU 來執行作業以達成約 8 MB/s 的處理速率，或使用 24 SU 來達成 16 MB/s 的處理速率。 接著，您可以決定何時要將作業的 SU 數目增加為什麼值，做為輸入速率的函式。



## <a name="case-2---if-your-query-is-not-embarrassingly-parallel"></a>案例 2 - 如果您的查詢不是窘迫平行。
如果您的查詢不是窘迫平行，您可以遵循下列步驟。
1.  先不使用 **PARTITION BY** 來撰寫查詢以避免分割複雜度，接著再使用 6 SU 來執行查詢，以便測量負載，如[案例 1](#case-1--your-query-is-inherently-fully-parallelizable-across-input-partitions)。
2.  如果您可以達到輸送量的預期負載，您就完成了。 您也可以選擇測量以 3 SU 和 1 SU 執行的相同工作，找出適合您案例的最少 SU 數目。
3.  如果您無法達到需要的輸送量，而且查詢原本就不含多個步驟，請試著將查詢分為多個步驟 (若可以的話)，再為查詢中的每個步驟配置 6 SU。 例如，如果您有 3 個步驟，請在 [調整] 選項中配置 18 SU。
4.  在執行這類型的作業時，串流分析會將每個步驟置放於擁有專用 6 SU 資源的專屬節點上。 
5.  如果這樣仍然無法達到負載目標，您可以嘗試從靠近輸入步驟開始使用 **PARTITION BY**。 對於本質上無法分割的 **GROUP BY** 運算子，您可以使用本機/全域彙總模式來執行分割的 **GROUP BY**，後面再加上非分割的 **GROUP BY**。 例如，如果您想要計算每 3 分鐘通過每個收費亭的車輛數目，但是資料量超過 6 SU 的處理能力。

查詢：

    WITH Step1 AS (
    SELECT COUNT(*) AS Count, TollBoothId, PartitionId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )
    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1
    GROUP BY TumblingWindow(minute, 3), TollBoothId

在上述查詢中，您會計算每個分割區中每個收費亭的車輛數目，然後將所有分割區的計數加總。

分割後，請為步驟的每個分割區配置 6 SU (每個分割區最多 6 SU)，讓每個分割區都能置放在自己的處理節點上。

> [!Note]
> 如果您的查詢無法分割，為多重步驟查詢新增額外的 SU 不見得能改善輸送量。 提升效能的其中一個方法，就是使用本機/全域彙總模式減少初始步驟的資料量，如前文步驟 5 所示。

## <a name="case-3---you-are-running-lots-of-independent-queries-in-a-job"></a>案例 3 - 您要在一項作業中執行許多獨立的查詢。
對於某些 ISV 使用案例 (在一項作業中處理多重租用戶資料最符合成本效益的方法) 來說，若是讓每個租用戶使用個別的輸入和輸出，最終您可能只會在一項作業中執行很少數 (如 20 個) 的獨立查詢。 我們的假設是，這類型的子查詢每個負擔的負載相對較小。 此時，您可以遵循以下步驟。
1.  在這種情況下，請勿在查詢中使用 **PARTITION BY**
2.  如果您使用事件中樞，請盡可能將輸入分割區計數減少為最小值 2。
3.  使用 6 SU 執行查詢。 搭配上每個子查詢的預期負載，請盡可能新增這類子查詢的數目，直到作業達到系統資源限制為止。 如需達到限制時的徵兆，請參閱[案例 1](#case-1--your-query-is-inherently-fully-parallelizable-across-input-partitions)。
4.  一旦達到前文測得的子查詢限制後，請開始將子查詢新增到新作業中。 假設您沒有任何負載扭曲，以獨立查詢數目之函式表示的執行作業數目應該會呈現線性的結果。 這樣一來，您就可以根據要提供服務之租用戶數目的函式來預測要執行多少個 6 SU 作業。
5.  在搭配使用參考資料聯結和這些查詢時，您應該在聯結相同的參考資料之前取得輸入的聯集，然後視需要分割事件。 否則，每個參考資料聯結都會將一份參考資料保存在記憶體中，導致記憶體使用量不必要地攀升。

> [!Note] 
> 要在每個作業中放置多少個租用戶？
> 這個查詢模式通常擁有大量的子查詢，造成非常龐大而複雜的拓撲。 作業的控制器可能無法應付這麼龐大的拓撲。 根據經驗法則，1 SU 作業的租用戶應保持低於 40 個，3 SU 和 6 SU 作業的租用戶則應低於 60 個。 當您超過控制器的容量時，作業將無法順利啟動。


## <a name="an-example-of-stream-analytics-throughput-at-scale"></a>大規模串流分析輸送量的範例
為了協助您了解串流分析作業如何調整，我們已根據來自 Raspberry Pi 裝置的輸入完成一項實驗。 此實驗讓我們看到對多個串流單位和分割區的輸送量造成的影響。

在此情節中，裝置會將感應器資料 (用戶端) 傳送到事件中樞。 串流分析會處理資料，並將警示或統計資料當作輸出傳送到另一個事件中樞。 

用戶端會以 JSON 格式傳送感應器資料。 資料輸出也是 JSON 格式。 資料如下所示：

    {"devicetime":"2014-12-11T02:24:56.8850110Z","hmdt":42.7,"temp":72.6,"prss":98187.75,"lght":0.38,"dspl":"R-PI Olivier's Office"}

下列查詢用於關閉燈光開關時傳送警示：

    SELECT AVG(lght), "LightOff" as AlertText
    FROM input TIMESTAMP BY devicetime 
    PARTITION BY PartitionID
    WHERE lght< 0.05 GROUP BY TumblingWindow(second, 1)

### <a name="measure-throughput"></a>測量輸送量

在此案例中，輸送量是串流分析在固定時間內處理的輸入資料量。 (我們測量 10 分鐘。)為了以最佳方式處理輸入資料的輸送量，資料流輸入和查詢都必須分割。 我們在查詢中包含 **COUNT()** 來測量已處理的輸入事件數目。 為了確保作業不會單純地等待輸入事件到來，輸入事件中樞的每個分割區都已預先載入大約 300 MB 的輸入資料。

下表顯示我們在增加串流單位數目時所看到的結果，以及事件中樞裡對應的分割區計數。  

<table border="1">
<tr><th>輸入資料分割</th><th>輸出資料分割</th><th>串流處理單位</th><th>持續的輸送量
</th></td>

<tr><td>12</td>
<td>12</td>
<td>6</td>
<td>4.06 MB/秒</td>
</tr>

<tr><td>12</td>
<td>12</td>
<td>12</td>
<td>8.06 MB/秒</td>
</tr>

<tr><td>48</td>
<td>48</td>
<td>48</td>
<td>38.32 MB/秒</td>
</tr>

<tr><td>192</td>
<td>192</td>
<td>192</td>
<td>172.67 MB/秒</td>
</tr>

<tr><td>480</td>
<td>480</td>
<td>480</td>
<td>454.27 MB/秒</td>
</tr>

<tr><td>720</td>
<td>720</td>
<td>720</td>
<td>609.69 MB/秒</td>
</tr>
</table>

下圖顯示 SU 和輸送量之間的關聯性視覺效果。

![img.stream.analytics.perfgraph][img.stream.analytics.perfgraph]

## <a name="get-help"></a>取得說明
如需進一步的協助，請參閱我們的 [Azure Stream Analytics 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)。

## <a name="next-steps"></a>後續步驟
* [Azure Stream Analytics 介紹](stream-analytics-introduction.md)
* [開始使用 Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Azure Stream Analytics 查詢語言參考](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure 串流分析管理 REST API 參考](https://msdn.microsoft.com/library/azure/dn835031.aspx)

<!--Image references-->

[img.stream.analytics.monitor.job]: ./media/stream-analytics-scale-jobs/StreamAnalytics.job.monitor-NewPortal.png
[img.stream.analytics.configure.scale]: ./media/stream-analytics-scale-jobs/StreamAnalytics.configure.scale.png
[img.stream.analytics.perfgraph]: ./media/stream-analytics-scale-jobs/perf.png
[img.stream.analytics.streaming.units.scale]: ./media/stream-analytics-scale-jobs/StreamAnalyticsStreamingUnitsExample.jpg
[img.stream.analytics.preview.portal.settings.scale]: ./media/stream-analytics-scale-jobs/StreamAnalyticsPreviewPortalJobSettings-NewPortal.png   

<!--Link references-->

[microsoft.support]: http://support.microsoft.com
[azure.event.hubs.developer.guide]: http://msdn.microsoft.com/library/azure/dn789972.aspx

[stream.analytics.introduction]: stream-analytics-introduction.md
[stream.analytics.get.started]: stream-analytics-real-time-fraud-detection.md
[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.rest.api.reference]: http://go.microsoft.com/fwlink/?LinkId=517301

