---
title: "將 Intel Edison (C) 連接到 Azure IoT - 第 2 課：Azure 工具 (macOS) | Microsoft Docs"
description: "在 macOS 上安裝 Python 與 Azure 命令列介面 (Azure CLI)。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "azure cli, iot 雲端服務, arduino 雲端"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: d561680f-69cc-427a-820d-24f710ba05a8
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 97beb04781f3f9809cdafc945d9499e71cbbd9b1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-azure-tools-macos-1010"></a><span data-ttu-id="90c52-104">取得 Azure 工具 (macOS 10.10)</span><span class="sxs-lookup"><span data-stu-id="90c52-104">Get Azure tools (macOS 10.10)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="90c52-105">[Windows 7 和更新版本][windows]</span><span class="sxs-lookup"><span data-stu-id="90c52-105">[Windows 7 and later][windows]</span></span>
> * <span data-ttu-id="90c52-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="90c52-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="90c52-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="90c52-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="90c52-108">將執行的作業</span><span class="sxs-lookup"><span data-stu-id="90c52-108">What you will do</span></span>
<span data-ttu-id="90c52-109">安裝 Azure 命令列介面 (Azure CLI)。</span><span class="sxs-lookup"><span data-stu-id="90c52-109">Install the Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="90c52-110">如果您有任何問題，請在[疑難排解頁面][troubleshooting]尋求解決方案。</span><span class="sxs-lookup"><span data-stu-id="90c52-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="90c52-111">學習目標</span><span class="sxs-lookup"><span data-stu-id="90c52-111">What you will learn</span></span>
<span data-ttu-id="90c52-112">在本文中，您將了解：</span><span class="sxs-lookup"><span data-stu-id="90c52-112">In this article, you will learn:</span></span>
* <span data-ttu-id="90c52-113">如何安裝 Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="90c52-113">How to install Azure CLI.</span></span>
* <span data-ttu-id="90c52-114">如何新增 Azure CLI 的 IoT 子群組。</span><span class="sxs-lookup"><span data-stu-id="90c52-114">How to add an IoT subgroup of the Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="90c52-115">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="90c52-115">What you need</span></span>
* <span data-ttu-id="90c52-116">有網際網路連線的 Mac。</span><span class="sxs-lookup"><span data-stu-id="90c52-116">A Mac with an Internet connection.</span></span>
* <span data-ttu-id="90c52-117">有效的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="90c52-117">An active Azure subscription.</span></span> <span data-ttu-id="90c52-118">如果您沒有 Azure 帳戶，只需要幾分鐘的時間就可以建立[免費的 Azure 試用帳戶](http://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="90c52-118">If you don't have an Azure account, you can create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-python"></a><span data-ttu-id="90c52-119">安裝 Python</span><span class="sxs-lookup"><span data-stu-id="90c52-119">Install Python</span></span>
<span data-ttu-id="90c52-120">雖然 macOS 有現成的 Python 2.7，但建議您透過 Homebrew 安裝 Python。</span><span class="sxs-lookup"><span data-stu-id="90c52-120">Although macOS comes with Python 2.7 out of the box, we recommend that you install Python through Homebrew.</span></span> <span data-ttu-id="90c52-121">請參閱 [Installing Python on macOS](http://docs.python-guide.org/en/latest/starting/install/osx/) (在 macOS 上安裝 Python)。</span><span class="sxs-lookup"><span data-stu-id="90c52-121">See [Installing Python on macOS](http://docs.python-guide.org/en/latest/starting/install/osx/).</span></span>

<span data-ttu-id="90c52-122">執行下列命令安裝 Python 與 pip：</span><span class="sxs-lookup"><span data-stu-id="90c52-122">Install Python and pip by running the following command:</span></span>

```bash
brew install python
```

## <a name="install-the-azure-cli"></a><span data-ttu-id="90c52-123">安裝 Azure CLI</span><span class="sxs-lookup"><span data-stu-id="90c52-123">Install the Azure CLI</span></span>
<span data-ttu-id="90c52-124">Azure CLI 提供適用於 Azure 的多平台命令列體驗。</span><span class="sxs-lookup"><span data-stu-id="90c52-124">The Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="90c52-125">您可直接從命令列工作以佈建和管理資源。</span><span class="sxs-lookup"><span data-stu-id="90c52-125">You work directly from your command line to provision and manage resources.</span></span> 

<span data-ttu-id="90c52-126">若要安裝最新的 Azure CLI，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="90c52-126">To install the latest Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="90c52-127">在終端機視窗中執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="90c52-127">Run the following commands in a terminal window.</span></span> <span data-ttu-id="90c52-128">安裝 Azure CLI 可能需要五分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="90c52-128">It might take five minutes to install the Azure CLI.</span></span>

   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
2. <span data-ttu-id="90c52-129">執行下列命令以驗證安裝：</span><span class="sxs-lookup"><span data-stu-id="90c52-129">Verify the installation by running the following command:</span></span>

   ```bash
   az iot -h
   ```

<span data-ttu-id="90c52-130">如果已成功安裝，您應該會看見下列輸出。</span><span class="sxs-lookup"><span data-stu-id="90c52-130">You should see the following output if the installation is successful.</span></span>

![表示成功的輸出](media/iot-hub-intel-edison-lessons/lesson2/az_iot_help_osx.png)

## <a name="summary"></a><span data-ttu-id="90c52-132">摘要</span><span class="sxs-lookup"><span data-stu-id="90c52-132">Summary</span></span>
<span data-ttu-id="90c52-133">您已安裝 Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="90c52-133">You've installed the Azure CLI.</span></span> <span data-ttu-id="90c52-134">下一個工作是使用 Azure CLI 建立 Azure IoT 中樞和裝置身分識別。</span><span class="sxs-lookup"><span data-stu-id="90c52-134">Your next task is to create your Azure IoT hub and device identity by using the Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="90c52-135">後續步驟</span><span class="sxs-lookup"><span data-stu-id="90c52-135">Next steps</span></span>
<span data-ttu-id="90c52-136">[建立 IoT 中樞並登錄 Intel Edison][create-your-iot-hub-and-register-intel-edison]</span><span class="sxs-lookup"><span data-stu-id="90c52-136">[Create your IoT hub and register Intel Edison][create-your-iot-hub-and-register-intel-edison]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[create-your-iot-hub-and-register-intel-edison]: iot-hub-intel-edison-kit-c-lesson2-prepare-azure-iot-hub.md
[windows]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-mac.md
