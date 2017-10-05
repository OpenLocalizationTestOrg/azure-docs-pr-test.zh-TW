---
title: "使用 Azure IoT 中樞傳送雲端到裝置訊息 (Java) | Microsoft Docs"
description: "如何使用適用於 Java 的 Azure IoT SDK，將雲端到裝置訊息從 Azure IoT 中樞傳送至裝置。 您可以修改模擬裝置應用程式，以接收雲端到裝置訊息，也可以修改後端應用程式，以傳送雲端到裝置訊息。"
services: iot-hub
documentationcenter: java
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 7f785ea8-e7c2-40c5-87ef-96525e9b9e1e
ms.service: iot-hub
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2017
ms.author: dobett
ms.openlocfilehash: f5e3ac46f4d144b12e2ab7fcfb456665ff6cc68f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="send-cloud-to-device-messages-with-iot-hub-java"></a><span data-ttu-id="ccdb9-104">使用 IoT 中樞傳送雲端到裝置訊息 (Java)</span><span class="sxs-lookup"><span data-stu-id="ccdb9-104">Send cloud-to-device messages with IoT Hub (Java)</span></span>
[!INCLUDE [iot-hub-selector-c2d](../../includes/iot-hub-selector-c2d.md)]

<span data-ttu-id="ccdb9-105">Azure IoT 中樞是一項完全受管理的服務，有助於讓數百萬個裝置和一個解決方案後端進行可靠且安全的雙向通訊。</span><span class="sxs-lookup"><span data-stu-id="ccdb9-105">Azure IoT Hub is a fully managed service that helps enable reliable and secure bi-directional communications between millions of devices and a solution back end.</span></span> <span data-ttu-id="ccdb9-106">[開始使用 IoT 中樞] 教學課程會示範如何建立 IoT 中樞、在其中佈建裝置識別，以及編寫模擬的裝置應用程式，以傳送裝置到雲端的訊息。</span><span class="sxs-lookup"><span data-stu-id="ccdb9-106">The [Get started with IoT Hub] tutorial shows how to create an IoT hub, provision a device identity in it, and code a simulated device app that sends device-to-cloud messages.</span></span>

<span data-ttu-id="ccdb9-107">本教學課程是以 [開始使用 IoT 中樞]為基礎。</span><span class="sxs-lookup"><span data-stu-id="ccdb9-107">This tutorial builds on [Get started with IoT Hub].</span></span> <span data-ttu-id="ccdb9-108">這會說明如何：</span><span class="sxs-lookup"><span data-stu-id="ccdb9-108">It shows you how to:</span></span>

* <span data-ttu-id="ccdb9-109">從您的解決方案後端，透過 IoT 中樞將雲端到裝置訊息傳送給單一裝置。</span><span class="sxs-lookup"><span data-stu-id="ccdb9-109">From your solution back end, send cloud-to-device messages to a single device through IoT Hub.</span></span>
* <span data-ttu-id="ccdb9-110">接收裝置上的雲端到裝置訊息。</span><span class="sxs-lookup"><span data-stu-id="ccdb9-110">Receive cloud-to-device messages on a device.</span></span>
* <span data-ttu-id="ccdb9-111">從您的解決方案後端，要求確認收到從 IoT 中樞傳送到裝置的訊息 (「意見反應」)。</span><span class="sxs-lookup"><span data-stu-id="ccdb9-111">From your solution back end, request delivery acknowledgement (*feedback*) for messages sent to a device from IoT Hub.</span></span>

<span data-ttu-id="ccdb9-112">您可以在 [IoT 中樞開發人員指南][IoT Hub developer guide - C2D]中，找到有關雲端到裝置訊息的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="ccdb9-112">You can find more information on cloud-to-device messages in the [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>

<span data-ttu-id="ccdb9-113">在本教學課程結尾，您將執行兩個 Java 主控台應用程式：</span><span class="sxs-lookup"><span data-stu-id="ccdb9-113">At the end of this tutorial, you run two Java console apps:</span></span>

* <span data-ttu-id="ccdb9-114">**simulated-device**：在 [開始使用 IoT 中樞]中建立的應用程式修改版本，可連接到您的「IoT 中樞」並接收雲端到裝置訊息。</span><span class="sxs-lookup"><span data-stu-id="ccdb9-114">**simulated-device**, a modified version of the app created in [Get started with IoT Hub], which connects to your IoT hub and receives cloud-to-device messages.</span></span>
* <span data-ttu-id="ccdb9-115">**send-c2d-messages**：會將雲端到裝置訊息透過「IoT 中樞」傳送到模擬的裝置應用程式，然後接收其傳遞通知。</span><span class="sxs-lookup"><span data-stu-id="ccdb9-115">**send-c2d-messages**, which sends a cloud-to-device message to the simulated device app through IoT Hub, and then receives its delivery acknowledgement.</span></span>

> [!NOTE]
> <span data-ttu-id="ccdb9-116">「IoT 中樞」透過 Azure IoT 裝置 SDK 為許多裝置平台和語言 (包括 C、Java 及 Javascript) 提供 SDK 支援。</span><span class="sxs-lookup"><span data-stu-id="ccdb9-116">IoT Hub has SDK support for many device platforms and languages (including C, Java, and Javascript) through Azure IoT device SDKs.</span></span> <span data-ttu-id="ccdb9-117">如需有關如何將您的裝置與本教學課程中的程式碼連接 (通常是連接到「Azure IoT 中樞」) 的逐步指示，請參閱 [Azure IoT 開發人員中樞]。</span><span class="sxs-lookup"><span data-stu-id="ccdb9-117">For step-by-step instructions on how to connect your device to this tutorial's code, and generally to Azure IoT Hub, see the [Azure IoT Developer Center].</span></span>

<span data-ttu-id="ccdb9-118">若要完成此教學課程，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="ccdb9-118">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="ccdb9-119">[開始使用 IoT 中樞](iot-hub-java-java-getstarted.md)或[處理 IoT 中樞裝置對雲端訊息](iot-hub-java-java-process-d2c.md)教學課程的完整運作版本。</span><span class="sxs-lookup"><span data-stu-id="ccdb9-119">A complete working version of the [Get started with IoT Hub](iot-hub-java-java-getstarted.md) or [Process IoT Hub device-to-cloud messages](iot-hub-java-java-process-d2c.md) tutorial.</span></span>
* <span data-ttu-id="ccdb9-120">最新的 [Java SE 開發套件 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span><span class="sxs-lookup"><span data-stu-id="ccdb9-120">The latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span>
* [<span data-ttu-id="ccdb9-121">Maven 3</span><span class="sxs-lookup"><span data-stu-id="ccdb9-121">Maven 3</span></span>](https://maven.apache.org/install.html)
* <span data-ttu-id="ccdb9-122">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="ccdb9-122">An active Azure account.</span></span> <span data-ttu-id="ccdb9-123">(如果您沒有帳戶，只需要幾分鐘的時間就可以建立[免費帳戶][lnk-free-trial]。)</span><span class="sxs-lookup"><span data-stu-id="ccdb9-123">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

## <a name="receive-messages-in-the-simulated-device-app"></a><span data-ttu-id="ccdb9-124">在模擬的裝置應用程式中接收訊息</span><span class="sxs-lookup"><span data-stu-id="ccdb9-124">Receive messages in the simulated device app</span></span>

<span data-ttu-id="ccdb9-125">在本節中，您會修改在[開始使用 IoT 中樞]中建立的模擬裝置應用程式，以接收來自 IoT 中樞的雲端對裝置訊息。</span><span class="sxs-lookup"><span data-stu-id="ccdb9-125">In this section, you modify the simulated device app you created in [Get started with IoT Hub] to receive cloud-to-device messages from the IoT hub.</span></span>

1. <span data-ttu-id="ccdb9-126">使用文字編輯器開啟 simulated-device\src\main\java\com\mycompany\app\App.java 檔案。</span><span class="sxs-lookup"><span data-stu-id="ccdb9-126">Using a text editor, open the simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span>

2. <span data-ttu-id="ccdb9-127">在 **App** 類別內新增下列 **MessageCallback** 類別作為巢狀類別。</span><span class="sxs-lookup"><span data-stu-id="ccdb9-127">Add the following **MessageCallback** class as a nested class inside the **App** class.</span></span> <span data-ttu-id="ccdb9-128">裝置從 IoT 中樞接收到訊息時會叫用 **execute** 方法。</span><span class="sxs-lookup"><span data-stu-id="ccdb9-128">The **execute** method is invoked when the device receives a message from IoT Hub.</span></span> <span data-ttu-id="ccdb9-129">在此範例中，裝置一律會通知 IoT 中樞其已完成訊息︰</span><span class="sxs-lookup"><span data-stu-id="ccdb9-129">In this example, the device always notifies the IoT hub that it has completed the message:</span></span>

    ```java
    private static class AppMessageCallback implements MessageCallback {
      public IotHubMessageResult execute(Message msg, Object context) {
        System.out.println("Received message from hub: "
          + new String(msg.getBytes(), Message.DEFAULT_IOTHUB_MESSAGE_CHARSET));
    
        return IotHubMessageResult.COMPLETE;
      }
    }
    ```
3. <span data-ttu-id="ccdb9-130">修改 **main** 方法來建立 **AppMessageCallback** 執行個體，並在其開啟用戶端之前，先呼叫 **setMessageCallback** 方法，如以下所示︰</span><span class="sxs-lookup"><span data-stu-id="ccdb9-130">Modify the **main** method to create an **AppMessageCallback** instance and call the **setMessageCallback** method before it opens the client as follows:</span></span>

    ```java
    client = new DeviceClient(connString, protocol);
   
    MessageCallback callback = new AppMessageCallback();
    client.setMessageCallback(callback, null);
    client.open();
    ```

    > [!NOTE]
    > <span data-ttu-id="ccdb9-131">如果您使用 HTTP 而非 MQTT 或 AMQP 作為傳輸，**DeviceClient** 執行個體將不會經常 (頻率低於每隔 25 分鐘) 檢查「IoT 中樞」是否傳來訊息。</span><span class="sxs-lookup"><span data-stu-id="ccdb9-131">If you use HTTP instead of MQTT or AMQP as the transport, the **DeviceClient** instance checks for messages from IoT Hub infrequently (less than every 25 minutes).</span></span> <span data-ttu-id="ccdb9-132">如需有關 AMQP、AMQP 和 HTTP 支援之間的差異，以及 IoT 中樞節流的詳細資訊，請參閱 [IoT 中樞開發人員指南][IoT Hub developer guide - C2D]。</span><span class="sxs-lookup"><span data-stu-id="ccdb9-132">For more information about the differences between MQTT, AMQP and HTTP support, and IoT Hub throttling, see the [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>

4. <span data-ttu-id="ccdb9-133">若要使用 Maven 建置 **simulated-device** 應用程式，請在命令提示字元中的 simulated-device 資料夾內執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="ccdb9-133">To build the **simulated-device** app using Maven, execute the following command at the command prompt in the simulated-device folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="send-a-cloud-to-device-message"></a><span data-ttu-id="ccdb9-134">傳送雲端到裝置訊息</span><span class="sxs-lookup"><span data-stu-id="ccdb9-134">Send a cloud-to-device message</span></span>

<span data-ttu-id="ccdb9-135">在本節中，您會建立 Java 主控台應用程式，以將雲端到裝置訊息傳送給模擬裝置應用程式。</span><span class="sxs-lookup"><span data-stu-id="ccdb9-135">In this section, you create a Java console app that sends cloud-to-device messages to the simulated device app.</span></span> <span data-ttu-id="ccdb9-136">您需要您在[開始使用 IoT 中樞]教學課程中所新增裝置的裝置識別碼。</span><span class="sxs-lookup"><span data-stu-id="ccdb9-136">You need the device ID of the device you added in the [Get started with IoT Hub] tutorial.</span></span> <span data-ttu-id="ccdb9-137">您也需要中樞的 IoT 中樞連接字串 (可在 [Azure 入口網站]中找到)。</span><span class="sxs-lookup"><span data-stu-id="ccdb9-137">You also need the IoT Hub connection string for your hub that you can find in the [Azure portal].</span></span>

1. <span data-ttu-id="ccdb9-138">在命令提示字元中使用下列命令，建立名為 **send-c2d-messages** 的 Maven 專案。</span><span class="sxs-lookup"><span data-stu-id="ccdb9-138">Create a Maven project called **send-c2d-messages** using the following command at your command prompt.</span></span> <span data-ttu-id="ccdb9-139">注意，此命令是單一且非常長的命令：</span><span class="sxs-lookup"><span data-stu-id="ccdb9-139">Note this command is a single, long command:</span></span>

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=send-c2d-messages -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. <span data-ttu-id="ccdb9-140">在命令提示字元中，瀏覽到新的 send-c2d-messages 資料夾。</span><span class="sxs-lookup"><span data-stu-id="ccdb9-140">At your command prompt, navigate to the new send-c2d-messages folder.</span></span>

3. <span data-ttu-id="ccdb9-141">使用文字編輯器，開啟 [send-c2d-messages] 資料夾中的 pom.xml 檔案，並將下列相依性新增到 [相依性] 節點。</span><span class="sxs-lookup"><span data-stu-id="ccdb9-141">Using a text editor, open the pom.xml file in the send-c2d-messages folder and add the following dependency to the **dependencies** node.</span></span> <span data-ttu-id="ccdb9-142">新增相依性可讓您在應用程式中使用 **iothub-java-service-client** 套件與 IoT 中樞服務進行通訊：</span><span class="sxs-lookup"><span data-stu-id="ccdb9-142">Adding the dependency enables you to use the **iothub-java-service-client** package in your application to communicate with your IoT hub service:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="ccdb9-143">您可以使用 [Maven 搜尋][lnk-maven-service-search]來檢查最新版的 **iot-service-client**。</span><span class="sxs-lookup"><span data-stu-id="ccdb9-143">You can check for the latest version of **iot-service-client** using [Maven search][lnk-maven-service-search].</span></span>

4. <span data-ttu-id="ccdb9-144">儲存並關閉 pom.xml 檔案。</span><span class="sxs-lookup"><span data-stu-id="ccdb9-144">Save and close the pom.xml file.</span></span>

5. <span data-ttu-id="ccdb9-145">使用文字編輯器開啟 send-c2d-messages\src\main\java\com\mycompany\app\App.java 檔案。</span><span class="sxs-lookup"><span data-stu-id="ccdb9-145">Using a text editor, open the send-c2d-messages\src\main\java\com\mycompany\app\App.java file.</span></span>

6. <span data-ttu-id="ccdb9-146">在此檔案中新增下列 **import** 陳述式：</span><span class="sxs-lookup"><span data-stu-id="ccdb9-146">Add the following **import** statements to the file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.service.*;
    import java.io.IOException;
    import java.net.URISyntaxException;
    ```

7. <span data-ttu-id="ccdb9-147">將下列類別層級變數新增至 **App** 類別，其中以您稍早記下的值取代 **{yourhubconnectionstring}** 和 **{yourdeviceid}**：</span><span class="sxs-lookup"><span data-stu-id="ccdb9-147">Add the following class-level variables to the **App** class, replacing **{yourhubconnectionstring}** and **{yourdeviceid}** with the values your noted earlier:</span></span>

    ```java
    private static final String connectionString = "{yourhubconnectionstring}";
    private static final String deviceId = "{yourdeviceid}";
    private static final IotHubServiceClientProtocol protocol = IotHubServiceClientProtocol.AMQPS;
    ```

8. <span data-ttu-id="ccdb9-148">以下列程式碼取代 **main** 方法。</span><span class="sxs-lookup"><span data-stu-id="ccdb9-148">Replace the **main** method with the following code.</span></span> <span data-ttu-id="ccdb9-149">此程式碼會連線至 IoT 中樞，傳送訊息給您的裝置，然後等候裝置已接收並處理訊息的通知︰</span><span class="sxs-lookup"><span data-stu-id="ccdb9-149">This code connects to your IoT hub, sends a message to your device, and then waits for an acknowledgment that the device received and processed the message:</span></span>
   
    ```java
    public static void main(String[] args) throws IOException,
        URISyntaxException, Exception {
      ServiceClient serviceClient = ServiceClient.createFromConnectionString(
        connectionString, protocol);
   
      if (serviceClient != null) {
        serviceClient.open();
        FeedbackReceiver feedbackReceiver = serviceClient
          .getFeedbackReceiver();
        if (feedbackReceiver != null) feedbackReceiver.open();
   
        Message messageToSend = new Message("Cloud to device message.");
        messageToSend.setDeliveryAcknowledgement(DeliveryAcknowledgement.Full);
   
        serviceClient.send(deviceId, messageToSend);
        System.out.println("Message sent to device");
   
        FeedbackBatch feedbackBatch = feedbackReceiver.receive(10000);
        if (feedbackBatch != null) {
          System.out.println("Message feedback received, feedback time: "
            + feedbackBatch.getEnqueuedTimeUtc().toString());
        }
   
        if (feedbackReceiver != null) feedbackReceiver.close();
        serviceClient.close();
      }
    }
    ```

    > [!NOTE]
    > <span data-ttu-id="ccdb9-150">為了簡單起見，本教學課程不會實作任何重試原則。</span><span class="sxs-lookup"><span data-stu-id="ccdb9-150">For simplicity's sake, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="ccdb9-151">在生產環境程式碼中，您應該如 MSDN 文章 [暫時性錯誤處理]所建議，實作重試原則 (例如指數型輪詢)。</span><span class="sxs-lookup"><span data-stu-id="ccdb9-151">In production code, you should implement retry policies (such as exponential backoff), as suggested in the MSDN article [Transient Fault Handling].</span></span>


9. <span data-ttu-id="ccdb9-152">若要使用 Maven 建置 **simulated-device** 應用程式，請在命令提示字元中的 simulated-device 資料夾內執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="ccdb9-152">To build the **simulated-device** app using Maven, execute the following command at the command prompt in the simulated-device folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="run-the-applications"></a><span data-ttu-id="ccdb9-153">執行應用程式</span><span class="sxs-lookup"><span data-stu-id="ccdb9-153">Run the applications</span></span>

<span data-ttu-id="ccdb9-154">現在您已經準備好執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="ccdb9-154">You are now ready to run the applications.</span></span>

1. <span data-ttu-id="ccdb9-155">在命令提示字元下，於 simulated-device 資料夾中執行下列命令，以開始將遙測傳送至 IoT 中樞，並接聽從中樞傳送的雲端到裝置訊息：</span><span class="sxs-lookup"><span data-stu-id="ccdb9-155">At a command prompt in the simulated-device folder, run the following command to begin sending telemetry to your IoT hub and to listen for cloud-to-device messages sent from your hub:</span></span>

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App" 
    ```

    ![執行模擬裝置應用程式][img-simulated-device]

2. <span data-ttu-id="ccdb9-157">在命令提示字元下，於 send-c2d-messages 資料夾中執行下列命令，以傳送雲端到裝置訊息並等候意見反應通知︰</span><span class="sxs-lookup"><span data-stu-id="ccdb9-157">At a command prompt in the send-c2d-messages folder, run the following command to send a cloud-to-device message and wait for a feedback acknowledgment:</span></span>

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
    ```

    ![執行命令以傳送雲端到裝置訊息][img-send-command]

## <a name="next-steps"></a><span data-ttu-id="ccdb9-159">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ccdb9-159">Next steps</span></span>

<span data-ttu-id="ccdb9-160">在本教學課程中，您已了解如何傳送和接收雲端到裝置的訊息。</span><span class="sxs-lookup"><span data-stu-id="ccdb9-160">In this tutorial, you learned how to send and receive cloud-to-device messages.</span></span> 

<span data-ttu-id="ccdb9-161">若要查看使用 IoT 中樞的完整端對端解決方案範例，請參閱 [Azure IoT 套件]。</span><span class="sxs-lookup"><span data-stu-id="ccdb9-161">To see examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Suite].</span></span>

<span data-ttu-id="ccdb9-162">若要深入了解如何使用 IoT 中樞開發解決方案，請參閱 [IoT 中樞開發人員指南]。</span><span class="sxs-lookup"><span data-stu-id="ccdb9-162">To learn more about developing solutions with IoT Hub, see the [IoT Hub developer guide].</span></span>

<!-- Images -->
[img-simulated-device]: media/iot-hub-java-java-c2d/receivec2d.png
[img-send-command]:  media/iot-hub-java-java-c2d/sendc2d.png
<!-- Links -->

<span data-ttu-id="ccdb9-163">[開始使用 IoT 中樞]: iot-hub-java-java-getstarted.md</span><span class="sxs-lookup"><span data-stu-id="ccdb9-163">[Get started with IoT Hub]: iot-hub-java-java-getstarted.md</span></span>
[IoT Hub developer guide - C2D]: iot-hub-devguide-messaging.md
<span data-ttu-id="ccdb9-164">[IoT 中樞開發人員指南]: iot-hub-devguide.md</span><span class="sxs-lookup"><span data-stu-id="ccdb9-164">[IoT Hub developer guide]: iot-hub-devguide.md</span></span>
<span data-ttu-id="ccdb9-165">[Azure IoT 開發人員中樞]: http://www.azure.com/develop/iot</span><span class="sxs-lookup"><span data-stu-id="ccdb9-165">[Azure IoT Developer Center]: http://www.azure.com/develop/iot</span></span>
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-java
<span data-ttu-id="ccdb9-166">[暫時性錯誤處理]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx</span><span class="sxs-lookup"><span data-stu-id="ccdb9-166">[Transient Fault Handling]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx</span></span>
<span data-ttu-id="ccdb9-167">[Azure 入口網站]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="ccdb9-167">[Azure portal]: https://portal.azure.com</span></span>
<span data-ttu-id="ccdb9-168">[Azure IoT 套件]: https://azure.microsoft.com/documentation/suites/iot-suite/</span><span class="sxs-lookup"><span data-stu-id="ccdb9-168">[Azure IoT Suite]: https://azure.microsoft.com/documentation/suites/iot-suite/</span></span>
[lnk-maven-service-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22