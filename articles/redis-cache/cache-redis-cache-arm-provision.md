---
title: "aaaProvision Redis 快取使用 Azure Resource Manager |Microsoft 文件"
description: "使用 Azure Resource Manager 範本 toodeploy Azure Redis 快取。"
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
ms.openlocfilehash: 46e7b3b2493ac51dbe6bab0b086304802afc5d48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-redis-cache-using-a-template"></a><span data-ttu-id="18df4-103">使用範本建立 Redis 快取</span><span class="sxs-lookup"><span data-stu-id="18df4-103">Create a Redis Cache using a template</span></span>
<span data-ttu-id="18df4-104">本主題中，在您了解如何部署 Azure Resource Manager 範本 toocreate Azure Redis 快取。</span><span class="sxs-lookup"><span data-stu-id="18df4-104">In this topic, you learn how toocreate an Azure Resource Manager template that deploys an Azure Redis Cache.</span></span> <span data-ttu-id="18df4-105">hello 快取可以搭配現有儲存體帳戶 tookeep 診斷資料。</span><span class="sxs-lookup"><span data-stu-id="18df4-105">hello cache can be used with an existing storage account tookeep diagnostic data.</span></span> <span data-ttu-id="18df4-106">您也學到如何 toodefine 部署的資源，以及如何 toodefine 參數指定當 hello 執行部署。</span><span class="sxs-lookup"><span data-stu-id="18df4-106">You also learn how toodefine which resources are deployed and how toodefine parameters that are specified when hello deployment is executed.</span></span> <span data-ttu-id="18df4-107">您可以使用此範本為您自己的部署，或自訂它 toomeet 您的需求。</span><span class="sxs-lookup"><span data-stu-id="18df4-107">You can use this template for your own deployments, or customize it toomeet your requirements.</span></span>

<span data-ttu-id="18df4-108">目前，診斷設定所有快取中共用 hello 訂用帳戶相同的區域。</span><span class="sxs-lookup"><span data-stu-id="18df4-108">Currently, diagnostic settings are shared for all caches in hello same region for a subscription.</span></span> <span data-ttu-id="18df4-109">更新 hello 區域中的一個快取會影響所有 hello 區域中的快取。</span><span class="sxs-lookup"><span data-stu-id="18df4-109">Updating one cache in hello region affects all other caches in hello region.</span></span>

<span data-ttu-id="18df4-110">如需關於建立範本的詳細資訊，請參閱 [編寫 Azure 資源管理員範本](../azure-resource-manager/resource-group-authoring-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="18df4-110">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="18df4-111">Hello 完成範本，請參閱[Redis 快取 範本](https://github.com/Azure/azure-quickstart-templates/blob/master/101-redis-cache/azuredeploy.json)。</span><span class="sxs-lookup"><span data-stu-id="18df4-111">For hello complete template, see [Redis Cache template](https://github.com/Azure/azure-quickstart-templates/blob/master/101-redis-cache/azuredeploy.json).</span></span>

> [!NOTE]
> <span data-ttu-id="18df4-112">資源管理員範本，新的 hello [Premium 層](cache-premium-tier-intro.md)可用。</span><span class="sxs-lookup"><span data-stu-id="18df4-112">Resource Manager templates for hello new [Premium tier](cache-premium-tier-intro.md) are available.</span></span> 
> 
> * [<span data-ttu-id="18df4-113">建立具有叢集的 Premium Redis 快取</span><span class="sxs-lookup"><span data-stu-id="18df4-113">Create a Premium Redis Cache with clustering</span></span>](https://azure.microsoft.com/documentation/templates/201-redis-premium-cluster-diagnostics/)
> * [<span data-ttu-id="18df4-114">建立具有資料永續性的 Premium Redis 快取</span><span class="sxs-lookup"><span data-stu-id="18df4-114">Create Premium Redis Cache with data persistence</span></span>](https://azure.microsoft.com/documentation/templates/201-redis-premium-persistence/)
> * [<span data-ttu-id="18df4-115">建立具有 VNet 和選擇性叢集的 Premium Redis 快取</span><span class="sxs-lookup"><span data-stu-id="18df4-115">Create Premium Redis Cache with VNet and optional clustering</span></span>](https://azure.microsoft.com/documentation/templates/201-redis-premium-vnet-cluster-diagnostics/)
> 
> <span data-ttu-id="18df4-116">toocheck hello 最新的範本，請參閱[Azure 快速入門範本](https://azure.microsoft.com/documentation/templates/)並搜尋`Redis Cache`。</span><span class="sxs-lookup"><span data-stu-id="18df4-116">toocheck for hello latest templates, see [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates/) and search for `Redis Cache`.</span></span>
> 
> 

## <a name="what-you-will-deploy"></a><span data-ttu-id="18df4-117">部署內容</span><span class="sxs-lookup"><span data-stu-id="18df4-117">What you will deploy</span></span>
<span data-ttu-id="18df4-118">在此範本中，您將部署使用現有儲存體帳戶的 Azure Redis 快取來診斷資料。</span><span class="sxs-lookup"><span data-stu-id="18df4-118">In this template, you will deploy an Azure Redis Cache that uses an existing storage account for diagnostic data.</span></span>

<span data-ttu-id="18df4-119">toorun 自動 hello 部署，請按一下下列按鈕 hello:</span><span class="sxs-lookup"><span data-stu-id="18df4-119">toorun hello deployment automatically, click hello following button:</span></span>

<span data-ttu-id="18df4-120">[![部署 tooAzure](./media/cache-redis-cache-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-redis-cache%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="18df4-120">[![Deploy tooAzure](./media/cache-redis-cache-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-redis-cache%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="18df4-121">參數</span><span class="sxs-lookup"><span data-stu-id="18df4-121">Parameters</span></span>
<span data-ttu-id="18df4-122">使用 Azure 資源管理員中，您定義參數的值要 toospecify 部署 hello 範本時。</span><span class="sxs-lookup"><span data-stu-id="18df4-122">With Azure Resource Manager, you define parameters for values you want toospecify when hello template is deployed.</span></span> <span data-ttu-id="18df4-123">hello 範本包括區段稱為參數，其中包含所有 hello 參數值。</span><span class="sxs-lookup"><span data-stu-id="18df4-123">hello template includes a section called Parameters that contains all of hello parameter values.</span></span>
<span data-ttu-id="18df4-124">您應該定義依據您要部署的 hello 專案，或根據您要部署的 hello 環境不同，這些值的參數。</span><span class="sxs-lookup"><span data-stu-id="18df4-124">You should define a parameter for those values that vary based on hello project you are deploying or based on hello environment you are deploying to.</span></span> <span data-ttu-id="18df4-125">不會定義參數的值一律保持 hello 相同。</span><span class="sxs-lookup"><span data-stu-id="18df4-125">Do not define parameters for values that always stay hello same.</span></span> <span data-ttu-id="18df4-126">每個參數值用於 hello 範本 toodefine hello 資源部署。</span><span class="sxs-lookup"><span data-stu-id="18df4-126">Each parameter value is used in hello template toodefine hello resources that are deployed.</span></span> 

[!INCLUDE [app-service-web-deploy-redis-parameters](../../includes/cache-deploy-parameters.md)]

### <a name="rediscachelocation"></a><span data-ttu-id="18df4-127">redisCacheLocation</span><span class="sxs-lookup"><span data-stu-id="18df4-127">redisCacheLocation</span></span>
<span data-ttu-id="18df4-128">hello hello Redis 快取位置。</span><span class="sxs-lookup"><span data-stu-id="18df4-128">hello location of hello Redis Cache.</span></span> <span data-ttu-id="18df4-129">為了達到最佳效能，使用 hello 相同 hello hello 快取搭配使用的應用程式 toobe 的位置。</span><span class="sxs-lookup"><span data-stu-id="18df4-129">For best performance, use hello same location as hello app toobe used with hello cache.</span></span>

    "redisCacheLocation": {
      "type": "string"
    }

### <a name="existingdiagnosticsstorageaccountname"></a><span data-ttu-id="18df4-130">existingDiagnosticsStorageAccountName</span><span class="sxs-lookup"><span data-stu-id="18df4-130">existingDiagnosticsStorageAccountName</span></span>
<span data-ttu-id="18df4-131">hello 名稱 hello 現有儲存體帳戶 toouse 診斷。</span><span class="sxs-lookup"><span data-stu-id="18df4-131">hello name of hello existing storage account toouse for diagnostics.</span></span> 

    "existingDiagnosticsStorageAccountName": {
      "type": "string"
    }

### <a name="enablenonsslport"></a><span data-ttu-id="18df4-132">enableNonSslPort</span><span class="sxs-lookup"><span data-stu-id="18df4-132">enableNonSslPort</span></span>
<span data-ttu-id="18df4-133">布林值，指出是否 tooallow 存取透過非 SSL 連接埠。</span><span class="sxs-lookup"><span data-stu-id="18df4-133">A boolean value that indicates whether tooallow access via non-SSL ports.</span></span>

    "enableNonSslPort": {
      "type": "bool"
    }

### <a name="diagnosticsstatus"></a><span data-ttu-id="18df4-134">diagnosticsStatus</span><span class="sxs-lookup"><span data-stu-id="18df4-134">diagnosticsStatus</span></span>
<span data-ttu-id="18df4-135">指出診斷是否啟用的值。</span><span class="sxs-lookup"><span data-stu-id="18df4-135">A value that indicates whether diagnostics is enabled.</span></span> <span data-ttu-id="18df4-136">使用 ON 或 OFF。</span><span class="sxs-lookup"><span data-stu-id="18df4-136">Use ON or OFF.</span></span>

    "diagnosticsStatus": {
      "type": "string",
      "defaultValue": "ON",
      "allowedValues": [
            "ON",
            "OFF"
        ]
    }

## <a name="resources-toodeploy"></a><span data-ttu-id="18df4-137">資源 toodeploy</span><span class="sxs-lookup"><span data-stu-id="18df4-137">Resources toodeploy</span></span>
### <a name="redis-cache"></a><span data-ttu-id="18df4-138">Redis 快取</span><span class="sxs-lookup"><span data-stu-id="18df4-138">Redis Cache</span></span>
<span data-ttu-id="18df4-139">建立 hello Azure Redis 快取。</span><span class="sxs-lookup"><span data-stu-id="18df4-139">Creates hello Azure Redis Cache.</span></span>

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



## <a name="commands-toorun-deployment"></a><span data-ttu-id="18df4-140">命令 toorun 部署</span><span class="sxs-lookup"><span data-stu-id="18df4-140">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="18df4-141">PowerShell</span><span class="sxs-lookup"><span data-stu-id="18df4-141">PowerShell</span></span>
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-redis-cache/azuredeploy.json -ResourceGroupName ExampleDeployGroup -redisCacheName ExampleCache

### <a name="azure-cli"></a><span data-ttu-id="18df4-142">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="18df4-142">Azure CLI</span></span>
    azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-redis-cache/azuredeploy.json -g ExampleDeployGroup


