---
title: "標籤的 Azure 資源原則 | Microsoft Docs"
description: "提供在資源上管理標籤之資源原則的範例"
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
ms.date: 08/24/2017
ms.author: tomfitz
ms.openlocfilehash: 469bd8d637337e5900ea84c6bfaf88064695fb7e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="apply-resource-policies-for-tags"></a><span data-ttu-id="0ffad-103">套用標籤的資源原則</span><span class="sxs-lookup"><span data-stu-id="0ffad-103">Apply resource policies for tags</span></span>

<span data-ttu-id="0ffad-104">本主題提供可套用以確保一致地在資源上使用標籤的通用原則規則。</span><span class="sxs-lookup"><span data-stu-id="0ffad-104">This topic provides common policy rules you can apply to ensure consistent use of tags on resources.</span></span>

<span data-ttu-id="0ffad-105">使用現有的資源將標籤原則套用到資源群組或訂用帳戶不會追溯性地將原則套用到這些資源。</span><span class="sxs-lookup"><span data-stu-id="0ffad-105">Applying a tag policy to a resource group or subscription with existing resources does not retroactively apply the policy to those resources.</span></span> <span data-ttu-id="0ffad-106">若要在這些資源上強制執行原則，請觸發現有資源的更新。</span><span class="sxs-lookup"><span data-stu-id="0ffad-106">To enforce the policies on those resources, trigger an update to the existing resources.</span></span> <span data-ttu-id="0ffad-107">本文包含觸發更新的 PowerShell 範例。</span><span class="sxs-lookup"><span data-stu-id="0ffad-107">This article includes a PowerShell example for triggering an update.</span></span>

## <a name="ensure-all-resources-in-a-resource-group-have-a-tagvalue"></a><span data-ttu-id="0ffad-108">請確定資源群組中的所有資源都有標籤/值</span><span class="sxs-lookup"><span data-stu-id="0ffad-108">Ensure all resources in a resource group have a tag/value</span></span>

<span data-ttu-id="0ffad-109">常見的需求是資源群組中的所有資源都有特定的標籤和值。</span><span class="sxs-lookup"><span data-stu-id="0ffad-109">A common requirement is that all resources in a resource group have a particular tag and value.</span></span> <span data-ttu-id="0ffad-110">通常需要這項需求來依部門追蹤成本。</span><span class="sxs-lookup"><span data-stu-id="0ffad-110">This requirement is often needed to track costs by department.</span></span> <span data-ttu-id="0ffad-111">必須符合下列條件：</span><span class="sxs-lookup"><span data-stu-id="0ffad-111">The following conditions must be met:</span></span>

* <span data-ttu-id="0ffad-112">必要的標籤和值會附加至沒有任何標籤的新增和更新的資源。</span><span class="sxs-lookup"><span data-stu-id="0ffad-112">The required tag and value are appended to new and updated resources that do not have the tag.</span></span>
* <span data-ttu-id="0ffad-113">無法從任何現有的資源移除必要的標籤和值。</span><span class="sxs-lookup"><span data-stu-id="0ffad-113">The required tag and value cannot be removed from any existing resources.</span></span>

<span data-ttu-id="0ffad-114">將下列兩個內建原則套用至資源群組來完成這項需求。</span><span class="sxs-lookup"><span data-stu-id="0ffad-114">You accomplish this requirement by applying two built-in policies to a resource group.</span></span>

| <span data-ttu-id="0ffad-115">ID</span><span class="sxs-lookup"><span data-stu-id="0ffad-115">ID</span></span> | <span data-ttu-id="0ffad-116">說明</span><span class="sxs-lookup"><span data-stu-id="0ffad-116">Description</span></span> |
| ---- | ---- |
| <span data-ttu-id="0ffad-117">2a0e14a6-b0a6-4fab-991a-187a4f81c498</span><span class="sxs-lookup"><span data-stu-id="0ffad-117">2a0e14a6-b0a6-4fab-991a-187a4f81c498</span></span> | <span data-ttu-id="0ffad-118">使用者未指定時，套用必要的標籤和其預設值。</span><span class="sxs-lookup"><span data-stu-id="0ffad-118">Applies a required tag and its default value when it is not specified by the user.</span></span> |
| <span data-ttu-id="0ffad-119">1e30110a-5ceb-460c-a204-c1c3969c6d62</span><span class="sxs-lookup"><span data-stu-id="0ffad-119">1e30110a-5ceb-460c-a204-c1c3969c6d62</span></span> | <span data-ttu-id="0ffad-120">強制必要的標籤和其值。</span><span class="sxs-lookup"><span data-stu-id="0ffad-120">Enforces a required tag and its value.</span></span> |

### <a name="powershell"></a><span data-ttu-id="0ffad-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0ffad-121">PowerShell</span></span>

<span data-ttu-id="0ffad-122">下列 PowerShell 指令碼會將兩個內建的原則定義指派給資源群組。</span><span class="sxs-lookup"><span data-stu-id="0ffad-122">The following PowerShell script assigns the two built-in policy definitions to a resource group.</span></span> <span data-ttu-id="0ffad-123">執行指令碼之前，請將所有必要的標籤指派給資源群組。</span><span class="sxs-lookup"><span data-stu-id="0ffad-123">Before running the script, assign all required tags to the resource group.</span></span> <span data-ttu-id="0ffad-124">資源群組中每個標籤對群組中的資源而言都是必要的。</span><span class="sxs-lookup"><span data-stu-id="0ffad-124">Each tag on the resource group is required for the resources in the group.</span></span> <span data-ttu-id="0ffad-125">若要指派給您的訂用帳戶中的所有資源群組，取得資源群組時請勿提供 `-Name` 參數。</span><span class="sxs-lookup"><span data-stu-id="0ffad-125">To assign to all resource groups in your subscription, do not provide the `-Name` parameter when getting the resource groups.</span></span>

```powershell
$appendpolicy = Get-AzureRmPolicyDefinition | Where-Object {$_.Name -eq '2a0e14a6-b0a6-4fab-991a-187a4f81c498'}
$denypolicy = Get-AzureRmPolicyDefinition | Where-Object {$_.Name -eq '1e30110a-5ceb-460c-a204-c1c3969c6d62'}

$rgs = Get-AzureRMResourceGroup -Name ExampleGroup

foreach($rg in $rgs)
{
    $tags = $rg.Tags
    foreach($key in $tags.Keys){
        $key 
        $tags[$key]
        New-AzureRmPolicyAssignment -Name ("append"+$key+"tag") -PolicyDefinition $appendpolicy -Scope $rg.ResourceId -tagName $key -tagValue  $tags[$key]
        New-AzureRmPolicyAssignment -Name ("denywithout"+$key+"tag") -PolicyDefinition $denypolicy -Scope $rg.ResourceId -tagName $key -tagValue  $tags[$key]
    }
}
```

<span data-ttu-id="0ffad-126">在指派原則之後，您可以對所有現有的資源觸發更新，以強制您加入的標籤原則。</span><span class="sxs-lookup"><span data-stu-id="0ffad-126">After assigning the policies, you can trigger an update to all existing resources to enforce the tag policies you have added.</span></span> <span data-ttu-id="0ffad-127">下列指令碼會保留資源中現存的任何其他標籤︰</span><span class="sxs-lookup"><span data-stu-id="0ffad-127">The following script retains any other tags that existed on the resources:</span></span>

```powershell
$group = Get-AzureRmResourceGroup -Name "ExampleGroup" 

$resources = Find-AzureRmResource -ResourceGroupName $group.ResourceGroupName 

foreach($r in $resources)
{
    try{
        $r | Set-AzureRmResource -Tags ($a=if($r.Tags -eq $NULL) { @{}} else {$r.Tags}) -Force -UsePatchSemantics
    }
    catch{
        Write-Host  $r.ResourceId + "can't be updated"
    }
}
```

## <a name="require-tags-for-a-resource-type"></a><span data-ttu-id="0ffad-128">需要資源類型的標籤</span><span class="sxs-lookup"><span data-stu-id="0ffad-128">Require tags for a resource type</span></span>
<span data-ttu-id="0ffad-129">下列範例說明如何建立巢狀邏輯運算子，只為指定的資源類型 (在此案例中為儲存體帳戶) 要求應用程式標籤。</span><span class="sxs-lookup"><span data-stu-id="0ffad-129">The following example shows how to nest logical operators to require an application tag for only a specified resource type (in this case, storage accounts).</span></span>

```json
{
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
    "then": {
        "effect": "audit"
    }
}
```

## <a name="require-tag"></a><span data-ttu-id="0ffad-130">需要標籤</span><span class="sxs-lookup"><span data-stu-id="0ffad-130">Require tag</span></span>
<span data-ttu-id="0ffad-131">下列原則會拒絕沒有包含 "costCenter" 索引鍵標籤的要求 (可套用任何值)：</span><span class="sxs-lookup"><span data-stu-id="0ffad-131">The following policy denies requests that don't have a tag containing "costCenter" key (any value can be applied):</span></span>

```json
{
  "if": {
    "not" : {
      "field" : "tags",
      "containsKey" : "costCenter"
    }
  },
  "then" : {
    "effect" : "deny"
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="0ffad-132">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0ffad-132">Next steps</span></span>
* <span data-ttu-id="0ffad-133">定義原則規則 (如上述範例所示) 之後，您必須建立原則定義，並將它指派到某個範圍。</span><span class="sxs-lookup"><span data-stu-id="0ffad-133">After defining a policy rule (as shown in the preceding examples), you need to create the policy definition and assign it to a scope.</span></span> <span data-ttu-id="0ffad-134">範圍可以是訂用帳戶、資源群組或資源。</span><span class="sxs-lookup"><span data-stu-id="0ffad-134">The scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="0ffad-135">若要透過入口網站來指派原則，請參閱[使用 Azure 入口網站來指派和管理資源原則](resource-manager-policy-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="0ffad-135">To assign policies through the portal, see [Use Azure portal to assign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="0ffad-136">若要透過 REST API、PowerShell 或 Azure CLI 來指派原則，請參閱[透過指令碼來指派和管理原則](resource-manager-policy-create-assign.md)。</span><span class="sxs-lookup"><span data-stu-id="0ffad-136">To assign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span>
* <span data-ttu-id="0ffad-137">如需資源原則的簡介，請參閱[資源原則概觀](resource-manager-policy.md)。</span><span class="sxs-lookup"><span data-stu-id="0ffad-137">For an introduction to resource policies, see [Resource policy overview](resource-manager-policy.md).</span></span>
* <span data-ttu-id="0ffad-138">如需關於企業如何使用 Resource Manager 有效地管理訂閱的指引，請參閱 [Azure 企業 Scaffold - 規定的訂用帳戶治理](resource-manager-subscription-governance.md)。</span><span class="sxs-lookup"><span data-stu-id="0ffad-138">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

