---
title: "使用 Azure 應用程式閘道裝載多個站台 | Microsoft Docs"
description: "本頁面提供設定現有 Azure 應用程式閘道以在具有 Azure 入口網站的相同閘道上裝載多個 Web 應用程式的指示。"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 95f892f6-fa27-47ee-b980-7abf4f2c66a9
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: 84bd62ae17b7f7ba4cd815ef1f9880679607ebce
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="configure-an-existing-application-gateway-for-hosting-multiple-web-applications"></a><span data-ttu-id="66fb8-103">設定現有應用程式閘道來裝載多個 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="66fb8-103">Configure an existing application gateway for hosting multiple web applications</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="66fb8-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="66fb8-104">Azure portal</span></span>](application-gateway-create-multisite-portal.md)
> * [<span data-ttu-id="66fb8-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="66fb8-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-multisite-azureresourcemanager-powershell.md)
> 
> 

<span data-ttu-id="66fb8-106">多站台裝載可讓您在相同的應用程式閘道上部署多個 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="66fb8-106">Multiple site hosting allows you to deploy more than one web application on the same application gateway.</span></span> <span data-ttu-id="66fb8-107">它需倚賴在連入的 HTTP 要求中有主機標頭存在，以判斷哪一個接聽程式要接收流量。</span><span class="sxs-lookup"><span data-stu-id="66fb8-107">It relies on presence of host header in the incoming HTTP request, to determine which listener would receive traffic.</span></span> <span data-ttu-id="66fb8-108">然後再由接聽程式將流量導向閘道的規則定義中所設定的適當後端集區。</span><span class="sxs-lookup"><span data-stu-id="66fb8-108">The listener then directs traffic to appropriate backend pool as configured in the rules definition of the gateway.</span></span> <span data-ttu-id="66fb8-109">在已啟用 SSL 功能的 Web 應用程式中，則應用程式閘道會依賴「伺服器名稱指示」(SNI) 擴充功能來選擇正確的 Web 流量接聽程式。</span><span class="sxs-lookup"><span data-stu-id="66fb8-109">In SSL enabled web applications, application gateway relies on the Server Name Indication (SNI) extension to choose the correct listener for the web traffic.</span></span> <span data-ttu-id="66fb8-110">多站台裝載的常見用法是將不同 Web 網域的要求負載平衡至不同的後端伺服器集區。</span><span class="sxs-lookup"><span data-stu-id="66fb8-110">A common use for multiple site hosting is to load balance requests for different web domains to different back-end server pools.</span></span> <span data-ttu-id="66fb8-111">同樣地，相同根網域的多個子網域也可以裝載在相同的應用程式閘道上。</span><span class="sxs-lookup"><span data-stu-id="66fb8-111">Similarly multiple subdomains of the same root domain could also be hosted on the same application gateway.</span></span>

## <a name="scenario"></a><span data-ttu-id="66fb8-112">案例</span><span class="sxs-lookup"><span data-stu-id="66fb8-112">Scenario</span></span>

<span data-ttu-id="66fb8-113">在下列範例中，應用程式閘道會利用兩個後端伺服器集區來為 contoso.com 和 fabrikam.com 的流量提供服務：contoso 伺服器集區和 fabrikam 伺服器集區。</span><span class="sxs-lookup"><span data-stu-id="66fb8-113">In the following example, application gateway is serving traffic for contoso.com and fabrikam.com with two back-end server pools: contoso server pool and fabrikam server pool.</span></span> <span data-ttu-id="66fb8-114">類似的設定也可用來裝載子網域，例如 app.contoso.com 和 blog.contoso.com。</span><span class="sxs-lookup"><span data-stu-id="66fb8-114">Similar setup could be used to host subdomains like app.contoso.com and blog.contoso.com.</span></span>

![多網站案例][multisite]

## <a name="before-you-begin"></a><span data-ttu-id="66fb8-116">開始之前</span><span class="sxs-lookup"><span data-stu-id="66fb8-116">Before you begin</span></span>

<span data-ttu-id="66fb8-117">這個案例會將多網站支援新增至現有應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="66fb8-117">This scenario adds multi-site support to an existing application gateway.</span></span> <span data-ttu-id="66fb8-118">若要完成此案例，現有的應用程式閘道必須可供設定。</span><span class="sxs-lookup"><span data-stu-id="66fb8-118">To complete this scenario, an existing application gateway needs to be available to configure.</span></span> <span data-ttu-id="66fb8-119">請造訪[使用入口網站建立應用程式閘道](application-gateway-create-gateway-portal.md)，以了解如何在入口網站中建立基本應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="66fb8-119">Visit [Create an application gateway by using the portal](application-gateway-create-gateway-portal.md) to learn how to create a basic application gateway in the portal.</span></span>

<span data-ttu-id="66fb8-120">以下是更新應用程式閘道所需的步驟：</span><span class="sxs-lookup"><span data-stu-id="66fb8-120">The following are the steps needed to update the application gateway:</span></span>

1. <span data-ttu-id="66fb8-121">建立要用於每個網站的後端集區。</span><span class="sxs-lookup"><span data-stu-id="66fb8-121">Create back-end pools to use for each site.</span></span>
2. <span data-ttu-id="66fb8-122">建立每個網站應用程式閘道都支援的接聽程式。</span><span class="sxs-lookup"><span data-stu-id="66fb8-122">Create a listener for each site application gateway supports.</span></span>
3. <span data-ttu-id="66fb8-123">建立規則，將每個接聽程式與適當的後端對應。</span><span class="sxs-lookup"><span data-stu-id="66fb8-123">Create rules to map each listener with the appropriate back-end.</span></span>

## <a name="requirements"></a><span data-ttu-id="66fb8-124">需求</span><span class="sxs-lookup"><span data-stu-id="66fb8-124">Requirements</span></span>

* <span data-ttu-id="66fb8-125">**後端伺服器集區：** 後端伺服器的 IP 位址清單。</span><span class="sxs-lookup"><span data-stu-id="66fb8-125">**Back-end server pool:** The list of IP addresses of the back-end servers.</span></span> <span data-ttu-id="66fb8-126">列出的 IP 位址應屬於虛擬網路子網路或是公用 IP/VIP。</span><span class="sxs-lookup"><span data-stu-id="66fb8-126">The IP addresses listed should either belong to the virtual network subnet or should be a public IP/VIP.</span></span> <span data-ttu-id="66fb8-127">您也可以使用 FQDN。</span><span class="sxs-lookup"><span data-stu-id="66fb8-127">FQDN can also be used.</span></span>
* <span data-ttu-id="66fb8-128">**後端伺服器集區設定：** 每個集區都包括一些設定，例如連接埠、通訊協定和以 Cookie 為基礎的同質性。</span><span class="sxs-lookup"><span data-stu-id="66fb8-128">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="66fb8-129">這些設定會繫結至集區，並套用至集區內所有伺服器。</span><span class="sxs-lookup"><span data-stu-id="66fb8-129">These settings are tied to a pool and are applied to all servers within the pool.</span></span>
* <span data-ttu-id="66fb8-130">**前端連接埠：** 此連接埠是在應用程式閘道上開啟的公用連接埠。</span><span class="sxs-lookup"><span data-stu-id="66fb8-130">**Front-end port:** This port is the public port that is opened on the application gateway.</span></span> <span data-ttu-id="66fb8-131">流量會到達此連接埠，然後重新導向至其中一個後端伺服器。</span><span class="sxs-lookup"><span data-stu-id="66fb8-131">Traffic hits this port, and then gets redirected to one of the back-end servers.</span></span>
* <span data-ttu-id="66fb8-132">**接聽程式：** 接聽程式具有前端連接埠、通訊協定 (Http 或 Https，這些值都區分大小寫) 和 SSL 憑證名稱 (如果已設定 SSL 卸載)。</span><span class="sxs-lookup"><span data-stu-id="66fb8-132">**Listener:** The listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span> <span data-ttu-id="66fb8-133">針對啟用多站台功能的應用程式閘道，會一併新增主機名稱和 SNI 指示器。</span><span class="sxs-lookup"><span data-stu-id="66fb8-133">For multi-site enabled application gateways, host name and SNI indicators are also added.</span></span>
* <span data-ttu-id="66fb8-134">**規則：**規則會繫結接聽程式和後端伺服器集區，並定義流量達到特定接聽程式時應該導向至哪個後端伺服器集區。</span><span class="sxs-lookup"><span data-stu-id="66fb8-134">**Rule:** The rule binds the listener, the back-end server pool, and defines which back-end server pool the traffic should be directed to when it hits a particular listener.</span></span> <span data-ttu-id="66fb8-135">會以規則列出的順序進行處理，且不論精確性，都會透過相符的第一個規則將流量進行導向。</span><span class="sxs-lookup"><span data-stu-id="66fb8-135">Rules are processed in the order they are listed, and traffic will be directed via the first rule that matches regardless of specificity.</span></span> <span data-ttu-id="66fb8-136">例如，如果您在相同的連接埠上同時使用基本接聽程式的規則和多站台接聽程式的規則，則必須將多站台接聽程式的規則列於基本接聽程式的規則之前，多站台規則才能如預期般運作。</span><span class="sxs-lookup"><span data-stu-id="66fb8-136">For example, if you have a rule using a basic listener and a rule using a multi-site listener both on the same port, the rule with the multi-site listener must be listed before the rule with the basic listener in order for the multi-site rule to function as expected.</span></span> 
* <span data-ttu-id="66fb8-137">**憑證︰**每個接聽程式需要唯一的憑證，在此範例中針對多網站建立 2 個接聽程式。</span><span class="sxs-lookup"><span data-stu-id="66fb8-137">**Certificates:** Each listener requires a unique certificate, in this example 2 listeners are created for multi-site.</span></span> <span data-ttu-id="66fb8-138">必須建立兩個 .pfx 憑證和它們的密碼。</span><span class="sxs-lookup"><span data-stu-id="66fb8-138">Two .pfx certificates and the passwords for them need to be created.</span></span>

## <a name="create-back-end-pools-for-each-site"></a><span data-ttu-id="66fb8-139">建立每個網站的後端集區</span><span class="sxs-lookup"><span data-stu-id="66fb8-139">Create back-end pools for each site</span></span>

<span data-ttu-id="66fb8-140">需要應用程式閘道支援之每個網站的後端集區，在此案例中會建立 2 個，一個用於 contoso11.com，另一個用於 fabrikam11.com。</span><span class="sxs-lookup"><span data-stu-id="66fb8-140">A back-end pool for each site that application gateway supports is needed, in this case 2 are be created, one for contoso11.com and one for fabrikam11.com.</span></span>

### <a name="step-1"></a><span data-ttu-id="66fb8-141">步驟 1</span><span class="sxs-lookup"><span data-stu-id="66fb8-141">Step 1</span></span>

<span data-ttu-id="66fb8-142">瀏覽至 Azure 入口網站中現有的應用程式閘道 ( https://portal.azure.com ) 。</span><span class="sxs-lookup"><span data-stu-id="66fb8-142">Navigate to an existing application gateway in the Azure portal (https://portal.azure.com).</span></span> <span data-ttu-id="66fb8-143">選取 [後端集區]，按一下 [新增]</span><span class="sxs-lookup"><span data-stu-id="66fb8-143">Select **Backend pools** and click **Add**</span></span>

![新增後端集區][7]

### <a name="step-2"></a><span data-ttu-id="66fb8-145">步驟 2</span><span class="sxs-lookup"><span data-stu-id="66fb8-145">Step 2</span></span>

<span data-ttu-id="66fb8-146">針對後端集區 **pool1** 填入資訊，新增後端伺服器的 ip 位址或 FQDN，然後按一下 [確定]</span><span class="sxs-lookup"><span data-stu-id="66fb8-146">Fill in the information for the back-end pool **pool1**, adding the ip addresses or FQDNs for the back-end servers and click **OK**</span></span>

![後端集區 pool1 設定][8]

### <a name="step-3"></a><span data-ttu-id="66fb8-148">步驟 3</span><span class="sxs-lookup"><span data-stu-id="66fb8-148">Step 3</span></span>

<span data-ttu-id="66fb8-149">在後端集區刀鋒視窗上按一下 [新增] 以新增額外的後端集區 **pool2**，新增後端伺服器的 ip 位址或 FQDN，然後按一下 **[確定]**</span><span class="sxs-lookup"><span data-stu-id="66fb8-149">On the backend-pools blade click **Add** to add an additional back-end pool **pool2**, adding the ip addresses or FQDNS for the back-end servers and click **OK**</span></span>

![後端集區 pool2 設定][9]

## <a name="create-listeners-for-each-back-end"></a><span data-ttu-id="66fb8-151">建立每個後端的接聽程式</span><span class="sxs-lookup"><span data-stu-id="66fb8-151">Create listeners for each back-end</span></span>

<span data-ttu-id="66fb8-152">「應用程式閘道」需依賴 HTTP 1.1 主機標頭，才能在相同的公用 IP 位址和連接埠上裝載多個網站。</span><span class="sxs-lookup"><span data-stu-id="66fb8-152">Application Gateway relies on HTTP 1.1 host headers to host more than one website on the same public IP address and port.</span></span> <span data-ttu-id="66fb8-153">在入口網站中建立的基本接聽程式不包含這個屬性。</span><span class="sxs-lookup"><span data-stu-id="66fb8-153">The basic listener created in the portal does not contain this property.</span></span>

### <a name="step-1"></a><span data-ttu-id="66fb8-154">步驟 1</span><span class="sxs-lookup"><span data-stu-id="66fb8-154">Step 1</span></span>

<span data-ttu-id="66fb8-155">按一下現有應用程式閘道上的 [接聽程式]，然後按一下 [多網站] 以新增第一個接聽程式。</span><span class="sxs-lookup"><span data-stu-id="66fb8-155">Click **Listeners** on the existing application gateway and click **Multi-site** to add the first listener.</span></span>

![接聽程式概觀刀鋒視窗][1]

### <a name="step-2"></a><span data-ttu-id="66fb8-157">步驟 2</span><span class="sxs-lookup"><span data-stu-id="66fb8-157">Step 2</span></span>

<span data-ttu-id="66fb8-158">填入接聽程式的資訊。</span><span class="sxs-lookup"><span data-stu-id="66fb8-158">Fill out the information for the listener.</span></span> <span data-ttu-id="66fb8-159">在此範例中，會設定 SSL 終止，建立新的前端連接埠。</span><span class="sxs-lookup"><span data-stu-id="66fb8-159">In this example SSL termination is configured, create a new frontend port.</span></span> <span data-ttu-id="66fb8-160">上傳 .pfx 憑證，用於進行 SSL 終止。</span><span class="sxs-lookup"><span data-stu-id="66fb8-160">Upload the .pfx certificate to be used for SSL termination.</span></span> <span data-ttu-id="66fb8-161">此刀鋒視窗上相較於標準基本接聽程式刀鋒視窗的唯一差別是主機名稱。</span><span class="sxs-lookup"><span data-stu-id="66fb8-161">The only difference on this blade compared to the standard basic listener blade is the hostname.</span></span>

![接聽程式屬性刀鋒視窗][2]

### <a name="step-3"></a><span data-ttu-id="66fb8-163">步驟 3</span><span class="sxs-lookup"><span data-stu-id="66fb8-163">Step 3</span></span>

<span data-ttu-id="66fb8-164">按一下 [多網站]，並且針對第二個網站建立另一個接聽程式，如同上一個步驟所述。</span><span class="sxs-lookup"><span data-stu-id="66fb8-164">Click **Multi-site** and create another listener as described in the previous step for the second site.</span></span> <span data-ttu-id="66fb8-165">請確定針對第二個接聽程式使用不同的憑證。</span><span class="sxs-lookup"><span data-stu-id="66fb8-165">Make sure to use a different certificate for the second listener.</span></span> <span data-ttu-id="66fb8-166">此刀鋒視窗上相較於標準基本接聽程式刀鋒視窗的唯一差別是主機名稱。</span><span class="sxs-lookup"><span data-stu-id="66fb8-166">The only difference on this blade compared to the standard basic listener blade is the hostname.</span></span> <span data-ttu-id="66fb8-167">填入接聽程式的資訊，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="66fb8-167">Fill out the information for the listener and click **OK**.</span></span>

![接聽程式屬性刀鋒視窗][3]

> [!NOTE]
> <span data-ttu-id="66fb8-169">在 Azure 入口網站中針對應用程式閘道建立接聽程式是長時間執行的工作，在此案例中可能需要一段時間來建立兩個接聽程式。</span><span class="sxs-lookup"><span data-stu-id="66fb8-169">Creation of listeners in the Azure portal for application gateway is a long running task, it may take some time to create the two listeners in this scenario.</span></span> <span data-ttu-id="66fb8-170">完成時，入口網站中的接聽程式如下圖所示：</span><span class="sxs-lookup"><span data-stu-id="66fb8-170">When complete the listeners show in the portal as seen in the following image:</span></span>

![接聽程式概觀][4]

## <a name="create-rules-to-map-listeners-to-backend-pools"></a><span data-ttu-id="66fb8-172">建立規則，將接聽程式對應至後端集區</span><span class="sxs-lookup"><span data-stu-id="66fb8-172">Create rules to map listeners to backend pools</span></span>

### <a name="step-1"></a><span data-ttu-id="66fb8-173">步驟 1</span><span class="sxs-lookup"><span data-stu-id="66fb8-173">Step 1</span></span>

<span data-ttu-id="66fb8-174">瀏覽至 Azure 入口網站中現有的應用程式閘道 ( https://portal.azure.com ) 。</span><span class="sxs-lookup"><span data-stu-id="66fb8-174">Navigate to an existing application gateway in the Azure portal (https://portal.azure.com).</span></span> <span data-ttu-id="66fb8-175">選取 [規則]，選擇現有的預設規則 **rule1**，然後按一下 [編輯]。</span><span class="sxs-lookup"><span data-stu-id="66fb8-175">Select **Rules** and choose the existing default rule **rule1** and click **Edit**.</span></span>

### <a name="step-2"></a><span data-ttu-id="66fb8-176">步驟 2</span><span class="sxs-lookup"><span data-stu-id="66fb8-176">Step 2</span></span>

<span data-ttu-id="66fb8-177">填寫 [規則] 刀鋒視窗，如下圖所示。</span><span class="sxs-lookup"><span data-stu-id="66fb8-177">Fill out the rules blade as seen in the following image.</span></span> <span data-ttu-id="66fb8-178">選擇第一個接聽程式和第一個集區，完成時按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="66fb8-178">Choosing the first listener and first pool and clicking **Save** when complete.</span></span>

![編輯現有的規則][6]

### <a name="step-3"></a><span data-ttu-id="66fb8-180">步驟 3</span><span class="sxs-lookup"><span data-stu-id="66fb8-180">Step 3</span></span>

<span data-ttu-id="66fb8-181">按一下 [基本規則] 以建立第 2 個規則。</span><span class="sxs-lookup"><span data-stu-id="66fb8-181">Click **Basic rule** to create the second rule.</span></span> <span data-ttu-id="66fb8-182">以第二個接聽程式和第二個後端集區填寫表單，按一下 [確定] 以儲存。</span><span class="sxs-lookup"><span data-stu-id="66fb8-182">Fill out the form with the second listener and second backend pool and click **OK** to save.</span></span>

![新增基本規則刀鋒視窗][10]

<span data-ttu-id="66fb8-184">此案例會完成透過 Azure 入口網站設定具有多網站支援的現有應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="66fb8-184">This scenario completes configuring an existing application gateway with multi-site support through the Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="66fb8-185">後續步驟</span><span class="sxs-lookup"><span data-stu-id="66fb8-185">Next steps</span></span>

<span data-ttu-id="66fb8-186">了解如何使用[應用程式閘道 - Web 應用程式防火牆](application-gateway-webapplicationfirewall-overview.md)保護您的網站</span><span class="sxs-lookup"><span data-stu-id="66fb8-186">Learn how to protect your websites with [Application Gateway - Web Application Firewall](application-gateway-webapplicationfirewall-overview.md)</span></span>

<!--Image references-->
[1]: ./media/application-gateway-create-multisite-portal/figure1.png
[2]: ./media/application-gateway-create-multisite-portal/figure2.png
[3]: ./media/application-gateway-create-multisite-portal/figure3.png
[4]: ./media/application-gateway-create-multisite-portal/figure4.png
[5]: ./media/application-gateway-create-multisite-portal/figure5.png
[6]: ./media/application-gateway-create-multisite-portal/figure6.png
[7]: ./media/application-gateway-create-multisite-portal/figure7.png
[8]: ./media/application-gateway-create-multisite-portal/figure8.png
[9]: ./media/application-gateway-create-multisite-portal/figure9.png
[10]: ./media/application-gateway-create-multisite-portal/figure10.png
[multisite]: ./media/application-gateway-create-multisite-portal/multisite.png
