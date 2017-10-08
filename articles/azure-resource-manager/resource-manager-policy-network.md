---
title: "網路資源的 aaaAzure 資源原則 |Microsoft 文件"
description: "描述 Azure 資源管理員管理的網路資源的 hello 部署原則。"
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
ms.openlocfilehash: a6072c1c30db0a4e4a1cae04efc7828d14069709
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="apply-resource-policies-toonetwork-resources"></a><span data-ttu-id="7a57b-103">適用於資源原則 toonetwork 資源</span><span class="sxs-lookup"><span data-stu-id="7a57b-103">Apply resource policies toonetwork resources</span></span>
<span data-ttu-id="7a57b-104">本文示範[資源原則](resource-manager-policy.md)可以套用 tooAzure 虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="7a57b-104">This article shows an example [resource policy](resource-manager-policy.md) you can apply tooAzure virtual network gateways.</span></span> <span data-ttu-id="7a57b-105">此原則可確保在組織中所部署閘道的一致性。</span><span class="sxs-lookup"><span data-stu-id="7a57b-105">This policy ensures consistency for gateways deployed in your organization.</span></span> 

## <a name="define-permitted-virtual-network-gateway-sku"></a><span data-ttu-id="7a57b-106">定義允許的虛擬網路閘道 SKU</span><span class="sxs-lookup"><span data-stu-id="7a57b-106">Define permitted virtual network gateway SKU</span></span>

<span data-ttu-id="7a57b-107">hello 遵循原則會限制哪些 Sku 可以部署的虛擬網路閘道：</span><span class="sxs-lookup"><span data-stu-id="7a57b-107">hello following policy restricts which SKUs can be deployed for virtual network gateways:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="7a57b-108">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7a57b-108">Next steps</span></span>
* <span data-ttu-id="7a57b-109">定義原則規則 （如 hello 前面範例所示） 之後, 您會需要 toocreate hello 原則定義，並將它指派 tooa 範圍。</span><span class="sxs-lookup"><span data-stu-id="7a57b-109">After defining a policy rule (as shown in hello preceding examples), you need toocreate hello policy definition and assign it tooa scope.</span></span> <span data-ttu-id="7a57b-110">hello 領域可以訂用帳戶、 資源群組或資源。</span><span class="sxs-lookup"><span data-stu-id="7a57b-110">hello scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="7a57b-111">tooassign 原則透過 hello 入口網站，請參閱[使用 Azure 入口網站 tooassign 和管理資源原則](resource-manager-policy-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="7a57b-111">tooassign policies through hello portal, see [Use Azure portal tooassign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="7a57b-112">tooassign 原則透過 REST API、 PowerShell 或 Azure CLI，請參閱[指派及管理透過指令碼的原則](resource-manager-policy-create-assign.md)。</span><span class="sxs-lookup"><span data-stu-id="7a57b-112">tooassign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span> 
* <span data-ttu-id="7a57b-113">如需指引企業可以如何使用資源管理員 tooeffectively 管理訂用帳戶，請參閱[Azure 企業版 scaffold-精準的訂閱控管](resource-manager-subscription-governance.md)。</span><span class="sxs-lookup"><span data-stu-id="7a57b-113">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

