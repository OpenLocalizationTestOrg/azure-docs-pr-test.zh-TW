---
title: "使用 Node.js 連接裝置 |Microsoft Docs"
description: "描述如何使用 Node.js 中已寫入的應用程式，將裝置連接至 Azure IoT Suite 預先設定遠端監視方案。"
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
ms.openlocfilehash: 6459b6196eb7f4a083b67e5a421bcc0d51d39e5c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="connect-your-device-to-the-remote-monitoring-preconfigured-solution-nodejs"></a><span data-ttu-id="e94c3-103">將裝置連接至遠端監視預先設定方案 (Node.js)</span><span class="sxs-lookup"><span data-stu-id="e94c3-103">Connect your device to the remote monitoring preconfigured solution (Node.js)</span></span>
[!INCLUDE [iot-suite-selector-connecting](../../includes/iot-suite-selector-connecting.md)]

## <a name="create-a-nodejs-sample-solution"></a><span data-ttu-id="e94c3-104">建立 node.js 範例解決方案</span><span class="sxs-lookup"><span data-stu-id="e94c3-104">Create a node.js sample solution</span></span>

<span data-ttu-id="e94c3-105">請確定 Node.js 0.11.5 版或更新版本已經安裝在您的開發電腦上。</span><span class="sxs-lookup"><span data-stu-id="e94c3-105">Ensure that Node.js version 0.11.5 or later is installed on your development machine.</span></span> <span data-ttu-id="e94c3-106">您可以在命令列執行 `node --version` 來檢查版本。</span><span class="sxs-lookup"><span data-stu-id="e94c3-106">You can run `node --version` at the command line to check the version.</span></span>

1. <span data-ttu-id="e94c3-107">在開發電腦上建立名為 **RemoteMonitoring** 的資料夾。</span><span class="sxs-lookup"><span data-stu-id="e94c3-107">Create a folder called **RemoteMonitoring** on your development machine.</span></span> <span data-ttu-id="e94c3-108">在命令列環境中瀏覽至此資料夾。</span><span class="sxs-lookup"><span data-stu-id="e94c3-108">Navigate to this folder in your command-line environment.</span></span>

1. <span data-ttu-id="e94c3-109">執行下列命令，以下載並安裝完成範例應用程式所需的套件︰</span><span class="sxs-lookup"><span data-stu-id="e94c3-109">Run the following commands to download and install the packages you need to complete the sample app:</span></span>

    ```
    npm init
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```

1. <span data-ttu-id="e94c3-110">在 **RemoteMonitoring** 資料夾中，建立名為 **remote_monitoring.js** 的檔案。</span><span class="sxs-lookup"><span data-stu-id="e94c3-110">In the **RemoteMonitoring** folder, create a file called **remote_monitoring.js**.</span></span> <span data-ttu-id="e94c3-111">在文字編輯器中開啟這個檔案。</span><span class="sxs-lookup"><span data-stu-id="e94c3-111">Open this file in a text editor.</span></span>

1. <span data-ttu-id="e94c3-112">在 **remote_monitoring.js** 檔案中，新增下列 `require` 陳述式︰</span><span class="sxs-lookup"><span data-stu-id="e94c3-112">In the **remote_monitoring.js** file, add the following `require` statements:</span></span>

    ```nodejs
    'use strict';

    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    var Client = require('azure-iot-device').Client;
    var ConnectionString = require('azure-iot-device').ConnectionString;
    var Message = require('azure-iot-device').Message;
    ```

1. <span data-ttu-id="e94c3-113">在 `require` 陳述式之後新增下列變數宣告。</span><span class="sxs-lookup"><span data-stu-id="e94c3-113">Add the following variable declarations after the `require` statements.</span></span> <span data-ttu-id="e94c3-114">使用您在遠端監視解決方案儀表板中為裝置記下的值來取代 [Device Id] 和 [Device Key] 預留位置值。</span><span class="sxs-lookup"><span data-stu-id="e94c3-114">Replace the placeholder values [Device Id] and [Device Key] with values you noted for your device in the remote monitoring solution dashboard.</span></span> <span data-ttu-id="e94c3-115">使用解決方案儀表板中的「IoT 中樞主機名稱」來取代 [IoTHub Name]。</span><span class="sxs-lookup"><span data-stu-id="e94c3-115">Use the IoT Hub Hostname from the solution dashboard to replace [IoTHub Name].</span></span> <span data-ttu-id="e94c3-116">例如，若您的 IoT 中樞主機名稱是 **contoso.azure-devices.net**，請使用 **contoso** 取代 [IoTHub Name]：</span><span class="sxs-lookup"><span data-stu-id="e94c3-116">For example, if your IoT Hub Hostname is **contoso.azure-devices.net**, replace [IoTHub Name] with **contoso**:</span></span>

    ```nodejs
    var connectionString = 'HostName=[IoTHub Name].azure-devices.net;DeviceId=[Device Id];SharedAccessKey=[Device Key]';
    var deviceId = ConnectionString.parse(connectionString).DeviceId;
    ```

1. <span data-ttu-id="e94c3-117">新增下列變數來定義一些基本遙測資料︰</span><span class="sxs-lookup"><span data-stu-id="e94c3-117">Add the following variables to define some base telemetry data:</span></span>

    ```nodejs
    var temperature = 50;
    var humidity = 50;
    var externalTemperature = 55;
    ```

1. <span data-ttu-id="e94c3-118">新增下列協助程式來列印作業結果︰</span><span class="sxs-lookup"><span data-stu-id="e94c3-118">Add the following helper function to print operation results:</span></span>

    ```nodejs
    function printErrorFor(op) {
        return function printError(err) {
            if (err) console.log(op + ' error: ' + err.toString());
        };
    }
    ```

1. <span data-ttu-id="e94c3-119">新增下列協助程式函式，用來將排遙測值隨機化︰</span><span class="sxs-lookup"><span data-stu-id="e94c3-119">Add the following helper function to use to randomize the telemetry values:</span></span>

    ```nodejs
    function generateRandomIncrement() {
        return ((Math.random() * 2) - 1);
    }
    ```

1. <span data-ttu-id="e94c3-120">針對裝置在啟動時傳送的 **DeviceInfo** 物件，新增下列定義︰</span><span class="sxs-lookup"><span data-stu-id="e94c3-120">Add the following definition for the **DeviceInfo** object the device sends on startup:</span></span>

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

1. <span data-ttu-id="e94c3-121">針對裝置對應項報告值新增下列定義。</span><span class="sxs-lookup"><span data-stu-id="e94c3-121">Add the following definition for the device twin reported values.</span></span> <span data-ttu-id="e94c3-122">此定義包含裝置支援的直接方法說明︰</span><span class="sxs-lookup"><span data-stu-id="e94c3-122">This definition includes descriptions of the direct methods the device supports:</span></span>

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
            "Reboot": "Reboot the device",
            "InitiateFirmwareUpdate--FwPackageURI-string": "Updates device Firmware. Use parameter FwPackageURI to specifiy the URI of the firmware file"
        },
    }
    ```

1. <span data-ttu-id="e94c3-123">新增下列函式以處理 **Reboot** 直接方法呼叫：</span><span class="sxs-lookup"><span data-stu-id="e94c3-123">Add the following function to handle the **Reboot** direct method call:</span></span>

    ```nodejs
    function onReboot(request, response) {
        // Implement actual logic here.
        console.log('Simulated reboot...');

        // Complete the response
        response.send(200, "Rebooting device", function(err) {
            if(!!err) {
                console.error('An error occurred when sending a method response:\n' + err.toString());
            } else {
                console.log('Response to method \'' + request.methodName + '\' sent successfully.' );
            }
        });
    }
    ```

1. <span data-ttu-id="e94c3-124">新增下列函式以處理 **InitiateFirmwareUpdate** 直接方法呼叫。</span><span class="sxs-lookup"><span data-stu-id="e94c3-124">Add the following function to handle the **InitiateFirmwareUpdate** direct method call.</span></span> <span data-ttu-id="e94c3-125">此直接方法使用參數來指定要下載之韌體映像的位置，並以非同步方式在裝置上啟始韌體更新︰</span><span class="sxs-lookup"><span data-stu-id="e94c3-125">This direct method uses a parameter to specify the location of the firmware image to download, and initiates the firmware update on the device asynchronously:</span></span>

    ```nodejs
    function onInitiateFirmwareUpdate(request, response) {
        console.log('Simulated firmware update initiated, using: ' + request.payload.FwPackageURI);

        // Complete the response
        response.send(200, "Firmware update initiated", function(err) {
            if(!!err) {
                console.error('An error occurred when sending a method response:\n' + err.toString());
            } else {
                console.log('Response to method \'' + request.methodName + '\' sent successfully.' );
            }
        });

        // Add logic here to perform the firmware update asynchronously
    }
    ```

1. <span data-ttu-id="e94c3-126">新增下列程式碼，以建立用戶端執行個體︰</span><span class="sxs-lookup"><span data-stu-id="e94c3-126">Add the following code to create a client instance:</span></span>

    ```nodejs
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```

1. <span data-ttu-id="e94c3-127">新增下列程式碼，以便：</span><span class="sxs-lookup"><span data-stu-id="e94c3-127">Add the following code to:</span></span>

    * <span data-ttu-id="e94c3-128">開啟連線。</span><span class="sxs-lookup"><span data-stu-id="e94c3-128">Open the connection.</span></span>
    * <span data-ttu-id="e94c3-129">傳送 **DeviceInfo** 物件。</span><span class="sxs-lookup"><span data-stu-id="e94c3-129">Send the **DeviceInfo** object.</span></span>
    * <span data-ttu-id="e94c3-130">設定所需屬性的處理常式。</span><span class="sxs-lookup"><span data-stu-id="e94c3-130">Set up a handler for desired properties.</span></span>
    * <span data-ttu-id="e94c3-131">傳送報告屬性。</span><span class="sxs-lookup"><span data-stu-id="e94c3-131">Send reported properties.</span></span>
    * <span data-ttu-id="e94c3-132">登錄直接方法的處理常式。</span><span class="sxs-lookup"><span data-stu-id="e94c3-132">Register handlers for the direct methods.</span></span>
    * <span data-ttu-id="e94c3-133">開始傳送遙測。</span><span class="sxs-lookup"><span data-stu-id="e94c3-133">Start sending telemetry.</span></span>

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

1. <span data-ttu-id="e94c3-134">將變更儲存至 **remote_monitoring.js** 檔案。</span><span class="sxs-lookup"><span data-stu-id="e94c3-134">Save the changes to the **remote_monitoring.js** file.</span></span>

1. <span data-ttu-id="e94c3-135">在命令提示字元中執行下列命令，以啟動範例應用程式：</span><span class="sxs-lookup"><span data-stu-id="e94c3-135">Run the following command at a command prompt to launch the sample application:</span></span>
   
    ```
    node remote_monitoring.js
    ```

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

[lnk-github-repo]: https://github.com/azure/azure-iot-sdk-node
[lnk-github-prepare]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md
