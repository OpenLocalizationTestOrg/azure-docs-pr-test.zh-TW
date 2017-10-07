---
title: "aaa Azure Stream Analytics 資料導向使用偵錯 hello 工作圖表 |Microsoft 文件"
description: "疑難排解使用 hello 工作圖表和度量的串流分析工作。"
keywords: 
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 05/01/2017
ms.author: jeffstok
ms.openlocfilehash: 1af884d485bebb06b034da01a13f7f8240516571
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="data-driven-debugging-by-using-hello-job-diagram"></a>資料驅動的偵錯使用 hello 工作圖表

hello 工作圖表上 hello**監視**hello Azure 入口網站中的刀鋒視窗可協助您以視覺化方式檢視您工作的管線。 圖表會顯示輸入、輸出和查詢步驟。 您可以針對每個步驟使用 hello 工作圖表 tooexamine hello 度量，toomore 迅速隔離 hello 問題來源，當您疑難排解問題。

## <a name="using-hello-job-diagram"></a>您可以使用 hello 工作圖表

在 hello Azure 入口網站中的資料流分析工作，而下**支援 + 疑難排解**，選取**工作圖表**:

![作業圖表與計量 - 位置](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-1.png)

在查詢編輯窗格中選取每個查詢步驟 toosee hello 對應的章節。 Hello 步驟的度量圖表會顯示在 hello 頁面的下方窗格中。

![作業圖表與計量 - 基本作業](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-2.png)

toosee hello 資料分割的 hello Azure 事件中樞輸入，選取**...** 操作功能表隨即出現。 您也可以看到 hello 輸入的合併。

![作業圖表與計量 - 展開分割區](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-3.png)

toosee hello 度量圖表只單一分割區，選取 hello 分割節點。 hello 度量資訊會顯示在 hello hello 頁面底部。

![作業圖表與計量 - 其他計量](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-4.png)

toosee hello 合併時，選取 hello 合併節點的度量圖表。 hello 下列圖表顯示任何事件已捨棄或調整。

![作業圖表與計量 - 格線](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-5.png)

hello 公制值和時間，點 toohello 圖表 toosee hello 詳細資料。

![作業圖表與計量 - 暫留](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-6.png)

## <a name="troubleshoot-by-using-metrics"></a>使用計量進行疑難排解

hello **QueryLastProcessedTime**公制表示特定的步驟時收到的資料。 藉由查看 hello 拓撲，您可以向後從工作 hello 輸出處理器 toosee 哪些步驟並未收到的資料。 如果步驟沒有取得資料，請移 toohello 它之前的查詢步驟。 檢查是否 hello 上述查詢步驟都有時間視窗中，而且如果它有充裕的時間 toooutput 資料。 （請注意，時間視窗包括 貼齊的 toohello 小時。）
 
如果 hello 上述的查詢步驟輸入的處理器，請使用下列目標的問題 hello 輸入的度量 toohelp 回應 hello。 這可協助您判斷作業是否正在從輸入來源取得資料。 如果已分割 hello 查詢，檢查每個資料分割。
 
### <a name="how-much-data-is-being-read"></a>已讀取多少資料？

*   **InputEventsSourcesTotal**是 hello 數目讀取資料單元。 例如，hello blob 的數目。
*   **InputEventsTotal**是 hello 讀取的事件數目。 此度量適用於每個資料分割。
*   **InputEventsInBytesTotal**是 hello 讀取的位元組數目。
*   **InputEventsLastArrivalTime** 會更新每個收到事件的加入佇列時間。
 
### <a name="is-time-moving-forward-if-actual-events-are-read-punctuation-might-not-be-issued"></a>時間是否正在前進？ 若實際事件已讀取，則可能無需加上標點符號。

*   **InputEventsLastPunctuationTime**表示當標點符號已發出 tookeep 時間移動向前復原。 若未加上標點符號，可能使資料流程遭到封鎖。
 
### <a name="are-there-any-errors-in-hello-input"></a>Hello 輸入中是否有任何錯誤？

*   **InputEventsEventDataNullTotal** 是具有 Null 資料的事件計數。
*   **InputEventsSerializerErrorsTotal** 是無法正確還原序列化的事件計數。
*   **InputEventsDegradedTotal** 是有其他還原序列化以外問題的事件計數。
 
### <a name="are-events-being-dropped-or-adjusted"></a>事件遭到捨棄或調整？

*   **InputEventsEarlyTotal**是 hello 具有應用程式之前的時間戳記 hello 高水位線的事件數目。
*   **InputEventsLateTotal**是 hello hello 高水位線之後，擁有應用程式時間戳記的事件數目。
*   **InputEventsDroppedBeforeApplicationStartTimeTotal**是 hello 的事件數 hello 工作開始時間之前卸除。
 
### <a name="are-we-falling-behind-in-reading-data"></a>讀取資料的速度太慢了嗎？

*   **InputEventsSourcesBackloggedTotal**告訴您需要更多的訊息數量的 toobe 事件中樞與 Azure IoT 中樞的輸入中讀取。


## <a name="get-help"></a>取得說明
如需其他協助，請參閱我們的 [Azure 串流分析論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)。

## <a name="next-steps"></a>後續步驟
* [簡介 tooStream 分析](stream-analytics-introduction.md)
* [開始使用串流分析](stream-analytics-real-time-fraud-detection.md)
* [調整串流分析作業](stream-analytics-scale-jobs.md)
* [串流分析查詢語言參考](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [串流分析管理 REST API 參考](https://msdn.microsoft.com/library/azure/dn835031.aspx)
