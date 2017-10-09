---
title: "aaaGet 開始使用 Azure IoT Hub 裝置雙 （.NET/節點） |Microsoft 文件"
description: "如何 toouse Azure IoT Hub 裝置雙 tooadd 標記，然後再使用 IoT 中樞查詢。 您可以使用 hello Azure IoT 裝置 SDK for Node.js tooimplement hello 模擬的裝置的應用程式與 hello Azure IoT 服務 SDK for.NET tooimplement 加入 hello 標記，並執行 hello IoT 中樞查詢中的服務應用程式。"
services: iot-hub
documentationcenter: node
author: fsautomata
manager: timlt
editor: 
ms.assetid: f7e23b6e-bfde-4fba-a6ec-dbb0f0e005f4
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/29/2017
ms.author: elioda
ms.openlocfilehash: 1cec082ebddc19c9b87998a5fd0159d32b07acd8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-twins-netnode"></a><span data-ttu-id="27098-104">開始使用裝置對應項 (.NET/Node)</span><span class="sxs-lookup"><span data-stu-id="27098-104">Get started with device twins (.NET/Node)</span></span>
[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

<span data-ttu-id="27098-105">在本教學課程的 hello 最後，您必須為.NET 和 Node.js 主控台應用程式：</span><span class="sxs-lookup"><span data-stu-id="27098-105">At hello end of this tutorial, you will have a .NET and a Node.js console app:</span></span>

* <span data-ttu-id="27098-106">**AddTagsAndQuery.sln**，這是 .NET 後端應用程式，可新增標籤和查詢裝置對應項。</span><span class="sxs-lookup"><span data-stu-id="27098-106">**AddTagsAndQuery.sln**, a .NET back-end app, which adds tags and queries device twins.</span></span>
* <span data-ttu-id="27098-107">**TwinSimulatedDevice.js**，Node.js 應用程式會模擬 tooyour IoT 中樞連線以稍早建立的 hello 裝置身分識別的裝置，並回報其連線的情況。</span><span class="sxs-lookup"><span data-stu-id="27098-107">**TwinSimulatedDevice.js**, a Node.js app which simulates a device that connects tooyour IoT hub with hello device identity created earlier, and reports its connectivity condition.</span></span>

> [!NOTE]
> <span data-ttu-id="27098-108">hello 文章[Azure IoT Sdk] [ lnk-hub-sdks]提供 hello Azure IoT Sdk 的相關資訊，您可以使用 toobuild 裝置與後端應用程式。</span><span class="sxs-lookup"><span data-stu-id="27098-108">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="27098-109">toocomplete 需要 hello 下列本教學課程：</span><span class="sxs-lookup"><span data-stu-id="27098-109">toocomplete this tutorial you need hello following:</span></span>

* <span data-ttu-id="27098-110">Visual Studio 2015 或 Visual Studio 2017。</span><span class="sxs-lookup"><span data-stu-id="27098-110">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="27098-111">Node.js 0.10.x 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="27098-111">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="27098-112">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="27098-112">An active Azure account.</span></span> <span data-ttu-id="27098-113">(如果您沒有帳戶，只需要幾分鐘的時間就可以建立[免費帳戶][lnk-free-trial]。)</span><span class="sxs-lookup"><span data-stu-id="27098-113">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-hello-service-app"></a><span data-ttu-id="27098-114">建立 hello 服務應用程式</span><span class="sxs-lookup"><span data-stu-id="27098-114">Create hello service app</span></span>
<span data-ttu-id="27098-115">在本節中，您建立.NET 主控台應用程式 （使用 C#） 加入位置的中繼資料 toohello 裝置兩個相關聯**myDeviceId**。</span><span class="sxs-lookup"><span data-stu-id="27098-115">In this section, you create a .NET console app (using C#) that adds location metadata toohello device twin associated with **myDeviceId**.</span></span> <span data-ttu-id="27098-116">接著，它查詢 hello 裝置雙 US，儲存在選取位於 hello hello 裝置 hello IoT 中樞中，然後 hello 所報告的行動電話通訊的連接。</span><span class="sxs-lookup"><span data-stu-id="27098-116">It then queries hello device twins stored in hello IoT hub selecting hello devices located in hello US, and then hello ones that reported a cellular connection.</span></span>

1. <span data-ttu-id="27098-117">在 Visual Studio 中，將 Visual C# Windows 傳統桌面專案 toohello 目前方案使用 hello**主控台應用程式**專案範本。</span><span class="sxs-lookup"><span data-stu-id="27098-117">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution by using hello **Console Application** project template.</span></span> <span data-ttu-id="27098-118">名稱 hello 專案**AddTagsAndQuery**。</span><span class="sxs-lookup"><span data-stu-id="27098-118">Name hello project **AddTagsAndQuery**.</span></span>
   
    ![新的 Visual C# Windows 傳統桌面專案][img-createapp]
1. <span data-ttu-id="27098-120">在 [方案總管] 中，以滑鼠右鍵按一下 hello **AddTagsAndQuery**專案，然後再按一下**管理 NuGet 封裝...**.</span><span class="sxs-lookup"><span data-stu-id="27098-120">In Solution Explorer, right-click hello **AddTagsAndQuery** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="27098-121">在 hello **NuGet 套件管理員**視窗中，選取**瀏覽**並搜尋**microsoft.azure.devices**。</span><span class="sxs-lookup"><span data-stu-id="27098-121">In hello **NuGet Package Manager** window, select **Browse** and search for **microsoft.azure.devices**.</span></span> <span data-ttu-id="27098-122">選取**安裝**tooinstall hello **Microsoft.Azure.Devices**封裝，並接受使用規定 hello。</span><span class="sxs-lookup"><span data-stu-id="27098-122">Select **Install** tooinstall hello **Microsoft.Azure.Devices** package, and accept hello terms of use.</span></span> <span data-ttu-id="27098-123">此程序下載、 安裝，並新增參考 toohello [Azure IoT 服務 SDK] [ lnk-nuget-service-sdk] NuGet 封裝和其相依性。</span><span class="sxs-lookup"><span data-stu-id="27098-123">This procedure downloads, installs, and adds a reference toohello [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![NuGet 封裝管理員視窗][img-servicenuget]
1. <span data-ttu-id="27098-125">新增下列 hello`using`在 hello hello 最上方的陳述式**Program.cs**檔案：</span><span class="sxs-lookup"><span data-stu-id="27098-125">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
1. <span data-ttu-id="27098-126">新增下列欄位 toohello hello**程式**類別。</span><span class="sxs-lookup"><span data-stu-id="27098-126">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="27098-127">取代 hello hello 中樞在 hello 上一節中所建立的 IoT 中樞連接字串中的 hello 預留位置的值。</span><span class="sxs-lookup"><span data-stu-id="27098-127">Replace hello placeholder value with hello IoT Hub connection string for hello hub that you created in hello previous section.</span></span>
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
1. <span data-ttu-id="27098-128">新增下列方法 toohello hello**程式**類別：</span><span class="sxs-lookup"><span data-stu-id="27098-128">Add hello following method toohello **Program** class:</span></span>
   
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
   
    <span data-ttu-id="27098-129">hello **RegistryManager**類別會公開與裝置雙 hello 服務從所有 hello 方法 toointeract 必要。</span><span class="sxs-lookup"><span data-stu-id="27098-129">hello **RegistryManager** class exposes all hello methods required toointeract with device twins from hello service.</span></span> <span data-ttu-id="27098-130">hello 先前的程式碼會先初始化 hello **registryManager**物件，然後擷取 hello 的裝置兩個**myDeviceId**，且最後 hello 預期位置資訊會以更新其標籤。</span><span class="sxs-lookup"><span data-stu-id="27098-130">hello previous code first initializes hello **registryManager** object, then retrieves hello device twin for **myDeviceId**, and finally updates its tags with hello desired location information.</span></span>
   
    <span data-ttu-id="27098-131">在更新之後，它會執行兩個查詢： hello 會先選取只 hello 裝置雙的裝置位於 hello **Redmond43**工廠和 hello 第二個精簡 hello 查詢 tooselect 只有 hello 裝置也會透過連接行動電話通訊網路。</span><span class="sxs-lookup"><span data-stu-id="27098-131">After updating, it executes two queries: hello first selects only hello device twins of devices located in hello **Redmond43** plant, and hello second refines hello query tooselect only hello devices that are also connected through cellular network.</span></span>
   
    <span data-ttu-id="27098-132">請注意該 hello 先前的程式碼，當它建立 hello**查詢**物件，指定傳回的文件的最大數目。</span><span class="sxs-lookup"><span data-stu-id="27098-132">Note that hello previous code, when it creates hello **query** object, specifies a maximum number of returned documents.</span></span> <span data-ttu-id="27098-133">hello**查詢**物件包含**HasMoreResults**布林值屬性，您可以使用 tooinvoke hello **GetNextAsTwinAsync**方法多次 tooretrieve 所有結果。</span><span class="sxs-lookup"><span data-stu-id="27098-133">hello **query** object contains a **HasMoreResults** boolean property that you can use tooinvoke hello **GetNextAsTwinAsync** methods multiple times tooretrieve all results.</span></span> <span data-ttu-id="27098-134">有一個稱為 **GetNextAsJson** 的方法適用於不是裝置對應項的結果，例如彙總查詢的結果。</span><span class="sxs-lookup"><span data-stu-id="27098-134">A method called **GetNextAsJson** is available for results that are not device twins, for example, results of aggregation queries.</span></span>
1. <span data-ttu-id="27098-135">最後，加入下列行 toohello hello **Main**方法：</span><span class="sxs-lookup"><span data-stu-id="27098-135">Finally, add hello following lines toohello **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        AddTagsAndQuery().Wait();
        Console.WriteLine("Press Enter tooexit.");
        Console.ReadLine();

1. <span data-ttu-id="27098-136">在 hello 方案總管 中，開啟 hello**設定啟始專案...** ，請確定 hello**動作**如**AddTagsAndQuery**專案是**啟動**。</span><span class="sxs-lookup"><span data-stu-id="27098-136">In hello Solution Explorer, open hello **Set StartUp projects...** and make sure hello **Action** for **AddTagsAndQuery** project is **Start**.</span></span> <span data-ttu-id="27098-137">建置 hello 方案。</span><span class="sxs-lookup"><span data-stu-id="27098-137">Build hello solution.</span></span>
1. <span data-ttu-id="27098-138">執行此應用程式，以滑鼠右鍵按一下 hello **AddTagsAndQuery**專案，並選取**偵錯**，後面接著**開始新執行個體**。</span><span class="sxs-lookup"><span data-stu-id="27098-138">Run this application by right-clicking on hello **AddTagsAndQuery** project and selecting **Debug**, followed by **Start new instance**.</span></span> <span data-ttu-id="27098-139">您應該會看到一個裝置 hello 結果中的 hello 查詢要求的所有裝置都位於**Redmond43**和無限制 hello 的 hello 查詢結果 toodevices 使用行動電話通訊網路。</span><span class="sxs-lookup"><span data-stu-id="27098-139">You should see one device in hello results for hello query asking for all devices located in **Redmond43** and none for hello query that restricts hello results toodevices that use a cellular network.</span></span>
   
    ![視窗中的查詢結果][img-addtagapp]

<span data-ttu-id="27098-141">Hello 下一節，您將建立報告 hello 連線資訊裝置應用程式，並變更 hello hello 前一節中的 hello 查詢的結果。</span><span class="sxs-lookup"><span data-stu-id="27098-141">In hello next section, you create a device app that reports hello connectivity information and changes hello result of hello query in hello previous section.</span></span>

## <a name="create-hello-device-app"></a><span data-ttu-id="27098-142">建立 hello 裝置應用程式</span><span class="sxs-lookup"><span data-stu-id="27098-142">Create hello device app</span></span>
<span data-ttu-id="27098-143">在本節中，您建立 Node.js 主控台應用程式連接成 tooyour 中樞**myDeviceId**，，然後更新其已連線使用行動電話通訊網路的報告的屬性 toocontain hello 資訊。</span><span class="sxs-lookup"><span data-stu-id="27098-143">In this section, you create a Node.js console app that connects tooyour hub as **myDeviceId**, and then updates its reported properties toocontain hello information that it is connected using a cellular network.</span></span>

1. <span data-ttu-id="27098-144">建立稱為 **reportconnectivity** 的新空白資料夾。</span><span class="sxs-lookup"><span data-stu-id="27098-144">Create a new empty folder called **reportconnectivity**.</span></span> <span data-ttu-id="27098-145">在 hello **reportconnectivity**資料夾中，建立新的 package.json 檔案使用下列命令，在您的命令提示字元的 hello。</span><span class="sxs-lookup"><span data-stu-id="27098-145">In hello **reportconnectivity** folder, create a new package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="27098-146">接受所有的 hello 預設值。</span><span class="sxs-lookup"><span data-stu-id="27098-146">Accept all hello defaults.</span></span>
   
    ```
    npm init
    ```
1. <span data-ttu-id="27098-147">在您的命令提示字元中 hello **reportconnectivity**資料夾中，執行下列命令 tooinstall hello hello **azure iot 裝置**，和**azure iot 裝置-mqtt**封裝:</span><span class="sxs-lookup"><span data-stu-id="27098-147">At your command prompt in hello **reportconnectivity** folder, run hello following command tooinstall hello **azure-iot-device**, and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
1. <span data-ttu-id="27098-148">使用文字編輯器中，建立新**ReportConnectivity.js**檔案在 hello **reportconnectivity**資料夾。</span><span class="sxs-lookup"><span data-stu-id="27098-148">Using a text editor, create a new **ReportConnectivity.js** file in hello **reportconnectivity** folder.</span></span>
1. <span data-ttu-id="27098-149">新增下列程式碼 toohello hello **ReportConnectivity.js**檔案，並以取代 hello 預留位置裝置連接字串，以建立 hello 時您複製一個 hello **myDeviceId**裝置身分識別：</span><span class="sxs-lookup"><span data-stu-id="27098-149">Add hello following code toohello **ReportConnectivity.js** file, and substitute hello placeholder for device connection string with hello one you copied when you created hello **myDeviceId** device identity:</span></span>
   
        'use strict';
        var Client = require('azure-iot-device').Client;
        var Protocol = require('azure-iot-device-mqtt').Mqtt;
   
        var connectionString = '{device connection string}';
        var client = Client.fromConnectionString(connectionString, Protocol);
   
        client.open(function(err) {
        if (err) {
            console.error('could not open IotHub client');
        }  else {
            console.log('client opened');
   
            client.getTwin(function(err, twin) {
            if (err) {
                console.error('could not get twin');
            } else {
                var patch = {
                    connectivity: {
                        type: 'cellular'
                    }
                };
   
                twin.properties.reported.update(patch, function(err) {
                    if (err) {
                        console.error('could not update twin');
                    } else {
                        console.log('twin state reported');
                        process.exit();
                    }
                });
            }
            });
        }
        });
   
    <span data-ttu-id="27098-150">hello**用戶端**物件會公開您需要將裝置從 hello 裝置的雙具備 toointeract 所有 hello 方法。</span><span class="sxs-lookup"><span data-stu-id="27098-150">hello **Client** object exposes all hello methods you require toointeract with device twins from hello device.</span></span> <span data-ttu-id="27098-151">hello 先前的程式碼，它會初始化 hello 之後**用戶端**物件，擷取 hello 的裝置兩個**myDeviceId**及更新其報告的屬性與 hello 連線資訊。</span><span class="sxs-lookup"><span data-stu-id="27098-151">hello previous code, after it initializes hello **Client** object, retrieves hello device twin for **myDeviceId** and updates its reported property with hello connectivity information.</span></span>
1. <span data-ttu-id="27098-152">執行 hello 裝置應用程式</span><span class="sxs-lookup"><span data-stu-id="27098-152">Run hello device app</span></span>
   
        node ReportConnectivity.js
   
    <span data-ttu-id="27098-153">您應該會看到 hello 訊息`twin state reported`。</span><span class="sxs-lookup"><span data-stu-id="27098-153">You should see hello message `twin state reported`.</span></span>
1. <span data-ttu-id="27098-154">既然 hello 裝置報告其連線資訊時，它應該會出現在這兩個查詢。</span><span class="sxs-lookup"><span data-stu-id="27098-154">Now that hello device reported its connectivity information, it should appear in both queries.</span></span> <span data-ttu-id="27098-155">執行 hello.NET **AddTagsAndQuery**應用程式 toorun hello 查詢一次。</span><span class="sxs-lookup"><span data-stu-id="27098-155">Run hello .NET **AddTagsAndQuery** app toorun hello queries again.</span></span> <span data-ttu-id="27098-156">這次，**myDeviceId** 應該會出現在這兩個查詢結果中。</span><span class="sxs-lookup"><span data-stu-id="27098-156">This time **myDeviceId** should appear in both query results.</span></span>
   
    ![][img-addtagapp2]

## <a name="next-steps"></a><span data-ttu-id="27098-157">後續步驟</span><span class="sxs-lookup"><span data-stu-id="27098-157">Next steps</span></span>
<span data-ttu-id="27098-158">在本教學課程中，您在 hello Azure 入口網站中設定新的 IoT 中樞，並接著 hello IoT 中樞的身分識別登錄中建立裝置身分識別。</span><span class="sxs-lookup"><span data-stu-id="27098-158">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="27098-159">您標記為加入裝置中繼資料，從後端應用程式，並在 hello 裝置兩個撰寫模擬的裝置的應用程式 tooreport 裝置連線資訊。</span><span class="sxs-lookup"><span data-stu-id="27098-159">You added device metadata as tags from a back-end app, and wrote a simulated device app tooreport device connectivity information in hello device twin.</span></span> <span data-ttu-id="27098-160">您也學到如何 tooquery 這項資訊使用 hello 類似 SQL 的 IoT 中樞查詢語言。</span><span class="sxs-lookup"><span data-stu-id="27098-160">You also learned how tooquery this information using hello SQL-like IoT Hub query language.</span></span>

<span data-ttu-id="27098-161">下列資源 toolearn 如何使用 hello 至：</span><span class="sxs-lookup"><span data-stu-id="27098-161">Use hello following resources toolearn how to:</span></span>

* <span data-ttu-id="27098-162">從以 hello 的裝置將遙測傳送[開始使用 IoT 中樞][ lnk-iothub-getstarted]教學課程中，</span><span class="sxs-lookup"><span data-stu-id="27098-162">send telemetry from devices with hello [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="27098-163">設定裝置使用兩個裝置所需的屬性以 hello[使用想要的話屬性 tooconfigure 裝置][ lnk-twin-how-to-configure]教學課程中，</span><span class="sxs-lookup"><span data-stu-id="27098-163">configure devices using device twin's desired properties with hello [Use desired properties tooconfigure devices][lnk-twin-how-to-configure] tutorial,</span></span>
* <span data-ttu-id="27098-164">控制以互動方式 （例如開啟風扇從使用者控制的應用程式） 的裝置以 hello[使用直接的方法][ lnk-methods-tutorial]教學課程。</span><span class="sxs-lookup"><span data-stu-id="27098-164">control devices interactively (such as turning on a fan from a user-controlled app) with hello [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-node-twin-getstarted/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-node-twin-getstarted/createnetapp.png
[img-addtagapp]: media/iot-hub-csharp-node-twin-getstarted/addtagapp.png
[img-addtagapp2]: media/iot-hub-csharp-node-twin-getstarted/addtagapp2.png

<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/

[lnk-d2c]: iot-hub-devguide-messaging.md#device-to-cloud-messages
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-identity]: iot-hub-devguide-identity-registry.md

[lnk-iothub-getstarted]: iot-hub-node-node-getstarted.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-twin-how-to-configure]: iot-hub-csharp-node-twin-how-to-configure.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md

