---
title: "Azure 功能中的函式應用程式的 aaaAutomate 資源部署 |Microsoft 文件"
description: "深入了解如何 toobuild 函式應用程式會將部署的 Azure Resource Manager 範本。"
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
ms.openlocfilehash: b0df0d4ef9fe93213f7b1cb1d1e6b4e14f8b3a30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="automate-resource-deployment-for-your-function-app-in-azure-functions"></a><span data-ttu-id="a0921-104">Azure Functions 中函數應用程式的自動化資源部署</span><span class="sxs-lookup"><span data-stu-id="a0921-104">Automate resource deployment for your function app in Azure Functions</span></span>

<span data-ttu-id="a0921-105">您可以使用 Azure Resource Manager 範本 toodeploy 函式應用程式。</span><span class="sxs-lookup"><span data-stu-id="a0921-105">You can use an Azure Resource Manager template toodeploy a function app.</span></span> <span data-ttu-id="a0921-106">本文概述所需的 hello 資源和執行這項作業的參數。</span><span class="sxs-lookup"><span data-stu-id="a0921-106">This article outlines hello required resources and parameters for doing so.</span></span> <span data-ttu-id="a0921-107">您可能需要 toodeploy 其他資源，根據 hello[觸發程序和繫結](functions-triggers-bindings.md)函式應用程式中。</span><span class="sxs-lookup"><span data-stu-id="a0921-107">You might need toodeploy additional resources, depending on hello [triggers and bindings](functions-triggers-bindings.md) in your function app.</span></span>

<span data-ttu-id="a0921-108">如需關於建立範本的詳細資訊，請參閱 [編寫 Azure Resource Manager 範本](../azure-resource-manager/resource-group-authoring-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="a0921-108">For more information about creating templates, see [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="a0921-109">如需範例範本，請參閱：</span><span class="sxs-lookup"><span data-stu-id="a0921-109">For sample templates, see:</span></span>
- <span data-ttu-id="a0921-110">[採用取用方案的函數應用程式]</span><span class="sxs-lookup"><span data-stu-id="a0921-110">[Function app on Consumption plan]</span></span>
- <span data-ttu-id="a0921-111">[採用 Azure App Service 方案的函數應用程式]</span><span class="sxs-lookup"><span data-stu-id="a0921-111">[Function app on Azure App Service plan]</span></span>

## <a name="required-resources"></a><span data-ttu-id="a0921-112">所需資源</span><span class="sxs-lookup"><span data-stu-id="a0921-112">Required resources</span></span>

<span data-ttu-id="a0921-113">函數應用程式需要以下資源：</span><span class="sxs-lookup"><span data-stu-id="a0921-113">A function app requires these resources:</span></span>

* <span data-ttu-id="a0921-114">[Azure 儲存體](../storage/index.md)帳戶</span><span class="sxs-lookup"><span data-stu-id="a0921-114">An [Azure Storage](../storage/index.md) account</span></span>
* <span data-ttu-id="a0921-115">主控方案 (取用方案或 App Service 方案)</span><span class="sxs-lookup"><span data-stu-id="a0921-115">A hosting plan (Consumption plan or App Service plan)</span></span>
* <span data-ttu-id="a0921-116">函數應用程式</span><span class="sxs-lookup"><span data-stu-id="a0921-116">A function app</span></span> 

### <a name="storage-account"></a><span data-ttu-id="a0921-117">儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="a0921-117">Storage account</span></span>

<span data-ttu-id="a0921-118">函數應用程式需要 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="a0921-118">An Azure storage account is required for a function app.</span></span> <span data-ttu-id="a0921-119">您需要支援 Blob、資料表、佇列和檔案的一般用途帳戶。</span><span class="sxs-lookup"><span data-stu-id="a0921-119">You need a general purpose account that supports blobs, tables, queues, and files.</span></span> <span data-ttu-id="a0921-120">如需詳細資訊，請參閱 [Azure Functions 儲存體帳戶需求](functions-create-function-app-portal.md#storage-account-requirements)。</span><span class="sxs-lookup"><span data-stu-id="a0921-120">For more information, see [Azure Functions storage account requirements](functions-create-function-app-portal.md#storage-account-requirements).</span></span>

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

<span data-ttu-id="a0921-121">此外，hello 屬性`AzureWebJobsStorage`和`AzureWebJobsDashboard`必須指定為 hello 站台設定中的應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="a0921-121">In addition, hello properties `AzureWebJobsStorage` and `AzureWebJobsDashboard` must be specified as app settings in hello site configuration.</span></span> <span data-ttu-id="a0921-122">hello Azure 函式執行階段會使用 hello `AzureWebJobsStorage` toocreate 內部佇列的連接字串。</span><span class="sxs-lookup"><span data-stu-id="a0921-122">hello Azure Functions runtime uses hello `AzureWebJobsStorage` connection string toocreate internal queues.</span></span> <span data-ttu-id="a0921-123">hello 連接字串`AzureWebJobsDashboard`為使用的 toolog tooAzure 資料表儲存體和電源 hello**監視器**hello 入口網站中的索引標籤。</span><span class="sxs-lookup"><span data-stu-id="a0921-123">hello connection string `AzureWebJobsDashboard` is used toolog tooAzure Table storage and power hello **Monitor** tab in hello portal.</span></span>

<span data-ttu-id="a0921-124">這些屬性會指定在 hello`appSettings`中 hello 集合`siteConfig`物件：</span><span class="sxs-lookup"><span data-stu-id="a0921-124">These properties are specified in hello `appSettings` collection in hello `siteConfig` object:</span></span>

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

### <a name="hosting-plan"></a><span data-ttu-id="a0921-125">主控方案</span><span class="sxs-lookup"><span data-stu-id="a0921-125">Hosting plan</span></span>

<span data-ttu-id="a0921-126">裝載計劃的 hello hello 定義會有所差異，取決於您是否使用 「 耗用量或應用程式服務方案。</span><span class="sxs-lookup"><span data-stu-id="a0921-126">hello definition of hello hosting plan varies, depending on whether you use a Consumption or App Service plan.</span></span> <span data-ttu-id="a0921-127">請參閱[部署函式的應用程式上 hello 耗用量計劃](#consumption)和[部署函式上的應用程式的 App Service 方案 hello](#app-service-plan)。</span><span class="sxs-lookup"><span data-stu-id="a0921-127">See [Deploy a function app on hello Consumption plan](#consumption) and [Deploy a function app on hello App Service plan](#app-service-plan).</span></span>

### <a name="function-app"></a><span data-ttu-id="a0921-128">函式應用程式</span><span class="sxs-lookup"><span data-stu-id="a0921-128">Function app</span></span>

<span data-ttu-id="a0921-129">使用類型的資源定義 hello 函式應用程式資源**Microsoft.Web/Site**以及種類**functionapp**:</span><span class="sxs-lookup"><span data-stu-id="a0921-129">hello function app resource is defined by using a resource of type **Microsoft.Web/Site** and kind **functionapp**:</span></span>

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

## <a name="deploy-a-function-app-on-hello-consumption-plan"></a><span data-ttu-id="a0921-130">部署 hello 耗用量計劃的函式應用程式</span><span class="sxs-lookup"><span data-stu-id="a0921-130">Deploy a function app on hello Consumption plan</span></span>

<span data-ttu-id="a0921-131">您可以在兩個不同的模式中執行的函式應用程式： hello 耗用量計劃和 hello 應用程式服務方案。</span><span class="sxs-lookup"><span data-stu-id="a0921-131">You can run a function app in two different modes: hello Consumption plan and hello App Service plan.</span></span> <span data-ttu-id="a0921-132">hello 耗用量計劃您的程式碼會執行時，能有效擴充為必要 toohandle 負載，而且再按比例減少 程式碼未執行時，自動配置運算能力。</span><span class="sxs-lookup"><span data-stu-id="a0921-132">hello Consumption plan automatically allocates compute power when your code is running, scales out as necessary toohandle load, and then scales down when code is not running.</span></span> <span data-ttu-id="a0921-133">因此，您不需要 toopay 對於閒置的 Vm，而且您沒有 tooreserve 容量事先。</span><span class="sxs-lookup"><span data-stu-id="a0921-133">So, you don't have toopay for idle VMs, and you don't have tooreserve capacity in advance.</span></span> <span data-ttu-id="a0921-134">toolearn 深入了解主控方案，請參閱[Azure 函式耗用量和應用程式服務計劃](functions-scale.md)。</span><span class="sxs-lookup"><span data-stu-id="a0921-134">toolearn more about hosting plans, see [Azure Functions Consumption and App Service plans](functions-scale.md).</span></span>

<span data-ttu-id="a0921-135">如需範例 Azure Resource Manager 範本，請參閱[採用取用方案的函數應用程式]。</span><span class="sxs-lookup"><span data-stu-id="a0921-135">For a sample Azure Resource Manager template, see [Function app on Consumption plan].</span></span>

### <a name="create-a-consumption-plan"></a><span data-ttu-id="a0921-136">建立取用方案</span><span class="sxs-lookup"><span data-stu-id="a0921-136">Create a Consumption plan</span></span>

<span data-ttu-id="a0921-137">取用方案是一種特殊的「伺服器陣列」資源類型。</span><span class="sxs-lookup"><span data-stu-id="a0921-137">A Consumption plan is a special type of "serverfarm" resource.</span></span> <span data-ttu-id="a0921-138">您指定使用 hello`Dynamic`值 hello`computeMode`和`sku`屬性：</span><span class="sxs-lookup"><span data-stu-id="a0921-138">You specify it by using hello `Dynamic` value for hello `computeMode` and `sku` properties:</span></span>

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

### <a name="create-a-function-app"></a><span data-ttu-id="a0921-139">建立函數應用程式</span><span class="sxs-lookup"><span data-stu-id="a0921-139">Create a function app</span></span>

<span data-ttu-id="a0921-140">此外，耗用量計劃需要 hello 站台設定中兩個額外的設定：`WEBSITE_CONTENTAZUREFILECONNECTIONSTRING`和`WEBSITE_CONTENTSHARE`。</span><span class="sxs-lookup"><span data-stu-id="a0921-140">In addition, a Consumption plan requires two additional settings in hello site configuration: `WEBSITE_CONTENTAZUREFILECONNECTIONSTRING` and `WEBSITE_CONTENTSHARE`.</span></span> <span data-ttu-id="a0921-141">這些屬性會設定 hello 儲存體帳戶和檔案路徑 hello 函式應用程式程式碼和組態的儲存位置。</span><span class="sxs-lookup"><span data-stu-id="a0921-141">These properties configure hello storage account and file path where hello function app code and configuration are stored.</span></span>

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

## <a name="deploy-a-function-app-on-hello-app-service-plan"></a><span data-ttu-id="a0921-142">部署函式的應用程式上 hello App Service 方案</span><span class="sxs-lookup"><span data-stu-id="a0921-142">Deploy a function app on hello App Service plan</span></span>

<span data-ttu-id="a0921-143">Hello App Service 方案，在應用程式函式會執行專用在 Basic、 Standard 和 Premium Sku 類似 tooweb 應用程式上的 Vm 上。</span><span class="sxs-lookup"><span data-stu-id="a0921-143">In hello App Service plan, your function app runs on dedicated VMs on Basic, Standard, and Premium SKUs, similar tooweb apps.</span></span> <span data-ttu-id="a0921-144">如需 hello 應用程式服務方案的運作方式的詳細資訊，請參閱 hello [Azure App Service 方案深入概觀](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="a0921-144">For details about how hello App Service plan works, see hello [Azure App Service plans in-depth overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span> 

<span data-ttu-id="a0921-145">如需範例 Azure Resource Manager 範本，請參閱[採用 Azure App Service 方案的函數應用程式]。</span><span class="sxs-lookup"><span data-stu-id="a0921-145">For a sample Azure Resource Manager template, see [Function app on Azure App Service plan].</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="a0921-146">建立應用程式服務方案</span><span class="sxs-lookup"><span data-stu-id="a0921-146">Create an App Service plan</span></span>

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

### <a name="create-a-function-app"></a><span data-ttu-id="a0921-147">建立函數應用程式</span><span class="sxs-lookup"><span data-stu-id="a0921-147">Create a function app</span></span> 

<span data-ttu-id="a0921-148">在您選取調整選項之後，請建立函數應用程式。</span><span class="sxs-lookup"><span data-stu-id="a0921-148">After you've selected a scaling option, create a function app.</span></span> <span data-ttu-id="a0921-149">hello 應用程式會保留您所有的函式的 hello 容器。</span><span class="sxs-lookup"><span data-stu-id="a0921-149">hello app is hello container that holds all your functions.</span></span>

<span data-ttu-id="a0921-150">函數應用程式有許多子資源可供您用於部署，包括應用程式設定和原始檔控制選項。</span><span class="sxs-lookup"><span data-stu-id="a0921-150">A function app has many child resources that you can use in your deployment, including app settings and source control options.</span></span> <span data-ttu-id="a0921-151">您也可以選擇 tooremove hello **sourcecontrols**子資源，並使用不同[部署選項](functions-continuous-deployment.md)改為。</span><span class="sxs-lookup"><span data-stu-id="a0921-151">You also might choose tooremove hello **sourcecontrols** child resource, and use a different [deployment option](functions-continuous-deployment.md) instead.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a0921-152">toosuccessfully 使用 Azure Resource Manager 部署應用程式，它是如何在 Azure 中部署資源的重要 toounderstand。</span><span class="sxs-lookup"><span data-stu-id="a0921-152">toosuccessfully deploy your application by using Azure Resource Manager, it's important toounderstand how resources are deployed in Azure.</span></span> <span data-ttu-id="a0921-153">在下列範例的 hello，最上層設定適用於使用**網站組態**。</span><span class="sxs-lookup"><span data-stu-id="a0921-153">In hello following example, top-level configurations are applied by using **siteConfig**.</span></span> <span data-ttu-id="a0921-154">是重要 tooset 這些組態在最上方層級，因為它們傳達資訊 toohello 函式的執行階段和部署引擎。</span><span class="sxs-lookup"><span data-stu-id="a0921-154">It's important tooset these configurations at a top level, because they convey information toohello Functions runtime and deployment engine.</span></span> <span data-ttu-id="a0921-155">Hello 子系之前所需的最上層的資訊是**sourcecontrols/web**資源套用。</span><span class="sxs-lookup"><span data-stu-id="a0921-155">Top-level information is required before hello child **sourcecontrols/web** resource is applied.</span></span> <span data-ttu-id="a0921-156">中的這些設定可能 tooconfigure 雖然 hello 子層級**appSettings 組態/**資源，在某些情況下，函式應用程式必須先部署*之前* **appSettings 組態 /**套用。</span><span class="sxs-lookup"><span data-stu-id="a0921-156">Although it's possible tooconfigure these settings in hello child-level **config/appSettings** resource, in some cases your function app must be deployed *before* **config/appSettings** is applied.</span></span> <span data-ttu-id="a0921-157">例如，在搭配使用函數應用程式與 [Logic Apps](../logic-apps/index.md) 時，您的函數為另一個資源的相依性。</span><span class="sxs-lookup"><span data-stu-id="a0921-157">For example, when you are using functions with [Logic Apps](../logic-apps/index.md), your functions are a dependency of another resource.</span></span>

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
> <span data-ttu-id="a0921-158">此範本使用 hello[專案](https://github.com/projectkudu/kudu/wiki/Customizing-deployments#using-app-settings-instead-of-a-deployment-file)應用程式設定值，設定 hello 基底目錄中的 hello 函式部署引擎 (Kudu) 會尋找任何可部署的程式碼。</span><span class="sxs-lookup"><span data-stu-id="a0921-158">This template uses hello [Project](https://github.com/projectkudu/kudu/wiki/Customizing-deployments#using-app-settings-instead-of-a-deployment-file) app settings value, which sets hello base directory in which hello Functions deployment engine (Kudu) looks for deployable code.</span></span> <span data-ttu-id="a0921-159">在我們的儲存機制中，我們函式是位於子資料夾中的 hello **src**資料夾。</span><span class="sxs-lookup"><span data-stu-id="a0921-159">In our repository, our functions are in a subfolder of hello **src** folder.</span></span> <span data-ttu-id="a0921-160">因此，在上述範例中的 hello，我們設定 hello 應用程式設定值太`src`。</span><span class="sxs-lookup"><span data-stu-id="a0921-160">So, in hello preceding example, we set hello app settings value too`src`.</span></span> <span data-ttu-id="a0921-161">如果您的函式是您的儲存機制的 hello 根目錄或並不會從原始檔控制部署，您可以移除此應用程式設定值。</span><span class="sxs-lookup"><span data-stu-id="a0921-161">If your functions are in hello root of your repository, or if you are not deploying from source control, you can remove this app settings value.</span></span>

## <a name="deploy-your-template"></a><span data-ttu-id="a0921-162">部署您的範本</span><span class="sxs-lookup"><span data-stu-id="a0921-162">Deploy your template</span></span>

<span data-ttu-id="a0921-163">您可以使用任何下列方式 toodeploy hello 範本：</span><span class="sxs-lookup"><span data-stu-id="a0921-163">You can use any of hello following ways toodeploy your template:</span></span>

* [<span data-ttu-id="a0921-164">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a0921-164">PowerShell</span></span>](../azure-resource-manager/resource-group-template-deploy.md)
* [<span data-ttu-id="a0921-165">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="a0921-165">Azure CLI</span></span>](../azure-resource-manager/resource-group-template-deploy-cli.md)
* [<span data-ttu-id="a0921-166">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="a0921-166">Azure portal</span></span>](../azure-resource-manager/resource-group-template-deploy-portal.md)
* [<span data-ttu-id="a0921-167">REST API</span><span class="sxs-lookup"><span data-stu-id="a0921-167">REST API</span></span>](../azure-resource-manager/resource-group-template-deploy-rest.md)

### <a name="deploy-tooazure-button"></a><span data-ttu-id="a0921-168">部署 tooAzure 按鈕</span><span class="sxs-lookup"><span data-stu-id="a0921-168">Deploy tooAzure button</span></span>

<span data-ttu-id="a0921-169">取代```<url-encoded-path-to-azuredeploy-json>```與[URL 編碼](https://www.bing.com/search?q=url+encode)hello 原始路徑的版本您`azuredeploy.json`GitHub 中的檔案。</span><span class="sxs-lookup"><span data-stu-id="a0921-169">Replace ```<url-encoded-path-to-azuredeploy-json>``` with a [URL-encoded](https://www.bing.com/search?q=url+encode) version of hello raw path of your `azuredeploy.json` file in GitHub.</span></span>

<span data-ttu-id="a0921-170">以下是使用 Markdown 的範例：</span><span class="sxs-lookup"><span data-stu-id="a0921-170">Here is an example that uses markdown:</span></span>

```markdown
[![Deploy tooAzure](http://azuredeploy.net/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/<url-encoded-path-to-azuredeploy-json>)
```

<span data-ttu-id="a0921-171">以下是使用 HTML 的範例：</span><span class="sxs-lookup"><span data-stu-id="a0921-171">Here is an example that uses HTML:</span></span>

```html
<a href="https://portal.azure.com/#create/Microsoft.Template/uri/<url-encoded-path-to-azuredeploy-json>" target="_blank"><img src="http://azuredeploy.net/deploybutton.png"></a>
```

## <a name="next-steps"></a><span data-ttu-id="a0921-172">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a0921-172">Next steps</span></span>

<span data-ttu-id="a0921-173">深入了解如何 toodevelop 及設定 Azure 函式。</span><span class="sxs-lookup"><span data-stu-id="a0921-173">Learn more about how toodevelop and configure Azure Functions.</span></span>

* [<span data-ttu-id="a0921-174">Azure Functions 開發人員參考</span><span class="sxs-lookup"><span data-stu-id="a0921-174">Azure Functions developer reference</span></span>](functions-reference.md)
* [<span data-ttu-id="a0921-175">Tooconfigure Azure 應用程式設定的運作方式</span><span class="sxs-lookup"><span data-stu-id="a0921-175">How tooconfigure Azure function app settings</span></span>](functions-how-to-use-azure-function-app-settings.md)
* [<span data-ttu-id="a0921-176">建立您的第一個 Azure 函式</span><span class="sxs-lookup"><span data-stu-id="a0921-176">Create your first Azure function</span></span>](functions-create-first-azure-function.md)

<!-- LINKS -->

[採用取用方案的函數應用程式]: https://github.com/Azure/azure-quickstart-templates/blob/master/101-function-app-create-dynamic/azuredeploy.json
[採用 Azure App Service 方案的函數應用程式]: https://github.com/Azure/azure-quickstart-templates/blob/master/101-function-app-create-dedicated/azuredeploy.json
