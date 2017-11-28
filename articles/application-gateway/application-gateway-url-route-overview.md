---
title: "aaaURL 為基礎的內容路由概觀 |Microsoft 文件"
description: "此頁面提供 hello 應用程式閘道 URL 為基礎內容的路由、 UrlPathMap 組態和 PathBasedRouting 規則的概觀。"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: 
ms.assetid: 4409159b-e22d-4c9a-a103-f5d32465d163
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/09/2017
ms.author: gwallace
ms.openlocfilehash: 5094b42625baffeb395beace68db0d269e46080c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="url-path-based-routing-overview"></a><span data-ttu-id="d3556-103">URL 路徑型路由概觀</span><span class="sxs-lookup"><span data-stu-id="d3556-103">URL Path Based Routing overview</span></span>

<span data-ttu-id="d3556-104">URL 路徑基礎的路由可讓您 tooroute 流量 tooback 後端伺服器集區根據 hello 要求的 URL 路徑。</span><span class="sxs-lookup"><span data-stu-id="d3556-104">URL Path Based Routing allows you tooroute traffic tooback-end server pools based on URL Paths of hello request.</span></span> 

<span data-ttu-id="d3556-105">Tooroute 要求不同的內容類型 toodifferent 後端伺服器集區的其中一個 hello 案例。</span><span class="sxs-lookup"><span data-stu-id="d3556-105">One of hello scenarios is tooroute requests for different content types toodifferent backend server pools.</span></span>

<span data-ttu-id="d3556-106">在下列範例的 hello，應用程式閘道正在提供服務給 contoso.com 從三個後端伺服器集區的流量，例如： VideoServerPool、 ImageServerPool 和 DefaultServerPool。</span><span class="sxs-lookup"><span data-stu-id="d3556-106">In hello following example, Application Gateway is serving traffic for contoso.com from three back-end server pools for example: VideoServerPool, ImageServerPool, and DefaultServerPool.</span></span>

![imageURLroute](./media/application-gateway-url-route-overview/figure1.png)

<span data-ttu-id="d3556-108">要求的 http://contoso.com/video * 路由的 tooVideoServerPool，而 http://contoso.com/images * 路由的 tooImageServerPool。</span><span class="sxs-lookup"><span data-stu-id="d3556-108">Requests for http://contoso.com/video* are routed tooVideoServerPool, and http://contoso.com/images* are routed tooImageServerPool.</span></span> <span data-ttu-id="d3556-109">如果沒有 hello 路徑模式符合，會選取 DefaultServerPool。</span><span class="sxs-lookup"><span data-stu-id="d3556-109">DefaultServerPool is selected if none of hello path patterns match.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d3556-110">規則的處理順序 hello hello 入口網站中列出。</span><span class="sxs-lookup"><span data-stu-id="d3556-110">Rules are processed in hello order they are listed in hello portal.</span></span> <span data-ttu-id="d3556-111">強烈建議使用的 tooconfigure 多站台接聽程式第一次先前 tooconfiguring 基本的接聽程式它。</span><span class="sxs-lookup"><span data-stu-id="d3556-111">It is highly recommended tooconfigure multi-site listeners first prior tooconfiguring a basic listener.</span></span>  <span data-ttu-id="d3556-112">這可確保該流量取得路由的 toohello 帶回結束。</span><span class="sxs-lookup"><span data-stu-id="d3556-112">This ensures that traffic gets routed toohello right back end.</span></span> <span data-ttu-id="d3556-113">如果先列出了基本接聽程式，且該接聽程式符合傳入的要求，就會由該接聽程式處理。</span><span class="sxs-lookup"><span data-stu-id="d3556-113">If a basic listener is listed first and matches an incoming request, it gets processed by that listener.</span></span>

## <a name="urlpathmap-configuration-element"></a><span data-ttu-id="d3556-114">UrlPathMap 組態元素</span><span class="sxs-lookup"><span data-stu-id="d3556-114">UrlPathMap configuration element</span></span>

<span data-ttu-id="d3556-115">hello urlPathMap 項目是使用的 toospecify 路徑模式 tooback 端伺服器集區對應。</span><span class="sxs-lookup"><span data-stu-id="d3556-115">hello urlPathMap element is used toospecify Path patterns tooback-end server pool mappings.</span></span> <span data-ttu-id="d3556-116">hello 下列程式碼範例是 hello urlPathMap 項目，從範本檔案的程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="d3556-116">hello following code example is hello snippet of urlPathMap element from template file.</span></span>

```json
"urlPathMaps": [{
    "name": "{urlpathMapName}",
    "id": "/subscriptions/{subscriptionId}/../microsoft.network/applicationGateways/{gatewayName}/urlPathMaps/{urlpathMapName}",
    "properties": {
        "defaultBackendAddressPool": {
            "id": "/subscriptions/    {subscriptionId}/../microsoft.network/applicationGateways/{gatewayName}/backendAddressPools/{poolName1}"
        },
        "defaultBackendHttpSettings": {
            "id": "/subscriptions/{subscriptionId}/../microsoft.network/applicationGateways/{gatewayName}/backendHttpSettingsList/{settingname1}"
        },
        "pathRules": [{
            "name": "{pathRuleName}",
            "properties": {
                "paths": [
                    "{pathPattern}"
                ],
                "backendAddressPool": {
                    "id": "/subscriptions/{subscriptionId}/../microsoft.network/applicationGateways/{gatewayName}/backendAddressPools/{poolName2}"
                },
                "backendHttpsettings": {
                    "id": "/subscriptions/{subscriptionId}/../microsoft.network/applicationGateways/{gatewayName}/backendHttpsettingsList/{settingName2}"
                }
            }
        }]
    }
}]
```

> [!NOTE]
> <span data-ttu-id="d3556-117">PathPattern： 此設定是一份路徑模式 toomatch。</span><span class="sxs-lookup"><span data-stu-id="d3556-117">PathPattern: This setting is a list of path patterns toomatch.</span></span> <span data-ttu-id="d3556-118">每個開頭必須是 / 和 hello 唯一地方"*"hello 在結束之後，允許"/。 」</span><span class="sxs-lookup"><span data-stu-id="d3556-118">Each must start with / and hello only place a "*" is allowed is at hello end following a "/."</span></span> <span data-ttu-id="d3556-119">fed toohello 路徑比對器 hello 字串不包含任何文字 hello 之後第一次嗎？或 #，且這些字元不得使用此處。</span><span class="sxs-lookup"><span data-stu-id="d3556-119">hello string fed toohello path matcher does not include any text after hello first? or #, and those chars are not allowed here.</span></span>

<span data-ttu-id="d3556-120">如需詳細資訊，您可以查看 [使用 URL 型路由的 Resource Manager 範本](https://azure.microsoft.com/documentation/templates/201-application-gateway-url-path-based-routing) 。</span><span class="sxs-lookup"><span data-stu-id="d3556-120">You can check out a [Resource Manager template using URL-based routing](https://azure.microsoft.com/documentation/templates/201-application-gateway-url-path-based-routing) for more information.</span></span>

## <a name="pathbasedrouting-rule"></a><span data-ttu-id="d3556-121">PathBasedRouting 規則</span><span class="sxs-lookup"><span data-stu-id="d3556-121">PathBasedRouting rule</span></span>

<span data-ttu-id="d3556-122">型別 PathBasedRouting RequestRoutingRule 是使用的 toobind 接聽程式 tooa urlPathMap。</span><span class="sxs-lookup"><span data-stu-id="d3556-122">RequestRoutingRule of type PathBasedRouting is used toobind a listener tooa urlPathMap.</span></span> <span data-ttu-id="d3556-123">針對此接聽程式接收到的所有要求都會根據 urlPathMap 中指定的原則進行路由傳送。</span><span class="sxs-lookup"><span data-stu-id="d3556-123">All requests that are received for this listener are routed based on policy specified in urlPathMap.</span></span>
<span data-ttu-id="d3556-124">PathBasedRouting 規則的程式碼片段：</span><span class="sxs-lookup"><span data-stu-id="d3556-124">Snippet of PathBasedRouting rule:</span></span>

```json
"requestRoutingRules": [
    {

"name": "{ruleName}",
"id": "/subscriptions/{subscriptionId}/../microsoft.network/applicationGateways/{gatewayName}/requestRoutingRules/{ruleName}",
"properties": {
    "ruleType": "PathBasedRouting",
    "httpListener": {
        "id": "/subscriptions/{subscriptionId}/../microsoft.network/applicationGateways/{gatewayName}/httpListeners/<listenerName>"
    },
    "urlPathMap": {
        "id": "/subscriptions/{subscriptionId}/../microsoft.network/applicationGateways/{gatewayName}/ urlPathMaps/{urlpathMapName}"
    },

}
    }
]
```

## <a name="next-steps"></a><span data-ttu-id="d3556-125">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d3556-125">Next steps</span></span>

<span data-ttu-id="d3556-126">在了解相關的 URL 為基礎的內容路由傳送之後, 請繼續太[建立應用程式閘道使用的 URL 為基礎的路由](application-gateway-create-url-route-portal.md)toocreate 應用程式閘道與 URL 的路由規則。</span><span class="sxs-lookup"><span data-stu-id="d3556-126">After learning about URL-based content routing, go too[create an application gateway using URL-based routing](application-gateway-create-url-route-portal.md) toocreate an application gateway with URL routing rules.</span></span>
