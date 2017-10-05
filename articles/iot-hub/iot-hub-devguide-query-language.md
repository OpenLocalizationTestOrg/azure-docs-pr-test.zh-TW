---
title: "了解 Azure IoT 中樞查詢語言 | Microsoft Docs"
description: "開發人員指南 - 說明類似 SQL 的 IoT 中樞查詢語言，用於從 IoT 中樞擷取裝置對應項和作業的相關資訊。"
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
ms.openlocfilehash: a7650104eda58923558892f6f0f6666d16dbce28
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="reference---iot-hub-query-language-for-device-twins-jobs-and-message-routing"></a><span data-ttu-id="214df-103">參考 - 裝置對應項、作業和訊息路由的 IoT 中樞查詢語言</span><span class="sxs-lookup"><span data-stu-id="214df-103">Reference - IoT Hub query language for device twins, jobs, and message routing</span></span>

<span data-ttu-id="214df-104">IoT 中樞提供功能強大、類似 SQL 的語言，來擷取有關[裝置對應項][lnk-twins]、[作業][lnk-jobs]和[訊息路由][lnk-devguide-messaging-routes]的資訊。</span><span class="sxs-lookup"><span data-stu-id="214df-104">IoT Hub provides a powerful SQL-like language to retrieve information regarding [device twins][lnk-twins] and [jobs][lnk-jobs], and [message routing][lnk-devguide-messaging-routes].</span></span> <span data-ttu-id="214df-105">本文提供︰</span><span class="sxs-lookup"><span data-stu-id="214df-105">This article presents:</span></span>

* <span data-ttu-id="214df-106">IoT 中樞查詢語言主要功能的簡介，以及</span><span class="sxs-lookup"><span data-stu-id="214df-106">An introduction to the major features of the IoT Hub query language, and</span></span>
* <span data-ttu-id="214df-107">語言的詳細說明。</span><span class="sxs-lookup"><span data-stu-id="214df-107">The detailed description of the language.</span></span>

## <a name="get-started-with-device-twin-queries"></a><span data-ttu-id="214df-108">開始使用裝置對應項查詢</span><span class="sxs-lookup"><span data-stu-id="214df-108">Get started with device twin queries</span></span>
<span data-ttu-id="214df-109">[裝置對應項][lnk-twins]可以包含標籤和屬性形式的任意 JSON 物件。</span><span class="sxs-lookup"><span data-stu-id="214df-109">[Device twins][lnk-twins] can contain arbitrary JSON objects as both tags and properties.</span></span> <span data-ttu-id="214df-110">IoT 中樞可讓您以包含所有裝置對應項資訊的單一 JSON 文件形式查詢裝置對應項。</span><span class="sxs-lookup"><span data-stu-id="214df-110">IoT Hub enables you to query device twins as a single JSON document containing all device twin information.</span></span>
<span data-ttu-id="214df-111">比方說，假設您的 IoT 中樞裝置對應項有下列結構︰</span><span class="sxs-lookup"><span data-stu-id="214df-111">Assume, for instance, that your IoT hub device twins have the following structure:</span></span>

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

<span data-ttu-id="214df-112">IoT 中樞可以將裝置對應項公開為稱為**裝置**的文件集合。</span><span class="sxs-lookup"><span data-stu-id="214df-112">IoT Hub exposes the device twins as a document collection called **devices**.</span></span>
<span data-ttu-id="214df-113">因此，下列查詢會擷取整組裝置對應項︰</span><span class="sxs-lookup"><span data-stu-id="214df-113">So the following query retrieves the whole set of device twins:</span></span>

```sql
SELECT * FROM devices
```

> [!NOTE]
> <span data-ttu-id="214df-114">[Azure IoT SDK][lnk-hub-sdks] 支援將大型結果分頁。</span><span class="sxs-lookup"><span data-stu-id="214df-114">[Azure IoT SDKs][lnk-hub-sdks] support paging of large results.</span></span>

<span data-ttu-id="214df-115">IoT 中樞允許擷取使用任意條件進行的裝置對應項篩選。</span><span class="sxs-lookup"><span data-stu-id="214df-115">IoT Hub allows you to retrieve device twins filtering with arbitrary conditions.</span></span> <span data-ttu-id="214df-116">例如，</span><span class="sxs-lookup"><span data-stu-id="214df-116">For instance,</span></span>

```sql
SELECT * FROM devices
WHERE tags.location.region = 'US'
```

<span data-ttu-id="214df-117">會擷取 **location.region** 標籤設為 **US**的裝置對應項。</span><span class="sxs-lookup"><span data-stu-id="214df-117">retrieves the device twins with the **location.region** tag set to **US**.</span></span>
<span data-ttu-id="214df-118">布林運算子和算術比較也受到支援，例如</span><span class="sxs-lookup"><span data-stu-id="214df-118">Boolean operators and arithmetic comparisons are supported as well, for example</span></span>

```sql
SELECT * FROM devices
WHERE tags.location.region = 'US'
    AND properties.reported.telemetryConfig.sendFrequencyInSecs >= 60
```

<span data-ttu-id="214df-119">會擷取所有位於 US、且設定為遙測傳送頻率比每分鐘還低的裝置對應項。</span><span class="sxs-lookup"><span data-stu-id="214df-119">retrieves all device twins located in the US configured to send telemetry less often than every minute.</span></span> <span data-ttu-id="214df-120">為了方便起見，您也可以使用陣列常數搭配 **IN** 和 **NIN** (不在) 運算子。</span><span class="sxs-lookup"><span data-stu-id="214df-120">As a convenience, it is also possible to use array constants with the **IN** and **NIN** (not in) operators.</span></span> <span data-ttu-id="214df-121">例如，</span><span class="sxs-lookup"><span data-stu-id="214df-121">For instance,</span></span>

```sql
SELECT * FROM devices
WHERE properties.reported.connectivity IN ['wired', 'wifi']
```

<span data-ttu-id="214df-122">會擷取所有報告使用 WiFi 或有線連線能力的裝置對應項。</span><span class="sxs-lookup"><span data-stu-id="214df-122">retrieves all device twins that reported WiFi or wired connectivity.</span></span> <span data-ttu-id="214df-123">您通常必須識別包含特定屬性的所有裝置對應項。</span><span class="sxs-lookup"><span data-stu-id="214df-123">It is often necessary to identify all device twins that contain a specific property.</span></span> <span data-ttu-id="214df-124">為了實現此目的，IoT 中樞支援 `is_defined()` 函式。</span><span class="sxs-lookup"><span data-stu-id="214df-124">IoT Hub supports the function `is_defined()` for this purpose.</span></span> <span data-ttu-id="214df-125">例如，</span><span class="sxs-lookup"><span data-stu-id="214df-125">For instance,</span></span>

```SQL
SELECT * FROM devices
WHERE is_defined(properties.reported.connectivity)
```

<span data-ttu-id="214df-126">擷取可定義 `connectivity` 報告屬性的所有裝置對應項。</span><span class="sxs-lookup"><span data-stu-id="214df-126">retrieved all device twins that define the `connectivity` reported property.</span></span> <span data-ttu-id="214df-127">請參閱 [WHERE 子句][lnk-query-where]一節，以取得篩選功能的完整參考。</span><span class="sxs-lookup"><span data-stu-id="214df-127">Refer to the [WHERE clause][lnk-query-where] section for the full reference of the filtering capabilities.</span></span>

<span data-ttu-id="214df-128">群組和彙總也受到支援。</span><span class="sxs-lookup"><span data-stu-id="214df-128">Grouping and aggregations are also supported.</span></span> <span data-ttu-id="214df-129">例如，</span><span class="sxs-lookup"><span data-stu-id="214df-129">For instance,</span></span>

```sql
SELECT properties.reported.telemetryConfig.status AS status,
    COUNT() AS numberOfDevices
FROM devices
GROUP BY properties.reported.telemetryConfig.status
```

<span data-ttu-id="214df-130">會傳回每個遙測組態狀態中的裝置計數。</span><span class="sxs-lookup"><span data-stu-id="214df-130">returns the count of the devices in each telemetry configuration status.</span></span>

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

<span data-ttu-id="214df-131">上述範例說明了如下情況：三個裝置回報設定成功、兩個仍在套用組態，一個回報發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="214df-131">The preceding example illustrates a situation where three devices reported successful configuration, two are still applying the configuration, and one reported an error.</span></span>

### <a name="c-example"></a><span data-ttu-id="214df-132">C# 範例</span><span class="sxs-lookup"><span data-stu-id="214df-132">C# example</span></span>
<span data-ttu-id="214df-133">查詢功能由 [C# 服務 SDK][lnk-hub-sdks] 在 **RegistryManager** 類別中公開。</span><span class="sxs-lookup"><span data-stu-id="214df-133">The query functionality is exposed by the [C# service SDK][lnk-hub-sdks] in the **RegistryManager** class.</span></span>
<span data-ttu-id="214df-134">以下是簡單查詢的範例︰</span><span class="sxs-lookup"><span data-stu-id="214df-134">Here is an example of a simple query:</span></span>

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

<span data-ttu-id="214df-135">請注意**查詢**物件如何以頁面大小 (最多 1000) 具現化，然後藉由呼叫 **GetNextAsTwinAsync** 方法多次擷取多個頁面。</span><span class="sxs-lookup"><span data-stu-id="214df-135">Note how the **query** object is instantiated with a page size (up to 1000), and then multiple pages can be retrieved by calling the **GetNextAsTwinAsync** methods multiple times.</span></span>
<span data-ttu-id="214df-136">請注意，查詢物件會公開多個 **Next\*** (視查詢所需的還原序列化選項，例如裝置對應項或作業物件，或使用投影時要使用的一般 JSON 而定)。</span><span class="sxs-lookup"><span data-stu-id="214df-136">Note that the query object exposes multiple **Next\***, depending on the deserialization option required by the query, such as device twin or job objects, or plain JSON to be used when using projections.</span></span>

### <a name="nodejs-example"></a><span data-ttu-id="214df-137">Node.js 範例</span><span class="sxs-lookup"><span data-stu-id="214df-137">Node.js example</span></span>
<span data-ttu-id="214df-138">查詢功能由[適用於 Node.js 的 Azure IoT 服務 SDK][lnk-hub-sdks] 在 **Registry** 物件中公開。</span><span class="sxs-lookup"><span data-stu-id="214df-138">The query functionality is exposed by the [Azure IoT service SDK for Node.js][lnk-hub-sdks] in the **Registry** object.</span></span>
<span data-ttu-id="214df-139">以下是簡單查詢的範例︰</span><span class="sxs-lookup"><span data-stu-id="214df-139">Here is an example of a simple query:</span></span>

```nodejs
var query = registry.createQuery('SELECT * FROM devices', 100);
var onResults = function(err, results) {
    if (err) {
        console.error('Failed to fetch the results: ' + err.message);
    } else {
        // Do something with the results
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

<span data-ttu-id="214df-140">請注意**查詢**物件如何以頁面大小 (最多 1000) 具現化，然後藉由呼叫 **nextAsTwin** 方法多次擷取多個頁面。</span><span class="sxs-lookup"><span data-stu-id="214df-140">Note how the **query** object is instantiated with a page size (up to 1000), and then multiple pages can be retrieved by calling the **nextAsTwin** methods multiple times.</span></span>
<span data-ttu-id="214df-141">請注意，查詢物件會公開多個 **Next\*** (視查詢所需的還原序列化選項，例如裝置對應項或作業物件，或使用投影時要使用的一般 JSON 而定)。</span><span class="sxs-lookup"><span data-stu-id="214df-141">Note that the query object exposes multiple **next\***, depending on the deserialization option required by the query, such as device twin or job objects, or plain JSON to be used when using projections.</span></span>

### <a name="limitations"></a><span data-ttu-id="214df-142">限制</span><span class="sxs-lookup"><span data-stu-id="214df-142">Limitations</span></span>
> [!IMPORTANT]
> <span data-ttu-id="214df-143">根據裝置對應項中的最新值，查詢結果可能會有數分鐘的延遲。</span><span class="sxs-lookup"><span data-stu-id="214df-143">Query results can have a few minutes of delay with respect to the latest values in device twins.</span></span> <span data-ttu-id="214df-144">若依識別碼查詢個別裝置對應項，建議您一律使用抓取裝置對應項 API，這一律包含最新的值，而且有較高的節流處理限制。</span><span class="sxs-lookup"><span data-stu-id="214df-144">If querying individual device twins by id, it is always preferable to use the retrieve device twin API, which always contains the latest values and has higher throttling limits.</span></span>

<span data-ttu-id="214df-145">目前僅支援在基本類型 (沒有物件) 之間進行比較，例如 `... WHERE properties.desired.config = properties.reported.config` 只會在這些屬性具有基本值時才受到支援。</span><span class="sxs-lookup"><span data-stu-id="214df-145">Currently, comparisons are supported only between primitive types (no objects), for instance `... WHERE properties.desired.config = properties.reported.config` is supported only if those properties have primitive values.</span></span>

## <a name="get-started-with-jobs-queries"></a><span data-ttu-id="214df-146">開始使用作業查詢</span><span class="sxs-lookup"><span data-stu-id="214df-146">Get started with jobs queries</span></span>
<span data-ttu-id="214df-147">[作業][lnk-jobs]可提供方法來對裝置組執行作業。</span><span class="sxs-lookup"><span data-stu-id="214df-147">[Jobs][lnk-jobs] provide a way to execute operations on sets of devices.</span></span> <span data-ttu-id="214df-148">每個裝置對應項皆包含屬於 **jobs** 集合一部分之作業的資訊。</span><span class="sxs-lookup"><span data-stu-id="214df-148">Each device twin contains the information of the jobs of which it is part in a collection called **jobs**.</span></span>
<span data-ttu-id="214df-149">在邏輯上，</span><span class="sxs-lookup"><span data-stu-id="214df-149">Logically,</span></span>

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

<span data-ttu-id="214df-150">目前，此集合可在 IoT 中樞查詢語言中以 **devices.jobs** 的形式來查詢。</span><span class="sxs-lookup"><span data-stu-id="214df-150">Currently, this collection is queryable as **devices.jobs** in the IoT Hub query language.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="214df-151">在查詢裝置對應項 (也就是含有「FROM 裝置」的查詢) 時，目前永遠不會傳回作業屬性。</span><span class="sxs-lookup"><span data-stu-id="214df-151">Currently, the jobs property is never returned when querying device twins (that is, queries that contains 'FROM devices').</span></span> <span data-ttu-id="214df-152">此屬性只能使用 `FROM devices.jobs` 直接透過查詢來存取。</span><span class="sxs-lookup"><span data-stu-id="214df-152">It can only be accessed directly with queries using `FROM devices.jobs`.</span></span>
>
>

<span data-ttu-id="214df-153">例如，若要取得影響單一裝置的所有作業 (過去的和排程的)，您可以使用下列查詢︰</span><span class="sxs-lookup"><span data-stu-id="214df-153">For instance, to get all jobs (past and scheduled) that affect a single device, you can use the following query:</span></span>

```sql
SELECT * FROM devices.jobs
WHERE devices.jobs.deviceId = 'myDeviceId'
```

<span data-ttu-id="214df-154">請注意這個查詢如何為每個傳回的作業提供裝置特定的狀態 (可能的話還會提供直接方法回應)。</span><span class="sxs-lookup"><span data-stu-id="214df-154">Note how this query provides the device-specific status (and possibly the direct method response) of each job returned.</span></span>
<span data-ttu-id="214df-155">您也可以在 **devices.jobs** 集合的所有物件屬性上，使用任意布林值條件進行篩選。</span><span class="sxs-lookup"><span data-stu-id="214df-155">It is also possible to filter with arbitrary Boolean conditions on all object properties in the **devices.jobs** collection.</span></span>
<span data-ttu-id="214df-156">例如下列查詢：</span><span class="sxs-lookup"><span data-stu-id="214df-156">For instance, the following query:</span></span>

```sql
SELECT * FROM devices.jobs
WHERE devices.jobs.deviceId = 'myDeviceId'
    AND devices.jobs.jobType = 'scheduleTwinUpdate'
    AND devices.jobs.status = 'completed'
    AND devices.jobs.createdTimeUtc > '2016-09-01'
```

<span data-ttu-id="214df-157">會針對在 2016 年 9 月之後所建立的裝置 **myDeviceId** 擷取所有已完成的裝置對應項更新作業。</span><span class="sxs-lookup"><span data-stu-id="214df-157">retrieves all completed device twin update jobs for device **myDeviceId** that were created after September 2016.</span></span>

<span data-ttu-id="214df-158">您也可以擷取單一作業的每一裝置結果。</span><span class="sxs-lookup"><span data-stu-id="214df-158">It is also possible to retrieve the per-device outcomes of a single job.</span></span>

```sql
SELECT * FROM devices.jobs
WHERE devices.jobs.jobId = 'myJobId'
```

### <a name="limitations"></a><span data-ttu-id="214df-159">限制</span><span class="sxs-lookup"><span data-stu-id="214df-159">Limitations</span></span>
<span data-ttu-id="214df-160">**devices.jobs** 上的查詢目前不支援︰</span><span class="sxs-lookup"><span data-stu-id="214df-160">Currently, queries on **devices.jobs** do not support:</span></span>

* <span data-ttu-id="214df-161">投影，因此只有 `SELECT *` 是可行的。</span><span class="sxs-lookup"><span data-stu-id="214df-161">Projections, therefore only `SELECT *` is possible.</span></span>
* <span data-ttu-id="214df-162">參照裝置對應項 (作業屬性除外) 的條件 (請參閱上一節)。</span><span class="sxs-lookup"><span data-stu-id="214df-162">Conditions that refer to the device twin in addition to job properties (see the preceding section).</span></span>
* <span data-ttu-id="214df-163">執行彙總，例如計數、平均、分組依據。</span><span class="sxs-lookup"><span data-stu-id="214df-163">Performing aggregations, such as count, avg, group by.</span></span>

## <a name="get-started-with-device-to-cloud-message-routes-query-expressions"></a><span data-ttu-id="214df-164">開始使用裝置對雲端訊息路由查詢運算式</span><span class="sxs-lookup"><span data-stu-id="214df-164">Get started with device-to-cloud message routes query expressions</span></span>

<span data-ttu-id="214df-165">使用[裝置對雲端路由][lnk-devguide-messaging-routes]，您可以設定 IoT 中樞，以根據對個別訊息評估的運算式，將裝置對雲端訊息分派至不同的端點。</span><span class="sxs-lookup"><span data-stu-id="214df-165">Using [device-to-cloud routes][lnk-devguide-messaging-routes], you can configure IoT Hub to dispatch device-to-cloud messages to different endpoints based on expressions evaluated against individual messages.</span></span>

<span data-ttu-id="214df-166">路由[條件][lnk-query-expressions]會使用相同的 IoT 中樞查詢語言做為對應項和作業查詢中的條件。</span><span class="sxs-lookup"><span data-stu-id="214df-166">The route [condition][lnk-query-expressions] uses the same IoT Hub query language as conditions in twin and job queries.</span></span> <span data-ttu-id="214df-167">路由條件會依據訊息標頭和內文進行評估。</span><span class="sxs-lookup"><span data-stu-id="214df-167">Route conditions are evaluated on the message headers and body.</span></span> <span data-ttu-id="214df-168">您的路由查詢運算式可能只涉及訊息標頭、只涉及訊息內文，或同時涉及訊息標頭和訊息內文。</span><span class="sxs-lookup"><span data-stu-id="214df-168">Your routing query expression may involve only message headers, only the message body, or both message headers and message body.</span></span> <span data-ttu-id="214df-169">IoT 中樞假設標頭和訊息內文有特定結構描述才能路由傳送訊息，下列各節將說明讓 IoT 中樞正確路由所需的項目：</span><span class="sxs-lookup"><span data-stu-id="214df-169">IoT Hub assumes a specific schema for the headers and message body in order to route messages, and the following sections describe what is required for IoT Hub to properly route:</span></span>

### <a name="routing-on-message-headers"></a><span data-ttu-id="214df-170">依據訊息標頭進行路由</span><span class="sxs-lookup"><span data-stu-id="214df-170">Routing on message headers</span></span>

<span data-ttu-id="214df-171">IoT 中樞假設訊息路由的訊息標頭採用下列 JSON 表示法：</span><span class="sxs-lookup"><span data-stu-id="214df-171">IoT Hub assumes the following JSON representation of message headers for message routing:</span></span>

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

<span data-ttu-id="214df-172">訊息系統屬性前面會加上 `'$'` 符號。</span><span class="sxs-lookup"><span data-stu-id="214df-172">Message system properties are prefixed with the `'$'` symbol.</span></span>
<span data-ttu-id="214df-173">使用者屬性則一律透過其名稱來存取。</span><span class="sxs-lookup"><span data-stu-id="214df-173">User properties are always accessed with their name.</span></span> <span data-ttu-id="214df-174">若使用者屬性名稱剛好與系統屬性 (例如 `$to`) 相同，將使用 `$to` 運算式擷取使用者屬性。</span><span class="sxs-lookup"><span data-stu-id="214df-174">If a user property name happens to coincide with a system property (such as `$to`), the user property will be retrieved with the `$to` expression.</span></span>
<span data-ttu-id="214df-175">您一律可以使用括弧 `{}` 來存取系統屬性：例如，您可以使用運算式 `{$to}` 來存取系統屬性 `to`。</span><span class="sxs-lookup"><span data-stu-id="214df-175">You can always access the system property using brackets `{}`: for instance, you can use the expression `{$to}` to access the system property `to`.</span></span> <span data-ttu-id="214df-176">以括弧括住的屬性名稱一律會擷取對應的系統屬性。</span><span class="sxs-lookup"><span data-stu-id="214df-176">Bracketed property names always retrieve the corresponding system property.</span></span>

<span data-ttu-id="214df-177">請記住，屬性名稱不區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="214df-177">Remember that property names are case insensitive.</span></span>

> [!NOTE]
> <span data-ttu-id="214df-178">所有屬性皆為字串。</span><span class="sxs-lookup"><span data-stu-id="214df-178">All message properties are strings.</span></span> <span data-ttu-id="214df-179">系統屬性 (如[開發人員指南][lnk-devguide-messaging-format]所述) 目前無法使用於查詢中。</span><span class="sxs-lookup"><span data-stu-id="214df-179">System properties, as described in the [developer guide][lnk-devguide-messaging-format], are currently not available to use in queries.</span></span>
>

<span data-ttu-id="214df-180">例如，如果您使用 `messageType` 屬性，您可能想要將所有遙測都路由傳送至一個端點，以及將所有警示路由傳送至另一個端點。</span><span class="sxs-lookup"><span data-stu-id="214df-180">For example, if you use a `messageType` property, you might want to route all telemetry to one endpoint, and all alerts to another endpoint.</span></span> <span data-ttu-id="214df-181">您可以撰寫下列運算式來路由傳送遙測資料︰</span><span class="sxs-lookup"><span data-stu-id="214df-181">You can write the following expression to route the telemetry:</span></span>

```sql
messageType = 'telemetry'
```

<span data-ttu-id="214df-182">以及撰寫下列運算式來路由傳送警示訊息︰</span><span class="sxs-lookup"><span data-stu-id="214df-182">And the following expression to route the alert messages:</span></span>

```sql
messageType = 'alert'
```

<span data-ttu-id="214df-183">也支援布林運算式和函式。</span><span class="sxs-lookup"><span data-stu-id="214df-183">Boolean expressions and functions are also supported.</span></span> <span data-ttu-id="214df-184">這項功能可讓您區分嚴重性層級，例如︰</span><span class="sxs-lookup"><span data-stu-id="214df-184">This feature enables you to distinguish between severity level, for example:</span></span>

```sql
messageType = 'alerts' AND as_number(severity) <= 2
```

<span data-ttu-id="214df-185">請參閱[運算式和條件][lnk-query-expressions]一節，以取得支援的完整運算子和函式清單。</span><span class="sxs-lookup"><span data-stu-id="214df-185">Refer to the [Expression and conditions][lnk-query-expressions] section for the full list of supported operators and functions.</span></span>

### <a name="routing-on-message-bodies"></a><span data-ttu-id="214df-186">依據訊息內文進行路由</span><span class="sxs-lookup"><span data-stu-id="214df-186">Routing on message bodies</span></span>

<span data-ttu-id="214df-187">IoT 中樞只有在訊息內文是以 UTF-8、UTF-16 或 UTF-32 編碼的正確格式 JSON 時，才能依據訊息內文的內容進行路由。</span><span class="sxs-lookup"><span data-stu-id="214df-187">IoT Hub can only route based on message body contents if the message body is properly formed JSON encoded in either UTF-8, UTF-16, or UTF-32.</span></span> <span data-ttu-id="214df-188">您必須將訊息的內容類型設定為 `application/json`，並將內容編碼設定為訊息標頭支援的其中一個 UTF 編碼，IoT 中樞才能依據內文的內容路由傳送訊息。</span><span class="sxs-lookup"><span data-stu-id="214df-188">You must set the content type of the message to `application/json` and the content encoding to one of the supported UTF encodings in the message headers to allow IoT Hub to route the message based on the body contents.</span></span> <span data-ttu-id="214df-189">如果未指定任一標頭，IoT 中樞將不會嘗試對訊息評估任何涉及內文的查詢運算式。</span><span class="sxs-lookup"><span data-stu-id="214df-189">If either of the headers is not specified, IoT Hub will not attempt to evaluate any query expression involving the body against the message.</span></span> <span data-ttu-id="214df-190">如果您的訊息不是 JSON 訊息，或者如果訊息未指定內容類型和內容編碼，您仍然可以使用訊息路由來依據訊息標頭路由傳送訊息。</span><span class="sxs-lookup"><span data-stu-id="214df-190">If your message is not a JSON message, or if the message does not specify the content type and content encoding, you may still use message routing to route the message based on the message headers.</span></span>

<span data-ttu-id="214df-191">您可以在查詢運算式中使用 `$body` 來路由傳送訊息。</span><span class="sxs-lookup"><span data-stu-id="214df-191">You can use `$body` in the query expression to route the message.</span></span> <span data-ttu-id="214df-192">您可以在查詢運算式中使用簡單內文參考、內文陣列參考或多個內文參考。</span><span class="sxs-lookup"><span data-stu-id="214df-192">You can use a simple body reference, body array reference, or multiple body references in the query expression.</span></span> <span data-ttu-id="214df-193">您的查詢運算式也可以將內文參考與訊息標頭參考合併。</span><span class="sxs-lookup"><span data-stu-id="214df-193">Your query expression can also combine a body reference with a message header reference.</span></span> <span data-ttu-id="214df-194">例如，以下是所有有效的查詢運算式：</span><span class="sxs-lookup"><span data-stu-id="214df-194">For example, the following are all valid query expressions:</span></span>

```sql
$body.message.Weather.Location.State = 'WA'
$body.Weather.HistoricalData[0].Month = 'Feb'
$body.Weather.Temperature = 50 AND $body.message.Weather.IsEnabled
length($body.Weather.Location.State) = 2
$body.Weather.Temperature = 50 AND Status = 'Active'
```

## <a name="basics-of-an-iot-hub-query"></a><span data-ttu-id="214df-195">IoT 中樞查詢的基本概念</span><span class="sxs-lookup"><span data-stu-id="214df-195">Basics of an IoT Hub query</span></span>
<span data-ttu-id="214df-196">每一個 IoT 中樞查詢都包含 SELECT 和 FROM 子句，以及選擇性的 WHERE 和 GROUP BY 子句。</span><span class="sxs-lookup"><span data-stu-id="214df-196">Every IoT Hub query consists of a SELECT and FROM clauses and by optional WHERE and GROUP BY clauses.</span></span> <span data-ttu-id="214df-197">每個查詢都會在 JSON 文件的集合上執行，例如裝置對應項。</span><span class="sxs-lookup"><span data-stu-id="214df-197">Every query is run on a collection of JSON documents, for example device twins.</span></span> <span data-ttu-id="214df-198">FROM 子句會指出要在其上反覆運算的文件集合 (**devices** 或 **devices.jobs**)。</span><span class="sxs-lookup"><span data-stu-id="214df-198">The FROM clause indicates the document collection to be iterated on (**devices** or **devices.jobs**).</span></span> <span data-ttu-id="214df-199">然後，會套用 WHERE 子句中的篩選。</span><span class="sxs-lookup"><span data-stu-id="214df-199">Then, the filter in the WHERE clause is applied.</span></span> <span data-ttu-id="214df-200">若為彙總，此步驟的結果會依照 GROUP BY 子句中所指定的方式針對每個群組進行分組，並依 SELECT 子句中所指定的方式產生一個資料列。</span><span class="sxs-lookup"><span data-stu-id="214df-200">With aggregations, the results of this step are grouped as specified in the GROUP BY clause and, for each group, a row is generated as specified in the SELECT clause.</span></span>

```sql
SELECT <select_list>
FROM <from_specification>
[WHERE <filter_condition>]
[GROUP BY <group_specification>]
```

## <a name="from-clause"></a><span data-ttu-id="214df-201">FROM 子句</span><span class="sxs-lookup"><span data-stu-id="214df-201">FROM clause</span></span>
<span data-ttu-id="214df-202">**FROM <from_specification>** 子句只能採用兩個值︰**FROM devices** (用來查詢裝置對應項) 或 **FROM devices.jobs** (用來查詢作業的每一裝置詳細資料)。</span><span class="sxs-lookup"><span data-stu-id="214df-202">The **FROM <from_specification>** clause can assume only two values: **FROM devices**, to query device twins, or **FROM devices.jobs**, to query job per-device details.</span></span>

## <a name="where-clause"></a><span data-ttu-id="214df-203">WHERE 子句</span><span class="sxs-lookup"><span data-stu-id="214df-203">WHERE clause</span></span>
<span data-ttu-id="214df-204">**WHERE <filter_condition>** 子句是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="214df-204">The **WHERE <filter_condition>** clause is optional.</span></span> <span data-ttu-id="214df-205">它會指定一或多個條件，而且 FROM 集合中的 JSON 文件必須滿足這些條件，才能納入為結果的一部分。</span><span class="sxs-lookup"><span data-stu-id="214df-205">It specifies one or more conditions that the JSON documents in the FROM collection must satisfy to be included as part of the result.</span></span> <span data-ttu-id="214df-206">任何 JSON 文件都必須將指定的條件評估為 "true"，才能併入結果。</span><span class="sxs-lookup"><span data-stu-id="214df-206">Any JSON document must evaluate the specified conditions to "true" to be included in the result.</span></span>

<span data-ttu-id="214df-207">[運算式和條件][lnk-query-expressions]一節中會說明允許的條件。</span><span class="sxs-lookup"><span data-stu-id="214df-207">The allowed conditions are described in section [Expressions and conditions][lnk-query-expressions].</span></span>

## <a name="select-clause"></a><span data-ttu-id="214df-208">SELECT 子句</span><span class="sxs-lookup"><span data-stu-id="214df-208">SELECT clause</span></span>
<span data-ttu-id="214df-209">SELECT 子句 (**SELECT <select_list>**) 是必要子句，並可指定要從查詢擷取的值。</span><span class="sxs-lookup"><span data-stu-id="214df-209">The SELECT clause (**SELECT <select_list>**) is mandatory and specifies what values are retrieved from the query.</span></span> <span data-ttu-id="214df-210">它會指定用來產生新 JSON 物件的 JSON 值。</span><span class="sxs-lookup"><span data-stu-id="214df-210">It specifies the JSON values to be used to generate new JSON objects.</span></span>
<span data-ttu-id="214df-211">針對 FROM 集合已經過篩選 (及選擇性分組) 之子集的每個項目，投影階段會產生新的 JSON 物件 (以 SELECT 子句中指定的值所建構)。</span><span class="sxs-lookup"><span data-stu-id="214df-211">For each element of the filtered (and optionally grouped) subset of the FROM collection, the projection phase generates a new JSON object, constructed with the values specified in the SELECT clause.</span></span>

<span data-ttu-id="214df-212">以下是 SELECT 子句的文法︰</span><span class="sxs-lookup"><span data-stu-id="214df-212">Following is the grammar of the SELECT clause:</span></span>

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

<span data-ttu-id="214df-213">其中 **attribute_name** 指的是 FROM 集合中 JSON 文件的任何屬性。</span><span class="sxs-lookup"><span data-stu-id="214df-213">where **attribute_name** refers to any property of the JSON document in the FROM collection.</span></span> <span data-ttu-id="214df-214">您可以在[開始使用裝置對應項查詢][lnk-query-getstarted]一節中找到一些 SELECT 子句範例。</span><span class="sxs-lookup"><span data-stu-id="214df-214">Some examples of SELECT clauses can be found in the [Getting started with device twin queries][lnk-query-getstarted] section.</span></span>

<span data-ttu-id="214df-215">與 **SELECT \*** 不同的選取範圍子句目前只支援在裝置對應項的彙總查詢中使用。</span><span class="sxs-lookup"><span data-stu-id="214df-215">Currently, selection clauses different than **SELECT \*** are only supported in aggregate queries on device twins.</span></span>

## <a name="group-by-clause"></a><span data-ttu-id="214df-216">GROUP BY 子句</span><span class="sxs-lookup"><span data-stu-id="214df-216">GROUP BY clause</span></span>
<span data-ttu-id="214df-217">**GROUP BY <group_specification>** 子句是選擇性步驟，可在 WHERE 子句中指定的篩選之後、SELECT 中指定的投影之前執行。</span><span class="sxs-lookup"><span data-stu-id="214df-217">The **GROUP BY <group_specification>** clause is an optional step that can be executed after the filter specified in the WHERE clause, and before the projection specified in the SELECT.</span></span> <span data-ttu-id="214df-218">它會根據屬性值來分組文件。</span><span class="sxs-lookup"><span data-stu-id="214df-218">It groups documents based on the value of an attribute.</span></span> <span data-ttu-id="214df-219">這些群組可用來產生 SELECT 子句中所指定的彙總值。</span><span class="sxs-lookup"><span data-stu-id="214df-219">These groups are used to generate aggregated values as specified in the SELECT clause.</span></span>

<span data-ttu-id="214df-220">使用 GROUP BY 的查詢範例如下︰</span><span class="sxs-lookup"><span data-stu-id="214df-220">An example of a query using GROUP BY is:</span></span>

```sql
SELECT properties.reported.telemetryConfig.status AS status,
    COUNT() AS numberOfDevices
FROM devices
GROUP BY properties.reported.telemetryConfig.status
```

<span data-ttu-id="214df-221">GROUP BY 的正式語法如下︰</span><span class="sxs-lookup"><span data-stu-id="214df-221">The formal syntax for GROUP BY is:</span></span>

```
GROUP BY <group_by_element>
<group_by_element> :==
    attribute_name
    | < group_by_element > '.' attribute_name
```

<span data-ttu-id="214df-222">其中 **attribute_name** 指的是 FROM 集合中 JSON 文件的任何屬性。</span><span class="sxs-lookup"><span data-stu-id="214df-222">where **attribute_name** refers to any property of the JSON document in the FROM collection.</span></span>

<span data-ttu-id="214df-223">目前，GROUP BY 子句只支援在查詢裝置對應項時使用。</span><span class="sxs-lookup"><span data-stu-id="214df-223">Currently, the GROUP BY clause is only supported when querying device twins.</span></span>

## <a name="expressions-and-conditions"></a><span data-ttu-id="214df-224">運算式和條件</span><span class="sxs-lookup"><span data-stu-id="214df-224">Expressions and conditions</span></span>
<span data-ttu-id="214df-225">概括而言，運算式：</span><span class="sxs-lookup"><span data-stu-id="214df-225">At a high level, an *expression*:</span></span>

* <span data-ttu-id="214df-226">會評估為 JSON 類型 (例如布林值、數字、字串、陣列或物件) 的執行個體，以及</span><span class="sxs-lookup"><span data-stu-id="214df-226">Evaluates to an instance of a JSON type (such as Boolean, number, string, array, or object), and</span></span>
* <span data-ttu-id="214df-227">定義方式是使用內建運算子和函式處理來自裝置 JSON 文件和常數的資料。</span><span class="sxs-lookup"><span data-stu-id="214df-227">Is defined by manipulating data coming from the device JSON document and constants using built-in operators and functions.</span></span>

<span data-ttu-id="214df-228">「條件」是評估為布林值的運算式。</span><span class="sxs-lookup"><span data-stu-id="214df-228">*Conditions* are expressions that evaluate to a Boolean.</span></span> <span data-ttu-id="214df-229">任何不同於布林值 **true** 的常數會被視為 **false** (包括 **null**、**undefined**、任何物件或陣列執行個體、任何字串，以及顯然是布林值 **false**)。</span><span class="sxs-lookup"><span data-stu-id="214df-229">Any constant different than Boolean **true** is considered as **false** (including **null**, **undefined**, any object or array instance, any string, and clearly the Boolean **false**).</span></span>

<span data-ttu-id="214df-230">運算式的語法如下︰</span><span class="sxs-lookup"><span data-stu-id="214df-230">The syntax for expressions is:</span></span>

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

<span data-ttu-id="214df-231">其中：</span><span class="sxs-lookup"><span data-stu-id="214df-231">where:</span></span>

| <span data-ttu-id="214df-232">符號</span><span class="sxs-lookup"><span data-stu-id="214df-232">Symbol</span></span> | <span data-ttu-id="214df-233">定義</span><span class="sxs-lookup"><span data-stu-id="214df-233">Definition</span></span> |
| --- | --- |
| <span data-ttu-id="214df-234">attribute_name</span><span class="sxs-lookup"><span data-stu-id="214df-234">attribute_name</span></span> | <span data-ttu-id="214df-235">**FROM** 集合中 JSON 文件的任何屬性。</span><span class="sxs-lookup"><span data-stu-id="214df-235">Any property of the JSON document in the **FROM** collection.</span></span> |
| <span data-ttu-id="214df-236">binary_operator</span><span class="sxs-lookup"><span data-stu-id="214df-236">binary_operator</span></span> | <span data-ttu-id="214df-237">[運算子](#operators)一節中所列的任何二元運算子。</span><span class="sxs-lookup"><span data-stu-id="214df-237">Any binary operator listed in the [Operators](#operators) section.</span></span> |
| <span data-ttu-id="214df-238">function_name</span><span class="sxs-lookup"><span data-stu-id="214df-238">function_name</span></span>| <span data-ttu-id="214df-239">[函式](#functions)一節中所列的任何函式。</span><span class="sxs-lookup"><span data-stu-id="214df-239">Any function listed in the [Functions](#functions) section.</span></span> |
| <span data-ttu-id="214df-240">decimal_literal</span><span class="sxs-lookup"><span data-stu-id="214df-240">decimal_literal</span></span> |<span data-ttu-id="214df-241">以小數點標記法表示的浮點數。</span><span class="sxs-lookup"><span data-stu-id="214df-241">A float expressed in decimal notation.</span></span> |
| <span data-ttu-id="214df-242">hexadecimal_literal</span><span class="sxs-lookup"><span data-stu-id="214df-242">hexadecimal_literal</span></span> |<span data-ttu-id="214df-243">以字串 '0x' 後面接著十六進位數字的字串所表示的數字。</span><span class="sxs-lookup"><span data-stu-id="214df-243">A number expressed by the string ‘0x’ followed by a string of hexadecimal digits.</span></span> |
| <span data-ttu-id="214df-244">string_literal</span><span class="sxs-lookup"><span data-stu-id="214df-244">string_literal</span></span> |<span data-ttu-id="214df-245">字串常值是由零個或多個 Unicode 字元序列或逸出序列所表示的 Unicode 字串。</span><span class="sxs-lookup"><span data-stu-id="214df-245">String literals are Unicode strings represented by a sequence of zero or more Unicode characters or escape sequences.</span></span> <span data-ttu-id="214df-246">字串常值會以單引號 (所有格符號：') 或雙引號 (引號：") 括起來。</span><span class="sxs-lookup"><span data-stu-id="214df-246">String literals are enclosed in single quotes (apostrophe: ' ) or double quotes (quotation mark: ").</span></span> <span data-ttu-id="214df-247">允許的逸出︰`\'`、`\"`、`\\`、`\uXXXX` (適用於由 4 個十六進位數字所定義的 Unicode 字元)。</span><span class="sxs-lookup"><span data-stu-id="214df-247">Allowed escapes: `\'`, `\"`, `\\`, `\uXXXX` for Unicode characters defined by 4 hexadecimal digits.</span></span> |

### <a name="operators"></a><span data-ttu-id="214df-248">運算子</span><span class="sxs-lookup"><span data-stu-id="214df-248">Operators</span></span>
<span data-ttu-id="214df-249">支援下列運算子：</span><span class="sxs-lookup"><span data-stu-id="214df-249">The following operators are supported:</span></span>

| <span data-ttu-id="214df-250">系列</span><span class="sxs-lookup"><span data-stu-id="214df-250">Family</span></span> | <span data-ttu-id="214df-251">運算子</span><span class="sxs-lookup"><span data-stu-id="214df-251">Operators</span></span> |
| --- | --- |
| <span data-ttu-id="214df-252">算術</span><span class="sxs-lookup"><span data-stu-id="214df-252">Arithmetic</span></span> |<span data-ttu-id="214df-253">+、-、*、/、%</span><span class="sxs-lookup"><span data-stu-id="214df-253">+,-,*,/,%</span></span> |
| <span data-ttu-id="214df-254">邏輯</span><span class="sxs-lookup"><span data-stu-id="214df-254">Logical</span></span> |<span data-ttu-id="214df-255">AND、OR、NOT</span><span class="sxs-lookup"><span data-stu-id="214df-255">AND, OR, NOT</span></span> |
| <span data-ttu-id="214df-256">比較</span><span class="sxs-lookup"><span data-stu-id="214df-256">Comparison</span></span> |<span data-ttu-id="214df-257">=、!=、<、>、<=、>=、<></span><span class="sxs-lookup"><span data-stu-id="214df-257">=, !=, <, >, <=, >=, <></span></span> |

### <a name="functions"></a><span data-ttu-id="214df-258">Functions</span><span class="sxs-lookup"><span data-stu-id="214df-258">Functions</span></span>
<span data-ttu-id="214df-259">查詢對應項和作業時唯一支援的函式為：</span><span class="sxs-lookup"><span data-stu-id="214df-259">When querying twins and jobs the only supported function is:</span></span>

| <span data-ttu-id="214df-260">函式</span><span class="sxs-lookup"><span data-stu-id="214df-260">Function</span></span> | <span data-ttu-id="214df-261">說明</span><span class="sxs-lookup"><span data-stu-id="214df-261">Description</span></span> |
| -------- | ----------- |
| <span data-ttu-id="214df-262">IS_DEFINED(property)</span><span class="sxs-lookup"><span data-stu-id="214df-262">IS_DEFINED(property)</span></span> | <span data-ttu-id="214df-263">傳回布林值，表示屬性是否已經指派值 (包含 `null`)。</span><span class="sxs-lookup"><span data-stu-id="214df-263">Returns a Boolean indicating if the property has been assigned a value (including `null`).</span></span> |

<span data-ttu-id="214df-264">在路由條件中，支援下列比對函式：</span><span class="sxs-lookup"><span data-stu-id="214df-264">In routes conditions, the following math functions are supported:</span></span>

| <span data-ttu-id="214df-265">函式</span><span class="sxs-lookup"><span data-stu-id="214df-265">Function</span></span> | <span data-ttu-id="214df-266">說明</span><span class="sxs-lookup"><span data-stu-id="214df-266">Description</span></span> |
| -------- | ----------- |
| <span data-ttu-id="214df-267">ABS(x)</span><span class="sxs-lookup"><span data-stu-id="214df-267">ABS(x)</span></span> | <span data-ttu-id="214df-268">傳回指定之數值運算式的絕對 (正) 值。</span><span class="sxs-lookup"><span data-stu-id="214df-268">Returns the absolute (positive) value of the specified numeric expression.</span></span> |
| <span data-ttu-id="214df-269">EXP(x)</span><span class="sxs-lookup"><span data-stu-id="214df-269">EXP(x)</span></span> | <span data-ttu-id="214df-270">傳回指定之數值運算式 (e^x) 的指數值。</span><span class="sxs-lookup"><span data-stu-id="214df-270">Returns the exponential value of the specified numeric expression (e^x).</span></span> |
| <span data-ttu-id="214df-271">POWER(x,y)</span><span class="sxs-lookup"><span data-stu-id="214df-271">POWER(x,y)</span></span> | <span data-ttu-id="214df-272">將指定之運算式的值傳回給指定的乘冪 (x^y)。</span><span class="sxs-lookup"><span data-stu-id="214df-272">Returns the value of the specified expression to the specified power (x^y).</span></span>|
| <span data-ttu-id="214df-273">SQUARE(x)</span><span class="sxs-lookup"><span data-stu-id="214df-273">SQUARE(x)</span></span> | <span data-ttu-id="214df-274">傳回指定之數值的平方。</span><span class="sxs-lookup"><span data-stu-id="214df-274">Returns the square of the specified numeric value.</span></span> |
| <span data-ttu-id="214df-275">CEILING(x)</span><span class="sxs-lookup"><span data-stu-id="214df-275">CEILING(x)</span></span> | <span data-ttu-id="214df-276">傳回大於或等於指定之數值運算式的最小整數值。</span><span class="sxs-lookup"><span data-stu-id="214df-276">Returns the smallest integer value greater than, or equal to, the specified numeric expression.</span></span> |
| <span data-ttu-id="214df-277">FLOOR(x)</span><span class="sxs-lookup"><span data-stu-id="214df-277">FLOOR(x)</span></span> | <span data-ttu-id="214df-278">傳回小於或等於指定之數值運算式的最大整數。</span><span class="sxs-lookup"><span data-stu-id="214df-278">Returns the largest integer less than or equal to the specified numeric expression.</span></span> |
| <span data-ttu-id="214df-279">SIGN(x)</span><span class="sxs-lookup"><span data-stu-id="214df-279">SIGN(x)</span></span> | <span data-ttu-id="214df-280">傳回指定之數值運算式的正數 (+1)、零 (0) 或負數 (-1) 符號。</span><span class="sxs-lookup"><span data-stu-id="214df-280">Returns the positive (+1), zero (0), or negative (-1) sign of the specified numeric expression.</span></span>|
| <span data-ttu-id="214df-281">SQRT(x)</span><span class="sxs-lookup"><span data-stu-id="214df-281">SQRT(x)</span></span> | <span data-ttu-id="214df-282">傳回指定之數值的平方。</span><span class="sxs-lookup"><span data-stu-id="214df-282">Returns the square of the specified numeric value.</span></span> |

<span data-ttu-id="214df-283">在路由條件中，支援下列類型檢查和轉換函式：</span><span class="sxs-lookup"><span data-stu-id="214df-283">In routes conditions, the following type checking and casting functions are supported:</span></span>

| <span data-ttu-id="214df-284">函式</span><span class="sxs-lookup"><span data-stu-id="214df-284">Function</span></span> | <span data-ttu-id="214df-285">說明</span><span class="sxs-lookup"><span data-stu-id="214df-285">Description</span></span> |
| -------- | ----------- |
| <span data-ttu-id="214df-286">AS_NUMBER</span><span class="sxs-lookup"><span data-stu-id="214df-286">AS_NUMBER</span></span> | <span data-ttu-id="214df-287">將輸入字串轉換為數字。</span><span class="sxs-lookup"><span data-stu-id="214df-287">Converts the input string to a number.</span></span> <span data-ttu-id="214df-288">如果輸入是一個數字則為 `noop`；如果字串不是數字則為 `Undefined`。</span><span class="sxs-lookup"><span data-stu-id="214df-288">`noop` if input is a number; `Undefined` if string does not represent a number.</span></span>|
| <span data-ttu-id="214df-289">IS_ARRAY</span><span class="sxs-lookup"><span data-stu-id="214df-289">IS_ARRAY</span></span> | <span data-ttu-id="214df-290">傳回布林值，表示指定之運算式的類型為陣列。</span><span class="sxs-lookup"><span data-stu-id="214df-290">Returns a Boolean value indicating if the type of the specified expression is an array.</span></span> |
| <span data-ttu-id="214df-291">IS_BOOL</span><span class="sxs-lookup"><span data-stu-id="214df-291">IS_BOOL</span></span> | <span data-ttu-id="214df-292">傳回布林值，表示指定之運算式的類型為布林值。</span><span class="sxs-lookup"><span data-stu-id="214df-292">Returns a Boolean value indicating if the type of the specified expression is a Boolean.</span></span> |
| <span data-ttu-id="214df-293">IS_DEFINED</span><span class="sxs-lookup"><span data-stu-id="214df-293">IS_DEFINED</span></span> | <span data-ttu-id="214df-294">傳回布林值，表示屬性是否已經指派值。</span><span class="sxs-lookup"><span data-stu-id="214df-294">Returns a Boolean indicating if the property has been assigned a value.</span></span> |
| <span data-ttu-id="214df-295">IS_NULL</span><span class="sxs-lookup"><span data-stu-id="214df-295">IS_NULL</span></span> | <span data-ttu-id="214df-296">傳回布林值，表示指定之運算式的類型為 null。</span><span class="sxs-lookup"><span data-stu-id="214df-296">Returns a Boolean value indicating if the type of the specified expression is null.</span></span> |
| <span data-ttu-id="214df-297">IS_NUMBER</span><span class="sxs-lookup"><span data-stu-id="214df-297">IS_NUMBER</span></span> | <span data-ttu-id="214df-298">傳回布林值，表示指定之運算式的類型為數字。</span><span class="sxs-lookup"><span data-stu-id="214df-298">Returns a Boolean value indicating if the type of the specified expression is a number.</span></span> |
| <span data-ttu-id="214df-299">IS_OBJECT</span><span class="sxs-lookup"><span data-stu-id="214df-299">IS_OBJECT</span></span> | <span data-ttu-id="214df-300">傳回布林值，表示指定之運算式的類型為 JSON 物件。</span><span class="sxs-lookup"><span data-stu-id="214df-300">Returns a Boolean value indicating if the type of the specified expression is a JSON object.</span></span> |
| <span data-ttu-id="214df-301">IS_PRIMITIVE</span><span class="sxs-lookup"><span data-stu-id="214df-301">IS_PRIMITIVE</span></span> | <span data-ttu-id="214df-302">傳回布林值，表示指定之運算式的類型為基本類型 (字串、布林值、數值或 `null`)。</span><span class="sxs-lookup"><span data-stu-id="214df-302">Returns a Boolean value indicating if the type of the specified expression is a primitive (string, Boolean, numeric or `null`).</span></span> |
| <span data-ttu-id="214df-303">IS_STRING</span><span class="sxs-lookup"><span data-stu-id="214df-303">IS_STRING</span></span> | <span data-ttu-id="214df-304">傳回布林值，表示指定之運算式的類型為字串。</span><span class="sxs-lookup"><span data-stu-id="214df-304">Returns a Boolean value indicating if the type of the specified expression is a string.</span></span> |

<span data-ttu-id="214df-305">在路由條件中，支援下列字串函式：</span><span class="sxs-lookup"><span data-stu-id="214df-305">In routes conditions, the following string functions are supported:</span></span>

| <span data-ttu-id="214df-306">函式</span><span class="sxs-lookup"><span data-stu-id="214df-306">Function</span></span> | <span data-ttu-id="214df-307">說明</span><span class="sxs-lookup"><span data-stu-id="214df-307">Description</span></span> |
| -------- | ----------- |
| <span data-ttu-id="214df-308">CONCAT(x, …)</span><span class="sxs-lookup"><span data-stu-id="214df-308">CONCAT(x, …)</span></span> | <span data-ttu-id="214df-309">傳回字串，該字串是串連兩個或多個字串值的結果。</span><span class="sxs-lookup"><span data-stu-id="214df-309">Returns a string that is the result of concatenating two or more string values.</span></span> |
| <span data-ttu-id="214df-310">LENGTH(x)</span><span class="sxs-lookup"><span data-stu-id="214df-310">LENGTH(x)</span></span> | <span data-ttu-id="214df-311">傳回指定字串運算式的字元數目。</span><span class="sxs-lookup"><span data-stu-id="214df-311">Returns the number of characters of the specified string expression.</span></span>|
| <span data-ttu-id="214df-312">LOWER(x)</span><span class="sxs-lookup"><span data-stu-id="214df-312">LOWER(x)</span></span> | <span data-ttu-id="214df-313">傳回將大寫字元資料轉換成小寫之後的字串運算式。</span><span class="sxs-lookup"><span data-stu-id="214df-313">Returns a string expression after converting uppercase character data to lowercase.</span></span> |
| <span data-ttu-id="214df-314">UPPER(x)</span><span class="sxs-lookup"><span data-stu-id="214df-314">UPPER(x)</span></span> | <span data-ttu-id="214df-315">傳回將小寫字元資料轉換成大寫之後的字串運算式。</span><span class="sxs-lookup"><span data-stu-id="214df-315">Returns a string expression after converting lowercase character data to uppercase.</span></span> |
| <span data-ttu-id="214df-316">SUBSTRING(string, start [, length])</span><span class="sxs-lookup"><span data-stu-id="214df-316">SUBSTRING(string, start [, length])</span></span> | <span data-ttu-id="214df-317">傳回字串運算式的部分，從指定字元以零為起始的位置開始，直到指定的長度，或直到字串的結尾。</span><span class="sxs-lookup"><span data-stu-id="214df-317">Returns part of a string expression starting at the specified character zero-based position and continues to the specified length, or to the end of the string.</span></span> |
| <span data-ttu-id="214df-318">INDEX_OF(string, fragment)</span><span class="sxs-lookup"><span data-stu-id="214df-318">INDEX_OF(string, fragment)</span></span> | <span data-ttu-id="214df-319">傳回第一個指定的字串運算式中，第二個字串運算式第一次出現的開始位置，或者如果找不到字串，則為 -1。</span><span class="sxs-lookup"><span data-stu-id="214df-319">Returns the starting position of the first occurrence of the second string expression within the first specified string expression, or -1 if the string is not found.</span></span>|
| <span data-ttu-id="214df-320">STARTS_WITH(x, y)</span><span class="sxs-lookup"><span data-stu-id="214df-320">STARTS_WITH(x, y)</span></span> | <span data-ttu-id="214df-321">傳回布林值，表示第一個字串運算式是否以第二個字串運算式開頭。</span><span class="sxs-lookup"><span data-stu-id="214df-321">Returns a Boolean indicating whether the first string expression starts with the second.</span></span> |
| <span data-ttu-id="214df-322">ENDS_WITH(x, y)</span><span class="sxs-lookup"><span data-stu-id="214df-322">ENDS_WITH(x, y)</span></span> | <span data-ttu-id="214df-323">傳回布林值，表示第一個字串運算式是否以第二個字串運算式結尾。</span><span class="sxs-lookup"><span data-stu-id="214df-323">Returns a Boolean indicating whether the first string expression ends with the second.</span></span> |
| <span data-ttu-id="214df-324">CONTAINS(x,y)</span><span class="sxs-lookup"><span data-stu-id="214df-324">CONTAINS(x,y)</span></span> | <span data-ttu-id="214df-325">傳回布林值，表示第一個字串運算式是否包含第二個字串運算式。</span><span class="sxs-lookup"><span data-stu-id="214df-325">Returns a Boolean indicating whether the first string expression contains the second.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="214df-326">後續步驟</span><span class="sxs-lookup"><span data-stu-id="214df-326">Next steps</span></span>
<span data-ttu-id="214df-327">了解如何使用 [Azure IoT SDK][lnk-hub-sdks] 在應用程式中執行查詢。</span><span class="sxs-lookup"><span data-stu-id="214df-327">Learn how to execute queries in your apps using [Azure IoT SDKs][lnk-hub-sdks].</span></span>

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
