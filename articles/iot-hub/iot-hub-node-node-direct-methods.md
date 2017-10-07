---
title: "IoT 中樞 aaaAzure 直接方法 （節點） |Microsoft 文件"
description: "如何 toouse Azure IoT 中樞直接的方法。 您可以使用 hello Azure IoT Sdk for Node.js tooimplement 模擬的裝置應用程式，其中包含直接的方法與 hello 直接的方法會叫用的服務應用程式。"
services: iot-hub
documentationcenter: 
author: nberdy
manager: timlt
editor: 
ms.assetid: ea9c73ca-7778-4e38-a8f1-0bee9d142f04
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: nberdy
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 12300ba451816fec1f80163b633f6b6e411d9e5c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-direct-methods-on-your-iot-device-with-nodejs"></a>搭配 Node.js 在 IoT 裝置上使用直接方法
[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

在本教學課程的 hello 最後，您有兩個 Node.js 主控台應用程式：

* **CallMethodOnDevice.js**，其中呼叫 hello 模擬的裝置應用程式中的方法，並顯示 hello 回應。
* **SimulatedDevice.js**，連接 tooyour IoT 中樞與 hello 稍早建立的裝置身分識別以及回應 hello 雲端呼叫 toohello 方法。

> [!NOTE]
> hello 文章[Azure IoT Sdk] [ lnk-hub-sdks]提供 hello Azure IoT Sdk 的相關資訊，您可以使用 toobuild 這兩個應用程式 toorun 裝置和您的方案後端上。
> 
> 

toocomplete 本教學課程中，您需要遵循的 hello:

* Node.js 0.10.x 版或更新版本。
* 使用中的 Azure 帳戶。 (如果您沒有帳戶，只需要幾分鐘的時間就可以建立[免費帳戶][lnk-free-trial]。)

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a>建立模擬裝置應用程式
本節中，您可以建立會回應呼叫 hello 雲端 tooa 方法 Node.js 主控台應用程式。

1. 建立稱為 **simulateddevice**的新的空資料夾。 在 hello **simulateddevice**資料夾中，建立使用下列命令，在您的命令提示字元的 hello package.json 檔案。 接受所有的 hello 預設值：
   
    ```
    npm init
    ```
2. 在您的命令提示字元中 hello **simulateddevice**資料夾中，執行下列命令 tooinstall hello hello **azure iot 裝置**裝置 SDK 封裝和**azure-iot-裝置-mqtt**封裝：
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. 使用文字編輯器中，建立新**SimulatedDevice.js**檔案在 hello **simulateddevice**資料夾。
4. 新增下列 hello`require`陳述式在 hello 開頭 hello **SimulatedDevice.js**檔案：
   
    ```
    'use strict';
   
    var Mqtt = require('azure-iot-device-mqtt').Mqtt;
    var DeviceClient = require('azure-iot-device').Client;
    ```
5. 新增**connectionString**變數，並使用它 toocreate **DeviceClient**執行個體。 取代**{裝置連接字串}** hello 裝置連接字串中 hello 產生*建立裝置身分識別*> 一節：
   
    ```
    var connectionString = '{device connection string}';
    var client = DeviceClient.fromConnectionString(connectionString, Mqtt);
    ```
6. 加入下列函式 tooimplement hello 方法 hello 裝置上的 hello:
   
    ```
    function onWriteLine(request, response) {
        console.log(request.payload);
   
        response.send(200, 'Input was written toolog.', function(err) {
            if(err) {
                console.error('An error ocurred when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.' );
            }
        });
    }
    ```
7. 開啟 hello 連接 tooyour IoT 中樞，並啟動初始化 hello 方法接聽程式：
   
    ```
    client.open(function(err) {
        if (err) {
            console.error('could not open IotHub client');
        }  else {
            console.log('client opened');
            client.onDeviceMethod('writeLine', onWriteLine);
        }
    });
    ```
8. 儲存並關閉 hello **SimulatedDevice.js**檔案。

> [!NOTE]
> 簡單 tookeep 方面，本教學課程未實作任何重試原則。 在實際執行程式碼，您應該實作重試原則 （例如連線重試），做為建議 hello MSDN 文件中[暫時性錯誤處理][lnk-transient-faults]。
> 
> 

## <a name="call-a-method-on-a-device"></a>在裝置上呼叫方法
在本節中，您可以建立 Node.js 主控台應用程式會呼叫 hello 模擬的裝置應用程式中的方法，並顯示 hello 回應。

1. 建立稱為 **callmethodondevice**的新的空資料夾。 在 hello **callmethodondevice**資料夾中，建立使用下列命令，在您的命令提示字元的 hello package.json 檔案。 接受所有的 hello 預設值：
   
    ```
    npm init
    ```
2. 在您的命令提示字元中 hello **callmethodondevice**資料夾中，執行下列命令 tooinstall hello hello **azure iot 中樞**封裝：
   
    ```
    npm install azure-iothub --save
    ```
3. 使用文字編輯器中，建立**CallMethodOnDevice.js**檔案在 hello **callmethodondevice**資料夾。
4. 新增下列 hello`require`陳述式在 hello 開頭 hello **CallMethodOnDevice.js**檔案：
   
    ```
    'use strict';
   
    var Client = require('azure-iothub').Client;
    ```
5. 加入下列變數宣告 hello 和 hello 預留位置值取代為您的中樞的 IoT 中樞連接字串 hello:
   
    ```
    var connectionString = '{iothub connection string}';
    var methodName = 'writeLine';
    var deviceId = 'myDeviceId';
    ```
6. 建立 hello 用 tooopen hello 連接 tooyour IoT 中樞。
   
    ```
    var client = Client.fromConnectionString(connectionString);
    ```
7. 加入下列函式 tooinvoke hello 裝置方法及列印 hello 裝置回應 toohello 主控台 hello:
   
    ```
    var methodParams = {
        methodName: methodName,
        payload: 'hello world',
        timeoutInSeconds: 30
    };
   
    client.invokeDeviceMethod(deviceId, methodParams, function (err, result) {
        if (err) {
            console.error('Failed tooinvoke method \'' + methodName + '\': ' + err.message);
        } else {
            console.log(methodName + ' on ' + deviceId + ':');
            console.log(JSON.stringify(result, null, 2));
        }
    });
    ```
8. 儲存並關閉 hello **CallMethodOnDevice.js**檔案。

## <a name="run-hello-apps"></a>執行 hello 應用程式
現在您已經準備就緒 toorun hello 應用程式。

1. 在命令提示字元中 hello **simulateddevice**資料夾中，執行下列命令 toostart 接聽從 IoT 中樞的方法呼叫的 hello:
   
    ```
    node SimulatedDevice.js
    ```
   
    ![][7]
2. 在命令提示字元中 hello **callmethodondevice**資料夾中，執行下列命令 toobegin 監視您的 IoT 中樞的 hello:
   
    ```
    node CallMethodOnDevice.js 
    ```
   
    ![][8]
3. 您會看見 hello 回應 toohello 方法列印出 hello 訊息和呼叫 hello 方法顯示 hello 回應 hello 裝置 hello 應用程式的裝置：
   
    ![][9]

## <a name="next-steps"></a>後續步驟
在本教學課程中，您在 hello Azure 入口網站中設定新的 IoT 中樞，並接著 hello IoT 中樞的身分識別登錄中建立裝置身分識別。 您已經使用此裝置身分識別 tooenable hello 模擬裝置的應用程式 tooreact toomethods hello 雲端所叫用。 您也會建立叫用 hello 裝置上的方法，並會顯示 hello 回應 hello 裝置的應用程式。 

使用者入門 toocontinue tooexplore IoT 中樞與其他 IoT 案例，請參閱：

* [IoT 中心入門]
* [排程多個裝置上的作業][lnk-devguide-jobs]

toolearn 如何 tooextend IoT 解決方案和排程方法呼叫上多個裝置，請參閱 hello[排程和廣播的工作][ lnk-tutorial-jobs]教學課程。

<!-- Images. -->
[7]: ./media/iot-hub-node-node-direct-methods/run-simulated-device.png
[8]: ./media/iot-hub-node-node-direct-methods/run-callmethodondevice.png
[9]: ./media/iot-hub-node-node-direct-methods/methods-output.png

<!-- Links -->
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal]: https://portal.azure.com/

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-devguide-methods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md

[Send Cloud-to-Device messages with IoT Hub]: iot-hub-csharp-csharp-c2d.md
[Process Device-to-Cloud messages]: iot-hub-csharp-csharp-process-d2c.md
[IoT 中心入門]: iot-hub-node-node-getstarted.md
