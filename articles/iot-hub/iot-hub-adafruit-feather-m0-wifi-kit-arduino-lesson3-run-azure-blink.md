---
title: "將 Arduino (C) 連接到 Azure IoT - 第 3 課：執行範例 | Microsoft Docs"
description: "將範例應用程式部署至 Adafruit Feather M0 WiFi，並執行該應用程式以傳送訊息至 IoT 中樞並讓 LED 閃爍。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "iot 雲端服務, arduino 傳送資料到雲端"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 92cce319-2b17-4c9b-889d-deac959e3e7c
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 0c17fe74dbd78abca955f7789a1674ed6333367f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="run-a-sample-application-to-send-device-to-cloud-messages"></a><span data-ttu-id="e7f05-104">執行範例應用程式以傳送裝置到雲端訊息</span><span class="sxs-lookup"><span data-stu-id="e7f05-104">Run a sample application to send device-to-cloud messages</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="e7f05-105">將執行的作業</span><span class="sxs-lookup"><span data-stu-id="e7f05-105">What you will do</span></span>
<span data-ttu-id="e7f05-106">本文將說明如何將範例應用程式部署至 Adafruit Feather M0 WiFi Arduino 面板，並執行該應用程式以傳送訊息至 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="e7f05-106">This article will show you how to deploy and run a sample application on your Adafruit Feather M0 WiFi Arduino board that sends messages to your IoT hub.</span></span>

<span data-ttu-id="e7f05-107">如果您有任何問題，請在[疑難排解頁面][troubleshooting]尋求解決方案。</span><span class="sxs-lookup"><span data-stu-id="e7f05-107">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="e7f05-108">學習目標</span><span class="sxs-lookup"><span data-stu-id="e7f05-108">What you will learn</span></span>
<span data-ttu-id="e7f05-109">您將了解如何使用 gulp 工具將範例 Arduino 應用程式部署在 Arduino 面板上並執行。</span><span class="sxs-lookup"><span data-stu-id="e7f05-109">You will learn how to use the gulp tool to deploy and run the sample Arduino application on your Arduino board.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="e7f05-110">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="e7f05-110">What you need</span></span>
* <span data-ttu-id="e7f05-111">開始這項工作之前，您必須先成功完成[建立 Azure 函式應用程式與儲存體帳戶以處理與儲存 IoT 中樞訊息][process-and-store-iot-hub-messages]。</span><span class="sxs-lookup"><span data-stu-id="e7f05-111">Before you start this task, you must have successfully completed [Create an Azure function app and a storage account to process and store IoT hub messages][process-and-store-iot-hub-messages].</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="e7f05-112">取得 IoT 中樞與裝置連接字串</span><span class="sxs-lookup"><span data-stu-id="e7f05-112">Get your IoT hub and device connection strings</span></span>
<span data-ttu-id="e7f05-113">裝置連接字串用於將 Arduino 面板連線至 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="e7f05-113">The device connection string is used to connect your Arduino board to your IoT hub.</span></span> <span data-ttu-id="e7f05-114">IoT 中樞連接字串用於將 IoT 中樞連線至在 IoT 中樞內代表 Arduino 面板的裝置識別。</span><span class="sxs-lookup"><span data-stu-id="e7f05-114">The IoT hub connection string is used to connect your IoT hub to the device identity that represents your Arduino board in the IoT hub.</span></span>

* <span data-ttu-id="e7f05-115">執行下列 Azure CLI 命令，列出您的資源群組中的所有 IoT 中樞：</span><span class="sxs-lookup"><span data-stu-id="e7f05-115">List all your IoT hubs in your resource group by running the following Azure CLI command:</span></span>

```bash
az iot hub list -g iot-sample --query [].name
```

<span data-ttu-id="e7f05-116">如果您未變更值，請使用 `iot-sample` 作為 `{resource group name}` 的值。</span><span class="sxs-lookup"><span data-stu-id="e7f05-116">Use `iot-sample` as the value of `{resource group name}` if you didn't change the value.</span></span>

* <span data-ttu-id="e7f05-117">執行下列 Azure CLI 命令取得 IoT 中樞連接字串：</span><span class="sxs-lookup"><span data-stu-id="e7f05-117">Get the IoT hub connection string by running the following Azure CLI command:</span></span>

```bash
az iot hub show-connection-string --name {my hub name}
```

<span data-ttu-id="e7f05-118">`{my hub name}` 是您建立 IoT 中樞並登錄 Arduino 面板時所指定的名稱。</span><span class="sxs-lookup"><span data-stu-id="e7f05-118">`{my hub name}` is the name that you specified when you created your IoT hub and registered your Arduino board.</span></span>

* <span data-ttu-id="e7f05-119">執行下列命令來取得裝置連接字串：</span><span class="sxs-lookup"><span data-stu-id="e7f05-119">Get the device connection string by running the following command:</span></span>

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id mym0wifi
```

<span data-ttu-id="e7f05-120">如果您未變更值，請使用 `mym0wifi` 作為 `{device id}` 的值。</span><span class="sxs-lookup"><span data-stu-id="e7f05-120">Use `mym0wifi` as the value of `{device id}` if you didn't change the value.</span></span>
## <a name="configure-the-device-connection"></a><span data-ttu-id="e7f05-121">設定裝置連線</span><span class="sxs-lookup"><span data-stu-id="e7f05-121">Configure the device connection</span></span>
<span data-ttu-id="e7f05-122">若要設定裝置連線，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="e7f05-122">To configure the device connection, follow these steps:</span></span>

1. <span data-ttu-id="e7f05-123">透過裝置探索 cli 取得裝置的序列連接埠︰</span><span class="sxs-lookup"><span data-stu-id="e7f05-123">Obtain the serial port of the device with the device discovery cli:</span></span>

   ```bash
   devdisco list --usb
   ```

   <span data-ttu-id="e7f05-124">您應該會看到類似下列的輸出，並找到 Arduino 面板的 usb COM 連接埠︰</span><span class="sxs-lookup"><span data-stu-id="e7f05-124">You should see an output that is similar to the following and find the usb COM port for your Arduino board:</span></span>

   ![裝置探索][device-discovery]

2. <span data-ttu-id="e7f05-126">開啟課程資料夾中的 `config.json` 檔案並新增找到的 COM 連接埠號碼值︰</span><span class="sxs-lookup"><span data-stu-id="e7f05-126">Open the file `config.json` in the lesson folder and add the value of the found COM port number:</span></span>

   ```json
   {
       "device_port" : "COM1"
   }
   ```

   ![config.json][config-json]

   > [!NOTE]
   > <span data-ttu-id="e7f05-128">若為 COM 連接埠，其在 Windows 平台上的格式為 `COM1, COM2, ...`。</span><span class="sxs-lookup"><span data-stu-id="e7f05-128">For the COM port, on Windows platform, it has the format of `COM1, COM2, ...`.</span></span> <span data-ttu-id="e7f05-129">在 macOS 或 Ubuntu 上，它是以 `/dev/` 開頭。</span><span class="sxs-lookup"><span data-stu-id="e7f05-129">On macOS or Ubuntu, it starts with `/dev/`.</span></span>

3. <span data-ttu-id="e7f05-130">執行下列命令初始化組態檔：</span><span class="sxs-lookup"><span data-stu-id="e7f05-130">Initialize the configuration file by running the following commands:</span></span>

   ```bash
   npm install
   gulp init
   gulp install-tools
   ```
4. <span data-ttu-id="e7f05-131">執行下列命令在 Visual Studio Code 中開啟裝置組態檔 `config-arduino.json`：</span><span class="sxs-lookup"><span data-stu-id="e7f05-131">Open the device configuration file `config-arduino.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-arduino.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-arduino.json
   ```

   ![config-arduino.json][config-arduino-json]

5. <span data-ttu-id="e7f05-133">在 `config-arduino.json` 檔案中進行下列取代：</span><span class="sxs-lookup"><span data-stu-id="e7f05-133">Make the following replacements in the `config-arduino.json` file:</span></span>

   * <span data-ttu-id="e7f05-134">以連線至網際網路的 Wi-Fi SSID 取代 **[Wi-Fi SSID]**。</span><span class="sxs-lookup"><span data-stu-id="e7f05-134">Replace **[Wi-Fi SSID]** with your Wi-Fi SSID that connected to the Internet.</span></span>
   * <span data-ttu-id="e7f05-135">以 Wi-Fi 密碼取代 **[Wi-Fi password]**。</span><span class="sxs-lookup"><span data-stu-id="e7f05-135">Replace **[Wi-Fi password]** with your Wi-Fi password.</span></span> <span data-ttu-id="e7f05-136">如果 Wi-Fi 不需要密碼，請移除字串。</span><span class="sxs-lookup"><span data-stu-id="e7f05-136">Remove the string if your Wi-Fi doesn't require password.</span></span>
   * <span data-ttu-id="e7f05-137">以您取得的 `device connection string` 來取代 **[IoT device connection string]**。</span><span class="sxs-lookup"><span data-stu-id="e7f05-137">Replace **[IoT device connection string]** with the `device connection string` you obtained.</span></span>
   * <span data-ttu-id="e7f05-138">以您取得的 `iot hub connection string` 來取代 **[IoT hub connection string]**。</span><span class="sxs-lookup"><span data-stu-id="e7f05-138">Replace **[IoT hub connection string]** with the `iot hub connection string` you obtained.</span></span>

   > [!NOTE]
   > <span data-ttu-id="e7f05-139">您在本文中不需要 `azure_storage_connection_string`。</span><span class="sxs-lookup"><span data-stu-id="e7f05-139">You don't need `azure_storage_connection_string` in this article.</span></span> <span data-ttu-id="e7f05-140">請讓它保持原狀。</span><span class="sxs-lookup"><span data-stu-id="e7f05-140">Keep it as is.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="e7f05-141">部署和執行範例應用程式</span><span class="sxs-lookup"><span data-stu-id="e7f05-141">Deploy and run the sample application</span></span>
<span data-ttu-id="e7f05-142">執行下列命令，以在 Arduino 面板上部署和執行範例應用程式：</span><span class="sxs-lookup"><span data-stu-id="e7f05-142">Deploy and run the sample application on your Arduino board by running the following command:</span></span>

```bash
gulp run
# You can monitor the serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

> [!NOTE]
> <span data-ttu-id="e7f05-143">預設 gulp 工作會依序執行 `install-tools` 和 `run` 工作。</span><span class="sxs-lookup"><span data-stu-id="e7f05-143">The default gulp task runs `install-tools` and `run` tasks sequentially.</span></span> <span data-ttu-id="e7f05-144">當您[部署了閃爍應用程式][deployed-the-blink-app]時，您需要個別執行這些工作。</span><span class="sxs-lookup"><span data-stu-id="e7f05-144">When you [deployed the blink app][deployed-the-blink-app], you ran these tasks separately.</span></span>

## <a name="verify-that-the-sample-application-works"></a><span data-ttu-id="e7f05-145">確認範例應用程式可運作</span><span class="sxs-lookup"><span data-stu-id="e7f05-145">Verify that the sample application works</span></span>
<span data-ttu-id="e7f05-146">您應該會看到 GPIO #0 面板上的 LED 每兩秒閃爍一次。</span><span class="sxs-lookup"><span data-stu-id="e7f05-146">You should see the GPIO #0 on-board LED blinking every two seconds.</span></span> <span data-ttu-id="e7f05-147">每次 LED 閃爍時，範例應用程式就會將訊息傳送至 IoT 中樞，並驗證該訊息已成功傳送至 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="e7f05-147">Every time the LED blinks, the sample application sends a message to your IoT hub and verifies that the message has been successfully sent to your IoT hub.</span></span> <span data-ttu-id="e7f05-148">此外，IoT 中樞所收到的每則訊息都會列印在主控台視窗中。</span><span class="sxs-lookup"><span data-stu-id="e7f05-148">In addition, each message received by the IoT hub is printed in the console window.</span></span> <span data-ttu-id="e7f05-149">在傳送 20 則訊息後，範例應用程式會自動終止。</span><span class="sxs-lookup"><span data-stu-id="e7f05-149">The sample application terminates automatically after sending 20 messages.</span></span>

![具有所傳送和接收之訊息的範例應用程式][sample-application-with-sent-and-received-messages]

## <a name="summary"></a><span data-ttu-id="e7f05-151">摘要</span><span class="sxs-lookup"><span data-stu-id="e7f05-151">Summary</span></span>
<span data-ttu-id="e7f05-152">您已在 Arduino 面板上部署新的閃爍範例應用程式，並執行該應用程式以將裝置到雲端訊息傳送至 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="e7f05-152">You've deployed and run the new blink sample application on your Arduino board to send device-to-cloud messages to your IoT hub.</span></span> <span data-ttu-id="e7f05-153">現在，您可以在訊息寫入儲存體帳戶時加以監視。</span><span class="sxs-lookup"><span data-stu-id="e7f05-153">You now monitor your messages as they are written to the storage account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e7f05-154">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e7f05-154">Next steps</span></span>
<span data-ttu-id="e7f05-155">[讀取保存在 Azure 儲存體中的訊息][read-messages-persisted-in-azure-storage]</span><span class="sxs-lookup"><span data-stu-id="e7f05-155">[Read messages persisted in Azure Storage][read-messages-persisted-in-azure-storage]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-deploy-resource-manager-template.md
[device-discovery]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/device_discovery.png
[config-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-config-mac.png
[config-arduino-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/config-arduino.png
[deployed-the-blink-app]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-deploy-blink-app.md
[sample-application-with-sent-and-received-messages]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/gulp_run_arduino.png
[read-messages-persisted-in-azure-storage]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-read-table-storage.md