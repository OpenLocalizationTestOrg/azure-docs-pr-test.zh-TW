---
title: "SensorTag 裝置與 Azure IoT 閘道 - 第 3 課︰執行範例應用程式 | Microsoft Docs"
description: "從 B SensorTag 以及 IoT 中樞，請執行範例應用程式 tooreceive b 的資料。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "b 應用程式、 感應器監視應用程式、 感應器資料收集、 感應器資料 toocloud 感應器資料"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: b33e53a1-1df7-4412-ade1-45185aec5bef
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 4a8acdeadd402ffc82d3b766e1ec03a77ddcebb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-run-a-ble-sample-application"></a><span data-ttu-id="6bb58-104">設定和執行 BLE 範例應用程式</span><span class="sxs-lookup"><span data-stu-id="6bb58-104">Configure and run a BLE sample application</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="6bb58-105">將執行的作業</span><span class="sxs-lookup"><span data-stu-id="6bb58-105">What you will do</span></span>

- <span data-ttu-id="6bb58-106">複製 hello 範例儲存機制。</span><span class="sxs-lookup"><span data-stu-id="6bb58-106">Clone hello sample repository.</span></span> 
- <span data-ttu-id="6bb58-107">設定 hello SensorTag 和 Intel NUC 之間的連線。</span><span class="sxs-lookup"><span data-stu-id="6bb58-107">Set up hello connectivity between SensorTag and Intel NUC.</span></span> 
- <span data-ttu-id="6bb58-108">使用您的 IoT 中樞與 SensorTag 資訊 hello Azure CLI tooget b （藍芽低能源） 範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="6bb58-108">Use hello Azure CLI tooget your IoT hub and SensorTag information for a BLE(Bluetooth Low Energy) sample application.</span></span> <span data-ttu-id="6bb58-109">設定和執行 hello b 範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="6bb58-109">And configure and run hello BLE sample application.</span></span> 

<span data-ttu-id="6bb58-110">如果您有任何問題，尋找解決方案上 hello[疑難排解頁面](iot-hub-gateway-kit-c-troubleshooting.md)。</span><span class="sxs-lookup"><span data-stu-id="6bb58-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="6bb58-111">學習目標</span><span class="sxs-lookup"><span data-stu-id="6bb58-111">What you will learn</span></span>

<span data-ttu-id="6bb58-112">在本文中，您將了解：</span><span class="sxs-lookup"><span data-stu-id="6bb58-112">In this article, you will learn:</span></span>

- <span data-ttu-id="6bb58-113">如何 tooconfigure 和執行的 hello b 範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="6bb58-113">How tooconfigure and run hello BLE sample application.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="6bb58-114">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="6bb58-114">What you need</span></span>

<span data-ttu-id="6bb58-115">您必須已成功完成</span><span class="sxs-lookup"><span data-stu-id="6bb58-115">You must have successfully completed</span></span>

- [<span data-ttu-id="6bb58-116">建立 IoT 中樞並登錄裝置</span><span class="sxs-lookup"><span data-stu-id="6bb58-116">Create an IoT hub and register SensorTag</span></span>](iot-hub-gateway-kit-c-lesson2-register-device.md)

## <a name="clone-hello-sample-repository-toohello-host-computer"></a><span data-ttu-id="6bb58-117">複製 hello 範例儲存機制 toohello 主機電腦</span><span class="sxs-lookup"><span data-stu-id="6bb58-117">Clone hello sample repository toohello host computer</span></span>

<span data-ttu-id="6bb58-118">tooclone hello 範例儲存機制，請遵循下列步驟在 hello 主機電腦上：</span><span class="sxs-lookup"><span data-stu-id="6bb58-118">tooclone hello sample repository, follow these steps on hello host computer:</span></span>

1. <span data-ttu-id="6bb58-119">在 Windows 上開啟命令提示字元視窗，或在 macOS 或 Ubuntu 上開啟終端機。</span><span class="sxs-lookup"><span data-stu-id="6bb58-119">Open a Command Prompt window in Windows or open a terminal in macOS or Ubuntu.</span></span>
2. <span data-ttu-id="6bb58-120">執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="6bb58-120">Run hello following commands:</span></span>

   ```bash
   git clone https://github.com/Azure-samples/iot-hub-c-intel-nuc-gateway-getting-started
   cd iot-hub-c-intel-nuc-gateway-getting-started
   ```

## <a name="set-up-hello-connectivity-between-sensortag-and-intel-nuc"></a><span data-ttu-id="6bb58-121">設定 hello SensorTag 和 Intel NUC 之間的連線</span><span class="sxs-lookup"><span data-stu-id="6bb58-121">Set up hello connectivity between SensorTag and Intel NUC</span></span>

<span data-ttu-id="6bb58-122">tooset 向上 hello 連線，請遵循下列步驟，在 hello 主機電腦上：</span><span class="sxs-lookup"><span data-stu-id="6bb58-122">tooset up hello connectivity, follow these steps on hello host computer:</span></span>

1. <span data-ttu-id="6bb58-123">藉由執行下列命令的 hello 初始化 hello 設定檔：</span><span class="sxs-lookup"><span data-stu-id="6bb58-123">Initialize hello configuration file by running hello following commands:</span></span>

   ```bash
   cd Lesson3
   npm install
   gulp init
   ```

2. <span data-ttu-id="6bb58-124">開啟`config-gateway.json`在 Visual Studio 程式碼執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="6bb58-124">Open `config-gateway.json` in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-gateway.json
   ```

3. <span data-ttu-id="6bb58-125">找出 hello 下列程式碼行並取代`[device hostname or IP address]`hello IP 位址或主機名稱為 Intel NUC。</span><span class="sxs-lookup"><span data-stu-id="6bb58-125">Locate hello following line of code and replace `[device hostname or IP address]` with hello IP address or host name of Intel NUC.</span></span>
   <span data-ttu-id="6bb58-126">![設定閘道器的螢幕擷取畫面](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)</span><span class="sxs-lookup"><span data-stu-id="6bb58-126">![screenshot of config gateway](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)</span></span>

4. <span data-ttu-id="6bb58-127">安裝在 Intel NUC 協助程式工具執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="6bb58-127">Install helper tools on Intel NUC by running hello following command:</span></span>

   ```bash
   gulp install-tools
   ```

5. <span data-ttu-id="6bb58-128">開啟 SensorTag 為 hello 下列圖片中，按下 hello 電源按鈕並 hello 綠色 LED 應閃爍。</span><span class="sxs-lookup"><span data-stu-id="6bb58-128">Turn on SensorTag by pressing hello power button as hello following picture, and hello green LED should blink.</span></span>

   ![開啟 SensorTag](media/iot-hub-gateway-kit-lessons/lesson3/turn on_off sensortag.jpg)

6. <span data-ttu-id="6bb58-130">藉由執行下列命令的 hello 掃描 SensorTag 裝置：</span><span class="sxs-lookup"><span data-stu-id="6bb58-130">Scan SensorTag devices by running hello following commands:</span></span>

   ```bash
   gulp discover-sensortag
   ```

7. <span data-ttu-id="6bb58-131">藉由執行下列命令的 hello 測試 hello hello SensorTag 和 Intel NUC 之間的連線：</span><span class="sxs-lookup"><span data-stu-id="6bb58-131">Test hello connectivity between hello SensorTag and Intel NUC by running hello following command:</span></span>

   ```bash
   gulp test-connectivity --mac {mac address}
   ```

   <span data-ttu-id="6bb58-132">取代`{mac address}`以 hello hello 先前步驟中取得的 MAC 位址。</span><span class="sxs-lookup"><span data-stu-id="6bb58-132">Replace `{mac address}` with hello MAC address that you obtained in hello previous step.</span></span>

## <a name="get-hello-connection-string-of-sensortag"></a><span data-ttu-id="6bb58-133">取得 SensorTag hello 連接字串</span><span class="sxs-lookup"><span data-stu-id="6bb58-133">Get hello connection string of SensorTag</span></span>

<span data-ttu-id="6bb58-134">tooget hello SensorTag，執行下列命令在 hello 主機電腦上的 hello Azure IoT 中樞連接字串：</span><span class="sxs-lookup"><span data-stu-id="6bb58-134">tooget hello Azure IoT hub connection string of SensorTag, run hello following command on hello host computer:</span></span>

```bash
az iot device show-connection-string --hub-name {IoT hub name} --device-id mydevice --resource-group iot-gateway
```

<span data-ttu-id="6bb58-135">`{IoT hub name}`是您所使用的 hello IoT 中樞名稱。</span><span class="sxs-lookup"><span data-stu-id="6bb58-135">`{IoT hub name}` is hello IoT hub name that you used.</span></span> <span data-ttu-id="6bb58-136">當做 hello 值使用 iot 閘道`{resource group name}`並用 mydevice 做為 hello 值`{device id}`如果您沒有變更 hello 課程 2 中的值。</span><span class="sxs-lookup"><span data-stu-id="6bb58-136">Use iot-gateway as hello value of `{resource group name}` and use mydevice as hello value of `{device id}` if you didn't change hello value in Lesson 2.</span></span>

## <a name="configure-hello-ble-sample-application"></a><span data-ttu-id="6bb58-137">Hello b 範例應用程式設定</span><span class="sxs-lookup"><span data-stu-id="6bb58-137">Configure hello BLE sample application</span></span>

<span data-ttu-id="6bb58-138">tooconfigure 和執行的 hello b 範例應用程式，請遵循下列步驟在 hello 主機電腦上：</span><span class="sxs-lookup"><span data-stu-id="6bb58-138">tooconfigure and run hello BLE sample application, follow these steps on hello host computer:</span></span>

1. <span data-ttu-id="6bb58-139">開啟`config-sensortag.json`在 Visual Studio 程式碼執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="6bb58-139">Open `config-sensortag.json` in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-sensortag.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-sensortag.json
   ```

   ![設定 sensortag 的螢幕擷取畫面](media/iot-hub-gateway-kit-lessons/lesson3/config_sensortag.png)

2. <span data-ttu-id="6bb58-141">請遵循取代 hello 程式碼中的 hello:</span><span class="sxs-lookup"><span data-stu-id="6bb58-141">Make hello following replacements in hello code:</span></span>
   - <span data-ttu-id="6bb58-142">取代`[IoT hub name]`與您所使用的 hello IoT 中樞名稱。</span><span class="sxs-lookup"><span data-stu-id="6bb58-142">Replace `[IoT hub name]` with hello IoT hub name that you used.</span></span>
   - <span data-ttu-id="6bb58-143">取代`[IoT device connection string]`與 hello SensorTag 取得的連接字串。</span><span class="sxs-lookup"><span data-stu-id="6bb58-143">Replace `[IoT device connection string]` with hello connection string of SensorTag that you obtained.</span></span>
   - <span data-ttu-id="6bb58-144">取代`[device_mac_address]`以 hello hello SensorTag 取得的 MAC 位址。</span><span class="sxs-lookup"><span data-stu-id="6bb58-144">Replace `[device_mac_address]` with hello MAC address of hello SensorTag that you obtained.</span></span>

3. <span data-ttu-id="6bb58-145">執行 hello b 範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="6bb58-145">Run hello BLE sample application.</span></span>

   <span data-ttu-id="6bb58-146">toorun hello b 範例應用程式，請遵循下列步驟，在 hello 主機電腦上：</span><span class="sxs-lookup"><span data-stu-id="6bb58-146">toorun hello BLE sample application, follow these steps on hello host computer:</span></span>

   1. <span data-ttu-id="6bb58-147">開啟 SensorTag。</span><span class="sxs-lookup"><span data-stu-id="6bb58-147">Turn on SensorTag.</span></span>

   2. <span data-ttu-id="6bb58-148">部署及執行 hello b 範例應用程式在 Intel NUC 上執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="6bb58-148">Deploy and run hello BLE sample application on Intel NUC by running hello following command:</span></span>
   
      ```bash
      gulp run
      ```

## <a name="verify-that-hello-ble-sample-application-works"></a><span data-ttu-id="6bb58-149">確認 hello b 範例應用程式可正常運作</span><span class="sxs-lookup"><span data-stu-id="6bb58-149">Verify that hello BLE sample application works</span></span>

<span data-ttu-id="6bb58-150">您現在應該會看到類似 hello 下列輸出：</span><span class="sxs-lookup"><span data-stu-id="6bb58-150">You should now see an output like hello following:</span></span>

![BLE 範例應用程式的輸出](media/iot-hub-gateway-kit-lessons/lesson3/BLE_running.png)

<span data-ttu-id="6bb58-152">hello 範例應用程式會持續收集溫度資料，並傳送它 tooyour IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="6bb58-152">hello sample application keeps collecting temperature data and sent it tooyour IoT hub.</span></span> <span data-ttu-id="6bb58-153">hello 範例應用程式會在傳送 40 秒後自動終止。</span><span class="sxs-lookup"><span data-stu-id="6bb58-153">hello sample application terminates automatically after sending 40 seconds.</span></span>

## <a name="summary"></a><span data-ttu-id="6bb58-154">摘要</span><span class="sxs-lookup"><span data-stu-id="6bb58-154">Summary</span></span>

<span data-ttu-id="6bb58-155">您已成功設定 hello SensorTag 和 Intel NUC 之間的連線，並執行會收集並傳送資料，從 SensorTag tooyour IoT 中樞 b 範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="6bb58-155">You've successfully set up hello connectivity between SensorTag and Intel NUC, and run a BLE sample application which collects and sends data from SensorTag tooyour IoT hub.</span></span> <span data-ttu-id="6bb58-156">您已準備好 toolearn tooverify 的 IoT 中樞收到 hello 資料的方式。</span><span class="sxs-lookup"><span data-stu-id="6bb58-156">You're ready toolearn how tooverify that your IoT hub has received hello data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6bb58-157">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6bb58-157">Next steps</span></span>
[<span data-ttu-id="6bb58-158">讀取來自 IoT 中樞的傳入訊息</span><span class="sxs-lookup"><span data-stu-id="6bb58-158">Read messages from your IoT hub</span></span>](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md)