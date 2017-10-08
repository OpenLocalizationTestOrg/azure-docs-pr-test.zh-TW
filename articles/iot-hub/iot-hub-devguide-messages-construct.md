---
title: "aaaUnderstand Azure IoT 中樞訊息格式 |Microsoft 文件"
description: "開發人員指南-descibes hello 格式和預期的 IoT 中樞訊息的內容。"
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
ms.openlocfilehash: 3b1567e47bc32f70c0c252996648c4035ae81243
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-read-iot-hub-messages"></a><span data-ttu-id="7ea38-103">建立及讀取 IoT 中樞訊息</span><span class="sxs-lookup"><span data-stu-id="7ea38-103">Create and read IoT Hub messages</span></span>

<span data-ttu-id="7ea38-104">toosupport 順暢互通性之間的通訊協定，IoT 中樞定義所有面對裝置的通訊協定的一般訊息格式。</span><span class="sxs-lookup"><span data-stu-id="7ea38-104">toosupport seamless interoperability across protocols, IoT Hub defines a common message format for all device-facing protocols.</span></span> <span data-ttu-id="7ea38-105">此訊息格式可用於[裝置對雲端][lnk-d2c]和[雲端對裝置][lnk-c2d]訊息。</span><span class="sxs-lookup"><span data-stu-id="7ea38-105">This message format is used for both [device-to-cloud][lnk-d2c] and [cloud-to-device][lnk-c2d] messages.</span></span> <span data-ttu-id="7ea38-106">[IoT 中樞訊息][lnk-messaging]包含：</span><span class="sxs-lookup"><span data-stu-id="7ea38-106">An [IoT Hub message][lnk-messaging] consists of:</span></span>

* <span data-ttu-id="7ea38-107">一組 *系統屬性*。</span><span class="sxs-lookup"><span data-stu-id="7ea38-107">A set of *system properties*.</span></span> <span data-ttu-id="7ea38-108">IoT 中樞解譯或設定的屬性。</span><span class="sxs-lookup"><span data-stu-id="7ea38-108">Properties that IoT Hub interprets or sets.</span></span> <span data-ttu-id="7ea38-109">這個集合是預先決定的。</span><span class="sxs-lookup"><span data-stu-id="7ea38-109">This set is predetermined.</span></span>
* <span data-ttu-id="7ea38-110">一組 *應用程式屬性*。</span><span class="sxs-lookup"><span data-stu-id="7ea38-110">A set of *application properties*.</span></span> <span data-ttu-id="7ea38-111">字串 hello 應用程式可以定義的屬性與存取權，而不需要 toodeserialize hello 訊息本文的字典。</span><span class="sxs-lookup"><span data-stu-id="7ea38-111">A dictionary of string properties that hello application can define and access, without needing toodeserialize hello message body.</span></span> <span data-ttu-id="7ea38-112">IoT 中樞不會修改這些屬性。</span><span class="sxs-lookup"><span data-stu-id="7ea38-112">IoT Hub never modifies these properties.</span></span>
* <span data-ttu-id="7ea38-113">不透明的二進位主體。</span><span class="sxs-lookup"><span data-stu-id="7ea38-113">An opaque binary body.</span></span>

<span data-ttu-id="7ea38-114">在下列情況下，屬性名稱和值只能包含 ASCII 英數字元和 ``{'!', '#', '$', '%, '&', "'", '*', '*', '+', '-', '.', '^', '_', '`', '|', '~'}`\`：</span><span class="sxs-lookup"><span data-stu-id="7ea38-114">Property names and values can only contain ASCII alphanumeric characters, plus ``{'!', '#', '$', '%, '&', "'", '*', '*', '+', '-', '.', '^', '_', '`', '|', '~'}`\` when you:</span></span>

* <span data-ttu-id="7ea38-115">傳送使用 hello HTTP 通訊協定的裝置到雲端訊息。</span><span class="sxs-lookup"><span data-stu-id="7ea38-115">Send device-to-cloud messages using hello HTTP protocol.</span></span>
* <span data-ttu-id="7ea38-116">傳送雲端到裝置的訊息。</span><span class="sxs-lookup"><span data-stu-id="7ea38-116">Send cloud-to-device messages.</span></span>

<span data-ttu-id="7ea38-117">如需有關如何 tooencode 和解碼使用不同的通訊協定傳送訊息，請參閱[Azure IoT Sdk][lnk-sdks]。</span><span class="sxs-lookup"><span data-stu-id="7ea38-117">For more information about how tooencode and decode messages sent using different protocols, see [Azure IoT SDKs][lnk-sdks].</span></span>

<span data-ttu-id="7ea38-118">hello 下表列出 hello 的 IoT 中樞訊息中的系統屬性。</span><span class="sxs-lookup"><span data-stu-id="7ea38-118">hello following table lists hello set of system properties in IoT Hub messages.</span></span>

| <span data-ttu-id="7ea38-119">屬性</span><span class="sxs-lookup"><span data-stu-id="7ea38-119">Property</span></span> | <span data-ttu-id="7ea38-120">說明</span><span class="sxs-lookup"><span data-stu-id="7ea38-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7ea38-121">MessageId</span><span class="sxs-lookup"><span data-stu-id="7ea38-121">MessageId</span></span> |<span data-ttu-id="7ea38-122">Hello 訊息，要求-回覆模式使用使用者可設定識別項。</span><span class="sxs-lookup"><span data-stu-id="7ea38-122">A user-settable identifier for hello message used for request-reply patterns.</span></span> <span data-ttu-id="7ea38-123">格式： 區分大小寫字串 （向上 too128 字元） 的英數字元的 ASCII 7 位元 + `{'-', ':',’.', '+', '%', '_', '#', '*', '?', '!', '(', ')', ',', '=', '@', ';', '$', '''}`。</span><span class="sxs-lookup"><span data-stu-id="7ea38-123">Format: A case-sensitive string (up too128 characters long) of ASCII 7-bit alphanumeric characters + `{'-', ':',’.', '+', '%', '_', '#', '*', '?', '!', '(', ')', ',', '=', '@', ';', '$', '''}`.</span></span> |
| <span data-ttu-id="7ea38-124">序號</span><span class="sxs-lookup"><span data-stu-id="7ea38-124">Sequence number</span></span> |<span data-ttu-id="7ea38-125">數字 （每個裝置佇列唯一） 指派的 IoT 中樞 tooeach 雲端到裝置的訊息。</span><span class="sxs-lookup"><span data-stu-id="7ea38-125">A number (unique per device-queue) assigned by IoT Hub tooeach cloud-to-device message.</span></span> |
| <span data-ttu-id="7ea38-126">太</span><span class="sxs-lookup"><span data-stu-id="7ea38-126">too</span></span>|<span data-ttu-id="7ea38-127">[雲端到裝置][lnk-c2d]訊息中指定的目的地。</span><span class="sxs-lookup"><span data-stu-id="7ea38-127">A destination specified in [Cloud-to-Device][lnk-c2d] messages.</span></span> |
| <span data-ttu-id="7ea38-128">ExpiryTimeUtc</span><span class="sxs-lookup"><span data-stu-id="7ea38-128">ExpiryTimeUtc</span></span> |<span data-ttu-id="7ea38-129">訊息到期的日期和時間。</span><span class="sxs-lookup"><span data-stu-id="7ea38-129">Date and time of message expiration.</span></span> |
| <span data-ttu-id="7ea38-130">EnqueuedTime</span><span class="sxs-lookup"><span data-stu-id="7ea38-130">EnqueuedTime</span></span> |<span data-ttu-id="7ea38-131">日期和時間的 hello[雲端到裝置][ lnk-c2d] IoT 中心已接收訊息。</span><span class="sxs-lookup"><span data-stu-id="7ea38-131">Date and time hello [Cloud-to-Device][lnk-c2d] message was received by IoT Hub.</span></span> |
| <span data-ttu-id="7ea38-132">CorrelationId</span><span class="sxs-lookup"><span data-stu-id="7ea38-132">CorrelationId</span></span> |<span data-ttu-id="7ea38-133">通常包含 hello MessageId hello 要求，要求-回覆模式中的回應訊息中的字串屬性。</span><span class="sxs-lookup"><span data-stu-id="7ea38-133">A string property in a response message that typically contains hello MessageId of hello request, in request-reply patterns.</span></span> |
| <span data-ttu-id="7ea38-134">UserId</span><span class="sxs-lookup"><span data-stu-id="7ea38-134">UserId</span></span> |<span data-ttu-id="7ea38-135">使用 toospecify hello 訊息來源的識別碼。</span><span class="sxs-lookup"><span data-stu-id="7ea38-135">An ID used toospecify hello origin of messages.</span></span> <span data-ttu-id="7ea38-136">當訊息透過 IoT 中樞產生時，它會設定太`{iot hub name}`。</span><span class="sxs-lookup"><span data-stu-id="7ea38-136">When messages are generated by IoT Hub, it is set too`{iot hub name}`.</span></span> |
| <span data-ttu-id="7ea38-137">Ack</span><span class="sxs-lookup"><span data-stu-id="7ea38-137">Ack</span></span> |<span data-ttu-id="7ea38-138">意見反應訊息產生器。</span><span class="sxs-lookup"><span data-stu-id="7ea38-138">A feedback message generator.</span></span> <span data-ttu-id="7ea38-139">這個屬性是雲端到裝置訊息 toorequest IoT 中樞 toogenerate 意見反應在訊息中使用結果 hello 耗用量的 hello 訊息 hello 裝置。</span><span class="sxs-lookup"><span data-stu-id="7ea38-139">This property is used in cloud-to-device messages toorequest IoT Hub toogenerate feedback messages as a result of hello consumption of hello message by hello device.</span></span> <span data-ttu-id="7ea38-140">可能的值：**無**（預設值）： 不意見反應會產生訊息，**正數**: hello 訊息已完成，如果收到的意見反應**負數**： 接收如果沒有完成 hello 裝置 hello 訊息過期 （或已達到最大傳遞計數） 的意見反應訊息或**完整**： 正數和負數。</span><span class="sxs-lookup"><span data-stu-id="7ea38-140">Possible values: **none** (default): no feedback message is generated, **positive**: receive a feedback message if hello message was completed, **negative**: receive a feedback message if hello message expired (or maximum delivery count was reached) without being completed by hello device, or **full**: both positive and negative.</span></span> <span data-ttu-id="7ea38-141">若需詳細資訊，請參閱[訊息意見反應][lnk-feedback]。</span><span class="sxs-lookup"><span data-stu-id="7ea38-141">For more information, see [Message feedback][lnk-feedback].</span></span> |
| <span data-ttu-id="7ea38-142">ConnectionDeviceId</span><span class="sxs-lookup"><span data-stu-id="7ea38-142">ConnectionDeviceId</span></span> |<span data-ttu-id="7ea38-143">由 IoT 中樞在裝置到雲端訊息上設定的識別碼。</span><span class="sxs-lookup"><span data-stu-id="7ea38-143">An ID set by IoT Hub on device-to-cloud messages.</span></span> <span data-ttu-id="7ea38-144">它包含 hello **deviceId**的 hello 裝置傳送 hello 訊息。</span><span class="sxs-lookup"><span data-stu-id="7ea38-144">It contains hello **deviceId** of hello device that sent hello message.</span></span> |
| <span data-ttu-id="7ea38-145">ConnectionDeviceGenerationId</span><span class="sxs-lookup"><span data-stu-id="7ea38-145">ConnectionDeviceGenerationId</span></span> |<span data-ttu-id="7ea38-146">由 IoT 中樞在裝置到雲端訊息上設定的識別碼。</span><span class="sxs-lookup"><span data-stu-id="7ea38-146">An ID set by IoT Hub on device-to-cloud messages.</span></span> <span data-ttu-id="7ea38-147">它包含 hello **generationId** (根據[裝置身分識別屬性][lnk-device-properties]) 的 hello 裝置傳送 hello 訊息。</span><span class="sxs-lookup"><span data-stu-id="7ea38-147">It contains hello **generationId** (as per [Device identity properties][lnk-device-properties]) of hello device that sent hello message.</span></span> |
| <span data-ttu-id="7ea38-148">ConnectionAuthMethod</span><span class="sxs-lookup"><span data-stu-id="7ea38-148">ConnectionAuthMethod</span></span> |<span data-ttu-id="7ea38-149">由 IoT 中樞在裝置到雲端訊息上設定的驗證方法。</span><span class="sxs-lookup"><span data-stu-id="7ea38-149">An authentication method set by IoT Hub on device-to-cloud messages.</span></span> <span data-ttu-id="7ea38-150">此屬性包含 hello 驗證方法使用 tooauthenticate hello 裝置傳送 hello 訊息的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="7ea38-150">This property contains information about hello authentication method used tooauthenticate hello device sending hello message.</span></span> <span data-ttu-id="7ea38-151">如需詳細資訊，請參閱[裝置 toocloud 的防詐騙功能][lnk-antispoofing]。</span><span class="sxs-lookup"><span data-stu-id="7ea38-151">For more information, see [Device toocloud anti-spoofing][lnk-antispoofing].</span></span> |

## <a name="message-size"></a><span data-ttu-id="7ea38-152">訊息大小</span><span class="sxs-lookup"><span data-stu-id="7ea38-152">Message size</span></span>

<span data-ttu-id="7ea38-153">IoT 中樞測量訊息大小無從驗證通訊協定的方式，考慮只有 hello 實際的承載。</span><span class="sxs-lookup"><span data-stu-id="7ea38-153">IoT Hub measures message size in a protocol-agnostic way, considering only hello actual payload.</span></span> <span data-ttu-id="7ea38-154">hello 大小 （位元組） 會計算為 hello hello 下列總和：</span><span class="sxs-lookup"><span data-stu-id="7ea38-154">hello size in bytes is calculated as hello sum of hello following:</span></span>

* <span data-ttu-id="7ea38-155">hello 本文大小 （位元組）。</span><span class="sxs-lookup"><span data-stu-id="7ea38-155">hello body size in bytes.</span></span>
* <span data-ttu-id="7ea38-156">hello 大小 （位元組） 的所有 hello 值 hello 訊息系統屬性。</span><span class="sxs-lookup"><span data-stu-id="7ea38-156">hello size in bytes of all hello values of hello message system properties.</span></span>
* <span data-ttu-id="7ea38-157">hello 大小 （位元組） 的所有使用者的屬性名稱和值。</span><span class="sxs-lookup"><span data-stu-id="7ea38-157">hello size in bytes of all user property names and values.</span></span>

<span data-ttu-id="7ea38-158">屬性名稱和值都是有限的 tooASCII 字元，因此 hello 字串 hello 長度等於 hello 大小 （位元組）。</span><span class="sxs-lookup"><span data-stu-id="7ea38-158">Property names and values are limited tooASCII characters, so hello length of hello strings equals hello size in bytes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7ea38-159">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7ea38-159">Next steps</span></span>

<span data-ttu-id="7ea38-160">如需 IoT 中樞訊息大小限制的資訊，請參閱 [IoT 中樞配額和節流][lnk-quotas]。</span><span class="sxs-lookup"><span data-stu-id="7ea38-160">For information about message size limits in IoT Hub, see [IoT Hub quotas and throttling][lnk-quotas].</span></span>

<span data-ttu-id="7ea38-161">toolearn 如何 toocreate 和讀取的 IoT 中樞訊息不同的程式語言，請參閱 hello[開始][ lnk-get-started]教學課程。</span><span class="sxs-lookup"><span data-stu-id="7ea38-161">toolearn how toocreate and read IoT Hub messages in various programming languages, see hello [Get started][lnk-get-started] tutorials.</span></span>

[lnk-messaging]: iot-hub-devguide-messaging.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-get-started]: iot-hub-get-started.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-c2d]: iot-hub-devguide-messages-c2d.md
[lnk-d2c]: iot-hub-devguide-messages-d2c.md
[lnk-feedback]: iot-hub-devguide-messages-c2d.md#message-feedback
[lnk-device-properties]: iot-hub-devguide-identity-registry.md#device-identity-properties
[lnk-antispoofing]: iot-hub-devguide-messages-d2c.md#anti-spoofing-properties
