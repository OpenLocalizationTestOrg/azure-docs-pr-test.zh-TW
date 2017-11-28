---
title: "將 Arduino 連接到 Azure IoT - 第 1 課：部署應用程式 | Microsoft Docs"
description: "從 GitHub 複製範例 Arduino 應用程式，並執行 gulp 以將此應用程式部署至您的 Adafruit Feather M0 WiFi。 此範例應用程式會閃爍 GPIO"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "arduino led 專案, arduino led 閃爍, arduino led 閃爍程式碼, arduino 閃爍程式, arduino 閃爍範例"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: b0a7d076-d580-4686-9f7d-c0712750b615
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 4431808ac6182d194e841c087c8f89f1a12b1911
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-deploy-the-blink-application"></a><span data-ttu-id="98ea7-105">建立並部署閃爍應用程式</span><span class="sxs-lookup"><span data-stu-id="98ea7-105">Create and deploy the blink application</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="98ea7-106">將執行的作業</span><span class="sxs-lookup"><span data-stu-id="98ea7-106">What you will do</span></span>
<span data-ttu-id="98ea7-107">從 GitHub 複製範例 Arduino 應用程式，並使用 gulp 工具將範例應用程式部署至您的 Adafruit Feather M0 WiFi Arduino 面板。</span><span class="sxs-lookup"><span data-stu-id="98ea7-107">Clone the sample Arduino application from GitHub, and use the gulp tool to deploy the sample application to your Adafruit Feather M0 WiFi Arduino board.</span></span> <span data-ttu-id="98ea7-108">範例應用程式會讓 GPIO #13 面板上的 LED 每兩秒閃爍一次。</span><span class="sxs-lookup"><span data-stu-id="98ea7-108">The sample application blinks the GPIO #13 on-barod LED every two seconds.</span></span>

<span data-ttu-id="98ea7-109">如果您有任何問題，請在[疑難排解頁面][troubleshooting-page]尋求解決方案。</span><span class="sxs-lookup"><span data-stu-id="98ea7-109">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting-page].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="98ea7-110">學習目標</span><span class="sxs-lookup"><span data-stu-id="98ea7-110">What you will learn</span></span>
* <span data-ttu-id="98ea7-111">如何在 Arduino 面板上部署和執行範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="98ea7-111">How to deploy and run the sample application on your Arduino board.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="98ea7-112">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="98ea7-112">What you need</span></span>
<span data-ttu-id="98ea7-113">您必須已順利完成下列作業︰</span><span class="sxs-lookup"><span data-stu-id="98ea7-113">You must have successfully completed the following operations:</span></span>

* <span data-ttu-id="98ea7-114">[設定裝置][configure-your-device]</span><span class="sxs-lookup"><span data-stu-id="98ea7-114">[Configure your device][configure-your-device]</span></span>
* <span data-ttu-id="98ea7-115">[取得工具][get-the-tools]</span><span class="sxs-lookup"><span data-stu-id="98ea7-115">[Get the tools][get-the-tools]</span></span>

## <a name="open-the-sample-application"></a><span data-ttu-id="98ea7-116">開啟範例應用程式</span><span class="sxs-lookup"><span data-stu-id="98ea7-116">Open the sample application</span></span>
<span data-ttu-id="98ea7-117">若要開啟範例應用程式，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="98ea7-117">To open the sample application, follow these steps:</span></span>

1. <span data-ttu-id="98ea7-118">執行下列命令，從 GitHub 複製範例儲存機制︰</span><span class="sxs-lookup"><span data-stu-id="98ea7-118">Clone the sample repository from GitHub by running the following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-c-feather-m0-getting-started.git
   ```
2. <span data-ttu-id="98ea7-119">執行下列命令來在 Visual Studio Code 中開啟範例應用程式︰</span><span class="sxs-lookup"><span data-stu-id="98ea7-119">Open the sample application in Visual Studio Code by running the following commands:</span></span>

   ```bash
   cd iot-hub-c-feather-m0-getting-started
   cd Lesson1
   code .
   ```

   ![儲存機制結構][repo-structure]

<span data-ttu-id="98ea7-121">`app` 子資料夾中的 `app.ino` 檔案是包含 LED 控制程式碼的關鍵來源檔案。</span><span class="sxs-lookup"><span data-stu-id="98ea7-121">The `app.ino` file in the `app` subfolder is the key source file that contains the code to control the LED.</span></span>

### <a name="install-application-dependencies"></a><span data-ttu-id="98ea7-122">安裝應用程式相依性</span><span class="sxs-lookup"><span data-stu-id="98ea7-122">Install application dependencies</span></span>
<span data-ttu-id="98ea7-123">執行下列命令，安裝範例應用程式需要的程式庫和其他模組︰</span><span class="sxs-lookup"><span data-stu-id="98ea7-123">Install the libraries and other modules you need for the sample application by running the following command:</span></span>

```bash
npm install
```

## <a name="configure-the-device-connection"></a><span data-ttu-id="98ea7-124">設定裝置連線</span><span class="sxs-lookup"><span data-stu-id="98ea7-124">Configure the device connection</span></span>
<span data-ttu-id="98ea7-125">若要設定裝置連線，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="98ea7-125">To configure the device connection, follow these steps:</span></span>

1. <span data-ttu-id="98ea7-126">透過裝置探索 cli 取得裝置的序列連接埠︰</span><span class="sxs-lookup"><span data-stu-id="98ea7-126">Obtain the serial port of the device with the device discovery cli:</span></span>

   ```bash
   devdisco list --usb
   ```

   <span data-ttu-id="98ea7-127">您應該會看到類似下列的輸出，並尋找 Arduino 面板的 usb COM 連接埠︰![裝置探索][device-discovery]</span><span class="sxs-lookup"><span data-stu-id="98ea7-127">You should see an output that is similar to the following and find the usb COM port for your Arduino board: ![Device discovery][device-discovery]</span></span>

2. <span data-ttu-id="98ea7-128">開啟課程資料夾中的 `config.json` 檔案並新增找到的 COM 連接埠號碼值︰</span><span class="sxs-lookup"><span data-stu-id="98ea7-128">Open the file `config.json` in the lesson folder and add the value of the found COM port number:</span></span>

   ```json
   {
       "device_port" : "COM1"
   }
   ```
   ![config.json][config-json]
   > [!NOTE]
   > <span data-ttu-id="98ea7-130">若為 COM 連接埠，其在 Windows 平台上的格式為 `COM1, COM2, ...`。</span><span class="sxs-lookup"><span data-stu-id="98ea7-130">For the COM port, on Windows platform, it has the format of `COM1, COM2, ...`.</span></span> <span data-ttu-id="98ea7-131">在 macOS 或 Ubuntu 上，它是以 `/dev/` 開頭。</span><span class="sxs-lookup"><span data-stu-id="98ea7-131">On macOS or Ubuntu, it starts with `/dev/`.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="98ea7-132">部署和執行範例應用程式</span><span class="sxs-lookup"><span data-stu-id="98ea7-132">Deploy and run the sample application</span></span>
### <a name="install-the-required-tools-for-your-arduino-board"></a><span data-ttu-id="98ea7-133">安裝 Arduino 面板的必要工具</span><span class="sxs-lookup"><span data-stu-id="98ea7-133">Install the required tools for your Arduino board</span></span>

<span data-ttu-id="98ea7-134">執行下列命令，為 Arduino 面板安裝 Azure IoT 中樞 SDK：</span><span class="sxs-lookup"><span data-stu-id="98ea7-134">Install the Azure IoT Hub SDK for your Arduino board by running the following command:</span></span>

```bash
gulp install-tools
```

<span data-ttu-id="98ea7-135">視您的網路連線而定，這項工作可能需要很長的時間才會完成。</span><span class="sxs-lookup"><span data-stu-id="98ea7-135">This task might take a long time to complete, depending on your network connection.</span></span>

> [!NOTE]
> <span data-ttu-id="98ea7-136">執行 gulp 工作時，請結束執行 Arduino IDE 執行個體︰`install-tools`、`run`。</span><span class="sxs-lookup"><span data-stu-id="98ea7-136">Please exit the running Arduino IDE instance when running gulp tasks: `install-tools`, `run`.</span></span>

### <a name="deploy-and-run-the-sample-app"></a><span data-ttu-id="98ea7-137">部署和執行範例應用程式</span><span class="sxs-lookup"><span data-stu-id="98ea7-137">Deploy and run the sample app</span></span>
<span data-ttu-id="98ea7-138">執行下列命令，部署和執行範例應用程式：</span><span class="sxs-lookup"><span data-stu-id="98ea7-138">Deploy and run the sample application by running the following command:</span></span>

```bash
gulp run

# You can monitor the serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

### <a name="verify-the-app-works"></a><span data-ttu-id="98ea7-139">確認應用程式可以運作</span><span class="sxs-lookup"><span data-stu-id="98ea7-139">Verify the app works</span></span>
<span data-ttu-id="98ea7-140">如果 LED 沒有閃爍，請參閱[疑難排解指南][troubleshooting-page]，裡面有常見問題的解決方案。</span><span class="sxs-lookup"><span data-stu-id="98ea7-140">If you don’t see the LED blinking, see the [troubleshooting guide][troubleshooting-page] for solutions to common problems.</span></span>

![LED 閃爍][led-blinking]

## <a name="summary"></a><span data-ttu-id="98ea7-142">摘要</span><span class="sxs-lookup"><span data-stu-id="98ea7-142">Summary</span></span>
<span data-ttu-id="98ea7-143">您已安裝必要工具來使用 Arduino 面板，並已在 Arduino 面板上部署範例應用程式來讓 LED 閃爍。</span><span class="sxs-lookup"><span data-stu-id="98ea7-143">You've installed the required tools to work with your Arduino board and deployed a sample application to your Arduino board to blink the LED.</span></span> <span data-ttu-id="98ea7-144">現在，您可以建立、部署和執行另一個範例應用程式，將 Arduino 面板連接至 Azure IoT 中樞來傳送和接收訊息。</span><span class="sxs-lookup"><span data-stu-id="98ea7-144">You can now create, deploy, and run another sample application that connects your Arduino board to Azure IoT Hub to send and receive messages.</span></span>

## <a name="next-steps"></a><span data-ttu-id="98ea7-145">後續步驟</span><span class="sxs-lookup"><span data-stu-id="98ea7-145">Next steps</span></span>
<span data-ttu-id="98ea7-146">[取得 Azure 工具][get-the-azure-tools]</span><span class="sxs-lookup"><span data-stu-id="98ea7-146">[Get the Azure tools][get-the-azure-tools]</span></span>

<!-- Images and links -->

[troubleshooting-page]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[configure-your-device]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-configure-your-device.md
[get-the-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md
[repo-structure]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-blink-arduino-mac.png
[device-discovery]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/device_discovery.png
[config-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-config-mac.png
[led-blinking]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/led_blinking.png
[get-the-azure-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-win32.md