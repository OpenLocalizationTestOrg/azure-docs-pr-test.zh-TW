---
title: "了解 Azure IoT 中樞訊息格式 | Microsoft Docs"
description: "開發人員指南 - 說明 IoT 中樞訊息的格式和預期內容。"
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 3fc5f1a3-3711-4611-9897-d4db079b4250
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: dobett
ms.openlocfilehash: e6eafb1a0030b022da2b5d0b787e092f3067c99f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="create-and-read-iot-hub-messages"></a><span data-ttu-id="ffa15-103">建立及讀取 IoT 中樞訊息</span><span class="sxs-lookup"><span data-stu-id="ffa15-103">Create and read IoT Hub messages</span></span>

<span data-ttu-id="ffa15-104">為了支援完美的跨通訊協定互通性，IoT 中樞定義了適用於所有裝置面向通訊協定的通用訊息格式。</span><span class="sxs-lookup"><span data-stu-id="ffa15-104">To support seamless interoperability across protocols, IoT Hub defines a common message format for all device-facing protocols.</span></span> <span data-ttu-id="ffa15-105">此訊息格式可用於[裝置對雲端][lnk-d2c]和[雲端對裝置][lnk-c2d]訊息。</span><span class="sxs-lookup"><span data-stu-id="ffa15-105">This message format is used for both [device-to-cloud][lnk-d2c] and [cloud-to-device][lnk-c2d] messages.</span></span> <span data-ttu-id="ffa15-106">[IoT 中樞訊息][lnk-messaging]包含：</span><span class="sxs-lookup"><span data-stu-id="ffa15-106">An [IoT Hub message][lnk-messaging] consists of:</span></span>

* <span data-ttu-id="ffa15-107">一組 *系統屬性*。</span><span class="sxs-lookup"><span data-stu-id="ffa15-107">A set of *system properties*.</span></span> <span data-ttu-id="ffa15-108">IoT 中樞解譯或設定的屬性。</span><span class="sxs-lookup"><span data-stu-id="ffa15-108">Properties that IoT Hub interprets or sets.</span></span> <span data-ttu-id="ffa15-109">這個集合是預先決定的。</span><span class="sxs-lookup"><span data-stu-id="ffa15-109">This set is predetermined.</span></span>
* <span data-ttu-id="ffa15-110">一組 *應用程式屬性*。</span><span class="sxs-lookup"><span data-stu-id="ffa15-110">A set of *application properties*.</span></span> <span data-ttu-id="ffa15-111">應用程式可以定義的字串屬性字典，而且不需將訊息本文還原序列化即可加以存取。</span><span class="sxs-lookup"><span data-stu-id="ffa15-111">A dictionary of string properties that the application can define and access, without needing to deserialize the message body.</span></span> <span data-ttu-id="ffa15-112">IoT 中樞不會修改這些屬性。</span><span class="sxs-lookup"><span data-stu-id="ffa15-112">IoT Hub never modifies these properties.</span></span>
* <span data-ttu-id="ffa15-113">不透明的二進位主體。</span><span class="sxs-lookup"><span data-stu-id="ffa15-113">An opaque binary body.</span></span>

<span data-ttu-id="ffa15-114">在下列情況下，屬性名稱和值只能包含 ASCII 英數字元和 ``{'!', '#', '$', '%, '&', "'", '*', '*', '+', '-', '.', '^', '_', '`', '|', '~'}`\`：</span><span class="sxs-lookup"><span data-stu-id="ffa15-114">Property names and values can only contain ASCII alphanumeric characters, plus ``{'!', '#', '$', '%, '&', "'", '*', '*', '+', '-', '.', '^', '_', '`', '|', '~'}`\` when you:</span></span>

* <span data-ttu-id="ffa15-115">使用 HTTP 通訊協定傳送裝置到雲端訊息。</span><span class="sxs-lookup"><span data-stu-id="ffa15-115">Send device-to-cloud messages using the HTTP protocol.</span></span>
* <span data-ttu-id="ffa15-116">傳送雲端到裝置的訊息。</span><span class="sxs-lookup"><span data-stu-id="ffa15-116">Send cloud-to-device messages.</span></span>

<span data-ttu-id="ffa15-117">如需如何將使用不同通訊協定傳送的訊息編碼和解碼的詳細資訊，請參閱 [Azure IoT SDK][lnk-sdks]。</span><span class="sxs-lookup"><span data-stu-id="ffa15-117">For more information about how to encode and decode messages sent using different protocols, see [Azure IoT SDKs][lnk-sdks].</span></span>

<span data-ttu-id="ffa15-118">下表列出 IoT 中樞訊息中的系統屬性集合。</span><span class="sxs-lookup"><span data-stu-id="ffa15-118">The following table lists the set of system properties in IoT Hub messages.</span></span>

| <span data-ttu-id="ffa15-119">屬性</span><span class="sxs-lookup"><span data-stu-id="ffa15-119">Property</span></span> | <span data-ttu-id="ffa15-120">說明</span><span class="sxs-lookup"><span data-stu-id="ffa15-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ffa15-121">MessageId</span><span class="sxs-lookup"><span data-stu-id="ffa15-121">MessageId</span></span> |<span data-ttu-id="ffa15-122">使用者可設定的訊息識別碼，用於「要求-回覆」模式。</span><span class="sxs-lookup"><span data-stu-id="ffa15-122">A user-settable identifier for the message used for request-reply patterns.</span></span> <span data-ttu-id="ffa15-123">格式：區分大小寫的字串，最長為 128 個字元，可使用 ASCII 7 位元英數字元和 `{'-', ':',’.', '+', '%', '_', '#', '*', '?', '!', '(', ')', ',', '=', '@', ';', '$', '''}`。</span><span class="sxs-lookup"><span data-stu-id="ffa15-123">Format: A case-sensitive string (up to 128 characters long) of ASCII 7-bit alphanumeric characters + `{'-', ':',’.', '+', '%', '_', '#', '*', '?', '!', '(', ')', ',', '=', '@', ';', '$', '''}`.</span></span> |
| <span data-ttu-id="ffa15-124">序號</span><span class="sxs-lookup"><span data-stu-id="ffa15-124">Sequence number</span></span> |<span data-ttu-id="ffa15-125">IoT 中樞指派給每則雲端到裝置訊息的數字 (對每個裝置佇列而言都是唯一的)。</span><span class="sxs-lookup"><span data-stu-id="ffa15-125">A number (unique per device-queue) assigned by IoT Hub to each cloud-to-device message.</span></span> |
| <span data-ttu-id="ffa15-126">收件人</span><span class="sxs-lookup"><span data-stu-id="ffa15-126">To</span></span> |<span data-ttu-id="ffa15-127">[雲端到裝置][lnk-c2d]訊息中指定的目的地。</span><span class="sxs-lookup"><span data-stu-id="ffa15-127">A destination specified in [Cloud-to-Device][lnk-c2d] messages.</span></span> |
| <span data-ttu-id="ffa15-128">ExpiryTimeUtc</span><span class="sxs-lookup"><span data-stu-id="ffa15-128">ExpiryTimeUtc</span></span> |<span data-ttu-id="ffa15-129">訊息到期的日期和時間。</span><span class="sxs-lookup"><span data-stu-id="ffa15-129">Date and time of message expiration.</span></span> |
| <span data-ttu-id="ffa15-130">EnqueuedTime</span><span class="sxs-lookup"><span data-stu-id="ffa15-130">EnqueuedTime</span></span> |<span data-ttu-id="ffa15-131">IoT 中樞收到[雲端到裝置][lnk-c2d]訊息的日期和時間。</span><span class="sxs-lookup"><span data-stu-id="ffa15-131">Date and time the [Cloud-to-Device][lnk-c2d] message was received by IoT Hub.</span></span> |
| <span data-ttu-id="ffa15-132">CorrelationId</span><span class="sxs-lookup"><span data-stu-id="ffa15-132">CorrelationId</span></span> |<span data-ttu-id="ffa15-133">回應訊息中的字串屬性，通常包含採用「要求-回覆」模式之要求的 MessageId。</span><span class="sxs-lookup"><span data-stu-id="ffa15-133">A string property in a response message that typically contains the MessageId of the request, in request-reply patterns.</span></span> |
| <span data-ttu-id="ffa15-134">UserId</span><span class="sxs-lookup"><span data-stu-id="ffa15-134">UserId</span></span> |<span data-ttu-id="ffa15-135">用來指定訊息來源的識別碼。</span><span class="sxs-lookup"><span data-stu-id="ffa15-135">An ID used to specify the origin of messages.</span></span> <span data-ttu-id="ffa15-136">當 IoT 中樞產生訊息時，它會設定為 `{iot hub name}`。</span><span class="sxs-lookup"><span data-stu-id="ffa15-136">When messages are generated by IoT Hub, it is set to `{iot hub name}`.</span></span> |
| <span data-ttu-id="ffa15-137">Ack</span><span class="sxs-lookup"><span data-stu-id="ffa15-137">Ack</span></span> |<span data-ttu-id="ffa15-138">意見反應訊息產生器。</span><span class="sxs-lookup"><span data-stu-id="ffa15-138">A feedback message generator.</span></span> <span data-ttu-id="ffa15-139">這個屬性是在雲端到裝置訊息中使用，可要求 IoT 中樞因為裝置取用訊息而產生意見反應訊息。</span><span class="sxs-lookup"><span data-stu-id="ffa15-139">This property is used in cloud-to-device messages to request IoT Hub to generate feedback messages as a result of the consumption of the message by the device.</span></span> <span data-ttu-id="ffa15-140">可能的值︰**none** (預設值)︰不會產生任何意見反應訊息；**positive**︰如果訊息已完成，則會收到意見反應訊息；**negative**︰如果訊息未由裝置完成就到期 (或已達到最大傳遞計數) 則會收到意見反應訊息；或者 **full**︰positive 和 negative。</span><span class="sxs-lookup"><span data-stu-id="ffa15-140">Possible values: **none** (default): no feedback message is generated, **positive**: receive a feedback message if the message was completed, **negative**: receive a feedback message if the message expired (or maximum delivery count was reached) without being completed by the device, or **full**: both positive and negative.</span></span> <span data-ttu-id="ffa15-141">若需詳細資訊，請參閱[訊息意見反應][lnk-feedback]。</span><span class="sxs-lookup"><span data-stu-id="ffa15-141">For more information, see [Message feedback][lnk-feedback].</span></span> |
| <span data-ttu-id="ffa15-142">ConnectionDeviceId</span><span class="sxs-lookup"><span data-stu-id="ffa15-142">ConnectionDeviceId</span></span> |<span data-ttu-id="ffa15-143">由 IoT 中樞在裝置到雲端訊息上設定的識別碼。</span><span class="sxs-lookup"><span data-stu-id="ffa15-143">An ID set by IoT Hub on device-to-cloud messages.</span></span> <span data-ttu-id="ffa15-144">它包含傳送訊息之裝置的 **deviceId** 。</span><span class="sxs-lookup"><span data-stu-id="ffa15-144">It contains the **deviceId** of the device that sent the message.</span></span> |
| <span data-ttu-id="ffa15-145">ConnectionDeviceGenerationId</span><span class="sxs-lookup"><span data-stu-id="ffa15-145">ConnectionDeviceGenerationId</span></span> |<span data-ttu-id="ffa15-146">由 IoT 中樞在裝置到雲端訊息上設定的識別碼。</span><span class="sxs-lookup"><span data-stu-id="ffa15-146">An ID set by IoT Hub on device-to-cloud messages.</span></span> <span data-ttu-id="ffa15-147">它包含傳送訊息之裝置的 **generationId** (依據[裝置身分識別屬性][lnk-device-properties])。</span><span class="sxs-lookup"><span data-stu-id="ffa15-147">It contains the **generationId** (as per [Device identity properties][lnk-device-properties]) of the device that sent the message.</span></span> |
| <span data-ttu-id="ffa15-148">ConnectionAuthMethod</span><span class="sxs-lookup"><span data-stu-id="ffa15-148">ConnectionAuthMethod</span></span> |<span data-ttu-id="ffa15-149">由 IoT 中樞在裝置到雲端訊息上設定的驗證方法。</span><span class="sxs-lookup"><span data-stu-id="ffa15-149">An authentication method set by IoT Hub on device-to-cloud messages.</span></span> <span data-ttu-id="ffa15-150">這個屬性包含用來驗證傳送訊息之裝置的驗證方法的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="ffa15-150">This property contains information about the authentication method used to authenticate the device sending the message.</span></span> <span data-ttu-id="ffa15-151">如需詳細資訊，請參閱[裝置到雲端反詐騙][lnk-antispoofing]。</span><span class="sxs-lookup"><span data-stu-id="ffa15-151">For more information, see [Device to cloud anti-spoofing][lnk-antispoofing].</span></span> |

## <a name="message-size"></a><span data-ttu-id="ffa15-152">訊息大小</span><span class="sxs-lookup"><span data-stu-id="ffa15-152">Message size</span></span>

<span data-ttu-id="ffa15-153">IoT 中樞會以不限通訊協定的方式 (只考慮實際的承載) 測量郵件大小。</span><span class="sxs-lookup"><span data-stu-id="ffa15-153">IoT Hub measures message size in a protocol-agnostic way, considering only the actual payload.</span></span> <span data-ttu-id="ffa15-154">大小 (以位元組為單位) 的計算方式為下列項目的總和︰</span><span class="sxs-lookup"><span data-stu-id="ffa15-154">The size in bytes is calculated as the sum of the following:</span></span>

* <span data-ttu-id="ffa15-155">內文大小 (以位元組為單位)。</span><span class="sxs-lookup"><span data-stu-id="ffa15-155">The body size in bytes.</span></span>
* <span data-ttu-id="ffa15-156">訊息系統屬性所有值的大小 (以位元組為單位)。</span><span class="sxs-lookup"><span data-stu-id="ffa15-156">The size in bytes of all the values of the message system properties.</span></span>
* <span data-ttu-id="ffa15-157">所有使用者屬性名稱和值的大小 (以位元組為單位)。</span><span class="sxs-lookup"><span data-stu-id="ffa15-157">The size in bytes of all user property names and values.</span></span>

<span data-ttu-id="ffa15-158">屬性名稱和值僅限使用 ASCII 字元，因此字串長度會等於大小 (以位元組為單位)。</span><span class="sxs-lookup"><span data-stu-id="ffa15-158">Property names and values are limited to ASCII characters, so the length of the strings equals the size in bytes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ffa15-159">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ffa15-159">Next steps</span></span>

<span data-ttu-id="ffa15-160">如需 IoT 中樞訊息大小限制的資訊，請參閱 [IoT 中樞配額和節流][lnk-quotas]。</span><span class="sxs-lookup"><span data-stu-id="ffa15-160">For information about message size limits in IoT Hub, see [IoT Hub quotas and throttling][lnk-quotas].</span></span>

<span data-ttu-id="ffa15-161">若要了解如何以各種程式設計語言建立及讀取 IoT 中樞訊息，請參閱[快速入門][lnk-get-started]教學課程。</span><span class="sxs-lookup"><span data-stu-id="ffa15-161">To learn how to create and read IoT Hub messages in various programming languages, see the [Get started][lnk-get-started] tutorials.</span></span>

[lnk-messaging]: iot-hub-devguide-messaging.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-get-started]: iot-hub-get-started.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-c2d]: iot-hub-devguide-messages-c2d.md
[lnk-d2c]: iot-hub-devguide-messages-d2c.md
[lnk-feedback]: iot-hub-devguide-messages-c2d.md#message-feedback
[lnk-device-properties]: iot-hub-devguide-identity-registry.md#device-identity-properties
[lnk-antispoofing]: iot-hub-devguide-messages-d2c.md#anti-spoofing-properties
