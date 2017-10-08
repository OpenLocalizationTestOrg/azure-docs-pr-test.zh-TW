---
title: "aaaAssign 和管理 Azure 資源原則 |Microsoft 文件"
description: "描述如何 tooapply Azure 資源原則 toosubscriptions 和資源群組，以及如何 tooview 資源原則。"
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/26/2017
ms.author: tomfitz
ms.openlocfilehash: b6999b43bbcc80d2fde9911352fd4352fa453443
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="assign-and-manage-resource-policies"></a>指派和管理資源原則

tooimplement 原則，您必須執行下列步驟：

1. 如果您的需求，可滿足您訂用帳戶中已經存在，請檢查原則 （包括 Azure 所提供的內建原則） 定義 toosee。
2. 如果存在，請記下它的名稱。
3. 如果不存在的話，定義使用 JSON，hello 原則規則，並將它新增為您的訂用帳戶中的原則定義。 這個步驟會讓 hello 原則可供指派，但不會套用 hello 規則 tooyour 訂用帳戶。
4. 對於任一種情況下，指派 hello 原則 tooa 範圍 （例如訂用帳戶或資源群組）。 hello 原則的 hello 規則現在會強制執行。

本文著重於 hello 步驟 toocreate 原則定義，並指派透過 REST API、 PowerShell 或 Azure CLI 該定義 tooa 範圍。 如果您偏好 toouse hello 入口 tooassign 原則，請參閱[使用 Azure 入口網站 tooassign 和管理資源原則](resource-manager-policy-portal.md)。 這篇文章不會著重在 hello 語法建立 hello 原則定義。 如需原則語法的詳細資訊，請參閱[資源原則概觀](resource-manager-policy.md)。

## <a name="rest-api"></a>REST API

### <a name="create-policy-definition"></a>建立原則定義

您可以建立原則，以 hello [REST API 的原則定義](/rest/api/resources/policydefinitions)。 hello REST API 可讓您 toocreate 和刪除原則定義，以及取得現有的定義相關資訊。

toocreate 的原則定義，執行：

```HTTP
PUT https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.authorization/policydefinitions/{policyDefinitionName}?api-version={api-version}
```

包括下列範例要求的主體類似 toohello:

```json
{
  "properties": {
    "parameters": {
      "allowedLocations": {
        "type": "array",
        "metadata": {
          "description": "hello list of locations that can be specified when deploying resources",
          "strongType": "location",
          "displayName": "Allowed locations"
        }
      }
    },
    "displayName": "Allowed locations",
    "description": "This policy enables you toorestrict hello locations your organization can specify when deploying resources.",
    "policyRule": {
      "if": {
        "not": {
          "field": "location",
          "in": "[parameters('allowedLocations')]"
        }
      },
      "then": {
        "effect": "deny"
      }
    }
  }
}
```

### <a name="assign-policy"></a>指派原則

您可以套用 hello 原則定義在透過 hello hello 預期範圍[REST API 的原則指派](/rest/api/resources/policyassignments)。 hello REST API 可讓您 toocreate 和刪除原則指派，以及取得現有指派的相關資訊。

toocreate 原則指派中，執行：

```HTTP
PUT https://management.azure.com /subscriptions/{subscription-id}/providers/Microsoft.authorization/policyassignments/{policyAssignmentName}?api-version={api-version}
```

hello {原則指派} 是 hello hello 原則指派名稱。

包括下列範例要求的主體類似 toohello:

```json
{
  "properties":{
    "displayName":"West US only policy assignment on hello subscription ",
    "description":"Resources can only be provisioned in West US regions",
    "parameters": {
      "allowedLocations": { "value": ["northeurope", "westus"] }
     },
    "policyDefinitionId":"/subscriptions/{subscription-id}/providers/Microsoft.Authorization/policyDefinitions/{definition-name}",
      "scope":"/subscriptions/{subscription-id}"
  },
}
```

### <a name="view-policy"></a>檢視原則
tooget 原則，使用 hello[取得原則定義](https://docs.microsoft.com/rest/api/resources/policydefinitions#PolicyDefinitions_Get)作業。

### <a name="get-aliases"></a>取得別名
您可以擷取透過 hello REST API 的別名：

```HTTP
GET /subscriptions/{id}/providers?$expand=resourceTypes/aliases&api-version=2015-11-01
```

下列範例中的 hello 顯示別名的定義。 如您所見，別名在不同 API 版本中均會定義路徑，無論屬性名稱是否變更。 

```json
"aliases": [
    {
      "name": "Microsoft.Storage/storageAccounts/sku.name",
      "paths": [
        {
          "path": "properties.accountType",
          "apiVersions": [
            "2015-06-15",
            "2015-05-01-preview"
          ]
        },
        {
          "path": "sku.name",
          "apiVersions": [
            "2016-01-01"
          ]
        }
      ]
    }
]
```

## <a name="powershell"></a>PowerShell

Hello PowerShell 範例之前，請確定您有[安裝最新版的 hello](/powershell/azure/install-azurerm-ps)的 Azure PowerShell。 原則參數是於 3.6.0 版中加入。 如果您有較早版本，hello 範例會傳回找不到的錯誤指出 hello 參數。

### <a name="view-policy-definitions"></a>檢視原則定義
toosee 所有的原則定義，在您的訂用帳戶中，而使用 hello 下列命令：

```powershell
Get-AzureRmPolicyDefinition
```

它會傳回所有可用的原則定義，包括內建原則。 每個原則就會傳回在 hello 下列格式：

```powershell
Name               : e56962a6-4747-49cd-b67b-bf8b01975c4c
ResourceId         : /providers/Microsoft.Authorization/policyDefinitions/e56962a6-4747-49cd-b67b-bf8b01975c4c
ResourceName       : e56962a6-4747-49cd-b67b-bf8b01975c4c
ResourceType       : Microsoft.Authorization/policyDefinitions
Properties         : @{displayName=Allowed locations; policyType=BuiltIn; description=This policy enables you to
                     restrict hello locations your organization can specify when deploying resources. Use tooenforce
                     your geo-compliance requirements.; parameters=; policyRule=}
PolicyDefinitionId : /providers/Microsoft.Authorization/policyDefinitions/e56962a6-4747-49cd-b67b-bf8b01975c4c
```

在之前繼續 toocreate 原則定義，看看 hello 內建原則。 如果您發現套用 hello 限制您需要的內建原則，您可以略過建立的原則定義。 相反地，指派 hello 內建原則 toohello 預期範圍。

### <a name="create-policy-definition"></a>建立原則定義
您可以建立使用 hello 的原則定義`New-AzureRmPolicyDefinition`cmdlet。

```powershell
$definition = New-AzureRmPolicyDefinition -Name coolAccessTier -Description "Policy toospecify access tier." -Policy '{
  "if": {
    "allOf": [
      {
        "field": "type",
        "equals": "Microsoft.Storage/storageAccounts"
      },
      {
        "field": "kind",
        "equals": "BlobStorage"
      },
      {
        "not": {
          "field": "Microsoft.Storage/storageAccounts/accessTier",
          "equals": "cool"
        }
      }
    ]
  },
  "then": {
    "effect": "deny"
  }
}'
```            

hello 輸出會儲存在`$definition`原則指派期間使用的物件。 

而不要指定 hello JSON 做為參數，您可以提供包含 hello 原則規則的 hello 路徑 tooa.json 檔案。

```powershell
$definition = New-AzureRmPolicyDefinition -Name coolAccessTier -Description "Policy toospecify access tier." -Policy "c:\policies\coolAccessTier.json"
```

hello 下列範例會建立包含參數的原則定義：

```powershell
$policy = '{
    "if": {
        "allOf": [
            {
                "field": "type",
                "equals": "Microsoft.Storage/storageAccounts"
            },
            {
                "not": {
                    "field": "location",
                    "in": "[parameters(''allowedLocations'')]"
                }
            }
        ]
    },
    "then": {
        "effect": "Deny"
    }
}'

$parameters = '{
    "allowedLocations": {
        "type": "array",
        "metadata": {
          "description": "hello list of locations that can be specified when deploying storage accounts.",
          "strongType": "location",
          "displayName": "Allowed locations"
        }
    }
}' 

$definition = New-AzureRmPolicyDefinition -Name storageLocations -Description "Policy toospecify locations for storage accounts." -Policy $policy -Parameter $parameters 
```

### <a name="assign-policy"></a>指派原則

使用 hello 套用在所需的 hello 範圍 hello 原則`New-AzureRmPolicyAssignment`cmdlet。 下列範例中的 hello 指派 hello 原則 tooa 資源群組。

```powershell
$rg = Get-AzureRmResourceGroup -Name "ExampleGroup"
New-AzureRMPolicyAssignment -Name accessTierAssignment -Scope $rg.ResourceId -PolicyDefinition $definition
```

tooassign 原則，要求參數，建立並使用這些值的物件。 hello 下列範例會擷取內建原則，並傳遞參數值：

```powershell
$rg = Get-AzureRmResourceGroup -Name "ExampleGroup"
$definition = Get-AzureRmPolicyDefinition -Id /providers/Microsoft.Authorization/policyDefinitions/e5662a6-4747-49cd-b67b-bf8b01975c4c
$array = @("West US", "West US 2")
$param = @{"listOfAllowedLocations"=$array}
New-AzureRMPolicyAssignment -Name locationAssignment -Scope $rg.ResourceId -PolicyDefinition $definition -PolicyParameterObject $param
```

### <a name="view-policy-assignment"></a>檢視原則指派

tooget 特定的原則指派，使用：

```powershell
$rg = Get-AzureRmResourceGroup -Name "ExampleGroup"
(Get-AzureRmPolicyAssignment -Name accessTierAssignment -Scope $rg.ResourceId
```

tooview hello 原則定義，請使用的原則規則：

```powershell
(Get-AzureRmPolicyDefinition -Name coolAccessTier).Properties.policyRule | ConvertTo-Json
```

### <a name="remove-policy-assignment"></a>移除原則指派 

tooremove 原則指派，使用：

```powershell
Remove-AzureRmPolicyAssignment -Name regionPolicyAssignment -Scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

## <a name="azure-cli"></a>Azure CLI

### <a name="view-policy-definitions"></a>檢視原則定義
toosee 所有的原則定義，在您的訂用帳戶中，而使用 hello 下列命令：

```azurecli
az policy definition list
```

它會傳回所有可用的原則定義，包括內建原則。 每個原則就會傳回在 hello 下列格式：

```azurecli
{                                                            
  "description": "This policy enables you toorestrict hello locations your organization can specify when deploying resources. Use tooenforce your geo-compliance requirements.",                      
  "displayName": "Allowed locations",
  "id": "/providers/Microsoft.Authorization/policyDefinitions/e56962a6-4747-49cd-b67b-bf8b01975c4c",
  "name": "e56962a6-4747-49cd-b67b-bf8b01975c4c",
  "policyRule": {
    "if": {
      "not": {
        "field": "location",
        "in": "[parameters('listOfAllowedLocations')]"
      }
    },
    "then": {
      "effect": "Deny"
    }
  },
  "policyType": "BuiltIn"
}
```

在之前繼續 toocreate 原則定義，看看 hello 內建原則。 如果您發現套用 hello 限制您需要的內建原則，您可以略過建立的原則定義。 相反地，指派 hello 內建原則 toohello 預期範圍。

### <a name="create-policy-definition"></a>建立原則定義

您可以建立使用 Azure CLI hello 原則定義命令的原則定義。

```azurecli
az policy definition create --name coolAccessTier --description "Policy toospecify access tier." --rules '{
  "if": {
    "allOf": [
      {
        "field": "type",
        "equals": "Microsoft.Storage/storageAccounts"
      },
      {
        "field": "kind",
        "equals": "BlobStorage"
      },
      {
        "not": {
          "field": "Microsoft.Storage/storageAccounts/accessTier",
          "equals": "cool"
        }
      }
    ]
  },
  "then": {
    "effect": "deny"
  }
}'    
```

### <a name="assign-policy"></a>指派原則

您可以使用 hello 原則指派命令套用 hello 原則 toohello 預期範圍。 下列範例中的 hello 指派原則 tooa 資源群組。

```azurecli
az policy assignment create --name coolAccessTierAssignment --policy coolAccessTier --scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

### <a name="view-policy-assignment"></a>檢視原則指派

tooview 原則指派，提供 hello 原則指派名稱及 hello 範圍：

```azurecli
az policy assignment show --name coolAccessTierAssignment --scope "/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}"
```

### <a name="remove-policy-assignment"></a>移除原則指派 

tooremove 原則指派，使用：

```azurecli
az policy assignment delete --name coolAccessTier --scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

## <a name="next-steps"></a>後續步驟
* 如需指引企業可以如何使用資源管理員 tooeffectively 管理訂用帳戶，請參閱[Azure 企業版 scaffold-精準的訂閱控管](resource-manager-subscription-governance.md)。

