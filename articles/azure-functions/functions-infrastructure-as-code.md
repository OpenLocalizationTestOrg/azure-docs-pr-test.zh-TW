---
title: "Azure Functions 中函數應用程式的自動化資源部署 | Microsoft Docs"
description: "了解如何建置能部署函數應用程式的 Azure Resource Manager 範本。"
services: Functions
documtationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: "azure functions, 函數, 無伺服器架構, 基礎結構即程式碼, azure resource manager"
ms.assetid: d20743e3-aab6-442c-a836-9bcea09bfd32
ms.server: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/25/2017
ms.author: glenga
ms.openlocfilehash: 15496e4ab2858b2aa319d53f1c438a259a3d5e49
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="automate-resource-deployment-for-your-function-app-in-azure-functions"></a><span data-ttu-id="65c93-104">Azure Functions 中函數應用程式的自動化資源部署</span><span class="sxs-lookup"><span data-stu-id="65c93-104">Automate resource deployment for your function app in Azure Functions</span></span>

<span data-ttu-id="65c93-105">您可以使用 Azure Resource Manager 範本來部署函數應用程式。</span><span class="sxs-lookup"><span data-stu-id="65c93-105">You can use an Azure Resource Manager template to deploy a function app.</span></span> <span data-ttu-id="65c93-106">本文概述執行這項作業所需的資源和參數。</span><span class="sxs-lookup"><span data-stu-id="65c93-106">This article outlines the required resources and parameters for doing so.</span></span> <span data-ttu-id="65c93-107">您可能需要部署額外的資源，視函數應用程式中的[觸發程序和繫結](functions-triggers-bindings.md)而定。</span><span class="sxs-lookup"><span data-stu-id="65c93-107">You might need to deploy additional resources, depending on the [triggers and bindings](functions-triggers-bindings.md) in your function app.</span></span>

<span data-ttu-id="65c93-108">如需關於建立範本的詳細資訊，請參閱 [編寫 Azure Resource Manager 範本](../azure-resource-manager/resource-group-authoring-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="65c93-108">For more information about creating templates, see [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="65c93-109">如需範例範本，請參閱：</span><span class="sxs-lookup"><span data-stu-id="65c93-109">For sample templates, see:</span></span>
- <span data-ttu-id="65c93-110">[採用取用方案的函數應用程式]</span><span class="sxs-lookup"><span data-stu-id="65c93-110">[Function app on Consumption plan]</span></span>
- <span data-ttu-id="65c93-111">[採用 Azure App Service 方案的函數應用程式]</span><span class="sxs-lookup"><span data-stu-id="65c93-111">[Function app on Azure App Service plan]</span></span>

## <a name="required-resources"></a><span data-ttu-id="65c93-112">所需資源</span><span class="sxs-lookup"><span data-stu-id="65c93-112">Required resources</span></span>

<span data-ttu-id="65c93-113">函數應用程式需要以下資源：</span><span class="sxs-lookup"><span data-stu-id="65c93-113">A function app requires these resources:</span></span>

* <span data-ttu-id="65c93-114">[Azure 儲存體](../storage/index.md)帳戶</span><span class="sxs-lookup"><span data-stu-id="65c93-114">An [Azure Storage](../storage/index.md) account</span></span>
* <span data-ttu-id="65c93-115">主控方案 (取用方案或 App Service 方案)</span><span class="sxs-lookup"><span data-stu-id="65c93-115">A hosting plan (Consumption plan or App Service plan)</span></span>
* <span data-ttu-id="65c93-116">函數應用程式</span><span class="sxs-lookup"><span data-stu-id="65c93-116">A function app</span></span> 

### <a name="storage-account"></a><span data-ttu-id="65c93-117">儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="65c93-117">Storage account</span></span>

<span data-ttu-id="65c93-118">函數應用程式需要 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="65c93-118">An Azure storage account is required for a function app.</span></span> <span data-ttu-id="65c93-119">您需要支援 Blob、資料表、佇列和檔案的一般用途帳戶。</span><span class="sxs-lookup"><span data-stu-id="65c93-119">You need a general purpose account that supports blobs, tables, queues, and files.</span></span> <span data-ttu-id="65c93-120">如需詳細資訊，請參閱 [Azure Functions 儲存體帳戶需求](functions-create-function-app-portal.md#storage-account-requirements)。</span><span class="sxs-lookup"><span data-stu-id="65c93-120">For more information, see [Azure Functions storage account requirements](functions-create-function-app-portal.md#storage-account-requirements).</span></span>

```json
{
    "type": "Microsoft.Storage/storageAccounts",
    "name": "[variables('storageAccountName')]",
    "apiVersion": "2015-06-15",
    "location": "[resourceGroup().location]",
    "properties": {
        "accountType": "[parameters('storageAccountType')]"
    }
}
```

<span data-ttu-id="65c93-121">此外，您必須在網站組態中將 `AzureWebJobsStorage` 和 `AzureWebJobsDashboard` 屬性指定為應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="65c93-121">In addition, the properties `AzureWebJobsStorage` and `AzureWebJobsDashboard` must be specified as app settings in the site configuration.</span></span> <span data-ttu-id="65c93-122">Azure Functions 執行階段會使用 `AzureWebJobsStorage` 連接字串來建立內部佇列。</span><span class="sxs-lookup"><span data-stu-id="65c93-122">The Azure Functions runtime uses the `AzureWebJobsStorage` connection string to create internal queues.</span></span> <span data-ttu-id="65c93-123">連接字串 `AzureWebJobsDashboard` 可用來記錄到 Azure 資料表儲存體，以及啟動入口網站中的 [監視] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="65c93-123">The connection string `AzureWebJobsDashboard` is used to log to Azure Table storage and power the **Monitor** tab in the portal.</span></span>

<span data-ttu-id="65c93-124">這些屬性會在 `siteConfig` 物件的 `appSettings`集合中指定：</span><span class="sxs-lookup"><span data-stu-id="65c93-124">These properties are specified in the `appSettings` collection in the `siteConfig` object:</span></span>

```json
"appSettings": [
    {
        "name": "AzureWebJobsStorage",
        "value": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
    },
    {
        "name": "AzureWebJobsDashboard",
        "value": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
    }
```    

### <a name="hosting-plan"></a><span data-ttu-id="65c93-125">主控方案</span><span class="sxs-lookup"><span data-stu-id="65c93-125">Hosting plan</span></span>

<span data-ttu-id="65c93-126">主控方案的定義有所差異，取決於您使用取用方案或 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="65c93-126">The definition of the hosting plan varies, depending on whether you use a Consumption or App Service plan.</span></span> <span data-ttu-id="65c93-127">請參閱[採用取用方案部署函數應用程式](#consumption)和[採用 App Service 方案部署函數應用程式](#app-service-plan)。</span><span class="sxs-lookup"><span data-stu-id="65c93-127">See [Deploy a function app on the Consumption plan](#consumption) and [Deploy a function app on the App Service plan](#app-service-plan).</span></span>

### <a name="function-app"></a><span data-ttu-id="65c93-128">函式應用程式</span><span class="sxs-lookup"><span data-stu-id="65c93-128">Function app</span></span>

<span data-ttu-id="65c93-129">函數應用程式資源可藉由使用 **Microsoft.Web/Site** 類型和 **functionapp** 種類的資源來定義：</span><span class="sxs-lookup"><span data-stu-id="65c93-129">The function app resource is defined by using a resource of type **Microsoft.Web/Site** and kind **functionapp**:</span></span>

```json
{
    "apiVersion": "2015-08-01",
    "type": "Microsoft.Web/sites",
    "name": "[variables('functionAppName')]",
    "location": "[resourceGroup().location]",
    "kind": "functionapp",            
    "dependsOn": [
        "[resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName'))]",
        "[resourceId('Microsoft.Storage/storageAccounts', variables('storageAccountName'))]"
    ]
```

<a name="consumption"></a>

## <a name="deploy-a-function-app-on-the-consumption-plan"></a><span data-ttu-id="65c93-130">採用取用方案部署函數應用程式</span><span class="sxs-lookup"><span data-stu-id="65c93-130">Deploy a function app on the Consumption plan</span></span>

<span data-ttu-id="65c93-131">函數應用程式的執行模式有兩種︰取用方案和 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="65c93-131">You can run a function app in two different modes: the Consumption plan and the App Service plan.</span></span> <span data-ttu-id="65c93-132">取用方案會在您的程式碼執行時自動配置計算能力、視需要相應放大來處理負載，然後在程式碼未執行時相應減少。</span><span class="sxs-lookup"><span data-stu-id="65c93-132">The Consumption plan automatically allocates compute power when your code is running, scales out as necessary to handle load, and then scales down when code is not running.</span></span> <span data-ttu-id="65c93-133">因此，您不必支付閒置 VM 的費用，或必須預先保留容量。</span><span class="sxs-lookup"><span data-stu-id="65c93-133">So, you don't have to pay for idle VMs, and you don't have to reserve capacity in advance.</span></span> <span data-ttu-id="65c93-134">若要深入了解主控方案的詳細資訊，請參閱 [Azure Functions 取用和 App Service 方案](functions-scale.md)。</span><span class="sxs-lookup"><span data-stu-id="65c93-134">To learn more about hosting plans, see [Azure Functions Consumption and App Service plans](functions-scale.md).</span></span>

<span data-ttu-id="65c93-135">如需範例 Azure Resource Manager 範本，請參閱[採用取用方案的函數應用程式]。</span><span class="sxs-lookup"><span data-stu-id="65c93-135">For a sample Azure Resource Manager template, see [Function app on Consumption plan].</span></span>

### <a name="create-a-consumption-plan"></a><span data-ttu-id="65c93-136">建立取用方案</span><span class="sxs-lookup"><span data-stu-id="65c93-136">Create a Consumption plan</span></span>

<span data-ttu-id="65c93-137">取用方案是一種特殊的「伺服器陣列」資源類型。</span><span class="sxs-lookup"><span data-stu-id="65c93-137">A Consumption plan is a special type of "serverfarm" resource.</span></span> <span data-ttu-id="65c93-138">您可以使用 `computeMode` 和 `sku` 屬性的 `Dynamic` 值加以指定：</span><span class="sxs-lookup"><span data-stu-id="65c93-138">You specify it by using the `Dynamic` value for the `computeMode` and `sku` properties:</span></span>

```json
{
    "type": "Microsoft.Web/serverfarms",
    "apiVersion": "2015-04-01",
    "name": "[variables('hostingPlanName')]",
    "location": "[resourceGroup().location]",
    "properties": {
        "name": "[variables('hostingPlanName')]",
        "computeMode": "Dynamic",
        "sku": "Dynamic"
    }
}
```

### <a name="create-a-function-app"></a><span data-ttu-id="65c93-139">建立函數應用程式</span><span class="sxs-lookup"><span data-stu-id="65c93-139">Create a function app</span></span>

<span data-ttu-id="65c93-140">此外，取用方案的網站組態中需要兩個額外的其他設定：`WEBSITE_CONTENTAZUREFILECONNECTIONSTRING` 和 `WEBSITE_CONTENTSHARE`。</span><span class="sxs-lookup"><span data-stu-id="65c93-140">In addition, a Consumption plan requires two additional settings in the site configuration: `WEBSITE_CONTENTAZUREFILECONNECTIONSTRING` and `WEBSITE_CONTENTSHARE`.</span></span> <span data-ttu-id="65c93-141">這些屬性能設定儲存函數應用程式程式碼和組態的儲存體帳戶和檔案路徑。</span><span class="sxs-lookup"><span data-stu-id="65c93-141">These properties configure the storage account and file path where the function app code and configuration are stored.</span></span>

```json
{
    "apiVersion": "2015-08-01",
    "type": "Microsoft.Web/sites",
    "name": "[variables('functionAppName')]",
    "location": "[resourceGroup().location]",
    "kind": "functionapp",            
    "dependsOn": [
        "[resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName'))]",
        "[resourceId('Microsoft.Storage/storageAccounts', variables('storageAccountName'))]"
    ],
    "properties": {
        "serverFarmId": "[resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName'))]",
        "siteConfig": {
            "appSettings": [
                {
                    "name": "AzureWebJobsDashboard",
                    "value": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
                },
                {
                    "name": "AzureWebJobsStorage",
                    "value": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
                },
                {
                    "name": "WEBSITE_CONTENTAZUREFILECONNECTIONSTRING",
                    "value": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
                },
                {
                    "name": "WEBSITE_CONTENTSHARE",
                    "value": "[toLower(variables('functionAppName'))]"
                },
                {
                    "name": "FUNCTIONS_EXTENSION_VERSION",
                    "value": "~1"
                }
            ]
        }
    }
}
```                    

<a name="app-service-plan"></a> 

## <a name="deploy-a-function-app-on-the-app-service-plan"></a><span data-ttu-id="65c93-142">採用 App Service 方案部署函數應用程式</span><span class="sxs-lookup"><span data-stu-id="65c93-142">Deploy a function app on the App Service plan</span></span>

<span data-ttu-id="65c93-143">在 App Service 方案中，您的函數應用程式是依據基本、標準或進階 SKU 在專用的 VM 上執行，就像 Web 應用程式一樣。</span><span class="sxs-lookup"><span data-stu-id="65c93-143">In the App Service plan, your function app runs on dedicated VMs on Basic, Standard, and Premium SKUs, similar to web apps.</span></span> <span data-ttu-id="65c93-144">如需 App Service 方案運作方式的詳細資訊，請參閱 [Azure App Service 方案深入概觀](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="65c93-144">For details about how the App Service plan works, see the [Azure App Service plans in-depth overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span> 

<span data-ttu-id="65c93-145">如需範例 Azure Resource Manager 範本，請參閱[採用 Azure App Service 方案的函數應用程式]。</span><span class="sxs-lookup"><span data-stu-id="65c93-145">For a sample Azure Resource Manager template, see [Function app on Azure App Service plan].</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="65c93-146">建立應用程式服務方案</span><span class="sxs-lookup"><span data-stu-id="65c93-146">Create an App Service plan</span></span>

```json
{
    "type": "Microsoft.Web/serverfarms",
    "apiVersion": "2015-04-01",
    "name": "[variables('hostingPlanName')]",
    "location": "[resourceGroup().location]",
    "properties": {
        "name": "[variables('hostingPlanName')]",
        "sku": "[parameters('sku')]",
        "workerSize": "[parameters('workerSize')]",
        "hostingEnvironment": "",
        "numberOfWorkers": 1
    }
}
```

### <a name="create-a-function-app"></a><span data-ttu-id="65c93-147">建立函數應用程式</span><span class="sxs-lookup"><span data-stu-id="65c93-147">Create a function app</span></span> 

<span data-ttu-id="65c93-148">在您選取調整選項之後，請建立函數應用程式。</span><span class="sxs-lookup"><span data-stu-id="65c93-148">After you've selected a scaling option, create a function app.</span></span> <span data-ttu-id="65c93-149">該 App 將會是保存您所有函數的容器。</span><span class="sxs-lookup"><span data-stu-id="65c93-149">The app is the container that holds all your functions.</span></span>

<span data-ttu-id="65c93-150">函數應用程式有許多子資源可供您用於部署，包括應用程式設定和原始檔控制選項。</span><span class="sxs-lookup"><span data-stu-id="65c93-150">A function app has many child resources that you can use in your deployment, including app settings and source control options.</span></span> <span data-ttu-id="65c93-151">您也可以選擇移除 **sourcecontrols** 子資源並改為使用不同的[部署選項](functions-continuous-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="65c93-151">You also might choose to remove the **sourcecontrols** child resource, and use a different [deployment option](functions-continuous-deployment.md) instead.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="65c93-152">若要使用 Azure Resource Manager 成功部署應用程式，請務必了解資源在 Azure 中部署的方式。</span><span class="sxs-lookup"><span data-stu-id="65c93-152">To successfully deploy your application by using Azure Resource Manager, it's important to understand how resources are deployed in Azure.</span></span> <span data-ttu-id="65c93-153">在下列範例中，將使用 **siteConfig** 套用高層級組態。</span><span class="sxs-lookup"><span data-stu-id="65c93-153">In the following example, top-level configurations are applied by using **siteConfig**.</span></span> <span data-ttu-id="65c93-154">請務必將這些組態設定為高層級，因為它們會將資訊傳遞給 Functions 執行階段和部署引擎。</span><span class="sxs-lookup"><span data-stu-id="65c93-154">It's important to set these configurations at a top level, because they convey information to the Functions runtime and deployment engine.</span></span> <span data-ttu-id="65c93-155">在套用子 **sourcecontrols/web** 資源之前，需要高層級資訊。</span><span class="sxs-lookup"><span data-stu-id="65c93-155">Top-level information is required before the child **sourcecontrols/web** resource is applied.</span></span> <span data-ttu-id="65c93-156">雖然也可以在子層級 **config/appSettings** 資源設定這些設定，在某些案例下，您的函數應用程式需在套用 **config/appSettings**「之前」完成部署。</span><span class="sxs-lookup"><span data-stu-id="65c93-156">Although it's possible to configure these settings in the child-level **config/appSettings** resource, in some cases your function app must be deployed *before* **config/appSettings** is applied.</span></span> <span data-ttu-id="65c93-157">例如，在搭配使用函數應用程式與 [Logic Apps](../logic-apps/index.md) 時，您的函數為另一個資源的相依性。</span><span class="sxs-lookup"><span data-stu-id="65c93-157">For example, when you are using functions with [Logic Apps](../logic-apps/index.md), your functions are a dependency of another resource.</span></span>

```json
{
  "apiVersion": "2015-08-01",
  "name": "[parameters('appName')]",
  "type": "Microsoft.Web/sites",
  "kind": "functionapp",
  "location": "[parameters('location')]",
  "dependsOn": [
    "[resourceId('Microsoft.Storage/storageAccounts', variables('storageAccountName'))]",
    "[resourceId('Microsoft.Web/serverfarms', parameters('appName'))]"
  ],
  "properties": {
     "serverFarmId": "[variables('appServicePlanName')]",
     "siteConfig": {
        "alwaysOn": true,
        "appSettings": [
            { "name": "FUNCTIONS_EXTENSION_VERSION", "value": "~1" },
            { "name": "Project", "value": "src" }
        ]
     }
  },
  "resources": [
     {
        "apiVersion": "2015-08-01",
        "name": "appsettings",
        "type": "config",
        "dependsOn": [
          "[resourceId('Microsoft.Web/Sites', parameters('appName'))]",
          "[resourceId('Microsoft.Web/Sites/sourcecontrols', parameters('appName'), 'web')]",
          "[resourceId('Microsoft.Storage/storageAccounts', variables('storageAccountName'))]"
        ],
        "properties": {
          "AzureWebJobsStorage": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]",
          "AzureWebJobsDashboard": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
        }
     },
     {
          "apiVersion": "2015-08-01",
          "name": "web",
          "type": "sourcecontrols",
          "dependsOn": [
            "[resourceId('Microsoft.Web/sites/', parameters('appName'))]"
          ],
          "properties": {
            "RepoUrl": "[parameters('sourceCodeRepositoryURL')]",
            "branch": "[parameters('sourceCodeBranch')]",
            "IsManualIntegration": "[parameters('sourceCodeManualIntegration')]"
          }
     }
  ]
}
```
> [!TIP]
> <span data-ttu-id="65c93-158">此範本使用[專案](https://github.com/projectkudu/kudu/wiki/Customizing-deployments#using-app-settings-instead-of-a-deployment-file) (英文) 應用程式設定值，它能設定「函數部署引擎」(Kudu) 在其中尋找可部署程式碼的基礎目錄。</span><span class="sxs-lookup"><span data-stu-id="65c93-158">This template uses the [Project](https://github.com/projectkudu/kudu/wiki/Customizing-deployments#using-app-settings-instead-of-a-deployment-file) app settings value, which sets the base directory in which the Functions deployment engine (Kudu) looks for deployable code.</span></span> <span data-ttu-id="65c93-159">在我們的存放庫中，我們的函數是位於 **src** 資料夾的子資料夾中。</span><span class="sxs-lookup"><span data-stu-id="65c93-159">In our repository, our functions are in a subfolder of the **src** folder.</span></span> <span data-ttu-id="65c93-160">因此，在上述範例中，我們將應用程式設定值設定為 `src`。</span><span class="sxs-lookup"><span data-stu-id="65c93-160">So, in the preceding example, we set the app settings value to `src`.</span></span> <span data-ttu-id="65c93-161">如果您的函數位於您存放庫的根，或您並非從來源控制項進行部署，您可以移除此應用程式設定值。</span><span class="sxs-lookup"><span data-stu-id="65c93-161">If your functions are in the root of your repository, or if you are not deploying from source control, you can remove this app settings value.</span></span>

## <a name="deploy-your-template"></a><span data-ttu-id="65c93-162">部署您的範本</span><span class="sxs-lookup"><span data-stu-id="65c93-162">Deploy your template</span></span>

<span data-ttu-id="65c93-163">您可以使用以下任何方式來部署範本：</span><span class="sxs-lookup"><span data-stu-id="65c93-163">You can use any of the following ways to deploy your template:</span></span>

* [<span data-ttu-id="65c93-164">PowerShell</span><span class="sxs-lookup"><span data-stu-id="65c93-164">PowerShell</span></span>](../azure-resource-manager/resource-group-template-deploy.md)
* [<span data-ttu-id="65c93-165">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="65c93-165">Azure CLI</span></span>](../azure-resource-manager/resource-group-template-deploy-cli.md)
* [<span data-ttu-id="65c93-166">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="65c93-166">Azure portal</span></span>](../azure-resource-manager/resource-group-template-deploy-portal.md)
* [<span data-ttu-id="65c93-167">REST API</span><span class="sxs-lookup"><span data-stu-id="65c93-167">REST API</span></span>](../azure-resource-manager/resource-group-template-deploy-rest.md)

### <a name="deploy-to-azure-button"></a><span data-ttu-id="65c93-168">部署至 Azure 按鈕</span><span class="sxs-lookup"><span data-stu-id="65c93-168">Deploy to Azure button</span></span>

<span data-ttu-id="65c93-169">以 GitHub 中 `azuredeploy.json` 檔案的原始路徑 [URL 編碼](https://www.bing.com/search?q=url+encode)版本取代 ```<url-encoded-path-to-azuredeploy-json>```。</span><span class="sxs-lookup"><span data-stu-id="65c93-169">Replace ```<url-encoded-path-to-azuredeploy-json>``` with a [URL-encoded](https://www.bing.com/search?q=url+encode) version of the raw path of your `azuredeploy.json` file in GitHub.</span></span>

<span data-ttu-id="65c93-170">以下是使用 Markdown 的範例：</span><span class="sxs-lookup"><span data-stu-id="65c93-170">Here is an example that uses markdown:</span></span>

```markdown
[![Deploy to Azure](http://azuredeploy.net/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/<url-encoded-path-to-azuredeploy-json>)
```

<span data-ttu-id="65c93-171">以下是使用 HTML 的範例：</span><span class="sxs-lookup"><span data-stu-id="65c93-171">Here is an example that uses HTML:</span></span>

```html
<a href="https://portal.azure.com/#create/Microsoft.Template/uri/<url-encoded-path-to-azuredeploy-json>" target="_blank"><img src="http://azuredeploy.net/deploybutton.png"></a>
```

## <a name="next-steps"></a><span data-ttu-id="65c93-172">後續步驟</span><span class="sxs-lookup"><span data-stu-id="65c93-172">Next steps</span></span>

<span data-ttu-id="65c93-173">深入了解如何開發並設定 Azure Functions。</span><span class="sxs-lookup"><span data-stu-id="65c93-173">Learn more about how to develop and configure Azure Functions.</span></span>

* [<span data-ttu-id="65c93-174">Azure Functions 開發人員參考</span><span class="sxs-lookup"><span data-stu-id="65c93-174">Azure Functions developer reference</span></span>](functions-reference.md)
* [<span data-ttu-id="65c93-175">如何設定 Azure Functions 應用程式設定</span><span class="sxs-lookup"><span data-stu-id="65c93-175">How to configure Azure function app settings</span></span>](functions-how-to-use-azure-function-app-settings.md)
* [<span data-ttu-id="65c93-176">建立您的第一個 Azure 函式</span><span class="sxs-lookup"><span data-stu-id="65c93-176">Create your first Azure function</span></span>](functions-create-first-azure-function.md)

<!-- LINKS -->

[採用取用方案的函數應用程式]: https://github.com/Azure/azure-quickstart-templates/blob/master/101-function-app-create-dynamic/azuredeploy.json
[採用 Azure App Service 方案的函數應用程式]: https://github.com/Azure/azure-quickstart-templates/blob/master/101-function-app-create-dedicated/azuredeploy.json
