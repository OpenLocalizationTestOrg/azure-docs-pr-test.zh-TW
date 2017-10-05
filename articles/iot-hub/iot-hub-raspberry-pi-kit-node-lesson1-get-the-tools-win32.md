---
title: "將 Raspberry Pi (節點) 連接到 Azure IoT - 第 1 課：取得工具 (Windows) | Microsoft Docs"
description: "在 Windows 7 和更新版本上，針對 Pi 的第一個範例應用程式下載並安裝必要的工具和軟體。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "iot 開發, iot 軟體, 物聯網軟體, 在 windows 上安裝 git, gulp , 在 windows 上安裝 node js, 在 windows 上安裝 npm, 在 windows 上安裝 python"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: b3d88e17-97cc-4f23-85fd-a688fc228eb8
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 24c58e006bbef9bbc1fcd626a0f8f6bcac063f05
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-windows-7-or-later"></a><span data-ttu-id="679fe-104">取得工具 (Windows 7 或更新版本)</span><span class="sxs-lookup"><span data-stu-id="679fe-104">Get the tools (Windows 7 or later)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="679fe-105">Windows 7 或更新版本</span><span class="sxs-lookup"><span data-stu-id="679fe-105">Windows 7 or later</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-win32.md)
> * [<span data-ttu-id="679fe-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="679fe-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="679fe-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="679fe-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-mac.md)


## <a name="what-you-will-do"></a><span data-ttu-id="679fe-108">將執行的作業</span><span class="sxs-lookup"><span data-stu-id="679fe-108">What you will do</span></span>
<span data-ttu-id="679fe-109">下載您 Raspberry Pi 3 第一個範例應用程式的開發工具和軟體。</span><span class="sxs-lookup"><span data-stu-id="679fe-109">Download the development tools and the software for the first sample application for Raspberry Pi 3.</span></span> <span data-ttu-id="679fe-110">如果您有任何問題，請在[疑難排解頁面](iot-hub-raspberry-pi-kit-node-troubleshooting.md)尋求解決方案。</span><span class="sxs-lookup"><span data-stu-id="679fe-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="679fe-111">學習目標</span><span class="sxs-lookup"><span data-stu-id="679fe-111">What you will learn</span></span>
<span data-ttu-id="679fe-112">在本文中，您將了解：</span><span class="sxs-lookup"><span data-stu-id="679fe-112">In this article, you will learn:</span></span>

* <span data-ttu-id="679fe-113">如何安裝 Git 和 Node.js。</span><span class="sxs-lookup"><span data-stu-id="679fe-113">How to install Git and Node.js.</span></span>
  * <span data-ttu-id="679fe-114">[Git](https://git-scm.com) 是一個開放原始碼分散式版本控制系統。</span><span class="sxs-lookup"><span data-stu-id="679fe-114">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="679fe-115">本文的範例應用程式將會儲存在 Git 上。</span><span class="sxs-lookup"><span data-stu-id="679fe-115">The sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="679fe-116">[Node.js](https://nodejs.org/en/) 是一個具有豐富套件生態系統的 JavaScript 執行階段。</span><span class="sxs-lookup"><span data-stu-id="679fe-116">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="679fe-117">如何使用 NPM 安裝額外的 Node.js 開發工具。</span><span class="sxs-lookup"><span data-stu-id="679fe-117">How to use NPM to install additional Node.js development tools.</span></span>
  * <span data-ttu-id="679fe-118">Node.js 的最低版本需求為 4.5 LTS。</span><span class="sxs-lookup"><span data-stu-id="679fe-118">The minimum version requirement of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="679fe-119">[NPM](https://www.npmjs.com) 是 Node.js 的其中一個套件管理員。</span><span class="sxs-lookup"><span data-stu-id="679fe-119">[NPM](https://www.npmjs.com) is one of the package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="679fe-120">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="679fe-120">What you need</span></span>
<span data-ttu-id="679fe-121">若要完成此作業，您需要：</span><span class="sxs-lookup"><span data-stu-id="679fe-121">To complete this operation, you will need:</span></span>

* <span data-ttu-id="679fe-122">網際網路連線以下載開發工具和軟體。</span><span class="sxs-lookup"><span data-stu-id="679fe-122">An Internet connection to download the development tools and the software.</span></span>
* <span data-ttu-id="679fe-123">一部執行 Windows 的電腦。</span><span class="sxs-lookup"><span data-stu-id="679fe-123">A computer that is running Windows.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="679fe-124">安裝 Git 和 Node.js</span><span class="sxs-lookup"><span data-stu-id="679fe-124">Install Git and Node.js</span></span>
<span data-ttu-id="679fe-125">按一下下列連結以下載並安裝 Git for Windows 和適用於 Windows 的 Node.js LTS。</span><span class="sxs-lookup"><span data-stu-id="679fe-125">Click the following links to download and install Git and Node.js LTS for Windows.</span></span>

* [<span data-ttu-id="679fe-126">取得 Git for Windows</span><span class="sxs-lookup"><span data-stu-id="679fe-126">Get Git for Windows</span></span>](https://git-scm.com/download/win/)
* [<span data-ttu-id="679fe-127">取得適用於 Windows 的 Node.js LTS</span><span class="sxs-lookup"><span data-stu-id="679fe-127">Get Node.js LTS for Windows</span></span>](https://nodejs.org/en/)

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="679fe-128">安裝額外的 Node.js 開發工具</span><span class="sxs-lookup"><span data-stu-id="679fe-128">Install additional Node.js development tools</span></span>
<span data-ttu-id="679fe-129">使用 [gulp.js](http://gulpjs.com) 對 Pi 自動部署範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="679fe-129">Use [gulp.js](http://gulpjs.com) to automate the deployment of the sample application to Pi.</span></span> <span data-ttu-id="679fe-130">您也會使用 [device-discovery-cli](https://github.com/Azure/device-discovery-cli)來擷取關於您 IoT 裝置的網路資訊。</span><span class="sxs-lookup"><span data-stu-id="679fe-130">You also use the [device-discovery-cli](https://github.com/Azure/device-discovery-cli) to retrieve network information about your IoT devices.</span></span>

<span data-ttu-id="679fe-131">以系統管理員身分開啟命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="679fe-131">Start a command prompt as an administrator.</span></span> <span data-ttu-id="679fe-132">執行下列命令以安裝 `gulp` 和 `device-discovery-cli`：</span><span class="sxs-lookup"><span data-stu-id="679fe-132">Install `gulp` and `device-discovery-cli` by running the following command:</span></span>

```bash
npm install -g device-discovery-cli gulp
```

<span data-ttu-id="679fe-133">如果您於電腦上安裝 Node.js 和這些額外的 Node.js 開發工具時遇到問題，請參閱[疑難排解指南](iot-hub-raspberry-pi-kit-node-troubleshooting.md)以取得常見問題的解決方案。</span><span class="sxs-lookup"><span data-stu-id="679fe-133">If you experience issues installing Node.js and these additional Node.js development tools on your computer, see the [troubleshooting guide](iot-hub-raspberry-pi-kit-node-troubleshooting.md) for solutions to common problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="679fe-134">安裝 Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="679fe-134">Install Visual Studio Code</span></span>
<span data-ttu-id="679fe-135">[下載](https://code.visualstudio.com/docs/setup/windows)並安裝 Visual Studio Code。</span><span class="sxs-lookup"><span data-stu-id="679fe-135">[Download](https://code.visualstudio.com/docs/setup/windows) and install Visual Studio Code.</span></span> <span data-ttu-id="679fe-136">Visual Studio Code 是一個輕量且強大的原始程式碼編輯器，適用於 Windows、Linux 及 macOS。</span><span class="sxs-lookup"><span data-stu-id="679fe-136">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="679fe-137">您可以稍後於教學課程中使用此編輯器來編輯範例程式碼。</span><span class="sxs-lookup"><span data-stu-id="679fe-137">You use this editor later in the tutorial to edit the sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="679fe-138">摘要</span><span class="sxs-lookup"><span data-stu-id="679fe-138">Summary</span></span>
<span data-ttu-id="679fe-139">您已安裝第一個範例應用程式所需的開發工具和軟體。</span><span class="sxs-lookup"><span data-stu-id="679fe-139">You've installed the required development tools and software for the first sample application.</span></span> <span data-ttu-id="679fe-140">下一個工作是在 Pi 上建立、部署和執行範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="679fe-140">The next task is to create, deploy, and run the sample application on Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="679fe-141">後續步驟</span><span class="sxs-lookup"><span data-stu-id="679fe-141">Next steps</span></span>
[<span data-ttu-id="679fe-142">建立並部署閃爍範例應用程式</span><span class="sxs-lookup"><span data-stu-id="679fe-142">Create and deploy the blink sample application</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-deploy-blink-app.md)

