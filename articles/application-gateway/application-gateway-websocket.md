---
title: "在 Azure 應用程式閘道 aaaWebSocket 支援 |Microsoft 文件"
description: "此頁面提供 hello 應用程式閘道 WebSocket 支援的概觀。"
documentationcenter: na
services: application-gateway
author: amsriva
manager: rossort
editor: amsriva
ms.assetid: 8968dac1-e9bc-4fa1-8415-96decacab83f
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/08/2017
ms.author: amsriva
ms.openlocfilehash: 3776117803e8559ad243c2d4c3dd661199c1e48a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-websocket-support-in-application-gateway"></a>應用程式閘道中的 WebSocket 支援概觀

應用程式閘道可跨所有閘道大小對 WebSocket 提供原生支援。 沒有任何使用者可設定的設定 tooselectively 啟用或停用 WebSocket 支援。 

以 [RFC6455](https://tools.ietf.org/html/rfc6455) 標準化的 WebSocket 通訊協定可透過長時間執行的 TCP 連線讓伺服器和用戶端之間能夠進行全雙工通訊。 這項功能可讓更多的互動之間的通訊 hello web 伺服器和 hello 用戶端，它可以是雙向而 hello 需要輪詢當做在需要以 HTTP 為基礎的實作。 WebSocket 具有低額外負荷與不同的是 HTTP，並重複使用可以 hello 相同多個要求/回應造成更有效率的資源使用量的 TCP 連線。 WebSocket 通訊協定是設計的 toowork 透過傳統的 HTTP 連接埠 80 和 443。

您可以繼續在連接埠 80 或 443 tooreceive WebSocket 傳輸使用標準的 HTTP 接聽程式。 WebSocket 流量會導向的 toohello WebSocket 啟用後端伺服器使用應用程式閘道規則中指定的 hello 適當的後端集區。 hello 後端伺服器必須回應 toohello 應用程式閘道探查，hello 中所述[健全狀況探查概觀](application-gateway-probe-overview.md)> 一節。 應用程式閘道健康情況探查僅限使用 HTTP/HTTPS。 每個後端伺服器必須回應 tooHTTP 探查應用程式閘道 tooroute WebSocket 傳輸 toohello 伺服器。

## <a name="listener-configuration-element"></a>接聽程式組態元素

現有的 HTTP 接聽程式可以使用的 toosupport WebSocket 傳輸。 hello 以下是範例範本檔案中 httplisteners 的數目元素的程式碼片段。 您會需要 HTTP 和 HTTPS 接聽程式 toosupport WebSocket，及保護 WebSocket 傳輸。 同樣地，您可以使用 hello[入口網站](application-gateway-create-gateway-portal.md)或[PowerShell](application-gateway-create-gateway-arm.md) toocreate 應用程式閘道與連接埠 80/443 toosupport WebSocket 流量上的接聽程式。

```json
"httpListeners": [
        {
            "name": "appGatewayHttpsListener",
            "properties": {
                "FrontendIPConfiguration": {
                    "Id": "/subscriptions/{subscriptionId/resourceGroups/{resourceGroupName/providers/Microsoft.Network/applicationGateways/{applicationGatewayName/frontendIPConfigurations/DefaultFrontendPublicIP"
                },
                "FrontendPort": {
                    "Id": "/subscriptions/{subscriptionId/resourceGroups/{resourceGroupName/providers/Microsoft.Network/applicationGateways/{applicationGatewayName/frontendPorts/appGatewayFrontendPort443'"
                },
                "Protocol": "Https",
                "SslCertificate": {
                    "Id": "/subscriptions/{subscriptionId/resourceGroups/{resourceGroupName/providers/Microsoft.Network/applicationGateways/{applicationGatewayName/sslCertificates/appGatewaySslCert1'"
                },
            }
        },
        {
            "name": "appGatewayHttpListener",
            "properties": {
                "FrontendIPConfiguration": {
                    "Id": "/subscriptions/{subscriptionId/resourceGroups/{resourceGroupName/providers/Microsoft.Network/applicationGateways/{applicationGatewayName/frontendIPConfigurations/appGatewayFrontendIP'"
                },
                "FrontendPort": {
                    "Id": "/subscriptions/{subscriptionId/resourceGroups/{resourceGroupName/providers/Microsoft.Network/applicationGateways/{applicationGatewayName/frontendPorts/appGatewayFrontendPort80'"
                },
                "Protocol": "Http",
            }
        }
    ],
```

## <a name="backendaddresspool-backendhttpsetting-and-routing-rule-configuration"></a>BackendAddressPool、BackendHttpSetting 和路由規則組態

BackendAddressPool 是使用的 toodefine 啟用 WebSocket 伺服器的後端集區。 hello backendHttpSetting 會定義與後端連接埠 80 和 443。 以 cookie 為基礎的親和性和 requestTimeouts hello 屬性不相關的 tooWebSocket 流量。 沒有任何變更，需要在 hello 路由規則，「 基本 」 使用的 tootie hello 適當的接聽程式 toohello 對應後端位址集區。 

```json
"requestRoutingRules": [{
    "name": "<ruleName1>",
    "properties": {
        "RuleType": "Basic",
        "httpListener": {
            "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/applicationGateways/{applicationGatewayName}/httpListeners/appGatewayHttpsListener')]"
        },
        "backendAddressPool": {
            "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/applicationGateways/{applicationGatewayName}/backendAddressPools/ContosoServerPool')]"
        },
        "backendHttpSettings": {
            "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/applicationGateways/{applicationGatewayName}/backendHttpSettingsCollection/appGatewayBackendHttpSettings')]"
        }
    }

}, {
    "name": "<ruleName2>",
    "properties": {
        "RuleType": "Basic",
        "httpListener": {
            "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/applicationGateways/{applicationGatewayName}/httpListeners/appGatewayHttpListener')]"
        },
        "backendAddressPool": {
            "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/applicationGateways/{applicationGatewayName}/backendAddressPools/ContosoServerPool')]"
        },
        "backendHttpSettings": {
            "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/applicationGateways/{applicationGatewayName}/backendHttpSettingsCollection/appGatewayBackendHttpSettings')]"
        }

    }
}]
```

## <a name="websocket-enabled-backend"></a>已啟用 WebSocket 的後端

您的後端必須有 HTTP/HTTPS web 伺服器上設定的 hello 執行 WebSocket toowork 的連接埠 (通常是 80/443)。 這是因為 WebSocket 通訊協定需要 hello 初始信號交換 toobe HTTP 標頭欄位升級 tooWebSocket 通訊協定。 hello 以下是範例標頭：

```
    GET /chat HTTP/1.1
    Host: server.example.com
    Upgrade: websocket
    Connection: Upgrade
    Sec-WebSocket-Key: dGhlIHNhbXBsZSBub25jZQ==
    Origin: http://example.com
    Sec-WebSocket-Protocol: chat, superchat
    Sec-WebSocket-Version: 13
```

另一個原因是該應用程式閘道後端健全狀態探查只支援 HTTP 和 HTTPS 通訊協定。 如果 tooHTTP 或 HTTPS 探查 hello 後端伺服器沒有回應，它被帶離後端集區。

## <a name="next-steps"></a>後續步驟

在了解 WebSocket 支援之後, 請繼續太[建立應用程式閘道](application-gateway-create-gateway.md)tooget 入門 WebSocket 啟用 web 應用程式。

