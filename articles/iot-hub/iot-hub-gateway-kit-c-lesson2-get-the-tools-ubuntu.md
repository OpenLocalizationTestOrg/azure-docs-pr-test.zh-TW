---
title: "SensorTag 裝置與 Azure IoT 閘道 - 第 2 課︰取得工具 (Ubuntu) | Microsoft Docs"
description: "執行 Ubuntu 的主機電腦上安裝 hello 工具和 hello 軟體建立 IoT 中心時，在 hello IoT 中樞註冊您的裝置。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "iot 開發, iot 軟體, iot 雲端服務, 物聯網軟體, azure cli, 在 ubuntu 上安裝 git, gulp 執行, 安裝 node js ubuntu"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 0bac1412-385b-4255-a33f-9d44c35feb3e
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: c9edca91e791ef914b1920178b66eadd12ae0281
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-ubuntu-1604"></a><span data-ttu-id="7894e-104">取得 hello 工具 (Ubuntu 16.04)</span><span class="sxs-lookup"><span data-stu-id="7894e-104">Get hello tools (Ubuntu 16.04)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7894e-105">Windows 7 或更新版本</span><span class="sxs-lookup"><span data-stu-id="7894e-105">Windows 7 or later</span></span>](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)
> * [<span data-ttu-id="7894e-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="7894e-106">Ubuntu 16.04</span></span>](iot-hub-gateway-kit-c-lesson2-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="7894e-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="7894e-107">macOS 10.10</span></span>](iot-hub-gateway-kit-c-lesson2-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="7894e-108">將執行的作業</span><span class="sxs-lookup"><span data-stu-id="7894e-108">What you will do</span></span>

- <span data-ttu-id="7894e-109">安裝 Git、Node.js、Gulp、Python。</span><span class="sxs-lookup"><span data-stu-id="7894e-109">Install Git, Node.js, Gulp, Python.</span></span>
- <span data-ttu-id="7894e-110">安裝 hello Azure 命令列介面 (Azure CLI)。</span><span class="sxs-lookup"><span data-stu-id="7894e-110">Install hello Azure command-line interface (Azure CLI).</span></span> 

<span data-ttu-id="7894e-111">如果您有任何問題，尋找解決方案上 hello[疑難排解頁面](iot-hub-gateway-kit-c-troubleshooting.md)。</span><span class="sxs-lookup"><span data-stu-id="7894e-111">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>
## <a name="what-you-will-learn"></a><span data-ttu-id="7894e-112">學習目標</span><span class="sxs-lookup"><span data-stu-id="7894e-112">What you will learn</span></span>

<span data-ttu-id="7894e-113">在這一課，您將了解：</span><span class="sxs-lookup"><span data-stu-id="7894e-113">In this lesson, you will learn:</span></span>

- <span data-ttu-id="7894e-114">如何 tooinstall Git 和 Node.js。</span><span class="sxs-lookup"><span data-stu-id="7894e-114">How tooinstall Git and Node.js.</span></span>
  - <span data-ttu-id="7894e-115">Git 是一個開放原始碼分散式版本控制系統。</span><span class="sxs-lookup"><span data-stu-id="7894e-115">Git is an open source distributed version control system.</span></span> <span data-ttu-id="7894e-116">本課程中的 hello 範例應用程式會儲存在 Git。</span><span class="sxs-lookup"><span data-stu-id="7894e-116">hello sample application for this lesson is stored on Git.</span></span>
  - <span data-ttu-id="7894e-117">Node.js 是一個具有豐富套件生態系統的 JavaScript 執行階段。</span><span class="sxs-lookup"><span data-stu-id="7894e-117">Node.js is a JavaScript runtime with a rich package ecosystem.</span></span>
- <span data-ttu-id="7894e-118">如何 toouse NPM tooinstall Node.js 開發工具。</span><span class="sxs-lookup"><span data-stu-id="7894e-118">How toouse NPM tooinstall Node.js development tools.</span></span>
  - <span data-ttu-id="7894e-119">hello 的最低必要的版本 Node.js 是 4.5 LTS。</span><span class="sxs-lookup"><span data-stu-id="7894e-119">hello minimum required version of Node.js is 4.5 LTS.</span></span>
  - <span data-ttu-id="7894e-120">NPM 是一個 Node.js 的 hello 封裝管理員。</span><span class="sxs-lookup"><span data-stu-id="7894e-120">NPM is one of hello package managers for Node.js.</span></span>
- <span data-ttu-id="7894e-121">如何 tooinstall Visual Studio 程式碼。</span><span class="sxs-lookup"><span data-stu-id="7894e-121">How tooinstall Visual Studio Code.</span></span>
  - <span data-ttu-id="7894e-122">Visual Studio Code 是一個跨平台、輕量且強大的原始程式碼編輯器，適用於 Windows、Linux 及 macOS。</span><span class="sxs-lookup"><span data-stu-id="7894e-122">Visual Studio Code is a cross platform, lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="7894e-123">它對偵錯、內嵌的 Git 控制項、語法反白顯示、智慧型程式碼完成、程式碼片段、程式碼重構也有絕佳的支援。</span><span class="sxs-lookup"><span data-stu-id="7894e-123">It has great support for debugging, embedded Git control, syntax highlighting, intelligent code completion, snippets, and code refactoring as well.</span></span>
- <span data-ttu-id="7894e-124">如何 tooinstall hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="7894e-124">How tooinstall hello Azure CLI</span></span>
  - <span data-ttu-id="7894e-125">hello Azure CLI 提供 Azure 的多平台命令列體驗。</span><span class="sxs-lookup"><span data-stu-id="7894e-125">hello Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="7894e-126">您可以直接從命令列 tooprovision 工作和管理資源。</span><span class="sxs-lookup"><span data-stu-id="7894e-126">You work directly from a command line tooprovision and manage resources.</span></span>
- <span data-ttu-id="7894e-127">如何 toouse hello Azure CLI toocreate IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="7894e-127">How toouse hello Azure CLI toocreate an IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="7894e-128">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="7894e-128">What you need</span></span>

- <span data-ttu-id="7894e-129">網際網路連線 toodownload hello 工具和軟體。</span><span class="sxs-lookup"><span data-stu-id="7894e-129">An Internet connection toodownload hello tools and software.</span></span>
- <span data-ttu-id="7894e-130">一部執行 Ubuntu 16.04 或以上版本的電腦。</span><span class="sxs-lookup"><span data-stu-id="7894e-130">A computer that is running Ubuntu 16.04 or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="7894e-131">安裝 Git 和 Node.js</span><span class="sxs-lookup"><span data-stu-id="7894e-131">Install Git and Node.js</span></span>

<span data-ttu-id="7894e-132">tooinstall Git 和 Node.js，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="7894e-132">tooinstall Git and Node.js, follow these steps:</span></span>

1. <span data-ttu-id="7894e-133">按`Ctrl + Alt + T`tooopen 終端機。</span><span class="sxs-lookup"><span data-stu-id="7894e-133">Press `Ctrl + Alt + T` tooopen a terminal.</span></span>
2. <span data-ttu-id="7894e-134">執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="7894e-134">Run hello following commands:</span></span>

   ```bash
   sudo apt-get update
   curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
   sudo apt-get install -y nodejs
   sudo apt-get install git
   ```

## <a name="install-nodejs-development-tools"></a><span data-ttu-id="7894e-135">安裝 Node.js 開發工具</span><span class="sxs-lookup"><span data-stu-id="7894e-135">Install Node.js development tools</span></span>

<span data-ttu-id="7894e-136">您使用[cwd](http://gulpjs.com/) tooautomate 部署和執行指令碼。</span><span class="sxs-lookup"><span data-stu-id="7894e-136">You use [gulp.js](http://gulpjs.com/) tooautomate deployment and execution of scripts.</span></span>

<span data-ttu-id="7894e-137">tooinstall gulp，執行下列命令在 hello 終端機中的 hello:</span><span class="sxs-lookup"><span data-stu-id="7894e-137">tooinstall gulp, run hello following command in hello terminal:</span></span>

```bash
sudo npm install -g gulp
```

<span data-ttu-id="7894e-138">如果您遇到 hello 安裝問題，請參閱 hello[疑難排解指南](iot-hub-gateway-kit-c-troubleshooting.md)解決方案 toocommon 問題。</span><span class="sxs-lookup"><span data-stu-id="7894e-138">If you experience issues with hello installation, see hello [troubleshooting guide](iot-hub-gateway-kit-c-troubleshooting.md) for solutions toocommon problems.</span></span>

> [!Note]
> <span data-ttu-id="7894e-139">節點、 NPM 及 Gulp 是在 Node.js 中開發的必要的 toorun 自動化指令碼。</span><span class="sxs-lookup"><span data-stu-id="7894e-139">Node, NPM and Gulp are required toorun automation scripts developed in Node.js.</span></span>

## <a name="install-hello-azure-cli"></a><span data-ttu-id="7894e-140">安裝 hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="7894e-140">Install hello Azure CLI</span></span>

<span data-ttu-id="7894e-141">tooinstall hello Azure CLI，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="7894e-141">tooinstall hello Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="7894e-142">執行下列命令在 hello 終端機的 hello:</span><span class="sxs-lookup"><span data-stu-id="7894e-142">Run hello following commands in hello terminal:</span></span>

   ```bash
   sudo apt-get update
   sudo apt-get install -y libssl-dev libffi-dev
   sudo apt-get install -y python-dev
   sudo apt-get install -y build-essential
   sudo apt-get install -y python-pip
   sudo pip install --upgrade azure-cli
   sudo pip install --upgrade azure-cli-iot
   ```

   <span data-ttu-id="7894e-143">hello 安裝可能需要 5 分鐘。</span><span class="sxs-lookup"><span data-stu-id="7894e-143">hello installation might take 5 minutes.</span></span>

2. <span data-ttu-id="7894e-144">執行下列命令的 hello 驗證 hello 安裝：</span><span class="sxs-lookup"><span data-stu-id="7894e-144">Verify hello installation by running hello following command:</span></span>

   ```bash
   az iot -h
   ```
<span data-ttu-id="7894e-145">您應該會看到下列 hello 輸出 hello 安裝是否成功。</span><span class="sxs-lookup"><span data-stu-id="7894e-145">You should see hello following output if hello installation is successful.</span></span>
<span data-ttu-id="7894e-146">![確認 Azure CLI 安裝](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_ubuntu.png)</span><span class="sxs-lookup"><span data-stu-id="7894e-146">![Verify Azure CLI installation](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_ubuntu.png)</span></span>

### <a name="install-visual-studio-code"></a><span data-ttu-id="7894e-147">安裝 Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="7894e-147">Install Visual Studio Code</span></span>

<span data-ttu-id="7894e-148">您稍後在 hello 教學課程 tooedit 組態檔中使用 Visual Studio 程式碼。</span><span class="sxs-lookup"><span data-stu-id="7894e-148">You use Visual Studio Code later in hello tutorial tooedit configuration files.</span></span>

<span data-ttu-id="7894e-149">[下載](https://code.visualstudio.com/docs/setup/linux)並安裝 Visual Studio Code。</span><span class="sxs-lookup"><span data-stu-id="7894e-149">[Download](https://code.visualstudio.com/docs/setup/linux) and install Visual Studio Code.</span></span>

## <a name="summary"></a><span data-ttu-id="7894e-150">摘要</span><span class="sxs-lookup"><span data-stu-id="7894e-150">Summary</span></span>

<span data-ttu-id="7894e-151">您已在主機電腦上安裝所有必要的 hello 工具和軟體。</span><span class="sxs-lookup"><span data-stu-id="7894e-151">You've installed all hello required tools and software on your host computer.</span></span> <span data-ttu-id="7894e-152">下一個工作是 toouse hello Azure CLI toocreate IoT 中樞，並在您的 IoT 中樞註冊您的裝置。</span><span class="sxs-lookup"><span data-stu-id="7894e-152">Your next task is toouse hello Azure CLI toocreate an IoT hub and register your device in your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7894e-153">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7894e-153">Next steps</span></span>
[<span data-ttu-id="7894e-154">建立 IoT 中樞並登錄您的裝置</span><span class="sxs-lookup"><span data-stu-id="7894e-154">Create an IoT hub and register your device</span></span>](iot-hub-gateway-kit-c-lesson2-register-device.md)
