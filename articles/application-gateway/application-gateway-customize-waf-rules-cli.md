---
title: "在 Azure 應用程式閘道 Azure CLI 2.0 aaaCustomize web 應用程式防火牆規則 |Microsoft 文件"
description: "本文提供在應用程式閘道 toocustomize web 應用程式防火牆規則以 hello Azure CLI 2.0 方式的資訊。"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: 
ms.workload: infrastructure-services
ms.date: 07/26/2017
ms.author: gwallace
ms.openlocfilehash: b83ffb9f6a7e0d0c8c970885d2bcb3b63d32581c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="customize-web-application-firewall-rules-through-hello-azure-cli-20"></a><span data-ttu-id="9c006-103">自訂透過 hello Azure CLI 2.0 的 web 應用程式防火牆規則</span><span class="sxs-lookup"><span data-stu-id="9c006-103">Customize web application firewall rules through hello Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="9c006-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="9c006-104">Azure portal</span></span>](application-gateway-customize-waf-rules-portal.md)
> * [<span data-ttu-id="9c006-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9c006-105">PowerShell</span></span>](application-gateway-customize-waf-rules-powershell.md)
> * [<span data-ttu-id="9c006-106">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="9c006-106">Azure CLI 2.0</span></span>](application-gateway-customize-waf-rules-cli.md)

<span data-ttu-id="9c006-107">hello Azure 應用程式閘道 web 應用程式防火牆 (WAF) 提供保護 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9c006-107">hello Azure Application Gateway web application firewall (WAF) provides protection for web applications.</span></span> <span data-ttu-id="9c006-108">這些保護 hello 開啟 Web 應用程式安全性專案 (OWASP) 核心規則設定 (CR) 所提供。</span><span class="sxs-lookup"><span data-stu-id="9c006-108">These protections are provided by hello Open Web Application Security Project (OWASP) Core Rule Set (CRS).</span></span> <span data-ttu-id="9c006-109">某些規則可能會導致誤判，並封鎖真正的流量。</span><span class="sxs-lookup"><span data-stu-id="9c006-109">Some rules can cause false positives and block real traffic.</span></span> <span data-ttu-id="9c006-110">基於這個理由，應用程式閘道提供 hello 功能 toocustomize 規則群組與規則。</span><span class="sxs-lookup"><span data-stu-id="9c006-110">For this reason, Application Gateway provides hello capability toocustomize rule groups and rules.</span></span> <span data-ttu-id="9c006-111">如需有關 hello 特定規則群組與規則的詳細資訊，請參閱[web 應用程式防火牆 CRS 規則群組和規則的清單](application-gateway-crs-rulegroups-rules.md)。</span><span class="sxs-lookup"><span data-stu-id="9c006-111">For more information on hello specific rule groups and rules, see [List of web application firewall CRS rule groups and rules](application-gateway-crs-rulegroups-rules.md).</span></span>

## <a name="view-rule-groups-and-rules"></a><span data-ttu-id="9c006-112">檢視規則群組與規則</span><span class="sxs-lookup"><span data-stu-id="9c006-112">View rule groups and rules</span></span>

<span data-ttu-id="9c006-113">hello，下列程式碼範例顯示如何 tooview 規則和規則設定的群組。</span><span class="sxs-lookup"><span data-stu-id="9c006-113">hello following code examples show how tooview rules and rule groups that are configurable.</span></span>

### <a name="view-rule-groups"></a><span data-ttu-id="9c006-114">檢視規則群組</span><span class="sxs-lookup"><span data-stu-id="9c006-114">View rule groups</span></span>

<span data-ttu-id="9c006-115">hello 下列範例顯示如何 tooview hello 規則群組：</span><span class="sxs-lookup"><span data-stu-id="9c006-115">hello following example shows how tooview hello rule groups:</span></span>

```azurecli-interactive
az network application-gateway waf-config list-rule-sets --type OWASP
```

<span data-ttu-id="9c006-116">hello 下列輸出會截斷的回應從前面範例中的 hello:</span><span class="sxs-lookup"><span data-stu-id="9c006-116">hello following output is a truncated response from hello preceding example:</span></span>

```
[
  {
    "id": "/subscriptions//resourceGroups//providers/Microsoft.Network/applicationGatewayAvailableWafRuleSets/",
    "location": null,
    "name": "OWASP_3.0",
    "provisioningState": "Succeeded",
    "resourceGroup": "",
    "ruleGroups": [
      {
        "description": "",
        "ruleGroupName": "REQUEST-910-IP-REPUTATION",
        "rules": null
      },
      ...
    ],
    "ruleSetType": "OWASP",
    "ruleSetVersion": "3.0",
    "tags": null,
    "type": "Microsoft.Network/applicationGatewayAvailableWafRuleSets"
  },
  {
    "id": "/subscriptions//resourceGroups//providers/Microsoft.Network/applicationGatewayAvailableWafRuleSets/",
    "location": null,
    "name": "OWASP_2.2.9",
    "provisioningState": "Succeeded",
    "resourceGroup": "",
   "ruleGroups": [
      {
        "description": "",
        "ruleGroupName": "crs_20_protocol_violations",
        "rules": null
      },
      ...
    ],
    "ruleSetType": "OWASP",
    "ruleSetVersion": "2.2.9",
    "tags": null,
    "type": "Microsoft.Network/applicationGatewayAvailableWafRuleSets"
  }
]
```

### <a name="view-rules-in-a-rule-group"></a><span data-ttu-id="9c006-117">檢視規則群組中的規則</span><span class="sxs-lookup"><span data-stu-id="9c006-117">View rules in a rule group</span></span>

<span data-ttu-id="9c006-118">下列範例中的 hello 顯示 tooview 規則指定的規則群組中的方式：</span><span class="sxs-lookup"><span data-stu-id="9c006-118">hello following example shows how tooview rules in a specified rule group:</span></span>

```azurecli-interactive
az network application-gateway waf-config list-rule-sets --group "REQUEST-910-IP-REPUTATION"
```

<span data-ttu-id="9c006-119">hello 下列輸出會截斷的回應從前面範例中的 hello:</span><span class="sxs-lookup"><span data-stu-id="9c006-119">hello following output is a truncated response from hello preceding example:</span></span>

```
[
  {
    "id": "/subscriptions//resourceGroups//providers/Microsoft.Network/applicationGatewayAvailableWafRuleSets/",
    "location": null,
    "name": "OWASP_3.0",
    "provisioningState": "Succeeded",
    "resourceGroup": "",
    "ruleGroups": [
      {
        "description": "",
        "ruleGroupName": "REQUEST-910-IP-REPUTATION",
        "rules": [
          {
            "description": "Rule 910011",
            "ruleId": 910011
          },
          ...
        ]
      }
    ],
    "ruleSetType": "OWASP",
    "ruleSetVersion": "3.0",
    "tags": null,
    "type": "Microsoft.Network/applicationGatewayAvailableWafRuleSets"
  }
]
```

## <a name="disable-rules"></a><span data-ttu-id="9c006-120">停用規則</span><span class="sxs-lookup"><span data-stu-id="9c006-120">Disable rules</span></span>

<span data-ttu-id="9c006-121">hello 下列範例會停用規則`910018`和`910017`上應用程式閘道：</span><span class="sxs-lookup"><span data-stu-id="9c006-121">hello following example disables rules `910018` and `910017` on an application gateway:</span></span>

```azurecli-interactive
az network application-gateway waf-config set --resource-group AdatumAppGatewayRG --gateway-name AdatumAppGateway --enabled true --rule-set-version 3.0 --disabled-rules 910018 910017
```

## <a name="next-steps"></a><span data-ttu-id="9c006-122">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9c006-122">Next steps</span></span>

<span data-ttu-id="9c006-123">您設定已停用的規則之後，您可以了解如何 tooview WAF 記錄。</span><span class="sxs-lookup"><span data-stu-id="9c006-123">After you configure your disabled rules, you can learn how tooview your WAF logs.</span></span> <span data-ttu-id="9c006-124">如需詳細資訊，請參閱[應用程式閘道診斷](application-gateway-diagnostics.md#diagnostic-logging)。</span><span class="sxs-lookup"><span data-stu-id="9c006-124">For more information, see [Application Gateway diagnostics](application-gateway-diagnostics.md#diagnostic-logging).</span></span>

[fig1]: ./media/application-gateway-customize-waf-rules-portal/1.png
[1]: ./media/application-gateway-customize-waf-rules-portal/figure1.png
[2]: ./media/application-gateway-customize-waf-rules-portal/figure2.png
[3]: ./media/application-gateway-customize-waf-rules-portal/figure3.png
