---
title: "aaaUse Azure IoT Hub 裝置的兩個屬性 (.NET/.NET) |Microsoft 文件"
description: "如何 toouse Azure IoT Hub 裝置雙 tooconfigure 裝置。 您可以使用.NET tooimplement 模擬的裝置應用程式的 hello Azure IoT 裝置 SDK 和 hello Azure IoT 服務 SDK for.NET tooimplement 修改使用裝置的兩個裝置設定的服務應用程式。"
services: iot-hub
documentationcenter: .net
author: dsk-2015
manager: timlt
editor: 
ms.assetid: 3c627476-f982-43c9-bd17-e0698c5d236d
ms.service: iot-hub
ms.devlang: csharp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/10/2017
ms.author: dkshir
ms.openlocfilehash: 486436d29abfd5158c253adc5abf5935e0e1fdba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-desired-properties-tooconfigure-devices"></a><span data-ttu-id="0a9bc-104">使用所需的屬性 tooconfigure 裝置</span><span class="sxs-lookup"><span data-stu-id="0a9bc-104">Use desired properties tooconfigure devices</span></span>
[!INCLUDE [iot-hub-selector-twin-how-to-configure](../../includes/iot-hub-selector-twin-how-to-configure.md)]

<span data-ttu-id="0a9bc-105">在本教學課程的 hello 結束時，您將擁有兩個.NET 主控台應用程式：</span><span class="sxs-lookup"><span data-stu-id="0a9bc-105">At hello end of this tutorial, you will have two .NET console apps:</span></span>

* <span data-ttu-id="0a9bc-106">**SimulateDeviceConfiguration**，模擬的裝置應用程式等候的所需的組態更新，並報告 hello 模擬的組態更新程序的狀態。</span><span class="sxs-lookup"><span data-stu-id="0a9bc-106">**SimulateDeviceConfiguration**, a simulated device app that waits for a desired configuration update and reports hello status of a simulated configuration update process.</span></span>
* <span data-ttu-id="0a9bc-107">**SetDesiredConfigurationAndQuery**、 設定 hello 後端應用程式預期在裝置上的設定和查詢 hello 組態更新程序。</span><span class="sxs-lookup"><span data-stu-id="0a9bc-107">**SetDesiredConfigurationAndQuery**, a back-end app, which sets hello desired configuration on a device and queries hello configuration update process.</span></span>

> [!NOTE]
> <span data-ttu-id="0a9bc-108">hello 文章[Azure IoT Sdk] [ lnk-hub-sdks]提供 hello Azure IoT Sdk 的相關資訊，您可以使用 toobuild 裝置與後端應用程式。</span><span class="sxs-lookup"><span data-stu-id="0a9bc-108">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="0a9bc-109">toocomplete 需要 hello 下列本教學課程：</span><span class="sxs-lookup"><span data-stu-id="0a9bc-109">toocomplete this tutorial you need hello following:</span></span>

* <span data-ttu-id="0a9bc-110">Visual Studio 2015 或 Visual Studio 2017。</span><span class="sxs-lookup"><span data-stu-id="0a9bc-110">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="0a9bc-111">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="0a9bc-111">An active Azure account.</span></span> <span data-ttu-id="0a9bc-112">如果您沒有帳戶，只需要幾分鐘的時間就可以建立[免費帳戶][lnk-free-trial]。</span><span class="sxs-lookup"><span data-stu-id="0a9bc-112">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>

<span data-ttu-id="0a9bc-113">如果您遵循 hello[開始使用裝置雙][ lnk-twin-tutorial]教學課程中，您已經有 IoT 中樞和裝置身分識別稱為**myDeviceId**。</span><span class="sxs-lookup"><span data-stu-id="0a9bc-113">If you followed hello [Get started with device twins][lnk-twin-tutorial] tutorial, you already have an IoT hub and a device identity called **myDeviceId**.</span></span> <span data-ttu-id="0a9bc-114">在此情況下，您可以略過 toohello[建立 hello 模擬的裝置應用程式][ lnk-how-to-configure-createapp] > 一節。</span><span class="sxs-lookup"><span data-stu-id="0a9bc-114">In that case, you can skip toohello [Create hello simulated device app][lnk-how-to-configure-createapp] section.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

<a id="#create-the-simulated-device-app"></a>
## <a name="create-hello-simulated-device-app"></a><span data-ttu-id="0a9bc-115">建立 hello 模擬的裝置應用程式</span><span class="sxs-lookup"><span data-stu-id="0a9bc-115">Create hello simulated device app</span></span>
<span data-ttu-id="0a9bc-116">在本節中，您會建立.NET 主控台應用程式連接成 tooyour 中樞**myDeviceId**等候所需的組態更新，然後報告 hello 模擬的組態更新程序中的 更新。</span><span class="sxs-lookup"><span data-stu-id="0a9bc-116">In this section, you create a .NET console app that connects tooyour hub as **myDeviceId**, waits for a desired configuration update and then reports updates on hello simulated configuration update process.</span></span>

1. <span data-ttu-id="0a9bc-117">在 Visual Studio 中，建立新的 Visual C# Windows 傳統桌面專案使用 hello**主控台應用程式**專案範本。</span><span class="sxs-lookup"><span data-stu-id="0a9bc-117">In Visual Studio, create a new Visual C# Windows Classic Desktop project by using hello **Console Application** project template.</span></span> <span data-ttu-id="0a9bc-118">名稱 hello 專案**SimulateDeviceConfiguration**。</span><span class="sxs-lookup"><span data-stu-id="0a9bc-118">Name hello project **SimulateDeviceConfiguration**.</span></span>
   
    ![新的 Visual C# Windows 傳統裝置應用程式][img-createdeviceapp]

1. <span data-ttu-id="0a9bc-120">在 [方案總管] 中，以滑鼠右鍵按一下 hello **SimulateDeviceConfiguration**專案，然後再按一下**管理 NuGet 封裝...**.</span><span class="sxs-lookup"><span data-stu-id="0a9bc-120">In Solution Explorer, right-click hello **SimulateDeviceConfiguration** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="0a9bc-121">在 hello **NuGet 套件管理員**視窗中，選取**瀏覽**並搜尋**microsoft.azure.devices.client**。</span><span class="sxs-lookup"><span data-stu-id="0a9bc-121">In hello **NuGet Package Manager** window, select **Browse** and search for **microsoft.azure.devices.client**.</span></span> <span data-ttu-id="0a9bc-122">選取**安裝**tooinstall hello **Microsoft.Azure.Devices.Client**封裝，並接受使用規定 hello。</span><span class="sxs-lookup"><span data-stu-id="0a9bc-122">Select **Install** tooinstall hello **Microsoft.Azure.Devices.Client** package, and accept hello terms of use.</span></span> <span data-ttu-id="0a9bc-123">此程序下載、 安裝，並新增參考 toohello [Azure IoT 裝置 SDK] [ lnk-nuget-client-sdk] NuGet 封裝和其相依性。</span><span class="sxs-lookup"><span data-stu-id="0a9bc-123">This procedure downloads, installs, and adds a reference toohello [Azure IoT device SDK][lnk-nuget-client-sdk] NuGet package and its dependencies.</span></span>
   
    ![NuGet 套件管理員視窗用戶端應用程式][img-clientnuget]
1. <span data-ttu-id="0a9bc-125">新增下列 hello`using`在 hello hello 最上方的陳述式**Program.cs**檔案：</span><span class="sxs-lookup"><span data-stu-id="0a9bc-125">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices.Client;
        using Microsoft.Azure.Devices.Shared;
        using Newtonsoft.Json;

1. <span data-ttu-id="0a9bc-126">新增下列欄位 toohello hello**程式**類別。</span><span class="sxs-lookup"><span data-stu-id="0a9bc-126">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="0a9bc-127">取代您記下 hello 前一節中的 hello 裝置連接字串中的 hello 預留位置的值。</span><span class="sxs-lookup"><span data-stu-id="0a9bc-127">Replace hello placeholder value with hello device connection string that you noted in hello previous section.</span></span>
   
        static string DeviceConnectionString = "HostName=<yourIotHubName>.azure-devices.net;DeviceId=<yourIotDeviceName>;SharedAccessKey=<yourIotDeviceAccessKey>";
        static DeviceClient Client = null;
        static TwinCollection reportedProperties = new TwinCollection();

1. <span data-ttu-id="0a9bc-128">新增下列方法 toohello hello**程式**類別：</span><span class="sxs-lookup"><span data-stu-id="0a9bc-128">Add hello following method toohello **Program** class:</span></span>
 
        public static void InitClient()
        {
            try
            {
                Console.WriteLine("Connecting toohub");
                Client = DeviceClient.CreateFromConnectionString(DeviceConnectionString, TransportType.Mqtt);
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }
    <span data-ttu-id="0a9bc-129">hello**用戶端**物件會公開您需要將裝置從 hello 裝置的雙具備 toointeract 所有 hello 方法。</span><span class="sxs-lookup"><span data-stu-id="0a9bc-129">hello **Client** object exposes all hello methods you require toointeract with device twins from hello device.</span></span> <span data-ttu-id="0a9bc-130">hello，如上所示的程式碼初始化 hello**用戶端**物件，然後按一下 擷取的 hello 裝置兩個**myDeviceId**。</span><span class="sxs-lookup"><span data-stu-id="0a9bc-130">hello code shown above, initializes hello **Client** object, and then retrieves hello device twin for **myDeviceId**.</span></span>

1. <span data-ttu-id="0a9bc-131">新增下列方法 toohello hello**程式**類別。</span><span class="sxs-lookup"><span data-stu-id="0a9bc-131">Add hello following method toohello **Program** class.</span></span> <span data-ttu-id="0a9bc-132">這個方法會設定初始值遙測 hello hello 本機裝置上，然後更新 hello 裝置兩個。</span><span class="sxs-lookup"><span data-stu-id="0a9bc-132">This method sets hello initial values of telemetry on hello local device and then updates hello device twin.</span></span>

        public static async void InitTelemetry()
        {
            try
            {
                Console.WriteLine("Report initial telemetry config:");
                TwinCollection telemetryConfig = new TwinCollection();
                
                telemetryConfig["configId"] = "0";
                telemetryConfig["sendFrequency"] = "24h";
                reportedProperties["telemetryConfig"] = telemetryConfig;
                Console.WriteLine(JsonConvert.SerializeObject(reportedProperties));

                await Client.UpdateReportedPropertiesAsync(reportedProperties);
            }
            catch (AggregateException ex)
            {
                foreach (Exception exception in ex.InnerExceptions)
                {
                    Console.WriteLine();
                    Console.WriteLine("Error in sample: {0}", exception);
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }

1. <span data-ttu-id="0a9bc-133">新增下列方法 toohello hello**程式**類別。</span><span class="sxs-lookup"><span data-stu-id="0a9bc-133">Add hello following method toohello **Program** class.</span></span> <span data-ttu-id="0a9bc-134">這是會偵測到變更的回呼*所需屬性*在 hello 裝置兩個。</span><span class="sxs-lookup"><span data-stu-id="0a9bc-134">This is a callback which will detect a change in *desired properties* in hello device twin.</span></span>

        private static async Task OnDesiredPropertyChanged(TwinCollection desiredProperties, object userContext)
        {
            try
            {
                Console.WriteLine("Desired property change:");
                Console.WriteLine(JsonConvert.SerializeObject(desiredProperties));

                var currentTelemetryConfig = reportedProperties["telemetryConfig"];
                var desiredTelemetryConfig = desiredProperties["telemetryConfig"];

                if ((desiredTelemetryConfig != null) && (desiredTelemetryConfig["configId"] != currentTelemetryConfig["configId"]))
                {
                    Console.WriteLine("\nInitiating config change");
                    currentTelemetryConfig["status"] = "Pending";
                    currentTelemetryConfig["pendingConfig"] = desiredTelemetryConfig;

                    await Client.UpdateReportedPropertiesAsync(reportedProperties);

                    CompleteConfigChange();
                }
            }
            catch (AggregateException ex)
            {
                foreach (Exception exception in ex.InnerExceptions)
                {
                    Console.WriteLine();
                    Console.WriteLine("Error in sample: {0}", exception);
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }

    <span data-ttu-id="0a9bc-135">此方法更新 hello 回報 hello 組態與 hello 本機裝置兩個物件上的內容更新要求和設定 hello 狀態太**暫止**，然後更新 hello 裝置 hello 服務上的兩個。</span><span class="sxs-lookup"><span data-stu-id="0a9bc-135">This method updates hello reported properties on hello local device twin object with hello configuration update request and sets hello status too**Pending**, then updates hello device twin on hello service.</span></span> <span data-ttu-id="0a9bc-136">已成功更新之後 hello 裝置兩個，完成 hello 組態變更呼叫 hello 方法`CompleteConfigChange`hello 下一個點中所述。</span><span class="sxs-lookup"><span data-stu-id="0a9bc-136">After successfully updating hello device twin, it completes hello config change by calling hello method `CompleteConfigChange` described in hello next point.</span></span>

1. <span data-ttu-id="0a9bc-137">新增下列方法 toohello hello**程式**類別。</span><span class="sxs-lookup"><span data-stu-id="0a9bc-137">Add hello following method toohello **Program** class.</span></span> <span data-ttu-id="0a9bc-138">這個方法可以模擬裝置重設，然後更新 hello 太 hello 狀態設定本機的報告的屬性**成功**和移除 hello **pendingConfig**項目。</span><span class="sxs-lookup"><span data-stu-id="0a9bc-138">This method simulates a device reset, then updates hello local reported properties setting hello status too**Success** and removes hello **pendingConfig** element.</span></span> <span data-ttu-id="0a9bc-139">然後，它會更新 hello 裝置的兩個 hello 服務上。</span><span class="sxs-lookup"><span data-stu-id="0a9bc-139">It then updates hello device twin on hello service.</span></span> 

        public static async void CompleteConfigChange()
        {
            try
            {
                var currentTelemetryConfig = reportedProperties["telemetryConfig"];

                Console.WriteLine("\nSimulating device reset");
                await Task.Delay(30000); 

                Console.WriteLine("\nCompleting config change");
                currentTelemetryConfig["configId"] = currentTelemetryConfig["pendingConfig"]["configId"];
                currentTelemetryConfig["sendFrequency"] = currentTelemetryConfig["pendingConfig"]["sendFrequency"];
                currentTelemetryConfig["status"] = "Success";
                currentTelemetryConfig["pendingConfig"] = null;

                await Client.UpdateReportedPropertiesAsync(reportedProperties);
                Console.WriteLine("Config change complete \nPress any key tooexit.");
            }
            catch (AggregateException ex)
            {
                foreach (Exception exception in ex.InnerExceptions)
                {
                    Console.WriteLine();
                    Console.WriteLine("Error in sample: {0}", exception);
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }

1. <span data-ttu-id="0a9bc-140">最後會加入下列行 toohello hello **Main**方法：</span><span class="sxs-lookup"><span data-stu-id="0a9bc-140">Finally add hello following lines toohello **Main** method:</span></span>

        try
        {
            InitClient();
            InitTelemetry();

            Console.WriteLine("Wait for desired telemetry...");
            Client.SetDesiredPropertyUpdateCallback(OnDesiredPropertyChanged, null).Wait();
            Console.ReadKey();
        }
        catch (AggregateException ex)
        {
            foreach (Exception exception in ex.InnerExceptions)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", exception);
            }
        }
        catch (Exception ex)
        {
            Console.WriteLine();
            Console.WriteLine("Error in sample: {0}", ex.Message);
        }

   > [!NOTE]
   > <span data-ttu-id="0a9bc-141">本教學課程不會模擬並行組態更新的任何行為。</span><span class="sxs-lookup"><span data-stu-id="0a9bc-141">This tutorial does not simulate any behavior for concurrent configuration updates.</span></span> <span data-ttu-id="0a9bc-142">某些組態更新處理程序可能會無法 tooaccommodate 變更目標組態的 hello 更新執行時，有些可能會有 tooqueue，以及一些無法拒絕它們與錯誤狀況。</span><span class="sxs-lookup"><span data-stu-id="0a9bc-142">Some configuration update processes might be able tooaccommodate changes of target configuration while hello update is running, some might have tooqueue them, and some could reject them with an error condition.</span></span> <span data-ttu-id="0a9bc-143">請確定 tooconsider hello 特定組態程序中，所要的行為，並加入初始化 hello 組態變更之前的 hello 適當的邏輯。</span><span class="sxs-lookup"><span data-stu-id="0a9bc-143">Make sure tooconsider hello desired behavior for your specific configuration process, and add hello appropriate logic before initiating hello configuration change.</span></span>
   > 
   > 
1. <span data-ttu-id="0a9bc-144">建置 hello 方案，然後從 Visual Studio 執行 hello 裝置應用程式，依序按一下**F5**。</span><span class="sxs-lookup"><span data-stu-id="0a9bc-144">Build hello solution and then run hello device app from Visual Studio by clicking **F5**.</span></span> <span data-ttu-id="0a9bc-145">Hello 輸出在主控台上，您應該會看到 hello 訊息，指出您模擬的裝置是擷取 hello 裝置兩個、 設定 hello 遙測和等候所需的屬性變更。</span><span class="sxs-lookup"><span data-stu-id="0a9bc-145">On hello output console, you should see hello messages indicating that your simulated device is retrieving hello device twin, setting up hello telemetry, and waiting for desired property change.</span></span> <span data-ttu-id="0a9bc-146">保留 hello 應用程式執行。</span><span class="sxs-lookup"><span data-stu-id="0a9bc-146">Keep hello app running.</span></span>

## <a name="create-hello-service-app"></a><span data-ttu-id="0a9bc-147">建立 hello 服務應用程式</span><span class="sxs-lookup"><span data-stu-id="0a9bc-147">Create hello service app</span></span>
<span data-ttu-id="0a9bc-148">在本節中，您將建立.NET 主控台應用程式的更新 hello*所需屬性*上 hello 與相關聯的裝置兩個**myDeviceId**與新的遙測組態物件。</span><span class="sxs-lookup"><span data-stu-id="0a9bc-148">In this section, you will create a .NET console app that updates hello *desired properties* on hello device twin associated with **myDeviceId** with a new telemetry configuration object.</span></span> <span data-ttu-id="0a9bc-149">接著會查詢儲存在 hello IoT 中樞中的 hello 裝置雙，並顯示 hello 差異 hello 想要與報告的 hello 裝置組態。</span><span class="sxs-lookup"><span data-stu-id="0a9bc-149">It then queries hello device twins stored in hello IoT hub and shows hello difference between hello desired and reported configurations of hello device.</span></span>

1. <span data-ttu-id="0a9bc-150">在 Visual Studio 中，將 Visual C# Windows 傳統桌面專案 toohello 目前方案使用 hello**主控台應用程式**專案範本。</span><span class="sxs-lookup"><span data-stu-id="0a9bc-150">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution by using hello **Console Application** project template.</span></span> <span data-ttu-id="0a9bc-151">名稱 hello 專案**SetDesiredConfigurationAndQuery**。</span><span class="sxs-lookup"><span data-stu-id="0a9bc-151">Name hello project **SetDesiredConfigurationAndQuery**.</span></span>
   
    ![新的 Visual C# Windows 傳統桌面專案][img-createapp]
1. <span data-ttu-id="0a9bc-153">在 [方案總管] 中，以滑鼠右鍵按一下 hello **SetDesiredConfigurationAndQuery**專案，然後再按一下**管理 NuGet 封裝...**.</span><span class="sxs-lookup"><span data-stu-id="0a9bc-153">In Solution Explorer, right-click hello **SetDesiredConfigurationAndQuery** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="0a9bc-154">在 hello **NuGet 套件管理員**視窗中，選取**瀏覽**，搜尋**microsoft.azure.devices**，選取**安裝**tooinstallhello **Microsoft.Azure.Devices**封裝，並接受使用規定 hello。</span><span class="sxs-lookup"><span data-stu-id="0a9bc-154">In hello **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** tooinstall hello **Microsoft.Azure.Devices** package, and accept hello terms of use.</span></span> <span data-ttu-id="0a9bc-155">此程序下載、 安裝，並新增參考 toohello [Azure IoT 服務 SDK] [ lnk-nuget-service-sdk] NuGet 封裝和其相依性。</span><span class="sxs-lookup"><span data-stu-id="0a9bc-155">This procedure downloads, installs, and adds a reference toohello [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![NuGet 封裝管理員視窗][img-servicenuget]
1. <span data-ttu-id="0a9bc-157">新增下列 hello`using`在 hello hello 最上方的陳述式**Program.cs**檔案：</span><span class="sxs-lookup"><span data-stu-id="0a9bc-157">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
        using System.Threading;
        using Newtonsoft.Json;
1. <span data-ttu-id="0a9bc-158">新增下列欄位 toohello hello**程式**類別。</span><span class="sxs-lookup"><span data-stu-id="0a9bc-158">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="0a9bc-159">取代 hello hello 中樞在 hello 上一節中所建立的 IoT 中樞連接字串中的 hello 預留位置的值。</span><span class="sxs-lookup"><span data-stu-id="0a9bc-159">Replace hello placeholder value with hello IoT Hub connection string for hello hub that you created in hello previous section.</span></span>
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
1. <span data-ttu-id="0a9bc-160">新增下列方法 toohello hello**程式**類別：</span><span class="sxs-lookup"><span data-stu-id="0a9bc-160">Add hello following method toohello **Program** class:</span></span>
   
        static private async Task SetDesiredConfigurationAndQuery()
        {
            var twin = await registryManager.GetTwinAsync("myDeviceId");
            var patch = new {
                    properties = new {
                        desired = new {
                            telemetryConfig = new {
                                configId = Guid.NewGuid().ToString(),
                                sendFrequency = "5m"
                            }
                        }
                    }
                };
   
            await registryManager.UpdateTwinAsync(twin.DeviceId, JsonConvert.SerializeObject(patch), twin.ETag);
            Console.WriteLine("Updated desired configuration");
   
            while (true)
            {
                var query = registryManager.CreateQuery("SELECT * FROM devices WHERE deviceId = 'myDeviceId'");
                var results = await query.GetNextAsTwinAsync();
                foreach (var result in results)
                {
                    Console.WriteLine("Config report for: {0}", result.DeviceId);
                    Console.WriteLine("Desired telemetryConfig: {0}", JsonConvert.SerializeObject(result.Properties.Desired["telemetryConfig"], Formatting.Indented));
                    Console.WriteLine("Reported telemetryConfig: {0}", JsonConvert.SerializeObject(result.Properties.Reported["telemetryConfig"], Formatting.Indented));
                    Console.WriteLine();
                }
                Thread.Sleep(10000);
            }
        }
   
    <span data-ttu-id="0a9bc-161">hello**登錄**物件會公開與裝置雙 hello 服務從所有 hello 方法 toointeract 必要。</span><span class="sxs-lookup"><span data-stu-id="0a9bc-161">hello **Registry** object exposes all hello methods required toointeract with device twins from hello service.</span></span> <span data-ttu-id="0a9bc-162">這個程式碼初始化 hello**登錄**物件，擷取 hello 的裝置兩個**myDeviceId**，然後使用新的遙測組態物件中更新其所需的屬性。</span><span class="sxs-lookup"><span data-stu-id="0a9bc-162">This code initializes hello **Registry** object, retrieves hello device twin for **myDeviceId**, and then updates its desired properties with a new telemetry configuration object.</span></span>
    <span data-ttu-id="0a9bc-163">之後，它會查詢 hello 裝置雙儲存在 hello IoT 中樞每隔 10 秒鐘，而想要的沖印 hello，與回報遙測組態。</span><span class="sxs-lookup"><span data-stu-id="0a9bc-163">After that, it queries hello device twins stored in hello IoT hub every 10 seconds, and prints hello desired and reported telemetry configurations.</span></span> <span data-ttu-id="0a9bc-164">請參閱 toohello [IoT 中樞的查詢語言][ lnk-query] toolearn toogenerate 豐富報告的方式，跨所有裝置。</span><span class="sxs-lookup"><span data-stu-id="0a9bc-164">Refer toohello [IoT Hub query language][lnk-query] toolearn how toogenerate rich reports across all your devices.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="0a9bc-165">為了便於說明，此應用程式每 10 秒查詢一次 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="0a9bc-165">This application queries IoT Hub every 10 seconds for illustrative purposes.</span></span> <span data-ttu-id="0a9bc-166">使用跨許多裝置和非 toodetect 變更查詢 toogenerate 面對使用者的報表。</span><span class="sxs-lookup"><span data-stu-id="0a9bc-166">Use queries toogenerate user-facing reports across many devices, and not toodetect changes.</span></span> <span data-ttu-id="0a9bc-167">如果您的解決方案需要裝置事件的即時通知，請使用[對應項通知][lnk-twin-notifications]。</span><span class="sxs-lookup"><span data-stu-id="0a9bc-167">If your solution requires real-time notifications of device events, use [twin notifications][lnk-twin-notifications].</span></span>
   > 
   > 
1. <span data-ttu-id="0a9bc-168">最後，加入下列行 toohello hello **Main**方法：</span><span class="sxs-lookup"><span data-stu-id="0a9bc-168">Finally, add hello following lines toohello **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        SetDesiredConfigurationAndQuery();
        Console.WriteLine("Press any key tooquit.");
        Console.ReadLine();
1. <span data-ttu-id="0a9bc-169">在 hello 方案總管 中，開啟 hello**設定啟始專案...** ，請確定 hello**動作**如**SetDesiredConfigurationAndQuery**專案是**啟動**。</span><span class="sxs-lookup"><span data-stu-id="0a9bc-169">In hello Solution Explorer, open hello **Set StartUp projects...** and make sure hello **Action** for **SetDesiredConfigurationAndQuery** project is **Start**.</span></span> <span data-ttu-id="0a9bc-170">建置 hello 方案。</span><span class="sxs-lookup"><span data-stu-id="0a9bc-170">Build hello solution.</span></span>
1. <span data-ttu-id="0a9bc-171">與**SimulateDeviceConfiguration**裝置應用程式執行的執行的 hello 服務應用程式，從 Visual Studio 使用**F5**。</span><span class="sxs-lookup"><span data-stu-id="0a9bc-171">With **SimulateDeviceConfiguration** device app running, run hello service app from Visual Studio using **F5**.</span></span> <span data-ttu-id="0a9bc-172">您應該會看見 hello 報告的設定，變更從**暫止**太**成功**傳送 hello 新使用中而不是 24 小時的五分鐘的頻率。</span><span class="sxs-lookup"><span data-stu-id="0a9bc-172">You should see hello reported configuration change from **Pending** too**Success** with hello new active send frequency of five minutes instead of 24 hours.</span></span>

 ![已成功設定裝置][img-deviceconfigured]
   
   > [!IMPORTANT]
   > <span data-ttu-id="0a9bc-174">沒有向上 tooa 分鐘 hello 裝置報告作業和 hello 查詢結果之間的延遲。</span><span class="sxs-lookup"><span data-stu-id="0a9bc-174">There is a delay of up tooa minute between hello device report operation and hello query result.</span></span> <span data-ttu-id="0a9bc-175">這是 tooenable hello 查詢在極高的小數位數的基礎結構 toowork。</span><span class="sxs-lookup"><span data-stu-id="0a9bc-175">This is tooenable hello query infrastructure toowork at very high scale.</span></span> <span data-ttu-id="0a9bc-176">tooretrieve 一致檢視的單一裝置的兩個使用 hello **getDeviceTwin**方法在 hello**登錄**類別。</span><span class="sxs-lookup"><span data-stu-id="0a9bc-176">tooretrieve consistent views of a single device twin use hello **getDeviceTwin** method in hello **Registry** class.</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="0a9bc-177">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0a9bc-177">Next steps</span></span>
<span data-ttu-id="0a9bc-178">在本教學課程中，您可以設定為所需的組態*所需屬性*hello 方案從備份結束時，和寫入裝置的應用程式 toodetect 的變更，並模擬報告其狀態報告的 hello 透過多個步驟更新程序屬性。</span><span class="sxs-lookup"><span data-stu-id="0a9bc-178">In this tutorial, you set a desired configuration as *desired properties* from hello solution back end, and wrote a device app toodetect that change and simulate a multi-step update process reporting its status through hello reported properties.</span></span>

<span data-ttu-id="0a9bc-179">下列資源 toolearn 如何使用 hello 至：</span><span class="sxs-lookup"><span data-stu-id="0a9bc-179">Use hello following resources toolearn how to:</span></span>

* <span data-ttu-id="0a9bc-180">從以 hello 的裝置將遙測傳送[開始使用 IoT 中樞][ lnk-iothub-getstarted]教學課程中，</span><span class="sxs-lookup"><span data-stu-id="0a9bc-180">send telemetry from devices with hello [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="0a9bc-181">排程執行，或是執行大量的裝置上的作業，請參閱 「 hello[排程和廣播的工作][ lnk-schedule-jobs]教學課程。</span><span class="sxs-lookup"><span data-stu-id="0a9bc-181">schedule or perform operations on large sets of devices see hello [Schedule and broadcast jobs][lnk-schedule-jobs] tutorial.</span></span>
* <span data-ttu-id="0a9bc-182">控制裝置以互動方式 （例如開啟風扇從使用者控制的應用程式），以 hello[使用直接的方法][ lnk-methods-tutorial]教學課程。</span><span class="sxs-lookup"><span data-stu-id="0a9bc-182">control devices interactively (such as turning on a fan from a user-controlled app), with hello [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-csharp-twin-how-to-configure/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-csharp-twin-how-to-configure/createnetapp.png
[img-deviceconfigured]: media/iot-hub-csharp-csharp-twin-how-to-configure/deviceconfigured.png
[img-createdeviceapp]: media/iot-hub-csharp-csharp-twin-how-to-configure/createdeviceapp.png
[img-clientnuget]: media/iot-hub-csharp-csharp-twin-how-to-configure/devicesdknuget.png
[img-deviceconfigured]: media/iot-hub-csharp-csharp-twin-how-to-configure/deviceconfigured.png


<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-nuget-client-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices.Client/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/1.1.0/

[lnk-query]: iot-hub-devguide-query-language.md
[lnk-twin-notifications]: iot-hub-devguide-device-twins.md#back-end-operations
[lnk-twin-tutorial]: iot-hub-csharp-csharp-twin-getstarted.md
[lnk-schedule-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-iothub-getstarted]: iot-hub-csharp-csharp-getstarted.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-how-to-configure-createapp]: iot-hub-csharp-csharp-twin-how-to-configure.md#create-the-simulated-device-app
