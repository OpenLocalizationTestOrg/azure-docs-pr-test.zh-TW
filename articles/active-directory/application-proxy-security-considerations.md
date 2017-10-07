---
title: "Azure AD Application Proxy 的 aaaSecurity 考量 |Microsoft 文件"
description: "涵蓋使用 Azure AD 應用程式 Proxy 的安全性考量"
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: ebd14b9d1fc8f4629c5916e5a910595727d935d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="security-considerations-for-accessing-apps-remotely-with-azure-ad-application-proxy"></a><span data-ttu-id="475e4-103">使用 Azure AD 應用程式 Proxy 遠端存取應用程式的安全性考量</span><span class="sxs-lookup"><span data-stu-id="475e4-103">Security considerations for accessing apps remotely with Azure AD Application Proxy</span></span>

<span data-ttu-id="475e4-104">本文說明 Azure Active Directory 應用程式 Proxy 如何提供遠端發佈及存取應用程式的安全服務。</span><span class="sxs-lookup"><span data-stu-id="475e4-104">This article explains how Azure Active Directory Application Proxy provides a secure service for publishing and accessing your applications remotely.</span></span>

<span data-ttu-id="475e4-105">下列圖表顯示 Azure AD 的 hello 可讓安全遠端存取 tooyour 在內部部署應用程式。</span><span class="sxs-lookup"><span data-stu-id="475e4-105">hello following diagram shows how Azure AD enables secure remote access tooyour on-premises applications.</span></span>

 ![透過 Azure AD 應用程式 Proxy 進行安全遠端存取的示意圖](./media/application-proxy-security-considerations/secure-remote-access.png)

## <a name="security-benefits"></a><span data-ttu-id="475e4-107">安全性優點</span><span class="sxs-lookup"><span data-stu-id="475e4-107">Security benefits</span></span>

<span data-ttu-id="475e4-108">Azure AD 應用程式 Proxy 提供下列安全性優點的 hello:</span><span class="sxs-lookup"><span data-stu-id="475e4-108">Azure AD Application Proxy offers hello following security benefits:</span></span>

### <a name="authenticated-access"></a><span data-ttu-id="475e4-109">已驗證的存取</span><span class="sxs-lookup"><span data-stu-id="475e4-109">Authenticated access</span></span> 

<span data-ttu-id="475e4-110">如果您選擇 toouse Azure Active Directory 預先驗證時，已驗證的連線可以存取您的網路。</span><span class="sxs-lookup"><span data-stu-id="475e4-110">If you choose toouse Azure Active Directory preauthentication, then only authenticated connections can access your network.</span></span>

<span data-ttu-id="475e4-111">Azure AD Application Proxy 依賴 hello 所有驗證的 Azure AD 安全性權杖服務 (STS)。</span><span class="sxs-lookup"><span data-stu-id="475e4-111">Azure AD Application Proxy relies on hello Azure AD security token service (STS) for all authentication.</span></span>  <span data-ttu-id="475e4-112">預先驗證，本質，區塊中，大量的匿名攻擊，因為只驗證之身分識別可以存取 hello 後端應用程式。</span><span class="sxs-lookup"><span data-stu-id="475e4-112">Preauthentication, by its very nature, blocks a significant number of anonymous attacks, because only authenticated identities can access hello back-end application.</span></span>

<span data-ttu-id="475e4-113">如果您選擇 Passthrough 作為預先驗證方法，就無法獲得這項優點。</span><span class="sxs-lookup"><span data-stu-id="475e4-113">If you choose Passthrough as your preauthentication method, you don't get this benefit.</span></span> 

### <a name="conditional-access"></a><span data-ttu-id="475e4-114">條件式存取</span><span class="sxs-lookup"><span data-stu-id="475e4-114">Conditional access</span></span>

<span data-ttu-id="475e4-115">適用於更豐富的原則控制項之前 tooyour 網路建立的連接。</span><span class="sxs-lookup"><span data-stu-id="475e4-115">Apply richer policy controls before connections tooyour network are established.</span></span>

<span data-ttu-id="475e4-116">與[條件式存取](active-directory-conditional-access-azuread-connected-apps.md)，您可以定義哪些流量的限制允許 tooaccess 後端應用程式。</span><span class="sxs-lookup"><span data-stu-id="475e4-116">With [conditional access](active-directory-conditional-access-azuread-connected-apps.md), you can define restrictions on what traffic is allowed tooaccess your back-end applications.</span></span> <span data-ttu-id="475e4-117">您可以位置、驗證強度和使用者風險狀況作為基礎，來建立限制登入的原則。</span><span class="sxs-lookup"><span data-stu-id="475e4-117">You can create policies that restrict sign-ins based on location, strength of authentication, and user risk profile.</span></span>

<span data-ttu-id="475e4-118">您也可以使用條件式存取 tooconfigure 多重要素驗證原則，新增另一層的安全性 tooyour 使用者驗證。</span><span class="sxs-lookup"><span data-stu-id="475e4-118">You can also use conditional access tooconfigure Multi-Factor Authentication policies, adding another layer of security tooyour user authentications.</span></span> 

### <a name="traffic-termination"></a><span data-ttu-id="475e4-119">流量終止</span><span class="sxs-lookup"><span data-stu-id="475e4-119">Traffic termination</span></span>

<span data-ttu-id="475e4-120">所有流量會都終止 hello 雲端中。</span><span class="sxs-lookup"><span data-stu-id="475e4-120">All traffic is terminated in hello cloud.</span></span>

<span data-ttu-id="475e4-121">因為 Azure AD Application Proxy 是反向 proxy，所有流量 tooback 端應用程式會都終止在 hello 服務。</span><span class="sxs-lookup"><span data-stu-id="475e4-121">Because Azure AD Application Proxy is a reverse-proxy, all traffic tooback-end applications is terminated at hello service.</span></span> <span data-ttu-id="475e4-122">hello 工作階段可以取得重新建立只能搭配 hello 後端伺服器，也就是說，您的後端伺服器在不公開 toodirect HTTP 流量。</span><span class="sxs-lookup"><span data-stu-id="475e4-122">hello session can get reestablished only with hello back-end server, which means that your back-end servers are not exposed toodirect HTTP traffic.</span></span> <span data-ttu-id="475e4-123">此設定表示，您會受到更妥善的保護，可免於目標型攻擊。</span><span class="sxs-lookup"><span data-stu-id="475e4-123">This configuration means that you are better protected from targeted attacks.</span></span>

### <a name="all-access-is-outbound"></a><span data-ttu-id="475e4-124">所有存取都是輸出</span><span class="sxs-lookup"><span data-stu-id="475e4-124">All access is outbound</span></span> 

<span data-ttu-id="475e4-125">您不需要 tooopen 傳入的連接 toohello 公司網路。</span><span class="sxs-lookup"><span data-stu-id="475e4-125">You don't need tooopen inbound connections toohello corporate network.</span></span>

<span data-ttu-id="475e4-126">應用程式 Proxy 連接器只使用輸出連線 toohello Azure AD 應用程式 Proxy 服務，這表示沒有必要 tooopen 防火牆連接埠的連入連線。</span><span class="sxs-lookup"><span data-stu-id="475e4-126">Application Proxy connectors only use outbound connections toohello Azure AD Application Proxy service, which means that there is no need tooopen firewall ports for incoming connections.</span></span> <span data-ttu-id="475e4-127">傳統的 proxy 所需的周邊網路 (也稱為*DMZ*，*非軍事區域*，或*過濾的子網路*)，允許存取 toounauthenticated在 hello 網路邊緣的連接。</span><span class="sxs-lookup"><span data-stu-id="475e4-127">Traditional proxies required a perimeter network (also known as *DMZ*, *demilitarized zone*, or *screened subnet*) and allowed access toounauthenticated connections at hello network edge.</span></span> <span data-ttu-id="475e4-128">此案例需要許多額外的投資在 web 應用程式的防火牆產品 tooanalyze 流量，並提供加法保護 toohello 環境。</span><span class="sxs-lookup"><span data-stu-id="475e4-128">This scenario required many additional investments in web application firewall products tooanalyze traffic and offer addition protections toohello environment.</span></span> <span data-ttu-id="475e4-129">使用應用程式 Proxy，您就不需要周邊網路，因為所有連線皆為輸出方向，並且是透過安全通道來傳輸。</span><span class="sxs-lookup"><span data-stu-id="475e4-129">With Application Proxy, you don't need a perimeter network because all connections are outbound and take place over a secure channel.</span></span>

<span data-ttu-id="475e4-130">如需連接器的詳細資訊，請參閱[了解 Azure AD 應用程式 Proxy 連接器](application-proxy-understand-connectors.md)。</span><span class="sxs-lookup"><span data-stu-id="475e4-130">For more information about connectors, see [Understand Azure AD Application Proxy connectors](application-proxy-understand-connectors.md).</span></span>

### <a name="cloud-scale-analytics-and-machine-learning"></a><span data-ttu-id="475e4-131">雲端級別分析與機器學習</span><span class="sxs-lookup"><span data-stu-id="475e4-131">Cloud-scale analytics and machine learning</span></span> 

<span data-ttu-id="475e4-132">取得最新的安全性保護。</span><span class="sxs-lookup"><span data-stu-id="475e4-132">Get cutting-edge security protection.</span></span>

<span data-ttu-id="475e4-133">因為它是 Azure Active Directory 的一部分，可以利用應用程式 Proxy [Azure AD Identity Protection](active-directory-identityprotection.md)、 機器學習驅動智慧與 hello Microsoft Security Response Center 和數位犯罪單位的資料。</span><span class="sxs-lookup"><span data-stu-id="475e4-133">Because it's part of Azure Active Directory, Application Proxy can leverage [Azure AD Identity Protection](active-directory-identityprotection.md), with machine learning-driven intelligence and data from hello Microsoft Security Response Center and Digital Crimes Unit.</span></span> <span data-ttu-id="475e4-134">我們共同主動識別遭入侵的帳戶，並提供來自高風險登入的即時防護。我們考慮許多因素，例如來自受感染裝置、透過匿名網路以及來自非典型與假位置的存取。</span><span class="sxs-lookup"><span data-stu-id="475e4-134">Together we proactively identify compromised accounts and offer real-time protection from high-risk sign-ins. We take into account numerous factors, such as access from infected devices, through anonymizing networks, and from atypical and unlikely locations.</span></span>

<span data-ttu-id="475e4-135">這些報告和事件中有許多已可透過 API 與安全性資訊和事件管理 (SIEM) 系統整合。</span><span class="sxs-lookup"><span data-stu-id="475e4-135">Many of these reports and events are already available through an API for integration with your security information and event management (SIEM) systems.</span></span>

### <a name="remote-access-as-a-service"></a><span data-ttu-id="475e4-136">遠端存取即服務</span><span class="sxs-lookup"><span data-stu-id="475e4-136">Remote access as a service</span></span>

<span data-ttu-id="475e4-137">您不需要 tooworry 關於維護及修補內部部署伺服器。</span><span class="sxs-lookup"><span data-stu-id="475e4-137">You don’t have tooworry about maintaining and patching on-premises servers.</span></span>

<span data-ttu-id="475e4-138">未更新的軟體仍需負責處理大量攻擊。</span><span class="sxs-lookup"><span data-stu-id="475e4-138">Unpatched software still accounts for a large number of attacks.</span></span> <span data-ttu-id="475e4-139">Azure AD Application Proxy 是 Microsoft 所擁有，網際網路規模服務，因此您一定要取得最新安全性修補程式 hello 與升級。</span><span class="sxs-lookup"><span data-stu-id="475e4-139">Azure AD Application Proxy is an Internet-scale service that Microsoft owns, so you always get hello latest security patches and upgrades.</span></span>

<span data-ttu-id="475e4-140">tooimprove hello 由 Azure AD Application Proxy 發行應用程式的安全性，我們會封鎖從編製索引和封存您的應用程式的 web crawler 機器人。</span><span class="sxs-lookup"><span data-stu-id="475e4-140">tooimprove hello security of applications published by Azure AD Application Proxy, we block web crawler robots from indexing and archiving your applications.</span></span> <span data-ttu-id="475e4-141">每次 Web 編目程式傀儡程式嘗試擷取已發佈應用程式的傀儡程式設定時，應用程式 Proxy 會以含有 `User-agent: * Disallow: /` 的 robots.txt 檔案回覆。</span><span class="sxs-lookup"><span data-stu-id="475e4-141">Each time a web crawler robot tries to retrieve the robot's settings for a published app, Application Proxy replies with a robots.txt file that includes `User-agent: * Disallow: /`.</span></span>

## <a name="under-hello-hood"></a><span data-ttu-id="475e4-142">Hello 幕後</span><span class="sxs-lookup"><span data-stu-id="475e4-142">Under hello hood</span></span>

<span data-ttu-id="475e4-143">Azure AD 應用程式 Proxy 是由兩個部分組成︰</span><span class="sxs-lookup"><span data-stu-id="475e4-143">Azure AD Application Proxy consists of two parts:</span></span>

* <span data-ttu-id="475e4-144">hello 雲端式服務： 此服務執行於 Azure，且其中 hello 外部的用戶端/使用者連線。</span><span class="sxs-lookup"><span data-stu-id="475e4-144">hello cloud-based service: This service runs in Azure, and is where hello external client/user connections are made.</span></span>
* <span data-ttu-id="475e4-145">[hello 內部部署連接器](application-proxy-understand-connectors.md): hello 連接器在內部部署元件會接聽來自 hello Azure AD 應用程式 Proxy 服務的要求和處理連線 toohello 內部應用程式。</span><span class="sxs-lookup"><span data-stu-id="475e4-145">[hello on-premises connector](application-proxy-understand-connectors.md): An on-premises component, hello connector listens for requests from hello Azure AD Application Proxy service and handles connections toohello internal applications.</span></span> 

<span data-ttu-id="475e4-146">建立 hello 連接器與 hello 應用程式 Proxy 服務之間的資料流程時：</span><span class="sxs-lookup"><span data-stu-id="475e4-146">A flow between hello connector and hello Application Proxy service is established when:</span></span>

* <span data-ttu-id="475e4-147">先設定 hello 連接器。</span><span class="sxs-lookup"><span data-stu-id="475e4-147">hello connector is first set up.</span></span>
* <span data-ttu-id="475e4-148">hello 連接器會提取從 hello 應用程式 Proxy 服務的組態資訊。</span><span class="sxs-lookup"><span data-stu-id="475e4-148">hello connector pulls configuration information from hello Application Proxy service.</span></span>
* <span data-ttu-id="475e4-149">使用者會存取發佈的應用程式。</span><span class="sxs-lookup"><span data-stu-id="475e4-149">A user accesses a published application.</span></span>

>[!NOTE]
><span data-ttu-id="475e4-150">所有的通訊會透過 SSL，而且它們永遠都是源自於 hello 連接器 toohello 應用程式 Proxy 服務。</span><span class="sxs-lookup"><span data-stu-id="475e4-150">All communications occur over SSL, and they always originate at hello connector toohello Application Proxy service.</span></span> <span data-ttu-id="475e4-151">hello 服務僅輸出。</span><span class="sxs-lookup"><span data-stu-id="475e4-151">hello service is outbound only.</span></span>

<span data-ttu-id="475e4-152">hello 連接器會使用用戶端憑證 tooauthenticate toohello 幾乎所有呼叫的應用程式 Proxy 服務。</span><span class="sxs-lookup"><span data-stu-id="475e4-152">hello connector uses a client certificate tooauthenticate toohello Application Proxy service for nearly all calls.</span></span> <span data-ttu-id="475e4-153">hello 只例外狀況 toothis 程序是 hello 初始設定步驟中，建立 hello 用戶端憑證的位置。</span><span class="sxs-lookup"><span data-stu-id="475e4-153">hello only exception toothis process is hello initial setup step, where hello client certificate is established.</span></span>

### <a name="installing-hello-connector"></a><span data-ttu-id="475e4-154">安裝 hello connector</span><span class="sxs-lookup"><span data-stu-id="475e4-154">Installing hello connector</span></span>

<span data-ttu-id="475e4-155">當第一次設定 hello 連接器時，hello 遵循的流程事件會發生：</span><span class="sxs-lookup"><span data-stu-id="475e4-155">When hello connector is first set up, hello following flow events take place:</span></span>

1. <span data-ttu-id="475e4-156">hello 連接器註冊 toohello 服務就會發生 hello hello 連接器安裝的一部分。</span><span class="sxs-lookup"><span data-stu-id="475e4-156">hello connector registration toohello service happens as part of hello installation of hello connector.</span></span> <span data-ttu-id="475e4-157">使用者會提示的 tooenter 其 Azure AD 系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="475e4-157">Users are prompted tooenter their Azure AD admin credentials.</span></span> <span data-ttu-id="475e4-158">從這項驗證權杖會接著呈現 toohello Azure AD 應用程式 Proxy 服務。</span><span class="sxs-lookup"><span data-stu-id="475e4-158">The token acquired from this authentication is then presented toohello Azure AD Application Proxy service.</span></span>
2. <span data-ttu-id="475e4-159">hello 應用程式 Proxy 服務會評估 hello 語彙基元。</span><span class="sxs-lookup"><span data-stu-id="475e4-159">hello Application Proxy service evaluates hello token.</span></span> <span data-ttu-id="475e4-160">它會確保該 hello 使用者即 hello 語彙基元的 hello 租用戶內的公司系統管理員已發出。</span><span class="sxs-lookup"><span data-stu-id="475e4-160">It ensures that hello user is a company administrator within hello tenant that hello token was issued for.</span></span> <span data-ttu-id="475e4-161">如果 hello 使用者不是系統管理員，則會終止 hello 程序。</span><span class="sxs-lookup"><span data-stu-id="475e4-161">If hello user is not an administrator, hello process is terminated.</span></span>
3. <span data-ttu-id="475e4-162">hello 連接器產生的用戶端憑證要求，並傳遞，連同 hello 語彙基元，toohello 應用程式 Proxy 服務。</span><span class="sxs-lookup"><span data-stu-id="475e4-162">hello connector generates a client certificate request and passes it, along with hello token, toohello Application Proxy service.</span></span> <span data-ttu-id="475e4-163">hello 服務接著會驗證 hello 語彙基元，並簽署 hello 用戶端憑證要求。</span><span class="sxs-lookup"><span data-stu-id="475e4-163">hello service in turn verifies hello token and signs hello client certificate request.</span></span>
4. <span data-ttu-id="475e4-164">hello 連接器會使用與 hello 應用程式 Proxy 服務的未來通訊 hello 用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="475e4-164">hello connector uses hello client certificate for future communication with hello Application Proxy service.</span></span>
5. <span data-ttu-id="475e4-165">hello 連接器 hello 系統組態資料的初始提取從 hello 服務使用用戶端憑證，並已準備好 tootake 要求。</span><span class="sxs-lookup"><span data-stu-id="475e4-165">hello connector performs an initial pull of hello system configuration data from hello service using its client certificate, and it is now ready tootake requests.</span></span>

### <a name="updating-hello-configuration-settings"></a><span data-ttu-id="475e4-166">更新 hello 組態設定</span><span class="sxs-lookup"><span data-stu-id="475e4-166">Updating hello configuration settings</span></span>

<span data-ttu-id="475e4-167">每當應用程式 Proxy 服務的 hello 更新 hello 組態設定，hello 遵循的流程事件會發生：</span><span class="sxs-lookup"><span data-stu-id="475e4-167">Whenever hello Application Proxy service updates hello configuration settings, hello following flow events take place:</span></span>

1. <span data-ttu-id="475e4-168">hello 連接器會使用其用戶端憑證，以連接 toohello hello 應用程式 Proxy 服務設定端點。</span><span class="sxs-lookup"><span data-stu-id="475e4-168">hello connector connects toohello configuration endpoint within hello Application Proxy service by using its client certificate.</span></span>
2. <span data-ttu-id="475e4-169">Hello 應用程式 Proxy 服務已驗證 hello 用戶端憑證之後，傳回組態資料 toohello 連接器 （例如，hello 連接器的 hello 連接器群組應該是的一部分）。</span><span class="sxs-lookup"><span data-stu-id="475e4-169">After hello client certificate has been validated, hello Application Proxy service returns configuration data toohello connector (for example, hello connector group that hello connector should be part of).</span></span>
3. <span data-ttu-id="475e4-170">如果 180 天以前 hello 目前的憑證，hello 連接器會產生新的憑證要求，並有效地更新每 180 天 hello 用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="475e4-170">If hello current certificate is more than 180 days old, hello connector generates a new certificate request, which effectively updates hello client certificate every 180 days.</span></span>

### <a name="accessing-published-applications"></a><span data-ttu-id="475e4-171">存取已發佈的應用程式</span><span class="sxs-lookup"><span data-stu-id="475e4-171">Accessing published applications</span></span>

<span data-ttu-id="475e4-172">當使用者存取已發行的應用程式時，hello 下列事件會發生 hello 應用程式 Proxy 服務之間 hello 應用程式 Proxy 連接器：</span><span class="sxs-lookup"><span data-stu-id="475e4-172">When users access a published application, hello following events take place between hello Application Proxy service and hello Application Proxy connector:</span></span>

1. [<span data-ttu-id="475e4-173">hello 服務會驗證 hello hello 應用程式的使用者</span><span class="sxs-lookup"><span data-stu-id="475e4-173">hello service authenticates hello user for hello app</span></span>](#the-service-checks-the-configuration-settings-for-the-app)
2. [<span data-ttu-id="475e4-174">hello 服務會將要求放在 hello 連接器佇列</span><span class="sxs-lookup"><span data-stu-id="475e4-174">hello service places a request in hello connector queue</span></span>](#The-service-places-a-request-in-the-connector-queue)
3. [<span data-ttu-id="475e4-175">連接器處理 hello hello 佇列要求</span><span class="sxs-lookup"><span data-stu-id="475e4-175">A connector processes hello request from hello queue</span></span>](#the-connector-receives-the-request-from-the-queue)
4. [<span data-ttu-id="475e4-176">hello 連接器等候回應</span><span class="sxs-lookup"><span data-stu-id="475e4-176">hello connector waits for a response</span></span>](#the-connector-waits-for-a-response)
5. [<span data-ttu-id="475e4-177">hello 服務資料流資料 toohello 使用者</span><span class="sxs-lookup"><span data-stu-id="475e4-177">hello service streams data toohello user</span></span>](#the-service-streams-data-to-the-user)

<span data-ttu-id="475e4-178">深入了解什麼發生在每個步驟，toolearn 保留讀取。</span><span class="sxs-lookup"><span data-stu-id="475e4-178">toolearn more about what takes place in each of these steps, keep reading.</span></span>


#### <a name="1-hello-service-authenticates-hello-user-for-hello-app"></a><span data-ttu-id="475e4-179">1.hello 服務會驗證 hello hello 應用程式的使用者</span><span class="sxs-lookup"><span data-stu-id="475e4-179">1. hello service authenticates hello user for hello app</span></span>

<span data-ttu-id="475e4-180">如果您設定 hello 應用程式 toouse 傳遞做為其預先驗證方法時，會略過本節中的 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="475e4-180">If you configured hello app toouse Passthrough as its preauthentication method, hello steps in this section are skipped.</span></span>

<span data-ttu-id="475e4-181">如果您使用 Azure AD 設定 hello 應用程式 toopreauthenticate，使用者會重新導向的 toohello Azure AD STS tooauthenticate，而且 hello 下列步驟進行：</span><span class="sxs-lookup"><span data-stu-id="475e4-181">If you configured hello app toopreauthenticate with Azure AD, users are redirected toohello Azure AD STS tooauthenticate, and hello following steps take place:</span></span>

1. <span data-ttu-id="475e4-182">應用程式 Proxy 會檢查任何 hello 特定應用程式的條件式存取原則需求。</span><span class="sxs-lookup"><span data-stu-id="475e4-182">Application Proxy checks for any conditional access policy requirements for hello specific application.</span></span> <span data-ttu-id="475e4-183">這個步驟可確保該 hello 使用者已獲指派 toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="475e4-183">This step ensures that hello user has been assigned toohello application.</span></span> <span data-ttu-id="475e4-184">如果需要雙步驟驗證，hello 驗證順序就會提示 hello 使用者在第二個驗證方法。</span><span class="sxs-lookup"><span data-stu-id="475e4-184">If two-step verification is required, hello authentication sequence prompts hello user for a second authentication method.</span></span>

2. <span data-ttu-id="475e4-185">已通過所有檢查之後，hello Azure AD STS 發出 hello 應用程式的簽署語彙基元，並重新導向 hello 使用者回復 toohello 應用程式 Proxy 服務。</span><span class="sxs-lookup"><span data-stu-id="475e4-185">After all checks have passed, hello Azure AD STS issues a signed token for hello application and redirects hello user back toohello Application Proxy service.</span></span>

3. <span data-ttu-id="475e4-186">應用程式 Proxy 會確認該 hello 語彙基元發出 toocorrect hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="475e4-186">Application Proxy verifies that hello token was issued toocorrect hello application.</span></span> <span data-ttu-id="475e4-187">它也會執行其他檢查權杖簽署由 Azure AD，例如確保該 hello，它仍在 hello 有效的視窗。</span><span class="sxs-lookup"><span data-stu-id="475e4-187">It performs other checks also, such as ensuring that hello token was signed by Azure AD, and that it is still within hello valid window.</span></span>

4. <span data-ttu-id="475e4-188">應用程式 Proxy 設定發生驗證 toohello 應用程式加密的驗證 cookie tooindicate。</span><span class="sxs-lookup"><span data-stu-id="475e4-188">Application Proxy sets an encrypted authentication cookie tooindicate that authentication toohello application has occurred.</span></span> <span data-ttu-id="475e4-189">hello cookie 包含根據 hello 來自 Azure AD 的權杖及其他資料的到期時間戳記，例如 hello hello 驗證的使用者名稱為基礎。</span><span class="sxs-lookup"><span data-stu-id="475e4-189">hello cookie includes an expiration timestamp that's based on hello token from Azure AD and other data, such as hello user name that hello authentication is based on.</span></span> <span data-ttu-id="475e4-190">使用已知 toohello 應用程式 Proxy 服務的私密金鑰來加密 hello cookie。</span><span class="sxs-lookup"><span data-stu-id="475e4-190">hello cookie is encrypted with a private key known only toohello Application Proxy service.</span></span>

5. <span data-ttu-id="475e4-191">應用程式 Proxy 重新導向 hello 使用者回復 toohello 原始要求的 URL。</span><span class="sxs-lookup"><span data-stu-id="475e4-191">Application Proxy redirects hello user back toohello originally requested URL.</span></span>

<span data-ttu-id="475e4-192">如果 hello 預先驗證步驟的任何部分失敗，hello 使用者的要求遭到拒絕，並 hello 使用者顯示訊息，指出 hello hello 問題來源。</span><span class="sxs-lookup"><span data-stu-id="475e4-192">If any part of hello preauthentication steps fails, hello user’s request is denied, and hello user is shown a message indicating hello source of hello problem.</span></span>


#### <a name="2-hello-service-places-a-request-in-hello-connector-queue"></a><span data-ttu-id="475e4-193">2.hello 服務會將要求放在 hello 連接器佇列</span><span class="sxs-lookup"><span data-stu-id="475e4-193">2. hello service places a request in hello connector queue</span></span>

<span data-ttu-id="475e4-194">連接器會將輸出連線開啟 toohello 應用程式 Proxy 服務。</span><span class="sxs-lookup"><span data-stu-id="475e4-194">Connectors keep an outbound connection open toohello Application Proxy service.</span></span> <span data-ttu-id="475e4-195">當要求進入時，則會將 hello 服務上的向上 hello 連接器 toopick hello 開啟連接的其中一個 hello 要求排入佇列。</span><span class="sxs-lookup"><span data-stu-id="475e4-195">When a request comes in, hello service queues up hello request on one of hello open connections for hello connector toopick up.</span></span>

<span data-ttu-id="475e4-196">hello 要求包含項目從 hello 應用程式，例如 hello 要求標頭，從 hello 加密 cookie 資料、 hello 使用者進行 hello 要求，並 hello 要求識別碼。</span><span class="sxs-lookup"><span data-stu-id="475e4-196">hello request includes items from hello application, such as hello request headers, data from hello encrypted cookie, hello user making hello request, and hello request ID.</span></span> <span data-ttu-id="475e4-197">雖然資料從 hello 加密 cookie 傳送 hello 要求，但不是本身 hello 驗證 cookie。</span><span class="sxs-lookup"><span data-stu-id="475e4-197">Although data from hello encrypted cookie is sent with hello request, hello authentication cookie itself is not.</span></span>

#### <a name="3-hello-connector-processes-hello-request-from-hello-queue"></a><span data-ttu-id="475e4-198">3.hello 連接器處理 hello 從 hello 佇列的要求。</span><span class="sxs-lookup"><span data-stu-id="475e4-198">3. hello connector processes hello request from hello queue.</span></span> 

<span data-ttu-id="475e4-199">根據 hello 要求，應用程式 Proxy 會執行下列動作的 hello 的其中一個：</span><span class="sxs-lookup"><span data-stu-id="475e4-199">Based on hello request, Application Proxy performs one of hello following actions:</span></span>

* <span data-ttu-id="475e4-200">如果 hello 要求是簡單的作業 (例如，沒有資料現況 RESTful hello 主體內*取得*要求)，hello 連接器可讓連接 toohello 目標內部資源，然後等候回應。</span><span class="sxs-lookup"><span data-stu-id="475e4-200">If hello request is a simple operation (for example, there is no data within hello body as is with a RESTful *GET* request), hello connector makes a connection toohello target internal resource and then waits for a response.</span></span>

* <span data-ttu-id="475e4-201">如果 hello 要求有與其相關聯 hello 主體中的資料 (例如，RESTful *POST*作業)，hello 連接器可藉由使用 hello 用戶端憑證 toohello 應用程式 Proxy 執行個體的輸出連線。</span><span class="sxs-lookup"><span data-stu-id="475e4-201">If hello request has data associated with it in hello body (for example, a RESTful *POST* operation), hello connector makes an outbound connection by using hello client certificate toohello Application Proxy instance.</span></span> <span data-ttu-id="475e4-202">它會建立此連線 toorequest hello 資料，並開啟連接 toohello 內部資源。</span><span class="sxs-lookup"><span data-stu-id="475e4-202">It makes this connection toorequest hello data and open a connection toohello internal resource.</span></span> <span data-ttu-id="475e4-203">在收到 hello 連接器 hello 要求之後，hello 應用程式 Proxy 服務開始接受來自 hello 使用者內容，並將轉寄資料 toohello 連接器。</span><span class="sxs-lookup"><span data-stu-id="475e4-203">After it receives hello request from hello connector, hello Application Proxy service begins accepting content from hello user and forwards data toohello connector.</span></span> <span data-ttu-id="475e4-204">hello 連接器，亦會將轉送 hello 資料 toohello 內部資源。</span><span class="sxs-lookup"><span data-stu-id="475e4-204">hello connector, in turn, forwards hello data toohello internal resource.</span></span>

#### <a name="4-hello-connector-waits-for-a-response"></a><span data-ttu-id="475e4-205">4.hello 連接器等候回應。</span><span class="sxs-lookup"><span data-stu-id="475e4-205">4. hello connector waits for a response.</span></span>

<span data-ttu-id="475e4-206">Hello 要求及所有內容 toohello 傳輸回後端完成，hello 連接器等候回應。</span><span class="sxs-lookup"><span data-stu-id="475e4-206">After hello request and transmission of all content toohello back end is complete, hello connector waits for a response.</span></span>

<span data-ttu-id="475e4-207">收到回應後，hello 連接器可讓輸出連線 toohello 應用程式 Proxy 服務，tooreturn hello 標頭的詳細資料，並開始串流處理 hello 傳回資料。</span><span class="sxs-lookup"><span data-stu-id="475e4-207">After it receives a response, hello connector makes an outbound connection toohello Application Proxy service, tooreturn hello header details and begin streaming hello return data.</span></span>

#### <a name="5-hello-service-streams-data-toohello-user"></a><span data-ttu-id="475e4-208">5.hello 服務資料流資料 toohello 使用者。</span><span class="sxs-lookup"><span data-stu-id="475e4-208">5. hello service streams data toohello user.</span></span> 

<span data-ttu-id="475e4-209">一些處理 hello 應用程式可能會發生以下。</span><span class="sxs-lookup"><span data-stu-id="475e4-209">Some processing of hello application may occur here.</span></span> <span data-ttu-id="475e4-210">如果您在應用程式中設定應用程式 Proxy tootranslate 標頭或 Url，該處理會視需要在此步驟進行。</span><span class="sxs-lookup"><span data-stu-id="475e4-210">If you configured Application Proxy tootranslate headers or URLs in your application, that processing happens as needed during this step.</span></span>


## <a name="next-steps"></a><span data-ttu-id="475e4-211">後續步驟</span><span class="sxs-lookup"><span data-stu-id="475e4-211">Next steps</span></span>

[<span data-ttu-id="475e4-212">使用 Azure AD 應用程式 Proxy 時的網路拓撲考量</span><span class="sxs-lookup"><span data-stu-id="475e4-212">Network topology considerations when using Azure AD Application Proxy</span></span>](application-proxy-network-topology-considerations.md)

[<span data-ttu-id="475e4-213">了解 Azure AD 應用程式 Proxy 連接器</span><span class="sxs-lookup"><span data-stu-id="475e4-213">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)
