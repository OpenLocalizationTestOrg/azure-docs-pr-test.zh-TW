---
title: "開始使用 Azure IoT 中樞 (Java) | Microsoft Docs"
description: "了解如何使用適用於 Java 的 IoT SDK 將裝置到雲端訊息傳送至 Azure IoT 中樞。 建立模擬裝置和服務應用程式來註冊您的裝置、傳送訊息，並從 IoT 中樞讀取訊息。"
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
ms.openlocfilehash: 707356a49970bcd76a55ee1b8a6fbddf6a6ba390
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="connect-your-device-to-your-iot-hub-using-java"></a><span data-ttu-id="de1a8-104">使用 Java 將您的裝置連線至 IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="de1a8-104">Connect your device to your IoT hub using Java</span></span>
[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

<span data-ttu-id="de1a8-105">在本教學課程結尾處，您會有三個 Java 主控台應用程式：</span><span class="sxs-lookup"><span data-stu-id="de1a8-105">At the end of this tutorial, you have three Java console apps:</span></span>

* <span data-ttu-id="de1a8-106">**create-device-identity**，這會建立裝置身分識別和相關聯的安全性金鑰，以連線到您的裝置應用程式。</span><span class="sxs-lookup"><span data-stu-id="de1a8-106">**create-device-identity**, which creates a device identity and associated security key to connect your device app.</span></span>
* <span data-ttu-id="de1a8-107">**read-d2c-messages**，其中顯示裝置應用程式所傳送的遙測。</span><span class="sxs-lookup"><span data-stu-id="de1a8-107">**read-d2c-messages**, which displays the telemetry sent by your device app.</span></span>
* <span data-ttu-id="de1a8-108">**simulated-device**，這會使用先前建立的裝置身分識別連接到您的 IoT 中樞，並使用 MQTT 通訊協定每秒傳送遙測訊息。</span><span class="sxs-lookup"><span data-stu-id="de1a8-108">**simulated-device**, which connects to your IoT hub with the device identity created earlier, and sends a telemetry message every second using the MQTT protocol.</span></span>

> [!NOTE]
> <span data-ttu-id="de1a8-109">[Azure IoT SDK][lnk-hub-sdks] 一文提供 Azure IoT SDK (可讓您同時建置在裝置與您的解決方案後端執行的兩個應用程式) 的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="de1a8-109">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both apps to run on devices and your solution back end.</span></span>

<span data-ttu-id="de1a8-110">若要完成此教學課程，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="de1a8-110">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="de1a8-111">最新的 [Java SE 開發套件 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span><span class="sxs-lookup"><span data-stu-id="de1a8-111">The latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span> 
* [<span data-ttu-id="de1a8-112">Maven 3</span><span class="sxs-lookup"><span data-stu-id="de1a8-112">Maven 3</span></span>](https://maven.apache.org/install.html) 
* <span data-ttu-id="de1a8-113">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="de1a8-113">An active Azure account.</span></span> <span data-ttu-id="de1a8-114">(如果您沒有帳戶，只需要幾分鐘的時間就可以建立[免費帳戶][lnk-free-trial]。)</span><span class="sxs-lookup"><span data-stu-id="de1a8-114">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

<span data-ttu-id="de1a8-115">最後一個步驟，記下**主要金鑰**值。</span><span class="sxs-lookup"><span data-stu-id="de1a8-115">As a final step, make a note of the **Primary key** value.</span></span> <span data-ttu-id="de1a8-116">然後按一下 [端點] 和 [事件] 內建端點。</span><span class="sxs-lookup"><span data-stu-id="de1a8-116">Then click **Endpoints** and the **Events** built-in endpoint.</span></span> <span data-ttu-id="de1a8-117">記下 [屬性] 刀鋒視窗上的 [事件中樞相容名稱] 和 [事件中樞相容端點] 位址。</span><span class="sxs-lookup"><span data-stu-id="de1a8-117">On the **Properties** blade, make a note of the **Event Hub-compatible name** and the **Event Hub-compatible endpoint** address.</span></span> <span data-ttu-id="de1a8-118">在建立 **read-d2c-messages** 應用程式時需要用到這三個值。</span><span class="sxs-lookup"><span data-stu-id="de1a8-118">You need these three values when you create your **read-d2c-messages** app.</span></span>

![Azure 入口網站的 IoT 中樞傳訊刀鋒視窗][6]

<span data-ttu-id="de1a8-120">您現在已經建立 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="de1a8-120">You have now created your IoT hub.</span></span> <span data-ttu-id="de1a8-121">您擁有完成本教學課程所需的 IoT 中樞主機名稱、IoT 中樞連接字串、IoT 中樞主要金鑰、事件中樞相容名稱和事件中樞相容端點。</span><span class="sxs-lookup"><span data-stu-id="de1a8-121">You have the IoT Hub host name, IoT Hub connection string, IoT Hub Primary Key, Event Hub-compatible name, and Event Hub-compatible endpoint you need to complete this tutorial.</span></span>

## <a name="create-a-device-identity"></a><span data-ttu-id="de1a8-122">建立裝置識別</span><span class="sxs-lookup"><span data-stu-id="de1a8-122">Create a device identity</span></span>
<span data-ttu-id="de1a8-123">在本節中，您會建立 Java 主控台應用程式，它會在 IoT 中樞的身分識別登錄中建立裝置識別。</span><span class="sxs-lookup"><span data-stu-id="de1a8-123">In this section, you create a Java console app that creates a device identity in the identity registry in your IoT hub.</span></span> <span data-ttu-id="de1a8-124">裝置無法連線到 IoT 中樞，除非它在身分識別登錄中具有項目。</span><span class="sxs-lookup"><span data-stu-id="de1a8-124">A device cannot connect to IoT hub unless it has an entry in the identity registry.</span></span> <span data-ttu-id="de1a8-125">如需詳細資訊，請參閱 [IoT 中樞開發人員指南][lnk-devguide-identity]的＜身分識別登錄＞一節。</span><span class="sxs-lookup"><span data-stu-id="de1a8-125">For more information, see the **Identity Registry** section of the [IoT Hub developer guide][lnk-devguide-identity].</span></span> <span data-ttu-id="de1a8-126">執行這個主控台應用程式時，它會產生唯一的裝置識別碼及金鑰，當裝置向 IoT 中樞傳送裝置對雲端訊息時，可以用來識別裝置本身。</span><span class="sxs-lookup"><span data-stu-id="de1a8-126">When you run this console app, it generates a unique device ID and key that your device can use to identify itself when it sends device-to-cloud messages to IoT Hub.</span></span>

1. <span data-ttu-id="de1a8-127">建立稱為 iot-java-get-started 的空資料夾。</span><span class="sxs-lookup"><span data-stu-id="de1a8-127">Create an empty folder called iot-java-get-started.</span></span> <span data-ttu-id="de1a8-128">在 iot-java-get-started 資料夾的命令提示字元下，使用下列命令建立名為 **create-device-identity** 的 Maven 專案。</span><span class="sxs-lookup"><span data-stu-id="de1a8-128">In the iot-java-get-started folder, create a Maven project called **create-device-identity** using the following command at your command prompt.</span></span> <span data-ttu-id="de1a8-129">注意，這是一個單一且非常長的命令：</span><span class="sxs-lookup"><span data-stu-id="de1a8-129">Note this is a single, long command:</span></span>

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=create-device-identity -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. <span data-ttu-id="de1a8-130">在命令提示字元中，瀏覽到 create-device-identity 資料夾。</span><span class="sxs-lookup"><span data-stu-id="de1a8-130">At your command prompt, navigate to the create-device-identity folder.</span></span>

3. <span data-ttu-id="de1a8-131">使用文字編輯器，在 create-device-identity 資料夾中開啟 pom.xml 檔案，並對 [相依性]  節點新增下列相依性。</span><span class="sxs-lookup"><span data-stu-id="de1a8-131">Using a text editor, open the pom.xml file in the create-device-identity folder and add the following dependency to the **dependencies** node.</span></span> <span data-ttu-id="de1a8-132">這個相依性可讓您在應用程式中使用 iot-service-client 套件：</span><span class="sxs-lookup"><span data-stu-id="de1a8-132">This dependency enables you to use the iot-service-client package in your app:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="de1a8-133">您可以使用 [Maven 搜尋][lnk-maven-service-search]來檢查最新版的 **iot-service-client**。</span><span class="sxs-lookup"><span data-stu-id="de1a8-133">You can check for the latest version of **iot-service-client** using [Maven search][lnk-maven-service-search].</span></span>

4. <span data-ttu-id="de1a8-134">儲存並關閉 pom.xml 檔案。</span><span class="sxs-lookup"><span data-stu-id="de1a8-134">Save and close the pom.xml file.</span></span>

5. <span data-ttu-id="de1a8-135">使用文字編輯器開啟 create-device-identity\src\main\java\com\mycompany\app\App.java 檔案。</span><span class="sxs-lookup"><span data-stu-id="de1a8-135">Using a text editor, open the create-device-identity\src\main\java\com\mycompany\app\App.java file.</span></span>

6. <span data-ttu-id="de1a8-136">在此檔案中新增下列 **import** 陳述式：</span><span class="sxs-lookup"><span data-stu-id="de1a8-136">Add the following **import** statements to the file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;
    import com.microsoft.azure.sdk.iot.service.Device;
    import com.microsoft.azure.sdk.iot.service.RegistryManager;
   
    import java.io.IOException;
    import java.net.URISyntaxException;
    ```

7. <span data-ttu-id="de1a8-137">將下列類別層級變數新增至 [應用程式] 類別，並以您稍早記下的值取代 **{yourhubconnectionstring}**：</span><span class="sxs-lookup"><span data-stu-id="de1a8-137">Add the following class-level variables to the **App** class, replacing **{yourhubconnectionstring}** with the value your noted earlier:</span></span>

    ```java
    private static final String connectionString = "{yourhubconnectionstring}";
    private static final String deviceId = "myFirstJavaDevice";
    ```
[!INCLUDE [iot-hub-pii-note-naming-device](../../includes/iot-hub-pii-note-naming-device.md)]

8. <span data-ttu-id="de1a8-138">修改 **main** 方法的簽章以新增如下所示的例外狀況：</span><span class="sxs-lookup"><span data-stu-id="de1a8-138">Modify the signature of the **main** method to include the exceptions as follows:</span></span>

    ```java
    public static void main( String[] args ) throws IOException, URISyntaxException, Exception
    ```

9. <span data-ttu-id="de1a8-139">新增下列程式碼作為 **main** 方法的主體。</span><span class="sxs-lookup"><span data-stu-id="de1a8-139">Add the following code as the body of the **main** method.</span></span> <span data-ttu-id="de1a8-140">如果還沒有裝置，此程式碼會在 IoT 中樞身分識別登錄中建立名為 javadevice  的裝置。</span><span class="sxs-lookup"><span data-stu-id="de1a8-140">This code creates a device called *javadevice* in your IoT Hub identity registry if doesn't already exist.</span></span> <span data-ttu-id="de1a8-141">然後它會顯示稍後需要用到的裝置識別碼和金鑰：</span><span class="sxs-lookup"><span data-stu-id="de1a8-141">It then displays the device ID and key that you need later:</span></span>

    ```java
    RegistryManager registryManager = RegistryManager.createFromConnectionString(connectionString);
RegistryManager registryManager = RegistryManager.createFromConnectionString(connectionString);

    // Create a device that's enabled by default, 
    // with an autogenerated key.
    Device device = Device.createFromId(deviceId, null, null);
    try {
      device = registryManager.addDevice(device);
    } catch (IotHubException iote) {
      // If the device already exists.
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
      // If the device already exists.
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

10. <span data-ttu-id="de1a8-142">儲存並關閉 App.java 檔案。</span><span class="sxs-lookup"><span data-stu-id="de1a8-142">Save and close the App.java file.</span></span>

11. <span data-ttu-id="de1a8-143">若要使用 Maven 建置 **create-device-identity** 應用程式，請在命令提示字元中的 create-device-identity 資料夾內執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="de1a8-143">To build the **create-device-identity** app using Maven, execute the following command at the command prompt in the create-device-identity folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

12. <span data-ttu-id="de1a8-144">若要使用 Maven 執行 **create-device-identity** 應用程式，請在命令提示字元中的 create-device-identity 資料夾內執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="de1a8-144">To run the **create-device-identity** app using Maven, execute the following command at the command prompt in the create-device-identity folder:</span></span>

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
    ```

13. <span data-ttu-id="de1a8-145">記下**裝置識別碼**和**裝置金鑰**。</span><span class="sxs-lookup"><span data-stu-id="de1a8-145">Make a note of the **Device ID** and **Device key**.</span></span> <span data-ttu-id="de1a8-146">稍後在建立連線至作為裝置之 IoT 中樞的應用程式時，您會需要這些值。</span><span class="sxs-lookup"><span data-stu-id="de1a8-146">You need these values later when you create an app that connects to IoT Hub as a device.</span></span>

> [!NOTE]
> <span data-ttu-id="de1a8-147">IoT 中樞身分識別登錄只會儲存裝置身分識別，以啟用對 IoT 中樞的安全存取。</span><span class="sxs-lookup"><span data-stu-id="de1a8-147">The IoT Hub identity registry only stores device identities to enable secure access to the IoT hub.</span></span> <span data-ttu-id="de1a8-148">它會儲存裝置識別碼和金鑰來作為安全性認證，以及啟用或停用旗標，讓您用來停用個別裝置的存取。</span><span class="sxs-lookup"><span data-stu-id="de1a8-148">It stores device IDs and keys to use as security credentials and an enabled/disabled flag that you can use to disable access for an individual device.</span></span> <span data-ttu-id="de1a8-149">如果您的應用程式需要儲存其他裝置特定中繼資料，它應該使用應用程式特定存放區。</span><span class="sxs-lookup"><span data-stu-id="de1a8-149">If your app needs to store other device-specific metadata, it should use an app-specific store.</span></span> <span data-ttu-id="de1a8-150">如需詳細資訊，請參閱 [IoT 中樞開發人員指南][lnk-devguide-identity]。</span><span class="sxs-lookup"><span data-stu-id="de1a8-150">For more information, see the [IoT Hub developer guide][lnk-devguide-identity].</span></span>

## <a name="receive-device-to-cloud-messages"></a><span data-ttu-id="de1a8-151">接收裝置到雲端的訊息</span><span class="sxs-lookup"><span data-stu-id="de1a8-151">Receive device-to-cloud messages</span></span>

<span data-ttu-id="de1a8-152">在本節中，您會建立 Java 主控台應用程式，以讀取來自 IoT 中樞的裝置到雲端訊息。</span><span class="sxs-lookup"><span data-stu-id="de1a8-152">In this section, you create a Java console app that reads device-to-cloud messages from IoT Hub.</span></span> <span data-ttu-id="de1a8-153">IoT 中樞會公開與[事件中樞][lnk-event-hubs-overview]相容的端點，讓您讀取裝置到雲端訊息。</span><span class="sxs-lookup"><span data-stu-id="de1a8-153">An IoT hub exposes an [Event Hub][lnk-event-hubs-overview]-compatible endpoint to enable you to read device-to-cloud messages.</span></span> <span data-ttu-id="de1a8-154">為了簡單起見，本教學課程會建立的基本讀取器不適合用於高輸送量部署。</span><span class="sxs-lookup"><span data-stu-id="de1a8-154">To keep things simple, this tutorial creates a basic reader that is not suitable for a high throughput deployment.</span></span> <span data-ttu-id="de1a8-155">[處理裝置到雲端訊息][lnk-process-d2c-tutorial]教學課程會說明如何大規模處理裝置到雲端訊息。</span><span class="sxs-lookup"><span data-stu-id="de1a8-155">The [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial shows you how to process device-to-cloud messages at scale.</span></span> <span data-ttu-id="de1a8-156">[開始使用事件中樞][lnk-eventhubs-tutorial]教學課程提供進一步的資訊，說明如何處理來自事件中樞的訊息，而且此教學課程也適用於 IoT 中樞事件中樞相容端點。</span><span class="sxs-lookup"><span data-stu-id="de1a8-156">The [Get Started with Event Hubs][lnk-eventhubs-tutorial] tutorial provides further information on how to process messages from Event Hubs and is applicable to the IoT Hub Event Hub-compatible endpoints.</span></span>

> [!NOTE]
> <span data-ttu-id="de1a8-157">用於讀取裝置到雲端訊息的事件中樞相容端點一律會使用 AMQP 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="de1a8-157">The Event Hub-compatible endpoint for reading device-to-cloud messages always uses the AMQP protocol.</span></span>

1. <span data-ttu-id="de1a8-158">在「建立裝置識別」一節所建立的 iot-java-get-started 資料夾中，於命令提示字元下使用下列命令建立名為 **read-d2c-messages** 的 Maven 專案。</span><span class="sxs-lookup"><span data-stu-id="de1a8-158">In the iot-java-get-started folder you created in the *Create a device identity* section, create a Maven project called **read-d2c-messages** using the following command at your command prompt.</span></span> <span data-ttu-id="de1a8-159">注意，這是一個單一且非常長的命令：</span><span class="sxs-lookup"><span data-stu-id="de1a8-159">Note this is a single, long command:</span></span>

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=read-d2c-messages -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. <span data-ttu-id="de1a8-160">在命令提示字元中，瀏覽到 read-d2c-messages 資料夾。</span><span class="sxs-lookup"><span data-stu-id="de1a8-160">At your command prompt, navigate to the read-d2c-messages folder.</span></span>

3. <span data-ttu-id="de1a8-161">使用文字編輯器，在 read-d2c-messages 資料夾中開啟 pom.xml 檔案，並對 [相依性]  節點新增下列相依性。</span><span class="sxs-lookup"><span data-stu-id="de1a8-161">Using a text editor, open the pom.xml file in the read-d2c-messages folder and add the following dependency to the **dependencies** node.</span></span> <span data-ttu-id="de1a8-162">這個相依性可讓您在應用程式中使用 eventhubs-client 套件，以從事件中樞相容端點進行讀取：</span><span class="sxs-lookup"><span data-stu-id="de1a8-162">This dependency enables you to use the eventhubs-client package in your app to read from the Event Hub-compatible endpoint:</span></span>

    ```xml
    <dependency> 
        <groupId>com.microsoft.azure</groupId> 
        <artifactId>azure-eventhubs</artifactId> 
        <version>0.13.0</version> 
    </dependency>
    ```

4. <span data-ttu-id="de1a8-163">儲存並關閉 pom.xml 檔案。</span><span class="sxs-lookup"><span data-stu-id="de1a8-163">Save and close the pom.xml file.</span></span>

5. <span data-ttu-id="de1a8-164">使用文字編輯器開啟 read-d2c-messages\src\main\java\com\mycompany\app\App.java 檔案。</span><span class="sxs-lookup"><span data-stu-id="de1a8-164">Using a text editor, open the read-d2c-messages\src\main\java\com\mycompany\app\App.java file.</span></span>

6. <span data-ttu-id="de1a8-165">在此檔案中新增下列 **import** 陳述式：</span><span class="sxs-lookup"><span data-stu-id="de1a8-165">Add the following **import** statements to the file:</span></span>

    ```java
    import java.io.IOException;
    import com.microsoft.azure.eventhubs.*;
    import com.microsoft.azure.servicebus.*;

    import java.nio.charset.Charset;
    import java.time.*;
    import java.util.function.*;
    ```

7. <span data-ttu-id="de1a8-166">將下列類別層級變數新增到 **App** 類別中。</span><span class="sxs-lookup"><span data-stu-id="de1a8-166">Add the following class-level variable to the **App** class.</span></span> <span data-ttu-id="de1a8-167">以先前記下的值取代 **{youriothubkey}**、**{youreventhubcompatibleendpoint}** 和 **{youreventhubcompatiblename}**：</span><span class="sxs-lookup"><span data-stu-id="de1a8-167">Replace **{youriothubkey}**, **{youreventhubcompatibleendpoint}**, and **{youreventhubcompatiblename}** with the values you noted previously:</span></span>

    ```java
    private static String connStr = "Endpoint={youreventhubcompatibleendpoint};EntityPath={youreventhubcompatiblename};SharedAccessKeyName=iothubowner;SharedAccessKey={youriothubkey}";
    ```

8. <span data-ttu-id="de1a8-168">在 **App** 類別中新增下列 **receiveMessages** 方法。</span><span class="sxs-lookup"><span data-stu-id="de1a8-168">Add the following **receiveMessages** method to the **App** class.</span></span> <span data-ttu-id="de1a8-169">這個方法會建立 **EventHubClient** 執行個體以連線至事件中樞相容的端點，然後以非同步方式建立 **PartitionReceiver** 執行個體以讀取事件中樞資料分割。</span><span class="sxs-lookup"><span data-stu-id="de1a8-169">This method creates an **EventHubClient** instance to connect to the Event Hub-compatible endpoint and then asynchronously creates a **PartitionReceiver** instance to read from an Event Hub partition.</span></span> <span data-ttu-id="de1a8-170">它會不斷地重複，並列印訊息的詳細資料，直到應用程式終止為止。</span><span class="sxs-lookup"><span data-stu-id="de1a8-170">It loops continuously and prints the message details until the app terminates.</span></span>

    ```java
    // Create a receiver on a partition.
    private static EventHubClient receiveMessages(final String partitionId) {
      EventHubClient client = null;
      try {
        client = EventHubClient.createFromConnectionStringSync(connStr);
      } catch (Exception e) {
        System.out.println("Failed to create client: " + e.getMessage());
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
                System.out.println("Failed to receive messages: " + e.getMessage());
              }
            }
          });
        } catch (Exception e) {
          System.out.println("Failed to create receiver: " + e.getMessage());
      }
      return client;
    }
    ```

   > [!NOTE]
   > <span data-ttu-id="de1a8-171">在建立開始執行後只會讀取傳送到 IoT 中樞之訊息的收件者時，這個方法會使用篩選器。</span><span class="sxs-lookup"><span data-stu-id="de1a8-171">This method uses a filter when it creates the receiver so that the receiver only reads messages sent to IoT Hub after the receiver starts running.</span></span> <span data-ttu-id="de1a8-172">這項技術很適合測試環境，因為如此一來您就可以看到目前的訊息集。</span><span class="sxs-lookup"><span data-stu-id="de1a8-172">This technique is useful in a test environment so you can see the current set of messages.</span></span> <span data-ttu-id="de1a8-173">在生產環境中，您的程式碼應該要確定它能處理所有訊息；如需詳細資訊，請參閱[如何處理 IoT 中樞裝置到雲端訊息][lnk-process-d2c-tutorial]教學課程。</span><span class="sxs-lookup"><span data-stu-id="de1a8-173">In a production environment, your code should make sure that it processes all the messages - for more information, see the [How to process IoT Hub device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span>

9. <span data-ttu-id="de1a8-174">修改 **main** 方法的簽章，以新增如下所示的例外狀況：</span><span class="sxs-lookup"><span data-stu-id="de1a8-174">Modify the signature of the **main** method to include the exception as follows:</span></span>

    ```java
    public static void main( String[] args ) throws IOException
    ```

10. <span data-ttu-id="de1a8-175">在 **App** 類別中對 **main** 方法新增下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="de1a8-175">Add the following code to the **main** method in the **App** class.</span></span> <span data-ttu-id="de1a8-176">此程式碼會建立兩個 **EventHubClient** 與 **PartitionReceiver** 執行個體，並可讓您在訊息處理完成時關閉應用程式︰</span><span class="sxs-lookup"><span data-stu-id="de1a8-176">This code creates the two **EventHubClient** and **PartitionReceiver** instances and enables you to close the app when you have finished processing messages:</span></span>

    ```java
    // Create receivers for partitions 0 and 1.
    EventHubClient client0 = receiveMessages("0");
    EventHubClient client1 = receiveMessages("1");
    System.out.println("Press ENTER to exit.");
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
    > <span data-ttu-id="de1a8-177">此程式碼假設您已在 F1 (免費) 層建立 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="de1a8-177">This code assumes you created your IoT hub in the F1 (free) tier.</span></span> <span data-ttu-id="de1a8-178">免費 IoT 中樞有 "0" 和 "1" 這兩個資料分割。</span><span class="sxs-lookup"><span data-stu-id="de1a8-178">A free IoT hub has two partitions named "0" and "1".</span></span>

11. <span data-ttu-id="de1a8-179">儲存並關閉 App.java 檔案。</span><span class="sxs-lookup"><span data-stu-id="de1a8-179">Save and close the App.java file.</span></span>

12. <span data-ttu-id="de1a8-180">若要使用 Maven 建置 **read-d2c-messages** 應用程式，請在命令提示字元中的 read-d2c-messages 資料夾內執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="de1a8-180">To build the **read-d2c-messages** app using Maven, execute the following command at the command prompt in the read-d2c-messages folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="create-a-device-app"></a><span data-ttu-id="de1a8-181">建立裝置應用程式</span><span class="sxs-lookup"><span data-stu-id="de1a8-181">Create a device app</span></span>
<span data-ttu-id="de1a8-182">在本節中，您會撰寫 Java 主控台應用程式，模擬裝置傳送裝置對雲端訊息至 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="de1a8-182">In this section, you create a Java console app that simulates a device that sends device-to-cloud messages to an IoT hub.</span></span>

1. <span data-ttu-id="de1a8-183">在「建立裝置識別」一節所建立的 iot-java-get-started 資料夾中，於命令提示字元下使用下列命令建立稱為 **simulated-device** 的 Maven 專案。</span><span class="sxs-lookup"><span data-stu-id="de1a8-183">In the iot-java-get-started folder you created in the *Create a device identity* section, create a Maven project called **simulated-device** using the following command at your command prompt.</span></span> <span data-ttu-id="de1a8-184">注意，這是一個單一且非常長的命令：</span><span class="sxs-lookup"><span data-stu-id="de1a8-184">Note this is a single, long command:</span></span>

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. <span data-ttu-id="de1a8-185">在命令提示字元中，瀏覽到 simulated-device 資料夾。</span><span class="sxs-lookup"><span data-stu-id="de1a8-185">At your command prompt, navigate to the simulated-device folder.</span></span>

3. <span data-ttu-id="de1a8-186">使用文字編輯器，在 simulated-device 資料夾中開啟 pom.xml 檔案，並對 [相依性]  節點新增下列相依性。</span><span class="sxs-lookup"><span data-stu-id="de1a8-186">Using a text editor, open the pom.xml file in the simulated-device folder and add the following dependencies to the **dependencies** node.</span></span> <span data-ttu-id="de1a8-187">這個相依性可讓您在應用程式中使用 iothub-java-client 套件與 IoT 中樞通訊，以及將 Java 物件序列化為 JSON：</span><span class="sxs-lookup"><span data-stu-id="de1a8-187">This dependency enables you to use the iothub-java-client package in your app to communicate with your IoT hub and to serialize Java objects to JSON:</span></span>

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
    > <span data-ttu-id="de1a8-188">您可以使用 [Maven 搜尋][lnk-maven-device-search]來檢查最新版的 **iot-device-client**。</span><span class="sxs-lookup"><span data-stu-id="de1a8-188">You can check for the latest version of **iot-device-client** using [Maven search][lnk-maven-device-search].</span></span>

4. <span data-ttu-id="de1a8-189">儲存並關閉 pom.xml 檔案。</span><span class="sxs-lookup"><span data-stu-id="de1a8-189">Save and close the pom.xml file.</span></span>

5. <span data-ttu-id="de1a8-190">使用文字編輯器開啟 simulated-device\src\main\java\com\mycompany\app\App.java 檔案。</span><span class="sxs-lookup"><span data-stu-id="de1a8-190">Using a text editor, open the simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span>

6. <span data-ttu-id="de1a8-191">在此檔案中新增下列 **import** 陳述式：</span><span class="sxs-lookup"><span data-stu-id="de1a8-191">Add the following **import** statements to the file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.google.gson.Gson;

    import java.io.*;
    import java.net.URISyntaxException;
    import java.util.Random;
    import java.util.concurrent.Executors;
    import java.util.concurrent.ExecutorService;
    ```

7. <span data-ttu-id="de1a8-192">將下列類別層級變數新增到 **App** 類別中。</span><span class="sxs-lookup"><span data-stu-id="de1a8-192">Add the following class-level variables to the **App** class.</span></span> <span data-ttu-id="de1a8-193">將 **{youriothubname}** 取代為 IoT 中樞名稱，並將 **{yourdevicekey}** 取代為您在「建立裝置識別」一節中產生的裝置金鑰值：</span><span class="sxs-lookup"><span data-stu-id="de1a8-193">Replacing **{youriothubname}** with your IoT hub name, and **{yourdevicekey}** with the device key value you generated in the *Create a device identity* section:</span></span>

    ```java
    private static String connString = "HostName={youriothubname}.azure-devices.net;DeviceId=myFirstJavaDevice;SharedAccessKey={yourdevicekey}";
    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String deviceId = "myFirstJavaDevice";
    private static DeviceClient client;
    ```
   
    <span data-ttu-id="de1a8-194">此範例應用程式在具現化 **DeviceClient** 物件時使用 **protocol** 變數。</span><span class="sxs-lookup"><span data-stu-id="de1a8-194">This sample app uses the **protocol** variable when it instantiates a **DeviceClient** object.</span></span> <span data-ttu-id="de1a8-195">您可以使用 MQTT、AMQP 或 HTTP 通訊協定與 IoT 中樞進行通訊。</span><span class="sxs-lookup"><span data-stu-id="de1a8-195">You can use either the MQTT, AMQP, or HTTP protocol to communicate with IoT Hub.</span></span>

8. <span data-ttu-id="de1a8-196">在 **App** 類別內新增下列巢狀 **TelemetryDataPoint** 類別，以指定裝置傳送至 IoT 中樞的遙測資料：</span><span class="sxs-lookup"><span data-stu-id="de1a8-196">Add the following nested **TelemetryDataPoint** class inside the **App** class to specify the telemetry data your device sends to your IoT hub:</span></span>

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
9. <span data-ttu-id="de1a8-197">在 **App** 類別內新增下列巢狀 **EventCallback** 類別，以顯示 IoT 中樞在處理來自裝置應用程式的訊息時，所傳回的認可狀態。</span><span class="sxs-lookup"><span data-stu-id="de1a8-197">Add the following nested **EventCallback** class inside the **App** class to display the acknowledgement status that the IoT hub returns when it processes a message from the device app.</span></span> <span data-ttu-id="de1a8-198">這個方法也會在處理訊息時通知應用程式中的主執行緒：</span><span class="sxs-lookup"><span data-stu-id="de1a8-198">This method also notifies the main thread in the app when the message has been processed:</span></span>
   
    ```java
    private static class EventCallback implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded to message with status: " + status.name());
   
        if (context != null) {
          synchronized (context) {
            context.notify();
          }
        }
      }
    }
    ```

10. <span data-ttu-id="de1a8-199">在 **App** 類別中新增下列巢狀 **MessageSender** 類別。</span><span class="sxs-lookup"><span data-stu-id="de1a8-199">Add the following nested **MessageSender** class inside the **App** class.</span></span> <span data-ttu-id="de1a8-200">此類別中的 **run** 方法會產生範例遙測資料以傳送至 IoT 中樞，並先等待認可再傳送下一則訊息：</span><span class="sxs-lookup"><span data-stu-id="de1a8-200">The **run** method in this class generates sample telemetry data to send to your IoT hub and waits for an acknowledgement before sending the next message:</span></span>

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

    <span data-ttu-id="de1a8-201">這個方法會在 IoT 中樞認可先前的訊息一秒後，傳送新的裝置到雲端訊息。</span><span class="sxs-lookup"><span data-stu-id="de1a8-201">This method sends a new device-to-cloud message one second after the IoT hub acknowledges the previous message.</span></span> <span data-ttu-id="de1a8-202">此訊息包含 JSON 序列化物件及裝置識別碼與隨機產生的數字，以模擬溫度感應器和溼度感應器。</span><span class="sxs-lookup"><span data-stu-id="de1a8-202">The message contains a JSON-serialized object with the deviceId and randomly generated numbers to simulate a temperature sensor, and a humidity sensor.</span></span>

11. <span data-ttu-id="de1a8-203">將 **main** 方法取代為下列程式碼，以建立執行緒來將裝置到雲端訊息傳送至 IoT 中樞：</span><span class="sxs-lookup"><span data-stu-id="de1a8-203">Replace the **main** method with the following code that creates a thread to send device-to-cloud messages to your IoT hub:</span></span>

    ```java
    public static void main( String[] args ) throws IOException, URISyntaxException {
      client = new DeviceClient(connString, protocol);
      client.open();
    
      MessageSender sender = new MessageSender();
    
      ExecutorService executor = Executors.newFixedThreadPool(1);
      executor.execute(sender);
    
      System.out.println("Press ENTER to exit.");
      System.in.read();
      executor.shutdownNow();
      client.closeNow();
    }
    ```

12. <span data-ttu-id="de1a8-204">儲存並關閉 App.java 檔案。</span><span class="sxs-lookup"><span data-stu-id="de1a8-204">Save and close the App.java file.</span></span>

13. <span data-ttu-id="de1a8-205">若要使用 Maven 建置 **simulated-device** 應用程式，請在命令提示字元中的 simulated-device 資料夾內執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="de1a8-205">To build the **simulated-device** app using Maven, execute the following command at the command prompt in the simulated-device folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

> [!NOTE]
> <span data-ttu-id="de1a8-206">為了簡單起見，本教學課程不會實作任何重試原則。</span><span class="sxs-lookup"><span data-stu-id="de1a8-206">To keep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="de1a8-207">在實際程式碼中，您應該如 MSDN 文章[暫時性錯誤處理][lnk-transient-faults]所建議，實作重試原則 (例如指數型輪詢)。</span><span class="sxs-lookup"><span data-stu-id="de1a8-207">In production code, you should implement retry policies (such as an exponential backoff), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>

## <a name="run-the-apps"></a><span data-ttu-id="de1a8-208">執行應用程式</span><span class="sxs-lookup"><span data-stu-id="de1a8-208">Run the apps</span></span>

<span data-ttu-id="de1a8-209">您現在可以開始執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="de1a8-209">You are now ready to run the apps.</span></span>

1. <span data-ttu-id="de1a8-210">在 read-d2c 資料夾的命令提示字元中，執行下列命令以開始監視 IoT 中樞內的第一個資料分割：</span><span class="sxs-lookup"><span data-stu-id="de1a8-210">At a command prompt in the read-d2c folder, run the following command to begin monitoring the first partition in your IoT hub:</span></span>

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
    ```

    ![用來監視裝置到雲端訊息的 Java IoT 中樞服務應用程式][7]

2. <span data-ttu-id="de1a8-212">在 simulated-device 資料夾的命令提示字元中，執行下列命令以開始將遙測資料傳送至 IoT 中樞：</span><span class="sxs-lookup"><span data-stu-id="de1a8-212">At a command prompt in the simulated-device folder, run the following command to begin sending telemetry data to your IoT hub:</span></span>

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App" 
    ```

    ![用來傳送裝置到雲端訊息的 Java IoT 中樞裝置應用程式][8]

3. <span data-ttu-id="de1a8-214">[Azure 入口網站][lnk-portal]中的 [使用量] 圖格會顯示傳送至 IoT 中樞的訊息數目︰</span><span class="sxs-lookup"><span data-stu-id="de1a8-214">The **Usage** tile in the [Azure portal][lnk-portal] shows the number of messages sent to the IoT hub:</span></span>

    ![顯示傳送到 IoT 中樞之訊息數目的 Azure 入口網站使用量圖格][43]

## <a name="next-steps"></a><span data-ttu-id="de1a8-216">後續步驟</span><span class="sxs-lookup"><span data-stu-id="de1a8-216">Next steps</span></span>
<span data-ttu-id="de1a8-217">在此教學課程中，您在 Azure 入口網站中設定了新的 IoT 中樞，然後在 IoT 中樞的身分識別登錄中建立了裝置身分識別。</span><span class="sxs-lookup"><span data-stu-id="de1a8-217">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="de1a8-218">您會將此裝置身分識別用於啟用裝置應用程式，以將裝置到雲端訊息傳送至 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="de1a8-218">You used this device identity to enable the device app to send device-to-cloud messages to the IoT hub.</span></span> <span data-ttu-id="de1a8-219">您也會建立一個應用程式來顯示 IoT 中樞所接收的訊息。</span><span class="sxs-lookup"><span data-stu-id="de1a8-219">You also created an app that displays the messages received by the IoT hub.</span></span>

<span data-ttu-id="de1a8-220">若要繼續開始使用 IoT 中樞並瀏覽其他 IoT 案例，請參閱︰</span><span class="sxs-lookup"><span data-stu-id="de1a8-220">To continue getting started with IoT Hub and to explore other IoT scenarios, see:</span></span>

* <span data-ttu-id="de1a8-221">[連接您的裝置][lnk-connect-device]</span><span class="sxs-lookup"><span data-stu-id="de1a8-221">[Connecting your device][lnk-connect-device]</span></span>
* <span data-ttu-id="de1a8-222">[開始使用裝置管理][lnk-device-management]</span><span class="sxs-lookup"><span data-stu-id="de1a8-222">[Getting started with device management][lnk-device-management]</span></span>
* <span data-ttu-id="de1a8-223">[開始使用 Azure IoT Edge][lnk-iot-edge]</span><span class="sxs-lookup"><span data-stu-id="de1a8-223">[Getting started with Azure IoT Edge][lnk-iot-edge]</span></span>

<span data-ttu-id="de1a8-224">若要了解如何擴充您的 IoT 解決方案及大規模處理裝置到雲端訊息，請參閱[處理裝置到雲端訊息][lnk-process-d2c-tutorial]教學課程。</span><span class="sxs-lookup"><span data-stu-id="de1a8-224">To learn how to extend your IoT solution and process device-to-cloud messages at scale, see the [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span>
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
