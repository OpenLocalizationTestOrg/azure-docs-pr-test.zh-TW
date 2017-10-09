---
title: "從裝置 tooAzure IoT 中樞與 Java aaaUpload 檔案 |Microsoft 文件"
description: "如何從使用 Azure IoT 裝置 SDK for Java 裝置 toohello 雲端檔案 tooupload。 上傳的檔案會儲存在 Azure 儲存體 blob 容器中。"
services: iot-hub
documentationcenter: java
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 4759d229-f856-4526-abda-414f8b00a56d
ms.service: iot-hub
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2017
ms.author: dobett
ms.openlocfilehash: e305fe61bf7ca0aeb2c092bc2c7efebdc78d4f68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-from-your-device-toohello-cloud-with-iot-hub"></a>從裝置與 IoT 中樞 toohello 雲端上傳檔案

[!INCLUDE [iot-hub-file-upload-language-selector](../../includes/iot-hub-file-upload-language-selector.md)]

本教學課程是 hello 程式碼在 hello[傳送雲端到裝置訊息與 IoT 中樞](iot-hub-java-java-c2d.md)教學課程 tooshow 您如何 toouse hello[檔案上傳功能的 IoT 中樞](iot-hub-devguide-file-upload.md)tooupload 檔案太[Azure blob 儲存體](../storage/index.md)。 hello 教學課程會示範如何以：

- 安全地將 Azure Blob URI 提供給裝置，以便上傳檔案。
- 使用 hello IoT 中樞檔案上傳通知 tootrigger 處理您的應用程式後端中的 hello 檔案。

hello[開始使用 IoT 中樞](iot-hub-java-java-getstarted.md)和[傳送雲端到裝置訊息與 IoT 中樞](iot-hub-java-java-c2d.md)教學課程示範 hello 基本裝置到雲端 」 和 「 雲端到裝置訊息功能的 IoT 中樞。 hello[程序裝置到雲端訊息](iot-hub-java-java-process-d2c.md)教學課程描述方式 tooreliably 將裝置到雲端訊息儲存在 Azure blob 儲存體。 不過，在某些情況下您無法輕鬆地 hello 資料對應您的裝置傳送到 hello 相對較小裝置到雲端 IoT 中樞所接受訊息。 例如：

* 包含映像的大型檔案
* 影片
* 取樣高頻率的震動資料
* 某種經前置處理過的資料。

這些檔案通常是使用類似的 hello 雲端中處理的批次[Azure Data Factory](../data-factory/index.md)或 hello [Hadoop](../hdinsight/index.md)堆疊。 當您需要從裝置 tooupland 檔案時，您仍然可以使用 hello 安全性和可靠性的 IoT 中樞。

在本教學課程中的 hello 結尾，您會執行兩個 Java 主控台應用程式：

* **模擬裝置**，hello hello [傳送雲端到裝置訊息與 IoT 中樞] 教學課程中建立的應用程式的修改的版本。 此應用程式上傳檔案 toostorage 使用提供的 IoT 中樞的 SAS URI。
* **read-file-upload-notification**，它會接收來自 IoT 中樞的檔案上傳通知。

> [!NOTE]
> IoT 中樞透過 Azure IoT 裝置 SDK 來支援許多裝置平台和語言 (包括 C、.NET 及 Javascript)。 請參閱 toohello [Azure IoT 開發人員中心]的逐步指示 tooconnect 您裝置 tooAzure IoT 中樞。

toocomplete 本教學課程中，您需要遵循的 hello:

* 最新 hello [Java SE 開發套件 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
* [Maven 3](https://maven.apache.org/install.html)
* 使用中的 Azure 帳戶。 (如果您沒有帳戶，只需要幾分鐘的時間就可以建立[免費帳戶](http://azure.microsoft.com/pricing/free-trial/)。)

[!INCLUDE [iot-hub-associate-storage](../../includes/iot-hub-associate-storage.md)]

## <a name="upload-a-file-from-a-device-app"></a>從裝置應用程式上傳檔案

在本節中，您將修改 hello 裝置應用程式中建立[傳送雲端到裝置訊息與 IoT 中樞](iot-hub-java-java-c2d.md)tooupload 檔案 tooIoT 中樞。

1. 複製映像檔案 toohello`simulated-device`資料夾並將它重新命名`myimage.png`。

1. 使用文字編輯器開啟 hello`simulated-device\src\main\java\com\mycompany\app\App.java`檔案。

1. 新增 hello 變數宣告 toohello**應用程式**類別：

    ```java
    private static String fileName = "myimage.png";
    ```

1. tooprocess 檔案上傳狀態回呼訊息時，請將 hello 面一行加入巢狀類別 toohello**應用程式**類別：

    ```java
    // Define a callback method tooprint status codes from IoT Hub.
    protected static class FileUploadStatusCallBack implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded toofile upload for " + fileName
            + " operation with status " + status.name());
      }
    }
    ```

1. tooupload 映像 tooIoT 中樞內，加入下列方法 toohello hello**應用程式**類別 tooupload 映像 tooIoT 中樞：

    ```java
    // Use IoT Hub tooupload a file asynchronously tooAzure blob storage.
    private static void uploadFile(String fullFileName) throws FileNotFoundException, IOException
    {
      File file = new File(fullFileName);
      InputStream inputStream = new FileInputStream(file);
      long streamLength = file.length();

      client.uploadToBlobAsync(fileName, inputStream, streamLength, new FileUploadStatusCallBack(), null);
    }
    ```

1. 修改 hello**主要**方法 toocall hello **uploadFile**方法 hello 下列程式碼片段所示：

    ```java
    client.open();

    try
    {
      // Get hello filename and start hello upload.
      String fullFileName = System.getProperty("user.dir") + File.separator + fileName;
      uploadFile(fullFileName);
      System.out.println("File upload started with success");
    }
    catch (Exception e)
    {
      System.out.println("Exception uploading file: " + e.getCause() + " \nERROR: " + e.getMessage());
    }

    MessageSender sender = new MessageSender();
    ```

1. 使用 hello 下列命令 toobuild hello**模擬裝置**應用程式並檢查是否發生錯誤：

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="receive-a-file-upload-notification"></a>接收檔案上傳通知

在本節中，您要建立一個 Java 主控台應用程式，接收來自 IoT 中樞的檔案上傳通知訊息。

您需要 hello **iothubowner**本節 IoT 中樞 toocomplete 連接字串。 您可以找到 hello 連接字串 hello [Azure 入口網站](https://portal.azure.com/)上 hello**共用存取原則**刀鋒視窗。

1. 建立名為 Maven 專案**讀取檔案-上傳通知**使用下列命令，在您的命令提示字元的 hello。 注意，此命令是單一且非常長的命令：

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=read-file-upload-notification -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

1. 在命令提示字元中，瀏覽新 toohello`read-file-upload-notification`資料夾。

1. 使用文字編輯器開啟 hello`pom.xml`檔案在 hello`read-file-upload-notification`資料夾並加入下列相依性 toohello hello**相依性**節點。 加入 hello 相依性可讓您 toouse hello **iot 中樞-java-服務-用戶端**中您的應用程式 toocommunicate 與 IoT 中樞服務封裝：

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
    </dependency>
    ```

    > [!NOTE]
    > 您可以檢查 hello 最新版本的**iot 服務用戶端**使用[Maven 搜尋](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22)。

1. 儲存並關閉 hello`pom.xml`檔案。

1. 使用文字編輯器開啟 hello`read-file-upload-notification\src\main\java\com\mycompany\app\App.java`檔案。

1. 新增下列 hello**匯入**陳述式 toohello 檔案：

    ```java
    import com.microsoft.azure.sdk.iot.service.*;
    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.util.concurrent.ExecutorService;
    import java.util.concurrent.Executors;
    ```

1. 新增下列類別層級變數 toohello hello**應用程式**類別：

    ```java
    private static final String connectionString = "{Your IoT Hub connection string}";
    private static final IotHubServiceClientProtocol protocol = IotHubServiceClientProtocol.AMQPS;
    private static FileUploadNotificationReceiver fileUploadNotificationReceiver = null;
    ```

1. tooprint hello 檔案上傳 toohello 主控台中，資訊將 hello 面一行加入巢狀類別 toohello**應用程式**類別：

    ```java
    // Create a thread tooreceive file upload notifications.
    private static class ShowFileUploadNotifications implements Runnable {
      public void run() {
        try {
          while (true) {
            System.out.println("Recieve file upload notifications...");
            FileUploadNotification fileUploadNotification = fileUploadNotificationReceiver.receive();
            if (fileUploadNotification != null) {
              System.out.println("File Upload notification received");
              System.out.println("Device Id : " + fileUploadNotification.getDeviceId());
              System.out.println("Blob Uri: " + fileUploadNotification.getBlobUri());
              System.out.println("Blob Name: " + fileUploadNotification.getBlobName());
              System.out.println("Last Updated : " + fileUploadNotification.getLastUpdatedTimeDate());
              System.out.println("Blob Size (Bytes): " + fileUploadNotification.getBlobSizeInBytes());
              System.out.println("Enqueued Time: " + fileUploadNotification.getEnqueuedTimeUtcDate());
            }
          }
        } catch (Exception ex) {
          System.out.println("Exception reading reported properties: " + ex.getMessage());
        }
      }
    }
    ```

1. toostart hello 執行緒接聽檔案上傳通知，加入下列程式碼 toohello hello**主要**方法：

    ```java
    public static void main(String[] args) throws IOException, URISyntaxException, Exception {
      ServiceClient serviceClient = ServiceClient.createFromConnectionString(connectionString, protocol);

      if (serviceClient != null) {
        serviceClient.open();

        // Get a file upload notification receiver from hello ServiceClient.
        fileUploadNotificationReceiver = serviceClient.getFileUploadNotificationReceiver();
        fileUploadNotificationReceiver.open();

        // Start hello thread tooreceive file upload notifications.
        ShowFileUploadNotifications showFileUploadNotifications = new ShowFileUploadNotifications();
        ExecutorService executor = Executors.newFixedThreadPool(1);
        executor.execute(showFileUploadNotifications);

        System.out.println("Press ENTER tooexit.");
        System.in.read();
        executor.shutdownNow();
        System.out.println("Shutting down sample...");
        fileUploadNotificationReceiver.close();
        serviceClient.close();
      }
    }
    ```

1. 儲存並關閉 hello`read-file-upload-notification\src\main\java\com\mycompany\app\App.java`檔案。

1. 使用 hello 下列命令 toobuild hello**讀取檔案-上傳通知**應用程式並檢查是否發生錯誤：

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="run-hello-applications"></a>執行 hello 應用程式

現在您已準備好 toorun hello 應用程式。

在命令提示字元中 hello`read-file-upload-notification`資料夾中，執行下列命令的 hello:

```cmd/sh
mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
```

在命令提示字元中 hello`simulated-device`資料夾中，執行下列命令的 hello:

```cmd/sh
mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
```

hello 下列螢幕擷取畫面顯示 hello 輸出 hello**模擬裝置**應用程式：

![simulated-device 應用程式的輸出](media/iot-hub-java-java-upload/simulated-device.png)

hello 下列螢幕擷取畫面顯示 hello 輸出 hello**讀取檔案-上傳通知**應用程式：

![read-file-upload-notification 應用程式的輸出](media/iot-hub-java-java-upload/read-file-upload-notification.png)

您可以使用您設定的 hello 儲存體容器中的 hello 入口 tooview hello 上傳檔案：

![上傳的檔案](media/iot-hub-java-java-upload/uploaded-file.png)

## <a name="next-steps"></a>後續步驟

在此教學課程中，您學會如何 toouse hello 檔案上傳的 IoT 中樞 toosimplify file uploads 從裝置的功能。 您可以繼續 tooexplore IoT 中樞功能和案例以下列發行項的 hello:

* [以程式設計方式建立 IoT 中樞][lnk-create-hub]
* [簡介 tooC SDK][lnk-c-sdk]
* [Azure IoT SDK][lnk-sdks]

toofurther 瀏覽的 IoT 中樞的 hello 功能，請參閱：

* [使用 IoT Edge 來模擬裝置][lnk-iotedge]

<!-- Images. -->

[50]: ./media/iot-hub-csharp-csharp-file-upload/run-apps1.png
[1]: ./media/iot-hub-csharp-csharp-file-upload/image-properties.png
[2]: ./media/iot-hub-csharp-csharp-file-upload/file-upload-project-csharp1.png
[3]: ./media/iot-hub-csharp-csharp-file-upload/enable-file-notifications.png

<!-- Links -->



[Azure IoT 開發人員中心]: http://www.azure.com/develop/iot

[Transient Fault Handling]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[Azure Storage]:../storage/common/storage-create-storage-account.md#create-a-storage-account
[lnk-configure-upload]: iot-hub-configure-file-upload.md
[Azure IoT service SDK NuGet package]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[lnk-create-hub]: iot-hub-rm-template-powershell.md
[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-windows-iot-edge-simulated-device.md


