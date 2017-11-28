---
title: "將 Intel Edison (節點) 連接到 Azure IoT - 第 1 課：取得工具 (Windows) | Microsoft Docs"
description: "在 Windows 7 和更新版本上，針對 Edison 的第一個範例應用程式下載並安裝必要的工具和軟體。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "arduino 開發工具, iot 開發, iot 軟體, 物聯網軟體, 在 windows 上安裝 git, 在 windows 上安裝 node js"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: 4164b5a1-5a42-4d8a-9ff6-441e79fcc936
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 35b7ae24f8616848eaa6affccb96630603b823b1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-windows-7-or-later"></a><span data-ttu-id="9d901-104">取得工具 (Windows 7 或更新版本)</span><span class="sxs-lookup"><span data-stu-id="9d901-104">Get the tools (Windows 7 or later)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="9d901-105">[Windows 7 或更新版本][windows]</span><span class="sxs-lookup"><span data-stu-id="9d901-105">[Windows 7 or later][windows]</span></span>
> * <span data-ttu-id="9d901-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="9d901-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="9d901-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="9d901-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="9d901-108">將執行的作業</span><span class="sxs-lookup"><span data-stu-id="9d901-108">What you will do</span></span>
<span data-ttu-id="9d901-109">下載 Intel Edison 第一個範例應用程式的開發工具和軟體。</span><span class="sxs-lookup"><span data-stu-id="9d901-109">Download the development tools and the software for the first sample application for Intel Edison.</span></span> <span data-ttu-id="9d901-110">如果您有任何問題，請在[疑難排解頁面][troubleshooting]尋求解決方案。</span><span class="sxs-lookup"><span data-stu-id="9d901-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="9d901-111">學習目標</span><span class="sxs-lookup"><span data-stu-id="9d901-111">What you will learn</span></span>
<span data-ttu-id="9d901-112">在本文中，您將了解：</span><span class="sxs-lookup"><span data-stu-id="9d901-112">In this article, you will learn:</span></span>

* <span data-ttu-id="9d901-113">如何安裝 Git 和 Node.js。</span><span class="sxs-lookup"><span data-stu-id="9d901-113">How to install Git and Node.js.</span></span>
  * <span data-ttu-id="9d901-114">[Git](https://git-scm.com) 是一個開放原始碼分散式版本控制系統。</span><span class="sxs-lookup"><span data-stu-id="9d901-114">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="9d901-115">本文的範例應用程式將會儲存在 Git 上。</span><span class="sxs-lookup"><span data-stu-id="9d901-115">The sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="9d901-116">[Node.js](https://nodejs.org/en/) 是一個具有豐富套件生態系統的 JavaScript 執行階段。</span><span class="sxs-lookup"><span data-stu-id="9d901-116">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="9d901-117">如何使用 NPM 安裝額外的 Node.js 開發工具。</span><span class="sxs-lookup"><span data-stu-id="9d901-117">How to use NPM to install additional Node.js development tools.</span></span>
  * <span data-ttu-id="9d901-118">Node.js 的最低版本需求為 4.5 LTS。</span><span class="sxs-lookup"><span data-stu-id="9d901-118">The minimum version requirement of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="9d901-119">[NPM](https://www.npmjs.com) 是 Node.js 的其中一個套件管理員。</span><span class="sxs-lookup"><span data-stu-id="9d901-119">[NPM](https://www.npmjs.com) is one of the package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="9d901-120">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="9d901-120">What you need</span></span>

<span data-ttu-id="9d901-121">若要完成此作業，您需要：</span><span class="sxs-lookup"><span data-stu-id="9d901-121">To complete this operation, you will need:</span></span>

* <span data-ttu-id="9d901-122">網際網路連線以下載開發工具和軟體。</span><span class="sxs-lookup"><span data-stu-id="9d901-122">An Internet connection to download the development tools and the software.</span></span>
* <span data-ttu-id="9d901-123">一部執行 Windows 的電腦。</span><span class="sxs-lookup"><span data-stu-id="9d901-123">A computer that is running Windows.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="9d901-124">安裝 Git 和 Node.js</span><span class="sxs-lookup"><span data-stu-id="9d901-124">Install Git and Node.js</span></span>

<span data-ttu-id="9d901-125">按一下下列連結以下載並安裝 Git for Windows 和適用於 Windows 的 Node.js LTS。</span><span class="sxs-lookup"><span data-stu-id="9d901-125">Click the links below to download and install Git and Node.js LTS for Windows.</span></span>

* [<span data-ttu-id="9d901-126">取得 Git for Windows</span><span class="sxs-lookup"><span data-stu-id="9d901-126">Get Git for Windows</span></span>](https://git-scm.com/download/win/)
* [<span data-ttu-id="9d901-127">取得適用於 Windows 的 Node.js LTS</span><span class="sxs-lookup"><span data-stu-id="9d901-127">Get Node.js LTS for Windows</span></span>](https://nodejs.org/en/)

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="9d901-128">安裝額外的 Node.js 開發工具</span><span class="sxs-lookup"><span data-stu-id="9d901-128">Install additional Node.js development tools</span></span>

<span data-ttu-id="9d901-129">使用 [gulp.js](http://gulpjs.com) 對 Edison 自動部署範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="9d901-129">Use [gulp.js](http://gulpjs.com) to automate the deployment of the sample application to Edison.</span></span>

<span data-ttu-id="9d901-130">以系統管理員身分開啟命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="9d901-130">Start a command prompt as an administrator.</span></span> <span data-ttu-id="9d901-131">執行下列命令以安裝 `gulp`：</span><span class="sxs-lookup"><span data-stu-id="9d901-131">Install `gulp` by running the following command:</span></span>

```cmd
npm install -g gulp
```

<span data-ttu-id="9d901-132">如果您於電腦上安裝 Node.js 和這些額外的 Node.js 開發工具時遇到問題，請參閱[疑難排解指南][troubleshooting]以取得常見問題的解決方案。</span><span class="sxs-lookup"><span data-stu-id="9d901-132">If you experience issues installing Node.js and these additional Node.js development tools on your computer, see the [troubleshooting guide][troubleshooting] for solutions to common problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="9d901-133">安裝 Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="9d901-133">Install Visual Studio Code</span></span>

<span data-ttu-id="9d901-134">[下載](https://code.visualstudio.com/docs/setup/windows)並安裝 Visual Studio Code。</span><span class="sxs-lookup"><span data-stu-id="9d901-134">[Download](https://code.visualstudio.com/docs/setup/windows) and install Visual Studio Code.</span></span> <span data-ttu-id="9d901-135">Visual Studio Code 是一個輕量且強大的原始程式碼編輯器，適用於 Windows、Linux 及 macOS。</span><span class="sxs-lookup"><span data-stu-id="9d901-135">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="9d901-136">您可以稍後於教學課程中使用此編輯器來編輯範例程式碼。</span><span class="sxs-lookup"><span data-stu-id="9d901-136">You use this editor later in the tutorial to edit the sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="9d901-137">摘要</span><span class="sxs-lookup"><span data-stu-id="9d901-137">Summary</span></span>

<span data-ttu-id="9d901-138">您已安裝第一個範例應用程式所需的開發工具和軟體。</span><span class="sxs-lookup"><span data-stu-id="9d901-138">You've installed the required development tools and software for the first sample application.</span></span> <span data-ttu-id="9d901-139">下一個工作是在 Edison 上建立、部署和執行範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="9d901-139">The next task is to create, deploy, and run the sample application on Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9d901-140">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9d901-140">Next steps</span></span>

<span data-ttu-id="9d901-141">[1.3 建立並部署閃爍應用程式][create-and-deploy-the-blink-application]</span><span class="sxs-lookup"><span data-stu-id="9d901-141">[Create and deploy the blink application][create-and-deploy-the-blink-application]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[create-and-deploy-the-blink-application]: iot-hub-intel-edison-kit-node-lesson1-deploy-blink-app.md
[windows]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-mac.md
