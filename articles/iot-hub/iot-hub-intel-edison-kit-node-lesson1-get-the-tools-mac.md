---
title: "將 Intel Edison (節點) 連接到 Azure IoT - 第 1 課：取得工具 (macOS) | Microsoft Docs"
description: "在 macOS 上針對 Edison 的第一個範例應用程式下載並安裝必要的工具和軟體。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "arduino 開發工具, iot 開發, iot 軟體, 物聯網軟體, 在 mac 上安裝 git, 在 mac 上安裝 node js"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: fb6742be-2825-4524-89f7-8ccb7e7f1de1
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: a5e406f49379e9f2192ee93334ab1dcf9f3e53d4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-macos-1010"></a><span data-ttu-id="99031-104">取得工具 (macOS 10.10)</span><span class="sxs-lookup"><span data-stu-id="99031-104">Get the tools (macOS 10.10)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="99031-105">[Windows 7 或更新版本][windows]</span><span class="sxs-lookup"><span data-stu-id="99031-105">[Windows 7 or later][windows]</span></span>
> * <span data-ttu-id="99031-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="99031-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="99031-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="99031-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="99031-108">將執行的作業</span><span class="sxs-lookup"><span data-stu-id="99031-108">What you will do</span></span>
<span data-ttu-id="99031-109">下載您 Intel Edison 第一個範例應用程式的開發工具和軟體。</span><span class="sxs-lookup"><span data-stu-id="99031-109">Download the development tools and the software for the first sample application for your Intel Edison.</span></span> <span data-ttu-id="99031-110">如果您有任何問題，請在[疑難排解頁面][troubleshooting]尋求解決方案。</span><span class="sxs-lookup"><span data-stu-id="99031-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="99031-111">學習目標</span><span class="sxs-lookup"><span data-stu-id="99031-111">What you will learn</span></span>
<span data-ttu-id="99031-112">在本文中，您將了解：</span><span class="sxs-lookup"><span data-stu-id="99031-112">In this article, you will learn:</span></span>

* <span data-ttu-id="99031-113">如何安裝 Git 和 Node.js。</span><span class="sxs-lookup"><span data-stu-id="99031-113">How to install Git and Node.js.</span></span>
  * <span data-ttu-id="99031-114">[Git](https://git-scm.com) 是一個開放原始碼分散式版本控制系統。</span><span class="sxs-lookup"><span data-stu-id="99031-114">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="99031-115">本文的範例應用程式將會儲存在 Git 上。</span><span class="sxs-lookup"><span data-stu-id="99031-115">The sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="99031-116">[Node.js](https://nodejs.org/en/) 是一個具有豐富套件生態系統的 JavaScript 執行階段。</span><span class="sxs-lookup"><span data-stu-id="99031-116">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="99031-117">如何使用 NPM 安裝其他 Node.js 開發工具。</span><span class="sxs-lookup"><span data-stu-id="99031-117">How to use NPM to install additional Node.js development tools.</span></span>
  * <span data-ttu-id="99031-118">Node.js 的版本最低需求為 4.5 LTS。</span><span class="sxs-lookup"><span data-stu-id="99031-118">The minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="99031-119">[NPM](https://www.npmjs.com) 是 Node.js 的其中一個套件管理員。</span><span class="sxs-lookup"><span data-stu-id="99031-119">[NPM](https://www.npmjs.com) is one of the package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="99031-120">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="99031-120">What you need</span></span>
<span data-ttu-id="99031-121">若要完成此作業，您需要：</span><span class="sxs-lookup"><span data-stu-id="99031-121">To complete this operation, you will need:</span></span>
* <span data-ttu-id="99031-122">網際網路連線以下載開發工具和軟體。</span><span class="sxs-lookup"><span data-stu-id="99031-122">An Internet connection to download the development tools and the software.</span></span>
* <span data-ttu-id="99031-123">執行 macOS Yosemite (10.10) 或更新版本的 Mac。</span><span class="sxs-lookup"><span data-stu-id="99031-123">A Mac that is running macOS Yosemite (10.10) or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="99031-124">安裝 Git 和 Node.js</span><span class="sxs-lookup"><span data-stu-id="99031-124">Install Git and Node.js</span></span>
<span data-ttu-id="99031-125">若要安裝 Git 和 Node.js，請遵循下列步驟以使用 [Homebrew](http://brew.sh) 套件管理公用程式︰</span><span class="sxs-lookup"><span data-stu-id="99031-125">To install Git and Node.js, use the [Homebrew](http://brew.sh) package management utility by following these steps:</span></span>

1. <span data-ttu-id="99031-126">安裝 Homebrew。</span><span class="sxs-lookup"><span data-stu-id="99031-126">Install Homebrew.</span></span> <span data-ttu-id="99031-127">如果您已經安裝 Homebrew，請移至步驟 2。</span><span class="sxs-lookup"><span data-stu-id="99031-127">If you've already installed Homebrew, go to step 2.</span></span>

   1. <span data-ttu-id="99031-128">按 `Cmd + Space` 並輸入 `Terminal` 以開啟終端機。</span><span class="sxs-lookup"><span data-stu-id="99031-128">Press `Cmd + Space` and enter `Terminal` to open a terminal.</span></span>
   2. <span data-ttu-id="99031-129">執行以下命令：</span><span class="sxs-lookup"><span data-stu-id="99031-129">Run the following command:</span></span>

      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```
2. <span data-ttu-id="99031-130">執行下列命令安裝 Git 和 Node.js：</span><span class="sxs-lookup"><span data-stu-id="99031-130">Install Git and Node.js by running the following command:</span></span>

   ```bash
   brew install node git
   ```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="99031-131">安裝額外的 Node.js 開發工具</span><span class="sxs-lookup"><span data-stu-id="99031-131">Install additional Node.js development tools</span></span>
<span data-ttu-id="99031-132">使用 [gulp.js](http://gulpjs.com) 來對 Edison 自動部署範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="99031-132">Use [gulp.js](http://gulpjs.com) to automate the deployment of the sample application to your Edison.</span></span>

<span data-ttu-id="99031-133">在終端機中執行下列命令以安裝 `gulp`：</span><span class="sxs-lookup"><span data-stu-id="99031-133">Install `gulp` by running the following command in the terminal:</span></span>

```bash
sudo npm install -g gulp
```

<span data-ttu-id="99031-134">如果您在 macOS 上安裝 Node.js 和這些額外的開發工具時遇到問題，請參閱[疑難排解指南][troubleshooting]以取得常見問題的解決方案。</span><span class="sxs-lookup"><span data-stu-id="99031-134">If you experience issues installing Node.js and these additional development tools on macOS, see the [troubleshooting guide][troubleshooting] for solutions to common problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="99031-135">安裝 Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="99031-135">Install Visual Studio Code</span></span>
<span data-ttu-id="99031-136">[下載](https://code.visualstudio.com/docs/setup/osx)並安裝 Visual Studio Code。</span><span class="sxs-lookup"><span data-stu-id="99031-136">[Download](https://code.visualstudio.com/docs/setup/osx) and install Visual Studio Code.</span></span> <span data-ttu-id="99031-137">Visual Studio Code 是一個輕量且強大的原始程式碼編輯器，適用於 Windows、Linux 及 macOS。</span><span class="sxs-lookup"><span data-stu-id="99031-137">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="99031-138">您可以稍後於教學課程中使用此編輯器來編輯範例程式碼。</span><span class="sxs-lookup"><span data-stu-id="99031-138">You use this editor later in the tutorial to edit the sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="99031-139">摘要</span><span class="sxs-lookup"><span data-stu-id="99031-139">Summary</span></span>
<span data-ttu-id="99031-140">您已安裝第一個範例應用程式所需的開發工具和軟體。</span><span class="sxs-lookup"><span data-stu-id="99031-140">You've installed the required development tools and software for the first sample application.</span></span> <span data-ttu-id="99031-141">下一個工作是在 Edison 上建立、部署和執行範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="99031-141">The next task is to create, deploy, and run the sample application on Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="99031-142">後續步驟</span><span class="sxs-lookup"><span data-stu-id="99031-142">Next steps</span></span>
<span data-ttu-id="99031-143">[1.3 建立並部署閃爍應用程式][create-and-deploy-the-blink-application]</span><span class="sxs-lookup"><span data-stu-id="99031-143">[Create and deploy the blink application][create-and-deploy-the-blink-application]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[create-and-deploy-the-blink-application]: iot-hub-intel-edison-kit-node-lesson1-deploy-blink-app.md
[windows]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-mac.md
