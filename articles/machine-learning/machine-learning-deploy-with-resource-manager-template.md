---
title: "aaaDeploy Machine Learning 工作區與 Azure Resource Manager |Microsoft 文件"
description: "如何 toodeploy Azure Machine Learning 使用 Azure Resource Manager 範本的工作區"
services: machine-learning
documentationcenter: 
author: ahgyger
manager: haining
editor: garye
ms.assetid: 4955ac4d-ff99-4908-aa27-69b6bfcc8e85
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/15/2017
ms.author: ahgyger
ms.openlocfilehash: 308959825bcbd670f6ce9b6dc381be767f172357
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-machine-learning-workspace-using-azure-resource-manager"></a>使用 Azure Resource Manager 部署 Machine Learning 工作區
## <a name="introduction"></a>簡介
使用 Azure 資源管理員部署範本為您節省時間，提供可擴充的方式 toodeploy 相互連接與驗證和重試機制元件。 tooset 向上 Azure 機器學習服務工作區，例如，您需要 toofirst 設定 Azure 儲存體帳戶，然後再部署您的工作區。 假想您要對數百個工作區手動進行此動作。 簡單的替代方式是 toouse Azure Resource Manager 範本 toodeploy Azure 機器學習服務工作區和所有相依性。 這篇文章會帶領您逐步完成此程序。 如需 Azure Resource Manager 的詳細概觀，請參閱 [Azure Resource Manager 概觀](../azure-resource-manager/resource-group-overview.md)。

## <a name="step-by-step-create-a-machine-learning-workspace"></a>逐步說明：建立 Machine Learning 工作區
我們將建立 Azure 資源群組，然後使用 Resource Manager 範本部署新的 Azure 儲存體帳戶和新的 Azure Machine Learning 工作區。 Hello 部署完成之後，我們會印出 hello （hello 主索引鍵、 hello 工作區識別碼和工作區中的 URL toohello hello） 所建立的工作區的相關重要資訊。

### <a name="create-an-azure-resource-manager-template"></a>建立 Azure Resource Manager 範本
機器學習服務工作區需要 Azure 儲存體帳戶 toostore hello 連結的資料集 tooit。
hello 下列範本會使用 hello 名稱 hello 資源群組 toogenerate hello 儲存體帳戶名稱和 hello 工作區名稱。  它也會使用 hello 儲存體帳戶名稱做為屬性建立 hello 工作區時。

```
{
    "contentVersion": "1.0.0.0",
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "variables": {
        "namePrefix": "[resourceGroup().name]",
        "location": "[resourceGroup().location]",
        "mlVersion": "2016-04-01",
        "stgVersion": "2015-06-15",
        "storageAccountName": "[concat(variables('namePrefix'),'stg')]",
        "mlWorkspaceName": "[concat(variables('namePrefix'),'mlwk')]",
        "mlResourceId": "[resourceId('Microsoft.MachineLearning/workspaces', variables('mlWorkspaceName'))]",
        "stgResourceId": "[resourceId('Microsoft.Storage/storageAccounts', variables('storageAccountName'))]",
        "storageAccountType": "Standard_LRS"
    },
    "resources": [
        {
            "apiVersion": "[variables('stgVersion')]",
            "name": "[variables('storageAccountName')]",
            "type": "Microsoft.Storage/storageAccounts",
            "location": "[variables('location')]",
            "properties": {
                "accountType": "[variables('storageAccountType')]"
            }
        },
        {
            "apiVersion": "[variables('mlVersion')]",
            "type": "Microsoft.MachineLearning/workspaces",
            "name": "[variables('mlWorkspaceName')]",
            "location": "[variables('location')]",
            "dependsOn": ["[variables('stgResourceId')]"],
            "properties": {
                "UserStorageAccountId": "[variables('stgResourceId')]"
            }
        }
    ],
    "outputs": {
        "mlWorkspaceObject": {"type": "object", "value": "[reference(variables('mlResourceId'), variables('mlVersion'))]"},
        "mlWorkspaceToken": {"type": "string", "value": "[listWorkspaceKeys(variables('mlResourceId'), variables('mlVersion')).primaryToken]"},
        "mlWorkspaceWorkspaceID": {"type": "string", "value": "[reference(variables('mlResourceId'), variables('mlVersion')).WorkspaceId]"},
        "mlWorkspaceWorkspaceLink": {"type": "string", "value": "[concat('https://studio.azureml.net/Home/ViewWorkspace/', reference(variables('mlResourceId'), variables('mlVersion')).WorkspaceId)]"}
    }
}

```
將此範本在 c:\temp\ 下儲存為 mlworkspace.json 檔案。

### <a name="deploy-hello-resource-group-based-on-hello-template"></a>部署 hello 範本為基礎的 hello 資源群組
* 開啟 PowerShell
* 安裝 Azure Resource Manager 和 Azure 服務管理的模組  

```
# Install hello Azure Resource Manager modules from hello PowerShell Gallery (press “A”)
Install-Module AzureRM -Scope CurrentUser

# Install hello Azure Service Management modules from hello PowerShell Gallery (press “A”)
Install-Module Azure -Scope CurrentUser
```

   下列步驟下載並安裝 hello 模組需要 toocomplete hello 其餘步驟。 這個動作只需要 toobe hello 執行 hello PowerShell 命令所在的環境中，執行一次。   

* 驗證 tooAzure  

```
# Authenticate (enter your credentials in hello pop-up window)
Add-AzureRmAccount
```
此步驟需要 toobe 重複每個工作階段。 驗證之後，應該會顯示您的訂用帳戶資訊。

![Azure 帳戶][1]

既然我們已經有存取 tooAzure，我們可以建立 hello 資源群組。

* 建立資源群組

```
$rg = New-AzureRmResourceGroup -Name "uniquenamerequired523" -Location "South Central US"
$rg
```

請確認已正確佈建 hello 資源群組。 **ProvisioningState** 應該是 “Succeeded”。
hello 資源群組名稱會使用 hello 範本 toogenerate hello 儲存體帳戶名稱。 hello 儲存體帳戶名稱必須介於 3 到 24 個字元的長度，並使用數字和小寫的字母。

![資源群組][2]

* 使用 hello 資源群組部署，部署新的機器學習服務工作區。

```
# Create a Resource Group, TemplateFile is hello location of hello JSON template.
$rgd = New-AzureRmResourceGroupDeployment -Name "demo" -TemplateFile "C:\temp\mlworkspace.json" -ResourceGroupName $rg.ResourceGroupName
```

一旦 hello 部署完成之後，就是您部署的 hello] 工作區的直接 tooaccess 屬性。 例如，您可以存取 hello 主要金鑰語彙基元。

```
# Access Azure ML Workspace Token after its deployment.
$rgd.Outputs.mlWorkspaceToken.Value
```

現有的工作區的另一個方式 tooretrieve 語彙基元為 toouse hello Invoke AzureRmResourceAction 命令。 例如，您可以列出所有工作區的 hello 主要和次要的權杖。

```  
# List hello primary and secondary tokens of all workspaces
Get-AzureRmResource |? { $_.ResourceType -Like "*MachineLearning/workspaces*"} |% { Invoke-AzureRmResourceAction -ResourceId $_.ResourceId -Action listworkspacekeys -Force}  
```
Hello 工作區中佈建之後，您也可以自動化許多 Azure Machine Learning Studio 工作使用 hello [PowerShell Module for Azure Machine Learning](http://aka.ms/amlps)。

## <a name="next-steps"></a>後續步驟
* 深入了解 [編寫 Azure Resource Manager 範本](../azure-resource-manager/resource-group-authoring-templates.md)。 
* 看看 hello [Azure 快速入門範本儲存機制](https://github.com/Azure/azure-quickstart-templates)。 
* 觀看這段 [Azure Resource Manager](https://channel9.msdn.com/Events/Ignite/2015/C9-39)影片。 

<!--Image references-->
[1]: ../media/machine-learning-deploy-with-resource-manager-template/azuresubscription.png
[2]: ../media/machine-learning-deploy-with-resource-manager-template/resourcegroupprovisioning.png


<!--Link references-->
