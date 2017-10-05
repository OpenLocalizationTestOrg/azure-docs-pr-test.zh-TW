---
title: "Azure 資源原則 | Microsoft Docs"
description: "描述如何使用 Azure Resource Manager 原則以確保在部署期間設定一致的資源內容。 原則可以套用在訂用帳戶或資源群組。"
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: abde0f73-c0fe-4e6d-a1ee-32a6fce52a2d
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/02/2017
ms.author: tomfitz
ms.openlocfilehash: 0ee2624f45a1de0c23cae4538a38ae3e302eedd3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="resource-policy-overview"></a><span data-ttu-id="bf278-104">資源原則概觀</span><span class="sxs-lookup"><span data-stu-id="bf278-104">Resource policy overview</span></span>
<span data-ttu-id="bf278-105">資源原則可讓您為組織中的資源建立慣例。</span><span class="sxs-lookup"><span data-stu-id="bf278-105">Resource policies enable you to establish conventions for resources in your organization.</span></span> <span data-ttu-id="bf278-106">藉由定義慣例，您可以控制成本以及更輕鬆地管理您的資源。</span><span class="sxs-lookup"><span data-stu-id="bf278-106">By defining conventions, you can control costs and more easily manage your resources.</span></span> <span data-ttu-id="bf278-107">例如，您可以指定僅允許特定類型的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="bf278-107">For example, you can specify that only certain types of virtual machines are allowed.</span></span> <span data-ttu-id="bf278-108">或者，您可以要求所有資源都有特定標籤。</span><span class="sxs-lookup"><span data-stu-id="bf278-108">Or, you can require that all resources have a particular tag.</span></span> <span data-ttu-id="bf278-109">原則會由所有子資源繼承。</span><span class="sxs-lookup"><span data-stu-id="bf278-109">Policies are inherited by all child resources.</span></span> <span data-ttu-id="bf278-110">所以，如果原則套用至資源群組，它會適用於該資源群組中的所有資源。</span><span class="sxs-lookup"><span data-stu-id="bf278-110">So, if a policy is applied to a resource group, it is applicable to all the resources in that resource group.</span></span>

<span data-ttu-id="bf278-111">有兩個概念可了解原則︰</span><span class="sxs-lookup"><span data-stu-id="bf278-111">There are two concepts to understand about policies:</span></span>

* <span data-ttu-id="bf278-112">原則定義 - 您說明何時會強制執行原則及要採取的動作</span><span class="sxs-lookup"><span data-stu-id="bf278-112">policy definition - you describe when the policy is enforced and what action to take</span></span>
* <span data-ttu-id="bf278-113">原則指派 - 您將原則定義套用至範圍 (訂用帳戶或資源群組)</span><span class="sxs-lookup"><span data-stu-id="bf278-113">policy assignment - you apply the policy definition to a scope (subscription or resource group)</span></span>

<span data-ttu-id="bf278-114">本主題著重於原則定義。</span><span class="sxs-lookup"><span data-stu-id="bf278-114">This topic focuses on policy definition.</span></span> <span data-ttu-id="bf278-115">如需原則指派的相關資訊，請參閱[使用 Azure 入口網站來指派和管理資源原則](resource-manager-policy-portal.md)或[透過指令碼來指派和管理原則](resource-manager-policy-create-assign.md)。</span><span class="sxs-lookup"><span data-stu-id="bf278-115">For information about policy assignment, see [Use Azure portal to assign and manage resource policies](resource-manager-policy-portal.md) or [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span>

<span data-ttu-id="bf278-116">建立和更新資源 (PUT 和 PATCH 作業) 時，會評估原則。</span><span class="sxs-lookup"><span data-stu-id="bf278-116">Policies are evaluated when creating and updating resources (PUT and PATCH operations).</span></span>

> [!NOTE]
> <span data-ttu-id="bf278-117">目前，原則不會評估不支援標記、種類及位置的資源類型，例如 Microsoft.Resources/deployments 資源類型。</span><span class="sxs-lookup"><span data-stu-id="bf278-117">Currently, policy does not evaluate resource types that do not support tags, kind, and location, such as the Microsoft.Resources/deployments resource type.</span></span> <span data-ttu-id="bf278-118">未來將加入此支援。</span><span class="sxs-lookup"><span data-stu-id="bf278-118">This support will be added at a future time.</span></span> <span data-ttu-id="bf278-119">若要避免向下相容問題，撰寫原則時應該明確指定類型。</span><span class="sxs-lookup"><span data-stu-id="bf278-119">To avoid backward compatibility issues, you should explicitly specify type when authoring policies.</span></span> <span data-ttu-id="bf278-120">例如，會對所有類型套用未指定類型的標記原則。</span><span class="sxs-lookup"><span data-stu-id="bf278-120">For example, a tag policy that does not specify types is applied for all types.</span></span> <span data-ttu-id="bf278-121">在此情況下，如果有不支援標記的巢狀資源，且部署資源類型已新增原則評估中，範本部署可能會失敗。</span><span class="sxs-lookup"><span data-stu-id="bf278-121">In that case, a template deployment may fail if there is a nested resource that doesn't support tags, and the deployment resource type has been added to policy evaluation.</span></span> 
> 
> 

## <a name="how-is-it-different-from-rbac"></a><span data-ttu-id="bf278-122">它和 RBAC 有什麼不同？</span><span class="sxs-lookup"><span data-stu-id="bf278-122">How is it different from RBAC?</span></span>
<span data-ttu-id="bf278-123">原則和角色型存取控制 (RBAC) 之間有幾個主要差異。</span><span class="sxs-lookup"><span data-stu-id="bf278-123">There are a few key differences between policy and role-based access control (RBAC).</span></span> <span data-ttu-id="bf278-124">RBAC 著重於不同範圍的**使用者**動作。</span><span class="sxs-lookup"><span data-stu-id="bf278-124">RBAC focuses on **user** actions at different scopes.</span></span> <span data-ttu-id="bf278-125">例如，若您被加入所需範圍內之資源群組的參與者角色中，您便能對該資源群組做出變更。</span><span class="sxs-lookup"><span data-stu-id="bf278-125">For example, you are added to the contributor role for a resource group at the desired scope, so you can make changes to that resource group.</span></span> <span data-ttu-id="bf278-126">原則在部署期間著重於**資源**屬性。</span><span class="sxs-lookup"><span data-stu-id="bf278-126">Policy focuses on **resource** properties during deployment.</span></span> <span data-ttu-id="bf278-127">例如，您能夠透過原則控制可以佈建的資源類型。</span><span class="sxs-lookup"><span data-stu-id="bf278-127">For example, through policies, you can control the types of resources that can be provisioned.</span></span> <span data-ttu-id="bf278-128">或者，您可以限制資源可以佈建的位置。</span><span class="sxs-lookup"><span data-stu-id="bf278-128">Or, you can restrict the locations in which the resources can be provisioned.</span></span> <span data-ttu-id="bf278-129">不同於 RBAC，原則是個預設允許和明確拒絕的系統。</span><span class="sxs-lookup"><span data-stu-id="bf278-129">Unlike RBAC, policy is a default allow and explicit deny system.</span></span> 

<span data-ttu-id="bf278-130">若要使用原則，您必須透過 RBAC 驗證。</span><span class="sxs-lookup"><span data-stu-id="bf278-130">To use policies, you must be authenticated through RBAC.</span></span> <span data-ttu-id="bf278-131">具體來說，您的帳戶需要：</span><span class="sxs-lookup"><span data-stu-id="bf278-131">Specifically, your account needs the:</span></span>

* <span data-ttu-id="bf278-132">定義原則的 `Microsoft.Authorization/policydefinitions/write` 權限</span><span class="sxs-lookup"><span data-stu-id="bf278-132">`Microsoft.Authorization/policydefinitions/write` permission to define a policy</span></span>
* <span data-ttu-id="bf278-133">指派原則的 `Microsoft.Authorization/policyassignments/write` 權限</span><span class="sxs-lookup"><span data-stu-id="bf278-133">`Microsoft.Authorization/policyassignments/write` permission to assign a policy</span></span> 

<span data-ttu-id="bf278-134">這些權限不包括在**參與者**角色中。</span><span class="sxs-lookup"><span data-stu-id="bf278-134">These permissions are not included in the **Contributor** role.</span></span>

## <a name="built-in-policies"></a><span data-ttu-id="bf278-135">內建原則</span><span class="sxs-lookup"><span data-stu-id="bf278-135">Built-in policies</span></span>

<span data-ttu-id="bf278-136">Azure 提供一些內建原則定義，可能會降低您需要定義的原則數目。</span><span class="sxs-lookup"><span data-stu-id="bf278-136">Azure provides some built-in policy definitions that may reduce the number of policies you have to define.</span></span> <span data-ttu-id="bf278-137">在繼續處理原則定義之前，您應該先考慮內建原則是否已提供所需的定義。</span><span class="sxs-lookup"><span data-stu-id="bf278-137">Before proceeding with policy definitions, you should consider whether a built-in policy already provides the definition you need.</span></span> <span data-ttu-id="bf278-138">內建的原則定義如下：</span><span class="sxs-lookup"><span data-stu-id="bf278-138">The built-in policy definitions are:</span></span>

* <span data-ttu-id="bf278-139">允許的位置</span><span class="sxs-lookup"><span data-stu-id="bf278-139">Allowed locations</span></span>
* <span data-ttu-id="bf278-140">允許的資源類型</span><span class="sxs-lookup"><span data-stu-id="bf278-140">Allowed resource types</span></span>
* <span data-ttu-id="bf278-141">允許的儲存體帳戶 SKU</span><span class="sxs-lookup"><span data-stu-id="bf278-141">Allowed storage account SKUs</span></span>
* <span data-ttu-id="bf278-142">允許的虛擬機器 SKU</span><span class="sxs-lookup"><span data-stu-id="bf278-142">Allowed virtual machine SKUs</span></span>
* <span data-ttu-id="bf278-143">套用標籤和預設值</span><span class="sxs-lookup"><span data-stu-id="bf278-143">Apply tag and default value</span></span>
* <span data-ttu-id="bf278-144">強制執行標籤和值</span><span class="sxs-lookup"><span data-stu-id="bf278-144">Enforce tag and value</span></span>
* <span data-ttu-id="bf278-145">不允許的資源類型</span><span class="sxs-lookup"><span data-stu-id="bf278-145">Not allowed resource types</span></span>
* <span data-ttu-id="bf278-146">需要 SQL Server 12.0 版</span><span class="sxs-lookup"><span data-stu-id="bf278-146">Require SQL Server version 12.0</span></span>
* <span data-ttu-id="bf278-147">需要儲存體帳戶加密</span><span class="sxs-lookup"><span data-stu-id="bf278-147">Require storage account encryption</span></span>

<span data-ttu-id="bf278-148">您可以透[入口網站](resource-manager-policy-portal.md)、[PowerShell](resource-manager-policy-create-assign.md#powershell) 或 [Azure CLI](resource-manager-policy-create-assign.md#azure-cli) 來指派任何這些原則。</span><span class="sxs-lookup"><span data-stu-id="bf278-148">You can assign any of these policies through the [portal](resource-manager-policy-portal.md), [PowerShell](resource-manager-policy-create-assign.md#powershell), or [Azure CLI](resource-manager-policy-create-assign.md#azure-cli).</span></span>

## <a name="policy-definition-structure"></a><span data-ttu-id="bf278-149">原則定義結構</span><span class="sxs-lookup"><span data-stu-id="bf278-149">Policy definition structure</span></span>
<span data-ttu-id="bf278-150">使用 JSON 來建立原則定義。</span><span class="sxs-lookup"><span data-stu-id="bf278-150">You use JSON to create a policy definition.</span></span> <span data-ttu-id="bf278-151">原則定義中包含以下的項目︰</span><span class="sxs-lookup"><span data-stu-id="bf278-151">The policy definition contains elements for:</span></span>

* <span data-ttu-id="bf278-152">參數</span><span class="sxs-lookup"><span data-stu-id="bf278-152">parameters</span></span>
* <span data-ttu-id="bf278-153">顯示名稱</span><span class="sxs-lookup"><span data-stu-id="bf278-153">display name</span></span>
* <span data-ttu-id="bf278-154">說明</span><span class="sxs-lookup"><span data-stu-id="bf278-154">description</span></span>
* <span data-ttu-id="bf278-155">原則規則</span><span class="sxs-lookup"><span data-stu-id="bf278-155">policy rule</span></span>
  * <span data-ttu-id="bf278-156">邏輯評估</span><span class="sxs-lookup"><span data-stu-id="bf278-156">logical evaluation</span></span>
  * <span data-ttu-id="bf278-157">效果</span><span class="sxs-lookup"><span data-stu-id="bf278-157">effect</span></span>

<span data-ttu-id="bf278-158">下列範例示範的原則會限制資源的部署之處︰</span><span class="sxs-lookup"><span data-stu-id="bf278-158">The following example shows a policy that limits where resources are deployed:</span></span>

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

## <a name="parameters"></a><span data-ttu-id="bf278-159">參數</span><span class="sxs-lookup"><span data-stu-id="bf278-159">Parameters</span></span>
<span data-ttu-id="bf278-160">使用參數會減少原則定義的數量，有助於簡化原則管理。</span><span class="sxs-lookup"><span data-stu-id="bf278-160">Using parameters helps simplify your policy management by reducing the number of policy definitions.</span></span> <span data-ttu-id="bf278-161">定義資源屬性的原則 (例如，限制可以在其中部署資源的位置)，並在定義中包含參數。</span><span class="sxs-lookup"><span data-stu-id="bf278-161">You define a policy for a resource property (such as limiting the locations where resources can be deployed), and include parameters in the definition.</span></span> <span data-ttu-id="bf278-162">然後，您藉由在指派原則時傳入不同的值 (例如，指定訂用帳戶的一組位置)，針對不同的案例重複使用該原則定義。</span><span class="sxs-lookup"><span data-stu-id="bf278-162">Then, you reuse that policy definition for different scenarios by passing in different values (such as specifying one set of locations for a subscription) when assigning the policy.</span></span>

<span data-ttu-id="bf278-163">當您建立原則定義時，宣告參數。</span><span class="sxs-lookup"><span data-stu-id="bf278-163">You declare parameters when you create policy definitions.</span></span>

```json
"parameters": {
  "allowedLocations": {
    "type": "array",
    "metadata": {
      "description": "The list of allowed locations for resources.",
      "displayName": "Allowed locations"
    }
  }
}
```

<span data-ttu-id="bf278-164">參數的類型可以是字串或陣列。</span><span class="sxs-lookup"><span data-stu-id="bf278-164">The type of a parameter can be either string or array.</span></span> <span data-ttu-id="bf278-165">中繼資料屬性是由 Azure 入口網站等工具所使用，用來顯示人性化的資訊。</span><span class="sxs-lookup"><span data-stu-id="bf278-165">The metadata property is used for tools like Azure portal to display user-friendly information.</span></span> 

<span data-ttu-id="bf278-166">在原則規則中，您可以使用下列語法參考參數︰</span><span class="sxs-lookup"><span data-stu-id="bf278-166">In the policy rule, you reference parameters with the following syntax:</span></span> 

```json
{ 
    "field": "location",
    "in": "[parameters('allowedLocations')]"
}
```

## <a name="display-name-and-description"></a><span data-ttu-id="bf278-167">顯示名稱和描述</span><span class="sxs-lookup"><span data-stu-id="bf278-167">Display name and description</span></span>

<span data-ttu-id="bf278-168">使用 **displayName** 和 **description**找出原則定義，並提供使用時的內容。</span><span class="sxs-lookup"><span data-stu-id="bf278-168">You use the **displayName** and **description** to identify the policy definition, and provide context for when it is used.</span></span>

## <a name="policy-rule"></a><span data-ttu-id="bf278-169">原則規則</span><span class="sxs-lookup"><span data-stu-id="bf278-169">Policy rule</span></span>

<span data-ttu-id="bf278-170">原則規則包含 **If** 和 **Then**區塊。</span><span class="sxs-lookup"><span data-stu-id="bf278-170">The policy rule consists of **If** and **Then** blocks.</span></span> <span data-ttu-id="bf278-171">在 **If** 區塊中，您可以定義一個或多個指定強制執行此原則時間的條件。</span><span class="sxs-lookup"><span data-stu-id="bf278-171">In the **If** block, you define one or more conditions that specify when the policy is enforced.</span></span> <span data-ttu-id="bf278-172">您可以將邏輯運算子套用至這些條件，以精確地定義原則的案例。</span><span class="sxs-lookup"><span data-stu-id="bf278-172">You can apply logical operators to these conditions to precisely define the scenario for a policy.</span></span> <span data-ttu-id="bf278-173">在 **Then** 區塊中，定義當 **If** 條件履行時所發生的效果。</span><span class="sxs-lookup"><span data-stu-id="bf278-173">In the **Then** block, you define the effect that happens when the **If** conditions are fulfilled.</span></span>

```json
{
  "if": {
    <condition> | <logical operator>
  },
  "then": {
    "effect": "deny | audit | append"
  }
}
```

### <a name="logical-operators"></a><span data-ttu-id="bf278-174">邏輯運算子</span><span class="sxs-lookup"><span data-stu-id="bf278-174">Logical operators</span></span>
<span data-ttu-id="bf278-175">支援的邏輯運算子包括︰</span><span class="sxs-lookup"><span data-stu-id="bf278-175">The supported logical operators are:</span></span>

* `"not": {condition  or operator}`
* `"allOf": [{condition or operator},{condition or operator}]`
* `"anyOf": [{condition or operator},{condition or operator}]`

<span data-ttu-id="bf278-176">**not** 語法會反轉條件的結果。</span><span class="sxs-lookup"><span data-stu-id="bf278-176">The **not** syntax inverts the result of the condition.</span></span> <span data-ttu-id="bf278-177">**allOf** 語法 (類似於邏輯**And** 作業) 需要所有的條件為 true。</span><span class="sxs-lookup"><span data-stu-id="bf278-177">The **allOf** syntax (similar to the logical **And** operation) requires all conditions to be true.</span></span> <span data-ttu-id="bf278-178">**anyOf** 語法 (類似於邏輯**Or** 作業) 需要一或多個條件為 true。</span><span class="sxs-lookup"><span data-stu-id="bf278-178">The **anyOf** syntax (similar to the logical **Or** operation) requires one or more conditions to be true.</span></span>

<span data-ttu-id="bf278-179">您可以巢狀邏輯運算子。</span><span class="sxs-lookup"><span data-stu-id="bf278-179">You can nest logical operators.</span></span> <span data-ttu-id="bf278-180">下列範例顯示 **allOf** 作業中的巢狀 **not** 作業。</span><span class="sxs-lookup"><span data-stu-id="bf278-180">The following example shows a **not** operation that is nested within an **allOf** operation.</span></span> 

```json
"if": {
  "allOf": [
    {
      "not": {
        "field": "tags",
        "containsKey": "application"
      }
    },
    {
      "field": "type",
      "equals": "Microsoft.Storage/storageAccounts"
    }
  ]
},
```

### <a name="conditions"></a><span data-ttu-id="bf278-181">條件</span><span class="sxs-lookup"><span data-stu-id="bf278-181">Conditions</span></span>
<span data-ttu-id="bf278-182">條件會評估某個**欄位**是否符合特定準則。</span><span class="sxs-lookup"><span data-stu-id="bf278-182">The condition evaluates whether a **field** meets certain criteria.</span></span> <span data-ttu-id="bf278-183">支援的條件如下︰</span><span class="sxs-lookup"><span data-stu-id="bf278-183">The supported conditions are:</span></span>

* `"equals": "value"`
* `"like": "value"`
* `"match": "value"`
* `"contains": "value"`
* `"in": ["value1","value2"]`
* `"containsKey": "keyName"`
* `"exists": "bool"`

<span data-ttu-id="bf278-184">當使用 **like**條件時，您可以在值中提供萬用字元 (*)。</span><span class="sxs-lookup"><span data-stu-id="bf278-184">When using the **like** condition, you can provide a wildcard (*) in the value.</span></span>

<span data-ttu-id="bf278-185">使用**符合**條件時，請提供 `#` 來表示數字、`?` 來表示字母，以及任何其他字元來表示該實際字元。</span><span class="sxs-lookup"><span data-stu-id="bf278-185">When using the **match** condition, provide `#` to represent a digit, `?` for a letter, and any other character to represent that actual character.</span></span> <span data-ttu-id="bf278-186">例如，請參閱[為名稱和文字套用資源原則](resource-manager-policy-naming-convention.md)。</span><span class="sxs-lookup"><span data-stu-id="bf278-186">For examples, see [Apply resource policies for names and text](resource-manager-policy-naming-convention.md).</span></span>

### <a name="fields"></a><span data-ttu-id="bf278-187">欄位</span><span class="sxs-lookup"><span data-stu-id="bf278-187">Fields</span></span>
<span data-ttu-id="bf278-188">條件是透過欄位所形成。</span><span class="sxs-lookup"><span data-stu-id="bf278-188">Conditions are formed by using fields.</span></span> <span data-ttu-id="bf278-189">欄位會顯示用來描述資源狀態的資源要求裝載屬性。</span><span class="sxs-lookup"><span data-stu-id="bf278-189">A field represents properties in the resource request payload that is used to describe the state of the resource.</span></span>  

<span data-ttu-id="bf278-190">支援下列欄位：</span><span class="sxs-lookup"><span data-stu-id="bf278-190">The following fields are supported:</span></span>

* `name`
* `kind`
* `type`
* `location`
* `tags`
* `tags.*` 
* <span data-ttu-id="bf278-191">屬性別名 - 如需清單，請參閱[別名](#aliases)。</span><span class="sxs-lookup"><span data-stu-id="bf278-191">property aliases - for a list, see [Aliases](#aliases).</span></span>

### <a name="effect"></a><span data-ttu-id="bf278-192">效果</span><span class="sxs-lookup"><span data-stu-id="bf278-192">Effect</span></span>
<span data-ttu-id="bf278-193">原則支援三種效果類型 - `deny`、`audit` 和 `append`。</span><span class="sxs-lookup"><span data-stu-id="bf278-193">Policy supports three types of effect - `deny`, `audit`, and `append`.</span></span> 

* <span data-ttu-id="bf278-194">**拒絕**會在稽核記錄中產生事件，並且使要求失敗</span><span class="sxs-lookup"><span data-stu-id="bf278-194">**Deny** generates an event in the audit log and fails the request</span></span>
* <span data-ttu-id="bf278-195">**稽核**會在稽核記錄中產生事件，但不會使要求失敗</span><span class="sxs-lookup"><span data-stu-id="bf278-195">**Audit** generates a warning event in audit log but does not fail the request</span></span>
* <span data-ttu-id="bf278-196">**附加**會在要求中加入一組已定義的欄位</span><span class="sxs-lookup"><span data-stu-id="bf278-196">**Append** adds the defined set of fields to the request</span></span> 

<span data-ttu-id="bf278-197">對於 **append**，您必須提供下列詳細資料：</span><span class="sxs-lookup"><span data-stu-id="bf278-197">For **append**, you must provide the following details:</span></span>

```json
"effect": "append",
"details": [
  {
    "field": "field name",
    "value": "value of the field"
  }
]
```

<span data-ttu-id="bf278-198">值可以是字串或 JSON 格式物件。</span><span class="sxs-lookup"><span data-stu-id="bf278-198">The value can be either a string or a JSON format object.</span></span> 

## <a name="aliases"></a><span data-ttu-id="bf278-199">別名</span><span class="sxs-lookup"><span data-stu-id="bf278-199">Aliases</span></span>

<span data-ttu-id="bf278-200">您可以使用屬性別名來存取資源類型的特定屬性。</span><span class="sxs-lookup"><span data-stu-id="bf278-200">You use property aliases to access specific properties for a resource type.</span></span> <span data-ttu-id="bf278-201">別名可讓您限制某個資源上的某個值所允許的值或條件。</span><span class="sxs-lookup"><span data-stu-id="bf278-201">Aliases enable you to restrict what values or conditions are permitted for a property on a resource.</span></span> <span data-ttu-id="bf278-202">每個別名會對應至指定資源類型之不同 API 版本中的路徑。</span><span class="sxs-lookup"><span data-stu-id="bf278-202">Each alias maps to paths in different API versions for a given resource type.</span></span> <span data-ttu-id="bf278-203">在原則評估期間，原則引擎會取得該 API 版本的屬性路徑。</span><span class="sxs-lookup"><span data-stu-id="bf278-203">During policy evaluation, the policy engine gets the property path for that API version.</span></span>

<span data-ttu-id="bf278-204">**Microsoft.Cache/Redis**</span><span class="sxs-lookup"><span data-stu-id="bf278-204">**Microsoft.Cache/Redis**</span></span>

| <span data-ttu-id="bf278-205">Alias</span><span class="sxs-lookup"><span data-stu-id="bf278-205">Alias</span></span> | <span data-ttu-id="bf278-206">說明</span><span class="sxs-lookup"><span data-stu-id="bf278-206">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="bf278-207">Microsoft.Cache/Redis/enableNonSslPort</span><span class="sxs-lookup"><span data-stu-id="bf278-207">Microsoft.Cache/Redis/enableNonSslPort</span></span> | <span data-ttu-id="bf278-208">設定是否啟用非 SSL Redis 伺服器連接埠 (6379)。</span><span class="sxs-lookup"><span data-stu-id="bf278-208">Set whether the non-ssl Redis server port (6379) is enabled.</span></span> |
| <span data-ttu-id="bf278-209">Microsoft.Cache/Redis/shardCount</span><span class="sxs-lookup"><span data-stu-id="bf278-209">Microsoft.Cache/Redis/shardCount</span></span> | <span data-ttu-id="bf278-210">設定要在進階叢集快取上建立的分區數目。</span><span class="sxs-lookup"><span data-stu-id="bf278-210">Set the number of shards to be created on a Premium Cluster Cache.</span></span>  |
| <span data-ttu-id="bf278-211">Microsoft.Cache/Redis/sku.capacity</span><span class="sxs-lookup"><span data-stu-id="bf278-211">Microsoft.Cache/Redis/sku.capacity</span></span> | <span data-ttu-id="bf278-212">設定要部署的 Redis 快取大小。</span><span class="sxs-lookup"><span data-stu-id="bf278-212">Set the size of the Redis cache to deploy.</span></span>  |
| <span data-ttu-id="bf278-213">Microsoft.Cache/Redis/sku.family</span><span class="sxs-lookup"><span data-stu-id="bf278-213">Microsoft.Cache/Redis/sku.family</span></span> | <span data-ttu-id="bf278-214">設定要使用的 SKU 系列。</span><span class="sxs-lookup"><span data-stu-id="bf278-214">Set the SKU family to use.</span></span> |
| <span data-ttu-id="bf278-215">Microsoft.Cache/Redis/sku.name</span><span class="sxs-lookup"><span data-stu-id="bf278-215">Microsoft.Cache/Redis/sku.name</span></span> | <span data-ttu-id="bf278-216">設定要部署的 Redis 快取類型。</span><span class="sxs-lookup"><span data-stu-id="bf278-216">Set the type of Redis Cache to deploy.</span></span> |

<span data-ttu-id="bf278-217">**Microsoft.Cdn/profiles**</span><span class="sxs-lookup"><span data-stu-id="bf278-217">**Microsoft.Cdn/profiles**</span></span>

| <span data-ttu-id="bf278-218">Alias</span><span class="sxs-lookup"><span data-stu-id="bf278-218">Alias</span></span> | <span data-ttu-id="bf278-219">說明</span><span class="sxs-lookup"><span data-stu-id="bf278-219">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="bf278-220">Microsoft.CDN/profiles/sku.name</span><span class="sxs-lookup"><span data-stu-id="bf278-220">Microsoft.CDN/profiles/sku.name</span></span> | <span data-ttu-id="bf278-221">設定定價層的名稱。</span><span class="sxs-lookup"><span data-stu-id="bf278-221">Set the name of the pricing tier.</span></span> |

<span data-ttu-id="bf278-222">**Microsoft.Compute/disks**</span><span class="sxs-lookup"><span data-stu-id="bf278-222">**Microsoft.Compute/disks**</span></span>

| <span data-ttu-id="bf278-223">Alias</span><span class="sxs-lookup"><span data-stu-id="bf278-223">Alias</span></span> | <span data-ttu-id="bf278-224">說明</span><span class="sxs-lookup"><span data-stu-id="bf278-224">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="bf278-225">Microsoft.Compute/imageOffer</span><span class="sxs-lookup"><span data-stu-id="bf278-225">Microsoft.Compute/imageOffer</span></span> | <span data-ttu-id="bf278-226">設定用來建立虛擬機器的平台映像或 Marketplace 映像供應項目。</span><span class="sxs-lookup"><span data-stu-id="bf278-226">Set the offer of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="bf278-227">Microsoft.Compute/imagePublisher</span><span class="sxs-lookup"><span data-stu-id="bf278-227">Microsoft.Compute/imagePublisher</span></span> | <span data-ttu-id="bf278-228">設定用來建立虛擬機器的平台映像或 Marketplace 映像發行者。</span><span class="sxs-lookup"><span data-stu-id="bf278-228">Set the publisher of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="bf278-229">Microsoft.Compute/imageSku</span><span class="sxs-lookup"><span data-stu-id="bf278-229">Microsoft.Compute/imageSku</span></span> | <span data-ttu-id="bf278-230">設定用來建立虛擬機器的平台映像或 Marketplace 映像 SKU。</span><span class="sxs-lookup"><span data-stu-id="bf278-230">Set the SKU of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="bf278-231">Microsoft.Compute/imageVersion</span><span class="sxs-lookup"><span data-stu-id="bf278-231">Microsoft.Compute/imageVersion</span></span> | <span data-ttu-id="bf278-232">設定用來建立虛擬機器的平台映像或 Marketplace 映像版本。</span><span class="sxs-lookup"><span data-stu-id="bf278-232">Set the version of the platform image or marketplace image used to create the virtual machine.</span></span> |


<span data-ttu-id="bf278-233">**Microsoft.Compute/virtualMachines**</span><span class="sxs-lookup"><span data-stu-id="bf278-233">**Microsoft.Compute/virtualMachines**</span></span>

| <span data-ttu-id="bf278-234">Alias</span><span class="sxs-lookup"><span data-stu-id="bf278-234">Alias</span></span> | <span data-ttu-id="bf278-235">說明</span><span class="sxs-lookup"><span data-stu-id="bf278-235">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="bf278-236">Microsoft.Compute/imageId</span><span class="sxs-lookup"><span data-stu-id="bf278-236">Microsoft.Compute/imageId</span></span> | <span data-ttu-id="bf278-237">設定用來建立虛擬機器的映像識別碼。</span><span class="sxs-lookup"><span data-stu-id="bf278-237">Set the identifier of the image used to create the virtual machine.</span></span> |
| <span data-ttu-id="bf278-238">Microsoft.Compute/imageOffer</span><span class="sxs-lookup"><span data-stu-id="bf278-238">Microsoft.Compute/imageOffer</span></span> | <span data-ttu-id="bf278-239">設定用來建立虛擬機器的平台映像或 Marketplace 映像供應項目。</span><span class="sxs-lookup"><span data-stu-id="bf278-239">Set the offer of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="bf278-240">Microsoft.Compute/imagePublisher</span><span class="sxs-lookup"><span data-stu-id="bf278-240">Microsoft.Compute/imagePublisher</span></span> | <span data-ttu-id="bf278-241">設定用來建立虛擬機器的平台映像或 Marketplace 映像發行者。</span><span class="sxs-lookup"><span data-stu-id="bf278-241">Set the publisher of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="bf278-242">Microsoft.Compute/imageSku</span><span class="sxs-lookup"><span data-stu-id="bf278-242">Microsoft.Compute/imageSku</span></span> | <span data-ttu-id="bf278-243">設定用來建立虛擬機器的平台映像或 Marketplace 映像 SKU。</span><span class="sxs-lookup"><span data-stu-id="bf278-243">Set the SKU of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="bf278-244">Microsoft.Compute/imageVersion</span><span class="sxs-lookup"><span data-stu-id="bf278-244">Microsoft.Compute/imageVersion</span></span> | <span data-ttu-id="bf278-245">設定用來建立虛擬機器的平台映像或 Marketplace 映像版本。</span><span class="sxs-lookup"><span data-stu-id="bf278-245">Set the version of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="bf278-246">Microsoft.Compute/licenseType</span><span class="sxs-lookup"><span data-stu-id="bf278-246">Microsoft.Compute/licenseType</span></span> | <span data-ttu-id="bf278-247">將映像或磁碟設定為內部部署授權。</span><span class="sxs-lookup"><span data-stu-id="bf278-247">Set that the image or disk is licensed on-premises.</span></span> <span data-ttu-id="bf278-248">這個值只會用於包含 Windows Server 作業系統的映象。</span><span class="sxs-lookup"><span data-stu-id="bf278-248">This value is only used for images that contain the Windows Server operating system.</span></span>  |
| <span data-ttu-id="bf278-249">Microsoft.Compute/virtualMachines/imageOffer</span><span class="sxs-lookup"><span data-stu-id="bf278-249">Microsoft.Compute/virtualMachines/imageOffer</span></span> | <span data-ttu-id="bf278-250">設定用來建立虛擬機器的平台映像或 Marketplace 映像供應項目。</span><span class="sxs-lookup"><span data-stu-id="bf278-250">Set the offer of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="bf278-251">Microsoft.Compute/virtualMachines/imagePublisher</span><span class="sxs-lookup"><span data-stu-id="bf278-251">Microsoft.Compute/virtualMachines/imagePublisher</span></span> | <span data-ttu-id="bf278-252">設定用來建立虛擬機器的平台映像或 Marketplace 映像發行者。</span><span class="sxs-lookup"><span data-stu-id="bf278-252">Set the publisher of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="bf278-253">Microsoft.Compute/virtualMachines/imageSku</span><span class="sxs-lookup"><span data-stu-id="bf278-253">Microsoft.Compute/virtualMachines/imageSku</span></span> | <span data-ttu-id="bf278-254">設定用來建立虛擬機器的平台映像或 Marketplace 映像 SKU。</span><span class="sxs-lookup"><span data-stu-id="bf278-254">Set the SKU of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="bf278-255">Microsoft.Compute/virtualMachines/imageVersion</span><span class="sxs-lookup"><span data-stu-id="bf278-255">Microsoft.Compute/virtualMachines/imageVersion</span></span> | <span data-ttu-id="bf278-256">設定用來建立虛擬機器的平台映像或 Marketplace 映像版本。</span><span class="sxs-lookup"><span data-stu-id="bf278-256">Set the version of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="bf278-257">Microsoft.Compute/virtualMachines/osDisk.Uri</span><span class="sxs-lookup"><span data-stu-id="bf278-257">Microsoft.Compute/virtualMachines/osDisk.Uri</span></span> | <span data-ttu-id="bf278-258">設定 vhd URI。</span><span class="sxs-lookup"><span data-stu-id="bf278-258">Set the vhd URI.</span></span> |
| <span data-ttu-id="bf278-259">Microsoft.Compute/virtualMachines/sku.name</span><span class="sxs-lookup"><span data-stu-id="bf278-259">Microsoft.Compute/virtualMachines/sku.name</span></span> | <span data-ttu-id="bf278-260">設定虛擬機器的大小。</span><span class="sxs-lookup"><span data-stu-id="bf278-260">Set the size of the virtual machine.</span></span> |

<span data-ttu-id="bf278-261">**Microsoft.Compute/virtualMachines/extensions**</span><span class="sxs-lookup"><span data-stu-id="bf278-261">**Microsoft.Compute/virtualMachines/extensions**</span></span>

| <span data-ttu-id="bf278-262">Alias</span><span class="sxs-lookup"><span data-stu-id="bf278-262">Alias</span></span> | <span data-ttu-id="bf278-263">說明</span><span class="sxs-lookup"><span data-stu-id="bf278-263">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="bf278-264">Microsoft.Compute/virtualMachines/extensions/publisher</span><span class="sxs-lookup"><span data-stu-id="bf278-264">Microsoft.Compute/virtualMachines/extensions/publisher</span></span> | <span data-ttu-id="bf278-265">設定擴充功能發行者的名稱。</span><span class="sxs-lookup"><span data-stu-id="bf278-265">Set the name of the extension’s publisher.</span></span> |
| <span data-ttu-id="bf278-266">Microsoft.Compute/virtualMachines/extensions/type</span><span class="sxs-lookup"><span data-stu-id="bf278-266">Microsoft.Compute/virtualMachines/extensions/type</span></span> | <span data-ttu-id="bf278-267">設定擴充功能的類型。</span><span class="sxs-lookup"><span data-stu-id="bf278-267">Set the type of extension.</span></span> |
| <span data-ttu-id="bf278-268">Microsoft.Compute/virtualMachines/extensions/typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="bf278-268">Microsoft.Compute/virtualMachines/extensions/typeHandlerVersion</span></span> | <span data-ttu-id="bf278-269">設定擴充功能的版本。</span><span class="sxs-lookup"><span data-stu-id="bf278-269">Set the version of the extension.</span></span> |

<span data-ttu-id="bf278-270">**Microsoft.Compute/virtualMachineScaleSets**</span><span class="sxs-lookup"><span data-stu-id="bf278-270">**Microsoft.Compute/virtualMachineScaleSets**</span></span>

| <span data-ttu-id="bf278-271">Alias</span><span class="sxs-lookup"><span data-stu-id="bf278-271">Alias</span></span> | <span data-ttu-id="bf278-272">說明</span><span class="sxs-lookup"><span data-stu-id="bf278-272">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="bf278-273">Microsoft.Compute/imageId</span><span class="sxs-lookup"><span data-stu-id="bf278-273">Microsoft.Compute/imageId</span></span> | <span data-ttu-id="bf278-274">設定用來建立虛擬機器的映像識別碼。</span><span class="sxs-lookup"><span data-stu-id="bf278-274">Set the identifier of the image used to create the virtual machine.</span></span> |
| <span data-ttu-id="bf278-275">Microsoft.Compute/imageOffer</span><span class="sxs-lookup"><span data-stu-id="bf278-275">Microsoft.Compute/imageOffer</span></span> | <span data-ttu-id="bf278-276">設定用來建立虛擬機器的平台映像或 Marketplace 映像供應項目。</span><span class="sxs-lookup"><span data-stu-id="bf278-276">Set the offer of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="bf278-277">Microsoft.Compute/imagePublisher</span><span class="sxs-lookup"><span data-stu-id="bf278-277">Microsoft.Compute/imagePublisher</span></span> | <span data-ttu-id="bf278-278">設定用來建立虛擬機器的平台映像或 Marketplace 映像發行者。</span><span class="sxs-lookup"><span data-stu-id="bf278-278">Set the publisher of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="bf278-279">Microsoft.Compute/imageSku</span><span class="sxs-lookup"><span data-stu-id="bf278-279">Microsoft.Compute/imageSku</span></span> | <span data-ttu-id="bf278-280">設定用來建立虛擬機器的平台映像或 Marketplace 映像 SKU。</span><span class="sxs-lookup"><span data-stu-id="bf278-280">Set the SKU of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="bf278-281">Microsoft.Compute/imageVersion</span><span class="sxs-lookup"><span data-stu-id="bf278-281">Microsoft.Compute/imageVersion</span></span> | <span data-ttu-id="bf278-282">設定用來建立虛擬機器的平台映像或 Marketplace 映像版本。</span><span class="sxs-lookup"><span data-stu-id="bf278-282">Set the version of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="bf278-283">Microsoft.Compute/licenseType</span><span class="sxs-lookup"><span data-stu-id="bf278-283">Microsoft.Compute/licenseType</span></span> | <span data-ttu-id="bf278-284">將映像或磁碟設定為內部部署授權。</span><span class="sxs-lookup"><span data-stu-id="bf278-284">Set that the image or disk is licensed on-premises.</span></span> <span data-ttu-id="bf278-285">這個值只會用於包含 Windows Server 作業系統的映象。</span><span class="sxs-lookup"><span data-stu-id="bf278-285">This value is only used for images that contain the Windows Server operating system.</span></span> |
| <span data-ttu-id="bf278-286">Microsoft.Compute/VirtualMachineScaleSets/computerNamePrefix</span><span class="sxs-lookup"><span data-stu-id="bf278-286">Microsoft.Compute/VirtualMachineScaleSets/computerNamePrefix</span></span> | <span data-ttu-id="bf278-287">設定擴展集中所有虛擬機器的電腦名稱前置詞。</span><span class="sxs-lookup"><span data-stu-id="bf278-287">Set the computer name prefix for all  the virtual machines in the scale set.</span></span> |
| <span data-ttu-id="bf278-288">Microsoft.Compute/VirtualMachineScaleSets/osdisk.imageUrl</span><span class="sxs-lookup"><span data-stu-id="bf278-288">Microsoft.Compute/VirtualMachineScaleSets/osdisk.imageUrl</span></span> | <span data-ttu-id="bf278-289">設定使用者映像的 Blob URI。</span><span class="sxs-lookup"><span data-stu-id="bf278-289">Set the blob URI for user image.</span></span> |
| <span data-ttu-id="bf278-290">Microsoft.Compute/VirtualMachineScaleSets/osdisk.vhdContainers</span><span class="sxs-lookup"><span data-stu-id="bf278-290">Microsoft.Compute/VirtualMachineScaleSets/osdisk.vhdContainers</span></span> | <span data-ttu-id="bf278-291">設定用於儲存擴展集作業系統磁碟的容器 URL。</span><span class="sxs-lookup"><span data-stu-id="bf278-291">Set the container URLs that are used to store operating system disks for the scale set.</span></span> |
| <span data-ttu-id="bf278-292">Microsoft.Compute/VirtualMachineScaleSets/sku.name</span><span class="sxs-lookup"><span data-stu-id="bf278-292">Microsoft.Compute/VirtualMachineScaleSets/sku.name</span></span> | <span data-ttu-id="bf278-293">設定擴展集中虛擬機器的大小。</span><span class="sxs-lookup"><span data-stu-id="bf278-293">Set the size of virtual machines in a scale set.</span></span> |
| <span data-ttu-id="bf278-294">Microsoft.Compute/VirtualMachineScaleSets/sku.tier</span><span class="sxs-lookup"><span data-stu-id="bf278-294">Microsoft.Compute/VirtualMachineScaleSets/sku.tier</span></span> | <span data-ttu-id="bf278-295">設定擴展集中的虛擬機器層。</span><span class="sxs-lookup"><span data-stu-id="bf278-295">Set the tier of virtual machines in a scale set.</span></span> |
  
<span data-ttu-id="bf278-296">**Microsoft.Network/applicationGateways**</span><span class="sxs-lookup"><span data-stu-id="bf278-296">**Microsoft.Network/applicationGateways**</span></span>

| <span data-ttu-id="bf278-297">Alias</span><span class="sxs-lookup"><span data-stu-id="bf278-297">Alias</span></span> | <span data-ttu-id="bf278-298">說明</span><span class="sxs-lookup"><span data-stu-id="bf278-298">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="bf278-299">Microsoft.Network/applicationGateways/sku.name</span><span class="sxs-lookup"><span data-stu-id="bf278-299">Microsoft.Network/applicationGateways/sku.name</span></span> | <span data-ttu-id="bf278-300">設定閘道的大小。</span><span class="sxs-lookup"><span data-stu-id="bf278-300">Set the size of the gateway.</span></span> |

<span data-ttu-id="bf278-301">**Microsoft.Network/virtualNetworkGateways**</span><span class="sxs-lookup"><span data-stu-id="bf278-301">**Microsoft.Network/virtualNetworkGateways**</span></span>

| <span data-ttu-id="bf278-302">Alias</span><span class="sxs-lookup"><span data-stu-id="bf278-302">Alias</span></span> | <span data-ttu-id="bf278-303">說明</span><span class="sxs-lookup"><span data-stu-id="bf278-303">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="bf278-304">Microsoft.Network/virtualNetworkGateways/gatewayType</span><span class="sxs-lookup"><span data-stu-id="bf278-304">Microsoft.Network/virtualNetworkGateways/gatewayType</span></span> | <span data-ttu-id="bf278-305">設定此虛擬網路閘道的類型。</span><span class="sxs-lookup"><span data-stu-id="bf278-305">Set the type of this virtual network gateway.</span></span> |
| <span data-ttu-id="bf278-306">Microsoft.Network/virtualNetworkGateways/sku.name</span><span class="sxs-lookup"><span data-stu-id="bf278-306">Microsoft.Network/virtualNetworkGateways/sku.name</span></span> | <span data-ttu-id="bf278-307">設定閘道 SKU 名稱。</span><span class="sxs-lookup"><span data-stu-id="bf278-307">Set the gateway SKU name.</span></span> |

<span data-ttu-id="bf278-308">**Microsoft.Sql/servers**</span><span class="sxs-lookup"><span data-stu-id="bf278-308">**Microsoft.Sql/servers**</span></span>

| <span data-ttu-id="bf278-309">Alias</span><span class="sxs-lookup"><span data-stu-id="bf278-309">Alias</span></span> | <span data-ttu-id="bf278-310">說明</span><span class="sxs-lookup"><span data-stu-id="bf278-310">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="bf278-311">Microsoft.Sql/servers/version</span><span class="sxs-lookup"><span data-stu-id="bf278-311">Microsoft.Sql/servers/version</span></span> | <span data-ttu-id="bf278-312">設定伺服器的版本。</span><span class="sxs-lookup"><span data-stu-id="bf278-312">Set the version of the server.</span></span> |

<span data-ttu-id="bf278-313">**Microsoft.Sql/databases**</span><span class="sxs-lookup"><span data-stu-id="bf278-313">**Microsoft.Sql/databases**</span></span>

| <span data-ttu-id="bf278-314">Alias</span><span class="sxs-lookup"><span data-stu-id="bf278-314">Alias</span></span> | <span data-ttu-id="bf278-315">說明</span><span class="sxs-lookup"><span data-stu-id="bf278-315">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="bf278-316">Microsoft.Sql/servers/databases/edition</span><span class="sxs-lookup"><span data-stu-id="bf278-316">Microsoft.Sql/servers/databases/edition</span></span> | <span data-ttu-id="bf278-317">設定資料庫的版本。</span><span class="sxs-lookup"><span data-stu-id="bf278-317">Set the edition of the database.</span></span> |
| <span data-ttu-id="bf278-318">Microsoft.Sql/servers/databases/elasticPoolName</span><span class="sxs-lookup"><span data-stu-id="bf278-318">Microsoft.Sql/servers/databases/elasticPoolName</span></span> | <span data-ttu-id="bf278-319">設定資料庫所在彈性集區的名稱。</span><span class="sxs-lookup"><span data-stu-id="bf278-319">Set the name of the elastic pool the database is in.</span></span> |
| <span data-ttu-id="bf278-320">Microsoft.Sql/servers/databases/requestedServiceObjectiveId</span><span class="sxs-lookup"><span data-stu-id="bf278-320">Microsoft.Sql/servers/databases/requestedServiceObjectiveId</span></span> | <span data-ttu-id="bf278-321">設定伺服器所設定的服務層級目標識別碼。</span><span class="sxs-lookup"><span data-stu-id="bf278-321">Set the configured service level objective ID of the database.</span></span> |
| <span data-ttu-id="bf278-322">Microsoft.Sql/servers/databases/requestedServiceObjectiveName</span><span class="sxs-lookup"><span data-stu-id="bf278-322">Microsoft.Sql/servers/databases/requestedServiceObjectiveName</span></span> | <span data-ttu-id="bf278-323">設定資料庫所設定之服務等級目標的名稱。</span><span class="sxs-lookup"><span data-stu-id="bf278-323">Set the name of the configured service level objective of the database.</span></span>  |

<span data-ttu-id="bf278-324">**Microsoft.Sql/elasticpools**</span><span class="sxs-lookup"><span data-stu-id="bf278-324">**Microsoft.Sql/elasticpools**</span></span>

| <span data-ttu-id="bf278-325">Alias</span><span class="sxs-lookup"><span data-stu-id="bf278-325">Alias</span></span> | <span data-ttu-id="bf278-326">說明</span><span class="sxs-lookup"><span data-stu-id="bf278-326">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="bf278-327">servers/elasticpools</span><span class="sxs-lookup"><span data-stu-id="bf278-327">servers/elasticpools</span></span> | <span data-ttu-id="bf278-328">Microsoft.Sql/servers/elasticPools/dtu</span><span class="sxs-lookup"><span data-stu-id="bf278-328">Microsoft.Sql/servers/elasticPools/dtu</span></span> | <span data-ttu-id="bf278-329">設定資料庫彈性集區的所有共用 DTU。</span><span class="sxs-lookup"><span data-stu-id="bf278-329">Set the total shared DTU for the database elastic pool.</span></span> |
| <span data-ttu-id="bf278-330">servers/elasticpools</span><span class="sxs-lookup"><span data-stu-id="bf278-330">servers/elasticpools</span></span> | <span data-ttu-id="bf278-331">Microsoft.Sql/servers/elasticPools/edition</span><span class="sxs-lookup"><span data-stu-id="bf278-331">Microsoft.Sql/servers/elasticPools/edition</span></span> | <span data-ttu-id="bf278-332">設定彈性集區的版本。</span><span class="sxs-lookup"><span data-stu-id="bf278-332">Set the edition of the elastic pool.</span></span> |

<span data-ttu-id="bf278-333">**Microsoft.Storage/storageAccounts**</span><span class="sxs-lookup"><span data-stu-id="bf278-333">**Microsoft.Storage/storageAccounts**</span></span>

| <span data-ttu-id="bf278-334">Alias</span><span class="sxs-lookup"><span data-stu-id="bf278-334">Alias</span></span> | <span data-ttu-id="bf278-335">說明</span><span class="sxs-lookup"><span data-stu-id="bf278-335">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="bf278-336">Microsoft.Storage/storageAccounts/accessTier</span><span class="sxs-lookup"><span data-stu-id="bf278-336">Microsoft.Storage/storageAccounts/accessTier</span></span> | <span data-ttu-id="bf278-337">設定用於計費的存取層。</span><span class="sxs-lookup"><span data-stu-id="bf278-337">Set the access tier used for billing.</span></span> |
| <span data-ttu-id="bf278-338">Microsoft.Storage/storageAccounts/accountType</span><span class="sxs-lookup"><span data-stu-id="bf278-338">Microsoft.Storage/storageAccounts/accountType</span></span> | <span data-ttu-id="bf278-339">設定 SKU 名稱。</span><span class="sxs-lookup"><span data-stu-id="bf278-339">Set the SKU name.</span></span> |
| <span data-ttu-id="bf278-340">Microsoft.Storage/storageAccounts/enableBlobEncryption</span><span class="sxs-lookup"><span data-stu-id="bf278-340">Microsoft.Storage/storageAccounts/enableBlobEncryption</span></span> | <span data-ttu-id="bf278-341">設定服務是否對儲存在 Blob 儲存體服務中的資料進行加密。</span><span class="sxs-lookup"><span data-stu-id="bf278-341">Set whether the service encrypts the data as it is stored in the blob storage service.</span></span> |
| <span data-ttu-id="bf278-342">Microsoft.Storage/storageAccounts/enableFileEncryption</span><span class="sxs-lookup"><span data-stu-id="bf278-342">Microsoft.Storage/storageAccounts/enableFileEncryption</span></span> | <span data-ttu-id="bf278-343">設定服務是否對儲存在檔案儲存體服務中的資料進行加密。</span><span class="sxs-lookup"><span data-stu-id="bf278-343">Set whether the service encrypts the data as it is stored in the file storage service.</span></span> |
| <span data-ttu-id="bf278-344">Microsoft.Storage/storageAccounts/sku.name</span><span class="sxs-lookup"><span data-stu-id="bf278-344">Microsoft.Storage/storageAccounts/sku.name</span></span> | <span data-ttu-id="bf278-345">設定 SKU 名稱。</span><span class="sxs-lookup"><span data-stu-id="bf278-345">Set the SKU name.</span></span> |
| <span data-ttu-id="bf278-346">Microsoft.Storage/storageAccounts/supportsHttpsTrafficOnly</span><span class="sxs-lookup"><span data-stu-id="bf278-346">Microsoft.Storage/storageAccounts/supportsHttpsTrafficOnly</span></span> | <span data-ttu-id="bf278-347">設定對於儲存體服務僅允許 HTTPS 流量。</span><span class="sxs-lookup"><span data-stu-id="bf278-347">Set to allow only https traffic to storage service.</span></span> |


## <a name="policy-examples"></a><span data-ttu-id="bf278-348">原則範例</span><span class="sxs-lookup"><span data-stu-id="bf278-348">Policy examples</span></span>

<span data-ttu-id="bf278-349">下列主題包含原則範例︰</span><span class="sxs-lookup"><span data-stu-id="bf278-349">The following topics contain policy examples:</span></span>

* <span data-ttu-id="bf278-350">如需標籤原則的範例，請參閱[套用標籤的資源原則](resource-manager-policy-tags.md)。</span><span class="sxs-lookup"><span data-stu-id="bf278-350">For examples of tag polices, see [Apply resource policies for tags](resource-manager-policy-tags.md).</span></span>
* <span data-ttu-id="bf278-351">如需命名和文字模式的範例，請參閱[為名稱和文字套用資源原則](resource-manager-policy-naming-convention.md)。</span><span class="sxs-lookup"><span data-stu-id="bf278-351">For examples of naming and text patterns, see [Apply resource policies for names and text](resource-manager-policy-naming-convention.md).</span></span>
* <span data-ttu-id="bf278-352">如需儲存體原則的範例，請參閱[將資源原則套用至儲存體帳戶](resource-manager-policy-storage.md)。</span><span class="sxs-lookup"><span data-stu-id="bf278-352">For examples of storage policies, see [Apply resource policies to storage accounts](resource-manager-policy-storage.md).</span></span>
* <span data-ttu-id="bf278-353">如需虛擬機器原則的範例，請參閱[將資源原則套用至 Linux VM](../virtual-machines/linux/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json) 和[將資源原則套用至 Windows VM](../virtual-machines/windows/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="bf278-353">For examples of virtual machine policies, see [Apply resource policies to Linux VMs](../virtual-machines/linux/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json) and [Apply resource policies to Windows VMs](../virtual-machines/windows/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json)</span></span>


## <a name="next-steps"></a><span data-ttu-id="bf278-354">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bf278-354">Next steps</span></span>
* <span data-ttu-id="bf278-355">在定義原則規則後，將它指派給範圍。</span><span class="sxs-lookup"><span data-stu-id="bf278-355">After defining a policy rule, assign it to a scope.</span></span> <span data-ttu-id="bf278-356">若要透過入口網站來指派原則，請參閱[使用 Azure 入口網站來指派和管理資源原則](resource-manager-policy-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="bf278-356">To assign policies through the portal, see [Use Azure portal to assign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="bf278-357">若要透過 REST API、PowerShell 或 Azure CLI 來指派原則，請參閱[透過指令碼來指派和管理原則](resource-manager-policy-create-assign.md)。</span><span class="sxs-lookup"><span data-stu-id="bf278-357">To assign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span>
* <span data-ttu-id="bf278-358">如需關於企業如何使用 Resource Manager 有效地管理訂閱的指引，請參閱 [Azure 企業 Scaffold - 規定的訂用帳戶治理](resource-manager-subscription-governance.md)。</span><span class="sxs-lookup"><span data-stu-id="bf278-358">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>
* <span data-ttu-id="bf278-359">原則結構描述會發佈於 [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json)。</span><span class="sxs-lookup"><span data-stu-id="bf278-359">The policy schema is published at [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json).</span></span> 

