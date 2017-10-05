---
title: "使用 Azure IoT 中樞傳送雲端到裝置訊息 (Node) | Microsoft Docs"
description: "如何使用適用於 Node.js 的 Azure IoT SDK，將雲端到裝置訊息從 Azure IoT 中樞傳送至裝置。 您可以修改模擬裝置應用程式，以接收雲端到裝置訊息，也可以修改後端應用程式，以傳送雲端到裝置訊息。"
services: iot-hub
documentationcenter: nodejs
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 3ca8a78f-ade2-46e8-8a49-d5d599cdf1f1
ms.service: iot-hub
ms.devlang: javascript
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: dobett
ms.openlocfilehash: 4580bda5633f84a7c7af0dc85f3cea4951024836
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="send-cloud-to-device-messages-with-iot-hub-node"></a><span data-ttu-id="6b0d6-104">使用 IoT 中樞 (Node) 傳送雲端到裝置訊息</span><span class="sxs-lookup"><span data-stu-id="6b0d6-104">Send cloud-to-device messages with IoT Hub (Node)</span></span>
[!INCLUDE [iot-hub-selector-c2d](../../includes/iot-hub-selector-c2d.md)]

## <a name="introduction"></a><span data-ttu-id="6b0d6-105">簡介</span><span class="sxs-lookup"><span data-stu-id="6b0d6-105">Introduction</span></span>
<span data-ttu-id="6b0d6-106">Azure IoT 中樞是一項完全受管理的服務，有助於讓數百萬個裝置和一個解決方案後端進行可靠且安全的雙向通訊。</span><span class="sxs-lookup"><span data-stu-id="6b0d6-106">Azure IoT Hub is a fully managed service that helps enable reliable and secure bi-directional communications between millions of devices and a solution back end.</span></span> <span data-ttu-id="6b0d6-107">[開始使用 IoT 中樞] 教學課程會示範如何建立 IoT 中樞、在其中佈建裝置識別，以及編寫模擬的裝置應用程式，以傳送裝置到雲端的訊息。</span><span class="sxs-lookup"><span data-stu-id="6b0d6-107">The [Get started with IoT Hub] tutorial shows how to create an IoT hub, provision a device identity in it, and code a simulated device app that sends device-to-cloud messages.</span></span>

<span data-ttu-id="6b0d6-108">本教學課程是以 [開始使用 IoT 中樞]為基礎。</span><span class="sxs-lookup"><span data-stu-id="6b0d6-108">This tutorial builds on [Get started with IoT Hub].</span></span> <span data-ttu-id="6b0d6-109">這會說明如何：</span><span class="sxs-lookup"><span data-stu-id="6b0d6-109">It shows you how to:</span></span>

* <span data-ttu-id="6b0d6-110">從您的解決方案後端，透過 IoT 中樞將雲端到裝置訊息傳送給單一裝置。</span><span class="sxs-lookup"><span data-stu-id="6b0d6-110">From your solution back end, send cloud-to-device messages to a single device through IoT Hub.</span></span>
* <span data-ttu-id="6b0d6-111">接收裝置上的雲端到裝置訊息。</span><span class="sxs-lookup"><span data-stu-id="6b0d6-111">Receive cloud-to-device messages on a device.</span></span>
* <span data-ttu-id="6b0d6-112">從您的解決方案後端，要求確認收到從 IoT 中樞傳送到裝置的訊息 (「意見反應」)。</span><span class="sxs-lookup"><span data-stu-id="6b0d6-112">From your solution back end, request delivery acknowledgement (*feedback*) for messages sent to a device from IoT Hub.</span></span>

<span data-ttu-id="6b0d6-113">您可以在 [IoT 中樞開發人員指南][IoT Hub developer guide - C2D]中，找到有關雲端到裝置訊息的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="6b0d6-113">You can find more information on cloud-to-device messages in the [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>

<span data-ttu-id="6b0d6-114">在本教學課程結尾處，您會執行兩個 Node.js 主控台應用程式：</span><span class="sxs-lookup"><span data-stu-id="6b0d6-114">At the end of this tutorial, you run two Node.js console apps:</span></span>

* <span data-ttu-id="6b0d6-115">**SimulatedDevice**， [開始使用 IoT 中樞]中建立之應用程式的修改版本，可連接到您的 IoT 中心，並接收雲端到裝置的訊息。</span><span class="sxs-lookup"><span data-stu-id="6b0d6-115">**SimulatedDevice**, a modified version of the app created in [Get started with IoT Hub], which connects to your IoT hub and receives cloud-to-device messages.</span></span>
* <span data-ttu-id="6b0d6-116">**SendCloudToDeviceMessage**：會透過 IoT 中樞，將雲端到裝置訊息傳送到模擬裝置應用程式，然後接收其傳遞通知。</span><span class="sxs-lookup"><span data-stu-id="6b0d6-116">**SendCloudToDeviceMessage**, which sends a cloud-to-device message to the simulated device app through IoT Hub, and then receives its delivery acknowledgement.</span></span>

> [!NOTE]
> <span data-ttu-id="6b0d6-117">「IoT 中樞」透過 Azure IoT 裝置 SDK 為許多裝置平台和語言 (包括 C、Java 及 Javascript) 提供 SDK 支援。</span><span class="sxs-lookup"><span data-stu-id="6b0d6-117">IoT Hub has SDK support for many device platforms and languages (including C, Java, and Javascript) through Azure IoT device SDKs.</span></span> <span data-ttu-id="6b0d6-118">如需有關如何將您的裝置與本教學課程中的程式碼連接 (通常是連接到「Azure IoT 中樞」) 的逐步指示，請參閱 [Azure IoT 開發人員中樞]。</span><span class="sxs-lookup"><span data-stu-id="6b0d6-118">For step-by-step instructions on how to connect your device to this tutorial's code, and generally to Azure IoT Hub, see the [Azure IoT Developer Center].</span></span>
> 
> 

<span data-ttu-id="6b0d6-119">若要完成此教學課程，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="6b0d6-119">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="6b0d6-120">Node.js 0.10.x 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="6b0d6-120">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="6b0d6-121">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="6b0d6-121">An active Azure account.</span></span> <span data-ttu-id="6b0d6-122">(如果您沒有帳戶，只需要幾分鐘的時間就可以建立[免費帳戶][lnk-free-trial]。)</span><span class="sxs-lookup"><span data-stu-id="6b0d6-122">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

## <a name="receive-messages-in-the-simulated-device-app"></a><span data-ttu-id="6b0d6-123">在模擬的裝置應用程式中接收訊息</span><span class="sxs-lookup"><span data-stu-id="6b0d6-123">Receive messages in the simulated device app</span></span>
<span data-ttu-id="6b0d6-124">在本節中，您會修改在[開始使用 IoT 中樞]中建立的模擬裝置應用程式，以接收來自 IoT 中樞的雲端對裝置訊息。</span><span class="sxs-lookup"><span data-stu-id="6b0d6-124">In this section, you modify the simulated device app you created in [Get started with IoT Hub] to receive cloud-to-device messages from the IoT hub.</span></span>

1. <span data-ttu-id="6b0d6-125">使用文字編輯器開啟 SimulatedDevice.js 檔案。</span><span class="sxs-lookup"><span data-stu-id="6b0d6-125">Using a text editor, open the SimulatedDevice.js file.</span></span>
2. <span data-ttu-id="6b0d6-126">修改 **connectCallback** 函式來處理從 IoT 中樞傳送的訊息。</span><span class="sxs-lookup"><span data-stu-id="6b0d6-126">Modify the **connectCallback** function to handle messages sent from IoT Hub.</span></span> <span data-ttu-id="6b0d6-127">在此範例中，裝置永遠會叫用 **完整** 函式，目的是通知 IoT 中樞訊息已處理完畢。</span><span class="sxs-lookup"><span data-stu-id="6b0d6-127">In this example, the device always invokes the **complete** function to notify IoT Hub that it has processed the message.</span></span> <span data-ttu-id="6b0d6-128">新版的 **connectCallback** 函式看起來會像下列程式碼片段︰</span><span class="sxs-lookup"><span data-stu-id="6b0d6-128">Your new version of the **connectCallback** function looks like the following snippet:</span></span>
   
    ```javascript
    var connectCallback = function (err) {
      if (err) {
        console.log('Could not connect: ' + err);
      } else {
        console.log('Client connected');
        client.on('message', function (msg) {
          console.log('Id: ' + msg.messageId + ' Body: ' + msg.data);
          client.complete(msg, printResultFor('completed'));
        });
        // Create a message and send it to the IoT Hub every second
        setInterval(function(){
            var temperature = 20 + (Math.random() * 15);
            var humidity = 60 + (Math.random() * 20);            
            var data = JSON.stringify({ deviceId: 'myFirstNodeDevice', temperature: temperature, humidity: humidity });
            var message = new Message(data);
            message.properties.add('temperatureAlert', (temperature > 30) ? 'true' : 'false');
            console.log("Sending message: " + message.getData());
            client.sendEvent(message, printResultFor('send'));
        }, 1000);
      }
    };
    ```
   
   > [!NOTE]
   > <span data-ttu-id="6b0d6-129">如果您使用 HTTP 而非 MQTT 或 AMQP 作為傳輸，**DeviceClient** 執行個體將不會經常 (頻率低於每隔 25 分鐘) 檢查「IoT 中樞」是否傳來訊息。</span><span class="sxs-lookup"><span data-stu-id="6b0d6-129">If you use HTTP instead of MQTT or AMQP as the transport, the **DeviceClient** instance checks for messages from IoT Hub infrequently (less than every 25 minutes).</span></span> <span data-ttu-id="6b0d6-130">如需有關 AMQP、AMQP 和 HTTP 支援之間的差異，以及 IoT 中樞節流的詳細資訊，請參閱 [IoT 中樞開發人員指南][IoT Hub developer guide - C2D]。</span><span class="sxs-lookup"><span data-stu-id="6b0d6-130">For more information about the differences between MQTT, AMQP and HTTP support, and IoT Hub throttling, see the [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>
   > 
   > 

## <a name="send-a-cloud-to-device-message"></a><span data-ttu-id="6b0d6-131">傳送雲端到裝置訊息</span><span class="sxs-lookup"><span data-stu-id="6b0d6-131">Send a cloud-to-device message</span></span>
<span data-ttu-id="6b0d6-132">在本節中，您會建立 Node.js 主控台應用程式，將雲端到裝置訊息傳送至模擬裝置應用程式。</span><span class="sxs-lookup"><span data-stu-id="6b0d6-132">In this section, you create a Node.js console app that sends cloud-to-device messages to the simulated device app.</span></span> <span data-ttu-id="6b0d6-133">您需要您在[開始使用 IoT 中樞]教學課程中所新增裝置的裝置識別碼。</span><span class="sxs-lookup"><span data-stu-id="6b0d6-133">You need the device ID of the device you added in the [Get started with IoT Hub] tutorial.</span></span> <span data-ttu-id="6b0d6-134">您也需要中樞的 IoT 中樞連接字串 (可在 [Azure 入口網站]中找到)。</span><span class="sxs-lookup"><span data-stu-id="6b0d6-134">You also need the IoT Hub connection string for your hub that you can find in the [Azure portal].</span></span>

1. <span data-ttu-id="6b0d6-135">建立新的名為 **sendcloudtodevicemessage**的空資料夾。</span><span class="sxs-lookup"><span data-stu-id="6b0d6-135">Create an empty folder called **sendcloudtodevicemessage**.</span></span> <span data-ttu-id="6b0d6-136">在 **sendcloudtodevicemessage** 資料夾中，於命令提示字元使用下列命令建立 package.json 檔案。</span><span class="sxs-lookup"><span data-stu-id="6b0d6-136">In the **sendcloudtodevicemessage** folder, create a package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="6b0d6-137">接受所有預設值：</span><span class="sxs-lookup"><span data-stu-id="6b0d6-137">Accept all the defaults:</span></span>
   
    ```shell
    npm init
    ```
2. <span data-ttu-id="6b0d6-138">在命令提示字元中，於 **sendcloudtodevicemessage** 資料夾中執行下列命令以安裝 **azure-iothub** 套件：</span><span class="sxs-lookup"><span data-stu-id="6b0d6-138">At your command prompt in the **sendcloudtodevicemessage** folder, run the following command to install the **azure-iothub** package:</span></span>
   
    ```shell
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="6b0d6-139">使用文字編輯器，在 **sendcloudtodevicemessage** 資料夾中建立 **SendCloudToDeviceMessage.js** 檔案。</span><span class="sxs-lookup"><span data-stu-id="6b0d6-139">Using a text editor, create a **SendCloudToDeviceMessage.js** file in the **sendcloudtodevicemessage** folder.</span></span>
4. <span data-ttu-id="6b0d6-140">在 **SendCloudToDeviceMessage.js** 檔案開頭新增下列 `require` 陳述式：</span><span class="sxs-lookup"><span data-stu-id="6b0d6-140">Add the following `require` statements at the start of the **SendCloudToDeviceMessage.js** file:</span></span>
   
    ```javascript
    'use strict';
   
    var Client = require('azure-iothub').Client;
    var Message = require('azure-iot-common').Message;
    ```
5. <span data-ttu-id="6b0d6-141">在 **SendCloudToDeviceMessage.js** 檔案中新增下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="6b0d6-141">Add the following code to **SendCloudToDeviceMessage.js** file.</span></span> <span data-ttu-id="6b0d6-142">將 "{IoT 中樞連接字串}" 預留位置的值，替換為您在[開始使用 IoT 中樞]教學課程中所建立中樞的 IoT 中樞連接字串。</span><span class="sxs-lookup"><span data-stu-id="6b0d6-142">Replace the "{iot hub connection string}" placeholder value with the IoT Hub connection string for the hub you created in the [Get started with IoT Hub] tutorial.</span></span> <span data-ttu-id="6b0d6-143">將 "{裝置識別碼}" 預留位置替換為您在[開始使用 IoT 中樞]教學課程中所新增裝置的裝置識別碼：</span><span class="sxs-lookup"><span data-stu-id="6b0d6-143">Replace the "{device id}" placeholder with the device ID of the device you added in the [Get started with IoT Hub] tutorial:</span></span>
   
    ```javascript
    var connectionString = '{iot hub connection string}';
    var targetDevice = '{device id}';
   
    var serviceClient = Client.fromConnectionString(connectionString);
    ```
6. <span data-ttu-id="6b0d6-144">加入下列函式來將作業結果列印至主控台︰</span><span class="sxs-lookup"><span data-stu-id="6b0d6-144">Add the following function to print operation results to the console:</span></span>
   
    ```javascript
    function printResultFor(op) {
      return function printResult(err, res) {
        if (err) console.log(op + ' error: ' + err.toString());
        if (res) console.log(op + ' status: ' + res.constructor.name);
      };
    }
    ```
7. <span data-ttu-id="6b0d6-145">加入下列函式來將傳遞意見反應訊息列印至主控台︰</span><span class="sxs-lookup"><span data-stu-id="6b0d6-145">Add the following function to print delivery feedback messages to the console:</span></span>
   
    ```javascript
    function receiveFeedback(err, receiver){
      receiver.on('message', function (msg) {
        console.log('Feedback message:')
        console.log(msg.getData().toString('utf-8'));
      });
    }
    ```
8. <span data-ttu-id="6b0d6-146">加入下列程式碼，當裝置收到雲端到裝置訊息時，會將訊息傳送至您的裝置，並處理意見反應訊息︰</span><span class="sxs-lookup"><span data-stu-id="6b0d6-146">Add the following code to send a message to your device and handle the feedback message when the device acknowledges the cloud-to-device message:</span></span>
   
    ```javascript
    serviceClient.open(function (err) {
      if (err) {
        console.error('Could not connect: ' + err.message);
      } else {
        console.log('Service client connected');
        serviceClient.getFeedbackReceiver(receiveFeedback);
        var message = new Message('Cloud to device message.');
        message.ack = 'full';
        message.messageId = "My Message ID";
        console.log('Sending message: ' + message.getData());
        serviceClient.send(targetDevice, message, printResultFor('send'));
      }
    });
    ```
9. <span data-ttu-id="6b0d6-147">儲存並關閉 **SendCloudToDeviceMessage.js** 檔案。</span><span class="sxs-lookup"><span data-stu-id="6b0d6-147">Save and close **SendCloudToDeviceMessage.js** file.</span></span>

## <a name="run-the-applications"></a><span data-ttu-id="6b0d6-148">執行應用程式</span><span class="sxs-lookup"><span data-stu-id="6b0d6-148">Run the applications</span></span>
<span data-ttu-id="6b0d6-149">現在您已經準備好執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="6b0d6-149">You are now ready to run the applications.</span></span>

1. <span data-ttu-id="6b0d6-150">在命令提示字元中，於 **simulateddevice** 資料夾中執行下列命令，將遙測傳送至 IoT 中樞並接聽雲端到裝置訊息：</span><span class="sxs-lookup"><span data-stu-id="6b0d6-150">At the command prompt in the **simulateddevice** folder, run the following command to send telemetry to IoT Hub and to listen for cloud-to-device messages:</span></span>
   
    ```shell
    node SimulatedDevice.js 
    ```
   
    ![執行模擬裝置應用程式][img-simulated-device]
2. <span data-ttu-id="6b0d6-152">在命令提示字元中，於 **sendcloudtodevicemessage** 資料夾中執行下列命令，以傳送雲端到裝置訊息並等候通知的意見反應︰</span><span class="sxs-lookup"><span data-stu-id="6b0d6-152">At a command prompt in the **sendcloudtodevicemessage** folder, run the following command to send a cloud-to-device message and wait for the acknowledgment feedback:</span></span>
   
    ```shell
    node SendCloudToDeviceMessage.js 
    ```
   
    ![執行應用程式以傳送雲端到裝置命令][img-send-command]
   
   > [!NOTE]
   > <span data-ttu-id="6b0d6-154">為了簡單起見，本教學課程不會實作任何重試原則。</span><span class="sxs-lookup"><span data-stu-id="6b0d6-154">For simplicity's sake, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="6b0d6-155">在生產環境程式碼中，您應該如 MSDN 文章 [暫時性錯誤處理]所建議，實作重試原則 (例如指數型輪詢)。</span><span class="sxs-lookup"><span data-stu-id="6b0d6-155">In production code, you should implement retry policies (such as exponential backoff), as suggested in the MSDN article [Transient Fault Handling].</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="6b0d6-156">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6b0d6-156">Next steps</span></span>
<span data-ttu-id="6b0d6-157">在本教學課程中，您已了解如何傳送和接收雲端到裝置的訊息。</span><span class="sxs-lookup"><span data-stu-id="6b0d6-157">In this tutorial, you learned how to send and receive cloud-to-device messages.</span></span> 

<span data-ttu-id="6b0d6-158">若要查看使用 IoT 中樞的完整端對端解決方案範例，請參閱 [Azure IoT 套件]。</span><span class="sxs-lookup"><span data-stu-id="6b0d6-158">To see examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Suite].</span></span>

<span data-ttu-id="6b0d6-159">若要深入了解如何使用 IoT 中樞開發解決方案，請參閱 [IoT 中樞開發人員指南]。</span><span class="sxs-lookup"><span data-stu-id="6b0d6-159">To learn more about developing solutions with IoT Hub, see the [IoT Hub developer guide].</span></span>

<!-- Images -->
[img-simulated-device]: media/iot-hub-node-node-c2d/receivec2d.png
[img-send-command]:  media/iot-hub-node-node-c2d/sendc2d.png

<!-- Links -->

<span data-ttu-id="6b0d6-160">[開始使用 IoT 中樞]: iot-hub-node-node-getstarted.md</span><span class="sxs-lookup"><span data-stu-id="6b0d6-160">[Get started with IoT Hub]: iot-hub-node-node-getstarted.md</span></span>
[IoT Hub developer guide - C2D]: iot-hub-devguide-messaging.md
<span data-ttu-id="6b0d6-161">[IoT 中樞開發人員指南]: iot-hub-devguide.md</span><span class="sxs-lookup"><span data-stu-id="6b0d6-161">[IoT Hub developer guide]: iot-hub-devguide.md</span></span>
<span data-ttu-id="6b0d6-162">[Azure IoT 開發人員中樞]: http://www.azure.com/develop/iot</span><span class="sxs-lookup"><span data-stu-id="6b0d6-162">[Azure IoT Developer Center]: http://www.azure.com/develop/iot</span></span>
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
<span data-ttu-id="6b0d6-163">[暫時性錯誤處理]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx</span><span class="sxs-lookup"><span data-stu-id="6b0d6-163">[Transient Fault Handling]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx</span></span>
<span data-ttu-id="6b0d6-164">[Azure 入口網站]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="6b0d6-164">[Azure portal]: https://portal.azure.com</span></span>
<span data-ttu-id="6b0d6-165">[Azure IoT 套件]: https://azure.microsoft.com/documentation/suites/iot-suite/</span><span class="sxs-lookup"><span data-stu-id="6b0d6-165">[Azure IoT Suite]: https://azure.microsoft.com/documentation/suites/iot-suite/</span></span>
