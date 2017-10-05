---
title: "模擬 Raspberry Pi 至 cloud (Node.js) - 將 Raspberry Pi Web 模擬器連線至 Azure IoT 中樞 | Microsoft Docs"
description: "將 Raspberry Pi Web 模擬器連線至 Azure IoT Hub，以便 Raspberry Pi 將資料傳送至 Azure 雲端。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "raspberry pi 模擬器, azure iot raspberry pi, raspberry pi iot 中樞, raspberry pi 將資料傳送至雲端, raspberry pi 至 cloud"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-web-simulator-get-started
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/7/2017
ms.author: xshi
ms.openlocfilehash: 5b7e209b65ccf6edb32d211797663e5e5b170df8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="connect-raspberry-pi-online-simulator-to-azure-iot-hub-nodejs"></a><span data-ttu-id="b3db2-104">將 Raspberry Pi 線上模擬器連線至 Azure IoT Hub (Node.js)</span><span class="sxs-lookup"><span data-stu-id="b3db2-104">Connect Raspberry Pi online simulator to Azure IoT Hub (Node.js)</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="b3db2-105">在本教學課程中，您首先會了解使用 Raspberry Pi 線上模擬器的基本知識。</span><span class="sxs-lookup"><span data-stu-id="b3db2-105">In this tutorial, you begin by learning the basics of working with Raspberry Pi online simulator.</span></span> <span data-ttu-id="b3db2-106">接著會了解如何使用 [Azure IoT 中樞](iot-hub-what-is-iot-hub.md)順暢地將 Pi 模擬器連線至雲端。</span><span class="sxs-lookup"><span data-stu-id="b3db2-106">You then learn how to seamlessly connect the Pi simulator to the cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span> 

<span data-ttu-id="b3db2-107">如果您有實體裝置，請瀏覽[將 Raspberry Pi 連線至 Azure IoT 中樞](iot-hub-raspberry-pi-kit-node-get-started.md)開始著手。</span><span class="sxs-lookup"><span data-stu-id="b3db2-107">If you have physical devices, visit [Connect Raspberry Pi to Azure IoT Hub](iot-hub-raspberry-pi-kit-node-get-started.md) to get started.</span></span> 

<p>
<div id="diag" style="width:100%; text-align:center">
<a href="https://azure-samples.github.io/raspberry-pi-web-simulator/#getstarted">
<img src="media/iot-hub-raspberry-pi-web-simulator/3_banner.png" alt="Connect Raspberry Pi web simulator to Azure IoT Hub" width="400">
</div>
<p>
<div id="button" style="width:100%; text-align:center">
<a href="https://azure-samples.github.io/raspberry-pi-web-simulator/#Getstarted">
<img src="media/iot-hub-raspberry-pi-web-simulator/6_button_default.png" alt="Start Raspberry Pi simulator" width="400" onmouseover="this.src='media/iot-hub-raspberry-pi-web-simulator/5_button_click.png';" onmouseout="this.src='media/iot-hub-raspberry-pi-web-simulator/6_button_default.png';">
</div>

## <a name="what-you-do"></a><span data-ttu-id="b3db2-108">您要做什麼</span><span class="sxs-lookup"><span data-stu-id="b3db2-108">What you do</span></span>

* <span data-ttu-id="b3db2-109">了解 Raspberry Pi 線上模擬器的基本知識。</span><span class="sxs-lookup"><span data-stu-id="b3db2-109">Learn the basics of Raspberry Pi online simulator.</span></span>
* <span data-ttu-id="b3db2-110">建立 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="b3db2-110">Create an IoT hub.</span></span>
* <span data-ttu-id="b3db2-111">在 IoT 中樞對於 Pi 註冊裝置。</span><span class="sxs-lookup"><span data-stu-id="b3db2-111">Register a device for Pi in your IoT hub.</span></span>
* <span data-ttu-id="b3db2-112">在 Pi 上執行範例應用程式，將模擬感應器資料傳送至 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="b3db2-112">Run a sample application on Pi to send simulated sensor data to your IoT hub.</span></span>

<span data-ttu-id="b3db2-113">將模擬 Raspberry Pi 連線至您建立的 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="b3db2-113">Connect simulated Raspberry Pi to an IoT hub that you create.</span></span> <span data-ttu-id="b3db2-114">然後使用模擬器執行範例應用程式，以產生感應器資料。</span><span class="sxs-lookup"><span data-stu-id="b3db2-114">Then you run a sample application with the simulator to generate sensor data.</span></span> <span data-ttu-id="b3db2-115">最後，將感應器資料傳送至 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="b3db2-115">Finally, you send the sensor data to your IoT hub.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="b3db2-116">您學到什麼</span><span class="sxs-lookup"><span data-stu-id="b3db2-116">What you learn</span></span>

* <span data-ttu-id="b3db2-117">如何建立 Azure IoT 中樞，並取得新的裝置連接字串。</span><span class="sxs-lookup"><span data-stu-id="b3db2-117">How to create an Azure IoT hub and get your new device connection string.</span></span> <span data-ttu-id="b3db2-118">如果您沒有 Azure 帳戶，請花幾分鐘的時間[建立免費的 Azure 試用帳戶](https://azure.microsoft.com/free/)。</span><span class="sxs-lookup"><span data-stu-id="b3db2-118">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="b3db2-119">如何使用 Raspberry Pi 線上模擬器。</span><span class="sxs-lookup"><span data-stu-id="b3db2-119">How to work with Raspberry Pi online simulator.</span></span>
* <span data-ttu-id="b3db2-120">如何將感應器資料傳送至 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="b3db2-120">How to send sensor data to your IoT hub.</span></span>

## <a name="overview-of-raspberry-pi-web-simulator"></a><span data-ttu-id="b3db2-121">Raspberry Pi Web 模擬器概觀</span><span class="sxs-lookup"><span data-stu-id="b3db2-121">Overview of Raspberry Pi web simulator</span></span>

<span data-ttu-id="b3db2-122">按一下按鈕以啟動 Raspberry Pi 線上模擬器。</span><span class="sxs-lookup"><span data-stu-id="b3db2-122">Click the button to launch Raspberry Pi online simulator.</span></span>

> [!div class="button"]
[<span data-ttu-id="b3db2-123">啟動 Raspberry Pi 模擬器</span><span class="sxs-lookup"><span data-stu-id="b3db2-123">Start Raspberry Pi simulator</span></span>](https://azure-samples.github.io/raspberry-pi-web-simulator/#GetStarted)

<span data-ttu-id="b3db2-124">Web 模擬器中有三個區域。</span><span class="sxs-lookup"><span data-stu-id="b3db2-124">There are three areas in the web simulator.</span></span>
* <span data-ttu-id="b3db2-125">組件區域 - 預設線路是 Pi 與 BME280 感應器和 LED 連線。</span><span class="sxs-lookup"><span data-stu-id="b3db2-125">Assembly area - The default circuit is that a Pi connects with a BME280 sensor and an LED.</span></span> <span data-ttu-id="b3db2-126">此區域已在預覽版本中鎖定，所以您目前無法進行自訂。</span><span class="sxs-lookup"><span data-stu-id="b3db2-126">The area is locked in preview version so currently you cannot do customization.</span></span>
* <span data-ttu-id="b3db2-127">編碼區域 - 可供您使用 Raspberry Pi 編碼的線上程式碼編輯器。</span><span class="sxs-lookup"><span data-stu-id="b3db2-127">Coding area - An online code editor for you to code with Raspberry Pi.</span></span> <span data-ttu-id="b3db2-128">預設範例應用程式有助於從 BME280 感應器收集感應器資料，並傳送至您的 Azure IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="b3db2-128">The default sample application helps to collect sensor data from BME280 sensor and sends to your Azure IoT Hub.</span></span> <span data-ttu-id="b3db2-129">應用程式與實際 Pi 裝置完全相容。</span><span class="sxs-lookup"><span data-stu-id="b3db2-129">The application is fully compatible with real Pi devices.</span></span> 
* <span data-ttu-id="b3db2-130">整合式主控台視窗 - 它會顯示您的程式碼輸出。</span><span class="sxs-lookup"><span data-stu-id="b3db2-130">Integrated console window - It shows the output of your code.</span></span> <span data-ttu-id="b3db2-131">在這個視窗頂端，有三個按鈕。</span><span class="sxs-lookup"><span data-stu-id="b3db2-131">At the top of this window, there are three buttons.</span></span>
   * <span data-ttu-id="b3db2-132">**執行** - 在編碼區域中執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="b3db2-132">**Run** - Run the application in the coding area.</span></span>
   * <span data-ttu-id="b3db2-133">**重設** - 將編碼區域重設為預設範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="b3db2-133">**Reset** - Reset the coding area to the default sample application.</span></span>
   * <span data-ttu-id="b3db2-134">**摺疊/展開** - 右邊有一個可供您摺疊/展開主控台視窗的按鈕。</span><span class="sxs-lookup"><span data-stu-id="b3db2-134">**Fold/Expand** - On the right side there is a button for you to fold/expand the console window.</span></span>

> [!NOTE] 
<span data-ttu-id="b3db2-135">預覽版本現在提供 Raspberry Pi Web 模擬器。</span><span class="sxs-lookup"><span data-stu-id="b3db2-135">The Raspberry Pi web simulator is now available in preview version.</span></span> <span data-ttu-id="b3db2-136">我們想要在 [Gitter 聊天室](https://gitter.im/Microsoft/raspberry-pi-web-simulator)中傾聽您的心聲。</span><span class="sxs-lookup"><span data-stu-id="b3db2-136">We'd like to hear your voice in the [Gitter Chatroom](https://gitter.im/Microsoft/raspberry-pi-web-simulator).</span></span> <span data-ttu-id="b3db2-137">原始程式碼公開於 [GitHub](https://github.com/Azure-Samples/raspberry-pi-web-simulator)。</span><span class="sxs-lookup"><span data-stu-id="b3db2-137">The source code is public on [Github](https://github.com/Azure-Samples/raspberry-pi-web-simulator).</span></span>

![Pi 線上模擬器概觀](media/iot-hub-raspberry-pi-web-simulator/0_overview.png)

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]


## <a name="run-a-sample-application-on-pi-web-simulator"></a><span data-ttu-id="b3db2-139">在 Pi Web 模擬器上執行範例應用程式</span><span class="sxs-lookup"><span data-stu-id="b3db2-139">Run a sample application on Pi web simulator</span></span>

1. <span data-ttu-id="b3db2-140">在編碼區域中，確定您是使用預設範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="b3db2-140">In coding area, make sure you are working on the default sample application.</span></span> <span data-ttu-id="b3db2-141">以 Azure IoT 中樞裝置連接字串取代行 15 中的預留位置。</span><span class="sxs-lookup"><span data-stu-id="b3db2-141">Replace the placeholder in Line 15 with the Azure IoT hub device connection string.</span></span>
   <span data-ttu-id="b3db2-142">![取代裝置連接字串](media/iot-hub-raspberry-pi-web-simulator/1_connectionstring.png)</span><span class="sxs-lookup"><span data-stu-id="b3db2-142">![Replace the device connection string](media/iot-hub-raspberry-pi-web-simulator/1_connectionstring.png)</span></span>

2. <span data-ttu-id="b3db2-143">按一下 [執行] 或輸入 `npm start` 以執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="b3db2-143">Click **Run** or type `npm start` to run the application.</span></span>


<span data-ttu-id="b3db2-144">您應該會看見下列輸出，顯示傳送至 IoT 中樞的感應器資料和訊息 ![輸出 - 從 Raspberry Pi 傳送至 IoT 中樞的感應器資料](media/iot-hub-raspberry-pi-web-simulator/2_run_application.png)</span><span class="sxs-lookup"><span data-stu-id="b3db2-144">You should see the following output that shows the sensor data and the messages that are sent to your IoT hub ![Output - sensor data sent from Raspberry Pi to your IoT hub](media/iot-hub-raspberry-pi-web-simulator/2_run_application.png)</span></span>


## <a name="next-steps"></a><span data-ttu-id="b3db2-145">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b3db2-145">Next steps</span></span>

<span data-ttu-id="b3db2-146">您已執行範例應用程式收集感應器資料並傳送至 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="b3db2-146">You’ve run a sample application to collect sensor data and send it to your IoT hub.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
