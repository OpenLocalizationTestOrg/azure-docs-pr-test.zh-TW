---
title: "aaaGet 開始使用 Azure IoT 中樞 （節點） |Microsoft 文件"
description: "了解如何 toosend 裝置到雲端訊息 tooAzure 使用 IoT Sdk for Node.js 的 IoT 中樞。 建立模擬的裝置和服務應用程式 tooregister 您的裝置、 傳送訊息，以及從 IoT 中樞讀取訊息。"
services: iot-hub
documentationcenter: nodejs
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 56618522-9a31-42c6-94bf-55e2233b39ac
ms.service: iot-hub
ms.devlang: javascript
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/22/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d0747895365f2359a9c38ea1e85a5881d6efec0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-simulated-device-tooyour-iot-hub-using-node"></a>連接使用節點您模擬的裝置 tooyour IoT 中樞
[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

在本教學課程的 hello 最後，您有三個 Node.js 主控台應用程式：

* **CreateDeviceIdentity.js**，這樣就可以建立裝置身分識別，以及相關聯的安全性金鑰 tooconnect 應用程式模擬的裝置。
* **ReadDeviceToCloudMessages.js**，其中顯示模擬的裝置之應用程式所傳送的 hello 遙測。
* **SimulatedDevice.js**，這與 hello 稍早建立的裝置身分識別連接 tooyour IoT 中樞，並傳送遙測訊息每個第二個使用 hello MQTT 通訊協定。

> [!NOTE]
> hello 文章[Azure IoT Sdk] [ lnk-hub-sdks]提供 hello Azure IoT Sdk 的相關資訊，您可以使用 toobuild 這兩個應用程式 toorun 裝置和您的方案後端上。
> 
> 

toocomplete 本教學課程中，您需要遵循的 hello:

* Node.js 0.10.x 版或更新版本。
* 使用中的 Azure 帳戶。 (如果您沒有帳戶，只需要幾分鐘的時間就可以建立[免費帳戶][lnk-free-trial]。)

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

您現在已經建立 IoT 中樞。 您有 hello IoT 中樞的主機名稱與 hello 您需要 toocomplete hello rest 本教學課程的 IoT 中樞連接字串。

## <a name="create-a-device-identity"></a>建立裝置識別
在本節中，您可以建立 IoT 中樞中的 hello 身分識別登錄中建立裝置身分識別的 Node.js 主控台應用程式。 如果其中有傳送 hello 身分識別登錄中的裝置只能連接 tooIoT 中樞。 如需詳細資訊，請參閱 hello**身分識別登錄**區段 hello [IoT 中樞開發人員指南][lnk-devguide-identity]。 當您執行此主控台應用程式時，它會產生唯一的裝置識別碼，並傳送至雲端的裝置時，您的裝置，可以使用 tooidentify 本身的索引鍵郵件 tooIoT 中樞。

1. 建立稱為 **createdeviceidentity**的新的空資料夾。 在 hello **createdeviceidentity**資料夾中，建立使用下列命令，在您的命令提示字元的 hello package.json 檔案。 接受所有的 hello 預設值：
   
    ```
    npm init
    ```
2. 在您的命令提示字元中 hello **createdeviceidentity**資料夾中，執行下列命令 tooinstall hello hello **azure iot 中樞**服務 SDK 封裝：
   
    ```
    npm install azure-iothub --save
    ```
3. 使用文字編輯器中，建立**CreateDeviceIdentity.js**檔案在 hello **createdeviceidentity**資料夾。
4. 新增下列 hello `require` hello 的 hello 開頭的陳述式**CreateDeviceIdentity.js**檔案：
   
    ```
    'use strict';
   
    var iothub = require('azure-iothub');
    ```
5. 新增下列程式碼 toohello hello **CreateDeviceIdentity.js**檔案，然後以 hello hello 中樞 hello 前一節中您建立 IoT 中樞連接字串取代 hello 預留位置的值： 
   
    ```
    var connectionString = '{iothub connection string}';
   
    var registry = iothub.Registry.fromConnectionString(connectionString);
    ```
6. 新增下列程式碼 toocreate IoT 中樞中的 hello 身分識別登錄中的裝置定義 hello。 此程式碼會建立裝置如果 hello 裝置識別碼不存在於 hello 身分識別登錄，否則它會傳回 hello 現有裝置 hello 索引鍵：
   
    ```
    var device = {
      deviceId: 'myFirstNodeDevice'
    }
    registry.create(device, function(err, deviceInfo, res) {
      if (err) {
        registry.get(device.deviceId, printDeviceInfo);
      }
      if (deviceInfo) {
        printDeviceInfo(err, deviceInfo, res)
      }
    });
   
    function printDeviceInfo(err, deviceInfo, res) {
      if (deviceInfo) {
        console.log('Device ID: ' + deviceInfo.deviceId);
        console.log('Device key: ' + deviceInfo.authentication.symmetricKey.primaryKey);
      }
    }
    ```
   [!INCLUDE [iot-hub-pii-note-naming-device](../../includes/iot-hub-pii-note-naming-device.md)]

7. 儲存並關閉 **CreateDeviceIdentity.js** 檔案。
8. toorun hello **createdeviceidentity**應用程式中，執行下列命令在 hello hello createdeviceidentity 資料夾中的命令提示字元的 hello:
   
    ```
    node CreateDeviceIdentity.js 
    ```
9. 請記下 hello**裝置識別碼**和**裝置金鑰**。 您需要這些值稍後當您建立連線 tooIoT 中樞為裝置的應用程式。

> [!NOTE]
> hello IoT 中樞身分識別登錄只會儲存裝置身分識別 tooenable 安全存取 toohello IoT 中樞。 它會儲存裝置識別碼和金鑰 toouse 安全性認證以及啟用/停用旗標，您可以使用 toodisable 存取個別的裝置。 如果您的應用程式需要 toostore 其他裝置專屬的中繼資料，它應該使用特定應用程式存放區。 如需詳細資訊，請參閱 hello [IoT 中樞開發人員指南][lnk-devguide-identity]。
> 
> 

<a id="D2C_node"></a>
## <a name="receive-device-to-cloud-messages"></a>接收裝置到雲端的訊息
在本節中，您會建立 Node.js 主控台應用程式，以讀取來自 IoT 中樞的裝置到雲端訊息。 IoT 中樞公開[事件中心][lnk-event-hubs-overview]-相容的端點 tooenable 您 tooread 裝置到雲端訊息。 簡單 tookeep 方面，本教學課程會建立基本的讀取器不是適用於高輸送量部署。 hello[處理裝置到雲端訊息][ lnk-process-d2c-tutorial]教學課程會示範大規模 tooprocess 裝置到雲端訊息的方式。 hello[開始使用事件中心][ lnk-eventhubs-tutorial]教學課程提供有關 tooprocess 如何從事件中心訊息和是適用的 toohello IoT 中樞事件中樞相容的端點的進一步資訊。

> [!NOTE]
> hello 一律讀取裝置到雲端訊息的事件中樞相容端點使用 hello AMQP 通訊協定。
> 
> 

1. 建立稱為 **readdevicetocloudmessages** 的空資料夾。 在 hello **readdevicetocloudmessages**資料夾中，建立使用下列命令，在您的命令提示字元的 hello package.json 檔案。 接受所有的 hello 預設值：
   
    ```
    npm init
    ```
2. 在您的命令提示字元中 hello **readdevicetocloudmessages**資料夾中，執行下列命令 tooinstall hello hello **azure 事件中心**封裝：
   
    ```
    npm install azure-event-hubs --save
    ```
3. 使用文字編輯器中，建立**ReadDeviceToCloudMessages.js**檔案在 hello **readdevicetocloudmessages**資料夾。
4. 新增下列 hello`require`陳述式在 hello 開頭 hello **ReadDeviceToCloudMessages.js**檔案：
   
    ```
    'use strict';
   
    var EventHubClient = require('azure-event-hubs').Client;
    ```
5. 加入下列變數宣告 hello 和 hello 預留位置值取代為您的中樞的 IoT 中樞連接字串 hello:
   
    ```
    var connectionString = '{iothub connection string}';
    ```
6. 加入下列兩個函數，列印輸出 toohello 主控台 hello:
   
    ```
    var printError = function (err) {
      console.log(err.message);
    };
   
    var printMessage = function (message) {
      console.log('Message received: ');
      console.log(JSON.stringify(message.body));
      console.log('');
    };
    ```
7. 新增下列程式碼 toocreate hello hello **EventHubClient**，開啟 hello 連接 tooyour IoT 中樞，並建立每個資料分割的接收器。 建立接收者以便 hello 接收者只會讀取傳送的訊息 tooIoT 中樞之後 hello 接收者就可開始執行時，此應用程式會使用篩選器。 此篩選器是適用於測試環境，因此您會看到剛才 hello 目前的一組訊息。 在實際執行環境中，您的程式碼應該要確定在處理所有的 hello 訊息。 如需詳細資訊，請參閱 hello[如何 tooprocess IoT 中樞裝置到雲端訊息][ lnk-process-d2c-tutorial]教學課程：
   
    ```
    var client = EventHubClient.fromConnectionString(connectionString);
    client.open()
        .then(client.getPartitionIds.bind(client))
        .then(function (partitionIds) {
            return partitionIds.map(function (partitionId) {
                return client.createReceiver('$Default', partitionId, { 'startAfterTime' : Date.now()}).then(function(receiver) {
                    console.log('Created partition receiver: ' + partitionId)
                    receiver.on('errorReceived', printError);
                    receiver.on('message', printMessage);
                });
            });
        })
        .catch(printError);
    ```
8. 儲存並關閉 hello **ReadDeviceToCloudMessages.js**檔案。

## <a name="create-a-simulated-device-app"></a>建立模擬裝置應用程式
在本節中，您可以建立 Node.js 主控台應用程式，可以模擬傳送裝置到雲端訊息 tooan IoT 中樞的裝置。

1. 建立稱為 **simulateddevice**的空資料夾。 在 hello **simulateddevice**資料夾中，建立使用下列命令，在您的命令提示字元的 hello package.json 檔案。 接受所有的 hello 預設值：
   
    ```
    npm init
    ```
2. 在您的命令提示字元中 hello **simulateddevice**資料夾中，執行下列命令 tooinstall hello hello **azure iot 裝置**裝置 SDK 封裝和**azure-iot-裝置-mqtt**封裝：
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. 使用文字編輯器中，建立**SimulatedDevice.js**檔案在 hello **simulateddevice**資料夾。
4. 新增下列 hello`require`陳述式在 hello 開頭 hello **SimulatedDevice.js**檔案：
   
    ```
    'use strict';
   
    var clientFromConnectionString = require('azure-iot-device-mqtt').clientFromConnectionString;
    var Message = require('azure-iot-device').Message;
    ```
5. 新增**connectionString**變數，並使用它 toocreate**用戶端**執行個體。 取代**{youriothostname}** hello hello IoT 中樞名稱與您建立 hello*建立 IoT 中樞*> 一節。 取代**{yourdevicekey}** hello 裝置索引鍵值中 hello 產生*建立裝置身分識別*> 一節：
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId=myFirstNodeDevice;SharedAccessKey={yourdevicekey}';
   
    var client = clientFromConnectionString(connectionString);
    ```
6. 新增 hello hello 應用程式中的下列函式 toodisplay 輸出：
   
    ```
    function printResultFor(op) {
      return function printResult(err, res) {
        if (err) console.log(op + ' error: ' + err.toString());
        if (res) console.log(op + ' status: ' + res.constructor.name);
      };
    }
    ```
7. 建立回呼，並使用 hello**依**函式 toosend 訊息 tooyour IoT 中樞每秒：
   
    ```
    var connectCallback = function (err) {
      if (err) {
        console.log('Could not connect: ' + err);
      } else {
        console.log('Client connected');
   
        // Create a message and send it toohello IoT Hub every second
        setInterval(function(){
            var temperature = 20 + (Math.random() * 15);
            var humidity = 60 + (Math.random() * 20);            
            var data = JSON.stringify({ deviceId: 'myFirstNodeDevice', temperature: temperature, humidity: humidity });
            var message = new Message(data);
            message.properties.add('temperatureAlert', (temperature > 30) ? 'true' : 'false');
            console.log("Sending message: " + message.getData());
            client.sendEvent(message, printResultFor('send'));
        }, 1000);
      }
    };
    ```
8. 開啟 hello 連接 tooyour IoT 中樞，並開始傳送訊息：
   
    ```
    client.open(connectCallback);
    ```
9. 儲存並關閉 hello **SimulatedDevice.js**檔案。

> [!NOTE]
> 簡單 tookeep 方面，本教學課程未實作任何重試原則。 在實際執行程式碼，您應該實作重試原則 （例如指數型輪詢），做為建議 hello MSDN 文件中[暫時性錯誤處理][lnk-transient-faults]。
> 
> 

## <a name="run-hello-apps"></a>執行 hello 應用程式
現在您已經準備就緒 toorun hello 應用程式。

1. 在命令提示字元中 hello **readdevicetocloudmessages**資料夾中，執行下列命令 toobegin 監視您的 IoT 中樞的 hello:
   
    ```
    node ReadDeviceToCloudMessages.js 
    ```
   
    ![Node.js IoT 中樞服務應用程式 toomonitor 裝置到雲端訊息][7]
2. 在命令提示字元中 hello **simulateddevice**資料夾中，執行下列命令 toobegin 傳送遙測資料 tooyour IoT 中樞的 hello:
   
    ```
    node SimulatedDevice.js
    ```
   
    ![Node.js IoT 中樞裝置應用程式 toosend 裝置到雲端訊息][8]
3. hello**使用量**磚中 hello [Azure 入口網站][ lnk-portal]顯示 hello 訊息傳送 toohello IoT 中樞的數目：
   
    ![Azure 入口網站使用並排顯示的數目傳送的訊息 tooIoT 中樞][43]

## <a name="next-steps"></a>後續步驟
在本教學課程中，您在 hello Azure 入口網站中設定新的 IoT 中樞，並接著 hello IoT 中樞的身分識別登錄中建立裝置身分識別。 您已經使用此裝置身分識別 tooenable hello 模擬裝置的應用程式 toosend 裝置到雲端訊息 toohello IoT 中樞。 您也會建立會顯示 hello IoT 中樞收到 hello 訊息的應用程式。 

使用者入門 toocontinue tooexplore IoT 中樞與其他 IoT 案例，請參閱：

* [連接您的裝置][lnk-connect-device]
* [開始使用裝置管理][lnk-device-management]
* [開始使用 Azure IoT Edge][lnk-iot-edge]

toolearn 如何 tooextend 您 IoT 方案和程序裝置到雲端訊息在小數位數，請參閱 hello[處理裝置到雲端訊息][ lnk-process-d2c-tutorial]教學課程。
[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]


<!-- Images. -->
[7]: ./media/iot-hub-node-node-getstarted/runapp1.png
[8]: ./media/iot-hub-node-node-getstarted/runapp2.png
[43]: ./media/iot-hub-csharp-csharp-getstarted/usage.png

<!-- Links -->
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-eventhubs-tutorial]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-devguide-identity]: iot-hub-devguide-identity-registry.md
[lnk-event-hubs-overview]: ../event-hubs/event-hubs-overview.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
[lnk-process-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal]: https://portal.azure.com/

[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/
