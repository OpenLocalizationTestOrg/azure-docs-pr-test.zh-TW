---
title: "aaaUnderstand Azure IoT 中樞作業 |Microsoft 文件"
description: "開發人員指南-排定多個裝置上的作業 toorun 連接 tooyour IoT 中樞。 作業可以在多個裝置上更新標籤和所需的屬性，並叫用直接方法。"
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: fe78458f-4f14-4358-ac83-4f7bd14ee8da
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/30/2016
ms.author: juanpere
ms.openlocfilehash: 8be134e6c379feae5087df8f562a74505c57afee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="schedule-jobs-on-multiple-devices"></a><span data-ttu-id="1a83c-104">排程多個裝置上的作業</span><span class="sxs-lookup"><span data-stu-id="1a83c-104">Schedule jobs on multiple devices</span></span>
## <a name="overview"></a><span data-ttu-id="1a83c-105">概觀</span><span class="sxs-lookup"><span data-stu-id="1a83c-105">Overview</span></span>
<span data-ttu-id="1a83c-106">如前面幾篇文章所述，Azure IoT 中樞可啟用許多建置組塊 ([裝置對應項屬性和標籤][lnk-twin-devguide]和[直接方法][lnk-dev-methods])。</span><span class="sxs-lookup"><span data-stu-id="1a83c-106">As described by previous articles, Azure IoT Hub enables a number of building blocks ([device twin properties and tags][lnk-twin-devguide] and [direct methods][lnk-dev-methods]).</span></span>  <span data-ttu-id="1a83c-107">一般而言後, 端應用程式啟用裝置系統管理員和操作員 tooupdate 並與其互動 IoT 裝置之間能夠大量並在排定的時間。</span><span class="sxs-lookup"><span data-stu-id="1a83c-107">Typically, back-end apps enable device administrators and operators tooupdate and interact with IoT devices in bulk and at a scheduled time.</span></span>  <span data-ttu-id="1a83c-108">工作會封裝在排程時間的 hello 執行裝置的兩個更新和直接的方法，針對一組裝置。</span><span class="sxs-lookup"><span data-stu-id="1a83c-108">Jobs encapsulate hello execution of device twin updates and direct methods against a set of devices at a schedule time.</span></span>  <span data-ttu-id="1a83c-109">例如，操作員會使用後端應用程式會起始與追蹤工作 tooreboot 一組裝置不會干擾 toohello hello 建置作業一次建置 43 和樓層 3。</span><span class="sxs-lookup"><span data-stu-id="1a83c-109">For example, an operator would use a back-end app that would initiate and track a job tooreboot a set of devices in building 43 and floor 3 at a time that would not be disruptive toohello operations of hello building.</span></span>

### <a name="when-toouse"></a><span data-ttu-id="1a83c-110">當 toouse</span><span class="sxs-lookup"><span data-stu-id="1a83c-110">When toouse</span></span>
<span data-ttu-id="1a83c-111">請考慮使用工作的時機： 方案後端需要 tooschedule 和追蹤進度任何 hello 一組裝置的下列活動：</span><span class="sxs-lookup"><span data-stu-id="1a83c-111">Consider using jobs when: a solution back end needs tooschedule and track progress any of hello following activities on a set of device:</span></span>

* <span data-ttu-id="1a83c-112">更新所需屬性</span><span class="sxs-lookup"><span data-stu-id="1a83c-112">Update desired properties</span></span>
* <span data-ttu-id="1a83c-113">更新標籤</span><span class="sxs-lookup"><span data-stu-id="1a83c-113">Update tags</span></span>
* <span data-ttu-id="1a83c-114">叫用直接方法</span><span class="sxs-lookup"><span data-stu-id="1a83c-114">Invoke direct methods</span></span>

## <a name="job-lifecycle"></a><span data-ttu-id="1a83c-115">作業生命週期</span><span class="sxs-lookup"><span data-stu-id="1a83c-115">Job lifecycle</span></span>
<span data-ttu-id="1a83c-116">作業會由 hello 方案後端所起始和維護的 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="1a83c-116">Jobs are initiated by hello solution back end and maintained by IoT Hub.</span></span>  <span data-ttu-id="1a83c-117">您可以透過面向服務的 URI (`{iot hub}/jobs/v2/{device id}/methods/<jobID>?api-version=2016-11-14`) 起始作業，並透過面向服務的 URI (`{iot hub}/jobs/v2/<jobId>?api-version=2016-11-14`) 查詢執行中作業的進度。</span><span class="sxs-lookup"><span data-stu-id="1a83c-117">You can initiate a job through a service-facing URI (`{iot hub}/jobs/v2/{device id}/methods/<jobID>?api-version=2016-11-14`) and query for progress on an executing job through a service-facing URI (`{iot hub}/jobs/v2/<jobId>?api-version=2016-11-14`).</span></span>  <span data-ttu-id="1a83c-118">一次作業會起始，查詢作業啟用 hello 後端應用程式 toorefresh hello 狀態執行的作業。</span><span class="sxs-lookup"><span data-stu-id="1a83c-118">Once a job is initiated, querying for jobs enables hello back-end app toorefresh hello status of running jobs.</span></span>

> [!NOTE]
> <span data-ttu-id="1a83c-119">當您起始的作業時，屬性名稱和值只能包含 US-ASCII 可列印英數字元、 在 hello 下列設定除外： ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``。</span><span class="sxs-lookup"><span data-stu-id="1a83c-119">When you initiate a job, property names and values can only contain US-ASCII printable alphanumeric, except any in hello following set: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.</span></span>
> 
> 

## <a name="reference-topics"></a><span data-ttu-id="1a83c-120">參考主題：</span><span class="sxs-lookup"><span data-stu-id="1a83c-120">Reference topics:</span></span>
<span data-ttu-id="1a83c-121">hello 下列參考主題提供有關使用 工作詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="1a83c-121">hello following reference topics provide you with more information about using jobs.</span></span>

## <a name="jobs-tooexecute-direct-methods"></a><span data-ttu-id="1a83c-122">作業 tooexecute 直接方法</span><span class="sxs-lookup"><span data-stu-id="1a83c-122">Jobs tooexecute direct methods</span></span>
<span data-ttu-id="1a83c-123">hello 如下 hello HTTP 1.1 要求詳細資料，執行[直接方法][ lnk-dev-methods]一組使用作業的裝置上：</span><span class="sxs-lookup"><span data-stu-id="1a83c-123">hello following is hello HTTP 1.1 request details for executing a [direct method][lnk-dev-methods] on a set of devices using a job:</span></span>

    ```
    PUT /jobs/v2/<jobId>?api-version=2016-11-14

    Authorization: <config.sharedAccessSignature>
    Content-Type: application/json; charset=utf-8
    Request-Id: <guid>
    User-Agent: <sdk-name>/<sdk-version>

    {
        jobId: '<jobId>',
        type: 'scheduleDirectRequest', 
        cloudToDeviceMethod: {
            methodName: '<methodName>',
            payload: <payload>,                 
            responseTimeoutInSeconds: methodTimeoutInSeconds 
        },
        queryCondition: '<queryOrDevices>', // query condition
        startTime: <jobStartTime>,          // as an ISO-8601 date string
        maxExecutionTimeInSeconds: <maxExecutionTimeInSeconds>        
    }
    ```
<span data-ttu-id="1a83c-124">hello 查詢條件也可以是單一裝置識別碼或裝置識別碼的清單如下所示</span><span class="sxs-lookup"><span data-stu-id="1a83c-124">hello query condition can also be on a single device Id or on a list of device Ids as shown below</span></span>

<span data-ttu-id="1a83c-125">**範例**</span><span class="sxs-lookup"><span data-stu-id="1a83c-125">**Examples**</span></span>
```
queryCondition = "deviceId = 'MyDevice1'"
queryCondition = "deviceId IN ['MyDevice1','MyDevice2']"
queryCondition = "deviceId IN ['MyDevice1']
```
<span data-ttu-id="1a83c-126">[IoT 中樞查詢語言][lnk-query]涵蓋了IoT 中樞查詢語言的其他詳細資料。</span><span class="sxs-lookup"><span data-stu-id="1a83c-126">[IoT Hub Query Language][lnk-query] covers IoT Hub query language in additional detail.</span></span>

## <a name="jobs-tooupdate-device-twin-properties"></a><span data-ttu-id="1a83c-127">作業 tooupdate 裝置兩個屬性</span><span class="sxs-lookup"><span data-stu-id="1a83c-127">Jobs tooupdate device twin properties</span></span>
<span data-ttu-id="1a83c-128">hello 下面是 hello HTTP 1.1 要求詳細資料，更新裝置使用作業的兩個屬性：</span><span class="sxs-lookup"><span data-stu-id="1a83c-128">hello following is hello HTTP 1.1 request details for updating device twin properties using a job:</span></span>

    ```
    PUT /jobs/v2/<jobId>?api-version=2016-11-14
    Authorization: <config.sharedAccessSignature>
    Content-Type: application/json; charset=utf-8
    Request-Id: <guid>
    User-Agent: <sdk-name>/<sdk-version>

    {
        jobId: '<jobId>',
        type: 'scheduleTwinUpdate', 
        updateTwin: <patch>                 // Valid JSON object
        queryCondition: '<queryOrDevices>', // query condition
        startTime: <jobStartTime>,          // as an ISO-8601 date string
        maxExecutionTimeInSeconds: <maxExecutionTimeInSeconds>        // format TBD
    }
    ```

## <a name="querying-for-progress-on-jobs"></a><span data-ttu-id="1a83c-129">查詢作業的進度</span><span class="sxs-lookup"><span data-stu-id="1a83c-129">Querying for progress on jobs</span></span>
<span data-ttu-id="1a83c-130">hello 如下 hello HTTP 1.1 要求詳細資料，如[查詢作業][lnk-query]:</span><span class="sxs-lookup"><span data-stu-id="1a83c-130">hello following is hello HTTP 1.1 request details for [querying for jobs][lnk-query]:</span></span>

    ```
    GET /jobs/v2/query?api-version=2016-11-14[&jobType=<jobType>][&jobStatus=<jobStatus>][&pageSize=<pageSize>][&continuationToken=<continuationToken>]

    Authorization: <config.sharedAccessSignature>
    Content-Type: application/json; charset=utf-8
    Request-Id: <guid>
    User-Agent: <sdk-name>/<sdk-version>
    ```

<span data-ttu-id="1a83c-131">hello continuationToken hello 回應中提供。</span><span class="sxs-lookup"><span data-stu-id="1a83c-131">hello continuationToken is provided from hello response.</span></span>  

## <a name="jobs-properties"></a><span data-ttu-id="1a83c-132">作業屬性</span><span class="sxs-lookup"><span data-stu-id="1a83c-132">Jobs Properties</span></span>
<span data-ttu-id="1a83c-133">hello 下列是屬性對應的描述，可用於查詢時的工作或作業結果的清單。</span><span class="sxs-lookup"><span data-stu-id="1a83c-133">hello following is a list of properties and corresponding descriptions, which can be used when querying for jobs or job results.</span></span>

| <span data-ttu-id="1a83c-134">屬性</span><span class="sxs-lookup"><span data-stu-id="1a83c-134">Property</span></span> | <span data-ttu-id="1a83c-135">說明</span><span class="sxs-lookup"><span data-stu-id="1a83c-135">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1a83c-136">**jobId**</span><span class="sxs-lookup"><span data-stu-id="1a83c-136">**jobId**</span></span> |<span data-ttu-id="1a83c-137">應用程式提供 hello 作業識別碼。</span><span class="sxs-lookup"><span data-stu-id="1a83c-137">Application provided ID for hello job.</span></span> |
| <span data-ttu-id="1a83c-138">**startTime**</span><span class="sxs-lookup"><span data-stu-id="1a83c-138">**startTime**</span></span> |<span data-ttu-id="1a83c-139">應用程式提供 hello 工作的開始時間 (ISO 8601)。</span><span class="sxs-lookup"><span data-stu-id="1a83c-139">Application provided start time (ISO-8601) for hello job.</span></span> |
| <span data-ttu-id="1a83c-140">**endTime**</span><span class="sxs-lookup"><span data-stu-id="1a83c-140">**endTime**</span></span> |<span data-ttu-id="1a83c-141">IoT 中樞 hello 作業完成時的日期 (ISO 8601) 提供。</span><span class="sxs-lookup"><span data-stu-id="1a83c-141">IoT Hub provided date (ISO-8601) for when hello job completed.</span></span> <span data-ttu-id="1a83c-142">Hello 作業到達完成' hello 狀態之後，才有效。</span><span class="sxs-lookup"><span data-stu-id="1a83c-142">Valid only after hello job reaches hello 'completed' state.</span></span> |
| <span data-ttu-id="1a83c-143">**type**</span><span class="sxs-lookup"><span data-stu-id="1a83c-143">**type**</span></span> |<span data-ttu-id="1a83c-144">作業類型：</span><span class="sxs-lookup"><span data-stu-id="1a83c-144">Types of jobs:</span></span> |
| <span data-ttu-id="1a83c-145">**scheduledUpdateTwin**: 作業，以便用 tooupdate 一組所需的屬性或標記。</span><span class="sxs-lookup"><span data-stu-id="1a83c-145">**scheduledUpdateTwin**: A job used tooupdate a set of desired properties or tags.</span></span> | |
| <span data-ttu-id="1a83c-146">**scheduledDeviceMethod**: 作業，以便用 tooinvoke 裝置上的方法裝置雙一組。</span><span class="sxs-lookup"><span data-stu-id="1a83c-146">**scheduledDeviceMethod**: A job used tooinvoke a device method on a set of device twins.</span></span> | |
| <span data-ttu-id="1a83c-147">**狀態**</span><span class="sxs-lookup"><span data-stu-id="1a83c-147">**status**</span></span> |<span data-ttu-id="1a83c-148">Hello 作業的目前狀態。</span><span class="sxs-lookup"><span data-stu-id="1a83c-148">Current state of hello job.</span></span> <span data-ttu-id="1a83c-149">狀態的可能值︰</span><span class="sxs-lookup"><span data-stu-id="1a83c-149">Possible values for status:</span></span> |
| <span data-ttu-id="1a83c-150">**暫止**： 排程並等候 toobe 收取 hello 工作服務。</span><span class="sxs-lookup"><span data-stu-id="1a83c-150">**pending** : Scheduled and waiting toobe picked up by hello job service.</span></span> | |
| <span data-ttu-id="1a83c-151">**排程**： 排程在未來的 hello 的時間。</span><span class="sxs-lookup"><span data-stu-id="1a83c-151">**scheduled** : Scheduled for a time in hello future.</span></span> | |
| <span data-ttu-id="1a83c-152">**執行中**︰目前作用中的作業。</span><span class="sxs-lookup"><span data-stu-id="1a83c-152">**running** : Currently active job.</span></span> | |
| <span data-ttu-id="1a83c-153">**取消**︰作業已遭到取消。</span><span class="sxs-lookup"><span data-stu-id="1a83c-153">**cancelled** : Job has been cancelled.</span></span> | |
| <span data-ttu-id="1a83c-154">**失敗**︰作業失敗。</span><span class="sxs-lookup"><span data-stu-id="1a83c-154">**failed** : Job failed.</span></span> | |
| <span data-ttu-id="1a83c-155">**完成**︰作業完成。</span><span class="sxs-lookup"><span data-stu-id="1a83c-155">**completed** : Job has completed.</span></span> | |
| <span data-ttu-id="1a83c-156">**deviceJobStatistics**</span><span class="sxs-lookup"><span data-stu-id="1a83c-156">**deviceJobStatistics**</span></span> |<span data-ttu-id="1a83c-157">Hello 作業的執行統計資料。</span><span class="sxs-lookup"><span data-stu-id="1a83c-157">Statistics about hello job's execution.</span></span> |

<span data-ttu-id="1a83c-158">**deviceJobStatistics** 屬性。</span><span class="sxs-lookup"><span data-stu-id="1a83c-158">**deviceJobStatistics** properties.</span></span>

| <span data-ttu-id="1a83c-159">屬性</span><span class="sxs-lookup"><span data-stu-id="1a83c-159">Property</span></span> | <span data-ttu-id="1a83c-160">說明</span><span class="sxs-lookup"><span data-stu-id="1a83c-160">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1a83c-161">**deviceJobStatistics.deviceCount**</span><span class="sxs-lookup"><span data-stu-id="1a83c-161">**deviceJobStatistics.deviceCount**</span></span> |<span data-ttu-id="1a83c-162">Hello 作業中的裝置數目。</span><span class="sxs-lookup"><span data-stu-id="1a83c-162">Number of devices in hello job.</span></span> |
| <span data-ttu-id="1a83c-163">**deviceJobStatistics.failedCount**</span><span class="sxs-lookup"><span data-stu-id="1a83c-163">**deviceJobStatistics.failedCount**</span></span> |<span data-ttu-id="1a83c-164">Hello 作業失敗的裝置數目。</span><span class="sxs-lookup"><span data-stu-id="1a83c-164">Number of devices where hello job failed.</span></span> |
| <span data-ttu-id="1a83c-165">**deviceJobStatistics.succeededCount**</span><span class="sxs-lookup"><span data-stu-id="1a83c-165">**deviceJobStatistics.succeededCount**</span></span> |<span data-ttu-id="1a83c-166">Hello 作業成功，其中的裝置數目。</span><span class="sxs-lookup"><span data-stu-id="1a83c-166">Number of devices where hello job succeeded.</span></span> |
| <span data-ttu-id="1a83c-167">**deviceJobStatistics.runningCount**</span><span class="sxs-lookup"><span data-stu-id="1a83c-167">**deviceJobStatistics.runningCount**</span></span> |<span data-ttu-id="1a83c-168">目前正在 hello 工作的裝置數目。</span><span class="sxs-lookup"><span data-stu-id="1a83c-168">Number of devices that are currently running hello job.</span></span> |
| <span data-ttu-id="1a83c-169">**deviceJobStatistics.pendingCount**</span><span class="sxs-lookup"><span data-stu-id="1a83c-169">**deviceJobStatistics.pendingCount**</span></span> |<span data-ttu-id="1a83c-170">Toorun hello 作業擱置的裝置數目。</span><span class="sxs-lookup"><span data-stu-id="1a83c-170">Number of devices that are pending toorun hello job.</span></span> |

### <a name="additional-reference-material"></a><span data-ttu-id="1a83c-171">其他參考資料</span><span class="sxs-lookup"><span data-stu-id="1a83c-171">Additional reference material</span></span>
<span data-ttu-id="1a83c-172">Hello IoT 中樞開發人員指南 》 中的其他參考主題包括：</span><span class="sxs-lookup"><span data-stu-id="1a83c-172">Other reference topics in hello IoT Hub developer guide include:</span></span>

* <span data-ttu-id="1a83c-173">[IoT 中樞端點][ lnk-endpoints]描述 hello 各種執行階段和管理作業的每個 IoT 中樞會公開的端點。</span><span class="sxs-lookup"><span data-stu-id="1a83c-173">[IoT Hub endpoints][lnk-endpoints] describes hello various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="1a83c-174">[節流和配額][ lnk-quotas]描述 hello 配額套用 toohello IoT 中心服務和 hello 節流行為 tooexpect，當您使用 hello 服務。</span><span class="sxs-lookup"><span data-stu-id="1a83c-174">[Throttling and quotas][lnk-quotas] describes hello quotas that apply toohello IoT Hub service and hello throttling behavior tooexpect when you use hello service.</span></span>
* <span data-ttu-id="1a83c-175">[Azure IoT 裝置和服務 Sdk] [ lnk-sdks]清單 hello 各種語言的 Sdk 可以與 IoT 中樞開發裝置與服務互動的應用程式時使用。</span><span class="sxs-lookup"><span data-stu-id="1a83c-175">[Azure IoT device and service SDKs][lnk-sdks] lists hello various language SDKs you an use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="1a83c-176">[IoT 中樞裝置雙、 作業和訊息路由的查詢語言][ lnk-query]描述 hello IoT 中樞的查詢語言，您可以使用您的裝置雙和作業相關的 tooretrieve 資訊從 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="1a83c-176">[IoT Hub query language for device twins, jobs, and message routing][lnk-query] describes hello IoT Hub query language you can use tooretrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="1a83c-177">[IoT 中樞 MQTT 支援][ lnk-devguide-mqtt] hello MQTT 通訊協定提供 IoT 中樞支援的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="1a83c-177">[IoT Hub MQTT support][lnk-devguide-mqtt] provides more information about IoT Hub support for hello MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1a83c-178">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1a83c-178">Next steps</span></span>
<span data-ttu-id="1a83c-179">如果您想要查看這篇文章中所述的 hello 概念 tootry，您可能想要遵循 IoT 中樞教學課程中的 hello:</span><span class="sxs-lookup"><span data-stu-id="1a83c-179">If you would like tootry out some of hello concepts described in this article, you may be interested in hello following IoT Hub tutorial:</span></span>

* <span data-ttu-id="1a83c-180">[排程及廣播作業][lnk-jobs-tutorial]</span><span class="sxs-lookup"><span data-stu-id="1a83c-180">[Schedule and broadcast jobs][lnk-jobs-tutorial]</span></span>

<!-- links and images -->

[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-jobs-tutorial]: iot-hub-node-node-schedule-jobs.md
[lnk-c2d-methods]: iot-hub-node-node-direct-methods.md
[lnk-dev-methods]: iot-hub-devguide-direct-methods.md
[lnk-get-started-twin]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-devguide]: iot-hub-devguide-device-twins.md
