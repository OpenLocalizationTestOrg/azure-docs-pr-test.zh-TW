---
title: "連接 （節點） 的 Intel Edison tooAzure IoT-第 4 課： 接收訊息 |Microsoft 文件"
description: "範例應用程式會在 Edison 上執行，並監視來自 IoT 中樞的傳入訊息。 新的 gulp 工作會從您的 IoT 中樞 tooblink hello LED 傳送訊息 tooEdison。"
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
ms.openlocfilehash: aab0ced4810dd3d4f5ba636940b06563f1db9241
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-tooreceive-cloud-to-device-messages"></a><span data-ttu-id="98e80-105">執行範例應用程式 tooreceive 雲端到裝置訊息</span><span class="sxs-lookup"><span data-stu-id="98e80-105">Run a sample application tooreceive cloud-to-device messages</span></span>
<span data-ttu-id="98e80-106">在本文中，您將在 Intel Edison 上部署範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="98e80-106">In this article, you deploy a sample application on Intel Edison.</span></span> <span data-ttu-id="98e80-107">hello 範例應用程式監視從 IoT 中樞的內送訊息。</span><span class="sxs-lookup"><span data-stu-id="98e80-107">hello sample application monitors incoming messages from your IoT hub.</span></span> <span data-ttu-id="98e80-108">您也 gulp 工作上執行您的電腦 toosend 訊息 tooEdison 從 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="98e80-108">You also run a gulp task on your computer toosend messages tooEdison from your IoT hub.</span></span> <span data-ttu-id="98e80-109">當 hello 範例應用程式收到 hello 訊息時，它會閃爍 hello LED。</span><span class="sxs-lookup"><span data-stu-id="98e80-109">When hello sample application receives hello messages, it blinks hello LED.</span></span> <span data-ttu-id="98e80-110">如果您有任何問題，尋找解決方案上 hello[疑難排解頁面][troubleshooting]。</span><span class="sxs-lookup"><span data-stu-id="98e80-110">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="98e80-111">將執行的作業</span><span class="sxs-lookup"><span data-stu-id="98e80-111">What you will do</span></span>
* <span data-ttu-id="98e80-112">連接 hello 範例應用程式 tooyour IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="98e80-112">Connect hello sample application tooyour IoT hub.</span></span>
* <span data-ttu-id="98e80-113">部署和執行 hello 範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="98e80-113">Deploy and run hello sample application.</span></span>
* <span data-ttu-id="98e80-114">從您 IoT 中樞 tooEdison tooblink hello LED 傳送訊息。</span><span class="sxs-lookup"><span data-stu-id="98e80-114">Send messages from your IoT hub tooEdison tooblink hello LED.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="98e80-115">學習目標</span><span class="sxs-lookup"><span data-stu-id="98e80-115">What you will learn</span></span>
<span data-ttu-id="98e80-116">在本文中，您將了解：</span><span class="sxs-lookup"><span data-stu-id="98e80-116">In this article, you will learn:</span></span>
* <span data-ttu-id="98e80-117">如何 toomonitor 傳入訊息從 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="98e80-117">How toomonitor incoming messages from your IoT hub.</span></span>
* <span data-ttu-id="98e80-118">如何從您的 IoT 中樞 tooEdison 訊息 toosend 雲端到裝置。</span><span class="sxs-lookup"><span data-stu-id="98e80-118">How toosend cloud-to-device messages from your IoT hub tooEdison.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="98e80-119">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="98e80-119">What you need</span></span>
* <span data-ttu-id="98e80-120">Intel Edison，進行設定以供使用。</span><span class="sxs-lookup"><span data-stu-id="98e80-120">Intel Edison, set up for use.</span></span> <span data-ttu-id="98e80-121">如何 tooset 向上 Edison，請參閱的 toolearn[設定您的裝置][configure-your-device]。</span><span class="sxs-lookup"><span data-stu-id="98e80-121">toolearn how tooset up Edison, see [Configure your device][configure-your-device].</span></span>
* <span data-ttu-id="98e80-122">在您的 Azure 訂用帳戶中建立的 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="98e80-122">An IoT hub that is created in your Azure subscription.</span></span> <span data-ttu-id="98e80-123">toolearn 如何 toocreate IoT 中樞，請參閱[建立您的 Azure IoT 中樞][create-your-azure-iot-hub]。</span><span class="sxs-lookup"><span data-stu-id="98e80-123">toolearn how toocreate your IoT hub, see [Create your Azure IoT Hub][create-your-azure-iot-hub].</span></span>

## <a name="connect-hello-sample-application-tooyour-iot-hub"></a><span data-ttu-id="98e80-124">連接 hello 範例應用程式 tooyour IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="98e80-124">Connect hello sample application tooyour IoT hub</span></span>
1. <span data-ttu-id="98e80-125">請確定您是在 hello 儲存機制資料夾`iot-hub-node-edison-getting-started`。</span><span class="sxs-lookup"><span data-stu-id="98e80-125">Make sure that you're in hello repo folder `iot-hub-node-edison-getting-started`.</span></span> <span data-ttu-id="98e80-126">開啟 Visual Studio 程式碼中的 hello 範例應用程式，藉由執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="98e80-126">Open hello sample application in Visual Studio Code by running hello following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```

   <span data-ttu-id="98e80-127">hello 檔案在 hello`app`子資料夾會包含從 hello IoT 中樞的 hello 碼 toomonitor 內送訊息的 hello 索引鍵的原始程式檔。</span><span class="sxs-lookup"><span data-stu-id="98e80-127">hello file in hello `app` subfolder is hello key source file that contains hello code toomonitor incoming messages from hello IoT hub.</span></span> <span data-ttu-id="98e80-128">hello`blinkLED`函式會閃爍 hello LED。</span><span class="sxs-lookup"><span data-stu-id="98e80-128">hello `blinkLED` function blinks hello LED.</span></span>

   ![Hello 範例應用程式中的儲存機制結構][repo-structure]
2. <span data-ttu-id="98e80-130">藉由執行下列命令的 hello 初始化 hello 設定檔：</span><span class="sxs-lookup"><span data-stu-id="98e80-130">Initialize hello configuration file by running hello following commands:</span></span>

   ```bash
   npm install
   gulp init
   ```

   <span data-ttu-id="98e80-131">如果您已完成中的 hello 步驟[建立 Azure 的函式應用程式和儲存體帳戶][ create-an-azure-function-app-and-storage-account]此電腦上所有的 hello 組態繼承的因此您可以略過部署的 hello 步驟 toohello 工作和執行 hello 範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="98e80-131">If you completed hello steps in [Create an Azure function app and storage account][create-an-azure-function-app-and-storage-account] on this computer, all hello configurations are inherited, so you can skip hello step toohello task of deploying and running hello sample application.</span></span> <span data-ttu-id="98e80-132">如果您已完成中的 hello 步驟[建立 Azure 的函式應用程式和儲存體帳戶][ create-an-azure-function-app-and-storage-account]不同電腦上，您需要在 hello tooreplace hello 預留位置`config-edison.json`檔案。</span><span class="sxs-lookup"><span data-stu-id="98e80-132">If you completed hello steps in [Create an Azure function app and storage account][create-an-azure-function-app-and-storage-account] on a different computer, you need tooreplace hello placeholders in hello `config-edison.json` file.</span></span> <span data-ttu-id="98e80-133">hello`config-edison.json`檔案是在主資料夾 hello 子資料夾。</span><span class="sxs-lookup"><span data-stu-id="98e80-133">hello `config-edison.json` file is in hello subfolder of your home folder.</span></span>

   ![Hello config edison.json 檔案的內容](media/iot-hub-intel-edison-lessons/lesson4/config-edison.png)

   * <span data-ttu-id="98e80-135">取代**[裝置的主機名稱或 IP 位址]** hello 裝置的 IP 位址設定您的裝置時關閉標記。</span><span class="sxs-lookup"><span data-stu-id="98e80-135">Replace **[device hostname or IP address]** with hello device IP address you marked down when you configured your device.</span></span>
   * <span data-ttu-id="98e80-136">取代**[IoT 裝置連接字串]** hello 裝置連接字串，您會得到執行 hello`az iot device show-connection-string --hub-name {my hub name} --device-id {device id}`命令。</span><span class="sxs-lookup"><span data-stu-id="98e80-136">Replace **[IoT device connection string]** with hello device connection string that you get by running hello `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` command.</span></span>
   * <span data-ttu-id="98e80-137">取代**[IoT 中樞連接字串]**以 hello IoT 中樞連接字串，您會得到執行 hello`az iot hub show-connection-string --name {my hub name}`命令。</span><span class="sxs-lookup"><span data-stu-id="98e80-137">Replace **[IoT hub connection string]** with hello IoT hub connection string that you get by running hello `az iot hub show-connection-string --name {my hub name}` command.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="98e80-138">部署和執行 hello 範例應用程式</span><span class="sxs-lookup"><span data-stu-id="98e80-138">Deploy and run hello sample application</span></span>
<span data-ttu-id="98e80-139">部署和執行下列命令的 hello Edison 執行 hello 範例應用程式：</span><span class="sxs-lookup"><span data-stu-id="98e80-139">Deploy and run hello sample application on Edison by running hello following commands:</span></span>

```bash
gulp deploy && gulp run
```

<span data-ttu-id="98e80-140">hello gulp 命令會將部署 hello 範例應用程式 tooEdison。</span><span class="sxs-lookup"><span data-stu-id="98e80-140">hello gulp command deploys hello sample application tooEdison.</span></span> <span data-ttu-id="98e80-141">然後，它 hello 應用程式上執行 Edison 和您的主機上的個別工作電腦 toosend 20 閃爍訊息 tooEdison 從 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="98e80-141">Then, it runs hello application on Edison and a separate task on your host computer toosend 20 blink messages tooEdison from your IoT hub.</span></span>

<span data-ttu-id="98e80-142">Hello 範例應用程式執行之後，它會啟動接聽 toomessages 從 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="98e80-142">After hello sample application runs, it starts listening toomessages from your IoT hub.</span></span> <span data-ttu-id="98e80-143">同時，hello gulp 工作會從您的 IoT 中樞 tooEdison 傳送"閃爍 」 的數個訊息。</span><span class="sxs-lookup"><span data-stu-id="98e80-143">Meanwhile, hello gulp task sends several "blink" messages from your IoT hub tooEdison.</span></span> <span data-ttu-id="98e80-144">每個閃爍訊息 Edison 接收 hello 範例應用程式呼叫 hello`blinkLED`函式 tooblink hello LED。</span><span class="sxs-lookup"><span data-stu-id="98e80-144">For each blink message that Edison receives, hello sample application calls hello `blinkLED` function tooblink hello LED.</span></span>

<span data-ttu-id="98e80-145">您應該會看到的 gulp 工作傳送 20 則訊息從您的 IoT 中樞 tooEdison hello LED 閃爍 hello 為每隔兩秒鐘。</span><span class="sxs-lookup"><span data-stu-id="98e80-145">You should see hello LED blink every two seconds as hello gulp task sends 20 messages from your IoT hub tooEdison.</span></span> <span data-ttu-id="98e80-146">hello 上次是停止 hello 應用程式無法執行 「 停止 」 訊息。</span><span class="sxs-lookup"><span data-stu-id="98e80-146">hello last one is a "stop" message that stops hello application from running.</span></span>

![具有 gulp 命令和閃爍訊息的範例應用程式][gulp-command-and-blink-messages]

## <a name="summary"></a><span data-ttu-id="98e80-148">摘要</span><span class="sxs-lookup"><span data-stu-id="98e80-148">Summary</span></span>
<span data-ttu-id="98e80-149">您已成功傳送訊息，從您 IoT 中樞 tooEdison tooblink hello LED。</span><span class="sxs-lookup"><span data-stu-id="98e80-149">You’ve successfully sent messages from your IoT hub tooEdison tooblink hello LED.</span></span> <span data-ttu-id="98e80-150">是選擇性的 hello 下一項工作： 變更 hello 開啟和關閉 hello LED 的行為。</span><span class="sxs-lookup"><span data-stu-id="98e80-150">hello next task is optional: change hello on and off behavior of hello LED.</span></span>

## <a name="next-steps"></a><span data-ttu-id="98e80-151">後續步驟</span><span class="sxs-lookup"><span data-stu-id="98e80-151">Next steps</span></span>
<span data-ttu-id="98e80-152">[變更 hello 開啟和關閉 hello LED 的行為][change-the-on-and-off-behavior-of-the-led]</span><span class="sxs-lookup"><span data-stu-id="98e80-152">[Change hello on and off behavior of hello LED][change-the-on-and-off-behavior-of-the-led]</span></span>

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[configure-your-device]: iot-hub-intel-edison-kit-node-lesson1-configure-your-device.md
[create-your-azure-iot-hub]: iot-hub-intel-edison-kit-node-lesson2-prepare-azure-iot-hub.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson4/repo_structure.png
[create-an-azure-function-app-and-storage-account]: iot-hub-intel-edison-kit-node-lesson3-deploy-resource-manager-template.md
[gulp-command-and-blink-messages]: media/iot-hub-intel-edison-lessons/lesson4/gulp_blink.png
[change-the-on-and-off-behavior-of-the-led]: iot-hub-intel-edison-kit-node-lesson4-change-led-behavior.md