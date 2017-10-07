---
title: "aaaHosting Azure 應用程式閘道上的多個站台 |Microsoft 文件"
description: "此頁面提供 hello 應用程式閘道多站台支援的概觀。"
documentationcenter: na
services: application-gateway
author: amsriva
manager: rossort
editor: 
ms.assetid: 49993fd2-87e5-4a66-b386-8d22056a616d
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/09/2017
ms.author: amsriva
ms.openlocfilehash: 4ab6faa97f1891d7525affdaa36463681bf99e9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="application-gateway-multiple-site-hosting"></a><span data-ttu-id="93a53-103">應用程式閘道多站台裝載</span><span class="sxs-lookup"><span data-stu-id="93a53-103">Application Gateway multiple site hosting</span></span>

<span data-ttu-id="93a53-104">多個站台裝載可讓您 tooconfigure 多個 hello 上的一個 web 應用程式相同的應用程式閘道執行個體。</span><span class="sxs-lookup"><span data-stu-id="93a53-104">Multiple site hosting enables you tooconfigure more than one web application on hello same application gateway instance.</span></span> <span data-ttu-id="93a53-105">這項功能可讓您更有效率地為您的部署拓撲 tooconfigure 新增 too20 網站 tooone 應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="93a53-105">This feature allows you tooconfigure a more efficient topology for your deployments by adding up too20 websites tooone application gateway.</span></span> <span data-ttu-id="93a53-106">每個網站可以導向 tooits 擁有後端集區。</span><span class="sxs-lookup"><span data-stu-id="93a53-106">Each website can be directed tooits own backend pool.</span></span> <span data-ttu-id="93a53-107">在下列範例的 hello，應用程式閘道正在提供服務給 contoso.com 和 fabrikam.com，從稱為 ContosoServerPool 和 FabrikamServerPool 的兩個後端伺服器集區的流量。</span><span class="sxs-lookup"><span data-stu-id="93a53-107">In hello following example, application gateway is serving traffic for contoso.com and fabrikam.com from two back-end server pools called ContosoServerPool and FabrikamServerPool.</span></span>

![imageURLroute](./media/application-gateway-multi-site-overview/multisite.png)

> [!IMPORTANT]
> <span data-ttu-id="93a53-109">規則的處理順序 hello hello 入口網站中列出。</span><span class="sxs-lookup"><span data-stu-id="93a53-109">Rules are processed in hello order they are listed in hello portal.</span></span> <span data-ttu-id="93a53-110">強烈建議使用的 tooconfigure 多站台接聽程式第一次先前 tooconfiguring 基本的接聽程式它。</span><span class="sxs-lookup"><span data-stu-id="93a53-110">It is highly recommended tooconfigure multi-site listeners first prior tooconfiguring a basic listener.</span></span>  <span data-ttu-id="93a53-111">這可確保該流量取得路由的 toohello 帶回結束。</span><span class="sxs-lookup"><span data-stu-id="93a53-111">This will ensure that traffic gets routed toohello right back end.</span></span> <span data-ttu-id="93a53-112">如果先列出了基本接聽程式，且該接聽程式符合傳入的要求，就會由該接聽程式處理。</span><span class="sxs-lookup"><span data-stu-id="93a53-112">If a basic listener is listed first and matches an incoming request, it gets processed by that listener.</span></span>

<span data-ttu-id="93a53-113">Http://contoso.com 的要求，則路由的 tooContosoServerPool，而且 http://fabrikam.com 路由的 tooFabrikamServerPool。</span><span class="sxs-lookup"><span data-stu-id="93a53-113">Requests for http://contoso.com are routed tooContosoServerPool, and http://fabrikam.com are routed tooFabrikamServerPool.</span></span>

<span data-ttu-id="93a53-114">同樣的兩個 hello 可裝載於相同的父系網域的子網域 hello 相同的應用程式閘道部署。</span><span class="sxs-lookup"><span data-stu-id="93a53-114">Similarly two subdomains of hello same parent domain can be hosted on hello same application gateway deployment.</span></span> <span data-ttu-id="93a53-115">使用子網域的範例可能包括單一應用程式閘道部署上裝載的 http://blog.contoso.com 和 http://app.contoso.com。</span><span class="sxs-lookup"><span data-stu-id="93a53-115">Examples of using subdomains could include http://blog.contoso.com and http://app.contoso.com hosted on a single application gateway deployment.</span></span>

## <a name="host-headers-and-server-name-indication-sni"></a><span data-ttu-id="93a53-116">主機標頭和伺服器名稱指示 (SNI)</span><span class="sxs-lookup"><span data-stu-id="93a53-116">Host headers and Server Name Indication (SNI)</span></span>

<span data-ttu-id="93a53-117">有三種常見的機制，可啟用多個站台上裝載 hello 相同基礎結構。</span><span class="sxs-lookup"><span data-stu-id="93a53-117">There are three common mechanisms for enabling multiple site hosting on hello same infrastructure.</span></span>

1. <span data-ttu-id="93a53-118">將多個 Web 應用程式分別裝載在一個唯一的 IP 位址上。</span><span class="sxs-lookup"><span data-stu-id="93a53-118">Host multiple web applications each on a unique IP address.</span></span>
2. <span data-ttu-id="93a53-119">使用主機名稱 toohost hello 上的多個 web 應用程式相同的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="93a53-119">Use host name toohost multiple web applications on hello same IP address.</span></span>
3. <span data-ttu-id="93a53-120">使用不同連接埠 toohost hello 上的多個 web 應用程式相同的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="93a53-120">Use different ports toohost multiple web applications on hello same IP address.</span></span>

<span data-ttu-id="93a53-121">目前應用程式閘道會取得它用來接聽流量的單一公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="93a53-121">Currently an application gateway gets a single public IP address on which it listens for traffic.</span></span> <span data-ttu-id="93a53-122">因此，目前不支援讓多個應用程式分別擁有自己的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="93a53-122">Therefore supporting multiple applications, each with its own IP address, is currently not supported.</span></span> <span data-ttu-id="93a53-123">應用程式閘道支援裝載多個應用程式每個不同的連接埠上接聽，但這種情況下需要非標準連接埠上的 hello 應用程式 tooaccept 流量，並通常不是所需的組態。</span><span class="sxs-lookup"><span data-stu-id="93a53-123">Application Gateway supports hosting multiple applications each listening on different ports but this scenario would require hello applications tooaccept traffic on non-standard ports and is often not a desired configuration.</span></span> <span data-ttu-id="93a53-124">應用程式閘道依賴 HTTP 1.1 以上某個網站上的主機標頭 toohost hello 相同的公開 IP 位址和連接埠。</span><span class="sxs-lookup"><span data-stu-id="93a53-124">Application Gateway relies on HTTP 1.1 host headers toohost more than one website on hello same public IP address and port.</span></span> <span data-ttu-id="93a53-125">應用程式閘道上裝載的 hello 站台也可以使用 TLS 伺服器名稱指示 (SNI) 延伸模組支援 SSL 卸載。</span><span class="sxs-lookup"><span data-stu-id="93a53-125">hello sites hosted on application gateway can also support SSL offload with Server Name Indication (SNI) TLS extension.</span></span> <span data-ttu-id="93a53-126">此案例中，表示該 hello 用戶端瀏覽器和後端 web 伺服陣列必須支援 HTTP/1.1 和 TLS 延伸模組 RFC 6066 中所定義。</span><span class="sxs-lookup"><span data-stu-id="93a53-126">This scenario means that hello client browser and backend web farm must support HTTP/1.1 and TLS extension as defined in RFC 6066.</span></span>

## <a name="listener-configuration-element"></a><span data-ttu-id="93a53-127">接聽程式組態元素</span><span class="sxs-lookup"><span data-stu-id="93a53-127">Listener configuration element</span></span>

<span data-ttu-id="93a53-128">組態項目是現有 HTTPListener 增強 toosupport 主機名稱和伺服器名稱指示項目，這由應用程式閘道 tooroute 流量 tooappropriate 後端集區。</span><span class="sxs-lookup"><span data-stu-id="93a53-128">Existing HTTPListener configuration element is enhanced toosupport host name and server name indication elements, which is used by application gateway tooroute traffic tooappropriate backend pool.</span></span> <span data-ttu-id="93a53-129">hello 下列程式碼範例是 hello httplisteners 的數目的項目從範本檔案的程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="93a53-129">hello following code example is hello snippet of HttpListeners element from template file.</span></span>

```json
"httpListeners": [
    {
        "name": "appGatewayHttpsListener1",
        "properties": {
            "FrontendIPConfiguration": {
                "Id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/frontendIPConfigurations/DefaultFrontendPublicIP"
            },
            "FrontendPort": {
                "Id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/frontendPorts/appGatewayFrontendPort443'"
            },
            "Protocol": "Https",
            "SslCertificate": {
                "Id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/sslCertificates/appGatewaySslCert1'"
            },
            "HostName": "contoso.com",
            "RequireServerNameIndication": "true"
        }
    },
    {
        "name": "appGatewayHttpListener2",
        "properties": {
            "FrontendIPConfiguration": {
                "Id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/frontendIPConfigurations/appGatewayFrontendIP'"
            },
            "FrontendPort": {
                "Id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/frontendPorts/appGatewayFrontendPort80'"
            },
            "Protocol": "Http",
            "HostName": "fabrikam.com",
            "RequireServerNameIndication": "false"
        }
    }
],
```

<span data-ttu-id="93a53-130">您可以瀏覽[Resource Manager 範本使用多個站台裝載](https://github.com/Azure/azure-quickstart-templates/blob/master/201-application-gateway-multihosting)的結束 tooend 範本為基礎的部署。</span><span class="sxs-lookup"><span data-stu-id="93a53-130">You can visit [Resource Manager template using multiple site hosting](https://github.com/Azure/azure-quickstart-templates/blob/master/201-application-gateway-multihosting) for an end tooend template-based deployment.</span></span>

## <a name="routing-rule"></a><span data-ttu-id="93a53-131">路由規則</span><span class="sxs-lookup"><span data-stu-id="93a53-131">Routing rule</span></span>

<span data-ttu-id="93a53-132">沒有任何變更，需要在 hello 路由規則。</span><span class="sxs-lookup"><span data-stu-id="93a53-132">There is no change required in hello routing rule.</span></span> <span data-ttu-id="93a53-133">hello 'Basic' 應該繼續選擇 toobe tootie hello 適當的站台接聽程式 toohello 對應後端位址集區的路由規則。</span><span class="sxs-lookup"><span data-stu-id="93a53-133">hello routing rule 'Basic' should continue toobe chosen tootie hello appropriate site listener toohello corresponding backend address pool.</span></span>

```json
"requestRoutingRules": [
{
    "name": "<ruleName1>",
    "properties": {
        "RuleType": "Basic",
        "httpListener": {
            "id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/httpListeners/appGatewayHttpsListener1')]"
        },
        "backendAddressPool": {
            "id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendAddressPools/ContosoServerPool')]"
        },
        "backendHttpSettings": {
            "id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendHttpSettingsCollection/appGatewayBackendHttpSettings')]"
        }
    }

},
{
    "name": "<ruleName2>",
    "properties": {
        "RuleType": "Basic",
        "httpListener": {
            "id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/httpListeners/appGatewayHttpListener2')]"
        },
        "backendAddressPool": {
            "id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendAddressPools/FabrikamServerPool')]"
        },
        "backendHttpSettings": {
            "id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendHttpSettingsCollection/appGatewayBackendHttpSettings')]"
        }
    }

}
]
```

## <a name="next-steps"></a><span data-ttu-id="93a53-134">後續步驟</span><span class="sxs-lookup"><span data-stu-id="93a53-134">Next steps</span></span>

<span data-ttu-id="93a53-135">在了解多個站台裝載之後, 請繼續太[建立使用多個站台裝載的應用程式閘道](application-gateway-create-multisite-azureresourcemanager-powershell.md)toocreate 能力 toosupport 多超過一個 web 應用程式的應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="93a53-135">After learning about multiple site hosting, go too[create an application gateway using multiple site hosting](application-gateway-create-multisite-azureresourcemanager-powershell.md) toocreate an application gateway with ability toosupport more than one web application.</span></span>

