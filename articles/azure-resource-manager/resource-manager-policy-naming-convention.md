---
title: "如需命名慣例 aaaAzure 資源原則 |Microsoft 文件"
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
ms.openlocfilehash: c8384b231263fb694aed8b936a953d5c0ca31e71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="apply-resource-policies-for-names-and-text"></a><span data-ttu-id="8d425-103">為名稱和文字套用資源原則</span><span class="sxs-lookup"><span data-stu-id="8d425-103">Apply resource policies for names and text</span></span>
<span data-ttu-id="8d425-104">本主題說明數個[資源原則](resource-manager-policy.md)可以套用 tooestablish 命名和文字的慣例。</span><span class="sxs-lookup"><span data-stu-id="8d425-104">This topic shows several [resource policies](resource-manager-policy.md) you can apply tooestablish naming and text conventions.</span></span> <span data-ttu-id="8d425-105">這些原則可確保資源名稱和標籤值的一致性。</span><span class="sxs-lookup"><span data-stu-id="8d425-105">These policies ensure consistency for resource names and tag values.</span></span> 

## <a name="set-naming-convention-with-wildcard"></a><span data-ttu-id="8d425-106">使用萬用字元設定命名慣例</span><span class="sxs-lookup"><span data-stu-id="8d425-106">Set naming convention with wildcard</span></span>
<span data-ttu-id="8d425-107">hello 下列範例顯示 hello 的使用萬用字元，這會受到 hello**像**條件。</span><span class="sxs-lookup"><span data-stu-id="8d425-107">hello following example shows hello use of wildcard, which is supported by hello **like** condition.</span></span> <span data-ttu-id="8d425-108">hello 條件狀態，是否 hello 名稱相符 hello 提及的模式 (namePrefix\*nameSuffix) 然後拒絕 hello 要求：</span><span class="sxs-lookup"><span data-stu-id="8d425-108">hello condition states that if hello name does match hello mentioned pattern (namePrefix\*nameSuffix) then deny hello request:</span></span>

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

## <a name="set-naming-convention-with-pattern"></a><span data-ttu-id="8d425-109">使用模式設定命名慣例</span><span class="sxs-lookup"><span data-stu-id="8d425-109">Set naming convention with pattern</span></span>

<span data-ttu-id="8d425-110">資源名稱比對模式中，使用 hello toospecify 符合條件。</span><span class="sxs-lookup"><span data-stu-id="8d425-110">toospecify that resource names match a pattern, use hello match condition.</span></span> <span data-ttu-id="8d425-111">hello 下列範例要求與名稱 toostart`contoso`而且包含六個其他字母：</span><span class="sxs-lookup"><span data-stu-id="8d425-111">hello following example requires names toostart with `contoso` and contain six additional letters:</span></span>

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

## <a name="set-date-pattern-for-tag-value"></a><span data-ttu-id="8d425-112">設定標籤值的日期模式</span><span class="sxs-lookup"><span data-stu-id="8d425-112">Set date pattern for tag value</span></span>

<span data-ttu-id="8d425-113">toorequire 日期圖樣的兩個數字字元、 虛線、 三個字母、 虛線和四位數，使用：</span><span class="sxs-lookup"><span data-stu-id="8d425-113">toorequire a date pattern of two digits, dash, three letters, dash, and four digits, use:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="8d425-114">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8d425-114">Next steps</span></span>
* <span data-ttu-id="8d425-115">定義原則規則 （如 hello 前面範例所示） 之後, 您會需要 toocreate hello 原則定義，並將它指派 tooa 範圍。</span><span class="sxs-lookup"><span data-stu-id="8d425-115">After defining a policy rule (as shown in hello preceding examples), you need toocreate hello policy definition and assign it tooa scope.</span></span> <span data-ttu-id="8d425-116">hello 領域可以訂用帳戶、 資源群組或資源。</span><span class="sxs-lookup"><span data-stu-id="8d425-116">hello scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="8d425-117">tooassign 原則透過 hello 入口網站，請參閱[使用 Azure 入口網站 tooassign 和管理資源原則](resource-manager-policy-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="8d425-117">tooassign policies through hello portal, see [Use Azure portal tooassign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="8d425-118">tooassign 原則透過 REST API、 PowerShell 或 Azure CLI，請參閱[指派及管理透過指令碼的原則](resource-manager-policy-create-assign.md)。</span><span class="sxs-lookup"><span data-stu-id="8d425-118">tooassign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span> 
* <span data-ttu-id="8d425-119">如需指引企業可以如何使用資源管理員 tooeffectively 管理訂用帳戶，請參閱[Azure 企業版 scaffold-精準的訂閱控管](resource-manager-subscription-governance.md)。</span><span class="sxs-lookup"><span data-stu-id="8d425-119">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

