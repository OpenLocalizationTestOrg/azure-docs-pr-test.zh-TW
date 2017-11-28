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
# <a name="use-direct-methods-java"></a><span data-ttu-id="d09be-104">使用直接方法 (Java)</span><span class="sxs-lookup"><span data-stu-id="d09be-104">Use direct methods (Java)</span></span>

[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

<span data-ttu-id="d09be-105">在本教學課程中，您將建立兩個 Java 主控台應用程式：</span><span class="sxs-lookup"><span data-stu-id="d09be-105">In this tutorial, you create two Java console apps:</span></span>

* <span data-ttu-id="d09be-106">**叫用直接方法**，Java 後端應用程式，以呼叫 hello 模擬的裝置應用程式中的方法，並顯示 hello 回應。</span><span class="sxs-lookup"><span data-stu-id="d09be-106">**invoke-direct-method**, a Java back-end app that calls a method in hello simulated device app and displays hello response.</span></span>
* <span data-ttu-id="d09be-107">**模擬裝置**，模擬裝置，使用您所建立的 hello 裝置身分識別連接 tooyour IoT 中樞的 Java 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d09be-107">**simulated-device**, a Java app that simulates a device connecting tooyour IoT hub with hello device identity you create.</span></span> <span data-ttu-id="d09be-108">此應用程式會回應 toohello 直接叫用從 hello 後端。</span><span class="sxs-lookup"><span data-stu-id="d09be-108">This app responds toohello direct invoked from hello back end.</span></span>

> [!NOTE]
> <span data-ttu-id="d09be-109">如需您可以在裝置和您的方案後端上使用 toobuild 應用程式 toorun 的 hello Sdk 資訊，請參閱[Azure IoT Sdk][lnk-hub-sdks]。</span><span class="sxs-lookup"><span data-stu-id="d09be-109">For information about hello SDKs that you can use toobuild applications toorun on devices and your solution back end, see [Azure IoT SDKs][lnk-hub-sdks].</span></span>

<span data-ttu-id="d09be-110">toocomplete 本教學課程中，您需要：</span><span class="sxs-lookup"><span data-stu-id="d09be-110">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="d09be-111">Java SE 8。</span><span class="sxs-lookup"><span data-stu-id="d09be-111">Java SE 8.</span></span> <br/> <span data-ttu-id="d09be-112">[準備開發環境][ lnk-dev-setup]描述如何 tooinstall Java 本教學課程中的 Windows 或 Linux。</span><span class="sxs-lookup"><span data-stu-id="d09be-112">[Prepare your development environment][lnk-dev-setup] describes how tooinstall Java for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="d09be-113">Maven 3。</span><span class="sxs-lookup"><span data-stu-id="d09be-113">Maven 3.</span></span>  <br/> <span data-ttu-id="d09be-114">[準備開發環境][ lnk-dev-setup]描述如何 tooinstall [Maven] [ lnk-maven]本教學課程中的 Windows 或 Linux。</span><span class="sxs-lookup"><span data-stu-id="d09be-114">[Prepare your development environment][lnk-dev-setup] describes how tooinstall [Maven][lnk-maven] for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="d09be-115">[Node.js 版本 0.10.0 或更新版本](http://nodejs.org)。</span><span class="sxs-lookup"><span data-stu-id="d09be-115">[Node.js version 0.10.0 or later](http://nodejs.org).</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="d09be-116">建立模擬裝置應用程式</span><span class="sxs-lookup"><span data-stu-id="d09be-116">Create a simulated device app</span></span>

<span data-ttu-id="d09be-117">在本節中，您可以建立回應 hello 方案回呼叫端的 tooa 方法的 Java 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="d09be-117">In this section, you create a Java console app that responds tooa method called by hello solution back end.</span></span>

1. <span data-ttu-id="d09be-118">建立名為 iot-java-direct-method 的空資料夾。</span><span class="sxs-lookup"><span data-stu-id="d09be-118">Create an empty folder called iot-java-direct-method.</span></span>

1. <span data-ttu-id="d09be-119">在 hello iot java-direct 方法資料夾中，建立名為 Maven 專案**模擬裝置**使用下列命令，在您的命令提示字元的 hello。</span><span class="sxs-lookup"><span data-stu-id="d09be-119">In hello iot-java-direct-method folder, create a Maven project called **simulated-device** using hello following command at your command prompt.</span></span> <span data-ttu-id="d09be-120">下列命令的 hello 是單一、 完整的命令：</span><span class="sxs-lookup"><span data-stu-id="d09be-120">hello following command is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="d09be-121">在命令提示字元中，瀏覽 toohello 模擬裝置資料夾。</span><span class="sxs-lookup"><span data-stu-id="d09be-121">At your command prompt, navigate toohello simulated-device folder.</span></span>

1. <span data-ttu-id="d09be-122">使用文字編輯器，開啟 hello 模擬裝置資料夾中的 hello pom.xml 檔案並新增下列相依性 toohello hello**相依性**節點。</span><span class="sxs-lookup"><span data-stu-id="d09be-122">Using a text editor, open hello pom.xml file in hello simulated-device folder and add hello following dependencies toohello **dependencies** node.</span></span> <span data-ttu-id="d09be-123">此相依性可讓您 toouse hello iot 裝置用戶端封裝您的應用程式 toocommunicate 與 IoT 中樞中：</span><span class="sxs-lookup"><span data-stu-id="d09be-123">This dependency enables you toouse hello iot-device-client package in your app toocommunicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="d09be-124">您可以檢查 hello 最新版本的**iot 裝置用戶端**使用[Maven 搜尋][lnk-maven-device-search]。</span><span class="sxs-lookup"><span data-stu-id="d09be-124">You can check for hello latest version of **iot-device-client** using [Maven search][lnk-maven-device-search].</span></span>

1. <span data-ttu-id="d09be-125">新增下列 hello**建置**節點之後 hello**相依性**節點。</span><span class="sxs-lookup"><span data-stu-id="d09be-125">Add hello following **build** node after hello **dependencies** node.</span></span> <span data-ttu-id="d09be-126">此設定會指示 Maven toouse Java 1.8 toobuild hello 應用程式：</span><span class="sxs-lookup"><span data-stu-id="d09be-126">This configuration instructs Maven toouse Java 1.8 toobuild hello app:</span></span>

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

1. <span data-ttu-id="d09be-127">儲存並關閉 hello pom.xml 檔案。</span><span class="sxs-lookup"><span data-stu-id="d09be-127">Save and close hello pom.xml file.</span></span>

1. <span data-ttu-id="d09be-128">使用文字編輯器開啟 hello simulated-device\src\main\java\com\mycompany\app\App.java 檔案。</span><span class="sxs-lookup"><span data-stu-id="d09be-128">Using a text editor, open hello simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span>

1. <span data-ttu-id="d09be-129">新增下列 hello**匯入**陳述式 toohello 檔案：</span><span class="sxs-lookup"><span data-stu-id="d09be-129">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.microsoft.azure.sdk.iot.device.DeviceTwin.*;

    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.util.Scanner;
    ```

1. <span data-ttu-id="d09be-130">新增下列類別層級變數 toohello hello**應用程式**類別。</span><span class="sxs-lookup"><span data-stu-id="d09be-130">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="d09be-131">取代`{youriothubname}`以您的 IoT 中樞名稱，和`{yourdevicekey}`hello 裝置索引鍵值中 hello 產生*建立裝置身分識別*> 一節：</span><span class="sxs-lookup"><span data-stu-id="d09be-131">Replacing `{youriothubname}` with your IoT hub name, and `{yourdevicekey}` with hello device key value you generated in hello *Create a device identity* section:</span></span>

    ```java
    private static String connString = "HostName={youriothubname}.azure-devices.net;DeviceId=myDeviceID;SharedAccessKey={yourdevicekey}";
    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String deviceId = "myDeviceId";
    private static final int METHOD_SUCCESS = 200;
    private static final int METHOD_NOT_DEFINED = 404;
    ```

    <span data-ttu-id="d09be-132">此範例應用程式會使用 hello**通訊協定**變數時，它會具現化**DeviceClient**物件。</span><span class="sxs-lookup"><span data-stu-id="d09be-132">This sample app uses hello **protocol** variable when it instantiates a **DeviceClient** object.</span></span> <span data-ttu-id="d09be-133">目前，toouse 直接方法，您必須使用 hello MQTT 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="d09be-133">Currently, toouse direct methods you must use hello MQTT protocol.</span></span>

1. <span data-ttu-id="d09be-134">tooreturn 狀態程式碼 tooyour IoT 中樞，將 hello 面一行加入巢狀類別 toohello**應用程式**類別：</span><span class="sxs-lookup"><span data-stu-id="d09be-134">tooreturn a status code tooyour IoT hub, add hello following nested class toohello **App** class:</span></span>

    ```java
    protected static class DirectMethodStatusCallback implements IotHubEventCallback
    {
      public void execute(IotHubStatusCode status, Object context)
      {
        System.out.println("IoT Hub responded toodevice method operation with status " + status.name());
      }
    }
    ```

1. <span data-ttu-id="d09be-135">toohandle hello 直接的方法引動過程從 hello 方案後端，將 hello 面一行加入巢狀類別 toohello**應用程式**類別：</span><span class="sxs-lookup"><span data-stu-id="d09be-135">toohandle hello direct method invocations from hello solution back end, add hello following nested class toohello **App** class:</span></span>

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

1. <span data-ttu-id="d09be-136">toocreate **DeviceClient**並接聽直接的方法引動過程，加入**主要**方法 toohello**應用程式**類別：</span><span class="sxs-lookup"><span data-stu-id="d09be-136">toocreate a **DeviceClient** and listen for direct method invocations, add a **main** method toohello **App** class:</span></span>

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

1. <span data-ttu-id="d09be-137">儲存並關閉 hello simulated-device\src\main\java\com\mycompany\app\App.java 檔案</span><span class="sxs-lookup"><span data-stu-id="d09be-137">Save and close hello simulated-device\src\main\java\com\mycompany\app\App.java file</span></span>

1. <span data-ttu-id="d09be-138">建置 hello**模擬裝置**應用程式，並更正任何錯誤。</span><span class="sxs-lookup"><span data-stu-id="d09be-138">Build hello **simulated-device** app and correct any errors.</span></span> <span data-ttu-id="d09be-139">在命令提示字元中，瀏覽 toohello 模擬裝置資料夾，然後執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="d09be-139">At your command prompt, navigate toohello simulated-device folder and run hello following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="call-a-direct-method-on-a-device"></a><span data-ttu-id="d09be-140">在裝置上呼叫直接方法</span><span class="sxs-lookup"><span data-stu-id="d09be-140">Call a direct method on a device</span></span>

<span data-ttu-id="d09be-141">在本節中，您可以建立 Java 主控台應用程式會叫用直接的方法，並顯示 hello 回應。</span><span class="sxs-lookup"><span data-stu-id="d09be-141">In this section, you create a Java console app that invokes a direct method and then displays hello response.</span></span> <span data-ttu-id="d09be-142">此主控台應用程式會連接 tooyour IoT 中樞 tooinvoke hello 直接的方法。</span><span class="sxs-lookup"><span data-stu-id="d09be-142">This console app connects tooyour IoT Hub tooinvoke hello direct method.</span></span>

1. <span data-ttu-id="d09be-143">在 hello iot java-direct 方法資料夾中，建立名為 Maven 專案**叫用直接方法**使用下列命令，在您的命令提示字元的 hello。</span><span class="sxs-lookup"><span data-stu-id="d09be-143">In hello iot-java-direct-method folder, create a Maven project called **invoke-direct-method** using hello following command at your command prompt.</span></span> <span data-ttu-id="d09be-144">下列命令的 hello 是單一、 完整的命令：</span><span class="sxs-lookup"><span data-stu-id="d09be-144">hello following command is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=invoke-direct-method -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="d09be-145">在命令提示字元中，瀏覽 toohello 叫用直接方法資料夾。</span><span class="sxs-lookup"><span data-stu-id="d09be-145">At your command prompt, navigate toohello invoke-direct-method folder.</span></span>

1. <span data-ttu-id="d09be-146">使用文字編輯器，開啟 hello 叫用直接方法資料夾中的 hello pom.xml 檔案並新增下列相依性 toohello hello**相依性**節點。</span><span class="sxs-lookup"><span data-stu-id="d09be-146">Using a text editor, open hello pom.xml file in hello invoke-direct-method folder and add hello following dependency toohello **dependencies** node.</span></span> <span data-ttu-id="d09be-147">此相依性可讓您 toouse hello iot 服務用戶端封裝您的應用程式 toocommunicate 與 IoT 中樞中：</span><span class="sxs-lookup"><span data-stu-id="d09be-147">This dependency enables you toouse hello iot-service-client package in your app toocommunicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
      <type>jar</type>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="d09be-148">您可以檢查 hello 最新版本的**iot 服務用戶端**使用[Maven 搜尋][lnk-maven-service-search]。</span><span class="sxs-lookup"><span data-stu-id="d09be-148">You can check for hello latest version of **iot-service-client** using [Maven search][lnk-maven-service-search].</span></span>

1. <span data-ttu-id="d09be-149">新增下列 hello**建置**節點之後 hello**相依性**節點。</span><span class="sxs-lookup"><span data-stu-id="d09be-149">Add hello following **build** node after hello **dependencies** node.</span></span> <span data-ttu-id="d09be-150">此設定會指示 Maven toouse Java 1.8 toobuild hello 應用程式：</span><span class="sxs-lookup"><span data-stu-id="d09be-150">This configuration instructs Maven toouse Java 1.8 toobuild hello app:</span></span>

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

1. <span data-ttu-id="d09be-151">儲存並關閉 hello pom.xml 檔案。</span><span class="sxs-lookup"><span data-stu-id="d09be-151">Save and close hello pom.xml file.</span></span>

1. <span data-ttu-id="d09be-152">使用文字編輯器開啟 hello invoke-direct-method\src\main\java\com\mycompany\app\App.java 檔案。</span><span class="sxs-lookup"><span data-stu-id="d09be-152">Using a text editor, open hello invoke-direct-method\src\main\java\com\mycompany\app\App.java file.</span></span>

1. <span data-ttu-id="d09be-153">新增下列 hello**匯入**陳述式 toohello 檔案：</span><span class="sxs-lookup"><span data-stu-id="d09be-153">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.service.devicetwin.DeviceMethod;
    import com.microsoft.azure.sdk.iot.service.devicetwin.MethodResult;
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;

    import java.io.IOException;
    import java.util.concurrent.TimeUnit;
    ```

1. <span data-ttu-id="d09be-154">新增下列類別層級變數 toohello hello**應用程式**類別。</span><span class="sxs-lookup"><span data-stu-id="d09be-154">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="d09be-155">取代`{youriothubconnectionstring}`與您在 hello 記下您的 IoT 中樞連接字串*建立 IoT 中樞*> 一節：</span><span class="sxs-lookup"><span data-stu-id="d09be-155">Replace `{youriothubconnectionstring}` with your IoT hub connection string you noted in hello *Create an IoT Hub* section:</span></span>

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    public static final String methodName = "writeLine";
    public static final Long responseTimeout = TimeUnit.SECONDS.toSeconds(30);
    public static final Long connectTimeout = TimeUnit.SECONDS.toSeconds(5);
    public static final String payload = "a line toobe written";
    ```

1. <span data-ttu-id="d09be-156">tooinvoke hello 方法 hello 模擬在裝置上，加入下列程式碼 toohello hello**主要**方法：</span><span class="sxs-lookup"><span data-stu-id="d09be-156">tooinvoke hello method on hello simulated device, add hello following code toohello **main** method:</span></span>

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

1. <span data-ttu-id="d09be-157">儲存並關閉 hello invoke-direct-method\src\main\java\com\mycompany\app\App.java 檔案</span><span class="sxs-lookup"><span data-stu-id="d09be-157">Save and close hello invoke-direct-method\src\main\java\com\mycompany\app\App.java file</span></span>

1. <span data-ttu-id="d09be-158">建置 hello**叫用直接方法**應用程式，並更正任何錯誤。</span><span class="sxs-lookup"><span data-stu-id="d09be-158">Build hello **invoke-direct-method** app and correct any errors.</span></span> <span data-ttu-id="d09be-159">在命令提示字元中，瀏覽 toohello 叫用直接方法資料夾，然後執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="d09be-159">At your command prompt, navigate toohello invoke-direct-method folder and run hello following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="run-hello-apps"></a><span data-ttu-id="d09be-160">執行 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="d09be-160">Run hello apps</span></span>

<span data-ttu-id="d09be-161">現在您已經準備就緒 toorun hello 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="d09be-161">You are now ready toorun hello console apps.</span></span>

1. <span data-ttu-id="d09be-162">Hello 模擬裝置資料夾中的命令提示字元，執行下列命令 toobegin 接聽從 IoT 中樞的方法呼叫的 hello:</span><span class="sxs-lookup"><span data-stu-id="d09be-162">At a command prompt in hello simulated-device folder, run hello following command toobegin listening for method calls from your IoT hub:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Java IoT 中樞模擬裝置的直接方法呼叫的應用程式 toolisten][8]

1. <span data-ttu-id="d09be-164">Hello 叫用直接方法資料夾中的命令提示字元，執行下列命令 toocall hello 方法模擬的裝置上從 IoT 中樞：</span><span class="sxs-lookup"><span data-stu-id="d09be-164">At a command prompt in hello invoke-direct-method folder, run hello following command toocall a method on your simulated device from your IoT hub:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Java IoT 中樞服務應用程式 toocall 直接的方法][7]

1. <span data-ttu-id="d09be-166">hello 模擬的裝置會回應 toohello 直接方法呼叫：</span><span class="sxs-lookup"><span data-stu-id="d09be-166">hello simulated device responds toohello direct method call:</span></span>

    ![Java IoT 中樞模擬的裝置應用程式回應 toohello 直接方法呼叫][9]

## <a name="next-steps"></a><span data-ttu-id="d09be-168">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d09be-168">Next steps</span></span>

<span data-ttu-id="d09be-169">在本教學課程中，您在 hello Azure 入口網站中設定新的 IoT 中樞，並接著 hello IoT 中樞的身分識別登錄中建立裝置身分識別。</span><span class="sxs-lookup"><span data-stu-id="d09be-169">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="d09be-170">您已經使用此裝置身分識別 tooenable hello 模擬裝置的應用程式 tooreact toomethods hello 雲端所叫用。</span><span class="sxs-lookup"><span data-stu-id="d09be-170">You used this device identity tooenable hello simulated device app tooreact toomethods invoked by hello cloud.</span></span> <span data-ttu-id="d09be-171">您也會建立叫用 hello 裝置上的方法，並會顯示 hello 回應 hello 裝置的應用程式。</span><span class="sxs-lookup"><span data-stu-id="d09be-171">You also created an app that invokes methods on hello device and displays hello response from hello device.</span></span>

<span data-ttu-id="d09be-172">tooexplore 其他 IoT 案例，請參閱[多個裝置上的工作排程][lnk-devguide-jobs]。</span><span class="sxs-lookup"><span data-stu-id="d09be-172">tooexplore other IoT scenarios, see [Schedule jobs on multiple devices][lnk-devguide-jobs].</span></span>

<span data-ttu-id="d09be-173">toolearn 如何 tooextend IoT 解決方案和排程方法呼叫上多個裝置，請參閱 hello[排程和廣播的工作][ lnk-tutorial-jobs]教學課程。</span><span class="sxs-lookup"><span data-stu-id="d09be-173">toolearn how tooextend your IoT solution and schedule method calls on multiple devices, see hello [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

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
