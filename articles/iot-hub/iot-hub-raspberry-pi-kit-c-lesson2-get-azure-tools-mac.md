---
title: "將 Raspberry Pi (C) 連接到 Azure IoT - 第 2 課：Azure 工具 (macOS) | Microsoft Docs"
description: "在 macOS 上安裝 Python 與 Azure 命令列介面 (Azure CLI)。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "iot 雲端服務, azure cli"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: f2d7d584-7734-401c-976c-81788a7282a3
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 3810990f4a27270fa45709f4d9dbb36a8f4369a8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-azure-tools-macos-1010"></a><span data-ttu-id="d3170-104">取得 Azure 工具 (macOS 10.10)</span><span class="sxs-lookup"><span data-stu-id="d3170-104">Get Azure tools (macOS 10.10)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d3170-105">Windows 7 和更新版本</span><span class="sxs-lookup"><span data-stu-id="d3170-105">Windows 7 and later</span></span>](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-win32.md)
> * [<span data-ttu-id="d3170-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="d3170-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-ubuntu.md)
> * [<span data-ttu-id="d3170-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="d3170-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="d3170-108">將執行的作業</span><span class="sxs-lookup"><span data-stu-id="d3170-108">What you will do</span></span>
<span data-ttu-id="d3170-109">安裝 Azure 命令列介面 (Azure CLI)。</span><span class="sxs-lookup"><span data-stu-id="d3170-109">Install the Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="d3170-110">如果您有任何問題，請在[疑難排解頁面](iot-hub-raspberry-pi-kit-c-troubleshooting.md)尋求解決方案。</span><span class="sxs-lookup"><span data-stu-id="d3170-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="d3170-111">學習目標</span><span class="sxs-lookup"><span data-stu-id="d3170-111">What you will learn</span></span>
<span data-ttu-id="d3170-112">在本文中，您將了解：</span><span class="sxs-lookup"><span data-stu-id="d3170-112">In this article, you will learn:</span></span>
* <span data-ttu-id="d3170-113">如何安裝 Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="d3170-113">How to install Azure CLI.</span></span>
* <span data-ttu-id="d3170-114">如何新增 Azure CLI 的 IoT 子群組。</span><span class="sxs-lookup"><span data-stu-id="d3170-114">How to add an IoT subgroup of the Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="d3170-115">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="d3170-115">What you need</span></span>
* <span data-ttu-id="d3170-116">有網際網路連線的 Mac。</span><span class="sxs-lookup"><span data-stu-id="d3170-116">A Mac with an Internet connection.</span></span>
* <span data-ttu-id="d3170-117">有效的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="d3170-117">An active Azure subscription.</span></span> <span data-ttu-id="d3170-118">如果您沒有 Azure 帳戶，只需要幾分鐘的時間就可以建立[免費的 Azure 試用帳戶](http://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="d3170-118">If you don't have an Azure account, you can create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-python"></a><span data-ttu-id="d3170-119">安裝 Python</span><span class="sxs-lookup"><span data-stu-id="d3170-119">Install Python</span></span>
<span data-ttu-id="d3170-120">雖然 macOS 有現成的 Python 2.7，但建議您透過 Homebrew 安裝 Python。</span><span class="sxs-lookup"><span data-stu-id="d3170-120">Although macOS comes with Python 2.7 out of the box, we recommend that you install Python through Homebrew.</span></span> <span data-ttu-id="d3170-121">請參閱 [Installing Python on macOS](http://docs.python-guide.org/en/latest/starting/install/osx/) (在 macOS 上安裝 Python)。</span><span class="sxs-lookup"><span data-stu-id="d3170-121">See [Installing Python on macOS](http://docs.python-guide.org/en/latest/starting/install/osx/).</span></span>

<span data-ttu-id="d3170-122">執行下列命令安裝 Python 與 pip：</span><span class="sxs-lookup"><span data-stu-id="d3170-122">Install Python and pip by running the following command:</span></span>

```bash
brew install python
```

## <a name="install-the-azure-cli"></a><span data-ttu-id="d3170-123">安裝 Azure CLI</span><span class="sxs-lookup"><span data-stu-id="d3170-123">Install the Azure CLI</span></span>
<span data-ttu-id="d3170-124">Azure CLI 提供適用於 Azure 的多平台命令列體驗。</span><span class="sxs-lookup"><span data-stu-id="d3170-124">The Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="d3170-125">您可直接從命令列工作以佈建和管理資源。</span><span class="sxs-lookup"><span data-stu-id="d3170-125">You work directly from your command line to provision and manage resources.</span></span> 

<span data-ttu-id="d3170-126">若要安裝最新的 Azure CLI，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="d3170-126">To install the latest Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="d3170-127">在終端機視窗中執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="d3170-127">Run the following commands in a terminal window.</span></span> <span data-ttu-id="d3170-128">安裝 Azure CLI 可能需要五分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="d3170-128">It might take five minutes to install the Azure CLI.</span></span>

   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
2. <span data-ttu-id="d3170-129">執行下列命令以驗證安裝：</span><span class="sxs-lookup"><span data-stu-id="d3170-129">Verify the installation by running the following command:</span></span>

   ```bash
   az iot -h
   ```

<span data-ttu-id="d3170-130">如果已成功安裝，您應該會看見下列輸出。</span><span class="sxs-lookup"><span data-stu-id="d3170-130">You should see the following output if the installation is successful.</span></span>

![表示成功的輸出](media/iot-hub-raspberry-pi-lessons/lesson2/az_iot_help_osx.png)

## <a name="summary"></a><span data-ttu-id="d3170-132">摘要</span><span class="sxs-lookup"><span data-stu-id="d3170-132">Summary</span></span>
<span data-ttu-id="d3170-133">您已安裝 Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="d3170-133">You've installed the Azure CLI.</span></span> <span data-ttu-id="d3170-134">下一個工作是使用 Azure CLI 建立 Azure IoT 中樞和裝置身分識別。</span><span class="sxs-lookup"><span data-stu-id="d3170-134">Your next task is to create your Azure IoT hub and device identity by using the Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d3170-135">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d3170-135">Next steps</span></span>
[<span data-ttu-id="d3170-136">建立 IoT 中樞並登錄 Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="d3170-136">Create your IoT hub and register Raspberry Pi 3</span></span>](iot-hub-raspberry-pi-kit-c-lesson2-prepare-azure-iot-hub.md)

