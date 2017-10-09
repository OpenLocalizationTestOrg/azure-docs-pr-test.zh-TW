---
title: "aaaUnderstand Azure IoT Hub 裝置到雲端訊息 |Microsoft 文件"
description: "開發人員指南-如何 toouse 裝置到雲端訊息與 IoT 中樞。 包含傳送遙測和非 telemtry 資料，並使用 toodeliver 訊息路由的相關資訊。"
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: dobett
ms.openlocfilehash: 07dc8a6be747365c7efbc528ab2762b0d9790758
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="send-device-to-cloud-messages-tooiot-hub"></a><span data-ttu-id="e7bf5-104">傳送裝置到雲端訊息 tooIoT 中樞</span><span class="sxs-lookup"><span data-stu-id="e7bf5-104">Send device-to-cloud messages tooIoT Hub</span></span>

<span data-ttu-id="e7bf5-105">toosend 時間序列遙測和警示的來源裝置 tooyour 方案後端，請從您的裝置 tooyour IoT 中樞傳送裝置到雲端訊息。</span><span class="sxs-lookup"><span data-stu-id="e7bf5-105">toosend time-series telemetry and alerts from your devices tooyour solution back end, send device-to-cloud messages from your device tooyour IoT hub.</span></span> <span data-ttu-id="e7bf5-106">如需 IoT 中樞所支援之其他裝置到雲端選項的討論，請參閱[裝置對雲端通訊指引][lnk-d2c-guidance]。</span><span class="sxs-lookup"><span data-stu-id="e7bf5-106">For a discussion of other device-to-cloud options supported by IoT Hub, see [Device-to-cloud communications guidance][lnk-d2c-guidance].</span></span>

<span data-ttu-id="e7bf5-107">您透過裝置面向端點傳送裝置到雲端訊息 (**/devices/{deviceId}/messages/events**)。</span><span class="sxs-lookup"><span data-stu-id="e7bf5-107">You send device-to-cloud messages through a device-facing endpoint (**/devices/{deviceId}/messages/events**).</span></span> <span data-ttu-id="e7bf5-108">路由規則，然後將您的郵件 tooone hello 服務向端點的路由 IoT 中樞上。</span><span class="sxs-lookup"><span data-stu-id="e7bf5-108">Routing rules then route your messages tooone of hello service-facing endpoints on your IoT hub.</span></span> <span data-ttu-id="e7bf5-109">路由規則使用 hello 標頭和本文 hello 裝置到雲端訊息通過集線器 toodetermine 其中 tooroute 它們。</span><span class="sxs-lookup"><span data-stu-id="e7bf5-109">Routing rules use hello headers and body of hello device-to-cloud messages flowing through your hub toodetermine where tooroute them.</span></span> <span data-ttu-id="e7bf5-110">根據預設，訊息會路由的 toohello 內建的服務對向端點 (**事件訊息/**)，也就是與相容[事件中心][lnk-event-hubs]。</span><span class="sxs-lookup"><span data-stu-id="e7bf5-110">By default, messages are routed toohello built-in service-facing endpoint (**messages/events**), that is compatible with [Event Hubs][lnk-event-hubs].</span></span> <span data-ttu-id="e7bf5-111">因此，您可以使用標準[事件中心 」 整合和 Sdk] [ lnk-compatible-endpoint] tooreceive 方案中的裝置到雲端訊息後端。</span><span class="sxs-lookup"><span data-stu-id="e7bf5-111">Therefore, you can use standard [Event Hubs integration and SDKs][lnk-compatible-endpoint] tooreceive device-to-cloud messages in your solution back end.</span></span>

<span data-ttu-id="e7bf5-112">IoT 中樞使用串流訊息模式實作裝置到雲端傳訊。</span><span class="sxs-lookup"><span data-stu-id="e7bf5-112">IoT Hub implements device-to-cloud messaging using a streaming messaging pattern.</span></span> <span data-ttu-id="e7bf5-113">IoT 中樞的裝置到雲端訊息是更像[事件中心][ lnk-event-hubs] *事件*比[Service Bus] [ lnk-servicebus]*訊息*中會有大量通過 hello 服務可由多個讀取器讀取的事件。</span><span class="sxs-lookup"><span data-stu-id="e7bf5-113">IoT Hub's device-to-cloud messages are more like [Event Hubs][lnk-event-hubs] *events* than [Service Bus][lnk-servicebus] *messages* in that there is a high volume of events passing through hello service that can be read by multiple readers.</span></span>

<span data-ttu-id="e7bf5-114">裝置的雲端與 IoT 中樞傳訊具有下列特性的 hello:</span><span class="sxs-lookup"><span data-stu-id="e7bf5-114">Device-to-cloud messaging with IoT Hub has hello following characteristics:</span></span>

* <span data-ttu-id="e7bf5-115">裝置到雲端訊息是永久性的 IoT 中樞的預設保留**事件訊息/**向上 tooseven 天的結束點。</span><span class="sxs-lookup"><span data-stu-id="e7bf5-115">Device-to-cloud messages are durable and retained in an IoT hub's default **messages/events** endpoint for up tooseven days.</span></span>
* <span data-ttu-id="e7bf5-116">裝置到雲端訊息最多可達 256 KB，並可以分組 toooptimize 傳送的批次中。</span><span class="sxs-lookup"><span data-stu-id="e7bf5-116">Device-to-cloud messages can be at most 256 KB, and can be grouped in batches toooptimize sends.</span></span> <span data-ttu-id="e7bf5-117">批次最多可達 256 KB。</span><span class="sxs-lookup"><span data-stu-id="e7bf5-117">Batches can be at most 256 KB.</span></span>
* <span data-ttu-id="e7bf5-118">Hello 中所述[控制存取 tooIoT 中樞][ lnk-devguide-security] ] 區段中，IoT 中樞可讓每一裝置的驗證和存取控制。</span><span class="sxs-lookup"><span data-stu-id="e7bf5-118">As explained in hello [Control access tooIoT Hub][lnk-devguide-security] section, IoT Hub enables per-device authentication and access control.</span></span>
* <span data-ttu-id="e7bf5-119">IoT 中樞可讓您 toocreate 個 too10 自訂端點。</span><span class="sxs-lookup"><span data-stu-id="e7bf5-119">IoT Hub allows you toocreate up too10 custom endpoints.</span></span> <span data-ttu-id="e7bf5-120">訊息會傳遞 toohello 根據您的 IoT 中樞上設定路由的端點。</span><span class="sxs-lookup"><span data-stu-id="e7bf5-120">Messages are delivered toohello endpoints based on routes configured on your IoT hub.</span></span> <span data-ttu-id="e7bf5-121">如需詳細資訊，請參閱[路由規則](#routing-rules)。</span><span class="sxs-lookup"><span data-stu-id="e7bf5-121">For more information, see [Routing rules](#routing-rules).</span></span>
* <span data-ttu-id="e7bf5-122">IoT 中樞可同時連線到數百萬部裝置 (請參閱[配額和節流][lnk-quotas])。</span><span class="sxs-lookup"><span data-stu-id="e7bf5-122">IoT Hub enables millions of simultaneously connected devices (see [Quotas and throttling][lnk-quotas]).</span></span>
* <span data-ttu-id="e7bf5-123">IoT 中樞不允許任意進行資料分割。</span><span class="sxs-lookup"><span data-stu-id="e7bf5-123">IoT Hub does not allow arbitrary partitioning.</span></span> <span data-ttu-id="e7bf5-124">裝置到雲端訊息會根據其原始的 **deviceId**進行分割。</span><span class="sxs-lookup"><span data-stu-id="e7bf5-124">Device-to-cloud messages are partitioned based on their originating **deviceId**.</span></span>

<span data-ttu-id="e7bf5-125">如需 hello IoT 中樞與事件中心服務的 hello 差異的詳細資訊，請參閱[Azure IoT 中樞的比較與 Azure 事件中心][lnk-comparison]。</span><span class="sxs-lookup"><span data-stu-id="e7bf5-125">For more information about hello differences between hello IoT Hub and Event Hubs services, see [Comparison of Azure IoT Hub and Azure Event Hubs][lnk-comparison].</span></span>

## <a name="send-non-telemetry-traffic"></a><span data-ttu-id="e7bf5-126">傳送非遙測流量</span><span class="sxs-lookup"><span data-stu-id="e7bf5-126">Send non-telemetry traffic</span></span>

<span data-ttu-id="e7bf5-127">通常，除了 tootelemetry 資料點、 裝置傳送訊息和需要個別的執行與 hello 方案後端中的處理要求。</span><span class="sxs-lookup"><span data-stu-id="e7bf5-127">Often, in addition tootelemetry data points, devices send messages and requests that require separate execution and handling in hello solution back end.</span></span> <span data-ttu-id="e7bf5-128">例如，必須觸發在 hello 特定動作的重要警示後端。</span><span class="sxs-lookup"><span data-stu-id="e7bf5-128">For example, critical alerts that must trigger a specific action in hello back end.</span></span> <span data-ttu-id="e7bf5-129">您可以輕鬆地撰寫[路由規則][ lnk-devguide-custom] toosend 這些類型的訊息 tooan 端點專用 tootheir 處理 hello 訊息上的任一個標頭或 hello 訊息內文中的值為基礎。</span><span class="sxs-lookup"><span data-stu-id="e7bf5-129">You can easily write a [routing rule][lnk-devguide-custom] toosend these types of messages tooan endpoint dedicated tootheir processing based on either a header on hello message or a value in hello message body.</span></span>

<span data-ttu-id="e7bf5-130">如需 hello 最佳方式 tooprocess 這種訊息的詳細資訊，請參閱 hello[教學課程： 如何 tooprocess IoT 中樞裝置到雲端訊息][ lnk-d2c-tutorial]教學課程。</span><span class="sxs-lookup"><span data-stu-id="e7bf5-130">For more information about hello best way tooprocess this kind of message, see hello [Tutorial: How tooprocess IoT Hub device-to-cloud messages][lnk-d2c-tutorial] tutorial.</span></span>

## <a name="route-device-to-cloud-messages"></a><span data-ttu-id="e7bf5-131">路由傳送裝置到雲端訊息</span><span class="sxs-lookup"><span data-stu-id="e7bf5-131">Route device-to-cloud messages</span></span>

<span data-ttu-id="e7bf5-132">您有兩個路由裝置到雲端訊息 tooyour 後端應用程式的選項：</span><span class="sxs-lookup"><span data-stu-id="e7bf5-132">You have two options for routing device-to-cloud messages tooyour back-end apps:</span></span>

* <span data-ttu-id="e7bf5-133">使用內建的 hello[事件中樞相容端點][ lnk-compatible-endpoint] tooenable 後端應用程式 tooread hello 裝置到雲端所收到的訊息 hello 中樞。</span><span class="sxs-lookup"><span data-stu-id="e7bf5-133">Use hello built-in [Event Hub-compatible endpoint][lnk-compatible-endpoint] tooenable back-end apps tooread hello device-to-cloud messages received by hello hub.</span></span> <span data-ttu-id="e7bf5-134">toolearn 有關內建事件中樞相容端點 hello，請參閱[讀取 hello 內建端點的裝置到雲端訊息][lnk-devguide-builtin]。</span><span class="sxs-lookup"><span data-stu-id="e7bf5-134">toolearn about hello built-in Event Hub-compatible endpoint, see [Read device-to-cloud messages from hello built-in endpoint][lnk-devguide-builtin].</span></span>
* <span data-ttu-id="e7bf5-135">使用您的 IoT 中樞中的路由規則 toosend 訊息 toocustom 端點。</span><span class="sxs-lookup"><span data-stu-id="e7bf5-135">Use routing rules toosend messages toocustom endpoints in your IoT hub.</span></span> <span data-ttu-id="e7bf5-136">自訂端點可讓您使用事件中心、 服務匯流排佇列或服務匯流排主題的後端應用程式 tooread 裝置到雲端訊息。</span><span class="sxs-lookup"><span data-stu-id="e7bf5-136">Custom endpoints enable your back-end apps tooread device-to-cloud messages using Event Hubs, Service Bus queues, or Service Bus topics.</span></span> <span data-ttu-id="e7bf5-137">toolearn 有關路由和自訂端點，請參閱[用於裝置到雲端訊息的自訂端點和路由規則][lnk-devguide-custom]。</span><span class="sxs-lookup"><span data-stu-id="e7bf5-137">toolearn about routing and custom endpoints, see [Use custom endpoints and routing rules for device-to-cloud messages][lnk-devguide-custom].</span></span>

## <a name="anti-spoofing-properties"></a><span data-ttu-id="e7bf5-138">防詐騙屬性</span><span class="sxs-lookup"><span data-stu-id="e7bf5-138">Anti-spoofing properties</span></span>

<span data-ttu-id="e7bf5-139">詐騙裝置到雲端訊息，IoT 中樞中的下列屬性的 hello 與所有訊息的戳記 tooavoid 裝置：</span><span class="sxs-lookup"><span data-stu-id="e7bf5-139">tooavoid device spoofing in device-to-cloud messages, IoT Hub stamps all messages with hello following properties:</span></span>

* <span data-ttu-id="e7bf5-140">**ConnectionDeviceId**</span><span class="sxs-lookup"><span data-stu-id="e7bf5-140">**ConnectionDeviceId**</span></span>
* <span data-ttu-id="e7bf5-141">**ConnectionDeviceGenerationId**</span><span class="sxs-lookup"><span data-stu-id="e7bf5-141">**ConnectionDeviceGenerationId**</span></span>
* <span data-ttu-id="e7bf5-142">**ConnectionAuthMethod**</span><span class="sxs-lookup"><span data-stu-id="e7bf5-142">**ConnectionAuthMethod**</span></span>

<span data-ttu-id="e7bf5-143">hello 前兩個包含 hello **deviceId**和**generationId**的 hello 源自裝置，請依照[裝置身分識別屬性][lnk-device-properties]。</span><span class="sxs-lookup"><span data-stu-id="e7bf5-143">hello first two contain hello **deviceId** and **generationId** of hello originating device, as per [Device identity properties][lnk-device-properties].</span></span>

<span data-ttu-id="e7bf5-144">hello **ConnectionAuthMethod**屬性包含序列化的 JSON 物件，具有下列屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="e7bf5-144">hello **ConnectionAuthMethod** property contains a JSON serialized object, with hello following properties:</span></span>

```json
{
  "scope": "{ hub | device}",
  "type": "{ symkey | sas}",
  "issuer": "iothub"
}
```

## <a name="next-steps"></a><span data-ttu-id="e7bf5-145">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e7bf5-145">Next steps</span></span>

<span data-ttu-id="e7bf5-146">如需 hello Sdk，您可以使用 toosend 裝置到雲端訊息，請參閱[Azure IoT Sdk][lnk-sdks]。</span><span class="sxs-lookup"><span data-stu-id="e7bf5-146">For information about hello SDKs you can use toosend device-to-cloud messages, see [Azure IoT SDKs][lnk-sdks].</span></span>

<span data-ttu-id="e7bf5-147">hello[開始][ lnk-get-started]教學課程告訴您如何 toosend 裝置到雲端訊息從模擬與實體裝置。</span><span class="sxs-lookup"><span data-stu-id="e7bf5-147">hello [Get Started][lnk-get-started] tutorials show you how toosend device-to-cloud messages from both simulated and physical devices.</span></span> <span data-ttu-id="e7bf5-148">如需詳細資訊，請參閱 hello[使用路由的處理序 IoT 中樞裝置到雲端訊息][ lnk-d2c-tutorial]教學課程。</span><span class="sxs-lookup"><span data-stu-id="e7bf5-148">For more detail, see hello [Process IoT Hub device-to-cloud messages using routes][lnk-d2c-tutorial] tutorial.</span></span>

[lnk-devguide-builtin]: iot-hub-devguide-messages-read-builtin.md
[lnk-devguide-custom]: iot-hub-devguide-messages-read-custom.md
[lnk-comparison]: iot-hub-compare-event-hubs.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md
[lnk-get-started]: iot-hub-get-started.md

[lnk-event-hubs]: http://azure.microsoft.com/documentation/services/event-hubs/
[lnk-servicebus]: http://azure.microsoft.com/documentation/services/service-bus/
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-compatible-endpoint]: iot-hub-devguide-messages-read-builtin.md
[lnk-device-properties]: iot-hub-devguide-identity-registry.md#device-identity-properties
[lnk-devguide-security]: iot-hub-devguide-security.md
[lnk-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md
