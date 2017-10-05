---
title: "了解 Azure IoT 中樞作業 | Microsoft Docs"
description: "開發人員指南 - 排定在連接至 IoT 中樞的多個裝置上執行作業。 作業可以在多個裝置上更新標籤和所需的屬性，並叫用直接方法。"
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
ms.openlocfilehash: abb7f80662650efa8f158f32125ebc5350cb4f62
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="schedule-jobs-on-multiple-devices"></a><span data-ttu-id="38c04-104">排程多個裝置上的作業</span><span class="sxs-lookup"><span data-stu-id="38c04-104">Schedule jobs on multiple devices</span></span>
## <a name="overview"></a><span data-ttu-id="38c04-105">概觀</span><span class="sxs-lookup"><span data-stu-id="38c04-105">Overview</span></span>
<span data-ttu-id="38c04-106">如前面幾篇文章所述，Azure IoT 中樞可啟用許多建置組塊 ([裝置對應項屬性和標籤][lnk-twin-devguide]和[直接方法][lnk-dev-methods])。</span><span class="sxs-lookup"><span data-stu-id="38c04-106">As described by previous articles, Azure IoT Hub enables a number of building blocks ([device twin properties and tags][lnk-twin-devguide] and [direct methods][lnk-dev-methods]).</span></span>  <span data-ttu-id="38c04-107">一般而言，後端應用程式可讓裝置管理員和操作員在排定的時間大量更新 IoT 裝置並與之互動。</span><span class="sxs-lookup"><span data-stu-id="38c04-107">Typically, back-end apps enable device administrators and operators to update and interact with IoT devices in bulk and at a scheduled time.</span></span>  <span data-ttu-id="38c04-108">作業可將在排定時間針對一組裝置執行裝置對應項更新和直接方法的操作封裝起來。</span><span class="sxs-lookup"><span data-stu-id="38c04-108">Jobs encapsulate the execution of device twin updates and direct methods against a set of devices at a schedule time.</span></span>  <span data-ttu-id="38c04-109">例如，操作員會使用後端應用程式來起始和追蹤作業，在不干擾大樓運作的時段，將 43 號大樓 3 樓的一組裝置重新開機。</span><span class="sxs-lookup"><span data-stu-id="38c04-109">For example, an operator would use a back-end app that would initiate and track a job to reboot a set of devices in building 43 and floor 3 at a time that would not be disruptive to the operations of the building.</span></span>

### <a name="when-to-use"></a><span data-ttu-id="38c04-110">使用時機</span><span class="sxs-lookup"><span data-stu-id="38c04-110">When to use</span></span>
<span data-ttu-id="38c04-111">當解決方案後端需要排程和追蹤一組裝置的下列任何活動進度時，請考慮使用作業︰</span><span class="sxs-lookup"><span data-stu-id="38c04-111">Consider using jobs when: a solution back end needs to schedule and track progress any of the following activities on a set of device:</span></span>

* <span data-ttu-id="38c04-112">更新所需屬性</span><span class="sxs-lookup"><span data-stu-id="38c04-112">Update desired properties</span></span>
* <span data-ttu-id="38c04-113">更新標籤</span><span class="sxs-lookup"><span data-stu-id="38c04-113">Update tags</span></span>
* <span data-ttu-id="38c04-114">叫用直接方法</span><span class="sxs-lookup"><span data-stu-id="38c04-114">Invoke direct methods</span></span>

## <a name="job-lifecycle"></a><span data-ttu-id="38c04-115">作業生命週期</span><span class="sxs-lookup"><span data-stu-id="38c04-115">Job lifecycle</span></span>
<span data-ttu-id="38c04-116">作業由解決方案後端起始，並由 IoT 中樞維護。</span><span class="sxs-lookup"><span data-stu-id="38c04-116">Jobs are initiated by the solution back end and maintained by IoT Hub.</span></span>  <span data-ttu-id="38c04-117">您可以透過面向服務的 URI (`{iot hub}/jobs/v2/{device id}/methods/<jobID>?api-version=2016-11-14`) 起始作業，並透過面向服務的 URI (`{iot hub}/jobs/v2/<jobId>?api-version=2016-11-14`) 查詢執行中作業的進度。</span><span class="sxs-lookup"><span data-stu-id="38c04-117">You can initiate a job through a service-facing URI (`{iot hub}/jobs/v2/{device id}/methods/<jobID>?api-version=2016-11-14`) and query for progress on an executing job through a service-facing URI (`{iot hub}/jobs/v2/<jobId>?api-version=2016-11-14`).</span></span>  <span data-ttu-id="38c04-118">作業起始後，只要查詢作業，就可讓後端應用程式重新整理執行中作業的狀態。</span><span class="sxs-lookup"><span data-stu-id="38c04-118">Once a job is initiated, querying for jobs enables the back-end app to refresh the status of running jobs.</span></span>

> [!NOTE]
> <span data-ttu-id="38c04-119">當您起始作業時，屬性名稱和值只能包含 US-ASCII 可列印英數字元，下列集合中的任何字元除外︰``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``。</span><span class="sxs-lookup"><span data-stu-id="38c04-119">When you initiate a job, property names and values can only contain US-ASCII printable alphanumeric, except any in the following set: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.</span></span>
> 
> 

## <a name="reference-topics"></a><span data-ttu-id="38c04-120">參考主題：</span><span class="sxs-lookup"><span data-stu-id="38c04-120">Reference topics:</span></span>
<span data-ttu-id="38c04-121">下列參考主題會提供您關於使用作業的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="38c04-121">The following reference topics provide you with more information about using jobs.</span></span>

## <a name="jobs-to-execute-direct-methods"></a><span data-ttu-id="38c04-122">用以執行直接方法的作業</span><span class="sxs-lookup"><span data-stu-id="38c04-122">Jobs to execute direct methods</span></span>
<span data-ttu-id="38c04-123">以下是使用作業在一組裝置上執行[直接方法][lnk-dev-methods]的 HTTP 1.1 要求詳細資料︰</span><span class="sxs-lookup"><span data-stu-id="38c04-123">The following is the HTTP 1.1 request details for executing a [direct method][lnk-dev-methods] on a set of devices using a job:</span></span>

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
<span data-ttu-id="38c04-124">查詢條件也可以在單一裝置識別碼或裝置識別碼清單中，如下所示</span><span class="sxs-lookup"><span data-stu-id="38c04-124">The query condition can also be on a single device Id or on a list of device Ids as shown below</span></span>

<span data-ttu-id="38c04-125">**範例**</span><span class="sxs-lookup"><span data-stu-id="38c04-125">**Examples**</span></span>
```
queryCondition = "deviceId = 'MyDevice1'"
queryCondition = "deviceId IN ['MyDevice1','MyDevice2']"
queryCondition = "deviceId IN ['MyDevice1']
```
<span data-ttu-id="38c04-126">[IoT 中樞查詢語言][lnk-query]涵蓋了IoT 中樞查詢語言的其他詳細資料。</span><span class="sxs-lookup"><span data-stu-id="38c04-126">[IoT Hub Query Language][lnk-query] covers IoT Hub query language in additional detail.</span></span>

## <a name="jobs-to-update-device-twin-properties"></a><span data-ttu-id="38c04-127">用以更新裝置對應項屬性的作業</span><span class="sxs-lookup"><span data-stu-id="38c04-127">Jobs to update device twin properties</span></span>
<span data-ttu-id="38c04-128">以下是使用作業更新裝置對應項屬性的 HTTP 1.1 要求詳細資料︰</span><span class="sxs-lookup"><span data-stu-id="38c04-128">The following is the HTTP 1.1 request details for updating device twin properties using a job:</span></span>

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

## <a name="querying-for-progress-on-jobs"></a><span data-ttu-id="38c04-129">查詢作業的進度</span><span class="sxs-lookup"><span data-stu-id="38c04-129">Querying for progress on jobs</span></span>
<span data-ttu-id="38c04-130">以下是用於[查詢作業][lnk-query]的 HTTP 1.1 要求詳細資料：</span><span class="sxs-lookup"><span data-stu-id="38c04-130">The following is the HTTP 1.1 request details for [querying for jobs][lnk-query]:</span></span>

    ```
    GET /jobs/v2/query?api-version=2016-11-14[&jobType=<jobType>][&jobStatus=<jobStatus>][&pageSize=<pageSize>][&continuationToken=<continuationToken>]

    Authorization: <config.sharedAccessSignature>
    Content-Type: application/json; charset=utf-8
    Request-Id: <guid>
    User-Agent: <sdk-name>/<sdk-version>
    ```

<span data-ttu-id="38c04-131">ContinuationToken 會從回應來提供。</span><span class="sxs-lookup"><span data-stu-id="38c04-131">The continuationToken is provided from the response.</span></span>  

## <a name="jobs-properties"></a><span data-ttu-id="38c04-132">作業屬性</span><span class="sxs-lookup"><span data-stu-id="38c04-132">Jobs Properties</span></span>
<span data-ttu-id="38c04-133">以下是屬性和相對應說明的清單，可於查詢作業或作業結果時使用。</span><span class="sxs-lookup"><span data-stu-id="38c04-133">The following is a list of properties and corresponding descriptions, which can be used when querying for jobs or job results.</span></span>

| <span data-ttu-id="38c04-134">屬性</span><span class="sxs-lookup"><span data-stu-id="38c04-134">Property</span></span> | <span data-ttu-id="38c04-135">說明</span><span class="sxs-lookup"><span data-stu-id="38c04-135">Description</span></span> |
| --- | --- |
| <span data-ttu-id="38c04-136">**jobId**</span><span class="sxs-lookup"><span data-stu-id="38c04-136">**jobId**</span></span> |<span data-ttu-id="38c04-137">應用程式所提供的作業識別碼。</span><span class="sxs-lookup"><span data-stu-id="38c04-137">Application provided ID for the job.</span></span> |
| <span data-ttu-id="38c04-138">**startTime**</span><span class="sxs-lookup"><span data-stu-id="38c04-138">**startTime**</span></span> |<span data-ttu-id="38c04-139">應用程式所提供的作業開始時間 (ISO-8601)。</span><span class="sxs-lookup"><span data-stu-id="38c04-139">Application provided start time (ISO-8601) for the job.</span></span> |
| <span data-ttu-id="38c04-140">**endTime**</span><span class="sxs-lookup"><span data-stu-id="38c04-140">**endTime**</span></span> |<span data-ttu-id="38c04-141">IoT 中樞所提供的作業完成日期 (ISO-8601)。</span><span class="sxs-lookup"><span data-stu-id="38c04-141">IoT Hub provided date (ISO-8601) for when the job completed.</span></span> <span data-ttu-id="38c04-142">在作業到達「已完成」狀態後才有效。</span><span class="sxs-lookup"><span data-stu-id="38c04-142">Valid only after the job reaches the 'completed' state.</span></span> |
| <span data-ttu-id="38c04-143">**type**</span><span class="sxs-lookup"><span data-stu-id="38c04-143">**type**</span></span> |<span data-ttu-id="38c04-144">作業類型：</span><span class="sxs-lookup"><span data-stu-id="38c04-144">Types of jobs:</span></span> |
| <span data-ttu-id="38c04-145">**scheduledUpdateTwin**︰用來更新一組所需屬性或標籤的作業。</span><span class="sxs-lookup"><span data-stu-id="38c04-145">**scheduledUpdateTwin**: A job used to update a set of desired properties or tags.</span></span> | |
| <span data-ttu-id="38c04-146">**scheduledDeviceMethod**︰用來在一組裝置對應項上叫用裝置方法的作業。</span><span class="sxs-lookup"><span data-stu-id="38c04-146">**scheduledDeviceMethod**: A job used to invoke a device method on a set of device twins.</span></span> | |
| <span data-ttu-id="38c04-147">**狀態**</span><span class="sxs-lookup"><span data-stu-id="38c04-147">**status**</span></span> |<span data-ttu-id="38c04-148">作業的目前狀態。</span><span class="sxs-lookup"><span data-stu-id="38c04-148">Current state of the job.</span></span> <span data-ttu-id="38c04-149">狀態的可能值︰</span><span class="sxs-lookup"><span data-stu-id="38c04-149">Possible values for status:</span></span> |
| <span data-ttu-id="38c04-150">**擱置中**︰已排定並等候作業服務揀選。</span><span class="sxs-lookup"><span data-stu-id="38c04-150">**pending** : Scheduled and waiting to be picked up by the job service.</span></span> | |
| <span data-ttu-id="38c04-151">**已排程**︰已排定未來時間。</span><span class="sxs-lookup"><span data-stu-id="38c04-151">**scheduled** : Scheduled for a time in the future.</span></span> | |
| <span data-ttu-id="38c04-152">**執行中**︰目前作用中的作業。</span><span class="sxs-lookup"><span data-stu-id="38c04-152">**running** : Currently active job.</span></span> | |
| <span data-ttu-id="38c04-153">**取消**︰作業已遭到取消。</span><span class="sxs-lookup"><span data-stu-id="38c04-153">**cancelled** : Job has been cancelled.</span></span> | |
| <span data-ttu-id="38c04-154">**失敗**︰作業失敗。</span><span class="sxs-lookup"><span data-stu-id="38c04-154">**failed** : Job failed.</span></span> | |
| <span data-ttu-id="38c04-155">**完成**︰作業完成。</span><span class="sxs-lookup"><span data-stu-id="38c04-155">**completed** : Job has completed.</span></span> | |
| <span data-ttu-id="38c04-156">**deviceJobStatistics**</span><span class="sxs-lookup"><span data-stu-id="38c04-156">**deviceJobStatistics**</span></span> |<span data-ttu-id="38c04-157">作業執行的相關統計資料。</span><span class="sxs-lookup"><span data-stu-id="38c04-157">Statistics about the job's execution.</span></span> |

<span data-ttu-id="38c04-158">**deviceJobStatistics** 屬性。</span><span class="sxs-lookup"><span data-stu-id="38c04-158">**deviceJobStatistics** properties.</span></span>

| <span data-ttu-id="38c04-159">屬性</span><span class="sxs-lookup"><span data-stu-id="38c04-159">Property</span></span> | <span data-ttu-id="38c04-160">說明</span><span class="sxs-lookup"><span data-stu-id="38c04-160">Description</span></span> |
| --- | --- |
| <span data-ttu-id="38c04-161">**deviceJobStatistics.deviceCount**</span><span class="sxs-lookup"><span data-stu-id="38c04-161">**deviceJobStatistics.deviceCount**</span></span> |<span data-ttu-id="38c04-162">作業中的裝置數目。</span><span class="sxs-lookup"><span data-stu-id="38c04-162">Number of devices in the job.</span></span> |
| <span data-ttu-id="38c04-163">**deviceJobStatistics.failedCount**</span><span class="sxs-lookup"><span data-stu-id="38c04-163">**deviceJobStatistics.failedCount**</span></span> |<span data-ttu-id="38c04-164">作業失敗的裝置數目。</span><span class="sxs-lookup"><span data-stu-id="38c04-164">Number of devices where the job failed.</span></span> |
| <span data-ttu-id="38c04-165">**deviceJobStatistics.succeededCount**</span><span class="sxs-lookup"><span data-stu-id="38c04-165">**deviceJobStatistics.succeededCount**</span></span> |<span data-ttu-id="38c04-166">作業成功的裝置數目。</span><span class="sxs-lookup"><span data-stu-id="38c04-166">Number of devices where the job succeeded.</span></span> |
| <span data-ttu-id="38c04-167">**deviceJobStatistics.runningCount**</span><span class="sxs-lookup"><span data-stu-id="38c04-167">**deviceJobStatistics.runningCount**</span></span> |<span data-ttu-id="38c04-168">目前正在執行作業的裝置數目。</span><span class="sxs-lookup"><span data-stu-id="38c04-168">Number of devices that are currently running the job.</span></span> |
| <span data-ttu-id="38c04-169">**deviceJobStatistics.pendingCount**</span><span class="sxs-lookup"><span data-stu-id="38c04-169">**deviceJobStatistics.pendingCount**</span></span> |<span data-ttu-id="38c04-170">等待執行作業的裝置數目。</span><span class="sxs-lookup"><span data-stu-id="38c04-170">Number of devices that are pending to run the job.</span></span> |

### <a name="additional-reference-material"></a><span data-ttu-id="38c04-171">其他參考資料</span><span class="sxs-lookup"><span data-stu-id="38c04-171">Additional reference material</span></span>
<span data-ttu-id="38c04-172">IoT 中樞開發人員指南中的其他參考主題包括︰</span><span class="sxs-lookup"><span data-stu-id="38c04-172">Other reference topics in the IoT Hub developer guide include:</span></span>

* <span data-ttu-id="38c04-173">[IoT 中樞端點][lnk-endpoints]說明每個 IoT 中樞公開給執行階段和管理作業的各種端點。</span><span class="sxs-lookup"><span data-stu-id="38c04-173">[IoT Hub endpoints][lnk-endpoints] describes the various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="38c04-174">[節流和配額][lnk-quotas]說明適用於 IoT 中樞服務的配額，和使用服務時所預期的節流行為。</span><span class="sxs-lookup"><span data-stu-id="38c04-174">[Throttling and quotas][lnk-quotas] describes the quotas that apply to the IoT Hub service and the throttling behavior to expect when you use the service.</span></span>
* <span data-ttu-id="38c04-175">[Azure IoT 中樞裝置和服務 SDK][lnk-sdks] 列出各種語言 SDK，讓您在開發可與 IoT 中樞互動的裝置和服務應用程式時使用。</span><span class="sxs-lookup"><span data-stu-id="38c04-175">[Azure IoT device and service SDKs][lnk-sdks] lists the various language SDKs you an use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="38c04-176">[裝置對應項、作業和訊息路由的 IoT 中樞查詢語言][lnk-query]說明可用於從 IoT 中樞擷取有關裝置對應項和作業資訊的 IoT 中樞查詢語言。</span><span class="sxs-lookup"><span data-stu-id="38c04-176">[IoT Hub query language for device twins, jobs, and message routing][lnk-query] describes the IoT Hub query language you can use to retrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="38c04-177">[IoT 中樞 MQTT 支援][lnk-devguide-mqtt]針對 MQTT 通訊協定提供 IoT 中樞支援的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="38c04-177">[IoT Hub MQTT support][lnk-devguide-mqtt] provides more information about IoT Hub support for the MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="38c04-178">後續步驟</span><span class="sxs-lookup"><span data-stu-id="38c04-178">Next steps</span></span>
<span data-ttu-id="38c04-179">如果您想要嘗試本文章所述的概念，您可能會對下列 IoT 中樞教學課程感興趣：</span><span class="sxs-lookup"><span data-stu-id="38c04-179">If you would like to try out some of the concepts described in this article, you may be interested in the following IoT Hub tutorial:</span></span>

* <span data-ttu-id="38c04-180">[排程及廣播作業][lnk-jobs-tutorial]</span><span class="sxs-lookup"><span data-stu-id="38c04-180">[Schedule and broadcast jobs][lnk-jobs-tutorial]</span></span>

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
