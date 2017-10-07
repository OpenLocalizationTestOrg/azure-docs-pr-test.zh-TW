---
title: "aaaDevice 韌體更新與 Azure IoT 中樞 （.NET/節點） |Microsoft 文件"
description: "如何在 Azure IoT 中樞 tooinitiate 裝置韌體 toouse 裝置管理更新。 您可以使用 Node.js tooimplement 模擬的裝置應用程式的 hello Azure IoT 裝置 SDK 和 hello Azure IoT 服務 SDK for.NET tooimplement hello 韌體更新觸發程序的服務應用程式。"
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: 70b84258-bc9f-43b1-b7cf-de1bb715f2cf
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/17/2017
ms.author: juanpere
ms.openlocfilehash: d48899651bcd5d67e577c971be0f9453c8f21592
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-device-management-tooinitiate-a-device-firmware-update-netnode"></a>使用裝置管理 tooinitiate 裝置韌體更新 （.NET/節點）
[!INCLUDE [iot-hub-selector-firmware-update](../../includes/iot-hub-selector-firmware-update.md)]

## <a name="introduction"></a>簡介
在 hello[開始使用 裝置管理][ lnk-dm-getstarted]教學課程中，您已看到如何 toouse hello[裝置兩個][ lnk-devtwin]和[直接方法][ lnk-c2dmethod]基本型別 tooremotely 裝置重新開機。 這個教學課程使用 hello 相同 IoT 中樞基本型別，並顯示如何 toodo 端對端模擬軔體更新。  此模式在 hello 韌體更新實作用於 hello[覆盆子 Pi 裝置實作範例][lnk-rpi-implementation]。

本教學課程說明如何：

* 建立.NET 主控台應用程式透過您的 IoT 中樞 hello 模擬的裝置應用程式中呼叫 hello firmwareUpdate 直接的方法。
* 建立會實作 **firmwareUpdate** 直接方法的模擬裝置應用程式。 這個方法會起始多階段程序，等候 toodownload hello 的韌體映像，下載 hello 的韌體映像，並在最後套用 hello 的韌體映像。 在每個階段 hello 更新中，hello 裝置使用 hello 報告屬性 tooreport 進度。

在本教學課程的 hello 最後，您有 Node.js 主控台裝置應用程式和.NET (C#) 主控台後端應用程式：

**dmpatterns_fwupdate_service.js**、 直接的方法呼叫 hello 模擬的裝置，應用程式中顯示 hello 回應，並定期 (每個的 500ms) 顯示 hello 更新報告內容。

**TriggerFWUpdate**，稍早建立的 hello 裝置身分識別與連線 tooyour IoT 中樞收到 firmwareUpdate 直接的方法時，會透過執行多重狀態的處理序 toosimulate 韌體更新，包括： 等候 hello 映像下載項目：正在下載 hello 新映像，以及最後套用的 hello 映像。

toocomplete 本教學課程中，您需要遵循的 hello:

* Visual Studio 2015 或 Visual Studio 2017。
* Node.js 0.12.x 版或更新版本， <br/>  [準備開發環境][ lnk-dev-setup]描述如何 tooinstall Node.js 本教學課程中的 Windows 或 Linux。
* 使用中的 Azure 帳戶。 (如果您沒有帳戶，只需要幾分鐘的時間就可以建立[免費帳戶][lnk-free-trial]。)

請遵循 hello[開始使用 裝置管理](iot-hub-csharp-node-device-management-get-started.md)文章 toocreate IoT 中樞，並取得您的 IoT 中樞連接字串。

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-firmware-update-on-hello-device-using-a-direct-method"></a>觸發遠端韌體更新 hello 裝置上使用直接的方法
在此節中，您會建立 .NET 主控台應用程式 (使用 C#)，此應用程式會在裝置上起始遠端韌體更新。 hello 應用程式使用直接的方法 tooinitiate hello 更新，並使用裝置兩個查詢 tooperiodically 取得 hello hello 作用中的韌體更新狀態。

1. 在 Visual Studio 中，將 Visual C# Windows 傳統桌面專案 toohello 目前方案使用 hello**主控台應用程式**專案範本。 名稱 hello 專案**TriggerFWUpdate**。

    ![新的 Visual C# Windows 傳統桌面專案][img-createapp]

1. 在 [方案總管] 中，以滑鼠右鍵按一下 hello **TriggerFWUpdate**專案，然後再按一下**管理 NuGet 封裝...**.
1. 在 hello **NuGet 套件管理員**視窗中，選取**瀏覽**，搜尋**microsoft.azure.devices**，選取**安裝**tooinstallhello **Microsoft.Azure.Devices**封裝，並接受使用規定 hello。 此程序下載、 安裝，並新增參考 toohello [Azure IoT 服務 SDK] [ lnk-nuget-service-sdk] NuGet 封裝和其相依性。

    ![NuGet 封裝管理員視窗][img-servicenuget]
1. 新增下列 hello`using`在 hello hello 最上方的陳述式**Program.cs**檔案：
   
        using Microsoft.Azure.Devices;
        using Microsoft.Azure.Devices.Shared;
        
1. 新增下列欄位 toohello hello**程式**類別。 取代具有多個預留位置值 hello IoT 中樞連接字串，您建立 hello 前一節中的 hello 中樞的 hello 和您的裝置識別碼 hello。
   
        static RegistryManager registryManager;
        static string connString = "{iot hub connection string}";
        static ServiceClient client;
        static JobClient jobClient;
        static string targetDevice = "{deviceIdForTargetDevice}";
        
1. 新增下列方法 toohello hello**程式**類別：
   
        public static async Task QueryTwinFWUpdateReported()
        {
            Twin twin = await registryManager.GetTwinAsync(targetDevice);
            Console.WriteLine(twin.Properties.Reported.ToJson());
        }
        
1. 新增下列方法 toohello hello**程式**類別：

        public static async Task StartFirmwareUpdate()
        {
            client = ServiceClient.CreateFromConnectionString(connString);
            CloudToDeviceMethod method = new CloudToDeviceMethod("firmwareUpdate");
            method.ResponseTimeout = TimeSpan.FromSeconds(30);
            method.SetPayloadJson(
                @"{
                    fwPackageUri : 'https://someurl'
                }");

            CloudToDeviceMethodResult result = await client.InvokeDeviceMethodAsync(targetDevice, method);

            Console.WriteLine("Invoked firmware update on device.");
        }

1. 最後，加入下列行 toohello hello **Main**方法：
   
        registryManager = RegistryManager.CreateFromConnectionString(connString);
        StartFirmwareUpdate().Wait();
        QueryTwinFWUpdateReported().Wait();
        Console.WriteLine("Press ENTER tooexit.");
        Console.ReadLine();
        
1. 在 hello 方案總管 中，開啟 hello**設定啟始專案...** ，請確定 hello**動作**如**TriggerFWUpdate**專案是**啟動**。

1. 建置 hello 方案。

[!INCLUDE [iot-hub-device-firmware-update](../../includes/iot-hub-device-firmware-update.md)]

## <a name="run-hello-apps"></a>執行 hello 應用程式
現在您已經準備就緒 toorun hello 應用程式。

1. 在 hello 命令提示字元中 hello **manageddevice**資料夾中，執行下列命令 toobegin 接聽 hello 重新開機直接方法 hello。
   
    ```
    node dmpatterns_fwupdate_device.js
    ```
2. 在 Visual Studio 中，以滑鼠右鍵按一下 hello **TriggerFWUpdate** projectRun toohello C# 主控台應用程式中，選取**偵錯**和**開始新執行個體**。

3. 您會看到 hello 裝置回應 toohello 直接方法 hello 主控台中。

    ![已順利更新韌體][img-fwupdate]

## <a name="next-steps"></a>後續步驟
在本教學課程中，您可以使用直接的方法 tootrigger 遠端裝置和使用的 hello 上的軔體更新報告 hello 韌體更新屬性 toofollow hello 進度。

toolearn 如何 tooextend IoT 解決方案和排程方法呼叫上多個裝置，請參閱 hello[排程和廣播的工作][ lnk-tutorial-jobs]教學課程。

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-node-firmware-update/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-node-firmware-update/createnetapp.png
[img-fwupdate]: media/iot-hub-csharp-node-firmware-update/fwupdated.png

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-dm-getstarted]: iot-hub-node-node-device-management-get-started.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-rpi-implementation]: https://github.com/Azure/azure-iot-sdk-c/tree/master/iothub_client/samples/iothub_client_sample_mqtt_dm/pi_device
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/