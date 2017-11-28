---
title: "連接 Arduino tooAzure IoT-第 1 課： 取得工具 (macOS) |Microsoft 文件"
description: "下載並安裝 hello 必要工具及軟體 hello 第一個範例應用程式 Adafruit 羽毛 M0 WiFi macOS 上。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "arduino 開發工具, iot 開發, iot 軟體, 物聯網軟體, 在 mac 上安裝 git, 在 mac 上安裝 node js"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 0262f3dd-0259-4eb0-962f-9fb534f8359e
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 5fd306fecd7259fb8f1e99d76282a1e464c4d4f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-macos-1010"></a><span data-ttu-id="350a4-104">取得 hello 工具 (macOS 10.10)</span><span class="sxs-lookup"><span data-stu-id="350a4-104">Get hello tools (macOS 10.10)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="350a4-105">[Windows 7 或更新版本][windows]</span><span class="sxs-lookup"><span data-stu-id="350a4-105">[Windows 7 or later][windows]</span></span>
> * <span data-ttu-id="350a4-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="350a4-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="350a4-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="350a4-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="350a4-108">將執行的作業</span><span class="sxs-lookup"><span data-stu-id="350a4-108">What you will do</span></span>

<span data-ttu-id="350a4-109">下載 hello 開發工具和 hello 第一個範例應用程式 Adafruit 羽毛 M0 WiFi Arduino 面板的 hello 軟體。</span><span class="sxs-lookup"><span data-stu-id="350a4-109">Download hello development tools and hello software for hello first sample application for your Adafruit Feather M0 WiFi Arduino board.</span></span> 

<span data-ttu-id="350a4-110">如果您有任何問題，尋找解決方案上 hello[疑難排解頁面][troubleshooting]。</span><span class="sxs-lookup"><span data-stu-id="350a4-110">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

> [!NOTE]
> <span data-ttu-id="350a4-111">雖然 hello 程式設計語言的 hello 主要邏輯是 Arduino 的 Node.js 工具用於 hello 課程 toobuild 及部署範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="350a4-111">Although hello programming language of hello main logic is Arduino, Node.js tools are used in hello lessons toobuild and deploy sample applications.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="350a4-112">學習目標</span><span class="sxs-lookup"><span data-stu-id="350a4-112">What you will learn</span></span>
<span data-ttu-id="350a4-113">在本文中，您將了解：</span><span class="sxs-lookup"><span data-stu-id="350a4-113">In this article, you will learn:</span></span>

* <span data-ttu-id="350a4-114">如何 tooinstall Git 和 Node.js。</span><span class="sxs-lookup"><span data-stu-id="350a4-114">How tooinstall Git and Node.js.</span></span>
  * <span data-ttu-id="350a4-115">[Git](https://git-scm.com) 是一個開放原始碼分散式版本控制系統。</span><span class="sxs-lookup"><span data-stu-id="350a4-115">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="350a4-116">這個發行項的 hello 範例應用程式會儲存在 Git。</span><span class="sxs-lookup"><span data-stu-id="350a4-116">hello sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="350a4-117">[Node.js](https://nodejs.org/en/) 是一個具有豐富套件生態系統的 JavaScript 執行階段。</span><span class="sxs-lookup"><span data-stu-id="350a4-117">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="350a4-118">如何 toouse NPM tooinstall 其他 Node.js 開發工具。</span><span class="sxs-lookup"><span data-stu-id="350a4-118">How toouse NPM tooinstall additional Node.js development tools.</span></span>
  * <span data-ttu-id="350a4-119">hello 的最低必要的版本 Node.js 是 4.5 LTS。</span><span class="sxs-lookup"><span data-stu-id="350a4-119">hello minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="350a4-120">[NPM](https://www.npmjs.com)是其中一個 hello for Node.js 的封裝管理員。</span><span class="sxs-lookup"><span data-stu-id="350a4-120">[NPM](https://www.npmjs.com) is one of hello package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="350a4-121">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="350a4-121">What you need</span></span>
<span data-ttu-id="350a4-122">toocomplete 這項作業，您將需要：</span><span class="sxs-lookup"><span data-stu-id="350a4-122">toocomplete this operation, you will need:</span></span>
* <span data-ttu-id="350a4-123">網際網路連線 toodownload hello 開發工具和 hello 軟體。</span><span class="sxs-lookup"><span data-stu-id="350a4-123">An Internet connection toodownload hello development tools and hello software.</span></span>
* <span data-ttu-id="350a4-124">執行 macOS Yosemite (10.10) 或更新版本的 Mac。</span><span class="sxs-lookup"><span data-stu-id="350a4-124">A Mac that is running macOS Yosemite (10.10) or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="350a4-125">安裝 Git 和 Node.js</span><span class="sxs-lookup"><span data-stu-id="350a4-125">Install Git and Node.js</span></span>
<span data-ttu-id="350a4-126">tooinstall Git 和 Node.js，使用 hello [Homebrew](http://brew.sh)封裝管理公用程式，依照下列步驟：</span><span class="sxs-lookup"><span data-stu-id="350a4-126">tooinstall Git and Node.js, use hello [Homebrew](http://brew.sh) package management utility by following these steps:</span></span>

1. <span data-ttu-id="350a4-127">安裝 Homebrew。</span><span class="sxs-lookup"><span data-stu-id="350a4-127">Install Homebrew.</span></span> <span data-ttu-id="350a4-128">如果您已經安裝 Homebrew，請移 toostep 2。</span><span class="sxs-lookup"><span data-stu-id="350a4-128">If you've already installed Homebrew, go toostep 2.</span></span>

   1. <span data-ttu-id="350a4-129">按`Cmd + Space`輸入`Terminal`tooopen 終端機。</span><span class="sxs-lookup"><span data-stu-id="350a4-129">Press `Cmd + Space` and enter `Terminal` tooopen a terminal.</span></span>
   2. <span data-ttu-id="350a4-130">執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="350a4-130">Run hello following command:</span></span>

      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```
2. <span data-ttu-id="350a4-131">安裝 Git 和 Node.js 藉由執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="350a4-131">Install Git and Node.js by running hello following command:</span></span>

   ```bash
   brew install node git
   ```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="350a4-132">安裝額外的 Node.js 開發工具</span><span class="sxs-lookup"><span data-stu-id="350a4-132">Install additional Node.js development tools</span></span>
<span data-ttu-id="350a4-133">使用[cwd](http://gulpjs.com) tooautomate hello 部署的 hello 範例應用程式 tooyour Arduino 面板。</span><span class="sxs-lookup"><span data-stu-id="350a4-133">Use [gulp.js](http://gulpjs.com) tooautomate hello deployment of hello sample application tooyour Arduino board.</span></span>

<span data-ttu-id="350a4-134">安裝`gulp`，`device-discovery-cli`藉由執行下列命令在 hello 終端機中的 hello:</span><span class="sxs-lookup"><span data-stu-id="350a4-134">Install `gulp`, `device-discovery-cli` by running hello following command in hello terminal:</span></span>

```bash
sudo npm install -g gulp device-discovery-cli
```

<span data-ttu-id="350a4-135">如果您遇到 macOS 上安裝 Node.js 和這些額外的開發工具的問題，請參閱 hello[疑難排解指南][ troubleshooting]解決方案 toocommon 問題。</span><span class="sxs-lookup"><span data-stu-id="350a4-135">If you experience issues installing Node.js and these additional development tools on macOS, see hello [troubleshooting guide][troubleshooting] for solutions toocommon problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="350a4-136">安裝 Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="350a4-136">Install Visual Studio Code</span></span>
<span data-ttu-id="350a4-137">[下載](https://code.visualstudio.com/docs/setup/osx)並安裝 Visual Studio Code。</span><span class="sxs-lookup"><span data-stu-id="350a4-137">[Download](https://code.visualstudio.com/docs/setup/osx) and install Visual Studio Code.</span></span> <span data-ttu-id="350a4-138">Visual Studio Code 是一個輕量且強大的原始程式碼編輯器，適用於 Windows、Linux 及 macOS。</span><span class="sxs-lookup"><span data-stu-id="350a4-138">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="350a4-139">您可以使用此編輯器 hello 教學課程 tooedit hello 範例程式碼中的更新版本。</span><span class="sxs-lookup"><span data-stu-id="350a4-139">You use this editor later in hello tutorial tooedit hello sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="350a4-140">摘要</span><span class="sxs-lookup"><span data-stu-id="350a4-140">Summary</span></span>
<span data-ttu-id="350a4-141">您已安裝所需的 hello 開發工具及軟體 hello 第一個範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="350a4-141">You've installed hello required development tools and software for hello first sample application.</span></span> <span data-ttu-id="350a4-142">hello 下一個工作是 toocreate、 部署和執行 Arduino 面板上的 hello 範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="350a4-142">hello next task is toocreate, deploy, and run hello sample application on your Arduino board.</span></span>

## <a name="next-steps"></a><span data-ttu-id="350a4-143">後續步驟</span><span class="sxs-lookup"><span data-stu-id="350a4-143">Next steps</span></span>
<span data-ttu-id="350a4-144">[建立及部署 hello 閃爍應用程式][create-and-deploy-the-blink-application]</span><span class="sxs-lookup"><span data-stu-id="350a4-144">[Create and deploy hello blink application][create-and-deploy-the-blink-application]</span></span>
<!-- Images and links -->

[windows]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-mac.md
[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[create-and-deploy-the-blink-application]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-deploy-blink-app.md