---
title: "將 Intel Edison (節點) 連接到 Azure IoT - 第 2 課：Azure 工具 (Ubuntu) | Microsoft Docs"
description: "在 Ubuntu 上安裝 Python 與 Azure 命令列介面 (Azure CLI)。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "azure cli, iot 雲端服務, arduino 雲端"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: 6dcb34bf-54a3-4af0-ba89-95d5cfafceff
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 65248e14d0ea05a44efe76e66e1ef519285982b3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-azure-tools-ubuntu-1604"></a><span data-ttu-id="a7540-104">取得 Azure 工具 (Ubuntu 16.04)</span><span class="sxs-lookup"><span data-stu-id="a7540-104">Get Azure tools (Ubuntu 16.04)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="a7540-105">[Windows 7 和更新版本][windows]</span><span class="sxs-lookup"><span data-stu-id="a7540-105">[Windows 7 and later][windows]</span></span>
> * <span data-ttu-id="a7540-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="a7540-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="a7540-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="a7540-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="a7540-108">將執行的作業</span><span class="sxs-lookup"><span data-stu-id="a7540-108">What you will do</span></span>
<span data-ttu-id="a7540-109">安裝 Azure 命令列介面 (Azure CLI)。</span><span class="sxs-lookup"><span data-stu-id="a7540-109">Install the Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="a7540-110">如果您有任何問題，請在[疑難排解頁面][troubleshooting]尋求解決方案。</span><span class="sxs-lookup"><span data-stu-id="a7540-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="a7540-111">學習目標</span><span class="sxs-lookup"><span data-stu-id="a7540-111">What you will learn</span></span>
<span data-ttu-id="a7540-112">在本文中，您將了解：</span><span class="sxs-lookup"><span data-stu-id="a7540-112">In this article, you will learn:</span></span>
* <span data-ttu-id="a7540-113">如何安裝 Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="a7540-113">How to install the Azure CLI.</span></span>
* <span data-ttu-id="a7540-114">如何新增 Azure CLI 的 IoT 子群組。</span><span class="sxs-lookup"><span data-stu-id="a7540-114">How to add an IoT subgroup of the Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="a7540-115">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="a7540-115">What you need</span></span>
* <span data-ttu-id="a7540-116">一部具有網際網路連線的 Ubuntu 電腦。</span><span class="sxs-lookup"><span data-stu-id="a7540-116">An Ubuntu computer with an Internet connection.</span></span>
* <span data-ttu-id="a7540-117">有效的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="a7540-117">An active Azure subscription.</span></span> <span data-ttu-id="a7540-118">如果您沒有帳戶，只需要幾分鐘的時間就可以建立[免費試用帳戶](http://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="a7540-118">If you don't have an account, you can create a [free trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-the-azure-cli"></a><span data-ttu-id="a7540-119">安裝 Azure CLI</span><span class="sxs-lookup"><span data-stu-id="a7540-119">Install the Azure CLI</span></span>
<span data-ttu-id="a7540-120">Azure CLI 能為 Azure 提供多平台的命令列體驗，使您可以直接從命令列進行資源的佈建及管理。</span><span class="sxs-lookup"><span data-stu-id="a7540-120">The Azure CLI provides a multiplatform command-line experience for Azure, enabling you to work directly from your command line to provision and manage resources.</span></span>

<span data-ttu-id="a7540-121">若要安裝最新的 Azure CLI，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="a7540-121">To install the latest Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="a7540-122">在終端機視窗中執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="a7540-122">Run the following commands in a terminal window.</span></span> <span data-ttu-id="a7540-123">安裝 Azure CLI 可能需要五分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="a7540-123">It might take five minutes to install the Azure CLI.</span></span>

   ```bash
   sudo apt-get update
   sudo apt-get install -y libssl-dev libffi-dev
   sudo apt-get install -y python-dev
   sudo apt-get install -y build-essential
   sudo apt-get install -y python-pip
   sudo pip install --upgrade azure-cli
   sudo pip install --upgrade azure-cli-iot
   ```
2. <span data-ttu-id="a7540-124">執行下列命令以驗證安裝：</span><span class="sxs-lookup"><span data-stu-id="a7540-124">Verify the installation by running the following command:</span></span>

   ```bash
   az iot -h
   ```

<span data-ttu-id="a7540-125">如果已成功安裝，您應該會看見下列輸出。</span><span class="sxs-lookup"><span data-stu-id="a7540-125">You should see the following output if the installation is successful.</span></span>

![表示成功的輸出](media/iot-hub-intel-edison-lessons/lesson2/az_iot_help_ubuntu.png)

## <a name="summary"></a><span data-ttu-id="a7540-127">摘要</span><span class="sxs-lookup"><span data-stu-id="a7540-127">Summary</span></span>
<span data-ttu-id="a7540-128">您已安裝 Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="a7540-128">You've installed the Azure CLI.</span></span> <span data-ttu-id="a7540-129">下一個工作是使用 Azure CLI 建立 Azure IoT 中樞和裝置身分識別。</span><span class="sxs-lookup"><span data-stu-id="a7540-129">Your next task is to create your Azure IoT hub and device identity using the Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a7540-130">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a7540-130">Next steps</span></span>
<span data-ttu-id="a7540-131">[建立 IoT 中樞並登錄 Intel Edison][create-your-iot-hub-and-register-intel-edison]</span><span class="sxs-lookup"><span data-stu-id="a7540-131">[Create your IoT hub and register Intel Edison][create-your-iot-hub-and-register-intel-edison]</span></span>


<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[create-your-iot-hub-and-register-intel-edison]: iot-hub-intel-edison-kit-node-lesson2-prepare-azure-iot-hub.md
[windows]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-mac.md
