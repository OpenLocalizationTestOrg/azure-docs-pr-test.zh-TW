---
title: "連接 Arduino tooAzure IoT-第 2 課： Azure tools (macOS) |Microsoft 文件"
description: "在 macOS 上安裝 Python 與 Azure 命令列介面 (Azure CLI)。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "azure cli, iot 雲端服務, arduino 雲端"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 9b719293-01d2-4a2d-9c49-476e67f4816d
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 8f0ec4131e54af5475cd0b4240480c3fda497e14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-azure-tools-macos-1010"></a><span data-ttu-id="54fc9-104">取得 Azure 工具 (macOS 10.10)</span><span class="sxs-lookup"><span data-stu-id="54fc9-104">Get Azure tools (macOS 10.10)</span></span>

> [!div class="op_single_selector"]
> * <span data-ttu-id="54fc9-105">[Windows 7 或更新版本][windows]</span><span class="sxs-lookup"><span data-stu-id="54fc9-105">[Windows 7 or later][windows]</span></span>
> * <span data-ttu-id="54fc9-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="54fc9-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="54fc9-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="54fc9-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="54fc9-108">將執行的作業</span><span class="sxs-lookup"><span data-stu-id="54fc9-108">What you will do</span></span>

<span data-ttu-id="54fc9-109">安裝 hello Azure 命令列介面 (Azure CLI)。</span><span class="sxs-lookup"><span data-stu-id="54fc9-109">Install hello Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="54fc9-110">如果您有任何問題，尋找解決方案上 hello[疑難排解頁面](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md)Adafruit 羽毛 M0 WiFi Arduino 版。</span><span class="sxs-lookup"><span data-stu-id="54fc9-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md) for your Adafruit Feather M0 WiFi Arduino board.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="54fc9-111">學習目標</span><span class="sxs-lookup"><span data-stu-id="54fc9-111">What you will learn</span></span>
<span data-ttu-id="54fc9-112">在本文中，您將了解：</span><span class="sxs-lookup"><span data-stu-id="54fc9-112">In this article, you will learn:</span></span>
* <span data-ttu-id="54fc9-113">如何 tooinstall Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="54fc9-113">How tooinstall Azure CLI.</span></span>
* <span data-ttu-id="54fc9-114">如何 tooadd 的 hello Azure CLI IoT 子群組。</span><span class="sxs-lookup"><span data-stu-id="54fc9-114">How tooadd an IoT subgroup of hello Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="54fc9-115">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="54fc9-115">What you need</span></span>
* <span data-ttu-id="54fc9-116">有網際網路連線的 Mac。</span><span class="sxs-lookup"><span data-stu-id="54fc9-116">A Mac with an Internet connection.</span></span>
* <span data-ttu-id="54fc9-117">有效的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="54fc9-117">An active Azure subscription.</span></span> <span data-ttu-id="54fc9-118">如果您沒有 Azure 帳戶，只需要幾分鐘的時間就可以建立[免費的 Azure 試用帳戶](http://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="54fc9-118">If you don't have an Azure account, you can create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-python"></a><span data-ttu-id="54fc9-119">安裝 Python</span><span class="sxs-lookup"><span data-stu-id="54fc9-119">Install Python</span></span>
<span data-ttu-id="54fc9-120">雖然 macOS 隨附 Python 2.7 hello 立即可用，但我們建議您安裝 Homebrew 透過 Python。</span><span class="sxs-lookup"><span data-stu-id="54fc9-120">Although macOS comes with Python 2.7 out of hello box, we recommend that you install Python through Homebrew.</span></span> <span data-ttu-id="54fc9-121">請參閱 [Installing Python on macOS](http://docs.python-guide.org/en/latest/starting/install/osx/) (在 macOS 上安裝 Python)。</span><span class="sxs-lookup"><span data-stu-id="54fc9-121">See [Installing Python on macOS](http://docs.python-guide.org/en/latest/starting/install/osx/).</span></span>

<span data-ttu-id="54fc9-122">安裝 Python 和 pip 執行 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="54fc9-122">Install Python and pip by running hello following command:</span></span>

```bash
brew install python
```

## <a name="install-hello-azure-cli"></a><span data-ttu-id="54fc9-123">安裝 hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="54fc9-123">Install hello Azure CLI</span></span>
<span data-ttu-id="54fc9-124">hello Azure CLI 提供 Azure 的多平台命令列體驗。</span><span class="sxs-lookup"><span data-stu-id="54fc9-124">hello Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="54fc9-125">您可以直接從命令列 tooprovision 工作和管理資源。</span><span class="sxs-lookup"><span data-stu-id="54fc9-125">You work directly from your command line tooprovision and manage resources.</span></span>

<span data-ttu-id="54fc9-126">tooinstall hello 最新的 Azure CLI，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="54fc9-126">tooinstall hello latest Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="54fc9-127">執行下列命令在 terminal 視窗中的 hello。</span><span class="sxs-lookup"><span data-stu-id="54fc9-127">Run hello following commands in a terminal window.</span></span> <span data-ttu-id="54fc9-128">可能需要五分鐘 tooinstall hello Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="54fc9-128">It might take five minutes tooinstall hello Azure CLI.</span></span>

   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
2. <span data-ttu-id="54fc9-129">執行下列命令的 hello 驗證 hello 安裝：</span><span class="sxs-lookup"><span data-stu-id="54fc9-129">Verify hello installation by running hello following command:</span></span>

   ```bash
   az iot -h
   ```

<span data-ttu-id="54fc9-130">您應該會看到下列 hello 輸出 hello 安裝是否成功。</span><span class="sxs-lookup"><span data-stu-id="54fc9-130">You should see hello following output if hello installation is successful.</span></span>

![表示成功的輸出][output]

## <a name="summary"></a><span data-ttu-id="54fc9-132">摘要</span><span class="sxs-lookup"><span data-stu-id="54fc9-132">Summary</span></span>
<span data-ttu-id="54fc9-133">您已安裝 hello Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="54fc9-133">You've installed hello Azure CLI.</span></span> <span data-ttu-id="54fc9-134">您的下一個工作是 toocreate 使用您 Azure IoT 中樞和裝置身分識別 hello Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="54fc9-134">Your next task is toocreate your Azure IoT hub and device identity by using hello Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="54fc9-135">後續步驟</span><span class="sxs-lookup"><span data-stu-id="54fc9-135">Next steps</span></span>
<span data-ttu-id="54fc9-136">[建立 IoT 中樞並註冊您的 Arduino 面板][create-your-iot-hub-and-register-your-arduino-board]</span><span class="sxs-lookup"><span data-stu-id="54fc9-136">[Create your IoT hub and register your Arduino board][create-your-iot-hub-and-register-your-arduino-board]</span></span>


<!-- Images and links -->

[windows]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-win32.md
[ubuntu]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-ubuntu.md
[macos]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-mac.md
[output]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson2/az_iot_help_osx.png
[create-your-iot-hub-and-register-your-arduino-board]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-prepare-azure-iot-hub.md