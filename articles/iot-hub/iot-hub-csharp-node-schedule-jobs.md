---
title: "aaaSchedule 作業與 Azure IoT 中樞 （.NET/節點） |Microsoft 文件"
description: "如何 tooschedule Azure IoT 中樞工作 tooinvoke 上多個裝置的直接的方法。 您可以使用 hello Azure IoT 裝置 SDK for Node.js tooimplement hello 模擬裝置的應用程式和 hello Azure IoT 服務 SDK for.NET tooimplement 服務應用程式 toorun hello 作業。"
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: 2233356e-b005-4765-ae41-3a4872bda943
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/10/2017
ms.author: juanpere
ms.openlocfilehash: f6148b67129dde4580bfe9ccceafd6400fbc5976
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="schedule-and-broadcast-jobs-netnodejs"></a>排程及廣播作業 (.NET/Node.js)

[!INCLUDE [iot-hub-selector-schedule-jobs](../../includes/iot-hub-selector-schedule-jobs.md)]

使用更新數百萬個裝置的 Azure IoT 中樞 tooschedule 和追蹤工作。 使用作業以：

* 更新所需屬性
* 更新標籤
* 叫用直接方法

作業會包裝其中一個動作，並追蹤 hello 執行則是根據一組裝置的裝置的兩個查詢所定義。 比方說後, 端應用程式可以使用 hello 裝置重新開機的 10,000 部裝置上的作業 tooinvoke 直接的方法。 您指定與裝置的兩個查詢的 hello 的一組裝置，然後 hello 作業 toorun 排程在未來的時間。 為每個 hello 裝置 hello 工作追蹤進度接收，並執行 hello 重新開機直接的方法。

toolearn 進一步了解每個這些功能，請參閱：

* 裝置的兩個與屬性：[開始使用裝置雙][ lnk-get-started-twin]和[教學課程： 如何 toouse 裝置 twin 屬性][lnk-twin-props]
* 直接方法：[IoT 中樞開發人員指南 - 直接方法][lnk-dev-methods]和[教學課程：使用直接方法][lnk-c2d-methods]

本教學課程說明如何：

* 建立裝置的應用程式實作直接的方法呼叫**lockDoor** hello 後端應用程式可以呼叫的。 hello 裝置應用程式也會接收來自 hello 後端應用程式的所需的屬性變更。
* 建立後端應用程式建立作業 toocall hello **lockDoor**直接多個裝置上的方法。 另一項工作會傳送所需的屬性更新 toomultiple 裝置。

在本教學課程的 hello 最後，您有 Node.js 主控台裝置應用程式和.NET (C#) 主控台後端應用程式：

**simDevice.js** ，連線到 tooyour IoT 中樞時，實作 hello **lockDoor**直接方法，並控制代碼所需屬性變更。

**ScheduleJob**使用作業 toocall hello **lockDoor**直接方法，並更新 hello 裝置兩個所需的多個裝置上的屬性。

toocomplete 本教學課程中，您需要遵循的 hello:

* Visual Studio 2015 或 Visual Studio 2017。
* Node.js 0.12.x 版或更新版本。 hello 文章[準備開發環境][ lnk-dev-setup]描述如何 tooinstall Node.js 本教學課程中的 Windows 或 Linux。
* 使用中的 Azure 帳戶。 如果您沒有帳戶，只需要幾分鐘的時間就可以建立[免費帳戶][lnk-free-trial]。

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="schedule-jobs-for-calling-a-direct-method-and-sending-device-twin-updates"></a>排程呼叫直接方法及傳送裝置對應項更新的作業

在本節中，您會建立.NET 主控台應用程式 （使用 C#） 會使用作業 toocall hello **lockDoor**直接方法，並傳送所需的屬性更新 toomultiple 裝置。

1. 在 Visual Studio 中，將 Visual C# Windows 傳統桌面專案 toohello 目前方案使用 hello**主控台應用程式**專案範本。 名稱 hello 專案**ScheduleJob**。

    ![新的 Visual C# Windows 傳統桌面專案][img-createapp]

1. 在 [方案總管] 中，以滑鼠右鍵按一下 hello **ScheduleJob**專案，然後再按一下**管理 NuGet 封裝...**.
1. 在 hello **NuGet 套件管理員**視窗中，選取**瀏覽**，搜尋**microsoft.azure.devices**，選取**安裝**tooinstallhello **Microsoft.Azure.Devices**封裝，並接受使用規定 hello。 此步驟中下載、 安裝，並將參考 toohello [Azure IoT 服務 SDK] [ lnk-nuget-service-sdk] NuGet 封裝和其相依性。

    ![NuGet 封裝管理員視窗][img-servicenuget]
1. 新增下列 hello`using`在 hello hello 最上方的陳述式**Program.cs**檔案：
    
    ```csharp
    using Microsoft.Azure.Devices;
    using Microsoft.Azure.Devices.Shared;
    ```

1. 新增下列 hello`using`若還未出現在 hello 預設陳述式中的陳述式。

    ```csharp
    using System.Threading.Tasks;
    ```

1. 新增下列欄位 toohello hello**程式**類別。 Hello 預留位置取代為 hello hello 中樞在 hello 上一節中所建立的 IoT 中樞連接字串。

    ```csharp
    static string connString = "{iot hub connection string}";
    static ServiceClient client;
    static JobClient jobClient;
    ```

1. 新增下列方法 toohello hello**程式**類別：

    ```csharp
    public static async Task MonitorJob(string jobId)
    {
        JobResponse result;
        do
        {
            result = await jobClient.GetJobAsync(jobId);
            Console.WriteLine("Job Status : " + result.Status.ToString());
            Thread.Sleep(2000);
        } while ((result.Status != JobStatus.Completed) && (result.Status != JobStatus.Failed));
    }
    ```

1. 新增下列方法 toohello hello**程式**類別：

    ```csharp
    public static async Task StartMethodJob(string jobId)
    {
        CloudToDeviceMethod directMethod = new CloudToDeviceMethod("lockDoor", TimeSpan.FromSeconds(5), TimeSpan.FromSeconds(5));

        JobResponse result = await jobClient.ScheduleDeviceMethodAsync(jobId,
            "deviceId='myDeviceId'",
            directMethod,
            DateTime.Now,
            10);

        Console.WriteLine("Started Method Job");
    }
    ```

1. 新增下列方法 toohello hello**程式**類別：

    ```csharp
    public static async Task StartTwinUpdateJob(string jobId)
    {
        var twin = new Twin();
        twin.Properties.Desired["Building"] = "43";
        twin.Properties.Desired["Floor"] = "3";
        twin.ETag = "*";

        JobResponse result = await jobClient.ScheduleTwinUpdateAsync(jobId,
            "deviceId='myDeviceId'",
            twin,
            DateTime.Now,
            10);

        Console.WriteLine("Started Twin Update Job");
    }
    ```

1. 最後，加入下列行 toohello hello **Main**方法：

    ```csharp
    jobClient = JobClient.CreateFromConnectionString(connString);

    string methodJobId = Guid.NewGuid().ToString();

    StartMethodJob(methodJobId);
    MonitorJob(methodJobId).Wait();
    Console.WriteLine("Press ENTER toorun hello next job.");
    Console.ReadLine();

    string twinUpdateJobId = Guid.NewGuid().ToString();

    StartTwinUpdateJob(twinUpdateJobId);
    MonitorJob(twinUpdateJobId).Wait();
    Console.WriteLine("Press ENTER tooexit.");
    Console.ReadLine();
    ```

1. 在 hello 方案總管 中，開啟 hello**設定啟始專案...** ，請確定 hello**動作**如**ScheduleJob**專案是**啟動**。 建置 hello 方案。

## <a name="create-a-simulated-device-app"></a>建立模擬裝置應用程式

在本節中，您建立 Node.js 主控台應用程式回應 tooa 直接方法呼叫 hello 雲端，觸發程序模擬的裝置重新開機，使用 hello 報告屬性 tooenable 裝置兩個查詢 tooidentify 裝置，當它們一次啟動。

1. 建立名為 **simDevice** 的新空白資料夾。  在 hello **simDevice**資料夾中，建立使用下列命令，在您的命令提示字元的 hello package.json 檔案。  接受所有的 hello 預設值：

    ```cmd/sh
    npm init
    ```

1. 在您的命令提示字元中 hello **simDevice**資料夾中，執行下列命令 tooinstall hello hello **azure iot 裝置**和**azure iot 裝置-mqtt**封裝：

    ```cmd/sh
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```

1. 使用文字編輯器中，建立新**simDevice.js**檔案在 hello **simDevice**資料夾。

1. 新增 hello 下列的 '需要' 陳述式在 hello 開頭的 hello **simDevice.js**檔案：

    ```nodejs
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```

1. 新增**connectionString**變數，並使用它 toocreate**用戶端**執行個體。 請確定 tooreplace hello 預留位置值適當 tooyour 安裝程式。

    ```nodejs
    var connectionString = 'HostName={youriothostname};DeviceId={yourdeviceid};SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```

1. 加入下列函式 toohandle hello hello **lockDoor**方法。

    ```nodejs
    var onLockDoor = function(request, response) {
   
        // Respond hello cloud app for hello direct method
        response.send(200, function(err) {
            if (!err) {
                console.error('An error occured when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.');
            }
        });
   
        console.log('Locking Door!');
    };
    ```

1. 新增下列程式碼的 hello tooregister hello 處理常式的 hello **lockDoor**方法。

    ```nodejs
    client.open(function(err) {
        if (err) {
            console.error('Could not connect tooIotHub client.');
        }  else {
            console.log('Client connected tooIoT Hub.  Waiting for lockDoor direct method.');
            client.onDeviceMethod('lockDoor', onLockDoor);
        }
    });
    ```

1. 儲存並關閉 hello **simDevice.js**檔案。

> [!NOTE]
> 簡單 tookeep 方面，本教學課程未實作任何重試原則。 在實際執行程式碼，您應該實作重試原則 （例如指數型輪詢），做為建議 hello MSDN 文件中[暫時性錯誤處理][lnk-transient-faults]。

## <a name="run-hello-apps"></a>執行 hello 應用程式

現在您已經準備就緒 toorun hello 應用程式。

1. 在 hello 命令提示字元中 hello **simDevice**資料夾中，執行下列命令 toobegin 接聽 hello 重新開機直接方法 hello。

    ```cmd/sh
    node simDevice.js
    ```

1. 執行的 hello C# 主控台應用程式**ScheduleJob**以滑鼠右鍵按一下 hello **ScheduleJob**專案，然後選取**偵錯**和**開始新執行個體**.

1. 您會看到從裝置和後端應用程式的 hello 輸出。

    ![Tooschedule 工作執行 hello 應用程式][img-schedulejobs]

## <a name="next-steps"></a>後續步驟

在此教學課程中，您可以使用作業 tooschedule 直接方法 tooa 裝置和 hello 更新的 hello 裝置兩個的屬性。

開始使用 IoT 中樞與裝置管理模式，例如遠端透過 hello 空中韌體更新，讀取 toocontinue[教學課程： 如何 toodo 韌體更新][lnk-fwupdate]。

請參閱 < 開始使用 IoT 中樞 toocontinue[入門 IoT 邊緣][lnk-iot-edge]。

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-node-schedule-jobs/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-node-schedule-jobs/createnetapp.png
[img-schedulejobs]: media/iot-hub-csharp-node-schedule-jobs/schedulejobs.png

[lnk-get-started-twin]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-props]: iot-hub-node-node-twin-how-to-configure.md
[lnk-c2d-methods]: iot-hub-node-node-direct-methods.md
[lnk-dev-methods]: iot-hub-devguide-direct-methods.md
[lnk-fwupdate]: iot-hub-node-node-firmware-update.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
