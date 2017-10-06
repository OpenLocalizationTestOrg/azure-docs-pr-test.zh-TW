---
title: "Connect Raspberry Pi (C) tooAzure IoT-第 2 課： 註冊裝置 |Microsoft 文件"
description: "建立資源群組、 建立 Azure IoT 中樞，並註冊 Pi hello Azure IoT 中樞中使用 Azure CLI hello。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "raspberry pi 雲端, pi 雲端連線"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: 4bcfb071-b3ae-48cc-8ea5-7e7434732287
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 473658c5a8e1e0d4cfced0efafbad2640a1e0696
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-iot-hub-and-register-raspberry-pi-3"></a><span data-ttu-id="86a94-104">建立 IoT 中樞並登錄 Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="86a94-104">Create your IoT hub and register Raspberry Pi 3</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="86a94-105">將執行的作業</span><span class="sxs-lookup"><span data-stu-id="86a94-105">What you will do</span></span>
* <span data-ttu-id="86a94-106">建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="86a94-106">Create a resource group.</span></span>
* <span data-ttu-id="86a94-107">建立您的 Azure IoT 中樞 hello 資源群組中。</span><span class="sxs-lookup"><span data-stu-id="86a94-107">Create your Azure IoT hub in hello resource group.</span></span>
* <span data-ttu-id="86a94-108">使用 hello Azure 命令列介面 (Azure CLI)，以新增覆盆子 Pi 3 toohello Azure IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="86a94-108">Add Raspberry Pi 3 toohello Azure IoT hub by using hello Azure command-line interface (Azure CLI).</span></span>

<span data-ttu-id="86a94-109">當您使用 hello Azure CLI tooadd Pi tooyour IoT 中樞時，hello 服務就會產生與 hello 服務 Pi tooauthenticate 的索引鍵。</span><span class="sxs-lookup"><span data-stu-id="86a94-109">When you use hello Azure CLI tooadd Pi tooyour IoT hub, hello service generates a key for Pi tooauthenticate with hello service.</span></span> <span data-ttu-id="86a94-110">如果您有任何問題，尋找解決方案上 hello[疑難排解頁面](iot-hub-raspberry-pi-kit-c-troubleshooting.md)。</span><span class="sxs-lookup"><span data-stu-id="86a94-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="86a94-111">學習目標</span><span class="sxs-lookup"><span data-stu-id="86a94-111">What you will learn</span></span>
<span data-ttu-id="86a94-112">在本文中，您將了解：</span><span class="sxs-lookup"><span data-stu-id="86a94-112">In this article, you will learn:</span></span>
* <span data-ttu-id="86a94-113">如何 toouse hello Azure CLI toocreate IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="86a94-113">How toouse hello Azure CLI toocreate an IoT hub.</span></span>
* <span data-ttu-id="86a94-114">如何 toocreate pi IoT 中樞中的裝置身分識別。</span><span class="sxs-lookup"><span data-stu-id="86a94-114">How toocreate a device identity for Pi in your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="86a94-115">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="86a94-115">What you need</span></span>
* <span data-ttu-id="86a94-116">一個 Azure 帳戶</span><span class="sxs-lookup"><span data-stu-id="86a94-116">An Azure account</span></span>
* <span data-ttu-id="86a94-117">在 Mac 或 hello Azure CLI 安裝的 Windows 電腦</span><span class="sxs-lookup"><span data-stu-id="86a94-117">A Mac or a Windows computer with hello Azure CLI installed</span></span>

## <a name="create-your-iot-hub"></a><span data-ttu-id="86a94-118">建立 IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="86a94-118">Create your IoT hub</span></span>
<span data-ttu-id="86a94-119">Azure IoT 中樞可以協助您連接、監視並管理數以百萬計的 IoT 資產。</span><span class="sxs-lookup"><span data-stu-id="86a94-119">Azure IoT Hub helps you connect, monitor, and manage millions of IoT assets.</span></span> <span data-ttu-id="86a94-120">toocreate IoT 中樞，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="86a94-120">toocreate your IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="86a94-121">登入 tooyour Azure 帳戶執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="86a94-121">Sign in tooyour Azure account by running hello following command:</span></span>

   ```bash
   az login
   ```

   <span data-ttu-id="86a94-122">成功登入之後，系統將會列出所有可用的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="86a94-122">All your available subscriptions are listed after a successful sign-in.</span></span>

2. <span data-ttu-id="86a94-123">設定您藉由執行下列命令的 hello 想 toouse hello 預設訂用帳戶：</span><span class="sxs-lookup"><span data-stu-id="86a94-123">Set hello default subscription that you want toouse by running hello following command:</span></span>

   ```bash
   az account set --subscription {subscription id or name}
   ```

   <span data-ttu-id="86a94-124">`subscription ID or name`可以找到 hello 輸出中的 hello`az login`或 hello`az account list`命令。</span><span class="sxs-lookup"><span data-stu-id="86a94-124">`subscription ID or name` can be found in hello output of hello `az login` or hello `az account list` command.</span></span>

3. <span data-ttu-id="86a94-125">執行下列命令的 hello 註冊 hello 提供者。</span><span class="sxs-lookup"><span data-stu-id="86a94-125">Register hello provider by running hello following command.</span></span> <span data-ttu-id="86a94-126">資源提供者是為應用程式提供資源的服務。</span><span class="sxs-lookup"><span data-stu-id="86a94-126">Resource providers are services that provide resources for your application.</span></span> <span data-ttu-id="86a94-127">您必須先註冊 hello 提供者，才能部署 hello hello 提供者提供的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="86a94-127">You must register hello provider before you can deploy hello Azure resource that hello provider offers.</span></span>

   ```bash
   az provider register -n "Microsoft.Devices"
   ```
4. <span data-ttu-id="86a94-128">藉由執行下列命令的 hello 的 hello 美國西部地區中建立資源群組名稱 iot 範例：</span><span class="sxs-lookup"><span data-stu-id="86a94-128">Create a resource group named iot-sample in hello West US region by running hello following command:</span></span>

   ```bash
   az group create --name iot-sample --location westus
   ```

   <span data-ttu-id="86a94-129">`westus`是您在建立資源群組的 hello 位置。</span><span class="sxs-lookup"><span data-stu-id="86a94-129">`westus` is hello location you create your resource group.</span></span> <span data-ttu-id="86a94-130">如果您想 toouse 另一個位置，您可以執行`az account list-locations -o table`toosee 所有 hello Azure 支援的位置。</span><span class="sxs-lookup"><span data-stu-id="86a94-130">If you want toouse another location, you can run `az account list-locations -o table` toosee all hello locations Azure supports.</span></span>
 
5. <span data-ttu-id="86a94-131">建立 IoT 中樞 hello iot 範例資源群組中，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="86a94-131">Create an IoT hub in hello iot-sample resource group by running hello following command:</span></span>

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-sample
   ```

   <span data-ttu-id="86a94-132">根據預設，hello 工具會在 hello 可用的定價層中，建立 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="86a94-132">By default, hello tool creates an IoT Hub in hello Free pricing tier.</span></span> <span data-ttu-id="86a94-133">如需詳細資訊，請參閱 [Azure IoT 中樞價格](https://azure.microsoft.com/pricing/details/iot-hub/)。</span><span class="sxs-lookup"><span data-stu-id="86a94-133">For more infomation, see [Azure IoT Hub pricing](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

> [!NOTE]
> <span data-ttu-id="86a94-134">IoT 中樞 hello 名稱必須是全域唯一的。</span><span class="sxs-lookup"><span data-stu-id="86a94-134">hello name of your IoT hub must be globally unique.</span></span> <span data-ttu-id="86a94-135">您的 Azure 訂用帳戶只能建立一個 F1 版本的 Azure IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="86a94-135">You can create only one F1 edition of Azure IoT Hub under your Azure subscription.</span></span>

## <a name="register-pi-in-your-iot-hub"></a><span data-ttu-id="86a94-136">在 IoT 中樞中登錄 Pi</span><span class="sxs-lookup"><span data-stu-id="86a94-136">Register Pi in your IoT hub</span></span>
<span data-ttu-id="86a94-137">傳送訊息 tooyour IoT 中樞和接收訊息，或從 IoT 中樞的每個裝置必須註冊並提供唯一的識別碼。</span><span class="sxs-lookup"><span data-stu-id="86a94-137">Each device that sends messages tooyour IoT hub and receives messages from your IoT hub must be registered with a unique ID.</span></span>

<span data-ttu-id="86a94-138">執行下列命令在中樞登錄 Pi：</span><span class="sxs-lookup"><span data-stu-id="86a94-138">Register Pi in your hub by running following command:</span></span>

```bash
az iot device create --device-id myraspberrypi --hub {my hub name} --resource-group iot-sample
```

## <a name="summary"></a><span data-ttu-id="86a94-139">摘要</span><span class="sxs-lookup"><span data-stu-id="86a94-139">Summary</span></span>
<span data-ttu-id="86a94-140">您已建立 IoT 中樞，並在 IoT 中樞中搭配裝置識別登錄 Pi。</span><span class="sxs-lookup"><span data-stu-id="86a94-140">You've created an IoT hub and registered Pi with a device identity in your IoT hub.</span></span> <span data-ttu-id="86a94-141">您已準備好 toolearn toosend 從 Pi tooyour IoT 中樞的訊息。</span><span class="sxs-lookup"><span data-stu-id="86a94-141">You're ready toolearn how toosend messages from Pi tooyour IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="86a94-142">後續步驟</span><span class="sxs-lookup"><span data-stu-id="86a94-142">Next steps</span></span>
<span data-ttu-id="86a94-143">[建立 Azure 的函式應用程式與 Azure 儲存體帳戶 tooprocess 和市集 IoT 中樞訊息](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md)。</span><span class="sxs-lookup"><span data-stu-id="86a94-143">[Create an Azure function app and an Azure Storage account tooprocess and store IoT hub messages](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md).</span></span>

