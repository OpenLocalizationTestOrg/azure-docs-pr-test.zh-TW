---
title: "模擬裝置與 Azure IoT 閘道 - 第 2 課︰取得工具 (Ubuntu) | Microsoft Docs"
description: "在執行 Ubuntu 的主機電腦上安裝工具和軟體、建立 IoT 中樞，並在 IoT 中樞登錄您的裝置。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "iot 開發, iot 軟體, iot 雲端服務, 物聯網軟體, azure cli, 在 ubuntu 上安裝 git, gulp 執行, 安裝 node js ubuntu"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: cf673154-ce67-4ed7-a9f7-2440301c6270
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 349daf5c3206f7fc20662beebd16928624142a56
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-ubuntu-1604"></a><span data-ttu-id="925c0-104">取得工具 (Ubuntu 16.04)</span><span class="sxs-lookup"><span data-stu-id="925c0-104">Get the tools (Ubuntu 16.04)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="925c0-105">Windows 7 或更新版本</span><span class="sxs-lookup"><span data-stu-id="925c0-105">Windows 7 or later</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)
> * [<span data-ttu-id="925c0-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="925c0-106">Ubuntu 16.04</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="925c0-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="925c0-107">macOS 10.10</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="925c0-108">將執行的作業</span><span class="sxs-lookup"><span data-stu-id="925c0-108">What you will do</span></span>

- <span data-ttu-id="925c0-109">安裝 Git、Node.js、Gulp、Python。</span><span class="sxs-lookup"><span data-stu-id="925c0-109">Install Git, Node.js, Gulp, Python.</span></span>
- <span data-ttu-id="925c0-110">安裝 Azure 命令列介面 (Azure CLI)。</span><span class="sxs-lookup"><span data-stu-id="925c0-110">Install the Azure command-line interface (Azure CLI).</span></span> 

<span data-ttu-id="925c0-111">如果您有任何問題，請在[疑難排解頁面](iot-hub-gateway-kit-c-sim-troubleshooting.md)尋求解決方案。</span><span class="sxs-lookup"><span data-stu-id="925c0-111">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>
## <a name="what-you-will-learn"></a><span data-ttu-id="925c0-112">學習目標</span><span class="sxs-lookup"><span data-stu-id="925c0-112">What you will learn</span></span>

<span data-ttu-id="925c0-113">在這一課，您將了解：</span><span class="sxs-lookup"><span data-stu-id="925c0-113">In this lesson, you will learn:</span></span>

- <span data-ttu-id="925c0-114">如何安裝 Git 和 Node.js。</span><span class="sxs-lookup"><span data-stu-id="925c0-114">How to install Git and Node.js.</span></span>
  - <span data-ttu-id="925c0-115">Git 是一個開放原始碼分散式版本控制系統。</span><span class="sxs-lookup"><span data-stu-id="925c0-115">Git is an open source distributed version control system.</span></span> <span data-ttu-id="925c0-116">本課程的範例應用程式將會儲存在 Git 上。</span><span class="sxs-lookup"><span data-stu-id="925c0-116">The sample application for this lesson is stored on Git.</span></span>
  - <span data-ttu-id="925c0-117">Node.js 是一個具有豐富套件生態系統的 JavaScript 執行階段。</span><span class="sxs-lookup"><span data-stu-id="925c0-117">Node.js is a JavaScript runtime with a rich package ecosystem.</span></span>
- <span data-ttu-id="925c0-118">如何使用 NPM 安裝 Node.js 開發工具。</span><span class="sxs-lookup"><span data-stu-id="925c0-118">How to use NPM to install Node.js development tools.</span></span>
  - <span data-ttu-id="925c0-119">Node.js 的版本最低需求為 4.5 LTS。</span><span class="sxs-lookup"><span data-stu-id="925c0-119">The minimum required version of Node.js is 4.5 LTS.</span></span>
  - <span data-ttu-id="925c0-120">NPM 是 Node.js 的其中一個套件管理員。</span><span class="sxs-lookup"><span data-stu-id="925c0-120">NPM is one of the package managers for Node.js.</span></span>
- <span data-ttu-id="925c0-121">如何安裝 Visual Studio Code。</span><span class="sxs-lookup"><span data-stu-id="925c0-121">How to install Visual Studio Code.</span></span>
  - <span data-ttu-id="925c0-122">Visual Studio Code 是一個跨平台、輕量且強大的原始程式碼編輯器，適用於 Windows、Linux 及 macOS。</span><span class="sxs-lookup"><span data-stu-id="925c0-122">Visual Studio Code is a cross platform, lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="925c0-123">它對偵錯、內嵌的 Git 控制項、語法反白顯示、智慧型程式碼完成、程式碼片段、程式碼重構也有絕佳的支援。</span><span class="sxs-lookup"><span data-stu-id="925c0-123">It has great support for debugging, embedded Git control, syntax highlighting, intelligent code completion, snippets, and code refactoring as well.</span></span>
- <span data-ttu-id="925c0-124">如何安裝 Azure CLI</span><span class="sxs-lookup"><span data-stu-id="925c0-124">How to install the Azure CLI</span></span>
  - <span data-ttu-id="925c0-125">Azure CLI 提供適用於 Azure 的多平台命令列體驗。</span><span class="sxs-lookup"><span data-stu-id="925c0-125">The Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="925c0-126">您可直接從命令列工作以佈建和管理資源。</span><span class="sxs-lookup"><span data-stu-id="925c0-126">You work directly from a command line to provision and manage resources.</span></span>
- <span data-ttu-id="925c0-127">如何使用 Azure CLI 建立 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="925c0-127">How to use the Azure CLI to create an IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="925c0-128">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="925c0-128">What you need</span></span>

- <span data-ttu-id="925c0-129">可下載工具和軟體的網際網路連線。</span><span class="sxs-lookup"><span data-stu-id="925c0-129">An Internet connection to download the tools and software.</span></span>
- <span data-ttu-id="925c0-130">一部執行 Ubuntu 16.04 或以上版本的電腦。</span><span class="sxs-lookup"><span data-stu-id="925c0-130">A computer that is running Ubuntu 16.04 or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="925c0-131">安裝 Git 和 Node.js</span><span class="sxs-lookup"><span data-stu-id="925c0-131">Install Git and Node.js</span></span>

<span data-ttu-id="925c0-132">若要安裝 Git 和 Node.js，遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="925c0-132">To install Git and Node.js, follow these steps:</span></span>

1. <span data-ttu-id="925c0-133">按 `Ctrl + Alt + T` 開啟終端機。</span><span class="sxs-lookup"><span data-stu-id="925c0-133">Press `Ctrl + Alt + T` to open a terminal.</span></span>
2. <span data-ttu-id="925c0-134">執行以下命令：</span><span class="sxs-lookup"><span data-stu-id="925c0-134">Run the following commands:</span></span>

   ```bash
   sudo apt-get update
   curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
   sudo apt-get install -y nodejs
   sudo apt-get install git
   ```

## <a name="install-nodejs-development-tools"></a><span data-ttu-id="925c0-135">安裝 Node.js 開發工具</span><span class="sxs-lookup"><span data-stu-id="925c0-135">Install Node.js development tools</span></span>

<span data-ttu-id="925c0-136">您使用 [gulp.js](http://gulpjs.com/) 來自動化部署和執行指令碼。</span><span class="sxs-lookup"><span data-stu-id="925c0-136">You use [gulp.js](http://gulpjs.com/) to automate deployment and execution of scripts.</span></span>

<span data-ttu-id="925c0-137">若要安裝 gulp，在終端機中執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="925c0-137">To install gulp, run the following command in the terminal:</span></span>

```bash
sudo npm install -g gulp
```

<span data-ttu-id="925c0-138">如果安裝遇到問題，請參閱[疑難排解指南](iot-hub-gateway-kit-c-sim-troubleshooting.md)，裡面有常見問題的解決辦法。</span><span class="sxs-lookup"><span data-stu-id="925c0-138">If you experience issues with the installation, see the [troubleshooting guide](iot-hub-gateway-kit-c-sim-troubleshooting.md) for solutions to common problems.</span></span>

> [!Note]
> <span data-ttu-id="925c0-139">需有節點、NPM、Gulp 才能執行 Node.js 開發的自動化指令碼。</span><span class="sxs-lookup"><span data-stu-id="925c0-139">Node, NPM and Gulp are required to run automation scripts developed in Node.js.</span></span>

## <a name="install-the-azure-cli"></a><span data-ttu-id="925c0-140">安裝 Azure CLI</span><span class="sxs-lookup"><span data-stu-id="925c0-140">Install the Azure CLI</span></span>

<span data-ttu-id="925c0-141">若要安裝 Azure CLI，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="925c0-141">To install the Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="925c0-142">在終端機中執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="925c0-142">Run the following commands in the terminal:</span></span>

   ```bash
   sudo apt-get update
   sudo apt-get install -y libssl-dev libffi-dev
   sudo apt-get install -y python-dev
   sudo apt-get install -y build-essential
   sudo apt-get install -y python-pip
   sudo pip install --upgrade azure-cli
   sudo pip install --upgrade azure-cli-iot
   ```

   <span data-ttu-id="925c0-143">安裝可能需要 5 分鐘。</span><span class="sxs-lookup"><span data-stu-id="925c0-143">The installation might take 5 minutes.</span></span>

2. <span data-ttu-id="925c0-144">執行下列命令以驗證安裝：</span><span class="sxs-lookup"><span data-stu-id="925c0-144">Verify the installation by running the following command:</span></span>

   ```bash
   az iot -h
   ```
<span data-ttu-id="925c0-145">如果已成功安裝，您應該會看見下列輸出。</span><span class="sxs-lookup"><span data-stu-id="925c0-145">You should see the following output if the installation is successful.</span></span>
<span data-ttu-id="925c0-146">![確認 Azure CLI 安裝](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_ubuntu.png)</span><span class="sxs-lookup"><span data-stu-id="925c0-146">![Verify Azure CLI installation](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_ubuntu.png)</span></span>

### <a name="install-visual-studio-code"></a><span data-ttu-id="925c0-147">安裝 Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="925c0-147">Install Visual Studio Code</span></span>

<span data-ttu-id="925c0-148">您在本教學課程稍後章節會使用 Visual Studio Code 來編輯設定檔。</span><span class="sxs-lookup"><span data-stu-id="925c0-148">You use Visual Studio Code later in the tutorial to edit configuration files.</span></span>

<span data-ttu-id="925c0-149">[下載](https://code.visualstudio.com/docs/setup/linux)並安裝 Visual Studio Code。</span><span class="sxs-lookup"><span data-stu-id="925c0-149">[Download](https://code.visualstudio.com/docs/setup/linux) and install Visual Studio Code.</span></span>

## <a name="summary"></a><span data-ttu-id="925c0-150">摘要</span><span class="sxs-lookup"><span data-stu-id="925c0-150">Summary</span></span>

<span data-ttu-id="925c0-151">您已在主機電腦上安裝所有必要的工具和軟體。</span><span class="sxs-lookup"><span data-stu-id="925c0-151">You've installed all the required tools and software on your host computer.</span></span> <span data-ttu-id="925c0-152">下一步是使用 Azure CLI 建立 IoT 中樞，並且在 IoT 中樞登錄您的裝置。</span><span class="sxs-lookup"><span data-stu-id="925c0-152">Your next task is to use the Azure CLI to create an IoT hub and register your device in your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="925c0-153">後續步驟</span><span class="sxs-lookup"><span data-stu-id="925c0-153">Next steps</span></span>
[<span data-ttu-id="925c0-154">建立 IoT 中樞並登錄您的裝置</span><span class="sxs-lookup"><span data-stu-id="925c0-154">Create an IoT hub and register your device</span></span>](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)
