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
# <a name="process-iot-hub-device-to-cloud-messages-java"></a>處理 IoT 中樞的裝置到雲端訊息 (Java)

[!INCLUDE [iot-hub-selector-process-d2c](../../includes/iot-hub-selector-process-d2c.md)]

Azure IoT 中樞是一項完全受管理的服務，可在數百萬個裝置和一個解決方案後端之間啟用可靠且安全的雙向通訊。 其他教學課程 ([開始使用 IoT 中樞]和[傳送雲端到裝置訊息與 IoT 中樞][lnk-c2d]) 顯示如何 toouse hello 基本裝置到雲端 」 和 「 雲端到裝置IoT 中樞的傳訊功能。

本教學課程是 hello 程式碼所示 hello[開始使用 IoT 中樞]教學課程中，並顯示 toouse 可擴充的方式郵件路由 tooprocess 裝置到雲端訊息的方式。 hello 教學課程說明如何 tooprocess 訊息需要立即採取行動 hello 方案從後端。 例如，裝置可能會傳送一則警示訊息，以觸發將票證插入 CRM 系統的作業。 相較之下，資料點訊息只會饋送至分析引擎。 例如，從 toobe 儲存供稍後分析的裝置的溫度遙測是資料點的訊息。

在本教學課程的 hello 最後，您可以執行三個 Java 主控台應用程式：

* **模擬裝置**，hello hello 中建立的應用程式的修改的版本[開始使用 IoT 中樞]教學課程中，傳送的資料點裝置到雲端訊息每秒，而互動式裝置到雲端訊息每隔 10秒數。 此應用程式使用 hello AMQP 通訊協定 toocommunicate 與 IoT 中樞。
* **閱讀 d2c 郵件**會顯示您裝置的應用程式所傳送的 hello 遙測。
* **讀取關鍵佇列**取消佇列 hello 重大訊息從 hello Service Bus 佇列附加 toohello IoT 中樞。

> [!NOTE]
> IoT 中樞對於許多裝置平台和語言 (包括 C、Java 和 JavaScript) 提供 SDK 支援。 如需如何 tooreplace hello 本教學課程中使用實體裝置，裝置的指示和如何 tooconnect 裝置 tooan IoT 中樞，請參閱 hello [Azure IoT 開發人員中心]。

toocomplete 本教學課程中，您需要遵循的 hello:

* 完成的工作版的 hello[開始使用 IoT 中樞]教學課程。
* 最新 hello [Java SE 開發套件 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
* [Maven 3](https://maven.apache.org/install.html)
* 使用中的 Azure 帳戶。 (如果您沒有帳戶，只需要幾分鐘的時間就可以建立 [免費帳戶][lnk-free-trial])。

您應具備 [Azure 儲存體]和 [Azure 服務匯流排]的基本知識。

## <a name="send-interactive-messages-from-a-device-app"></a>從裝置應用程式傳送互動式訊息
在本節中，您將修改 hello 裝置應用程式，您可以在 hello[開始使用 IoT 中樞]教學課程 toooccasionally 傳送需要立即處理的訊息。

1. 使用文字編輯器 tooopen hello simulated-device\src\main\java\com\mycompany\app\App.java 檔案。 這個檔案包含 hello hello 碼**模擬裝置**hello 中建立的應用程式[開始使用 IoT 中樞]教學課程。

2. 取代 hello **MessageSender**類別以下列程式碼的 hello:

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
   
    此方法會隨機將 hello 屬性`"level": "critical"`toomessages 傳送 hello 裝置，這將模擬 hello 應用程式後端時，需要立即採取行動的訊息。 hello 應用程式將此資訊傳遞在 hello 訊息內容中，而不是在 hello 訊息主體中，因此該 IoT 中樞可以路由傳送 hello 訊息 toohello 適當訊息目的地。
   
   > [!NOTE]
   > 您可以使用訊息內容 tooroute 訊息各種案例，包括冷路徑的處理，此外 toohello 最忙碌路徑範例所示。

2. 儲存並關閉 hello simulated-device\src\main\java\com\mycompany\app\App.java 檔案。

    > [!NOTE]
    > 為了簡化的 hello 起見，本教學課程未實作任何重試原則。 在實際執行程式碼，您應該實作重試原則，例如 hello MSDN 文章中建議的指數型撤退[暫時性錯誤處理]。

3. toobuild hello**模擬裝置**使用 Maven，應用程式執行下列命令在 hello hello 模擬裝置資料夾中的命令提示字元的 hello:

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="add-a-queue-tooyour-iot-hub-and-route-messages-tooit"></a>新增佇列 tooyour IoT 中樞與路由訊息 tooit

在本節中，您可以建立服務匯流排佇列、 tooyour IoT 中樞時，將它連接並設定 IoT 中樞 toosend 訊息 toohello 佇列根據 hello hello 訊息上的屬性存在。 如需如何 tooprocess 訊息從服務匯流排佇列的詳細資訊，請參閱[開始使用佇列][lnk-sb-queues-java]。

1. 如[開始使用佇列][lnk-sb-queues-java]所述，建立服務匯流排佇列。 記下 hello 命名空間和佇列名稱。

2. 在 hello Azure 入口網站，開啟您的 IoT 中樞，然後按一下**端點**。

    ![IoT 中樞端點][30]

3. 在 hello**端點**刀鋒視窗中，按一下 **新增**在 hello 頂端 tooadd 佇列 tooyour IoT 中樞。 名稱 hello 端點**CriticalQueue**並用 hello 下拉式清單 tooselect **Service Bus 佇列**、 hello 佇列所在的服務匯流排命名空間和 hello 您的佇列名稱。 當您完成之後時，按一下 **儲存**hello 底部。

    ![新增端點][31]

4. 現在按一下 IoT 中樞中的 [路由]。 按一下**新增**頂端 hello hello 刀鋒視窗 toocreate 加入路由傳送訊息 toohello 佇列只路由規則。 選取**DeviceTelemetry** hello 的資料來源。 輸入`level="critical"`做為 hello 條件，然後選擇您剛才加入做為自訂的端點，如 hello 路由規則端點 hello 佇列。 當您完成之後時，按一下 **儲存**hello 底部。

    ![新增路由][32]

    請確定 hello 後援路由設定得**ON**。 IoT 中樞 hello 預設設定此設定。

    ![後援路由][33]

## <a name="optional-read-from-hello-queue-endpoint"></a>（選擇性）讀取 hello 佇列端點

您可以選擇性地讀取 hello 訊息 hello 佇列端點中的 hello 指示[開始使用佇列][lnk-sb-queues-java]。 名稱 hello 應用程式**讀取關鍵佇列**。

## <a name="run-hello-applications"></a>執行 hello 應用程式

現在您已準備好 toorun hello 三個應用程式。

1. toorun hello**閱讀 d2c 郵件**應用程式，在命令提示字元或殼層巡覽 toohello 讀取 d2c 資料夾，並執行下列命令的 hello:

   ```cmd/sh
   mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
   ```

   ![執行 read-d2c-messages][readd2c]

2. toorun hello**讀取關鍵佇列**應用程式，在命令提示字元或殼層巡覽 toohello 讀取關鍵佇列資料夾，並執行下列命令的 hello:

   ```cmd/sh
   mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
   ```
   
   ![執行 read-critical-messages][readqueue]

3. toorun hello**模擬裝置**應用程式中的，在命令提示字元或殼層巡覽 toohello 模擬裝置資料夾，並執行下列命令的 hello:

   ```cmd/sh
   mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
   ```
   
   ![執行 simulated-device][simulateddevice]

## <a name="next-steps"></a>後續步驟

在本教學課程中，您學會如何 tooreliably 裝置到雲端訊息分派使用 IoT 中樞的 hello 訊息路由功能。

hello [toosend 雲端到裝置與 IoT 中樞的訊息][ lnk-c2d]顯示 toosend 訊息從您的方案後端 tooyour 裝置的方式。

完整的端對端解決方案使用 IoT 中樞 toosee 範例請參閱[Azure IoT 套件][lnk-suite]。

toolearn 進一步了解開發與 IoT 中樞的解決方案，請參閱 「 hello [IoT 中樞開發人員指南]。

請參閱詳細訊息路由在 IoT 中樞 toolearn[傳送和接收訊息與 IoT 中樞][lnk-devguide-messaging]。

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
