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
# <a name="customize-web-application-firewall-rules-through-hello-azure-cli-20"></a>自訂透過 hello Azure CLI 2.0 的 web 應用程式防火牆規則

> [!div class="op_single_selector"]
> * [Azure 入口網站](application-gateway-customize-waf-rules-portal.md)
> * [PowerShell](application-gateway-customize-waf-rules-powershell.md)
> * [Azure CLI 2.0](application-gateway-customize-waf-rules-cli.md)

hello Azure 應用程式閘道 web 應用程式防火牆 (WAF) 提供保護 web 應用程式。 這些保護 hello 開啟 Web 應用程式安全性專案 (OWASP) 核心規則設定 (CR) 所提供。 某些規則可能會導致誤判，並封鎖真正的流量。 基於這個理由，應用程式閘道提供 hello 功能 toocustomize 規則群組與規則。 如需有關 hello 特定規則群組與規則的詳細資訊，請參閱[web 應用程式防火牆 CRS 規則群組和規則的清單](application-gateway-crs-rulegroups-rules.md)。

## <a name="view-rule-groups-and-rules"></a>檢視規則群組與規則

hello，下列程式碼範例顯示如何 tooview 規則和規則設定的群組。

### <a name="view-rule-groups"></a>檢視規則群組

hello 下列範例顯示如何 tooview hello 規則群組：

```azurecli-interactive
az network application-gateway waf-config list-rule-sets --type OWASP
```

hello 下列輸出會截斷的回應從前面範例中的 hello:

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

### <a name="view-rules-in-a-rule-group"></a>檢視規則群組中的規則

下列範例中的 hello 顯示 tooview 規則指定的規則群組中的方式：

```azurecli-interactive
az network application-gateway waf-config list-rule-sets --group "REQUEST-910-IP-REPUTATION"
```

hello 下列輸出會截斷的回應從前面範例中的 hello:

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

## <a name="disable-rules"></a>停用規則

hello 下列範例會停用規則`910018`和`910017`上應用程式閘道：

```azurecli-interactive
az network application-gateway waf-config set --resource-group AdatumAppGatewayRG --gateway-name AdatumAppGateway --enabled true --rule-set-version 3.0 --disabled-rules 910018 910017
```

## <a name="next-steps"></a>後續步驟

您設定已停用的規則之後，您可以了解如何 tooview WAF 記錄。 如需詳細資訊，請參閱[應用程式閘道診斷](application-gateway-diagnostics.md#diagnostic-logging)。

[fig1]: ./media/application-gateway-customize-waf-rules-portal/1.png
[1]: ./media/application-gateway-customize-waf-rules-portal/figure1.png
[2]: ./media/application-gateway-customize-waf-rules-portal/figure2.png
[3]: ./media/application-gateway-customize-waf-rules-portal/figure3.png
