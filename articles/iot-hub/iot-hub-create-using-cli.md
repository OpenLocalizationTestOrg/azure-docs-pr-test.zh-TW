---
title: "使用 Azure CLI (az.py) 建立 IoT 中樞 | Microsoft Docs"
description: "如何使用跨平台 Azure CLI 2.0 (az.py) 建立 Azure IoT 中樞。"
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
ms.openlocfilehash: 161089159999a4a63a39b059e69a08b7a9297445
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-iot-hub-using-the-azure-cli-20"></a><span data-ttu-id="3c101-103">使用 Azure CLI 2.0 建立 IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="3c101-103">Create an IoT hub using the Azure CLI 2.0</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

## <a name="introduction"></a><span data-ttu-id="3c101-104">簡介</span><span class="sxs-lookup"><span data-stu-id="3c101-104">Introduction</span></span>

<span data-ttu-id="3c101-105">您可以使用 Azure CLI 2.0 (az.py)，以程式設計方式建立和管理 Azure IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="3c101-105">You can use Azure CLI 2.0 (az.py) to create and manage Azure IoT hubs programmatically.</span></span> <span data-ttu-id="3c101-106">本文將說明如何使用 Azure CLI 2.0 (az.py) 建立 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="3c101-106">This article shows you how to use the Azure CLI 2.0 (az.py) to create an IoT hub.</span></span>

<span data-ttu-id="3c101-107">您可以使用下列其中一個 CLI 版本來完成工作︰</span><span class="sxs-lookup"><span data-stu-id="3c101-107">You can complete the task using one of the following CLI versions:</span></span>

* <span data-ttu-id="3c101-108">[Azure CLI (azure.js)](iot-hub-create-using-cli-nodejs.md) – 適用於傳統和資源管理部署模型的 CLI。</span><span class="sxs-lookup"><span data-stu-id="3c101-108">[Azure CLI (azure.js)](iot-hub-create-using-cli-nodejs.md) – the CLI for the classic and resource management deployment models.</span></span>
* <span data-ttu-id="3c101-109">Azure CLI 2.0 (az.py) - 適用於資源管理部署模型的新一代 CLI (如本文中所述)。</span><span class="sxs-lookup"><span data-stu-id="3c101-109">Azure CLI 2.0 (az.py) - the next generation CLI for the resource management deployment model as described in this article.</span></span>

<span data-ttu-id="3c101-110">若要完成此教學課程，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="3c101-110">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="3c101-111">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="3c101-111">An active Azure account.</span></span> <span data-ttu-id="3c101-112">如果您沒有帳戶，只需要幾分鐘的時間就可以建立[免費帳戶][lnk-free-trial]。</span><span class="sxs-lookup"><span data-stu-id="3c101-112">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="3c101-113">[Azure CLI 2.0][lnk-CLI-install]。</span><span class="sxs-lookup"><span data-stu-id="3c101-113">[Azure CLI 2.0][lnk-CLI-install].</span></span>

## <a name="sign-in-and-set-your-azure-account"></a><span data-ttu-id="3c101-114">登入並設定 Azure 帳戶</span><span class="sxs-lookup"><span data-stu-id="3c101-114">Sign in and set your Azure account</span></span>

<span data-ttu-id="3c101-115">登入您的 Azure 帳戶並選取您的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="3c101-115">Sign in to your Azure account and select your subscription.</span></span>

1. <span data-ttu-id="3c101-116">在命令提示字元中，執行[登入命令][lnk-login-command]：</span><span class="sxs-lookup"><span data-stu-id="3c101-116">At the command prompt, run the [login command][lnk-login-command]:</span></span>
    
    ```azurecli
    az login
    ```

    <span data-ttu-id="3c101-117">依照指示使用程式碼進行驗證，並透過網頁瀏覽器登入 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="3c101-117">Follow the instructions to authenticate using the code and sign in to your Azure account through a web browser.</span></span>

2. <span data-ttu-id="3c101-118">如果您有多個 Azure 訂用帳戶，則登入 Azure 會授予您所有與認證相關聯之 Azure 帳戶的存取權。</span><span class="sxs-lookup"><span data-stu-id="3c101-118">If you have multiple Azure subscriptions, signing in to Azure grants you access to all the Azure accounts associated with your credentials.</span></span> <span data-ttu-id="3c101-119">使用下列[命令來列出可供您使用的 Azure 帳戶][lnk-az-account-command]︰</span><span class="sxs-lookup"><span data-stu-id="3c101-119">Use the following [command to list the Azure accounts][lnk-az-account-command] available for you to use:</span></span>
    
    ```azurecli
    az account list 
    ```

    <span data-ttu-id="3c101-120">使用下列命令，選取您想要用來執行命令以建立 IoT 中樞的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="3c101-120">Use the following command to select subscription that you want to use to run the commands to create your IoT hub.</span></span> <span data-ttu-id="3c101-121">您可以使用來自上一個命令之輸出內的訂用帳戶名稱或識別碼︰</span><span class="sxs-lookup"><span data-stu-id="3c101-121">You can use either the subscription name or ID from the output of the previous command:</span></span>

    ```azurecli
    az account set --subscription {your subscription name or id}
    ```

## <a name="create-an-iot-hub"></a><span data-ttu-id="3c101-122">建立 IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="3c101-122">Create an IoT Hub</span></span>

<span data-ttu-id="3c101-123">使用 Azure CLI 建立資源群組，然後新增 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="3c101-123">Use the Azure CLI to create a resource group and then add an IoT hub.</span></span>

1. <span data-ttu-id="3c101-124">在建立 IoT 中樞時，必須將其建立在資源群組內。</span><span class="sxs-lookup"><span data-stu-id="3c101-124">When you create an IoT hub, you must create it in a resource group.</span></span> <span data-ttu-id="3c101-125">使用現有的資源群組，或執行下列[命令來建立資源群組][lnk-az-resource-command]：</span><span class="sxs-lookup"><span data-stu-id="3c101-125">Either use an existing resource group, or run the following [command to create a resource group][lnk-az-resource-command]:</span></span>
    
    ```azurecli
     az group create --name {your resource group name} --location westus
    ```

    > [!TIP]
    > <span data-ttu-id="3c101-126">上一個範例會建立位於美國西部位置的資源群組。</span><span class="sxs-lookup"><span data-stu-id="3c101-126">The previous example creates the resource group in the West US location.</span></span> <span data-ttu-id="3c101-127">您可以執行命令 `az account list-locations -o table`，以檢視可用位置清單。</span><span class="sxs-lookup"><span data-stu-id="3c101-127">You can view a list of available locations by running the command `az account list-locations -o table`.</span></span>
    >
    >

2. <span data-ttu-id="3c101-128">使用 IoT 中樞的全域唯一名稱，在資源群組中執行下列命令[建立 IoT 中樞][lnk-az-iot-command]：</span><span class="sxs-lookup"><span data-stu-id="3c101-128">Run the following [command to create an IoT hub][lnk-az-iot-command] in your resource group, using a globally unique name for your IoT hub:</span></span>
    
    ```azurecli
    az iot hub create --name {your iot hub name} --resource-group {your resource group name} --sku S1
    ```

   [!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]


> [!NOTE]
> <span data-ttu-id="3c101-129">上一個命令會在您付費使用的 S1 定價層中建立 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="3c101-129">The previous command creates an IoT hub in the S1 pricing tier for which you are billed.</span></span> <span data-ttu-id="3c101-130">如需詳細資訊，請參閱 [Azure IoT 中樞價格][lnk-iot-pricing]。</span><span class="sxs-lookup"><span data-stu-id="3c101-130">For more information, see [Azure IoT Hub pricing][lnk-iot-pricing].</span></span>
>
>

## <a name="remove-an-iot-hub"></a><span data-ttu-id="3c101-131">移除 IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="3c101-131">Remove an IoT Hub</span></span>

<span data-ttu-id="3c101-132">您可以使用 Azure CLI 來[刪除個別資源][lnk-az-resource-command](例如 IoT 中樞)，或刪除資源群組和其所有資源 (包括任何 IoT 中樞)。</span><span class="sxs-lookup"><span data-stu-id="3c101-132">You can use the Azure CLI to [delete an individual resource][lnk-az-resource-command], such as an IoT hub, or delete a resource group and all its resources, including any IoT hubs.</span></span>

<span data-ttu-id="3c101-133">若要刪除 IoT 中樞，請執行下列命令︰</span><span class="sxs-lookup"><span data-stu-id="3c101-133">To delete an IoT hub, run the following command:</span></span>

```azurecli
az iot hub delete --name {your iot hub name} --resource-group {your resource group name}
```

<span data-ttu-id="3c101-134">若要刪除資源群組和其所有資源，請執行下列命令︰</span><span class="sxs-lookup"><span data-stu-id="3c101-134">To delete a resource group and all its resources, run the following command:</span></span>

```azurecli
az group delete --name {your resource group name}
```

## <a name="next-steps"></a><span data-ttu-id="3c101-135">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3c101-135">Next steps</span></span>
<span data-ttu-id="3c101-136">若要深入了解如何開發 IoT 中樞，請參閱以下文章︰</span><span class="sxs-lookup"><span data-stu-id="3c101-136">To learn more about developing for IoT Hub, see the following articles:</span></span>

* <span data-ttu-id="3c101-137">[IoT 中樞開發人員指南][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="3c101-137">[IoT Hub developer guide][lnk-devguide]</span></span>

<span data-ttu-id="3c101-138">若要進一步探索 IoT 中樞的功能，請參閱︰</span><span class="sxs-lookup"><span data-stu-id="3c101-138">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="3c101-139">[使用 Azure 入口網站管理 IoT 中樞][lnk-portal]</span><span class="sxs-lookup"><span data-stu-id="3c101-139">[Using the Azure portal to manage IoT Hub][lnk-portal]</span></span>

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
