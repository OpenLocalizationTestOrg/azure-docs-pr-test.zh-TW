---
title: "aaaUse Azure IoT Hub 裝置的兩個屬性 （節點） |Microsoft 文件"
description: "如何 toouse Azure IoT Hub 裝置雙 tooconfigure 裝置。 使用 hello Azure IoT Sdk for Node.js tooimplement 模擬的裝置應用程式和服務應用程式，以修改使用裝置的兩個裝置設定。"
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: d0bcec50-26e6-40f0-8096-733b2f3071ec
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/13/2016
ms.author: elioda
ms.openlocfilehash: 7ebfe2dfa0876bf04fdbaceae55db76456523e8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-desired-properties-tooconfigure-devices-node"></a><span data-ttu-id="ddb1d-104">使用所需屬性 tooconfigure 裝置 （節點）</span><span class="sxs-lookup"><span data-stu-id="ddb1d-104">Use desired properties tooconfigure devices (Node)</span></span>
[!INCLUDE [iot-hub-selector-twin-how-to-configure](../../includes/iot-hub-selector-twin-how-to-configure.md)]

<span data-ttu-id="ddb1d-105">在本教學課程的 hello 結束時，您將擁有兩個 Node.js 主控台應用程式：</span><span class="sxs-lookup"><span data-stu-id="ddb1d-105">At hello end of this tutorial, you will have two Node.js console apps:</span></span>

* <span data-ttu-id="ddb1d-106">**SimulateDeviceConfiguration.js**，模擬的裝置應用程式等候的所需的組態更新，並報告 hello 模擬的組態更新程序的狀態。</span><span class="sxs-lookup"><span data-stu-id="ddb1d-106">**SimulateDeviceConfiguration.js**, a simulated device app that waits for a desired configuration update and reports hello status of a simulated configuration update process.</span></span>
* <span data-ttu-id="ddb1d-107">**SetDesiredConfigurationAndQuery.js**、 設定 hello Node.js 後端應用程式預期在裝置上的設定和查詢 hello 組態更新程序。</span><span class="sxs-lookup"><span data-stu-id="ddb1d-107">**SetDesiredConfigurationAndQuery.js**, a Node.js back-end app, which sets hello desired configuration on a device and queries hello configuration update process.</span></span>

> [!NOTE]
> <span data-ttu-id="ddb1d-108">hello 文章[Azure IoT Sdk] [ lnk-hub-sdks]提供 hello Azure IoT Sdk 的相關資訊，您可以使用 toobuild 裝置與後端應用程式。</span><span class="sxs-lookup"><span data-stu-id="ddb1d-108">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="ddb1d-109">toocomplete 需要 hello 下列本教學課程：</span><span class="sxs-lookup"><span data-stu-id="ddb1d-109">toocomplete this tutorial you need hello following:</span></span>

* <span data-ttu-id="ddb1d-110">Node.js 0.10.x 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="ddb1d-110">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="ddb1d-111">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="ddb1d-111">An active Azure account.</span></span> <span data-ttu-id="ddb1d-112">(如果您沒有帳戶，只需要幾分鐘的時間就可以建立[免費帳戶][lnk-free-trial]。)</span><span class="sxs-lookup"><span data-stu-id="ddb1d-112">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

<span data-ttu-id="ddb1d-113">如果您遵循 hello[開始使用裝置雙][ lnk-twin-tutorial]教學課程中，您已經有 IoT 中樞和裝置身分識別稱為**myDeviceId**; 您可以略過 toohello [建立 hello 模擬的裝置應用程式][ lnk-how-to-configure-createapp] > 一節。</span><span class="sxs-lookup"><span data-stu-id="ddb1d-113">If you followed hello [Get started with device twins][lnk-twin-tutorial] tutorial, you already have an IoT hub and a device identity called **myDeviceId**; and you can skip toohello [Create hello simulated device app][lnk-how-to-configure-createapp] section.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-hello-simulated-device-app"></a><span data-ttu-id="ddb1d-114">建立 hello 模擬的裝置應用程式</span><span class="sxs-lookup"><span data-stu-id="ddb1d-114">Create hello simulated device app</span></span>
<span data-ttu-id="ddb1d-115">在本節中，您建立 Node.js 主控台應用程式連接成 tooyour 中樞**myDeviceId**等候所需的組態更新，然後報告 hello 模擬的組態更新程序中的 更新。</span><span class="sxs-lookup"><span data-stu-id="ddb1d-115">In this section, you create a Node.js console app that connects tooyour hub as **myDeviceId**, waits for a desired configuration update and then reports updates on hello simulated configuration update process.</span></span>

1. <span data-ttu-id="ddb1d-116">建立稱為 **simulatedeviceconfiguration** 的新空白資料夾。</span><span class="sxs-lookup"><span data-stu-id="ddb1d-116">Create a new empty folder called **simulatedeviceconfiguration**.</span></span> <span data-ttu-id="ddb1d-117">在 hello **simulatedeviceconfiguration**資料夾中，建立新的 package.json 檔案使用下列命令，在您的命令提示字元的 hello。</span><span class="sxs-lookup"><span data-stu-id="ddb1d-117">In hello **simulatedeviceconfiguration** folder, create a new package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="ddb1d-118">接受所有的 hello 預設值：</span><span class="sxs-lookup"><span data-stu-id="ddb1d-118">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="ddb1d-119">在您的命令提示字元中 hello **simulatedeviceconfiguration**資料夾中，執行下列命令 tooinstall hello hello **azure iot 裝置**，和**azure-iot-裝置-mqtt**封裝：</span><span class="sxs-lookup"><span data-stu-id="ddb1d-119">At your command prompt in hello **simulatedeviceconfiguration** folder, run hello following command tooinstall hello **azure-iot-device**, and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="ddb1d-120">使用文字編輯器中，建立新**SimulateDeviceConfiguration.js**檔案在 hello **simulatedeviceconfiguration**資料夾。</span><span class="sxs-lookup"><span data-stu-id="ddb1d-120">Using a text editor, create a new **SimulateDeviceConfiguration.js** file in hello **simulatedeviceconfiguration** folder.</span></span>
4. <span data-ttu-id="ddb1d-121">新增下列程式碼 toohello hello **SimulateDeviceConfiguration.js**檔案，並以取代 hello **{裝置連接字串}**預留位置 hello 裝置連接字串複製時您建立 hello **myDeviceId**裝置身分識別：</span><span class="sxs-lookup"><span data-stu-id="ddb1d-121">Add hello following code toohello **SimulateDeviceConfiguration.js** file, and substitute hello **{device connection string}** placeholder with hello device connection string you copied when you created hello **myDeviceId** device identity:</span></span>
   
        'use strict';
        var Client = require('azure-iot-device').Client;
        var Protocol = require('azure-iot-device-mqtt').Mqtt;
   
        var connectionString = '{device connection string}';
        var client = Client.fromConnectionString(connectionString, Protocol);
   
        client.open(function(err) {
            if (err) {
                console.error('could not open IotHub client');
            } else {
                client.getTwin(function(err, twin) {
                    if (err) {
                        console.error('could not get twin');
                    } else {
                        console.log('retrieved device twin');
                        twin.properties.reported.telemetryConfig = {
                            configId: "0",
                            sendFrequency: "24h"
                        }
                        twin.on('properties.desired', function(desiredChange) {
                            console.log("received change: "+JSON.stringify(desiredChange));
                            var currentTelemetryConfig = twin.properties.reported.telemetryConfig;
                            if (desiredChange.telemetryConfig &&desiredChange.telemetryConfig.configId !== currentTelemetryConfig.configId) {
                                initConfigChange(twin);
                            }
                        });
                    }
                });
            }
        });
   
    <span data-ttu-id="ddb1d-122">hello**用戶端**物件會公開與 hello 裝置從裝置雙所有 hello 方法 toointeract 必要。</span><span class="sxs-lookup"><span data-stu-id="ddb1d-122">hello **Client** object exposes all hello methods required toointeract with device twins from hello device.</span></span> <span data-ttu-id="ddb1d-123">hello 先前的程式碼，它會初始化 hello 之後**用戶端**物件，擷取 hello 的裝置兩個**myDeviceId**，並附加 hello 更新所需的屬性上的處理常式。</span><span class="sxs-lookup"><span data-stu-id="ddb1d-123">hello previous code, after it initializes hello **Client** object, retrieves hello device twin for **myDeviceId**, and attaches a handler for hello update on desired properties.</span></span> <span data-ttu-id="ddb1d-124">hello 處理常式驗證那里實際的設定變更要求是藉由比較 hello configIds，然後啟動 hello 組態變更的方法會叫用。</span><span class="sxs-lookup"><span data-stu-id="ddb1d-124">hello handler verifies that there is an actual configuration change request by comparing hello configIds, then invokes a method that starts hello configuration change.</span></span>
   
    <span data-ttu-id="ddb1d-125">請注意，為了簡單明瞭的 hello 起見，hello 先前的程式碼使用硬式編碼預設值為 hello 初始設定。</span><span class="sxs-lookup"><span data-stu-id="ddb1d-125">Note that for hello sake of simplicity, hello previous code uses a hard-coded default for hello inital configuration.</span></span> <span data-ttu-id="ddb1d-126">實際的應用程式可能會從本機儲存體載入該組態。</span><span class="sxs-lookup"><span data-stu-id="ddb1d-126">A real app would probably load that configuration from a local storage.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="ddb1d-127">所需的屬性變更事件永遠會發出一次在裝置連線，請確定是在 hello 變更的實際 toocheck 所需屬性然後再執行任何動作。</span><span class="sxs-lookup"><span data-stu-id="ddb1d-127">Desired property change events are always emitted once at device connection, make sure toocheck that there is an actual change in hello desired properties before performing any action.</span></span>
   > 
   > 
5. <span data-ttu-id="ddb1d-128">新增下列方法之前 hello hello`client.open()`引動過程：</span><span class="sxs-lookup"><span data-stu-id="ddb1d-128">Add hello following methods before hello `client.open()` invocation:</span></span>
   
        var initConfigChange = function(twin) {
            var currentTelemetryConfig = twin.properties.reported.telemetryConfig;
            currentTelemetryConfig.pendingConfig = twin.properties.desired.telemetryConfig;
            currentTelemetryConfig.status = "Pending";
   
            var patch = {
            telemetryConfig: currentTelemetryConfig
            };
            twin.properties.reported.update(patch, function(err) {
                if (err) {
                    console.log('Could not report properties');
                } else {
                    console.log('Reported pending config change: ' + JSON.stringify(patch));
                    setTimeout(function() {completeConfigChange(twin);}, 60000);
                }
            });
        }
   
        var completeConfigChange =  function(twin) {
            var currentTelemetryConfig = twin.properties.reported.telemetryConfig;
            currentTelemetryConfig.configId = currentTelemetryConfig.pendingConfig.configId;
            currentTelemetryConfig.sendFrequency = currentTelemetryConfig.pendingConfig.sendFrequency;
            currentTelemetryConfig.status = "Success";
            delete currentTelemetryConfig.pendingConfig;
   
            var patch = {
                telemetryConfig: currentTelemetryConfig
            };
            patch.telemetryConfig.pendingConfig = null;
   
            twin.properties.reported.update(patch, function(err) {
                if (err) {
                    console.error('Error reporting properties: ' + err);
                } else {
                    console.log('Reported completed config change: ' + JSON.stringify(patch));
                }
            });
        };
   
    <span data-ttu-id="ddb1d-129">hello **initConfigChange**方法會更新與 hello 設定更新要求 hello 本機裝置兩個物件所報告的屬性和設定太 hello 狀態**暫止**，然後更新 hello 裝置hello 服務上的兩個。</span><span class="sxs-lookup"><span data-stu-id="ddb1d-129">hello **initConfigChange** method updates reported properties on hello local device twin object with hello configuration update request and sets hello status too**Pending**, then updates hello device twin on hello service.</span></span> <span data-ttu-id="ddb1d-130">已成功更新之後 hello 裝置兩個，它會模擬長時間執行的處理程序會終止在 hello 執行**completeConfigChange**。</span><span class="sxs-lookup"><span data-stu-id="ddb1d-130">After successfully updating hello device twin, it simulates a long running process that terminates in hello execution of **completeConfigChange**.</span></span> <span data-ttu-id="ddb1d-131">此方法更新 hello 本機裝置兩個的報告屬性設定 hello 狀態太**成功**和移除 hello **pendingConfig**物件。</span><span class="sxs-lookup"><span data-stu-id="ddb1d-131">This method updates hello local device twin's reported properties setting hello status too**Success** and removing hello **pendingConfig** object.</span></span> <span data-ttu-id="ddb1d-132">然後，它會更新 hello 裝置的兩個 hello 服務上。</span><span class="sxs-lookup"><span data-stu-id="ddb1d-132">It then updates hello device twin on hello service.</span></span>
   
    <span data-ttu-id="ddb1d-133">請注意，toosave 頻寬報告內容更新時所指定 hello 屬性 toobe 修改 (名為**修補程式**hello 上述程式碼中)，而不是取代 hello 整份文件。</span><span class="sxs-lookup"><span data-stu-id="ddb1d-133">Note that, toosave bandwidth, reported properties are updated by specifying only hello properties toobe modified (named **patch** in hello above code), instead of replacing hello whole document.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="ddb1d-134">本教學課程不會模擬並行組態更新的任何行為。</span><span class="sxs-lookup"><span data-stu-id="ddb1d-134">This tutorial does not simulate any behavior for concurrent configuration updates.</span></span> <span data-ttu-id="ddb1d-135">某些組態更新處理程序可能會無法 tooaccommodate 變更目標組態的 hello 更新執行時，其他人可能 tooqueue，以及其他人無法拒絕它們與錯誤狀況。</span><span class="sxs-lookup"><span data-stu-id="ddb1d-135">Some configuration update processes might be able tooaccommodate changes of target configuration while hello update is running, others might have tooqueue them, and others could reject them with an error condition.</span></span> <span data-ttu-id="ddb1d-136">請確定 tooconsider hello 特定組態程序中，所要的行為，並加入初始化 hello 組態變更之前的 hello 適當的邏輯。</span><span class="sxs-lookup"><span data-stu-id="ddb1d-136">Make sure tooconsider hello desired behavior for your specific configuration process, and add hello appropriate logic before initiating hello configuration change.</span></span>
   > 
   > 
6. <span data-ttu-id="ddb1d-137">執行 hello 裝置應用程式：</span><span class="sxs-lookup"><span data-stu-id="ddb1d-137">Run hello device app:</span></span>
   
        node SimulateDeviceConfiguration.js
   
    <span data-ttu-id="ddb1d-138">您應該會看到 hello 訊息`retrieved device twin`。</span><span class="sxs-lookup"><span data-stu-id="ddb1d-138">You should see hello message `retrieved device twin`.</span></span> <span data-ttu-id="ddb1d-139">保留 hello 應用程式執行。</span><span class="sxs-lookup"><span data-stu-id="ddb1d-139">Keep hello app running.</span></span>

## <a name="create-hello-service-app"></a><span data-ttu-id="ddb1d-140">建立 hello 服務應用程式</span><span class="sxs-lookup"><span data-stu-id="ddb1d-140">Create hello service app</span></span>
<span data-ttu-id="ddb1d-141">在本節中，您將建立 Node.js 主控台應用程式的更新 hello*所需屬性*上 hello 與相關聯的裝置兩個**myDeviceId**與新的遙測組態物件。</span><span class="sxs-lookup"><span data-stu-id="ddb1d-141">In this section, you will create a Node.js console app that updates hello *desired properties* on hello device twin associated with **myDeviceId** with a new telemetry configuration object.</span></span> <span data-ttu-id="ddb1d-142">接著會查詢儲存在 hello IoT 中樞中的 hello 裝置雙，並顯示 hello 差異 hello 想要與報告的 hello 裝置組態。</span><span class="sxs-lookup"><span data-stu-id="ddb1d-142">It then queries hello device twins stored in hello IoT hub and shows hello difference between hello desired and reported configurations of hello device.</span></span>

1. <span data-ttu-id="ddb1d-143">建立稱為 **setdesiredandqueryapp** 的新空白資料夾。</span><span class="sxs-lookup"><span data-stu-id="ddb1d-143">Create a new empty folder called **setdesiredandqueryapp**.</span></span> <span data-ttu-id="ddb1d-144">在 hello **setdesiredandqueryapp**資料夾中，建立新的 package.json 檔案使用下列命令，在您的命令提示字元的 hello。</span><span class="sxs-lookup"><span data-stu-id="ddb1d-144">In hello **setdesiredandqueryapp** folder, create a new package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="ddb1d-145">接受所有的 hello 預設值：</span><span class="sxs-lookup"><span data-stu-id="ddb1d-145">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="ddb1d-146">在您的命令提示字元中 hello **setdesiredandqueryapp**資料夾中，執行下列命令 tooinstall hello hello **azure iot 中樞**封裝：</span><span class="sxs-lookup"><span data-stu-id="ddb1d-146">At your command prompt in hello **setdesiredandqueryapp** folder, run hello following command tooinstall hello **azure-iothub** package:</span></span>
   
    ```
    npm install azure-iothub node-uuid --save
    ```
3. <span data-ttu-id="ddb1d-147">使用文字編輯器中，建立新**SetDesiredAndQuery.js**檔案在 hello **addtagsandqueryapp**資料夾。</span><span class="sxs-lookup"><span data-stu-id="ddb1d-147">Using a text editor, create a new **SetDesiredAndQuery.js** file in hello **addtagsandqueryapp** folder.</span></span>
4. <span data-ttu-id="ddb1d-148">新增下列程式碼 toohello hello **SetDesiredAndQuery.js**檔案，並以取代 hello **{iot 中樞連接字串}**預留位置 hello 您複製當您建立中樞的 IoT 中樞連接字串:</span><span class="sxs-lookup"><span data-stu-id="ddb1d-148">Add hello following code toohello **SetDesiredAndQuery.js** file, and substitute hello **{iot hub connection string}** placeholder with hello IoT Hub connection string you copied when you created your hub:</span></span>
   
        'use strict';
        var iothub = require('azure-iothub');
        var uuid = require('node-uuid');
        var connectionString = '{iot hub connection string}';
        var registry = iothub.Registry.fromConnectionString(connectionString);
   
        registry.getTwin('myDeviceId', function(err, twin){
            if (err) {
                console.error(err.constructor.name + ': ' + err.message);
            } else {
                var newConfigId = uuid.v4();
                var newFrequency = process.argv[2] || "5m";
                var patch = {
                    properties: {
                        desired: {
                            telemetryConfig: {
                                configId: newConfigId,
                                sendFrequency: newFrequency
                            }
                        }
                    }
                }
                twin.update(patch, function(err) {
                    if (err) {
                        console.error('Could not update twin: ' + err.constructor.name + ': ' + err.message);
                    } else {
                        console.log(twin.deviceId + ' twin updated successfully');
                    }
                });
                setInterval(queryTwins, 10000);
            }
        });

    <span data-ttu-id="ddb1d-149">hello**登錄**物件會公開與裝置雙 hello 服務從所有 hello 方法 toointeract 必要。</span><span class="sxs-lookup"><span data-stu-id="ddb1d-149">hello **Registry** object exposes all hello methods required toointeract with device twins from hello service.</span></span> <span data-ttu-id="ddb1d-150">hello 先前的程式碼，它會初始化 hello 之後**登錄**物件，擷取 hello 的裝置兩個**myDeviceId**，並更新其所需的屬性，以新的遙測組態物件。</span><span class="sxs-lookup"><span data-stu-id="ddb1d-150">hello previous code, after it initializes hello **Registry** object, retrieves hello device twin for **myDeviceId**, and updates its desired properties with a new telemetry configuration object.</span></span> <span data-ttu-id="ddb1d-151">在這之後，它會呼叫 hello **queryTwins**函式事件 10 秒。</span><span class="sxs-lookup"><span data-stu-id="ddb1d-151">After that, it calls hello **queryTwins** function event 10 seconds.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="ddb1d-152">為了便於說明，此應用程式每 10 秒查詢一次 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="ddb1d-152">This application queries IoT Hub every 10 seconds for illustrative purposes.</span></span> <span data-ttu-id="ddb1d-153">使用跨許多裝置和非 toodetect 變更查詢 toogenerate 面對使用者的報表。</span><span class="sxs-lookup"><span data-stu-id="ddb1d-153">Use queries toogenerate user-facing reports across many devices, and not toodetect changes.</span></span> <span data-ttu-id="ddb1d-154">如果您的解決方案需要裝置事件的即時通知，請使用[對應項通知][lnk-twin-notifications]。</span><span class="sxs-lookup"><span data-stu-id="ddb1d-154">If your solution requires real-time notifications of device events, use [twin notifications][lnk-twin-notifications].</span></span>
    > 
    ><span data-ttu-id="ddb1d-155">.</span><span class="sxs-lookup"><span data-stu-id="ddb1d-155">.</span></span>

1. <span data-ttu-id="ddb1d-156">新增下列程式碼權限之前 hello hello`registry.getDeviceTwin()`引動過程 tooimplement hello **queryTwins**函式：</span><span class="sxs-lookup"><span data-stu-id="ddb1d-156">Add hello following code right before hello `registry.getDeviceTwin()` invocation tooimplement hello **queryTwins** function:</span></span>
   
        var queryTwins = function() {
            var query = registry.createQuery("SELECT * FROM devices WHERE deviceId = 'myDeviceId'", 100);
            query.nextAsTwin(function(err, results) {
                if (err) {
                    console.error('Failed toofetch hello results: ' + err.message);
                } else {
                    console.log();
                    results.forEach(function(twin) {
                        var desiredConfig = twin.properties.desired.telemetryConfig;
                        var reportedConfig = twin.properties.reported.telemetryConfig;
                        console.log("Config report for: " + twin.deviceId);
                        console.log("Desired: ");
                        console.log(JSON.stringify(desiredConfig, null, 2));
                        console.log("Reported: ");
                        console.log(JSON.stringify(reportedConfig, null, 2));
                    });
                }
            });
        };
   
    <span data-ttu-id="ddb1d-157">hello 先前的程式碼查詢 hello 裝置雙 hello IoT 中樞中儲存和列印 hello 想要與回報遙測組態。</span><span class="sxs-lookup"><span data-stu-id="ddb1d-157">hello previous code queries hello device twins stored in hello IoT hub and prints hello desired and reported telemetry configurations.</span></span> <span data-ttu-id="ddb1d-158">請參閱 toohello [IoT 中樞的查詢語言][ lnk-query] toolearn toogenerate 豐富報告的方式，跨所有裝置。</span><span class="sxs-lookup"><span data-stu-id="ddb1d-158">Refer toohello [IoT Hub query language][lnk-query] toolearn how toogenerate rich reports across all your devices.</span></span>
2. <span data-ttu-id="ddb1d-159">與**SimulateDeviceConfiguration.js**執行，請執行與 hello 應用程式：</span><span class="sxs-lookup"><span data-stu-id="ddb1d-159">With **SimulateDeviceConfiguration.js** running, run hello application with:</span></span>
   
        node SetDesiredAndQuery.js 5m
   
    <span data-ttu-id="ddb1d-160">您應該會看見 hello 報告的設定，變更從**成功**太**暫止**太**成功**再次 hello 新的作用中的傳送頻率 5 分鐘，而不是 24時數。</span><span class="sxs-lookup"><span data-stu-id="ddb1d-160">You should see hello reported configuration change from **Success** too**Pending** too**Success** again with hello new active send frequency of five minutes instead of 24 hours.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="ddb1d-161">沒有向上 tooa 分鐘 hello 裝置報告作業和 hello 查詢結果之間的延遲。</span><span class="sxs-lookup"><span data-stu-id="ddb1d-161">There is a delay of up tooa minute between hello device report operation and hello query result.</span></span> <span data-ttu-id="ddb1d-162">這是 tooenable hello 查詢在極高的小數位數的基礎結構 toowork。</span><span class="sxs-lookup"><span data-stu-id="ddb1d-162">This is tooenable hello query infrastructure toowork at very high scale.</span></span> <span data-ttu-id="ddb1d-163">tooretrieve 一致檢視的單一裝置的兩個使用 hello **getDeviceTwin**方法在 hello**登錄**類別。</span><span class="sxs-lookup"><span data-stu-id="ddb1d-163">tooretrieve consistent views of a single device twin use hello **getDeviceTwin** method in hello **Registry** class.</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="ddb1d-164">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ddb1d-164">Next steps</span></span>
<span data-ttu-id="ddb1d-165">在本教學課程中，您可以設定為所需的組態*所需屬性*從後端應用程式，並寫下的變更，並模擬報告其狀態為多步驟更新程序模擬的裝置應用程式 toodetect *報告內容*toohello 裝置兩個。</span><span class="sxs-lookup"><span data-stu-id="ddb1d-165">In this tutorial, you set a desired configuration as *desired properties* from a back-end app, and wrote a simulated device app toodetect that change and simulate a multi-step update process reporting its status as *reported properties* toohello device twin.</span></span>

<span data-ttu-id="ddb1d-166">下列資源 toolearn 如何使用 hello 至：</span><span class="sxs-lookup"><span data-stu-id="ddb1d-166">Use hello following resources toolearn how to:</span></span>

* <span data-ttu-id="ddb1d-167">從以 hello 的裝置將遙測傳送[開始使用 IoT 中樞][ lnk-iothub-getstarted]教學課程中，</span><span class="sxs-lookup"><span data-stu-id="ddb1d-167">send telemetry from devices with hello [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="ddb1d-168">排程執行，或是執行大量的裝置上的作業，請參閱 「 hello[排程和廣播的工作][ lnk-schedule-jobs]教學課程。</span><span class="sxs-lookup"><span data-stu-id="ddb1d-168">schedule or perform operations on large sets of devices see hello [Schedule and broadcast jobs][lnk-schedule-jobs] tutorial.</span></span>
* <span data-ttu-id="ddb1d-169">控制裝置以互動方式 （例如開啟風扇從使用者控制的應用程式），以 hello[使用直接的方法][ lnk-methods-tutorial]教學課程。</span><span class="sxs-lookup"><span data-stu-id="ddb1d-169">control devices interactively (such as turning on a fan from a user-controlled app), with hello [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-twin-notifications]: iot-hub-devguide-device-twins.md#back-end-operations
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-dm-overview]: iot-hub-device-management-overview.md
[lnk-twin-tutorial]: iot-hub-node-node-twin-getstarted.md
[lnk-schedule-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/
[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-iothub-getstarted]: iot-hub-node-node-getstarted.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md

[lnk-guid]: https://en.wikipedia.org/wiki/Globally_unique_identifier

[lnk-how-to-configure-createapp]: iot-hub-node-node-twin-how-to-configure.md#create-the-simulated-device-app
