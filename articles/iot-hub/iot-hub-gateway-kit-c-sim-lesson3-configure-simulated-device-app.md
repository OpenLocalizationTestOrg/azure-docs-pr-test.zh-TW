---
title: "模擬裝置與 Azure IoT 閘道 - 第 3 課︰執行範例應用程式 | Microsoft Docs"
description: "執行模擬的裝置範例應用程式 toosend 溫度資料 tooyour IoT 中樞"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "資料 toocloud"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 5d051d99-9749-4150-b3c8-573b0bda9c52
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: bc2c97919e95e4e3977a8b6ac75162bf2b5017be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-run-a-simulated-device-sample-app"></a><span data-ttu-id="fe6ba-104">設定並執行模擬裝置範例應用程式</span><span class="sxs-lookup"><span data-stu-id="fe6ba-104">Configure and run a simulated device sample app</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="fe6ba-105">將執行的作業</span><span class="sxs-lookup"><span data-stu-id="fe6ba-105">What you will do</span></span>

- <span data-ttu-id="fe6ba-106">複製 hello 範例儲存機制。</span><span class="sxs-lookup"><span data-stu-id="fe6ba-106">Clone hello sample repository.</span></span>
- <span data-ttu-id="fe6ba-107">使用您的 IoT 中樞與邏輯裝置資訊 hello Azure CLI tooget 用於模擬的裝置範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="fe6ba-107">Use hello Azure CLI tooget your IoT hub and logical device information for simulated device sample application.</span></span> <span data-ttu-id="fe6ba-108">設定和執行 hello 模擬裝置的範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="fe6ba-108">Configure and run hello simulated device sample application.</span></span>

<span data-ttu-id="fe6ba-109">如果您有任何問題，尋找解決方案上 hello[疑難排解頁面](iot-hub-gateway-kit-c-sim-troubleshooting.md)。</span><span class="sxs-lookup"><span data-stu-id="fe6ba-109">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="fe6ba-110">學習目標</span><span class="sxs-lookup"><span data-stu-id="fe6ba-110">What you will learn</span></span>

<span data-ttu-id="fe6ba-111">在本文中，您將了解：</span><span class="sxs-lookup"><span data-stu-id="fe6ba-111">In this article, you will learn:</span></span>

- <span data-ttu-id="fe6ba-112">如何 tooconfigure 和執行的 hello 模擬裝置的範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="fe6ba-112">How tooconfigure and run hello simulated device sample application.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="fe6ba-113">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="fe6ba-113">What you need</span></span>

<span data-ttu-id="fe6ba-114">您必須已成功完成</span><span class="sxs-lookup"><span data-stu-id="fe6ba-114">You must have successfully completed</span></span>

- [<span data-ttu-id="fe6ba-115">建立 IoT 中樞並登錄您的裝置</span><span class="sxs-lookup"><span data-stu-id="fe6ba-115">Create an IoT hub and register your device</span></span>](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)

## <a name="clone-hello-sample-repository-toohello-host-computer"></a><span data-ttu-id="fe6ba-116">複製 hello 範例儲存機制 toohello 主機電腦</span><span class="sxs-lookup"><span data-stu-id="fe6ba-116">Clone hello sample repository toohello host computer</span></span>

<span data-ttu-id="fe6ba-117">tooclone hello 範例儲存機制，請遵循下列步驟在 hello 主機電腦上：</span><span class="sxs-lookup"><span data-stu-id="fe6ba-117">tooclone hello sample repository, follow these steps on hello host computer:</span></span>

1. <span data-ttu-id="fe6ba-118">在 Windows 上開啟命令提示字元，或在 macOS 或 Ubuntu 上開啟終端機。</span><span class="sxs-lookup"><span data-stu-id="fe6ba-118">Open a Command Prompt in Windows or open a terminal in macOS or Ubuntu.</span></span>
2. <span data-ttu-id="fe6ba-119">執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="fe6ba-119">Run hello following commands:</span></span>

   ```bash
   git clone https://github.com/Azure-samples/iot-hub-c-intel-nuc-gateway-getting-started
   cd iot-hub-c-intel-nuc-gateway-getting-started
   ```

## <a name="configure-hello-simulated-device-and-your-nuc"></a><span data-ttu-id="fe6ba-120">設定 hello 模擬的裝置和您 NUC</span><span class="sxs-lookup"><span data-stu-id="fe6ba-120">Configure hello simulated device and your NUC</span></span>

1. <span data-ttu-id="fe6ba-121">開啟 hello 設定檔`config.json`在 Visual Studio 程式碼執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="fe6ba-121">Open hello configuration file `config.json` in Visual Studio Code by running hello following command:</span></span>

   ```bash
   code config.json
   ```

2. <span data-ttu-id="fe6ba-122">將 `"has_sensortag": true` 取代為 `"has_sensortag": false`</span><span class="sxs-lookup"><span data-stu-id="fe6ba-122">Replace `"has_sensortag": true` with `"has_sensortag": false`</span></span>

   ![設定為您沒有 TI SensorTag 裝置](media/iot-hub-gateway-kit-lessons/lesson3/config_no_sensortag.png)

3. <span data-ttu-id="fe6ba-124">藉由執行下列命令的 hello 初始化 hello 設定檔：</span><span class="sxs-lookup"><span data-stu-id="fe6ba-124">Initialize hello configuration file by running hello following commands:</span></span>

   ```bash
   cd Lesson3
   npm install
   gulp init
   ```

4. <span data-ttu-id="fe6ba-125">開啟`config-gateway.json`在 Visual Studio 程式碼執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="fe6ba-125">Open `config-gateway.json` in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-gateway.json
   ```

5. <span data-ttu-id="fe6ba-126">找出 hello 下列程式碼行並取代`[device hostname or IP address]`與 hello Intel NUC 的 IP 位址或主機名稱。</span><span class="sxs-lookup"><span data-stu-id="fe6ba-126">Locate hello following line of code and replace `[device hostname or IP address]` with IP address or host name of hello Intel NUC.</span></span>
   <span data-ttu-id="fe6ba-127">![設定閘道器的螢幕擷取畫面](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)</span><span class="sxs-lookup"><span data-stu-id="fe6ba-127">![screenshot of config gateway](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)</span></span>

## <a name="get-hello-connection-string-of-your-iot-hub-logical-device"></a><span data-ttu-id="fe6ba-128">取得您的 IoT 中樞邏輯裝置 hello 連接字串</span><span class="sxs-lookup"><span data-stu-id="fe6ba-128">Get hello connection string of your IoT hub logical device</span></span>

<span data-ttu-id="fe6ba-129">tooget hello Azure IoT 中樞連接字串的邏輯裝置，執行下列命令在 hello 主機電腦上的 hello:</span><span class="sxs-lookup"><span data-stu-id="fe6ba-129">tooget hello Azure IoT hub connection string of your logical device, run hello following command on hello host computer:</span></span>

```bash
az iot device show-connection-string --hub-name {IoT hub name} --device-id mydevice --resource-group iot-gateway
```

<span data-ttu-id="fe6ba-130">`{IoT hub name}`是您所使用的 hello IoT 中樞名稱。</span><span class="sxs-lookup"><span data-stu-id="fe6ba-130">`{IoT hub name}` is hello IoT hub name that you used.</span></span> <span data-ttu-id="fe6ba-131">當做 hello 值使用 iot 閘道`{resource group name}`並用 mydevice 做為 hello 值`{device id}`如果您沒有變更 hello 課程 2 中的值。</span><span class="sxs-lookup"><span data-stu-id="fe6ba-131">Use iot-gateway as hello value of `{resource group name}` and use mydevice as hello value of `{device id}` if you didn't change hello value in Lesson 2.</span></span>

## <a name="configure-hello-simulated-device-cloud-upload-sample-application"></a><span data-ttu-id="fe6ba-132">設定 hello 模擬裝置的雲端上傳範例應用程式</span><span class="sxs-lookup"><span data-stu-id="fe6ba-132">Configure hello simulated device cloud upload sample application</span></span>

<span data-ttu-id="fe6ba-133">tooconfigure 和執行的 hello 模擬裝置的雲端上傳範例應用程式，請遵循下列步驟在 hello 主機電腦上：</span><span class="sxs-lookup"><span data-stu-id="fe6ba-133">tooconfigure and run hello simulated device cloud upload sample application, follow these steps on hello host computer:</span></span>

1. <span data-ttu-id="fe6ba-134">開啟`config-sensortag.json`在 Visual Studio 程式碼執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="fe6ba-134">Open `config-sensortag.json` in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-sensortag.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-sensortag.json
   ```

   ![設定 sensortag 的螢幕擷取畫面](media/iot-hub-gateway-kit-lessons/lesson3/config_simulated_device.png)

2. <span data-ttu-id="fe6ba-136">請遵循取代 hello 程式碼中的 hello:</span><span class="sxs-lookup"><span data-stu-id="fe6ba-136">Make hello following replacements in hello code:</span></span>
   - <span data-ttu-id="fe6ba-137">取代`[IoT hub name]`hello IoT 中樞名稱。</span><span class="sxs-lookup"><span data-stu-id="fe6ba-137">Replace `[IoT hub name]` with hello IoT hub name.</span></span>
   - <span data-ttu-id="fe6ba-138">取代`[IoT device connection string]`hello 的 IoT 中樞的邏輯裝置的連接字串。</span><span class="sxs-lookup"><span data-stu-id="fe6ba-138">Replace `[IoT device connection string]` with hello connection string of your IoT hub logical device.</span></span>

3. <span data-ttu-id="fe6ba-139">執行 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="fe6ba-139">Run hello application.</span></span>

   <span data-ttu-id="fe6ba-140">部署和執行 hello 應用程式，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="fe6ba-140">Deploy and run hello application by running hello following command:</span></span>

   ```bash
   gulp run
   ```

## <a name="verify-hello-sample-application-works"></a><span data-ttu-id="fe6ba-141">確認 hello 範例應用程式可運作</span><span class="sxs-lookup"><span data-stu-id="fe6ba-141">Verify hello sample application works</span></span>

<span data-ttu-id="fe6ba-142">您現在應該會看到類似 hello 下列輸出：</span><span class="sxs-lookup"><span data-stu-id="fe6ba-142">You should now see output like hello following:</span></span>

![模擬裝置範例應用程式的輸出](media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_simudev.png)

<span data-ttu-id="fe6ba-144">hello 應用程式傳送溫度資料 tooyour IoT 中樞，可在延續 40 秒。</span><span class="sxs-lookup"><span data-stu-id="fe6ba-144">hello application sends temperature data tooyour IoT hub, which lasts for 40 seconds.</span></span>

## <a name="summary"></a><span data-ttu-id="fe6ba-145">摘要</span><span class="sxs-lookup"><span data-stu-id="fe6ba-145">Summary</span></span>

<span data-ttu-id="fe6ba-146">您已順利設定並執行的 hello 模擬裝置的雲端上傳範例應用程式傳送資料 tooyour IoT 中樞與模擬的裝置。</span><span class="sxs-lookup"><span data-stu-id="fe6ba-146">You've successfully configured and run hello simulated device cloud upload sample application which sends data tooyour IoT hub with simulated device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fe6ba-147">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fe6ba-147">Next steps</span></span>
[<span data-ttu-id="fe6ba-148">讀取來自 IoT 中樞的傳入訊息</span><span class="sxs-lookup"><span data-stu-id="fe6ba-148">Read messages from your IoT hub</span></span>](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md)