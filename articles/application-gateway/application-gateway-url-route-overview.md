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
# <a name="url-path-based-routing-overview"></a>URL 路徑型路由概觀

URL 路徑基礎的路由可讓您 tooroute 流量 tooback 後端伺服器集區根據 hello 要求的 URL 路徑。 

Tooroute 要求不同的內容類型 toodifferent 後端伺服器集區的其中一個 hello 案例。

在下列範例的 hello，應用程式閘道正在提供服務給 contoso.com 從三個後端伺服器集區的流量，例如： VideoServerPool、 ImageServerPool 和 DefaultServerPool。

![imageURLroute](./media/application-gateway-url-route-overview/figure1.png)

要求的 http://contoso.com/video * 路由的 tooVideoServerPool，而 http://contoso.com/images * 路由的 tooImageServerPool。 如果沒有 hello 路徑模式符合，會選取 DefaultServerPool。

> [!IMPORTANT]
> 規則的處理順序 hello hello 入口網站中列出。 強烈建議使用的 tooconfigure 多站台接聽程式第一次先前 tooconfiguring 基本的接聽程式它。  這可確保該流量取得路由的 toohello 帶回結束。 如果先列出了基本接聽程式，且該接聽程式符合傳入的要求，就會由該接聽程式處理。

## <a name="urlpathmap-configuration-element"></a>UrlPathMap 組態元素

hello urlPathMap 項目是使用的 toospecify 路徑模式 tooback 端伺服器集區對應。 hello 下列程式碼範例是 hello urlPathMap 項目，從範本檔案的程式碼片段。

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
> PathPattern： 此設定是一份路徑模式 toomatch。 每個開頭必須是 / 和 hello 唯一地方"*"hello 在結束之後，允許"/。 」 fed toohello 路徑比對器 hello 字串不包含任何文字 hello 之後第一次嗎？或 #，且這些字元不得使用此處。

如需詳細資訊，您可以查看 [使用 URL 型路由的 Resource Manager 範本](https://azure.microsoft.com/documentation/templates/201-application-gateway-url-path-based-routing) 。

## <a name="pathbasedrouting-rule"></a>PathBasedRouting 規則

型別 PathBasedRouting RequestRoutingRule 是使用的 toobind 接聽程式 tooa urlPathMap。 針對此接聽程式接收到的所有要求都會根據 urlPathMap 中指定的原則進行路由傳送。
PathBasedRouting 規則的程式碼片段：

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

## <a name="next-steps"></a>後續步驟

在了解相關的 URL 為基礎的內容路由傳送之後, 請繼續太[建立應用程式閘道使用的 URL 為基礎的路由](application-gateway-create-url-route-portal.md)toocreate 應用程式閘道與 URL 的路由規則。
