---
title: "一部裝置使用 Node.js aaaConnect |Microsoft 文件"
description: "描述如何 tooconnect 裝置 toohello Azure IoT 套件預先設定的遠端使用 Node.js 撰寫的應用程式的監視解決方案。"
services: 
suite: iot-suite
documentationcenter: na
author: dominicbetts
manager: timlt
editor: 
ms.assetid: fc50a33f-9fb9-42d7-b1b8-eb5cff19335e
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: 80bf2b70f15f539bfce4f135d533c46dd2b3f5a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-device-toohello-remote-monitoring-preconfigured-solution-nodejs"></a>連接您的裝置 toohello 遠端監視預先設定的解決方案 (Node.js)
[!INCLUDE [iot-suite-selector-connecting](../../includes/iot-suite-selector-connecting.md)]

## <a name="create-a-nodejs-sample-solution"></a>建立 node.js 範例解決方案

請確定 Node.js 0.11.5 版或更新版本已經安裝在您的開發電腦上。 您可以執行`node --version`hello 命令列 toocheck hello 版本。

1. 在開發電腦上建立名為 **RemoteMonitoring** 的資料夾。 瀏覽 toothis 命令列環境中的資料夾。

1. 執行下列的 hello 命令 toodownload 並安裝需要 toocomplete hello 範例應用程式的 hello 封裝：

    ```
    npm init
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```

1. 在 hello **RemoteMonitoring**資料夾中，建立名為的檔案**remote_monitoring.js**。 在文字編輯器中開啟這個檔案。

1. 在 hello **remote_monitoring.js** file、 add hello 下列`require`陳述式：

    ```nodejs
    'use strict';

    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    var Client = require('azure-iot-device').Client;
    var ConnectionString = require('azure-iot-device').ConnectionString;
    var Message = require('azure-iot-device').Message;
    ```

1. 加入下列變數宣告之後 hello hello`require`陳述式。 取代 hello 預留位置值 [裝置識別碼] 和 [裝置機碼] 與您記下您的裝置 hello 遠端監視方案儀表板中的值。 使用從 hello 方案儀表板 tooreplace [iot 中樞名稱] 的 hello IoT 中樞的主機名稱。 例如，若您的 IoT 中樞主機名稱是 **contoso.azure-devices.net**，請使用 **contoso** 取代 [IoTHub Name]：

    ```nodejs
    var connectionString = 'HostName=[IoTHub Name].azure-devices.net;DeviceId=[Device Id];SharedAccessKey=[Device Key]';
    var deviceId = ConnectionString.parse(connectionString).DeviceId;
    ```

1. 加入下列變數 toodefine hello 某些基底的遙測資料：

    ```nodejs
    var temperature = 50;
    var humidity = 50;
    var externalTemperature = 55;
    ```

1. 新增下列 helper 函式 tooprint 作業結果的 hello:

    ```nodejs
    function printErrorFor(op) {
        return function printError(err) {
            if (err) console.log(op + ' error: ' + err.toString());
        };
    }
    ```

1. 新增下列 helper 函式 toouse toorandomize hello 遙測值的 hello:

    ```nodejs
    function generateRandomIncrement() {
        return ((Math.random() * 2) - 1);
    }
    ```

1. 新增下列定義 hello hello **DeviceInfo**物件 hello 裝置會在啟動時傳送：

    ```nodejs
    var deviceMetaData = {
        'ObjectType': 'DeviceInfo',
        'IsSimulatedDevice': 0,
        'Version': '1.0',
        'DeviceProperties': {
            'DeviceID': deviceId,
            'HubEnabledState': 1
        }
    };
    ```

1. 新增下列 hello hello 裝置兩個定義報告的值。 這個定義包含 hello hello 裝置支援的直接方法的描述：

    ```nodejs
    var reportedProperties = {
        "Device": {
            "DeviceState": "normal",
            "Location": {
                "Latitude": 47.642877,
                "Longitude": -122.125497
            }
        },
        "Config": {
            "TemperatureMeanValue": 56.7,
            "TelemetryInterval": 45
        },
        "System": {
            "Manufacturer": "Contoso Inc.",
            "FirmwareVersion": "2.22",
            "InstalledRAM": "8 MB",
            "ModelNumber": "DB-14",
            "Platform": "Plat 9.75",
            "Processor": "i3-9",
            "SerialNumber": "SER99"
        },
        "Location": {
            "Latitude": 47.642877,
            "Longitude": -122.125497
        },
        "SupportedMethods": {
            "Reboot": "Reboot hello device",
            "InitiateFirmwareUpdate--FwPackageURI-string": "Updates device Firmware. Use parameter FwPackageURI toospecifiy hello URI of hello firmware file"
        },
    }
    ```

1. 加入下列函式 toohandle hello hello**重新開機**直接方法呼叫：

    ```nodejs
    function onReboot(request, response) {
        // Implement actual logic here.
        console.log('Simulated reboot...');

        // Complete hello response
        response.send(200, "Rebooting device", function(err) {
            if(!!err) {
                console.error('An error occurred when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.' );
            }
        });
    }
    ```

1. 加入下列函式 toohandle hello hello **InitiateFirmwareUpdate**直接方法呼叫。 這個直接的方法會使用參數的 toospecify hello 位置 hello 韌體映像 toodownload，並起始以非同步方式 hello hello 裝置上的軔體更新：

    ```nodejs
    function onInitiateFirmwareUpdate(request, response) {
        console.log('Simulated firmware update initiated, using: ' + request.payload.FwPackageURI);

        // Complete hello response
        response.send(200, "Firmware update initiated", function(err) {
            if(!!err) {
                console.error('An error occurred when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.' );
            }
        });

        // Add logic here tooperform hello firmware update asynchronously
    }
    ```

1. 加入下列程式碼 toocreate 用戶端執行個體的 hello:

    ```nodejs
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```

1. 加入下列程式碼的 hello:

    * 開啟 hello 連接。
    * 傳送嗨**DeviceInfo**物件。
    * 設定所需屬性的處理常式。
    * 傳送報告屬性。
    * 註冊處理常式的 hello 直接的方法。
    * 開始傳送遙測。

    ```nodejs
    client.open(function (err) {
        if (err) {
            printErrorFor('open')(err);
        } else {
            console.log('Sending device metadata:\n' + JSON.stringify(deviceMetaData));
            client.sendEvent(new Message(JSON.stringify(deviceMetaData)), printErrorFor('send metadata'));

            // Create device twin
            client.getTwin(function(err, twin) {
                if (err) {
                    console.error('Could not get device twin');
                } else {
                    console.log('Device twin created');

                    twin.on('properties.desired', function(delta) {
                        console.log('Received new desired properties:');
                        console.log(JSON.stringify(delta));
                    });

                    // Send reported properties
                    twin.properties.reported.update(reportedProperties, function(err) {
                        if (err) throw err;
                        console.log('twin state reported');
                    });

                    // Register handlers for direct methods
                    client.onDeviceMethod('Reboot', onReboot);
                    client.onDeviceMethod('InitiateFirmwareUpdate', onInitiateFirmwareUpdate);
                }
            });

            // Start sending telemetry
            var sendInterval = setInterval(function () {
                temperature += generateRandomIncrement();
                externalTemperature += generateRandomIncrement();
                humidity += generateRandomIncrement();

                var data = JSON.stringify({
                    'DeviceID': deviceId,
                    'Temperature': temperature,
                    'Humidity': humidity,
                    'ExternalTemperature': externalTemperature
                });

                console.log('Sending device event data:\n' + data);
                client.sendEvent(new Message(data), printErrorFor('send event'));
            }, 5000);

            client.on('error', function (err) {
                printErrorFor('client')(err);
                if (sendInterval) clearInterval(sendInterval);
                client.close(printErrorFor('client.close'));
            });
        }
    });
    ```

1. 儲存 hello 變更 toohello **remote_monitoring.js**檔案。

1. 執行下列命令，在命令提示字元 toolaunch hello 範例應用程式的 hello:
   
    ```
    node remote_monitoring.js
    ```

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

[lnk-github-repo]: https://github.com/azure/azure-iot-sdk-node
[lnk-github-prepare]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md
