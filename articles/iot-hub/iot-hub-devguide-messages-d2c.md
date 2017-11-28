---
title: "了解 Azure IoT 中樞的裝置到雲端傳訊 | Microsoft Docs"
description: "開發人員指南 - 如何使用 IoT 中樞的裝置到雲端傳訊。 包含傳送遙測和非遙測資料，以及使用路由來傳遞訊息的相關資訊。"
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
ms.openlocfilehash: d856e26084ee79386a2e8e0e527804bda86b477b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="send-device-to-cloud-messages-to-iot-hub"></a><span data-ttu-id="a4158-104">將裝置到雲端訊息傳送至 IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="a4158-104">Send device-to-cloud messages to IoT Hub</span></span>

<span data-ttu-id="a4158-105">若要從您的裝置傳送時間序列遙測和警示到您的解決方案後端，請從您的裝置傳送裝置到雲端訊息到您的 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="a4158-105">To send time-series telemetry and alerts from your devices to your solution back end, send device-to-cloud messages from your device to your IoT hub.</span></span> <span data-ttu-id="a4158-106">如需 IoT 中樞所支援之其他裝置到雲端選項的討論，請參閱[裝置對雲端通訊指引][lnk-d2c-guidance]。</span><span class="sxs-lookup"><span data-stu-id="a4158-106">For a discussion of other device-to-cloud options supported by IoT Hub, see [Device-to-cloud communications guidance][lnk-d2c-guidance].</span></span>

<span data-ttu-id="a4158-107">您透過裝置面向端點傳送裝置到雲端訊息 (**/devices/{deviceId}/messages/events**)。</span><span class="sxs-lookup"><span data-stu-id="a4158-107">You send device-to-cloud messages through a device-facing endpoint (**/devices/{deviceId}/messages/events**).</span></span> <span data-ttu-id="a4158-108">路由規則接著會將訊息路由至您 IoT 中樞上的其中一個服務面向端點。</span><span class="sxs-lookup"><span data-stu-id="a4158-108">Routing rules then route your messages to one of the service-facing endpoints on your IoT hub.</span></span> <span data-ttu-id="a4158-109">路由規則會使用流經您中樞的裝置到雲端訊息標頭和內文，決定訊息的路由目標。</span><span class="sxs-lookup"><span data-stu-id="a4158-109">Routing rules use the headers and body of the device-to-cloud messages flowing through your hub to determine where to route them.</span></span> <span data-ttu-id="a4158-110">根據預設，訊息會路由至內建的服務面向端點 (**messages/events**)，此端點與[事件中樞][lnk-event-hubs]相容。</span><span class="sxs-lookup"><span data-stu-id="a4158-110">By default, messages are routed to the built-in service-facing endpoint (**messages/events**), that is compatible with [Event Hubs][lnk-event-hubs].</span></span> <span data-ttu-id="a4158-111">因此，您可以使用標準[事件中樞整合和 SDK][lnk-compatible-endpoint] 在解決方案後端接收裝置到雲端訊息。</span><span class="sxs-lookup"><span data-stu-id="a4158-111">Therefore, you can use standard [Event Hubs integration and SDKs][lnk-compatible-endpoint] to receive device-to-cloud messages in your solution back end.</span></span>

<span data-ttu-id="a4158-112">IoT 中樞使用串流訊息模式實作裝置到雲端傳訊。</span><span class="sxs-lookup"><span data-stu-id="a4158-112">IoT Hub implements device-to-cloud messaging using a streaming messaging pattern.</span></span> <span data-ttu-id="a4158-113">IoT 中樞的裝置到雲端訊息與[事件中樞][lnk-event-hubs]*事件*較為相似 (而不像[服務匯流排][lnk-servicebus]*訊息*) 因為會有大量的事件傳遞給該服務，並可由多個讀取器讀取。</span><span class="sxs-lookup"><span data-stu-id="a4158-113">IoT Hub's device-to-cloud messages are more like [Event Hubs][lnk-event-hubs] *events* than [Service Bus][lnk-servicebus] *messages* in that there is a high volume of events passing through the service that can be read by multiple readers.</span></span>

<span data-ttu-id="a4158-114">IoT 中樞的裝置對雲端傳訊具有下列特性：</span><span class="sxs-lookup"><span data-stu-id="a4158-114">Device-to-cloud messaging with IoT Hub has the following characteristics:</span></span>

* <span data-ttu-id="a4158-115">裝置到雲端訊息會長期保留在 IoT 中樞的預設 **messages/events** 端點，最多達七天。</span><span class="sxs-lookup"><span data-stu-id="a4158-115">Device-to-cloud messages are durable and retained in an IoT hub's default **messages/events** endpoint for up to seven days.</span></span>
* <span data-ttu-id="a4158-116">裝置到雲端訊息最大可能為 256 KB，而且可分成數個批次以最佳化傳送。</span><span class="sxs-lookup"><span data-stu-id="a4158-116">Device-to-cloud messages can be at most 256 KB, and can be grouped in batches to optimize sends.</span></span> <span data-ttu-id="a4158-117">批次最多可達 256 KB。</span><span class="sxs-lookup"><span data-stu-id="a4158-117">Batches can be at most 256 KB.</span></span>
* <span data-ttu-id="a4158-118">如[控制 IoT 中樞的存取權][lnk-devguide-security]一節所述，IoT 中樞會啟用每一裝置的驗證和存取控制。</span><span class="sxs-lookup"><span data-stu-id="a4158-118">As explained in the [Control access to IoT Hub][lnk-devguide-security] section, IoT Hub enables per-device authentication and access control.</span></span>
* <span data-ttu-id="a4158-119">IoT 中樞可讓您建立最多 10 個自訂端點。</span><span class="sxs-lookup"><span data-stu-id="a4158-119">IoT Hub allows you to create up to 10 custom endpoints.</span></span> <span data-ttu-id="a4158-120">訊息會根據您 IoT 中樞上所設定的路由傳遞至端點。</span><span class="sxs-lookup"><span data-stu-id="a4158-120">Messages are delivered to the endpoints based on routes configured on your IoT hub.</span></span> <span data-ttu-id="a4158-121">如需詳細資訊，請參閱[路由規則](#routing-rules)。</span><span class="sxs-lookup"><span data-stu-id="a4158-121">For more information, see [Routing rules](#routing-rules).</span></span>
* <span data-ttu-id="a4158-122">IoT 中樞可同時連線到數百萬部裝置 (請參閱[配額和節流][lnk-quotas])。</span><span class="sxs-lookup"><span data-stu-id="a4158-122">IoT Hub enables millions of simultaneously connected devices (see [Quotas and throttling][lnk-quotas]).</span></span>
* <span data-ttu-id="a4158-123">IoT 中樞不允許任意進行資料分割。</span><span class="sxs-lookup"><span data-stu-id="a4158-123">IoT Hub does not allow arbitrary partitioning.</span></span> <span data-ttu-id="a4158-124">裝置到雲端訊息會根據其原始的 **deviceId**進行分割。</span><span class="sxs-lookup"><span data-stu-id="a4158-124">Device-to-cloud messages are partitioned based on their originating **deviceId**.</span></span>

<span data-ttu-id="a4158-125">如需 IoT 中樞與事件中樞服務之間差異的詳細資訊，請參閱 [Azure IoT 中樞和 Azure 事件中樞的比較][lnk-comparison]。</span><span class="sxs-lookup"><span data-stu-id="a4158-125">For more information about the differences between the IoT Hub and Event Hubs services, see [Comparison of Azure IoT Hub and Azure Event Hubs][lnk-comparison].</span></span>

## <a name="send-non-telemetry-traffic"></a><span data-ttu-id="a4158-126">傳送非遙測流量</span><span class="sxs-lookup"><span data-stu-id="a4158-126">Send non-telemetry traffic</span></span>

<span data-ttu-id="a4158-127">通常除了遙測資料點之外，裝置也會傳送需要在解決方案後端進行個別執行與處理的訊息及要求。</span><span class="sxs-lookup"><span data-stu-id="a4158-127">Often, in addition to telemetry data points, devices send messages and requests that require separate execution and handling in the solution back end.</span></span> <span data-ttu-id="a4158-128">例如，必須於後端觸發特定動作的重大警示。</span><span class="sxs-lookup"><span data-stu-id="a4158-128">For example, critical alerts that must trigger a specific action in the back end.</span></span> <span data-ttu-id="a4158-129">您可以輕鬆地撰寫[路由規則][lnk-devguide-custom]，以根據訊息的標頭或訊息內文中的值，將這些訊息類型傳送至專屬的處理端點。</span><span class="sxs-lookup"><span data-stu-id="a4158-129">You can easily write a [routing rule][lnk-devguide-custom] to send these types of messages to an endpoint dedicated to their processing based on either a header on the message or a value in the message body.</span></span>

<span data-ttu-id="a4158-130">如需處理這種訊息最佳方式的詳細資訊，請參閱[教學課程：如何處理 IoT 中樞裝置到雲端訊息][lnk-d2c-tutorial]教學課程。</span><span class="sxs-lookup"><span data-stu-id="a4158-130">For more information about the best way to process this kind of message, see the [Tutorial: How to process IoT Hub device-to-cloud messages][lnk-d2c-tutorial] tutorial.</span></span>

## <a name="route-device-to-cloud-messages"></a><span data-ttu-id="a4158-131">路由傳送裝置到雲端訊息</span><span class="sxs-lookup"><span data-stu-id="a4158-131">Route device-to-cloud messages</span></span>

<span data-ttu-id="a4158-132">您有兩個選項可將裝置對雲端訊息路由傳送到後端應用程式：</span><span class="sxs-lookup"><span data-stu-id="a4158-132">You have two options for routing device-to-cloud messages to your back-end apps:</span></span>

* <span data-ttu-id="a4158-133">使用內建[事件中樞相容端點][lnk-compatible-endpoint]，讓後端應用程式讀取中樞所接收的裝置到雲端訊息。</span><span class="sxs-lookup"><span data-stu-id="a4158-133">Use the built-in [Event Hub-compatible endpoint][lnk-compatible-endpoint] to enable back-end apps to read the device-to-cloud messages received by the hub.</span></span> <span data-ttu-id="a4158-134">若要深入了解內建事件中樞相容端點，請參閱[從內建端點讀取裝置對雲端訊息][lnk-devguide-builtin]。</span><span class="sxs-lookup"><span data-stu-id="a4158-134">To learn about the built-in Event Hub-compatible endpoint, see [Read device-to-cloud messages from the built-in endpoint][lnk-devguide-builtin].</span></span>
* <span data-ttu-id="a4158-135">使用路由規則，將訊息傳送至您 IoT 中樞內的自訂端點。</span><span class="sxs-lookup"><span data-stu-id="a4158-135">Use routing rules to send messages to custom endpoints in your IoT hub.</span></span> <span data-ttu-id="a4158-136">自訂端點可讓您的後端應用程式使用事件中樞、服務匯流排佇列或服務匯流排主題，來讀取裝置對雲端訊息。</span><span class="sxs-lookup"><span data-stu-id="a4158-136">Custom endpoints enable your back-end apps to read device-to-cloud messages using Event Hubs, Service Bus queues, or Service Bus topics.</span></span> <span data-ttu-id="a4158-137">若要深入了解路由和自訂端點，請參閱[使用適用於裝置對雲端訊息的自訂端點和路由規則][lnk-devguide-custom]。</span><span class="sxs-lookup"><span data-stu-id="a4158-137">To learn about routing and custom endpoints, see [Use custom endpoints and routing rules for device-to-cloud messages][lnk-devguide-custom].</span></span>

## <a name="anti-spoofing-properties"></a><span data-ttu-id="a4158-138">防詐騙屬性</span><span class="sxs-lookup"><span data-stu-id="a4158-138">Anti-spoofing properties</span></span>

<span data-ttu-id="a4158-139">為了避免裝置到雲端的訊息中出現裝置詐騙，IoT 中樞使用下列屬性在所有訊息上加上戳記：</span><span class="sxs-lookup"><span data-stu-id="a4158-139">To avoid device spoofing in device-to-cloud messages, IoT Hub stamps all messages with the following properties:</span></span>

* <span data-ttu-id="a4158-140">**ConnectionDeviceId**</span><span class="sxs-lookup"><span data-stu-id="a4158-140">**ConnectionDeviceId**</span></span>
* <span data-ttu-id="a4158-141">**ConnectionDeviceGenerationId**</span><span class="sxs-lookup"><span data-stu-id="a4158-141">**ConnectionDeviceGenerationId**</span></span>
* <span data-ttu-id="a4158-142">**ConnectionAuthMethod**</span><span class="sxs-lookup"><span data-stu-id="a4158-142">**ConnectionAuthMethod**</span></span>

<span data-ttu-id="a4158-143">前兩個屬性包含來源裝置的 **deviceId** 和 **generationId** (依據[裝置身分識別屬性][lnk-device-properties])。</span><span class="sxs-lookup"><span data-stu-id="a4158-143">The first two contain the **deviceId** and **generationId** of the originating device, as per [Device identity properties][lnk-device-properties].</span></span>

<span data-ttu-id="a4158-144">**ConnectionAuthMethod** 屬性包含具有下列屬性的 JSON 序列化物件︰</span><span class="sxs-lookup"><span data-stu-id="a4158-144">The **ConnectionAuthMethod** property contains a JSON serialized object, with the following properties:</span></span>

```json
{
  "scope": "{ hub | device}",
  "type": "{ symkey | sas}",
  "issuer": "iothub"
}
```

## <a name="next-steps"></a><span data-ttu-id="a4158-145">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a4158-145">Next steps</span></span>

<span data-ttu-id="a4158-146">如需您可以用來傳送裝置對雲端訊息之 SDK 的資訊，請參閱 [Azure IoT SDK][lnk-sdks]。</span><span class="sxs-lookup"><span data-stu-id="a4158-146">For information about the SDKs you can use to send device-to-cloud messages, see [Azure IoT SDKs][lnk-sdks].</span></span>

<span data-ttu-id="a4158-147">[快速入門][lnk-get-started]教學課程示範如何從模擬和實體裝置傳送裝置對雲端訊息。</span><span class="sxs-lookup"><span data-stu-id="a4158-147">The [Get Started][lnk-get-started] tutorials show you how to send device-to-cloud messages from both simulated and physical devices.</span></span> <span data-ttu-id="a4158-148">如需詳細資訊，請參閱[使用路由處理 IoT 中樞的裝置到雲端訊息][lnk-d2c-tutorial]教學課程。</span><span class="sxs-lookup"><span data-stu-id="a4158-148">For more detail, see the [Process IoT Hub device-to-cloud messages using routes][lnk-d2c-tutorial] tutorial.</span></span>

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
