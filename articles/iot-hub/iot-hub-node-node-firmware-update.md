---
title: "使用 Azure IoT 中樞進行裝置韌體更新 | Microsoft Docs"
description: "如何使用 Azure IoT 中樞上的裝置管理來起始裝置韌體更新。 您可以使用適用於 Node.js 的 Azure IoT SDK，實作模擬裝置應用程式和服務應用程式，以觸發韌體更新。"
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
ms.openlocfilehash: 350cf1cbec8847d1bbf29814435502af6f098e54
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-device-management-to-initiate-a-device-firmware-update-nodenode"></a><span data-ttu-id="4054a-104">使用裝置管理來起始裝置韌體更新 (節點/節點)</span><span class="sxs-lookup"><span data-stu-id="4054a-104">Use device management to initiate a device firmware update (Node/Node)</span></span>
[!INCLUDE [iot-hub-selector-firmware-update](../../includes/iot-hub-selector-firmware-update.md)]

## <a name="introduction"></a><span data-ttu-id="4054a-105">簡介</span><span class="sxs-lookup"><span data-stu-id="4054a-105">Introduction</span></span>
<span data-ttu-id="4054a-106">在[開始使用裝置管理][lnk-dm-getstarted]教學課程中，您已了解如何使用[裝置對應項][lnk-devtwin]和[直接方案][lnk-c2dmethod]基礎，從遠端重新啟動裝置。</span><span class="sxs-lookup"><span data-stu-id="4054a-106">In the [Get started with device management][lnk-dm-getstarted] tutorial, you saw how to use the [device twin][lnk-devtwin] and [direct methods][lnk-c2dmethod] primitives to remotely reboot a device.</span></span> <span data-ttu-id="4054a-107">本教學課程會使用相同的 IoT 中樞基礎，並且提供指引和示範如何進行端對端模擬韌體更新。</span><span class="sxs-lookup"><span data-stu-id="4054a-107">This tutorial uses the same IoT Hub primitives and provides guidance and shows you how to do an end-to-end simulated firmware update.</span></span>  <span data-ttu-id="4054a-108">此模式用於 Intel Edison 裝置範例的韌體更新實作。</span><span class="sxs-lookup"><span data-stu-id="4054a-108">This pattern is used in the firmware update implementation for the Intel Edison device sample.</span></span>

<span data-ttu-id="4054a-109">本教學課程說明如何：</span><span class="sxs-lookup"><span data-stu-id="4054a-109">This tutorial shows you how to:</span></span>

* <span data-ttu-id="4054a-110">建立 Node.js 主控台應用程式，以透過您的 IoT 中樞在模擬裝置應用程式中呼叫 firmwareUpdate 直接方法。</span><span class="sxs-lookup"><span data-stu-id="4054a-110">Create a Node.js console app that calls the firmwareUpdate direct method in the simulated device app through your IoT hub.</span></span>
* <span data-ttu-id="4054a-111">建立會實作 **firmwareUpdate** 直接方法的模擬裝置應用程式。</span><span class="sxs-lookup"><span data-stu-id="4054a-111">Create a simulated device app that implements a **firmwareUpdate** direct method.</span></span> <span data-ttu-id="4054a-112">此方法會起始多階段程序，此程序會等候下載韌映像、下載韌體映像，最後再套用韌體映像。</span><span class="sxs-lookup"><span data-stu-id="4054a-112">This method initiates a multi-stage process that waits to download the firmware image, downloads the firmware image, and finally applies the firmware image.</span></span> <span data-ttu-id="4054a-113">在更新的每個階段，裝置都會使用回報的屬性來回報進度。</span><span class="sxs-lookup"><span data-stu-id="4054a-113">During each stage of the update, the device uses the reported properties to report on progress.</span></span>

<span data-ttu-id="4054a-114">在本教學課程結尾處，您會有兩個 Node.js 主控台應用程式：</span><span class="sxs-lookup"><span data-stu-id="4054a-114">At the end of this tutorial, you have two Node.js console apps:</span></span>

<span data-ttu-id="4054a-115">**dmpatterns_fwupdate_service.js**：在模擬裝置應用程式中呼叫直接方法、顯示回應，並定期 (每 500 毫秒) 顯示更新的報告屬性。</span><span class="sxs-lookup"><span data-stu-id="4054a-115">**dmpatterns_fwupdate_service.js**, which calls a direct method in the simulated device app, displays the response, and periodically (every 500ms) displays the updated reported properties.</span></span>

<span data-ttu-id="4054a-116">**dmpatterns_fwupdate_device.js**，這會將您的 IoT 中樞連接至稍早建立的裝置身分識別，接收 firmwareUpdate 直接方法，透過多重狀態處理執行以模擬韌體更新，包括等待映像下載、下載新的映像，最後套用映像。</span><span class="sxs-lookup"><span data-stu-id="4054a-116">**dmpatterns_fwupdate_device.js**, which connects to your IoT hub with the device identity created earlier, receives a firmwareUpdate direct method, runs through a multi-state process to simulate a firmware update including: waiting for the image download, downloading the new image, and finally applying the image.</span></span>

<span data-ttu-id="4054a-117">若要完成此教學課程，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="4054a-117">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="4054a-118">Node.js 0.12.x 版或更新版本，</span><span class="sxs-lookup"><span data-stu-id="4054a-118">Node.js version 0.12.x or later,</span></span> <br/>  <span data-ttu-id="4054a-119">[準備您的開發環境][lnk-dev-setup]說明如何在 Windows 或 Linux 上安裝本教學課程的 Node.js。</span><span class="sxs-lookup"><span data-stu-id="4054a-119">[Prepare your development environment][lnk-dev-setup] describes how to install Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="4054a-120">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="4054a-120">An active Azure account.</span></span> <span data-ttu-id="4054a-121">(如果您沒有帳戶，只需要幾分鐘的時間就可以建立[免費帳戶][lnk-free-trial]。)</span><span class="sxs-lookup"><span data-stu-id="4054a-121">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

<span data-ttu-id="4054a-122">請依照[開始使用裝置管理](iot-hub-node-node-device-management-get-started.md)文件，以建立 IoT 中樞及取得 IoT 中樞連接字串。</span><span class="sxs-lookup"><span data-stu-id="4054a-122">Follow the [Get started with device management](iot-hub-node-node-device-management-get-started.md) article to create your IoT hub and get your IoT Hub connection string.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-firmware-update-on-the-device-using-a-direct-method"></a><span data-ttu-id="4054a-123">使用直接方法在裝置上觸發遠端韌體更新</span><span class="sxs-lookup"><span data-stu-id="4054a-123">Trigger a remote firmware update on the device using a direct method</span></span>
<span data-ttu-id="4054a-124">在此節中，您會建立 Node.js 主控台應用程式，此應用程式會在裝置上起始遠端韌體更新。</span><span class="sxs-lookup"><span data-stu-id="4054a-124">In this section, you create a Node.js console app that initiates a remote firmware update on a device.</span></span> <span data-ttu-id="4054a-125">此應用程式使用直接方法來起始更新，並使用裝置對應項查詢來定期取得作用中韌體更新的狀態。</span><span class="sxs-lookup"><span data-stu-id="4054a-125">The app uses a direct method to initiate the update and uses device twin queries to periodically get the status of the active firmware update.</span></span>

1. <span data-ttu-id="4054a-126">建立稱為 **triggerfwupdateondevice** 的空資料夾。</span><span class="sxs-lookup"><span data-stu-id="4054a-126">Create an empty folder called **triggerfwupdateondevice**.</span></span>  <span data-ttu-id="4054a-127">在 **triggerfwupdateondevice** 資料夾中，於命令提示字元使用下列命令建立 package.json 檔案。</span><span class="sxs-lookup"><span data-stu-id="4054a-127">In the **triggerfwupdateondevice** folder, create a package.json file using the following command at your command prompt.</span></span>  <span data-ttu-id="4054a-128">接受所有預設值：</span><span class="sxs-lookup"><span data-stu-id="4054a-128">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="4054a-129">在 **triggerfwupdateondevice** 資料夾中，於命令提示字元執行下列命令以安裝 **azure-iot-hub** 與 **azure-iot-device-mqtt** 裝置 SDK 套件：</span><span class="sxs-lookup"><span data-stu-id="4054a-129">At your command prompt in the **triggerfwupdateondevice** folder, run the following command to install the **azure-iot-hub** and **azure-iot-device-mqtt** Device SDK packages:</span></span>
   
    ```
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="4054a-130">使用文字編輯器，在 **triggerfwupdateondevice** 資料夾中建立 **dmpatterns_getstarted_service.js** 檔案。</span><span class="sxs-lookup"><span data-stu-id="4054a-130">Using a text editor, create a **dmpatterns_getstarted_service.js** file in the **triggerfwupdateondevice** folder.</span></span>
4. <span data-ttu-id="4054a-131">在 **dmpatterns_getstarted_service.js** 檔案開頭新增下列 'require' 陳述式：</span><span class="sxs-lookup"><span data-stu-id="4054a-131">Add the following 'require' statements at the start of the **dmpatterns_getstarted_service.js** file:</span></span>
   
    ```
    'use strict';
   
    var Registry = require('azure-iothub').Registry;
    var Client = require('azure-iothub').Client;
    ```
5. <span data-ttu-id="4054a-132">新增下列變數宣告，並取代預留位置值︰</span><span class="sxs-lookup"><span data-stu-id="4054a-132">Add the following variable declarations and replace the placeholder values:</span></span>
   
    ```
    var connectionString = '{device_connectionstring}';
    var registry = Registry.fromConnectionString(connectionString);
    var client = Client.fromConnectionString(connectionString);
    var deviceToUpdate = 'myDeviceId';
    ```
6. <span data-ttu-id="4054a-133">新增下列函式來尋找並顯示 firmwareUpdate 報告屬性的值。</span><span class="sxs-lookup"><span data-stu-id="4054a-133">Add the following function to find and display the value of the firmwareUpdate reported property.</span></span>
   
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
7. <span data-ttu-id="4054a-134">新增下列函式來叫用 firmwareUpdate 方法，以重新啟動目標裝置︰</span><span class="sxs-lookup"><span data-stu-id="4054a-134">Add the following function to invoke the firmwareUpdate method to reboot the target device:</span></span>
   
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
          console.error('Could not start the firmware update on the device: ' + err.message)
        } 
      });
    };
    ```
8. <span data-ttu-id="4054a-135">最後，新增下列函式至程式碼，以啟動韌體更新順序，並且定期顯示報告屬性︰</span><span class="sxs-lookup"><span data-stu-id="4054a-135">Finally, Add the following function to code to start the firmware update sequence and start periodically showing the reported properties:</span></span>
   
    ```
    startFirmwareUpdateDevice();
    setInterval(queryTwinFWUpdateReported, 500);
    ```
9. <span data-ttu-id="4054a-136">儲存並關閉 **dmpatterns_fwupdate_service.js** 檔案。</span><span class="sxs-lookup"><span data-stu-id="4054a-136">Save and close the **dmpatterns_fwupdate_service.js** file.</span></span>

[!INCLUDE [iot-hub-device-firmware-update](../../includes/iot-hub-device-firmware-update.md)]

## <a name="run-the-apps"></a><span data-ttu-id="4054a-137">執行應用程式</span><span class="sxs-lookup"><span data-stu-id="4054a-137">Run the apps</span></span>
<span data-ttu-id="4054a-138">您現在可以開始執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="4054a-138">You are now ready to run the apps.</span></span>

1. <span data-ttu-id="4054a-139">在 **manageddevice** 資料夾中，於命令提示字元中執行下列命令以開始接聽重新啟動直接方法。</span><span class="sxs-lookup"><span data-stu-id="4054a-139">At the command prompt in the **manageddevice** folder, run the following command to begin listening for the reboot direct method.</span></span>
   
    ```
    node dmpatterns_fwupdate_device.js
    ```
2. <span data-ttu-id="4054a-140">在命令提示字元中，於 **triggerfwupdateondevice** 資料夾執行下列命令以觸發裝置對應項的遠端重新啟動，以及查詢裝置對應項來尋找上次重新啟動時間。</span><span class="sxs-lookup"><span data-stu-id="4054a-140">At the command prompt in the **triggerfwupdateondevice** folder, run the following command to trigger the remote reboot and query for the device twin to find the last reboot time.</span></span>
   
    ```
    node dmpatterns_fwupdate_service.js
    ```
3. <span data-ttu-id="4054a-141">您會在主控台中看到直接方法的裝置回應。</span><span class="sxs-lookup"><span data-stu-id="4054a-141">You see the device response to the direct method in the console.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4054a-142">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4054a-142">Next steps</span></span>
<span data-ttu-id="4054a-143">在此教學課程中，您使用直接方法來觸發裝置上的遠端韌體更新，並且使用回報的屬性追蹤韌體更新的進度。</span><span class="sxs-lookup"><span data-stu-id="4054a-143">In this tutorial, you used a direct method to trigger a remote firmware update on a device and used the reported properties to follow the progress of the firmware update.</span></span>

<span data-ttu-id="4054a-144">若要了解如何擴充您的 IoT 解決方案以及在多個裝置上排程方法呼叫，請參閱[排程及廣播作業][lnk-tutorial-jobs]教學課程。</span><span class="sxs-lookup"><span data-stu-id="4054a-144">To learn how to extend your IoT solution and schedule method calls on multiple devices, see the [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-dm-getstarted]: iot-hub-node-node-device-management-get-started.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
