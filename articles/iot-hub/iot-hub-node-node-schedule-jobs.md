---
title: "aaaSchedule 作業與 Azure IoT 中樞 （節點） |Microsoft 文件"
description: "如何 tooschedule Azure IoT 中樞工作 tooinvoke 上多個裝置的直接的方法。 您可以使用 hello Azure IoT Sdk for Node.js tooimplement hello 模擬裝置的應用程式和服務應用程式 toorun hello 作業。"
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
ms.date: 09/30/2016
ms.author: juanpere
ms.openlocfilehash: be293362447fbcddaa3433b66f208f22545fe0c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="schedule-and-broadcast-jobs-node"></a><span data-ttu-id="d76e1-104">排定及廣播作業 (Node)</span><span class="sxs-lookup"><span data-stu-id="d76e1-104">Schedule and broadcast jobs (Node)</span></span>

[!INCLUDE [iot-hub-selector-schedule-jobs](../../includes/iot-hub-selector-schedule-jobs.md)]

<span data-ttu-id="d76e1-105">Azure IoT 中樞是完全受管理的服務，可讓後端應用程式 toocreate 和追蹤作業的排程並更新數百萬個裝置。</span><span class="sxs-lookup"><span data-stu-id="d76e1-105">Azure IoT Hub is a fully managed service that enables a back-end app toocreate and track jobs that schedule and update millions of devices.</span></span>  <span data-ttu-id="d76e1-106">作業可以用於 hello 下列動作：</span><span class="sxs-lookup"><span data-stu-id="d76e1-106">Jobs can be used for hello following actions:</span></span>

* <span data-ttu-id="d76e1-107">更新所需屬性</span><span class="sxs-lookup"><span data-stu-id="d76e1-107">Update desired properties</span></span>
* <span data-ttu-id="d76e1-108">更新標籤</span><span class="sxs-lookup"><span data-stu-id="d76e1-108">Update tags</span></span>
* <span data-ttu-id="d76e1-109">叫用直接方法</span><span class="sxs-lookup"><span data-stu-id="d76e1-109">Invoke direct methods</span></span>

<span data-ttu-id="d76e1-110">就概念而言，作業會包裝其中一個動作，並追蹤 hello 根據一組裝置，裝置的兩個查詢所定義的執行進度。</span><span class="sxs-lookup"><span data-stu-id="d76e1-110">Conceptually, a job wraps one of these actions and tracks hello progress of execution against a set of devices, which is defined by a device twin query.</span></span>  <span data-ttu-id="d76e1-111">例如後, 端應用程式可以使用作業 tooinvoke 重新開機方法上 10,000 部裝置，裝置的兩個查詢所指定，以及排程在未來的時間。</span><span class="sxs-lookup"><span data-stu-id="d76e1-111">For example, a back-end app can use a job tooinvoke a reboot method on 10,000 devices, specified by a device twin query and scheduled at a future time.</span></span>  <span data-ttu-id="d76e1-112">當這些裝置接收並執行 hello 重新開機方法，該應用程式可以再追蹤進度。</span><span class="sxs-lookup"><span data-stu-id="d76e1-112">That application can then track progress as each of those devices receive and execute hello reboot method.</span></span>

<span data-ttu-id="d76e1-113">從下列文章深入了解這當中的每一項功能：</span><span class="sxs-lookup"><span data-stu-id="d76e1-113">Learn more about each of these capabilities in these articles:</span></span>

* <span data-ttu-id="d76e1-114">裝置的兩個與屬性：[開始使用裝置雙][ lnk-get-started-twin]和[教學課程： 如何 toouse 裝置 twin 屬性][lnk-twin-props]</span><span class="sxs-lookup"><span data-stu-id="d76e1-114">Device twin and properties: [Get started with device twins][lnk-get-started-twin] and [Tutorial: How toouse device twin properties][lnk-twin-props]</span></span>
* <span data-ttu-id="d76e1-115">直接方法：[IoT 中樞開發人員指南 - 直接方法][lnk-dev-methods]和[教學課程：直接方法][lnk-c2d-methods]</span><span class="sxs-lookup"><span data-stu-id="d76e1-115">direct methods: [IoT Hub developer guide - direct methods][lnk-dev-methods] and [Tutorial: direct methods][lnk-c2d-methods]</span></span>

<span data-ttu-id="d76e1-116">本教學課程說明如何：</span><span class="sxs-lookup"><span data-stu-id="d76e1-116">This tutorial shows you how to:</span></span>

* <span data-ttu-id="d76e1-117">建立模擬的裝置應用程式有直接的方法可讓**lockDoor** hello 方案後端可以呼叫它。</span><span class="sxs-lookup"><span data-stu-id="d76e1-117">Create a simulated device app that has a direct method which enables **lockDoor** which can be called by hello solution back end.</span></span>
* <span data-ttu-id="d76e1-118">建立 Node.js 的主控台應用程式，該呼叫 hello **lockDoor**直接的方法中使用工作和更新的 hello hello 模擬的裝置應用程式所需使用 裝置工作的屬性。</span><span class="sxs-lookup"><span data-stu-id="d76e1-118">Create a Node.js console app that calls hello **lockDoor** direct method in hello simulated device app using a job and updates hello desired properties using a device job.</span></span>

<span data-ttu-id="d76e1-119">在本教學課程的 hello 最後，您有兩個 Node.js 主控台應用程式：</span><span class="sxs-lookup"><span data-stu-id="d76e1-119">At hello end of this tutorial, you have two Node.js console apps:</span></span>

<span data-ttu-id="d76e1-120">**simDevice.js**，這與 hello 裝置身分識別連接 tooyour IoT 中樞，並接收**lockDoor**直接方法。</span><span class="sxs-lookup"><span data-stu-id="d76e1-120">**simDevice.js**, which connects tooyour IoT hub with hello device identity and receives a **lockDoor** direct method.</span></span>

<span data-ttu-id="d76e1-121">**scheduleJobService.js**，呼叫直接的方法在 hello 模擬的裝置的應用程式和更新 hello 裝置中兩個的使用作業所需的屬性。</span><span class="sxs-lookup"><span data-stu-id="d76e1-121">**scheduleJobService.js**, which calls a direct method in hello simulated device app and update hello device twin's desired properties using a job.</span></span>

<span data-ttu-id="d76e1-122">toocomplete 本教學課程中，您需要遵循的 hello:</span><span class="sxs-lookup"><span data-stu-id="d76e1-122">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="d76e1-123">Node.js 0.12.x 版或更新版本，</span><span class="sxs-lookup"><span data-stu-id="d76e1-123">Node.js version 0.12.x or later,</span></span> <br/>  <span data-ttu-id="d76e1-124">[準備開發環境][ lnk-dev-setup]描述如何 tooinstall Node.js 本教學課程中的 Windows 或 Linux。</span><span class="sxs-lookup"><span data-stu-id="d76e1-124">[Prepare your development environment][lnk-dev-setup] describes how tooinstall Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="d76e1-125">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="d76e1-125">An active Azure account.</span></span> <span data-ttu-id="d76e1-126">(如果您沒有帳戶，只需要幾分鐘的時間就可以建立[免費帳戶][lnk-free-trial]。)</span><span class="sxs-lookup"><span data-stu-id="d76e1-126">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="d76e1-127">建立模擬裝置應用程式</span><span class="sxs-lookup"><span data-stu-id="d76e1-127">Create a simulated device app</span></span>
<span data-ttu-id="d76e1-128">在本節中，您建立 Node.js 主控台應用程式回應 tooa 直接方法呼叫 hello 雲端，觸發程序模擬的裝置重新開機，使用 hello 報告屬性 tooenable 裝置兩個查詢 tooidentify 裝置，當它們一次啟動。</span><span class="sxs-lookup"><span data-stu-id="d76e1-128">In this section, you create a Node.js console app that responds tooa direct method called by hello cloud, which triggers a simulated device reboot and uses hello reported properties tooenable device twin queries tooidentify devices and when they last rebooted.</span></span>

1. <span data-ttu-id="d76e1-129">建立名為 **simDevice** 的新空白資料夾。</span><span class="sxs-lookup"><span data-stu-id="d76e1-129">Create a new empty folder called **simDevice**.</span></span>  <span data-ttu-id="d76e1-130">在 hello **simDevice**資料夾中，建立使用下列命令，在您的命令提示字元的 hello package.json 檔案。</span><span class="sxs-lookup"><span data-stu-id="d76e1-130">In hello **simDevice** folder, create a package.json file using hello following command at your command prompt.</span></span>  <span data-ttu-id="d76e1-131">接受所有的 hello 預設值：</span><span class="sxs-lookup"><span data-stu-id="d76e1-131">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="d76e1-132">在您的命令提示字元中 hello **simDevice**資料夾中，執行下列命令 tooinstall hello hello **azure iot 裝置**裝置 SDK 封裝和**azure iot 裝置-mqtt**封裝：</span><span class="sxs-lookup"><span data-stu-id="d76e1-132">At your command prompt in hello **simDevice** folder, run hello following command tooinstall hello **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="d76e1-133">使用文字編輯器中，建立新**simDevice.js**檔案在 hello **simDevice**資料夾。</span><span class="sxs-lookup"><span data-stu-id="d76e1-133">Using a text editor, create a new **simDevice.js** file in hello **simDevice** folder.</span></span>
4. <span data-ttu-id="d76e1-134">新增 hello 下列的 '需要' 陳述式在 hello 開頭的 hello **simDevice.js**檔案：</span><span class="sxs-lookup"><span data-stu-id="d76e1-134">Add hello following 'require' statements at hello start of hello **simDevice.js** file:</span></span>
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
5. <span data-ttu-id="d76e1-135">新增**connectionString**變數，並使用它 toocreate**用戶端**執行個體。</span><span class="sxs-lookup"><span data-stu-id="d76e1-135">Add a **connectionString** variable and use it toocreate a **Client** instance.</span></span>  
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId={yourdeviceid};SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```
6. <span data-ttu-id="d76e1-136">加入下列函式 toohandle hello hello **lockDoor**方法。</span><span class="sxs-lookup"><span data-stu-id="d76e1-136">Add hello following function toohandle hello **lockDoor** method.</span></span>
   
    ```
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
7. <span data-ttu-id="d76e1-137">新增下列程式碼的 hello tooregister hello 處理常式的 hello **lockDoor**方法。</span><span class="sxs-lookup"><span data-stu-id="d76e1-137">Add hello following code tooregister hello handler for hello **lockDoor** method.</span></span>
   
    ```
    client.open(function(err) {
        if (err) {
            console.error('Could not connect tooIotHub client.');
        }  else {
            console.log('Client connected tooIoT Hub. Register handler for lockDoor direct method.');
            client.onDeviceMethod('lockDoor', onLockDoor);
        }
    });
    ```
8. <span data-ttu-id="d76e1-138">儲存並關閉 hello **simDevice.js**檔案。</span><span class="sxs-lookup"><span data-stu-id="d76e1-138">Save and close hello **simDevice.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="d76e1-139">簡單 tookeep 方面，本教學課程未實作任何重試原則。</span><span class="sxs-lookup"><span data-stu-id="d76e1-139">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="d76e1-140">在實際執行程式碼，您應該實作重試原則 （例如指數型輪詢），做為建議 hello MSDN 文件中[暫時性錯誤處理][lnk-transient-faults]。</span><span class="sxs-lookup"><span data-stu-id="d76e1-140">In production code, you should implement retry policies (such as an exponential backoff), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="schedule-jobs-for-calling-a-direct-method-and-updating-a-device-twins-properties"></a><span data-ttu-id="d76e1-141">排定用於呼叫直接方法及更新裝置對應項 (twin) 屬性的作業</span><span class="sxs-lookup"><span data-stu-id="d76e1-141">Schedule jobs for calling a direct method and updating a device twin's properties</span></span>
<span data-ttu-id="d76e1-142">在本節中，您建立 Node.js 主控台應用程式起始遠端**lockDoor**裝置上使用直接方法，並更新 hello 裝置兩個的屬性。</span><span class="sxs-lookup"><span data-stu-id="d76e1-142">In this section, you create a Node.js console app that initiates a remote **lockDoor** on a device using a direct method and update hello device twin's properties.</span></span>

1. <span data-ttu-id="d76e1-143">建立名為 **scheduleJobService** 的新空白資料夾。</span><span class="sxs-lookup"><span data-stu-id="d76e1-143">Create a new empty folder called **scheduleJobService**.</span></span>  <span data-ttu-id="d76e1-144">在 hello **scheduleJobService**資料夾中，建立使用下列命令，在您的命令提示字元的 hello package.json 檔案。</span><span class="sxs-lookup"><span data-stu-id="d76e1-144">In hello **scheduleJobService** folder, create a package.json file using hello following command at your command prompt.</span></span>  <span data-ttu-id="d76e1-145">接受所有的 hello 預設值：</span><span class="sxs-lookup"><span data-stu-id="d76e1-145">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="d76e1-146">在您的命令提示字元中 hello **scheduleJobService**資料夾中，執行下列命令 tooinstall hello hello **azure iot 中樞**裝置 SDK 封裝和**azure-iot-裝置-mqtt**封裝：</span><span class="sxs-lookup"><span data-stu-id="d76e1-146">At your command prompt in hello **scheduleJobService** folder, run hello following command tooinstall hello **azure-iothub** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iothub uuid --save
    ```
3. <span data-ttu-id="d76e1-147">使用文字編輯器中，建立新**scheduleJobService.js**檔案在 hello **scheduleJobService**資料夾。</span><span class="sxs-lookup"><span data-stu-id="d76e1-147">Using a text editor, create a new **scheduleJobService.js** file in hello **scheduleJobService** folder.</span></span>
4. <span data-ttu-id="d76e1-148">新增 hello 下列的 '需要' 陳述式在 hello 開頭的 hello **dmpatterns_gscheduleJobServiceetstarted_service.js**檔案：</span><span class="sxs-lookup"><span data-stu-id="d76e1-148">Add hello following 'require' statements at hello start of hello **dmpatterns_gscheduleJobServiceetstarted_service.js** file:</span></span>
   
    ```
    'use strict';
   
    var uuid = require('uuid');
    var JobClient = require('azure-iothub').JobClient;
    ```
5. <span data-ttu-id="d76e1-149">新增 hello 下列變數宣告，並取代 hello 預留位置值：</span><span class="sxs-lookup"><span data-stu-id="d76e1-149">Add hello following variable declarations and replace hello placeholder values:</span></span>
   
    ```
    var connectionString = '{iothubconnectionstring}';
    var queryCondition = "deviceId IN ['myDeviceId']";
    var startTime = new Date();
    var maxExecutionTimeInSeconds =  3600;
    var jobClient = JobClient.fromConnectionString(connectionString);
    ```
6. <span data-ttu-id="d76e1-150">加入下列函式，將會使用的 toomonitor hello hello 工作執行的 hello:</span><span class="sxs-lookup"><span data-stu-id="d76e1-150">Add hello following function that will be used toomonitor hello execution of hello job:</span></span>
   
    ```
    function monitorJob (jobId, callback) {
        var jobMonitorInterval = setInterval(function() {
            jobClient.getJob(jobId, function(err, result) {
            if (err) {
                console.error('Could not get job status: ' + err.message);
            } else {
                console.log('Job: ' + jobId + ' - status: ' + result.status);
                if (result.status === 'completed' || result.status === 'failed' || result.status === 'cancelled') {
                clearInterval(jobMonitorInterval);
                callback(null, result);
                }
            }
            });
        }, 5000);
    }
    ```
7. <span data-ttu-id="d76e1-151">加入下列程式碼呼叫 hello 裝置方法 tooschedule hello 作業 hello:</span><span class="sxs-lookup"><span data-stu-id="d76e1-151">Add hello following code tooschedule hello job that calls hello device method:</span></span>
   
    ```
    var methodParams = {
        methodName: 'lockDoor',
        payload: null,
        responseTimeoutInSeconds: 15 // Timeout after 15 seconds if device is unable tooprocess method
    };
   
    var methodJobId = uuid.v4();
    console.log('scheduling Device Method job with id: ' + methodJobId);
    jobClient.scheduleDeviceMethod(methodJobId,
                                queryCondition,
                                methodParams,
                                startTime,
                                maxExecutionTimeInSeconds,
                                function(err) {
        if (err) {
            console.error('Could not schedule device method job: ' + err.message);
        } else {
            monitorJob(methodJobId, function(err, result) {
                if (err) {
                    console.error('Could not monitor device method job: ' + err.message);
                } else {
                    console.log(JSON.stringify(result, null, 2));
                }
            });
        }
    });
    ```
8. <span data-ttu-id="d76e1-152">加入下列程式碼 tooschedule hello 作業 tooupdate hello 裝置兩個 hello:</span><span class="sxs-lookup"><span data-stu-id="d76e1-152">Add hello following code tooschedule hello job tooupdate hello device twin:</span></span>
   
    ```
    var twinPatch = {
        etag: '*',
        desired: {
            building: '43',
            floor: 3
        }
    };
   
    var twinJobId = uuid.v4();
   
    console.log('scheduling Twin Update job with id: ' + twinJobId);
    jobClient.scheduleTwinUpdate(twinJobId,
                                queryCondition,
                                twinPatch,
                                startTime,
                                maxExecutionTimeInSeconds,
                                function(err) {
        if (err) {
            console.error('Could not schedule twin update job: ' + err.message);
        } else {
            monitorJob(twinJobId, function(err, result) {
                if (err) {
                    console.error('Could not monitor twin update job: ' + err.message);
                } else {
                    console.log(JSON.stringify(result, null, 2));
                }
            });
        }
    });
    ```
9. <span data-ttu-id="d76e1-153">儲存並關閉 hello **scheduleJobService.js**檔案。</span><span class="sxs-lookup"><span data-stu-id="d76e1-153">Save and close hello **scheduleJobService.js** file.</span></span>

## <a name="run-hello-applications"></a><span data-ttu-id="d76e1-154">執行 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="d76e1-154">Run hello applications</span></span>
<span data-ttu-id="d76e1-155">現在您已經準備就緒 toorun hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d76e1-155">You are now ready toorun hello applications.</span></span>

1. <span data-ttu-id="d76e1-156">在 hello 命令提示字元中 hello **simDevice**資料夾中，執行下列命令 toobegin 接聽 hello 重新開機直接方法 hello。</span><span class="sxs-lookup"><span data-stu-id="d76e1-156">At hello command prompt in hello **simDevice** folder, run hello following command toobegin listening for hello reboot direct method.</span></span>
   
    ```
    node simDevice.js
    ```
2. <span data-ttu-id="d76e1-157">在 hello 命令提示字元中 hello **scheduleJobService**資料夾中，執行下列命令 tootrigger hello 作業 toolock hello 門和更新 hello 兩個 hello</span><span class="sxs-lookup"><span data-stu-id="d76e1-157">At hello command prompt in hello **scheduleJobService** folder, run hello following command tootrigger hello jobs toolock hello door and update hello twin</span></span>
   
    ```
    node scheduleJobService.js
    ```
3. <span data-ttu-id="d76e1-158">您會看到 hello 裝置回應 toohello 直接方法 hello 主控台中。</span><span class="sxs-lookup"><span data-stu-id="d76e1-158">You see hello device response toohello direct method in hello console.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d76e1-159">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d76e1-159">Next steps</span></span>
<span data-ttu-id="d76e1-160">在此教學課程中，您可以使用作業 tooschedule 直接方法 tooa 裝置和 hello 更新的 hello 裝置兩個的屬性。</span><span class="sxs-lookup"><span data-stu-id="d76e1-160">In this tutorial, you used a job tooschedule a direct method tooa device and hello update of hello device twin's properties.</span></span>

<span data-ttu-id="d76e1-161">toocontinue 開始使用 IoT 中樞與裝置管理模式，例如遠端透過 hello 空中韌體更新，請參閱：</span><span class="sxs-lookup"><span data-stu-id="d76e1-161">toocontinue getting started with IoT Hub and device management patterns such as remote over hello air firmware update, see:</span></span>

<span data-ttu-id="d76e1-162">[教學課程： 如何 toodo 韌體更新][lnk-fwupdate]</span><span class="sxs-lookup"><span data-stu-id="d76e1-162">[Tutorial: How toodo a firmware update][lnk-fwupdate]</span></span>

<span data-ttu-id="d76e1-163">請參閱 < 開始使用 IoT 中樞 toocontinue[開始使用 Azure IoT 邊緣][lnk-iot-edge]。</span><span class="sxs-lookup"><span data-stu-id="d76e1-163">toocontinue getting started with IoT Hub, see [Getting started with Azure IoT Edge][lnk-iot-edge].</span></span>

[lnk-get-started-twin]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-props]: iot-hub-node-node-twin-how-to-configure.md
[lnk-c2d-methods]: iot-hub-node-node-direct-methods.md
[lnk-dev-methods]: iot-hub-devguide-direct-methods.md
[lnk-fwupdate]: iot-hub-node-node-firmware-update.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
