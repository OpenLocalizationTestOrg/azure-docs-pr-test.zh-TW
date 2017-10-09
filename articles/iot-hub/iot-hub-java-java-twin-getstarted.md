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
# <a name="get-started-with-device-twins-java"></a><span data-ttu-id="719c6-104">開始使用裝置對應項 (Java)</span><span class="sxs-lookup"><span data-stu-id="719c6-104">Get started with device twins (Java)</span></span>

[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

<span data-ttu-id="719c6-105">在本教學課程中，您將建立兩個 Java 主控台應用程式：</span><span class="sxs-lookup"><span data-stu-id="719c6-105">In this tutorial, you create two Java console apps:</span></span>

* <span data-ttu-id="719c6-106">**add-tags-query**，可新增標籤和查詢裝置對應項的 Java 後端應用程式。</span><span class="sxs-lookup"><span data-stu-id="719c6-106">**add-tags-query**, a Java back-end app that adds tags and queries device twins.</span></span>
* <span data-ttu-id="719c6-107">**模擬裝置**，Java 裝置的應用程式，該連接 tooyour IoT 中樞與報表使用報告的屬性及其連線條件。</span><span class="sxs-lookup"><span data-stu-id="719c6-107">**simulated-device**, a Java device app that that connects tooyour IoT hub and reports its connectivity condition using a reported property.</span></span>

> [!NOTE]
> <span data-ttu-id="719c6-108">hello 文章[Azure IoT Sdk](iot-hub-devguide-sdks.md)提供 hello Azure IoT Sdk 的相關資訊，您可以使用 toobuild 裝置與後端應用程式。</span><span class="sxs-lookup"><span data-stu-id="719c6-108">hello article [Azure IoT SDKs](iot-hub-devguide-sdks.md) provides information about hello Azure IoT SDKs that you can use toobuild both device and back-end apps.</span></span>

<span data-ttu-id="719c6-109">toocomplete 本教學課程中，您需要：</span><span class="sxs-lookup"><span data-stu-id="719c6-109">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="719c6-110">最新 hello [Java SE 開發套件 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span><span class="sxs-lookup"><span data-stu-id="719c6-110">hello latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span>
* [<span data-ttu-id="719c6-111">Maven 3</span><span class="sxs-lookup"><span data-stu-id="719c6-111">Maven 3</span></span>](https://maven.apache.org/install.html)
* <span data-ttu-id="719c6-112">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="719c6-112">An active Azure account.</span></span> <span data-ttu-id="719c6-113">(如果您沒有帳戶，只需要幾分鐘的時間就可以建立[免費帳戶](http://azure.microsoft.com/pricing/free-trial/)。)</span><span class="sxs-lookup"><span data-stu-id="719c6-113">(If you don't have an account, you can create a [free account](http://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

<span data-ttu-id="719c6-114">如果您以程式設計方式偏好 toocreate hello 裝置識別身分，讀取 hello 對應的章節 hello[連接使用 Java 程式裝置 tooyour IoT 中樞](iot-hub-java-java-getstarted.md#create-a-device-identity)發行項。</span><span class="sxs-lookup"><span data-stu-id="719c6-114">If you prefer toocreate hello device identity programmatically, read hello corresponding section in hello [Connect your device tooyour IoT hub using Java](iot-hub-java-java-getstarted.md#create-a-device-identity) article.</span></span>

## <a name="create-hello-service-app"></a><span data-ttu-id="719c6-115">建立 hello 服務應用程式</span><span class="sxs-lookup"><span data-stu-id="719c6-115">Create hello service app</span></span>

<span data-ttu-id="719c6-116">在本節中，您會建立與相關聯的標記 toohello 裝置兩個在 IoT 中樞將位置中繼資料的 Java 應用程式**myDeviceId**。</span><span class="sxs-lookup"><span data-stu-id="719c6-116">In this section, you create a Java app that adds location metadata as a tag toohello device twin in IoT Hub associated with **myDeviceId**.</span></span> <span data-ttu-id="719c6-117">hello 應用程式會先查詢 IoT 中樞位於美國、 hello 的裝置，然後再針對報表行動電話通訊網路連線的裝置。</span><span class="sxs-lookup"><span data-stu-id="719c6-117">hello app first queries IoT hub for devices located in hello US, and then for devices that report a cellular network connection.</span></span>

1. <span data-ttu-id="719c6-118">在您的開發電腦上建立名為 `iot-java-twin-getstarted` 的空資料夾。</span><span class="sxs-lookup"><span data-stu-id="719c6-118">On your development machine, create an empty folder called `iot-java-twin-getstarted`.</span></span>

1. <span data-ttu-id="719c6-119">在 hello`iot-java-twin-getstarted`資料夾中，建立名為 Maven 專案**加入標記查詢**使用下列命令，在您的命令提示字元的 hello。</span><span class="sxs-lookup"><span data-stu-id="719c6-119">In hello `iot-java-twin-getstarted` folder, create a Maven project called **add-tags-query** using hello following command at your command prompt.</span></span> <span data-ttu-id="719c6-120">注意，這是一個單一且非常長的命令：</span><span class="sxs-lookup"><span data-stu-id="719c6-120">Note this is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=add-tags-query -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="719c6-121">在命令提示字元中，瀏覽 toohello`add-tags-query`資料夾。</span><span class="sxs-lookup"><span data-stu-id="719c6-121">At your command prompt, navigate toohello `add-tags-query` folder.</span></span>

1. <span data-ttu-id="719c6-122">使用文字編輯器開啟 hello`pom.xml`檔案在 hello`add-tags-query`資料夾並加入下列相依性 toohello hello**相依性**節點。</span><span class="sxs-lookup"><span data-stu-id="719c6-122">Using a text editor, open hello `pom.xml` file in hello `add-tags-query` folder and add hello following dependency toohello **dependencies** node.</span></span> <span data-ttu-id="719c6-123">此相依性可讓您 toouse hello **iot 服務用戶端**在您的應用程式 toocommunicate 與 IoT 中樞中的套件：</span><span class="sxs-lookup"><span data-stu-id="719c6-123">This dependency enables you toouse hello **iot-service-client** package in your app toocommunicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
      <type>jar</type>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="719c6-124">您可以檢查 hello 最新版本的**iot 服務用戶端**使用[Maven 搜尋](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22)。</span><span class="sxs-lookup"><span data-stu-id="719c6-124">You can check for hello latest version of **iot-service-client** using [Maven search](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span></span>

1. <span data-ttu-id="719c6-125">新增下列 hello**建置**節點之後 hello**相依性**節點。</span><span class="sxs-lookup"><span data-stu-id="719c6-125">Add hello following **build** node after hello **dependencies** node.</span></span> <span data-ttu-id="719c6-126">此設定會指示 Maven toouse Java 1.8 toobuild hello 應用程式：</span><span class="sxs-lookup"><span data-stu-id="719c6-126">This configuration instructs Maven toouse Java 1.8 toobuild hello app:</span></span>

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

1. <span data-ttu-id="719c6-127">儲存並關閉 hello`pom.xml`檔案。</span><span class="sxs-lookup"><span data-stu-id="719c6-127">Save and close hello `pom.xml` file.</span></span>

1. <span data-ttu-id="719c6-128">使用文字編輯器開啟 hello`add-tags-query\src\main\java\com\mycompany\app\App.java`檔案。</span><span class="sxs-lookup"><span data-stu-id="719c6-128">Using a text editor, open hello `add-tags-query\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="719c6-129">新增下列 hello**匯入**陳述式 toohello 檔案：</span><span class="sxs-lookup"><span data-stu-id="719c6-129">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.service.devicetwin.*;
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;

    import java.io.IOException;
    import java.util.HashSet;
    import java.util.Set;
    ```

1. <span data-ttu-id="719c6-130">新增下列類別層級變數 toohello hello**應用程式**類別。</span><span class="sxs-lookup"><span data-stu-id="719c6-130">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="719c6-131">取代`{youriothubconnectionstring}`與您在 hello 記下您的 IoT 中樞連接字串*建立 IoT 中樞*> 一節：</span><span class="sxs-lookup"><span data-stu-id="719c6-131">Replace `{youriothubconnectionstring}` with your IoT hub connection string you noted in hello *Create an IoT Hub* section:</span></span>

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    public static final String region = "US";
    public static final String plant = "Redmond43";
    ```

1. <span data-ttu-id="719c6-132">更新 hello**主要**方法簽章 tooinclude hello 下列`throws`子句：</span><span class="sxs-lookup"><span data-stu-id="719c6-132">Update hello **main** method signature tooinclude hello following `throws` clause:</span></span>

    ```java
    public static void main( String[] args ) throws IOException
    ```

1. <span data-ttu-id="719c6-133">新增下列程式碼 toohello hello**主要**方法 toocreate hello **DeviceTwin**和**DeviceTwinDevice**物件。</span><span class="sxs-lookup"><span data-stu-id="719c6-133">Add hello following code toohello **main** method toocreate hello **DeviceTwin** and **DeviceTwinDevice** objects.</span></span> <span data-ttu-id="719c6-134">hello **DeviceTwin**物件會處理與 IoT 中樞 hello 通訊。</span><span class="sxs-lookup"><span data-stu-id="719c6-134">hello **DeviceTwin** object handles hello communication with your IoT hub.</span></span> <span data-ttu-id="719c6-135">hello **DeviceTwinDevice**物件都代表 hello 裝置的兩個具有其屬性和標記：</span><span class="sxs-lookup"><span data-stu-id="719c6-135">hello **DeviceTwinDevice** object represents hello device twin with its properties and tags:</span></span>

    ```java
    // Get hello DeviceTwin and DeviceTwinDevice objects
    DeviceTwin twinClient = DeviceTwin.createFromConnectionString(iotHubConnectionString);
    DeviceTwinDevice device = new DeviceTwinDevice(deviceId);
    ```

1. <span data-ttu-id="719c6-136">新增下列 hello`try/catch`封鎖 toohello**主要**方法：</span><span class="sxs-lookup"><span data-stu-id="719c6-136">Add hello following `try/catch` block toohello **main** method:</span></span>

    ```java
    try {
      // Code goes here
    } catch (IotHubException e) {
      System.out.println(e.getMessage());
    } catch (IOException e) {
      System.out.println(e.getMessage());
    }
    ```

1. <span data-ttu-id="719c6-137">tooupdate hello**區域**和**工廠**裝置兩個標籤，在您的裝置兩個，加入下列程式碼中 hello hello`try`區塊：</span><span class="sxs-lookup"><span data-stu-id="719c6-137">tooupdate hello **region** and **plant** device twin tags in your device twin, add hello following code in hello `try` block:</span></span>

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

1. <span data-ttu-id="719c6-138">在 IoT 中樞 tooquery hello 裝置雙加入下列程式碼 toohello hello`try`之後 hello hello 先前步驟中所加入的程式碼區塊。</span><span class="sxs-lookup"><span data-stu-id="719c6-138">tooquery hello device twins in IoT hub, add hello following code toohello `try` block after hello code you added in hello previous step.</span></span> <span data-ttu-id="719c6-139">hello 程式碼會執行兩個查詢。</span><span class="sxs-lookup"><span data-stu-id="719c6-139">hello code runs two queries.</span></span> <span data-ttu-id="719c6-140">每個查詢都會傳回上限為 100 的裝置：</span><span class="sxs-lookup"><span data-stu-id="719c6-140">Each query returns a maximum of 100 devices:</span></span>

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

1. <span data-ttu-id="719c6-141">儲存並關閉 hello`add-tags-query\src\main\java\com\mycompany\app\App.java`檔案</span><span class="sxs-lookup"><span data-stu-id="719c6-141">Save and close hello `add-tags-query\src\main\java\com\mycompany\app\App.java` file</span></span>

1. <span data-ttu-id="719c6-142">建置 hello**加入標記查詢**應用程式，並更正任何錯誤。</span><span class="sxs-lookup"><span data-stu-id="719c6-142">Build hello **add-tags-query** app and correct any errors.</span></span> <span data-ttu-id="719c6-143">在命令提示字元中，瀏覽 toohello`add-tags-query`資料夾，然後執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="719c6-143">At your command prompt, navigate toohello `add-tags-query` folder and run hello following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="create-a-device-app"></a><span data-ttu-id="719c6-144">建立裝置應用程式</span><span class="sxs-lookup"><span data-stu-id="719c6-144">Create a device app</span></span>

<span data-ttu-id="719c6-145">在本節中，您可以建立設定報告的屬性值，會傳送 tooIoT 中樞的 Java 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="719c6-145">In this section, you create a Java console app that sets a reported property value that is sent tooIoT Hub.</span></span>

1. <span data-ttu-id="719c6-146">在 hello`iot-java-twin-getstarted`資料夾中，建立名為 Maven 專案**模擬裝置**使用下列命令，在您的命令提示字元的 hello。</span><span class="sxs-lookup"><span data-stu-id="719c6-146">In hello `iot-java-twin-getstarted` folder, create a Maven project called **simulated-device** using hello following command at your command prompt.</span></span> <span data-ttu-id="719c6-147">注意，這是一個單一且非常長的命令：</span><span class="sxs-lookup"><span data-stu-id="719c6-147">Note this is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="719c6-148">在命令提示字元中，瀏覽 toohello`simulated-device`資料夾。</span><span class="sxs-lookup"><span data-stu-id="719c6-148">At your command prompt, navigate toohello `simulated-device` folder.</span></span>

1. <span data-ttu-id="719c6-149">使用文字編輯器開啟 hello`pom.xml`檔案在 hello`simulated-device`資料夾並加入下列相依性 toohello hello**相依性**節點。</span><span class="sxs-lookup"><span data-stu-id="719c6-149">Using a text editor, open hello `pom.xml` file in hello `simulated-device` folder and add hello following dependencies toohello **dependencies** node.</span></span> <span data-ttu-id="719c6-150">此相依性可讓您 toouse hello **iot 裝置用戶端**在您的應用程式 toocommunicate 與 IoT 中樞中的套件：</span><span class="sxs-lookup"><span data-stu-id="719c6-150">This dependency enables you toouse hello **iot-device-client** package in your app toocommunicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="719c6-151">您可以檢查 hello 最新版本的**iot 裝置用戶端**使用[Maven 搜尋](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22)。</span><span class="sxs-lookup"><span data-stu-id="719c6-151">You can check for hello latest version of **iot-device-client** using [Maven search](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span></span>

1. <span data-ttu-id="719c6-152">新增下列 hello**建置**節點之後 hello**相依性**節點。</span><span class="sxs-lookup"><span data-stu-id="719c6-152">Add hello following **build** node after hello **dependencies** node.</span></span> <span data-ttu-id="719c6-153">此設定會指示 Maven toouse Java 1.8 toobuild hello 應用程式：</span><span class="sxs-lookup"><span data-stu-id="719c6-153">This configuration instructs Maven toouse Java 1.8 toobuild hello app:</span></span>

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

1. <span data-ttu-id="719c6-154">儲存並關閉 hello`pom.xml`檔案。</span><span class="sxs-lookup"><span data-stu-id="719c6-154">Save and close hello `pom.xml` file.</span></span>

1. <span data-ttu-id="719c6-155">使用文字編輯器開啟 hello`simulated-device\src\main\java\com\mycompany\app\App.java`檔案。</span><span class="sxs-lookup"><span data-stu-id="719c6-155">Using a text editor, open hello `simulated-device\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="719c6-156">新增下列 hello**匯入**陳述式 toohello 檔案：</span><span class="sxs-lookup"><span data-stu-id="719c6-156">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.microsoft.azure.sdk.iot.device.DeviceTwin.*;

    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.util.Scanner;
    ```

1. <span data-ttu-id="719c6-157">新增下列類別層級變數 toohello hello**應用程式**類別。</span><span class="sxs-lookup"><span data-stu-id="719c6-157">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="719c6-158">取代`{youriothubname}`以您的 IoT 中樞名稱，和`{yourdevicekey}`hello 裝置索引鍵值中 hello 產生*建立裝置身分識別*> 一節：</span><span class="sxs-lookup"><span data-stu-id="719c6-158">Replacing `{youriothubname}` with your IoT hub name, and `{yourdevicekey}` with hello device key value you generated in hello *Create a device identity* section:</span></span>

    ```java
    private static String connString = "HostName={youriothubname}.azure-devices.net;DeviceId=myDeviceID;SharedAccessKey={yourdevicekey}";
    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String deviceId = "myDeviceId";
    ```

    <span data-ttu-id="719c6-159">此範例應用程式會使用 hello**通訊協定**變數時，它會具現化**DeviceClient**物件。</span><span class="sxs-lookup"><span data-stu-id="719c6-159">This sample app uses hello **protocol** variable when it instantiates a **DeviceClient** object.</span></span> <span data-ttu-id="719c6-160">目前，toouse 裝置兩個功能您必須使用 hello MQTT 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="719c6-160">Currently, toouse device twin features you must use hello MQTT protocol.</span></span>

1. <span data-ttu-id="719c6-161">新增下列程式碼 toohello hello**主要**方法：</span><span class="sxs-lookup"><span data-stu-id="719c6-161">Add hello following code toohello **main** method to:</span></span>
    * <span data-ttu-id="719c6-162">建立裝置用戶端 toocommunicate 與 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="719c6-162">Create a device client toocommunicate with IoT Hub.</span></span>
    * <span data-ttu-id="719c6-163">建立**裝置**物件 toostore hello 裝置兩個屬性。</span><span class="sxs-lookup"><span data-stu-id="719c6-163">Create a **Device** object toostore hello device twin properties.</span></span>

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

1. <span data-ttu-id="719c6-164">新增下列程式碼 toohello hello**主要**方法 toocreate **connectivityType**報告屬性，並將它傳送 tooIoT 中樞：</span><span class="sxs-lookup"><span data-stu-id="719c6-164">Add hello following code toohello **main** method toocreate a **connectivityType** reported property and send it tooIoT Hub:</span></span>

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

1. <span data-ttu-id="719c6-165">新增下列程式碼 toohello 結尾 hello hello**主要**方法。</span><span class="sxs-lookup"><span data-stu-id="719c6-165">Add hello following code toohello end of hello **main** method.</span></span> <span data-ttu-id="719c6-166">等候 hello **Enter**金鑰可讓 hello 裝置兩個作業的 IoT 中樞 tooreport hello 狀態的時間：</span><span class="sxs-lookup"><span data-stu-id="719c6-166">Waiting for hello **Enter** key allows time for IoT Hub tooreport hello status of hello device twin operations:</span></span>

    ```java
    System.out.println("Press any key tooexit...");

    Scanner scanner = new Scanner(System.in);
    scanner.nextLine();

    dataCollector.clean();
    client.close();
    ```

1. <span data-ttu-id="719c6-167">儲存並關閉 hello`simulated-device\src\main\java\com\mycompany\app\App.java`檔案。</span><span class="sxs-lookup"><span data-stu-id="719c6-167">Save and close hello `simulated-device\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="719c6-168">建置 hello**模擬裝置**應用程式，並更正任何錯誤。</span><span class="sxs-lookup"><span data-stu-id="719c6-168">Build hello **simulated-device** app and correct any errors.</span></span> <span data-ttu-id="719c6-169">在命令提示字元中，瀏覽 toohello`simulated-device`資料夾，然後執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="719c6-169">At your command prompt, navigate toohello `simulated-device` folder and run hello following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="run-hello-apps"></a><span data-ttu-id="719c6-170">執行 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="719c6-170">Run hello apps</span></span>

<span data-ttu-id="719c6-171">現在您已經準備就緒 toorun hello 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="719c6-171">You are now ready toorun hello console apps.</span></span>

1. <span data-ttu-id="719c6-172">在命令提示字元中 hello`add-tags-query`資料夾中，執行下列命令 toorun hello hello**加入標記查詢**服務應用程式：</span><span class="sxs-lookup"><span data-stu-id="719c6-172">At a command prompt in hello `add-tags-query` folder, run hello following command toorun hello **add-tags-query** service app:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Java IoT 中樞服務應用程式 tooupdate 標記值，並執行裝置查詢](media/iot-hub-java-java-twin-getstarted/service-app-1.png)

    <span data-ttu-id="719c6-174">您可以看到 hello**工廠**和**區域**加入 toohello 裝置兩個標記。</span><span class="sxs-lookup"><span data-stu-id="719c6-174">You can see hello **plant** and **region** tags added toohello device twin.</span></span> <span data-ttu-id="719c6-175">hello 第一個查詢會傳回您的裝置，但 hello 第二個則不然。</span><span class="sxs-lookup"><span data-stu-id="719c6-175">hello first query returns your device, but hello second does not.</span></span>

1. <span data-ttu-id="719c6-176">在命令提示字元中 hello`simulated-device`資料夾中，執行下列命令 tooadd hello hello **connectivityType**報告屬性 toohello 裝置兩個：</span><span class="sxs-lookup"><span data-stu-id="719c6-176">At a command prompt in hello `simulated-device` folder, run hello following command tooadd hello **connectivityType** reported property toohello device twin:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![hello 裝置用戶端加入 hello * * connectivityType * * 報告屬性](media/iot-hub-java-java-twin-getstarted/device-app-1.png)

1. <span data-ttu-id="719c6-178">在命令提示字元中 hello`add-tags-query`資料夾中，執行下列命令 toorun hello hello**加入標記查詢**服務應用程式第二次：</span><span class="sxs-lookup"><span data-stu-id="719c6-178">At a command prompt in hello `add-tags-query` folder, run hello following command toorun hello **add-tags-query** service app a second time:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Java IoT 中樞服務應用程式 tooupdate 標記值，並執行裝置查詢](media/iot-hub-java-java-twin-getstarted/service-app-2.png)

    <span data-ttu-id="719c6-180">現在您的裝置已傳送嗨**connectivityType**屬性 tooIoT 集線器，hello 第二個查詢傳回您的裝置。</span><span class="sxs-lookup"><span data-stu-id="719c6-180">Now your device has sent hello **connectivityType** property tooIoT Hub, hello second query returns your device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="719c6-181">後續步驟</span><span class="sxs-lookup"><span data-stu-id="719c6-181">Next steps</span></span>

<span data-ttu-id="719c6-182">在本教學課程中，您在 hello Azure 入口網站中設定新的 IoT 中樞，並接著 hello IoT 中樞的身分識別登錄中建立裝置身分識別。</span><span class="sxs-lookup"><span data-stu-id="719c6-182">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="719c6-183">您標記為加入裝置中繼資料，從後端應用程式，並在 hello 裝置兩個撰寫裝置應用程式 tooreport 裝置連線資訊。</span><span class="sxs-lookup"><span data-stu-id="719c6-183">You added device metadata as tags from a back-end app, and wrote a device app tooreport device connectivity information in hello device twin.</span></span> <span data-ttu-id="719c6-184">您也學到如何 tooquery hello 裝置使用 hello 類似 SQL 的 IoT 中樞查詢語言的兩個資訊。</span><span class="sxs-lookup"><span data-stu-id="719c6-184">You also learned how tooquery hello device twin information using hello SQL-like IoT Hub query language.</span></span>

<span data-ttu-id="719c6-185">下列資源 toolearn 如何使用 hello 至：</span><span class="sxs-lookup"><span data-stu-id="719c6-185">Use hello following resources toolearn how to:</span></span>

* <span data-ttu-id="719c6-186">從以 hello 的裝置將遙測傳送[開始使用 IoT 中樞](iot-hub-java-java-getstarted.md)教學課程。</span><span class="sxs-lookup"><span data-stu-id="719c6-186">Send telemetry from devices with hello [Get started with IoT Hub](iot-hub-java-java-getstarted.md) tutorial.</span></span>
* <span data-ttu-id="719c6-187">控制以互動方式 （例如開啟風扇從使用者控制的應用程式） 的裝置以 hello[使用直接的方法](iot-hub-java-java-direct-methods.md)教學課程。</span><span class="sxs-lookup"><span data-stu-id="719c6-187">Control devices interactively (such as turning on a fan from a user-controlled app) with hello [Use direct methods](iot-hub-java-java-direct-methods.md) tutorial.</span></span>

<!-- Images. -->
[7]: ./media/iot-hub-java-java-twin-getstarted/invoke-method.png
[8]: ./media/iot-hub-java-java-twin-getstarted/device-listen.png
[9]: ./media/iot-hub-java-java-twin-getstarted/device-respond.png

<!-- Links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
