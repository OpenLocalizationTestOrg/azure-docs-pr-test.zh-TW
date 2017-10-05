---
title: "使用 Azure IoT 中樞進行裝置韌體更新 (.NET/Node) | Microsoft Docs"
description: "如何使用 Azure IoT 中樞上的裝置管理來起始裝置韌體更新。 您可以使用適用於 Node.js 的 Azure IoT 裝置 SDK，實作模擬裝置應用程式，也可以使用適用於 .NET 的 Azure IoT 服務 SDK，實作服務應用程式以觸發韌體更新。"
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
ms.date: 03/17/2017
ms.author: juanpere
ms.openlocfilehash: c2192328a152e955d182c4a07b391c98a5960964
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-device-management-to-initiate-a-device-firmware-update-netnode"></a><span data-ttu-id="5262e-104">使用裝置管理來起始裝置韌體更新 (.NET/Node)</span><span class="sxs-lookup"><span data-stu-id="5262e-104">Use device management to initiate a device firmware update (.NET/Node)</span></span>
[!INCLUDE [iot-hub-selector-firmware-update](../../includes/iot-hub-selector-firmware-update.md)]

## <a name="introduction"></a><span data-ttu-id="5262e-105">簡介</span><span class="sxs-lookup"><span data-stu-id="5262e-105">Introduction</span></span>
<span data-ttu-id="5262e-106">在[開始使用裝置管理][lnk-dm-getstarted]教學課程中，您已了解如何使用[裝置對應項][lnk-devtwin]和[直接方案][lnk-c2dmethod]基礎，從遠端重新啟動裝置。</span><span class="sxs-lookup"><span data-stu-id="5262e-106">In the [Get started with device management][lnk-dm-getstarted] tutorial, you saw how to use the [device twin][lnk-devtwin] and [direct methods][lnk-c2dmethod] primitives to remotely reboot a device.</span></span> <span data-ttu-id="5262e-107">本教學課程使用相同的 IoT 中樞基元，並示範如何進行端對端模擬韌體更新。</span><span class="sxs-lookup"><span data-stu-id="5262e-107">This tutorial uses the same IoT Hub primitives and shows you how to do an end-to-end simulated firmware update.</span></span>  <span data-ttu-id="5262e-108">此模式用於 [Raspberry Pi 裝置實作範例][lnk-rpi-implementation]的韌體更新實作。</span><span class="sxs-lookup"><span data-stu-id="5262e-108">This pattern is used in the firmware update implementation for the [Raspberry Pi device implementation sample][lnk-rpi-implementation].</span></span>

<span data-ttu-id="5262e-109">本教學課程說明如何：</span><span class="sxs-lookup"><span data-stu-id="5262e-109">This tutorial shows you how to:</span></span>

* <span data-ttu-id="5262e-110">建立 .NET 主控台應用程式，以透過您的 IoT 中樞在模擬裝置應用程式中呼叫 firmwareUpdate 直接方法。</span><span class="sxs-lookup"><span data-stu-id="5262e-110">Create a .NET console app that calls the firmwareUpdate direct method in the simulated device app through your IoT hub.</span></span>
* <span data-ttu-id="5262e-111">建立會實作 **firmwareUpdate** 直接方法的模擬裝置應用程式。</span><span class="sxs-lookup"><span data-stu-id="5262e-111">Create a simulated device app that implements a **firmwareUpdate** direct method.</span></span> <span data-ttu-id="5262e-112">此方法會起始多階段程序，此程序會等候下載韌映像、下載韌體映像，最後再套用韌體映像。</span><span class="sxs-lookup"><span data-stu-id="5262e-112">This method initiates a multi-stage process that waits to download the firmware image, downloads the firmware image, and finally applies the firmware image.</span></span> <span data-ttu-id="5262e-113">在更新的每個階段，裝置都會使用回報的屬性來回報進度。</span><span class="sxs-lookup"><span data-stu-id="5262e-113">During each stage of the update, the device uses the reported properties to report on progress.</span></span>

<span data-ttu-id="5262e-114">在本教學課程結束時，您會有 Node.js 主控台裝置應用程式和 .NET (C#) 主控台後端應用程式：</span><span class="sxs-lookup"><span data-stu-id="5262e-114">At the end of this tutorial, you have a Node.js console device app and a .NET (C#) console back-end app:</span></span>

<span data-ttu-id="5262e-115">**dmpatterns_fwupdate_service.js**：在模擬裝置應用程式中呼叫直接方法、顯示回應，並定期 (每 500 毫秒) 顯示更新的報告屬性。</span><span class="sxs-lookup"><span data-stu-id="5262e-115">**dmpatterns_fwupdate_service.js**, which calls a direct method in the simulated device app, displays the response, and periodically (every 500ms) displays the updated reported properties.</span></span>

<span data-ttu-id="5262e-116">**TriggerFWUpdate**會將您的 IoT 中樞連接至稍早建立的裝置身分識別，接收 firmwareUpdate 直接方法，透過多重狀態處理執行以模擬韌體更新，包括等待映像下載、下載新的映像，最後套用映像。</span><span class="sxs-lookup"><span data-stu-id="5262e-116">**TriggerFWUpdate**, which connects to your IoT hub with the device identity created earlier, receives a firmwareUpdate direct method, runs through a multi-state process to simulate a firmware update including: waiting for the image download, downloading the new image, and finally applying the image.</span></span>

<span data-ttu-id="5262e-117">若要完成此教學課程，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="5262e-117">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="5262e-118">Visual Studio 2015 或 Visual Studio 2017。</span><span class="sxs-lookup"><span data-stu-id="5262e-118">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="5262e-119">Node.js 0.12.x 版或更新版本，</span><span class="sxs-lookup"><span data-stu-id="5262e-119">Node.js version 0.12.x or later,</span></span> <br/>  <span data-ttu-id="5262e-120">[準備您的開發環境][lnk-dev-setup]說明如何在 Windows 或 Linux 上安裝本教學課程的 Node.js。</span><span class="sxs-lookup"><span data-stu-id="5262e-120">[Prepare your development environment][lnk-dev-setup] describes how to install Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="5262e-121">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="5262e-121">An active Azure account.</span></span> <span data-ttu-id="5262e-122">(如果您沒有帳戶，只需要幾分鐘的時間就可以建立[免費帳戶][lnk-free-trial]。)</span><span class="sxs-lookup"><span data-stu-id="5262e-122">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

<span data-ttu-id="5262e-123">請依照[開始使用裝置管理](iot-hub-csharp-node-device-management-get-started.md)文件，以建立 IoT 中樞及取得 IoT 中樞連接字串。</span><span class="sxs-lookup"><span data-stu-id="5262e-123">Follow the [Get started with device management](iot-hub-csharp-node-device-management-get-started.md) article to create your IoT hub and get your IoT Hub connection string.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-firmware-update-on-the-device-using-a-direct-method"></a><span data-ttu-id="5262e-124">使用直接方法在裝置上觸發遠端韌體更新</span><span class="sxs-lookup"><span data-stu-id="5262e-124">Trigger a remote firmware update on the device using a direct method</span></span>
<span data-ttu-id="5262e-125">在此節中，您會建立 .NET 主控台應用程式 (使用 C#)，此應用程式會在裝置上起始遠端韌體更新。</span><span class="sxs-lookup"><span data-stu-id="5262e-125">In this section, you create a .NET console app (using C#) that initiates a remote firmware update on a device.</span></span> <span data-ttu-id="5262e-126">此應用程式使用直接方法來起始更新，並使用裝置對應項查詢來定期取得作用中韌體更新的狀態。</span><span class="sxs-lookup"><span data-stu-id="5262e-126">The app uses a direct method to initiate the update and uses device twin queries to periodically get the status of the active firmware update.</span></span>

1. <span data-ttu-id="5262e-127">在 Visual Studio 中，使用 [主控台應用程式] 專案範本，將 Visual C# Windows 傳統桌面專案新增至目前的方案。</span><span class="sxs-lookup"><span data-stu-id="5262e-127">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution by using the **Console Application** project template.</span></span> <span data-ttu-id="5262e-128">將專案命名為 **TriggerFWUpdate**。</span><span class="sxs-lookup"><span data-stu-id="5262e-128">Name the project **TriggerFWUpdate**.</span></span>

    ![新的 Visual C# Windows 傳統桌面專案][img-createapp]

1. <span data-ttu-id="5262e-130">在 [方案總管] 中，以滑鼠右鍵按一下 [TriggerFWUpdate] 專案，然後按一下 [管理 NuGet 套件]。</span><span class="sxs-lookup"><span data-stu-id="5262e-130">In Solution Explorer, right-click the **TriggerFWUpdate** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="5262e-131">在 [Nuget 套件管理員] 視窗中選取 [瀏覽]、搜尋 **microsoft.azure.devices**、選取 [安裝] 以安裝 **Microsoft.Azure.Devices** 套件，並接受使用規定。</span><span class="sxs-lookup"><span data-stu-id="5262e-131">In the **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** to install the **Microsoft.Azure.Devices** package, and accept the terms of use.</span></span> <span data-ttu-id="5262e-132">此程序會下載及安裝 [Azure IoT 服務 SDK][lnk-nuget-service-sdk] NuGet 套件與其相依項目，並新增對它的參考。</span><span class="sxs-lookup"><span data-stu-id="5262e-132">This procedure downloads, installs, and adds a reference to the [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>

    ![NuGet 套件管理員視窗][img-servicenuget]
1. <span data-ttu-id="5262e-134">在 **Program.cs** 檔案開頭處新增下列 `using` 陳述式：</span><span class="sxs-lookup"><span data-stu-id="5262e-134">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
        using Microsoft.Azure.Devices.Shared;
        
1. <span data-ttu-id="5262e-135">將下列欄位新增到 **Program** 類別。</span><span class="sxs-lookup"><span data-stu-id="5262e-135">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="5262e-136">將多個預留位置值取代為您在上一節中為中樞所建立的 IoT 中樞連接字串與您的裝置識別碼。</span><span class="sxs-lookup"><span data-stu-id="5262e-136">Replace the multiple placeholder values with the IoT Hub connection string for the hub that you created in the previous section and the Id of your device.</span></span>
   
        static RegistryManager registryManager;
        static string connString = "{iot hub connection string}";
        static ServiceClient client;
        static JobClient jobClient;
        static string targetDevice = "{deviceIdForTargetDevice}";
        
1. <span data-ttu-id="5262e-137">將下列方法加入至 **Program** 類別：</span><span class="sxs-lookup"><span data-stu-id="5262e-137">Add the following method to the **Program** class:</span></span>
   
        public static async Task QueryTwinFWUpdateReported()
        {
            Twin twin = await registryManager.GetTwinAsync(targetDevice);
            Console.WriteLine(twin.Properties.Reported.ToJson());
        }
        
1. <span data-ttu-id="5262e-138">將下列方法加入至 **Program** 類別：</span><span class="sxs-lookup"><span data-stu-id="5262e-138">Add the following method to the **Program** class:</span></span>

        public static async Task StartFirmwareUpdate()
        {
            client = ServiceClient.CreateFromConnectionString(connString);
            CloudToDeviceMethod method = new CloudToDeviceMethod("firmwareUpdate");
            method.ResponseTimeout = TimeSpan.FromSeconds(30);
            method.SetPayloadJson(
                @"{
                    fwPackageUri : 'https://someurl'
                }");

            CloudToDeviceMethodResult result = await client.InvokeDeviceMethodAsync(targetDevice, method);

            Console.WriteLine("Invoked firmware update on device.");
        }

1. <span data-ttu-id="5262e-139">最後，將下列幾行加入至 **Main** 方法：</span><span class="sxs-lookup"><span data-stu-id="5262e-139">Finally, add the following lines to the **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connString);
        StartFirmwareUpdate().Wait();
        QueryTwinFWUpdateReported().Wait();
        Console.WriteLine("Press ENTER to exit.");
        Console.ReadLine();
        
1. <span data-ttu-id="5262e-140">在 [方案總管] 中，開啟 [設定起始專案]，並確定 **TriggerFWUpdate** 專案的 [動作] 是 [起始]。</span><span class="sxs-lookup"><span data-stu-id="5262e-140">In the Solution Explorer, open the **Set StartUp projects...** and make sure the **Action** for **TriggerFWUpdate** project is **Start**.</span></span>

1. <span data-ttu-id="5262e-141">建置方案。</span><span class="sxs-lookup"><span data-stu-id="5262e-141">Build the solution.</span></span>

[!INCLUDE [iot-hub-device-firmware-update](../../includes/iot-hub-device-firmware-update.md)]

## <a name="run-the-apps"></a><span data-ttu-id="5262e-142">執行應用程式</span><span class="sxs-lookup"><span data-stu-id="5262e-142">Run the apps</span></span>
<span data-ttu-id="5262e-143">您現在可以開始執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="5262e-143">You are now ready to run the apps.</span></span>

1. <span data-ttu-id="5262e-144">在 **manageddevice** 資料夾中，於命令提示字元中執行下列命令以開始接聽重新啟動直接方法。</span><span class="sxs-lookup"><span data-stu-id="5262e-144">At the command prompt in the **manageddevice** folder, run the following command to begin listening for the reboot direct method.</span></span>
   
    ```
    node dmpatterns_fwupdate_device.js
    ```
2. <span data-ttu-id="5262e-145">在 Visual Studio 中，以滑鼠右鍵按一下 [TriggerFWUpdate] 專案。執行到 C# 主控台應用程式，選取 [偵錯] 與 [開始新執行個體]。</span><span class="sxs-lookup"><span data-stu-id="5262e-145">In Visual Studio, right-click on the **TriggerFWUpdate** projectRun to the C# console app, select **Debug** and **Start new instance**.</span></span>

3. <span data-ttu-id="5262e-146">您會在主控台中看到直接方法的裝置回應。</span><span class="sxs-lookup"><span data-stu-id="5262e-146">You see the device response to the direct method in the console.</span></span>

    ![已順利更新韌體][img-fwupdate]

## <a name="next-steps"></a><span data-ttu-id="5262e-148">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5262e-148">Next steps</span></span>
<span data-ttu-id="5262e-149">在此教學課程中，您使用直接方法來觸發裝置上的遠端韌體更新，並且使用回報的屬性追蹤韌體更新的進度。</span><span class="sxs-lookup"><span data-stu-id="5262e-149">In this tutorial, you used a direct method to trigger a remote firmware update on a device and used the reported properties to follow the progress of the firmware update.</span></span>

<span data-ttu-id="5262e-150">若要了解如何擴充您的 IoT 解決方案以及在多個裝置上排程方法呼叫，請參閱[排程及廣播作業][lnk-tutorial-jobs]教學課程。</span><span class="sxs-lookup"><span data-stu-id="5262e-150">To learn how to extend your IoT solution and schedule method calls on multiple devices, see the [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-node-firmware-update/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-node-firmware-update/createnetapp.png
[img-fwupdate]: media/iot-hub-csharp-node-firmware-update/fwupdated.png

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-dm-getstarted]: iot-hub-node-node-device-management-get-started.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-rpi-implementation]: https://github.com/Azure/azure-iot-sdk-c/tree/master/iothub_client/samples/iothub_client_sample_mqtt_dm/pi_device
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/