---
title: "處理 Azure IoT 中樞的裝置到雲端訊息 (Java) | Microsoft Docs"
description: "如何使用路由規則和自訂端點來處理 IoT 中樞的裝置到雲端訊息，以將訊息分派至其他後端服務。"
services: iot-hub
documentationcenter: java
author: dominicbetts
manager: timlt
editor: 
ms.assetid: bd9af5f9-a740-4780-a2a6-8c0e2752cf48
ms.service: iot-hub
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: dobett
ms.openlocfilehash: d1aca8f39e305105d4ec9f63fbe7bee95487e294
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="process-iot-hub-device-to-cloud-messages-java"></a><span data-ttu-id="045dc-103">處理 IoT 中樞的裝置到雲端訊息 (Java)</span><span class="sxs-lookup"><span data-stu-id="045dc-103">Process IoT Hub device-to-cloud messages (Java)</span></span>

[!INCLUDE [iot-hub-selector-process-d2c](../../includes/iot-hub-selector-process-d2c.md)]

<span data-ttu-id="045dc-104">Azure IoT 中樞是一項完全受管理的服務，可在數百萬個裝置和一個解決方案後端之間啟用可靠且安全的雙向通訊。</span><span class="sxs-lookup"><span data-stu-id="045dc-104">Azure IoT Hub is a fully managed service that enables reliable and secure bi-directional communications between millions of devices and a solution back end.</span></span> <span data-ttu-id="045dc-105">其他教學課程 ([開始使用IoT 中樞入門]和[使用 IoT 中樞傳送雲端到裝置訊息][lnk-c2d]) 說明如何使用 IoT 中樞的裝置到雲端和雲端到裝置的基本傳訊功能。</span><span class="sxs-lookup"><span data-stu-id="045dc-105">Other tutorials ([Get started with IoT Hub] and [Send cloud-to-device messages with IoT Hub][lnk-c2d]) show you how to use the basic device-to-cloud and cloud-to-device messaging functionality of IoT Hub.</span></span>

<span data-ttu-id="045dc-106">本教學課程是以 [開始使用IoT 中樞入門]中顯示的程式碼為基礎，並示範如何使用訊息路由以可調整的方式來處理裝置到雲端訊息。</span><span class="sxs-lookup"><span data-stu-id="045dc-106">This tutorial builds on the code shown in the [Get started with IoT Hub] tutorial, and shows you how to use message routing to process device-to-cloud messages in a scalable way.</span></span> <span data-ttu-id="045dc-107">本教學課程說明如何從解決方案後端處理需要立即採取行動的訊息。</span><span class="sxs-lookup"><span data-stu-id="045dc-107">The tutorial illustrates how to process messages that require immediate action from the solution back end.</span></span> <span data-ttu-id="045dc-108">例如，裝置可能會傳送一則警示訊息，以觸發將票證插入 CRM 系統的作業。</span><span class="sxs-lookup"><span data-stu-id="045dc-108">For example, a device might send an alarm message that triggers inserting a ticket into a CRM system.</span></span> <span data-ttu-id="045dc-109">相較之下，資料點訊息只會饋送至分析引擎。</span><span class="sxs-lookup"><span data-stu-id="045dc-109">By contrast, data-point messages simply feed into an analytics engine.</span></span> <span data-ttu-id="045dc-110">例如，來自裝置且要儲存以供日後分析的溫度遙測就是資料點訊息。</span><span class="sxs-lookup"><span data-stu-id="045dc-110">For example, temperature telemetry from a device that is to be stored for later analysis is a data-point message.</span></span>

<span data-ttu-id="045dc-111">在本教學課程結尾，您會執行三個 Java 主控台應用程式：</span><span class="sxs-lookup"><span data-stu-id="045dc-111">At the end of this tutorial, you run three Java console apps:</span></span>

* <span data-ttu-id="045dc-112">**simulated-device**(在 [開始使用IoT 中樞入門] 教學課程中建立之應用程式的已修改版本) 會每秒傳送資料點裝置到雲端訊息，以及每 10 秒傳送互動式裝置到雲端訊息。</span><span class="sxs-lookup"><span data-stu-id="045dc-112">**simulated-device**, a modified version of the app created in the [Get started with IoT Hub] tutorial, sends data-point device-to-cloud messages every second, and interactive device-to-cloud messages every 10 seconds.</span></span> <span data-ttu-id="045dc-113">此應用程式會使用 AMQP 通訊協定與「IoT 中樞」進行通訊。</span><span class="sxs-lookup"><span data-stu-id="045dc-113">This app uses the AMQP protocol to communicate with IoT Hub.</span></span>
* <span data-ttu-id="045dc-114">**read-d2c-messages** 會顯示您的裝置應用程式所傳送的遙測資料。</span><span class="sxs-lookup"><span data-stu-id="045dc-114">**read-d2c-messages** displays the telemetry sent by your device app.</span></span>
* <span data-ttu-id="045dc-115">**read-critical-queue** 可從連接到 IoT 中樞的服務匯流排佇列中移除重要訊息。</span><span class="sxs-lookup"><span data-stu-id="045dc-115">**read-critical-queue** de-queues the critical messages from the Service Bus queue attached to the IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="045dc-116">IoT 中樞對於許多裝置平台和語言 (包括 C、Java 和 JavaScript) 提供 SDK 支援。</span><span class="sxs-lookup"><span data-stu-id="045dc-116">IoT Hub has SDK support for many device platforms and languages, including C, Java, and JavaScript.</span></span> <span data-ttu-id="045dc-117">如需了解如何以實體裝置取代本教學課程中的裝置，以及如何將裝置連接到「IoT 中樞」，請參閱 [Azure IoT 開發人員中心]。</span><span class="sxs-lookup"><span data-stu-id="045dc-117">For instructions on how to replace the device in this tutorial with a physical device, and how to connect devices to an IoT Hub, see the [Azure IoT Developer Center].</span></span>

<span data-ttu-id="045dc-118">若要完成此教學課程，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="045dc-118">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="045dc-119">[開始使用IoT 中樞入門] 教學課程的完整運作版本。</span><span class="sxs-lookup"><span data-stu-id="045dc-119">A complete working version of the [Get started with IoT Hub] tutorial.</span></span>
* <span data-ttu-id="045dc-120">最新的 [Java SE 開發套件 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span><span class="sxs-lookup"><span data-stu-id="045dc-120">The latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span>
* [<span data-ttu-id="045dc-121">Maven 3</span><span class="sxs-lookup"><span data-stu-id="045dc-121">Maven 3</span></span>](https://maven.apache.org/install.html)
* <span data-ttu-id="045dc-122">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="045dc-122">An active Azure account.</span></span> <span data-ttu-id="045dc-123">(如果您沒有帳戶，只需要幾分鐘的時間就可以建立 [免費帳戶][lnk-free-trial])。</span><span class="sxs-lookup"><span data-stu-id="045dc-123">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

<span data-ttu-id="045dc-124">您應具備 [Azure 儲存體]和 [Azure 服務匯流排]的基本知識。</span><span class="sxs-lookup"><span data-stu-id="045dc-124">You should have some basic knowledge of [Azure Storage] and [Azure Service Bus].</span></span>

## <a name="send-interactive-messages-from-a-device-app"></a><span data-ttu-id="045dc-125">從裝置應用程式傳送互動式訊息</span><span class="sxs-lookup"><span data-stu-id="045dc-125">Send interactive messages from a device app</span></span>
<span data-ttu-id="045dc-126">在本節中，您會修改您在[開始使用IoT 中樞入門]教學課程中建立的裝置應用程式，偶爾傳送需要立即處理的訊息。</span><span class="sxs-lookup"><span data-stu-id="045dc-126">In this section, you modify the device app you created in the [Get started with IoT Hub] tutorial to occasionally send messages that require immediate processing.</span></span>

1. <span data-ttu-id="045dc-127">使用文字編輯器來開啟 simulated-device\src\main\java\com\mycompany\app\App.java 檔案。</span><span class="sxs-lookup"><span data-stu-id="045dc-127">Use a text editor to open the simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span> <span data-ttu-id="045dc-128">這個檔案包含您在 **開始使用 IoT 中樞** 教學課程中建立的 [開始使用IoT 中樞入門] 應用程式。</span><span class="sxs-lookup"><span data-stu-id="045dc-128">This file contains the code for the **simulated-device** app you created in the [Get started with IoT Hub] tutorial.</span></span>

2. <span data-ttu-id="045dc-129">以下列程式碼取代 **MessageSender** 類別：</span><span class="sxs-lookup"><span data-stu-id="045dc-129">Replace the **MessageSender** class with the following code:</span></span>

    ```java
    private static class MessageSender implements Runnable {

        public void run()  {
            try {
                double minTemperature = 20;
                double minHumidity = 60;
                Random rand = new Random();

                while (true) {
                    String msgStr;
                    Message msg;
                    if (new Random().nextDouble() > 0.7) {
                        msgStr = "This is a critical message.";
                        msg = new Message(msgStr);
                        msg.setProperty("level", "critical");
                    } else {
                        double currentTemperature = minTemperature + rand.nextDouble() * 15;
                        double currentHumidity = minHumidity + rand.nextDouble() * 20; 
                        TelemetryDataPoint telemetryDataPoint = new TelemetryDataPoint();
                        telemetryDataPoint.deviceId = deviceId;
                        telemetryDataPoint.temperature = currentTemperature;
                        telemetryDataPoint.humidity = currentHumidity;

                        msgStr = telemetryDataPoint.serialize();
                        msg = new Message(msgStr);
                    }
                    
                    System.out.println("Sending: " + msgStr);

                    Object lockobj = new Object();
                    EventCallback callback = new EventCallback();
                    client.sendEventAsync(msg, callback, lockobj);

                    synchronized (lockobj) {
                        lockobj.wait();
                    }
                    Thread.sleep(1000);
                }
            } catch (InterruptedException e) {
                System.out.println("Finished.");
            }
        }
    }
    ```
   
    <span data-ttu-id="045dc-130">這個方法會隨機將 `"level": "critical"` 屬性新增至裝置所傳送的訊息，該裝置會模擬需要應用程式後端立即採取行動的訊息。</span><span class="sxs-lookup"><span data-stu-id="045dc-130">This method randomly adds the property `"level": "critical"` to messages sent by the device, which simulates a message that requires immediate action by the application back-end.</span></span> <span data-ttu-id="045dc-131">應用程式會在訊息屬性中傳遞此資訊，而不是在訊息主體中傳遞，因此 IoT 中樞可以將訊息路由傳送至適當的訊息目的地。</span><span class="sxs-lookup"><span data-stu-id="045dc-131">The application passes this information in the message properties, instead of in the message body, so that IoT Hub can route the message to the proper message destination.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="045dc-132">除了此處顯示的最忙碌路徑範例以外，您可以使用訊息屬性來路由傳送各種案例的訊息，包括冷門路徑處理。</span><span class="sxs-lookup"><span data-stu-id="045dc-132">You can use message properties to route messages for various scenarios including cold-path processing, in addition to the hot path example shown here.</span></span>

2. <span data-ttu-id="045dc-133">儲存並關閉 simulated-device\src\main\java\com\mycompany\app\App.java 檔案。</span><span class="sxs-lookup"><span data-stu-id="045dc-133">Save and close the simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span>

    > [!NOTE]
    > <span data-ttu-id="045dc-134">為了簡單起見，本教學課程不會實作任何重試原則。</span><span class="sxs-lookup"><span data-stu-id="045dc-134">For the sake of simplicity, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="045dc-135">在實際程式碼中，您應該如 MSDN 文章 [Transient Fault Handling (暫時性錯誤處理)]所建議來實作重試原則 (例如指數型輪詢)。</span><span class="sxs-lookup"><span data-stu-id="045dc-135">In production code, you should implement a retry policy such as exponential backoff, as suggested in the MSDN article [Transient Fault Handling].</span></span>

3. <span data-ttu-id="045dc-136">若要使用 Maven 建置 **simulated-device** 應用程式，請在命令提示字元中的 simulated-device 資料夾內執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="045dc-136">To build the **simulated-device** app using Maven, execute the following command at the command prompt in the simulated-device folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="add-a-queue-to-your-iot-hub-and-route-messages-to-it"></a><span data-ttu-id="045dc-137">將佇列新增至 IoT 中樞並將訊息路由傳送至該佇列</span><span class="sxs-lookup"><span data-stu-id="045dc-137">Add a queue to your IoT hub and route messages to it</span></span>

<span data-ttu-id="045dc-138">本節中，您會建立服務匯流排佇列、將它連接到您的 IoT 中樞，以及設定您的 IoT 中樞，進而根據訊息的屬性目前狀態，將訊息傳送至佇列。</span><span class="sxs-lookup"><span data-stu-id="045dc-138">In this section, you create a Service Bus queue, connect it to your IoT hub, and configure your IoT hub to send messages to the queue based on the presence of a property on the message.</span></span> <span data-ttu-id="045dc-139">如需有關如何處理來自服務匯流排佇列之訊息的詳細資訊，請參閱[開始使用佇列][lnk-sb-queues-java]。</span><span class="sxs-lookup"><span data-stu-id="045dc-139">For more information about how to process messages from Service Bus queues, see [Get started with queues][lnk-sb-queues-java].</span></span>

1. <span data-ttu-id="045dc-140">如[開始使用佇列][lnk-sb-queues-java]所述，建立服務匯流排佇列。</span><span class="sxs-lookup"><span data-stu-id="045dc-140">Create a Service Bus queue as described in [Get started with queues][lnk-sb-queues-java].</span></span> <span data-ttu-id="045dc-141">記下命名空間和佇列名稱。</span><span class="sxs-lookup"><span data-stu-id="045dc-141">Make a note of the namespace and queue name.</span></span>

2. <span data-ttu-id="045dc-142">在 Azure 入口網站中，開啟 IoT 中樞然後按一下 [端點]。</span><span class="sxs-lookup"><span data-stu-id="045dc-142">In the Azure portal, open your IoT hub and click **Endpoints**.</span></span>

    ![IoT 中樞端點][30]

3. <span data-ttu-id="045dc-144">在 [端點] 刀鋒視窗中，按一下頂端的 [新增] 將您的佇列新增至 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="045dc-144">In the **Endpoints** blade, click **Add** at the top to add your queue to your IoT hub.</span></span> <span data-ttu-id="045dc-145">將端點命名為 **CriticalQueue**，並使用下拉式清單來選取 [服務匯流排佇列]、您的佇列所在的服務匯流排命名空間，以及您的佇列名稱。</span><span class="sxs-lookup"><span data-stu-id="045dc-145">Name the endpoint **CriticalQueue** and use the drop-downs to select **Service Bus queue**, the Service Bus namespace in which your queue resides, and the name of your queue.</span></span> <span data-ttu-id="045dc-146">完成時，請按一下底部的 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="045dc-146">When you are done, click **Save** at the bottom.</span></span>

    ![新增端點][31]

4. <span data-ttu-id="045dc-148">現在按一下 IoT 中樞中的 [路由]。</span><span class="sxs-lookup"><span data-stu-id="045dc-148">Now click **Routes** in your IoT Hub.</span></span> <span data-ttu-id="045dc-149">按一下刀鋒視窗頂端的 [新增] 來建立路由規則，以便將訊息路由傳送至您剛才新增的佇列。</span><span class="sxs-lookup"><span data-stu-id="045dc-149">Click **Add** at the top of the blade to create a routing rule that routes messages to the queue you just added.</span></span> <span data-ttu-id="045dc-150">選取 **DeviceTelemetry** 做為資料來源。</span><span class="sxs-lookup"><span data-stu-id="045dc-150">Select **DeviceTelemetry** as the source of data.</span></span> <span data-ttu-id="045dc-151">輸入 `level="critical"` 做為條件，然後選擇您剛才新增為自訂端點的佇列做為路由規則端點。</span><span class="sxs-lookup"><span data-stu-id="045dc-151">Enter `level="critical"` as the condition, and choose the queue you just added as a custom endpoint as the routing rule endpoint.</span></span> <span data-ttu-id="045dc-152">完成時，請按一下底部的 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="045dc-152">When you are done, click **Save** at the bottom.</span></span>

    ![新增路由][32]

    <span data-ttu-id="045dc-154">確定後援路由設定為 [開啟]。</span><span class="sxs-lookup"><span data-stu-id="045dc-154">Make sure the fallback route is set to **ON**.</span></span> <span data-ttu-id="045dc-155">此設定為 IoT 中樞的預設設定。</span><span class="sxs-lookup"><span data-stu-id="045dc-155">This setting is the default configuration of an IoT hub.</span></span>

    ![後援路由][33]

## <a name="optional-read-from-the-queue-endpoint"></a><span data-ttu-id="045dc-157">(選用) 從佇列端點讀取</span><span class="sxs-lookup"><span data-stu-id="045dc-157">(Optional) Read from the queue endpoint</span></span>

<span data-ttu-id="045dc-158">您可以依照[開始使用佇列][lnk-sb-queues-java]中的指示，選擇性地從佇列端點讀取訊息。</span><span class="sxs-lookup"><span data-stu-id="045dc-158">You can optionally read the messages from the queue endpoint by following the instructions in [Get started with queues][lnk-sb-queues-java].</span></span> <span data-ttu-id="045dc-159">將應用程式命名為 **read-critical-queue**。</span><span class="sxs-lookup"><span data-stu-id="045dc-159">Name the app **read-critical-queue**.</span></span>

## <a name="run-the-applications"></a><span data-ttu-id="045dc-160">執行應用程式</span><span class="sxs-lookup"><span data-stu-id="045dc-160">Run the applications</span></span>

<span data-ttu-id="045dc-161">現在您已經準備好執行這三個應用程式。</span><span class="sxs-lookup"><span data-stu-id="045dc-161">Now you are ready to run the three applications.</span></span>

1. <span data-ttu-id="045dc-162">若要執行 **read-d2c-messages** 應用程式，請在命令提示字元或殼層中，瀏覽至 read-d2c 資料夾，然後執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="045dc-162">To run the **read-d2c-messages** application, in a command prompt or shell navigate to the read-d2c folder and execute the following command:</span></span>

   ```cmd/sh
   mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
   ```

   ![執行 read-d2c-messages][readd2c]

2. <span data-ttu-id="045dc-164">若要執行 **read-critical-queue** 應用程式，請在命令提示字元或殼層中，瀏覽至 read-critical-queue 資料夾，然後執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="045dc-164">To run the **read-critical-queue** application, in a command prompt or shell navigate to the read-critical-queue folder and execute the following command:</span></span>

   ```cmd/sh
   mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
   ```
   
   ![執行 read-critical-messages][readqueue]

3. <span data-ttu-id="045dc-166">若要執行 **simulated-device** 應用程式，請在命令提示字元或殼層中，瀏覽至 [simulated-device] 資料夾，然後執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="045dc-166">To run the **simulated-device** app, in a command prompt or shell navigate to the simulated-device folder and execute the following command:</span></span>

   ```cmd/sh
   mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
   ```
   
   ![執行 simulated-device][simulateddevice]

## <a name="next-steps"></a><span data-ttu-id="045dc-168">後續步驟</span><span class="sxs-lookup"><span data-stu-id="045dc-168">Next steps</span></span>

<span data-ttu-id="045dc-169">在本教學課程中，您已學到如何使用 IoT 中樞的訊息路由功能來可靠地分派裝置到雲端訊息。</span><span class="sxs-lookup"><span data-stu-id="045dc-169">In this tutorial, you learned how to reliably dispatch device-to-cloud messages by using the message routing functionality of IoT Hub.</span></span>

<span data-ttu-id="045dc-170">[如何使用 IoT 中樞傳送雲端到裝置訊息][lnk-c2d]示範如何從解決方案後端將訊息傳送至您的裝置。</span><span class="sxs-lookup"><span data-stu-id="045dc-170">The [How to send cloud-to-device messages with IoT Hub][lnk-c2d] shows you how to send messages to your devices from your solution back end.</span></span>

<span data-ttu-id="045dc-171">若要查看使用 IoT 中樞的完整端對端解決方案範例，請參閱 [Azure IoT 套件][lnk-suite]。</span><span class="sxs-lookup"><span data-stu-id="045dc-171">To see examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Suite][lnk-suite].</span></span>

<span data-ttu-id="045dc-172">若要深入了解如何使用 IoT 中樞開發解決方案，請參閱 [IoT 中樞開發人員指南]。</span><span class="sxs-lookup"><span data-stu-id="045dc-172">To learn more about developing solutions with IoT Hub, see the [IoT Hub developer guide].</span></span>

<span data-ttu-id="045dc-173">若要深入了解 IoT 中樞的訊息路由，請參閱[使用 IoT 中樞傳送和接收訊息][lnk-devguide-messaging]。</span><span class="sxs-lookup"><span data-stu-id="045dc-173">To learn more about message routing in IoT Hub, see [Send and receive messages with IoT Hub][lnk-devguide-messaging].</span></span>

<!-- Images. -->
<!-- TODO: UPDATE PICTURES -->
[simulateddevice]: ./media/iot-hub-java-java-process-d2c/runsimulateddevice.png
[readd2c]: ./media/iot-hub-java-java-process-d2c/runprocessinteractive.png
[readqueue]: ./media/iot-hub-java-java-process-d2c/runprocessd2c.png

[30]: ./media/iot-hub-java-java-process-d2c/click-endpoints.png
[31]: ./media/iot-hub-java-java-process-d2c/endpoint-creation.png
[32]: ./media/iot-hub-java-java-process-d2c/route-creation.png
[33]: ./media/iot-hub-java-java-process-d2c/fallback-route.png

<!-- Links -->

[lnk-sb-queues-java]: ../service-bus-messaging/service-bus-java-how-to-use-queues.md

<span data-ttu-id="045dc-174">[Azure 儲存體]: https://azure.microsoft.com/documentation/services/storage/</span><span class="sxs-lookup"><span data-stu-id="045dc-174">[Azure Storage]: https://azure.microsoft.com/documentation/services/storage/</span></span>
<span data-ttu-id="045dc-175">[Azure 服務匯流排]: https://azure.microsoft.com/documentation/services/service-bus/</span><span class="sxs-lookup"><span data-stu-id="045dc-175">[Azure Service Bus]: https://azure.microsoft.com/documentation/services/service-bus/</span></span>

<span data-ttu-id="045dc-176">[IoT 中樞開發人員指南]: iot-hub-devguide.md</span><span class="sxs-lookup"><span data-stu-id="045dc-176">[IoT Hub developer guide]: iot-hub-devguide.md</span></span>
[lnk-devguide-messaging]: iot-hub-devguide-messaging.md
<span data-ttu-id="045dc-177">[開始使用IoT 中樞入門]: iot-hub-java-java-getstarted.md</span><span class="sxs-lookup"><span data-stu-id="045dc-177">[Get started with IoT Hub]: iot-hub-java-java-getstarted.md</span></span>
<span data-ttu-id="045dc-178">[Azure IoT 開發人員中心]: https://azure.microsoft.com/develop/iot</span><span class="sxs-lookup"><span data-stu-id="045dc-178">[Azure IoT Developer Center]: https://azure.microsoft.com/develop/iot</span></span>
<span data-ttu-id="045dc-179">[Transient Fault Handling (暫時性錯誤處理)]: https://msdn.microsoft.com/library/hh675232.aspx</span><span class="sxs-lookup"><span data-stu-id="045dc-179">[Transient Fault Handling]: https://msdn.microsoft.com/library/hh675232.aspx</span></span>

<!-- Links -->
<span data-ttu-id="045dc-180">[暫時性錯誤處理]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx</span><span class="sxs-lookup"><span data-stu-id="045dc-180">[Transient Fault Handling]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx</span></span>

[lnk-c2d]: iot-hub-java-java-c2d.md
[lnk-suite]: https://azure.microsoft.com/documentation/suites/iot-suite/
