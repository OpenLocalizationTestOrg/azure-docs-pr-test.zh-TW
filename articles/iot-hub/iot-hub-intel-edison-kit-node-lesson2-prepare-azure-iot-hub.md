---
title: "將 Intel Edison (節點) 連接到 Azure IoT - 第 2 課：登錄裝置 | Microsoft Docs"
description: "使用 Azure CLI 建立資源群組、建立 Azure IoT 中樞，並在 Azure IoT 中樞中登錄 Edison。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: 
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: c1465cc2-d0d9-4326-967c-64d95b61dd54
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 81584c1b7314c4331ac059b8e3ed782970588ae2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-your-iot-hub-and-register-intel-edison"></a><span data-ttu-id="9396f-103">建立 IoT 中樞並登錄 Intel Edison</span><span class="sxs-lookup"><span data-stu-id="9396f-103">Create your IoT hub and register Intel Edison</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="9396f-104">將執行的作業</span><span class="sxs-lookup"><span data-stu-id="9396f-104">What you will do</span></span>
* <span data-ttu-id="9396f-105">建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="9396f-105">Create a resource group.</span></span>
* <span data-ttu-id="9396f-106">在資源群組中建立 Azure IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="9396f-106">Create your Azure IoT hub in the resource group.</span></span>
* <span data-ttu-id="9396f-107">使用 Azure 命令列介面 (Azure CLI)，將 Intel Edison 新增至 Azure IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="9396f-107">Add Intel Edison to the Azure IoT hub by using the Azure command-line interface (Azure CLI).</span></span>

<span data-ttu-id="9396f-108">當您使用 Azure CLI 將 Edison 加入 IoT 中樞時，服務將會為 Edison 產生一組金鑰，以向服務進行驗證。</span><span class="sxs-lookup"><span data-stu-id="9396f-108">When you use the Azure CLI to add Edison to your IoT hub, the service generates a key for Edison to authenticate with the service.</span></span> <span data-ttu-id="9396f-109">如果您有任何問題，請在[疑難排解頁面][troubleshooting]尋求解決方案。</span><span class="sxs-lookup"><span data-stu-id="9396f-109">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="9396f-110">學習目標</span><span class="sxs-lookup"><span data-stu-id="9396f-110">What you will learn</span></span>
<span data-ttu-id="9396f-111">在本文中，您將了解：</span><span class="sxs-lookup"><span data-stu-id="9396f-111">In this article, you will learn:</span></span>
* <span data-ttu-id="9396f-112">如何使用 Azure CLI 建立 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="9396f-112">How to use the Azure CLI to create an IoT hub.</span></span>
* <span data-ttu-id="9396f-113">如何在 IoT 中樞為 Edison 建立裝置身分識別。</span><span class="sxs-lookup"><span data-stu-id="9396f-113">How to create a device identity for Edison in your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="9396f-114">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="9396f-114">What you need</span></span>
* <span data-ttu-id="9396f-115">一個 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="9396f-115">An Azure account.</span></span> <span data-ttu-id="9396f-116">如果您沒有 Azure 帳戶，請花幾分鐘的時間建立[免費的 Azure 試用帳戶](http://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="9396f-116">If you don't have an Azure account, create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>
* <span data-ttu-id="9396f-117">您應該已經安裝 Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="9396f-117">You should have the Azure CLI installed.</span></span>

## <a name="create-your-iot-hub"></a><span data-ttu-id="9396f-118">建立 IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="9396f-118">Create your IoT hub</span></span>
<span data-ttu-id="9396f-119">Azure IoT 中樞可以協助您連接、監視並管理數以百萬計的 IoT 資產。</span><span class="sxs-lookup"><span data-stu-id="9396f-119">Azure IoT Hub helps you connect, monitor, and manage millions of IoT assets.</span></span> <span data-ttu-id="9396f-120">若要建立 IoT 中樞，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="9396f-120">To create your IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="9396f-121">執行下列命令來登入您的 Azure 帳戶：</span><span class="sxs-lookup"><span data-stu-id="9396f-121">Sign in to your Azure account by running the following command:</span></span>

   ```bash
   az login
   ```

   <span data-ttu-id="9396f-122">成功登入之後，系統將會列出所有可用的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="9396f-122">All your available subscriptions are listed after a successful sign-in.</span></span>

2. <span data-ttu-id="9396f-123">執行下列命令來設定您想要使用的預設訂用帳戶：</span><span class="sxs-lookup"><span data-stu-id="9396f-123">Set the default subscription that you want to use by running the following command:</span></span>

   ```bash
   az account set --subscription {subscription id or name}
   ```

   <span data-ttu-id="9396f-124">`subscription ID or name` 可在 `az login` 或 `az account list` 命令的輸出中找到。</span><span class="sxs-lookup"><span data-stu-id="9396f-124">`subscription ID or name` can be found in the output of the `az login` or the `az account list` command.</span></span>

3. <span data-ttu-id="9396f-125">執行下列命令來登錄提供者。</span><span class="sxs-lookup"><span data-stu-id="9396f-125">Register the provider by running the following command.</span></span> <span data-ttu-id="9396f-126">資源提供者是為應用程式提供資源的服務。</span><span class="sxs-lookup"><span data-stu-id="9396f-126">Resource providers are services that provide resources for your application.</span></span> <span data-ttu-id="9396f-127">您必須先登錄提供者，才能部署該提供者所提供的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="9396f-127">You must register the provider before you can deploy the Azure resource that the provider offers.</span></span>

   ```bash
   az provider register -n "Microsoft.Devices"
   ```
4. <span data-ttu-id="9396f-128">執行下列命令來在美國西部區域建立名為 iot-sample 的資源群組：</span><span class="sxs-lookup"><span data-stu-id="9396f-128">Create a resource group named iot-sample in the West US region by running the following command:</span></span>

   ```bash
   az group create --name iot-sample --location westus
   ```

   <span data-ttu-id="9396f-129">`westus` 是資源群組建立所在的位置。</span><span class="sxs-lookup"><span data-stu-id="9396f-129">`westus` is the location you create your resource group.</span></span> <span data-ttu-id="9396f-130">如果您想要使用另一個位置，您可以執行 `az account list-locations -o table` 來查看 Azure 支援的所有位置。</span><span class="sxs-lookup"><span data-stu-id="9396f-130">If you want to use another location, you can run `az account list-locations -o table` to see all the locations Azure supports.</span></span>

5. <span data-ttu-id="9396f-131">執行下列命令來在 iot-sample 資源群組中建立 IoT 中樞：</span><span class="sxs-lookup"><span data-stu-id="9396f-131">Create an IoT hub in the iot-sample resource group by running the following command:</span></span>

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-sample
   ```

<span data-ttu-id="9396f-132">根據預設，此工具會在免費定價層建立 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="9396f-132">By default, the tool creates an IoT Hub in the Free pricing tier.</span></span> <span data-ttu-id="9396f-133">如需詳細資訊，請參閱 [Azure IoT 中樞價格](https://azure.microsoft.com/pricing/details/iot-hub/)。</span><span class="sxs-lookup"><span data-stu-id="9396f-133">For more infomation, see [Azure IoT Hub pricing](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

> [!NOTE] 
> <span data-ttu-id="9396f-134">您 IoT 中樞的名稱必須是全域唯一的。</span><span class="sxs-lookup"><span data-stu-id="9396f-134">The name of your IoT hub must be globally unique.</span></span>
> <span data-ttu-id="9396f-135">您的 Azure 訂用帳戶只能建立一個 F1 版本的 Azure IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="9396f-135">You can create only one F1 edition of Azure IoT Hub under your Azure subscription.</span></span>


## <a name="register-edison-in-your-iot-hub"></a><span data-ttu-id="9396f-136">在 IoT 中樞中登錄 Edison</span><span class="sxs-lookup"><span data-stu-id="9396f-136">Register Edison in your IoT hub</span></span>
<span data-ttu-id="9396f-137">每一個向/從 IoT 中樞傳送/接收訊息的裝置，都必須以唯一識別碼登錄。</span><span class="sxs-lookup"><span data-stu-id="9396f-137">Each device that sends messages to your IoT hub and receives messages from your IoT hub must be registered with a unique ID.</span></span>

<span data-ttu-id="9396f-138">執行下列命令在 Azure IoT 中樞中登錄 Edison：</span><span class="sxs-lookup"><span data-stu-id="9396f-138">Register Edison in your IoT hub by running following command:</span></span>

```bash
az iot device create --device-id myinteledison --hub-name {my hub name}
```

## <a name="summary"></a><span data-ttu-id="9396f-139">摘要</span><span class="sxs-lookup"><span data-stu-id="9396f-139">Summary</span></span>
<span data-ttu-id="9396f-140">您已建立 IoT 中樞，並在 IoT 中樞中搭配裝置識別登錄 Edison。</span><span class="sxs-lookup"><span data-stu-id="9396f-140">You've created an IoT hub and registered Edison with a device identity in your IoT hub.</span></span> <span data-ttu-id="9396f-141">您已準備好了解如何從 Edison 傳送訊息至 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="9396f-141">You're ready to learn how to send messages from Edison to your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9396f-142">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9396f-142">Next steps</span></span>
<span data-ttu-id="9396f-143">[建立 Azure 函式應用程式和 Azure 儲存體帳戶以處理並儲存 IoT 中樞訊息][process-and-store-iot-hub-messages]。</span><span class="sxs-lookup"><span data-stu-id="9396f-143">[Create an Azure function app and an Azure Storage account to process and store IoT hub messages][process-and-store-iot-hub-messages].</span></span>


<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-intel-edison-kit-node-lesson3-deploy-resource-manager-template.md