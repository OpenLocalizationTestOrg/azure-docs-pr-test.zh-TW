---
title: "模擬裝置與 Azure IoT 閘道 - 第 2 課︰取得工具 (Windows) | Microsoft Docs"
description: "執行 Windows 的主機電腦上安裝 hello 工具和 hello 軟體建立 IoT 中心時，在 hello IoT 中樞註冊您的裝置。"
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
ms.openlocfilehash: 7ca3c9f11eb232f853fc8fd921b0a49ae37d0184
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-windows-7-and-later"></a><span data-ttu-id="58b34-104">取得 hello tools (Windows 7 及更新版本)</span><span class="sxs-lookup"><span data-stu-id="58b34-104">Get hello tools (Windows 7 and later)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="58b34-105">Windows 7 或更新版本</span><span class="sxs-lookup"><span data-stu-id="58b34-105">Windows 7 or later</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)
> * [<span data-ttu-id="58b34-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="58b34-106">Ubuntu 16.04</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="58b34-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="58b34-107">macOS 10.10</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="58b34-108">將執行的作業</span><span class="sxs-lookup"><span data-stu-id="58b34-108">What you will do</span></span>

- <span data-ttu-id="58b34-109">安裝 Git、Node.js、Gulp、Python。</span><span class="sxs-lookup"><span data-stu-id="58b34-109">Install Git, Node.js, Gulp, Python.</span></span>
- <span data-ttu-id="58b34-110">安裝 hello Azure 命令列介面 (Azure CLI)。</span><span class="sxs-lookup"><span data-stu-id="58b34-110">Install hello Azure command-line interface (Azure CLI).</span></span> 

<span data-ttu-id="58b34-111">如果您有任何問題，尋找解決方案上 hello[疑難排解頁面](iot-hub-gateway-kit-c-sim-troubleshooting.md)。</span><span class="sxs-lookup"><span data-stu-id="58b34-111">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="58b34-112">學習目標</span><span class="sxs-lookup"><span data-stu-id="58b34-112">What you will learn</span></span>

<span data-ttu-id="58b34-113">在這一課，您將了解：</span><span class="sxs-lookup"><span data-stu-id="58b34-113">In this lesson, you will learn:</span></span>

- <span data-ttu-id="58b34-114">如何 tooinstall [Git](https://git-scm.com/)和[Node.js](https://nodejs.org/en/)。</span><span class="sxs-lookup"><span data-stu-id="58b34-114">How tooinstall [Git](https://git-scm.com/) and [Node.js](https://nodejs.org/en/).</span></span>
  - <span data-ttu-id="58b34-115">Git 是一個開放原始碼分散式版本控制系統。</span><span class="sxs-lookup"><span data-stu-id="58b34-115">Git is an open source distributed version control system.</span></span> <span data-ttu-id="58b34-116">本課程中的 hello 範例應用程式會儲存在 Git。</span><span class="sxs-lookup"><span data-stu-id="58b34-116">hello sample application for this lesson is stored on Git.</span></span>
  - <span data-ttu-id="58b34-117">Node.js 是一個具有豐富套件生態系統的 JavaScript 執行階段。</span><span class="sxs-lookup"><span data-stu-id="58b34-117">Node.js is a JavaScript runtime with a rich package ecosystem.</span></span>
- <span data-ttu-id="58b34-118">如何 toouse [NPM](https://www.npmjs.com/) tooinstall Node.js 開發工具。</span><span class="sxs-lookup"><span data-stu-id="58b34-118">How toouse [NPM](https://www.npmjs.com/) tooinstall Node.js development tools.</span></span>
  - <span data-ttu-id="58b34-119">hello 的最低必要的版本 Node.js 是 4.5 LTS。</span><span class="sxs-lookup"><span data-stu-id="58b34-119">hello minimum required version of Node.js is 4.5 LTS.</span></span>
  - <span data-ttu-id="58b34-120">NPM 是一個 Node.js 的 hello 封裝管理員。</span><span class="sxs-lookup"><span data-stu-id="58b34-120">NPM is one of hello package managers for Node.js.</span></span>
- <span data-ttu-id="58b34-121">如何 tooinstall Visual Studio 程式碼。</span><span class="sxs-lookup"><span data-stu-id="58b34-121">How tooinstall Visual Studio Code.</span></span>
  - <span data-ttu-id="58b34-122">Visual Studio Code 是一個跨平台、輕量且強大的原始程式碼編輯器，適用於 Windows、Linux 及 macOS。</span><span class="sxs-lookup"><span data-stu-id="58b34-122">Visual Studio Code is a cross platform, lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="58b34-123">它對偵錯、內嵌的 Git 控制項、語法反白顯示、智慧型程式碼完成、程式碼片段、程式碼重構也有絕佳的支援。</span><span class="sxs-lookup"><span data-stu-id="58b34-123">It has great support for debugging, embedded Git control, syntax highlighting, intelligent code completion, snippets, and code refactoring as well.</span></span>
- <span data-ttu-id="58b34-124">如何 tooinstall Python。</span><span class="sxs-lookup"><span data-stu-id="58b34-124">How tooinstall Python.</span></span>
  - <span data-ttu-id="58b34-125">Python 是普遍使用的高階、一般用途、解譯、動態的程式設計語言。</span><span class="sxs-lookup"><span data-stu-id="58b34-125">Python is a widely used high-level, general-purpose, interpreted and dynamic programming language.</span></span>
- <span data-ttu-id="58b34-126">如何 tooinstall hello Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="58b34-126">How tooinstall hello Azure CLI.</span></span>
  - <span data-ttu-id="58b34-127">hello Azure CLI 提供 Azure 的多平台命令列體驗。</span><span class="sxs-lookup"><span data-stu-id="58b34-127">hello Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="58b34-128">您可以直接從命令列 tooprovision 工作和管理資源。</span><span class="sxs-lookup"><span data-stu-id="58b34-128">You work directly from a command line tooprovision and manage resources.</span></span>
- <span data-ttu-id="58b34-129">如何 toouse hello Azure CLI toocreate IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="58b34-129">How toouse hello Azure CLI toocreate an IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="58b34-130">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="58b34-130">What you need</span></span>

- <span data-ttu-id="58b34-131">網際網路連線 toodownload hello 工具和軟體。</span><span class="sxs-lookup"><span data-stu-id="58b34-131">An Internet connection toodownload hello tools and software.</span></span>
- <span data-ttu-id="58b34-132">Windows 電腦。</span><span class="sxs-lookup"><span data-stu-id="58b34-132">A Windows computer.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="58b34-133">安裝 Git 和 Node.js</span><span class="sxs-lookup"><span data-stu-id="58b34-133">Install Git and Node.js</span></span>

<span data-ttu-id="58b34-134">按一下下列連結 toodownload hello 並安裝 Git 和 Node.js LTS for Windows。</span><span class="sxs-lookup"><span data-stu-id="58b34-134">Click hello following links toodownload and install Git and Node.js LTS for Windows.</span></span>

- [<span data-ttu-id="58b34-135">取得 Git for Windows</span><span class="sxs-lookup"><span data-stu-id="58b34-135">Get Git for Windows</span></span>](https://git-scm.com/download/win/)
- [<span data-ttu-id="58b34-136">取得適用於 Windows 的 Node.js LTS</span><span class="sxs-lookup"><span data-stu-id="58b34-136">Get Node.js LTS for Windows</span></span>](https://nodejs.org/en/)

## <a name="install-nodejs-development-tools"></a><span data-ttu-id="58b34-137">安裝 Node.js 開發工具</span><span class="sxs-lookup"><span data-stu-id="58b34-137">Install Node.js development tools</span></span>

<span data-ttu-id="58b34-138">您使用[cwd](http://gulpjs.com/) tooautomate 部署和執行指令碼。</span><span class="sxs-lookup"><span data-stu-id="58b34-138">You use [gulp.js](http://gulpjs.com/) tooautomate deployment and execution of scripts.</span></span>

<span data-ttu-id="58b34-139">按`Windows + R`，型別`cmd`按`Enter`tooopen 的命令提示字元視窗，然後執行的 hello 遵從命令：</span><span class="sxs-lookup"><span data-stu-id="58b34-139">Press `Windows + R`, type `cmd` and press `Enter` tooopen a Command Prompt window, and then run hello following command:</span></span>

```cmd
npm install -g gulp
```

<span data-ttu-id="58b34-140">如果您遇到 hello 安裝問題，請參閱 hello[疑難排解指南](iot-hub-gateway-kit-c-sim-troubleshooting.md)解決方案 toocommon 問題。</span><span class="sxs-lookup"><span data-stu-id="58b34-140">If you experience issues with hello installation, see hello [troubleshooting guide](iot-hub-gateway-kit-c-sim-troubleshooting.md) for solutions toocommon problems.</span></span>

> [!Note]
> <span data-ttu-id="58b34-141">節點、 NPM 及 Gulp 是在 Node.js 中開發的必要的 toorun 自動化指令碼。</span><span class="sxs-lookup"><span data-stu-id="58b34-141">Node, NPM and Gulp are required toorun automation scripts developed in Node.js.</span></span>

## <a name="install-python"></a><span data-ttu-id="58b34-142">安裝 Python</span><span class="sxs-lookup"><span data-stu-id="58b34-142">Install Python</span></span>

<span data-ttu-id="58b34-143">您可以選擇 Python 2.7、3.4 或 3.5。</span><span class="sxs-lookup"><span data-stu-id="58b34-143">You can choose from Python 2.7, 3.4 or 3.5.</span></span> <span data-ttu-id="58b34-144">在本教學課程中，我們使用 Python 2.7。</span><span class="sxs-lookup"><span data-stu-id="58b34-144">In this tutorial, we use Python 2.7.</span></span> <span data-ttu-id="58b34-145">如果您已經安裝 python，請移 toohello 下一節。</span><span class="sxs-lookup"><span data-stu-id="58b34-145">If you've already installed python, go toohello next section.</span></span>

[<span data-ttu-id="58b34-146">取得適用於 Windows 的 Python</span><span class="sxs-lookup"><span data-stu-id="58b34-146">Get Python for Windows</span></span>](https://www.python.org/downloads/)

<span data-ttu-id="58b34-147">您也需要 hello 資料夾其中 Python.exe 和 pip.exe 是 已安裝的 toohello 系統 tooadd hello 路徑`PATH`環境變數。</span><span class="sxs-lookup"><span data-stu-id="58b34-147">You also need tooadd hello path of hello folders where Python.exe and pip.exe are installed toohello system `PATH` environment variable.</span></span> <span data-ttu-id="58b34-148">根據預設，python.exe 是安裝在 `C:\Python27`，而 pip.exe 是安裝在 `C:\Python27\Scripts`。</span><span class="sxs-lookup"><span data-stu-id="58b34-148">By default, python.exe is installed in `C:\Python27` and pip.exe is installed in `C:\Python27\Scripts`.</span></span>

## <a name="install-hello-azure-cli"></a><span data-ttu-id="58b34-149">安裝 hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="58b34-149">Install hello Azure CLI</span></span>

<span data-ttu-id="58b34-150">tooinstall hello Azure CLI，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="58b34-150">tooinstall hello Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="58b34-151">以系統管理員身分開啟 [命令提示字元] 視窗。</span><span class="sxs-lookup"><span data-stu-id="58b34-151">Open a Command Prompt window as an administrator.</span></span>

2. <span data-ttu-id="58b34-152">執行下列命令的 hello 安裝 hello Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="58b34-152">Install hello Azure CLI by running hello following commands:</span></span>

   ```cmd
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```

   <span data-ttu-id="58b34-153">hello 安裝可能需要 5 分鐘。</span><span class="sxs-lookup"><span data-stu-id="58b34-153">hello installation might take 5 minutes.</span></span>

3. <span data-ttu-id="58b34-154">執行下列命令的 hello 驗證 hello 安裝：</span><span class="sxs-lookup"><span data-stu-id="58b34-154">Verify hello installation by running hello following command:</span></span>

   ```cmd
   az iot -h
   ```

   <span data-ttu-id="58b34-155">您應該會看到下列 hello 輸出 hello 安裝是否成功。</span><span class="sxs-lookup"><span data-stu-id="58b34-155">You should see hello following output if hello installation is successful.</span></span>

   ![確認 Azure CLI 安裝](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_win.png)

## <a name="install-visual-studio-code"></a><span data-ttu-id="58b34-157">安裝 Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="58b34-157">Install Visual Studio Code</span></span>

<span data-ttu-id="58b34-158">您稍後在 hello 教學課程 tooedit 組態檔中使用 Visual Studio 程式碼。</span><span class="sxs-lookup"><span data-stu-id="58b34-158">You use Visual Studio Code later in hello tutorial tooedit configuration files.</span></span>

<span data-ttu-id="58b34-159">[下載](https://code.visualstudio.com/docs/setup/windows)並安裝 Visual Studio Code。</span><span class="sxs-lookup"><span data-stu-id="58b34-159">[Download](https://code.visualstudio.com/docs/setup/windows) and install Visual Studio Code.</span></span>

## <a name="summary"></a><span data-ttu-id="58b34-160">摘要</span><span class="sxs-lookup"><span data-stu-id="58b34-160">Summary</span></span>

<span data-ttu-id="58b34-161">您已在主機電腦上安裝所有必要的 hello 工具和軟體。</span><span class="sxs-lookup"><span data-stu-id="58b34-161">You've installed all hello required tools and software on your host computer.</span></span> <span data-ttu-id="58b34-162">下一個工作是 toouse hello Azure CLI toocreate IoT 中樞，並在您的 IoT 中樞註冊您的裝置。</span><span class="sxs-lookup"><span data-stu-id="58b34-162">Your next task is toouse hello Azure CLI toocreate an IoT hub and register your device in your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="58b34-163">後續步驟</span><span class="sxs-lookup"><span data-stu-id="58b34-163">Next steps</span></span>
[<span data-ttu-id="58b34-164">建立 IoT 中樞並登錄您的裝置</span><span class="sxs-lookup"><span data-stu-id="58b34-164">Create an IoT hub and register your device</span></span>](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)
