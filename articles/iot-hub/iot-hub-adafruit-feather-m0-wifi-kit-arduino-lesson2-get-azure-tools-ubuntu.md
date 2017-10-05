---
title: "將 Arduino 連線至 Azure IoT - 第 2 課：取得工具 (Ubuntu) | Microsoft Docs"
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
ms.openlocfilehash: a2f83e59a37abc3f44e770b22ac089b88481a6a4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-azure-tools-ubuntu-1604"></a><span data-ttu-id="03f2d-104">取得 Azure 工具 (Ubuntu 16.04)</span><span class="sxs-lookup"><span data-stu-id="03f2d-104">Get Azure tools (Ubuntu 16.04)</span></span>

> [!div class="op_single_selector"]
> * <span data-ttu-id="03f2d-105">[Windows 7 或更新版本][windows]</span><span class="sxs-lookup"><span data-stu-id="03f2d-105">[Windows 7 or later][windows]</span></span>
> * <span data-ttu-id="03f2d-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="03f2d-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="03f2d-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="03f2d-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="03f2d-108">將執行的作業</span><span class="sxs-lookup"><span data-stu-id="03f2d-108">What you will do</span></span>

<span data-ttu-id="03f2d-109">安裝 Azure 命令列介面 (Azure CLI)。</span><span class="sxs-lookup"><span data-stu-id="03f2d-109">Install the Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="03f2d-110">如果您有任何問題，請在 Adafruit Feather M0 WiFi Arduino 面版的[疑難排解頁面](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md)尋求解決方案。</span><span class="sxs-lookup"><span data-stu-id="03f2d-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md) for your Adafruit Feather M0 WiFi Arduino board.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="03f2d-111">學習目標</span><span class="sxs-lookup"><span data-stu-id="03f2d-111">What you will learn</span></span>
<span data-ttu-id="03f2d-112">在本文中，您將了解：</span><span class="sxs-lookup"><span data-stu-id="03f2d-112">In this article, you will learn:</span></span>
* <span data-ttu-id="03f2d-113">如何安裝 Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="03f2d-113">How to install the Azure CLI.</span></span>
* <span data-ttu-id="03f2d-114">如何新增 Azure CLI 的 IoT 子群組。</span><span class="sxs-lookup"><span data-stu-id="03f2d-114">How to add an IoT subgroup of the Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="03f2d-115">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="03f2d-115">What you need</span></span>
* <span data-ttu-id="03f2d-116">一部具有網際網路連線的 Ubuntu 電腦。</span><span class="sxs-lookup"><span data-stu-id="03f2d-116">An Ubuntu computer with an Internet connection.</span></span>
* <span data-ttu-id="03f2d-117">有效的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="03f2d-117">An active Azure subscription.</span></span> <span data-ttu-id="03f2d-118">如果您沒有帳戶，只需要幾分鐘的時間就可以建立[免費試用帳戶](http://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="03f2d-118">If you don't have an account, you can create a [free trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-the-azure-cli"></a><span data-ttu-id="03f2d-119">安裝 Azure CLI</span><span class="sxs-lookup"><span data-stu-id="03f2d-119">Install the Azure CLI</span></span>
<span data-ttu-id="03f2d-120">Azure CLI 能為 Azure 提供多平台的命令列體驗，使您可以直接從命令列進行資源的佈建及管理。</span><span class="sxs-lookup"><span data-stu-id="03f2d-120">The Azure CLI provides a multiplatform command-line experience for Azure, enabling you to work directly from your command line to provision and manage resources.</span></span>

<span data-ttu-id="03f2d-121">若要安裝最新的 Azure CLI，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="03f2d-121">To install the latest Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="03f2d-122">在終端機視窗中執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="03f2d-122">Run the following commands in a terminal window.</span></span> <span data-ttu-id="03f2d-123">安裝 Azure CLI 可能需要五分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="03f2d-123">It might take five minutes to install the Azure CLI.</span></span>

   ```bash
   sudo apt-get update
   sudo apt-get install -y libssl-dev libffi-dev
   sudo apt-get install -y python-dev
   sudo apt-get install -y build-essential
   sudo apt-get install -y python-pip
   sudo pip install --upgrade azure-cli
   sudo pip install --upgrade azure-cli-iot
   ```
2. <span data-ttu-id="03f2d-124">執行下列命令以驗證安裝：</span><span class="sxs-lookup"><span data-stu-id="03f2d-124">Verify the installation by running the following command:</span></span>

   ```bash
   az iot -h
   ```

<span data-ttu-id="03f2d-125">如果已成功安裝，您應該會看見下列輸出。</span><span class="sxs-lookup"><span data-stu-id="03f2d-125">You should see the following output if the installation is successful.</span></span>

![表示成功的輸出][output]

## <a name="summary"></a><span data-ttu-id="03f2d-127">摘要</span><span class="sxs-lookup"><span data-stu-id="03f2d-127">Summary</span></span>
<span data-ttu-id="03f2d-128">您已安裝 Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="03f2d-128">You've installed the Azure CLI.</span></span> <span data-ttu-id="03f2d-129">下一個工作是使用 Azure CLI 建立 Azure IoT 中樞和裝置身分識別。</span><span class="sxs-lookup"><span data-stu-id="03f2d-129">Your next task is to create your Azure IoT hub and device identity using the Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="03f2d-130">後續步驟</span><span class="sxs-lookup"><span data-stu-id="03f2d-130">Next steps</span></span>
<span data-ttu-id="03f2d-131">[建立 IoT 中樞並註冊您的 Arduino 面板][create-your-iot-hub-and-register-your-arduino-board]</span><span class="sxs-lookup"><span data-stu-id="03f2d-131">[Create your IoT hub and register your Arduino board][create-your-iot-hub-and-register-your-arduino-board]</span></span>
<!-- Images and links -->

[windows]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-win32.md
[ubuntu]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-ubuntu.md
[macos]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-mac.md
[output]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson2/az_iot_help_ubuntu.png
[create-your-iot-hub-and-register-your-arduino-board]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-prepare-azure-iot-hub.md