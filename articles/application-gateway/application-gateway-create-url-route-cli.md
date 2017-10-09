---
title: "應用程式閘道使用的 URL 路由規則-aaaCreate Azure CLI 2.0 |Microsoft 文件"
description: "本頁面提供的指示 toocreate、 設定 Azure 應用程式閘道使用的 URL 路由規則"
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
ms.openlocfilehash: 335b52be258945e1172eb0252b732e0e6ecb2ef0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-using-path-based-routing-with-azure-cli-20"></a><span data-ttu-id="fecf6-103">以 Azure CLI 2.0 使用路徑型路由建立應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="fecf6-103">Create an application gateway using Path-based routing with Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="fecf6-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="fecf6-104">Azure portal</span></span>](application-gateway-create-url-route-portal.md)
> * [<span data-ttu-id="fecf6-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="fecf6-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-url-route-arm-ps.md)
> * [<span data-ttu-id="fecf6-106">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="fecf6-106">Azure CLI 2.0</span></span>](application-gateway-create-url-route-cli.md)

<span data-ttu-id="fecf6-107">路徑為基礎的路由 URL 可讓您 tooassociate 路由根據 hello 的 Http 要求的 URL 路徑。</span><span class="sxs-lookup"><span data-stu-id="fecf6-107">URL Path-based routing enables you tooassociate routes based on hello URL path of an Http request.</span></span> <span data-ttu-id="fecf6-108">它會檢查是否顯示 hello 應用程式閘道中的 hello URL 設定的路由 tooa 後端集區，並將傳送 hello 網路流量 toohello 定義後端集區。</span><span class="sxs-lookup"><span data-stu-id="fecf6-108">It checks if there is a route tooa back-end pool configured for hello URL presented in hello Application Gateway and sends hello network traffic toohello defined back-end pool.</span></span> <span data-ttu-id="fecf6-109">URL 為基礎的路由的常見用法是不同的內容類型 toodifferent 後端伺服器集區的 tooload 平衡要求。</span><span class="sxs-lookup"><span data-stu-id="fecf6-109">A common use for URL-based routing is tooload balance requests for different content types toodifferent back-end server pools.</span></span>

<span data-ttu-id="fecf6-110">URL 為基礎的路由導入了新的規則類型 tooapplication 閘道。</span><span class="sxs-lookup"><span data-stu-id="fecf6-110">URL-based routing introduces a new rule type tooapplication gateway.</span></span> <span data-ttu-id="fecf6-111">應用程式閘道具有 2 種規則類型：基本和 PathBasedRouting。</span><span class="sxs-lookup"><span data-stu-id="fecf6-111">Application gateway has two rule types: basic and PathBasedRouting.</span></span> <span data-ttu-id="fecf6-112">基本規則類型提供循環配置資源 hello 後端服務集區時 PathBasedRouting 此外 tooround 環散佈，並選擇 hello 後端集區也會納入考量的 hello 要求 URL 的路徑模式。</span><span class="sxs-lookup"><span data-stu-id="fecf6-112">Basic rule type provides round-robin service for hello back-end pools while PathBasedRouting in addition tooround robin distribution, also takes path pattern of hello request URL into account while choosing hello back-end pool.</span></span>

## <a name="scenario"></a><span data-ttu-id="fecf6-113">案例</span><span class="sxs-lookup"><span data-stu-id="fecf6-113">Scenario</span></span>

<span data-ttu-id="fecf6-114">在下列範例的 hello，應用程式閘道為 contoso.com 的流量提供兩個後端伺服器集區： 預設的伺服器集區以及映像伺服器集區。</span><span class="sxs-lookup"><span data-stu-id="fecf6-114">In hello following example, Application Gateway is serving traffic for contoso.com with two back-end server pools: a default server pool and an image server pool.</span></span>

<span data-ttu-id="fecf6-115">要求的 http://contoso.com/image * tooimage 伺服器集區 (imagesBackendPool) 路由傳送，hello 路徑模式不符，如果已選取預設伺服器集區 (appGatewayBackendPool)。</span><span class="sxs-lookup"><span data-stu-id="fecf6-115">Requests for http://contoso.com/image* are routed tooimage server pool (imagesBackendPool), if hello path pattern does not match, a default server pool (appGatewayBackendPool) is selected.</span></span>

![URL 路由](./media/application-gateway-create-url-route-cli/scenario.png)

## <a name="log-in-tooazure"></a><span data-ttu-id="fecf6-117">登入 tooAzure</span><span class="sxs-lookup"><span data-stu-id="fecf6-117">Log in tooAzure</span></span>

<span data-ttu-id="fecf6-118">開啟 hello **Microsoft Azure 命令提示字元**，並登入。</span><span class="sxs-lookup"><span data-stu-id="fecf6-118">Open hello **Microsoft Azure Command Prompt**, and log in.</span></span> 

```azurecli
az login -u "username"
```

> [!NOTE]
> <span data-ttu-id="fecf6-119">您也可以使用`az login`不需要輸入 aka.ms/devicelogin 在程式碼的裝置登入的 hello 參數。</span><span class="sxs-lookup"><span data-stu-id="fecf6-119">You can also use `az login` without hello switch for device login that requires entering a code at aka.ms/devicelogin.</span></span>

<span data-ttu-id="fecf6-120">一旦您輸入 hello 前面範例中，將程式碼。</span><span class="sxs-lookup"><span data-stu-id="fecf6-120">Once you type hello preceding example, a code is provided.</span></span> <span data-ttu-id="fecf6-121">瀏覽 toohttps://aka.ms/devicelogin 瀏覽器 toocontinue hello 登入處理序。</span><span class="sxs-lookup"><span data-stu-id="fecf6-121">Navigate toohttps://aka.ms/devicelogin in a browser toocontinue hello login process.</span></span>

![顯示裝置登入的 cmd][1]

<span data-ttu-id="fecf6-123">在 hello 瀏覽器中，輸入您收到 hello 程式碼。</span><span class="sxs-lookup"><span data-stu-id="fecf6-123">In hello browser, enter hello code you received.</span></span> <span data-ttu-id="fecf6-124">您已重新導向的 tooa 登入頁面。</span><span class="sxs-lookup"><span data-stu-id="fecf6-124">You are redirected tooa sign-in page.</span></span>

![瀏覽器 tooenter 程式碼][2]

<span data-ttu-id="fecf6-126">一旦輸入 hello 程式碼後您登入，關閉 hello 瀏覽器 toocontinue 與 hello 案例。</span><span class="sxs-lookup"><span data-stu-id="fecf6-126">Once hello code has been entered you are signed in, close hello browser toocontinue on with hello scenario.</span></span>

![已順利登入][3]

## <a name="add-a-path-based-rule-tooan-existing-application-gateway"></a><span data-ttu-id="fecf6-128">新增路徑為基礎的規則 tooan 現有應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="fecf6-128">Add a path-based rule tooan existing application gateway</span></span>

<span data-ttu-id="fecf6-129">建立已定義路徑規則的應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="fecf6-129">Create an application gateway with a path rule defined</span></span>

### <a name="create-a-new-back-end-pool"></a><span data-ttu-id="fecf6-130">建立新的後端集區</span><span class="sxs-lookup"><span data-stu-id="fecf6-130">Create a new back-end pool</span></span>

<span data-ttu-id="fecf6-131">設定應用程式閘道設定**imagesBackendPool** hello hello 後端集區中，負載平衡網路流量。</span><span class="sxs-lookup"><span data-stu-id="fecf6-131">Configure application gateway setting **imagesBackendPool** for hello load-balanced network traffic in hello back-end pool.</span></span> <span data-ttu-id="fecf6-132">在此範例中，您可以設定不同的後端集區設定為 hello 新增後端集區。</span><span class="sxs-lookup"><span data-stu-id="fecf6-132">In this example, you configure different back-end pool settings for hello new back-end pool.</span></span> <span data-ttu-id="fecf6-133">每個後端集區都可以有它自己的後端集區設定。</span><span class="sxs-lookup"><span data-stu-id="fecf6-133">Each back-end pool can have its own back-end pool setting.</span></span>  <span data-ttu-id="fecf6-134">後端 HTTP 設定使用規則 tooroute 流量 toohello 正確的後端集區成員。</span><span class="sxs-lookup"><span data-stu-id="fecf6-134">Backend HTTP settings are used by rules tooroute traffic toohello correct backend pool members.</span></span> <span data-ttu-id="fecf6-135">這會決定 hello 通訊協定和連接埠傳送流量 toohello 後端集區成員時所使用。</span><span class="sxs-lookup"><span data-stu-id="fecf6-135">This determines hello protocol and port that is used when sending traffic toohello backend pool members.</span></span> <span data-ttu-id="fecf6-136">Cookie 架構工作階段，也取決於 hello 後端 HTTP 設定。</span><span class="sxs-lookup"><span data-stu-id="fecf6-136">Cookie-based sessions are also determined by hello backend HTTP settings.</span></span>  <span data-ttu-id="fecf6-137">Cookie 架構工作階段相似性啟用時，會傳送流量 toohello 相同的後端，為每個封包的先前要求。</span><span class="sxs-lookup"><span data-stu-id="fecf6-137">If enabled, cookie-based session affinity sends traffic toohello same backend as previous requests for each packet.</span></span>

```azurecli-interactive
az network application-gateway address-pool create \
--gateway-name AdatumAppGateway \
--name imagesBackendPool  \
--resource-group myresourcegroup \
--servers 10.0.0.6 10.0.0.7
```

### <a name="create-a-new-front-end-port"></a><span data-ttu-id="fecf6-138">建立新的前端連接埠</span><span class="sxs-lookup"><span data-stu-id="fecf6-138">Create a new front-end port</span></span>

<span data-ttu-id="fecf6-139">設定應用程式閘道 hello 前端連接埠。</span><span class="sxs-lookup"><span data-stu-id="fecf6-139">Configure hello front-end port for an application gateway.</span></span> <span data-ttu-id="fecf6-140">hello 前端連接埠組態物件會使用接聽程式 toodefine 哪些連接埠 hello 應用程式閘道接聽 hello 接聽程式上的流量。</span><span class="sxs-lookup"><span data-stu-id="fecf6-140">hello front-end port configuration object is used by a listener toodefine what port hello Application Gateway listens for traffic on hello listener.</span></span>

```azurecli-interactive
az network application-gateway frontend-port create --port 82 --gateway-name AdatumAppGateway --resource-group myresourcegroup --name port82
```

### <a name="create-a-new-listener"></a><span data-ttu-id="fecf6-141">建立新的接聽程式</span><span class="sxs-lookup"><span data-stu-id="fecf6-141">Create a new listener</span></span>

<span data-ttu-id="fecf6-142">Hello 接聽程式設定。</span><span class="sxs-lookup"><span data-stu-id="fecf6-142">Configure hello listener.</span></span> <span data-ttu-id="fecf6-143">此步驟會設定 hello hello 公用 IP 位址的接聽程式，以及使用 tooreceive 連入網路流量的連接埠。</span><span class="sxs-lookup"><span data-stu-id="fecf6-143">This step configures hello listener for hello public IP address and port used tooreceive incoming network traffic.</span></span> <span data-ttu-id="fecf6-144">hello 下列範例會使用前端 IP 組態之前設定的 hello、 前端連接埠組態和通訊協定 （http 或 https），並設定 hello 接聽程式。</span><span class="sxs-lookup"><span data-stu-id="fecf6-144">hello following example takes hello previously configured front-end IP configuration,  front-end port configuration, and a protocol (http or https) and configures hello listener.</span></span> <span data-ttu-id="fecf6-145">在此範例中，hello 接聽 hello 公用 IP 位址上稍早建立的連接埠 82 tooHTTP 流量。</span><span class="sxs-lookup"><span data-stu-id="fecf6-145">In this example, hello listener listens tooHTTP traffic on port 82 on hello public IP address that was created earlier.</span></span>

```azurecli-interactive
az network application-gateway http-listener create --name imageListener --frontend-ip appGatewayFrontendIP  --frontend-port port82 --resource-group myresourcegroup --gateway-name AdatumAppGateway
```

### <a name="create-hello-url-path-map"></a><span data-ttu-id="fecf6-146">建立 hello Url 路徑對應</span><span class="sxs-lookup"><span data-stu-id="fecf6-146">Create hello Url path map</span></span>

<span data-ttu-id="fecf6-147">設定 URL 規則路徑 hello 後端集區。</span><span class="sxs-lookup"><span data-stu-id="fecf6-147">Configure URL rule paths for hello back-end pools.</span></span> <span data-ttu-id="fecf6-148">此步驟會設定應用程式閘道 toodefine hello 對應 URL 路徑與哪一個後端集區指派 toohandle hello 連入流量之間所使用的 hello 相對路徑。</span><span class="sxs-lookup"><span data-stu-id="fecf6-148">This step configures hello relative path used by application gateway toodefine hello mapping between URL path and which back-end pool is assigned toohandle hello incoming traffic.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fecf6-149">每個路徑開頭必須 / 和 hello 唯一地方"\*」 允許，則在 hello 結束。</span><span class="sxs-lookup"><span data-stu-id="fecf6-149">Each path must start with / and hello only place a "\*" is allowed, is at hello end.</span></span> <span data-ttu-id="fecf6-150">有效範例包括 /xyz、/xyz* 或 /xyz/*。</span><span class="sxs-lookup"><span data-stu-id="fecf6-150">Valid examples are /xyz, /xyz* or /xyz/*.</span></span> <span data-ttu-id="fecf6-151">hello fed toohello 路徑比對器的字串不包含任何文字 hello 之後第一次"？"或"#"，且這些字元不得使用。</span><span class="sxs-lookup"><span data-stu-id="fecf6-151">hello string fed toohello path matcher does not include any text after hello first "?" or "#", and those characters are not allowed.</span></span> 

<span data-ttu-id="fecf6-152">hello 下列範例會建立一個規則 」 映像 / / *"路徑路由流量 tooback 端"imagesBackendPool。 」</span><span class="sxs-lookup"><span data-stu-id="fecf6-152">hello following example creates one rule for "/images/*" path routing traffic tooback-end "imagesBackendPool."</span></span> <span data-ttu-id="fecf6-153">此規則可確保每一組 url 的流量路由的 toohello 後端。</span><span class="sxs-lookup"><span data-stu-id="fecf6-153">This rule ensures that traffic for each set of urls is routed toohello backend.</span></span> <span data-ttu-id="fecf6-154">比方說，http://adatum.com/images/figure1.jpg 會太"imagesBackendPool。 」</span><span class="sxs-lookup"><span data-stu-id="fecf6-154">For example, http://adatum.com/images/figure1.jpg goes too"imagesBackendPool."</span></span> <span data-ttu-id="fecf6-155">如果 hello 路徑不符合任何 hello 預先定義的路徑規則，hello 規則路徑對應設定也會設定預設的後端位址集區。</span><span class="sxs-lookup"><span data-stu-id="fecf6-155">If hello path doesn't match any of hello pre-defined path rules, hello rule path map configuration also configures a default back-end address pool.</span></span> <span data-ttu-id="fecf6-156">比方說，http://adatum.com/shoppingcart/test.html 會 toopool1，因為它定義為 hello 預設集區不相符的流量。</span><span class="sxs-lookup"><span data-stu-id="fecf6-156">For example, http://adatum.com/shoppingcart/test.html goes toopool1 as it is defined as hello default pool for unmatched traffic.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="fecf6-157">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fecf6-157">Next steps</span></span>

<span data-ttu-id="fecf6-158">如果您想 toolearn 有關安全通訊端層 (SSL) 卸載時，請參閱[設定 SSL 卸載的應用程式閘道](application-gateway-ssl-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="fecf6-158">If you want toolearn about Secure Sockets Layer (SSL) offload, see [Configure an application gateway for SSL offload](application-gateway-ssl-cli.md).</span></span>


[scenario]: ./media/application-gateway-create-url-route-cli/scenario.png
[1]: ./media/application-gateway-create-url-route-cli/figure1.png
[2]: ./media/application-gateway-create-url-route-cli/figure2.png
[3]: ./media/application-gateway-create-url-route-cli/figure3.png
