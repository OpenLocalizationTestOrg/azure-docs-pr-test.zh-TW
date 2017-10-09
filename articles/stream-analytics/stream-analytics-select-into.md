---
title: "aaaDebug Azure 串流分析查詢使用 SELECT INTO |Microsoft 文件"
description: "在串流分析中使用 SELECT INTO 陳述式對進行中的查詢進行資料取樣"
keywords: 
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 9952e2cf-b335-4a5c-8f45-8d3e1eda2e20
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: 27e41af1a6ea06b4509d07a3a67087490d0ec1fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="debug-queries-by-using-select-into-statements"></a>使用 SELECT INTO 陳述式對查詢進行偵錯

在即時的資料處理，得知哪些 hello 資料似乎 hello 中間 hello 的查詢可以是很有幫助。 由於 Azure 串流分析作業的輸入或步驟可以讀取多次，因此您可以寫入額外的 SELECT INTO 陳述式。 這樣會輸出到儲存體的中繼資料並可讓您檢查 hello 正確性的 hello 資料，就像*監看變數*執行時偵錯程式。

## <a name="use-select-into-toocheck-hello-data-stream"></a>使用 SELECT INTO toocheck hello 資料流

hello Azure Stream Analytics 工作中的下列範例查詢有一個資料流輸入、 兩個參考資料輸入和輸出 tooAzure 資料表儲存體。 hello 查詢會聯結來自 hello 事件中樞與兩個參考 blob tooget hello 名稱和類別目錄資訊的資料：

![SELECT INTO 查詢範例](./media/stream-analytics-select-into/stream-analytics-select-into-query1.png)

請注意，執行 hello 工作時，正在 hello 輸出中產生任何事件。 在 hello**監視**磚，在這裡顯示，您可以看到 hello 輸入產生的資料，但是您不知道哪一個步驟中的 hello**聯結**造成所有 hello 事件 toobe 卸除。

![hello 監視磚](./media/stream-analytics-select-into/stream-analytics-select-into-monitor.png)
 
在此情況下，您可以加入幾個額外 SELECT INTO 陳述式太 「 記錄 」 hello 中繼聯結結果和 hello 讀取資料，從輸入 hello。

在此範例中，我們新增了兩個新的「暫存輸出」。 這些暫存輸出可以是您喜歡的任何接收體。 在這裡我們使用 Azure 儲存體作為範例︰

![新增額外的 SELECT INTO 陳述式](./media/stream-analytics-select-into/stream-analytics-select-into-outputs.png)

然後，您可以重新撰寫 hello 查詢如下：

![重新撰寫 SELECT INTO 查詢](./media/stream-analytics-select-into/stream-analytics-select-into-query2.png)

現在 hello 作業重新啟動，並讓它在幾分鐘後執行。 然後，請查詢 temp1 和 temp2 以 Visual Studio Cloud Explorer tooproduce hello 下列資料表：

**temp1 資料表**
![SELECT INTO temp1 資料表](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-1.png)

**temp2 資料表**
![SELECT INTO temp2 資料表](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-2.png)

如您所見，temp1 和 temp2 都有資料，並 hello 名稱資料行都已填妥正確 temp2。 不過，因為輸出中仍沒有資料，可能有些地方出了問題︰

![SELECT INTO output1 資料表沒有資料](./media/stream-analytics-select-into/stream-analytics-select-into-out-table-1.png)

根據取樣 hello 資料，您可以是幾乎可以肯定 hello 問題是以 hello 聯結的第二個。 您可以下載 hello blob hello 參考資料，並請參閱：

![SELECT INTO 參考資料表](./media/stream-analytics-select-into/stream-analytics-select-into-ref-table-1.png)

如您所見，hello 這個參考資料中的 hello GUID 格式會與不同的 [從] 資料行中 temp2 hello hello 格式。 這就是為什麼 hello 資料未到達 output1 如預期般。

您可以修正 hello 資料格式、 將它上傳 tooreference blob，並再試一次：

![SELECT INTO 暫存資料表](./media/stream-analytics-select-into/stream-analytics-select-into-ref-table-2.png)

這次 hello hello 輸出中的資料是格式化，並且如預期般填入。

![SELECT INTO 的最終資料表](./media/stream-analytics-select-into/stream-analytics-select-into-final-table.png)


## <a name="get-help"></a>取得說明

如需進一步的協助，請參閱我們的 [Azure Stream Analytics 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)。

## <a name="next-steps"></a>後續步驟

* [簡介 tooAzure 資料流分析](stream-analytics-introduction.md)
* [開始使用 Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [調整 Azure Stream Analytics 工作](stream-analytics-scale-jobs.md)
* [Azure Stream Analytics 查詢語言參考](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure 串流分析管理 REST API 參考](https://msdn.microsoft.com/library/azure/dn835031.aspx)

