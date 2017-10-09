---
title: "aaaHow tooBuild 複雜的排程與使用 Azure 排程器的 進階循環"
description: "如何 tooBuild 複雜排程與進階與 Azure 排程器的循環"
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 5c124986-9f29-4cbc-ad5a-c667b37fbe5a
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/18/2016
ms.author: deli
ms.openlocfilehash: 02172791978b12be0ccb3078125d057b2efe8523
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toobuild-complex-schedules-and-advanced-recurrence-with-azure-scheduler"></a>如何 tooBuild 複雜排程與進階與 Azure 排程器的循環
## <a name="overview"></a>概觀
Azure 排程器 hello 核心作業為 hello*排程*。 hello 排程會決定何時以及如何 hello 排程器執行 hello 工作。

Azure 排程器可讓您 toospecify 不同一次性和週期性的排程工作。 *一次*排程會在指定的時間引發一次 – 實際上，它們是僅執行一次的*週期*排程。 週期排程會根據預先決定的頻率引發。

由於這種彈性，Azure 排程器可讓您支援各種商務案例：

* 定期清除資料 – 例如，每一天，刪除所有超過 3 個月的推文
* 封存-例如每月、 推播發票記錄 toobackup 服務
* 要求外部資料 – 例如，每隔 15 分鐘，從 NOAA 提取新的 Ski 氣象報告
* 映像處理-例如每個工作天，在離峰時間，使用的雲端運算 toocompress 映像上傳的那一天

在本文中，我們會逐步引導您完成您可以使用 Azure 排程器建立的範例工作。 我們提供描述每個排程的 hello JSON 資料。 如果您使用 hello[排程器 REST API](https://msdn.microsoft.com/library/mt629143.aspx)，您可以使用這個相同的 JSON[建立 Azure 排程器工作](https://msdn.microsoft.com/library/mt629145.aspx)。

## <a name="supported-scenarios"></a>支援的案例
本主題中的許多範例說明 Azure 排程器支援的案例的 hello 廣度 hello。 廣泛而言，這些範例說明如何對於許多的行為模式，包括 toocreate 排程 hello 的下方：

* 在特定日期和時間執行一次
* 執行並重複執行明確的次數
* 立即執行並重複執行
* 執行，並從特定時間開始，每隔 *n* 分鐘、小時、天、週或個月重複執行一次
* 執行並每週或每個月重複執行一次，但是只在特定日、特定星期幾或特定月日
* 執行並在某個期間執行多次 – 例如，每個月的最後一個星期五和星期一，或在每天上午 5:15 和下午 5:15

## <a name="dates-and-datetimes"></a>日期和日期時間
Azure 排程器作業中的日期，請遵循 「 hello [ISO 8601 規格](http://en.wikipedia.org/wiki/ISO_8601)，並且包含只 hello 日期。

在 Azure 排程器工作的日期時間參考遵循 hello [ISO 8601 規格](http://en.wikipedia.org/wiki/ISO_8601)和包含日期和時間的組件。 未指定 UTC 時差的日期時間會假設 toobe UTC。  

## <a name="how-to-use-json-and-rest-api-for-creating-schedules"></a>如何：使用 JSON 和 REST API 建立排程
簡易排程，使用 toocreate hello [Azure 排程器 REST API](https://msdn.microsoft.com/library/mt629143)、 第一個[向資源提供者註冊訂用帳戶](https://msdn.microsoft.com/library/azure/dn790548.aspx)(排程器的 hello 提供者名稱是*Microsoft.Scheduler*)，然後[建立工作集合](https://msdn.microsoft.com/library/mt629159.aspx)，最後再[建立作業](https://msdn.microsoft.com/library/mt629145.aspx)。 當您建立作業時，您可以指定排程與循環使用 JSON 像 hello 下列節錄的其中一個：

    {
        "startTime": "2012-08-04T00:00Z", // optional
         …
        "recurrence":                     // optional
        {
            "frequency": "week",     // can be "year" "month" "day" "week" "hour" "minute"
            "interval": 1,                // optional, how often toofire (default too1)
            "schedule":                   // optional (advanced scheduling specifics)
            {
                "weekDays": ["monday", "wednesday", "friday"],
                "hours": [10, 22]                      
            },
            "count": 10,                  // optional (default toorecur infinitely)
            "endTime": "2012-11-04",      // optional (default toorecur infinitely)
        },
        …
    }

## <a name="overview-job-schema-basics"></a>概觀：工作結構描述的基本概念
下表中的 hello 提供 hello 主要項目相關的 toorecurrence 和排程工作中的高階概觀：

| **JSON 名稱** | **說明** |
|:--- |:--- |
| ***startTime*** |*startTime* 是日期時間。 簡單的排程， *startTime* hello 第一次出現而且複雜的排程，hello 工作將啟動比立即*startTime*。 |
| ***recurrence*** |hello*循環*物件指定循環規則 hello 作業和 hello 循環 hello 作業將使用來執行。 hello 循環物件支援 hello 元素*頻率、 間隔、 結束時間、 計數、*和*排程*。 如果*循環*定義，*頻率*需要; hello 的其他項目*循環*是選擇性的。 |
| ***frequency*** |hello*頻率*字串 hello 在哪一個 hello 工作重複執行的頻率單位。 支援的值有 *"minute"、"hour"、"day"、"week"* 或 *"month"*。 |
| ***interval*** |hello*間隔*這是一個正整數，並代表 hello hello 間隔*頻率*hello 作業將會執行的頻率決定。 例如，如果*間隔*是 3 和*頻率*是 「 一週 hello 工作重複執行的每個 3 週的時間。 Azure 排程器支援的每個月頻率、每週頻率和每日頻率的最大 *interval* 分別為 18 個月、78 週和 548 天。 小時和分鐘的頻率，hello 支援的範圍是 1 < =*間隔*< = 1000年。 |
| ***endTime*** |hello *endTime*字串會指定 hello 日期-時間過去的 hello 作業不應執行。 它不是有效的 toohave *endTime* hello 過去中。 如果沒有*endTime*或計數指定，則 hello 作業持續執行。 同時*endTime*和*計數*不能包含 hello 相同的作業。 |
| ***count*** |<p>hello*計數*是正整數 （小於或等於零），指定應該執行此作業完成之前的 hello 次數。</p><p>hello*計數*代表 hello 的 hello 作業之前被判定為已完成執行的次數。 例如，針對每日執行的工作*計數*5 和星期一的開始日期、 hello 作業完成之後在星期五執行。 如果 hello 開始日期為過去的 hello，hello 第一次執行會計算從 hello 建立時間。</p><p>如果沒有*endTime*或*計數*指定，則 hello 作業持續執行。 同時*endTime*和*計數*不能包含 hello 相同的作業。</p> |
| ***schedule*** |具有指定頻率的工作會根據週期排程來改變其週期。 *schedule* 包含根據分鐘數、小時數、星期幾數、月日數和週數的修改。 |

## <a name="overview-job-schema-defaults-limits-and-examples"></a>概觀：工作結構描述的預設值、限制和範例
在本概觀之後，讓我們詳細討論其中每一個元素。

| **JSON 名稱** | **值類型** | **必要？** | **預設值** | **有效值** | **範例** |
|:--- |:--- |:--- |:--- |:--- |:--- |
| ***startTime*** |String |否 |None |ISO 8601 日期時間 |<code>"startTime" : "2013-01-09T09:30:00-08:00"</code> |
| ***recurrence*** |Object |否 |None |Recurrence 物件 |<code>"recurrence" : { "frequency" : "monthly", "interval" : 1 }</code> |
| ***frequency*** |String |是 |None |"minute"、"hour"、"day"、"week"、"month" |<code>"frequency" : "hour"</code> |
| ***interval*** |Number |否 |1 |1 too1000。 |<code>"interval":10</code> |
| ***endTime*** |String |否 |None |日期時間值，代表 hello 未來的時間 |<code>"endTime" : "2013-02-09T09:30:00-08:00"</code> |
| ***count*** |Number |否 |None |>= 1 |<code>"count": 5</code> |
| ***schedule*** |Object |否 |None |Schedule 物件 |<code>"schedule" : { "minute" : [30], "hour" : [8,17] }</code> |

## <a name="deep-dive-starttime"></a>深入探討：*startTime*
hello 以下資料表的擷取方式*startTime*控制作業的執行方式。

| **startTime 值** | **無週期** | **週期。無排程** | **搭配排程的週期** |
|:--- |:--- |:--- |:--- |
| **没有開始時間** |立即執行一次 |立即執行一次。 根據從上次執行時間算出的時間執行後續的執行作業 |<p>立即執行一次</p><p>根據週期排程執行後續的執行作業</p> |
| **過去的開始時間** |立即執行一次 |<p>計算開始時間之後的第一個未來執行時間，並在該時間執行</p><p>根據從上次執行時間算出的時間執行後續的執行作業</p><p>如需進一步說明，請參閱此資料表後面的範例</p> |<p>作業啟動*不還快比*hello 指定開始時間。 hello 第一次出現根據 hello 排程從 hello 開始時間計算</p><p>根據週期排程執行後續的執行作業</p> |
| **未來或目前的開始時間** |在指定的開始時間執行一次 |<p>在指定的開始時間執行一次</p><p>根據從上次執行時間算出的時間執行後續的執行作業</p> |<p>作業啟動*不還快比*hello 指定開始時間。 hello 第一次出現根據 hello 排程從 hello 開始時間計算</p><p>根據週期排程執行後續的執行作業</p> |

我們來看看會發生什麼情況的範例位置*startTime*在過去，hello 與*循環*但沒有*排程*。  假設該 hello 目前時間為 2015年-04-08 13:00， *startTime*為 2015年-04-07 14:00，和*循環*為每 2 天 (以定義*頻率*： 日*間隔*: 2。)請注意該 hello *startTime*在過去，hello 和 hello 目前時間之前發生

下列情況 hello*第一次執行*會在 14:00 2015年-04 09\. hello 排程器引擎會計算從 hello 開始時間執行出現次數。  在 hello 過去任何執行個體都會被捨棄。 hello 引擎會使用是發生在未來的 hello 的 hello 下一個執行個體。  因此在此情況下， *startTime*在下午 2:00，為 2015年-04-07，因此 hello 下一個執行個體可從這段時間，也就是在下午 2:00 2015年-04 09 2 天。

請注意 hello 第一次執行會是 hello 相同，即使 hello startTime 2015-04-05 14:00 或 14:00\ 2015年-04-01。 Hello 第一次執行之後，後續執行作業會使用計算 hello 排定 –，其方式是在 2015年-04-11 下午 2:00，然後 2015年-04-13 在下午 2:00，然後在下午 2:00，2015年-04-15 等等。

最後，當某項作業有排程，如果小時及/或分鐘的時間不在 hello 排程，它們預設 toohello 小時及/或分鐘 hello 第一次執行，分別設定。

## <a name="deep-dive-schedule"></a>深入探討：*schedule*
在某一方面，*排程*可以*限制*hello 工作執行的數目。  例如，如果作業的 「 月 」 頻率有*排程*只有 day 31 上執行的、 具有 31 這些月份中的 hello 作業執行<sup>st</sup>一天。

在 hello 相反地，*排程*也可以*展開*hello 工作執行的數目。 例如，如果作業的 「 月 」 頻率有*排程*的月份天數 1 和 2 上的執行，hello 作業上執行 hello 1<sup>st</sup>和 2<sup>nd</sup> hello 而不是只有一次的每月天數月份。

如果指定了多個排程項目，hello 順序是評估的從 hello 最大 toosmallest-週數、 月份日期、 星期、 小時和分鐘。

hello 以下表格說明*排程*詳細資料中的項目。

| **JSON 名稱** | **說明** | **有效值** |
|:--- |:--- |:--- |
| **minutes** |工作將執行的時間的 hello hello 小時的分鐘數 |<ul><li>整數或</li><li>一連串整數</li></ul> |
| **hours** |Hello 一天的 hello 在執行工作時數 |<ul><li>整數或</li><li>一連串整數</li></ul> |
| **weekDays** |天數 hello 週 hello 作業將會執行。 只能搭配 weekly 頻率指定。 |<ul><li>星期一、星期二、星期三、星期四、星期五、星期六或星期日</li><li>陣列的任何值 （最大值的陣列大小 7） 以上的 hello</li></ul>「不」區分大小寫 |
| **monthlyOccurrences** |決定要執行 hello 月份 hello 作業的哪幾天。 只能搭配 monthly 頻率指定。 |<ul><li>monthlyOccurrence 物件的陣列︰</li></ul> <pre>{ "day": *day*,<br />  "occurrence": *occurrence*<br />}</pre><p> *天*hello 天數 hello 週 hello 作業將會執行，例如 {星期日} 是每個星期日的 hello 月份。 必要。</p><p>發生*出現*hello 月 hello 一天的例如 {星期日，-1} 是 hello hello 月份的最後一個星期日。 選用。</p> |
| **monthDays** |天數 hello 月份 hello 作業將會執行。 只能搭配 monthly 頻率指定。 |<ul><li>任何值 <= -1 和 >= -31。</li><li>任何值 >= 1 和 <= 31。</li><li>上述值的陣列</li></ul> |

## <a name="examples-recurrence-schedules"></a>範例：週期排程
hello 如下的循環排程 – 將焦點放在 hello 排程物件和子元素的各種範例。

hello 下方所有排程會假設該 hello*間隔*設定 too1\. 此外，一個必須假設 hello 右邊的頻率，以根據 toowhat 處於 hello*排程*– 例如，一個無法使用頻率"day"，"間 」 所做的修改在 hello 排程。 上面說明了這類限制。

| **範例** | **說明** |
|:--- |:--- |
| <code>{"hours":[5]}</code> |在每天上午 5 點執行。 Azure 排程器中"hours"與每個值"minutes"、 一個、 toocreate 一份所有 hello 時間在哪一個 hello 工作是 toobe 執行符合每個值。 |
| <code>{"minutes":[15], "hours":[5]}</code> |在每天上午 5:15 執行 |
| <code>{"minutes":[15], "hours":[5,17]}</code> |在每天上午 5:15 和下午 5:15 執行 |
| <code>{"minutes":[15,45], "hours":[5,17]}</code> |在每天上午 5:15、上午 5:45、下午 5:15 和下午 5:45 執行 |
| <code>{"minutes":[0,15,30,45]}</code> |每隔 15 分鐘執行一次 |
| <code>{hours":[0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23]}</code> |每小時執行一次。 這項工作每小時執行一次。 hello 分鐘由 hello *startTime*、 如果有指定，或如果未指定，依據 hello 建立時間。 例如，如果 hello 開始時間或 （準套用） 的建立時間為下午 12:25，hello 作業將會執行在 00:01:25，25 02:25，...，23:25。 hello 排程是相等的 toohaving 工作與*頻率*的 「 小時 」，*間隔*的 1，且沒有*排程*。 hello 差異在於，此排程可以用於不同*頻率*和*間隔*toocreate 其他作業太。 例如，如果 hello*頻率*是 「 月 」，hello 排程會執行一次而不是每一天的月份，如果*頻率*了 「 日 」 |
| <code>{minutes:[0]}</code> |每小時執行上 hello 小時。 此作業也會執行每個小時，但在 hello 小時 (例如 12 AM，1 上午 2 AM 等。)這是對等 tooa 工作頻率為 「 小時 」，零分鐘的時間，與沒有排程的 startTime 如果 hello 頻率"day"，但如果 hello 頻率 「 週 」 或 「 月 」，hello 排程就會執行僅一天一週或月，一天分別。 |
| <code>{"minutes":[15]}</code> |在過去每小時 15 分鐘執行。 每小時執行，開始於上午 00:15、上午 1:15、上午 2:15 等等，並結束於下午 10:15 和下午 11:15。 |
| <code>{"hours":[17], "weekDays":["saturday"]}</code> |在每週星期六下午 5 點執行 |
| <code>{hours":[17], "weekDays":["monday", "wednesday", "friday"]}</code> |在每週星期一、星期三、星期五下午 5 點執行 |
| <code>{"minutes":[15,45], "hours":[17], "weekDays":["monday", "wednesday", "friday"]}</code> |在每週星期一、星期三、星期五下午 5:15PM 和 5:45 執行 |
| <code>{"hours":[5,17], "weekDays":["monday", "wednesday", "friday"]}</code> |在每週星期一、星期三、星期五上午 5 點和下午 5 點執行 |
| <code>{"minutes":[15,45], "hours":[5,17], "weekDays":["monday", "wednesday", "friday"]}</code> |在每週星期一、星期三、星期五上午 5:15、上午 5:45、下午 5:15 和下午 5:45 執行 |
| <code>{"minutes":[0,15,30,45], "weekDays":["monday", "tuesday", "wednesday", "thursday", "friday"]}</code> |在工作日每隔 15 分鐘執行一次 |
| <code>{"minutes":[0,15,30,45], "hours": [9, 10, 11, 12, 13, 14, 15, 16] "weekDays":["monday", "tuesday", "wednesday", "thursday", "friday"]}</code> |在工作日上午 9 點與下午 4:45 之間每隔 15 分鐘執行一次 |
| <code>{"weekDays":["sunday"]}</code> |在星期日開始時間執行 |
| <code>{"weekDays":["tuesday", "thursday"]}</code> |在星期二和星期四開始時間執行 |
| <code>{"minutes":[0], "hours":[6], "monthDays":[28]}</code> |上午 6 點上執行 hello 28 日的每個月 （假設頻率個月） |
| <code>{"minutes":[0], "hours":[6], "monthDays":[-1]}</code> |執行於上午 6 點 hello hello 月份的最後一天。 如果您想要的當月最後一天 toorun hello 上的工作，請使用-1，而不是 28、 29、 30 或 31 天。 |
| <code>{"minutes":[0], "hours":[6], "monthDays":[1,-1]}</code> |第一個和最後一天的每個月，上午 6 點執行在 hello |
| <code>{monthDays":[1,-1]}</code> |對執行 hello 第一個和最後一天的每個月開始時間 |
| <code>{monthDays":[1,14]}</code> |對執行 hello 第一個和每月的第十四天開始時間 |
| <code>{monthDays":[2]}</code> |在 hello hello 在開始時間的月份的第二天執行 |
| <code>{"minutes":[0], "hours":[5], "monthlyOccurrences":[{"day":"friday", "occurrence":1}]}</code> |在每個月第一個星期五上午 5 點執行 |
| <code>{"monthlyOccurrences":[{"day":"friday", "occurrence":1}]}</code> |在每個月第一個星期五的開始時間執行 |
| <code>{"monthlyOccurrences":[{"day":"friday", "occurrence":-3}]}</code> |在每個月倒數第三個星期五的開始時間執行 |
| <code>{"minutes":[15], "hours":[5], "monthlyOccurrences":[{"day":"friday", "occurrence":1},{"day":"friday", "occurrence":-1}]}</code> |在每個月第一個和最後一個星期五上午 5:15 執行 |
| <code>{"monthlyOccurrences":[{"day":"friday", "occurrence":1},{"day":"friday", "occurrence":-1}]}</code> |在每個月第一個和最後一個星期五的開始時間執行 |
| <code>{"monthlyOccurrences":[{"day":"friday", "occurrence":5}]}</code> |在每個月第五個星期五的開始時間執行 如果沒有第五個星期五這不會執行，因為它是，一個月中排程的 toorun 星期五只第五個。 您可以考慮使用-1 而不 5，hello 相符項目如果您想在 hello 上次發生的 hello 月份星期五 toorun hello 作業。 |
| <code>{"minutes":[0,15,30,45], "monthlyOccurrences":[{"day":"friday", "occurrence":-1}]}</code> |Hello 月份的最後一個星期五執行每隔 15 分鐘 |
| <code>{"minutes":[15,45], "hours":[5,17], "monthlyOccurrences":[{"day":"wednesday", "occurrence":3}]}</code> |執行在上午 5:15，5:45 AM，5:15 PM 和 5:45 PM 上 hello 第 3 個星期三的每個月 |

## <a name="see-also"></a>另請參閱
 [排程器是什麼？](scheduler-intro.md)

 [Azure 排程器概念、術語及實體階層](scheduler-concepts-terms.md)

 [開始在 hello Azure 入口網站中使用排程器](scheduler-get-started-portal.md)

 [Azure 排程器的計劃和計費](scheduler-plans-billing.md)

 [Azure 排程器 REST API 參考](https://msdn.microsoft.com/library/mt629143)

 [Azure 排程器 PowerShell Cmdlet 參考](scheduler-powershell-reference.md)

 [Azure 排程器高可用性和可靠性](scheduler-high-availability-reliability.md)

 [Azure 排程器限制、預設值和錯誤碼](scheduler-limits-defaults-errors.md)

 [Azure 排程器輸出驗證](scheduler-outbound-authentication.md)

