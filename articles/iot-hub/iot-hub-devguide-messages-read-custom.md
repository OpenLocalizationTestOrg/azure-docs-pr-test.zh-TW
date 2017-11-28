---
title: "了解 Azure IoT 中樞自訂端點 | Microsoft Docs"
description: "開發人員指南 - 使用路由規則將裝置對雲端訊息路由傳送至自訂端點。"
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
ms.openlocfilehash: a21f1c61f344f96e2e03422e41fd8c5f7f841a0c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-message-routes-and-custom-endpoints-for-device-to-cloud-messages"></a><span data-ttu-id="05209-103">針對裝置對雲端訊息使用訊息路由和自訂端點</span><span class="sxs-lookup"><span data-stu-id="05209-103">Use message routes and custom endpoints for device-to-cloud messages</span></span>

<span data-ttu-id="05209-104">IoT 中樞可讓您根據訊息屬性，將[裝置對雲端訊息][lnk-device-to-cloud]路由傳送至 IoT 中樞服務面向端點。</span><span class="sxs-lookup"><span data-stu-id="05209-104">IoT Hub enables you to route [device-to-cloud messages][lnk-device-to-cloud] to IoT Hub service-facing endpoints based on message properties.</span></span> <span data-ttu-id="05209-105">路由規則提供您傳送訊息目的地的彈性，而不需要其他服務來處理訊息或撰寫額外程式碼。</span><span class="sxs-lookup"><span data-stu-id="05209-105">Routing rules give you the flexibility to send messages where they need to go without the need for additional services to process messages or to write additional code.</span></span> <span data-ttu-id="05209-106">您設定的每個路由規則都具有下列屬性：</span><span class="sxs-lookup"><span data-stu-id="05209-106">Each routing rule you configure has the following properties:</span></span>

| <span data-ttu-id="05209-107">屬性</span><span class="sxs-lookup"><span data-stu-id="05209-107">Property</span></span>      | <span data-ttu-id="05209-108">說明</span><span class="sxs-lookup"><span data-stu-id="05209-108">Description</span></span> |
| ------------- | ----------- |
| <span data-ttu-id="05209-109">**名稱**</span><span class="sxs-lookup"><span data-stu-id="05209-109">**Name**</span></span>      | <span data-ttu-id="05209-110">可識別規則的唯一名稱。</span><span class="sxs-lookup"><span data-stu-id="05209-110">The unique name that identifies the rule.</span></span> |
| <span data-ttu-id="05209-111">**來源**</span><span class="sxs-lookup"><span data-stu-id="05209-111">**Source**</span></span>    | <span data-ttu-id="05209-112">要據以處理的資料串流來源。</span><span class="sxs-lookup"><span data-stu-id="05209-112">The origin of the data stream to be acted upon.</span></span> <span data-ttu-id="05209-113">例如裝置遙測。</span><span class="sxs-lookup"><span data-stu-id="05209-113">For example, device telemetry.</span></span> |
| <span data-ttu-id="05209-114">**Condition**</span><span class="sxs-lookup"><span data-stu-id="05209-114">**Condition**</span></span> | <span data-ttu-id="05209-115">針對訊息標頭和內文執行的路由規則查詢運算式，用來判斷它是否符合端點。</span><span class="sxs-lookup"><span data-stu-id="05209-115">The query expression for the routing rule that is run against the message's headers and body and used to determine whether it is a match for the endpoint.</span></span> <span data-ttu-id="05209-116">如需建構路由條件的詳細資訊，請參閱[參考 - 裝置對應項和作業的查詢語言][lnk-devguide-query-language]。</span><span class="sxs-lookup"><span data-stu-id="05209-116">For more information about constructing a route condition, see the [Reference - query language for device twins and jobs][lnk-devguide-query-language].</span></span> |
| <span data-ttu-id="05209-117">**端點**</span><span class="sxs-lookup"><span data-stu-id="05209-117">**Endpoint**</span></span>  | <span data-ttu-id="05209-118">IoT 中樞傳送符合條件之訊息的目的地端點名稱。</span><span class="sxs-lookup"><span data-stu-id="05209-118">The name of the endpoint where IoT Hub sends messages that match the condition.</span></span> <span data-ttu-id="05209-119">端點應該與 IoT 中樞位於相同區域，否則您可能需要支付跨區域寫入費用。</span><span class="sxs-lookup"><span data-stu-id="05209-119">Endpoints should be in the same region as the IoT hub, otherwise you may be charged for cross-region writes.</span></span> |

<span data-ttu-id="05209-120">單一訊息可能符合多個路由規則的條件，在這種情況下 IoT 中樞會將訊息傳遞至與每個符合的規則相關聯的端點。</span><span class="sxs-lookup"><span data-stu-id="05209-120">A single message may match the condition on multiple routing rules, in which case IoT Hub delivers the message to the endpoint associated with each matched rule.</span></span> <span data-ttu-id="05209-121">IoT 中樞也會自動刪除重複的訊息傳遞，如此若有訊息符合多個規則並且都有相同的目的地，則訊息僅會寫入到該目的地一次。</span><span class="sxs-lookup"><span data-stu-id="05209-121">IoT Hub also automatically deduplicates message delivery, so if a message matches multiple rules that all have the same destination, it is only written to that destination once.</span></span>

<span data-ttu-id="05209-122">IoT 中樞具有預設[內建端點][lnk-built-in]。</span><span class="sxs-lookup"><span data-stu-id="05209-122">An IoT hub has a default [built-in endpoint][lnk-built-in].</span></span> <span data-ttu-id="05209-123">您可以將訂用帳戶中的其他服務連結到中樞，來建立要路由傳送訊息的目標自訂端點。</span><span class="sxs-lookup"><span data-stu-id="05209-123">You can create custom endpoints to route messages to by linking other services in your subscription to the hub.</span></span> <span data-ttu-id="05209-124">IoT 中樞目前支援事件中樞、服務匯流排佇列，及服務匯流排主題做為自訂端點。</span><span class="sxs-lookup"><span data-stu-id="05209-124">IoT Hub currently supports Event Hubs, Service Bus queues, and Service Bus topics as custom endpoints.</span></span>

> [!WARNING]
> <span data-ttu-id="05209-125">不支援將啟用 [工作階段] 或 [重複偵測] 的服務匯流排佇列和主題作為自訂端點。</span><span class="sxs-lookup"><span data-stu-id="05209-125">Service Bus queues and topics with **Sessions** or **Duplicate Detection** enabled are not supported as custom endpoints.</span></span>

<span data-ttu-id="05209-126">如需在 IoT 中樞建立自訂端點的詳細資訊，請參閱 [IoT 中樞端點][lnk-devguide-endpoints]。</span><span class="sxs-lookup"><span data-stu-id="05209-126">For more information about creating custom endpoints in IoT Hub, see [IoT Hub endpoints][lnk-devguide-endpoints].</span></span>

<span data-ttu-id="05209-127">如需從自訂端點讀取的詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="05209-127">For more information about reading from custom endpoints, see:</span></span>

* <span data-ttu-id="05209-128">從[事件中樞][lnk-getstarted-eh]讀取。</span><span class="sxs-lookup"><span data-stu-id="05209-128">Reading from [Event Hubs][lnk-getstarted-eh].</span></span>
* <span data-ttu-id="05209-129">從[服務匯流排佇列][lnk-getstarted-queue]讀取。</span><span class="sxs-lookup"><span data-stu-id="05209-129">Reading from [Service Bus queues][lnk-getstarted-queue].</span></span>
* <span data-ttu-id="05209-130">從[服務匯流排主題][lnk-getstarted-topic]讀取。</span><span class="sxs-lookup"><span data-stu-id="05209-130">Reading from [Service Bus topics][lnk-getstarted-topic].</span></span>

### <a name="next-steps"></a><span data-ttu-id="05209-131">後續步驟</span><span class="sxs-lookup"><span data-stu-id="05209-131">Next steps</span></span>

<span data-ttu-id="05209-132">如需 IoT 中樞端點的詳細資訊，請參閱 [IoT 中樞端點][lnk-devguide-endpoints]。</span><span class="sxs-lookup"><span data-stu-id="05209-132">For more information about IoT Hub endpoints, see [IoT Hub endpoints][lnk-devguide-endpoints].</span></span>

<span data-ttu-id="05209-133">如需您用來定義路由規則之查詢語言的詳細資訊，請參閱[裝置對應項、作業和訊息路由的 IoT 中樞查詢語言][lnk-devguide-query-language]。</span><span class="sxs-lookup"><span data-stu-id="05209-133">For more information about the query language you use to define routing rules, see [IoT Hub query language for device twins, jobs, and message routing][lnk-devguide-query-language].</span></span>

<span data-ttu-id="05209-134">[使用路由處理 IoT 中樞的裝置對雲端訊息][lnk-d2c-tutorial] 教學課程示範如何使用路由規則和自訂端點。</span><span class="sxs-lookup"><span data-stu-id="05209-134">The [Process IoT Hub device-to-cloud messages using routes][lnk-d2c-tutorial] tutorial shows you how to use routing rules and custom endpoints.</span></span>

[lnk-built-in]: iot-hub-devguide-messages-read-builtin.md
[lnk-device-to-cloud]: iot-hub-devguide-messages-d2c.md
[lnk-devguide-query-language]: iot-hub-devguide-query-language.md
[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
[lnk-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md
[lnk-getstarted-eh]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-getstarted-queue]: ../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md
[lnk-getstarted-topic]: ../service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions.md
