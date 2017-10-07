---
title: "aaaProvision Redis 快取的 Web 應用程式"
description: "Azure Resource Manager 範本 toodeploy web 應用程式使用 Redis 快取。"
services: app-service
documentationcenter: 
author: steved0x
manager: erickson-doug
editor: 
ms.assetid: 6e99c71f-ef8e-4570-a307-e4c059e60c35
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: sdanie
ms.openlocfilehash: b95b5e230dc40c1157940c2017cba836975b6930
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-plus-redis-cache-using-a-template"></a><span data-ttu-id="d6a34-103">使用範本建立 Web 應用程式和 Redis 快取</span><span class="sxs-lookup"><span data-stu-id="d6a34-103">Create a Web App plus Redis Cache using a template</span></span>
<span data-ttu-id="d6a34-104">在本主題中，您將學習如何 toocreate 部署 Azure Web 應用程式使用 Redis 快取的 Azure Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="d6a34-104">In this topic, you will learn how toocreate an Azure Resource Manager template that deploys an Azure Web App with Redis cache.</span></span> <span data-ttu-id="d6a34-105">您將學習如何 toodefine 部署的資源，以及如何 toodefine 參數指定當 hello 執行部署。</span><span class="sxs-lookup"><span data-stu-id="d6a34-105">You will learn how toodefine which resources are deployed and how toodefine parameters that are specified when hello deployment is executed.</span></span> <span data-ttu-id="d6a34-106">您可以使用此範本為您自己的部署，或自訂它 toomeet 您的需求。</span><span class="sxs-lookup"><span data-stu-id="d6a34-106">You can use this template for your own deployments, or customize it toomeet your requirements.</span></span>

<span data-ttu-id="d6a34-107">如需關於建立範本的詳細資訊，請參閱 [編寫 Azure 資源管理員範本](../azure-resource-manager/resource-group-authoring-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="d6a34-107">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="d6a34-108">Hello 完成範本，請參閱[Web 應用程式使用 Redis 快取範本](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-with-redis-cache/azuredeploy.json)。</span><span class="sxs-lookup"><span data-stu-id="d6a34-108">For hello complete template, see [Web App with Redis Cache template](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-with-redis-cache/azuredeploy.json).</span></span>

## <a name="what-you-will-deploy"></a><span data-ttu-id="d6a34-109">部署內容</span><span class="sxs-lookup"><span data-stu-id="d6a34-109">What you will deploy</span></span>
<span data-ttu-id="d6a34-110">在此範本中，您將部署：</span><span class="sxs-lookup"><span data-stu-id="d6a34-110">In this template, you will deploy:</span></span>

* <span data-ttu-id="d6a34-111">Azure Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="d6a34-111">Azure Web App</span></span>
* <span data-ttu-id="d6a34-112">Azure Redis 快取.</span><span class="sxs-lookup"><span data-stu-id="d6a34-112">Azure Redis Cache.</span></span>

<span data-ttu-id="d6a34-113">toorun 自動 hello 部署，請按一下下列按鈕 hello:</span><span class="sxs-lookup"><span data-stu-id="d6a34-113">toorun hello deployment automatically, click hello following button:</span></span>

<span data-ttu-id="d6a34-114">[![部署 tooAzure](./media/cache-web-app-arm-with-redis-cache-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-with-redis-cache%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="d6a34-114">[![Deploy tooAzure](./media/cache-web-app-arm-with-redis-cache-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-with-redis-cache%2Fazuredeploy.json)</span></span>

## <a name="parameters-toospecify"></a><span data-ttu-id="d6a34-115">參數 toospecify</span><span class="sxs-lookup"><span data-stu-id="d6a34-115">Parameters toospecify</span></span>
[!INCLUDE [app-service-web-deploy-web-parameters](../../includes/app-service-web-deploy-web-parameters.md)]

[!INCLUDE [cache-deploy-parameters](../../includes/cache-deploy-parameters.md)]

## <a name="variables-for-names"></a><span data-ttu-id="d6a34-116">名稱的變數</span><span class="sxs-lookup"><span data-stu-id="d6a34-116">Variables for names</span></span>
<span data-ttu-id="d6a34-117">此範本會使用變數 tooconstruct hello 資源名稱。</span><span class="sxs-lookup"><span data-stu-id="d6a34-117">This template uses variables tooconstruct names for hello resources.</span></span> <span data-ttu-id="d6a34-118">它會使用 hello [uniqueString](../azure-resource-manager/resource-group-template-functions-string.md#uniquestring)函式的 tooconstruct 值根據資源群組識別碼。</span><span class="sxs-lookup"><span data-stu-id="d6a34-118">It uses hello [uniqueString](../azure-resource-manager/resource-group-template-functions-string.md#uniquestring) function tooconstruct a value based on the resource group id.</span></span>

    "variables": {
      "hostingPlanName": "[concat('hostingplan', uniqueString(resourceGroup().id))]",
      "webSiteName": "[concat('webSite', uniqueString(resourceGroup().id))]",
      "cacheName": "[concat('cache', uniqueString(resourceGroup().id))]"
    },


## <a name="resources-toodeploy"></a><span data-ttu-id="d6a34-119">資源 toodeploy</span><span class="sxs-lookup"><span data-stu-id="d6a34-119">Resources toodeploy</span></span>
[!INCLUDE [app-service-web-deploy-web-host](../../includes/app-service-web-deploy-web-host.md)]

### <a name="redis-cache"></a><span data-ttu-id="d6a34-120">Redis 快取</span><span class="sxs-lookup"><span data-stu-id="d6a34-120">Redis Cache</span></span>
<span data-ttu-id="d6a34-121">建立 hello Azure Redis 快取與 hello web 應用程式搭配使用。</span><span class="sxs-lookup"><span data-stu-id="d6a34-121">Creates hello Azure Redis Cache that is used with hello web app.</span></span> <span data-ttu-id="d6a34-122">hello hello 快取名稱會指定在 hello **cacheName**變數。</span><span class="sxs-lookup"><span data-stu-id="d6a34-122">hello name of hello cache is specified in hello **cacheName** variable.</span></span>

<span data-ttu-id="d6a34-123">hello 範本建立 hello 快取在 hello 與 hello 資源群組相同的位置。</span><span class="sxs-lookup"><span data-stu-id="d6a34-123">hello template creates hello cache in hello same location as hello resource group.</span></span>

    {
      "name": "[variables('cacheName')]",
      "type": "Microsoft.Cache/Redis",
      "location": "[resourceGroup().location]",
      "apiVersion": "2015-08-01",
      "dependsOn": [ ],
      "tags": {
        "displayName": "cache"
      },
      "properties": {
        "sku": {
          "name": "[parameters('cacheSKUName')]",
          "family": "[parameters('cacheSKUFamily')]",
          "capacity": "[parameters('cacheSKUCapacity')]"
        }
      }
    }


### <a name="web-app"></a><span data-ttu-id="d6a34-124">Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="d6a34-124">Web app</span></span>
<span data-ttu-id="d6a34-125">Hello 中指定的名稱建立 hello web 應用程式**webSiteName**變數。</span><span class="sxs-lookup"><span data-stu-id="d6a34-125">Creates hello web app with name specified in hello **webSiteName** variable.</span></span>

<span data-ttu-id="d6a34-126">請注意該 hello web 應用程式會設定與應用程式設定屬性，使其 toowork 以 hello Redis 快取。</span><span class="sxs-lookup"><span data-stu-id="d6a34-126">Notice that hello web app is configured with app setting properties that enable it toowork with hello Redis Cache.</span></span> <span data-ttu-id="d6a34-127">此應用程式設定是根據部署期間所提供的值動態建立。</span><span class="sxs-lookup"><span data-stu-id="d6a34-127">This app settings are dynamically created based on values provided during deployment.</span></span>

    {
      "apiVersion": "2015-08-01",
      "name": "[variables('webSiteName')]",
      "type": "Microsoft.Web/sites",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Web/serverFarms/', variables('hostingPlanName'))]",
        "[concat('Microsoft.Cache/Redis/', variables('cacheName'))]"
      ],
      "tags": {
        "[concat('hidden-related:', resourceGroup().id, '/providers/Microsoft.Web/serverfarms/', variables('hostingPlanName'))]": "empty",
        "displayName": "Website"
      },
      "properties": {
        "name": "[variables('webSiteName')]",
        "serverFarmId": "[resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName'))]"
      },
      "resources": [
        {
          "apiVersion": "2015-08-01",
          "type": "config",
          "name": "appsettings",
          "dependsOn": [
            "[concat('Microsoft.Web/Sites/', variables('webSiteName'))]",
            "[concat('Microsoft.Cache/Redis/', variables('cacheName'))]"
          ],
          "properties": {
            "CacheConnection": "[concat(variables('cacheName'),'.redis.cache.windows.net,abortConnect=false,ssl=true,password=', listKeys(resourceId('Microsoft.Cache/Redis', variables('cacheName')), '2015-08-01').primaryKey)]"
          }
        }
      ]
    }

## <a name="commands-toorun-deployment"></a><span data-ttu-id="d6a34-128">命令 toorun 部署</span><span class="sxs-lookup"><span data-stu-id="d6a34-128">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="d6a34-129">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d6a34-129">PowerShell</span></span>
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-with-redis-cache/azuredeploy.json -ResourceGroupName ExampleDeployGroup

### <a name="azure-cli"></a><span data-ttu-id="d6a34-130">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="d6a34-130">Azure CLI</span></span>
    azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-with-redis-cache/azuredeploy.json -g ExampleDeployGroup
