---
title: "使用 Azure IoT 中樞 (.NET/Node) 排定作業 | Microsoft Docs"
description: "如何排定 Azure IoT 中樞作業在多個裝置上叫用直接方法。 您可以使用適用於 Node.js 的 Azure IoT 裝置 SDK，實作模擬裝置應用程式，也可以使用適用於 .NET 的 Azure IoT 服務 SDK，實作服務應用程式以執行作業。"
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
ms.openlocfilehash: a8f4f34aa99c4a9966957cac213ec9170de80a46
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="schedule-and-broadcast-jobs-netnodejs"></a><span data-ttu-id="6b0a5-104">排程及廣播作業 (.NET/Node.js)</span><span class="sxs-lookup"><span data-stu-id="6b0a5-104">Schedule and broadcast jobs (.NET/Node.js)</span></span>

[!INCLUDE [iot-hub-selector-schedule-jobs](../../includes/iot-hub-selector-schedule-jobs.md)]

<span data-ttu-id="6b0a5-105">使用 Azure IoT 中樞排程和追蹤會更新數百萬部裝置的作業。</span><span class="sxs-lookup"><span data-stu-id="6b0a5-105">Use Azure IoT Hub to schedule and track jobs that update millions of devices.</span></span> <span data-ttu-id="6b0a5-106">使用作業以：</span><span class="sxs-lookup"><span data-stu-id="6b0a5-106">Use jobs to:</span></span>

* <span data-ttu-id="6b0a5-107">更新所需屬性</span><span class="sxs-lookup"><span data-stu-id="6b0a5-107">Update desired properties</span></span>
* <span data-ttu-id="6b0a5-108">更新標籤</span><span class="sxs-lookup"><span data-stu-id="6b0a5-108">Update tags</span></span>
* <span data-ttu-id="6b0a5-109">叫用直接方法</span><span class="sxs-lookup"><span data-stu-id="6b0a5-109">Invoke direct methods</span></span>

<span data-ttu-id="6b0a5-110">作業會包裝上述其中一個動作，然後針對由裝置對應項查詢所定義的一組裝置，追蹤執行進度。</span><span class="sxs-lookup"><span data-stu-id="6b0a5-110">A job wraps one of these actions and tracks the execution against a set of devices that is defined by a device twin query.</span></span> <span data-ttu-id="6b0a5-111">例如，後端應用程式可以使用作業，以在 10,000 部裝置上叫用重新開機裝置的直接方法。</span><span class="sxs-lookup"><span data-stu-id="6b0a5-111">For example, a back-end app can use a job to invoke a direct method on 10,000 devices that reboots the devices.</span></span> <span data-ttu-id="6b0a5-112">您以裝置對應項查詢指定一組裝置，並排程在未來的時間執行作業。</span><span class="sxs-lookup"><span data-stu-id="6b0a5-112">You specify the set of devices with a device twin query and schedule the job to run at a future time.</span></span> <span data-ttu-id="6b0a5-113">作業會在每部裝置接收和執行重新開機直接方法時追蹤進度。</span><span class="sxs-lookup"><span data-stu-id="6b0a5-113">The job tracks progress as each of the devices receive and execute the reboot direct method.</span></span>

<span data-ttu-id="6b0a5-114">若要一一了解這些功能，請參閱：</span><span class="sxs-lookup"><span data-stu-id="6b0a5-114">To learn more about each of these capabilities, see:</span></span>

* <span data-ttu-id="6b0a5-115">裝置對應項和屬性：[開始使用裝置對應項][lnk-get-started-twin]和[教學課程：如何使用裝置對應項屬性][lnk-twin-props]</span><span class="sxs-lookup"><span data-stu-id="6b0a5-115">Device twin and properties: [Get started with device twins][lnk-get-started-twin] and [Tutorial: How to use device twin properties][lnk-twin-props]</span></span>
* <span data-ttu-id="6b0a5-116">直接方法：[IoT 中樞開發人員指南 - 直接方法][lnk-dev-methods]和[教學課程：使用直接方法][lnk-c2d-methods]</span><span class="sxs-lookup"><span data-stu-id="6b0a5-116">Direct methods: [IoT Hub developer guide - direct methods][lnk-dev-methods] and [Tutorial: Use direct methods][lnk-c2d-methods]</span></span>

<span data-ttu-id="6b0a5-117">本教學課程說明如何：</span><span class="sxs-lookup"><span data-stu-id="6b0a5-117">This tutorial shows you how to:</span></span>

* <span data-ttu-id="6b0a5-118">建立實作 **lockDoor** 直接方法的裝置應用程式，後端應用程式可以呼叫此方法。</span><span class="sxs-lookup"><span data-stu-id="6b0a5-118">Create a device app that implements a direct method called **lockDoor** that can be called by the back-end app.</span></span> <span data-ttu-id="6b0a5-119">裝置應用程式也會從後端應用程式收到所需的屬性變更。</span><span class="sxs-lookup"><span data-stu-id="6b0a5-119">The device app also receives desired property changes from the back-end app.</span></span>
* <span data-ttu-id="6b0a5-120">建立後端應用程式，以建立作業在多部裝置上呼叫 **lockDoor** 直接方法。</span><span class="sxs-lookup"><span data-stu-id="6b0a5-120">Create a back-end app that creates a job to call the **lockDoor** direct method on multiple devices.</span></span> <span data-ttu-id="6b0a5-121">另一項作業會將所需的屬性更新傳送到多部裝置。</span><span class="sxs-lookup"><span data-stu-id="6b0a5-121">Another job sends desired property updates to multiple devices.</span></span>

<span data-ttu-id="6b0a5-122">在本教學課程結束時，您會有 Node.js 主控台裝置應用程式和 .NET (C#) 主控台後端應用程式：</span><span class="sxs-lookup"><span data-stu-id="6b0a5-122">At the end of this tutorial, you have a Node.js console device app and a .NET (C#) console back-end app:</span></span>

<span data-ttu-id="6b0a5-123">**simDevice.js** 會連線至 IoT 中樞，實作 **lockDoor** 直接方法，並處理所需的屬性變更。</span><span class="sxs-lookup"><span data-stu-id="6b0a5-123">**simDevice.js** that connects to your IoT hub, implements the **lockDoor** direct method, and handles desired property changes.</span></span>

<span data-ttu-id="6b0a5-124">**ScheduleJob** 會使用作業呼叫 **lockDoor** 直接方法，並在多部裝置上更新裝置對應項所需的屬性。</span><span class="sxs-lookup"><span data-stu-id="6b0a5-124">**ScheduleJob** that uses jobs to call the **lockDoor** direct method and update the device twin desired properties on multiple devices.</span></span>

<span data-ttu-id="6b0a5-125">若要完成此教學課程，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="6b0a5-125">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="6b0a5-126">Visual Studio 2015 或 Visual Studio 2017。</span><span class="sxs-lookup"><span data-stu-id="6b0a5-126">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="6b0a5-127">Node.js 0.12.x 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="6b0a5-127">Node.js version 0.12.x or later.</span></span> <span data-ttu-id="6b0a5-128">[準備您的開發環境][lnk-dev-setup]一文說明如何在 Windows 或 Linux 上安裝本教學課程的 Node.js。</span><span class="sxs-lookup"><span data-stu-id="6b0a5-128">The article [Prepare your development environment][lnk-dev-setup] describes how to install Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="6b0a5-129">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="6b0a5-129">An active Azure account.</span></span> <span data-ttu-id="6b0a5-130">如果您沒有帳戶，只需要幾分鐘的時間就可以建立[免費帳戶][lnk-free-trial]。</span><span class="sxs-lookup"><span data-stu-id="6b0a5-130">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="schedule-jobs-for-calling-a-direct-method-and-sending-device-twin-updates"></a><span data-ttu-id="6b0a5-131">排程呼叫直接方法及傳送裝置對應項更新的作業</span><span class="sxs-lookup"><span data-stu-id="6b0a5-131">Schedule jobs for calling a direct method and sending device twin updates</span></span>

<span data-ttu-id="6b0a5-132">在本節中，您要建立 .NET 主控台應用程式 (使用 C#)，使用作業呼叫 **lockDoor** 直接方法，並將所需的屬性更新傳送至多部裝置。</span><span class="sxs-lookup"><span data-stu-id="6b0a5-132">In this section, you create a .NET console app (using C#) that uses jobs to call the **lockDoor** direct method and send desired property updates to multiple devices.</span></span>

1. <span data-ttu-id="6b0a5-133">在 Visual Studio 中，使用 [主控台應用程式] 專案範本，將 Visual C# Windows 傳統桌面專案新增至目前的方案。</span><span class="sxs-lookup"><span data-stu-id="6b0a5-133">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution by using the **Console Application** project template.</span></span> <span data-ttu-id="6b0a5-134">將專案命名為 **ScheduleJob**。</span><span class="sxs-lookup"><span data-stu-id="6b0a5-134">Name the project **ScheduleJob**.</span></span>

    ![新的 Visual C# Windows 傳統桌面專案][img-createapp]

1. <span data-ttu-id="6b0a5-136">在 [方案總管] 中，以滑鼠右鍵按一下 **ScheduleJob** 專案，然後按一下 [管理 NuGet 套件...]。</span><span class="sxs-lookup"><span data-stu-id="6b0a5-136">In Solution Explorer, right-click the **ScheduleJob** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="6b0a5-137">在 [Nuget 套件管理員] 視窗中選取 [瀏覽]、搜尋 **microsoft.azure.devices**、選取 [安裝] 以安裝 **Microsoft.Azure.Devices** 套件，並接受使用規定。</span><span class="sxs-lookup"><span data-stu-id="6b0a5-137">In the **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** to install the **Microsoft.Azure.Devices** package, and accept the terms of use.</span></span> <span data-ttu-id="6b0a5-138">此步驟會下載及安裝 [Azure IoT 服務 SDK][lnk-nuget-service-sdk] NuGet 套件與其相依項目，並加入對它的參考。</span><span class="sxs-lookup"><span data-stu-id="6b0a5-138">This step downloads, installs, and adds a reference to the [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>

    ![NuGet 封裝管理員視窗][img-servicenuget]
1. <span data-ttu-id="6b0a5-140">在 **Program.cs** 檔案開頭處新增下列 `using` 陳述式：</span><span class="sxs-lookup"><span data-stu-id="6b0a5-140">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
    
    ```csharp
    using Microsoft.Azure.Devices;
    using Microsoft.Azure.Devices.Shared;
    ```

1. <span data-ttu-id="6b0a5-141">新增下列 `using` 陳述式 (如果預設陳述式中尚不存在)。</span><span class="sxs-lookup"><span data-stu-id="6b0a5-141">Add the following `using` statement if not already present in the default statements.</span></span>

    ```csharp
    using System.Threading.Tasks;
    ```

1. <span data-ttu-id="6b0a5-142">將下列欄位新增到 **Program** 類別。</span><span class="sxs-lookup"><span data-stu-id="6b0a5-142">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="6b0a5-143">將預留位置替換為您在上一節中為中樞所建立的 IoT 中樞連接字串。</span><span class="sxs-lookup"><span data-stu-id="6b0a5-143">Replace the placeholder with the IoT Hub connection string for the hub that you created in the previous section.</span></span>

    ```csharp
    static string connString = "{iot hub connection string}";
    static ServiceClient client;
    static JobClient jobClient;
    ```

1. <span data-ttu-id="6b0a5-144">將下列方法加入至 **Program** 類別：</span><span class="sxs-lookup"><span data-stu-id="6b0a5-144">Add the following method to the **Program** class:</span></span>

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

1. <span data-ttu-id="6b0a5-145">將下列方法加入至 **Program** 類別：</span><span class="sxs-lookup"><span data-stu-id="6b0a5-145">Add the following method to the **Program** class:</span></span>

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

1. <span data-ttu-id="6b0a5-146">將下列方法加入至 **Program** 類別：</span><span class="sxs-lookup"><span data-stu-id="6b0a5-146">Add the following method to the **Program** class:</span></span>

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

1. <span data-ttu-id="6b0a5-147">最後，將下列幾行加入至 **Main** 方法：</span><span class="sxs-lookup"><span data-stu-id="6b0a5-147">Finally, add the following lines to the **Main** method:</span></span>

    ```csharp
    jobClient = JobClient.CreateFromConnectionString(connString);

    string methodJobId = Guid.NewGuid().ToString();

    StartMethodJob(methodJobId);
    MonitorJob(methodJobId).Wait();
    Console.WriteLine("Press ENTER to run the next job.");
    Console.ReadLine();

    string twinUpdateJobId = Guid.NewGuid().ToString();

    StartTwinUpdateJob(twinUpdateJobId);
    MonitorJob(twinUpdateJobId).Wait();
    Console.WriteLine("Press ENTER to exit.");
    Console.ReadLine();
    ```

1. <span data-ttu-id="6b0a5-148">在 [方案總管] 中，開啟 [設定起始專案...]，並確定 **ScheduleJob** 專案的 [動作] 是 [啟動]。</span><span class="sxs-lookup"><span data-stu-id="6b0a5-148">In the Solution Explorer, open the **Set StartUp projects...** and make sure the **Action** for **ScheduleJob** project is **Start**.</span></span> <span data-ttu-id="6b0a5-149">建置方案。</span><span class="sxs-lookup"><span data-stu-id="6b0a5-149">Build the solution.</span></span>

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="6b0a5-150">建立模擬裝置應用程式</span><span class="sxs-lookup"><span data-stu-id="6b0a5-150">Create a simulated device app</span></span>

<span data-ttu-id="6b0a5-151">在本節中，您會建立 Node.js 主控台應用程式，它會回應雲端所呼叫的直接方法，這會讓模擬的裝置重新啟動，並使用報告屬性來啟用裝置對應項查詢，以識別裝置以及上次重新啟動的時機。</span><span class="sxs-lookup"><span data-stu-id="6b0a5-151">In this section, you create a Node.js console app that responds to a direct method called by the cloud, which triggers a simulated device reboot and uses the reported properties to enable device twin queries to identify devices and when they last rebooted.</span></span>

1. <span data-ttu-id="6b0a5-152">建立名為 **simDevice** 的新空白資料夾。</span><span class="sxs-lookup"><span data-stu-id="6b0a5-152">Create a new empty folder called **simDevice**.</span></span>  <span data-ttu-id="6b0a5-153">在命令提示字元中，使用下列命令在 **simDevice** 資料夾中建立 package.json 檔案。</span><span class="sxs-lookup"><span data-stu-id="6b0a5-153">In the **simDevice** folder, create a package.json file using the following command at your command prompt.</span></span>  <span data-ttu-id="6b0a5-154">接受所有預設值：</span><span class="sxs-lookup"><span data-stu-id="6b0a5-154">Accept all the defaults:</span></span>

    ```cmd/sh
    npm init
    ```

1. <span data-ttu-id="6b0a5-155">在 **simDevice** 資料夾中，於命令提示字元執行下列命令以安裝 **azure-iot-device** 和 **azure-iot-device-mqtt** 套件：</span><span class="sxs-lookup"><span data-stu-id="6b0a5-155">At your command prompt in the **simDevice** folder, run the following command to install the **azure-iot-device** and **azure-iot-device-mqtt** packages:</span></span>

    ```cmd/sh
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```

1. <span data-ttu-id="6b0a5-156">使用文字編輯器，在 [simDevice] 資料夾中建立新的 **simDevice.js** 檔案。</span><span class="sxs-lookup"><span data-stu-id="6b0a5-156">Using a text editor, create a new **simDevice.js** file in the **simDevice** folder.</span></span>

1. <span data-ttu-id="6b0a5-157">在 **simDevice.js** 檔案的開頭新增下列 'require' 陳述式：</span><span class="sxs-lookup"><span data-stu-id="6b0a5-157">Add the following 'require' statements at the start of the **simDevice.js** file:</span></span>

    ```nodejs
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```

1. <span data-ttu-id="6b0a5-158">新增 **connectionString** 變數，並用它來建立**用戶端**執行個體。</span><span class="sxs-lookup"><span data-stu-id="6b0a5-158">Add a **connectionString** variable and use it to create a **Client** instance.</span></span> <span data-ttu-id="6b0a5-159">務必以適合您設定的值來取代預留位置。</span><span class="sxs-lookup"><span data-stu-id="6b0a5-159">Make sure to replace the placeholders with values appropriate to your setup.</span></span>

    ```nodejs
    var connectionString = 'HostName={youriothostname};DeviceId={yourdeviceid};SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```

1. <span data-ttu-id="6b0a5-160">新增下列函式以處理 **lockDoor** 方法。</span><span class="sxs-lookup"><span data-stu-id="6b0a5-160">Add the following function to handle the **lockDoor** method.</span></span>

    ```nodejs
    var onLockDoor = function(request, response) {
   
        // Respond the cloud app for the direct method
        response.send(200, function(err) {
            if (!err) {
                console.error('An error occured when sending a method response:\n' + err.toString());
            } else {
                console.log('Response to method \'' + request.methodName + '\' sent successfully.');
            }
        });
   
        console.log('Locking Door!');
    };
    ```

1. <span data-ttu-id="6b0a5-161">新增下列程式碼以註冊 **lockDoor** 方法的處理常式。</span><span class="sxs-lookup"><span data-stu-id="6b0a5-161">Add the following code to register the handler for the **lockDoor** method.</span></span>

    ```nodejs
    client.open(function(err) {
        if (err) {
            console.error('Could not connect to IotHub client.');
        }  else {
            console.log('Client connected to IoT Hub.  Waiting for lockDoor direct method.');
            client.onDeviceMethod('lockDoor', onLockDoor);
        }
    });
    ```

1. <span data-ttu-id="6b0a5-162">儲存並關閉 **simDevice.js** 檔案。</span><span class="sxs-lookup"><span data-stu-id="6b0a5-162">Save and close the **simDevice.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="6b0a5-163">為了簡單起見，本教學課程不會實作任何重試原則。</span><span class="sxs-lookup"><span data-stu-id="6b0a5-163">To keep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="6b0a5-164">在實際程式碼中，您應該如 MSDN 文章[暫時性錯誤處理][lnk-transient-faults]所建議，實作重試原則 (例如指數型輪詢)。</span><span class="sxs-lookup"><span data-stu-id="6b0a5-164">In production code, you should implement retry policies (such as an exponential backoff), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>

## <a name="run-the-apps"></a><span data-ttu-id="6b0a5-165">執行應用程式</span><span class="sxs-lookup"><span data-stu-id="6b0a5-165">Run the apps</span></span>

<span data-ttu-id="6b0a5-166">您現在可以開始執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="6b0a5-166">You are now ready to run the apps.</span></span>

1. <span data-ttu-id="6b0a5-167">在命令提示字元中，於 **simDevice** 資料夾中執行下列命令來開始接聽重新啟動直接方法。</span><span class="sxs-lookup"><span data-stu-id="6b0a5-167">At the command prompt in the **simDevice** folder, run the following command to begin listening for the reboot direct method.</span></span>

    ```cmd/sh
    node simDevice.js
    ```

1. <span data-ttu-id="6b0a5-168">執行 C# 主控台應用程式 **ScheduleJob** - 以滑鼠右鍵按一下 **ScheduleJob** 專案，然後選取 [偵錯] 和 [開始新執行個體]。</span><span class="sxs-lookup"><span data-stu-id="6b0a5-168">Run the C# console app **ScheduleJob** by right-clicking on the **ScheduleJob** project, then selecting **Debug** and **Start new instance**.</span></span>

1. <span data-ttu-id="6b0a5-169">您會看到來自裝置及後端應用程式的輸出。</span><span class="sxs-lookup"><span data-stu-id="6b0a5-169">You see the output from both device and back-end apps.</span></span>

    ![執行應用程式以排程作業][img-schedulejobs]

## <a name="next-steps"></a><span data-ttu-id="6b0a5-171">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6b0a5-171">Next steps</span></span>

<span data-ttu-id="6b0a5-172">在本教學課程中，您已使用作業來排定裝置的直接方法，以及更新裝置對應項 (twin) 的屬性。</span><span class="sxs-lookup"><span data-stu-id="6b0a5-172">In this tutorial, you used a job to schedule a direct method to a device and the update of the device twin's properties.</span></span>

<span data-ttu-id="6b0a5-173">若要繼續開始使用「IoT 中樞」和裝置管理模式 (例如遠端無線韌體更新)，請參閱[教學課程：如何進行韌體更新][lnk-fwupdate]。</span><span class="sxs-lookup"><span data-stu-id="6b0a5-173">To continue getting started with IoT Hub and device management patterns such as remote over the air firmware update, read [Tutorial: How to do a firmware update][lnk-fwupdate].</span></span>

<span data-ttu-id="6b0a5-174">若要繼續開始使用 IoT 中樞，請參閱[開始使用 IoT Edge][lnk-iot-edge]。</span><span class="sxs-lookup"><span data-stu-id="6b0a5-174">To continue getting started with IoT Hub, see [Getting started with IoT Edge][lnk-iot-edge].</span></span>

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
