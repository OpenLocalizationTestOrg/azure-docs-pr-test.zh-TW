---
title: "將 Intel Edison (節點) 連接到 Azure IoT - 第 4 課：接收訊息 | Microsoft Docs"
description: "範例應用程式會在 Edison 上執行，並監視來自 IoT 中樞的傳入訊息。 新的 Gulp 工作會從 IoT 中樞將訊息傳送到 Edison 來使 LED 閃爍。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "arduino 從 web 控制 led, arduino 透過 web 控制 led"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: bc738bf6-e38d-4024-82d7-39b6c2d4bacb
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 76ea59acd848f60663a0c821bff42166aac5823a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="run-a-sample-application-to-receive-cloud-to-device-messages"></a><span data-ttu-id="36f43-105">執行範例應用程式以接收雲端到裝置訊息</span><span class="sxs-lookup"><span data-stu-id="36f43-105">Run a sample application to receive cloud-to-device messages</span></span>
<span data-ttu-id="36f43-106">在本文中，您將在 Intel Edison 上部署範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="36f43-106">In this article, you deploy a sample application on Intel Edison.</span></span> <span data-ttu-id="36f43-107">範例應用程式會監視來自 IoT 中樞的傳入訊息。</span><span class="sxs-lookup"><span data-stu-id="36f43-107">The sample application monitors incoming messages from your IoT hub.</span></span> <span data-ttu-id="36f43-108">您也會在電腦上執行 Gulp 工作，以從 IoT 中樞將訊息傳送到 Edison。</span><span class="sxs-lookup"><span data-stu-id="36f43-108">You also run a gulp task on your computer to send messages to Edison from your IoT hub.</span></span> <span data-ttu-id="36f43-109">當範例應用程式收到訊息時，便會使 LED 閃爍。</span><span class="sxs-lookup"><span data-stu-id="36f43-109">When the sample application receives the messages, it blinks the LED.</span></span> <span data-ttu-id="36f43-110">如果您有任何問題，請在[疑難排解頁面][troubleshooting]尋求解決方案。</span><span class="sxs-lookup"><span data-stu-id="36f43-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="36f43-111">將執行的作業</span><span class="sxs-lookup"><span data-stu-id="36f43-111">What you will do</span></span>
* <span data-ttu-id="36f43-112">將範例應用程式連接到 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="36f43-112">Connect the sample application to your IoT hub.</span></span>
* <span data-ttu-id="36f43-113">部署並執行範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="36f43-113">Deploy and run the sample application.</span></span>
* <span data-ttu-id="36f43-114">從 IoT 中樞將訊息傳送到 Edison 來使 LED 閃爍。</span><span class="sxs-lookup"><span data-stu-id="36f43-114">Send messages from your IoT hub to Edison to blink the LED.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="36f43-115">學習目標</span><span class="sxs-lookup"><span data-stu-id="36f43-115">What you will learn</span></span>
<span data-ttu-id="36f43-116">在本文中，您將了解：</span><span class="sxs-lookup"><span data-stu-id="36f43-116">In this article, you will learn:</span></span>
* <span data-ttu-id="36f43-117">如何監視來自 IoT 中樞的傳入訊息。</span><span class="sxs-lookup"><span data-stu-id="36f43-117">How to monitor incoming messages from your IoT hub.</span></span>
* <span data-ttu-id="36f43-118">如何從 IoT 中樞將「雲端到裝置」訊息傳送到 Edison。</span><span class="sxs-lookup"><span data-stu-id="36f43-118">How to send cloud-to-device messages from your IoT hub to Edison.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="36f43-119">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="36f43-119">What you need</span></span>
* <span data-ttu-id="36f43-120">Intel Edison，進行設定以供使用。</span><span class="sxs-lookup"><span data-stu-id="36f43-120">Intel Edison, set up for use.</span></span> <span data-ttu-id="36f43-121">若要了解如何設定 Edison，請參閱[設定裝置][configure-your-device]。</span><span class="sxs-lookup"><span data-stu-id="36f43-121">To learn how to set up Edison, see [Configure your device][configure-your-device].</span></span>
* <span data-ttu-id="36f43-122">在您的 Azure 訂用帳戶中建立的 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="36f43-122">An IoT hub that is created in your Azure subscription.</span></span> <span data-ttu-id="36f43-123">若要了解如何建立 IoT 中樞，請參閱[建立您的 Azure IoT 中樞][create-your-azure-iot-hub]。</span><span class="sxs-lookup"><span data-stu-id="36f43-123">To learn how to create your IoT hub, see [Create your Azure IoT Hub][create-your-azure-iot-hub].</span></span>

## <a name="connect-the-sample-application-to-your-iot-hub"></a><span data-ttu-id="36f43-124">將範例應用程式連接到 IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="36f43-124">Connect the sample application to your IoT hub</span></span>
1. <span data-ttu-id="36f43-125">請確定您已位於存放庫資料夾 `iot-hub-node-edison-getting-started`。</span><span class="sxs-lookup"><span data-stu-id="36f43-125">Make sure that you're in the repo folder `iot-hub-node-edison-getting-started`.</span></span> <span data-ttu-id="36f43-126">執行下列命令來在 Visual Studio Code 中開啟範例應用程式︰</span><span class="sxs-lookup"><span data-stu-id="36f43-126">Open the sample application in Visual Studio Code by running the following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```

   <span data-ttu-id="36f43-127">`app` 子資料夾中的檔案為關鍵的來源檔案，這個來源檔案包含監視來自 IoT 中樞之傳入訊息的程式碼。</span><span class="sxs-lookup"><span data-stu-id="36f43-127">The file in the `app` subfolder is the key source file that contains the code to monitor incoming messages from the IoT hub.</span></span> <span data-ttu-id="36f43-128">`blinkLED` 函數會使 LED 閃爍。</span><span class="sxs-lookup"><span data-stu-id="36f43-128">The `blinkLED` function blinks the LED.</span></span>

   ![範例應用程式中的儲存機制結構][repo-structure]
2. <span data-ttu-id="36f43-130">執行下列命令初始化組態檔：</span><span class="sxs-lookup"><span data-stu-id="36f43-130">Initialize the configuration file by running the following commands:</span></span>

   ```bash
   npm install
   gulp init
   ```

   <span data-ttu-id="36f43-131">如果您已在此電腦上完成[建立 Azure 函式應用程式與儲存體帳戶][create-an-azure-function-app-and-storage-account]中的步驟，則會繼承所有組態，因此您可以略過部署和執行範例應用程式之工作的步驟。</span><span class="sxs-lookup"><span data-stu-id="36f43-131">If you completed the steps in [Create an Azure function app and storage account][create-an-azure-function-app-and-storage-account] on this computer, all the configurations are inherited, so you can skip the step to the task of deploying and running the sample application.</span></span> <span data-ttu-id="36f43-132">如果您是在不同電腦上完成[建立 Azure 函數應用程式與儲存體帳戶][create-an-azure-function-app-and-storage-account]中的步驟，您必須取代 `config-edison.json` 檔案中的預留位置。</span><span class="sxs-lookup"><span data-stu-id="36f43-132">If you completed the steps in [Create an Azure function app and storage account][create-an-azure-function-app-and-storage-account] on a different computer, you need to replace the placeholders in the `config-edison.json` file.</span></span> <span data-ttu-id="36f43-133">`config-edison.json` 檔案位於您主資料夾的子資料夾中。</span><span class="sxs-lookup"><span data-stu-id="36f43-133">The `config-edison.json` file is in the subfolder of your home folder.</span></span>

   ![config-edison.json 檔案的內容](media/iot-hub-intel-edison-lessons/lesson4/config-edison.png)

   * <span data-ttu-id="36f43-135">以您設定裝置時所記下的裝置 IP 位址來取代 **[device hostname or IP address]**。</span><span class="sxs-lookup"><span data-stu-id="36f43-135">Replace **[device hostname or IP address]** with the device IP address you marked down when you configured your device.</span></span>
   * <span data-ttu-id="36f43-136">以透過執行 `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` 命令所取得的裝置連接字串取代 **[IoT device connection string]**。</span><span class="sxs-lookup"><span data-stu-id="36f43-136">Replace **[IoT device connection string]** with the device connection string that you get by running the `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` command.</span></span>
   * <span data-ttu-id="36f43-137">以透過執行 `az iot hub show-connection-string --name {my hub name}` 命令所取得的 IoT 中樞連接字串取代 **[IoT hub connection string]**。</span><span class="sxs-lookup"><span data-stu-id="36f43-137">Replace **[IoT hub connection string]** with the IoT hub connection string that you get by running the `az iot hub show-connection-string --name {my hub name}` command.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="36f43-138">部署和執行範例應用程式</span><span class="sxs-lookup"><span data-stu-id="36f43-138">Deploy and run the sample application</span></span>
<span data-ttu-id="36f43-139">執行下列命令，在 Edison 上部署和執行範例應用程式：</span><span class="sxs-lookup"><span data-stu-id="36f43-139">Deploy and run the sample application on Edison by running the following commands:</span></span>

```bash
gulp deploy && gulp run
```

<span data-ttu-id="36f43-140">gulp 命令會將範例應用程式部署到 Edison。</span><span class="sxs-lookup"><span data-stu-id="36f43-140">The gulp command deploys the sample application to Edison.</span></span> <span data-ttu-id="36f43-141">然後，它會在 Edison 上執行應用程式，並在主機電腦上執行個別的工作，以從 IoT 中樞將 20 個閃爍訊息傳送到 Edison。</span><span class="sxs-lookup"><span data-stu-id="36f43-141">Then, it runs the application on Edison and a separate task on your host computer to send 20 blink messages to Edison from your IoT hub.</span></span>

<span data-ttu-id="36f43-142">在範例應用程式執行後，它便會開始接聽來自 IoT 中樞的訊息。</span><span class="sxs-lookup"><span data-stu-id="36f43-142">After the sample application runs, it starts listening to messages from your IoT hub.</span></span> <span data-ttu-id="36f43-143">同時，gulp 工作會從 IoT 中樞將數個「閃爍」訊息傳送到 Edison。</span><span class="sxs-lookup"><span data-stu-id="36f43-143">Meanwhile, the gulp task sends several "blink" messages from your IoT hub to Edison.</span></span> <span data-ttu-id="36f43-144">每當 Edison 收到閃爍訊息時，範例應用程式便會呼叫 `blinkLED` 函式來使 LED 閃爍。</span><span class="sxs-lookup"><span data-stu-id="36f43-144">For each blink message that Edison receives, the sample application calls the `blinkLED` function to blink the LED.</span></span>

<span data-ttu-id="36f43-145">當 gulp 工作從 IoT 中樞將 20 個訊息傳送到 Edison 時，LED 每兩秒應該會閃爍一次。</span><span class="sxs-lookup"><span data-stu-id="36f43-145">You should see the LED blink every two seconds as the gulp task sends 20 messages from your IoT hub to Edison.</span></span> <span data-ttu-id="36f43-146">最後將會有一個「停止」訊息，來讓應用程式停止執行。</span><span class="sxs-lookup"><span data-stu-id="36f43-146">The last one is a "stop" message that stops the application from running.</span></span>

![具有 gulp 命令和閃爍訊息的範例應用程式][gulp-command-and-blink-messages]

## <a name="summary"></a><span data-ttu-id="36f43-148">摘要</span><span class="sxs-lookup"><span data-stu-id="36f43-148">Summary</span></span>
<span data-ttu-id="36f43-149">您已成功從 IoT 中樞將訊息傳送到 Edison 來使 LED 閃爍。</span><span class="sxs-lookup"><span data-stu-id="36f43-149">You’ve successfully sent messages from your IoT hub to Edison to blink the LED.</span></span> <span data-ttu-id="36f43-150">下一個工作是「選讀：變更 LED 的開與關行為」。</span><span class="sxs-lookup"><span data-stu-id="36f43-150">The next task is optional: change the on and off behavior of the LED.</span></span>

## <a name="next-steps"></a><span data-ttu-id="36f43-151">後續步驟</span><span class="sxs-lookup"><span data-stu-id="36f43-151">Next steps</span></span>
<span data-ttu-id="36f43-152">[變更 LED 的開與關行為][change-the-on-and-off-behavior-of-the-led]</span><span class="sxs-lookup"><span data-stu-id="36f43-152">[Change the on and off behavior of the LED][change-the-on-and-off-behavior-of-the-led]</span></span>

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[configure-your-device]: iot-hub-intel-edison-kit-node-lesson1-configure-your-device.md
[create-your-azure-iot-hub]: iot-hub-intel-edison-kit-node-lesson2-prepare-azure-iot-hub.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson4/repo_structure.png
[create-an-azure-function-app-and-storage-account]: iot-hub-intel-edison-kit-node-lesson3-deploy-resource-manager-template.md
[gulp-command-and-blink-messages]: media/iot-hub-intel-edison-lessons/lesson4/gulp_blink.png
[change-the-on-and-off-behavior-of-the-led]: iot-hub-intel-edison-kit-node-lesson4-change-led-behavior.md