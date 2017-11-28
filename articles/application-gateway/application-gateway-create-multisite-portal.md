---
title: "aaaHost 與 Azure 應用程式閘道的多個站台 |Microsoft 文件"
description: "此頁面會提供指示 tooconfigure 現有的 Azure 應用程式閘道器裝載 hello 上的多個 web 應用程式相同的閘道器以 hello Azure 入口網站。"
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
ms.openlocfilehash: 2172aa2c80720f6f1ab7dd91745b44654bcaee00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-existing-application-gateway-for-hosting-multiple-web-applications"></a><span data-ttu-id="edf68-103">設定現有應用程式閘道來裝載多個 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="edf68-103">Configure an existing application gateway for hosting multiple web applications</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="edf68-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="edf68-104">Azure portal</span></span>](application-gateway-create-multisite-portal.md)
> * [<span data-ttu-id="edf68-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="edf68-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-multisite-azureresourcemanager-powershell.md)
> 
> 

<span data-ttu-id="edf68-106">多個站台裝載可讓您以上一個 web 應用程式的 toodeploy hello 上相同的應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="edf68-106">Multiple site hosting allows you toodeploy more than one web application on hello same application gateway.</span></span> <span data-ttu-id="edf68-107">它依賴在 hello 的傳入 HTTP 要求，而 toodetermine 的接聽程式將會收到流量的主機標頭存在。</span><span class="sxs-lookup"><span data-stu-id="edf68-107">It relies on presence of host header in hello incoming HTTP request, toodetermine which listener would receive traffic.</span></span> <span data-ttu-id="edf68-108">hello 接聽程式，然後指示流量 tooappropriate 後端集區中的 hello 閘道 hello 規則定義的設定。</span><span class="sxs-lookup"><span data-stu-id="edf68-108">hello listener then directs traffic tooappropriate backend pool as configured in hello rules definition of hello gateway.</span></span> <span data-ttu-id="edf68-109">在啟用 SSL 的 web 應用程式，應用程式閘道依賴 hello 伺服器名稱指示 (SNI) 延伸模組 toochoose hello 正確接聽程式 hello 網路流量。</span><span class="sxs-lookup"><span data-stu-id="edf68-109">In SSL enabled web applications, application gateway relies on hello Server Name Indication (SNI) extension toochoose hello correct listener for hello web traffic.</span></span> <span data-ttu-id="edf68-110">多個站台裝載的常見用法是不同的網頁網域 toodifferent 後端伺服器集區的 tooload 平衡要求。</span><span class="sxs-lookup"><span data-stu-id="edf68-110">A common use for multiple site hosting is tooload balance requests for different web domains toodifferent back-end server pools.</span></span> <span data-ttu-id="edf68-111">同樣的多個相同的根網域也無法裝載在 hello 的子網域 hello 相同的應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="edf68-111">Similarly multiple subdomains of hello same root domain could also be hosted on hello same application gateway.</span></span>

## <a name="scenario"></a><span data-ttu-id="edf68-112">案例</span><span class="sxs-lookup"><span data-stu-id="edf68-112">Scenario</span></span>

<span data-ttu-id="edf68-113">在下列範例的 hello，應用程式閘道為 contoso.com 和 fabrikam.com 的流量提供兩個後端伺服器集區： contoso 伺服器集區及 fabrikam 伺服器集區。</span><span class="sxs-lookup"><span data-stu-id="edf68-113">In hello following example, application gateway is serving traffic for contoso.com and fabrikam.com with two back-end server pools: contoso server pool and fabrikam server pool.</span></span> <span data-ttu-id="edf68-114">類似的安裝程式可能使用的 toohost 子網域，例如 app.contoso.com 和 blog.contoso.com。</span><span class="sxs-lookup"><span data-stu-id="edf68-114">Similar setup could be used toohost subdomains like app.contoso.com and blog.contoso.com.</span></span>

![多網站案例][multisite]

## <a name="before-you-begin"></a><span data-ttu-id="edf68-116">開始之前</span><span class="sxs-lookup"><span data-stu-id="edf68-116">Before you begin</span></span>

<span data-ttu-id="edf68-117">這個案例會新增多站台支援 tooan 現有應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="edf68-117">This scenario adds multi-site support tooan existing application gateway.</span></span> <span data-ttu-id="edf68-118">toocomplete 此案例中，現有的應用程式閘道需要 toobe 可用 tooconfigure。</span><span class="sxs-lookup"><span data-stu-id="edf68-118">toocomplete this scenario, an existing application gateway needs toobe available tooconfigure.</span></span> <span data-ttu-id="edf68-119">請瀏覽[透過 hello 入口網站建立應用程式閘道](application-gateway-create-gateway-portal.md)toolearn 如何 toocreate hello 入口網站中的基本應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="edf68-119">Visit [Create an application gateway by using hello portal](application-gateway-create-gateway-portal.md) toolearn how toocreate a basic application gateway in hello portal.</span></span>

<span data-ttu-id="edf68-120">hello 以下是需要 tooupdate hello 應用程式閘道 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="edf68-120">hello following are hello steps needed tooupdate hello application gateway:</span></span>

1. <span data-ttu-id="edf68-121">建立每個站台的後端集區 toouse。</span><span class="sxs-lookup"><span data-stu-id="edf68-121">Create back-end pools toouse for each site.</span></span>
2. <span data-ttu-id="edf68-122">建立每個網站應用程式閘道都支援的接聽程式。</span><span class="sxs-lookup"><span data-stu-id="edf68-122">Create a listener for each site application gateway supports.</span></span>
3. <span data-ttu-id="edf68-123">建立 hello 適當後端規則 toomap 每個接聽程式。</span><span class="sxs-lookup"><span data-stu-id="edf68-123">Create rules toomap each listener with hello appropriate back-end.</span></span>

## <a name="requirements"></a><span data-ttu-id="edf68-124">需求</span><span class="sxs-lookup"><span data-stu-id="edf68-124">Requirements</span></span>

* <span data-ttu-id="edf68-125">**後端伺服器集區：** hello hello 後端伺服器的 IP 位址清單。</span><span class="sxs-lookup"><span data-stu-id="edf68-125">**Back-end server pool:** hello list of IP addresses of hello back-end servers.</span></span> <span data-ttu-id="edf68-126">列出 hello IP 位址應該是屬於 toohello 虛擬網路子網路，或應該是公用 IP/VIP。</span><span class="sxs-lookup"><span data-stu-id="edf68-126">hello IP addresses listed should either belong toohello virtual network subnet or should be a public IP/VIP.</span></span> <span data-ttu-id="edf68-127">您也可以使用 FQDN。</span><span class="sxs-lookup"><span data-stu-id="edf68-127">FQDN can also be used.</span></span>
* <span data-ttu-id="edf68-128">**後端伺服器集區設定：** 每個集區都包括一些設定，例如連接埠、通訊協定和以 Cookie 為基礎的同質性。</span><span class="sxs-lookup"><span data-stu-id="edf68-128">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="edf68-129">這些設定會繫結的 tooa 集區，並套用的 tooall hello 集區內的伺服器。</span><span class="sxs-lookup"><span data-stu-id="edf68-129">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="edf68-130">**前端連接埠：**此連接埠是開啟 hello 應用程式閘道上的 hello 公用連接埠。</span><span class="sxs-lookup"><span data-stu-id="edf68-130">**Front-end port:** This port is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="edf68-131">流量叫用這個連接埠，然後再取得重新導向 tooone 的 hello 後端伺服器。</span><span class="sxs-lookup"><span data-stu-id="edf68-131">Traffic hits this port, and then gets redirected tooone of hello back-end servers.</span></span>
* <span data-ttu-id="edf68-132">**接聽程式：** hello 接聽程式有前端連接埠的通訊協定 （Http 或 Https，這些值會區分大小寫），與 hello 的 SSL 憑證名稱 （如果有設定 SSL 卸載）。</span><span class="sxs-lookup"><span data-stu-id="edf68-132">**Listener:** hello listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span> <span data-ttu-id="edf68-133">針對啟用多站台功能的應用程式閘道，會一併新增主機名稱和 SNI 指示器。</span><span class="sxs-lookup"><span data-stu-id="edf68-133">For multi-site enabled application gateways, host name and SNI indicators are also added.</span></span>
* <span data-ttu-id="edf68-134">**規則：** hello 規則繫結 hello 接聽程式，hello 後端伺服器集區，並定義哪一個後端伺服器集區 hello 流量應導向的 toowhen 配接器特定接聽程式。</span><span class="sxs-lookup"><span data-stu-id="edf68-134">**Rule:** hello rule binds hello listener, hello back-end server pool, and defines which back-end server pool hello traffic should be directed toowhen it hits a particular listener.</span></span> <span data-ttu-id="edf68-135">規則會在處理 hello 排列順序，而且將會導向流量，透過 hello 比對，不論明確性比較的第一個規則。</span><span class="sxs-lookup"><span data-stu-id="edf68-135">Rules are processed in hello order they are listed, and traffic will be directed via hello first rule that matches regardless of specificity.</span></span> <span data-ttu-id="edf68-136">比方說，如果您有使用基本的接聽程式的規則和規則，使用多站台接聽程式同時在相同連接埠，與 hello 規則 hello hello 多站台接聽程式必須列出 hello 規則之前為 hello 多站台規則 toofunction 順序中的 hello 基本接聽程式預期的。</span><span class="sxs-lookup"><span data-stu-id="edf68-136">For example, if you have a rule using a basic listener and a rule using a multi-site listener both on hello same port, hello rule with hello multi-site listener must be listed before hello rule with hello basic listener in order for hello multi-site rule toofunction as expected.</span></span> 
* <span data-ttu-id="edf68-137">**憑證︰**每個接聽程式需要唯一的憑證，在此範例中針對多網站建立 2 個接聽程式。</span><span class="sxs-lookup"><span data-stu-id="edf68-137">**Certificates:** Each listener requires a unique certificate, in this example 2 listeners are created for multi-site.</span></span> <span data-ttu-id="edf68-138">兩個.pfx 憑證和它們的 hello 密碼需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="edf68-138">Two .pfx certificates and hello passwords for them need toobe created.</span></span>

## <a name="create-back-end-pools-for-each-site"></a><span data-ttu-id="edf68-139">建立每個網站的後端集區</span><span class="sxs-lookup"><span data-stu-id="edf68-139">Create back-end pools for each site</span></span>

<span data-ttu-id="edf68-140">需要應用程式閘道支援之每個網站的後端集區，在此案例中會建立 2 個，一個用於 contoso11.com，另一個用於 fabrikam11.com。</span><span class="sxs-lookup"><span data-stu-id="edf68-140">A back-end pool for each site that application gateway supports is needed, in this case 2 are be created, one for contoso11.com and one for fabrikam11.com.</span></span>

### <a name="step-1"></a><span data-ttu-id="edf68-141">步驟 1</span><span class="sxs-lookup"><span data-stu-id="edf68-141">Step 1</span></span>

<span data-ttu-id="edf68-142">瀏覽 tooan 現有應用程式閘道 hello Azure 入口網站 (https://portal.azure.com) 中。</span><span class="sxs-lookup"><span data-stu-id="edf68-142">Navigate tooan existing application gateway in hello Azure portal (https://portal.azure.com).</span></span> <span data-ttu-id="edf68-143">選取 [後端集區]，按一下 [新增]</span><span class="sxs-lookup"><span data-stu-id="edf68-143">Select **Backend pools** and click **Add**</span></span>

![新增後端集區][7]

### <a name="step-2"></a><span data-ttu-id="edf68-145">步驟 2</span><span class="sxs-lookup"><span data-stu-id="edf68-145">Step 2</span></span>

<span data-ttu-id="edf68-146">填寫 hello 後端集區的 hello 資訊**pool1**，新增 hello 後端伺服器 hello ip 位址或 Fqdn，然後按一下**[確定]**</span><span class="sxs-lookup"><span data-stu-id="edf68-146">Fill in hello information for hello back-end pool **pool1**, adding hello ip addresses or FQDNs for hello back-end servers and click **OK**</span></span>

![後端集區 pool1 設定][8]

### <a name="step-3"></a><span data-ttu-id="edf68-148">步驟 3</span><span class="sxs-lookup"><span data-stu-id="edf68-148">Step 3</span></span>

<span data-ttu-id="edf68-149">在 [hello 後端集區] 刀鋒視窗上按一下**新增**tooadd 額外的後端集區**pool2**，新增 hello 後端伺服器 hello ip 位址或 FQDN，然後按一下**[確定]**</span><span class="sxs-lookup"><span data-stu-id="edf68-149">On hello backend-pools blade click **Add** tooadd an additional back-end pool **pool2**, adding hello ip addresses or FQDNS for hello back-end servers and click **OK**</span></span>

![後端集區 pool2 設定][9]

## <a name="create-listeners-for-each-back-end"></a><span data-ttu-id="edf68-151">建立每個後端的接聽程式</span><span class="sxs-lookup"><span data-stu-id="edf68-151">Create listeners for each back-end</span></span>

<span data-ttu-id="edf68-152">應用程式閘道依賴 HTTP 1.1 以上某個網站上的主機標頭 toohost hello 相同的公開 IP 位址和連接埠。</span><span class="sxs-lookup"><span data-stu-id="edf68-152">Application Gateway relies on HTTP 1.1 host headers toohost more than one website on hello same public IP address and port.</span></span> <span data-ttu-id="edf68-153">hello 基本接聽程式 hello 入口網站中建立不包含這個屬性。</span><span class="sxs-lookup"><span data-stu-id="edf68-153">hello basic listener created in hello portal does not contain this property.</span></span>

### <a name="step-1"></a><span data-ttu-id="edf68-154">步驟 1</span><span class="sxs-lookup"><span data-stu-id="edf68-154">Step 1</span></span>

<span data-ttu-id="edf68-155">按一下**接聽程式**hello 現有應用程式閘道且按一下**多站台**tooadd hello 第一個接聽程式。</span><span class="sxs-lookup"><span data-stu-id="edf68-155">Click **Listeners** on hello existing application gateway and click **Multi-site** tooadd hello first listener.</span></span>

![接聽程式概觀刀鋒視窗][1]

### <a name="step-2"></a><span data-ttu-id="edf68-157">步驟 2</span><span class="sxs-lookup"><span data-stu-id="edf68-157">Step 2</span></span>

<span data-ttu-id="edf68-158">填寫 hello hello 接聽程式的資訊。</span><span class="sxs-lookup"><span data-stu-id="edf68-158">Fill out hello information for hello listener.</span></span> <span data-ttu-id="edf68-159">在此範例中，會設定 SSL 終止，建立新的前端連接埠。</span><span class="sxs-lookup"><span data-stu-id="edf68-159">In this example SSL termination is configured, create a new frontend port.</span></span> <span data-ttu-id="edf68-160">上傳 hello.pfx 憑證 toobe 用於 SSL 終止。</span><span class="sxs-lookup"><span data-stu-id="edf68-160">Upload hello .pfx certificate toobe used for SSL termination.</span></span> <span data-ttu-id="edf68-161">hello 這個刀鋒視窗中比較 toohello 標準基本的接聽程式 刀鋒視窗的唯一差異是 hello 主機名稱。</span><span class="sxs-lookup"><span data-stu-id="edf68-161">hello only difference on this blade compared toohello standard basic listener blade is hello hostname.</span></span>

![接聽程式屬性刀鋒視窗][2]

### <a name="step-3"></a><span data-ttu-id="edf68-163">步驟 3</span><span class="sxs-lookup"><span data-stu-id="edf68-163">Step 3</span></span>

<span data-ttu-id="edf68-164">按一下**多站台**和 hello hello 第二個網站的上一個步驟中所述，建立其他接聽程式。</span><span class="sxs-lookup"><span data-stu-id="edf68-164">Click **Multi-site** and create another listener as described in hello previous step for hello second site.</span></span> <span data-ttu-id="edf68-165">請確定 toouse hello 第二個接聽程式的不同憑證。</span><span class="sxs-lookup"><span data-stu-id="edf68-165">Make sure toouse a different certificate for hello second listener.</span></span> <span data-ttu-id="edf68-166">hello 這個刀鋒視窗中比較 toohello 標準基本的接聽程式 刀鋒視窗的唯一差異是 hello 主機名稱。</span><span class="sxs-lookup"><span data-stu-id="edf68-166">hello only difference on this blade compared toohello standard basic listener blade is hello hostname.</span></span> <span data-ttu-id="edf68-167">填寫 hello hello 接聽程式的資訊，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="edf68-167">Fill out hello information for hello listener and click **OK**.</span></span>

![接聽程式屬性刀鋒視窗][3]

> [!NOTE]
> <span data-ttu-id="edf68-169">建立 hello 應用程式閘道的 Azure 入口網站中的接聽程式已長時間執行的工作，它可能需要一些時間 toocreate hello 兩個接聽程式在此案例中。</span><span class="sxs-lookup"><span data-stu-id="edf68-169">Creation of listeners in hello Azure portal for application gateway is a long running task, it may take some time toocreate hello two listeners in this scenario.</span></span> <span data-ttu-id="edf68-170">當完成 hello 接聽程式中顯示 hello 入口網站 hello 下列影像所示：</span><span class="sxs-lookup"><span data-stu-id="edf68-170">When complete hello listeners show in hello portal as seen in hello following image:</span></span>

![接聽程式概觀][4]

## <a name="create-rules-toomap-listeners-toobackend-pools"></a><span data-ttu-id="edf68-172">建立規則 toomap 接聽程式 toobackend 集區</span><span class="sxs-lookup"><span data-stu-id="edf68-172">Create rules toomap listeners toobackend pools</span></span>

### <a name="step-1"></a><span data-ttu-id="edf68-173">步驟 1</span><span class="sxs-lookup"><span data-stu-id="edf68-173">Step 1</span></span>

<span data-ttu-id="edf68-174">瀏覽 tooan 現有應用程式閘道 hello Azure 入口網站 (https://portal.azure.com) 中。</span><span class="sxs-lookup"><span data-stu-id="edf68-174">Navigate tooan existing application gateway in hello Azure portal (https://portal.azure.com).</span></span> <span data-ttu-id="edf68-175">選取**規則**選擇現有預設規則 hello **rule1**按一下**編輯**。</span><span class="sxs-lookup"><span data-stu-id="edf68-175">Select **Rules** and choose hello existing default rule **rule1** and click **Edit**.</span></span>

### <a name="step-2"></a><span data-ttu-id="edf68-176">步驟 2</span><span class="sxs-lookup"><span data-stu-id="edf68-176">Step 2</span></span>

<span data-ttu-id="edf68-177">Hello 下列影像中所見，請填寫 hello 規則刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="edf68-177">Fill out hello rules blade as seen in hello following image.</span></span> <span data-ttu-id="edf68-178">選擇第一個接聽程式 hello 和第一個集區，然後按一下**儲存**時完成。</span><span class="sxs-lookup"><span data-stu-id="edf68-178">Choosing hello first listener and first pool and clicking **Save** when complete.</span></span>

![編輯現有的規則][6]

### <a name="step-3"></a><span data-ttu-id="edf68-180">步驟 3</span><span class="sxs-lookup"><span data-stu-id="edf68-180">Step 3</span></span>

<span data-ttu-id="edf68-181">按一下**基本規則**toocreate hello 第二個規則。</span><span class="sxs-lookup"><span data-stu-id="edf68-181">Click **Basic rule** toocreate hello second rule.</span></span> <span data-ttu-id="edf68-182">填寫 hello 表單與 hello 第二個接聽程式，第二個後端集區，然後按一下**確定**toosave。</span><span class="sxs-lookup"><span data-stu-id="edf68-182">Fill out hello form with hello second listener and second backend pool and click **OK** toosave.</span></span>

![新增基本規則刀鋒視窗][10]

<span data-ttu-id="edf68-184">這種情況下完成使用多站台支援透過 hello Azure 入口網站中設定現有的應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="edf68-184">This scenario completes configuring an existing application gateway with multi-site support through hello Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="edf68-185">後續步驟</span><span class="sxs-lookup"><span data-stu-id="edf68-185">Next steps</span></span>

<span data-ttu-id="edf68-186">深入了解如何 tooprotect 與網站[應用程式閘道的 Web 應用程式防火牆](application-gateway-webapplicationfirewall-overview.md)</span><span class="sxs-lookup"><span data-stu-id="edf68-186">Learn how tooprotect your websites with [Application Gateway - Web Application Firewall](application-gateway-webapplicationfirewall-overview.md)</span></span>

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
