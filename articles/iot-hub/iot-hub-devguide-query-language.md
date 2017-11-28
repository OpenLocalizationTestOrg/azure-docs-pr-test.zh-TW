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
# <a name="reference---iot-hub-query-language-for-device-twins-jobs-and-message-routing"></a><span data-ttu-id="94b7c-103">參考 - 裝置對應項、作業和訊息路由的 IoT 中樞查詢語言</span><span class="sxs-lookup"><span data-stu-id="94b7c-103">Reference - IoT Hub query language for device twins, jobs, and message routing</span></span>

<span data-ttu-id="94b7c-104">IoT 中樞提供功能強大的類似 SQL 的語言 tooretrieve 資訊有關[裝置雙][ lnk-twins]和[作業][lnk-jobs]，和[訊息路由][lnk-devguide-messaging-routes]。</span><span class="sxs-lookup"><span data-stu-id="94b7c-104">IoT Hub provides a powerful SQL-like language tooretrieve information regarding [device twins][lnk-twins] and [jobs][lnk-jobs], and [message routing][lnk-devguide-messaging-routes].</span></span> <span data-ttu-id="94b7c-105">本文提供︰</span><span class="sxs-lookup"><span data-stu-id="94b7c-105">This article presents:</span></span>

* <span data-ttu-id="94b7c-106">Hello IoT 中樞的查詢語言，簡介 toohello 主要功能和</span><span class="sxs-lookup"><span data-stu-id="94b7c-106">An introduction toohello major features of hello IoT Hub query language, and</span></span>
* <span data-ttu-id="94b7c-107">hello 詳細 hello 語言的描述。</span><span class="sxs-lookup"><span data-stu-id="94b7c-107">hello detailed description of hello language.</span></span>

## <a name="get-started-with-device-twin-queries"></a><span data-ttu-id="94b7c-108">開始使用裝置對應項查詢</span><span class="sxs-lookup"><span data-stu-id="94b7c-108">Get started with device twin queries</span></span>
<span data-ttu-id="94b7c-109">[裝置對應項][lnk-twins]可以包含標籤和屬性形式的任意 JSON 物件。</span><span class="sxs-lookup"><span data-stu-id="94b7c-109">[Device twins][lnk-twins] can contain arbitrary JSON objects as both tags and properties.</span></span> <span data-ttu-id="94b7c-110">IoT 中樞可讓您 tooquery 裝置雙為單一的 JSON 文件，其中包含所有裝置的兩個資訊。</span><span class="sxs-lookup"><span data-stu-id="94b7c-110">IoT Hub enables you tooquery device twins as a single JSON document containing all device twin information.</span></span>
<span data-ttu-id="94b7c-111">比方說，假設您的 IoT 中樞裝置雙具有下列結構的 hello:</span><span class="sxs-lookup"><span data-stu-id="94b7c-111">Assume, for instance, that your IoT hub device twins have hello following structure:</span></span>

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

<span data-ttu-id="94b7c-112">IoT 中樞公開做為文件集合，稱為 hello 裝置雙**裝置**。</span><span class="sxs-lookup"><span data-stu-id="94b7c-112">IoT Hub exposes hello device twins as a document collection called **devices**.</span></span>
<span data-ttu-id="94b7c-113">因此 hello 下列查詢會擷取整組裝置雙 hello:</span><span class="sxs-lookup"><span data-stu-id="94b7c-113">So hello following query retrieves hello whole set of device twins:</span></span>

```sql
SELECT * FROM devices
```

> [!NOTE]
> <span data-ttu-id="94b7c-114">[Azure IoT SDK][lnk-hub-sdks] 支援將大型結果分頁。</span><span class="sxs-lookup"><span data-stu-id="94b7c-114">[Azure IoT SDKs][lnk-hub-sdks] support paging of large results.</span></span>

<span data-ttu-id="94b7c-115">IoT 中樞可讓您 tooretrieve 裝置雙使用任意的條件進行篩選。</span><span class="sxs-lookup"><span data-stu-id="94b7c-115">IoT Hub allows you tooretrieve device twins filtering with arbitrary conditions.</span></span> <span data-ttu-id="94b7c-116">例如，</span><span class="sxs-lookup"><span data-stu-id="94b7c-116">For instance,</span></span>

```sql
SELECT * FROM devices
WHERE tags.location.region = 'US'
```

<span data-ttu-id="94b7c-117">擷取與 hello hello 裝置雙**location.region**標記設定得**美國**。</span><span class="sxs-lookup"><span data-stu-id="94b7c-117">retrieves hello device twins with hello **location.region** tag set too**US**.</span></span>
<span data-ttu-id="94b7c-118">布林運算子和算術比較也受到支援，例如</span><span class="sxs-lookup"><span data-stu-id="94b7c-118">Boolean operators and arithmetic comparisons are supported as well, for example</span></span>

```sql
SELECT * FROM devices
WHERE tags.location.region = 'US'
    AND properties.reported.telemetryConfig.sendFrequencyInSecs >= 60
```

<span data-ttu-id="94b7c-119">擷取所有的裝置雙位於 hello 我們設定 toosend 遙測小於通常每隔一分鐘。</span><span class="sxs-lookup"><span data-stu-id="94b7c-119">retrieves all device twins located in hello US configured toosend telemetry less often than every minute.</span></span> <span data-ttu-id="94b7c-120">為了方便起見，也很可能 toouse 陣列常數以 hello **IN**和**‧ 尼恩之**（不能在） 運算子。</span><span class="sxs-lookup"><span data-stu-id="94b7c-120">As a convenience, it is also possible toouse array constants with hello **IN** and **NIN** (not in) operators.</span></span> <span data-ttu-id="94b7c-121">例如，</span><span class="sxs-lookup"><span data-stu-id="94b7c-121">For instance,</span></span>

```sql
SELECT * FROM devices
WHERE properties.reported.connectivity IN ['wired', 'wifi']
```

<span data-ttu-id="94b7c-122">會擷取所有報告使用 WiFi 或有線連線能力的裝置對應項。</span><span class="sxs-lookup"><span data-stu-id="94b7c-122">retrieves all device twins that reported WiFi or wired connectivity.</span></span> <span data-ttu-id="94b7c-123">它是經常需要 tooidentify 包含特定屬性的所有裝置雙。</span><span class="sxs-lookup"><span data-stu-id="94b7c-123">It is often necessary tooidentify all device twins that contain a specific property.</span></span> <span data-ttu-id="94b7c-124">IoT 中樞支援 hello 函式，`is_defined()`針對此目的。</span><span class="sxs-lookup"><span data-stu-id="94b7c-124">IoT Hub supports hello function `is_defined()` for this purpose.</span></span> <span data-ttu-id="94b7c-125">例如，</span><span class="sxs-lookup"><span data-stu-id="94b7c-125">For instance,</span></span>

```SQL
SELECT * FROM devices
WHERE is_defined(properties.reported.connectivity)
```

<span data-ttu-id="94b7c-126">擷取所有的裝置雙定義 hello`connectivity`報告屬性。</span><span class="sxs-lookup"><span data-stu-id="94b7c-126">retrieved all device twins that define hello `connectivity` reported property.</span></span> <span data-ttu-id="94b7c-127">請參閱 toohello [WHERE 子句][ lnk-query-where] hello 篩選功能 hello 完整參考一節。</span><span class="sxs-lookup"><span data-stu-id="94b7c-127">Refer toohello [WHERE clause][lnk-query-where] section for hello full reference of hello filtering capabilities.</span></span>

<span data-ttu-id="94b7c-128">群組和彙總也受到支援。</span><span class="sxs-lookup"><span data-stu-id="94b7c-128">Grouping and aggregations are also supported.</span></span> <span data-ttu-id="94b7c-129">例如，</span><span class="sxs-lookup"><span data-stu-id="94b7c-129">For instance,</span></span>

```sql
SELECT properties.reported.telemetryConfig.status AS status,
    COUNT() AS numberOfDevices
FROM devices
GROUP BY properties.reported.telemetryConfig.status
```

<span data-ttu-id="94b7c-130">傳回每個遙測設定狀態的 hello 裝置 hello 計數。</span><span class="sxs-lookup"><span data-stu-id="94b7c-130">returns hello count of hello devices in each telemetry configuration status.</span></span>

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

<span data-ttu-id="94b7c-131">hello 前述範例說明其中三個裝置會回報成功設定組態、 兩個仍會套用 hello 組態，以及其中一個報告了錯誤的情況。</span><span class="sxs-lookup"><span data-stu-id="94b7c-131">hello preceding example illustrates a situation where three devices reported successful configuration, two are still applying hello configuration, and one reported an error.</span></span>

### <a name="c-example"></a><span data-ttu-id="94b7c-132">C# 範例</span><span class="sxs-lookup"><span data-stu-id="94b7c-132">C# example</span></span>
<span data-ttu-id="94b7c-133">hello 查詢功能由 hello [C# 服務 SDK] [ lnk-hub-sdks]在 hello **RegistryManager**類別。</span><span class="sxs-lookup"><span data-stu-id="94b7c-133">hello query functionality is exposed by hello [C# service SDK][lnk-hub-sdks] in hello **RegistryManager** class.</span></span>
<span data-ttu-id="94b7c-134">以下是簡單查詢的範例︰</span><span class="sxs-lookup"><span data-stu-id="94b7c-134">Here is an example of a simple query:</span></span>

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

<span data-ttu-id="94b7c-135">請注意如何 hello**查詢**物件具現化 （向上 too1000)，頁面大小，然後擷取多個頁面，透過呼叫 hello **GetNextAsTwinAsync**方法多次。</span><span class="sxs-lookup"><span data-stu-id="94b7c-135">Note how hello **query** object is instantiated with a page size (up too1000), and then multiple pages can be retrieved by calling hello **GetNextAsTwinAsync** methods multiple times.</span></span>
<span data-ttu-id="94b7c-136">請注意該 hello 查詢物件會公開多個**下一步\***、 根據 hello 還原序列化選項所需的 hello 查詢，例如裝置的兩個或工作物件或純文字的 JSON toobe 使用投射時使用。</span><span class="sxs-lookup"><span data-stu-id="94b7c-136">Note that hello query object exposes multiple **Next\***, depending on hello deserialization option required by hello query, such as device twin or job objects, or plain JSON toobe used when using projections.</span></span>

### <a name="nodejs-example"></a><span data-ttu-id="94b7c-137">Node.js 範例</span><span class="sxs-lookup"><span data-stu-id="94b7c-137">Node.js example</span></span>
<span data-ttu-id="94b7c-138">hello 查詢功能由 hello [Azure IoT 服務 SDK for Node.js] [ lnk-hub-sdks]在 hello**登錄**物件。</span><span class="sxs-lookup"><span data-stu-id="94b7c-138">hello query functionality is exposed by hello [Azure IoT service SDK for Node.js][lnk-hub-sdks] in hello **Registry** object.</span></span>
<span data-ttu-id="94b7c-139">以下是簡單查詢的範例︰</span><span class="sxs-lookup"><span data-stu-id="94b7c-139">Here is an example of a simple query:</span></span>

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

<span data-ttu-id="94b7c-140">請注意如何 hello**查詢**物件具現化 （向上 too1000)，頁面大小，然後擷取多個頁面，透過呼叫 hello **nextAsTwin**方法多次。</span><span class="sxs-lookup"><span data-stu-id="94b7c-140">Note how hello **query** object is instantiated with a page size (up too1000), and then multiple pages can be retrieved by calling hello **nextAsTwin** methods multiple times.</span></span>
<span data-ttu-id="94b7c-141">請注意該 hello 查詢物件會公開多個**下一步\***、 根據 hello 還原序列化選項所需的 hello 查詢，例如裝置的兩個或工作物件或純文字的 JSON toobe 使用投射時使用。</span><span class="sxs-lookup"><span data-stu-id="94b7c-141">Note that hello query object exposes multiple **next\***, depending on hello deserialization option required by hello query, such as device twin or job objects, or plain JSON toobe used when using projections.</span></span>

### <a name="limitations"></a><span data-ttu-id="94b7c-142">限制</span><span class="sxs-lookup"><span data-stu-id="94b7c-142">Limitations</span></span>
> [!IMPORTANT]
> <span data-ttu-id="94b7c-143">查詢結果中裝置雙有幾分鐘的延遲尊重 toohello 最新的值。</span><span class="sxs-lookup"><span data-stu-id="94b7c-143">Query results can have a few minutes of delay with respect toohello latest values in device twins.</span></span> <span data-ttu-id="94b7c-144">如果查詢個別裝置雙依識別碼，它一律為偏好 toouse hello 擷取裝置的兩個 API，它一律包含 hello 最新的值，而且具有更高的節流限制。</span><span class="sxs-lookup"><span data-stu-id="94b7c-144">If querying individual device twins by id, it is always preferable toouse hello retrieve device twin API, which always contains hello latest values and has higher throttling limits.</span></span>

<span data-ttu-id="94b7c-145">目前僅支援在基本類型 (沒有物件) 之間進行比較，例如 `... WHERE properties.desired.config = properties.reported.config` 只會在這些屬性具有基本值時才受到支援。</span><span class="sxs-lookup"><span data-stu-id="94b7c-145">Currently, comparisons are supported only between primitive types (no objects), for instance `... WHERE properties.desired.config = properties.reported.config` is supported only if those properties have primitive values.</span></span>

## <a name="get-started-with-jobs-queries"></a><span data-ttu-id="94b7c-146">開始使用作業查詢</span><span class="sxs-lookup"><span data-stu-id="94b7c-146">Get started with jobs queries</span></span>
<span data-ttu-id="94b7c-147">[作業][ lnk-jobs]提供方式 tooexecute 集合的裝置上的作業。</span><span class="sxs-lookup"><span data-stu-id="94b7c-147">[Jobs][lnk-jobs] provide a way tooexecute operations on sets of devices.</span></span> <span data-ttu-id="94b7c-148">每個裝置的兩個包含的 hello 工作都屬於呼叫集合中的 hello 資訊**作業**。</span><span class="sxs-lookup"><span data-stu-id="94b7c-148">Each device twin contains hello information of hello jobs of which it is part in a collection called **jobs**.</span></span>
<span data-ttu-id="94b7c-149">在邏輯上，</span><span class="sxs-lookup"><span data-stu-id="94b7c-149">Logically,</span></span>

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

<span data-ttu-id="94b7c-150">目前，這個集合是可做為查詢**devices.jobs** hello IoT 中樞的查詢語言中。</span><span class="sxs-lookup"><span data-stu-id="94b7c-150">Currently, this collection is queryable as **devices.jobs** in hello IoT Hub query language.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="94b7c-151">目前，查詢裝置雙 （亦即，查詢包含 'FROM '的裝置） 時，會永遠不會傳回 hello 工作屬性。</span><span class="sxs-lookup"><span data-stu-id="94b7c-151">Currently, hello jobs property is never returned when querying device twins (that is, queries that contains 'FROM devices').</span></span> <span data-ttu-id="94b7c-152">此屬性只能使用 `FROM devices.jobs` 直接透過查詢來存取。</span><span class="sxs-lookup"><span data-stu-id="94b7c-152">It can only be accessed directly with queries using `FROM devices.jobs`.</span></span>
>
>

<span data-ttu-id="94b7c-153">比方說，tooget 所有工作 （過去和排程） 會影響單一裝置，您可以都使用下列查詢的 hello:</span><span class="sxs-lookup"><span data-stu-id="94b7c-153">For instance, tooget all jobs (past and scheduled) that affect a single device, you can use hello following query:</span></span>

```sql
SELECT * FROM devices.jobs
WHERE devices.jobs.deviceId = 'myDeviceId'
```

<span data-ttu-id="94b7c-154">請注意如何此查詢提供 hello 裝置的特定狀態 （和可能 hello 直接方法回應） 的每個傳回的工作。</span><span class="sxs-lookup"><span data-stu-id="94b7c-154">Note how this query provides hello device-specific status (and possibly hello direct method response) of each job returned.</span></span>
<span data-ttu-id="94b7c-155">它也是可能 toofilter hello 中的所有物件屬性上的任意布林條件**devices.jobs**集合。</span><span class="sxs-lookup"><span data-stu-id="94b7c-155">It is also possible toofilter with arbitrary Boolean conditions on all object properties in hello **devices.jobs** collection.</span></span>
<span data-ttu-id="94b7c-156">例如，下列查詢 hello:</span><span class="sxs-lookup"><span data-stu-id="94b7c-156">For instance, hello following query:</span></span>

```sql
SELECT * FROM devices.jobs
WHERE devices.jobs.deviceId = 'myDeviceId'
    AND devices.jobs.jobType = 'scheduleTwinUpdate'
    AND devices.jobs.status = 'completed'
    AND devices.jobs.createdTimeUtc > '2016-09-01'
```

<span data-ttu-id="94b7c-157">會針對在 2016 年 9 月之後所建立的裝置 **myDeviceId** 擷取所有已完成的裝置對應項更新作業。</span><span class="sxs-lookup"><span data-stu-id="94b7c-157">retrieves all completed device twin update jobs for device **myDeviceId** that were created after September 2016.</span></span>

<span data-ttu-id="94b7c-158">它也是可能 tooretrieve hello 每一裝置的結果，在單一作業。</span><span class="sxs-lookup"><span data-stu-id="94b7c-158">It is also possible tooretrieve hello per-device outcomes of a single job.</span></span>

```sql
SELECT * FROM devices.jobs
WHERE devices.jobs.jobId = 'myJobId'
```

### <a name="limitations"></a><span data-ttu-id="94b7c-159">限制</span><span class="sxs-lookup"><span data-stu-id="94b7c-159">Limitations</span></span>
<span data-ttu-id="94b7c-160">**devices.jobs** 上的查詢目前不支援︰</span><span class="sxs-lookup"><span data-stu-id="94b7c-160">Currently, queries on **devices.jobs** do not support:</span></span>

* <span data-ttu-id="94b7c-161">投影，因此只有 `SELECT *` 是可行的。</span><span class="sxs-lookup"><span data-stu-id="94b7c-161">Projections, therefore only `SELECT *` is possible.</span></span>
* <span data-ttu-id="94b7c-162">參考 toohello 裝置的兩個加法 toojob 屬性 （請參閱前面一節的 hello） 中的條件。</span><span class="sxs-lookup"><span data-stu-id="94b7c-162">Conditions that refer toohello device twin in addition toojob properties (see hello preceding section).</span></span>
* <span data-ttu-id="94b7c-163">執行彙總，例如計數、平均、分組依據。</span><span class="sxs-lookup"><span data-stu-id="94b7c-163">Performing aggregations, such as count, avg, group by.</span></span>

## <a name="get-started-with-device-to-cloud-message-routes-query-expressions"></a><span data-ttu-id="94b7c-164">開始使用裝置對雲端訊息路由查詢運算式</span><span class="sxs-lookup"><span data-stu-id="94b7c-164">Get started with device-to-cloud message routes query expressions</span></span>

<span data-ttu-id="94b7c-165">使用[裝置到雲端路由][lnk-devguide-messaging-routes]，您可以設定 toodispatch 裝置到雲端訊息 toodifferent 端點針對個別訊息評估的運算式為基礎的 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="94b7c-165">Using [device-to-cloud routes][lnk-devguide-messaging-routes], you can configure IoT Hub toodispatch device-to-cloud messages toodifferent endpoints based on expressions evaluated against individual messages.</span></span>

<span data-ttu-id="94b7c-166">hello 路由[條件][ lnk-query-expressions]使用 hello 條件在兩個與工作的查詢中相同的 IoT 中樞查詢語言。</span><span class="sxs-lookup"><span data-stu-id="94b7c-166">hello route [condition][lnk-query-expressions] uses hello same IoT Hub query language as conditions in twin and job queries.</span></span> <span data-ttu-id="94b7c-167">路由條件會評估 hello 訊息標頭和主體。</span><span class="sxs-lookup"><span data-stu-id="94b7c-167">Route conditions are evaluated on hello message headers and body.</span></span> <span data-ttu-id="94b7c-168">路由的查詢運算式可能只訊息標頭，只有 hello 訊息內文，或兩者訊息標頭和訊息主體。</span><span class="sxs-lookup"><span data-stu-id="94b7c-168">Your routing query expression may involve only message headers, only hello message body, or both message headers and message body.</span></span> <span data-ttu-id="94b7c-169">IoT 中樞假設 hello 標頭和訊息本文的訂單 tooroute 訊息，特定的結構描述和 hello 下列各節描述所需 IoT 中樞 tooproperly 路由內容：</span><span class="sxs-lookup"><span data-stu-id="94b7c-169">IoT Hub assumes a specific schema for hello headers and message body in order tooroute messages, and hello following sections describe what is required for IoT Hub tooproperly route:</span></span>

### <a name="routing-on-message-headers"></a><span data-ttu-id="94b7c-170">依據訊息標頭進行路由</span><span class="sxs-lookup"><span data-stu-id="94b7c-170">Routing on message headers</span></span>

<span data-ttu-id="94b7c-171">IoT 中樞會假設採用下列的訊息標頭路由訊息的 JSON 表示法的 hello:</span><span class="sxs-lookup"><span data-stu-id="94b7c-171">IoT Hub assumes hello following JSON representation of message headers for message routing:</span></span>

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

<span data-ttu-id="94b7c-172">訊息系統屬性會加上 hello`'$'`符號。</span><span class="sxs-lookup"><span data-stu-id="94b7c-172">Message system properties are prefixed with hello `'$'` symbol.</span></span>
<span data-ttu-id="94b7c-173">使用者屬性則一律透過其名稱來存取。</span><span class="sxs-lookup"><span data-stu-id="94b7c-173">User properties are always accessed with their name.</span></span> <span data-ttu-id="94b7c-174">如果使用者的屬性名稱不會 toocoincide 系統屬性 (例如`$to`)，將擷取 hello 使用者屬性，以 hello`$to`運算式。</span><span class="sxs-lookup"><span data-stu-id="94b7c-174">If a user property name happens toocoincide with a system property (such as `$to`), hello user property will be retrieved with hello `$to` expression.</span></span>
<span data-ttu-id="94b7c-175">您永遠可以存取使用方括號 hello 系統屬性`{}`： 例如，您可以使用 hello 運算式`{$to}`tooaccess hello 系統屬性`to`。</span><span class="sxs-lookup"><span data-stu-id="94b7c-175">You can always access hello system property using brackets `{}`: for instance, you can use hello expression `{$to}` tooaccess hello system property `to`.</span></span> <span data-ttu-id="94b7c-176">以方括弧括住的屬性名稱一律會擷取 hello 對應的系統屬性。</span><span class="sxs-lookup"><span data-stu-id="94b7c-176">Bracketed property names always retrieve hello corresponding system property.</span></span>

<span data-ttu-id="94b7c-177">請記住，屬性名稱不區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="94b7c-177">Remember that property names are case insensitive.</span></span>

> [!NOTE]
> <span data-ttu-id="94b7c-178">所有屬性皆為字串。</span><span class="sxs-lookup"><span data-stu-id="94b7c-178">All message properties are strings.</span></span> <span data-ttu-id="94b7c-179">系統屬性，如述 hello[開發人員指南][lnk-devguide-messaging-format]，目前不是在查詢中的可用 toouse。</span><span class="sxs-lookup"><span data-stu-id="94b7c-179">System properties, as described in hello [developer guide][lnk-devguide-messaging-format], are currently not available toouse in queries.</span></span>
>

<span data-ttu-id="94b7c-180">例如，如果您使用`messageType`屬性，您可能會想 tooroute，所有遙測 tooone 端點和所有警示 tooanother 端點。</span><span class="sxs-lookup"><span data-stu-id="94b7c-180">For example, if you use a `messageType` property, you might want tooroute all telemetry tooone endpoint, and all alerts tooanother endpoint.</span></span> <span data-ttu-id="94b7c-181">您可以撰寫下列運算式 tooroute hello 遙測 hello:</span><span class="sxs-lookup"><span data-stu-id="94b7c-181">You can write hello following expression tooroute hello telemetry:</span></span>

```sql
messageType = 'telemetry'
```

<span data-ttu-id="94b7c-182">並 hello 遵循運算式 tooroute hello 警示訊息：</span><span class="sxs-lookup"><span data-stu-id="94b7c-182">And hello following expression tooroute hello alert messages:</span></span>

```sql
messageType = 'alert'
```

<span data-ttu-id="94b7c-183">也支援布林運算式和函式。</span><span class="sxs-lookup"><span data-stu-id="94b7c-183">Boolean expressions and functions are also supported.</span></span> <span data-ttu-id="94b7c-184">這項功能可讓您 toodistinguish 之間嚴重性層級，例如：</span><span class="sxs-lookup"><span data-stu-id="94b7c-184">This feature enables you toodistinguish between severity level, for example:</span></span>

```sql
messageType = 'alerts' AND as_number(severity) <= 2
```

<span data-ttu-id="94b7c-185">請參閱 toohello[運算式與條件][ lnk-query-expressions]一節，以 hello 完整清單支援的運算子和函式。</span><span class="sxs-lookup"><span data-stu-id="94b7c-185">Refer toohello [Expression and conditions][lnk-query-expressions] section for hello full list of supported operators and functions.</span></span>

### <a name="routing-on-message-bodies"></a><span data-ttu-id="94b7c-186">依據訊息內文進行路由</span><span class="sxs-lookup"><span data-stu-id="94b7c-186">Routing on message bodies</span></span>

<span data-ttu-id="94b7c-187">IoT 中樞只路由根據訊息本文內容，如果 hello 訊息內文是正確格式的 JSON 編碼在 utf-8、 utf-16 或 utf-32。</span><span class="sxs-lookup"><span data-stu-id="94b7c-187">IoT Hub can only route based on message body contents if hello message body is properly formed JSON encoded in either UTF-8, UTF-16, or UTF-32.</span></span> <span data-ttu-id="94b7c-188">您必須設定 hello 訊息內容型別的 hello 太`application/json`和 hello 內容編碼方式的 tooone hello 的 hello 訊息標頭 tooallow IoT 中樞 tooroute hello 訊息根據 hello 本文內容中支援 UTF-8 編碼方式。</span><span class="sxs-lookup"><span data-stu-id="94b7c-188">You must set hello content type of hello message too`application/json` and hello content encoding tooone of hello supported UTF encodings in hello message headers tooallow IoT Hub tooroute hello message based on hello body contents.</span></span> <span data-ttu-id="94b7c-189">如果任一 hello 標頭未指定，IoT 中樞將不會嘗試 tooevaluate 涉及 hello 主體針對 hello 訊息的任何查詢運算式。</span><span class="sxs-lookup"><span data-stu-id="94b7c-189">If either of hello headers is not specified, IoT Hub will not attempt tooevaluate any query expression involving hello body against hello message.</span></span> <span data-ttu-id="94b7c-190">如果您的訊息不是 JSON 訊息時，或 hello 訊息未指定 hello 內容類型和內容編碼方式，您可能仍然會使用根據 hello 訊息標頭 tooroute hello 訊息路由傳送的訊息。</span><span class="sxs-lookup"><span data-stu-id="94b7c-190">If your message is not a JSON message, or if hello message does not specify hello content type and content encoding, you may still use message routing tooroute hello message based on hello message headers.</span></span>

<span data-ttu-id="94b7c-191">您可以使用`$body`hello 查詢運算式 tooroute hello 訊息中。</span><span class="sxs-lookup"><span data-stu-id="94b7c-191">You can use `$body` in hello query expression tooroute hello message.</span></span> <span data-ttu-id="94b7c-192">您可以使用簡單的主體參考、 主體陣列參考或主體的多個參照 hello 查詢運算式中。</span><span class="sxs-lookup"><span data-stu-id="94b7c-192">You can use a simple body reference, body array reference, or multiple body references in hello query expression.</span></span> <span data-ttu-id="94b7c-193">您的查詢運算式也可以將內文參考與訊息標頭參考合併。</span><span class="sxs-lookup"><span data-stu-id="94b7c-193">Your query expression can also combine a body reference with a message header reference.</span></span> <span data-ttu-id="94b7c-194">例如，hello 下列都是有效的查詢運算式：</span><span class="sxs-lookup"><span data-stu-id="94b7c-194">For example, hello following are all valid query expressions:</span></span>

```sql
$body.message.Weather.Location.State = 'WA'
$body.Weather.HistoricalData[0].Month = 'Feb'
$body.Weather.Temperature = 50 AND $body.message.Weather.IsEnabled
length($body.Weather.Location.State) = 2
$body.Weather.Temperature = 50 AND Status = 'Active'
```

## <a name="basics-of-an-iot-hub-query"></a><span data-ttu-id="94b7c-195">IoT 中樞查詢的基本概念</span><span class="sxs-lookup"><span data-stu-id="94b7c-195">Basics of an IoT Hub query</span></span>
<span data-ttu-id="94b7c-196">每一個 IoT 中樞查詢都包含 SELECT 和 FROM 子句，以及選擇性的 WHERE 和 GROUP BY 子句。</span><span class="sxs-lookup"><span data-stu-id="94b7c-196">Every IoT Hub query consists of a SELECT and FROM clauses and by optional WHERE and GROUP BY clauses.</span></span> <span data-ttu-id="94b7c-197">每個查詢都會在 JSON 文件的集合上執行，例如裝置對應項。</span><span class="sxs-lookup"><span data-stu-id="94b7c-197">Every query is run on a collection of JSON documents, for example device twins.</span></span> <span data-ttu-id="94b7c-198">hello FROM 子句指出 hello 反覆運算上的文件集合 toobe (**裝置**或**devices.jobs**)。</span><span class="sxs-lookup"><span data-stu-id="94b7c-198">hello FROM clause indicates hello document collection toobe iterated on (**devices** or **devices.jobs**).</span></span> <span data-ttu-id="94b7c-199">然後，hello 的 hello 才會套用子句中的篩選器。</span><span class="sxs-lookup"><span data-stu-id="94b7c-199">Then, hello filter in hello WHERE clause is applied.</span></span> <span data-ttu-id="94b7c-200">彙總，hello 這個步驟的結果會以指定在 hello GROUP BY 子句分組，並針對每個群組，產生一個資料列 hello SELECT 子句中所指定。</span><span class="sxs-lookup"><span data-stu-id="94b7c-200">With aggregations, hello results of this step are grouped as specified in hello GROUP BY clause and, for each group, a row is generated as specified in hello SELECT clause.</span></span>

```sql
SELECT <select_list>
FROM <from_specification>
[WHERE <filter_condition>]
[GROUP BY <group_specification>]
```

## <a name="from-clause"></a><span data-ttu-id="94b7c-201">FROM 子句</span><span class="sxs-lookup"><span data-stu-id="94b7c-201">FROM clause</span></span>
<span data-ttu-id="94b7c-202">hello **< from_specification > 從**子句可指定只有兩個值：**從裝置**，tooquery 裝置雙，或**從 devices.jobs**，tooquery 作業每個裝置詳細資料。</span><span class="sxs-lookup"><span data-stu-id="94b7c-202">hello **FROM <from_specification>** clause can assume only two values: **FROM devices**, tooquery device twins, or **FROM devices.jobs**, tooquery job per-device details.</span></span>

## <a name="where-clause"></a><span data-ttu-id="94b7c-203">WHERE 子句</span><span class="sxs-lookup"><span data-stu-id="94b7c-203">WHERE clause</span></span>
<span data-ttu-id="94b7c-204">hello**其中 < filter_condition >**子句是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="94b7c-204">hello **WHERE <filter_condition>** clause is optional.</span></span> <span data-ttu-id="94b7c-205">它會指定一或多個條件 hello 從集合中的 hello JSON 文件必須滿足 toobe 納入 hello 結果的一部分。</span><span class="sxs-lookup"><span data-stu-id="94b7c-205">It specifies one or more conditions that hello JSON documents in hello FROM collection must satisfy toobe included as part of hello result.</span></span> <span data-ttu-id="94b7c-206">任何 JSON 文件都必須評估 hello 指定條件太"true"toobe 會包含在 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="94b7c-206">Any JSON document must evaluate hello specified conditions too"true" toobe included in hello result.</span></span>

<span data-ttu-id="94b7c-207">hello 允許一節所述條件[運算式和條件][lnk-query-expressions]。</span><span class="sxs-lookup"><span data-stu-id="94b7c-207">hello allowed conditions are described in section [Expressions and conditions][lnk-query-expressions].</span></span>

## <a name="select-clause"></a><span data-ttu-id="94b7c-208">SELECT 子句</span><span class="sxs-lookup"><span data-stu-id="94b7c-208">SELECT clause</span></span>
<span data-ttu-id="94b7c-209">hello SELECT 子句 (**SELECT < select_list >**) 是必要項，指定從 hello 查詢會擷取哪些值。</span><span class="sxs-lookup"><span data-stu-id="94b7c-209">hello SELECT clause (**SELECT <select_list>**) is mandatory and specifies what values are retrieved from hello query.</span></span> <span data-ttu-id="94b7c-210">它會指定 hello JSON 值 toobe 用 toogenerate 新 JSON 物件。</span><span class="sxs-lookup"><span data-stu-id="94b7c-210">It specifies hello JSON values toobe used toogenerate new JSON objects.</span></span>
<span data-ttu-id="94b7c-211">每個項目 hello hello FROM 集合的篩選 （及選擇性地群組） 的子集、 hello 投影階段會產生新的 JSON 物件，建構 hello hello SELECT 子句中指定的值。</span><span class="sxs-lookup"><span data-stu-id="94b7c-211">For each element of hello filtered (and optionally grouped) subset of hello FROM collection, hello projection phase generates a new JSON object, constructed with hello values specified in hello SELECT clause.</span></span>

<span data-ttu-id="94b7c-212">以下是 hello 文法 hello SELECT 子句：</span><span class="sxs-lookup"><span data-stu-id="94b7c-212">Following is hello grammar of hello SELECT clause:</span></span>

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

<span data-ttu-id="94b7c-213">其中**attribute_name**參考 tooany hello 從集合中的 hello JSON 文件屬性。</span><span class="sxs-lookup"><span data-stu-id="94b7c-213">where **attribute_name** refers tooany property of hello JSON document in hello FROM collection.</span></span> <span data-ttu-id="94b7c-214">SELECT 子句的一些範例可以在 hello[開始使用裝置的兩個查詢][ lnk-query-getstarted] > 一節。</span><span class="sxs-lookup"><span data-stu-id="94b7c-214">Some examples of SELECT clauses can be found in hello [Getting started with device twin queries][lnk-query-getstarted] section.</span></span>

<span data-ttu-id="94b7c-215">與 **SELECT \*** 不同的選取範圍子句目前只支援在裝置對應項的彙總查詢中使用。</span><span class="sxs-lookup"><span data-stu-id="94b7c-215">Currently, selection clauses different than **SELECT \*** are only supported in aggregate queries on device twins.</span></span>

## <a name="group-by-clause"></a><span data-ttu-id="94b7c-216">GROUP BY 子句</span><span class="sxs-lookup"><span data-stu-id="94b7c-216">GROUP BY clause</span></span>
<span data-ttu-id="94b7c-217">hello **GROUP BY < group_specification >**子句是選擇性步驟，可以在之後 hello 篩選 hello 中 WHERE 子句，指定執行之前指定 hello 中的 hello 投影選取。</span><span class="sxs-lookup"><span data-stu-id="94b7c-217">hello **GROUP BY <group_specification>** clause is an optional step that can be executed after hello filter specified in hello WHERE clause, and before hello projection specified in hello SELECT.</span></span> <span data-ttu-id="94b7c-218">它會群組 hello 屬性值為基礎的文件。</span><span class="sxs-lookup"><span data-stu-id="94b7c-218">It groups documents based on hello value of an attribute.</span></span> <span data-ttu-id="94b7c-219">這些群組是彙總使用的 toogenerate hello SELECT 子句中所指定的值。</span><span class="sxs-lookup"><span data-stu-id="94b7c-219">These groups are used toogenerate aggregated values as specified in hello SELECT clause.</span></span>

<span data-ttu-id="94b7c-220">使用 GROUP BY 的查詢範例如下︰</span><span class="sxs-lookup"><span data-stu-id="94b7c-220">An example of a query using GROUP BY is:</span></span>

```sql
SELECT properties.reported.telemetryConfig.status AS status,
    COUNT() AS numberOfDevices
FROM devices
GROUP BY properties.reported.telemetryConfig.status
```

<span data-ttu-id="94b7c-221">hello GROUP by 的正式語法是：</span><span class="sxs-lookup"><span data-stu-id="94b7c-221">hello formal syntax for GROUP BY is:</span></span>

```
GROUP BY <group_by_element>
<group_by_element> :==
    attribute_name
    | < group_by_element > '.' attribute_name
```

<span data-ttu-id="94b7c-222">其中**attribute_name**參考 tooany hello 從集合中的 hello JSON 文件屬性。</span><span class="sxs-lookup"><span data-stu-id="94b7c-222">where **attribute_name** refers tooany property of hello JSON document in hello FROM collection.</span></span>

<span data-ttu-id="94b7c-223">目前，hello GROUP BY 子句只能查詢時，支援裝置雙。</span><span class="sxs-lookup"><span data-stu-id="94b7c-223">Currently, hello GROUP BY clause is only supported when querying device twins.</span></span>

## <a name="expressions-and-conditions"></a><span data-ttu-id="94b7c-224">運算式和條件</span><span class="sxs-lookup"><span data-stu-id="94b7c-224">Expressions and conditions</span></span>
<span data-ttu-id="94b7c-225">概括而言，運算式：</span><span class="sxs-lookup"><span data-stu-id="94b7c-225">At a high level, an *expression*:</span></span>

* <span data-ttu-id="94b7c-226">評估 tooan JSON 型別 （例如布林值、 數字、 字串、 陣列或物件），執行個體和</span><span class="sxs-lookup"><span data-stu-id="94b7c-226">Evaluates tooan instance of a JSON type (such as Boolean, number, string, array, or object), and</span></span>
* <span data-ttu-id="94b7c-227">定義處理來自 hello 裝置 JSON 文件與使用內建運算子和函數的常數。</span><span class="sxs-lookup"><span data-stu-id="94b7c-227">Is defined by manipulating data coming from hello device JSON document and constants using built-in operators and functions.</span></span>

<span data-ttu-id="94b7c-228">*條件*是評估 tooa 布林值運算式。</span><span class="sxs-lookup"><span data-stu-id="94b7c-228">*Conditions* are expressions that evaluate tooa Boolean.</span></span> <span data-ttu-id="94b7c-229">不同於布林值的任何常數**true**會被視為**false** (包括**null**，**未定義**，任何物件或陣列的執行個體，任何字串，並清楚 hello 布林值**false**)。</span><span class="sxs-lookup"><span data-stu-id="94b7c-229">Any constant different than Boolean **true** is considered as **false** (including **null**, **undefined**, any object or array instance, any string, and clearly hello Boolean **false**).</span></span>

<span data-ttu-id="94b7c-230">hello 運算式的語法為：</span><span class="sxs-lookup"><span data-stu-id="94b7c-230">hello syntax for expressions is:</span></span>

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

<span data-ttu-id="94b7c-231">其中：</span><span class="sxs-lookup"><span data-stu-id="94b7c-231">where:</span></span>

| <span data-ttu-id="94b7c-232">符號</span><span class="sxs-lookup"><span data-stu-id="94b7c-232">Symbol</span></span> | <span data-ttu-id="94b7c-233">定義</span><span class="sxs-lookup"><span data-stu-id="94b7c-233">Definition</span></span> |
| --- | --- |
| <span data-ttu-id="94b7c-234">attribute_name</span><span class="sxs-lookup"><span data-stu-id="94b7c-234">attribute_name</span></span> | <span data-ttu-id="94b7c-235">任何屬性的 hello JSON 文件以 hello **FROM**集合。</span><span class="sxs-lookup"><span data-stu-id="94b7c-235">Any property of hello JSON document in hello **FROM** collection.</span></span> |
| <span data-ttu-id="94b7c-236">binary_operator</span><span class="sxs-lookup"><span data-stu-id="94b7c-236">binary_operator</span></span> | <span data-ttu-id="94b7c-237">Hello 中列出的任何二元運算子[運算子](#operators)> 一節。</span><span class="sxs-lookup"><span data-stu-id="94b7c-237">Any binary operator listed in hello [Operators](#operators) section.</span></span> |
| <span data-ttu-id="94b7c-238">function_name</span><span class="sxs-lookup"><span data-stu-id="94b7c-238">function_name</span></span>| <span data-ttu-id="94b7c-239">任何函式列在 hello[函式](#functions)> 一節。</span><span class="sxs-lookup"><span data-stu-id="94b7c-239">Any function listed in hello [Functions](#functions) section.</span></span> |
| <span data-ttu-id="94b7c-240">decimal_literal</span><span class="sxs-lookup"><span data-stu-id="94b7c-240">decimal_literal</span></span> |<span data-ttu-id="94b7c-241">以小數點標記法表示的浮點數。</span><span class="sxs-lookup"><span data-stu-id="94b7c-241">A float expressed in decimal notation.</span></span> |
| <span data-ttu-id="94b7c-242">hexadecimal_literal</span><span class="sxs-lookup"><span data-stu-id="94b7c-242">hexadecimal_literal</span></span> |<span data-ttu-id="94b7c-243">Hello 字串所表示的數字 '0x' 後面接著十六進位數字的字串。</span><span class="sxs-lookup"><span data-stu-id="94b7c-243">A number expressed by hello string ‘0x’ followed by a string of hexadecimal digits.</span></span> |
| <span data-ttu-id="94b7c-244">string_literal</span><span class="sxs-lookup"><span data-stu-id="94b7c-244">string_literal</span></span> |<span data-ttu-id="94b7c-245">字串常值是由零個或多個 Unicode 字元序列或逸出序列所表示的 Unicode 字串。</span><span class="sxs-lookup"><span data-stu-id="94b7c-245">String literals are Unicode strings represented by a sequence of zero or more Unicode characters or escape sequences.</span></span> <span data-ttu-id="94b7c-246">字串常值會以單引號 (所有格符號：') 或雙引號 (引號：") 括起來。</span><span class="sxs-lookup"><span data-stu-id="94b7c-246">String literals are enclosed in single quotes (apostrophe: ' ) or double quotes (quotation mark: ").</span></span> <span data-ttu-id="94b7c-247">允許的逸出︰`\'`、`\"`、`\\`、`\uXXXX` (適用於由 4 個十六進位數字所定義的 Unicode 字元)。</span><span class="sxs-lookup"><span data-stu-id="94b7c-247">Allowed escapes: `\'`, `\"`, `\\`, `\uXXXX` for Unicode characters defined by 4 hexadecimal digits.</span></span> |

### <a name="operators"></a><span data-ttu-id="94b7c-248">運算子</span><span class="sxs-lookup"><span data-stu-id="94b7c-248">Operators</span></span>
<span data-ttu-id="94b7c-249">支援下列運算子的 hello:</span><span class="sxs-lookup"><span data-stu-id="94b7c-249">hello following operators are supported:</span></span>

| <span data-ttu-id="94b7c-250">系列</span><span class="sxs-lookup"><span data-stu-id="94b7c-250">Family</span></span> | <span data-ttu-id="94b7c-251">運算子</span><span class="sxs-lookup"><span data-stu-id="94b7c-251">Operators</span></span> |
| --- | --- |
| <span data-ttu-id="94b7c-252">算術</span><span class="sxs-lookup"><span data-stu-id="94b7c-252">Arithmetic</span></span> |<span data-ttu-id="94b7c-253">+、-、*、/、%</span><span class="sxs-lookup"><span data-stu-id="94b7c-253">+,-,*,/,%</span></span> |
| <span data-ttu-id="94b7c-254">邏輯</span><span class="sxs-lookup"><span data-stu-id="94b7c-254">Logical</span></span> |<span data-ttu-id="94b7c-255">AND、OR、NOT</span><span class="sxs-lookup"><span data-stu-id="94b7c-255">AND, OR, NOT</span></span> |
| <span data-ttu-id="94b7c-256">比較</span><span class="sxs-lookup"><span data-stu-id="94b7c-256">Comparison</span></span> |<span data-ttu-id="94b7c-257">=、!=、<、>、<=、>=、<></span><span class="sxs-lookup"><span data-stu-id="94b7c-257">=, !=, <, >, <=, >=, <></span></span> |

### <a name="functions"></a><span data-ttu-id="94b7c-258">Functions</span><span class="sxs-lookup"><span data-stu-id="94b7c-258">Functions</span></span>
<span data-ttu-id="94b7c-259">當查詢雙和工作，才支援的 hello 函式為：</span><span class="sxs-lookup"><span data-stu-id="94b7c-259">When querying twins and jobs hello only supported function is:</span></span>

| <span data-ttu-id="94b7c-260">函式</span><span class="sxs-lookup"><span data-stu-id="94b7c-260">Function</span></span> | <span data-ttu-id="94b7c-261">說明</span><span class="sxs-lookup"><span data-stu-id="94b7c-261">Description</span></span> |
| -------- | ----------- |
| <span data-ttu-id="94b7c-262">IS_DEFINED(property)</span><span class="sxs-lookup"><span data-stu-id="94b7c-262">IS_DEFINED(property)</span></span> | <span data-ttu-id="94b7c-263">傳回布林值，指出如果 hello 尚未指派屬性值 (包括`null`)。</span><span class="sxs-lookup"><span data-stu-id="94b7c-263">Returns a Boolean indicating if hello property has been assigned a value (including `null`).</span></span> |

<span data-ttu-id="94b7c-264">在路由情況下，支援下列數學函式的 hello:</span><span class="sxs-lookup"><span data-stu-id="94b7c-264">In routes conditions, hello following math functions are supported:</span></span>

| <span data-ttu-id="94b7c-265">函式</span><span class="sxs-lookup"><span data-stu-id="94b7c-265">Function</span></span> | <span data-ttu-id="94b7c-266">說明</span><span class="sxs-lookup"><span data-stu-id="94b7c-266">Description</span></span> |
| -------- | ----------- |
| <span data-ttu-id="94b7c-267">ABS(x)</span><span class="sxs-lookup"><span data-stu-id="94b7c-267">ABS(x)</span></span> | <span data-ttu-id="94b7c-268">傳回 hello 絕對 （正） 值 hello 指定數值運算式。</span><span class="sxs-lookup"><span data-stu-id="94b7c-268">Returns hello absolute (positive) value of hello specified numeric expression.</span></span> |
| <span data-ttu-id="94b7c-269">EXP(x)</span><span class="sxs-lookup"><span data-stu-id="94b7c-269">EXP(x)</span></span> | <span data-ttu-id="94b7c-270">傳回的 hello hello 指數值指定數值運算式 (e ^ x)。</span><span class="sxs-lookup"><span data-stu-id="94b7c-270">Returns hello exponential value of hello specified numeric expression (e^x).</span></span> |
| <span data-ttu-id="94b7c-271">POWER(x,y)</span><span class="sxs-lookup"><span data-stu-id="94b7c-271">POWER(x,y)</span></span> | <span data-ttu-id="94b7c-272">傳回 hello hello 指定的值運算式 toohello 指定的冪 (x ^ y)。</span><span class="sxs-lookup"><span data-stu-id="94b7c-272">Returns hello value of hello specified expression toohello specified power (x^y).</span></span>|
| <span data-ttu-id="94b7c-273">SQUARE(x)</span><span class="sxs-lookup"><span data-stu-id="94b7c-273">SQUARE(x)</span></span> | <span data-ttu-id="94b7c-274">傳回 hello 正方形 hello 的指定數字值。</span><span class="sxs-lookup"><span data-stu-id="94b7c-274">Returns hello square of hello specified numeric value.</span></span> |
| <span data-ttu-id="94b7c-275">CEILING(x)</span><span class="sxs-lookup"><span data-stu-id="94b7c-275">CEILING(x)</span></span> | <span data-ttu-id="94b7c-276">傳回 hello 最小整數值大於或等於，hello 指定數值運算式。</span><span class="sxs-lookup"><span data-stu-id="94b7c-276">Returns hello smallest integer value greater than, or equal to, hello specified numeric expression.</span></span> |
| <span data-ttu-id="94b7c-277">FLOOR(x)</span><span class="sxs-lookup"><span data-stu-id="94b7c-277">FLOOR(x)</span></span> | <span data-ttu-id="94b7c-278">傳回小於 hello 最大整數 toohello 或等於指定數值運算式。</span><span class="sxs-lookup"><span data-stu-id="94b7c-278">Returns hello largest integer less than or equal toohello specified numeric expression.</span></span> |
| <span data-ttu-id="94b7c-279">SIGN(x)</span><span class="sxs-lookup"><span data-stu-id="94b7c-279">SIGN(x)</span></span> | <span data-ttu-id="94b7c-280">傳回 hello 正 (+ 1)、 零 (0)，或 hello 負 (-1) 號指定數值運算式。</span><span class="sxs-lookup"><span data-stu-id="94b7c-280">Returns hello positive (+1), zero (0), or negative (-1) sign of hello specified numeric expression.</span></span>|
| <span data-ttu-id="94b7c-281">SQRT(x)</span><span class="sxs-lookup"><span data-stu-id="94b7c-281">SQRT(x)</span></span> | <span data-ttu-id="94b7c-282">傳回 hello 正方形 hello 的指定數字值。</span><span class="sxs-lookup"><span data-stu-id="94b7c-282">Returns hello square of hello specified numeric value.</span></span> |

<span data-ttu-id="94b7c-283">在路由情況下，支援下列型別檢查和轉換函式的 hello:</span><span class="sxs-lookup"><span data-stu-id="94b7c-283">In routes conditions, hello following type checking and casting functions are supported:</span></span>

| <span data-ttu-id="94b7c-284">函式</span><span class="sxs-lookup"><span data-stu-id="94b7c-284">Function</span></span> | <span data-ttu-id="94b7c-285">說明</span><span class="sxs-lookup"><span data-stu-id="94b7c-285">Description</span></span> |
| -------- | ----------- |
| <span data-ttu-id="94b7c-286">AS_NUMBER</span><span class="sxs-lookup"><span data-stu-id="94b7c-286">AS_NUMBER</span></span> | <span data-ttu-id="94b7c-287">將轉換 hello 輸入的字串 tooa 數。</span><span class="sxs-lookup"><span data-stu-id="94b7c-287">Converts hello input string tooa number.</span></span> <span data-ttu-id="94b7c-288">如果輸入是一個數字則為 `noop`；如果字串不是數字則為 `Undefined`。</span><span class="sxs-lookup"><span data-stu-id="94b7c-288">`noop` if input is a number; `Undefined` if string does not represent a number.</span></span>|
| <span data-ttu-id="94b7c-289">IS_ARRAY</span><span class="sxs-lookup"><span data-stu-id="94b7c-289">IS_ARRAY</span></span> | <span data-ttu-id="94b7c-290">傳回布林值，指出是否指定運算式的 hello hello 類型是陣列。</span><span class="sxs-lookup"><span data-stu-id="94b7c-290">Returns a Boolean value indicating if hello type of hello specified expression is an array.</span></span> |
| <span data-ttu-id="94b7c-291">IS_BOOL</span><span class="sxs-lookup"><span data-stu-id="94b7c-291">IS_BOOL</span></span> | <span data-ttu-id="94b7c-292">傳回布林值，指出是否 hello hello 類型指定的運算式是布林值。</span><span class="sxs-lookup"><span data-stu-id="94b7c-292">Returns a Boolean value indicating if hello type of hello specified expression is a Boolean.</span></span> |
| <span data-ttu-id="94b7c-293">IS_DEFINED</span><span class="sxs-lookup"><span data-stu-id="94b7c-293">IS_DEFINED</span></span> | <span data-ttu-id="94b7c-294">傳回布林值，指出如果 hello 尚未指派屬性值。</span><span class="sxs-lookup"><span data-stu-id="94b7c-294">Returns a Boolean indicating if hello property has been assigned a value.</span></span> |
| <span data-ttu-id="94b7c-295">IS_NULL</span><span class="sxs-lookup"><span data-stu-id="94b7c-295">IS_NULL</span></span> | <span data-ttu-id="94b7c-296">傳回布林值，指出是否 hello hello 類型指定的運算式為 null。</span><span class="sxs-lookup"><span data-stu-id="94b7c-296">Returns a Boolean value indicating if hello type of hello specified expression is null.</span></span> |
| <span data-ttu-id="94b7c-297">IS_NUMBER</span><span class="sxs-lookup"><span data-stu-id="94b7c-297">IS_NUMBER</span></span> | <span data-ttu-id="94b7c-298">傳回布林值，指出是否 hello hello 類型指定的運算式是一個數字。</span><span class="sxs-lookup"><span data-stu-id="94b7c-298">Returns a Boolean value indicating if hello type of hello specified expression is a number.</span></span> |
| <span data-ttu-id="94b7c-299">IS_OBJECT</span><span class="sxs-lookup"><span data-stu-id="94b7c-299">IS_OBJECT</span></span> | <span data-ttu-id="94b7c-300">傳回布林值，指出是否 hello hello 類型指定的運算式是一個 JSON 物件。</span><span class="sxs-lookup"><span data-stu-id="94b7c-300">Returns a Boolean value indicating if hello type of hello specified expression is a JSON object.</span></span> |
| <span data-ttu-id="94b7c-301">IS_PRIMITIVE</span><span class="sxs-lookup"><span data-stu-id="94b7c-301">IS_PRIMITIVE</span></span> | <span data-ttu-id="94b7c-302">傳回布林值，指出是否 hello hello 類型指定運算式是基本型別 (字串、 布林值，數字或`null`)。</span><span class="sxs-lookup"><span data-stu-id="94b7c-302">Returns a Boolean value indicating if hello type of hello specified expression is a primitive (string, Boolean, numeric or `null`).</span></span> |
| <span data-ttu-id="94b7c-303">IS_STRING</span><span class="sxs-lookup"><span data-stu-id="94b7c-303">IS_STRING</span></span> | <span data-ttu-id="94b7c-304">傳回布林值，指出是否 hello hello 類型指定的運算式是字串。</span><span class="sxs-lookup"><span data-stu-id="94b7c-304">Returns a Boolean value indicating if hello type of hello specified expression is a string.</span></span> |

<span data-ttu-id="94b7c-305">在路由情況下，支援下列字串函數的 hello:</span><span class="sxs-lookup"><span data-stu-id="94b7c-305">In routes conditions, hello following string functions are supported:</span></span>

| <span data-ttu-id="94b7c-306">函式</span><span class="sxs-lookup"><span data-stu-id="94b7c-306">Function</span></span> | <span data-ttu-id="94b7c-307">說明</span><span class="sxs-lookup"><span data-stu-id="94b7c-307">Description</span></span> |
| -------- | ----------- |
| <span data-ttu-id="94b7c-308">CONCAT(x, …)</span><span class="sxs-lookup"><span data-stu-id="94b7c-308">CONCAT(x, …)</span></span> | <span data-ttu-id="94b7c-309">傳回字串 hello 因產生的串連兩個或多個字串值。</span><span class="sxs-lookup"><span data-stu-id="94b7c-309">Returns a string that is hello result of concatenating two or more string values.</span></span> |
| <span data-ttu-id="94b7c-310">LENGTH(x)</span><span class="sxs-lookup"><span data-stu-id="94b7c-310">LENGTH(x)</span></span> | <span data-ttu-id="94b7c-311">傳回 hello 數目的 hello 字元指定的字串運算式。</span><span class="sxs-lookup"><span data-stu-id="94b7c-311">Returns hello number of characters of hello specified string expression.</span></span>|
| <span data-ttu-id="94b7c-312">LOWER(x)</span><span class="sxs-lookup"><span data-stu-id="94b7c-312">LOWER(x)</span></span> | <span data-ttu-id="94b7c-313">傳回將大寫字元資料 toolowercase 轉換後的字串運算式。</span><span class="sxs-lookup"><span data-stu-id="94b7c-313">Returns a string expression after converting uppercase character data toolowercase.</span></span> |
| <span data-ttu-id="94b7c-314">UPPER(x)</span><span class="sxs-lookup"><span data-stu-id="94b7c-314">UPPER(x)</span></span> | <span data-ttu-id="94b7c-315">傳回將小寫字元資料 toouppercase 轉換後的字串運算式。</span><span class="sxs-lookup"><span data-stu-id="94b7c-315">Returns a string expression after converting lowercase character data toouppercase.</span></span> |
| <span data-ttu-id="94b7c-316">SUBSTRING(string, start [, length])</span><span class="sxs-lookup"><span data-stu-id="94b7c-316">SUBSTRING(string, start [, length])</span></span> | <span data-ttu-id="94b7c-317">Hello 處開始的字串運算式的傳回屬於指定的字元以零為起始的位置，並繼續 toohello 指定長度或 toohello hello 字串的結尾。</span><span class="sxs-lookup"><span data-stu-id="94b7c-317">Returns part of a string expression starting at hello specified character zero-based position and continues toohello specified length, or toohello end of hello string.</span></span> |
| <span data-ttu-id="94b7c-318">INDEX_OF(string, fragment)</span><span class="sxs-lookup"><span data-stu-id="94b7c-318">INDEX_OF(string, fragment)</span></span> | <span data-ttu-id="94b7c-319">傳回開始 hello 內 hello 第一個指定的字串運算式，則為-1 hello 第二個字串運算式的第一次出現的位置，如果找不到 hello 字串 hello。</span><span class="sxs-lookup"><span data-stu-id="94b7c-319">Returns hello starting position of hello first occurrence of hello second string expression within hello first specified string expression, or -1 if hello string is not found.</span></span>|
| <span data-ttu-id="94b7c-320">STARTS_WITH(x, y)</span><span class="sxs-lookup"><span data-stu-id="94b7c-320">STARTS_WITH(x, y)</span></span> | <span data-ttu-id="94b7c-321">傳回布林值，指出 hello 第一個字串運算式的開頭是否 hello 第二個。</span><span class="sxs-lookup"><span data-stu-id="94b7c-321">Returns a Boolean indicating whether hello first string expression starts with hello second.</span></span> |
| <span data-ttu-id="94b7c-322">ENDS_WITH(x, y)</span><span class="sxs-lookup"><span data-stu-id="94b7c-322">ENDS_WITH(x, y)</span></span> | <span data-ttu-id="94b7c-323">傳回布林值，指出是否 hello 第一個字串運算式的結尾 hello 第二個。</span><span class="sxs-lookup"><span data-stu-id="94b7c-323">Returns a Boolean indicating whether hello first string expression ends with hello second.</span></span> |
| <span data-ttu-id="94b7c-324">CONTAINS(x,y)</span><span class="sxs-lookup"><span data-stu-id="94b7c-324">CONTAINS(x,y)</span></span> | <span data-ttu-id="94b7c-325">傳回布林值，指出是否 hello 第一個字串運算式中第二個包含 hello。</span><span class="sxs-lookup"><span data-stu-id="94b7c-325">Returns a Boolean indicating whether hello first string expression contains hello second.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="94b7c-326">後續步驟</span><span class="sxs-lookup"><span data-stu-id="94b7c-326">Next steps</span></span>
<span data-ttu-id="94b7c-327">了解如何 tooexecute 查詢使用的應用程式中[Azure IoT Sdk][lnk-hub-sdks]。</span><span class="sxs-lookup"><span data-stu-id="94b7c-327">Learn how tooexecute queries in your apps using [Azure IoT SDKs][lnk-hub-sdks].</span></span>

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
