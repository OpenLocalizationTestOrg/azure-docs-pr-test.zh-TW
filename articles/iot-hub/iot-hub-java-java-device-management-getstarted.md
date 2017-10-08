---
title: "aaaGet 開始使用 Azure IoT 中心裝置管理 (Java) |Microsoft 文件"
description: "如何 toouse Azure IoT 中心裝置管理 tooinitiate 遠端裝置重新開機。 您可以使用 hello Azure IoT 裝置 SDK for Java tooimplement 模擬的裝置應用程式，其中包含直接的方法和 hello Java tooimplement hello 直接的方法會叫用的服務應用程式的 Azure IoT 服務 SDK。"
services: iot-hub
documentationcenter: .java
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 7aaeda9d4ff7002e5c66adfd61e2dfd5bcea964f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-management-java"></a>開始使用裝置管理 (Java)

[!INCLUDE [iot-hub-selector-dm-getstarted](../../includes/iot-hub-selector-dm-getstarted.md)]

本教學課程說明如何：

* 使用 hello Azure 入口網站 toocreate IoT 中樞，並在您的 IoT 中樞中建立裝置身分識別。
* 建立實作直接方法 tooreboot hello 裝置模擬的裝置應用程式。 直接的方法會叫用從 hello 雲端。
* 建立會叫用 hello 重新開機直接方法 hello 模擬的裝置的應用程式透過您的 IoT 中樞中的應用程式。 此應用程式然後 hello 報告的屬性，與 hello 裝置 toosee hello 重新開機作業完成時的監視。

在本教學課程的 hello 最後，您有兩個 Java 主控台應用程式：

**simulated-device**。 此應用程式會：

* 使用先前建立的 hello 裝置身分識別連接 tooyour IoT 中樞。
* 收到 reboot 直接方法呼叫。
* 模擬實體重新開機。
* 報表 hello hello 透過報告屬性上次重新開機的時間。

**trigger-reboot**。 此應用程式會：

* 會呼叫 hello 模擬的裝置應用程式中直接的方法。
* 顯示 hello 模擬的裝置所傳送的 hello 回應 toohello 直接方法呼叫
* 顯示 hello 更新所報告的屬性。

> [!NOTE]
> 如需您可以在裝置和您的方案後端上使用 toobuild 應用程式 toorun 的 hello Sdk 資訊，請參閱[Azure IoT Sdk][lnk-hub-sdks]。

toocomplete 本教學課程中，您需要：

* Java SE 8。 <br/> [準備開發環境][ lnk-dev-setup]描述如何 tooinstall Java 本教學課程中的 Windows 或 Linux。
* Maven 3。  <br/> [準備開發環境][ lnk-dev-setup]描述如何 tooinstall [Maven] [ lnk-maven]本教學課程中的 Windows 或 Linux。
* [Node.js 版本 0.10.0 或更新版本](http://nodejs.org)。

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-reboot-on-hello-device-using-a-direct-method"></a>觸發程序使用直接的方法 hello 裝置上遠端重新開機

在本節中，您將建立 Java 主控台應用程式以：

1. Hello hello 模擬的裝置應用程式中重新開機直接方法會叫用。
1. 會顯示 hello 回應。
1. 輪詢 hello 報告 hello 重新開機完成後，從 hello 裝置 toodetermine 傳送的屬性。

此主控台應用程式連接 tooyour IoT 中樞 tooinvoke hello 直接方法，並讀取的 hello 報告內容。

1. 建立稱為 dm-get-started 的空資料夾。

1. 在 hello dm get 啟動資料夾中，建立名為 Maven 專案**觸發程序重新開機**使用下列命令，在您的命令提示字元的 hello。 hello 下列範例示範單一、 完整的命令：

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=trigger-reboot -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. 在命令提示字元中，瀏覽 toohello 觸發程序重新開機資料夾。

1. 使用文字編輯器，開啟 hello 觸發程序重新啟動資料夾中的 hello pom.xml 檔案並新增下列相依性 toohello hello**相依性**節點。 此相依性可讓您 toouse hello iot 服務用戶端封裝您的應用程式 toocommunicate 與 IoT 中樞中：

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
      <type>jar</type>
    </dependency>
    ```

    > [!NOTE]
    > 您可以檢查 hello 最新版本的**iot 服務用戶端**使用[Maven 搜尋][lnk-maven-service-search]。

1. 新增下列 hello**建置**節點之後 hello**相依性**節點。 此設定會指示 Maven toouse Java 1.8 toobuild hello 應用程式：

    ```xml
    <build>
      <plugins>
        <plugin>
          <groupId>org.apache.maven.plugins</groupId>
          <artifactId>maven-compiler-plugin</artifactId>
          <version>3.3</version>
          <configuration>
            <source>1.8</source>
            <target>1.8</target>
          </configuration>
        </plugin>
      </plugins>
    </build>
    ```

1. 儲存並關閉 hello pom.xml 檔案。

1. 使用文字編輯器開啟 hello trigger-reboot\src\main\java\com\mycompany\app\App.java 原始程式檔。

1. 新增下列 hello**匯入**陳述式 toohello 檔案：

    ```java
    import com.microsoft.azure.sdk.iot.service.devicetwin.DeviceMethod;
    import com.microsoft.azure.sdk.iot.service.devicetwin.MethodResult;
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;
    import com.microsoft.azure.sdk.iot.service.devicetwin.DeviceTwin;
    import com.microsoft.azure.sdk.iot.service.devicetwin.DeviceTwinDevice;

    import java.io.IOException;
    import java.util.concurrent.TimeUnit;
    import java.util.concurrent.Executors;
    import java.util.concurrent.ExecutorService;
    ```

1. 新增下列類別層級變數 toohello hello**應用程式**類別。 取代`{youriothubconnectionstring}`與您在 hello 記下您的 IoT 中樞連接字串*建立 IoT 中樞*> 一節：

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    private static final String methodName = "reboot";
    private static final Long responseTimeout = TimeUnit.SECONDS.toSeconds(30);
    private static final Long connectTimeout = TimeUnit.SECONDS.toSeconds(5);
    ```

1. tooimplement 讀取 hello 執行緒報告屬性從 hello 裝置兩個每隔 10 秒鐘，加入下列 hello 巢狀類別 toohello**應用程式**類別：

    ```java
    private static class ShowReportedProperties implements Runnable {
      public void run() {
        try {
          DeviceTwin deviceTwins = DeviceTwin.createFromConnectionString(iotHubConnectionString);
          DeviceTwinDevice twinDevice = new DeviceTwinDevice(deviceId);
          while (true) {
            System.out.println("Get reported properties from device twin");
            deviceTwins.getTwin(twinDevice);
            System.out.println(twinDevice.reportedPropertiesToString());
            Thread.sleep(10000);
          }
        } catch (Exception ex) {
          System.out.println("Exception reading reported properties: " + ex.getMessage());
        }
      }
    }
    ```

1. hello 模擬的裝置上的 tooinvoke hello 重新開機直接方法中加入下列程式碼 toohello hello**主要**方法：

    ```java
    System.out.println("Starting sample...");
    DeviceMethod methodClient = DeviceMethod.createFromConnectionString(iotHubConnectionString);

    try
    {
      System.out.println("Invoke reboot direct method");
      MethodResult result = methodClient.invoke(deviceId, methodName, responseTimeout, connectTimeout, null);

      if(result == null)
      {
        throw new IOException("Invoke direct method reboot returns null");
      }
      System.out.println("Invoked reboot on device");
      System.out.println("Status for device:   " + result.getStatus());
      System.out.println("Message from device: " + result.getPayload());
    }
    catch (IotHubException e)
    {
        System.out.println(e.getMessage());
    }
    ```

1. toostart hello 執行緒 toopoll hello hello 模擬裝置的報告的屬性，加入下列程式碼 toohello hello**主要**方法：

    ```java
    ShowReportedProperties showReportedProperties = new ShowReportedProperties();
    ExecutorService executor = Executors.newFixedThreadPool(1);
    executor.execute(showReportedProperties);
    ```

1. tooenable 您 toostop hello 應用程式，加入下列程式碼 toohello hello**主要**方法：

    ```java
    System.out.println("Press ENTER tooexit.");
    System.in.read();
    executor.shutdownNow();
    System.out.println("Shutting down sample...");
    ```

1. 儲存並關閉 hello trigger-reboot\src\main\java\com\mycompany\app\App.java 檔案。

1. 建置 hello**觸發程序重新開機**後端應用程式，並更正任何錯誤。 在命令提示字元中，瀏覽 toohello 觸發程序重新開機資料夾，然後執行下列命令的 hello:

    `mvn clean package -DskipTests`

## <a name="create-a-simulated-device-app"></a>建立模擬裝置應用程式

在本節中，您將建立模擬裝置的 Java 主控台應用程式。 hello 應用程式會接聽 hello 重新開機直接方法呼叫從 IoT 中樞，並立即回應 toothat 呼叫。 應用程式，然後一段時間的睡眠 hello toosimulate hello 重新開機處理程序之前它會使用報告的屬性 toonotify hello**觸發程序重新開機**hello 重新開機的後端應用程式已完成。

1. 在 hello dm get 啟動資料夾中，建立名為 Maven 專案**模擬裝置**使用下列命令，在您的命令提示字元的 hello。 hello 以下是單一、 完整的命令：

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. 在命令提示字元中，瀏覽 toohello 模擬裝置資料夾。

1. 使用文字編輯器，開啟 hello 模擬裝置資料夾中的 hello pom.xml 檔案並新增下列相依性 toohello hello**相依性**節點。 此相依性可讓您 toouse hello iot 服務用戶端封裝您的應用程式 toocommunicate 與 IoT 中樞中：

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    ```

    > [!NOTE]
    > 您可以檢查 hello 最新版本的**iot 裝置用戶端**使用[Maven 搜尋][lnk-maven-device-search]。

1. 新增下列 hello**建置**節點之後 hello**相依性**節點。 此設定會指示 Maven toouse Java 1.8 toobuild hello 應用程式：

    ```xml
    <build>
      <plugins>
        <plugin>
          <groupId>org.apache.maven.plugins</groupId>
          <artifactId>maven-compiler-plugin</artifactId>
          <version>3.3</version>
          <configuration>
            <source>1.8</source>
            <target>1.8</target>
          </configuration>
        </plugin>
      </plugins>
    </build>
    ```

1. 儲存並關閉 hello pom.xml 檔案。

1. 使用文字編輯器開啟 hello simulated-device\src\main\java\com\mycompany\app\App.java 原始程式檔。

1. 新增下列 hello**匯入**陳述式 toohello 檔案：

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.microsoft.azure.sdk.iot.device.DeviceTwin.*;

    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.time.LocalDateTime;
    import java.util.Scanner;
    import java.util.Set;
    import java.util.HashSet;
    ```

1. 新增下列類別層級變數 toohello hello**應用程式**類別。 取代`{yourdeviceconnectionstring}`hello 裝置連接字串，而您在 hello 記下與*建立裝置身分識別*> 一節：

    ```java
    private static final int METHOD_SUCCESS = 200;
    private static final int METHOD_NOT_DEFINED = 404;

    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String connString = "{yourdeviceconnectionstring}";
    private static DeviceClient client;
    ```

1. tooimplement 直接的方法狀態事件的回呼處理常式將 hello 面一行加入巢狀類別 toohello**應用程式**類別：

    ```java
    protected static class DirectMethodStatusCallback implements IotHubEventCallback
    {
      public void execute(IotHubStatusCode status, Object context)
      {
        System.out.println("IoT Hub responded toodevice method operation with status " + status.name());
      }
    }
    ```

1. tooimplement 裝置兩個狀態事件的回呼處理常式將 hello 面一行加入巢狀類別 toohello**應用程式**類別：

    ```java
    protected static class DeviceTwinStatusCallback implements IotHubEventCallback
    {
        public void execute(IotHubStatusCode status, Object context)
        {
            System.out.println("IoT Hub responded toodevice twin operation with status " + status.name());
        }
    }
    ```

1. tooimplement 屬性事件的回呼處理常式將 hello 面一行加入巢狀類別 toohello**應用程式**類別：

    ```java
    protected static class PropertyCallback implements PropertyCallBack<String, String>
    {
      public void PropertyCall(String propertyKey, String propertyValue, Object context)
      {
        System.out.println("PropertyKey:     " + propertyKey);
        System.out.println("PropertyKvalue:  " + propertyKey);
      }
    }
    ```

1. tooimplement 執行緒 toosimulate hello 裝置重新開機，將 hello 面一行加入巢狀類別 toohello**應用程式**類別。 hello 執行緒進入睡眠狀態五秒，然後設定 hello **lastReboot**報告屬性：

    ```java
    protected static class RebootDeviceThread implements Runnable {
      public void run() {
        try {
          System.out.println("Rebooting...");
          Thread.sleep(5000);
          Property property = new Property("lastReboot", LocalDateTime.now());
          Set<Property> properties = new HashSet<Property>();
          properties.add(property);
          client.sendReportedProperties(properties);
          System.out.println("Rebooted");
        }
        catch (Exception ex) {
          System.out.println("Exception in reboot thread: " + ex.getMessage());
        }
      }
    }
    ```

1. tooimplement hello 直接方法 hello 在裝置上，將 hello 面一行加入巢狀類別 toohello**應用程式**類別。 當 hello 模擬應用程式會接收呼叫 toohello**重新開機**直接的方法，它會傳回通知 toohello 呼叫者，然後啟動執行緒 tooprocess hello 重新啟動：

    ```java
    protected static class DirectMethodCallback implements com.microsoft.azure.sdk.iot.device.DeviceTwin.DeviceMethodCallback
    {
      @Override
      public DeviceMethodData call(String methodName, Object methodData, Object context)
      {
        DeviceMethodData deviceMethodData;
        switch (methodName)
        {
          case "reboot" :
          {
            int status = METHOD_SUCCESS;
            System.out.println("Received reboot request");
            deviceMethodData = new DeviceMethodData(status, "Started reboot");
            RebootDeviceThread rebootThread = new RebootDeviceThread();
            Thread t = new Thread(rebootThread);
            t.start();
            break;
          }
          default:
          {
            int status = METHOD_NOT_DEFINED;
            deviceMethodData = new DeviceMethodData(status, "Not defined direct method " + methodName);
          }
        }
        return deviceMethodData;
      }
    }
    ```

1. 修改 hello 簽章的 hello**主要**方法 toothrow hello 下列例外狀況：

    ```java
    public static void main(String[] args) throws IOException, URISyntaxException
    ```

1. tooinstantiate **DeviceClient**，加入下列程式碼 toohello hello**主要**方法：

    ```java
    System.out.println("Starting device client sample...");
    client = new DeviceClient(connString, protocol);
    ```

1. toostart 接聽直接方法呼叫中，加入下列程式碼 toohello hello**主要**方法：

    ```java
    try
    {
      client.open();
      client.subscribeToDeviceMethod(new DirectMethodCallback(), null, new DirectMethodStatusCallback(), null);
      client.startDeviceTwin(new DeviceTwinStatusCallback(), null, new PropertyCallback(), null);
      System.out.println("Subscribed toodirect methods and polling for reported properties. Waiting...");
    }
    catch (Exception e)
    {
      System.out.println("On exception, shutting down \n" + " Cause: " + e.getCause() + " \n" +  e.getMessage());
      client.close();
      System.out.println("Shutting down...");
    }
    ```

1. tooshut 向 hello 裝置模擬器，加入下列程式碼 toohello hello**主要**方法：

    ```java
    System.out.println("Press any key tooexit...");
    Scanner scanner = new Scanner(System.in);
    scanner.nextLine();
    scanner.close();
    client.close();
    System.out.println("Shutting down...");
    ```

1. 儲存並關閉 hello simulated-device\src\main\java\com\mycompany\app\App.java 檔案。

1. 建置 hello**模擬裝置**後端應用程式，並更正任何錯誤。 在命令提示字元中，瀏覽 toohello 模擬裝置資料夾，然後執行下列命令的 hello:

    `mvn clean package -DskipTests`

## <a name="run-hello-apps"></a>執行 hello 應用程式

現在您已經準備就緒 toorun hello 應用程式。

1. Hello 模擬裝置資料夾中的命令提示字元，執行下列命令 toobegin 接聽重新開機或從 IoT 中樞的方法呼叫的 hello:

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Java IoT 中樞模擬裝置重新開機直接方法呼叫的應用程式 toolisten][1]

1. Hello 觸發程序重新啟動資料夾中的命令提示字元，執行下列模擬的裝置上的命令 toocall hello 重新開機方法，從 IoT 中樞的 hello:

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Java IoT 中樞服務應用程式 toocall hello 重新開機直接方法][2]

1. hello 模擬的裝置會回應 toohello 重新開機直接方法呼叫：

    ![Java IoT 中樞模擬的裝置應用程式回應 toohello 直接方法呼叫][3]

[!INCLUDE [iot-hub-dm-followup](../../includes/iot-hub-dm-followup.md)]

<!-- images and links -->
[1]: ./media/iot-hub-java-java-device-management-getstarted/launchsimulator.png
[2]: ./media/iot-hub-java-java-device-management-getstarted/triggerreboot.png
[3]: ./media/iot-hub-java-java-device-management-getstarted/respondtoreboot.png
<!-- Links -->

[lnk-maven]: https://maven.apache.org/what-is-maven.html

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-java/blob/master/doc/java-devbox-setup.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md

[lnk-maven-service-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22
[lnk-maven-device-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22