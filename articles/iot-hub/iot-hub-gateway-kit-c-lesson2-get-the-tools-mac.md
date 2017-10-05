---
title: "SensorTag 裝置與 Azure IoT 閘道 - 第 2 課︰取得工具 (macOS) | Microsoft Docs"
description: "在您的 Mac 電腦上安裝工具、建立 IoT 中樞，並在 IoT 中樞登錄您的裝置。"
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
ms.openlocfilehash: 07bc5f2cf6542273c334371b77520c674c5d2f00
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-macos"></a><span data-ttu-id="6c03a-104">取得工具 (MacOS)</span><span class="sxs-lookup"><span data-stu-id="6c03a-104">Get the tools (MacOS)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6c03a-105">Windows 7 或更新版本</span><span class="sxs-lookup"><span data-stu-id="6c03a-105">Windows 7 or later</span></span>](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)
> * [<span data-ttu-id="6c03a-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="6c03a-106">Ubuntu 16.04</span></span>](iot-hub-gateway-kit-c-lesson2-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="6c03a-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="6c03a-107">macOS 10.10</span></span>](iot-hub-gateway-kit-c-lesson2-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="6c03a-108">將執行的作業</span><span class="sxs-lookup"><span data-stu-id="6c03a-108">What you will do</span></span>

- <span data-ttu-id="6c03a-109">安裝 Git、Node.js、Gulp、Python。</span><span class="sxs-lookup"><span data-stu-id="6c03a-109">Install Git, Node.js, Gulp, Python.</span></span>
- <span data-ttu-id="6c03a-110">安裝 Azure 命令列介面 (Azure CLI)。</span><span class="sxs-lookup"><span data-stu-id="6c03a-110">Install the Azure command-line interface (Azure CLI).</span></span> 

<span data-ttu-id="6c03a-111">如果您有任何問題，請在[疑難排解頁面](iot-hub-gateway-kit-c-troubleshooting.md)尋求解決方案。</span><span class="sxs-lookup"><span data-stu-id="6c03a-111">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="6c03a-112">學習目標</span><span class="sxs-lookup"><span data-stu-id="6c03a-112">What you will learn</span></span>

<span data-ttu-id="6c03a-113">在這一課，您將了解：</span><span class="sxs-lookup"><span data-stu-id="6c03a-113">In this lesson, you will learn:</span></span>

- <span data-ttu-id="6c03a-114">如何安裝 [Git](https://git-scm.com/) 和 [Node.js](https://nodejs.org/en/)。</span><span class="sxs-lookup"><span data-stu-id="6c03a-114">How to install [Git](https://git-scm.com/) and [Node.js](https://nodejs.org/en/).</span></span>
  - <span data-ttu-id="6c03a-115">Git 是一個開放原始碼分散式版本控制系統。</span><span class="sxs-lookup"><span data-stu-id="6c03a-115">Git is an open source distributed version control system.</span></span> <span data-ttu-id="6c03a-116">本課程的範例應用程式將會儲存在 Git 上。</span><span class="sxs-lookup"><span data-stu-id="6c03a-116">The sample application for this lesson is stored on Git.</span></span>
  - <span data-ttu-id="6c03a-117">Node.js 是一個具有豐富套件生態系統的 JavaScript 執行階段。</span><span class="sxs-lookup"><span data-stu-id="6c03a-117">Node.js is a JavaScript runtime with a rich package ecosystem.</span></span>
- <span data-ttu-id="6c03a-118">如何使用 [NPM](https://www.npmjs.com/) 安裝 Node.js 開發工具。</span><span class="sxs-lookup"><span data-stu-id="6c03a-118">How to use [NPM](https://www.npmjs.com/) to install Node.js development tools.</span></span>
  - <span data-ttu-id="6c03a-119">Node.js 的版本最低需求為 4.5 LTS。</span><span class="sxs-lookup"><span data-stu-id="6c03a-119">The minimum required version of Node.js is 4.5 LTS.</span></span>
  - <span data-ttu-id="6c03a-120">NPM 是 Node.js 的其中一個套件管理員。</span><span class="sxs-lookup"><span data-stu-id="6c03a-120">NPM is one of the package managers for Node.js.</span></span>
- <span data-ttu-id="6c03a-121">如何安裝 Visual Studio Code。</span><span class="sxs-lookup"><span data-stu-id="6c03a-121">How to install Visual Studio Code.</span></span>
  - <span data-ttu-id="6c03a-122">Visual Studio Code 是一個跨平台、輕量且強大的原始程式碼編輯器，適用於 Windows、Linux 及 macOS。</span><span class="sxs-lookup"><span data-stu-id="6c03a-122">Visual Studio Code is a cross platform, lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="6c03a-123">它對偵錯、內嵌的 Git 控制項、語法反白顯示、智慧型程式碼完成、程式碼片段、程式碼重構也有絕佳的支援。</span><span class="sxs-lookup"><span data-stu-id="6c03a-123">It has great support for debugging, embedded Git control, syntax highlighting, intelligent code completion, snippets, and code refactoring as well.</span></span>
- <span data-ttu-id="6c03a-124">如何安裝 Python。</span><span class="sxs-lookup"><span data-stu-id="6c03a-124">How to install Python.</span></span>
  - <span data-ttu-id="6c03a-125">Python 是普遍使用的高階、一般用途、解譯、動態的程式設計語言。</span><span class="sxs-lookup"><span data-stu-id="6c03a-125">Python is a widely used high-level, general-purpose, interpreted and dynamic programming language.</span></span>
- <span data-ttu-id="6c03a-126">如何安裝 Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="6c03a-126">How to install the Azure CLI.</span></span>
  - <span data-ttu-id="6c03a-127">Azure CLI 提供適用於 Azure 的多平台命令列體驗。</span><span class="sxs-lookup"><span data-stu-id="6c03a-127">The Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="6c03a-128">您可直接從命令列工作以佈建和管理資源。</span><span class="sxs-lookup"><span data-stu-id="6c03a-128">You work directly from a command line to provision and manage resources.</span></span>
- <span data-ttu-id="6c03a-129">如何使用 Azure CLI 建立 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="6c03a-129">How to use the Azure CLI to create an IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="6c03a-130">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="6c03a-130">What you need</span></span>

- <span data-ttu-id="6c03a-131">可下載工具和軟體的網際網路連線。</span><span class="sxs-lookup"><span data-stu-id="6c03a-131">An Internet connection to download the tools and software.</span></span>
- <span data-ttu-id="6c03a-132">執行 OS X Yosemite (10.10) 或更新版本的 Mac 電腦。</span><span class="sxs-lookup"><span data-stu-id="6c03a-132">A Mac computer that’s running OS X Yosemite (10.10) or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="6c03a-133">安裝 Git 和 Node.js</span><span class="sxs-lookup"><span data-stu-id="6c03a-133">Install Git and Node.js</span></span>

<span data-ttu-id="6c03a-134">若要安裝 Git 和 Node.js，請遵循下列步驟，使用 Homebrew 套件管理公用程式︰</span><span class="sxs-lookup"><span data-stu-id="6c03a-134">To install Git and Node.js, use the Homebrew package management utility by following these steps:</span></span>

1. <span data-ttu-id="6c03a-135">[下載](http://brew.sh/)並安裝 Homebrew。</span><span class="sxs-lookup"><span data-stu-id="6c03a-135">[Download](http://brew.sh/) and install Homebrew.</span></span> <span data-ttu-id="6c03a-136">如果您已經安裝 Homebrew，請移至步驟 2。</span><span class="sxs-lookup"><span data-stu-id="6c03a-136">If you’ve already installed Homebrew, go to step 2.</span></span>
   1. <span data-ttu-id="6c03a-137">按 `Cmd + Space` 並輸入 `Terminal` 以開啟終端機。</span><span class="sxs-lookup"><span data-stu-id="6c03a-137">Press `Cmd + Space` and enter `Terminal` to open a terminal.</span></span>
   2. <span data-ttu-id="6c03a-138">執行以下命令：</span><span class="sxs-lookup"><span data-stu-id="6c03a-138">Run the following command:</span></span>

      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```

2. <span data-ttu-id="6c03a-139">執行下列命令安裝 Git 和 Node.js：</span><span class="sxs-lookup"><span data-stu-id="6c03a-139">Install Git and Node.js by running the following command:</span></span>

    ```bash
    brew install node git
    ```

## <a name="install-nodejs-development-tools"></a><span data-ttu-id="6c03a-140">安裝 Node.js 開發工具</span><span class="sxs-lookup"><span data-stu-id="6c03a-140">Install Node.js development tools</span></span>

<span data-ttu-id="6c03a-141">您使用 [gulp.js](http://gulpjs.com/) 來自動化部署和執行指令碼。</span><span class="sxs-lookup"><span data-stu-id="6c03a-141">You use [gulp.js](http://gulpjs.com/) to automate deployment and execution of scripts.</span></span>

<span data-ttu-id="6c03a-142">若要安裝 gulp，在終端機中執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="6c03a-142">To install gulp, run the following command in the terminal:</span></span>

```bash
npm install -g gulp
```

<span data-ttu-id="6c03a-143">如果安裝遇到問題，請參閱[疑難排解指南](iot-hub-gateway-kit-c-troubleshooting.md)，裡面有常見問題的解決辦法。</span><span class="sxs-lookup"><span data-stu-id="6c03a-143">If you experience issues with the installation, see the [troubleshooting guide](iot-hub-gateway-kit-c-troubleshooting.md) for solutions to common problems.</span></span>

> [!Note]
> <span data-ttu-id="6c03a-144">需有節點、NPM、Gulp 才能執行 Node.js 開發的自動化指令碼。</span><span class="sxs-lookup"><span data-stu-id="6c03a-144">Node, NPM and Gulp are required to run automation scripts developed in Node.js.</span></span>

## <a name="install-python"></a><span data-ttu-id="6c03a-145">安裝 Python</span><span class="sxs-lookup"><span data-stu-id="6c03a-145">Install Python</span></span>

<span data-ttu-id="6c03a-146">雖然 Mac OS X 有 Python 2.7，但建議您透過 Homebrew 安裝 Python。</span><span class="sxs-lookup"><span data-stu-id="6c03a-146">Although Mac OS X comes with Python 2.7, we recommend that you install Python through Homebrew.</span></span> <span data-ttu-id="6c03a-147">請參閱[在 Mac OS X 上安裝 Python](http://docs.python-guide.org/en/latest/starting/install/osx/)。</span><span class="sxs-lookup"><span data-stu-id="6c03a-147">See [Installing Python on Mac OS X](http://docs.python-guide.org/en/latest/starting/install/osx/).</span></span>

<span data-ttu-id="6c03a-148">執行下列命令安裝 Python 與 pip：</span><span class="sxs-lookup"><span data-stu-id="6c03a-148">Install Python and pip by running the following command:</span></span>

```bash
brew install python
```

## <a name="install-the-azure-cli"></a><span data-ttu-id="6c03a-149">安裝 Azure CLI</span><span class="sxs-lookup"><span data-stu-id="6c03a-149">Install the Azure CLI</span></span>

<span data-ttu-id="6c03a-150">若要安裝 Azure CLI，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="6c03a-150">To install the Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="6c03a-151">在終端機中執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="6c03a-151">Run the following commands in the terminal:</span></span>
   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
   <span data-ttu-id="6c03a-152">安裝可能需要 5 分鐘。</span><span class="sxs-lookup"><span data-stu-id="6c03a-152">The installation might take 5 minutes.</span></span>

2. <span data-ttu-id="6c03a-153">執行下列命令以驗證安裝：</span><span class="sxs-lookup"><span data-stu-id="6c03a-153">Verify the installation by running the following command:</span></span>
   ```bash
   az iot -h
   ```
   <span data-ttu-id="6c03a-154">如果已成功安裝，您應該會看見下列輸出。</span><span class="sxs-lookup"><span data-stu-id="6c03a-154">You should see the following output if the installation is successful.</span></span>

   ![確認 Azure CLI 安裝](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_osx.png)

## <a name="install-visual-studio-code"></a><span data-ttu-id="6c03a-156">安裝 Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="6c03a-156">Install Visual Studio Code</span></span>

<span data-ttu-id="6c03a-157">您在本教學課程稍後章節會使用 Visual Studio Code 來編輯設定檔。</span><span class="sxs-lookup"><span data-stu-id="6c03a-157">You use Visual Studio Code later in the tutorial to edit configuration files.</span></span>

<span data-ttu-id="6c03a-158">[下載](https://code.visualstudio.com/docs/setup/osx)並安裝 Visual Studio Code。</span><span class="sxs-lookup"><span data-stu-id="6c03a-158">[Download](https://code.visualstudio.com/docs/setup/osx) and install Visual Studio Code.</span></span>

## <a name="summary"></a><span data-ttu-id="6c03a-159">摘要</span><span class="sxs-lookup"><span data-stu-id="6c03a-159">Summary</span></span>

<span data-ttu-id="6c03a-160">您已在 Mac 電腦上安裝所有必要的工具和軟體。</span><span class="sxs-lookup"><span data-stu-id="6c03a-160">You’ve installed all the required tools and software on your Mac computer.</span></span> <span data-ttu-id="6c03a-161">下一步是使用 Azure CLI 建立 IoT 中樞，並且在 IoT 中樞登錄您的裝置。</span><span class="sxs-lookup"><span data-stu-id="6c03a-161">Your next task is to use the Azure CLI to create an IoT hub and register your device in your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6c03a-162">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6c03a-162">Next steps</span></span>
[<span data-ttu-id="6c03a-163">建立 IoT 中樞並登錄裝置</span><span class="sxs-lookup"><span data-stu-id="6c03a-163">Create an IoT hub and register Device</span></span>](iot-hub-gateway-kit-c-lesson2-register-device.md)
