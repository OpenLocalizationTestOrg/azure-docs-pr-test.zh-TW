---
title: "aaaUnderstand Azure IoT 中樞自訂端點 |Microsoft 文件"
description: "開發人員指南-使用 路由規則 tooroute 裝置到雲端訊息 toocustom 端點。"
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
ms.openlocfilehash: daa9cfb35d0853e316bbf469b034d4dadbd4e85d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-message-routes-and-custom-endpoints-for-device-to-cloud-messages"></a><span data-ttu-id="7075b-103">針對裝置對雲端訊息使用訊息路由和自訂端點</span><span class="sxs-lookup"><span data-stu-id="7075b-103">Use message routes and custom endpoints for device-to-cloud messages</span></span>

<span data-ttu-id="7075b-104">IoT 中樞可讓您 tooroute[裝置到雲端訊息][ lnk-device-to-cloud] tooIoT 中樞服務向端點根據訊息屬性。</span><span class="sxs-lookup"><span data-stu-id="7075b-104">IoT Hub enables you tooroute [device-to-cloud messages][lnk-device-to-cloud] tooIoT Hub service-facing endpoints based on message properties.</span></span> <span data-ttu-id="7075b-105">路由規則提供 hello 彈性 toosend 訊息需要 toogo hello 不需要其他服務 tooprocess 訊息或 toowrite 額外的程式碼。</span><span class="sxs-lookup"><span data-stu-id="7075b-105">Routing rules give you hello flexibility toosend messages where they need toogo without hello need for additional services tooprocess messages or toowrite additional code.</span></span> <span data-ttu-id="7075b-106">您設定每個路由規則具有下列屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="7075b-106">Each routing rule you configure has hello following properties:</span></span>

| <span data-ttu-id="7075b-107">屬性</span><span class="sxs-lookup"><span data-stu-id="7075b-107">Property</span></span>      | <span data-ttu-id="7075b-108">說明</span><span class="sxs-lookup"><span data-stu-id="7075b-108">Description</span></span> |
| ------------- | ----------- |
| <span data-ttu-id="7075b-109">**名稱**</span><span class="sxs-lookup"><span data-stu-id="7075b-109">**Name**</span></span>      | <span data-ttu-id="7075b-110">hello 唯一識別名稱 hello 規則。</span><span class="sxs-lookup"><span data-stu-id="7075b-110">hello unique name that identifies hello rule.</span></span> |
| <span data-ttu-id="7075b-111">**來源**</span><span class="sxs-lookup"><span data-stu-id="7075b-111">**Source**</span></span>    | <span data-ttu-id="7075b-112">hello hello 資料來源資料流 toobe 作用時。</span><span class="sxs-lookup"><span data-stu-id="7075b-112">hello origin of hello data stream toobe acted upon.</span></span> <span data-ttu-id="7075b-113">例如裝置遙測。</span><span class="sxs-lookup"><span data-stu-id="7075b-113">For example, device telemetry.</span></span> |
| <span data-ttu-id="7075b-114">**Condition**</span><span class="sxs-lookup"><span data-stu-id="7075b-114">**Condition**</span></span> | <span data-ttu-id="7075b-115">hello hello 路由規則針對 hello 訊息標頭和主體執行，並使用 toodetermine 是否 hello 端點的相符項目查詢運算式。</span><span class="sxs-lookup"><span data-stu-id="7075b-115">hello query expression for hello routing rule that is run against hello message's headers and body and used toodetermine whether it is a match for hello endpoint.</span></span> <span data-ttu-id="7075b-116">如需有關如何建構路由條件的詳細資訊，請參閱 hello[參考-裝置雙及作業的查詢語言][lnk-devguide-query-language]。</span><span class="sxs-lookup"><span data-stu-id="7075b-116">For more information about constructing a route condition, see hello [Reference - query language for device twins and jobs][lnk-devguide-query-language].</span></span> |
| <span data-ttu-id="7075b-117">**端點**</span><span class="sxs-lookup"><span data-stu-id="7075b-117">**Endpoint**</span></span>  | <span data-ttu-id="7075b-118">hello hello 端點 IoT 中樞讓傳送訊息符合 hello 條件的名稱。</span><span class="sxs-lookup"><span data-stu-id="7075b-118">hello name of hello endpoint where IoT Hub sends messages that match hello condition.</span></span> <span data-ttu-id="7075b-119">端點應該位於 hello hello IoT 中樞與相同的區域，否則您可能需要支付費用的跨地區寫入。</span><span class="sxs-lookup"><span data-stu-id="7075b-119">Endpoints should be in hello same region as hello IoT hub, otherwise you may be charged for cross-region writes.</span></span> |

<span data-ttu-id="7075b-120">在多個路由規則、 大小寫 IoT 中樞將傳遞每個相符的規則相關聯的 hello 訊息 toohello 端點上 hello 狀況時，可能會比單一訊息。</span><span class="sxs-lookup"><span data-stu-id="7075b-120">A single message may match hello condition on multiple routing rules, in which case IoT Hub delivers hello message toohello endpoint associated with each matched rule.</span></span> <span data-ttu-id="7075b-121">IoT 中樞也會自動 deduplicates 訊息傳遞，因此如果訊息符合多個規則都有 hello 相同的目的地，它僅寫入 toothat 目的地一次。</span><span class="sxs-lookup"><span data-stu-id="7075b-121">IoT Hub also automatically deduplicates message delivery, so if a message matches multiple rules that all have hello same destination, it is only written toothat destination once.</span></span>

<span data-ttu-id="7075b-122">IoT 中樞具有預設[內建端點][lnk-built-in]。</span><span class="sxs-lookup"><span data-stu-id="7075b-122">An IoT hub has a default [built-in endpoint][lnk-built-in].</span></span> <span data-ttu-id="7075b-123">您可以建立自訂端點 tooroute 訊息 tooby 連結您的訂用帳戶 toohello 中樞中的其他服務。</span><span class="sxs-lookup"><span data-stu-id="7075b-123">You can create custom endpoints tooroute messages tooby linking other services in your subscription toohello hub.</span></span> <span data-ttu-id="7075b-124">IoT 中樞目前支援事件中樞、服務匯流排佇列，及服務匯流排主題做為自訂端點。</span><span class="sxs-lookup"><span data-stu-id="7075b-124">IoT Hub currently supports Event Hubs, Service Bus queues, and Service Bus topics as custom endpoints.</span></span>

> [!WARNING]
> <span data-ttu-id="7075b-125">不支援將啟用 [工作階段] 或 [重複偵測] 的服務匯流排佇列和主題作為自訂端點。</span><span class="sxs-lookup"><span data-stu-id="7075b-125">Service Bus queues and topics with **Sessions** or **Duplicate Detection** enabled are not supported as custom endpoints.</span></span>

<span data-ttu-id="7075b-126">如需在 IoT 中樞建立自訂端點的詳細資訊，請參閱 [IoT 中樞端點][lnk-devguide-endpoints]。</span><span class="sxs-lookup"><span data-stu-id="7075b-126">For more information about creating custom endpoints in IoT Hub, see [IoT Hub endpoints][lnk-devguide-endpoints].</span></span>

<span data-ttu-id="7075b-127">如需從自訂端點讀取的詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="7075b-127">For more information about reading from custom endpoints, see:</span></span>

* <span data-ttu-id="7075b-128">從[事件中樞][lnk-getstarted-eh]讀取。</span><span class="sxs-lookup"><span data-stu-id="7075b-128">Reading from [Event Hubs][lnk-getstarted-eh].</span></span>
* <span data-ttu-id="7075b-129">從[服務匯流排佇列][lnk-getstarted-queue]讀取。</span><span class="sxs-lookup"><span data-stu-id="7075b-129">Reading from [Service Bus queues][lnk-getstarted-queue].</span></span>
* <span data-ttu-id="7075b-130">從[服務匯流排主題][lnk-getstarted-topic]讀取。</span><span class="sxs-lookup"><span data-stu-id="7075b-130">Reading from [Service Bus topics][lnk-getstarted-topic].</span></span>

### <a name="next-steps"></a><span data-ttu-id="7075b-131">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7075b-131">Next steps</span></span>

<span data-ttu-id="7075b-132">如需 IoT 中樞端點的詳細資訊，請參閱 [IoT 中樞端點][lnk-devguide-endpoints]。</span><span class="sxs-lookup"><span data-stu-id="7075b-132">For more information about IoT Hub endpoints, see [IoT Hub endpoints][lnk-devguide-endpoints].</span></span>

<span data-ttu-id="7075b-133">如需有關 hello 查詢語言使用 toodefine 路由規則，請參閱[裝置雙、 作業和訊息路由的 IoT 中樞查詢語言][lnk-devguide-query-language]。</span><span class="sxs-lookup"><span data-stu-id="7075b-133">For more information about hello query language you use toodefine routing rules, see [IoT Hub query language for device twins, jobs, and message routing][lnk-devguide-query-language].</span></span>

<span data-ttu-id="7075b-134">hello[使用路由的處理序 IoT 中樞裝置到雲端訊息][ lnk-d2c-tutorial]教學課程示範如何 toouse 路由規則，並自訂端點。</span><span class="sxs-lookup"><span data-stu-id="7075b-134">hello [Process IoT Hub device-to-cloud messages using routes][lnk-d2c-tutorial] tutorial shows you how toouse routing rules and custom endpoints.</span></span>

[lnk-built-in]: iot-hub-devguide-messages-read-builtin.md
[lnk-device-to-cloud]: iot-hub-devguide-messages-d2c.md
[lnk-devguide-query-language]: iot-hub-devguide-query-language.md
[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
[lnk-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md
[lnk-getstarted-eh]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-getstarted-queue]: ../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md
[lnk-getstarted-topic]: ../service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions.md
