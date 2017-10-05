---
title: "使用 URL 路由規則建立應用程式閘道 - Azure CLI 2.0 | Microsoft Docs"
description: "本頁面提供使用 URL 路由規則建立和設定 Azure 應用程式閘道的指示。"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/26/2017
ms.author: gwallace
ms.openlocfilehash: 958049830d6753ec26635f18f8f8b2fabdec0733
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="create-an-application-gateway-using-path-based-routing-with-azure-cli-20"></a><span data-ttu-id="eff23-103">以 Azure CLI 2.0 使用路徑型路由建立應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="eff23-103">Create an application gateway using Path-based routing with Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="eff23-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="eff23-104">Azure portal</span></span>](application-gateway-create-url-route-portal.md)
> * [<span data-ttu-id="eff23-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="eff23-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-url-route-arm-ps.md)
> * [<span data-ttu-id="eff23-106">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="eff23-106">Azure CLI 2.0</span></span>](application-gateway-create-url-route-cli.md)

<span data-ttu-id="eff23-107">以 URL 路徑為基礎的路由可讓您根據 Http 要求的 URL 路徑來關聯路由。</span><span class="sxs-lookup"><span data-stu-id="eff23-107">URL Path-based routing enables you to associate routes based on the URL path of an Http request.</span></span> <span data-ttu-id="eff23-108">它會檢查應用程式閘道中是否有路由指向 URL 設定的後端集區，然後將網路流量傳送至已定義的後端集區。</span><span class="sxs-lookup"><span data-stu-id="eff23-108">It checks if there is a route to a back-end pool configured for the URL presented in the Application Gateway and sends the network traffic to the defined back-end pool.</span></span> <span data-ttu-id="eff23-109">URL 型路由的常見用法是將不同內容類型的要求負載平衡至不同的後端伺服器集區。</span><span class="sxs-lookup"><span data-stu-id="eff23-109">A common use for URL-based routing is to load balance requests for different content types to different back-end server pools.</span></span>

<span data-ttu-id="eff23-110">URL 型路由會將新的規則類型引進應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="eff23-110">URL-based routing introduces a new rule type to application gateway.</span></span> <span data-ttu-id="eff23-111">應用程式閘道具有 2 種規則類型：基本和 PathBasedRouting。</span><span class="sxs-lookup"><span data-stu-id="eff23-111">Application gateway has two rule types: basic and PathBasedRouting.</span></span> <span data-ttu-id="eff23-112">基本規則類型會針對後端集區提供循環配置資源服務，而 PathBasedRouting 除了循環配置資源發佈之外也會在選擇後端集區時將要求 URL 的路徑模式納入考慮。</span><span class="sxs-lookup"><span data-stu-id="eff23-112">Basic rule type provides round-robin service for the back-end pools while PathBasedRouting in addition to round robin distribution, also takes path pattern of the request URL into account while choosing the back-end pool.</span></span>

## <a name="scenario"></a><span data-ttu-id="eff23-113">案例</span><span class="sxs-lookup"><span data-stu-id="eff23-113">Scenario</span></span>

<span data-ttu-id="eff23-114">在下列範例中，應用程式閘道會利用兩個後端伺服器集區來為 contoso.com 提供流量：預設伺服器集區和映像伺服器集區。</span><span class="sxs-lookup"><span data-stu-id="eff23-114">In the following example, Application Gateway is serving traffic for contoso.com with two back-end server pools: a default server pool and an image server pool.</span></span>

<span data-ttu-id="eff23-115">對 http://contoso.com/image* 的要求會路由至映像伺服器集區 (imagesBackendPool)，如果路徑模式不符，就會選取預設的伺服器集區 (appGatewayBackendPool)。</span><span class="sxs-lookup"><span data-stu-id="eff23-115">Requests for http://contoso.com/image* are routed to image server pool (imagesBackendPool), if the path pattern does not match, a default server pool (appGatewayBackendPool) is selected.</span></span>

![URL 路由](./media/application-gateway-create-url-route-cli/scenario.png)

## <a name="log-in-to-azure"></a><span data-ttu-id="eff23-117">登入 Azure</span><span class="sxs-lookup"><span data-stu-id="eff23-117">Log in to Azure</span></span>

<span data-ttu-id="eff23-118">開啟 [Microsoft Azure 命令提示字元] 並登入。</span><span class="sxs-lookup"><span data-stu-id="eff23-118">Open the **Microsoft Azure Command Prompt**, and log in.</span></span> 

```azurecli
az login -u "username"
```

> [!NOTE]
> <span data-ttu-id="eff23-119">您也可以使用 `az login` 而不搭配會要求在 aka.ms/devicelogin 輸入代碼的裝置登入參數。</span><span class="sxs-lookup"><span data-stu-id="eff23-119">You can also use `az login` without the switch for device login that requires entering a code at aka.ms/devicelogin.</span></span>

<span data-ttu-id="eff23-120">輸入上述範例後會提供程式碼。</span><span class="sxs-lookup"><span data-stu-id="eff23-120">Once you type the preceding example, a code is provided.</span></span> <span data-ttu-id="eff23-121">在瀏覽器中瀏覽至 https://aka.ms/devicelogin 以繼續登入程序。</span><span class="sxs-lookup"><span data-stu-id="eff23-121">Navigate to https://aka.ms/devicelogin in a browser to continue the login process.</span></span>

![顯示裝置登入的 cmd][1]

<span data-ttu-id="eff23-123">在瀏覽器中，輸入收到的程式碼。</span><span class="sxs-lookup"><span data-stu-id="eff23-123">In the browser, enter the code you received.</span></span> <span data-ttu-id="eff23-124">系統會將您重新導向至 [登入] 頁面。</span><span class="sxs-lookup"><span data-stu-id="eff23-124">You are redirected to a sign-in page.</span></span>

![要輸入程式碼的瀏覽器][2]

<span data-ttu-id="eff23-126">輸入程式碼後您已登入，請關閉瀏覽器以繼續進行案例。</span><span class="sxs-lookup"><span data-stu-id="eff23-126">Once the code has been entered you are signed in, close the browser to continue on with the scenario.</span></span>

![已順利登入][3]

## <a name="add-a-path-based-rule-to-an-existing-application-gateway"></a><span data-ttu-id="eff23-128">將路徑型規則新增至現有應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="eff23-128">Add a path-based rule to an existing application gateway</span></span>

<span data-ttu-id="eff23-129">建立已定義路徑規則的應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="eff23-129">Create an application gateway with a path rule defined</span></span>

### <a name="create-a-new-back-end-pool"></a><span data-ttu-id="eff23-130">建立新的後端集區</span><span class="sxs-lookup"><span data-stu-id="eff23-130">Create a new back-end pool</span></span>

<span data-ttu-id="eff23-131">為後端集區中負載平衡的網路流量，設定應用程式閘道設定 **imagesBackendPool**。</span><span class="sxs-lookup"><span data-stu-id="eff23-131">Configure application gateway setting **imagesBackendPool** for the load-balanced network traffic in the back-end pool.</span></span> <span data-ttu-id="eff23-132">在此範例中，您會針對新的後端集區設定不同的後端集區設定。</span><span class="sxs-lookup"><span data-stu-id="eff23-132">In this example, you configure different back-end pool settings for the new back-end pool.</span></span> <span data-ttu-id="eff23-133">每個後端集區都可以有它自己的後端集區設定。</span><span class="sxs-lookup"><span data-stu-id="eff23-133">Each back-end pool can have its own back-end pool setting.</span></span>  <span data-ttu-id="eff23-134">規則會使用後端 HTTP 設定，將流量路由傳送至正確的後端集區成員。</span><span class="sxs-lookup"><span data-stu-id="eff23-134">Backend HTTP settings are used by rules to route traffic to the correct backend pool members.</span></span> <span data-ttu-id="eff23-135">這會決定將流量傳送至後端集區成員時使用的通訊協定和連接埠。</span><span class="sxs-lookup"><span data-stu-id="eff23-135">This determines the protocol and port that is used when sending traffic to the backend pool members.</span></span> <span data-ttu-id="eff23-136">Cookie 型工作階段也是由後端 HTTP 設定決定。</span><span class="sxs-lookup"><span data-stu-id="eff23-136">Cookie-based sessions are also determined by the backend HTTP settings.</span></span>  <span data-ttu-id="eff23-137">啟用時，Cookie 型工作階段親和性會如每個封包的先前要求將流量至相同的後端。</span><span class="sxs-lookup"><span data-stu-id="eff23-137">If enabled, cookie-based session affinity sends traffic to the same backend as previous requests for each packet.</span></span>

```azurecli-interactive
az network application-gateway address-pool create \
--gateway-name AdatumAppGateway \
--name imagesBackendPool  \
--resource-group myresourcegroup \
--servers 10.0.0.6 10.0.0.7
```

### <a name="create-a-new-front-end-port"></a><span data-ttu-id="eff23-138">建立新的前端連接埠</span><span class="sxs-lookup"><span data-stu-id="eff23-138">Create a new front-end port</span></span>

<span data-ttu-id="eff23-139">設定應用程式閘道的前端連接埠。</span><span class="sxs-lookup"><span data-stu-id="eff23-139">Configure the front-end port for an application gateway.</span></span> <span data-ttu-id="eff23-140">接聽程式會使用前端連接埠組態物件來定義應用程式閘道會接聽哪個連接埠以取得接聽程式上的流量。</span><span class="sxs-lookup"><span data-stu-id="eff23-140">The front-end port configuration object is used by a listener to define what port the Application Gateway listens for traffic on the listener.</span></span>

```azurecli-interactive
az network application-gateway frontend-port create --port 82 --gateway-name AdatumAppGateway --resource-group myresourcegroup --name port82
```

### <a name="create-a-new-listener"></a><span data-ttu-id="eff23-141">建立新的接聽程式</span><span class="sxs-lookup"><span data-stu-id="eff23-141">Create a new listener</span></span>

<span data-ttu-id="eff23-142">設定接聽程式。</span><span class="sxs-lookup"><span data-stu-id="eff23-142">Configure the listener.</span></span> <span data-ttu-id="eff23-143">這個步驟會針對用來接收連入網路流量的公用 IP 位址和連接埠設定接聽程式。</span><span class="sxs-lookup"><span data-stu-id="eff23-143">This step configures the listener for the public IP address and port used to receive incoming network traffic.</span></span> <span data-ttu-id="eff23-144">下列範例會採用先前設定的前端 IP 設定、前端連接埠設定及通訊協定 (http 或 https)，並設定接聽程式。</span><span class="sxs-lookup"><span data-stu-id="eff23-144">The following example takes the previously configured front-end IP configuration,  front-end port configuration, and a protocol (http or https) and configures the listener.</span></span> <span data-ttu-id="eff23-145">在此範例中，接聽程式會接聽稍早建立的公用 IP 位址上連接埠 82 的 HTTP 流量。</span><span class="sxs-lookup"><span data-stu-id="eff23-145">In this example, the listener listens to HTTP traffic on port 82 on the public IP address that was created earlier.</span></span>

```azurecli-interactive
az network application-gateway http-listener create --name imageListener --frontend-ip appGatewayFrontendIP  --frontend-port port82 --resource-group myresourcegroup --gateway-name AdatumAppGateway
```

### <a name="create-the-url-path-map"></a><span data-ttu-id="eff23-146">建立 URL 路徑對應</span><span class="sxs-lookup"><span data-stu-id="eff23-146">Create the Url path map</span></span>

<span data-ttu-id="eff23-147">設定後端集區的 URL 規則路徑。</span><span class="sxs-lookup"><span data-stu-id="eff23-147">Configure URL rule paths for the back-end pools.</span></span> <span data-ttu-id="eff23-148">這個步驟會設定應用程式閘道用來定義 URL 路徑間對應的相對路徑，而且會指派其中的後端集區來處理連入流量。</span><span class="sxs-lookup"><span data-stu-id="eff23-148">This step configures the relative path used by application gateway to define the mapping between URL path and which back-end pool is assigned to handle the incoming traffic.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="eff23-149">每個路徑都必須以 / 開頭，而且只有結尾允許使用 "\*"。</span><span class="sxs-lookup"><span data-stu-id="eff23-149">Each path must start with / and the only place a "\*" is allowed, is at the end.</span></span> <span data-ttu-id="eff23-150">有效範例包括 /xyz、/xyz* 或 /xyz/*。</span><span class="sxs-lookup"><span data-stu-id="eff23-150">Valid examples are /xyz, /xyz* or /xyz/*.</span></span> <span data-ttu-id="eff23-151">傳送給路徑比對器的字串未在第一個 "?" 或 "#" 之後包含任何文字，而這些字元是不允許的。</span><span class="sxs-lookup"><span data-stu-id="eff23-151">The string fed to the path matcher does not include any text after the first "?" or "#", and those characters are not allowed.</span></span> 

<span data-ttu-id="eff23-152">下列範例會為將流量路由傳送至後端 imagesBackendPool 的 /images/ 路徑建立簡單的規則。</span><span class="sxs-lookup"><span data-stu-id="eff23-152">The following example creates one rule for "/images/*" path routing traffic to back-end "imagesBackendPool."</span></span> <span data-ttu-id="eff23-153">此規則確保每一組 URL 的流量都路由傳送至後端。</span><span class="sxs-lookup"><span data-stu-id="eff23-153">This rule ensures that traffic for each set of urls is routed to the backend.</span></span> <span data-ttu-id="eff23-154">例如，http://adatum.com/images/figure1.jpg 會傳送至 imagesBackendPool。</span><span class="sxs-lookup"><span data-stu-id="eff23-154">For example, http://adatum.com/images/figure1.jpg goes to "imagesBackendPool."</span></span> <span data-ttu-id="eff23-155">如果路徑不符合任何預先定義的路徑規則，規則路徑對應組態也會設定預設的後端位址集區。</span><span class="sxs-lookup"><span data-stu-id="eff23-155">If the path doesn't match any of the pre-defined path rules, the rule path map configuration also configures a default back-end address pool.</span></span> <span data-ttu-id="eff23-156">例如，http://adatum.com/shoppingcart/test.html 會傳送至 pool1，因為它定義為不相符流量的預設集區。</span><span class="sxs-lookup"><span data-stu-id="eff23-156">For example, http://adatum.com/shoppingcart/test.html goes to pool1 as it is defined as the default pool for unmatched traffic.</span></span>

```azurecli-interactive
az network application-gateway url-path-map create \
--gateway-name AdatumAppGateway \
--name imagespathmap \
--paths /images/* \
--resource-group myresourcegroup2 \
--address-pool imagesBackendPool \
--default-address-pool appGatewayBackendPool \
--default-http-settings appGatewayBackendHttpSettings \
--http-settings appGatewayBackendHttpSettings \
--rule-name images
```

## <a name="next-steps"></a><span data-ttu-id="eff23-157">後續步驟</span><span class="sxs-lookup"><span data-stu-id="eff23-157">Next steps</span></span>

<span data-ttu-id="eff23-158">如果您想要了解「安全通訊端層」(SSL) 卸載，請參閱[設定適用於 SSL 卸載的應用程式閘道](application-gateway-ssl-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="eff23-158">If you want to learn about Secure Sockets Layer (SSL) offload, see [Configure an application gateway for SSL offload](application-gateway-ssl-cli.md).</span></span>


[scenario]: ./media/application-gateway-create-url-route-cli/scenario.png
[1]: ./media/application-gateway-create-url-route-cli/figure1.png
[2]: ./media/application-gateway-create-url-route-cli/figure2.png
[3]: ./media/application-gateway-create-url-route-cli/figure3.png
