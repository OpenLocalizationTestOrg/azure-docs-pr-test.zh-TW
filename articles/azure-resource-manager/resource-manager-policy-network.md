---
title: "網路資源的 Azure 資源原則 | Microsoft Docs"
description: "描述管理網路資源部署的 Azure Resource Manager 原則。"
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
ms.date: 07/05/2017
ms.author: tomfitz
ms.openlocfilehash: bca66bbdd9da9b3e4099d0d961f42c9368a17f5e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="apply-resource-policies-to-network-resources"></a><span data-ttu-id="fb3f2-103">將資源原則套用至網路資源</span><span class="sxs-lookup"><span data-stu-id="fb3f2-103">Apply resource policies to network resources</span></span>
<span data-ttu-id="fb3f2-104">本文示範可套用到 Azure 虛擬網路閘道的[資源原則](resource-manager-policy.md)範例。</span><span class="sxs-lookup"><span data-stu-id="fb3f2-104">This article shows an example [resource policy](resource-manager-policy.md) you can apply to Azure virtual network gateways.</span></span> <span data-ttu-id="fb3f2-105">此原則可確保在組織中所部署閘道的一致性。</span><span class="sxs-lookup"><span data-stu-id="fb3f2-105">This policy ensures consistency for gateways deployed in your organization.</span></span> 

## <a name="define-permitted-virtual-network-gateway-sku"></a><span data-ttu-id="fb3f2-106">定義允許的虛擬網路閘道 SKU</span><span class="sxs-lookup"><span data-stu-id="fb3f2-106">Define permitted virtual network gateway SKU</span></span>

<span data-ttu-id="fb3f2-107">下列原則會限制可針對虛擬網路閘道部署的 SKU：</span><span class="sxs-lookup"><span data-stu-id="fb3f2-107">The following policy restricts which SKUs can be deployed for virtual network gateways:</span></span>

```json
{
  "if": {
    "allOf": [
      {
        "field": "type",
        "equals": "Microsoft.Network/virtualNetworkGateways"
      },
      {
        "not": {
          "field": "Microsoft.Network/virtualNetworkGateways/sku.name",
          "in": [
            "Basic",
            "VpnGw1"
          ]
        }
      }
    ]
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="fb3f2-108">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fb3f2-108">Next steps</span></span>
* <span data-ttu-id="fb3f2-109">定義原則規則 (如上述範例所示) 之後，您必須建立原則定義，並將它指派到某個範圍。</span><span class="sxs-lookup"><span data-stu-id="fb3f2-109">After defining a policy rule (as shown in the preceding examples), you need to create the policy definition and assign it to a scope.</span></span> <span data-ttu-id="fb3f2-110">範圍可以是訂用帳戶、資源群組或資源。</span><span class="sxs-lookup"><span data-stu-id="fb3f2-110">The scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="fb3f2-111">若要透過入口網站來指派原則，請參閱[使用 Azure 入口網站來指派和管理資源原則](resource-manager-policy-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="fb3f2-111">To assign policies through the portal, see [Use Azure portal to assign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="fb3f2-112">若要透過 REST API、PowerShell 或 Azure CLI 來指派原則，請參閱[透過指令碼來指派和管理原則](resource-manager-policy-create-assign.md)。</span><span class="sxs-lookup"><span data-stu-id="fb3f2-112">To assign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span> 
* <span data-ttu-id="fb3f2-113">如需關於企業如何使用 Resource Manager 有效地管理訂閱的指引，請參閱 [Azure 企業 Scaffold - 規定的訂用帳戶治理](resource-manager-subscription-governance.md)。</span><span class="sxs-lookup"><span data-stu-id="fb3f2-113">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

