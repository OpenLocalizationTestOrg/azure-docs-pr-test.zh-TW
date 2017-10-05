---
title: "在 Azure 應用程式閘道中自訂 Web 應用程式防火牆規則 - Azure CLI 2.0 | Microsoft Docs"
description: "本文提供如何透過 Azure CLI 2.0，在應用程式閘道中自訂 Web 應用程式防火牆規則的相關資訊。"
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
ms.openlocfilehash: 456be048dc2d82cd50d145b71f17a84a7189ea96
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="customize-web-application-firewall-rules-through-the-azure-cli-20"></a><span data-ttu-id="6ef04-103">透過 Azure CLI 2.0 自訂 Web 應用程式防火牆規則</span><span class="sxs-lookup"><span data-stu-id="6ef04-103">Customize web application firewall rules through the Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="6ef04-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="6ef04-104">Azure portal</span></span>](application-gateway-customize-waf-rules-portal.md)
> * [<span data-ttu-id="6ef04-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6ef04-105">PowerShell</span></span>](application-gateway-customize-waf-rules-powershell.md)
> * [<span data-ttu-id="6ef04-106">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="6ef04-106">Azure CLI 2.0</span></span>](application-gateway-customize-waf-rules-cli.md)

<span data-ttu-id="6ef04-107">Azure 應用程式閘道 Web 應用程式防火牆 (WAF) 提供 Web 應用程式的保護。</span><span class="sxs-lookup"><span data-stu-id="6ef04-107">The Azure Application Gateway web application firewall (WAF) provides protection for web applications.</span></span> <span data-ttu-id="6ef04-108">這些保護是由開放 Web 應用程式安全性專案 (OWASP) 的核心規則集 (CRS) 所提供。</span><span class="sxs-lookup"><span data-stu-id="6ef04-108">These protections are provided by the Open Web Application Security Project (OWASP) Core Rule Set (CRS).</span></span> <span data-ttu-id="6ef04-109">某些規則可能會導致誤判，並封鎖真正的流量。</span><span class="sxs-lookup"><span data-stu-id="6ef04-109">Some rules can cause false positives and block real traffic.</span></span> <span data-ttu-id="6ef04-110">因此，應用程式閘道會提供功能以自訂規則群組與規則。</span><span class="sxs-lookup"><span data-stu-id="6ef04-110">For this reason, Application Gateway provides the capability to customize rule groups and rules.</span></span> <span data-ttu-id="6ef04-111">如需特定規則群組與規則的詳細資訊，請參閱 [Web 應用程式防火牆 CRS 規則群組與規則的清單](application-gateway-crs-rulegroups-rules.md)。</span><span class="sxs-lookup"><span data-stu-id="6ef04-111">For more information on the specific rule groups and rules, see [List of web application firewall CRS rule groups and rules](application-gateway-crs-rulegroups-rules.md).</span></span>

## <a name="view-rule-groups-and-rules"></a><span data-ttu-id="6ef04-112">檢視規則群組與規則</span><span class="sxs-lookup"><span data-stu-id="6ef04-112">View rule groups and rules</span></span>

<span data-ttu-id="6ef04-113">以下程式碼範例顯示如何檢視可設定的規則和規則群組。</span><span class="sxs-lookup"><span data-stu-id="6ef04-113">The following code examples show how to view rules and rule groups that are configurable.</span></span>

### <a name="view-rule-groups"></a><span data-ttu-id="6ef04-114">檢視規則群組</span><span class="sxs-lookup"><span data-stu-id="6ef04-114">View rule groups</span></span>

<span data-ttu-id="6ef04-115">下列範例顯示如何檢視規則群組：</span><span class="sxs-lookup"><span data-stu-id="6ef04-115">The following example shows how to view the rule groups:</span></span>

```azurecli-interactive
az network application-gateway waf-config list-rule-sets --type OWASP
```

<span data-ttu-id="6ef04-116">以下輸出是上述範例的截斷回應：</span><span class="sxs-lookup"><span data-stu-id="6ef04-116">The following output is a truncated response from the preceding example:</span></span>

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

### <a name="view-rules-in-a-rule-group"></a><span data-ttu-id="6ef04-117">檢視規則群組中的規則</span><span class="sxs-lookup"><span data-stu-id="6ef04-117">View rules in a rule group</span></span>

<span data-ttu-id="6ef04-118">下列範例顯示如何檢視指定規則群組中的規則：</span><span class="sxs-lookup"><span data-stu-id="6ef04-118">The following example shows how to view rules in a specified rule group:</span></span>

```azurecli-interactive
az network application-gateway waf-config list-rule-sets --group "REQUEST-910-IP-REPUTATION"
```

<span data-ttu-id="6ef04-119">以下輸出是上述範例的截斷回應：</span><span class="sxs-lookup"><span data-stu-id="6ef04-119">The following output is a truncated response from the preceding example:</span></span>

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

## <a name="disable-rules"></a><span data-ttu-id="6ef04-120">停用規則</span><span class="sxs-lookup"><span data-stu-id="6ef04-120">Disable rules</span></span>

<span data-ttu-id="6ef04-121">下列範例會停用應用程式閘道上的規則 `910018` 和 `910017`：</span><span class="sxs-lookup"><span data-stu-id="6ef04-121">The following example disables rules `910018` and `910017` on an application gateway:</span></span>

```azurecli-interactive
az network application-gateway waf-config set --resource-group AdatumAppGatewayRG --gateway-name AdatumAppGateway --enabled true --rule-set-version 3.0 --disabled-rules 910018 910017
```

## <a name="next-steps"></a><span data-ttu-id="6ef04-122">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6ef04-122">Next steps</span></span>

<span data-ttu-id="6ef04-123">設定已停用的規則之後，您可以了解如何檢視 WAF 記錄。</span><span class="sxs-lookup"><span data-stu-id="6ef04-123">After you configure your disabled rules, you can learn how to view your WAF logs.</span></span> <span data-ttu-id="6ef04-124">如需詳細資訊，請參閱[應用程式閘道診斷](application-gateway-diagnostics.md#diagnostic-logging)。</span><span class="sxs-lookup"><span data-stu-id="6ef04-124">For more information, see [Application Gateway diagnostics](application-gateway-diagnostics.md#diagnostic-logging).</span></span>

[fig1]: ./media/application-gateway-customize-waf-rules-portal/1.png
[1]: ./media/application-gateway-customize-waf-rules-portal/figure1.png
[2]: ./media/application-gateway-customize-waf-rules-portal/figure2.png
[3]: ./media/application-gateway-customize-waf-rules-portal/figure3.png
