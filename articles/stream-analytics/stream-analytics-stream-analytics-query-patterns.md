---
title: "在 Stream Analytics 中常見的使用模式的 aaaQuery 範例 |Microsoft 文件"
description: "常見的 Azure 串流分析查詢模式"
keywords: "查詢範例"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jenniehubbard
editor: cgronlun
ms.assetid: 6b9a7d00-fbcc-42f6-9cbb-8bbf0bbd3d0e
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/08/2017
ms.author: jenniehubbard
ms.openlocfilehash: c8f7a8ac661eaf0281f4140b02c42141b73040fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="query-examples-for-common-stream-analytics-usage-patterns"></a>一般串流分析使用模式的查詢範例
## <a name="introduction"></a>簡介
Azure 串流分析的查詢會以類似 SQL 的查詢語言表達。 這些查詢會記載於 hello [Stream Analytics 查詢語言參考](https://msdn.microsoft.com/library/azure/dn834998.aspx)指南。 此文件大綱解決方案 tooseveral 常見的查詢模式，根據的真實世界案例。 進行中工作，並繼續 toobe 以新的模式，持續地更新。

## <a name="query-example-convert-data-types"></a>查詢範例：轉換資料類型
**描述**: hello 輸入資料流定義 hello 類型的屬性。
比方說，hello 汽車權數是 hello 輸入資料流為字串，並且需要 toobe 太轉換**INT** tooperform**總和**它。

**輸入**：

| Make | 時間 | Weight |
| --- | --- | --- |
| Honda |2015-01-01T00:00:01.0000000Z |"1000" |
| Honda |2015-01-01T00:00:02.0000000Z |"2000" |

**輸出**：

| Make | Weight |
| --- | --- |
| Honda |3000 |

**解決方案**：

    SELECT
        Make,
        SUM(CAST(Weight AS BIGINT)) AS Weight
    FROM
        Input TIMESTAMP BY Time
    GROUP BY
        Make,
        TumblingWindow(second, 10)

**說明**： 使用**轉換**陳述式中 hello**加權**欄位 toospecify 其資料類型。 請參閱支援的資料類型中的 hello 清單[資料類型 (Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835065.aspx)。

## <a name="query-example-use-likenot-like-toodo-pattern-matching"></a>查詢範例： 使用類似/Not like toodo 模式比對
**描述**： 檢查 hello 事件的欄位值是否符合特定模式。
例如，檢查 hello 結果傳回授權盤子與起始或結束與 9。

**輸入**：

| Make | LicensePlate | 時間 |
| --- | --- | --- |
| Honda |ABC-123 |2015-01-01T00:00:01.0000000Z |
| Toyota |AAA-999 |2015-01-01T00:00:02.0000000Z |
| Nissan |ABC-369 |2015-01-01T00:00:03.0000000Z |

**輸出**：

| Make | LicensePlate | 時間 |
| --- | --- | --- |
| Toyota |AAA-999 |2015-01-01T00:00:02.0000000Z |
| Nissan |ABC-369 |2015-01-01T00:00:03.0000000Z |

**解決方案**：

    SELECT
        *
    FROM
        Input TIMESTAMP BY Time
    WHERE
        LicensePlate LIKE 'A%9'

**說明**： 使用 hello**像**陳述式 toocheck hello **LicensePlate**欄位值。 開頭應該為 A，接著是長度為零或更多字元的字串，並以 9 結尾。 

## <a name="query-example-specify-logic-for-different-casesvalues-case-statements"></a>查詢範例：為不同的案例/值指定邏輯 (CASE 陳述式)
**描述**：根據特定準則，提供不同的欄位計算方式。
例如，提供與特殊案例 1 多少汽車的 hello 相同進行傳遞的字串描述。

**輸入**：

| Make | 時間 |
| --- | --- |
| Honda |2015-01-01T00:00:01.0000000Z |
| Toyota |2015-01-01T00:00:02.0000000Z |
| Toyota |2015-01-01T00:00:03.0000000Z |

**輸出**：

| CarsPassed | 時間 |
| --- | --- | --- |
| 1 Honda |2015-01-01T00:00:10.0000000Z |
| 2 Toyotas |2015-01-01T00:00:10.0000000Z |

**解決方案**：

    SELECT
        CASE
            WHEN COUNT(*) = 1 THEN CONCAT('1 ', Make)
            ELSE CONCAT(CAST(COUNT(*) AS NVARCHAR(MAX)), ' ', Make, 's')
        END AS CarsPassed,
        System.TimeStamp AS Time
    FROM
        Input TIMESTAMP BY Time
    GROUP BY
        Make,
        TumblingWindow(second, 10)

**說明**: hello**案例**子句可讓我們 tooprovide 不同的計算，根據一些條件 （在此案例中的 hello 彙總視窗中的 hello 汽車 hello 計數）。

## <a name="query-example-send-data-toomultiple-outputs"></a>查詢範例： 傳送資料 toomultiple 輸出
**描述**： 傳送資料 toomultiple 輸出一項工作的目標。
例如，分析臨界值為基礎的警示資料和封存所有事件 tooblob 存放裝置。

**輸入**：

| Make | 時間 |
| --- | --- |
| Honda |2015-01-01T00:00:01.0000000Z |
| Honda |2015-01-01T00:00:02.0000000Z |
| Toyota |2015-01-01T00:00:01.0000000Z |
| Toyota |2015-01-01T00:00:02.0000000Z |
| Toyota |2015-01-01T00:00:03.0000000Z |

**Output1**：

| Make | 時間 |
| --- | --- |
| Honda |2015-01-01T00:00:01.0000000Z |
| Honda |2015-01-01T00:00:02.0000000Z |
| Toyota |2015-01-01T00:00:01.0000000Z |
| Toyota |2015-01-01T00:00:02.0000000Z |
| Toyota |2015-01-01T00:00:03.0000000Z |

**Output2**：

| Make | 時間 | Count |
| --- | --- | --- |
| Toyota |2015-01-01T00:00:10.0000000Z |3 |

**解決方案**：

    SELECT
        *
    INTO
        ArchiveOutput
    FROM
        Input TIMESTAMP BY Time

    SELECT
        Make,
        System.TimeStamp AS Time,
        COUNT(*) AS [Count]
    INTO
        AlertOutput
    FROM
        Input TIMESTAMP BY Time
    GROUP BY
        Make,
        TumblingWindow(second, 10)
    HAVING
        [Count] >= 3

**說明**: hello **INTO**子句會告知串流分析會輸出 toowrite hello 資料 toofrom 的 hello 這個陳述式。
hello 第一個查詢是 hello 我們所收到的資料，我們名為 tooan 輸出傳遞**ArchiveOutput**。
hello 第二個查詢執行一些簡單的彙總並篩選，和它傳送嗨結果 tooa 下游警示系統。

請注意，您也可以重複使用的 hello 通用資料表運算式 (Cte) 的 hello 結果 (例如**WITH**陳述式) 中多個輸出的陳述式。 此選項已 hello 開啟較少的讀取器 toohello 輸入的來源的好處。
例如： 

    WITH AllRedCars AS (
        SELECT
            *
        FROM
            Input TIMESTAMP BY Time
        WHERE
            Color = 'red'
    )
    SELECT * INTO HondaOutput FROM AllRedCars WHERE Make = 'Honda'
    SELECT * INTO ToyotaOutput FROM AllRedCars WHERE Make = 'Toyota'

## <a name="query-example-count-unique-values"></a>查詢範例：計算唯一值
**描述**: hello 計數的 hello 的時間間隔內的資料流中出現的唯一欄位值。
例如，多少唯一可讓您的傳遞 2 第二個視窗中的 hello 收費亭的車輛嗎？

**輸入**：

| Make | 時間 |
| --- | --- |
| Honda |2015-01-01T00:00:01.0000000Z |
| Honda |2015-01-01T00:00:02.0000000Z |
| Toyota |2015-01-01T00:00:01.0000000Z |
| Toyota |2015-01-01T00:00:02.0000000Z |
| Toyota |2015-01-01T00:00:03.0000000Z |

**輸出：**

| Count | 時間 |
| --- | --- |
| 2 |2015-01-01T00:00:02.000Z |
| 1 |2015-01-01T00:00:04.000Z |

**解決方案：**

````
SELECT
     COUNT(DISTINCT Make) AS CountMake,
     System.TIMESTAMP AS TIME
FROM Input TIMESTAMP BY TIME
GROUP BY 
     TumblingWindow(second, 2)
````


**說明：**
**計數 （相異請）**傳回 hello hello 中相異值數目**進行**的時間間隔內的資料行。

## <a name="query-example-determine-if-a-value-has-changed"></a>查詢範例：判斷值是否已變更
**描述**： 查看先前的值 toodetermine 是否不同於 hello 目前值。
比方說，位於相同讓 hello 目前汽車 hello 付費道路 hello hello 先前汽車嗎？

**輸入**：

| Make | 時間 |
| --- | --- |
| Honda |2015-01-01T00:00:01.0000000Z |
| Toyota |2015-01-01T00:00:02.0000000Z |

**輸出**：

| Make | 時間 |
| --- | --- |
| Toyota |2015-01-01T00:00:02.0000000Z |

**解決方案**：

    SELECT
        Make,
        Time
    FROM
        Input TIMESTAMP BY Time
    WHERE
        LAG(Make, 1) OVER (LIMIT DURATION(minute, 1)) <> Make

**說明**： 使用**延隔**toopeek hello 到輸入資料流的回一個事件，並取得 hello**進行**值。 然後比較 toohello**進行**值 hello 目前事件和輸出 hello 事件上，如果不相同。

## <a name="query-example-find-hello-first-event-in-a-window"></a>查詢範例： 尋找 hello 中的第一個事件視窗
**描述**： 每隔 10 分鐘的間隔中尋找 hello 第一個汽車。

**輸入**：

| LicensePlate | Make | 時間 |
| --- | --- | --- |
| DXE 5291 |Honda |2015-07-27T00:00:05.0000000Z |
| YZK 5704 |Ford |2015-07-27T00:02:17.0000000Z |
| RMV 8282 |Honda |2015-07-27T00:05:01.0000000Z |
| YHN 6970 |Toyota |2015-07-27T00:06:00.0000000Z |
| VFE 1616 |Toyota |2015-07-27T00:09:31.0000000Z |
| QYF 9358 |Honda |2015-07-27T00:12:02.0000000Z |
| MDR 6128 |BMW |2015-07-27T00:13:45.0000000Z |

**輸出**：

| LicensePlate | Make | 時間 |
| --- | --- | --- |
| DXE 5291 |Honda |2015-07-27T00:00:05.0000000Z |
| QYF 9358 |Honda |2015-07-27T00:12:02.0000000Z |

**解決方案**：

    SELECT 
        LicensePlate,
        Make,
        Time
    FROM 
        Input TIMESTAMP BY Time
    WHERE 
        IsFirst(minute, 10) = 1

現在我們變更 hello 問題，並尋找 hello 第一個汽車的特定把每隔 10 分鐘的間隔中。

| LicensePlate | Make | 時間 |
| --- | --- | --- |
| DXE 5291 |Honda |2015-07-27T00:00:05.0000000Z |
| YZK 5704 |Ford |2015-07-27T00:02:17.0000000Z |
| YHN 6970 |Toyota |2015-07-27T00:06:00.0000000Z |
| QYF 9358 |Honda |2015-07-27T00:12:02.0000000Z |
| MDR 6128 |BMW |2015-07-27T00:13:45.0000000Z |

**解決方案**：

    SELECT 
        LicensePlate,
        Make,
        Time
    FROM 
        Input TIMESTAMP BY Time
    WHERE 
        IsFirst(minute, 10) OVER (PARTITION BY Make) = 1

## <a name="query-example-find-hello-last-event-in-a-window"></a>查詢範例： 尋找 hello 中的最後一個事件視窗
**描述**： 每隔 10 分鐘的間隔中尋找 hello 最後一個汽車。

**輸入**：

| LicensePlate | Make | 時間 |
| --- | --- | --- |
| DXE 5291 |Honda |2015-07-27T00:00:05.0000000Z |
| YZK 5704 |Ford |2015-07-27T00:02:17.0000000Z |
| RMV 8282 |Honda |2015-07-27T00:05:01.0000000Z |
| YHN 6970 |Toyota |2015-07-27T00:06:00.0000000Z |
| VFE 1616 |Toyota |2015-07-27T00:09:31.0000000Z |
| QYF 9358 |Honda |2015-07-27T00:12:02.0000000Z |
| MDR 6128 |BMW |2015-07-27T00:13:45.0000000Z |

**輸出**：

| LicensePlate | Make | 時間 |
| --- | --- | --- |
| VFE 1616 |Toyota |2015-07-27T00:09:31.0000000Z |
| MDR 6128 |BMW |2015-07-27T00:13:45.0000000Z |

**解決方案**：

    WITH LastInWindow AS
    (
        SELECT 
            MAX(Time) AS LastEventTime
        FROM 
            Input TIMESTAMP BY Time
        GROUP BY 
            TumblingWindow(minute, 10)
    )
    SELECT 
        Input.LicensePlate,
        Input.Make,
        Input.Time
    FROM
        Input TIMESTAMP BY Time 
        INNER JOIN LastInWindow
        ON DATEDIFF(minute, Input, LastInWindow) BETWEEN 0 AND 10
        AND Input.Time = LastInWindow.LastEventTime

**說明**: hello 查詢中有兩個步驟。 hello 第一次一個尋找 hello 時間戳記最新 windows 10 分鐘中。 第二個步驟聯結 hello hello hello 與 hello 原始資料流 toofind hello 符合事件 hello 最後一個時間戳記之各個視窗中的第一個查詢的結果。 

## <a name="query-example-detect-hello-absence-of-events"></a>查詢範例： 偵測 hello 沒有事件
**描述**：檢查串流中是否沒有和特定準則相符的值。
比方說，從相同進行的 hello 2 連續汽車輸入 hello 付費道路 hello 內最後 90 秒嗎？

**輸入**：

| Make | LicensePlate | 時間 |
| --- | --- | --- |
| Honda |ABC-123 |2015-01-01T00:00:01.0000000Z |
| Honda |AAA-999 |2015-01-01T00:00:02.0000000Z |
| Toyota |DEF-987 |2015-01-01T00:00:03.0000000Z |
| Honda |GHI-345 |2015-01-01T00:00:04.0000000Z |

**輸出**：

| Make | 時間 | CurrentCarLicensePlate | FirstCarLicensePlate | FirstCarTime |
| --- | --- | --- | --- | --- |
| Honda |2015-01-01T00:00:02.0000000Z |AAA-999 |ABC-123 |2015-01-01T00:00:01.0000000Z |

**解決方案**：

    SELECT
        Make,
        Time,
        LicensePlate AS CurrentCarLicensePlate,
        LAG(LicensePlate, 1) OVER (LIMIT DURATION(second, 90)) AS FirstCarLicensePlate,
        LAG(Time, 1) OVER (LIMIT DURATION(second, 90)) AS FirstCarTime
    FROM
        Input TIMESTAMP BY Time
    WHERE
        LAG(Make, 1) OVER (LIMIT DURATION(second, 90)) = Make

**說明**： 使用**延隔**toopeek hello 到輸入資料流的回一個事件，並取得 hello**進行**值。 它比較 toohello**進行**hello 目前事件，然後輸出 hello 事件如果它們是 hello 相同的值。 您也可以使用**延隔**tooget hello 先前汽車相關的資料。

## <a name="query-example-detect-hello-duration-between-events"></a>查詢範例： 偵測 hello 事件之間的持續期間
**描述**： 尋找 hello 的給定事件的持續時間。 例如，給定網站的點選流，判斷 hello 時間花在功能上。

**輸入**：  

| User | 功能 | Event | 時間 |
| --- | --- | --- | --- |
| user@location.com |RightMenu |Start |2015-01-01T00:00:01.0000000Z |
| user@location.com |RightMenu |End |2015-01-01T00:00:08.0000000Z |

**輸出**：  

| User | 功能 | Duration |
| --- | --- | --- |
| user@location.com |RightMenu |7 |

**解決方案**：

````
    SELECT
        [user], feature, DATEDIFF(second, LAST(Time) OVER (PARTITION BY [user], feature LIMIT DURATION(hour, 1) WHEN Event = 'start'), Time) as duration
    FROM input TIMESTAMP BY Time
    WHERE
        Event = 'end'
````

**說明**： 使用 hello**最後**函式 tooretrieve hello**時間**值 hello 事件類型時**啟動**。 hello**最後**函式使用**PARTITION BY [使用者]** hello 結果的 tooindicate 計算每個唯一的使用者。 hello 查詢具有 1 小時 hello 之間的時間差異的最大閾值**啟動**和**停止**事件，但是您視需要**(限制 DURATION(hour, 1)**。

## <a name="query-example-detect-hello-duration-of-a-condition"></a>查詢範例： 偵測條件的 hello 持續時間
**描述**：找出某個情況的持續時間。
例如，假設有個錯誤導致所有車輛的重量不正確 (超過 20,000 磅)， 我們想要 hello bug toocompute hello 持續的時間。

**輸入**：

| Make | 時間 | Weight |
| --- | --- | --- |
| Honda |2015-01-01T00:00:01.0000000Z |2000 |
| Toyota |2015-01-01T00:00:02.0000000Z |25000 |
| Honda |2015-01-01T00:00:03.0000000Z |26000 |
| Toyota |2015-01-01T00:00:04.0000000Z |25000 |
| Honda |2015-01-01T00:00:05.0000000Z |26000 |
| Toyota |2015-01-01T00:00:06.0000000Z |25000 |
| Honda |2015-01-01T00:00:07.0000000Z |26000 |
| Toyota |2015-01-01T00:00:08.0000000Z |2000 |

**輸出**：

| StartFault | EndFault |
| --- | --- |
| 2015-01-01T00:00:02.000Z |2015-01-01T00:00:07.000Z |

**解決方案**：

````
    WITH SelectPreviousEvent AS
    (
    SELECT
    *,
        LAG([time]) OVER (LIMIT DURATION(hour, 24)) as previousTime,
        LAG([weight]) OVER (LIMIT DURATION(hour, 24)) as previousWeight
    FROM input TIMESTAMP BY [time]
    )

    SELECT 
        LAG(time) OVER (LIMIT DURATION(hour, 24) WHEN previousWeight < 20000 ) [StartFault],
        previousTime [EndFault]
    FROM SelectPreviousEvent
    WHERE
        [weight] < 20000
        AND previousWeight > 20000
````

**說明**： 使用**延隔**24 小時的 tooview hello 輸入資料流並尋找執行個體**StartFault**和**StopFault**合併的 hello加權 < 20000。

## <a name="query-example-fill-missing-values"></a>查詢範例：填入遺漏值
**描述**: hello 資料流有遺漏值的事件，會產生以固定間隔事件資料流。
例如，產生報告的事件每隔 5 秒，最常出現的 hello 資料點。

**輸入**：

| t | value |
| --- | --- |
| "2014-01-01T06:01:00" |1 |
| "2014-01-01T06:01:05" |2 |
| "2014-01-01T06:01:10" |3 |
| "2014-01-01T06:01:15" |4 |
| "2014-01-01T06:01:30" |5 |
| "2014-01-01T06:01:35" |6 |

**輸出 (前 10 個資料列)**：

| windowend | lastevent.t | lastevent.value |
| --- | --- | --- |
| 2014-01-01T14:01:00.000Z |2014-01-01T14:01:00.000Z |1 |
| 2014-01-01T14:01:05.000Z |2014-01-01T14:01:05.000Z |2 |
| 2014-01-01T14:01:10.000Z |2014-01-01T14:01:10.000Z |3 |
| 2014-01-01T14:01:15.000Z |2014-01-01T14:01:15.000Z |4 |
| 2014-01-01T14:01:20.000Z |2014-01-01T14:01:15.000Z |4 |
| 2014-01-01T14:01:25.000Z |2014-01-01T14:01:15.000Z |4 |
| 2014-01-01T14:01:30.000Z |2014-01-01T14:01:30.000Z |5 |
| 2014-01-01T14:01:35.000Z |2014-01-01T14:01:35.000Z |6 |
| 2014-01-01T14:01:40.000Z |2014-01-01T14:01:35.000Z |6 |
| 2014-01-01T14:01:45.000Z |2014-01-01T14:01:35.000Z |6 |

**解決方案**：

    SELECT
        System.Timestamp AS windowEnd,
        TopOne() OVER (ORDER BY t DESC) AS lastEvent
    FROM
        input TIMESTAMP BY t
    GROUP BY HOPPINGWINDOW(second, 300, 5)


**說明**： 此查詢會產生事件每隔 5 秒，並輸出 hello 先前接收的最後一個事件。 hello [Hopping 視窗](https://msdn.microsoft.com/library/dn835041.aspx "Hopping 視窗-Azure Stream Analytics")持續時間會決定多久後 hello 查詢會尋找 toofind hello 最新事件 （在此範例中的 300 秒）。

## <a name="get-help"></a>取得說明
如需進一步的協助，請參閱我們的 [Azure Stream Analytics 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)。

## <a name="next-steps"></a>後續步驟
* [簡介 tooAzure 資料流分析](stream-analytics-introduction.md)
* [開始使用 Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [調整 Azure Stream Analytics 工作](stream-analytics-scale-jobs.md)
* [Azure Stream Analytics 查詢語言參考](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure 串流分析管理 REST API 參考](https://msdn.microsoft.com/library/azure/dn835031.aspx)

