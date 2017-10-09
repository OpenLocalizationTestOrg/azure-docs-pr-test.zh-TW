---
title: "Connect Raspberry Pi (C) tooAzure IoT-第 1 課： 將應用程式部署 |Microsoft 文件"
description: "複製從 GitHub，hello 範例 C 應用程式，此應用程式 tooyour 覆盆子 Pi 3 面板的 gulp toodeploy。 此範例應用程式會閃爍 hello LED 連接 toohello 面板每隔兩秒鐘。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "raspberry pi led 閃爍, raspberry pi 上的閃爍 led"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: f601d1e1-2bc3-4cc5-a6b1-0467e5304dcf
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: e90c3360c4de1873313db19561c781eb21dbf1d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-hello-blink-application"></a><span data-ttu-id="9af25-105">建立及部署 hello 閃爍應用程式</span><span class="sxs-lookup"><span data-stu-id="9af25-105">Create and deploy hello blink application</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="9af25-106">將執行的作業</span><span class="sxs-lookup"><span data-stu-id="9af25-106">What you will do</span></span>
<span data-ttu-id="9af25-107">複製 hello 範例 C 應用程式從 GitHub，並使用 hello gulp 工具 toodeploy hello 範例應用程式 tooRaspberry Pi 3。</span><span class="sxs-lookup"><span data-stu-id="9af25-107">Clone hello sample C application from GitHub, and use hello gulp tool toodeploy hello sample application tooRaspberry Pi 3.</span></span> <span data-ttu-id="9af25-108">hello 範例應用程式會閃爍 hello LED 連接 toohello 面板每隔兩秒鐘。</span><span class="sxs-lookup"><span data-stu-id="9af25-108">hello sample application blinks hello LED connected toohello board every two seconds.</span></span> <span data-ttu-id="9af25-109">如果您有任何問題，尋找解決方案上 hello[疑難排解頁面](iot-hub-raspberry-pi-kit-c-troubleshooting.md)。</span><span class="sxs-lookup"><span data-stu-id="9af25-109">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="9af25-110">學習目標</span><span class="sxs-lookup"><span data-stu-id="9af25-110">What you will learn</span></span>
<span data-ttu-id="9af25-111">在本文中，您將了解：</span><span class="sxs-lookup"><span data-stu-id="9af25-111">In this article, you will learn:</span></span>

* <span data-ttu-id="9af25-112">如何 toouse hello`device-discover-cli`工具 tooretrieve 網路 Pi 的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="9af25-112">How toouse hello `device-discover-cli` tool tooretrieve networking information about Pi.</span></span>
* <span data-ttu-id="9af25-113">如何 toodeploy 和執行的 hello 範例 pi 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="9af25-113">How toodeploy and run hello sample application on Pi.</span></span>
* <span data-ttu-id="9af25-114">如何從遠端執行 pi toodeploy 和偵錯應用程式。</span><span class="sxs-lookup"><span data-stu-id="9af25-114">How toodeploy and debug applications running remotely on Pi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="9af25-115">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="9af25-115">What you need</span></span>
<span data-ttu-id="9af25-116">您必須先成功完成下列作業的 hello:</span><span class="sxs-lookup"><span data-stu-id="9af25-116">You must have successfully completed hello following operations:</span></span>

* [<span data-ttu-id="9af25-117">設定裝置</span><span class="sxs-lookup"><span data-stu-id="9af25-117">Configure your device</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-configure-your-device.md)
* [<span data-ttu-id="9af25-118">取得 hello 工具</span><span class="sxs-lookup"><span data-stu-id="9af25-118">Get hello tools</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)

## <a name="obtain-hello-ip-address-and-host-name-of-pi"></a><span data-ttu-id="9af25-119">取得 hello IP 位址和主機名稱的 Pi</span><span class="sxs-lookup"><span data-stu-id="9af25-119">Obtain hello IP address and host name of Pi</span></span>
<span data-ttu-id="9af25-120">開啟命令提示字元在視窗中或在 macOS 或 Ubuntu，終端機，然後執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="9af25-120">Open a command prompt in Windows or a terminal in macOS or Ubuntu, and then run hello following command:</span></span>

```bash
devdisco list --eth
```

<span data-ttu-id="9af25-121">您應該會看到類似 toohello 下列輸出：</span><span class="sxs-lookup"><span data-stu-id="9af25-121">You should see an output that is similar toohello following:</span></span>

![裝置探索](media/iot-hub-raspberry-pi-lessons/lesson1/device_discovery.png)

<span data-ttu-id="9af25-123">記下 hello`IP address`和`hostname`Pi。</span><span class="sxs-lookup"><span data-stu-id="9af25-123">Take note of hello `IP address` and `hostname` of Pi.</span></span> <span data-ttu-id="9af25-124">本文稍後需要此資訊。</span><span class="sxs-lookup"><span data-stu-id="9af25-124">You need this information later in this article.</span></span>

> [!NOTE]
> <span data-ttu-id="9af25-125">請確定 Pi 為您的電腦相同網路的連線的 toohello。</span><span class="sxs-lookup"><span data-stu-id="9af25-125">Make sure that Pi is connected toohello same network as your computer.</span></span> <span data-ttu-id="9af25-126">例如，如果您的電腦是連線的 tooa 無線網路，Pi 是連接的 tooa 有線網路時，您可能不會看到 hello IP 位址 hello devdisco 輸出中的。</span><span class="sxs-lookup"><span data-stu-id="9af25-126">For example, if your computer is connected tooa wireless network while Pi is connected tooa wired network, you might not see hello IP address in hello devdisco output.</span></span>

## <a name="open-hello-sample-application"></a><span data-ttu-id="9af25-127">開啟 hello 範例應用程式</span><span class="sxs-lookup"><span data-stu-id="9af25-127">Open hello sample application</span></span>
<span data-ttu-id="9af25-128">tooopen hello 範例應用程式，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="9af25-128">tooopen hello sample application, follow these steps:</span></span>

1. <span data-ttu-id="9af25-129">藉由執行下列命令的 hello 複製從 GitHub hello 範例儲存機制：</span><span class="sxs-lookup"><span data-stu-id="9af25-129">Clone hello sample repository from GitHub by running hello following command:</span></span>
   
    ```bash
    git clone https://github.com/Azure-Samples/iot-hub-c-raspberrypi-getting-started.git
    ```
2. <span data-ttu-id="9af25-130">開啟 Visual Studio 程式碼中的 hello 範例應用程式，藉由執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="9af25-130">Open hello sample application in Visual Studio Code by running hello following commands:</span></span>
   
    ```bash
    cd iot-hub-c-raspberrypi-getting-started
    cd Lesson1
    code .
    ```

![儲存機制結構](media/iot-hub-raspberry-pi-lessons/lesson1/vscode-blink-c-mac.png)

<span data-ttu-id="9af25-132">hello`main.c`檔案在 hello`app`子資料夾是包含 hello 程式碼 toocontrol hello LED 的 hello 金鑰來源檔案。</span><span class="sxs-lookup"><span data-stu-id="9af25-132">hello `main.c` file in hello `app` subfolder is hello key source file that contains hello code toocontrol hello LED.</span></span>

### <a name="install-application-dependencies"></a><span data-ttu-id="9af25-133">安裝應用程式相依性</span><span class="sxs-lookup"><span data-stu-id="9af25-133">Install application dependencies</span></span>
<span data-ttu-id="9af25-134">安裝 hello 程式庫和其他您需要執行下列命令的 hello hello 範例應用程式的模組：</span><span class="sxs-lookup"><span data-stu-id="9af25-134">Install hello libraries and other modules you need for hello sample application by running hello following command:</span></span>

```bash
npm install
```

## <a name="configure-hello-device-connection"></a><span data-ttu-id="9af25-135">設定 hello 裝置連線</span><span class="sxs-lookup"><span data-stu-id="9af25-135">Configure hello device connection</span></span>
<span data-ttu-id="9af25-136">tooconfigure hello 裝置連線，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="9af25-136">tooconfigure hello device connection, follow these steps:</span></span>

1. <span data-ttu-id="9af25-137">執行下列命令的 hello 產生 hello 裝置組態檔：</span><span class="sxs-lookup"><span data-stu-id="9af25-137">Generate hello device configuration file by running hello following command:</span></span>
   
   ```bash
   gulp init
   ```
   
   <span data-ttu-id="9af25-138">hello 設定檔`config-raspberrypi.json`包含 toolog 用於 tooPi hello 使用者認證。</span><span class="sxs-lookup"><span data-stu-id="9af25-138">hello configuration file `config-raspberrypi.json` contains hello user credentials you use toolog in tooPi.</span></span> <span data-ttu-id="9af25-139">tooavoid hello 流失 hello 設定檔產生 hello 子資料夾中的使用者認證`.iot-hub-getting-started`hello 您電腦上的主資料夾。</span><span class="sxs-lookup"><span data-stu-id="9af25-139">tooavoid hello leak of user credentials, hello configuration file is generated in hello subfolder `.iot-hub-getting-started` of hello home folder on your computer.</span></span>

2. <span data-ttu-id="9af25-140">開啟 Visual Studio 程式碼中的 hello 裝置組態檔，藉由執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="9af25-140">Open hello device configuration file in Visual Studio Code by running hello following command:</span></span>
   
   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
   
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```

3. <span data-ttu-id="9af25-141">取代 hello 預留位置`[device hostname or IP address]`hello IP 位址或您先前有"取得 hello IP 位址和主機名稱的 Pi。"中的 hello 主機名稱</span><span class="sxs-lookup"><span data-stu-id="9af25-141">Replace hello placeholder `[device hostname or IP address]` with hello IP address or hello host name that you got previously in "Obtain hello IP address and host name of Pi."</span></span>
   
   ![Config.json](media/iot-hub-raspberry-pi-lessons/lesson1/vscode-config-mac.png)

> [!NOTE]
> <span data-ttu-id="9af25-143">連接 tooRaspberry Pi 時，您可以使用 SSH 金鑰而不是使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="9af25-143">You can use SSH key instead of user name and password when connecting tooRaspberry Pi.</span></span> <span data-ttu-id="9af25-144">在順序 toodo 此您將需要 toogenerate hello 索引鍵使用**透過像是**和**@ ssh-複製-識別碼 pi\<裝置位址\>**。</span><span class="sxs-lookup"><span data-stu-id="9af25-144">In order toodo this you will have toogenerate hello key using **ssh-keygen** and **ssh-copy-id pi@\<device address\>**.</span></span>
>
> <span data-ttu-id="9af25-145">在 Windows 上，可在 **Git Bash** 中使用這些命令。</span><span class="sxs-lookup"><span data-stu-id="9af25-145">On Windows these commands are available in **Git Bash**.</span></span>
>
> <span data-ttu-id="9af25-146">您需要 toorun MacOS **brew 安裝 ssh-複製-識別碼**。</span><span class="sxs-lookup"><span data-stu-id="9af25-146">On MacOS you need toorun **brew install ssh-copy-id**.</span></span>
>
> <span data-ttu-id="9af25-147">已成功上傳之後 hello 金鑰 toohello 覆盆子 Pi，取代**device_password**與**device_key_path**屬性**config raspberrypi.json**。</span><span class="sxs-lookup"><span data-stu-id="9af25-147">After successfully uploading hello key toohello Raspberry Pi, replace **device_password** with **device_key_path** property in **config-raspberrypi.json**.</span></span>
>
> <span data-ttu-id="9af25-148">更新的程式碼行應該如下所示︰</span><span class="sxs-lookup"><span data-stu-id="9af25-148">Updated lines should look as below:</span></span>
> ```javascript
> "device_user_name": "pi",
> "device_key_path": "id_rsa",
> ```

<span data-ttu-id="9af25-149">恭喜！</span><span class="sxs-lookup"><span data-stu-id="9af25-149">Congratulations!</span></span> <span data-ttu-id="9af25-150">您已成功建立 hello 第一個範例應用程式 Pi。</span><span class="sxs-lookup"><span data-stu-id="9af25-150">You've successfully created hello first sample application for Pi.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="9af25-151">部署和執行 hello 範例應用程式</span><span class="sxs-lookup"><span data-stu-id="9af25-151">Deploy and run hello sample application</span></span>
### <a name="install-hello-azure-iot-hub-sdk-on-pi"></a><span data-ttu-id="9af25-152">Pi 安裝 hello Azure IoT 中樞 SDK</span><span class="sxs-lookup"><span data-stu-id="9af25-152">Install hello Azure IoT Hub SDK on Pi</span></span>
<span data-ttu-id="9af25-153">執行下列命令的 hello pi 安裝 hello Azure IoT 中樞 SDK:</span><span class="sxs-lookup"><span data-stu-id="9af25-153">Install hello Azure IoT Hub SDK on Pi by running hello following command:</span></span>

```bash
gulp install-tools
```

<span data-ttu-id="9af25-154">這項工作可能需要幾分鐘的時間 toocomplete hello 執行它的第一次。</span><span class="sxs-lookup"><span data-stu-id="9af25-154">This task might take a few minutes toocomplete hello first time you run it.</span></span>

### <a name="deploy-and-run-hello-sample-app"></a><span data-ttu-id="9af25-155">部署和執行 hello 範例應用程式</span><span class="sxs-lookup"><span data-stu-id="9af25-155">Deploy and run hello sample app</span></span>
<span data-ttu-id="9af25-156">部署和執行 hello 範例應用程式藉由執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="9af25-156">Deploy and run hello sample application by running hello following command:</span></span>

```bash
gulp deploy && gulp run
```

### <a name="verify-hello-app-works"></a><span data-ttu-id="9af25-157">確認 hello 應用程式可運作</span><span class="sxs-lookup"><span data-stu-id="9af25-157">Verify hello app works</span></span>
<span data-ttu-id="9af25-158">hello 範例應用程式會自動終止之後 hello LED 閃爍的 20 倍。</span><span class="sxs-lookup"><span data-stu-id="9af25-158">hello sample application terminates automatically after hello LED blinks for 20 times.</span></span> <span data-ttu-id="9af25-159">如果您沒有看到 hello LED 閃爍不停，請參閱 hello[疑難排解指南](iot-hub-raspberry-pi-kit-c-troubleshooting.md)解決方案 toocommon 問題。</span><span class="sxs-lookup"><span data-stu-id="9af25-159">If you don’t see hello LED blinking, see hello [troubleshooting guide](iot-hub-raspberry-pi-kit-c-troubleshooting.md) for solutions toocommon problems.</span></span>
<span data-ttu-id="9af25-160">![LED 閃爍](media/iot-hub-raspberry-pi-lessons/lesson1/led_blinking.jpg)</span><span class="sxs-lookup"><span data-stu-id="9af25-160">![LED blinking](media/iot-hub-raspberry-pi-lessons/lesson1/led_blinking.jpg)</span></span>

## <a name="summary"></a><span data-ttu-id="9af25-161">摘要</span><span class="sxs-lookup"><span data-stu-id="9af25-161">Summary</span></span>
<span data-ttu-id="9af25-162">安裝所需的 hello 工具 toowork 使用 Pi 和部署範例應用程式 tooPi tooblink hello LED。</span><span class="sxs-lookup"><span data-stu-id="9af25-162">You've installed hello required tools toowork with Pi and deployed a sample application tooPi tooblink hello LED.</span></span> <span data-ttu-id="9af25-163">您現在可以建立、 部署和執行另一個連接 Pi tooAzure IoT 中樞 toosend 範例應用程式和接收訊息。</span><span class="sxs-lookup"><span data-stu-id="9af25-163">You can now create, deploy, and run another sample application that connects Pi tooAzure IoT Hub toosend and receive messages.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9af25-164">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9af25-164">Next steps</span></span>
[<span data-ttu-id="9af25-165">取得 Azure 工具</span><span class="sxs-lookup"><span data-stu-id="9af25-165">Get Azure tools</span></span>](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-win32.md)

