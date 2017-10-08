---
title: "aaaGet 開始使用 Azure IoT 中樞 （節點） |Microsoft 文件"
description: "了解如何 toosend 裝置到雲端訊息 tooAzure 使用 IoT Sdk for Node.js 的 IoT 中樞。 建立模擬的裝置和服務應用程式 tooregister 您的裝置、 傳送訊息，以及從 IoT 中樞讀取訊息。"
services: iot-hub
documentationcenter: nodejs
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 56618522-9a31-42c6-94bf-55e2233b39ac
ms.service: iot-hub
ms.devlang: javascript
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/22/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d0747895365f2359a9c38ea1e85a5881d6efec0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-simulated-device-tooyour-iot-hub-using-node"></a><span data-ttu-id="4776c-104">連接使用節點您模擬的裝置 tooyour IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="4776c-104">Connect your simulated device tooyour IoT hub using Node</span></span>
[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

<span data-ttu-id="4776c-105">在本教學課程的 hello 最後，您有三個 Node.js 主控台應用程式：</span><span class="sxs-lookup"><span data-stu-id="4776c-105">At hello end of this tutorial, you have three Node.js console apps:</span></span>

* <span data-ttu-id="4776c-106">**CreateDeviceIdentity.js**，這樣就可以建立裝置身分識別，以及相關聯的安全性金鑰 tooconnect 應用程式模擬的裝置。</span><span class="sxs-lookup"><span data-stu-id="4776c-106">**CreateDeviceIdentity.js**, which creates a device identity and associated security key tooconnect your simulated device app.</span></span>
* <span data-ttu-id="4776c-107">**ReadDeviceToCloudMessages.js**，其中顯示模擬的裝置之應用程式所傳送的 hello 遙測。</span><span class="sxs-lookup"><span data-stu-id="4776c-107">**ReadDeviceToCloudMessages.js**, which displays hello telemetry sent by your simulated device app.</span></span>
* <span data-ttu-id="4776c-108">**SimulatedDevice.js**，這與 hello 稍早建立的裝置身分識別連接 tooyour IoT 中樞，並傳送遙測訊息每個第二個使用 hello MQTT 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="4776c-108">**SimulatedDevice.js**, which connects tooyour IoT hub with hello device identity created earlier, and sends a telemetry message every second using hello MQTT protocol.</span></span>

> [!NOTE]
> <span data-ttu-id="4776c-109">hello 文章[Azure IoT Sdk] [ lnk-hub-sdks]提供 hello Azure IoT Sdk 的相關資訊，您可以使用 toobuild 這兩個應用程式 toorun 裝置和您的方案後端上。</span><span class="sxs-lookup"><span data-stu-id="4776c-109">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both applications toorun on devices and your solution back end.</span></span>
> 
> 

<span data-ttu-id="4776c-110">toocomplete 本教學課程中，您需要遵循的 hello:</span><span class="sxs-lookup"><span data-stu-id="4776c-110">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="4776c-111">Node.js 0.10.x 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="4776c-111">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="4776c-112">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="4776c-112">An active Azure account.</span></span> <span data-ttu-id="4776c-113">(如果您沒有帳戶，只需要幾分鐘的時間就可以建立[免費帳戶][lnk-free-trial]。)</span><span class="sxs-lookup"><span data-stu-id="4776c-113">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

<span data-ttu-id="4776c-114">您現在已經建立 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="4776c-114">You have now created your IoT hub.</span></span> <span data-ttu-id="4776c-115">您有 hello IoT 中樞的主機名稱與 hello 您需要 toocomplete hello rest 本教學課程的 IoT 中樞連接字串。</span><span class="sxs-lookup"><span data-stu-id="4776c-115">You have hello IoT Hub host name and hello IoT Hub connection string that you need toocomplete hello rest of this tutorial.</span></span>

## <a name="create-a-device-identity"></a><span data-ttu-id="4776c-116">建立裝置識別</span><span class="sxs-lookup"><span data-stu-id="4776c-116">Create a device identity</span></span>
<span data-ttu-id="4776c-117">在本節中，您可以建立 IoT 中樞中的 hello 身分識別登錄中建立裝置身分識別的 Node.js 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="4776c-117">In this section, you create a Node.js console app that creates a device identity in hello identity registry in your IoT hub.</span></span> <span data-ttu-id="4776c-118">如果其中有傳送 hello 身分識別登錄中的裝置只能連接 tooIoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="4776c-118">A device can only connect tooIoT hub if it has an entry in hello identity registry.</span></span> <span data-ttu-id="4776c-119">如需詳細資訊，請參閱 hello**身分識別登錄**區段 hello [IoT 中樞開發人員指南][lnk-devguide-identity]。</span><span class="sxs-lookup"><span data-stu-id="4776c-119">For more information, see hello **Identity Registry** section of hello [IoT Hub developer guide][lnk-devguide-identity].</span></span> <span data-ttu-id="4776c-120">當您執行此主控台應用程式時，它會產生唯一的裝置識別碼，並傳送至雲端的裝置時，您的裝置，可以使用 tooidentify 本身的索引鍵郵件 tooIoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="4776c-120">When you run this console app, it generates a unique device ID and key that your device can use tooidentify itself when it sends device-to-cloud messages tooIoT Hub.</span></span>

1. <span data-ttu-id="4776c-121">建立稱為 **createdeviceidentity**的新的空資料夾。</span><span class="sxs-lookup"><span data-stu-id="4776c-121">Create a new empty folder called **createdeviceidentity**.</span></span> <span data-ttu-id="4776c-122">在 hello **createdeviceidentity**資料夾中，建立使用下列命令，在您的命令提示字元的 hello package.json 檔案。</span><span class="sxs-lookup"><span data-stu-id="4776c-122">In hello **createdeviceidentity** folder, create a package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="4776c-123">接受所有的 hello 預設值：</span><span class="sxs-lookup"><span data-stu-id="4776c-123">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="4776c-124">在您的命令提示字元中 hello **createdeviceidentity**資料夾中，執行下列命令 tooinstall hello hello **azure iot 中樞**服務 SDK 封裝：</span><span class="sxs-lookup"><span data-stu-id="4776c-124">At your command prompt in hello **createdeviceidentity** folder, run hello following command tooinstall hello **azure-iothub** Service SDK package:</span></span>
   
    ```
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="4776c-125">使用文字編輯器中，建立**CreateDeviceIdentity.js**檔案在 hello **createdeviceidentity**資料夾。</span><span class="sxs-lookup"><span data-stu-id="4776c-125">Using a text editor, create a **CreateDeviceIdentity.js** file in hello **createdeviceidentity** folder.</span></span>
4. <span data-ttu-id="4776c-126">新增下列 hello `require` hello 的 hello 開頭的陳述式**CreateDeviceIdentity.js**檔案：</span><span class="sxs-lookup"><span data-stu-id="4776c-126">Add hello following `require` statement at hello start of hello **CreateDeviceIdentity.js** file:</span></span>
   
    ```
    'use strict';
   
    var iothub = require('azure-iothub');
    ```
5. <span data-ttu-id="4776c-127">新增下列程式碼 toohello hello **CreateDeviceIdentity.js**檔案，然後以 hello hello 中樞 hello 前一節中您建立 IoT 中樞連接字串取代 hello 預留位置的值：</span><span class="sxs-lookup"><span data-stu-id="4776c-127">Add hello following code toohello **CreateDeviceIdentity.js** file and replace hello placeholder value with hello IoT Hub connection string for hello hub you created in hello previous section:</span></span> 
   
    ```
    var connectionString = '{iothub connection string}';
   
    var registry = iothub.Registry.fromConnectionString(connectionString);
    ```
6. <span data-ttu-id="4776c-128">新增下列程式碼 toocreate IoT 中樞中的 hello 身分識別登錄中的裝置定義 hello。</span><span class="sxs-lookup"><span data-stu-id="4776c-128">Add hello following code toocreate a device definition in hello identity registry in your IoT hub.</span></span> <span data-ttu-id="4776c-129">此程式碼會建立裝置如果 hello 裝置識別碼不存在於 hello 身分識別登錄，否則它會傳回 hello 現有裝置 hello 索引鍵：</span><span class="sxs-lookup"><span data-stu-id="4776c-129">This code creates a device if hello device ID does not exist in hello identity registry, otherwise it returns hello key of hello existing device:</span></span>
   
    ```
    var device = {
      deviceId: 'myFirstNodeDevice'
    }
    registry.create(device, function(err, deviceInfo, res) {
      if (err) {
        registry.get(device.deviceId, printDeviceInfo);
      }
      if (deviceInfo) {
        printDeviceInfo(err, deviceInfo, res)
      }
    });
   
    function printDeviceInfo(err, deviceInfo, res) {
      if (deviceInfo) {
        console.log('Device ID: ' + deviceInfo.deviceId);
        console.log('Device key: ' + deviceInfo.authentication.symmetricKey.primaryKey);
      }
    }
    ```
   [!INCLUDE [iot-hub-pii-note-naming-device](../../includes/iot-hub-pii-note-naming-device.md)]

7. <span data-ttu-id="4776c-130">儲存並關閉 **CreateDeviceIdentity.js** 檔案。</span><span class="sxs-lookup"><span data-stu-id="4776c-130">Save and close **CreateDeviceIdentity.js** file.</span></span>
8. <span data-ttu-id="4776c-131">toorun hello **createdeviceidentity**應用程式中，執行下列命令在 hello hello createdeviceidentity 資料夾中的命令提示字元的 hello:</span><span class="sxs-lookup"><span data-stu-id="4776c-131">toorun hello **createdeviceidentity** application, execute hello following command at hello command prompt in hello createdeviceidentity folder:</span></span>
   
    ```
    node CreateDeviceIdentity.js 
    ```
9. <span data-ttu-id="4776c-132">請記下 hello**裝置識別碼**和**裝置金鑰**。</span><span class="sxs-lookup"><span data-stu-id="4776c-132">Make a note of hello **Device ID** and **Device key**.</span></span> <span data-ttu-id="4776c-133">您需要這些值稍後當您建立連線 tooIoT 中樞為裝置的應用程式。</span><span class="sxs-lookup"><span data-stu-id="4776c-133">You need these values later when you create an application that connects tooIoT Hub as a device.</span></span>

> [!NOTE]
> <span data-ttu-id="4776c-134">hello IoT 中樞身分識別登錄只會儲存裝置身分識別 tooenable 安全存取 toohello IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="4776c-134">hello IoT Hub identity registry only stores device identities tooenable secure access toohello IoT hub.</span></span> <span data-ttu-id="4776c-135">它會儲存裝置識別碼和金鑰 toouse 安全性認證以及啟用/停用旗標，您可以使用 toodisable 存取個別的裝置。</span><span class="sxs-lookup"><span data-stu-id="4776c-135">It stores device IDs and keys toouse as security credentials and an enabled/disabled flag that you can use toodisable access for an individual device.</span></span> <span data-ttu-id="4776c-136">如果您的應用程式需要 toostore 其他裝置專屬的中繼資料，它應該使用特定應用程式存放區。</span><span class="sxs-lookup"><span data-stu-id="4776c-136">If your application needs toostore other device-specific metadata, it should use an application-specific store.</span></span> <span data-ttu-id="4776c-137">如需詳細資訊，請參閱 hello [IoT 中樞開發人員指南][lnk-devguide-identity]。</span><span class="sxs-lookup"><span data-stu-id="4776c-137">For more information, see hello [IoT Hub developer guide][lnk-devguide-identity].</span></span>
> 
> 

<a id="D2C_node"></a>
## <a name="receive-device-to-cloud-messages"></a><span data-ttu-id="4776c-138">接收裝置到雲端的訊息</span><span class="sxs-lookup"><span data-stu-id="4776c-138">Receive device-to-cloud messages</span></span>
<span data-ttu-id="4776c-139">在本節中，您會建立 Node.js 主控台應用程式，以讀取來自 IoT 中樞的裝置到雲端訊息。</span><span class="sxs-lookup"><span data-stu-id="4776c-139">In this section, you create a Node.js console app that reads device-to-cloud messages from IoT Hub.</span></span> <span data-ttu-id="4776c-140">IoT 中樞公開[事件中心][lnk-event-hubs-overview]-相容的端點 tooenable 您 tooread 裝置到雲端訊息。</span><span class="sxs-lookup"><span data-stu-id="4776c-140">An IoT hub exposes an [Event Hubs][lnk-event-hubs-overview]-compatible endpoint tooenable you tooread device-to-cloud messages.</span></span> <span data-ttu-id="4776c-141">簡單 tookeep 方面，本教學課程會建立基本的讀取器不是適用於高輸送量部署。</span><span class="sxs-lookup"><span data-stu-id="4776c-141">tookeep things simple, this tutorial creates a basic reader that is not suitable for a high throughput deployment.</span></span> <span data-ttu-id="4776c-142">hello[處理裝置到雲端訊息][ lnk-process-d2c-tutorial]教學課程會示範大規模 tooprocess 裝置到雲端訊息的方式。</span><span class="sxs-lookup"><span data-stu-id="4776c-142">hello [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial shows you how tooprocess device-to-cloud messages at scale.</span></span> <span data-ttu-id="4776c-143">hello[開始使用事件中心][ lnk-eventhubs-tutorial]教學課程提供有關 tooprocess 如何從事件中心訊息和是適用的 toohello IoT 中樞事件中樞相容的端點的進一步資訊。</span><span class="sxs-lookup"><span data-stu-id="4776c-143">hello [Get Started with Event Hubs][lnk-eventhubs-tutorial] tutorial provides further information on how tooprocess messages from Event Hubs and is applicable toohello IoT Hub Event Hub-compatible endpoints.</span></span>

> [!NOTE]
> <span data-ttu-id="4776c-144">hello 一律讀取裝置到雲端訊息的事件中樞相容端點使用 hello AMQP 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="4776c-144">hello Event Hub-compatible endpoint for reading device-to-cloud messages always uses hello AMQP protocol.</span></span>
> 
> 

1. <span data-ttu-id="4776c-145">建立稱為 **readdevicetocloudmessages** 的空資料夾。</span><span class="sxs-lookup"><span data-stu-id="4776c-145">Create an empty folder called **readdevicetocloudmessages**.</span></span> <span data-ttu-id="4776c-146">在 hello **readdevicetocloudmessages**資料夾中，建立使用下列命令，在您的命令提示字元的 hello package.json 檔案。</span><span class="sxs-lookup"><span data-stu-id="4776c-146">In hello **readdevicetocloudmessages** folder, create a package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="4776c-147">接受所有的 hello 預設值：</span><span class="sxs-lookup"><span data-stu-id="4776c-147">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="4776c-148">在您的命令提示字元中 hello **readdevicetocloudmessages**資料夾中，執行下列命令 tooinstall hello hello **azure 事件中心**封裝：</span><span class="sxs-lookup"><span data-stu-id="4776c-148">At your command prompt in hello **readdevicetocloudmessages** folder, run hello following command tooinstall hello **azure-event-hubs** package:</span></span>
   
    ```
    npm install azure-event-hubs --save
    ```
3. <span data-ttu-id="4776c-149">使用文字編輯器中，建立**ReadDeviceToCloudMessages.js**檔案在 hello **readdevicetocloudmessages**資料夾。</span><span class="sxs-lookup"><span data-stu-id="4776c-149">Using a text editor, create a **ReadDeviceToCloudMessages.js** file in hello **readdevicetocloudmessages** folder.</span></span>
4. <span data-ttu-id="4776c-150">新增下列 hello`require`陳述式在 hello 開頭 hello **ReadDeviceToCloudMessages.js**檔案：</span><span class="sxs-lookup"><span data-stu-id="4776c-150">Add hello following `require` statements at hello start of hello **ReadDeviceToCloudMessages.js** file:</span></span>
   
    ```
    'use strict';
   
    var EventHubClient = require('azure-event-hubs').Client;
    ```
5. <span data-ttu-id="4776c-151">加入下列變數宣告 hello 和 hello 預留位置值取代為您的中樞的 IoT 中樞連接字串 hello:</span><span class="sxs-lookup"><span data-stu-id="4776c-151">Add hello following variable declaration and replace hello placeholder value with hello IoT Hub connection string for your hub:</span></span>
   
    ```
    var connectionString = '{iothub connection string}';
    ```
6. <span data-ttu-id="4776c-152">加入下列兩個函數，列印輸出 toohello 主控台 hello:</span><span class="sxs-lookup"><span data-stu-id="4776c-152">Add hello following two functions that print output toohello console:</span></span>
   
    ```
    var printError = function (err) {
      console.log(err.message);
    };
   
    var printMessage = function (message) {
      console.log('Message received: ');
      console.log(JSON.stringify(message.body));
      console.log('');
    };
    ```
7. <span data-ttu-id="4776c-153">新增下列程式碼 toocreate hello hello **EventHubClient**，開啟 hello 連接 tooyour IoT 中樞，並建立每個資料分割的接收器。</span><span class="sxs-lookup"><span data-stu-id="4776c-153">Add hello following code toocreate hello **EventHubClient**, open hello connection tooyour IoT Hub, and create a receiver for each partition.</span></span> <span data-ttu-id="4776c-154">建立接收者以便 hello 接收者只會讀取傳送的訊息 tooIoT 中樞之後 hello 接收者就可開始執行時，此應用程式會使用篩選器。</span><span class="sxs-lookup"><span data-stu-id="4776c-154">This application uses a filter when it creates a receiver so that hello receiver only reads messages sent tooIoT Hub after hello receiver starts running.</span></span> <span data-ttu-id="4776c-155">此篩選器是適用於測試環境，因此您會看到剛才 hello 目前的一組訊息。</span><span class="sxs-lookup"><span data-stu-id="4776c-155">This filter is useful in a test environment so you see just hello current set of messages.</span></span> <span data-ttu-id="4776c-156">在實際執行環境中，您的程式碼應該要確定在處理所有的 hello 訊息。</span><span class="sxs-lookup"><span data-stu-id="4776c-156">In a production environment, your code should make sure that it processes all hello messages.</span></span> <span data-ttu-id="4776c-157">如需詳細資訊，請參閱 hello[如何 tooprocess IoT 中樞裝置到雲端訊息][ lnk-process-d2c-tutorial]教學課程：</span><span class="sxs-lookup"><span data-stu-id="4776c-157">For more information, see hello [How tooprocess IoT Hub device-to-cloud messages][lnk-process-d2c-tutorial] tutorial:</span></span>
   
    ```
    var client = EventHubClient.fromConnectionString(connectionString);
    client.open()
        .then(client.getPartitionIds.bind(client))
        .then(function (partitionIds) {
            return partitionIds.map(function (partitionId) {
                return client.createReceiver('$Default', partitionId, { 'startAfterTime' : Date.now()}).then(function(receiver) {
                    console.log('Created partition receiver: ' + partitionId)
                    receiver.on('errorReceived', printError);
                    receiver.on('message', printMessage);
                });
            });
        })
        .catch(printError);
    ```
8. <span data-ttu-id="4776c-158">儲存並關閉 hello **ReadDeviceToCloudMessages.js**檔案。</span><span class="sxs-lookup"><span data-stu-id="4776c-158">Save and close hello **ReadDeviceToCloudMessages.js** file.</span></span>

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="4776c-159">建立模擬裝置應用程式</span><span class="sxs-lookup"><span data-stu-id="4776c-159">Create a simulated device app</span></span>
<span data-ttu-id="4776c-160">在本節中，您可以建立 Node.js 主控台應用程式，可以模擬傳送裝置到雲端訊息 tooan IoT 中樞的裝置。</span><span class="sxs-lookup"><span data-stu-id="4776c-160">In this section, you create a Node.js console app that simulates a device that sends device-to-cloud messages tooan IoT hub.</span></span>

1. <span data-ttu-id="4776c-161">建立稱為 **simulateddevice**的空資料夾。</span><span class="sxs-lookup"><span data-stu-id="4776c-161">Create an empty folder called **simulateddevice**.</span></span> <span data-ttu-id="4776c-162">在 hello **simulateddevice**資料夾中，建立使用下列命令，在您的命令提示字元的 hello package.json 檔案。</span><span class="sxs-lookup"><span data-stu-id="4776c-162">In hello **simulateddevice** folder, create a package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="4776c-163">接受所有的 hello 預設值：</span><span class="sxs-lookup"><span data-stu-id="4776c-163">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="4776c-164">在您的命令提示字元中 hello **simulateddevice**資料夾中，執行下列命令 tooinstall hello hello **azure iot 裝置**裝置 SDK 封裝和**azure-iot-裝置-mqtt**封裝：</span><span class="sxs-lookup"><span data-stu-id="4776c-164">At your command prompt in hello **simulateddevice** folder, run hello following command tooinstall hello **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="4776c-165">使用文字編輯器中，建立**SimulatedDevice.js**檔案在 hello **simulateddevice**資料夾。</span><span class="sxs-lookup"><span data-stu-id="4776c-165">Using a text editor, create a **SimulatedDevice.js** file in hello **simulateddevice** folder.</span></span>
4. <span data-ttu-id="4776c-166">新增下列 hello`require`陳述式在 hello 開頭 hello **SimulatedDevice.js**檔案：</span><span class="sxs-lookup"><span data-stu-id="4776c-166">Add hello following `require` statements at hello start of hello **SimulatedDevice.js** file:</span></span>
   
    ```
    'use strict';
   
    var clientFromConnectionString = require('azure-iot-device-mqtt').clientFromConnectionString;
    var Message = require('azure-iot-device').Message;
    ```
5. <span data-ttu-id="4776c-167">新增**connectionString**變數，並使用它 toocreate**用戶端**執行個體。</span><span class="sxs-lookup"><span data-stu-id="4776c-167">Add a **connectionString** variable and use it toocreate a **Client** instance.</span></span> <span data-ttu-id="4776c-168">取代**{youriothostname}** hello hello IoT 中樞名稱與您建立 hello*建立 IoT 中樞*> 一節。</span><span class="sxs-lookup"><span data-stu-id="4776c-168">Replace **{youriothostname}** with hello name of hello IoT hub you created hello *Create an IoT Hub* section.</span></span> <span data-ttu-id="4776c-169">取代**{yourdevicekey}** hello 裝置索引鍵值中 hello 產生*建立裝置身分識別*> 一節：</span><span class="sxs-lookup"><span data-stu-id="4776c-169">Replace **{yourdevicekey}** with hello device key value you generated in hello *Create a device identity* section:</span></span>
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId=myFirstNodeDevice;SharedAccessKey={yourdevicekey}';
   
    var client = clientFromConnectionString(connectionString);
    ```
6. <span data-ttu-id="4776c-170">新增 hello hello 應用程式中的下列函式 toodisplay 輸出：</span><span class="sxs-lookup"><span data-stu-id="4776c-170">Add hello following function toodisplay output from hello application:</span></span>
   
    ```
    function printResultFor(op) {
      return function printResult(err, res) {
        if (err) console.log(op + ' error: ' + err.toString());
        if (res) console.log(op + ' status: ' + res.constructor.name);
      };
    }
    ```
7. <span data-ttu-id="4776c-171">建立回呼，並使用 hello**依**函式 toosend 訊息 tooyour IoT 中樞每秒：</span><span class="sxs-lookup"><span data-stu-id="4776c-171">Create a callback and use hello **setInterval** function toosend a message tooyour IoT hub every second:</span></span>
   
    ```
    var connectCallback = function (err) {
      if (err) {
        console.log('Could not connect: ' + err);
      } else {
        console.log('Client connected');
   
        // Create a message and send it toohello IoT Hub every second
        setInterval(function(){
            var temperature = 20 + (Math.random() * 15);
            var humidity = 60 + (Math.random() * 20);            
            var data = JSON.stringify({ deviceId: 'myFirstNodeDevice', temperature: temperature, humidity: humidity });
            var message = new Message(data);
            message.properties.add('temperatureAlert', (temperature > 30) ? 'true' : 'false');
            console.log("Sending message: " + message.getData());
            client.sendEvent(message, printResultFor('send'));
        }, 1000);
      }
    };
    ```
8. <span data-ttu-id="4776c-172">開啟 hello 連接 tooyour IoT 中樞，並開始傳送訊息：</span><span class="sxs-lookup"><span data-stu-id="4776c-172">Open hello connection tooyour IoT Hub and start sending messages:</span></span>
   
    ```
    client.open(connectCallback);
    ```
9. <span data-ttu-id="4776c-173">儲存並關閉 hello **SimulatedDevice.js**檔案。</span><span class="sxs-lookup"><span data-stu-id="4776c-173">Save and close hello **SimulatedDevice.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="4776c-174">簡單 tookeep 方面，本教學課程未實作任何重試原則。</span><span class="sxs-lookup"><span data-stu-id="4776c-174">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="4776c-175">在實際執行程式碼，您應該實作重試原則 （例如指數型輪詢），做為建議 hello MSDN 文件中[暫時性錯誤處理][lnk-transient-faults]。</span><span class="sxs-lookup"><span data-stu-id="4776c-175">In production code, you should implement retry policies (such as an exponential backoff), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="run-hello-apps"></a><span data-ttu-id="4776c-176">執行 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="4776c-176">Run hello apps</span></span>
<span data-ttu-id="4776c-177">現在您已經準備就緒 toorun hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4776c-177">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="4776c-178">在命令提示字元中 hello **readdevicetocloudmessages**資料夾中，執行下列命令 toobegin 監視您的 IoT 中樞的 hello:</span><span class="sxs-lookup"><span data-stu-id="4776c-178">At a command prompt in hello **readdevicetocloudmessages** folder, run hello following command toobegin monitoring your IoT hub:</span></span>
   
    ```
    node ReadDeviceToCloudMessages.js 
    ```
   
    ![Node.js IoT 中樞服務應用程式 toomonitor 裝置到雲端訊息][7]
2. <span data-ttu-id="4776c-180">在命令提示字元中 hello **simulateddevice**資料夾中，執行下列命令 toobegin 傳送遙測資料 tooyour IoT 中樞的 hello:</span><span class="sxs-lookup"><span data-stu-id="4776c-180">At a command prompt in hello **simulateddevice** folder, run hello following command toobegin sending telemetry data tooyour IoT hub:</span></span>
   
    ```
    node SimulatedDevice.js
    ```
   
    ![Node.js IoT 中樞裝置應用程式 toosend 裝置到雲端訊息][8]
3. <span data-ttu-id="4776c-182">hello**使用量**磚中 hello [Azure 入口網站][ lnk-portal]顯示 hello 訊息傳送 toohello IoT 中樞的數目：</span><span class="sxs-lookup"><span data-stu-id="4776c-182">hello **Usage** tile in hello [Azure portal][lnk-portal] shows hello number of messages sent toohello IoT hub:</span></span>
   
    ![Azure 入口網站使用並排顯示的數目傳送的訊息 tooIoT 中樞][43]

## <a name="next-steps"></a><span data-ttu-id="4776c-184">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4776c-184">Next steps</span></span>
<span data-ttu-id="4776c-185">在本教學課程中，您在 hello Azure 入口網站中設定新的 IoT 中樞，並接著 hello IoT 中樞的身分識別登錄中建立裝置身分識別。</span><span class="sxs-lookup"><span data-stu-id="4776c-185">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="4776c-186">您已經使用此裝置身分識別 tooenable hello 模擬裝置的應用程式 toosend 裝置到雲端訊息 toohello IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="4776c-186">You used this device identity tooenable hello simulated device app toosend device-to-cloud messages toohello IoT hub.</span></span> <span data-ttu-id="4776c-187">您也會建立會顯示 hello IoT 中樞收到 hello 訊息的應用程式。</span><span class="sxs-lookup"><span data-stu-id="4776c-187">You also created an app that displays hello messages received by hello IoT hub.</span></span> 

<span data-ttu-id="4776c-188">使用者入門 toocontinue tooexplore IoT 中樞與其他 IoT 案例，請參閱：</span><span class="sxs-lookup"><span data-stu-id="4776c-188">toocontinue getting started with IoT Hub and tooexplore other IoT scenarios, see:</span></span>

* <span data-ttu-id="4776c-189">[連接您的裝置][lnk-connect-device]</span><span class="sxs-lookup"><span data-stu-id="4776c-189">[Connecting your device][lnk-connect-device]</span></span>
* <span data-ttu-id="4776c-190">[開始使用裝置管理][lnk-device-management]</span><span class="sxs-lookup"><span data-stu-id="4776c-190">[Getting started with device management][lnk-device-management]</span></span>
* <span data-ttu-id="4776c-191">[開始使用 Azure IoT Edge][lnk-iot-edge]</span><span class="sxs-lookup"><span data-stu-id="4776c-191">[Getting started with Azure IoT Edge][lnk-iot-edge]</span></span>

<span data-ttu-id="4776c-192">toolearn 如何 tooextend 您 IoT 方案和程序裝置到雲端訊息在小數位數，請參閱 hello[處理裝置到雲端訊息][ lnk-process-d2c-tutorial]教學課程。</span><span class="sxs-lookup"><span data-stu-id="4776c-192">toolearn how tooextend your IoT solution and process device-to-cloud messages at scale, see hello [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span>
[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]


<!-- Images. -->
[7]: ./media/iot-hub-node-node-getstarted/runapp1.png
[8]: ./media/iot-hub-node-node-getstarted/runapp2.png
[43]: ./media/iot-hub-csharp-csharp-getstarted/usage.png

<!-- Links -->
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-eventhubs-tutorial]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-devguide-identity]: iot-hub-devguide-identity-registry.md
[lnk-event-hubs-overview]: ../event-hubs/event-hubs-overview.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
[lnk-process-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal]: https://portal.azure.com/

[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/
