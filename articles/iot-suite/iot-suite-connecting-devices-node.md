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
# <a name="connect-your-device-toohello-remote-monitoring-preconfigured-solution-nodejs"></a><span data-ttu-id="0446d-103">連接您的裝置 toohello 遠端監視預先設定的解決方案 (Node.js)</span><span class="sxs-lookup"><span data-stu-id="0446d-103">Connect your device toohello remote monitoring preconfigured solution (Node.js)</span></span>
[!INCLUDE [iot-suite-selector-connecting](../../includes/iot-suite-selector-connecting.md)]

## <a name="create-a-nodejs-sample-solution"></a><span data-ttu-id="0446d-104">建立 node.js 範例解決方案</span><span class="sxs-lookup"><span data-stu-id="0446d-104">Create a node.js sample solution</span></span>

<span data-ttu-id="0446d-105">請確定 Node.js 0.11.5 版或更新版本已經安裝在您的開發電腦上。</span><span class="sxs-lookup"><span data-stu-id="0446d-105">Ensure that Node.js version 0.11.5 or later is installed on your development machine.</span></span> <span data-ttu-id="0446d-106">您可以執行`node --version`hello 命令列 toocheck hello 版本。</span><span class="sxs-lookup"><span data-stu-id="0446d-106">You can run `node --version` at hello command line toocheck hello version.</span></span>

1. <span data-ttu-id="0446d-107">在開發電腦上建立名為 **RemoteMonitoring** 的資料夾。</span><span class="sxs-lookup"><span data-stu-id="0446d-107">Create a folder called **RemoteMonitoring** on your development machine.</span></span> <span data-ttu-id="0446d-108">瀏覽 toothis 命令列環境中的資料夾。</span><span class="sxs-lookup"><span data-stu-id="0446d-108">Navigate toothis folder in your command-line environment.</span></span>

1. <span data-ttu-id="0446d-109">執行下列的 hello 命令 toodownload 並安裝需要 toocomplete hello 範例應用程式的 hello 封裝：</span><span class="sxs-lookup"><span data-stu-id="0446d-109">Run hello following commands toodownload and install hello packages you need toocomplete hello sample app:</span></span>

    ```
    npm init
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```

1. <span data-ttu-id="0446d-110">在 hello **RemoteMonitoring**資料夾中，建立名為的檔案**remote_monitoring.js**。</span><span class="sxs-lookup"><span data-stu-id="0446d-110">In hello **RemoteMonitoring** folder, create a file called **remote_monitoring.js**.</span></span> <span data-ttu-id="0446d-111">在文字編輯器中開啟這個檔案。</span><span class="sxs-lookup"><span data-stu-id="0446d-111">Open this file in a text editor.</span></span>

1. <span data-ttu-id="0446d-112">在 hello **remote_monitoring.js** file、 add hello 下列`require`陳述式：</span><span class="sxs-lookup"><span data-stu-id="0446d-112">In hello **remote_monitoring.js** file, add hello following `require` statements:</span></span>

    ```nodejs
    'use strict';

    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    var Client = require('azure-iot-device').Client;
    var ConnectionString = require('azure-iot-device').ConnectionString;
    var Message = require('azure-iot-device').Message;
    ```

1. <span data-ttu-id="0446d-113">加入下列變數宣告之後 hello hello`require`陳述式。</span><span class="sxs-lookup"><span data-stu-id="0446d-113">Add hello following variable declarations after hello `require` statements.</span></span> <span data-ttu-id="0446d-114">取代 hello 預留位置值 [裝置識別碼] 和 [裝置機碼] 與您記下您的裝置 hello 遠端監視方案儀表板中的值。</span><span class="sxs-lookup"><span data-stu-id="0446d-114">Replace hello placeholder values [Device Id] and [Device Key] with values you noted for your device in hello remote monitoring solution dashboard.</span></span> <span data-ttu-id="0446d-115">使用從 hello 方案儀表板 tooreplace [iot 中樞名稱] 的 hello IoT 中樞的主機名稱。</span><span class="sxs-lookup"><span data-stu-id="0446d-115">Use hello IoT Hub Hostname from hello solution dashboard tooreplace [IoTHub Name].</span></span> <span data-ttu-id="0446d-116">例如，若您的 IoT 中樞主機名稱是 **contoso.azure-devices.net**，請使用 **contoso** 取代 [IoTHub Name]：</span><span class="sxs-lookup"><span data-stu-id="0446d-116">For example, if your IoT Hub Hostname is **contoso.azure-devices.net**, replace [IoTHub Name] with **contoso**:</span></span>

    ```nodejs
    var connectionString = 'HostName=[IoTHub Name].azure-devices.net;DeviceId=[Device Id];SharedAccessKey=[Device Key]';
    var deviceId = ConnectionString.parse(connectionString).DeviceId;
    ```

1. <span data-ttu-id="0446d-117">加入下列變數 toodefine hello 某些基底的遙測資料：</span><span class="sxs-lookup"><span data-stu-id="0446d-117">Add hello following variables toodefine some base telemetry data:</span></span>

    ```nodejs
    var temperature = 50;
    var humidity = 50;
    var externalTemperature = 55;
    ```

1. <span data-ttu-id="0446d-118">新增下列 helper 函式 tooprint 作業結果的 hello:</span><span class="sxs-lookup"><span data-stu-id="0446d-118">Add hello following helper function tooprint operation results:</span></span>

    ```nodejs
    function printErrorFor(op) {
        return function printError(err) {
            if (err) console.log(op + ' error: ' + err.toString());
        };
    }
    ```

1. <span data-ttu-id="0446d-119">新增下列 helper 函式 toouse toorandomize hello 遙測值的 hello:</span><span class="sxs-lookup"><span data-stu-id="0446d-119">Add hello following helper function toouse toorandomize hello telemetry values:</span></span>

    ```nodejs
    function generateRandomIncrement() {
        return ((Math.random() * 2) - 1);
    }
    ```

1. <span data-ttu-id="0446d-120">新增下列定義 hello hello **DeviceInfo**物件 hello 裝置會在啟動時傳送：</span><span class="sxs-lookup"><span data-stu-id="0446d-120">Add hello following definition for hello **DeviceInfo** object hello device sends on startup:</span></span>

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

1. <span data-ttu-id="0446d-121">新增下列 hello hello 裝置兩個定義報告的值。</span><span class="sxs-lookup"><span data-stu-id="0446d-121">Add hello following definition for hello device twin reported values.</span></span> <span data-ttu-id="0446d-122">這個定義包含 hello hello 裝置支援的直接方法的描述：</span><span class="sxs-lookup"><span data-stu-id="0446d-122">This definition includes descriptions of hello direct methods hello device supports:</span></span>

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

1. <span data-ttu-id="0446d-123">加入下列函式 toohandle hello hello**重新開機**直接方法呼叫：</span><span class="sxs-lookup"><span data-stu-id="0446d-123">Add hello following function toohandle hello **Reboot** direct method call:</span></span>

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

1. <span data-ttu-id="0446d-124">加入下列函式 toohandle hello hello **InitiateFirmwareUpdate**直接方法呼叫。</span><span class="sxs-lookup"><span data-stu-id="0446d-124">Add hello following function toohandle hello **InitiateFirmwareUpdate** direct method call.</span></span> <span data-ttu-id="0446d-125">這個直接的方法會使用參數的 toospecify hello 位置 hello 韌體映像 toodownload，並起始以非同步方式 hello hello 裝置上的軔體更新：</span><span class="sxs-lookup"><span data-stu-id="0446d-125">This direct method uses a parameter toospecify hello location of hello firmware image toodownload, and initiates hello firmware update on hello device asynchronously:</span></span>

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

1. <span data-ttu-id="0446d-126">加入下列程式碼 toocreate 用戶端執行個體的 hello:</span><span class="sxs-lookup"><span data-stu-id="0446d-126">Add hello following code toocreate a client instance:</span></span>

    ```nodejs
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```

1. <span data-ttu-id="0446d-127">加入下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="0446d-127">Add hello following code to:</span></span>

    * <span data-ttu-id="0446d-128">開啟 hello 連接。</span><span class="sxs-lookup"><span data-stu-id="0446d-128">Open hello connection.</span></span>
    * <span data-ttu-id="0446d-129">傳送嗨**DeviceInfo**物件。</span><span class="sxs-lookup"><span data-stu-id="0446d-129">Send hello **DeviceInfo** object.</span></span>
    * <span data-ttu-id="0446d-130">設定所需屬性的處理常式。</span><span class="sxs-lookup"><span data-stu-id="0446d-130">Set up a handler for desired properties.</span></span>
    * <span data-ttu-id="0446d-131">傳送報告屬性。</span><span class="sxs-lookup"><span data-stu-id="0446d-131">Send reported properties.</span></span>
    * <span data-ttu-id="0446d-132">註冊處理常式的 hello 直接的方法。</span><span class="sxs-lookup"><span data-stu-id="0446d-132">Register handlers for hello direct methods.</span></span>
    * <span data-ttu-id="0446d-133">開始傳送遙測。</span><span class="sxs-lookup"><span data-stu-id="0446d-133">Start sending telemetry.</span></span>

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

1. <span data-ttu-id="0446d-134">儲存 hello 變更 toohello **remote_monitoring.js**檔案。</span><span class="sxs-lookup"><span data-stu-id="0446d-134">Save hello changes toohello **remote_monitoring.js** file.</span></span>

1. <span data-ttu-id="0446d-135">執行下列命令，在命令提示字元 toolaunch hello 範例應用程式的 hello:</span><span class="sxs-lookup"><span data-stu-id="0446d-135">Run hello following command at a command prompt toolaunch hello sample application:</span></span>
   
    ```
    node remote_monitoring.js
    ```

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

[lnk-github-repo]: https://github.com/azure/azure-iot-sdk-node
[lnk-github-prepare]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md
