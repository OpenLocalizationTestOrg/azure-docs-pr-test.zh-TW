---
title: "Azure 應用程式閘道的 WebSocket 支援 | Microsoft Docs"
description: "本頁面提供應用程式閘道 WebSocket 支援的概觀。"
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
ms.openlocfilehash: 75b06ddd02da231b7813c609c848c75e42116da5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="overview-of-websocket-support-in-application-gateway"></a><span data-ttu-id="0cbfa-103">應用程式閘道中的 WebSocket 支援概觀</span><span class="sxs-lookup"><span data-stu-id="0cbfa-103">Overview of WebSocket support in Application Gateway</span></span>

<span data-ttu-id="0cbfa-104">應用程式閘道可跨所有閘道大小對 WebSocket 提供原生支援。</span><span class="sxs-lookup"><span data-stu-id="0cbfa-104">Application Gateway provides native support for WebSocket across all gateway sizes.</span></span> <span data-ttu-id="0cbfa-105">使用者無法進行設定來選擇要啟用或停用 WebSocket 支援。</span><span class="sxs-lookup"><span data-stu-id="0cbfa-105">There is no user-configurable setting to selectively enable or disable WebSocket support.</span></span> 

<span data-ttu-id="0cbfa-106">以 [RFC6455](https://tools.ietf.org/html/rfc6455) 標準化的 WebSocket 通訊協定可透過長時間執行的 TCP 連線讓伺服器和用戶端之間能夠進行全雙工通訊。</span><span class="sxs-lookup"><span data-stu-id="0cbfa-106">WebSocket protocol standardized in [RFC6455](https://tools.ietf.org/html/rfc6455) enables a full duplex communication between a server and a client over a long running TCP connection.</span></span> <span data-ttu-id="0cbfa-107">此功能可讓 Web 伺服器和用戶端之間進行互動性更高的通訊，此通訊可以是雙向的，而不需要像 HTTP 型實作所要求的進行輪詢。</span><span class="sxs-lookup"><span data-stu-id="0cbfa-107">This feature allows for a more interactive communication between the web server and the client, which can be bidirectional without the need for polling as required in HTTP-based implementations.</span></span> <span data-ttu-id="0cbfa-108">不同於 HTTP，WebSocket 的負荷很低，而且可以對多個要求/回應重複使用相同的 TCP 連線，進而提升資源使用效率。</span><span class="sxs-lookup"><span data-stu-id="0cbfa-108">WebSocket has low overhead unlike HTTP and can reuse the same TCP connection for multiple request/responses resulting in a more efficient utilization of resources.</span></span> <span data-ttu-id="0cbfa-109">WebSocket 通訊協定設計為透過傳統 HTTP 連接埠 80 和 443 進行運作。</span><span class="sxs-lookup"><span data-stu-id="0cbfa-109">WebSocket protocols are designed to work over traditional HTTP ports of 80 and 443.</span></span>

<span data-ttu-id="0cbfa-110">您可以在連接埠 80 或 443 上繼續使用標準 HTTP 接聽程式來接收 WebSocket 流量。</span><span class="sxs-lookup"><span data-stu-id="0cbfa-110">You can continue using a standard HTTP listener on port 80 or 443 to receive WebSocket traffic.</span></span> <span data-ttu-id="0cbfa-111">WebSocket 流量接著會使用應用程式閘道規則中指定的適當後端集區，來導向到已啟用 WebSocket 的後端伺服器。</span><span class="sxs-lookup"><span data-stu-id="0cbfa-111">WebSocket traffic is then directed to the WebSocket enabled backend server using the appropriate backend pool as specified in application gateway rules.</span></span> <span data-ttu-id="0cbfa-112">後端伺服器必須回應應用程式閘道探查，[健康情況探查概觀](application-gateway-probe-overview.md)一節中會有所說明。</span><span class="sxs-lookup"><span data-stu-id="0cbfa-112">The backend server must respond to the application gateway probes, which are described in the [health probe overview](application-gateway-probe-overview.md) section.</span></span> <span data-ttu-id="0cbfa-113">應用程式閘道健康情況探查僅限使用 HTTP/HTTPS。</span><span class="sxs-lookup"><span data-stu-id="0cbfa-113">Application gateway health probes are HTTP/HTTPS only.</span></span> <span data-ttu-id="0cbfa-114">每一部後端伺服器都必須回應 HTTP 探查，應用程式閘道才能將 WebSocket 流量路由傳送至伺服器。</span><span class="sxs-lookup"><span data-stu-id="0cbfa-114">Each backend server must respond to HTTP probes for application gateway to route WebSocket traffic to the server.</span></span>

## <a name="listener-configuration-element"></a><span data-ttu-id="0cbfa-115">接聽程式組態元素</span><span class="sxs-lookup"><span data-stu-id="0cbfa-115">Listener configuration element</span></span>

<span data-ttu-id="0cbfa-116">現有的 HTTP 接聽程式可用來支援 WebSocket 流量。</span><span class="sxs-lookup"><span data-stu-id="0cbfa-116">An existing HTTP listener can be used to support WebSocket traffic.</span></span> <span data-ttu-id="0cbfa-117">以下是來自範例範本檔案中 httpListeners 元素的程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="0cbfa-117">The following is a snippet of an httpListeners element from a sample template file.</span></span> <span data-ttu-id="0cbfa-118">您必須同時擁有 HTTP 和 HTTPS 接聽程式才能支援 WebSocket 和保護 WebSocket 流量。</span><span class="sxs-lookup"><span data-stu-id="0cbfa-118">You would need both HTTP and HTTPS listeners to support WebSocket and secure WebSocket traffic.</span></span> <span data-ttu-id="0cbfa-119">同樣地，您可以使用[入口網站](application-gateway-create-gateway-portal.md)或 [PowerShell](application-gateway-create-gateway-arm.md) 在連接埠 80/443 上建立具有接聽程式的應用程式閘道，才能支援 WebSocket 流量。</span><span class="sxs-lookup"><span data-stu-id="0cbfa-119">Similarly you can use the [portal](application-gateway-create-gateway-portal.md) or [PowerShell](application-gateway-create-gateway-arm.md) to create an application gateway with listeners on port 80/443 to support WebSocket traffic.</span></span>

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

## <a name="backendaddresspool-backendhttpsetting-and-routing-rule-configuration"></a><span data-ttu-id="0cbfa-120">BackendAddressPool、BackendHttpSetting 和路由規則組態</span><span class="sxs-lookup"><span data-stu-id="0cbfa-120">BackendAddressPool, BackendHttpSetting, and Routing rule configuration</span></span>

<span data-ttu-id="0cbfa-121">若後端集區具有已啟用 WebSocket 的伺服器，使用 backendAddressPool 加以定義。</span><span class="sxs-lookup"><span data-stu-id="0cbfa-121">A BackendAddressPool is used to define a backend pool with WebSocket enabled servers.</span></span> <span data-ttu-id="0cbfa-122">backendHttpSetting 是以後端連接埠 80 和 443 加以定義。</span><span class="sxs-lookup"><span data-stu-id="0cbfa-122">The backendHttpSetting is defined with a backend port 80 and 443.</span></span> <span data-ttu-id="0cbfa-123">Cookie 型同質性和 requestTimeouts 的屬性與 WebSocket 流量無關。</span><span class="sxs-lookup"><span data-stu-id="0cbfa-123">The properties for cookie-based affinity and requestTimeouts are not relevant to WebSocket traffic.</span></span> <span data-ttu-id="0cbfa-124">路由規則不需要任何變更，'Basic' 用於將適當的接聽程式繫結到對應的後端位址集區。</span><span class="sxs-lookup"><span data-stu-id="0cbfa-124">There is no change required in the routing rule, 'Basic' is used to tie the appropriate listener to the corresponding backend address pool.</span></span> 

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

## <a name="websocket-enabled-backend"></a><span data-ttu-id="0cbfa-125">已啟用 WebSocket 的後端</span><span class="sxs-lookup"><span data-stu-id="0cbfa-125">WebSocket enabled backend</span></span>

<span data-ttu-id="0cbfa-126">後端必須在設定的連接埠 (通常是 80/443) 上執行 HTTP/HTTPS Web 伺服器，WebSocket 才能運作。</span><span class="sxs-lookup"><span data-stu-id="0cbfa-126">Your backend must have a HTTP/HTTPS web server running on the configured port (usually 80/443) for WebSocket to work.</span></span> <span data-ttu-id="0cbfa-127">此需求是因為 WebSocket 通訊協定要求初始交握必須是 HTTP，並以升級為 WebSocket 通訊協定作為標頭欄位。</span><span class="sxs-lookup"><span data-stu-id="0cbfa-127">This requirement is because WebSocket protocol requires the initial handshake to be HTTP with upgrade to WebSocket protocol as a header field.</span></span> <span data-ttu-id="0cbfa-128">以下是標題的範例：</span><span class="sxs-lookup"><span data-stu-id="0cbfa-128">The following is an example of a header:</span></span>

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

<span data-ttu-id="0cbfa-129">另一個原因是該應用程式閘道後端健全狀態探查只支援 HTTP 和 HTTPS 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="0cbfa-129">Another reason for this is that application gateway backend health probe supports HTTP and HTTPS protocols only.</span></span> <span data-ttu-id="0cbfa-130">如果後端伺服器未回應 HTTP 或 HTTPS 探查，它被帶離後端集區。</span><span class="sxs-lookup"><span data-stu-id="0cbfa-130">If the backend server does not respond to HTTP or HTTPS probes, it is taken out of backend pool.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0cbfa-131">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0cbfa-131">Next steps</span></span>

<span data-ttu-id="0cbfa-132">在了解 WebSocket 支援之後，請移至 [建立應用程式閘道](application-gateway-create-gateway.md) 以開始使用已啟用 WebSocket 的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0cbfa-132">After learning about WebSocket support, go to [create an application gateway](application-gateway-create-gateway.md) to get started with a WebSocket enabled web application.</span></span>

