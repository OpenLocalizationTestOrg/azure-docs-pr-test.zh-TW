---
title: "aaaUnderstand Azure IoT 中樞雲端到裝置訊息 |Microsoft 文件"
description: "開發人員指南-如何 toouse 雲端到裝置與 IoT 中樞通訊。 包含 hello 訊息生命週期和組態選項的詳細資訊。"
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
ms.openlocfilehash: 5c747b50163873d823556a8baa769c4b8f7f8c44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="send-cloud-to-device-messages-from-iot-hub"></a><span data-ttu-id="b5206-104">從 IoT 中樞傳送雲端到裝置訊息</span><span class="sxs-lookup"><span data-stu-id="b5206-104">Send cloud-to-device messages from IoT Hub</span></span>

<span data-ttu-id="b5206-105">toosend 單向通知 toohello 裝置應用程式從您的方案後端，從您的 IoT 中樞 tooyour 裝置傳送雲端到裝置訊息。</span><span class="sxs-lookup"><span data-stu-id="b5206-105">toosend one-way notifications toohello device app from your solution back end, send cloud-to-devices messages from your IoT hub tooyour device.</span></span> <span data-ttu-id="b5206-106">如需 IoT 中樞所支援之其他雲端到裝置選項的討論，請參閱[雲端對裝置通訊指引][lnk-c2d-guidance]。</span><span class="sxs-lookup"><span data-stu-id="b5206-106">For a discussion of other cloud-to-devices options supported by IoT Hub, see [Cloud-to-device communications guidance][lnk-c2d-guidance].</span></span>

<span data-ttu-id="b5206-107">您可以透過面向服務的端點 (**/messages/devicebound**) 來傳送雲端到裝置訊息。</span><span class="sxs-lookup"><span data-stu-id="b5206-107">You send cloud-to-device messages through a service-facing endpoint (**/messages/devicebound**).</span></span> <span data-ttu-id="b5206-108">裝置再收到 hello 訊息透過裝置的特定端點 (**/devices/ {deviceId} / 訊息/devicebound**)。</span><span class="sxs-lookup"><span data-stu-id="b5206-108">A device then receives hello messages through a device-specific endpoint (**/devices/{deviceId}/messages/devicebound**).</span></span>

<span data-ttu-id="b5206-109">每個雲端到裝置訊息為目標的單一裝置設定 hello**至**屬性太**/devices/ {deviceId} / 訊息/devicebound**。</span><span class="sxs-lookup"><span data-stu-id="b5206-109">Each cloud-to-device message is targeted at a single device by setting hello **to** property too**/devices/{deviceId}/messages/devicebound**.</span></span>

<span data-ttu-id="b5206-110">每個裝置佇列最多保留 50 則雲端到裝置訊息。</span><span class="sxs-lookup"><span data-stu-id="b5206-110">Each device queue holds at most 50 cloud-to-device messages.</span></span> <span data-ttu-id="b5206-111">嘗試 toosend 詳細訊息 toohello 相同的裝置會導致錯誤。</span><span class="sxs-lookup"><span data-stu-id="b5206-111">Trying toosend more messages toohello same device results in an error.</span></span>

## <a name="hello-cloud-to-device-message-lifecycle"></a><span data-ttu-id="b5206-112">hello 雲端到裝置訊息生命週期</span><span class="sxs-lookup"><span data-stu-id="b5206-112">hello cloud-to-device message lifecycle</span></span>

<span data-ttu-id="b5206-113">tooguarantee 在-至少一次訊息傳遞，IoT 中樞保存每一裝置的佇列中的雲端到裝置訊息。</span><span class="sxs-lookup"><span data-stu-id="b5206-113">tooguarantee at-least-once message delivery, IoT Hub persists cloud-to-device messages in per-device queues.</span></span> <span data-ttu-id="b5206-114">裝置必須明確地認可*完成*的 IoT 中樞 tooremove 從 hello 佇列。</span><span class="sxs-lookup"><span data-stu-id="b5206-114">Devices must explicitly acknowledge *completion* for IoT Hub tooremove them from hello queue.</span></span> <span data-ttu-id="b5206-115">此方法保證連線失敗和裝置故障能夠恢復。</span><span class="sxs-lookup"><span data-stu-id="b5206-115">This approach guarantees resiliency against connectivity and device failures.</span></span>

<span data-ttu-id="b5206-116">hello 下列圖表顯示 hello 生命週期狀態圖表雲端到裝置訊息在 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="b5206-116">hello following diagram shows hello lifecycle state graph for a cloud-to-device message in IoT Hub.</span></span>

![雲端到裝置的訊息生命週期][img-lifecycle]

<span data-ttu-id="b5206-118">當 hello IoT 中樞服務傳送訊息 tooa 裝置、 hello 服務太設定 hello 訊息狀態**佇列**。</span><span class="sxs-lookup"><span data-stu-id="b5206-118">When hello IoT Hub service sends a message tooa device, hello service sets hello message state too**Enqueued**.</span></span> <span data-ttu-id="b5206-119">當裝置想太*接收*訊息時，IoT 中樞*鎖定*hello 訊息 (藉由設定 hello 狀態太**看不見**)，可讓其他執行緒上 hello 裝置 toostart接收其他訊息。</span><span class="sxs-lookup"><span data-stu-id="b5206-119">When a device wants too*receive* a message, IoT Hub *locks* hello message (by setting hello state too**Invisible**), which allows other threads on hello device toostart receiving other messages.</span></span> <span data-ttu-id="b5206-120">當裝置執行緒完成 hello 處理訊息時，它會通知的 IoT 中樞*完成*hello 訊息。</span><span class="sxs-lookup"><span data-stu-id="b5206-120">When a device thread completes hello processing of a message, it notifies IoT Hub by *completing* hello message.</span></span> <span data-ttu-id="b5206-121">IoT 中樞設定 hello 狀態太**已完成**。</span><span class="sxs-lookup"><span data-stu-id="b5206-121">IoT Hub then sets hello state too**Completed**.</span></span>

<span data-ttu-id="b5206-122">裝置也可以選擇：</span><span class="sxs-lookup"><span data-stu-id="b5206-122">A device can also choose to:</span></span>

* <span data-ttu-id="b5206-123">*拒絕*hello 訊息，導致 IoT 中樞 tooset 它 toohello**成為無效**狀態。</span><span class="sxs-lookup"><span data-stu-id="b5206-123">*Reject* hello message, which causes IoT Hub tooset it toohello **Deadlettered** state.</span></span> <span data-ttu-id="b5206-124">透過 hello MQTT 通訊協定連線的裝置無法拒絕雲端到裝置的訊息。</span><span class="sxs-lookup"><span data-stu-id="b5206-124">Devices that connect over hello MQTT protocol cannot reject cloud-to-device messages.</span></span>
* <span data-ttu-id="b5206-125">*放棄*hello 訊息，導致 IoT 中樞 tooput hello 訊息回 hello 佇列中，與 hello 狀態設定得**佇列**。</span><span class="sxs-lookup"><span data-stu-id="b5206-125">*Abandon* hello message, which causes IoT Hub tooput hello message back in hello queue, with hello state set too**Enqueued**.</span></span>

<span data-ttu-id="b5206-126">執行緒可能會失敗 tooprocess 訊息且不會通知 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="b5206-126">A thread could fail tooprocess a message without notifying IoT Hub.</span></span> <span data-ttu-id="b5206-127">在此情況下，自動訊息從 hello 轉換**看不見**狀態回復 toohello**佇列**狀態之後*可見性 （或鎖定） 的逾時*。</span><span class="sxs-lookup"><span data-stu-id="b5206-127">In this case, messages automatically transition from hello **Invisible** state back toohello **Enqueued** state after a *visibility (or lock) timeout*.</span></span> <span data-ttu-id="b5206-128">此逾時的 hello 預設值是一分鐘。</span><span class="sxs-lookup"><span data-stu-id="b5206-128">hello default value of this timeout is one minute.</span></span>

<span data-ttu-id="b5206-129">訊息可以切換 hello**加入佇列**和**看不見**狀態，最多 hello 的 hello 中指定的次數**最大傳遞計數**IoT 中樞上的屬性。</span><span class="sxs-lookup"><span data-stu-id="b5206-129">A message can transition between hello **Enqueued** and **Invisible** states for, at most, hello number of times specified in hello **max delivery count** property on IoT Hub.</span></span> <span data-ttu-id="b5206-130">轉換的次數之後, IoT 中樞設定 hello hello 訊息狀態太**成為無效**。</span><span class="sxs-lookup"><span data-stu-id="b5206-130">After that number of transitions, IoT Hub sets hello state of hello message too**Deadlettered**.</span></span> <span data-ttu-id="b5206-131">同樣地，IoT 中樞設定 hello 訊息狀態太**成為無效**的到期時間之後 (請參閱[時間 toolive][lnk-ttl])。</span><span class="sxs-lookup"><span data-stu-id="b5206-131">Similarly, IoT Hub sets hello state of a message too**Deadlettered** after its expiration time (see [Time toolive][lnk-ttl]).</span></span>

<span data-ttu-id="b5206-132">hello [toosend 雲端到裝置與 IoT 中樞的訊息][ lnk-c2d-tutorial]會示範如何從 hello toosend 雲端到裝置訊息雲端及接收這些裝置上。</span><span class="sxs-lookup"><span data-stu-id="b5206-132">hello [How toosend cloud-to-device messages with IoT Hub][lnk-c2d-tutorial] shows you how toosend cloud-to-device messages from hello cloud and receive them on a device.</span></span>

<span data-ttu-id="b5206-133">一般而言，裝置會在雲端到裝置訊息完成時 hello 遺失 hello 訊息不會影響 hello 應用程式邏輯。</span><span class="sxs-lookup"><span data-stu-id="b5206-133">Typically, a device completes a cloud-to-device message when hello loss of hello message does not affect hello application logic.</span></span> <span data-ttu-id="b5206-134">比方說，當 hello 裝置已保存在本機 hello 訊息內容或已成功執行作業。</span><span class="sxs-lookup"><span data-stu-id="b5206-134">For example, when hello device has persisted hello message content locally or has successfully executed an operation.</span></span> <span data-ttu-id="b5206-135">hello 訊息也可能具有暫時性資訊，其遺失不會影響 hello hello 應用程式功能。</span><span class="sxs-lookup"><span data-stu-id="b5206-135">hello message could also carry transient information, whose loss would not impact hello functionality of hello application.</span></span> <span data-ttu-id="b5206-136">某些情況下，對於長時間執行工作，您可以完成 hello 雲端到裝置訊息後保存 hello 本機儲存體中的工作描述。</span><span class="sxs-lookup"><span data-stu-id="b5206-136">Sometimes, for long-running tasks, you can complete hello cloud-to-device message after persisting hello task description in local storage.</span></span> <span data-ttu-id="b5206-137">然後您可以在各個階段的 hello 工作的進度通知 hello 與一或多個裝置到雲端訊息方案後的端。</span><span class="sxs-lookup"><span data-stu-id="b5206-137">Then you can notify hello solution back end with one or more device-to-cloud messages at various stages of progress of hello task.</span></span>

## <a name="message-expiration-time-toolive"></a><span data-ttu-id="b5206-138">訊息的過期 （toolive 時間）</span><span class="sxs-lookup"><span data-stu-id="b5206-138">Message expiration (time toolive)</span></span>

<span data-ttu-id="b5206-139">每個雲端到裝置的訊息都有到期時間。</span><span class="sxs-lookup"><span data-stu-id="b5206-139">Every cloud-to-device message has an expiration time.</span></span> <span data-ttu-id="b5206-140">這次透過設定 hello 服務 (在 hello **ExpiryTimeUtc**屬性)，或使用 hello 預設的 IoT 中樞*時間 toolive*指定為 IoT 中樞內容。</span><span class="sxs-lookup"><span data-stu-id="b5206-140">This time is set either by hello service (in hello **ExpiryTimeUtc** property), or by IoT Hub using hello default *time toolive* specified as an IoT Hub property.</span></span> <span data-ttu-id="b5206-141">請參閱[雲端到裝置的設定選項][lnk-c2d-configuration]。</span><span class="sxs-lookup"><span data-stu-id="b5206-141">See [Cloud-to-device configuration options][lnk-c2d-configuration].</span></span>

<span data-ttu-id="b5206-142">常見方式 tootake 優點訊息過期並避免 toodisconnected 裝置傳送訊息，是 tooset toolive 的簡短時間值。</span><span class="sxs-lookup"><span data-stu-id="b5206-142">A common way tootake advantage of message expiration and avoid sending messages toodisconnected devices, is tooset short time toolive values.</span></span> <span data-ttu-id="b5206-143">這種方法可達到相同結果與維護 hello 裝置連接狀態，同時會更有效率的 hello。</span><span class="sxs-lookup"><span data-stu-id="b5206-143">This approach achieves hello same result as maintaining hello device connection state, while being more efficient.</span></span> <span data-ttu-id="b5206-144">當您要求訊息收條時，IoT 中樞會通知您哪些裝置可以 tooreceive 訊息，以及哪些裝置不在線上或已失敗。</span><span class="sxs-lookup"><span data-stu-id="b5206-144">When you request message acknowledgements, IoT Hub notifies you which devices are able tooreceive messages, and which devices are not online or have failed.</span></span>

## <a name="message-feedback"></a><span data-ttu-id="b5206-145">訊息意見反應</span><span class="sxs-lookup"><span data-stu-id="b5206-145">Message feedback</span></span>

<span data-ttu-id="b5206-146">當您傳送雲端到裝置訊息時，hello 服務可以要求 hello 傳送 hello 訊息的最終狀態有關的每個訊息意見反應。</span><span class="sxs-lookup"><span data-stu-id="b5206-146">When you send a cloud-to-device message, hello service can request hello delivery of per-message feedback regarding hello final state of that message.</span></span>

| <span data-ttu-id="b5206-147">Ack 屬性</span><span class="sxs-lookup"><span data-stu-id="b5206-147">Ack property</span></span> | <span data-ttu-id="b5206-148">行為</span><span class="sxs-lookup"><span data-stu-id="b5206-148">Behavior</span></span> |
| ------------ | -------- |
| <span data-ttu-id="b5206-149">**positive**</span><span class="sxs-lookup"><span data-stu-id="b5206-149">**positive**</span></span> | <span data-ttu-id="b5206-150">IoT 中樞會產生回應訊息，並僅有，hello 雲端到裝置訊息已到達 hello**已完成**狀態。</span><span class="sxs-lookup"><span data-stu-id="b5206-150">IoT Hub generates a feedback message if, and only if, hello cloud-to-device message reached hello **Completed** state.</span></span> |
| <span data-ttu-id="b5206-151">**negative**</span><span class="sxs-lookup"><span data-stu-id="b5206-151">**negative**</span></span> | <span data-ttu-id="b5206-152">IoT 中樞會產生回應訊息時，如果且只有，hello 雲端到裝置訊息到達 hello**成為無效**狀態。</span><span class="sxs-lookup"><span data-stu-id="b5206-152">IoT Hub generates a feedback message, if and only if, hello cloud-to-device message reaches hello **Deadlettered** state.</span></span> |
| <span data-ttu-id="b5206-153">**full**</span><span class="sxs-lookup"><span data-stu-id="b5206-153">**full**</span></span>     | <span data-ttu-id="b5206-154">IoT 中樞在任一情況下都會產生意見反應訊息。</span><span class="sxs-lookup"><span data-stu-id="b5206-154">IoT Hub generates a feedback message in either case.</span></span> |

<span data-ttu-id="b5206-155">如果**Ack**是**完整**，而且您沒有收到回應訊息，則表示該 hello 回應訊息過期。</span><span class="sxs-lookup"><span data-stu-id="b5206-155">If **Ack** is **full**, and you don't receive a feedback message, it means that hello feedback message expired.</span></span> <span data-ttu-id="b5206-156">hello 服務無法知道哪些情形的 toohello 原始訊息。</span><span class="sxs-lookup"><span data-stu-id="b5206-156">hello service can't know what happened toohello original message.</span></span> <span data-ttu-id="b5206-157">在實務上，服務應該確定在到期之前可以處理 hello 意見反應。</span><span class="sxs-lookup"><span data-stu-id="b5206-157">In practice, a service should ensure that it can process hello feedback before it expires.</span></span> <span data-ttu-id="b5206-158">hello 最長有效時間是兩天內，這允許充足的時間 tooget hello 服務執行一次發生失敗時。</span><span class="sxs-lookup"><span data-stu-id="b5206-158">hello maximum expiry time is two days, which allows plenty of time tooget hello service running again if a failure occurs.</span></span>

<span data-ttu-id="b5206-159">如[端點][lnk-endpoints]中所述，IoT 中樞會透過面向服務的端點 (**/messages/servicebound/feedback**) 利用訊息來傳遞意見反應。</span><span class="sxs-lookup"><span data-stu-id="b5206-159">As explained in [Endpoints][lnk-endpoints], IoT Hub delivers feedback through a service-facing endpoint (**/messages/servicebound/feedback**) as messages.</span></span> <span data-ttu-id="b5206-160">hello 語意收到意見 hello 相同與雲端到裝置訊息與 hello 相同[訊息生命週期][lnk-lifecycle]。</span><span class="sxs-lookup"><span data-stu-id="b5206-160">hello semantics for receiving feedback are hello same as for cloud-to-device messages, and have hello same [Message lifecycle][lnk-lifecycle].</span></span> <span data-ttu-id="b5206-161">可能的話，會在單一訊息中，以下列格式的 hello 進行批次處理訊息的意見反應：</span><span class="sxs-lookup"><span data-stu-id="b5206-161">Whenever possible, message feedback is batched in a single message, with hello following format:</span></span>

| <span data-ttu-id="b5206-162">屬性</span><span class="sxs-lookup"><span data-stu-id="b5206-162">Property</span></span>     | <span data-ttu-id="b5206-163">說明</span><span class="sxs-lookup"><span data-stu-id="b5206-163">Description</span></span> |
| ------------ | ----------- |
| <span data-ttu-id="b5206-164">EnqueuedTime</span><span class="sxs-lookup"><span data-stu-id="b5206-164">EnqueuedTime</span></span> | <span data-ttu-id="b5206-165">指出建立 hello 訊息時的時間戳記。</span><span class="sxs-lookup"><span data-stu-id="b5206-165">Timestamp indicating when hello message was created.</span></span> |
| <span data-ttu-id="b5206-166">UserId</span><span class="sxs-lookup"><span data-stu-id="b5206-166">UserId</span></span>       | `{iot hub name}` |
| <span data-ttu-id="b5206-167">ContentType</span><span class="sxs-lookup"><span data-stu-id="b5206-167">ContentType</span></span>  | `application/vnd.microsoft.iothub.feedback.json` |

<span data-ttu-id="b5206-168">hello 內文是 JSON 序列化的記錄陣列，每個都具有下列屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="b5206-168">hello body is a JSON-serialized array of records, each with hello following properties:</span></span>

| <span data-ttu-id="b5206-169">屬性</span><span class="sxs-lookup"><span data-stu-id="b5206-169">Property</span></span>           | <span data-ttu-id="b5206-170">說明</span><span class="sxs-lookup"><span data-stu-id="b5206-170">Description</span></span> |
| ------------------ | ----------- |
| <span data-ttu-id="b5206-171">EnqueuedTimeUtc</span><span class="sxs-lookup"><span data-stu-id="b5206-171">EnqueuedTimeUtc</span></span>    | <span data-ttu-id="b5206-172">指出發生 hello 結果 hello 訊息的時間戳記。</span><span class="sxs-lookup"><span data-stu-id="b5206-172">Timestamp indicating when hello outcome of hello message happened.</span></span> <span data-ttu-id="b5206-173">例如，hello 完成裝置或 hello 訊息過期。</span><span class="sxs-lookup"><span data-stu-id="b5206-173">For example, hello device completed or hello message expired.</span></span> |
| <span data-ttu-id="b5206-174">OriginalMessageId</span><span class="sxs-lookup"><span data-stu-id="b5206-174">OriginalMessageId</span></span>  | <span data-ttu-id="b5206-175">**MessageId**的 hello 雲端到裝置訊息 toowhich 此意見反應資訊與相關。</span><span class="sxs-lookup"><span data-stu-id="b5206-175">**MessageId** of hello cloud-to-device message toowhich this feedback information relates.</span></span> |
| <span data-ttu-id="b5206-176">StatusCode</span><span class="sxs-lookup"><span data-stu-id="b5206-176">StatusCode</span></span>         | <span data-ttu-id="b5206-177">必要字串。</span><span class="sxs-lookup"><span data-stu-id="b5206-177">Required string.</span></span> <span data-ttu-id="b5206-178">用於 IoT 中樞所產生的回饋訊息中。</span><span class="sxs-lookup"><span data-stu-id="b5206-178">Used in feedback messages generated by IoT Hub.</span></span> <br/> <span data-ttu-id="b5206-179">「成功」</span><span class="sxs-lookup"><span data-stu-id="b5206-179">'Success'</span></span> <br/> <span data-ttu-id="b5206-180">「已過期」</span><span class="sxs-lookup"><span data-stu-id="b5206-180">'Expired'</span></span> <br/> <span data-ttu-id="b5206-181">「DeliveryCountExceeded」</span><span class="sxs-lookup"><span data-stu-id="b5206-181">'DeliveryCountExceeded'</span></span> <br/> <span data-ttu-id="b5206-182">「已拒絕」</span><span class="sxs-lookup"><span data-stu-id="b5206-182">'Rejected'</span></span> <br/> <span data-ttu-id="b5206-183">「已清除」</span><span class="sxs-lookup"><span data-stu-id="b5206-183">'Purged'</span></span> |
| <span data-ttu-id="b5206-184">描述</span><span class="sxs-lookup"><span data-stu-id="b5206-184">Description</span></span>        | <span data-ttu-id="b5206-185">**StatusCode**的字串值。</span><span class="sxs-lookup"><span data-stu-id="b5206-185">String values for **StatusCode**.</span></span> |
| <span data-ttu-id="b5206-186">deviceId</span><span class="sxs-lookup"><span data-stu-id="b5206-186">DeviceId</span></span>           | <span data-ttu-id="b5206-187">**DeviceId** hello 目標裝置的 hello 雲端到裝置訊息 toowhich 相關的意見反應此片段。</span><span class="sxs-lookup"><span data-stu-id="b5206-187">**DeviceId** of hello target device of hello cloud-to-device message toowhich this piece of feedback relates.</span></span> |
| <span data-ttu-id="b5206-188">DeviceGenerationId</span><span class="sxs-lookup"><span data-stu-id="b5206-188">DeviceGenerationId</span></span> | <span data-ttu-id="b5206-189">**DeviceGenerationId** hello 目標裝置的 hello 雲端到裝置訊息 toowhich 相關的意見反應此片段。</span><span class="sxs-lookup"><span data-stu-id="b5206-189">**DeviceGenerationId** of hello target device of hello cloud-to-device message toowhich this piece of feedback relates.</span></span> |

<span data-ttu-id="b5206-190">必須指定 hello 服務**MessageId** hello 雲端到裝置訊息 toobe 無法 toocorrelate 其意見反應與 hello 原始訊息。</span><span class="sxs-lookup"><span data-stu-id="b5206-190">hello service must specify a **MessageId** for hello cloud-to-device message toobe able toocorrelate its feedback with hello original message.</span></span>

<span data-ttu-id="b5206-191">hello 下列範例顯示 hello 訊息本文的意見反應。</span><span class="sxs-lookup"><span data-stu-id="b5206-191">hello following example shows hello body of a feedback message.</span></span>

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

## <a name="cloud-to-device-configuration-options"></a><span data-ttu-id="b5206-192">雲端到裝置組態選項</span><span class="sxs-lookup"><span data-stu-id="b5206-192">Cloud-to-device configuration options</span></span>

<span data-ttu-id="b5206-193">每個 IoT 中樞會公開下列組態選項適用於雲端到裝置訊息 hello:</span><span class="sxs-lookup"><span data-stu-id="b5206-193">Each IoT hub exposes hello following configuration options for cloud-to-device messaging:</span></span>

| <span data-ttu-id="b5206-194">屬性</span><span class="sxs-lookup"><span data-stu-id="b5206-194">Property</span></span>                  | <span data-ttu-id="b5206-195">說明</span><span class="sxs-lookup"><span data-stu-id="b5206-195">Description</span></span> | <span data-ttu-id="b5206-196">範圍和預設值</span><span class="sxs-lookup"><span data-stu-id="b5206-196">Range and default</span></span> |
| ------------------------- | ----------- | ----------------- |
| <span data-ttu-id="b5206-197">defaultTtlAsIso8601</span><span class="sxs-lookup"><span data-stu-id="b5206-197">defaultTtlAsIso8601</span></span>       | <span data-ttu-id="b5206-198">雲端到裝置訊息的預設 TTL。</span><span class="sxs-lookup"><span data-stu-id="b5206-198">Default TTL for cloud-to-device messages.</span></span> | <span data-ttu-id="b5206-199">向上 too2D ISO_8601 間隔 （最小的 1 分鐘）。</span><span class="sxs-lookup"><span data-stu-id="b5206-199">ISO_8601 interval up too2D (minimum 1 minute).</span></span> <span data-ttu-id="b5206-200">預設值︰1 小時。</span><span class="sxs-lookup"><span data-stu-id="b5206-200">Default: 1 hour.</span></span> |
| <span data-ttu-id="b5206-201">maxDeliveryCount</span><span class="sxs-lookup"><span data-stu-id="b5206-201">maxDeliveryCount</span></span>          | <span data-ttu-id="b5206-202">每個裝置佇列的雲端到裝置最大傳遞計數。</span><span class="sxs-lookup"><span data-stu-id="b5206-202">Maximum delivery count for cloud-to-device per-device queues.</span></span> | <span data-ttu-id="b5206-203">1 too100。</span><span class="sxs-lookup"><span data-stu-id="b5206-203">1 too100.</span></span> <span data-ttu-id="b5206-204">預設值：10</span><span class="sxs-lookup"><span data-stu-id="b5206-204">Default: 10.</span></span> |
| <span data-ttu-id="b5206-205">feedback.ttlAsIso8601</span><span class="sxs-lookup"><span data-stu-id="b5206-205">feedback.ttlAsIso8601</span></span>     | <span data-ttu-id="b5206-206">保留服務繫結的意見反應訊息。</span><span class="sxs-lookup"><span data-stu-id="b5206-206">Retention for service-bound feedback messages.</span></span> | <span data-ttu-id="b5206-207">向上 too2D ISO_8601 間隔 （最小的 1 分鐘）。</span><span class="sxs-lookup"><span data-stu-id="b5206-207">ISO_8601 interval up too2D (minimum 1 minute).</span></span> <span data-ttu-id="b5206-208">預設值︰1 小時。</span><span class="sxs-lookup"><span data-stu-id="b5206-208">Default: 1 hour.</span></span> |
| <span data-ttu-id="b5206-209">feedback.maxDeliveryCount</span><span class="sxs-lookup"><span data-stu-id="b5206-209">feedback.maxDeliveryCount</span></span> |<span data-ttu-id="b5206-210">意見反應佇列的最大傳遞計數。</span><span class="sxs-lookup"><span data-stu-id="b5206-210">Maximum delivery count for feedback queue.</span></span> | <span data-ttu-id="b5206-211">1 too100。</span><span class="sxs-lookup"><span data-stu-id="b5206-211">1 too100.</span></span> <span data-ttu-id="b5206-212">預設值 = 100。</span><span class="sxs-lookup"><span data-stu-id="b5206-212">Default: 100.</span></span> |

<span data-ttu-id="b5206-213">如需有關如何 tooset 這些組態選項，請參閱[建立 IoT 中樞][lnk-portal]。</span><span class="sxs-lookup"><span data-stu-id="b5206-213">For more information about how tooset these configuration options, see [Create IoT hubs][lnk-portal].</span></span>

## <a name="next-steps"></a><span data-ttu-id="b5206-214">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b5206-214">Next steps</span></span>

<span data-ttu-id="b5206-215">如需 hello Sdk，您可以使用 tooreceive 雲端到裝置訊息，請參閱[Azure IoT Sdk][lnk-sdks]。</span><span class="sxs-lookup"><span data-stu-id="b5206-215">For information about hello SDKs you can use tooreceive cloud-to-device messages, see [Azure IoT SDKs][lnk-sdks].</span></span>

<span data-ttu-id="b5206-216">tootry 出接收雲端到裝置訊息，請參閱 hello[傳送雲端到裝置][ lnk-c2d-tutorial]教學課程。</span><span class="sxs-lookup"><span data-stu-id="b5206-216">tootry out receiving cloud-to-device messages, see hello [Send cloud-to-device][lnk-c2d-tutorial] tutorial.</span></span>

[img-lifecycle]: ./media/iot-hub-devguide-messages-c2d/lifecycle.png

[lnk-portal]: iot-hub-create-through-portal.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-ttl]: #message-expiration-time-to-live
[lnk-c2d-configuration]: #cloud-to-device-configuration-options
[lnk-lifecycle]: #message-lifecycle
[lnk-c2d-tutorial]: iot-hub-csharp-csharp-c2d.md
