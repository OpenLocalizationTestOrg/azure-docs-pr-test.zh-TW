---
title: "Connect Intel Edison (C) tooAzure IoT-第 1 課： 取得工具 (Ubuntu) |Microsoft 文件"
description: "下載並安裝 hello 必要工具及軟體 hello 第一個範例應用程式 Edison Ubuntu 上。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "arduino 開發工具, iot 開發, iot 軟體, 物聯網軟體, 在 ubuntu 上安裝 git, 在 ubuntu 上安裝 node js"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: 4c7b8e04-b892-459b-8b03-85bcaff2465c
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 1ebd599def4e8bb33d891517cc76bc2fcdc3c35a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-ubuntu-1604"></a><span data-ttu-id="31fb1-104">取得 hello 工具 (Ubuntu 16.04)</span><span class="sxs-lookup"><span data-stu-id="31fb1-104">Get hello tools (Ubuntu 16.04)</span></span>

> [!div class="op_single_selector"]
> * <span data-ttu-id="31fb1-105">[Windows 7 或更新版本][windows]</span><span class="sxs-lookup"><span data-stu-id="31fb1-105">[Windows 7 or later][windows]</span></span>
> * <span data-ttu-id="31fb1-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="31fb1-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="31fb1-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="31fb1-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="31fb1-108">將執行的作業</span><span class="sxs-lookup"><span data-stu-id="31fb1-108">What you will do</span></span>
<span data-ttu-id="31fb1-109">下載 hello 開發工具及 hello 第一個範例應用程式 Intel Edison hello 軟體。</span><span class="sxs-lookup"><span data-stu-id="31fb1-109">Download hello development tools and hello software for hello first sample application for your Intel Edison.</span></span> <span data-ttu-id="31fb1-110">如果您有任何問題，尋找解決方案上 hello[疑難排解頁面][troubleshooting]。</span><span class="sxs-lookup"><span data-stu-id="31fb1-110">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

> [!NOTE]
> <span data-ttu-id="31fb1-111">雖然 hello 程式設計語言的 hello 主要邏輯是 C 的 Node.js 工具 hello 課程 toobuild 中使用，而且部署範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="31fb1-111">Although hello programming language of hello main logic is C, Node.js tools are used in hello lessons toobuild and deploy sample applications.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="31fb1-112">學習目標</span><span class="sxs-lookup"><span data-stu-id="31fb1-112">What you will learn</span></span>
<span data-ttu-id="31fb1-113">在本文中，您將了解：</span><span class="sxs-lookup"><span data-stu-id="31fb1-113">In this article, you will learn:</span></span>

* <span data-ttu-id="31fb1-114">如何 tooinstall Git 和 Node.js</span><span class="sxs-lookup"><span data-stu-id="31fb1-114">How tooinstall Git and Node.js</span></span>
  * <span data-ttu-id="31fb1-115">[Git](https://git-scm.com) 是一個開放原始碼分散式版本控制系統。</span><span class="sxs-lookup"><span data-stu-id="31fb1-115">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="31fb1-116">這個發行項的 hello 範例應用程式會儲存在 Git。</span><span class="sxs-lookup"><span data-stu-id="31fb1-116">hello sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="31fb1-117">[Node.js](https://nodejs.org/en/) 是一個具有豐富套件生態系統的 JavaScript 執行階段。</span><span class="sxs-lookup"><span data-stu-id="31fb1-117">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="31fb1-118">如何 toouse NPM tooinstall 其他 Node.js 開發工具。</span><span class="sxs-lookup"><span data-stu-id="31fb1-118">How toouse NPM tooinstall additional Node.js development tools.</span></span>
  * <span data-ttu-id="31fb1-119">hello 的最低必要的版本 Node.js 是 4.5 LTS。</span><span class="sxs-lookup"><span data-stu-id="31fb1-119">hello minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="31fb1-120">[NPM](https://www.npmjs.com)是其中一個 hello for Node.js 的封裝管理員。</span><span class="sxs-lookup"><span data-stu-id="31fb1-120">[NPM](https://www.npmjs.com) is one of hello package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="31fb1-121">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="31fb1-121">What you need</span></span>
<span data-ttu-id="31fb1-122">toocomplete 這項作業，您將需要：</span><span class="sxs-lookup"><span data-stu-id="31fb1-122">toocomplete this operation, you will need:</span></span>
* <span data-ttu-id="31fb1-123">網際網路連線 toodownload hello 開發工具和 hello 軟體。</span><span class="sxs-lookup"><span data-stu-id="31fb1-123">An Internet connection toodownload hello development tools and hello software.</span></span>
* <span data-ttu-id="31fb1-124">一部執行 Ubuntu 16.04 或以上版本的電腦。</span><span class="sxs-lookup"><span data-stu-id="31fb1-124">A computer that is running Ubuntu 16.04 or later.</span></span>

## <a name="install-git-nodejs-and-npm"></a><span data-ttu-id="31fb1-125">安裝 Git、Node.js 及 NPM</span><span class="sxs-lookup"><span data-stu-id="31fb1-125">Install Git, Node.js, and NPM</span></span>
<span data-ttu-id="31fb1-126">使用 hello 鍵盤快速鍵`Ctrl + Alt + T`tooopen 終端機及執行 hello，下列命令：</span><span class="sxs-lookup"><span data-stu-id="31fb1-126">Use hello keyboard shortcut `Ctrl + Alt + T` tooopen a terminal and run hello following commands:</span></span>

```bash
sudo apt-get update
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install -y nodejs
sudo apt-get install git
```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="31fb1-127">安裝額外的 Node.js 開發工具</span><span class="sxs-lookup"><span data-stu-id="31fb1-127">Install additional Node.js development tools</span></span>
<span data-ttu-id="31fb1-128">使用[cwd](http://gulpjs.com) hello 範例應用程式 tooEdison tooautomate hello 部署。</span><span class="sxs-lookup"><span data-stu-id="31fb1-128">Use [gulp.js](http://gulpjs.com) tooautomate hello deployment of hello sample application tooEdison.</span></span>

<span data-ttu-id="31fb1-129">安裝`gulp`藉由執行下列命令在 hello 終端機中的 hello:</span><span class="sxs-lookup"><span data-stu-id="31fb1-129">Install `gulp` by running hello following command in hello terminal:</span></span>

```bash
sudo npm install -g gulp
```

<span data-ttu-id="31fb1-130">如果您遇到安裝 Node.js 和這些額外的開發工具在 Ubuntu 上的問題，請參閱 hello[疑難排解指南][ troubleshooting]解決方案 toocommon 問題。</span><span class="sxs-lookup"><span data-stu-id="31fb1-130">If you experience issues installing Node.js and these additional development tools on Ubuntu, see hello [troubleshooting guide][troubleshooting] for solutions toocommon problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="31fb1-131">安裝 Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="31fb1-131">Install Visual Studio Code</span></span>
<span data-ttu-id="31fb1-132">[下載](https://code.visualstudio.com/docs/setup/linux)並安裝 Visual Studio Code。</span><span class="sxs-lookup"><span data-stu-id="31fb1-132">[Download](https://code.visualstudio.com/docs/setup/linux) and install Visual Studio Code.</span></span> <span data-ttu-id="31fb1-133">Visual Studio Code 是一個輕量且強大的原始程式碼編輯器，適用於 Windows、Linux 及 macOS。</span><span class="sxs-lookup"><span data-stu-id="31fb1-133">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="31fb1-134">您可以使用此編輯器 hello 教學課程 tooedit hello 範例程式碼中的更新版本。</span><span class="sxs-lookup"><span data-stu-id="31fb1-134">You use this editor later in hello tutorial tooedit hello sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="31fb1-135">摘要</span><span class="sxs-lookup"><span data-stu-id="31fb1-135">Summary</span></span>
<span data-ttu-id="31fb1-136">您已安裝所需的 hello 開發工具及軟體 hello 第一個範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="31fb1-136">You've installed hello required development tools and software for hello first sample application.</span></span> <span data-ttu-id="31fb1-137">hello 下一個工作是 toocreate、 部署和執行上 Edison hello 範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="31fb1-137">hello next task is toocreate, deploy, and run hello sample application on Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="31fb1-138">後續步驟</span><span class="sxs-lookup"><span data-stu-id="31fb1-138">Next steps</span></span>
<span data-ttu-id="31fb1-139">[建立及部署 hello 閃爍範例應用程式][create-and-deploy-the-blink-application]</span><span class="sxs-lookup"><span data-stu-id="31fb1-139">[Create and deploy hello blink sample application][create-and-deploy-the-blink-application]</span></span>

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[create-and-deploy-the-blink-application]: iot-hub-intel-edison-kit-c-lesson1-deploy-blink-app.md
[windows]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-mac.md
