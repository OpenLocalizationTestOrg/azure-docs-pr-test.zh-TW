---
title: "使用 Azure IoT 中樞直接方法 (Java) | Microsoft Docs"
description: "如何使用 Azure IoT 中樞直接方法。 您可以使用適用於 Java 的 Azure IoT 裝置 SDK，實作模擬的裝置應用程式 (包含直接方法)，也可以使用適用於 Java 的 Azure IoT 服務 SDK，實作服務應用程式 (叫用直接方法)。"
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
ms.openlocfilehash: 6243a1a8cc971c53c797182b2beb6f594d2ac5f7
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="use-direct-methods-java"></a><span data-ttu-id="fa87e-104">使用直接方法 (Java)</span><span class="sxs-lookup"><span data-stu-id="fa87e-104">Use direct methods (Java)</span></span>

[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

<span data-ttu-id="fa87e-105">在本教學課程中，您將建立兩個 Java 主控台應用程式：</span><span class="sxs-lookup"><span data-stu-id="fa87e-105">In this tutorial, you create two Java console apps:</span></span>

* <span data-ttu-id="fa87e-106">**invoke-direct-method**，這是 Java 後端應用程式，可在模擬裝置應用程式中呼叫方法，並顯示回應。</span><span class="sxs-lookup"><span data-stu-id="fa87e-106">**invoke-direct-method**, a Java back-end app that calls a method in the simulated device app and displays the response.</span></span>
* <span data-ttu-id="fa87e-107">**simulated-device**，這是 Java 應用程式，可使用您所建立的裝置身分識別，模擬連線到您 IoT 中樞的裝置。</span><span class="sxs-lookup"><span data-stu-id="fa87e-107">**simulated-device**, a Java app that simulates a device connecting to your IoT hub with the device identity you create.</span></span> <span data-ttu-id="fa87e-108">此應用程式會回應來自後端的直接叫用。</span><span class="sxs-lookup"><span data-stu-id="fa87e-108">This app responds to the direct invoked from the back end.</span></span>

> [!NOTE]
> <span data-ttu-id="fa87e-109">如需可用來建置應用程式，以在裝置與您的解決方案後端執行之 SDK 的資訊，請參閱 [Azure IoT SDK][lnk-hub-sdks]。</span><span class="sxs-lookup"><span data-stu-id="fa87e-109">For information about the SDKs that you can use to build applications to run on devices and your solution back end, see [Azure IoT SDKs][lnk-hub-sdks].</span></span>

<span data-ttu-id="fa87e-110">若要完成本教學課程，您需要：</span><span class="sxs-lookup"><span data-stu-id="fa87e-110">To complete this tutorial, you need:</span></span>

* <span data-ttu-id="fa87e-111">Java SE 8。</span><span class="sxs-lookup"><span data-stu-id="fa87e-111">Java SE 8.</span></span> <br/> <span data-ttu-id="fa87e-112">[準備您的開發環境][lnk-dev-setup]說明如何在 Windows 或 Linux 上安裝本教學課程的 Java。</span><span class="sxs-lookup"><span data-stu-id="fa87e-112">[Prepare your development environment][lnk-dev-setup] describes how to install Java for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="fa87e-113">Maven 3。</span><span class="sxs-lookup"><span data-stu-id="fa87e-113">Maven 3.</span></span>  <br/> <span data-ttu-id="fa87e-114">[準備您的開發環境][lnk-dev-setup]說明如何在 Windows 或 Linux 上安裝本教學課程的 [Maven][lnk-maven]。</span><span class="sxs-lookup"><span data-stu-id="fa87e-114">[Prepare your development environment][lnk-dev-setup] describes how to install [Maven][lnk-maven] for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="fa87e-115">[Node.js 版本 0.10.0 或更新版本](http://nodejs.org)。</span><span class="sxs-lookup"><span data-stu-id="fa87e-115">[Node.js version 0.10.0 or later](http://nodejs.org).</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="fa87e-116">建立模擬裝置應用程式</span><span class="sxs-lookup"><span data-stu-id="fa87e-116">Create a simulated device app</span></span>

<span data-ttu-id="fa87e-117">在本節中，您會建立 Java 主控台應用程式，回應解決方案後端所呼叫的方法。</span><span class="sxs-lookup"><span data-stu-id="fa87e-117">In this section, you create a Java console app that responds to a method called by the solution back end.</span></span>

1. <span data-ttu-id="fa87e-118">建立名為 iot-java-direct-method 的空資料夾。</span><span class="sxs-lookup"><span data-stu-id="fa87e-118">Create an empty folder called iot-java-direct-method.</span></span>

1. <span data-ttu-id="fa87e-119">在 iot-java-direct-method 資料夾的命令提示字元下，使用下列命令建立名為 **simulated-device** 的 Maven 專案。</span><span class="sxs-lookup"><span data-stu-id="fa87e-119">In the iot-java-direct-method folder, create a Maven project called **simulated-device** using the following command at your command prompt.</span></span> <span data-ttu-id="fa87e-120">下列命令是完整的單一命令：</span><span class="sxs-lookup"><span data-stu-id="fa87e-120">The following command is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="fa87e-121">在命令提示字元中，瀏覽到 simulated-device 資料夾。</span><span class="sxs-lookup"><span data-stu-id="fa87e-121">At your command prompt, navigate to the simulated-device folder.</span></span>

1. <span data-ttu-id="fa87e-122">使用文字編輯器，在 simulated-device 資料夾中開啟 pom.xml 檔案，並對 [相依性]  節點新增下列相依性。</span><span class="sxs-lookup"><span data-stu-id="fa87e-122">Using a text editor, open the pom.xml file in the simulated-device folder and add the following dependencies to the **dependencies** node.</span></span> <span data-ttu-id="fa87e-123">這個相依性可讓您在應用程式中使用 iot-device-client 套件與 IoT 中樞通訊：</span><span class="sxs-lookup"><span data-stu-id="fa87e-123">This dependency enables you to use the iot-device-client package in your app to communicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="fa87e-124">您可以使用 [Maven 搜尋][lnk-maven-device-search]來檢查最新版的 **iot-device-client**。</span><span class="sxs-lookup"><span data-stu-id="fa87e-124">You can check for the latest version of **iot-device-client** using [Maven search][lnk-maven-device-search].</span></span>

1. <span data-ttu-id="fa87e-125">將下列 [建置] 節點新增至 [相依性] 節點之後。</span><span class="sxs-lookup"><span data-stu-id="fa87e-125">Add the following **build** node after the **dependencies** node.</span></span> <span data-ttu-id="fa87e-126">此設定會指示 Maven 使用 Java 1.8 來建置應用程式：</span><span class="sxs-lookup"><span data-stu-id="fa87e-126">This configuration instructs Maven to use Java 1.8 to build the app:</span></span>

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

1. <span data-ttu-id="fa87e-127">儲存並關閉 pom.xml 檔案。</span><span class="sxs-lookup"><span data-stu-id="fa87e-127">Save and close the pom.xml file.</span></span>

1. <span data-ttu-id="fa87e-128">使用文字編輯器開啟 simulated-device\src\main\java\com\mycompany\app\App.java 檔案。</span><span class="sxs-lookup"><span data-stu-id="fa87e-128">Using a text editor, open the simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span>

1. <span data-ttu-id="fa87e-129">在此檔案中新增下列 **import** 陳述式：</span><span class="sxs-lookup"><span data-stu-id="fa87e-129">Add the following **import** statements to the file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.microsoft.azure.sdk.iot.device.DeviceTwin.*;

    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.util.Scanner;
    ```

1. <span data-ttu-id="fa87e-130">將下列類別層級變數新增到 **App** 類別中。</span><span class="sxs-lookup"><span data-stu-id="fa87e-130">Add the following class-level variables to the **App** class.</span></span> <span data-ttu-id="fa87e-131">以您的 IoT 中樞名稱取代 `{youriothubname}`，並以您在＜建立裝置身分識別＞一節中產生的裝置金鑰值取代 `{yourdevicekey}`：</span><span class="sxs-lookup"><span data-stu-id="fa87e-131">Replacing `{youriothubname}` with your IoT hub name, and `{yourdevicekey}` with the device key value you generated in the *Create a device identity* section:</span></span>

    ```java
    private static String connString = "HostName={youriothubname}.azure-devices.net;DeviceId=myDeviceID;SharedAccessKey={yourdevicekey}";
    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String deviceId = "myDeviceId";
    private static final int METHOD_SUCCESS = 200;
    private static final int METHOD_NOT_DEFINED = 404;
    ```

    <span data-ttu-id="fa87e-132">此範例應用程式在具現化 **DeviceClient** 物件時使用 **protocol** 變數。</span><span class="sxs-lookup"><span data-stu-id="fa87e-132">This sample app uses the **protocol** variable when it instantiates a **DeviceClient** object.</span></span> <span data-ttu-id="fa87e-133">目前，若要使用直接方法，您必須使用 MQTT 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="fa87e-133">Currently, to use direct methods you must use the MQTT protocol.</span></span>

1. <span data-ttu-id="fa87e-134">若要將狀態碼傳回 IoT 中樞，請將下列巢狀類別新增到 **App** 類別中：</span><span class="sxs-lookup"><span data-stu-id="fa87e-134">To return a status code to your IoT hub, add the following nested class to the **App** class:</span></span>

    ```java
    protected static class DirectMethodStatusCallback implements IotHubEventCallback
    {
      public void execute(IotHubStatusCode status, Object context)
      {
        System.out.println("IoT Hub responded to device method operation with status " + status.name());
      }
    }
    ```

1. <span data-ttu-id="fa87e-135">若要處理解決方案後端的直接方法引動過程，請將下列巢狀類別新增到 **App** 類別中︰</span><span class="sxs-lookup"><span data-stu-id="fa87e-135">To handle the direct method invocations from the solution back end, add the following nested class to the **App** class:</span></span>

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

1. <span data-ttu-id="fa87e-136">若要建立 **DeviceClient** 及接聽直接方法引動過程，請將 **main** 方法新增至 **App** 類別︰</span><span class="sxs-lookup"><span data-stu-id="fa87e-136">To create a **DeviceClient** and listen for direct method invocations, add a **main** method to the **App** class:</span></span>

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
        System.out.println("Subscribed to direct methods. Waiting...");
      }
      catch (Exception e)
      {
        System.out.println("On exception, shutting down \n" + " Cause: " + e.getCause() + " \n" +  e.getMessage());
        client.close();
        System.out.println("Shutting down...");
      }

      System.out.println("Press any key to exit...");
      Scanner scanner = new Scanner(System.in);
      scanner.nextLine();
      scanner.close();
      client.close();
      System.out.println("Shutting down...");
    }
    ```

1. <span data-ttu-id="fa87e-137">儲存並關閉 simulated-device\src\main\java\com\mycompany\app\App.java 檔案</span><span class="sxs-lookup"><span data-stu-id="fa87e-137">Save and close the simulated-device\src\main\java\com\mycompany\app\App.java file</span></span>

1. <span data-ttu-id="fa87e-138">建置 **simulated-device** 應用程式，並更正所有錯誤。</span><span class="sxs-lookup"><span data-stu-id="fa87e-138">Build the **simulated-device** app and correct any errors.</span></span> <span data-ttu-id="fa87e-139">在命令提示字元中，瀏覽到 simulated-device 資料夾，並執行下列命令︰</span><span class="sxs-lookup"><span data-stu-id="fa87e-139">At your command prompt, navigate to the simulated-device folder and run the following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="call-a-direct-method-on-a-device"></a><span data-ttu-id="fa87e-140">在裝置上呼叫直接方法</span><span class="sxs-lookup"><span data-stu-id="fa87e-140">Call a direct method on a device</span></span>

<span data-ttu-id="fa87e-141">在本節中，您會建立 Java 主控台應用程式，以叫用直接方法，然後顯示回應。</span><span class="sxs-lookup"><span data-stu-id="fa87e-141">In this section, you create a Java console app that invokes a direct method and then displays the response.</span></span> <span data-ttu-id="fa87e-142">此主控台應用程式會連線到您的 IoT 中樞來叫用直接方法。</span><span class="sxs-lookup"><span data-stu-id="fa87e-142">This console app connects to your IoT Hub to invoke the direct method.</span></span>

1. <span data-ttu-id="fa87e-143">在 iot-java-direct-method 資料夾的命令提示字元下，使用下列命令建立名為 **invoke-direct-method** 的 Maven 專案。</span><span class="sxs-lookup"><span data-stu-id="fa87e-143">In the iot-java-direct-method folder, create a Maven project called **invoke-direct-method** using the following command at your command prompt.</span></span> <span data-ttu-id="fa87e-144">下列命令是完整的單一命令：</span><span class="sxs-lookup"><span data-stu-id="fa87e-144">The following command is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=invoke-direct-method -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="fa87e-145">在命令提示字元中，瀏覽到 invoke-direct-method 資料夾。</span><span class="sxs-lookup"><span data-stu-id="fa87e-145">At your command prompt, navigate to the invoke-direct-method folder.</span></span>

1. <span data-ttu-id="fa87e-146">使用文字編輯器，在 invoke-direct-method 資料夾中將 pom.xml 檔案開啟，並對 [相依性] 節點新增下列相依性。</span><span class="sxs-lookup"><span data-stu-id="fa87e-146">Using a text editor, open the pom.xml file in the invoke-direct-method folder and add the following dependency to the **dependencies** node.</span></span> <span data-ttu-id="fa87e-147">這個相依性可讓您在應用程式中使用 iot-service-client 套件與 IoT 中樞通訊：</span><span class="sxs-lookup"><span data-stu-id="fa87e-147">This dependency enables you to use the iot-service-client package in your app to communicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
      <type>jar</type>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="fa87e-148">您可以使用 [Maven 搜尋][lnk-maven-service-search]來檢查最新版的 **iot-service-client**。</span><span class="sxs-lookup"><span data-stu-id="fa87e-148">You can check for the latest version of **iot-service-client** using [Maven search][lnk-maven-service-search].</span></span>

1. <span data-ttu-id="fa87e-149">將下列 [建置] 節點新增至 [相依性] 節點之後。</span><span class="sxs-lookup"><span data-stu-id="fa87e-149">Add the following **build** node after the **dependencies** node.</span></span> <span data-ttu-id="fa87e-150">此設定會指示 Maven 使用 Java 1.8 來建置應用程式：</span><span class="sxs-lookup"><span data-stu-id="fa87e-150">This configuration instructs Maven to use Java 1.8 to build the app:</span></span>

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

1. <span data-ttu-id="fa87e-151">儲存並關閉 pom.xml 檔案。</span><span class="sxs-lookup"><span data-stu-id="fa87e-151">Save and close the pom.xml file.</span></span>

1. <span data-ttu-id="fa87e-152">使用文字編輯器開啟 invoke-direct-method\src\main\java\com\mycompany\app\App.java 檔案。</span><span class="sxs-lookup"><span data-stu-id="fa87e-152">Using a text editor, open the invoke-direct-method\src\main\java\com\mycompany\app\App.java file.</span></span>

1. <span data-ttu-id="fa87e-153">在此檔案中新增下列 **import** 陳述式：</span><span class="sxs-lookup"><span data-stu-id="fa87e-153">Add the following **import** statements to the file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.service.devicetwin.DeviceMethod;
    import com.microsoft.azure.sdk.iot.service.devicetwin.MethodResult;
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;

    import java.io.IOException;
    import java.util.concurrent.TimeUnit;
    ```

1. <span data-ttu-id="fa87e-154">將下列類別層級變數新增到 **App** 類別中。</span><span class="sxs-lookup"><span data-stu-id="fa87e-154">Add the following class-level variables to the **App** class.</span></span> <span data-ttu-id="fa87e-155">以您在＜建立 IoT 中樞＞一節中所記下的 IoT 中樞連接字串取代 `{youriothubconnectionstring}`：</span><span class="sxs-lookup"><span data-stu-id="fa87e-155">Replace `{youriothubconnectionstring}` with your IoT hub connection string you noted in the *Create an IoT Hub* section:</span></span>

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    public static final String methodName = "writeLine";
    public static final Long responseTimeout = TimeUnit.SECONDS.toSeconds(30);
    public static final Long connectTimeout = TimeUnit.SECONDS.toSeconds(5);
    public static final String payload = "a line to be written";
    ```

1. <span data-ttu-id="fa87e-156">若要在模擬的裝置上叫用方法，請將下列程式碼新增至 **main** 方法：</span><span class="sxs-lookup"><span data-stu-id="fa87e-156">To invoke the method on the simulated device, add the following code to the **main** method:</span></span>

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

1. <span data-ttu-id="fa87e-157">儲存並關閉 invoke-direct-method\src\main\java\com\mycompany\app\App.java 檔案</span><span class="sxs-lookup"><span data-stu-id="fa87e-157">Save and close the invoke-direct-method\src\main\java\com\mycompany\app\App.java file</span></span>

1. <span data-ttu-id="fa87e-158">建置 **invoke-direct-method** 應用程式，並更正所有錯誤。</span><span class="sxs-lookup"><span data-stu-id="fa87e-158">Build the **invoke-direct-method** app and correct any errors.</span></span> <span data-ttu-id="fa87e-159">在命令提示字元中，巡覽至 invoke-direct-method 資料夾，並執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="fa87e-159">At your command prompt, navigate to the invoke-direct-method folder and run the following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="run-the-apps"></a><span data-ttu-id="fa87e-160">執行應用程式</span><span class="sxs-lookup"><span data-stu-id="fa87e-160">Run the apps</span></span>

<span data-ttu-id="fa87e-161">您現在已經準備好執行主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="fa87e-161">You are now ready to run the console apps.</span></span>

1. <span data-ttu-id="fa87e-162">在 simulated-device 資料夾的命令提示字元中，執行下列命令以開始接聽來自您 IoT 中樞的方法呼叫：</span><span class="sxs-lookup"><span data-stu-id="fa87e-162">At a command prompt in the simulated-device folder, run the following command to begin listening for method calls from your IoT hub:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![會接聽直接方法呼叫的 Java IoT 中樞模擬裝置應用程式][8]

1. <span data-ttu-id="fa87e-164">在 invoke-direct-method 資料夾的命令提示字元中，執行下列命令以呼叫您模擬裝置上來自 IoT 中樞的方法：</span><span class="sxs-lookup"><span data-stu-id="fa87e-164">At a command prompt in the invoke-direct-method folder, run the following command to call a method on your simulated device from your IoT hub:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![會呼叫直接方法的 Java IoT 中樞服務應用程式][7]

1. <span data-ttu-id="fa87e-166">會回應直接方法呼叫的模擬裝置︰</span><span class="sxs-lookup"><span data-stu-id="fa87e-166">The simulated device responds to the direct method call:</span></span>

    ![Java IoT 中樞模擬裝置會回應直接方法呼叫][9]

## <a name="next-steps"></a><span data-ttu-id="fa87e-168">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fa87e-168">Next steps</span></span>

<span data-ttu-id="fa87e-169">在此教學課程中，您在 Azure 入口網站中設定了新的 IoT 中樞，然後在 IoT 中樞的身分識別登錄中建立了裝置身分識別。</span><span class="sxs-lookup"><span data-stu-id="fa87e-169">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="fa87e-170">您會將此裝置識別用於啟用模擬的裝置應用程式，以將雲端所叫用的方法進行反應。</span><span class="sxs-lookup"><span data-stu-id="fa87e-170">You used this device identity to enable the simulated device app to react to methods invoked by the cloud.</span></span> <span data-ttu-id="fa87e-171">您也會建立應用程式，在裝置上叫用方法，並且顯示來自裝置的回應。</span><span class="sxs-lookup"><span data-stu-id="fa87e-171">You also created an app that invokes methods on the device and displays the response from the device.</span></span>

<span data-ttu-id="fa87e-172">若要瀏覽其他的 IoT 案例，請參閱[排程多個裝置上的作業][lnk-devguide-jobs]。</span><span class="sxs-lookup"><span data-stu-id="fa87e-172">To explore other IoT scenarios, see [Schedule jobs on multiple devices][lnk-devguide-jobs].</span></span>

<span data-ttu-id="fa87e-173">若要了解如何擴充您的 IoT 解決方案以及在多個裝置上排程方法呼叫，請參閱[排程及廣播作業][lnk-tutorial-jobs]教學課程。</span><span class="sxs-lookup"><span data-stu-id="fa87e-173">To learn how to extend your IoT solution and schedule method calls on multiple devices, see the [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

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
