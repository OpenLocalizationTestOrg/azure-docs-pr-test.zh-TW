---
title: "Connect Raspberry Pi (C) tooAzure IoT-第 1 課： 取得工具 (Ubuntu) |Microsoft 文件"
description: "下載並安裝 hello 必要工具及軟體 hello 第一個範例應用程式 Pi Ubuntu 上。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "iot 開發, iot 軟體, 物聯網軟體, 在 ubuntu 上安裝 git, gulp 執行, 安裝 node js ubuntu"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: 32cfea00-c254-4cef-8f6f-bbf807eca6b6
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 794928b5da63521cb0a72cb54256f2ad9724ec84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-ubuntu-1604"></a><span data-ttu-id="aaad8-104">取得 hello 工具 (Ubuntu 16.04)</span><span class="sxs-lookup"><span data-stu-id="aaad8-104">Get hello tools (Ubuntu 16.04)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="aaad8-105">Windows 7 或更新版本</span><span class="sxs-lookup"><span data-stu-id="aaad8-105">Windows 7 or later</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)
> * [<span data-ttu-id="aaad8-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="aaad8-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="aaad8-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="aaad8-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="aaad8-108">將執行的作業</span><span class="sxs-lookup"><span data-stu-id="aaad8-108">What you will do</span></span>
<span data-ttu-id="aaad8-109">下載 hello 開發工具及 hello 第一個範例應用程式程式覆盆子 Pi 3 hello 軟體。</span><span class="sxs-lookup"><span data-stu-id="aaad8-109">Download hello development tools and hello software for hello first sample application for your Raspberry Pi 3.</span></span> <span data-ttu-id="aaad8-110">如果您有任何問題，尋找解決方案上 hello[疑難排解頁面](iot-hub-raspberry-pi-kit-c-troubleshooting.md)。</span><span class="sxs-lookup"><span data-stu-id="aaad8-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

> [!NOTE]
> <span data-ttu-id="aaad8-111">雖然 hello 程式設計語言的 hello 主要邏輯是 C 的 Node.js 工具會用於 hello 課程 toodiscover 裝置，並建置和部署範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="aaad8-111">Although hello programming language of hello main logic is C, Node.js tools are used in hello lessons toodiscover devices, and build and deploy sample applications.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="aaad8-112">學習目標</span><span class="sxs-lookup"><span data-stu-id="aaad8-112">What you will learn</span></span>
<span data-ttu-id="aaad8-113">在本文中，您將了解：</span><span class="sxs-lookup"><span data-stu-id="aaad8-113">In this article, you will learn:</span></span>

* <span data-ttu-id="aaad8-114">如何 tooinstall Git 和 Node.js</span><span class="sxs-lookup"><span data-stu-id="aaad8-114">How tooinstall Git and Node.js</span></span>
  * <span data-ttu-id="aaad8-115">[Git](https://git-scm.com) 是一個開放原始碼分散式版本控制系統。</span><span class="sxs-lookup"><span data-stu-id="aaad8-115">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="aaad8-116">這個發行項的 hello 範例應用程式會儲存在 Git。</span><span class="sxs-lookup"><span data-stu-id="aaad8-116">hello sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="aaad8-117">[Node.js](https://nodejs.org/en/) 是一個具有豐富套件生態系統的 JavaScript 執行階段。</span><span class="sxs-lookup"><span data-stu-id="aaad8-117">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="aaad8-118">如何 toouse NPM tooinstall 其他 Node.js 開發工具。</span><span class="sxs-lookup"><span data-stu-id="aaad8-118">How toouse NPM tooinstall additional Node.js development tools.</span></span>
  * <span data-ttu-id="aaad8-119">hello 的最低必要的版本 Node.js 是 4.5 LTS。</span><span class="sxs-lookup"><span data-stu-id="aaad8-119">hello minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="aaad8-120">[NPM](https://www.npmjs.com)是其中一個 hello for Node.js 的封裝管理員。</span><span class="sxs-lookup"><span data-stu-id="aaad8-120">[NPM](https://www.npmjs.com) is one of hello package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="aaad8-121">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="aaad8-121">What you need</span></span>
<span data-ttu-id="aaad8-122">toocomplete 這項作業，您將需要：</span><span class="sxs-lookup"><span data-stu-id="aaad8-122">toocomplete this operation, you will need:</span></span>

* <span data-ttu-id="aaad8-123">網際網路連線 toodownload hello 開發工具和 hello 軟體。</span><span class="sxs-lookup"><span data-stu-id="aaad8-123">An Internet connection toodownload hello development tools and hello software.</span></span>
* <span data-ttu-id="aaad8-124">一部執行 Ubuntu 16.04 或以上版本的電腦。</span><span class="sxs-lookup"><span data-stu-id="aaad8-124">A computer that is running Ubuntu 16.04 or later.</span></span>

## <a name="install-git-nodejs-and-npm"></a><span data-ttu-id="aaad8-125">安裝 Git、Node.js 及 NPM</span><span class="sxs-lookup"><span data-stu-id="aaad8-125">Install Git, Node.js, and NPM</span></span>
<span data-ttu-id="aaad8-126">使用 hello 鍵盤快速鍵`Ctrl + Alt + T`tooopen 終端機及執行 hello，下列命令：</span><span class="sxs-lookup"><span data-stu-id="aaad8-126">Use hello keyboard shortcut `Ctrl + Alt + T` tooopen a terminal and run hello following commands:</span></span>

```bash
sudo apt-get update
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install -y nodejs
sudo apt-get install git
```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="aaad8-127">安裝額外的 Node.js 開發工具</span><span class="sxs-lookup"><span data-stu-id="aaad8-127">Install additional Node.js development tools</span></span>
<span data-ttu-id="aaad8-128">使用[cwd](http://gulpjs.com) hello 範例應用程式 tooPi tooautomate hello 部署。</span><span class="sxs-lookup"><span data-stu-id="aaad8-128">Use [gulp.js](http://gulpjs.com) tooautomate hello deployment of hello sample application tooPi.</span></span> <span data-ttu-id="aaad8-129">使用 hello[裝置-探索-cli](https://github.com/Azure/device-discovery-cli) tooretrieve IoT 裝置相關的網路資訊。</span><span class="sxs-lookup"><span data-stu-id="aaad8-129">Use hello [device-discovery-cli](https://github.com/Azure/device-discovery-cli) tooretrieve network information about your IoT devices.</span></span>

<span data-ttu-id="aaad8-130">安裝`gulp`和`device-discovery-cli`藉由執行下列命令在 hello 終端機中的 hello:</span><span class="sxs-lookup"><span data-stu-id="aaad8-130">Install `gulp` and `device-discovery-cli` by running hello following command in hello terminal:</span></span>

```bash
sudo npm install -g device-discovery-cli gulp
```

<span data-ttu-id="aaad8-131">如果您遇到安裝 Node.js 和這些額外的開發工具在 Ubuntu 上的問題，請參閱 hello[疑難排解指南](iot-hub-raspberry-pi-kit-c-troubleshooting.md)解決方案 toocommon 問題。</span><span class="sxs-lookup"><span data-stu-id="aaad8-131">If you experience issues installing Node.js and these additional development tools on Ubuntu, see hello [troubleshooting guide](iot-hub-raspberry-pi-kit-c-troubleshooting.md) for solutions toocommon problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="aaad8-132">安裝 Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="aaad8-132">Install Visual Studio Code</span></span>
<span data-ttu-id="aaad8-133">[下載](https://code.visualstudio.com/docs/setup/linux)並安裝 Visual Studio Code。</span><span class="sxs-lookup"><span data-stu-id="aaad8-133">[Download](https://code.visualstudio.com/docs/setup/linux) and install Visual Studio Code.</span></span> <span data-ttu-id="aaad8-134">Visual Studio Code 是一個輕量且強大的原始程式碼編輯器，適用於 Windows、Linux 及 macOS。</span><span class="sxs-lookup"><span data-stu-id="aaad8-134">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="aaad8-135">您可以使用此編輯器 hello 教學課程 tooedit hello 範例程式碼中的更新版本。</span><span class="sxs-lookup"><span data-stu-id="aaad8-135">You use this editor later in hello tutorial tooedit hello sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="aaad8-136">摘要</span><span class="sxs-lookup"><span data-stu-id="aaad8-136">Summary</span></span>
<span data-ttu-id="aaad8-137">您已安裝所需的 hello 開發工具及軟體 hello 第一個範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="aaad8-137">You've installed hello required development tools and software for hello first sample application.</span></span> <span data-ttu-id="aaad8-138">hello 下一個工作是 toocreate、 部署和執行 pi 的 hello 範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="aaad8-138">hello next task is toocreate, deploy, and run hello sample application on Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="aaad8-139">後續步驟</span><span class="sxs-lookup"><span data-stu-id="aaad8-139">Next steps</span></span>
[<span data-ttu-id="aaad8-140">建立及部署 hello 閃爍應用程式</span><span class="sxs-lookup"><span data-stu-id="aaad8-140">Create and deploy hello blink application</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-deploy-blink-app.md)

