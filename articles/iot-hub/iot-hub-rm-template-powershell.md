---
title: "使用範本建立 Azure IoT 中樞 (PowerShell) | Microsoft Docs"
description: "如何在 PowerShell 中使用 Azure Resource Manager 範本建立 IoT 中樞。"
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
ms.openlocfilehash: f83fac6cffc9e58582417324a4348ca3b6220f0c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="create-an-iot-hub-using-azure-resource-manager-template-powershell"></a><span data-ttu-id="049cb-103">使用 Azure Resource Manager 範本建立 IoT 中樞 (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="049cb-103">Create an IoT hub using Azure Resource Manager template (PowerShell)</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

<span data-ttu-id="049cb-104">您可以使用 Azure 資源管理員，以程式設計方式建立和管理 Azure IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="049cb-104">You can use Azure Resource Manager to create and manage Azure IoT hubs programmatically.</span></span> <span data-ttu-id="049cb-105">本教學課程示範如何使用 Azure Resource Manager 範本以 PowerShell 建立 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="049cb-105">This tutorial shows you how to use an Azure Resource Manager template to create an IoT hub with PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="049cb-106">Azure 建立和處理資源的部署模型有兩種：[Azure Resource Manager](../azure-resource-manager/resource-manager-deployment-model.md) 和傳統。</span><span class="sxs-lookup"><span data-stu-id="049cb-106">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="049cb-107">本文涵蓋使用 Azure Resource Manager 部署模型的部分。</span><span class="sxs-lookup"><span data-stu-id="049cb-107">This article covers using the Azure Resource Manager deployment model.</span></span>

<span data-ttu-id="049cb-108">若要完成此教學課程，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="049cb-108">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="049cb-109">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="049cb-109">An active Azure account.</span></span> <br/><span data-ttu-id="049cb-110">如果您沒有帳戶，只需要幾分鐘的時間就可以建立[免費帳戶][lnk-free-trial]。</span><span class="sxs-lookup"><span data-stu-id="049cb-110">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="049cb-111">[Azure PowerShell 1.0][lnk-powershell-install] 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="049cb-111">[Azure PowerShell 1.0][lnk-powershell-install] or later.</span></span>

> [!TIP]
> <span data-ttu-id="049cb-112">[搭配使用 Azure PowerShell 與 Azure Resource Manager][lnk-powershell-arm] 一文提供有關如何使用 PowerShell 和 Azure Resource Manager 範本來建立 Azure 資源的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="049cb-112">The article [Using Azure PowerShell with Azure Resource Manager][lnk-powershell-arm] provides more information about how to use PowerShell and Azure Resource Manager templates to create Azure resources.</span></span>

## <a name="connect-to-your-azure-subscription"></a><span data-ttu-id="049cb-113">連接到 Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="049cb-113">Connect to your Azure subscription</span></span>

<span data-ttu-id="049cb-114">在 PowerShell 命令提示字元中，輸入下列命令來登入您的 Azure 訂用帳戶：</span><span class="sxs-lookup"><span data-stu-id="049cb-114">In a PowerShell command prompt, enter the following command to sign in to your Azure subscription:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="049cb-115">如果您有多個 Azure 訂用帳戶，則登入 Azure 即會為您授與和您認證相關聯之所有 Azure 訂用帳戶的存取權。</span><span class="sxs-lookup"><span data-stu-id="049cb-115">If you have multiple Azure subscriptions, signing in to Azure grants you access to all the Azure subscriptions associated with your credentials.</span></span> <span data-ttu-id="049cb-116">使用下列命令來列出可供您使用的 Azure 訂用帳戶：</span><span class="sxs-lookup"><span data-stu-id="049cb-116">Use the following command to list the Azure subscriptions available for you to use:</span></span>

```powershell
Get-AzureRMSubscription
```

<span data-ttu-id="049cb-117">使用下列命令，選取您想要用來執行命令以建立 IoT 中樞的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="049cb-117">Use the following command to select subscription that you want to use to run the commands to create your IoT hub.</span></span> <span data-ttu-id="049cb-118">您可以使用來自上一個命令之輸出內的訂用帳戶名稱或識別碼︰</span><span class="sxs-lookup"><span data-stu-id="049cb-118">You can use either the subscription name or ID from the output of the previous command:</span></span>

```powershell
Select-AzureRMSubscription `
    -SubscriptionName "{your subscription name}"
```

<span data-ttu-id="049cb-119">您可以使用下列命令來探索可部署 IoT 中樞的位置和目前支援的 API 版本：</span><span class="sxs-lookup"><span data-stu-id="049cb-119">You can use the following commands to discover where you can deploy an IoT hub and the currently supported API versions:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Devices).ResourceTypes | Where-Object ResourceTypeName -eq IoTHubs).Locations
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Devices).ResourceTypes | Where-Object ResourceTypeName -eq IoTHubs).ApiVersions
```

<span data-ttu-id="049cb-120">在 IoT 中樞支援的其中一個位置，使用下列命令建立資源群組來包含您的 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="049cb-120">Create a resource group to contain your IoT hub using the following command in one of the supported locations for IoT Hub.</span></span> <span data-ttu-id="049cb-121">這個範例會建立一個稱為 **MyIoTRG1**的資源群組：</span><span class="sxs-lookup"><span data-stu-id="049cb-121">This example creates a resource group called **MyIoTRG1**:</span></span>

```powershell
New-AzureRmResourceGroup -Name MyIoTRG1 -Location "East US"
```

## <a name="submit-a-template-to-create-an-iot-hub"></a><span data-ttu-id="049cb-122">提交範本，以建立 IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="049cb-122">Submit a template to create an IoT hub</span></span>

<span data-ttu-id="049cb-123">使用 JSON 範本在資源群組中建立 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="049cb-123">Use a JSON template to create an IoT hub in your resource group.</span></span> <span data-ttu-id="049cb-124">您也可以使用 Azure Resource Manager 範本來對現有的 IoT 中樞進行變更。</span><span class="sxs-lookup"><span data-stu-id="049cb-124">You can also use an Azure Resource Manager template to make changes to an existing IoT hub.</span></span>

1. <span data-ttu-id="049cb-125">使用文字編輯器來建立名為 **template.json** 的 Azure Resource Manager 範本，其中包含下列資源定義來建立新的標準 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="049cb-125">Use a text editor to create an Azure Resource Manager template called **template.json** with the following resource definition to create a new standard IoT hub.</span></span> <span data-ttu-id="049cb-126">這個範例會在「美國東部」區域新增「IoT 中樞」、在「事件中樞」相容端點上建立兩個取用者群組 (**cg1** 和 **cg2**)，並使用 **2016-02-03** API 版本。</span><span class="sxs-lookup"><span data-stu-id="049cb-126">This example adds the IoT Hub in the **East US** region, creates two consumer groups (**cg1** and **cg2**) on the Event Hub-compatible endpoint, and uses the **2016-02-03** API version.</span></span> <span data-ttu-id="049cb-127">這個範本也要求您在一個名為 **hubName**的參數中傳入 IoT 中樞名稱。</span><span class="sxs-lookup"><span data-stu-id="049cb-127">This template also expects you to pass in the IoT hub name as a parameter called **hubName**.</span></span> <span data-ttu-id="049cb-128">如需目前支援「IoT 中樞」的位置清單，請參閱 [Azure 狀態][lnk-status]。</span><span class="sxs-lookup"><span data-stu-id="049cb-128">For the current list of locations that support IoT Hub see [Azure Status][lnk-status].</span></span>

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

2. <span data-ttu-id="049cb-129">將 Azure Resource Manager 範本檔案儲存在您的本機電腦上。</span><span class="sxs-lookup"><span data-stu-id="049cb-129">Save the Azure Resource Manager template file on your local machine.</span></span> <span data-ttu-id="049cb-130">這個範例假設您將它儲存在名為 **c:\templates** 的資料夾中。</span><span class="sxs-lookup"><span data-stu-id="049cb-130">This example assumes you save it in a folder called **c:\templates**.</span></span>

3. <span data-ttu-id="049cb-131">執行下列命令來部署新的 IoT 中樞，並傳遞 IoT 中樞的名稱做為參數。</span><span class="sxs-lookup"><span data-stu-id="049cb-131">Run the following command to deploy your new IoT hub, passing the name of your IoT hub as a parameter.</span></span> <span data-ttu-id="049cb-132">在此範例中，IoT 中樞的名稱是 `abcmyiothub`。</span><span class="sxs-lookup"><span data-stu-id="049cb-132">In this example, the name of the IoT hub is `abcmyiothub`.</span></span> <span data-ttu-id="049cb-133">您的 IoT 中樞名稱必須是全域唯一：</span><span class="sxs-lookup"><span data-stu-id="049cb-133">The name of your IoT hub must be globally unique:</span></span>

    ```powershell
    New-AzureRmResourceGroupDeployment -ResourceGroupName MyIoTRG1 -TemplateFile C:\templates\template.json -hubName abcmyiothub
    ```
  [!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

4. <span data-ttu-id="049cb-134">輸出會顯示您建立的 IoT 中樞的金鑰。</span><span class="sxs-lookup"><span data-stu-id="049cb-134">The output displays the keys for the IoT hub you created.</span></span>

5. <span data-ttu-id="049cb-135">若要確認您的應用程式已新增新的 IoT 中樞，請前往 [Azure 入口網站][ lnk-azure-portal]並檢視您的資源清單。</span><span class="sxs-lookup"><span data-stu-id="049cb-135">To verify your application added the new IoT hub, visit the [Azure portal][lnk-azure-portal] and view your list of resources.</span></span> <span data-ttu-id="049cb-136">或者，使用 **Get-AzureRmResource** PowerShell Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="049cb-136">Alternatively, use the **Get-AzureRmResource** PowerShell cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="049cb-137">此範例應用程式會加入您付費的「S1 標準 IoT 中樞」。</span><span class="sxs-lookup"><span data-stu-id="049cb-137">This example application adds an S1 Standard IoT Hub for which you are billed.</span></span> <span data-ttu-id="049cb-138">您可透過 [Azure 入口網站][lnk-azure-portal]刪除此 IoT 中樞，或在完成時，使用 **Remove-AzureRmResource** PowerShell Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="049cb-138">You can delete the IoT hub through the [Azure portal][lnk-azure-portal] or by using the **Remove-AzureRmResource** PowerShell cmdlet when you are finished.</span></span>

## <a name="next-steps"></a><span data-ttu-id="049cb-139">後續步驟</span><span class="sxs-lookup"><span data-stu-id="049cb-139">Next steps</span></span>

<span data-ttu-id="049cb-140">現在您已使用 Azure Resource Manager 範本搭配 PowerShell 來部署 IoT 中樞，您可以再進一步探索：</span><span class="sxs-lookup"><span data-stu-id="049cb-140">Now you have deployed an IoT hub using an Azure Resource Manager template with PowerShell, you may want to explore further:</span></span>

* <span data-ttu-id="049cb-141">閱讀 [IoT 中樞資源提供者 REST API][lnk-rest-api] 功能的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="049cb-141">Read about the capabilities of the [IoT Hub resource provider REST API][lnk-rest-api].</span></span>
* <span data-ttu-id="049cb-142">如需 Azure Resource Manager 功能的詳細資訊，請參閱 [Azure Resource Manager 概觀][lnk-azure-rm-overview]。</span><span class="sxs-lookup"><span data-stu-id="049cb-142">Read [Azure Resource Manager overview][lnk-azure-rm-overview] to learn more about the capabilities of Azure Resource Manager.</span></span>

<span data-ttu-id="049cb-143">若要深入了解如何開發 IoT 中樞，請參閱以下文章︰</span><span class="sxs-lookup"><span data-stu-id="049cb-143">To learn more about developing for IoT Hub, see the following articles:</span></span>

* <span data-ttu-id="049cb-144">[C SDK 簡介][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="049cb-144">[Introduction to C SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="049cb-145">[Azure IoT SDK][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="049cb-145">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="049cb-146">若要進一步探索 IoT 中樞的功能，請參閱︰</span><span class="sxs-lookup"><span data-stu-id="049cb-146">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="049cb-147">[使用 Azure IoT Edge 來模擬裝置][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="049cb-147">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

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
