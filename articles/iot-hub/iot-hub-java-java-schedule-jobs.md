---
title: "使用 Azure IoT 中樞 (Java) 排定作業 | Microsoft Docs"
description: "如何排定 Azure IoT 中樞作業在多個裝置上叫用直接方法和設定所需屬性。 您可以使用適用於 Java 的 Azure IoT 裝置 SDK，實作模擬裝置應用程式，也可以使用適用於 Java 的 Azure IoT 服務 SDK，實作服務應用程式以執行作業。"
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
ms.date: 07/10/2017
ms.author: dobett
ms.openlocfilehash: 003a548ef2da2921a699df1aa9f7aee366d341ab
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="schedule-and-broadcast-jobs-java"></a><span data-ttu-id="675d5-104">排定及廣播作業 (Java)</span><span class="sxs-lookup"><span data-stu-id="675d5-104">Schedule and broadcast jobs (Java)</span></span>

[!INCLUDE [iot-hub-selector-schedule-jobs](../../includes/iot-hub-selector-schedule-jobs.md)]

<span data-ttu-id="675d5-105">使用 Azure IoT 中樞排程和追蹤會更新數百萬部裝置的作業。</span><span class="sxs-lookup"><span data-stu-id="675d5-105">Use Azure IoT Hub to schedule and track jobs that update millions of devices.</span></span> <span data-ttu-id="675d5-106">使用作業以：</span><span class="sxs-lookup"><span data-stu-id="675d5-106">Use jobs to:</span></span>

* <span data-ttu-id="675d5-107">更新所需屬性</span><span class="sxs-lookup"><span data-stu-id="675d5-107">Update desired properties</span></span>
* <span data-ttu-id="675d5-108">更新標籤</span><span class="sxs-lookup"><span data-stu-id="675d5-108">Update tags</span></span>
* <span data-ttu-id="675d5-109">叫用直接方法</span><span class="sxs-lookup"><span data-stu-id="675d5-109">Invoke direct methods</span></span>

<span data-ttu-id="675d5-110">作業會包裝上述其中一個動作，然後針對一組裝置追蹤執行進度。</span><span class="sxs-lookup"><span data-stu-id="675d5-110">A job wraps one of these actions and tracks the execution against a set of devices.</span></span> <span data-ttu-id="675d5-111">裝置對應項查詢會定義對其執行作業的一組裝置。</span><span class="sxs-lookup"><span data-stu-id="675d5-111">A device twin query defines the set of devices the job executes against.</span></span> <span data-ttu-id="675d5-112">例如，後端應用程式可以使用作業，以在 10,000 部裝置上叫用重新開機裝置的直接方法。</span><span class="sxs-lookup"><span data-stu-id="675d5-112">For example, a back-end app can use a job to invoke a direct method on 10,000 devices that reboots the devices.</span></span> <span data-ttu-id="675d5-113">您以裝置對應項查詢指定一組裝置，並排程在未來的時間執行作業。</span><span class="sxs-lookup"><span data-stu-id="675d5-113">You specify the set of devices with a device twin query and schedule the job to run at a future time.</span></span> <span data-ttu-id="675d5-114">作業會在每部裝置接收和執行重新開機直接方法時追蹤進度。</span><span class="sxs-lookup"><span data-stu-id="675d5-114">The job tracks progress as each of the devices receive and execute the reboot direct method.</span></span>

<span data-ttu-id="675d5-115">若要一一了解這些功能，請參閱：</span><span class="sxs-lookup"><span data-stu-id="675d5-115">To learn more about each of these capabilities, see:</span></span>

* <span data-ttu-id="675d5-116">裝置對應項和屬性：[開始使用裝置對應項](iot-hub-java-java-twin-getstarted.md)</span><span class="sxs-lookup"><span data-stu-id="675d5-116">Device twin and properties: [Get started with device twins](iot-hub-java-java-twin-getstarted.md)</span></span>
* <span data-ttu-id="675d5-117">直接方法：[IoT 中樞開發人員指南 - 直接方法](iot-hub-devguide-direct-methods.md)和[教學課程：使用直接方法](iot-hub-java-java-direct-methods.md)</span><span class="sxs-lookup"><span data-stu-id="675d5-117">Direct methods: [IoT Hub developer guide - direct methods](iot-hub-devguide-direct-methods.md) and [Tutorial: Use direct methods](iot-hub-java-java-direct-methods.md)</span></span>

<span data-ttu-id="675d5-118">本教學課程說明如何：</span><span class="sxs-lookup"><span data-stu-id="675d5-118">This tutorial shows you how to:</span></span>

* <span data-ttu-id="675d5-119">建立實作 **lockDoor** 直接方法的裝置應用程式。</span><span class="sxs-lookup"><span data-stu-id="675d5-119">Create a device app that implements a direct method called **lockDoor**.</span></span> <span data-ttu-id="675d5-120">裝置應用程式也會從後端應用程式收到所需的屬性變更。</span><span class="sxs-lookup"><span data-stu-id="675d5-120">The device app also receives desired property changes from the back-end app.</span></span>
* <span data-ttu-id="675d5-121">建立後端應用程式，以建立作業在多部裝置上呼叫 **lockDoor** 直接方法。</span><span class="sxs-lookup"><span data-stu-id="675d5-121">Create a back-end app that creates a job to call the **lockDoor** direct method on multiple devices.</span></span> <span data-ttu-id="675d5-122">另一項作業會將所需的屬性更新傳送到多部裝置。</span><span class="sxs-lookup"><span data-stu-id="675d5-122">Another job sends desired property updates to multiple devices.</span></span>

<span data-ttu-id="675d5-123">在本教學課程結束時，您會有 Java 主控台裝置應用程式和 Java 主控台後端應用程式：</span><span class="sxs-lookup"><span data-stu-id="675d5-123">At the end of this tutorial, you have a java console device app and a java console back-end app:</span></span>

<span data-ttu-id="675d5-124">**simulated-device** 會連線至 IoT 中樞，實作 **lockDoor** 直接方法，並處理所需的屬性變更。</span><span class="sxs-lookup"><span data-stu-id="675d5-124">**simulated-device** that connects to your IoT hub, implements the **lockDoor** direct method, and handles desired property changes.</span></span>

<span data-ttu-id="675d5-125">**schedule-jobs** 會使用作業呼叫 **lockDoor** 直接方法，並在多部裝置上更新裝置對應項所需的屬性。</span><span class="sxs-lookup"><span data-stu-id="675d5-125">**schedule-jobs** that use jobs to call the **lockDoor** direct method and update the device twin desired properties on multiple devices.</span></span>

> [!NOTE]
> <span data-ttu-id="675d5-126">[Azure IoT SDK](iot-hub-devguide-sdks.md) 一文提供可用來建置裝置和後端應用程式之 Azure IoT SDK 的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="675d5-126">The article [Azure IoT SDKs](iot-hub-devguide-sdks.md) provides information about the Azure IoT SDKs that you can use to build both device and back-end apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="675d5-127">必要條件</span><span class="sxs-lookup"><span data-stu-id="675d5-127">Prerequisites</span></span>

<span data-ttu-id="675d5-128">若要完成本教學課程，您需要：</span><span class="sxs-lookup"><span data-stu-id="675d5-128">To complete this tutorial, you need:</span></span>

* <span data-ttu-id="675d5-129">最新的 [Java SE 開發套件 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span><span class="sxs-lookup"><span data-stu-id="675d5-129">The latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span>
* [<span data-ttu-id="675d5-130">Maven 3</span><span class="sxs-lookup"><span data-stu-id="675d5-130">Maven 3</span></span>](https://maven.apache.org/install.html)
* <span data-ttu-id="675d5-131">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="675d5-131">An active Azure account.</span></span> <span data-ttu-id="675d5-132">(如果您沒有帳戶，只需要幾分鐘的時間就可以建立[免費帳戶](http://azure.microsoft.com/pricing/free-trial/)。)</span><span class="sxs-lookup"><span data-stu-id="675d5-132">(If you don't have an account, you can create a [free account](http://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

<span data-ttu-id="675d5-133">如果您更想要以程式設計方式建立裝置身分識別，請閱讀[使用 Java 將您的裝置連線至 IoT 中樞](iot-hub-java-java-getstarted.md#create-a-device-identity)一文中的對應章節。</span><span class="sxs-lookup"><span data-stu-id="675d5-133">If you prefer to create the device identity programmatically, read the corresponding section in the [Connect your device to your IoT hub using Java](iot-hub-java-java-getstarted.md#create-a-device-identity) article.</span></span> <span data-ttu-id="675d5-134">您也可以使用 [iothub-explorer](https://github.com/Azure/iothub-explorer) 工具，將裝置新增至您的 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="675d5-134">You can also use the [iothub-explorer](https://github.com/Azure/iothub-explorer) tool to add a device to your IoT hub.</span></span>

## <a name="create-the-service-app"></a><span data-ttu-id="675d5-135">建立服務應用程式</span><span class="sxs-lookup"><span data-stu-id="675d5-135">Create the service app</span></span>

<span data-ttu-id="675d5-136">在本節中，您將建立 Java 主控台應用程式，使用作業以：</span><span class="sxs-lookup"><span data-stu-id="675d5-136">In this section, you create a Java console app that uses jobs to:</span></span>

* <span data-ttu-id="675d5-137">在多個裝置上呼叫 **lockDoor** 直接方法。</span><span class="sxs-lookup"><span data-stu-id="675d5-137">Call the **lockDoor** direct method on multiple devices.</span></span>
* <span data-ttu-id="675d5-138">將所需屬性傳送至多個裝置。</span><span class="sxs-lookup"><span data-stu-id="675d5-138">Send desired properties to multiple devices.</span></span>

<span data-ttu-id="675d5-139">若要建立應用程式：</span><span class="sxs-lookup"><span data-stu-id="675d5-139">To create the app:</span></span>

1. <span data-ttu-id="675d5-140">在您的開發電腦上建立名為 `iot-java-schedule-jobs` 的空資料夾。</span><span class="sxs-lookup"><span data-stu-id="675d5-140">On your development machine, create an empty folder called `iot-java-schedule-jobs`.</span></span>

1. <span data-ttu-id="675d5-141">在 `iot-java-schedule-jobs` 資料夾中，在命令提示字元中使用下列命令，建立名為 **schedule-jobs** 的 Maven 專案。</span><span class="sxs-lookup"><span data-stu-id="675d5-141">In the `iot-java-schedule-jobs` folder, create a Maven project called **schedule-jobs** using the following command at your command prompt.</span></span> <span data-ttu-id="675d5-142">注意，這是一個單一且非常長的命令：</span><span class="sxs-lookup"><span data-stu-id="675d5-142">Note this is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=schedule-jobs -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="675d5-143">在命令提示字元中，巡覽至 `schedule-jobs` 資料夾。</span><span class="sxs-lookup"><span data-stu-id="675d5-143">At your command prompt, navigate to the `schedule-jobs` folder.</span></span>

1. <span data-ttu-id="675d5-144">使用文字編輯器，開啟 `schedule-jobs` 資料夾中的 `pom.xml` 檔案，並在 [相依性] 節點中新增下列相依性。</span><span class="sxs-lookup"><span data-stu-id="675d5-144">Using a text editor, open the `pom.xml` file in the `schedule-jobs` folder and add the following dependency to the **dependencies** node.</span></span> <span data-ttu-id="675d5-145">這個相依性可讓您在應用程式中使用 **iot-service-client** 套件與 IoT 中樞通訊：</span><span class="sxs-lookup"><span data-stu-id="675d5-145">This dependency enables you to use the **iot-service-client** package in your app to communicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
      <type>jar</type>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="675d5-146">您可以使用 [Maven 搜尋](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22)來檢查最新版的 **iot-service-client**。</span><span class="sxs-lookup"><span data-stu-id="675d5-146">You can check for the latest version of **iot-service-client** using [Maven search](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span></span>

1. <span data-ttu-id="675d5-147">將下列 [建置] 節點新增至 [相依性] 節點之後。</span><span class="sxs-lookup"><span data-stu-id="675d5-147">Add the following **build** node after the **dependencies** node.</span></span> <span data-ttu-id="675d5-148">此設定會指示 Maven 使用 Java 1.8 來建置應用程式：</span><span class="sxs-lookup"><span data-stu-id="675d5-148">This configuration instructs Maven to use Java 1.8 to build the app:</span></span>

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

1. <span data-ttu-id="675d5-149">儲存並關閉 `pom.xml` 檔案。</span><span class="sxs-lookup"><span data-stu-id="675d5-149">Save and close the `pom.xml` file.</span></span>

1. <span data-ttu-id="675d5-150">使用文字編輯器開啟 `schedule-jobs\src\main\java\com\mycompany\app\App.java` 檔案。</span><span class="sxs-lookup"><span data-stu-id="675d5-150">Using a text editor, open the `schedule-jobs\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="675d5-151">在此檔案中新增下列 **import** 陳述式：</span><span class="sxs-lookup"><span data-stu-id="675d5-151">Add the following **import** statements to the file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.service.devicetwin.DeviceTwinDevice;
    import com.microsoft.azure.sdk.iot.service.devicetwin.Pair;
    import com.microsoft.azure.sdk.iot.service.devicetwin.Query;
    import com.microsoft.azure.sdk.iot.service.devicetwin.SqlQuery;
    import com.microsoft.azure.sdk.iot.service.jobs.JobClient;
    import com.microsoft.azure.sdk.iot.service.jobs.JobResult;
    import com.microsoft.azure.sdk.iot.service.jobs.JobStatus;

    import java.util.Date;
    import java.time.Instant;
    import java.util.HashSet;
    import java.util.Set;
    import java.util.UUID;
    ```

1. <span data-ttu-id="675d5-152">將下列類別層級變數新增到 **App** 類別中。</span><span class="sxs-lookup"><span data-stu-id="675d5-152">Add the following class-level variables to the **App** class.</span></span> <span data-ttu-id="675d5-153">以您在＜建立 IoT 中樞＞一節中所記下的 IoT 中樞連接字串取代 `{youriothubconnectionstring}`：</span><span class="sxs-lookup"><span data-stu-id="675d5-153">Replace `{youriothubconnectionstring}` with your IoT hub connection string you noted in the *Create an IoT Hub* section:</span></span>

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    // How long the job is permitted to run without
    // completing its work on the set of devices
    private static final long maxExecutionTimeInSeconds = 30;
    ```

1. <span data-ttu-id="675d5-154">將下列方法新增至 **App** 類別，排程作業以更新裝置對應項中的 **Building** 和 **Floor** 所需屬性：</span><span class="sxs-lookup"><span data-stu-id="675d5-154">Add the following method to the **App** class to schedule a job to update the **Building** and **Floor** desired properties in the device twin:</span></span>

    ```java
    private static JobResult scheduleJobSetDesiredProperties(JobClient jobClient, String jobId) {
      DeviceTwinDevice twin = new DeviceTwinDevice(deviceId);
      Set<Pair> desiredProperties = new HashSet<Pair>();
      desiredProperties.add(new Pair("Building", 43));
      desiredProperties.add(new Pair("Floor", 3));
      twin.setDesiredProperties(desiredProperties);
      // Optimistic concurrency control
      twin.setETag("*");

      // Schedule the update twin job to run now
      // against a single device
      System.out.println("Schedule job " + jobId + " for device " + deviceId);
      try {
        JobResult jobResult = jobClient.scheduleUpdateTwin(jobId, 
          "deviceId='" + deviceId + "'",
          twin,
          new Date(),
          maxExecutionTimeInSeconds);
        return jobResult;
      } catch (Exception e) {
        System.out.println("Exception scheduling desired properties job: " + jobId);
        System.out.println(e.getMessage());
        return null;
      }
    }
    ```

1. <span data-ttu-id="675d5-155">若要排程作業以呼叫 **lockDoor** 方法，將下列方法新增至 **App** 類別：</span><span class="sxs-lookup"><span data-stu-id="675d5-155">To schedule a job to call the **lockDoor** method, add the following method to the **App** class:</span></span>

    ```java
    private static JobResult scheduleJobCallDirectMethod(JobClient jobClient, String jobId) {
      // Schedule a job now to call the lockDoor direct method
      // against a single device. Response and connection
      // timeouts are set to 5 seconds.
      System.out.println("Schedule job " + jobId + " for device " + deviceId);
      try {
        JobResult jobResult = jobClient.scheduleDeviceMethod(jobId,
          "deviceId='" + deviceId + "'",
          "lockDoor",
          5L, 5L, null,
          new Date(),
          maxExecutionTimeInSeconds);
        return jobResult;
      } catch (Exception e) {
        System.out.println("Exception scheduling direct method job: " + jobId);
        System.out.println(e.getMessage());
        return null;
      }
    };
    ```

1. <span data-ttu-id="675d5-156">若要監視作業，將下列方法新增至 **App** 類別：</span><span class="sxs-lookup"><span data-stu-id="675d5-156">To monitor a job, add the following method to the **App** class:</span></span>

    ```java
    private static void monitorJob(JobClient jobClient, String jobId) {
      try {
        JobResult jobResult = jobClient.getJob(jobId);
        if(jobResult == null)
        {
          System.out.println("No JobResult for: " + jobId);
          return;
        }
        // Check the job result until it's completed
        while(jobResult.getJobStatus() != JobStatus.completed)
        {
          Thread.sleep(100);
          jobResult = jobClient.getJob(jobId);
          System.out.println("Status " + jobResult.getJobStatus() + " for job " + jobId);
        }
        System.out.println("Final status " + jobResult.getJobStatus() + " for job " + jobId);
      } catch (Exception e) {
        System.out.println("Exception monitoring job: " + jobId);
        System.out.println(e.getMessage());
        return;
      }
    }
    ```

1. <span data-ttu-id="675d5-157">若要查詢您執行之作業的詳細資料，請新增下列方法：</span><span class="sxs-lookup"><span data-stu-id="675d5-157">To query for the details of the jobs you ran, add the following method:</span></span>

    ```java
    private static void queryDeviceJobs(JobClient jobClient, String start) throws Exception {
      System.out.println("\nQuery device jobs since " + start);

      // Create a jobs query using the time the jobs started
      Query deviceJobQuery = jobClient
          .queryDeviceJob(SqlQuery.createSqlQuery("*", SqlQuery.FromType.JOBS, "devices.jobs.startTimeUtc > '" + start + "'", null).getQuery());

      // Iterate over the list of jobs and print the details
      while (jobClient.hasNextJob(deviceJobQuery)) {
        System.out.println(jobClient.getNextJob(deviceJobQuery));
      }
    }
    ```

1. <span data-ttu-id="675d5-158">更新 **Main** 方法簽章，以包含下列 `throws` 子句：</span><span class="sxs-lookup"><span data-stu-id="675d5-158">Update the **main** method signature to include the following `throws` clause:</span></span>

    ```java
    public static void main( String[] args ) throws Exception
    ```

1. <span data-ttu-id="675d5-159">若要循序執行及監視兩個作業，請將下列程式碼新增至 **main** 方法：</span><span class="sxs-lookup"><span data-stu-id="675d5-159">To run and monitor two jobs sequentially, add the following code to the **main** method:</span></span>

    ```java
    // Record the start time
    String start = Instant.now().toString();

    // Create JobClient
    JobClient jobClient = JobClient.createFromConnectionString(iotHubConnectionString);
    System.out.println("JobClient created with success");

    // Schedule twin job desired properties
    // Maximum concurrent jobs is 1 for Free and S1 tiers
    String desiredPropertiesJobId = "DPCMD" + UUID.randomUUID();
    scheduleJobSetDesiredProperties(jobClient, desiredPropertiesJobId);
    monitorJob(jobClient, desiredPropertiesJobId);

    // Schedule twin job direct method
    String directMethodJobId = "DMCMD" + UUID.randomUUID();
    scheduleJobCallDirectMethod(jobClient, directMethodJobId);
    monitorJob(jobClient, directMethodJobId);

    // Run a query to show the job detail
    queryDeviceJobs(jobClient, start);

    System.out.println("Shutting down schedule-jobs app");
    ```

1. <span data-ttu-id="675d5-160">儲存並關閉 `schedule-jobs\src\main\java\com\mycompany\app\App.java` 檔案。</span><span class="sxs-lookup"><span data-stu-id="675d5-160">Save and close the `schedule-jobs\src\main\java\com\mycompany\app\App.java` file</span></span>

1. <span data-ttu-id="675d5-161">建置 **schedule-jobs** 應用程式，並更正所有錯誤。</span><span class="sxs-lookup"><span data-stu-id="675d5-161">Build the **schedule-jobs** app and correct any errors.</span></span> <span data-ttu-id="675d5-162">在命令提示字元中，巡覽至 `schedule-jobs` 資料夾，並執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="675d5-162">At your command prompt, navigate to the `schedule-jobs` folder and run the following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="create-a-device-app"></a><span data-ttu-id="675d5-163">建立裝置應用程式</span><span class="sxs-lookup"><span data-stu-id="675d5-163">Create a device app</span></span>

<span data-ttu-id="675d5-164">在本節中，您會建立 Java 主控台應用程式來處理從 IoT 中樞傳送的所需屬性，以及實作直接方法呼叫。</span><span class="sxs-lookup"><span data-stu-id="675d5-164">In this section, you create a Java console app that handles the desired properties sent from IoT Hub and implements the direct method call.</span></span>

1. <span data-ttu-id="675d5-165">在 `iot-java-schedule-jobs` 資料夾中，在命令提示字元中使用下列命令，建立名為 **simulated-device** 的 Maven 專案。</span><span class="sxs-lookup"><span data-stu-id="675d5-165">In the `iot-java-schedule-jobs` folder, create a Maven project called **simulated-device** using the following command at your command prompt.</span></span> <span data-ttu-id="675d5-166">注意，這是一個單一且非常長的命令：</span><span class="sxs-lookup"><span data-stu-id="675d5-166">Note this is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="675d5-167">在命令提示字元中，巡覽至 `simulated-device` 資料夾。</span><span class="sxs-lookup"><span data-stu-id="675d5-167">At your command prompt, navigate to the `simulated-device` folder.</span></span>

1. <span data-ttu-id="675d5-168">使用文字編輯器，開啟 `simulated-device` 資料夾中的 `pom.xml` 檔案，並在 [相依性] 節點中新增下列相依性。</span><span class="sxs-lookup"><span data-stu-id="675d5-168">Using a text editor, open the `pom.xml` file in the `simulated-device` folder and add the following dependencies to the **dependencies** node.</span></span> <span data-ttu-id="675d5-169">這個相依性可讓您在應用程式中使用 **iot-device-client** 套件與 IoT 中樞通訊：</span><span class="sxs-lookup"><span data-stu-id="675d5-169">This dependency enables you to use the **iot-device-client** package in your app to communicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="675d5-170">您可以使用 [Maven 搜尋](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22)來檢查最新版的 **iot-device-client**。</span><span class="sxs-lookup"><span data-stu-id="675d5-170">You can check for the latest version of **iot-device-client** using [Maven search](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span></span>

1. <span data-ttu-id="675d5-171">將下列 [建置] 節點新增至 [相依性] 節點之後。</span><span class="sxs-lookup"><span data-stu-id="675d5-171">Add the following **build** node after the **dependencies** node.</span></span> <span data-ttu-id="675d5-172">此設定會指示 Maven 使用 Java 1.8 來建置應用程式：</span><span class="sxs-lookup"><span data-stu-id="675d5-172">This configuration instructs Maven to use Java 1.8 to build the app:</span></span>

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

1. <span data-ttu-id="675d5-173">儲存並關閉 `pom.xml` 檔案。</span><span class="sxs-lookup"><span data-stu-id="675d5-173">Save and close the `pom.xml` file.</span></span>

1. <span data-ttu-id="675d5-174">使用文字編輯器開啟 `simulated-device\src\main\java\com\mycompany\app\App.java` 檔案。</span><span class="sxs-lookup"><span data-stu-id="675d5-174">Using a text editor, open the `simulated-device\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="675d5-175">在此檔案中新增下列 **import** 陳述式：</span><span class="sxs-lookup"><span data-stu-id="675d5-175">Add the following **import** statements to the file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.microsoft.azure.sdk.iot.device.DeviceTwin.*;

    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.util.Scanner;
    ```

1. <span data-ttu-id="675d5-176">將下列類別層級變數新增到 **App** 類別中。</span><span class="sxs-lookup"><span data-stu-id="675d5-176">Add the following class-level variables to the **App** class.</span></span> <span data-ttu-id="675d5-177">以您的 IoT 中樞名稱取代 `{youriothubname}`，並以您在＜建立裝置身分識別＞一節中產生的裝置金鑰值取代 `{yourdevicekey}`：</span><span class="sxs-lookup"><span data-stu-id="675d5-177">Replacing `{youriothubname}` with your IoT hub name, and `{yourdevicekey}` with the device key value you generated in the *Create a device identity* section:</span></span>

    ```java
    private static String connString = "HostName={youriothubname}.azure-devices.net;DeviceId=myDeviceID;SharedAccessKey={yourdevicekey}";
    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static final int METHOD_SUCCESS = 200;
    private static final int METHOD_NOT_DEFINED = 404;
    ```

    <span data-ttu-id="675d5-178">此範例應用程式在具現化 **DeviceClient** 物件時使用 **protocol** 變數。</span><span class="sxs-lookup"><span data-stu-id="675d5-178">This sample app uses the **protocol** variable when it instantiates a **DeviceClient** object.</span></span> <span data-ttu-id="675d5-179">目前，若要使用裝置對應項功能，您必須使用 MQTT 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="675d5-179">Currently, to use device twin features you must use the MQTT protocol.</span></span>

1. <span data-ttu-id="675d5-180">若要將裝置對應項通知列印至主控台，請在 **App** 類別中新增下列巢狀類別：</span><span class="sxs-lookup"><span data-stu-id="675d5-180">To print device twin notifications to the console, add the following nested class to the **App** class:</span></span>

    ```java
    // Handler for device twin operation notifications from IoT Hub
    protected static class DeviceTwinStatusCallBack implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded to device twin operation with status " + status.name());
      }
    }
    ```

1. <span data-ttu-id="675d5-181">若要將直接方法通知列印至主控台，請在 **App** 類別中新增下列巢狀類別：</span><span class="sxs-lookup"><span data-stu-id="675d5-181">To print direct method notifications to the console, add the following nested class to the **App** class:</span></span>

    ```java
    // Handler for direct method notifications from IoT Hub
    protected static class DirectMethodStatusCallback implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded to direct method operation with status " + status.name());
      }
    }
    ```

1. <span data-ttu-id="675d5-182">若要處理來自 IoT 中樞的直接方法呼叫，請在 **App** 類別中新增下列巢狀類別：</span><span class="sxs-lookup"><span data-stu-id="675d5-182">To handle direct method calls from IoT Hub, add the following nested class to the **App** class:</span></span>

    ```java
    // Handler for direct method calls from IoT Hub
    protected static class DirectMethodCallback
        implements DeviceMethodCallback {
      @Override
      public DeviceMethodData call(String methodName, Object methodData, Object context) {
        DeviceMethodData deviceMethodData;
        switch (methodName) {
          case "lockDoor": {
            System.out.println("Executing direct method: " + methodName);
            deviceMethodData = new DeviceMethodData(METHOD_SUCCESS, "Executed direct method " + methodName);
            break;
          }
          default: {
            deviceMethodData = new DeviceMethodData(METHOD_NOT_DEFINED, "Not defined direct method " + methodName);
          }
        }
        // Notify IoT Hub of result
        return deviceMethodData;
      }
    }
    ```

1. <span data-ttu-id="675d5-183">更新 **Main** 方法簽章，以包含下列 `throws` 子句：</span><span class="sxs-lookup"><span data-stu-id="675d5-183">Update the **main** method signature to include the following `throws` clause:</span></span>

    ```java
    public static void main( String[] args ) throws IOException, URISyntaxException
    ```

1. <span data-ttu-id="675d5-184">將以下程式碼新增至 **Main** 方法，以：</span><span class="sxs-lookup"><span data-stu-id="675d5-184">Add the following code to the **main** method to:</span></span>
    * <span data-ttu-id="675d5-185">建立與 IoT 中樞通訊的裝置用戶端。</span><span class="sxs-lookup"><span data-stu-id="675d5-185">Create a device client to communicate with IoT Hub.</span></span>
    * <span data-ttu-id="675d5-186">建立**裝置**物件以儲存裝置對應項屬性。</span><span class="sxs-lookup"><span data-stu-id="675d5-186">Create a **Device** object to store the device twin properties.</span></span>

    ```java
    // Create a device client
    DeviceClient client = new DeviceClient(connString, protocol);

    // An object to manage device twin desired and reported properties
    Device dataCollector = new Device() {
      @Override
      public void PropertyCall(String propertyKey, Object propertyValue, Object context)
      {
        System.out.println("Received desired property change: " + propertyKey + " " + propertyValue);
      }
    };
    ```

1. <span data-ttu-id="675d5-187">若要啟動裝置用戶端服務，請將下列程式碼新增至 **main** 方法：</span><span class="sxs-lookup"><span data-stu-id="675d5-187">To start the device client services, add the following code to the **main** method:</span></span>

    ```java
    try {
      // Open the DeviceClient
      // Start the device twin services
      // Subscribe to direct method calls
      client.open();
      client.startDeviceTwin(new DeviceTwinStatusCallBack(), null, dataCollector, null);
      client.subscribeToDeviceMethod(new DirectMethodCallback(), null, new DirectMethodStatusCallback(), null);
    } catch (Exception e) {
      System.out.println("Exception, shutting down \n" + " Cause: " + e.getCause() + " \n" + e.getMessage());
      dataCollector.clean();
      client.closeNow();
      System.out.println("Shutting down...");
    }
    ```

1. <span data-ttu-id="675d5-188">若要在關閉之前等候使用者按下 **Enter** 鍵，請將下列程式碼新增至 **main** 方法的結尾：</span><span class="sxs-lookup"><span data-stu-id="675d5-188">To wait for the user to press the **Enter** key before shutting down, add the following code to the end of the **main** method:</span></span>

    ```java
    // Close the app
    System.out.println("Press any key to exit...");
    Scanner scanner = new Scanner(System.in);
    scanner.nextLine();
    dataCollector.clean();
    client.closeNow();
    scanner.close();
    ```

1. <span data-ttu-id="675d5-189">儲存並關閉 `simulated-device\src\main\java\com\mycompany\app\App.java` 檔案。</span><span class="sxs-lookup"><span data-stu-id="675d5-189">Save and close the `simulated-device\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="675d5-190">建置 **simulated-device** 應用程式，並更正所有錯誤。</span><span class="sxs-lookup"><span data-stu-id="675d5-190">Build the **simulated-device** app and correct any errors.</span></span> <span data-ttu-id="675d5-191">在命令提示字元中，巡覽至 `simulated-device` 資料夾，並執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="675d5-191">At your command prompt, navigate to the `simulated-device` folder and run the following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="run-the-apps"></a><span data-ttu-id="675d5-192">執行應用程式</span><span class="sxs-lookup"><span data-stu-id="675d5-192">Run the apps</span></span>

<span data-ttu-id="675d5-193">您現在已經準備好執行主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="675d5-193">You are now ready to run the console apps.</span></span>

1. <span data-ttu-id="675d5-194">在 `simulated-device` 資料夾的命令提示字元中，執行下列命令以啟動裝置應用程式，接聽所需屬性變更和直接方法呼叫：</span><span class="sxs-lookup"><span data-stu-id="675d5-194">At a command prompt in the `simulated-device` folder, run the following command to start the device app listening for desired property changes and direct method calls:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![裝置用戶端啟動](media/iot-hub-java-java-schedule-jobs/device-app-1.png)

1. <span data-ttu-id="675d5-196">在 `schedule-jobs` 資料夾的命令提示字元中執行下列命令，執行 **schedule-jobs** 服務應用程式以執行兩個作業。</span><span class="sxs-lookup"><span data-stu-id="675d5-196">At a command prompt in the `schedule-jobs` folder, run the following command to run the **schedule-jobs** service app to run two jobs.</span></span> <span data-ttu-id="675d5-197">第一個作業會設定所需屬性值，第二個作業會呼叫直接方法：</span><span class="sxs-lookup"><span data-stu-id="675d5-197">The first sets the desired property values, the second calls the direct method:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Java IoT 中樞服務應用程式會建立兩個作業](media/iot-hub-java-java-schedule-jobs/service-app-1.png)

1. <span data-ttu-id="675d5-199">裝置應用程式會處理所需屬性變更和直接方法呼叫：</span><span class="sxs-lookup"><span data-stu-id="675d5-199">The device app handles the desired property change and the direct method call:</span></span>

    ![裝置用戶端會回應變更](media/iot-hub-java-java-schedule-jobs/device-app-2.png)

## <a name="next-steps"></a><span data-ttu-id="675d5-201">後續步驟</span><span class="sxs-lookup"><span data-stu-id="675d5-201">Next steps</span></span>

<span data-ttu-id="675d5-202">在此教學課程中，您在 Azure 入口網站中設定了新的 IoT 中樞，然後在 IoT 中樞的身分識別登錄中建立了裝置身分識別。</span><span class="sxs-lookup"><span data-stu-id="675d5-202">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="675d5-203">您建立後端應用程式以執行兩個作業。</span><span class="sxs-lookup"><span data-stu-id="675d5-203">You created a back-end app to run two jobs.</span></span> <span data-ttu-id="675d5-204">第一個作業會設定所需屬性值，第二個作業會呼叫直接方法。</span><span class="sxs-lookup"><span data-stu-id="675d5-204">The first job set desired property values, and the second job called a direct method.</span></span>

<span data-ttu-id="675d5-205">使用下列資源來了解如何：</span><span class="sxs-lookup"><span data-stu-id="675d5-205">Use the following resources to learn how to:</span></span>

* <span data-ttu-id="675d5-206">利用[開始使用 IoT 中樞](iot-hub-java-java-getstarted.md)教學課程，傳送裝置的遙測資料。</span><span class="sxs-lookup"><span data-stu-id="675d5-206">Send telemetry from devices with the [Get started with IoT Hub](iot-hub-java-java-getstarted.md) tutorial.</span></span>
* <span data-ttu-id="675d5-207">以互動方式控制裝置 (例如，從使用者控制的應用程式開啟風扇)，請參閱[使用直接方法](iot-hub-java-java-direct-methods.md)教學課程。</span><span class="sxs-lookup"><span data-stu-id="675d5-207">Control devices interactively (such as turning on a fan from a user-controlled app) with the [Use direct methods](iot-hub-java-java-direct-methods.md) tutorial.</span></span>
