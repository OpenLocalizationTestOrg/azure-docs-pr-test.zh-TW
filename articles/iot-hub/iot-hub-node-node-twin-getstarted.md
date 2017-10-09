---
title: "aaaGet 開始使用 Azure IoT Hub 裝置雙 （節點） |Microsoft 文件"
description: "如何 toouse Azure IoT Hub 裝置雙 tooadd 標記，然後再使用 IoT 中樞查詢。 您可以使用 hello Azure IoT Sdk for Node.js tooimplement hello 模擬的裝置的應用程式和服務應用程式加入 hello 標記，並執行 hello IoT 中樞查詢。"
services: iot-hub
documentationcenter: node
author: fsautomata
manager: timlt
editor: 
ms.assetid: 314c88e4-cce1-441c-b75a-d2e08e39ae7d
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: elioda
ms.openlocfilehash: d60b8c3de85e9285e496b86e27d4ee31a0554a1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-twins-node"></a>開始使用裝置對應項 (Node)
[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

在本教學課程的 hello 結束時，您將擁有兩個 Node.js 主控台應用程式：

* **AddTagsAndQuery.js**，這是 Node.js 後端應用程式，可新增標籤和查詢裝置對應項。
* **TwinSimulatedDevice.js**，Node.js 應用程式會模擬 tooyour IoT 中樞連線以稍早建立的 hello 裝置身分識別的裝置，並回報其連線的情況。

> [!NOTE]
> hello 文章[Azure IoT Sdk] [ lnk-hub-sdks]提供 hello Azure IoT Sdk 的相關資訊，您可以使用 toobuild 裝置與後端應用程式。
> 
> 

toocomplete 需要 hello 下列本教學課程：

* Node.js 0.10.x 版或更新版本。
* 使用中的 Azure 帳戶。 (如果您沒有帳戶，只需要幾分鐘的時間就可以建立[免費帳戶][lnk-free-trial]。)

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-hello-service-app"></a>建立 hello 服務應用程式
在本節中，您會建立將位置的中繼資料 toohello 裝置兩個相關聯的 Node.js 主控台應用程式**myDeviceId**。 接著，它查詢 hello 裝置雙 US，儲存在選取位於 hello hello 裝置 hello IoT 中樞中，然後 hello 所報告的行動電話通訊的連接。

1. 建立稱為 **addtagsandqueryapp** 的新空白資料夾。 在 hello **addtagsandqueryapp**資料夾中，建立新的 package.json 檔案使用下列命令，在您的命令提示字元的 hello。 接受所有的 hello 預設值：
   
    ```
    npm init
    ```
2. 在您的命令提示字元中 hello **addtagsandqueryapp**資料夾中，執行下列命令 tooinstall hello hello **azure iot 中樞**封裝：
   
    ```
    npm install azure-iothub --save
    ```
3. 使用文字編輯器中，建立新**AddTagsAndQuery.js**檔案在 hello **addtagsandqueryapp**資料夾。
4. 新增下列程式碼 toohello hello **AddTagsAndQuery.js**檔案，並以取代 hello **{iot 中樞連接字串}**預留位置 hello 您複製當您建立中樞的 IoT 中樞連接字串：
   
        'use strict';
        var iothub = require('azure-iothub');
        var connectionString = '{iot hub connection string}';
        var registry = iothub.Registry.fromConnectionString(connectionString);
   
        registry.getTwin('myDeviceId', function(err, twin){
            if (err) {
                console.error(err.constructor.name + ': ' + err.message);
            } else {
                var patch = {
                    tags: {
                        location: {
                            region: 'US',
                            plant: 'Redmond43'
                      }
                    }
                };
   
                twin.update(patch, function(err) {
                  if (err) {
                    console.error('Could not update twin: ' + err.constructor.name + ': ' + err.message);
                  } else {
                    console.log(twin.deviceId + ' twin updated successfully');
                    queryTwins();
                  }
                });
            }
        });
   
    hello**登錄**物件會公開與裝置雙 hello 服務從所有 hello 方法 toointeract 必要。 hello 先前的程式碼會先初始化 hello**登錄**物件，然後擷取 hello 的裝置兩個**myDeviceId**，且最後 hello 預期位置資訊會以更新其標籤。
   
    Hello 之後更新 hello 標記放在它呼叫 hello **queryTwins**函式。
5. 新增下列程式碼結尾的 hello hello **AddTagsAndQuery.js** tooimplement hello **queryTwins**函式：
   
        var queryTwins = function() {
            var query = registry.createQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43'", 100);
            query.nextAsTwin(function(err, results) {
                if (err) {
                    console.error('Failed toofetch hello results: ' + err.message);
                } else {
                    console.log("Devices in Redmond43: " + results.map(function(twin) {return twin.deviceId}).join(','));
                }
            });
   
            query = registry.createQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43' AND properties.reported.connectivity.type = 'cellular'", 100);
            query.nextAsTwin(function(err, results) {
                if (err) {
                    console.error('Failed toofetch hello results: ' + err.message);
                } else {
                    console.log("Devices in Redmond43 using cellular network: " + results.map(function(twin) {return twin.deviceId}).join(','));
                }
            });
        };
   
    hello 先前的程式碼會執行兩個查詢： hello 會先選取只 hello 裝置雙的裝置位於 hello **Redmond43**工廠和 hello 第二個精簡 hello 查詢 tooselect 只有 hello 裝置也會透過連接行動電話通訊網路。
   
    請注意該 hello 先前的程式碼，當它建立 hello**查詢**物件，指定傳回的文件的最大數目。 hello**查詢**物件包含**hasMoreResults**布林值屬性，您可以使用 tooinvoke hello **nextAsTwin**方法多次 tooretrieve 所有結果。 有一個稱為 **next** 的方法適用於不是裝置對應項的結果，例如彙總查詢的結果。
6. 執行與 hello 應用程式：
   
        node AddTagsAndQuery.js
   
    您應該會看到一個裝置 hello 結果中的 hello 查詢要求的所有裝置都位於**Redmond43**和無限制 hello 的 hello 查詢結果 toodevices 使用行動電話通訊網路。
   
    ![][1]

Hello 下一節中建立報告 hello 連線資訊裝置應用程式，然後變更 hello hello 前一節中的 hello 查詢的結果。

## <a name="create-hello-device-app"></a>建立 hello 裝置應用程式
在本節中，您建立 Node.js 主控台應用程式連接成 tooyour 中樞**myDeviceId**，，然後更新其裝置的兩個的報告屬性 toocontain hello 資訊已連接使用行動電話通訊網路。

> [!NOTE]
> 此時，裝置雙都只連接 tooIoT 中樞的裝置可以存取使用 hello MQTT 通訊協定。 請參閱 toohello [MQTT 支援][ lnk-devguide-mqtt]文章的指示現有裝置的應用程式 toouse tooconvert MQTT。
> 
> 

1. 建立稱為 **reportconnectivity** 的新空白資料夾。 在 hello **reportconnectivity**資料夾中，建立新的 package.json 檔案使用下列命令，在您的命令提示字元的 hello。 接受所有的 hello 預設值：
   
    ```
    npm init
    ```
2. 在您的命令提示字元中 hello **reportconnectivity**資料夾中，執行下列命令 tooinstall hello hello **azure iot 裝置**，和**azure iot 裝置-mqtt**封裝:
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. 使用文字編輯器中，建立新**ReportConnectivity.js**檔案在 hello **reportconnectivity**資料夾。
4. 新增下列程式碼 toohello hello **ReportConnectivity.js**檔案，並以取代 hello **{裝置連接字串}**預留位置複製時建立 hello hello 裝置連接字串**myDeviceId**裝置身分識別：
   
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
5. 執行 hello 裝置應用程式
   
        node ReportConnectivity.js
   
    您應該會看到 hello 訊息`twin state reported`。
6. 既然 hello 裝置報告其連線資訊時，它應該會出現在這兩個查詢。 移入 hello **addtagsandqueryapp** hello 資料夾並執行查詢一次：
   
        node AddTagsAndQuery.js
   
    這次，**myDeviceId** 應該會出現在這兩個查詢結果中。
   
    ![][3]

## <a name="next-steps"></a>後續步驟
在本教學課程中，您在 hello Azure 入口網站中設定新的 IoT 中樞，並接著 hello IoT 中樞的身分識別登錄中建立裝置身分識別。 您標記為加入裝置中繼資料，從後端應用程式，並在 hello 裝置兩個撰寫模擬的裝置的應用程式 tooreport 裝置連線資訊。 您也學到如何 tooquery 這項資訊使用 hello 類似 SQL 的 IoT 中樞查詢語言。

下列資源 toolearn 如何使用 hello 至：

* 從以 hello 的裝置將遙測傳送[開始使用 IoT 中樞][ lnk-iothub-getstarted]教學課程中，
* 設定裝置使用兩個裝置所需的屬性以 hello[使用想要的話屬性 tooconfigure 裝置][ lnk-twin-how-to-configure]教學課程中，
* 控制裝置以互動方式 （例如開啟風扇從使用者控制的應用程式），以 hello[使用直接的方法][ lnk-methods-tutorial]教學課程。

<!-- images -->
[1]: media/iot-hub-node-node-twin-getstarted/service1.png
[3]: media/iot-hub-node-node-twin-getstarted/service2.png

<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[lnk-d2c]: iot-hub-devguide-messaging.md#device-to-cloud-messages
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-identity]: iot-hub-devguide-identity-registry.md

[lnk-iothub-getstarted]: iot-hub-node-node-getstarted.md
[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/

[lnk-twin-how-to-configure]: iot-hub-node-node-twin-how-to-configure.md
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md

[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
