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
# <a name="customize-web-application-firewall-rules-through-powershell"></a><span data-ttu-id="c5cfa-103">透過 PowerShell 自訂 Web 應用程式防火牆規則</span><span class="sxs-lookup"><span data-stu-id="c5cfa-103">Customize web application firewall rules through PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="c5cfa-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="c5cfa-104">Azure portal</span></span>](application-gateway-customize-waf-rules-portal.md)
> * [<span data-ttu-id="c5cfa-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c5cfa-105">PowerShell</span></span>](application-gateway-customize-waf-rules-powershell.md)
> * [<span data-ttu-id="c5cfa-106">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="c5cfa-106">Azure CLI 2.0</span></span>](application-gateway-customize-waf-rules-cli.md)

<span data-ttu-id="c5cfa-107">hello Azure 應用程式閘道 web 應用程式防火牆 (WAF) 提供保護 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c5cfa-107">hello Azure Application Gateway web application firewall (WAF) provides protection for web applications.</span></span> <span data-ttu-id="c5cfa-108">這些保護 hello 開啟 Web 應用程式安全性專案 (OWASP) 核心規則設定 (CR) 所提供。</span><span class="sxs-lookup"><span data-stu-id="c5cfa-108">These protections are provided by hello Open Web Application Security Project (OWASP) Core Rule Set (CRS).</span></span> <span data-ttu-id="c5cfa-109">某些規則可能會導致誤判，並封鎖真正的流量。</span><span class="sxs-lookup"><span data-stu-id="c5cfa-109">Some rules can cause false positives and block real traffic.</span></span> <span data-ttu-id="c5cfa-110">基於這個理由，應用程式閘道提供 hello 功能 toocustomize 規則群組與規則。</span><span class="sxs-lookup"><span data-stu-id="c5cfa-110">For this reason, Application Gateway provides hello capability toocustomize rule groups and rules.</span></span> <span data-ttu-id="c5cfa-111">如需有關 hello 特定規則群組與規則的詳細資訊，請參閱[web 應用程式防火牆 CRS 規則群組和規則的清單](application-gateway-crs-rulegroups-rules.md)。</span><span class="sxs-lookup"><span data-stu-id="c5cfa-111">For more information on hello specific rule groups and rules, see [List of web application firewall CRS Rule groups and rules](application-gateway-crs-rulegroups-rules.md).</span></span>

## <a name="view-rule-groups-and-rules"></a><span data-ttu-id="c5cfa-112">檢視規則群組與規則</span><span class="sxs-lookup"><span data-stu-id="c5cfa-112">View rule groups and rules</span></span>

<span data-ttu-id="c5cfa-113">hello，下列程式碼範例顯示如何 tooview 規則和規則 WAF 啟用應用程式閘道設定的群組。</span><span class="sxs-lookup"><span data-stu-id="c5cfa-113">hello following code examples show how tooview rules and rule groups that are configurable on a WAF-enabled application gateway.</span></span>

### <a name="view-rule-groups"></a><span data-ttu-id="c5cfa-114">檢視規則群組</span><span class="sxs-lookup"><span data-stu-id="c5cfa-114">View rule groups</span></span>

<span data-ttu-id="c5cfa-115">下列範例會示範如何 hello tooview 規則群組：</span><span class="sxs-lookup"><span data-stu-id="c5cfa-115">hello following example shows how tooview rule groups:</span></span>

```powershell
Get-AzureRmApplicationGatewayAvailableWafRuleSets
```

<span data-ttu-id="c5cfa-116">hello 下列輸出會截斷的回應從前面範例中的 hello:</span><span class="sxs-lookup"><span data-stu-id="c5cfa-116">hello following output is a truncated response from hello preceding example:</span></span>

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

## <a name="disable-rules"></a><span data-ttu-id="c5cfa-117">停用規則</span><span class="sxs-lookup"><span data-stu-id="c5cfa-117">Disable rules</span></span>

<span data-ttu-id="c5cfa-118">hello 下列範例會停用規則`910018`和`910017`上應用程式閘道：</span><span class="sxs-lookup"><span data-stu-id="c5cfa-118">hello following example disables rules `910018` and `910017` on an application gateway:</span></span>

```azurecli
az network application-gateway waf-config set --resource-group AdatumAppGatewayRG --gateway-name AdatumAppGateway --enabled true --rule-set-version 3.0 --disabled-rules 910018 910017
```

## <a name="next-steps"></a><span data-ttu-id="c5cfa-119">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c5cfa-119">Next steps</span></span>

<span data-ttu-id="c5cfa-120">您設定已停用的規則之後，您可以了解如何 tooview WAF 記錄。</span><span class="sxs-lookup"><span data-stu-id="c5cfa-120">After you configure your disabled rules, you can learn how tooview your WAF logs.</span></span> <span data-ttu-id="c5cfa-121">如需詳細資訊，請參閱[應用程式閘道診斷](application-gateway-diagnostics.md#diagnostic-logging)。</span><span class="sxs-lookup"><span data-stu-id="c5cfa-121">For more information, see [Application Gateway Diagnostics](application-gateway-diagnostics.md#diagnostic-logging).</span></span>

[fig1]: ./media/application-gateway-customize-waf-rules-portal/1.png
[1]: ./media/application-gateway-customize-waf-rules-portal/figure1.png
[2]: ./media/application-gateway-customize-waf-rules-portal/figure2.png
[3]: ./media/application-gateway-customize-waf-rules-portal/figure3.png
