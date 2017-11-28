---
title: "aaaProcess Azure IoT Hub 裝置到雲端訊息 (Java) |Microsoft 文件"
description: "如何使用路由規則和自訂端點 toodispatch IoT 中樞裝置到雲端訊息 tooprocess 訊息 tooother 後端服務。"
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
ms.openlocfilehash: 084e84e721ca4297c4d7d6cb06a43b0bed9bce85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="process-iot-hub-device-to-cloud-messages-java"></a><span data-ttu-id="eb718-103">處理 IoT 中樞的裝置到雲端訊息 (Java)</span><span class="sxs-lookup"><span data-stu-id="eb718-103">Process IoT Hub device-to-cloud messages (Java)</span></span>

[!INCLUDE [iot-hub-selector-process-d2c](../../includes/iot-hub-selector-process-d2c.md)]

<span data-ttu-id="eb718-104">Azure IoT 中樞是一項完全受管理的服務，可在數百萬個裝置和一個解決方案後端之間啟用可靠且安全的雙向通訊。</span><span class="sxs-lookup"><span data-stu-id="eb718-104">Azure IoT Hub is a fully managed service that enables reliable and secure bi-directional communications between millions of devices and a solution back end.</span></span> <span data-ttu-id="eb718-105">其他教學課程 ([開始使用 IoT 中樞]和[傳送雲端到裝置訊息與 IoT 中樞][lnk-c2d]) 顯示如何 toouse hello 基本裝置到雲端 」 和 「 雲端到裝置IoT 中樞的傳訊功能。</span><span class="sxs-lookup"><span data-stu-id="eb718-105">Other tutorials ([Get started with IoT Hub] and [Send cloud-to-device messages with IoT Hub][lnk-c2d]) show you how toouse hello basic device-to-cloud and cloud-to-device messaging functionality of IoT Hub.</span></span>

<span data-ttu-id="eb718-106">本教學課程是 hello 程式碼所示 hello[開始使用 IoT 中樞]教學課程中，並顯示 toouse 可擴充的方式郵件路由 tooprocess 裝置到雲端訊息的方式。</span><span class="sxs-lookup"><span data-stu-id="eb718-106">This tutorial builds on hello code shown in hello [Get started with IoT Hub] tutorial, and shows you how toouse message routing tooprocess device-to-cloud messages in a scalable way.</span></span> <span data-ttu-id="eb718-107">hello 教學課程說明如何 tooprocess 訊息需要立即採取行動 hello 方案從後端。</span><span class="sxs-lookup"><span data-stu-id="eb718-107">hello tutorial illustrates how tooprocess messages that require immediate action from hello solution back end.</span></span> <span data-ttu-id="eb718-108">例如，裝置可能會傳送一則警示訊息，以觸發將票證插入 CRM 系統的作業。</span><span class="sxs-lookup"><span data-stu-id="eb718-108">For example, a device might send an alarm message that triggers inserting a ticket into a CRM system.</span></span> <span data-ttu-id="eb718-109">相較之下，資料點訊息只會饋送至分析引擎。</span><span class="sxs-lookup"><span data-stu-id="eb718-109">By contrast, data-point messages simply feed into an analytics engine.</span></span> <span data-ttu-id="eb718-110">例如，從 toobe 儲存供稍後分析的裝置的溫度遙測是資料點的訊息。</span><span class="sxs-lookup"><span data-stu-id="eb718-110">For example, temperature telemetry from a device that is toobe stored for later analysis is a data-point message.</span></span>

<span data-ttu-id="eb718-111">在本教學課程的 hello 最後，您可以執行三個 Java 主控台應用程式：</span><span class="sxs-lookup"><span data-stu-id="eb718-111">At hello end of this tutorial, you run three Java console apps:</span></span>

* <span data-ttu-id="eb718-112">**模擬裝置**，hello hello 中建立的應用程式的修改的版本[開始使用 IoT 中樞]教學課程中，傳送的資料點裝置到雲端訊息每秒，而互動式裝置到雲端訊息每隔 10秒數。</span><span class="sxs-lookup"><span data-stu-id="eb718-112">**simulated-device**, a modified version of hello app created in hello [Get started with IoT Hub] tutorial, sends data-point device-to-cloud messages every second, and interactive device-to-cloud messages every 10 seconds.</span></span> <span data-ttu-id="eb718-113">此應用程式使用 hello AMQP 通訊協定 toocommunicate 與 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="eb718-113">This app uses hello AMQP protocol toocommunicate with IoT Hub.</span></span>
* <span data-ttu-id="eb718-114">**閱讀 d2c 郵件**會顯示您裝置的應用程式所傳送的 hello 遙測。</span><span class="sxs-lookup"><span data-stu-id="eb718-114">**read-d2c-messages** displays hello telemetry sent by your device app.</span></span>
* <span data-ttu-id="eb718-115">**讀取關鍵佇列**取消佇列 hello 重大訊息從 hello Service Bus 佇列附加 toohello IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="eb718-115">**read-critical-queue** de-queues hello critical messages from hello Service Bus queue attached toohello IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="eb718-116">IoT 中樞對於許多裝置平台和語言 (包括 C、Java 和 JavaScript) 提供 SDK 支援。</span><span class="sxs-lookup"><span data-stu-id="eb718-116">IoT Hub has SDK support for many device platforms and languages, including C, Java, and JavaScript.</span></span> <span data-ttu-id="eb718-117">如需如何 tooreplace hello 本教學課程中使用實體裝置，裝置的指示和如何 tooconnect 裝置 tooan IoT 中樞，請參閱 hello [Azure IoT 開發人員中心]。</span><span class="sxs-lookup"><span data-stu-id="eb718-117">For instructions on how tooreplace hello device in this tutorial with a physical device, and how tooconnect devices tooan IoT Hub, see hello [Azure IoT Developer Center].</span></span>

<span data-ttu-id="eb718-118">toocomplete 本教學課程中，您需要遵循的 hello:</span><span class="sxs-lookup"><span data-stu-id="eb718-118">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="eb718-119">完成的工作版的 hello[開始使用 IoT 中樞]教學課程。</span><span class="sxs-lookup"><span data-stu-id="eb718-119">A complete working version of hello [Get started with IoT Hub] tutorial.</span></span>
* <span data-ttu-id="eb718-120">最新 hello [Java SE 開發套件 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span><span class="sxs-lookup"><span data-stu-id="eb718-120">hello latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span>
* [<span data-ttu-id="eb718-121">Maven 3</span><span class="sxs-lookup"><span data-stu-id="eb718-121">Maven 3</span></span>](https://maven.apache.org/install.html)
* <span data-ttu-id="eb718-122">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="eb718-122">An active Azure account.</span></span> <span data-ttu-id="eb718-123">(如果您沒有帳戶，只需要幾分鐘的時間就可以建立 [免費帳戶][lnk-free-trial])。</span><span class="sxs-lookup"><span data-stu-id="eb718-123">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

<span data-ttu-id="eb718-124">您應具備 [Azure 儲存體]和 [Azure 服務匯流排]的基本知識。</span><span class="sxs-lookup"><span data-stu-id="eb718-124">You should have some basic knowledge of [Azure Storage] and [Azure Service Bus].</span></span>

## <a name="send-interactive-messages-from-a-device-app"></a><span data-ttu-id="eb718-125">從裝置應用程式傳送互動式訊息</span><span class="sxs-lookup"><span data-stu-id="eb718-125">Send interactive messages from a device app</span></span>
<span data-ttu-id="eb718-126">在本節中，您將修改 hello 裝置應用程式，您可以在 hello[開始使用 IoT 中樞]教學課程 toooccasionally 傳送需要立即處理的訊息。</span><span class="sxs-lookup"><span data-stu-id="eb718-126">In this section, you modify hello device app you created in hello [Get started with IoT Hub] tutorial toooccasionally send messages that require immediate processing.</span></span>

1. <span data-ttu-id="eb718-127">使用文字編輯器 tooopen hello simulated-device\src\main\java\com\mycompany\app\App.java 檔案。</span><span class="sxs-lookup"><span data-stu-id="eb718-127">Use a text editor tooopen hello simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span> <span data-ttu-id="eb718-128">這個檔案包含 hello hello 碼**模擬裝置**hello 中建立的應用程式[開始使用 IoT 中樞]教學課程。</span><span class="sxs-lookup"><span data-stu-id="eb718-128">This file contains hello code for hello **simulated-device** app you created in hello [Get started with IoT Hub] tutorial.</span></span>

2. <span data-ttu-id="eb718-129">取代 hello **MessageSender**類別以下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="eb718-129">Replace hello **MessageSender** class with hello following code:</span></span>

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
   
    <span data-ttu-id="eb718-130">此方法會隨機將 hello 屬性`"level": "critical"`toomessages 傳送 hello 裝置，這將模擬 hello 應用程式後端時，需要立即採取行動的訊息。</span><span class="sxs-lookup"><span data-stu-id="eb718-130">This method randomly adds hello property `"level": "critical"` toomessages sent by hello device, which simulates a message that requires immediate action by hello application back-end.</span></span> <span data-ttu-id="eb718-131">hello 應用程式將此資訊傳遞在 hello 訊息內容中，而不是在 hello 訊息主體中，因此該 IoT 中樞可以路由傳送 hello 訊息 toohello 適當訊息目的地。</span><span class="sxs-lookup"><span data-stu-id="eb718-131">hello application passes this information in hello message properties, instead of in hello message body, so that IoT Hub can route hello message toohello proper message destination.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="eb718-132">您可以使用訊息內容 tooroute 訊息各種案例，包括冷路徑的處理，此外 toohello 最忙碌路徑範例所示。</span><span class="sxs-lookup"><span data-stu-id="eb718-132">You can use message properties tooroute messages for various scenarios including cold-path processing, in addition toohello hot path example shown here.</span></span>

2. <span data-ttu-id="eb718-133">儲存並關閉 hello simulated-device\src\main\java\com\mycompany\app\App.java 檔案。</span><span class="sxs-lookup"><span data-stu-id="eb718-133">Save and close hello simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span>

    > [!NOTE]
    > <span data-ttu-id="eb718-134">為了簡化的 hello 起見，本教學課程未實作任何重試原則。</span><span class="sxs-lookup"><span data-stu-id="eb718-134">For hello sake of simplicity, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="eb718-135">在實際執行程式碼，您應該實作重試原則，例如 hello MSDN 文章中建議的指數型撤退[暫時性錯誤處理]。</span><span class="sxs-lookup"><span data-stu-id="eb718-135">In production code, you should implement a retry policy such as exponential backoff, as suggested in hello MSDN article [Transient Fault Handling].</span></span>

3. <span data-ttu-id="eb718-136">toobuild hello**模擬裝置**使用 Maven，應用程式執行下列命令在 hello hello 模擬裝置資料夾中的命令提示字元的 hello:</span><span class="sxs-lookup"><span data-stu-id="eb718-136">toobuild hello **simulated-device** app using Maven, execute hello following command at hello command prompt in hello simulated-device folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="add-a-queue-tooyour-iot-hub-and-route-messages-tooit"></a><span data-ttu-id="eb718-137">新增佇列 tooyour IoT 中樞與路由訊息 tooit</span><span class="sxs-lookup"><span data-stu-id="eb718-137">Add a queue tooyour IoT hub and route messages tooit</span></span>

<span data-ttu-id="eb718-138">在本節中，您可以建立服務匯流排佇列、 tooyour IoT 中樞時，將它連接並設定 IoT 中樞 toosend 訊息 toohello 佇列根據 hello hello 訊息上的屬性存在。</span><span class="sxs-lookup"><span data-stu-id="eb718-138">In this section, you create a Service Bus queue, connect it tooyour IoT hub, and configure your IoT hub toosend messages toohello queue based on hello presence of a property on hello message.</span></span> <span data-ttu-id="eb718-139">如需如何 tooprocess 訊息從服務匯流排佇列的詳細資訊，請參閱[開始使用佇列][lnk-sb-queues-java]。</span><span class="sxs-lookup"><span data-stu-id="eb718-139">For more information about how tooprocess messages from Service Bus queues, see [Get started with queues][lnk-sb-queues-java].</span></span>

1. <span data-ttu-id="eb718-140">如[開始使用佇列][lnk-sb-queues-java]所述，建立服務匯流排佇列。</span><span class="sxs-lookup"><span data-stu-id="eb718-140">Create a Service Bus queue as described in [Get started with queues][lnk-sb-queues-java].</span></span> <span data-ttu-id="eb718-141">記下 hello 命名空間和佇列名稱。</span><span class="sxs-lookup"><span data-stu-id="eb718-141">Make a note of hello namespace and queue name.</span></span>

2. <span data-ttu-id="eb718-142">在 hello Azure 入口網站，開啟您的 IoT 中樞，然後按一下**端點**。</span><span class="sxs-lookup"><span data-stu-id="eb718-142">In hello Azure portal, open your IoT hub and click **Endpoints**.</span></span>

    ![IoT 中樞端點][30]

3. <span data-ttu-id="eb718-144">在 hello**端點**刀鋒視窗中，按一下 **新增**在 hello 頂端 tooadd 佇列 tooyour IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="eb718-144">In hello **Endpoints** blade, click **Add** at hello top tooadd your queue tooyour IoT hub.</span></span> <span data-ttu-id="eb718-145">名稱 hello 端點**CriticalQueue**並用 hello 下拉式清單 tooselect **Service Bus 佇列**、 hello 佇列所在的服務匯流排命名空間和 hello 您的佇列名稱。</span><span class="sxs-lookup"><span data-stu-id="eb718-145">Name hello endpoint **CriticalQueue** and use hello drop-downs tooselect **Service Bus queue**, hello Service Bus namespace in which your queue resides, and hello name of your queue.</span></span> <span data-ttu-id="eb718-146">當您完成之後時，按一下 **儲存**hello 底部。</span><span class="sxs-lookup"><span data-stu-id="eb718-146">When you are done, click **Save** at hello bottom.</span></span>

    ![新增端點][31]

4. <span data-ttu-id="eb718-148">現在按一下 IoT 中樞中的 [路由]。</span><span class="sxs-lookup"><span data-stu-id="eb718-148">Now click **Routes** in your IoT Hub.</span></span> <span data-ttu-id="eb718-149">按一下**新增**頂端 hello hello 刀鋒視窗 toocreate 加入路由傳送訊息 toohello 佇列只路由規則。</span><span class="sxs-lookup"><span data-stu-id="eb718-149">Click **Add** at hello top of hello blade toocreate a routing rule that routes messages toohello queue you just added.</span></span> <span data-ttu-id="eb718-150">選取**DeviceTelemetry** hello 的資料來源。</span><span class="sxs-lookup"><span data-stu-id="eb718-150">Select **DeviceTelemetry** as hello source of data.</span></span> <span data-ttu-id="eb718-151">輸入`level="critical"`做為 hello 條件，然後選擇您剛才加入做為自訂的端點，如 hello 路由規則端點 hello 佇列。</span><span class="sxs-lookup"><span data-stu-id="eb718-151">Enter `level="critical"` as hello condition, and choose hello queue you just added as a custom endpoint as hello routing rule endpoint.</span></span> <span data-ttu-id="eb718-152">當您完成之後時，按一下 **儲存**hello 底部。</span><span class="sxs-lookup"><span data-stu-id="eb718-152">When you are done, click **Save** at hello bottom.</span></span>

    ![新增路由][32]

    <span data-ttu-id="eb718-154">請確定 hello 後援路由設定得**ON**。</span><span class="sxs-lookup"><span data-stu-id="eb718-154">Make sure hello fallback route is set too**ON**.</span></span> <span data-ttu-id="eb718-155">IoT 中樞 hello 預設設定此設定。</span><span class="sxs-lookup"><span data-stu-id="eb718-155">This setting is hello default configuration of an IoT hub.</span></span>

    ![後援路由][33]

## <a name="optional-read-from-hello-queue-endpoint"></a><span data-ttu-id="eb718-157">（選擇性）讀取 hello 佇列端點</span><span class="sxs-lookup"><span data-stu-id="eb718-157">(Optional) Read from hello queue endpoint</span></span>

<span data-ttu-id="eb718-158">您可以選擇性地讀取 hello 訊息 hello 佇列端點中的 hello 指示[開始使用佇列][lnk-sb-queues-java]。</span><span class="sxs-lookup"><span data-stu-id="eb718-158">You can optionally read hello messages from hello queue endpoint by following hello instructions in [Get started with queues][lnk-sb-queues-java].</span></span> <span data-ttu-id="eb718-159">名稱 hello 應用程式**讀取關鍵佇列**。</span><span class="sxs-lookup"><span data-stu-id="eb718-159">Name hello app **read-critical-queue**.</span></span>

## <a name="run-hello-applications"></a><span data-ttu-id="eb718-160">執行 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="eb718-160">Run hello applications</span></span>

<span data-ttu-id="eb718-161">現在您已準備好 toorun hello 三個應用程式。</span><span class="sxs-lookup"><span data-stu-id="eb718-161">Now you are ready toorun hello three applications.</span></span>

1. <span data-ttu-id="eb718-162">toorun hello**閱讀 d2c 郵件**應用程式，在命令提示字元或殼層巡覽 toohello 讀取 d2c 資料夾，並執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="eb718-162">toorun hello **read-d2c-messages** application, in a command prompt or shell navigate toohello read-d2c folder and execute hello following command:</span></span>

   ```cmd/sh
   mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
   ```

   ![執行 read-d2c-messages][readd2c]

2. <span data-ttu-id="eb718-164">toorun hello**讀取關鍵佇列**應用程式，在命令提示字元或殼層巡覽 toohello 讀取關鍵佇列資料夾，並執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="eb718-164">toorun hello **read-critical-queue** application, in a command prompt or shell navigate toohello read-critical-queue folder and execute hello following command:</span></span>

   ```cmd/sh
   mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
   ```
   
   ![執行 read-critical-messages][readqueue]

3. <span data-ttu-id="eb718-166">toorun hello**模擬裝置**應用程式中的，在命令提示字元或殼層巡覽 toohello 模擬裝置資料夾，並執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="eb718-166">toorun hello **simulated-device** app, in a command prompt or shell navigate toohello simulated-device folder and execute hello following command:</span></span>

   ```cmd/sh
   mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
   ```
   
   ![執行 simulated-device][simulateddevice]

## <a name="next-steps"></a><span data-ttu-id="eb718-168">後續步驟</span><span class="sxs-lookup"><span data-stu-id="eb718-168">Next steps</span></span>

<span data-ttu-id="eb718-169">在本教學課程中，您學會如何 tooreliably 裝置到雲端訊息分派使用 IoT 中樞的 hello 訊息路由功能。</span><span class="sxs-lookup"><span data-stu-id="eb718-169">In this tutorial, you learned how tooreliably dispatch device-to-cloud messages by using hello message routing functionality of IoT Hub.</span></span>

<span data-ttu-id="eb718-170">hello [toosend 雲端到裝置與 IoT 中樞的訊息][ lnk-c2d]顯示 toosend 訊息從您的方案後端 tooyour 裝置的方式。</span><span class="sxs-lookup"><span data-stu-id="eb718-170">hello [How toosend cloud-to-device messages with IoT Hub][lnk-c2d] shows you how toosend messages tooyour devices from your solution back end.</span></span>

<span data-ttu-id="eb718-171">完整的端對端解決方案使用 IoT 中樞 toosee 範例請參閱[Azure IoT 套件][lnk-suite]。</span><span class="sxs-lookup"><span data-stu-id="eb718-171">toosee examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Suite][lnk-suite].</span></span>

<span data-ttu-id="eb718-172">toolearn 進一步了解開發與 IoT 中樞的解決方案，請參閱 「 hello [IoT 中樞開發人員指南]。</span><span class="sxs-lookup"><span data-stu-id="eb718-172">toolearn more about developing solutions with IoT Hub, see hello [IoT Hub developer guide].</span></span>

<span data-ttu-id="eb718-173">請參閱詳細訊息路由在 IoT 中樞 toolearn[傳送和接收訊息與 IoT 中樞][lnk-devguide-messaging]。</span><span class="sxs-lookup"><span data-stu-id="eb718-173">toolearn more about message routing in IoT Hub, see [Send and receive messages with IoT Hub][lnk-devguide-messaging].</span></span>

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

[Azure 儲存體]: https://azure.microsoft.com/documentation/services/storage/
[Azure 服務匯流排]: https://azure.microsoft.com/documentation/services/service-bus/

[IoT 中樞開發人員指南]: iot-hub-devguide.md
[lnk-devguide-messaging]: iot-hub-devguide-messaging.md
[開始使用 IoT 中樞]: iot-hub-java-java-getstarted.md
[Azure IoT 開發人員中心]: https://azure.microsoft.com/develop/iot
[暫時性錯誤處理]: https://msdn.microsoft.com/library/hh675232.aspx

<!-- Links -->
[暫時性錯誤處理]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-c2d]: iot-hub-java-java-c2d.md
[lnk-suite]: https://azure.microsoft.com/documentation/suites/iot-suite/
