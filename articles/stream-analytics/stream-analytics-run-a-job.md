---
title: "資料流中資料流分析工作的 aaaHow toostart |Microsoft 文件"
description: "如何在 Azure 串流分析中執行串流工作 | 學習路徑區段。"
keywords: "串流工作"
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 9d46950f-2b69-49ce-a567-df558c5dd820
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 67aa14860c38cbd0535d0ec4f23729445d0185c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorun-a-streaming-job-in-azure-stream-analytics"></a>在 Azure Stream Analytics toorun 串流工作的方式
作業輸入，當查詢和輸出都已指定您可以啟動 hello 資料流分析工作。

toostart 您的工作：

1. 在 hello Azure 傳統入口網站，從 hello 作業儀表板中，按一下 **啟動**hello hello 頁底端。
   
   ![開始工作按鈕](./media/stream-analytics-run-a-job/1-stream-analytics-run-a-job.png)  
   
   在 hello Azure 入口網站，按一下 **啟動**在 hello 頁面頂端的工作。
   
   ![Azure 入口網站開始工作按鈕](./media/stream-analytics-run-a-job/4-stream-analytics-run-a-job.png)  
2. 指定**開始輸出**值 toodetermine 時此工作會開始產生輸出。 hello 先前尚未啟動的工作的預設值是**工作開始時間**，這表示 hello 作業會立即開始處理資料。 您也可以指定**自訂**hello 時間 （適用於使用歷程記錄資料） 的過去或未來 hello (toodelay 處理，直到未來的時間)。 情況下，作業已經先前啟動和停止，hello 選項**上次停止時間**隨附於從 hello 上次輸出順序 tooresume hello 作業，避免資料遺失。  
   
   ![啟動串流工作的時間](./media/stream-analytics-run-a-job/2-stream-analytics-run-a-job.png)  
   
   ![Azure 入口網站開始串流工作的時間](./media/stream-analytics-run-a-job/5-stream-analytics-run-a-job.png)  
3. 確認選擇。 hello 工作狀態會變更太*起始*和稍後也會跟著移動*執行*hello 工作啟動之後。 您可以監視 hello 進度的 hello**啟動**作業在 hello**通知中樞**:
   
   ![串流工作進度](./media/stream-analytics-run-a-job/3-stream-analytics-run-a-job.png)  
   
   ![Azure 入口網站串流工作進度](./media/stream-analytics-run-a-job/6-stream-analytics-run-a-job.png)  

## <a name="get-help"></a>取得說明
如需進一步的協助，請參閱我們的 [Azure Stream Analytics 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>後續步驟
* [簡介 tooAzure 資料流分析](stream-analytics-introduction.md)
* [開始使用 Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [調整 Azure Stream Analytics 工作](stream-analytics-scale-jobs.md)
* [Azure Stream Analytics 查詢語言參考](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure 串流分析管理 REST API 參考](https://msdn.microsoft.com/library/azure/dn835031.aspx)

