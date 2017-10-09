---
title: "Connect Intel Edison (C) tooAzure IoT-第 1 課： 將應用程式部署 |Microsoft 文件"
description: "複製 hello 範例 C 應用程式從 GitHub，並執行 gulp toodeploy 此應用程式 tooyour Intel Edison 面板。 此範例應用程式會閃爍 hello LED 連接 toohello 面板每隔兩秒鐘。"
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
ms.openlocfilehash: fa84fae812dd742a2ad4997a5e213c8e40e6fcf9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-hello-blink-application"></a><span data-ttu-id="96818-105">建立及部署 hello 閃爍應用程式</span><span class="sxs-lookup"><span data-stu-id="96818-105">Create and deploy hello blink application</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="96818-106">將執行的作業</span><span class="sxs-lookup"><span data-stu-id="96818-106">What you will do</span></span>
<span data-ttu-id="96818-107">複製 hello 範例 C 應用程式從 GitHub，並使用 hello gulp 工具 toodeploy hello 範例應用程式 tooIntel Edison。</span><span class="sxs-lookup"><span data-stu-id="96818-107">Clone hello sample C application from GitHub, and use hello gulp tool toodeploy hello sample application tooIntel Edison.</span></span> <span data-ttu-id="96818-108">hello 範例應用程式會閃爍 hello LED 連接 toohello 面板每隔兩秒鐘。</span><span class="sxs-lookup"><span data-stu-id="96818-108">hello sample application blinks hello LED connected toohello board every two seconds.</span></span> <span data-ttu-id="96818-109">如果您有任何問題，尋找解決方案上 hello[疑難排解頁面][troubleshooting]。</span><span class="sxs-lookup"><span data-stu-id="96818-109">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="96818-110">學習目標</span><span class="sxs-lookup"><span data-stu-id="96818-110">What you will learn</span></span>
* <span data-ttu-id="96818-111">如何 toodeploy 和執行的 hello 範例 Edison 上的應用程式。</span><span class="sxs-lookup"><span data-stu-id="96818-111">How toodeploy and run hello sample application on Edison.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="96818-112">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="96818-112">What you need</span></span>
<span data-ttu-id="96818-113">您必須先成功完成下列作業的 hello:</span><span class="sxs-lookup"><span data-stu-id="96818-113">You must have successfully completed hello following operations:</span></span>

* <span data-ttu-id="96818-114">[設定裝置][configure-your-device]</span><span class="sxs-lookup"><span data-stu-id="96818-114">[Configure your device][configure-your-device]</span></span>
* <span data-ttu-id="96818-115">[取得 hello 工具][get-the-tools]</span><span class="sxs-lookup"><span data-stu-id="96818-115">[Get hello tools][get-the-tools]</span></span>

## <a name="open-hello-sample-application"></a><span data-ttu-id="96818-116">開啟 hello 範例應用程式</span><span class="sxs-lookup"><span data-stu-id="96818-116">Open hello sample application</span></span>
<span data-ttu-id="96818-117">tooopen hello 範例應用程式，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="96818-117">tooopen hello sample application, follow these steps:</span></span>

1. <span data-ttu-id="96818-118">藉由執行下列命令的 hello 複製從 GitHub hello 範例儲存機制：</span><span class="sxs-lookup"><span data-stu-id="96818-118">Clone hello sample repository from GitHub by running hello following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-c-edison-getting-started.git
   ```
2. <span data-ttu-id="96818-119">開啟 Visual Studio 程式碼中的 hello 範例應用程式，藉由執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="96818-119">Open hello sample application in Visual Studio Code by running hello following commands:</span></span>

   ```bash
   cd iot-hub-c-edison-getting-started
   cd Lesson1
   code .
   ```

   ![儲存機制結構][repo-structure]

<span data-ttu-id="96818-121">hello 檔案在 hello`app`子資料夾是包含 hello 程式碼 toocontrol hello LED 的 hello 金鑰來源檔案。</span><span class="sxs-lookup"><span data-stu-id="96818-121">hello file in hello `app` subfolder is hello key source file that contains hello code toocontrol hello LED.</span></span>

### <a name="install-application-dependencies"></a><span data-ttu-id="96818-122">安裝應用程式相依性</span><span class="sxs-lookup"><span data-stu-id="96818-122">Install application dependencies</span></span>
<span data-ttu-id="96818-123">安裝 hello 程式庫和其他您需要執行下列命令的 hello hello 範例應用程式的模組：</span><span class="sxs-lookup"><span data-stu-id="96818-123">Install hello libraries and other modules you need for hello sample application by running hello following command:</span></span>

```bash
npm install
```

## <a name="configure-hello-device-connection"></a><span data-ttu-id="96818-124">設定 hello 裝置連線</span><span class="sxs-lookup"><span data-stu-id="96818-124">Configure hello device connection</span></span>
<span data-ttu-id="96818-125">tooconfigure hello 裝置連線，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="96818-125">tooconfigure hello device connection, follow these steps:</span></span>

1. <span data-ttu-id="96818-126">執行下列命令的 hello 產生 hello 裝置組態檔：</span><span class="sxs-lookup"><span data-stu-id="96818-126">Generate hello device configuration file by running hello following command:</span></span>

   ```bash
   gulp init
   ```

   <span data-ttu-id="96818-127">hello 設定檔`config-edison.json`包含 toolog 用於 tooEdison hello 使用者認證。</span><span class="sxs-lookup"><span data-stu-id="96818-127">hello configuration file `config-edison.json` contains hello user credentials you use toolog in tooEdison.</span></span> <span data-ttu-id="96818-128">tooavoid hello 流失 hello 設定檔產生 hello 子資料夾中的使用者認證`.iot-hub-getting-started`hello 您電腦上的主資料夾。</span><span class="sxs-lookup"><span data-stu-id="96818-128">tooavoid hello leak of user credentials, hello configuration file is generated in hello subfolder `.iot-hub-getting-started` of hello home folder on your computer.</span></span>

2. <span data-ttu-id="96818-129">開啟 Visual Studio 程式碼中的 hello 裝置組態檔，藉由執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="96818-129">Open hello device configuration file in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```

3. <span data-ttu-id="96818-130">取代 hello 預留位置`[device hostname or IP address]`和`[device password]`hello IP 位址與密碼在上一課中標記為。</span><span class="sxs-lookup"><span data-stu-id="96818-130">Replace hello placeholder `[device hostname or IP address]` and `[device password]` with hello IP address and password that you marked down in previous lesson.</span></span>

   ![Config.json](media/iot-hub-intel-edison-lessons/lesson1/vscode-config-mac.png)

<span data-ttu-id="96818-132">恭喜！</span><span class="sxs-lookup"><span data-stu-id="96818-132">Congratulations!</span></span> <span data-ttu-id="96818-133">您已成功建立 hello 第一個範例應用程式 Edison。</span><span class="sxs-lookup"><span data-stu-id="96818-133">You've successfully created hello first sample application for Edison.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="96818-134">部署和執行 hello 範例應用程式</span><span class="sxs-lookup"><span data-stu-id="96818-134">Deploy and run hello sample application</span></span>
### <a name="install-hello-azure-iot-hub-sdk-on-edison"></a><span data-ttu-id="96818-135">Edison 上安裝 hello Azure IoT 中樞 SDK</span><span class="sxs-lookup"><span data-stu-id="96818-135">Install hello Azure IoT Hub SDK on Edison</span></span>
<span data-ttu-id="96818-136">執行下列命令的 hello Edison 上安裝 hello Azure IoT 中樞 SDK:</span><span class="sxs-lookup"><span data-stu-id="96818-136">Install hello Azure IoT Hub SDK on Edison by running hello following command:</span></span>

```bash
gulp install-tools
```

<span data-ttu-id="96818-137">這項工作可能需要很長的時間 toocomplete，取決於您的網路連線。</span><span class="sxs-lookup"><span data-stu-id="96818-137">This task might take a long time toocomplete, depending on your network connection.</span></span> <span data-ttu-id="96818-138">它需要 toobe 只執行一次針對一個 Edison。</span><span class="sxs-lookup"><span data-stu-id="96818-138">It needs toobe run only once for one Edison.</span></span>

### <a name="deploy-and-run-hello-sample-app"></a><span data-ttu-id="96818-139">部署和執行 hello 範例應用程式</span><span class="sxs-lookup"><span data-stu-id="96818-139">Deploy and run hello sample app</span></span>
<span data-ttu-id="96818-140">部署和執行 hello 範例應用程式藉由執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="96818-140">Deploy and run hello sample application by running hello following command:</span></span>

```bash
gulp deploy && gulp run
```

### <a name="verify-hello-app-works"></a><span data-ttu-id="96818-141">確認 hello 應用程式可運作</span><span class="sxs-lookup"><span data-stu-id="96818-141">Verify hello app works</span></span>
<span data-ttu-id="96818-142">hello 範例應用程式會自動終止之後 hello LED 閃爍的 20 倍。</span><span class="sxs-lookup"><span data-stu-id="96818-142">hello sample application terminates automatically after hello LED blinks for 20 times.</span></span> <span data-ttu-id="96818-143">如果您沒有看到 hello LED 閃爍不停，請參閱 hello[疑難排解指南][ troubleshooting]解決方案 toocommon 問題。</span><span class="sxs-lookup"><span data-stu-id="96818-143">If you don’t see hello LED blinking, see hello [troubleshooting guide][troubleshooting] for solutions toocommon problems.</span></span>

![LED 閃爍][led-blinking]

## <a name="summary"></a><span data-ttu-id="96818-145">摘要</span><span class="sxs-lookup"><span data-stu-id="96818-145">Summary</span></span>
<span data-ttu-id="96818-146">您所需的 hello 工具 toowork 隨 Edison 並部署範例應用程式 tooEdison tooblink hello LED。</span><span class="sxs-lookup"><span data-stu-id="96818-146">You've installed hello required tools toowork with Edison and deployed a sample application tooEdison tooblink hello LED.</span></span> <span data-ttu-id="96818-147">您現在可以建立、 部署和執行另一個連接 Edison tooAzure IoT 中樞 toosend 範例應用程式和接收訊息。</span><span class="sxs-lookup"><span data-stu-id="96818-147">You can now create, deploy, and run another sample application that connects Edison tooAzure IoT Hub toosend and receive messages.</span></span>

## <a name="next-steps"></a><span data-ttu-id="96818-148">後續步驟</span><span class="sxs-lookup"><span data-stu-id="96818-148">Next steps</span></span>
<span data-ttu-id="96818-149">[取得 hello Azure tools][get-the-azure-tools]</span><span class="sxs-lookup"><span data-stu-id="96818-149">[Get hello Azure tools][get-the-azure-tools]</span></span>

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[Configure-your-device]: iot-hub-intel-edison-kit-c-lesson1-configure-your-device.md
[get-the-tools]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-win32.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson1/repo_structure_c.png
[led-blinking]: media/iot-hub-intel-edison-lessons/lesson1/led_blinking_c.jpg
[get-the-azure-tools]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-win32.md
