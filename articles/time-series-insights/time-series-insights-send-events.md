---
title: "aaaSend 事件 tooAzure 時間數列 Insights 環境 |Microsoft 文件"
description: "本教學課程涵蓋 hello 步驟 toopush 事件 tooyour 時間數列 Insights 環境"
keywords: 
services: tsi
documentationcenter: 
author: venkatgct
manager: jhubbard
editor: 
ms.assetid: 
ms.service: tsi
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/21/2017
ms.author: venkatja
ms.openlocfilehash: dbccc23f61351a0033cd48c1a02fb3841b45d560
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="send-events-tooa-time-series-insights-environment-using-event-hub"></a>傳送事件 tooa 時間數列 Insights 環境中使用事件中樞

本教學課程說明如何 toocreate 和設定事件中樞，並執行範例應用程式 toopush 事件。 如果您現有的事件中樞內含 JSON 格式的事件，請跳過本教學課程，並在 [Time Series Insights](https://insights.timeseries.azure.com) 檢視您的環境。

## <a name="configure-an-event-hub"></a>設定事件中樞
1. toocreate 事件中心，請依照指示執行 hello 事件中心[文件](https://docs.microsoft.com/azure/event-hubs/event-hubs-create)。

2. 確定您已建立專供 Time Series Insights 事件來源使用的取用者群組。

  > [!IMPORTANT]
  > 確定任何其他服務 (例如串流分析作業或其他 Time Series Insights 環境) 均未使用此取用者群組。 如果取用者群組由其他服務，讀取作業造成負面影響此環境並 hello 其他服務。 如果您使用 「 $Default"作為 hello 取用者群組，可能導致 toopotential 重複使用其他讀取器。

  ![選取事件中樞取用者群組](media/send-events/consumer-group.png)

3. 在 hello 事件中樞內，建立 「 MySendPolicy"也就是使用的 toosend hello csharp 範例中的事件。

  ![選取 [共用存取原則]，然後按一下 [新增] 按鈕](media/send-events/shared-access-policy.png)  

  ![新增共用存取原則](media/send-events/shared-access-policy-2.png)  

## <a name="create-time-series-insights-event-source"></a>建立 Time Series Insights 事件來源
1. 如果您尚未建立事件來源，請遵循[這些指示](time-series-insights-add-event-source.md)toocreate 事件來源。

2. 為 hello 時間戳記屬性名稱指定"deviceTimestamp"– 此屬性作為 hello hello csharp 範例中的實際時間戳記。 hello 時間戳記屬性名稱會區分大小寫，且值必須遵照 hello 格式__yyyy-MM-Yyyy-mm-ddthh。SS'.'FFFFFFFK__傳送 JSON tooevent 集線器時。 如果 hello 屬性不存在於 hello 事件，然後 hello 事件中樞加入佇列的時間會使用。

  ![建立事件來源](media/send-events/event-source-1.png)

## <a name="sample-code-toopush-events"></a>範例程式碼 toopush 事件
1. 移 toohello 事件中樞原則 」 MySendPolicy 」，並使用 hello 原則機碼複製 hello 連接字串。

  ![複製 MySendPolicy 連接字串](media/send-events/sample-code-connection-string.png)

2. 執行下列程式碼的 hello hello 三個裝置的每個的 toosend 600 事件。 使用連接字串更新 `eventHubConnectionString`。

```csharp
using System;
using System.Collections.Generic;
using System.Globalization;
using System.IO;
using Microsoft.ServiceBus.Messaging;

namespace Microsoft.Rdx.DataGenerator
{
    internal class Program
    {
        private static void Main(string[] args)
        {
            var from = new DateTime(2017, 4, 20, 15, 0, 0, DateTimeKind.Utc);
            Random r = new Random();
            const int numberOfEvents = 600;

            var deviceIds = new[] { "device1", "device2", "device3" };

            var events = new List<string>();
            for (int i = 0; i < numberOfEvents; ++i)
            {
                for (int device = 0; device < deviceIds.Length; ++device)
                {
                    // Generate event and serialize as JSON object:
                    // { "deviceTimestamp": "utc timestamp", "deviceId": "guid", "value": 123.456 }
                    events.Add(
                        String.Format(
                            CultureInfo.InvariantCulture,
                            @"{{ ""deviceTimestamp"": ""{0}"", ""deviceId"": ""{1}"", ""value"": {2} }}",
                            (from + TimeSpan.FromSeconds(i * 30)).ToString("o"),
                            deviceIds[device],
                            r.NextDouble()));
                }
            }

            // Create event hub connection.
            var eventHubConnectionString = @"Endpoint=sb://...";
            var eventHubClient = EventHubClient.CreateFromConnectionString(eventHubConnectionString);

            using (var ms = new MemoryStream())
            using (var sw = new StreamWriter(ms))
            {
                // Wrap events into JSON array:
                sw.Write("[");
                for (int i = 0; i < events.Count; ++i)
                {
                    if (i > 0)
                    {
                        sw.Write(',');
                    }
                    sw.Write(events[i]);
                }
                sw.Write("]");

                sw.Flush();
                ms.Position = 0;

                // Send JSON tooevent hub.
                EventData eventData = new EventData(ms);
                eventHubClient.Send(eventData);
            }
        }
    }
}

```
## <a name="supported-json-shapes"></a>支援的 JSON 樣貌
### <a name="sample-1"></a>範例 1

#### <a name="input"></a>輸入

簡單的 JSON 物件。

```json
{
    "id":"device1",
    "timestamp":"2016-01-08T01:08:00Z"
}
```
#### <a name="output---1-event"></a>輸出 - 1 個事件

|id|timestamp|
|--------|---------------|
|device1|2016-01-08T01:08:00Z|

### <a name="sample-2"></a>範例 2

#### <a name="input"></a>輸入
具有兩個 JSON 物件的 JSON 陣列。 已轉換的 tooan 事件是每個 JSON 物件。
```json
[
    {
        "id":"device1",
        "timestamp":"2016-01-08T01:08:00Z"
    },
    {
        "id":"device2",
        "timestamp":"2016-01-17T01:17:00Z"
    }
]
```
#### <a name="output---2-events"></a>輸出 - 2 個事件

|id|timestamp|
|--------|---------------|
|device1|2016-01-08T01:08:00Z|
|device2|2016-01-08T01:17:00Z|
### <a name="sample-3"></a>範例 3

#### <a name="input"></a>輸入

具有巢狀 JSON 陣列的 JSON 物件，此陣列中包含兩個 JSON 物件。
```json
{
    "location":"WestUs",
    "events":[
        {
            "id":"device1",
            "timestamp":"2016-01-08T01:08:00Z"
        },
        {
            "id":"device2",
            "timestamp":"2016-01-17T01:17:00Z"
        }
    ]
}

```
#### <a name="output---2-events"></a>輸出 - 2 個事件
請注意 hello 屬性 「 位置 」 會透過 tooeach hello 事件的複製。

|location|events.id|events.timestamp|
|--------|---------------|----------------------|
|WestUs|device1|2016-01-08T01:08:00Z|
|WestUs|device2|2016-01-08T01:17:00Z|

### <a name="sample-4"></a>範例 4

#### <a name="input"></a>輸入

具有巢狀 JSON 陣列的 JSON 物件，此陣列中包含兩個 JSON 物件。 此輸入示範 hello 全域屬性可能會由 hello 複雜 JSON 物件。

```json
{
    "location":"WestUs",
    "manufacturer":{
        "name":"manufacturer1",
        "location":"EastUs"
    },
    "events":[
        {
            "id":"device1",
            "timestamp":"2016-01-08T01:08:00Z",
            "data":{
                "type":"pressure",
                "units":"psi",
                "value":108.09
            }
        },
        {
            "id":"device2",
            "timestamp":"2016-01-17T01:17:00Z",
            "data":{
                "type":"vibration",
                "units":"abs G",
                "value":217.09
            }
        }
    ]
}
```
#### <a name="output---2-events"></a>輸出 - 2 個事件

|location|manufacturer.name|manufacturer.location|events.id|events.timestamp|events.data.type|events.data.units|events.data.value|
|---|---|---|---|---|---|---|---|
|WestUs|manufacturer1|EastUs|device1|2016-01-08T01:08:00Z|pressure|psi|108.09|
|WestUs|manufacturer1|EastUs|device2|2016-01-08T01:17:00Z|vibration|abs G|217.09|

## <a name="next-steps"></a>後續步驟

* 在 [Time Series Insights 入口網站](https://insights.timeseries.azure.com)中檢視您的環境
