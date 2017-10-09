---
title: "aaaIntroduction tooStream 分析視窗函數 |Microsoft 文件"
description: "深入了解在 Stream Analytics 輪轉、 跳動 (滑動） hello 三個視窗函數。"
keywords: "輪轉時間範圍、滑動時間範圍、跳動時間範圍"
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 0d8d8717-5d23-43f0-b475-af078ab4627d
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 7fc36eb9afb2b28e2791d925d26923145eb38074
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toostream-analytics-window-functions"></a>簡介 tooStream Analytics 視窗函式
在許多即時資料流案例來說，是只在暫時的視窗中所包含的 hello 資料上的必要 tooperform 作業。 一項重要功能的 Azure Stream Analytics 將 hello 指針移動上撰寫複雜的資料流處理工作的開發人員生產力視窗化函式的原生支援。 資料流分析可讓開發人員 toouse [**輪轉**](https://msdn.microsoft.com/library/dn835055.aspx)， [ **Hopping** ](https://msdn.microsoft.com/library/dn835041.aspx)和[**滑動**](https://msdn.microsoft.com/library/dn835051.aspx) windows tooperform 時態上的作業資料流處理資料。 值得注意的是，所有[視窗](https://msdn.microsoft.com/library/dn835019.aspx)作業輸出結果在 hello**結束**hello 視窗。 hello hello 視窗輸出將會根據使用 hello 彙總函式的單一事件。 所有的視窗函數定義固定長度與 hello 事件將會有 hello hello hello 視窗結束時間戳記。 它最後會應用於所有的視窗函數的重要 toonote [ **GROUP BY** ](https://msdn.microsoft.com/library/dn835023.aspx)子句。

![串流分析時間範圍函式概念](media/stream-analytics-window-functions/stream-analytics-window-functions-conceptual.png)

## <a name="tumbling-window"></a>輪轉時間範圍
輪轉視窗函數會使用的 toosegment 到不同的時間區段的資料流，並執行它們，針對在函式，例如以下 hello 範例。 輪轉視窗的 hello 重要的區別因素是，它們重複，沒有重疊，而且事件不能隸屬於一個輪轉視窗 toomore。

![串流分析時間範圍函式輪轉簡介](media/stream-analytics-window-functions/stream-analytics-window-functions-tumbling-intro.png)

## <a name="hopping-window"></a>跳動時間範圍
跳動時間範圍函式會在一段固定的時間向前跳動。 它可能是簡單 toothink 它們做為可以重疊的輪轉視窗，所以事件可以隸屬 toomore 比 Hopping 視窗結果集。 toomake Hopping 視窗相同 hello 做為另一個只會指定的輪轉視窗 hello 躍點大小 toobe 相同 hello 與 hello 視窗大小。 

![串流分析時間範圍函式跳動簡介](media/stream-analytics-window-functions/stream-analytics-window-functions-hopping-intro.png)

## <a name="sliding-window"></a>滑動時間範圍
不同於輪轉或跳動時間範圍，滑動時間範圍函式**只**會在事件發生時產生輸出。 每個視窗會有一個以上的事件和 hello 視窗持續推進由 € (epsilon)。 跳動視窗，類似事件可隸屬 toomore 超過一個滑動視窗。

![串流分析時間範圍函式滑動簡介](media/stream-analytics-window-functions/stream-analytics-window-functions-sliding-intro.png)

## <a name="getting-help-with-window-functions"></a>取得使用時間範圍函式的說明
如需進一步的協助，請參閱我們的 [Azure Stream Analytics 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>後續步驟
* [簡介 tooAzure 資料流分析](stream-analytics-introduction.md)
* [開始使用 Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [調整 Azure Stream Analytics 工作](stream-analytics-scale-jobs.md)
* [Azure Stream Analytics 查詢語言參考](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure 串流分析管理 REST API 參考](https://msdn.microsoft.com/library/azure/dn835031.aspx)

