---
title: "Azure IoT 中樞直接方法 (Node) | Microsoft Docs"
description: "如何使用 Azure IoT 中樞直接方法。 您可以使用適用於 Node.js 的 Azure IoT SDK，實作模擬裝置應用程式 (包含直接方法) 和服務應用程式 (叫用直接方法)。"
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
ms.openlocfilehash: 83725c3ae3fd3807f2469be888e270ba078a8972
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="use-direct-methods-on-your-iot-device-with-nodejs"></a><span data-ttu-id="04627-104">搭配 Node.js 在 IoT 裝置上使用直接方法</span><span class="sxs-lookup"><span data-stu-id="04627-104">Use direct methods on your IoT device with Node.js</span></span>
[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

<span data-ttu-id="04627-105">在本教學課程結尾處，您會有兩個 Node.js 主控台應用程式：</span><span class="sxs-lookup"><span data-stu-id="04627-105">At the end of this tutorial, you have two Node.js console apps:</span></span>

* <span data-ttu-id="04627-106">**CallMethodOnDevice.js**，會在模擬裝置應用程式中呼叫方法，並顯示回應。</span><span class="sxs-lookup"><span data-stu-id="04627-106">**CallMethodOnDevice.js**, which calls a method in the simulated device app and displays the response.</span></span>
* <span data-ttu-id="04627-107">**SimulatedDevice.js**，會使用先前建立的裝置身分識別連接到您的 IoT 中樞，並且回應雲端呼叫的方法。</span><span class="sxs-lookup"><span data-stu-id="04627-107">**SimulatedDevice.js**, which connects to your IoT hub with the device identity created earlier, and responds to the method called by the cloud.</span></span>

> [!NOTE]
> <span data-ttu-id="04627-108">[Azure IoT SDK][lnk-hub-sdks] 一文提供 Azure IoT SDK (可讓您同時建置在裝置與您的解決方案後端執行的兩個應用程式) 的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="04627-108">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both applications to run on devices and your solution back end.</span></span>
> 
> 

<span data-ttu-id="04627-109">若要完成此教學課程，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="04627-109">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="04627-110">Node.js 0.10.x 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="04627-110">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="04627-111">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="04627-111">An active Azure account.</span></span> <span data-ttu-id="04627-112">(如果您沒有帳戶，只需要幾分鐘的時間就可以建立[免費帳戶][lnk-free-trial]。)</span><span class="sxs-lookup"><span data-stu-id="04627-112">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="04627-113">建立模擬裝置應用程式</span><span class="sxs-lookup"><span data-stu-id="04627-113">Create a simulated device app</span></span>
<span data-ttu-id="04627-114">在本節中，您建立 Node.js 主控台應用程式，回應雲端所呼叫的方法。</span><span class="sxs-lookup"><span data-stu-id="04627-114">In this section, you create a Node.js console app that responds to a method called by the cloud.</span></span>

1. <span data-ttu-id="04627-115">建立稱為 **simulateddevice**的新的空資料夾。</span><span class="sxs-lookup"><span data-stu-id="04627-115">Create a new empty folder called **simulateddevice**.</span></span> <span data-ttu-id="04627-116">在 **simulateddevice** 資料夾中，於命令提示字元使用下列命令建立 package.json 檔案。</span><span class="sxs-lookup"><span data-stu-id="04627-116">In the **simulateddevice** folder, create a package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="04627-117">接受所有預設值：</span><span class="sxs-lookup"><span data-stu-id="04627-117">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="04627-118">在 **simulateddevice** 資料夾中，於命令提示字元執行下列命令以安裝 **azure-iot-device** 裝置 SDK 套件以及 **azure-iot-device-mqtt** 套件：</span><span class="sxs-lookup"><span data-stu-id="04627-118">At your command prompt in the **simulateddevice** folder, run the following command to install the **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="04627-119">使用文字編輯器，在 **simulateddevice** 資料夾中建立新的 **SimulatedDevice.js** 檔案。</span><span class="sxs-lookup"><span data-stu-id="04627-119">Using a text editor, create a new **SimulatedDevice.js** file in the **simulateddevice** folder.</span></span>
4. <span data-ttu-id="04627-120">在 **SimulatedDevice.js** 檔案開頭新增下列 `require` 陳述式：</span><span class="sxs-lookup"><span data-stu-id="04627-120">Add the following `require` statements at the start of the **SimulatedDevice.js** file:</span></span>
   
    ```
    'use strict';
   
    var Mqtt = require('azure-iot-device-mqtt').Mqtt;
    var DeviceClient = require('azure-iot-device').Client;
    ```
5. <span data-ttu-id="04627-121">新增 **connectionString** 變數，並用它來建立 **DeviceClient** 執行個體。</span><span class="sxs-lookup"><span data-stu-id="04627-121">Add a **connectionString** variable and use it to create a **DeviceClient** instance.</span></span> <span data-ttu-id="04627-122">將 **{device connection string}** 取代為您在*建立裝置身分識別*一節中產生的連接字串：</span><span class="sxs-lookup"><span data-stu-id="04627-122">Replace **{device connection string}** with the device connection string you generated in the *Create a device identity* section:</span></span>
   
    ```
    var connectionString = '{device connection string}';
    var client = DeviceClient.fromConnectionString(connectionString, Mqtt);
    ```
6. <span data-ttu-id="04627-123">新增下列函式，在裝置上實作方法︰</span><span class="sxs-lookup"><span data-stu-id="04627-123">Add the following function to implement the method on the device:</span></span>
   
    ```
    function onWriteLine(request, response) {
        console.log(request.payload);
   
        response.send(200, 'Input was written to log.', function(err) {
            if(err) {
                console.error('An error ocurred when sending a method response:\n' + err.toString());
            } else {
                console.log('Response to method \'' + request.methodName + '\' sent successfully.' );
            }
        });
    }
    ```
7. <span data-ttu-id="04627-124">開啟您 IoT 中樞的連線，並開始初始化方法接聽程式︰</span><span class="sxs-lookup"><span data-stu-id="04627-124">Open the connection to your IoT hub and start initialize the method listener:</span></span>
   
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
8. <span data-ttu-id="04627-125">儲存並關閉 **SimulatedDevice.js** 檔案。</span><span class="sxs-lookup"><span data-stu-id="04627-125">Save and close the **SimulatedDevice.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="04627-126">為了簡單起見，本教學課程不會實作任何重試原則。</span><span class="sxs-lookup"><span data-stu-id="04627-126">To keep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="04627-127">在生產環境程式碼中，您應該如 MSDN 文章[暫時性錯誤處理][lnk-transient-faults]所建議，實作重試原則 (例如連接重試)。</span><span class="sxs-lookup"><span data-stu-id="04627-127">In production code, you should implement retry policies (such as connection retry), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="call-a-method-on-a-device"></a><span data-ttu-id="04627-128">在裝置上呼叫方法</span><span class="sxs-lookup"><span data-stu-id="04627-128">Call a method on a device</span></span>
<span data-ttu-id="04627-129">在本節中，您會建立 Node.js 主控台應用程式，在模擬裝置應用程式中呼叫方法，然後顯示回應。</span><span class="sxs-lookup"><span data-stu-id="04627-129">In this section, you create a Node.js console app that calls a method in the simulated device app and then displays the response.</span></span>

1. <span data-ttu-id="04627-130">建立稱為 **callmethodondevice**的新的空資料夾。</span><span class="sxs-lookup"><span data-stu-id="04627-130">Create a new empty folder called **callmethodondevice**.</span></span> <span data-ttu-id="04627-131">在 **callmethodondevice** 資料夾中，於命令提示字元使用下列命令建立 package.json 檔案。</span><span class="sxs-lookup"><span data-stu-id="04627-131">In the **callmethodondevice** folder, create a package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="04627-132">接受所有預設值：</span><span class="sxs-lookup"><span data-stu-id="04627-132">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="04627-133">在 **callmethodondevice** 資料夾中，於命令提示字元執行下列命令以安裝 **azure-iothub** 套件：</span><span class="sxs-lookup"><span data-stu-id="04627-133">At your command prompt in the **callmethodondevice** folder, run the following command to install the **azure-iothub** package:</span></span>
   
    ```
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="04627-134">使用文字編輯器，在 **callmethodondevice** 資料夾中建立 **CallMethodOnDevice.js** 檔案。</span><span class="sxs-lookup"><span data-stu-id="04627-134">Using a text editor, create a **CallMethodOnDevice.js** file in the **callmethodondevice** folder.</span></span>
4. <span data-ttu-id="04627-135">在 **CallMethodOnDevice.js** 檔案開頭新增下列 `require` 陳述式：</span><span class="sxs-lookup"><span data-stu-id="04627-135">Add the following `require` statements at the start of the **CallMethodOnDevice.js** file:</span></span>
   
    ```
    'use strict';
   
    var Client = require('azure-iothub').Client;
    ```
5. <span data-ttu-id="04627-136">新增下列變數宣告，並將預留位置值替換為中樞的 IoT 中樞連接字串：</span><span class="sxs-lookup"><span data-stu-id="04627-136">Add the following variable declaration and replace the placeholder value with the IoT Hub connection string for your hub:</span></span>
   
    ```
    var connectionString = '{iothub connection string}';
    var methodName = 'writeLine';
    var deviceId = 'myDeviceId';
    ```
6. <span data-ttu-id="04627-137">建立用戶端以開啟到您的 IoT 中樞的連接。</span><span class="sxs-lookup"><span data-stu-id="04627-137">Create the client to open the connection to your IoT hub.</span></span>
   
    ```
    var client = Client.fromConnectionString(connectionString);
    ```
7. <span data-ttu-id="04627-138">新增下列函式來叫用裝置方法，並列印對主控台的裝置回應︰</span><span class="sxs-lookup"><span data-stu-id="04627-138">Add the following function to invoke the device method and print the device response to the console:</span></span>
   
    ```
    var methodParams = {
        methodName: methodName,
        payload: 'hello world',
        timeoutInSeconds: 30
    };
   
    client.invokeDeviceMethod(deviceId, methodParams, function (err, result) {
        if (err) {
            console.error('Failed to invoke method \'' + methodName + '\': ' + err.message);
        } else {
            console.log(methodName + ' on ' + deviceId + ':');
            console.log(JSON.stringify(result, null, 2));
        }
    });
    ```
8. <span data-ttu-id="04627-139">儲存並關閉 **CallMethodOnDevice.js** 檔案。</span><span class="sxs-lookup"><span data-stu-id="04627-139">Save and close the **CallMethodOnDevice.js** file.</span></span>

## <a name="run-the-apps"></a><span data-ttu-id="04627-140">執行應用程式</span><span class="sxs-lookup"><span data-stu-id="04627-140">Run the apps</span></span>
<span data-ttu-id="04627-141">您現在可以開始執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="04627-141">You are now ready to run the apps.</span></span>

1. <span data-ttu-id="04627-142">在 **simulateddevice** 資料夾的命令提示字元中，執行下列命令以開始接聽來自您的 IoT 中樞的方法呼叫：</span><span class="sxs-lookup"><span data-stu-id="04627-142">At a command prompt in the **simulateddevice** folder, run the following command to start listening for method calls from your IoT Hub:</span></span>
   
    ```
    node SimulatedDevice.js
    ```
   
    ![][7]
2. <span data-ttu-id="04627-143">在 **callmethodondevice** 資料夾的命令提示字元中，執行下列命令以開始監視 IoT 中樞：</span><span class="sxs-lookup"><span data-stu-id="04627-143">At a command prompt in the **callmethodondevice** folder, run the following command to begin monitoring your IoT hub:</span></span>
   
    ```
    node CallMethodOnDevice.js 
    ```
   
    ![][8]
3. <span data-ttu-id="04627-144">您會看到裝置對方法的反應，方法是列印訊息和應用程式，它們會呼叫方法並且顯示來自裝置的回應：</span><span class="sxs-lookup"><span data-stu-id="04627-144">You will see the device react to the method by printing out the message and the application which called the method display the response from the device:</span></span>
   
    ![][9]

## <a name="next-steps"></a><span data-ttu-id="04627-145">後續步驟</span><span class="sxs-lookup"><span data-stu-id="04627-145">Next steps</span></span>
<span data-ttu-id="04627-146">在此教學課程中，您在 Azure 入口網站中設定了新的 IoT 中樞，然後在 IoT 中樞的身分識別登錄中建立了裝置身分識別。</span><span class="sxs-lookup"><span data-stu-id="04627-146">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="04627-147">您會將此裝置識別用於啟用模擬的裝置應用程式，以將雲端所叫用的方法進行反應。</span><span class="sxs-lookup"><span data-stu-id="04627-147">You used this device identity to enable the simulated device app to react to methods invoked by the cloud.</span></span> <span data-ttu-id="04627-148">您也會建立應用程式，在裝置上叫用方法，並且顯示來自裝置的回應。</span><span class="sxs-lookup"><span data-stu-id="04627-148">You also created an app that invokes methods on the device and displays the response from the device.</span></span> 

<span data-ttu-id="04627-149">若要繼續開始使用 IoT 中樞並瀏覽其他 IoT 案例，請參閱︰</span><span class="sxs-lookup"><span data-stu-id="04627-149">To continue getting started with IoT Hub and to explore other IoT scenarios, see:</span></span>

* <span data-ttu-id="04627-150">[IoT 中樞入門]</span><span class="sxs-lookup"><span data-stu-id="04627-150">[Get started with IoT Hub]</span></span>
* <span data-ttu-id="04627-151">[排程多個裝置上的作業][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="04627-151">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="04627-152">若要了解如何擴充您的 IoT 解決方案以及在多個裝置上排程方法呼叫，請參閱[排程及廣播作業][lnk-tutorial-jobs]教學課程。</span><span class="sxs-lookup"><span data-stu-id="04627-152">To learn how to extend your IoT solution and schedule method calls on multiple devices, see the [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

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
[IoT 中樞入門]: iot-hub-node-node-getstarted.md
