---
title: "aaaCompare Azure IoT 中樞 tooAzure 事件中心 |Microsoft 文件"
description: "IoT 中樞 hello 和功能差異與使用案例，反白顯示的事件中心的 Azure 服務的比較。 hello 比較包含支援的通訊協定，裝置管理、 監視，並將檔案上傳。"
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
ms.openlocfilehash: e5f546b54e29860498d540abfc86a41c4662c0df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="comparison-of-azure-iot-hub-and-azure-event-hubs"></a><span data-ttu-id="e0cae-104">Azure IoT 中樞和 Azure 事件中樞的比較</span><span class="sxs-lookup"><span data-stu-id="e0cae-104">Comparison of Azure IoT Hub and Azure Event Hubs</span></span>
<span data-ttu-id="e0cae-105">IoT 中樞的 hello 主要的使用案例的其中一個是從裝置 toogather 遙測。</span><span class="sxs-lookup"><span data-stu-id="e0cae-105">One of hello main use cases for IoT Hub is toogather telemetry from devices.</span></span> <span data-ttu-id="e0cae-106">基於這個理由，IoT 中樞通常比較太[Azure 事件中心][Azure Event Hubs]。</span><span class="sxs-lookup"><span data-stu-id="e0cae-106">For this reason, IoT Hub is often compared too[Azure Event Hubs][Azure Event Hubs].</span></span> <span data-ttu-id="e0cae-107">IoT 中樞，類似事件中心是事件處理服務，可讓事件和遙測 ingress toohello 雲端，同時可靠性高且延遲低的大幅延展。</span><span class="sxs-lookup"><span data-stu-id="e0cae-107">Like IoT Hub, Event Hubs is an event processing service that enables event and telemetry ingress toohello cloud at massive scale, with low latency and high reliability.</span></span>

<span data-ttu-id="e0cae-108">不過，hello 服務有許多差異，詳述於下表中的 hello:</span><span class="sxs-lookup"><span data-stu-id="e0cae-108">However, hello services have many differences, which are detailed in hello following table:</span></span>

| <span data-ttu-id="e0cae-109">領域</span><span class="sxs-lookup"><span data-stu-id="e0cae-109">Area</span></span> | <span data-ttu-id="e0cae-110">IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="e0cae-110">IoT Hub</span></span> | <span data-ttu-id="e0cae-111">事件中樞</span><span class="sxs-lookup"><span data-stu-id="e0cae-111">Event Hubs</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e0cae-112">通訊模式</span><span class="sxs-lookup"><span data-stu-id="e0cae-112">Communication patterns</span></span> | <span data-ttu-id="e0cae-113">能夠進行[裝置到雲端通訊][lnk-d2c-guidance] (傳訊、檔案上傳和報告屬性) 和[雲端到裝置通訊][lnk-c2d-guidance] (直接方法、所需屬性、傳訊)。</span><span class="sxs-lookup"><span data-stu-id="e0cae-113">Enables [device-to-cloud communications][lnk-d2c-guidance] (messaging, file uploads, and reported properties) and [cloud-to-device communications][lnk-c2d-guidance] (direct methods, desired properties, messaging).</span></span> |<span data-ttu-id="e0cae-114">僅提供事件輸入 (通常視為裝置到雲端案例)。</span><span class="sxs-lookup"><span data-stu-id="e0cae-114">Only enables event ingress (usually considered for device-to-cloud scenarios).</span></span> |
| <span data-ttu-id="e0cae-115">裝置狀態資訊</span><span class="sxs-lookup"><span data-stu-id="e0cae-115">Device state information</span></span> | <span data-ttu-id="e0cae-116">[裝置對應項][lnk-twins]可以儲存和查詢裝置狀態資訊。</span><span class="sxs-lookup"><span data-stu-id="e0cae-116">[Device twins][lnk-twins] can store and query device state information.</span></span> | <span data-ttu-id="e0cae-117">無法儲存裝置狀態資訊。</span><span class="sxs-lookup"><span data-stu-id="e0cae-117">No device state information can be stored.</span></span> |
| <span data-ttu-id="e0cae-118">裝置通訊協定支援</span><span class="sxs-lookup"><span data-stu-id="e0cae-118">Device protocol support</span></span> |<span data-ttu-id="e0cae-119">支援 MQTT、MQTT over WebSockets、AMQP、AMQP over WebSocket 及 HTTP。</span><span class="sxs-lookup"><span data-stu-id="e0cae-119">Supports MQTT, MQTT over WebSockets, AMQP, AMQP over WebSockets, and HTTP.</span></span> <span data-ttu-id="e0cae-120">此外，IoT 中樞搭配 hello [Azure IoT 通訊協定閘道][lnk-azure-protocol-gateway]，可自訂的通訊協定閘道實作 toosupport 自訂通訊協定。</span><span class="sxs-lookup"><span data-stu-id="e0cae-120">Additionally, IoT Hub works with hello [Azure IoT protocol gateway][lnk-azure-protocol-gateway], a customizable protocol gateway implementation toosupport custom protocols.</span></span> |<span data-ttu-id="e0cae-121">支援 AMQP、透過 WebSockets 的 AMQP 和 HTTP。</span><span class="sxs-lookup"><span data-stu-id="e0cae-121">Supports AMQP, AMQP over WebSockets, and HTTP.</span></span> |
| <span data-ttu-id="e0cae-122">安全性</span><span class="sxs-lookup"><span data-stu-id="e0cae-122">Security</span></span> |<span data-ttu-id="e0cae-123">提供每個裝置的身分識別與可撤銷的存取控制。</span><span class="sxs-lookup"><span data-stu-id="e0cae-123">Provides per-device identity and revocable access control.</span></span> <span data-ttu-id="e0cae-124">請參閱 hello[安全性 &amp;gt; 一節的 hello IoT 中樞開發人員指南]。</span><span class="sxs-lookup"><span data-stu-id="e0cae-124">See hello [Security section of hello IoT Hub developer guide].</span></span> |<span data-ttu-id="e0cae-125">提供全事件中樞的[共用存取原則][Event Hubs - security]，以及透過[發行者原則][Event Hubs publisher policies]的有限撤銷支援。</span><span class="sxs-lookup"><span data-stu-id="e0cae-125">Provides Event Hubs-wide [shared access policies][Event Hubs - security], with limited revocation support through [publisher's policies][Event Hubs publisher policies].</span></span> <span data-ttu-id="e0cae-126">IoT 解決方案通常是需要的 tooimplement 自訂方案 toosupport 個別裝置認證和的防詐騙功能的量值。</span><span class="sxs-lookup"><span data-stu-id="e0cae-126">IoT solutions are often required tooimplement a custom solution toosupport per-device credentials and anti-spoofing measures.</span></span> |
| <span data-ttu-id="e0cae-127">作業監視</span><span class="sxs-lookup"><span data-stu-id="e0cae-127">Operations monitoring</span></span> |<span data-ttu-id="e0cae-128">可讓 IoT 解決方案 toosubscribe tooa 豐富的裝置身分識別管理和連接事件，例如個別的裝置驗證錯誤、 節流和格式錯誤的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="e0cae-128">Enables IoT solutions toosubscribe tooa rich set of device identity management and connectivity events such as individual device authentication errors, throttling, and bad format exceptions.</span></span> <span data-ttu-id="e0cae-129">這些事件可讓您 tooquickly 識別 hello 個別的裝置層級的連線問題。</span><span class="sxs-lookup"><span data-stu-id="e0cae-129">These events enable you tooquickly identify connectivity problems at hello individual device level.</span></span> |<span data-ttu-id="e0cae-130">僅公開彙總的度量。</span><span class="sxs-lookup"><span data-stu-id="e0cae-130">Exposes only aggregate metrics.</span></span> |
| <span data-ttu-id="e0cae-131">調整</span><span class="sxs-lookup"><span data-stu-id="e0cae-131">Scale</span></span> |<span data-ttu-id="e0cae-132">是最佳化的 toosupport 數以百萬計的同時連線的裝置。</span><span class="sxs-lookup"><span data-stu-id="e0cae-132">Is optimized toosupport millions of simultaneously connected devices.</span></span> |<span data-ttu-id="e0cae-133">公尺 hello 做為每個連線[Azure 事件中心配額][Azure Event Hubs quotas]。</span><span class="sxs-lookup"><span data-stu-id="e0cae-133">Meters hello connections as per [Azure Event Hubs quotas][Azure Event Hubs quotas].</span></span> <span data-ttu-id="e0cae-134">在 hello 另一方面，事件中心可讓您為每個訊息傳送的 toospecify hello 分割區。</span><span class="sxs-lookup"><span data-stu-id="e0cae-134">On hello other hand, Event Hubs enables you toospecify hello partition for each message sent.</span></span> |
| <span data-ttu-id="e0cae-135">裝置 SDK</span><span class="sxs-lookup"><span data-stu-id="e0cae-135">Device SDKs</span></span> |<span data-ttu-id="e0cae-136">提供[裝置 Sdk] [ Azure IoT SDKs]大型各種不同的平台和語言，加法 toodirect MQTT、 AMQP 和 HTTP 應用程式開發介面中的。</span><span class="sxs-lookup"><span data-stu-id="e0cae-136">Provides [device SDKs][Azure IoT SDKs] for a large variety of platforms and languages, in addition toodirect MQTT, AMQP, and HTTP APIs.</span></span> |<span data-ttu-id="e0cae-137">支援.NET、 Java 和 C，加法 tooAMQP 和 HTTP 傳送介面中。</span><span class="sxs-lookup"><span data-stu-id="e0cae-137">Is supported on .NET, Java, and C, in addition tooAMQP and HTTP send interfaces.</span></span> |
| <span data-ttu-id="e0cae-138">檔案上傳</span><span class="sxs-lookup"><span data-stu-id="e0cae-138">File upload</span></span> |<span data-ttu-id="e0cae-139">讓裝置 toohello 雲端的 IoT 解決方案 tooupload 檔案。</span><span class="sxs-lookup"><span data-stu-id="e0cae-139">Enables IoT solutions tooupload files from devices toohello cloud.</span></span> <span data-ttu-id="e0cae-140">包含一個用於整合工作流程的檔案通知端點，以及一個用於支援偵錯的作業監視類別。</span><span class="sxs-lookup"><span data-stu-id="e0cae-140">Includes a file notification endpoint for workflow integration and an operations monitoring category for debugging support.</span></span> | <span data-ttu-id="e0cae-141">不支援。</span><span class="sxs-lookup"><span data-stu-id="e0cae-141">Not supported.</span></span> |
| <span data-ttu-id="e0cae-142">路由訊息 toomultiple 端點</span><span class="sxs-lookup"><span data-stu-id="e0cae-142">Route messages toomultiple endpoints</span></span> | <span data-ttu-id="e0cae-143">向上 too10 支援自訂端點。</span><span class="sxs-lookup"><span data-stu-id="e0cae-143">Up too10 custom endpoints are supported.</span></span> <span data-ttu-id="e0cae-144">規則會決定訊息的路由的 toocustom 端點的方式。</span><span class="sxs-lookup"><span data-stu-id="e0cae-144">Rules determine how messages are routed toocustom endpoints.</span></span> <span data-ttu-id="e0cae-145">如需詳細資訊，請參閱[使用 IoT 中樞傳送及接收訊息][lnk-devguide-messaging]。</span><span class="sxs-lookup"><span data-stu-id="e0cae-145">For more information, see [Send and receive messages with IoT Hub][lnk-devguide-messaging].</span></span> | <span data-ttu-id="e0cae-146">需要額外的程式碼 toobe 寫入，而訊息發送的裝載。</span><span class="sxs-lookup"><span data-stu-id="e0cae-146">Requires additional code toobe written and hosted for message dispatching.</span></span> |

<span data-ttu-id="e0cae-147">總而言之，即使 hello 唯一的使用案例是裝置到雲端遙測 ingress IoT 中樞提供的服務，設計 IoT 裝置連線。</span><span class="sxs-lookup"><span data-stu-id="e0cae-147">In summary, even if hello only use case is device-to-cloud telemetry ingress, IoT Hub provides a service that is designed for IoT device connectivity.</span></span> <span data-ttu-id="e0cae-148">它會繼續 tooexpand hello 價值主張 IoT 特定的功能與這些案例。</span><span class="sxs-lookup"><span data-stu-id="e0cae-148">It continues tooexpand hello value propositions for these scenarios with IoT-specific features.</span></span> <span data-ttu-id="e0cae-149">事件中心被針對大規模，兩者間資料中心與內部資料中心案例 hello 內容中的事件輸入。</span><span class="sxs-lookup"><span data-stu-id="e0cae-149">Event Hubs is designed for event ingress at a massive scale, both in hello context of inter-datacenter and intra-datacenter scenarios.</span></span>

<span data-ttu-id="e0cae-150">它不是很常見的 toouse IoT 中樞與中的事件中樞 hello 相同的方案。</span><span class="sxs-lookup"><span data-stu-id="e0cae-150">It is not uncommon toouse both IoT Hub and Event Hubs in hello same solution.</span></span> <span data-ttu-id="e0cae-151">IoT 中樞處理 hello 裝置到雲端的通訊，而事件中心處理後續階段事件輸入至即時處理引擎。</span><span class="sxs-lookup"><span data-stu-id="e0cae-151">IoT Hub handles hello device-to-cloud communication, and Event Hubs handles later-stage event ingress into real-time processing engines.</span></span>

### <a name="next-steps"></a><span data-ttu-id="e0cae-152">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e0cae-152">Next steps</span></span>
<span data-ttu-id="e0cae-153">toolearn 進一步了解規劃您的 IoT 中樞的部署，請參閱[調整、 高可用性及用為 DR][lnk-scaling]。</span><span class="sxs-lookup"><span data-stu-id="e0cae-153">toolearn more about planning your IoT Hub deployment, see [Scaling, HA, and DR][lnk-scaling].</span></span>

<span data-ttu-id="e0cae-154">toofurther 瀏覽的 IoT 中樞的 hello 功能，請參閱：</span><span class="sxs-lookup"><span data-stu-id="e0cae-154">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="e0cae-155">[IoT 中樞開發人員指南][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="e0cae-155">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="e0cae-156">[使用 IoT Edge 來模擬裝置][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="e0cae-156">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>

[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md

[Azure Event Hubs]: ../event-hubs/event-hubs-what-is-event-hubs.md
[安全性 &gt; 一節的 hello IoT 中樞開發人員指南]: iot-hub-devguide-security.md
[Event Hubs - security]: ../event-hubs/event-hubs-authentication-and-security-model-overview.md
[Event Hubs publisher policies]: ../event-hubs/event-hubs-features.md#event-publishers
[Azure Event Hubs quotas]: ../event-hubs/event-hubs-quotas.md
[Azure IoT SDKs]: https://github.com/Azure/azure-iot-sdks
[lnk-azure-protocol-gateway]: iot-hub-protocol-gateway.md

[lnk-scaling]: iot-hub-scaling.md
[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
[lnk-devguide-messaging]: iot-hub-devguide-messaging.md
