---
title: "將 Raspberry Pi (C) 連接到 Azure IoT - 第 1 課：取得工具 (macOS) | Microsoft Docs"
description: "在 macOS 上針對 Pi 的第一個範例應用程式下載並安裝必要的工具和軟體。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "iot 開發, iot 軟體, 物聯網軟體, 在 mac 上安裝 git, gulp 執行, 安裝 node js mac"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: fc6bd2c8-a847-4bf5-818f-6f7f9a6835ee
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 64db77040ef3482f213bd622320fdb5df243fa93
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-macos-1010"></a><span data-ttu-id="3fc95-104">取得工具 (macOS 10.10)</span><span class="sxs-lookup"><span data-stu-id="3fc95-104">Get the tools (macOS 10.10)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3fc95-105">Windows 7 或更新版本</span><span class="sxs-lookup"><span data-stu-id="3fc95-105">Windows 7 or later</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)
> * [<span data-ttu-id="3fc95-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="3fc95-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="3fc95-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="3fc95-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="3fc95-108">將執行的作業</span><span class="sxs-lookup"><span data-stu-id="3fc95-108">What you will do</span></span>
<span data-ttu-id="3fc95-109">下載您 Raspberry Pi 3 第一個範例應用程式的開發工具和軟體。</span><span class="sxs-lookup"><span data-stu-id="3fc95-109">Download the development tools and the software for the first sample application for your Raspberry Pi 3.</span></span> <span data-ttu-id="3fc95-110">如果您有任何問題，請在[疑難排解頁面](iot-hub-raspberry-pi-kit-c-troubleshooting.md)尋求解決方案。</span><span class="sxs-lookup"><span data-stu-id="3fc95-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

> [!NOTE]
> <span data-ttu-id="3fc95-111">雖然主要邏輯的程式語言是 C，但這些課程中會使用 Node.js 工具來探索裝置，以及建置和部署範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="3fc95-111">Although the programming language of the main logic is C, Node.js tools are used in the lessons to discover devices, and build and deploy sample applications.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="3fc95-112">學習目標</span><span class="sxs-lookup"><span data-stu-id="3fc95-112">What you will learn</span></span>
<span data-ttu-id="3fc95-113">在本文中，您將了解：</span><span class="sxs-lookup"><span data-stu-id="3fc95-113">In this article, you will learn:</span></span>

* <span data-ttu-id="3fc95-114">如何安裝 Git 和 Node.js。</span><span class="sxs-lookup"><span data-stu-id="3fc95-114">How to install Git and Node.js.</span></span>
  * <span data-ttu-id="3fc95-115">[Git](https://git-scm.com) 是一個開放原始碼分散式版本控制系統。</span><span class="sxs-lookup"><span data-stu-id="3fc95-115">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="3fc95-116">本文的範例應用程式將會儲存在 Git 上。</span><span class="sxs-lookup"><span data-stu-id="3fc95-116">The sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="3fc95-117">[Node.js](https://nodejs.org/en/) 是一個具有豐富套件生態系統的 JavaScript 執行階段。</span><span class="sxs-lookup"><span data-stu-id="3fc95-117">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="3fc95-118">如何使用 NPM 安裝其他 Node.js 開發工具。</span><span class="sxs-lookup"><span data-stu-id="3fc95-118">How to use NPM to install additional Node.js development tools.</span></span>
  * <span data-ttu-id="3fc95-119">Node.js 的版本最低需求為 4.5 LTS。</span><span class="sxs-lookup"><span data-stu-id="3fc95-119">The minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="3fc95-120">[NPM](https://www.npmjs.com) 是 Node.js 的其中一個套件管理員。</span><span class="sxs-lookup"><span data-stu-id="3fc95-120">[NPM](https://www.npmjs.com) is one of the package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="3fc95-121">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="3fc95-121">What you need</span></span>
<span data-ttu-id="3fc95-122">若要完成此作業，您需要：</span><span class="sxs-lookup"><span data-stu-id="3fc95-122">To complete this operation, you will need:</span></span>

* <span data-ttu-id="3fc95-123">網際網路連線以下載開發工具和軟體。</span><span class="sxs-lookup"><span data-stu-id="3fc95-123">An Internet connection to download the development tools and the software.</span></span>
* <span data-ttu-id="3fc95-124">執行 macOS Yosemite (10.10) 或更新版本的 Mac。</span><span class="sxs-lookup"><span data-stu-id="3fc95-124">A Mac that is running macOS Yosemite (10.10) or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="3fc95-125">安裝 Git 和 Node.js</span><span class="sxs-lookup"><span data-stu-id="3fc95-125">Install Git and Node.js</span></span>
<span data-ttu-id="3fc95-126">若要安裝 Git 和 Node.js，請遵循下列步驟以使用 [Homebrew](http://brew.sh) 套件管理公用程式︰</span><span class="sxs-lookup"><span data-stu-id="3fc95-126">To install Git and Node.js, use the [Homebrew](http://brew.sh) package management utility by following these steps:</span></span>

1. <span data-ttu-id="3fc95-127">安裝 Homebrew。</span><span class="sxs-lookup"><span data-stu-id="3fc95-127">Install Homebrew.</span></span> <span data-ttu-id="3fc95-128">如果您已經安裝 Homebrew，請移至步驟 2。</span><span class="sxs-lookup"><span data-stu-id="3fc95-128">If you've already installed Homebrew, go to step 2.</span></span>
   
   1. <span data-ttu-id="3fc95-129">按 `Cmd + Space` 並輸入 `Terminal` 以開啟終端機。</span><span class="sxs-lookup"><span data-stu-id="3fc95-129">Press `Cmd + Space` and enter `Terminal` to open a terminal.</span></span>
   2. <span data-ttu-id="3fc95-130">執行以下命令：</span><span class="sxs-lookup"><span data-stu-id="3fc95-130">Run the following command:</span></span>
      
      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```
2. <span data-ttu-id="3fc95-131">執行下列命令安裝 Git 和 Node.js：</span><span class="sxs-lookup"><span data-stu-id="3fc95-131">Install Git and Node.js by running the following command:</span></span>
   
   ```bash
   brew install node git
   ```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="3fc95-132">安裝額外的 Node.js 開發工具</span><span class="sxs-lookup"><span data-stu-id="3fc95-132">Install additional Node.js development tools</span></span>
<span data-ttu-id="3fc95-133">使用 [gulp.js](http://gulpjs.com) 自動將範例應用程式部署至 Pi。</span><span class="sxs-lookup"><span data-stu-id="3fc95-133">Use [gulp.js](http://gulpjs.com) to automate the deployment of the sample application to your Pi.</span></span> <span data-ttu-id="3fc95-134">使用 [device-discovery-cli](https://github.com/Azure/device-discovery-cli) 來擷取關於您 IoT 裝置的網路資訊。</span><span class="sxs-lookup"><span data-stu-id="3fc95-134">Use the [device-discovery-cli](https://github.com/Azure/device-discovery-cli) to retrieve network information about your IoT devices.</span></span>

<span data-ttu-id="3fc95-135">在終端機中執行下列命令以安裝 `gulp` 和 `device-discovery-cli`：</span><span class="sxs-lookup"><span data-stu-id="3fc95-135">Install `gulp` and `device-discovery-cli` by running the following command in the terminal:</span></span>

```bash
sudo npm install -g device-discovery-cli gulp
```

<span data-ttu-id="3fc95-136">如果您在 macOS 上安裝 Node.js 和這些額外的開發工具時遇到問題，請參閱[疑難排解指南](iot-hub-raspberry-pi-kit-c-troubleshooting.md)以取得常見問題的解決方案。</span><span class="sxs-lookup"><span data-stu-id="3fc95-136">If you experience issues installing Node.js and these additional development tools on macOS, see the [troubleshooting guide](iot-hub-raspberry-pi-kit-c-troubleshooting.md) for solutions to common problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="3fc95-137">安裝 Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="3fc95-137">Install Visual Studio Code</span></span>
<span data-ttu-id="3fc95-138">[下載](https://code.visualstudio.com/docs/setup/osx)並安裝 Visual Studio Code。</span><span class="sxs-lookup"><span data-stu-id="3fc95-138">[Download](https://code.visualstudio.com/docs/setup/osx) and install Visual Studio Code.</span></span> <span data-ttu-id="3fc95-139">Visual Studio Code 是一個輕量且強大的原始程式碼編輯器，適用於 Windows、Linux 及 macOS。</span><span class="sxs-lookup"><span data-stu-id="3fc95-139">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="3fc95-140">您可以稍後於教學課程中使用此編輯器來編輯範例程式碼。</span><span class="sxs-lookup"><span data-stu-id="3fc95-140">You use this editor later in the tutorial to edit the sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="3fc95-141">摘要</span><span class="sxs-lookup"><span data-stu-id="3fc95-141">Summary</span></span>
<span data-ttu-id="3fc95-142">您已安裝第一個範例應用程式所需的開發工具和軟體。</span><span class="sxs-lookup"><span data-stu-id="3fc95-142">You've installed the required development tools and software for the first sample application.</span></span> <span data-ttu-id="3fc95-143">下一個工作是在 Pi 上建立、部署和執行範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="3fc95-143">The next task is to create, deploy, and run the sample application on Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3fc95-144">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3fc95-144">Next steps</span></span>
[<span data-ttu-id="3fc95-145">1.3 建立並部署閃爍應用程式</span><span class="sxs-lookup"><span data-stu-id="3fc95-145">Create and deploy the blink application</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-deploy-blink-app.md)

