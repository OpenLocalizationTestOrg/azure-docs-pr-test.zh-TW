---
title: "與 Azure IoT 中樞 (Java) aaaCloud 到裝置訊息 |Microsoft 文件"
description: "如何 toosend 雲端到裝置訊息 tooa 裝置使用 hello Azure IoT Sdk for Java 的 Azure IoT 中樞。 您修改應用程式 tooreceive 模擬的裝置的雲端到裝置訊息，並修改後端應用程式 toosend hello 雲端到裝置訊息。"
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
ms.openlocfilehash: 8721f18428c849ed9a04aa2e45c65605c3e38101
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="send-cloud-to-device-messages-with-iot-hub-java"></a><span data-ttu-id="1260f-104">使用 IoT 中樞傳送雲端到裝置訊息 (Java)</span><span class="sxs-lookup"><span data-stu-id="1260f-104">Send cloud-to-device messages with IoT Hub (Java)</span></span>
[!INCLUDE [iot-hub-selector-c2d](../../includes/iot-hub-selector-c2d.md)]

<span data-ttu-id="1260f-105">Azure IoT 中樞是一項完全受管理的服務，有助於讓數百萬個裝置和一個解決方案後端進行可靠且安全的雙向通訊。</span><span class="sxs-lookup"><span data-stu-id="1260f-105">Azure IoT Hub is a fully managed service that helps enable reliable and secure bi-directional communications between millions of devices and a solution back end.</span></span> <span data-ttu-id="1260f-106">hello[開始使用 IoT 中樞]教學課程將說明如何 toocreate IoT 中樞，佈建裝置身分識別，並傳送裝置到雲端訊息的模擬的裝置應用程式的程式碼。</span><span class="sxs-lookup"><span data-stu-id="1260f-106">hello [Get started with IoT Hub] tutorial shows how toocreate an IoT hub, provision a device identity in it, and code a simulated device app that sends device-to-cloud messages.</span></span>

<span data-ttu-id="1260f-107">本教學課程是以 [開始使用 IoT 中樞]為基礎。</span><span class="sxs-lookup"><span data-stu-id="1260f-107">This tutorial builds on [Get started with IoT Hub].</span></span> <span data-ttu-id="1260f-108">這會說明如何：</span><span class="sxs-lookup"><span data-stu-id="1260f-108">It shows you how to:</span></span>

* <span data-ttu-id="1260f-109">從您的方案後端，傳送到 IoT 中樞雲端到裝置訊息 tooa 單一裝置。</span><span class="sxs-lookup"><span data-stu-id="1260f-109">From your solution back end, send cloud-to-device messages tooa single device through IoT Hub.</span></span>
* <span data-ttu-id="1260f-110">接收裝置上的雲端到裝置訊息。</span><span class="sxs-lookup"><span data-stu-id="1260f-110">Receive cloud-to-device messages on a device.</span></span>
* <span data-ttu-id="1260f-111">從您的方案後端，要求傳遞通知 (*意見反應*) 的訊息傳送 tooa 裝置從 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="1260f-111">From your solution back end, request delivery acknowledgement (*feedback*) for messages sent tooa device from IoT Hub.</span></span>

<span data-ttu-id="1260f-112">您可以找到更多有關雲端到裝置訊息在 hello [IoT 中樞開發人員指南][IoT Hub developer guide - C2D]。</span><span class="sxs-lookup"><span data-stu-id="1260f-112">You can find more information on cloud-to-device messages in hello [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>

<span data-ttu-id="1260f-113">在本教學課程的 hello 最後，您可以執行兩個 Java 主控台應用程式：</span><span class="sxs-lookup"><span data-stu-id="1260f-113">At hello end of this tutorial, you run two Java console apps:</span></span>

* <span data-ttu-id="1260f-114">**模擬裝置**，hello 應用程式中建立的修改的版本[開始使用 IoT 中樞]，這會連接 tooyour IoT 中樞，並接收雲端到裝置訊息。</span><span class="sxs-lookup"><span data-stu-id="1260f-114">**simulated-device**, a modified version of hello app created in [Get started with IoT Hub], which connects tooyour IoT hub and receives cloud-to-device messages.</span></span>
* <span data-ttu-id="1260f-115">**傳送 c2d 訊息**，其中會傳送到 IoT 中樞的雲端到裝置訊息 toohello 模擬的裝置應用程式，但收到其傳遞通知。</span><span class="sxs-lookup"><span data-stu-id="1260f-115">**send-c2d-messages**, which sends a cloud-to-device message toohello simulated device app through IoT Hub, and then receives its delivery acknowledgement.</span></span>

> [!NOTE]
> <span data-ttu-id="1260f-116">「IoT 中樞」透過 Azure IoT 裝置 SDK 為許多裝置平台和語言 (包括 C、Java 及 Javascript) 提供 SDK 支援。</span><span class="sxs-lookup"><span data-stu-id="1260f-116">IoT Hub has SDK support for many device platforms and languages (including C, Java, and Javascript) through Azure IoT device SDKs.</span></span> <span data-ttu-id="1260f-117">如需如何 tooconnect 裝置 toothis 教學課程的程式碼，以及通常 tooAzure IoT 中樞，請參閱逐步指示 hello [Azure IoT 開發人員中心]。</span><span class="sxs-lookup"><span data-stu-id="1260f-117">For step-by-step instructions on how tooconnect your device toothis tutorial's code, and generally tooAzure IoT Hub, see hello [Azure IoT Developer Center].</span></span>

<span data-ttu-id="1260f-118">toocomplete 本教學課程中，您需要遵循的 hello:</span><span class="sxs-lookup"><span data-stu-id="1260f-118">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="1260f-119">完成的工作版的 hello[開始使用 IoT 中樞](iot-hub-java-java-getstarted.md)或[程序 IoT 中樞裝置到雲端訊息](iot-hub-java-java-process-d2c.md)教學課程。</span><span class="sxs-lookup"><span data-stu-id="1260f-119">A complete working version of hello [Get started with IoT Hub](iot-hub-java-java-getstarted.md) or [Process IoT Hub device-to-cloud messages](iot-hub-java-java-process-d2c.md) tutorial.</span></span>
* <span data-ttu-id="1260f-120">最新 hello [Java SE 開發套件 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span><span class="sxs-lookup"><span data-stu-id="1260f-120">hello latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span>
* [<span data-ttu-id="1260f-121">Maven 3</span><span class="sxs-lookup"><span data-stu-id="1260f-121">Maven 3</span></span>](https://maven.apache.org/install.html)
* <span data-ttu-id="1260f-122">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="1260f-122">An active Azure account.</span></span> <span data-ttu-id="1260f-123">(如果您沒有帳戶，只需要幾分鐘的時間就可以建立[免費帳戶][lnk-free-trial]。)</span><span class="sxs-lookup"><span data-stu-id="1260f-123">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

## <a name="receive-messages-in-hello-simulated-device-app"></a><span data-ttu-id="1260f-124">在 hello 模擬的裝置應用程式中接收訊息</span><span class="sxs-lookup"><span data-stu-id="1260f-124">Receive messages in hello simulated device app</span></span>

<span data-ttu-id="1260f-125">在本節中，您將修改 hello 模擬的裝置應用程式中建立[開始使用 IoT 中樞]tooreceive 雲端到裝置訊息從 hello IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="1260f-125">In this section, you modify hello simulated device app you created in [Get started with IoT Hub] tooreceive cloud-to-device messages from hello IoT hub.</span></span>

1. <span data-ttu-id="1260f-126">使用文字編輯器開啟 hello simulated-device\src\main\java\com\mycompany\app\App.java 檔案。</span><span class="sxs-lookup"><span data-stu-id="1260f-126">Using a text editor, open hello simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span>

2. <span data-ttu-id="1260f-127">新增下列 hello **MessageCallback**類別作為巢狀類別內 hello**應用程式**類別。</span><span class="sxs-lookup"><span data-stu-id="1260f-127">Add hello following **MessageCallback** class as a nested class inside hello **App** class.</span></span> <span data-ttu-id="1260f-128">hello**執行**hello 裝置從 IoT 中心接收訊息時，會叫用方法。</span><span class="sxs-lookup"><span data-stu-id="1260f-128">hello **execute** method is invoked when hello device receives a message from IoT Hub.</span></span> <span data-ttu-id="1260f-129">在此範例中，hello 裝置一律通知 hello IoT 中心已完成 hello 訊息：</span><span class="sxs-lookup"><span data-stu-id="1260f-129">In this example, hello device always notifies hello IoT hub that it has completed hello message:</span></span>

    ```java
    private static class AppMessageCallback implements MessageCallback {
      public IotHubMessageResult execute(Message msg, Object context) {
        System.out.println("Received message from hub: "
          + new String(msg.getBytes(), Message.DEFAULT_IOTHUB_MESSAGE_CHARSET));
    
        return IotHubMessageResult.COMPLETE;
      }
    }
    ```
3. <span data-ttu-id="1260f-130">修改 hello**主要**方法 toocreate **AppMessageCallback**執行個體並呼叫 hello **setMessageCallback**方法開幕前 hello 用戶端，如下所示：</span><span class="sxs-lookup"><span data-stu-id="1260f-130">Modify hello **main** method toocreate an **AppMessageCallback** instance and call hello **setMessageCallback** method before it opens hello client as follows:</span></span>

    ```java
    client = new DeviceClient(connString, protocol);
   
    MessageCallback callback = new AppMessageCallback();
    client.setMessageCallback(callback, null);
    client.open();
    ```

    > [!NOTE]
    > <span data-ttu-id="1260f-131">如果您使用 HTTP 而不是 MQTT 或 AMQP 做 hello 傳輸，hello **DeviceClient**從 IoT 中樞不常 （每隔 25 分鐘內） 的訊息會檢查執行個體。</span><span class="sxs-lookup"><span data-stu-id="1260f-131">If you use HTTP instead of MQTT or AMQP as hello transport, hello **DeviceClient** instance checks for messages from IoT Hub infrequently (less than every 25 minutes).</span></span> <span data-ttu-id="1260f-132">如需 MQTT、 AMQP 和 HTTP 支援與 IoT 中樞節流的 hello 差異的詳細資訊，請參閱 hello [IoT 中樞開發人員指南][IoT Hub developer guide - C2D]。</span><span class="sxs-lookup"><span data-stu-id="1260f-132">For more information about hello differences between MQTT, AMQP and HTTP support, and IoT Hub throttling, see hello [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>

4. <span data-ttu-id="1260f-133">toobuild hello**模擬裝置**使用 Maven，應用程式執行下列命令在 hello hello 模擬裝置資料夾中的命令提示字元的 hello:</span><span class="sxs-lookup"><span data-stu-id="1260f-133">toobuild hello **simulated-device** app using Maven, execute hello following command at hello command prompt in hello simulated-device folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="send-a-cloud-to-device-message"></a><span data-ttu-id="1260f-134">傳送雲端到裝置訊息</span><span class="sxs-lookup"><span data-stu-id="1260f-134">Send a cloud-to-device message</span></span>

<span data-ttu-id="1260f-135">在本節中，您可以建立傳送雲端到裝置訊息 toohello 模擬的裝置應用程式的 Java 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="1260f-135">In this section, you create a Java console app that sends cloud-to-device messages toohello simulated device app.</span></span> <span data-ttu-id="1260f-136">您需要 hello hello 裝置 hello 中加入的裝置識別碼[開始使用 IoT 中樞]教學課程。</span><span class="sxs-lookup"><span data-stu-id="1260f-136">You need hello device ID of hello device you added in hello [Get started with IoT Hub] tutorial.</span></span> <span data-ttu-id="1260f-137">您也需要 hello IoT 中樞連接字串，您可以在 hello 找到中樞[Azure 入口網站]。</span><span class="sxs-lookup"><span data-stu-id="1260f-137">You also need hello IoT Hub connection string for your hub that you can find in hello [Azure portal].</span></span>

1. <span data-ttu-id="1260f-138">建立名為 Maven 專案**傳送 c2d 訊息**使用下列命令，在您的命令提示字元的 hello。</span><span class="sxs-lookup"><span data-stu-id="1260f-138">Create a Maven project called **send-c2d-messages** using hello following command at your command prompt.</span></span> <span data-ttu-id="1260f-139">注意，此命令是單一且非常長的命令：</span><span class="sxs-lookup"><span data-stu-id="1260f-139">Note this command is a single, long command:</span></span>

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=send-c2d-messages -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. <span data-ttu-id="1260f-140">在命令提示字元中，瀏覽 toohello 新的傳送 c2d 訊息資料夾。</span><span class="sxs-lookup"><span data-stu-id="1260f-140">At your command prompt, navigate toohello new send-c2d-messages folder.</span></span>

3. <span data-ttu-id="1260f-141">使用文字編輯器，開啟 hello 傳送 c2d 訊息資料夾中的 hello pom.xml 檔案並新增下列相依性 toohello hello**相依性**節點。</span><span class="sxs-lookup"><span data-stu-id="1260f-141">Using a text editor, open hello pom.xml file in hello send-c2d-messages folder and add hello following dependency toohello **dependencies** node.</span></span> <span data-ttu-id="1260f-142">加入 hello 相依性可讓您 toouse hello **iot 中樞-java-服務-用戶端**中您的應用程式 toocommunicate 與 IoT 中樞服務封裝：</span><span class="sxs-lookup"><span data-stu-id="1260f-142">Adding hello dependency enables you toouse hello **iothub-java-service-client** package in your application toocommunicate with your IoT hub service:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="1260f-143">您可以檢查 hello 最新版本的**iot 服務用戶端**使用[Maven 搜尋][lnk-maven-service-search]。</span><span class="sxs-lookup"><span data-stu-id="1260f-143">You can check for hello latest version of **iot-service-client** using [Maven search][lnk-maven-service-search].</span></span>

4. <span data-ttu-id="1260f-144">儲存並關閉 hello pom.xml 檔案。</span><span class="sxs-lookup"><span data-stu-id="1260f-144">Save and close hello pom.xml file.</span></span>

5. <span data-ttu-id="1260f-145">使用文字編輯器開啟 hello send-c2d-messages\src\main\java\com\mycompany\app\App.java 檔案。</span><span class="sxs-lookup"><span data-stu-id="1260f-145">Using a text editor, open hello send-c2d-messages\src\main\java\com\mycompany\app\App.java file.</span></span>

6. <span data-ttu-id="1260f-146">新增下列 hello**匯入**陳述式 toohello 檔案：</span><span class="sxs-lookup"><span data-stu-id="1260f-146">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.service.*;
    import java.io.IOException;
    import java.net.URISyntaxException;
    ```

7. <span data-ttu-id="1260f-147">新增下列類別層級變數 toohello hello**應用程式**類別取代**{yourhubconnectionstring}**和**{yourdeviceid}**以 hello 值您記下前面：</span><span class="sxs-lookup"><span data-stu-id="1260f-147">Add hello following class-level variables toohello **App** class, replacing **{yourhubconnectionstring}** and **{yourdeviceid}** with hello values your noted earlier:</span></span>

    ```java
    private static final String connectionString = "{yourhubconnectionstring}";
    private static final String deviceId = "{yourdeviceid}";
    private static final IotHubServiceClientProtocol protocol = IotHubServiceClientProtocol.AMQPS;
    ```

8. <span data-ttu-id="1260f-148">取代 hello**主要**以下列程式碼的 hello 的方法。</span><span class="sxs-lookup"><span data-stu-id="1260f-148">Replace hello **main** method with hello following code.</span></span> <span data-ttu-id="1260f-149">這段程式碼連接 tooyour IoT 中樞、 傳送訊息 tooyour 裝置，然後等候認可該 hello 裝置接收和處理 hello 訊息：</span><span class="sxs-lookup"><span data-stu-id="1260f-149">This code connects tooyour IoT hub, sends a message tooyour device, and then waits for an acknowledgment that hello device received and processed hello message:</span></span>
   
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
   
        Message messageToSend = new Message("Cloud toodevice message.");
        messageToSend.setDeliveryAcknowledgement(DeliveryAcknowledgement.Full);
   
        serviceClient.send(deviceId, messageToSend);
        System.out.println("Message sent toodevice");
   
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
    > <span data-ttu-id="1260f-150">為了簡單起見，本教學課程不會實作任何重試原則。</span><span class="sxs-lookup"><span data-stu-id="1260f-150">For simplicity's sake, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="1260f-151">在實際執行程式碼，您應該實作重試原則 （例如指數型輪詢），做為建議 hello MSDN 文件中[暫時性錯誤處理]。</span><span class="sxs-lookup"><span data-stu-id="1260f-151">In production code, you should implement retry policies (such as exponential backoff), as suggested in hello MSDN article [Transient Fault Handling].</span></span>


9. <span data-ttu-id="1260f-152">toobuild hello**模擬裝置**使用 Maven，應用程式執行下列命令在 hello hello 模擬裝置資料夾中的命令提示字元的 hello:</span><span class="sxs-lookup"><span data-stu-id="1260f-152">toobuild hello **simulated-device** app using Maven, execute hello following command at hello command prompt in hello simulated-device folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="run-hello-applications"></a><span data-ttu-id="1260f-153">執行 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="1260f-153">Run hello applications</span></span>

<span data-ttu-id="1260f-154">現在您已經準備就緒 toorun hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="1260f-154">You are now ready toorun hello applications.</span></span>

1. <span data-ttu-id="1260f-155">Hello 模擬裝置資料夾中的命令提示字元，執行下列命令 toobegin 傳送遙測 tooyour IoT 中樞與 toolisten 雲端到裝置訊息從您的中樞傳送的 hello:</span><span class="sxs-lookup"><span data-stu-id="1260f-155">At a command prompt in hello simulated-device folder, run hello following command toobegin sending telemetry tooyour IoT hub and toolisten for cloud-to-device messages sent from your hub:</span></span>

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App" 
    ```

    ![執行 hello 模擬的裝置應用程式][img-simulated-device]

2. <span data-ttu-id="1260f-157">Hello 傳送 c2d 訊息資料夾中的命令提示字元，執行下列命令 toosend hello 雲端到裝置訊息並等候回應通知：</span><span class="sxs-lookup"><span data-stu-id="1260f-157">At a command prompt in hello send-c2d-messages folder, run hello following command toosend a cloud-to-device message and wait for a feedback acknowledgment:</span></span>

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
    ```

    ![執行 hello 命令 toosend hello 雲端到裝置訊息][img-send-command]

## <a name="next-steps"></a><span data-ttu-id="1260f-159">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1260f-159">Next steps</span></span>

<span data-ttu-id="1260f-160">在本教學課程中，您學到如何 toosend 和接收雲端到裝置訊息。</span><span class="sxs-lookup"><span data-stu-id="1260f-160">In this tutorial, you learned how toosend and receive cloud-to-device messages.</span></span> 

<span data-ttu-id="1260f-161">完整的端對端解決方案使用 IoT 中樞 toosee 範例請參閱[Azure IoT 套件]。</span><span class="sxs-lookup"><span data-stu-id="1260f-161">toosee examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Suite].</span></span>

<span data-ttu-id="1260f-162">toolearn 進一步了解開發與 IoT 中樞的解決方案，請參閱 「 hello [IoT 中樞開發人員指南]。</span><span class="sxs-lookup"><span data-stu-id="1260f-162">toolearn more about developing solutions with IoT Hub, see hello [IoT Hub developer guide].</span></span>

<!-- Images -->
[img-simulated-device]: media/iot-hub-java-java-c2d/receivec2d.png
[img-send-command]:  media/iot-hub-java-java-c2d/sendc2d.png
<!-- Links -->

[開始使用 IoT 中樞]: iot-hub-java-java-getstarted.md
[IoT Hub developer guide - C2D]: iot-hub-devguide-messaging.md
[IoT 中樞開發人員指南]: iot-hub-devguide.md
[Azure IoT 開發人員中心]: http://www.azure.com/develop/iot
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-java
[暫時性錯誤處理]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[Azure 入口網站]: https://portal.azure.com
[Azure IoT 套件]: https://azure.microsoft.com/documentation/suites/iot-suite/
[lnk-maven-service-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22