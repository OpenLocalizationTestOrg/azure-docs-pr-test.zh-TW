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
ms.openlocfilehash: 5d2322268aa18f52f60c2833778323773ac4eec3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-azure-iot-hub-and-register-your-device"></a><span data-ttu-id="54327-103">建立 IoT 中樞並登錄您的裝置</span><span class="sxs-lookup"><span data-stu-id="54327-103">Create your Azure IoT hub and register your device</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="54327-104">將執行的作業</span><span class="sxs-lookup"><span data-stu-id="54327-104">What you will do</span></span>

- <span data-ttu-id="54327-105">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="54327-105">Create a resource group</span></span>
- <span data-ttu-id="54327-106">建立您的第一個 IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="54327-106">Create your first IoT hub</span></span>
- <span data-ttu-id="54327-107">在您的 IoT 中樞註冊您的裝置，使用 Azure CLI hello。</span><span class="sxs-lookup"><span data-stu-id="54327-107">Register your device in your IoT hub by using hello Azure CLI.</span></span> 

<span data-ttu-id="54327-108">當您在 IoT 中樞註冊您的裝置時，hello Azure IoT 中心服務會產生與 hello 服務您裝置 toouse tooauthenticate 的索引鍵。</span><span class="sxs-lookup"><span data-stu-id="54327-108">When you register your device in your IoT hub, hello Azure IoT Hub service generates a key for your device toouse tooauthenticate with hello service.</span></span> 

<span data-ttu-id="54327-109">如果您有任何問題，尋找解決方案上 hello[疑難排解頁面](iot-hub-gateway-kit-c-troubleshooting.md)。</span><span class="sxs-lookup"><span data-stu-id="54327-109">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="54327-110">學習目標</span><span class="sxs-lookup"><span data-stu-id="54327-110">What you will learn</span></span>

<span data-ttu-id="54327-111">在這一課，您將了解：</span><span class="sxs-lookup"><span data-stu-id="54327-111">In this lesson, you will learn:</span></span>

- <span data-ttu-id="54327-112">如何 toouse hello Azure CLI toocreate IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="54327-112">How toouse hello Azure CLI toocreate an IoT hub.</span></span>
- <span data-ttu-id="54327-113">如何 tooregister IoT 中樞中的裝置。</span><span class="sxs-lookup"><span data-stu-id="54327-113">How tooregister a device in an IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="54327-114">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="54327-114">What you need</span></span>

- <span data-ttu-id="54327-115">有效的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="54327-115">An active Azure subscription.</span></span> <span data-ttu-id="54327-116">如果您沒有 Azure 帳戶，只需要幾分鐘的時間就可以建立[免費的 Azure 試用帳戶](http://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="54327-116">If you don't have an Azure account, you can create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>
- <span data-ttu-id="54327-117">您應該有的 hello Azure CLI 安裝。</span><span class="sxs-lookup"><span data-stu-id="54327-117">You should have hello Azure CLI installed.</span></span>

## <a name="create-an-iot-hub"></a><span data-ttu-id="54327-118">建立 IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="54327-118">Create an IoT hub</span></span>

<span data-ttu-id="54327-119">toocreate IoT 中樞，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="54327-119">toocreate an IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="54327-120">登入 tooyour Azure 帳戶執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="54327-120">Sign in tooyour Azure account by running hello following command:</span></span>

   ```bash
   az login
   ```

   <span data-ttu-id="54327-121">成功登入之後，系統會列出所有可用的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="54327-121">All your available subscriptions will be listed after a successful sign-in.</span></span>

2. <span data-ttu-id="54327-122">設定 hello 預設您藉由執行下列命令的 hello 想 toouse 的 Azure 訂用帳戶：</span><span class="sxs-lookup"><span data-stu-id="54327-122">Set hello default Azure subscription that you want toouse by running hello following command:</span></span>

   ```bash
   az account set --subscription {subscription id or name}
   ```

   <span data-ttu-id="54327-123">`subscription ID or name`可以找到 hello 輸出中的 hello`az login`或 hello`az account list`命令。</span><span class="sxs-lookup"><span data-stu-id="54327-123">`subscription ID or name` can be found in hello output of hello `az login` or hello `az account list` command.</span></span>

3. <span data-ttu-id="54327-124">執行下列命令的 hello 註冊 hello 提供者。</span><span class="sxs-lookup"><span data-stu-id="54327-124">Register hello provider by running hello following command.</span></span> <span data-ttu-id="54327-125">資源提供者是為應用程式提供資源的服務。</span><span class="sxs-lookup"><span data-stu-id="54327-125">Resource providers are services that provide resources for your application.</span></span> <span data-ttu-id="54327-126">您必須先註冊 hello 提供者，才能部署 hello hello 提供者提供的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="54327-126">You must register hello provider before you can deploy hello Azure resource that hello provider offers.</span></span>

   ```bash
   az provider register -n "Microsoft.Devices"
   ```

4. <span data-ttu-id="54327-127">建立資源群組名稱為`iot-gateway`藉由執行下列命令的 hello hello 美國西部區域中：</span><span class="sxs-lookup"><span data-stu-id="54327-127">Create a resource group named `iot-gateway` in hello West US region by running hello following command:</span></span>

   ```bash
   az group create --name iot-gateway --location westus
   ```
   
   <span data-ttu-id="54327-128">`westus`是您在建立資源群組的 hello 位置。</span><span class="sxs-lookup"><span data-stu-id="54327-128">`westus` is hello location you create your resource group.</span></span> <span data-ttu-id="54327-129">如果您想 toouse 另一個位置，您可以執行`az account list-locations -o table`toosee 所有 hello Azure 支援的位置。</span><span class="sxs-lookup"><span data-stu-id="54327-129">If you want toouse another location, you can run `az account list-locations -o table` toosee all hello locations Azure supports.</span></span>

5. <span data-ttu-id="54327-130">在 hello 建立 IoT 中樞`iot-gateway`資源群組，藉由執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="54327-130">Create an IoT hub in hello `iot-gateway` resource group by running hello following command:</span></span>

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-gateway
   ```

<span data-ttu-id="54327-131">根據預設，hello 工具會在 hello 可用的定價層中，建立 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="54327-131">By default, hello tool creates an IoT Hub in hello Free pricing tier.</span></span> <span data-ttu-id="54327-132">如需詳細資訊，請參閱 [Azure IoT 中樞價格](https://azure.microsoft.com/pricing/details/iot-hub/)。</span><span class="sxs-lookup"><span data-stu-id="54327-132">For more infomation, see [Azure IoT Hub pricing](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

> [!NOTE]
> <span data-ttu-id="54327-133">IoT 中樞 hello 名稱必須是全域唯一的。</span><span class="sxs-lookup"><span data-stu-id="54327-133">hello name of your IoT hub must be globally unique.</span></span> <span data-ttu-id="54327-134">您的 Azure 訂用帳戶只能建立一個 F1 版本的 Azure IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="54327-134">You can create only one F1 edition of Azure Iot Hub under your Azure subscription.</span></span>

## <a name="register-your-device-in-your-iot-hub"></a><span data-ttu-id="54327-135">在 IoT 中樞登錄您的裝置</span><span class="sxs-lookup"><span data-stu-id="54327-135">Register your device in your IoT hub</span></span>

<span data-ttu-id="54327-136">傳送訊息 tooyour IoT 中樞和接收訊息，或從 IoT 中樞的每個裝置必須註冊並提供唯一的識別碼。</span><span class="sxs-lookup"><span data-stu-id="54327-136">Each device that sends messages tooyour IoT hub and receives messages from your IoT hub must be registered with a unique ID.</span></span>
<span data-ttu-id="54327-137">執行下列命令在 Azure IoT 中樞中登錄您的裝置：</span><span class="sxs-lookup"><span data-stu-id="54327-137">Register your device in your IoT hub by running following command:</span></span>

```bash
az iot device create --device-id mydevice --hub-name {my hub name} --resource-group iot-gateway
```

## <a name="summary"></a><span data-ttu-id="54327-138">摘要</span><span class="sxs-lookup"><span data-stu-id="54327-138">Summary</span></span>

<span data-ttu-id="54327-139">您已建立 IoT 中樞，並在 IoT 中樞中登錄您的邏輯裝置及裝置身分識別。</span><span class="sxs-lookup"><span data-stu-id="54327-139">You've created an IoT hub and registered your logical device with a device identity in your IoT hub.</span></span> <span data-ttu-id="54327-140">您已準備好 toolearn tooconfigure 並從您的實體裝置 tooyour IoT 中樞 hello 中執行的閘道範例應用程式 toosend 資料的雲端。</span><span class="sxs-lookup"><span data-stu-id="54327-140">You're ready toolearn how tooconfigure and run a gateway sample application toosend data from your physical device tooyour IoT hub in hello cloud.</span></span>

## <a name="next-steps"></a><span data-ttu-id="54327-141">後續步驟</span><span class="sxs-lookup"><span data-stu-id="54327-141">Next steps</span></span>
[<span data-ttu-id="54327-142">設定和執行 BLE 範例應用程式</span><span class="sxs-lookup"><span data-stu-id="54327-142">Configure and run a BLE sample app</span></span>](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md)