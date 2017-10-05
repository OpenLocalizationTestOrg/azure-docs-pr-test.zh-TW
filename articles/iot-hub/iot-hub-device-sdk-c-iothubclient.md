---
title: "適用於 C 的 Azure IoT 裝置 SDK - IoTHubClient | Microsoft Docs"
description: "如何使用適用於 C 的 Azure IoT 裝置 SDK 中的 IoTHubClient 程式庫，以建立與 IoT 中樞通訊的裝置應用程式。"
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
ms.openlocfilehash: 422d89014511f0d08ba57a893570ff7b253b7bc4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-iot-device-sdk-for-c--more-about-iothubclient"></a><span data-ttu-id="32b78-103">適用於 C 的 Azure IoT 裝置 SDK - 深入了解 IoTHubClient</span><span class="sxs-lookup"><span data-stu-id="32b78-103">Azure IoT device SDK for C – more about IoTHubClient</span></span>
<span data-ttu-id="32b78-104">本系列的[第一篇文章](iot-hub-device-sdk-c-intro.md)介紹了「適用於 C 的 Azure IoT 裝置 SDK」。該文章已說明 SDK 中有兩個架構層。</span><span class="sxs-lookup"><span data-stu-id="32b78-104">The [first article](iot-hub-device-sdk-c-intro.md) in this series introduced the **Azure IoT device SDK for C**. That article explained that there are two architectural layers in SDK.</span></span> <span data-ttu-id="32b78-105">在基底的是 **IoTHubClient** 程式庫，可直接管理與 IoT 中樞的通訊。</span><span class="sxs-lookup"><span data-stu-id="32b78-105">At the base is the **IoTHubClient** library which directly manages communication with IoT Hub.</span></span> <span data-ttu-id="32b78-106">還有 **序列化程式** 庫，此程式庫建置於其頂部以提供序列化服務。</span><span class="sxs-lookup"><span data-stu-id="32b78-106">There's also the **serializer** library that builds on top of that to provide serialization services.</span></span> <span data-ttu-id="32b78-107">在本文中，我們將提供 **IoTHubClient** 程式庫的其他詳細資料。</span><span class="sxs-lookup"><span data-stu-id="32b78-107">In this article we'll provide additional detail on the **IoTHubClient** library.</span></span>

<span data-ttu-id="32b78-108">前一篇文章描述如何使用 **IoTHubClient** 程式庫傳送事件到 IoT 中樞及接收訊息。</span><span class="sxs-lookup"><span data-stu-id="32b78-108">The previous article described how to use the **IoTHubClient** library to send events to IoT Hub and receive messages.</span></span> <span data-ttu-id="32b78-109">本文將向您介紹「較低層級 API」，以說明如何更精確地管理傳送和接收資料的「時機」來延伸該討論。</span><span class="sxs-lookup"><span data-stu-id="32b78-109">This article extends that discussion by explaining how to more precisely manage *when* you send and receive data, introducing you to the **lower-level APIs**.</span></span> <span data-ttu-id="32b78-110">我們也將說明如何使用 **IoTHubClient** 程式庫中的屬性處理功能，將屬性附加到事件 (並從訊息將其擷取)。</span><span class="sxs-lookup"><span data-stu-id="32b78-110">We'll also explain how to attach properties to events (and retrieve them from messages) using the property handling features in the **IoTHubClient** library.</span></span> <span data-ttu-id="32b78-111">最後，我們將提供其他說明，以不同的方式來處理從 IoT 中樞接收的訊息。</span><span class="sxs-lookup"><span data-stu-id="32b78-111">Finally, we'll provide additional explanation of different ways to handle messages received from IoT Hub.</span></span>

<span data-ttu-id="32b78-112">本文以涵蓋幾個其他主題 (包括更多有關裝置認證及如何透過組態選項變更 **IoTHubClient** 行為的資訊) 做總結。</span><span class="sxs-lookup"><span data-stu-id="32b78-112">The article concludes by covering a couple of miscellaneous topics, including more about device credentials and how to change the behavior of the **IoTHubClient** through configuration options.</span></span>

<span data-ttu-id="32b78-113">我們將使用 **IoTHubClient** SDK 範例來說明這些主題。</span><span class="sxs-lookup"><span data-stu-id="32b78-113">We'll use the **IoTHubClient** SDK samples to explain these topics.</span></span> <span data-ttu-id="32b78-114">如果您想要依照這些內容，請參閱「適用於 C 的 Azure IoT 裝置 SDK」中隨附的 **iothub\_client\_sample\_http** 和 **iothub\_client\_sample\_amqp** 應用程式。這些範例會示範下列各節中所述的所有內容。</span><span class="sxs-lookup"><span data-stu-id="32b78-114">If you want to follow along, see the **iothub\_client\_sample\_http** and **iothub\_client\_sample\_amqp** applications that are included in the Azure IoT device SDK for C. Everything described in the following sections is demonstrated in these samples.</span></span>

<span data-ttu-id="32b78-115">您可以尋找[**適用於 C 的 Azure IoT 裝置 SDK**](https://github.com/Azure/azure-iot-sdk-c) GitHub 儲存機制，然後在 [C API 參考資料](https://azure.github.io/azure-iot-sdk-c/index.html)中檢視 API 的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="32b78-115">You can find the [**Azure IoT device SDK for C**](https://github.com/Azure/azure-iot-sdk-c) GitHub repository and view details of the API in the [C API reference](https://azure.github.io/azure-iot-sdk-c/index.html).</span></span>

## <a name="the-lower-level-apis"></a><span data-ttu-id="32b78-116">較低層級的 API</span><span class="sxs-lookup"><span data-stu-id="32b78-116">The lower-level APIs</span></span>
<span data-ttu-id="32b78-117">前一篇文章描述了 **iothub\_client\_sample\_amqp** 應用程式內容中 **IotHubClient** 的基本作業。</span><span class="sxs-lookup"><span data-stu-id="32b78-117">The previous article described the basic operation of the **IotHubClient** within the context of the **iothub\_client\_sample\_amqp** application.</span></span> <span data-ttu-id="32b78-118">比方說，該文說明如何使用下列程式碼初始化程式庫。</span><span class="sxs-lookup"><span data-stu-id="32b78-118">For example, it explained how to initialize the library using this code.</span></span>

```
IOTHUB_CLIENT_HANDLE iotHubClientHandle;
iotHubClientHandle = IoTHubClient_CreateFromConnectionString(connectionString, AMQP_Protocol);
```

<span data-ttu-id="32b78-119">此外，還會說明如何使用這個函式呼叫來傳送事件。</span><span class="sxs-lookup"><span data-stu-id="32b78-119">It also described how to send events using this function call.</span></span>

```
IoTHubClient_SendEventAsync(iotHubClientHandle, message.messageHandle, SendConfirmationCallback, &message);
```

<span data-ttu-id="32b78-120">本文還會說明如何藉由註冊回呼函式來接收訊息。</span><span class="sxs-lookup"><span data-stu-id="32b78-120">The article also described how to receive messages by registering a callback function.</span></span>

```
int receiveContext = 0;
IoTHubClient_SetMessageCallback(iotHubClientHandle, ReceiveMessageCallback, &receiveContext);
```

<span data-ttu-id="32b78-121">本文同時示範了如何使用如下的程式碼釋放資源。</span><span class="sxs-lookup"><span data-stu-id="32b78-121">The article also showed how to free resources using code such as the following.</span></span>

```
IoTHubClient_Destroy(iotHubClientHandle);
```

<span data-ttu-id="32b78-122">但是每個 API 都有隨附函式：</span><span class="sxs-lookup"><span data-stu-id="32b78-122">However there are companion functions to each of these APIs:</span></span>

* <span data-ttu-id="32b78-123">IoTHubClient\_LL\_CreateFromConnectionString</span><span class="sxs-lookup"><span data-stu-id="32b78-123">IoTHubClient\_LL\_CreateFromConnectionString</span></span>
* <span data-ttu-id="32b78-124">IoTHubClient\_LL\_SendEventAsync</span><span class="sxs-lookup"><span data-stu-id="32b78-124">IoTHubClient\_LL\_SendEventAsync</span></span>
* <span data-ttu-id="32b78-125">IoTHubClient\_LL\_SetMessageCallback</span><span class="sxs-lookup"><span data-stu-id="32b78-125">IoTHubClient\_LL\_SetMessageCallback</span></span>
* <span data-ttu-id="32b78-126">IoTHubClient\_LL\_Destroy</span><span class="sxs-lookup"><span data-stu-id="32b78-126">IoTHubClient\_LL\_Destroy</span></span>

<span data-ttu-id="32b78-127">這些函式的 API 名稱中都包含 "LL"。</span><span class="sxs-lookup"><span data-stu-id="32b78-127">These functions all include “LL” in the API name.</span></span> <span data-ttu-id="32b78-128">除此之外，這其中每個函式的參數都會與其非 LL 的對應項目相同。</span><span class="sxs-lookup"><span data-stu-id="32b78-128">Other than that, the parameters of each of these functions are identical to their non-LL counterparts.</span></span> <span data-ttu-id="32b78-129">不過，這些函式的行為有一個重要的差異。</span><span class="sxs-lookup"><span data-stu-id="32b78-129">However, the behavior of these functions is different in one important way.</span></span>

<span data-ttu-id="32b78-130">當您呼叫 **IoTHubClient\_CreateFromConnectionString** 時，基礎程式庫會建立在背景中執行的新執行緒。</span><span class="sxs-lookup"><span data-stu-id="32b78-130">When you call **IoTHubClient\_CreateFromConnectionString**, the underlying libraries create a new thread that runs in the background.</span></span> <span data-ttu-id="32b78-131">此執行緒會將事件傳送到 IoT 中樞以及接收其訊息。</span><span class="sxs-lookup"><span data-stu-id="32b78-131">This thread sends events to, and receives messages from, IoT Hub.</span></span> <span data-ttu-id="32b78-132">使用 "LL" API 時不會建立這類執行緒。</span><span class="sxs-lookup"><span data-stu-id="32b78-132">No such thread is created when working with the "LL" APIs.</span></span> <span data-ttu-id="32b78-133">背景執行緒的建立是為了方便開發人員。</span><span class="sxs-lookup"><span data-stu-id="32b78-133">The creation of the background thread is a convenience to the developer.</span></span> <span data-ttu-id="32b78-134">您完全不必擔心要明確地將事件傳送到 IoT 中樞以及從中接收訊息 -- 此動作會在背景中自動進行。</span><span class="sxs-lookup"><span data-stu-id="32b78-134">You don’t have to worry about explicitly sending events and receiving messages from IoT Hub -- it happens automatically in the background.</span></span> <span data-ttu-id="32b78-135">相對地，"LL" API 可讓您明確控制與「IoT 中樞」的通訊 (如果您需要的話)。</span><span class="sxs-lookup"><span data-stu-id="32b78-135">In contrast, the "LL" APIs give you explicit control over communication with IoT Hub, if you need it.</span></span>

<span data-ttu-id="32b78-136">若要更深入了解，讓我們看看一個範例：</span><span class="sxs-lookup"><span data-stu-id="32b78-136">To understand this better, let’s look at an example:</span></span>

<span data-ttu-id="32b78-137">當您呼叫 **IoTHubClient\_SendEventAsync** 時，其實是將事件放入緩衝區中。</span><span class="sxs-lookup"><span data-stu-id="32b78-137">When you call **IoTHubClient\_SendEventAsync**, what you're actually doing is putting the event in a buffer.</span></span> <span data-ttu-id="32b78-138">在您呼叫 **IoTHubClient\_CreateFromConnectionString** 時建立的背景執行緒會持續監視這個緩衝區，並將它所包含的任何資料傳送到「IoT 中樞」。</span><span class="sxs-lookup"><span data-stu-id="32b78-138">The background thread created when you call **IoTHubClient\_CreateFromConnectionString** continually monitors this buffer and sends any data that it contains to IoT Hub.</span></span> <span data-ttu-id="32b78-139">這些動作會在主執行緒執行其他工作的同時在背景中進行。</span><span class="sxs-lookup"><span data-stu-id="32b78-139">This happens in the background at the same time that the main thread is performing other work.</span></span>

<span data-ttu-id="32b78-140">同樣地，當您使用 **IoTHubClient\_SetMessageCallback** 來註冊訊息的回呼函式時，即是在指示 SDK 讓背景執行緒在收到訊息時叫用回呼函式 (不受主執行緒影響)。</span><span class="sxs-lookup"><span data-stu-id="32b78-140">Similarly, when you register a callback function for messages using **IoTHubClient\_SetMessageCallback**, you're instructing the SDK to have the background thread invoke the callback function when a message is received, independent of the main thread.</span></span>

<span data-ttu-id="32b78-141">"LL" API 不會建立背景執行緒。</span><span class="sxs-lookup"><span data-stu-id="32b78-141">The "LL" APIs don’t create a background thread.</span></span> <span data-ttu-id="32b78-142">而是必須呼叫新的 API 明確地與 IoT 中樞之間傳送和接收資料。</span><span class="sxs-lookup"><span data-stu-id="32b78-142">Instead, a new API must be called to explicitly send and receive data from IoT Hub.</span></span> <span data-ttu-id="32b78-143">下列範例就將此進行示範。</span><span class="sxs-lookup"><span data-stu-id="32b78-143">This is demonstrated in the following example.</span></span>

<span data-ttu-id="32b78-144">SDK 中隨附的 **iothub\_client\_sample\_http** 應用程式會示範較低層級的 API。</span><span class="sxs-lookup"><span data-stu-id="32b78-144">The **iothub\_client\_sample\_http** application that’s included in the SDK demonstrates the lower-level APIs.</span></span> <span data-ttu-id="32b78-145">在該範例中，我們會使用類似以下的程式碼，將事件傳送給「IoT 中樞」︰</span><span class="sxs-lookup"><span data-stu-id="32b78-145">In that sample, we send events to IoT Hub with code such as the following:</span></span>

```
EVENT_INSTANCE message;
sprintf_s(msgText, sizeof(msgText), "Message_%d_From_IoTHubClient_LL_Over_HTTP", i);
message.messageHandle = IoTHubMessage_CreateFromByteArray((const unsigned char*)msgText, strlen(msgText));

IoTHubClient_LL_SendEventAsync(iotHubClientHandle, message.messageHandle, SendConfirmationCallback, &message)
```

<span data-ttu-id="32b78-146">前三行會建立訊息，而最後一行會傳送事件。</span><span class="sxs-lookup"><span data-stu-id="32b78-146">The first three lines create the message, and the last line sends the event.</span></span> <span data-ttu-id="32b78-147">不過，如先前所述，「傳送」事件表示只是將資料放置於緩衝區中。</span><span class="sxs-lookup"><span data-stu-id="32b78-147">However, as mentioned previously, "sending" the event means that the data is simply placed in a buffer.</span></span> <span data-ttu-id="32b78-148">當我們呼叫 **IoTHubClient\_LL\_SendEventAsync** 時，不會在網路上傳輸任何內容。</span><span class="sxs-lookup"><span data-stu-id="32b78-148">Nothing is transmitted on the network when we call **IoTHubClient\_LL\_SendEventAsync**.</span></span> <span data-ttu-id="32b78-149">若要實際將資料輸入到「IoT 中樞」，您必須呼叫 **IoTHubClient\_LL\_DoWork**，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="32b78-149">In order to actually ingress the data to IoT Hub, you must call **IoTHubClient\_LL\_DoWork**, as in this example:</span></span>

```
while (1)
{
    IoTHubClient_LL_DoWork(iotHubClientHandle);
    ThreadAPI_Sleep(1000);
}
```

<span data-ttu-id="32b78-150">此程式碼 (來自 **iothub\_client\_sample\_http** 應用程式) 會重複地呼叫 **IoTHubClient\_LL\_DoWork**。</span><span class="sxs-lookup"><span data-stu-id="32b78-150">This code (from the **iothub\_client\_sample\_http** application) repeatedly calls **IoTHubClient\_LL\_DoWork**.</span></span> <span data-ttu-id="32b78-151">每次呼叫 **IoTHubClient\_LL\_DoWork** 時，它都會將某些事件從緩衝區傳送到「IoT 中樞」，而且會擷取傳送到裝置的佇列訊息。</span><span class="sxs-lookup"><span data-stu-id="32b78-151">Each time **IoTHubClient\_LL\_DoWork** is called, it sends some events from the buffer to IoT Hub and it retrieves a queued message being sent to the device.</span></span> <span data-ttu-id="32b78-152">在後者的情況下，這表示如果我們已註冊訊息的回呼函式，則會叫用回呼 (假設所有訊息皆已加入佇列)。</span><span class="sxs-lookup"><span data-stu-id="32b78-152">The latter case means that if we registered a callback function for messages, then the callback is invoked (assuming any messages are queued up).</span></span> <span data-ttu-id="32b78-153">我們會使用如下的程式碼來註冊這類回呼函式：</span><span class="sxs-lookup"><span data-stu-id="32b78-153">We would have registered such a callback function with code such as the following:</span></span>

```
IoTHubClient_LL_SetMessageCallback(iotHubClientHandle, ReceiveMessageCallback, &receiveContext)
```

<span data-ttu-id="32b78-154">迴圈中經常呼叫 **IoTHubClient\_LL\_DoWork** 的原因是每次呼叫它時，它都會將「一些」緩衝的事件傳送到「IoT 中樞」，並為裝置擷取加入佇列的「下一個」訊息。</span><span class="sxs-lookup"><span data-stu-id="32b78-154">The reason that **IoTHubClient\_LL\_DoWork** is often called in a loop is that each time it’s called, it sends *some* buffered events to IoT Hub and retrieves *the next* message queued up for the device.</span></span> <span data-ttu-id="32b78-155">每次呼叫都不保證會傳送所有緩衝的事件或擷取所有加入佇列的訊息。</span><span class="sxs-lookup"><span data-stu-id="32b78-155">Each call isn’t guaranteed to send all buffered events or to retrieve all queued messages.</span></span> <span data-ttu-id="32b78-156">如果您想要傳送緩衝區中的所有事件，並繼續進行其他處理程序，您可以使用如下程式碼來取代此迴圈：</span><span class="sxs-lookup"><span data-stu-id="32b78-156">If you want to send all events in the buffer and then continue on with other processing you can replace this loop with code such as the following:</span></span>

```
IOTHUB_CLIENT_STATUS status;

while ((IoTHubClient_LL_GetSendStatus(iotHubClientHandle, &status) == IOTHUB_CLIENT_OK) && (status == IOTHUB_CLIENT_SEND_STATUS_BUSY))
{
    IoTHubClient_LL_DoWork(iotHubClientHandle);
    ThreadAPI_Sleep(1000);
}
```

<span data-ttu-id="32b78-157">此程式碼會呼叫 **IoTHubClient\_LL\_DoWork**，直到緩衝區中的所有事件都已傳送到「IoT 中樞」為止。</span><span class="sxs-lookup"><span data-stu-id="32b78-157">This code calls **IoTHubClient\_LL\_DoWork** until all events in the buffer have been sent to IoT Hub.</span></span> <span data-ttu-id="32b78-158">請注意，這並未一併暗示已收到所有佇列的訊息。</span><span class="sxs-lookup"><span data-stu-id="32b78-158">Note this does not also imply that all queued messages have been received.</span></span> <span data-ttu-id="32b78-159">部分原因是因為檢查「所有」訊息的決定性並不如動作一般。</span><span class="sxs-lookup"><span data-stu-id="32b78-159">Part of the reason for this is that checking for "all" messages isn’t as deterministic an action.</span></span> <span data-ttu-id="32b78-160">如果您擷取「所有」訊息，但另一個訊息又隨即傳送至裝置，會發生什麼事？</span><span class="sxs-lookup"><span data-stu-id="32b78-160">What happens if you retrieve "all" of the messages, but then another one is sent to the device immediately after?</span></span> <span data-ttu-id="32b78-161">更好的處理方法是利用程式化的逾時。</span><span class="sxs-lookup"><span data-stu-id="32b78-161">A better way to deal with that is with a programmed timeout.</span></span> <span data-ttu-id="32b78-162">例如，每次叫用訊息回呼函式時，它可以重設計時器。</span><span class="sxs-lookup"><span data-stu-id="32b78-162">For example, the message callback function could reset a timer every time it’s invoked.</span></span> <span data-ttu-id="32b78-163">如果最後 *X* 秒都沒有收到任何訊息，您可以接著撰寫邏輯來繼續處理。</span><span class="sxs-lookup"><span data-stu-id="32b78-163">You can then write logic to continue processing if, for example, no messages have been received in the last *X* seconds.</span></span>

<span data-ttu-id="32b78-164">當您完成輸入事件和接收訊息時，請務必呼叫相對應的函式來清除資源。</span><span class="sxs-lookup"><span data-stu-id="32b78-164">When you’re finished ingressing events and receiving messages, be sure to call the corresponding function to clean up resources.</span></span>

```
IoTHubClient_LL_Destroy(iotHubClientHandle);
```

<span data-ttu-id="32b78-165">基本上，只有一組 API 會利用背景執行緒來傳送和接收資料，另一組 API 不會利用背景執行緒來執行相同的動作。</span><span class="sxs-lookup"><span data-stu-id="32b78-165">Basically there’s only one set of APIs to send and receive data with a background thread and another set of APIs that does the same thing without the background thread.</span></span> <span data-ttu-id="32b78-166">許多開發人員可能會偏好非 LL API，但是如果開發人員想要明確控制網路傳輸，則較低層級的 API 會相當有用。</span><span class="sxs-lookup"><span data-stu-id="32b78-166">A lot of developers may prefer the non-LL APIs, but the lower-level APIs are useful when the developer wants explicit control over network transmissions.</span></span> <span data-ttu-id="32b78-167">例如，有些裝置會隨時間收集資料，並且只在指定的時間間隔輸入事件 (例如，每小時一次或一天一次)。</span><span class="sxs-lookup"><span data-stu-id="32b78-167">For example, some devices collect data over time and only ingress events at specified intervals (for example, once an hour or once a day).</span></span> <span data-ttu-id="32b78-168">較低層級 API 可在您與 IoT 中樞之間傳送和接收資料時，提供您明確控制的功能。</span><span class="sxs-lookup"><span data-stu-id="32b78-168">The lower-level APIs give you the ability to explicitly control when you send and receive data from IoT Hub.</span></span> <span data-ttu-id="32b78-169">其他人則會單純地偏好較低層級 API 所提供的簡單性。</span><span class="sxs-lookup"><span data-stu-id="32b78-169">Others will simply prefer the simplicity that the lower-level APIs provide.</span></span> <span data-ttu-id="32b78-170">一切動作都發生在主執行緒上，而不是有些工作會在背景中發生。</span><span class="sxs-lookup"><span data-stu-id="32b78-170">Everything happens on the main thread rather than some work happening in the background.</span></span>

<span data-ttu-id="32b78-171">無論您選擇哪種模型，請務必與您使用的 API 一致。</span><span class="sxs-lookup"><span data-stu-id="32b78-171">Whichever model you choose, be sure to be consistent in which APIs you use.</span></span> <span data-ttu-id="32b78-172">如果您是透過呼叫 **IoTHubClient\_LL\_CreateFromConnectionString** 來開始著手，請務必只使用對應的較低層級 API 來進行任何追蹤工作：</span><span class="sxs-lookup"><span data-stu-id="32b78-172">If you start by calling **IoTHubClient\_LL\_CreateFromConnectionString**, be sure you only use the corresponding lower-level APIs for any follow-up work:</span></span>

* <span data-ttu-id="32b78-173">IoTHubClient\_LL\_SendEventAsync</span><span class="sxs-lookup"><span data-stu-id="32b78-173">IoTHubClient\_LL\_SendEventAsync</span></span>
* <span data-ttu-id="32b78-174">IoTHubClient\_LL\_SetMessageCallback</span><span class="sxs-lookup"><span data-stu-id="32b78-174">IoTHubClient\_LL\_SetMessageCallback</span></span>
* <span data-ttu-id="32b78-175">IoTHubClient\_LL\_Destroy</span><span class="sxs-lookup"><span data-stu-id="32b78-175">IoTHubClient\_LL\_Destroy</span></span>
* <span data-ttu-id="32b78-176">IoTHubClient\_LL\_DoWork</span><span class="sxs-lookup"><span data-stu-id="32b78-176">IoTHubClient\_LL\_DoWork</span></span>

<span data-ttu-id="32b78-177">相反的情況也成立。</span><span class="sxs-lookup"><span data-stu-id="32b78-177">The opposite is true as well.</span></span> <span data-ttu-id="32b78-178">如果您從 **IoTHubClient\_CreateFromConnectionString** 開始著手，則請使用非 LL API 來進行任何額外的處理。</span><span class="sxs-lookup"><span data-stu-id="32b78-178">If you start with **IoTHubClient\_CreateFromConnectionString**, then use the non-LL APIs for any additional processing.</span></span>

<span data-ttu-id="32b78-179">在「適用於 C 的 Azure IoT 裝置 SDK」中，如需較低層級 API 的完整範例，請參閱 **iothub\_client\_sample\_http** 應用程式。</span><span class="sxs-lookup"><span data-stu-id="32b78-179">In the Azure IoT device SDK for C, see the **iothub\_client\_sample\_http** application for a complete example of the lower-level APIs.</span></span> <span data-ttu-id="32b78-180">如需非 LL API 的完整範例，請參考 **iothub\_client\_sample\_amqp** 應用程式。</span><span class="sxs-lookup"><span data-stu-id="32b78-180">The **iothub\_client\_sample\_amqp** application can be referenced for a full example of the non-LL APIs.</span></span>

## <a name="property-handling"></a><span data-ttu-id="32b78-181">屬性處理</span><span class="sxs-lookup"><span data-stu-id="32b78-181">Property handling</span></span>
<span data-ttu-id="32b78-182">到我們描述了傳送資料的目前為止，我們也已經參考訊息的內文。</span><span class="sxs-lookup"><span data-stu-id="32b78-182">So far when we've described sending data, we've been referring to the body of the message.</span></span> <span data-ttu-id="32b78-183">例如，請思考下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="32b78-183">For example, consider this code:</span></span>

```
EVENT_INSTANCE message;
sprintf_s(msgText, sizeof(msgText), "Hello World");
message.messageHandle = IoTHubMessage_CreateFromByteArray((const unsigned char*)msgText, strlen(msgText));
IoTHubClient_LL_SendEventAsync(iotHubClientHandle, message.messageHandle, SendConfirmationCallback, &message)
```

<span data-ttu-id="32b78-184">此範例會傳送訊息給 IoT 中樞，包含文字 "Hello World"。</span><span class="sxs-lookup"><span data-stu-id="32b78-184">This example sends a message to IoT Hub with the text "Hello World."</span></span> <span data-ttu-id="32b78-185">不過，IoT 中樞也允許屬性附加至每個訊息。</span><span class="sxs-lookup"><span data-stu-id="32b78-185">However, IoT Hub also allows properties to be attached to each message.</span></span> <span data-ttu-id="32b78-186">這些屬性是可附加至訊息的名稱/值組。</span><span class="sxs-lookup"><span data-stu-id="32b78-186">Properties are name/value pairs that can be attached to the message.</span></span> <span data-ttu-id="32b78-187">例如，我們可以修改上述程式碼，將屬性附加至訊息：</span><span class="sxs-lookup"><span data-stu-id="32b78-187">For example, we can modify the previous code to attach a property to the message:</span></span>

```
MAP_HANDLE propMap = IoTHubMessage_Properties(message.messageHandle);
sprintf_s(propText, sizeof(propText), "%d", i);
Map_AddOrUpdate(propMap, "SequenceNumber", propText);
```

<span data-ttu-id="32b78-188">我們從呼叫 **IoTHubMessage\_Properties** 開始著手，然後將訊息的控制代碼傳遞給它。</span><span class="sxs-lookup"><span data-stu-id="32b78-188">We start by calling **IoTHubMessage\_Properties** and passing it the handle of our message.</span></span> <span data-ttu-id="32b78-189">我們得到的回應是 **MAP\_HANDLE** 參考，這可讓我們開始新增屬性。</span><span class="sxs-lookup"><span data-stu-id="32b78-189">What we get back is a **MAP\_HANDLE** reference that enables us to start adding properties.</span></span> <span data-ttu-id="32b78-190">後者可透過呼叫 **Map\_AddOrUpdate** 來完成，這會參考 MAP\_HANDLE、屬性名稱和屬性值。</span><span class="sxs-lookup"><span data-stu-id="32b78-190">The latter is accomplished by calling **Map\_AddOrUpdate**, which takes a reference to a MAP\_HANDLE, the property name, and the property value.</span></span> <span data-ttu-id="32b78-191">利用此 API，我們可以依意願新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="32b78-191">With this API we can add as many properties as we like.</span></span>

<span data-ttu-id="32b78-192">從「事件中樞」讀取事件時，接收者可以列舉屬性並擷取其對應的值。</span><span class="sxs-lookup"><span data-stu-id="32b78-192">When the event is read from **Event Hubs**, the receiver can enumerate the properties and retrieve their corresponding values.</span></span> <span data-ttu-id="32b78-193">例如，在 .NET 中，這可藉由存取 [EventData 物件上的屬性集合](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.eventdata.properties.aspx)來完成。</span><span class="sxs-lookup"><span data-stu-id="32b78-193">For example, in .NET this would be accomplished by accessing the [Properties collection on the EventData object](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.eventdata.properties.aspx).</span></span>

<span data-ttu-id="32b78-194">在上述範例中，我們會將屬性附加至我們傳送給 IoT 中樞的事件。</span><span class="sxs-lookup"><span data-stu-id="32b78-194">In the previous example, we’re attaching properties to an event that we send to IoT Hub.</span></span> <span data-ttu-id="32b78-195">屬性也可以附加至從 IoT 中樞接收的訊息。</span><span class="sxs-lookup"><span data-stu-id="32b78-195">Properties can also be attached to messages received from IoT Hub.</span></span> <span data-ttu-id="32b78-196">如果我們想要從訊息擷取屬性，可以在訊息回呼函式中使用如下的程式碼：</span><span class="sxs-lookup"><span data-stu-id="32b78-196">If we want to retrieve properties from a message, we can use code such as the following in our message callback function:</span></span>

```
static IOTHUBMESSAGE_DISPOSITION_RESULT ReceiveMessageCallback(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    . . .

    // Retrieve properties from the message
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

<span data-ttu-id="32b78-197">對 **IoTHubMessage\_Properties** 的呼叫會傳回 **MAP\_HANDLE** 參考。</span><span class="sxs-lookup"><span data-stu-id="32b78-197">The call to **IoTHubMessage\_Properties** returns the **MAP\_HANDLE** reference.</span></span> <span data-ttu-id="32b78-198">然後，我們會將該參考傳遞給 **Map\_GetInternals**，以取得對名稱/值組陣列的參考 (以及屬性的計數)。</span><span class="sxs-lookup"><span data-stu-id="32b78-198">We then pass that reference to **Map\_GetInternals** to obtain a reference to an array of the name/value pairs (as well as a count of the properties).</span></span> <span data-ttu-id="32b78-199">此時就可以很容易地列舉屬性來取得我們想要的值。</span><span class="sxs-lookup"><span data-stu-id="32b78-199">At that point it's a simple matter of enumerating the properties to get to the values we want.</span></span>

<span data-ttu-id="32b78-200">您不必在應用程式中使用屬性。</span><span class="sxs-lookup"><span data-stu-id="32b78-200">You don't have to use properties in your application.</span></span> <span data-ttu-id="32b78-201">不過，如果您需要在事件上設定它們，或從訊息擷取它們， **IoTHubClient** 程式庫很容易就能辦到。</span><span class="sxs-lookup"><span data-stu-id="32b78-201">However, if you need to set them on events or retrieve them from messages, the **IoTHubClient** library makes it easy.</span></span>

## <a name="message-handling"></a><span data-ttu-id="32b78-202">訊息處理</span><span class="sxs-lookup"><span data-stu-id="32b78-202">Message handling</span></span>
<span data-ttu-id="32b78-203">如先前所述，當訊息從 IoT 中樞送達時， **IoTHubClient** 程式庫會叫用註冊的回呼函式來回應。</span><span class="sxs-lookup"><span data-stu-id="32b78-203">As stated previously, when messages arrive from IoT Hub the **IoTHubClient** library responds by invoking a registered callback function.</span></span> <span data-ttu-id="32b78-204">此函式有一個傳回參數值得額外說明。</span><span class="sxs-lookup"><span data-stu-id="32b78-204">There is a return parameter of this function that deserves some additional explanation.</span></span> <span data-ttu-id="32b78-205">以下是 **iothub\_client\_sample\_http** 範例應用程式中回呼函式的摘錄：</span><span class="sxs-lookup"><span data-stu-id="32b78-205">Here’s an excerpt of the callback function in the **iothub\_client\_sample\_http** sample application:</span></span>

```
static IOTHUBMESSAGE_DISPOSITION_RESULT ReceiveMessageCallback(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    . . .
    return IOTHUBMESSAGE_ACCEPTED;
}
```

<span data-ttu-id="32b78-206">請注意，傳回類型為 **IOTHUBMESSAGE\_DISPOSITION\_RESULT**，而在此特殊案例中，我們會傳回 **IOTHUBMESSAGE\_ACCEPTED**。</span><span class="sxs-lookup"><span data-stu-id="32b78-206">Note that the return type is **IOTHUBMESSAGE\_DISPOSITION\_RESULT** and in this particular case we return **IOTHUBMESSAGE\_ACCEPTED**.</span></span> <span data-ttu-id="32b78-207">我們還有其他的值可從此函式傳回，這些值會變更 **IoTHubClient** 程式庫回應訊息回呼的方式。</span><span class="sxs-lookup"><span data-stu-id="32b78-207">There are other values we can return from this function that change how the **IoTHubClient** library reacts to the message callback.</span></span> <span data-ttu-id="32b78-208">選項如下。</span><span class="sxs-lookup"><span data-stu-id="32b78-208">Here are the options.</span></span>

* <span data-ttu-id="32b78-209">**IOTHUBMESSAGE\_ACCEPTED** – 已成功處理訊息。</span><span class="sxs-lookup"><span data-stu-id="32b78-209">**IOTHUBMESSAGE\_ACCEPTED** – The message has been processed successfully.</span></span> <span data-ttu-id="32b78-210">**IoTHubClient** 程式庫將不會以相同的訊息再次叫用回呼函式。</span><span class="sxs-lookup"><span data-stu-id="32b78-210">The **IoTHubClient** library will not invoke the callback function again with the same message.</span></span>
* <span data-ttu-id="32b78-211">**IOTHUBMESSAGE\_REJECTED** – 未處理訊息，且未來也不打算處理。</span><span class="sxs-lookup"><span data-stu-id="32b78-211">**IOTHUBMESSAGE\_REJECTED** – The message was not processed and there is no desire to do so in the future.</span></span> <span data-ttu-id="32b78-212">**IoTHubClient** 程式庫不得以相同的訊息再次叫用回呼函式。</span><span class="sxs-lookup"><span data-stu-id="32b78-212">The **IoTHubClient** library should not invoke the callback function again with the same message.</span></span>
* <span data-ttu-id="32b78-213">**IOTHUBMESSAGE\_ABANDONED** – 未成功處理訊息，但 **IoTHubClient** 程式庫應以相同的訊息再次叫用回呼函式。</span><span class="sxs-lookup"><span data-stu-id="32b78-213">**IOTHUBMESSAGE\_ABANDONED** – The message was not processed successfully, but the **IoTHubClient** library should invoke the callback function again with the same message.</span></span>

<span data-ttu-id="32b78-214">針對前兩個傳回程式碼， **IoTHubClient** 程式庫會將訊息傳送至 IoT 中樞，代表應該從裝置佇列中刪除訊息且不再傳遞。</span><span class="sxs-lookup"><span data-stu-id="32b78-214">For the first two return codes, the **IoTHubClient** library sends a message to IoT Hub indicating that the message should be deleted from the device queue and not delivered again.</span></span> <span data-ttu-id="32b78-215">最終結果一樣 (從裝置佇列刪除訊息)，但仍會記錄是否已接受或拒絕訊息。</span><span class="sxs-lookup"><span data-stu-id="32b78-215">The net effect is the same (the message is deleted from the device queue), but whether the message was accepted or rejected is still recorded.</span></span>  <span data-ttu-id="32b78-216">對於可聽取意見回應並了解裝置已接受或拒絕特定訊息的訊息傳送者而言，記錄這項區別的功能非常實用。</span><span class="sxs-lookup"><span data-stu-id="32b78-216">Recording this distinction is useful to senders of the message who can listen for feedback and find out if a device has accepted or rejected a particular message.</span></span>

<span data-ttu-id="32b78-217">在最後一個案例中，訊息也會傳送至 IoT 中樞，但它表示應重新傳遞訊息。</span><span class="sxs-lookup"><span data-stu-id="32b78-217">In the last case a message is also sent to IoT Hub, but it indicates that the message should be redelivered.</span></span> <span data-ttu-id="32b78-218">如果您遇到某個錯誤但想要再次嘗試處理訊息，您通常會放棄訊息。</span><span class="sxs-lookup"><span data-stu-id="32b78-218">Typically you’ll abandon a message if you encounter some error but want to try to process the message again.</span></span> <span data-ttu-id="32b78-219">相對地，當您遇到無法復原的錯誤時 (或者如果您只是決定不想處理訊息)，拒絕訊息是適當的方式。</span><span class="sxs-lookup"><span data-stu-id="32b78-219">In contrast, rejecting a message is appropriate when you encounter an unrecoverable error (or if you simply decide you don’t want to process the message).</span></span>

<span data-ttu-id="32b78-220">在任何情況下，請留意不同的傳回程式碼，您就能從 **IoTHubClient** 程式庫引發所需的行為。</span><span class="sxs-lookup"><span data-stu-id="32b78-220">In any case, be aware of the different return codes so that you can elicit the behavior you want from the **IoTHubClient** library.</span></span>

## <a name="alternate-device-credentials"></a><span data-ttu-id="32b78-221">替代裝置認證</span><span class="sxs-lookup"><span data-stu-id="32b78-221">Alternate device credentials</span></span>
<span data-ttu-id="32b78-222">如先前所述，使用 **IoTHubClient** 程式庫時，必須先使用如以下的呼叫來取得 **IOTHUB\_CLIENT\_HANDLE**：</span><span class="sxs-lookup"><span data-stu-id="32b78-222">As explained previously, the first thing to do when working with the **IoTHubClient** library is to obtain a **IOTHUB\_CLIENT\_HANDLE** with a call such as the following:</span></span>

```
IOTHUB_CLIENT_HANDLE iotHubClientHandle;
iotHubClientHandle = IoTHubClient_CreateFromConnectionString(connectionString, AMQP_Protocol);
```

<span data-ttu-id="32b78-223">**IoTHubClient\_CreateFromConnectionString** 的引數是裝置連接字串和一個參數，此參數指出用來與 IoT 中樞通訊的通訊協定。</span><span class="sxs-lookup"><span data-stu-id="32b78-223">The arguments to **IoTHubClient\_CreateFromConnectionString** are the device connection string and a parameter that indicates the protocol we use to communicate with IoT Hub.</span></span> <span data-ttu-id="32b78-224">裝置連接字串的格式如下所示：</span><span class="sxs-lookup"><span data-stu-id="32b78-224">The device connection string has a format that appears as follows:</span></span>

```
HostName=IOTHUBNAME.IOTHUBSUFFIX;DeviceId=DEVICEID;SharedAccessKey=SHAREDACCESSKEY
```

<span data-ttu-id="32b78-225">這個字串中包含四項資訊：IoT 中樞名稱、IoT 中樞尾碼、裝置識別碼和共用存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="32b78-225">There are four pieces of information in this string: IoT Hub name, IoT Hub suffix, device ID, and shared access key.</span></span> <span data-ttu-id="32b78-226">當您在 Azure 入口網站中建立 IoT 中樞執行個體時，可以取得 IoT 中樞的完整網域名稱 (FQDN) - 這可為您提供 IoT 中樞名稱 (FQDN 的第一個部分) 和 IoT 中樞尾碼 (FQDN 的其餘部分)。</span><span class="sxs-lookup"><span data-stu-id="32b78-226">You obtain the fully qualified domain name (FQDN) of an IoT hub when you create your IoT hub instance in the Azure portal — this gives you the IoT hub name (the first part of the FQDN) and the IoT hub suffix (the rest of the FQDN).</span></span> <span data-ttu-id="32b78-227">您會在使用 IoT 中樞註冊裝置時，取得裝置識別碼和共用存取金鑰 (如[前一篇文章](iot-hub-device-sdk-c-intro.md)所述)。</span><span class="sxs-lookup"><span data-stu-id="32b78-227">You get the device ID and the shared access key when you register your device with IoT Hub (as described in the [previous article](iot-hub-device-sdk-c-intro.md)).</span></span>

<span data-ttu-id="32b78-228">**IoTHubClient\_CreateFromConnectionString** 提供您一個方法來初始化程式庫。</span><span class="sxs-lookup"><span data-stu-id="32b78-228">**IoTHubClient\_CreateFromConnectionString** gives you one way to initialize the library.</span></span> <span data-ttu-id="32b78-229">喜歡的話，您也可以使用這些個別的參數 (而不是裝置連接字串) 建立新的 **IOTHUB\_CLIENT\_HANDLE**。</span><span class="sxs-lookup"><span data-stu-id="32b78-229">If you prefer, you can create a new **IOTHUB\_CLIENT\_HANDLE** by using these individual parameters rather than the device connection string.</span></span> <span data-ttu-id="32b78-230">使用下列程式碼即可達成：</span><span class="sxs-lookup"><span data-stu-id="32b78-230">This is achieved with the following code:</span></span>

```
IOTHUB_CLIENT_CONFIG iotHubClientConfig;
iotHubClientConfig.iotHubName = "";
iotHubClientConfig.deviceId = "";
iotHubClientConfig.deviceKey = "";
iotHubClientConfig.iotHubSuffix = "";
iotHubClientConfig.protocol = HTTP_Protocol;
IOTHUB_CLIENT_HANDLE iotHubClientHandle = IoTHubClient_LL_Create(&iotHubClientConfig);
```

<span data-ttu-id="32b78-231">其作用與 **IoTHubClient\_CreateFromConnectionString** 相同。</span><span class="sxs-lookup"><span data-stu-id="32b78-231">This accomplishes the same thing as **IoTHubClient\_CreateFromConnectionString**.</span></span>

<span data-ttu-id="32b78-232">顯而易見，您會想要使用 **IoTHubClient\_CreateFromConnectionString**，而不是這個較冗長的初始化方法。</span><span class="sxs-lookup"><span data-stu-id="32b78-232">It may seem obvious that you would want to use **IoTHubClient\_CreateFromConnectionString** rather than this more verbose method of initialization.</span></span> <span data-ttu-id="32b78-233">但請記住，當您在 IoT 中樞註冊裝置時，您得到的是裝置識別碼和裝置金鑰 (不是連接字串)。</span><span class="sxs-lookup"><span data-stu-id="32b78-233">Keep in mind, however, that when you register a device in IoT Hub what you get is a device ID and device key (not a connection string).</span></span> <span data-ttu-id="32b78-234">[前一篇文章](iot-hub-device-sdk-c-intro.md)介紹的「裝置總管」SDK 工具會使用 **Azure IoT 服務 SDK** 中的程式庫，從裝置識別碼、裝置金鑰及 IoT 中樞主機名稱建立裝置連接字串。</span><span class="sxs-lookup"><span data-stu-id="32b78-234">The *device explorer* SDK tool introduced in the [previous article](iot-hub-device-sdk-c-intro.md) uses libraries in the **Azure IoT service SDK** to create the device connection string from the device ID, device key, and IoT Hub host name.</span></span> <span data-ttu-id="32b78-235">因此，呼叫 **IoTHubClient\_LL\_Create** 可能是較慣用的做法，因為它可以為您省下產生連接字串的步驟。</span><span class="sxs-lookup"><span data-stu-id="32b78-235">So calling **IoTHubClient\_LL\_Create** may be preferable because it saves you the step of generating a connection string.</span></span> <span data-ttu-id="32b78-236">使用任何方法都很方便。</span><span class="sxs-lookup"><span data-stu-id="32b78-236">Use whichever method is convenient.</span></span>

## <a name="configuration-options"></a><span data-ttu-id="32b78-237">組態選項</span><span class="sxs-lookup"><span data-stu-id="32b78-237">Configuration options</span></span>
<span data-ttu-id="32b78-238">到目前為止，有關 **IoTHubClient** 程式庫運作方式的所有描述內容都反映其預設行為。</span><span class="sxs-lookup"><span data-stu-id="32b78-238">So far everything described about the way the **IoTHubClient** library works reflects its default behavior.</span></span> <span data-ttu-id="32b78-239">不過，您可以設定幾個選項來變更程式庫的運作方式。</span><span class="sxs-lookup"><span data-stu-id="32b78-239">However, there are a few options that you can set to change how the library works.</span></span> <span data-ttu-id="32b78-240">這可以藉由運用 **IoTHubClient\_LL\_SetOption** API 來完成。</span><span class="sxs-lookup"><span data-stu-id="32b78-240">This is accomplished by leveraging the **IoTHubClient\_LL\_SetOption** API.</span></span> <span data-ttu-id="32b78-241">請思考此範例：</span><span class="sxs-lookup"><span data-stu-id="32b78-241">Consider this example:</span></span>

```
unsigned int timeout = 30000;
IoTHubClient_LL_SetOption(iotHubClientHandle, "timeout", &timeout);
```

<span data-ttu-id="32b78-242">有一些常用的選項：</span><span class="sxs-lookup"><span data-stu-id="32b78-242">There are a couple of options that are commonly used:</span></span>

* <span data-ttu-id="32b78-243">**SetBatching** (bool) - 如果為 **true**，則傳送到「IoT 中樞」的資料會以批次傳送。</span><span class="sxs-lookup"><span data-stu-id="32b78-243">**SetBatching** (bool) – If **true**, then data sent to IoT Hub is sent in batches.</span></span> <span data-ttu-id="32b78-244">如果為 **false**，就表示訊息會個別傳送。</span><span class="sxs-lookup"><span data-stu-id="32b78-244">If **false**, then messages are sent individually.</span></span> <span data-ttu-id="32b78-245">預設值為 **false**。</span><span class="sxs-lookup"><span data-stu-id="32b78-245">The default is **false**.</span></span> <span data-ttu-id="32b78-246">請注意，**SetBatching** 選項僅適用於 HTTP 通訊協定，不適用於 MQTT 或 AMQP 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="32b78-246">Note that the **SetBatching** option only applies to the HTTP protocol and not to the MQTT or AMQP protocols.</span></span>
* <span data-ttu-id="32b78-247">**Timeout** (unsigned int) - 這個值會以毫秒為單位表示。</span><span class="sxs-lookup"><span data-stu-id="32b78-247">**Timeout** (unsigned int) – This value is represented in milliseconds.</span></span> <span data-ttu-id="32b78-248">如果傳送 HTTP 要求或接收回應所花費的時間超過這個時間，即表示連接逾時。</span><span class="sxs-lookup"><span data-stu-id="32b78-248">If sending an HTTP request or receiving a response takes longer than this time, then the connection times out.</span></span>

<span data-ttu-id="32b78-249">此批次處理選項極為重要。</span><span class="sxs-lookup"><span data-stu-id="32b78-249">The batching option is important.</span></span> <span data-ttu-id="32b78-250">根據預設，程式庫會個別輸入事件 (單一事件是您傳遞給 **IoTHubClient\_LL\_SendEventAsync** 的任何內容)。</span><span class="sxs-lookup"><span data-stu-id="32b78-250">By default, the library ingresses events individually (a single event is whatever you pass to **IoTHubClient\_LL\_SendEventAsync**).</span></span> <span data-ttu-id="32b78-251">如果批次處理選項為 **true**，程式庫會盡可能從緩衝區收集事件 (上限為 IoT 中樞將接受的最大訊息大小)。</span><span class="sxs-lookup"><span data-stu-id="32b78-251">If the batching option is **true**, the library collects as many events as it can from the buffer (up to the maximum message size that IoT Hub will accept).</span></span>  <span data-ttu-id="32b78-252">事件批次會在單一 HTTP 呼叫中傳送到 IoT 中樞 (個別事件已統合至 JSON 陣列中)。</span><span class="sxs-lookup"><span data-stu-id="32b78-252">The event batch is sent to IoT Hub in a single HTTP call (the individual events are bundled into a JSON array).</span></span> <span data-ttu-id="32b78-253">啟用批次處理通常會導致效能大幅提升，因為網路來回行程正在減少。</span><span class="sxs-lookup"><span data-stu-id="32b78-253">Enabling batching typically results in big performance gains since you’re reducing network round-trips.</span></span> <span data-ttu-id="32b78-254">它也會大幅減少頻寬，因為您正利用事件批次傳送一組 HTTP 標頭，而不是針對每個個別事件傳送一組標頭。</span><span class="sxs-lookup"><span data-stu-id="32b78-254">It also significantly reduces bandwidth since you are sending one set of HTTP headers with an event batch rather than a set of headers for each individual event.</span></span> <span data-ttu-id="32b78-255">除非您有使用其他方式的特定理由，否則通常會想要啟用批次處理。</span><span class="sxs-lookup"><span data-stu-id="32b78-255">Unless you have a specific reason to do otherwise, typically you’ll want to enable batching.</span></span>

## <a name="next-steps"></a><span data-ttu-id="32b78-256">後續步驟</span><span class="sxs-lookup"><span data-stu-id="32b78-256">Next steps</span></span>
<span data-ttu-id="32b78-257">本文詳細說明「適用於 C 的 Azure IoT 裝置 SDK」中所發現 **IoTHubClient** 程式庫的行為。利用這項資訊，您應可充分了解 **IoTHubClient** 程式庫的功能。</span><span class="sxs-lookup"><span data-stu-id="32b78-257">This article describes in detail the behavior of the **IoTHubClient** library found in the **Azure IoT device SDK for C**. With this information, you should have a good understanding of the capabilities of the **IoTHubClient** library.</span></span> <span data-ttu-id="32b78-258">[下一篇文章](iot-hub-device-sdk-c-serializer.md) 將提供 **序列化程式** 庫的類似詳細資料。</span><span class="sxs-lookup"><span data-stu-id="32b78-258">The [next article](iot-hub-device-sdk-c-serializer.md) provides similar detail on the **serializer** library.</span></span>

<span data-ttu-id="32b78-259">若要深入了解如何開發 IoT 中樞，請參閱 [Azure IoT SDK][lnk-sdks]。</span><span class="sxs-lookup"><span data-stu-id="32b78-259">To learn more about developing for IoT Hub, see the [Azure IoT SDKs][lnk-sdks].</span></span>

<span data-ttu-id="32b78-260">若要進一步探索 IoT 中樞的功能，請參閱︰</span><span class="sxs-lookup"><span data-stu-id="32b78-260">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="32b78-261">[使用 Azure IoT Edge 來模擬裝置][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="32b78-261">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
