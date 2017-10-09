---
title: "aaaGet 開始使用 Azure IoT 中心裝置管理 （節點） |Microsoft 文件"
description: "如何 toouse IoT 中心裝置管理 tooinitiate 遠端裝置重新開機。 您可以使用 hello Azure IoT SDK for Node.js tooimplement 模擬的裝置應用程式，其中包含直接的方法與 hello 直接的方法會叫用的服務應用程式。"
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: e044006d-ffd6-469b-bc63-c182ad066e31
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: juanpere
ms.openlocfilehash: 5dd1878e71231850fb95f4170b823f1e86c3ee83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-management-node"></a><span data-ttu-id="e30e9-104">開始使用裝置管理 (Node)</span><span class="sxs-lookup"><span data-stu-id="e30e9-104">Get started with device management (Node)</span></span>

[!INCLUDE [iot-hub-selector-dm-getstarted](../../includes/iot-hub-selector-dm-getstarted.md)]

<span data-ttu-id="e30e9-105">本教學課程說明如何：</span><span class="sxs-lookup"><span data-stu-id="e30e9-105">This tutorial shows you how to:</span></span>

* <span data-ttu-id="e30e9-106">使用 hello Azure 入口網站 toocreate IoT 中樞，並在您的 IoT 中樞中建立裝置身分識別。</span><span class="sxs-lookup"><span data-stu-id="e30e9-106">Use hello Azure portal toocreate an IoT Hub and create a device identity in your IoT hub.</span></span>
* <span data-ttu-id="e30e9-107">建立模擬裝置應用程式，其包含可將該裝置重新開機的直接方法。</span><span class="sxs-lookup"><span data-stu-id="e30e9-107">Create a simulated device app that contains a direct method that reboots that device.</span></span> <span data-ttu-id="e30e9-108">直接的方法會叫用從 hello 雲端。</span><span class="sxs-lookup"><span data-stu-id="e30e9-108">Direct methods are invoked from hello cloud.</span></span>
* <span data-ttu-id="e30e9-109">建立 Node.js 主控台應用程式透過您的 IoT 中樞 hello 模擬的裝置應用程式中呼叫 hello 重新開機直接的方法。</span><span class="sxs-lookup"><span data-stu-id="e30e9-109">Create a Node.js console app that calls hello reboot direct method in hello simulated device app through your IoT hub.</span></span>

<span data-ttu-id="e30e9-110">在本教學課程的 hello 最後，您有兩個 Node.js 主控台應用程式：</span><span class="sxs-lookup"><span data-stu-id="e30e9-110">At hello end of this tutorial, you have two Node.js console apps:</span></span>

<span data-ttu-id="e30e9-111">**dmpatterns_getstarted_device.js**，稍早建立的 hello 裝置身分識別與連線 tooyour IoT 中樞收到重新開機直接的方法，會模擬實際的重新開機，並報告 hello hello 上次重新開機的時間。</span><span class="sxs-lookup"><span data-stu-id="e30e9-111">**dmpatterns_getstarted_device.js**, which connects tooyour IoT hub with hello device identity created earlier, receives a reboot direct method, simulates a physical reboot, and reports hello time for hello last reboot.</span></span>

<span data-ttu-id="e30e9-112">**dmpatterns_getstarted_service.js**、 直接的方法呼叫 hello 模擬的裝置，應用程式中顯示 hello 回應，並顯示 hello 更新報告內容。</span><span class="sxs-lookup"><span data-stu-id="e30e9-112">**dmpatterns_getstarted_service.js**, which calls a direct method in hello simulated device app, displays hello response, and displays hello updated reported properties.</span></span>

<span data-ttu-id="e30e9-113">toocomplete 本教學課程中，您需要遵循的 hello:</span><span class="sxs-lookup"><span data-stu-id="e30e9-113">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="e30e9-114">Node.js 0.12.x 版或更新版本，</span><span class="sxs-lookup"><span data-stu-id="e30e9-114">Node.js version 0.12.x or later,</span></span> <br/>  <span data-ttu-id="e30e9-115">[準備開發環境][ lnk-dev-setup]描述如何 tooinstall Node.js 本教學課程中的 Windows 或 Linux。</span><span class="sxs-lookup"><span data-stu-id="e30e9-115">[Prepare your development environment][lnk-dev-setup] describes how tooinstall Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="e30e9-116">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="e30e9-116">An active Azure account.</span></span> <span data-ttu-id="e30e9-117">(如果您沒有帳戶，只需要幾分鐘的時間就可以建立[免費帳戶][lnk-free-trial]。)</span><span class="sxs-lookup"><span data-stu-id="e30e9-117">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="e30e9-118">建立模擬裝置應用程式</span><span class="sxs-lookup"><span data-stu-id="e30e9-118">Create a simulated device app</span></span>
<span data-ttu-id="e30e9-119">在本節中，您將：</span><span class="sxs-lookup"><span data-stu-id="e30e9-119">In this section, you will</span></span>

* <span data-ttu-id="e30e9-120">建立回應 tooa 直接方法呼叫 hello 雲端 Node.js 主控台應用程式</span><span class="sxs-lookup"><span data-stu-id="e30e9-120">Create a Node.js console app that responds tooa direct method called by hello cloud</span></span>
* <span data-ttu-id="e30e9-121">觸發模擬裝置重新啟動</span><span class="sxs-lookup"><span data-stu-id="e30e9-121">Trigger a simulated device reboot</span></span>
* <span data-ttu-id="e30e9-122">使用 hello 報告屬性 tooenable 裝置兩個查詢 tooidentify 裝置，當它們一次啟動</span><span class="sxs-lookup"><span data-stu-id="e30e9-122">Use hello reported properties tooenable device twin queries tooidentify devices and when they last rebooted</span></span>

1. <span data-ttu-id="e30e9-123">建立稱為 **manageddevice** 的空資料夾。</span><span class="sxs-lookup"><span data-stu-id="e30e9-123">Create an empty folder called **manageddevice**.</span></span>  <span data-ttu-id="e30e9-124">在 hello **manageddevice**資料夾中，建立使用下列命令，在您的命令提示字元的 hello package.json 檔案。</span><span class="sxs-lookup"><span data-stu-id="e30e9-124">In hello **manageddevice** folder, create a package.json file using hello following command at your command prompt.</span></span>  <span data-ttu-id="e30e9-125">接受所有的 hello 預設值：</span><span class="sxs-lookup"><span data-stu-id="e30e9-125">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="e30e9-126">在您的命令提示字元中 hello **manageddevice**資料夾中，執行下列命令 tooinstall hello hello **azure iot 裝置**裝置 SDK 封裝和**azure-iot-裝置-mqtt**封裝：</span><span class="sxs-lookup"><span data-stu-id="e30e9-126">At your command prompt in hello **manageddevice** folder, run hello following command tooinstall hello **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="e30e9-127">使用文字編輯器中，建立**dmpatterns_getstarted_device.js**檔案在 hello **manageddevice**資料夾。</span><span class="sxs-lookup"><span data-stu-id="e30e9-127">Using a text editor, create a **dmpatterns_getstarted_device.js** file in hello **manageddevice** folder.</span></span>
4. <span data-ttu-id="e30e9-128">新增 hello 下列的 '需要' 陳述式在 hello 開頭的 hello **dmpatterns_getstarted_device.js**檔案：</span><span class="sxs-lookup"><span data-stu-id="e30e9-128">Add hello following 'require' statements at hello start of hello **dmpatterns_getstarted_device.js** file:</span></span>
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
5. <span data-ttu-id="e30e9-129">新增**connectionString**變數，並使用它 toocreate**用戶端**執行個體。</span><span class="sxs-lookup"><span data-stu-id="e30e9-129">Add a **connectionString** variable and use it toocreate a **Client** instance.</span></span>  <span data-ttu-id="e30e9-130">Hello 連接字串取代為您的裝置連接字串。</span><span class="sxs-lookup"><span data-stu-id="e30e9-130">Replace hello connection string with your device connection string.</span></span>  
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId=myDeviceId;SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```
6. <span data-ttu-id="e30e9-131">新增 hello 遵循 hello 裝置上的函式 tooimplement hello 直接方法</span><span class="sxs-lookup"><span data-stu-id="e30e9-131">Add hello following function tooimplement hello direct method on hello device</span></span>
   
    ```
    var onReboot = function(request, response) {
   
        // Respond hello cloud app for hello direct method
        response.send(200, 'Reboot started', function(err) {
            if (!err) {
                console.error('An error occured when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.');
            }
        });
   
        // Report hello reboot before hello physical restart
        var date = new Date();
        var patch = {
            iothubDM : {
                reboot : {
                    lastReboot : date.toISOString(),
                }
            }
        };
   
        // Get device Twin
        client.getTwin(function(err, twin) {
            if (err) {
                console.error('could not get twin');
            } else {
                console.log('twin acquired');
                twin.properties.reported.update(patch, function(err) {
                    if (err) throw err;
                    console.log('Device reboot twin state reported')
                });  
            }
        });
   
        // Add your device's reboot API for physical restart.
        console.log('Rebooting!');
    };
    ```
7. <span data-ttu-id="e30e9-132">開啟 hello 連接 tooyour IoT 中樞，並啟動 hello 直接方法接聽程式：</span><span class="sxs-lookup"><span data-stu-id="e30e9-132">Open hello connection tooyour IoT hub and start hello direct method listener:</span></span>
   
    ```
    client.open(function(err) {
        if (err) {
            console.error('Could not open IotHub client');
        }  else {
            console.log('Client opened.  Waiting for reboot method.');
            client.onDeviceMethod('reboot', onReboot);
        }
    });
    ```
8. <span data-ttu-id="e30e9-133">儲存並關閉 hello **dmpatterns_getstarted_device.js**檔案。</span><span class="sxs-lookup"><span data-stu-id="e30e9-133">Save and close hello **dmpatterns_getstarted_device.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="e30e9-134">簡單 tookeep 方面，本教學課程未實作任何重試原則。</span><span class="sxs-lookup"><span data-stu-id="e30e9-134">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="e30e9-135">在實際執行程式碼，您應該實作重試原則 （例如指數型輪詢），做為建議 hello MSDN 文件中[暫時性錯誤處理][lnk-transient-faults]。</span><span class="sxs-lookup"><span data-stu-id="e30e9-135">In production code, you should implement retry policies (such as an exponential backoff), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>

## <a name="trigger-a-remote-reboot-on-hello-device-using-a-direct-method"></a><span data-ttu-id="e30e9-136">觸發程序使用直接的方法 hello 裝置上遠端重新開機</span><span class="sxs-lookup"><span data-stu-id="e30e9-136">Trigger a remote reboot on hello device using a direct method</span></span>
<span data-ttu-id="e30e9-137">在本節中，您會建立 Node.js 主控台應用程式，此應用程式會使用直接方法起始遠端重新開機。</span><span class="sxs-lookup"><span data-stu-id="e30e9-137">In this section, you create a Node.js console app that initiates a remote reboot on a device using a direct method.</span></span> <span data-ttu-id="e30e9-138">hello 應用程式中使用該裝置的裝置兩個查詢 toodiscover hello 上次重新開機。</span><span class="sxs-lookup"><span data-stu-id="e30e9-138">hello app uses device twin queries toodiscover hello last reboot time for that device.</span></span>

1. <span data-ttu-id="e30e9-139">建立名為 **triggerrebootondevice** 的空白資料夾。</span><span class="sxs-lookup"><span data-stu-id="e30e9-139">Create an empty folder called **triggerrebootondevice**.</span></span>  <span data-ttu-id="e30e9-140">在 hello **triggerrebootondevice**資料夾中，建立使用下列命令，在您的命令提示字元的 hello package.json 檔案。</span><span class="sxs-lookup"><span data-stu-id="e30e9-140">In hello **triggerrebootondevice** folder, create a package.json file using hello following command at your command prompt.</span></span>  <span data-ttu-id="e30e9-141">接受所有的 hello 預設值：</span><span class="sxs-lookup"><span data-stu-id="e30e9-141">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="e30e9-142">在您的命令提示字元中 hello **triggerrebootondevice**資料夾中，執行下列命令 tooinstall hello hello **azure iot 中樞**裝置 SDK 封裝和**azure-iot-裝置-mqtt**封裝：</span><span class="sxs-lookup"><span data-stu-id="e30e9-142">At your command prompt in hello **triggerrebootondevice** folder, run hello following command tooinstall hello **azure-iothub** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="e30e9-143">使用文字編輯器中，建立**dmpatterns_getstarted_service.js**檔案在 hello **triggerrebootondevice**資料夾。</span><span class="sxs-lookup"><span data-stu-id="e30e9-143">Using a text editor, create a **dmpatterns_getstarted_service.js** file in hello **triggerrebootondevice** folder.</span></span>
4. <span data-ttu-id="e30e9-144">新增 hello 下列的 '需要' 陳述式在 hello 開頭的 hello **dmpatterns_getstarted_service.js**檔案：</span><span class="sxs-lookup"><span data-stu-id="e30e9-144">Add hello following 'require' statements at hello start of hello **dmpatterns_getstarted_service.js** file:</span></span>
   
    ```
    'use strict';
   
    var Registry = require('azure-iothub').Registry;
    var Client = require('azure-iothub').Client;
    ```
5. <span data-ttu-id="e30e9-145">新增 hello 下列變數宣告，並取代 hello 預留位置值：</span><span class="sxs-lookup"><span data-stu-id="e30e9-145">Add hello following variable declarations and replace hello placeholder values:</span></span>
   
    ```
    var connectionString = '{iothubconnectionstring}';
    var registry = Registry.fromConnectionString(connectionString);
    var client = Client.fromConnectionString(connectionString);
    var deviceToReboot = 'myDeviceId';
    ```
6. <span data-ttu-id="e30e9-146">加入下列函式 tooinvoke hello 方法 tooreboot hello 目標裝置 hello:</span><span class="sxs-lookup"><span data-stu-id="e30e9-146">Add hello following function tooinvoke hello device method tooreboot hello target device:</span></span>
   
    ```
    var startRebootDevice = function(twin) {
   
        var methodName = "reboot";
   
        var methodParams = {
            methodName: methodName,
            payload: null,
            timeoutInSeconds: 30
        };
   
        client.invokeDeviceMethod(deviceToReboot, methodParams, function(err, result) {
            if (err) { 
                console.error("Direct method error: "+err.message);
            } else {
                console.log("Successfully invoked hello device tooreboot.");  
            }
        });
    };
    ```
7. <span data-ttu-id="e30e9-147">加入下列 hello 函式 tooquery hello 裝置，並取得 hello 上次重新開機：</span><span class="sxs-lookup"><span data-stu-id="e30e9-147">Add hello following function tooquery for hello device and get hello last reboot time:</span></span>
   
    ```
    var queryTwinLastReboot = function() {
   
        registry.getTwin(deviceToReboot, function(err, twin){
   
            if (twin.properties.reported.iothubDM != null)
            {
                if (err) {
                    console.error('Could not query twins: ' + err.constructor.name + ': ' + err.message);
                } else {
                    var lastRebootTime = twin.properties.reported.iothubDM.reboot.lastReboot;
                    console.log('Last reboot time: ' + JSON.stringify(lastRebootTime, null, 2));
                }
            } else 
                console.log('Waiting for device tooreport last reboot time.');
        });
    };
    ```
8. <span data-ttu-id="e30e9-148">加入下列程式碼 toocall hello 函式會觸發 hello hello 重新開機直接的方法和查詢 hello 上次重新啟動時間：</span><span class="sxs-lookup"><span data-stu-id="e30e9-148">Add hello following code toocall hello functions that trigger hello reboot direct method and query for hello last reboot time:</span></span>
   
    ```
    startRebootDevice();
    setInterval(queryTwinLastReboot, 2000);
    ```
9. <span data-ttu-id="e30e9-149">儲存並關閉 hello **dmpatterns_getstarted_service.js**檔案。</span><span class="sxs-lookup"><span data-stu-id="e30e9-149">Save and close hello **dmpatterns_getstarted_service.js** file.</span></span>

## <a name="run-hello-apps"></a><span data-ttu-id="e30e9-150">執行 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="e30e9-150">Run hello apps</span></span>
<span data-ttu-id="e30e9-151">現在您已經準備就緒 toorun hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e30e9-151">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="e30e9-152">在 hello 命令提示字元中 hello **manageddevice**資料夾中，執行下列命令 toobegin 接聽 hello 重新開機直接方法 hello。</span><span class="sxs-lookup"><span data-stu-id="e30e9-152">At hello command prompt in hello **manageddevice** folder, run hello following command toobegin listening for hello reboot direct method.</span></span>
   
    ```
    node dmpatterns_getstarted_device.js
    ```
2. <span data-ttu-id="e30e9-153">在 hello 命令提示字元中 hello **triggerrebootondevice**資料夾中，執行下列命令 tootrigger hello 遠端 hello 重新開機，查詢 hello 裝置兩個 toofind hello 上次重新啟動時間。</span><span class="sxs-lookup"><span data-stu-id="e30e9-153">At hello command prompt in hello **triggerrebootondevice** folder, run hello following command tootrigger hello remote reboot and query for hello device twin toofind hello last reboot time.</span></span>
   
    ```
    node dmpatterns_getstarted_service.js
    ```
3. <span data-ttu-id="e30e9-154">您會看到 hello 裝置回應 toohello 直接方法 hello 主控台中。</span><span class="sxs-lookup"><span data-stu-id="e30e9-154">You see hello device response toohello direct method in hello console.</span></span>

[!INCLUDE [iot-hub-dm-followup](../../includes/iot-hub-dm-followup.md)]

<!-- images and links -->
[img-output]: media/iot-hub-get-started-with-dm/image6.png
[img-dm-ui]: media/iot-hub-get-started-with-dm/dmui.png

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md

[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[Azure portal]: https://portal.azure.com/
[Using resource groups toomanage your Azure resources]: ../azure-portal/resource-group-portal.md
[lnk-dm-github]: https://github.com/Azure/azure-iot-device-management

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
