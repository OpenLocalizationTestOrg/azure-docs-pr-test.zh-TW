---
title: "將 Raspberry Pi (C) 連接到 Azure IoT - 第 4 課：雲端到裝置 | Microsoft Docs"
description: "範例應用程式會在 Pi 上執行，並監視從 IoT 中樞傳入的訊息。 新的 Gulp 工作會從 IoT 中樞將訊息傳送到 Pi 來使 LED 閃爍。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "雲端到裝置, 來自雲端的訊息"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: fcbc0dd0-cae3-47b0-8e58-240e4f406f75
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 86c7be931319d9995c2a7311267c7e7c03c3c1b8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="run-a-sample-application-to-receive-cloud-to-device-messages"></a><span data-ttu-id="7e507-105">執行範例應用程式以接收雲端到裝置訊息</span><span class="sxs-lookup"><span data-stu-id="7e507-105">Run a sample application to receive cloud-to-device messages</span></span>
<span data-ttu-id="7e507-106">在本文中，您將在 Raspberry Pi 3 上部署範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="7e507-106">In this article, you deploy a sample application on Raspberry Pi 3.</span></span> <span data-ttu-id="7e507-107">範例應用程式會監視來自 IoT 中樞的傳入訊息。</span><span class="sxs-lookup"><span data-stu-id="7e507-107">The sample application monitors incoming messages from your IoT hub.</span></span> <span data-ttu-id="7e507-108">您也會在電腦上執行 Gulp 工作，以從 IoT 中樞將訊息傳送到 Pi。</span><span class="sxs-lookup"><span data-stu-id="7e507-108">You also run a gulp task on your computer to send messages to Pi from your IoT hub.</span></span> <span data-ttu-id="7e507-109">當範例應用程式收到訊息時，便會使 LED 閃爍。</span><span class="sxs-lookup"><span data-stu-id="7e507-109">When the sample application receives the messages, it blinks the LED.</span></span> <span data-ttu-id="7e507-110">如果您有任何問題，請在[疑難排解頁面](iot-hub-raspberry-pi-kit-c-troubleshooting.md)尋求解決方案。</span><span class="sxs-lookup"><span data-stu-id="7e507-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="7e507-111">將執行的作業</span><span class="sxs-lookup"><span data-stu-id="7e507-111">What you will do</span></span>
* <span data-ttu-id="7e507-112">將範例應用程式連接到 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="7e507-112">Connect the sample application to your IoT hub.</span></span>
* <span data-ttu-id="7e507-113">部署並執行範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="7e507-113">Deploy and run the sample application.</span></span>
* <span data-ttu-id="7e507-114">從 IoT 中樞將訊息傳送到 Pi 來使 LED 閃爍。</span><span class="sxs-lookup"><span data-stu-id="7e507-114">Send messages from your IoT hub to Pi to blink the LED.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="7e507-115">學習目標</span><span class="sxs-lookup"><span data-stu-id="7e507-115">What you will learn</span></span>
<span data-ttu-id="7e507-116">在本文中，您將了解：</span><span class="sxs-lookup"><span data-stu-id="7e507-116">In this article, you will learn:</span></span>
* <span data-ttu-id="7e507-117">如何監視來自 IoT 中樞的傳入訊息。</span><span class="sxs-lookup"><span data-stu-id="7e507-117">How to monitor incoming messages from your IoT hub.</span></span>
* <span data-ttu-id="7e507-118">如何從 IoT 中樞將「雲端到裝置」訊息傳送到 Pi。</span><span class="sxs-lookup"><span data-stu-id="7e507-118">How to send cloud-to-device messages from your IoT hub to Pi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="7e507-119">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="7e507-119">What you need</span></span>
* <span data-ttu-id="7e507-120">Raspberry Pi 3，以完成使用設定。</span><span class="sxs-lookup"><span data-stu-id="7e507-120">Raspberry Pi 3, set up for use.</span></span> <span data-ttu-id="7e507-121">若要了解如何設定 Pi，請參閱[設定裝置](iot-hub-raspberry-pi-kit-c-lesson1-configure-your-device.md)。</span><span class="sxs-lookup"><span data-stu-id="7e507-121">To learn how to set up Pi, see [Configure your device](iot-hub-raspberry-pi-kit-c-lesson1-configure-your-device.md).</span></span>
* <span data-ttu-id="7e507-122">在您的 Azure 訂用帳戶中建立的 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="7e507-122">An IoT hub that is created in your Azure subscription.</span></span> <span data-ttu-id="7e507-123">若要了解如何建立 IoT 中樞，請參閱[建立 IoT 中樞並登錄 Raspberry Pi 3](iot-hub-raspberry-pi-kit-c-lesson2-prepare-azure-iot-hub.md)。</span><span class="sxs-lookup"><span data-stu-id="7e507-123">To learn how to create your IoT hub, see [Create your IoT hub and register Raspberry Pi 3](iot-hub-raspberry-pi-kit-c-lesson2-prepare-azure-iot-hub.md).</span></span>

## <a name="connect-the-sample-application-to-your-iot-hub"></a><span data-ttu-id="7e507-124">將範例應用程式連接到 IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="7e507-124">Connect the sample application to your IoT hub</span></span>
1. <span data-ttu-id="7e507-125">請確定您已位於存放庫資料夾 `iot-hub-c-raspberrypi-getting-started`。</span><span class="sxs-lookup"><span data-stu-id="7e507-125">Make sure that you're in the repo folder `iot-hub-c-raspberrypi-getting-started`.</span></span> <span data-ttu-id="7e507-126">執行下列命令來在 Visual Studio Code 中開啟範例應用程式︰</span><span class="sxs-lookup"><span data-stu-id="7e507-126">Open the sample application in Visual Studio Code by running the following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```

   <span data-ttu-id="7e507-127">請注意到 `app` 子資料夾中的 `app.c` 檔案。</span><span class="sxs-lookup"><span data-stu-id="7e507-127">Notice the `app.c` file in the `app` subfolder.</span></span> <span data-ttu-id="7e507-128">`app.c` 檔案為關鍵的來源檔案，這個來源檔案包含監視來自 IoT 中樞之傳入訊息的程式碼。</span><span class="sxs-lookup"><span data-stu-id="7e507-128">The `app.c` file is the key source file that contains the code to monitor incoming messages from the IoT hub.</span></span> <span data-ttu-id="7e507-129">`blinkLED` 函數會使 LED 閃爍。</span><span class="sxs-lookup"><span data-stu-id="7e507-129">The `blinkLED` function blinks the LED.</span></span>

   ![範例應用程式中的儲存機制結構](media/iot-hub-raspberry-pi-lessons/lesson4/repo_structure_c.png)
2. <span data-ttu-id="7e507-131">執行下列命令初始化組態檔：</span><span class="sxs-lookup"><span data-stu-id="7e507-131">Initialize the configuration file by running the following commands:</span></span>

   ```bash
   npm install
   gulp init
   ```

   <span data-ttu-id="7e507-132">如果您已在此電腦上完成[建立 Azure 函式應用程式和儲存體帳戶](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md)中的步驟，則會繼承所有組態，因此您可以略過部署和執行範例應用程式的工作步驟。</span><span class="sxs-lookup"><span data-stu-id="7e507-132">If you completed the steps in [Create an Azure function app and storage account](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md) on this computer, all the configurations are inherited, so you can skip to step to the task of deploying and running the sample application.</span></span> <span data-ttu-id="7e507-133">如果您已在不同電腦上完成[建立 Azure 函式應用程式與儲存體帳戶](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md)中的步驟，您必須取代 `config-raspberrypi.json` 檔案中的預留位置。</span><span class="sxs-lookup"><span data-stu-id="7e507-133">If you completed the steps in [Create an Azure function app and storage account](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md) on a different computer, you need to replace the placeholders in the `config-raspberrypi.json` file.</span></span> <span data-ttu-id="7e507-134">`config-raspberrypi.json` 檔案位於您主資料夾的子資料夾中。</span><span class="sxs-lookup"><span data-stu-id="7e507-134">The `config-raspberrypi.json` file is in the subfolder of your home folder.</span></span>

   ![config-raspberrypi.json 檔案的內容](media/iot-hub-raspberry-pi-lessons/lesson4/config_raspberrypi.png)

* <span data-ttu-id="7e507-136">以您執行 `devdisco list --eth` 命令所取得的 Pi IP 位址或主機名稱，取代 **device hostname or IP address]**。</span><span class="sxs-lookup"><span data-stu-id="7e507-136">Replace **[device hostname or IP address]** with Pi’s IP address or host name that you get by running the `devdisco list --eth` command.</span></span>
* <span data-ttu-id="7e507-137">以透過執行 `az iot device show-connection-string --hub-name {my hub name} --device-id {device id} -g iot-sample {resource group name}` 命令所取得的裝置連接字串取代 **[IoT device connection string]**。</span><span class="sxs-lookup"><span data-stu-id="7e507-137">Replace **[IoT device connection string]** with the device connection string that you get by running the `az iot device show-connection-string --hub-name {my hub name} --device-id {device id} -g iot-sample {resource group name}` command.</span></span>
* <span data-ttu-id="7e507-138">以透過執行 `az iot hub show-connection-string --name {my hub name} -g iot-sample {resource group name}` 命令所取得的 IoT 中樞連接字串取代 **[IoT hub connection string]**。</span><span class="sxs-lookup"><span data-stu-id="7e507-138">Replace **[IoT hub connection string]** with the IoT hub connection string that you get by running the `az iot hub show-connection-string --name {my hub name} -g iot-sample {resource group name}` command.</span></span>

> [!NOTE]
> <span data-ttu-id="7e507-139">也請執行 **gulp install-tools** (如果您未在第 1 課這麼做)。</span><span class="sxs-lookup"><span data-stu-id="7e507-139">Run **gulp install-tools** as well, if you haven't done it in Lesson 1.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="7e507-140">部署和執行範例應用程式</span><span class="sxs-lookup"><span data-stu-id="7e507-140">Deploy and run the sample application</span></span>
<span data-ttu-id="7e507-141">執行下列命令，在 Pi 上部署和執行範例應用程式：</span><span class="sxs-lookup"><span data-stu-id="7e507-141">Deploy and run the sample application on Pi by running the following commands:</span></span>

```
gulp deploy && gulp run
```

<span data-ttu-id="7e507-142">Gulp 命令會先執行 install-tools 工作。</span><span class="sxs-lookup"><span data-stu-id="7e507-142">The gulp command runs the install-tools task first.</span></span> <span data-ttu-id="7e507-143">接著會將範例應用程式部署至 Pi。</span><span class="sxs-lookup"><span data-stu-id="7e507-143">Then it deploys the sample application to Pi.</span></span> <span data-ttu-id="7e507-144">最後，它會在 Pi 上執行應用程式，並在主機電腦上執行個別的工作，以從 IoT 中樞將 20 個閃爍訊息傳送至 Pi。</span><span class="sxs-lookup"><span data-stu-id="7e507-144">Finally, it runs the application on Pi and a separate task on your host computer to send 20 blink messages to Pi from your IoT hub.</span></span>

<span data-ttu-id="7e507-145">在範例應用程式執行後，它便會開始接聽來自 IoT 中樞的訊息。</span><span class="sxs-lookup"><span data-stu-id="7e507-145">After the sample application runs, it starts listening to messages from your IoT hub.</span></span> <span data-ttu-id="7e507-146">同時，gulp 工作會從 IoT 中樞將數個「閃爍」訊息傳送到 Pi。</span><span class="sxs-lookup"><span data-stu-id="7e507-146">Meanwhile, the gulp task sends several "blink" messages from your IoT hub to Pi.</span></span> <span data-ttu-id="7e507-147">每當 Pi 收到閃爍訊息時，範例應用程式便會呼叫 `blinkLED` 函式來使 LED 閃爍。</span><span class="sxs-lookup"><span data-stu-id="7e507-147">For each blink message that Pi receives, the sample application calls the `blinkLED` function to blink the LED.</span></span>

<span data-ttu-id="7e507-148">當 gulp 工作從 IoT 中樞將 20 個訊息傳送到 Pi 時，LED 每兩秒應該會閃爍一次。</span><span class="sxs-lookup"><span data-stu-id="7e507-148">You should see the LED blink every two seconds as the gulp task sends 20 messages from your IoT hub to Pi.</span></span> <span data-ttu-id="7e507-149">最後將會有一個「停止」訊息，讓應用程式停止執行。</span><span class="sxs-lookup"><span data-stu-id="7e507-149">The last one is a "stop" message that stops the application from running.</span></span>

![具有 gulp 命令和閃爍訊息的範例應用程式](media/iot-hub-raspberry-pi-lessons/lesson4/gulp_blink_c.png)

## <a name="summary"></a><span data-ttu-id="7e507-151">摘要</span><span class="sxs-lookup"><span data-stu-id="7e507-151">Summary</span></span>
<span data-ttu-id="7e507-152">您已成功從 IoT 中樞將訊息傳送到 Pi 來使 LED 閃爍。</span><span class="sxs-lookup"><span data-stu-id="7e507-152">You’ve successfully sent messages from your IoT hub to Pi to blink the LED.</span></span> <span data-ttu-id="7e507-153">下一個工作是「選讀：變更 LED 的開與關行為」。</span><span class="sxs-lookup"><span data-stu-id="7e507-153">The next task is optional: change the on and off behavior of the LED.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7e507-154">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7e507-154">Next steps</span></span>
[<span data-ttu-id="7e507-155">變更 LED 的開與關行為</span><span class="sxs-lookup"><span data-stu-id="7e507-155">Change the on and off behavior of the LED</span></span>](iot-hub-raspberry-pi-kit-c-lesson4-change-led-behavior.md)