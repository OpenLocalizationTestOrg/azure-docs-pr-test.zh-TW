---
title: "資料流分析作業的監視 aaaUnderstanding |Microsoft 文件"
description: "了解串流分析工作監視"
keywords: "查詢監視"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 5f5cc00f-4a7b-491e-89e1-dbafea46d399
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 36819025c7b2ddbf4b9694522f1b4820407ca5f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="understand-stream-analytics-job-monitoring-and-how-toomonitor-queries"></a>了解資料流分析作業的監視和如何 toomonitor 查詢

## <a name="introduction-hello-monitor-page"></a>簡介： hello 監視頁面
hello 兩者介面，可以使用的 toomonitor 並疑難排解查詢和作業的效能關鍵效能標準的 Azure 入口網站。 toosee 這些度量，瀏覽 toohello 資料流分析工作，您有興趣查看的度量，檢視 hello**監視**hello 概觀 頁面上的一節。  

![監視連結](./media/stream-analytics-monitoring/02-stream-analytics-monitoring-block.png)

hello 視窗會出現如下所示：

![監視工作儀表板](./media/stream-analytics-monitoring/01-stream-analytics-monitoring.png)  

## <a name="metrics-available-for-stream-analytics"></a>可供串流分析使用的度量
| 度量                 | 定義                               |
| ---------------------- | ---------------------------------------- |
| SU % 使用率       | hello hello 使用量串流處理單元指派 tooa 作業 hello hello 工作的 [調整] 索引標籤中。 若此指標達到 80% 以上，則代表事件處理作業極有可能延遲或暫停。 |
| 輸入事件           | 收到 hello 資料流分析作業中的事件數目的資料量。 這可以是使用的 toovalidate 事件會被傳送 toohello 輸入的來源。 |
| 輸出事件          | 傳送 hello 資料流分析作業 toohello 輸出目標中的事件數目的資料量。 |
| 順序錯亂事件    | 從卸除或調整時間戳記，根據 hello 事件排序原則的順序接收的事件數目。 這可能會影響 hello 設定 hello 次序不對的容錯時間設定。 |
| 資料轉換錯誤 | 串流分析工作所造成的錯誤訊息數目。 |
| 執行階段錯誤         | hello 的資料流分析作業執行時，就可能發生的錯誤總數。 |
| 延遲輸入事件      | 這是已卸除的 hello 來源或依時間戳記晚抵達的事件數目已經被自動調整，hello 事件順序的原則設定的設定。 hello 晚抵達容錯時間為基礎。 |
| 函式要求      | 呼叫 toohello Azure Machine Learning 函式 （如果有的話） 的數目。 |
| 失敗的函式要求 | 失敗的 Azure Machine Learning 函式呼叫次數 (如果有的話)。 |
| 函式事件        | （如果有的話） 傳送 toohello Azure Machine Learning 函式的事件數目。 |
| 輸入事件位元組      | 收到 hello 資料流分析工作，以位元組為單位的資料量。 這可以是使用的 toovalidate 事件會被傳送 toohello 輸入的來源。 |


## <a name="customizing-monitoring-in-hello-azure-portal"></a>在 hello Azure 入口網站中自訂監視
您可以調整圖表所示，度量 hello 類型和時間 hello 編輯圖表設定中的範圍。 如需詳細資訊，請參閱[如何 tooCustomize 監視](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md)。

  ![查詢監視時間圖](./media/stream-analytics-monitoring/08-stream-analytics-monitoring.png)  


## <a name="get-help"></a>取得說明
如需進一步的協助，請參閱我們的 [Azure Stream Analytics 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>後續步驟
* [簡介 tooAzure 資料流分析](stream-analytics-introduction.md)
* [開始使用 Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [調整 Azure Stream Analytics 工作](stream-analytics-scale-jobs.md)
* [Azure Stream Analytics 查詢語言參考](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure 串流分析管理 REST API 參考](https://msdn.microsoft.com/library/azure/dn835031.aspx)

