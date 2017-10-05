---
title: "SensorTag 裝置與 Azure IoT 閘道 - 第 2 課：登錄裝置 | Microsoft Docs"
description: 
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "azure iot 中樞, 物聯網雲端, azure iot 中樞建立裝置, ti sensortag, ti ble"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 2c18f5ae-e39a-48ae-a9fe-04bb595740a0
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 685a479583f5f11f57bef22dc5881285bb1f70d0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-your-azure-iot-hub-and-register-your-device"></a><span data-ttu-id="3b4e1-103">建立 IoT 中樞並登錄您的裝置</span><span class="sxs-lookup"><span data-stu-id="3b4e1-103">Create your Azure IoT hub and register your device</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="3b4e1-104">將執行的作業</span><span class="sxs-lookup"><span data-stu-id="3b4e1-104">What you will do</span></span>

- <span data-ttu-id="3b4e1-105">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="3b4e1-105">Create a resource group</span></span>
- <span data-ttu-id="3b4e1-106">建立您的第一個 IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="3b4e1-106">Create your first IoT hub</span></span>
- <span data-ttu-id="3b4e1-107">使用 Azure CLI 在 IoT 中樞登錄您的裝置。</span><span class="sxs-lookup"><span data-stu-id="3b4e1-107">Register your device in your IoT hub by using the Azure CLI.</span></span> 

<span data-ttu-id="3b4e1-108">當您在 IoT 中樞登錄您的裝置時，Azure IoT 中樞服務將會為您的裝置產生一個金鑰，用以向服務進行驗證。</span><span class="sxs-lookup"><span data-stu-id="3b4e1-108">When you register your device in your IoT hub, the Azure IoT Hub service generates a key for your device to use to authenticate with the service.</span></span> 

<span data-ttu-id="3b4e1-109">如果您有任何問題，請在[疑難排解頁面](iot-hub-gateway-kit-c-troubleshooting.md)尋求解決方案。</span><span class="sxs-lookup"><span data-stu-id="3b4e1-109">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="3b4e1-110">學習目標</span><span class="sxs-lookup"><span data-stu-id="3b4e1-110">What you will learn</span></span>

<span data-ttu-id="3b4e1-111">在這一課，您將了解：</span><span class="sxs-lookup"><span data-stu-id="3b4e1-111">In this lesson, you will learn:</span></span>

- <span data-ttu-id="3b4e1-112">如何使用 Azure CLI 建立 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="3b4e1-112">How to use the Azure CLI to create an IoT hub.</span></span>
- <span data-ttu-id="3b4e1-113">如何在 IoT 中樞登錄裝置。</span><span class="sxs-lookup"><span data-stu-id="3b4e1-113">How to register a device in an IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="3b4e1-114">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="3b4e1-114">What you need</span></span>

- <span data-ttu-id="3b4e1-115">有效的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="3b4e1-115">An active Azure subscription.</span></span> <span data-ttu-id="3b4e1-116">如果您沒有 Azure 帳戶，只需要幾分鐘的時間就可以建立[免費的 Azure 試用帳戶](http://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="3b4e1-116">If you don't have an Azure account, you can create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>
- <span data-ttu-id="3b4e1-117">您應該已經安裝 Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="3b4e1-117">You should have the Azure CLI installed.</span></span>

## <a name="create-an-iot-hub"></a><span data-ttu-id="3b4e1-118">建立 IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="3b4e1-118">Create an IoT hub</span></span>

<span data-ttu-id="3b4e1-119">若要建立 IoT 中樞，遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="3b4e1-119">To create an IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="3b4e1-120">執行下列命令來登入您的 Azure 帳戶：</span><span class="sxs-lookup"><span data-stu-id="3b4e1-120">Sign in to your Azure account by running the following command:</span></span>

   ```bash
   az login
   ```

   <span data-ttu-id="3b4e1-121">成功登入之後，系統會列出所有可用的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="3b4e1-121">All your available subscriptions will be listed after a successful sign-in.</span></span>

2. <span data-ttu-id="3b4e1-122">執行下列命令來設定您想要使用的預設 Azure 訂用帳戶：</span><span class="sxs-lookup"><span data-stu-id="3b4e1-122">Set the default Azure subscription that you want to use by running the following command:</span></span>

   ```bash
   az account set --subscription {subscription id or name}
   ```

   <span data-ttu-id="3b4e1-123">`subscription ID or name` 可在 `az login` 或 `az account list` 命令的輸出中找到。</span><span class="sxs-lookup"><span data-stu-id="3b4e1-123">`subscription ID or name` can be found in the output of the `az login` or the `az account list` command.</span></span>

3. <span data-ttu-id="3b4e1-124">執行下列命令來登錄提供者。</span><span class="sxs-lookup"><span data-stu-id="3b4e1-124">Register the provider by running the following command.</span></span> <span data-ttu-id="3b4e1-125">資源提供者是為應用程式提供資源的服務。</span><span class="sxs-lookup"><span data-stu-id="3b4e1-125">Resource providers are services that provide resources for your application.</span></span> <span data-ttu-id="3b4e1-126">您必須先登錄提供者，才能部署該提供者所提供的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="3b4e1-126">You must register the provider before you can deploy the Azure resource that the provider offers.</span></span>

   ```bash
   az provider register -n "Microsoft.Devices"
   ```

4. <span data-ttu-id="3b4e1-127">執行下列命令在美國西部區域建立名為 `iot-gateway` 的資源群組：</span><span class="sxs-lookup"><span data-stu-id="3b4e1-127">Create a resource group named `iot-gateway` in the West US region by running the following command:</span></span>

   ```bash
   az group create --name iot-gateway --location westus
   ```
   
   <span data-ttu-id="3b4e1-128">`westus` 是資源群組建立所在的位置。</span><span class="sxs-lookup"><span data-stu-id="3b4e1-128">`westus` is the location you create your resource group.</span></span> <span data-ttu-id="3b4e1-129">如果您想要使用另一個位置，您可以執行 `az account list-locations -o table` 來查看 Azure 支援的所有位置。</span><span class="sxs-lookup"><span data-stu-id="3b4e1-129">If you want to use another location, you can run `az account list-locations -o table` to see all the locations Azure supports.</span></span>

5. <span data-ttu-id="3b4e1-130">執行下列命令在 `iot-gateway` 資源群組中建立 IoT 中樞：</span><span class="sxs-lookup"><span data-stu-id="3b4e1-130">Create an IoT hub in the `iot-gateway` resource group by running the following command:</span></span>

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-gateway
   ```

<span data-ttu-id="3b4e1-131">根據預設，此工具會在免費定價層建立 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="3b4e1-131">By default, the tool creates an IoT Hub in the Free pricing tier.</span></span> <span data-ttu-id="3b4e1-132">如需詳細資訊，請參閱 [Azure IoT 中樞價格](https://azure.microsoft.com/pricing/details/iot-hub/)。</span><span class="sxs-lookup"><span data-stu-id="3b4e1-132">For more infomation, see [Azure IoT Hub pricing](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

> [!NOTE]
> <span data-ttu-id="3b4e1-133">您 IoT 中樞的名稱必須是全域唯一的。</span><span class="sxs-lookup"><span data-stu-id="3b4e1-133">The name of your IoT hub must be globally unique.</span></span> <span data-ttu-id="3b4e1-134">您的 Azure 訂用帳戶只能建立一個 F1 版本的 Azure IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="3b4e1-134">You can create only one F1 edition of Azure Iot Hub under your Azure subscription.</span></span>

## <a name="register-your-device-in-your-iot-hub"></a><span data-ttu-id="3b4e1-135">在 IoT 中樞登錄您的裝置</span><span class="sxs-lookup"><span data-stu-id="3b4e1-135">Register your device in your IoT hub</span></span>

<span data-ttu-id="3b4e1-136">每一個向/從 IoT 中樞傳送/接收訊息的裝置，都必須以唯一識別碼登錄。</span><span class="sxs-lookup"><span data-stu-id="3b4e1-136">Each device that sends messages to your IoT hub and receives messages from your IoT hub must be registered with a unique ID.</span></span>
<span data-ttu-id="3b4e1-137">執行下列命令在 Azure IoT 中樞中登錄您的裝置：</span><span class="sxs-lookup"><span data-stu-id="3b4e1-137">Register your device in your IoT hub by running following command:</span></span>

```bash
az iot device create --device-id mydevice --hub-name {my hub name} --resource-group iot-gateway
```

## <a name="summary"></a><span data-ttu-id="3b4e1-138">摘要</span><span class="sxs-lookup"><span data-stu-id="3b4e1-138">Summary</span></span>

<span data-ttu-id="3b4e1-139">您已建立 IoT 中樞，並在 IoT 中樞中登錄您的邏輯裝置及裝置身分識別。</span><span class="sxs-lookup"><span data-stu-id="3b4e1-139">You've created an IoT hub and registered your logical device with a device identity in your IoT hub.</span></span> <span data-ttu-id="3b4e1-140">您可以開始了解如何設定及執行閘道器範例應用程式，將資料從您的實體裝置傳送至您位於雲端的 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="3b4e1-140">You're ready to learn how to configure and run a gateway sample application to send data from your physical device to your IoT hub in the cloud.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3b4e1-141">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3b4e1-141">Next steps</span></span>
[<span data-ttu-id="3b4e1-142">設定和執行 BLE 範例應用程式</span><span class="sxs-lookup"><span data-stu-id="3b4e1-142">Configure and run a BLE sample app</span></span>](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md)