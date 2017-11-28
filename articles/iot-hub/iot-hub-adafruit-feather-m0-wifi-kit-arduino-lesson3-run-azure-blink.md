---
title: "Connect Arduino (C) tooAzure IoT-第 3 課： 執行範例 |Microsoft 文件"
description: "部署和執行範例應用程式 tooAdafruit 羽毛 M0 WiFi 傳送訊息 tooyour IoT 中樞和閃爍 hello LED。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "iot 雲端服務，arduino 傳送資料 toocloud"
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
ms.openlocfilehash: ddca015a3655f8a1a9de2a00e718ec0d28a5affb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-toosend-device-to-cloud-messages"></a><span data-ttu-id="51657-104">執行範例應用程式 toosend 裝置到雲端訊息</span><span class="sxs-lookup"><span data-stu-id="51657-104">Run a sample application toosend device-to-cloud messages</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="51657-105">將執行的作業</span><span class="sxs-lookup"><span data-stu-id="51657-105">What you will do</span></span>
<span data-ttu-id="51657-106">本文將告訴您 toodeploy 及執行範例應用程式上 Adafruit 羽毛 M0 WiFi Arduino board 該傳送訊息 tooyour IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="51657-106">This article will show you how toodeploy and run a sample application on your Adafruit Feather M0 WiFi Arduino board that sends messages tooyour IoT hub.</span></span>

<span data-ttu-id="51657-107">如果您有任何問題，尋找解決方案上 hello[疑難排解頁面][troubleshooting]。</span><span class="sxs-lookup"><span data-stu-id="51657-107">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="51657-108">學習目標</span><span class="sxs-lookup"><span data-stu-id="51657-108">What you will learn</span></span>
<span data-ttu-id="51657-109">您將學習如何 toouse hello 的 gulp 工具 toodeploy 和 Arduino 面板上執行 hello 範例 Arduino 應用程式。</span><span class="sxs-lookup"><span data-stu-id="51657-109">You will learn how toouse hello gulp tool toodeploy and run hello sample Arduino application on your Arduino board.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="51657-110">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="51657-110">What you need</span></span>
* <span data-ttu-id="51657-111">在開始這項工作之前，您必須已順利完成[建立 Azure 的函式應用程式與儲存體帳戶 tooprocess 和市集 IoT 中樞訊息][process-and-store-iot-hub-messages]。</span><span class="sxs-lookup"><span data-stu-id="51657-111">Before you start this task, you must have successfully completed [Create an Azure function app and a storage account tooprocess and store IoT hub messages][process-and-store-iot-hub-messages].</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="51657-112">取得 IoT 中樞與裝置連接字串</span><span class="sxs-lookup"><span data-stu-id="51657-112">Get your IoT hub and device connection strings</span></span>
<span data-ttu-id="51657-113">hello 裝置連接字串是使用的 tooconnect Arduino 面板 tooyour IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="51657-113">hello device connection string is used tooconnect your Arduino board tooyour IoT hub.</span></span> <span data-ttu-id="51657-114">hello IoT 中樞連接字串是使用的 tooconnect 您 IoT 中樞 toohello 裝置身分識別，表示您 Arduino 面板在 hello IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="51657-114">hello IoT hub connection string is used tooconnect your IoT hub toohello device identity that represents your Arduino board in hello IoT hub.</span></span>

* <span data-ttu-id="51657-115">列出資源群組中的所有您 IoT 中樞執行下列 Azure CLI 命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="51657-115">List all your IoT hubs in your resource group by running hello following Azure CLI command:</span></span>

```bash
az iot hub list -g iot-sample --query [].name
```

<span data-ttu-id="51657-116">使用`iot-sample`做為 hello 值`{resource group name}`如果您沒有變更 hello 值。</span><span class="sxs-lookup"><span data-stu-id="51657-116">Use `iot-sample` as hello value of `{resource group name}` if you didn't change hello value.</span></span>

* <span data-ttu-id="51657-117">藉由執行下列 Azure CLI 命令的 hello 收到 hello IoT 中樞連接字串：</span><span class="sxs-lookup"><span data-stu-id="51657-117">Get hello IoT hub connection string by running hello following Azure CLI command:</span></span>

```bash
az iot hub show-connection-string --name {my hub name}
```

<span data-ttu-id="51657-118">`{my hub name}`這是您指定當您建立 IoT 中樞，並註冊 Arduino 面板 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="51657-118">`{my hub name}` is hello name that you specified when you created your IoT hub and registered your Arduino board.</span></span>

* <span data-ttu-id="51657-119">藉由執行下列命令的 hello 收到 hello 裝置連接字串：</span><span class="sxs-lookup"><span data-stu-id="51657-119">Get hello device connection string by running hello following command:</span></span>

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id mym0wifi
```

<span data-ttu-id="51657-120">使用`mym0wifi`做為 hello 值`{device id}`如果您沒有變更 hello 值。</span><span class="sxs-lookup"><span data-stu-id="51657-120">Use `mym0wifi` as hello value of `{device id}` if you didn't change hello value.</span></span>
## <a name="configure-hello-device-connection"></a><span data-ttu-id="51657-121">設定 hello 裝置連線</span><span class="sxs-lookup"><span data-stu-id="51657-121">Configure hello device connection</span></span>
<span data-ttu-id="51657-122">tooconfigure hello 裝置連線，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="51657-122">tooconfigure hello device connection, follow these steps:</span></span>

1. <span data-ttu-id="51657-123">取得 hello hello 裝置探索 cli hello 裝置的序列通訊埠：</span><span class="sxs-lookup"><span data-stu-id="51657-123">Obtain hello serial port of hello device with hello device discovery cli:</span></span>

   ```bash
   devdisco list --usb
   ```

   <span data-ttu-id="51657-124">您應該看到的類似 toohello 下列輸出，並尋找 Arduino 面板 hello usb COM 連接埠：</span><span class="sxs-lookup"><span data-stu-id="51657-124">You should see an output that is similar toohello following and find hello usb COM port for your Arduino board:</span></span>

   ![裝置探索][device-discovery]

2. <span data-ttu-id="51657-126">開啟 hello 檔案`config.json`在 hello 課程資料夾並加入 hello 的 hello 找到 COM 連接埠號碼的值：</span><span class="sxs-lookup"><span data-stu-id="51657-126">Open hello file `config.json` in hello lesson folder and add hello value of hello found COM port number:</span></span>

   ```json
   {
       "device_port" : "COM1"
   }
   ```

   ![config.json][config-json]

   > [!NOTE]
   > <span data-ttu-id="51657-128">Hello COM 連接埠，Windows 平台上，它有 hello 格式`COM1, COM2, ...`。</span><span class="sxs-lookup"><span data-stu-id="51657-128">For hello COM port, on Windows platform, it has hello format of `COM1, COM2, ...`.</span></span> <span data-ttu-id="51657-129">在 macOS 或 Ubuntu 上，它是以 `/dev/` 開頭。</span><span class="sxs-lookup"><span data-stu-id="51657-129">On macOS or Ubuntu, it starts with `/dev/`.</span></span>

3. <span data-ttu-id="51657-130">藉由執行下列命令的 hello 初始化 hello 設定檔：</span><span class="sxs-lookup"><span data-stu-id="51657-130">Initialize hello configuration file by running hello following commands:</span></span>

   ```bash
   npm install
   gulp init
   gulp install-tools
   ```
4. <span data-ttu-id="51657-131">開啟 hello 裝置組態檔`config-arduino.json`在 Visual Studio 程式碼執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="51657-131">Open hello device configuration file `config-arduino.json` in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-arduino.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-arduino.json
   ```

   ![config-arduino.json][config-arduino-json]

5. <span data-ttu-id="51657-133">請遵循取代 hello hello`config-arduino.json`檔案：</span><span class="sxs-lookup"><span data-stu-id="51657-133">Make hello following replacements in hello `config-arduino.json` file:</span></span>

   * <span data-ttu-id="51657-134">取代**[Wi-fi SSID]**具有連接 toohello 網際網路您 Wi-fi SSID。</span><span class="sxs-lookup"><span data-stu-id="51657-134">Replace **[Wi-Fi SSID]** with your Wi-Fi SSID that connected toohello Internet.</span></span>
   * <span data-ttu-id="51657-135">以 Wi-Fi 密碼取代 **[Wi-Fi password]**。</span><span class="sxs-lookup"><span data-stu-id="51657-135">Replace **[Wi-Fi password]** with your Wi-Fi password.</span></span> <span data-ttu-id="51657-136">如果您 Wi-fi 不需要密碼，請移除 hello 字串。</span><span class="sxs-lookup"><span data-stu-id="51657-136">Remove hello string if your Wi-Fi doesn't require password.</span></span>
   * <span data-ttu-id="51657-137">取代**[IoT 裝置連接字串]**以 hello`device connection string`您取得的。</span><span class="sxs-lookup"><span data-stu-id="51657-137">Replace **[IoT device connection string]** with hello `device connection string` you obtained.</span></span>
   * <span data-ttu-id="51657-138">取代**[IoT 中樞連接字串]**以 hello`iot hub connection string`您取得的。</span><span class="sxs-lookup"><span data-stu-id="51657-138">Replace **[IoT hub connection string]** with hello `iot hub connection string` you obtained.</span></span>

   > [!NOTE]
   > <span data-ttu-id="51657-139">您在本文中不需要 `azure_storage_connection_string`。</span><span class="sxs-lookup"><span data-stu-id="51657-139">You don't need `azure_storage_connection_string` in this article.</span></span> <span data-ttu-id="51657-140">請讓它保持原狀。</span><span class="sxs-lookup"><span data-stu-id="51657-140">Keep it as is.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="51657-141">部署和執行 hello 範例應用程式</span><span class="sxs-lookup"><span data-stu-id="51657-141">Deploy and run hello sample application</span></span>
<span data-ttu-id="51657-142">部署和執行 hello 範例應用程式 Arduino 面板上，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="51657-142">Deploy and run hello sample application on your Arduino board by running hello following command:</span></span>

```bash
gulp run
# You can monitor hello serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

> [!NOTE]
> <span data-ttu-id="51657-143">hello 預設 gulp 工作執行`install-tools`和`run`循序的工作。</span><span class="sxs-lookup"><span data-stu-id="51657-143">hello default gulp task runs `install-tools` and `run` tasks sequentially.</span></span> <span data-ttu-id="51657-144">當您[hello 閃爍應用程式部署][deployed-the-blink-app]，個別執行這些工作。</span><span class="sxs-lookup"><span data-stu-id="51657-144">When you [deployed hello blink app][deployed-the-blink-app], you ran these tasks separately.</span></span>

## <a name="verify-that-hello-sample-application-works"></a><span data-ttu-id="51657-145">確認 hello 範例應用程式可正常運作</span><span class="sxs-lookup"><span data-stu-id="51657-145">Verify that hello sample application works</span></span>
<span data-ttu-id="51657-146">您應該會看到 hello GPIO #0 主機板 LED 閃爍不停每隔兩秒鐘。</span><span class="sxs-lookup"><span data-stu-id="51657-146">You should see hello GPIO #0 on-board LED blinking every two seconds.</span></span> <span data-ttu-id="51657-147">每次 hello LED 閃爍，hello 範例應用程式傳送訊息 tooyour IoT 中樞，並確認該 hello 訊息已成功傳送 tooyour IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="51657-147">Every time hello LED blinks, hello sample application sends a message tooyour IoT hub and verifies that hello message has been successfully sent tooyour IoT hub.</span></span> <span data-ttu-id="51657-148">此外，收到 hello IoT 中樞的每個訊息會列印 hello 主控台視窗中。</span><span class="sxs-lookup"><span data-stu-id="51657-148">In addition, each message received by hello IoT hub is printed in hello console window.</span></span> <span data-ttu-id="51657-149">hello 範例應用程式會自動終止後傳送 20 則訊息。</span><span class="sxs-lookup"><span data-stu-id="51657-149">hello sample application terminates automatically after sending 20 messages.</span></span>

![具有所傳送和接收之訊息的範例應用程式][sample-application-with-sent-and-received-messages]

## <a name="summary"></a><span data-ttu-id="51657-151">摘要</span><span class="sxs-lookup"><span data-stu-id="51657-151">Summary</span></span>
<span data-ttu-id="51657-152">您部署，並在您 Arduino 面板 toosend 裝置到雲端訊息 tooyour IoT 中樞執行 hello 新閃爍範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="51657-152">You've deployed and run hello new blink sample application on your Arduino board toosend device-to-cloud messages tooyour IoT hub.</span></span> <span data-ttu-id="51657-153">您現在監視您的郵件將它們寫入 toohello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="51657-153">You now monitor your messages as they are written toohello storage account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="51657-154">後續步驟</span><span class="sxs-lookup"><span data-stu-id="51657-154">Next steps</span></span>
<span data-ttu-id="51657-155">[讀取保存在 Azure 儲存體中的訊息][read-messages-persisted-in-azure-storage]</span><span class="sxs-lookup"><span data-stu-id="51657-155">[Read messages persisted in Azure Storage][read-messages-persisted-in-azure-storage]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-deploy-resource-manager-template.md
[device-discovery]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/device_discovery.png
[config-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-config-mac.png
[config-arduino-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/config-arduino.png
[deployed-the-blink-app]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-deploy-blink-app.md
[sample-application-with-sent-and-received-messages]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/gulp_run_arduino.png
[read-messages-persisted-in-azure-storage]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-read-table-storage.md