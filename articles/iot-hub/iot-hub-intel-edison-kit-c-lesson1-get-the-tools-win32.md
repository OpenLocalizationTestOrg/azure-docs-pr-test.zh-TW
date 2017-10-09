---
title: "Connect Intel Edison (C) tooAzure IoT-第 1 課： 取得 tools (Windows) |Microsoft 文件"
description: "下載並安裝在 Windows 7 和更新版本的 hello 必要的工具和 hello 第一個範例應用程式 Edison 的軟體。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "arduino 開發工具, iot 開發, iot 軟體, 物聯網軟體, 在 windows 上安裝 git, 在 windows 上安裝 node js"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: 7d29a358-544d-4657-a504-5ed9b79c2925
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 64d8684ffcb858845de02276a11cf2b2e5c701a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-windows-7-or-later"></a><span data-ttu-id="37611-104">取得 hello tools (Windows 7 或更新版本)</span><span class="sxs-lookup"><span data-stu-id="37611-104">Get hello tools (Windows 7 or later)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="37611-105">[Windows 7 或更新版本][windows]</span><span class="sxs-lookup"><span data-stu-id="37611-105">[Windows 7 or later][windows]</span></span>
> * <span data-ttu-id="37611-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="37611-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="37611-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="37611-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="37611-108">將執行的作業</span><span class="sxs-lookup"><span data-stu-id="37611-108">What you will do</span></span>
<span data-ttu-id="37611-109">下載 hello 開發工具及 hello 第一個範例應用程式 Intel Edison hello 軟體。</span><span class="sxs-lookup"><span data-stu-id="37611-109">Download hello development tools and hello software for hello first sample application for Intel Edison.</span></span> <span data-ttu-id="37611-110">如果您有任何問題，尋找解決方案上 hello[疑難排解頁面][troubleshooting]。</span><span class="sxs-lookup"><span data-stu-id="37611-110">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

> [!NOTE]
> <span data-ttu-id="37611-111">雖然 hello 程式設計語言的 hello 主要邏輯是 C 的 Node.js 工具 hello 課程 toobuild 中使用，而且部署範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="37611-111">Although hello programming language of hello main logic is C, Node.js tools are used in hello lessons toobuild and deploy sample applications.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="37611-112">學習目標</span><span class="sxs-lookup"><span data-stu-id="37611-112">What you will learn</span></span>
<span data-ttu-id="37611-113">在本文中，您將了解：</span><span class="sxs-lookup"><span data-stu-id="37611-113">In this article, you will learn:</span></span>

* <span data-ttu-id="37611-114">如何 tooinstall Git 和 Node.js。</span><span class="sxs-lookup"><span data-stu-id="37611-114">How tooinstall Git and Node.js.</span></span>
  * <span data-ttu-id="37611-115">[Git](https://git-scm.com) 是一個開放原始碼分散式版本控制系統。</span><span class="sxs-lookup"><span data-stu-id="37611-115">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="37611-116">這個發行項的 hello 範例應用程式會儲存在 Git。</span><span class="sxs-lookup"><span data-stu-id="37611-116">hello sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="37611-117">[Node.js](https://nodejs.org/en/) 是一個具有豐富套件生態系統的 JavaScript 執行階段。</span><span class="sxs-lookup"><span data-stu-id="37611-117">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="37611-118">如何 toouse NPM tooinstall 其他 Node.js 開發工具。</span><span class="sxs-lookup"><span data-stu-id="37611-118">How toouse NPM tooinstall additional Node.js development tools.</span></span>
  * <span data-ttu-id="37611-119">Node.js hello 最低版本需求是 4.5 LTS。</span><span class="sxs-lookup"><span data-stu-id="37611-119">hello minimum version requirement of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="37611-120">[NPM](https://www.npmjs.com)是其中一個 hello for Node.js 的封裝管理員。</span><span class="sxs-lookup"><span data-stu-id="37611-120">[NPM](https://www.npmjs.com) is one of hello package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="37611-121">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="37611-121">What you need</span></span>

<span data-ttu-id="37611-122">toocomplete 這項作業，您將需要：</span><span class="sxs-lookup"><span data-stu-id="37611-122">toocomplete this operation, you will need:</span></span>

* <span data-ttu-id="37611-123">網際網路連線 toodownload hello 開發工具和 hello 軟體。</span><span class="sxs-lookup"><span data-stu-id="37611-123">An Internet connection toodownload hello development tools and hello software.</span></span>
* <span data-ttu-id="37611-124">一部執行 Windows 的電腦。</span><span class="sxs-lookup"><span data-stu-id="37611-124">A computer that is running Windows.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="37611-125">安裝 Git 和 Node.js</span><span class="sxs-lookup"><span data-stu-id="37611-125">Install Git and Node.js</span></span>

<span data-ttu-id="37611-126">按一下下方 toodownload hello 連結，並安裝 Git 和適用於 Windows 的 Node.js LTS。</span><span class="sxs-lookup"><span data-stu-id="37611-126">Click hello links below toodownload and install Git and Node.js LTS for Windows.</span></span>

* [<span data-ttu-id="37611-127">取得 Git for Windows</span><span class="sxs-lookup"><span data-stu-id="37611-127">Get Git for Windows</span></span>](https://git-scm.com/download/win/)
* [<span data-ttu-id="37611-128">取得適用於 Windows 的 Node.js LTS</span><span class="sxs-lookup"><span data-stu-id="37611-128">Get Node.js LTS for Windows</span></span>](https://nodejs.org/en/)

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="37611-129">安裝額外的 Node.js 開發工具</span><span class="sxs-lookup"><span data-stu-id="37611-129">Install additional Node.js development tools</span></span>

<span data-ttu-id="37611-130">使用[cwd](http://gulpjs.com) hello 範例應用程式 tooEdison tooautomate hello 部署。</span><span class="sxs-lookup"><span data-stu-id="37611-130">Use [gulp.js](http://gulpjs.com) tooautomate hello deployment of hello sample application tooEdison.</span></span>

<span data-ttu-id="37611-131">以系統管理員身分開啟命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="37611-131">Start a command prompt as an administrator.</span></span> <span data-ttu-id="37611-132">安裝`gulp`藉由執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="37611-132">Install `gulp` by running hello following command:</span></span>

```cmd
npm install -g gulp
```

<span data-ttu-id="37611-133">如果您遇到您的電腦上安裝 Node.js 和下列其他的 Node.js 開發工具的問題，請參閱 hello[疑難排解指南][ troubleshooting]解決方案 toocommon 問題。</span><span class="sxs-lookup"><span data-stu-id="37611-133">If you experience issues installing Node.js and these additional Node.js development tools on your computer, see hello [troubleshooting guide][troubleshooting] for solutions toocommon problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="37611-134">安裝 Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="37611-134">Install Visual Studio Code</span></span>

<span data-ttu-id="37611-135">[下載](https://code.visualstudio.com/docs/setup/windows)並安裝 Visual Studio Code。</span><span class="sxs-lookup"><span data-stu-id="37611-135">[Download](https://code.visualstudio.com/docs/setup/windows) and install Visual Studio Code.</span></span> <span data-ttu-id="37611-136">Visual Studio Code 是一個輕量且強大的原始程式碼編輯器，適用於 Windows、Linux 及 macOS。</span><span class="sxs-lookup"><span data-stu-id="37611-136">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="37611-137">您可以使用此編輯器 hello 教學課程 tooedit hello 範例程式碼中的更新版本。</span><span class="sxs-lookup"><span data-stu-id="37611-137">You use this editor later in hello tutorial tooedit hello sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="37611-138">摘要</span><span class="sxs-lookup"><span data-stu-id="37611-138">Summary</span></span>

<span data-ttu-id="37611-139">您已安裝所需的 hello 開發工具及軟體 hello 第一個範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="37611-139">You've installed hello required development tools and software for hello first sample application.</span></span> <span data-ttu-id="37611-140">hello 下一個工作是 toocreate、 部署和執行上 Edison hello 範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="37611-140">hello next task is toocreate, deploy, and run hello sample application on Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="37611-141">後續步驟</span><span class="sxs-lookup"><span data-stu-id="37611-141">Next steps</span></span>

<span data-ttu-id="37611-142">[建立及部署 hello 閃爍應用程式][create-and-deploy-the-blink-application]</span><span class="sxs-lookup"><span data-stu-id="37611-142">[Create and deploy hello blink application][create-and-deploy-the-blink-application]</span></span>

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[create-and-deploy-the-blink-application]: iot-hub-intel-edison-kit-c-lesson1-deploy-blink-app.md
[windows]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-mac.md
