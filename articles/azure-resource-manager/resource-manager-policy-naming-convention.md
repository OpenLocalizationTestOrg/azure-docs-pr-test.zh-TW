---
title: "命名慣例的 Azure 資源原則 | Microsoft Docs"
description: "描述資源命名慣例的 Azure Resource Manager 原則。"
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
ms.date: 06/27/2017
ms.author: tomfitz
ms.openlocfilehash: 51b3519bbba8cb4c768bfdd7dadf92fced434f22
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="apply-resource-policies-for-names-and-text"></a><span data-ttu-id="bade2-103">為名稱和文字套用資源原則</span><span class="sxs-lookup"><span data-stu-id="bade2-103">Apply resource policies for names and text</span></span>
<span data-ttu-id="bade2-104">本主題將示範數個您可以套用的[資源原則](resource-manager-policy.md)，以建立名稱和文字慣例。</span><span class="sxs-lookup"><span data-stu-id="bade2-104">This topic shows several [resource policies](resource-manager-policy.md) you can apply to establish naming and text conventions.</span></span> <span data-ttu-id="bade2-105">這些原則可確保資源名稱和標籤值的一致性。</span><span class="sxs-lookup"><span data-stu-id="bade2-105">These policies ensure consistency for resource names and tag values.</span></span> 

## <a name="set-naming-convention-with-wildcard"></a><span data-ttu-id="bade2-106">使用萬用字元設定命名慣例</span><span class="sxs-lookup"><span data-stu-id="bade2-106">Set naming convention with wildcard</span></span>
<span data-ttu-id="bade2-107">下列範例示範如何使用 **like** 條件所支援的萬用字元。</span><span class="sxs-lookup"><span data-stu-id="bade2-107">The following example shows the use of wildcard, which is supported by the **like** condition.</span></span> <span data-ttu-id="bade2-108">條件指出如果名稱符合所述模式 (namePrefix\*nameSuffix)，則拒絕要求：</span><span class="sxs-lookup"><span data-stu-id="bade2-108">The condition states that if the name does match the mentioned pattern (namePrefix\*nameSuffix) then deny the request:</span></span>

```json
{
  "if": {
    "not": {
      "field": "name",
      "like": "namePrefix*nameSuffix"
    }
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="set-naming-convention-with-pattern"></a><span data-ttu-id="bade2-109">使用模式設定命名慣例</span><span class="sxs-lookup"><span data-stu-id="bade2-109">Set naming convention with pattern</span></span>

<span data-ttu-id="bade2-110">若要指定資源名稱符合模式，請使用符合條件。</span><span class="sxs-lookup"><span data-stu-id="bade2-110">To specify that resource names match a pattern, use the match condition.</span></span> <span data-ttu-id="bade2-111">下列範例需要以 `contoso` 為開頭，且包含六個額外字母的名稱︰</span><span class="sxs-lookup"><span data-stu-id="bade2-111">The following example requires names to start with `contoso` and contain six additional letters:</span></span>

```json
{
  "if": {
    "not": {
      "field": "name",
      "match": "contoso??????"
    }
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="set-date-pattern-for-tag-value"></a><span data-ttu-id="bade2-112">設定標籤值的日期模式</span><span class="sxs-lookup"><span data-stu-id="bade2-112">Set date pattern for tag value</span></span>

<span data-ttu-id="bade2-113">如需兩個數字、破折號、三個字母、破折號和四個數字的日期模式，請使用︰</span><span class="sxs-lookup"><span data-stu-id="bade2-113">To require a date pattern of two digits, dash, three letters, dash, and four digits, use:</span></span>

```json
{
  "if": {
    "field": "tags.date",
    "match": "##-???-####"
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="bade2-114">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bade2-114">Next steps</span></span>
* <span data-ttu-id="bade2-115">定義原則規則 (如上述範例所示) 之後，您必須建立原則定義，並將它指派到某個範圍。</span><span class="sxs-lookup"><span data-stu-id="bade2-115">After defining a policy rule (as shown in the preceding examples), you need to create the policy definition and assign it to a scope.</span></span> <span data-ttu-id="bade2-116">範圍可以是訂用帳戶、資源群組或資源。</span><span class="sxs-lookup"><span data-stu-id="bade2-116">The scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="bade2-117">若要透過入口網站來指派原則，請參閱[使用 Azure 入口網站來指派和管理資源原則](resource-manager-policy-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="bade2-117">To assign policies through the portal, see [Use Azure portal to assign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="bade2-118">若要透過 REST API、PowerShell 或 Azure CLI 來指派原則，請參閱[透過指令碼來指派和管理原則](resource-manager-policy-create-assign.md)。</span><span class="sxs-lookup"><span data-stu-id="bade2-118">To assign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span> 
* <span data-ttu-id="bade2-119">如需關於企業如何使用 Resource Manager 有效地管理訂閱的指引，請參閱 [Azure 企業 Scaffold - 規定的訂用帳戶治理](resource-manager-subscription-governance.md)。</span><span class="sxs-lookup"><span data-stu-id="bade2-119">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

