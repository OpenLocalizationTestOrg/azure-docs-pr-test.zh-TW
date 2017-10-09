---
title: "SensorTag 裝置與 Azure IoT 閘道 - 第 2 課︰取得工具 (macOS) | Microsoft Docs"
description: "您的 Mac 電腦上安裝工具、 建立 IoT 中樞和在 hello IoT 中樞註冊您的裝置。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "iot 開發, iot 軟體, iot 雲端服務, 物聯網軟體, azure cli, 安裝 python mac, 在 mac 上安裝 git, gulp 執行, 安裝 node js mac"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 94e538ef-9857-4023-9c3c-e92a0be7c395
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 44bce452690e18e6c803df564fdafcdda7f41c8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-macos"></a><span data-ttu-id="42f59-104">取得 hello 工具 (MacOS)</span><span class="sxs-lookup"><span data-stu-id="42f59-104">Get hello tools (MacOS)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="42f59-105">Windows 7 或更新版本</span><span class="sxs-lookup"><span data-stu-id="42f59-105">Windows 7 or later</span></span>](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)
> * [<span data-ttu-id="42f59-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="42f59-106">Ubuntu 16.04</span></span>](iot-hub-gateway-kit-c-lesson2-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="42f59-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="42f59-107">macOS 10.10</span></span>](iot-hub-gateway-kit-c-lesson2-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="42f59-108">將執行的作業</span><span class="sxs-lookup"><span data-stu-id="42f59-108">What you will do</span></span>

- <span data-ttu-id="42f59-109">安裝 Git、Node.js、Gulp、Python。</span><span class="sxs-lookup"><span data-stu-id="42f59-109">Install Git, Node.js, Gulp, Python.</span></span>
- <span data-ttu-id="42f59-110">安裝 hello Azure 命令列介面 (Azure CLI)。</span><span class="sxs-lookup"><span data-stu-id="42f59-110">Install hello Azure command-line interface (Azure CLI).</span></span> 

<span data-ttu-id="42f59-111">如果您有任何問題，尋找解決方案上 hello[疑難排解頁面](iot-hub-gateway-kit-c-troubleshooting.md)。</span><span class="sxs-lookup"><span data-stu-id="42f59-111">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="42f59-112">學習目標</span><span class="sxs-lookup"><span data-stu-id="42f59-112">What you will learn</span></span>

<span data-ttu-id="42f59-113">在這一課，您將了解：</span><span class="sxs-lookup"><span data-stu-id="42f59-113">In this lesson, you will learn:</span></span>

- <span data-ttu-id="42f59-114">如何 tooinstall [Git](https://git-scm.com/)和[Node.js](https://nodejs.org/en/)。</span><span class="sxs-lookup"><span data-stu-id="42f59-114">How tooinstall [Git](https://git-scm.com/) and [Node.js](https://nodejs.org/en/).</span></span>
  - <span data-ttu-id="42f59-115">Git 是一個開放原始碼分散式版本控制系統。</span><span class="sxs-lookup"><span data-stu-id="42f59-115">Git is an open source distributed version control system.</span></span> <span data-ttu-id="42f59-116">本課程中的 hello 範例應用程式會儲存在 Git。</span><span class="sxs-lookup"><span data-stu-id="42f59-116">hello sample application for this lesson is stored on Git.</span></span>
  - <span data-ttu-id="42f59-117">Node.js 是一個具有豐富套件生態系統的 JavaScript 執行階段。</span><span class="sxs-lookup"><span data-stu-id="42f59-117">Node.js is a JavaScript runtime with a rich package ecosystem.</span></span>
- <span data-ttu-id="42f59-118">如何 toouse [NPM](https://www.npmjs.com/) tooinstall Node.js 開發工具。</span><span class="sxs-lookup"><span data-stu-id="42f59-118">How toouse [NPM](https://www.npmjs.com/) tooinstall Node.js development tools.</span></span>
  - <span data-ttu-id="42f59-119">hello 的最低必要的版本 Node.js 是 4.5 LTS。</span><span class="sxs-lookup"><span data-stu-id="42f59-119">hello minimum required version of Node.js is 4.5 LTS.</span></span>
  - <span data-ttu-id="42f59-120">NPM 是一個 Node.js 的 hello 封裝管理員。</span><span class="sxs-lookup"><span data-stu-id="42f59-120">NPM is one of hello package managers for Node.js.</span></span>
- <span data-ttu-id="42f59-121">如何 tooinstall Visual Studio 程式碼。</span><span class="sxs-lookup"><span data-stu-id="42f59-121">How tooinstall Visual Studio Code.</span></span>
  - <span data-ttu-id="42f59-122">Visual Studio Code 是一個跨平台、輕量且強大的原始程式碼編輯器，適用於 Windows、Linux 及 macOS。</span><span class="sxs-lookup"><span data-stu-id="42f59-122">Visual Studio Code is a cross platform, lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="42f59-123">它對偵錯、內嵌的 Git 控制項、語法反白顯示、智慧型程式碼完成、程式碼片段、程式碼重構也有絕佳的支援。</span><span class="sxs-lookup"><span data-stu-id="42f59-123">It has great support for debugging, embedded Git control, syntax highlighting, intelligent code completion, snippets, and code refactoring as well.</span></span>
- <span data-ttu-id="42f59-124">如何 tooinstall Python。</span><span class="sxs-lookup"><span data-stu-id="42f59-124">How tooinstall Python.</span></span>
  - <span data-ttu-id="42f59-125">Python 是普遍使用的高階、一般用途、解譯、動態的程式設計語言。</span><span class="sxs-lookup"><span data-stu-id="42f59-125">Python is a widely used high-level, general-purpose, interpreted and dynamic programming language.</span></span>
- <span data-ttu-id="42f59-126">如何 tooinstall hello Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="42f59-126">How tooinstall hello Azure CLI.</span></span>
  - <span data-ttu-id="42f59-127">hello Azure CLI 提供 Azure 的多平台命令列體驗。</span><span class="sxs-lookup"><span data-stu-id="42f59-127">hello Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="42f59-128">您可以直接從命令列 tooprovision 工作和管理資源。</span><span class="sxs-lookup"><span data-stu-id="42f59-128">You work directly from a command line tooprovision and manage resources.</span></span>
- <span data-ttu-id="42f59-129">如何 toouse hello Azure CLI toocreate IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="42f59-129">How toouse hello Azure CLI toocreate an IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="42f59-130">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="42f59-130">What you need</span></span>

- <span data-ttu-id="42f59-131">網際網路連線 toodownload hello 工具和軟體。</span><span class="sxs-lookup"><span data-stu-id="42f59-131">An Internet connection toodownload hello tools and software.</span></span>
- <span data-ttu-id="42f59-132">執行 OS X Yosemite (10.10) 或更新版本的 Mac 電腦。</span><span class="sxs-lookup"><span data-stu-id="42f59-132">A Mac computer that’s running OS X Yosemite (10.10) or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="42f59-133">安裝 Git 和 Node.js</span><span class="sxs-lookup"><span data-stu-id="42f59-133">Install Git and Node.js</span></span>

<span data-ttu-id="42f59-134">tooinstall Git 和 Node.js，請依照下列步驟使用 hello Homebrew 套件管理公用程式：</span><span class="sxs-lookup"><span data-stu-id="42f59-134">tooinstall Git and Node.js, use hello Homebrew package management utility by following these steps:</span></span>

1. <span data-ttu-id="42f59-135">[下載](http://brew.sh/)並安裝 Homebrew。</span><span class="sxs-lookup"><span data-stu-id="42f59-135">[Download](http://brew.sh/) and install Homebrew.</span></span> <span data-ttu-id="42f59-136">如果您已經安裝 Homebrew，請移 toostep 2。</span><span class="sxs-lookup"><span data-stu-id="42f59-136">If you’ve already installed Homebrew, go toostep 2.</span></span>
   1. <span data-ttu-id="42f59-137">按`Cmd + Space`輸入`Terminal`tooopen 終端機。</span><span class="sxs-lookup"><span data-stu-id="42f59-137">Press `Cmd + Space` and enter `Terminal` tooopen a terminal.</span></span>
   2. <span data-ttu-id="42f59-138">執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="42f59-138">Run hello following command:</span></span>

      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```

2. <span data-ttu-id="42f59-139">安裝 Git 和 Node.js 藉由執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="42f59-139">Install Git and Node.js by running hello following command:</span></span>

    ```bash
    brew install node git
    ```

## <a name="install-nodejs-development-tools"></a><span data-ttu-id="42f59-140">安裝 Node.js 開發工具</span><span class="sxs-lookup"><span data-stu-id="42f59-140">Install Node.js development tools</span></span>

<span data-ttu-id="42f59-141">您使用[cwd](http://gulpjs.com/) tooautomate 部署和執行指令碼。</span><span class="sxs-lookup"><span data-stu-id="42f59-141">You use [gulp.js](http://gulpjs.com/) tooautomate deployment and execution of scripts.</span></span>

<span data-ttu-id="42f59-142">tooinstall gulp，執行下列命令在 hello 終端機中的 hello:</span><span class="sxs-lookup"><span data-stu-id="42f59-142">tooinstall gulp, run hello following command in hello terminal:</span></span>

```bash
npm install -g gulp
```

<span data-ttu-id="42f59-143">如果您遇到 hello 安裝問題，請參閱 hello[疑難排解指南](iot-hub-gateway-kit-c-troubleshooting.md)解決方案 toocommon 問題。</span><span class="sxs-lookup"><span data-stu-id="42f59-143">If you experience issues with hello installation, see hello [troubleshooting guide](iot-hub-gateway-kit-c-troubleshooting.md) for solutions toocommon problems.</span></span>

> [!Note]
> <span data-ttu-id="42f59-144">節點、 NPM 及 Gulp 是在 Node.js 中開發的必要的 toorun 自動化指令碼。</span><span class="sxs-lookup"><span data-stu-id="42f59-144">Node, NPM and Gulp are required toorun automation scripts developed in Node.js.</span></span>

## <a name="install-python"></a><span data-ttu-id="42f59-145">安裝 Python</span><span class="sxs-lookup"><span data-stu-id="42f59-145">Install Python</span></span>

<span data-ttu-id="42f59-146">雖然 Mac OS X 有 Python 2.7，但建議您透過 Homebrew 安裝 Python。</span><span class="sxs-lookup"><span data-stu-id="42f59-146">Although Mac OS X comes with Python 2.7, we recommend that you install Python through Homebrew.</span></span> <span data-ttu-id="42f59-147">請參閱[在 Mac OS X 上安裝 Python](http://docs.python-guide.org/en/latest/starting/install/osx/)。</span><span class="sxs-lookup"><span data-stu-id="42f59-147">See [Installing Python on Mac OS X](http://docs.python-guide.org/en/latest/starting/install/osx/).</span></span>

<span data-ttu-id="42f59-148">安裝 Python 和 pip 執行 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="42f59-148">Install Python and pip by running hello following command:</span></span>

```bash
brew install python
```

## <a name="install-hello-azure-cli"></a><span data-ttu-id="42f59-149">安裝 hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="42f59-149">Install hello Azure CLI</span></span>

<span data-ttu-id="42f59-150">tooinstall hello Azure CLI，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="42f59-150">tooinstall hello Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="42f59-151">執行下列命令在 hello 終端機的 hello:</span><span class="sxs-lookup"><span data-stu-id="42f59-151">Run hello following commands in hello terminal:</span></span>
   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
   <span data-ttu-id="42f59-152">hello 安裝可能需要 5 分鐘。</span><span class="sxs-lookup"><span data-stu-id="42f59-152">hello installation might take 5 minutes.</span></span>

2. <span data-ttu-id="42f59-153">執行下列命令的 hello 驗證 hello 安裝：</span><span class="sxs-lookup"><span data-stu-id="42f59-153">Verify hello installation by running hello following command:</span></span>
   ```bash
   az iot -h
   ```
   <span data-ttu-id="42f59-154">您應該會看到下列 hello 輸出 hello 安裝是否成功。</span><span class="sxs-lookup"><span data-stu-id="42f59-154">You should see hello following output if hello installation is successful.</span></span>

   ![確認 Azure CLI 安裝](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_osx.png)

## <a name="install-visual-studio-code"></a><span data-ttu-id="42f59-156">安裝 Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="42f59-156">Install Visual Studio Code</span></span>

<span data-ttu-id="42f59-157">您稍後在 hello 教學課程 tooedit 組態檔中使用 Visual Studio 程式碼。</span><span class="sxs-lookup"><span data-stu-id="42f59-157">You use Visual Studio Code later in hello tutorial tooedit configuration files.</span></span>

<span data-ttu-id="42f59-158">[下載](https://code.visualstudio.com/docs/setup/osx)並安裝 Visual Studio Code。</span><span class="sxs-lookup"><span data-stu-id="42f59-158">[Download](https://code.visualstudio.com/docs/setup/osx) and install Visual Studio Code.</span></span>

## <a name="summary"></a><span data-ttu-id="42f59-159">摘要</span><span class="sxs-lookup"><span data-stu-id="42f59-159">Summary</span></span>

<span data-ttu-id="42f59-160">您已在您的 Mac 電腦上安裝所有必要的 hello 工具和軟體。</span><span class="sxs-lookup"><span data-stu-id="42f59-160">You’ve installed all hello required tools and software on your Mac computer.</span></span> <span data-ttu-id="42f59-161">下一個工作是 toouse hello Azure CLI toocreate IoT 中樞，並在您的 IoT 中樞註冊您的裝置。</span><span class="sxs-lookup"><span data-stu-id="42f59-161">Your next task is toouse hello Azure CLI toocreate an IoT hub and register your device in your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="42f59-162">後續步驟</span><span class="sxs-lookup"><span data-stu-id="42f59-162">Next steps</span></span>
[<span data-ttu-id="42f59-163">建立 IoT 中樞並登錄裝置</span><span class="sxs-lookup"><span data-stu-id="42f59-163">Create an IoT hub and register Device</span></span>](iot-hub-gateway-kit-c-lesson2-register-device.md)
