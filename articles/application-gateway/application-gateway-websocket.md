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
# <a name="overview-of-websocket-support-in-application-gateway"></a><span data-ttu-id="9dee2-103">應用程式閘道中的 WebSocket 支援概觀</span><span class="sxs-lookup"><span data-stu-id="9dee2-103">Overview of WebSocket support in Application Gateway</span></span>

<span data-ttu-id="9dee2-104">應用程式閘道可跨所有閘道大小對 WebSocket 提供原生支援。</span><span class="sxs-lookup"><span data-stu-id="9dee2-104">Application Gateway provides native support for WebSocket across all gateway sizes.</span></span> <span data-ttu-id="9dee2-105">沒有任何使用者可設定的設定 tooselectively 啟用或停用 WebSocket 支援。</span><span class="sxs-lookup"><span data-stu-id="9dee2-105">There is no user-configurable setting tooselectively enable or disable WebSocket support.</span></span> 

<span data-ttu-id="9dee2-106">以 [RFC6455](https://tools.ietf.org/html/rfc6455) 標準化的 WebSocket 通訊協定可透過長時間執行的 TCP 連線讓伺服器和用戶端之間能夠進行全雙工通訊。</span><span class="sxs-lookup"><span data-stu-id="9dee2-106">WebSocket protocol standardized in [RFC6455](https://tools.ietf.org/html/rfc6455) enables a full duplex communication between a server and a client over a long running TCP connection.</span></span> <span data-ttu-id="9dee2-107">這項功能可讓更多的互動之間的通訊 hello web 伺服器和 hello 用戶端，它可以是雙向而 hello 需要輪詢當做在需要以 HTTP 為基礎的實作。</span><span class="sxs-lookup"><span data-stu-id="9dee2-107">This feature allows for a more interactive communication between hello web server and hello client, which can be bidirectional without hello need for polling as required in HTTP-based implementations.</span></span> <span data-ttu-id="9dee2-108">WebSocket 具有低額外負荷與不同的是 HTTP，並重複使用可以 hello 相同多個要求/回應造成更有效率的資源使用量的 TCP 連線。</span><span class="sxs-lookup"><span data-stu-id="9dee2-108">WebSocket has low overhead unlike HTTP and can reuse hello same TCP connection for multiple request/responses resulting in a more efficient utilization of resources.</span></span> <span data-ttu-id="9dee2-109">WebSocket 通訊協定是設計的 toowork 透過傳統的 HTTP 連接埠 80 和 443。</span><span class="sxs-lookup"><span data-stu-id="9dee2-109">WebSocket protocols are designed toowork over traditional HTTP ports of 80 and 443.</span></span>

<span data-ttu-id="9dee2-110">您可以繼續在連接埠 80 或 443 tooreceive WebSocket 傳輸使用標準的 HTTP 接聽程式。</span><span class="sxs-lookup"><span data-stu-id="9dee2-110">You can continue using a standard HTTP listener on port 80 or 443 tooreceive WebSocket traffic.</span></span> <span data-ttu-id="9dee2-111">WebSocket 流量會導向的 toohello WebSocket 啟用後端伺服器使用應用程式閘道規則中指定的 hello 適當的後端集區。</span><span class="sxs-lookup"><span data-stu-id="9dee2-111">WebSocket traffic is then directed toohello WebSocket enabled backend server using hello appropriate backend pool as specified in application gateway rules.</span></span> <span data-ttu-id="9dee2-112">hello 後端伺服器必須回應 toohello 應用程式閘道探查，hello 中所述[健全狀況探查概觀](application-gateway-probe-overview.md)> 一節。</span><span class="sxs-lookup"><span data-stu-id="9dee2-112">hello backend server must respond toohello application gateway probes, which are described in hello [health probe overview](application-gateway-probe-overview.md) section.</span></span> <span data-ttu-id="9dee2-113">應用程式閘道健康情況探查僅限使用 HTTP/HTTPS。</span><span class="sxs-lookup"><span data-stu-id="9dee2-113">Application gateway health probes are HTTP/HTTPS only.</span></span> <span data-ttu-id="9dee2-114">每個後端伺服器必須回應 tooHTTP 探查應用程式閘道 tooroute WebSocket 傳輸 toohello 伺服器。</span><span class="sxs-lookup"><span data-stu-id="9dee2-114">Each backend server must respond tooHTTP probes for application gateway tooroute WebSocket traffic toohello server.</span></span>

## <a name="listener-configuration-element"></a><span data-ttu-id="9dee2-115">接聽程式組態元素</span><span class="sxs-lookup"><span data-stu-id="9dee2-115">Listener configuration element</span></span>

<span data-ttu-id="9dee2-116">現有的 HTTP 接聽程式可以使用的 toosupport WebSocket 傳輸。</span><span class="sxs-lookup"><span data-stu-id="9dee2-116">An existing HTTP listener can be used toosupport WebSocket traffic.</span></span> <span data-ttu-id="9dee2-117">hello 以下是範例範本檔案中 httplisteners 的數目元素的程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="9dee2-117">hello following is a snippet of an httpListeners element from a sample template file.</span></span> <span data-ttu-id="9dee2-118">您會需要 HTTP 和 HTTPS 接聽程式 toosupport WebSocket，及保護 WebSocket 傳輸。</span><span class="sxs-lookup"><span data-stu-id="9dee2-118">You would need both HTTP and HTTPS listeners toosupport WebSocket and secure WebSocket traffic.</span></span> <span data-ttu-id="9dee2-119">同樣地，您可以使用 hello[入口網站](application-gateway-create-gateway-portal.md)或[PowerShell](application-gateway-create-gateway-arm.md) toocreate 應用程式閘道與連接埠 80/443 toosupport WebSocket 流量上的接聽程式。</span><span class="sxs-lookup"><span data-stu-id="9dee2-119">Similarly you can use hello [portal](application-gateway-create-gateway-portal.md) or [PowerShell](application-gateway-create-gateway-arm.md) toocreate an application gateway with listeners on port 80/443 toosupport WebSocket traffic.</span></span>

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

## <a name="backendaddresspool-backendhttpsetting-and-routing-rule-configuration"></a><span data-ttu-id="9dee2-120">BackendAddressPool、BackendHttpSetting 和路由規則組態</span><span class="sxs-lookup"><span data-stu-id="9dee2-120">BackendAddressPool, BackendHttpSetting, and Routing rule configuration</span></span>

<span data-ttu-id="9dee2-121">BackendAddressPool 是使用的 toodefine 啟用 WebSocket 伺服器的後端集區。</span><span class="sxs-lookup"><span data-stu-id="9dee2-121">A BackendAddressPool is used toodefine a backend pool with WebSocket enabled servers.</span></span> <span data-ttu-id="9dee2-122">hello backendHttpSetting 會定義與後端連接埠 80 和 443。</span><span class="sxs-lookup"><span data-stu-id="9dee2-122">hello backendHttpSetting is defined with a backend port 80 and 443.</span></span> <span data-ttu-id="9dee2-123">以 cookie 為基礎的親和性和 requestTimeouts hello 屬性不相關的 tooWebSocket 流量。</span><span class="sxs-lookup"><span data-stu-id="9dee2-123">hello properties for cookie-based affinity and requestTimeouts are not relevant tooWebSocket traffic.</span></span> <span data-ttu-id="9dee2-124">沒有任何變更，需要在 hello 路由規則，「 基本 」 使用的 tootie hello 適當的接聽程式 toohello 對應後端位址集區。</span><span class="sxs-lookup"><span data-stu-id="9dee2-124">There is no change required in hello routing rule, 'Basic' is used tootie hello appropriate listener toohello corresponding backend address pool.</span></span> 

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

## <a name="websocket-enabled-backend"></a><span data-ttu-id="9dee2-125">已啟用 WebSocket 的後端</span><span class="sxs-lookup"><span data-stu-id="9dee2-125">WebSocket enabled backend</span></span>

<span data-ttu-id="9dee2-126">您的後端必須有 HTTP/HTTPS web 伺服器上設定的 hello 執行 WebSocket toowork 的連接埠 (通常是 80/443)。</span><span class="sxs-lookup"><span data-stu-id="9dee2-126">Your backend must have a HTTP/HTTPS web server running on hello configured port (usually 80/443) for WebSocket toowork.</span></span> <span data-ttu-id="9dee2-127">這是因為 WebSocket 通訊協定需要 hello 初始信號交換 toobe HTTP 標頭欄位升級 tooWebSocket 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="9dee2-127">This requirement is because WebSocket protocol requires hello initial handshake toobe HTTP with upgrade tooWebSocket protocol as a header field.</span></span> <span data-ttu-id="9dee2-128">hello 以下是範例標頭：</span><span class="sxs-lookup"><span data-stu-id="9dee2-128">hello following is an example of a header:</span></span>

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

<span data-ttu-id="9dee2-129">另一個原因是該應用程式閘道後端健全狀態探查只支援 HTTP 和 HTTPS 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="9dee2-129">Another reason for this is that application gateway backend health probe supports HTTP and HTTPS protocols only.</span></span> <span data-ttu-id="9dee2-130">如果 tooHTTP 或 HTTPS 探查 hello 後端伺服器沒有回應，它被帶離後端集區。</span><span class="sxs-lookup"><span data-stu-id="9dee2-130">If hello backend server does not respond tooHTTP or HTTPS probes, it is taken out of backend pool.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9dee2-131">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9dee2-131">Next steps</span></span>

<span data-ttu-id="9dee2-132">在了解 WebSocket 支援之後, 請繼續太[建立應用程式閘道](application-gateway-create-gateway.md)tooget 入門 WebSocket 啟用 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9dee2-132">After learning about WebSocket support, go too[create an application gateway](application-gateway-create-gateway.md) tooget started with a WebSocket enabled web application.</span></span>

