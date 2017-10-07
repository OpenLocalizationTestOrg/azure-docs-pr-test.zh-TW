---
title: "aaaUse 參考資料與查閱資料表中資料流分析 |Microsoft 文件"
description: "在串流分析查詢中使用參考資料"
keywords: "查閱資料表, 參考資料"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 06103be5-553a-4da1-8a8d-3be9ca2aff54
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: fb1d18fba920db5e097d0c95d333e8e8390d1589
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-reference-data-or-lookup-tables-in-a-stream-analytics-input-stream"></a>在串流分析的輸入串流中使用參考資料或查詢資料表
參考資料 （也稱為查閱資料表） 是有限的資料集是靜態，或降低的本質，變更使用 tooperform 查閱或 toocorrelate 與資料流。 toomake 使用參考資料在 Azure Stream Analytics 工作中，您通常會使用[參考資料 Join](https://msdn.microsoft.com/library/azure/dn949258.aspx)在查詢中。 串流分析會為 hello 參考資料的儲存層的 Azure Blob 儲存體和 Azure Data Factory 參考資料可以是轉換後及/或複製 tooAzure Blob 儲存體，用來參考資料做[任意數目的雲端和在內部部署資料存放區](../data-factory/data-factory-data-movement-activities.md)。 參考資料會以一連串 blob （hello 輸入組態中定義），以遞增的 hello 日期/時間 hello blob 名稱中指定的模型化。 它**只**支援 toohello hello 序列的結尾加入使用日期/時間**大於**比 hello hello 最後一個 blob 中所指定 hello 序列中。

資料流分析**100 mb 的限制每個 blob**但作業可以處理多個參考 blob 使用 hello**路徑模式**屬性。


## <a name="configuring-reference-data"></a>設定參考資料
tooconfigure 您參考的資料，您必須先 toocreate 的型別輸入**參考資料**。 hello 下表說明每個屬性，您將需要 tooprovide 時使用其描述建立 hello 參考資料輸入：


<table>
<tbody>
<tr>
<td>屬性名稱</td>
<td>說明</td>
</tr>
<tr>
<td>輸入別名</td>
<td>這個輸入將用於 hello 工作查詢 tooreference 中的易記名稱。</td>
</tr>
<tr>
<td>儲存體帳戶</td>
<td>hello hello blob 的所在位置的儲存體帳戶名稱。 如果是在 hello 做為資料流分析工作的相同訂用帳戶，您也可以從選取 hello 下拉式清單。</td>
</tr>
<tr>
<td>儲存體帳戶金鑰</td>
<td>hello 秘密金鑰與 hello 儲存體帳戶相關聯。 這會自動填入 hello hello 儲存體帳戶是否相同的訂用帳戶與串流分析工作。</td>
</tr>
<tr>
<td>儲存體容器</td>
<td>容器提供 blob 儲存在 hello Microsoft Azure Blob 服務中的邏輯分組。 當您上傳 blob toohello Blob 服務時，您必須指定該 blob 的容器。</td>
</tr>
<tr>
<td>路徑格式</td>
<td>使用 toolocate hello 指定容器中的 blob hello 路徑。 Hello 路徑內，您可以選擇 toospecify hello 下列 2 個變數的一或多個執行個體：<BR>{date}、{time}<BR>範例 1：products/{date}/{time}/product-list.csv<BR>範例 2：products/{date}/product-list.csv
</tr>
<tr>
<td>日期格式 [選用]</td>
<td>如果您已經使用 {date} hello 您指定的路徑模式中，您可以從支援的格式 hello 下拉式清單選取 hello 編排您的 blob 的日期格式。<BR>範例︰YYYY/MM/DD、MM/DD/YYYY 等。</td>
</tr>
<tr>
<td>時間格式 [選用]</td>
<td>如果您已經使用 {time} hello 您指定的路徑模式中，您可以從支援的格式 hello 下拉式清單選取 hello 編排您的 blob 的時間格式。<BR>範例︰HH、HH/mm 或 HH-mm</td>
</tr>
<tr>
<td>事件序列化格式</td>
<td>確定您的查詢工作 hello 您預期的方式，串流分析 toomake 需要的 tooknow 為傳入的資料流正在使用哪一種序列化格式。 參考資料 hello 支援的格式為 CSV 和 JSON。</td>
</tr>
<tr>
<td>編碼</td>
<td>Utf-8 是 hello 此時只支援編碼格式</td>
</tr>
</tbody>
</table>

## <a name="generating-reference-data-on-a-schedule"></a>產生排程上的參考資料
如果參考資料是緩時變更的資料集，藉由在使用 hello {date} 及 {time} 替代語彙基元的 hello 輸入組態中指定路徑模式已啟用支援重新整理參考資料。 資料流分析會拾取 hello 更新參考資料定義依據這個路徑模式。 例如，模式的`sample/{date}/{time}/products.csv`使用的日期格式**"YYYY-MM-DD"**和時間格式的**"HH mm"**指示 hello 更新 blob 上的資料流分析 toopick`sample/2015-04-16/17-30/products.csv`年 4 月下午 5:3016，2015 UTC 時區為準。

> [!NOTE]
> 目前資料流分析工作時看起來 hello blob 重新整理只 hello 機器時間往前推進 toohello 時間，並在 hello blob 名稱編碼。 例如，將會尋找 hello 作業`sample/2015-04-16/17-30/products.csv`儘速但前面沒有比下午 5:30 於 2015 年 4 月 16 日 UTC 時區。 它會*從未*尋找編碼時間早於 hello 探索到的最後一個 blob。
> 
> 例如 一旦 hello 作業尋找 hello blob`sample/2015-04-16/17-30/products.csv`就會忽略所有的檔案編碼的日期早於 2015 年 4 月 16 日下午 5:30，如果晚期抵達`sample/2015-04-16/17-25/products.csv`blob 取得中建立 hello 相同容器 hello 作業不會使用它。
> 
> 同樣地如果`sample/2015-04-16/17-30/products.csv`，才會產生在 2015 年 4 月 16 日下午 10:03，但沒有與較早日期的 blob 存在 hello 容器中，hello 作業將會使用在 2015 年 4 月 16 日下午 10:03 啟動這個檔案，並使用之前的 hello 先前的參考資料。
> 
> 例外狀況 toothis 是在 hello 作業必須回到過去 toore 同處理序資料，或者 hello 作業初次啟動時。 在開始時間 hello 作業正在尋找 hello 產生 hello 作業指定的開始時間之前的最新 blob。 這是沒有的 tooensure**非空白**hello 作業啟動時，參考資料集。 如果無法找到一個，hello 作業就會顯示下列診斷 hello: `Initializing input without a valid reference data blob for UTC time <start time>`。
> 
> 

[Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/)可以建立 hello 更新 blob 所需的資料流分析 tooupdate 參考資料定義使用的 tooorchestrate hello 工作。 Data Factory 是以雲端為基礎的資料整合服務會協調及自動 hello 移動和轉換資料。 Data Factory 支援[連接 tooa 大量的雲端和內部部署資料存放區](../data-factory/data-factory-data-movement-activities.md)和您指定的定期輕鬆地移動資料。 如需詳細資訊和逐步指引 tooset 向上 Data Factory 的預先定義的排程重新整理的資料流分析管線 toogenerate 參考資料的方式，請參閱這[GitHub 範例](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ReferenceDataRefreshForASAJobs)。

## <a name="tips-on-refreshing-your-reference-data"></a>重新整理參考資料的秘訣
1. 覆寫參考資料 blob 不會造成資料流分析 tooreload hello blob，而且在某些情況下它可能會導致 hello 作業 toofail。 hello 的建議方式 toochange 參考資料是 tooadd 新 blob 使用相同的容器和路徑模式定義 hello 作業輸入中的 hello 和使用日期/時間**大於**比 hello hello 最後一個 blob 中所指定 hello 序列中。
2. 參考資料 blob**不**排序 hello blob 的 「 上次修改 」 的時間，但只能由 hello 時間與 hello blob 名稱使用 hello {date} 及 {time} 替代項目中指定的日期。
3. 在一些情況下，作業必須回到之前的時間，因此參照資料不得被更改或刪除。

## <a name="get-help"></a>取得說明
如需進一步的協助，請參閱我們的 [Azure Stream Analytics 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>後續步驟
您已經導入了的 tooStream 分析，資料流分析的資料是來自 hello 物聯網的受管理的服務。 toolearn 進一步了解這項服務，請參閱：

* [開始使用 Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [調整 Azure Stream Analytics 工作](stream-analytics-scale-jobs.md)
* [Azure Stream Analytics 查詢語言參考](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure 串流分析管理 REST API 參考](https://msdn.microsoft.com/library/azure/dn835031.aspx)

<!--Link references-->
[stream.analytics.developer.guide]: ../stream-analytics-developer-guide.md
[stream.analytics.scale.jobs]: stream-analytics-scale-jobs.md
[stream.analytics.introduction]: stream-analytics-real-time-fraud-detection.md
[stream.analytics.get.started]: stream-analytics-get-started.md
[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.rest.api.reference]: http://go.microsoft.com/fwlink/?LinkId=517301
