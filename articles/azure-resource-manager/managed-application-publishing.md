---
title: "aaaCreate 和發行的 Azure 服務管理的類別目錄的應用程式 |Microsoft 文件"
description: "顯示如何 toocreate Azure 管理應用程式，僅供貴組織的成員。"
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 08/23/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: 31f2f9e3b50f57dae7f4dcf2edefa7366bfff25c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="publish-a-managed-application-for-internal-consumption"></a>發佈受管理的應用程式，以供內部使用

您可以建立及發佈 Azure [受管理的應用程式](managed-application-overview.md)，以供組織成員使用。 例如，IT 部門可以發佈受管理的應用程式，以確保符合組織標準。 這些受管理的應用程式皆可透過 hello 服務類別目錄，hello Azure Marketplace。

toopublish hello 服務類別目錄的受管理應用程式，您必須：

* 建立包含三個所需的範本檔案 hello 以.zip 封裝。
* 決定哪些使用者、 群組或應用程式需要存取 toohello hello 使用者訂用帳戶中的資源群組。
* 建立 hello 受管理應用程式定義點 toohello.zip 套件，並要求 hello 身分識別的存取權。

## <a name="create-a-managed-application-package"></a>建立受管理的應用程式套件

hello 第一個步驟是 toocreate hello 三個所需的範本檔案。 這三個檔案封裝成.zip 檔，並將它上傳 tooan 可存取的位置，例如儲存體帳戶。 建立 hello 受管理的應用程式定義時，您可以傳遞連結 toothis.zip 檔案。

* **applianceMainTemplate.json**： 此檔案會定義 hello Azure 管理應用程式的一部分 hello 佈建的資源。 hello 範本並無不同規則的 Resource Manager 範本。 例如，toocreate 透過 managed 應用程式的儲存體帳戶，applianceMainTemplate.json 包含：

  ```json
  {
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "storageAccountNamePrefix": {
            "type": "string"
        }
    },
    "resources": [
        {
            "type": "Microsoft.Storage/storageAccounts",
            "name": "[concat(parameters('storageAccountNamePrefix'), uniqueString(resourceGroup().id))]",
            "apiVersion": "2016-01-01",
            "location": "[resourceGroup().location]",
            "sku": {
                "name": "Standard_LRS"
            },
            "kind": "Storage",
            "properties": {}
        }
    ],
    "outputs": {}
  }
  ```

* **mainTemplate.json**： 建立 hello 受管理的應用程式時，使用者將部署此範本。 它會定義受管理的 hello 應用程式資源，也就是 Microsoft.Solutions/appliances 資源類型。 此檔案包含所有的 hello 參數，您需要的 applianceMainTemplate.json hello 資源。

  您會在此範本中設定兩個重要的屬性。 首先，hello **applianceDefinitionId**屬性是 hello 識別碼 hello 受管理應用程式定義。 您在本主題稍後建立 hello 定義。 設定此值時，您必須決定哪些訂用帳戶和儲存資源群組 toouse hello 受管理的應用程式定義。 而且，您必須決定 hello 定義的名稱。 hello 識別碼的 hello 格式：

  `/subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Solutions/applianceDefinitions/<definition-name>`

  第二，hello **managedResourceGroupId**屬性是 hello hello 資源群組識別碼 hello Azure 資源建立的位置。 您可以指派值給這個資源群組名稱，或讓 hello 使用者提供的名稱。 hello 的 hello 識別碼的格式如下：

  `/subscriptions/<subscription-id>/resourceGroups/<resoure-group-name>`。

  下列範例中的 hello 顯示 mainTemplate.json 檔案。 它會指定部署的 hello 資源的資源群組。 hello 定義 ID 已定義命名集 toouse **storageApp**資源群組中名為**managedApplicationGroup**。 您可以變更這些值 toouse 不同的名稱。 提供您自己的訂用帳戶 ID 中 hello 定義 id。

  ```json
  {
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "storageAccountNamePrefix": {
            "type": "string"
        }
    },
    "variables": {
        "managedRGId": "[concat(resourceGroup().id,'-application-resources')]",
        "managedAppName": "[concat('managedStorage', uniqueString(resourceGroup().id))]"
    },
    "resources": [
        {
            "type": "Microsoft.Solutions/appliances",
            "name": "[variables('managedAppName')]",
            "apiVersion": "2016-09-01-preview",
            "location": "[resourceGroup().location]",
            "kind": "ServiceCatalog",
            "properties": {
                "managedResourceGroupId": "[variables('managedRGId')]",
                "applianceDefinitionId": "/subscriptions/<subscription-id>/resourceGroups/managedApplicationGroup/providers/Microsoft.Solutions/applianceDefinitions/storageApp",
                "parameters": {
                    "storageAccountNamePrefix": {
                        "value": "[parameters('storageAccountNamePrefix')]"
                    }
                }
            }
        }
    ]
  }
  ```

* **applianceCreateUiDefinition.json**: hello Azure 入口網站會使用這個檔案 toogenerate hello 使用者介面的使用者建立 hello 受管理的應用程式。 您可以定義使用者提供每個參數輸入的方式。 您可以使用諸如下拉式清單、文字方塊、密碼方塊和其他輸入工具等選項。 如何 toocreate UI 定義檔案為受管理的應用程式，請參閱的 toolearn[開始使用 CreateUiDefinition](managed-application-createuidefinition-overview.md)。

  hello 下列範例顯示 applianceCreateUiDefinition.json 檔案，可讓使用者 toospecify hello 儲存體帳戶名稱前置詞到文字方塊。

  ```json
  {
    "$schema": "https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json",
    "handler": "Microsoft.Compute.MultiVm",
    "version": "0.1.2-preview",
    "parameters": {
        "basics": [
            {
                "name": "storageAccounts",
                "type": "Microsoft.Common.TextBox",
                "label": "Storage account name prefix",
                "defaultValue": "storage",
                "toolTip": "Provide a value that is used for hello prefix of your storage account. Limit too11 characters.",
                "constraints": {
                    "required": true,
                    "regex": "^[a-z0-9A-Z]{1,11}$",
                    "validationMessage": "Only alphanumeric characters are allowed, and hello value must be 1-11 characters long."
                },
                "visible": true
            }
        ],
        "steps": [],
        "outputs": {
            "storageAccountNamePrefix": "[basics('storageAccounts')]"
        }
    }
  }
  ```

準備好 hello 所需的所有檔案後，封裝它們的.zip 檔。 hello 三個檔案必須位於根層級 hello hello.zip 檔案。 如果您將其放在資料夾中，建立 hello 受管理的應用程式定義指出 hello 所需的檔案不存在時收到錯誤。 上傳從可以取用它的 hello 封裝 tooan 存取位置。 hello 本文其餘部分會假設 hello.zip 檔案存在於可公開存取的儲存體 blob 容器。

## <a name="create-an-azure-active-directory-user-group-or-application"></a>建立 Azure Active Directory 使用者群組或應用程式

tooselect 使用者群組或應用程式管理 hello 資源代表 hello 客戶 hello 第二個步驟。 此使用者群組或應用程式對 hello 受管理的資源群組相應 toohello 角色指派的權限。 hello 角色可以是任何內建的角色型存取控制 (RBAC) 角色，例如擁有者或參與者。 您也可以提供個別的使用者權限 toomanage hello 資源，但您通常指派此權限 tooa 使用者群組。 toocreate 新的 Active Directory 使用者群組，請參閱[建立群組並新增 Azure Active Directory 中的成員](../active-directory/active-directory-groups-create-azure-portal.md)。

您用於管理 hello 資源需要 hello 使用者群組 toouse hello 物件識別碼。 hello 下列範例顯示如何 tooget hello 從 hello 群組的顯示名稱的物件識別碼：

```azurecli-interactive
az ad group show --group exampleGroupName
```

hello 範例命令會傳回下列輸出的 hello:

```azurecli
{
    "displayName": "exampleGroupName",
    "mail": null,
    "objectId": "9aabd3ad-3716-4242-9d8e-a85df479d5d9",
    "objectType": "Group",
    "securityEnabled": true
}
```

tooretrieve 只 hello 物件識別碼，使用：

```azurecli-interactive
groupid=$(az ad group show --group exampleGroupName --query objectId --output tsv)
```

## <a name="get-hello-role-definition-id"></a>取得 hello 角色定義 ID

接下來，您需要 hello RBAC toogrant 存取 toohello 使用者、 使用者群組或應用程式的內建角色 hello 角色定義 ID。 通常，您會使用 hello 擁有者或參與者或讀取器角色。 hello，下列命令顯示如何 tooget hello hello 擁有者角色的角色定義 ID:


```azurecli-interactive
az role definition list --name owner
```

該命令會傳回下列輸出的 hello:

```azurecli
{
    "id": "/subscriptions/<subscription-id>/providers/Microsoft.Authorization/roleDefinitions/8e3af657-a8ff-443c-a75c-2fe8c4bcb635",
    "name": "8e3af657-a8ff-443c-a75c-2fe8c4bcb635",
    "properties": {
      "assignableScopes": [
        "/"
      ],
      "description": "Lets you manage everything, including access tooresources.",
      "permissions": [
        {
          "actions": [
            "*"
         ],
         "notActions": []
        }
      ],
      "roleName": "Owner",
      "type": "BuiltInRole"
    },
    "type": "Microsoft.Authorization/roleDefinitions"
}
```

您需要從前面範例中的 hello hello"name"屬性 hello 值。 您可以透過下列程式碼只擷取該屬性：

```azurecli-interactive
roleid=$(az role definition list --name Owner --query [].name --output tsv)
```

## <a name="create-hello-managed-application-definition"></a>建立 hello 受管理應用程式定義

如果您尚未有可儲存受管理應用程式定義的資源群組，請立即建立一個：

```azurecli-interactive
az group create --name managedApplicationGroup --location westcentralus
```

現在，建立 hello 受管理應用程式定義的資源。

```azurecli-interactive
az managedapp definition create \
  --name storageApp \
  --location "westcentralus" \
  --resource-group managedApplicationGroup \
  --lock-level ReadOnly \
  --display-name myteststorageapp \
  --description storageapp \
  --authorizations "$groupid:$roleid" \
  --package-file-uri <uri-path-to-zip-file>
```

hello hello 前面範例中使用的參數如下：

* **資源群組**： 建立 hello hello hello 要受管理應用程式定義的資源群組名稱。
* **鎖定層級**: hello 鎖定類型的放置 hello 受管理的資源群組。 它可以防止 hello 客戶執行非預期的作業上此資源群組。 目前，ReadOnly 是 hello 才支援鎖定層級。 當指定 ReadOnly 時，hello 客戶只能讀取 hello hello 受管理的資源群組中的資源。
* **授權**： 描述 hello 主體識別碼和 hello 角色定義 ID 使用的 toogrant 權限 toohello 受管理的資源群組。 指定格式的 hello `<principalId>:<roleDefinitionId>`。 這個屬性也可以指定多個值。 如果需要多個值，則應該指定 hello 形式`<principalId1>:<roleDefinitionId1> <principalId2>:<roleDefinitionId2>`。 多個值之間以空格分隔。
* **封裝檔案 uri**: hello hello hello 範本，其中包含檔案可以是 Azure 儲存體 blob 的受管理的應用程式封裝的位置。

## <a name="next-steps"></a>後續步驟

* 對於簡介 toomanaged 應用程式，請參閱[受管理應用程式概觀](managed-application-overview.md)。
* 如需 hello 檔案的範例，請參閱[受管理應用程式範例](https://github.com/Azure/azure-managedapp-samples/tree/master/samples)。
* 如需使用 Service Catalog 受管理應用程式的詳細資訊，請參閱[使用 Service Catalog 受管理的應用程式](managed-application-consumption.md)。
* 發佈受管理的應用程式 toohello Azure Marketplace 的相關資訊，請參閱[Azure 受管理應用程式在 hello Marketplace](managed-application-author-marketplace.md)。
* 使用來自 hello Marketplace 的受管理應用程式的相關資訊，請參閱[取用 Azure managed hello Marketplace 中的應用程式](managed-application-consume-marketplace.md)。
* 如何 toocreate UI 定義檔案為受管理的應用程式，請參閱的 toolearn[開始使用 CreateUiDefinition](managed-application-createuidefinition-overview.md)。
