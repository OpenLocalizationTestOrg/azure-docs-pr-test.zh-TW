---
title: "aaaCreate Azure IoT 中樞使用的範本 (PowerShell) |Microsoft 文件"
description: "如何 toouse Azure Resource Manager 範本 toocreate IoT 中樞與 PowerShell。"
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 7eade855-c289-4ffb-b5ef-02be8c5f670f
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: e98ff5e898200cd727b9326fb3df393e43b021e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-azure-resource-manager-template-powershell"></a><span data-ttu-id="dd6bb-103">使用 Azure Resource Manager 範本建立 IoT 中樞 (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="dd6bb-103">Create an IoT hub using Azure Resource Manager template (PowerShell)</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

<span data-ttu-id="dd6bb-104">您可以使用 Azure Resource Manager toocreate，並以程式設計方式管理 Azure IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="dd6bb-104">You can use Azure Resource Manager toocreate and manage Azure IoT hubs programmatically.</span></span> <span data-ttu-id="dd6bb-105">本教學課程示範如何 toouse Azure Resource Manager 範本 toocreate IoT 中樞與 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="dd6bb-105">This tutorial shows you how toouse an Azure Resource Manager template toocreate an IoT hub with PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="dd6bb-106">Azure 建立和處理資源的部署模型有兩種：[Azure Resource Manager](../azure-resource-manager/resource-manager-deployment-model.md) 和傳統。</span><span class="sxs-lookup"><span data-stu-id="dd6bb-106">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="dd6bb-107">本文件涵蓋使用 hello Azure Resource Manager 部署模型。</span><span class="sxs-lookup"><span data-stu-id="dd6bb-107">This article covers using hello Azure Resource Manager deployment model.</span></span>

<span data-ttu-id="dd6bb-108">toocomplete 本教學課程中，您需要遵循的 hello:</span><span class="sxs-lookup"><span data-stu-id="dd6bb-108">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="dd6bb-109">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="dd6bb-109">An active Azure account.</span></span> <br/><span data-ttu-id="dd6bb-110">如果您沒有帳戶，只需要幾分鐘的時間就可以建立[免費帳戶][lnk-free-trial]。</span><span class="sxs-lookup"><span data-stu-id="dd6bb-110">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="dd6bb-111">[Azure PowerShell 1.0][lnk-powershell-install] 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="dd6bb-111">[Azure PowerShell 1.0][lnk-powershell-install] or later.</span></span>

> [!TIP]
> <span data-ttu-id="dd6bb-112">hello 文章[使用 Azure PowerShell 的 Azure Resource Manager] [ lnk-powershell-arm]提供更多有關 toouse PowerShell 和 Azure 資源管理員範本 toocreate Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="dd6bb-112">hello article [Using Azure PowerShell with Azure Resource Manager][lnk-powershell-arm] provides more information about how toouse PowerShell and Azure Resource Manager templates toocreate Azure resources.</span></span>

## <a name="connect-tooyour-azure-subscription"></a><span data-ttu-id="dd6bb-113">連接 tooyour Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="dd6bb-113">Connect tooyour Azure subscription</span></span>

<span data-ttu-id="dd6bb-114">在 PowerShell 命令提示字元中，輸入下列命令 toosign tooyour Azure 訂用帳戶中的 hello:</span><span class="sxs-lookup"><span data-stu-id="dd6bb-114">In a PowerShell command prompt, enter hello following command toosign in tooyour Azure subscription:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="dd6bb-115">如果您有多個 Azure 訂用帳戶，授與存取 tooall 登入 tooAzure hello 與認證相關聯的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="dd6bb-115">If you have multiple Azure subscriptions, signing in tooAzure grants you access tooall hello Azure subscriptions associated with your credentials.</span></span> <span data-ttu-id="dd6bb-116">使用下列命令 toolist hello Azure 訂用帳戶可讓您 toouse hello:</span><span class="sxs-lookup"><span data-stu-id="dd6bb-116">Use hello following command toolist hello Azure subscriptions available for you toouse:</span></span>

```powershell
Get-AzureRMSubscription
```

<span data-ttu-id="dd6bb-117">使用下列命令 tooselect 訂用帳戶的 toouse toorun hello 命令 toocreate IoT 中樞的 hello。</span><span class="sxs-lookup"><span data-stu-id="dd6bb-117">Use hello following command tooselect subscription that you want toouse toorun hello commands toocreate your IoT hub.</span></span> <span data-ttu-id="dd6bb-118">您可以使用 hello 訂用帳戶名稱或識別碼，從 hello 輸出 hello 前一個命令：</span><span class="sxs-lookup"><span data-stu-id="dd6bb-118">You can use either hello subscription name or ID from hello output of hello previous command:</span></span>

```powershell
Select-AzureRMSubscription `
    -SubscriptionName "{your subscription name}"
```

<span data-ttu-id="dd6bb-119">您可以使用下列命令 toodiscover 其中您可以部署 IoT 中樞與 hello 目前支援的 API 版本的 hello:</span><span class="sxs-lookup"><span data-stu-id="dd6bb-119">You can use hello following commands toodiscover where you can deploy an IoT hub and hello currently supported API versions:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Devices).ResourceTypes | Where-Object ResourceTypeName -eq IoTHubs).Locations
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Devices).ResourceTypes | Where-Object ResourceTypeName -eq IoTHubs).ApiVersions
```

<span data-ttu-id="dd6bb-120">建立資源群組 toocontain 您使用下列命令中其中一個支援的 hello 位置 IoT 中樞的 hello 的 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="dd6bb-120">Create a resource group toocontain your IoT hub using hello following command in one of hello supported locations for IoT Hub.</span></span> <span data-ttu-id="dd6bb-121">這個範例會建立一個稱為 **MyIoTRG1**的資源群組：</span><span class="sxs-lookup"><span data-stu-id="dd6bb-121">This example creates a resource group called **MyIoTRG1**:</span></span>

```powershell
New-AzureRmResourceGroup -Name MyIoTRG1 -Location "East US"
```

## <a name="submit-a-template-toocreate-an-iot-hub"></a><span data-ttu-id="dd6bb-122">送出範本 toocreate IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="dd6bb-122">Submit a template toocreate an IoT hub</span></span>

<span data-ttu-id="dd6bb-123">使用資源群組中的 JSON 範本 toocreate IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="dd6bb-123">Use a JSON template toocreate an IoT hub in your resource group.</span></span> <span data-ttu-id="dd6bb-124">您也可以使用 Azure Resource Manager 範本 toomake 變更 tooan 現有 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="dd6bb-124">You can also use an Azure Resource Manager template toomake changes tooan existing IoT hub.</span></span>

1. <span data-ttu-id="dd6bb-125">使用 Azure Resource Manager 範本所呼叫的文字編輯器 toocreate **template.json**與 hello 資源定義 toocreate 下列新的標準 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="dd6bb-125">Use a text editor toocreate an Azure Resource Manager template called **template.json** with hello following resource definition toocreate a new standard IoT hub.</span></span> <span data-ttu-id="dd6bb-126">這個範例會將 hello IoT 中樞中 hello**美國東部**區域中，會建立兩個取用者群組 (**cg1**和**cg2**) hello 事件中樞相容的端點，以及使用 hello **2016年-02-03** API 版本。</span><span class="sxs-lookup"><span data-stu-id="dd6bb-126">This example adds hello IoT Hub in hello **East US** region, creates two consumer groups (**cg1** and **cg2**) on hello Event Hub-compatible endpoint, and uses hello **2016-02-03** API version.</span></span> <span data-ttu-id="dd6bb-127">此範本也需要您 toopass hello IoT 中樞名稱做為參數，呼叫**hubName**。</span><span class="sxs-lookup"><span data-stu-id="dd6bb-127">This template also expects you toopass in hello IoT hub name as a parameter called **hubName**.</span></span> <span data-ttu-id="dd6bb-128">如 hello 目前的位置，其支援 IoT 中樞的清單，請參閱[Azure 狀態][lnk-status]。</span><span class="sxs-lookup"><span data-stu-id="dd6bb-128">For hello current list of locations that support IoT Hub see [Azure Status][lnk-status].</span></span>

    ```json
    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "hubName": {
          "type": "string"
        }
      },
      "resources": [
      {
        "apiVersion": "2016-02-03",
        "type": "Microsoft.Devices/IotHubs",
        "name": "[parameters('hubName')]",
        "location": "East US",
        "sku": {
          "name": "S1",
          "tier": "Standard",
          "capacity": 1
        },
        "properties": {
          "location": "East US"
        }
      },
      {
        "apiVersion": "2016-02-03",
        "type": "Microsoft.Devices/IotHubs/eventhubEndpoints/ConsumerGroups",
        "name": "[concat(parameters('hubName'), '/events/cg1')]",
        "dependsOn": [
          "[concat('Microsoft.Devices/Iothubs/', parameters('hubName'))]"
        ]
      },
      {
        "apiVersion": "2016-02-03",
        "type": "Microsoft.Devices/IotHubs/eventhubEndpoints/ConsumerGroups",
        "name": "[concat(parameters('hubName'), '/events/cg2')]",
        "dependsOn": [
          "[concat('Microsoft.Devices/Iothubs/', parameters('hubName'))]"
        ]
      }
      ],
      "outputs": {
        "hubKeys": {
          "value": "[listKeys(resourceId('Microsoft.Devices/IotHubs', parameters('hubName')), '2016-02-03')]",
          "type": "object"
        }
      }
    }
    ```

2. <span data-ttu-id="dd6bb-129">儲存在本機電腦上的 hello Azure 資源管理員範本檔案。</span><span class="sxs-lookup"><span data-stu-id="dd6bb-129">Save hello Azure Resource Manager template file on your local machine.</span></span> <span data-ttu-id="dd6bb-130">這個範例假設您將它儲存在名為 **c:\templates** 的資料夾中。</span><span class="sxs-lookup"><span data-stu-id="dd6bb-130">This example assumes you save it in a folder called **c:\templates**.</span></span>

3. <span data-ttu-id="dd6bb-131">執行下列命令 toodeploy hello 您新的 IoT 中樞，做為參數傳遞 hello IoT 中樞名稱。</span><span class="sxs-lookup"><span data-stu-id="dd6bb-131">Run hello following command toodeploy your new IoT hub, passing hello name of your IoT hub as a parameter.</span></span> <span data-ttu-id="dd6bb-132">在此範例中，是 hello hello IoT 中樞名稱`abcmyiothub`。</span><span class="sxs-lookup"><span data-stu-id="dd6bb-132">In this example, hello name of hello IoT hub is `abcmyiothub`.</span></span> <span data-ttu-id="dd6bb-133">IoT 中樞 hello 名稱必須是全域唯一的：</span><span class="sxs-lookup"><span data-stu-id="dd6bb-133">hello name of your IoT hub must be globally unique:</span></span>

    ```powershell
    New-AzureRmResourceGroupDeployment -ResourceGroupName MyIoTRG1 -TemplateFile C:\templates\template.json -hubName abcmyiothub
    ```
  [!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

4. <span data-ttu-id="dd6bb-134">hello 輸出會顯示 hello hello IoT 中樞，您所建立的索引鍵。</span><span class="sxs-lookup"><span data-stu-id="dd6bb-134">hello output displays hello keys for hello IoT hub you created.</span></span>

5. <span data-ttu-id="dd6bb-135">您的應用程式加入的 tooverify hello IoT 中樞，請瀏覽 hello [Azure 入口網站][ lnk-azure-portal]並檢視您資源的清單。</span><span class="sxs-lookup"><span data-stu-id="dd6bb-135">tooverify your application added hello new IoT hub, visit hello [Azure portal][lnk-azure-portal] and view your list of resources.</span></span> <span data-ttu-id="dd6bb-136">或者，使用 hello **Get AzureRmResource** PowerShell cmdlet。</span><span class="sxs-lookup"><span data-stu-id="dd6bb-136">Alternatively, use hello **Get-AzureRmResource** PowerShell cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="dd6bb-137">此範例應用程式會加入您付費的「S1 標準 IoT 中樞」。</span><span class="sxs-lookup"><span data-stu-id="dd6bb-137">This example application adds an S1 Standard IoT Hub for which you are billed.</span></span> <span data-ttu-id="dd6bb-138">您可以刪除透過 hello hello IoT 中樞[Azure 入口網站][ lnk-azure-portal]或使用 hello**移除 AzureRmResource** PowerShell 指令程式完成時。</span><span class="sxs-lookup"><span data-stu-id="dd6bb-138">You can delete hello IoT hub through hello [Azure portal][lnk-azure-portal] or by using hello **Remove-AzureRmResource** PowerShell cmdlet when you are finished.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dd6bb-139">後續步驟</span><span class="sxs-lookup"><span data-stu-id="dd6bb-139">Next steps</span></span>

<span data-ttu-id="dd6bb-140">現在您已經部署使用 Azure Resource Manager 範本搭配 PowerShell IoT 中樞，您可以進一步 tooexplore:</span><span class="sxs-lookup"><span data-stu-id="dd6bb-140">Now you have deployed an IoT hub using an Azure Resource Manager template with PowerShell, you may want tooexplore further:</span></span>

* <span data-ttu-id="dd6bb-141">閱讀有關 hello hello 功能[IoT 中樞資源提供者 REST API][lnk-rest-api]。</span><span class="sxs-lookup"><span data-stu-id="dd6bb-141">Read about hello capabilities of hello [IoT Hub resource provider REST API][lnk-rest-api].</span></span>
* <span data-ttu-id="dd6bb-142">讀取[Azure 資源管理員概觀][ lnk-azure-rm-overview] toolearn 更多關於 hello 功能的 Azure 資源管理員。</span><span class="sxs-lookup"><span data-stu-id="dd6bb-142">Read [Azure Resource Manager overview][lnk-azure-rm-overview] toolearn more about hello capabilities of Azure Resource Manager.</span></span>

<span data-ttu-id="dd6bb-143">進一步了解開發的 IoT 中樞 toolearn，請參閱下列文章的 hello:</span><span class="sxs-lookup"><span data-stu-id="dd6bb-143">toolearn more about developing for IoT Hub, see hello following articles:</span></span>

* <span data-ttu-id="dd6bb-144">[簡介 tooC SDK][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="dd6bb-144">[Introduction tooC SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="dd6bb-145">[Azure IoT SDK][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="dd6bb-145">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="dd6bb-146">toofurther 瀏覽的 IoT 中樞的 hello 功能，請參閱：</span><span class="sxs-lookup"><span data-stu-id="dd6bb-146">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="dd6bb-147">[使用 Azure IoT Edge 來模擬裝置][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="dd6bb-147">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-azure-portal]: https://portal.azure.com/
[lnk-status]: https://azure.microsoft.com/status/
[lnk-powershell-install]: /powershell/azure/install-azurerm-ps
[lnk-rest-api]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-azure-rm-overview]: ../azure-resource-manager/resource-group-overview.md
[lnk-powershell-arm]: ../azure-resource-manager/powershell-azure-resource-manager.md

[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
