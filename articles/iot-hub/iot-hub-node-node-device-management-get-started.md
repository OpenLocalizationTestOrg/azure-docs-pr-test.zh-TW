---
title: "開始使用 Azure IoT 中樞裝置管理 (Node) | Microsoft Docs"
description: "如何使用 IoT 中樞裝置管理來起始遠端裝置重新開機。 您可以使用適用於 Node.js 的 Azure IoT SDK，實作模擬裝置應用程式 (包含直接方法) 和服務應用程式 (叫用直接方法)。"
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
ms.openlocfilehash: 332a3e62cb1ef75e2c6dd5562ee799465c401128
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-device-management-node"></a><span data-ttu-id="b10c1-104">開始使用裝置管理 (Node)</span><span class="sxs-lookup"><span data-stu-id="b10c1-104">Get started with device management (Node)</span></span>

[!INCLUDE [iot-hub-selector-dm-getstarted](../../includes/iot-hub-selector-dm-getstarted.md)]

<span data-ttu-id="b10c1-105">本教學課程說明如何：</span><span class="sxs-lookup"><span data-stu-id="b10c1-105">This tutorial shows you how to:</span></span>

* <span data-ttu-id="b10c1-106">使用 Azure 入口網站來建立 IoT 中樞，並且在 IoT 中樞建立裝置識別。</span><span class="sxs-lookup"><span data-stu-id="b10c1-106">Use the Azure portal to create an IoT Hub and create a device identity in your IoT hub.</span></span>
* <span data-ttu-id="b10c1-107">建立模擬裝置應用程式，其包含可將該裝置重新開機的直接方法。</span><span class="sxs-lookup"><span data-stu-id="b10c1-107">Create a simulated device app that contains a direct method that reboots that device.</span></span> <span data-ttu-id="b10c1-108">直接方法是從雲端叫用。</span><span class="sxs-lookup"><span data-stu-id="b10c1-108">Direct methods are invoked from the cloud.</span></span>
* <span data-ttu-id="b10c1-109">建立 Node.js 主控台應用程式，可透過您的 IoT 中樞在模擬的裝置應用程式中呼叫重新啟動直接方法。</span><span class="sxs-lookup"><span data-stu-id="b10c1-109">Create a Node.js console app that calls the reboot direct method in the simulated device app through your IoT hub.</span></span>

<span data-ttu-id="b10c1-110">在本教學課程結尾處，您會有兩個 Node.js 主控台應用程式：</span><span class="sxs-lookup"><span data-stu-id="b10c1-110">At the end of this tutorial, you have two Node.js console apps:</span></span>

<span data-ttu-id="b10c1-111">**dmpatterns_getstarted_device.js**，它會以先前建立的裝置識別連線到您的 IoT 中樞，接收重新啟動直接方法，模擬實體重新啟動，並報告上一次重新啟動的時間。</span><span class="sxs-lookup"><span data-stu-id="b10c1-111">**dmpatterns_getstarted_device.js**, which connects to your IoT hub with the device identity created earlier, receives a reboot direct method, simulates a physical reboot, and reports the time for the last reboot.</span></span>

<span data-ttu-id="b10c1-112">**dmpatterns_getstarted_service.js**，它會在模擬裝置應用程式上呼叫直接方法，顯示回應，並顯示更新的報告屬性。</span><span class="sxs-lookup"><span data-stu-id="b10c1-112">**dmpatterns_getstarted_service.js**, which calls a direct method in the simulated device app, displays the response, and displays the updated reported properties.</span></span>

<span data-ttu-id="b10c1-113">若要完成此教學課程，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="b10c1-113">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="b10c1-114">Node.js 0.12.x 版或更新版本，</span><span class="sxs-lookup"><span data-stu-id="b10c1-114">Node.js version 0.12.x or later,</span></span> <br/>  <span data-ttu-id="b10c1-115">[準備您的開發環境][lnk-dev-setup]說明如何在 Windows 或 Linux 上安裝本教學課程的 Node.js。</span><span class="sxs-lookup"><span data-stu-id="b10c1-115">[Prepare your development environment][lnk-dev-setup] describes how to install Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="b10c1-116">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="b10c1-116">An active Azure account.</span></span> <span data-ttu-id="b10c1-117">(如果您沒有帳戶，只需要幾分鐘的時間就可以建立[免費帳戶][lnk-free-trial]。)</span><span class="sxs-lookup"><span data-stu-id="b10c1-117">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="b10c1-118">建立模擬裝置應用程式</span><span class="sxs-lookup"><span data-stu-id="b10c1-118">Create a simulated device app</span></span>
<span data-ttu-id="b10c1-119">在本節中，您將：</span><span class="sxs-lookup"><span data-stu-id="b10c1-119">In this section, you will</span></span>

* <span data-ttu-id="b10c1-120">建立 Node.js 主控台應用程式，以回應雲端所呼叫的直接方法</span><span class="sxs-lookup"><span data-stu-id="b10c1-120">Create a Node.js console app that responds to a direct method called by the cloud</span></span>
* <span data-ttu-id="b10c1-121">觸發模擬裝置重新啟動</span><span class="sxs-lookup"><span data-stu-id="b10c1-121">Trigger a simulated device reboot</span></span>
* <span data-ttu-id="b10c1-122">使用報告屬性來啟用裝置對應項查詢，以識別裝置及其上次重新啟動時間</span><span class="sxs-lookup"><span data-stu-id="b10c1-122">Use the reported properties to enable device twin queries to identify devices and when they last rebooted</span></span>

1. <span data-ttu-id="b10c1-123">建立稱為 **manageddevice** 的空資料夾。</span><span class="sxs-lookup"><span data-stu-id="b10c1-123">Create an empty folder called **manageddevice**.</span></span>  <span data-ttu-id="b10c1-124">在 **manageddevice** 資料夾中，於命令提示字元使用下列命令建立 package.json 檔案。</span><span class="sxs-lookup"><span data-stu-id="b10c1-124">In the **manageddevice** folder, create a package.json file using the following command at your command prompt.</span></span>  <span data-ttu-id="b10c1-125">接受所有預設值：</span><span class="sxs-lookup"><span data-stu-id="b10c1-125">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="b10c1-126">在命令提示字元中，於 **manageddevice** 資料夾中執行下列命令來安裝 **azure-iot-device** 裝置 SDK 套件和 **azure-iot-device-mqtt** 套件：</span><span class="sxs-lookup"><span data-stu-id="b10c1-126">At your command prompt in the **manageddevice** folder, run the following command to install the **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="b10c1-127">使用文字編輯器，在 **manageddevice** 資料夾中建立 **dmpatterns_getstarted_device.js** 檔案。</span><span class="sxs-lookup"><span data-stu-id="b10c1-127">Using a text editor, create a **dmpatterns_getstarted_device.js** file in the **manageddevice** folder.</span></span>
4. <span data-ttu-id="b10c1-128">在 **dmpatterns_getstarted_device.js** 檔案開頭新增下列 'require' 陳述式：</span><span class="sxs-lookup"><span data-stu-id="b10c1-128">Add the following 'require' statements at the start of the **dmpatterns_getstarted_device.js** file:</span></span>
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
5. <span data-ttu-id="b10c1-129">新增 **connectionString** 變數，並用它來建立**用戶端**執行個體。</span><span class="sxs-lookup"><span data-stu-id="b10c1-129">Add a **connectionString** variable and use it to create a **Client** instance.</span></span>  <span data-ttu-id="b10c1-130">以您裝置的連接字串取代連接字串。</span><span class="sxs-lookup"><span data-stu-id="b10c1-130">Replace the connection string with your device connection string.</span></span>  
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId=myDeviceId;SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```
6. <span data-ttu-id="b10c1-131">新增下列函式以在裝置上實作直接方法</span><span class="sxs-lookup"><span data-stu-id="b10c1-131">Add the following function to implement the direct method on the device</span></span>
   
    ```
    var onReboot = function(request, response) {
   
        // Respond the cloud app for the direct method
        response.send(200, 'Reboot started', function(err) {
            if (!err) {
                console.error('An error occured when sending a method response:\n' + err.toString());
            } else {
                console.log('Response to method \'' + request.methodName + '\' sent successfully.');
            }
        });
   
        // Report the reboot before the physical restart
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
7. <span data-ttu-id="b10c1-132">開啟您 IoT 中樞的連線，並啟動直接方法接聽程式︰</span><span class="sxs-lookup"><span data-stu-id="b10c1-132">Open the connection to your IoT hub and start the direct method listener:</span></span>
   
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
8. <span data-ttu-id="b10c1-133">儲存並關閉 **dmpatterns_getstarted_device.js**檔案。</span><span class="sxs-lookup"><span data-stu-id="b10c1-133">Save and close the **dmpatterns_getstarted_device.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="b10c1-134">為了簡單起見，本教學課程不會實作任何重試原則。</span><span class="sxs-lookup"><span data-stu-id="b10c1-134">To keep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="b10c1-135">在實際程式碼中，您應該如 MSDN 文章[暫時性錯誤處理][lnk-transient-faults]所建議，實作重試原則 (例如指數型輪詢)。</span><span class="sxs-lookup"><span data-stu-id="b10c1-135">In production code, you should implement retry policies (such as an exponential backoff), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>

## <a name="trigger-a-remote-reboot-on-the-device-using-a-direct-method"></a><span data-ttu-id="b10c1-136">使用直接方法在裝置上觸發遠端重新啟動</span><span class="sxs-lookup"><span data-stu-id="b10c1-136">Trigger a remote reboot on the device using a direct method</span></span>
<span data-ttu-id="b10c1-137">在本節中，您會建立 Node.js 主控台應用程式，此應用程式會使用直接方法起始遠端重新開機。</span><span class="sxs-lookup"><span data-stu-id="b10c1-137">In this section, you create a Node.js console app that initiates a remote reboot on a device using a direct method.</span></span> <span data-ttu-id="b10c1-138">應用程式使用裝置對應項查詢來探索該裝置的上次重新開機時間。</span><span class="sxs-lookup"><span data-stu-id="b10c1-138">The app uses device twin queries to discover the last reboot time for that device.</span></span>

1. <span data-ttu-id="b10c1-139">建立名為 **triggerrebootondevice** 的空白資料夾。</span><span class="sxs-lookup"><span data-stu-id="b10c1-139">Create an empty folder called **triggerrebootondevice**.</span></span>  <span data-ttu-id="b10c1-140">在命令提示字元中，於 **triggerrebootondevice** 資料夾中使用下列命令來建立 package.json 檔案。</span><span class="sxs-lookup"><span data-stu-id="b10c1-140">In the **triggerrebootondevice** folder, create a package.json file using the following command at your command prompt.</span></span>  <span data-ttu-id="b10c1-141">接受所有預設值：</span><span class="sxs-lookup"><span data-stu-id="b10c1-141">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="b10c1-142">在 **triggerrebootondevice** 資料夾中，於命令提示字元執行下列命令以安裝 **azure-iothub** 裝置 SDK 套件以及 **azure-iot-device-mqtt** 套件：</span><span class="sxs-lookup"><span data-stu-id="b10c1-142">At your command prompt in the **triggerrebootondevice** folder, run the following command to install the **azure-iothub** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="b10c1-143">使用文字編輯器，在 **triggerrebootondevice** 資料夾中建立 **dmpatterns_getstarted_service.js** 檔案。</span><span class="sxs-lookup"><span data-stu-id="b10c1-143">Using a text editor, create a **dmpatterns_getstarted_service.js** file in the **triggerrebootondevice** folder.</span></span>
4. <span data-ttu-id="b10c1-144">在 **dmpatterns_getstarted_service.js** 檔案開頭新增下列 'require' 陳述式：</span><span class="sxs-lookup"><span data-stu-id="b10c1-144">Add the following 'require' statements at the start of the **dmpatterns_getstarted_service.js** file:</span></span>
   
    ```
    'use strict';
   
    var Registry = require('azure-iothub').Registry;
    var Client = require('azure-iothub').Client;
    ```
5. <span data-ttu-id="b10c1-145">新增下列變數宣告，並取代預留位置值︰</span><span class="sxs-lookup"><span data-stu-id="b10c1-145">Add the following variable declarations and replace the placeholder values:</span></span>
   
    ```
    var connectionString = '{iothubconnectionstring}';
    var registry = Registry.fromConnectionString(connectionString);
    var client = Client.fromConnectionString(connectionString);
    var deviceToReboot = 'myDeviceId';
    ```
6. <span data-ttu-id="b10c1-146">新增下列函式來叫用裝置方法，以重新啟動目標裝置︰</span><span class="sxs-lookup"><span data-stu-id="b10c1-146">Add the following function to invoke the device method to reboot the target device:</span></span>
   
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
                console.log("Successfully invoked the device to reboot.");  
            }
        });
    };
    ```
7. <span data-ttu-id="b10c1-147">新增下列函式來查詢裝置並取得上次重新啟動時間︰</span><span class="sxs-lookup"><span data-stu-id="b10c1-147">Add the following function to query for the device and get the last reboot time:</span></span>
   
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
                console.log('Waiting for device to report last reboot time.');
        });
    };
    ```
8. <span data-ttu-id="b10c1-148">新增下列函式來呼叫可觸發重新啟動直接方法，並查詢上次重新啟動時間的函式︰</span><span class="sxs-lookup"><span data-stu-id="b10c1-148">Add the following code to call the functions that trigger the reboot direct method and query for the last reboot time:</span></span>
   
    ```
    startRebootDevice();
    setInterval(queryTwinLastReboot, 2000);
    ```
9. <span data-ttu-id="b10c1-149">儲存並關閉 **dmpatterns_getstarted_service.js** 檔案。</span><span class="sxs-lookup"><span data-stu-id="b10c1-149">Save and close the **dmpatterns_getstarted_service.js** file.</span></span>

## <a name="run-the-apps"></a><span data-ttu-id="b10c1-150">執行應用程式</span><span class="sxs-lookup"><span data-stu-id="b10c1-150">Run the apps</span></span>
<span data-ttu-id="b10c1-151">您現在可以開始執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="b10c1-151">You are now ready to run the apps.</span></span>

1. <span data-ttu-id="b10c1-152">在 **manageddevice** 資料夾中，於命令提示字元中執行下列命令以開始接聽重新啟動直接方法。</span><span class="sxs-lookup"><span data-stu-id="b10c1-152">At the command prompt in the **manageddevice** folder, run the following command to begin listening for the reboot direct method.</span></span>
   
    ```
    node dmpatterns_getstarted_device.js
    ```
2. <span data-ttu-id="b10c1-153">在命令提示字元中，於 **triggerrebootondevice** 資料夾執行下列命令以觸發裝置對應項的遠端重新啟動，以及查詢裝置對應項來尋找上次重新啟動時間。</span><span class="sxs-lookup"><span data-stu-id="b10c1-153">At the command prompt in the **triggerrebootondevice** folder, run the following command to trigger the remote reboot and query for the device twin to find the last reboot time.</span></span>
   
    ```
    node dmpatterns_getstarted_service.js
    ```
3. <span data-ttu-id="b10c1-154">您會在主控台中看到直接方法的裝置回應。</span><span class="sxs-lookup"><span data-stu-id="b10c1-154">You see the device response to the direct method in the console.</span></span>

[!INCLUDE [iot-hub-dm-followup](../../includes/iot-hub-dm-followup.md)]

<!-- images and links -->
[img-output]: media/iot-hub-get-started-with-dm/image6.png
[img-dm-ui]: media/iot-hub-get-started-with-dm/dmui.png

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md

[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[Azure portal]: https://portal.azure.com/
[Using resource groups to manage your Azure resources]: ../azure-portal/resource-group-portal.md
[lnk-dm-github]: https://github.com/Azure/azure-iot-device-management

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
