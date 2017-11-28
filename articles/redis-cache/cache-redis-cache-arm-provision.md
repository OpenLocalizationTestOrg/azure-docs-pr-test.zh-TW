---
title: "使用 Azure Resource Manager 佈建 Redis Cache | Microsoft Docs"
description: "使用 Azure 資源管理員範本來部署 Azure Redis 快取。"
services: app-service
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: ce6f5372-7038-4655-b1c5-108f7c148282
ms.service: cache
ms.workload: web
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: sdanie
ms.openlocfilehash: cce5d63e8bad2dd066cb4c28e2a8a9cb16c47953
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-redis-cache-using-a-template"></a><span data-ttu-id="01689-103">使用範本建立 Redis 快取</span><span class="sxs-lookup"><span data-stu-id="01689-103">Create a Redis Cache using a template</span></span>
<span data-ttu-id="01689-104">在本主題中，您將學習如何建立 Azure Resource Manager 範本，以部署 Azure Redis 快取。</span><span class="sxs-lookup"><span data-stu-id="01689-104">In this topic, you learn how to create an Azure Resource Manager template that deploys an Azure Redis Cache.</span></span> <span data-ttu-id="01689-105">快取可以搭配現有的儲存體帳戶以保留診斷資料。</span><span class="sxs-lookup"><span data-stu-id="01689-105">The cache can be used with an existing storage account to keep diagnostic data.</span></span> <span data-ttu-id="01689-106">您將學習如何定義要部署哪些資源，以及如何定義執行部署時所指定的參數。</span><span class="sxs-lookup"><span data-stu-id="01689-106">You also learn how to define which resources are deployed and how to define parameters that are specified when the deployment is executed.</span></span> <span data-ttu-id="01689-107">您可以直接在自己的部署中使用此範本，或自訂此範本以符合您的需求。</span><span class="sxs-lookup"><span data-stu-id="01689-107">You can use this template for your own deployments, or customize it to meet your requirements.</span></span>

<span data-ttu-id="01689-108">目前對於訂用帳戶，同一區域中所有快取的診斷設定是共用的。</span><span class="sxs-lookup"><span data-stu-id="01689-108">Currently, diagnostic settings are shared for all caches in the same region for a subscription.</span></span> <span data-ttu-id="01689-109">更新區域中的一個快取將會影響區域中的所有其他快取。</span><span class="sxs-lookup"><span data-stu-id="01689-109">Updating one cache in the region affects all other caches in the region.</span></span>

<span data-ttu-id="01689-110">如需關於建立範本的詳細資訊，請參閱 [編寫 Azure 資源管理員範本](../azure-resource-manager/resource-group-authoring-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="01689-110">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="01689-111">如需完整範本，請參閱 [Redis 快取範本](https://github.com/Azure/azure-quickstart-templates/blob/master/101-redis-cache/azuredeploy.json)。</span><span class="sxs-lookup"><span data-stu-id="01689-111">For the complete template, see [Redis Cache template](https://github.com/Azure/azure-quickstart-templates/blob/master/101-redis-cache/azuredeploy.json).</span></span>

> [!NOTE]
> <span data-ttu-id="01689-112">新 [Premium 層](cache-premium-tier-intro.md) 中有可用的 Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="01689-112">Resource Manager templates for the new [Premium tier](cache-premium-tier-intro.md) are available.</span></span> 
> 
> * [<span data-ttu-id="01689-113">建立具有叢集的 Premium Redis 快取</span><span class="sxs-lookup"><span data-stu-id="01689-113">Create a Premium Redis Cache with clustering</span></span>](https://azure.microsoft.com/documentation/templates/201-redis-premium-cluster-diagnostics/)
> * [<span data-ttu-id="01689-114">建立具有資料永續性的 Premium Redis 快取</span><span class="sxs-lookup"><span data-stu-id="01689-114">Create Premium Redis Cache with data persistence</span></span>](https://azure.microsoft.com/documentation/templates/201-redis-premium-persistence/)
> * [<span data-ttu-id="01689-115">建立具有 VNet 和選擇性叢集的 Premium Redis 快取</span><span class="sxs-lookup"><span data-stu-id="01689-115">Create Premium Redis Cache with VNet and optional clustering</span></span>](https://azure.microsoft.com/documentation/templates/201-redis-premium-vnet-cluster-diagnostics/)
> 
> <span data-ttu-id="01689-116">若要查看最新的範本，請參閱 [Azure 快速入門範本](https://azure.microsoft.com/documentation/templates/)並搜尋 `Redis Cache`。</span><span class="sxs-lookup"><span data-stu-id="01689-116">To check for the latest templates, see [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates/) and search for `Redis Cache`.</span></span>
> 
> 

## <a name="what-you-will-deploy"></a><span data-ttu-id="01689-117">部署內容</span><span class="sxs-lookup"><span data-stu-id="01689-117">What you will deploy</span></span>
<span data-ttu-id="01689-118">在此範本中，您將部署使用現有儲存體帳戶的 Azure Redis 快取來診斷資料。</span><span class="sxs-lookup"><span data-stu-id="01689-118">In this template, you will deploy an Azure Redis Cache that uses an existing storage account for diagnostic data.</span></span>

<span data-ttu-id="01689-119">若要自動執行部署，請按一下下列按鈕：</span><span class="sxs-lookup"><span data-stu-id="01689-119">To run the deployment automatically, click the following button:</span></span>

<span data-ttu-id="01689-120">[![部署至 Azure](./media/cache-redis-cache-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-redis-cache%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="01689-120">[![Deploy to Azure](./media/cache-redis-cache-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-redis-cache%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="01689-121">參數</span><span class="sxs-lookup"><span data-stu-id="01689-121">Parameters</span></span>
<span data-ttu-id="01689-122">透過 Azure 資源管理員，您可以定義在部署範本時想要指定之值的參數。</span><span class="sxs-lookup"><span data-stu-id="01689-122">With Azure Resource Manager, you define parameters for values you want to specify when the template is deployed.</span></span> <span data-ttu-id="01689-123">此範本有一個 Parameters 區段，內含所有參數值。</span><span class="sxs-lookup"><span data-stu-id="01689-123">The template includes a section called Parameters that contains all of the parameter values.</span></span>
<span data-ttu-id="01689-124">您應該為會隨著要部署的專案或要部署到的環境而變化的值定義參數。</span><span class="sxs-lookup"><span data-stu-id="01689-124">You should define a parameter for those values that vary based on the project you are deploying or based on the environment you are deploying to.</span></span> <span data-ttu-id="01689-125">請不要為永遠保持不變的值定義參數。</span><span class="sxs-lookup"><span data-stu-id="01689-125">Do not define parameters for values that always stay the same.</span></span> <span data-ttu-id="01689-126">每個參數值都可在範本中用來定義所部署的資源。</span><span class="sxs-lookup"><span data-stu-id="01689-126">Each parameter value is used in the template to define the resources that are deployed.</span></span> 

[!INCLUDE [app-service-web-deploy-redis-parameters](../../includes/cache-deploy-parameters.md)]

### <a name="rediscachelocation"></a><span data-ttu-id="01689-127">redisCacheLocation</span><span class="sxs-lookup"><span data-stu-id="01689-127">redisCacheLocation</span></span>
<span data-ttu-id="01689-128">Redis 快取的位置。</span><span class="sxs-lookup"><span data-stu-id="01689-128">The location of the Redis Cache.</span></span> <span data-ttu-id="01689-129">針對最佳效能，使用要與快取搭配使用之應用程式相同的位置。</span><span class="sxs-lookup"><span data-stu-id="01689-129">For best performance, use the same location as the app to be used with the cache.</span></span>

    "redisCacheLocation": {
      "type": "string"
    }

### <a name="existingdiagnosticsstorageaccountname"></a><span data-ttu-id="01689-130">existingDiagnosticsStorageAccountName</span><span class="sxs-lookup"><span data-stu-id="01689-130">existingDiagnosticsStorageAccountName</span></span>
<span data-ttu-id="01689-131">要用於診斷的現有儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="01689-131">The name of the existing storage account to use for diagnostics.</span></span> 

    "existingDiagnosticsStorageAccountName": {
      "type": "string"
    }

### <a name="enablenonsslport"></a><span data-ttu-id="01689-132">enableNonSslPort</span><span class="sxs-lookup"><span data-stu-id="01689-132">enableNonSslPort</span></span>
<span data-ttu-id="01689-133">指出是否允許透過非 SSL 連接埠存取的布林值。</span><span class="sxs-lookup"><span data-stu-id="01689-133">A boolean value that indicates whether to allow access via non-SSL ports.</span></span>

    "enableNonSslPort": {
      "type": "bool"
    }

### <a name="diagnosticsstatus"></a><span data-ttu-id="01689-134">diagnosticsStatus</span><span class="sxs-lookup"><span data-stu-id="01689-134">diagnosticsStatus</span></span>
<span data-ttu-id="01689-135">指出診斷是否啟用的值。</span><span class="sxs-lookup"><span data-stu-id="01689-135">A value that indicates whether diagnostics is enabled.</span></span> <span data-ttu-id="01689-136">使用 ON 或 OFF。</span><span class="sxs-lookup"><span data-stu-id="01689-136">Use ON or OFF.</span></span>

    "diagnosticsStatus": {
      "type": "string",
      "defaultValue": "ON",
      "allowedValues": [
            "ON",
            "OFF"
        ]
    }

## <a name="resources-to-deploy"></a><span data-ttu-id="01689-137">要部署的資源</span><span class="sxs-lookup"><span data-stu-id="01689-137">Resources to deploy</span></span>
### <a name="redis-cache"></a><span data-ttu-id="01689-138">Redis 快取</span><span class="sxs-lookup"><span data-stu-id="01689-138">Redis Cache</span></span>
<span data-ttu-id="01689-139">建立 Azure Redis 快取。</span><span class="sxs-lookup"><span data-stu-id="01689-139">Creates the Azure Redis Cache.</span></span>

    {
      "apiVersion": "2015-08-01",
      "name": "[parameters('redisCacheName')]",
      "type": "Microsoft.Cache/Redis",
      "location": "[parameters('redisCacheLocation')]",
      "properties": {
        "enableNonSslPort": "[parameters('enableNonSslPort')]",
        "sku": {
          "capacity": "[parameters('redisCacheCapacity')]",
          "family": "[parameters('redisCacheFamily')]",
          "name": "[parameters('redisCacheSKU')]"
        }
      },
      "resources": [
        {
          "apiVersion": "2015-07-01",
          "type": "Microsoft.Cache/redis/providers/diagnosticsettings",
          "name": "[concat(parameters('redisCacheName'), '/Microsoft.Insights/service')]",
          "location": "[parameters('redisCacheLocation')]",
          "dependsOn": [
            "[concat('Microsoft.Cache/Redis/', parameters('redisCacheName'))]"
          ],
          "properties": {
            "status": "[parameters('diagnosticsStatus')]",
            "storageAccountName": "[parameters('existingDiagnosticsStorageAccountName')]"
          }
        }
      ]
    }



## <a name="commands-to-run-deployment"></a><span data-ttu-id="01689-140">執行部署的命令</span><span class="sxs-lookup"><span data-stu-id="01689-140">Commands to run deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="01689-141">PowerShell</span><span class="sxs-lookup"><span data-stu-id="01689-141">PowerShell</span></span>
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-redis-cache/azuredeploy.json -ResourceGroupName ExampleDeployGroup -redisCacheName ExampleCache

### <a name="azure-cli"></a><span data-ttu-id="01689-142">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="01689-142">Azure CLI</span></span>
    azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-redis-cache/azuredeploy.json -g ExampleDeployGroup


