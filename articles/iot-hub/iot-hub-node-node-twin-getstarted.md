---
title: "開始使用 Azure IoT 中樞裝置對應項 (Node) | Microsoft Docs"
description: "如何使用 Azure IoT 中樞裝置對應項來新增標籤，然後使用 IoT 中樞查詢。 您可以使用適用於 Node.js 的 Azure IoT SDK，實作模擬裝置應用程式和服務應用程式，以新增標籤和執行 IoT 中樞查詢。"
services: iot-hub
documentationcenter: node
author: fsautomata
manager: timlt
editor: 
ms.assetid: 314c88e4-cce1-441c-b75a-d2e08e39ae7d
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: elioda
ms.openlocfilehash: 633c9fd4f8a1d017d93148f8c2e860ccba14238c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-device-twins-node"></a><span data-ttu-id="0dc3b-104">開始使用裝置對應項 (Node)</span><span class="sxs-lookup"><span data-stu-id="0dc3b-104">Get started with device twins (Node)</span></span>
[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

<span data-ttu-id="0dc3b-105">在本教學課程結尾端，您將會有兩個 Node.js 主控台應用程式：</span><span class="sxs-lookup"><span data-stu-id="0dc3b-105">At the end of this tutorial, you will have two Node.js console apps:</span></span>

* <span data-ttu-id="0dc3b-106">**AddTagsAndQuery.js**，這是 Node.js 後端應用程式，可新增標籤和查詢裝置對應項。</span><span class="sxs-lookup"><span data-stu-id="0dc3b-106">**AddTagsAndQuery.js**, a Node.js back-end app, which adds tags and queries device twins.</span></span>
* <span data-ttu-id="0dc3b-107">**TwinSimulatedDevice.js**，這是會模擬裝置的 Node.js 應用程式，此裝置會以稍早建立的身分識別連接到您的 IoT 中樞，並報告其連線狀況。</span><span class="sxs-lookup"><span data-stu-id="0dc3b-107">**TwinSimulatedDevice.js**, a Node.js app which simulates a device that connects to your IoT hub with the device identity created earlier, and reports its connectivity condition.</span></span>

> [!NOTE]
> <span data-ttu-id="0dc3b-108">[Azure IoT SDK][lnk-hub-sdks] 一文提供可用來建置裝置和後端應用程式之 Azure IoT SDK 的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="0dc3b-108">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="0dc3b-109">若要完成此教學課程，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="0dc3b-109">To complete this tutorial you need the following:</span></span>

* <span data-ttu-id="0dc3b-110">Node.js 0.10.x 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="0dc3b-110">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="0dc3b-111">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="0dc3b-111">An active Azure account.</span></span> <span data-ttu-id="0dc3b-112">(如果您沒有帳戶，只需要幾分鐘的時間就可以建立[免費帳戶][lnk-free-trial]。)</span><span class="sxs-lookup"><span data-stu-id="0dc3b-112">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-the-service-app"></a><span data-ttu-id="0dc3b-113">建立服務應用程式</span><span class="sxs-lookup"><span data-stu-id="0dc3b-113">Create the service app</span></span>
<span data-ttu-id="0dc3b-114">在本節中，您將建立一個 Node.js 主控台應用程式，此應用程式會將位置中繼資料新增至與 **myDeviceId** 相關聯的裝置對應項。</span><span class="sxs-lookup"><span data-stu-id="0dc3b-114">In this section, you create a Node.js console app that adds location metadata to the device twin associated with **myDeviceId**.</span></span> <span data-ttu-id="0dc3b-115">接著，它會選取位於美國的裝置來查詢儲存在 IoT 中樞的裝置對應項，再查詢會報告行動電話連線的對應項。</span><span class="sxs-lookup"><span data-stu-id="0dc3b-115">It then queries the device twins stored in the IoT hub selecting the devices located in the US, and then the ones that are reporting a cellular connection.</span></span>

1. <span data-ttu-id="0dc3b-116">建立稱為 **addtagsandqueryapp** 的新空白資料夾。</span><span class="sxs-lookup"><span data-stu-id="0dc3b-116">Create a new empty folder called **addtagsandqueryapp**.</span></span> <span data-ttu-id="0dc3b-117">在 **addtagsandqueryapp** 資料夾中，於命令提示字元使用下列命令建立新的 package.json 檔案。</span><span class="sxs-lookup"><span data-stu-id="0dc3b-117">In the **addtagsandqueryapp** folder, create a new package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="0dc3b-118">接受所有預設值：</span><span class="sxs-lookup"><span data-stu-id="0dc3b-118">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="0dc3b-119">在命令提示字元下，於 **addtagsandqueryapp** 資料夾中執行下列命令以安裝 **azure-iothub** 套件：</span><span class="sxs-lookup"><span data-stu-id="0dc3b-119">At your command prompt in the **addtagsandqueryapp** folder, run the following command to install the **azure-iothub** package:</span></span>
   
    ```
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="0dc3b-120">使用文字編輯器，在 **addtagsandqueryapp** 資料夾中建立新的 **AddTagsAndQuery.js** 檔案。</span><span class="sxs-lookup"><span data-stu-id="0dc3b-120">Using a text editor, create a new **AddTagsAndQuery.js** file in the **addtagsandqueryapp** folder.</span></span>
4. <span data-ttu-id="0dc3b-121">將下列程式碼新增至 **AddTagsAndQuery.js** 檔案，並以您建立中樞時所複製的 IoT 中樞連接字串，取代 **{iot hub connection string}** 預留位置︰</span><span class="sxs-lookup"><span data-stu-id="0dc3b-121">Add the following code to the **AddTagsAndQuery.js** file, and substitute the **{iot hub connection string}** placeholder with the IoT Hub connection string you copied when you created your hub:</span></span>
   
        'use strict';
        var iothub = require('azure-iothub');
        var connectionString = '{iot hub connection string}';
        var registry = iothub.Registry.fromConnectionString(connectionString);
   
        registry.getTwin('myDeviceId', function(err, twin){
            if (err) {
                console.error(err.constructor.name + ': ' + err.message);
            } else {
                var patch = {
                    tags: {
                        location: {
                            region: 'US',
                            plant: 'Redmond43'
                      }
                    }
                };
   
                twin.update(patch, function(err) {
                  if (err) {
                    console.error('Could not update twin: ' + err.constructor.name + ': ' + err.message);
                  } else {
                    console.log(twin.deviceId + ' twin updated successfully');
                    queryTwins();
                  }
                });
            }
        });
   
    <span data-ttu-id="0dc3b-122">**Registry** 物件會公開從服務來與裝置對應項進行互動時所需的所有方法。</span><span class="sxs-lookup"><span data-stu-id="0dc3b-122">The **Registry** object exposes all the methods required to interact with device twins from the service.</span></span> <span data-ttu-id="0dc3b-123">先前的程式碼會先初始化 **Registry** 物件，然後擷取 **myDeviceId** 的裝置對應項，最後會以所需的位置資訊來更新其標籤。</span><span class="sxs-lookup"><span data-stu-id="0dc3b-123">The previous code first initializes the **Registry** object, then retrieves the device twin for **myDeviceId**, and finally updates its tags with the desired location information.</span></span>
   
    <span data-ttu-id="0dc3b-124">更新標籤之後，它會呼叫 **queryTwins** 函式。</span><span class="sxs-lookup"><span data-stu-id="0dc3b-124">After the updating the tags it calls the **queryTwins** function.</span></span>
5. <span data-ttu-id="0dc3b-125">在 **AddTagsAndQuery.js** 結尾處新增下列程式碼來實作 **queryTwins** 函式︰</span><span class="sxs-lookup"><span data-stu-id="0dc3b-125">Add the following code at the end of  **AddTagsAndQuery.js** to implement the **queryTwins** function:</span></span>
   
        var queryTwins = function() {
            var query = registry.createQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43'", 100);
            query.nextAsTwin(function(err, results) {
                if (err) {
                    console.error('Failed to fetch the results: ' + err.message);
                } else {
                    console.log("Devices in Redmond43: " + results.map(function(twin) {return twin.deviceId}).join(','));
                }
            });
   
            query = registry.createQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43' AND properties.reported.connectivity.type = 'cellular'", 100);
            query.nextAsTwin(function(err, results) {
                if (err) {
                    console.error('Failed to fetch the results: ' + err.message);
                } else {
                    console.log("Devices in Redmond43 using cellular network: " + results.map(function(twin) {return twin.deviceId}).join(','));
                }
            });
        };
   
    <span data-ttu-id="0dc3b-126">先前的程式碼會執行兩個查詢︰第一個只選取位於 **Redmond43** 工廠的裝置的裝置對應項，第二個會修改查詢，只選取也透過行動電話網路來連接的裝置。</span><span class="sxs-lookup"><span data-stu-id="0dc3b-126">The previous code executes two queries: the first selects only the device twins of devices located in the **Redmond43** plant, and the second refines the query to select only the devices that are also connected through cellular network.</span></span>
   
    <span data-ttu-id="0dc3b-127">請注意，先前的程式碼在建立 **查詢** 物件時，指定傳回的最大文件數。</span><span class="sxs-lookup"><span data-stu-id="0dc3b-127">Note that the previous code, when it creates the **query** object, specifies a maximum number of returned documents.</span></span> <span data-ttu-id="0dc3b-128">**query** 物件包含 **hasMoreResults** 布林值屬性，可用來多次叫用 **nextAsTwin** 方法以擷取所有結果。</span><span class="sxs-lookup"><span data-stu-id="0dc3b-128">The **query** object contains a **hasMoreResults** boolean property that you can use to invoke the **nextAsTwin** methods multiple times to retrieve all results.</span></span> <span data-ttu-id="0dc3b-129">有一個稱為 **next** 的方法適用於不是裝置對應項的結果，例如彙總查詢的結果。</span><span class="sxs-lookup"><span data-stu-id="0dc3b-129">A method called **next** is available for results that are not device twins for example, results of aggregation queries.</span></span>
6. <span data-ttu-id="0dc3b-130">使用下列命令執行應用程式：</span><span class="sxs-lookup"><span data-stu-id="0dc3b-130">Run the application with:</span></span>
   
        node AddTagsAndQuery.js
   
    <span data-ttu-id="0dc3b-131">如果是查詢所有位於 **Redmond43** 中的裝置，您在結果中會看到一個裝置，而如果查詢將結果限於使用行動電話網路的裝置，則您不會看到任何裝置。</span><span class="sxs-lookup"><span data-stu-id="0dc3b-131">You should see one device in the results for the query asking for all devices located in **Redmond43** and none for the query that restricts the results to devices that use a cellular network.</span></span>
   
    ![][1]

<span data-ttu-id="0dc3b-132">在下一節，您將建立一個裝置應用程式，以報告連線資訊並變更上一節的查詢結果。</span><span class="sxs-lookup"><span data-stu-id="0dc3b-132">In the next section you create a device app that reports the connectivity information and changes the result of the query in the previous section.</span></span>

## <a name="create-the-device-app"></a><span data-ttu-id="0dc3b-133">建立裝置應用程式</span><span class="sxs-lookup"><span data-stu-id="0dc3b-133">Create the device app</span></span>
<span data-ttu-id="0dc3b-134">在本節中，您將建立一個 Node.js 主控台應用程式，此應用程式會以 **myDeviceId** 來連接到您的中樞，然後更新其裝置對應項所報告的屬性，以包含資訊來指出目前使用行動電話網路來連線。</span><span class="sxs-lookup"><span data-stu-id="0dc3b-134">In this section, you create a Node.js console app that connects to your hub as **myDeviceId**, and then updates its device twin's reported properties to contain the information that it is connected using a cellular network.</span></span>

> [!NOTE]
> <span data-ttu-id="0dc3b-135">目前，裝置對應項只能從使用 MQTT 通訊協定連線至 IoT 中樞的裝置存取。</span><span class="sxs-lookup"><span data-stu-id="0dc3b-135">At this time, device twins are accessible only from devices that connect to IoT Hub using the MQTT protocol.</span></span> <span data-ttu-id="0dc3b-136">請參閱 [MQTT 支援][lnk-devguide-mqtt]文章，以取得如何將現有裝置應用程式轉換為使用 MQTT 的指示。</span><span class="sxs-lookup"><span data-stu-id="0dc3b-136">Please refer to the [MQTT support][lnk-devguide-mqtt] article for instructions on how to convert existing device app to use MQTT.</span></span>
> 
> 

1. <span data-ttu-id="0dc3b-137">建立稱為 **reportconnectivity** 的新空白資料夾。</span><span class="sxs-lookup"><span data-stu-id="0dc3b-137">Create a new empty folder called **reportconnectivity**.</span></span> <span data-ttu-id="0dc3b-138">在 **reportconnectivity** 資料夾中，於命令提示字元使用下列命令建立新的 package.json 檔案。</span><span class="sxs-lookup"><span data-stu-id="0dc3b-138">In the **reportconnectivity** folder, create a new package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="0dc3b-139">接受所有預設值：</span><span class="sxs-lookup"><span data-stu-id="0dc3b-139">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="0dc3b-140">在 **reportconnectivity** 資料夾中，於命令提示字元執行下列命令以安裝 **azure-iot-device** 和 **azure-iot-device-mqtt** 套件：</span><span class="sxs-lookup"><span data-stu-id="0dc3b-140">At your command prompt in the **reportconnectivity** folder, run the following command to install the **azure-iot-device**, and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="0dc3b-141">使用文字編輯器，在 **reportconnectivity** 資料夾中建立新的 **ReportConnectivity.js** 檔案。</span><span class="sxs-lookup"><span data-stu-id="0dc3b-141">Using a text editor, create a new **ReportConnectivity.js** file in the **reportconnectivity** folder.</span></span>
4. <span data-ttu-id="0dc3b-142">將下列程式碼新增至 **ReportConnectivity.js** 檔案，並以您建立 **myDeviceId** 裝置身分識別時所複製的裝置連接字串，取代 **{device connection string}** 預留位置︰</span><span class="sxs-lookup"><span data-stu-id="0dc3b-142">Add the following code to the **ReportConnectivity.js** file, and substitute the **{device connection string}** placeholder with the device connection string you copied when you created the **myDeviceId** device identity:</span></span>
   
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
   
    <span data-ttu-id="0dc3b-143">**Client** 物件會公開從裝置來與裝置對應項進行互動時所需的所有方法。</span><span class="sxs-lookup"><span data-stu-id="0dc3b-143">The **Client** object exposes all the methods you require to interact with device twins from the device.</span></span> <span data-ttu-id="0dc3b-144">先前的程式碼在初始化 **Client** 物件之後，會擷取 **myDeviceId** 的裝置對應項，並以連線資訊來更新其報告屬性。</span><span class="sxs-lookup"><span data-stu-id="0dc3b-144">The previous code, after it initializes the **Client** object, retrieves the device twin for **myDeviceId** and updates its reported property with the connectivity information.</span></span>
5. <span data-ttu-id="0dc3b-145">執行裝置應用程式</span><span class="sxs-lookup"><span data-stu-id="0dc3b-145">Run the device app</span></span>
   
        node ReportConnectivity.js
   
    <span data-ttu-id="0dc3b-146">您應該會看見訊息 `twin state reported`。</span><span class="sxs-lookup"><span data-stu-id="0dc3b-146">You should see the message `twin state reported`.</span></span>
6. <span data-ttu-id="0dc3b-147">現在，裝置已回報其連線資訊，它應該會出現在這兩個查詢中。</span><span class="sxs-lookup"><span data-stu-id="0dc3b-147">Now that the device reported its connectivity information, it should appear in both queries.</span></span> <span data-ttu-id="0dc3b-148">回到 **addtagsandqueryapp** 資料夾，並再次執行查詢︰</span><span class="sxs-lookup"><span data-stu-id="0dc3b-148">Go back in the **addtagsandqueryapp** folder and run the queries again:</span></span>
   
        node AddTagsAndQuery.js
   
    <span data-ttu-id="0dc3b-149">這次，**myDeviceId** 應該會出現在這兩個查詢結果中。</span><span class="sxs-lookup"><span data-stu-id="0dc3b-149">This time **myDeviceId** should appear in both query results.</span></span>
   
    ![][3]

## <a name="next-steps"></a><span data-ttu-id="0dc3b-150">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0dc3b-150">Next steps</span></span>
<span data-ttu-id="0dc3b-151">在此教學課程中，您在 Azure 入口網站中設定了新的 IoT 中樞，然後在 IoT 中樞的身分識別登錄中建立了裝置身分識別。</span><span class="sxs-lookup"><span data-stu-id="0dc3b-151">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="0dc3b-152">您已從後端應用程式將裝置中繼資料新增為標籤，並撰寫模擬裝置應用程式來報告裝置對應項中的裝置連線資訊。</span><span class="sxs-lookup"><span data-stu-id="0dc3b-152">You added device metadata as tags from a back-end app, and wrote a simulated device app to report device connectivity information in the device twin.</span></span> <span data-ttu-id="0dc3b-153">您也了解如何使 類似 SQL 的 IoT 中樞查詢語言來查詢此資訊。</span><span class="sxs-lookup"><span data-stu-id="0dc3b-153">You also learned how to query this information using the SQL-like IoT Hub query language.</span></span>

<span data-ttu-id="0dc3b-154">使用下列資源來了解如何：</span><span class="sxs-lookup"><span data-stu-id="0dc3b-154">Use the following resources to learn how to:</span></span>

* <span data-ttu-id="0dc3b-155">從裝置傳送遙測，請參閱[開始使用 IoT 中樞][lnk-iothub-getstarted]教學課程，</span><span class="sxs-lookup"><span data-stu-id="0dc3b-155">send telemetry from devices with the [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="0dc3b-156">使用裝置對應項的所需屬性來設定裝置，請參閱[使用所需的屬性來設定裝置][lnk-twin-how-to-configure]教學課程，</span><span class="sxs-lookup"><span data-stu-id="0dc3b-156">configure devices using device twin's desired properties with the [Use desired properties to configure devices][lnk-twin-how-to-configure] tutorial,</span></span>
* <span data-ttu-id="0dc3b-157">以互動方式控制裝置 (例如，從使用者控制的應用程式開啟風扇)，請參閱[使用直接方法][lnk-methods-tutorial]教學課程。</span><span class="sxs-lookup"><span data-stu-id="0dc3b-157">control devices interactively (such as turning on a fan from a user-controlled app), with the [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

<!-- images -->
[1]: media/iot-hub-node-node-twin-getstarted/service1.png
[3]: media/iot-hub-node-node-twin-getstarted/service2.png

<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[lnk-d2c]: iot-hub-devguide-messaging.md#device-to-cloud-messages
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-identity]: iot-hub-devguide-identity-registry.md

[lnk-iothub-getstarted]: iot-hub-node-node-getstarted.md
[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/

[lnk-twin-how-to-configure]: iot-hub-node-node-twin-how-to-configure.md
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md

[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
