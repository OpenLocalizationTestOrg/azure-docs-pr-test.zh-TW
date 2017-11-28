---
title: "連接覆盆子 Pi （節點） tooAzure IoT-第 2 課： 取得 tools (Windows) |Microsoft 文件"
description: "在 Windows 7 和更新版本安裝 Python 和 hello Azure 命令列介面 (Azure CLI)。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "iot 雲端服務, azure cli"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: acfa13e3-6d2c-4e68-9a77-1cbc2cf3f9c1
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 25b50214322137ea32861fd1131c474e2fc7ebb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-azure-tools-windows-7-and-later"></a><span data-ttu-id="05f6f-104">取得 Azure 工具 (Windows 7 和更新版本)</span><span class="sxs-lookup"><span data-stu-id="05f6f-104">Get Azure tools (Windows 7 and later)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="05f6f-105">Windows 7 和更新版本</span><span class="sxs-lookup"><span data-stu-id="05f6f-105">Windows 7 and later</span></span>](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-win32.md)
> * [<span data-ttu-id="05f6f-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="05f6f-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-ubuntu.md)
> * [<span data-ttu-id="05f6f-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="05f6f-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="05f6f-108">將執行的作業</span><span class="sxs-lookup"><span data-stu-id="05f6f-108">What you will do</span></span>
<span data-ttu-id="05f6f-109">安裝 Python 和 hello Azure 命令列介面 (Azure CLI)。</span><span class="sxs-lookup"><span data-stu-id="05f6f-109">Install Python and hello Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="05f6f-110">如果您有任何問題，尋找解決方案上 hello[疑難排解頁面](iot-hub-raspberry-pi-kit-node-troubleshooting.md)。</span><span class="sxs-lookup"><span data-stu-id="05f6f-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="05f6f-111">學習目標</span><span class="sxs-lookup"><span data-stu-id="05f6f-111">What you will learn</span></span>
<span data-ttu-id="05f6f-112">在本文中，您將了解：</span><span class="sxs-lookup"><span data-stu-id="05f6f-112">In this article, you will learn:</span></span>
* <span data-ttu-id="05f6f-113">如何 tooinstall Python。</span><span class="sxs-lookup"><span data-stu-id="05f6f-113">How tooinstall Python.</span></span>
* <span data-ttu-id="05f6f-114">如何 tooinstall hello Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="05f6f-114">How tooinstall hello Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="05f6f-115">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="05f6f-115">What you need</span></span>
* <span data-ttu-id="05f6f-116">一部具有網際網路連線的 Windows 電腦。</span><span class="sxs-lookup"><span data-stu-id="05f6f-116">A Windows computer with an Internet connection.</span></span>
* <span data-ttu-id="05f6f-117">有效的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="05f6f-117">An active Azure subscription.</span></span> <span data-ttu-id="05f6f-118">如果您沒有 Azure 帳戶，請花幾分鐘的時間建立[免費的 Azure 試用帳戶](http://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="05f6f-118">If you don't have an Azure account, create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-python"></a><span data-ttu-id="05f6f-119">安裝 Python</span><span class="sxs-lookup"><span data-stu-id="05f6f-119">Install Python</span></span>
<span data-ttu-id="05f6f-120">在 Windows 電腦上[安裝 Python](https://www.python.org/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="05f6f-120">[Install Python](https://www.python.org/downloads/) on your Windows computer.</span></span> <span data-ttu-id="05f6f-121">您可以安裝 Python 2.7、3.4 或 3.5。</span><span class="sxs-lookup"><span data-stu-id="05f6f-121">You can install Python 2.7, 3.4 or 3.5.</span></span> <span data-ttu-id="05f6f-122">本教學課程是以 Python 2.7 為依據。</span><span class="sxs-lookup"><span data-stu-id="05f6f-122">This tutorial is based on Python 2.7.</span></span> <span data-ttu-id="05f6f-123">如果您已經安裝 Python，移 toohello 下一節，並安裝 hello Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="05f6f-123">If you've already installed Python, go toohello next section and install hello Azure CLI.</span></span>

<span data-ttu-id="05f6f-124">您也需要 hello 資料夾其中 python.exe 和 pip.exe 是 已安裝的 toohello 系統 tooadd hello 路徑`PATH`環境變數。</span><span class="sxs-lookup"><span data-stu-id="05f6f-124">You also need tooadd hello path of hello folders where python.exe and pip.exe are installed toohello system `PATH` environment variable.</span></span> <span data-ttu-id="05f6f-125">根據預設，python.exe 是安裝在 `C:\Python27`，而 pip.exe 是安裝在 `C:\Python27\Scripts`。</span><span class="sxs-lookup"><span data-stu-id="05f6f-125">By default, python.exe is installed in `C:\Python27` and pip.exe is installed in `C:\Python27\Scripts`.</span></span>

## <a name="install-hello-azure-cli"></a><span data-ttu-id="05f6f-126">安裝 hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="05f6f-126">Install hello Azure CLI</span></span>
<span data-ttu-id="05f6f-127">hello Azure CLI 提供 Azure 的多平台命令列體驗。</span><span class="sxs-lookup"><span data-stu-id="05f6f-127">hello Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="05f6f-128">您可以直接從您的命令列 tooprovision 工作和管理資源。</span><span class="sxs-lookup"><span data-stu-id="05f6f-128">You work directly from your command-line tooprovision and manage resources.</span></span>

<span data-ttu-id="05f6f-129">tooinstall hello Azure CLI，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="05f6f-129">tooinstall hello Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="05f6f-130">以系統管理員身分開啟 [命令提示字元] 視窗。</span><span class="sxs-lookup"><span data-stu-id="05f6f-130">Open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="05f6f-131">執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="05f6f-131">Run hello following commands:</span></span>

   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
3. <span data-ttu-id="05f6f-132">執行下列命令的 hello 驗證 hello 安裝：</span><span class="sxs-lookup"><span data-stu-id="05f6f-132">Verify hello installation by running hello following command:</span></span>

   ```bash
   az iot -h
   ```

<span data-ttu-id="05f6f-133">您會看到下列 hello 輸出 hello 安裝是否成功。</span><span class="sxs-lookup"><span data-stu-id="05f6f-133">You see hello following output if hello installation is successful.</span></span>

![表示成功的輸出](media/iot-hub-raspberry-pi-lessons/lesson2/az_iot_help_win.png)

## <a name="summary"></a><span data-ttu-id="05f6f-135">摘要</span><span class="sxs-lookup"><span data-stu-id="05f6f-135">Summary</span></span>
<span data-ttu-id="05f6f-136">您已安裝 hello Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="05f6f-136">You've installed hello Azure CLI.</span></span> <span data-ttu-id="05f6f-137">您的下一步 工作使用 hello Azure CLI toocreate 您的 Azure IoT 中樞和裝置身分識別。</span><span class="sxs-lookup"><span data-stu-id="05f6f-137">Your next task toocreate your Azure IoT hub and device identity by using hello Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="05f6f-138">後續步驟</span><span class="sxs-lookup"><span data-stu-id="05f6f-138">Next steps</span></span>
[<span data-ttu-id="05f6f-139">建立 IoT 中樞並登錄 Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="05f6f-139">Create your IoT hub and register Raspberry Pi 3</span></span>](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md)

