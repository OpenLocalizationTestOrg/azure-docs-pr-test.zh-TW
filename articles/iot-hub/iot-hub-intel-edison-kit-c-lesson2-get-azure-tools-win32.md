---
title: "將 Intel Edison (C) 連接到 Azure IoT - 第 2 課：Azure 工具 (Windows) | Microsoft Docs"
description: "在 Windows 7 和更新版本上安裝 Python 和 Azure 命令列介面 (Azure CLI)。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "azure cli, iot 雲端服務, arduino 雲端"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: 1035760e-cdd1-4d99-8003-067e98b29762
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 90ef113ae84ccc8cb3cbdbe8c245e138320a93c6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-azure-tools-windows-7-and-later"></a><span data-ttu-id="2556d-104">取得 Azure 工具 (Windows 7 和更新版本)</span><span class="sxs-lookup"><span data-stu-id="2556d-104">Get Azure tools (Windows 7 and later)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="2556d-105">[Windows 7 和更新版本][windows]</span><span class="sxs-lookup"><span data-stu-id="2556d-105">[Windows 7 and later][windows]</span></span>
> * <span data-ttu-id="2556d-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="2556d-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="2556d-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="2556d-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="2556d-108">將執行的作業</span><span class="sxs-lookup"><span data-stu-id="2556d-108">What you will do</span></span>
<span data-ttu-id="2556d-109">安裝 Python 和 Azure 命令列介面 (Azure CLI)。</span><span class="sxs-lookup"><span data-stu-id="2556d-109">Install Python and the Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="2556d-110">如果您有任何問題，請在[疑難排解頁面][troubleshooting]尋求解決方案。</span><span class="sxs-lookup"><span data-stu-id="2556d-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="2556d-111">學習目標</span><span class="sxs-lookup"><span data-stu-id="2556d-111">What you will learn</span></span>
<span data-ttu-id="2556d-112">在本文中，您將了解：</span><span class="sxs-lookup"><span data-stu-id="2556d-112">In this article, you will learn:</span></span>
* <span data-ttu-id="2556d-113">如何安裝 Python。</span><span class="sxs-lookup"><span data-stu-id="2556d-113">How to install Python.</span></span>
* <span data-ttu-id="2556d-114">如何安裝 Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="2556d-114">How to install the Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="2556d-115">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="2556d-115">What you need</span></span>
* <span data-ttu-id="2556d-116">一部具有網際網路連線的 Windows 電腦。</span><span class="sxs-lookup"><span data-stu-id="2556d-116">A Windows computer with an Internet connection.</span></span>
* <span data-ttu-id="2556d-117">有效的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="2556d-117">An active Azure subscription.</span></span> <span data-ttu-id="2556d-118">如果您沒有 Azure 帳戶，請花幾分鐘的時間建立[免費的 Azure 試用帳戶](http://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="2556d-118">If you don't have an Azure account, create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-python"></a><span data-ttu-id="2556d-119">安裝 Python</span><span class="sxs-lookup"><span data-stu-id="2556d-119">Install Python</span></span>
<span data-ttu-id="2556d-120">在 Windows 電腦上[安裝 Python](https://www.python.org/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="2556d-120">[Install Python](https://www.python.org/downloads/) on your Windows computer.</span></span> <span data-ttu-id="2556d-121">您可以安裝 Python 2.7、3.4 或 3.5。</span><span class="sxs-lookup"><span data-stu-id="2556d-121">You can install Python 2.7, 3.4 or 3.5.</span></span> <span data-ttu-id="2556d-122">本教學課程是以 Python 2.7 為依據。</span><span class="sxs-lookup"><span data-stu-id="2556d-122">This tutorial is based on Python 2.7.</span></span> <span data-ttu-id="2556d-123">如果您已安裝 Python，請移至下一節，並安裝 Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="2556d-123">If you've already installed Python, go to the next section and install the Azure CLI.</span></span>

<span data-ttu-id="2556d-124">您也必須將安裝 python.exe 和 pip.exe 的資料夾路徑新增到系統 `PATH` 環境變數。</span><span class="sxs-lookup"><span data-stu-id="2556d-124">You also need to add the path of the folders where python.exe and pip.exe are installed to the system `PATH` environment variable.</span></span> <span data-ttu-id="2556d-125">根據預設，python.exe 是安裝在 `C:\Python27`，而 pip.exe 是安裝在 `C:\Python27\Scripts`。</span><span class="sxs-lookup"><span data-stu-id="2556d-125">By default, python.exe is installed in `C:\Python27` and pip.exe is installed in `C:\Python27\Scripts`.</span></span>

## <a name="install-the-azure-cli"></a><span data-ttu-id="2556d-126">安裝 Azure CLI</span><span class="sxs-lookup"><span data-stu-id="2556d-126">Install the Azure CLI</span></span>
<span data-ttu-id="2556d-127">Azure CLI 提供適用於 Azure 的多平台命令列體驗。</span><span class="sxs-lookup"><span data-stu-id="2556d-127">The Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="2556d-128">您可直接從命令列工作以佈建和管理資源。</span><span class="sxs-lookup"><span data-stu-id="2556d-128">You work directly from your command line to provision and manage resources.</span></span>

<span data-ttu-id="2556d-129">若要安裝 Azure CLI，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="2556d-129">To install the Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="2556d-130">以系統管理員身分開啟 [命令提示字元] 視窗。</span><span class="sxs-lookup"><span data-stu-id="2556d-130">Open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="2556d-131">執行以下命令：</span><span class="sxs-lookup"><span data-stu-id="2556d-131">Run the following commands:</span></span>

   ```cmd
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
3. <span data-ttu-id="2556d-132">執行下列命令以驗證安裝：</span><span class="sxs-lookup"><span data-stu-id="2556d-132">Verify the installation by running the following command:</span></span>

   ```cmd
   az iot -h
   ```

<span data-ttu-id="2556d-133">如果已成功安裝，您將會看見下列輸出。</span><span class="sxs-lookup"><span data-stu-id="2556d-133">You see the following output if the installation is successful.</span></span>

![表示成功的輸出](media/iot-hub-intel-edison-lessons/lesson2/az_iot_help_win.png)

## <a name="summary"></a><span data-ttu-id="2556d-135">摘要</span><span class="sxs-lookup"><span data-stu-id="2556d-135">Summary</span></span>
<span data-ttu-id="2556d-136">您已安裝 Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="2556d-136">You've installed the Azure CLI.</span></span> <span data-ttu-id="2556d-137">下一個工作是使用 Azure CLI 建立 Azure IoT 中樞和裝置身分識別。</span><span class="sxs-lookup"><span data-stu-id="2556d-137">Your next task to create your Azure IoT hub and device identity by using the Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2556d-138">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2556d-138">Next steps</span></span>
<span data-ttu-id="2556d-139">[建立 IoT 中樞並登錄 Intel Edison][create-your-iot-hub-and-register-intel-edison]</span><span class="sxs-lookup"><span data-stu-id="2556d-139">[Create your IoT hub and register Intel Edison][create-your-iot-hub-and-register-intel-edison]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[create-your-iot-hub-and-register-intel-edison]: iot-hub-intel-edison-kit-c-lesson2-prepare-azure-iot-hub.md
[windows]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-mac.md
