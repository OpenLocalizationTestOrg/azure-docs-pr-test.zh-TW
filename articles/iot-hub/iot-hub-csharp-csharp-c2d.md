---
title: "使用 Azure IoT 中樞傳送雲端到裝置訊息 (.NET) | Microsoft Docs"
description: "如何使用適用於 .NET 的 Azure IoT SDK，將雲端到裝置訊息從 Azure IoT 中樞傳送至裝置。 您可以修改裝置應用程式，以接收雲端到裝置訊息，也可以修改後端應用程式，以傳送雲端到裝置訊息。"
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: a31c05ed-6ec0-40f3-99ab-8fdd28b1a89a
ms.service: iot-hub
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: elioda
ms.openlocfilehash: 3f5f83671054c30afde3d7f18ff0edcdb8f78a01
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="send-messages-from-the-cloud-to-your-device-with-iot-hub-net"></a><span data-ttu-id="f17fc-104">使用 IoT 中樞將訊息從雲端傳送至裝置 (.NET)</span><span class="sxs-lookup"><span data-stu-id="f17fc-104">Send messages from the cloud to your device with IoT Hub (.NET)</span></span>
[!INCLUDE [iot-hub-selector-c2d](../../includes/iot-hub-selector-c2d.md)]

## <a name="introduction"></a><span data-ttu-id="f17fc-105">簡介</span><span class="sxs-lookup"><span data-stu-id="f17fc-105">Introduction</span></span>
<span data-ttu-id="f17fc-106">Azure IoT 中樞是一項完全受管理的服務，有助於讓數百萬個裝置和一個解決方案後端進行可靠且安全的雙向通訊。</span><span class="sxs-lookup"><span data-stu-id="f17fc-106">Azure IoT Hub is a fully managed service that helps enable reliable and secure bi-directional communications between millions of devices and a solution back end.</span></span> <span data-ttu-id="f17fc-107">[開始使用 IoT 中樞]教學課程會示範如何建立 IoT 中樞、在其中佈建裝置識別，以及編寫裝置應用程式，以傳送裝置到雲端的訊息。</span><span class="sxs-lookup"><span data-stu-id="f17fc-107">The [Get started with IoT Hub] tutorial shows how to create an IoT hub, provision a device identity in it, and code a device app that sends device-to-cloud messages.</span></span>

<span data-ttu-id="f17fc-108">本教學課程是以 [開始使用 IoT 中樞]為基礎。</span><span class="sxs-lookup"><span data-stu-id="f17fc-108">This tutorial builds on [Get started with IoT Hub].</span></span> <span data-ttu-id="f17fc-109">這會說明如何：</span><span class="sxs-lookup"><span data-stu-id="f17fc-109">It shows you how to:</span></span>

* <span data-ttu-id="f17fc-110">從您的解決方案後端，透過 IoT 中樞將雲端到裝置訊息傳送給單一裝置。</span><span class="sxs-lookup"><span data-stu-id="f17fc-110">From your solution back end, send cloud-to-device messages to a single device through IoT Hub.</span></span>
* <span data-ttu-id="f17fc-111">接收裝置上的雲端到裝置訊息。</span><span class="sxs-lookup"><span data-stu-id="f17fc-111">Receive cloud-to-device messages on a device.</span></span>
* <span data-ttu-id="f17fc-112">從您的解決方案後端，要求確認收到從 IoT 中樞傳送到裝置的訊息 (「意見反應」)。</span><span class="sxs-lookup"><span data-stu-id="f17fc-112">From your solution back end, request delivery acknowledgement (*feedback*) for messages sent to a device from IoT Hub.</span></span>

<span data-ttu-id="f17fc-113">您可以在 [IoT 中樞開發人員指南][IoT Hub developer guide - C2D]中，找到有關雲端到裝置訊息的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="f17fc-113">You can find more information on cloud-to-device messages in the [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>

<span data-ttu-id="f17fc-114">在本教學課程結尾處，您會執行兩個 .NET 主控台應用程式：</span><span class="sxs-lookup"><span data-stu-id="f17fc-114">At the end of this tutorial, you run two .NET console apps:</span></span>

* <span data-ttu-id="f17fc-115">**SimulatedDevice**， [開始使用 IoT 中樞]中建立之應用程式的修改版本，可連接到您的 IoT 中心，並接收雲端到裝置的訊息。</span><span class="sxs-lookup"><span data-stu-id="f17fc-115">**SimulatedDevice**, a modified version of the app created in [Get started with IoT Hub], which connects to your IoT hub and receives cloud-to-device messages.</span></span>
* <span data-ttu-id="f17fc-116">**SendCloudToDevice**會透過 IoT 中樞，將雲端到裝置訊息傳送到裝置應用程式，然後接收其傳遞通知。</span><span class="sxs-lookup"><span data-stu-id="f17fc-116">**SendCloudToDevice**, which sends a cloud-to-device message to the device app through IoT Hub, and then receives its delivery acknowledgement.</span></span>

> [!NOTE]
> <span data-ttu-id="f17fc-117">IoT 中樞會透過 [Azure IoT 裝置 SDK] 為許多裝置平台和語言 (包括 C、Java 及 Javascript) 提供 SDK 支援。</span><span class="sxs-lookup"><span data-stu-id="f17fc-117">IoT Hub has SDK support for many device platforms and languages (including C, Java, and Javascript) through [Azure IoT device SDKs].</span></span> <span data-ttu-id="f17fc-118">如需有關如何將您的裝置與本教學課程中的程式碼連接 (通常是連線至 Azure IoT 中樞) 的逐步指示，請參閱 [Azure IoT 中樞開發人員指南]。</span><span class="sxs-lookup"><span data-stu-id="f17fc-118">For step-by-step instructions on how to connect your device to this tutorial's code, and generally to Azure IoT Hub, see the [IoT Hub developer guide].</span></span>
> 
> 

<span data-ttu-id="f17fc-119">若要完成此教學課程，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="f17fc-119">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="f17fc-120">Visual Studio 2015 或 Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="f17fc-120">Visual Studio 2015 or Visual Studio 2017</span></span>
* <span data-ttu-id="f17fc-121">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="f17fc-121">An active Azure account.</span></span> <span data-ttu-id="f17fc-122">(如果您沒有帳戶，只需要幾分鐘的時間就可以建立[免費帳戶][lnk-free-trial]。)</span><span class="sxs-lookup"><span data-stu-id="f17fc-122">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

## <a name="receive-messages-in-the-device-app"></a><span data-ttu-id="f17fc-123">在裝置應用程式中接收訊息</span><span class="sxs-lookup"><span data-stu-id="f17fc-123">Receive messages in the device app</span></span>
<span data-ttu-id="f17fc-124">在本節中，您會修改在[開始使用 IoT 中樞]中建立的裝置應用程式，以接收來自 IoT 中樞的雲端到裝置訊息。</span><span class="sxs-lookup"><span data-stu-id="f17fc-124">In this section, you'll modify the device app you created in [Get started with IoT Hub] to receive cloud-to-device messages from the IoT hub.</span></span>

1. <span data-ttu-id="f17fc-125">在 Visual Studio 的 **SimulatedDevice** 專案中，將下列方法新增 [程式] 類別。</span><span class="sxs-lookup"><span data-stu-id="f17fc-125">In Visual Studio, in the **SimulatedDevice** project, add the following method to the **Program** class.</span></span>
   
        private static async void ReceiveC2dAsync()
        {
            Console.WriteLine("\nReceiving cloud to device messages from service");
            while (true)
            {
                Message receivedMessage = await deviceClient.ReceiveAsync();
                if (receivedMessage == null) continue;
   
                Console.ForegroundColor = ConsoleColor.Yellow;
                Console.WriteLine("Received message: {0}", Encoding.ASCII.GetString(receivedMessage.GetBytes()));
                Console.ResetColor();
   
                await deviceClient.CompleteAsync(receivedMessage);
            }
        }
   
    <span data-ttu-id="f17fc-126">`ReceiveAsync` 方法會以非同步方式，在裝置收到訊息時，傳回收到的訊息。</span><span class="sxs-lookup"><span data-stu-id="f17fc-126">The `ReceiveAsync` method asynchronously returns the received message at the time that it is received by the device.</span></span> <span data-ttu-id="f17fc-127">它會在可指定的逾時期間過後傳回「null」  (在本例中，使用的是預設值 1 分鐘)。</span><span class="sxs-lookup"><span data-stu-id="f17fc-127">It returns *null* after a specifiable timeout period (in this case, the default of one minute is used).</span></span> <span data-ttu-id="f17fc-128">當應用程式收到 *null* 時，應繼續等待新訊息。</span><span class="sxs-lookup"><span data-stu-id="f17fc-128">When the app receives a *null*, it should continue to wait for new messages.</span></span> <span data-ttu-id="f17fc-129">這項要求是 `if (receivedMessage == null) continue` 行的的原因。</span><span class="sxs-lookup"><span data-stu-id="f17fc-129">This requirement is the reason for the `if (receivedMessage == null) continue` line.</span></span>
   
    <span data-ttu-id="f17fc-130">對 `CompleteAsync()` 的呼叫會通知 IoT 中樞，說明已成功處理訊息。</span><span class="sxs-lookup"><span data-stu-id="f17fc-130">The call to `CompleteAsync()` notifies IoT Hub that the message has been successfully processed.</span></span> <span data-ttu-id="f17fc-131">可以安全地從裝置佇列中移除該訊息。</span><span class="sxs-lookup"><span data-stu-id="f17fc-131">The message can be safely removed from the device queue.</span></span> <span data-ttu-id="f17fc-132">如果因故導致裝置應用程式無法完成訊息處理作業，「IoT 中樞」將會重新傳遞該訊息。</span><span class="sxs-lookup"><span data-stu-id="f17fc-132">If something happened that prevented the device app from completing the processing of the message, IoT Hub delivers it again.</span></span> <span data-ttu-id="f17fc-133">因此，裝置應用程式中的訊息處理邏輯必須是「等冪」，如此一來，多次接收相同的訊息才會產生相同的結果。</span><span class="sxs-lookup"><span data-stu-id="f17fc-133">It is then important that message processing logic in the device app is *idempotent*, so that receiving the same message multiple times produces the same result.</span></span> <span data-ttu-id="f17fc-134">應用程式也可以暫時放棄訊息，這會使得「IoT 中樞」將訊息保留在佇列中以供未來取用。</span><span class="sxs-lookup"><span data-stu-id="f17fc-134">An application can also temporarily abandon a message, which results in IoT hub retaining the message in the queue for future consumption.</span></span> <span data-ttu-id="f17fc-135">或者，應用程式可以拒絕訊息，這會將訊息從佇列中永久移除。</span><span class="sxs-lookup"><span data-stu-id="f17fc-135">Or, the application can reject a message, which permanently removes the message from the queue.</span></span> <span data-ttu-id="f17fc-136">如需有關雲端到裝置訊息生命週期的詳細資訊，請參閱 [IoT 中樞開發人員指南][IoT Hub developer guide - C2D]。</span><span class="sxs-lookup"><span data-stu-id="f17fc-136">For more information about the cloud-to-device message lifecycle, see the [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="f17fc-137">使用 HTTP 而不使用 MQTT 或 AMQP 做為傳輸時，`ReceiveAsync` 方法會立即傳回。</span><span class="sxs-lookup"><span data-stu-id="f17fc-137">When using HTTP instead of MQTT or AMQP as a transport, the `ReceiveAsync` method returns immediately.</span></span> <span data-ttu-id="f17fc-138">使用 HTTP 時，針對雲端到裝置訊息支援的模式是裝置以間歇方式連接而不常檢查訊息 (低於每 25 分鐘一次)。</span><span class="sxs-lookup"><span data-stu-id="f17fc-138">The supported pattern for cloud-to-device messages with HTTP is intermittently connected devices that check for messages infrequently (less than every 25 minutes).</span></span> <span data-ttu-id="f17fc-139">發出更多 HTTP 接收會導致「IoT 中樞」對要求進行節流。</span><span class="sxs-lookup"><span data-stu-id="f17fc-139">Issuing more HTTP receives results in IoT Hub throttling the requests.</span></span> <span data-ttu-id="f17fc-140">如需有關 AMQP、AMQP 和 HTTP 支援之間的差異，以及 IoT 中樞節流的詳細資訊，請參閱 [IoT 中樞開發人員指南][IoT Hub developer guide - C2D]。</span><span class="sxs-lookup"><span data-stu-id="f17fc-140">For more information about the differences between MQTT, AMQP and HTTP support, and IoT Hub throttling, see the [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>
   > 
   > 
2. <span data-ttu-id="f17fc-141">將下列方法新增到 **Main** 方法中緊接在 `Console.ReadLine()` 行前面：</span><span class="sxs-lookup"><span data-stu-id="f17fc-141">Add the following method in the **Main** method, right before the `Console.ReadLine()` line:</span></span>
   
        ReceiveC2dAsync();

> [!NOTE]
> <span data-ttu-id="f17fc-142">為了簡單起見，本教學課程不會實作任何重試原則。</span><span class="sxs-lookup"><span data-stu-id="f17fc-142">For simplicity's sake, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="f17fc-143">在生產環境程式碼中，您應該如 MSDN 文章 [暫時性錯誤處理]所建議，實作重試原則 (例如指數型輪詢)。</span><span class="sxs-lookup"><span data-stu-id="f17fc-143">In production code, you should implement retry policies (such as exponential backoff), as suggested in the MSDN article [Transient Fault Handling].</span></span>
> 
> 

## <a name="send-a-cloud-to-device-message"></a><span data-ttu-id="f17fc-144">傳送雲端到裝置訊息</span><span class="sxs-lookup"><span data-stu-id="f17fc-144">Send a cloud-to-device message</span></span>
<span data-ttu-id="f17fc-145">在本節中，您會撰寫 .NET 主控台應用程式，將雲端到裝置訊息傳送至裝置應用程式。</span><span class="sxs-lookup"><span data-stu-id="f17fc-145">In this section, you write a .NET console app that sends cloud-to-device messages to the device app.</span></span>

1. <span data-ttu-id="f17fc-146">在目前的 Visual Studio 方案中，使用 [主控台應用程式] 專案範本來建立「Visual C# 傳統型應用程式」專案。</span><span class="sxs-lookup"><span data-stu-id="f17fc-146">In the current Visual Studio solution, create a Visual C# Desktop App project by using the **Console Application** project template.</span></span> <span data-ttu-id="f17fc-147">將專案命名為 **SendCloudToDevice**。</span><span class="sxs-lookup"><span data-stu-id="f17fc-147">Name the project **SendCloudToDevice**.</span></span>
   
    ![Visual Studio 中的新專案][20]
2. <span data-ttu-id="f17fc-149">在 [方案總管] 中，以滑鼠右鍵按一下方案，然後按一下 [ **管理方案的 NuGet 封裝...**]。</span><span class="sxs-lookup"><span data-stu-id="f17fc-149">In Solution Explorer, right-click the solution, and then click **Manage NuGet Packages for Solution...**.</span></span> 
   
    <span data-ttu-id="f17fc-150">此動作會開啟 [管理 NuGet 套件] 視窗。</span><span class="sxs-lookup"><span data-stu-id="f17fc-150">This action opens the **Manage NuGet Packages** window.</span></span>
3. <span data-ttu-id="f17fc-151">搜尋 **Microsoft.Azure.Devices**，按一下 [安裝]，然後接受使用規定。</span><span class="sxs-lookup"><span data-stu-id="f17fc-151">Search for **Microsoft.Azure.Devices**, click **Install**, and accept the terms of use.</span></span> 
   
    <span data-ttu-id="f17fc-152">這會下載和安裝 [Azure IoT 服務 SDK NuGet 套件]，並新增其參考。</span><span class="sxs-lookup"><span data-stu-id="f17fc-152">This downloads, installs, and adds a reference to the [Azure IoT service SDK NuGet package].</span></span>

4. <span data-ttu-id="f17fc-153">在 **Program.cs** 檔案開頭處新增下列 `using` 陳述式：</span><span class="sxs-lookup"><span data-stu-id="f17fc-153">Add the following `using` statement at the top of the **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
5. <span data-ttu-id="f17fc-154">將下列欄位新增到 **Program** 類別。</span><span class="sxs-lookup"><span data-stu-id="f17fc-154">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="f17fc-155">將預留位置的值從 IoT 中樞連接字串替換成[開始使用 IoT 中樞]：</span><span class="sxs-lookup"><span data-stu-id="f17fc-155">Substitute the placeholder value with the IoT hub connection string from [Get started with IoT Hub]:</span></span>
   
        static ServiceClient serviceClient;
        static string connectionString = "{iot hub connection string}";
6. <span data-ttu-id="f17fc-156">將下列方法加入至 **Program** 類別：</span><span class="sxs-lookup"><span data-stu-id="f17fc-156">Add the following method to the **Program** class:</span></span>
   
        private async static Task SendCloudToDeviceMessageAsync()
        {
            var commandMessage = new Message(Encoding.ASCII.GetBytes("Cloud to device message."));
            await serviceClient.SendAsync("myFirstDevice", commandMessage);
        }
   
    <span data-ttu-id="f17fc-157">這個方法會將新的雲端到裝置訊息傳送給識別碼為 `myFirstDevice`的裝置。</span><span class="sxs-lookup"><span data-stu-id="f17fc-157">This method sends a new cloud-to-device message to the device with the ID, `myFirstDevice`.</span></span> <span data-ttu-id="f17fc-158">只有在您修改了[開始使用 IoT 中樞]內的方法時，才要變更此參數。</span><span class="sxs-lookup"><span data-stu-id="f17fc-158">Change this parameter only if you modified it from the one used in [Get started with IoT Hub].</span></span>
7. <span data-ttu-id="f17fc-159">最後，將下列幾行加入至 **Main** 方法：</span><span class="sxs-lookup"><span data-stu-id="f17fc-159">Finally, add the following lines to the **Main** method:</span></span>
   
        Console.WriteLine("Send Cloud-to-Device message\n");
        serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
   
        Console.WriteLine("Press any key to send a C2D message.");
        Console.ReadLine();
        SendCloudToDeviceMessageAsync().Wait();
        Console.ReadLine();
8. <span data-ttu-id="f17fc-160">從 Visual Studio 中，在您的方案上按一下滑鼠右鍵，然後選取 [設定啟始專案...]。選取 [多個啟始專案]，然後同時針對 **ReadDeviceToCloudMessages**、**SimulatedDevice** 以及 **SendCloudToDevice** 選取 [啟動] 動作。</span><span class="sxs-lookup"><span data-stu-id="f17fc-160">From within Visual Studio, right-click your solution, and select **Set StartUp projects...**. Select **Multiple startup projects**, then select the **Start** action for **ReadDeviceToCloudMessages**, **SimulatedDevice**, and **SendCloudToDevice**.</span></span>
9. <span data-ttu-id="f17fc-161">按 **F5**。</span><span class="sxs-lookup"><span data-stu-id="f17fc-161">Press **F5**.</span></span> <span data-ttu-id="f17fc-162">三個應用程式應該全部都會啟動。</span><span class="sxs-lookup"><span data-stu-id="f17fc-162">All three applications should start.</span></span> <span data-ttu-id="f17fc-163">選取 [SendCloudToDevice] 視窗，然後按 **Enter**。</span><span class="sxs-lookup"><span data-stu-id="f17fc-163">Select the **SendCloudToDevice** windows, and press **Enter**.</span></span> <span data-ttu-id="f17fc-164">您應該會看到裝置應用程式正在接收訊息。</span><span class="sxs-lookup"><span data-stu-id="f17fc-164">You should see the message being received by the device app.</span></span>
   
   ![正在接收訊息的應用程式][21]

## <a name="receive-delivery-feedback"></a><span data-ttu-id="f17fc-166">接收傳遞意見反應</span><span class="sxs-lookup"><span data-stu-id="f17fc-166">Receive delivery feedback</span></span>
<span data-ttu-id="f17fc-167">您可以向「IoT 中樞」要求每個雲端到裝置訊息的傳遞 (或到期) 通知。</span><span class="sxs-lookup"><span data-stu-id="f17fc-167">It is possible to request delivery (or expiration) acknowledgements from IoT Hub for each cloud-to-device message.</span></span> <span data-ttu-id="f17fc-168">這個選項可讓解決方案後端輕鬆地通知重試或補償邏輯。</span><span class="sxs-lookup"><span data-stu-id="f17fc-168">This option enables the solution back end to easily inform retry or compensation logic.</span></span> <span data-ttu-id="f17fc-169">如需有關雲端到裝置意見反應的詳細資訊，請參閱 [IoT 中樞開發人員指南][IoT Hub developer guide - C2D]。</span><span class="sxs-lookup"><span data-stu-id="f17fc-169">For more information about cloud-to-device feedback, see the [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>

<span data-ttu-id="f17fc-170">在本節中，您會修改 **SendCloudToDevice** 應用程式以要求意見反應，然後從 IoT 中樞接收意見反應。</span><span class="sxs-lookup"><span data-stu-id="f17fc-170">In this section, you modify the **SendCloudToDevice** app to request feedback, and receive it from IoT Hub.</span></span>

1. <span data-ttu-id="f17fc-171">在 Visual Studio 的 **SendCloudToDevice** 專案中，將下列方法加入至 **Program** 類別。</span><span class="sxs-lookup"><span data-stu-id="f17fc-171">In Visual Studio, in the **SendCloudToDevice** project, add the following method to the **Program** class.</span></span>
   
        private async static void ReceiveFeedbackAsync()
        {
            var feedbackReceiver = serviceClient.GetFeedbackReceiver();
   
            Console.WriteLine("\nReceiving c2d feedback from service");
            while (true)
            {
                var feedbackBatch = await feedbackReceiver.ReceiveAsync();
                if (feedbackBatch == null) continue;
   
                Console.ForegroundColor = ConsoleColor.Yellow;
                Console.WriteLine("Received feedback: {0}", string.Join(", ", feedbackBatch.Records.Select(f => f.StatusCode)));
                Console.ResetColor();
   
                await feedbackReceiver.CompleteAsync(feedbackBatch);
            }
        }
   
    <span data-ttu-id="f17fc-172">請注意，此接收模式與用來從裝置應用程式接收雲端到裝置訊息的模式相同。</span><span class="sxs-lookup"><span data-stu-id="f17fc-172">Note this receive pattern is the same one used to receive cloud-to-device messages from the device app.</span></span>
2. <span data-ttu-id="f17fc-173">緊接在 `serviceClient = ServiceClient.CreateFromConnectionString(connectionString)` 行後面，將下列方法新增到 **Main** 方法中：</span><span class="sxs-lookup"><span data-stu-id="f17fc-173">Add the following method in the **Main** method, right after the `serviceClient = ServiceClient.CreateFromConnectionString(connectionString)` line:</span></span>
   
        ReceiveFeedbackAsync();
3. <span data-ttu-id="f17fc-174">為了要求雲端到裝置訊息傳遞狀況的意見反應，您必須在 **SendCloudToDeviceMessageAsync** 方法中指定屬性。</span><span class="sxs-lookup"><span data-stu-id="f17fc-174">To request feedback for the delivery of your cloud-to-device message, you have to specify a property in the **SendCloudToDeviceMessageAsync** method.</span></span> <span data-ttu-id="f17fc-175">將以下行加入 `var commandMessage = new Message(...);` 行之後：</span><span class="sxs-lookup"><span data-stu-id="f17fc-175">Add the following line, right after the `var commandMessage = new Message(...);` line:</span></span>
   
        commandMessage.Ack = DeliveryAcknowledgement.Full;
4. <span data-ttu-id="f17fc-176">按 **F5**來執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="f17fc-176">Run the apps by pressing **F5**.</span></span> <span data-ttu-id="f17fc-177">您應該會看到三個應用程式全部都啟動。</span><span class="sxs-lookup"><span data-stu-id="f17fc-177">You should see all three applications start.</span></span> <span data-ttu-id="f17fc-178">選取 [SendCloudToDevice] 視窗，然後按 **Enter**。</span><span class="sxs-lookup"><span data-stu-id="f17fc-178">Select the **SendCloudToDevice** windows, and press **Enter**.</span></span> <span data-ttu-id="f17fc-179">您應該會看到裝置應用程式正在接收訊息，而幾秒之後，則會看到您的 **SendCloudToDevice** 應用程式正在接收意見反應訊息。</span><span class="sxs-lookup"><span data-stu-id="f17fc-179">You should see the message being received by the device app, and after a few seconds, the feedback message being received by your **SendCloudToDevice** application.</span></span>
   
   ![正在接收訊息的應用程式][22]

> [!NOTE]
> <span data-ttu-id="f17fc-181">為了簡單起見，本教學課程不會實作任何重試原則。</span><span class="sxs-lookup"><span data-stu-id="f17fc-181">For simplicity's sake, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="f17fc-182">在生產環境程式碼中，您應該如 MSDN 文章 [暫時性錯誤處理]所建議，實作重試原則 (例如指數型輪詢)。</span><span class="sxs-lookup"><span data-stu-id="f17fc-182">In production code, you should implement retry policies (such as exponential backoff), as suggested in the MSDN article [Transient Fault Handling].</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="f17fc-183">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f17fc-183">Next steps</span></span>
<span data-ttu-id="f17fc-184">在本教學課程中，您已了解如何傳送和接收雲端到裝置的訊息。</span><span class="sxs-lookup"><span data-stu-id="f17fc-184">In this tutorial, you learned how to send and receive cloud-to-device messages.</span></span> 

<span data-ttu-id="f17fc-185">若要查看使用 IoT 中樞的完整端對端解決方案範例，請參閱 [Azure IoT 套件]。</span><span class="sxs-lookup"><span data-stu-id="f17fc-185">To see examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Suite].</span></span>

<span data-ttu-id="f17fc-186">若要深入了解如何使用 IoT 中樞開發解決方案，請參閱 [Azure IoT 中樞開發人員指南]。</span><span class="sxs-lookup"><span data-stu-id="f17fc-186">To learn more about developing solutions with IoT Hub, see the [IoT Hub developer guide].</span></span>

<!-- Images -->
[20]: ./media/iot-hub-csharp-csharp-c2d/create-identity-csharp1.png
[21]: ./media/iot-hub-csharp-csharp-c2d/sendc2d1.png
[22]: ./media/iot-hub-csharp-csharp-c2d/sendc2d2.png

<!-- Links -->

[Azure IoT 服務 SDK NuGet 套件]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
[暫時性錯誤處理]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[IoT Hub developer guide - C2D]: iot-hub-devguide-messaging.md

[Azure IoT 中樞開發人員指南]: iot-hub-devguide.md
[開始使用 IoT 中樞]: iot-hub-csharp-csharp-getstarted.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[Azure IoT 套件]: https://docs.microsoft.com/en-us/azure/iot-suite/
[Azure IoT 裝置 SDK]: iot-hub-devguide-sdks.md