---
title: "aaaSchedule 作業與 Azure IoT 中樞 （.NET/節點） |Microsoft 文件"
description: "如何 tooschedule Azure IoT 中樞工作 tooinvoke 上多個裝置的直接的方法。 您可以使用 hello Azure IoT 裝置 SDK for Node.js tooimplement hello 模擬裝置的應用程式和 hello Azure IoT 服務 SDK for.NET tooimplement 服務應用程式 toorun hello 作業。"
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: 2233356e-b005-4765-ae41-3a4872bda943
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/10/2017
ms.author: juanpere
ms.openlocfilehash: f6148b67129dde4580bfe9ccceafd6400fbc5976
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="schedule-and-broadcast-jobs-netnodejs"></a><span data-ttu-id="a471b-104">排程及廣播作業 (.NET/Node.js)</span><span class="sxs-lookup"><span data-stu-id="a471b-104">Schedule and broadcast jobs (.NET/Node.js)</span></span>

[!INCLUDE [iot-hub-selector-schedule-jobs](../../includes/iot-hub-selector-schedule-jobs.md)]

<span data-ttu-id="a471b-105">使用更新數百萬個裝置的 Azure IoT 中樞 tooschedule 和追蹤工作。</span><span class="sxs-lookup"><span data-stu-id="a471b-105">Use Azure IoT Hub tooschedule and track jobs that update millions of devices.</span></span> <span data-ttu-id="a471b-106">使用作業以：</span><span class="sxs-lookup"><span data-stu-id="a471b-106">Use jobs to:</span></span>

* <span data-ttu-id="a471b-107">更新所需屬性</span><span class="sxs-lookup"><span data-stu-id="a471b-107">Update desired properties</span></span>
* <span data-ttu-id="a471b-108">更新標籤</span><span class="sxs-lookup"><span data-stu-id="a471b-108">Update tags</span></span>
* <span data-ttu-id="a471b-109">叫用直接方法</span><span class="sxs-lookup"><span data-stu-id="a471b-109">Invoke direct methods</span></span>

<span data-ttu-id="a471b-110">作業會包裝其中一個動作，並追蹤 hello 執行則是根據一組裝置的裝置的兩個查詢所定義。</span><span class="sxs-lookup"><span data-stu-id="a471b-110">A job wraps one of these actions and tracks hello execution against a set of devices that is defined by a device twin query.</span></span> <span data-ttu-id="a471b-111">比方說後, 端應用程式可以使用 hello 裝置重新開機的 10,000 部裝置上的作業 tooinvoke 直接的方法。</span><span class="sxs-lookup"><span data-stu-id="a471b-111">For example, a back-end app can use a job tooinvoke a direct method on 10,000 devices that reboots hello devices.</span></span> <span data-ttu-id="a471b-112">您指定與裝置的兩個查詢的 hello 的一組裝置，然後 hello 作業 toorun 排程在未來的時間。</span><span class="sxs-lookup"><span data-stu-id="a471b-112">You specify hello set of devices with a device twin query and schedule hello job toorun at a future time.</span></span> <span data-ttu-id="a471b-113">為每個 hello 裝置 hello 工作追蹤進度接收，並執行 hello 重新開機直接的方法。</span><span class="sxs-lookup"><span data-stu-id="a471b-113">hello job tracks progress as each of hello devices receive and execute hello reboot direct method.</span></span>

<span data-ttu-id="a471b-114">toolearn 進一步了解每個這些功能，請參閱：</span><span class="sxs-lookup"><span data-stu-id="a471b-114">toolearn more about each of these capabilities, see:</span></span>

* <span data-ttu-id="a471b-115">裝置的兩個與屬性：[開始使用裝置雙][ lnk-get-started-twin]和[教學課程： 如何 toouse 裝置 twin 屬性][lnk-twin-props]</span><span class="sxs-lookup"><span data-stu-id="a471b-115">Device twin and properties: [Get started with device twins][lnk-get-started-twin] and [Tutorial: How toouse device twin properties][lnk-twin-props]</span></span>
* <span data-ttu-id="a471b-116">直接方法：[IoT 中樞開發人員指南 - 直接方法][lnk-dev-methods]和[教學課程：使用直接方法][lnk-c2d-methods]</span><span class="sxs-lookup"><span data-stu-id="a471b-116">Direct methods: [IoT Hub developer guide - direct methods][lnk-dev-methods] and [Tutorial: Use direct methods][lnk-c2d-methods]</span></span>

<span data-ttu-id="a471b-117">本教學課程說明如何：</span><span class="sxs-lookup"><span data-stu-id="a471b-117">This tutorial shows you how to:</span></span>

* <span data-ttu-id="a471b-118">建立裝置的應用程式實作直接的方法呼叫**lockDoor** hello 後端應用程式可以呼叫的。</span><span class="sxs-lookup"><span data-stu-id="a471b-118">Create a device app that implements a direct method called **lockDoor** that can be called by hello back-end app.</span></span> <span data-ttu-id="a471b-119">hello 裝置應用程式也會接收來自 hello 後端應用程式的所需的屬性變更。</span><span class="sxs-lookup"><span data-stu-id="a471b-119">hello device app also receives desired property changes from hello back-end app.</span></span>
* <span data-ttu-id="a471b-120">建立後端應用程式建立作業 toocall hello **lockDoor**直接多個裝置上的方法。</span><span class="sxs-lookup"><span data-stu-id="a471b-120">Create a back-end app that creates a job toocall hello **lockDoor** direct method on multiple devices.</span></span> <span data-ttu-id="a471b-121">另一項工作會傳送所需的屬性更新 toomultiple 裝置。</span><span class="sxs-lookup"><span data-stu-id="a471b-121">Another job sends desired property updates toomultiple devices.</span></span>

<span data-ttu-id="a471b-122">在本教學課程的 hello 最後，您有 Node.js 主控台裝置應用程式和.NET (C#) 主控台後端應用程式：</span><span class="sxs-lookup"><span data-stu-id="a471b-122">At hello end of this tutorial, you have a Node.js console device app and a .NET (C#) console back-end app:</span></span>

<span data-ttu-id="a471b-123">**simDevice.js** ，連線到 tooyour IoT 中樞時，實作 hello **lockDoor**直接方法，並控制代碼所需屬性變更。</span><span class="sxs-lookup"><span data-stu-id="a471b-123">**simDevice.js** that connects tooyour IoT hub, implements hello **lockDoor** direct method, and handles desired property changes.</span></span>

<span data-ttu-id="a471b-124">**ScheduleJob**使用作業 toocall hello **lockDoor**直接方法，並更新 hello 裝置兩個所需的多個裝置上的屬性。</span><span class="sxs-lookup"><span data-stu-id="a471b-124">**ScheduleJob** that uses jobs toocall hello **lockDoor** direct method and update hello device twin desired properties on multiple devices.</span></span>

<span data-ttu-id="a471b-125">toocomplete 本教學課程中，您需要遵循的 hello:</span><span class="sxs-lookup"><span data-stu-id="a471b-125">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="a471b-126">Visual Studio 2015 或 Visual Studio 2017。</span><span class="sxs-lookup"><span data-stu-id="a471b-126">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="a471b-127">Node.js 0.12.x 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="a471b-127">Node.js version 0.12.x or later.</span></span> <span data-ttu-id="a471b-128">hello 文章[準備開發環境][ lnk-dev-setup]描述如何 tooinstall Node.js 本教學課程中的 Windows 或 Linux。</span><span class="sxs-lookup"><span data-stu-id="a471b-128">hello article [Prepare your development environment][lnk-dev-setup] describes how tooinstall Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="a471b-129">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="a471b-129">An active Azure account.</span></span> <span data-ttu-id="a471b-130">如果您沒有帳戶，只需要幾分鐘的時間就可以建立[免費帳戶][lnk-free-trial]。</span><span class="sxs-lookup"><span data-stu-id="a471b-130">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="schedule-jobs-for-calling-a-direct-method-and-sending-device-twin-updates"></a><span data-ttu-id="a471b-131">排程呼叫直接方法及傳送裝置對應項更新的作業</span><span class="sxs-lookup"><span data-stu-id="a471b-131">Schedule jobs for calling a direct method and sending device twin updates</span></span>

<span data-ttu-id="a471b-132">在本節中，您會建立.NET 主控台應用程式 （使用 C#） 會使用作業 toocall hello **lockDoor**直接方法，並傳送所需的屬性更新 toomultiple 裝置。</span><span class="sxs-lookup"><span data-stu-id="a471b-132">In this section, you create a .NET console app (using C#) that uses jobs toocall hello **lockDoor** direct method and send desired property updates toomultiple devices.</span></span>

1. <span data-ttu-id="a471b-133">在 Visual Studio 中，將 Visual C# Windows 傳統桌面專案 toohello 目前方案使用 hello**主控台應用程式**專案範本。</span><span class="sxs-lookup"><span data-stu-id="a471b-133">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution by using hello **Console Application** project template.</span></span> <span data-ttu-id="a471b-134">名稱 hello 專案**ScheduleJob**。</span><span class="sxs-lookup"><span data-stu-id="a471b-134">Name hello project **ScheduleJob**.</span></span>

    ![新的 Visual C# Windows 傳統桌面專案][img-createapp]

1. <span data-ttu-id="a471b-136">在 [方案總管] 中，以滑鼠右鍵按一下 hello **ScheduleJob**專案，然後再按一下**管理 NuGet 封裝...**.</span><span class="sxs-lookup"><span data-stu-id="a471b-136">In Solution Explorer, right-click hello **ScheduleJob** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="a471b-137">在 hello **NuGet 套件管理員**視窗中，選取**瀏覽**，搜尋**microsoft.azure.devices**，選取**安裝**tooinstallhello **Microsoft.Azure.Devices**封裝，並接受使用規定 hello。</span><span class="sxs-lookup"><span data-stu-id="a471b-137">In hello **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** tooinstall hello **Microsoft.Azure.Devices** package, and accept hello terms of use.</span></span> <span data-ttu-id="a471b-138">此步驟中下載、 安裝，並將參考 toohello [Azure IoT 服務 SDK] [ lnk-nuget-service-sdk] NuGet 封裝和其相依性。</span><span class="sxs-lookup"><span data-stu-id="a471b-138">This step downloads, installs, and adds a reference toohello [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>

    ![NuGet 封裝管理員視窗][img-servicenuget]
1. <span data-ttu-id="a471b-140">新增下列 hello`using`在 hello hello 最上方的陳述式**Program.cs**檔案：</span><span class="sxs-lookup"><span data-stu-id="a471b-140">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
    
    ```csharp
    using Microsoft.Azure.Devices;
    using Microsoft.Azure.Devices.Shared;
    ```

1. <span data-ttu-id="a471b-141">新增下列 hello`using`若還未出現在 hello 預設陳述式中的陳述式。</span><span class="sxs-lookup"><span data-stu-id="a471b-141">Add hello following `using` statement if not already present in hello default statements.</span></span>

    ```csharp
    using System.Threading.Tasks;
    ```

1. <span data-ttu-id="a471b-142">新增下列欄位 toohello hello**程式**類別。</span><span class="sxs-lookup"><span data-stu-id="a471b-142">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="a471b-143">Hello 預留位置取代為 hello hello 中樞在 hello 上一節中所建立的 IoT 中樞連接字串。</span><span class="sxs-lookup"><span data-stu-id="a471b-143">Replace hello placeholder with hello IoT Hub connection string for hello hub that you created in hello previous section.</span></span>

    ```csharp
    static string connString = "{iot hub connection string}";
    static ServiceClient client;
    static JobClient jobClient;
    ```

1. <span data-ttu-id="a471b-144">新增下列方法 toohello hello**程式**類別：</span><span class="sxs-lookup"><span data-stu-id="a471b-144">Add hello following method toohello **Program** class:</span></span>

    ```csharp
    public static async Task MonitorJob(string jobId)
    {
        JobResponse result;
        do
        {
            result = await jobClient.GetJobAsync(jobId);
            Console.WriteLine("Job Status : " + result.Status.ToString());
            Thread.Sleep(2000);
        } while ((result.Status != JobStatus.Completed) && (result.Status != JobStatus.Failed));
    }
    ```

1. <span data-ttu-id="a471b-145">新增下列方法 toohello hello**程式**類別：</span><span class="sxs-lookup"><span data-stu-id="a471b-145">Add hello following method toohello **Program** class:</span></span>

    ```csharp
    public static async Task StartMethodJob(string jobId)
    {
        CloudToDeviceMethod directMethod = new CloudToDeviceMethod("lockDoor", TimeSpan.FromSeconds(5), TimeSpan.FromSeconds(5));

        JobResponse result = await jobClient.ScheduleDeviceMethodAsync(jobId,
            "deviceId='myDeviceId'",
            directMethod,
            DateTime.Now,
            10);

        Console.WriteLine("Started Method Job");
    }
    ```

1. <span data-ttu-id="a471b-146">新增下列方法 toohello hello**程式**類別：</span><span class="sxs-lookup"><span data-stu-id="a471b-146">Add hello following method toohello **Program** class:</span></span>

    ```csharp
    public static async Task StartTwinUpdateJob(string jobId)
    {
        var twin = new Twin();
        twin.Properties.Desired["Building"] = "43";
        twin.Properties.Desired["Floor"] = "3";
        twin.ETag = "*";

        JobResponse result = await jobClient.ScheduleTwinUpdateAsync(jobId,
            "deviceId='myDeviceId'",
            twin,
            DateTime.Now,
            10);

        Console.WriteLine("Started Twin Update Job");
    }
    ```

1. <span data-ttu-id="a471b-147">最後，加入下列行 toohello hello **Main**方法：</span><span class="sxs-lookup"><span data-stu-id="a471b-147">Finally, add hello following lines toohello **Main** method:</span></span>

    ```csharp
    jobClient = JobClient.CreateFromConnectionString(connString);

    string methodJobId = Guid.NewGuid().ToString();

    StartMethodJob(methodJobId);
    MonitorJob(methodJobId).Wait();
    Console.WriteLine("Press ENTER toorun hello next job.");
    Console.ReadLine();

    string twinUpdateJobId = Guid.NewGuid().ToString();

    StartTwinUpdateJob(twinUpdateJobId);
    MonitorJob(twinUpdateJobId).Wait();
    Console.WriteLine("Press ENTER tooexit.");
    Console.ReadLine();
    ```

1. <span data-ttu-id="a471b-148">在 hello 方案總管 中，開啟 hello**設定啟始專案...** ，請確定 hello**動作**如**ScheduleJob**專案是**啟動**。</span><span class="sxs-lookup"><span data-stu-id="a471b-148">In hello Solution Explorer, open hello **Set StartUp projects...** and make sure hello **Action** for **ScheduleJob** project is **Start**.</span></span> <span data-ttu-id="a471b-149">建置 hello 方案。</span><span class="sxs-lookup"><span data-stu-id="a471b-149">Build hello solution.</span></span>

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="a471b-150">建立模擬裝置應用程式</span><span class="sxs-lookup"><span data-stu-id="a471b-150">Create a simulated device app</span></span>

<span data-ttu-id="a471b-151">在本節中，您建立 Node.js 主控台應用程式回應 tooa 直接方法呼叫 hello 雲端，觸發程序模擬的裝置重新開機，使用 hello 報告屬性 tooenable 裝置兩個查詢 tooidentify 裝置，當它們一次啟動。</span><span class="sxs-lookup"><span data-stu-id="a471b-151">In this section, you create a Node.js console app that responds tooa direct method called by hello cloud, which triggers a simulated device reboot and uses hello reported properties tooenable device twin queries tooidentify devices and when they last rebooted.</span></span>

1. <span data-ttu-id="a471b-152">建立名為 **simDevice** 的新空白資料夾。</span><span class="sxs-lookup"><span data-stu-id="a471b-152">Create a new empty folder called **simDevice**.</span></span>  <span data-ttu-id="a471b-153">在 hello **simDevice**資料夾中，建立使用下列命令，在您的命令提示字元的 hello package.json 檔案。</span><span class="sxs-lookup"><span data-stu-id="a471b-153">In hello **simDevice** folder, create a package.json file using hello following command at your command prompt.</span></span>  <span data-ttu-id="a471b-154">接受所有的 hello 預設值：</span><span class="sxs-lookup"><span data-stu-id="a471b-154">Accept all hello defaults:</span></span>

    ```cmd/sh
    npm init
    ```

1. <span data-ttu-id="a471b-155">在您的命令提示字元中 hello **simDevice**資料夾中，執行下列命令 tooinstall hello hello **azure iot 裝置**和**azure iot 裝置-mqtt**封裝：</span><span class="sxs-lookup"><span data-stu-id="a471b-155">At your command prompt in hello **simDevice** folder, run hello following command tooinstall hello **azure-iot-device** and **azure-iot-device-mqtt** packages:</span></span>

    ```cmd/sh
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```

1. <span data-ttu-id="a471b-156">使用文字編輯器中，建立新**simDevice.js**檔案在 hello **simDevice**資料夾。</span><span class="sxs-lookup"><span data-stu-id="a471b-156">Using a text editor, create a new **simDevice.js** file in hello **simDevice** folder.</span></span>

1. <span data-ttu-id="a471b-157">新增 hello 下列的 '需要' 陳述式在 hello 開頭的 hello **simDevice.js**檔案：</span><span class="sxs-lookup"><span data-stu-id="a471b-157">Add hello following 'require' statements at hello start of hello **simDevice.js** file:</span></span>

    ```nodejs
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```

1. <span data-ttu-id="a471b-158">新增**connectionString**變數，並使用它 toocreate**用戶端**執行個體。</span><span class="sxs-lookup"><span data-stu-id="a471b-158">Add a **connectionString** variable and use it toocreate a **Client** instance.</span></span> <span data-ttu-id="a471b-159">請確定 tooreplace hello 預留位置值適當 tooyour 安裝程式。</span><span class="sxs-lookup"><span data-stu-id="a471b-159">Make sure tooreplace hello placeholders with values appropriate tooyour setup.</span></span>

    ```nodejs
    var connectionString = 'HostName={youriothostname};DeviceId={yourdeviceid};SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```

1. <span data-ttu-id="a471b-160">加入下列函式 toohandle hello hello **lockDoor**方法。</span><span class="sxs-lookup"><span data-stu-id="a471b-160">Add hello following function toohandle hello **lockDoor** method.</span></span>

    ```nodejs
    var onLockDoor = function(request, response) {
   
        // Respond hello cloud app for hello direct method
        response.send(200, function(err) {
            if (!err) {
                console.error('An error occured when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.');
            }
        });
   
        console.log('Locking Door!');
    };
    ```

1. <span data-ttu-id="a471b-161">新增下列程式碼的 hello tooregister hello 處理常式的 hello **lockDoor**方法。</span><span class="sxs-lookup"><span data-stu-id="a471b-161">Add hello following code tooregister hello handler for hello **lockDoor** method.</span></span>

    ```nodejs
    client.open(function(err) {
        if (err) {
            console.error('Could not connect tooIotHub client.');
        }  else {
            console.log('Client connected tooIoT Hub.  Waiting for lockDoor direct method.');
            client.onDeviceMethod('lockDoor', onLockDoor);
        }
    });
    ```

1. <span data-ttu-id="a471b-162">儲存並關閉 hello **simDevice.js**檔案。</span><span class="sxs-lookup"><span data-stu-id="a471b-162">Save and close hello **simDevice.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="a471b-163">簡單 tookeep 方面，本教學課程未實作任何重試原則。</span><span class="sxs-lookup"><span data-stu-id="a471b-163">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="a471b-164">在實際執行程式碼，您應該實作重試原則 （例如指數型輪詢），做為建議 hello MSDN 文件中[暫時性錯誤處理][lnk-transient-faults]。</span><span class="sxs-lookup"><span data-stu-id="a471b-164">In production code, you should implement retry policies (such as an exponential backoff), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>

## <a name="run-hello-apps"></a><span data-ttu-id="a471b-165">執行 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="a471b-165">Run hello apps</span></span>

<span data-ttu-id="a471b-166">現在您已經準備就緒 toorun hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a471b-166">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="a471b-167">在 hello 命令提示字元中 hello **simDevice**資料夾中，執行下列命令 toobegin 接聽 hello 重新開機直接方法 hello。</span><span class="sxs-lookup"><span data-stu-id="a471b-167">At hello command prompt in hello **simDevice** folder, run hello following command toobegin listening for hello reboot direct method.</span></span>

    ```cmd/sh
    node simDevice.js
    ```

1. <span data-ttu-id="a471b-168">執行的 hello C# 主控台應用程式**ScheduleJob**以滑鼠右鍵按一下 hello **ScheduleJob**專案，然後選取**偵錯**和**開始新執行個體**.</span><span class="sxs-lookup"><span data-stu-id="a471b-168">Run hello C# console app **ScheduleJob** by right-clicking on hello **ScheduleJob** project, then selecting **Debug** and **Start new instance**.</span></span>

1. <span data-ttu-id="a471b-169">您會看到從裝置和後端應用程式的 hello 輸出。</span><span class="sxs-lookup"><span data-stu-id="a471b-169">You see hello output from both device and back-end apps.</span></span>

    ![Tooschedule 工作執行 hello 應用程式][img-schedulejobs]

## <a name="next-steps"></a><span data-ttu-id="a471b-171">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a471b-171">Next steps</span></span>

<span data-ttu-id="a471b-172">在此教學課程中，您可以使用作業 tooschedule 直接方法 tooa 裝置和 hello 更新的 hello 裝置兩個的屬性。</span><span class="sxs-lookup"><span data-stu-id="a471b-172">In this tutorial, you used a job tooschedule a direct method tooa device and hello update of hello device twin's properties.</span></span>

<span data-ttu-id="a471b-173">開始使用 IoT 中樞與裝置管理模式，例如遠端透過 hello 空中韌體更新，讀取 toocontinue[教學課程： 如何 toodo 韌體更新][lnk-fwupdate]。</span><span class="sxs-lookup"><span data-stu-id="a471b-173">toocontinue getting started with IoT Hub and device management patterns such as remote over hello air firmware update, read [Tutorial: How toodo a firmware update][lnk-fwupdate].</span></span>

<span data-ttu-id="a471b-174">請參閱 < 開始使用 IoT 中樞 toocontinue[入門 IoT 邊緣][lnk-iot-edge]。</span><span class="sxs-lookup"><span data-stu-id="a471b-174">toocontinue getting started with IoT Hub, see [Getting started with IoT Edge][lnk-iot-edge].</span></span>

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-node-schedule-jobs/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-node-schedule-jobs/createnetapp.png
[img-schedulejobs]: media/iot-hub-csharp-node-schedule-jobs/schedulejobs.png

[lnk-get-started-twin]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-props]: iot-hub-node-node-twin-how-to-configure.md
[lnk-c2d-methods]: iot-hub-node-node-direct-methods.md
[lnk-dev-methods]: iot-hub-devguide-direct-methods.md
[lnk-fwupdate]: iot-hub-node-node-firmware-update.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
