---
title: "aaaDevice 韌體更新與 Azure IoT 中樞 （節點） |Microsoft 文件"
description: "如何在 Azure IoT 中樞 tooinitiate 裝置韌體 toouse 裝置管理更新。 使用 hello Azure IoT Sdk for Node.js tooimplement 模擬的裝置應用程式和服務應用程式觸發 hello 軔體更新。"
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: 70b84258-bc9f-43b1-b7cf-de1bb715f2cf
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/06/2017
ms.author: juanpere
ms.openlocfilehash: 99d4b369e7aba334bf713e0c657e6e5d227fb691
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-device-management-tooinitiate-a-device-firmware-update-nodenode"></a>使用裝置管理 tooinitiate 裝置韌體更新 （節點/節點）
[!INCLUDE [iot-hub-selector-firmware-update](../../includes/iot-hub-selector-firmware-update.md)]

## <a name="introduction"></a>簡介
在 hello[開始使用 裝置管理][ lnk-dm-getstarted]教學課程中，您已看到如何 toouse hello[裝置兩個][ lnk-devtwin]和[直接方法][ lnk-c2dmethod]基本型別 tooremotely 裝置重新開機。 這個教學課程使用 hello 相同 IoT 中樞基本類型和提供指引，並示範如何 toodo 端對端模擬軔體更新。  此模式用於 hello Intel Edison 裝置範例 hello 韌體更新的實作。

本教學課程說明如何：

* 建立 hello firmwareUpdate 直接方法呼叫中 hello 模擬的裝置的應用程式透過您的 IoT 中樞 Node.js 主控台應用程式。
* 建立會實作 **firmwareUpdate** 直接方法的模擬裝置應用程式。 這個方法會起始多階段程序，等候 toodownload hello 的韌體映像，下載 hello 的韌體映像，並在最後套用 hello 的韌體映像。 在每個階段 hello 更新中，hello 裝置使用 hello 報告屬性 tooreport 進度。

在本教學課程的 hello 最後，您有兩個 Node.js 主控台應用程式：

**dmpatterns_fwupdate_service.js**、 直接的方法呼叫 hello 模擬的裝置，應用程式中顯示 hello 回應，並定期 (每個的 500ms) 顯示 hello 更新報告內容。

**dmpatterns_fwupdate_device.js**，稍早建立的 hello 裝置身分識別與連線 tooyour IoT 中樞收到 firmwareUpdate 直接的方法時，會透過執行多重狀態的處理序 toosimulate 韌體更新，包括： 等候 hello下載 hello 新映像，並最後套用 hello 映像下載映像。

toocomplete 本教學課程中，您需要遵循的 hello:

* Node.js 0.12.x 版或更新版本， <br/>  [準備開發環境][ lnk-dev-setup]描述如何 tooinstall Node.js 本教學課程中的 Windows 或 Linux。
* 使用中的 Azure 帳戶。 (如果您沒有帳戶，只需要幾分鐘的時間就可以建立[免費帳戶][lnk-free-trial]。)

請遵循 hello[開始使用 裝置管理](iot-hub-node-node-device-management-get-started.md)文章 toocreate IoT 中樞，並取得您的 IoT 中樞連接字串。

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-firmware-update-on-hello-device-using-a-direct-method"></a>觸發遠端韌體更新 hello 裝置上使用直接的方法
在此節中，您會建立 Node.js 主控台應用程式，此應用程式會在裝置上起始遠端韌體更新。 hello 應用程式使用直接的方法 tooinitiate hello 更新，並使用裝置兩個查詢 tooperiodically 取得 hello hello 作用中的韌體更新狀態。

1. 建立稱為 **triggerfwupdateondevice** 的空資料夾。  在 hello **triggerfwupdateondevice**資料夾中，建立使用下列命令，在您的命令提示字元的 hello package.json 檔案。  接受所有的 hello 預設值：
   
    ```
    npm init
    ```
2. 在您的命令提示字元中 hello **triggerfwupdateondevice**資料夾中，執行下列命令 tooinstall hello hello **azure iot 中樞**和**azure iot 裝置-mqtt**裝置SDK 封裝：
   
    ```
    npm install azure-iothub --save
    ```
3. 使用文字編輯器中，建立**dmpatterns_getstarted_service.js**檔案在 hello **triggerfwupdateondevice**資料夾。
4. 新增 hello 下列的 '需要' 陳述式在 hello 開頭的 hello **dmpatterns_getstarted_service.js**檔案：
   
    ```
    'use strict';
   
    var Registry = require('azure-iothub').Registry;
    var Client = require('azure-iothub').Client;
    ```
5. 新增 hello 下列變數宣告，並取代 hello 預留位置值：
   
    ```
    var connectionString = '{device_connectionstring}';
    var registry = Registry.fromConnectionString(connectionString);
    var client = Client.fromConnectionString(connectionString);
    var deviceToUpdate = 'myDeviceId';
    ```
6. 新增下列 hello toofind 函式，並顯示 hello firmwareUpdate hello 值報告的屬性。
   
    ```
    var queryTwinFWUpdateReported = function() {
        registry.getTwin(deviceToUpdate, function(err, twin){
            if (err) {
              console.error('Could not query twins: ' + err.constructor.name + ': ' + err.message);
            } else {
              console.log((JSON.stringify(twin.properties.reported.iothubDM.firmwareUpdate)) + "\n");
            }
        });
    };
    ```
7. 加入下列函式 tooinvoke hello firmwareUpdate 方法 tooreboot hello 目標裝置 hello:
   
    ```
    var startFirmwareUpdateDevice = function() {
      var params = {
          fwPackageUri: 'https://secureurl'
      };
   
      var methodName = "firmwareUpdate";
      var payloadData =  JSON.stringify(params);
   
      var methodParams = {
        methodName: methodName,
        payload: payloadData,
        timeoutInSeconds: 30
      };
   
      client.invokeDeviceMethod(deviceToUpdate, methodParams, function(err, result) {
        if (err) {
          console.error('Could not start hello firmware update on hello device: ' + err.message)
        } 
      });
    };
    ```
8. 最後，新增 hello 下列函式 toocode toostart hello 韌體更新序列，並定期顯示 hello 報告屬性：
   
    ```
    startFirmwareUpdateDevice();
    setInterval(queryTwinFWUpdateReported, 500);
    ```
9. 儲存並關閉 hello **dmpatterns_fwupdate_service.js**檔案。

[!INCLUDE [iot-hub-device-firmware-update](../../includes/iot-hub-device-firmware-update.md)]

## <a name="run-hello-apps"></a>執行 hello 應用程式
現在您已經準備就緒 toorun hello 應用程式。

1. 在 hello 命令提示字元中 hello **manageddevice**資料夾中，執行下列命令 toobegin 接聽 hello 重新開機直接方法 hello。
   
    ```
    node dmpatterns_fwupdate_device.js
    ```
2. 在 hello 命令提示字元中 hello **triggerfwupdateondevice**資料夾中，執行下列命令 tootrigger hello 遠端 hello 重新開機，查詢 hello 裝置兩個 toofind hello 上次重新啟動時間。
   
    ```
    node dmpatterns_fwupdate_service.js
    ```
3. 您會看到 hello 裝置回應 toohello 直接方法 hello 主控台中。

## <a name="next-steps"></a>後續步驟
在本教學課程中，您可以使用直接的方法 tootrigger 遠端裝置和使用的 hello 上的軔體更新報告 hello 韌體更新屬性 toofollow hello 進度。

toolearn 如何 tooextend IoT 解決方案和排程方法呼叫上多個裝置，請參閱 hello[排程和廣播的工作][ lnk-tutorial-jobs]教學課程。

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-dm-getstarted]: iot-hub-node-node-device-management-get-started.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
