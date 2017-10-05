---
title: "比較 Azure IoT 中樞與 Azure 事件中樞 | Microsoft Docs"
description: "IoT 中樞和事件中樞 Azure 服務的比較，重點在於功能差異和使用案例。 比較的項目包括支援的通訊協定、裝置管理、監視及檔案上傳。"
services: iot-hub
documentationcenter: 
author: fsautomata
manager: timlt
editor: 
ms.assetid: aeddea62-8302-48e2-9aad-c5a0e5f5abe9
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: elioda
ms.openlocfilehash: a37df79a38a35b61cca72918d4d893a4bfc83b7e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="comparison-of-azure-iot-hub-and-azure-event-hubs"></a><span data-ttu-id="070bc-104">Azure IoT 中樞和 Azure 事件中樞的比較</span><span class="sxs-lookup"><span data-stu-id="070bc-104">Comparison of Azure IoT Hub and Azure Event Hubs</span></span>
<span data-ttu-id="070bc-105">IoT 中樞的主要使用案例之一是從裝置收集遙測。</span><span class="sxs-lookup"><span data-stu-id="070bc-105">One of the main use cases for IoT Hub is to gather telemetry from devices.</span></span> <span data-ttu-id="070bc-106">因此，經常會比較 IoT 中樞與 [Azure 事件中樞][Azure Event Hubs]。</span><span class="sxs-lookup"><span data-stu-id="070bc-106">For this reason, IoT Hub is often compared to [Azure Event Hubs][Azure Event Hubs].</span></span> <span data-ttu-id="070bc-107">類似於 IoT 中樞，事件中樞是事件處理服務，它能提供大規模進入雲端的事件和遙測入口，並具備低延遲和高可靠性等特性。</span><span class="sxs-lookup"><span data-stu-id="070bc-107">Like IoT Hub, Event Hubs is an event processing service that enables event and telemetry ingress to the cloud at massive scale, with low latency and high reliability.</span></span>

<span data-ttu-id="070bc-108">不過，這些服務有許多差異，將在下表中詳述：</span><span class="sxs-lookup"><span data-stu-id="070bc-108">However, the services have many differences, which are detailed in the following table:</span></span>

| <span data-ttu-id="070bc-109">領域</span><span class="sxs-lookup"><span data-stu-id="070bc-109">Area</span></span> | <span data-ttu-id="070bc-110">IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="070bc-110">IoT Hub</span></span> | <span data-ttu-id="070bc-111">事件中樞</span><span class="sxs-lookup"><span data-stu-id="070bc-111">Event Hubs</span></span> |
| --- | --- | --- |
| <span data-ttu-id="070bc-112">通訊模式</span><span class="sxs-lookup"><span data-stu-id="070bc-112">Communication patterns</span></span> | <span data-ttu-id="070bc-113">能夠進行[裝置到雲端通訊][lnk-d2c-guidance] (傳訊、檔案上傳和報告屬性) 和[雲端到裝置通訊][lnk-c2d-guidance] (直接方法、所需屬性、傳訊)。</span><span class="sxs-lookup"><span data-stu-id="070bc-113">Enables [device-to-cloud communications][lnk-d2c-guidance] (messaging, file uploads, and reported properties) and [cloud-to-device communications][lnk-c2d-guidance] (direct methods, desired properties, messaging).</span></span> |<span data-ttu-id="070bc-114">僅提供事件輸入 (通常視為裝置到雲端案例)。</span><span class="sxs-lookup"><span data-stu-id="070bc-114">Only enables event ingress (usually considered for device-to-cloud scenarios).</span></span> |
| <span data-ttu-id="070bc-115">裝置狀態資訊</span><span class="sxs-lookup"><span data-stu-id="070bc-115">Device state information</span></span> | <span data-ttu-id="070bc-116">[裝置對應項][lnk-twins]可以儲存和查詢裝置狀態資訊。</span><span class="sxs-lookup"><span data-stu-id="070bc-116">[Device twins][lnk-twins] can store and query device state information.</span></span> | <span data-ttu-id="070bc-117">無法儲存裝置狀態資訊。</span><span class="sxs-lookup"><span data-stu-id="070bc-117">No device state information can be stored.</span></span> |
| <span data-ttu-id="070bc-118">裝置通訊協定支援</span><span class="sxs-lookup"><span data-stu-id="070bc-118">Device protocol support</span></span> |<span data-ttu-id="070bc-119">支援 MQTT、MQTT over WebSockets、AMQP、AMQP over WebSocket 及 HTTP。</span><span class="sxs-lookup"><span data-stu-id="070bc-119">Supports MQTT, MQTT over WebSockets, AMQP, AMQP over WebSockets, and HTTP.</span></span> <span data-ttu-id="070bc-120">此外，IoT 中樞還可搭配 [Azure IoT 通訊協定閘道][lnk-azure-protocol-gateway]來使用，後者是支援自訂通訊協定的可自訂通訊協定閘道實作。</span><span class="sxs-lookup"><span data-stu-id="070bc-120">Additionally, IoT Hub works with the [Azure IoT protocol gateway][lnk-azure-protocol-gateway], a customizable protocol gateway implementation to support custom protocols.</span></span> |<span data-ttu-id="070bc-121">支援 AMQP、透過 WebSockets 的 AMQP 和 HTTP。</span><span class="sxs-lookup"><span data-stu-id="070bc-121">Supports AMQP, AMQP over WebSockets, and HTTP.</span></span> |
| <span data-ttu-id="070bc-122">安全性</span><span class="sxs-lookup"><span data-stu-id="070bc-122">Security</span></span> |<span data-ttu-id="070bc-123">提供每個裝置的身分識別與可撤銷的存取控制。</span><span class="sxs-lookup"><span data-stu-id="070bc-123">Provides per-device identity and revocable access control.</span></span> <span data-ttu-id="070bc-124">請參閱 [IoT 中樞開發人員指南的安全性章節]。</span><span class="sxs-lookup"><span data-stu-id="070bc-124">See the [Security section of the IoT Hub developer guide].</span></span> |<span data-ttu-id="070bc-125">提供全事件中樞的[共用存取原則][Event Hubs - security]，以及透過[發行者原則][Event Hubs publisher policies]的有限撤銷支援。</span><span class="sxs-lookup"><span data-stu-id="070bc-125">Provides Event Hubs-wide [shared access policies][Event Hubs - security], with limited revocation support through [publisher's policies][Event Hubs publisher policies].</span></span> <span data-ttu-id="070bc-126">IoT 解決方案通常需要實作自訂解決方案來支援每個裝置的認證以及防詐騙措施。</span><span class="sxs-lookup"><span data-stu-id="070bc-126">IoT solutions are often required to implement a custom solution to support per-device credentials and anti-spoofing measures.</span></span> |
| <span data-ttu-id="070bc-127">作業監視</span><span class="sxs-lookup"><span data-stu-id="070bc-127">Operations monitoring</span></span> |<span data-ttu-id="070bc-128">可讓 IoT 解決方案訂閱一組豐富的裝置身分識別管理和連線事件，例如個別裝置驗證錯誤、節流和格式錯誤的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="070bc-128">Enables IoT solutions to subscribe to a rich set of device identity management and connectivity events such as individual device authentication errors, throttling, and bad format exceptions.</span></span> <span data-ttu-id="070bc-129">這些事件可讓您快速識別個別裝置層級的連線問題。</span><span class="sxs-lookup"><span data-stu-id="070bc-129">These events enable you to quickly identify connectivity problems at the individual device level.</span></span> |<span data-ttu-id="070bc-130">僅公開彙總的度量。</span><span class="sxs-lookup"><span data-stu-id="070bc-130">Exposes only aggregate metrics.</span></span> |
| <span data-ttu-id="070bc-131">調整</span><span class="sxs-lookup"><span data-stu-id="070bc-131">Scale</span></span> |<span data-ttu-id="070bc-132">已最佳化以支援數百萬同時連接的裝置。</span><span class="sxs-lookup"><span data-stu-id="070bc-132">Is optimized to support millions of simultaneously connected devices.</span></span> |<span data-ttu-id="070bc-133">依據每個 [Azure 事件中樞配額][Azure Event Hubs quotas]計量連線數目。</span><span class="sxs-lookup"><span data-stu-id="070bc-133">Meters the connections as per [Azure Event Hubs quotas][Azure Event Hubs quotas].</span></span> <span data-ttu-id="070bc-134">另一方面，事件中樞可讓您指定每個傳送訊息的分割。</span><span class="sxs-lookup"><span data-stu-id="070bc-134">On the other hand, Event Hubs enables you to specify the partition for each message sent.</span></span> |
| <span data-ttu-id="070bc-135">裝置 SDK</span><span class="sxs-lookup"><span data-stu-id="070bc-135">Device SDKs</span></span> |<span data-ttu-id="070bc-136">除了直接 MQTT、AMQP 和 HTTP API 以外，提供[裝置 SDK][Azure IoT SDKs] 給各種平台和語言。</span><span class="sxs-lookup"><span data-stu-id="070bc-136">Provides [device SDKs][Azure IoT SDKs] for a large variety of platforms and languages, in addition to direct MQTT, AMQP, and HTTP APIs.</span></span> |<span data-ttu-id="070bc-137">除了 AMQP 和 HTTP 傳送介面以外，在 .NET、Java 和 C 上都提供支援。</span><span class="sxs-lookup"><span data-stu-id="070bc-137">Is supported on .NET, Java, and C, in addition to AMQP and HTTP send interfaces.</span></span> |
| <span data-ttu-id="070bc-138">檔案上傳</span><span class="sxs-lookup"><span data-stu-id="070bc-138">File upload</span></span> |<span data-ttu-id="070bc-139">可讓 IoT 解決方案將檔案從裝置上傳到雲端。</span><span class="sxs-lookup"><span data-stu-id="070bc-139">Enables IoT solutions to upload files from devices to the cloud.</span></span> <span data-ttu-id="070bc-140">包含一個用於整合工作流程的檔案通知端點，以及一個用於支援偵錯的作業監視類別。</span><span class="sxs-lookup"><span data-stu-id="070bc-140">Includes a file notification endpoint for workflow integration and an operations monitoring category for debugging support.</span></span> | <span data-ttu-id="070bc-141">不支援。</span><span class="sxs-lookup"><span data-stu-id="070bc-141">Not supported.</span></span> |
| <span data-ttu-id="070bc-142">將訊息路由至多個端點</span><span class="sxs-lookup"><span data-stu-id="070bc-142">Route messages to multiple endpoints</span></span> | <span data-ttu-id="070bc-143">最多支援 10 個自訂端點。</span><span class="sxs-lookup"><span data-stu-id="070bc-143">Up to 10 custom endpoints are supported.</span></span> <span data-ttu-id="070bc-144">規則會決定訊息路由至自訂端點的方式。</span><span class="sxs-lookup"><span data-stu-id="070bc-144">Rules determine how messages are routed to custom endpoints.</span></span> <span data-ttu-id="070bc-145">如需詳細資訊，請參閱[使用 IoT 中樞傳送及接收訊息][lnk-devguide-messaging]。</span><span class="sxs-lookup"><span data-stu-id="070bc-145">For more information, see [Send and receive messages with IoT Hub][lnk-devguide-messaging].</span></span> | <span data-ttu-id="070bc-146">需要撰寫及裝載額外的程式碼才能發送訊息。</span><span class="sxs-lookup"><span data-stu-id="070bc-146">Requires additional code to be written and hosted for message dispatching.</span></span> |

<span data-ttu-id="070bc-147">總而言之，即使唯一的使用案例是裝置到雲端遙測輸入，IoT 中樞仍會提供為 IoT 裝置連線所設計的服務。</span><span class="sxs-lookup"><span data-stu-id="070bc-147">In summary, even if the only use case is device-to-cloud telemetry ingress, IoT Hub provides a service that is designed for IoT device connectivity.</span></span> <span data-ttu-id="070bc-148">它會持續擴充具備 IoT 功能之案例的價值主張。</span><span class="sxs-lookup"><span data-stu-id="070bc-148">It continues to expand the value propositions for these scenarios with IoT-specific features.</span></span> <span data-ttu-id="070bc-149">事件中樞的設計對象是資料中心之間及資料中心內部案例的大規模事件輸入。</span><span class="sxs-lookup"><span data-stu-id="070bc-149">Event Hubs is designed for event ingress at a massive scale, both in the context of inter-datacenter and intra-datacenter scenarios.</span></span>

<span data-ttu-id="070bc-150">在相同解決方案中同時使用 IoT 中樞和事件中樞的情況並不常見。</span><span class="sxs-lookup"><span data-stu-id="070bc-150">It is not uncommon to use both IoT Hub and Event Hubs in the same solution.</span></span> <span data-ttu-id="070bc-151">IoT 中樞是處理裝置到雲端通訊，而事件中樞處理後期事件輸入至即時處理引擎。</span><span class="sxs-lookup"><span data-stu-id="070bc-151">IoT Hub handles the device-to-cloud communication, and Event Hubs handles later-stage event ingress into real-time processing engines.</span></span>

### <a name="next-steps"></a><span data-ttu-id="070bc-152">後續步驟</span><span class="sxs-lookup"><span data-stu-id="070bc-152">Next steps</span></span>
<span data-ttu-id="070bc-153">若要深入了解如何規劃 IoT 中樞部署，請參閱[調整、HA 及 DR][lnk-scaling]。</span><span class="sxs-lookup"><span data-stu-id="070bc-153">To learn more about planning your IoT Hub deployment, see [Scaling, HA, and DR][lnk-scaling].</span></span>

<span data-ttu-id="070bc-154">若要進一步探索 IoT 中樞的功能，請參閱︰</span><span class="sxs-lookup"><span data-stu-id="070bc-154">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="070bc-155">[IoT 中樞開發人員指南][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="070bc-155">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="070bc-156">[使用 IoT Edge 來模擬裝置][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="070bc-156">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>

[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md

[Azure Event Hubs]: ../event-hubs/event-hubs-what-is-event-hubs.md
[IoT 中樞開發人員指南的安全性章節]: iot-hub-devguide-security.md
[Event Hubs - security]: ../event-hubs/event-hubs-authentication-and-security-model-overview.md
[Event Hubs publisher policies]: ../event-hubs/event-hubs-features.md#event-publishers
[Azure Event Hubs quotas]: ../event-hubs/event-hubs-quotas.md
[Azure IoT SDKs]: https://github.com/Azure/azure-iot-sdks
[lnk-azure-protocol-gateway]: iot-hub-protocol-gateway.md

[lnk-scaling]: iot-hub-scaling.md
[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
[lnk-devguide-messaging]: iot-hub-devguide-messaging.md
