---
title: "SensorTag 裝置與 Azure IoT 閘道 - 第 3 課︰執行範例應用程式 | Microsoft Docs"
description: "執行 BLE 範例應用程式，從 SensorTag 和您的 IoT 中樞接收資料。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "ble 應用程式, 感應器監視應用程式, 感應器資料收集, 來自感應器的資料, 送至雲端的感應器資料"
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
ms.openlocfilehash: f6fa158dbe1d48be7d493efa6217e1e0a759d2f2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="configure-and-run-a-ble-sample-application"></a><span data-ttu-id="d316c-104">設定和執行 BLE 範例應用程式</span><span class="sxs-lookup"><span data-stu-id="d316c-104">Configure and run a BLE sample application</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="d316c-105">將執行的作業</span><span class="sxs-lookup"><span data-stu-id="d316c-105">What you will do</span></span>

- <span data-ttu-id="d316c-106">複製範例存放庫。</span><span class="sxs-lookup"><span data-stu-id="d316c-106">Clone the sample repository.</span></span> 
- <span data-ttu-id="d316c-107">設定 SensorTag 與 Intel NUC 之間的連線。</span><span class="sxs-lookup"><span data-stu-id="d316c-107">Set up the connectivity between SensorTag and Intel NUC.</span></span> 
- <span data-ttu-id="d316c-108">使用 Azure CLI 取得 IoT 中樞和 SensorTag 的 BLE (Bluetooth Low Energy) 範例應用程式的資訊。</span><span class="sxs-lookup"><span data-stu-id="d316c-108">Use the Azure CLI to get your IoT hub and SensorTag information for a BLE(Bluetooth Low Energy) sample application.</span></span> <span data-ttu-id="d316c-109">然後設定並執行 BLE 範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="d316c-109">And configure and run the BLE sample application.</span></span> 

<span data-ttu-id="d316c-110">如果您有任何問題，請在[疑難排解頁面](iot-hub-gateway-kit-c-troubleshooting.md)尋求解決方案。</span><span class="sxs-lookup"><span data-stu-id="d316c-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="d316c-111">學習目標</span><span class="sxs-lookup"><span data-stu-id="d316c-111">What you will learn</span></span>

<span data-ttu-id="d316c-112">在本文中，您將了解：</span><span class="sxs-lookup"><span data-stu-id="d316c-112">In this article, you will learn:</span></span>

- <span data-ttu-id="d316c-113">如何設定和執行 BLE 範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="d316c-113">How to configure and run the BLE sample application.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="d316c-114">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="d316c-114">What you need</span></span>

<span data-ttu-id="d316c-115">您必須已成功完成</span><span class="sxs-lookup"><span data-stu-id="d316c-115">You must have successfully completed</span></span>

- [<span data-ttu-id="d316c-116">建立 IoT 中樞並登錄裝置</span><span class="sxs-lookup"><span data-stu-id="d316c-116">Create an IoT hub and register SensorTag</span></span>](iot-hub-gateway-kit-c-lesson2-register-device.md)

## <a name="clone-the-sample-repository-to-the-host-computer"></a><span data-ttu-id="d316c-117">將範例存放庫複製至主機電腦</span><span class="sxs-lookup"><span data-stu-id="d316c-117">Clone the sample repository to the host computer</span></span>

<span data-ttu-id="d316c-118">若要複製範例存放庫，在主機電腦上遵循下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="d316c-118">To clone the sample repository, follow these steps on the host computer:</span></span>

1. <span data-ttu-id="d316c-119">在 Windows 上開啟命令提示字元視窗，或在 macOS 或 Ubuntu 上開啟終端機。</span><span class="sxs-lookup"><span data-stu-id="d316c-119">Open a Command Prompt window in Windows or open a terminal in macOS or Ubuntu.</span></span>
2. <span data-ttu-id="d316c-120">執行以下命令：</span><span class="sxs-lookup"><span data-stu-id="d316c-120">Run the following commands:</span></span>

   ```bash
   git clone https://github.com/Azure-samples/iot-hub-c-intel-nuc-gateway-getting-started
   cd iot-hub-c-intel-nuc-gateway-getting-started
   ```

## <a name="set-up-the-connectivity-between-sensortag-and-intel-nuc"></a><span data-ttu-id="d316c-121">設定 SensorTag 與 Intel NUC 之間的連線</span><span class="sxs-lookup"><span data-stu-id="d316c-121">Set up the connectivity between SensorTag and Intel NUC</span></span>

<span data-ttu-id="d316c-122">若要設定連線，在主機電腦上遵循下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="d316c-122">To set up the connectivity, follow these steps on the host computer:</span></span>

1. <span data-ttu-id="d316c-123">執行下列命令初始化組態檔：</span><span class="sxs-lookup"><span data-stu-id="d316c-123">Initialize the configuration file by running the following commands:</span></span>

   ```bash
   cd Lesson3
   npm install
   gulp init
   ```

2. <span data-ttu-id="d316c-124">執行下列命令在 Visual Studio Code 中開啟 `config-gateway.json`︰</span><span class="sxs-lookup"><span data-stu-id="d316c-124">Open `config-gateway.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-gateway.json
   ```

3. <span data-ttu-id="d316c-125">找到下列這行程式碼，並將 `[device hostname or IP address]` 取代為 Intel NUC 的 IP 位址或主機名稱。</span><span class="sxs-lookup"><span data-stu-id="d316c-125">Locate the following line of code and replace `[device hostname or IP address]` with the IP address or host name of Intel NUC.</span></span>
   <span data-ttu-id="d316c-126">![設定閘道器的螢幕擷取畫面](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)</span><span class="sxs-lookup"><span data-stu-id="d316c-126">![screenshot of config gateway](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)</span></span>

4. <span data-ttu-id="d316c-127">執行下列命令，在 Intel NUC 上安裝協助程式工具︰</span><span class="sxs-lookup"><span data-stu-id="d316c-127">Install helper tools on Intel NUC by running the following command:</span></span>

   ```bash
   gulp install-tools
   ```

5. <span data-ttu-id="d316c-128">按下電源按鈕 (如下圖) 開啟 SensorTag，綠色 LED 應該會閃爍。</span><span class="sxs-lookup"><span data-stu-id="d316c-128">Turn on SensorTag by pressing the power button as the following picture, and the green LED should blink.</span></span>

   ![開啟 SensorTag](media/iot-hub-gateway-kit-lessons/lesson3/turn on_off sensortag.jpg)

6. <span data-ttu-id="d316c-130">執行下列命令來掃描 SensorTag 裝置：</span><span class="sxs-lookup"><span data-stu-id="d316c-130">Scan SensorTag devices by running the following commands:</span></span>

   ```bash
   gulp discover-sensortag
   ```

7. <span data-ttu-id="d316c-131">執行下列命令測試 SensorTag 和 Intel NUC 之間的連線︰</span><span class="sxs-lookup"><span data-stu-id="d316c-131">Test the connectivity between the SensorTag and Intel NUC by running the following command:</span></span>

   ```bash
   gulp test-connectivity --mac {mac address}
   ```

   <span data-ttu-id="d316c-132">將 `{mac address}` 取代為您在先前步驟取得的 MAC 位址。</span><span class="sxs-lookup"><span data-stu-id="d316c-132">Replace `{mac address}` with the MAC address that you obtained in the previous step.</span></span>

## <a name="get-the-connection-string-of-sensortag"></a><span data-ttu-id="d316c-133">取得 SensorTag 的連接字串</span><span class="sxs-lookup"><span data-stu-id="d316c-133">Get the connection string of SensorTag</span></span>

<span data-ttu-id="d316c-134">若要取得 SensorTag 的 Azure IoT 中樞連接字串，在主機電腦上執行下列命令︰</span><span class="sxs-lookup"><span data-stu-id="d316c-134">To get the Azure IoT hub connection string of SensorTag, run the following command on the host computer:</span></span>

```bash
az iot device show-connection-string --hub-name {IoT hub name} --device-id mydevice --resource-group iot-gateway
```

<span data-ttu-id="d316c-135">`{IoT hub name}` 是您所使用的 IoT 中樞名稱。</span><span class="sxs-lookup"><span data-stu-id="d316c-135">`{IoT hub name}` is the IoT hub name that you used.</span></span> <span data-ttu-id="d316c-136">如果您在第 2 課沒有變更值，使用 iot-gateway 作為 `{resource group name}` 的值，使用 mydevice 作為 `{device id}` 的值。</span><span class="sxs-lookup"><span data-stu-id="d316c-136">Use iot-gateway as the value of `{resource group name}` and use mydevice as the value of `{device id}` if you didn't change the value in Lesson 2.</span></span>

## <a name="configure-the-ble-sample-application"></a><span data-ttu-id="d316c-137">設定 BLE 範例應用程式</span><span class="sxs-lookup"><span data-stu-id="d316c-137">Configure the BLE sample application</span></span>

<span data-ttu-id="d316c-138">若要設定及執行 BLE 範例應用程式，在主機電腦上遵循下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="d316c-138">To configure and run the BLE sample application, follow these steps on the host computer:</span></span>

1. <span data-ttu-id="d316c-139">執行下列命令在 Visual Studio Code 中開啟 `config-sensortag.json`︰</span><span class="sxs-lookup"><span data-stu-id="d316c-139">Open `config-sensortag.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-sensortag.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-sensortag.json
   ```

   ![設定 sensortag 的螢幕擷取畫面](media/iot-hub-gateway-kit-lessons/lesson3/config_sensortag.png)

2. <span data-ttu-id="d316c-141">取代程式碼中的下列內容：</span><span class="sxs-lookup"><span data-stu-id="d316c-141">Make the following replacements in the code:</span></span>
   - <span data-ttu-id="d316c-142">將 `[IoT hub name]` 取代為您使用的 IoT 中樞名稱。</span><span class="sxs-lookup"><span data-stu-id="d316c-142">Replace `[IoT hub name]` with the IoT hub name that you used.</span></span>
   - <span data-ttu-id="d316c-143">將 `[IoT device connection string]` 取代為您取得的 SensorTag 連接字串。</span><span class="sxs-lookup"><span data-stu-id="d316c-143">Replace `[IoT device connection string]` with the connection string of SensorTag that you obtained.</span></span>
   - <span data-ttu-id="d316c-144">將 `[device_mac_address]` 取代為您取得的 MAC 位址。</span><span class="sxs-lookup"><span data-stu-id="d316c-144">Replace `[device_mac_address]` with the MAC address of the SensorTag that you obtained.</span></span>

3. <span data-ttu-id="d316c-145">執行 BLE 範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="d316c-145">Run the BLE sample application.</span></span>

   <span data-ttu-id="d316c-146">若要執行 BLE 範例應用程式，在主機電腦上遵循下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="d316c-146">To run the BLE sample application, follow these steps on the host computer:</span></span>

   1. <span data-ttu-id="d316c-147">開啟 SensorTag。</span><span class="sxs-lookup"><span data-stu-id="d316c-147">Turn on SensorTag.</span></span>

   2. <span data-ttu-id="d316c-148">執行下列命令在 Intel NUC 上部署及執行 BLE 範例應用程式：</span><span class="sxs-lookup"><span data-stu-id="d316c-148">Deploy and run the BLE sample application on Intel NUC by running the following command:</span></span>
   
      ```bash
      gulp run
      ```

## <a name="verify-that-the-ble-sample-application-works"></a><span data-ttu-id="d316c-149">確認 BLE 範例應用程式可運作</span><span class="sxs-lookup"><span data-stu-id="d316c-149">Verify that the BLE sample application works</span></span>

<span data-ttu-id="d316c-150">您現在應該會看到如下的輸出：</span><span class="sxs-lookup"><span data-stu-id="d316c-150">You should now see an output like the following:</span></span>

![BLE 範例應用程式的輸出](media/iot-hub-gateway-kit-lessons/lesson3/BLE_running.png)

<span data-ttu-id="d316c-152">範例應用程式會收集溫度資料，並傳送至您的 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="d316c-152">The sample application keeps collecting temperature data and sent it to your IoT hub.</span></span> <span data-ttu-id="d316c-153">範例應用程式會在傳送 40 則訊息後自動終止。</span><span class="sxs-lookup"><span data-stu-id="d316c-153">The sample application terminates automatically after sending 40 seconds.</span></span>

## <a name="summary"></a><span data-ttu-id="d316c-154">摘要</span><span class="sxs-lookup"><span data-stu-id="d316c-154">Summary</span></span>

<span data-ttu-id="d316c-155">您已成功設定 SensorTag 和 Intel NUC 之間的連線，並且執行 BLE 範例應用程式從 SensorTag 收集資料並將資料傳送至您的 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="d316c-155">You've successfully set up the connectivity between SensorTag and Intel NUC, and run a BLE sample application which collects and sends data from SensorTag to your IoT hub.</span></span> <span data-ttu-id="d316c-156">您可以開始了解如何確認 IoT 中樞是否已收到資料。</span><span class="sxs-lookup"><span data-stu-id="d316c-156">You're ready to learn how to verify that your IoT hub has received the data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d316c-157">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d316c-157">Next steps</span></span>
[<span data-ttu-id="d316c-158">讀取來自 IoT 中樞的傳入訊息</span><span class="sxs-lookup"><span data-stu-id="d316c-158">Read messages from your IoT hub</span></span>](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md)