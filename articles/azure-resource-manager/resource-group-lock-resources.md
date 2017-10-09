---
title: "aaaLock Azure 資源 tooprevent 變更 |Microsoft 文件"
description: "透過將鎖定套用到所有使用者和角色，防止使用者更新或刪除重要的 Azure 資源。"
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 53c57e8f-741c-4026-80e0-f4c02638c98b
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: tomfitz
ms.openlocfilehash: 1f0d8911b2b129069bd2f01a9a4ec0a3cf700118
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="lock-resources-tooprevent-unexpected-changes"></a>鎖定資源 tooprevent 突如其來的變化 
身為管理員，您可能需要 toolock 訂用帳戶、 資源群組或資源 tooprevent 不小心刪除或修改重要的資源組織中其他使用者。 您可以設定 hello 鎖定層級太**CanNotDelete**或**ReadOnly**。 

* **CanNotDelete**表示授權的使用者仍然可以讀取和修改資源，但無法刪除 hello 資源。 
* **ReadOnly**表示授權的使用者可以讀取資源，但不能刪除或更新 hello 的資源。 套用這個鎖定是所有授權使用者 toohello 權限授與的 hello 類似 toorestricting**讀取器**角色。 

## <a name="how-locks-are-applied"></a>如何套用鎖定

當您套用在父範圍的鎖定時，該範圍內的所有資源都繼承 hello 相同的鎖定。 即使您稍後新增的資源會繼承 hello 父系中的 hello 鎖定。 hello hello 繼承中限制最嚴格的鎖定會優先使用。

不同於以角色為基礎的存取控制，您可以使用管理鎖定 tooapply 限制跨所有使用者和角色。 toolearn 有關設定權限的使用者和角色，請參閱[Azure 角色型存取控制](../active-directory/role-based-access-control-configure.md)。

資源管理員鎖定套用在 hello 管理平面組成太傳送作業中發生的 toooperations`https://management.azure.com`。 hello 鎖定不會限制資源如何執行他們自己的函式。 限制資源的變更，但沒有限制資源的作業。 例如，SQL Database 的 ReadOnly 鎖定可防止您刪除或修改 hello 資料庫，但它不會阻止您建立、 更新或刪除 hello 資料庫中的資料。 可以使用資料的交易，因為這些作業不會傳送過`https://management.azure.com`。

套用**ReadOnly**可能會造成 toounexpected 結果，因為看起來雖然某些作業讀取作業實際需要的其他動作。 例如，放置**ReadOnly**儲存體帳戶上的鎖定可防止所有使用者列出 hello 索引鍵。 hello 清單索引鍵作業透過 POST 要求因為 hello 傳回索引鍵是可用的寫入作業。 如需其他範例，放置**ReadOnly** App Service 資源鎖定可防止 Visual Studio 伺服器總管顯示 hello 資源的檔案，因為互動需要寫入權限。

## <a name="who-can-create-or-delete-locks-in-your-organization"></a>誰可以建立或刪除您的組織中的鎖定
toocreate 或刪除管理鎖定，您必須能夠存取太`Microsoft.Authorization/*`或`Microsoft.Authorization/locks/*`動作。 Hello 內建角色時，只有**擁有者**和**使用者存取系統管理員**授與這些動作。

## <a name="portal"></a>入口網站
[!INCLUDE [resource-manager-lock-resources](../../includes/resource-manager-lock-resources.md)]

## <a name="template"></a>範本
hello 下列範例顯示建立鎖定的儲存體帳戶的範本。 hello 哪些 tooapply 當成參數提供 hello 鎖定的儲存體帳戶。 hello hello 鎖定的名稱由串連 hello 資源名稱與**/Microsoft.Authorization/**和 hello hello 鎖定的名稱在此情況下**myLock**。

提供的 hello 型別是特定 toohello 資源類型。 針對存放裝置，設定 hello 類型 too"Microsoft.Storage/storageaccounts/providers/locks 」。

    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "lockedResource": {
          "type": "string"
        }
      },
      "resources": [
        {
          "name": "[concat(parameters('lockedResource'), '/Microsoft.Authorization/myLock')]",
          "type": "Microsoft.Storage/storageAccounts/providers/locks",
          "apiVersion": "2015-01-01",
          "properties": {
            "level": "CannotDelete"
          }
        }
      ]
    }

## <a name="powershell"></a>PowerShell
您的鎖定資源使用 Azure PowerShell 使用部署的 hello[新增 AzureRmResourceLock](/powershell/module/azurerm.resources/new-azurermresourcelock)命令。

toolock 資源時，提供 hello hello 資源名稱、 資源類型，以及其資源群組名稱。

```powershell
New-AzureRmResourceLock -LockLevel CanNotDelete -LockName LockSite `
  -ResourceName examplesite -ResourceType Microsoft.Web/sites `
  -ResourceGroupName exampleresourcegroup
```

資源群組、 toolock 提供 hello hello 資源群組名稱。

```powershell
New-AzureRmResourceLock -LockName LockGroup -LockLevel CanNotDelete `
  -ResourceGroupName exampleresourcegroup
```

鎖定時，使用的 tooget 資訊[Get AzureRmResourceLock](/powershell/module/azurerm.resources/get-azurermresourcelock)。 tooget 所有 hello 鎖定您的訂閱中都使用：

```powershell
Get-AzureRmResourceLock
```

tooget 所有鎖定的資源，都使用：

```powershell
Get-AzureRmResourceLock -ResourceName examplesite -ResourceType Microsoft.Web/sites `
  -ResourceGroupName exampleresourcegroup
```

tooget 所有鎖定的資源群組中，都使用：

```powershell
Get-AzureRmResourceLock -ResourceGroupName exampleresourcegroup
```

Azure PowerShell 提供其他命令工作鎖定，例如[組 AzureRmResourceLock](/powershell/module/azurerm.resources/set-azurermresourcelock) tooupdate 鎖定，以及[移除 AzureRmResourceLock](/powershell/module/azurerm.resources/remove-azurermresourcelock) toodelete 鎖定。

## <a name="azure-cli"></a>Azure CLI

您的鎖定資源使用 Azure CLI 使用部署的 hello [az 鎖定建立](/cli/azure/lock#create)命令。

toolock 資源時，提供 hello hello 資源名稱、 資源類型，以及其資源群組名稱。

```azurecli
az lock create --name LockSite --lock-type CanNotDelete \
  --resource-group exampleresourcegroup --resource-name examplesite \
  --resource-type Microsoft.Web/sites
```

資源群組、 toolock 提供 hello hello 資源群組名稱。

```azurecli
az lock create --name LockGroup --lock-type CanNotDelete \
  --resource-group exampleresourcegroup
```

鎖定時，使用的 tooget 資訊[az 鎖定清單](/cli/azure/lock#list)。 tooget 所有 hello 鎖定您的訂閱中都使用：

```azurecli
az lock list
```

tooget 所有鎖定的資源，都使用：

```azurecli
az lock list --resource-group exampleresourcegroup --resource-name examplesite \
  --namespace Microsoft.Web --resource-type sites --parent ""
```

tooget 所有鎖定的資源群組中，都使用：

```azurecli
az lock list --resource-group exampleresourcegroup
```

Azure CLI 提供其他命令工作鎖定，例如[az 鎖定更新](/cli/azure/lock#update)tooupdate 鎖定，以及[az 鎖定刪除](/cli/azure/lock#delete)toodelete 鎖定。

## <a name="rest-api"></a>REST API
您可以鎖定已部署的資源，以 hello [REST API 管理鎖定](https://docs.microsoft.com/rest/api/resources/managementlocks)。 hello REST API 可讓您 toocreate 及刪除鎖定，以及擷取現有的鎖定有關的資訊。

toocreate 鎖定，執行：

    PUT https://management.azure.com/{scope}/providers/Microsoft.Authorization/locks/{lock-name}?api-version={api-version}

訂用帳戶、 資源群組或資源，可能是 hello 範圍。 hello 鎖定名稱是您所要的任何 toocall hello 鎖定。 對於 api-version，請使用 **2015-01-01**。

Hello 要求中包含的 JSON 物件，指定 hello hello 鎖定屬性。

    {
      "properties": {
        "level": "CanNotDelete",
        "notes": "Optional text notes."
      }
    } 

## <a name="next-steps"></a>後續步驟
* 的如需使用資源鎖定的詳細資訊，請參閱 [鎖定您的 Azure 資源](http://blogs.msdn.com/b/cloud_solution_architect/archive/2015/06/18/lock-down-your-azure-resources.aspx)
* toolearn 需以邏輯方式組織您的資源，請參閱[使用標記 tooorganize 資源](resource-group-using-tags.md)
* toochange 哪一個資源群組資源所在，請參閱[移動資源 toonew 資源群組](resource-group-move-resources.md)
* 您可以使用自訂原則，在訂用帳戶內套用限制和慣例。 如需詳細資訊，請參閱[使用原則 toomanage 資源和控制存取](resource-manager-policy.md)。
* 如需指引企業可以如何使用資源管理員 tooeffectively 管理訂用帳戶，請參閱[Azure 企業版 scaffold-精準的訂閱控管](resource-manager-subscription-governance.md)。

