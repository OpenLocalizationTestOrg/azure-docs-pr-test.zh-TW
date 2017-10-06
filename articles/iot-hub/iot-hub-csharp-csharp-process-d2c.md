---
title: "使用路由 (.Net) aaaProcess Azure IoT Hub 裝置到雲端訊息 |Microsoft 文件"
description: "如何使用路由規則和自訂端點 toodispatch IoT 中樞裝置到雲端訊息 tooprocess 訊息 tooother 後端服務。"
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
ms.openlocfilehash: c1dd5be04ca30c65af2be466ba6c8c1858333154
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="process-iot-hub-device-to-cloud-messages-using-routes-net"></a><span data-ttu-id="b1aa6-103">使用路由處理 Azure IoT 中樞的裝置到雲端訊息 (.NET)</span><span class="sxs-lookup"><span data-stu-id="b1aa6-103">Process IoT Hub device-to-cloud messages using routes (.NET)</span></span>

[!INCLUDE [iot-hub-selector-process-d2c](../../includes/iot-hub-selector-process-d2c.md)]

<span data-ttu-id="b1aa6-104">本教學課程是 hello[開始使用 IoT 中樞]教學課程。</span><span class="sxs-lookup"><span data-stu-id="b1aa6-104">This tutorial builds on hello [Get started with IoT Hub] tutorial.</span></span> <span data-ttu-id="b1aa6-105">hello 教學課程：</span><span class="sxs-lookup"><span data-stu-id="b1aa6-105">hello tutorial:</span></span>

* <span data-ttu-id="b1aa6-106">顯示如何 toouse 路由規則 toodispatch 裝置到雲端訊息以簡單、 以組態為基礎的方式。</span><span class="sxs-lookup"><span data-stu-id="b1aa6-106">Shows you how toouse routing rules toodispatch device-to-cloud messages in an easy, configuration-based way.</span></span>
* <span data-ttu-id="b1aa6-107">說明 tooisolate 互動式訊息需要立即採取行動 hello 方案從傳回的進一步處理結束的方式。</span><span class="sxs-lookup"><span data-stu-id="b1aa6-107">Illustrates how tooisolate interactive messages that require immediate action from hello solution back end for further processing.</span></span> <span data-ttu-id="b1aa6-108">例如，裝置可能會傳送一則警示訊息，以觸發將票證插入 CRM 系統的作業。</span><span class="sxs-lookup"><span data-stu-id="b1aa6-108">For example, a device might send an alarm message that triggers inserting a ticket into a CRM system.</span></span> <span data-ttu-id="b1aa6-109">相較之下，資料點訊息 (例如溫度遙測) 只會饋送至分析引擎。</span><span class="sxs-lookup"><span data-stu-id="b1aa6-109">In contrast, data-point messages, such as temperature telemetry, feed into an analytics engine.</span></span>

<span data-ttu-id="b1aa6-110">在本教學課程的 hello 最後，您可以執行三個.NET 主控台應用程式：</span><span class="sxs-lookup"><span data-stu-id="b1aa6-110">At hello end of this tutorial, you run three .NET console apps:</span></span>

* <span data-ttu-id="b1aa6-111">**SimulatedDevice**，hello hello 中建立的應用程式的修改的版本[開始使用 IoT 中樞]教學課程傳送的資料點裝置到雲端訊息每秒，而互動式裝置到雲端訊息每隔 10秒數。</span><span class="sxs-lookup"><span data-stu-id="b1aa6-111">**SimulatedDevice**, a modified version of hello app created in hello [Get started with IoT Hub] tutorial sends data-point device-to-cloud messages every second, and interactive device-to-cloud messages every 10 seconds.</span></span>
* <span data-ttu-id="b1aa6-112">**ReadDeviceToCloudMessages**顯示 hello 裝置之應用程式所傳送的非關鍵遙測。</span><span class="sxs-lookup"><span data-stu-id="b1aa6-112">**ReadDeviceToCloudMessages** that displays hello non-critical telemetry sent by your device app.</span></span>
* <span data-ttu-id="b1aa6-113">**ReadCriticalQueue**取消佇列 hello 重大裝置之應用程式所傳送來自服務匯流排佇列的訊息。</span><span class="sxs-lookup"><span data-stu-id="b1aa6-113">**ReadCriticalQueue** de-queues hello critical messages sent by your device app from a Service Bus queue.</span></span> <span data-ttu-id="b1aa6-114">此佇列為附加的 toohello IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="b1aa6-114">This queue is attached toohello IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="b1aa6-115">IoT 中樞對於許多裝置平台和語言 (包括 C、Java 和 JavaScript) 提供 SDK 支援。</span><span class="sxs-lookup"><span data-stu-id="b1aa6-115">IoT Hub has SDK support for many device platforms and languages, including C, Java, and JavaScript.</span></span> <span data-ttu-id="b1aa6-116">toolearn 如何 tooreplace 本教學課程中模擬的裝置 hello 與實體裝置，請參閱 hello [Azure IoT 開發人員中心]。</span><span class="sxs-lookup"><span data-stu-id="b1aa6-116">toolearn how tooreplace hello simulated device in this tutorial with a physical device, see hello [Azure IoT Developer Center].</span></span>

<span data-ttu-id="b1aa6-117">toocomplete 本教學課程中，您需要遵循的 hello:</span><span class="sxs-lookup"><span data-stu-id="b1aa6-117">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="b1aa6-118">Visual Studio 2015 或 Visual Studio 2017。</span><span class="sxs-lookup"><span data-stu-id="b1aa6-118">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="b1aa6-119">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="b1aa6-119">An active Azure account.</span></span> <br/><span data-ttu-id="b1aa6-120">如果您沒有帳戶，只需要幾分鐘的時間就可以建立 [免費帳戶](https://azure.microsoft.com/free/) 。</span><span class="sxs-lookup"><span data-stu-id="b1aa6-120">If you don't have an account, you can create a [free account](https://azure.microsoft.com/free/) in just a couple of minutes.</span></span>

<span data-ttu-id="b1aa6-121">您應具備 [Azure 儲存體]和 [Azure 服務匯流排]的基本知識。</span><span class="sxs-lookup"><span data-stu-id="b1aa6-121">You should have some basic knowledge of [Azure Storage] and [Azure Service Bus].</span></span>

## <a name="send-interactive-messages"></a><span data-ttu-id="b1aa6-122">傳送互動式訊息</span><span class="sxs-lookup"><span data-stu-id="b1aa6-122">Send interactive messages</span></span>

<span data-ttu-id="b1aa6-123">修改 hello 裝置應用程式，您可以在 hello[開始使用 IoT 中樞]教學課程 toooccasionally 傳送互動的訊息。</span><span class="sxs-lookup"><span data-stu-id="b1aa6-123">Modify hello device app you created in hello [Get started with IoT Hub] tutorial toooccasionally send interactive messages.</span></span>

<span data-ttu-id="b1aa6-124">在 Visual Studio，在 hello **SimulatedDevice**專案中，取代 hello`SendDeviceToCloudMessagesAsync`方法，以下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="b1aa6-124">In Visual Studio, in hello **SimulatedDevice** project, replace hello `SendDeviceToCloudMessagesAsync` method with hello following code:</span></span>

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

<span data-ttu-id="b1aa6-125">此方法會隨機將 hello 屬性`"level": "critical"`toomessages 傳送 hello 裝置，這將模擬 hello 方案後端時，需要立即採取行動的訊息。</span><span class="sxs-lookup"><span data-stu-id="b1aa6-125">This method randomly adds hello property `"level": "critical"` toomessages sent by hello device, which simulates a message that requires immediate action by hello solution back-end.</span></span> <span data-ttu-id="b1aa6-126">hello 裝置應用程式將此資訊傳遞在 hello 訊息內容中，而不是在 hello 訊息主體中，因此該 IoT 中樞可以路由傳送 hello 訊息 toohello 適當訊息目的地。</span><span class="sxs-lookup"><span data-stu-id="b1aa6-126">hello device app passes this information in hello message properties, instead of in hello message body, so that IoT Hub can route hello message toohello proper message destination.</span></span>

> [!NOTE]
> <span data-ttu-id="b1aa6-127">您可以使用訊息內容 tooroute 訊息各種案例，包括冷路徑的處理，此外 toohello 熱路徑範例所示。</span><span class="sxs-lookup"><span data-stu-id="b1aa6-127">You can use message properties tooroute messages for various scenarios including cold-path processing, in addition toohello hot-path example shown here.</span></span>

> [!NOTE]
> <span data-ttu-id="b1aa6-128">為了簡化的 hello 起見，本教學課程未實作任何重試原則。</span><span class="sxs-lookup"><span data-stu-id="b1aa6-128">For hello sake of simplicity, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="b1aa6-129">在實際執行程式碼，您應該實作重試原則，例如 hello MSDN 文章中建議的指數型撤退[暫時性錯誤處理]。</span><span class="sxs-lookup"><span data-stu-id="b1aa6-129">In production code, you should implement a retry policy such as exponential backoff, as suggested in hello MSDN article [Transient Fault Handling].</span></span>

## <a name="route-messages-tooa-queue-in-your-iot-hub"></a><span data-ttu-id="b1aa6-130">路由的郵件 tooa 佇列在 IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="b1aa6-130">Route messages tooa queue in your IoT hub</span></span>

<span data-ttu-id="b1aa6-131">在本節中，您可：</span><span class="sxs-lookup"><span data-stu-id="b1aa6-131">In this section, you:</span></span>

* <span data-ttu-id="b1aa6-132">建立服務匯流排佇列。</span><span class="sxs-lookup"><span data-stu-id="b1aa6-132">Create a Service Bus queue.</span></span>
* <span data-ttu-id="b1aa6-133">連接 tooyour IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="b1aa6-133">Connect it tooyour IoT hub.</span></span>
* <span data-ttu-id="b1aa6-134">設定您 IoT 中樞 toosend 訊息 toohello 佇列根據 hello hello 訊息上的屬性存在。</span><span class="sxs-lookup"><span data-stu-id="b1aa6-134">Configure your IoT hub toosend messages toohello queue based on hello presence of a property on hello message.</span></span>

<span data-ttu-id="b1aa6-135">如需如何 tooprocess 訊息從服務匯流排佇列的詳細資訊，請參閱[開始使用佇列][Service Bus queue]。</span><span class="sxs-lookup"><span data-stu-id="b1aa6-135">For more information about how tooprocess messages from Service Bus queues, see [Get started with queues][Service Bus queue].</span></span>

1. <span data-ttu-id="b1aa6-136">如[開始使用佇列][Service Bus queue]所述，建立服務匯流排佇列。</span><span class="sxs-lookup"><span data-stu-id="b1aa6-136">Create a Service Bus queue as described in [Get started with queues][Service Bus queue].</span></span> <span data-ttu-id="b1aa6-137">hello hello 佇列必須是相同的訂用帳戶和與 IoT 中樞區域。</span><span class="sxs-lookup"><span data-stu-id="b1aa6-137">hello queue must be in hello same subscription and region as your IoT hub.</span></span> <span data-ttu-id="b1aa6-138">記下 hello 命名空間和佇列名稱。</span><span class="sxs-lookup"><span data-stu-id="b1aa6-138">Make a note of hello namespace and queue name.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b1aa6-139">做為 IoT 中樞端點的服務匯流排佇列和主題不能啟用 [工作階段] 或 [重複偵測]。</span><span class="sxs-lookup"><span data-stu-id="b1aa6-139">Service Bus queues and topics used as IoT Hub endpoints must not have **Sessions** or **Duplicate Detection** enabled.</span></span> <span data-ttu-id="b1aa6-140">如果這些選項的其中一個已啟用，以顯示 hello 端點**連線**hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="b1aa6-140">If either of those options are enabled, hello endpoint appears as **Unreachable** in hello Azure portal.</span></span>

2. <span data-ttu-id="b1aa6-141">在 hello Azure 入口網站，開啟您的 IoT 中樞，然後按一下**端點**。</span><span class="sxs-lookup"><span data-stu-id="b1aa6-141">In hello Azure portal, open your IoT hub and click **Endpoints**.</span></span>
    
    ![IoT 中樞端點][30]

3. <span data-ttu-id="b1aa6-143">在 hello**端點**刀鋒視窗中，按一下 **新增**在 hello 頂端 tooadd 佇列 tooyour IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="b1aa6-143">In hello **Endpoints** blade, click **Add** at hello top tooadd your queue tooyour IoT hub.</span></span> <span data-ttu-id="b1aa6-144">名稱 hello 端點**CriticalQueue**並用 hello 下拉式清單 tooselect **Service Bus 佇列**、 hello 佇列所在的服務匯流排命名空間和 hello 您的佇列名稱。</span><span class="sxs-lookup"><span data-stu-id="b1aa6-144">Name hello endpoint **CriticalQueue** and use hello drop-downs tooselect **Service Bus queue**, hello Service Bus namespace in which your queue resides, and hello name of your queue.</span></span> <span data-ttu-id="b1aa6-145">當您完成之後時，按一下 **儲存**hello 底部。</span><span class="sxs-lookup"><span data-stu-id="b1aa6-145">When you are done, click **Save** at hello bottom.</span></span>
    
    ![新增端點][31]
    
4. <span data-ttu-id="b1aa6-147">現在按一下 IoT 中樞中的 [路由]。</span><span class="sxs-lookup"><span data-stu-id="b1aa6-147">Now click **Routes** in your IoT Hub.</span></span> <span data-ttu-id="b1aa6-148">按一下**新增**頂端 hello hello 刀鋒視窗 toocreate 加入路由傳送訊息 toohello 佇列只路由規則。</span><span class="sxs-lookup"><span data-stu-id="b1aa6-148">Click **Add** at hello top of hello blade toocreate a routing rule that routes messages toohello queue you just added.</span></span> <span data-ttu-id="b1aa6-149">選取**DeviceTelemetry** hello 的資料來源。</span><span class="sxs-lookup"><span data-stu-id="b1aa6-149">Select **DeviceTelemetry** as hello source of data.</span></span> <span data-ttu-id="b1aa6-150">輸入`level="critical"`做為 hello 條件，然後選擇您剛才加入做為自訂的端點，如 hello 路由規則端點 hello 佇列。</span><span class="sxs-lookup"><span data-stu-id="b1aa6-150">Enter `level="critical"` as hello condition, and choose hello queue you just added as a custom endpoint as hello routing rule endpoint.</span></span> <span data-ttu-id="b1aa6-151">當您完成之後時，按一下 **儲存**hello 底部。</span><span class="sxs-lookup"><span data-stu-id="b1aa6-151">When you are done, click **Save** at hello bottom.</span></span>
    
    ![新增路由][32]
    
    <span data-ttu-id="b1aa6-153">請確定 hello 後援路由設定得**ON**。</span><span class="sxs-lookup"><span data-stu-id="b1aa6-153">Make sure hello fallback route is set too**ON**.</span></span> <span data-ttu-id="b1aa6-154">此值為 hello IoT 中樞的預設組態。</span><span class="sxs-lookup"><span data-stu-id="b1aa6-154">This value is hello default configuration for an IoT hub.</span></span>
    
    ![後援路由][33]

## <a name="read-from-hello-queue-endpoint"></a><span data-ttu-id="b1aa6-156">讀取 hello 佇列端點</span><span class="sxs-lookup"><span data-stu-id="b1aa6-156">Read from hello queue endpoint</span></span>

<span data-ttu-id="b1aa6-157">在本節中，您會從 hello 佇列端點讀取 hello 訊息。</span><span class="sxs-lookup"><span data-stu-id="b1aa6-157">In this section, you read hello messages from hello queue endpoint.</span></span>

1. <span data-ttu-id="b1aa6-158">在 Visual Studio 中，將 Visual C# Windows 傳統桌面專案 toohello 目前方案，使用 hello**主控台應用程式 (.NET Framework)**專案範本。</span><span class="sxs-lookup"><span data-stu-id="b1aa6-158">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution, by using hello **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="b1aa6-159">名稱 hello 專案**ReadCriticalQueue**。</span><span class="sxs-lookup"><span data-stu-id="b1aa6-159">Name hello project **ReadCriticalQueue**.</span></span>

2. <span data-ttu-id="b1aa6-160">在 [方案總管] 中，以滑鼠右鍵按一下 hello **ReadCriticalQueue**專案，然後再按一下**管理 NuGet 封裝**。</span><span class="sxs-lookup"><span data-stu-id="b1aa6-160">In Solution Explorer, right-click hello **ReadCriticalQueue** project, and then click **Manage NuGet Packages**.</span></span> <span data-ttu-id="b1aa6-161">這項作業會顯示 hello **NuGet 套件管理員**視窗。</span><span class="sxs-lookup"><span data-stu-id="b1aa6-161">This operation displays hello **NuGet Package Manager** window.</span></span>

3. <span data-ttu-id="b1aa6-162">搜尋**WindowsAzure.ServiceBus**，按一下 **安裝**，並接受使用規定 hello。</span><span class="sxs-lookup"><span data-stu-id="b1aa6-162">Search for **WindowsAzure.ServiceBus**, click **Install**, and accept hello terms of use.</span></span> <span data-ttu-id="b1aa6-163">這項作業會下載、 安裝，並新增參考 toohello Azure 服務匯流排，所有相依性。</span><span class="sxs-lookup"><span data-stu-id="b1aa6-163">This operation downloads, installs, and adds a reference toohello Azure Service Bus, with all its dependencies.</span></span>

4. <span data-ttu-id="b1aa6-164">新增下列 hello**使用**在 hello hello 最上方的陳述式**Program.cs**檔案：</span><span class="sxs-lookup"><span data-stu-id="b1aa6-164">Add hello following **using** statements at hello top of hello **Program.cs** file:</span></span>
   
    ```csharp
    using System.IO;
    using Microsoft.ServiceBus.Messaging;
    ```

5. <span data-ttu-id="b1aa6-165">最後，加入下列行 toohello hello **Main**方法。</span><span class="sxs-lookup"><span data-stu-id="b1aa6-165">Finally, add hello following lines toohello **Main** method.</span></span> <span data-ttu-id="b1aa6-166">取代連接字串 hello**接聽**hello 佇列的權限：</span><span class="sxs-lookup"><span data-stu-id="b1aa6-166">Substitute hello connection string with **Listen** permissions for hello queue:</span></span>
   
    ```csharp
    Console.WriteLine("Receive critical messages. Ctrl-C tooexit.\n");
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

## <a name="run-hello-applications"></a><span data-ttu-id="b1aa6-167">執行 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="b1aa6-167">Run hello applications</span></span>
<span data-ttu-id="b1aa6-168">現在您已準備好 toorun hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b1aa6-168">Now you are ready toorun hello applications.</span></span>

1. <span data-ttu-id="b1aa6-169">在 Visual Studio 的方案總管中，以滑鼠右鍵按一下您的方案，然後選取 [設定啟始專案]。</span><span class="sxs-lookup"><span data-stu-id="b1aa6-169">In Visual Studio, in Solution Explorer, right-click your solution and select **Set StartUp Projects**.</span></span> <span data-ttu-id="b1aa6-170">選取**多個啟始專案**，然後選取**啟動**hello hello 動作**ReadDeviceToCloudMessages**， **SimulatedDevice**，和**ReadCriticalQueue**專案。</span><span class="sxs-lookup"><span data-stu-id="b1aa6-170">Select **Multiple startup projects**, then select **Start** as hello action for hello **ReadDeviceToCloudMessages**, **SimulatedDevice**, and **ReadCriticalQueue** projects.</span></span>
2. <span data-ttu-id="b1aa6-171">按**F5** toostart hello 三個主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="b1aa6-171">Press **F5** toostart hello three console apps.</span></span> <span data-ttu-id="b1aa6-172">hello **ReadDeviceToCloudMessages**應用程式必須僅非重大訊息寄件者 hello **SimulatedDevice**應用程式，以及 hello **ReadCriticalQueue**只剩應用程式重要訊息。</span><span class="sxs-lookup"><span data-stu-id="b1aa6-172">hello **ReadDeviceToCloudMessages** app has only non-critical messages sent from hello **SimulatedDevice** application, and hello **ReadCriticalQueue** app has only critical messages.</span></span>
   
   ![三個主控台應用程式][50]

## <a name="next-steps"></a><span data-ttu-id="b1aa6-174">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b1aa6-174">Next steps</span></span>
<span data-ttu-id="b1aa6-175">在本教學課程中，您學會如何 tooreliably 裝置到雲端訊息分派使用 IoT 中樞的 hello 訊息路由功能。</span><span class="sxs-lookup"><span data-stu-id="b1aa6-175">In this tutorial, you learned how tooreliably dispatch device-to-cloud messages by using hello message routing functionality of IoT Hub.</span></span>

<span data-ttu-id="b1aa6-176">hello [toosend 雲端到裝置與 IoT 中樞的訊息][ lnk-c2d]顯示 toosend 訊息從您的方案後端 tooyour 裝置的方式。</span><span class="sxs-lookup"><span data-stu-id="b1aa6-176">hello [How toosend cloud-to-device messages with IoT Hub][lnk-c2d] shows you how toosend messages tooyour devices from your solution back end.</span></span>

<span data-ttu-id="b1aa6-177">完整的端對端解決方案使用 IoT 中樞 toosee 範例請參閱[Azure IoT 套件][lnk-suite]。</span><span class="sxs-lookup"><span data-stu-id="b1aa6-177">toosee examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Suite][lnk-suite].</span></span>

<span data-ttu-id="b1aa6-178">toolearn 進一步了解開發與 IoT 中樞的解決方案，請參閱 「 hello [IoT 中樞開發人員指南]。</span><span class="sxs-lookup"><span data-stu-id="b1aa6-178">toolearn more about developing solutions with IoT Hub, see hello [IoT Hub developer guide].</span></span>

<span data-ttu-id="b1aa6-179">請參閱詳細訊息路由在 IoT 中樞 toolearn[傳送和接收訊息與 IoT 中樞][lnk-devguide-messaging]。</span><span class="sxs-lookup"><span data-stu-id="b1aa6-179">toolearn more about message routing in IoT Hub, see [Send and receive messages with IoT Hub][lnk-devguide-messaging].</span></span>

<!-- Images. -->
[50]: ./media/iot-hub-csharp-csharp-process-d2c/run1.png
[30]: ./media/iot-hub-csharp-csharp-process-d2c/click-endpoints.png
[31]: ./media/iot-hub-csharp-csharp-process-d2c/endpoint-creation.png
[32]: ./media/iot-hub-csharp-csharp-process-d2c/route-creation.png
[33]: ./media/iot-hub-csharp-csharp-process-d2c/fallback-route.png

<!-- Links -->
[Service Bus queue]: ../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md
[Azure 儲存體]: https://azure.microsoft.com/documentation/services/storage/
[Azure 服務匯流排]: https://azure.microsoft.com/documentation/services/service-bus/
[IoT 中樞開發人員指南]: iot-hub-devguide.md
[開始使用 IoT 中樞]: iot-hub-csharp-csharp-getstarted.md
[lnk-devguide-messaging]: iot-hub-devguide-messaging.md
[Azure IoT 開發人員中心]: https://azure.microsoft.com/develop/iot
[暫時性錯誤處理]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-c2d]: iot-hub-csharp-csharp-process-d2c.md
[lnk-suite]: https://azure.microsoft.com/documentation/suites/iot-suite/
