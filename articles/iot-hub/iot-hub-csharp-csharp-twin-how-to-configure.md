---
title: "使用 Azure IoT 中樞裝置對應項屬性 (.NET/.NET) | Microsoft Docs"
description: "如何使用 Azure IoT 中樞裝置對應項來設定裝置。 您可以使用適用於 .NET 的 Azure IoT 裝置 SDK，實作模擬裝置應用程式，也可以使用適用於 .NET 的 Azure IoT 服務 SDK，實作服務應用程式，以修改使用裝置對應項的裝置設定。"
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
ms.openlocfilehash: 679cda28bf3ce9fb207fe3693a3453b355f1de15
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/29/2017
---
# <a name="use-desired-properties-to-configure-devices"></a><span data-ttu-id="54516-104">使用所需屬性來設定裝置</span><span class="sxs-lookup"><span data-stu-id="54516-104">Use desired properties to configure devices</span></span>
[!INCLUDE [iot-hub-selector-twin-how-to-configure](../../includes/iot-hub-selector-twin-how-to-configure.md)]

<span data-ttu-id="54516-105">在本教學課程結尾，您將會有兩個 .NET 主控台應用程式：</span><span class="sxs-lookup"><span data-stu-id="54516-105">At the end of this tutorial, you will have two .NET console apps:</span></span>

* <span data-ttu-id="54516-106">**SimulateDeviceConfiguration**，這是模擬裝置應用程式，可等候所需的設定更新，並報告模擬設定更新程序的狀態。</span><span class="sxs-lookup"><span data-stu-id="54516-106">**SimulateDeviceConfiguration**, a simulated device app that waits for a desired configuration update and reports the status of a simulated configuration update process.</span></span>
* <span data-ttu-id="54516-107">**SetDesiredConfigurationAndQuery**，這是後端應用程式，可在裝置上設定所需的設定，並查詢設定更新程序。</span><span class="sxs-lookup"><span data-stu-id="54516-107">**SetDesiredConfigurationAndQuery**, a back-end app, which sets the desired configuration on a device and queries the configuration update process.</span></span>

> [!NOTE]
> <span data-ttu-id="54516-108">[Azure IoT SDK][lnk-hub-sdks] 一文提供可用來建置裝置和後端應用程式之 Azure IoT SDK 的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="54516-108">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="54516-109">若要完成此教學課程，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="54516-109">To complete this tutorial you need the following:</span></span>

* <span data-ttu-id="54516-110">Visual Studio 2015 或 Visual Studio 2017。</span><span class="sxs-lookup"><span data-stu-id="54516-110">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="54516-111">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="54516-111">An active Azure account.</span></span> <span data-ttu-id="54516-112">如果您沒有帳戶，只需要幾分鐘的時間就可以建立[免費帳戶][lnk-free-trial]。</span><span class="sxs-lookup"><span data-stu-id="54516-112">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>

<span data-ttu-id="54516-113">如果您遵循[開始使用裝置對應項][lnk-twin-tutorial]教學課程進行，您便已經有一個 IoT 中樞和一個稱為 **myDeviceId** 的裝置身分識別。</span><span class="sxs-lookup"><span data-stu-id="54516-113">If you followed the [Get started with device twins][lnk-twin-tutorial] tutorial, you already have an IoT hub and a device identity called **myDeviceId**.</span></span> <span data-ttu-id="54516-114">在該情況下，您可以直接跳到[建立模擬裝置應用程式][lnk-how-to-configure-createapp]一節。</span><span class="sxs-lookup"><span data-stu-id="54516-114">In that case, you can skip to the [Create the simulated device app][lnk-how-to-configure-createapp] section.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

<a id="#create-the-simulated-device-app"></a>
## <a name="create-the-simulated-device-app"></a><span data-ttu-id="54516-115">建立模擬裝置應用程式</span><span class="sxs-lookup"><span data-stu-id="54516-115">Create the simulated device app</span></span>
<span data-ttu-id="54516-116">在本節中，您將建立 .NET 主控台應用程式，此應用程式會以 **myDeviceId** 連接到您的中樞、等候所需的設定更新，然後報告模擬設定更新程序上的更新。</span><span class="sxs-lookup"><span data-stu-id="54516-116">In this section, you create a .NET console app that connects to your hub as **myDeviceId**, waits for a desired configuration update and then reports updates on the simulated configuration update process.</span></span>

1. <span data-ttu-id="54516-117">在 Visual Studio 中，使用 [主控台應用程式] 專案範本，建立新的 Visual C# Windows 傳統桌面專案。</span><span class="sxs-lookup"><span data-stu-id="54516-117">In Visual Studio, create a new Visual C# Windows Classic Desktop project by using the **Console Application** project template.</span></span> <span data-ttu-id="54516-118">將專案命名為 **SimulateDeviceConfiguration**。</span><span class="sxs-lookup"><span data-stu-id="54516-118">Name the project **SimulateDeviceConfiguration**.</span></span>
   
    ![新的 Visual C# Windows 傳統裝置應用程式][img-createdeviceapp]

1. <span data-ttu-id="54516-120">在方案總管中，以滑鼠右鍵按一下 **SimulateDeviceConfiguration** 專案，然後按一下 [管理 NuGet 套件...]。</span><span class="sxs-lookup"><span data-stu-id="54516-120">In Solution Explorer, right-click the **SimulateDeviceConfiguration** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="54516-121">在 [NuGet 套件管理員] 視窗中，選取 [瀏覽]，並搜尋 **microsoft.azure.devices.client**。</span><span class="sxs-lookup"><span data-stu-id="54516-121">In the **NuGet Package Manager** window, select **Browse** and search for **microsoft.azure.devices.client**.</span></span> <span data-ttu-id="54516-122">選取 [安裝] 來安裝 **Microsoft.Azure.Devices.Client** 套件，並接受使用規定。</span><span class="sxs-lookup"><span data-stu-id="54516-122">Select **Install** to install the **Microsoft.Azure.Devices.Client** package, and accept the terms of use.</span></span> <span data-ttu-id="54516-123">此程序會下載及安裝 [Azure IoT 裝置 SDK][lnk-nuget-client-sdk] NuGet 套件與其相依項目，並新增對它的參考。</span><span class="sxs-lookup"><span data-stu-id="54516-123">This procedure downloads, installs, and adds a reference to the [Azure IoT device SDK][lnk-nuget-client-sdk] NuGet package and its dependencies.</span></span>
   
    ![NuGet 套件管理員視窗用戶端應用程式][img-clientnuget]
1. <span data-ttu-id="54516-125">在 **Program.cs** 檔案開頭處新增下列 `using` 陳述式：</span><span class="sxs-lookup"><span data-stu-id="54516-125">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices.Client;
        using Microsoft.Azure.Devices.Shared;
        using Newtonsoft.Json;

1. <span data-ttu-id="54516-126">將下列欄位新增到 **Program** 類別。</span><span class="sxs-lookup"><span data-stu-id="54516-126">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="54516-127">將預留位置的值取代為您在上一節中所記下的裝置連接字串。</span><span class="sxs-lookup"><span data-stu-id="54516-127">Replace the placeholder value with the device connection string that you noted in the previous section.</span></span>
   
        static string DeviceConnectionString = "HostName=<yourIotHubName>.azure-devices.net;DeviceId=<yourIotDeviceName>;SharedAccessKey=<yourIotDeviceAccessKey>";
        static DeviceClient Client = null;
        static TwinCollection reportedProperties = new TwinCollection();

1. <span data-ttu-id="54516-128">將下列方法加入至 **Program** 類別：</span><span class="sxs-lookup"><span data-stu-id="54516-128">Add the following method to the **Program** class:</span></span>
 
        public static void InitClient()
        {
            try
            {
                Console.WriteLine("Connecting to hub");
                Client = DeviceClient.CreateFromConnectionString(DeviceConnectionString, TransportType.Mqtt);
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }
    <span data-ttu-id="54516-129">**Client** 物件會公開從裝置來與裝置對應項進行互動時所需的所有方法。</span><span class="sxs-lookup"><span data-stu-id="54516-129">The **Client** object exposes all the methods you require to interact with device twins from the device.</span></span> <span data-ttu-id="54516-130">以上所示的程式碼會初始化**用戶端**物件，然後擷取 **myDeviceId** 的裝置對應項。</span><span class="sxs-lookup"><span data-stu-id="54516-130">The code shown above, initializes the **Client** object, and then retrieves the device twin for **myDeviceId**.</span></span>

1. <span data-ttu-id="54516-131">將下列方法新增至 **Program** 類別。</span><span class="sxs-lookup"><span data-stu-id="54516-131">Add the following method to the **Program** class.</span></span> <span data-ttu-id="54516-132">這個方法會設定本機裝置上的遙測資料起始值，然後更新裝置對應項。</span><span class="sxs-lookup"><span data-stu-id="54516-132">This method sets the initial values of telemetry on the local device and then updates the device twin.</span></span>

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

1. <span data-ttu-id="54516-133">將下列方法新增至 **Program** 類別。</span><span class="sxs-lookup"><span data-stu-id="54516-133">Add the following method to the **Program** class.</span></span> <span data-ttu-id="54516-134">這是會在裝置對應項中偵測到「所需屬性」變更的回呼。</span><span class="sxs-lookup"><span data-stu-id="54516-134">This is a callback which will detect a change in *desired properties* in the device twin.</span></span>

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

    <span data-ttu-id="54516-135">此方法會依設定更新要求，在本機裝置對應項物件上更新所報告的屬性，並將狀態設為 **Pending**，然後更新服務上的裝置對應項。</span><span class="sxs-lookup"><span data-stu-id="54516-135">This method updates the reported properties on the local device twin object with the configuration update request and sets the status to **Pending**, then updates the device twin on the service.</span></span> <span data-ttu-id="54516-136">成功更新裝置對應項之後，就會呼叫下一個點中所述的方法 `CompleteConfigChange`，完成設定變更。</span><span class="sxs-lookup"><span data-stu-id="54516-136">After successfully updating the device twin, it completes the config change by calling the method `CompleteConfigChange` described in the next point.</span></span>

1. <span data-ttu-id="54516-137">將下列方法新增至 **Program** 類別。</span><span class="sxs-lookup"><span data-stu-id="54516-137">Add the following method to the **Program** class.</span></span> <span data-ttu-id="54516-138">這個方法會模擬裝置重設，然後更新本機回報屬性，將狀態設定為 **Success**，並移除 **pendingConfig** 項目。</span><span class="sxs-lookup"><span data-stu-id="54516-138">This method simulates a device reset, then updates the local reported properties setting the status to **Success** and removes the **pendingConfig** element.</span></span> <span data-ttu-id="54516-139">然後更新服務上的裝置對應項。</span><span class="sxs-lookup"><span data-stu-id="54516-139">It then updates the device twin on the service.</span></span> 

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
                Console.WriteLine("Config change complete \nPress any key to exit.");
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

1. <span data-ttu-id="54516-140">最後，將下列幾行新增至 **Main** 方法：</span><span class="sxs-lookup"><span data-stu-id="54516-140">Finally add the following lines to the **Main** method:</span></span>

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
   > <span data-ttu-id="54516-141">本教學課程不會模擬並行組態更新的任何行為。</span><span class="sxs-lookup"><span data-stu-id="54516-141">This tutorial does not simulate any behavior for concurrent configuration updates.</span></span> <span data-ttu-id="54516-142">某些組態更新程序可能在更新執行時能夠接受目標組態的變更，部分程序可能必須將變更排入佇列，還有部分程序可能會因錯誤條件而拒絕變更。</span><span class="sxs-lookup"><span data-stu-id="54516-142">Some configuration update processes might be able to accommodate changes of target configuration while the update is running, some might have to queue them, and some could reject them with an error condition.</span></span> <span data-ttu-id="54516-143">請務必考慮您的特定程序所需的行為，並在初始化組態變更之前新增適當的邏輯。</span><span class="sxs-lookup"><span data-stu-id="54516-143">Make sure to consider the desired behavior for your specific configuration process, and add the appropriate logic before initiating the configuration change.</span></span>
   > 
   > 
1. <span data-ttu-id="54516-144">建置方案，然後按一下 **F5** 從 Visual Studio 執行裝置應用程式。</span><span class="sxs-lookup"><span data-stu-id="54516-144">Build the solution and then run the device app from Visual Studio by clicking **F5**.</span></span> <span data-ttu-id="54516-145">在輸出主控台上，應該會有訊息指出：您模擬的裝置正在擷取裝置對應項、設定遙測資料和等候所需的屬性變更。</span><span class="sxs-lookup"><span data-stu-id="54516-145">On the output console, you should see the messages indicating that your simulated device is retrieving the device twin, setting up the telemetry, and waiting for desired property change.</span></span> <span data-ttu-id="54516-146">保持應用程式執行。</span><span class="sxs-lookup"><span data-stu-id="54516-146">Keep the app running.</span></span>

## <a name="create-the-service-app"></a><span data-ttu-id="54516-147">建立服務應用程式</span><span class="sxs-lookup"><span data-stu-id="54516-147">Create the service app</span></span>
<span data-ttu-id="54516-148">在本節中，您將建立 .NET 主控台應用程式，在與 **myDeviceId** 相關聯的裝置對應項上，以新的遙測組態物件來更新「所需屬性」。</span><span class="sxs-lookup"><span data-stu-id="54516-148">In this section, you will create a .NET console app that updates the *desired properties* on the device twin associated with **myDeviceId** with a new telemetry configuration object.</span></span> <span data-ttu-id="54516-149">然後，它會查詢儲存在 IoT 中樞的裝置對應項，並顯示裝置的所需和所報告組態之間的差異。</span><span class="sxs-lookup"><span data-stu-id="54516-149">It then queries the device twins stored in the IoT hub and shows the difference between the desired and reported configurations of the device.</span></span>

1. <span data-ttu-id="54516-150">在 Visual Studio 中，使用 [主控台應用程式] 專案範本，將 Visual C# Windows 傳統桌面專案新增至目前的方案。</span><span class="sxs-lookup"><span data-stu-id="54516-150">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution by using the **Console Application** project template.</span></span> <span data-ttu-id="54516-151">將專案命名為 **SetDesiredConfigurationAndQuery**。</span><span class="sxs-lookup"><span data-stu-id="54516-151">Name the project **SetDesiredConfigurationAndQuery**.</span></span>
   
    ![新的 Visual C# Windows 傳統桌面專案][img-createapp]
1. <span data-ttu-id="54516-153">在 [方案總管] 中，以滑鼠右鍵按一下 **SetDesiredConfigurationAndQuery** 專案，然後按一下 [管理 NuGet 套件...]。</span><span class="sxs-lookup"><span data-stu-id="54516-153">In Solution Explorer, right-click the **SetDesiredConfigurationAndQuery** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="54516-154">在 [Nuget 套件管理員] 視窗中選取 [瀏覽]、搜尋 **microsoft.azure.devices**、選取 [安裝] 以安裝 **Microsoft.Azure.Devices** 套件，並接受使用規定。</span><span class="sxs-lookup"><span data-stu-id="54516-154">In the **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** to install the **Microsoft.Azure.Devices** package, and accept the terms of use.</span></span> <span data-ttu-id="54516-155">此程序會下載及安裝 [Azure IoT 服務 SDK][lnk-nuget-service-sdk] NuGet 套件與其相依項目，並新增對它的參考。</span><span class="sxs-lookup"><span data-stu-id="54516-155">This procedure downloads, installs, and adds a reference to the [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![NuGet 套件管理員視窗][img-servicenuget]
1. <span data-ttu-id="54516-157">在 **Program.cs** 檔案開頭處新增下列 `using` 陳述式：</span><span class="sxs-lookup"><span data-stu-id="54516-157">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
        using System.Threading;
        using Newtonsoft.Json;
1. <span data-ttu-id="54516-158">將下列欄位新增到 **Program** 類別。</span><span class="sxs-lookup"><span data-stu-id="54516-158">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="54516-159">將預留位置的值替換為您在上一節中為中樞所建立的 IoT 中樞連接字串。</span><span class="sxs-lookup"><span data-stu-id="54516-159">Replace the placeholder value with the IoT Hub connection string for the hub that you created in the previous section.</span></span>
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
1. <span data-ttu-id="54516-160">將下列方法加入至 **Program** 類別：</span><span class="sxs-lookup"><span data-stu-id="54516-160">Add the following method to the **Program** class:</span></span>
   
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
   
    <span data-ttu-id="54516-161">**Registry** 物件會公開從服務來與裝置對應項進行互動時所需的所有方法。</span><span class="sxs-lookup"><span data-stu-id="54516-161">The **Registry** object exposes all the methods required to interact with device twins from the service.</span></span> <span data-ttu-id="54516-162">此程式碼會初始化 **Registry** 物件，擷取 **myDeviceId** 的裝置對應項，然後以新的遙測組態物件來更新其所需屬性。</span><span class="sxs-lookup"><span data-stu-id="54516-162">This code initializes the **Registry** object, retrieves the device twin for **myDeviceId**, and then updates its desired properties with a new telemetry configuration object.</span></span>
    <span data-ttu-id="54516-163">之後，它每隔 10 秒就會查詢儲存在 IoT 中樞的裝置對應項，並列印所需和所報告的遙測組態。</span><span class="sxs-lookup"><span data-stu-id="54516-163">After that, it queries the device twins stored in the IoT hub every 10 seconds, and prints the desired and reported telemetry configurations.</span></span> <span data-ttu-id="54516-164">請參閱 [IoT 中樞查詢語言][lnk-query]，以了解如何產生跨所有裝置的實用報告。</span><span class="sxs-lookup"><span data-stu-id="54516-164">Refer to the [IoT Hub query language][lnk-query] to learn how to generate rich reports across all your devices.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="54516-165">為了便於說明，此應用程式每 10 秒查詢一次 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="54516-165">This application queries IoT Hub every 10 seconds for illustrative purposes.</span></span> <span data-ttu-id="54516-166">跨許多裝置時，請使用查詢來產生適合使用者的報告，而非偵測變更。</span><span class="sxs-lookup"><span data-stu-id="54516-166">Use queries to generate user-facing reports across many devices, and not to detect changes.</span></span> <span data-ttu-id="54516-167">如果您的解決方案需要裝置事件的即時通知，請使用[對應項通知][lnk-twin-notifications]。</span><span class="sxs-lookup"><span data-stu-id="54516-167">If your solution requires real-time notifications of device events, use [twin notifications][lnk-twin-notifications].</span></span>
   > 
   > 
1. <span data-ttu-id="54516-168">最後，將下列幾行新增至 **Main** 方法：</span><span class="sxs-lookup"><span data-stu-id="54516-168">Finally, add the following lines to the **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        SetDesiredConfigurationAndQuery();
        Console.WriteLine("Press any key to quit.");
        Console.ReadLine();
1. <span data-ttu-id="54516-169">在 [方案總管] 中，開啟 [設定起始專案...]，並確定 **SetDesiredConfigurationAndQuery** 專案的 [動作] 是 [啟動]。</span><span class="sxs-lookup"><span data-stu-id="54516-169">In the Solution Explorer, open the **Set StartUp projects...** and make sure the **Action** for **SetDesiredConfigurationAndQuery** project is **Start**.</span></span> <span data-ttu-id="54516-170">建置方案。</span><span class="sxs-lookup"><span data-stu-id="54516-170">Build the solution.</span></span>
1. <span data-ttu-id="54516-171">在 **SimulateDeviceConfiguration** 裝置應用程式執行的狀態下，使用 **F5** 從 Visual Studio 執行服務應用程式。</span><span class="sxs-lookup"><span data-stu-id="54516-171">With **SimulateDeviceConfiguration** device app running, run the service app from Visual Studio using **F5**.</span></span> <span data-ttu-id="54516-172">您應該會看到回報的設定從 **Pending** 變更成 **Success**，作用中的新傳送頻率是五分鐘，而不是 24 小時。</span><span class="sxs-lookup"><span data-stu-id="54516-172">You should see the reported configuration change from **Pending** to **Success** with the new active send frequency of five minutes instead of 24 hours.</span></span>

 ![已成功設定裝置][img-deviceconfigured]
   
   > [!IMPORTANT]
   > <span data-ttu-id="54516-174">裝置報告作業和查詢結果之間的延遲最多一分鐘。</span><span class="sxs-lookup"><span data-stu-id="54516-174">There is a delay of up to a minute between the device report operation and the query result.</span></span> <span data-ttu-id="54516-175">這是為了讓查詢基礎結構能夠以非常高的延展性運作。</span><span class="sxs-lookup"><span data-stu-id="54516-175">This is to enable the query infrastructure to work at very high scale.</span></span> <span data-ttu-id="54516-176">若要擷取單一裝置對應項的一致檢視，請使用 **Registry** 類別中的 **getDeviceTwin** 方法。</span><span class="sxs-lookup"><span data-stu-id="54516-176">To retrieve consistent views of a single device twin use the **getDeviceTwin** method in the **Registry** class.</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="54516-177">後續步驟</span><span class="sxs-lookup"><span data-stu-id="54516-177">Next steps</span></span>
<span data-ttu-id="54516-178">在本教學課程中，您將會從解決方案後端將所需的組態設為「所需屬性」，還會撰寫裝置應用程式來偵測該變更並模擬多步驟更新程序，以透過報告屬性來回報其狀態。</span><span class="sxs-lookup"><span data-stu-id="54516-178">In this tutorial, you set a desired configuration as *desired properties* from the solution back end, and wrote a device app to detect that change and simulate a multi-step update process reporting its status through the reported properties.</span></span>

<span data-ttu-id="54516-179">使用下列資源來了解如何：</span><span class="sxs-lookup"><span data-stu-id="54516-179">Use the following resources to learn how to:</span></span>

* <span data-ttu-id="54516-180">從裝置傳送遙測，請參閱[開始使用 IoT 中樞][lnk-iothub-getstarted]教學課程，</span><span class="sxs-lookup"><span data-stu-id="54516-180">send telemetry from devices with the [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="54516-181">在大量裝置上排定或執行作業，請參閱[排定及廣播作業][lnk-schedule-jobs]教學課程。</span><span class="sxs-lookup"><span data-stu-id="54516-181">schedule or perform operations on large sets of devices see the [Schedule and broadcast jobs][lnk-schedule-jobs] tutorial.</span></span>
* <span data-ttu-id="54516-182">以互動方式控制裝置 (例如，從使用者控制的應用程式開啟風扇)，請參閱[使用直接方法][lnk-methods-tutorial]教學課程。</span><span class="sxs-lookup"><span data-stu-id="54516-182">control devices interactively (such as turning on a fan from a user-controlled app), with the [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

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
