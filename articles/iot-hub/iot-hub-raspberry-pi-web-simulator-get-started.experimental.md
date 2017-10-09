---
title: "aaaSimulated 覆盆子 Pi toocloud (Node.js) 的連線覆盆子 Pi web 模擬器 tooAzure IoT 中樞 |Microsoft 文件"
description: "連接覆盆子 Pi web 模擬器 tooAzure 覆盆子 Pi toosend 資料 toohello Azure 雲端的 IoT 中樞。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "木莓澆 pi 模擬器，azure iot 木莓澆 pi 木莓澆 pi iot 中樞，木莓澆 pi 傳送資料 toocloud 木莓澆 pi toocloud"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-web-simulator-get-started
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/7/2017
ms.author: xshi
ms.openlocfilehash: 0ebe1004e96ff4e64fdd1b05b7e35192ec42f7d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-raspberry-pi-online-simulator-tooazure-iot-hub-nodejs"></a><span data-ttu-id="3211e-104">連接覆盆子 Pi 線上模擬器 tooAzure IoT 中樞 (Node.js)</span><span class="sxs-lookup"><span data-stu-id="3211e-104">Connect Raspberry Pi online simulator tooAzure IoT Hub (Node.js)</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="3211e-105">在本教學課程中，您必須開始學習覆盆子 Pi 線上模擬器所使用的 hello 基本概念。</span><span class="sxs-lookup"><span data-stu-id="3211e-105">In this tutorial, you begin by learning hello basics of working with Raspberry Pi online simulator.</span></span> <span data-ttu-id="3211e-106">然後您學習如何 tooseamlessly hello Pi 模擬器 toohello 雲端使用連線[Azure IoT 中樞](iot-hub-what-is-iot-hub.md)。</span><span class="sxs-lookup"><span data-stu-id="3211e-106">You then learn how tooseamlessly connect hello Pi simulator toohello cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span> 

<span data-ttu-id="3211e-107">如果您有實體裝置，請瀏覽[連接覆盆子 Pi tooAzure IoT 中樞](iot-hub-raspberry-pi-kit-node-get-started.md)tooget 啟動。</span><span class="sxs-lookup"><span data-stu-id="3211e-107">If you have physical devices, visit [Connect Raspberry Pi tooAzure IoT Hub](iot-hub-raspberry-pi-kit-node-get-started.md) tooget started.</span></span> 

<p>
<div id="diag" style="width:100%; text-align:center">
<a href="https://azure-samples.github.io/raspberry-pi-web-simulator/#getstarted">
<img src="media/iot-hub-raspberry-pi-web-simulator/3_banner.png" alt="Connect Raspberry Pi web simulator tooAzure IoT Hub" width="400">
</div>
<p>
<div id="button" style="width:100%; text-align:center">
<a href="https://azure-samples.github.io/raspberry-pi-web-simulator/#Getstarted">
<img src="media/iot-hub-raspberry-pi-web-simulator/6_button_default.png" alt="Start Raspberry Pi simulator" width="400" onmouseover="this.src='media/iot-hub-raspberry-pi-web-simulator/5_button_click.png';" onmouseout="this.src='media/iot-hub-raspberry-pi-web-simulator/6_button_default.png';">
</div>

## <a name="what-you-do"></a><span data-ttu-id="3211e-108">您要做什麼</span><span class="sxs-lookup"><span data-stu-id="3211e-108">What you do</span></span>

* <span data-ttu-id="3211e-109">學習覆盆子 Pi 線上模擬器 hello 基本概念。</span><span class="sxs-lookup"><span data-stu-id="3211e-109">Learn hello basics of Raspberry Pi online simulator.</span></span>
* <span data-ttu-id="3211e-110">建立 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="3211e-110">Create an IoT hub.</span></span>
* <span data-ttu-id="3211e-111">在 IoT 中樞對於 Pi 註冊裝置。</span><span class="sxs-lookup"><span data-stu-id="3211e-111">Register a device for Pi in your IoT hub.</span></span>
* <span data-ttu-id="3211e-112">Pi toosend 模擬感應器資料 tooyour IoT 中樞上執行範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="3211e-112">Run a sample application on Pi toosend simulated sensor data tooyour IoT hub.</span></span>

<span data-ttu-id="3211e-113">連接模擬覆盆子 Pi tooan 的 IoT 中樞您所建立。</span><span class="sxs-lookup"><span data-stu-id="3211e-113">Connect simulated Raspberry Pi tooan IoT hub that you create.</span></span> <span data-ttu-id="3211e-114">然後您可以執行範例應用程式與 hello 模擬器 toogenerate 感應器資料。</span><span class="sxs-lookup"><span data-stu-id="3211e-114">Then you run a sample application with hello simulator toogenerate sensor data.</span></span> <span data-ttu-id="3211e-115">最後，您可以傳送 hello 感應器資料 tooyour IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="3211e-115">Finally, you send hello sensor data tooyour IoT hub.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="3211e-116">您學到什麼</span><span class="sxs-lookup"><span data-stu-id="3211e-116">What you learn</span></span>

* <span data-ttu-id="3211e-117">如何 toocreate Azure IoT 中樞，並取得新的裝置連接字串。</span><span class="sxs-lookup"><span data-stu-id="3211e-117">How toocreate an Azure IoT hub and get your new device connection string.</span></span> <span data-ttu-id="3211e-118">如果您沒有 Azure 帳戶，請花幾分鐘的時間[建立免費的 Azure 試用帳戶](https://azure.microsoft.com/free/)。</span><span class="sxs-lookup"><span data-stu-id="3211e-118">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="3211e-119">如何與覆盆子 Pi 線上模擬器 toowork。</span><span class="sxs-lookup"><span data-stu-id="3211e-119">How toowork with Raspberry Pi online simulator.</span></span>
* <span data-ttu-id="3211e-120">如何 toosend 感應器資料 tooyour IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="3211e-120">How toosend sensor data tooyour IoT hub.</span></span>

## <a name="overview-of-raspberry-pi-web-simulator"></a><span data-ttu-id="3211e-121">Raspberry Pi Web 模擬器概觀</span><span class="sxs-lookup"><span data-stu-id="3211e-121">Overview of Raspberry Pi web simulator</span></span>

<span data-ttu-id="3211e-122">按一下 [hello] 按鈕 toolaunch 覆盆子 Pi 線上模擬器。</span><span class="sxs-lookup"><span data-stu-id="3211e-122">Click hello button toolaunch Raspberry Pi online simulator.</span></span>

> [!div class="button"]
[<span data-ttu-id="3211e-123">啟動 Raspberry Pi 模擬器</span><span class="sxs-lookup"><span data-stu-id="3211e-123">Start Raspberry Pi simulator</span></span>](https://azure-samples.github.io/raspberry-pi-web-simulator/#GetStarted)

<span data-ttu-id="3211e-124">Hello web 模擬器中有三個區域。</span><span class="sxs-lookup"><span data-stu-id="3211e-124">There are three areas in hello web simulator.</span></span>
* <span data-ttu-id="3211e-125">組件範圍-Pi 連接 BME280 感應器和 LED 是 hello 預設循環。</span><span class="sxs-lookup"><span data-stu-id="3211e-125">Assembly area - hello default circuit is that a Pi connects with a BME280 sensor and an LED.</span></span> <span data-ttu-id="3211e-126">hello 區域已經鎖定在預覽版本，所以目前您無法進行自訂。</span><span class="sxs-lookup"><span data-stu-id="3211e-126">hello area is locked in preview version so currently you cannot do customization.</span></span>
* <span data-ttu-id="3211e-127">撰寫程式碼區域-toocode 覆盆子 Pi 與線上的程式碼編輯器。</span><span class="sxs-lookup"><span data-stu-id="3211e-127">Coding area - An online code editor for you toocode with Raspberry Pi.</span></span> <span data-ttu-id="3211e-128">hello 預設範例應用程式從 BME280 感應器可協助 toocollect 感應器資料，並將傳送 tooyour Azure IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="3211e-128">hello default sample application helps toocollect sensor data from BME280 sensor and sends tooyour Azure IoT Hub.</span></span> <span data-ttu-id="3211e-129">hello 應用程式是與實際 Pi 裝置完全相容。</span><span class="sxs-lookup"><span data-stu-id="3211e-129">hello application is fully compatible with real Pi devices.</span></span> 
* <span data-ttu-id="3211e-130">整合式的主控台窗口-它會顯示 hello 輸出的程式碼。</span><span class="sxs-lookup"><span data-stu-id="3211e-130">Integrated console window - It shows hello output of your code.</span></span> <span data-ttu-id="3211e-131">在這個視窗 hello 頂端，有三個按鈕。</span><span class="sxs-lookup"><span data-stu-id="3211e-131">At hello top of this window, there are three buttons.</span></span>
   * <span data-ttu-id="3211e-132">**執行**-hello 撰寫程式碼區域中執行 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="3211e-132">**Run** - Run hello application in hello coding area.</span></span>
   * <span data-ttu-id="3211e-133">**重設**-重設 hello 撰寫程式碼區域 toohello 預設範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="3211e-133">**Reset** - Reset hello coding area toohello default sample application.</span></span>
   * <span data-ttu-id="3211e-134">**摺疊/展開**-hello 右端有是一個按鈕，針對您展開 toofold/hello 主控台視窗上。</span><span class="sxs-lookup"><span data-stu-id="3211e-134">**Fold/Expand** - On hello right side there is a button for you toofold/expand hello console window.</span></span>

> [!NOTE] 
<span data-ttu-id="3211e-135">現在在預覽版本中提供 hello 覆盆子 Pi web 模擬器。</span><span class="sxs-lookup"><span data-stu-id="3211e-135">hello Raspberry Pi web simulator is now available in preview version.</span></span> <span data-ttu-id="3211e-136">我們希望 toohear 在 hello 語音[Gitter 聊天室](https://gitter.im/Microsoft/raspberry-pi-web-simulator)。</span><span class="sxs-lookup"><span data-stu-id="3211e-136">We'd like toohear your voice in hello [Gitter Chatroom](https://gitter.im/Microsoft/raspberry-pi-web-simulator).</span></span> <span data-ttu-id="3211e-137">hello 原始程式碼是 public [Github](https://github.com/Azure-Samples/raspberry-pi-web-simulator)。</span><span class="sxs-lookup"><span data-stu-id="3211e-137">hello source code is public on [Github](https://github.com/Azure-Samples/raspberry-pi-web-simulator).</span></span>

![Pi 線上模擬器概觀](media/iot-hub-raspberry-pi-web-simulator/0_overview.png)

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]


## <a name="run-a-sample-application-on-pi-web-simulator"></a><span data-ttu-id="3211e-139">在 Pi Web 模擬器上執行範例應用程式</span><span class="sxs-lookup"><span data-stu-id="3211e-139">Run a sample application on Pi web simulator</span></span>

1. <span data-ttu-id="3211e-140">在撰寫程式碼區域，請確定您在處理 hello 預設範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="3211e-140">In coding area, make sure you are working on hello default sample application.</span></span> <span data-ttu-id="3211e-141">行 15 中的 hello 預留位置取代為 hello Azure IoT 中樞裝置連接字串。</span><span class="sxs-lookup"><span data-stu-id="3211e-141">Replace hello placeholder in Line 15 with hello Azure IoT hub device connection string.</span></span>
   <span data-ttu-id="3211e-142">![取代 hello 裝置連接字串](media/iot-hub-raspberry-pi-web-simulator/1_connectionstring.png)</span><span class="sxs-lookup"><span data-stu-id="3211e-142">![Replace hello device connection string](media/iot-hub-raspberry-pi-web-simulator/1_connectionstring.png)</span></span>

2. <span data-ttu-id="3211e-143">按一下**執行**或型別`npm start`toorun hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="3211e-143">Click **Run** or type `npm start` toorun hello application.</span></span>


<span data-ttu-id="3211e-144">您應該會看到下列 hello 輸出，它會顯示 hello 感應器資料以及 tooyour IoT 中樞傳送 hello 訊息![輸出-從覆盆子 Pi tooyour IoT 中樞傳送的感應器資料](media/iot-hub-raspberry-pi-web-simulator/2_run_application.png)</span><span class="sxs-lookup"><span data-stu-id="3211e-144">You should see hello following output that shows hello sensor data and hello messages that are sent tooyour IoT hub ![Output - sensor data sent from Raspberry Pi tooyour IoT hub](media/iot-hub-raspberry-pi-web-simulator/2_run_application.png)</span></span>


## <a name="next-steps"></a><span data-ttu-id="3211e-145">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3211e-145">Next steps</span></span>

<span data-ttu-id="3211e-146">您已執行範例應用程式 toocollect 感應器資料，並將它傳送 tooyour IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="3211e-146">You’ve run a sample application toocollect sensor data and send it tooyour IoT hub.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
