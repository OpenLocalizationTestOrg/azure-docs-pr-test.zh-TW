---
title: "了解 Azure IoT 中樞的雲端到裝置傳訊 | Microsoft Docs"
description: "開發人員指南 - 如何使用 IoT 中樞的雲端到裝置傳訊。 包含訊息生命週期和設定選項的相關資訊。"
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
ms.openlocfilehash: 04ac46498c912b0503036f70b7f3d0e28e5a82b8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="send-cloud-to-device-messages-from-iot-hub"></a><span data-ttu-id="b64ca-104">從 IoT 中樞傳送雲端到裝置訊息</span><span class="sxs-lookup"><span data-stu-id="b64ca-104">Send cloud-to-device messages from IoT Hub</span></span>

<span data-ttu-id="b64ca-105">若要從您的解決方案後端傳送單向通知到裝置應用程式，請從您的 IoT 中樞傳送雲端對裝置訊息到您的裝置。</span><span class="sxs-lookup"><span data-stu-id="b64ca-105">To send one-way notifications to the device app from your solution back end, send cloud-to-devices messages from your IoT hub to your device.</span></span> <span data-ttu-id="b64ca-106">如需 IoT 中樞所支援之其他雲端到裝置選項的討論，請參閱[雲端對裝置通訊指引][lnk-c2d-guidance]。</span><span class="sxs-lookup"><span data-stu-id="b64ca-106">For a discussion of other cloud-to-devices options supported by IoT Hub, see [Cloud-to-device communications guidance][lnk-c2d-guidance].</span></span>

<span data-ttu-id="b64ca-107">您可以透過面向服務的端點 (**/messages/devicebound**) 來傳送雲端到裝置訊息。</span><span class="sxs-lookup"><span data-stu-id="b64ca-107">You send cloud-to-device messages through a service-facing endpoint (**/messages/devicebound**).</span></span> <span data-ttu-id="b64ca-108">裝置接著會透過裝置專用的端點 (**/devices/{deviceId}/messages/devicebound**) 來接收訊息。</span><span class="sxs-lookup"><span data-stu-id="b64ca-108">A device then receives the messages through a device-specific endpoint (**/devices/{deviceId}/messages/devicebound**).</span></span>

<span data-ttu-id="b64ca-109">每個雲端到裝置訊息都是以單一裝置為目標，其中會將 **to** 屬性設定為 **/devices/{deviceId}/messages/devicebound**。</span><span class="sxs-lookup"><span data-stu-id="b64ca-109">Each cloud-to-device message is targeted at a single device by setting the **to** property to **/devices/{deviceId}/messages/devicebound**.</span></span>

<span data-ttu-id="b64ca-110">每個裝置佇列最多保留 50 則雲端到裝置訊息。</span><span class="sxs-lookup"><span data-stu-id="b64ca-110">Each device queue holds at most 50 cloud-to-device messages.</span></span> <span data-ttu-id="b64ca-111">嘗試將更多訊息傳送到相同的裝置會導致錯誤。</span><span class="sxs-lookup"><span data-stu-id="b64ca-111">Trying to send more messages to the same device results in an error.</span></span>

## <a name="the-cloud-to-device-message-lifecycle"></a><span data-ttu-id="b64ca-112">雲端到裝置訊息生命週期</span><span class="sxs-lookup"><span data-stu-id="b64ca-112">The cloud-to-device message lifecycle</span></span>

<span data-ttu-id="b64ca-113">為了保證至少一次訊息傳遞，IoT 中樞會在每個裝置佇列保留雲端到裝置訊息。</span><span class="sxs-lookup"><span data-stu-id="b64ca-113">To guarantee at-least-once message delivery, IoT Hub persists cloud-to-device messages in per-device queues.</span></span> <span data-ttu-id="b64ca-114">裝置必須明確地認可「完成」  ，如此一來，IoT 中樞便能從佇列中移除它們。</span><span class="sxs-lookup"><span data-stu-id="b64ca-114">Devices must explicitly acknowledge *completion* for IoT Hub to remove them from the queue.</span></span> <span data-ttu-id="b64ca-115">此方法保證連線失敗和裝置故障能夠恢復。</span><span class="sxs-lookup"><span data-stu-id="b64ca-115">This approach guarantees resiliency against connectivity and device failures.</span></span>

<span data-ttu-id="b64ca-116">下圖顯示 IoT 中樞之雲端到裝置訊息的生命週期狀態圖。</span><span class="sxs-lookup"><span data-stu-id="b64ca-116">The following diagram shows the lifecycle state graph for a cloud-to-device message in IoT Hub.</span></span>

![雲端到裝置的訊息生命週期][img-lifecycle]

<span data-ttu-id="b64ca-118">當 IoT 中樞服務傳送訊息至裝置時，該服務會將訊息狀態設定為 [已加入佇列]。</span><span class="sxs-lookup"><span data-stu-id="b64ca-118">When the IoT Hub service sends a message to a device, the service sets the message state to **Enqueued**.</span></span> <span data-ttu-id="b64ca-119">當裝置想要「接收」訊息時，IoT 中樞會「鎖定」該訊息 (藉由將狀態設為 [不可見])，以便讓裝置上的其他執行緒開始接收其他訊息。</span><span class="sxs-lookup"><span data-stu-id="b64ca-119">When a device wants to *receive* a message, IoT Hub *locks* the message (by setting the state to **Invisible**), which allows other threads on the device to start receiving other messages.</span></span> <span data-ttu-id="b64ca-120">當裝置執行緒完成處理訊息時，它會藉由「完成」  訊息來通知 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="b64ca-120">When a device thread completes the processing of a message, it notifies IoT Hub by *completing* the message.</span></span> <span data-ttu-id="b64ca-121">IoT 中樞接著會將狀態設定為 [已完成]。</span><span class="sxs-lookup"><span data-stu-id="b64ca-121">IoT Hub then sets the state to **Completed**.</span></span>

<span data-ttu-id="b64ca-122">裝置也可以選擇：</span><span class="sxs-lookup"><span data-stu-id="b64ca-122">A device can also choose to:</span></span>

* <span data-ttu-id="b64ca-123">*拒絕*訊息，這會導致 IoT 中樞將它設定為 **寄不出**狀態。</span><span class="sxs-lookup"><span data-stu-id="b64ca-123">*Reject* the message, which causes IoT Hub to set it to the **Deadlettered** state.</span></span> <span data-ttu-id="b64ca-124">透過 MQTT 通訊協定連線的裝置無法拒絕雲端到裝置訊息。</span><span class="sxs-lookup"><span data-stu-id="b64ca-124">Devices that connect over the MQTT protocol cannot reject cloud-to-device messages.</span></span>
* <span data-ttu-id="b64ca-125">*放棄*訊息，這會導致 IoT 中樞將訊息放回佇列，並將狀態設定為**已排入佇列**。</span><span class="sxs-lookup"><span data-stu-id="b64ca-125">*Abandon* the message, which causes IoT Hub to put the message back in the queue, with the state set to **Enqueued**.</span></span>

<span data-ttu-id="b64ca-126">執行緒可能無法處理訊息，且不會通知 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="b64ca-126">A thread could fail to process a message without notifying IoT Hub.</span></span> <span data-ttu-id="b64ca-127">在此情況下，訊息會在過了 [可見性 (或鎖定) 逾時] 之後，自動從**不可見**狀態轉換回**已加入佇列**狀態。</span><span class="sxs-lookup"><span data-stu-id="b64ca-127">In this case, messages automatically transition from the **Invisible** state back to the **Enqueued** state after a *visibility (or lock) timeout*.</span></span> <span data-ttu-id="b64ca-128">此逾時的預設值是一分鐘。</span><span class="sxs-lookup"><span data-stu-id="b64ca-128">The default value of this timeout is one minute.</span></span>

<span data-ttu-id="b64ca-129">訊息可以在**已加入佇列**與**不可見**狀態之間轉換的次數，以 IoT 中樞上**最大傳遞計數**屬性中指定的次數為限。</span><span class="sxs-lookup"><span data-stu-id="b64ca-129">A message can transition between the **Enqueued** and **Invisible** states for, at most, the number of times specified in the **max delivery count** property on IoT Hub.</span></span> <span data-ttu-id="b64ca-130">達到該轉換次數之後，IoT 中樞就會將訊息的狀態設定為 **寄不出**。</span><span class="sxs-lookup"><span data-stu-id="b64ca-130">After that number of transitions, IoT Hub sets the state of the message to **Deadlettered**.</span></span> <span data-ttu-id="b64ca-131">同樣地，IoT 中樞也會在訊息的到期時間過後 (請參閱[存留時間][lnk-ttl])，將訊息的狀態設定為**寄不出**。</span><span class="sxs-lookup"><span data-stu-id="b64ca-131">Similarly, IoT Hub sets the state of a message to **Deadlettered** after its expiration time (see [Time to live][lnk-ttl]).</span></span>

<span data-ttu-id="b64ca-132">[如何使用 IoT 中樞傳送雲端到裝置訊息][lnk-c2d-tutorial]示範如何從雲端傳送雲端到裝置訊息，並在裝置上接收訊息。</span><span class="sxs-lookup"><span data-stu-id="b64ca-132">The [How to send cloud-to-device messages with IoT Hub][lnk-c2d-tutorial] shows you how to send cloud-to-device messages from the cloud and receive them on a device.</span></span>

<span data-ttu-id="b64ca-133">通常只要遺失訊息不會影響應用程式邏輯，裝置就應該完成雲端到裝置訊息。</span><span class="sxs-lookup"><span data-stu-id="b64ca-133">Typically, a device completes a cloud-to-device message when the loss of the message does not affect the application logic.</span></span> <span data-ttu-id="b64ca-134">例如，當裝置已在本機保存訊息內容，或已成功執行作業時。</span><span class="sxs-lookup"><span data-stu-id="b64ca-134">For example, when the device has persisted the message content locally or has successfully executed an operation.</span></span> <span data-ttu-id="b64ca-135">訊息可能也會攜帶暫時性資訊，遺失該訊息並不會影響應用程式的功能。</span><span class="sxs-lookup"><span data-stu-id="b64ca-135">The message could also carry transient information, whose loss would not impact the functionality of the application.</span></span> <span data-ttu-id="b64ca-136">有時，對於長時間執行的作業，您可以在將作業描述保存於本機儲存體之後，完成雲端到裝置訊息。</span><span class="sxs-lookup"><span data-stu-id="b64ca-136">Sometimes, for long-running tasks, you can complete the cloud-to-device message after persisting the task description in local storage.</span></span> <span data-ttu-id="b64ca-137">接著，您可以在作業進度的各個階段，利用一或多個裝置到雲端訊息來通知解決方案後端。</span><span class="sxs-lookup"><span data-stu-id="b64ca-137">Then you can notify the solution back end with one or more device-to-cloud messages at various stages of progress of the task.</span></span>

## <a name="message-expiration-time-to-live"></a><span data-ttu-id="b64ca-138">訊息到期 (存留時間)</span><span class="sxs-lookup"><span data-stu-id="b64ca-138">Message expiration (time to live)</span></span>

<span data-ttu-id="b64ca-139">每個雲端到裝置的訊息都有到期時間。</span><span class="sxs-lookup"><span data-stu-id="b64ca-139">Every cloud-to-device message has an expiration time.</span></span> <span data-ttu-id="b64ca-140">此時間可以由服務 (在 **ExpiryTimeUtc** 屬性中) 設定，或由 IoT 中樞使用指定為 IoT 中樞屬性的預設「存留時間」來設定。</span><span class="sxs-lookup"><span data-stu-id="b64ca-140">This time is set either by the service (in the **ExpiryTimeUtc** property), or by IoT Hub using the default *time to live* specified as an IoT Hub property.</span></span> <span data-ttu-id="b64ca-141">請參閱[雲端到裝置的設定選項][lnk-c2d-configuration]。</span><span class="sxs-lookup"><span data-stu-id="b64ca-141">See [Cloud-to-device configuration options][lnk-c2d-configuration].</span></span>

<span data-ttu-id="b64ca-142">利用訊息到期和避免將訊息傳送至已中斷連線裝置的常見方法是設定較短的存留時間值。</span><span class="sxs-lookup"><span data-stu-id="b64ca-142">A common way to take advantage of message expiration and avoid sending messages to disconnected devices, is to set short time to live values.</span></span> <span data-ttu-id="b64ca-143">這個做法可達到與維護裝置連線狀態相同的效果，同時更具效率。</span><span class="sxs-lookup"><span data-stu-id="b64ca-143">This approach achieves the same result as maintaining the device connection state, while being more efficient.</span></span> <span data-ttu-id="b64ca-144">當您要求訊息收條時，IoT 中樞會通知您，哪些裝置能夠收到訊息，而哪些裝置不在線上或故障。</span><span class="sxs-lookup"><span data-stu-id="b64ca-144">When you request message acknowledgements, IoT Hub notifies you which devices are able to receive messages, and which devices are not online or have failed.</span></span>

## <a name="message-feedback"></a><span data-ttu-id="b64ca-145">訊息意見反應</span><span class="sxs-lookup"><span data-stu-id="b64ca-145">Message feedback</span></span>

<span data-ttu-id="b64ca-146">當您傳送雲端到裝置的訊息時，服務可以要求傳遞每則訊息的意見反應 (關於該訊息的最終狀態)。</span><span class="sxs-lookup"><span data-stu-id="b64ca-146">When you send a cloud-to-device message, the service can request the delivery of per-message feedback regarding the final state of that message.</span></span>

| <span data-ttu-id="b64ca-147">Ack 屬性</span><span class="sxs-lookup"><span data-stu-id="b64ca-147">Ack property</span></span> | <span data-ttu-id="b64ca-148">行為</span><span class="sxs-lookup"><span data-stu-id="b64ca-148">Behavior</span></span> |
| ------------ | -------- |
| <span data-ttu-id="b64ca-149">**positive**</span><span class="sxs-lookup"><span data-stu-id="b64ca-149">**positive**</span></span> | <span data-ttu-id="b64ca-150">只有在雲端到裝置訊息達到 [已完成] 狀態時，IoT 中樞才會產生意見反應訊息。</span><span class="sxs-lookup"><span data-stu-id="b64ca-150">IoT Hub generates a feedback message if, and only if, the cloud-to-device message reached the **Completed** state.</span></span> |
| <span data-ttu-id="b64ca-151">**negative**</span><span class="sxs-lookup"><span data-stu-id="b64ca-151">**negative**</span></span> | <span data-ttu-id="b64ca-152">只有在雲端到裝置訊息達到 [寄不出] 狀態時，IoT 中樞才會產生意見反應訊息。</span><span class="sxs-lookup"><span data-stu-id="b64ca-152">IoT Hub generates a feedback message, if and only if, the cloud-to-device message reaches the **Deadlettered** state.</span></span> |
| <span data-ttu-id="b64ca-153">**full**</span><span class="sxs-lookup"><span data-stu-id="b64ca-153">**full**</span></span>     | <span data-ttu-id="b64ca-154">IoT 中樞在任一情況下都會產生意見反應訊息。</span><span class="sxs-lookup"><span data-stu-id="b64ca-154">IoT Hub generates a feedback message in either case.</span></span> |

<span data-ttu-id="b64ca-155">如果 **Ack** 是 **full**，而且您沒有收到意見反應訊息，這表示該意見反應訊息已過期。</span><span class="sxs-lookup"><span data-stu-id="b64ca-155">If **Ack** is **full**, and you don't receive a feedback message, it means that the feedback message expired.</span></span> <span data-ttu-id="b64ca-156">服務無法得知原始訊息發生了什麼事。</span><span class="sxs-lookup"><span data-stu-id="b64ca-156">The service can't know what happened to the original message.</span></span> <span data-ttu-id="b64ca-157">實際上，服務應該確保它可以在回饋到期之前對其進行處理。</span><span class="sxs-lookup"><span data-stu-id="b64ca-157">In practice, a service should ensure that it can process the feedback before it expires.</span></span> <span data-ttu-id="b64ca-158">最長到期時間是兩天，在發生失敗時，能夠有相當充裕的時間可讓服務啟動並正常執行。</span><span class="sxs-lookup"><span data-stu-id="b64ca-158">The maximum expiry time is two days, which allows plenty of time to get the service running again if a failure occurs.</span></span>

<span data-ttu-id="b64ca-159">如[端點][lnk-endpoints]中所述，IoT 中樞會透過面向服務的端點 (**/messages/servicebound/feedback**) 利用訊息來傳遞意見反應。</span><span class="sxs-lookup"><span data-stu-id="b64ca-159">As explained in [Endpoints][lnk-endpoints], IoT Hub delivers feedback through a service-facing endpoint (**/messages/servicebound/feedback**) as messages.</span></span> <span data-ttu-id="b64ca-160">接收意見反應的語意與雲端到裝置訊息的接收語意相同，並且具有相同的[訊息生命週期][lnk-lifecycle]。</span><span class="sxs-lookup"><span data-stu-id="b64ca-160">The semantics for receiving feedback are the same as for cloud-to-device messages, and have the same [Message lifecycle][lnk-lifecycle].</span></span> <span data-ttu-id="b64ca-161">可能的話，訊息意見反應會放入單一訊息中，其格式如下：</span><span class="sxs-lookup"><span data-stu-id="b64ca-161">Whenever possible, message feedback is batched in a single message, with the following format:</span></span>

| <span data-ttu-id="b64ca-162">屬性</span><span class="sxs-lookup"><span data-stu-id="b64ca-162">Property</span></span>     | <span data-ttu-id="b64ca-163">說明</span><span class="sxs-lookup"><span data-stu-id="b64ca-163">Description</span></span> |
| ------------ | ----------- |
| <span data-ttu-id="b64ca-164">EnqueuedTime</span><span class="sxs-lookup"><span data-stu-id="b64ca-164">EnqueuedTime</span></span> | <span data-ttu-id="b64ca-165">指出訊息建立時間的時間戳記。</span><span class="sxs-lookup"><span data-stu-id="b64ca-165">Timestamp indicating when the message was created.</span></span> |
| <span data-ttu-id="b64ca-166">UserId</span><span class="sxs-lookup"><span data-stu-id="b64ca-166">UserId</span></span>       | `{iot hub name}` |
| <span data-ttu-id="b64ca-167">ContentType</span><span class="sxs-lookup"><span data-stu-id="b64ca-167">ContentType</span></span>  | `application/vnd.microsoft.iothub.feedback.json` |

<span data-ttu-id="b64ca-168">主體是記錄的 JSON 序列化陣列，而每筆記錄都具有下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="b64ca-168">The body is a JSON-serialized array of records, each with the following properties:</span></span>

| <span data-ttu-id="b64ca-169">屬性</span><span class="sxs-lookup"><span data-stu-id="b64ca-169">Property</span></span>           | <span data-ttu-id="b64ca-170">說明</span><span class="sxs-lookup"><span data-stu-id="b64ca-170">Description</span></span> |
| ------------------ | ----------- |
| <span data-ttu-id="b64ca-171">EnqueuedTimeUtc</span><span class="sxs-lookup"><span data-stu-id="b64ca-171">EnqueuedTimeUtc</span></span>    | <span data-ttu-id="b64ca-172">指出訊息的結果出現時的時間戳記。</span><span class="sxs-lookup"><span data-stu-id="b64ca-172">Timestamp indicating when the outcome of the message happened.</span></span> <span data-ttu-id="b64ca-173">例如，完成已裝置或訊息已到期。</span><span class="sxs-lookup"><span data-stu-id="b64ca-173">For example, the device completed or the message expired.</span></span> |
| <span data-ttu-id="b64ca-174">OriginalMessageId</span><span class="sxs-lookup"><span data-stu-id="b64ca-174">OriginalMessageId</span></span>  | <span data-ttu-id="b64ca-175">此意見反應資訊相關之雲端到裝置訊息的 **MessageId**。</span><span class="sxs-lookup"><span data-stu-id="b64ca-175">**MessageId** of the cloud-to-device message to which this feedback information relates.</span></span> |
| <span data-ttu-id="b64ca-176">StatusCode</span><span class="sxs-lookup"><span data-stu-id="b64ca-176">StatusCode</span></span>         | <span data-ttu-id="b64ca-177">必要字串。</span><span class="sxs-lookup"><span data-stu-id="b64ca-177">Required string.</span></span> <span data-ttu-id="b64ca-178">用於 IoT 中樞所產生的回饋訊息中。</span><span class="sxs-lookup"><span data-stu-id="b64ca-178">Used in feedback messages generated by IoT Hub.</span></span> <br/> <span data-ttu-id="b64ca-179">「成功」</span><span class="sxs-lookup"><span data-stu-id="b64ca-179">'Success'</span></span> <br/> <span data-ttu-id="b64ca-180">「已過期」</span><span class="sxs-lookup"><span data-stu-id="b64ca-180">'Expired'</span></span> <br/> <span data-ttu-id="b64ca-181">「DeliveryCountExceeded」</span><span class="sxs-lookup"><span data-stu-id="b64ca-181">'DeliveryCountExceeded'</span></span> <br/> <span data-ttu-id="b64ca-182">「已拒絕」</span><span class="sxs-lookup"><span data-stu-id="b64ca-182">'Rejected'</span></span> <br/> <span data-ttu-id="b64ca-183">「已清除」</span><span class="sxs-lookup"><span data-stu-id="b64ca-183">'Purged'</span></span> |
| <span data-ttu-id="b64ca-184">描述</span><span class="sxs-lookup"><span data-stu-id="b64ca-184">Description</span></span>        | <span data-ttu-id="b64ca-185">**StatusCode**的字串值。</span><span class="sxs-lookup"><span data-stu-id="b64ca-185">String values for **StatusCode**.</span></span> |
| <span data-ttu-id="b64ca-186">deviceId</span><span class="sxs-lookup"><span data-stu-id="b64ca-186">DeviceId</span></span>           | <span data-ttu-id="b64ca-187">此意見反應資訊相關之雲端到裝置訊息的目標裝置 **DeviceId**。</span><span class="sxs-lookup"><span data-stu-id="b64ca-187">**DeviceId** of the target device of the cloud-to-device message to which this piece of feedback relates.</span></span> |
| <span data-ttu-id="b64ca-188">DeviceGenerationId</span><span class="sxs-lookup"><span data-stu-id="b64ca-188">DeviceGenerationId</span></span> | <span data-ttu-id="b64ca-189">此意見反應資訊相關之雲端到裝置訊息的目標裝置 **DeviceGenerationId**。</span><span class="sxs-lookup"><span data-stu-id="b64ca-189">**DeviceGenerationId** of the target device of the cloud-to-device message to which this piece of feedback relates.</span></span> |

<span data-ttu-id="b64ca-190">服務必須指定雲端到裝置訊息的 **MessageId** ，才能使其意見反應與原始訊息相互關聯。</span><span class="sxs-lookup"><span data-stu-id="b64ca-190">The service must specify a **MessageId** for the cloud-to-device message to be able to correlate its feedback with the original message.</span></span>

<span data-ttu-id="b64ca-191">下列範例顯示意見反應訊息的本文。</span><span class="sxs-lookup"><span data-stu-id="b64ca-191">The following example shows the body of a feedback message.</span></span>

```json
[
  {
    "OriginalMessageId": "0987654321",
    "EnqueuedTimeUtc": "2015-07-28T16:24:48.789Z",
    "StatusCode": 0,
    "Description": "Success",
    "DeviceId": "123",
    "DeviceGenerationId": "abcdefghijklmnopqrstuvwxyz"
  },
  {
    ...
  },
  ...
]
```

## <a name="cloud-to-device-configuration-options"></a><span data-ttu-id="b64ca-192">雲端到裝置組態選項</span><span class="sxs-lookup"><span data-stu-id="b64ca-192">Cloud-to-device configuration options</span></span>

<span data-ttu-id="b64ca-193">每個 IoT 中樞都會針對雲端到裝置傳訊公開下列設定選項：</span><span class="sxs-lookup"><span data-stu-id="b64ca-193">Each IoT hub exposes the following configuration options for cloud-to-device messaging:</span></span>

| <span data-ttu-id="b64ca-194">屬性</span><span class="sxs-lookup"><span data-stu-id="b64ca-194">Property</span></span>                  | <span data-ttu-id="b64ca-195">說明</span><span class="sxs-lookup"><span data-stu-id="b64ca-195">Description</span></span> | <span data-ttu-id="b64ca-196">範圍和預設值</span><span class="sxs-lookup"><span data-stu-id="b64ca-196">Range and default</span></span> |
| ------------------------- | ----------- | ----------------- |
| <span data-ttu-id="b64ca-197">defaultTtlAsIso8601</span><span class="sxs-lookup"><span data-stu-id="b64ca-197">defaultTtlAsIso8601</span></span>       | <span data-ttu-id="b64ca-198">雲端到裝置訊息的預設 TTL。</span><span class="sxs-lookup"><span data-stu-id="b64ca-198">Default TTL for cloud-to-device messages.</span></span> | <span data-ttu-id="b64ca-199">ISO_8601 間隔高達 2D (最小為 1 分鐘)。</span><span class="sxs-lookup"><span data-stu-id="b64ca-199">ISO_8601 interval up to 2D (minimum 1 minute).</span></span> <span data-ttu-id="b64ca-200">預設值︰1 小時。</span><span class="sxs-lookup"><span data-stu-id="b64ca-200">Default: 1 hour.</span></span> |
| <span data-ttu-id="b64ca-201">maxDeliveryCount</span><span class="sxs-lookup"><span data-stu-id="b64ca-201">maxDeliveryCount</span></span>          | <span data-ttu-id="b64ca-202">每個裝置佇列的雲端到裝置最大傳遞計數。</span><span class="sxs-lookup"><span data-stu-id="b64ca-202">Maximum delivery count for cloud-to-device per-device queues.</span></span> | <span data-ttu-id="b64ca-203">1 到 100。</span><span class="sxs-lookup"><span data-stu-id="b64ca-203">1 to 100.</span></span> <span data-ttu-id="b64ca-204">預設值：10</span><span class="sxs-lookup"><span data-stu-id="b64ca-204">Default: 10.</span></span> |
| <span data-ttu-id="b64ca-205">feedback.ttlAsIso8601</span><span class="sxs-lookup"><span data-stu-id="b64ca-205">feedback.ttlAsIso8601</span></span>     | <span data-ttu-id="b64ca-206">保留服務繫結的意見反應訊息。</span><span class="sxs-lookup"><span data-stu-id="b64ca-206">Retention for service-bound feedback messages.</span></span> | <span data-ttu-id="b64ca-207">ISO_8601 間隔高達 2D (最小為 1 分鐘)。</span><span class="sxs-lookup"><span data-stu-id="b64ca-207">ISO_8601 interval up to 2D (minimum 1 minute).</span></span> <span data-ttu-id="b64ca-208">預設值︰1 小時。</span><span class="sxs-lookup"><span data-stu-id="b64ca-208">Default: 1 hour.</span></span> |
| <span data-ttu-id="b64ca-209">feedback.maxDeliveryCount</span><span class="sxs-lookup"><span data-stu-id="b64ca-209">feedback.maxDeliveryCount</span></span> |<span data-ttu-id="b64ca-210">意見反應佇列的最大傳遞計數。</span><span class="sxs-lookup"><span data-stu-id="b64ca-210">Maximum delivery count for feedback queue.</span></span> | <span data-ttu-id="b64ca-211">1 到 100。</span><span class="sxs-lookup"><span data-stu-id="b64ca-211">1 to 100.</span></span> <span data-ttu-id="b64ca-212">預設值 = 100。</span><span class="sxs-lookup"><span data-stu-id="b64ca-212">Default: 100.</span></span> |

<span data-ttu-id="b64ca-213">如需如何設定這些設定選項的詳細資訊，請參閱[建立 IoT 中樞][lnk-portal]。</span><span class="sxs-lookup"><span data-stu-id="b64ca-213">For more information about how to set these configuration options, see [Create IoT hubs][lnk-portal].</span></span>

## <a name="next-steps"></a><span data-ttu-id="b64ca-214">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b64ca-214">Next steps</span></span>

<span data-ttu-id="b64ca-215">如需您可以用來接收雲端對裝置訊息之 SDK 的資訊，請參閱 [Azure IoT SDK][lnk-sdks]。</span><span class="sxs-lookup"><span data-stu-id="b64ca-215">For information about the SDKs you can use to receive cloud-to-device messages, see [Azure IoT SDKs][lnk-sdks].</span></span>

<span data-ttu-id="b64ca-216">若要嘗試接收雲端對裝置訊息，請參閱 [傳送雲端到裝置][lnk-c2d-tutorial] 教學課程。</span><span class="sxs-lookup"><span data-stu-id="b64ca-216">To try out receiving cloud-to-device messages, see the [Send cloud-to-device][lnk-c2d-tutorial] tutorial.</span></span>

[img-lifecycle]: ./media/iot-hub-devguide-messages-c2d/lifecycle.png

[lnk-portal]: iot-hub-create-through-portal.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-ttl]: #message-expiration-time-to-live
[lnk-c2d-configuration]: #cloud-to-device-configuration-options
[lnk-lifecycle]: #message-lifecycle
[lnk-c2d-tutorial]: iot-hub-csharp-csharp-c2d.md
