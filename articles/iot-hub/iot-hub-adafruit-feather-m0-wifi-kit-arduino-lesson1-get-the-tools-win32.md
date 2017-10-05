---
title: "將 Arduino 連接到 Azure IoT - 第 1 課：取得工具 (Windows) | Microsoft Docs"
description: "在 Windows 7 和更新版本上，針對 Adafruit Feather M0 WiFi 的第一個範例應用程式下載並安裝必要的工具和軟體。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "arduino 開發工具, iot 開發, iot 軟體, 物聯網軟體, 在 windows 上安裝 git, 在 windows 上安裝 node js"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 9cfb8cd2-eafb-4ba2-b23e-d94e114ff3a6
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 5d27c016c4a74e31455e676b3c3070a8e262b21f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-windows-7-or-later"></a><span data-ttu-id="3192d-104">取得工具 (Windows 7 或更新版本)</span><span class="sxs-lookup"><span data-stu-id="3192d-104">Get the tools (Windows 7 or later)</span></span>

> [!div class="op_single_selector"]
> * <span data-ttu-id="3192d-105">[Windows 7 或更新版本][windows]</span><span class="sxs-lookup"><span data-stu-id="3192d-105">[Windows 7 or later][windows]</span></span>
> * <span data-ttu-id="3192d-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="3192d-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="3192d-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="3192d-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="3192d-108">將執行的作業</span><span class="sxs-lookup"><span data-stu-id="3192d-108">What you will do</span></span>

<span data-ttu-id="3192d-109">下載您 Adafruit Feather M0 WiFi Arduino 面板第一個範例應用程式的開發工具和軟體。</span><span class="sxs-lookup"><span data-stu-id="3192d-109">Download the development tools and the software for the first sample application for your Adafruit Feather M0 WiFi Arduino board.</span></span>

<span data-ttu-id="3192d-110">如果您有任何問題，請在[疑難排解頁面][troubleshooting]尋求解決方案。</span><span class="sxs-lookup"><span data-stu-id="3192d-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

> [!NOTE]
> <span data-ttu-id="3192d-111">雖然主要邏輯的程式語言是 Arduino，但這些課程中會使用 Node.js 工具來建置和部署範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="3192d-111">Although the programming language of the main logic is Arduino, Node.js tools are used in the lessons to build and deploy sample applications.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="3192d-112">學習目標</span><span class="sxs-lookup"><span data-stu-id="3192d-112">What you will learn</span></span>
<span data-ttu-id="3192d-113">在本文中，您將了解：</span><span class="sxs-lookup"><span data-stu-id="3192d-113">In this article, you will learn:</span></span>

* <span data-ttu-id="3192d-114">如何安裝 Git 和 Node.js。</span><span class="sxs-lookup"><span data-stu-id="3192d-114">How to install Git and Node.js.</span></span>
  * <span data-ttu-id="3192d-115">[Git](https://git-scm.com) 是一個開放原始碼分散式版本控制系統。</span><span class="sxs-lookup"><span data-stu-id="3192d-115">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="3192d-116">本文的範例應用程式將會儲存在 Git 上。</span><span class="sxs-lookup"><span data-stu-id="3192d-116">The sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="3192d-117">[Node.js](https://nodejs.org/en/) 是一個具有豐富套件生態系統的 JavaScript 執行階段。</span><span class="sxs-lookup"><span data-stu-id="3192d-117">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="3192d-118">如何使用 NPM 安裝額外的 Node.js 開發工具。</span><span class="sxs-lookup"><span data-stu-id="3192d-118">How to use NPM to install additional Node.js development tools.</span></span>
  * <span data-ttu-id="3192d-119">Node.js 的最低版本需求為 4.5 LTS。</span><span class="sxs-lookup"><span data-stu-id="3192d-119">The minimum version requirement of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="3192d-120">[NPM](https://www.npmjs.com) 是 Node.js 的其中一個套件管理員。</span><span class="sxs-lookup"><span data-stu-id="3192d-120">[NPM](https://www.npmjs.com) is one of the package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="3192d-121">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="3192d-121">What you need</span></span>

<span data-ttu-id="3192d-122">若要完成此作業，您需要：</span><span class="sxs-lookup"><span data-stu-id="3192d-122">To complete this operation, you will need:</span></span>

* <span data-ttu-id="3192d-123">網際網路連線以下載開發工具和軟體。</span><span class="sxs-lookup"><span data-stu-id="3192d-123">An Internet connection to download the development tools and the software.</span></span>
* <span data-ttu-id="3192d-124">一部執行 Windows 的電腦。</span><span class="sxs-lookup"><span data-stu-id="3192d-124">A computer that is running Windows.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="3192d-125">安裝 Git 和 Node.js</span><span class="sxs-lookup"><span data-stu-id="3192d-125">Install Git and Node.js</span></span>

<span data-ttu-id="3192d-126">按一下下列連結以下載並安裝 Git for Windows 和適用於 Windows 的 Node.js LTS。</span><span class="sxs-lookup"><span data-stu-id="3192d-126">Click the links below to download and install Git and Node.js LTS for Windows.</span></span>

* [<span data-ttu-id="3192d-127">取得 Git for Windows</span><span class="sxs-lookup"><span data-stu-id="3192d-127">Get Git for Windows</span></span>](https://git-scm.com/download/win/)
* [<span data-ttu-id="3192d-128">取得適用於 Windows 的 Node.js LTS</span><span class="sxs-lookup"><span data-stu-id="3192d-128">Get Node.js LTS for Windows</span></span>](https://nodejs.org/en/)

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="3192d-129">安裝額外的 Node.js 開發工具</span><span class="sxs-lookup"><span data-stu-id="3192d-129">Install additional Node.js development tools</span></span>

<span data-ttu-id="3192d-130">使用 [gulp.js](http://gulpjs.com) 自動將範例應用程式部署至 Arduino 面板。</span><span class="sxs-lookup"><span data-stu-id="3192d-130">Use [gulp.js](http://gulpjs.com) to automate the deployment of the sample application to your Arduino board.</span></span>

<span data-ttu-id="3192d-131">以系統管理員身分開啟命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="3192d-131">Start a command prompt as an administrator.</span></span> <span data-ttu-id="3192d-132">在終端機中執行下列命令以安裝 `gulp`、`device-discovery-cli`：</span><span class="sxs-lookup"><span data-stu-id="3192d-132">Install `gulp`, `device-discovery-cli` by running the following command in the terminal:</span></span>

```bash
npm install -g gulp device-discovery-cli
```

<span data-ttu-id="3192d-133">如果您於電腦上安裝 Node.js 和這些額外的 Node.js 開發工具時遇到問題，請參閱[疑難排解指南][troubleshooting]以取得常見問題的解決方案。</span><span class="sxs-lookup"><span data-stu-id="3192d-133">If you experience issues installing Node.js and these additional Node.js development tools on your computer, see the [troubleshooting guide][troubleshooting] for solutions to common problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="3192d-134">安裝 Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="3192d-134">Install Visual Studio Code</span></span>

<span data-ttu-id="3192d-135">[下載](https://code.visualstudio.com/docs/setup/windows)並安裝 Visual Studio Code。</span><span class="sxs-lookup"><span data-stu-id="3192d-135">[Download](https://code.visualstudio.com/docs/setup/windows) and install Visual Studio Code.</span></span> <span data-ttu-id="3192d-136">Visual Studio Code 是一個輕量且強大的原始程式碼編輯器，適用於 Windows、Linux 及 macOS。</span><span class="sxs-lookup"><span data-stu-id="3192d-136">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="3192d-137">您可以稍後於教學課程中使用此編輯器來編輯範例程式碼。</span><span class="sxs-lookup"><span data-stu-id="3192d-137">You use this editor later in the tutorial to edit the sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="3192d-138">摘要</span><span class="sxs-lookup"><span data-stu-id="3192d-138">Summary</span></span>

<span data-ttu-id="3192d-139">您已安裝第一個範例應用程式所需的開發工具和軟體。</span><span class="sxs-lookup"><span data-stu-id="3192d-139">You've installed the required development tools and software for the first sample application.</span></span> <span data-ttu-id="3192d-140">下一個工作是在 Arduino 面板上建立、部署和執行範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="3192d-140">The next task is to create, deploy, and run the sample application on your Arduino board.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3192d-141">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3192d-141">Next steps</span></span>

<span data-ttu-id="3192d-142">[建立並部署閃爍範例應用程式][create-and-deploy-the-blink-sample-application]</span><span class="sxs-lookup"><span data-stu-id="3192d-142">[Create and deploy the blink sample application][create-and-deploy-the-blink-sample-application]</span></span>
<!-- Images and links -->

[windows]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-mac.md
[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[create-and-deploy-the-blink-sample-application]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-deploy-blink-app.md