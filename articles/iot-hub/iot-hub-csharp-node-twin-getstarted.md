---
title: "aaaGet 開始使用 Azure IoT Hub 裝置雙 （.NET/節點） |Microsoft 文件"
description: "如何 toouse Azure IoT Hub 裝置雙 tooadd 標記，然後再使用 IoT 中樞查詢。 您可以使用 hello Azure IoT 裝置 SDK for Node.js tooimplement hello 模擬的裝置的應用程式與 hello Azure IoT 服務 SDK for.NET tooimplement 加入 hello 標記，並執行 hello IoT 中樞查詢中的服務應用程式。"
services: iot-hub
documentationcenter: node
author: fsautomata
manager: timlt
editor: 
ms.assetid: f7e23b6e-bfde-4fba-a6ec-dbb0f0e005f4
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/29/2017
ms.author: elioda
ms.openlocfilehash: 1cec082ebddc19c9b87998a5fd0159d32b07acd8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-twins-netnode"></a>開始使用裝置對應項 (.NET/Node)
[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

在本教學課程的 hello 最後，您必須為.NET 和 Node.js 主控台應用程式：

* **AddTagsAndQuery.sln**，這是 .NET 後端應用程式，可新增標籤和查詢裝置對應項。
* **TwinSimulatedDevice.js**，Node.js 應用程式會模擬 tooyour IoT 中樞連線以稍早建立的 hello 裝置身分識別的裝置，並回報其連線的情況。

> [!NOTE]
> hello 文章[Azure IoT Sdk] [ lnk-hub-sdks]提供 hello Azure IoT Sdk 的相關資訊，您可以使用 toobuild 裝置與後端應用程式。
> 
> 

toocomplete 需要 hello 下列本教學課程：

* Visual Studio 2015 或 Visual Studio 2017。
* Node.js 0.10.x 版或更新版本。
* 使用中的 Azure 帳戶。 (如果您沒有帳戶，只需要幾分鐘的時間就可以建立[免費帳戶][lnk-free-trial]。)

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-hello-service-app"></a>建立 hello 服務應用程式
在本節中，您建立.NET 主控台應用程式 （使用 C#） 加入位置的中繼資料 toohello 裝置兩個相關聯**myDeviceId**。 接著，它查詢 hello 裝置雙 US，儲存在選取位於 hello hello 裝置 hello IoT 中樞中，然後 hello 所報告的行動電話通訊的連接。

1. 在 Visual Studio 中，將 Visual C# Windows 傳統桌面專案 toohello 目前方案使用 hello**主控台應用程式**專案範本。 名稱 hello 專案**AddTagsAndQuery**。
   
    ![新的 Visual C# Windows 傳統桌面專案][img-createapp]
1. 在 [方案總管] 中，以滑鼠右鍵按一下 hello **AddTagsAndQuery**專案，然後再按一下**管理 NuGet 封裝...**.
1. 在 hello **NuGet 套件管理員**視窗中，選取**瀏覽**並搜尋**microsoft.azure.devices**。 選取**安裝**tooinstall hello **Microsoft.Azure.Devices**封裝，並接受使用規定 hello。 此程序下載、 安裝，並新增參考 toohello [Azure IoT 服務 SDK] [ lnk-nuget-service-sdk] NuGet 封裝和其相依性。
   
    ![NuGet 封裝管理員視窗][img-servicenuget]
1. 新增下列 hello`using`在 hello hello 最上方的陳述式**Program.cs**檔案：
   
        using Microsoft.Azure.Devices;
1. 新增下列欄位 toohello hello**程式**類別。 取代 hello hello 中樞在 hello 上一節中所建立的 IoT 中樞連接字串中的 hello 預留位置的值。
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
1. 新增下列方法 toohello hello**程式**類別：
   
        public static async Task AddTagsAndQuery()
        {
            var twin = await registryManager.GetTwinAsync("myDeviceId");
            var patch =
                @"{
                    tags: {
                        location: {
                            region: 'US',
                            plant: 'Redmond43'
                        }
                    }
                }";
            await registryManager.UpdateTwinAsync(twin.DeviceId, patch, twin.ETag);
   
            var query = registryManager.CreateQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43'", 100);
            var twinsInRedmond43 = await query.GetNextAsTwinAsync();
            Console.WriteLine("Devices in Redmond43: {0}", string.Join(", ", twinsInRedmond43.Select(t => t.DeviceId)));
   
            query = registryManager.CreateQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43' AND properties.reported.connectivity.type = 'cellular'", 100);
            var twinsInRedmond43UsingCellular = await query.GetNextAsTwinAsync();
            Console.WriteLine("Devices in Redmond43 using cellular network: {0}", string.Join(", ", twinsInRedmond43UsingCellular.Select(t => t.DeviceId)));
        }
   
    hello **RegistryManager**類別會公開與裝置雙 hello 服務從所有 hello 方法 toointeract 必要。 hello 先前的程式碼會先初始化 hello **registryManager**物件，然後擷取 hello 的裝置兩個**myDeviceId**，且最後 hello 預期位置資訊會以更新其標籤。
   
    在更新之後，它會執行兩個查詢： hello 會先選取只 hello 裝置雙的裝置位於 hello **Redmond43**工廠和 hello 第二個精簡 hello 查詢 tooselect 只有 hello 裝置也會透過連接行動電話通訊網路。
   
    請注意該 hello 先前的程式碼，當它建立 hello**查詢**物件，指定傳回的文件的最大數目。 hello**查詢**物件包含**HasMoreResults**布林值屬性，您可以使用 tooinvoke hello **GetNextAsTwinAsync**方法多次 tooretrieve 所有結果。 有一個稱為 **GetNextAsJson** 的方法適用於不是裝置對應項的結果，例如彙總查詢的結果。
1. 最後，加入下列行 toohello hello **Main**方法：
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        AddTagsAndQuery().Wait();
        Console.WriteLine("Press Enter tooexit.");
        Console.ReadLine();

1. 在 hello 方案總管 中，開啟 hello**設定啟始專案...** ，請確定 hello**動作**如**AddTagsAndQuery**專案是**啟動**。 建置 hello 方案。
1. 執行此應用程式，以滑鼠右鍵按一下 hello **AddTagsAndQuery**專案，並選取**偵錯**，後面接著**開始新執行個體**。 您應該會看到一個裝置 hello 結果中的 hello 查詢要求的所有裝置都位於**Redmond43**和無限制 hello 的 hello 查詢結果 toodevices 使用行動電話通訊網路。
   
    ![視窗中的查詢結果][img-addtagapp]

Hello 下一節，您將建立報告 hello 連線資訊裝置應用程式，並變更 hello hello 前一節中的 hello 查詢的結果。

## <a name="create-hello-device-app"></a>建立 hello 裝置應用程式
在本節中，您建立 Node.js 主控台應用程式連接成 tooyour 中樞**myDeviceId**，，然後更新其已連線使用行動電話通訊網路的報告的屬性 toocontain hello 資訊。

1. 建立稱為 **reportconnectivity** 的新空白資料夾。 在 hello **reportconnectivity**資料夾中，建立新的 package.json 檔案使用下列命令，在您的命令提示字元的 hello。 接受所有的 hello 預設值。
   
    ```
    npm init
    ```
1. 在您的命令提示字元中 hello **reportconnectivity**資料夾中，執行下列命令 tooinstall hello hello **azure iot 裝置**，和**azure iot 裝置-mqtt**封裝:
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
1. 使用文字編輯器中，建立新**ReportConnectivity.js**檔案在 hello **reportconnectivity**資料夾。
1. 新增下列程式碼 toohello hello **ReportConnectivity.js**檔案，並以取代 hello 預留位置裝置連接字串，以建立 hello 時您複製一個 hello **myDeviceId**裝置身分識別：
   
        'use strict';
        var Client = require('azure-iot-device').Client;
        var Protocol = require('azure-iot-device-mqtt').Mqtt;
   
        var connectionString = '{device connection string}';
        var client = Client.fromConnectionString(connectionString, Protocol);
   
        client.open(function(err) {
        if (err) {
            console.error('could not open IotHub client');
        }  else {
            console.log('client opened');
   
            client.getTwin(function(err, twin) {
            if (err) {
                console.error('could not get twin');
            } else {
                var patch = {
                    connectivity: {
                        type: 'cellular'
                    }
                };
   
                twin.properties.reported.update(patch, function(err) {
                    if (err) {
                        console.error('could not update twin');
                    } else {
                        console.log('twin state reported');
                        process.exit();
                    }
                });
            }
            });
        }
        });
   
    hello**用戶端**物件會公開您需要將裝置從 hello 裝置的雙具備 toointeract 所有 hello 方法。 hello 先前的程式碼，它會初始化 hello 之後**用戶端**物件，擷取 hello 的裝置兩個**myDeviceId**及更新其報告的屬性與 hello 連線資訊。
1. 執行 hello 裝置應用程式
   
        node ReportConnectivity.js
   
    您應該會看到 hello 訊息`twin state reported`。
1. 既然 hello 裝置報告其連線資訊時，它應該會出現在這兩個查詢。 執行 hello.NET **AddTagsAndQuery**應用程式 toorun hello 查詢一次。 這次，**myDeviceId** 應該會出現在這兩個查詢結果中。
   
    ![][img-addtagapp2]

## <a name="next-steps"></a>後續步驟
在本教學課程中，您在 hello Azure 入口網站中設定新的 IoT 中樞，並接著 hello IoT 中樞的身分識別登錄中建立裝置身分識別。 您標記為加入裝置中繼資料，從後端應用程式，並在 hello 裝置兩個撰寫模擬的裝置的應用程式 tooreport 裝置連線資訊。 您也學到如何 tooquery 這項資訊使用 hello 類似 SQL 的 IoT 中樞查詢語言。

下列資源 toolearn 如何使用 hello 至：

* 從以 hello 的裝置將遙測傳送[開始使用 IoT 中樞][ lnk-iothub-getstarted]教學課程中，
* 設定裝置使用兩個裝置所需的屬性以 hello[使用想要的話屬性 tooconfigure 裝置][ lnk-twin-how-to-configure]教學課程中，
* 控制以互動方式 （例如開啟風扇從使用者控制的應用程式） 的裝置以 hello[使用直接的方法][ lnk-methods-tutorial]教學課程。

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-node-twin-getstarted/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-node-twin-getstarted/createnetapp.png
[img-addtagapp]: media/iot-hub-csharp-node-twin-getstarted/addtagapp.png
[img-addtagapp2]: media/iot-hub-csharp-node-twin-getstarted/addtagapp2.png

<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/

[lnk-d2c]: iot-hub-devguide-messaging.md#device-to-cloud-messages
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-identity]: iot-hub-devguide-identity-registry.md

[lnk-iothub-getstarted]: iot-hub-node-node-getstarted.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-twin-how-to-configure]: iot-hub-csharp-node-twin-how-to-configure.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md

