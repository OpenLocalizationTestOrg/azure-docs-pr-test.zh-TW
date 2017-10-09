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
# <a name="send-cloud-to-device-messages-with-iot-hub-java"></a>使用 IoT 中樞傳送雲端到裝置訊息 (Java)
[!INCLUDE [iot-hub-selector-c2d](../../includes/iot-hub-selector-c2d.md)]

Azure IoT 中樞是一項完全受管理的服務，有助於讓數百萬個裝置和一個解決方案後端進行可靠且安全的雙向通訊。 hello[開始使用 IoT 中樞]教學課程將說明如何 toocreate IoT 中樞，佈建裝置身分識別，並傳送裝置到雲端訊息的模擬的裝置應用程式的程式碼。

本教學課程是以 [開始使用 IoT 中樞]為基礎。 這會說明如何：

* 從您的方案後端，傳送到 IoT 中樞雲端到裝置訊息 tooa 單一裝置。
* 接收裝置上的雲端到裝置訊息。
* 從您的方案後端，要求傳遞通知 (*意見反應*) 的訊息傳送 tooa 裝置從 IoT 中樞。

您可以找到更多有關雲端到裝置訊息在 hello [IoT 中樞開發人員指南][IoT Hub developer guide - C2D]。

在本教學課程的 hello 最後，您可以執行兩個 Java 主控台應用程式：

* **模擬裝置**，hello 應用程式中建立的修改的版本[開始使用 IoT 中樞]，這會連接 tooyour IoT 中樞，並接收雲端到裝置訊息。
* **傳送 c2d 訊息**，其中會傳送到 IoT 中樞的雲端到裝置訊息 toohello 模擬的裝置應用程式，但收到其傳遞通知。

> [!NOTE]
> 「IoT 中樞」透過 Azure IoT 裝置 SDK 為許多裝置平台和語言 (包括 C、Java 及 Javascript) 提供 SDK 支援。 如需如何 tooconnect 裝置 toothis 教學課程的程式碼，以及通常 tooAzure IoT 中樞，請參閱逐步指示 hello [Azure IoT 開發人員中心]。

toocomplete 本教學課程中，您需要遵循的 hello:

* 完成的工作版的 hello[開始使用 IoT 中樞](iot-hub-java-java-getstarted.md)或[程序 IoT 中樞裝置到雲端訊息](iot-hub-java-java-process-d2c.md)教學課程。
* 最新 hello [Java SE 開發套件 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
* [Maven 3](https://maven.apache.org/install.html)
* 使用中的 Azure 帳戶。 (如果您沒有帳戶，只需要幾分鐘的時間就可以建立[免費帳戶][lnk-free-trial]。)

## <a name="receive-messages-in-hello-simulated-device-app"></a>在 hello 模擬的裝置應用程式中接收訊息

在本節中，您將修改 hello 模擬的裝置應用程式中建立[開始使用 IoT 中樞]tooreceive 雲端到裝置訊息從 hello IoT 中樞。

1. 使用文字編輯器開啟 hello simulated-device\src\main\java\com\mycompany\app\App.java 檔案。

2. 新增下列 hello **MessageCallback**類別作為巢狀類別內 hello**應用程式**類別。 hello**執行**hello 裝置從 IoT 中心接收訊息時，會叫用方法。 在此範例中，hello 裝置一律通知 hello IoT 中心已完成 hello 訊息：

    ```java
    private static class AppMessageCallback implements MessageCallback {
      public IotHubMessageResult execute(Message msg, Object context) {
        System.out.println("Received message from hub: "
          + new String(msg.getBytes(), Message.DEFAULT_IOTHUB_MESSAGE_CHARSET));
    
        return IotHubMessageResult.COMPLETE;
      }
    }
    ```
3. 修改 hello**主要**方法 toocreate **AppMessageCallback**執行個體並呼叫 hello **setMessageCallback**方法開幕前 hello 用戶端，如下所示：

    ```java
    client = new DeviceClient(connString, protocol);
   
    MessageCallback callback = new AppMessageCallback();
    client.setMessageCallback(callback, null);
    client.open();
    ```

    > [!NOTE]
    > 如果您使用 HTTP 而不是 MQTT 或 AMQP 做 hello 傳輸，hello **DeviceClient**從 IoT 中樞不常 （每隔 25 分鐘內） 的訊息會檢查執行個體。 如需 MQTT、 AMQP 和 HTTP 支援與 IoT 中樞節流的 hello 差異的詳細資訊，請參閱 hello [IoT 中樞開發人員指南][IoT Hub developer guide - C2D]。

4. toobuild hello**模擬裝置**使用 Maven，應用程式執行下列命令在 hello hello 模擬裝置資料夾中的命令提示字元的 hello:

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="send-a-cloud-to-device-message"></a>傳送雲端到裝置訊息

在本節中，您可以建立傳送雲端到裝置訊息 toohello 模擬的裝置應用程式的 Java 主控台應用程式。 您需要 hello hello 裝置 hello 中加入的裝置識別碼[開始使用 IoT 中樞]教學課程。 您也需要 hello IoT 中樞連接字串，您可以在 hello 找到中樞[Azure 入口網站]。

1. 建立名為 Maven 專案**傳送 c2d 訊息**使用下列命令，在您的命令提示字元的 hello。 注意，此命令是單一且非常長的命令：

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=send-c2d-messages -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. 在命令提示字元中，瀏覽 toohello 新的傳送 c2d 訊息資料夾。

3. 使用文字編輯器，開啟 hello 傳送 c2d 訊息資料夾中的 hello pom.xml 檔案並新增下列相依性 toohello hello**相依性**節點。 加入 hello 相依性可讓您 toouse hello **iot 中樞-java-服務-用戶端**中您的應用程式 toocommunicate 與 IoT 中樞服務封裝：

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
    </dependency>
    ```

    > [!NOTE]
    > 您可以檢查 hello 最新版本的**iot 服務用戶端**使用[Maven 搜尋][lnk-maven-service-search]。

4. 儲存並關閉 hello pom.xml 檔案。

5. 使用文字編輯器開啟 hello send-c2d-messages\src\main\java\com\mycompany\app\App.java 檔案。

6. 新增下列 hello**匯入**陳述式 toohello 檔案：

    ```java
    import com.microsoft.azure.sdk.iot.service.*;
    import java.io.IOException;
    import java.net.URISyntaxException;
    ```

7. 新增下列類別層級變數 toohello hello**應用程式**類別取代**{yourhubconnectionstring}**和**{yourdeviceid}**以 hello 值您記下前面：

    ```java
    private static final String connectionString = "{yourhubconnectionstring}";
    private static final String deviceId = "{yourdeviceid}";
    private static final IotHubServiceClientProtocol protocol = IotHubServiceClientProtocol.AMQPS;
    ```

8. 取代 hello**主要**以下列程式碼的 hello 的方法。 這段程式碼連接 tooyour IoT 中樞、 傳送訊息 tooyour 裝置，然後等候認可該 hello 裝置接收和處理 hello 訊息：
   
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
    > 為了簡單起見，本教學課程不會實作任何重試原則。 在實際執行程式碼，您應該實作重試原則 （例如指數型輪詢），做為建議 hello MSDN 文件中[暫時性錯誤處理]。


9. toobuild hello**模擬裝置**使用 Maven，應用程式執行下列命令在 hello hello 模擬裝置資料夾中的命令提示字元的 hello:

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="run-hello-applications"></a>執行 hello 應用程式

現在您已經準備就緒 toorun hello 應用程式。

1. Hello 模擬裝置資料夾中的命令提示字元，執行下列命令 toobegin 傳送遙測 tooyour IoT 中樞與 toolisten 雲端到裝置訊息從您的中樞傳送的 hello:

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App" 
    ```

    ![執行 hello 模擬的裝置應用程式][img-simulated-device]

2. Hello 傳送 c2d 訊息資料夾中的命令提示字元，執行下列命令 toosend hello 雲端到裝置訊息並等候回應通知：

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
    ```

    ![執行 hello 命令 toosend hello 雲端到裝置訊息][img-send-command]

## <a name="next-steps"></a>後續步驟

在本教學課程中，您學到如何 toosend 和接收雲端到裝置訊息。 

完整的端對端解決方案使用 IoT 中樞 toosee 範例請參閱[Azure IoT 套件]。

toolearn 進一步了解開發與 IoT 中樞的解決方案，請參閱 「 hello [IoT 中樞開發人員指南]。

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