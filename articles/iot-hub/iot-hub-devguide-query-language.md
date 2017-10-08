---
title: "aaaUnderstand hello Azure IoT 中樞的查詢語言 |Microsoft 文件"
description: "開發人員指南-使用 tooretrieve 裝置雙和作業相關資訊從 IoT 中樞 hello 類似 SQL 的 IoT 中樞查詢語言的描述。"
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: 851a9ed3-b69e-422e-8a5d-1d79f91ddf15
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/17
ms.author: elioda
ms.openlocfilehash: 01a7c8ffdf44c6c27b834739d02c8fef1dd3d3fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="reference---iot-hub-query-language-for-device-twins-jobs-and-message-routing"></a>參考 - 裝置對應項、作業和訊息路由的 IoT 中樞查詢語言

IoT 中樞提供功能強大的類似 SQL 的語言 tooretrieve 資訊有關[裝置雙][ lnk-twins]和[作業][lnk-jobs]，和[訊息路由][lnk-devguide-messaging-routes]。 本文提供︰

* Hello IoT 中樞的查詢語言，簡介 toohello 主要功能和
* hello 詳細 hello 語言的描述。

## <a name="get-started-with-device-twin-queries"></a>開始使用裝置對應項查詢
[裝置對應項][lnk-twins]可以包含標籤和屬性形式的任意 JSON 物件。 IoT 中樞可讓您 tooquery 裝置雙為單一的 JSON 文件，其中包含所有裝置的兩個資訊。
比方說，假設您的 IoT 中樞裝置雙具有下列結構的 hello:

```json
{
    "deviceId": "myDeviceId",
    "etag": "AAAAAAAAAAc=",
    "tags": {
        "location": {
            "region": "US",
            "plant": "Redmond43"
        }
    },
    "properties": {
        "desired": {
            "telemetryConfig": {
                "configId": "db00ebf5-eeeb-42be-86a1-458cccb69e57",
                "sendFrequencyInSecs": 300
            },
            "$metadata": {
            ...
            },
            "$version": 4
        },
        "reported": {
            "connectivity": {
                "type": "cellular"
            },
            "telemetryConfig": {
                "configId": "db00ebf5-eeeb-42be-86a1-458cccb69e57",
                "sendFrequencyInSecs": 300,
                "status": "Success"
            },
            "$metadata": {
            ...
            },
            "$version": 7
        }
    }
}
```

IoT 中樞公開做為文件集合，稱為 hello 裝置雙**裝置**。
因此 hello 下列查詢會擷取整組裝置雙 hello:

```sql
SELECT * FROM devices
```

> [!NOTE]
> [Azure IoT SDK][lnk-hub-sdks] 支援將大型結果分頁。

IoT 中樞可讓您 tooretrieve 裝置雙使用任意的條件進行篩選。 例如，

```sql
SELECT * FROM devices
WHERE tags.location.region = 'US'
```

擷取與 hello hello 裝置雙**location.region**標記設定得**美國**。
布林運算子和算術比較也受到支援，例如

```sql
SELECT * FROM devices
WHERE tags.location.region = 'US'
    AND properties.reported.telemetryConfig.sendFrequencyInSecs >= 60
```

擷取所有的裝置雙位於 hello 我們設定 toosend 遙測小於通常每隔一分鐘。 為了方便起見，也很可能 toouse 陣列常數以 hello **IN**和**‧ 尼恩之**（不能在） 運算子。 例如，

```sql
SELECT * FROM devices
WHERE properties.reported.connectivity IN ['wired', 'wifi']
```

會擷取所有報告使用 WiFi 或有線連線能力的裝置對應項。 它是經常需要 tooidentify 包含特定屬性的所有裝置雙。 IoT 中樞支援 hello 函式，`is_defined()`針對此目的。 例如，

```SQL
SELECT * FROM devices
WHERE is_defined(properties.reported.connectivity)
```

擷取所有的裝置雙定義 hello`connectivity`報告屬性。 請參閱 toohello [WHERE 子句][ lnk-query-where] hello 篩選功能 hello 完整參考一節。

群組和彙總也受到支援。 例如，

```sql
SELECT properties.reported.telemetryConfig.status AS status,
    COUNT() AS numberOfDevices
FROM devices
GROUP BY properties.reported.telemetryConfig.status
```

傳回每個遙測設定狀態的 hello 裝置 hello 計數。

```json
[
    {
        "numberOfDevices": 3,
        "status": "Success"
    },
    {
        "numberOfDevices": 2,
        "status": "Pending"
    },
    {
        "numberOfDevices": 1,
        "status": "Error"
    }
]
```

hello 前述範例說明其中三個裝置會回報成功設定組態、 兩個仍會套用 hello 組態，以及其中一個報告了錯誤的情況。

### <a name="c-example"></a>C# 範例
hello 查詢功能由 hello [C# 服務 SDK] [ lnk-hub-sdks]在 hello **RegistryManager**類別。
以下是簡單查詢的範例︰

```csharp
var query = registryManager.CreateQuery("SELECT * FROM devices", 100);
while (query.HasMoreResults)
{
    var page = await query.GetNextAsTwinAsync();
    foreach (var twin in page)
    {
        // do work on twin object
    }
}
```

請注意如何 hello**查詢**物件具現化 （向上 too1000)，頁面大小，然後擷取多個頁面，透過呼叫 hello **GetNextAsTwinAsync**方法多次。
請注意該 hello 查詢物件會公開多個**下一步\***、 根據 hello 還原序列化選項所需的 hello 查詢，例如裝置的兩個或工作物件或純文字的 JSON toobe 使用投射時使用。

### <a name="nodejs-example"></a>Node.js 範例
hello 查詢功能由 hello [Azure IoT 服務 SDK for Node.js] [ lnk-hub-sdks]在 hello**登錄**物件。
以下是簡單查詢的範例︰

```nodejs
var query = registry.createQuery('SELECT * FROM devices', 100);
var onResults = function(err, results) {
    if (err) {
        console.error('Failed toofetch hello results: ' + err.message);
    } else {
        // Do something with hello results
        results.forEach(function(twin) {
            console.log(twin.deviceId);
        });

        if (query.hasMoreResults) {
            query.nextAsTwin(onResults);
        }
    }
};
query.nextAsTwin(onResults);
```

請注意如何 hello**查詢**物件具現化 （向上 too1000)，頁面大小，然後擷取多個頁面，透過呼叫 hello **nextAsTwin**方法多次。
請注意該 hello 查詢物件會公開多個**下一步\***、 根據 hello 還原序列化選項所需的 hello 查詢，例如裝置的兩個或工作物件或純文字的 JSON toobe 使用投射時使用。

### <a name="limitations"></a>限制
> [!IMPORTANT]
> 查詢結果中裝置雙有幾分鐘的延遲尊重 toohello 最新的值。 如果查詢個別裝置雙依識別碼，它一律為偏好 toouse hello 擷取裝置的兩個 API，它一律包含 hello 最新的值，而且具有更高的節流限制。

目前僅支援在基本類型 (沒有物件) 之間進行比較，例如 `... WHERE properties.desired.config = properties.reported.config` 只會在這些屬性具有基本值時才受到支援。

## <a name="get-started-with-jobs-queries"></a>開始使用作業查詢
[作業][ lnk-jobs]提供方式 tooexecute 集合的裝置上的作業。 每個裝置的兩個包含的 hello 工作都屬於呼叫集合中的 hello 資訊**作業**。
在邏輯上，

```json
{
    "deviceId": "myDeviceId",
    "etag": "AAAAAAAAAAc=",
    "tags": {
        ...
    },
    "properties": {
        ...
    },
    "jobs": [
        {
            "deviceId": "myDeviceId",
            "jobId": "myJobId",
            "jobType": "scheduleTwinUpdate",
            "status": "completed",
            "startTimeUtc": "2016-09-29T18:18:52.7418462",
            "endTimeUtc": "2016-09-29T18:20:52.7418462",
            "createdDateTimeUtc": "2016-09-29T18:18:56.7787107Z",
            "lastUpdatedDateTimeUtc": "2016-09-29T18:18:56.8894408Z",
            "outcome": {
                "deviceMethodResponse": null
            }
        },
        ...
    ]
}
```

目前，這個集合是可做為查詢**devices.jobs** hello IoT 中樞的查詢語言中。

> [!IMPORTANT]
> 目前，查詢裝置雙 （亦即，查詢包含 'FROM '的裝置） 時，會永遠不會傳回 hello 工作屬性。 此屬性只能使用 `FROM devices.jobs` 直接透過查詢來存取。
>
>

比方說，tooget 所有工作 （過去和排程） 會影響單一裝置，您可以都使用下列查詢的 hello:

```sql
SELECT * FROM devices.jobs
WHERE devices.jobs.deviceId = 'myDeviceId'
```

請注意如何此查詢提供 hello 裝置的特定狀態 （和可能 hello 直接方法回應） 的每個傳回的工作。
它也是可能 toofilter hello 中的所有物件屬性上的任意布林條件**devices.jobs**集合。
例如，下列查詢 hello:

```sql
SELECT * FROM devices.jobs
WHERE devices.jobs.deviceId = 'myDeviceId'
    AND devices.jobs.jobType = 'scheduleTwinUpdate'
    AND devices.jobs.status = 'completed'
    AND devices.jobs.createdTimeUtc > '2016-09-01'
```

會針對在 2016 年 9 月之後所建立的裝置 **myDeviceId** 擷取所有已完成的裝置對應項更新作業。

它也是可能 tooretrieve hello 每一裝置的結果，在單一作業。

```sql
SELECT * FROM devices.jobs
WHERE devices.jobs.jobId = 'myJobId'
```

### <a name="limitations"></a>限制
**devices.jobs** 上的查詢目前不支援︰

* 投影，因此只有 `SELECT *` 是可行的。
* 參考 toohello 裝置的兩個加法 toojob 屬性 （請參閱前面一節的 hello） 中的條件。
* 執行彙總，例如計數、平均、分組依據。

## <a name="get-started-with-device-to-cloud-message-routes-query-expressions"></a>開始使用裝置對雲端訊息路由查詢運算式

使用[裝置到雲端路由][lnk-devguide-messaging-routes]，您可以設定 toodispatch 裝置到雲端訊息 toodifferent 端點針對個別訊息評估的運算式為基礎的 IoT 中樞。

hello 路由[條件][ lnk-query-expressions]使用 hello 條件在兩個與工作的查詢中相同的 IoT 中樞查詢語言。 路由條件會評估 hello 訊息標頭和主體。 路由的查詢運算式可能只訊息標頭，只有 hello 訊息內文，或兩者訊息標頭和訊息主體。 IoT 中樞假設 hello 標頭和訊息本文的訂單 tooroute 訊息，特定的結構描述和 hello 下列各節描述所需 IoT 中樞 tooproperly 路由內容：

### <a name="routing-on-message-headers"></a>依據訊息標頭進行路由

IoT 中樞會假設採用下列的訊息標頭路由訊息的 JSON 表示法的 hello:

```json
{
    "$messageId": "",
    "$enqueuedTime": "",
    "$to": "",
    "$expiryTimeUtc": "",
    "$correlationId": "",
    "$userId": "",
    "$ack": "",
    "$connectionDeviceId": "",
    "$connectionDeviceGenerationId": "",
    "$connectionAuthMethod": "",
    "$content-type": "",
    "$content-encoding": "",

    "userProperty1": "",
    "userProperty2": ""
}
```

訊息系統屬性會加上 hello`'$'`符號。
使用者屬性則一律透過其名稱來存取。 如果使用者的屬性名稱不會 toocoincide 系統屬性 (例如`$to`)，將擷取 hello 使用者屬性，以 hello`$to`運算式。
您永遠可以存取使用方括號 hello 系統屬性`{}`： 例如，您可以使用 hello 運算式`{$to}`tooaccess hello 系統屬性`to`。 以方括弧括住的屬性名稱一律會擷取 hello 對應的系統屬性。

請記住，屬性名稱不區分大小寫。

> [!NOTE]
> 所有屬性皆為字串。 系統屬性，如述 hello[開發人員指南][lnk-devguide-messaging-format]，目前不是在查詢中的可用 toouse。
>

例如，如果您使用`messageType`屬性，您可能會想 tooroute，所有遙測 tooone 端點和所有警示 tooanother 端點。 您可以撰寫下列運算式 tooroute hello 遙測 hello:

```sql
messageType = 'telemetry'
```

並 hello 遵循運算式 tooroute hello 警示訊息：

```sql
messageType = 'alert'
```

也支援布林運算式和函式。 這項功能可讓您 toodistinguish 之間嚴重性層級，例如：

```sql
messageType = 'alerts' AND as_number(severity) <= 2
```

請參閱 toohello[運算式與條件][ lnk-query-expressions]一節，以 hello 完整清單支援的運算子和函式。

### <a name="routing-on-message-bodies"></a>依據訊息內文進行路由

IoT 中樞只路由根據訊息本文內容，如果 hello 訊息內文是正確格式的 JSON 編碼在 utf-8、 utf-16 或 utf-32。 您必須設定 hello 訊息內容型別的 hello 太`application/json`和 hello 內容編碼方式的 tooone hello 的 hello 訊息標頭 tooallow IoT 中樞 tooroute hello 訊息根據 hello 本文內容中支援 UTF-8 編碼方式。 如果任一 hello 標頭未指定，IoT 中樞將不會嘗試 tooevaluate 涉及 hello 主體針對 hello 訊息的任何查詢運算式。 如果您的訊息不是 JSON 訊息時，或 hello 訊息未指定 hello 內容類型和內容編碼方式，您可能仍然會使用根據 hello 訊息標頭 tooroute hello 訊息路由傳送的訊息。

您可以使用`$body`hello 查詢運算式 tooroute hello 訊息中。 您可以使用簡單的主體參考、 主體陣列參考或主體的多個參照 hello 查詢運算式中。 您的查詢運算式也可以將內文參考與訊息標頭參考合併。 例如，hello 下列都是有效的查詢運算式：

```sql
$body.message.Weather.Location.State = 'WA'
$body.Weather.HistoricalData[0].Month = 'Feb'
$body.Weather.Temperature = 50 AND $body.message.Weather.IsEnabled
length($body.Weather.Location.State) = 2
$body.Weather.Temperature = 50 AND Status = 'Active'
```

## <a name="basics-of-an-iot-hub-query"></a>IoT 中樞查詢的基本概念
每一個 IoT 中樞查詢都包含 SELECT 和 FROM 子句，以及選擇性的 WHERE 和 GROUP BY 子句。 每個查詢都會在 JSON 文件的集合上執行，例如裝置對應項。 hello FROM 子句指出 hello 反覆運算上的文件集合 toobe (**裝置**或**devices.jobs**)。 然後，hello 的 hello 才會套用子句中的篩選器。 彙總，hello 這個步驟的結果會以指定在 hello GROUP BY 子句分組，並針對每個群組，產生一個資料列 hello SELECT 子句中所指定。

```sql
SELECT <select_list>
FROM <from_specification>
[WHERE <filter_condition>]
[GROUP BY <group_specification>]
```

## <a name="from-clause"></a>FROM 子句
hello **< from_specification > 從**子句可指定只有兩個值：**從裝置**，tooquery 裝置雙，或**從 devices.jobs**，tooquery 作業每個裝置詳細資料。

## <a name="where-clause"></a>WHERE 子句
hello**其中 < filter_condition >**子句是選擇性的。 它會指定一或多個條件 hello 從集合中的 hello JSON 文件必須滿足 toobe 納入 hello 結果的一部分。 任何 JSON 文件都必須評估 hello 指定條件太"true"toobe 會包含在 hello 結果。

hello 允許一節所述條件[運算式和條件][lnk-query-expressions]。

## <a name="select-clause"></a>SELECT 子句
hello SELECT 子句 (**SELECT < select_list >**) 是必要項，指定從 hello 查詢會擷取哪些值。 它會指定 hello JSON 值 toobe 用 toogenerate 新 JSON 物件。
每個項目 hello hello FROM 集合的篩選 （及選擇性地群組） 的子集、 hello 投影階段會產生新的 JSON 物件，建構 hello hello SELECT 子句中指定的值。

以下是 hello 文法 hello SELECT 子句：

```
SELECT [TOP <max number>] <projection list>

<projection_list> ::=
    '*'
    | <projection_element> AS alias [, <projection_element> AS alias]+

<projection_element> :==
    attribute_name
    | <projection_element> '.' attribute_name
    | <aggregate>

<aggregate> :==
    count()
    | avg(<projection_element>)
    | sum(<projection_element>)
    | min(<projection_element>)
    | max(<projection_element>)
```

其中**attribute_name**參考 tooany hello 從集合中的 hello JSON 文件屬性。 SELECT 子句的一些範例可以在 hello[開始使用裝置的兩個查詢][ lnk-query-getstarted] > 一節。

與 **SELECT \*** 不同的選取範圍子句目前只支援在裝置對應項的彙總查詢中使用。

## <a name="group-by-clause"></a>GROUP BY 子句
hello **GROUP BY < group_specification >**子句是選擇性步驟，可以在之後 hello 篩選 hello 中 WHERE 子句，指定執行之前指定 hello 中的 hello 投影選取。 它會群組 hello 屬性值為基礎的文件。 這些群組是彙總使用的 toogenerate hello SELECT 子句中所指定的值。

使用 GROUP BY 的查詢範例如下︰

```sql
SELECT properties.reported.telemetryConfig.status AS status,
    COUNT() AS numberOfDevices
FROM devices
GROUP BY properties.reported.telemetryConfig.status
```

hello GROUP by 的正式語法是：

```
GROUP BY <group_by_element>
<group_by_element> :==
    attribute_name
    | < group_by_element > '.' attribute_name
```

其中**attribute_name**參考 tooany hello 從集合中的 hello JSON 文件屬性。

目前，hello GROUP BY 子句只能查詢時，支援裝置雙。

## <a name="expressions-and-conditions"></a>運算式和條件
概括而言，運算式：

* 評估 tooan JSON 型別 （例如布林值、 數字、 字串、 陣列或物件），執行個體和
* 定義處理來自 hello 裝置 JSON 文件與使用內建運算子和函數的常數。

*條件*是評估 tooa 布林值運算式。 不同於布林值的任何常數**true**會被視為**false** (包括**null**，**未定義**，任何物件或陣列的執行個體，任何字串，並清楚 hello 布林值**false**)。

hello 運算式的語法為：

```
<expression> ::=
    <constant> |
    attribute_name |
    <function_call> |
    <expression> binary_operator <expression> |
    <create_array_expression> |
    '(' <expression> ')'

<function_call> ::=
    <function_name> '(' expression ')'

<constant> ::=
    <undefined_constant>
    | <null_constant>
    | <number_constant>
    | <string_constant>
    | <array_constant>

<undefined_constant> ::= undefined
<null_constant> ::= null
<number_constant> ::= decimal_literal | hexadecimal_literal
<string_constant> ::= string_literal
<array_constant> ::= '[' <constant> [, <constant>]+ ']'
```

其中：

| 符號 | 定義 |
| --- | --- |
| attribute_name | 任何屬性的 hello JSON 文件以 hello **FROM**集合。 |
| binary_operator | Hello 中列出的任何二元運算子[運算子](#operators)> 一節。 |
| function_name| 任何函式列在 hello[函式](#functions)> 一節。 |
| decimal_literal |以小數點標記法表示的浮點數。 |
| hexadecimal_literal |Hello 字串所表示的數字 '0x' 後面接著十六進位數字的字串。 |
| string_literal |字串常值是由零個或多個 Unicode 字元序列或逸出序列所表示的 Unicode 字串。 字串常值會以單引號 (所有格符號：') 或雙引號 (引號：") 括起來。 允許的逸出︰`\'`、`\"`、`\\`、`\uXXXX` (適用於由 4 個十六進位數字所定義的 Unicode 字元)。 |

### <a name="operators"></a>運算子
支援下列運算子的 hello:

| 系列 | 運算子 |
| --- | --- |
| 算術 |+、-、*、/、% |
| 邏輯 |AND、OR、NOT |
| 比較 |=、!=、<、>、<=、>=、<> |

### <a name="functions"></a>Functions
當查詢雙和工作，才支援的 hello 函式為：

| 函式 | 說明 |
| -------- | ----------- |
| IS_DEFINED(property) | 傳回布林值，指出如果 hello 尚未指派屬性值 (包括`null`)。 |

在路由情況下，支援下列數學函式的 hello:

| 函式 | 說明 |
| -------- | ----------- |
| ABS(x) | 傳回 hello 絕對 （正） 值 hello 指定數值運算式。 |
| EXP(x) | 傳回的 hello hello 指數值指定數值運算式 (e ^ x)。 |
| POWER(x,y) | 傳回 hello hello 指定的值運算式 toohello 指定的冪 (x ^ y)。|
| SQUARE(x) | 傳回 hello 正方形 hello 的指定數字值。 |
| CEILING(x) | 傳回 hello 最小整數值大於或等於，hello 指定數值運算式。 |
| FLOOR(x) | 傳回小於 hello 最大整數 toohello 或等於指定數值運算式。 |
| SIGN(x) | 傳回 hello 正 (+ 1)、 零 (0)，或 hello 負 (-1) 號指定數值運算式。|
| SQRT(x) | 傳回 hello 正方形 hello 的指定數字值。 |

在路由情況下，支援下列型別檢查和轉換函式的 hello:

| 函式 | 說明 |
| -------- | ----------- |
| AS_NUMBER | 將轉換 hello 輸入的字串 tooa 數。 如果輸入是一個數字則為 `noop`；如果字串不是數字則為 `Undefined`。|
| IS_ARRAY | 傳回布林值，指出是否指定運算式的 hello hello 類型是陣列。 |
| IS_BOOL | 傳回布林值，指出是否 hello hello 類型指定的運算式是布林值。 |
| IS_DEFINED | 傳回布林值，指出如果 hello 尚未指派屬性值。 |
| IS_NULL | 傳回布林值，指出是否 hello hello 類型指定的運算式為 null。 |
| IS_NUMBER | 傳回布林值，指出是否 hello hello 類型指定的運算式是一個數字。 |
| IS_OBJECT | 傳回布林值，指出是否 hello hello 類型指定的運算式是一個 JSON 物件。 |
| IS_PRIMITIVE | 傳回布林值，指出是否 hello hello 類型指定運算式是基本型別 (字串、 布林值，數字或`null`)。 |
| IS_STRING | 傳回布林值，指出是否 hello hello 類型指定的運算式是字串。 |

在路由情況下，支援下列字串函數的 hello:

| 函式 | 說明 |
| -------- | ----------- |
| CONCAT(x, …) | 傳回字串 hello 因產生的串連兩個或多個字串值。 |
| LENGTH(x) | 傳回 hello 數目的 hello 字元指定的字串運算式。|
| LOWER(x) | 傳回將大寫字元資料 toolowercase 轉換後的字串運算式。 |
| UPPER(x) | 傳回將小寫字元資料 toouppercase 轉換後的字串運算式。 |
| SUBSTRING(string, start [, length]) | Hello 處開始的字串運算式的傳回屬於指定的字元以零為起始的位置，並繼續 toohello 指定長度或 toohello hello 字串的結尾。 |
| INDEX_OF(string, fragment) | 傳回開始 hello 內 hello 第一個指定的字串運算式，則為-1 hello 第二個字串運算式的第一次出現的位置，如果找不到 hello 字串 hello。|
| STARTS_WITH(x, y) | 傳回布林值，指出 hello 第一個字串運算式的開頭是否 hello 第二個。 |
| ENDS_WITH(x, y) | 傳回布林值，指出是否 hello 第一個字串運算式的結尾 hello 第二個。 |
| CONTAINS(x,y) | 傳回布林值，指出是否 hello 第一個字串運算式中第二個包含 hello。 |

## <a name="next-steps"></a>後續步驟
了解如何 tooexecute 查詢使用的應用程式中[Azure IoT Sdk][lnk-hub-sdks]。

[lnk-query-where]: iot-hub-devguide-query-language.md#where-clause
[lnk-query-expressions]: iot-hub-devguide-query-language.md#expressions-and-conditions
[lnk-query-getstarted]: iot-hub-devguide-query-language.md#get-started-with-device-twin-queries

[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-jobs]: iot-hub-devguide-jobs.md
[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
[lnk-devguide-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-devguide-messaging-routes]: iot-hub-devguide-messages-read-custom.md
[lnk-devguide-messaging-format]: iot-hub-devguide-messages-construct.md
[lnk-devguide-messaging-routes]: ./iot-hub-devguide-messages-read-custom.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
