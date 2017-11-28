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
# <a name="send-events-tooa-time-series-insights-environment-using-event-hub"></a><span data-ttu-id="dd558-103">傳送事件 tooa 時間數列 Insights 環境中使用事件中樞</span><span class="sxs-lookup"><span data-stu-id="dd558-103">Send events tooa Time Series Insights environment using event hub</span></span>

<span data-ttu-id="dd558-104">本教學課程說明如何 toocreate 和設定事件中樞，並執行範例應用程式 toopush 事件。</span><span class="sxs-lookup"><span data-stu-id="dd558-104">This tutorial explains how toocreate and configure event hub and run a sample application toopush events.</span></span> <span data-ttu-id="dd558-105">如果您現有的事件中樞內含 JSON 格式的事件，請跳過本教學課程，並在 [Time Series Insights](https://insights.timeseries.azure.com) 檢視您的環境。</span><span class="sxs-lookup"><span data-stu-id="dd558-105">If you have an existing event hub with events in JSON format, skip this tutorial and view your environment in [time series insights](https://insights.timeseries.azure.com).</span></span>

## <a name="configure-an-event-hub"></a><span data-ttu-id="dd558-106">設定事件中樞</span><span class="sxs-lookup"><span data-stu-id="dd558-106">Configure an event hub</span></span>
1. <span data-ttu-id="dd558-107">toocreate 事件中心，請依照指示執行 hello 事件中心[文件](https://docs.microsoft.com/azure/event-hubs/event-hubs-create)。</span><span class="sxs-lookup"><span data-stu-id="dd558-107">toocreate an event hub, follow instructions from hello Event Hub [documentation](https://docs.microsoft.com/azure/event-hubs/event-hubs-create).</span></span>

2. <span data-ttu-id="dd558-108">確定您已建立專供 Time Series Insights 事件來源使用的取用者群組。</span><span class="sxs-lookup"><span data-stu-id="dd558-108">Make sure you create a consumer group that is used exclusively by your Time Series Insights event source.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="dd558-109">確定任何其他服務 (例如串流分析作業或其他 Time Series Insights 環境) 均未使用此取用者群組。</span><span class="sxs-lookup"><span data-stu-id="dd558-109">Make sure this consumer group is not used by any other service (such as Stream Analytics job or another Time Series Insights environment).</span></span> <span data-ttu-id="dd558-110">如果取用者群組由其他服務，讀取作業造成負面影響此環境並 hello 其他服務。</span><span class="sxs-lookup"><span data-stu-id="dd558-110">If consumer group is used by other services, read operation is negatively affected for this environment and hello other services.</span></span> <span data-ttu-id="dd558-111">如果您使用 「 $Default"作為 hello 取用者群組，可能導致 toopotential 重複使用其他讀取器。</span><span class="sxs-lookup"><span data-stu-id="dd558-111">If you are using “$Default” as hello consumer group, it could lead toopotential reuse by other readers.</span></span>

  ![選取事件中樞取用者群組](media/send-events/consumer-group.png)

3. <span data-ttu-id="dd558-113">在 hello 事件中樞內，建立 「 MySendPolicy"也就是使用的 toosend hello csharp 範例中的事件。</span><span class="sxs-lookup"><span data-stu-id="dd558-113">On hello event hub, create “MySendPolicy” that is used toosend events in hello csharp sample.</span></span>

  ![選取 [共用存取原則]，然後按一下 [新增] 按鈕](media/send-events/shared-access-policy.png)  

  ![新增共用存取原則](media/send-events/shared-access-policy-2.png)  

## <a name="create-time-series-insights-event-source"></a><span data-ttu-id="dd558-116">建立 Time Series Insights 事件來源</span><span class="sxs-lookup"><span data-stu-id="dd558-116">Create Time Series Insights event source</span></span>
1. <span data-ttu-id="dd558-117">如果您尚未建立事件來源，請遵循[這些指示](time-series-insights-add-event-source.md)toocreate 事件來源。</span><span class="sxs-lookup"><span data-stu-id="dd558-117">If you haven't created an event source, follow [these instructions](time-series-insights-add-event-source.md) toocreate an event source.</span></span>

2. <span data-ttu-id="dd558-118">為 hello 時間戳記屬性名稱指定"deviceTimestamp"– 此屬性作為 hello hello csharp 範例中的實際時間戳記。</span><span class="sxs-lookup"><span data-stu-id="dd558-118">Specify “deviceTimestamp” as hello timestamp property name – this property is used as hello actual timestamp in hello csharp sample.</span></span> <span data-ttu-id="dd558-119">hello 時間戳記屬性名稱會區分大小寫，且值必須遵照 hello 格式__yyyy-MM-Yyyy-mm-ddthh。SS'.'FFFFFFFK__傳送 JSON tooevent 集線器時。</span><span class="sxs-lookup"><span data-stu-id="dd558-119">hello timestamp property name is case-sensitive and values must follow hello format __yyyy-MM-ddTHH:mm:ss.FFFFFFFK__ when sent as JSON tooevent hub.</span></span> <span data-ttu-id="dd558-120">如果 hello 屬性不存在於 hello 事件，然後 hello 事件中樞加入佇列的時間會使用。</span><span class="sxs-lookup"><span data-stu-id="dd558-120">If hello property does not exist in hello event, then hello event hub enqueued time is used.</span></span>

  ![建立事件來源](media/send-events/event-source-1.png)

## <a name="sample-code-toopush-events"></a><span data-ttu-id="dd558-122">範例程式碼 toopush 事件</span><span class="sxs-lookup"><span data-stu-id="dd558-122">Sample code toopush events</span></span>
1. <span data-ttu-id="dd558-123">移 toohello 事件中樞原則 」 MySendPolicy 」，並使用 hello 原則機碼複製 hello 連接字串。</span><span class="sxs-lookup"><span data-stu-id="dd558-123">Go toohello event hub policy “MySendPolicy” and copy hello connection string with hello policy key.</span></span>

  ![複製 MySendPolicy 連接字串](media/send-events/sample-code-connection-string.png)

2. <span data-ttu-id="dd558-125">執行下列程式碼的 hello hello 三個裝置的每個的 toosend 600 事件。</span><span class="sxs-lookup"><span data-stu-id="dd558-125">Run hello following code that toosend 600 events per each of hello three devices.</span></span> <span data-ttu-id="dd558-126">使用連接字串更新 `eventHubConnectionString`。</span><span class="sxs-lookup"><span data-stu-id="dd558-126">Update `eventHubConnectionString` with your connection string.</span></span>

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
## <a name="supported-json-shapes"></a><span data-ttu-id="dd558-127">支援的 JSON 樣貌</span><span class="sxs-lookup"><span data-stu-id="dd558-127">Supported JSON shapes</span></span>
### <a name="sample-1"></a><span data-ttu-id="dd558-128">範例 1</span><span class="sxs-lookup"><span data-stu-id="dd558-128">Sample 1</span></span>

#### <a name="input"></a><span data-ttu-id="dd558-129">輸入</span><span class="sxs-lookup"><span data-stu-id="dd558-129">Input</span></span>

<span data-ttu-id="dd558-130">簡單的 JSON 物件。</span><span class="sxs-lookup"><span data-stu-id="dd558-130">A simple JSON object.</span></span>

```json
{
    "id":"device1",
    "timestamp":"2016-01-08T01:08:00Z"
}
```
#### <a name="output---1-event"></a><span data-ttu-id="dd558-131">輸出 - 1 個事件</span><span class="sxs-lookup"><span data-stu-id="dd558-131">Output - 1 event</span></span>

|<span data-ttu-id="dd558-132">id</span><span class="sxs-lookup"><span data-stu-id="dd558-132">id</span></span>|<span data-ttu-id="dd558-133">timestamp</span><span class="sxs-lookup"><span data-stu-id="dd558-133">timestamp</span></span>|
|--------|---------------|
|<span data-ttu-id="dd558-134">device1</span><span class="sxs-lookup"><span data-stu-id="dd558-134">device1</span></span>|<span data-ttu-id="dd558-135">2016-01-08T01:08:00Z</span><span class="sxs-lookup"><span data-stu-id="dd558-135">2016-01-08T01:08:00Z</span></span>|

### <a name="sample-2"></a><span data-ttu-id="dd558-136">範例 2</span><span class="sxs-lookup"><span data-stu-id="dd558-136">Sample 2</span></span>

#### <a name="input"></a><span data-ttu-id="dd558-137">輸入</span><span class="sxs-lookup"><span data-stu-id="dd558-137">Input</span></span>
<span data-ttu-id="dd558-138">具有兩個 JSON 物件的 JSON 陣列。</span><span class="sxs-lookup"><span data-stu-id="dd558-138">A JSON array with two JSON objects.</span></span> <span data-ttu-id="dd558-139">已轉換的 tooan 事件是每個 JSON 物件。</span><span class="sxs-lookup"><span data-stu-id="dd558-139">Each JSON object will be converted tooan event.</span></span>
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
#### <a name="output---2-events"></a><span data-ttu-id="dd558-140">輸出 - 2 個事件</span><span class="sxs-lookup"><span data-stu-id="dd558-140">Output - 2 Events</span></span>

|<span data-ttu-id="dd558-141">id</span><span class="sxs-lookup"><span data-stu-id="dd558-141">id</span></span>|<span data-ttu-id="dd558-142">timestamp</span><span class="sxs-lookup"><span data-stu-id="dd558-142">timestamp</span></span>|
|--------|---------------|
|<span data-ttu-id="dd558-143">device1</span><span class="sxs-lookup"><span data-stu-id="dd558-143">device1</span></span>|<span data-ttu-id="dd558-144">2016-01-08T01:08:00Z</span><span class="sxs-lookup"><span data-stu-id="dd558-144">2016-01-08T01:08:00Z</span></span>|
|<span data-ttu-id="dd558-145">device2</span><span class="sxs-lookup"><span data-stu-id="dd558-145">device2</span></span>|<span data-ttu-id="dd558-146">2016-01-08T01:17:00Z</span><span class="sxs-lookup"><span data-stu-id="dd558-146">2016-01-08T01:17:00Z</span></span>|
### <a name="sample-3"></a><span data-ttu-id="dd558-147">範例 3</span><span class="sxs-lookup"><span data-stu-id="dd558-147">Sample 3</span></span>

#### <a name="input"></a><span data-ttu-id="dd558-148">輸入</span><span class="sxs-lookup"><span data-stu-id="dd558-148">Input</span></span>

<span data-ttu-id="dd558-149">具有巢狀 JSON 陣列的 JSON 物件，此陣列中包含兩個 JSON 物件。</span><span class="sxs-lookup"><span data-stu-id="dd558-149">A JSON object with a nested JSON array containing two JSON objects.</span></span>
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
#### <a name="output---2-events"></a><span data-ttu-id="dd558-150">輸出 - 2 個事件</span><span class="sxs-lookup"><span data-stu-id="dd558-150">Output - 2 Events</span></span>
<span data-ttu-id="dd558-151">請注意 hello 屬性 「 位置 」 會透過 tooeach hello 事件的複製。</span><span class="sxs-lookup"><span data-stu-id="dd558-151">Note that hello property "location" is copied over tooeach of hello event.</span></span>

|<span data-ttu-id="dd558-152">location</span><span class="sxs-lookup"><span data-stu-id="dd558-152">location</span></span>|<span data-ttu-id="dd558-153">events.id</span><span class="sxs-lookup"><span data-stu-id="dd558-153">events.id</span></span>|<span data-ttu-id="dd558-154">events.timestamp</span><span class="sxs-lookup"><span data-stu-id="dd558-154">events.timestamp</span></span>|
|--------|---------------|----------------------|
|<span data-ttu-id="dd558-155">WestUs</span><span class="sxs-lookup"><span data-stu-id="dd558-155">WestUs</span></span>|<span data-ttu-id="dd558-156">device1</span><span class="sxs-lookup"><span data-stu-id="dd558-156">device1</span></span>|<span data-ttu-id="dd558-157">2016-01-08T01:08:00Z</span><span class="sxs-lookup"><span data-stu-id="dd558-157">2016-01-08T01:08:00Z</span></span>|
|<span data-ttu-id="dd558-158">WestUs</span><span class="sxs-lookup"><span data-stu-id="dd558-158">WestUs</span></span>|<span data-ttu-id="dd558-159">device2</span><span class="sxs-lookup"><span data-stu-id="dd558-159">device2</span></span>|<span data-ttu-id="dd558-160">2016-01-08T01:17:00Z</span><span class="sxs-lookup"><span data-stu-id="dd558-160">2016-01-08T01:17:00Z</span></span>|

### <a name="sample-4"></a><span data-ttu-id="dd558-161">範例 4</span><span class="sxs-lookup"><span data-stu-id="dd558-161">Sample 4</span></span>

#### <a name="input"></a><span data-ttu-id="dd558-162">輸入</span><span class="sxs-lookup"><span data-stu-id="dd558-162">Input</span></span>

<span data-ttu-id="dd558-163">具有巢狀 JSON 陣列的 JSON 物件，此陣列中包含兩個 JSON 物件。</span><span class="sxs-lookup"><span data-stu-id="dd558-163">A JSON object with a nested JSON array containing two JSON objects.</span></span> <span data-ttu-id="dd558-164">此輸入示範 hello 全域屬性可能會由 hello 複雜 JSON 物件。</span><span class="sxs-lookup"><span data-stu-id="dd558-164">This input demonstrates that hello global properties may be represented by hello complex JSON object.</span></span>

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
#### <a name="output---2-events"></a><span data-ttu-id="dd558-165">輸出 - 2 個事件</span><span class="sxs-lookup"><span data-stu-id="dd558-165">Output - 2 Events</span></span>

|<span data-ttu-id="dd558-166">location</span><span class="sxs-lookup"><span data-stu-id="dd558-166">location</span></span>|<span data-ttu-id="dd558-167">manufacturer.name</span><span class="sxs-lookup"><span data-stu-id="dd558-167">manufacturer.name</span></span>|<span data-ttu-id="dd558-168">manufacturer.location</span><span class="sxs-lookup"><span data-stu-id="dd558-168">manufacturer.location</span></span>|<span data-ttu-id="dd558-169">events.id</span><span class="sxs-lookup"><span data-stu-id="dd558-169">events.id</span></span>|<span data-ttu-id="dd558-170">events.timestamp</span><span class="sxs-lookup"><span data-stu-id="dd558-170">events.timestamp</span></span>|<span data-ttu-id="dd558-171">events.data.type</span><span class="sxs-lookup"><span data-stu-id="dd558-171">events.data.type</span></span>|<span data-ttu-id="dd558-172">events.data.units</span><span class="sxs-lookup"><span data-stu-id="dd558-172">events.data.units</span></span>|<span data-ttu-id="dd558-173">events.data.value</span><span class="sxs-lookup"><span data-stu-id="dd558-173">events.data.value</span></span>|
|---|---|---|---|---|---|---|---|
|<span data-ttu-id="dd558-174">WestUs</span><span class="sxs-lookup"><span data-stu-id="dd558-174">WestUs</span></span>|<span data-ttu-id="dd558-175">manufacturer1</span><span class="sxs-lookup"><span data-stu-id="dd558-175">manufacturer1</span></span>|<span data-ttu-id="dd558-176">EastUs</span><span class="sxs-lookup"><span data-stu-id="dd558-176">EastUs</span></span>|<span data-ttu-id="dd558-177">device1</span><span class="sxs-lookup"><span data-stu-id="dd558-177">device1</span></span>|<span data-ttu-id="dd558-178">2016-01-08T01:08:00Z</span><span class="sxs-lookup"><span data-stu-id="dd558-178">2016-01-08T01:08:00Z</span></span>|<span data-ttu-id="dd558-179">pressure</span><span class="sxs-lookup"><span data-stu-id="dd558-179">pressure</span></span>|<span data-ttu-id="dd558-180">psi</span><span class="sxs-lookup"><span data-stu-id="dd558-180">psi</span></span>|<span data-ttu-id="dd558-181">108.09</span><span class="sxs-lookup"><span data-stu-id="dd558-181">108.09</span></span>|
|<span data-ttu-id="dd558-182">WestUs</span><span class="sxs-lookup"><span data-stu-id="dd558-182">WestUs</span></span>|<span data-ttu-id="dd558-183">manufacturer1</span><span class="sxs-lookup"><span data-stu-id="dd558-183">manufacturer1</span></span>|<span data-ttu-id="dd558-184">EastUs</span><span class="sxs-lookup"><span data-stu-id="dd558-184">EastUs</span></span>|<span data-ttu-id="dd558-185">device2</span><span class="sxs-lookup"><span data-stu-id="dd558-185">device2</span></span>|<span data-ttu-id="dd558-186">2016-01-08T01:17:00Z</span><span class="sxs-lookup"><span data-stu-id="dd558-186">2016-01-08T01:17:00Z</span></span>|<span data-ttu-id="dd558-187">vibration</span><span class="sxs-lookup"><span data-stu-id="dd558-187">vibration</span></span>|<span data-ttu-id="dd558-188">abs G</span><span class="sxs-lookup"><span data-stu-id="dd558-188">abs G</span></span>|<span data-ttu-id="dd558-189">217.09</span><span class="sxs-lookup"><span data-stu-id="dd558-189">217.09</span></span>|

## <a name="next-steps"></a><span data-ttu-id="dd558-190">後續步驟</span><span class="sxs-lookup"><span data-stu-id="dd558-190">Next steps</span></span>

* <span data-ttu-id="dd558-191">在 [Time Series Insights 入口網站](https://insights.timeseries.azure.com)中檢視您的環境</span><span class="sxs-lookup"><span data-stu-id="dd558-191">View your environment in [Time Series Insights Portal](https://insights.timeseries.azure.com)</span></span>
