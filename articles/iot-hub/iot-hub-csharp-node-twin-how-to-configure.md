---
title: "aaaUse Azure IoT Hub 裝置的兩個屬性 （.NET/節點） |Microsoft 文件"
description: "如何 toouse Azure IoT Hub 裝置雙 tooconfigure 裝置。 您可以使用 Node.js tooimplement 模擬的裝置應用程式的 hello Azure IoT 裝置 SDK 和 hello Azure IoT 服務 SDK for.NET tooimplement 修改使用裝置的兩個裝置設定的服務應用程式。"
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: 3c627476-f982-43c9-bd17-e0698c5d236d
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: elioda
ms.openlocfilehash: 840a1b2e45f4763131299577583aa89015dcdd1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-desired-properties-tooconfigure-devices"></a>使用所需的屬性 tooconfigure 裝置
[!INCLUDE [iot-hub-selector-twin-how-to-configure](../../includes/iot-hub-selector-twin-how-to-configure.md)]

在本教學課程的 hello 結束時，您將擁有兩個主控台應用程式：

* **SimulateDeviceConfiguration.js**，模擬的裝置應用程式等候的所需的組態更新，並報告 hello 模擬的組態更新程序的狀態。
* **SetDesiredConfigurationAndQuery**、 設定 hello.NET 後端應用程式預期在裝置上的設定和查詢 hello 組態更新程序。

> [!NOTE]
> hello 文章[Azure IoT Sdk] [ lnk-hub-sdks]提供 hello Azure IoT Sdk 的相關資訊，您可以使用 toobuild 裝置與後端應用程式。
> 
> 

toocomplete 需要 hello 下列本教學課程：

* Visual Studio 2015 或 Visual Studio 2017。
* Node.js 0.10.x 版或更新版本。
* 使用中的 Azure 帳戶。 如果您沒有帳戶，只需要幾分鐘的時間就可以建立[免費帳戶][lnk-free-trial]。

如果您遵循 hello[開始使用裝置雙][ lnk-twin-tutorial]教學課程中，您已經有 IoT 中樞和裝置身分識別稱為**myDeviceId**。 在此情況下，您可以略過 toohello[建立 hello 模擬的裝置應用程式][ lnk-how-to-configure-createapp] > 一節。

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

<a id="#create-the-simulated-device-app"></a>
## <a name="create-hello-simulated-device-app"></a>建立 hello 模擬的裝置應用程式
在本節中，您建立 Node.js 主控台應用程式連接成 tooyour 中樞**myDeviceId**等候所需的組態更新，然後報告 hello 模擬的組態更新程序中的 更新。

1. 建立稱為 **simulatedeviceconfiguration** 的新空白資料夾。 在 hello **simulatedeviceconfiguration**資料夾中，建立新的 package.json 檔案使用下列命令，在您的命令提示字元的 hello。 接受所有的 hello 預設值。
   
    ```
    npm init
    ```
1. 在您的命令提示字元中 hello **simulatedeviceconfiguration**資料夾中，執行下列命令 tooinstall hello hello **azure iot 裝置**和**azure-iot-裝置-mqtt**封裝：
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
1. 使用文字編輯器中，建立新**SimulateDeviceConfiguration.js**檔案在 hello **simulatedeviceconfiguration**資料夾。
1. 新增下列程式碼 toohello hello **SimulateDeviceConfiguration.js**檔案，並以取代 hello **{裝置連接字串}**預留位置 hello 裝置連接字串複製時您建立 hello **myDeviceId**裝置身分識別：
   
        'use strict';
        var Client = require('azure-iot-device').Client;
        var Protocol = require('azure-iot-device-mqtt').Mqtt;
   
        var connectionString = '{device connection string}';
        var client = Client.fromConnectionString(connectionString, Protocol);
   
        client.open(function(err) {
            if (err) {
                console.error('could not open IotHub client');
            } else {
                client.getTwin(function(err, twin) {
                    if (err) {
                        console.error('could not get twin');
                    } else {
                        console.log('retrieved device twin');
                        twin.properties.reported.telemetryConfig = {
                            configId: "0",
                            sendFrequency: "24h"
                        }
                        twin.on('properties.desired', function(desiredChange) {
                            console.log("received change: "+JSON.stringify(desiredChange));
                            var currentTelemetryConfig = twin.properties.reported.telemetryConfig;
                            if (desiredChange.telemetryConfig &&desiredChange.telemetryConfig.configId !== currentTelemetryConfig.configId) {
                                initConfigChange(twin);
                            }
                        });
                    }
                });
            }
        });
   
    hello**用戶端**物件會公開與 hello 裝置從裝置雙所有 hello 方法 toointeract 必要。 這個程式碼初始化 hello**用戶端**物件，擷取 hello 的裝置兩個**myDeviceId**，，然後再附加 hello 更新的處理常式上*所需屬性*。 hello 處理常式驗證那里實際的設定變更要求是藉由比較 hello configIds，然後啟動 hello 組態變更的方法會叫用。
   
    請注意，為了簡單明瞭的 hello 起見，這段程式碼使用硬式編碼預設值為 hello 初始設定。 實際的應用程式可能會從本機儲存體載入該組態。
   
   > [!IMPORTANT]
   > 所需的屬性變更事件永遠會在裝置連線時發出一次。 請確定是在 hello 變更的實際 toocheck 所需屬性然後再執行任何動作。
   > 
   > 
1. 新增下列方法之前 hello hello`client.open()`引動過程：
   
        var initConfigChange = function(twin) {
            var currentTelemetryConfig = twin.properties.reported.telemetryConfig;
            currentTelemetryConfig.pendingConfig = twin.properties.desired.telemetryConfig;
            currentTelemetryConfig.status = "Pending";
   
            var patch = {
            telemetryConfig: currentTelemetryConfig
            };
            twin.properties.reported.update(patch, function(err) {
                if (err) {
                    console.log('Could not report properties');
                } else {
                    console.log('Reported pending config change: ' + JSON.stringify(patch));
                    setTimeout(function() {completeConfigChange(twin);}, 60000);
                }
            });
        }
   
        var completeConfigChange =  function(twin) {
            var currentTelemetryConfig = twin.properties.reported.telemetryConfig;
            currentTelemetryConfig.configId = currentTelemetryConfig.pendingConfig.configId;
            currentTelemetryConfig.sendFrequency = currentTelemetryConfig.pendingConfig.sendFrequency;
            currentTelemetryConfig.status = "Success";
            delete currentTelemetryConfig.pendingConfig;
   
            var patch = {
                telemetryConfig: currentTelemetryConfig
            };
            patch.telemetryConfig.pendingConfig = null;
   
            twin.properties.reported.update(patch, function(err) {
                if (err) {
                    console.error('Error reporting properties: ' + err);
                } else {
                    console.log('Reported completed config change: ' + JSON.stringify(patch));
                }
            });
        };
   
    hello **initConfigChange**方法更新 hello 回報 hello 組態與 hello 本機裝置兩個物件上的內容更新要求和設定 hello 狀態太**暫止**，然後更新 hellohello 服務上的裝置兩個。 已成功更新之後 hello 裝置兩個，它會模擬長時間執行的處理程序會終止在 hello 執行**completeConfigChange**。 這個方法會更新本機 hello 太 hello 狀態設定報告的內容**成功**和移除 hello **pendingConfig**物件。 然後，它會更新 hello 裝置的兩個 hello 服務上。
   
    請注意，toosave 頻寬報告內容更新時所指定 hello 屬性 toobe 修改 (名為**修補程式**hello 上述程式碼中)，而不是取代 hello 整份文件。
   
   > [!NOTE]
   > 本教學課程不會模擬並行組態更新的任何行為。 某些組態更新處理程序可能會無法 tooaccommodate 變更目標組態的 hello 更新執行時，有些可能會有 tooqueue，以及一些無法拒絕它們與錯誤狀況。 請確定 tooconsider hello 特定組態程序中，所要的行為，並加入初始化 hello 組態變更之前的 hello 適當的邏輯。
   > 
   > 
1. 執行 hello 裝置應用程式：
   
        node SimulateDeviceConfiguration.js
   
    您應該會看到 hello 訊息`retrieved device twin`。 保留 hello 應用程式執行。

## <a name="create-hello-service-app"></a>建立 hello 服務應用程式
在本節中，您將建立.NET 主控台應用程式的更新 hello*所需屬性*上 hello 與相關聯的裝置兩個**myDeviceId**與新的遙測組態物件。 接著會查詢儲存在 hello IoT 中樞中的 hello 裝置雙，並顯示 hello 差異 hello 想要與報告的 hello 裝置組態。

1. 在 Visual Studio 中，將 Visual C# Windows 傳統桌面專案 toohello 目前方案使用 hello**主控台應用程式**專案範本。 名稱 hello 專案**SetDesiredConfigurationAndQuery**。
   
    ![新的 Visual C# Windows 傳統桌面專案][img-createapp]
1. 在 [方案總管] 中，以滑鼠右鍵按一下 hello **SetDesiredConfigurationAndQuery**專案，然後再按一下**管理 NuGet 封裝...**.
1. 在 hello **NuGet 套件管理員**視窗中，選取**瀏覽**，搜尋**microsoft.azure.devices**，選取**安裝**tooinstallhello **Microsoft.Azure.Devices**封裝，並接受使用規定 hello。 此程序下載、 安裝，並新增參考 toohello [Azure IoT 服務 SDK] [ lnk-nuget-service-sdk] NuGet 封裝和其相依性。
   
    ![NuGet 封裝管理員視窗][img-servicenuget]
1. 新增下列 hello`using`在 hello hello 最上方的陳述式**Program.cs**檔案：
   
        using Microsoft.Azure.Devices;
        using System.Threading;
        using Newtonsoft.Json;
1. 新增下列欄位 toohello hello**程式**類別。 取代 hello hello 中樞在 hello 上一節中所建立的 IoT 中樞連接字串中的 hello 預留位置的值。
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
1. 新增下列方法 toohello hello**程式**類別：
   
        static private async Task SetDesiredConfigurationAndQuery()
        {
            var twin = await registryManager.GetTwinAsync("myDeviceId");
            var patch = new {
                    properties = new {
                        desired = new {
                            telemetryConfig = new {
                                configId = Guid.NewGuid().ToString(),
                                sendFrequency = "5m"
                            }
                        }
                    }
                };
   
            await registryManager.UpdateTwinAsync(twin.DeviceId, JsonConvert.SerializeObject(patch), twin.ETag);
            Console.WriteLine("Updated desired configuration");
   
            try
            {
                while (true)
                {
                    var query = registryManager.CreateQuery("SELECT * FROM devices WHERE deviceId = 'myDeviceId'");
                    var results = await query.GetNextAsTwinAsync();
                    foreach (var result in results)
                    {
                        Console.WriteLine("Config report for: {0}", result.DeviceId);
                        Console.WriteLine("Desired telemetryConfig: {0}", JsonConvert.SerializeObject(result.Properties.Desired["telemetryConfig"], Formatting.Indented));
                        Console.WriteLine("Reported telemetryConfig: {0}", JsonConvert.SerializeObject(result.Properties.Reported["telemetryConfig"], Formatting.Indented));
                        Console.WriteLine();
                    }
                    Thread.Sleep(10000);
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Exception: {ex.Message}");
            }
        }
   
    hello**登錄**物件會公開與裝置雙 hello 服務從所有 hello 方法 toointeract 必要。 這個程式碼初始化 hello**登錄**物件，擷取 hello 的裝置兩個**myDeviceId**，然後使用新的遙測組態物件中更新其所需的屬性。
    之後，它會查詢 hello 裝置雙儲存在 hello IoT 中樞每隔 10 秒鐘，而想要的沖印 hello，與回報遙測組態。 請參閱 toohello [IoT 中樞的查詢語言][ lnk-query] toolearn toogenerate 豐富報告的方式，跨所有裝置。
   
   > [!IMPORTANT]
   > 為了便於說明，此應用程式每 10 秒查詢一次 IoT 中樞。 使用跨許多裝置和非 toodetect 變更查詢 toogenerate 面對使用者的報表。 如果您的解決方案需要裝置事件的即時通知，請使用[對應項通知][lnk-twin-notifications]。
   > 
   > 
1. 最後，加入下列行 toohello hello **Main**方法：
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        SetDesiredConfigurationAndQuery().Wait();
        Console.WriteLine("Press any key tooquit.");
        Console.ReadLine();
1. 在 hello 方案總管 中，開啟 hello**設定啟始專案...** ，請確定 hello**動作**如**SetDesiredConfigurationAndQuery**專案是**啟動**。 建置 hello 方案。
1. 與**SimulateDeviceConfiguration.js**執行，請從使用 Visual Studio 執行 hello.NET 應用程式**F5** ，您應該會看見 hello 報告的設定，變更從**成功**太**暫止**太**成功**再次傳送 hello 新的作用中的 五分鐘，而不是 24 小時的頻率。

 ![已成功設定裝置][img-deviceconfigured]
   
   > [!IMPORTANT]
   > 沒有向上 tooa 分鐘 hello 裝置報告作業和 hello 查詢結果之間的延遲。 這是 tooenable hello 查詢在極高的小數位數的基礎結構 toowork。 tooretrieve 一致檢視的單一裝置的兩個使用 hello **getDeviceTwin**方法在 hello**登錄**類別。
   > 
   > 

## <a name="next-steps"></a>後續步驟
在本教學課程中，您可以設定為所需的組態*所需屬性*hello 方案從備份結束時，和寫入裝置的應用程式 toodetect 的變更，並模擬報告其狀態報告的 hello 透過多個步驟更新程序屬性。

下列資源 toolearn 如何使用 hello 至：

* 從以 hello 的裝置將遙測傳送[開始使用 IoT 中樞][ lnk-iothub-getstarted]教學課程中，
* 排程執行，或是執行大量的裝置上的作業，請參閱 「 hello[排程和廣播的工作][ lnk-schedule-jobs]教學課程。
* 控制裝置以互動方式 （例如開啟風扇從使用者控制的應用程式），以 hello[使用直接的方法][ lnk-methods-tutorial]教學課程。

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-node-twin-how-to-configure/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-node-twin-how-to-configure/createnetapp.png
[img-deviceconfigured]: media/iot-hub-csharp-node-twin-how-to-configure/deviceconfigured.png

<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/1.1.0/

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-twin-notifications]: iot-hub-devguide-device-twins.md#back-end-operations
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-dm-overview]: iot-hub-device-management-overview.md
[lnk-twin-tutorial]: iot-hub-node-node-twin-getstarted.md
[lnk-schedule-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/
[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iothub-getstarted]: iot-hub-node-node-getstarted.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md

[lnk-guid]: https://en.wikipedia.org/wiki/Globally_unique_identifier

[lnk-how-to-configure-createapp]: iot-hub-csharp-node-twin-how-to-configure.md#create-the-simulated-device-app
