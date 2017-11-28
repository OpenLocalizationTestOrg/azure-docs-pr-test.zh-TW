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
# <a name="assign-and-manage-resource-policies"></a><span data-ttu-id="59474-103">指派和管理資源原則</span><span class="sxs-lookup"><span data-stu-id="59474-103">Assign and manage resource policies</span></span>

<span data-ttu-id="59474-104">tooimplement 原則，您必須執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="59474-104">tooimplement a policy, you must perform these steps:</span></span>

1. <span data-ttu-id="59474-105">如果您的需求，可滿足您訂用帳戶中已經存在，請檢查原則 （包括 Azure 所提供的內建原則） 定義 toosee。</span><span class="sxs-lookup"><span data-stu-id="59474-105">Check policy definitions (including built-in policies provided by Azure) toosee if one already exists in your subscription that fulfills your requirements.</span></span>
2. <span data-ttu-id="59474-106">如果存在，請記下它的名稱。</span><span class="sxs-lookup"><span data-stu-id="59474-106">If one exists, get its name.</span></span>
3. <span data-ttu-id="59474-107">如果不存在的話，定義使用 JSON，hello 原則規則，並將它新增為您的訂用帳戶中的原則定義。</span><span class="sxs-lookup"><span data-stu-id="59474-107">If one does not exist, define hello policy rule with JSON, and add it as a policy definition in your subscription.</span></span> <span data-ttu-id="59474-108">這個步驟會讓 hello 原則可供指派，但不會套用 hello 規則 tooyour 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="59474-108">This step makes hello policy available for assignment but does not apply hello rules tooyour subscription.</span></span>
4. <span data-ttu-id="59474-109">對於任一種情況下，指派 hello 原則 tooa 範圍 （例如訂用帳戶或資源群組）。</span><span class="sxs-lookup"><span data-stu-id="59474-109">For either case, assign hello policy tooa scope (such as a subscription or resource group).</span></span> <span data-ttu-id="59474-110">hello 原則的 hello 規則現在會強制執行。</span><span class="sxs-lookup"><span data-stu-id="59474-110">hello rules of hello policy are now enforced.</span></span>

<span data-ttu-id="59474-111">本文著重於 hello 步驟 toocreate 原則定義，並指派透過 REST API、 PowerShell 或 Azure CLI 該定義 tooa 範圍。</span><span class="sxs-lookup"><span data-stu-id="59474-111">This article focuses on hello steps toocreate a policy definition and assign that definition tooa scope through REST API, PowerShell, or Azure CLI.</span></span> <span data-ttu-id="59474-112">如果您偏好 toouse hello 入口 tooassign 原則，請參閱[使用 Azure 入口網站 tooassign 和管理資源原則](resource-manager-policy-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="59474-112">If you prefer toouse hello portal tooassign policies, see [Use Azure portal tooassign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="59474-113">這篇文章不會著重在 hello 語法建立 hello 原則定義。</span><span class="sxs-lookup"><span data-stu-id="59474-113">This article does not focus on hello syntax for creating hello policy definition.</span></span> <span data-ttu-id="59474-114">如需原則語法的詳細資訊，請參閱[資源原則概觀](resource-manager-policy.md)。</span><span class="sxs-lookup"><span data-stu-id="59474-114">For information about policy syntax, see [Resource policy overview](resource-manager-policy.md).</span></span>

## <a name="rest-api"></a><span data-ttu-id="59474-115">REST API</span><span class="sxs-lookup"><span data-stu-id="59474-115">REST API</span></span>

### <a name="create-policy-definition"></a><span data-ttu-id="59474-116">建立原則定義</span><span class="sxs-lookup"><span data-stu-id="59474-116">Create policy definition</span></span>

<span data-ttu-id="59474-117">您可以建立原則，以 hello [REST API 的原則定義](/rest/api/resources/policydefinitions)。</span><span class="sxs-lookup"><span data-stu-id="59474-117">You can create a policy with hello [REST API for Policy Definitions](/rest/api/resources/policydefinitions).</span></span> <span data-ttu-id="59474-118">hello REST API 可讓您 toocreate 和刪除原則定義，以及取得現有的定義相關資訊。</span><span class="sxs-lookup"><span data-stu-id="59474-118">hello REST API enables you toocreate and delete policy definitions, and get information about existing definitions.</span></span>

<span data-ttu-id="59474-119">toocreate 的原則定義，執行：</span><span class="sxs-lookup"><span data-stu-id="59474-119">toocreate a policy definition, run:</span></span>

```HTTP
PUT https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.authorization/policydefinitions/{policyDefinitionName}?api-version={api-version}
```

<span data-ttu-id="59474-120">包括下列範例要求的主體類似 toohello:</span><span class="sxs-lookup"><span data-stu-id="59474-120">Include a request body similar toohello following example:</span></span>

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

### <a name="assign-policy"></a><span data-ttu-id="59474-121">指派原則</span><span class="sxs-lookup"><span data-stu-id="59474-121">Assign policy</span></span>

<span data-ttu-id="59474-122">您可以套用 hello 原則定義在透過 hello hello 預期範圍[REST API 的原則指派](/rest/api/resources/policyassignments)。</span><span class="sxs-lookup"><span data-stu-id="59474-122">You can apply hello policy definition at hello desired scope through hello [REST API for policy assignments](/rest/api/resources/policyassignments).</span></span> <span data-ttu-id="59474-123">hello REST API 可讓您 toocreate 和刪除原則指派，以及取得現有指派的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="59474-123">hello REST API enables you toocreate and delete policy assignments, and get information about existing assignments.</span></span>

<span data-ttu-id="59474-124">toocreate 原則指派中，執行：</span><span class="sxs-lookup"><span data-stu-id="59474-124">toocreate a policy assignment, run:</span></span>

```HTTP
PUT https://management.azure.com /subscriptions/{subscription-id}/providers/Microsoft.authorization/policyassignments/{policyAssignmentName}?api-version={api-version}
```

<span data-ttu-id="59474-125">hello {原則指派} 是 hello hello 原則指派名稱。</span><span class="sxs-lookup"><span data-stu-id="59474-125">hello {policy-assignment} is hello name of hello policy assignment.</span></span>

<span data-ttu-id="59474-126">包括下列範例要求的主體類似 toohello:</span><span class="sxs-lookup"><span data-stu-id="59474-126">Include a request body similar toohello following example:</span></span>

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

### <a name="view-policy"></a><span data-ttu-id="59474-127">檢視原則</span><span class="sxs-lookup"><span data-stu-id="59474-127">View policy</span></span>
<span data-ttu-id="59474-128">tooget 原則，使用 hello[取得原則定義](https://docs.microsoft.com/rest/api/resources/policydefinitions#PolicyDefinitions_Get)作業。</span><span class="sxs-lookup"><span data-stu-id="59474-128">tooget a policy, use hello [Get policy definition](https://docs.microsoft.com/rest/api/resources/policydefinitions#PolicyDefinitions_Get) operation.</span></span>

### <a name="get-aliases"></a><span data-ttu-id="59474-129">取得別名</span><span class="sxs-lookup"><span data-stu-id="59474-129">Get aliases</span></span>
<span data-ttu-id="59474-130">您可以擷取透過 hello REST API 的別名：</span><span class="sxs-lookup"><span data-stu-id="59474-130">You can retrieve aliases through hello REST API:</span></span>

```HTTP
GET /subscriptions/{id}/providers?$expand=resourceTypes/aliases&api-version=2015-11-01
```

<span data-ttu-id="59474-131">下列範例中的 hello 顯示別名的定義。</span><span class="sxs-lookup"><span data-stu-id="59474-131">hello following example shows a definition of an alias.</span></span> <span data-ttu-id="59474-132">如您所見，別名在不同 API 版本中均會定義路徑，無論屬性名稱是否變更。</span><span class="sxs-lookup"><span data-stu-id="59474-132">As you can see, an alias defines paths in different API versions, even when there is a property name change.</span></span> 

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

## <a name="powershell"></a><span data-ttu-id="59474-133">PowerShell</span><span class="sxs-lookup"><span data-stu-id="59474-133">PowerShell</span></span>

<span data-ttu-id="59474-134">Hello PowerShell 範例之前，請確定您有[安裝最新版的 hello](/powershell/azure/install-azurerm-ps)的 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="59474-134">Before proceeding with hello PowerShell examples, make sure you have [installed hello latest version](/powershell/azure/install-azurerm-ps) of Azure PowerShell.</span></span> <span data-ttu-id="59474-135">原則參數是於 3.6.0 版中加入。</span><span class="sxs-lookup"><span data-stu-id="59474-135">Policy parameters were added in version 3.6.0.</span></span> <span data-ttu-id="59474-136">如果您有較早版本，hello 範例會傳回找不到的錯誤指出 hello 參數。</span><span class="sxs-lookup"><span data-stu-id="59474-136">If you have an earlier version, hello examples return an error indicating hello parameter cannot be found.</span></span>

### <a name="view-policy-definitions"></a><span data-ttu-id="59474-137">檢視原則定義</span><span class="sxs-lookup"><span data-stu-id="59474-137">View policy definitions</span></span>
<span data-ttu-id="59474-138">toosee 所有的原則定義，在您的訂用帳戶中，而使用 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="59474-138">toosee all policy definitions in your subscription, use hello following command:</span></span>

```powershell
Get-AzureRmPolicyDefinition
```

<span data-ttu-id="59474-139">它會傳回所有可用的原則定義，包括內建原則。</span><span class="sxs-lookup"><span data-stu-id="59474-139">It returns all available policy definitions, including built-in policies.</span></span> <span data-ttu-id="59474-140">每個原則就會傳回在 hello 下列格式：</span><span class="sxs-lookup"><span data-stu-id="59474-140">Each policy is returned in hello following format:</span></span>

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

<span data-ttu-id="59474-141">在之前繼續 toocreate 原則定義，看看 hello 內建原則。</span><span class="sxs-lookup"><span data-stu-id="59474-141">Before proceeding toocreate a policy definition, look at hello built-in policies.</span></span> <span data-ttu-id="59474-142">如果您發現套用 hello 限制您需要的內建原則，您可以略過建立的原則定義。</span><span class="sxs-lookup"><span data-stu-id="59474-142">If you find a built-in policy that applies hello limits you need, you can skip creating a policy definition.</span></span> <span data-ttu-id="59474-143">相反地，指派 hello 內建原則 toohello 預期範圍。</span><span class="sxs-lookup"><span data-stu-id="59474-143">Instead, assign hello built-in policy toohello desired scope.</span></span>

### <a name="create-policy-definition"></a><span data-ttu-id="59474-144">建立原則定義</span><span class="sxs-lookup"><span data-stu-id="59474-144">Create policy definition</span></span>
<span data-ttu-id="59474-145">您可以建立使用 hello 的原則定義`New-AzureRmPolicyDefinition`cmdlet。</span><span class="sxs-lookup"><span data-stu-id="59474-145">You can create a policy definition using hello `New-AzureRmPolicyDefinition` cmdlet.</span></span>

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

<span data-ttu-id="59474-146">hello 輸出會儲存在`$definition`原則指派期間使用的物件。</span><span class="sxs-lookup"><span data-stu-id="59474-146">hello output is stored in a `$definition` object, which is used during policy assignment.</span></span> 

<span data-ttu-id="59474-147">而不要指定 hello JSON 做為參數，您可以提供包含 hello 原則規則的 hello 路徑 tooa.json 檔案。</span><span class="sxs-lookup"><span data-stu-id="59474-147">Rather than specifying hello JSON as a parameter, you can provide hello path tooa .json file containing hello policy rule.</span></span>

```powershell
$definition = New-AzureRmPolicyDefinition -Name coolAccessTier -Description "Policy toospecify access tier." -Policy "c:\policies\coolAccessTier.json"
```

<span data-ttu-id="59474-148">hello 下列範例會建立包含參數的原則定義：</span><span class="sxs-lookup"><span data-stu-id="59474-148">hello following example creates a policy definition that includes parameters:</span></span>

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

### <a name="assign-policy"></a><span data-ttu-id="59474-149">指派原則</span><span class="sxs-lookup"><span data-stu-id="59474-149">Assign policy</span></span>

<span data-ttu-id="59474-150">使用 hello 套用在所需的 hello 範圍 hello 原則`New-AzureRmPolicyAssignment`cmdlet。</span><span class="sxs-lookup"><span data-stu-id="59474-150">You apply hello policy at hello desired scope by using hello `New-AzureRmPolicyAssignment` cmdlet.</span></span> <span data-ttu-id="59474-151">下列範例中的 hello 指派 hello 原則 tooa 資源群組。</span><span class="sxs-lookup"><span data-stu-id="59474-151">hello following example assigns hello policy tooa resource group.</span></span>

```powershell
$rg = Get-AzureRmResourceGroup -Name "ExampleGroup"
New-AzureRMPolicyAssignment -Name accessTierAssignment -Scope $rg.ResourceId -PolicyDefinition $definition
```

<span data-ttu-id="59474-152">tooassign 原則，要求參數，建立並使用這些值的物件。</span><span class="sxs-lookup"><span data-stu-id="59474-152">tooassign a policy that requires parameters, create and object with those values.</span></span> <span data-ttu-id="59474-153">hello 下列範例會擷取內建原則，並傳遞參數值：</span><span class="sxs-lookup"><span data-stu-id="59474-153">hello following example retrieves a built-in policy and passes in parameters values:</span></span>

```powershell
$rg = Get-AzureRmResourceGroup -Name "ExampleGroup"
$definition = Get-AzureRmPolicyDefinition -Id /providers/Microsoft.Authorization/policyDefinitions/e5662a6-4747-49cd-b67b-bf8b01975c4c
$array = @("West US", "West US 2")
$param = @{"listOfAllowedLocations"=$array}
New-AzureRMPolicyAssignment -Name locationAssignment -Scope $rg.ResourceId -PolicyDefinition $definition -PolicyParameterObject $param
```

### <a name="view-policy-assignment"></a><span data-ttu-id="59474-154">檢視原則指派</span><span class="sxs-lookup"><span data-stu-id="59474-154">View policy assignment</span></span>

<span data-ttu-id="59474-155">tooget 特定的原則指派，使用：</span><span class="sxs-lookup"><span data-stu-id="59474-155">tooget a specific policy assignment, use:</span></span>

```powershell
$rg = Get-AzureRmResourceGroup -Name "ExampleGroup"
(Get-AzureRmPolicyAssignment -Name accessTierAssignment -Scope $rg.ResourceId
```

<span data-ttu-id="59474-156">tooview hello 原則定義，請使用的原則規則：</span><span class="sxs-lookup"><span data-stu-id="59474-156">tooview hello policy rule for a policy definition, use:</span></span>

```powershell
(Get-AzureRmPolicyDefinition -Name coolAccessTier).Properties.policyRule | ConvertTo-Json
```

### <a name="remove-policy-assignment"></a><span data-ttu-id="59474-157">移除原則指派</span><span class="sxs-lookup"><span data-stu-id="59474-157">Remove policy assignment</span></span> 

<span data-ttu-id="59474-158">tooremove 原則指派，使用：</span><span class="sxs-lookup"><span data-stu-id="59474-158">tooremove a policy assignment, use:</span></span>

```powershell
Remove-AzureRmPolicyAssignment -Name regionPolicyAssignment -Scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

## <a name="azure-cli"></a><span data-ttu-id="59474-159">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="59474-159">Azure CLI</span></span>

### <a name="view-policy-definitions"></a><span data-ttu-id="59474-160">檢視原則定義</span><span class="sxs-lookup"><span data-stu-id="59474-160">View policy definitions</span></span>
<span data-ttu-id="59474-161">toosee 所有的原則定義，在您的訂用帳戶中，而使用 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="59474-161">toosee all policy definitions in your subscription, use hello following command:</span></span>

```azurecli
az policy definition list
```

<span data-ttu-id="59474-162">它會傳回所有可用的原則定義，包括內建原則。</span><span class="sxs-lookup"><span data-stu-id="59474-162">It returns all available policy definitions, including built-in policies.</span></span> <span data-ttu-id="59474-163">每個原則就會傳回在 hello 下列格式：</span><span class="sxs-lookup"><span data-stu-id="59474-163">Each policy is returned in hello following format:</span></span>

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

<span data-ttu-id="59474-164">在之前繼續 toocreate 原則定義，看看 hello 內建原則。</span><span class="sxs-lookup"><span data-stu-id="59474-164">Before proceeding toocreate a policy definition, look at hello built-in policies.</span></span> <span data-ttu-id="59474-165">如果您發現套用 hello 限制您需要的內建原則，您可以略過建立的原則定義。</span><span class="sxs-lookup"><span data-stu-id="59474-165">If you find a built-in policy that applies hello limits you need, you can skip creating a policy definition.</span></span> <span data-ttu-id="59474-166">相反地，指派 hello 內建原則 toohello 預期範圍。</span><span class="sxs-lookup"><span data-stu-id="59474-166">Instead, assign hello built-in policy toohello desired scope.</span></span>

### <a name="create-policy-definition"></a><span data-ttu-id="59474-167">建立原則定義</span><span class="sxs-lookup"><span data-stu-id="59474-167">Create policy definition</span></span>

<span data-ttu-id="59474-168">您可以建立使用 Azure CLI hello 原則定義命令的原則定義。</span><span class="sxs-lookup"><span data-stu-id="59474-168">You can create a policy definition using Azure CLI with hello policy definition command.</span></span>

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

### <a name="assign-policy"></a><span data-ttu-id="59474-169">指派原則</span><span class="sxs-lookup"><span data-stu-id="59474-169">Assign policy</span></span>

<span data-ttu-id="59474-170">您可以使用 hello 原則指派命令套用 hello 原則 toohello 預期範圍。</span><span class="sxs-lookup"><span data-stu-id="59474-170">You can apply hello policy toohello desired scope by using hello policy assignment command.</span></span> <span data-ttu-id="59474-171">下列範例中的 hello 指派原則 tooa 資源群組。</span><span class="sxs-lookup"><span data-stu-id="59474-171">hello following example assigns a policy tooa resource group.</span></span>

```azurecli
az policy assignment create --name coolAccessTierAssignment --policy coolAccessTier --scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

### <a name="view-policy-assignment"></a><span data-ttu-id="59474-172">檢視原則指派</span><span class="sxs-lookup"><span data-stu-id="59474-172">View policy assignment</span></span>

<span data-ttu-id="59474-173">tooview 原則指派，提供 hello 原則指派名稱及 hello 範圍：</span><span class="sxs-lookup"><span data-stu-id="59474-173">tooview a policy assignment, provide hello policy assignment name and hello scope:</span></span>

```azurecli
az policy assignment show --name coolAccessTierAssignment --scope "/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}"
```

### <a name="remove-policy-assignment"></a><span data-ttu-id="59474-174">移除原則指派</span><span class="sxs-lookup"><span data-stu-id="59474-174">Remove policy assignment</span></span> 

<span data-ttu-id="59474-175">tooremove 原則指派，使用：</span><span class="sxs-lookup"><span data-stu-id="59474-175">tooremove a policy assignment, use:</span></span>

```azurecli
az policy assignment delete --name coolAccessTier --scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

## <a name="next-steps"></a><span data-ttu-id="59474-176">後續步驟</span><span class="sxs-lookup"><span data-stu-id="59474-176">Next steps</span></span>
* <span data-ttu-id="59474-177">如需指引企業可以如何使用資源管理員 tooeffectively 管理訂用帳戶，請參閱[Azure 企業版 scaffold-精準的訂閱控管](resource-manager-subscription-governance.md)。</span><span class="sxs-lookup"><span data-stu-id="59474-177">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

