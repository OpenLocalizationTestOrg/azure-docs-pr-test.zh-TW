---
title: "aaaSchedule 作業與 Azure IoT 中樞 (Java) |Microsoft 文件"
description: "如何 tooschedule Azure IoT 中樞作業 tooinvoke 直接的方法，與多個裝置上設定所需的屬性。 您可以使用 hello Azure IoT 裝置 SDK for Java tooimplement hello 模擬裝置的應用程式和 hello Azure IoT 服務 SDK for Java tooimplement 服務應用程式 toorun hello 作業。"
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
ms.openlocfilehash: b1b05fa56c3ce96af0b33d4cca0dd54da0f4e927
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="schedule-and-broadcast-jobs-java"></a>排定及廣播作業 (Java)

[!INCLUDE [iot-hub-selector-schedule-jobs](../../includes/iot-hub-selector-schedule-jobs.md)]

使用更新數百萬個裝置的 Azure IoT 中樞 tooschedule 和追蹤工作。 使用作業以：

* 更新所需屬性
* 更新標籤
* 叫用直接方法

作業會包裝其中一個動作，並追蹤 hello 執行則是根據一組裝置。 裝置的兩個查詢定義針對 hello 工作執行的裝置 hello 組。 比方說後, 端應用程式可以使用 hello 裝置重新開機的 10,000 部裝置上的作業 tooinvoke 直接的方法。 您指定與裝置的兩個查詢的 hello 的一組裝置，然後 hello 作業 toorun 排程在未來的時間。 為每個 hello 裝置 hello 工作追蹤進度接收，並執行 hello 重新開機直接的方法。

toolearn 進一步了解每個這些功能，請參閱：

* 裝置對應項和屬性：[開始使用裝置對應項](iot-hub-java-java-twin-getstarted.md)
* 直接方法：[IoT 中樞開發人員指南 - 直接方法](iot-hub-devguide-direct-methods.md)和[教學課程：使用直接方法](iot-hub-java-java-direct-methods.md)

本教學課程說明如何：

* 建立實作 **lockDoor** 直接方法的裝置應用程式。 hello 裝置應用程式也會接收來自 hello 後端應用程式的所需的屬性變更。
* 建立後端應用程式建立作業 toocall hello **lockDoor**直接多個裝置上的方法。 另一項工作會傳送所需的屬性更新 toomultiple 裝置。

在本教學課程的 hello 最後，您有具備 java 主控台裝置應用程式及 java 主控台後端應用程式：

**模擬裝置**，連線到 tooyour IoT 中樞時，實作 hello **lockDoor**直接方法，並控制代碼所需屬性變更。

**排程作業**使用作業 toocall hello **lockDoor**直接方法，並更新 hello 裝置兩個所需的多個裝置上的屬性。

> [!NOTE]
> hello 文章[Azure IoT Sdk](iot-hub-devguide-sdks.md)提供 hello Azure IoT Sdk 的相關資訊，您可以使用 toobuild 裝置與後端應用程式。

## <a name="prerequisites"></a>必要條件

toocomplete 本教學課程中，您需要：

* 最新 hello [Java SE 開發套件 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
* [Maven 3](https://maven.apache.org/install.html)
* 使用中的 Azure 帳戶。 (如果您沒有帳戶，只需要幾分鐘的時間就可以建立[免費帳戶](http://azure.microsoft.com/pricing/free-trial/)。)

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

如果您以程式設計方式偏好 toocreate hello 裝置識別身分，讀取 hello 對應的章節 hello[連接使用 Java 程式裝置 tooyour IoT 中樞](iot-hub-java-java-getstarted.md#create-a-device-identity)發行項。 您也可以使用 hello [iot 中樞總管](https://github.com/Azure/iothub-explorer)工具 tooadd 裝置 tooyour IoT 中樞。

## <a name="create-hello-service-app"></a>建立 hello 服務應用程式

在本節中，您將建立 Java 主控台應用程式，使用作業以：

* 呼叫 hello **lockDoor**直接多個裝置上的方法。
* 傳送所需的屬性 toomultiple 裝置。

toocreate hello 應用程式：

1. 在您的開發電腦上建立名為 `iot-java-schedule-jobs` 的空資料夾。

1. 在 hello`iot-java-schedule-jobs`資料夾中，建立名為 Maven 專案**排定工作**使用下列命令，在您的命令提示字元的 hello。 注意，這是一個單一且非常長的命令：

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=schedule-jobs -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. 在命令提示字元中，瀏覽 toohello`schedule-jobs`資料夾。

1. 使用文字編輯器開啟 hello`pom.xml`檔案在 hello`schedule-jobs`資料夾並加入下列相依性 toohello hello**相依性**節點。 此相依性可讓您 toouse hello **iot 服務用戶端**在您的應用程式 toocommunicate 與 IoT 中樞中的套件：

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

1. 使用文字編輯器開啟 hello`schedule-jobs\src\main\java\com\mycompany\app\App.java`檔案。

1. 新增下列 hello**匯入**陳述式 toohello 檔案：

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

1. 新增下列類別層級變數 toohello hello**應用程式**類別。 取代`{youriothubconnectionstring}`與您在 hello 記下您的 IoT 中樞連接字串*建立 IoT 中樞*> 一節：

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    // How long hello job is permitted toorun without
    // completing its work on hello set of devices
    private static final long maxExecutionTimeInSeconds = 30;
    ```

1. 新增下列方法 toohello hello**應用程式**類別 tooschedule 作業 tooupdate hello**建置**和**Floor**所需的 hello 裝置兩個屬性：

    ```java
    private static JobResult scheduleJobSetDesiredProperties(JobClient jobClient, String jobId) {
      DeviceTwinDevice twin = new DeviceTwinDevice(deviceId);
      Set<Pair> desiredProperties = new HashSet<Pair>();
      desiredProperties.add(new Pair("Building", 43));
      desiredProperties.add(new Pair("Floor", 3));
      twin.setDesiredProperties(desiredProperties);
      // Optimistic concurrency control
      twin.setETag("*");

      // Schedule hello update twin job toorun now
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

1. tooschedule 作業 toocall hello **lockDoor**方法，加入下列方法 toohello hello**應用程式**類別：

    ```java
    private static JobResult scheduleJobCallDirectMethod(JobClient jobClient, String jobId) {
      // Schedule a job now toocall hello lockDoor direct method
      // against a single device. Response and connection
      // timeouts are set too5 seconds.
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

1. toomonitor 作業新增下列方法 toohello hello**應用程式**類別：

    ```java
    private static void monitorJob(JobClient jobClient, String jobId) {
      try {
        JobResult jobResult = jobClient.getJob(jobId);
        if(jobResult == null)
        {
          System.out.println("No JobResult for: " + jobId);
          return;
        }
        // Check hello job result until it's completed
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

1. tooquery hello 詳細資料的 hello 工作執行時，加入下列方法 hello:

    ```java
    private static void queryDeviceJobs(JobClient jobClient, String start) throws Exception {
      System.out.println("\nQuery device jobs since " + start);

      // Create a jobs query using hello time hello jobs started
      Query deviceJobQuery = jobClient
          .queryDeviceJob(SqlQuery.createSqlQuery("*", SqlQuery.FromType.JOBS, "devices.jobs.startTimeUtc > '" + start + "'", null).getQuery());

      // Iterate over hello list of jobs and print hello details
      while (jobClient.hasNextJob(deviceJobQuery)) {
        System.out.println(jobClient.getNextJob(deviceJobQuery));
      }
    }
    ```

1. 更新 hello**主要**方法簽章 tooinclude hello 下列`throws`子句：

    ```java
    public static void main( String[] args ) throws Exception
    ```

1. toorun 和監視器的兩個工作以循序方式，加入下列程式碼 toohello hello**主要**方法：

    ```java
    // Record hello start time
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

    // Run a query tooshow hello job detail
    queryDeviceJobs(jobClient, start);

    System.out.println("Shutting down schedule-jobs app");
    ```

1. 儲存並關閉 hello`schedule-jobs\src\main\java\com\mycompany\app\App.java`檔案

1. 建置 hello**排定工作**應用程式，並更正任何錯誤。 在命令提示字元中，瀏覽 toohello`schedule-jobs`資料夾，然後執行下列命令的 hello:

    `mvn clean package -DskipTests`

## <a name="create-a-device-app"></a>建立裝置應用程式

在本節中，您可以建立 Java 主控台應用程式的控制代碼 hello 從 IoT 中樞與實作 hello 直接方法呼叫傳送所需的屬性。

1. 在 hello`iot-java-schedule-jobs`資料夾中，建立名為 Maven 專案**模擬裝置**使用下列命令，在您的命令提示字元的 hello。 注意，這是一個單一且非常長的命令：

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
    private static final int METHOD_SUCCESS = 200;
    private static final int METHOD_NOT_DEFINED = 404;
    ```

    此範例應用程式會使用 hello**通訊協定**變數時，它會具現化**DeviceClient**物件。 目前，toouse 裝置兩個功能您必須使用 hello MQTT 通訊協定。

1. tooprint 裝置兩個通知 toohello 主控台中，將 hello 面一行加入巢狀類別 toohello**應用程式**類別：

    ```java
    // Handler for device twin operation notifications from IoT Hub
    protected static class DeviceTwinStatusCallBack implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded toodevice twin operation with status " + status.name());
      }
    }
    ```

1. tooprint 直接方法通知 toohello 主控台中，將 hello 面一行加入巢狀類別 toohello**應用程式**類別：

    ```java
    // Handler for direct method notifications from IoT Hub
    protected static class DirectMethodStatusCallback implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded toodirect method operation with status " + status.name());
      }
    }
    ```

1. toohandle 直接方法呼叫從 IoT 中樞將 hello 面一行加入巢狀類別 toohello**應用程式**類別：

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

1. 更新 hello**主要**方法簽章 tooinclude hello 下列`throws`子句：

    ```java
    public static void main( String[] args ) throws IOException, URISyntaxException
    ```

1. 新增下列程式碼 toohello hello**主要**方法：
    * 建立裝置用戶端 toocommunicate 與 IoT 中樞。
    * 建立**裝置**物件 toostore hello 裝置兩個屬性。

    ```java
    // Create a device client
    DeviceClient client = new DeviceClient(connString, protocol);

    // An object toomanage device twin desired and reported properties
    Device dataCollector = new Device() {
      @Override
      public void PropertyCall(String propertyKey, Object propertyValue, Object context)
      {
        System.out.println("Received desired property change: " + propertyKey + " " + propertyValue);
      }
    };
    ```

1. toostart hello 裝置用戶端服務，加入下列程式碼 toohello hello**主要**方法：

    ```java
    try {
      // Open hello DeviceClient
      // Start hello device twin services
      // Subscribe toodirect method calls
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

1. hello 使用者 toopress hello toowait **Enter**鍵關閉之前，加入下列程式碼 toohello 結尾 hello hello**主要**方法：

    ```java
    // Close hello app
    System.out.println("Press any key tooexit...");
    Scanner scanner = new Scanner(System.in);
    scanner.nextLine();
    dataCollector.clean();
    client.closeNow();
    scanner.close();
    ```

1. 儲存並關閉 hello`simulated-device\src\main\java\com\mycompany\app\App.java`檔案。

1. 建置 hello**模擬裝置**應用程式，並更正任何錯誤。 在命令提示字元中，瀏覽 toohello`simulated-device`資料夾，然後執行下列命令的 hello:

    `mvn clean package -DskipTests`

## <a name="run-hello-apps"></a>執行 hello 應用程式

現在您已經準備就緒 toorun hello 主控台應用程式。

1. 在命令提示字元中 hello`simulated-device`資料夾中，執行下列命令 toostart hello 裝置應用程式接聽所需的屬性變更及直接方法呼叫的 hello:

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![hello 裝置用戶端啟動](media/iot-hub-java-java-schedule-jobs/device-app-1.png)

1. 在命令提示字元中 hello`schedule-jobs`資料夾中，執行下列命令 toorun hello hello**排定工作**服務應用程式 toorun 兩個工作。 hello 先設定想要的 hello 屬性值，第二個呼叫的 hello hello 直接的方法：

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Java IoT 中樞服務應用程式會建立兩個作業](media/iot-hub-java-java-schedule-jobs/service-app-1.png)

1. hello 裝置應用程式處理所需的 hello 屬性變更及 hello 直接方法呼叫：

    ![hello 裝置用戶端會回應 toohello 變更](media/iot-hub-java-java-schedule-jobs/device-app-2.png)

## <a name="next-steps"></a>後續步驟

在本教學課程中，您在 hello Azure 入口網站中設定新的 IoT 中樞，並接著 hello IoT 中樞的身分識別登錄中建立裝置身分識別。 Toorun 兩個工作建立後端應用程式。 hello 第一份工作設定所需的屬性值和 hello 第二個工作，稱為直接的方法。

下列資源 toolearn 如何使用 hello 至：

* 從以 hello 的裝置將遙測傳送[開始使用 IoT 中樞](iot-hub-java-java-getstarted.md)教學課程。
* 控制以互動方式 （例如開啟風扇從使用者控制的應用程式） 的裝置以 hello[使用直接的方法](iot-hub-java-java-direct-methods.md)教學課程。
