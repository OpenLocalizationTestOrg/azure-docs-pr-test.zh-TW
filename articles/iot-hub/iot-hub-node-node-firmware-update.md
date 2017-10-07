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
# <a name="use-device-management-tooinitiate-a-device-firmware-update-nodenode"></a><span data-ttu-id="6ade4-104">使用裝置管理 tooinitiate 裝置韌體更新 （節點/節點）</span><span class="sxs-lookup"><span data-stu-id="6ade4-104">Use device management tooinitiate a device firmware update (Node/Node)</span></span>
[!INCLUDE [iot-hub-selector-firmware-update](../../includes/iot-hub-selector-firmware-update.md)]

## <a name="introduction"></a><span data-ttu-id="6ade4-105">簡介</span><span class="sxs-lookup"><span data-stu-id="6ade4-105">Introduction</span></span>
<span data-ttu-id="6ade4-106">在 hello[開始使用 裝置管理][ lnk-dm-getstarted]教學課程中，您已看到如何 toouse hello[裝置兩個][ lnk-devtwin]和[直接方法][ lnk-c2dmethod]基本型別 tooremotely 裝置重新開機。</span><span class="sxs-lookup"><span data-stu-id="6ade4-106">In hello [Get started with device management][lnk-dm-getstarted] tutorial, you saw how toouse hello [device twin][lnk-devtwin] and [direct methods][lnk-c2dmethod] primitives tooremotely reboot a device.</span></span> <span data-ttu-id="6ade4-107">這個教學課程使用 hello 相同 IoT 中樞基本類型和提供指引，並示範如何 toodo 端對端模擬軔體更新。</span><span class="sxs-lookup"><span data-stu-id="6ade4-107">This tutorial uses hello same IoT Hub primitives and provides guidance and shows you how toodo an end-to-end simulated firmware update.</span></span>  <span data-ttu-id="6ade4-108">此模式用於 hello Intel Edison 裝置範例 hello 韌體更新的實作。</span><span class="sxs-lookup"><span data-stu-id="6ade4-108">This pattern is used in hello firmware update implementation for hello Intel Edison device sample.</span></span>

<span data-ttu-id="6ade4-109">本教學課程說明如何：</span><span class="sxs-lookup"><span data-stu-id="6ade4-109">This tutorial shows you how to:</span></span>

* <span data-ttu-id="6ade4-110">建立 hello firmwareUpdate 直接方法呼叫中 hello 模擬的裝置的應用程式透過您的 IoT 中樞 Node.js 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="6ade4-110">Create a Node.js console app that calls hello firmwareUpdate direct method in hello simulated device app through your IoT hub.</span></span>
* <span data-ttu-id="6ade4-111">建立會實作 **firmwareUpdate** 直接方法的模擬裝置應用程式。</span><span class="sxs-lookup"><span data-stu-id="6ade4-111">Create a simulated device app that implements a **firmwareUpdate** direct method.</span></span> <span data-ttu-id="6ade4-112">這個方法會起始多階段程序，等候 toodownload hello 的韌體映像，下載 hello 的韌體映像，並在最後套用 hello 的韌體映像。</span><span class="sxs-lookup"><span data-stu-id="6ade4-112">This method initiates a multi-stage process that waits toodownload hello firmware image, downloads hello firmware image, and finally applies hello firmware image.</span></span> <span data-ttu-id="6ade4-113">在每個階段 hello 更新中，hello 裝置使用 hello 報告屬性 tooreport 進度。</span><span class="sxs-lookup"><span data-stu-id="6ade4-113">During each stage of hello update, hello device uses hello reported properties tooreport on progress.</span></span>

<span data-ttu-id="6ade4-114">在本教學課程的 hello 最後，您有兩個 Node.js 主控台應用程式：</span><span class="sxs-lookup"><span data-stu-id="6ade4-114">At hello end of this tutorial, you have two Node.js console apps:</span></span>

<span data-ttu-id="6ade4-115">**dmpatterns_fwupdate_service.js**、 直接的方法呼叫 hello 模擬的裝置，應用程式中顯示 hello 回應，並定期 (每個的 500ms) 顯示 hello 更新報告內容。</span><span class="sxs-lookup"><span data-stu-id="6ade4-115">**dmpatterns_fwupdate_service.js**, which calls a direct method in hello simulated device app, displays hello response, and periodically (every 500ms) displays hello updated reported properties.</span></span>

<span data-ttu-id="6ade4-116">**dmpatterns_fwupdate_device.js**，稍早建立的 hello 裝置身分識別與連線 tooyour IoT 中樞收到 firmwareUpdate 直接的方法時，會透過執行多重狀態的處理序 toosimulate 韌體更新，包括： 等候 hello下載 hello 新映像，並最後套用 hello 映像下載映像。</span><span class="sxs-lookup"><span data-stu-id="6ade4-116">**dmpatterns_fwupdate_device.js**, which connects tooyour IoT hub with hello device identity created earlier, receives a firmwareUpdate direct method, runs through a multi-state process toosimulate a firmware update including: waiting for hello image download, downloading hello new image, and finally applying hello image.</span></span>

<span data-ttu-id="6ade4-117">toocomplete 本教學課程中，您需要遵循的 hello:</span><span class="sxs-lookup"><span data-stu-id="6ade4-117">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="6ade4-118">Node.js 0.12.x 版或更新版本，</span><span class="sxs-lookup"><span data-stu-id="6ade4-118">Node.js version 0.12.x or later,</span></span> <br/>  <span data-ttu-id="6ade4-119">[準備開發環境][ lnk-dev-setup]描述如何 tooinstall Node.js 本教學課程中的 Windows 或 Linux。</span><span class="sxs-lookup"><span data-stu-id="6ade4-119">[Prepare your development environment][lnk-dev-setup] describes how tooinstall Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="6ade4-120">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="6ade4-120">An active Azure account.</span></span> <span data-ttu-id="6ade4-121">(如果您沒有帳戶，只需要幾分鐘的時間就可以建立[免費帳戶][lnk-free-trial]。)</span><span class="sxs-lookup"><span data-stu-id="6ade4-121">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

<span data-ttu-id="6ade4-122">請遵循 hello[開始使用 裝置管理](iot-hub-node-node-device-management-get-started.md)文章 toocreate IoT 中樞，並取得您的 IoT 中樞連接字串。</span><span class="sxs-lookup"><span data-stu-id="6ade4-122">Follow hello [Get started with device management](iot-hub-node-node-device-management-get-started.md) article toocreate your IoT hub and get your IoT Hub connection string.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-firmware-update-on-hello-device-using-a-direct-method"></a><span data-ttu-id="6ade4-123">觸發遠端韌體更新 hello 裝置上使用直接的方法</span><span class="sxs-lookup"><span data-stu-id="6ade4-123">Trigger a remote firmware update on hello device using a direct method</span></span>
<span data-ttu-id="6ade4-124">在此節中，您會建立 Node.js 主控台應用程式，此應用程式會在裝置上起始遠端韌體更新。</span><span class="sxs-lookup"><span data-stu-id="6ade4-124">In this section, you create a Node.js console app that initiates a remote firmware update on a device.</span></span> <span data-ttu-id="6ade4-125">hello 應用程式使用直接的方法 tooinitiate hello 更新，並使用裝置兩個查詢 tooperiodically 取得 hello hello 作用中的韌體更新狀態。</span><span class="sxs-lookup"><span data-stu-id="6ade4-125">hello app uses a direct method tooinitiate hello update and uses device twin queries tooperiodically get hello status of hello active firmware update.</span></span>

1. <span data-ttu-id="6ade4-126">建立稱為 **triggerfwupdateondevice** 的空資料夾。</span><span class="sxs-lookup"><span data-stu-id="6ade4-126">Create an empty folder called **triggerfwupdateondevice**.</span></span>  <span data-ttu-id="6ade4-127">在 hello **triggerfwupdateondevice**資料夾中，建立使用下列命令，在您的命令提示字元的 hello package.json 檔案。</span><span class="sxs-lookup"><span data-stu-id="6ade4-127">In hello **triggerfwupdateondevice** folder, create a package.json file using hello following command at your command prompt.</span></span>  <span data-ttu-id="6ade4-128">接受所有的 hello 預設值：</span><span class="sxs-lookup"><span data-stu-id="6ade4-128">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="6ade4-129">在您的命令提示字元中 hello **triggerfwupdateondevice**資料夾中，執行下列命令 tooinstall hello hello **azure iot 中樞**和**azure iot 裝置-mqtt**裝置SDK 封裝：</span><span class="sxs-lookup"><span data-stu-id="6ade4-129">At your command prompt in hello **triggerfwupdateondevice** folder, run hello following command tooinstall hello **azure-iot-hub** and **azure-iot-device-mqtt** Device SDK packages:</span></span>
   
    ```
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="6ade4-130">使用文字編輯器中，建立**dmpatterns_getstarted_service.js**檔案在 hello **triggerfwupdateondevice**資料夾。</span><span class="sxs-lookup"><span data-stu-id="6ade4-130">Using a text editor, create a **dmpatterns_getstarted_service.js** file in hello **triggerfwupdateondevice** folder.</span></span>
4. <span data-ttu-id="6ade4-131">新增 hello 下列的 '需要' 陳述式在 hello 開頭的 hello **dmpatterns_getstarted_service.js**檔案：</span><span class="sxs-lookup"><span data-stu-id="6ade4-131">Add hello following 'require' statements at hello start of hello **dmpatterns_getstarted_service.js** file:</span></span>
   
    ```
    'use strict';
   
    var Registry = require('azure-iothub').Registry;
    var Client = require('azure-iothub').Client;
    ```
5. <span data-ttu-id="6ade4-132">新增 hello 下列變數宣告，並取代 hello 預留位置值：</span><span class="sxs-lookup"><span data-stu-id="6ade4-132">Add hello following variable declarations and replace hello placeholder values:</span></span>
   
    ```
    var connectionString = '{device_connectionstring}';
    var registry = Registry.fromConnectionString(connectionString);
    var client = Client.fromConnectionString(connectionString);
    var deviceToUpdate = 'myDeviceId';
    ```
6. <span data-ttu-id="6ade4-133">新增下列 hello toofind 函式，並顯示 hello firmwareUpdate hello 值報告的屬性。</span><span class="sxs-lookup"><span data-stu-id="6ade4-133">Add hello following function toofind and display hello value of hello firmwareUpdate reported property.</span></span>
   
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
7. <span data-ttu-id="6ade4-134">加入下列函式 tooinvoke hello firmwareUpdate 方法 tooreboot hello 目標裝置 hello:</span><span class="sxs-lookup"><span data-stu-id="6ade4-134">Add hello following function tooinvoke hello firmwareUpdate method tooreboot hello target device:</span></span>
   
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
8. <span data-ttu-id="6ade4-135">最後，新增 hello 下列函式 toocode toostart hello 韌體更新序列，並定期顯示 hello 報告屬性：</span><span class="sxs-lookup"><span data-stu-id="6ade4-135">Finally, Add hello following function toocode toostart hello firmware update sequence and start periodically showing hello reported properties:</span></span>
   
    ```
    startFirmwareUpdateDevice();
    setInterval(queryTwinFWUpdateReported, 500);
    ```
9. <span data-ttu-id="6ade4-136">儲存並關閉 hello **dmpatterns_fwupdate_service.js**檔案。</span><span class="sxs-lookup"><span data-stu-id="6ade4-136">Save and close hello **dmpatterns_fwupdate_service.js** file.</span></span>

[!INCLUDE [iot-hub-device-firmware-update](../../includes/iot-hub-device-firmware-update.md)]

## <a name="run-hello-apps"></a><span data-ttu-id="6ade4-137">執行 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="6ade4-137">Run hello apps</span></span>
<span data-ttu-id="6ade4-138">現在您已經準備就緒 toorun hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6ade4-138">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="6ade4-139">在 hello 命令提示字元中 hello **manageddevice**資料夾中，執行下列命令 toobegin 接聽 hello 重新開機直接方法 hello。</span><span class="sxs-lookup"><span data-stu-id="6ade4-139">At hello command prompt in hello **manageddevice** folder, run hello following command toobegin listening for hello reboot direct method.</span></span>
   
    ```
    node dmpatterns_fwupdate_device.js
    ```
2. <span data-ttu-id="6ade4-140">在 hello 命令提示字元中 hello **triggerfwupdateondevice**資料夾中，執行下列命令 tootrigger hello 遠端 hello 重新開機，查詢 hello 裝置兩個 toofind hello 上次重新啟動時間。</span><span class="sxs-lookup"><span data-stu-id="6ade4-140">At hello command prompt in hello **triggerfwupdateondevice** folder, run hello following command tootrigger hello remote reboot and query for hello device twin toofind hello last reboot time.</span></span>
   
    ```
    node dmpatterns_fwupdate_service.js
    ```
3. <span data-ttu-id="6ade4-141">您會看到 hello 裝置回應 toohello 直接方法 hello 主控台中。</span><span class="sxs-lookup"><span data-stu-id="6ade4-141">You see hello device response toohello direct method in hello console.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6ade4-142">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6ade4-142">Next steps</span></span>
<span data-ttu-id="6ade4-143">在本教學課程中，您可以使用直接的方法 tootrigger 遠端裝置和使用的 hello 上的軔體更新報告 hello 韌體更新屬性 toofollow hello 進度。</span><span class="sxs-lookup"><span data-stu-id="6ade4-143">In this tutorial, you used a direct method tootrigger a remote firmware update on a device and used hello reported properties toofollow hello progress of hello firmware update.</span></span>

<span data-ttu-id="6ade4-144">toolearn 如何 tooextend IoT 解決方案和排程方法呼叫上多個裝置，請參閱 hello[排程和廣播的工作][ lnk-tutorial-jobs]教學課程。</span><span class="sxs-lookup"><span data-stu-id="6ade4-144">toolearn how tooextend your IoT solution and schedule method calls on multiple devices, see hello [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-dm-getstarted]: iot-hub-node-node-device-management-get-started.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
