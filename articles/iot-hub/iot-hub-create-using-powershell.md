---
title: "使用 PowerShell Cmdlet 建立 Azure IoT 中樞 | Microsoft Docs"
description: "如何使用 PowerShell Cmdlet 建立 IoT 中樞。"
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 02227adeb8a9a7463506efa44ddc2977f8aae65a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="create-an-iot-hub-using-the-new-azurermiothub-cmdlet"></a><span data-ttu-id="50b16-103">使用 New-AzureRmIotHub Cmdlet 建立 IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="50b16-103">Create an IoT hub using the New-AzureRmIotHub cmdlet</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

## <a name="introduction"></a><span data-ttu-id="50b16-104">簡介</span><span class="sxs-lookup"><span data-stu-id="50b16-104">Introduction</span></span>

<span data-ttu-id="50b16-105">您可以使用 Azure PowerShell Cmdlet 建立及管理 Azure IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="50b16-105">You can use Azure PowerShell cmdlets to create and manage Azure IoT hubs.</span></span> <span data-ttu-id="50b16-106">此教學課程會示範如何使用 PowerShell 建立 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="50b16-106">This tutorial shows you how to create an IoT hub with PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="50b16-107">Azure 建立和處理資源的部署模型有兩種：[Azure Resource Manager](../azure-resource-manager/resource-manager-deployment-model.md) 和傳統。</span><span class="sxs-lookup"><span data-stu-id="50b16-107">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="50b16-108">本文涵蓋使用 Azure Resource Manager 部署模型的部分。</span><span class="sxs-lookup"><span data-stu-id="50b16-108">This article covers using the Azure Resource Manager deployment model.</span></span>

<span data-ttu-id="50b16-109">若要完成此教學課程，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="50b16-109">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="50b16-110">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="50b16-110">An active Azure account.</span></span> <br/><span data-ttu-id="50b16-111">如果您沒有帳戶，只需要幾分鐘的時間就可以建立[免費帳戶][lnk-free-trial]。</span><span class="sxs-lookup"><span data-stu-id="50b16-111">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="50b16-112">[Azure PowerShell Cmdlet][lnk-powershell-install]。</span><span class="sxs-lookup"><span data-stu-id="50b16-112">[Azure PowerShell cmdlets][lnk-powershell-install].</span></span>

## <a name="connect-to-your-azure-subscription"></a><span data-ttu-id="50b16-113">連接到 Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="50b16-113">Connect to your Azure subscription</span></span>
<span data-ttu-id="50b16-114">在 PowerShell 命令提示字元中，輸入下列命令來登入您的 Azure 訂用帳戶：</span><span class="sxs-lookup"><span data-stu-id="50b16-114">In a PowerShell command prompt, enter the following command to sign in to your Azure subscription:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="50b16-115">如果您有多個 Azure 訂用帳戶，則登入 Azure 即會為您授與和您認證相關聯之所有 Azure 訂用帳戶的存取權。</span><span class="sxs-lookup"><span data-stu-id="50b16-115">If you have multiple Azure subscriptions, signing in to Azure grants you access to all the Azure subscriptions associated with your credentials.</span></span> <span data-ttu-id="50b16-116">使用下列命令來列出可供您使用的 Azure 訂用帳戶：</span><span class="sxs-lookup"><span data-stu-id="50b16-116">Use the following command to list the Azure subscriptions available for you to use:</span></span>

```powershell
Get-AzureRMSubscription
```

<span data-ttu-id="50b16-117">使用下列命令，選取您想要用來執行命令以建立 IoT 中樞的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="50b16-117">Use the following command to select subscription that you want to use to run the commands to create your IoT hub.</span></span> <span data-ttu-id="50b16-118">您可以使用來自上一個命令之輸出內的訂用帳戶名稱或識別碼︰</span><span class="sxs-lookup"><span data-stu-id="50b16-118">You can use either the subscription name or ID from the output of the previous command:</span></span>

```powershell
Select-AzureRMSubscription `
    -SubscriptionName "{your subscription name}"
```

## <a name="create-resource-group"></a><span data-ttu-id="50b16-119">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="50b16-119">Create resource group</span></span>

<span data-ttu-id="50b16-120">您需要一個資源群組來部署 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="50b16-120">You need a resource group to deploy an IoT hub.</span></span> <span data-ttu-id="50b16-121">您可以使用現有的資源群組，或建立一個新的群組。</span><span class="sxs-lookup"><span data-stu-id="50b16-121">You can use an existing resource group or create a new one.</span></span>

<span data-ttu-id="50b16-122">您可以使用下列命令，探索您可以在其中部署 IoT 中樞的位置：</span><span class="sxs-lookup"><span data-stu-id="50b16-122">You can use the following command to discover the locations where you can deploy an IoT hub:</span></span>

```powershell
((Get-AzureRmResourceProvider `
  -ProviderNamespace Microsoft.Devices).ResourceTypes `
  | Where-Object ResourceTypeName -eq IoTHubs).Locations
```

<span data-ttu-id="50b16-123">若要在下列其中一個支援的 IoT 中樞位置中建立 IoT 中樞的資源群組，請使用下列命令。</span><span class="sxs-lookup"><span data-stu-id="50b16-123">To create a resource group for your IoT hub in one of the supported locations for IoT Hub, use the following command.</span></span> <span data-ttu-id="50b16-124">此範例會在**美國東部**區域中建立一個稱為 **MyIoTRG1** 的資源群組：</span><span class="sxs-lookup"><span data-stu-id="50b16-124">This example creates a resource group called **MyIoTRG1** in the **East US** region:</span></span>

```powershell
New-AzureRmResourceGroup -Name MyIoTRG1 -Location "East US"
```

## <a name="create-an-iot-hub"></a><span data-ttu-id="50b16-125">建立 IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="50b16-125">Create an IoT hub</span></span>

<span data-ttu-id="50b16-126">若要在您於上一個步驟中建立的資源群組中建立 IoT 中樞，請使用下列命令。</span><span class="sxs-lookup"><span data-stu-id="50b16-126">To create an IoT hub in the resource group you created in the previous step, use the following command.</span></span> <span data-ttu-id="50b16-127">此範例會在**美國東部**區域中建立一個稱為 **MyTestIoTHub** 的 **S1** 中樞：</span><span class="sxs-lookup"><span data-stu-id="50b16-127">This example creates an **S1** hub called **MyTestIoTHub** in the **East US** region:</span></span>

```powershell
New-AzureRmIotHub `
    -ResourceGroupName MyIoTRG1 `
    -Name MyTestIoTHub `
    -SkuName S1 -Units 1 `
    -Location "East US"
```

<span data-ttu-id="50b16-128">IoT 中樞名稱必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="50b16-128">The name of the IoT hub must be unique.</span></span>

[!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]


<span data-ttu-id="50b16-129">您可以使用下列命令來列出您訂用帳戶中的所有 IoT 中樞︰</span><span class="sxs-lookup"><span data-stu-id="50b16-129">You can list all the IoT hubs in your subscription using the following command:</span></span>

```powershell
Get-AzureRmIotHub
```

<span data-ttu-id="50b16-130">前一個範例會新增一個向您收費的 S1 標準 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="50b16-130">The previous example adds an S1 Standard IoT Hub for which you are billed.</span></span> <span data-ttu-id="50b16-131">您可以使用下列命令刪除該 IoT 中樞：</span><span class="sxs-lookup"><span data-stu-id="50b16-131">You can delete the IoT hub using the following command:</span></span>

```powershell
Remove-AzureRmIotHub `
    -ResourceGroupName MyIoTRG1 `
    -Name MyTestIoTHub
```

<span data-ttu-id="50b16-132">或者，您可以使用下列命令移除資源群組，及其包含的所有資源：</span><span class="sxs-lookup"><span data-stu-id="50b16-132">Alternatively, you can remove a resource group and all the resources it contains using the following command:</span></span>

```powershell
Remove-AzureRmResourceGroup -Name MyIoTRG1
```

## <a name="next-steps"></a><span data-ttu-id="50b16-133">後續步驟</span><span class="sxs-lookup"><span data-stu-id="50b16-133">Next steps</span></span>

<span data-ttu-id="50b16-134">現在您已經使用 PowerShell Cmdlet 部署 IoT 中樞，您可能想要進一步探索︰</span><span class="sxs-lookup"><span data-stu-id="50b16-134">Now you have deployed an IoT hub using a PowerShell cmdlet, you may want to explore further:</span></span>

* <span data-ttu-id="50b16-135">探索其他[搭配您的 IoT 中樞使用的 PowerShell Cmdlet][lnk-iothub-cmdlets]。</span><span class="sxs-lookup"><span data-stu-id="50b16-135">Discover other [PowerShell cmdlets for working with your IoT hub][lnk-iothub-cmdlets].</span></span>
* <span data-ttu-id="50b16-136">閱讀 [IoT 中樞資源提供者 REST API][lnk-rest-api] 功能的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="50b16-136">Read about the capabilities of the [IoT Hub resource provider REST API][lnk-rest-api].</span></span>

<span data-ttu-id="50b16-137">若要深入了解如何開發 IoT 中樞，請參閱以下文章︰</span><span class="sxs-lookup"><span data-stu-id="50b16-137">To learn more about developing for IoT Hub, see the following articles:</span></span>

* <span data-ttu-id="50b16-138">[C SDK 簡介][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="50b16-138">[Introduction to C SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="50b16-139">[Azure IoT SDK][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="50b16-139">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="50b16-140">若要進一步探索 IoT 中樞的功能，請參閱︰</span><span class="sxs-lookup"><span data-stu-id="50b16-140">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="50b16-141">[使用 IoT Edge 來模擬裝置][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="50b16-141">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-powershell-install]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps
[lnk-iothub-cmdlets]: https://docs.microsoft.com/powershell/module/azurerm.iothub/
[lnk-rest-api]: https://docs.microsoft.com/rest/api/iothub/iothubresource

[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
