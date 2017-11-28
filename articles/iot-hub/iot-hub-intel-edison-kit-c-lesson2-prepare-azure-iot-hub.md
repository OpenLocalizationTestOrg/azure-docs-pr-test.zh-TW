---
title: "Connect Intel Edison (C) tooAzure IoT-第 2 課： 註冊裝置 |Microsoft 文件"
description: "建立資源群組、 建立 Azure IoT 中樞，並註冊 Edison hello Azure IoT 中樞中使用 Azure CLI hello。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: 
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: 80bfc3cd-a1fc-4775-8994-d8033381dd3d
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 9635e916425883d65793d0ed46843ab49b3f35ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-iot-hub-and-register-intel-edison"></a><span data-ttu-id="0d30d-103">建立 IoT 中樞並登錄 Intel Edison</span><span class="sxs-lookup"><span data-stu-id="0d30d-103">Create your IoT hub and register Intel Edison</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="0d30d-104">將執行的作業</span><span class="sxs-lookup"><span data-stu-id="0d30d-104">What you will do</span></span>
* <span data-ttu-id="0d30d-105">建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="0d30d-105">Create a resource group.</span></span>
* <span data-ttu-id="0d30d-106">建立您的 Azure IoT 中樞 hello 資源群組中。</span><span class="sxs-lookup"><span data-stu-id="0d30d-106">Create your Azure IoT hub in hello resource group.</span></span>
* <span data-ttu-id="0d30d-107">使用 hello Azure 命令列介面 (Azure CLI)，以新增 Intel Edison toohello Azure IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="0d30d-107">Add Intel Edison toohello Azure IoT hub by using hello Azure command-line interface (Azure CLI).</span></span>

<span data-ttu-id="0d30d-108">當您使用 hello Azure CLI tooadd Edison tooyour IoT 中樞時，hello 服務就會產生與 hello 服務 Edison tooauthenticate 的索引鍵。</span><span class="sxs-lookup"><span data-stu-id="0d30d-108">When you use hello Azure CLI tooadd Edison tooyour IoT hub, hello service generates a key for Edison tooauthenticate with hello service.</span></span> <span data-ttu-id="0d30d-109">如果您有任何問題，尋找解決方案上 hello[疑難排解頁面][troubleshooting]。</span><span class="sxs-lookup"><span data-stu-id="0d30d-109">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="0d30d-110">學習目標</span><span class="sxs-lookup"><span data-stu-id="0d30d-110">What you will learn</span></span>
<span data-ttu-id="0d30d-111">在本文中，您將了解：</span><span class="sxs-lookup"><span data-stu-id="0d30d-111">In this article, you will learn:</span></span>
* <span data-ttu-id="0d30d-112">如何 toouse hello Azure CLI toocreate IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="0d30d-112">How toouse hello Azure CLI toocreate an IoT hub.</span></span>
* <span data-ttu-id="0d30d-113">如何 toocreate Edison 裝置身分識別在您的 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="0d30d-113">How toocreate a device identity for Edison in your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="0d30d-114">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="0d30d-114">What you need</span></span>
* <span data-ttu-id="0d30d-115">一個 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="0d30d-115">An Azure account.</span></span> <span data-ttu-id="0d30d-116">如果您沒有 Azure 帳戶，請花幾分鐘的時間建立[免費的 Azure 試用帳戶](http://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="0d30d-116">If you don't have an Azure account, create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>
* <span data-ttu-id="0d30d-117">您應該有的 hello Azure CLI 安裝。</span><span class="sxs-lookup"><span data-stu-id="0d30d-117">You should have hello Azure CLI installed.</span></span>

## <a name="create-your-iot-hub"></a><span data-ttu-id="0d30d-118">建立 IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="0d30d-118">Create your IoT hub</span></span>
<span data-ttu-id="0d30d-119">Azure IoT 中樞可以協助您連接、監視並管理數以百萬計的 IoT 資產。</span><span class="sxs-lookup"><span data-stu-id="0d30d-119">Azure IoT Hub helps you connect, monitor, and manage millions of IoT assets.</span></span> <span data-ttu-id="0d30d-120">toocreate IoT 中樞，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="0d30d-120">toocreate your IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="0d30d-121">登入 tooyour Azure 帳戶執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="0d30d-121">Sign in tooyour Azure account by running hello following command:</span></span>

   ```bash
   az login
   ```

   <span data-ttu-id="0d30d-122">成功登入之後，系統將會列出所有可用的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="0d30d-122">All your available subscriptions are listed after a successful sign-in.</span></span>

2. <span data-ttu-id="0d30d-123">設定您藉由執行下列命令的 hello 想 toouse hello 預設訂用帳戶：</span><span class="sxs-lookup"><span data-stu-id="0d30d-123">Set hello default subscription that you want toouse by running hello following command:</span></span>

   ```bash
   az account set --subscription {subscription id or name}
   ```

   <span data-ttu-id="0d30d-124">`subscription ID or name`可以找到 hello 輸出中的 hello`az login`或 hello`az account list`命令。</span><span class="sxs-lookup"><span data-stu-id="0d30d-124">`subscription ID or name` can be found in hello output of hello `az login` or hello `az account list` command.</span></span>

3. <span data-ttu-id="0d30d-125">執行下列命令的 hello 註冊 hello 提供者。</span><span class="sxs-lookup"><span data-stu-id="0d30d-125">Register hello provider by running hello following command.</span></span> <span data-ttu-id="0d30d-126">資源提供者是為應用程式提供資源的服務。</span><span class="sxs-lookup"><span data-stu-id="0d30d-126">Resource providers are services that provide resources for your application.</span></span> <span data-ttu-id="0d30d-127">您必須先註冊 hello 提供者，才能部署 hello hello 提供者提供的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="0d30d-127">You must register hello provider before you can deploy hello Azure resource that hello provider offers.</span></span>

   ```bash
   az provider register -n "Microsoft.Devices"
   ```
4. <span data-ttu-id="0d30d-128">藉由執行下列命令的 hello 的 hello 美國西部地區中建立資源群組名稱 iot 範例：</span><span class="sxs-lookup"><span data-stu-id="0d30d-128">Create a resource group named iot-sample in hello West US region by running hello following command:</span></span>

   ```bash
   az group create --name iot-sample --location westus
   ```

   <span data-ttu-id="0d30d-129">`westus`是您在建立資源群組的 hello 位置。</span><span class="sxs-lookup"><span data-stu-id="0d30d-129">`westus` is hello location you create your resource group.</span></span> <span data-ttu-id="0d30d-130">如果您想 toouse 另一個位置，您可以執行`az account list-locations -o table`toosee 所有 hello Azure 支援的位置。</span><span class="sxs-lookup"><span data-stu-id="0d30d-130">If you want toouse another location, you can run `az account list-locations -o table` toosee all hello locations Azure supports.</span></span>

5. <span data-ttu-id="0d30d-131">建立 IoT 中樞 hello iot 範例資源群組中，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="0d30d-131">Create an IoT hub in hello iot-sample resource group by running hello following command:</span></span>

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-sample
   ```

<span data-ttu-id="0d30d-132">根據預設，hello 工具會在 hello 可用的定價層中，建立 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="0d30d-132">By default, hello tool creates an IoT Hub in hello Free pricing tier.</span></span> <span data-ttu-id="0d30d-133">如需詳細資訊，請參閱 [Azure IoT 中樞價格](https://azure.microsoft.com/pricing/details/iot-hub/)。</span><span class="sxs-lookup"><span data-stu-id="0d30d-133">For more infomation, see [Azure IoT Hub pricing](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

> [!NOTE] 
> <span data-ttu-id="0d30d-134">IoT 中樞 hello 名稱必須是全域唯一的。</span><span class="sxs-lookup"><span data-stu-id="0d30d-134">hello name of your IoT hub must be globally unique.</span></span>
> <span data-ttu-id="0d30d-135">您的 Azure 訂用帳戶只能建立一個 F1 版本的 Azure IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="0d30d-135">You can create only one F1 edition of Azure IoT Hub under your Azure subscription.</span></span>


## <a name="register-edison-in-your-iot-hub"></a><span data-ttu-id="0d30d-136">在 IoT 中樞中登錄 Edison</span><span class="sxs-lookup"><span data-stu-id="0d30d-136">Register Edison in your IoT hub</span></span>
<span data-ttu-id="0d30d-137">傳送訊息 tooyour IoT 中樞和接收訊息，或從 IoT 中樞的每個裝置必須註冊並提供唯一的識別碼。</span><span class="sxs-lookup"><span data-stu-id="0d30d-137">Each device that sends messages tooyour IoT hub and receives messages from your IoT hub must be registered with a unique ID.</span></span>

<span data-ttu-id="0d30d-138">執行下列命令在 Azure IoT 中樞中登錄 Edison：</span><span class="sxs-lookup"><span data-stu-id="0d30d-138">Register Edison in your IoT hub by running following command:</span></span>

```bash
az iot device create --device-id myinteledison --hub-name {my hub name}
```

## <a name="summary"></a><span data-ttu-id="0d30d-139">摘要</span><span class="sxs-lookup"><span data-stu-id="0d30d-139">Summary</span></span>
<span data-ttu-id="0d30d-140">您已建立 IoT 中樞，並在 IoT 中樞中搭配裝置識別登錄 Edison。</span><span class="sxs-lookup"><span data-stu-id="0d30d-140">You've created an IoT hub and registered Edison with a device identity in your IoT hub.</span></span> <span data-ttu-id="0d30d-141">您已準備好 toolearn toosend 從 Edison tooyour IoT 中樞的訊息。</span><span class="sxs-lookup"><span data-stu-id="0d30d-141">You're ready toolearn how toosend messages from Edison tooyour IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0d30d-142">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0d30d-142">Next steps</span></span>
<span data-ttu-id="0d30d-143">[建立 Azure 的函式應用程式與 Azure 儲存體帳戶 tooprocess 和市集 IoT 中樞訊息][process-and-store-iot-hub-messages]。</span><span class="sxs-lookup"><span data-stu-id="0d30d-143">[Create an Azure function app and an Azure Storage account tooprocess and store IoT hub messages][process-and-store-iot-hub-messages].</span></span>


<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-intel-edison-kit-c-lesson3-deploy-resource-manager-template.md