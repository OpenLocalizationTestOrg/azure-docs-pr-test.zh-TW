---
title: "模擬裝置與 Azure IoT 閘道 - 第 3 課︰執行範例應用程式 | Microsoft Docs"
description: "執行模擬裝置範例應用程式將溫度資料傳送至您的 Azure IoT 中樞"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "資料送至雲端"
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
ms.openlocfilehash: 7df2d730c38a9f715e0fd57b4d436724a5727760
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="configure-and-run-a-simulated-device-sample-app"></a><span data-ttu-id="00da7-104">設定並執行模擬裝置範例應用程式</span><span class="sxs-lookup"><span data-stu-id="00da7-104">Configure and run a simulated device sample app</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="00da7-105">將執行的作業</span><span class="sxs-lookup"><span data-stu-id="00da7-105">What you will do</span></span>

- <span data-ttu-id="00da7-106">複製範例存放庫。</span><span class="sxs-lookup"><span data-stu-id="00da7-106">Clone the sample repository.</span></span>
- <span data-ttu-id="00da7-107">使用 Azure CLI 取得模擬裝置範例應用程式的 IoT 中樞和邏輯裝置資訊。</span><span class="sxs-lookup"><span data-stu-id="00da7-107">Use the Azure CLI to get your IoT hub and logical device information for simulated device sample application.</span></span> <span data-ttu-id="00da7-108">設定及執行模擬裝置範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="00da7-108">Configure and run the simulated device sample application.</span></span>

<span data-ttu-id="00da7-109">如果您有任何問題，請在[疑難排解頁面](iot-hub-gateway-kit-c-sim-troubleshooting.md)尋求解決方案。</span><span class="sxs-lookup"><span data-stu-id="00da7-109">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="00da7-110">學習目標</span><span class="sxs-lookup"><span data-stu-id="00da7-110">What you will learn</span></span>

<span data-ttu-id="00da7-111">在本文中，您將了解：</span><span class="sxs-lookup"><span data-stu-id="00da7-111">In this article, you will learn:</span></span>

- <span data-ttu-id="00da7-112">如何設定及執行模擬裝置範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="00da7-112">How to configure and run the simulated device sample application.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="00da7-113">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="00da7-113">What you need</span></span>

<span data-ttu-id="00da7-114">您必須已成功完成</span><span class="sxs-lookup"><span data-stu-id="00da7-114">You must have successfully completed</span></span>

- [<span data-ttu-id="00da7-115">建立 IoT 中樞並登錄您的裝置</span><span class="sxs-lookup"><span data-stu-id="00da7-115">Create an IoT hub and register your device</span></span>](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)

## <a name="clone-the-sample-repository-to-the-host-computer"></a><span data-ttu-id="00da7-116">將範例存放庫複製至主機電腦</span><span class="sxs-lookup"><span data-stu-id="00da7-116">Clone the sample repository to the host computer</span></span>

<span data-ttu-id="00da7-117">若要複製範例存放庫，在主機電腦上遵循下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="00da7-117">To clone the sample repository, follow these steps on the host computer:</span></span>

1. <span data-ttu-id="00da7-118">在 Windows 上開啟命令提示字元，或在 macOS 或 Ubuntu 上開啟終端機。</span><span class="sxs-lookup"><span data-stu-id="00da7-118">Open a Command Prompt in Windows or open a terminal in macOS or Ubuntu.</span></span>
2. <span data-ttu-id="00da7-119">執行以下命令：</span><span class="sxs-lookup"><span data-stu-id="00da7-119">Run the following commands:</span></span>

   ```bash
   git clone https://github.com/Azure-samples/iot-hub-c-intel-nuc-gateway-getting-started
   cd iot-hub-c-intel-nuc-gateway-getting-started
   ```

## <a name="configure-the-simulated-device-and-your-nuc"></a><span data-ttu-id="00da7-120">設定模擬裝置和您的 NUC</span><span class="sxs-lookup"><span data-stu-id="00da7-120">Configure the simulated device and your NUC</span></span>

1. <span data-ttu-id="00da7-121">在 Visual Studio Code 中開啟組態檔 `config.json`，方法是執行下列命令︰</span><span class="sxs-lookup"><span data-stu-id="00da7-121">Open the configuration file `config.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   code config.json
   ```

2. <span data-ttu-id="00da7-122">將 `"has_sensortag": true` 取代為 `"has_sensortag": false`</span><span class="sxs-lookup"><span data-stu-id="00da7-122">Replace `"has_sensortag": true` with `"has_sensortag": false`</span></span>

   ![設定為您沒有 TI SensorTag 裝置](media/iot-hub-gateway-kit-lessons/lesson3/config_no_sensortag.png)

3. <span data-ttu-id="00da7-124">執行下列命令初始化組態檔：</span><span class="sxs-lookup"><span data-stu-id="00da7-124">Initialize the configuration file by running the following commands:</span></span>

   ```bash
   cd Lesson3
   npm install
   gulp init
   ```

4. <span data-ttu-id="00da7-125">執行下列命令在 Visual Studio Code 中開啟 `config-gateway.json`︰</span><span class="sxs-lookup"><span data-stu-id="00da7-125">Open `config-gateway.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-gateway.json
   ```

5. <span data-ttu-id="00da7-126">找到下列這行程式碼，並將 `[device hostname or IP address]` 取代為 Intel NUC 的 IP 位址或主機名稱。</span><span class="sxs-lookup"><span data-stu-id="00da7-126">Locate the following line of code and replace `[device hostname or IP address]` with IP address or host name of the Intel NUC.</span></span>
   <span data-ttu-id="00da7-127">![設定閘道器的螢幕擷取畫面](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)</span><span class="sxs-lookup"><span data-stu-id="00da7-127">![screenshot of config gateway](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)</span></span>

## <a name="get-the-connection-string-of-your-iot-hub-logical-device"></a><span data-ttu-id="00da7-128">取得 IoT 中樞邏輯裝置的連接字串</span><span class="sxs-lookup"><span data-stu-id="00da7-128">Get the connection string of your IoT hub logical device</span></span>

<span data-ttu-id="00da7-129">若要取得邏輯裝置的 Azure IoT 中樞連接字串，在主機電腦上執行下列命令︰</span><span class="sxs-lookup"><span data-stu-id="00da7-129">To get the Azure IoT hub connection string of your logical device, run the following command on the host computer:</span></span>

```bash
az iot device show-connection-string --hub-name {IoT hub name} --device-id mydevice --resource-group iot-gateway
```

<span data-ttu-id="00da7-130">`{IoT hub name}` 是您所使用的 IoT 中樞名稱。</span><span class="sxs-lookup"><span data-stu-id="00da7-130">`{IoT hub name}` is the IoT hub name that you used.</span></span> <span data-ttu-id="00da7-131">如果您在第 2 課沒有變更值，使用 iot-gateway 作為 `{resource group name}` 的值，使用 mydevice 作為 `{device id}` 的值。</span><span class="sxs-lookup"><span data-stu-id="00da7-131">Use iot-gateway as the value of `{resource group name}` and use mydevice as the value of `{device id}` if you didn't change the value in Lesson 2.</span></span>

## <a name="configure-the-simulated-device-cloud-upload-sample-application"></a><span data-ttu-id="00da7-132">設定模擬裝置雲端上傳範例應用程式</span><span class="sxs-lookup"><span data-stu-id="00da7-132">Configure the simulated device cloud upload sample application</span></span>

<span data-ttu-id="00da7-133">若要設定及執行模擬裝置雲端上傳範例應用程式，在主機電腦上執行下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="00da7-133">To configure and run the simulated device cloud upload sample application, follow these steps on the host computer:</span></span>

1. <span data-ttu-id="00da7-134">執行下列命令在 Visual Studio Code 中開啟 `config-sensortag.json`︰</span><span class="sxs-lookup"><span data-stu-id="00da7-134">Open `config-sensortag.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-sensortag.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-sensortag.json
   ```

   ![設定 sensortag 的螢幕擷取畫面](media/iot-hub-gateway-kit-lessons/lesson3/config_simulated_device.png)

2. <span data-ttu-id="00da7-136">取代程式碼中的下列內容：</span><span class="sxs-lookup"><span data-stu-id="00da7-136">Make the following replacements in the code:</span></span>
   - <span data-ttu-id="00da7-137">將 `[IoT hub name]` 取代為 IoT 中樞名稱。</span><span class="sxs-lookup"><span data-stu-id="00da7-137">Replace `[IoT hub name]` with the IoT hub name.</span></span>
   - <span data-ttu-id="00da7-138">將 `[IoT device connection string]` 取代為您的 IoT 中樞邏輯裝置的連接字串。</span><span class="sxs-lookup"><span data-stu-id="00da7-138">Replace `[IoT device connection string]` with the connection string of your IoT hub logical device.</span></span>

3. <span data-ttu-id="00da7-139">執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="00da7-139">Run the application.</span></span>

   <span data-ttu-id="00da7-140">執行下列命令，部署及執行應用程式：</span><span class="sxs-lookup"><span data-stu-id="00da7-140">Deploy and run the application by running the following command:</span></span>

   ```bash
   gulp run
   ```

## <a name="verify-the-sample-application-works"></a><span data-ttu-id="00da7-141">確認範例應用程式可運作</span><span class="sxs-lookup"><span data-stu-id="00da7-141">Verify the sample application works</span></span>

<span data-ttu-id="00da7-142">您現在應該會看到如下的輸出：</span><span class="sxs-lookup"><span data-stu-id="00da7-142">You should now see output like the following:</span></span>

![模擬裝置範例應用程式的輸出](media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_simudev.png)

<span data-ttu-id="00da7-144">應用程式會將溫度資料傳送至您的 IoT 中樞，持續 40 秒。</span><span class="sxs-lookup"><span data-stu-id="00da7-144">The application sends temperature data to your IoT hub, which lasts for 40 seconds.</span></span>

## <a name="summary"></a><span data-ttu-id="00da7-145">摘要</span><span class="sxs-lookup"><span data-stu-id="00da7-145">Summary</span></span>

<span data-ttu-id="00da7-146">您已成功設定及執行模擬裝置雲端上傳範例應用程式，此程式會以模擬裝置將資料傳送至您的 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="00da7-146">You've successfully configured and run the simulated device cloud upload sample application which sends data to your IoT hub with simulated device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="00da7-147">後續步驟</span><span class="sxs-lookup"><span data-stu-id="00da7-147">Next steps</span></span>
[<span data-ttu-id="00da7-148">讀取來自 IoT 中樞的傳入訊息</span><span class="sxs-lookup"><span data-stu-id="00da7-148">Read messages from your IoT hub</span></span>](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md)