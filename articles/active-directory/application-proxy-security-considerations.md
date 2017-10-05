---
title: "Azure AD 應用程式 Proxy 的安全性考量 | Microsoft Docs"
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
ms.openlocfilehash: c6ead651133eb17fd55f7567cdb14dc3bcd64245
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="security-considerations-for-accessing-apps-remotely-with-azure-ad-application-proxy"></a><span data-ttu-id="32030-103">使用 Azure AD 應用程式 Proxy 遠端存取應用程式的安全性考量</span><span class="sxs-lookup"><span data-stu-id="32030-103">Security considerations for accessing apps remotely with Azure AD Application Proxy</span></span>

<span data-ttu-id="32030-104">本文說明 Azure Active Directory 應用程式 Proxy 如何提供遠端發佈及存取應用程式的安全服務。</span><span class="sxs-lookup"><span data-stu-id="32030-104">This article explains how Azure Active Directory Application Proxy provides a secure service for publishing and accessing your applications remotely.</span></span>

<span data-ttu-id="32030-105">下圖顯示 Azure AD 如何讓您在內部部署應用程式實現安全的遠端存取。</span><span class="sxs-lookup"><span data-stu-id="32030-105">The following diagram shows how Azure AD enables secure remote access to your on-premises applications.</span></span>

 ![透過 Azure AD 應用程式 Proxy 進行安全遠端存取的示意圖](./media/application-proxy-security-considerations/secure-remote-access.png)

## <a name="security-benefits"></a><span data-ttu-id="32030-107">安全性優點</span><span class="sxs-lookup"><span data-stu-id="32030-107">Security benefits</span></span>

<span data-ttu-id="32030-108">Azure AD 應用程式 Proxy 提供下列安全性優點︰</span><span class="sxs-lookup"><span data-stu-id="32030-108">Azure AD Application Proxy offers the following security benefits:</span></span>

### <a name="authenticated-access"></a><span data-ttu-id="32030-109">已驗證的存取</span><span class="sxs-lookup"><span data-stu-id="32030-109">Authenticated access</span></span> 

<span data-ttu-id="32030-110">如果您選擇使用 Azure Active Directory 預先驗證，則只有已驗證的連線可以存取您的網路。</span><span class="sxs-lookup"><span data-stu-id="32030-110">If you choose to use Azure Active Directory preauthentication, then only authenticated connections can access your network.</span></span>

<span data-ttu-id="32030-111">Azure AD 應用程式 Proxy 依賴 Azure AD Security Token Service (STS) 來進行所有驗證。</span><span class="sxs-lookup"><span data-stu-id="32030-111">Azure AD Application Proxy relies on the Azure AD security token service (STS) for all authentication.</span></span>  <span data-ttu-id="32030-112">預先驗證 (就其本質) 會封鎖大量匿名攻擊，因為只有已驗證的身分識別可以存取後端應用程式。</span><span class="sxs-lookup"><span data-stu-id="32030-112">Preauthentication, by its very nature, blocks a significant number of anonymous attacks, because only authenticated identities can access the back-end application.</span></span>

<span data-ttu-id="32030-113">如果您選擇 Passthrough 作為預先驗證方法，就無法獲得這項優點。</span><span class="sxs-lookup"><span data-stu-id="32030-113">If you choose Passthrough as your preauthentication method, you don't get this benefit.</span></span> 

### <a name="conditional-access"></a><span data-ttu-id="32030-114">條件式存取</span><span class="sxs-lookup"><span data-stu-id="32030-114">Conditional access</span></span>

<span data-ttu-id="32030-115">在建立您的網路連線之前，先套用更豐富的原則控制。</span><span class="sxs-lookup"><span data-stu-id="32030-115">Apply richer policy controls before connections to your network are established.</span></span>

<span data-ttu-id="32030-116">使用[條件式存取](active-directory-conditional-access-azuread-connected-apps.md)，就可以定義允許哪些流量存取後端應用程式上的限制。</span><span class="sxs-lookup"><span data-stu-id="32030-116">With [conditional access](active-directory-conditional-access-azuread-connected-apps.md), you can define restrictions on what traffic is allowed to access your back-end applications.</span></span> <span data-ttu-id="32030-117">您可以位置、驗證強度和使用者風險狀況作為基礎，來建立限制登入的原則。</span><span class="sxs-lookup"><span data-stu-id="32030-117">You can create policies that restrict sign-ins based on location, strength of authentication, and user risk profile.</span></span>

<span data-ttu-id="32030-118">您也可以使用條件式存取來設定 Multi-Factor Authentication 原則，為您的使用者驗證新增另一層的安全性。</span><span class="sxs-lookup"><span data-stu-id="32030-118">You can also use conditional access to configure Multi-Factor Authentication policies, adding another layer of security to your user authentications.</span></span> 

### <a name="traffic-termination"></a><span data-ttu-id="32030-119">流量終止</span><span class="sxs-lookup"><span data-stu-id="32030-119">Traffic termination</span></span>

<span data-ttu-id="32030-120">終止雲端中所有的流量。</span><span class="sxs-lookup"><span data-stu-id="32030-120">All traffic is terminated in the cloud.</span></span>

<span data-ttu-id="32030-121">Azure AD 應用程式 Proxy 是反向 Proxy，因此所有至後端應用程式的流量會在服務終止。</span><span class="sxs-lookup"><span data-stu-id="32030-121">Because Azure AD Application Proxy is a reverse-proxy, all traffic to back-end applications is terminated at the service.</span></span> <span data-ttu-id="32030-122">工作階段只能利用後端伺服器來重新建立，也就是說，後端伺服器不會對直接的 HTTP 流量公開。</span><span class="sxs-lookup"><span data-stu-id="32030-122">The session can get reestablished only with the back-end server, which means that your back-end servers are not exposed to direct HTTP traffic.</span></span> <span data-ttu-id="32030-123">此設定表示，您會受到更妥善的保護，可免於目標型攻擊。</span><span class="sxs-lookup"><span data-stu-id="32030-123">This configuration means that you are better protected from targeted attacks.</span></span>

### <a name="all-access-is-outbound"></a><span data-ttu-id="32030-124">所有存取都是輸出</span><span class="sxs-lookup"><span data-stu-id="32030-124">All access is outbound</span></span> 

<span data-ttu-id="32030-125">不需要開啟連往公司網路的輸入連線。</span><span class="sxs-lookup"><span data-stu-id="32030-125">You don't need to open inbound connections to the corporate network.</span></span>

<span data-ttu-id="32030-126">應用程式 Proxy 連接器只會使用連往 Azure AD 應用程式 Proxy 服務的輸出連線；亦即，您不需要開啟防火牆連接埠以供連入連線使用。</span><span class="sxs-lookup"><span data-stu-id="32030-126">Application Proxy connectors only use outbound connections to the Azure AD Application Proxy service, which means that there is no need to open firewall ports for incoming connections.</span></span> <span data-ttu-id="32030-127">傳統 Proxy 需要周邊網路 (也稱為「DMZ」、「非軍事區」或「遮蔽式子網路」) 並在網路邊緣允許未經授權連線的存取權。</span><span class="sxs-lookup"><span data-stu-id="32030-127">Traditional proxies required a perimeter network (also known as *DMZ*, *demilitarized zone*, or *screened subnet*) and allowed access to unauthenticated connections at the network edge.</span></span> <span data-ttu-id="32030-128">這種情節需要額外投資許多 Web 應用程式防火牆產品，以便分析流量並對環境提供額外的保護。</span><span class="sxs-lookup"><span data-stu-id="32030-128">This scenario required many additional investments in web application firewall products to analyze traffic and offer addition protections to the environment.</span></span> <span data-ttu-id="32030-129">使用應用程式 Proxy，您就不需要周邊網路，因為所有連線皆為輸出方向，並且是透過安全通道來傳輸。</span><span class="sxs-lookup"><span data-stu-id="32030-129">With Application Proxy, you don't need a perimeter network because all connections are outbound and take place over a secure channel.</span></span>

<span data-ttu-id="32030-130">如需連接器的詳細資訊，請參閱[了解 Azure AD 應用程式 Proxy 連接器](application-proxy-understand-connectors.md)。</span><span class="sxs-lookup"><span data-stu-id="32030-130">For more information about connectors, see [Understand Azure AD Application Proxy connectors](application-proxy-understand-connectors.md).</span></span>

### <a name="cloud-scale-analytics-and-machine-learning"></a><span data-ttu-id="32030-131">雲端級別分析與機器學習</span><span class="sxs-lookup"><span data-stu-id="32030-131">Cloud-scale analytics and machine learning</span></span> 

<span data-ttu-id="32030-132">取得最新的安全性保護。</span><span class="sxs-lookup"><span data-stu-id="32030-132">Get cutting-edge security protection.</span></span>

<span data-ttu-id="32030-133">因為應用程式 Proxy 是 Azure Active Directory 的一部分，所以可以利用 [Azure AD Identity Protection](active-directory-identityprotection.md)，其中包含來自 Microsoft Security Response Center 和 Digital Crimes Unit 的機器學習服務導向情報和資料。</span><span class="sxs-lookup"><span data-stu-id="32030-133">Because it's part of Azure Active Directory, Application Proxy can leverage [Azure AD Identity Protection](active-directory-identityprotection.md), with machine learning-driven intelligence and data from the Microsoft Security Response Center and Digital Crimes Unit.</span></span> <span data-ttu-id="32030-134">我們共同主動識別遭入侵的帳戶，並提供來自高風險登入的即時防護。我們考慮許多因素，例如來自受感染裝置、透過匿名網路以及來自非典型與假位置的存取。</span><span class="sxs-lookup"><span data-stu-id="32030-134">Together we proactively identify compromised accounts and offer real-time protection from high-risk sign-ins. We take into account numerous factors, such as access from infected devices, through anonymizing networks, and from atypical and unlikely locations.</span></span>

<span data-ttu-id="32030-135">這些報告和事件中有許多已可透過 API 與安全性資訊和事件管理 (SIEM) 系統整合。</span><span class="sxs-lookup"><span data-stu-id="32030-135">Many of these reports and events are already available through an API for integration with your security information and event management (SIEM) systems.</span></span>

### <a name="remote-access-as-a-service"></a><span data-ttu-id="32030-136">遠端存取即服務</span><span class="sxs-lookup"><span data-stu-id="32030-136">Remote access as a service</span></span>

<span data-ttu-id="32030-137">您不必擔心維護及修補內部部署伺服器的事宜。</span><span class="sxs-lookup"><span data-stu-id="32030-137">You don’t have to worry about maintaining and patching on-premises servers.</span></span>

<span data-ttu-id="32030-138">未更新的軟體仍需負責處理大量攻擊。</span><span class="sxs-lookup"><span data-stu-id="32030-138">Unpatched software still accounts for a large number of attacks.</span></span> <span data-ttu-id="32030-139">Azure AD 應用程式 Proxy 是 Microsoft 自有的網際網路級別服務，因此您永遠會獲得最新的安全性修補程式和升級。</span><span class="sxs-lookup"><span data-stu-id="32030-139">Azure AD Application Proxy is an Internet-scale service that Microsoft owns, so you always get the latest security patches and upgrades.</span></span>

<span data-ttu-id="32030-140">為了改善 Azure AD 應用程式 Proxy 所發佈應用程式的安全性，我們會封鎖 Web 編目程式傀儡程式，使其無法對您的應用程式編製索引和進行保存。</span><span class="sxs-lookup"><span data-stu-id="32030-140">To improve the security of applications published by Azure AD Application Proxy, we block web crawler robots from indexing and archiving your applications.</span></span> <span data-ttu-id="32030-141">每次 Web 編目程式傀儡程式嘗試擷取已發佈應用程式的傀儡程式設定時，應用程式 Proxy 會以含有 `User-agent: * Disallow: /` 的 robots.txt 檔案回覆。</span><span class="sxs-lookup"><span data-stu-id="32030-141">Each time a web crawler robot tries to retrieve the robot's settings for a published app, Application Proxy replies with a robots.txt file that includes `User-agent: * Disallow: /`.</span></span>

## <a name="under-the-hood"></a><span data-ttu-id="32030-142">幕後</span><span class="sxs-lookup"><span data-stu-id="32030-142">Under the hood</span></span>

<span data-ttu-id="32030-143">Azure AD 應用程式 Proxy 是由兩個部分組成︰</span><span class="sxs-lookup"><span data-stu-id="32030-143">Azure AD Application Proxy consists of two parts:</span></span>

* <span data-ttu-id="32030-144">雲端架構服務︰此服務會在 Azure 中執行，且外部用戶端/使用者會連線到此服務。</span><span class="sxs-lookup"><span data-stu-id="32030-144">The cloud-based service: This service runs in Azure, and is where the external client/user connections are made.</span></span>
* <span data-ttu-id="32030-145">[內部部署連接器](application-proxy-understand-connectors.md)︰這是內部部署元件，此連接器會接聽來自 Azure AD 應用程式 Proxy 服務的要求，並處理對內部應用程式的連線。</span><span class="sxs-lookup"><span data-stu-id="32030-145">[The on-premises connector](application-proxy-understand-connectors.md): An on-premises component, the connector listens for requests from the Azure AD Application Proxy service and handles connections to the internal applications.</span></span> 

<span data-ttu-id="32030-146">以下為建立連接器與應用程式 Proxy 服務之間流量的時機︰</span><span class="sxs-lookup"><span data-stu-id="32030-146">A flow between the connector and the Application Proxy service is established when:</span></span>

* <span data-ttu-id="32030-147">第一次設定連接器。</span><span class="sxs-lookup"><span data-stu-id="32030-147">The connector is first set up.</span></span>
* <span data-ttu-id="32030-148">連接器會從應用程式 Proxy 服務提取設定資訊。</span><span class="sxs-lookup"><span data-stu-id="32030-148">The connector pulls configuration information from the Application Proxy service.</span></span>
* <span data-ttu-id="32030-149">使用者會存取發佈的應用程式。</span><span class="sxs-lookup"><span data-stu-id="32030-149">A user accesses a published application.</span></span>

>[!NOTE]
><span data-ttu-id="32030-150">所有通訊會透過 SSL 發生，且一律源自於至應用程式 Proxy 服務的連接器。</span><span class="sxs-lookup"><span data-stu-id="32030-150">All communications occur over SSL, and they always originate at the connector to the Application Proxy service.</span></span> <span data-ttu-id="32030-151">此服務只會輸出。</span><span class="sxs-lookup"><span data-stu-id="32030-151">The service is outbound only.</span></span>

<span data-ttu-id="32030-152">連接器會使用用戶端憑證來驗證幾乎所有呼叫的應用程式 Proxy 服務。</span><span class="sxs-lookup"><span data-stu-id="32030-152">The connector uses a client certificate to authenticate to the Application Proxy service for nearly all calls.</span></span> <span data-ttu-id="32030-153">此程序的唯一例外是可供建立用戶端憑證的初始設定步驟。</span><span class="sxs-lookup"><span data-stu-id="32030-153">The only exception to this process is the initial setup step, where the client certificate is established.</span></span>

### <a name="installing-the-connector"></a><span data-ttu-id="32030-154">安裝連接器</span><span class="sxs-lookup"><span data-stu-id="32030-154">Installing the connector</span></span>

<span data-ttu-id="32030-155">第一次設定連接器時，會發生下列流程事件：</span><span class="sxs-lookup"><span data-stu-id="32030-155">When the connector is first set up, the following flow events take place:</span></span>

1. <span data-ttu-id="32030-156">連接器註冊服務會做為連接器安裝的一部分。</span><span class="sxs-lookup"><span data-stu-id="32030-156">The connector registration to the service happens as part of the installation of the connector.</span></span> <span data-ttu-id="32030-157">系統會提示使用者輸入其 Azure AD 系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="32030-157">Users are prompted to enter their Azure AD admin credentials.</span></span> <span data-ttu-id="32030-158">接著會向 Azure AD 應用程式 Proxy 服務顯示此驗證的必要權杖。</span><span class="sxs-lookup"><span data-stu-id="32030-158">The token acquired from this authentication is then presented to the Azure AD Application Proxy service.</span></span>
2. <span data-ttu-id="32030-159">應用程式 Proxy 服務會評估權杖。</span><span class="sxs-lookup"><span data-stu-id="32030-159">The Application Proxy service evaluates the token.</span></span> <span data-ttu-id="32030-160">它會確保使用者是在獲得權杖之租用戶內的公司系統管理員。</span><span class="sxs-lookup"><span data-stu-id="32030-160">It ensures that the user is a company administrator within the tenant that the token was issued for.</span></span> <span data-ttu-id="32030-161">如果使用者不是系統管理員，就會終止流程。</span><span class="sxs-lookup"><span data-stu-id="32030-161">If the user is not an administrator, the process is terminated.</span></span>
3. <span data-ttu-id="32030-162">連接器會產生用戶端憑證要求，並與權杖一起傳遞至應用程式 Proxy 服務。</span><span class="sxs-lookup"><span data-stu-id="32030-162">The connector generates a client certificate request and passes it, along with the token, to the Application Proxy service.</span></span> <span data-ttu-id="32030-163">服務接著會驗證權杖，並簽署用戶端憑證要求。</span><span class="sxs-lookup"><span data-stu-id="32030-163">The service in turn verifies the token and signs the client certificate request.</span></span>
4. <span data-ttu-id="32030-164">連接器可以使用此用戶端憑證，以便未來與應用程式 Proxy 服務通訊。</span><span class="sxs-lookup"><span data-stu-id="32030-164">The connector uses the client certificate for future communication with the Application Proxy service.</span></span>
5. <span data-ttu-id="32030-165">連接器會使用其用戶端憑證從服務執行系統設定資料的初始提取，而它現在已準備好接受要求。</span><span class="sxs-lookup"><span data-stu-id="32030-165">The connector performs an initial pull of the system configuration data from the service using its client certificate, and it is now ready to take requests.</span></span>

### <a name="updating-the-configuration-settings"></a><span data-ttu-id="32030-166">更新組態設定</span><span class="sxs-lookup"><span data-stu-id="32030-166">Updating the configuration settings</span></span>

<span data-ttu-id="32030-167">每當應用程式 Proxy 服務更新組態設定時，就會發生下列流程事件︰</span><span class="sxs-lookup"><span data-stu-id="32030-167">Whenever the Application Proxy service updates the configuration settings, the following flow events take place:</span></span>

1. <span data-ttu-id="32030-168">連接器會使用其用戶端憑證連線至應用程式 Proxy 服務內的組態端點。</span><span class="sxs-lookup"><span data-stu-id="32030-168">The connector connects to the configuration endpoint within the Application Proxy service by using its client certificate.</span></span>
2. <span data-ttu-id="32030-169">用戶端憑證經過驗證後，應用程式 Proxy 服務會將組態資料傳回連接器 (例如，連接器應屬之連接器群組)。</span><span class="sxs-lookup"><span data-stu-id="32030-169">After the client certificate has been validated, the Application Proxy service returns configuration data to the connector (for example, the connector group that the connector should be part of).</span></span>
3. <span data-ttu-id="32030-170">如果目前的憑證已存在超過 180 天，連接器就會產生新的憑證要求，每隔 180 天會有效地更新用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="32030-170">If the current certificate is more than 180 days old, the connector generates a new certificate request, which effectively updates the client certificate every 180 days.</span></span>

### <a name="accessing-published-applications"></a><span data-ttu-id="32030-171">存取已發佈的應用程式</span><span class="sxs-lookup"><span data-stu-id="32030-171">Accessing published applications</span></span>

<span data-ttu-id="32030-172">當使用者存取已發佈的應用程式時，會在應用程式 Proxy 服務和應用程式 Proxy 連接器之間進行下列事件：</span><span class="sxs-lookup"><span data-stu-id="32030-172">When users access a published application, the following events take place between the Application Proxy service and the Application Proxy connector:</span></span>

1. [<span data-ttu-id="32030-173">服務會驗證應用程式的使用者</span><span class="sxs-lookup"><span data-stu-id="32030-173">The service authenticates the user for the app</span></span>](#the-service-checks-the-configuration-settings-for-the-app)
2. [<span data-ttu-id="32030-174">服務會將要求放在連接器佇列中</span><span class="sxs-lookup"><span data-stu-id="32030-174">The service places a request in the connector queue</span></span>](#The-service-places-a-request-in-the-connector-queue)
3. [<span data-ttu-id="32030-175">連接器會處理來自佇列的要求</span><span class="sxs-lookup"><span data-stu-id="32030-175">A connector processes the request from the queue</span></span>](#the-connector-receives-the-request-from-the-queue)
4. [<span data-ttu-id="32030-176">連接器會等候回應</span><span class="sxs-lookup"><span data-stu-id="32030-176">The connector waits for a response</span></span>](#the-connector-waits-for-a-response)
5. [<span data-ttu-id="32030-177">服務會將資料串流給使用者</span><span class="sxs-lookup"><span data-stu-id="32030-177">The service streams data to the user</span></span>](#the-service-streams-data-to-the-user)

<span data-ttu-id="32030-178">若要深入了解每個步驟中所發生的事項，請繼續閱讀。</span><span class="sxs-lookup"><span data-stu-id="32030-178">To learn more about what takes place in each of these steps, keep reading.</span></span>


#### <a name="1-the-service-authenticates-the-user-for-the-app"></a><span data-ttu-id="32030-179">1.服務會驗證應用程式的使用者</span><span class="sxs-lookup"><span data-stu-id="32030-179">1. The service authenticates the user for the app</span></span>

<span data-ttu-id="32030-180">如果您將應用程式設定成使用 Passthrough 作為其預先驗證方法時，就會跳過本節中的步驟。</span><span class="sxs-lookup"><span data-stu-id="32030-180">If you configured the app to use Passthrough as its preauthentication method, the steps in this section are skipped.</span></span>

<span data-ttu-id="32030-181">如果您將應用程式設定為以 Azure AD 預先驗證時，使用者會重新導向至 Azure AD STS 驗證，並採取下列步驟：</span><span class="sxs-lookup"><span data-stu-id="32030-181">If you configured the app to preauthenticate with Azure AD, users are redirected to the Azure AD STS to authenticate, and the following steps take place:</span></span>

1. <span data-ttu-id="32030-182">應用程式 Proxy 會檢查特定應用程式的所有條件式存取原則需求。</span><span class="sxs-lookup"><span data-stu-id="32030-182">Application Proxy checks for any conditional access policy requirements for the specific application.</span></span> <span data-ttu-id="32030-183">這個步驟可確保已對應用程式指派使用者。</span><span class="sxs-lookup"><span data-stu-id="32030-183">This step ensures that the user has been assigned to the application.</span></span> <span data-ttu-id="32030-184">如果需要雙步驟驗證，驗證順序會提示使用者進行第二驗證方法。</span><span class="sxs-lookup"><span data-stu-id="32030-184">If two-step verification is required, the authentication sequence prompts the user for a second authentication method.</span></span>

2. <span data-ttu-id="32030-185">通過所有檢查後，Azure AD STS 會針對應用程式發出已簽署權杖，並將使用者重新導向回到應用程式 Proxy 服務。</span><span class="sxs-lookup"><span data-stu-id="32030-185">After all checks have passed, the Azure AD STS issues a signed token for the application and redirects the user back to the Application Proxy service.</span></span>

3. <span data-ttu-id="32030-186">應用程式 Proxy 會驗證權杖已發給正確的應用程式。</span><span class="sxs-lookup"><span data-stu-id="32030-186">Application Proxy verifies that the token was issued to correct the application.</span></span> <span data-ttu-id="32030-187">它也會執行其他檢查，例如確保權杖是由 Azure AD 所簽署，且仍在有效期限內。</span><span class="sxs-lookup"><span data-stu-id="32030-187">It performs other checks also, such as ensuring that the token was signed by Azure AD, and that it is still within the valid window.</span></span>

4. <span data-ttu-id="32030-188">應用程式 Proxy 會設定加密的驗證 cookie，以表示已發生應用程式驗證。</span><span class="sxs-lookup"><span data-stu-id="32030-188">Application Proxy sets an encrypted authentication cookie to indicate that authentication to the application has occurred.</span></span> <span data-ttu-id="32030-189">此 cookie 包含根據 Azure AD 的權杖和其他資料之到期時間戳記，例如以驗證為基礎的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="32030-189">The cookie includes an expiration timestamp that's based on the token from Azure AD and other data, such as the user name that the authentication is based on.</span></span> <span data-ttu-id="32030-190">會使用僅應用程式 Proxy 服務所知的私密金鑰來加密此 cookie。</span><span class="sxs-lookup"><span data-stu-id="32030-190">The cookie is encrypted with a private key known only to the Application Proxy service.</span></span>

5. <span data-ttu-id="32030-191">應用程式 Proxy 會將使用者重新導向回到原始要求的 URL。</span><span class="sxs-lookup"><span data-stu-id="32030-191">Application Proxy redirects the user back to the originally requested URL.</span></span>

<span data-ttu-id="32030-192">如果預先驗證步驟的任何部分失敗，使用者的要求會遭到拒絕，且使用者會顯示訊息，指出問題的來源。</span><span class="sxs-lookup"><span data-stu-id="32030-192">If any part of the preauthentication steps fails, the user’s request is denied, and the user is shown a message indicating the source of the problem.</span></span>


#### <a name="2-the-service-places-a-request-in-the-connector-queue"></a><span data-ttu-id="32030-193">2.服務會將要求放在連接器佇列中</span><span class="sxs-lookup"><span data-stu-id="32030-193">2. The service places a request in the connector queue</span></span>

<span data-ttu-id="32030-194">連接器保持對應用程式 Proxy 服務開啟輸出連線。</span><span class="sxs-lookup"><span data-stu-id="32030-194">Connectors keep an outbound connection open to the Application Proxy service.</span></span> <span data-ttu-id="32030-195">當要求傳入時，服務會在其中一個開啟連線上佇列要求，以供連接器挑選。</span><span class="sxs-lookup"><span data-stu-id="32030-195">When a request comes in, the service queues up the request on one of the open connections for the connector to pick up.</span></span>

<span data-ttu-id="32030-196">要求包含來自應用程式的項目，例如要求標頭、來自加密 cookie 的資料、提出要求的使用者，以及要求識別碼。</span><span class="sxs-lookup"><span data-stu-id="32030-196">The request includes items from the application, such as the request headers, data from the encrypted cookie, the user making the request, and the request ID.</span></span> <span data-ttu-id="32030-197">雖然來自加密 cookie 的資料會與要求一起傳送，但驗證 cookie 本身並不是。</span><span class="sxs-lookup"><span data-stu-id="32030-197">Although data from the encrypted cookie is sent with the request, the authentication cookie itself is not.</span></span>

#### <a name="3-the-connector-processes-the-request-from-the-queue"></a><span data-ttu-id="32030-198">3.連接器會處理來自佇列的要求。</span><span class="sxs-lookup"><span data-stu-id="32030-198">3. The connector processes the request from the queue.</span></span> 

<span data-ttu-id="32030-199">根據要求，應用程式 Proxy 會執行下列其中一個動作︰</span><span class="sxs-lookup"><span data-stu-id="32030-199">Based on the request, Application Proxy performs one of the following actions:</span></span>

* <span data-ttu-id="32030-200">如果要求是簡單的作業 (例如，主體內沒有資料現狀符合 RESTful「GET」要求)，連接器會建立連往目標內部資源的連線，然後等候回應。</span><span class="sxs-lookup"><span data-stu-id="32030-200">If the request is a simple operation (for example, there is no data within the body as is with a RESTful *GET* request), the connector makes a connection to the target internal resource and then waits for a response.</span></span>

* <span data-ttu-id="32030-201">如果要求在主體中具有與它相關聯的資料 (例如，RESTful「POST」作業)，連接器會使用用戶端憑證建立與應用程式 Proxy 執行個體的輸出連線。</span><span class="sxs-lookup"><span data-stu-id="32030-201">If the request has data associated with it in the body (for example, a RESTful *POST* operation), the connector makes an outbound connection by using the client certificate to the Application Proxy instance.</span></span> <span data-ttu-id="32030-202">它會建立此連線來要求資料，並開啟與內部部署資源的連線。</span><span class="sxs-lookup"><span data-stu-id="32030-202">It makes this connection to request the data and open a connection to the internal resource.</span></span> <span data-ttu-id="32030-203">在收到來自連接器的要求後，應用程式 Proxy 服務會開始接受來自使用者的內容，並將資料轉送至連接器。</span><span class="sxs-lookup"><span data-stu-id="32030-203">After it receives the request from the connector, the Application Proxy service begins accepting content from the user and forwards data to the connector.</span></span> <span data-ttu-id="32030-204">連接器會依次將資料轉送到內部資源。</span><span class="sxs-lookup"><span data-stu-id="32030-204">The connector, in turn, forwards the data to the internal resource.</span></span>

#### <a name="4-the-connector-waits-for-a-response"></a><span data-ttu-id="32030-205">4.連接器會等候回應。</span><span class="sxs-lookup"><span data-stu-id="32030-205">4. The connector waits for a response.</span></span>

<span data-ttu-id="32030-206">完成所有內容的要求並傳輸至後端後，連接器會等候回應。</span><span class="sxs-lookup"><span data-stu-id="32030-206">After the request and transmission of all content to the back end is complete, the connector waits for a response.</span></span>

<span data-ttu-id="32030-207">在收到回應後，連接器會建立對應用程式 Proxy 服務的輸出連線，以傳回標頭詳細資料，並開始串流傳回的資料。</span><span class="sxs-lookup"><span data-stu-id="32030-207">After it receives a response, the connector makes an outbound connection to the Application Proxy service, to return the header details and begin streaming the return data.</span></span>

#### <a name="5-the-service-streams-data-to-the-user"></a><span data-ttu-id="32030-208">5.服務會將資料串流給使用者。</span><span class="sxs-lookup"><span data-stu-id="32030-208">5. The service streams data to the user.</span></span> 

<span data-ttu-id="32030-209">應用程式的一些處理可能會在這裡發生。</span><span class="sxs-lookup"><span data-stu-id="32030-209">Some processing of the application may occur here.</span></span> <span data-ttu-id="32030-210">如果您將應用程式中的應用程式 Proxy 應用程式設定為轉譯標頭或 URL，會視需要在此步驟進行該處理。</span><span class="sxs-lookup"><span data-stu-id="32030-210">If you configured Application Proxy to translate headers or URLs in your application, that processing happens as needed during this step.</span></span>


## <a name="next-steps"></a><span data-ttu-id="32030-211">後續步驟</span><span class="sxs-lookup"><span data-stu-id="32030-211">Next steps</span></span>

[<span data-ttu-id="32030-212">使用 Azure AD 應用程式 Proxy 時的網路拓撲考量</span><span class="sxs-lookup"><span data-stu-id="32030-212">Network topology considerations when using Azure AD Application Proxy</span></span>](application-proxy-network-topology-considerations.md)

[<span data-ttu-id="32030-213">了解 Azure AD 應用程式 Proxy 連接器</span><span class="sxs-lookup"><span data-stu-id="32030-213">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)
