---
title: "使用 Azure CLI (az.py) IoT 中樞 aaaCreate |Microsoft 文件"
description: "如何使用您建立 Azure IoT 中樞 toocreate hello 跨平台 Azure CLI 2.0 (az.py)。"
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 
ms.service: iot-hub
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: dobett
ms.openlocfilehash: 9c9639235c2ac343e6ceb9578291dafaea26ea24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-hello-azure-cli-20"></a><span data-ttu-id="11c64-103">建立使用 Azure CLI 2.0 hello IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="11c64-103">Create an IoT hub using hello Azure CLI 2.0</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

## <a name="introduction"></a><span data-ttu-id="11c64-104">簡介</span><span class="sxs-lookup"><span data-stu-id="11c64-104">Introduction</span></span>

<span data-ttu-id="11c64-105">您可以使用 Azure CLI 2.0 (az.py) toocreate，並以程式設計方式管理 Azure IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="11c64-105">You can use Azure CLI 2.0 (az.py) toocreate and manage Azure IoT hubs programmatically.</span></span> <span data-ttu-id="11c64-106">本文章將示範如何 toouse 會 hello Azure CLI 2.0 (az.py) toocreate IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="11c64-106">This article shows you how toouse hello Azure CLI 2.0 (az.py) toocreate an IoT hub.</span></span>

<span data-ttu-id="11c64-107">您可以完成 hello 工作使用其中一種 hello 遵循 CLI 版本：</span><span class="sxs-lookup"><span data-stu-id="11c64-107">You can complete hello task using one of hello following CLI versions:</span></span>

* <span data-ttu-id="11c64-108">[Azure CLI (azure.js)](iot-hub-create-using-cli-nodejs.md) – hello CLI hello 傳統和資源管理部署模型。</span><span class="sxs-lookup"><span data-stu-id="11c64-108">[Azure CLI (azure.js)](iot-hub-create-using-cli-nodejs.md) – hello CLI for hello classic and resource management deployment models.</span></span>
* <span data-ttu-id="11c64-109">Azure CLI 2.0 (az.py)-hello 新一代 CLI hello 資源管理部署模型的這篇文章中所述。</span><span class="sxs-lookup"><span data-stu-id="11c64-109">Azure CLI 2.0 (az.py) - hello next generation CLI for hello resource management deployment model as described in this article.</span></span>

<span data-ttu-id="11c64-110">toocomplete 本教學課程中，您需要遵循的 hello:</span><span class="sxs-lookup"><span data-stu-id="11c64-110">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="11c64-111">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="11c64-111">An active Azure account.</span></span> <span data-ttu-id="11c64-112">如果您沒有帳戶，只需要幾分鐘的時間就可以建立[免費帳戶][lnk-free-trial]。</span><span class="sxs-lookup"><span data-stu-id="11c64-112">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="11c64-113">[Azure CLI 2.0][lnk-CLI-install]。</span><span class="sxs-lookup"><span data-stu-id="11c64-113">[Azure CLI 2.0][lnk-CLI-install].</span></span>

## <a name="sign-in-and-set-your-azure-account"></a><span data-ttu-id="11c64-114">登入並設定 Azure 帳戶</span><span class="sxs-lookup"><span data-stu-id="11c64-114">Sign in and set your Azure account</span></span>

<span data-ttu-id="11c64-115">登入 tooyour Azure 帳戶，並選取您的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="11c64-115">Sign in tooyour Azure account and select your subscription.</span></span>

1. <span data-ttu-id="11c64-116">在 hello 命令提示字元中執行 hello[登入命令][lnk-login-command]:</span><span class="sxs-lookup"><span data-stu-id="11c64-116">At hello command prompt, run hello [login command][lnk-login-command]:</span></span>
    
    ```azurecli
    az login
    ```

    <span data-ttu-id="11c64-117">請遵循 hello 指示 tooauthenticate 使用 hello 程式碼，並登入 tooyour 透過 web 瀏覽器的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="11c64-117">Follow hello instructions tooauthenticate using hello code and sign in tooyour Azure account through a web browser.</span></span>

2. <span data-ttu-id="11c64-118">如果您有多個 Azure 訂用帳戶，授與存取 tooall 登入 tooAzure hello 與認證相關聯的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="11c64-118">If you have multiple Azure subscriptions, signing in tooAzure grants you access tooall hello Azure accounts associated with your credentials.</span></span> <span data-ttu-id="11c64-119">使用下列 hello[命令 toolist hello Azure 帳戶][ lnk-az-account-command]適用於您 toouse:</span><span class="sxs-lookup"><span data-stu-id="11c64-119">Use hello following [command toolist hello Azure accounts][lnk-az-account-command] available for you toouse:</span></span>
    
    ```azurecli
    az account list 
    ```

    <span data-ttu-id="11c64-120">使用下列命令 tooselect 訂用帳戶的 toouse toorun hello 命令 toocreate IoT 中樞的 hello。</span><span class="sxs-lookup"><span data-stu-id="11c64-120">Use hello following command tooselect subscription that you want toouse toorun hello commands toocreate your IoT hub.</span></span> <span data-ttu-id="11c64-121">您可以使用 hello 訂用帳戶名稱或識別碼，從 hello 輸出 hello 前一個命令：</span><span class="sxs-lookup"><span data-stu-id="11c64-121">You can use either hello subscription name or ID from hello output of hello previous command:</span></span>

    ```azurecli
    az account set --subscription {your subscription name or id}
    ```

## <a name="create-an-iot-hub"></a><span data-ttu-id="11c64-122">建立 IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="11c64-122">Create an IoT Hub</span></span>

<span data-ttu-id="11c64-123">使用 hello Azure CLI toocreate 資源群組，然後再加入 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="11c64-123">Use hello Azure CLI toocreate a resource group and then add an IoT hub.</span></span>

1. <span data-ttu-id="11c64-124">在建立 IoT 中樞時，必須將其建立在資源群組內。</span><span class="sxs-lookup"><span data-stu-id="11c64-124">When you create an IoT hub, you must create it in a resource group.</span></span> <span data-ttu-id="11c64-125">使用現有的資源群組，或執行 hello 下列[命令 toocreate 資源群組][lnk-az-resource-command]:</span><span class="sxs-lookup"><span data-stu-id="11c64-125">Either use an existing resource group, or run hello following [command toocreate a resource group][lnk-az-resource-command]:</span></span>
    
    ```azurecli
     az group create --name {your resource group name} --location westus
    ```

    > [!TIP]
    > <span data-ttu-id="11c64-126">hello 前一個範例會在 hello 美國西部位置中建立 hello 資源群組。</span><span class="sxs-lookup"><span data-stu-id="11c64-126">hello previous example creates hello resource group in hello West US location.</span></span> <span data-ttu-id="11c64-127">您可以執行 hello 命令，以檢視可用位置清單`az account list-locations -o table`。</span><span class="sxs-lookup"><span data-stu-id="11c64-127">You can view a list of available locations by running hello command `az account list-locations -o table`.</span></span>
    >
    >

2. <span data-ttu-id="11c64-128">執行下列 hello[命令 toocreate IoT 中樞][ lnk-az-iot-command]在資源群組中，使用您的 IoT 中樞的全域唯一名稱：</span><span class="sxs-lookup"><span data-stu-id="11c64-128">Run hello following [command toocreate an IoT hub][lnk-az-iot-command] in your resource group, using a globally unique name for your IoT hub:</span></span>
    
    ```azurecli
    az iot hub create --name {your iot hub name} --resource-group {your resource group name} --sku S1
    ```

   [!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]


> [!NOTE]
> <span data-ttu-id="11c64-129">hello 前一個命令會建立 IoT 中樞 hello S1 定價的層，您需要付費。</span><span class="sxs-lookup"><span data-stu-id="11c64-129">hello previous command creates an IoT hub in hello S1 pricing tier for which you are billed.</span></span> <span data-ttu-id="11c64-130">如需詳細資訊，請參閱 [Azure IoT 中樞價格][lnk-iot-pricing]。</span><span class="sxs-lookup"><span data-stu-id="11c64-130">For more information, see [Azure IoT Hub pricing][lnk-iot-pricing].</span></span>
>
>

## <a name="remove-an-iot-hub"></a><span data-ttu-id="11c64-131">移除 IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="11c64-131">Remove an IoT Hub</span></span>

<span data-ttu-id="11c64-132">您也可以使用 Azure CLI hello[刪除個別的資源，][lnk-az-resource-command]，例如 IoT 中心] 或 [刪除資源群組和它的所有資源，包括任何 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="11c64-132">You can use hello Azure CLI too[delete an individual resource][lnk-az-resource-command], such as an IoT hub, or delete a resource group and all its resources, including any IoT hubs.</span></span>

<span data-ttu-id="11c64-133">IoT 中樞，執行下列命令的 hello toodelete:</span><span class="sxs-lookup"><span data-stu-id="11c64-133">toodelete an IoT hub, run hello following command:</span></span>

```azurecli
az iot hub delete --name {your iot hub name} --resource-group {your resource group name}
```

<span data-ttu-id="11c64-134">toodelete 資源群組和其所有資源，執行 hello，下列命令：</span><span class="sxs-lookup"><span data-stu-id="11c64-134">toodelete a resource group and all its resources, run hello following command:</span></span>

```azurecli
az group delete --name {your resource group name}
```

## <a name="next-steps"></a><span data-ttu-id="11c64-135">後續步驟</span><span class="sxs-lookup"><span data-stu-id="11c64-135">Next steps</span></span>
<span data-ttu-id="11c64-136">進一步了解開發的 IoT 中樞 toolearn，請參閱下列文章的 hello:</span><span class="sxs-lookup"><span data-stu-id="11c64-136">toolearn more about developing for IoT Hub, see hello following articles:</span></span>

* <span data-ttu-id="11c64-137">[IoT 中樞開發人員指南][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="11c64-137">[IoT Hub developer guide][lnk-devguide]</span></span>

<span data-ttu-id="11c64-138">toofurther 瀏覽的 IoT 中樞的 hello 功能，請參閱：</span><span class="sxs-lookup"><span data-stu-id="11c64-138">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="11c64-139">[使用 hello Azure 入口網站 toomanage IoT 中樞][lnk-portal]</span><span class="sxs-lookup"><span data-stu-id="11c64-139">[Using hello Azure portal toomanage IoT Hub][lnk-portal]</span></span>

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-CLI-install]: https://docs.microsoft.com/cli/azure/install-az-cli2
[lnk-login-command]: https://docs.microsoft.com/cli/azure/get-started-with-az-cli2
[lnk-az-account-command]: https://docs.microsoft.com/cli/azure/account
[lnk-az-register-command]: https://docs.microsoft.com/cli/azure/provider
[lnk-az-addcomponent-command]: https://docs.microsoft.com/cli/azure/component
[lnk-az-resource-command]: https://docs.microsoft.com/cli/azure/resource
[lnk-az-iot-command]: https://docs.microsoft.com/cli/azure/iot
[lnk-iot-pricing]: https://azure.microsoft.com/pricing/details/iot-hub/
[lnk-devguide]: iot-hub-devguide.md
[lnk-portal]: iot-hub-create-through-portal.md 
