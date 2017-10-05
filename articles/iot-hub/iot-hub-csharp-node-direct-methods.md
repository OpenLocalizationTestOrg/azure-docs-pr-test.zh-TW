---
title: "使用 Azure IoT 中樞直接方法 (.NET/Node) | Microsoft Docs"
description: "如何使用 Azure IoT 中樞直接方法。 您可以使用適用於 Node.js 的 Azure IoT 裝置 SDK，實作模擬裝置應用程式 (包含直接方法)，也可以使用適用於 .NET 的 Azure IoT 服務 SDK，實作服務應用程式 (叫用直接方法)。"
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
ms.openlocfilehash: ad705789a153381e21b2ccb05d4e0c17f78671fd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-direct-methods-netnode"></a><span data-ttu-id="ee651-104">使用直接方法 (.NET/Node)</span><span class="sxs-lookup"><span data-stu-id="ee651-104">Use direct methods (.NET/Node)</span></span>
[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

<span data-ttu-id="ee651-105">在本教學課程中，我們即將開發 .NET 和 Node.js 主控台應用程式：</span><span class="sxs-lookup"><span data-stu-id="ee651-105">In this tutorial, we are going to develop a .NET and a Node.js console app:</span></span>

* <span data-ttu-id="ee651-106">**CallMethodOnDevice.js**，這是 NET 後端應用程式，可在模擬裝置應用程式中呼叫方法，並顯示回應。</span><span class="sxs-lookup"><span data-stu-id="ee651-106">**CallMethodOnDevice.sln**, a .NET back-end app, which calls a method in the simulated device app and displays the response.</span></span>
* <span data-ttu-id="ee651-107">**TwinSimulatedDevice.js** 是可模擬裝置的 Node.js 應用程式，而此裝置會以稍早建立的裝置身分識別連線至您的 IoT 中樞，並回應雲端所呼叫的方法。</span><span class="sxs-lookup"><span data-stu-id="ee651-107">**SimulatedDevice.js**, a Node.js app, which simulates a device connecting to your IoT hub with the device identity created earlier, and responds to the method called by the cloud.</span></span>

> [!NOTE]
> <span data-ttu-id="ee651-108">[Azure IoT SDK][lnk-hub-sdks] 一文提供 Azure IoT SDK (可讓您同時建置在裝置與您的解決方案後端執行的兩個應用程式) 的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="ee651-108">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both applications to run on devices and your solution back end.</span></span>
> 
> 

<span data-ttu-id="ee651-109">若要完成本教學課程，您需要：</span><span class="sxs-lookup"><span data-stu-id="ee651-109">To complete this tutorial, you need:</span></span>

* <span data-ttu-id="ee651-110">Visual Studio 2015 或 Visual Studio 2017。</span><span class="sxs-lookup"><span data-stu-id="ee651-110">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="ee651-111">Node.js 0.10.x 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="ee651-111">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="ee651-112">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="ee651-112">An active Azure account.</span></span> <span data-ttu-id="ee651-113">(如果您沒有帳戶，只需要幾分鐘的時間就可以建立[免費帳戶][lnk-free-trial]。)</span><span class="sxs-lookup"><span data-stu-id="ee651-113">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="ee651-114">建立模擬裝置應用程式</span><span class="sxs-lookup"><span data-stu-id="ee651-114">Create a simulated device app</span></span>
<span data-ttu-id="ee651-115">在本節中，您建立 Node.js 主控台應用程式，回應解決方案後端所呼叫的方法。</span><span class="sxs-lookup"><span data-stu-id="ee651-115">In this section, you create a Node.js console app that responds to a method called by the solution back end.</span></span>

1. <span data-ttu-id="ee651-116">建立稱為 **simulateddevice**的新的空資料夾。</span><span class="sxs-lookup"><span data-stu-id="ee651-116">Create a new empty folder called **simulateddevice**.</span></span> <span data-ttu-id="ee651-117">在 **simulateddevice** 資料夾中，於命令提示字元使用下列命令建立 package.json 檔案。</span><span class="sxs-lookup"><span data-stu-id="ee651-117">In the **simulateddevice** folder, create a package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="ee651-118">接受所有預設值：</span><span class="sxs-lookup"><span data-stu-id="ee651-118">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="ee651-119">在 **simulateddevice** 資料夾中，於命令提示字元執行下列命令以安裝 **azure-iot-device** 和 **azure-iot-device-mqtt** 套件：</span><span class="sxs-lookup"><span data-stu-id="ee651-119">At your command prompt in the **simulateddevice** folder, run the following command to install the **azure-iot-device** and **azure-iot-device-mqtt** packages:</span></span>
   
    ```
        npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="ee651-120">使用文字編輯器，在 **simulateddevice** 資料夾中建立檔案並將它命名為 **SimulatedDevice.js**。</span><span class="sxs-lookup"><span data-stu-id="ee651-120">Using a text editor, create a file in the **simulateddevice** folder and name it **SimulatedDevice.js**.</span></span>
4. <span data-ttu-id="ee651-121">在 **SimulatedDevice.js** 檔案開頭新增下列 `require` 陳述式：</span><span class="sxs-lookup"><span data-stu-id="ee651-121">Add the following `require` statements at the start of the **SimulatedDevice.js** file:</span></span>
   
    ```
    'use strict';
   
    var Mqtt = require('azure-iot-device-mqtt').Mqtt;
    var DeviceClient = require('azure-iot-device').Client;
    ```
5. <span data-ttu-id="ee651-122">新增 **connectionString** 變數，並用它來建立 **DeviceClient** 執行個體。</span><span class="sxs-lookup"><span data-stu-id="ee651-122">Add a **connectionString** variable and use it to create a **DeviceClient** instance.</span></span> <span data-ttu-id="ee651-123">將 **{device connection string}** 取代為您在*建立裝置身分識別*一節中產生的連接字串：</span><span class="sxs-lookup"><span data-stu-id="ee651-123">Replace **{device connection string}** with the device connection string you generated in the *Create a device identity* section:</span></span>
   
    ```
    var connectionString = '{device connection string}';
    var client = DeviceClient.fromConnectionString(connectionString, Mqtt);
    ```
6. <span data-ttu-id="ee651-124">新增下列函式以在裝置上實作直接方法：</span><span class="sxs-lookup"><span data-stu-id="ee651-124">Add the following function to implement the direct method on the device:</span></span>
   
    ```
    function onWriteLine(request, response) {
        console.log(request.payload);
   
        response.send(200, 'Input was written to log.', function(err) {
            if(err) {
                console.error('An error occurred when sending a method response:\n' + err.toString());
            } else {
                console.log('Response to method \'' + request.methodName + '\' sent successfully.' );
            }
        });
    }
    ```
7. <span data-ttu-id="ee651-125">開啟 IoT 中樞的連線並初始化方法接聽程式︰</span><span class="sxs-lookup"><span data-stu-id="ee651-125">Open the connection to your IoT hub and initialize the method listener:</span></span>
   
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
8. <span data-ttu-id="ee651-126">儲存並關閉 **SimulatedDevice.js** 檔案。</span><span class="sxs-lookup"><span data-stu-id="ee651-126">Save and close the **SimulatedDevice.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="ee651-127">為了簡單起見，本教學課程不會實作任何重試原則。</span><span class="sxs-lookup"><span data-stu-id="ee651-127">To keep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="ee651-128">在生產環境程式碼中，您應該如 MSDN 文章[暫時性錯誤處理][lnk-transient-faults]所建議，實作重試原則 (例如連接重試)。</span><span class="sxs-lookup"><span data-stu-id="ee651-128">In production code, you should implement retry policies (such as connection retry), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="call-a-direct-method-on-a-device"></a><span data-ttu-id="ee651-129">在裝置上呼叫直接方法</span><span class="sxs-lookup"><span data-stu-id="ee651-129">Call a direct method on a device</span></span>
<span data-ttu-id="ee651-130">在本節中，您會建立 .NET 主控台應用程式，以在模擬裝置應用程式中呼叫方法，然後顯示回應。</span><span class="sxs-lookup"><span data-stu-id="ee651-130">In this section, you create a .NET console app that calls a method in the simulated device app and then displays the response.</span></span>

1. <span data-ttu-id="ee651-131">在 Visual Studio 中，使用 [主控台應用程式] 專案範本，將 Visual C# Windows 傳統桌面專案新增至目前的方案。</span><span class="sxs-lookup"><span data-stu-id="ee651-131">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution by using the **Console Application** project template.</span></span> <span data-ttu-id="ee651-132">確定 .NET Framework 為 4.5.1 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="ee651-132">Make sure the .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="ee651-133">將專案命名為 **CallMethodOnDevice**。</span><span class="sxs-lookup"><span data-stu-id="ee651-133">Name the project **CallMethodOnDevice**.</span></span>
   
    ![新的 Visual C# Windows 傳統桌面專案][10]
2. <span data-ttu-id="ee651-135">在 [方案總管] 中，以滑鼠右鍵按一下 **CallMethodOnDevice** 專案，然後按一下 [管理 NuGet 套件...]。</span><span class="sxs-lookup"><span data-stu-id="ee651-135">In Solution Explorer, right-click the **CallMethodOnDevice** project, and then click **Manage NuGet Packages...**.</span></span>
3. <span data-ttu-id="ee651-136">在 [Nuget 套件管理員] 視窗中選取 [瀏覽]、搜尋 **microsoft.azure.devices**、選取 [安裝] 以安裝 **Microsoft.Azure.Devices** 套件，並接受使用規定。</span><span class="sxs-lookup"><span data-stu-id="ee651-136">In the **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** to install the **Microsoft.Azure.Devices** package, and accept the terms of use.</span></span> <span data-ttu-id="ee651-137">此程序會下載及安裝 [Azure IoT 服務 SDK][lnk-nuget-service-sdk] NuGet 套件與其相依項目，並新增對它的參考。</span><span class="sxs-lookup"><span data-stu-id="ee651-137">This procedure downloads, installs, and adds a reference to the [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![NuGet 套件管理員視窗][11]

4. <span data-ttu-id="ee651-139">在 **Program.cs** 檔案開頭處新增下列 `using` 陳述式：</span><span class="sxs-lookup"><span data-stu-id="ee651-139">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
        using System.Threading.Tasks;
        using Microsoft.Azure.Devices;
5. <span data-ttu-id="ee651-140">將下列欄位新增到 **Program** 類別。</span><span class="sxs-lookup"><span data-stu-id="ee651-140">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="ee651-141">將預留位置的值替換為您在上一節中為中樞所建立的 IoT 中樞連接字串。</span><span class="sxs-lookup"><span data-stu-id="ee651-141">Replace the placeholder value with the IoT Hub connection string for the hub that you created in the previous section.</span></span>
   
        static ServiceClient serviceClient;
        static string connectionString = "{iot hub connection string}";
6. <span data-ttu-id="ee651-142">將下列方法加入至 **Program** 類別：</span><span class="sxs-lookup"><span data-stu-id="ee651-142">Add the following method to the **Program** class:</span></span>
   
        private static async Task InvokeMethod()
        {
            var methodInvocation = new CloudToDeviceMethod("writeLine") { ResponseTimeout = TimeSpan.FromSeconds(30) };
            methodInvocation.SetPayloadJson("'a line to be written'");

            var response = await serviceClient.InvokeDeviceMethodAsync("myDeviceId", methodInvocation);

            Console.WriteLine("Response status: {0}, payload:", response.Status);
            Console.WriteLine(response.GetPayloadAsJson());
        }
   
    <span data-ttu-id="ee651-143">此方法會在 `myDeviceId` 裝置上叫用名稱為 `writeLine` 的直接方法。</span><span class="sxs-lookup"><span data-stu-id="ee651-143">This method invokes a direct method with name `writeLine` on the `myDeviceId` device.</span></span> <span data-ttu-id="ee651-144">然後，它會在主控台上寫入裝置所提供的回應。</span><span class="sxs-lookup"><span data-stu-id="ee651-144">Then, it writes the response provided by the device on the console.</span></span> <span data-ttu-id="ee651-145">請注意，可以針對要回應的裝置指定逾時值。</span><span class="sxs-lookup"><span data-stu-id="ee651-145">Note how it is possible to specify a timeout value for the device to respond.</span></span>
7. <span data-ttu-id="ee651-146">最後，將下列幾行加入至 **Main** 方法：</span><span class="sxs-lookup"><span data-stu-id="ee651-146">Finally, add the following lines to the **Main** method:</span></span>
   
        serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
        InvokeMethod().Wait();
        Console.WriteLine("Press Enter to exit.");
        Console.ReadLine();

## <a name="run-the-applications"></a><span data-ttu-id="ee651-147">執行應用程式</span><span class="sxs-lookup"><span data-stu-id="ee651-147">Run the applications</span></span>
<span data-ttu-id="ee651-148">現在您已經準備好執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="ee651-148">You are now ready to run the applications.</span></span>

1. <span data-ttu-id="ee651-149">在 Visual Studio 的 [方案總管] 中，以滑鼠右鍵按一下您的方案，然後按一下 [設定啟始專案...]。</span><span class="sxs-lookup"><span data-stu-id="ee651-149">In the Visual Studio Solution Explorer, right-click your solution, and then click **Set StartUp Projects...**.</span></span> <span data-ttu-id="ee651-150">選取 [單一啟始專案]，然後選取下拉式功能表中的 **CallMethodOnDevice** 專案。</span><span class="sxs-lookup"><span data-stu-id="ee651-150">Select **Single startup project**, and then select the **CallMethodOnDevice** project in the dropdown menu.</span></span>

2. <span data-ttu-id="ee651-151">在 **simulateddevice** 資料夾的命令提示字元中，執行下列命令以開始接聽來自您的 IoT 中樞的方法呼叫：</span><span class="sxs-lookup"><span data-stu-id="ee651-151">At a command prompt in the **simulateddevice** folder, run the following command to start listening for method calls from your IoT Hub:</span></span>
   
    ```
    node SimulatedDevice.js
    ```
   <span data-ttu-id="ee651-152">等候模擬裝置開啟︰![][7]</span><span class="sxs-lookup"><span data-stu-id="ee651-152">Wait for the simulated device to open:  ![][7]</span></span>
3. <span data-ttu-id="ee651-153">裝置現在已連接並等候方法引動過程，請執行 .NET **CallMethodOnDevice** 應用程式，以在模擬裝置應用程式中叫用方法。</span><span class="sxs-lookup"><span data-stu-id="ee651-153">Now that the device is connected and waiting for method invocations, run the .NET **CallMethodOnDevice** app to invoke the method in the simulated device app.</span></span> <span data-ttu-id="ee651-154">您應會看到在主控台中寫入的裝置回應。</span><span class="sxs-lookup"><span data-stu-id="ee651-154">You should see the device response written in the console.</span></span>
   
    ![][8]
4. <span data-ttu-id="ee651-155">此裝置接著藉由列印此訊息來回應此方法︰</span><span class="sxs-lookup"><span data-stu-id="ee651-155">The device then reacts to the method by printing this message:</span></span>
   
    ![][9]

## <a name="next-steps"></a><span data-ttu-id="ee651-156">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ee651-156">Next steps</span></span>
<span data-ttu-id="ee651-157">在此教學課程中，您在 Azure 入口網站中設定了新的 IoT 中樞，然後在 IoT 中樞的身分識別登錄中建立了裝置身分識別。</span><span class="sxs-lookup"><span data-stu-id="ee651-157">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="ee651-158">您會將此裝置識別用於啟用模擬的裝置應用程式，以將雲端所叫用的方法進行反應。</span><span class="sxs-lookup"><span data-stu-id="ee651-158">You used this device identity to enable the simulated device app to react to methods invoked by the cloud.</span></span> <span data-ttu-id="ee651-159">您也會建立應用程式，在裝置上叫用方法，並且顯示來自裝置的回應。</span><span class="sxs-lookup"><span data-stu-id="ee651-159">You also created an app that invokes methods on the device and displays the response from the device.</span></span> 

<span data-ttu-id="ee651-160">若要繼續開始使用 IoT 中樞並瀏覽其他 IoT 案例，請參閱︰</span><span class="sxs-lookup"><span data-stu-id="ee651-160">To continue getting started with IoT Hub and to explore other IoT scenarios, see:</span></span>

* <span data-ttu-id="ee651-161">[IoT 中樞入門]</span><span class="sxs-lookup"><span data-stu-id="ee651-161">[Get started with IoT Hub]</span></span>
* <span data-ttu-id="ee651-162">[排程多個裝置上的作業][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="ee651-162">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="ee651-163">若要了解如何擴充您的 IoT 解決方案以及在多個裝置上排程方法呼叫，請參閱[排程及廣播作業][lnk-tutorial-jobs]教學課程。</span><span class="sxs-lookup"><span data-stu-id="ee651-163">To learn how to extend your IoT solution and schedule method calls on multiple devices, see the [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

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
<span data-ttu-id="ee651-164">[IoT 中樞入門]: iot-hub-node-node-getstarted.md</span><span class="sxs-lookup"><span data-stu-id="ee651-164">[Get started with IoT Hub]: iot-hub-node-node-getstarted.md</span></span>
