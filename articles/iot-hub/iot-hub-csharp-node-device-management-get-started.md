---
title: "aaaGet 開始使用 Azure IoT 中心裝置管理 （.NET/節點） |Microsoft 文件"
description: "如何 toouse Azure IoT 中心裝置管理 tooinitiate 遠端裝置重新開機。 您可以使用 hello Azure IoT 裝置 SDK for Node.js tooimplement 模擬的裝置應用程式，其中包含直接的方法和 hello Azure IoT 服務 SDK for.NET tooimplement hello 直接的方法會叫用的服務應用程式。"
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
ms.date: 11/17/2016
ms.author: juanpere
ms.openlocfilehash: ea6d50dfac1c222d7836e3bf5503c6c9b8c89dfa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-management-netnode"></a><span data-ttu-id="65055-104">開始使用裝置管理 (.NET/Node)</span><span class="sxs-lookup"><span data-stu-id="65055-104">Get started with device management (.NET/Node)</span></span>

[!INCLUDE [iot-hub-selector-dm-getstarted](../../includes/iot-hub-selector-dm-getstarted.md)]

<span data-ttu-id="65055-105">本教學課程說明如何：</span><span class="sxs-lookup"><span data-stu-id="65055-105">This tutorial shows you how to:</span></span>

* <span data-ttu-id="65055-106">使用 hello Azure 入口網站 toocreate IoT 中樞，並在您的 IoT 中樞中建立裝置身分識別。</span><span class="sxs-lookup"><span data-stu-id="65055-106">Use hello Azure portal toocreate an IoT Hub and create a device identity in your IoT hub.</span></span>
* <span data-ttu-id="65055-107">建立模擬裝置應用程式，其包含可將該裝置重新開機的直接方法。</span><span class="sxs-lookup"><span data-stu-id="65055-107">Create a simulated device app that contains a direct method that reboots that device.</span></span> <span data-ttu-id="65055-108">直接的方法會叫用從 hello 雲端。</span><span class="sxs-lookup"><span data-stu-id="65055-108">Direct methods are invoked from hello cloud.</span></span>
* <span data-ttu-id="65055-109">建立.NET 主控台應用程式透過您的 IoT 中樞 hello 模擬的裝置應用程式中呼叫 hello 重新開機直接的方法。</span><span class="sxs-lookup"><span data-stu-id="65055-109">Create a .NET console app that calls hello reboot direct method in hello simulated device app through your IoT hub.</span></span>

<span data-ttu-id="65055-110">在本教學課程的 hello 最後，您有 Node.js 主控台裝置應用程式和.NET (C#) 主控台後端應用程式：</span><span class="sxs-lookup"><span data-stu-id="65055-110">At hello end of this tutorial, you have a Node.js console device app and a .NET (C#) console back-end app:</span></span>

<span data-ttu-id="65055-111">**dmpatterns_getstarted_device.js**，稍早建立的 hello 裝置身分識別與連線 tooyour IoT 中樞收到重新開機直接的方法，會模擬實際的重新開機，並報告 hello hello 上次重新開機的時間。</span><span class="sxs-lookup"><span data-stu-id="65055-111">**dmpatterns_getstarted_device.js**, which connects tooyour IoT hub with hello device identity created earlier, receives a reboot direct method, simulates a physical reboot, and reports hello time for hello last reboot.</span></span>

<span data-ttu-id="65055-112">**TriggerReboot**、 直接的方法呼叫 hello 模擬的裝置，應用程式中顯示 hello 回應，並顯示 hello 更新報告內容。</span><span class="sxs-lookup"><span data-stu-id="65055-112">**TriggerReboot**, which calls a direct method in hello simulated device app, displays hello response, and displays hello updated reported properties.</span></span>

<span data-ttu-id="65055-113">toocomplete 本教學課程中，您需要遵循的 hello:</span><span class="sxs-lookup"><span data-stu-id="65055-113">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="65055-114">Visual Studio 2015 或 Visual Studio 2017。</span><span class="sxs-lookup"><span data-stu-id="65055-114">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="65055-115">Node.js 0.12.x 版或更新版本，</span><span class="sxs-lookup"><span data-stu-id="65055-115">Node.js version 0.12.x or later,</span></span> <br/>  <span data-ttu-id="65055-116">[準備開發環境][ lnk-dev-setup]描述如何 tooinstall Node.js 本教學課程中的 Windows 或 Linux。</span><span class="sxs-lookup"><span data-stu-id="65055-116">[Prepare your development environment][lnk-dev-setup] describes how tooinstall Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="65055-117">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="65055-117">An active Azure account.</span></span> <span data-ttu-id="65055-118">(如果您沒有帳戶，只需要幾分鐘的時間就可以建立[免費帳戶][lnk-free-trial]。)</span><span class="sxs-lookup"><span data-stu-id="65055-118">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-reboot-on-hello-device-using-a-direct-method"></a><span data-ttu-id="65055-119">觸發程序使用直接的方法 hello 裝置上遠端重新開機</span><span class="sxs-lookup"><span data-stu-id="65055-119">Trigger a remote reboot on hello device using a direct method</span></span>
<span data-ttu-id="65055-120">在本節中，您會建立 .NET 主控台應用程式 (使用 C#)，此應用程式會使用直接方法起始遠端重新開機。</span><span class="sxs-lookup"><span data-stu-id="65055-120">In this section, you create a .NET console app (using C#) that initiates a remote reboot on a device using a direct method.</span></span> <span data-ttu-id="65055-121">hello 應用程式中使用該裝置的裝置兩個查詢 toodiscover hello 上次重新開機。</span><span class="sxs-lookup"><span data-stu-id="65055-121">hello app uses device twin queries toodiscover hello last reboot time for that device.</span></span>

1. <span data-ttu-id="65055-122">在 Visual Studio 中，將 Visual C# Windows 傳統桌面專案 tooa 新方案使用 hello**主控台應用程式 (.NET Framework)**專案範本。</span><span class="sxs-lookup"><span data-stu-id="65055-122">In Visual Studio, add a Visual C# Windows Classic Desktop project tooa new solution by using hello **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="65055-123">請確定 hello.NET Framework 版本 4.5.1 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="65055-123">Make sure hello .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="65055-124">名稱 hello 專案**TriggerReboot**。</span><span class="sxs-lookup"><span data-stu-id="65055-124">Name hello project **TriggerReboot**.</span></span>

    ![新的 Visual C# Windows 傳統桌面專案][img-createapp]

2. <span data-ttu-id="65055-126">在 [方案總管] 中，以滑鼠右鍵按一下 hello **TriggerReboot**專案，然後再按一下**管理 NuGet 封裝**。</span><span class="sxs-lookup"><span data-stu-id="65055-126">In Solution Explorer, right-click hello **TriggerReboot** project, and then click **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="65055-127">在 hello **NuGet 套件管理員**視窗中，選取**瀏覽**，搜尋**microsoft.azure.devices**，選取**安裝**tooinstallhello **Microsoft.Azure.Devices**封裝，並接受使用規定 hello。</span><span class="sxs-lookup"><span data-stu-id="65055-127">In hello **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** tooinstall hello **Microsoft.Azure.Devices** package, and accept hello terms of use.</span></span> <span data-ttu-id="65055-128">此程序下載、 安裝，並新增參考 toohello [Azure IoT 服務 SDK] [ lnk-nuget-service-sdk] NuGet 封裝和其相依性。</span><span class="sxs-lookup"><span data-stu-id="65055-128">This procedure downloads, installs, and adds a reference toohello [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>

    ![NuGet 封裝管理員視窗][img-servicenuget]
4. <span data-ttu-id="65055-130">新增下列 hello`using`在 hello hello 最上方的陳述式**Program.cs**檔案：</span><span class="sxs-lookup"><span data-stu-id="65055-130">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
        using Microsoft.Azure.Devices.Shared;
        
5. <span data-ttu-id="65055-131">新增下列欄位 toohello hello**程式**類別。</span><span class="sxs-lookup"><span data-stu-id="65055-131">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="65055-132">取代 hello hello 中樞 hello 上一節和 hello 目標裝置中您建立 IoT 中樞連接字串中的 hello 預留位置的值。</span><span class="sxs-lookup"><span data-stu-id="65055-132">Replace hello placeholder value with hello IoT Hub connection string for hello hub that you created in hello previous section and hello target device.</span></span>
   
        static RegistryManager registryManager;
        static string connString = "{iot hub connection string}";
        static ServiceClient client;
        static JobClient jobClient;
        static string targetDevice = "{deviceIdForTargetDevice}";
        
6. <span data-ttu-id="65055-133">新增下列方法 toohello hello**程式**類別。</span><span class="sxs-lookup"><span data-stu-id="65055-133">Add hello following method toohello **Program** class.</span></span>  <span data-ttu-id="65055-134">重新啟動裝置和輸出 hello hello 這個程式碼取得 hello 裝置兩個報告的屬性。</span><span class="sxs-lookup"><span data-stu-id="65055-134">This code gets hello device twin for hello rebooting device and outputs hello reported properties.</span></span>
   
        public static async Task QueryTwinRebootReported()
        {
            Twin twin = await registryManager.GetTwinAsync(targetDevice);
            Console.WriteLine(twin.Properties.Reported.ToJson());
        }
        
7. <span data-ttu-id="65055-135">新增下列方法 toohello hello**程式**類別。</span><span class="sxs-lookup"><span data-stu-id="65055-135">Add hello following method toohello **Program** class.</span></span>  <span data-ttu-id="65055-136">此程式碼起始 hello 重新開機 hello 裝置上使用直接的方法。</span><span class="sxs-lookup"><span data-stu-id="65055-136">This code initiates hello reboot on hello device using a direct method.</span></span>

        public static async Task StartReboot()
        {
            client = ServiceClient.CreateFromConnectionString(connString);
            CloudToDeviceMethod method = new CloudToDeviceMethod("reboot");
            method.ResponseTimeout = TimeSpan.FromSeconds(30);

            CloudToDeviceMethodResult result = await client.InvokeDeviceMethodAsync(targetDevice, method);

            Console.WriteLine("Invoked firmware update on device.");
        }

7. <span data-ttu-id="65055-137">最後，加入下列行 toohello hello **Main**方法：</span><span class="sxs-lookup"><span data-stu-id="65055-137">Finally, add hello following lines toohello **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connString);
        StartReboot().Wait();
        QueryTwinRebootReported().Wait();
        Console.WriteLine("Press ENTER tooexit.");
        Console.ReadLine();
        
8. <span data-ttu-id="65055-138">建置 hello 方案。</span><span class="sxs-lookup"><span data-stu-id="65055-138">Build hello solution.</span></span>

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="65055-139">建立模擬裝置應用程式</span><span class="sxs-lookup"><span data-stu-id="65055-139">Create a simulated device app</span></span>
<span data-ttu-id="65055-140">在本節中，您將：</span><span class="sxs-lookup"><span data-stu-id="65055-140">In this section, you will</span></span>

* <span data-ttu-id="65055-141">建立回應 tooa 直接方法呼叫 hello 雲端 Node.js 主控台應用程式</span><span class="sxs-lookup"><span data-stu-id="65055-141">Create a Node.js console app that responds tooa direct method called by hello cloud</span></span>
* <span data-ttu-id="65055-142">觸發模擬裝置重新啟動</span><span class="sxs-lookup"><span data-stu-id="65055-142">Trigger a simulated device reboot</span></span>
* <span data-ttu-id="65055-143">使用 hello 報告屬性 tooenable 裝置兩個查詢 tooidentify 裝置，當它們一次啟動</span><span class="sxs-lookup"><span data-stu-id="65055-143">Use hello reported properties tooenable device twin queries tooidentify devices and when they last rebooted</span></span>

1. <span data-ttu-id="65055-144">建立稱為 **manageddevice**的新的空資料夾。</span><span class="sxs-lookup"><span data-stu-id="65055-144">Create a new empty folder called **manageddevice**.</span></span>  <span data-ttu-id="65055-145">在 hello **manageddevice**資料夾中，建立使用下列命令，在您的命令提示字元的 hello package.json 檔案。</span><span class="sxs-lookup"><span data-stu-id="65055-145">In hello **manageddevice** folder, create a package.json file using hello following command at your command prompt.</span></span>  <span data-ttu-id="65055-146">接受所有的 hello 預設值：</span><span class="sxs-lookup"><span data-stu-id="65055-146">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="65055-147">在您的命令提示字元中 hello **manageddevice**資料夾中，執行下列命令 tooinstall hello hello **azure iot 裝置**裝置 SDK 封裝和**azure-iot-裝置-mqtt**封裝：</span><span class="sxs-lookup"><span data-stu-id="65055-147">At your command prompt in hello **manageddevice** folder, run hello following command tooinstall hello **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="65055-148">使用文字編輯器中，建立新**dmpatterns_getstarted_device.js**檔案在 hello **manageddevice**資料夾。</span><span class="sxs-lookup"><span data-stu-id="65055-148">Using a text editor, create a new **dmpatterns_getstarted_device.js** file in hello **manageddevice** folder.</span></span>
4. <span data-ttu-id="65055-149">新增 hello 下列的 '需要' 陳述式在 hello 開頭的 hello **dmpatterns_getstarted_device.js**檔案：</span><span class="sxs-lookup"><span data-stu-id="65055-149">Add hello following 'require' statements at hello start of hello **dmpatterns_getstarted_device.js** file:</span></span>
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
5. <span data-ttu-id="65055-150">新增**connectionString**變數，並使用它 toocreate**用戶端**執行個體。</span><span class="sxs-lookup"><span data-stu-id="65055-150">Add a **connectionString** variable and use it toocreate a **Client** instance.</span></span>  <span data-ttu-id="65055-151">Hello 連接字串取代為您的裝置連接字串。</span><span class="sxs-lookup"><span data-stu-id="65055-151">Replace hello connection string with your device connection string.</span></span>  
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId=myDeviceId;SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```
6. <span data-ttu-id="65055-152">新增 hello 遵循 hello 裝置上的函式 tooimplement hello 直接方法</span><span class="sxs-lookup"><span data-stu-id="65055-152">Add hello following function tooimplement hello direct method on hello device</span></span>
   
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
7. <span data-ttu-id="65055-153">加入 hello 下列程式碼 tooopen hello 連接 tooyour IoT 中樞，並啟動 hello 直接方法接聽程式：</span><span class="sxs-lookup"><span data-stu-id="65055-153">Add hello following code tooopen hello connection tooyour IoT hub and start hello direct method listener:</span></span>
   
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
8. <span data-ttu-id="65055-154">儲存並關閉 hello **dmpatterns_getstarted_device.js**檔案。</span><span class="sxs-lookup"><span data-stu-id="65055-154">Save and close hello **dmpatterns_getstarted_device.js** file.</span></span>
   
> [!NOTE]
> <span data-ttu-id="65055-155">簡單 tookeep 方面，本教學課程未實作任何重試原則。</span><span class="sxs-lookup"><span data-stu-id="65055-155">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="65055-156">在實際執行程式碼，您應該實作重試原則 （例如指數型輪詢），做為建議 hello MSDN 文件中[暫時性錯誤處理][lnk-transient-faults]。</span><span class="sxs-lookup"><span data-stu-id="65055-156">In production code, you should implement retry policies (such as an exponential backoff), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>


## <a name="run-hello-apps"></a><span data-ttu-id="65055-157">執行 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="65055-157">Run hello apps</span></span>
<span data-ttu-id="65055-158">現在您已經準備就緒 toorun hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="65055-158">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="65055-159">在 hello 命令提示字元中 hello **manageddevice**資料夾中，執行下列命令 toobegin 接聽 hello 重新開機直接方法 hello。</span><span class="sxs-lookup"><span data-stu-id="65055-159">At hello command prompt in hello **manageddevice** folder, run hello following command toobegin listening for hello reboot direct method.</span></span>
   
    ```
    node dmpatterns_getstarted_device.js
    ```
2. <span data-ttu-id="65055-160">執行的 hello C# 主控台應用程式**TriggerReboot**。</span><span class="sxs-lookup"><span data-stu-id="65055-160">Run hello C# console app **TriggerReboot**.</span></span> <span data-ttu-id="65055-161">以滑鼠右鍵按一下 hello **TriggerReboot**專案，然後選取**偵錯**，然後選取**開始新執行個體**。</span><span class="sxs-lookup"><span data-stu-id="65055-161">Right-click hello **TriggerReboot** project, select **Debug**, and then select **Start new instance**.</span></span>

3. <span data-ttu-id="65055-162">您會看到 hello 裝置回應 toohello 直接方法 hello 主控台中。</span><span class="sxs-lookup"><span data-stu-id="65055-162">You see hello device response toohello direct method in hello console.</span></span>

[!INCLUDE [iot-hub-dm-followup](../../includes/iot-hub-dm-followup.md)]

<!-- images and links -->
[img-output]: media/iot-hub-get-started-with-dm/image6.png
[img-dm-ui]: media/iot-hub-get-started-with-dm/dmui.png
[img-servicenuget]: media/iot-hub-csharp-node-device-management-get-started/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-node-device-management-get-started/createnetapp.png

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md

[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[Azure portal]: https://portal.azure.com/
[Using resource groups toomanage your Azure resources]: ../azure-portal/resource-group-portal.md
[lnk-dm-github]: https://github.com/Azure/azure-iot-device-management

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/