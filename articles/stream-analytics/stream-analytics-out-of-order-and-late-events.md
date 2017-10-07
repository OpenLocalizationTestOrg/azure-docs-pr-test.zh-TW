---
title: "aaaHandling 事件順序和使用 Azure Stream Analytics lateness |Microsoft 文件"
description: "深入了解串流分析如何處理資料串流中順序錯亂或延遲的事件。"
keywords: "順序錯亂、延遲、事件"
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
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: 87c028662fbafbf4f72f57f215d017f65bb649f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-stream-analytics-event-order-handling"></a>Azure 串流分析事件的順序處理

在暫存資料流的事件，每個事件會記錄與 hello 時間收到 hello 事件。 某些條件可能會導致 toooccasionally 接收的事件資料流某些事件比用其傳送順序不同。 簡單的 TCP 重新傳輸，或甚至 hello 傳送裝置和 hello 接收事件中心之間的時鐘誤差可能會導致此 toooccur。 「 對稱 」 事件也會加入 tooreceived 事件資料流，在事件抵達的 hello 缺乏 tooadvance hello 時間。 例如「3 分鐘後沒出現登入作業請通知我」的情況就需要標點符號事件。

未依照順序的輸入串流為以下兩者其中之一：
* 已分類 (並因此**延遲**)。
* 調整 hello 系統中，根據 tooa 使用者指定的原則。


## <a name="lateness-tolerance"></a>延遲容許
串流分析可容許這類情況。 串流分析可處理「順序錯亂」和「延遲」事件。 它會處理這些事件中 hello 下列方法：

* 事件不按順序抵達，但 hello 內設定容限是**時間戳記來重新排列**。
* 抵達時間比容許範圍還晚的事件會遭到**捨棄或調整**。
    * **調整**： 調整的 tooappear toohave 抵達 hello 最新接受的時間。
    * **捨棄**︰放棄。

![串流分析事件處理](media/stream-analytics-event-handling/stream-analytics-event-handling.png)

## <a name="reduce-hello-number-of-out-of-order-events"></a>減少 hello 次序不對的事件數目

由於串流分析在處理傳入事件時會套用暫存轉換 (例如視窗型彙總或暫存聯結)，因此串流分析會以時間戳記的順序將傳入事件排序。

當由的 hello"timestamp"關鍵字是**不**hello Azure 事件中心事件加入佇列的時間會使用預設。 事件中心可保證單一性 hello hello 事件中樞的每個磁碟分割上的時間戳記。 也保證所有分割區的事件將會依時間戳記順序進行合併。 這兩個事件中樞保證可確保沒有順序錯亂的事件發生。

有時候，很重要您 toouse hello 寄件者的時間戳記。 在此情況下，從 hello 事件裝載的時間戳記會選擇使用 「 依時間戳記。 」 以下案列會介紹一個或多個事件順序錯誤的情況：

* 事件產生器有時鐘誤差。 此狀況常見於不同電腦的產生器，因為電腦的時鐘不同。
* 沒有從 hello 來源 hello 事件 toohello 目的地事件中心的網路延遲。
* 事件中樞分割區之間存在時鐘誤差。 串流分析第一次從所有事件中樞分割區排序事件時是以事件加入佇列的時間排序。 然後，它會檢查 hello 順序的事件資料流。

Hello 組態索引標籤上，您會看到下列預設值的 hello:

![串流分析順序錯亂處理](media/stream-analytics-event-handling/stream-analytics-out-of-order-handling.png)

如果您使用 0 秒做 hello 次序不對容錯時間，您正在判斷提示，所有事件都的順序所有 hello 時間。 指定 hello 三個來源的順序的事件，也不太可能，這是 true。 

Stream Analytics toocorrect 事件 misorder tooallow，您可以指定非零次序不對容錯時間。 資料流分析緩衝區事件向上 toothat 視窗，然後再重新排列它們使用 hello 您選擇的時間戳記。 然後，它會套用 hello 暫時轉換。 您可以從 3 秒 視窗中，開始，並微調 hello 值 tooreduce hello 事件數目的時間調整。 

Hello 緩衝的副作用是，hello 輸出**延遲 hello 相同的時間量**。 您可以微調 hello 值 tooreduce hello 次序不對的事件數目，並保留 hello 作業延遲更低。

## <a name="get-help"></a>取得說明
如需其他協助，請參閱我們的 [Azure 串流分析論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)。

## <a name="next-steps"></a>後續步驟
* [簡介 tooStream 分析](stream-analytics-introduction.md)
* [開始使用串流分析](stream-analytics-real-time-fraud-detection.md)
* [調整串流分析作業](stream-analytics-scale-jobs.md)
* [串流分析查詢語言參考](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [串流分析管理 REST API 參考](https://msdn.microsoft.com/library/azure/dn835031.aspx)