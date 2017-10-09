---
title: "使用 Azure CLI (azure.js) IoT 中樞 aaaCreate |Microsoft 文件"
description: "如何使用您建立 Azure IoT 中樞 toocreate hello 跨平台 Azure CLI (azure.js)。"
services: iot-hub
documentationcenter: .net
author: BeatriceOltean
manager: timlt
editor: 
ms.assetid: 46a17831-650c-41d9-b228-445c5bb423d3
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/04/2017
ms.author: boltean
ms.openlocfilehash: c2a7ea98500b0a0e55a39f4cdfea4605c92add94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-hello-azure-cli"></a><span data-ttu-id="8dc1e-103">建立使用 Azure CLI hello IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="8dc1e-103">Create an IoT hub using hello Azure CLI</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

## <a name="introduction"></a><span data-ttu-id="8dc1e-104">簡介</span><span class="sxs-lookup"><span data-stu-id="8dc1e-104">Introduction</span></span>

<span data-ttu-id="8dc1e-105">您可以使用 Azure CLI (azure.js) toocreate，並以程式設計方式管理 Azure IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="8dc1e-105">You can use Azure CLI (azure.js) toocreate and manage Azure IoT hubs programmatically.</span></span> <span data-ttu-id="8dc1e-106">本文章將示範如何 toouse 會 hello Azure CLI (azure.js) toocreate IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="8dc1e-106">This article shows you how toouse hello Azure CLI (azure.js) toocreate an IoT hub.</span></span>

<span data-ttu-id="8dc1e-107">您可以完成 hello 工作使用其中一種 hello 遵循 CLI 版本：</span><span class="sxs-lookup"><span data-stu-id="8dc1e-107">You can complete hello task using one of hello following CLI versions:</span></span>

* <span data-ttu-id="8dc1e-108">Azure CLI (azure.js) – hello CLI 傳統的 hello 與資源管理部署模型這篇文章中所述。</span><span class="sxs-lookup"><span data-stu-id="8dc1e-108">Azure CLI (azure.js) – hello CLI for hello classic and resource management deployment models as described in this article.</span></span>
* <span data-ttu-id="8dc1e-109">[Azure CLI 2.0 (az.py)](iot-hub-create-using-cli.md) -hello 新一代 CLI hello 資源管理部署模型。</span><span class="sxs-lookup"><span data-stu-id="8dc1e-109">[Azure CLI 2.0 (az.py)](iot-hub-create-using-cli.md) - hello next generation CLI for hello resource management deployment model.</span></span>

<span data-ttu-id="8dc1e-110">toocomplete 本教學課程中，您需要遵循的 hello:</span><span class="sxs-lookup"><span data-stu-id="8dc1e-110">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="8dc1e-111">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="8dc1e-111">An active Azure account.</span></span> <span data-ttu-id="8dc1e-112">如果您沒有帳戶，只需要幾分鐘的時間就可以建立[免費帳戶][lnk-free-trial]。</span><span class="sxs-lookup"><span data-stu-id="8dc1e-112">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="8dc1e-113">[Azure CLI 0.10.4][lnk-CLI-install] 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="8dc1e-113">[Azure CLI 0.10.4][lnk-CLI-install] or later.</span></span> <span data-ttu-id="8dc1e-114">如果您已經有 hello Azure CLI 安裝，您可以驗證 hello 目前版本在 hello 命令提示字元以 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="8dc1e-114">If you already have hello Azure CLI installed, you can validate hello current version at hello command prompt with hello following command:</span></span>

```azurecli
azure --version
```

> [!NOTE]
> <span data-ttu-id="8dc1e-115">Azure 有兩種不同的部署模型可建立和處理資源：[Azure Resource Manager 和傳統](../azure-resource-manager/resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="8dc1e-115">Azure has two different deployment models for creating and working with resources:  [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="8dc1e-116">hello Azure CLI 必須是 Azure Resource Manager 模式：</span><span class="sxs-lookup"><span data-stu-id="8dc1e-116">hello Azure CLI must be in Azure Resource Manager mode:</span></span>
>
> ```azurecli
> azure config mode arm
> ```

## <a name="set-your-azure-account-and-subscription"></a><span data-ttu-id="8dc1e-117">設定 Azure 帳戶和訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="8dc1e-117">Set your Azure account and subscription</span></span>

1. <span data-ttu-id="8dc1e-118">在 hello 命令提示字元中輸入下列命令的 hello 登入：</span><span class="sxs-lookup"><span data-stu-id="8dc1e-118">At hello command prompt, login by typing hello following command:</span></span>

   ```azurecli
    azure login
   ```

   <span data-ttu-id="8dc1e-119">使用 hello 建議的網頁瀏覽器和程式碼 tooauthenticate。</span><span class="sxs-lookup"><span data-stu-id="8dc1e-119">Use hello suggested web browser and code tooauthenticate.</span></span>
1. <span data-ttu-id="8dc1e-120">如果您有多個 Azure 訂用帳戶，連接 tooAzure 授與存取 tooall hello 與認證相關聯的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="8dc1e-120">If you have multiple Azure subscriptions, connecting tooAzure grants you access tooall hello Azure subscriptions associated with your credentials.</span></span> <span data-ttu-id="8dc1e-121">您可以檢視 hello Azure 訂用帳戶，並找出哪一種 hello 預設，使用 hello 命令：</span><span class="sxs-lookup"><span data-stu-id="8dc1e-121">You can view hello Azure subscriptions, and identify which one is hello default, using hello command:</span></span>

   ```azurecli
    azure account list
   ```

   <span data-ttu-id="8dc1e-122">您想要在其下 toorun hello 其餘的 hello 命令使用 tooset hello 訂用帳戶內容：</span><span class="sxs-lookup"><span data-stu-id="8dc1e-122">tooset hello subscription context under which you want toorun hello rest of hello commands use:</span></span>

   ```azurecli
    azure account set <subscription name>
   ```

1. <span data-ttu-id="8dc1e-123">如果您沒有資源群組，您可以建立一個名為 **exampleResourceGroup** 的資源群組：</span><span class="sxs-lookup"><span data-stu-id="8dc1e-123">If you do not have a resource group, you can create one named **exampleResourceGroup**:</span></span>

   ```azurecli
    azure group create -n exampleResourceGroup -l westus
   ```

> [!TIP]
> <span data-ttu-id="8dc1e-124">hello 文章[使用 hello Azure CLI toomanage Azure 資源與資源群組][ lnk-CLI-arm]提供詳細的資訊關於如何 toouse hello Azure CLI toomanage Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="8dc1e-124">hello article [Use hello Azure CLI toomanage Azure resources and resource groups][lnk-CLI-arm] provides more information about how toouse hello Azure CLI toomanage Azure resources.</span></span>

## <a name="create-an-iot-hub"></a><span data-ttu-id="8dc1e-125">建立 IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="8dc1e-125">Create an IoT Hub</span></span>

<span data-ttu-id="8dc1e-126">必要參數：</span><span class="sxs-lookup"><span data-stu-id="8dc1e-126">Required parameters:</span></span>

```azurecli
azure iothub create -g <resource-group> -n <name> -l <location> -s <sku-name> -u <units>
```

* <span data-ttu-id="8dc1e-127">**resource-group**。</span><span class="sxs-lookup"><span data-stu-id="8dc1e-127">**resource-group**.</span></span> <span data-ttu-id="8dc1e-128">hello 資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="8dc1e-128">hello resource group name.</span></span> <span data-ttu-id="8dc1e-129">不區分大小寫英數字元、 底線和連字號，1-64 長度 hello 格式。</span><span class="sxs-lookup"><span data-stu-id="8dc1e-129">hello format is case insensitive alphanumeric, underscore, and hyphen, 1-64 length.</span></span>
* <span data-ttu-id="8dc1e-130">**名稱**。</span><span class="sxs-lookup"><span data-stu-id="8dc1e-130">**name**.</span></span> <span data-ttu-id="8dc1e-131">建立 hello IoT 中樞 toobe hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="8dc1e-131">hello name of hello IoT hub toobe created.</span></span> <span data-ttu-id="8dc1e-132">不區分大小寫英數字元、 底線和連字號、 3-50 長度 hello 格式。</span><span class="sxs-lookup"><span data-stu-id="8dc1e-132">hello format is case insensitive alphanumeric, underscore, and hyphen, 3-50 length.</span></span>
* <span data-ttu-id="8dc1e-133">**location**。</span><span class="sxs-lookup"><span data-stu-id="8dc1e-133">**location**.</span></span> <span data-ttu-id="8dc1e-134">hello 位置 （azure 區域/資料中心） tooprovision hello IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="8dc1e-134">hello location (azure region/datacenter) tooprovision hello IoT hub.</span></span>
* <span data-ttu-id="8dc1e-135">**sku-name**。</span><span class="sxs-lookup"><span data-stu-id="8dc1e-135">**sku-name**.</span></span> <span data-ttu-id="8dc1e-136">hello hello sku 的其中一個名稱: [F1、 S1、 S2、 S3]。</span><span class="sxs-lookup"><span data-stu-id="8dc1e-136">hello name of hello sku, one of: [F1, S1, S2, S3].</span></span> <span data-ttu-id="8dc1e-137">Hello 最新的完整清單，請參閱 toohello IoT 中樞定價頁面。</span><span class="sxs-lookup"><span data-stu-id="8dc1e-137">For hello latest full list, refer toohello pricing page for IoT Hub.</span></span>
* <span data-ttu-id="8dc1e-138">**units**。</span><span class="sxs-lookup"><span data-stu-id="8dc1e-138">**units**.</span></span> <span data-ttu-id="8dc1e-139">hello 佈建的單位數目。</span><span class="sxs-lookup"><span data-stu-id="8dc1e-139">hello number of provisioned units.</span></span> <span data-ttu-id="8dc1e-140">範圍：F1 [1-1]：S1、S2 [1-200]：S3 [1-10]。</span><span class="sxs-lookup"><span data-stu-id="8dc1e-140">Range: F1 [1-1] : S1, S2 [1-200] : S3 [1-10].</span></span> <span data-ttu-id="8dc1e-141">IoT 中樞單位以您想 tooconnect 您總訊息計數和 hello 裝置數目。</span><span class="sxs-lookup"><span data-stu-id="8dc1e-141">IoT Hub units are based on your total message count and hello number of devices you want tooconnect.</span></span>

[!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

<span data-ttu-id="8dc1e-142">toosee 所有 hello 參數可供建立，您可以使用命令提示字元中的 hello [說明] 命令：</span><span class="sxs-lookup"><span data-stu-id="8dc1e-142">toosee all hello parameters available for creation, you can use hello help command in command prompt:</span></span>

```azurecli
azure iothub create -h
```

<span data-ttu-id="8dc1e-143">簡單的範例： toocreate IoT 中樞呼叫**exampleIoTHubName** hello 資源群組中**exampleResourceGroup**，請執行 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="8dc1e-143">Quick example: toocreate an IoT Hub called **exampleIoTHubName** in hello resource group **exampleResourceGroup**, run hello following command:</span></span>

```azurecli
azure iothub create -g exampleResourceGroup -n exampleIoTHubName -l westus -k s1 -u 1
```

> [!NOTE]
> <span data-ttu-id="8dc1e-144">此 Azure CLI 命令會新增您付費的「S1 標準 IoT 中樞」。</span><span class="sxs-lookup"><span data-stu-id="8dc1e-144">This Azure CLI command creates an S1 Standard IoT Hub for which you are billed.</span></span> <span data-ttu-id="8dc1e-145">您可以刪除 hello IoT 中樞**exampleIoTHubName**使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="8dc1e-145">You can delete hello IoT hub **exampleIoTHubName** using following command:</span></span>
>
> ```azurecli
> azure iothub delete -g exampleResourceGroup -n exampleIoTHubName
> ```

## <a name="next-steps"></a><span data-ttu-id="8dc1e-146">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8dc1e-146">Next steps</span></span>

<span data-ttu-id="8dc1e-147">toolearn 進一步了解開發的 IoT 中樞，請參閱下列文章 hello:</span><span class="sxs-lookup"><span data-stu-id="8dc1e-147">toolearn more about developing for IoT Hub, see hello following article:</span></span>

* <span data-ttu-id="8dc1e-148">[IoT SDK][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="8dc1e-148">[IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="8dc1e-149">toofurther 瀏覽的 IoT 中樞的 hello 功能，請參閱：</span><span class="sxs-lookup"><span data-stu-id="8dc1e-149">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="8dc1e-150">[使用 hello Azure 入口網站 toomanage IoT 中樞][lnk-portal]</span><span class="sxs-lookup"><span data-stu-id="8dc1e-150">[Using hello Azure portal toomanage IoT Hub][lnk-portal]</span></span>

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-azure-portal]: https://portal.azure.com/
[lnk-status]: https://azure.microsoft.com/status/
[lnk-CLI-install]:../cli-install-nodejs.md
[lnk-rest-api]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-CLI-arm]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md

[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-portal]: iot-hub-create-through-portal.md 
