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
# <a name="automate-resource-deployment-for-your-function-app-in-azure-functions"></a>Azure Functions 中函數應用程式的自動化資源部署

您可以使用 Azure Resource Manager 範本 toodeploy 函式應用程式。 本文概述所需的 hello 資源和執行這項作業的參數。 您可能需要 toodeploy 其他資源，根據 hello[觸發程序和繫結](functions-triggers-bindings.md)函式應用程式中。

如需關於建立範本的詳細資訊，請參閱 [編寫 Azure Resource Manager 範本](../azure-resource-manager/resource-group-authoring-templates.md)。

如需範例範本，請參閱：
- [採用取用方案的函數應用程式]
- [採用 Azure App Service 方案的函數應用程式]

## <a name="required-resources"></a>所需資源

函數應用程式需要以下資源：

* [Azure 儲存體](../storage/index.md)帳戶
* 主控方案 (取用方案或 App Service 方案)
* 函數應用程式 

### <a name="storage-account"></a>儲存體帳戶

函數應用程式需要 Azure 儲存體帳戶。 您需要支援 Blob、資料表、佇列和檔案的一般用途帳戶。 如需詳細資訊，請參閱 [Azure Functions 儲存體帳戶需求](functions-create-function-app-portal.md#storage-account-requirements)。

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

此外，hello 屬性`AzureWebJobsStorage`和`AzureWebJobsDashboard`必須指定為 hello 站台設定中的應用程式設定。 hello Azure 函式執行階段會使用 hello `AzureWebJobsStorage` toocreate 內部佇列的連接字串。 hello 連接字串`AzureWebJobsDashboard`為使用的 toolog tooAzure 資料表儲存體和電源 hello**監視器**hello 入口網站中的索引標籤。

這些屬性會指定在 hello`appSettings`中 hello 集合`siteConfig`物件：

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

### <a name="hosting-plan"></a>主控方案

裝載計劃的 hello hello 定義會有所差異，取決於您是否使用 「 耗用量或應用程式服務方案。 請參閱[部署函式的應用程式上 hello 耗用量計劃](#consumption)和[部署函式上的應用程式的 App Service 方案 hello](#app-service-plan)。

### <a name="function-app"></a>函式應用程式

使用類型的資源定義 hello 函式應用程式資源**Microsoft.Web/Site**以及種類**functionapp**:

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

## <a name="deploy-a-function-app-on-hello-consumption-plan"></a>部署 hello 耗用量計劃的函式應用程式

您可以在兩個不同的模式中執行的函式應用程式： hello 耗用量計劃和 hello 應用程式服務方案。 hello 耗用量計劃您的程式碼會執行時，能有效擴充為必要 toohandle 負載，而且再按比例減少 程式碼未執行時，自動配置運算能力。 因此，您不需要 toopay 對於閒置的 Vm，而且您沒有 tooreserve 容量事先。 toolearn 深入了解主控方案，請參閱[Azure 函式耗用量和應用程式服務計劃](functions-scale.md)。

如需範例 Azure Resource Manager 範本，請參閱[採用取用方案的函數應用程式]。

### <a name="create-a-consumption-plan"></a>建立取用方案

取用方案是一種特殊的「伺服器陣列」資源類型。 您指定使用 hello`Dynamic`值 hello`computeMode`和`sku`屬性：

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

### <a name="create-a-function-app"></a>建立函數應用程式

此外，耗用量計劃需要 hello 站台設定中兩個額外的設定：`WEBSITE_CONTENTAZUREFILECONNECTIONSTRING`和`WEBSITE_CONTENTSHARE`。 這些屬性會設定 hello 儲存體帳戶和檔案路徑 hello 函式應用程式程式碼和組態的儲存位置。

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

## <a name="deploy-a-function-app-on-hello-app-service-plan"></a>部署函式的應用程式上 hello App Service 方案

Hello App Service 方案，在應用程式函式會執行專用在 Basic、 Standard 和 Premium Sku 類似 tooweb 應用程式上的 Vm 上。 如需 hello 應用程式服務方案的運作方式的詳細資訊，請參閱 hello [Azure App Service 方案深入概觀](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)。 

如需範例 Azure Resource Manager 範本，請參閱[採用 Azure App Service 方案的函數應用程式]。

### <a name="create-an-app-service-plan"></a>建立應用程式服務方案

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

### <a name="create-a-function-app"></a>建立函數應用程式 

在您選取調整選項之後，請建立函數應用程式。 hello 應用程式會保留您所有的函式的 hello 容器。

函數應用程式有許多子資源可供您用於部署，包括應用程式設定和原始檔控制選項。 您也可以選擇 tooremove hello **sourcecontrols**子資源，並使用不同[部署選項](functions-continuous-deployment.md)改為。

> [!IMPORTANT]
> toosuccessfully 使用 Azure Resource Manager 部署應用程式，它是如何在 Azure 中部署資源的重要 toounderstand。 在下列範例的 hello，最上層設定適用於使用**網站組態**。 是重要 tooset 這些組態在最上方層級，因為它們傳達資訊 toohello 函式的執行階段和部署引擎。 Hello 子系之前所需的最上層的資訊是**sourcecontrols/web**資源套用。 中的這些設定可能 tooconfigure 雖然 hello 子層級**appSettings 組態/**資源，在某些情況下，函式應用程式必須先部署*之前* **appSettings 組態 /**套用。 例如，在搭配使用函數應用程式與 [Logic Apps](../logic-apps/index.md) 時，您的函數為另一個資源的相依性。

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
> 此範本使用 hello[專案](https://github.com/projectkudu/kudu/wiki/Customizing-deployments#using-app-settings-instead-of-a-deployment-file)應用程式設定值，設定 hello 基底目錄中的 hello 函式部署引擎 (Kudu) 會尋找任何可部署的程式碼。 在我們的儲存機制中，我們函式是位於子資料夾中的 hello **src**資料夾。 因此，在上述範例中的 hello，我們設定 hello 應用程式設定值太`src`。 如果您的函式是您的儲存機制的 hello 根目錄或並不會從原始檔控制部署，您可以移除此應用程式設定值。

## <a name="deploy-your-template"></a>部署您的範本

您可以使用任何下列方式 toodeploy hello 範本：

* [PowerShell](../azure-resource-manager/resource-group-template-deploy.md)
* [Azure CLI](../azure-resource-manager/resource-group-template-deploy-cli.md)
* [Azure 入口網站](../azure-resource-manager/resource-group-template-deploy-portal.md)
* [REST API](../azure-resource-manager/resource-group-template-deploy-rest.md)

### <a name="deploy-tooazure-button"></a>部署 tooAzure 按鈕

取代```<url-encoded-path-to-azuredeploy-json>```與[URL 編碼](https://www.bing.com/search?q=url+encode)hello 原始路徑的版本您`azuredeploy.json`GitHub 中的檔案。

以下是使用 Markdown 的範例：

```markdown
[![Deploy tooAzure](http://azuredeploy.net/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/<url-encoded-path-to-azuredeploy-json>)
```

以下是使用 HTML 的範例：

```html
<a href="https://portal.azure.com/#create/Microsoft.Template/uri/<url-encoded-path-to-azuredeploy-json>" target="_blank"><img src="http://azuredeploy.net/deploybutton.png"></a>
```

## <a name="next-steps"></a>後續步驟

深入了解如何 toodevelop 及設定 Azure 函式。

* [Azure Functions 開發人員參考](functions-reference.md)
* [Tooconfigure Azure 應用程式設定的運作方式](functions-how-to-use-azure-function-app-settings.md)
* [建立您的第一個 Azure 函式](functions-create-first-azure-function.md)

<!-- LINKS -->

[採用取用方案的函數應用程式]: https://github.com/Azure/azure-quickstart-templates/blob/master/101-function-app-create-dynamic/azuredeploy.json
[採用 Azure App Service 方案的函數應用程式]: https://github.com/Azure/azure-quickstart-templates/blob/master/101-function-app-create-dedicated/azuredeploy.json
