---
title: "Azure IoT 中樞 aaaUse 直接方法 (.NET/.NET) |Microsoft 文件"
description: "如何 toouse Azure IoT 中樞直接的方法。 您可以使用 hello Azure IoT 裝置 SDK for.NET tooimplement 模擬的裝置應用程式，其中包含直接的方法和 hello Azure IoT 服務 SDK for.NET tooimplement hello 直接的方法會叫用的服務應用程式。"
services: iot-hub
documentationcenter: 
author: dsk-2015
manager: timlt
editor: 
ms.assetid: ab035b8e-bff8-4e12-9536-f31d6b6fe425
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2017
ms.author: dkshir
ms.openlocfilehash: d4fa093a99558ec6faf294c2583a14a722b9ac03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-direct-methods-netnet"></a><span data-ttu-id="5e7c4-104">使用直接方法 (.NET/.NET)</span><span class="sxs-lookup"><span data-stu-id="5e7c4-104">Use direct methods (.NET/.NET)</span></span>
[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

<span data-ttu-id="5e7c4-105">在本教學課程中，我們會持續 toodevelop 兩個.NET 主控台應用程式：</span><span class="sxs-lookup"><span data-stu-id="5e7c4-105">In this tutorial, we are going toodevelop two .NET console apps:</span></span>

* <span data-ttu-id="5e7c4-106">**CallMethodOnDevice**後, 端應用程式，會呼叫 hello 模擬的裝置應用程式中的方法，並顯示 hello 回應。</span><span class="sxs-lookup"><span data-stu-id="5e7c4-106">**CallMethodOnDevice**, a back-end app, which calls a method in hello simulated device app and displays hello response.</span></span>
* <span data-ttu-id="5e7c4-107">**SimulateDeviceMethods**，主控台應用程式的模擬連接 tooyour IoT 中樞與 hello 稍早建立的裝置身分識別的裝置，以及回應 hello 雲端呼叫 toohello 方法。</span><span class="sxs-lookup"><span data-stu-id="5e7c4-107">**SimulateDeviceMethods**, a console app which simulates a device connecting tooyour IoT hub with hello device identity created earlier, and responds toohello method called by hello cloud.</span></span>

> [!NOTE]
> <span data-ttu-id="5e7c4-108">hello 文章[Azure IoT Sdk] [ lnk-hub-sdks]提供 hello Azure IoT Sdk 的相關資訊，您可以使用 toobuild 這兩個應用程式 toorun 裝置和您的方案後端上。</span><span class="sxs-lookup"><span data-stu-id="5e7c4-108">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both applications toorun on devices and your solution back end.</span></span>
> 
> 

<span data-ttu-id="5e7c4-109">toocomplete 本教學課程中，您需要：</span><span class="sxs-lookup"><span data-stu-id="5e7c4-109">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="5e7c4-110">Visual Studio 2015 或 Visual Studio 2017。</span><span class="sxs-lookup"><span data-stu-id="5e7c4-110">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="5e7c4-111">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="5e7c4-111">An active Azure account.</span></span> <span data-ttu-id="5e7c4-112">(如果您沒有帳戶，只需要幾分鐘的時間就可以建立[免費帳戶][lnk-free-trial]。)</span><span class="sxs-lookup"><span data-stu-id="5e7c4-112">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

<span data-ttu-id="5e7c4-113">如果您想 toocreate hello 裝置身分識別以程式設計方式相反地，讀取 hello 對應的章節 hello[連接您使用適用於.NET 的模擬的裝置 tooyour IoT 中樞][ lnk-device-identity-csharp]發行項。</span><span class="sxs-lookup"><span data-stu-id="5e7c4-113">If you want toocreate hello device identity programmatically instead, read hello corresponding section in hello [Connect your simulated device tooyour IoT hub using .NET][lnk-device-identity-csharp] article.</span></span>


## <a name="create-a-simulated-device-app"></a><span data-ttu-id="5e7c4-114">建立模擬裝置應用程式</span><span class="sxs-lookup"><span data-stu-id="5e7c4-114">Create a simulated device app</span></span>
<span data-ttu-id="5e7c4-115">在本節中，您可以建立回應 hello 方案回呼叫端的 tooa 方法 .NET 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="5e7c4-115">In this section, you create a .NET console app that responds tooa method called by hello solution back end.</span></span>

1. <span data-ttu-id="5e7c4-116">在 Visual Studio 中，將 Visual C# Windows 傳統桌面專案 toohello 目前方案使用 hello**主控台應用程式**專案範本。</span><span class="sxs-lookup"><span data-stu-id="5e7c4-116">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution by using hello **Console Application** project template.</span></span> <span data-ttu-id="5e7c4-117">名稱 hello 專案**SimulateDeviceMethods**。</span><span class="sxs-lookup"><span data-stu-id="5e7c4-117">Name hello project **SimulateDeviceMethods**.</span></span>
   
    ![新的 Visual C# Windows 傳統裝置應用程式][img-createdeviceapp]
    
1. <span data-ttu-id="5e7c4-119">在 [方案總管] 中，以滑鼠右鍵按一下 hello **SimulateDeviceMethods**專案，然後再按一下**管理 NuGet 封裝...**.</span><span class="sxs-lookup"><span data-stu-id="5e7c4-119">In Solution Explorer, right-click hello **SimulateDeviceMethods** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="5e7c4-120">在 hello **NuGet 套件管理員**視窗中，選取**瀏覽**並搜尋**microsoft.azure.devices.client**。</span><span class="sxs-lookup"><span data-stu-id="5e7c4-120">In hello **NuGet Package Manager** window, select **Browse** and search for **microsoft.azure.devices.client**.</span></span> <span data-ttu-id="5e7c4-121">選取**安裝**tooinstall hello **Microsoft.Azure.Devices.Client**封裝，並接受使用規定 hello。</span><span class="sxs-lookup"><span data-stu-id="5e7c4-121">Select **Install** tooinstall hello **Microsoft.Azure.Devices.Client** package, and accept hello terms of use.</span></span> <span data-ttu-id="5e7c4-122">此程序下載、 安裝，並新增參考 toohello [Azure IoT 裝置 SDK] [ lnk-nuget-client-sdk] NuGet 封裝和其相依性。</span><span class="sxs-lookup"><span data-stu-id="5e7c4-122">This procedure downloads, installs, and adds a reference toohello [Azure IoT device SDK][lnk-nuget-client-sdk] NuGet package and its dependencies.</span></span>
   
    ![NuGet 套件管理員視窗用戶端應用程式][img-clientnuget]
1. <span data-ttu-id="5e7c4-124">新增下列 hello`using`在 hello hello 最上方的陳述式**Program.cs**檔案：</span><span class="sxs-lookup"><span data-stu-id="5e7c4-124">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices.Client;
        using Microsoft.Azure.Devices.Shared;

1. <span data-ttu-id="5e7c4-125">新增下列欄位 toohello hello**程式**類別。</span><span class="sxs-lookup"><span data-stu-id="5e7c4-125">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="5e7c4-126">取代您記下 hello 前一節中的 hello 裝置連接字串中的 hello 預留位置的值。</span><span class="sxs-lookup"><span data-stu-id="5e7c4-126">Replace hello placeholder value with hello device connection string that you noted in hello previous section.</span></span>
   
        static string DeviceConnectionString = "HostName=<yourIotHubName>.azure-devices.net;DeviceId=<yourIotDeviceName>;SharedAccessKey=<yourIotDeviceAccessKey>";
        static DeviceClient Client = null;

1. <span data-ttu-id="5e7c4-127">新增下列 tooimplement hello 直接方法 hello 裝置上的 hello:</span><span class="sxs-lookup"><span data-stu-id="5e7c4-127">Add hello following tooimplement hello direct method on hello device:</span></span>

        static Task<MethodResponse> WriteLineToConsole(MethodRequest methodRequest, object userContext)
        {
            Console.WriteLine();
            Console.WriteLine("\t{0}", methodRequest.DataAsJson);
            Console.WriteLine("\nReturning response for method {0}", methodRequest.Name);

            string result = "'Input was written toolog.'";
            return Task.FromResult(new MethodResponse(Encoding.UTF8.GetBytes(result), 200));
        }

1. <span data-ttu-id="5e7c4-128">最後，加入下列程式碼 toohello hello **Main**方法 tooopen hello 連接 tooyour IoT 中樞和初始化 hello 方法接聽程式：</span><span class="sxs-lookup"><span data-stu-id="5e7c4-128">Finally, add hello following code toohello **Main** method tooopen hello connection tooyour IoT hub and initialize hello method listener:</span></span>
   
        try
        {
            Console.WriteLine("Connecting toohub");
            Client = DeviceClient.CreateFromConnectionString(DeviceConnectionString, TransportType.Mqtt);

            // setup callback for "writeLine" method
            Client.SetMethodHandlerAsync("writeLine", WriteLineToConsole, null).Wait();
            Console.WriteLine("Waiting for direct method call\n Press enter tooexit.");
            Console.ReadLine();

            Console.WriteLine("Exiting...");

            // as a good practice, remove hello "writeLine" handler
            Client.SetMethodHandlerAsync("writeLine", null, null).Wait();
            Client.CloseAsync().Wait();
        }
        catch (Exception ex)
        {
            Console.WriteLine();
            Console.WriteLine("Error in sample: {0}", ex.Message);
        }
        
1. <span data-ttu-id="5e7c4-129">在 hello Visual Studio 方案總管]，以滑鼠右鍵按一下您的方案，然後按一下**設定啟始專案...**.選取**單一啟始專案**，然後選取 [hello **SimulateDeviceMethods** hello 下拉式功能表中的專案。</span><span class="sxs-lookup"><span data-stu-id="5e7c4-129">In hello Visual Studio Solution Explorer, right-click your solution, and then click **Set StartUp Projects...**. Select **Single startup project**, and then select hello **SimulateDeviceMethods** project in hello dropdown menu.</span></span>        

> [!NOTE]
> <span data-ttu-id="5e7c4-130">簡單 tookeep 方面，本教學課程未實作任何重試原則。</span><span class="sxs-lookup"><span data-stu-id="5e7c4-130">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="5e7c4-131">在實際執行程式碼，您應該實作重試原則 （例如連線重試），做為建議 hello MSDN 文件中[暫時性錯誤處理][lnk-transient-faults]。</span><span class="sxs-lookup"><span data-stu-id="5e7c4-131">In production code, you should implement retry policies (such as connection retry), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="call-a-direct-method-on-a-device"></a><span data-ttu-id="5e7c4-132">在裝置上呼叫直接方法</span><span class="sxs-lookup"><span data-stu-id="5e7c4-132">Call a direct method on a device</span></span>
<span data-ttu-id="5e7c4-133">在本節中，您可以建立.NET 主控台應用程式會呼叫 hello 模擬的裝置應用程式中的方法，並顯示 hello 回應。</span><span class="sxs-lookup"><span data-stu-id="5e7c4-133">In this section, you create a .NET console app that calls a method in hello simulated device app and then displays hello response.</span></span>

1. <span data-ttu-id="5e7c4-134">在 Visual Studio 中，將 Visual C# Windows 傳統桌面專案 toohello 目前方案使用 hello**主控台應用程式**專案範本。</span><span class="sxs-lookup"><span data-stu-id="5e7c4-134">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution by using hello **Console Application** project template.</span></span> <span data-ttu-id="5e7c4-135">請確定 hello.NET Framework 版本 4.5.1 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="5e7c4-135">Make sure hello .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="5e7c4-136">名稱 hello 專案**CallMethodOnDevice**。</span><span class="sxs-lookup"><span data-stu-id="5e7c4-136">Name hello project **CallMethodOnDevice**.</span></span>
   
    ![新的 Visual C# Windows 傳統桌面專案][img-createserviceapp]
2. <span data-ttu-id="5e7c4-138">在 [方案總管] 中，以滑鼠右鍵按一下 hello **CallMethodOnDevice**專案，然後再按一下**管理 NuGet 封裝...**.</span><span class="sxs-lookup"><span data-stu-id="5e7c4-138">In Solution Explorer, right-click hello **CallMethodOnDevice** project, and then click **Manage NuGet Packages...**.</span></span>
3. <span data-ttu-id="5e7c4-139">在 hello **NuGet 套件管理員**視窗中，選取**瀏覽**，搜尋**microsoft.azure.devices**，選取**安裝**tooinstallhello **Microsoft.Azure.Devices**封裝，並接受使用規定 hello。</span><span class="sxs-lookup"><span data-stu-id="5e7c4-139">In hello **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** tooinstall hello **Microsoft.Azure.Devices** package, and accept hello terms of use.</span></span> <span data-ttu-id="5e7c4-140">此程序下載、 安裝，並新增參考 toohello [Azure IoT 服務 SDK] [ lnk-nuget-service-sdk] NuGet 封裝和其相依性。</span><span class="sxs-lookup"><span data-stu-id="5e7c4-140">This procedure downloads, installs, and adds a reference toohello [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![NuGet 封裝管理員視窗][img-servicenuget]

4. <span data-ttu-id="5e7c4-142">新增下列 hello`using`在 hello hello 最上方的陳述式**Program.cs**檔案：</span><span class="sxs-lookup"><span data-stu-id="5e7c4-142">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using System.Threading.Tasks;
        using Microsoft.Azure.Devices;
5. <span data-ttu-id="5e7c4-143">新增下列欄位 toohello hello**程式**類別。</span><span class="sxs-lookup"><span data-stu-id="5e7c4-143">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="5e7c4-144">取代 hello hello 中樞在 hello 上一節中所建立的 IoT 中樞連接字串中的 hello 預留位置的值。</span><span class="sxs-lookup"><span data-stu-id="5e7c4-144">Replace hello placeholder value with hello IoT Hub connection string for hello hub that you created in hello previous section.</span></span>
   
        static ServiceClient serviceClient;
        static string connectionString = "{iot hub connection string}";
6. <span data-ttu-id="5e7c4-145">新增下列方法 toohello hello**程式**類別：</span><span class="sxs-lookup"><span data-stu-id="5e7c4-145">Add hello following method toohello **Program** class:</span></span>
   
        private static async Task InvokeMethod()
        {
            var methodInvocation = new CloudToDeviceMethod("writeLine") { ResponseTimeout = TimeSpan.FromSeconds(30) };
            methodInvocation.SetPayloadJson("'a line toobe written'");

            var response = await serviceClient.InvokeDeviceMethodAsync("myDeviceId", methodInvocation);

            Console.WriteLine("Response status: {0}, payload:", response.Status);
            Console.WriteLine(response.GetPayloadAsJson());
        }
   
    <span data-ttu-id="5e7c4-146">這個方法會叫用具有名稱的直接方法`writeLine`上 hello`myDeviceId`裝置。</span><span class="sxs-lookup"><span data-stu-id="5e7c4-146">This method invokes a direct method with name `writeLine` on hello `myDeviceId` device.</span></span> <span data-ttu-id="5e7c4-147">然後，它會寫入 hello 回應 hello 裝置 hello 主控台上所提供。</span><span class="sxs-lookup"><span data-stu-id="5e7c4-147">Then, it writes hello response provided by hello device on hello console.</span></span> <span data-ttu-id="5e7c4-148">請注意如何可能 toospecify hello 裝置 toorespond 的逾時值。</span><span class="sxs-lookup"><span data-stu-id="5e7c4-148">Note how it is possible toospecify a timeout value for hello device toorespond.</span></span>
7. <span data-ttu-id="5e7c4-149">最後，加入下列行 toohello hello **Main**方法：</span><span class="sxs-lookup"><span data-stu-id="5e7c4-149">Finally, add hello following lines toohello **Main** method:</span></span>
   
        serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
        InvokeMethod().Wait();
        Console.WriteLine("Press Enter tooexit.");
        Console.ReadLine();

1. <span data-ttu-id="5e7c4-150">在 hello Visual Studio 方案總管]，以滑鼠右鍵按一下您的方案，然後按一下**設定啟始專案...**.選取**單一啟始專案**，然後選取 [hello **CallMethodOnDevice** hello 下拉式功能表中的專案。</span><span class="sxs-lookup"><span data-stu-id="5e7c4-150">In hello Visual Studio Solution Explorer, right-click your solution, and then click **Set StartUp Projects...**. Select **Single startup project**, and then select hello **CallMethodOnDevice** project in hello dropdown menu.</span></span>

## <a name="run-hello-applications"></a><span data-ttu-id="5e7c4-151">執行 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="5e7c4-151">Run hello applications</span></span>
<span data-ttu-id="5e7c4-152">現在您已經準備就緒 toorun hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5e7c4-152">You are now ready toorun hello applications.</span></span>

1. <span data-ttu-id="5e7c4-153">執行 hello.NET 裝置的應用程式**SimulateDeviceMethods**。</span><span class="sxs-lookup"><span data-stu-id="5e7c4-153">Run hello .NET device app **SimulateDeviceMethods**.</span></span> <span data-ttu-id="5e7c4-154">它應該會開始接聽來自 IoT 中樞的方法呼叫：</span><span class="sxs-lookup"><span data-stu-id="5e7c4-154">It should start listening for method calls from your IoT Hub:</span></span> 

    ![裝置應用程式已執行][img-deviceapprun]
1. <span data-ttu-id="5e7c4-156">現在該 hello 裝置連線，並等候方法叫用時，執行 hello.NET **CallMethodOnDevice** hello 模擬的裝置應用程式中的應用程式 tooinvoke hello 方法。</span><span class="sxs-lookup"><span data-stu-id="5e7c4-156">Now that hello device is connected and waiting for method invocations, run hello .NET **CallMethodOnDevice** app tooinvoke hello method in hello simulated device app.</span></span> <span data-ttu-id="5e7c4-157">您應該會看到寫入 hello 主控台中的 hello 裝置回應。</span><span class="sxs-lookup"><span data-stu-id="5e7c4-157">You should see hello device response written in hello console.</span></span>
   
    ![裝置應用程式已執行][img-serviceapprun]
1. <span data-ttu-id="5e7c4-159">hello 裝置然後反應 toohello 方法列印此訊息：</span><span class="sxs-lookup"><span data-stu-id="5e7c4-159">hello device then reacts toohello method by printing this message:</span></span>
   
    ![直接在 hello 裝置上叫用的方法][img-directmethodinvoked]

## <a name="next-steps"></a><span data-ttu-id="5e7c4-161">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5e7c4-161">Next steps</span></span>
<span data-ttu-id="5e7c4-162">在本教學課程中，您在 hello Azure 入口網站中設定新的 IoT 中樞，並接著 hello IoT 中樞的身分識別登錄中建立裝置身分識別。</span><span class="sxs-lookup"><span data-stu-id="5e7c4-162">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="5e7c4-163">您已經使用此裝置身分識別 tooenable hello 模擬裝置的應用程式 tooreact toomethods hello 雲端所叫用。</span><span class="sxs-lookup"><span data-stu-id="5e7c4-163">You used this device identity tooenable hello simulated device app tooreact toomethods invoked by hello cloud.</span></span> <span data-ttu-id="5e7c4-164">您也會建立叫用 hello 裝置上的方法，並會顯示 hello 回應 hello 裝置的應用程式。</span><span class="sxs-lookup"><span data-stu-id="5e7c4-164">You also created an app that invokes methods on hello device and displays hello response from hello device.</span></span> 

<span data-ttu-id="5e7c4-165">使用者入門 toocontinue tooexplore IoT 中樞與其他 IoT 案例，請參閱：</span><span class="sxs-lookup"><span data-stu-id="5e7c4-165">toocontinue getting started with IoT Hub and tooexplore other IoT scenarios, see:</span></span>

* <span data-ttu-id="5e7c4-166">[IoT 中心入門]</span><span class="sxs-lookup"><span data-stu-id="5e7c4-166">[Get started with IoT Hub]</span></span>
* <span data-ttu-id="5e7c4-167">[排程多個裝置上的作業][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="5e7c4-167">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="5e7c4-168">toolearn 如何 tooextend IoT 解決方案和排程方法呼叫上多個裝置，請參閱 hello[排程和廣播的工作][ lnk-tutorial-jobs]教學課程。</span><span class="sxs-lookup"><span data-stu-id="5e7c4-168">toolearn how tooextend your IoT solution and schedule method calls on multiple devices, see hello [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

<!-- Images. -->
[img-createdeviceapp]: ./media/iot-hub-csharp-csharp-direct-methods/create-device-app.png
[img-clientnuget]: ./media/iot-hub-csharp-csharp-direct-methods/device-app-nuget.png
[img-createserviceapp]: ./media/iot-hub-csharp-csharp-direct-methods/create-service-app.png
[img-servicenuget]: ./media/iot-hub-csharp-csharp-direct-methods/service-app-nuget.png
[img-deviceapprun]: ./media/iot-hub-csharp-csharp-direct-methods/run-device-app.png
[img-serviceapprun]: ./media/iot-hub-csharp-csharp-direct-methods/run-service-app.png
[img-directmethodinvoked]: ./media/iot-hub-csharp-csharp-direct-methods/direct-method-invoked.png

<!-- Links -->
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-nuget-client-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices.Client/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/

[lnk-device-identity-csharp]: iot-hub-csharp-csharp-getstarted.md#DeviceIdentity_csharp

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md

[IoT 中心入門]: iot-hub-node-node-getstarted.md
