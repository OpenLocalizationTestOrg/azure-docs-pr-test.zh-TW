---
featureFlags: usabilla
title: "連接覆盆子 Pi （節點） tooAzure IoT-第 4 課： 雲端到裝置 |Microsoft 文件"
description: "hello 範例應用程式在 Pi 上執行，並監視從 IoT 中樞的內送訊息。 新的 gulp 工作會從您的 IoT 中樞 tooblink hello LED 傳送訊息 tooPi。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "雲端 toodevice，來自雲端的訊息"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 6ae6539e-1163-4490-8d72-fdf7803e3054
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: d69ded4e30c27378481ab2a4fb9c5b73be7bd44e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="run-hello-sample-application-tooreceive-cloud-to-device-messages"></a><span data-ttu-id="96686-105">執行 hello 範例應用程式 tooreceive 雲端到裝置訊息</span><span class="sxs-lookup"><span data-stu-id="96686-105">Run hello sample application tooreceive cloud-to-device messages</span></span>
<span data-ttu-id="96686-106">在本文中，您將在 Raspberry Pi 3 上部署範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="96686-106">In this article, you deploy a sample application on Raspberry Pi 3.</span></span> <span data-ttu-id="96686-107">hello 範例應用程式監視從 IoT 中樞的內送訊息。</span><span class="sxs-lookup"><span data-stu-id="96686-107">hello sample application monitors incoming messages from your IoT hub.</span></span> <span data-ttu-id="96686-108">您也 gulp 工作上執行您的電腦 toosend 訊息 tooPi 從 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="96686-108">You also run a gulp task on your computer toosend messages tooPi from your IoT hub.</span></span> <span data-ttu-id="96686-109">當 hello 範例應用程式收到 hello 訊息時，它會閃爍 hello LED。</span><span class="sxs-lookup"><span data-stu-id="96686-109">When hello sample application receives hello messages, it blinks hello LED.</span></span> <span data-ttu-id="96686-110">如果您有任何問題，搜尋解決方案 hello[疑難排解頁面](iot-hub-raspberry-pi-kit-node-troubleshooting.md)。</span><span class="sxs-lookup"><span data-stu-id="96686-110">If you have any problems, seek solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="96686-111">將執行的作業</span><span class="sxs-lookup"><span data-stu-id="96686-111">What you will do</span></span>
* <span data-ttu-id="96686-112">連接 hello 範例應用程式 tooyour IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="96686-112">Connect hello sample application tooyour IoT hub.</span></span>
* <span data-ttu-id="96686-113">部署和執行 hello 範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="96686-113">Deploy and run hello sample application.</span></span>
* <span data-ttu-id="96686-114">從您 IoT 中樞 tooPi tooblink hello LED 傳送訊息。</span><span class="sxs-lookup"><span data-stu-id="96686-114">Send messages from your IoT hub tooPi tooblink hello LED.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="96686-115">學習目標</span><span class="sxs-lookup"><span data-stu-id="96686-115">What you will learn</span></span>
<span data-ttu-id="96686-116">在本文中，您將了解：</span><span class="sxs-lookup"><span data-stu-id="96686-116">In this article, you will learn:</span></span>
* <span data-ttu-id="96686-117">從您的 IoT 中樞 toomonitor 傳入訊息的方式</span><span class="sxs-lookup"><span data-stu-id="96686-117">How toomonitor incoming messages from your IoT hub</span></span>
* <span data-ttu-id="96686-118">如何從您的 IoT 中樞 tooPi 訊息 toosend 雲端到裝置。</span><span class="sxs-lookup"><span data-stu-id="96686-118">How toosend cloud-to-device messages from your IoT hub tooPi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="96686-119">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="96686-119">What you need</span></span>
* <span data-ttu-id="96686-120">Raspberry Pi 3，以完成使用設定。</span><span class="sxs-lookup"><span data-stu-id="96686-120">Raspberry Pi 3, set up for use.</span></span> <span data-ttu-id="96686-121">如何 tooset 向上 Pi，請參閱的 toolearn[設定您的裝置](iot-hub-raspberry-pi-kit-node-lesson1-configure-your-device.md)。</span><span class="sxs-lookup"><span data-stu-id="96686-121">toolearn how tooset up Pi, see [Configure your device](iot-hub-raspberry-pi-kit-node-lesson1-configure-your-device.md).</span></span>
* <span data-ttu-id="96686-122">在您的 Azure 訂用帳戶中建立的 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="96686-122">An IoT hub that is created in your Azure subscription.</span></span> <span data-ttu-id="96686-123">toolearn 如何 toocreate IoT 中樞，請參閱[建立 IoT 中樞，並註冊覆盆子 Pi 3](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md)。</span><span class="sxs-lookup"><span data-stu-id="96686-123">toolearn how toocreate your IoT hub, see [Create your IoT hub and register Raspberry Pi 3](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md).</span></span>

## <a name="connect-hello-sample-application-tooyour-iot-hub"></a><span data-ttu-id="96686-124">連接 hello 範例應用程式 tooyour IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="96686-124">Connect hello sample application tooyour IoT hub</span></span>
1. <span data-ttu-id="96686-125">請確定您是在 hello 儲存機制資料夾`iot-hub-node-raspberrypi-getting-started`。</span><span class="sxs-lookup"><span data-stu-id="96686-125">Make sure that you're in hello repo folder `iot-hub-node-raspberrypi-getting-started`.</span></span> <span data-ttu-id="96686-126">開啟 Visual Studio 程式碼中的 hello 範例應用程式，藉由執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="96686-126">Open hello sample application in Visual Studio Code by running hello following commands:</span></span>
   
   ```bash
   cd Lesson4
   code .
   ```
   
   <span data-ttu-id="96686-127">請注意 hello`app.js`檔案在 hello`app`子資料夾。</span><span class="sxs-lookup"><span data-stu-id="96686-127">Notice hello `app.js` file in hello `app` subfolder.</span></span> <span data-ttu-id="96686-128">hello`app.js`檔案是 hello 金鑰來源檔案，其中包含從 hello IoT 中樞的 hello 碼 toomonitor 內送訊息。</span><span class="sxs-lookup"><span data-stu-id="96686-128">hello `app.js` file is hello key source file that contains hello code toomonitor incoming messages from hello IoT hub.</span></span> <span data-ttu-id="96686-129">hello`blinkLED`函式會閃爍 hello LED。</span><span class="sxs-lookup"><span data-stu-id="96686-129">hello `blinkLED` function blinks hello LED.</span></span>
   
   ![Hello 範例應用程式中的儲存機制結構](media/iot-hub-raspberry-pi-lessons/lesson4/repo_structure.png)
2. <span data-ttu-id="96686-131">使用下列命令的 hello 初始化 hello 設定檔：</span><span class="sxs-lookup"><span data-stu-id="96686-131">Initialize hello configuration file by using hello following commands:</span></span>
   
   ```bash
   npm install
   gulp init
   ```
   
   <span data-ttu-id="96686-132">如果您已完成中的 hello 步驟[建立 Azure 的函式應用程式和儲存體帳戶](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md)此電腦上所有的 hello 組態繼承的因此您可以略過部署和執行 hello 範例應用程式的 toohello 工作。</span><span class="sxs-lookup"><span data-stu-id="96686-132">If you completed hello steps in [Create an Azure function app and storage account](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md) on this computer, all hello configurations are inherited, so you can skip toohello task of deploying and running hello sample application.</span></span> <span data-ttu-id="96686-133">如果您已完成中的 hello 步驟[建立 Azure 的函式應用程式和儲存體帳戶](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md)不同電腦上，您需要在 hello tooreplace hello 預留位置`config-raspberrypi.json`檔案。</span><span class="sxs-lookup"><span data-stu-id="96686-133">If you completed hello steps in [Create an Azure function app and storage account](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md) on a different computer, you need tooreplace hello placeholders in hello `config-raspberrypi.json` file.</span></span> <span data-ttu-id="96686-134">hello`config-raspberrypi.json`檔案是在主資料夾 hello 子資料夾。</span><span class="sxs-lookup"><span data-stu-id="96686-134">hello `config-raspberrypi.json` file is in hello subfolder of your home folder.</span></span>
   
   ![Hello config raspberrypi.json 檔案的內容](media/iot-hub-raspberry-pi-lessons/lesson4/config_raspberrypi.png)

* <span data-ttu-id="96686-136">取代**[裝置的主機名稱或 IP 位址]** Pi 或 hello 主機名稱，您會得到執行 hello hello IP 位址與`devdisco list --eth`命令。</span><span class="sxs-lookup"><span data-stu-id="96686-136">Replace **[device hostname or IP address]** with hello IP address of Pi or hello host name that you get by running hello `devdisco list --eth` command.</span></span>
* <span data-ttu-id="96686-137">取代**[IoT 裝置連接字串]** hello 裝置連接字串，您會得到執行 hello`az iot device show-connection-string --hub-name {my hub name} --device-id {device id} -g iot-sample {resource group name}`命令。</span><span class="sxs-lookup"><span data-stu-id="96686-137">Replace **[IoT device connection string]** with hello device connection string that you get by running hello `az iot device show-connection-string --hub-name {my hub name} --device-id {device id} -g iot-sample {resource group name}` command.</span></span>
* <span data-ttu-id="96686-138">取代**[IoT 中樞連接字串]**以 hello IoT 中樞連接字串，您會得到執行 hello`az iot hub show-connection-string --name {my hub name} -g iot-sample {resource group name}`命令。</span><span class="sxs-lookup"><span data-stu-id="96686-138">Replace **[IoT hub connection string]** with hello IoT hub connection string that you get by running hello `az iot hub show-connection-string --name {my hub name} -g iot-sample {resource group name}` command.</span></span>

> [!NOTE]
> <span data-ttu-id="96686-139">也請執行 **gulp install-tools** (如果您未在第 1 課這麼做)。</span><span class="sxs-lookup"><span data-stu-id="96686-139">Run **gulp install-tools** as well, if you haven't done it in Lesson 1.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="96686-140">部署和執行 hello 範例應用程式</span><span class="sxs-lookup"><span data-stu-id="96686-140">Deploy and run hello sample application</span></span>
<span data-ttu-id="96686-141">部署和執行 pi 的 hello 範例應用程式，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="96686-141">Deploy and run hello sample application on Pi by running hello following command:</span></span>

```bash
gulp deploy && gulp run
```

<span data-ttu-id="96686-142">hello 命令會將部署 hello 範例應用程式 tooPi。</span><span class="sxs-lookup"><span data-stu-id="96686-142">hello command deploys hello sample application tooPi.</span></span> <span data-ttu-id="96686-143">然後，它 hello 應用程式上執行 Pi 和您的主機上的個別工作電腦 toosend 20 閃爍訊息 tooPi 從 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="96686-143">Then, it runs hello application on Pi and a separate task on your host computer toosend 20 blink messages tooPi from your IoT hub.</span></span>

<span data-ttu-id="96686-144">Hello 範例應用程式執行之後，它會啟動接聽 toomessages 從 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="96686-144">After hello sample application runs, it starts listening toomessages from your IoT hub.</span></span> <span data-ttu-id="96686-145">同時，hello gulp 工作會從您的 IoT 中樞 tooPi 傳送"閃爍 」 的數個訊息。</span><span class="sxs-lookup"><span data-stu-id="96686-145">Meanwhile, hello gulp task sends several "blink" messages from your IoT hub tooPi.</span></span> <span data-ttu-id="96686-146">每個閃爍訊息接收 Pi hello 範例應用程式呼叫 hello`blinkLED`函式 tooblink hello LED。</span><span class="sxs-lookup"><span data-stu-id="96686-146">For each blink message that Pi receives, hello sample application calls hello `blinkLED` function tooblink hello LED.</span></span>

<span data-ttu-id="96686-147">您應該會看到的 gulp 工作傳送 20 則訊息從您的 IoT 中樞 tooPi hello LED 閃爍 hello 為每隔兩秒鐘。</span><span class="sxs-lookup"><span data-stu-id="96686-147">You should see hello LED blink every two seconds as hello gulp task sends 20 messages from your IoT hub tooPi.</span></span> <span data-ttu-id="96686-148">hello 最後是 「 停止 」 的訊息，告知 hello 應用程式 toostop 執行。</span><span class="sxs-lookup"><span data-stu-id="96686-148">hello last one is a "stop" message that tells hello application toostop running.</span></span>

![具有 gulp 命令和閃爍訊息的範例應用程式](media/iot-hub-raspberry-pi-lessons/lesson4/gulp_blink.png)

## <a name="summary"></a><span data-ttu-id="96686-150">摘要</span><span class="sxs-lookup"><span data-stu-id="96686-150">Summary</span></span>
<span data-ttu-id="96686-151">您已成功傳送訊息，從您 IoT 中樞 tooPi tooblink hello LED。</span><span class="sxs-lookup"><span data-stu-id="96686-151">You’ve successfully sent messages from your IoT hub tooPi tooblink hello LED.</span></span> <span data-ttu-id="96686-152">是選擇性的 hello 下一項工作： 變更 hello 開啟和關閉 hello LED 的行為。</span><span class="sxs-lookup"><span data-stu-id="96686-152">hello next task is optional: change hello on and off behavior of hello LED.</span></span>

## <a name="next-steps"></a><span data-ttu-id="96686-153">後續步驟</span><span class="sxs-lookup"><span data-stu-id="96686-153">Next steps</span></span>
[<span data-ttu-id="96686-154">變更 hello 開啟和關閉 hello LED 的行為</span><span class="sxs-lookup"><span data-stu-id="96686-154">Change hello on and off behavior of hello LED</span></span>](iot-hub-raspberry-pi-kit-node-lesson4-change-led-behavior.md)

