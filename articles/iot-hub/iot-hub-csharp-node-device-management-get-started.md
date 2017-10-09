---
title: "aaaGet 開始使用 Azure IoT 中心裝置管理 （.NET/節點） |Microsoft 文件"
description: "如何 toouse Azure IoT 中心裝置管理 tooinitiate 遠端裝置重新開機。 您可以使用 hello Azure IoT 裝置 SDK for Node.js tooimplement 模擬的裝置應用程式，其中包含直接的方法和 hello Azure IoT 服務 SDK for.NET tooimplement hello 直接的方法會叫用的服務應用程式。"
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: e044006d-ffd6-469b-bc63-c182ad066e31
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/17/2016
ms.author: juanpere
ms.openlocfilehash: ea6d50dfac1c222d7836e3bf5503c6c9b8c89dfa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-management-netnode"></a>開始使用裝置管理 (.NET/Node)

[!INCLUDE [iot-hub-selector-dm-getstarted](../../includes/iot-hub-selector-dm-getstarted.md)]

本教學課程說明如何：

* 使用 hello Azure 入口網站 toocreate IoT 中樞，並在您的 IoT 中樞中建立裝置身分識別。
* 建立模擬裝置應用程式，其包含可將該裝置重新開機的直接方法。 直接的方法會叫用從 hello 雲端。
* 建立.NET 主控台應用程式透過您的 IoT 中樞 hello 模擬的裝置應用程式中呼叫 hello 重新開機直接的方法。

在本教學課程的 hello 最後，您有 Node.js 主控台裝置應用程式和.NET (C#) 主控台後端應用程式：

**dmpatterns_getstarted_device.js**，稍早建立的 hello 裝置身分識別與連線 tooyour IoT 中樞收到重新開機直接的方法，會模擬實際的重新開機，並報告 hello hello 上次重新開機的時間。

**TriggerReboot**、 直接的方法呼叫 hello 模擬的裝置，應用程式中顯示 hello 回應，並顯示 hello 更新報告內容。

toocomplete 本教學課程中，您需要遵循的 hello:

* Visual Studio 2015 或 Visual Studio 2017。
* Node.js 0.12.x 版或更新版本， <br/>  [準備開發環境][ lnk-dev-setup]描述如何 tooinstall Node.js 本教學課程中的 Windows 或 Linux。
* 使用中的 Azure 帳戶。 (如果您沒有帳戶，只需要幾分鐘的時間就可以建立[免費帳戶][lnk-free-trial]。)

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-reboot-on-hello-device-using-a-direct-method"></a>觸發程序使用直接的方法 hello 裝置上遠端重新開機
在本節中，您會建立 .NET 主控台應用程式 (使用 C#)，此應用程式會使用直接方法起始遠端重新開機。 hello 應用程式中使用該裝置的裝置兩個查詢 toodiscover hello 上次重新開機。

1. 在 Visual Studio 中，將 Visual C# Windows 傳統桌面專案 tooa 新方案使用 hello**主控台應用程式 (.NET Framework)**專案範本。 請確定 hello.NET Framework 版本 4.5.1 或更新版本。 名稱 hello 專案**TriggerReboot**。

    ![新的 Visual C# Windows 傳統桌面專案][img-createapp]

2. 在 [方案總管] 中，以滑鼠右鍵按一下 hello **TriggerReboot**專案，然後再按一下**管理 NuGet 封裝**。
3. 在 hello **NuGet 套件管理員**視窗中，選取**瀏覽**，搜尋**microsoft.azure.devices**，選取**安裝**tooinstallhello **Microsoft.Azure.Devices**封裝，並接受使用規定 hello。 此程序下載、 安裝，並新增參考 toohello [Azure IoT 服務 SDK] [ lnk-nuget-service-sdk] NuGet 封裝和其相依性。

    ![NuGet 封裝管理員視窗][img-servicenuget]
4. 新增下列 hello`using`在 hello hello 最上方的陳述式**Program.cs**檔案：
   
        using Microsoft.Azure.Devices;
        using Microsoft.Azure.Devices.Shared;
        
5. 新增下列欄位 toohello hello**程式**類別。 取代 hello hello 中樞 hello 上一節和 hello 目標裝置中您建立 IoT 中樞連接字串中的 hello 預留位置的值。
   
        static RegistryManager registryManager;
        static string connString = "{iot hub connection string}";
        static ServiceClient client;
        static JobClient jobClient;
        static string targetDevice = "{deviceIdForTargetDevice}";
        
6. 新增下列方法 toohello hello**程式**類別。  重新啟動裝置和輸出 hello hello 這個程式碼取得 hello 裝置兩個報告的屬性。
   
        public static async Task QueryTwinRebootReported()
        {
            Twin twin = await registryManager.GetTwinAsync(targetDevice);
            Console.WriteLine(twin.Properties.Reported.ToJson());
        }
        
7. 新增下列方法 toohello hello**程式**類別。  此程式碼起始 hello 重新開機 hello 裝置上使用直接的方法。

        public static async Task StartReboot()
        {
            client = ServiceClient.CreateFromConnectionString(connString);
            CloudToDeviceMethod method = new CloudToDeviceMethod("reboot");
            method.ResponseTimeout = TimeSpan.FromSeconds(30);

            CloudToDeviceMethodResult result = await client.InvokeDeviceMethodAsync(targetDevice, method);

            Console.WriteLine("Invoked firmware update on device.");
        }

7. 最後，加入下列行 toohello hello **Main**方法：
   
        registryManager = RegistryManager.CreateFromConnectionString(connString);
        StartReboot().Wait();
        QueryTwinRebootReported().Wait();
        Console.WriteLine("Press ENTER tooexit.");
        Console.ReadLine();
        
8. 建置 hello 方案。

## <a name="create-a-simulated-device-app"></a>建立模擬裝置應用程式
在本節中，您將：

* 建立回應 tooa 直接方法呼叫 hello 雲端 Node.js 主控台應用程式
* 觸發模擬裝置重新啟動
* 使用 hello 報告屬性 tooenable 裝置兩個查詢 tooidentify 裝置，當它們一次啟動

1. 建立稱為 **manageddevice**的新的空資料夾。  在 hello **manageddevice**資料夾中，建立使用下列命令，在您的命令提示字元的 hello package.json 檔案。  接受所有的 hello 預設值：
   
    ```
    npm init
    ```
2. 在您的命令提示字元中 hello **manageddevice**資料夾中，執行下列命令 tooinstall hello hello **azure iot 裝置**裝置 SDK 封裝和**azure-iot-裝置-mqtt**封裝：
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. 使用文字編輯器中，建立新**dmpatterns_getstarted_device.js**檔案在 hello **manageddevice**資料夾。
4. 新增 hello 下列的 '需要' 陳述式在 hello 開頭的 hello **dmpatterns_getstarted_device.js**檔案：
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
5. 新增**connectionString**變數，並使用它 toocreate**用戶端**執行個體。  Hello 連接字串取代為您的裝置連接字串。  
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId=myDeviceId;SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```
6. 新增 hello 遵循 hello 裝置上的函式 tooimplement hello 直接方法
   
    ```
    var onReboot = function(request, response) {
   
        // Respond hello cloud app for hello direct method
        response.send(200, 'Reboot started', function(err) {
            if (!err) {
                console.error('An error occured when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.');
            }
        });
   
        // Report hello reboot before hello physical restart
        var date = new Date();
        var patch = {
            iothubDM : {
                reboot : {
                    lastReboot : date.toISOString(),
                }
            }
        };
   
        // Get device Twin
        client.getTwin(function(err, twin) {
            if (err) {
                console.error('could not get twin');
            } else {
                console.log('twin acquired');
                twin.properties.reported.update(patch, function(err) {
                    if (err) throw err;
                    console.log('Device reboot twin state reported')
                });  
            }
        });
   
        // Add your device's reboot API for physical restart.
        console.log('Rebooting!');
    };
    ```
7. 加入 hello 下列程式碼 tooopen hello 連接 tooyour IoT 中樞，並啟動 hello 直接方法接聽程式：
   
    ```
    client.open(function(err) {
        if (err) {
            console.error('Could not open IotHub client');
        }  else {
            console.log('Client opened.  Waiting for reboot method.');
            client.onDeviceMethod('reboot', onReboot);
        }
    });
    ```
8. 儲存並關閉 hello **dmpatterns_getstarted_device.js**檔案。
   
> [!NOTE]
> 簡單 tookeep 方面，本教學課程未實作任何重試原則。 在實際執行程式碼，您應該實作重試原則 （例如指數型輪詢），做為建議 hello MSDN 文件中[暫時性錯誤處理][lnk-transient-faults]。


## <a name="run-hello-apps"></a>執行 hello 應用程式
現在您已經準備就緒 toorun hello 應用程式。

1. 在 hello 命令提示字元中 hello **manageddevice**資料夾中，執行下列命令 toobegin 接聽 hello 重新開機直接方法 hello。
   
    ```
    node dmpatterns_getstarted_device.js
    ```
2. 執行的 hello C# 主控台應用程式**TriggerReboot**。 以滑鼠右鍵按一下 hello **TriggerReboot**專案，然後選取**偵錯**，然後選取**開始新執行個體**。

3. 您會看到 hello 裝置回應 toohello 直接方法 hello 主控台中。

[!INCLUDE [iot-hub-dm-followup](../../includes/iot-hub-dm-followup.md)]

<!-- images and links -->
[img-output]: media/iot-hub-get-started-with-dm/image6.png
[img-dm-ui]: media/iot-hub-get-started-with-dm/dmui.png
[img-servicenuget]: media/iot-hub-csharp-node-device-management-get-started/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-node-device-management-get-started/createnetapp.png

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md

[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[Azure portal]: https://portal.azure.com/
[Using resource groups toomanage your Azure resources]: ../azure-portal/resource-group-portal.md
[lnk-dm-github]: https://github.com/Azure/azure-iot-device-management

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/