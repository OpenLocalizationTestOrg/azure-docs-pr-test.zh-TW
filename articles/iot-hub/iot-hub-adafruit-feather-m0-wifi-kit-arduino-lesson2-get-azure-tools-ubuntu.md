---
title: "連接 Arduino tooAzure IoT-第 2 課： Azure tools (Ubuntu) |Microsoft 文件"
description: "在 Ubuntu 上安裝 Python 與 Azure 命令列介面 (Azure CLI)。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "azure cli, iot 雲端服務, arduino 雲端"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: bb5cb602-7292-4772-ac90-c0b52ebc8340
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 7eb9c891a6340fee018894883583022d740ecb6f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-azure-tools-ubuntu-1604"></a><span data-ttu-id="05117-104">取得 Azure 工具 (Ubuntu 16.04)</span><span class="sxs-lookup"><span data-stu-id="05117-104">Get Azure tools (Ubuntu 16.04)</span></span>

> [!div class="op_single_selector"]
> * <span data-ttu-id="05117-105">[Windows 7 或更新版本][windows]</span><span class="sxs-lookup"><span data-stu-id="05117-105">[Windows 7 or later][windows]</span></span>
> * <span data-ttu-id="05117-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="05117-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="05117-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="05117-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="05117-108">將執行的作業</span><span class="sxs-lookup"><span data-stu-id="05117-108">What you will do</span></span>

<span data-ttu-id="05117-109">安裝 hello Azure 命令列介面 (Azure CLI)。</span><span class="sxs-lookup"><span data-stu-id="05117-109">Install hello Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="05117-110">如果您有任何問題，尋找解決方案上 hello[疑難排解頁面](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md)Adafruit 羽毛 M0 WiFi Arduino 版。</span><span class="sxs-lookup"><span data-stu-id="05117-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md) for your Adafruit Feather M0 WiFi Arduino board.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="05117-111">學習目標</span><span class="sxs-lookup"><span data-stu-id="05117-111">What you will learn</span></span>
<span data-ttu-id="05117-112">在本文中，您將了解：</span><span class="sxs-lookup"><span data-stu-id="05117-112">In this article, you will learn:</span></span>
* <span data-ttu-id="05117-113">如何 tooinstall hello Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="05117-113">How tooinstall hello Azure CLI.</span></span>
* <span data-ttu-id="05117-114">如何 tooadd 的 hello Azure CLI IoT 子群組。</span><span class="sxs-lookup"><span data-stu-id="05117-114">How tooadd an IoT subgroup of hello Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="05117-115">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="05117-115">What you need</span></span>
* <span data-ttu-id="05117-116">一部具有網際網路連線的 Ubuntu 電腦。</span><span class="sxs-lookup"><span data-stu-id="05117-116">An Ubuntu computer with an Internet connection.</span></span>
* <span data-ttu-id="05117-117">有效的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="05117-117">An active Azure subscription.</span></span> <span data-ttu-id="05117-118">如果您沒有帳戶，只需要幾分鐘的時間就可以建立[免費試用帳戶](http://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="05117-118">If you don't have an account, you can create a [free trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-hello-azure-cli"></a><span data-ttu-id="05117-119">安裝 hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="05117-119">Install hello Azure CLI</span></span>
<span data-ttu-id="05117-120">提供以多平台命令列體驗 azure，讓您直接從命令列 tooprovision toowork hello Azure CLI，並管理資源。</span><span class="sxs-lookup"><span data-stu-id="05117-120">hello Azure CLI provides a multiplatform command-line experience for Azure, enabling you toowork directly from your command line tooprovision and manage resources.</span></span>

<span data-ttu-id="05117-121">tooinstall hello 最新的 Azure CLI，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="05117-121">tooinstall hello latest Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="05117-122">執行下列命令在 terminal 視窗中的 hello。</span><span class="sxs-lookup"><span data-stu-id="05117-122">Run hello following commands in a terminal window.</span></span> <span data-ttu-id="05117-123">可能需要五分鐘 tooinstall hello Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="05117-123">It might take five minutes tooinstall hello Azure CLI.</span></span>

   ```bash
   sudo apt-get update
   sudo apt-get install -y libssl-dev libffi-dev
   sudo apt-get install -y python-dev
   sudo apt-get install -y build-essential
   sudo apt-get install -y python-pip
   sudo pip install --upgrade azure-cli
   sudo pip install --upgrade azure-cli-iot
   ```
2. <span data-ttu-id="05117-124">執行下列命令的 hello 驗證 hello 安裝：</span><span class="sxs-lookup"><span data-stu-id="05117-124">Verify hello installation by running hello following command:</span></span>

   ```bash
   az iot -h
   ```

<span data-ttu-id="05117-125">您應該會看到下列 hello 輸出 hello 安裝是否成功。</span><span class="sxs-lookup"><span data-stu-id="05117-125">You should see hello following output if hello installation is successful.</span></span>

![表示成功的輸出][output]

## <a name="summary"></a><span data-ttu-id="05117-127">摘要</span><span class="sxs-lookup"><span data-stu-id="05117-127">Summary</span></span>
<span data-ttu-id="05117-128">您已安裝 hello Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="05117-128">You've installed hello Azure CLI.</span></span> <span data-ttu-id="05117-129">您的下一個工作是 toocreate 您的 Azure IoT 中樞與裝置身分識別使用 hello Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="05117-129">Your next task is toocreate your Azure IoT hub and device identity using hello Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="05117-130">後續步驟</span><span class="sxs-lookup"><span data-stu-id="05117-130">Next steps</span></span>
<span data-ttu-id="05117-131">[建立 IoT 中樞並註冊您的 Arduino 面板][create-your-iot-hub-and-register-your-arduino-board]</span><span class="sxs-lookup"><span data-stu-id="05117-131">[Create your IoT hub and register your Arduino board][create-your-iot-hub-and-register-your-arduino-board]</span></span>
<!-- Images and links -->

[windows]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-win32.md
[ubuntu]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-ubuntu.md
[macos]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-mac.md
[output]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson2/az_iot_help_ubuntu.png
[create-your-iot-hub-and-register-your-arduino-board]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-prepare-azure-iot-hub.md