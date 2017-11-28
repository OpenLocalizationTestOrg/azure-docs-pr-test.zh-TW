---
title: "開始使用 Azure IoT 中樞裝置對應項 (.NET/.NET) | Microsoft Docs"
description: "如何使用 Azure IoT 中樞裝置對應項來新增標籤，然後使用 IoT 中樞查詢。 您可以使用適用於 .NET 的 Azure IoT 裝置 SDK，實作模擬的裝置應用程式，也可以使用適用於 .NET 的 Azure IoT 服務 SDK，實作服務應用程式，以新增標籤和執行 IoT 中樞查詢。"
services: iot-hub
documentationcenter: node
author: dsk-2015
manager: timlt
editor: 
ms.assetid: f7e23b6e-bfde-4fba-a6ec-dbb0f0e005f4
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: dkshir
ms.openlocfilehash: 6073d594117e69676b753a1e3af25fffa3583a2b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-device-twins-netnet"></a><span data-ttu-id="e3a56-104">開始使用裝置對應項 (.NET/.NET)</span><span class="sxs-lookup"><span data-stu-id="e3a56-104">Get started with device twins (.NET/.NET)</span></span>
[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

<span data-ttu-id="e3a56-105">在本教學課程結尾，您將會有下列 .NET 主控台應用程式：</span><span class="sxs-lookup"><span data-stu-id="e3a56-105">At the end of this tutorial, you will have these .NET console apps:</span></span>

* <span data-ttu-id="e3a56-106">**CreateDeviceIdentity**，這是 .NET 應用程式，可建立裝置識別與相關聯的安全性金鑰，來連線到您的模擬裝置應用程式。</span><span class="sxs-lookup"><span data-stu-id="e3a56-106">**CreateDeviceIdentity**, a .NET app which creates a device identity and associated security key to connect your simulated device app.</span></span>
* <span data-ttu-id="e3a56-107">**AddTagsAndQuery**，這是 .NET 後端應用程式，可新增標籤和查詢裝置對應項。</span><span class="sxs-lookup"><span data-stu-id="e3a56-107">**AddTagsAndQuery**, a .NET back-end app which adds tags and queries device twins.</span></span>
* <span data-ttu-id="e3a56-108">**ReportConnectivity**，這是會模擬裝置的 .NET 裝置應用程式，此裝置會以稍早建立的裝置識別連線到您的 IoT 中樞，並報告其連線狀況。</span><span class="sxs-lookup"><span data-stu-id="e3a56-108">**ReportConnectivity**, a .NET device app which simulates a device that connects to your IoT hub with the device identity created earlier, and reports its connectivity condition.</span></span>

> [!NOTE]
> <span data-ttu-id="e3a56-109">[Azure IoT SDK][lnk-hub-sdks] 一文提供可用來建置裝置和後端應用程式之 Azure IoT SDK 的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="e3a56-109">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="e3a56-110">若要完成此教學課程，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="e3a56-110">To complete this tutorial you need the following:</span></span>

* <span data-ttu-id="e3a56-111">Visual Studio 2015 或 Visual Studio 2017。</span><span class="sxs-lookup"><span data-stu-id="e3a56-111">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="e3a56-112">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="e3a56-112">An active Azure account.</span></span> <span data-ttu-id="e3a56-113">(如果您沒有帳戶，只需要幾分鐘的時間就可以建立[免費帳戶][lnk-free-trial]。)</span><span class="sxs-lookup"><span data-stu-id="e3a56-113">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

<span data-ttu-id="e3a56-114">如果您想要改為以程式設計方式建立裝置識別，請閱讀[使用 .NET 將您的模擬裝置連線至 IoT 中樞][lnk-device-identity-csharp]一文中的對應章節。</span><span class="sxs-lookup"><span data-stu-id="e3a56-114">If you want to create the device identity programmatically instead, read the corresponding section in the [Connect your simulated device to your IoT hub using .NET][lnk-device-identity-csharp] article.</span></span>

## <a name="create-the-service-app"></a><span data-ttu-id="e3a56-115">建立服務應用程式</span><span class="sxs-lookup"><span data-stu-id="e3a56-115">Create the service app</span></span>
<span data-ttu-id="e3a56-116">在本節中，您將 (使用 C#) 建立一個 .NET 主控台應用程式，此應用程式會將位置中繼資料新增至與 **myDeviceId** 相關聯的裝置對應項。</span><span class="sxs-lookup"><span data-stu-id="e3a56-116">In this section, you create a .NET console app (using C#) that adds location metadata to the device twin associated with **myDeviceId**.</span></span> <span data-ttu-id="e3a56-117">接著，它會選取位於美國的裝置來查詢儲存在 IoT 中樞的裝置對應項，再查詢會報告行動電話連線的對應項。</span><span class="sxs-lookup"><span data-stu-id="e3a56-117">It then queries the device twins stored in the IoT hub selecting the devices located in the US, and then the ones that reported a cellular connection.</span></span>

1. <span data-ttu-id="e3a56-118">在 Visual Studio 中，使用 [主控台應用程式] 專案範本，將 Visual C# Windows 傳統桌面專案新增至目前的方案。</span><span class="sxs-lookup"><span data-stu-id="e3a56-118">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution by using the **Console Application** project template.</span></span> <span data-ttu-id="e3a56-119">將專案命名為 **AddTagsAndQuery**。</span><span class="sxs-lookup"><span data-stu-id="e3a56-119">Name the project **AddTagsAndQuery**.</span></span>
   
    ![新的 Visual C# Windows 傳統桌面專案][img-createapp]
1. <span data-ttu-id="e3a56-121">在 [方案總管] 中，以滑鼠右鍵按一下 **AddTagsAndQuery** 專案，然後按一下 [管理 NuGet 套件...]。</span><span class="sxs-lookup"><span data-stu-id="e3a56-121">In Solution Explorer, right-click the **AddTagsAndQuery** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="e3a56-122">在 [NuGet 套件管理員] 視窗中，選取 [瀏覽]，並搜尋 **microsoft.azure.devices**。</span><span class="sxs-lookup"><span data-stu-id="e3a56-122">In the **NuGet Package Manager** window, select **Browse** and search for **microsoft.azure.devices**.</span></span> <span data-ttu-id="e3a56-123">選取 [安裝] 來安裝 **Microsoft.Azure.Devices** 套件，並接受使用規定。</span><span class="sxs-lookup"><span data-stu-id="e3a56-123">Select **Install** to install the **Microsoft.Azure.Devices** package, and accept the terms of use.</span></span> <span data-ttu-id="e3a56-124">此程序會下載及安裝 [Azure IoT 服務 SDK][lnk-nuget-service-sdk] NuGet 套件與其相依項目，並加入對它的參考。</span><span class="sxs-lookup"><span data-stu-id="e3a56-124">This procedure downloads, installs, and adds a reference to the [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![NuGet 套件管理員視窗][img-servicenuget]
1. <span data-ttu-id="e3a56-126">在 **Program.cs** 檔案開頭處新增下列 `using` 陳述式：</span><span class="sxs-lookup"><span data-stu-id="e3a56-126">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
1. <span data-ttu-id="e3a56-127">將下列欄位新增到 **Program** 類別。</span><span class="sxs-lookup"><span data-stu-id="e3a56-127">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="e3a56-128">將預留位置的值替換為您在上一節中為中樞所建立的 IoT 中樞連接字串。</span><span class="sxs-lookup"><span data-stu-id="e3a56-128">Replace the placeholder value with the IoT Hub connection string for the hub that you created in the previous section.</span></span>
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
1. <span data-ttu-id="e3a56-129">將下列方法加入至 **Program** 類別：</span><span class="sxs-lookup"><span data-stu-id="e3a56-129">Add the following method to the **Program** class:</span></span>
   
        public static async Task AddTagsAndQuery()
        {
            var twin = await registryManager.GetTwinAsync("myDeviceId");
            var patch =
                @"{
                    tags: {
                        location: {
                            region: 'US',
                            plant: 'Redmond43'
                        }
                    }
                }";
            await registryManager.UpdateTwinAsync(twin.DeviceId, patch, twin.ETag);
   
            var query = registryManager.CreateQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43'", 100);
            var twinsInRedmond43 = await query.GetNextAsTwinAsync();
            Console.WriteLine("Devices in Redmond43: {0}", string.Join(", ", twinsInRedmond43.Select(t => t.DeviceId)));
   
            query = registryManager.CreateQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43' AND properties.reported.connectivity.type = 'cellular'", 100);
            var twinsInRedmond43UsingCellular = await query.GetNextAsTwinAsync();
            Console.WriteLine("Devices in Redmond43 using cellular network: {0}", string.Join(", ", twinsInRedmond43UsingCellular.Select(t => t.DeviceId)));
        }
   
    <span data-ttu-id="e3a56-130">**RegistryManager** 類別會公開從服務來與裝置對應項進行互動時所需的所有方法。</span><span class="sxs-lookup"><span data-stu-id="e3a56-130">The **RegistryManager** class exposes all the methods required to interact with device twins from the service.</span></span> <span data-ttu-id="e3a56-131">先前的程式碼會先初始化 **registryManager** 物件，然後擷取 **myDeviceId** 的裝置對應項，最後會以所需的位置資訊來更新其標籤。</span><span class="sxs-lookup"><span data-stu-id="e3a56-131">The previous code first initializes the **registryManager** object, then retrieves the device twin for **myDeviceId**, and finally updates its tags with the desired location information.</span></span>
   
    <span data-ttu-id="e3a56-132">在更新後，它會執行兩個查詢：第一個只選取位於 **Redmond43** 工廠的裝置對應項，第二個會修改查詢，只選取也透過行動電話網路來連接的裝置。</span><span class="sxs-lookup"><span data-stu-id="e3a56-132">After updating, it executes two queries: the first selects only the device twins of devices located in the **Redmond43** plant, and the second refines the query to select only the devices that are also connected through cellular network.</span></span>
   
    <span data-ttu-id="e3a56-133">請注意，先前的程式碼在建立 **查詢** 物件時，指定傳回的最大文件數。</span><span class="sxs-lookup"><span data-stu-id="e3a56-133">Note that the previous code, when it creates the **query** object, specifies a maximum number of returned documents.</span></span> <span data-ttu-id="e3a56-134">**query** 物件包含 **HasMoreResults** 布林值屬性，可用來多次叫用 **GetNextAsTwinAsync** 方法以擷取所有結果。</span><span class="sxs-lookup"><span data-stu-id="e3a56-134">The **query** object contains a **HasMoreResults** boolean property that you can use to invoke the **GetNextAsTwinAsync** methods multiple times to retrieve all results.</span></span> <span data-ttu-id="e3a56-135">有一個稱為 **GetNextAsJson** 的方法適用於不是裝置對應項的結果，例如彙總查詢的結果。</span><span class="sxs-lookup"><span data-stu-id="e3a56-135">A method called **GetNextAsJson** is available for results that are not device twins, for example, results of aggregation queries.</span></span>
1. <span data-ttu-id="e3a56-136">最後，將下列幾行加入至 **Main** 方法：</span><span class="sxs-lookup"><span data-stu-id="e3a56-136">Finally, add the following lines to the **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        AddTagsAndQuery().Wait();
        Console.WriteLine("Press Enter to exit.");
        Console.ReadLine();

1. <span data-ttu-id="e3a56-137">在 [方案總管] 中，開啟 [設定起始專案...]，並確定 **AddTagsAndQuery** 專案的 [動作] 是 [啟動]。</span><span class="sxs-lookup"><span data-stu-id="e3a56-137">In the Solution Explorer, open the **Set StartUp projects...** and make sure the **Action** for **AddTagsAndQuery** project is **Start**.</span></span> <span data-ttu-id="e3a56-138">建置方案。</span><span class="sxs-lookup"><span data-stu-id="e3a56-138">Build the solution.</span></span>
1. <span data-ttu-id="e3a56-139">以滑鼠右鍵按一下 **AddTagsAndQuery** 專案，並選取 [偵錯]，後面接著 [開始新執行個體] 來執行此應用程式。</span><span class="sxs-lookup"><span data-stu-id="e3a56-139">Run this application by right-clicking on the **AddTagsAndQuery** project and selecting **Debug**, followed by **Start new instance**.</span></span> <span data-ttu-id="e3a56-140">如果是查詢所有位於 **Redmond43** 中的裝置，您在結果中會看到一個裝置，而如果查詢將結果限於使用行動電話網路的裝置，則您不會看到任何裝置。</span><span class="sxs-lookup"><span data-stu-id="e3a56-140">You should see one device in the results for the query asking for all devices located in **Redmond43** and none for the query that restricts the results to devices that use a cellular network.</span></span>
   
    ![視窗中的查詢結果][img-addtagapp]

<span data-ttu-id="e3a56-142">在下一節，您將建立一個裝置應用程式，以報告連線資訊並變更上一節的查詢結果。</span><span class="sxs-lookup"><span data-stu-id="e3a56-142">In the next section, you create a device app that reports the connectivity information and changes the result of the query in the previous section.</span></span>

## <a name="create-the-device-app"></a><span data-ttu-id="e3a56-143">建立裝置應用程式</span><span class="sxs-lookup"><span data-stu-id="e3a56-143">Create the device app</span></span>
<span data-ttu-id="e3a56-144">在本節中，您將建立一個 .NET 主控台應用程式，此應用程式會以 **myDeviceId** 來連線到您的中樞，然後更新其回報屬性，以包含資訊來指出目前使用行動電話通訊網路來連線。</span><span class="sxs-lookup"><span data-stu-id="e3a56-144">In this section, you create a .NET console app that connects to your hub as **myDeviceId**, and then updates its reported properties to contain the information that it is connected using a cellular network.</span></span>

1. <span data-ttu-id="e3a56-145">在 Visual Studio 中，使用 [主控台應用程式] 專案範本，將 Visual C# Windows 傳統桌面專案新增至目前的方案。</span><span class="sxs-lookup"><span data-stu-id="e3a56-145">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution by using the **Console Application** project template.</span></span> <span data-ttu-id="e3a56-146">將專案命名為 **ReportConnectivity**。</span><span class="sxs-lookup"><span data-stu-id="e3a56-146">Name the project **ReportConnectivity**.</span></span>
   
    ![新的 Visual C# Windows 傳統裝置應用程式][img-createdeviceapp]
    
1. <span data-ttu-id="e3a56-148">在方案總管中，以滑鼠右鍵按一下 **ReportConnectivity** 專案，然後按一下 [管理 NuGet 套件...]。</span><span class="sxs-lookup"><span data-stu-id="e3a56-148">In Solution Explorer, right-click the **ReportConnectivity** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="e3a56-149">在 [NuGet 套件管理員] 視窗中，選取 [瀏覽]，並搜尋 **microsoft.azure.devices.client**。</span><span class="sxs-lookup"><span data-stu-id="e3a56-149">In the **NuGet Package Manager** window, select **Browse** and search for **microsoft.azure.devices.client**.</span></span> <span data-ttu-id="e3a56-150">選取 [安裝] 來安裝 **Microsoft.Azure.Devices.Client** 套件，並接受使用規定。</span><span class="sxs-lookup"><span data-stu-id="e3a56-150">Select **Install** to install the **Microsoft.Azure.Devices.Client** package, and accept the terms of use.</span></span> <span data-ttu-id="e3a56-151">此程序會下載及安裝 [Azure IoT 裝置 SDK][lnk-nuget-client-sdk] NuGet 套件與其相依項目，並新增對它的參考。</span><span class="sxs-lookup"><span data-stu-id="e3a56-151">This procedure downloads, installs, and adds a reference to the [Azure IoT device SDK][lnk-nuget-client-sdk] NuGet package and its dependencies.</span></span>
   
    ![NuGet 套件管理員視窗用戶端應用程式][img-clientnuget]
1. <span data-ttu-id="e3a56-153">在 **Program.cs** 檔案開頭處新增下列 `using` 陳述式：</span><span class="sxs-lookup"><span data-stu-id="e3a56-153">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices.Client;
        using Microsoft.Azure.Devices.Shared;
        using Newtonsoft.Json;

1. <span data-ttu-id="e3a56-154">將下列欄位新增到 **Program** 類別。</span><span class="sxs-lookup"><span data-stu-id="e3a56-154">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="e3a56-155">將預留位置的值取代為您在上一節中所記下的裝置連接字串。</span><span class="sxs-lookup"><span data-stu-id="e3a56-155">Replace the placeholder value with the device connection string that you noted in the previous section.</span></span>
   
        static string DeviceConnectionString = "HostName=<yourIotHubName>.azure-devices.net;DeviceId=<yourIotDeviceName>;SharedAccessKey=<yourIotDeviceAccessKey>";
        static DeviceClient Client = null;

1. <span data-ttu-id="e3a56-156">將下列方法加入至 **Program** 類別：</span><span class="sxs-lookup"><span data-stu-id="e3a56-156">Add the following method to the **Program** class:</span></span>

       public static async void InitClient()
        {
            try
            {
                Console.WriteLine("Connecting to hub");
                Client = DeviceClient.CreateFromConnectionString(DeviceConnectionString, TransportType.Mqtt);
                Console.WriteLine("Retrieving twin");
                await Client.GetTwinAsync();
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }

    <span data-ttu-id="e3a56-157">**Client** 物件會公開從裝置來與裝置對應項進行互動時所需的所有方法。</span><span class="sxs-lookup"><span data-stu-id="e3a56-157">The **Client** object exposes all the methods you require to interact with device twins from the device.</span></span> <span data-ttu-id="e3a56-158">以上所示的程式碼會初始化**用戶端**物件，然後擷取 **myDeviceId** 的裝置對應項。</span><span class="sxs-lookup"><span data-stu-id="e3a56-158">The code shown above, initializes the **Client** object, and then retrieves the device twin for **myDeviceId**.</span></span>

1. <span data-ttu-id="e3a56-159">將下列方法加入至 **Program** 類別：</span><span class="sxs-lookup"><span data-stu-id="e3a56-159">Add the following method to the **Program** class:</span></span>
   
        public static async void ReportConnectivity()
        {
            try
            {
                Console.WriteLine("Sending connectivity data as reported property");
                
                TwinCollection reportedProperties, connectivity;
                reportedProperties = new TwinCollection();
                connectivity = new TwinCollection();
                connectivity["type"] = "cellular";
                reportedProperties["connectivity"] = connectivity;
                await Client.UpdateReportedPropertiesAsync(reportedProperties);
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }

   <span data-ttu-id="e3a56-160">上述程式碼會將 **myDeviceId** 的回報屬性更新為連線資訊。</span><span class="sxs-lookup"><span data-stu-id="e3a56-160">The code above updates **myDeviceId**'s reported property with the connectivity information.</span></span>

1. <span data-ttu-id="e3a56-161">最後，將下列幾行加入至 **Main** 方法：</span><span class="sxs-lookup"><span data-stu-id="e3a56-161">Finally, add the following lines to the **Main** method:</span></span>
   
       try
       {
            InitClient();
            ReportConnectivity();
       }
       catch (Exception ex)
       {
            Console.WriteLine();
            Console.WriteLine("Error in sample: {0}", ex.Message);
       }
       Console.WriteLine("Press Enter to exit.");
       Console.ReadLine();

1. <span data-ttu-id="e3a56-162">在方案總管中，開啟 [設定起始專案...]，並確定 **ReportConnectivity** 專案的 [動作] 是 [啟動]。</span><span class="sxs-lookup"><span data-stu-id="e3a56-162">In the Solution Explorer, open the **Set StartUp projects...** and make sure the **Action** for **ReportConnectivity** project is **Start**.</span></span> <span data-ttu-id="e3a56-163">建置方案。</span><span class="sxs-lookup"><span data-stu-id="e3a56-163">Build the solution.</span></span>
1. <span data-ttu-id="e3a56-164">以滑鼠右鍵按一下 **ReportConnectivity** 專案，並選取 [偵錯]，後面接著 [開始新執行個體] 來執行此應用程式。</span><span class="sxs-lookup"><span data-stu-id="e3a56-164">Run this application by right-clicking on the **ReportConnectivity** project and selecting **Debug**, followed by **Start new instance**.</span></span> <span data-ttu-id="e3a56-165">您應該會看到它取得對應項資訊，然後傳送連線作為「回報屬性」。</span><span class="sxs-lookup"><span data-stu-id="e3a56-165">You should see it getting the twin information, and then sending connectivity as a *reported property*.</span></span>
   
    ![執行裝置應用程式以回報連線][img-rundeviceapp]
    
    
1. <span data-ttu-id="e3a56-167">現在，裝置已回報其連線資訊，它應該會出現在這兩個查詢中。</span><span class="sxs-lookup"><span data-stu-id="e3a56-167">Now that the device reported its connectivity information, it should appear in both queries.</span></span> <span data-ttu-id="e3a56-168">執行 .NET **AddTagsAndQuery** 應用程式，以再次執行查詢。</span><span class="sxs-lookup"><span data-stu-id="e3a56-168">Run the .NET **AddTagsAndQuery** app to run the queries again.</span></span> <span data-ttu-id="e3a56-169">這次，**myDeviceId** 應該會出現在這兩個查詢結果中。</span><span class="sxs-lookup"><span data-stu-id="e3a56-169">This time **myDeviceId** should appear in both query results.</span></span>
   
    ![已成功回報裝置連線][img-tagappsuccess]

## <a name="next-steps"></a><span data-ttu-id="e3a56-171">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e3a56-171">Next steps</span></span>
<span data-ttu-id="e3a56-172">在此教學課程中，您在 Azure 入口網站中設定了新的 IoT 中樞，然後在 IoT 中樞的身分識別登錄中建立了裝置身分識別。</span><span class="sxs-lookup"><span data-stu-id="e3a56-172">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="e3a56-173">您已從後端應用程式將裝置中繼資料新增為標籤，並撰寫模擬裝置應用程式來報告裝置對應項中的裝置連線資訊。</span><span class="sxs-lookup"><span data-stu-id="e3a56-173">You added device metadata as tags from a back-end app, and wrote a simulated device app to report device connectivity information in the device twin.</span></span> <span data-ttu-id="e3a56-174">您也了解如何使 類似 SQL 的 IoT 中樞查詢語言來查詢此資訊。</span><span class="sxs-lookup"><span data-stu-id="e3a56-174">You also learned how to query this information using the SQL-like IoT Hub query language.</span></span>

<span data-ttu-id="e3a56-175">使用下列資源來了解如何：</span><span class="sxs-lookup"><span data-stu-id="e3a56-175">Use the following resources to learn how to:</span></span>

* <span data-ttu-id="e3a56-176">從裝置傳送遙測，請參閱[開始使用 IoT 中樞][lnk-iothub-getstarted]教學課程，</span><span class="sxs-lookup"><span data-stu-id="e3a56-176">send telemetry from devices with the [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="e3a56-177">使用裝置對應項的所需屬性來設定裝置，請參閱[使用所需的屬性來設定裝置][lnk-twin-how-to-configure]教學課程，</span><span class="sxs-lookup"><span data-stu-id="e3a56-177">configure devices using device twin's desired properties with the [Use desired properties to configure devices][lnk-twin-how-to-configure] tutorial,</span></span>
* <span data-ttu-id="e3a56-178">以互動方式控制裝置 (例如，從使用者控制的應用程式開啟風扇)，請參閱[使用直接方法][lnk-methods-tutorial]教學課程。</span><span class="sxs-lookup"><span data-stu-id="e3a56-178">control devices interactively (such as turning on a fan from a user-controlled app) with the [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-csharp-twin-getstarted/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-csharp-twin-getstarted/createnetapp.png
[img-addtagapp]: media/iot-hub-csharp-csharp-twin-getstarted/addtagapp.png
[img-createdeviceapp]: media/iot-hub-csharp-csharp-twin-getstarted/createdeviceapp.png
[img-clientnuget]: media/iot-hub-csharp-csharp-twin-getstarted/clientsdknuget.png
[img-rundeviceapp]: media/iot-hub-csharp-csharp-twin-getstarted/rundeviceapp.png
[img-tagappsuccess]: media/iot-hub-csharp-csharp-twin-getstarted/tagappsuccess.png

<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
[lnk-nuget-client-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices.Client/

[lnk-device-identity-csharp]: iot-hub-csharp-csharp-getstarted.md#DeviceIdentity_csharp
[lnk-d2c]: iot-hub-devguide-messaging.md#device-to-cloud-messages
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-identity]: iot-hub-devguide-identity-registry.md

[lnk-iothub-getstarted]: iot-hub-csharp-csharp-getstarted.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-twin-how-to-configure]: iot-hub-csharp-node-twin-how-to-configure.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md

