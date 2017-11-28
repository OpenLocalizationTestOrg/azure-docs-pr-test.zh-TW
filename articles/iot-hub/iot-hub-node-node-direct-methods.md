---
title: "IoT 中樞 aaaAzure 直接方法 （節點） |Microsoft 文件"
description: "如何 toouse Azure IoT 中樞直接的方法。 您可以使用 hello Azure IoT Sdk for Node.js tooimplement 模擬的裝置應用程式，其中包含直接的方法與 hello 直接的方法會叫用的服務應用程式。"
services: iot-hub
documentationcenter: 
author: nberdy
manager: timlt
editor: 
ms.assetid: ea9c73ca-7778-4e38-a8f1-0bee9d142f04
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: nberdy
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 12300ba451816fec1f80163b633f6b6e411d9e5c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-direct-methods-on-your-iot-device-with-nodejs"></a><span data-ttu-id="ee7b8-104">搭配 Node.js 在 IoT 裝置上使用直接方法</span><span class="sxs-lookup"><span data-stu-id="ee7b8-104">Use direct methods on your IoT device with Node.js</span></span>
[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

<span data-ttu-id="ee7b8-105">在本教學課程的 hello 最後，您有兩個 Node.js 主控台應用程式：</span><span class="sxs-lookup"><span data-stu-id="ee7b8-105">At hello end of this tutorial, you have two Node.js console apps:</span></span>

* <span data-ttu-id="ee7b8-106">**CallMethodOnDevice.js**，其中呼叫 hello 模擬的裝置應用程式中的方法，並顯示 hello 回應。</span><span class="sxs-lookup"><span data-stu-id="ee7b8-106">**CallMethodOnDevice.js**, which calls a method in hello simulated device app and displays hello response.</span></span>
* <span data-ttu-id="ee7b8-107">**SimulatedDevice.js**，連接 tooyour IoT 中樞與 hello 稍早建立的裝置身分識別以及回應 hello 雲端呼叫 toohello 方法。</span><span class="sxs-lookup"><span data-stu-id="ee7b8-107">**SimulatedDevice.js**, which connects tooyour IoT hub with hello device identity created earlier, and responds toohello method called by hello cloud.</span></span>

> [!NOTE]
> <span data-ttu-id="ee7b8-108">hello 文章[Azure IoT Sdk] [ lnk-hub-sdks]提供 hello Azure IoT Sdk 的相關資訊，您可以使用 toobuild 這兩個應用程式 toorun 裝置和您的方案後端上。</span><span class="sxs-lookup"><span data-stu-id="ee7b8-108">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both applications toorun on devices and your solution back end.</span></span>
> 
> 

<span data-ttu-id="ee7b8-109">toocomplete 本教學課程中，您需要遵循的 hello:</span><span class="sxs-lookup"><span data-stu-id="ee7b8-109">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="ee7b8-110">Node.js 0.10.x 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="ee7b8-110">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="ee7b8-111">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="ee7b8-111">An active Azure account.</span></span> <span data-ttu-id="ee7b8-112">(如果您沒有帳戶，只需要幾分鐘的時間就可以建立[免費帳戶][lnk-free-trial]。)</span><span class="sxs-lookup"><span data-stu-id="ee7b8-112">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="ee7b8-113">建立模擬裝置應用程式</span><span class="sxs-lookup"><span data-stu-id="ee7b8-113">Create a simulated device app</span></span>
<span data-ttu-id="ee7b8-114">本節中，您可以建立會回應呼叫 hello 雲端 tooa 方法 Node.js 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="ee7b8-114">In this section, you create a Node.js console app that responds tooa method called by hello cloud.</span></span>

1. <span data-ttu-id="ee7b8-115">建立稱為 **simulateddevice**的新的空資料夾。</span><span class="sxs-lookup"><span data-stu-id="ee7b8-115">Create a new empty folder called **simulateddevice**.</span></span> <span data-ttu-id="ee7b8-116">在 hello **simulateddevice**資料夾中，建立使用下列命令，在您的命令提示字元的 hello package.json 檔案。</span><span class="sxs-lookup"><span data-stu-id="ee7b8-116">In hello **simulateddevice** folder, create a package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="ee7b8-117">接受所有的 hello 預設值：</span><span class="sxs-lookup"><span data-stu-id="ee7b8-117">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="ee7b8-118">在您的命令提示字元中 hello **simulateddevice**資料夾中，執行下列命令 tooinstall hello hello **azure iot 裝置**裝置 SDK 封裝和**azure-iot-裝置-mqtt**封裝：</span><span class="sxs-lookup"><span data-stu-id="ee7b8-118">At your command prompt in hello **simulateddevice** folder, run hello following command tooinstall hello **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="ee7b8-119">使用文字編輯器中，建立新**SimulatedDevice.js**檔案在 hello **simulateddevice**資料夾。</span><span class="sxs-lookup"><span data-stu-id="ee7b8-119">Using a text editor, create a new **SimulatedDevice.js** file in hello **simulateddevice** folder.</span></span>
4. <span data-ttu-id="ee7b8-120">新增下列 hello`require`陳述式在 hello 開頭 hello **SimulatedDevice.js**檔案：</span><span class="sxs-lookup"><span data-stu-id="ee7b8-120">Add hello following `require` statements at hello start of hello **SimulatedDevice.js** file:</span></span>
   
    ```
    'use strict';
   
    var Mqtt = require('azure-iot-device-mqtt').Mqtt;
    var DeviceClient = require('azure-iot-device').Client;
    ```
5. <span data-ttu-id="ee7b8-121">新增**connectionString**變數，並使用它 toocreate **DeviceClient**執行個體。</span><span class="sxs-lookup"><span data-stu-id="ee7b8-121">Add a **connectionString** variable and use it toocreate a **DeviceClient** instance.</span></span> <span data-ttu-id="ee7b8-122">取代**{裝置連接字串}** hello 裝置連接字串中 hello 產生*建立裝置身分識別*> 一節：</span><span class="sxs-lookup"><span data-stu-id="ee7b8-122">Replace **{device connection string}** with hello device connection string you generated in hello *Create a device identity* section:</span></span>
   
    ```
    var connectionString = '{device connection string}';
    var client = DeviceClient.fromConnectionString(connectionString, Mqtt);
    ```
6. <span data-ttu-id="ee7b8-123">加入下列函式 tooimplement hello 方法 hello 裝置上的 hello:</span><span class="sxs-lookup"><span data-stu-id="ee7b8-123">Add hello following function tooimplement hello method on hello device:</span></span>
   
    ```
    function onWriteLine(request, response) {
        console.log(request.payload);
   
        response.send(200, 'Input was written toolog.', function(err) {
            if(err) {
                console.error('An error ocurred when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.' );
            }
        });
    }
    ```
7. <span data-ttu-id="ee7b8-124">開啟 hello 連接 tooyour IoT 中樞，並啟動初始化 hello 方法接聽程式：</span><span class="sxs-lookup"><span data-stu-id="ee7b8-124">Open hello connection tooyour IoT hub and start initialize hello method listener:</span></span>
   
    ```
    client.open(function(err) {
        if (err) {
            console.error('could not open IotHub client');
        }  else {
            console.log('client opened');
            client.onDeviceMethod('writeLine', onWriteLine);
        }
    });
    ```
8. <span data-ttu-id="ee7b8-125">儲存並關閉 hello **SimulatedDevice.js**檔案。</span><span class="sxs-lookup"><span data-stu-id="ee7b8-125">Save and close hello **SimulatedDevice.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="ee7b8-126">簡單 tookeep 方面，本教學課程未實作任何重試原則。</span><span class="sxs-lookup"><span data-stu-id="ee7b8-126">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="ee7b8-127">在實際執行程式碼，您應該實作重試原則 （例如連線重試），做為建議 hello MSDN 文件中[暫時性錯誤處理][lnk-transient-faults]。</span><span class="sxs-lookup"><span data-stu-id="ee7b8-127">In production code, you should implement retry policies (such as connection retry), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="call-a-method-on-a-device"></a><span data-ttu-id="ee7b8-128">在裝置上呼叫方法</span><span class="sxs-lookup"><span data-stu-id="ee7b8-128">Call a method on a device</span></span>
<span data-ttu-id="ee7b8-129">在本節中，您可以建立 Node.js 主控台應用程式會呼叫 hello 模擬的裝置應用程式中的方法，並顯示 hello 回應。</span><span class="sxs-lookup"><span data-stu-id="ee7b8-129">In this section, you create a Node.js console app that calls a method in hello simulated device app and then displays hello response.</span></span>

1. <span data-ttu-id="ee7b8-130">建立稱為 **callmethodondevice**的新的空資料夾。</span><span class="sxs-lookup"><span data-stu-id="ee7b8-130">Create a new empty folder called **callmethodondevice**.</span></span> <span data-ttu-id="ee7b8-131">在 hello **callmethodondevice**資料夾中，建立使用下列命令，在您的命令提示字元的 hello package.json 檔案。</span><span class="sxs-lookup"><span data-stu-id="ee7b8-131">In hello **callmethodondevice** folder, create a package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="ee7b8-132">接受所有的 hello 預設值：</span><span class="sxs-lookup"><span data-stu-id="ee7b8-132">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="ee7b8-133">在您的命令提示字元中 hello **callmethodondevice**資料夾中，執行下列命令 tooinstall hello hello **azure iot 中樞**封裝：</span><span class="sxs-lookup"><span data-stu-id="ee7b8-133">At your command prompt in hello **callmethodondevice** folder, run hello following command tooinstall hello **azure-iothub** package:</span></span>
   
    ```
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="ee7b8-134">使用文字編輯器中，建立**CallMethodOnDevice.js**檔案在 hello **callmethodondevice**資料夾。</span><span class="sxs-lookup"><span data-stu-id="ee7b8-134">Using a text editor, create a **CallMethodOnDevice.js** file in hello **callmethodondevice** folder.</span></span>
4. <span data-ttu-id="ee7b8-135">新增下列 hello`require`陳述式在 hello 開頭 hello **CallMethodOnDevice.js**檔案：</span><span class="sxs-lookup"><span data-stu-id="ee7b8-135">Add hello following `require` statements at hello start of hello **CallMethodOnDevice.js** file:</span></span>
   
    ```
    'use strict';
   
    var Client = require('azure-iothub').Client;
    ```
5. <span data-ttu-id="ee7b8-136">加入下列變數宣告 hello 和 hello 預留位置值取代為您的中樞的 IoT 中樞連接字串 hello:</span><span class="sxs-lookup"><span data-stu-id="ee7b8-136">Add hello following variable declaration and replace hello placeholder value with hello IoT Hub connection string for your hub:</span></span>
   
    ```
    var connectionString = '{iothub connection string}';
    var methodName = 'writeLine';
    var deviceId = 'myDeviceId';
    ```
6. <span data-ttu-id="ee7b8-137">建立 hello 用 tooopen hello 連接 tooyour IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="ee7b8-137">Create hello client tooopen hello connection tooyour IoT hub.</span></span>
   
    ```
    var client = Client.fromConnectionString(connectionString);
    ```
7. <span data-ttu-id="ee7b8-138">加入下列函式 tooinvoke hello 裝置方法及列印 hello 裝置回應 toohello 主控台 hello:</span><span class="sxs-lookup"><span data-stu-id="ee7b8-138">Add hello following function tooinvoke hello device method and print hello device response toohello console:</span></span>
   
    ```
    var methodParams = {
        methodName: methodName,
        payload: 'hello world',
        timeoutInSeconds: 30
    };
   
    client.invokeDeviceMethod(deviceId, methodParams, function (err, result) {
        if (err) {
            console.error('Failed tooinvoke method \'' + methodName + '\': ' + err.message);
        } else {
            console.log(methodName + ' on ' + deviceId + ':');
            console.log(JSON.stringify(result, null, 2));
        }
    });
    ```
8. <span data-ttu-id="ee7b8-139">儲存並關閉 hello **CallMethodOnDevice.js**檔案。</span><span class="sxs-lookup"><span data-stu-id="ee7b8-139">Save and close hello **CallMethodOnDevice.js** file.</span></span>

## <a name="run-hello-apps"></a><span data-ttu-id="ee7b8-140">執行 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="ee7b8-140">Run hello apps</span></span>
<span data-ttu-id="ee7b8-141">現在您已經準備就緒 toorun hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ee7b8-141">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="ee7b8-142">在命令提示字元中 hello **simulateddevice**資料夾中，執行下列命令 toostart 接聽從 IoT 中樞的方法呼叫的 hello:</span><span class="sxs-lookup"><span data-stu-id="ee7b8-142">At a command prompt in hello **simulateddevice** folder, run hello following command toostart listening for method calls from your IoT Hub:</span></span>
   
    ```
    node SimulatedDevice.js
    ```
   
    ![][7]
2. <span data-ttu-id="ee7b8-143">在命令提示字元中 hello **callmethodondevice**資料夾中，執行下列命令 toobegin 監視您的 IoT 中樞的 hello:</span><span class="sxs-lookup"><span data-stu-id="ee7b8-143">At a command prompt in hello **callmethodondevice** folder, run hello following command toobegin monitoring your IoT hub:</span></span>
   
    ```
    node CallMethodOnDevice.js 
    ```
   
    ![][8]
3. <span data-ttu-id="ee7b8-144">您會看見 hello 回應 toohello 方法列印出 hello 訊息和呼叫 hello 方法顯示 hello 回應 hello 裝置 hello 應用程式的裝置：</span><span class="sxs-lookup"><span data-stu-id="ee7b8-144">You will see hello device react toohello method by printing out hello message and hello application which called hello method display hello response from hello device:</span></span>
   
    ![][9]

## <a name="next-steps"></a><span data-ttu-id="ee7b8-145">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ee7b8-145">Next steps</span></span>
<span data-ttu-id="ee7b8-146">在本教學課程中，您在 hello Azure 入口網站中設定新的 IoT 中樞，並接著 hello IoT 中樞的身分識別登錄中建立裝置身分識別。</span><span class="sxs-lookup"><span data-stu-id="ee7b8-146">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="ee7b8-147">您已經使用此裝置身分識別 tooenable hello 模擬裝置的應用程式 tooreact toomethods hello 雲端所叫用。</span><span class="sxs-lookup"><span data-stu-id="ee7b8-147">You used this device identity tooenable hello simulated device app tooreact toomethods invoked by hello cloud.</span></span> <span data-ttu-id="ee7b8-148">您也會建立叫用 hello 裝置上的方法，並會顯示 hello 回應 hello 裝置的應用程式。</span><span class="sxs-lookup"><span data-stu-id="ee7b8-148">You also created an app that invokes methods on hello device and displays hello response from hello device.</span></span> 

<span data-ttu-id="ee7b8-149">使用者入門 toocontinue tooexplore IoT 中樞與其他 IoT 案例，請參閱：</span><span class="sxs-lookup"><span data-stu-id="ee7b8-149">toocontinue getting started with IoT Hub and tooexplore other IoT scenarios, see:</span></span>

* <span data-ttu-id="ee7b8-150">[IoT 中心入門]</span><span class="sxs-lookup"><span data-stu-id="ee7b8-150">[Get started with IoT Hub]</span></span>
* <span data-ttu-id="ee7b8-151">[排程多個裝置上的作業][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="ee7b8-151">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="ee7b8-152">toolearn 如何 tooextend IoT 解決方案和排程方法呼叫上多個裝置，請參閱 hello[排程和廣播的工作][ lnk-tutorial-jobs]教學課程。</span><span class="sxs-lookup"><span data-stu-id="ee7b8-152">toolearn how tooextend your IoT solution and schedule method calls on multiple devices, see hello [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

<!-- Images. -->
[7]: ./media/iot-hub-node-node-direct-methods/run-simulated-device.png
[8]: ./media/iot-hub-node-node-direct-methods/run-callmethodondevice.png
[9]: ./media/iot-hub-node-node-direct-methods/methods-output.png

<!-- Links -->
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal]: https://portal.azure.com/

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-devguide-methods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md

[Send Cloud-to-Device messages with IoT Hub]: iot-hub-csharp-csharp-c2d.md
[Process Device-to-Cloud messages]: iot-hub-csharp-csharp-process-d2c.md
[IoT 中心入門]: iot-hub-node-node-getstarted.md
