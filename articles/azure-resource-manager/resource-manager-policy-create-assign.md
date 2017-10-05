---
title: "指派和管理 Azure 資源原則 | Microsoft Docs"
description: "描述如何將 Azure 資源原則套用至訂用帳戶和資源群組，以及如何檢視資源原則。"
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
ms.openlocfilehash: b204cffa8fab0ad27a9f78a81c04f0a0225d95f5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="assign-and-manage-resource-policies"></a><span data-ttu-id="015ed-103">指派和管理資源原則</span><span class="sxs-lookup"><span data-stu-id="015ed-103">Assign and manage resource policies</span></span>

<span data-ttu-id="015ed-104">若要實作原則，您必須執行這些步驟︰</span><span class="sxs-lookup"><span data-stu-id="015ed-104">To implement a policy, you must perform these steps:</span></span>

1. <span data-ttu-id="015ed-105">檢查原則定義 (包含 Azure 提供的內建原則)，以查看您的訂用帳戶中是否已存在符合您需求的定義。</span><span class="sxs-lookup"><span data-stu-id="015ed-105">Check policy definitions (including built-in policies provided by Azure) to see if one already exists in your subscription that fulfills your requirements.</span></span>
2. <span data-ttu-id="015ed-106">如果存在，請記下它的名稱。</span><span class="sxs-lookup"><span data-stu-id="015ed-106">If one exists, get its name.</span></span>
3. <span data-ttu-id="015ed-107">如果不存在，請使用 JSON 定義原則規則，並將它新增為訂用帳戶中的原則定義。</span><span class="sxs-lookup"><span data-stu-id="015ed-107">If one does not exist, define the policy rule with JSON, and add it as a policy definition in your subscription.</span></span> <span data-ttu-id="015ed-108">這個步驟會使原則可供指派，但不會將規則套用至您的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="015ed-108">This step makes the policy available for assignment but does not apply the rules to your subscription.</span></span>
4. <span data-ttu-id="015ed-109">不論存在與否，請將原則指派給範圍 (例如訂用帳戶或資源群組)。</span><span class="sxs-lookup"><span data-stu-id="015ed-109">For either case, assign the policy to a scope (such as a subscription or resource group).</span></span> <span data-ttu-id="015ed-110">現在會強制執行原則的規則。</span><span class="sxs-lookup"><span data-stu-id="015ed-110">The rules of the policy are now enforced.</span></span>

<span data-ttu-id="015ed-111">本文著重於建立原則定義，然後透過 REST API、PowerShell 或 Azure CLI 將該定義指派至範圍的步驟。</span><span class="sxs-lookup"><span data-stu-id="015ed-111">This article focuses on the steps to create a policy definition and assign that definition to a scope through REST API, PowerShell, or Azure CLI.</span></span> <span data-ttu-id="015ed-112">如果您想要使用入口網站來指派原則，請參閱[使用 Azure 入口網站來指派和管理資源原則](resource-manager-policy-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="015ed-112">If you prefer to use the portal to assign policies, see [Use Azure portal to assign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="015ed-113">本文並不會著重於建立原則定義的語法。</span><span class="sxs-lookup"><span data-stu-id="015ed-113">This article does not focus on the syntax for creating the policy definition.</span></span> <span data-ttu-id="015ed-114">如需原則語法的詳細資訊，請參閱[資源原則概觀](resource-manager-policy.md)。</span><span class="sxs-lookup"><span data-stu-id="015ed-114">For information about policy syntax, see [Resource policy overview](resource-manager-policy.md).</span></span>

## <a name="rest-api"></a><span data-ttu-id="015ed-115">REST API</span><span class="sxs-lookup"><span data-stu-id="015ed-115">REST API</span></span>

### <a name="create-policy-definition"></a><span data-ttu-id="015ed-116">建立原則定義</span><span class="sxs-lookup"><span data-stu-id="015ed-116">Create policy definition</span></span>

<span data-ttu-id="015ed-117">您可以使用 [適用於原則定義的 REST API](/rest/api/resources/policydefinitions)來建立原則。</span><span class="sxs-lookup"><span data-stu-id="015ed-117">You can create a policy with the [REST API for Policy Definitions](/rest/api/resources/policydefinitions).</span></span> <span data-ttu-id="015ed-118">REST API 可讓您建立和刪除原則定義，以及取得現有定義的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="015ed-118">The REST API enables you to create and delete policy definitions, and get information about existing definitions.</span></span>

<span data-ttu-id="015ed-119">若要建立原則定義，請執行︰</span><span class="sxs-lookup"><span data-stu-id="015ed-119">To create a policy definition, run:</span></span>

```HTTP
PUT https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.authorization/policydefinitions/{policyDefinitionName}?api-version={api-version}
```

<span data-ttu-id="015ed-120">納入如下範例的要求內文：</span><span class="sxs-lookup"><span data-stu-id="015ed-120">Include a request body similar to the following example:</span></span>

```json
{
  "properties": {
    "parameters": {
      "allowedLocations": {
        "type": "array",
        "metadata": {
          "description": "The list of locations that can be specified when deploying resources",
          "strongType": "location",
          "displayName": "Allowed locations"
        }
      }
    },
    "displayName": "Allowed locations",
    "description": "This policy enables you to restrict the locations your organization can specify when deploying resources.",
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

### <a name="assign-policy"></a><span data-ttu-id="015ed-121">指派原則</span><span class="sxs-lookup"><span data-stu-id="015ed-121">Assign policy</span></span>

<span data-ttu-id="015ed-122">您可以透過 [適用於原則指派的 REST API](/rest/api/resources/policyassignments)，在所需範圍內套用原則定義。</span><span class="sxs-lookup"><span data-stu-id="015ed-122">You can apply the policy definition at the desired scope through the [REST API for policy assignments](/rest/api/resources/policyassignments).</span></span> <span data-ttu-id="015ed-123">REST API 可讓您建立和刪除原則指派，以及取得現有指派的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="015ed-123">The REST API enables you to create and delete policy assignments, and get information about existing assignments.</span></span>

<span data-ttu-id="015ed-124">若要建立原則指派，請執行：</span><span class="sxs-lookup"><span data-stu-id="015ed-124">To create a policy assignment, run:</span></span>

```HTTP
PUT https://management.azure.com /subscriptions/{subscription-id}/providers/Microsoft.authorization/policyassignments/{policyAssignmentName}?api-version={api-version}
```

<span data-ttu-id="015ed-125">{policy-assignment} 是原則指派的名稱。</span><span class="sxs-lookup"><span data-stu-id="015ed-125">The {policy-assignment} is the name of the policy assignment.</span></span>

<span data-ttu-id="015ed-126">納入如下範例的要求內文：</span><span class="sxs-lookup"><span data-stu-id="015ed-126">Include a request body similar to the following example:</span></span>

```json
{
  "properties":{
    "displayName":"West US only policy assignment on the subscription ",
    "description":"Resources can only be provisioned in West US regions",
    "parameters": {
      "allowedLocations": { "value": ["northeurope", "westus"] }
     },
    "policyDefinitionId":"/subscriptions/{subscription-id}/providers/Microsoft.Authorization/policyDefinitions/{definition-name}",
      "scope":"/subscriptions/{subscription-id}"
  },
}
```

### <a name="view-policy"></a><span data-ttu-id="015ed-127">檢視原則</span><span class="sxs-lookup"><span data-stu-id="015ed-127">View policy</span></span>
<span data-ttu-id="015ed-128">若要取得原則，請使用[取得原則定義](https://docs.microsoft.com/rest/api/resources/policydefinitions#PolicyDefinitions_Get)作業。</span><span class="sxs-lookup"><span data-stu-id="015ed-128">To get a policy, use the [Get policy definition](https://docs.microsoft.com/rest/api/resources/policydefinitions#PolicyDefinitions_Get) operation.</span></span>

### <a name="get-aliases"></a><span data-ttu-id="015ed-129">取得別名</span><span class="sxs-lookup"><span data-stu-id="015ed-129">Get aliases</span></span>
<span data-ttu-id="015ed-130">您可以透過 REST API 擷取別名︰</span><span class="sxs-lookup"><span data-stu-id="015ed-130">You can retrieve aliases through the REST API:</span></span>

```HTTP
GET /subscriptions/{id}/providers?$expand=resourceTypes/aliases&api-version=2015-11-01
```

<span data-ttu-id="015ed-131">下列範例顯示別名的定義。</span><span class="sxs-lookup"><span data-stu-id="015ed-131">The following example shows a definition of an alias.</span></span> <span data-ttu-id="015ed-132">如您所見，別名在不同 API 版本中均會定義路徑，無論屬性名稱是否變更。</span><span class="sxs-lookup"><span data-stu-id="015ed-132">As you can see, an alias defines paths in different API versions, even when there is a property name change.</span></span> 

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

## <a name="powershell"></a><span data-ttu-id="015ed-133">PowerShell</span><span class="sxs-lookup"><span data-stu-id="015ed-133">PowerShell</span></span>

<span data-ttu-id="015ed-134">繼續 PowerShell 範例之前，請確定您已[安裝最新版](/powershell/azure/install-azurerm-ps)的 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="015ed-134">Before proceeding with the PowerShell examples, make sure you have [installed the latest version](/powershell/azure/install-azurerm-ps) of Azure PowerShell.</span></span> <span data-ttu-id="015ed-135">原則參數是於 3.6.0 版中加入。</span><span class="sxs-lookup"><span data-stu-id="015ed-135">Policy parameters were added in version 3.6.0.</span></span> <span data-ttu-id="015ed-136">如果您使用舊版本，範例會傳回找不到參數的錯誤。</span><span class="sxs-lookup"><span data-stu-id="015ed-136">If you have an earlier version, the examples return an error indicating the parameter cannot be found.</span></span>

### <a name="view-policy-definitions"></a><span data-ttu-id="015ed-137">檢視原則定義</span><span class="sxs-lookup"><span data-stu-id="015ed-137">View policy definitions</span></span>
<span data-ttu-id="015ed-138">若要查看訂用帳戶中的所有原則定義，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="015ed-138">To see all policy definitions in your subscription, use the following command:</span></span>

```powershell
Get-AzureRmPolicyDefinition
```

<span data-ttu-id="015ed-139">它會傳回所有可用的原則定義，包括內建原則。</span><span class="sxs-lookup"><span data-stu-id="015ed-139">It returns all available policy definitions, including built-in policies.</span></span> <span data-ttu-id="015ed-140">每個原則都以下列格式傳回：</span><span class="sxs-lookup"><span data-stu-id="015ed-140">Each policy is returned in the following format:</span></span>

```powershell
Name               : e56962a6-4747-49cd-b67b-bf8b01975c4c
ResourceId         : /providers/Microsoft.Authorization/policyDefinitions/e56962a6-4747-49cd-b67b-bf8b01975c4c
ResourceName       : e56962a6-4747-49cd-b67b-bf8b01975c4c
ResourceType       : Microsoft.Authorization/policyDefinitions
Properties         : @{displayName=Allowed locations; policyType=BuiltIn; description=This policy enables you to
                     restrict the locations your organization can specify when deploying resources. Use to enforce
                     your geo-compliance requirements.; parameters=; policyRule=}
PolicyDefinitionId : /providers/Microsoft.Authorization/policyDefinitions/e56962a6-4747-49cd-b67b-bf8b01975c4c
```

<span data-ttu-id="015ed-141">在繼續建立原則定義之前，請先查看內建原則。</span><span class="sxs-lookup"><span data-stu-id="015ed-141">Before proceeding to create a policy definition, look at the built-in policies.</span></span> <span data-ttu-id="015ed-142">如果找到可套用所需限制的內建原則，則您可以略過建立原則定義。</span><span class="sxs-lookup"><span data-stu-id="015ed-142">If you find a built-in policy that applies the limits you need, you can skip creating a policy definition.</span></span> <span data-ttu-id="015ed-143">反之，將內建原則指派給所需的範圍。</span><span class="sxs-lookup"><span data-stu-id="015ed-143">Instead, assign the built-in policy to the desired scope.</span></span>

### <a name="create-policy-definition"></a><span data-ttu-id="015ed-144">建立原則定義</span><span class="sxs-lookup"><span data-stu-id="015ed-144">Create policy definition</span></span>
<span data-ttu-id="015ed-145">您可以使用 `New-AzureRmPolicyDefinition` cmdlet 建立原則定義。</span><span class="sxs-lookup"><span data-stu-id="015ed-145">You can create a policy definition using the `New-AzureRmPolicyDefinition` cmdlet.</span></span>

```powershell
$definition = New-AzureRmPolicyDefinition -Name coolAccessTier -Description "Policy to specify access tier." -Policy '{
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

<span data-ttu-id="015ed-146">輸出會儲存在於原則指派期間使用的 `$definition` 物件中。</span><span class="sxs-lookup"><span data-stu-id="015ed-146">The output is stored in a `$definition` object, which is used during policy assignment.</span></span> 

<span data-ttu-id="015ed-147">您不需要指定 JSON 做為參數，而可以提供路徑給包含原則規則的 .json 檔案。</span><span class="sxs-lookup"><span data-stu-id="015ed-147">Rather than specifying the JSON as a parameter, you can provide the path to a .json file containing the policy rule.</span></span>

```powershell
$definition = New-AzureRmPolicyDefinition -Name coolAccessTier -Description "Policy to specify access tier." -Policy "c:\policies\coolAccessTier.json"
```

<span data-ttu-id="015ed-148">下列範例建立了包含參數的原則定義：</span><span class="sxs-lookup"><span data-stu-id="015ed-148">The following example creates a policy definition that includes parameters:</span></span>

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
          "description": "The list of locations that can be specified when deploying storage accounts.",
          "strongType": "location",
          "displayName": "Allowed locations"
        }
    }
}' 

$definition = New-AzureRmPolicyDefinition -Name storageLocations -Description "Policy to specify locations for storage accounts." -Policy $policy -Parameter $parameters 
```

### <a name="assign-policy"></a><span data-ttu-id="015ed-149">指派原則</span><span class="sxs-lookup"><span data-stu-id="015ed-149">Assign policy</span></span>

<span data-ttu-id="015ed-150">使用 `New-AzureRmPolicyAssignment` Cmdlet 將原則套用至所需範圍。</span><span class="sxs-lookup"><span data-stu-id="015ed-150">You apply the policy at the desired scope by using the `New-AzureRmPolicyAssignment` cmdlet.</span></span> <span data-ttu-id="015ed-151">以下範例將原則指派到資源群組。</span><span class="sxs-lookup"><span data-stu-id="015ed-151">The following example assigns the policy to a resource group.</span></span>

```powershell
$rg = Get-AzureRmResourceGroup -Name "ExampleGroup"
New-AzureRMPolicyAssignment -Name accessTierAssignment -Scope $rg.ResourceId -PolicyDefinition $definition
```

<span data-ttu-id="015ed-152">若要指派需要參數的原則，可建立包含那些值的物件。</span><span class="sxs-lookup"><span data-stu-id="015ed-152">To assign a policy that requires parameters, create and object with those values.</span></span> <span data-ttu-id="015ed-153">以下範例會擷取內建原則並將參數值傳入：</span><span class="sxs-lookup"><span data-stu-id="015ed-153">The following example retrieves a built-in policy and passes in parameters values:</span></span>

```powershell
$rg = Get-AzureRmResourceGroup -Name "ExampleGroup"
$definition = Get-AzureRmPolicyDefinition -Id /providers/Microsoft.Authorization/policyDefinitions/e5662a6-4747-49cd-b67b-bf8b01975c4c
$array = @("West US", "West US 2")
$param = @{"listOfAllowedLocations"=$array}
New-AzureRMPolicyAssignment -Name locationAssignment -Scope $rg.ResourceId -PolicyDefinition $definition -PolicyParameterObject $param
```

### <a name="view-policy-assignment"></a><span data-ttu-id="015ed-154">檢視原則指派</span><span class="sxs-lookup"><span data-stu-id="015ed-154">View policy assignment</span></span>

<span data-ttu-id="015ed-155">若要取得特定的原則指派，請使用：</span><span class="sxs-lookup"><span data-stu-id="015ed-155">To get a specific policy assignment, use:</span></span>

```powershell
$rg = Get-AzureRmResourceGroup -Name "ExampleGroup"
(Get-AzureRmPolicyAssignment -Name accessTierAssignment -Scope $rg.ResourceId
```

<span data-ttu-id="015ed-156">若要檢視原則定義的原則規則，請使用：</span><span class="sxs-lookup"><span data-stu-id="015ed-156">To view the policy rule for a policy definition, use:</span></span>

```powershell
(Get-AzureRmPolicyDefinition -Name coolAccessTier).Properties.policyRule | ConvertTo-Json
```

### <a name="remove-policy-assignment"></a><span data-ttu-id="015ed-157">移除原則指派</span><span class="sxs-lookup"><span data-stu-id="015ed-157">Remove policy assignment</span></span> 

<span data-ttu-id="015ed-158">若要移除原則指派，請使用：</span><span class="sxs-lookup"><span data-stu-id="015ed-158">To remove a policy assignment, use:</span></span>

```powershell
Remove-AzureRmPolicyAssignment -Name regionPolicyAssignment -Scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

## <a name="azure-cli"></a><span data-ttu-id="015ed-159">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="015ed-159">Azure CLI</span></span>

### <a name="view-policy-definitions"></a><span data-ttu-id="015ed-160">檢視原則定義</span><span class="sxs-lookup"><span data-stu-id="015ed-160">View policy definitions</span></span>
<span data-ttu-id="015ed-161">若要查看訂用帳戶中的所有原則定義，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="015ed-161">To see all policy definitions in your subscription, use the following command:</span></span>

```azurecli
az policy definition list
```

<span data-ttu-id="015ed-162">它會傳回所有可用的原則定義，包括內建原則。</span><span class="sxs-lookup"><span data-stu-id="015ed-162">It returns all available policy definitions, including built-in policies.</span></span> <span data-ttu-id="015ed-163">每個原則都以下列格式傳回：</span><span class="sxs-lookup"><span data-stu-id="015ed-163">Each policy is returned in the following format:</span></span>

```azurecli
{                                                            
  "description": "This policy enables you to restrict the locations your organization can specify when deploying resources. Use to enforce your geo-compliance requirements.",                      
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

<span data-ttu-id="015ed-164">在繼續建立原則定義之前，請先查看內建原則。</span><span class="sxs-lookup"><span data-stu-id="015ed-164">Before proceeding to create a policy definition, look at the built-in policies.</span></span> <span data-ttu-id="015ed-165">如果找到可套用所需限制的內建原則，則您可以略過建立原則定義。</span><span class="sxs-lookup"><span data-stu-id="015ed-165">If you find a built-in policy that applies the limits you need, you can skip creating a policy definition.</span></span> <span data-ttu-id="015ed-166">反之，將內建原則指派給所需的範圍。</span><span class="sxs-lookup"><span data-stu-id="015ed-166">Instead, assign the built-in policy to the desired scope.</span></span>

### <a name="create-policy-definition"></a><span data-ttu-id="015ed-167">建立原則定義</span><span class="sxs-lookup"><span data-stu-id="015ed-167">Create policy definition</span></span>

<span data-ttu-id="015ed-168">您可以使用 Azure CLI 搭配原則定義命令來建立原則定義。</span><span class="sxs-lookup"><span data-stu-id="015ed-168">You can create a policy definition using Azure CLI with the policy definition command.</span></span>

```azurecli
az policy definition create --name coolAccessTier --description "Policy to specify access tier." --rules '{
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

### <a name="assign-policy"></a><span data-ttu-id="015ed-169">指派原則</span><span class="sxs-lookup"><span data-stu-id="015ed-169">Assign policy</span></span>

<span data-ttu-id="015ed-170">您可以使用原則指派命令將原則套用至所需的範圍。</span><span class="sxs-lookup"><span data-stu-id="015ed-170">You can apply the policy to the desired scope by using the policy assignment command.</span></span> <span data-ttu-id="015ed-171">以下範例將原則指派到資源群組。</span><span class="sxs-lookup"><span data-stu-id="015ed-171">The following example assigns a policy to a resource group.</span></span>

```azurecli
az policy assignment create --name coolAccessTierAssignment --policy coolAccessTier --scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

### <a name="view-policy-assignment"></a><span data-ttu-id="015ed-172">檢視原則指派</span><span class="sxs-lookup"><span data-stu-id="015ed-172">View policy assignment</span></span>

<span data-ttu-id="015ed-173">若要檢視原則指派，請提供原則指派名稱和範圍：</span><span class="sxs-lookup"><span data-stu-id="015ed-173">To view a policy assignment, provide the policy assignment name and the scope:</span></span>

```azurecli
az policy assignment show --name coolAccessTierAssignment --scope "/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}"
```

### <a name="remove-policy-assignment"></a><span data-ttu-id="015ed-174">移除原則指派</span><span class="sxs-lookup"><span data-stu-id="015ed-174">Remove policy assignment</span></span> 

<span data-ttu-id="015ed-175">若要移除原則指派，請使用：</span><span class="sxs-lookup"><span data-stu-id="015ed-175">To remove a policy assignment, use:</span></span>

```azurecli
az policy assignment delete --name coolAccessTier --scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

## <a name="next-steps"></a><span data-ttu-id="015ed-176">後續步驟</span><span class="sxs-lookup"><span data-stu-id="015ed-176">Next steps</span></span>
* <span data-ttu-id="015ed-177">如需關於企業如何使用 Resource Manager 有效地管理訂閱的指引，請參閱 [Azure 企業 Scaffold - 規定的訂用帳戶治理](resource-manager-subscription-governance.md)。</span><span class="sxs-lookup"><span data-stu-id="015ed-177">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

