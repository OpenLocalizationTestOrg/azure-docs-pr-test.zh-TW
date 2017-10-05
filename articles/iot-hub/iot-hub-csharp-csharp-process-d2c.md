---
title: "使用路由處理 Azure IoT 中樞的裝置到雲端訊息 (.Net) | Microsoft Docs"
description: "如何使用路由規則和自訂端點來處理 IoT 中樞的裝置到雲端訊息，以將訊息分派至其他後端服務。"
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 5177bac9-722f-47ef-8a14-b201142ba4bc
ms.service: iot-hub
ms.devlang: csharp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 1d2b52ea005ab520bf294efa603512c00a92ee63
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="process-iot-hub-device-to-cloud-messages-using-routes-net"></a><span data-ttu-id="cdcab-103">使用路由處理 Azure IoT 中樞的裝置到雲端訊息 (.NET)</span><span class="sxs-lookup"><span data-stu-id="cdcab-103">Process IoT Hub device-to-cloud messages using routes (.NET)</span></span>

[!INCLUDE [iot-hub-selector-process-d2c](../../includes/iot-hub-selector-process-d2c.md)]

<span data-ttu-id="cdcab-104">本教學課程是以[開始使用 IoT 中樞]教學課程為基礎。</span><span class="sxs-lookup"><span data-stu-id="cdcab-104">This tutorial builds on the [Get started with IoT Hub] tutorial.</span></span> <span data-ttu-id="cdcab-105">教學課程會：</span><span class="sxs-lookup"><span data-stu-id="cdcab-105">The tutorial:</span></span>

* <span data-ttu-id="cdcab-106">說明如何使用路由規則，以簡單的設定方式來分派裝置到雲端訊息。</span><span class="sxs-lookup"><span data-stu-id="cdcab-106">Shows you how to use routing rules to dispatch device-to-cloud messages in an easy, configuration-based way.</span></span>
* <span data-ttu-id="cdcab-107">說明如何從解決方案後端隔離需要立即採取行動的互動式訊息，以便進一步處理。</span><span class="sxs-lookup"><span data-stu-id="cdcab-107">Illustrates how to isolate interactive messages that require immediate action from the solution back end for further processing.</span></span> <span data-ttu-id="cdcab-108">例如，裝置可能會傳送一則警示訊息，以觸發將票證插入 CRM 系統的作業。</span><span class="sxs-lookup"><span data-stu-id="cdcab-108">For example, a device might send an alarm message that triggers inserting a ticket into a CRM system.</span></span> <span data-ttu-id="cdcab-109">相較之下，資料點訊息 (例如溫度遙測) 只會饋送至分析引擎。</span><span class="sxs-lookup"><span data-stu-id="cdcab-109">In contrast, data-point messages, such as temperature telemetry, feed into an analytics engine.</span></span>

<span data-ttu-id="cdcab-110">在本教學課程結尾處，您會執行三個 .NET 主控台應用程式：</span><span class="sxs-lookup"><span data-stu-id="cdcab-110">At the end of this tutorial, you run three .NET console apps:</span></span>

* <span data-ttu-id="cdcab-111">**SimulatedDevice** (修改自[開始使用 IoT 中樞]教學課程中所建立的應用程式) 每秒會傳送資料點的裝置到雲端訊息，而且每 10 秒會傳送互動式裝置到雲端訊息。</span><span class="sxs-lookup"><span data-stu-id="cdcab-111">**SimulatedDevice**, a modified version of the app created in the [Get started with IoT Hub] tutorial sends data-point device-to-cloud messages every second, and interactive device-to-cloud messages every 10 seconds.</span></span>
* <span data-ttu-id="cdcab-112">**ReadDeviceToCloudMessages** 會顯示裝置應用程式所傳送的非關鍵性遙測。</span><span class="sxs-lookup"><span data-stu-id="cdcab-112">**ReadDeviceToCloudMessages** that displays the non-critical telemetry sent by your device app.</span></span>
* <span data-ttu-id="cdcab-113">**ReadCriticalQueue** 可從服務匯流排佇列中移除裝置應用程式所傳送的重要訊息。</span><span class="sxs-lookup"><span data-stu-id="cdcab-113">**ReadCriticalQueue** de-queues the critical messages sent by your device app from a Service Bus queue.</span></span> <span data-ttu-id="cdcab-114">此佇列連結至 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="cdcab-114">This queue is attached to the IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="cdcab-115">IoT 中樞對於許多裝置平台和語言 (包括 C、Java 和 JavaScript) 提供 SDK 支援。</span><span class="sxs-lookup"><span data-stu-id="cdcab-115">IoT Hub has SDK support for many device platforms and languages, including C, Java, and JavaScript.</span></span> <span data-ttu-id="cdcab-116">若要了解如何以實體裝置取代本教學課程中的模擬裝置，請參閱 [Azure IoT 開發人員中心]。</span><span class="sxs-lookup"><span data-stu-id="cdcab-116">To learn how to replace the simulated device in this tutorial with a physical device, see the [Azure IoT Developer Center].</span></span>

<span data-ttu-id="cdcab-117">若要完成此教學課程，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="cdcab-117">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="cdcab-118">Visual Studio 2015 或 Visual Studio 2017。</span><span class="sxs-lookup"><span data-stu-id="cdcab-118">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="cdcab-119">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="cdcab-119">An active Azure account.</span></span> <br/><span data-ttu-id="cdcab-120">如果您沒有帳戶，只需要幾分鐘的時間就可以建立 [免費帳戶](https://azure.microsoft.com/free/) 。</span><span class="sxs-lookup"><span data-stu-id="cdcab-120">If you don't have an account, you can create a [free account](https://azure.microsoft.com/free/) in just a couple of minutes.</span></span>

<span data-ttu-id="cdcab-121">您應具備 [Azure 儲存體]和 [Azure 服務匯流排]的基本知識。</span><span class="sxs-lookup"><span data-stu-id="cdcab-121">You should have some basic knowledge of [Azure Storage] and [Azure Service Bus].</span></span>

## <a name="send-interactive-messages"></a><span data-ttu-id="cdcab-122">傳送互動式訊息</span><span class="sxs-lookup"><span data-stu-id="cdcab-122">Send interactive messages</span></span>

<span data-ttu-id="cdcab-123">修改在[開始使用 IoT 中樞]教學課程中建立的裝置應用程式，偶爾傳送互動式訊息。</span><span class="sxs-lookup"><span data-stu-id="cdcab-123">Modify the device app you created in the [Get started with IoT Hub] tutorial to occasionally send interactive messages.</span></span>

<span data-ttu-id="cdcab-124">在 Visual Studio 的 **SimulatedDevice** 專案中，以下列程式碼取代 `SendDeviceToCloudMessagesAsync` 方法：</span><span class="sxs-lookup"><span data-stu-id="cdcab-124">In Visual Studio, in the **SimulatedDevice** project, replace the `SendDeviceToCloudMessagesAsync` method with the following code:</span></span>

```csharp
private static async void SendDeviceToCloudMessagesAsync()
{
    double minTemperature = 20;
    double minHumidity = 60;
    Random rand = new Random();

    while (true)
    {
        double currentTemperature = minTemperature + rand.NextDouble() * 15;
        double currentHumidity = minHumidity + rand.NextDouble() * 20;

        var telemetryDataPoint = new
        {
            deviceId = "myFirstDevice",
            temperature = currentTemperature,
            humidity = currentHumidity
        };
        var messageString = JsonConvert.SerializeObject(telemetryDataPoint);
        string levelValue;

        if (rand.NextDouble() > 0.7)
        {
            messageString = "This is a critical message";
            levelValue = "critical";
        }
        else
        {
            levelValue = "normal";
        }
        
        var message = new Message(Encoding.ASCII.GetBytes(messageString));
        message.Properties.Add("level", levelValue);
        
        await deviceClient.SendEventAsync(message);
        Console.WriteLine("{0} > Sent message: {1}", DateTime.Now, messageString);

        await Task.Delay(1000);
    }
}
```

<span data-ttu-id="cdcab-125">這個方法會隨機將 `"level": "critical"` 屬性新增至裝置所傳送的訊息，該裝置會模擬需要解決方案後端立即採取行動的訊息。</span><span class="sxs-lookup"><span data-stu-id="cdcab-125">This method randomly adds the property `"level": "critical"` to messages sent by the device, which simulates a message that requires immediate action by the solution back-end.</span></span> <span data-ttu-id="cdcab-126">裝置應用程式會在訊息屬性中傳遞此資訊，而不是在訊息主體中傳遞，因此 IoT 中樞可以將訊息路由傳送至適當的訊息目的地。</span><span class="sxs-lookup"><span data-stu-id="cdcab-126">The device app passes this information in the message properties, instead of in the message body, so that IoT Hub can route the message to the proper message destination.</span></span>

> [!NOTE]
> <span data-ttu-id="cdcab-127">除了此處顯示的最忙碌路徑範例以外，您可以使用訊息屬性來路由傳送各種案例的訊息，包括冷門路徑處理。</span><span class="sxs-lookup"><span data-stu-id="cdcab-127">You can use message properties to route messages for various scenarios including cold-path processing, in addition to the hot-path example shown here.</span></span>

> [!NOTE]
> <span data-ttu-id="cdcab-128">為了簡單起見，本教學課程不會實作任何重試原則。</span><span class="sxs-lookup"><span data-stu-id="cdcab-128">For the sake of simplicity, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="cdcab-129">在實際程式碼中，您應該如 MSDN 文章 [Transient Fault Handling (暫時性錯誤處理)]所建議來實作重試原則 (例如指數型輪詢)。</span><span class="sxs-lookup"><span data-stu-id="cdcab-129">In production code, you should implement a retry policy such as exponential backoff, as suggested in the MSDN article [Transient Fault Handling].</span></span>

## <a name="route-messages-to-a-queue-in-your-iot-hub"></a><span data-ttu-id="cdcab-130">將訊息路由至 IoT 中樞中的佇列</span><span class="sxs-lookup"><span data-stu-id="cdcab-130">Route messages to a queue in your IoT hub</span></span>

<span data-ttu-id="cdcab-131">在本節中，您可：</span><span class="sxs-lookup"><span data-stu-id="cdcab-131">In this section, you:</span></span>

* <span data-ttu-id="cdcab-132">建立服務匯流排佇列。</span><span class="sxs-lookup"><span data-stu-id="cdcab-132">Create a Service Bus queue.</span></span>
* <span data-ttu-id="cdcab-133">將它連接到您的 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="cdcab-133">Connect it to your IoT hub.</span></span>
* <span data-ttu-id="cdcab-134">設定您的 IoT 中樞，根據訊息上存在的屬性將訊息傳送到佇列。</span><span class="sxs-lookup"><span data-stu-id="cdcab-134">Configure your IoT hub to send messages to the queue based on the presence of a property on the message.</span></span>

<span data-ttu-id="cdcab-135">如需有關如何處理來自服務匯流排佇列之訊息的詳細資訊，請參閱[開始使用佇列][Service Bus queue]。</span><span class="sxs-lookup"><span data-stu-id="cdcab-135">For more information about how to process messages from Service Bus queues, see [Get started with queues][Service Bus queue].</span></span>

1. <span data-ttu-id="cdcab-136">如[開始使用佇列][Service Bus queue]所述，建立服務匯流排佇列。</span><span class="sxs-lookup"><span data-stu-id="cdcab-136">Create a Service Bus queue as described in [Get started with queues][Service Bus queue].</span></span> <span data-ttu-id="cdcab-137">此佇列必須與您的 IoT 中樞位於相同的訂用帳戶和區域中。</span><span class="sxs-lookup"><span data-stu-id="cdcab-137">The queue must be in the same subscription and region as your IoT hub.</span></span> <span data-ttu-id="cdcab-138">記下命名空間和佇列名稱。</span><span class="sxs-lookup"><span data-stu-id="cdcab-138">Make a note of the namespace and queue name.</span></span>

    > [!NOTE]
    > <span data-ttu-id="cdcab-139">作為 IoT 中樞端點的服務匯流排佇列和主題不能啟用 [工作階段] 或 [重複偵測]。</span><span class="sxs-lookup"><span data-stu-id="cdcab-139">Service Bus queues and topics used as IoT Hub endpoints must not have **Sessions** or **Duplicate Detection** enabled.</span></span> <span data-ttu-id="cdcab-140">如果已啟用其中一個選項，端點會在 Azure 入口網站中顯示為 [無法連線]。</span><span class="sxs-lookup"><span data-stu-id="cdcab-140">If either of those options are enabled, the endpoint appears as **Unreachable** in the Azure portal.</span></span>

2. <span data-ttu-id="cdcab-141">在 Azure 入口網站中，開啟 IoT 中樞然後按一下 [端點]。</span><span class="sxs-lookup"><span data-stu-id="cdcab-141">In the Azure portal, open your IoT hub and click **Endpoints**.</span></span>
    
    ![IoT 中樞端點][30]

3. <span data-ttu-id="cdcab-143">在 [端點] 刀鋒視窗中，按一下頂端的 [新增] 將您的佇列新增至 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="cdcab-143">In the **Endpoints** blade, click **Add** at the top to add your queue to your IoT hub.</span></span> <span data-ttu-id="cdcab-144">將端點命名為 **CriticalQueue**，並使用下拉式清單來選取 [服務匯流排佇列]、您的佇列所在的服務匯流排命名空間，以及您的佇列名稱。</span><span class="sxs-lookup"><span data-stu-id="cdcab-144">Name the endpoint **CriticalQueue** and use the drop-downs to select **Service Bus queue**, the Service Bus namespace in which your queue resides, and the name of your queue.</span></span> <span data-ttu-id="cdcab-145">完成時，請按一下底部的 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="cdcab-145">When you are done, click **Save** at the bottom.</span></span>
    
    ![新增端點][31]
    
4. <span data-ttu-id="cdcab-147">現在按一下 IoT 中樞中的 [路由]。</span><span class="sxs-lookup"><span data-stu-id="cdcab-147">Now click **Routes** in your IoT Hub.</span></span> <span data-ttu-id="cdcab-148">按一下刀鋒視窗頂端的 [新增] 來建立路由規則，以便將訊息路由傳送至您剛才新增的佇列。</span><span class="sxs-lookup"><span data-stu-id="cdcab-148">Click **Add** at the top of the blade to create a routing rule that routes messages to the queue you just added.</span></span> <span data-ttu-id="cdcab-149">選取 **DeviceTelemetry** 做為資料來源。</span><span class="sxs-lookup"><span data-stu-id="cdcab-149">Select **DeviceTelemetry** as the source of data.</span></span> <span data-ttu-id="cdcab-150">輸入 `level="critical"` 做為條件，然後選擇您剛才新增為自訂端點的佇列做為路由規則端點。</span><span class="sxs-lookup"><span data-stu-id="cdcab-150">Enter `level="critical"` as the condition, and choose the queue you just added as a custom endpoint as the routing rule endpoint.</span></span> <span data-ttu-id="cdcab-151">完成時，請按一下底部的 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="cdcab-151">When you are done, click **Save** at the bottom.</span></span>
    
    ![新增路由][32]
    
    <span data-ttu-id="cdcab-153">確定後援路由設定為 [開啟]。</span><span class="sxs-lookup"><span data-stu-id="cdcab-153">Make sure the fallback route is set to **ON**.</span></span> <span data-ttu-id="cdcab-154">這個值是 IoT 中樞的預設設定。</span><span class="sxs-lookup"><span data-stu-id="cdcab-154">This value is the default configuration for an IoT hub.</span></span>
    
    ![後援路由][33]

## <a name="read-from-the-queue-endpoint"></a><span data-ttu-id="cdcab-156">從佇列端點讀取</span><span class="sxs-lookup"><span data-stu-id="cdcab-156">Read from the queue endpoint</span></span>

<span data-ttu-id="cdcab-157">在本節中，您會讀取佇列端點中的訊息。</span><span class="sxs-lookup"><span data-stu-id="cdcab-157">In this section, you read the messages from the queue endpoint.</span></span>

1. <span data-ttu-id="cdcab-158">在 Visual Studio 中，使用 [主控台應用程式 (.NET Framework)] 專案範本，將 Visual C# Windows 傳統桌面專案新增至目前的方案。</span><span class="sxs-lookup"><span data-stu-id="cdcab-158">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution, by using the **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="cdcab-159">將專案命名為 **ReadCriticalQueue**。</span><span class="sxs-lookup"><span data-stu-id="cdcab-159">Name the project **ReadCriticalQueue**.</span></span>

2. <span data-ttu-id="cdcab-160">在 [方案總管] 中，以滑鼠右鍵按一下 **ReadCriticalQueue** 專案，然後按一下 [管理 NuGet 套件]。</span><span class="sxs-lookup"><span data-stu-id="cdcab-160">In Solution Explorer, right-click the **ReadCriticalQueue** project, and then click **Manage NuGet Packages**.</span></span> <span data-ttu-id="cdcab-161">此操作會顯示 [NuGet 套件管理員]  視窗。</span><span class="sxs-lookup"><span data-stu-id="cdcab-161">This operation displays the **NuGet Package Manager** window.</span></span>

3. <span data-ttu-id="cdcab-162">搜尋 **WindowsAzure.ServiceBus**，按一下 [安裝]，然後接受使用規定。</span><span class="sxs-lookup"><span data-stu-id="cdcab-162">Search for **WindowsAzure.ServiceBus**, click **Install**, and accept the terms of use.</span></span> <span data-ttu-id="cdcab-163">此操作會對 Azure 服務匯流排及其所有相依性進行下載、安裝和新增參考。</span><span class="sxs-lookup"><span data-stu-id="cdcab-163">This operation downloads, installs, and adds a reference to the Azure Service Bus, with all its dependencies.</span></span>

4. <span data-ttu-id="cdcab-164">在 **Program.cs** 檔案的最上方，新增下列 **using** 陳述式：</span><span class="sxs-lookup"><span data-stu-id="cdcab-164">Add the following **using** statements at the top of the **Program.cs** file:</span></span>
   
    ```csharp
    using System.IO;
    using Microsoft.ServiceBus.Messaging;
    ```

5. <span data-ttu-id="cdcab-165">最後，將下列幾行新增到 **Main** 方法中。</span><span class="sxs-lookup"><span data-stu-id="cdcab-165">Finally, add the following lines to the **Main** method.</span></span> <span data-ttu-id="cdcab-166">以佇列的 **Listen** 權限取代連接字串：</span><span class="sxs-lookup"><span data-stu-id="cdcab-166">Substitute the connection string with **Listen** permissions for the queue:</span></span>
   
    ```csharp
    Console.WriteLine("Receive critical messages. Ctrl-C to exit.\n");
    var connectionString = "{service bus listen string}";
    var queueName = "{queue name}";
    
    var client = QueueClient.CreateFromConnectionString(connectionString, queueName);

    client.OnMessage(message =>
        {
            Stream stream = message.GetBody<Stream>();
            StreamReader reader = new StreamReader(stream, Encoding.ASCII);
            string s = reader.ReadToEnd();
            Console.WriteLine(String.Format("Message body: {0}", s));
        });
        
    Console.ReadLine();
    ```

## <a name="run-the-applications"></a><span data-ttu-id="cdcab-167">執行應用程式</span><span class="sxs-lookup"><span data-stu-id="cdcab-167">Run the applications</span></span>
<span data-ttu-id="cdcab-168">現在您已經準備好執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="cdcab-168">Now you are ready to run the applications.</span></span>

1. <span data-ttu-id="cdcab-169">在 Visual Studio 的方案總管中，以滑鼠右鍵按一下您的方案，然後選取 [設定啟始專案]。</span><span class="sxs-lookup"><span data-stu-id="cdcab-169">In Visual Studio, in Solution Explorer, right-click your solution and select **Set StartUp Projects**.</span></span> <span data-ttu-id="cdcab-170">選取 [多個啟始專案]，然後針對 **ReadDeviceToCloudMessages**、**SimulatedDevice** 和 **ReadCriticalQueue** 專案選取 [啟動] 做為動作。</span><span class="sxs-lookup"><span data-stu-id="cdcab-170">Select **Multiple startup projects**, then select **Start** as the action for the **ReadDeviceToCloudMessages**, **SimulatedDevice**, and **ReadCriticalQueue** projects.</span></span>
2. <span data-ttu-id="cdcab-171">按 **F5** 啟動三個主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="cdcab-171">Press **F5** to start the three console apps.</span></span> <span data-ttu-id="cdcab-172">**ReadDeviceToCloudMessages** 應用程式只有從 **SimulatedDevice** 應用程式傳送的非重要訊息，而 **ReadCriticalQueue** 應用程式只有重要訊息。</span><span class="sxs-lookup"><span data-stu-id="cdcab-172">The **ReadDeviceToCloudMessages** app has only non-critical messages sent from the **SimulatedDevice** application, and the **ReadCriticalQueue** app has only critical messages.</span></span>
   
   ![三個主控台應用程式][50]

## <a name="next-steps"></a><span data-ttu-id="cdcab-174">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cdcab-174">Next steps</span></span>
<span data-ttu-id="cdcab-175">在本教學課程中，您已學到如何使用 IoT 中樞的訊息路由功能來可靠地分派裝置到雲端訊息。</span><span class="sxs-lookup"><span data-stu-id="cdcab-175">In this tutorial, you learned how to reliably dispatch device-to-cloud messages by using the message routing functionality of IoT Hub.</span></span>

<span data-ttu-id="cdcab-176">[如何使用 IoT 中樞傳送雲端到裝置訊息][lnk-c2d]示範如何從解決方案後端將訊息傳送至您的裝置。</span><span class="sxs-lookup"><span data-stu-id="cdcab-176">The [How to send cloud-to-device messages with IoT Hub][lnk-c2d] shows you how to send messages to your devices from your solution back end.</span></span>

<span data-ttu-id="cdcab-177">若要查看使用 IoT 中樞的完整端對端解決方案範例，請參閱 [Azure IoT 套件][lnk-suite]。</span><span class="sxs-lookup"><span data-stu-id="cdcab-177">To see examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Suite][lnk-suite].</span></span>

<span data-ttu-id="cdcab-178">若要深入了解如何使用 IoT 中樞開發解決方案，請參閱 [IoT 中樞開發人員指南]。</span><span class="sxs-lookup"><span data-stu-id="cdcab-178">To learn more about developing solutions with IoT Hub, see the [IoT Hub developer guide].</span></span>

<span data-ttu-id="cdcab-179">若要深入了解 IoT 中樞的訊息路由，請參閱[使用 IoT 中樞傳送和接收訊息][lnk-devguide-messaging]。</span><span class="sxs-lookup"><span data-stu-id="cdcab-179">To learn more about message routing in IoT Hub, see [Send and receive messages with IoT Hub][lnk-devguide-messaging].</span></span>

<!-- Images. -->
[50]: ./media/iot-hub-csharp-csharp-process-d2c/run1.png
[30]: ./media/iot-hub-csharp-csharp-process-d2c/click-endpoints.png
[31]: ./media/iot-hub-csharp-csharp-process-d2c/endpoint-creation.png
[32]: ./media/iot-hub-csharp-csharp-process-d2c/route-creation.png
[33]: ./media/iot-hub-csharp-csharp-process-d2c/fallback-route.png

<!-- Links -->
[Service Bus queue]: ../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md
<span data-ttu-id="cdcab-180">[Azure 儲存體]: https://azure.microsoft.com/documentation/services/storage/</span><span class="sxs-lookup"><span data-stu-id="cdcab-180">[Azure Storage]: https://azure.microsoft.com/documentation/services/storage/</span></span>
<span data-ttu-id="cdcab-181">[Azure 服務匯流排]: https://azure.microsoft.com/documentation/services/service-bus/</span><span class="sxs-lookup"><span data-stu-id="cdcab-181">[Azure Service Bus]: https://azure.microsoft.com/documentation/services/service-bus/</span></span>
<span data-ttu-id="cdcab-182">[IoT 中樞開發人員指南]: iot-hub-devguide.md</span><span class="sxs-lookup"><span data-stu-id="cdcab-182">[IoT Hub developer guide]: iot-hub-devguide.md</span></span>
<span data-ttu-id="cdcab-183">[開始使用 IoT 中樞]: iot-hub-csharp-csharp-getstarted.md</span><span class="sxs-lookup"><span data-stu-id="cdcab-183">[Get started with IoT Hub]: iot-hub-csharp-csharp-getstarted.md</span></span>
[lnk-devguide-messaging]: iot-hub-devguide-messaging.md
<span data-ttu-id="cdcab-184">[Azure IoT 開發人員中心]: https://azure.microsoft.com/develop/iot</span><span class="sxs-lookup"><span data-stu-id="cdcab-184">[Azure IoT Developer Center]: https://azure.microsoft.com/develop/iot</span></span>
<span data-ttu-id="cdcab-185">[Transient Fault Handling (暫時性錯誤處理)]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx</span><span class="sxs-lookup"><span data-stu-id="cdcab-185">[Transient Fault Handling]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx</span></span>
[lnk-c2d]: iot-hub-csharp-csharp-process-d2c.md
[lnk-suite]: https://azure.microsoft.com/documentation/suites/iot-suite/
