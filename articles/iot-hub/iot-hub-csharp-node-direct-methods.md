---
title: "Azure IoT 中樞 aaaUse 直接方法 （.NET/節點） |Microsoft 文件"
description: "如何 toouse Azure IoT 中樞直接的方法。 您可以使用 hello Azure IoT 裝置 SDK for Node.js tooimplement 模擬的裝置應用程式，其中包含直接的方法和 hello Azure IoT 服務 SDK for.NET tooimplement hello 直接的方法會叫用的服務應用程式。"
services: iot-hub
documentationcenter: 
author: nberdy
manager: timlt
editor: 
ms.assetid: ab035b8e-bff8-4e12-9536-f31d6b6fe425
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/10/2017
ms.author: nberdy
ms.openlocfilehash: f566f939be840eb308b00ffa4e05c4e5b3fefb39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-direct-methods-netnode"></a><span data-ttu-id="d5783-104">使用直接方法 (.NET/Node)</span><span class="sxs-lookup"><span data-stu-id="d5783-104">Use direct methods (.NET/Node)</span></span>
[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

<span data-ttu-id="d5783-105">在本教學課程中，我們會 toodevelop.NET 和 Node.js 主控台應用程式：</span><span class="sxs-lookup"><span data-stu-id="d5783-105">In this tutorial, we are going toodevelop a .NET and a Node.js console app:</span></span>

* <span data-ttu-id="d5783-106">**CallMethodOnDevice.sln**，.NET 後端應用程式中，會呼叫 hello 模擬的裝置應用程式中的方法，並顯示 hello 回應。</span><span class="sxs-lookup"><span data-stu-id="d5783-106">**CallMethodOnDevice.sln**, a .NET back-end app, which calls a method in hello simulated device app and displays hello response.</span></span>
* <span data-ttu-id="d5783-107">**SimulatedDevice.js**，Node.js 應用程式，這會模擬使用稍早建立的 hello 裝置身分識別連接 tooyour IoT 中樞的裝置，並會回應呼叫 hello 雲端 toohello 方法。</span><span class="sxs-lookup"><span data-stu-id="d5783-107">**SimulatedDevice.js**, a Node.js app, which simulates a device connecting tooyour IoT hub with hello device identity created earlier, and responds toohello method called by hello cloud.</span></span>

> [!NOTE]
> <span data-ttu-id="d5783-108">hello 文章[Azure IoT Sdk] [ lnk-hub-sdks]提供 hello Azure IoT Sdk 的相關資訊，您可以使用 toobuild 這兩個應用程式 toorun 裝置和您的方案後端上。</span><span class="sxs-lookup"><span data-stu-id="d5783-108">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both applications toorun on devices and your solution back end.</span></span>
> 
> 

<span data-ttu-id="d5783-109">toocomplete 本教學課程中，您需要：</span><span class="sxs-lookup"><span data-stu-id="d5783-109">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="d5783-110">Visual Studio 2015 或 Visual Studio 2017。</span><span class="sxs-lookup"><span data-stu-id="d5783-110">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="d5783-111">Node.js 0.10.x 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="d5783-111">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="d5783-112">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="d5783-112">An active Azure account.</span></span> <span data-ttu-id="d5783-113">(如果您沒有帳戶，只需要幾分鐘的時間就可以建立[免費帳戶][lnk-free-trial]。)</span><span class="sxs-lookup"><span data-stu-id="d5783-113">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="d5783-114">建立模擬裝置應用程式</span><span class="sxs-lookup"><span data-stu-id="d5783-114">Create a simulated device app</span></span>
<span data-ttu-id="d5783-115">在本節中，您可以建立回應 hello 方案回呼叫端的 tooa 方法 Node.js 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="d5783-115">In this section, you create a Node.js console app that responds tooa method called by hello solution back end.</span></span>

1. <span data-ttu-id="d5783-116">建立稱為 **simulateddevice**的新的空資料夾。</span><span class="sxs-lookup"><span data-stu-id="d5783-116">Create a new empty folder called **simulateddevice**.</span></span> <span data-ttu-id="d5783-117">在 hello **simulateddevice**資料夾中，建立使用下列命令，在您的命令提示字元的 hello package.json 檔案。</span><span class="sxs-lookup"><span data-stu-id="d5783-117">In hello **simulateddevice** folder, create a package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="d5783-118">接受所有的 hello 預設值：</span><span class="sxs-lookup"><span data-stu-id="d5783-118">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="d5783-119">在您的命令提示字元中 hello **simulateddevice**資料夾中，執行下列命令 tooinstall hello hello **azure iot 裝置**和**azure iot 裝置-mqtt**封裝：</span><span class="sxs-lookup"><span data-stu-id="d5783-119">At your command prompt in hello **simulateddevice** folder, run hello following command tooinstall hello **azure-iot-device** and **azure-iot-device-mqtt** packages:</span></span>
   
    ```
        npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="d5783-120">使用文字編輯器中，建立的檔案在 hello **simulateddevice**資料夾並將其命名**SimulatedDevice.js**。</span><span class="sxs-lookup"><span data-stu-id="d5783-120">Using a text editor, create a file in hello **simulateddevice** folder and name it **SimulatedDevice.js**.</span></span>
4. <span data-ttu-id="d5783-121">新增下列 hello`require`陳述式在 hello 開頭 hello **SimulatedDevice.js**檔案：</span><span class="sxs-lookup"><span data-stu-id="d5783-121">Add hello following `require` statements at hello start of hello **SimulatedDevice.js** file:</span></span>
   
    ```
    'use strict';
   
    var Mqtt = require('azure-iot-device-mqtt').Mqtt;
    var DeviceClient = require('azure-iot-device').Client;
    ```
5. <span data-ttu-id="d5783-122">新增**connectionString**變數，並使用它 toocreate **DeviceClient**執行個體。</span><span class="sxs-lookup"><span data-stu-id="d5783-122">Add a **connectionString** variable and use it toocreate a **DeviceClient** instance.</span></span> <span data-ttu-id="d5783-123">取代**{裝置連接字串}** hello 裝置連接字串中 hello 產生*建立裝置身分識別*> 一節：</span><span class="sxs-lookup"><span data-stu-id="d5783-123">Replace **{device connection string}** with hello device connection string you generated in hello *Create a device identity* section:</span></span>
   
    ```
    var connectionString = '{device connection string}';
    var client = DeviceClient.fromConnectionString(connectionString, Mqtt);
    ```
6. <span data-ttu-id="d5783-124">加入下列函式 tooimplement hello 直接方法 hello 裝置上的 hello:</span><span class="sxs-lookup"><span data-stu-id="d5783-124">Add hello following function tooimplement hello direct method on hello device:</span></span>
   
    ```
    function onWriteLine(request, response) {
        console.log(request.payload);
   
        response.send(200, 'Input was written toolog.', function(err) {
            if(err) {
                console.error('An error occurred when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.' );
            }
        });
    }
    ```
7. <span data-ttu-id="d5783-125">開啟 hello 連接 tooyour IoT 中樞，並初始化 hello 方法接聽程式：</span><span class="sxs-lookup"><span data-stu-id="d5783-125">Open hello connection tooyour IoT hub and initialize hello method listener:</span></span>
   
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
8. <span data-ttu-id="d5783-126">儲存並關閉 hello **SimulatedDevice.js**檔案。</span><span class="sxs-lookup"><span data-stu-id="d5783-126">Save and close hello **SimulatedDevice.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="d5783-127">簡單 tookeep 方面，本教學課程未實作任何重試原則。</span><span class="sxs-lookup"><span data-stu-id="d5783-127">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="d5783-128">在實際執行程式碼，您應該實作重試原則 （例如連線重試），做為建議 hello MSDN 文件中[暫時性錯誤處理][lnk-transient-faults]。</span><span class="sxs-lookup"><span data-stu-id="d5783-128">In production code, you should implement retry policies (such as connection retry), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="call-a-direct-method-on-a-device"></a><span data-ttu-id="d5783-129">在裝置上呼叫直接方法</span><span class="sxs-lookup"><span data-stu-id="d5783-129">Call a direct method on a device</span></span>
<span data-ttu-id="d5783-130">在本節中，您可以建立.NET 主控台應用程式會呼叫 hello 模擬的裝置應用程式中的方法，並顯示 hello 回應。</span><span class="sxs-lookup"><span data-stu-id="d5783-130">In this section, you create a .NET console app that calls a method in hello simulated device app and then displays hello response.</span></span>

1. <span data-ttu-id="d5783-131">在 Visual Studio 中，將 Visual C# Windows 傳統桌面專案 toohello 目前方案使用 hello**主控台應用程式**專案範本。</span><span class="sxs-lookup"><span data-stu-id="d5783-131">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution by using hello **Console Application** project template.</span></span> <span data-ttu-id="d5783-132">請確定 hello.NET Framework 版本 4.5.1 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="d5783-132">Make sure hello .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="d5783-133">名稱 hello 專案**CallMethodOnDevice**。</span><span class="sxs-lookup"><span data-stu-id="d5783-133">Name hello project **CallMethodOnDevice**.</span></span>
   
    ![新的 Visual C# Windows 傳統桌面專案][10]
2. <span data-ttu-id="d5783-135">在 [方案總管] 中，以滑鼠右鍵按一下 hello **CallMethodOnDevice**專案，然後再按一下**管理 NuGet 封裝...**.</span><span class="sxs-lookup"><span data-stu-id="d5783-135">In Solution Explorer, right-click hello **CallMethodOnDevice** project, and then click **Manage NuGet Packages...**.</span></span>
3. <span data-ttu-id="d5783-136">在 hello **NuGet 套件管理員**視窗中，選取**瀏覽**，搜尋**microsoft.azure.devices**，選取**安裝**tooinstallhello **Microsoft.Azure.Devices**封裝，並接受使用規定 hello。</span><span class="sxs-lookup"><span data-stu-id="d5783-136">In hello **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** tooinstall hello **Microsoft.Azure.Devices** package, and accept hello terms of use.</span></span> <span data-ttu-id="d5783-137">此程序下載、 安裝，並新增參考 toohello [Azure IoT 服務 SDK] [ lnk-nuget-service-sdk] NuGet 封裝和其相依性。</span><span class="sxs-lookup"><span data-stu-id="d5783-137">This procedure downloads, installs, and adds a reference toohello [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![NuGet 封裝管理員視窗][11]

4. <span data-ttu-id="d5783-139">新增下列 hello`using`在 hello hello 最上方的陳述式**Program.cs**檔案：</span><span class="sxs-lookup"><span data-stu-id="d5783-139">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using System.Threading.Tasks;
        using Microsoft.Azure.Devices;
5. <span data-ttu-id="d5783-140">新增下列欄位 toohello hello**程式**類別。</span><span class="sxs-lookup"><span data-stu-id="d5783-140">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="d5783-141">取代 hello hello 中樞在 hello 上一節中所建立的 IoT 中樞連接字串中的 hello 預留位置的值。</span><span class="sxs-lookup"><span data-stu-id="d5783-141">Replace hello placeholder value with hello IoT Hub connection string for hello hub that you created in hello previous section.</span></span>
   
        static ServiceClient serviceClient;
        static string connectionString = "{iot hub connection string}";
6. <span data-ttu-id="d5783-142">新增下列方法 toohello hello**程式**類別：</span><span class="sxs-lookup"><span data-stu-id="d5783-142">Add hello following method toohello **Program** class:</span></span>
   
        private static async Task InvokeMethod()
        {
            var methodInvocation = new CloudToDeviceMethod("writeLine") { ResponseTimeout = TimeSpan.FromSeconds(30) };
            methodInvocation.SetPayloadJson("'a line toobe written'");

            var response = await serviceClient.InvokeDeviceMethodAsync("myDeviceId", methodInvocation);

            Console.WriteLine("Response status: {0}, payload:", response.Status);
            Console.WriteLine(response.GetPayloadAsJson());
        }
   
    <span data-ttu-id="d5783-143">這個方法會叫用具有名稱的直接方法`writeLine`上 hello`myDeviceId`裝置。</span><span class="sxs-lookup"><span data-stu-id="d5783-143">This method invokes a direct method with name `writeLine` on hello `myDeviceId` device.</span></span> <span data-ttu-id="d5783-144">然後，它會寫入 hello 回應 hello 裝置 hello 主控台上所提供。</span><span class="sxs-lookup"><span data-stu-id="d5783-144">Then, it writes hello response provided by hello device on hello console.</span></span> <span data-ttu-id="d5783-145">請注意如何可能 toospecify hello 裝置 toorespond 的逾時值。</span><span class="sxs-lookup"><span data-stu-id="d5783-145">Note how it is possible toospecify a timeout value for hello device toorespond.</span></span>
7. <span data-ttu-id="d5783-146">最後，加入下列行 toohello hello **Main**方法：</span><span class="sxs-lookup"><span data-stu-id="d5783-146">Finally, add hello following lines toohello **Main** method:</span></span>
   
        serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
        InvokeMethod().Wait();
        Console.WriteLine("Press Enter tooexit.");
        Console.ReadLine();

## <a name="run-hello-applications"></a><span data-ttu-id="d5783-147">執行 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="d5783-147">Run hello applications</span></span>
<span data-ttu-id="d5783-148">現在您已經準備就緒 toorun hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d5783-148">You are now ready toorun hello applications.</span></span>

1. <span data-ttu-id="d5783-149">在 hello Visual Studio 方案總管]，以滑鼠右鍵按一下您的方案，然後按一下**設定啟始專案...**.選取**單一啟始專案**，然後選取 [hello **CallMethodOnDevice** hello 下拉式功能表中的專案。</span><span class="sxs-lookup"><span data-stu-id="d5783-149">In hello Visual Studio Solution Explorer, right-click your solution, and then click **Set StartUp Projects...**. Select **Single startup project**, and then select hello **CallMethodOnDevice** project in hello dropdown menu.</span></span>

2. <span data-ttu-id="d5783-150">在命令提示字元中 hello **simulateddevice**資料夾中，執行下列命令 toostart 接聽從 IoT 中樞的方法呼叫的 hello:</span><span class="sxs-lookup"><span data-stu-id="d5783-150">At a command prompt in hello **simulateddevice** folder, run hello following command toostart listening for method calls from your IoT Hub:</span></span>
   
    ```
    node SimulatedDevice.js
    ```
   <span data-ttu-id="d5783-151">等候 hello 模擬裝置 tooopen:![][7]</span><span class="sxs-lookup"><span data-stu-id="d5783-151">Wait for hello simulated device tooopen:  ![][7]</span></span>
3. <span data-ttu-id="d5783-152">現在該 hello 裝置連線，並等候方法叫用時，執行 hello.NET **CallMethodOnDevice** hello 模擬的裝置應用程式中的應用程式 tooinvoke hello 方法。</span><span class="sxs-lookup"><span data-stu-id="d5783-152">Now that hello device is connected and waiting for method invocations, run hello .NET **CallMethodOnDevice** app tooinvoke hello method in hello simulated device app.</span></span> <span data-ttu-id="d5783-153">您應該會看到寫入 hello 主控台中的 hello 裝置回應。</span><span class="sxs-lookup"><span data-stu-id="d5783-153">You should see hello device response written in hello console.</span></span>
   
    ![][8]
4. <span data-ttu-id="d5783-154">hello 裝置然後反應 toohello 方法列印此訊息：</span><span class="sxs-lookup"><span data-stu-id="d5783-154">hello device then reacts toohello method by printing this message:</span></span>
   
    ![][9]

## <a name="next-steps"></a><span data-ttu-id="d5783-155">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d5783-155">Next steps</span></span>
<span data-ttu-id="d5783-156">在本教學課程中，您在 hello Azure 入口網站中設定新的 IoT 中樞，並接著 hello IoT 中樞的身分識別登錄中建立裝置身分識別。</span><span class="sxs-lookup"><span data-stu-id="d5783-156">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="d5783-157">您已經使用此裝置身分識別 tooenable hello 模擬裝置的應用程式 tooreact toomethods hello 雲端所叫用。</span><span class="sxs-lookup"><span data-stu-id="d5783-157">You used this device identity tooenable hello simulated device app tooreact toomethods invoked by hello cloud.</span></span> <span data-ttu-id="d5783-158">您也會建立叫用 hello 裝置上的方法，並會顯示 hello 回應 hello 裝置的應用程式。</span><span class="sxs-lookup"><span data-stu-id="d5783-158">You also created an app that invokes methods on hello device and displays hello response from hello device.</span></span> 

<span data-ttu-id="d5783-159">使用者入門 toocontinue tooexplore IoT 中樞與其他 IoT 案例，請參閱：</span><span class="sxs-lookup"><span data-stu-id="d5783-159">toocontinue getting started with IoT Hub and tooexplore other IoT scenarios, see:</span></span>

* <span data-ttu-id="d5783-160">[IoT 中心入門]</span><span class="sxs-lookup"><span data-stu-id="d5783-160">[Get started with IoT Hub]</span></span>
* <span data-ttu-id="d5783-161">[排程多個裝置上的作業][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="d5783-161">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="d5783-162">toolearn 如何 tooextend IoT 解決方案和排程方法呼叫上多個裝置，請參閱 hello[排程和廣播的工作][ lnk-tutorial-jobs]教學課程。</span><span class="sxs-lookup"><span data-stu-id="d5783-162">toolearn how tooextend your IoT solution and schedule method calls on multiple devices, see hello [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

<!-- Images. -->
[7]: ./media/iot-hub-csharp-node-direct-methods/run-simulated-device.png
[8]: ./media/iot-hub-csharp-node-direct-methods/netserviceapp.png
[9]: ./media/iot-hub-csharp-node-direct-methods/methods-output.png

[10]: ./media/iot-hub-csharp-node-direct-methods/direct-methods-csharp1.png
[11]: ./media/iot-hub-csharp-node-direct-methods/direct-methods-csharp2.png

<!-- Links -->
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal]: https://portal.azure.com/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-devguide-methods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md

[Send Cloud-to-Device messages with IoT Hub]: iot-hub-csharp-csharp-c2d.md
[Process Device-to-Cloud messages]: iot-hub-csharp-csharp-process-d2c.md
[IoT 中心入門]: iot-hub-node-node-getstarted.md
