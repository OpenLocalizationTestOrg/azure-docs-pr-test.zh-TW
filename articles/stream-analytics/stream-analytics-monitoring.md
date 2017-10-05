---
title: "了解串流分析工作監視 | Microsoft Docs"
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
ms.openlocfilehash: 13d96807a5591ec88deda19ea73cfedc07078433
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="understand-stream-analytics-job-monitoring-and-how-to-monitor-queries"></a>了解串流分析工作監視功能，以及如何監視查詢

## <a name="introduction-the-monitor-page"></a>簡介：監視頁面
Azure 入口網站會顯示關鍵效能計量，可供您用來監視查詢和工作效能並進行疑難排解。 若要查看這些計量，請瀏覽至您有興趣查看計量的「串流分析」工作，然後檢視 [概觀] 頁面上的 [監視] 區段。  

![監視連結](./media/stream-analytics-monitoring/02-stream-analytics-monitoring-block.png)

視窗將會出現，如下所示：

![監視工作儀表板](./media/stream-analytics-monitoring/01-stream-analytics-monitoring.png)  

## <a name="metrics-available-for-stream-analytics"></a>可供串流分析使用的度量
| 度量                 | 定義                               |
| ---------------------- | ---------------------------------------- |
| SU % 使用率       | 從工作的 [調整] 索引標籤指派給工作的串流處理單元使用率。 若此指標達到 80% 以上，則代表事件處理作業極有可能延遲或暫停。 |
| 輸入事件           | 「串流分析」工作所接收到的資料量 (以事件數為單位)。 這可以用來驗證傳送到輸入來源的事件。 |
| 輸出事件          | 「串流分析」工作所傳送的資料量 (以事件數為單位)。 |
| 順序錯亂事件    | 所收到順序錯亂的事件數目，這些事件會根據事件順序原則，予以捨棄或指定調整後的時間戳記。 順序錯亂容錯視窗設定的組態可能會造成影響。 |
| 資料轉換錯誤 | 串流分析工作所造成的錯誤訊息數目。 |
| 執行階段錯誤         | 在執行「串流分析」工作期間發生的錯誤總數。 |
| 延遲輸入事件      | 從來源延遲抵達的事件數目，這些事件已根據延遲抵達容錯視窗設定的事件順序原則組態卸除或調整其時間戳記。 |
| 函式要求      | 對 Azure Machine Learning 函式發出的呼叫次數 (如果有的話)。 |
| 失敗的函式要求 | 失敗的 Azure Machine Learning 函式呼叫次數 (如果有的話)。 |
| 函式事件        | 傳送給 Azure Machine Learning 函式的事件數目 (如果有的話)。 |
| 輸入事件位元組      | 「串流分析」工作所接收到的資料量 (以位元組為單位)。 這可以用來驗證傳送到輸入來源的事件。 |


## <a name="customizing-monitoring-in-the-azure-portal"></a>在 Azure 入口網站中自訂監視
您可以在 [編輯圖表] 設定中調整圖表類型、顯示的度量和時間範圍。 如需詳細資料，請參閱[如何自訂監視](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md)。

  ![查詢監視時間圖](./media/stream-analytics-monitoring/08-stream-analytics-monitoring.png)  


## <a name="get-help"></a>取得說明
如需進一步的協助，請參閱我們的 [Azure Stream Analytics 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>後續步驟
* [Azure Stream Analytics 介紹](stream-analytics-introduction.md)
* [開始使用 Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [調整 Azure Stream Analytics 工作](stream-analytics-scale-jobs.md)
* [Azure Stream Analytics 查詢語言參考](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure 串流分析管理 REST API 參考](https://msdn.microsoft.com/library/azure/dn835031.aspx)

