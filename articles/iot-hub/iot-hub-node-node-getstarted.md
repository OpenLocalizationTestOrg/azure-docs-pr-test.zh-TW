---
title: "開始使用 Azure IoT 中樞 (Node) | Microsoft Docs"
description: "了解如何使用適用於 Node.js 的 IoT SDK 將裝置到雲端訊息傳送至 Azure IoT 中樞。 建立模擬裝置和服務應用程式來註冊您的裝置、傳送訊息，並從 IoT 中樞讀取訊息。"
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
ms.openlocfilehash: b27a34c0f1f127628912ad68a002e15cc838b4d0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="connect-your-simulated-device-to-your-iot-hub-using-node"></a><span data-ttu-id="0d879-104">使用 Node 將您的模擬裝置連線至 IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="0d879-104">Connect your simulated device to your IoT hub using Node</span></span>
[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

<span data-ttu-id="0d879-105">在本教學課程結尾處，您會有三個 Node.js 主控台應用程式：</span><span class="sxs-lookup"><span data-stu-id="0d879-105">At the end of this tutorial, you have three Node.js console apps:</span></span>

* <span data-ttu-id="0d879-106">**CreateDeviceIdentity.js**，這會建立裝置身分識別與相關聯的安全性金鑰，來連線到您的模擬裝置應用程式。</span><span class="sxs-lookup"><span data-stu-id="0d879-106">**CreateDeviceIdentity.js**, which creates a device identity and associated security key to connect your simulated device app.</span></span>
* <span data-ttu-id="0d879-107">**ReadDeviceToCloudMessages.js**，其中顯示模擬裝置應用程式所傳送的遙測。</span><span class="sxs-lookup"><span data-stu-id="0d879-107">**ReadDeviceToCloudMessages.js**, which displays the telemetry sent by your simulated device app.</span></span>
* <span data-ttu-id="0d879-108">**SimulatedDevice.js**，這會使用先前建立的裝置識別連接到您的 IoT 中樞，並使用 MQTT 通訊協定每秒傳送遙測訊息。</span><span class="sxs-lookup"><span data-stu-id="0d879-108">**SimulatedDevice.js**, which connects to your IoT hub with the device identity created earlier, and sends a telemetry message every second using the MQTT protocol.</span></span>

> [!NOTE]
> <span data-ttu-id="0d879-109">[Azure IoT SDK][lnk-hub-sdks] 一文提供 Azure IoT SDK (可讓您同時建置在裝置與您的解決方案後端執行的兩個應用程式) 的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="0d879-109">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both applications to run on devices and your solution back end.</span></span>
> 
> 

<span data-ttu-id="0d879-110">若要完成此教學課程，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="0d879-110">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="0d879-111">Node.js 0.10.x 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="0d879-111">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="0d879-112">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="0d879-112">An active Azure account.</span></span> <span data-ttu-id="0d879-113">(如果您沒有帳戶，只需要幾分鐘的時間就可以建立[免費帳戶][lnk-free-trial]。)</span><span class="sxs-lookup"><span data-stu-id="0d879-113">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

<span data-ttu-id="0d879-114">您現在已經建立 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="0d879-114">You have now created your IoT hub.</span></span> <span data-ttu-id="0d879-115">您具有完成本教學課程的其餘部分所需的 IoT 中樞主機名稱和連接字串。</span><span class="sxs-lookup"><span data-stu-id="0d879-115">You have the IoT Hub host name and the IoT Hub connection string that you need to complete the rest of this tutorial.</span></span>

## <a name="create-a-device-identity"></a><span data-ttu-id="0d879-116">建立裝置識別</span><span class="sxs-lookup"><span data-stu-id="0d879-116">Create a device identity</span></span>
<span data-ttu-id="0d879-117">在本節中，您會建立 Node.js 主控台應用程式，而它會在 IoT 中樞的識別登錄中建立裝置識別。</span><span class="sxs-lookup"><span data-stu-id="0d879-117">In this section, you create a Node.js console app that creates a device identity in the identity registry in your IoT hub.</span></span> <span data-ttu-id="0d879-118">如果裝置在身分識別登錄中具有項目，則只能連線到 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="0d879-118">A device can only connect to IoT hub if it has an entry in the identity registry.</span></span> <span data-ttu-id="0d879-119">如需詳細資訊，請參閱 [IoT 中樞開發人員指南][lnk-devguide-identity]的＜身分識別登錄＞一節。</span><span class="sxs-lookup"><span data-stu-id="0d879-119">For more information, see the **Identity Registry** section of the [IoT Hub developer guide][lnk-devguide-identity].</span></span> <span data-ttu-id="0d879-120">執行這個主控台應用程式時，它會產生唯一的裝置識別碼及金鑰，當裝置向 IoT 中樞傳送裝置對雲端訊息時，可以用來識別裝置本身。</span><span class="sxs-lookup"><span data-stu-id="0d879-120">When you run this console app, it generates a unique device ID and key that your device can use to identify itself when it sends device-to-cloud messages to IoT Hub.</span></span>

1. <span data-ttu-id="0d879-121">建立稱為 **createdeviceidentity**的新的空資料夾。</span><span class="sxs-lookup"><span data-stu-id="0d879-121">Create a new empty folder called **createdeviceidentity**.</span></span> <span data-ttu-id="0d879-122">在 **createdeviceidentity** 資料夾中，於命令提示字元使用下列命令建立 package.json 檔案。</span><span class="sxs-lookup"><span data-stu-id="0d879-122">In the **createdeviceidentity** folder, create a package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="0d879-123">接受所有預設值：</span><span class="sxs-lookup"><span data-stu-id="0d879-123">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="0d879-124">在 **createdeviceidentity** 資料夾中，於命令提示字元執行下列命令以安裝 **azure-iothub** 服務 SDK 套件：</span><span class="sxs-lookup"><span data-stu-id="0d879-124">At your command prompt in the **createdeviceidentity** folder, run the following command to install the **azure-iothub** Service SDK package:</span></span>
   
    ```
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="0d879-125">使用文字編輯器，在 **createdeviceidentity** 資料夾中建立 **CreateDeviceIdentity.js** 檔案。</span><span class="sxs-lookup"><span data-stu-id="0d879-125">Using a text editor, create a **CreateDeviceIdentity.js** file in the **createdeviceidentity** folder.</span></span>
4. <span data-ttu-id="0d879-126">在 **CreateDeviceIdentity.js** 檔案開頭新增下列 `require` 陳述式：</span><span class="sxs-lookup"><span data-stu-id="0d879-126">Add the following `require` statement at the start of the **CreateDeviceIdentity.js** file:</span></span>
   
    ```
    'use strict';
   
    var iothub = require('azure-iothub');
    ```
5. <span data-ttu-id="0d879-127">將下列程式碼加入至 **CreateDeviceIdentity.js** 檔案，並將預留位置的值替換為您在上一節中為中樞所建立的 IoT 中樞連接字串：</span><span class="sxs-lookup"><span data-stu-id="0d879-127">Add the following code to the **CreateDeviceIdentity.js** file and replace the placeholder value with the IoT Hub connection string for the hub you created in the previous section:</span></span> 
   
    ```
    var connectionString = '{iothub connection string}';
   
    var registry = iothub.Registry.fromConnectionString(connectionString);
    ```
6. <span data-ttu-id="0d879-128">新增下列程式碼以在 IoT 中樞的身分識別登錄建立裝置定義。</span><span class="sxs-lookup"><span data-stu-id="0d879-128">Add the following code to create a device definition in the identity registry in your IoT hub.</span></span> <span data-ttu-id="0d879-129">如果身分識別登錄中沒有該裝置識別碼，此程式碼會建立裝置，否則會傳回現有裝置的金鑰：</span><span class="sxs-lookup"><span data-stu-id="0d879-129">This code creates a device if the device ID does not exist in the identity registry, otherwise it returns the key of the existing device:</span></span>
   
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

7. <span data-ttu-id="0d879-130">儲存並關閉 **CreateDeviceIdentity.js** 檔案。</span><span class="sxs-lookup"><span data-stu-id="0d879-130">Save and close **CreateDeviceIdentity.js** file.</span></span>
8. <span data-ttu-id="0d879-131">若要執行 **createdeviceidentity** 應用程式，請在命令提示字元中於 createdeviceidentity 資料夾內執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="0d879-131">To run the **createdeviceidentity** application, execute the following command at the command prompt in the createdeviceidentity folder:</span></span>
   
    ```
    node CreateDeviceIdentity.js 
    ```
9. <span data-ttu-id="0d879-132">記下**裝置識別碼**和**裝置金鑰**。</span><span class="sxs-lookup"><span data-stu-id="0d879-132">Make a note of the **Device ID** and **Device key**.</span></span> <span data-ttu-id="0d879-133">稍後在建立連線至做為裝置之 IoT 中樞的應用程式時，您會需要這些值。</span><span class="sxs-lookup"><span data-stu-id="0d879-133">You need these values later when you create an application that connects to IoT Hub as a device.</span></span>

> [!NOTE]
> <span data-ttu-id="0d879-134">IoT 中樞身分識別登錄只會儲存裝置身分識別，以啟用對 IoT 中樞的安全存取。</span><span class="sxs-lookup"><span data-stu-id="0d879-134">The IoT Hub identity registry only stores device identities to enable secure access to the IoT hub.</span></span> <span data-ttu-id="0d879-135">它會儲存裝置識別碼和金鑰來作為安全性認證，以及啟用或停用旗標，讓您用來停用個別裝置的存取。</span><span class="sxs-lookup"><span data-stu-id="0d879-135">It stores device IDs and keys to use as security credentials and an enabled/disabled flag that you can use to disable access for an individual device.</span></span> <span data-ttu-id="0d879-136">如果您的應用程式需要儲存其他裝置特定的中繼資料，它應該使用應用程式專用的存放區。</span><span class="sxs-lookup"><span data-stu-id="0d879-136">If your application needs to store other device-specific metadata, it should use an application-specific store.</span></span> <span data-ttu-id="0d879-137">如需詳細資訊，請參閱 [IoT 中樞開發人員指南][lnk-devguide-identity]。</span><span class="sxs-lookup"><span data-stu-id="0d879-137">For more information, see the [IoT Hub developer guide][lnk-devguide-identity].</span></span>
> 
> 

<a id="D2C_node"></a>
## <a name="receive-device-to-cloud-messages"></a><span data-ttu-id="0d879-138">接收裝置到雲端的訊息</span><span class="sxs-lookup"><span data-stu-id="0d879-138">Receive device-to-cloud messages</span></span>
<span data-ttu-id="0d879-139">在本節中，您會建立 Node.js 主控台應用程式，以讀取來自 IoT 中樞的裝置到雲端訊息。</span><span class="sxs-lookup"><span data-stu-id="0d879-139">In this section, you create a Node.js console app that reads device-to-cloud messages from IoT Hub.</span></span> <span data-ttu-id="0d879-140">IoT 中樞會公開與[事件中樞][lnk-event-hubs-overview]相容的端點以讓您讀取裝置到雲端訊息。</span><span class="sxs-lookup"><span data-stu-id="0d879-140">An IoT hub exposes an [Event Hubs][lnk-event-hubs-overview]-compatible endpoint to enable you to read device-to-cloud messages.</span></span> <span data-ttu-id="0d879-141">為了簡單起見，本教學課程會建立的基本讀取器不適合用於高輸送量部署。</span><span class="sxs-lookup"><span data-stu-id="0d879-141">To keep things simple, this tutorial creates a basic reader that is not suitable for a high throughput deployment.</span></span> <span data-ttu-id="0d879-142">[處理裝置到雲端訊息][lnk-process-d2c-tutorial]教學課程會說明如何大規模處理裝置到雲端訊息。</span><span class="sxs-lookup"><span data-stu-id="0d879-142">The [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial shows you how to process device-to-cloud messages at scale.</span></span> <span data-ttu-id="0d879-143">[開始使用事件中樞][lnk-eventhubs-tutorial]教學課程提供進一步的資訊，說明如何處理來自事件中樞的訊息，而且此教學課程也適用於 IoT 中樞事件中樞相容端點。</span><span class="sxs-lookup"><span data-stu-id="0d879-143">The [Get Started with Event Hubs][lnk-eventhubs-tutorial] tutorial provides further information on how to process messages from Event Hubs and is applicable to the IoT Hub Event Hub-compatible endpoints.</span></span>

> [!NOTE]
> <span data-ttu-id="0d879-144">用於讀取裝置到雲端訊息的事件中樞相容端點一律會使用 AMQP 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="0d879-144">The Event Hub-compatible endpoint for reading device-to-cloud messages always uses the AMQP protocol.</span></span>
> 
> 

1. <span data-ttu-id="0d879-145">建立稱為 **readdevicetocloudmessages** 的空資料夾。</span><span class="sxs-lookup"><span data-stu-id="0d879-145">Create an empty folder called **readdevicetocloudmessages**.</span></span> <span data-ttu-id="0d879-146">在 **readdevicetocloudmessages** 資料夾中，於命令提示字元使用下列命令建立 package.json 檔案。</span><span class="sxs-lookup"><span data-stu-id="0d879-146">In the **readdevicetocloudmessages** folder, create a package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="0d879-147">接受所有預設值：</span><span class="sxs-lookup"><span data-stu-id="0d879-147">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="0d879-148">在 **readdevicetocloudmessages** 資料夾的命令提示字元中，執行下列命令以安裝 **azure-event-hubs** 套件：</span><span class="sxs-lookup"><span data-stu-id="0d879-148">At your command prompt in the **readdevicetocloudmessages** folder, run the following command to install the **azure-event-hubs** package:</span></span>
   
    ```
    npm install azure-event-hubs --save
    ```
3. <span data-ttu-id="0d879-149">使用文字編輯器，在 **readdevicetocloudmessages** 資料夾中建立 **ReadDeviceToCloudMessages.js** 檔案。</span><span class="sxs-lookup"><span data-stu-id="0d879-149">Using a text editor, create a **ReadDeviceToCloudMessages.js** file in the **readdevicetocloudmessages** folder.</span></span>
4. <span data-ttu-id="0d879-150">在 **ReadDeviceToCloudMessages.js** 檔案開頭新增下列 `require` 陳述式：</span><span class="sxs-lookup"><span data-stu-id="0d879-150">Add the following `require` statements at the start of the **ReadDeviceToCloudMessages.js** file:</span></span>
   
    ```
    'use strict';
   
    var EventHubClient = require('azure-event-hubs').Client;
    ```
5. <span data-ttu-id="0d879-151">新增下列變數宣告，並將預留位置值替換為中樞的 IoT 中樞連接字串：</span><span class="sxs-lookup"><span data-stu-id="0d879-151">Add the following variable declaration and replace the placeholder value with the IoT Hub connection string for your hub:</span></span>
   
    ```
    var connectionString = '{iothub connection string}';
    ```
6. <span data-ttu-id="0d879-152">新增下列兩個會將輸出列印到主控台的函數：</span><span class="sxs-lookup"><span data-stu-id="0d879-152">Add the following two functions that print output to the console:</span></span>
   
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
7. <span data-ttu-id="0d879-153">加入下列程式碼以建立 **EventHubClient**、開啟您的 IoT 中樞的連線，並建立每個資料分割的接收者。</span><span class="sxs-lookup"><span data-stu-id="0d879-153">Add the following code to create the **EventHubClient**, open the connection to your IoT Hub, and create a receiver for each partition.</span></span> <span data-ttu-id="0d879-154">在建立開始執行後只會讀取傳送到 IoT 中樞之訊息的收件者時，此應用程式會使用篩選器。</span><span class="sxs-lookup"><span data-stu-id="0d879-154">This application uses a filter when it creates a receiver so that the receiver only reads messages sent to IoT Hub after the receiver starts running.</span></span> <span data-ttu-id="0d879-155">此篩選器很適合測試環境，如此一來您即可看到目前的訊息集。</span><span class="sxs-lookup"><span data-stu-id="0d879-155">This filter is useful in a test environment so you see just the current set of messages.</span></span> <span data-ttu-id="0d879-156">在生產環境中，您的程式碼應該要確定它能處理所有訊息。</span><span class="sxs-lookup"><span data-stu-id="0d879-156">In a production environment, your code should make sure that it processes all the messages.</span></span> <span data-ttu-id="0d879-157">如需詳細資訊，請參閱[如何處理 IoT 中樞裝置到雲端訊息][lnk-process-d2c-tutorial]教學課程：</span><span class="sxs-lookup"><span data-stu-id="0d879-157">For more information, see the [How to process IoT Hub device-to-cloud messages][lnk-process-d2c-tutorial] tutorial:</span></span>
   
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
8. <span data-ttu-id="0d879-158">儲存並關閉 **ReadDeviceToCloudMessages.js** 檔案。</span><span class="sxs-lookup"><span data-stu-id="0d879-158">Save and close the **ReadDeviceToCloudMessages.js** file.</span></span>

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="0d879-159">建立模擬裝置應用程式</span><span class="sxs-lookup"><span data-stu-id="0d879-159">Create a simulated device app</span></span>
<span data-ttu-id="0d879-160">在本節中，您會撰寫 Node.js 主控台應用程式，模擬裝置傳送裝置對雲端訊息至 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="0d879-160">In this section, you create a Node.js console app that simulates a device that sends device-to-cloud messages to an IoT hub.</span></span>

1. <span data-ttu-id="0d879-161">建立稱為 **simulateddevice**的空資料夾。</span><span class="sxs-lookup"><span data-stu-id="0d879-161">Create an empty folder called **simulateddevice**.</span></span> <span data-ttu-id="0d879-162">在 **simulateddevice** 資料夾中，於命令提示字元使用下列命令建立 package.json 檔案。</span><span class="sxs-lookup"><span data-stu-id="0d879-162">In the **simulateddevice** folder, create a package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="0d879-163">接受所有預設值：</span><span class="sxs-lookup"><span data-stu-id="0d879-163">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="0d879-164">在 **simulateddevice** 資料夾中，於命令提示字元執行下列命令以安裝 **azure-iot-device** 裝置 SDK 套件以及 **azure-iot-device-mqtt** 套件：</span><span class="sxs-lookup"><span data-stu-id="0d879-164">At your command prompt in the **simulateddevice** folder, run the following command to install the **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="0d879-165">使用文字編輯器，在 **simulateddevice** 資料夾中建立 **SimulatedDevice.js** 檔案。</span><span class="sxs-lookup"><span data-stu-id="0d879-165">Using a text editor, create a **SimulatedDevice.js** file in the **simulateddevice** folder.</span></span>
4. <span data-ttu-id="0d879-166">在 **SimulatedDevice.js** 檔案開頭新增下列 `require` 陳述式：</span><span class="sxs-lookup"><span data-stu-id="0d879-166">Add the following `require` statements at the start of the **SimulatedDevice.js** file:</span></span>
   
    ```
    'use strict';
   
    var clientFromConnectionString = require('azure-iot-device-mqtt').clientFromConnectionString;
    var Message = require('azure-iot-device').Message;
    ```
5. <span data-ttu-id="0d879-167">新增 **connectionString** 變數，並用它來建立**用戶端**執行個體。</span><span class="sxs-lookup"><span data-stu-id="0d879-167">Add a **connectionString** variable and use it to create a **Client** instance.</span></span> <span data-ttu-id="0d879-168">以您在＜建立 IoT 中樞＞  一節中建立的 IoT 中樞名稱取代 *{youriothostname}* 。</span><span class="sxs-lookup"><span data-stu-id="0d879-168">Replace **{youriothostname}** with the name of the IoT hub you created the *Create an IoT Hub* section.</span></span> <span data-ttu-id="0d879-169">以您在＜建立裝置識別＞  一節中產生的裝置金鑰值取代 *{yourdevicekey}* ：</span><span class="sxs-lookup"><span data-stu-id="0d879-169">Replace **{yourdevicekey}** with the device key value you generated in the *Create a device identity* section:</span></span>
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId=myFirstNodeDevice;SharedAccessKey={yourdevicekey}';
   
    var client = clientFromConnectionString(connectionString);
    ```
6. <span data-ttu-id="0d879-170">新增下列函數來顯示應用程式的輸出：</span><span class="sxs-lookup"><span data-stu-id="0d879-170">Add the following function to display output from the application:</span></span>
   
    ```
    function printResultFor(op) {
      return function printResult(err, res) {
        if (err) console.log(op + ' error: ' + err.toString());
        if (res) console.log(op + ' status: ' + res.constructor.name);
      };
    }
    ```
7. <span data-ttu-id="0d879-171">建立回呼，並使用 **setInterval** 函式每秒將新訊息傳送至 IoT 中樞：</span><span class="sxs-lookup"><span data-stu-id="0d879-171">Create a callback and use the **setInterval** function to send a message to your IoT hub every second:</span></span>
   
    ```
    var connectCallback = function (err) {
      if (err) {
        console.log('Could not connect: ' + err);
      } else {
        console.log('Client connected');
   
        // Create a message and send it to the IoT Hub every second
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
8. <span data-ttu-id="0d879-172">開啟您 IoT 中樞的連線，並開始傳送訊息︰</span><span class="sxs-lookup"><span data-stu-id="0d879-172">Open the connection to your IoT Hub and start sending messages:</span></span>
   
    ```
    client.open(connectCallback);
    ```
9. <span data-ttu-id="0d879-173">儲存並關閉 **SimulatedDevice.js** 檔案。</span><span class="sxs-lookup"><span data-stu-id="0d879-173">Save and close the **SimulatedDevice.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="0d879-174">為了簡單起見，本教學課程不會實作任何重試原則。</span><span class="sxs-lookup"><span data-stu-id="0d879-174">To keep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="0d879-175">在實際程式碼中，您應該如 MSDN 文章[暫時性錯誤處理][lnk-transient-faults]所建議，實作重試原則 (例如指數型輪詢)。</span><span class="sxs-lookup"><span data-stu-id="0d879-175">In production code, you should implement retry policies (such as an exponential backoff), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="run-the-apps"></a><span data-ttu-id="0d879-176">執行應用程式</span><span class="sxs-lookup"><span data-stu-id="0d879-176">Run the apps</span></span>
<span data-ttu-id="0d879-177">您現在可以開始執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="0d879-177">You are now ready to run the apps.</span></span>

1. <span data-ttu-id="0d879-178">在 **readdevicetocloudmessages** 資料夾的命令提示字元中，執行下列命令以開始監視 IoT 中樞：</span><span class="sxs-lookup"><span data-stu-id="0d879-178">At a command prompt in the **readdevicetocloudmessages** folder, run the following command to begin monitoring your IoT hub:</span></span>
   
    ```
    node ReadDeviceToCloudMessages.js 
    ```
   
    ![用來監視裝置到雲端訊息的 Node.js IoT 中樞服務應用程式][7]
2. <span data-ttu-id="0d879-180">在 **simulateddevice** 資料夾的命令提示字元中，執行下列命令以開始將遙測資料傳送至 IoT 中樞：</span><span class="sxs-lookup"><span data-stu-id="0d879-180">At a command prompt in the **simulateddevice** folder, run the following command to begin sending telemetry data to your IoT hub:</span></span>
   
    ```
    node SimulatedDevice.js
    ```
   
    ![用來傳送裝置到雲端訊息的 Node.js IoT 中樞裝置應用程式][8]
3. <span data-ttu-id="0d879-182">[Azure 入口網站][lnk-portal]中的 [使用量] 圖格會顯示傳送至 IoT 中樞的訊息數目︰</span><span class="sxs-lookup"><span data-stu-id="0d879-182">The **Usage** tile in the [Azure portal][lnk-portal] shows the number of messages sent to the IoT hub:</span></span>
   
    ![顯示傳送到 IoT 中樞之訊息數目的 Azure 入口網站使用量圖格][43]

## <a name="next-steps"></a><span data-ttu-id="0d879-184">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0d879-184">Next steps</span></span>
<span data-ttu-id="0d879-185">在此教學課程中，您在 Azure 入口網站中設定了新的 IoT 中樞，然後在 IoT 中樞的身分識別登錄中建立了裝置身分識別。</span><span class="sxs-lookup"><span data-stu-id="0d879-185">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="0d879-186">您會將此裝置身分識別用於啟用模擬裝置應用程式，以將裝置到雲端訊息傳送至 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="0d879-186">You used this device identity to enable the simulated device app to send device-to-cloud messages to the IoT hub.</span></span> <span data-ttu-id="0d879-187">您也會建立一個應用程式來顯示 IoT 中樞所接收的訊息。</span><span class="sxs-lookup"><span data-stu-id="0d879-187">You also created an app that displays the messages received by the IoT hub.</span></span> 

<span data-ttu-id="0d879-188">若要繼續開始使用 IoT 中樞並瀏覽其他 IoT 案例，請參閱︰</span><span class="sxs-lookup"><span data-stu-id="0d879-188">To continue getting started with IoT Hub and to explore other IoT scenarios, see:</span></span>

* <span data-ttu-id="0d879-189">[連接您的裝置][lnk-connect-device]</span><span class="sxs-lookup"><span data-stu-id="0d879-189">[Connecting your device][lnk-connect-device]</span></span>
* <span data-ttu-id="0d879-190">[開始使用裝置管理][lnk-device-management]</span><span class="sxs-lookup"><span data-stu-id="0d879-190">[Getting started with device management][lnk-device-management]</span></span>
* <span data-ttu-id="0d879-191">[開始使用 Azure IoT Edge][lnk-iot-edge]</span><span class="sxs-lookup"><span data-stu-id="0d879-191">[Getting started with Azure IoT Edge][lnk-iot-edge]</span></span>

<span data-ttu-id="0d879-192">若要了解如何擴充您的 IoT 解決方案及大規模處理裝置到雲端訊息，請參閱[處理裝置到雲端訊息][lnk-process-d2c-tutorial]教學課程。</span><span class="sxs-lookup"><span data-stu-id="0d879-192">To learn how to extend your IoT solution and process device-to-cloud messages at scale, see the [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span>
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
