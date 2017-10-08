---
title: "Azure IoT 中樞 aaaUnderstand 直接方法 |Microsoft 文件"
description: "開發人員指南-使用直接的方法 tooinvoke 程式碼，在您的服務應用程式的裝置上。"
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
ms.openlocfilehash: 0d15d44a0c3e1d1cda1669c1ed011c2f932e3d92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="understand-and-invoke-direct-methods-from-iot-hub"></a><span data-ttu-id="358ec-103">了解 IoT 中樞的直接方法並從中樞叫用直接方法</span><span class="sxs-lookup"><span data-stu-id="358ec-103">Understand and invoke direct methods from IoT Hub</span></span>
## <a name="overview"></a><span data-ttu-id="358ec-104">概觀</span><span class="sxs-lookup"><span data-stu-id="358ec-104">Overview</span></span>
<span data-ttu-id="358ec-105">IoT 中樞讓您能夠 tooinvoke 直接的方法在 hello 雲端的裝置上。</span><span class="sxs-lookup"><span data-stu-id="358ec-105">IoT Hub gives you ability tooinvoke direct methods on devices from hello cloud.</span></span> <span data-ttu-id="358ec-106">直接方法代表與裝置的類似 tooan，在於它們成功或失敗 （之後立即使用者指定的逾時），呼叫 HTTP 要求-回覆之間的互動。</span><span class="sxs-lookup"><span data-stu-id="358ec-106">Direct methods represent a request-reply interaction with a device similar tooan HTTP call in that they succeed or fail immediately (after a user-specified timeout).</span></span> <span data-ttu-id="358ec-107">這是適合的情況下立即採取行動的 hello 課程 hello 裝置是否可以 toorespond，例如傳送 SMS 喚醒 tooa 裝置，如果裝置已離線 (SMS 正在成本高於方法呼叫) 而有所不同。</span><span class="sxs-lookup"><span data-stu-id="358ec-107">This is useful for scenarios where hello course of immediate action is different depending on whether hello device was able toorespond, such as sending an SMS wake-up tooa device if a device is offline (SMS being more expensive than a method call).</span></span>

<span data-ttu-id="358ec-108">每個裝置方法的目標是單一裝置。</span><span class="sxs-lookup"><span data-stu-id="358ec-108">Each device method targets a single device.</span></span> <span data-ttu-id="358ec-109">[作業][ lnk-devguide-jobs]提供多個裝置，方式 tooinvoke 直接的方法，並排定方法引動過程已中斷連線的裝置。</span><span class="sxs-lookup"><span data-stu-id="358ec-109">[Jobs][lnk-devguide-jobs] provide a way tooinvoke direct methods on multiple devices, and schedule method invocation for disconnected devices.</span></span>

<span data-ttu-id="358ec-110">IoT 中樞上具有**服務連線**權限的任何人都可以叫用裝置上的方法。</span><span class="sxs-lookup"><span data-stu-id="358ec-110">Anyone with **service connect** permissions on IoT Hub may invoke a method on a device.</span></span>

### <a name="when-toouse"></a><span data-ttu-id="358ec-111">當 toouse</span><span class="sxs-lookup"><span data-stu-id="358ec-111">When toouse</span></span>
<span data-ttu-id="358ec-112">直接的方法會遵循要求-回應模式，而需要立即確認其結果，通常是互動式控制權，hello 裝置，例如 tooturn 上 風扇的通訊開放。</span><span class="sxs-lookup"><span data-stu-id="358ec-112">Direct methods follow a request-response pattern and are meant for communications that require immediate confirmation of their result, usually interactive control of hello device, for example tooturn on a fan.</span></span>

<span data-ttu-id="358ec-113">請參閱太[雲端到裝置通訊指引][ lnk-c2d-guidance]使用所需的屬性之間的不確定，直接方法或雲端到裝置訊息。</span><span class="sxs-lookup"><span data-stu-id="358ec-113">Refer too[Cloud-to-device communication guidance][lnk-c2d-guidance] if in doubt between using desired properties, direct methods, or cloud-to-device messages.</span></span>

## <a name="method-lifecycle"></a><span data-ttu-id="358ec-114">方法生命週期</span><span class="sxs-lookup"><span data-stu-id="358ec-114">Method lifecycle</span></span>
<span data-ttu-id="358ec-115">直接的方法會實作 hello 裝置上，而且可能需要零或多個輸入 hello 方法裝載 toocorrectly 中的具現化。</span><span class="sxs-lookup"><span data-stu-id="358ec-115">Direct methods are implemented on hello device and may require zero or more inputs in hello method payload toocorrectly instantiate.</span></span> <span data-ttu-id="358ec-116">您可以透過面向服務的 URI 叫用直接方法 (`{iot hub}/twins/{device id}/methods/`)。</span><span class="sxs-lookup"><span data-stu-id="358ec-116">You invoke a direct method through a service-facing URI (`{iot hub}/twins/{device id}/methods/`).</span></span> <span data-ttu-id="358ec-117">裝置會透過裝置特定 MQTT 主題收到直接方法 (`$iothub/methods/POST/{method name}/`)。</span><span class="sxs-lookup"><span data-stu-id="358ec-117">A device receives direct methods through a device-specific MQTT topic (`$iothub/methods/POST/{method name}/`).</span></span> <span data-ttu-id="358ec-118">我們可能支援其他的裝置後端網路通訊協定，在未來的 hello 直接的方法。</span><span class="sxs-lookup"><span data-stu-id="358ec-118">We may support direct methods on additional device-side networking protocols in hello future.</span></span>

> [!NOTE]
> <span data-ttu-id="358ec-119">當您叫用的裝置上直接方法時，屬性名稱和值只能包含 US-ASCII 可列印英數字元、 在 hello 下列設定除外： ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``。</span><span class="sxs-lookup"><span data-stu-id="358ec-119">When you invoke a direct method on a device, property names and values can only contain US-ASCII printable alphanumeric, except any in hello following set: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.</span></span>
> 
> 

<span data-ttu-id="358ec-120">直接方法是同步，可能會成功或失敗之後 hello 逾時期限 (預設： 30 秒，可設定總 too3600 秒)。</span><span class="sxs-lookup"><span data-stu-id="358ec-120">Direct methods are synchronous and either succeed or fail after hello timeout period (default: 30 seconds, settable up too3600 seconds).</span></span> <span data-ttu-id="358ec-121">直接的方法可用於互動式案例中，您的裝置 tooact 才 hello 裝置是線上和接收的命令，例如開啟的燈號電話。</span><span class="sxs-lookup"><span data-stu-id="358ec-121">Direct methods are useful in interactive scenarios where you want a device tooact if and only if hello device is online and receiving commands, such as turning on a light from a phone.</span></span> <span data-ttu-id="358ec-122">在這些情況下，您想 toosee 立即成功或失敗所以 hello 雲端服務可以儘速處理 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="358ec-122">In these scenarios, you want toosee an immediate success or failure so hello cloud service can act on hello result as soon as possible.</span></span> <span data-ttu-id="358ec-123">hello 裝置可能會傳回 hello 方法，因為某些訊息本文，但不需要 hello 方法 toodo 如此。</span><span class="sxs-lookup"><span data-stu-id="358ec-123">hello device may return some message body as a result of hello method, but it isn't required for hello method toodo so.</span></span> <span data-ttu-id="358ec-124">不保證方法呼叫的順序或任何並行語意。</span><span class="sxs-lookup"><span data-stu-id="358ec-124">There is no guarantee on ordering or any concurrency semantics on method calls.</span></span>

<span data-ttu-id="358ec-125">直接的方法是僅限 HTTP 從 hello 雲端端，和 MQTT 僅從 hello 裝置端。</span><span class="sxs-lookup"><span data-stu-id="358ec-125">Direct method are HTTP-only from hello cloud side, and MQTT-only from hello device side.</span></span>

<span data-ttu-id="358ec-126">方法要求和回應的 hello 裝載是總 too8KB JSON 文件。</span><span class="sxs-lookup"><span data-stu-id="358ec-126">hello payload for method requests and responses is a JSON document up too8KB.</span></span>

## <a name="reference-topics"></a><span data-ttu-id="358ec-127">參考主題：</span><span class="sxs-lookup"><span data-stu-id="358ec-127">Reference topics:</span></span>
<span data-ttu-id="358ec-128">hello 下列參考主題提供有關使用直接的方法的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="358ec-128">hello following reference topics provide you with more information about using direct methods.</span></span>

## <a name="invoke-a-direct-method-from-a-back-end-app"></a><span data-ttu-id="358ec-129">從後端應用程式叫用直接方法</span><span class="sxs-lookup"><span data-stu-id="358ec-129">Invoke a direct method from a back-end app</span></span>
### <a name="method-invocation"></a><span data-ttu-id="358ec-130">方法引動過程</span><span class="sxs-lookup"><span data-stu-id="358ec-130">Method invocation</span></span>
<span data-ttu-id="358ec-131">裝置上的直接方法引動過程是 HTTP 呼叫，包含︰</span><span class="sxs-lookup"><span data-stu-id="358ec-131">Direct method invocations on a device are HTTP calls which comprise:</span></span>

* <span data-ttu-id="358ec-132">hello *URI*特定 toohello 裝置 (`{iot hub}/twins/{device id}/methods/`)</span><span class="sxs-lookup"><span data-stu-id="358ec-132">hello *URI* specific toohello device (`{iot hub}/twins/{device id}/methods/`)</span></span>
* <span data-ttu-id="358ec-133">hello POST*方法*</span><span class="sxs-lookup"><span data-stu-id="358ec-133">hello POST *method*</span></span>
* <span data-ttu-id="358ec-134">*標頭*其中包含 hello 的授權，請要求識別碼、 內容類型和內容編碼方式</span><span class="sxs-lookup"><span data-stu-id="358ec-134">*Headers* which contain hello authorization, request ID, content type, and content encoding</span></span>
* <span data-ttu-id="358ec-135">透明 JSON*主體*在 hello 下列格式：</span><span class="sxs-lookup"><span data-stu-id="358ec-135">A transparent JSON *body* in hello following format:</span></span>

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

<span data-ttu-id="358ec-136">逾時 (秒)。</span><span class="sxs-lookup"><span data-stu-id="358ec-136">Timeout is in seconds.</span></span> <span data-ttu-id="358ec-137">如果未設定逾時，它會預設 too30 秒。</span><span class="sxs-lookup"><span data-stu-id="358ec-137">If timeout is not set, it defaults too30 seconds.</span></span>

### <a name="response"></a><span data-ttu-id="358ec-138">Response</span><span class="sxs-lookup"><span data-stu-id="358ec-138">Response</span></span>
<span data-ttu-id="358ec-139">hello 後端應用程式收到的回應所組成：</span><span class="sxs-lookup"><span data-stu-id="358ec-139">hello back-end app receives a response which comprises:</span></span>

* <span data-ttu-id="358ec-140">*HTTP 狀態碼*，用來自 hello IoT 中樞的錯誤，包括 404 錯誤的裝置目前未連接</span><span class="sxs-lookup"><span data-stu-id="358ec-140">*HTTP status code*, which is used for errors coming from hello IoT Hub, including a 404 error for devices not currently connected</span></span>
* <span data-ttu-id="358ec-141">*標頭*其中包含 hello ETag，要求識別碼、 內容類型和內容編碼方式</span><span class="sxs-lookup"><span data-stu-id="358ec-141">*Headers* which contain hello ETag, request ID, content type, and content encoding</span></span>
* <span data-ttu-id="358ec-142">JSON*主體*在 hello 下列格式：</span><span class="sxs-lookup"><span data-stu-id="358ec-142">A JSON *body* in hello following format:</span></span>

```
{
    "status" : 201,
    "payload" : {...}
}
```

   <span data-ttu-id="358ec-143">同時`status`和`body`hello 裝置所提供，且 toorespond 搭配 hello 裝置本身的狀態碼和/或描述。</span><span class="sxs-lookup"><span data-stu-id="358ec-143">Both `status` and `body` are provided by hello device and used toorespond with hello device's own status code and/or description.</span></span>

## <a name="handle-a-direct-method-on-a-device"></a><span data-ttu-id="358ec-144">在裝置上處理直接方法</span><span class="sxs-lookup"><span data-stu-id="358ec-144">Handle a direct method on a device</span></span>
### <a name="method-invocation"></a><span data-ttu-id="358ec-145">方法引動過程</span><span class="sxs-lookup"><span data-stu-id="358ec-145">Method invocation</span></span>
<span data-ttu-id="358ec-146">裝置收到 hello MQTT 主題上的直接方法要求：`$iothub/methods/POST/{method name}/?$rid={request id}`</span><span class="sxs-lookup"><span data-stu-id="358ec-146">Devices receive direct method requests on hello MQTT topic: `$iothub/methods/POST/{method name}/?$rid={request id}`</span></span>

<span data-ttu-id="358ec-147">哪些 hello 裝置收到 hello 主體為下列格式的 hello:</span><span class="sxs-lookup"><span data-stu-id="358ec-147">hello body which hello device receives is in hello following format:</span></span>

```
{
    "input1": "someInput",
    "input2": "anotherInput"
}
```

<span data-ttu-id="358ec-148">方法要求為 QoS 0。</span><span class="sxs-lookup"><span data-stu-id="358ec-148">Method requests are QoS 0.</span></span>

### <a name="response"></a><span data-ttu-id="358ec-149">Response</span><span class="sxs-lookup"><span data-stu-id="358ec-149">Response</span></span>
<span data-ttu-id="358ec-150">hello 裝置所傳送的回應太`$iothub/methods/res/{status}/?$rid={request id}`，其中：</span><span class="sxs-lookup"><span data-stu-id="358ec-150">hello device sends responses too`$iothub/methods/res/{status}/?$rid={request id}`, where:</span></span>

* <span data-ttu-id="358ec-151">hello`status`屬性是 hello 方法執行的裝置提供狀態。</span><span class="sxs-lookup"><span data-stu-id="358ec-151">hello `status` property is hello device-supplied status of method execution.</span></span>
* <span data-ttu-id="358ec-152">hello`$rid`屬性是從 IoT 中樞從收到 hello 方法引動過程的 hello 要求識別碼。</span><span class="sxs-lookup"><span data-stu-id="358ec-152">hello `$rid` property is hello request ID from hello method invocation received from IoT Hub.</span></span>

<span data-ttu-id="358ec-153">hello 主體由 hello 裝置設定，而且可以是任何狀態。</span><span class="sxs-lookup"><span data-stu-id="358ec-153">hello body is set by hello device and can be any status.</span></span>

## <a name="additional-reference-material"></a><span data-ttu-id="358ec-154">其他參考資料</span><span class="sxs-lookup"><span data-stu-id="358ec-154">Additional reference material</span></span>
<span data-ttu-id="358ec-155">Hello IoT 中樞開發人員指南 》 中的其他參考主題包括：</span><span class="sxs-lookup"><span data-stu-id="358ec-155">Other reference topics in hello IoT Hub developer guide include:</span></span>

* <span data-ttu-id="358ec-156">[IoT 中樞端點][ lnk-endpoints]描述 hello 各種執行階段和管理作業的每個 IoT 中樞會公開的端點。</span><span class="sxs-lookup"><span data-stu-id="358ec-156">[IoT Hub endpoints][lnk-endpoints] describes hello various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="358ec-157">[節流和配額][ lnk-quotas]描述 hello 配額套用 toohello IoT 中心服務和 hello 節流行為 tooexpect，當您使用 hello 服務。</span><span class="sxs-lookup"><span data-stu-id="358ec-157">[Throttling and quotas][lnk-quotas] describes hello quotas that apply toohello IoT Hub service and hello throttling behavior tooexpect when you use hello service.</span></span>
* <span data-ttu-id="358ec-158">[Azure IoT 裝置和服務 Sdk] [ lnk-sdks]清單 hello 各種語言互動的裝置和服務應用程式開發與 IoT 中樞時，您可以使用的 Sdk。</span><span class="sxs-lookup"><span data-stu-id="358ec-158">[Azure IoT device and service SDKs][lnk-sdks] lists hello various language SDKs you can use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="358ec-159">[IoT 中樞裝置雙、 作業和訊息路由的查詢語言][ lnk-query]描述 hello IoT 中樞的查詢語言，您可以使用您的裝置雙和作業相關的 tooretrieve 資訊從 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="358ec-159">[IoT Hub query language for device twins, jobs, and message routing][lnk-query] describes hello IoT Hub query language you can use tooretrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="358ec-160">[IoT 中樞 MQTT 支援][ lnk-devguide-mqtt] hello MQTT 通訊協定提供 IoT 中樞支援的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="358ec-160">[IoT Hub MQTT support][lnk-devguide-mqtt] provides more information about IoT Hub support for hello MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="358ec-161">後續步驟</span><span class="sxs-lookup"><span data-stu-id="358ec-161">Next steps</span></span>
<span data-ttu-id="358ec-162">現在您已經學會如何 toouse 直接的方法，您可能會想要 hello 遵循 IoT 中樞開發人員指南 》 主題：</span><span class="sxs-lookup"><span data-stu-id="358ec-162">Now you have learned how toouse direct methods, you may be interested in hello following IoT Hub developer guide topic:</span></span>

* <span data-ttu-id="358ec-163">[排程多個裝置上的作業][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="358ec-163">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="358ec-164">如果您想要查看這篇文章中所述的 hello 概念 tootry，您可能想要遵循 IoT 中樞教學課程中的 hello:</span><span class="sxs-lookup"><span data-stu-id="358ec-164">If you would like tootry out some of hello concepts described in this article, you may be interested in hello following IoT Hub tutorial:</span></span>

* <span data-ttu-id="358ec-165">[使用直接方法][lnk-methods-tutorial]</span><span class="sxs-lookup"><span data-stu-id="358ec-165">[Use direct methods][lnk-methods-tutorial]</span></span>

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
