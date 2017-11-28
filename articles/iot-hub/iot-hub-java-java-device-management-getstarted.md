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
# <a name="get-started-with-device-management-java"></a><span data-ttu-id="20f92-104">開始使用裝置管理 (Java)</span><span class="sxs-lookup"><span data-stu-id="20f92-104">Get started with device management (Java)</span></span>

[!INCLUDE [iot-hub-selector-dm-getstarted](../../includes/iot-hub-selector-dm-getstarted.md)]

<span data-ttu-id="20f92-105">本教學課程說明如何：</span><span class="sxs-lookup"><span data-stu-id="20f92-105">This tutorial shows you how to:</span></span>

* <span data-ttu-id="20f92-106">使用 hello Azure 入口網站 toocreate IoT 中樞，並在您的 IoT 中樞中建立裝置身分識別。</span><span class="sxs-lookup"><span data-stu-id="20f92-106">Use hello Azure portal toocreate an IoT Hub and create a device identity in your IoT hub.</span></span>
* <span data-ttu-id="20f92-107">建立實作直接方法 tooreboot hello 裝置模擬的裝置應用程式。</span><span class="sxs-lookup"><span data-stu-id="20f92-107">Create a simulated device app that implements a direct method tooreboot hello device.</span></span> <span data-ttu-id="20f92-108">直接的方法會叫用從 hello 雲端。</span><span class="sxs-lookup"><span data-stu-id="20f92-108">Direct methods are invoked from hello cloud.</span></span>
* <span data-ttu-id="20f92-109">建立會叫用 hello 重新開機直接方法 hello 模擬的裝置的應用程式透過您的 IoT 中樞中的應用程式。</span><span class="sxs-lookup"><span data-stu-id="20f92-109">Create an app that invokes hello reboot direct method in hello simulated device app through your IoT hub.</span></span> <span data-ttu-id="20f92-110">此應用程式然後 hello 報告的屬性，與 hello 裝置 toosee hello 重新開機作業完成時的監視。</span><span class="sxs-lookup"><span data-stu-id="20f92-110">This app then monitors hello reported properties from hello device toosee when hello reboot operation is complete.</span></span>

<span data-ttu-id="20f92-111">在本教學課程的 hello 最後，您有兩個 Java 主控台應用程式：</span><span class="sxs-lookup"><span data-stu-id="20f92-111">At hello end of this tutorial, you have two Java console apps:</span></span>

<span data-ttu-id="20f92-112">**simulated-device**。</span><span class="sxs-lookup"><span data-stu-id="20f92-112">**simulated-device**.</span></span> <span data-ttu-id="20f92-113">此應用程式會：</span><span class="sxs-lookup"><span data-stu-id="20f92-113">This app:</span></span>

* <span data-ttu-id="20f92-114">使用先前建立的 hello 裝置身分識別連接 tooyour IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="20f92-114">Connects tooyour IoT hub with hello device identity created earlier.</span></span>
* <span data-ttu-id="20f92-115">收到 reboot 直接方法呼叫。</span><span class="sxs-lookup"><span data-stu-id="20f92-115">Receives a reboot direct method call.</span></span>
* <span data-ttu-id="20f92-116">模擬實體重新開機。</span><span class="sxs-lookup"><span data-stu-id="20f92-116">Simulates a physical reboot.</span></span>
* <span data-ttu-id="20f92-117">報表 hello hello 透過報告屬性上次重新開機的時間。</span><span class="sxs-lookup"><span data-stu-id="20f92-117">Reports hello time of hello last reboot through a reported property.</span></span>

<span data-ttu-id="20f92-118">**trigger-reboot**。</span><span class="sxs-lookup"><span data-stu-id="20f92-118">**trigger-reboot**.</span></span> <span data-ttu-id="20f92-119">此應用程式會：</span><span class="sxs-lookup"><span data-stu-id="20f92-119">This app:</span></span>

* <span data-ttu-id="20f92-120">會呼叫 hello 模擬的裝置應用程式中直接的方法。</span><span class="sxs-lookup"><span data-stu-id="20f92-120">Calls a direct method in hello simulated device app.</span></span>
* <span data-ttu-id="20f92-121">顯示 hello 模擬的裝置所傳送的 hello 回應 toohello 直接方法呼叫</span><span class="sxs-lookup"><span data-stu-id="20f92-121">Displays hello response toohello direct method call sent by hello simulated device</span></span>
* <span data-ttu-id="20f92-122">顯示 hello 更新所報告的屬性。</span><span class="sxs-lookup"><span data-stu-id="20f92-122">Displays hello updated reported properties.</span></span>

> [!NOTE]
> <span data-ttu-id="20f92-123">如需您可以在裝置和您的方案後端上使用 toobuild 應用程式 toorun 的 hello Sdk 資訊，請參閱[Azure IoT Sdk][lnk-hub-sdks]。</span><span class="sxs-lookup"><span data-stu-id="20f92-123">For information about hello SDKs that you can use toobuild applications toorun on devices and your solution back end, see [Azure IoT SDKs][lnk-hub-sdks].</span></span>

<span data-ttu-id="20f92-124">toocomplete 本教學課程中，您需要：</span><span class="sxs-lookup"><span data-stu-id="20f92-124">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="20f92-125">Java SE 8。</span><span class="sxs-lookup"><span data-stu-id="20f92-125">Java SE 8.</span></span> <br/> <span data-ttu-id="20f92-126">[準備開發環境][ lnk-dev-setup]描述如何 tooinstall Java 本教學課程中的 Windows 或 Linux。</span><span class="sxs-lookup"><span data-stu-id="20f92-126">[Prepare your development environment][lnk-dev-setup] describes how tooinstall Java for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="20f92-127">Maven 3。</span><span class="sxs-lookup"><span data-stu-id="20f92-127">Maven 3.</span></span>  <br/> <span data-ttu-id="20f92-128">[準備開發環境][ lnk-dev-setup]描述如何 tooinstall [Maven] [ lnk-maven]本教學課程中的 Windows 或 Linux。</span><span class="sxs-lookup"><span data-stu-id="20f92-128">[Prepare your development environment][lnk-dev-setup] describes how tooinstall [Maven][lnk-maven] for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="20f92-129">[Node.js 版本 0.10.0 或更新版本](http://nodejs.org)。</span><span class="sxs-lookup"><span data-stu-id="20f92-129">[Node.js version 0.10.0 or later](http://nodejs.org).</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-reboot-on-hello-device-using-a-direct-method"></a><span data-ttu-id="20f92-130">觸發程序使用直接的方法 hello 裝置上遠端重新開機</span><span class="sxs-lookup"><span data-stu-id="20f92-130">Trigger a remote reboot on hello device using a direct method</span></span>

<span data-ttu-id="20f92-131">在本節中，您將建立 Java 主控台應用程式以：</span><span class="sxs-lookup"><span data-stu-id="20f92-131">In this section, you create a Java console app that:</span></span>

1. <span data-ttu-id="20f92-132">Hello hello 模擬的裝置應用程式中重新開機直接方法會叫用。</span><span class="sxs-lookup"><span data-stu-id="20f92-132">Invokes hello reboot direct method in hello simulated device app.</span></span>
1. <span data-ttu-id="20f92-133">會顯示 hello 回應。</span><span class="sxs-lookup"><span data-stu-id="20f92-133">Displays hello response.</span></span>
1. <span data-ttu-id="20f92-134">輪詢 hello 報告 hello 重新開機完成後，從 hello 裝置 toodetermine 傳送的屬性。</span><span class="sxs-lookup"><span data-stu-id="20f92-134">Polls hello reported properties sent from hello device toodetermine when hello reboot is complete.</span></span>

<span data-ttu-id="20f92-135">此主控台應用程式連接 tooyour IoT 中樞 tooinvoke hello 直接方法，並讀取的 hello 報告內容。</span><span class="sxs-lookup"><span data-stu-id="20f92-135">This console app connects tooyour IoT Hub tooinvoke hello direct method and read hello reported properties.</span></span>

1. <span data-ttu-id="20f92-136">建立稱為 dm-get-started 的空資料夾。</span><span class="sxs-lookup"><span data-stu-id="20f92-136">Create an empty folder called dm-get-started.</span></span>

1. <span data-ttu-id="20f92-137">在 hello dm get 啟動資料夾中，建立名為 Maven 專案**觸發程序重新開機**使用下列命令，在您的命令提示字元的 hello。</span><span class="sxs-lookup"><span data-stu-id="20f92-137">In hello dm-get-started folder, create a Maven project called **trigger-reboot** using hello following command at your command prompt.</span></span> <span data-ttu-id="20f92-138">hello 下列範例示範單一、 完整的命令：</span><span class="sxs-lookup"><span data-stu-id="20f92-138">hello following shows a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=trigger-reboot -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="20f92-139">在命令提示字元中，瀏覽 toohello 觸發程序重新開機資料夾。</span><span class="sxs-lookup"><span data-stu-id="20f92-139">At your command prompt, navigate toohello trigger-reboot folder.</span></span>

1. <span data-ttu-id="20f92-140">使用文字編輯器，開啟 hello 觸發程序重新啟動資料夾中的 hello pom.xml 檔案並新增下列相依性 toohello hello**相依性**節點。</span><span class="sxs-lookup"><span data-stu-id="20f92-140">Using a text editor, open hello pom.xml file in hello trigger-reboot folder and add hello following dependency toohello **dependencies** node.</span></span> <span data-ttu-id="20f92-141">此相依性可讓您 toouse hello iot 服務用戶端封裝您的應用程式 toocommunicate 與 IoT 中樞中：</span><span class="sxs-lookup"><span data-stu-id="20f92-141">This dependency enables you toouse hello iot-service-client package in your app toocommunicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
      <type>jar</type>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="20f92-142">您可以檢查 hello 最新版本的**iot 服務用戶端**使用[Maven 搜尋][lnk-maven-service-search]。</span><span class="sxs-lookup"><span data-stu-id="20f92-142">You can check for hello latest version of **iot-service-client** using [Maven search][lnk-maven-service-search].</span></span>

1. <span data-ttu-id="20f92-143">新增下列 hello**建置**節點之後 hello**相依性**節點。</span><span class="sxs-lookup"><span data-stu-id="20f92-143">Add hello following **build** node after hello **dependencies** node.</span></span> <span data-ttu-id="20f92-144">此設定會指示 Maven toouse Java 1.8 toobuild hello 應用程式：</span><span class="sxs-lookup"><span data-stu-id="20f92-144">This configuration instructs Maven toouse Java 1.8 toobuild hello app:</span></span>

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

1. <span data-ttu-id="20f92-145">儲存並關閉 hello pom.xml 檔案。</span><span class="sxs-lookup"><span data-stu-id="20f92-145">Save and close hello pom.xml file.</span></span>

1. <span data-ttu-id="20f92-146">使用文字編輯器開啟 hello trigger-reboot\src\main\java\com\mycompany\app\App.java 原始程式檔。</span><span class="sxs-lookup"><span data-stu-id="20f92-146">Using a text editor, open hello trigger-reboot\src\main\java\com\mycompany\app\App.java source file.</span></span>

1. <span data-ttu-id="20f92-147">新增下列 hello**匯入**陳述式 toohello 檔案：</span><span class="sxs-lookup"><span data-stu-id="20f92-147">Add hello following **import** statements toohello file:</span></span>

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

1. <span data-ttu-id="20f92-148">新增下列類別層級變數 toohello hello**應用程式**類別。</span><span class="sxs-lookup"><span data-stu-id="20f92-148">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="20f92-149">取代`{youriothubconnectionstring}`與您在 hello 記下您的 IoT 中樞連接字串*建立 IoT 中樞*> 一節：</span><span class="sxs-lookup"><span data-stu-id="20f92-149">Replace `{youriothubconnectionstring}` with your IoT hub connection string you noted in hello *Create an IoT Hub* section:</span></span>

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    private static final String methodName = "reboot";
    private static final Long responseTimeout = TimeUnit.SECONDS.toSeconds(30);
    private static final Long connectTimeout = TimeUnit.SECONDS.toSeconds(5);
    ```

1. <span data-ttu-id="20f92-150">tooimplement 讀取 hello 執行緒報告屬性從 hello 裝置兩個每隔 10 秒鐘，加入下列 hello 巢狀類別 toohello**應用程式**類別：</span><span class="sxs-lookup"><span data-stu-id="20f92-150">tooimplement a thread that reads hello reported properties from hello device twin every 10 seconds, add hello following nested class toohello **App** class:</span></span>

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

1. <span data-ttu-id="20f92-151">hello 模擬的裝置上的 tooinvoke hello 重新開機直接方法中加入下列程式碼 toohello hello**主要**方法：</span><span class="sxs-lookup"><span data-stu-id="20f92-151">tooinvoke hello reboot direct method on hello simulated device, add hello following code toohello **main** method:</span></span>

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

1. <span data-ttu-id="20f92-152">toostart hello 執行緒 toopoll hello hello 模擬裝置的報告的屬性，加入下列程式碼 toohello hello**主要**方法：</span><span class="sxs-lookup"><span data-stu-id="20f92-152">toostart hello thread toopoll hello reported properties from hello simulated device, add hello following code toohello **main** method:</span></span>

    ```java
    ShowReportedProperties showReportedProperties = new ShowReportedProperties();
    ExecutorService executor = Executors.newFixedThreadPool(1);
    executor.execute(showReportedProperties);
    ```

1. <span data-ttu-id="20f92-153">tooenable 您 toostop hello 應用程式，加入下列程式碼 toohello hello**主要**方法：</span><span class="sxs-lookup"><span data-stu-id="20f92-153">tooenable you toostop hello app, add hello following code toohello **main** method:</span></span>

    ```java
    System.out.println("Press ENTER tooexit.");
    System.in.read();
    executor.shutdownNow();
    System.out.println("Shutting down sample...");
    ```

1. <span data-ttu-id="20f92-154">儲存並關閉 hello trigger-reboot\src\main\java\com\mycompany\app\App.java 檔案。</span><span class="sxs-lookup"><span data-stu-id="20f92-154">Save and close hello trigger-reboot\src\main\java\com\mycompany\app\App.java file.</span></span>

1. <span data-ttu-id="20f92-155">建置 hello**觸發程序重新開機**後端應用程式，並更正任何錯誤。</span><span class="sxs-lookup"><span data-stu-id="20f92-155">Build hello **trigger-reboot** back-end app and correct any errors.</span></span> <span data-ttu-id="20f92-156">在命令提示字元中，瀏覽 toohello 觸發程序重新開機資料夾，然後執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="20f92-156">At your command prompt, navigate toohello trigger-reboot folder and run hello following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="20f92-157">建立模擬裝置應用程式</span><span class="sxs-lookup"><span data-stu-id="20f92-157">Create a simulated device app</span></span>

<span data-ttu-id="20f92-158">在本節中，您將建立模擬裝置的 Java 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="20f92-158">In this section, you create a Java console app that simulates a device.</span></span> <span data-ttu-id="20f92-159">hello 應用程式會接聽 hello 重新開機直接方法呼叫從 IoT 中樞，並立即回應 toothat 呼叫。</span><span class="sxs-lookup"><span data-stu-id="20f92-159">hello app listens for hello reboot direct method call from your IoT hub and immediately responds toothat call.</span></span> <span data-ttu-id="20f92-160">應用程式，然後一段時間的睡眠 hello toosimulate hello 重新開機處理程序之前它會使用報告的屬性 toonotify hello**觸發程序重新開機**hello 重新開機的後端應用程式已完成。</span><span class="sxs-lookup"><span data-stu-id="20f92-160">hello app then sleeps for a while toosimulate hello reboot process before it uses a reported property toonotify hello **trigger-reboot** back-end app that hello reboot is complete.</span></span>

1. <span data-ttu-id="20f92-161">在 hello dm get 啟動資料夾中，建立名為 Maven 專案**模擬裝置**使用下列命令，在您的命令提示字元的 hello。</span><span class="sxs-lookup"><span data-stu-id="20f92-161">In hello dm-get-started folder, create a Maven project called **simulated-device** using hello following command at your command prompt.</span></span> <span data-ttu-id="20f92-162">hello 以下是單一、 完整的命令：</span><span class="sxs-lookup"><span data-stu-id="20f92-162">hello following is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="20f92-163">在命令提示字元中，瀏覽 toohello 模擬裝置資料夾。</span><span class="sxs-lookup"><span data-stu-id="20f92-163">At your command prompt, navigate toohello simulated-device folder.</span></span>

1. <span data-ttu-id="20f92-164">使用文字編輯器，開啟 hello 模擬裝置資料夾中的 hello pom.xml 檔案並新增下列相依性 toohello hello**相依性**節點。</span><span class="sxs-lookup"><span data-stu-id="20f92-164">Using a text editor, open hello pom.xml file in hello simulated-device folder and add hello following dependency toohello **dependencies** node.</span></span> <span data-ttu-id="20f92-165">此相依性可讓您 toouse hello iot 服務用戶端封裝您的應用程式 toocommunicate 與 IoT 中樞中：</span><span class="sxs-lookup"><span data-stu-id="20f92-165">This dependency enables you toouse hello iot-service-client package in your app toocommunicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="20f92-166">您可以檢查 hello 最新版本的**iot 裝置用戶端**使用[Maven 搜尋][lnk-maven-device-search]。</span><span class="sxs-lookup"><span data-stu-id="20f92-166">You can check for hello latest version of **iot-device-client** using [Maven search][lnk-maven-device-search].</span></span>

1. <span data-ttu-id="20f92-167">新增下列 hello**建置**節點之後 hello**相依性**節點。</span><span class="sxs-lookup"><span data-stu-id="20f92-167">Add hello following **build** node after hello **dependencies** node.</span></span> <span data-ttu-id="20f92-168">此設定會指示 Maven toouse Java 1.8 toobuild hello 應用程式：</span><span class="sxs-lookup"><span data-stu-id="20f92-168">This configuration instructs Maven toouse Java 1.8 toobuild hello app:</span></span>

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

1. <span data-ttu-id="20f92-169">儲存並關閉 hello pom.xml 檔案。</span><span class="sxs-lookup"><span data-stu-id="20f92-169">Save and close hello pom.xml file.</span></span>

1. <span data-ttu-id="20f92-170">使用文字編輯器開啟 hello simulated-device\src\main\java\com\mycompany\app\App.java 原始程式檔。</span><span class="sxs-lookup"><span data-stu-id="20f92-170">Using a text editor, open hello simulated-device\src\main\java\com\mycompany\app\App.java source file.</span></span>

1. <span data-ttu-id="20f92-171">新增下列 hello**匯入**陳述式 toohello 檔案：</span><span class="sxs-lookup"><span data-stu-id="20f92-171">Add hello following **import** statements toohello file:</span></span>

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

1. <span data-ttu-id="20f92-172">新增下列類別層級變數 toohello hello**應用程式**類別。</span><span class="sxs-lookup"><span data-stu-id="20f92-172">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="20f92-173">取代`{yourdeviceconnectionstring}`hello 裝置連接字串，而您在 hello 記下與*建立裝置身分識別*> 一節：</span><span class="sxs-lookup"><span data-stu-id="20f92-173">Replace `{yourdeviceconnectionstring}` with hello device connection string you noted in hello *Create a device identity* section:</span></span>

    ```java
    private static final int METHOD_SUCCESS = 200;
    private static final int METHOD_NOT_DEFINED = 404;

    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String connString = "{yourdeviceconnectionstring}";
    private static DeviceClient client;
    ```

1. <span data-ttu-id="20f92-174">tooimplement 直接的方法狀態事件的回呼處理常式將 hello 面一行加入巢狀類別 toohello**應用程式**類別：</span><span class="sxs-lookup"><span data-stu-id="20f92-174">tooimplement a callback handler for direct method status events, add hello following nested class toohello **App** class:</span></span>

    ```java
    protected static class DirectMethodStatusCallback implements IotHubEventCallback
    {
      public void execute(IotHubStatusCode status, Object context)
      {
        System.out.println("IoT Hub responded toodevice method operation with status " + status.name());
      }
    }
    ```

1. <span data-ttu-id="20f92-175">tooimplement 裝置兩個狀態事件的回呼處理常式將 hello 面一行加入巢狀類別 toohello**應用程式**類別：</span><span class="sxs-lookup"><span data-stu-id="20f92-175">tooimplement a callback handler for device twin status events, add hello following nested class toohello **App** class:</span></span>

    ```java
    protected static class DeviceTwinStatusCallback implements IotHubEventCallback
    {
        public void execute(IotHubStatusCode status, Object context)
        {
            System.out.println("IoT Hub responded toodevice twin operation with status " + status.name());
        }
    }
    ```

1. <span data-ttu-id="20f92-176">tooimplement 屬性事件的回呼處理常式將 hello 面一行加入巢狀類別 toohello**應用程式**類別：</span><span class="sxs-lookup"><span data-stu-id="20f92-176">tooimplement a callback handler for property events, add hello following nested class toohello **App** class:</span></span>

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

1. <span data-ttu-id="20f92-177">tooimplement 執行緒 toosimulate hello 裝置重新開機，將 hello 面一行加入巢狀類別 toohello**應用程式**類別。</span><span class="sxs-lookup"><span data-stu-id="20f92-177">tooimplement a thread toosimulate hello device reboot, add hello following nested class toohello **App** class.</span></span> <span data-ttu-id="20f92-178">hello 執行緒進入睡眠狀態五秒，然後設定 hello **lastReboot**報告屬性：</span><span class="sxs-lookup"><span data-stu-id="20f92-178">hello thread sleeps for five seconds and then sets hello **lastReboot** reported property:</span></span>

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

1. <span data-ttu-id="20f92-179">tooimplement hello 直接方法 hello 在裝置上，將 hello 面一行加入巢狀類別 toohello**應用程式**類別。</span><span class="sxs-lookup"><span data-stu-id="20f92-179">tooimplement hello direct method on hello device, add hello following nested class toohello **App** class.</span></span> <span data-ttu-id="20f92-180">當 hello 模擬應用程式會接收呼叫 toohello**重新開機**直接的方法，它會傳回通知 toohello 呼叫者，然後啟動執行緒 tooprocess hello 重新啟動：</span><span class="sxs-lookup"><span data-stu-id="20f92-180">When hello simulated app receives a call toohello **reboot** direct method, it returns an acknowledgement toohello caller and then starts a thread tooprocess hello reboot:</span></span>

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

1. <span data-ttu-id="20f92-181">修改 hello 簽章的 hello**主要**方法 toothrow hello 下列例外狀況：</span><span class="sxs-lookup"><span data-stu-id="20f92-181">Modify hello signature of hello **main** method toothrow hello following exceptions:</span></span>

    ```java
    public static void main(String[] args) throws IOException, URISyntaxException
    ```

1. <span data-ttu-id="20f92-182">tooinstantiate **DeviceClient**，加入下列程式碼 toohello hello**主要**方法：</span><span class="sxs-lookup"><span data-stu-id="20f92-182">tooinstantiate a **DeviceClient**, add hello following code toohello **main** method:</span></span>

    ```java
    System.out.println("Starting device client sample...");
    client = new DeviceClient(connString, protocol);
    ```

1. <span data-ttu-id="20f92-183">toostart 接聽直接方法呼叫中，加入下列程式碼 toohello hello**主要**方法：</span><span class="sxs-lookup"><span data-stu-id="20f92-183">toostart listening for direct method calls, add hello following code toohello **main** method:</span></span>

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

1. <span data-ttu-id="20f92-184">tooshut 向 hello 裝置模擬器，加入下列程式碼 toohello hello**主要**方法：</span><span class="sxs-lookup"><span data-stu-id="20f92-184">tooshut down hello device simulator, add hello following code toohello **main** method:</span></span>

    ```java
    System.out.println("Press any key tooexit...");
    Scanner scanner = new Scanner(System.in);
    scanner.nextLine();
    scanner.close();
    client.close();
    System.out.println("Shutting down...");
    ```

1. <span data-ttu-id="20f92-185">儲存並關閉 hello simulated-device\src\main\java\com\mycompany\app\App.java 檔案。</span><span class="sxs-lookup"><span data-stu-id="20f92-185">Save and close hello simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span>

1. <span data-ttu-id="20f92-186">建置 hello**模擬裝置**後端應用程式，並更正任何錯誤。</span><span class="sxs-lookup"><span data-stu-id="20f92-186">Build hello **simulated-device** back-end app and correct any errors.</span></span> <span data-ttu-id="20f92-187">在命令提示字元中，瀏覽 toohello 模擬裝置資料夾，然後執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="20f92-187">At your command prompt, navigate toohello simulated-device folder and run hello following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="run-hello-apps"></a><span data-ttu-id="20f92-188">執行 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="20f92-188">Run hello apps</span></span>

<span data-ttu-id="20f92-189">現在您已經準備就緒 toorun hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="20f92-189">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="20f92-190">Hello 模擬裝置資料夾中的命令提示字元，執行下列命令 toobegin 接聽重新開機或從 IoT 中樞的方法呼叫的 hello:</span><span class="sxs-lookup"><span data-stu-id="20f92-190">At a command prompt in hello simulated-device folder, run hello following command toobegin listening for reboot method calls from your IoT hub:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Java IoT 中樞模擬裝置重新開機直接方法呼叫的應用程式 toolisten][1]

1. <span data-ttu-id="20f92-192">Hello 觸發程序重新啟動資料夾中的命令提示字元，執行下列模擬的裝置上的命令 toocall hello 重新開機方法，從 IoT 中樞的 hello:</span><span class="sxs-lookup"><span data-stu-id="20f92-192">At a command prompt in hello trigger-reboot folder, run hello following command toocall hello reboot method on your simulated device from your IoT hub:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Java IoT 中樞服務應用程式 toocall hello 重新開機直接方法][2]

1. <span data-ttu-id="20f92-194">hello 模擬的裝置會回應 toohello 重新開機直接方法呼叫：</span><span class="sxs-lookup"><span data-stu-id="20f92-194">hello simulated device responds toohello reboot direct method call:</span></span>

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