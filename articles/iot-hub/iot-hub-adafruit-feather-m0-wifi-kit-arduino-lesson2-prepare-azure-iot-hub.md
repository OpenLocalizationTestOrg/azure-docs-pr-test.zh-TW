---
title: "連接 Arduino tooAzure IoT-第 2 課： 註冊裝置 |Microsoft 文件"
description: "建立資源群組、 建立 Azure IoT 中樞，並註冊 Adafruit 羽毛 M0 WiFi hello Azure IoT 中樞中使用 Azure CLI hello。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "連接 arduino toocloud、 azure iot 中樞、 網際網路事項雲端的 azure iot 中樞建立 arduino 雲端的裝置"
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
ms.openlocfilehash: ca362f9c143dd3a98bf47a66b63a9725a0ffc2d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-iot-hub-and-register-your-adafruit-feather-m0-wifi-arduino-board"></a><span data-ttu-id="435fc-104">建立 IoT 中樞並登錄 Adafruit Feather M0 WiFi Arduino 面板</span><span class="sxs-lookup"><span data-stu-id="435fc-104">Create your IoT hub and register your Adafruit Feather M0 WiFi Arduino board</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="435fc-105">將執行的作業</span><span class="sxs-lookup"><span data-stu-id="435fc-105">What you will do</span></span>
* <span data-ttu-id="435fc-106">建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="435fc-106">Create a resource group.</span></span>
* <span data-ttu-id="435fc-107">建立您的 Azure IoT 中樞 hello 資源群組中。</span><span class="sxs-lookup"><span data-stu-id="435fc-107">Create your Azure IoT hub in hello resource group.</span></span>
* <span data-ttu-id="435fc-108">使用 hello Azure 命令列介面 (Azure CLI)，以新增您 Arduino 面板 toohello 的 Azure IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="435fc-108">Add your Arduino board toohello Azure IoT hub by using hello Azure command-line interface (Azure CLI).</span></span>

<span data-ttu-id="435fc-109">當您使用 hello Azure CLI tooadd Arduino 面板 tooyour IoT 中樞時，hello 服務就會產生與 hello 服務您 Arduino 面板 tooauthenticate 的索引鍵。</span><span class="sxs-lookup"><span data-stu-id="435fc-109">When you use hello Azure CLI tooadd your Arduino board tooyour IoT hub, hello service generates a key for your Arduino board tooauthenticate with hello service.</span></span> <span data-ttu-id="435fc-110">如果您有任何問題，尋找解決方案上 hello[疑難排解頁面][troubleshoot]。</span><span class="sxs-lookup"><span data-stu-id="435fc-110">If you have any problems, look for solutions on hello [troubleshooting page][troubleshoot].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="435fc-111">學習目標</span><span class="sxs-lookup"><span data-stu-id="435fc-111">What you will learn</span></span>
<span data-ttu-id="435fc-112">在本文中，您將了解：</span><span class="sxs-lookup"><span data-stu-id="435fc-112">In this article, you will learn:</span></span>
* <span data-ttu-id="435fc-113">如何 toouse hello Azure CLI toocreate IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="435fc-113">How toouse hello Azure CLI toocreate an IoT hub.</span></span>
* <span data-ttu-id="435fc-114">如何 toocreate Arduino 您的裝置識別面板在 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="435fc-114">How toocreate a device identity for your Arduino board in your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="435fc-115">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="435fc-115">What you need</span></span>
* <span data-ttu-id="435fc-116">一個 Azure 帳戶</span><span class="sxs-lookup"><span data-stu-id="435fc-116">An Azure account</span></span>
* <span data-ttu-id="435fc-117">已安裝的電腦 hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="435fc-117">A computer with hello Azure CLI installed</span></span>

## <a name="create-your-iot-hub"></a><span data-ttu-id="435fc-118">建立 IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="435fc-118">Create your IoT hub</span></span>
<span data-ttu-id="435fc-119">Azure IoT 中樞可以協助您連接、監視並管理數以百萬計的 IoT 資產。</span><span class="sxs-lookup"><span data-stu-id="435fc-119">Azure IoT Hub helps you connect, monitor, and manage millions of IoT assets.</span></span> <span data-ttu-id="435fc-120">toocreate IoT 中樞，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="435fc-120">toocreate your IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="435fc-121">登入 tooyour Azure 帳戶執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="435fc-121">Sign in tooyour Azure account by running hello following command:</span></span>

   ```bash
   az login
   ```

   <span data-ttu-id="435fc-122">成功登入之後，系統將會列出所有可用的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="435fc-122">All your available subscriptions are listed after a successful sign-in.</span></span>

2. <span data-ttu-id="435fc-123">設定您藉由執行下列命令的 hello 想 toouse hello 預設訂用帳戶：</span><span class="sxs-lookup"><span data-stu-id="435fc-123">Set hello default subscription that you want toouse by running hello following command:</span></span>

   ```bash
   az account set --subscription {subscription id or name}
   ```

   <span data-ttu-id="435fc-124">`subscription ID or name`可以找到 hello 輸出中的 hello`az login`或 hello`az account list`命令。</span><span class="sxs-lookup"><span data-stu-id="435fc-124">`subscription ID or name` can be found in hello output of hello `az login` or hello `az account list` command.</span></span>

3. <span data-ttu-id="435fc-125">執行下列命令的 hello 註冊 hello 提供者。</span><span class="sxs-lookup"><span data-stu-id="435fc-125">Register hello provider by running hello following command.</span></span> <span data-ttu-id="435fc-126">資源提供者是為應用程式提供資源的服務。</span><span class="sxs-lookup"><span data-stu-id="435fc-126">Resource providers are services that provide resources for your application.</span></span> <span data-ttu-id="435fc-127">您必須先註冊 hello 提供者，才能部署 hello hello 提供者提供的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="435fc-127">You must register hello provider before you can deploy hello Azure resource that hello provider offers.</span></span>

   ```bash
   az provider register -n "Microsoft.Devices"
   ```
4. <span data-ttu-id="435fc-128">藉由執行下列命令的 hello 的 hello 美國西部地區中建立資源群組名稱 iot 範例：</span><span class="sxs-lookup"><span data-stu-id="435fc-128">Create a resource group named iot-sample in hello West US region by running hello following command:</span></span>

   ```bash
   az group create --name iot-sample --location westus
   ```

   <span data-ttu-id="435fc-129">`westus`是您在建立資源群組的 hello 位置。</span><span class="sxs-lookup"><span data-stu-id="435fc-129">`westus` is hello location you create your resource group.</span></span> <span data-ttu-id="435fc-130">如果您想 toouse 另一個位置，您可以執行`az account list-locations -o table`toosee 所有 hello Azure 支援的位置。</span><span class="sxs-lookup"><span data-stu-id="435fc-130">If you want toouse another location, you can run `az account list-locations -o table` toosee all hello locations Azure supports.</span></span>

5. <span data-ttu-id="435fc-131">建立 IoT 中樞 hello iot 範例資源群組中，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="435fc-131">Create an IoT hub in hello iot-sample resource group by running hello following command:</span></span>

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-sample
   ```

<span data-ttu-id="435fc-132">根據預設，hello 工具會在 hello 可用的定價層中，建立 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="435fc-132">By default, hello tool creates an IoT Hub in hello Free pricing tier.</span></span> <span data-ttu-id="435fc-133">如需詳細資訊，請參閱 [Azure IoT 中樞價格](https://azure.microsoft.com/pricing/details/iot-hub/)。</span><span class="sxs-lookup"><span data-stu-id="435fc-133">For more infomation, see [Azure IoT Hub pricing](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

> [!NOTE]
> <span data-ttu-id="435fc-134">IoT 中樞 hello 名稱必須是全域唯一的。</span><span class="sxs-lookup"><span data-stu-id="435fc-134">hello name of your IoT hub must be globally unique.</span></span>
> <span data-ttu-id="435fc-135">您的 Azure 訂用帳戶只能建立一個 F1 版本的 Azure IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="435fc-135">You can create only one F1 edition of Azure IoT Hub under your Azure subscription.</span></span>

## <a name="register-your-arduino-board-in-your-iot-hub"></a><span data-ttu-id="435fc-136">在 IoT 中樞登錄您的 Arduino 面板</span><span class="sxs-lookup"><span data-stu-id="435fc-136">Register your Arduino board in your IoT hub</span></span>
<span data-ttu-id="435fc-137">傳送訊息 tooyour IoT 中樞和接收訊息，或從 IoT 中樞的每個裝置必須註冊並提供唯一的識別碼。</span><span class="sxs-lookup"><span data-stu-id="435fc-137">Each device that sends messages tooyour IoT hub and receives messages from your IoT hub must be registered with a unique ID.</span></span>

<span data-ttu-id="435fc-138">執行下列命令在 Azure IoT 中樞中登錄您的 Arduino 面板：</span><span class="sxs-lookup"><span data-stu-id="435fc-138">Register your Arduino board in your IoT hub by running following command:</span></span>

```bash
az iot device create --device-id mym0wifi --hub-name {my hub name}
```

## <a name="summary"></a><span data-ttu-id="435fc-139">摘要</span><span class="sxs-lookup"><span data-stu-id="435fc-139">Summary</span></span>
<span data-ttu-id="435fc-140">您已建立 IoT 中樞，並在 IoT 中樞中登錄您的 Arduino 面板及裝置身分識別。</span><span class="sxs-lookup"><span data-stu-id="435fc-140">You've created an IoT hub and registered your Arduino board with a device identity in your IoT hub.</span></span> <span data-ttu-id="435fc-141">您已準備好 toolearn toosend 的訊息從 Arduino 面板 tooyour IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="435fc-141">You're ready toolearn how toosend messages from your Arduino board tooyour IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="435fc-142">後續步驟</span><span class="sxs-lookup"><span data-stu-id="435fc-142">Next steps</span></span>
<span data-ttu-id="435fc-143">[建立 Azure 的函式應用程式與 Azure 儲存體帳戶 tooprocess 和市集 IoT 中樞訊息][process-and-store-iot-hub-messages]。</span><span class="sxs-lookup"><span data-stu-id="435fc-143">[Create an Azure function app and an Azure Storage account tooprocess and store IoT hub messages][process-and-store-iot-hub-messages].</span></span>


<!-- Images and links -->

[troubleshoot]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-deploy-resource-manager-template.md