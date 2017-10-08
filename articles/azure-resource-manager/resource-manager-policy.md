---
title: "aaaAzure 資源原則 |Microsoft 文件"
description: "描述如何在部署期間設定 toouse Azure 資源管理員原則 tooensure 一致的資源內容。 原則可以套用在 hello 訂用帳戶或資源群組。"
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
ms.openlocfilehash: f1b0bbb5f838f6bb70721e1040ad3eac2d881cea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="resource-policy-overview"></a><span data-ttu-id="2ebd3-104">資源原則概觀</span><span class="sxs-lookup"><span data-stu-id="2ebd3-104">Resource policy overview</span></span>
<span data-ttu-id="2ebd3-105">資源原則可讓您在組織中的資源 tooestablish 慣例。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-105">Resource policies enable you tooestablish conventions for resources in your organization.</span></span> <span data-ttu-id="2ebd3-106">藉由定義慣例，您可以控制成本以及更輕鬆地管理您的資源。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-106">By defining conventions, you can control costs and more easily manage your resources.</span></span> <span data-ttu-id="2ebd3-107">例如，您可以指定僅允許特定類型的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-107">For example, you can specify that only certain types of virtual machines are allowed.</span></span> <span data-ttu-id="2ebd3-108">或者，您可以要求所有資源都有特定標籤。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-108">Or, you can require that all resources have a particular tag.</span></span> <span data-ttu-id="2ebd3-109">原則會由所有子資源繼承。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-109">Policies are inherited by all child resources.</span></span> <span data-ttu-id="2ebd3-110">因此，如果原則已套用的 tooa 資源群組，則該資源群組中的適用 tooall hello 資源。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-110">So, if a policy is applied tooa resource group, it is applicable tooall hello resources in that resource group.</span></span>

<span data-ttu-id="2ebd3-111">有兩個概念 toounderstand 有關原則：</span><span class="sxs-lookup"><span data-stu-id="2ebd3-111">There are two concepts toounderstand about policies:</span></span>

* <span data-ttu-id="2ebd3-112">原則定義-您說明 hello 原則會強制執行以及何種動作 tootake</span><span class="sxs-lookup"><span data-stu-id="2ebd3-112">policy definition - you describe when hello policy is enforced and what action tootake</span></span>
* <span data-ttu-id="2ebd3-113">原則指派-套用 hello 原則定義 tooa 範圍 （訂用帳戶或資源群組）</span><span class="sxs-lookup"><span data-stu-id="2ebd3-113">policy assignment - you apply hello policy definition tooa scope (subscription or resource group)</span></span>

<span data-ttu-id="2ebd3-114">本主題著重於原則定義。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-114">This topic focuses on policy definition.</span></span> <span data-ttu-id="2ebd3-115">原則指派的詳細資訊，請參閱[使用 Azure 入口網站 tooassign 和管理資源原則](resource-manager-policy-portal.md)或[指派及管理透過指令碼的原則](resource-manager-policy-create-assign.md)。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-115">For information about policy assignment, see [Use Azure portal tooassign and manage resource policies](resource-manager-policy-portal.md) or [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span>

<span data-ttu-id="2ebd3-116">建立和更新資源 (PUT 和 PATCH 作業) 時，會評估原則。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-116">Policies are evaluated when creating and updating resources (PUT and PATCH operations).</span></span>

> [!NOTE]
> <span data-ttu-id="2ebd3-117">目前，原則不會評估標記、 種類和位置，例如 hello Microsoft.Resources/deployments 資源類型不支援的資源類型。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-117">Currently, policy does not evaluate resource types that do not support tags, kind, and location, such as hello Microsoft.Resources/deployments resource type.</span></span> <span data-ttu-id="2ebd3-118">未來將加入此支援。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-118">This support will be added at a future time.</span></span> <span data-ttu-id="2ebd3-119">tooavoid 回溯相容性問題，您應該明確地指定類型撰寫原則時。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-119">tooavoid backward compatibility issues, you should explicitly specify type when authoring policies.</span></span> <span data-ttu-id="2ebd3-120">例如，會對所有類型套用未指定類型的標記原則。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-120">For example, a tag policy that does not specify types is applied for all types.</span></span> <span data-ttu-id="2ebd3-121">在此情況下，如果沒有不支援標記的巢狀的資源，範本部署可能會失敗，且已新增 hello 部署資源類型 toopolicy 評估。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-121">In that case, a template deployment may fail if there is a nested resource that doesn't support tags, and hello deployment resource type has been added toopolicy evaluation.</span></span> 
> 
> 

## <a name="how-is-it-different-from-rbac"></a><span data-ttu-id="2ebd3-122">它和 RBAC 有什麼不同？</span><span class="sxs-lookup"><span data-stu-id="2ebd3-122">How is it different from RBAC?</span></span>
<span data-ttu-id="2ebd3-123">原則和角色型存取控制 (RBAC) 之間有幾個主要差異。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-123">There are a few key differences between policy and role-based access control (RBAC).</span></span> <span data-ttu-id="2ebd3-124">RBAC 著重於不同範圍的**使用者**動作。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-124">RBAC focuses on **user** actions at different scopes.</span></span> <span data-ttu-id="2ebd3-125">比方說，您會加入資源群組的 toohello 參與者角色在 hello 預期範圍，因此您可以變更 toothat 資源群組。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-125">For example, you are added toohello contributor role for a resource group at hello desired scope, so you can make changes toothat resource group.</span></span> <span data-ttu-id="2ebd3-126">原則在部署期間著重於**資源**屬性。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-126">Policy focuses on **resource** properties during deployment.</span></span> <span data-ttu-id="2ebd3-127">例如，透過原則，您可以控制 hello 類型可以佈建的資源。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-127">For example, through policies, you can control hello types of resources that can be provisioned.</span></span> <span data-ttu-id="2ebd3-128">或者，您可以限制 hello hello 資源可以佈建所在的位置。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-128">Or, you can restrict hello locations in which hello resources can be provisioned.</span></span> <span data-ttu-id="2ebd3-129">不同於 RBAC，原則是個預設允許和明確拒絕的系統。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-129">Unlike RBAC, policy is a default allow and explicit deny system.</span></span> 

<span data-ttu-id="2ebd3-130">toouse 原則，您必須透過 RBAC 進行驗證。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-130">toouse policies, you must be authenticated through RBAC.</span></span> <span data-ttu-id="2ebd3-131">具體來說，您的帳戶需要：</span><span class="sxs-lookup"><span data-stu-id="2ebd3-131">Specifically, your account needs the:</span></span>

* <span data-ttu-id="2ebd3-132">`Microsoft.Authorization/policydefinitions/write`權限 toodefine 原則</span><span class="sxs-lookup"><span data-stu-id="2ebd3-132">`Microsoft.Authorization/policydefinitions/write` permission toodefine a policy</span></span>
* <span data-ttu-id="2ebd3-133">`Microsoft.Authorization/policyassignments/write`權限 tooassign 原則</span><span class="sxs-lookup"><span data-stu-id="2ebd3-133">`Microsoft.Authorization/policyassignments/write` permission tooassign a policy</span></span> 

<span data-ttu-id="2ebd3-134">這些權限不包含在 hello**參與者**角色。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-134">These permissions are not included in hello **Contributor** role.</span></span>

## <a name="built-in-policies"></a><span data-ttu-id="2ebd3-135">內建原則</span><span class="sxs-lookup"><span data-stu-id="2ebd3-135">Built-in policies</span></span>

<span data-ttu-id="2ebd3-136">Azure 提供 hello 數目可能會降低某些內建的原則定義的原則，您有 toodefine。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-136">Azure provides some built-in policy definitions that may reduce hello number of policies you have toodefine.</span></span> <span data-ttu-id="2ebd3-137">原則定義之前，您應該考慮的內建原則是否已提供您需要的 hello 定義。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-137">Before proceeding with policy definitions, you should consider whether a built-in policy already provides hello definition you need.</span></span> <span data-ttu-id="2ebd3-138">hello 內建的原則定義如下：</span><span class="sxs-lookup"><span data-stu-id="2ebd3-138">hello built-in policy definitions are:</span></span>

* <span data-ttu-id="2ebd3-139">允許的位置</span><span class="sxs-lookup"><span data-stu-id="2ebd3-139">Allowed locations</span></span>
* <span data-ttu-id="2ebd3-140">允許的資源類型</span><span class="sxs-lookup"><span data-stu-id="2ebd3-140">Allowed resource types</span></span>
* <span data-ttu-id="2ebd3-141">允許的儲存體帳戶 SKU</span><span class="sxs-lookup"><span data-stu-id="2ebd3-141">Allowed storage account SKUs</span></span>
* <span data-ttu-id="2ebd3-142">允許的虛擬機器 SKU</span><span class="sxs-lookup"><span data-stu-id="2ebd3-142">Allowed virtual machine SKUs</span></span>
* <span data-ttu-id="2ebd3-143">套用標籤和預設值</span><span class="sxs-lookup"><span data-stu-id="2ebd3-143">Apply tag and default value</span></span>
* <span data-ttu-id="2ebd3-144">強制執行標籤和值</span><span class="sxs-lookup"><span data-stu-id="2ebd3-144">Enforce tag and value</span></span>
* <span data-ttu-id="2ebd3-145">不允許的資源類型</span><span class="sxs-lookup"><span data-stu-id="2ebd3-145">Not allowed resource types</span></span>
* <span data-ttu-id="2ebd3-146">需要 SQL Server 12.0 版</span><span class="sxs-lookup"><span data-stu-id="2ebd3-146">Require SQL Server version 12.0</span></span>
* <span data-ttu-id="2ebd3-147">需要儲存體帳戶加密</span><span class="sxs-lookup"><span data-stu-id="2ebd3-147">Require storage account encryption</span></span>

<span data-ttu-id="2ebd3-148">您可以指定任何這些原則透過 hello[入口網站](resource-manager-policy-portal.md)， [PowerShell](resource-manager-policy-create-assign.md#powershell)，或[Azure CLI](resource-manager-policy-create-assign.md#azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-148">You can assign any of these policies through hello [portal](resource-manager-policy-portal.md), [PowerShell](resource-manager-policy-create-assign.md#powershell), or [Azure CLI](resource-manager-policy-create-assign.md#azure-cli).</span></span>

## <a name="policy-definition-structure"></a><span data-ttu-id="2ebd3-149">原則定義結構</span><span class="sxs-lookup"><span data-stu-id="2ebd3-149">Policy definition structure</span></span>
<span data-ttu-id="2ebd3-150">您使用 JSON toocreate 原則定義。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-150">You use JSON toocreate a policy definition.</span></span> <span data-ttu-id="2ebd3-151">hello 原則定義中包含項的目：</span><span class="sxs-lookup"><span data-stu-id="2ebd3-151">hello policy definition contains elements for:</span></span>

* <span data-ttu-id="2ebd3-152">參數</span><span class="sxs-lookup"><span data-stu-id="2ebd3-152">parameters</span></span>
* <span data-ttu-id="2ebd3-153">顯示名稱</span><span class="sxs-lookup"><span data-stu-id="2ebd3-153">display name</span></span>
* <span data-ttu-id="2ebd3-154">說明</span><span class="sxs-lookup"><span data-stu-id="2ebd3-154">description</span></span>
* <span data-ttu-id="2ebd3-155">原則規則</span><span class="sxs-lookup"><span data-stu-id="2ebd3-155">policy rule</span></span>
  * <span data-ttu-id="2ebd3-156">邏輯評估</span><span class="sxs-lookup"><span data-stu-id="2ebd3-156">logical evaluation</span></span>
  * <span data-ttu-id="2ebd3-157">效果</span><span class="sxs-lookup"><span data-stu-id="2ebd3-157">effect</span></span>

<span data-ttu-id="2ebd3-158">下列範例中的 hello 顯示限制在部署資源的原則：</span><span class="sxs-lookup"><span data-stu-id="2ebd3-158">hello following example shows a policy that limits where resources are deployed:</span></span>

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

## <a name="parameters"></a><span data-ttu-id="2ebd3-159">參數</span><span class="sxs-lookup"><span data-stu-id="2ebd3-159">Parameters</span></span>
<span data-ttu-id="2ebd3-160">使用參數，可協助減少 hello 原則定義的數量，以簡化原則管理。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-160">Using parameters helps simplify your policy management by reducing hello number of policy definitions.</span></span> <span data-ttu-id="2ebd3-161">定義的原則，資源內容 （例如限制可部署資源的 hello 位置），並在 hello 定義中包含參數。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-161">You define a policy for a resource property (such as limiting hello locations where resources can be deployed), and include parameters in hello definition.</span></span> <span data-ttu-id="2ebd3-162">然後，您重複使用該原則的定義不同的案例藉由傳遞不同的值 （例如，指定一組訂用帳戶的位置） 時指派 hello 原則。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-162">Then, you reuse that policy definition for different scenarios by passing in different values (such as specifying one set of locations for a subscription) when assigning hello policy.</span></span>

<span data-ttu-id="2ebd3-163">當您建立原則定義時，宣告參數。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-163">You declare parameters when you create policy definitions.</span></span>

```json
"parameters": {
  "allowedLocations": {
    "type": "array",
    "metadata": {
      "description": "hello list of allowed locations for resources.",
      "displayName": "Allowed locations"
    }
  }
}
```

<span data-ttu-id="2ebd3-164">hello 參數型別可以是字串或陣列。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-164">hello type of a parameter can be either string or array.</span></span> <span data-ttu-id="2ebd3-165">hello 中繼資料屬性用於 Azure 入口網站 toodisplay 人性化的資訊等工具。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-165">hello metadata property is used for tools like Azure portal toodisplay user-friendly information.</span></span> 

<span data-ttu-id="2ebd3-166">Hello 原則規則中，您可以參考參數以 hello，請使用下列語法：</span><span class="sxs-lookup"><span data-stu-id="2ebd3-166">In hello policy rule, you reference parameters with hello following syntax:</span></span> 

```json
{ 
    "field": "location",
    "in": "[parameters('allowedLocations')]"
}
```

## <a name="display-name-and-description"></a><span data-ttu-id="2ebd3-167">顯示名稱和描述</span><span class="sxs-lookup"><span data-stu-id="2ebd3-167">Display name and description</span></span>

<span data-ttu-id="2ebd3-168">使用 hello **displayName**和**描述**tooidentify hello 原則定義和使用時才提供的內容。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-168">You use hello **displayName** and **description** tooidentify hello policy definition, and provide context for when it is used.</span></span>

## <a name="policy-rule"></a><span data-ttu-id="2ebd3-169">原則規則</span><span class="sxs-lookup"><span data-stu-id="2ebd3-169">Policy rule</span></span>

<span data-ttu-id="2ebd3-170">hello 原則規則包含**如果**和**然後**區塊。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-170">hello policy rule consists of **If** and **Then** blocks.</span></span> <span data-ttu-id="2ebd3-171">在 hello**如果**區塊中，您定義一個或多個條件，指定 hello 原則會強制執行。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-171">In hello **If** block, you define one or more conditions that specify when hello policy is enforced.</span></span> <span data-ttu-id="2ebd3-172">您可以套用邏輯運算子 toothese 條件 tooprecisely 定義 hello 案例的原則。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-172">You can apply logical operators toothese conditions tooprecisely define hello scenario for a policy.</span></span> <span data-ttu-id="2ebd3-173">在 hello**然後**區塊中，定義當 hello hello 效果**如果**符合條件。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-173">In hello **Then** block, you define hello effect that happens when hello **If** conditions are fulfilled.</span></span>

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

### <a name="logical-operators"></a><span data-ttu-id="2ebd3-174">邏輯運算子</span><span class="sxs-lookup"><span data-stu-id="2ebd3-174">Logical operators</span></span>
<span data-ttu-id="2ebd3-175">是支援的 hello 邏輯運算子：</span><span class="sxs-lookup"><span data-stu-id="2ebd3-175">hello supported logical operators are:</span></span>

* `"not": {condition  or operator}`
* `"allOf": [{condition or operator},{condition or operator}]`
* `"anyOf": [{condition or operator},{condition or operator}]`

<span data-ttu-id="2ebd3-176">hello**不**語法反轉 hello 條件的 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-176">hello **not** syntax inverts hello result of hello condition.</span></span> <span data-ttu-id="2ebd3-177">hello **allOf**語法 (類似 toohello 邏輯**和**作業) 需要所有的條件 toobe true。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-177">hello **allOf** syntax (similar toohello logical **And** operation) requires all conditions toobe true.</span></span> <span data-ttu-id="2ebd3-178">hello **anyOf**語法 (類似 toohello 邏輯**或**作業) 需要一或多個條件 toobe true。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-178">hello **anyOf** syntax (similar toohello logical **Or** operation) requires one or more conditions toobe true.</span></span>

<span data-ttu-id="2ebd3-179">您可以巢狀邏輯運算子。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-179">You can nest logical operators.</span></span> <span data-ttu-id="2ebd3-180">下列範例所示的 hello**不**內變成巢狀的作業**allOf**作業。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-180">hello following example shows a **not** operation that is nested within an **allOf** operation.</span></span> 

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

### <a name="conditions"></a><span data-ttu-id="2ebd3-181">條件</span><span class="sxs-lookup"><span data-stu-id="2ebd3-181">Conditions</span></span>
<span data-ttu-id="2ebd3-182">hello 條件評估是否**欄位**是否符合特定準則。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-182">hello condition evaluates whether a **field** meets certain criteria.</span></span> <span data-ttu-id="2ebd3-183">支援的 hello 條件如下：</span><span class="sxs-lookup"><span data-stu-id="2ebd3-183">hello supported conditions are:</span></span>

* `"equals": "value"`
* `"like": "value"`
* `"match": "value"`
* `"contains": "value"`
* `"in": ["value1","value2"]`
* `"containsKey": "keyName"`
* `"exists": "bool"`

<span data-ttu-id="2ebd3-184">當使用 hello**像**條件，您可以提供萬用字元 （*） 在 hello 值。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-184">When using hello **like** condition, you can provide a wildcard (*) in hello value.</span></span>

<span data-ttu-id="2ebd3-185">當使用 hello**符合**條件，請提供`#`toorepresent 數字，`?`的字母，而且其他所有字元 toorepresent 的實際字元。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-185">When using hello **match** condition, provide `#` toorepresent a digit, `?` for a letter, and any other character toorepresent that actual character.</span></span> <span data-ttu-id="2ebd3-186">例如，請參閱[為名稱和文字套用資源原則](resource-manager-policy-naming-convention.md)。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-186">For examples, see [Apply resource policies for names and text](resource-manager-policy-naming-convention.md).</span></span>

### <a name="fields"></a><span data-ttu-id="2ebd3-187">欄位</span><span class="sxs-lookup"><span data-stu-id="2ebd3-187">Fields</span></span>
<span data-ttu-id="2ebd3-188">條件是透過欄位所形成。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-188">Conditions are formed by using fields.</span></span> <span data-ttu-id="2ebd3-189">欄位代表 hello 資源要求裝載中的內容也就是使用的 toodescribe hello hello 資源狀態。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-189">A field represents properties in hello resource request payload that is used toodescribe hello state of hello resource.</span></span>  

<span data-ttu-id="2ebd3-190">支援下列欄位的 hello:</span><span class="sxs-lookup"><span data-stu-id="2ebd3-190">hello following fields are supported:</span></span>

* `name`
* `kind`
* `type`
* `location`
* `tags`
* `tags.*` 
* <span data-ttu-id="2ebd3-191">屬性別名 - 如需清單，請參閱[別名](#aliases)。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-191">property aliases - for a list, see [Aliases](#aliases).</span></span>

### <a name="effect"></a><span data-ttu-id="2ebd3-192">效果</span><span class="sxs-lookup"><span data-stu-id="2ebd3-192">Effect</span></span>
<span data-ttu-id="2ebd3-193">原則支援三種效果類型 - `deny`、`audit` 和 `append`。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-193">Policy supports three types of effect - `deny`, `audit`, and `append`.</span></span> 

* <span data-ttu-id="2ebd3-194">**拒絕**hello 稽核記錄檔中產生事件，就會失敗 hello 要求</span><span class="sxs-lookup"><span data-stu-id="2ebd3-194">**Deny** generates an event in hello audit log and fails hello request</span></span>
* <span data-ttu-id="2ebd3-195">**稽核**稽核記錄檔中就會產生警告事件，但不會失敗 hello 要求</span><span class="sxs-lookup"><span data-stu-id="2ebd3-195">**Audit** generates a warning event in audit log but does not fail hello request</span></span>
* <span data-ttu-id="2ebd3-196">**附加**新增 hello 定義欄位 toohello 要求組</span><span class="sxs-lookup"><span data-stu-id="2ebd3-196">**Append** adds hello defined set of fields toohello request</span></span> 

<span data-ttu-id="2ebd3-197">如**附加**，您必須提供下列詳細資料的 hello:</span><span class="sxs-lookup"><span data-stu-id="2ebd3-197">For **append**, you must provide hello following details:</span></span>

```json
"effect": "append",
"details": [
  {
    "field": "field name",
    "value": "value of hello field"
  }
]
```

<span data-ttu-id="2ebd3-198">hello 值可以是字串或物件的 JSON 格式。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-198">hello value can be either a string or a JSON format object.</span></span> 

## <a name="aliases"></a><span data-ttu-id="2ebd3-199">別名</span><span class="sxs-lookup"><span data-stu-id="2ebd3-199">Aliases</span></span>

<span data-ttu-id="2ebd3-200">您可以使用屬性別名 tooaccess 特定屬性資源類型。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-200">You use property aliases tooaccess specific properties for a resource type.</span></span> <span data-ttu-id="2ebd3-201">別名可讓您 toorestrict 哪些值或條件允許資源上的屬性。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-201">Aliases enable you toorestrict what values or conditions are permitted for a property on a resource.</span></span> <span data-ttu-id="2ebd3-202">每個別名將對應 toopaths 中指定的資源類型的不同應用程式開發介面版本。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-202">Each alias maps toopaths in different API versions for a given resource type.</span></span> <span data-ttu-id="2ebd3-203">原則評估期間 hello 原則引擎會取得該應用程式開發介面版本 hello 屬性路徑。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-203">During policy evaluation, hello policy engine gets hello property path for that API version.</span></span>

<span data-ttu-id="2ebd3-204">**Microsoft.Cache/Redis**</span><span class="sxs-lookup"><span data-stu-id="2ebd3-204">**Microsoft.Cache/Redis**</span></span>

| <span data-ttu-id="2ebd3-205">Alias</span><span class="sxs-lookup"><span data-stu-id="2ebd3-205">Alias</span></span> | <span data-ttu-id="2ebd3-206">說明</span><span class="sxs-lookup"><span data-stu-id="2ebd3-206">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="2ebd3-207">Microsoft.Cache/Redis/enableNonSslPort</span><span class="sxs-lookup"><span data-stu-id="2ebd3-207">Microsoft.Cache/Redis/enableNonSslPort</span></span> | <span data-ttu-id="2ebd3-208">設定 hello 非 ssl 的 Redis 伺服器連接埠 (6379) 是否已啟用。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-208">Set whether hello non-ssl Redis server port (6379) is enabled.</span></span> |
| <span data-ttu-id="2ebd3-209">Microsoft.Cache/Redis/shardCount</span><span class="sxs-lookup"><span data-stu-id="2ebd3-209">Microsoft.Cache/Redis/shardCount</span></span> | <span data-ttu-id="2ebd3-210">設定進階叢集快取上建立的分區 toobe hello 號碼。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-210">Set hello number of shards toobe created on a Premium Cluster Cache.</span></span>  |
| <span data-ttu-id="2ebd3-211">Microsoft.Cache/Redis/sku.capacity</span><span class="sxs-lookup"><span data-stu-id="2ebd3-211">Microsoft.Cache/Redis/sku.capacity</span></span> | <span data-ttu-id="2ebd3-212">設定 hello Redis 快取 toodeploy hello 大小。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-212">Set hello size of hello Redis cache toodeploy.</span></span>  |
| <span data-ttu-id="2ebd3-213">Microsoft.Cache/Redis/sku.family</span><span class="sxs-lookup"><span data-stu-id="2ebd3-213">Microsoft.Cache/Redis/sku.family</span></span> | <span data-ttu-id="2ebd3-214">設定 hello SKU 系列 toouse。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-214">Set hello SKU family toouse.</span></span> |
| <span data-ttu-id="2ebd3-215">Microsoft.Cache/Redis/sku.name</span><span class="sxs-lookup"><span data-stu-id="2ebd3-215">Microsoft.Cache/Redis/sku.name</span></span> | <span data-ttu-id="2ebd3-216">設定 Redis 快取 toodeploy hello 類型。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-216">Set hello type of Redis Cache toodeploy.</span></span> |

<span data-ttu-id="2ebd3-217">**Microsoft.Cdn/profiles**</span><span class="sxs-lookup"><span data-stu-id="2ebd3-217">**Microsoft.Cdn/profiles**</span></span>

| <span data-ttu-id="2ebd3-218">Alias</span><span class="sxs-lookup"><span data-stu-id="2ebd3-218">Alias</span></span> | <span data-ttu-id="2ebd3-219">說明</span><span class="sxs-lookup"><span data-stu-id="2ebd3-219">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="2ebd3-220">Microsoft.CDN/profiles/sku.name</span><span class="sxs-lookup"><span data-stu-id="2ebd3-220">Microsoft.CDN/profiles/sku.name</span></span> | <span data-ttu-id="2ebd3-221">Hello 名稱 hello 定價層設定。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-221">Set hello name of hello pricing tier.</span></span> |

<span data-ttu-id="2ebd3-222">**Microsoft.Compute/disks**</span><span class="sxs-lookup"><span data-stu-id="2ebd3-222">**Microsoft.Compute/disks**</span></span>

| <span data-ttu-id="2ebd3-223">Alias</span><span class="sxs-lookup"><span data-stu-id="2ebd3-223">Alias</span></span> | <span data-ttu-id="2ebd3-224">說明</span><span class="sxs-lookup"><span data-stu-id="2ebd3-224">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="2ebd3-225">Microsoft.Compute/imageOffer</span><span class="sxs-lookup"><span data-stu-id="2ebd3-225">Microsoft.Compute/imageOffer</span></span> | <span data-ttu-id="2ebd3-226">Hello 平台映像或 marketplace 映像組 hello 優惠 toocreate hello 虛擬機器的使用。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-226">Set hello offer of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="2ebd3-227">Microsoft.Compute/imagePublisher</span><span class="sxs-lookup"><span data-stu-id="2ebd3-227">Microsoft.Compute/imagePublisher</span></span> | <span data-ttu-id="2ebd3-228">Hello 平台映像或 marketplace 映像組 hello 發行者使用 toocreate hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-228">Set hello publisher of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="2ebd3-229">Microsoft.Compute/imageSku</span><span class="sxs-lookup"><span data-stu-id="2ebd3-229">Microsoft.Compute/imageSku</span></span> | <span data-ttu-id="2ebd3-230">設定 hello hello 平台映像或 marketplace 映像的 SKU toocreate hello 虛擬機器的使用。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-230">Set hello SKU of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="2ebd3-231">Microsoft.Compute/imageVersion</span><span class="sxs-lookup"><span data-stu-id="2ebd3-231">Microsoft.Compute/imageVersion</span></span> | <span data-ttu-id="2ebd3-232">設定 hello hello 平台映像或 marketplace 映像使用新版 toocreate hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-232">Set hello version of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |


<span data-ttu-id="2ebd3-233">**Microsoft.Compute/virtualMachines**</span><span class="sxs-lookup"><span data-stu-id="2ebd3-233">**Microsoft.Compute/virtualMachines**</span></span>

| <span data-ttu-id="2ebd3-234">Alias</span><span class="sxs-lookup"><span data-stu-id="2ebd3-234">Alias</span></span> | <span data-ttu-id="2ebd3-235">說明</span><span class="sxs-lookup"><span data-stu-id="2ebd3-235">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="2ebd3-236">Microsoft.Compute/imageId</span><span class="sxs-lookup"><span data-stu-id="2ebd3-236">Microsoft.Compute/imageId</span></span> | <span data-ttu-id="2ebd3-237">設定 hello hello 用映像 toocreate hello 虛擬機器的識別項。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-237">Set hello identifier of hello image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="2ebd3-238">Microsoft.Compute/imageOffer</span><span class="sxs-lookup"><span data-stu-id="2ebd3-238">Microsoft.Compute/imageOffer</span></span> | <span data-ttu-id="2ebd3-239">Hello 平台映像或 marketplace 映像組 hello 優惠 toocreate hello 虛擬機器的使用。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-239">Set hello offer of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="2ebd3-240">Microsoft.Compute/imagePublisher</span><span class="sxs-lookup"><span data-stu-id="2ebd3-240">Microsoft.Compute/imagePublisher</span></span> | <span data-ttu-id="2ebd3-241">Hello 平台映像或 marketplace 映像組 hello 發行者使用 toocreate hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-241">Set hello publisher of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="2ebd3-242">Microsoft.Compute/imageSku</span><span class="sxs-lookup"><span data-stu-id="2ebd3-242">Microsoft.Compute/imageSku</span></span> | <span data-ttu-id="2ebd3-243">設定 hello hello 平台映像或 marketplace 映像的 SKU toocreate hello 虛擬機器的使用。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-243">Set hello SKU of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="2ebd3-244">Microsoft.Compute/imageVersion</span><span class="sxs-lookup"><span data-stu-id="2ebd3-244">Microsoft.Compute/imageVersion</span></span> | <span data-ttu-id="2ebd3-245">設定 hello hello 平台映像或 marketplace 映像使用新版 toocreate hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-245">Set hello version of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="2ebd3-246">Microsoft.Compute/licenseType</span><span class="sxs-lookup"><span data-stu-id="2ebd3-246">Microsoft.Compute/licenseType</span></span> | <span data-ttu-id="2ebd3-247">設定 hello 映像或磁碟為內部授權。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-247">Set that hello image or disk is licensed on-premises.</span></span> <span data-ttu-id="2ebd3-248">這個值只用於包含 hello Windows 伺服器作業系統映像。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-248">This value is only used for images that contain hello Windows Server operating system.</span></span>  |
| <span data-ttu-id="2ebd3-249">Microsoft.Compute/virtualMachines/imageOffer</span><span class="sxs-lookup"><span data-stu-id="2ebd3-249">Microsoft.Compute/virtualMachines/imageOffer</span></span> | <span data-ttu-id="2ebd3-250">Hello 平台映像或 marketplace 映像組 hello 優惠 toocreate hello 虛擬機器的使用。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-250">Set hello offer of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="2ebd3-251">Microsoft.Compute/virtualMachines/imagePublisher</span><span class="sxs-lookup"><span data-stu-id="2ebd3-251">Microsoft.Compute/virtualMachines/imagePublisher</span></span> | <span data-ttu-id="2ebd3-252">Hello 平台映像或 marketplace 映像組 hello 發行者使用 toocreate hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-252">Set hello publisher of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="2ebd3-253">Microsoft.Compute/virtualMachines/imageSku</span><span class="sxs-lookup"><span data-stu-id="2ebd3-253">Microsoft.Compute/virtualMachines/imageSku</span></span> | <span data-ttu-id="2ebd3-254">設定 hello hello 平台映像或 marketplace 映像的 SKU toocreate hello 虛擬機器的使用。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-254">Set hello SKU of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="2ebd3-255">Microsoft.Compute/virtualMachines/imageVersion</span><span class="sxs-lookup"><span data-stu-id="2ebd3-255">Microsoft.Compute/virtualMachines/imageVersion</span></span> | <span data-ttu-id="2ebd3-256">設定 hello hello 平台映像或 marketplace 映像使用新版 toocreate hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-256">Set hello version of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="2ebd3-257">Microsoft.Compute/virtualMachines/osDisk.Uri</span><span class="sxs-lookup"><span data-stu-id="2ebd3-257">Microsoft.Compute/virtualMachines/osDisk.Uri</span></span> | <span data-ttu-id="2ebd3-258">設定 hello vhd URI。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-258">Set hello vhd URI.</span></span> |
| <span data-ttu-id="2ebd3-259">Microsoft.Compute/virtualMachines/sku.name</span><span class="sxs-lookup"><span data-stu-id="2ebd3-259">Microsoft.Compute/virtualMachines/sku.name</span></span> | <span data-ttu-id="2ebd3-260">設定 hello hello 虛擬機器大小。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-260">Set hello size of hello virtual machine.</span></span> |

<span data-ttu-id="2ebd3-261">**Microsoft.Compute/virtualMachines/extensions**</span><span class="sxs-lookup"><span data-stu-id="2ebd3-261">**Microsoft.Compute/virtualMachines/extensions**</span></span>

| <span data-ttu-id="2ebd3-262">Alias</span><span class="sxs-lookup"><span data-stu-id="2ebd3-262">Alias</span></span> | <span data-ttu-id="2ebd3-263">說明</span><span class="sxs-lookup"><span data-stu-id="2ebd3-263">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="2ebd3-264">Microsoft.Compute/virtualMachines/extensions/publisher</span><span class="sxs-lookup"><span data-stu-id="2ebd3-264">Microsoft.Compute/virtualMachines/extensions/publisher</span></span> | <span data-ttu-id="2ebd3-265">設定 hello hello 擴充功能的發行者名稱。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-265">Set hello name of hello extension’s publisher.</span></span> |
| <span data-ttu-id="2ebd3-266">Microsoft.Compute/virtualMachines/extensions/type</span><span class="sxs-lookup"><span data-stu-id="2ebd3-266">Microsoft.Compute/virtualMachines/extensions/type</span></span> | <span data-ttu-id="2ebd3-267">設定延伸 hello 型別。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-267">Set hello type of extension.</span></span> |
| <span data-ttu-id="2ebd3-268">Microsoft.Compute/virtualMachines/extensions/typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="2ebd3-268">Microsoft.Compute/virtualMachines/extensions/typeHandlerVersion</span></span> | <span data-ttu-id="2ebd3-269">設定 hello hello 擴充功能版本。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-269">Set hello version of hello extension.</span></span> |

<span data-ttu-id="2ebd3-270">**Microsoft.Compute/virtualMachineScaleSets**</span><span class="sxs-lookup"><span data-stu-id="2ebd3-270">**Microsoft.Compute/virtualMachineScaleSets**</span></span>

| <span data-ttu-id="2ebd3-271">Alias</span><span class="sxs-lookup"><span data-stu-id="2ebd3-271">Alias</span></span> | <span data-ttu-id="2ebd3-272">說明</span><span class="sxs-lookup"><span data-stu-id="2ebd3-272">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="2ebd3-273">Microsoft.Compute/imageId</span><span class="sxs-lookup"><span data-stu-id="2ebd3-273">Microsoft.Compute/imageId</span></span> | <span data-ttu-id="2ebd3-274">設定 hello hello 用映像 toocreate hello 虛擬機器的識別項。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-274">Set hello identifier of hello image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="2ebd3-275">Microsoft.Compute/imageOffer</span><span class="sxs-lookup"><span data-stu-id="2ebd3-275">Microsoft.Compute/imageOffer</span></span> | <span data-ttu-id="2ebd3-276">Hello 平台映像或 marketplace 映像組 hello 優惠 toocreate hello 虛擬機器的使用。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-276">Set hello offer of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="2ebd3-277">Microsoft.Compute/imagePublisher</span><span class="sxs-lookup"><span data-stu-id="2ebd3-277">Microsoft.Compute/imagePublisher</span></span> | <span data-ttu-id="2ebd3-278">Hello 平台映像或 marketplace 映像組 hello 發行者使用 toocreate hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-278">Set hello publisher of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="2ebd3-279">Microsoft.Compute/imageSku</span><span class="sxs-lookup"><span data-stu-id="2ebd3-279">Microsoft.Compute/imageSku</span></span> | <span data-ttu-id="2ebd3-280">設定 hello hello 平台映像或 marketplace 映像的 SKU toocreate hello 虛擬機器的使用。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-280">Set hello SKU of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="2ebd3-281">Microsoft.Compute/imageVersion</span><span class="sxs-lookup"><span data-stu-id="2ebd3-281">Microsoft.Compute/imageVersion</span></span> | <span data-ttu-id="2ebd3-282">設定 hello hello 平台映像或 marketplace 映像使用新版 toocreate hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-282">Set hello version of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="2ebd3-283">Microsoft.Compute/licenseType</span><span class="sxs-lookup"><span data-stu-id="2ebd3-283">Microsoft.Compute/licenseType</span></span> | <span data-ttu-id="2ebd3-284">設定 hello 映像或磁碟為內部授權。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-284">Set that hello image or disk is licensed on-premises.</span></span> <span data-ttu-id="2ebd3-285">這個值只用於包含 hello Windows 伺服器作業系統映像。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-285">This value is only used for images that contain hello Windows Server operating system.</span></span> |
| <span data-ttu-id="2ebd3-286">Microsoft.Compute/VirtualMachineScaleSets/computerNamePrefix</span><span class="sxs-lookup"><span data-stu-id="2ebd3-286">Microsoft.Compute/VirtualMachineScaleSets/computerNamePrefix</span></span> | <span data-ttu-id="2ebd3-287">Hello 規模集中設定 hello hello 的所有虛擬機器的電腦名稱前置詞。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-287">Set hello computer name prefix for all  hello virtual machines in hello scale set.</span></span> |
| <span data-ttu-id="2ebd3-288">Microsoft.Compute/VirtualMachineScaleSets/osdisk.imageUrl</span><span class="sxs-lookup"><span data-stu-id="2ebd3-288">Microsoft.Compute/VirtualMachineScaleSets/osdisk.imageUrl</span></span> | <span data-ttu-id="2ebd3-289">設定使用者映像的 hello blob URI。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-289">Set hello blob URI for user image.</span></span> |
| <span data-ttu-id="2ebd3-290">Microsoft.Compute/VirtualMachineScaleSets/osdisk.vhdContainers</span><span class="sxs-lookup"><span data-stu-id="2ebd3-290">Microsoft.Compute/VirtualMachineScaleSets/osdisk.vhdContainers</span></span> | <span data-ttu-id="2ebd3-291">設定使用的 toostore hello 擴展集的作業系統磁碟的 hello 容器 Url。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-291">Set hello container URLs that are used toostore operating system disks for hello scale set.</span></span> |
| <span data-ttu-id="2ebd3-292">Microsoft.Compute/VirtualMachineScaleSets/sku.name</span><span class="sxs-lookup"><span data-stu-id="2ebd3-292">Microsoft.Compute/VirtualMachineScaleSets/sku.name</span></span> | <span data-ttu-id="2ebd3-293">設定 hello 大小的虛擬機器規模集中的。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-293">Set hello size of virtual machines in a scale set.</span></span> |
| <span data-ttu-id="2ebd3-294">Microsoft.Compute/VirtualMachineScaleSets/sku.tier</span><span class="sxs-lookup"><span data-stu-id="2ebd3-294">Microsoft.Compute/VirtualMachineScaleSets/sku.tier</span></span> | <span data-ttu-id="2ebd3-295">設定虛擬機器規模集中的 hello 層。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-295">Set hello tier of virtual machines in a scale set.</span></span> |
  
<span data-ttu-id="2ebd3-296">**Microsoft.Network/applicationGateways**</span><span class="sxs-lookup"><span data-stu-id="2ebd3-296">**Microsoft.Network/applicationGateways**</span></span>

| <span data-ttu-id="2ebd3-297">Alias</span><span class="sxs-lookup"><span data-stu-id="2ebd3-297">Alias</span></span> | <span data-ttu-id="2ebd3-298">說明</span><span class="sxs-lookup"><span data-stu-id="2ebd3-298">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="2ebd3-299">Microsoft.Network/applicationGateways/sku.name</span><span class="sxs-lookup"><span data-stu-id="2ebd3-299">Microsoft.Network/applicationGateways/sku.name</span></span> | <span data-ttu-id="2ebd3-300">設定的 hello 閘道的 hello 大小。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-300">Set hello size of hello gateway.</span></span> |

<span data-ttu-id="2ebd3-301">**Microsoft.Network/virtualNetworkGateways**</span><span class="sxs-lookup"><span data-stu-id="2ebd3-301">**Microsoft.Network/virtualNetworkGateways**</span></span>

| <span data-ttu-id="2ebd3-302">Alias</span><span class="sxs-lookup"><span data-stu-id="2ebd3-302">Alias</span></span> | <span data-ttu-id="2ebd3-303">說明</span><span class="sxs-lookup"><span data-stu-id="2ebd3-303">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="2ebd3-304">Microsoft.Network/virtualNetworkGateways/gatewayType</span><span class="sxs-lookup"><span data-stu-id="2ebd3-304">Microsoft.Network/virtualNetworkGateways/gatewayType</span></span> | <span data-ttu-id="2ebd3-305">將此虛擬網路閘道 hello 類型的設定。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-305">Set hello type of this virtual network gateway.</span></span> |
| <span data-ttu-id="2ebd3-306">Microsoft.Network/virtualNetworkGateways/sku.name</span><span class="sxs-lookup"><span data-stu-id="2ebd3-306">Microsoft.Network/virtualNetworkGateways/sku.name</span></span> | <span data-ttu-id="2ebd3-307">設定 hello 閘道 SKU 的名稱。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-307">Set hello gateway SKU name.</span></span> |

<span data-ttu-id="2ebd3-308">**Microsoft.Sql/servers**</span><span class="sxs-lookup"><span data-stu-id="2ebd3-308">**Microsoft.Sql/servers**</span></span>

| <span data-ttu-id="2ebd3-309">Alias</span><span class="sxs-lookup"><span data-stu-id="2ebd3-309">Alias</span></span> | <span data-ttu-id="2ebd3-310">說明</span><span class="sxs-lookup"><span data-stu-id="2ebd3-310">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="2ebd3-311">Microsoft.Sql/servers/version</span><span class="sxs-lookup"><span data-stu-id="2ebd3-311">Microsoft.Sql/servers/version</span></span> | <span data-ttu-id="2ebd3-312">設定 hello hello 伺服器版本。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-312">Set hello version of hello server.</span></span> |

<span data-ttu-id="2ebd3-313">**Microsoft.Sql/databases**</span><span class="sxs-lookup"><span data-stu-id="2ebd3-313">**Microsoft.Sql/databases**</span></span>

| <span data-ttu-id="2ebd3-314">Alias</span><span class="sxs-lookup"><span data-stu-id="2ebd3-314">Alias</span></span> | <span data-ttu-id="2ebd3-315">說明</span><span class="sxs-lookup"><span data-stu-id="2ebd3-315">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="2ebd3-316">Microsoft.Sql/servers/databases/edition</span><span class="sxs-lookup"><span data-stu-id="2ebd3-316">Microsoft.Sql/servers/databases/edition</span></span> | <span data-ttu-id="2ebd3-317">設定 hello hello 資料庫版本。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-317">Set hello edition of hello database.</span></span> |
| <span data-ttu-id="2ebd3-318">Microsoft.Sql/servers/databases/elasticPoolName</span><span class="sxs-lookup"><span data-stu-id="2ebd3-318">Microsoft.Sql/servers/databases/elasticPoolName</span></span> | <span data-ttu-id="2ebd3-319">」 組 hello hello 彈性集區 hello 資料庫名稱。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-319">Set hello name of hello elastic pool hello database is in.</span></span> |
| <span data-ttu-id="2ebd3-320">Microsoft.Sql/servers/databases/requestedServiceObjectiveId</span><span class="sxs-lookup"><span data-stu-id="2ebd3-320">Microsoft.Sql/servers/databases/requestedServiceObjectiveId</span></span> | <span data-ttu-id="2ebd3-321">設定 hello 設定層級的服務目標識別碼 hello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-321">Set hello configured service level objective ID of hello database.</span></span> |
| <span data-ttu-id="2ebd3-322">Microsoft.Sql/servers/databases/requestedServiceObjectiveName</span><span class="sxs-lookup"><span data-stu-id="2ebd3-322">Microsoft.Sql/servers/databases/requestedServiceObjectiveName</span></span> | <span data-ttu-id="2ebd3-323">Hello hello 設定 hello 資料庫的服務等級目標名稱設定。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-323">Set hello name of hello configured service level objective of hello database.</span></span>  |

<span data-ttu-id="2ebd3-324">**Microsoft.Sql/elasticpools**</span><span class="sxs-lookup"><span data-stu-id="2ebd3-324">**Microsoft.Sql/elasticpools**</span></span>

| <span data-ttu-id="2ebd3-325">Alias</span><span class="sxs-lookup"><span data-stu-id="2ebd3-325">Alias</span></span> | <span data-ttu-id="2ebd3-326">說明</span><span class="sxs-lookup"><span data-stu-id="2ebd3-326">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="2ebd3-327">servers/elasticpools</span><span class="sxs-lookup"><span data-stu-id="2ebd3-327">servers/elasticpools</span></span> | <span data-ttu-id="2ebd3-328">Microsoft.Sql/servers/elasticPools/dtu</span><span class="sxs-lookup"><span data-stu-id="2ebd3-328">Microsoft.Sql/servers/elasticPools/dtu</span></span> | <span data-ttu-id="2ebd3-329">設定 hello 總計共用 hello 資料庫彈性集區 DTU。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-329">Set hello total shared DTU for hello database elastic pool.</span></span> |
| <span data-ttu-id="2ebd3-330">servers/elasticpools</span><span class="sxs-lookup"><span data-stu-id="2ebd3-330">servers/elasticpools</span></span> | <span data-ttu-id="2ebd3-331">Microsoft.Sql/servers/elasticPools/edition</span><span class="sxs-lookup"><span data-stu-id="2ebd3-331">Microsoft.Sql/servers/elasticPools/edition</span></span> | <span data-ttu-id="2ebd3-332">將 hello edition hello 彈性集區的設定。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-332">Set hello edition of hello elastic pool.</span></span> |

<span data-ttu-id="2ebd3-333">**Microsoft.Storage/storageAccounts**</span><span class="sxs-lookup"><span data-stu-id="2ebd3-333">**Microsoft.Storage/storageAccounts**</span></span>

| <span data-ttu-id="2ebd3-334">Alias</span><span class="sxs-lookup"><span data-stu-id="2ebd3-334">Alias</span></span> | <span data-ttu-id="2ebd3-335">說明</span><span class="sxs-lookup"><span data-stu-id="2ebd3-335">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="2ebd3-336">Microsoft.Storage/storageAccounts/accessTier</span><span class="sxs-lookup"><span data-stu-id="2ebd3-336">Microsoft.Storage/storageAccounts/accessTier</span></span> | <span data-ttu-id="2ebd3-337">設定用於計費 hello 存取層。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-337">Set hello access tier used for billing.</span></span> |
| <span data-ttu-id="2ebd3-338">Microsoft.Storage/storageAccounts/accountType</span><span class="sxs-lookup"><span data-stu-id="2ebd3-338">Microsoft.Storage/storageAccounts/accountType</span></span> | <span data-ttu-id="2ebd3-339">設定 hello SKU 的名稱。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-339">Set hello SKU name.</span></span> |
| <span data-ttu-id="2ebd3-340">Microsoft.Storage/storageAccounts/enableBlobEncryption</span><span class="sxs-lookup"><span data-stu-id="2ebd3-340">Microsoft.Storage/storageAccounts/enableBlobEncryption</span></span> | <span data-ttu-id="2ebd3-341">設定是否 hello 服務加密 hello 資料會儲存在 hello blob 儲存體服務。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-341">Set whether hello service encrypts hello data as it is stored in hello blob storage service.</span></span> |
| <span data-ttu-id="2ebd3-342">Microsoft.Storage/storageAccounts/enableFileEncryption</span><span class="sxs-lookup"><span data-stu-id="2ebd3-342">Microsoft.Storage/storageAccounts/enableFileEncryption</span></span> | <span data-ttu-id="2ebd3-343">設定是否 hello 服務加密 hello 資料儲存在 hello 檔案儲存體服務。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-343">Set whether hello service encrypts hello data as it is stored in hello file storage service.</span></span> |
| <span data-ttu-id="2ebd3-344">Microsoft.Storage/storageAccounts/sku.name</span><span class="sxs-lookup"><span data-stu-id="2ebd3-344">Microsoft.Storage/storageAccounts/sku.name</span></span> | <span data-ttu-id="2ebd3-345">設定 hello SKU 的名稱。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-345">Set hello SKU name.</span></span> |
| <span data-ttu-id="2ebd3-346">Microsoft.Storage/storageAccounts/supportsHttpsTrafficOnly</span><span class="sxs-lookup"><span data-stu-id="2ebd3-346">Microsoft.Storage/storageAccounts/supportsHttpsTrafficOnly</span></span> | <span data-ttu-id="2ebd3-347">設定 tooallow 只有 https 流量 toostorage 服務。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-347">Set tooallow only https traffic toostorage service.</span></span> |


## <a name="policy-examples"></a><span data-ttu-id="2ebd3-348">原則範例</span><span class="sxs-lookup"><span data-stu-id="2ebd3-348">Policy examples</span></span>

<span data-ttu-id="2ebd3-349">下列主題中的 hello 包含原則範例：</span><span class="sxs-lookup"><span data-stu-id="2ebd3-349">hello following topics contain policy examples:</span></span>

* <span data-ttu-id="2ebd3-350">如需標籤原則的範例，請參閱[套用標籤的資源原則](resource-manager-policy-tags.md)。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-350">For examples of tag polices, see [Apply resource policies for tags](resource-manager-policy-tags.md).</span></span>
* <span data-ttu-id="2ebd3-351">如需命名和文字模式的範例，請參閱[為名稱和文字套用資源原則](resource-manager-policy-naming-convention.md)。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-351">For examples of naming and text patterns, see [Apply resource policies for names and text](resource-manager-policy-naming-convention.md).</span></span>
* <span data-ttu-id="2ebd3-352">儲存原則的範例，請參閱[套用資源原則 toostorage 帳戶](resource-manager-policy-storage.md)。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-352">For examples of storage policies, see [Apply resource policies toostorage accounts](resource-manager-policy-storage.md).</span></span>
* <span data-ttu-id="2ebd3-353">虛擬機器原則的範例，請參閱[套用資源原則 tooLinux Vm](../virtual-machines/linux/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json)和[套用資源原則 tooWindows Vm](../virtual-machines/windows/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="2ebd3-353">For examples of virtual machine policies, see [Apply resource policies tooLinux VMs](../virtual-machines/linux/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json) and [Apply resource policies tooWindows VMs](../virtual-machines/windows/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json)</span></span>


## <a name="next-steps"></a><span data-ttu-id="2ebd3-354">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2ebd3-354">Next steps</span></span>
* <span data-ttu-id="2ebd3-355">定義原則規則之後, 將它指派 tooa 範圍。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-355">After defining a policy rule, assign it tooa scope.</span></span> <span data-ttu-id="2ebd3-356">tooassign 原則透過 hello 入口網站，請參閱[使用 Azure 入口網站 tooassign 和管理資源原則](resource-manager-policy-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-356">tooassign policies through hello portal, see [Use Azure portal tooassign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="2ebd3-357">tooassign 原則透過 REST API、 PowerShell 或 Azure CLI，請參閱[指派及管理透過指令碼的原則](resource-manager-policy-create-assign.md)。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-357">tooassign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span>
* <span data-ttu-id="2ebd3-358">如需指引企業可以如何使用資源管理員 tooeffectively 管理訂用帳戶，請參閱[Azure 企業版 scaffold-精準的訂閱控管](resource-manager-subscription-governance.md)。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-358">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>
* <span data-ttu-id="2ebd3-359">發行位置 hello 原則結構描述是在[http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json)。</span><span class="sxs-lookup"><span data-stu-id="2ebd3-359">hello policy schema is published at [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json).</span></span> 

