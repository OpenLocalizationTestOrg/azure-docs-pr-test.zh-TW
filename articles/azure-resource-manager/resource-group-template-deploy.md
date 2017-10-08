---
title: "使用 PowerShell 和範本 aaaDeploy 資源 |Microsoft 文件"
description: "使用 Azure 資源管理員和 Azure PowerShell toodeploy 資源 tooAzure。 hello 資源的資源管理員範本中定義。"
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 55903f35-6c16-4c6d-bf52-dbf365605c3f
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: tomfitz
ms.openlocfilehash: 41506811ba3c2ea5df6313db70978ade50f71161
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-azure-powershell"></a>使用 Resource Manager 範本與 Azure PowerShell 來部署資源

本主題說明如何使用資源管理員範本 toodeploy toouse Azure PowerShell 資源 tooAzure。 如果您不熟悉以部署的 hello 概念，並管理您的 Azure 解決方案，請參閱[Azure 資源管理員概觀](resource-group-overview.md)。

您所部署的 hello Resource Manager 範本可為您的電腦上的本機檔案或位於等 GitHub 儲存機制中的外部檔案。 您在本文中部署的 hello 範本位於 hello[範例範本](#sample-template) 區段中，或為[GitHub 中的儲存體帳戶範本](https://github.com/Azure/azure-quickstart-templates/blob/master/101-storage-account-create/azuredeploy.json)。

[!INCLUDE [sample-powershell-install](../../includes/sample-powershell-install.md)]

<a id="deploy-local-template" />

## <a name="deploy-a-template-from-your-local-machine"></a>從本機電腦部署範本

部署資源 tooAzure 時您：

1. 登入 tooyour Azure 帳戶
2. 建立可做為部署的 hello 資源的 hello 容器的資源群組。 hello hello 資源群組名稱只可包含英數字元、 句號、 底線、 連字號及括號。 它可以是 too90 字元組成。 不能以句點結束。
3. 部署 toohello 資源群組 hello 範本定義 hello 資源 toocreate

範本可以包含 toocustomize hello 部署可讓您的參數。 例如，您可以提供針對特定環境 (例如開發、測試和生產) 量身訂做的值。 hello 範例範本定義 hello 儲存體帳戶 SKU 的參數。

hello 下列範例會建立資源群組，並部署範本從本機電腦：

```powershell
Login-AzureRmAccount
 
New-AzureRmResourceGroup -Name ExampleResourceGroup -Location "South Central US"
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json -storageAccountType Standard_GRS
```

hello 部署可能需要幾分鐘的時間 toocomplete。 完成時，您會看到訊息，其中包含 hello 結果：

```powershell
ProvisioningState       : Succeeded
```

## <a name="deploy-a-template-from-an-external-source"></a>從外部來源部署範本

而不是儲存在本機電腦上的資源管理員範本，您可能會想 toostore 外部位置中。 您可以將範本儲存在原始檔控制存放庫 (例如 GitHub) 中。 或者，您可以將它們儲存在 Azure 儲存體帳戶中，以在組織內共用存取。

toodeploy 的外部的範本，請使用 hello **TemplateUri**參數。 使用 hello 範例 toodeploy hello 範例範本從 GitHub 中的 hello URI。

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json `
  -storageAccountType Standard_GRS
```

hello 上述範例要求可公開存取 URI hello 範本，適用於大部分的情況下，因為您的範本不應該包含機密資料。 如果您需要 toospecify 敏感性資料 （例如系統管理員密碼），將值傳遞做為安全的參數。 不過，如果您不想範本 toobe 可公開存取，您可以保護它儲存在私人儲存體容器中。 如需部署需要共用存取簽章 (SAS) 權杖之範本的相關資訊，請參閱[使用 SAS 權杖部署私人範本](resource-manager-powershell-sas-token.md)。

## <a name="parameter-files"></a>參數檔案

而不是傳遞參數做為內嵌指令碼中的值，您可能會發現它更容易 toouse 包含 hello 參數值的 JSON 檔案。 hello 參數檔案必須是下列格式的 hello:

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
     "storageAccountType": {
         "value": "Standard_GRS"
     }
  }
}
```

請注意 hello 參數 > 一節包含符合您的範本 (storageAccountType) 中定義的 hello 參數的參數名稱。 hello 參數檔案包含 hello 參數的值。 這個值會自動在部署期間傳遞 toohello 範本。 您可以建立不同部署案例中，多個參數檔案，並接著傳入 hello 適當的參數檔案。 

複製 hello 前面範例中，然後將它儲存為檔案命名為`storage.parameters.json`。

toopass 本機參數檔案中，使用 hello **TemplateParameterFile**參數：

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json `
  -TemplateParameterFile c:\MyTemplates\storage.parameters.json
```

toopass 的外部參數檔案，使用 hello **TemplateParameterUri**參數：

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json `
  -TemplateParameterUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.parameters.json
```

您可以使用內嵌參數與本機參數檔案中 hello 相同部署作業。 比方說，您可以在 hello 本機參數檔案中指定某些值，並新增其他值內嵌在部署期間。 如果您提供參數的值在 hello 本機參數檔案和內嵌，hello 內嵌值的優先順序較高。

不過，當使用外部參數檔案時，您無法傳遞內嵌或本機檔案的其他值。 當您指定的參數檔案中 hello **TemplateParameterUri**參數，所有內嵌參數被忽略。 提供 hello 外部檔案中的所有參數值。 如果您的範本包含機密值，您不能包含 hello 參數檔案中，新增該值 tooa 金鑰保存庫，或是以動態方式提供所有參數值內嵌。

如果您的範本包含具有相同的名稱，做為其中一個 hello PowerShell 命令中的 hello 參數 hello 的參數，PowerShell 會顯示 hello 參數，從您的範本與 hello 後置**FromTemplate**。 例如，名為的參數**ResourceGroupName**在您範本與 hello 衝突**ResourceGroupName**中 hello 參數[新增 AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment)cmdlet。 值是提示的 tooprovide **ResourceGroupNameFromTemplate**。 一般情況下，您應該避免混淆，未指名參數，以做為部署作業所使用的參數名稱相同的 hello。

## <a name="test-a-template-deployment"></a>測試範本部署

您的範本和參數值，而不實際部署任何資源，使用 tootest[測試 AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/test-azurermresourcegroupdeployment)。 

```powershell
Test-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json -storageAccountType Standard_GRS
```

如果偵測不到任何錯誤，hello 命令執行完成，無回應。 如果偵測到錯誤時，hello 命令會傳回錯誤訊息。 例如，嘗試 toopass hello 儲存體帳戶 SKU 不正確的值會傳回下列錯誤 hello:

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName testgroup `
  -TemplateFile c:\MyTemplates\storage.json -storageAccountType badSku

Code    : InvalidTemplate
Message : Deployment template validation failed: 'hello provided value 'badSku' for hello template parameter 'storageAccountType'
          at line '15' and column '24' is not valid. hello parameter value is not part of hello allowed value(s):
          'Standard_LRS,Standard_ZRS,Standard_GRS,Standard_RAGRS,Premium_LRS'.'.
Details :
```

如果您的範本有語法錯誤，hello 命令會傳回錯誤，指出無法剖析 hello 範本。 hello 訊息表示 hello 行號和 hello 剖析錯誤的位置。

```powershell
Test-AzureRmResourceGroupDeployment : After parsing a value an unexpected character was encountered: 
  ". Path 'variables', line 31, position 3.
```

[!INCLUDE [resource-manager-deployments](../../includes/resource-manager-deployments.md)]

toouse 完成模式中，使用 hello`Mode`參數：

```powershell
New-AzureRmResourceGroupDeployment -Mode Complete -Name ExampleDeployment `
  -ResourceGroupName ExampleResourceGroup -TemplateFile c:\MyTemplates\storage.json 
```

## <a name="sample-template"></a>範例範本

hello 下列範本會用於本主題中的 hello 範例。 請複製它並另存為名叫 storage.json 的檔案。 toounderstand 如何 toocreate 此範本，請參閱[建立第一個 Azure Resource Manager 範本](resource-manager-create-first-template.md)。  

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageAccountType": {
      "type": "string",
      "defaultValue": "Standard_LRS",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS",
        "Standard_ZRS",
        "Premium_LRS"
      ],
      "metadata": {
        "description": "Storage Account type"
      }
    }
  },
  "variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), 'standardsa')]"
  },
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[variables('storageAccountName')]",
      "apiVersion": "2016-01-01",
      "location": "[resourceGroup().location]",
      "sku": {
          "name": "[parameters('storageAccountType')]"
      },
      "kind": "Storage", 
      "properties": {
      }
    }
  ],
  "outputs": {
      "storageAccountName": {
          "type": "string",
          "value": "[variables('storageAccountName')]"
      }
  }
}
```

## <a name="next-steps"></a>後續步驟
* 本文中的 hello 範例部署中預設訂用帳戶資源 tooa 資源群組。 toouse 不同的訂用帳戶，請參閱[管理多個 Azure 訂用帳戶](/powershell/azure/manage-subscriptions-azureps)。
* 如需部署範本的完整範例指令碼，請參閱 [Resource Manager 範本部署指令碼](resource-manager-samples-powershell-deploy.md)。
* 如何 toodefine 參數在範本中，請參閱的 toounderstand [hello 結構和語法的 Azure 資源管理員範本了解](resource-group-authoring-templates.md)。
* 如需解決常見部署錯誤的秘訣，請參閱[使用 Azure Resource Manager 針對常見的 Azure 部署錯誤進行疑難排解](resource-manager-common-deployment-errors.md)。
* 如需部署需要 SAS 權杖之範本的詳細資訊，請參閱[使用 SAS 權杖部署私人範本](resource-manager-powershell-sas-token.md)。
* 如需指引企業可以如何使用資源管理員 tooeffectively 管理訂用帳戶，請參閱[Azure 企業版 scaffold-精準的訂閱控管](resource-manager-subscription-governance.md)。

