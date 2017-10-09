---
title: "aaaGet 開始使用 Azure IoT Hub 裝置雙 (.NET/.NET) |Microsoft 文件"
description: "如何 toouse Azure IoT Hub 裝置雙 tooadd 標記，然後再使用 IoT 中樞查詢。 您可以使用 hello Azure IoT 裝置 SDK for.NET tooimplement hello 模擬的裝置的應用程式與 hello.NET tooimplement 加入 hello 標記，並執行 hello IoT 中樞查詢中的服務應用程式的 Azure IoT 服務 SDK。"
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
ms.openlocfilehash: 7fa73ac896c44e79c6522d252cd1515bd6e7bb2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-twins-netnet"></a><span data-ttu-id="385f9-104">開始使用裝置對應項 (.NET/.NET)</span><span class="sxs-lookup"><span data-stu-id="385f9-104">Get started with device twins (.NET/.NET)</span></span>
[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

<span data-ttu-id="385f9-105">在本教學課程的 hello 結束時，您將擁有這些.NET 主控台應用程式：</span><span class="sxs-lookup"><span data-stu-id="385f9-105">At hello end of this tutorial, you will have these .NET console apps:</span></span>

* <span data-ttu-id="385f9-106">**CreateDeviceIdentity**，.NET 應用程式會建立裝置身分識別和相關聯的安全性金鑰 tooconnect 應用程式模擬的裝置。</span><span class="sxs-lookup"><span data-stu-id="385f9-106">**CreateDeviceIdentity**, a .NET app which creates a device identity and associated security key tooconnect your simulated device app.</span></span>
* <span data-ttu-id="385f9-107">**AddTagsAndQuery**，這是 .NET 後端應用程式，可新增標籤和查詢裝置對應項。</span><span class="sxs-lookup"><span data-stu-id="385f9-107">**AddTagsAndQuery**, a .NET back-end app which adds tags and queries device twins.</span></span>
* <span data-ttu-id="385f9-108">**ReportConnectivity**，.NET 裝置應用程式會模擬 tooyour IoT 中樞連線以稍早建立的 hello 裝置身分識別的裝置，並回報其連線的情況。</span><span class="sxs-lookup"><span data-stu-id="385f9-108">**ReportConnectivity**, a .NET device app which simulates a device that connects tooyour IoT hub with hello device identity created earlier, and reports its connectivity condition.</span></span>

> [!NOTE]
> <span data-ttu-id="385f9-109">hello 文章[Azure IoT Sdk] [ lnk-hub-sdks]提供 hello Azure IoT Sdk 的相關資訊，您可以使用 toobuild 裝置與後端應用程式。</span><span class="sxs-lookup"><span data-stu-id="385f9-109">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="385f9-110">toocomplete 需要 hello 下列本教學課程：</span><span class="sxs-lookup"><span data-stu-id="385f9-110">toocomplete this tutorial you need hello following:</span></span>

* <span data-ttu-id="385f9-111">Visual Studio 2015 或 Visual Studio 2017。</span><span class="sxs-lookup"><span data-stu-id="385f9-111">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="385f9-112">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="385f9-112">An active Azure account.</span></span> <span data-ttu-id="385f9-113">(如果您沒有帳戶，只需要幾分鐘的時間就可以建立[免費帳戶][lnk-free-trial]。)</span><span class="sxs-lookup"><span data-stu-id="385f9-113">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

<span data-ttu-id="385f9-114">如果您想 toocreate hello 裝置身分識別以程式設計方式相反地，讀取 hello 對應的章節 hello[連接您使用適用於.NET 的模擬的裝置 tooyour IoT 中樞][ lnk-device-identity-csharp]發行項。</span><span class="sxs-lookup"><span data-stu-id="385f9-114">If you want toocreate hello device identity programmatically instead, read hello corresponding section in hello [Connect your simulated device tooyour IoT hub using .NET][lnk-device-identity-csharp] article.</span></span>

## <a name="create-hello-service-app"></a><span data-ttu-id="385f9-115">建立 hello 服務應用程式</span><span class="sxs-lookup"><span data-stu-id="385f9-115">Create hello service app</span></span>
<span data-ttu-id="385f9-116">在本節中，您建立.NET 主控台應用程式 （使用 C#） 加入位置的中繼資料 toohello 裝置兩個相關聯**myDeviceId**。</span><span class="sxs-lookup"><span data-stu-id="385f9-116">In this section, you create a .NET console app (using C#) that adds location metadata toohello device twin associated with **myDeviceId**.</span></span> <span data-ttu-id="385f9-117">接著，它查詢 hello 裝置雙 US，儲存在選取位於 hello hello 裝置 hello IoT 中樞中，然後 hello 所報告的行動電話通訊的連接。</span><span class="sxs-lookup"><span data-stu-id="385f9-117">It then queries hello device twins stored in hello IoT hub selecting hello devices located in hello US, and then hello ones that reported a cellular connection.</span></span>

1. <span data-ttu-id="385f9-118">在 Visual Studio 中，將 Visual C# Windows 傳統桌面專案 toohello 目前方案使用 hello**主控台應用程式**專案範本。</span><span class="sxs-lookup"><span data-stu-id="385f9-118">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution by using hello **Console Application** project template.</span></span> <span data-ttu-id="385f9-119">名稱 hello 專案**AddTagsAndQuery**。</span><span class="sxs-lookup"><span data-stu-id="385f9-119">Name hello project **AddTagsAndQuery**.</span></span>
   
    ![新的 Visual C# Windows 傳統桌面專案][img-createapp]
1. <span data-ttu-id="385f9-121">在 [方案總管] 中，以滑鼠右鍵按一下 hello **AddTagsAndQuery**專案，然後再按一下**管理 NuGet 封裝...**.</span><span class="sxs-lookup"><span data-stu-id="385f9-121">In Solution Explorer, right-click hello **AddTagsAndQuery** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="385f9-122">在 hello **NuGet 套件管理員**視窗中，選取**瀏覽**並搜尋**microsoft.azure.devices**。</span><span class="sxs-lookup"><span data-stu-id="385f9-122">In hello **NuGet Package Manager** window, select **Browse** and search for **microsoft.azure.devices**.</span></span> <span data-ttu-id="385f9-123">選取**安裝**tooinstall hello **Microsoft.Azure.Devices**封裝，並接受使用規定 hello。</span><span class="sxs-lookup"><span data-stu-id="385f9-123">Select **Install** tooinstall hello **Microsoft.Azure.Devices** package, and accept hello terms of use.</span></span> <span data-ttu-id="385f9-124">此程序下載、 安裝，並新增參考 toohello [Azure IoT 服務 SDK] [ lnk-nuget-service-sdk] NuGet 封裝和其相依性。</span><span class="sxs-lookup"><span data-stu-id="385f9-124">This procedure downloads, installs, and adds a reference toohello [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![NuGet 封裝管理員視窗][img-servicenuget]
1. <span data-ttu-id="385f9-126">新增下列 hello`using`在 hello hello 最上方的陳述式**Program.cs**檔案：</span><span class="sxs-lookup"><span data-stu-id="385f9-126">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
1. <span data-ttu-id="385f9-127">新增下列欄位 toohello hello**程式**類別。</span><span class="sxs-lookup"><span data-stu-id="385f9-127">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="385f9-128">取代 hello hello 中樞在 hello 上一節中所建立的 IoT 中樞連接字串中的 hello 預留位置的值。</span><span class="sxs-lookup"><span data-stu-id="385f9-128">Replace hello placeholder value with hello IoT Hub connection string for hello hub that you created in hello previous section.</span></span>
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
1. <span data-ttu-id="385f9-129">新增下列方法 toohello hello**程式**類別：</span><span class="sxs-lookup"><span data-stu-id="385f9-129">Add hello following method toohello **Program** class:</span></span>
   
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
   
    <span data-ttu-id="385f9-130">hello **RegistryManager**類別會公開與裝置雙 hello 服務從所有 hello 方法 toointeract 必要。</span><span class="sxs-lookup"><span data-stu-id="385f9-130">hello **RegistryManager** class exposes all hello methods required toointeract with device twins from hello service.</span></span> <span data-ttu-id="385f9-131">hello 先前的程式碼會先初始化 hello **registryManager**物件，然後擷取 hello 的裝置兩個**myDeviceId**，且最後 hello 預期位置資訊會以更新其標籤。</span><span class="sxs-lookup"><span data-stu-id="385f9-131">hello previous code first initializes hello **registryManager** object, then retrieves hello device twin for **myDeviceId**, and finally updates its tags with hello desired location information.</span></span>
   
    <span data-ttu-id="385f9-132">在更新之後，它會執行兩個查詢： hello 會先選取只 hello 裝置雙的裝置位於 hello **Redmond43**工廠和 hello 第二個精簡 hello 查詢 tooselect 只有 hello 裝置也會透過連接行動電話通訊網路。</span><span class="sxs-lookup"><span data-stu-id="385f9-132">After updating, it executes two queries: hello first selects only hello device twins of devices located in hello **Redmond43** plant, and hello second refines hello query tooselect only hello devices that are also connected through cellular network.</span></span>
   
    <span data-ttu-id="385f9-133">請注意該 hello 先前的程式碼，當它建立 hello**查詢**物件，指定傳回的文件的最大數目。</span><span class="sxs-lookup"><span data-stu-id="385f9-133">Note that hello previous code, when it creates hello **query** object, specifies a maximum number of returned documents.</span></span> <span data-ttu-id="385f9-134">hello**查詢**物件包含**HasMoreResults**布林值屬性，您可以使用 tooinvoke hello **GetNextAsTwinAsync**方法多次 tooretrieve 所有結果。</span><span class="sxs-lookup"><span data-stu-id="385f9-134">hello **query** object contains a **HasMoreResults** boolean property that you can use tooinvoke hello **GetNextAsTwinAsync** methods multiple times tooretrieve all results.</span></span> <span data-ttu-id="385f9-135">有一個稱為 **GetNextAsJson** 的方法適用於不是裝置對應項的結果，例如彙總查詢的結果。</span><span class="sxs-lookup"><span data-stu-id="385f9-135">A method called **GetNextAsJson** is available for results that are not device twins, for example, results of aggregation queries.</span></span>
1. <span data-ttu-id="385f9-136">最後，加入下列行 toohello hello **Main**方法：</span><span class="sxs-lookup"><span data-stu-id="385f9-136">Finally, add hello following lines toohello **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        AddTagsAndQuery().Wait();
        Console.WriteLine("Press Enter tooexit.");
        Console.ReadLine();

1. <span data-ttu-id="385f9-137">在 hello 方案總管 中，開啟 hello**設定啟始專案...** ，請確定 hello**動作**如**AddTagsAndQuery**專案是**啟動**。</span><span class="sxs-lookup"><span data-stu-id="385f9-137">In hello Solution Explorer, open hello **Set StartUp projects...** and make sure hello **Action** for **AddTagsAndQuery** project is **Start**.</span></span> <span data-ttu-id="385f9-138">建置 hello 方案。</span><span class="sxs-lookup"><span data-stu-id="385f9-138">Build hello solution.</span></span>
1. <span data-ttu-id="385f9-139">執行此應用程式，以滑鼠右鍵按一下 hello **AddTagsAndQuery**專案，並選取**偵錯**，後面接著**開始新執行個體**。</span><span class="sxs-lookup"><span data-stu-id="385f9-139">Run this application by right-clicking on hello **AddTagsAndQuery** project and selecting **Debug**, followed by **Start new instance**.</span></span> <span data-ttu-id="385f9-140">您應該會看到一個裝置 hello 結果中的 hello 查詢要求的所有裝置都位於**Redmond43**和無限制 hello 的 hello 查詢結果 toodevices 使用行動電話通訊網路。</span><span class="sxs-lookup"><span data-stu-id="385f9-140">You should see one device in hello results for hello query asking for all devices located in **Redmond43** and none for hello query that restricts hello results toodevices that use a cellular network.</span></span>
   
    ![視窗中的查詢結果][img-addtagapp]

<span data-ttu-id="385f9-142">Hello 下一節，您將建立報告 hello 連線資訊裝置應用程式，並變更 hello hello 前一節中的 hello 查詢的結果。</span><span class="sxs-lookup"><span data-stu-id="385f9-142">In hello next section, you create a device app that reports hello connectivity information and changes hello result of hello query in hello previous section.</span></span>

## <a name="create-hello-device-app"></a><span data-ttu-id="385f9-143">建立 hello 裝置應用程式</span><span class="sxs-lookup"><span data-stu-id="385f9-143">Create hello device app</span></span>
<span data-ttu-id="385f9-144">在本節中，您會建立.NET 主控台應用程式連接成 tooyour 中樞**myDeviceId**，，然後更新其已連線使用行動電話通訊網路的報告的屬性 toocontain hello 資訊。</span><span class="sxs-lookup"><span data-stu-id="385f9-144">In this section, you create a .NET console app that connects tooyour hub as **myDeviceId**, and then updates its reported properties toocontain hello information that it is connected using a cellular network.</span></span>

1. <span data-ttu-id="385f9-145">在 Visual Studio 中，將 Visual C# Windows 傳統桌面專案 toohello 目前方案使用 hello**主控台應用程式**專案範本。</span><span class="sxs-lookup"><span data-stu-id="385f9-145">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution by using hello **Console Application** project template.</span></span> <span data-ttu-id="385f9-146">名稱 hello 專案**ReportConnectivity**。</span><span class="sxs-lookup"><span data-stu-id="385f9-146">Name hello project **ReportConnectivity**.</span></span>
   
    ![新的 Visual C# Windows 傳統裝置應用程式][img-createdeviceapp]
    
1. <span data-ttu-id="385f9-148">在 [方案總管] 中，以滑鼠右鍵按一下 hello **ReportConnectivity**專案，然後再按一下**管理 NuGet 封裝...**.</span><span class="sxs-lookup"><span data-stu-id="385f9-148">In Solution Explorer, right-click hello **ReportConnectivity** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="385f9-149">在 hello **NuGet 套件管理員**視窗中，選取**瀏覽**並搜尋**microsoft.azure.devices.client**。</span><span class="sxs-lookup"><span data-stu-id="385f9-149">In hello **NuGet Package Manager** window, select **Browse** and search for **microsoft.azure.devices.client**.</span></span> <span data-ttu-id="385f9-150">選取**安裝**tooinstall hello **Microsoft.Azure.Devices.Client**封裝，並接受使用規定 hello。</span><span class="sxs-lookup"><span data-stu-id="385f9-150">Select **Install** tooinstall hello **Microsoft.Azure.Devices.Client** package, and accept hello terms of use.</span></span> <span data-ttu-id="385f9-151">此程序下載、 安裝，並新增參考 toohello [Azure IoT 裝置 SDK] [ lnk-nuget-client-sdk] NuGet 封裝和其相依性。</span><span class="sxs-lookup"><span data-stu-id="385f9-151">This procedure downloads, installs, and adds a reference toohello [Azure IoT device SDK][lnk-nuget-client-sdk] NuGet package and its dependencies.</span></span>
   
    ![NuGet 套件管理員視窗用戶端應用程式][img-clientnuget]
1. <span data-ttu-id="385f9-153">新增下列 hello`using`在 hello hello 最上方的陳述式**Program.cs**檔案：</span><span class="sxs-lookup"><span data-stu-id="385f9-153">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices.Client;
        using Microsoft.Azure.Devices.Shared;
        using Newtonsoft.Json;

1. <span data-ttu-id="385f9-154">新增下列欄位 toohello hello**程式**類別。</span><span class="sxs-lookup"><span data-stu-id="385f9-154">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="385f9-155">取代您記下 hello 前一節中的 hello 裝置連接字串中的 hello 預留位置的值。</span><span class="sxs-lookup"><span data-stu-id="385f9-155">Replace hello placeholder value with hello device connection string that you noted in hello previous section.</span></span>
   
        static string DeviceConnectionString = "HostName=<yourIotHubName>.azure-devices.net;DeviceId=<yourIotDeviceName>;SharedAccessKey=<yourIotDeviceAccessKey>";
        static DeviceClient Client = null;

1. <span data-ttu-id="385f9-156">新增下列方法 toohello hello**程式**類別：</span><span class="sxs-lookup"><span data-stu-id="385f9-156">Add hello following method toohello **Program** class:</span></span>

       public static async void InitClient()
        {
            try
            {
                Console.WriteLine("Connecting toohub");
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

    <span data-ttu-id="385f9-157">hello**用戶端**物件會公開您需要將裝置從 hello 裝置的雙具備 toointeract 所有 hello 方法。</span><span class="sxs-lookup"><span data-stu-id="385f9-157">hello **Client** object exposes all hello methods you require toointeract with device twins from hello device.</span></span> <span data-ttu-id="385f9-158">hello，如上所示的程式碼初始化 hello**用戶端**物件，然後按一下 擷取的 hello 裝置兩個**myDeviceId**。</span><span class="sxs-lookup"><span data-stu-id="385f9-158">hello code shown above, initializes hello **Client** object, and then retrieves hello device twin for **myDeviceId**.</span></span>

1. <span data-ttu-id="385f9-159">新增下列方法 toohello hello**程式**類別：</span><span class="sxs-lookup"><span data-stu-id="385f9-159">Add hello following method toohello **Program** class:</span></span>
   
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

   <span data-ttu-id="385f9-160">hello 上方更新程式碼**myDeviceId**的報告與 hello 連線資訊的屬性。</span><span class="sxs-lookup"><span data-stu-id="385f9-160">hello code above updates **myDeviceId**'s reported property with hello connectivity information.</span></span>

1. <span data-ttu-id="385f9-161">最後，加入下列行 toohello hello **Main**方法：</span><span class="sxs-lookup"><span data-stu-id="385f9-161">Finally, add hello following lines toohello **Main** method:</span></span>
   
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
       Console.WriteLine("Press Enter tooexit.");
       Console.ReadLine();

1. <span data-ttu-id="385f9-162">在 hello 方案總管 中，開啟 hello**設定啟始專案...** ，請確定 hello**動作**如**ReportConnectivity**專案是**啟動**。</span><span class="sxs-lookup"><span data-stu-id="385f9-162">In hello Solution Explorer, open hello **Set StartUp projects...** and make sure hello **Action** for **ReportConnectivity** project is **Start**.</span></span> <span data-ttu-id="385f9-163">建置 hello 方案。</span><span class="sxs-lookup"><span data-stu-id="385f9-163">Build hello solution.</span></span>
1. <span data-ttu-id="385f9-164">執行此應用程式，以滑鼠右鍵按一下 hello **ReportConnectivity**專案，並選取**偵錯**，後面接著**開始新執行個體**。</span><span class="sxs-lookup"><span data-stu-id="385f9-164">Run this application by right-clicking on hello **ReportConnectivity** project and selecting **Debug**, followed by **Start new instance**.</span></span> <span data-ttu-id="385f9-165">您應該看到它取得 hello 的兩個資訊，然後將傳送做為連線*報告屬性*。</span><span class="sxs-lookup"><span data-stu-id="385f9-165">You should see it getting hello twin information, and then sending connectivity as a *reported property*.</span></span>
   
    ![執行裝置的應用程式 tooreport 連線能力][img-rundeviceapp]
    
    
1. <span data-ttu-id="385f9-167">既然 hello 裝置報告其連線資訊時，它應該會出現在這兩個查詢。</span><span class="sxs-lookup"><span data-stu-id="385f9-167">Now that hello device reported its connectivity information, it should appear in both queries.</span></span> <span data-ttu-id="385f9-168">執行 hello.NET **AddTagsAndQuery**應用程式 toorun hello 查詢一次。</span><span class="sxs-lookup"><span data-stu-id="385f9-168">Run hello .NET **AddTagsAndQuery** app toorun hello queries again.</span></span> <span data-ttu-id="385f9-169">這次，**myDeviceId** 應該會出現在這兩個查詢結果中。</span><span class="sxs-lookup"><span data-stu-id="385f9-169">This time **myDeviceId** should appear in both query results.</span></span>
   
    ![已成功回報裝置連線][img-tagappsuccess]

## <a name="next-steps"></a><span data-ttu-id="385f9-171">後續步驟</span><span class="sxs-lookup"><span data-stu-id="385f9-171">Next steps</span></span>
<span data-ttu-id="385f9-172">在本教學課程中，您在 hello Azure 入口網站中設定新的 IoT 中樞，並接著 hello IoT 中樞的身分識別登錄中建立裝置身分識別。</span><span class="sxs-lookup"><span data-stu-id="385f9-172">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="385f9-173">您標記為加入裝置中繼資料，從後端應用程式，並在 hello 裝置兩個撰寫模擬的裝置的應用程式 tooreport 裝置連線資訊。</span><span class="sxs-lookup"><span data-stu-id="385f9-173">You added device metadata as tags from a back-end app, and wrote a simulated device app tooreport device connectivity information in hello device twin.</span></span> <span data-ttu-id="385f9-174">您也學到如何 tooquery 這項資訊使用 hello 類似 SQL 的 IoT 中樞查詢語言。</span><span class="sxs-lookup"><span data-stu-id="385f9-174">You also learned how tooquery this information using hello SQL-like IoT Hub query language.</span></span>

<span data-ttu-id="385f9-175">下列資源 toolearn 如何使用 hello 至：</span><span class="sxs-lookup"><span data-stu-id="385f9-175">Use hello following resources toolearn how to:</span></span>

* <span data-ttu-id="385f9-176">從以 hello 的裝置將遙測傳送[開始使用 IoT 中樞][ lnk-iothub-getstarted]教學課程中，</span><span class="sxs-lookup"><span data-stu-id="385f9-176">send telemetry from devices with hello [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="385f9-177">設定裝置使用兩個裝置所需的屬性以 hello[使用想要的話屬性 tooconfigure 裝置][ lnk-twin-how-to-configure]教學課程中，</span><span class="sxs-lookup"><span data-stu-id="385f9-177">configure devices using device twin's desired properties with hello [Use desired properties tooconfigure devices][lnk-twin-how-to-configure] tutorial,</span></span>
* <span data-ttu-id="385f9-178">控制以互動方式 （例如開啟風扇從使用者控制的應用程式） 的裝置以 hello[使用直接的方法][ lnk-methods-tutorial]教學課程。</span><span class="sxs-lookup"><span data-stu-id="385f9-178">control devices interactively (such as turning on a fan from a user-controlled app) with hello [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

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

