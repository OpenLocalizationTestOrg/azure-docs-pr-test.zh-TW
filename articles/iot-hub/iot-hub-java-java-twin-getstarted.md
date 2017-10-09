---
title: "aaaGet 開始使用 Azure IoT Hub 裝置雙 (Java) |Microsoft 文件"
description: "如何 toouse Azure IoT Hub 裝置雙 tooadd 標記，然後再使用 IoT 中樞查詢。 您可以使用 hello Azure IoT 裝置 SDK for Java tooimplement hello 裝置應用程式和 hello Java tooimplement 加入 hello 標記，並執行 hello IoT 中樞查詢中的服務應用程式的 Azure IoT 服務 SDK。"
services: iot-hub
documentationcenter: java
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/04/2017
ms.author: dobett
ms.openlocfilehash: 25f6fc81471d59c62bcdc3766bb5c33f5733c930
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-twins-java"></a>開始使用裝置對應項 (Java)

[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

在本教學課程中，您將建立兩個 Java 主控台應用程式：

* **add-tags-query**，可新增標籤和查詢裝置對應項的 Java 後端應用程式。
* **模擬裝置**，Java 裝置的應用程式，該連接 tooyour IoT 中樞與報表使用報告的屬性及其連線條件。

> [!NOTE]
> hello 文章[Azure IoT Sdk](iot-hub-devguide-sdks.md)提供 hello Azure IoT Sdk 的相關資訊，您可以使用 toobuild 裝置與後端應用程式。

toocomplete 本教學課程中，您需要：

* 最新 hello [Java SE 開發套件 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
* [Maven 3](https://maven.apache.org/install.html)
* 使用中的 Azure 帳戶。 (如果您沒有帳戶，只需要幾分鐘的時間就可以建立[免費帳戶](http://azure.microsoft.com/pricing/free-trial/)。)

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

如果您以程式設計方式偏好 toocreate hello 裝置識別身分，讀取 hello 對應的章節 hello[連接使用 Java 程式裝置 tooyour IoT 中樞](iot-hub-java-java-getstarted.md#create-a-device-identity)發行項。

## <a name="create-hello-service-app"></a>建立 hello 服務應用程式

在本節中，您會建立與相關聯的標記 toohello 裝置兩個在 IoT 中樞將位置中繼資料的 Java 應用程式**myDeviceId**。 hello 應用程式會先查詢 IoT 中樞位於美國、 hello 的裝置，然後再針對報表行動電話通訊網路連線的裝置。

1. 在您的開發電腦上建立名為 `iot-java-twin-getstarted` 的空資料夾。

1. 在 hello`iot-java-twin-getstarted`資料夾中，建立名為 Maven 專案**加入標記查詢**使用下列命令，在您的命令提示字元的 hello。 注意，這是一個單一且非常長的命令：

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=add-tags-query -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. 在命令提示字元中，瀏覽 toohello`add-tags-query`資料夾。

1. 使用文字編輯器開啟 hello`pom.xml`檔案在 hello`add-tags-query`資料夾並加入下列相依性 toohello hello**相依性**節點。 此相依性可讓您 toouse hello **iot 服務用戶端**在您的應用程式 toocommunicate 與 IoT 中樞中的套件：

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
      <type>jar</type>
    </dependency>
    ```

    > [!NOTE]
    > 您可以檢查 hello 最新版本的**iot 服務用戶端**使用[Maven 搜尋](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22)。

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

1. 儲存並關閉 hello`pom.xml`檔案。

1. 使用文字編輯器開啟 hello`add-tags-query\src\main\java\com\mycompany\app\App.java`檔案。

1. 新增下列 hello**匯入**陳述式 toohello 檔案：

    ```java
    import com.microsoft.azure.sdk.iot.service.devicetwin.*;
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;

    import java.io.IOException;
    import java.util.HashSet;
    import java.util.Set;
    ```

1. 新增下列類別層級變數 toohello hello**應用程式**類別。 取代`{youriothubconnectionstring}`與您在 hello 記下您的 IoT 中樞連接字串*建立 IoT 中樞*> 一節：

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    public static final String region = "US";
    public static final String plant = "Redmond43";
    ```

1. 更新 hello**主要**方法簽章 tooinclude hello 下列`throws`子句：

    ```java
    public static void main( String[] args ) throws IOException
    ```

1. 新增下列程式碼 toohello hello**主要**方法 toocreate hello **DeviceTwin**和**DeviceTwinDevice**物件。 hello **DeviceTwin**物件會處理與 IoT 中樞 hello 通訊。 hello **DeviceTwinDevice**物件都代表 hello 裝置的兩個具有其屬性和標記：

    ```java
    // Get hello DeviceTwin and DeviceTwinDevice objects
    DeviceTwin twinClient = DeviceTwin.createFromConnectionString(iotHubConnectionString);
    DeviceTwinDevice device = new DeviceTwinDevice(deviceId);
    ```

1. 新增下列 hello`try/catch`封鎖 toohello**主要**方法：

    ```java
    try {
      // Code goes here
    } catch (IotHubException e) {
      System.out.println(e.getMessage());
    } catch (IOException e) {
      System.out.println(e.getMessage());
    }
    ```

1. tooupdate hello**區域**和**工廠**裝置兩個標籤，在您的裝置兩個，加入下列程式碼中 hello hello`try`區塊：

    ```java
    // Get hello device twin from IoT Hub
    System.out.println("Device twin before update:");
    twinClient.getTwin(device);
    System.out.println(device);

    // Update device twin tags if they are different
    // from hello existing values
    String currentTags = device.tagsToString();
    if ((!currentTags.contains("region=" + region) && !currentTags.contains("plant=" + plant))) {
      // Create hello tags and attach them toohello DeviceTwinDevice object
      Set<Pair> tags = new HashSet<Pair>();
      tags.add(new Pair("region", region));
      tags.add(new Pair("plant", plant));
      device.setTags(tags);

      // Update hello device twin in IoT Hub
      System.out.println("Updating device twin");
      twinClient.updateTwin(device);
    }

    // Retrieve hello device twin with hello tag values from IoT Hub
    System.out.println("Device twin after update:");
    twinClient.getTwin(device);
    System.out.println(device);
    ```

1. 在 IoT 中樞 tooquery hello 裝置雙加入下列程式碼 toohello hello`try`之後 hello hello 先前步驟中所加入的程式碼區塊。 hello 程式碼會執行兩個查詢。 每個查詢都會傳回上限為 100 的裝置：

    ```java
    // Query hello device twins in IoT Hub
    System.out.println("Devices in Redmond:");

    // Construct hello query
    SqlQuery sqlQuery = SqlQuery.createSqlQuery("*", SqlQuery.FromType.DEVICES, "tags.plant='Redmond43'", null);

    // Run hello query, returning a maximum of 100 devices
    Query twinQuery = twinClient.queryTwin(sqlQuery.getQuery(), 100);
    while (twinClient.hasNextDeviceTwin(twinQuery)) {
      DeviceTwinDevice d = twinClient.getNextDeviceTwin(twinQuery);
      System.out.println(d.getDeviceId());
    }

    System.out.println("Devices in Redmond using a cellular network:");

    // Construct hello query
    sqlQuery = SqlQuery.createSqlQuery("*", SqlQuery.FromType.DEVICES, "tags.plant='Redmond43' AND properties.reported.connectivityType = 'cellular'", null);

    // Run hello query, returning a maximum of 100 devices
    twinQuery = twinClient.queryTwin(sqlQuery.getQuery(), 3);
    while (twinClient.hasNextDeviceTwin(twinQuery)) {
      DeviceTwinDevice d = twinClient.getNextDeviceTwin(twinQuery);
      System.out.println(d.getDeviceId());
    }
    ```

1. 儲存並關閉 hello`add-tags-query\src\main\java\com\mycompany\app\App.java`檔案

1. 建置 hello**加入標記查詢**應用程式，並更正任何錯誤。 在命令提示字元中，瀏覽 toohello`add-tags-query`資料夾，然後執行下列命令的 hello:

    `mvn clean package -DskipTests`

## <a name="create-a-device-app"></a>建立裝置應用程式

在本節中，您可以建立設定報告的屬性值，會傳送 tooIoT 中樞的 Java 主控台應用程式。

1. 在 hello`iot-java-twin-getstarted`資料夾中，建立名為 Maven 專案**模擬裝置**使用下列命令，在您的命令提示字元的 hello。 注意，這是一個單一且非常長的命令：

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. 在命令提示字元中，瀏覽 toohello`simulated-device`資料夾。

1. 使用文字編輯器開啟 hello`pom.xml`檔案在 hello`simulated-device`資料夾並加入下列相依性 toohello hello**相依性**節點。 此相依性可讓您 toouse hello **iot 裝置用戶端**在您的應用程式 toocommunicate 與 IoT 中樞中的套件：

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    ```

    > [!NOTE]
    > 您可以檢查 hello 最新版本的**iot 裝置用戶端**使用[Maven 搜尋](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22)。

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

1. 儲存並關閉 hello`pom.xml`檔案。

1. 使用文字編輯器開啟 hello`simulated-device\src\main\java\com\mycompany\app\App.java`檔案。

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
    ```

    此範例應用程式會使用 hello**通訊協定**變數時，它會具現化**DeviceClient**物件。 目前，toouse 裝置兩個功能您必須使用 hello MQTT 通訊協定。

1. 新增下列程式碼 toohello hello**主要**方法：
    * 建立裝置用戶端 toocommunicate 與 IoT 中樞。
    * 建立**裝置**物件 toostore hello 裝置兩個屬性。

    ```java
    DeviceClient client = new DeviceClient(connString, protocol);

    // Create a Device object toostore hello device twin properties
    Device dataCollector = new Device() {
      // Print details when a property value changes
      @Override
      public void PropertyCall(String propertyKey, Object propertyValue, Object context) {
        System.out.println(propertyKey + " changed too" + propertyValue);
      }
    };
    ```

1. 新增下列程式碼 toohello hello**主要**方法 toocreate **connectivityType**報告屬性，並將它傳送 tooIoT 中樞：

    ```java
    try {
      // Open hello DeviceClient and start hello device twin services.
      client.open();
      client.startDeviceTwin(new DeviceTwinStatusCallBack(), null, dataCollector, null);

      // Create a reported property and send it tooyour IoT hub.
      dataCollector.setReportedProp(new Property("connectivityType", "cellular"));
      client.sendReportedProperties(dataCollector.getReportedProp());
    }
    catch (Exception e) {
      System.out.println("On exception, shutting down \n" + " Cause: " + e.getCause() + " \n" + e.getMessage());
      dataCollector.clean();
      client.close();
      System.out.println("Shutting down...");
    }
    ```

1. 新增下列程式碼 toohello 結尾 hello hello**主要**方法。 等候 hello **Enter**金鑰可讓 hello 裝置兩個作業的 IoT 中樞 tooreport hello 狀態的時間：

    ```java
    System.out.println("Press any key tooexit...");

    Scanner scanner = new Scanner(System.in);
    scanner.nextLine();

    dataCollector.clean();
    client.close();
    ```

1. 儲存並關閉 hello`simulated-device\src\main\java\com\mycompany\app\App.java`檔案。

1. 建置 hello**模擬裝置**應用程式，並更正任何錯誤。 在命令提示字元中，瀏覽 toohello`simulated-device`資料夾，然後執行下列命令的 hello:

    `mvn clean package -DskipTests`

## <a name="run-hello-apps"></a>執行 hello 應用程式

現在您已經準備就緒 toorun hello 主控台應用程式。

1. 在命令提示字元中 hello`add-tags-query`資料夾中，執行下列命令 toorun hello hello**加入標記查詢**服務應用程式：

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Java IoT 中樞服務應用程式 tooupdate 標記值，並執行裝置查詢](media/iot-hub-java-java-twin-getstarted/service-app-1.png)

    您可以看到 hello**工廠**和**區域**加入 toohello 裝置兩個標記。 hello 第一個查詢會傳回您的裝置，但 hello 第二個則不然。

1. 在命令提示字元中 hello`simulated-device`資料夾中，執行下列命令 tooadd hello hello **connectivityType**報告屬性 toohello 裝置兩個：

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![hello 裝置用戶端加入 hello * * connectivityType * * 報告屬性](media/iot-hub-java-java-twin-getstarted/device-app-1.png)

1. 在命令提示字元中 hello`add-tags-query`資料夾中，執行下列命令 toorun hello hello**加入標記查詢**服務應用程式第二次：

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Java IoT 中樞服務應用程式 tooupdate 標記值，並執行裝置查詢](media/iot-hub-java-java-twin-getstarted/service-app-2.png)

    現在您的裝置已傳送嗨**connectivityType**屬性 tooIoT 集線器，hello 第二個查詢傳回您的裝置。

## <a name="next-steps"></a>後續步驟

在本教學課程中，您在 hello Azure 入口網站中設定新的 IoT 中樞，並接著 hello IoT 中樞的身分識別登錄中建立裝置身分識別。 您標記為加入裝置中繼資料，從後端應用程式，並在 hello 裝置兩個撰寫裝置應用程式 tooreport 裝置連線資訊。 您也學到如何 tooquery hello 裝置使用 hello 類似 SQL 的 IoT 中樞查詢語言的兩個資訊。

下列資源 toolearn 如何使用 hello 至：

* 從以 hello 的裝置將遙測傳送[開始使用 IoT 中樞](iot-hub-java-java-getstarted.md)教學課程。
* 控制以互動方式 （例如開啟風扇從使用者控制的應用程式） 的裝置以 hello[使用直接的方法](iot-hub-java-java-direct-methods.md)教學課程。

<!-- Images. -->
[7]: ./media/iot-hub-java-java-twin-getstarted/invoke-method.png
[8]: ./media/iot-hub-java-java-twin-getstarted/device-listen.png
[9]: ./media/iot-hub-java-java-twin-getstarted/device-respond.png

<!-- Links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
