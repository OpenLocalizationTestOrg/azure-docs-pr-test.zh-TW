---
title: "Azure IoT 中樞 aaaUse 直接方法 (Java) |Microsoft 文件"
description: "如何 toouse Azure IoT 中樞直接的方法。 您可以使用 hello Azure IoT 裝置 SDK for Java tooimplement 模擬的裝置應用程式，其中包含直接的方法和 hello Java tooimplement hello 直接的方法會叫用的服務應用程式的 Azure IoT 服務 SDK。"
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: ab035b8e-bff8-4e12-9536-f31d6b6fe425
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: b6f2f4a64535ab649a3965cd9c5a19bebaf88eef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-direct-methods-java"></a>使用直接方法 (Java)

[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

在本教學課程中，您將建立兩個 Java 主控台應用程式：

* **叫用直接方法**，Java 後端應用程式，以呼叫 hello 模擬的裝置應用程式中的方法，並顯示 hello 回應。
* **模擬裝置**，模擬裝置，使用您所建立的 hello 裝置身分識別連接 tooyour IoT 中樞的 Java 應用程式。 此應用程式會回應 toohello 直接叫用從 hello 後端。

> [!NOTE]
> 如需您可以在裝置和您的方案後端上使用 toobuild 應用程式 toorun 的 hello Sdk 資訊，請參閱[Azure IoT Sdk][lnk-hub-sdks]。

toocomplete 本教學課程中，您需要：

* Java SE 8。 <br/> [準備開發環境][ lnk-dev-setup]描述如何 tooinstall Java 本教學課程中的 Windows 或 Linux。
* Maven 3。  <br/> [準備開發環境][ lnk-dev-setup]描述如何 tooinstall [Maven] [ lnk-maven]本教學課程中的 Windows 或 Linux。
* [Node.js 版本 0.10.0 或更新版本](http://nodejs.org)。

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a>建立模擬裝置應用程式

在本節中，您可以建立回應 hello 方案回呼叫端的 tooa 方法的 Java 主控台應用程式。

1. 建立名為 iot-java-direct-method 的空資料夾。

1. 在 hello iot java-direct 方法資料夾中，建立名為 Maven 專案**模擬裝置**使用下列命令，在您的命令提示字元的 hello。 下列命令的 hello 是單一、 完整的命令：

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. 在命令提示字元中，瀏覽 toohello 模擬裝置資料夾。

1. 使用文字編輯器，開啟 hello 模擬裝置資料夾中的 hello pom.xml 檔案並新增下列相依性 toohello hello**相依性**節點。 此相依性可讓您 toouse hello iot 裝置用戶端封裝您的應用程式 toocommunicate 與 IoT 中樞中：

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

1. 使用文字編輯器開啟 hello simulated-device\src\main\java\com\mycompany\app\App.java 檔案。

1. 新增下列 hello**匯入**陳述式 toohello 檔案：

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.microsoft.azure.sdk.iot.device.DeviceTwin.*;

    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.util.Scanner;
    ```

1. 新增下列類別層級變數 toohello hello**應用程式**類別。 取代`{youriothubname}`以您的 IoT 中樞名稱，和`{yourdevicekey}`hello 裝置索引鍵值中 hello 產生*建立裝置身分識別*> 一節：

    ```java
    private static String connString = "HostName={youriothubname}.azure-devices.net;DeviceId=myDeviceID;SharedAccessKey={yourdevicekey}";
    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String deviceId = "myDeviceId";
    private static final int METHOD_SUCCESS = 200;
    private static final int METHOD_NOT_DEFINED = 404;
    ```

    此範例應用程式會使用 hello**通訊協定**變數時，它會具現化**DeviceClient**物件。 目前，toouse 直接方法，您必須使用 hello MQTT 通訊協定。

1. tooreturn 狀態程式碼 tooyour IoT 中樞，將 hello 面一行加入巢狀類別 toohello**應用程式**類別：

    ```java
    protected static class DirectMethodStatusCallback implements IotHubEventCallback
    {
      public void execute(IotHubStatusCode status, Object context)
      {
        System.out.println("IoT Hub responded toodevice method operation with status " + status.name());
      }
    }
    ```

1. toohandle hello 直接的方法引動過程從 hello 方案後端，將 hello 面一行加入巢狀類別 toohello**應用程式**類別：

    ```java
    protected static class DirectMethodCallback implements com.microsoft.azure.sdk.iot.device.DeviceTwin.DeviceMethodCallback
    {
      @Override
      public DeviceMethodData call(String methodName, Object methodData, Object context)
      {
        DeviceMethodData deviceMethodData;
        switch (methodName)
        {
          case "writeLine" :
          {
            int status = METHOD_SUCCESS;
            System.out.println(new String((byte[])methodData));
            deviceMethodData = new DeviceMethodData(status, "Executed direct method " + methodName);
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

1. toocreate **DeviceClient**並接聽直接的方法引動過程，加入**主要**方法 toohello**應用程式**類別：

    ```java
    public static void main(String[] args)
      throws IOException, URISyntaxException
    {
      System.out.println("Starting device sample...");

      DeviceClient client = new DeviceClient(connString, protocol);

      try
      {
        client.open();
        client.subscribeToDeviceMethod(new DirectMethodCallback(), null, new DirectMethodStatusCallback(), null);
        System.out.println("Subscribed toodirect methods. Waiting...");
      }
      catch (Exception e)
      {
        System.out.println("On exception, shutting down \n" + " Cause: " + e.getCause() + " \n" +  e.getMessage());
        client.close();
        System.out.println("Shutting down...");
      }

      System.out.println("Press any key tooexit...");
      Scanner scanner = new Scanner(System.in);
      scanner.nextLine();
      scanner.close();
      client.close();
      System.out.println("Shutting down...");
    }
    ```

1. 儲存並關閉 hello simulated-device\src\main\java\com\mycompany\app\App.java 檔案

1. 建置 hello**模擬裝置**應用程式，並更正任何錯誤。 在命令提示字元中，瀏覽 toohello 模擬裝置資料夾，然後執行下列命令的 hello:

    `mvn clean package -DskipTests`

## <a name="call-a-direct-method-on-a-device"></a>在裝置上呼叫直接方法

在本節中，您可以建立 Java 主控台應用程式會叫用直接的方法，並顯示 hello 回應。 此主控台應用程式會連接 tooyour IoT 中樞 tooinvoke hello 直接的方法。

1. 在 hello iot java-direct 方法資料夾中，建立名為 Maven 專案**叫用直接方法**使用下列命令，在您的命令提示字元的 hello。 下列命令的 hello 是單一、 完整的命令：

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=invoke-direct-method -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. 在命令提示字元中，瀏覽 toohello 叫用直接方法資料夾。

1. 使用文字編輯器，開啟 hello 叫用直接方法資料夾中的 hello pom.xml 檔案並新增下列相依性 toohello hello**相依性**節點。 此相依性可讓您 toouse hello iot 服務用戶端封裝您的應用程式 toocommunicate 與 IoT 中樞中：

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

1. 使用文字編輯器開啟 hello invoke-direct-method\src\main\java\com\mycompany\app\App.java 檔案。

1. 新增下列 hello**匯入**陳述式 toohello 檔案：

    ```java
    import com.microsoft.azure.sdk.iot.service.devicetwin.DeviceMethod;
    import com.microsoft.azure.sdk.iot.service.devicetwin.MethodResult;
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;

    import java.io.IOException;
    import java.util.concurrent.TimeUnit;
    ```

1. 新增下列類別層級變數 toohello hello**應用程式**類別。 取代`{youriothubconnectionstring}`與您在 hello 記下您的 IoT 中樞連接字串*建立 IoT 中樞*> 一節：

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    public static final String methodName = "writeLine";
    public static final Long responseTimeout = TimeUnit.SECONDS.toSeconds(30);
    public static final Long connectTimeout = TimeUnit.SECONDS.toSeconds(5);
    public static final String payload = "a line toobe written";
    ```

1. tooinvoke hello 方法 hello 模擬在裝置上，加入下列程式碼 toohello hello**主要**方法：

    ```java
    System.out.println("Starting sample...");
    DeviceMethod methodClient = DeviceMethod.createFromConnectionString(iotHubConnectionString);

    try
    {
        System.out.println("Invoke direct method");
        MethodResult result = methodClient.invoke(deviceId, methodName, responseTimeout, connectTimeout, payload);

        if(result == null)
        {
            throw new IOException("Direct method invoke returns null");
        }
        System.out.println("Status=" + result.getStatus());
        System.out.println("Payload=" + result.getPayload());
    }
    catch (IotHubException e)
    {
        System.out.println(e.getMessage());
    }

    System.out.println("Shutting down sample...");
    ```

1. 儲存並關閉 hello invoke-direct-method\src\main\java\com\mycompany\app\App.java 檔案

1. 建置 hello**叫用直接方法**應用程式，並更正任何錯誤。 在命令提示字元中，瀏覽 toohello 叫用直接方法資料夾，然後執行下列命令的 hello:

    `mvn clean package -DskipTests`

## <a name="run-hello-apps"></a>執行 hello 應用程式

現在您已經準備就緒 toorun hello 主控台應用程式。

1. Hello 模擬裝置資料夾中的命令提示字元，執行下列命令 toobegin 接聽從 IoT 中樞的方法呼叫的 hello:

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Java IoT 中樞模擬裝置的直接方法呼叫的應用程式 toolisten][8]

1. Hello 叫用直接方法資料夾中的命令提示字元，執行下列命令 toocall hello 方法模擬的裝置上從 IoT 中樞：

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Java IoT 中樞服務應用程式 toocall 直接的方法][7]

1. hello 模擬的裝置會回應 toohello 直接方法呼叫：

    ![Java IoT 中樞模擬的裝置應用程式回應 toohello 直接方法呼叫][9]

## <a name="next-steps"></a>後續步驟

在本教學課程中，您在 hello Azure 入口網站中設定新的 IoT 中樞，並接著 hello IoT 中樞的身分識別登錄中建立裝置身分識別。 您已經使用此裝置身分識別 tooenable hello 模擬裝置的應用程式 tooreact toomethods hello 雲端所叫用。 您也會建立叫用 hello 裝置上的方法，並會顯示 hello 回應 hello 裝置的應用程式。

tooexplore 其他 IoT 案例，請參閱[多個裝置上的工作排程][lnk-devguide-jobs]。

toolearn 如何 tooextend IoT 解決方案和排程方法呼叫上多個裝置，請參閱 hello[排程和廣播的工作][ lnk-tutorial-jobs]教學課程。

<!-- Images. -->
[7]: ./media/iot-hub-java-java-direct-methods/invoke-method.png
[8]: ./media/iot-hub-java-java-direct-methods/device-listen.png
[9]: ./media/iot-hub-java-java-direct-methods/device-respond.png

<!-- Links -->
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-java/blob/master/doc/java-devbox-setup.md
[lnk-maven]: https://maven.apache.org/what-is-maven.html
[lnk-hub-sdks]: iot-hub-devguide-sdks.md

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-maven-service-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22
[lnk-maven-device-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22
