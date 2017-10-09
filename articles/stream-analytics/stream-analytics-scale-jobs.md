---
title: "aaaScale 資料流分析工作 tooincrease 輸送量 |Microsoft 文件"
description: "了解如何 tooscale 串流分析工作，藉由設定輸入資料分割、 微調 hello 查詢定義，並設定工作資料流處理單位。"
keywords: "資料串流處理, 串流資料處理, 微調分析"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 7e857ddb-71dd-4537-b7ab-4524335d7b35
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/22/2017
ms.author: jeffstok
ms.openlocfilehash: 4ba8f6b2f8bfebd52cfa07696b501b42cda21f75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="scale-azure-stream-analytics-jobs-tooincrease-stream-data-processing-throughput"></a>向 Azure Stream Analytics 工作 tooincrease 資料流資料處理輸送量
本文章將示範如何 tootune 資料流分析查詢的資料流分析工作的 tooincrease 輸送量。 您將學習如何 tooscale 資料流分析工作設定輸入資料分割、 微調 hello 分析查詢定義，和計算，並設定工作*串流單位*(SUs)。 

## <a name="what-are-hello-parts-of-a-stream-analytics-job"></a>資料流分析工作的 hello 部分有哪些？
串流分析工作的定義包含輸入、查詢及輸出。 輸入如下： hello 工作位置讀取從 hello 資料流。 hello 查詢是使用的 tootransform hello 資料輸入資料流，而 hello 輸出其中 hello 作業會傳送 hello 作業結果。  

一個工作至少需要一個輸入來源來進行資料串流。 hello 資料流輸入的來源可以儲存在 Azure 事件中心或 Azure blob 儲存體中。 如需詳細資訊，請參閱[簡介 tooAzure Stream Analytics](stream-analytics-introduction.md)和[開始使用 Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)。

## <a name="partitions-in-event-hubs-and-azure-storage"></a>事件中樞和 Azure 儲存體中的分割區
調整資料流分析工作 hello 輸入或輸出中會利用資料分割。 資料分割可讓您根據分割索引鍵，將資料分成子集。 取用 hello 資料 （例如資料流分析工作） 的處理序可以使用和寫入不同資料分割，以平行方式，會增加輸送量。 使用串流分析時，您可以利用事件中樞和 Blob 儲存體中的分割區。 

如需有關資料分割的詳細資訊，請參閱下列文章 hello:

* [事件中樞功能概觀](../event-hubs/event-hubs-features.md#partitions)
* [資料分割](https://docs.microsoft.com/azure/architecture/best-practices/data-partitioning#partitioning-azure-blob-storage)


## <a name="streaming-units-sus"></a>串流單位 (SU)
資料流單位 (SUs) 代表 hello 資源且運算能力所需的順序 tooexecute Azure Stream Analytics 工作。 SUs 提供方式 toodescribe hello 相對事件處理為基礎的混合測量結果的 CPU、 記憶體容量和讀寫率。 每個 SU 對應 tooroughly 1 MB/秒的輸送量。 

選擇多少 SUs 所需的特定作業取決於 hello 輸入 hello 磁碟分割設定以及 hello 工作所定義的 hello 查詢。 您可以選取工作 SUs tooyour 配額。 根據預設，每個 Azure 訂用帳戶會在特定地區有向上 too50 SUs 所有 hello 分析作業的配額。 超過這個配額影響，請連絡訂用帳戶的 tooincrease SUs [Microsoft 支援服務](http://support.microsoft.com)。 每個作業有效的 SU 值為 1、3、6 和更大 (以 6 為增量單位)。

## <a name="embarrassingly-parallel-jobs"></a>窘迫平行作業
*平行*作業是 hello 擴充性最高的案例，我們已在 Azure Stream Analytics。 它會連接一個磁碟分割的 hello 輸入的 tooone hello 查詢 tooone 磁碟分割的 hello 輸出執行個體。 此平行處理原則具有下列需求的 hello:

1. 如果您的查詢邏輯取決於相同金鑰所處理的 hello hello 相同查詢執行個體，您必須確定 hello 事件移 toohello 您輸入的相同資料分割。 對於事件中心，這表示 hello 事件資料必須擁有 hello **PartitionKey**值的設定。 或者，您可以使用分割的傳送者。 Blob 儲存體，這表示，傳送嗨事件 toohello 相同的磁碟分割資料夾。 如果您的查詢邏輯不需要相同索引鍵 toobe 處理的 hello hello 相同查詢執行個體，您可以忽略這項需求。 簡單的選取-投影-篩選查詢，即為此邏輯的一個例子。  

2. 一旦 hello 資料配置在 hello 輸入端上，您必須確定您的查詢資料分割。 這需要 toouse **Partition By**中所有的 hello 步驟。 允許多個步驟，但它們都必須由 hello 分割成相同的金鑰。 目前，資料分割索引鍵的 hello 必須設定太**PartitionId** hello 作業 toobe 完全平行的順序。  

3. 目前，只有事件中樞和 blob 儲存體支援已分割的輸出。 事件中樞輸出中，您必須設定 hello 資料分割索引鍵 toobe **PartitionId**。 針對 blob 儲存體的輸出，您不需要 toodo 任何項目。  

4. hello 輸入的資料分割數目必須等於輸出資料分割的 hello 數目。 Blob 儲存體輸出目前不支援分割區。 但是沒關係，因為它繼承 hello 分割 hello 上游查詢的配置。 以下是允許完全平行作業的分割區值範例：  

   * 8 個事件中樞輸入分割區和 8 個事件中樞輸出分割區
   * 8 個事件中樞輸入分割區和 blob 儲存體輸出  
   * 8 個 blob 儲存體輸入分割區和 blob 儲存體輸出  
   * 8 個 blob 儲存體輸入分割區和 8 個事件中樞輸出分割區  

hello 下列各節討論是窘迫平行的一些範例案例。

### <a name="simple-query"></a>簡單查詢

* 輸入：具有 8 個分割區的事件中樞
* 輸出：具有 8 個分割區的事件中樞

查詢：

    SELECT TollBoothId
    FROM Input1 Partition By PartitionId
    WHERE TollBoothId > 100

此查詢是簡單的篩選。 因此，我們不需要有關資料分割正在傳送 toohello 事件中心的 hello 輸入 tooworry。 請注意該 hello 查詢包含**由 PartitionId 分割**，因此它可滿足需求 #2 與前面。 Hello 輸出中，我們需要 tooconfigure hello 事件中樞輸出中 hello 作業 toohave hello 資料分割索引鍵集太**PartitionId**。 一次的最後一個檢查是 toomake 確定 hello 輸入的資料分割數目等於 toohello 輸出資料分割數目。

### <a name="query-with-a-grouping-key"></a>利用群組索引鍵的查詢

* 輸入：具有 8 個分割區的事件中樞
* 輸出：Blob 儲存體

查詢：

    SELECT COUNT(*) AS Count, TollBoothId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

此查詢含有群組索引鍵。 因此，hello 相同索引鍵需求 toobe hello 同樣的查詢執行個體，這表示，事件必須傳送 toohello 事件中樞分割區的方式處理。 但是，應該使用哪個索引鍵？ **PartitionId** 是作業邏輯概念。 我們實際上關心的 hello 索引鍵是**TollBoothId**，因此 hello **PartitionKey** hello 事件資料的值應該是**TollBoothId**。 我們可以在 hello 查詢設定**Partition By**太**PartitionId**。 由於 hello 輸出 blob 儲存體，我們不需要有關設定資料分割索引鍵值，根據需求 #4 tooworry。

### <a name="multi-step-query-with-a-grouping-key"></a>利用群組索引鍵的多重步驟查詢
* 輸入：具有 8 個分割區的事件中樞
* 輸出：具有 8 個分割區的事件中樞執行個體

查詢：

    WITH Step1 AS (
    SELECT COUNT(*) AS Count, TollBoothId, PartitionId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

此查詢的群組索引鍵，因此 hello hello 所處理的相同索引鍵需求 toobe 相同的查詢執行個體。 我們可以使用 hello 同樣的策略，如同 hello 先前的範例。 在此情況下，hello 查詢有多個步驟。 每個步驟都有 **Partition By PartitionId** 嗎？ 是的所以 hello 查詢可滿足需求 #3。 Hello 輸出中，我們需要 tooset hello 資料分割索引鍵太**PartitionId**，如同先前討論一般。 我們也可以查看有 hello 相同數目的資料分割，做為輸入 hello。

## <a name="example-scenarios-that-are-not-embarrassingly-parallel"></a>「非」窘迫平行的範例情節

Hello 前一節，我們也示範了一些平行的案例。 在本節中，我們會討論不符合所有 hello 需求 toobe 平行的案例。 

### <a name="mismatched-partition-count"></a>不相符的分割區計數
* 輸入：具有 8 個分割區的事件中樞
* 輸出：具有 32 個分割區的事件中樞

在此情況下，不論是哪一個 hello 查詢。 如果 hello 輸入的資料分割計數不符合 hello 輸出資料分割計數，不是平行 hello 拓撲。

### <a name="not-using-event-hubs-or-blob-storage-as-output"></a>不使用事件中樞或 blob 儲存體作為輸出
* 輸入：具有 8 個分割區的事件中樞
* 輸出：PowerBI

PowerBI 輸出目前不支援資料分割。 因此，此情節不是窘迫平行。

### <a name="multi-step-query-with-different-partition-by-values"></a>具有不同 Partition By 值的多重步驟查詢
* 輸入：具有 8 個分割區的事件中樞
* 輸出：具有 8 個分割區的事件中樞

查詢：

    WITH Step1 AS (
    SELECT COUNT(*) AS Count, TollBoothId, PartitionId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1 Partition By TollBoothId
    GROUP BY TumblingWindow(minute, 3), TollBoothId

如您所見，會使用第二個步驟的 hello **TollBoothId**為 hello 資料分割索引鍵。 這個步驟不是 hello 相同 hello 第一個步驟，並因此我們必須 toodo 隨機播放。 

hello 前面的範例會顯示某些資料流分析工作太符合 （或不要） 平行的拓撲。 如果它們符合執行，也會具有 hello 可能會達到最大效能。 對於不符合其中一個設定檔的作業，則提供未來更新時的調整指引。 現在，請在 hello 下列各節中使用 hello 一般指引。

## <a name="calculate-hello-maximum-streaming-units-of-a-job"></a>計算 hello 最大資料流處理單位作業
可供資料流分析工作的資料流處理單位的 hello 總數取決於 hello hello hello 作業與 hello 資料分割數目的每個步驟所定義的查詢中的步驟數目。

### <a name="steps-in-a-query"></a>查詢中的步驟
一個查詢可以有一或多個步驟。 每個步驟都 hello 所定義的子查詢**WITH**關鍵字。 hello 查詢超出 hello **WITH**關鍵字 （僅一個查詢） 也會列入步驟中，例如 hello**選取**hello 下列查詢中的陳述式：

    WITH Step1 AS (
        SELECT COUNT(*) AS Count, TollBoothId
        FROM Input1 Partition By PartitionId
        GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1
    GROUP BY TumblingWindow(minute,3), TollBoothId

此查詢有兩個步驟。

> [!NOTE]
> 此查詢在 hello 文件中稍後詳細討論。
>  

### <a name="partition-a-step"></a>分割步驟
分割步驟需要下列條件的 hello:

* 必須分割 hello 輸入的來源。 
* hello**選取**hello 查詢的陳述式必須從資料分割的輸入來源讀取。
* hello 步驟內的 hello 查詢都必須有 hello **Partition By**關鍵字。

當查詢資料分割時，hello 輸入的事件處理和彙總中的個別資料分割群組，而且不會產生輸出事件的每個 hello 群組。 如果您想結合彙總，您必須建立第二個的非資料分割步驟 tooaggregate。

### <a name="calculate-hello-max-streaming-units-for-a-job"></a>計算 hello 串流工作單位的最大值
非資料分割的所有步驟一起就能都相應 toosix 串流單位 (SUs) 的資料流分析工作。 必須分割 tooadd SUs，步驟。 每個分割區可以有 6 個 SU。

<table border="1">
<tr><th>查詢</th><th>Hello 作業的最大 SUs</th></td>

<tr><td>
<ul>
<li>hello 查詢包含一個步驟。</li>
<li>hello 步驟不是資料分割。</li>
</ul>
</td>
<td>6</td></tr>

<tr><td>
<ul>
<li>hello 輸入的資料流分割 3。</li>
<li>hello 查詢包含一個步驟。</li>
<li>hello 步驟已分割。</li>
</ul>
</td>
<td>18</td></tr>

<tr><td>
<ul>
<li>hello 查詢包含兩個步驟。</li>
<li>Hello 步驟都不會分割。</li>
</ul>
</td>
<td>6</td></tr>

<tr><td>
<ul>
<li>hello 輸入的資料流分割 3。</li>
<li>hello 查詢包含兩個步驟。 hello 輸入的步驟已分割，而且不 hello 第二個步驟。</li>
<li>hello<strong>選取</strong>陳述式會從資料分割的 hello 輸入讀取。</li>
</ul>
</td>
<td>24 (18 個用於分割的步驟 + 6 個用於非分割的步驟)</td></tr>
</table>

### <a name="examples-of-scaling"></a>調整的範例

hello 下列查詢會計算 hello 透過付費站台具有三個 tollbooths 在 3 分鐘期間內的汽車數。 此查詢可以 toosix SUs 向上調整。

    SELECT COUNT(*) AS Count, TollBoothId
    FROM Input1
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

多個 toouse SUs 的 hello 查詢、 同時 hello 輸入的資料流和 hello 查詢必須分割。 因為 hello 資料資料流資料分割設定 too3，hello 下列修改過的查詢可以延伸 too18 SUs:

    SELECT COUNT(*) AS Count, TollBoothId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

查詢資料分割，會 hello 輸入的事件處理和個別分割區群組中的彙總資料。 每個 hello 群組，也會產生輸出事件。 資料分割可能會導致一些意外的結果時 hello **GROUP BY**欄位不是 hello hello 輸入的資料流中的資料分割索引鍵。 例如，hello **TollBoothId** hello 先前查詢中的欄位不是 hello 資料分割索引鍵**Input1**。 hello 結果為該 hello 收費站 #1 的資料可以分散在多個資料分割。

每個 hello **Input1**資料分割將分別由處理串流分析。 如此一來，多筆記錄的 hello 汽車計數 hello 相同收費站 hello 會建立相同的輪轉視窗中。 如果無法變更 hello 輸入的資料分割索引鍵，即可修正這個問題加入非分割區的步驟，如 hello 下列範例所示：

    WITH Step1 AS (
        SELECT COUNT(*) AS Count, TollBoothId
        FROM Input1 Partition By PartitionId
        GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1
    GROUP BY TumblingWindow(minute, 3), TollBoothId

此查詢可以縮放的 too24 SUs。

> [!NOTE]
> 如果您要聯結兩個資料流，請確定該 hello 資料流分割 hello hello 資料行的資料分割索引鍵，您會使用 toocreate hello 聯結。 也請確定您已擁有 hello 相同數目的兩個資料流中的資料分割。
> 
> 

## <a name="configure-stream-analytics-streaming-units"></a>設定串流分析串流單位

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. 在 hello 清單中的資源，尋找您想 tooscale，然後再開啟它的 hello 資料流分析工作。
3. 在 hello 作業刀鋒視窗中，在**設定**，按一下 **標尺**。

    ![Azure 入口網站串流分析作業組態][img.stream.analytics.preview.portal.settings.scale]

4. 使用 hello 滑桿 tooset hello SUs hello 工作。 請注意，您是有限的 toospecific SU 的設定。


## <a name="monitor-job-performance"></a>監視工作效能
您可以使用 hello Azure 入口網站，來追蹤工作的 hello 輸送量：

![Azure 串流分析監視工作][img.stream.analytics.monitor.job]

計算預期的 hello hello 工作負載輸送量。 如果少於預期 hello 輸送量，微調 hello 輸入磁碟分割、 微調 hello 查詢，以及加入 SUs tooyour 作業。


## <a name="visualize-stream-analytics-throughput-at-scale-hello-raspberry-pi-scenario"></a>以視覺化方式檢視大規模的資料流分析輸送量： hello 覆盆子 Pi 案例
您了解串流分析工作如何調整的 toohelp，我們執行實驗根據來自覆盆子 Pi 裝置的輸入。 此實驗，可讓我們查看 hello 效果對輸送量的多個資料流處理單位和資料分割。

在此案例中，hello 裝置傳送感應器資料 （用戶端） tooan 事件中心。 資料流分析處理 hello 資料，並以輸出 tooanother 事件中心傳送的警示或統計資料。 

hello 用戶端會以 JSON 格式傳送感應器資料。 hello 資料輸出也是以 JSON 格式。 hello 資料看起來像這樣：

    {"devicetime":"2014-12-11T02:24:56.8850110Z","hmdt":42.7,"temp":72.6,"prss":98187.75,"lght":0.38,"dspl":"R-PI Olivier's Office"}

下列查詢的 hello 光線關閉時使用的 toosend 警示：

    SELECT AVG(lght),
     "LightOff" as AlertText
    FROM input TIMESTAMP
    BY devicetime
     WHERE
        lght< 0.05 GROUP BY TumblingWindow(second, 1)

### <a name="measure-throughput"></a>測量輸送量

在此情況下，輸送量為 hello 在固定的時間內處理的資料流分析的輸入資料的數量。 （我們單位為 10 分鐘）。tooachieve hello 最佳處理輸送量 hello 輸入資料、 hello 資料流輸入和 hello 查詢已進行資料分割。 我們包含**count （)**在 hello 查詢 toomeasure 多少輸入的事件已處理。 toomake 確定 hello 工作已不只等候輸入的事件 toocome，大約 300 MB 的輸入資料已預先載入 hello 輸入的事件中樞的每個資料分割。

hello 下表顯示我們增加的資料流單位數目 hello 和事件中心中的 hello 對應的分割區計數時，我們會看見 hello 結果。  

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

而且 hello 下列圖形會顯示 hello SUs 與輸送量之間的關聯性的視覺效果。

![img.stream.analytics.perfgraph][img.stream.analytics.perfgraph]

## <a name="get-help"></a>取得說明
如需進一步的協助，請參閱我們的 [Azure Stream Analytics 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)。

## <a name="next-steps"></a>後續步驟
* [簡介 tooAzure 資料流分析](stream-analytics-introduction.md)
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
[azure.management.portal]: http://manage.windowsazure.com
[azure.event.hubs.developer.guide]: http://msdn.microsoft.com/library/azure/dn789972.aspx

[stream.analytics.introduction]: stream-analytics-introduction.md
[stream.analytics.get.started]: stream-analytics-real-time-fraud-detection.md
[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.rest.api.reference]: http://go.microsoft.com/fwlink/?LinkId=517301

