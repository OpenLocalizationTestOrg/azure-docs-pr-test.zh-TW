---
title: "將 Arduino 連線至 Azure IoT - 第 2 課：註冊裝置 | Microsoft Docs"
description: "使用 Azure CLI 建立資源群組、建立 Azure IoT 中樞，並在 Azure IoT 中樞登錄 Adafruit Feather M0 WiFi。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "將 arduino 連線至雲端, azure iot 中樞, 物聯網雲端, azure iot 中樞建立裝置, arduino 雲端"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 5edc690b-7a1d-4ebc-b011-ff27bfffe6e8
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: c5ad5e900671c7cedd3cdad2c2aa345315de223b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-your-iot-hub-and-register-your-adafruit-feather-m0-wifi-arduino-board"></a><span data-ttu-id="8d0d8-104">建立 IoT 中樞並登錄 Adafruit Feather M0 WiFi Arduino 面板</span><span class="sxs-lookup"><span data-stu-id="8d0d8-104">Create your IoT hub and register your Adafruit Feather M0 WiFi Arduino board</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="8d0d8-105">將執行的作業</span><span class="sxs-lookup"><span data-stu-id="8d0d8-105">What you will do</span></span>
* <span data-ttu-id="8d0d8-106">建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="8d0d8-106">Create a resource group.</span></span>
* <span data-ttu-id="8d0d8-107">在資源群組中建立 Azure IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="8d0d8-107">Create your Azure IoT hub in the resource group.</span></span>
* <span data-ttu-id="8d0d8-108">使用 Azure 命令列介面 (Azure CLI)，將 Arduino 面板新增至 Azure IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="8d0d8-108">Add your Arduino board to the Azure IoT hub by using the Azure command-line interface (Azure CLI).</span></span>

<span data-ttu-id="8d0d8-109">當您使用 Azure CLI 將 Arduino 面板新增至 IoT 中樞時，服務將會為您的 Arduino 面板產生一組金鑰，以向服務進行驗證。</span><span class="sxs-lookup"><span data-stu-id="8d0d8-109">When you use the Azure CLI to add your Arduino board to your IoT hub, the service generates a key for your Arduino board to authenticate with the service.</span></span> <span data-ttu-id="8d0d8-110">如果您有任何問題，請在[疑難排解頁面][troubleshoot]尋求解決方案。</span><span class="sxs-lookup"><span data-stu-id="8d0d8-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshoot].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="8d0d8-111">學習目標</span><span class="sxs-lookup"><span data-stu-id="8d0d8-111">What you will learn</span></span>
<span data-ttu-id="8d0d8-112">在本文中，您將了解：</span><span class="sxs-lookup"><span data-stu-id="8d0d8-112">In this article, you will learn:</span></span>
* <span data-ttu-id="8d0d8-113">如何使用 Azure CLI 建立 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="8d0d8-113">How to use the Azure CLI to create an IoT hub.</span></span>
* <span data-ttu-id="8d0d8-114">如何在 IoT 中樞中為您的 Arduino 面板建立裝置識別。</span><span class="sxs-lookup"><span data-stu-id="8d0d8-114">How to create a device identity for your Arduino board in your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="8d0d8-115">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="8d0d8-115">What you need</span></span>
* <span data-ttu-id="8d0d8-116">一個 Azure 帳戶</span><span class="sxs-lookup"><span data-stu-id="8d0d8-116">An Azure account</span></span>
* <span data-ttu-id="8d0d8-117">一部已安裝 Azure CLI 的電腦</span><span class="sxs-lookup"><span data-stu-id="8d0d8-117">A computer with the Azure CLI installed</span></span>

## <a name="create-your-iot-hub"></a><span data-ttu-id="8d0d8-118">建立 IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="8d0d8-118">Create your IoT hub</span></span>
<span data-ttu-id="8d0d8-119">Azure IoT 中樞可以協助您連接、監視並管理數以百萬計的 IoT 資產。</span><span class="sxs-lookup"><span data-stu-id="8d0d8-119">Azure IoT Hub helps you connect, monitor, and manage millions of IoT assets.</span></span> <span data-ttu-id="8d0d8-120">若要建立 IoT 中樞，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="8d0d8-120">To create your IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="8d0d8-121">執行下列命令來登入您的 Azure 帳戶：</span><span class="sxs-lookup"><span data-stu-id="8d0d8-121">Sign in to your Azure account by running the following command:</span></span>

   ```bash
   az login
   ```

   <span data-ttu-id="8d0d8-122">成功登入之後，系統將會列出所有可用的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="8d0d8-122">All your available subscriptions are listed after a successful sign-in.</span></span>

2. <span data-ttu-id="8d0d8-123">執行下列命令來設定您想要使用的預設訂用帳戶：</span><span class="sxs-lookup"><span data-stu-id="8d0d8-123">Set the default subscription that you want to use by running the following command:</span></span>

   ```bash
   az account set --subscription {subscription id or name}
   ```

   <span data-ttu-id="8d0d8-124">`subscription ID or name` 可在 `az login` 或 `az account list` 命令的輸出中找到。</span><span class="sxs-lookup"><span data-stu-id="8d0d8-124">`subscription ID or name` can be found in the output of the `az login` or the `az account list` command.</span></span>

3. <span data-ttu-id="8d0d8-125">執行下列命令來登錄提供者。</span><span class="sxs-lookup"><span data-stu-id="8d0d8-125">Register the provider by running the following command.</span></span> <span data-ttu-id="8d0d8-126">資源提供者是為應用程式提供資源的服務。</span><span class="sxs-lookup"><span data-stu-id="8d0d8-126">Resource providers are services that provide resources for your application.</span></span> <span data-ttu-id="8d0d8-127">您必須先登錄提供者，才能部署該提供者所提供的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="8d0d8-127">You must register the provider before you can deploy the Azure resource that the provider offers.</span></span>

   ```bash
   az provider register -n "Microsoft.Devices"
   ```
4. <span data-ttu-id="8d0d8-128">執行下列命令來在美國西部區域建立名為 iot-sample 的資源群組：</span><span class="sxs-lookup"><span data-stu-id="8d0d8-128">Create a resource group named iot-sample in the West US region by running the following command:</span></span>

   ```bash
   az group create --name iot-sample --location westus
   ```

   <span data-ttu-id="8d0d8-129">`westus` 是資源群組建立所在的位置。</span><span class="sxs-lookup"><span data-stu-id="8d0d8-129">`westus` is the location you create your resource group.</span></span> <span data-ttu-id="8d0d8-130">如果您想要使用另一個位置，您可以執行 `az account list-locations -o table` 來查看 Azure 支援的所有位置。</span><span class="sxs-lookup"><span data-stu-id="8d0d8-130">If you want to use another location, you can run `az account list-locations -o table` to see all the locations Azure supports.</span></span>

5. <span data-ttu-id="8d0d8-131">執行下列命令來在 iot-sample 資源群組中建立 IoT 中樞：</span><span class="sxs-lookup"><span data-stu-id="8d0d8-131">Create an IoT hub in the iot-sample resource group by running the following command:</span></span>

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-sample
   ```

<span data-ttu-id="8d0d8-132">根據預設，此工具會在免費定價層建立 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="8d0d8-132">By default, the tool creates an IoT Hub in the Free pricing tier.</span></span> <span data-ttu-id="8d0d8-133">如需詳細資訊，請參閱 [Azure IoT 中樞價格](https://azure.microsoft.com/pricing/details/iot-hub/)。</span><span class="sxs-lookup"><span data-stu-id="8d0d8-133">For more infomation, see [Azure IoT Hub pricing](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

> [!NOTE]
> <span data-ttu-id="8d0d8-134">您 IoT 中樞的名稱必須是全域唯一的。</span><span class="sxs-lookup"><span data-stu-id="8d0d8-134">The name of your IoT hub must be globally unique.</span></span>
> <span data-ttu-id="8d0d8-135">您的 Azure 訂用帳戶只能建立一個 F1 版本的 Azure IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="8d0d8-135">You can create only one F1 edition of Azure IoT Hub under your Azure subscription.</span></span>

## <a name="register-your-arduino-board-in-your-iot-hub"></a><span data-ttu-id="8d0d8-136">在 IoT 中樞登錄您的 Arduino 面板</span><span class="sxs-lookup"><span data-stu-id="8d0d8-136">Register your Arduino board in your IoT hub</span></span>
<span data-ttu-id="8d0d8-137">每一個向/從 IoT 中樞傳送/接收訊息的裝置，都必須以唯一識別碼登錄。</span><span class="sxs-lookup"><span data-stu-id="8d0d8-137">Each device that sends messages to your IoT hub and receives messages from your IoT hub must be registered with a unique ID.</span></span>

<span data-ttu-id="8d0d8-138">執行下列命令在 Azure IoT 中樞中登錄您的 Arduino 面板：</span><span class="sxs-lookup"><span data-stu-id="8d0d8-138">Register your Arduino board in your IoT hub by running following command:</span></span>

```bash
az iot device create --device-id mym0wifi --hub-name {my hub name}
```

## <a name="summary"></a><span data-ttu-id="8d0d8-139">摘要</span><span class="sxs-lookup"><span data-stu-id="8d0d8-139">Summary</span></span>
<span data-ttu-id="8d0d8-140">您已建立 IoT 中樞，並在 IoT 中樞中登錄您的 Arduino 面板及裝置身分識別。</span><span class="sxs-lookup"><span data-stu-id="8d0d8-140">You've created an IoT hub and registered your Arduino board with a device identity in your IoT hub.</span></span> <span data-ttu-id="8d0d8-141">您已準備好了解如何從 Arduino 面板傳送訊息至 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="8d0d8-141">You're ready to learn how to send messages from your Arduino board to your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8d0d8-142">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8d0d8-142">Next steps</span></span>
<span data-ttu-id="8d0d8-143">[建立 Azure 函式應用程式和 Azure 儲存體帳戶以處理並儲存 IoT 中樞訊息][process-and-store-iot-hub-messages]。</span><span class="sxs-lookup"><span data-stu-id="8d0d8-143">[Create an Azure function app and an Azure Storage account to process and store IoT hub messages][process-and-store-iot-hub-messages].</span></span>


<!-- Images and links -->

[troubleshoot]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-deploy-resource-manager-template.md