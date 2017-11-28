---
title: "aaaGet 開始使用 Azure IoT 中樞 (Java) |Microsoft 文件"
description: "了解如何 toosend 裝置到雲端訊息 tooAzure 使用 IoT Sdk for Java 的 IoT 中樞。 建立模擬的裝置和服務應用程式 tooregister 您的裝置、 傳送訊息，以及從 IoT 中樞讀取訊息。"
services: iot-hub
documentationcenter: java
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 70dae4a8-0e98-4c53-b5a5-9d6963abb245
ms.service: iot-hub
ms.devlang: java
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ac954f0522b46ed2a5b4a819bc611c13be0b9a9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-device-tooyour-iot-hub-using-java"></a><span data-ttu-id="13572-104">連接使用 Java 程式裝置 tooyour IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="13572-104">Connect your device tooyour IoT hub using Java</span></span>
[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

<span data-ttu-id="13572-105">在本教學課程的 hello 最後，您有三個 Java 主控台應用程式：</span><span class="sxs-lookup"><span data-stu-id="13572-105">At hello end of this tutorial, you have three Java console apps:</span></span>

* <span data-ttu-id="13572-106">**建立裝置身分識別**，這樣就可以建立裝置身分識別，以及相關聯的安全性金鑰 tooconnect 您裝置的應用程式。</span><span class="sxs-lookup"><span data-stu-id="13572-106">**create-device-identity**, which creates a device identity and associated security key tooconnect your device app.</span></span>
* <span data-ttu-id="13572-107">**閱讀 d2c 郵件**，其中顯示您裝置的應用程式所傳送的 hello 遙測。</span><span class="sxs-lookup"><span data-stu-id="13572-107">**read-d2c-messages**, which displays hello telemetry sent by your device app.</span></span>
* <span data-ttu-id="13572-108">**模擬裝置**，這與 hello 稍早建立的裝置身分識別連接 tooyour IoT 中樞，並傳送遙測訊息每個第二個使用 hello MQTT 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="13572-108">**simulated-device**, which connects tooyour IoT hub with hello device identity created earlier, and sends a telemetry message every second using hello MQTT protocol.</span></span>

> [!NOTE]
> <span data-ttu-id="13572-109">hello 文章[Azure IoT Sdk] [ lnk-hub-sdks]提供 hello Azure IoT Sdk 的相關資訊，您可以使用 toobuild 這兩個應用程式 toorun 裝置和您的方案後端上。</span><span class="sxs-lookup"><span data-stu-id="13572-109">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both apps toorun on devices and your solution back end.</span></span>

<span data-ttu-id="13572-110">toocomplete 本教學課程中，您需要遵循的 hello:</span><span class="sxs-lookup"><span data-stu-id="13572-110">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="13572-111">最新 hello [Java SE 開發套件 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span><span class="sxs-lookup"><span data-stu-id="13572-111">hello latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span> 
* [<span data-ttu-id="13572-112">Maven 3</span><span class="sxs-lookup"><span data-stu-id="13572-112">Maven 3</span></span>](https://maven.apache.org/install.html) 
* <span data-ttu-id="13572-113">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="13572-113">An active Azure account.</span></span> <span data-ttu-id="13572-114">(如果您沒有帳戶，只需要幾分鐘的時間就可以建立[免費帳戶][lnk-free-trial]。)</span><span class="sxs-lookup"><span data-stu-id="13572-114">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

<span data-ttu-id="13572-115">最後一個步驟中，記下 hello**主索引鍵**值。</span><span class="sxs-lookup"><span data-stu-id="13572-115">As a final step, make a note of hello **Primary key** value.</span></span> <span data-ttu-id="13572-116">然後按一下 **端點**和 hello**事件**內建端點。</span><span class="sxs-lookup"><span data-stu-id="13572-116">Then click **Endpoints** and hello **Events** built-in endpoint.</span></span> <span data-ttu-id="13572-117">在 hello**屬性**刀鋒視窗中，記下的 hello**事件中樞相容名稱**和 hello**事件中樞相容端點**位址。</span><span class="sxs-lookup"><span data-stu-id="13572-117">On hello **Properties** blade, make a note of hello **Event Hub-compatible name** and hello **Event Hub-compatible endpoint** address.</span></span> <span data-ttu-id="13572-118">在建立 **read-d2c-messages** 應用程式時需要用到這三個值。</span><span class="sxs-lookup"><span data-stu-id="13572-118">You need these three values when you create your **read-d2c-messages** app.</span></span>

![Azure 入口網站的 IoT 中樞傳訊刀鋒視窗][6]

<span data-ttu-id="13572-120">您現在已經建立 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="13572-120">You have now created your IoT hub.</span></span> <span data-ttu-id="13572-121">您有 hello IoT 中樞的主機名稱、 IoT 中樞連接字串、 IoT 中樞的主索引鍵、 事件中樞相容的名稱，以及您需要 toocomplete 本教學課程中的事件中樞相容端點。</span><span class="sxs-lookup"><span data-stu-id="13572-121">You have hello IoT Hub host name, IoT Hub connection string, IoT Hub Primary Key, Event Hub-compatible name, and Event Hub-compatible endpoint you need toocomplete this tutorial.</span></span>

## <a name="create-a-device-identity"></a><span data-ttu-id="13572-122">建立裝置識別</span><span class="sxs-lookup"><span data-stu-id="13572-122">Create a device identity</span></span>
<span data-ttu-id="13572-123">在本節中，您可以建立 IoT 中樞中的 hello 身分識別登錄中建立裝置身分識別的 Java 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="13572-123">In this section, you create a Java console app that creates a device identity in hello identity registry in your IoT hub.</span></span> <span data-ttu-id="13572-124">裝置無法連線 tooIoT 中樞，除非它有 hello 身分識別登錄中的項目。</span><span class="sxs-lookup"><span data-stu-id="13572-124">A device cannot connect tooIoT hub unless it has an entry in hello identity registry.</span></span> <span data-ttu-id="13572-125">如需詳細資訊，請參閱 hello**身分識別登錄**區段 hello [IoT 中樞開發人員指南][lnk-devguide-identity]。</span><span class="sxs-lookup"><span data-stu-id="13572-125">For more information, see hello **Identity Registry** section of hello [IoT Hub developer guide][lnk-devguide-identity].</span></span> <span data-ttu-id="13572-126">當您執行此主控台應用程式時，它會產生唯一的裝置識別碼，並傳送至雲端的裝置時，您的裝置，可以使用 tooidentify 本身的索引鍵郵件 tooIoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="13572-126">When you run this console app, it generates a unique device ID and key that your device can use tooidentify itself when it sends device-to-cloud messages tooIoT Hub.</span></span>

1. <span data-ttu-id="13572-127">建立稱為 iot-java-get-started 的空資料夾。</span><span class="sxs-lookup"><span data-stu-id="13572-127">Create an empty folder called iot-java-get-started.</span></span> <span data-ttu-id="13572-128">在 hello iot java-get-啟動資料夾中，建立名為 Maven 專案**建立裝置身分識別**使用下列命令，在您的命令提示字元的 hello。</span><span class="sxs-lookup"><span data-stu-id="13572-128">In hello iot-java-get-started folder, create a Maven project called **create-device-identity** using hello following command at your command prompt.</span></span> <span data-ttu-id="13572-129">注意，這是一個單一且非常長的命令：</span><span class="sxs-lookup"><span data-stu-id="13572-129">Note this is a single, long command:</span></span>

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=create-device-identity -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. <span data-ttu-id="13572-130">在命令提示字元中，瀏覽 toohello 建立裝置身分識別的資料夾。</span><span class="sxs-lookup"><span data-stu-id="13572-130">At your command prompt, navigate toohello create-device-identity folder.</span></span>

3. <span data-ttu-id="13572-131">使用文字編輯器，開啟 hello 建立裝置身分識別資料夾中的 hello pom.xml 檔案並新增下列相依性 toohello hello**相依性**節點。</span><span class="sxs-lookup"><span data-stu-id="13572-131">Using a text editor, open hello pom.xml file in hello create-device-identity folder and add hello following dependency toohello **dependencies** node.</span></span> <span data-ttu-id="13572-132">此相依性可讓您 toouse hello iot 服務用戶端封裝應用程式中：</span><span class="sxs-lookup"><span data-stu-id="13572-132">This dependency enables you toouse hello iot-service-client package in your app:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="13572-133">您可以檢查 hello 最新版本的**iot 服務用戶端**使用[Maven 搜尋][lnk-maven-service-search]。</span><span class="sxs-lookup"><span data-stu-id="13572-133">You can check for hello latest version of **iot-service-client** using [Maven search][lnk-maven-service-search].</span></span>

4. <span data-ttu-id="13572-134">儲存並關閉 hello pom.xml 檔案。</span><span class="sxs-lookup"><span data-stu-id="13572-134">Save and close hello pom.xml file.</span></span>

5. <span data-ttu-id="13572-135">使用文字編輯器開啟 hello create-device-identity\src\main\java\com\mycompany\app\App.java 檔案。</span><span class="sxs-lookup"><span data-stu-id="13572-135">Using a text editor, open hello create-device-identity\src\main\java\com\mycompany\app\App.java file.</span></span>

6. <span data-ttu-id="13572-136">新增下列 hello**匯入**陳述式 toohello 檔案：</span><span class="sxs-lookup"><span data-stu-id="13572-136">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;
    import com.microsoft.azure.sdk.iot.service.Device;
    import com.microsoft.azure.sdk.iot.service.RegistryManager;
   
    import java.io.IOException;
    import java.net.URISyntaxException;
    ```

7. <span data-ttu-id="13572-137">新增下列類別層級變數 toohello hello**應用程式**類別取代**{yourhubconnectionstring}** hello 值取代您記下前面：</span><span class="sxs-lookup"><span data-stu-id="13572-137">Add hello following class-level variables toohello **App** class, replacing **{yourhubconnectionstring}** with hello value your noted earlier:</span></span>

    ```java
    private static final String connectionString = "{yourhubconnectionstring}";
    private static final String deviceId = "myFirstJavaDevice";
    ```
[!INCLUDE [iot-hub-pii-note-naming-device](../../includes/iot-hub-pii-note-naming-device.md)]

8. <span data-ttu-id="13572-138">修改 hello 簽章的 hello**主要**方法 tooinclude hello 例外狀況，如下所示：</span><span class="sxs-lookup"><span data-stu-id="13572-138">Modify hello signature of hello **main** method tooinclude hello exceptions as follows:</span></span>

    ```java
    public static void main( String[] args ) throws IOException, URISyntaxException, Exception
    ```

9. <span data-ttu-id="13572-139">新增下列程式碼作為 hello hello 主體 hello**主要**方法。</span><span class="sxs-lookup"><span data-stu-id="13572-139">Add hello following code as hello body of hello **main** method.</span></span> <span data-ttu-id="13572-140">如果還沒有裝置，此程式碼會在 IoT 中樞身分識別登錄中建立名為 javadevice  的裝置。</span><span class="sxs-lookup"><span data-stu-id="13572-140">This code creates a device called *javadevice* in your IoT Hub identity registry if doesn't already exist.</span></span> <span data-ttu-id="13572-141">然後，它會顯示 hello 裝置識別碼和金鑰，您稍後需要：</span><span class="sxs-lookup"><span data-stu-id="13572-141">It then displays hello device ID and key that you need later:</span></span>

    ```java
    RegistryManager registryManager = RegistryManager.createFromConnectionString(connectionString);
RegistryManager registryManager = RegistryManager.createFromConnectionString(connectionString);

    // Create a device that's enabled by default, 
    // with an autogenerated key.
    Device device = Device.createFromId(deviceId, null, null);
    try {
      device = registryManager.addDevice(device);
    } catch (IotHubException iote) {
      // If hello device already exists.
      try {
        device = registryManager.getDevice(deviceId);
      } catch (IotHubException iotf) {
        iotf.printStackTrace();
      }
    }

    // Display information about the
    // device you created.
    System.out.println("Device Id: " + device.getDeviceId());
    System.out.println("Device key: " + device.getPrimaryKey());
    // Create a device that's enabled by default, 
    // with an autogenerated key.
    Device device = Device.createFromId(deviceId, null, null);
    try {
      device = registryManager.addDevice(device);
    } catch (IotHubException iote) {
      // If hello device already exists.
      try {
        device = registryManager.getDevice(deviceId);
      } catch (IotHubException iotf) {
        iotf.printStackTrace();
      }
    }

    // Display information about the
    // device you created.
    System.out.println("Device Id: " + device.getDeviceId());
    System.out.println("Device key: " + device.getPrimaryKey());
    ```

10. <span data-ttu-id="13572-142">儲存並關閉 hello App.java 檔案。</span><span class="sxs-lookup"><span data-stu-id="13572-142">Save and close hello App.java file.</span></span>

11. <span data-ttu-id="13572-143">toobuild hello**建立裝置身分識別**使用 Maven，應用程式執行下列命令在 hello hello 建立裝置身分識別資料夾中的命令提示字元的 hello:</span><span class="sxs-lookup"><span data-stu-id="13572-143">toobuild hello **create-device-identity** app using Maven, execute hello following command at hello command prompt in hello create-device-identity folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

12. <span data-ttu-id="13572-144">toorun hello**建立裝置身分識別**使用 Maven，應用程式執行下列命令在 hello hello 建立裝置身分識別資料夾中的命令提示字元的 hello:</span><span class="sxs-lookup"><span data-stu-id="13572-144">toorun hello **create-device-identity** app using Maven, execute hello following command at hello command prompt in hello create-device-identity folder:</span></span>

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
    ```

13. <span data-ttu-id="13572-145">請記下 hello**裝置識別碼**和**裝置金鑰**。</span><span class="sxs-lookup"><span data-stu-id="13572-145">Make a note of hello **Device ID** and **Device key**.</span></span> <span data-ttu-id="13572-146">您需要這些值稍後當您建立應用程式連接 tooIoT 為裝置的集線器。</span><span class="sxs-lookup"><span data-stu-id="13572-146">You need these values later when you create an app that connects tooIoT Hub as a device.</span></span>

> [!NOTE]
> <span data-ttu-id="13572-147">hello IoT 中樞身分識別登錄只會儲存裝置身分識別 tooenable 安全存取 toohello IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="13572-147">hello IoT Hub identity registry only stores device identities tooenable secure access toohello IoT hub.</span></span> <span data-ttu-id="13572-148">它會儲存裝置識別碼和金鑰 toouse 安全性認證以及啟用/停用旗標，您可以使用 toodisable 存取個別的裝置。</span><span class="sxs-lookup"><span data-stu-id="13572-148">It stores device IDs and keys toouse as security credentials and an enabled/disabled flag that you can use toodisable access for an individual device.</span></span> <span data-ttu-id="13572-149">如果您的應用程式需要 toostore 其他裝置專屬的中繼資料，它應該使用的應用程式而異的存放區。</span><span class="sxs-lookup"><span data-stu-id="13572-149">If your app needs toostore other device-specific metadata, it should use an app-specific store.</span></span> <span data-ttu-id="13572-150">如需詳細資訊，請參閱 hello [IoT 中樞開發人員指南][lnk-devguide-identity]。</span><span class="sxs-lookup"><span data-stu-id="13572-150">For more information, see hello [IoT Hub developer guide][lnk-devguide-identity].</span></span>

## <a name="receive-device-to-cloud-messages"></a><span data-ttu-id="13572-151">接收裝置到雲端的訊息</span><span class="sxs-lookup"><span data-stu-id="13572-151">Receive device-to-cloud messages</span></span>

<span data-ttu-id="13572-152">在本節中，您會建立 Java 主控台應用程式，以讀取來自 IoT 中樞的裝置到雲端訊息。</span><span class="sxs-lookup"><span data-stu-id="13572-152">In this section, you create a Java console app that reads device-to-cloud messages from IoT Hub.</span></span> <span data-ttu-id="13572-153">IoT 中樞公開[事件中心][lnk-event-hubs-overview]-相容的端點 tooenable 您 tooread 裝置到雲端訊息。</span><span class="sxs-lookup"><span data-stu-id="13572-153">An IoT hub exposes an [Event Hub][lnk-event-hubs-overview]-compatible endpoint tooenable you tooread device-to-cloud messages.</span></span> <span data-ttu-id="13572-154">簡單 tookeep 方面，本教學課程會建立基本的讀取器不是適用於高輸送量部署。</span><span class="sxs-lookup"><span data-stu-id="13572-154">tookeep things simple, this tutorial creates a basic reader that is not suitable for a high throughput deployment.</span></span> <span data-ttu-id="13572-155">hello[處理裝置到雲端訊息][ lnk-process-d2c-tutorial]教學課程會示範大規模 tooprocess 裝置到雲端訊息的方式。</span><span class="sxs-lookup"><span data-stu-id="13572-155">hello [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial shows you how tooprocess device-to-cloud messages at scale.</span></span> <span data-ttu-id="13572-156">hello[開始使用事件中心][ lnk-eventhubs-tutorial]教學課程提供有關 tooprocess 如何從事件中心訊息和是適用的 toohello IoT 中樞事件中樞相容的端點的進一步資訊。</span><span class="sxs-lookup"><span data-stu-id="13572-156">hello [Get Started with Event Hubs][lnk-eventhubs-tutorial] tutorial provides further information on how tooprocess messages from Event Hubs and is applicable toohello IoT Hub Event Hub-compatible endpoints.</span></span>

> [!NOTE]
> <span data-ttu-id="13572-157">hello 一律讀取裝置到雲端訊息的事件中樞相容端點使用 hello AMQP 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="13572-157">hello Event Hub-compatible endpoint for reading device-to-cloud messages always uses hello AMQP protocol.</span></span>

1. <span data-ttu-id="13572-158">您在 hello hello iot java-get-啟動資料夾中建立*建立裝置身分識別*區段中，建立名為 Maven 專案**閱讀 d2c 郵件**使用下列命令，在您的命令提示字元的 hello。</span><span class="sxs-lookup"><span data-stu-id="13572-158">In hello iot-java-get-started folder you created in hello *Create a device identity* section, create a Maven project called **read-d2c-messages** using hello following command at your command prompt.</span></span> <span data-ttu-id="13572-159">注意，這是一個單一且非常長的命令：</span><span class="sxs-lookup"><span data-stu-id="13572-159">Note this is a single, long command:</span></span>

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=read-d2c-messages -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. <span data-ttu-id="13572-160">在命令提示字元中，瀏覽 toohello 閱讀 d2c 郵件資料夾。</span><span class="sxs-lookup"><span data-stu-id="13572-160">At your command prompt, navigate toohello read-d2c-messages folder.</span></span>

3. <span data-ttu-id="13572-161">使用文字編輯器，開啟 hello 閱讀 d2c 郵件資料夾中的 hello pom.xml 檔案並新增下列相依性 toohello hello**相依性**節點。</span><span class="sxs-lookup"><span data-stu-id="13572-161">Using a text editor, open hello pom.xml file in hello read-d2c-messages folder and add hello following dependency toohello **dependencies** node.</span></span> <span data-ttu-id="13572-162">此相依性，可讓您在 hello 事件中樞相容端點從您的應用程式 tooread toouse hello eventhubs 用戶端套件：</span><span class="sxs-lookup"><span data-stu-id="13572-162">This dependency enables you toouse hello eventhubs-client package in your app tooread from hello Event Hub-compatible endpoint:</span></span>

    ```xml
    <dependency> 
        <groupId>com.microsoft.azure</groupId> 
        <artifactId>azure-eventhubs</artifactId> 
        <version>0.13.0</version> 
    </dependency>
    ```

4. <span data-ttu-id="13572-163">儲存並關閉 hello pom.xml 檔案。</span><span class="sxs-lookup"><span data-stu-id="13572-163">Save and close hello pom.xml file.</span></span>

5. <span data-ttu-id="13572-164">使用文字編輯器開啟 hello read-d2c-messages\src\main\java\com\mycompany\app\App.java 檔案。</span><span class="sxs-lookup"><span data-stu-id="13572-164">Using a text editor, open hello read-d2c-messages\src\main\java\com\mycompany\app\App.java file.</span></span>

6. <span data-ttu-id="13572-165">新增下列 hello**匯入**陳述式 toohello 檔案：</span><span class="sxs-lookup"><span data-stu-id="13572-165">Add hello following **import** statements toohello file:</span></span>

    ```java
    import java.io.IOException;
    import com.microsoft.azure.eventhubs.*;
    import com.microsoft.azure.servicebus.*;

    import java.nio.charset.Charset;
    import java.time.*;
    import java.util.function.*;
    ```

7. <span data-ttu-id="13572-166">新增下列類別層級變數 toohello hello**應用程式**類別。</span><span class="sxs-lookup"><span data-stu-id="13572-166">Add hello following class-level variable toohello **App** class.</span></span> <span data-ttu-id="13572-167">取代**{youriothubkey}**， **{youreventhubcompatibleendpoint}**，和**{youreventhubcompatiblename}**與您先前記下的 hello 值：</span><span class="sxs-lookup"><span data-stu-id="13572-167">Replace **{youriothubkey}**, **{youreventhubcompatibleendpoint}**, and **{youreventhubcompatiblename}** with hello values you noted previously:</span></span>

    ```java
    private static String connStr = "Endpoint={youreventhubcompatibleendpoint};EntityPath={youreventhubcompatiblename};SharedAccessKeyName=iothubowner;SharedAccessKey={youriothubkey}";
    ```

8. <span data-ttu-id="13572-168">新增下列 hello **receiveMessages**方法 toohello**應用程式**類別。</span><span class="sxs-lookup"><span data-stu-id="13572-168">Add hello following **receiveMessages** method toohello **App** class.</span></span> <span data-ttu-id="13572-169">這個方法會建立**EventHubClient** tooconnect toohello 事件中樞相容端點執行個體，然後以非同步方式建立**PartitionReceiver**自事件中心的執行個體 tooread資料分割。</span><span class="sxs-lookup"><span data-stu-id="13572-169">This method creates an **EventHubClient** instance tooconnect toohello Event Hub-compatible endpoint and then asynchronously creates a **PartitionReceiver** instance tooread from an Event Hub partition.</span></span> <span data-ttu-id="13572-170">它會不斷地重複，並列印 hello 訊息詳細資料，直到 hello 應用程式結束為止。</span><span class="sxs-lookup"><span data-stu-id="13572-170">It loops continuously and prints hello message details until hello app terminates.</span></span>

    ```java
    // Create a receiver on a partition.
    private static EventHubClient receiveMessages(final String partitionId) {
      EventHubClient client = null;
      try {
        client = EventHubClient.createFromConnectionStringSync(connStr);
      } catch (Exception e) {
        System.out.println("Failed toocreate client: " + e.getMessage());
        System.exit(1);
      }
      try {
        // Create a receiver using the
        // default Event Hubs consumer group
        // that listens for messages from now on.
        client.createReceiver(EventHubClient.DEFAULT_CONSUMER_GROUP_NAME, partitionId, Instant.now())
          .thenAccept(new Consumer<PartitionReceiver>() {
            public void accept(PartitionReceiver receiver) {
              System.out.println("** Created receiver on partition " + partitionId);
              try {
                while (true) {
                  Iterable<EventData> receivedEvents = receiver.receive(100).get();
                  int batchSize = 0;
                  if (receivedEvents != null) {
                    System.out.println("Got some evenst");
                    for (EventData receivedEvent : receivedEvents) {
                      System.out.println(String.format("Offset: %s, SeqNo: %s, EnqueueTime: %s",
                        receivedEvent.getSystemProperties().getOffset(),
                        receivedEvent.getSystemProperties().getSequenceNumber(),
                        receivedEvent.getSystemProperties().getEnqueuedTime()));
                      System.out.println(String.format("| Device ID: %s",
                        receivedEvent.getSystemProperties().get("iothub-connection-device-id")));
                      System.out.println(String.format("| Message Payload: %s",
                        new String(receivedEvent.getBytes(), Charset.defaultCharset())));
                      batchSize++;
                    }
                  }
                  System.out.println(String.format("Partition: %s, ReceivedBatch Size: %s", partitionId, batchSize));
                }
              } catch (Exception e) {
                System.out.println("Failed tooreceive messages: " + e.getMessage());
              }
            }
          });
        } catch (Exception e) {
          System.out.println("Failed toocreate receiver: " + e.getMessage());
      }
      return client;
    }
    ```

   > [!NOTE]
   > <span data-ttu-id="13572-171">建立 hello 接收者以便 hello 接收者只會讀取傳送的訊息 tooIoT 中樞之後 hello 接收者就可開始執行時，這個方法會使用篩選器。</span><span class="sxs-lookup"><span data-stu-id="13572-171">This method uses a filter when it creates hello receiver so that hello receiver only reads messages sent tooIoT Hub after hello receiver starts running.</span></span> <span data-ttu-id="13572-172">此技術是適用於測試環境，讓您可以查看 hello 訊息的目前資料集。</span><span class="sxs-lookup"><span data-stu-id="13572-172">This technique is useful in a test environment so you can see hello current set of messages.</span></span> <span data-ttu-id="13572-173">在實際執行環境中，您的程式碼應該確定它會處理所有的 hello 訊息-如需詳細資訊，請參閱 hello[如何 tooprocess IoT 中樞裝置到雲端訊息][ lnk-process-d2c-tutorial]教學課程。</span><span class="sxs-lookup"><span data-stu-id="13572-173">In a production environment, your code should make sure that it processes all hello messages - for more information, see hello [How tooprocess IoT Hub device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span>

9. <span data-ttu-id="13572-174">修改 hello 簽章的 hello**主要**方法 tooinclude hello 例外狀況，如下所示：</span><span class="sxs-lookup"><span data-stu-id="13572-174">Modify hello signature of hello **main** method tooinclude hello exception as follows:</span></span>

    ```java
    public static void main( String[] args ) throws IOException
    ```

10. <span data-ttu-id="13572-175">新增下列程式碼 toohello hello**主要**方法在 hello**應用程式**類別。</span><span class="sxs-lookup"><span data-stu-id="13572-175">Add hello following code toohello **main** method in hello **App** class.</span></span> <span data-ttu-id="13572-176">此程式碼會建立兩個 hello **EventHubClient**和**PartitionReceiver**執行個體，並完成處理訊息時，tooclose hello 應用程式讓您：</span><span class="sxs-lookup"><span data-stu-id="13572-176">This code creates hello two **EventHubClient** and **PartitionReceiver** instances and enables you tooclose hello app when you have finished processing messages:</span></span>

    ```java
    // Create receivers for partitions 0 and 1.
    EventHubClient client0 = receiveMessages("0");
    EventHubClient client1 = receiveMessages("1");
    System.out.println("Press ENTER tooexit.");
    System.in.read();
    try {
      client0.closeSync();
      client1.closeSync();
      System.exit(0);
    } catch (ServiceBusException sbe) {
      System.exit(1);
    }
    ```

    > [!NOTE]
    > <span data-ttu-id="13572-177">此程式碼假設您建立 IoT 中樞 hello F1 （免費） 層。</span><span class="sxs-lookup"><span data-stu-id="13572-177">This code assumes you created your IoT hub in hello F1 (free) tier.</span></span> <span data-ttu-id="13572-178">免費 IoT 中樞有 "0" 和 "1" 這兩個資料分割。</span><span class="sxs-lookup"><span data-stu-id="13572-178">A free IoT hub has two partitions named "0" and "1".</span></span>

11. <span data-ttu-id="13572-179">儲存並關閉 hello App.java 檔案。</span><span class="sxs-lookup"><span data-stu-id="13572-179">Save and close hello App.java file.</span></span>

12. <span data-ttu-id="13572-180">toobuild hello**閱讀 d2c 郵件**使用 Maven，應用程式執行下列命令在 hello hello 閱讀 d2c 郵件資料夾中的命令提示字元的 hello:</span><span class="sxs-lookup"><span data-stu-id="13572-180">toobuild hello **read-d2c-messages** app using Maven, execute hello following command at hello command prompt in hello read-d2c-messages folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="create-a-device-app"></a><span data-ttu-id="13572-181">建立裝置應用程式</span><span class="sxs-lookup"><span data-stu-id="13572-181">Create a device app</span></span>
<span data-ttu-id="13572-182">在本節中，您可以建立 Java 主控台應用程式，可以模擬傳送裝置到雲端訊息 tooan IoT 中樞的裝置。</span><span class="sxs-lookup"><span data-stu-id="13572-182">In this section, you create a Java console app that simulates a device that sends device-to-cloud messages tooan IoT hub.</span></span>

1. <span data-ttu-id="13572-183">您在 hello hello iot java-get-啟動資料夾中建立*建立裝置身分識別*區段中，建立名為 Maven 專案**模擬裝置**使用下列命令，在您的命令提示字元的 hello。</span><span class="sxs-lookup"><span data-stu-id="13572-183">In hello iot-java-get-started folder you created in hello *Create a device identity* section, create a Maven project called **simulated-device** using hello following command at your command prompt.</span></span> <span data-ttu-id="13572-184">注意，這是一個單一且非常長的命令：</span><span class="sxs-lookup"><span data-stu-id="13572-184">Note this is a single, long command:</span></span>

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. <span data-ttu-id="13572-185">在命令提示字元中，瀏覽 toohello 模擬裝置資料夾。</span><span class="sxs-lookup"><span data-stu-id="13572-185">At your command prompt, navigate toohello simulated-device folder.</span></span>

3. <span data-ttu-id="13572-186">使用文字編輯器，開啟 hello 模擬裝置資料夾中的 hello pom.xml 檔案並新增下列相依性 toohello hello**相依性**節點。</span><span class="sxs-lookup"><span data-stu-id="13572-186">Using a text editor, open hello pom.xml file in hello simulated-device folder and add hello following dependencies toohello **dependencies** node.</span></span> <span data-ttu-id="13572-187">此相依性可讓您 toouse hello iot 中樞 java 用戶端封裝您的應用程式 toocommunicate 與您的 IoT 中樞 tooserialize Java 物件 tooJSON 中：</span><span class="sxs-lookup"><span data-stu-id="13572-187">This dependency enables you toouse hello iothub-java-client package in your app toocommunicate with your IoT hub and tooserialize Java objects tooJSON:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    <dependency>
      <groupId>com.google.code.gson</groupId>
      <artifactId>gson</artifactId>
      <version>2.3.1</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="13572-188">您可以檢查 hello 最新版本的**iot 裝置用戶端**使用[Maven 搜尋][lnk-maven-device-search]。</span><span class="sxs-lookup"><span data-stu-id="13572-188">You can check for hello latest version of **iot-device-client** using [Maven search][lnk-maven-device-search].</span></span>

4. <span data-ttu-id="13572-189">儲存並關閉 hello pom.xml 檔案。</span><span class="sxs-lookup"><span data-stu-id="13572-189">Save and close hello pom.xml file.</span></span>

5. <span data-ttu-id="13572-190">使用文字編輯器開啟 hello simulated-device\src\main\java\com\mycompany\app\App.java 檔案。</span><span class="sxs-lookup"><span data-stu-id="13572-190">Using a text editor, open hello simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span>

6. <span data-ttu-id="13572-191">新增下列 hello**匯入**陳述式 toohello 檔案：</span><span class="sxs-lookup"><span data-stu-id="13572-191">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.google.gson.Gson;

    import java.io.*;
    import java.net.URISyntaxException;
    import java.util.Random;
    import java.util.concurrent.Executors;
    import java.util.concurrent.ExecutorService;
    ```

7. <span data-ttu-id="13572-192">新增下列類別層級變數 toohello hello**應用程式**類別。</span><span class="sxs-lookup"><span data-stu-id="13572-192">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="13572-193">取代**{youriothubname}**以您的 IoT 中樞名稱，和**{yourdevicekey}** hello 裝置索引鍵值中 hello 產生*建立裝置身分識別*> 一節：</span><span class="sxs-lookup"><span data-stu-id="13572-193">Replacing **{youriothubname}** with your IoT hub name, and **{yourdevicekey}** with hello device key value you generated in hello *Create a device identity* section:</span></span>

    ```java
    private static String connString = "HostName={youriothubname}.azure-devices.net;DeviceId=myFirstJavaDevice;SharedAccessKey={yourdevicekey}";
    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String deviceId = "myFirstJavaDevice";
    private static DeviceClient client;
    ```
   
    <span data-ttu-id="13572-194">此範例應用程式會使用 hello**通訊協定**變數時，它會具現化**DeviceClient**物件。</span><span class="sxs-lookup"><span data-stu-id="13572-194">This sample app uses hello **protocol** variable when it instantiates a **DeviceClient** object.</span></span> <span data-ttu-id="13572-195">您可以使用任一 hello MQTT、 AMQP 或 HTTP 通訊協定 toocommunicate 與 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="13572-195">You can use either hello MQTT, AMQP, or HTTP protocol toocommunicate with IoT Hub.</span></span>

8. <span data-ttu-id="13572-196">加入巢狀的 hello 下列**TelemetryDataPoint**內部 hello 類別**應用程式**類別 toospecify hello 遙測資料，而您的裝置傳送 tooyour IoT 中樞：</span><span class="sxs-lookup"><span data-stu-id="13572-196">Add hello following nested **TelemetryDataPoint** class inside hello **App** class toospecify hello telemetry data your device sends tooyour IoT hub:</span></span>

    ```java
    private static class TelemetryDataPoint {
      public String deviceId;
      public double temperature;
      public double humidity;
   
      public String serialize() {
        Gson gson = new Gson();
        return gson.toJson(this);
      }
    }
    ```
9. <span data-ttu-id="13572-197">加入巢狀的 hello 下列**EventCallback**內部 hello 類別**應用程式**類別 toodisplay hello 認可狀態的 hello IoT 中樞會傳回處理來自 hello 裝置應用程式的訊息時。</span><span class="sxs-lookup"><span data-stu-id="13572-197">Add hello following nested **EventCallback** class inside hello **App** class toodisplay hello acknowledgement status that hello IoT hub returns when it processes a message from hello device app.</span></span> <span data-ttu-id="13572-198">在處理 hello 訊息時，這個方法也會通知 hello 應用程式中的 hello 主執行緒：</span><span class="sxs-lookup"><span data-stu-id="13572-198">This method also notifies hello main thread in hello app when hello message has been processed:</span></span>
   
    ```java
    private static class EventCallback implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded toomessage with status: " + status.name());
   
        if (context != null) {
          synchronized (context) {
            context.notify();
          }
        }
      }
    }
    ```

10. <span data-ttu-id="13572-199">加入巢狀的 hello 下列**MessageSender**內部 hello 類別**應用程式**類別。</span><span class="sxs-lookup"><span data-stu-id="13572-199">Add hello following nested **MessageSender** class inside hello **App** class.</span></span> <span data-ttu-id="13572-200">hello**執行**此類別中的方法會產生範例遙測資料 toosend tooyour IoT 中樞，並等待傳送嗨下一個訊息之前，先通知：</span><span class="sxs-lookup"><span data-stu-id="13572-200">hello **run** method in this class generates sample telemetry data toosend tooyour IoT hub and waits for an acknowledgement before sending hello next message:</span></span>

    ```java
    private static class MessageSender implements Runnable {
      public void run()  {
        try {
          double minTemperature = 20;
          double minHumidity = 60;
          Random rand = new Random();
    
          while (true) {
            double currentTemperature = minTemperature + rand.nextDouble() * 15;
            double currentHumidity = minHumidity + rand.nextDouble() * 20;
            TelemetryDataPoint telemetryDataPoint = new TelemetryDataPoint();
            telemetryDataPoint.deviceId = deviceId;
            telemetryDataPoint.temperature = currentTemperature;
            telemetryDataPoint.humidity = currentHumidity;
    
            String msgStr = telemetryDataPoint.serialize();
            Message msg = new Message(msgStr);
            msg.setProperty("temperatureAlert", (currentTemperature > 30) ? "true" : "false");
            msg.setMessageId(java.util.UUID.randomUUID().toString()); 
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

    <span data-ttu-id="13572-201">這個方法會傳送新的裝置到雲端訊息 hello IoT 中樞確認收到 hello 前一個訊息之後的每秒。</span><span class="sxs-lookup"><span data-stu-id="13572-201">This method sends a new device-to-cloud message one second after hello IoT hub acknowledges hello previous message.</span></span> <span data-ttu-id="13572-202">hello 訊息包含與 hello deviceId JSON 序列化的物件，並隨機產生的數字 toosimulate 溫度感應器和溼度感應器。</span><span class="sxs-lookup"><span data-stu-id="13572-202">hello message contains a JSON-serialized object with hello deviceId and randomly generated numbers toosimulate a temperature sensor, and a humidity sensor.</span></span>

11. <span data-ttu-id="13572-203">取代 hello**主要**方法，以下列程式碼會建立執行緒 toosend 裝置到雲端訊息 tooyour IoT 中樞的 hello:</span><span class="sxs-lookup"><span data-stu-id="13572-203">Replace hello **main** method with hello following code that creates a thread toosend device-to-cloud messages tooyour IoT hub:</span></span>

    ```java
    public static void main( String[] args ) throws IOException, URISyntaxException {
      client = new DeviceClient(connString, protocol);
      client.open();
    
      MessageSender sender = new MessageSender();
    
      ExecutorService executor = Executors.newFixedThreadPool(1);
      executor.execute(sender);
    
      System.out.println("Press ENTER tooexit.");
      System.in.read();
      executor.shutdownNow();
      client.closeNow();
    }
    ```

12. <span data-ttu-id="13572-204">儲存並關閉 hello App.java 檔案。</span><span class="sxs-lookup"><span data-stu-id="13572-204">Save and close hello App.java file.</span></span>

13. <span data-ttu-id="13572-205">toobuild hello**模擬裝置**使用 Maven，應用程式執行下列命令在 hello hello 模擬裝置資料夾中的命令提示字元的 hello:</span><span class="sxs-lookup"><span data-stu-id="13572-205">toobuild hello **simulated-device** app using Maven, execute hello following command at hello command prompt in hello simulated-device folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

> [!NOTE]
> <span data-ttu-id="13572-206">簡單 tookeep 方面，本教學課程未實作任何重試原則。</span><span class="sxs-lookup"><span data-stu-id="13572-206">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="13572-207">在實際執行程式碼，您應該實作重試原則 （例如指數型輪詢），做為建議 hello MSDN 文件中[暫時性錯誤處理][lnk-transient-faults]。</span><span class="sxs-lookup"><span data-stu-id="13572-207">In production code, you should implement retry policies (such as an exponential backoff), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>

## <a name="run-hello-apps"></a><span data-ttu-id="13572-208">執行 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="13572-208">Run hello apps</span></span>

<span data-ttu-id="13572-209">現在您已經準備就緒 toorun hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="13572-209">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="13572-210">Hello 讀取 d2c 資料夾中的命令提示字元，執行下列命令 toobegin 監視 hello IoT 中樞中的第一個資料分割的 hello:</span><span class="sxs-lookup"><span data-stu-id="13572-210">At a command prompt in hello read-d2c folder, run hello following command toobegin monitoring hello first partition in your IoT hub:</span></span>

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
    ```

    ![Java IoT 中樞服務應用程式的 toomonitor 裝置到雲端訊息][7]

2. <span data-ttu-id="13572-212">Hello 模擬裝置資料夾中的命令提示字元，執行下列命令 toobegin 傳送遙測資料 tooyour IoT 中樞的 hello:</span><span class="sxs-lookup"><span data-stu-id="13572-212">At a command prompt in hello simulated-device folder, run hello following command toobegin sending telemetry data tooyour IoT hub:</span></span>

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App" 
    ```

    ![Java IoT 中樞裝置應用程式的 toosend 裝置到雲端訊息][8]

3. <span data-ttu-id="13572-214">hello**使用量**磚中 hello [Azure 入口網站][ lnk-portal]顯示 hello 訊息傳送 toohello IoT 中樞的數目：</span><span class="sxs-lookup"><span data-stu-id="13572-214">hello **Usage** tile in hello [Azure portal][lnk-portal] shows hello number of messages sent toohello IoT hub:</span></span>

    ![Azure 入口網站使用並排顯示的數目傳送的訊息 tooIoT 中樞][43]

## <a name="next-steps"></a><span data-ttu-id="13572-216">後續步驟</span><span class="sxs-lookup"><span data-stu-id="13572-216">Next steps</span></span>
<span data-ttu-id="13572-217">在本教學課程中，您在 hello Azure 入口網站中設定新的 IoT 中樞，並接著 hello IoT 中樞的身分識別登錄中建立裝置身分識別。</span><span class="sxs-lookup"><span data-stu-id="13572-217">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="13572-218">您已經使用此裝置身分識別 tooenable hello 裝置應用程式 toosend 裝置到雲端訊息 toohello IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="13572-218">You used this device identity tooenable hello device app toosend device-to-cloud messages toohello IoT hub.</span></span> <span data-ttu-id="13572-219">您也會建立會顯示 hello IoT 中樞收到 hello 訊息的應用程式。</span><span class="sxs-lookup"><span data-stu-id="13572-219">You also created an app that displays hello messages received by hello IoT hub.</span></span>

<span data-ttu-id="13572-220">使用者入門 toocontinue tooexplore IoT 中樞與其他 IoT 案例，請參閱：</span><span class="sxs-lookup"><span data-stu-id="13572-220">toocontinue getting started with IoT Hub and tooexplore other IoT scenarios, see:</span></span>

* <span data-ttu-id="13572-221">[連接您的裝置][lnk-connect-device]</span><span class="sxs-lookup"><span data-stu-id="13572-221">[Connecting your device][lnk-connect-device]</span></span>
* <span data-ttu-id="13572-222">[開始使用裝置管理][lnk-device-management]</span><span class="sxs-lookup"><span data-stu-id="13572-222">[Getting started with device management][lnk-device-management]</span></span>
* <span data-ttu-id="13572-223">[開始使用 Azure IoT Edge][lnk-iot-edge]</span><span class="sxs-lookup"><span data-stu-id="13572-223">[Getting started with Azure IoT Edge][lnk-iot-edge]</span></span>

<span data-ttu-id="13572-224">toolearn 如何 tooextend 您 IoT 方案和程序裝置到雲端訊息在小數位數，請參閱 hello[處理裝置到雲端訊息][ lnk-process-d2c-tutorial]教學課程。</span><span class="sxs-lookup"><span data-stu-id="13572-224">toolearn how tooextend your IoT solution and process device-to-cloud messages at scale, see hello [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span>
[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

<!-- Images. -->
[6]: ./media/iot-hub-java-java-getstarted/create-iot-hub6.png
[7]: ./media/iot-hub-java-java-getstarted/runapp1.png
[8]: ./media/iot-hub-java-java-getstarted/runapp2.png
[43]: ./media/iot-hub-java-java-getstarted/usage.png

<!-- Links -->
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-eventhubs-tutorial]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-devguide-identity]: iot-hub-devguide-identity-registry.md
[lnk-event-hubs-overview]: ../event-hubs/event-hubs-overview.md
[lnk-process-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal]: https://portal.azure.com/

[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/
[lnk-maven-service-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22
[lnk-maven-device-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22
[lnk-maven-eventhubs-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22
