---
title: "連接覆盆子 Pi （節點） tooAzure IoT-第 3 課： 執行範例 |Microsoft 文件"
description: "部署和執行範例應用程式 tooRaspberry Pi 3 傳送訊息 tooyour IoT 中樞和閃爍 hello LED。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "閃爍 led 雲端 pi, 來自雲端的 led 閃爍"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 427d8e5e-8af8-4249-8607-44edc90a4972
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 991c64e0b1b6f965b029560cdc6403e557841e30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-toosend-device-to-cloud-messages"></a><span data-ttu-id="fca55-104">執行範例應用程式 toosend 裝置到雲端訊息</span><span class="sxs-lookup"><span data-stu-id="fca55-104">Run a sample application toosend device-to-cloud messages</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="fca55-105">將執行的作業</span><span class="sxs-lookup"><span data-stu-id="fca55-105">What you will do</span></span>
<span data-ttu-id="fca55-106">本文將告訴您 toodeploy 及執行範例應用程式覆盆子 Pi 3 傳送訊息 tooyour IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="fca55-106">This article will show you how toodeploy and run a sample application on Raspberry Pi 3 that sends messages tooyour IoT hub.</span></span> <span data-ttu-id="fca55-107">如果您有任何問題，尋找解決方案上 hello[疑難排解頁面](iot-hub-raspberry-pi-kit-node-troubleshooting.md)。</span><span class="sxs-lookup"><span data-stu-id="fca55-107">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="fca55-108">學習目標</span><span class="sxs-lookup"><span data-stu-id="fca55-108">What you will learn</span></span>
<span data-ttu-id="fca55-109">您將學習如何 toouse hello 的 gulp 工具 toodeploy 和 pi 執行 hello 範例 Node.js 應用程式。</span><span class="sxs-lookup"><span data-stu-id="fca55-109">You will learn how toouse hello gulp tool toodeploy and run hello sample Node.js application on Pi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="fca55-110">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="fca55-110">What you need</span></span>
* <span data-ttu-id="fca55-111">在開始這項工作之前，您必須已順利完成[建立 Azure 的函式應用程式與儲存體帳戶 tooprocess 和市集 IoT 中樞訊息](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md)。</span><span class="sxs-lookup"><span data-stu-id="fca55-111">Before you start this task, you must have successfully completed [Create an Azure function app and a storage account tooprocess and store IoT hub messages](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md).</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="fca55-112">取得 IoT 中樞與裝置連接字串</span><span class="sxs-lookup"><span data-stu-id="fca55-112">Get your IoT hub and device connection strings</span></span>
<span data-ttu-id="fca55-113">hello 裝置連接字串會使用 Pi tooconnect tooyour IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="fca55-113">hello device connection string is used by your Pi tooconnect tooyour IoT hub.</span></span> <span data-ttu-id="fca55-114">hello IoT 中樞連接字串是使用的 tooconnect toohello 身分識別登錄在 IoT 中樞 toomanage hello 裝置允許 tooconnect tooyour IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="fca55-114">hello IoT hub connection string is used tooconnect toohello identity registry in your IoT hub toomanage hello devices that are allowed tooconnect tooyour IoT hub.</span></span> 

* <span data-ttu-id="fca55-115">列出資源群組中的所有您 IoT 中樞執行下列 Azure CLI 命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="fca55-115">List all your IoT hubs in your resource group by running hello following Azure CLI command:</span></span>

```bash
az iot hub list -g iot-sample --query [].name
```

<span data-ttu-id="fca55-116">使用`iot-sample`做為 hello 值`{resource group name}`如果您沒有變更 hello 值。</span><span class="sxs-lookup"><span data-stu-id="fca55-116">Use `iot-sample` as hello value of `{resource group name}` if you didn't change hello value.</span></span>

* <span data-ttu-id="fca55-117">藉由執行下列 Azure CLI 命令的 hello 收到 hello IoT 中樞連接字串：</span><span class="sxs-lookup"><span data-stu-id="fca55-117">Get hello IoT hub connection string by running hello following Azure CLI command:</span></span>

```bash
az iot hub show-connection-string --name {my hub name} -g iot-sample
```

<span data-ttu-id="fca55-118">`{my hub name}`這是您指定當您建立 IoT 中樞，並註冊 Pi hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="fca55-118">`{my hub name}` is hello name that you specified when you created your IoT hub and registered Pi.</span></span>

* <span data-ttu-id="fca55-119">藉由執行下列命令的 hello 收到 hello 裝置連接字串：</span><span class="sxs-lookup"><span data-stu-id="fca55-119">Get hello device connection string by running hello following command:</span></span>

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id myraspberrypi -g iot-sample
```

<span data-ttu-id="fca55-120">使用`myraspberrypi`做為 hello 值`{device id}`如果您沒有變更 hello 值。</span><span class="sxs-lookup"><span data-stu-id="fca55-120">Use `myraspberrypi` as hello value of `{device id}` if you didn't change hello value.</span></span>

## <a name="configure-hello-device-connection"></a><span data-ttu-id="fca55-121">設定 hello 裝置連線</span><span class="sxs-lookup"><span data-stu-id="fca55-121">Configure hello device connection</span></span>
1. <span data-ttu-id="fca55-122">藉由執行下列命令的 hello 初始化 hello 設定檔：</span><span class="sxs-lookup"><span data-stu-id="fca55-122">Initialize hello configuration file by running hello following commands:</span></span>
   
   ```bash
   npm install
   gulp init
   ```
2. <span data-ttu-id="fca55-123">開啟 hello 裝置組態檔`config-raspberrypi.json`在 Visual Studio 程式碼執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="fca55-123">Open hello device configuration file `config-raspberrypi.json` in Visual Studio Code by running hello following command:</span></span>
   
   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
  
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```
  
   ![config.json](media/iot-hub-raspberry-pi-lessons/lesson3/config.png)
3. <span data-ttu-id="fca55-125">請遵循取代 hello hello`config-raspberrypi.json`檔案：</span><span class="sxs-lookup"><span data-stu-id="fca55-125">Make hello following replacements in hello `config-raspberrypi.json` file:</span></span>
   
   * <span data-ttu-id="fca55-126">取代**[裝置的主機名稱或 IP 位址]** hello 裝置 IP 位址或主機名稱與您向`device-discovery-cli`或與您的裝置設定時，會繼承 hello 值。</span><span class="sxs-lookup"><span data-stu-id="fca55-126">Replace **[device hostname or IP address]** with hello device IP address or host name you got from `device-discovery-cli` or with hello value inherited when you configured your device.</span></span>
   * <span data-ttu-id="fca55-127">取代**[IoT 裝置連接字串]**以 hello`device connection string`您取得的。</span><span class="sxs-lookup"><span data-stu-id="fca55-127">Replace **[IoT device connection string]** with hello `device connection string` you obtained.</span></span>
   * <span data-ttu-id="fca55-128">取代**[IoT 中樞連接字串]**以 hello`iot hub connection string`您取得的。</span><span class="sxs-lookup"><span data-stu-id="fca55-128">Replace **[IoT hub connection string]** with hello `iot hub connection string` you obtained.</span></span>

<span data-ttu-id="fca55-129">更新 hello`config-raspberrypi.json`檔案，所以您可以部署 hello 範例應用程式，從您的電腦。</span><span class="sxs-lookup"><span data-stu-id="fca55-129">Update hello `config-raspberrypi.json` file so that you can deploy hello sample application from your computer.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="fca55-130">部署和執行 hello 範例應用程式</span><span class="sxs-lookup"><span data-stu-id="fca55-130">Deploy and run hello sample application</span></span>
<span data-ttu-id="fca55-131">部署和執行 pi 的 hello 範例應用程式，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="fca55-131">Deploy and run hello sample application on Pi by running hello following command:</span></span>

```bash
gulp deploy && gulp run
```

## <a name="verify-that-hello-sample-application-works"></a><span data-ttu-id="fca55-132">確認 hello 範例應用程式可正常運作</span><span class="sxs-lookup"><span data-stu-id="fca55-132">Verify that hello sample application works</span></span>
<span data-ttu-id="fca55-133">您應該會看到 hello LED 所連接的 tooPi 閃爍每隔兩秒鐘。</span><span class="sxs-lookup"><span data-stu-id="fca55-133">You should see hello LED that is connected tooPi blinking every two seconds.</span></span> <span data-ttu-id="fca55-134">每次 hello LED 閃爍，hello 範例應用程式傳送訊息 tooyour IoT 中樞，並確認該 hello 訊息已成功傳送 tooyour IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="fca55-134">Every time hello LED blinks, hello sample application sends a message tooyour IoT hub and verifies that hello message has been successfully sent tooyour IoT hub.</span></span> <span data-ttu-id="fca55-135">此外，收到 hello IoT 中樞的每個訊息會列印 hello 主控台視窗中。</span><span class="sxs-lookup"><span data-stu-id="fca55-135">In addition, each message received by hello IoT hub is printed in hello console window.</span></span> <span data-ttu-id="fca55-136">hello 範例應用程式會自動終止後傳送 20 則訊息。</span><span class="sxs-lookup"><span data-stu-id="fca55-136">hello sample application terminates automatically after sending 20 messages.</span></span>

![具有所傳送和接收之訊息的範例應用程式](media/iot-hub-raspberry-pi-lessons/lesson3/gulp_run.png)

## <a name="summary"></a><span data-ttu-id="fca55-138">摘要</span><span class="sxs-lookup"><span data-stu-id="fca55-138">Summary</span></span>
<span data-ttu-id="fca55-139">您已部署並執行 hello 新閃爍範例應用程式上 Pi toosend 裝置到雲端訊息 tooyour IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="fca55-139">You've deployed and run hello new blink sample application on Pi toosend device-to-cloud messages tooyour IoT hub.</span></span> <span data-ttu-id="fca55-140">現在，當它們被寫入 toohello 儲存體帳戶，您可以監視您的訊息。</span><span class="sxs-lookup"><span data-stu-id="fca55-140">You can now monitor your messages as they are written toohello storage account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fca55-141">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fca55-141">Next steps</span></span>
[<span data-ttu-id="fca55-142">讀取保留在 Azure 儲存體中的訊息</span><span class="sxs-lookup"><span data-stu-id="fca55-142">Read messages persisted in Azure Storage</span></span>](iot-hub-raspberry-pi-kit-node-lesson3-read-table-storage.md)

