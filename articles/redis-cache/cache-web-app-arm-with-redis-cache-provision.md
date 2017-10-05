---
title: "佈建 Web 應用程式和 Redis 快取"
description: "使用 Azure 資源管理員範本來部署 Web 應用程式和 Redis 快取。"
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
ms.openlocfilehash: 810c1cedd4fe0bd6ecdf9bd32dfb241f5f345300
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-web-app-plus-redis-cache-using-a-template"></a><span data-ttu-id="be47e-103">使用範本建立 Web 應用程式和 Redis 快取</span><span class="sxs-lookup"><span data-stu-id="be47e-103">Create a Web App plus Redis Cache using a template</span></span>
<span data-ttu-id="be47e-104">在本主題中，您將學習如何建立 Azure 資源管理員範本，以部署 Azure Web 應用程式和 Redis 快取。</span><span class="sxs-lookup"><span data-stu-id="be47e-104">In this topic, you will learn how to create an Azure Resource Manager template that deploys an Azure Web App with Redis cache.</span></span> <span data-ttu-id="be47e-105">您將學習如何定義要部署哪些資源，以及如何定義執行部署時所指定的參數。</span><span class="sxs-lookup"><span data-stu-id="be47e-105">You will learn how to define which resources are deployed and how to define parameters that are specified when the deployment is executed.</span></span> <span data-ttu-id="be47e-106">您可以直接在自己的部署中使用此範本，或自訂此範本以符合您的需求。</span><span class="sxs-lookup"><span data-stu-id="be47e-106">You can use this template for your own deployments, or customize it to meet your requirements.</span></span>

<span data-ttu-id="be47e-107">如需關於建立範本的詳細資訊，請參閱 [編寫 Azure 資源管理員範本](../azure-resource-manager/resource-group-authoring-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="be47e-107">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="be47e-108">如需完整的範本，請參閱 [Web 應用程式與 Redis 快取 範本](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-with-redis-cache/azuredeploy.json)。</span><span class="sxs-lookup"><span data-stu-id="be47e-108">For the complete template, see [Web App with Redis Cache template](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-with-redis-cache/azuredeploy.json).</span></span>

## <a name="what-you-will-deploy"></a><span data-ttu-id="be47e-109">部署內容</span><span class="sxs-lookup"><span data-stu-id="be47e-109">What you will deploy</span></span>
<span data-ttu-id="be47e-110">在此範本中，您將部署：</span><span class="sxs-lookup"><span data-stu-id="be47e-110">In this template, you will deploy:</span></span>

* <span data-ttu-id="be47e-111">Azure Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="be47e-111">Azure Web App</span></span>
* <span data-ttu-id="be47e-112">Azure Redis 快取.</span><span class="sxs-lookup"><span data-stu-id="be47e-112">Azure Redis Cache.</span></span>

<span data-ttu-id="be47e-113">若要自動執行部署，請按一下下列按鈕：</span><span class="sxs-lookup"><span data-stu-id="be47e-113">To run the deployment automatically, click the following button:</span></span>

<span data-ttu-id="be47e-114">[![部署至 Azure](./media/cache-web-app-arm-with-redis-cache-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-with-redis-cache%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="be47e-114">[![Deploy to Azure](./media/cache-web-app-arm-with-redis-cache-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-with-redis-cache%2Fazuredeploy.json)</span></span>

## <a name="parameters-to-specify"></a><span data-ttu-id="be47e-115">要指定的參數</span><span class="sxs-lookup"><span data-stu-id="be47e-115">Parameters to specify</span></span>
[!INCLUDE [app-service-web-deploy-web-parameters](../../includes/app-service-web-deploy-web-parameters.md)]

[!INCLUDE [cache-deploy-parameters](../../includes/cache-deploy-parameters.md)]

## <a name="variables-for-names"></a><span data-ttu-id="be47e-116">名稱的變數</span><span class="sxs-lookup"><span data-stu-id="be47e-116">Variables for names</span></span>
<span data-ttu-id="be47e-117">這個範本會使用變數來建構資源的名稱。</span><span class="sxs-lookup"><span data-stu-id="be47e-117">This template uses variables to construct names for the resources.</span></span> <span data-ttu-id="be47e-118">它會使用 [uniqueString](../azure-resource-manager/resource-group-template-functions-string.md#uniquestring) 函式，根據資源群組識別碼來建構值。</span><span class="sxs-lookup"><span data-stu-id="be47e-118">It uses the [uniqueString](../azure-resource-manager/resource-group-template-functions-string.md#uniquestring) function to construct a value based on the resource group id.</span></span>

    "variables": {
      "hostingPlanName": "[concat('hostingplan', uniqueString(resourceGroup().id))]",
      "webSiteName": "[concat('webSite', uniqueString(resourceGroup().id))]",
      "cacheName": "[concat('cache', uniqueString(resourceGroup().id))]"
    },


## <a name="resources-to-deploy"></a><span data-ttu-id="be47e-119">要部署的資源</span><span class="sxs-lookup"><span data-stu-id="be47e-119">Resources to deploy</span></span>
[!INCLUDE [app-service-web-deploy-web-host](../../includes/app-service-web-deploy-web-host.md)]

### <a name="redis-cache"></a><span data-ttu-id="be47e-120">Redis 快取</span><span class="sxs-lookup"><span data-stu-id="be47e-120">Redis Cache</span></span>
<span data-ttu-id="be47e-121">建立與 Web 應用程式搭配使用的 Azure Redis 快取。</span><span class="sxs-lookup"><span data-stu-id="be47e-121">Creates the Azure Redis Cache that is used with the web app.</span></span> <span data-ttu-id="be47e-122">快取的名稱指定於 **cacheName** 變數中。</span><span class="sxs-lookup"><span data-stu-id="be47e-122">The name of the cache is specified in the **cacheName** variable.</span></span>

<span data-ttu-id="be47e-123">範本會在資源群組的相同位置建立快取。</span><span class="sxs-lookup"><span data-stu-id="be47e-123">The template creates the cache in the same location as the resource group.</span></span>

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


### <a name="web-app"></a><span data-ttu-id="be47e-124">Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="be47e-124">Web app</span></span>
<span data-ttu-id="be47e-125">使用 **webSiteName** 變數中所指定的名稱來建立 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="be47e-125">Creates the web app with name specified in the **webSiteName** variable.</span></span>

<span data-ttu-id="be47e-126">請注意，Web 應用程式是使用應用程式設定屬性所設定，可讓它使用 Redis 快取。</span><span class="sxs-lookup"><span data-stu-id="be47e-126">Notice that the web app is configured with app setting properties that enable it to work with the Redis Cache.</span></span> <span data-ttu-id="be47e-127">此應用程式設定是根據部署期間所提供的值動態建立。</span><span class="sxs-lookup"><span data-stu-id="be47e-127">This app settings are dynamically created based on values provided during deployment.</span></span>

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

## <a name="commands-to-run-deployment"></a><span data-ttu-id="be47e-128">執行部署的命令</span><span class="sxs-lookup"><span data-stu-id="be47e-128">Commands to run deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="be47e-129">PowerShell</span><span class="sxs-lookup"><span data-stu-id="be47e-129">PowerShell</span></span>
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-with-redis-cache/azuredeploy.json -ResourceGroupName ExampleDeployGroup

### <a name="azure-cli"></a><span data-ttu-id="be47e-130">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="be47e-130">Azure CLI</span></span>
    azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-with-redis-cache/azuredeploy.json -g ExampleDeployGroup