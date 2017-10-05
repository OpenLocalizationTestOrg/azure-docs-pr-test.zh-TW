---
featureFlags: usabilla
title: "將 Raspberry Pi (節點) 連接到 Azure IoT - 第 1 課：部署應用程式 | Microsoft Docs"
description: "從 GitHub 複製範例 Node.js 應用程式，並複製 gulp 以將此應用程式部署至您的 Raspberry Pi 3 面板。 此範例應用程式會讓與面板連接的 LED 每兩秒閃爍一次。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "raspberry pi led 閃爍, raspberry pi 上的閃爍 led"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: a5a03a57-fe86-416f-90ff-6eca17775842
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 8b73000c166950172c07b8e188025dc9da5bc011
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-deploy-the-blink-application"></a><span data-ttu-id="b65b5-105">建立並部署閃爍應用程式</span><span class="sxs-lookup"><span data-stu-id="b65b5-105">Create and deploy the blink application</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="b65b5-106">將執行的作業</span><span class="sxs-lookup"><span data-stu-id="b65b5-106">What you will do</span></span>
<span data-ttu-id="b65b5-107">從 GitHub 複製範例 Node.js 應用程式，並使用 gulp 工具將範例應用程式部署至您的 Raspberry Pi 3。</span><span class="sxs-lookup"><span data-stu-id="b65b5-107">Clone the sample Node.js application from GitHub and use the gulp tool to deploy the sample application to your Raspberry Pi 3.</span></span> <span data-ttu-id="b65b5-108">範例應用程式會讓與面板連接的 LED 每兩秒閃爍一次。</span><span class="sxs-lookup"><span data-stu-id="b65b5-108">The sample application blinks the LED connected to the board every two seconds.</span></span> <span data-ttu-id="b65b5-109">如果您有任何問題，請在[疑難排解頁面](iot-hub-raspberry-pi-kit-node-troubleshooting.md)尋求解決方案。</span><span class="sxs-lookup"><span data-stu-id="b65b5-109">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="b65b5-110">學習目標</span><span class="sxs-lookup"><span data-stu-id="b65b5-110">What you will learn</span></span>
<span data-ttu-id="b65b5-111">在本文中，您將了解：</span><span class="sxs-lookup"><span data-stu-id="b65b5-111">In this article, you will learn:</span></span>

* <span data-ttu-id="b65b5-112">如何使用 `device-discover-cli` 工具擷取關於 Pi 的網路資訊。</span><span class="sxs-lookup"><span data-stu-id="b65b5-112">How to use the `device-discover-cli` tool to retrieve networking information about Pi.</span></span>
* <span data-ttu-id="b65b5-113">如何在 Pi 上部署和執行範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="b65b5-113">How to deploy and run the sample application on Pi.</span></span>
* <span data-ttu-id="b65b5-114">如何在 Pi 上部署和偵錯遠端執行的應用程式。</span><span class="sxs-lookup"><span data-stu-id="b65b5-114">How to deploy and debug applications running remotely on Pi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="b65b5-115">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="b65b5-115">What you need</span></span>
<span data-ttu-id="b65b5-116">您必須已順利完成下列作業︰</span><span class="sxs-lookup"><span data-stu-id="b65b5-116">You must have successfully completed the following operations:</span></span>

* [<span data-ttu-id="b65b5-117">設定裝置</span><span class="sxs-lookup"><span data-stu-id="b65b5-117">Configure your device</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-configure-your-device.md)
* [<span data-ttu-id="b65b5-118">取得工具</span><span class="sxs-lookup"><span data-stu-id="b65b5-118">Get the tools</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-win32.md)

## <a name="obtain-the-ip-address-and-host-name-of-pi"></a><span data-ttu-id="b65b5-119">取得 Pi 的 IP 位址和主機名稱</span><span class="sxs-lookup"><span data-stu-id="b65b5-119">Obtain the IP address and host name of Pi</span></span>
<span data-ttu-id="b65b5-120">在 Windows 開啟命令提示字元或在 macOS 或 Ubuntu 開啟終端機，然後執行下列命令︰</span><span class="sxs-lookup"><span data-stu-id="b65b5-120">Open a command prompt in Windows or a terminal in macOS or Ubuntu, and then run the following command:</span></span>

```bash
devdisco list --eth
```

<span data-ttu-id="b65b5-121">您應該會看到如下所示的輸出：</span><span class="sxs-lookup"><span data-stu-id="b65b5-121">You should see an output that is similar to the following:</span></span>

![裝置探索](media/iot-hub-raspberry-pi-lessons/lesson1/device_discovery.png)

<span data-ttu-id="b65b5-123">記下 Pi 的 `IP address` 和 `hostname`。</span><span class="sxs-lookup"><span data-stu-id="b65b5-123">Take note of the `IP address` and `hostname` of Pi.</span></span> <span data-ttu-id="b65b5-124">本文稍後需要此資訊。</span><span class="sxs-lookup"><span data-stu-id="b65b5-124">You need this information later in this article.</span></span>

> [!NOTE]
> <span data-ttu-id="b65b5-125">請確定 Pi 是連接到與您電腦相同的網路。</span><span class="sxs-lookup"><span data-stu-id="b65b5-125">Make sure that Pi is connected to the same network as your computer.</span></span> <span data-ttu-id="b65b5-126">例如，如果您的電腦連線到無線網路，而 Pi 連線到有線網路，您可能不會在 devdisco 輸出中看到 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="b65b5-126">For example, if your computer is connected to a wireless network while Pi is connected to a wired network, you might not see the IP address in the devdisco output.</span></span>

## <a name="clone-the-sample-application"></a><span data-ttu-id="b65b5-127">複製範例應用程式</span><span class="sxs-lookup"><span data-stu-id="b65b5-127">Clone the sample application</span></span>
<span data-ttu-id="b65b5-128">若要開啟範例程式碼，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="b65b5-128">To open the sample code, follow these steps:</span></span>

1. <span data-ttu-id="b65b5-129">執行下列命令，從 GitHub 複製範例儲存機制︰</span><span class="sxs-lookup"><span data-stu-id="b65b5-129">Clone the sample repository from GitHub by running the following command:</span></span>
   
   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-node-raspberrypi-getting-started.git
   ```
2. <span data-ttu-id="b65b5-130">執行下列命令來在 Visual Studio Code 中開啟範例應用程式︰</span><span class="sxs-lookup"><span data-stu-id="b65b5-130">Open the sample application in Visual Studio Code by running the following commands:</span></span>
   
   ```bash
   cd iot-hub-node-raspberrypi-getting-started
   cd Lesson1
   code .
   ```

![儲存機制結構](media/iot-hub-raspberry-pi-lessons/lesson1/vscode-blink-mac.png)

<span data-ttu-id="b65b5-132">`app` 子資料夾中的 `app.js` 檔案是包含 LED 控制程式碼的關鍵來源檔案。</span><span class="sxs-lookup"><span data-stu-id="b65b5-132">The `app.js` file in the `app` subfolder is the key source file that contains the code to control the LED.</span></span>

### <a name="install-application-dependencies"></a><span data-ttu-id="b65b5-133">安裝應用程式相依性</span><span class="sxs-lookup"><span data-stu-id="b65b5-133">Install application dependencies</span></span>
<span data-ttu-id="b65b5-134">執行下列命令，安裝範例應用程式需要的程式庫和其他模組︰</span><span class="sxs-lookup"><span data-stu-id="b65b5-134">Install the libraries and other modules you need for the sample application by running the following command:</span></span>

```bash
npm install
```

## <a name="configure-the-device-connection"></a><span data-ttu-id="b65b5-135">設定裝置連線</span><span class="sxs-lookup"><span data-stu-id="b65b5-135">Configure the device connection</span></span>
<span data-ttu-id="b65b5-136">若要設定裝置連線，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="b65b5-136">To configure the device connection, follow these steps:</span></span>

1. <span data-ttu-id="b65b5-137">執行下列命令來產生裝置組態檔：</span><span class="sxs-lookup"><span data-stu-id="b65b5-137">Generate the device configuration file by running the following command:</span></span>
   
   ```bash
   gulp init
   ```
   
   <span data-ttu-id="b65b5-138">組態檔 `config-raspberrypi.json` 包含您用來登入 Pi 的使用者認證。</span><span class="sxs-lookup"><span data-stu-id="b65b5-138">The configuration file `config-raspberrypi.json` contains the user credentials you use to log in to Pi.</span></span> <span data-ttu-id="b65b5-139">為了避免使用者認證外流，組態檔會產生於電腦主資料夾的 `.iot-hub-getting-started` 子資料夾中。</span><span class="sxs-lookup"><span data-stu-id="b65b5-139">To avoid the leak of user credentials, the configuration file is generated in the subfolder `.iot-hub-getting-started` of the home folder on your computer.</span></span>

2. <span data-ttu-id="b65b5-140">執行下列命令在 Visual Studio Code 中開啟裝置組態檔：</span><span class="sxs-lookup"><span data-stu-id="b65b5-140">Open the device configuration file in Visual Studio Code by running the following command:</span></span>
   
   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
   
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```
   
3. <span data-ttu-id="b65b5-141">使用先前在＜取得 Pi 的 IP 位址和主機名稱＞中取得的 IP 位址和主機名稱取代預留位置 `[device hostname or IP address]`。</span><span class="sxs-lookup"><span data-stu-id="b65b5-141">Replace the placeholder `[device hostname or IP address]` with the IP address or the host name that you got previously in "Obtain the IP address and host name of Pi."</span></span>
   
   ![Config.json](media/iot-hub-raspberry-pi-lessons/lesson1/vscode-config-mac.png)

> [!NOTE]
> <span data-ttu-id="b65b5-143">在連接到 Raspberry Pi 時，您可以使用 SSH 金鑰而非使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="b65b5-143">You can use SSH key instead of user name and password when connecting to Raspberry Pi.</span></span> <span data-ttu-id="b65b5-144">若要這樣做您必須產生索引鍵使用**透過像是**和**@ ssh-複製-識別碼 pi\<裝置位址\>**。</span><span class="sxs-lookup"><span data-stu-id="b65b5-144">In order to do this you will have to generate the key using **ssh-keygen** and **ssh-copy-id pi@\<device address\>**.</span></span>
>
> <span data-ttu-id="b65b5-145">在 Windows 上，可在 **Git Bash** 中使用這些命令。</span><span class="sxs-lookup"><span data-stu-id="b65b5-145">On Windows these commands are available in **Git Bash**.</span></span>
>
> <span data-ttu-id="b65b5-146">在 MacOS 上，則必須執行 **brew install ssh-copy-id**。</span><span class="sxs-lookup"><span data-stu-id="b65b5-146">On MacOS you need to run **brew install ssh-copy-id**.</span></span>
>
> <span data-ttu-id="b65b5-147">成功將金鑰上傳至 Raspberry Pi 後，請將 **device_password** 替換為 **config-raspberrypi.json** 中的 **device_key_path** 屬性。</span><span class="sxs-lookup"><span data-stu-id="b65b5-147">After successfully uploading the key to the Raspberry Pi, replace **device_password** with **device_key_path** property in **config-raspberrypi.json**.</span></span>
>
> <span data-ttu-id="b65b5-148">更新的程式碼行應該如下所示︰</span><span class="sxs-lookup"><span data-stu-id="b65b5-148">Updated lines should look as below:</span></span>
> ```javascript
> "device_user_name": "pi",
> "device_key_path": "id_rsa",
> ```

<span data-ttu-id="b65b5-149">恭喜！</span><span class="sxs-lookup"><span data-stu-id="b65b5-149">Congratulations!</span></span> <span data-ttu-id="b65b5-150">您已成功建立 Pi 的第一個範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="b65b5-150">You've successfully created the first sample application for Pi.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="b65b5-151">部署和執行範例應用程式</span><span class="sxs-lookup"><span data-stu-id="b65b5-151">Deploy and run the sample application</span></span>
### <a name="install-nodejs-and-npm-on-pi"></a><span data-ttu-id="b65b5-152">在 Pi 上安裝 Node.js 和 NPM</span><span class="sxs-lookup"><span data-stu-id="b65b5-152">Install Node.js and NPM on Pi</span></span>
<span data-ttu-id="b65b5-153">執行下列命令，在 Pi 上安裝 Node.js 和 NPM︰</span><span class="sxs-lookup"><span data-stu-id="b65b5-153">Install Node.js and NPM on Pi by running the following command:</span></span>

```bash
gulp install-tools
```

<span data-ttu-id="b65b5-154">第一次執行此工作時，可能需要 10 分鐘才會完成。</span><span class="sxs-lookup"><span data-stu-id="b65b5-154">This task might take 10 minutes to complete the first time you run it.</span></span>

### <a name="deploy-and-run-the-sample-app"></a><span data-ttu-id="b65b5-155">部署和執行範例應用程式</span><span class="sxs-lookup"><span data-stu-id="b65b5-155">Deploy and run the sample app</span></span>
<span data-ttu-id="b65b5-156">執行下列命令，部署和執行範例應用程式：</span><span class="sxs-lookup"><span data-stu-id="b65b5-156">Deploy and run the sample application by running the following command:</span></span>

```bash
gulp deploy && gulp run
```

### <a name="verify-the-app-works"></a><span data-ttu-id="b65b5-157">確認應用程式可以運作</span><span class="sxs-lookup"><span data-stu-id="b65b5-157">Verify the app works</span></span>
<span data-ttu-id="b65b5-158">您現在應該會看到 Pi 上的 LED 每兩秒閃爍一次。</span><span class="sxs-lookup"><span data-stu-id="b65b5-158">You should now see the LED on Pi blinking every two seconds.</span></span>  <span data-ttu-id="b65b5-159">如果 LED 沒有閃爍，請參閱[疑難排解指南](iot-hub-raspberry-pi-kit-node-troubleshooting.md)，裡面有常見問題的解決方案。</span><span class="sxs-lookup"><span data-stu-id="b65b5-159">If you don’t see the LED blinking, see the [troubleshooting guide](iot-hub-raspberry-pi-kit-node-troubleshooting.md) for solutions to common problems.</span></span>
<span data-ttu-id="b65b5-160">![LED 閃爍](media/iot-hub-raspberry-pi-lessons/lesson1/led_blinking.jpg)</span><span class="sxs-lookup"><span data-stu-id="b65b5-160">![LED blinking](media/iot-hub-raspberry-pi-lessons/lesson1/led_blinking.jpg)</span></span>

## <a name="summary"></a><span data-ttu-id="b65b5-161">摘要</span><span class="sxs-lookup"><span data-stu-id="b65b5-161">Summary</span></span>
<span data-ttu-id="b65b5-162">您已安裝必要工具來使用 Pi，並已在 Pi 上部署範例應用程式來讓 LED 閃爍。</span><span class="sxs-lookup"><span data-stu-id="b65b5-162">You've installed the required tools to work with Pi and deployed a sample application to Pi to blink the LED.</span></span> <span data-ttu-id="b65b5-163">現在，您可以建立、部署和執行另一個範例應用程式，將 Pi 連線至 Azure IoT 中樞來傳送和接收訊息。</span><span class="sxs-lookup"><span data-stu-id="b65b5-163">You can now create, deploy, and run another sample application that connects Pi to Azure IoT Hub to send and receive messages.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b65b5-164">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b65b5-164">Next steps</span></span>
[<span data-ttu-id="b65b5-165">取得 Azure 工具</span><span class="sxs-lookup"><span data-stu-id="b65b5-165">Get the Azure tools</span></span>](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-win32.md)

