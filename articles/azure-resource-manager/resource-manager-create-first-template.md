---
title: "第一個 Azure Resource Manager 範本 aaaCreate |Microsoft 文件"
description: "逐步指南 toocreating 第一個的 Azure Resource Manager 範本。 它會顯示您如何 toouse hello 範本參考儲存體帳戶 toocreate hello 範本。"
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 07/27/2017
ms.topic: get-started-article
ms.author: tomfitz
ms.openlocfilehash: 92e6d6bb7094fe0e4537ee080704967862804bdb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-your-first-azure-resource-manager-template"></a>建立及部署第一個 Azure Resource Manager 範本
本主題會引導您建立第一個的 Azure Resource Manager 範本的 hello 步驟。 資源管理員範本是定義您的解決方案需 toodeploy hello 資源的 JSON 檔案。 請參閱 < 部署和管理 Azure 解決方案，相關聯的 toounderstand hello 概念[Azure 資源管理員概觀](resource-group-overview.md)。 如果您有現有的資源，並想 tooget 範本，這些資源，請參閱[匯出 Azure Resource Manager 範本，從現有的資源](resource-manager-export-template.md)。

toocreate 和修訂的範本，您需要 JSON 編輯器。 [Visual Studio Code](https://code.visualstudio.com/) 是輕量型、開放原始碼、跨平台的程式碼編輯器。 強烈建議使用 Visual Studio Code 來建立 Resource Manager 範本。 本主題假設您使用 VS Code；不過，如果您有其他 JSON 編輯器 (如 Visual Studio)，您可以使用該編輯器。

## <a name="prerequisites"></a>必要條件

* Visual Studio Code。 如有需要，請從 [https://code.visualstudio.com/](https://code.visualstudio.com/) 進行安裝。
* Azure 訂用帳戶。 如果您沒有 Azure 訂用帳戶，請在開始前建立 [免費帳戶](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) 。

## <a name="create-template"></a>建立範本

讓我們開始與簡單的範本部署儲存體帳戶 tooyour 訂用帳戶。

1. 選取 [檔案] > [新增檔案]。 

   ![新增檔案](./media/resource-manager-create-first-template/new-file.png)

2. 複製並貼到您的檔案使用下列 JSON 語法 hello:

   ```json
   {
     "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
     "contentVersion": "1.0.0.0",
     "parameters": {
     },
     "variables": {
     },
     "resources": [
       {
         "name": "[concat('storage', uniqueString(resourceGroup().id))]",
         "type": "Microsoft.Storage/storageAccounts",
         "apiVersion": "2016-01-01",
         "sku": {
           "name": "Standard_LRS"
         },
         "kind": "Storage",
         "location": "South Central US",
         "tags": {},
         "properties": {}
       }
     ],
     "outputs": {  }
   }
   ```

   儲存體帳戶名稱中有許多限制，使其難以 tooset。 hello 名稱必須介於 3 到 24 個字元，長度、 使用數字和小寫字母，而且是唯一。 hello 上述範本使用 hello [uniqueString](resource-group-template-functions-string.md#uniquestring)函式 toogenerate 雜湊值。 此雜湊值表示多 toogive，便會新增 hello 前置詞*儲存體*。 

3. 將此檔案儲存為**azuredeploy.json** tooa 本機資料夾。

   ![儲存範本](./media/resource-manager-create-first-template/save-template.png)

## <a name="deploy-template"></a>部署範本

您已準備好 toodeploy 此範本。 您使用 PowerShell 或 Azure CLI toocreate 資源群組。 接著，您將部署的儲存體帳戶 toothat 資源群組。

* 如需 PowerShell，使用 hello hello 包含 hello 範本的資料夾中的下列命令：

   ```powershell
   Login-AzureRmAccount
   
   New-AzureRmResourceGroup -Name examplegroup -Location "South Central US"
   New-AzureRmResourceGroupDeployment -ResourceGroupName examplegroup -TemplateFile azuredeploy.json
   ```

* 使用 Azure CLI 是本機安裝，hello hello 包含 hello 範本的資料夾中的下列命令：

   ```azurecli
   az login

   az group create --name examplegroup --location "South Central US"
   az group deployment create --resource-group examplegroup --template-file azuredeploy.json
   ```

當部署完成時，則會在 hello 資源群組中有儲存體帳戶。

## <a name="deploy-template-from-cloud-shell"></a>從 Cloud Shell 部署範本

您可以使用[雲端殼層](../cloud-shell/overview.md)toorun hello Azure CLI 命令來部署您的範本。 不過，您必須先載入您的範本 hello 檔案共用雲端 shell。 如果您尚未使用 Cloud Shell，請參閱 [Azure Cloud Shell 概觀](../cloud-shell/overview.md)以取得如何設定的相關資訊。

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。   

2. 選取您的 Cloud Shell 資源群組。 hello 名稱模式`cloud-shell-storage-<region>`。

   ![選取資源群組](./media/resource-manager-create-first-template/select-cs-resource-group.png)

3. 選取您的雲端 Shell hello 儲存體帳戶。

   ![選取儲存體帳戶](./media/resource-manager-create-first-template/select-storage.png)

4. 選取 [檔案]。

   ![選取檔案](./media/resource-manager-create-first-template/select-files.png)

5. 選取雲端殼層 hello 檔案共用。 hello 名稱模式`cs-<user>-<domain>-com-<uniqueGuid>`。

   ![選取檔案共用](./media/resource-manager-create-first-template/select-file-share.png)

6. 選取 [新增目錄]。

   ![新增目錄](./media/resource-manager-create-first-template/select-add-directory.png)

7. 將它命名為 **templates**，然後選取 [確定]。

   ![命名目錄](./media/resource-manager-create-first-template/name-templates.png)

8. 選取您的新目錄。

   ![選取目錄](./media/resource-manager-create-first-template/select-templates.png)

9. 選取 [上傳] 。

   ![選取上傳](./media/resource-manager-create-first-template/select-upload.png)

10. 尋找並上傳您的範本。

   ![上傳檔案](./media/resource-manager-create-first-template/upload-files.png)

11. 開啟 hello 提示字元。

   ![開啟 Cloud Shell](./media/resource-manager-create-first-template/start-cloud-shell.png)

12. 輸入 hello 遵循 hello 雲端殼層中的命令：

   ```azurecli
   az group create --name examplegroup --location "South Central US"
   az group deployment create --resource-group examplegroup --template-file clouddrive/templates/azuredeploy.json
   ```

當部署完成時，則會在 hello 資源群組中有儲存體帳戶。

## <a name="customize-hello-template"></a>自訂 hello 範本

hello 範本可正常運作，但不是有彈性。 一律將部署本機備援儲存體 tooSouth 美國中部。 hello 名稱永遠是*儲存體*後面雜湊值。 tooenable hello 範本使用不同的情況下，新增參數 toohello 範本。

hello 下列範例示範具有兩個參數的 hello 參數 > 一節。 hello 第一個參數`storageSKU`可讓您的備援 toospecify hello 型別。 它會限制您可以傳入有效的儲存體帳戶 toovalues hello 值。 它也會指定預設值。 hello 第二個參數`storageNamePrefix`是集 tooallow 11 個字元的最大值。 它會指定預設值。

```json
"parameters": {
  "storageSKU": {
    "type": "string",
    "allowedValues": [
      "Standard_LRS",
      "Standard_ZRS",
      "Standard_GRS",
      "Standard_RAGRS",
      "Premium_LRS"
    ],
    "defaultValue": "Standard_LRS",
    "metadata": {
      "description": "hello type of replication toouse for hello storage account."
    }
  },
  "storageNamePrefix": {
    "type": "string",
    "maxLength": 11,
    "defaultValue": "storage",
    "metadata": {
      "description": "hello value toouse for starting hello storage account name. Use only lowercase letters and numbers."
    }
  }
},
```

在 hello 變數區段中，加入名為的變數`storageName`。 它會結合 hello hello 參數前置詞值和雜湊值從 hello [uniqueString](resource-group-template-functions-string.md#uniquestring)函式。 它會使用 hello [toLower](resource-group-template-functions-string.md#tolower)函式 tooconvert 所有字元 toolowercase。

```json
"variables": {
  "storageName": "[concat(toLower(parameters('storageNamePrefix')), uniqueString(resourceGroup().id))]"
},
```

toouse 儲存體帳戶，這些新值會變更 hello 資源定義：

```json
"resources": [
  {
    "name": "[variables('storageName')]",
    "type": "Microsoft.Storage/storageAccounts",
    "apiVersion": "2016-01-01",
    "sku": {
      "name": "[parameters('storageSKU')]"
    },
    "kind": "Storage",
    "location": "[resourceGroup().location]",
    "tags": {},
    "properties": {}
  }
],
```

請注意該 hello hello 儲存體帳戶名稱現在已設定您加入的 toohello 變數。 hello SKU 名稱設定 toohello hello 參數值。 hello 位置會設定 hello 與 hello 資源群組相同的位置。

儲存您的檔案。 

完成本文章中的 hello 步驟之後，您範本現在看起來像：

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageSKU": {
      "type": "string",
      "allowedValues": [
        "Standard_LRS",
        "Standard_ZRS",
        "Standard_GRS",
        "Standard_RAGRS",
        "Premium_LRS"
      ],
      "defaultValue": "Standard_LRS",
      "metadata": {
        "description": "hello type of replication toouse for hello storage account."
      }
    },   
    "storageNamePrefix": {
      "type": "string",
      "maxLength": 11,
      "defaultValue": "storage",
      "metadata": {
        "description": "hello value toouse for starting hello storage account name. Use only lowercase letters and numbers."
      }
    }
  },
  "variables": {
    "storageName": "[concat(toLower(parameters('storageNamePrefix')), uniqueString(resourceGroup().id))]"
  },
  "resources": [
    {
      "name": "[variables('storageName')]",
      "type": "Microsoft.Storage/storageAccounts",
      "apiVersion": "2016-01-01",
      "sku": {
        "name": "[parameters('storageSKU')]"
      },
      "kind": "Storage",
      "location": "[resourceGroup().location]",
      "tags": {},
      "properties": {}
    }
  ],
  "outputs": {  }
}
```

## <a name="redeploy-template"></a>重新部署範本

重新部署 hello 範本有不同的值。

對於 PowerShell，請使用：

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName examplegroup -TemplateFile azuredeploy.json -storageNamePrefix newstore -storageSKU Standard_RAGRS
```

對於 Azure CLI，請使用：

```azurecli
az group deployment create --resource-group examplegroup --template-file azuredeploy.json --parameters storageSKU=Standard_RAGRS storageNamePrefix=newstore
```

Hello 雲端殼層上, 傳您已變更的範本 toohello 檔案共用。 覆寫 hello 現有檔案。 然後，使用下列命令的 hello:

```azurecli
az group deployment create --resource-group examplegroup --template-file clouddrive/templates/azuredeploy.json --parameters storageSKU=Standard_RAGRS storageNamePrefix=newstore
```

## <a name="clean-up-resources"></a>清除資源

當不再需要請清除您藉由刪除 hello 資源群組部署的 hello 資源。

對於 PowerShell，請使用：

```powershell
Remove-AzureRmResourceGroup -Name examplegroup
```

對於 Azure CLI，請使用：

```azurecli
az group delete --name examplegroup
```

## <a name="next-steps"></a>後續步驟
* toolearn 進一步了解 hello 結構的範本，請參閱[撰寫 Azure 資源管理員範本](resource-group-authoring-templates.md)。
* toolearn 有關 hello 屬性儲存體帳戶，請參閱[儲存體帳戶的範本參考](/azure/templates/microsoft.storage/storageaccounts)。
* tooview 完成範本的許多不同類型的方案，請參閱 hello [Azure 快速入門範本](https://azure.microsoft.com/documentation/templates/)。
