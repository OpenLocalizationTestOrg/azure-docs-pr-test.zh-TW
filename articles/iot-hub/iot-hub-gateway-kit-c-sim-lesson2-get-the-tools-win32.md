---
title: "模擬裝置與 Azure IoT 閘道 - 第 2 課︰取得工具 (Windows) | Microsoft Docs"
description: "在執行 Windows 的主機電腦上安裝工具和軟體，建立 IoT 中樞，在 IoT 中樞登錄您的裝置。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "iot 開發, iot 軟體, iot 雲端服務, 物聯網軟體, azure cli, 在 windows 上安裝 git, gulp 執行, 安裝 node js windows, 在 windows 上安裝 npm, 在 windows 上安裝 python"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: c16eee4c-8756-454b-82bf-3eb0dd51aa5f
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: ecedf5ef89677c73c5d9a3e5250eb9f45f6bad32
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-windows-7-and-later"></a><span data-ttu-id="f6169-104">取得工具 (Windows 7 和更新版本)</span><span class="sxs-lookup"><span data-stu-id="f6169-104">Get the tools (Windows 7 and later)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f6169-105">Windows 7 或更新版本</span><span class="sxs-lookup"><span data-stu-id="f6169-105">Windows 7 or later</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)
> * [<span data-ttu-id="f6169-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="f6169-106">Ubuntu 16.04</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="f6169-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="f6169-107">macOS 10.10</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="f6169-108">將執行的作業</span><span class="sxs-lookup"><span data-stu-id="f6169-108">What you will do</span></span>

- <span data-ttu-id="f6169-109">安裝 Git、Node.js、Gulp、Python。</span><span class="sxs-lookup"><span data-stu-id="f6169-109">Install Git, Node.js, Gulp, Python.</span></span>
- <span data-ttu-id="f6169-110">安裝 Azure 命令列介面 (Azure CLI)。</span><span class="sxs-lookup"><span data-stu-id="f6169-110">Install the Azure command-line interface (Azure CLI).</span></span> 

<span data-ttu-id="f6169-111">如果您有任何問題，請在[疑難排解頁面](iot-hub-gateway-kit-c-sim-troubleshooting.md)尋求解決方案。</span><span class="sxs-lookup"><span data-stu-id="f6169-111">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="f6169-112">學習目標</span><span class="sxs-lookup"><span data-stu-id="f6169-112">What you will learn</span></span>

<span data-ttu-id="f6169-113">在這一課，您將了解：</span><span class="sxs-lookup"><span data-stu-id="f6169-113">In this lesson, you will learn:</span></span>

- <span data-ttu-id="f6169-114">如何安裝 [Git](https://git-scm.com/) 和 [Node.js](https://nodejs.org/en/)。</span><span class="sxs-lookup"><span data-stu-id="f6169-114">How to install [Git](https://git-scm.com/) and [Node.js](https://nodejs.org/en/).</span></span>
  - <span data-ttu-id="f6169-115">Git 是一個開放原始碼分散式版本控制系統。</span><span class="sxs-lookup"><span data-stu-id="f6169-115">Git is an open source distributed version control system.</span></span> <span data-ttu-id="f6169-116">本課程的範例應用程式將會儲存在 Git 上。</span><span class="sxs-lookup"><span data-stu-id="f6169-116">The sample application for this lesson is stored on Git.</span></span>
  - <span data-ttu-id="f6169-117">Node.js 是一個具有豐富套件生態系統的 JavaScript 執行階段。</span><span class="sxs-lookup"><span data-stu-id="f6169-117">Node.js is a JavaScript runtime with a rich package ecosystem.</span></span>
- <span data-ttu-id="f6169-118">如何使用 [NPM](https://www.npmjs.com/) 安裝 Node.js 開發工具。</span><span class="sxs-lookup"><span data-stu-id="f6169-118">How to use [NPM](https://www.npmjs.com/) to install Node.js development tools.</span></span>
  - <span data-ttu-id="f6169-119">Node.js 的版本最低需求為 4.5 LTS。</span><span class="sxs-lookup"><span data-stu-id="f6169-119">The minimum required version of Node.js is 4.5 LTS.</span></span>
  - <span data-ttu-id="f6169-120">NPM 是 Node.js 的其中一個套件管理員。</span><span class="sxs-lookup"><span data-stu-id="f6169-120">NPM is one of the package managers for Node.js.</span></span>
- <span data-ttu-id="f6169-121">如何安裝 Visual Studio Code。</span><span class="sxs-lookup"><span data-stu-id="f6169-121">How to install Visual Studio Code.</span></span>
  - <span data-ttu-id="f6169-122">Visual Studio Code 是一個跨平台、輕量且強大的原始程式碼編輯器，適用於 Windows、Linux 及 macOS。</span><span class="sxs-lookup"><span data-stu-id="f6169-122">Visual Studio Code is a cross platform, lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="f6169-123">它對偵錯、內嵌的 Git 控制項、語法反白顯示、智慧型程式碼完成、程式碼片段、程式碼重構也有絕佳的支援。</span><span class="sxs-lookup"><span data-stu-id="f6169-123">It has great support for debugging, embedded Git control, syntax highlighting, intelligent code completion, snippets, and code refactoring as well.</span></span>
- <span data-ttu-id="f6169-124">如何安裝 Python。</span><span class="sxs-lookup"><span data-stu-id="f6169-124">How to install Python.</span></span>
  - <span data-ttu-id="f6169-125">Python 是普遍使用的高階、一般用途、解譯、動態的程式設計語言。</span><span class="sxs-lookup"><span data-stu-id="f6169-125">Python is a widely used high-level, general-purpose, interpreted and dynamic programming language.</span></span>
- <span data-ttu-id="f6169-126">如何安裝 Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="f6169-126">How to install the Azure CLI.</span></span>
  - <span data-ttu-id="f6169-127">Azure CLI 提供適用於 Azure 的多平台命令列體驗。</span><span class="sxs-lookup"><span data-stu-id="f6169-127">The Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="f6169-128">您可直接從命令列工作以佈建和管理資源。</span><span class="sxs-lookup"><span data-stu-id="f6169-128">You work directly from a command line to provision and manage resources.</span></span>
- <span data-ttu-id="f6169-129">如何使用 Azure CLI 建立 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="f6169-129">How to use the Azure CLI to create an IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="f6169-130">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="f6169-130">What you need</span></span>

- <span data-ttu-id="f6169-131">可下載工具和軟體的網際網路連線。</span><span class="sxs-lookup"><span data-stu-id="f6169-131">An Internet connection to download the tools and software.</span></span>
- <span data-ttu-id="f6169-132">Windows 電腦。</span><span class="sxs-lookup"><span data-stu-id="f6169-132">A Windows computer.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="f6169-133">安裝 Git 和 Node.js</span><span class="sxs-lookup"><span data-stu-id="f6169-133">Install Git and Node.js</span></span>

<span data-ttu-id="f6169-134">按一下下列連結以下載並安裝 Git for Windows 和適用於 Windows 的 Node.js LTS。</span><span class="sxs-lookup"><span data-stu-id="f6169-134">Click the following links to download and install Git and Node.js LTS for Windows.</span></span>

- [<span data-ttu-id="f6169-135">取得 Git for Windows</span><span class="sxs-lookup"><span data-stu-id="f6169-135">Get Git for Windows</span></span>](https://git-scm.com/download/win/)
- [<span data-ttu-id="f6169-136">取得適用於 Windows 的 Node.js LTS</span><span class="sxs-lookup"><span data-stu-id="f6169-136">Get Node.js LTS for Windows</span></span>](https://nodejs.org/en/)

## <a name="install-nodejs-development-tools"></a><span data-ttu-id="f6169-137">安裝 Node.js 開發工具</span><span class="sxs-lookup"><span data-stu-id="f6169-137">Install Node.js development tools</span></span>

<span data-ttu-id="f6169-138">您使用 [gulp.js](http://gulpjs.com/) 來自動化部署和執行指令碼。</span><span class="sxs-lookup"><span data-stu-id="f6169-138">You use [gulp.js](http://gulpjs.com/) to automate deployment and execution of scripts.</span></span>

<span data-ttu-id="f6169-139">按 `Windows + R`，輸入 `cmd`，然後按 `Enter` 開啟命令提示字元視窗，執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="f6169-139">Press `Windows + R`, type `cmd` and press `Enter` to open a Command Prompt window, and then run the following command:</span></span>

```cmd
npm install -g gulp
```

<span data-ttu-id="f6169-140">如果安裝遇到問題，請參閱[疑難排解指南](iot-hub-gateway-kit-c-sim-troubleshooting.md)，裡面有常見問題的解決辦法。</span><span class="sxs-lookup"><span data-stu-id="f6169-140">If you experience issues with the installation, see the [troubleshooting guide](iot-hub-gateway-kit-c-sim-troubleshooting.md) for solutions to common problems.</span></span>

> [!Note]
> <span data-ttu-id="f6169-141">需有節點、NPM、Gulp 才能執行 Node.js 開發的自動化指令碼。</span><span class="sxs-lookup"><span data-stu-id="f6169-141">Node, NPM and Gulp are required to run automation scripts developed in Node.js.</span></span>

## <a name="install-python"></a><span data-ttu-id="f6169-142">安裝 Python</span><span class="sxs-lookup"><span data-stu-id="f6169-142">Install Python</span></span>

<span data-ttu-id="f6169-143">您可以選擇 Python 2.7、3.4 或 3.5。</span><span class="sxs-lookup"><span data-stu-id="f6169-143">You can choose from Python 2.7, 3.4 or 3.5.</span></span> <span data-ttu-id="f6169-144">在本教學課程中，我們使用 Python 2.7。</span><span class="sxs-lookup"><span data-stu-id="f6169-144">In this tutorial, we use Python 2.7.</span></span> <span data-ttu-id="f6169-145">如果您已經安裝 Python，請移至下一節。</span><span class="sxs-lookup"><span data-stu-id="f6169-145">If you've already installed python, go to the next section.</span></span>

[<span data-ttu-id="f6169-146">取得適用於 Windows 的 Python</span><span class="sxs-lookup"><span data-stu-id="f6169-146">Get Python for Windows</span></span>](https://www.python.org/downloads/)

<span data-ttu-id="f6169-147">您也必須將安裝 python.exe 和 pip.exe 的資料夾路徑新增到系統 `PATH` 環境變數。</span><span class="sxs-lookup"><span data-stu-id="f6169-147">You also need to add the path of the folders where Python.exe and pip.exe are installed to the system `PATH` environment variable.</span></span> <span data-ttu-id="f6169-148">根據預設，python.exe 是安裝在 `C:\Python27`，而 pip.exe 是安裝在 `C:\Python27\Scripts`。</span><span class="sxs-lookup"><span data-stu-id="f6169-148">By default, python.exe is installed in `C:\Python27` and pip.exe is installed in `C:\Python27\Scripts`.</span></span>

## <a name="install-the-azure-cli"></a><span data-ttu-id="f6169-149">安裝 Azure CLI</span><span class="sxs-lookup"><span data-stu-id="f6169-149">Install the Azure CLI</span></span>

<span data-ttu-id="f6169-150">若要安裝 Azure CLI，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="f6169-150">To install the Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="f6169-151">以系統管理員身分開啟 [命令提示字元] 視窗。</span><span class="sxs-lookup"><span data-stu-id="f6169-151">Open a Command Prompt window as an administrator.</span></span>

2. <span data-ttu-id="f6169-152">執行以下命令來安裝 Azure CLI：</span><span class="sxs-lookup"><span data-stu-id="f6169-152">Install the Azure CLI by running the following commands:</span></span>

   ```cmd
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```

   <span data-ttu-id="f6169-153">安裝可能需要 5 分鐘。</span><span class="sxs-lookup"><span data-stu-id="f6169-153">The installation might take 5 minutes.</span></span>

3. <span data-ttu-id="f6169-154">執行下列命令以驗證安裝：</span><span class="sxs-lookup"><span data-stu-id="f6169-154">Verify the installation by running the following command:</span></span>

   ```cmd
   az iot -h
   ```

   <span data-ttu-id="f6169-155">如果已成功安裝，您應該會看見下列輸出。</span><span class="sxs-lookup"><span data-stu-id="f6169-155">You should see the following output if the installation is successful.</span></span>

   ![確認 Azure CLI 安裝](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_win.png)

## <a name="install-visual-studio-code"></a><span data-ttu-id="f6169-157">安裝 Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="f6169-157">Install Visual Studio Code</span></span>

<span data-ttu-id="f6169-158">您在本教學課程稍後章節會使用 Visual Studio Code 來編輯設定檔。</span><span class="sxs-lookup"><span data-stu-id="f6169-158">You use Visual Studio Code later in the tutorial to edit configuration files.</span></span>

<span data-ttu-id="f6169-159">[下載](https://code.visualstudio.com/docs/setup/windows)並安裝 Visual Studio Code。</span><span class="sxs-lookup"><span data-stu-id="f6169-159">[Download](https://code.visualstudio.com/docs/setup/windows) and install Visual Studio Code.</span></span>

## <a name="summary"></a><span data-ttu-id="f6169-160">摘要</span><span class="sxs-lookup"><span data-stu-id="f6169-160">Summary</span></span>

<span data-ttu-id="f6169-161">您已在主機電腦上安裝所有必要的工具和軟體。</span><span class="sxs-lookup"><span data-stu-id="f6169-161">You've installed all the required tools and software on your host computer.</span></span> <span data-ttu-id="f6169-162">下一步是使用 Azure CLI 建立 IoT 中樞，並且在 IoT 中樞登錄您的裝置。</span><span class="sxs-lookup"><span data-stu-id="f6169-162">Your next task is to use the Azure CLI to create an IoT hub and register your device in your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f6169-163">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f6169-163">Next steps</span></span>
[<span data-ttu-id="f6169-164">建立 IoT 中樞並登錄您的裝置</span><span class="sxs-lookup"><span data-stu-id="f6169-164">Create an IoT hub and register your device</span></span>](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)
