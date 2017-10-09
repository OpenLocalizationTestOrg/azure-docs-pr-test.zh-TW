---
title: "使用事件中樞接收者 aaaDebug Azure Stream Analytics |Microsoft 文件"
description: "查詢最佳做法以配置串流分析作業中的事件中樞取用者群組。"
keywords: "事件中樞限制、取用者群組"
services: stream-analytics
documentationcenter: 
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
ms.openlocfilehash: 89821e6273151de43b5e42d907e547c939e24824
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="debug-azure-stream-analytics-with-event-hub-receivers"></a>針對 Azure 串流分析與事件中樞接收器進行偵錯

Azure Stream Analytics tooingest 或輸出資料從作業中，您可以使用 Azure 事件中心。 使用事件中心的最佳作法是 toouse 多個取用者群組、 tooensure 作業延展性。 其中一個原因是特定的輸入的 hello Stream Analytics 工作中的讀取器的 hello 數目會影響單一取用者群組中的讀取器的 hello 數目。 hello 精確接收者數目根據 hello 向外延展拓撲邏輯的內部實作詳細資料。 hello 接收者數目不會從外部公開。 在 hello 工作開始時間，或是在升級作業期間，可以變更 hello 讀取器數目。

> [!NOTE]
> 當作業在升級期間，變更 hello 讀取器數目時，暫時性的警告會寫入 tooaudit 記錄檔。 串流分析作業會從這些暫時性問題中自動復原。

## <a name="number-of-readers-per-partition-exceeds-event-hubs-limit-of-five"></a>讀取器數量 (每個分割區) 超過事件中樞上限 (5 個)

案例中的 hello 的每個資料分割的讀取器數目超過五個 hello 事件中心限制 hello 如下：

* 多個 SELECT 陳述式： 如果您使用多個 SELECT 陳述式，請參閱太**相同**事件中樞輸入，每個 SELECT 陳述式會建立新的接收者 toobe。
* 等位： 當您使用等位時，很可能 toohave 參考 toohello 的多個輸入**相同**事件中樞取用者群組。
* 自我聯結： 當您使用自我聯結作業時，就可能 toorefer toohello**相同**事件中心多次。

## <a name="solution"></a>方案

hello 下列最佳作法可協助減少的案例中的 hello 的每個資料分割的讀取器數目超過五個 hello 事件中心限制。

### <a name="split-your-query-into-multiple-steps-by-using-a-with-clause"></a>使用 WITH 子句將查詢分割成多個步驟

hello WITH 子句指定可以在 hello 查詢的 FROM 子句中參考的暫存具名的結果集。 您可以定義 hello WITH 子句 hello 執行範圍中的單一 SELECT 陳述式。

例如，不要使用此查詢︰

```
SELECT foo 
INTO output1
FROM inputEventHub

SELECT bar
INTO output2
FROM inputEventHub 
…
```

使用此查詢︰

```
WITH input (
   SELECT * FROM inputEventHub
) as data

SELECT foo
INTO output1
FROM data

SELECT bar
INTO output2
FROM data
…
```

### <a name="ensure-that-inputs-bind-toodifferent-consumer-groups"></a>請確定輸入繫結 toodifferent 取用者群組

查詢中的三個或多個輸入是連接的 toohello 相同事件中心取用者群組中，建立個別取用者群組。 這需要額外的資料流分析輸入 hello 建立。


## <a name="get-help"></a>取得說明
如需其他協助，請參閱我們的 [Azure 串流分析論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)。

## <a name="next-steps"></a>後續步驟
* [簡介 tooStream 分析](stream-analytics-introduction.md)
* [開始使用串流分析](stream-analytics-real-time-fraud-detection.md)
* [調整串流分析作業](stream-analytics-scale-jobs.md)
* [串流分析查詢語言參考](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [串流分析管理 REST API 參考](https://msdn.microsoft.com/library/azure/dn835031.aspx)
