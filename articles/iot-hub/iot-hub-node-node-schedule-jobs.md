---
title: "aaaSchedule 作業與 Azure IoT 中樞 （節點） |Microsoft 文件"
description: "如何 tooschedule Azure IoT 中樞工作 tooinvoke 上多個裝置的直接的方法。 您可以使用 hello Azure IoT Sdk for Node.js tooimplement hello 模擬裝置的應用程式和服務應用程式 toorun hello 作業。"
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: 2233356e-b005-4765-ae41-3a4872bda943
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/30/2016
ms.author: juanpere
ms.openlocfilehash: be293362447fbcddaa3433b66f208f22545fe0c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="schedule-and-broadcast-jobs-node"></a>排定及廣播作業 (Node)

[!INCLUDE [iot-hub-selector-schedule-jobs](../../includes/iot-hub-selector-schedule-jobs.md)]

Azure IoT 中樞是完全受管理的服務，可讓後端應用程式 toocreate 和追蹤作業的排程並更新數百萬個裝置。  作業可以用於 hello 下列動作：

* 更新所需屬性
* 更新標籤
* 叫用直接方法

就概念而言，作業會包裝其中一個動作，並追蹤 hello 根據一組裝置，裝置的兩個查詢所定義的執行進度。  例如後, 端應用程式可以使用作業 tooinvoke 重新開機方法上 10,000 部裝置，裝置的兩個查詢所指定，以及排程在未來的時間。  當這些裝置接收並執行 hello 重新開機方法，該應用程式可以再追蹤進度。

從下列文章深入了解這當中的每一項功能：

* 裝置的兩個與屬性：[開始使用裝置雙][ lnk-get-started-twin]和[教學課程： 如何 toouse 裝置 twin 屬性][lnk-twin-props]
* 直接方法：[IoT 中樞開發人員指南 - 直接方法][lnk-dev-methods]和[教學課程：直接方法][lnk-c2d-methods]

本教學課程說明如何：

* 建立模擬的裝置應用程式有直接的方法可讓**lockDoor** hello 方案後端可以呼叫它。
* 建立 Node.js 的主控台應用程式，該呼叫 hello **lockDoor**直接的方法中使用工作和更新的 hello hello 模擬的裝置應用程式所需使用 裝置工作的屬性。

在本教學課程的 hello 最後，您有兩個 Node.js 主控台應用程式：

**simDevice.js**，這與 hello 裝置身分識別連接 tooyour IoT 中樞，並接收**lockDoor**直接方法。

**scheduleJobService.js**，呼叫直接的方法在 hello 模擬的裝置的應用程式和更新 hello 裝置中兩個的使用作業所需的屬性。

toocomplete 本教學課程中，您需要遵循的 hello:

* Node.js 0.12.x 版或更新版本， <br/>  [準備開發環境][ lnk-dev-setup]描述如何 tooinstall Node.js 本教學課程中的 Windows 或 Linux。
* 使用中的 Azure 帳戶。 (如果您沒有帳戶，只需要幾分鐘的時間就可以建立[免費帳戶][lnk-free-trial]。)

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a>建立模擬裝置應用程式
在本節中，您建立 Node.js 主控台應用程式回應 tooa 直接方法呼叫 hello 雲端，觸發程序模擬的裝置重新開機，使用 hello 報告屬性 tooenable 裝置兩個查詢 tooidentify 裝置，當它們一次啟動。

1. 建立名為 **simDevice** 的新空白資料夾。  在 hello **simDevice**資料夾中，建立使用下列命令，在您的命令提示字元的 hello package.json 檔案。  接受所有的 hello 預設值：
   
    ```
    npm init
    ```
2. 在您的命令提示字元中 hello **simDevice**資料夾中，執行下列命令 tooinstall hello hello **azure iot 裝置**裝置 SDK 封裝和**azure iot 裝置-mqtt**封裝：
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. 使用文字編輯器中，建立新**simDevice.js**檔案在 hello **simDevice**資料夾。
4. 新增 hello 下列的 '需要' 陳述式在 hello 開頭的 hello **simDevice.js**檔案：
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
5. 新增**connectionString**變數，並使用它 toocreate**用戶端**執行個體。  
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId={yourdeviceid};SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```
6. 加入下列函式 toohandle hello hello **lockDoor**方法。
   
    ```
    var onLockDoor = function(request, response) {
   
        // Respond hello cloud app for hello direct method
        response.send(200, function(err) {
            if (!err) {
                console.error('An error occured when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.');
            }
        });
   
        console.log('Locking Door!');
    };
    ```
7. 新增下列程式碼的 hello tooregister hello 處理常式的 hello **lockDoor**方法。
   
    ```
    client.open(function(err) {
        if (err) {
            console.error('Could not connect tooIotHub client.');
        }  else {
            console.log('Client connected tooIoT Hub. Register handler for lockDoor direct method.');
            client.onDeviceMethod('lockDoor', onLockDoor);
        }
    });
    ```
8. 儲存並關閉 hello **simDevice.js**檔案。

> [!NOTE]
> 簡單 tookeep 方面，本教學課程未實作任何重試原則。 在實際執行程式碼，您應該實作重試原則 （例如指數型輪詢），做為建議 hello MSDN 文件中[暫時性錯誤處理][lnk-transient-faults]。
> 
> 

## <a name="schedule-jobs-for-calling-a-direct-method-and-updating-a-device-twins-properties"></a>排定用於呼叫直接方法及更新裝置對應項 (twin) 屬性的作業
在本節中，您建立 Node.js 主控台應用程式起始遠端**lockDoor**裝置上使用直接方法，並更新 hello 裝置兩個的屬性。

1. 建立名為 **scheduleJobService** 的新空白資料夾。  在 hello **scheduleJobService**資料夾中，建立使用下列命令，在您的命令提示字元的 hello package.json 檔案。  接受所有的 hello 預設值：
   
    ```
    npm init
    ```
2. 在您的命令提示字元中 hello **scheduleJobService**資料夾中，執行下列命令 tooinstall hello hello **azure iot 中樞**裝置 SDK 封裝和**azure-iot-裝置-mqtt**封裝：
   
    ```
    npm install azure-iothub uuid --save
    ```
3. 使用文字編輯器中，建立新**scheduleJobService.js**檔案在 hello **scheduleJobService**資料夾。
4. 新增 hello 下列的 '需要' 陳述式在 hello 開頭的 hello **dmpatterns_gscheduleJobServiceetstarted_service.js**檔案：
   
    ```
    'use strict';
   
    var uuid = require('uuid');
    var JobClient = require('azure-iothub').JobClient;
    ```
5. 新增 hello 下列變數宣告，並取代 hello 預留位置值：
   
    ```
    var connectionString = '{iothubconnectionstring}';
    var queryCondition = "deviceId IN ['myDeviceId']";
    var startTime = new Date();
    var maxExecutionTimeInSeconds =  3600;
    var jobClient = JobClient.fromConnectionString(connectionString);
    ```
6. 加入下列函式，將會使用的 toomonitor hello hello 工作執行的 hello:
   
    ```
    function monitorJob (jobId, callback) {
        var jobMonitorInterval = setInterval(function() {
            jobClient.getJob(jobId, function(err, result) {
            if (err) {
                console.error('Could not get job status: ' + err.message);
            } else {
                console.log('Job: ' + jobId + ' - status: ' + result.status);
                if (result.status === 'completed' || result.status === 'failed' || result.status === 'cancelled') {
                clearInterval(jobMonitorInterval);
                callback(null, result);
                }
            }
            });
        }, 5000);
    }
    ```
7. 加入下列程式碼呼叫 hello 裝置方法 tooschedule hello 作業 hello:
   
    ```
    var methodParams = {
        methodName: 'lockDoor',
        payload: null,
        responseTimeoutInSeconds: 15 // Timeout after 15 seconds if device is unable tooprocess method
    };
   
    var methodJobId = uuid.v4();
    console.log('scheduling Device Method job with id: ' + methodJobId);
    jobClient.scheduleDeviceMethod(methodJobId,
                                queryCondition,
                                methodParams,
                                startTime,
                                maxExecutionTimeInSeconds,
                                function(err) {
        if (err) {
            console.error('Could not schedule device method job: ' + err.message);
        } else {
            monitorJob(methodJobId, function(err, result) {
                if (err) {
                    console.error('Could not monitor device method job: ' + err.message);
                } else {
                    console.log(JSON.stringify(result, null, 2));
                }
            });
        }
    });
    ```
8. 加入下列程式碼 tooschedule hello 作業 tooupdate hello 裝置兩個 hello:
   
    ```
    var twinPatch = {
        etag: '*',
        desired: {
            building: '43',
            floor: 3
        }
    };
   
    var twinJobId = uuid.v4();
   
    console.log('scheduling Twin Update job with id: ' + twinJobId);
    jobClient.scheduleTwinUpdate(twinJobId,
                                queryCondition,
                                twinPatch,
                                startTime,
                                maxExecutionTimeInSeconds,
                                function(err) {
        if (err) {
            console.error('Could not schedule twin update job: ' + err.message);
        } else {
            monitorJob(twinJobId, function(err, result) {
                if (err) {
                    console.error('Could not monitor twin update job: ' + err.message);
                } else {
                    console.log(JSON.stringify(result, null, 2));
                }
            });
        }
    });
    ```
9. 儲存並關閉 hello **scheduleJobService.js**檔案。

## <a name="run-hello-applications"></a>執行 hello 應用程式
現在您已經準備就緒 toorun hello 應用程式。

1. 在 hello 命令提示字元中 hello **simDevice**資料夾中，執行下列命令 toobegin 接聽 hello 重新開機直接方法 hello。
   
    ```
    node simDevice.js
    ```
2. 在 hello 命令提示字元中 hello **scheduleJobService**資料夾中，執行下列命令 tootrigger hello 作業 toolock hello 門和更新 hello 兩個 hello
   
    ```
    node scheduleJobService.js
    ```
3. 您會看到 hello 裝置回應 toohello 直接方法 hello 主控台中。

## <a name="next-steps"></a>後續步驟
在此教學課程中，您可以使用作業 tooschedule 直接方法 tooa 裝置和 hello 更新的 hello 裝置兩個的屬性。

toocontinue 開始使用 IoT 中樞與裝置管理模式，例如遠端透過 hello 空中韌體更新，請參閱：

[教學課程： 如何 toodo 韌體更新][lnk-fwupdate]

請參閱 < 開始使用 IoT 中樞 toocontinue[開始使用 Azure IoT 邊緣][lnk-iot-edge]。

[lnk-get-started-twin]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-props]: iot-hub-node-node-twin-how-to-configure.md
[lnk-c2d-methods]: iot-hub-node-node-direct-methods.md
[lnk-dev-methods]: iot-hub-devguide-direct-methods.md
[lnk-fwupdate]: iot-hub-node-node-firmware-update.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
