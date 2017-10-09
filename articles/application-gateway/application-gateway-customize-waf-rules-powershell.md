---
title: "在 Azure 應用程式閘道 PowerShell aaaCustomize web 應用程式防火牆規則 |Microsoft 文件"
description: "這篇文章提供資訊 toocustomize web 應用程式防火牆規則中使用 PowerShell 的應用程式閘道的方式。"
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
ms.openlocfilehash: f320e687b0f621515255469dac8e375cdd900dda
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="customize-web-application-firewall-rules-through-powershell"></a>透過 PowerShell 自訂 Web 應用程式防火牆規則

> [!div class="op_single_selector"]
> * [Azure 入口網站](application-gateway-customize-waf-rules-portal.md)
> * [PowerShell](application-gateway-customize-waf-rules-powershell.md)
> * [Azure CLI 2.0](application-gateway-customize-waf-rules-cli.md)

hello Azure 應用程式閘道 web 應用程式防火牆 (WAF) 提供保護 web 應用程式。 這些保護 hello 開啟 Web 應用程式安全性專案 (OWASP) 核心規則設定 (CR) 所提供。 某些規則可能會導致誤判，並封鎖真正的流量。 基於這個理由，應用程式閘道提供 hello 功能 toocustomize 規則群組與規則。 如需有關 hello 特定規則群組與規則的詳細資訊，請參閱[web 應用程式防火牆 CRS 規則群組和規則的清單](application-gateway-crs-rulegroups-rules.md)。

## <a name="view-rule-groups-and-rules"></a>檢視規則群組與規則

hello，下列程式碼範例顯示如何 tooview 規則和規則 WAF 啟用應用程式閘道設定的群組。

### <a name="view-rule-groups"></a>檢視規則群組

下列範例會示範如何 hello tooview 規則群組：

```powershell
Get-AzureRmApplicationGatewayAvailableWafRuleSets
```

hello 下列輸出會截斷的回應從前面範例中的 hello:

```
OWASP (Ver. 3.0):

    REQUEST-910-IP-REPUTATION:
        Description:
            
        Rules:
            RuleId     Description
            ------     -----------
            910011     Rule 910011
            910012     Rule 910012
            ...        ...

    REQUEST-911-METHOD-ENFORCEMENT:
        Description:
            
        Rules:
            RuleId     Description
            ------     -----------
            911011     Rule 911011
            ...        ...

OWASP (Ver. 2.2.9):

    crs_20_protocol_violations:
        Description:
            
        Rules:
            RuleId     Description
            ------     -----------
            960911     Invalid HTTP Request Line
            981227     Apache Error: Invalid URI in Request.
            960000     Attempted multipart/form-data bypass
            ...        ...
```

## <a name="disable-rules"></a>停用規則

hello 下列範例會停用規則`910018`和`910017`上應用程式閘道：

```azurecli
az network application-gateway waf-config set --resource-group AdatumAppGatewayRG --gateway-name AdatumAppGateway --enabled true --rule-set-version 3.0 --disabled-rules 910018 910017
```

## <a name="next-steps"></a>後續步驟

您設定已停用的規則之後，您可以了解如何 tooview WAF 記錄。 如需詳細資訊，請參閱[應用程式閘道診斷](application-gateway-diagnostics.md#diagnostic-logging)。

[fig1]: ./media/application-gateway-customize-waf-rules-portal/1.png
[1]: ./media/application-gateway-customize-waf-rules-portal/figure1.png
[2]: ./media/application-gateway-customize-waf-rules-portal/figure2.png
[3]: ./media/application-gateway-customize-waf-rules-portal/figure3.png
