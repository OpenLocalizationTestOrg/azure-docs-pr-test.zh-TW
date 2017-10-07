---
title: "使用 PowerShell 指令程式的 Azure IoT 中樞 aaaCreate |Microsoft 文件"
description: "如何 toouse PowerShell cmdlet toocreate IoT 中樞。"
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
ms.openlocfilehash: 005cd8d48eb39d2e8b1bfb9ef84330d4aae4658f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-hello-new-azurermiothub-cmdlet"></a><span data-ttu-id="0edd5-103">建立 IoT 中心使用 hello 新增 AzureRmIotHub cmdlet</span><span class="sxs-lookup"><span data-stu-id="0edd5-103">Create an IoT hub using hello New-AzureRmIotHub cmdlet</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

## <a name="introduction"></a><span data-ttu-id="0edd5-104">簡介</span><span class="sxs-lookup"><span data-stu-id="0edd5-104">Introduction</span></span>

<span data-ttu-id="0edd5-105">您可以使用 Azure PowerShell cmdlet toocreate 和管理 Azure IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="0edd5-105">You can use Azure PowerShell cmdlets toocreate and manage Azure IoT hubs.</span></span> <span data-ttu-id="0edd5-106">本教學課程示範如何使用 PowerShell IoT 中樞 toocreate。</span><span class="sxs-lookup"><span data-stu-id="0edd5-106">This tutorial shows you how toocreate an IoT hub with PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="0edd5-107">Azure 建立和處理資源的部署模型有兩種：[Azure Resource Manager](../azure-resource-manager/resource-manager-deployment-model.md) 和傳統。</span><span class="sxs-lookup"><span data-stu-id="0edd5-107">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="0edd5-108">本文件涵蓋使用 hello Azure Resource Manager 部署模型。</span><span class="sxs-lookup"><span data-stu-id="0edd5-108">This article covers using hello Azure Resource Manager deployment model.</span></span>

<span data-ttu-id="0edd5-109">toocomplete 本教學課程中，您需要遵循的 hello:</span><span class="sxs-lookup"><span data-stu-id="0edd5-109">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="0edd5-110">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="0edd5-110">An active Azure account.</span></span> <br/><span data-ttu-id="0edd5-111">如果您沒有帳戶，只需要幾分鐘的時間就可以建立[免費帳戶][lnk-free-trial]。</span><span class="sxs-lookup"><span data-stu-id="0edd5-111">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="0edd5-112">[Azure PowerShell Cmdlet][lnk-powershell-install]。</span><span class="sxs-lookup"><span data-stu-id="0edd5-112">[Azure PowerShell cmdlets][lnk-powershell-install].</span></span>

## <a name="connect-tooyour-azure-subscription"></a><span data-ttu-id="0edd5-113">連接 tooyour Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="0edd5-113">Connect tooyour Azure subscription</span></span>
<span data-ttu-id="0edd5-114">在 PowerShell 命令提示字元中，輸入下列命令 toosign tooyour Azure 訂用帳戶中的 hello:</span><span class="sxs-lookup"><span data-stu-id="0edd5-114">In a PowerShell command prompt, enter hello following command toosign in tooyour Azure subscription:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="0edd5-115">如果您有多個 Azure 訂用帳戶，授與存取 tooall 登入 tooAzure hello 與認證相關聯的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="0edd5-115">If you have multiple Azure subscriptions, signing in tooAzure grants you access tooall hello Azure subscriptions associated with your credentials.</span></span> <span data-ttu-id="0edd5-116">使用下列命令 toolist hello Azure 訂用帳戶可讓您 toouse hello:</span><span class="sxs-lookup"><span data-stu-id="0edd5-116">Use hello following command toolist hello Azure subscriptions available for you toouse:</span></span>

```powershell
Get-AzureRMSubscription
```

<span data-ttu-id="0edd5-117">使用下列命令 tooselect 訂用帳戶的 toouse toorun hello 命令 toocreate IoT 中樞的 hello。</span><span class="sxs-lookup"><span data-stu-id="0edd5-117">Use hello following command tooselect subscription that you want toouse toorun hello commands toocreate your IoT hub.</span></span> <span data-ttu-id="0edd5-118">您可以使用 hello 訂用帳戶名稱或識別碼，從 hello 輸出 hello 前一個命令：</span><span class="sxs-lookup"><span data-stu-id="0edd5-118">You can use either hello subscription name or ID from hello output of hello previous command:</span></span>

```powershell
Select-AzureRMSubscription `
    -SubscriptionName "{your subscription name}"
```

## <a name="create-resource-group"></a><span data-ttu-id="0edd5-119">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="0edd5-119">Create resource group</span></span>

<span data-ttu-id="0edd5-120">您需要的資源群組 toodeploy IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="0edd5-120">You need a resource group toodeploy an IoT hub.</span></span> <span data-ttu-id="0edd5-121">您可以使用現有的資源群組，或建立一個新的群組。</span><span class="sxs-lookup"><span data-stu-id="0edd5-121">You can use an existing resource group or create a new one.</span></span>

<span data-ttu-id="0edd5-122">您可以使用下列命令 toodiscover hello 位置，您可以在其中部署 IoT 中樞的 hello:</span><span class="sxs-lookup"><span data-stu-id="0edd5-122">You can use hello following command toodiscover hello locations where you can deploy an IoT hub:</span></span>

```powershell
((Get-AzureRmResourceProvider `
  -ProviderNamespace Microsoft.Devices).ResourceTypes `
  | Where-Object ResourceTypeName -eq IoTHubs).Locations
```

<span data-ttu-id="0edd5-123">toocreate IoT 中樞，下列命令使用 hello hello 支援位置其中之一的 IoT 中心的資源群組。</span><span class="sxs-lookup"><span data-stu-id="0edd5-123">toocreate a resource group for your IoT hub in one of hello supported locations for IoT Hub, use hello following command.</span></span> <span data-ttu-id="0edd5-124">這個範例會建立一個稱為資源群組**MyIoTRG1**在 hello**美國東部**區域：</span><span class="sxs-lookup"><span data-stu-id="0edd5-124">This example creates a resource group called **MyIoTRG1** in hello **East US** region:</span></span>

```powershell
New-AzureRmResourceGroup -Name MyIoTRG1 -Location "East US"
```

## <a name="create-an-iot-hub"></a><span data-ttu-id="0edd5-125">建立 IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="0edd5-125">Create an IoT hub</span></span>

<span data-ttu-id="0edd5-126">toocreate IoT 中心在您建立在 hello 先前步驟中，下列命令使用 hello hello 資源群組中。</span><span class="sxs-lookup"><span data-stu-id="0edd5-126">toocreate an IoT hub in hello resource group you created in hello previous step, use hello following command.</span></span> <span data-ttu-id="0edd5-127">這個範例會建立**S1**中樞呼叫**MyTestIoTHub**在 hello**美國東部**區域：</span><span class="sxs-lookup"><span data-stu-id="0edd5-127">This example creates an **S1** hub called **MyTestIoTHub** in hello **East US** region:</span></span>

```powershell
New-AzureRmIotHub `
    -ResourceGroupName MyIoTRG1 `
    -Name MyTestIoTHub `
    -SkuName S1 -Units 1 `
    -Location "East US"
```

<span data-ttu-id="0edd5-128">hello hello IoT 中樞名稱不得重複。</span><span class="sxs-lookup"><span data-stu-id="0edd5-128">hello name of hello IoT hub must be unique.</span></span>

[!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]


<span data-ttu-id="0edd5-129">您可以使用下列命令的 hello 您訂用帳戶中列出所有 hello IoT 中心：</span><span class="sxs-lookup"><span data-stu-id="0edd5-129">You can list all hello IoT hubs in your subscription using hello following command:</span></span>

```powershell
Get-AzureRmIotHub
```

<span data-ttu-id="0edd5-130">hello 前一個範例會將 S1 標準 IoT 中樞，您需要付費。</span><span class="sxs-lookup"><span data-stu-id="0edd5-130">hello previous example adds an S1 Standard IoT Hub for which you are billed.</span></span> <span data-ttu-id="0edd5-131">您可以刪除 hello IoT 中樞使用 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="0edd5-131">You can delete hello IoT hub using hello following command:</span></span>

```powershell
Remove-AzureRmIotHub `
    -ResourceGroupName MyIoTRG1 `
    -Name MyTestIoTHub
```

<span data-ttu-id="0edd5-132">或者，您可以移除資源群組，而且所有 hello 它包含使用下列命令的 hello 的資源：</span><span class="sxs-lookup"><span data-stu-id="0edd5-132">Alternatively, you can remove a resource group and all hello resources it contains using hello following command:</span></span>

```powershell
Remove-AzureRmResourceGroup -Name MyIoTRG1
```

## <a name="next-steps"></a><span data-ttu-id="0edd5-133">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0edd5-133">Next steps</span></span>

<span data-ttu-id="0edd5-134">現在您已經部署 IoT 中心使用 PowerShell cmdlet，您可以進一步 tooexplore:</span><span class="sxs-lookup"><span data-stu-id="0edd5-134">Now you have deployed an IoT hub using a PowerShell cmdlet, you may want tooexplore further:</span></span>

* <span data-ttu-id="0edd5-135">探索其他[搭配您的 IoT 中樞使用的 PowerShell Cmdlet][lnk-iothub-cmdlets]。</span><span class="sxs-lookup"><span data-stu-id="0edd5-135">Discover other [PowerShell cmdlets for working with your IoT hub][lnk-iothub-cmdlets].</span></span>
* <span data-ttu-id="0edd5-136">閱讀有關 hello hello 功能[IoT 中樞資源提供者 REST API][lnk-rest-api]。</span><span class="sxs-lookup"><span data-stu-id="0edd5-136">Read about hello capabilities of hello [IoT Hub resource provider REST API][lnk-rest-api].</span></span>

<span data-ttu-id="0edd5-137">進一步了解開發的 IoT 中樞 toolearn，請參閱下列文章的 hello:</span><span class="sxs-lookup"><span data-stu-id="0edd5-137">toolearn more about developing for IoT Hub, see hello following articles:</span></span>

* <span data-ttu-id="0edd5-138">[簡介 tooC SDK][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="0edd5-138">[Introduction tooC SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="0edd5-139">[Azure IoT SDK][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="0edd5-139">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="0edd5-140">toofurther 瀏覽的 IoT 中樞的 hello 功能，請參閱：</span><span class="sxs-lookup"><span data-stu-id="0edd5-140">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="0edd5-141">[使用 IoT Edge 來模擬裝置][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="0edd5-141">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-powershell-install]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps
[lnk-iothub-cmdlets]: https://docs.microsoft.com/powershell/module/azurerm.iothub/
[lnk-rest-api]: https://docs.microsoft.com/rest/api/iothub/iothubresource

[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
