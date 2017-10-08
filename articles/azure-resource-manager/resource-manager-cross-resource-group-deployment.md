---
title: "aaaDeploy Azure 資源 toomultiple 資源群組 |Microsoft 文件"
description: "顯示如何 tootarget 以上的一項 Azure 資源群組部署期間。"
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/15/2017
ms.author: tomfitz
ms.openlocfilehash: 93a39a26e0ca18dfcb5c6e8de95c38a64186d6de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-azure-resources-toomore-than-one-resource-group"></a>部署 Azure 資源 toomore 比一個資源群組

一般而言，您可以部署所有 hello 資源範本 tooa 單一資源群組中。 不過，有一些當您一起想 toodeploy 一組資源，但將它們放在不同的資源群組的案例。 例如，您可能想 toodeploy hello 備份虛擬機器的 Azure Site Recovery tooa 個別資源群組和位置。 資源管理員可讓您 toouse 巢狀範本 tootarget 不同的資源群組與 hello hello 父樣板使用的資源群組。

hello 資源群組都 hello hello 應用程式生命週期容器和它的資源的集合。 您建立 hello hello 範本以外的資源群組，並指定在部署期間的 hello 資源群組 tootarget。 對於簡介 tooresource 的群組，請參閱[Azure 資源管理員概觀](resource-group-overview.md)。

## <a name="example-template"></a>範本範例

tootarget 不同的資源，您必須在部署期間使用巢狀或連結的範本。 hello`Microsoft.Resources/deployments`資源類型提供`resourceGroup`參數，可讓您 toospecify hello 的不同資源群組巢狀部署。 執行 hello 部署之前，必須有所有的 hello 資源群組。 hello 下列範例會將部署兩個儲存體帳戶-指定在部署期間，hello 資源群組中，名為資源群組中的另一個`crossResourceGroupDeployment`:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "StorageAccountName1": {
            "type": "string"
        },
        "StorageAccountName2": {
            "type": "string"
        }
    },
    "variables": {},
    "resources": [
        {
            "apiVersion": "2017-05-10",
            "name": "nestedTemplate",
            "type": "Microsoft.Resources/deployments",
            "resourceGroup": "crossResourceGroupDeployment",
            "properties": {
                "mode": "Incremental",
                "template": {
                    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
                    "contentVersion": "1.0.0.0",
                    "parameters": {},
                    "variables": {},
                    "resources": [
                        {
                            "type": "Microsoft.Storage/storageAccounts",
                            "name": "[parameters('StorageAccountName2')]",
                            "apiVersion": "2015-06-15",
                            "location": "West US",
                            "properties": {
                                "accountType": "Standard_LRS"
                            }
                        }
                    ]
                },
                "parameters": {}
            }
        },
        {
            "type": "Microsoft.Storage/storageAccounts",
            "name": "[parameters('StorageAccountName1')]",
            "apiVersion": "2015-06-15",
            "location": "West US",
            "properties": {
                "accountType": "Standard_LRS"
            }
        }
    ]
}
```

如果您設定`resourceGroup`toohello 不存在的資源群組名稱，hello 部署失敗。 如果您未提供的值`resourceGroup`，資源管理員會使用 hello 父資源群組。  

## <a name="deploy-hello-template"></a>部署 hello 範本

toodeploy hello 範例範本，您可以使用 hello 入口網站、 Azure PowerShell 或 Azure CLI。 若是使用 Azure PowerShell 或 Azure CLI，您必須使用 2017年 5 月或更新版本。 hello 範例假設您已在本機儲存 hello 範本，檔案名稱為**crossrgdeployment.json**。

對於 PowerShell：

```powershell
Login-AzureRmAccount

New-AzureRmResourceGroup -Name mainResourceGroup -Location "South Central US"
New-AzureRmResourceGroup -Name crossResourceGroupDeployment -Location "Central US"
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName mainResourceGroup `
  -TemplateFile c:\MyTemplates\crossrgdeployment.json
```

對於 Azure CLI：

```azurecli
az login

az group create --name mainResourceGroup --location "South Central US"
az group create --name crossResourceGroupDeployment --location "Central US"
az group deployment create \
    --name ExampleDeployment \
    --resource-group mainResourceGroup \
    --template-file crossrgdeployment.json
```

部署完成後，您會看到兩個資源群組。 每個資源群組都包含儲存體帳戶。

## <a name="use-resourcegroup-function"></a>使用 resourceGroup() 函數

針對交叉資源群組部署，hello [resouceGroup() 函式](resource-group-template-functions-resource.md#resourcegroup)解析以不同的方式會根據您指定 hello 巢狀的樣板的方式。 

如果您內嵌在另一個範本內的一個範本，resouceGroup() hello 巢狀範本中的會解析 toohello 父資源群組。 內嵌的範本會使用下列格式的 hello:

```json
"apiVersion": "2017-05-10",
"name": "embeddedTemplate",
"type": "Microsoft.Resources/deployments",
"resourceGroup": "crossResourceGroupDeployment",
"properties": {
    "mode": "Incremental",
    "template": {
        ...
        resourceGroup() refers tooparent resource group
    }
}
```

如果您將連結 tooa 另一個範本，resouceGroup() hello 連結的範本中會解析 toohello 巢狀的資源群組。 連結的範本會使用下列格式的 hello:

```json
"apiVersion": "2017-05-10",
"name": "linkedTemplate",
"type": "Microsoft.Resources/deployments",
"resourceGroup": "crossResourceGroupDeployment",
"properties": {
    "mode": "Incremental",
    "templateLink": {
        ...
        resourceGroup() in linked template refers toolinked resource group
    }
}
```

## <a name="next-steps"></a>後續步驟

* 如何 toodefine 參數在範本中，請參閱的 toounderstand [hello 結構和語法的 Azure 資源管理員範本了解](resource-group-authoring-templates.md)。
* 如需解決常見部署錯誤的秘訣，請參閱[使用 Azure Resource Manager 針對常見的 Azure 部署錯誤進行疑難排解](resource-manager-common-deployment-errors.md)。
* 如需部署需要 SAS 權杖之範本的詳細資訊，請參閱[使用 SAS 權杖部署私人範本](resource-manager-powershell-sas-token.md)。
