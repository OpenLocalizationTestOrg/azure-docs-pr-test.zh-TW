---
title: "開始使用 Azure IoT 中樞裝置管理 (Java) | Microsoft Docs"
description: "如何使用 Azure IoT 中樞裝置管理來起始遠端裝置重新開機。 您可以使用適用於 Java 的 Azure IoT 裝置 SDK，實作模擬的裝置應用程式 (包含直接方法)，也可以使用適用於 Java 的 Azure IoT 服務 SDK，實作服務應用程式 (叫用直接方法)。"
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
ms.openlocfilehash: c75635f366f5ced4bf91792d1a905dd6aab8ed79
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-device-management-java"></a><span data-ttu-id="c7209-104">開始使用裝置管理 (Java)</span><span class="sxs-lookup"><span data-stu-id="c7209-104">Get started with device management (Java)</span></span>

[!INCLUDE [iot-hub-selector-dm-getstarted](../../includes/iot-hub-selector-dm-getstarted.md)]

<span data-ttu-id="c7209-105">本教學課程說明如何：</span><span class="sxs-lookup"><span data-stu-id="c7209-105">This tutorial shows you how to:</span></span>

* <span data-ttu-id="c7209-106">使用 Azure 入口網站來建立 IoT 中樞，並且在 IoT 中樞建立裝置識別。</span><span class="sxs-lookup"><span data-stu-id="c7209-106">Use the Azure portal to create an IoT Hub and create a device identity in your IoT hub.</span></span>
* <span data-ttu-id="c7209-107">建立模擬的裝置應用程式，以實作重新啟動裝置的直接方法。</span><span class="sxs-lookup"><span data-stu-id="c7209-107">Create a simulated device app that implements a direct method to reboot the device.</span></span> <span data-ttu-id="c7209-108">直接方法是從雲端叫用。</span><span class="sxs-lookup"><span data-stu-id="c7209-108">Direct methods are invoked from the cloud.</span></span>
* <span data-ttu-id="c7209-109">建立應用程式，以透過您的 IoT 中樞在模擬的裝置應用程式中叫用 reboot 直接方法。</span><span class="sxs-lookup"><span data-stu-id="c7209-109">Create an app that invokes the reboot direct method in the simulated device app through your IoT hub.</span></span> <span data-ttu-id="c7209-110">此應用程式會接著監視從裝置回報的屬性，以查看何時完成重新開機作業。</span><span class="sxs-lookup"><span data-stu-id="c7209-110">This app then monitors the reported properties from the device to see when the reboot operation is complete.</span></span>

<span data-ttu-id="c7209-111">在本教學課程結尾處，您會有兩個 Java 主控台應用程式：</span><span class="sxs-lookup"><span data-stu-id="c7209-111">At the end of this tutorial, you have two Java console apps:</span></span>

<span data-ttu-id="c7209-112">**simulated-device**。</span><span class="sxs-lookup"><span data-stu-id="c7209-112">**simulated-device**.</span></span> <span data-ttu-id="c7209-113">此應用程式會：</span><span class="sxs-lookup"><span data-stu-id="c7209-113">This app:</span></span>

* <span data-ttu-id="c7209-114">使用稍早建立的裝置識別連線到您的 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="c7209-114">Connects to your IoT hub with the device identity created earlier.</span></span>
* <span data-ttu-id="c7209-115">收到 reboot 直接方法呼叫。</span><span class="sxs-lookup"><span data-stu-id="c7209-115">Receives a reboot direct method call.</span></span>
* <span data-ttu-id="c7209-116">模擬實體重新開機。</span><span class="sxs-lookup"><span data-stu-id="c7209-116">Simulates a physical reboot.</span></span>
* <span data-ttu-id="c7209-117">透過回報屬性報告上次重新開機的時間。</span><span class="sxs-lookup"><span data-stu-id="c7209-117">Reports the time of the last reboot through a reported property.</span></span>

<span data-ttu-id="c7209-118">**trigger-reboot**。</span><span class="sxs-lookup"><span data-stu-id="c7209-118">**trigger-reboot**.</span></span> <span data-ttu-id="c7209-119">此應用程式會：</span><span class="sxs-lookup"><span data-stu-id="c7209-119">This app:</span></span>

* <span data-ttu-id="c7209-120">在模擬的裝置應用程式中呼叫直接方法。</span><span class="sxs-lookup"><span data-stu-id="c7209-120">Calls a direct method in the simulated device app.</span></span>
* <span data-ttu-id="c7209-121">顯示對模擬的裝置所傳送之直接方法呼叫的回應</span><span class="sxs-lookup"><span data-stu-id="c7209-121">Displays the response to the direct method call sent by the simulated device</span></span>
* <span data-ttu-id="c7209-122">顯示更新的回報屬性。</span><span class="sxs-lookup"><span data-stu-id="c7209-122">Displays the updated reported properties.</span></span>

> [!NOTE]
> <span data-ttu-id="c7209-123">如需可用來建置應用程式，以在裝置與您的解決方案後端執行之 SDK 的資訊，請參閱 [Azure IoT SDK][lnk-hub-sdks]。</span><span class="sxs-lookup"><span data-stu-id="c7209-123">For information about the SDKs that you can use to build applications to run on devices and your solution back end, see [Azure IoT SDKs][lnk-hub-sdks].</span></span>

<span data-ttu-id="c7209-124">若要完成本教學課程，您需要：</span><span class="sxs-lookup"><span data-stu-id="c7209-124">To complete this tutorial, you need:</span></span>

* <span data-ttu-id="c7209-125">Java SE 8。</span><span class="sxs-lookup"><span data-stu-id="c7209-125">Java SE 8.</span></span> <br/> <span data-ttu-id="c7209-126">[準備您的開發環境][lnk-dev-setup]說明如何在 Windows 或 Linux 上安裝本教學課程的 Java。</span><span class="sxs-lookup"><span data-stu-id="c7209-126">[Prepare your development environment][lnk-dev-setup] describes how to install Java for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="c7209-127">Maven 3。</span><span class="sxs-lookup"><span data-stu-id="c7209-127">Maven 3.</span></span>  <br/> <span data-ttu-id="c7209-128">[準備您的開發環境][lnk-dev-setup]說明如何在 Windows 或 Linux 上安裝本教學課程的 [Maven][lnk-maven]。</span><span class="sxs-lookup"><span data-stu-id="c7209-128">[Prepare your development environment][lnk-dev-setup] describes how to install [Maven][lnk-maven] for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="c7209-129">[Node.js 版本 0.10.0 或更新版本](http://nodejs.org)。</span><span class="sxs-lookup"><span data-stu-id="c7209-129">[Node.js version 0.10.0 or later](http://nodejs.org).</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-reboot-on-the-device-using-a-direct-method"></a><span data-ttu-id="c7209-130">使用直接方法在裝置上觸發遠端重新啟動</span><span class="sxs-lookup"><span data-stu-id="c7209-130">Trigger a remote reboot on the device using a direct method</span></span>

<span data-ttu-id="c7209-131">在本節中，您將建立 Java 主控台應用程式以：</span><span class="sxs-lookup"><span data-stu-id="c7209-131">In this section, you create a Java console app that:</span></span>

1. <span data-ttu-id="c7209-132">在模擬的裝置應用程式中叫用 reboot 直接方法。</span><span class="sxs-lookup"><span data-stu-id="c7209-132">Invokes the reboot direct method in the simulated device app.</span></span>
1. <span data-ttu-id="c7209-133">顯示回應。</span><span class="sxs-lookup"><span data-stu-id="c7209-133">Displays the response.</span></span>
1. <span data-ttu-id="c7209-134">輪詢從裝置傳送的回報屬性，來判斷何時完成重新開機。</span><span class="sxs-lookup"><span data-stu-id="c7209-134">Polls the reported properties sent from the device to determine when the reboot is complete.</span></span>

<span data-ttu-id="c7209-135">此主控台應用程式會連線到您的 IoT 中樞來叫用直接方法，並讀取回報屬性。</span><span class="sxs-lookup"><span data-stu-id="c7209-135">This console app connects to your IoT Hub to invoke the direct method and read the reported properties.</span></span>

1. <span data-ttu-id="c7209-136">建立稱為 dm-get-started 的空資料夾。</span><span class="sxs-lookup"><span data-stu-id="c7209-136">Create an empty folder called dm-get-started.</span></span>

1. <span data-ttu-id="c7209-137">在 dm-get-started 資料夾的命令提示字元下，使用下列命令建立名為 **trigger-reboot** 的 Maven 專案。</span><span class="sxs-lookup"><span data-stu-id="c7209-137">In the dm-get-started folder, create a Maven project called **trigger-reboot** using the following command at your command prompt.</span></span> <span data-ttu-id="c7209-138">以下顯示完整的單一命令：</span><span class="sxs-lookup"><span data-stu-id="c7209-138">The following shows a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=trigger-reboot -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="c7209-139">在命令提示字元中，巡覽至 trigger-reboot 資料夾。</span><span class="sxs-lookup"><span data-stu-id="c7209-139">At your command prompt, navigate to the trigger-reboot folder.</span></span>

1. <span data-ttu-id="c7209-140">使用文字編輯器，在 trigger-reboot 資料夾中開啟 pom.xml 檔案，並對 [相依性] 節點新增下列相依性。</span><span class="sxs-lookup"><span data-stu-id="c7209-140">Using a text editor, open the pom.xml file in the trigger-reboot folder and add the following dependency to the **dependencies** node.</span></span> <span data-ttu-id="c7209-141">這個相依性可讓您在應用程式中使用 iot-service-client 套件與 IoT 中樞通訊：</span><span class="sxs-lookup"><span data-stu-id="c7209-141">This dependency enables you to use the iot-service-client package in your app to communicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
      <type>jar</type>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="c7209-142">您可以使用 [Maven 搜尋][lnk-maven-service-search]來檢查最新版的 **iot-service-client**。</span><span class="sxs-lookup"><span data-stu-id="c7209-142">You can check for the latest version of **iot-service-client** using [Maven search][lnk-maven-service-search].</span></span>

1. <span data-ttu-id="c7209-143">將下列 [建置] 節點新增至 [相依性] 節點之後。</span><span class="sxs-lookup"><span data-stu-id="c7209-143">Add the following **build** node after the **dependencies** node.</span></span> <span data-ttu-id="c7209-144">此設定會指示 Maven 使用 Java 1.8 來建置應用程式：</span><span class="sxs-lookup"><span data-stu-id="c7209-144">This configuration instructs Maven to use Java 1.8 to build the app:</span></span>

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

1. <span data-ttu-id="c7209-145">儲存並關閉 pom.xml 檔案。</span><span class="sxs-lookup"><span data-stu-id="c7209-145">Save and close the pom.xml file.</span></span>

1. <span data-ttu-id="c7209-146">使用文字編輯器開啟 trigger-reboot\src\main\java\com\mycompany\app\App.java 來源檔案。</span><span class="sxs-lookup"><span data-stu-id="c7209-146">Using a text editor, open the trigger-reboot\src\main\java\com\mycompany\app\App.java source file.</span></span>

1. <span data-ttu-id="c7209-147">在此檔案中新增下列 **import** 陳述式：</span><span class="sxs-lookup"><span data-stu-id="c7209-147">Add the following **import** statements to the file:</span></span>

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

1. <span data-ttu-id="c7209-148">將下列類別層級變數新增到 **App** 類別中。</span><span class="sxs-lookup"><span data-stu-id="c7209-148">Add the following class-level variables to the **App** class.</span></span> <span data-ttu-id="c7209-149">以您在＜建立 IoT 中樞＞一節中所記下的 IoT 中樞連接字串取代 `{youriothubconnectionstring}`：</span><span class="sxs-lookup"><span data-stu-id="c7209-149">Replace `{youriothubconnectionstring}` with your IoT hub connection string you noted in the *Create an IoT Hub* section:</span></span>

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    private static final String methodName = "reboot";
    private static final Long responseTimeout = TimeUnit.SECONDS.toSeconds(30);
    private static final Long connectTimeout = TimeUnit.SECONDS.toSeconds(5);
    ```

1. <span data-ttu-id="c7209-150">若要實作執行緒以每隔 10 秒從裝置對應項讀取回報屬性，請將下列巢狀類別新增至 **App** 類別：</span><span class="sxs-lookup"><span data-stu-id="c7209-150">To implement a thread that reads the reported properties from the device twin every 10 seconds, add the following nested class to the **App** class:</span></span>

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

1. <span data-ttu-id="c7209-151">若要在模擬的裝置上叫用 reboot 直接方法，請將下列程式碼新增至 **main** 方法：</span><span class="sxs-lookup"><span data-stu-id="c7209-151">To invoke the reboot direct method on the simulated device, add the following code to the **main** method:</span></span>

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

1. <span data-ttu-id="c7209-152">若要啟動執行緒以從模擬的裝置輪詢回報屬性，請將下列程式碼新增至 **main** 方法：</span><span class="sxs-lookup"><span data-stu-id="c7209-152">To start the thread to poll the reported properties from the simulated device, add the following code to the **main** method:</span></span>

    ```java
    ShowReportedProperties showReportedProperties = new ShowReportedProperties();
    ExecutorService executor = Executors.newFixedThreadPool(1);
    executor.execute(showReportedProperties);
    ```

1. <span data-ttu-id="c7209-153">若要讓您停止應用程式，請將下列程式碼新增至 **main** 方法：</span><span class="sxs-lookup"><span data-stu-id="c7209-153">To enable you to stop the app, add the following code to the **main** method:</span></span>

    ```java
    System.out.println("Press ENTER to exit.");
    System.in.read();
    executor.shutdownNow();
    System.out.println("Shutting down sample...");
    ```

1. <span data-ttu-id="c7209-154">儲存並關閉 trigger-reboot\src\main\java\com\mycompany\app\App.java 檔案。</span><span class="sxs-lookup"><span data-stu-id="c7209-154">Save and close the trigger-reboot\src\main\java\com\mycompany\app\App.java file.</span></span>

1. <span data-ttu-id="c7209-155">建置 **trigger-reboot** 後端應用程式，並更正任何錯誤。</span><span class="sxs-lookup"><span data-stu-id="c7209-155">Build the **trigger-reboot** back-end app and correct any errors.</span></span> <span data-ttu-id="c7209-156">在命令提示字元中，巡覽至 trigger-reboot 資料夾，並執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="c7209-156">At your command prompt, navigate to the trigger-reboot folder and run the following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="c7209-157">建立模擬裝置應用程式</span><span class="sxs-lookup"><span data-stu-id="c7209-157">Create a simulated device app</span></span>

<span data-ttu-id="c7209-158">在本節中，您將建立模擬裝置的 Java 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="c7209-158">In this section, you create a Java console app that simulates a device.</span></span> <span data-ttu-id="c7209-159">此應用程式會從您的 IoT 中樞接聽 reboot 直接方法呼叫，並立即回應該呼叫。</span><span class="sxs-lookup"><span data-stu-id="c7209-159">The app listens for the reboot direct method call from your IoT hub and immediately responds to that call.</span></span> <span data-ttu-id="c7209-160">然後會休眠一段時間，以模擬重新開機程序，再使用回報屬性來通知 **trigger-reboot** 後端應用程式重新開機已完成。</span><span class="sxs-lookup"><span data-stu-id="c7209-160">The app then sleeps for a while to simulate the reboot process before it uses a reported property to notify the **trigger-reboot** back-end app that the reboot is complete.</span></span>

1. <span data-ttu-id="c7209-161">在 dm-get-started 資料夾的命令提示字元下，使用下列命令建立名為 **simulated-device** 的 Maven 專案。</span><span class="sxs-lookup"><span data-stu-id="c7209-161">In the dm-get-started folder, create a Maven project called **simulated-device** using the following command at your command prompt.</span></span> <span data-ttu-id="c7209-162">以下是完整的單一命令：</span><span class="sxs-lookup"><span data-stu-id="c7209-162">The following is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="c7209-163">在命令提示字元中，瀏覽到 simulated-device 資料夾。</span><span class="sxs-lookup"><span data-stu-id="c7209-163">At your command prompt, navigate to the simulated-device folder.</span></span>

1. <span data-ttu-id="c7209-164">使用文字編輯器，在 simulated-device 資料夾中開啟 pom.xml 檔案，並對 [相依性] 節點新增下列相依性。</span><span class="sxs-lookup"><span data-stu-id="c7209-164">Using a text editor, open the pom.xml file in the simulated-device folder and add the following dependency to the **dependencies** node.</span></span> <span data-ttu-id="c7209-165">這個相依性可讓您在應用程式中使用 iot-service-client 套件與 IoT 中樞通訊：</span><span class="sxs-lookup"><span data-stu-id="c7209-165">This dependency enables you to use the iot-service-client package in your app to communicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="c7209-166">您可以使用 [Maven 搜尋][lnk-maven-device-search]來檢查最新版的 **iot-device-client**。</span><span class="sxs-lookup"><span data-stu-id="c7209-166">You can check for the latest version of **iot-device-client** using [Maven search][lnk-maven-device-search].</span></span>

1. <span data-ttu-id="c7209-167">將下列 [建置] 節點新增至 [相依性] 節點之後。</span><span class="sxs-lookup"><span data-stu-id="c7209-167">Add the following **build** node after the **dependencies** node.</span></span> <span data-ttu-id="c7209-168">此設定會指示 Maven 使用 Java 1.8 來建置應用程式：</span><span class="sxs-lookup"><span data-stu-id="c7209-168">This configuration instructs Maven to use Java 1.8 to build the app:</span></span>

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

1. <span data-ttu-id="c7209-169">儲存並關閉 pom.xml 檔案。</span><span class="sxs-lookup"><span data-stu-id="c7209-169">Save and close the pom.xml file.</span></span>

1. <span data-ttu-id="c7209-170">使用文字編輯器開啟 simulated-device\src\main\java\com\mycompany\app\App.java 來源檔案。</span><span class="sxs-lookup"><span data-stu-id="c7209-170">Using a text editor, open the simulated-device\src\main\java\com\mycompany\app\App.java source file.</span></span>

1. <span data-ttu-id="c7209-171">在此檔案中新增下列 **import** 陳述式：</span><span class="sxs-lookup"><span data-stu-id="c7209-171">Add the following **import** statements to the file:</span></span>

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

1. <span data-ttu-id="c7209-172">將下列類別層級變數新增到 **App** 類別中。</span><span class="sxs-lookup"><span data-stu-id="c7209-172">Add the following class-level variables to the **App** class.</span></span> <span data-ttu-id="c7209-173">將 `{yourdeviceconnectionstring}` 取代為您在＜建立裝置身分識別＞一節中所記下的裝置連接字串：</span><span class="sxs-lookup"><span data-stu-id="c7209-173">Replace `{yourdeviceconnectionstring}` with the device connection string you noted in the *Create a device identity* section:</span></span>

    ```java
    private static final int METHOD_SUCCESS = 200;
    private static final int METHOD_NOT_DEFINED = 404;

    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String connString = "{yourdeviceconnectionstring}";
    private static DeviceClient client;
    ```

1. <span data-ttu-id="c7209-174">若要實作直接方法狀態事件的回呼處理常式，請將下列巢狀類別新增至 **App** 類別：</span><span class="sxs-lookup"><span data-stu-id="c7209-174">To implement a callback handler for direct method status events, add the following nested class to the **App** class:</span></span>

    ```java
    protected static class DirectMethodStatusCallback implements IotHubEventCallback
    {
      public void execute(IotHubStatusCode status, Object context)
      {
        System.out.println("IoT Hub responded to device method operation with status " + status.name());
      }
    }
    ```

1. <span data-ttu-id="c7209-175">若要實作裝置對應項狀態事件的回呼處理常式，請將下列巢狀類別新增至 **App** 類別：</span><span class="sxs-lookup"><span data-stu-id="c7209-175">To implement a callback handler for device twin status events, add the following nested class to the **App** class:</span></span>

    ```java
    protected static class DeviceTwinStatusCallback implements IotHubEventCallback
    {
        public void execute(IotHubStatusCode status, Object context)
        {
            System.out.println("IoT Hub responded to device twin operation with status " + status.name());
        }
    }
    ```

1. <span data-ttu-id="c7209-176">若要實作屬性事件的回呼處理常式，請將下列巢狀類別新增至 **App** 類別：</span><span class="sxs-lookup"><span data-stu-id="c7209-176">To implement a callback handler for property events, add the following nested class to the **App** class:</span></span>

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

1. <span data-ttu-id="c7209-177">若要實作執行緒以模擬裝置重新開機，請將下列巢狀類別新增至 **App** 類別。</span><span class="sxs-lookup"><span data-stu-id="c7209-177">To implement a thread to simulate the device reboot, add the following nested class to the **App** class.</span></span> <span data-ttu-id="c7209-178">此執行緒會休眠五秒，再設定 **lastReboot** 回報屬性：</span><span class="sxs-lookup"><span data-stu-id="c7209-178">The thread sleeps for five seconds and then sets the **lastReboot** reported property:</span></span>

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

1. <span data-ttu-id="c7209-179">若要在裝置上實作直接方法，請將下列巢狀類別新增至 **App** 類別。</span><span class="sxs-lookup"><span data-stu-id="c7209-179">To implement the direct method on the device, add the following nested class to the **App** class.</span></span> <span data-ttu-id="c7209-180">當模擬的應用程式收到 **reboot** 直接方法的呼叫時，它會傳回通知給呼叫者，然後啟動執行緒以處理重新開機：</span><span class="sxs-lookup"><span data-stu-id="c7209-180">When the simulated app receives a call to the **reboot** direct method, it returns an acknowledgement to the caller and then starts a thread to process the reboot:</span></span>

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

1. <span data-ttu-id="c7209-181">修改 **main** 方法的簽章以擲回下列例外狀況：</span><span class="sxs-lookup"><span data-stu-id="c7209-181">Modify the signature of the **main** method to throw the following exceptions:</span></span>

    ```java
    public static void main(String[] args) throws IOException, URISyntaxException
    ```

1. <span data-ttu-id="c7209-182">若要具現化 **main** 方法，請將下列程式碼新增至 **DeviceClient**：</span><span class="sxs-lookup"><span data-stu-id="c7209-182">To instantiate a **DeviceClient**, add the following code to the **main** method:</span></span>

    ```java
    System.out.println("Starting device client sample...");
    client = new DeviceClient(connString, protocol);
    ```

1. <span data-ttu-id="c7209-183">若要開始接聽直接方法呼叫，請將下列程式碼新增至 **main** 方法：</span><span class="sxs-lookup"><span data-stu-id="c7209-183">To start listening for direct method calls, add the following code to the **main** method:</span></span>

    ```java
    try
    {
      client.open();
      client.subscribeToDeviceMethod(new DirectMethodCallback(), null, new DirectMethodStatusCallback(), null);
      client.startDeviceTwin(new DeviceTwinStatusCallback(), null, new PropertyCallback(), null);
      System.out.println("Subscribed to direct methods and polling for reported properties. Waiting...");
    }
    catch (Exception e)
    {
      System.out.println("On exception, shutting down \n" + " Cause: " + e.getCause() + " \n" +  e.getMessage());
      client.close();
      System.out.println("Shutting down...");
    }
    ```

1. <span data-ttu-id="c7209-184">若要關閉裝置模擬器，請將下列程式碼新增至 **main** 方法：</span><span class="sxs-lookup"><span data-stu-id="c7209-184">To shut down the device simulator, add the following code to the **main** method:</span></span>

    ```java
    System.out.println("Press any key to exit...");
    Scanner scanner = new Scanner(System.in);
    scanner.nextLine();
    scanner.close();
    client.close();
    System.out.println("Shutting down...");
    ```

1. <span data-ttu-id="c7209-185">儲存並關閉 simulated-device\src\main\java\com\mycompany\app\App.java 檔案。</span><span class="sxs-lookup"><span data-stu-id="c7209-185">Save and close the simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span>

1. <span data-ttu-id="c7209-186">建置 **simulated-device** 後端應用程式，並更正所有錯誤。</span><span class="sxs-lookup"><span data-stu-id="c7209-186">Build the **simulated-device** back-end app and correct any errors.</span></span> <span data-ttu-id="c7209-187">在命令提示字元中，瀏覽到 simulated-device 資料夾，並執行下列命令︰</span><span class="sxs-lookup"><span data-stu-id="c7209-187">At your command prompt, navigate to the simulated-device folder and run the following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="run-the-apps"></a><span data-ttu-id="c7209-188">執行應用程式</span><span class="sxs-lookup"><span data-stu-id="c7209-188">Run the apps</span></span>

<span data-ttu-id="c7209-189">您現在可以開始執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="c7209-189">You are now ready to run the apps.</span></span>

1. <span data-ttu-id="c7209-190">在 simulated-device 資料夾的命令提示字元中，執行下列命令以開始接聽來自您 IoT 中樞的 reboot 方法呼叫：</span><span class="sxs-lookup"><span data-stu-id="c7209-190">At a command prompt in the simulated-device folder, run the following command to begin listening for reboot method calls from your IoT hub:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![會接聽 reboot 直接方法呼叫的 Java IoT 中樞模擬裝置應用程式][1]

1. <span data-ttu-id="c7209-192">在 trigger-reboot 資料夾的命令提示字元中，執行下列命令以呼叫您模擬裝置上來自 IoT 中樞的 reboot 方法：</span><span class="sxs-lookup"><span data-stu-id="c7209-192">At a command prompt in the trigger-reboot folder, run the following command to call the reboot method on your simulated device from your IoT hub:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![會呼叫 reboot 直接方法的 Java IoT 中樞服務應用程式][2]

1. <span data-ttu-id="c7209-194">會回應 reboot 直接方法呼叫的模擬裝置：</span><span class="sxs-lookup"><span data-stu-id="c7209-194">The simulated device responds to the reboot direct method call:</span></span>

    ![Java IoT 中樞模擬裝置會回應直接方法呼叫][3]

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