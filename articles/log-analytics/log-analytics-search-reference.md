---
title: "aaaAzure 記錄分析搜尋參考 |Microsoft 文件"
description: "hello 記錄分析搜尋參考描述 hello 搜尋語言，並提供資料的搜尋和篩選運算式 toohelp 縮小搜尋範圍時，您可以使用 hello 一般查詢語法選項。"
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.assetid: 402615a2-bed0-4831-ba69-53be49059718
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7478a1139b88a1ce76ebb7b76027a6ccd66f4f27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-search-reference"></a>Log Analytics 搜尋參考

>[!NOTE]
> 本文說明的記錄搜尋記錄分析中使用 hello 目前的查詢語言。  如果您的工作區已升級的 toohello[新的記錄分析查詢語言](log-analytics-log-search-upgrade.md)，則您應該太參閱[hello hello 新語言的語言參考](https://go.microsoft.com/fwlink/?linkid=856079)。

hello 關於搜尋語言的下列參考章節描述 hello 一般查詢語法選項，您可以搜尋資料及篩選運算式 toohelp 縮小搜尋範圍時使用。 此外也說明您可以擷取 hello 資料上使用 tootake 動作的命令。

您可以閱讀搜尋中傳回的 hello 欄位和 hello facet，協助您更深入的資料，請在 hello 類別相似探索[搜尋欄位和 facet 參考章節](#search-field-and-facet-reference)。

## <a name="general-query-syntax"></a>一般查詢語法
hello 一般查詢語法如下所示：

```
filterExpression | command1 | command2 …
```

hello 篩選條件運算式 (`filterExpression`) 定義的 hello"where"條件 hello 查詢。 hello 命令會套用 toohello hello 查詢所傳回的結果。 多個命令必須以 hello 縱線字元 (|) 分隔。

### <a name="general-syntax-examples"></a>一般語法範例
範例：

```
system
```

此查詢會傳回結果包含 hello 文字*系統*已索引的全文檢索或詞彙搜尋的任何欄位中。

> [!NOTE]
> 並非所有的欄位會編製索引如此一來，但最常見的文字欄位 （例如描述和名稱） 通常 hello。
>
>

```
system error
```

此查詢會傳回結果包含 hello 文字*系統*和*錯誤*。

```
system error | sort ManagementGroupName, TimeGenerated desc | top 10
```

此查詢會傳回結果包含 hello 文字*系統*和*錯誤*。 它再依 hello 結果 hello *ManagementGroupName*欄位 （依遞增順序），再以 hello *TimeGenerated*欄位 （依遞減順序）。 它會採用只有 hello 前 10 個結果。

> [!IMPORTANT]
> 所有 hello 欄位名稱和 hello hello 字串和文字欄位值會區分大小寫。
>
>

## <a name="filter-expressions"></a>篩選運算式
hello 下列小節將詳細說明 hello 篩選運算式。

### <a name="string-literals"></a>字串常值
字串常值是無法 hello 剖析器辨識為關鍵字或預先定義的資料類型 （例如，數字或日期） 的任何字串。

範例：

```
These all are string literals
```

此查詢會搜尋包含五個字全都出現的結果。 tooperform 複雜的字串搜尋，請 hello 字串常值以引號括起來。 例如：

```
"Windows Server"
```

這只會傳回結果為 Windows Server 的完全相符項目。

### <a name="numbers"></a>數字
hello 剖析器支援數值欄位 hello 十進位整數和浮點數語法。

範例：

```
Type:Perf 0.5
```

```
HTTP 500
```

### <a name="dates-and-times"></a>日期和時間
Hello 系統中的資料的每個片段都有*TimeGenerated*屬性，代表的 hello 記錄 hello 原始日期和時間。 某些資料類型可能另外有日期和時間欄位 (例如，*LastModified*)。

hello 時間表**圖表/時間**Azure Log Analytics 中的選取器會顯示經過一段時間 （相應 toohello 目前執行的查詢） 的結果分佈。 這根據 hello *TimeGenerated*欄位。 日期和時間欄位具有特定字串格式，可用於查詢 toorestrict hello 查詢 tooa 特定時間範圍內。 您也可以使用語法 toorefer toorelative （比方說，「 3 天前和 2 小時前之間 」） 的時間間隔。

hello 下面是語法的供日期和時間的有效形式:

```
yyyy-mm-ddThh:mm:ss.dddZ
```

```
yyyy-mm-ddThh:mm:ss.ddd
```

```
yyyy-mm-ddThh:mm:ss
```

```
yyyy-mm-ddThh:mm:ss
```

```
yyyy-mm-ddThh:mm
```

```
yyyy-mm-dd
```


例如：

```
TimeGenerated:2013-10-01T12:20
```

hello 前一個命令只會傳回*TimeGenerated* 12:20 於 2013 年 10 月 1 日的值。

hello 剖析器也支援助憶鍵日期/時間值 hello，NOW。 （它是不太可能，這樣會產生任何結果，因為資料無法這麼快速 hello 系統）。

這些範例是用於相對與絕對日期的建置組塊 toouse。 在 hello 接下來的三個子節中，您會看到如何 toouse 在更進階的篩選器，透過使用相對日期範圍的範例。

### <a name="datetime-math"></a>日期/時間數學
使用 hello 日期/時間數學運算子 toooffset 或四捨五入 hello 日期/時間值，透過簡單的日期/時間計算。

語法：

```
datetime/unit
```

```
datetime[+|-]count unit
```

| 運算子 | 說明 |
| --- | --- |
| / |將日期/時間 toohello 指定單位。 例如，現在 / DAY 會四捨五入 hello 目前日期/時間 toomidnight hello 的目前日期。 |
| + 或 - |位移日期/時間 hello 所指定單位的數。 例如，NOW + 1hour 會 hello 目前日期/時間往後移一個小時。 2013-10-01t12: 00-10days hello 日期值往回位移 10 天。 |

Hello 日期/時間數學運算子可以鏈結在一起。 例如：

```
NOW+1HOUR-10MONTHS/MINUTE
```

hello 下表列出支援的 hello 日期/時間單位。

| 日期/時間單位 | 說明 |
| --- | --- |
| YEAR, YEARS |重試回合 toocurrent 年份或由 hello 位移指定年的數。 |
| MONTH, MONTHS |重試回合 toocurrent 月份或由 hello 位移指定月的數。 |
| DAY, DAYS, DATE |重試回合 toocurrent 天 hello 月份或由 hello 位移指定的天數。 |
| HOUR, HOURS |重試回合 toocurrent 小時或由 hello 位移指定小時的數。 |
| MINUTE, MINUTES |重試回合 toocurrent 分鐘或由 hello 位移指定分鐘的數。 |
| SECOND, SECONDS |第二，四捨五入 toocurrent 或位移指定的 hello 的秒數字。 |
| MILLISECOND, MILLISECONDS, MILLI, MILLIS |重試回合 toocurrent 毫秒或由 hello 位移指定毫秒的數。 |

### <a name="field-facets"></a>欄位 facet
藉由使用欄位 facet，您可以指定 hello 搜尋條件的特定欄位及其實際值。 這不同於整個 hello 索引的各種詞彙撰寫 「 任意文字 」 查詢。 您已經在數個先前的範例中看過這項技術。 hello 以下是更複雜的範例。

**語法**

```
field:value
```

```
field=value
```

**說明**

搜尋 hello hello 特定值的欄位。 hello 值可以是字串常值、 數字或日期和時間。

例如：

```
TimeGenerated:NOW
```

```
ObjectDisplayName:"server01.contoso.com"
```

```
SampleValue:0.3
```

**語法**

field>value

field<value

field>=value

field<=value

*field!=value*

**說明**

提供比較。

例如：

```
TimeGenerated>NOW+2HOURS
```

**語法**

```
field:[from..to]
```

**說明**

提供範圍面相化。

例如：

```
TimeGenerated:[NOW..NOW+1DAY]
```

```
SampleValue:[0..2]
```

### <a name="in"></a>IN
hello **IN**關鍵字可讓您 tooselect 從值清單。 根據您使用的 hello 語法，這可以是簡單清單所提供，值或彙總從值清單。

語法 1：

```
field IN {value1,value2,value3,...}
```

此語法可讓您 tooinclude 簡易清單中的所有值。



範例：

```
EventID IN {1201,1204,1210}
```

```
Computer IN {"srv01.contoso.com","srv02.contoso.com"}
```

語法 2：

```
(Outer query) (Field toouse with inner query results) IN {Inner query | measure count() by (Field toosend tooouter query)} (rest  of outer query)  
```

此語法可讓您 toocreate 彙總。 您接著可以從這個彙總到另一個外部的 （主要） 搜尋，尋找具有這些值的事件摘要 hello 值清單。 做法是以大括號括住 hello 內部搜尋，再饋送其結果為 hello 外部搜尋中欄位的可能值，使用 hello IN 運算子。

內部查詢範例：*目前遺失安全性更新的電腦*以 hello 下列彙總查詢：

```
Type:Update Classification="Security Updates"  UpdateState=needed TimeGenerated>NOW-25HOURS | measure count() by Computer
```    

hello 最終查詢，以尋找*目前遺失安全性更新的電腦的所有 Windows 事件*類似 hello 下列：

```
Type=Event Computer IN {Type:Update Classification="Security Updates"  UpdateState=needed TimeGenerated>NOW-25HOURS | measure count() by Computer}
```

### <a name="contains"></a>Contains
hello **Contains**關鍵字可讓您 toofilter 記錄與欄位，其中包含指定的字串。 這區分大小寫、僅適用於字串欄位，而且可能不包含任何逸出字元。

語法：

```
field:contains("string")
```

範例：

```
Type:contains("Event")
```

這會傳回包含 hello 字串類型的記錄 「 事件 」。 範例包括 **Event**、**SecurityEvent** 和 **ServiceFabricOperationEvent**。



### <a name="regular-expressions"></a>規則運算式
您也可以使用 hello 與規則運算式，指定欄位的搜尋條件**Regex**關鍵字。 您可以使用規則運算式中的 hello 語法的完整說明，請參閱[記錄分析中使用規則運算式 toofilter 記錄搜尋](log-analytics-log-searches-regex.md)。

語法：

```
field:Regex("Regular Expression")
```

範例：

```
Computer:Regex("^C.*")
```

### <a name="logical-operators"></a>邏輯運算子
hello 查詢語言支援 hello 邏輯運算子 (*AND*，*或者*，和*不*) 及其 C 樣式別名 (*&&*， *||* ，和*！*分別)。 您可以使用括號 toogroup 這些運算子。

範例：

```
system OR error

```

```
Type:Alert AND NOT(Severity:1 OR ObjectId:"8066bbc0-9ec8-ca83-1edc-6f30d4779bcb8066bbc0-9ec8-ca83-1edc-6f30d4779bcb")
```

您可以省略 hello 最上層篩選引數的 hello 邏輯運算子。 在此情況下，會假設 hello AND 運算子。

| 篩選運算式 | 對等太|
| --- | --- |
| system error |system AND error |
| system "Windows Server" OR Severity:1 |system AND ("Windows Server" OR Severity:1) |

### <a name="wildcarding"></a>萬用字元
hello 查詢語言支援使用 hello ( \* ) 字元太表示值在查詢中的一或多個字元。

範例：

 Hello 名稱，例如"REDMOND-SQL"中尋找具有"SQL"的所有電腦。

```
Type=Event Computer=*SQL*
```

> [!NOTE]
> 此時，無法在引號內使用萬用字元。 例如，hello 訊息`"*This text*"`會考慮 hello (\*) 做為常值 (\*) 字元。


## <a name="commands"></a>命令


hello 命令會套用 toohello hello 查詢所傳回的結果。 使用 hello 管道字元 (|) tooapply 命令 toohello 擷取結果。 多個命令必須以 hello 縱線字元分隔。

> [!NOTE]
> 命令名稱可以大寫或小寫，不同於 hello 欄位名稱和 hello 資料撰寫。
>
>

### <a name="sort"></a>排序
語法：

    sort field1 asc|desc, field2 asc|desc, …

依特定欄位排序 hello 結果。 hello asc/desc 表示後置詞 toosort hello 結果按照遞增或遞減的順序是選擇性的。 如果省略，hello *asc*會假設採用排序順序。 Hello **TimeGenerated**  欄位中， *desc*假設排序順序，讓它預設會傳回 hello 最新的結果第一次。

### <a name="toplimit"></a>Top/Limit
語法：

    top number


    limit number
限制 hello 回應 toohello 前 N 個結果。

範例：

    Type:Alert errors detected | top 10

傳回 hello 前 10 個比對結果。

### <a name="skip"></a>Skip
語法：

    skip number

略過 hello 列出的結果數目。

範例：

    Type:Alert errors detected | top 10 | skip 200

從結果 200 開始傳回 10 個比對結果。

### <a name="select"></a>選取
語法：

    select field1, field2, ...

您選擇限制結果 toohello 欄位。

範例：

    Type:Alert errors detected | select Name, Severity

限制太 hello 傳回的結果欄位*名稱*和*嚴重性*。

### <a name="measure"></a>Measure
hello*量值*命令是使用的 tooapply 統計函數 toohello 未經處理的搜尋結果。 這是很有幫助 tooget*分組*hello 資料的檢視。 當您使用 hello measure 命令時，記錄分析搜尋會顯示含有彙總結果的資料表。

**語法：**

    measure aggregateFunction1([aggregatedField]) [as fieldAlias1] [, aggregateFunction2([aggregatedField2]) [as fieldAlias2] [, ...]] by groupField1 [, groupField2 [, groupField3]]  [interval interval]


    measure aggregateFunction1([aggregatedField]) [as fieldAlias1] [, aggregateFunction2([aggregatedField2]) [as fieldAlias2] [, ...]]  interval interval



彙總依 hello 結果*groupField*，並使用計算 hello 彙總的量值*aggregatedField*。

| 量值統計函式 | 說明 |
| --- | --- |
| *aggregateFunction* |hello hello 彙總函式 （不區分大小寫） 的名稱。 支援下列彙總函式的 hello： 計數、 MAX、 MIN、 SUM、 AVG、 STDDEV、 COUNTDISTINCT、 百分位數 # # 或 PCT # # (# # 是介於 1 到 99 之間的數字)。 |
| *aggregatedField* |hello 進行彙總的欄位。 這個欄位是選擇性的 hello 計數彙總函式，但是具有 toobe SUM、 MAX、 MIN、 AVG、 STDDEV、 百分位數 # # 或 PCT # # 的現有數值欄位 (# # 是介於 1 到 99 之間的數字)。 hello aggregatedField 也可以是任何 hello**擴充**支援的函數。 |
| *fieldAlias* |hello hello （選擇性） 別名計算彙總值。 如果未指定，hello 的欄位名稱為**AggregatedValue**。 |
| *groupField* |為分組依據的 hello hello hello 結果集的欄位名稱。 |
| *間隔* |hello 時間間隔，hello 格式：**nnnNAME**。 **nnn**是 hello 正整數。 **名稱**hello 間隔名稱。 支援的間隔名稱區分大小寫，且包括：MILLISECOND[S]、SECOND[S]、MINUTE[S]、HOUR[S]、DAY[S]、MONTH[S] 和 YEAR[S]。 |

hello 間隔選項只可以用於日期/時間群組欄位 (例如*TimeGenerated*和*TimeCreated*)。 目前，這不會強制執行 hello 服務，但是沒有傳遞 toohello 後端的日期/時間欄位會導致執行階段錯誤。 實作 hello 結構描述驗證時，hello 服務 API 會拒絕間隔彙總的使用不含日期/時間欄位的查詢。 目前的 hello*量值*實作支援為任何彙總函式的間隔分組。

如果省略 hello BY 子句，但指定間隔 （作為第二個語法），hello *TimeGenerated*欄位預設會假設。

範例：

**範例 1**

    Type:Alert | measure count() as Count by ObjectId

群組 hello 警示*ObjectID*，並計算每個群組的警示的 hello 數目。 hello 傳回彙的總值為 hello*計數*欄位 （別名）。

**範例 2**

    Type:Alert | measure count() interval 1HOUR

群組依據 1 小時間隔 hello 警示使用 hello *TimeGenerated*欄位，以及每個間隔中的警示傳回 hello 數目。

**範例 3**

    Type:Alert | measure count() as AlertsPerHour interval 1HOUR

如同 hello 上述範例中，但使用彙總的欄位別名 (*AlertsPerHour*)。

**範例 4**

    * | measure count() by TimeCreated interval 5DAYS

使用 hello，依據 5 天間隔分組 hello 結果*TimeCreated*欄位，以及每個間隔中的結果傳回 hello 數目。

**範例 5**

    Type:Alert | measure max(Severity) by WorkflowName

群組的工作負載名稱 hello 警示，並傳回 hello 每個工作流程的最大警示嚴重性值。

**範例 6**

    Type:Alert | measure min(Severity) by WorkflowName

如同 hello 上述範例中，但使用 hello *min*彙總函式。

**範例 7**

    Type:Perf | measure avg(CounterValue) by Computer

效能分組的電腦，然後計算 hello 平均 (avg)。

**範例 8**

    Type:Perf | measure sum(CounterValue) by Computer

與 hello 前一個範例相同，但使用*總和*。

**範例 9**

    Type:Perf | measure stddev(CounterValue) by Computer

與 hello 前一個範例相同，但使用*stddev*。

**範例 10**

    Type:Perf | measure percentile70(CounterValue) by Computer

與 hello 前一個範例相同，但使用*percentile70*。

**範例 11**

    Type:Perf | measure pct70(CounterValue) by Computer

與 hello 前一個範例相同，但使用*pct70*。 請注意，PCT## 只是 PERCENTILE## 函式的別名。

**範例 12**

    Type:Perf | measure avg(CounterValue) by Computer, CounterName

依電腦第一次群組效能然後 CounterName 和計算 hello 平均 (avg)。

**範例 13**

    Type:Alert | measure count() as Count by WorkflowName | sort Count desc | top 5

取得 hello 與 hello 警示最大數目的前五個工作流程。

**範例 14**

    * | measure countdistinct(Computer) by Type

計算 hello 報告每個類型的唯一電腦數目。

**範例 15**

    * | measure countdistinct(Computer) Interval 1HOUR

計算 hello 每小時報告的唯一電腦數目。

**範例 16**

```
Type:Perf CounterName=”% Processor Time” InstanceName=”_Total” | measure avg(CounterValue) by Computer Interval 1HOUR
```

群組 %Processor Time 的電腦，並傳回 hello 平均每小時。

**範例 17**

    Type:W3CIISLog | measure max(TimeTaken) by csMethod Interval 5MINUTES

群組 W3CIISLog 方法，並傳回 hello 最大值為每隔 5 分鐘。

**範例 18**

```
Type:Perf CounterName=”% Processor Time” InstanceName=”_Total”  | measure min(CounterValue) as MIN, avg(CounterValue) as AVG, percentile75(CounterValue) as PCT75, max(CounterValue) as MAX by Computer Interval 1HOUR
```

群組 %Processor Time 的電腦，並傳回 hello 最小值、 平均、 第 75 百分位數 及每小時最大值。

**範例 19**

```
Type:Perf CounterName=”% Processor Time”  | measure min(CounterValue) as MIN, avg(CounterValue) as AVG, percentile75(CounterValue) as PCT75, max(CounterValue) as MAX by Computer, InstanceName Interval 1HOUR
```

群組 %Processor Time 先依電腦和執行個體名稱，以及傳回 hello 最小值、 平均值、 第 75 個百分位數及每小時最大值。

**範例 20**

```
Type= Perf CounterName="Disk Writes/sec" Computer="BaconDC01.BaconLand.com" | measure max(product(CounterValue,60)) as MaxDWPerMin by InstanceName Interval 1HOUR
```

計算每個磁碟的每分鐘在您的電腦上的磁碟寫入的 hello 最大值。

### <a name="where"></a>Where
語法：

```
**where** AggregatedValue>20
```

僅適用於之後*量值*命令 toofurther 篩選 hello 彙總結果的 hello*量值*彙總函數所產生。

範例：

    Type:Perf CounterName:"% Total Run Time" | Measure max(CounterValue) as MAXCPU by Computer

    Type:Perf CounterName:"% Total Run Time" | Measure max(CounterValue) by Computer | where (AggregatedValue>50 and AggregatedValue<90)



### <a name="dedup"></a>Dedup
語法：

    Dedup FieldName

傳回 hello hello 指定欄位的每個唯一值找到的第一個文件。

範例：

    Type=Event | Dedup EventID | sort TimeGenerated DESC

這個範例會傳回一個事件 （hello 最新事件），每個 EventID。

### <a name="join"></a>Join
聯結 hello 結果的兩個查詢 tooform 單一結果集。  支援多個聯結類型描述 hello 依照資料表。

| 聯結類型 | 說明 |
|:--|:--|
| inner | 只傳回具有兩個查詢相符值的記錄。 |
| outer | 傳回兩個查詢的所有記錄。  |
| left  | 傳回左查詢的所有記錄，以及傳回右查詢的相符記錄。 |


- 聯結目前不支援包含 hello 查詢**IN**關鍵字、 hello**量值**命令或 hello**擴充**命令它是否為目標欄位從 hello 右側的查詢。
- 您目前只可以在一個聯結中包含單一欄位。
- 單一搜尋可能不包含一個以上的聯結。

**語法**

```
<left-query> | JOIN <join-type> <left-query-field-name> (<right-query>) <right-query-field-name>
```

**範例**

tooillustrate hello 不同的聯結類型，請考慮加入的資料類型從呼叫 hello 活動訊號 MyBackup_CL 每一部電腦的自訂記錄檔收集。  這些資料型別具有下列資料的 hello。

`Type = MyBackup_CL`

| TimeGenerated | 電腦 | LastBackupStatus |
|:---|:---|:---|
| 4/20/2017 01:26:32.137 AM | srv01.contoso.com | 成功 |
| 4/20/2017 02:13:12.381 AM | srv02.contoso.com | 成功 |
| 4/20/2017 02:13:12.381 AM | srv03.contoso.com | 失敗 |

`Type = Hearbeat` (只會顯示部分的欄位)

| TimeGenerated | 電腦 | ComputerIP |
|:---|:---|:---|
| 4/21/2017 12:01:34.482 PM | srv01.contoso.com | 10.10.100.1 |
| 4/21/2017 12:02:21.916 PM | srv02.contoso.com | 10.10.100.2 |
| 4/21/2017 12:01:47.373 PM | srv04.contoso.com | 10.10.100.4 |

#### <a name="inner-join"></a>inner join

`Type=MyBackup_CL | join inner Computer (Type=Heartbeat) Computer`

傳回 hello 下列記錄其中 hello 電腦欄位必須符合為這兩個資料型別。

| 電腦| TimeGenerated | LastBackupStatus | TimeGenerated_joined | ComputerIP_joined | Type_joined |
|:---|:---|:---|:---|:---|:---|
| srv01.contoso.com | 4/20/2017 01:26:32.137 AM | 成功 | 4/21/2017 12:01:34.482 PM | 10.10.100.1 | Heartbeat |
| srv02.contoso.com | 4/20/2017 02:13:12.381 AM | 成功 | 4/21/2017 12:02:21.916 PM | 10.10.100.2 | Heartbeat |


#### <a name="outer-join"></a>outer join

`Type=MyBackup_CL | join outer Computer (Type=Heartbeat) Computer`

傳回 hello 下列這兩種資料類型的記錄。

| 電腦| TimeGenerated | LastBackupStatus | TimeGenerated_joined | ComputerIP_joined | Type_joined |
|:---|:---|:---|:---|:---|:---|
| srv01.contoso.com | 4/20/2017 01:26:32.137 AM | 成功  | 4/21/2017 12:01:34.482 PM | 10.10.100.1 | Heartbeat |
| srv02.contoso.com | 4/20/2017 02:14:12.381 AM | 成功  | 4/21/2017 12:02:21.916 PM | 10.10.100.2 | Heartbeat |
| srv03.contoso.com | 4/20/2017 01:33:35.974 AM | 失敗  | 4/21/2017 12:01:47.373 PM | | |
| srv04.contoso.com |                           |          | 4/21/2017 12:01:47.373 PM | 10.10.100.2 | Heartbeat |



#### <a name="left-join"></a>left join

`Type=MyBackup_CL | join left Computer (Type=Heartbeat) Computer`

傳回從 MyBackup_CL 下列記錄與任何比對的欄位從 活動訊號的 hello。

| 電腦| TimeGenerated | LastBackupStatus | TimeGenerated_joined | ComputerIP_joined | Type_joined |
|:---|:---|:---|:---|:---|:---|
| srv01.contoso.com | 4/20/2017 01:26:32.137 AM | 成功 | 4/21/2017 12:01:34.482 PM | 10.10.100.1 | Heartbeat |
| srv02.contoso.com | 4/20/2017 02:13:12.381 AM | 成功 | 4/21/2017 12:02:21.916 PM | 10.10.100.2 | Heartbeat |
| srv03.contoso.com | 4/20/2017 02:13:12.381 AM | 失敗 | | | |


### <a name="extend"></a>Extend
可讓您 toocreate 執行階段在查詢欄位中。 請注意，執行階段欄位不能與 hello measure 命令 tooperform 彙總。

**範例 1**

    Type=SQLAssessmentRecommendation | Extend product(RecommendationScore, RecommendationWeight) AS RecommendationWeightedScore
顯示 SQL 評估建議的加權建議分數。

**範例 2**

    Type=Perf CounterName="Private Bytes" | EXTEND div(CounterValue,1024) AS KBs | Select CounterValue,Computer,KBs
顯示計數器值，單位為 KB，而非位元組。

**範例 3**

    Type=WireData | EXTEND scale(TotalBytes,0,100) AS ScaledTotalBytes | Select ScaledTotalBytes,TotalBytes | SORT TotalBytes DESC
標尺 hello WireData TotalBytes 的值的所有結果介於 0 到 100 之間。

**範例 4**

```
Type=Perf CounterName="% Processor Time" | EXTEND if(map(CounterValue,0,50,0,1),"HIGH","LOW") as UTILIZATION
```
將小於 50% 的效能計數器值標記為 LOW，而將其他值標記為 HIGH。

**範例 5**

```
Type= Perf CounterName="Disk Writes/sec" Computer="BaconDC01.BaconLand.com" | Extend product(CounterValue,60) as DWPerMin| measure max(DWPerMin) by InstanceName Interval 1HOUR
```
計算每個磁碟的每分鐘在您的電腦上的磁碟寫入的 hello 最大值。

**支援的函式**

| 函式 | 說明 | 語法範例 |
| --- | --- | --- |
| abs |傳回 hello 絕對值 hello 指定值或函式。 |`abs(x)` <br> `abs(-5)` |
| acos |傳回值或函式的反餘弦值。 |`acos(x)` |
| 和 |如果且只有全部的運算元都評估 tootrue，則傳回 true 值。 |`and(not(exists(popularity)),exists(price))` |
| asin |傳回值或函式的反正弦值。 |`asin(x)` |
| atan |傳回值或函式的反正切值。 |`atan(x)` |
| atan2 |傳回所產生的 x，y toopolar 座標 hello 矩形座標 hello 轉換 hello 角度。 |`atan2(x,y)` |
| cbrt |立方根。 |`cbrt(x)` |
| ceil |Tooan 整數向上四捨五入。 |`ceil(x)`  <br> `ceil(5.6)`：傳回 6 |
| cos |傳回角度的餘弦值。 |`cos(x)` |
| cosh |傳回角度的雙曲餘弦值。 |`cosh(x)` |
| def |預設值的縮寫。 傳回 hello 欄位"field"的值。 如果 hello 欄位不存在，傳回指定的 hello 預設值，並產生 hello 第一個值位置： `exists()==true`。 |`def(rating,5)`。 此 def() 函式傳回 hello 評等，或如果未分級是 hello 文件中指定，會傳回 5。 <br> `def(myfield, 1.0)`相當太`if(exists(myfield),myfield,1.0)`。 |
| 度 |將弧度 toodegrees 的轉換。 |`deg(x)` |
| div |`div(x,y)` 除以 x 乘以 y。 |`div(1,y)` <br> `div(sum(x,100),max(y,1))` |
| dist |傳回兩個向量之間，（點） n 維度空間中的 hello 距離。 採用 hello 電源，加上兩個或多個，ValueSource 執行個體，並計算 hello hello 兩個向量之間的距離。 每個 ValueSource 都必須是數字。 必須有偶數的 ValueSource 執行個體傳入，並 hello 方法會假設 hello 前半部代表第一個向量的 hello，hello 半部代表 hello 第二個向量。 |`dist(2, x, y, 0, 0)`計算 hello 歐幾里德距離 (0，0) 和 (x，y) 每個文件。 <br> `dist(1, x, y, 0, 0)`計算 hello 曼哈頓 （計程車） 距離 (0，0) 和 (x，y) 每個文件。 <br> `dist(2,,x,y,z,0,0,0)`：每個文件的 (0,0,0) 和 (x,y,z) 之間的 Euclidean 距離。<br>`dist(1,x,y,z,e,f,g)`：(x,y,z) 和 (e,f,g) 之間的 Manhattan 距離，其中每個字母是欄位名稱。 |
| exists |傳回 TRUE，如果有任何欄位成員的 hello 存在。 |`exists(author)`傳回在 hello"author"欄位具有數值的任何文件，則為 TRUE。<br>`exists(query(price:5.00))`：如果 "price" 符合 "5.00" 則傳回 TRUE。 |
| exp |傳回歐拉數引發 toopower x。 |`exp(x)` |
| floor |將下 tooan 整數進位。 |`floor(x)`  <br> `floor(5.6)`：傳回 5 |
| hypo |傳回 sqrt(sum(pow(x,2),pow(y,2)))，而不需要中繼溢位或反向溢位。 |`hypo(x,y)`  <br> ` |
| if |啟用條件式函式查詢。 在`if(test,value1,value2)`，測試為或稱為 tooa 邏輯值或傳回邏輯值 （TRUE 或 FALSE） 運算式。 `value1`hello 值傳回 hello 函式如果測試結果為 TRUE。 `value2`hello 值傳回 hello 函式如果測試結果 FALSE。 運算式可以是輸出布林值的任何函式。 也可以是傳回數值的函式，在此情況下，值 0 會解譯為 false 或傳回字串，在此情況下，空字串會解譯為 false。 |`if(termfreq(cat,'electronics'),popularity,42)`此函式會檢查每個文件 toosee，如果它包含"electronics"hello cat 欄位中的 hello 一詞。 如果它，然後 hello hello popularity 欄位的值會傳回。 否則，傳回 hello 42 一值。 |
| linear |實作 `m*x+c`，其中 m 和 c 是常數，而 x 是任意函式。 這相當太`sum(product(m,x),c)`，但當它實作為單一函式稍微更有效率。 |`linear(x,m,c) linear(x,2,4)` 傳回 `2*x+4` |
| ln |傳回 hello 自然對數的 hello 指定函式。 |`ln(x)` |
| log |傳回 hello 記錄檔基底 10 hello 的指定函式。 |`log(x)   log(sum(x,100))` |
| map |對應任何輸入函式 x 的值落在 min 和 max (含） 之間 toohello 指定的目標。 hello 引數的 min 和 max 必須是常數。 hello 引數的目標和預設值可以是常數或函式。 如果 x 的 hello 值不在 min 和 max 之間，則會傳回 x 的任一個 hello 值，或若指定做為第 5 個引數，則傳回預設值。 |`map(x,min,max,target) map(x,0,0,1)`變更任何 0 too1 的值。 這可用於處理預設值 0 的值。<br> `map(x,min,max,target,default)    map(x,0,100,1,-1)`變更任何 0 和 100 too1 與所有其他值太-1 之間的值。<br>  `map(x,0,100,sum(x,599),docfreq(text,solr))`變更任何值，介於 0 和 100 toox + 599 和所有其他值 toofrequency 的 hello hello 欄位文字中的 ' solr' 一詞。 |
| max |傳回 hello 的多個巢狀函式或常數，指定為引數的最大數值： `max(x,y,...)`。 hello max 函式也可用於 「 bottoming"另一個函式位於某些指定常數或欄位。  使用 hello`field(myfield,max)`語法選取單一多值欄位的 hello 最大值。 |`max(myfield,myotherfield,0)` |
| Min |傳回 hello 的常數，指定為引數的多個巢狀函式的最小數值： `min(x,y,...)`。 hello min 函式也可以用來將提供在使用常數的函式 「 上限 」。 使用 hello`field(myfield,min)`語法選取單一多值欄位的 hello 最小值。 |`min(myfield,myotherfield,0)` |
| mod |計算 hello 的 hello 函式 x 的 hello 函式 y 的模數。 |`mod(1,x)` <br> `mod(sum(x,100), max(y,1))` |
| ms |傳回其引數之間差異的毫秒。 日期是相對 toohello Unix 或 POSIX 時間 epoch、 午夜，1970 年 1 月 1 日 UTC。 引數可以是 hello 名稱索引的 TrieDateField 或根據常數日期或 NOW。 `ms()`相當太`ms(NOW)`，數目 hello 新紀元以來的毫秒數。 `ms(a)`傳回 hello 引數代表的 hello 新紀元以來的 hello 的毫秒數。 `ms(a,b)`傳回 hello 的毫秒數 b 之前發生，也就是`a - b`。 |`ms(NOW/DAY)`<br>`ms(2000-01-01T00:00:00Z)`<br>`ms(mydatefield)`<br>`ms(NOW,mydatefield)`<br>`ms(mydatefield,2000-01-01T00:00:00Z)`<br>`ms(datefield1,datefield2)` |
| 否 |邏輯否定的 hello hello 值包裝函式。 |`not(exists(author))`：當 `exists(author)` 為 false 時才為 TRUE。 |
| 或 |邏輯分離。 |`or(value1,value2)`：如果 value1 或 value2 為 true，則為 TRUE。 |
| pow |引發 hello 指定指定的基底 toohello 電源。 `pow(x,y)`引發 x toohello 乘 y。 |`pow(x,y)`<br>`pow(x,log(y))`<br>`pow(x,0.5)`hello 與 sqrt 的相同。 |
| product |傳回 hello 的多個值或函式，以逗號分隔的清單中指定的產品。 `mul(...)` 也可以作為這個函式的別名。 |`product(x,y,...)`<br>`product(x,2)`<br>`product(x,y)`<br>`mul(x,y)` |
| recip |執行 `recip(x,m,a,b)` 實作 `a/(m*x+b)` 的倒數函式，其中 m、a 和 b 是常數，而 x 是任何任意複雜函式。 a 與 b 相等而且 x>=0 時，此函式的最大值為 1，會在 x 增加時減少。 增加 hello 值 hello 整個函式 tooa 移動 b 一起結果呈現 hello 曲線的一部分。 x 為 `rord(datefield)`時，這些屬性可以將這個設為提升較新文件的理想函式。 |`recip(myfield,m,a,b)`<br>`recip(rord(creationDate),1,1000,1000)` |
| rad |將轉換度 tooradians。 |`rad(x)` |
| rint |重試回合 toohello 接近的整數。 |`rint(x)`  <br> `rint(5.6)`：傳回 6 |
| sin |傳回角度的正弦值。 |`sin(x)` |
| sinh |傳回角度的雙曲正弦值。 |`sinh(x)` |
| 級別 |標尺的 hello 函式 x 的值，例如其落 hello 之間指定的 minTarget 和 maxTarget （含)。 hello 目前的實作會周遊所有的 hello 函式值 tooobtain hello min 和 max，因而取得 hello 正確調整規模。 hello 目前的實作無法區別已刪除的文件，或沒有值的文件。 在這些情況下，它會使用 0.0 值。 這表示，如果值通常都大於 0.0，其中一個可以仍然以 0.0 結束 hello 從最小值 toomap 如下。 在這些情況下，適當`map()`函式可用為因應措施 toochange 0.0 tooa hello 實際範圍內值，如下所示：`scale(map(x,0,0,5),1,2)` |`scale(x,minTarget,maxTarget)`<br>`scale(x,1,2)`標尺 hello x 的值，使所有值都都介於 1 和 2 （含) 之間。 |
| sqrt |傳回 hello 平方根 hello 指定值或函式。 |`sqrt(x)`<br>`sqrt(100)`<br>`sqrt(sum(x,100))` |
| strdist |計算兩個字串之間的 hello 距離。 使用 hello Lucene 拼字檢查工具 StringDistance 介面，並支援所有可用該套件中的 hello 實作。 也允許應用程式 tooplug 自己，透過 Solr 的資源載入功能。 strdist 採用 `(string1, string2, distance measure)`。 距離量值的可能值如下︰<ul><li>jw: Jaro-Winkler</li><li>編輯︰Levenstein 或編輯距離</li><li>ngram: NGramDistance，hello 如果指定，可以選擇傳入 hello ngram 大小太。 預設值為 2。</li><li>FQN︰ 完整類別名稱 hello StringDistance 介面的實作。 必須要有無引數建構函式。</li></ul> |`strdist("SOLR",id,edit)` |
| sub |從 `sub(x,y)`傳回 x-y。 |`sub(myfield,myfield2)`<br>`sub(100,sqrt(myfield))` |
| Sum |傳回 hello 多個值或函式，以逗號分隔的清單中指定的總和。 `add(...)` 可以作為這個函式的別名。 |`sum(x,y,...)`<br>`sum(x,1)`<br>`sum(x,y)`<br>`sum(sqrt(x),log(y),z,0.5)`<br>`add(x,y)` |
| termfreq |傳回 hello 詞彙出現在該文件的 hello 欄位中的 hello 次數。 |termfreq(text,'memory') |
| tan |傳回角度的正切值。 |`tan(x)` |
| tanh |傳回角度的雙曲正切值。 |`tanh(x)` |

## <a name="search-field-and-facet-reference"></a>搜尋欄位和 Facet 參考 (英文)
當您使用記錄搜尋 toofind 資料時，結果會顯示各種欄位和 facet。 Hello 資訊的某些部分可能不會出現太清楚。 使用下列資訊 toohelp 您了解 hello 結果 hello。

| 欄位 | 搜尋類型 | 說明 |
| --- | --- | --- |
| TenantId |全部 |使用 toopartition 資料。 |
| TimeGenerated |全部 |使用 toodrive hello 時間軸，timeselectors （在搜尋和其他螢幕中）。 它代表 hello 資料片段的產生 （通常在 hello 代理程式）。 hello 時間以 ISO 格式表示，且一律為 UTC。 在現有的檢測 （也就是記錄檔中的事件） 為基礎之型別的 hello 情況下，這通常是真實時間該 hello 日誌項目/行/記錄 hello。 Hello 的某些其他透過管理組件或 hello 雲端 （例如，建議或警示） 中所產生的型別 hello 一些不同的時間表示。 這是當收集到這個新資料片段和某種組態之快照，或根據它產生建議/警示的 hello 時間。 |
| EventID |Event |Hello Windows 事件記錄檔中的 EventID。 |
| EventLog |Event |其中 hello 事件記錄的 Windows 事件記錄檔。 |
| EventLevelName |Event |重大/警告/資訊/成功 |
| EventLevel |Event |重大/警告/資訊/成功的數值 (對於更容易/更適合閱讀的查詢，請改用 EventLevelName)。 |
| SourceSystem |全部 |Hello 資料來自何處 （的附加模式 toohello 服務）。 範例包括 Microsoft System Center Operations Manager 和 Azure 儲存體。 |
| ObjectName |PerfHourly |Windows 效能物件名稱。 |
| InstanceName |PerfHourly |Windows 效能計數器執行個體名稱。 |
| CounteName |PerfHourly |Windows 效能計數器名稱。 |
| ObjectDisplayName |PerfHourly、ConfigurationAlert、ConfigurationObject、ConfigurationObjectProperty |在 Operations Manager 中效能集合規則以其為目標的 hello 物件的顯示名稱。 也可能是 hello 的 Operational Insights 所探索到的 hello 物件的顯示名稱，或針對哪些 hello 產生警示。 |
| RootObjectName |PerfHourly、ConfigurationAlert、ConfigurationObject、ConfigurationObjectProperty |Hello hello （在雙主控關聯性） 中的父代在 Operations Manager 中效能集合規則以其為目標的 hello 物件父系的顯示名稱。 也可能是 hello 的 Operational Insights 所探索到的 hello 物件的顯示名稱，或針對哪些 hello 產生警示。 |
| 電腦 |大部分的類型 |Hello 資料所屬的電腦名稱。 |
| DeviceName |ProtectionStatus |電腦名稱 hello 資料太所屬 （相同 「 電腦 」）。 |
| DetectionId |ProtectionStatus | |
| ThreatStatusRank |ProtectionStatus |威脅狀態排名是 hello 威脅狀態的數值表示法。 類似 tooHTTP 回應碼，hello 排名有 hello 數字之間的間距 （這就是為什麼沒有威脅是 150 並不是 100 或 0），留出空間 tooadd 新狀態。 威脅狀態和防護狀態的彙總，如 hello 意圖會是 tooshow hello 的最差狀態 hello 電腦已在選取的時間週期的 hello 期間。 hello 數字排名 hello 不同狀態，讓您可以查看 hello 記錄與 hello 最高數字。 |
| ThreatStatus |ProtectionStatus |ThreatStatus 的描述，與 ThreatStatusRank 1:1 對應。 |
| TypeofProtection |ProtectionStatus |Hello 電腦中偵測到的反惡意程式碼產品： 無、 Microsoft 惡意程式碼移除工具、 Forefront 等等。 |
| ScanDate |ProtectionStatus | |
| SourceHealthServiceId |ProtectionStatus、RequiredUpdate |這台電腦之代理程式的 HealthService 識別碼。 |
| HealthServiceId |大部分的類型 |這台電腦之代理程式的 HealthService 識別碼。 |
| ManagementGroupName |大部分的類型 |Operations Manager 附加代理程式的管理群組名稱。 否則會是 null/空白。 |
| ObjectType |ConfigurationObject |由 Log Analytics 組態評估所探索到之這個物件的類型 (例如 Operations Manager 管理組件的類型/類別)。 |
| UpdateTitle |RequiredUpdate |Hello 已找不到已安裝的更新名稱。 |
| PublishDate |RequiredUpdate |當 hello 更新 Microsoft Update 上發佈。 |
| 伺服器 |RequiredUpdate |電腦名稱 hello 資料太所屬 （相同 「 電腦 」）。 |
| 產品 |RequiredUpdate |套用於 hello 更新的產品。 |
| UpdateClassification |RequiredUpdate |更新類型 (例如，更新彙總套件、Service Pack)。 |
| KBID |RequiredUpdate |描述此最佳做法或更新的 KB 文章識別碼。 |
| WorkflowName |ConfigurationAlert |Hello 規則或監視產生 hello 警示的名稱。 |
| 嚴重性 |ConfigurationAlert |Hello 警示的嚴重性。 |
| 優先順序 |ConfigurationAlert |Hello 警示的優先順序。 |
| IsMonitorAlert |ConfigurationAlert |此警示由監視器 (true) 或規則 (false) 所產生？ |
| AlertParameters |ConfigurationAlert |Hello 記錄分析警示的 hello 參數的 XML。 |
| Context |ConfigurationAlert |Hello 警示內容的 hello 記錄分析的 XML。 |
| 工作負載 |ConfigurationAlert |技術或 hello 警示的工作負載參考。 |
| AdvisorWorkload |建議 |技術或 hello 建議的工作負載參考。 |
| 說明 |ConfigurationAlert |警示描述 (簡短)。 |
| DaysSinceLastUpdate |UpdateAgent |幾天前 (這筆記錄的相對 tooTimeGenerated) 沒有此代理程式安裝任何更新從 Windows Server Update Service (WSUS) 或 Microsoft Update？ |
| DaysSinceLastUpdateBucket |UpdateAgent |根據 DaysSinceLastUpdate，多久以前的時間值區分類是上一次從 WSUS/Microsoft Update 安裝任何更新的電腦。 |
| AutomaticUpdateEnabled |UpdateAgent |自動更新檢查是在此代理程式上啟用或停用的嗎？ |
| AutomaticUpdateValue |UpdateAgent |是用來自動更新檢查設定 tooautomatically 下載和安裝、 只下載，或只檢查嗎？ |
| WindowsUpdateAgentVersion |UpdateAgent |Hello Microsoft Update 代理程式版本號碼。 |
| WSUSServer |UpdateAgent |此更新代理程式的目標是哪個 WSUS 伺服器？ |
| OSVersion |UpdateAgent |Hello 作業系統版本上執行此更新代理程式。 |
| 名稱 |建議，ConfigurationObjectProperty |名稱/標題 hello 建議，或記錄分析 configuration assessment 中的 hello 屬性的名稱。 |
| 值 |ConfigurationObjectProperty |來自 Log Analytics 組態評估的屬性值。 |
| KBLink |建議 |描述此最佳作法或更新的 URL toohello KB 文章。 |
| RecommendationStatus |建議 |建議 hello 為一些類型，其記錄取得更新，剛加入 toohello 搜尋索引。 此狀態會變更 hello 建議是否作用中/開啟，或如果記錄分析偵測到它已解決。 |
| RenderedDescription |Event |Windows 事件的呈現描述 (具有填入參數的重複使用文字)。 |
| ParameterXml |Event |Windows 事件 （如事件檢視器中所見） hello data 區段中的 hello 參數的 XML。 |
| EventData |Event |Hello 整個資料一節中的 Windows 事件 （如同在事件檢視器） 的 XML。 |
| 來源 |Event |產生 hello 事件的事件記錄檔來源。 |
| EventCategory |Event |直接從 hello Windows 事件記錄檔的 hello 事件類別目錄。 |
| UserName |Event |Hello Windows 事件 (通常是 NT AUTHORITY\LOCALSYSTEM) 的使用者名稱。 |
| SampleValue |PerfHourly |Hello 每小時彙總效能計數器的平均值。 |
| Min |PerfHourly |Hello 效能計數器每小時彙總的每小時間隔內的最小值。 |
| max |PerfHourly |Hello 效能計數器每小時彙總的每小時間隔內的最大值。 |
| Percentile95 |PerfHourly |hello 第 95 個百分 hello 效能計數器每小時彙總的每小時間隔。 |
| SampleCount |PerfHourly |多少 「 未經處理的效能計數器範例已使用的 tooproduce 此每小時彙總記錄。 |
| Threat |ProtectionStatus |找到的惡意程式碼名稱。 |
| StorageAccount |W3CIISLog |Azure 儲存體帳戶 hello 記錄被讀取。 |
| AzureDeploymentID |W3CIISLog |所屬的 azure 部署識別碼 hello 雲端服務 hello 記錄檔。 |
| 角色 |W3CIISLog |所屬的 hello Azure 雲端服務 hello 記錄檔的角色。 |
| RoleInstance |W3CIISLog |Hello hello 記錄的 Azure 角色的 RoleInstance 所屬。 |
| sSiteName |W3CIISLog |Hello 記錄檔的 IIS 網站所屬 too(metabase notation);hello hello 原始記錄中的 s-sitename 欄位。 |
| sComputerName |W3CIISLog |hello hello 原始記錄中的 s-computername 欄位。 |
| sIP |W3CIISLog |伺服器 IP 位址 hello HTTP 要求被定址的目標。 hello hello 原始記錄中的 s-ip 欄位。 |
| csMethod |W3CIISLog |HTTP 方法 （例如，GET/POST） hello hello HTTP 要求中的用戶端使用。 hello cs 方法 hello 原始記錄中。 |
| cIP |W3CIISLog |用戶端 IP 位址 hello HTTP 要求的來源。 hello hello 原始記錄中的 c-ip 欄位。 |
| csUserAgent |W3CIISLog |Hello 用戶端所宣告的 HTTP User-agent (瀏覽器或其他)。 hello cs-使用者代理程式 hello 原始記錄中。 |
| scStatus |W3CIISLog |用戶端-伺服器 toohello hello 傳回 HTTP 狀態碼 (例如 200/403/500)。 hello 中 cs-status hello 原始記錄檔。 |
| TimeTaken |W3CIISLog |時間長度 （以毫秒為單位） 的 hello 要求所花費 toocomplete。 hello hello 原始記錄中的 timetaken 欄位。 |
| csUriStem |W3CIISLog |要求的相對 URI (沒有主機位址，也就是 /search) 的要求。 hello hello 原始記錄中的 cs-uristem 欄位。 |
| csUriQuery |W3CIISLog |URI 查詢。 只有 ASP 頁面等動態頁面才需要 URI 查詢，所以此欄位通常包含靜態網頁的連字號。 |
| sPort |W3CIISLog |已傳送 hello HTTP 要求的伺服器連接埠 （和 IIS 所接聽，因為它會挑選它）。 |
| csUserName |W3CIISLog |如果 hello 要求已通過驗證且不匿名，驗證使用者名稱。 |
| csVersion |W3CIISLog |Hello 要求 (例如，HTTP/1.1) 中使用的 HTTP 通訊協定版本。 |
| csCookie |W3CIISLog |Cookie 資訊。 |
| csReferer |W3CIISLog |Hello 使用者上次造訪的網站。 這個網站提供連結 toohello 目前站台。 |
| csHost |W3CIISLog |要求的主機標頭 (例如，www.mysite.com)。 |
| scSubStatus |W3CIISLog |子狀態錯誤碼。 |
| scWin32Status |W3CIISLog |Windows 狀態碼。 |
| csBytes |W3CIISLog |從 hello 用戶端 toohello 伺服器 hello 要求中傳送的位元組。 |
| scBytes |W3CIISLog |在 hello 伺服器 toohello 用戶端 hello 回應中傳回的位元組。 |
| ConfigChangeType |ConfigurationChange |變更的類別 (例如，WindowsServices/Software)。 |
| ChangeCategory |ConfigurationChange |Hello 變更 （已修改/新增/移除） 類別。 |
| SoftwareType |ConfigurationChange |軟體的類型 (更新/應用程式)。 |
| SoftwareName |ConfigurationChange |Hello 軟體 （僅適用 toosoftware 變更） 的名稱。 |
| 發佈者 |ConfigurationChange |發佈 hello 軟體 （僅適用 toosoftware 變更） 供應商。 |
| SvcChangeType |ConfigurationChange |已套用在 Windows 服務的變更類型 (State/StartupType/Path/ServiceAccount)。 這是適用於 tooWindows 服務變更。 |
| SvcDisplayName |ConfigurationChange |已變更的 hello 服務顯示名稱。 |
| SvcName |ConfigurationChange |已變更的 hello 服務的名稱。 |
| SvcState |ConfigurationChange |Hello 服務新 （目前） 狀態。 |
| SvcPreviousState |ConfigurationChange |上一個已知 hello 服務 （僅適用於服務狀態變更） 的狀態。 |
| SvcStartupType |ConfigurationChange |服務啟動類型。 |
| SvcPreviousStartupType |ConfigurationChange |上一個服務啟動類型 (僅適用於服務啟動類型變更時)。 |
| SvcAccount |ConfigurationChange |服務帳戶。 |
| SvcPreviousAccount |ConfigurationChange |先前的服務帳戶 (僅適用於服務帳戶變更時)。 |
| SvcPath |ConfigurationChange |路徑 toohello 可執行檔的 hello Windows 服務。 |
| SvcPreviousPath |ConfigurationChange |上一個 hello hello （僅適用於其變更） 的 Windows 服務的可執行檔的路徑。 |
| SvcDescription |ConfigurationChange |Hello 服務的描述。 |
| 上一步 |ConfigurationChange |此軟體先前的狀態 (已安裝/未安裝/上一個版本)。 |
| Current |ConfigurationChange |此軟體最新的狀態 (已安裝/未安裝/上一個版本)。 |

## <a name="next-steps"></a>後續步驟
如需記錄搜尋的其他資訊：

* 讓您熟悉[記錄搜尋](log-analytics-log-searches.md)tooview 詳細解決方案所收集的資訊。
* 使用[記錄分析中的自訂欄位](log-analytics-custom-fields.md)tooextend 記錄搜尋。
