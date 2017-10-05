---
title: "了解 Azure IoT 中樞直接方法 | Microsoft Docs"
description: "開發人員指南 - 從服務應用程式使用直接方法叫用您裝置上的程式碼。"
services: iot-hub
documentationcenter: .net
author: nberdy
manager: timlt
editor: 
ms.assetid: 9f0535f1-02e6-467a-9fc4-c0950702102d
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: nberdy
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 77e788a32097edbcb1cd4faaa45f35812eabd94a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="understand-and-invoke-direct-methods-from-iot-hub"></a><span data-ttu-id="7ba35-103">了解 IoT 中樞的直接方法並從中樞叫用直接方法</span><span class="sxs-lookup"><span data-stu-id="7ba35-103">Understand and invoke direct methods from IoT Hub</span></span>
## <a name="overview"></a><span data-ttu-id="7ba35-104">概觀</span><span class="sxs-lookup"><span data-stu-id="7ba35-104">Overview</span></span>
<span data-ttu-id="7ba35-105">IoT 中樞能讓您從雲端在裝置上叫用直接方法。</span><span class="sxs-lookup"><span data-stu-id="7ba35-105">IoT Hub gives you ability to invoke direct methods on devices from the cloud.</span></span> <span data-ttu-id="7ba35-106">直接方法代表與裝置的要求-回覆互動，類似於 HTTP 呼叫，因為會立即成功或失敗 (在使用者指定的逾時之後)。</span><span class="sxs-lookup"><span data-stu-id="7ba35-106">Direct methods represent a request-reply interaction with a device similar to an HTTP call in that they succeed or fail immediately (after a user-specified timeout).</span></span> <span data-ttu-id="7ba35-107">這對於依據裝置是否可以回應的不同立即動作的案例相當有用，例如如果裝置離線時傳送 SMS 喚醒至裝置 (SMS 比方法呼叫還貴)。</span><span class="sxs-lookup"><span data-stu-id="7ba35-107">This is useful for scenarios where the course of immediate action is different depending on whether the device was able to respond, such as sending an SMS wake-up to a device if a device is offline (SMS being more expensive than a method call).</span></span>

<span data-ttu-id="7ba35-108">每個裝置方法的目標是單一裝置。</span><span class="sxs-lookup"><span data-stu-id="7ba35-108">Each device method targets a single device.</span></span> <span data-ttu-id="7ba35-109">[作業][lnk-devguide-jobs]提供方法來在多個裝置上叫用直接方法，並針對已中斷連接的裝置排定方法引動過程。</span><span class="sxs-lookup"><span data-stu-id="7ba35-109">[Jobs][lnk-devguide-jobs] provide a way to invoke direct methods on multiple devices, and schedule method invocation for disconnected devices.</span></span>

<span data-ttu-id="7ba35-110">IoT 中樞上具有**服務連線**權限的任何人都可以叫用裝置上的方法。</span><span class="sxs-lookup"><span data-stu-id="7ba35-110">Anyone with **service connect** permissions on IoT Hub may invoke a method on a device.</span></span>

### <a name="when-to-use"></a><span data-ttu-id="7ba35-111">使用時機</span><span class="sxs-lookup"><span data-stu-id="7ba35-111">When to use</span></span>
<span data-ttu-id="7ba35-112">直接方法會遵循要求-回應模式，主要用於需要立即確認其結果的通訊，通常為裝置的互動式控制，例如開啟風扇。</span><span class="sxs-lookup"><span data-stu-id="7ba35-112">Direct methods follow a request-response pattern and are meant for communications that require immediate confirmation of their result, usually interactive control of the device, for example to turn on a fan.</span></span>

<span data-ttu-id="7ba35-113">如果不確定要使用所需屬性、直接方法或雲端對裝置訊息，請參閱[雲端對裝置通訊指引][lnk-c2d-guidance]。</span><span class="sxs-lookup"><span data-stu-id="7ba35-113">Refer to [Cloud-to-device communication guidance][lnk-c2d-guidance] if in doubt between using desired properties, direct methods, or cloud-to-device messages.</span></span>

## <a name="method-lifecycle"></a><span data-ttu-id="7ba35-114">方法生命週期</span><span class="sxs-lookup"><span data-stu-id="7ba35-114">Method lifecycle</span></span>
<span data-ttu-id="7ba35-115">直接方法是在裝置上實作，而且可能需要方法承載中的零或多個輸入以正確具現化。</span><span class="sxs-lookup"><span data-stu-id="7ba35-115">Direct methods are implemented on the device and may require zero or more inputs in the method payload to correctly instantiate.</span></span> <span data-ttu-id="7ba35-116">您可以透過面向服務的 URI 叫用直接方法 (`{iot hub}/twins/{device id}/methods/`)。</span><span class="sxs-lookup"><span data-stu-id="7ba35-116">You invoke a direct method through a service-facing URI (`{iot hub}/twins/{device id}/methods/`).</span></span> <span data-ttu-id="7ba35-117">裝置會透過裝置特定 MQTT 主題收到直接方法 (`$iothub/methods/POST/{method name}/`)。</span><span class="sxs-lookup"><span data-stu-id="7ba35-117">A device receives direct methods through a device-specific MQTT topic (`$iothub/methods/POST/{method name}/`).</span></span> <span data-ttu-id="7ba35-118">我們未來可能會在額外的裝置端網路通訊協定上支援直接方法。</span><span class="sxs-lookup"><span data-stu-id="7ba35-118">We may support direct methods on additional device-side networking protocols in the future.</span></span>

> [!NOTE]
> <span data-ttu-id="7ba35-119">當您在裝置上叫用直接方法時，屬性名稱和值只能包含 US-ASCII 可列印英數字元，下列集合中的任何字元除外︰``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``。</span><span class="sxs-lookup"><span data-stu-id="7ba35-119">When you invoke a direct method on a device, property names and values can only contain US-ASCII printable alphanumeric, except any in the following set: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.</span></span>
> 
> 

<span data-ttu-id="7ba35-120">直接方法是同步的，可能在逾時期間後成功或失敗 (預設︰30 秒，可設定為 3600 秒)。</span><span class="sxs-lookup"><span data-stu-id="7ba35-120">Direct methods are synchronous and either succeed or fail after the timeout period (default: 30 seconds, settable up to 3600 seconds).</span></span> <span data-ttu-id="7ba35-121">直接方法在您想要裝置當作在線上並且接收命令 (例如透過手機開燈) 的互動案例中相當有用。</span><span class="sxs-lookup"><span data-stu-id="7ba35-121">Direct methods are useful in interactive scenarios where you want a device to act if and only if the device is online and receiving commands, such as turning on a light from a phone.</span></span> <span data-ttu-id="7ba35-122">在這些案例中，您想要查看立即成功或失敗，讓雲端服務可以儘速處理結果。</span><span class="sxs-lookup"><span data-stu-id="7ba35-122">In these scenarios, you want to see an immediate success or failure so the cloud service can act on the result as soon as possible.</span></span> <span data-ttu-id="7ba35-123">裝置可能會傳回部分訊息本文作為方法的結果，但是不需要方法這麼做。</span><span class="sxs-lookup"><span data-stu-id="7ba35-123">The device may return some message body as a result of the method, but it isn't required for the method to do so.</span></span> <span data-ttu-id="7ba35-124">不保證方法呼叫的順序或任何並行語意。</span><span class="sxs-lookup"><span data-stu-id="7ba35-124">There is no guarantee on ordering or any concurrency semantics on method calls.</span></span>

<span data-ttu-id="7ba35-125">直接的方法從雲端側為僅限 HTTP，從裝置側則為僅限 MQTT。</span><span class="sxs-lookup"><span data-stu-id="7ba35-125">Direct method are HTTP-only from the cloud side, and MQTT-only from the device side.</span></span>

<span data-ttu-id="7ba35-126">方法要求和回應的承載是 JSON 文件 (最多 8 KB)。</span><span class="sxs-lookup"><span data-stu-id="7ba35-126">The payload for method requests and responses is a JSON document up to 8KB.</span></span>

## <a name="reference-topics"></a><span data-ttu-id="7ba35-127">參考主題：</span><span class="sxs-lookup"><span data-stu-id="7ba35-127">Reference topics:</span></span>
<span data-ttu-id="7ba35-128">下列參考主題會提供您關於使用直接方法的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="7ba35-128">The following reference topics provide you with more information about using direct methods.</span></span>

## <a name="invoke-a-direct-method-from-a-back-end-app"></a><span data-ttu-id="7ba35-129">從後端應用程式叫用直接方法</span><span class="sxs-lookup"><span data-stu-id="7ba35-129">Invoke a direct method from a back-end app</span></span>
### <a name="method-invocation"></a><span data-ttu-id="7ba35-130">方法引動過程</span><span class="sxs-lookup"><span data-stu-id="7ba35-130">Method invocation</span></span>
<span data-ttu-id="7ba35-131">裝置上的直接方法引動過程是 HTTP 呼叫，包含︰</span><span class="sxs-lookup"><span data-stu-id="7ba35-131">Direct method invocations on a device are HTTP calls which comprise:</span></span>

* <span data-ttu-id="7ba35-132">裝置特定的 *URI* (`{iot hub}/twins/{device id}/methods/`)</span><span class="sxs-lookup"><span data-stu-id="7ba35-132">The *URI* specific to the device (`{iot hub}/twins/{device id}/methods/`)</span></span>
* <span data-ttu-id="7ba35-133">POST *方法*</span><span class="sxs-lookup"><span data-stu-id="7ba35-133">The POST *method*</span></span>
* <span data-ttu-id="7ba35-134">*標頭*，其中包含授權、要求識別碼、內容類型及內容編碼</span><span class="sxs-lookup"><span data-stu-id="7ba35-134">*Headers* which contain the authorization, request ID, content type, and content encoding</span></span>
* <span data-ttu-id="7ba35-135">透明 JSON *本文*格式如下︰</span><span class="sxs-lookup"><span data-stu-id="7ba35-135">A transparent JSON *body* in the following format:</span></span>

```
{
    "methodName": "reboot",
    "responseTimeoutInSeconds": 200,
    "payload": {
        "input1": "someInput",
        "input2": "anotherInput"
    }
}
```

<span data-ttu-id="7ba35-136">逾時 (秒)。</span><span class="sxs-lookup"><span data-stu-id="7ba35-136">Timeout is in seconds.</span></span> <span data-ttu-id="7ba35-137">如果未設定逾時，它會預設為 30 秒。</span><span class="sxs-lookup"><span data-stu-id="7ba35-137">If timeout is not set, it defaults to 30 seconds.</span></span>

### <a name="response"></a><span data-ttu-id="7ba35-138">Response</span><span class="sxs-lookup"><span data-stu-id="7ba35-138">Response</span></span>
<span data-ttu-id="7ba35-139">後端應用程式收到的回應包含︰</span><span class="sxs-lookup"><span data-stu-id="7ba35-139">The back-end app receives a response which comprises:</span></span>

* <span data-ttu-id="7ba35-140">*HTTP 狀態碼*，用於來自 IoT 中樞的錯誤，包括裝置目前未連接的 404 錯誤</span><span class="sxs-lookup"><span data-stu-id="7ba35-140">*HTTP status code*, which is used for errors coming from the IoT Hub, including a 404 error for devices not currently connected</span></span>
* <span data-ttu-id="7ba35-141">*標頭*，其中包含 ETag、要求識別碼、內容類型及內容編碼</span><span class="sxs-lookup"><span data-stu-id="7ba35-141">*Headers* which contain the ETag, request ID, content type, and content encoding</span></span>
* <span data-ttu-id="7ba35-142">JSON *本文*格式如下︰</span><span class="sxs-lookup"><span data-stu-id="7ba35-142">A JSON *body* in the following format:</span></span>

```
{
    "status" : 201,
    "payload" : {...}
}
```

   <span data-ttu-id="7ba35-143">`status` 和 `body` 都是由裝置提供，用來回應裝置本身的狀態碼和/或描述。</span><span class="sxs-lookup"><span data-stu-id="7ba35-143">Both `status` and `body` are provided by the device and used to respond with the device's own status code and/or description.</span></span>

## <a name="handle-a-direct-method-on-a-device"></a><span data-ttu-id="7ba35-144">在裝置上處理直接方法</span><span class="sxs-lookup"><span data-stu-id="7ba35-144">Handle a direct method on a device</span></span>
### <a name="method-invocation"></a><span data-ttu-id="7ba35-145">方法引動過程</span><span class="sxs-lookup"><span data-stu-id="7ba35-145">Method invocation</span></span>
<span data-ttu-id="7ba35-146">裝置會接收 MQTT 主題的直接方法要求︰`$iothub/methods/POST/{method name}/?$rid={request id}`</span><span class="sxs-lookup"><span data-stu-id="7ba35-146">Devices receive direct method requests on the MQTT topic: `$iothub/methods/POST/{method name}/?$rid={request id}`</span></span>

<span data-ttu-id="7ba35-147">裝置所接收的本文格式如下︰</span><span class="sxs-lookup"><span data-stu-id="7ba35-147">The body which the device receives is in the following format:</span></span>

```
{
    "input1": "someInput",
    "input2": "anotherInput"
}
```

<span data-ttu-id="7ba35-148">方法要求為 QoS 0。</span><span class="sxs-lookup"><span data-stu-id="7ba35-148">Method requests are QoS 0.</span></span>

### <a name="response"></a><span data-ttu-id="7ba35-149">Response</span><span class="sxs-lookup"><span data-stu-id="7ba35-149">Response</span></span>
<span data-ttu-id="7ba35-150">裝置會傳送回應至 `$iothub/methods/res/{status}/?$rid={request id}`，其中︰</span><span class="sxs-lookup"><span data-stu-id="7ba35-150">The device sends responses to `$iothub/methods/res/{status}/?$rid={request id}`, where:</span></span>

* <span data-ttu-id="7ba35-151">`status` 屬性是方法執行的裝置提供狀態。</span><span class="sxs-lookup"><span data-stu-id="7ba35-151">The `status` property is the device-supplied status of method execution.</span></span>
* <span data-ttu-id="7ba35-152">`$rid` 屬性是從 IoT 中樞接收的方法引動過程的要求識別碼。</span><span class="sxs-lookup"><span data-stu-id="7ba35-152">The `$rid` property is the request ID from the method invocation received from IoT Hub.</span></span>

<span data-ttu-id="7ba35-153">本文是由裝置設定，而且可以是任何狀態。</span><span class="sxs-lookup"><span data-stu-id="7ba35-153">The body is set by the device and can be any status.</span></span>

## <a name="additional-reference-material"></a><span data-ttu-id="7ba35-154">其他參考資料</span><span class="sxs-lookup"><span data-stu-id="7ba35-154">Additional reference material</span></span>
<span data-ttu-id="7ba35-155">IoT 中樞開發人員指南中的其他參考主題包括︰</span><span class="sxs-lookup"><span data-stu-id="7ba35-155">Other reference topics in the IoT Hub developer guide include:</span></span>

* <span data-ttu-id="7ba35-156">[IoT 中樞端點][lnk-endpoints]說明每個 IoT 中樞公開給執行階段和管理作業的各種端點。</span><span class="sxs-lookup"><span data-stu-id="7ba35-156">[IoT Hub endpoints][lnk-endpoints] describes the various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="7ba35-157">[節流和配額][lnk-quotas]說明適用於 IoT 中樞服務的配額，和使用服務時所預期的節流行為。</span><span class="sxs-lookup"><span data-stu-id="7ba35-157">[Throttling and quotas][lnk-quotas] describes the quotas that apply to the IoT Hub service and the throttling behavior to expect when you use the service.</span></span>
* <span data-ttu-id="7ba35-158">[Azure IoT 裝置和服務 SDK][lnk-sdks] 列出各種語言 SDK，可供您在開發與「IoT 中樞」互動的裝置和服務應用程式時使用。</span><span class="sxs-lookup"><span data-stu-id="7ba35-158">[Azure IoT device and service SDKs][lnk-sdks] lists the various language SDKs you can use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="7ba35-159">[裝置對應項、作業和訊息路由的 IoT 中樞查詢語言][lnk-query]說明可用於從 IoT 中樞擷取有關裝置對應項和作業資訊的 IoT 中樞查詢語言。</span><span class="sxs-lookup"><span data-stu-id="7ba35-159">[IoT Hub query language for device twins, jobs, and message routing][lnk-query] describes the IoT Hub query language you can use to retrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="7ba35-160">[IoT 中樞 MQTT 支援][lnk-devguide-mqtt]針對 MQTT 通訊協定提供 IoT 中樞支援的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="7ba35-160">[IoT Hub MQTT support][lnk-devguide-mqtt] provides more information about IoT Hub support for the MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7ba35-161">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7ba35-161">Next steps</span></span>
<span data-ttu-id="7ba35-162">現在您已了解如何使用直接方法，接下來您可能對下列 IoT 中樞開發人員指南主題感興趣︰</span><span class="sxs-lookup"><span data-stu-id="7ba35-162">Now you have learned how to use direct methods, you may be interested in the following IoT Hub developer guide topic:</span></span>

* <span data-ttu-id="7ba35-163">[排程多個裝置上的作業][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="7ba35-163">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="7ba35-164">如果您想要嘗試本文章所述的概念，您可能會對下列 IoT 中樞教學課程感興趣：</span><span class="sxs-lookup"><span data-stu-id="7ba35-164">If you would like to try out some of the concepts described in this article, you may be interested in the following IoT Hub tutorial:</span></span>

* <span data-ttu-id="7ba35-165">[使用直接方法][lnk-methods-tutorial]</span><span class="sxs-lookup"><span data-stu-id="7ba35-165">[Use direct methods][lnk-methods-tutorial]</span></span>

<!-- links and images -->

[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-devguide-messages]: iot-hub-devguide-messaging.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
