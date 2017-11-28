---
title: "將 Intel Edison (C) 連接到 Azure IoT - 第 1 課：部署應用程式 | Microsoft Docs"
description: "從 GitHub 複製範例 C 應用程式，並執行 gulp 以將此應用程式部署至您的 Intel Edison 面板。 此範例應用程式會讓與面板連接的 LED 每兩秒閃爍一次。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "arduino led 專案, arduino led 閃爍, arduino led 閃爍程式碼, arduino 閃爍程式, arduino 閃爍範例"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: b02dfd3f-28fd-4b52-8775-eb0eaf74d707
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: c45ff5f41bdbc78da8532ffdcaaeec15c695f531
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-deploy-the-blink-application"></a><span data-ttu-id="6e44e-105">建立並部署閃爍應用程式</span><span class="sxs-lookup"><span data-stu-id="6e44e-105">Create and deploy the blink application</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="6e44e-106">將執行的作業</span><span class="sxs-lookup"><span data-stu-id="6e44e-106">What you will do</span></span>
<span data-ttu-id="6e44e-107">從 GitHub 複製範例 C 應用程式，並使用 gulp 工具將範例應用程式部署至您的 Intel Edison。</span><span class="sxs-lookup"><span data-stu-id="6e44e-107">Clone the sample C application from GitHub, and use the gulp tool to deploy the sample application to Intel Edison.</span></span> <span data-ttu-id="6e44e-108">範例應用程式會讓與面板連接的 LED 每兩秒閃爍一次。</span><span class="sxs-lookup"><span data-stu-id="6e44e-108">The sample application blinks the LED connected to the board every two seconds.</span></span> <span data-ttu-id="6e44e-109">如果您有任何問題，請在[疑難排解頁面][troubleshooting]尋求解決方案。</span><span class="sxs-lookup"><span data-stu-id="6e44e-109">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="6e44e-110">學習目標</span><span class="sxs-lookup"><span data-stu-id="6e44e-110">What you will learn</span></span>
* <span data-ttu-id="6e44e-111">如何在 Edison 上部署和執行範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="6e44e-111">How to deploy and run the sample application on Edison.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="6e44e-112">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="6e44e-112">What you need</span></span>
<span data-ttu-id="6e44e-113">您必須已順利完成下列作業︰</span><span class="sxs-lookup"><span data-stu-id="6e44e-113">You must have successfully completed the following operations:</span></span>

* <span data-ttu-id="6e44e-114">[設定裝置][configure-your-device]</span><span class="sxs-lookup"><span data-stu-id="6e44e-114">[Configure your device][configure-your-device]</span></span>
* <span data-ttu-id="6e44e-115">[取得工具][get-the-tools]</span><span class="sxs-lookup"><span data-stu-id="6e44e-115">[Get the tools][get-the-tools]</span></span>

## <a name="open-the-sample-application"></a><span data-ttu-id="6e44e-116">開啟範例應用程式</span><span class="sxs-lookup"><span data-stu-id="6e44e-116">Open the sample application</span></span>
<span data-ttu-id="6e44e-117">若要開啟範例應用程式，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="6e44e-117">To open the sample application, follow these steps:</span></span>

1. <span data-ttu-id="6e44e-118">執行下列命令，從 GitHub 複製範例儲存機制︰</span><span class="sxs-lookup"><span data-stu-id="6e44e-118">Clone the sample repository from GitHub by running the following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-c-edison-getting-started.git
   ```
2. <span data-ttu-id="6e44e-119">執行下列命令來在 Visual Studio Code 中開啟範例應用程式︰</span><span class="sxs-lookup"><span data-stu-id="6e44e-119">Open the sample application in Visual Studio Code by running the following commands:</span></span>

   ```bash
   cd iot-hub-c-edison-getting-started
   cd Lesson1
   code .
   ```

   ![儲存機制結構][repo-structure]

<span data-ttu-id="6e44e-121">`app` 子資料夾中的檔案是包含 LED 控制程式碼的關鍵來源檔案。</span><span class="sxs-lookup"><span data-stu-id="6e44e-121">The file in the `app` subfolder is the key source file that contains the code to control the LED.</span></span>

### <a name="install-application-dependencies"></a><span data-ttu-id="6e44e-122">安裝應用程式相依性</span><span class="sxs-lookup"><span data-stu-id="6e44e-122">Install application dependencies</span></span>
<span data-ttu-id="6e44e-123">執行下列命令，安裝範例應用程式需要的程式庫和其他模組︰</span><span class="sxs-lookup"><span data-stu-id="6e44e-123">Install the libraries and other modules you need for the sample application by running the following command:</span></span>

```bash
npm install
```

## <a name="configure-the-device-connection"></a><span data-ttu-id="6e44e-124">設定裝置連線</span><span class="sxs-lookup"><span data-stu-id="6e44e-124">Configure the device connection</span></span>
<span data-ttu-id="6e44e-125">若要設定裝置連線，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="6e44e-125">To configure the device connection, follow these steps:</span></span>

1. <span data-ttu-id="6e44e-126">執行下列命令來產生裝置組態檔：</span><span class="sxs-lookup"><span data-stu-id="6e44e-126">Generate the device configuration file by running the following command:</span></span>

   ```bash
   gulp init
   ```

   <span data-ttu-id="6e44e-127">組態檔 `config-edison.json` 包含您用來登入 Edison 的使用者認證。</span><span class="sxs-lookup"><span data-stu-id="6e44e-127">The configuration file `config-edison.json` contains the user credentials you use to log in to Edison.</span></span> <span data-ttu-id="6e44e-128">為了避免使用者認證外流，組態檔會產生於電腦主資料夾的 `.iot-hub-getting-started` 子資料夾中。</span><span class="sxs-lookup"><span data-stu-id="6e44e-128">To avoid the leak of user credentials, the configuration file is generated in the subfolder `.iot-hub-getting-started` of the home folder on your computer.</span></span>

2. <span data-ttu-id="6e44e-129">執行下列命令在 Visual Studio Code 中開啟裝置組態檔：</span><span class="sxs-lookup"><span data-stu-id="6e44e-129">Open the device configuration file in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```

3. <span data-ttu-id="6e44e-130">使用您在上一課所記下的 IP 位址和密碼取代預留位置 `[device hostname or IP address]` 和 `[device password]`。</span><span class="sxs-lookup"><span data-stu-id="6e44e-130">Replace the placeholder `[device hostname or IP address]` and `[device password]` with the IP address and password that you marked down in previous lesson.</span></span>

   ![Config.json](media/iot-hub-intel-edison-lessons/lesson1/vscode-config-mac.png)

<span data-ttu-id="6e44e-132">恭喜！</span><span class="sxs-lookup"><span data-stu-id="6e44e-132">Congratulations!</span></span> <span data-ttu-id="6e44e-133">您已成功建立 Edison 的第一個範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="6e44e-133">You've successfully created the first sample application for Edison.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="6e44e-134">部署和執行範例應用程式</span><span class="sxs-lookup"><span data-stu-id="6e44e-134">Deploy and run the sample application</span></span>
### <a name="install-the-azure-iot-hub-sdk-on-edison"></a><span data-ttu-id="6e44e-135">在 Edison 上安裝 Azure IoT 中樞 SDK</span><span class="sxs-lookup"><span data-stu-id="6e44e-135">Install the Azure IoT Hub SDK on Edison</span></span>
<span data-ttu-id="6e44e-136">執行以下命令，在 Edison 上安裝 Azure IoT 中樞 SDK：</span><span class="sxs-lookup"><span data-stu-id="6e44e-136">Install the Azure IoT Hub SDK on Edison by running the following command:</span></span>

```bash
gulp install-tools
```

<span data-ttu-id="6e44e-137">視您的網路連線而定，這項工作可能需要很長的時間才會完成。</span><span class="sxs-lookup"><span data-stu-id="6e44e-137">This task might take a long time to complete, depending on your network connection.</span></span> <span data-ttu-id="6e44e-138">一個 Edison 只需要執行此命令一次。</span><span class="sxs-lookup"><span data-stu-id="6e44e-138">It needs to be run only once for one Edison.</span></span>

### <a name="deploy-and-run-the-sample-app"></a><span data-ttu-id="6e44e-139">部署和執行範例應用程式</span><span class="sxs-lookup"><span data-stu-id="6e44e-139">Deploy and run the sample app</span></span>
<span data-ttu-id="6e44e-140">執行下列命令，部署和執行範例應用程式：</span><span class="sxs-lookup"><span data-stu-id="6e44e-140">Deploy and run the sample application by running the following command:</span></span>

```bash
gulp deploy && gulp run
```

### <a name="verify-the-app-works"></a><span data-ttu-id="6e44e-141">確認應用程式可以運作</span><span class="sxs-lookup"><span data-stu-id="6e44e-141">Verify the app works</span></span>
<span data-ttu-id="6e44e-142">在 LED 閃爍 20 次後，範例應用程式就會自動終止。</span><span class="sxs-lookup"><span data-stu-id="6e44e-142">The sample application terminates automatically after the LED blinks for 20 times.</span></span> <span data-ttu-id="6e44e-143">如果 LED 沒有閃爍，請參閱[疑難排解指南][troubleshooting]，裡面有常見問題的解決方案。</span><span class="sxs-lookup"><span data-stu-id="6e44e-143">If you don’t see the LED blinking, see the [troubleshooting guide][troubleshooting] for solutions to common problems.</span></span>

![LED 閃爍][led-blinking]

## <a name="summary"></a><span data-ttu-id="6e44e-145">摘要</span><span class="sxs-lookup"><span data-stu-id="6e44e-145">Summary</span></span>
<span data-ttu-id="6e44e-146">您已安裝必要工具來使用 Edison，並已在 Edison 上部署範例應用程式來讓 LED 閃爍。</span><span class="sxs-lookup"><span data-stu-id="6e44e-146">You've installed the required tools to work with Edison and deployed a sample application to Edison to blink the LED.</span></span> <span data-ttu-id="6e44e-147">現在，您可以建立、部署和執行另一個範例應用程式，將 Edison 連線至 Azure IoT 中樞來傳送和接收訊息。</span><span class="sxs-lookup"><span data-stu-id="6e44e-147">You can now create, deploy, and run another sample application that connects Edison to Azure IoT Hub to send and receive messages.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6e44e-148">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6e44e-148">Next steps</span></span>
<span data-ttu-id="6e44e-149">[取得 Azure 工具][get-the-azure-tools]</span><span class="sxs-lookup"><span data-stu-id="6e44e-149">[Get the Azure tools][get-the-azure-tools]</span></span>

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[Configure-your-device]: iot-hub-intel-edison-kit-c-lesson1-configure-your-device.md
[get-the-tools]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-win32.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson1/repo_structure_c.png
[led-blinking]: media/iot-hub-intel-edison-lessons/lesson1/led_blinking_c.jpg
[get-the-azure-tools]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-win32.md
