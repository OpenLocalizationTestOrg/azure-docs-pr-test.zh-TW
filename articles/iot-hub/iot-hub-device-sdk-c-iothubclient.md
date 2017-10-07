---
title: "c-IoTHubClient aaaAzure IoT 裝置 SDK |Microsoft 文件"
description: "如何在 C toocreate 裝置應用程式的 hello Azure IoT 裝置 SDK toouse hello IoTHubClient 程式庫進行通訊的與 IoT 中樞。"
services: iot-hub
documentationcenter: 
author: olivierbloch
manager: timlt
editor: 
ms.assetid: 828cf2bf-999d-4b8a-8a28-c7c901629600
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/06/2016
ms.author: obloch
ms.openlocfilehash: d1ece79e9ba6d1e5fd45cabb8fca393b24052e07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-device-sdk-for-c--more-about-iothubclient"></a><span data-ttu-id="f693e-103">適用於 C 的 Azure IoT 裝置 SDK - 深入了解 IoTHubClient</span><span class="sxs-lookup"><span data-stu-id="f693e-103">Azure IoT device SDK for C – more about IoTHubClient</span></span>
<span data-ttu-id="f693e-104">hello[先文章](iot-hub-device-sdk-c-intro.md)中這個數列導入 hello **C 的 Azure IoT 裝置 SDK**。該文章已說明 SDK 中有兩個架構層。</span><span class="sxs-lookup"><span data-stu-id="f693e-104">hello [first article](iot-hub-device-sdk-c-intro.md) in this series introduced hello **Azure IoT device SDK for C**. That article explained that there are two architectural layers in SDK.</span></span> <span data-ttu-id="f693e-105">在 [hello 基底 hello **IoTHubClient**可直接管理與 IoT 中樞通訊的程式庫。</span><span class="sxs-lookup"><span data-stu-id="f693e-105">At hello base is hello **IoTHubClient** library which directly manages communication with IoT Hub.</span></span> <span data-ttu-id="f693e-106">另外還有 hello**序列化程式**在該組建 tooprovide 序列化服務的程式庫。</span><span class="sxs-lookup"><span data-stu-id="f693e-106">There's also hello **serializer** library that builds on top of that tooprovide serialization services.</span></span> <span data-ttu-id="f693e-107">本文章中我們將提供其他詳細資料上 hello **IoTHubClient**程式庫。</span><span class="sxs-lookup"><span data-stu-id="f693e-107">In this article we'll provide additional detail on hello **IoTHubClient** library.</span></span>

<span data-ttu-id="f693e-108">hello 前一篇文章所述方式 toouse hello **IoTHubClient**文件庫 toosend 事件 tooIoT 中樞和接收訊息。</span><span class="sxs-lookup"><span data-stu-id="f693e-108">hello previous article described how toouse hello **IoTHubClient** library toosend events tooIoT Hub and receive messages.</span></span> <span data-ttu-id="f693e-109">這篇文章解釋 toomore 精確地管理已延伸，討論*時*您傳送和接收資料，引入您 toohello**較低層級 Api**。</span><span class="sxs-lookup"><span data-stu-id="f693e-109">This article extends that discussion by explaining how toomore precisely manage *when* you send and receive data, introducing you toohello **lower-level APIs**.</span></span> <span data-ttu-id="f693e-110">我們也將說明如何 tooattach 屬性 tooevents （和擷取訊息） 使用 hello 屬性處理 hello 的功能**IoTHubClient**程式庫。</span><span class="sxs-lookup"><span data-stu-id="f693e-110">We'll also explain how tooattach properties tooevents (and retrieve them from messages) using hello property handling features in hello **IoTHubClient** library.</span></span> <span data-ttu-id="f693e-111">最後，我們將提供詳細說明不同的方式 toohandle 從 IoT 中樞接收的訊息。</span><span class="sxs-lookup"><span data-stu-id="f693e-111">Finally, we'll provide additional explanation of different ways toohandle messages received from IoT Hub.</span></span>

<span data-ttu-id="f693e-112">hello 文章結束時，會涵蓋數個其他的主題，包括裝置認證有關的詳細資訊和如何 toochange hello 行為 hello **IoTHubClient**透過組態選項。</span><span class="sxs-lookup"><span data-stu-id="f693e-112">hello article concludes by covering a couple of miscellaneous topics, including more about device credentials and how toochange hello behavior of hello **IoTHubClient** through configuration options.</span></span>

<span data-ttu-id="f693e-113">我們將使用 hello **IoTHubClient** SDK 範例 tooexplain 這些主題。</span><span class="sxs-lookup"><span data-stu-id="f693e-113">We'll use hello **IoTHubClient** SDK samples tooexplain these topics.</span></span> <span data-ttu-id="f693e-114">如果您想沿著 toofollow，請參閱 hello **iot 中樞\_用戶端\_範例\_http**和**iot 中樞\_用戶端\_範例\_amqp** hello Azure IoT 裝置 SDK 中包含的這些範例會示範 c 的所有項目 hello 下列各節中所述的應用程式。</span><span class="sxs-lookup"><span data-stu-id="f693e-114">If you want toofollow along, see hello **iothub\_client\_sample\_http** and **iothub\_client\_sample\_amqp** applications that are included in hello Azure IoT device SDK for C. Everything described in hello following sections is demonstrated in these samples.</span></span>

<span data-ttu-id="f693e-115">您可以找到 hello [ **C 的 Azure IoT 裝置 SDK** ](https://github.com/Azure/azure-iot-sdk-c) GitHub 儲存機制和檢視詳細資料的 hello API 在 hello [C 應用程式開發介面參考](https://azure.github.io/azure-iot-sdk-c/index.html)。</span><span class="sxs-lookup"><span data-stu-id="f693e-115">You can find hello [**Azure IoT device SDK for C**](https://github.com/Azure/azure-iot-sdk-c) GitHub repository and view details of hello API in hello [C API reference](https://azure.github.io/azure-iot-sdk-c/index.html).</span></span>

## <a name="hello-lower-level-apis"></a><span data-ttu-id="f693e-116">hello 較低層級應用程式開發介面</span><span class="sxs-lookup"><span data-stu-id="f693e-116">hello lower-level APIs</span></span>
<span data-ttu-id="f693e-117">hello 前一篇文章所述的 hello hello 基本作業**IotHubClient** hello hello 內容中**iot 中樞\_用戶端\_範例\_amqp**應用程式。</span><span class="sxs-lookup"><span data-stu-id="f693e-117">hello previous article described hello basic operation of hello **IotHubClient** within hello context of hello **iothub\_client\_sample\_amqp** application.</span></span> <span data-ttu-id="f693e-118">比方說，它會說明如何 tooinitialize hello 使用此程式碼的程式庫。</span><span class="sxs-lookup"><span data-stu-id="f693e-118">For example, it explained how tooinitialize hello library using this code.</span></span>

```
IOTHUB_CLIENT_HANDLE iotHubClientHandle;
iotHubClientHandle = IoTHubClient_CreateFromConnectionString(connectionString, AMQP_Protocol);
```

<span data-ttu-id="f693e-119">它也說明如何使用這個 toosend 事件函式呼叫。</span><span class="sxs-lookup"><span data-stu-id="f693e-119">It also described how toosend events using this function call.</span></span>

```
IoTHubClient_SendEventAsync(iotHubClientHandle, message.messageHandle, SendConfirmationCallback, &message);
```

<span data-ttu-id="f693e-120">hello 同時也說明 tooreceive 藉由註冊回呼函式的訊息。</span><span class="sxs-lookup"><span data-stu-id="f693e-120">hello article also described how tooreceive messages by registering a callback function.</span></span>

```
int receiveContext = 0;
IoTHubClient_SetMessageCallback(iotHubClientHandle, ReceiveMessageCallback, &receiveContext);
```

<span data-ttu-id="f693e-121">hello 發行項也會示範使用 toofree 資源 hello 如下的程式碼。</span><span class="sxs-lookup"><span data-stu-id="f693e-121">hello article also showed how toofree resources using code such as hello following.</span></span>

```
IoTHubClient_Destroy(iotHubClientHandle);
```

<span data-ttu-id="f693e-122">但是有附屬的這些 Api 的函式 tooeach:</span><span class="sxs-lookup"><span data-stu-id="f693e-122">However there are companion functions tooeach of these APIs:</span></span>

* <span data-ttu-id="f693e-123">IoTHubClient\_LL\_CreateFromConnectionString</span><span class="sxs-lookup"><span data-stu-id="f693e-123">IoTHubClient\_LL\_CreateFromConnectionString</span></span>
* <span data-ttu-id="f693e-124">IoTHubClient\_LL\_SendEventAsync</span><span class="sxs-lookup"><span data-stu-id="f693e-124">IoTHubClient\_LL\_SendEventAsync</span></span>
* <span data-ttu-id="f693e-125">IoTHubClient\_LL\_SetMessageCallback</span><span class="sxs-lookup"><span data-stu-id="f693e-125">IoTHubClient\_LL\_SetMessageCallback</span></span>
* <span data-ttu-id="f693e-126">IoTHubClient\_LL\_Destroy</span><span class="sxs-lookup"><span data-stu-id="f693e-126">IoTHubClient\_LL\_Destroy</span></span>

<span data-ttu-id="f693e-127">所有這些函式 hello API 名稱中包含"LL"。</span><span class="sxs-lookup"><span data-stu-id="f693e-127">These functions all include “LL” in hello API name.</span></span> <span data-ttu-id="f693e-128">除此之外，其他每一個這些函式的 hello 參數都是相同 tootheir 非 LL 對應項目。</span><span class="sxs-lookup"><span data-stu-id="f693e-128">Other than that, hello parameters of each of these functions are identical tootheir non-LL counterparts.</span></span> <span data-ttu-id="f693e-129">不過，這些函式的 hello 行為不相同，有一項重要的。</span><span class="sxs-lookup"><span data-stu-id="f693e-129">However, hello behavior of these functions is different in one important way.</span></span>

<span data-ttu-id="f693e-130">當您呼叫**IoTHubClient\_CreateFromConnectionString**，hello 基礎程式庫建立新的執行緒 hello 背景中執行。</span><span class="sxs-lookup"><span data-stu-id="f693e-130">When you call **IoTHubClient\_CreateFromConnectionString**, hello underlying libraries create a new thread that runs in hello background.</span></span> <span data-ttu-id="f693e-131">此執行緒會將事件傳送到 IoT 中樞以及接收其訊息。</span><span class="sxs-lookup"><span data-stu-id="f693e-131">This thread sends events to, and receives messages from, IoT Hub.</span></span> <span data-ttu-id="f693e-132">使用 hello"LL"應用程式開發介面時，會建立沒有這類執行緒。</span><span class="sxs-lookup"><span data-stu-id="f693e-132">No such thread is created when working with hello "LL" APIs.</span></span> <span data-ttu-id="f693e-133">hello 建立 hello 背景執行緒是方便 toohello 開發人員。</span><span class="sxs-lookup"><span data-stu-id="f693e-133">hello creation of hello background thread is a convenience toohello developer.</span></span> <span data-ttu-id="f693e-134">您不需要明確地將事件傳送和接收訊息從 IoT 中樞-它在 hello 背景中自動進行有關 tooworry。</span><span class="sxs-lookup"><span data-stu-id="f693e-134">You don’t have tooworry about explicitly sending events and receiving messages from IoT Hub -- it happens automatically in hello background.</span></span> <span data-ttu-id="f693e-135">相反地，hello"LL"應用程式開發介面可讓您明確掌控與 IoT 中樞通訊如有需要。</span><span class="sxs-lookup"><span data-stu-id="f693e-135">In contrast, hello "LL" APIs give you explicit control over communication with IoT Hub, if you need it.</span></span>

<span data-ttu-id="f693e-136">toounderstand 這個較好，讓我們來看一個範例：</span><span class="sxs-lookup"><span data-stu-id="f693e-136">toounderstand this better, let’s look at an example:</span></span>

<span data-ttu-id="f693e-137">當您呼叫**IoTHubClient\_SendEventAsync**，您正在實際做什麼 hello 事件放在緩衝區中。</span><span class="sxs-lookup"><span data-stu-id="f693e-137">When you call **IoTHubClient\_SendEventAsync**, what you're actually doing is putting hello event in a buffer.</span></span> <span data-ttu-id="f693e-138">hello 背景執行緒呼叫時建立**IoTHubClient\_CreateFromConnectionString**持續監視這個緩衝區，並傳送任何資料，它包含 tooIoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="f693e-138">hello background thread created when you call **IoTHubClient\_CreateFromConnectionString** continually monitors this buffer and sends any data that it contains tooIoT Hub.</span></span> <span data-ttu-id="f693e-139">發生這種情況在 hello hello 背景中相同時間該 hello 主執行緒所執行的其他工作。</span><span class="sxs-lookup"><span data-stu-id="f693e-139">This happens in hello background at hello same time that hello main thread is performing other work.</span></span>

<span data-ttu-id="f693e-140">同樣地，當您註冊的回呼函式，以訊息**IoTHubClient\_SetMessageCallback**，您要指示 hello SDK toohave hello 背景執行緒會將訊息時，叫用 hello 回呼函式接收獨立的 hello 主執行緒。</span><span class="sxs-lookup"><span data-stu-id="f693e-140">Similarly, when you register a callback function for messages using **IoTHubClient\_SetMessageCallback**, you're instructing hello SDK toohave hello background thread invoke hello callback function when a message is received, independent of hello main thread.</span></span>

<span data-ttu-id="f693e-141">背景執行緒時，請勿建立 hello"LL"應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="f693e-141">hello "LL" APIs don’t create a background thread.</span></span> <span data-ttu-id="f693e-142">相反地，新的 API，必須先呼叫 tooexplicitly 傳送和接收來自 IoT 中樞的資料。</span><span class="sxs-lookup"><span data-stu-id="f693e-142">Instead, a new API must be called tooexplicitly send and receive data from IoT Hub.</span></span> <span data-ttu-id="f693e-143">Hello 下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="f693e-143">This is demonstrated in hello following example.</span></span>

<span data-ttu-id="f693e-144">hello **iot 中樞\_用戶端\_範例\_http** hello 示範 SDK 中隨附的應用程式 hello 較低層級應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="f693e-144">hello **iothub\_client\_sample\_http** application that’s included in hello SDK demonstrates hello lower-level APIs.</span></span> <span data-ttu-id="f693e-145">在該範例中，我們會傳送事件 tooIoT 集線器與 hello 如下的程式碼：</span><span class="sxs-lookup"><span data-stu-id="f693e-145">In that sample, we send events tooIoT Hub with code such as hello following:</span></span>

```
EVENT_INSTANCE message;
sprintf_s(msgText, sizeof(msgText), "Message_%d_From_IoTHubClient_LL_Over_HTTP", i);
message.messageHandle = IoTHubMessage_CreateFromByteArray((const unsigned char*)msgText, strlen(msgText));

IoTHubClient_LL_SendEventAsync(iotHubClientHandle, message.messageHandle, SendConfirmationCallback, &message)
```

<span data-ttu-id="f693e-146">hello 前三行建立 hello 訊息和 hello 最後一行會傳送 hello 事件。</span><span class="sxs-lookup"><span data-stu-id="f693e-146">hello first three lines create hello message, and hello last line sends hello event.</span></span> <span data-ttu-id="f693e-147">不過，如先前所述，「 傳送 」 hello 事件表示 hello 資料只會置於緩衝區。</span><span class="sxs-lookup"><span data-stu-id="f693e-147">However, as mentioned previously, "sending" hello event means that hello data is simply placed in a buffer.</span></span> <span data-ttu-id="f693e-148">執行任何動作會當我們呼叫 hello 網路上傳輸**IoTHubClient\_LL\_SendEventAsync**。</span><span class="sxs-lookup"><span data-stu-id="f693e-148">Nothing is transmitted on hello network when we call **IoTHubClient\_LL\_SendEventAsync**.</span></span> <span data-ttu-id="f693e-149">在訂單 tooactually 輸入 hello 資料 tooIoT 中樞，您必須呼叫**IoTHubClient\_LL\_DoWork**，如這個範例所示：</span><span class="sxs-lookup"><span data-stu-id="f693e-149">In order tooactually ingress hello data tooIoT Hub, you must call **IoTHubClient\_LL\_DoWork**, as in this example:</span></span>

```
while (1)
{
    IoTHubClient_LL_DoWork(iotHubClientHandle);
    ThreadAPI_Sleep(1000);
}
```

<span data-ttu-id="f693e-150">此程式碼 (從 hello **iot 中樞\_用戶端\_範例\_http**應用程式) 重複呼叫**IoTHubClient\_LL\_DoWork**.</span><span class="sxs-lookup"><span data-stu-id="f693e-150">This code (from hello **iothub\_client\_sample\_http** application) repeatedly calls **IoTHubClient\_LL\_DoWork**.</span></span> <span data-ttu-id="f693e-151">每次**IoTHubClient\_LL\_DoWork**是呼叫，從 hello 緩衝區 tooIoT 中樞傳送某些事件，而且它會擷取佇列的訊息傳送 toohello 裝置。</span><span class="sxs-lookup"><span data-stu-id="f693e-151">Each time **IoTHubClient\_LL\_DoWork** is called, it sends some events from hello buffer tooIoT Hub and it retrieves a queued message being sent toohello device.</span></span> <span data-ttu-id="f693e-152">hello 後者的情況下表示，如果我們註冊回呼函式的訊息，然後 hello 會叫用回呼 （假設任何訊息的佇列）。</span><span class="sxs-lookup"><span data-stu-id="f693e-152">hello latter case means that if we registered a callback function for messages, then hello callback is invoked (assuming any messages are queued up).</span></span> <span data-ttu-id="f693e-153">我們會註冊這類的回呼函式與 hello 如下的程式碼：</span><span class="sxs-lookup"><span data-stu-id="f693e-153">We would have registered such a callback function with code such as hello following:</span></span>

```
IoTHubClient_LL_SetMessageCallback(iotHubClientHandle, ReceiveMessageCallback, &receiveContext)
```

<span data-ttu-id="f693e-154">hello 原因**IoTHubClient\_LL\_DoWork**通常稱為迴圈是每次呼叫時，它會傳送*某些*緩衝事件 tooIoT 中樞並擷取*接下來 hello*訊息佇列中等待 hello 裝置。</span><span class="sxs-lookup"><span data-stu-id="f693e-154">hello reason that **IoTHubClient\_LL\_DoWork** is often called in a loop is that each time it’s called, it sends *some* buffered events tooIoT Hub and retrieves *hello next* message queued up for hello device.</span></span> <span data-ttu-id="f693e-155">每個呼叫不保證 toosend 所有經過緩衝處理的事件或 tooretrieve 所有排入佇列的訊息。</span><span class="sxs-lookup"><span data-stu-id="f693e-155">Each call isn’t guaranteed toosend all buffered events or tooretrieve all queued messages.</span></span> <span data-ttu-id="f693e-156">如果您想的 toosend hello 中的所有事件緩衝區，然後繼續執行上其他處理此迴圈可以取代 hello 如下的程式碼：</span><span class="sxs-lookup"><span data-stu-id="f693e-156">If you want toosend all events in hello buffer and then continue on with other processing you can replace this loop with code such as hello following:</span></span>

```
IOTHUB_CLIENT_STATUS status;

while ((IoTHubClient_LL_GetSendStatus(iotHubClientHandle, &status) == IOTHUB_CLIENT_OK) && (status == IOTHUB_CLIENT_SEND_STATUS_BUSY))
{
    IoTHubClient_LL_DoWork(iotHubClientHandle);
    ThreadAPI_Sleep(1000);
}
```

<span data-ttu-id="f693e-157">此程式碼會呼叫**IoTHubClient\_LL\_DoWork**之前已傳送嗨緩衝區中的所有事件 tooIoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="f693e-157">This code calls **IoTHubClient\_LL\_DoWork** until all events in hello buffer have been sent tooIoT Hub.</span></span> <span data-ttu-id="f693e-158">請注意，這並未一併暗示已收到所有佇列的訊息。</span><span class="sxs-lookup"><span data-stu-id="f693e-158">Note this does not also imply that all queued messages have been received.</span></span> <span data-ttu-id="f693e-159">部分 hello 這個錯誤是原因的，檢查 「 全部 」 的訊息不會為具決定性的動作。</span><span class="sxs-lookup"><span data-stu-id="f693e-159">Part of hello reason for this is that checking for "all" messages isn’t as deterministic an action.</span></span> <span data-ttu-id="f693e-160">如果您擷取"all"hello 訊息，但另一個然後傳送 toohello 裝置，會發生什麼情況之後立即？</span><span class="sxs-lookup"><span data-stu-id="f693e-160">What happens if you retrieve "all" of hello messages, but then another one is sent toohello device immediately after?</span></span> <span data-ttu-id="f693e-161">與更好的方式 toodeal 是經過程式設計逾時。</span><span class="sxs-lookup"><span data-stu-id="f693e-161">A better way toodeal with that is with a programmed timeout.</span></span> <span data-ttu-id="f693e-162">例如，hello 訊息回呼函式無法重設的計時器，每次叫用它。</span><span class="sxs-lookup"><span data-stu-id="f693e-162">For example, hello message callback function could reset a timer every time it’s invoked.</span></span> <span data-ttu-id="f693e-163">然後您可以撰寫邏輯 toocontinue 處理，例如，沒有訊息所收到的 hello 上次*X*秒。</span><span class="sxs-lookup"><span data-stu-id="f693e-163">You can then write logic toocontinue processing if, for example, no messages have been received in hello last *X* seconds.</span></span>

<span data-ttu-id="f693e-164">當您在完成的 ingressing 事件，並接收訊息，是確定 toocall hello 對應函式 tooclean 資源。</span><span class="sxs-lookup"><span data-stu-id="f693e-164">When you’re finished ingressing events and receiving messages, be sure toocall hello corresponding function tooclean up resources.</span></span>

```
IoTHubClient_LL_Destroy(iotHubClientHandle);
```

<span data-ttu-id="f693e-165">基本上是只有一組 Api toosend 利用背景執行緒與另一組 Api，並 hello hello 背景執行緒沒有相同的動作和接收資料。</span><span class="sxs-lookup"><span data-stu-id="f693e-165">Basically there’s only one set of APIs toosend and receive data with a background thread and another set of APIs that does hello same thing without hello background thread.</span></span> <span data-ttu-id="f693e-166">許多開發人員可能偏好使用 hello 非-LL Api，但 hello 較低層級 Api 時很有用 hello 開發人員想要明確控制網路傳輸。</span><span class="sxs-lookup"><span data-stu-id="f693e-166">A lot of developers may prefer hello non-LL APIs, but hello lower-level APIs are useful when hello developer wants explicit control over network transmissions.</span></span> <span data-ttu-id="f693e-167">例如，有些裝置會隨時間收集資料，並且只在指定的時間間隔輸入事件 (例如，每小時一次或一天一次)。</span><span class="sxs-lookup"><span data-stu-id="f693e-167">For example, some devices collect data over time and only ingress events at specified intervals (for example, once an hour or once a day).</span></span> <span data-ttu-id="f693e-168">hello 較低層級應用程式開發介面提供當您傳送和接收資料，或從 IoT 中樞時，hello 能力 tooexplicitly 控制項。</span><span class="sxs-lookup"><span data-stu-id="f693e-168">hello lower-level APIs give you hello ability tooexplicitly control when you send and receive data from IoT Hub.</span></span> <span data-ttu-id="f693e-169">其他人只會偏好 hello 簡化較低層級 Api，提供該 hello。</span><span class="sxs-lookup"><span data-stu-id="f693e-169">Others will simply prefer hello simplicity that hello lower-level APIs provide.</span></span> <span data-ttu-id="f693e-170">Hello 主執行緒，而不是在 hello 背景某些工作發生的所有項目會發生。</span><span class="sxs-lookup"><span data-stu-id="f693e-170">Everything happens on hello main thread rather than some work happening in hello background.</span></span>

<span data-ttu-id="f693e-171">您選擇，無論模型是確定 toobe 一致的應用程式開發介面中使用。</span><span class="sxs-lookup"><span data-stu-id="f693e-171">Whichever model you choose, be sure toobe consistent in which APIs you use.</span></span> <span data-ttu-id="f693e-172">如果您藉由呼叫啟動**IoTHubClient\_LL\_CreateFromConnectionString**，確定您只使用 hello 對應較低層級 Api，任何後續追蹤的工作：</span><span class="sxs-lookup"><span data-stu-id="f693e-172">If you start by calling **IoTHubClient\_LL\_CreateFromConnectionString**, be sure you only use hello corresponding lower-level APIs for any follow-up work:</span></span>

* <span data-ttu-id="f693e-173">IoTHubClient\_LL\_SendEventAsync</span><span class="sxs-lookup"><span data-stu-id="f693e-173">IoTHubClient\_LL\_SendEventAsync</span></span>
* <span data-ttu-id="f693e-174">IoTHubClient\_LL\_SetMessageCallback</span><span class="sxs-lookup"><span data-stu-id="f693e-174">IoTHubClient\_LL\_SetMessageCallback</span></span>
* <span data-ttu-id="f693e-175">IoTHubClient\_LL\_Destroy</span><span class="sxs-lookup"><span data-stu-id="f693e-175">IoTHubClient\_LL\_Destroy</span></span>
* <span data-ttu-id="f693e-176">IoTHubClient\_LL\_DoWork</span><span class="sxs-lookup"><span data-stu-id="f693e-176">IoTHubClient\_LL\_DoWork</span></span>

<span data-ttu-id="f693e-177">相反的 hello 也是如此。</span><span class="sxs-lookup"><span data-stu-id="f693e-177">hello opposite is true as well.</span></span> <span data-ttu-id="f693e-178">如果您開始使用**IoTHubClient\_CreateFromConnectionString**，然後使用 hello 非-LL Api 進行任何其他處理。</span><span class="sxs-lookup"><span data-stu-id="f693e-178">If you start with **IoTHubClient\_CreateFromConnectionString**, then use hello non-LL APIs for any additional processing.</span></span>

<span data-ttu-id="f693e-179">在 [hello Azure IoT 裝置 SDK c，請參閱 hello **iot 中樞\_用戶端\_範例\_http** hello 的完整範例應用程式較低層級應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="f693e-179">In hello Azure IoT device SDK for C, see hello **iothub\_client\_sample\_http** application for a complete example of hello lower-level APIs.</span></span> <span data-ttu-id="f693e-180">hello **iot 中樞\_用戶端\_範例\_amqp**應用程式可以如需完整範例的 hello 非-LL 應用程式開發介面參考。</span><span class="sxs-lookup"><span data-stu-id="f693e-180">hello **iothub\_client\_sample\_amqp** application can be referenced for a full example of hello non-LL APIs.</span></span>

## <a name="property-handling"></a><span data-ttu-id="f693e-181">屬性處理</span><span class="sxs-lookup"><span data-stu-id="f693e-181">Property handling</span></span>
<span data-ttu-id="f693e-182">到目前為止我們已說明傳送資料，我們已被參照 toohello hello 訊息本文。</span><span class="sxs-lookup"><span data-stu-id="f693e-182">So far when we've described sending data, we've been referring toohello body of hello message.</span></span> <span data-ttu-id="f693e-183">例如，請思考下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="f693e-183">For example, consider this code:</span></span>

```
EVENT_INSTANCE message;
sprintf_s(msgText, sizeof(msgText), "Hello World");
message.messageHandle = IoTHubMessage_CreateFromByteArray((const unsigned char*)msgText, strlen(msgText));
IoTHubClient_LL_SendEventAsync(iotHubClientHandle, message.messageHandle, SendConfirmationCallback, &message)
```

<span data-ttu-id="f693e-184">這個範例會傳送訊息 tooIoT 集線器與 hello 文字"Hello World"。</span><span class="sxs-lookup"><span data-stu-id="f693e-184">This example sends a message tooIoT Hub with hello text "Hello World."</span></span> <span data-ttu-id="f693e-185">不過，IoT 中樞也可讓屬性 toobe 附加的 tooeach 訊息。</span><span class="sxs-lookup"><span data-stu-id="f693e-185">However, IoT Hub also allows properties toobe attached tooeach message.</span></span> <span data-ttu-id="f693e-186">屬性是可附加的 toohello 訊息的名稱/值組。</span><span class="sxs-lookup"><span data-stu-id="f693e-186">Properties are name/value pairs that can be attached toohello message.</span></span> <span data-ttu-id="f693e-187">例如，我們可以修改前一個程式碼 tooattach hello 屬性 toohello 訊息：</span><span class="sxs-lookup"><span data-stu-id="f693e-187">For example, we can modify hello previous code tooattach a property toohello message:</span></span>

```
MAP_HANDLE propMap = IoTHubMessage_Properties(message.messageHandle);
sprintf_s(propText, sizeof(propText), "%d", i);
Map_AddOrUpdate(propMap, "SequenceNumber", propText);
```

<span data-ttu-id="f693e-188">我們一開始呼叫**IoTHubMessage\_屬性**並將其傳遞訊息的 hello 控制代碼。</span><span class="sxs-lookup"><span data-stu-id="f693e-188">We start by calling **IoTHubMessage\_Properties** and passing it hello handle of our message.</span></span> <span data-ttu-id="f693e-189">我們會得到回**對應\_處理**可讓我們 toostart 加入屬性的參考。</span><span class="sxs-lookup"><span data-stu-id="f693e-189">What we get back is a **MAP\_HANDLE** reference that enables us toostart adding properties.</span></span> <span data-ttu-id="f693e-190">後者的 hello 伴隨著呼叫**對應\_AddOrUpdate**，其可接受參考 tooa 對應\_控制代碼、 hello 屬性名稱，以及 hello 屬性值。</span><span class="sxs-lookup"><span data-stu-id="f693e-190">hello latter is accomplished by calling **Map\_AddOrUpdate**, which takes a reference tooa MAP\_HANDLE, hello property name, and hello property value.</span></span> <span data-ttu-id="f693e-191">利用此 API，我們可以依意願新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="f693e-191">With this API we can add as many properties as we like.</span></span>

<span data-ttu-id="f693e-192">從讀取 hello 事件時**事件中心**，hello 接收者可以列舉 hello 屬性並擷取其對應的值。</span><span class="sxs-lookup"><span data-stu-id="f693e-192">When hello event is read from **Event Hubs**, hello receiver can enumerate hello properties and retrieve their corresponding values.</span></span> <span data-ttu-id="f693e-193">例如，在.NET 中達成這點會藉由存取 hello [hello EventData 物件上的屬性集合](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.eventdata.properties.aspx)。</span><span class="sxs-lookup"><span data-stu-id="f693e-193">For example, in .NET this would be accomplished by accessing hello [Properties collection on hello EventData object](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.eventdata.properties.aspx).</span></span>

<span data-ttu-id="f693e-194">在 hello 前一個範例中，我們正在將附加我們傳送給 tooIoT 中樞屬性 tooan 事件。</span><span class="sxs-lookup"><span data-stu-id="f693e-194">In hello previous example, we’re attaching properties tooan event that we send tooIoT Hub.</span></span> <span data-ttu-id="f693e-195">屬性也可以附加的 toomessages 接收從 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="f693e-195">Properties can also be attached toomessages received from IoT Hub.</span></span> <span data-ttu-id="f693e-196">如果我們想要從訊息 tooretrieve 屬性，我們可以使用我們訊息回呼函式中的 hello 如下的程式碼：</span><span class="sxs-lookup"><span data-stu-id="f693e-196">If we want tooretrieve properties from a message, we can use code such as hello following in our message callback function:</span></span>

```
static IOTHUBMESSAGE_DISPOSITION_RESULT ReceiveMessageCallback(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    . . .

    // Retrieve properties from hello message
    MAP_HANDLE mapProperties = IoTHubMessage_Properties(message);
    if (mapProperties != NULL)
    {
        const char*const* keys;
        const char*const* values;
        size_t propertyCount = 0;
        if (Map_GetInternals(mapProperties, &keys, &values, &propertyCount) == MAP_OK)
        {
            if (propertyCount > 0)
            {
                printf("Message Properties:\r\n");
                for (size_t index = 0; index < propertyCount; index++)
                {
                    printf("\tKey: %s Value: %s\r\n", keys[index], values[index]);
                }
                printf("\r\n");
            }
        }
    }

    . . .
}
```

<span data-ttu-id="f693e-197">太 hello 呼叫**IoTHubMessage\_屬性**傳回 hello**對應\_處理**參考。</span><span class="sxs-lookup"><span data-stu-id="f693e-197">hello call too**IoTHubMessage\_Properties** returns hello **MAP\_HANDLE** reference.</span></span> <span data-ttu-id="f693e-198">我們再傳遞該參考太**對應\_GetInternals** tooobtain hello 名稱/值的參考 tooan 陣列配對 （以及 hello 屬性的計數）。</span><span class="sxs-lookup"><span data-stu-id="f693e-198">We then pass that reference too**Map\_GetInternals** tooobtain a reference tooan array of hello name/value pairs (as well as a count of hello properties).</span></span> <span data-ttu-id="f693e-199">此時，它是列舉 hello 屬性 tooget toohello 值我們想要的簡單方式。</span><span class="sxs-lookup"><span data-stu-id="f693e-199">At that point it's a simple matter of enumerating hello properties tooget toohello values we want.</span></span>

<span data-ttu-id="f693e-200">在您的應用程式中，您不需要 toouse 屬性。</span><span class="sxs-lookup"><span data-stu-id="f693e-200">You don't have toouse properties in your application.</span></span> <span data-ttu-id="f693e-201">不過，如果您需要 tooset 這些事件或擷取這些訊息，從 hello **IoTHubClient**程式庫可讓您輕鬆。</span><span class="sxs-lookup"><span data-stu-id="f693e-201">However, if you need tooset them on events or retrieve them from messages, hello **IoTHubClient** library makes it easy.</span></span>

## <a name="message-handling"></a><span data-ttu-id="f693e-202">訊息處理</span><span class="sxs-lookup"><span data-stu-id="f693e-202">Message handling</span></span>
<span data-ttu-id="f693e-203">如先前所述，當訊息抵達從 IoT 中樞 hello **IoTHubClient**回應叫用註冊的回呼函式的程式庫。</span><span class="sxs-lookup"><span data-stu-id="f693e-203">As stated previously, when messages arrive from IoT Hub hello **IoTHubClient** library responds by invoking a registered callback function.</span></span> <span data-ttu-id="f693e-204">此函式有一個傳回參數值得額外說明。</span><span class="sxs-lookup"><span data-stu-id="f693e-204">There is a return parameter of this function that deserves some additional explanation.</span></span> <span data-ttu-id="f693e-205">以下是在 hello hello 回呼函式的摘錄**iot 中樞\_用戶端\_範例\_http**範例應用程式：</span><span class="sxs-lookup"><span data-stu-id="f693e-205">Here’s an excerpt of hello callback function in hello **iothub\_client\_sample\_http** sample application:</span></span>

```
static IOTHUBMESSAGE_DISPOSITION_RESULT ReceiveMessageCallback(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    . . .
    return IOTHUBMESSAGE_ACCEPTED;
}
```

<span data-ttu-id="f693e-206">請注意，hello 傳回型別是**IOTHUBMESSAGE\_配置\_結果**，在這個特定案例，我們決定傳回**IOTHUBMESSAGE\_接受**。</span><span class="sxs-lookup"><span data-stu-id="f693e-206">Note that hello return type is **IOTHUBMESSAGE\_DISPOSITION\_RESULT** and in this particular case we return **IOTHUBMESSAGE\_ACCEPTED**.</span></span> <span data-ttu-id="f693e-207">有其他值，我們可以從這個函式傳回變更如何 hello **IoTHubClient**程式庫會做出反應 toohello 訊息回呼。</span><span class="sxs-lookup"><span data-stu-id="f693e-207">There are other values we can return from this function that change how hello **IoTHubClient** library reacts toohello message callback.</span></span> <span data-ttu-id="f693e-208">以下是 hello 選項。</span><span class="sxs-lookup"><span data-stu-id="f693e-208">Here are hello options.</span></span>

* <span data-ttu-id="f693e-209">**IOTHUBMESSAGE\_接受**– hello 訊息已成功處理。</span><span class="sxs-lookup"><span data-stu-id="f693e-209">**IOTHUBMESSAGE\_ACCEPTED** – hello message has been processed successfully.</span></span> <span data-ttu-id="f693e-210">hello **IoTHubClient**程式庫不會叫用一次以 hello hello 回呼函式相同的訊息。</span><span class="sxs-lookup"><span data-stu-id="f693e-210">hello **IoTHubClient** library will not invoke hello callback function again with hello same message.</span></span>
* <span data-ttu-id="f693e-211">**IOTHUBMESSAGE\_已拒絕**– hello 訊息尚未處理，而且沒有任何 desire toodo 動作 hello 未來。</span><span class="sxs-lookup"><span data-stu-id="f693e-211">**IOTHUBMESSAGE\_REJECTED** – hello message was not processed and there is no desire toodo so in hello future.</span></span> <span data-ttu-id="f693e-212">hello **IoTHubClient**程式庫不叫用一次以 hello hello 回呼函式相同的訊息。</span><span class="sxs-lookup"><span data-stu-id="f693e-212">hello **IoTHubClient** library should not invoke hello callback function again with hello same message.</span></span>
* <span data-ttu-id="f693e-213">**IOTHUBMESSAGE\_已放棄**– hello 訊息尚未處理成功，但 hello **IoTHubClient**程式庫應該要叫用一次以 hello hello 回呼函式相同的訊息。</span><span class="sxs-lookup"><span data-stu-id="f693e-213">**IOTHUBMESSAGE\_ABANDONED** – hello message was not processed successfully, but hello **IoTHubClient** library should invoke hello callback function again with hello same message.</span></span>

<span data-ttu-id="f693e-214">Hello 前兩個傳回碼，hello **IoTHubClient**程式庫會傳送訊息 tooIoT 中樞 hello 訊息，指出應該從 hello 裝置佇列中刪除，並不會傳遞一次。</span><span class="sxs-lookup"><span data-stu-id="f693e-214">For hello first two return codes, hello **IoTHubClient** library sends a message tooIoT Hub indicating that hello message should be deleted from hello device queue and not delivered again.</span></span> <span data-ttu-id="f693e-215">hello 淨效果為 hello 相同 （hello 訊息從佇列中刪除 hello 裝置），但仍會記錄 hello 訊息是否已接受或拒絕。</span><span class="sxs-lookup"><span data-stu-id="f693e-215">hello net effect is hello same (hello message is deleted from hello device queue), but whether hello message was accepted or rejected is still recorded.</span></span>  <span data-ttu-id="f693e-216">錄製區別這兩者是有用的 hello 訊息 toosenders 可以接聽的意見反應和了解，是否裝置已接受或拒絕特定的訊息。</span><span class="sxs-lookup"><span data-stu-id="f693e-216">Recording this distinction is useful toosenders of hello message who can listen for feedback and find out if a device has accepted or rejected a particular message.</span></span>

<span data-ttu-id="f693e-217">在最後一個案例中 hello 訊息也會傳送 tooIoT 集線器，但它會指出該 hello 訊息應重新傳遞。</span><span class="sxs-lookup"><span data-stu-id="f693e-217">In hello last case a message is also sent tooIoT Hub, but it indicates that hello message should be redelivered.</span></span> <span data-ttu-id="f693e-218">通常您會放棄的訊息，如果您遇到某些錯誤，但想 tootry tooprocess hello 訊息一次。</span><span class="sxs-lookup"><span data-stu-id="f693e-218">Typically you’ll abandon a message if you encounter some error but want tootry tooprocess hello message again.</span></span> <span data-ttu-id="f693e-219">相較之下，拒絕的訊息適合，當您遇到無法復原的錯誤 （或如果您只需決定您不要 tooprocess hello 訊息）。</span><span class="sxs-lookup"><span data-stu-id="f693e-219">In contrast, rejecting a message is appropriate when you encounter an unrecoverable error (or if you simply decide you don’t want tooprocess hello message).</span></span>

<span data-ttu-id="f693e-220">在任何情況下，請留意 hello 不同傳回碼，讓您可以引發您想要從 hello 的 hello 行為**IoTHubClient**程式庫。</span><span class="sxs-lookup"><span data-stu-id="f693e-220">In any case, be aware of hello different return codes so that you can elicit hello behavior you want from hello **IoTHubClient** library.</span></span>

## <a name="alternate-device-credentials"></a><span data-ttu-id="f693e-221">替代裝置認證</span><span class="sxs-lookup"><span data-stu-id="f693e-221">Alternate device credentials</span></span>
<span data-ttu-id="f693e-222">如先前所述，hello 首先 toodo 時使用 hello **IoTHubClient**程式庫是 tooobtain **iot 中樞\_用戶端\_處理**例如 hello 呼叫下列：</span><span class="sxs-lookup"><span data-stu-id="f693e-222">As explained previously, hello first thing toodo when working with hello **IoTHubClient** library is tooobtain a **IOTHUB\_CLIENT\_HANDLE** with a call such as hello following:</span></span>

```
IOTHUB_CLIENT_HANDLE iotHubClientHandle;
iotHubClientHandle = IoTHubClient_CreateFromConnectionString(connectionString, AMQP_Protocol);
```

<span data-ttu-id="f693e-223">hello 引數太**IoTHubClient\_CreateFromConnectionString** hello 裝置連接字串和表示我們使用 toocommunicate 與 IoT 中樞的 hello 通訊協定的參數。</span><span class="sxs-lookup"><span data-stu-id="f693e-223">hello arguments too**IoTHubClient\_CreateFromConnectionString** are hello device connection string and a parameter that indicates hello protocol we use toocommunicate with IoT Hub.</span></span> <span data-ttu-id="f693e-224">hello 裝置連接字串的格式顯示，如下所示：</span><span class="sxs-lookup"><span data-stu-id="f693e-224">hello device connection string has a format that appears as follows:</span></span>

```
HostName=IOTHUBNAME.IOTHUBSUFFIX;DeviceId=DEVICEID;SharedAccessKey=SHAREDACCESSKEY
```

<span data-ttu-id="f693e-225">這個字串中包含四項資訊：IoT 中樞名稱、IoT 中樞尾碼、裝置識別碼和共用存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="f693e-225">There are four pieces of information in this string: IoT Hub name, IoT Hub suffix, device ID, and shared access key.</span></span> <span data-ttu-id="f693e-226">Hello Azure 入口網站中建立您的 IoT 中樞執行個體時，取得的 IoT 中樞的 hello 完整的網域名稱 (FQDN)，這可讓您 hello IoT 中樞名稱 （hello 第一部份 hello FQDN） 和 hello IoT 中樞後置詞 (hello rest 的 hello FQDN)。</span><span class="sxs-lookup"><span data-stu-id="f693e-226">You obtain hello fully qualified domain name (FQDN) of an IoT hub when you create your IoT hub instance in hello Azure portal — this gives you hello IoT hub name (hello first part of hello FQDN) and hello IoT hub suffix (hello rest of hello FQDN).</span></span> <span data-ttu-id="f693e-227">當您註冊您的裝置與 IoT 中樞時，取得 hello 裝置識別碼和 hello 共用的存取金鑰 (hello 中所述[前一篇文章](iot-hub-device-sdk-c-intro.md))。</span><span class="sxs-lookup"><span data-stu-id="f693e-227">You get hello device ID and hello shared access key when you register your device with IoT Hub (as described in hello [previous article](iot-hub-device-sdk-c-intro.md)).</span></span>

<span data-ttu-id="f693e-228">**IoTHubClient\_CreateFromConnectionString**可讓您其中一種方式 tooinitialize hello 程式庫。</span><span class="sxs-lookup"><span data-stu-id="f693e-228">**IoTHubClient\_CreateFromConnectionString** gives you one way tooinitialize hello library.</span></span> <span data-ttu-id="f693e-229">如果您想要的話，您可以建立新**iot 中樞\_用戶端\_處理**使用這些個別的參數，而不是 hello 裝置連接字串。</span><span class="sxs-lookup"><span data-stu-id="f693e-229">If you prefer, you can create a new **IOTHUB\_CLIENT\_HANDLE** by using these individual parameters rather than hello device connection string.</span></span> <span data-ttu-id="f693e-230">這是以下列程式碼的 hello 來達成：</span><span class="sxs-lookup"><span data-stu-id="f693e-230">This is achieved with hello following code:</span></span>

```
IOTHUB_CLIENT_CONFIG iotHubClientConfig;
iotHubClientConfig.iotHubName = "";
iotHubClientConfig.deviceId = "";
iotHubClientConfig.deviceKey = "";
iotHubClientConfig.iotHubSuffix = "";
iotHubClientConfig.protocol = HTTP_Protocol;
IOTHUB_CLIENT_HANDLE iotHubClientHandle = IoTHubClient_LL_Create(&iotHubClientConfig);
```

<span data-ttu-id="f693e-231">這可達成 hello 相同的動作**IoTHubClient\_CreateFromConnectionString**。</span><span class="sxs-lookup"><span data-stu-id="f693e-231">This accomplishes hello same thing as **IoTHubClient\_CreateFromConnectionString**.</span></span>

<span data-ttu-id="f693e-232">很明顯，您會想 toouse **IoTHubClient\_CreateFromConnectionString**而不是這個更多詳細資料的初始化方法。</span><span class="sxs-lookup"><span data-stu-id="f693e-232">It may seem obvious that you would want toouse **IoTHubClient\_CreateFromConnectionString** rather than this more verbose method of initialization.</span></span> <span data-ttu-id="f693e-233">但請記住，當您在 IoT 中樞註冊裝置時，您得到的是裝置識別碼和裝置金鑰 (不是連接字串)。</span><span class="sxs-lookup"><span data-stu-id="f693e-233">Keep in mind, however, that when you register a device in IoT Hub what you get is a device ID and device key (not a connection string).</span></span> <span data-ttu-id="f693e-234">hello*裝置總管*hello 中導入的 SDK 工具[前一篇文章](iot-hub-device-sdk-c-intro.md)使用文件庫中 hello **Azure IoT 服務 SDK** toocreate hello 裝置中的連接字串hello 裝置識別碼、 裝置識別碼和 IoT 中樞的主機名稱。</span><span class="sxs-lookup"><span data-stu-id="f693e-234">hello *device explorer* SDK tool introduced in hello [previous article](iot-hub-device-sdk-c-intro.md) uses libraries in hello **Azure IoT service SDK** toocreate hello device connection string from hello device ID, device key, and IoT Hub host name.</span></span> <span data-ttu-id="f693e-235">因此呼叫**IoTHubClient\_LL\_建立**可能是更理想，因為它可以節省 hello 步驟產生連接字串。</span><span class="sxs-lookup"><span data-stu-id="f693e-235">So calling **IoTHubClient\_LL\_Create** may be preferable because it saves you hello step of generating a connection string.</span></span> <span data-ttu-id="f693e-236">使用任何方法都很方便。</span><span class="sxs-lookup"><span data-stu-id="f693e-236">Use whichever method is convenient.</span></span>

## <a name="configuration-options"></a><span data-ttu-id="f693e-237">組態選項</span><span class="sxs-lookup"><span data-stu-id="f693e-237">Configuration options</span></span>
<span data-ttu-id="f693e-238">到目前為止的所有項目所述有關 hello 方式 hello **IoTHubClient**程式庫的運作方式會反映其預設行為。</span><span class="sxs-lookup"><span data-stu-id="f693e-238">So far everything described about hello way hello **IoTHubClient** library works reflects its default behavior.</span></span> <span data-ttu-id="f693e-239">不過，有一些您可以設定的 toochange hello 程式庫的運作方式的選項。</span><span class="sxs-lookup"><span data-stu-id="f693e-239">However, there are a few options that you can set toochange how hello library works.</span></span> <span data-ttu-id="f693e-240">這會透過利用 hello **IoTHubClient\_LL\_SetOption**應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="f693e-240">This is accomplished by leveraging hello **IoTHubClient\_LL\_SetOption** API.</span></span> <span data-ttu-id="f693e-241">請思考此範例：</span><span class="sxs-lookup"><span data-stu-id="f693e-241">Consider this example:</span></span>

```
unsigned int timeout = 30000;
IoTHubClient_LL_SetOption(iotHubClientHandle, "timeout", &timeout);
```

<span data-ttu-id="f693e-242">有一些常用的選項：</span><span class="sxs-lookup"><span data-stu-id="f693e-242">There are a couple of options that are commonly used:</span></span>

* <span data-ttu-id="f693e-243">**SetBatching** (bool) – 如果**true**，再傳送資料 tooIoT 中樞傳送批次中。</span><span class="sxs-lookup"><span data-stu-id="f693e-243">**SetBatching** (bool) – If **true**, then data sent tooIoT Hub is sent in batches.</span></span> <span data-ttu-id="f693e-244">如果為 **false**，就表示訊息會個別傳送。</span><span class="sxs-lookup"><span data-stu-id="f693e-244">If **false**, then messages are sent individually.</span></span> <span data-ttu-id="f693e-245">hello 預設值是**false**。</span><span class="sxs-lookup"><span data-stu-id="f693e-245">hello default is **false**.</span></span> <span data-ttu-id="f693e-246">請注意該 hello **SetBatching**選項只適用於 toohello HTTP 通訊協定和不 toohello MQTT 或 AMQP 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="f693e-246">Note that hello **SetBatching** option only applies toohello HTTP protocol and not toohello MQTT or AMQP protocols.</span></span>
* <span data-ttu-id="f693e-247">**Timeout** (unsigned int) - 這個值會以毫秒為單位表示。</span><span class="sxs-lookup"><span data-stu-id="f693e-247">**Timeout** (unsigned int) – This value is represented in milliseconds.</span></span> <span data-ttu-id="f693e-248">如果要傳送的 HTTP 要求或接收回應使用超過這個時間，hello 連接逾時。</span><span class="sxs-lookup"><span data-stu-id="f693e-248">If sending an HTTP request or receiving a response takes longer than this time, then hello connection times out.</span></span>

<span data-ttu-id="f693e-249">批次處理選項的 hello 很重要。</span><span class="sxs-lookup"><span data-stu-id="f693e-249">hello batching option is important.</span></span> <span data-ttu-id="f693e-250">根據預設，hello 庫 ingresses 事件個別 (單一事件是任何您傳遞太**IoTHubClient\_LL\_SendEventAsync**)。</span><span class="sxs-lookup"><span data-stu-id="f693e-250">By default, hello library ingresses events individually (a single event is whatever you pass too**IoTHubClient\_LL\_SendEventAsync**).</span></span> <span data-ttu-id="f693e-251">如果批次處理選項的 hello **true**，hello 程式庫會收集會從 hello 緩衝區 （向上 toohello IoT 中樞將會接受最大訊息大小） 的事件數目。</span><span class="sxs-lookup"><span data-stu-id="f693e-251">If hello batching option is **true**, hello library collects as many events as it can from hello buffer (up toohello maximum message size that IoT Hub will accept).</span></span>  <span data-ttu-id="f693e-252">hello 事件批次傳送 tooIoT 中樞在單一 HTTP 呼叫 （hello 個別事件會配套到 JSON 陣列）。</span><span class="sxs-lookup"><span data-stu-id="f693e-252">hello event batch is sent tooIoT Hub in a single HTTP call (hello individual events are bundled into a JSON array).</span></span> <span data-ttu-id="f693e-253">啟用批次處理通常會導致效能大幅提升，因為網路來回行程正在減少。</span><span class="sxs-lookup"><span data-stu-id="f693e-253">Enabling batching typically results in big performance gains since you’re reducing network round-trips.</span></span> <span data-ttu-id="f693e-254">它也會大幅減少頻寬，因為您正利用事件批次傳送一組 HTTP 標頭，而不是針對每個個別事件傳送一組標頭。</span><span class="sxs-lookup"><span data-stu-id="f693e-254">It also significantly reduces bandwidth since you are sending one set of HTTP headers with an event batch rather than a set of headers for each individual event.</span></span> <span data-ttu-id="f693e-255">除非有特定原因 toodo，否則您通常會想 tooenable 批次處理。</span><span class="sxs-lookup"><span data-stu-id="f693e-255">Unless you have a specific reason toodo otherwise, typically you’ll want tooenable batching.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f693e-256">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f693e-256">Next steps</span></span>
<span data-ttu-id="f693e-257">本文說明中的 hello 詳細 hello 行為**IoTHubClient** hello 中找到程式庫**C 的 Azure IoT 裝置 SDK**。利用此資訊，您應該深入了解的 hello hello 功能**IoTHubClient**程式庫。</span><span class="sxs-lookup"><span data-stu-id="f693e-257">This article describes in detail hello behavior of hello **IoTHubClient** library found in hello **Azure IoT device SDK for C**. With this information, you should have a good understanding of hello capabilities of hello **IoTHubClient** library.</span></span> <span data-ttu-id="f693e-258">hello[下一篇文章](iot-hub-device-sdk-c-serializer.md)hello 會類似的詳細說明**序列化程式**程式庫。</span><span class="sxs-lookup"><span data-stu-id="f693e-258">hello [next article](iot-hub-device-sdk-c-serializer.md) provides similar detail on hello **serializer** library.</span></span>

<span data-ttu-id="f693e-259">toolearn 進一步了解開發的 IoT 中樞，請參閱 hello [Azure IoT Sdk][lnk-sdks]。</span><span class="sxs-lookup"><span data-stu-id="f693e-259">toolearn more about developing for IoT Hub, see hello [Azure IoT SDKs][lnk-sdks].</span></span>

<span data-ttu-id="f693e-260">toofurther 瀏覽的 IoT 中樞的 hello 功能，請參閱：</span><span class="sxs-lookup"><span data-stu-id="f693e-260">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="f693e-261">[使用 Azure IoT Edge 來模擬裝置][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="f693e-261">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
