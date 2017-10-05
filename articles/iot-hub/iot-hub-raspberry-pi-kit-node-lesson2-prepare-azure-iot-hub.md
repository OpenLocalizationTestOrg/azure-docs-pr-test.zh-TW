---
featureFlags: usabilla
title: "將 Raspberry Pi (節點) 連接到 Azure IoT - 第 2 課：登錄裝置 | Microsoft Docs"
description: "使用 Azure CLI 建立資源群組、建立 Azure IoT 中樞，並在 IoT 中樞身分識別登錄中登錄 Pi。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "raspberry pi 雲端, pi 雲端連線"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 736215b6-e7e4-46f9-af30-0ded9ffa5204
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 774f9356d7a11b2c61905ada75bed92d44e5fc0c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-your-iot-hub-and-register-raspberry-pi-3"></a><span data-ttu-id="c2f55-104">建立 IoT 中樞並登錄 Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="c2f55-104">Create your IoT hub and register Raspberry Pi 3</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="c2f55-105">將執行的作業</span><span class="sxs-lookup"><span data-stu-id="c2f55-105">What you will do</span></span>
* <span data-ttu-id="c2f55-106">建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="c2f55-106">Create a resource group.</span></span>
* <span data-ttu-id="c2f55-107">在資源群組中建立 Azure IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="c2f55-107">Create your Azure IoT hub in the resource group.</span></span>
* <span data-ttu-id="c2f55-108">使用 Azure 命令列介面 (Azure CLI)，將 Raspberry Pi 3 新增至 Azure IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="c2f55-108">Add Raspberry Pi 3 to the Azure IoT hub by using the Azure command-line interface (Azure CLI).</span></span>

<span data-ttu-id="c2f55-109">當您使用 Azure CLI 將 Pi 加入 IoT 中樞時，服務將會為 Pi 產生一組金鑰，以向服務進行驗證。</span><span class="sxs-lookup"><span data-stu-id="c2f55-109">When you use Azure CLI to add Pi to your IoT hub, the service generates a key for Pi to authenticate with the service.</span></span> <span data-ttu-id="c2f55-110">如果您有任何問題，請在[疑難排解頁面](iot-hub-raspberry-pi-kit-node-troubleshooting.md)尋求解決方案。</span><span class="sxs-lookup"><span data-stu-id="c2f55-110">If you have any problems, seek solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="c2f55-111">學習目標</span><span class="sxs-lookup"><span data-stu-id="c2f55-111">What you will learn</span></span>
<span data-ttu-id="c2f55-112">在本文中，您將了解：</span><span class="sxs-lookup"><span data-stu-id="c2f55-112">In this article, you will learn:</span></span>
* <span data-ttu-id="c2f55-113">如何使用 Azure CLI 建立 IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="c2f55-113">How to use Azure CLI to create an IoT hub</span></span>
* <span data-ttu-id="c2f55-114">如何在 IoT 中樞為 Pi 建立裝置身分識別</span><span class="sxs-lookup"><span data-stu-id="c2f55-114">How to create a device identity for Pi in your IoT hub</span></span>

## <a name="what-you-need"></a><span data-ttu-id="c2f55-115">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="c2f55-115">What you need</span></span>
* <span data-ttu-id="c2f55-116">一個 Azure 帳戶</span><span class="sxs-lookup"><span data-stu-id="c2f55-116">An Azure account</span></span>
* <span data-ttu-id="c2f55-117">一部已安裝 Azure CLI 的 Mac 或 Windows 電腦</span><span class="sxs-lookup"><span data-stu-id="c2f55-117">A Mac or a Windows computer with the Azure CLI installed</span></span>

## <a name="create-your-iot-hub"></a><span data-ttu-id="c2f55-118">建立 IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="c2f55-118">Create your IoT hub</span></span>
<span data-ttu-id="c2f55-119">Azure IoT 中樞可以協助您連接、監視並管理數以百萬計的 IoT 資產。</span><span class="sxs-lookup"><span data-stu-id="c2f55-119">Azure IoT Hub helps you connect, monitor, and manage millions of IoT assets.</span></span> <span data-ttu-id="c2f55-120">若要建立 IoT 中樞，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="c2f55-120">To create your IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="c2f55-121">執行下列命令來登入您的 Azure 帳戶：</span><span class="sxs-lookup"><span data-stu-id="c2f55-121">Sign in to your Azure account by running the following command:</span></span>

   ```bash
   az login
   ```

   <span data-ttu-id="c2f55-122">成功登入之後，系統將會列出所有可用的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="c2f55-122">All your available subscriptions are listed after a successful sign-in.</span></span>

2. <span data-ttu-id="c2f55-123">執行下列命令來設定您想要使用的預設訂用帳戶：</span><span class="sxs-lookup"><span data-stu-id="c2f55-123">Set the default subscription that you want to use by running the following command:</span></span>

   ```bash
   az account set --subscription {subscription id or name}
   ```

   <span data-ttu-id="c2f55-124">`subscription ID or name` 可在 `az login` 或 `az account list` 命令的輸出中找到。</span><span class="sxs-lookup"><span data-stu-id="c2f55-124">`subscription ID or name` can be found in the output of the `az login` or the `az account list` command.</span></span>

3. <span data-ttu-id="c2f55-125">執行下列命令來登錄提供者。</span><span class="sxs-lookup"><span data-stu-id="c2f55-125">Register the provider by running the following command.</span></span> <span data-ttu-id="c2f55-126">資源提供者是為應用程式提供資源的服務。</span><span class="sxs-lookup"><span data-stu-id="c2f55-126">Resource providers are services that provide resources for your application.</span></span> <span data-ttu-id="c2f55-127">您必須先登錄提供者，才能部署該提供者所提供的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="c2f55-127">You must register the provider before you can deploy the Azure resource that the provider offers.</span></span>

   ```bash
   az provider register -n "Microsoft.Devices"
   ```
4. <span data-ttu-id="c2f55-128">執行下列命令來在美國西部區域建立名為 iot-sample 的資源群組：</span><span class="sxs-lookup"><span data-stu-id="c2f55-128">Create a resource group named iot-sample in the West US region by running the following command:</span></span>

   ```bash
   az group create --name iot-sample --location westus
   ```

   <span data-ttu-id="c2f55-129">`westus` 是資源群組建立所在的位置。</span><span class="sxs-lookup"><span data-stu-id="c2f55-129">`westus` is the location you create your resource group.</span></span> <span data-ttu-id="c2f55-130">如果您想要使用另一個位置，您可以執行 `az account list-locations -o table` 來查看 Azure 支援的所有位置。</span><span class="sxs-lookup"><span data-stu-id="c2f55-130">If you want to use another location, you can run `az account list-locations -o table` to see all the locations Azure supports.</span></span>
 
5. <span data-ttu-id="c2f55-131">執行下列命令來在 iot-sample 資源群組中建立 IoT 中樞：</span><span class="sxs-lookup"><span data-stu-id="c2f55-131">Create an IoT hub in the iot-sample resource group by running the following command:</span></span>

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-sample
   ```

   <span data-ttu-id="c2f55-132">根據預設，此工具會在免費定價層建立 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="c2f55-132">By default, the tool creates an IoT Hub in the Free pricing tier.</span></span> <span data-ttu-id="c2f55-133">如需詳細資訊，請參閱 [Azure IoT 中樞價格](https://azure.microsoft.com/pricing/details/iot-hub/)。</span><span class="sxs-lookup"><span data-stu-id="c2f55-133">For more infomation, see [Azure IoT Hub pricing](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

> [!NOTE] 
> <span data-ttu-id="c2f55-134">您 IoT 中樞的名稱必須是全域唯一的。</span><span class="sxs-lookup"><span data-stu-id="c2f55-134">The name of your IoT hub must be globally unique.</span></span> <span data-ttu-id="c2f55-135">您的 Azure 訂用帳戶只能建立一個 F1 版本的 Azure IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="c2f55-135">You can create only one F1 edition of Azure IoT Hub under your Azure subscription.</span></span>

## <a name="register-pi-in-your-iot-hub"></a><span data-ttu-id="c2f55-136">在 IoT 中樞中登錄 Pi</span><span class="sxs-lookup"><span data-stu-id="c2f55-136">Register Pi in your IoT hub</span></span>
<span data-ttu-id="c2f55-137">每一個向/從 IoT 中樞傳送/接收訊息的裝置，都必須以唯一識別碼登錄。</span><span class="sxs-lookup"><span data-stu-id="c2f55-137">Each device that sends messages to your IoT hub and receives messages from your IoT hub must be registered with a unique ID.</span></span> <span data-ttu-id="c2f55-138">您將會使用 Azure CLI 來登錄 Pi，並建立自我簽署的 X.509 憑證來驗證裝置。</span><span class="sxs-lookup"><span data-stu-id="c2f55-138">You will use Azure CLI to register your Pi and create a self-signed X.509 certificate for device authentication.</span></span>

<span data-ttu-id="c2f55-139">執行以下命令：</span><span class="sxs-lookup"><span data-stu-id="c2f55-139">Run the following command:</span></span>

```bash
# For Windows command prompt
az iot device create --device-id myraspberrypi --hub-name {my hub name} --x509 --output-dir %USERPROFILE%\.iot-hub-getting-started
 
# For macOS or Ubuntu
az iot device create --device-id myraspberrypi --hub-name {my hub name} --x509 --output-dir ~/.iot-hub-getting-started
```

## <a name="summary"></a><span data-ttu-id="c2f55-140">摘要</span><span class="sxs-lookup"><span data-stu-id="c2f55-140">Summary</span></span>
<span data-ttu-id="c2f55-141">您已建立 IoT 中樞，並在 IoT 中樞中搭配裝置識別登錄 Pi。</span><span class="sxs-lookup"><span data-stu-id="c2f55-141">You've created an IoT hub and registered Pi with a device identity in your IoT hub.</span></span> <span data-ttu-id="c2f55-142">您已準備好了解如何從 Pi 傳送訊息至 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="c2f55-142">You're ready to learn how to send messages from Pi to your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c2f55-143">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c2f55-143">Next steps</span></span>
[<span data-ttu-id="c2f55-144">建立 Azure 函式應用程式和 Azure 儲存體帳戶以處理並儲存 IoT 中樞訊息</span><span class="sxs-lookup"><span data-stu-id="c2f55-144">Create an Azure function app and an Azure storage account to process and store IoT hub messages</span></span>](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md)
