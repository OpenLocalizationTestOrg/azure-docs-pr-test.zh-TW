---
title: "使用 Azure CLI 和範本 aaaDeploy 資源 |Microsoft 文件"
description: "使用 Azure 資源管理員和 Azure CLI toodeploy 資源 tooAzure。 hello 資源的資源管理員範本中定義。"
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 493b7932-8d1e-4499-912c-26098282ec95
ms.service: azure-resource-manager
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/31/2017
ms.author: tomfitz
ms.openlocfilehash: 9f8bb9a8720399390a407030d2d32bcd97d32f13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-azure-cli"></a>使用 Resource Manager 範本與 Azure CLI 部署資源

本主題說明如何使用資源管理員範本 toodeploy toouse Azure CLI 2.0 資源 tooAzure。 如果您不熟悉以部署的 hello 概念，並管理您的 Azure 解決方案，請參閱[Azure 資源管理員概觀](resource-group-overview.md)。  

您所部署的 hello Resource Manager 範本可為您的電腦上的本機檔案或位於等 GitHub 儲存機制中的外部檔案。 您在本文中部署的 hello 範本位於 hello[範例範本](#sample-template) 區段中，或為[GitHub 中的儲存體帳戶範本](https://github.com/Azure/azure-quickstart-templates/blob/master/101-storage-account-create/azuredeploy.json)。

[!INCLUDE [sample-cli-install](../../includes/sample-cli-install.md)]

如果您沒有 Azure CLI 安裝，您可以使用 hello[雲端殼層](#deploy-template-from-cloud-shell)。

## <a name="deploy-local-template"></a>部署本機範本

部署資源 tooAzure 時您：

1. 登入 tooyour Azure 帳戶
2. 建立可做為部署的 hello 資源的 hello 容器的資源群組。 hello hello 資源群組名稱只可包含英數字元、 句號、 底線、 連字號及括號。 它可以是 too90 字元組成。 不能以句點結束。
3. 部署 toohello 資源群組 hello 範本定義 hello 資源 toocreate

範本可以包含 toocustomize hello 部署可讓您的參數。 例如，您可以提供針對特定環境 (例如開發、測試和生產) 量身訂做的值。 hello 範例範本定義 hello 儲存體帳戶 SKU 的參數。 

hello 下列範例會建立資源群組，並部署範本從本機電腦：

```azurecli
az login

az group create --name ExampleGroup --location "Central US"
az group deployment create \
    --name ExampleDeployment \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters storageAccountType=Standard_GRS
```

hello 部署可能需要幾分鐘的時間 toocomplete。 完成時，您會看到訊息，其中包含 hello 結果：

```azurecli
"provisioningState": "Succeeded",
```

## <a name="deploy-external-template"></a>部署外部範本

而不是儲存在本機電腦上的資源管理員範本，您可能會想 toostore 外部位置中。 您可以將範本儲存在原始檔控制存放庫 (例如 GitHub) 中。 或者，您可以將它們儲存在 Azure 儲存體帳戶中，以在組織內共用存取。

toodeploy 的外部的範本，請使用 hello**範本 uri**參數。 使用 hello 範例 toodeploy hello 範例範本從 GitHub 中的 hello URI。
   
```azurecli
az login

az group create --name ExampleGroup --location "Central US"
az group deployment create \
    --name ExampleDeployment \
    --resource-group ExampleGroup \
    --template-uri "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json" \
    --parameters storageAccountType=Standard_GRS
```

hello 上述範例要求可公開存取 URI hello 範本，適用於大部分的情況下，因為您的範本不應該包含機密資料。 如果您需要 toospecify 敏感性資料 （例如系統管理員密碼），將值傳遞做為安全的參數。 不過，如果您不想範本 toobe 可公開存取，您可以保護它儲存在私人儲存體容器中。 如需部署需要共用存取簽章 (SAS) 權杖之範本的相關資訊，請參閱[使用 SAS 權杖部署私人範本](resource-manager-cli-sas-token.md)。

## <a name="deploy-template-from-cloud-shell"></a>從 Cloud Shell 部署範本

您可以使用[雲端殼層](../cloud-shell/overview.md)toorun hello Azure CLI 命令來部署您的範本。 不過，您必須先載入您的範本 hello 檔案共用雲端 shell。 如果您尚未使用 Cloud Shell，請參閱 [Azure Cloud Shell 概觀](../cloud-shell/overview.md)以取得如何設定的相關資訊。

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。   

2. 選取您的 Cloud Shell 資源群組。 hello 名稱模式`cloud-shell-storage-<region>`。

   ![選取資源群組](./media/resource-group-template-deploy-cli/select-cs-resource-group.png)

3. 選取您的雲端 Shell hello 儲存體帳戶。

   ![選取儲存體帳戶](./media/resource-group-template-deploy-cli/select-storage.png)

4. 選取 [檔案]。

   ![選取檔案](./media/resource-group-template-deploy-cli/select-files.png)

5. 選取雲端殼層 hello 檔案共用。 hello 名稱模式`cs-<user>-<domain>-com-<uniqueGuid>`。

   ![選取檔案共用](./media/resource-group-template-deploy-cli/select-file-share.png)

6. 選取 [新增目錄]。

   ![新增目錄](./media/resource-group-template-deploy-cli/select-add-directory.png)

7. 將它命名為 **templates**，然後選取 [確定]。

   ![命名目錄](./media/resource-group-template-deploy-cli/name-templates.png)

8. 選取您的新目錄。

   ![選取目錄](./media/resource-group-template-deploy-cli/select-templates.png)

9. 選取 [上傳] 。

   ![選取上傳](./media/resource-group-template-deploy-cli/select-upload.png)

10. 尋找並上傳您的範本。

   ![上傳檔案](./media/resource-group-template-deploy-cli/upload-files.png)

11. 開啟 hello 提示字元。

   ![開啟 Cloud Shell](./media/resource-group-template-deploy-cli/start-cloud-shell.png)

12. 輸入 hello 遵循 hello 雲端殼層中的命令：

   ```azurecli
   az group create --name examplegroup --location "South Central US"
   az group deployment create --resource-group examplegroup --template-file clouddrive/templates/azuredeploy.json --parameters storageAccountType=Standard_GRS
   ```

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

toopass 本機參數檔案中，使用`@`toospecify 名為 storage.parameters.json 的本機檔案。

```azurecli
az group deployment create \
    --name ExampleDeployment \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters @storage.parameters.json
```

## <a name="test-a-template-deployment"></a>測試範本部署

您的範本和參數值，而不實際部署任何資源，使用 tootest [az 群組部署驗證](/cli/azure/group/deployment#validate)。 

```azurecli
az group deployment validate \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters @storage.parameters.json
```

如果偵測不到任何錯誤，hello 命令會傳回 hello 測試部署的相關資訊。 特別是，請注意該 hello**錯誤**值為 null。

```azurecli
{
  "error": null,
  "properties": {
      ...
```

如果偵測到錯誤時，hello 命令會傳回錯誤訊息。 例如，嘗試 toopass hello 儲存體帳戶 SKU 不正確的值會傳回下列錯誤 hello:

```azurecli
{
  "error": {
    "code": "InvalidTemplate",
    "details": null,
    "message": "Deployment template validation failed: 'hello provided value 'badSKU' for hello template parameter 
      'storageAccountType' at line '13' and column '20' is not valid. hello parameter value is not part of hello allowed 
      value(s): 'Standard_LRS,Standard_ZRS,Standard_GRS,Standard_RAGRS,Premium_LRS'.'.",
    "target": null
  },
  "properties": null
}
```

如果您的範本有語法錯誤，hello 命令會傳回錯誤，指出無法剖析 hello 範本。 hello 訊息表示 hello 行號和 hello 剖析錯誤的位置。

```azurecli
{
  "error": {
    "code": "InvalidTemplate",
    "details": null,
    "message": "Deployment template parse failed: 'After parsing a value an unexpected character was encountered:
      \". Path 'variables', line 31, position 3.'.",
    "target": null
  },
  "properties": null
}
```

[!INCLUDE [resource-manager-deployments](../../includes/resource-manager-deployments.md)]

toouse 完成模式中，使用 hello`mode`參數：

```azurecli
az group deployment create \
    --name ExampleDeployment \
    --mode Complete \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters storageAccountType=Standard_GRS
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
* 本文中的 hello 範例部署中預設訂用帳戶資源 tooa 資源群組。 toouse 不同的訂用帳戶，請參閱[管理多個 Azure 訂用帳戶](/cli/azure/manage-azure-subscriptions-azure-cli)。
* 如需部署範本的完整範例指令碼，請參閱 [Resource Manager 範本部署指令碼](resource-manager-samples-cli-deploy.md)。
* 如何 toodefine 參數在範本中，請參閱的 toounderstand [hello 結構和語法的 Azure 資源管理員範本了解](resource-group-authoring-templates.md)。
* 如需解決常見部署錯誤的秘訣，請參閱[使用 Azure Resource Manager 針對常見的 Azure 部署錯誤進行疑難排解](resource-manager-common-deployment-errors.md)。
* 如需部署需要 SAS 權杖之範本的詳細資訊，請參閱[使用 SAS 權杖部署私人範本](resource-manager-cli-sas-token.md)。
* 如需指引企業可以如何使用資源管理員 tooeffectively 管理訂用帳戶，請參閱[Azure 企業版 scaffold-精準的訂閱控管](resource-manager-subscription-governance.md)。
