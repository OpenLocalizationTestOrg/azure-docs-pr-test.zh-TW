---
title: "aaaHow tooprovide 安全遠端存取 tooon 內部部署應用程式"
description: "涵蓋如何 toouse Azure AD Application Proxy tooprovide 安全遠端存取 tooyour 內部部署應用程式。"
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: d5450da1-9e06-4d08-8146-011c84922ab5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 289e970ed0596fcd06ccf6b2ad92203366fbb494
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooprovide-secure-remote-access-tooon-premises-applications"></a><span data-ttu-id="c47a8-103">如何 tooprovide 安全的遠端存取 tooon 內部部署應用程式</span><span class="sxs-lookup"><span data-stu-id="c47a8-103">How tooprovide secure remote access tooon-premises applications</span></span>

<span data-ttu-id="c47a8-104">員工目前想 toobe 產能在任何位置，在任何時間，以及從任何裝置。</span><span class="sxs-lookup"><span data-stu-id="c47a8-104">Employees today want toobe productive at any place, at any time, and from any device.</span></span> <span data-ttu-id="c47a8-105">不管它們是平板電腦、 電話或膝上型電腦，他們想 toowork 自己的裝置上。</span><span class="sxs-lookup"><span data-stu-id="c47a8-105">They want toowork on their own devices, whether they be tablets, phones, or laptops.</span></span> <span data-ttu-id="c47a8-106">以及他們希望 toobe 無法 tooaccess 其應用程式，內部 hello 雲端中的 SaaS 應用程式和公司應用程式。</span><span class="sxs-lookup"><span data-stu-id="c47a8-106">And they expect toobe able tooaccess all their applications, both SaaS apps in hello cloud and corporate apps on-premises.</span></span> <span data-ttu-id="c47a8-107">提供存取 tooon 內部部署應用程式的傳統上會涉及虛擬私人網路 (Vpn) 或非軍事區域 (Dmz)。</span><span class="sxs-lookup"><span data-stu-id="c47a8-107">Providing access tooon-premises applications has traditionally involved virtual private networks (VPNs) or demilitarized zones (DMZs).</span></span> <span data-ttu-id="c47a8-108">不是安全的這些解決方案複雜且困難 toomake 只他們是昂貴的 tooset 及管理。</span><span class="sxs-lookup"><span data-stu-id="c47a8-108">Not only are these solutions complex and hard toomake secure, but they are costly tooset up and manage.</span></span>

<span data-ttu-id="c47a8-109">還有更好的辦法！</span><span class="sxs-lookup"><span data-stu-id="c47a8-109">There is a better way!</span></span>

<span data-ttu-id="c47a8-110">Hello 行動優先 （contract-first） 中的現代員工，雲端優先世界需要現代的遠端存取解決方案。</span><span class="sxs-lookup"><span data-stu-id="c47a8-110">A modern workforce in hello mobile-first, cloud-first world needs a modern remote access solution.</span></span> <span data-ttu-id="c47a8-111">Azure AD 應用程式 Proxy 是 Azure Active Directory 的一項功能，並提供遠端存取做為服務。</span><span class="sxs-lookup"><span data-stu-id="c47a8-111">Azure AD Application Proxy is a feature of Azure Active Directory that offers remote access as a service.</span></span> <span data-ttu-id="c47a8-112">這表示它是簡單 toodeploy、 使用和管理。</span><span class="sxs-lookup"><span data-stu-id="c47a8-112">That means it's easy toodeploy, use, and manage.</span></span>

[!INCLUDE [identity](../../includes/azure-ad-licenses.md)]

## <a name="what-is-azure-active-directory-application-proxy"></a><span data-ttu-id="c47a8-113">什麼是 Azure Active Directory 應用程式 Proxy？</span><span class="sxs-lookup"><span data-stu-id="c47a8-113">What is Azure Active Directory Application Proxy?</span></span>
<span data-ttu-id="c47a8-114">Azure AD 應用程式 Proxy 針對 Web 應用程式託管的內部部署，提供單一登入 (SSO) 及安全的遠端存取。</span><span class="sxs-lookup"><span data-stu-id="c47a8-114">Azure AD Application Proxy provides single sign-on (SSO) and secure remote access for web applications hosted on-premises.</span></span> <span data-ttu-id="c47a8-115">您會想 toopublish 某些應用程式包含 SharePoint 網站、 Outlook Web Access 中或任何其他 LOB web 應用程式必須。</span><span class="sxs-lookup"><span data-stu-id="c47a8-115">Some apps you would want toopublish include SharePoint sites, Outlook Web Access, or any other LOB web applications you have.</span></span> <span data-ttu-id="c47a8-116">這些應用程式與 Azure AD 整合的內部部署 web hello 相同的識別，並控制由 O365 的平台。</span><span class="sxs-lookup"><span data-stu-id="c47a8-116">These on-premises web applications are integrated with Azure AD, hello same identity and control platform that is used by O365.</span></span> <span data-ttu-id="c47a8-117">使用者可以存取您在內部部署應用程式 hello 與 Azure AD 整合他們存取 O365 和其他 SaaS 應用程式的方式相同。</span><span class="sxs-lookup"><span data-stu-id="c47a8-117">End users can access your on-premises applications hello same way they access O365 and other SaaS apps integrated with Azure AD.</span></span> <span data-ttu-id="c47a8-118">您不需要 toochange hello 網路基礎結構，或為您的使用者需要 VPN tooprovide 此解決方案。</span><span class="sxs-lookup"><span data-stu-id="c47a8-118">You don't need toochange hello network infrastructure or require VPN tooprovide this solution for your users.</span></span>

## <a name="why-is-application-proxy-a-better-solution"></a><span data-ttu-id="c47a8-119">為什麼應用程式 Proxy 是較佳的解決方案？</span><span class="sxs-lookup"><span data-stu-id="c47a8-119">Why is Application Proxy a better solution?</span></span>
<span data-ttu-id="c47a8-120">Azure AD 應用程式 Proxy 提供簡單、 安全且符合成本效益的遠端存取解決方案 tooall 在內部部署應用程式。</span><span class="sxs-lookup"><span data-stu-id="c47a8-120">Azure AD Application Proxy provides a simple, secure, and cost-effective remote access solution tooall your on-premises applications.</span></span>

<span data-ttu-id="c47a8-121">Azure AD 應用程式 Proxy：</span><span class="sxs-lookup"><span data-stu-id="c47a8-121">Azure AD Application Proxy is:</span></span>

* <span data-ttu-id="c47a8-122">**簡單**</span><span class="sxs-lookup"><span data-stu-id="c47a8-122">**Simple**</span></span>
   * <span data-ttu-id="c47a8-123">您不需要 toochange 或更新您的應用程式 toowork 應用程式 proxy。</span><span class="sxs-lookup"><span data-stu-id="c47a8-123">You don't need toochange or update your applications toowork with Application Proxy.</span></span> 
   * <span data-ttu-id="c47a8-124">使用者享有一致的驗證體驗。</span><span class="sxs-lookup"><span data-stu-id="c47a8-124">Your users get a consistent authentication experience.</span></span> <span data-ttu-id="c47a8-125">他們可以使用 hello 雲端和您的應用程式內部部署中的 hello MyApps tooget 入口網站單一登入 tooboth SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c47a8-125">They can use hello MyApps portal tooget single sign-on tooboth SaaS apps in hello cloud and your apps on-premises.</span></span> 
* <span data-ttu-id="c47a8-126">**安全**</span><span class="sxs-lookup"><span data-stu-id="c47a8-126">**Secure**</span></span>
   * <span data-ttu-id="c47a8-127">當您發行應用程式使用 Azure AD Application Proxy 時，您可以利用的 hello 豐富的授權控制項和安全性分析在 Azure 中。</span><span class="sxs-lookup"><span data-stu-id="c47a8-127">When you publish your apps using Azure AD Application Proxy, you can take advantage of hello rich authorization controls and security analytics in Azure.</span></span> <span data-ttu-id="c47a8-128">您會取得雲端級別安全性和 Azure 安全性功能，例如條件式存取和雙步驟驗證。</span><span class="sxs-lookup"><span data-stu-id="c47a8-128">You get cloud-scale security and Azure security features like conditional access and two-step verification.</span></span>
   * <span data-ttu-id="c47a8-129">您不需要 tooopen 任何輸入的連線透過防火牆 toogive 您使用者的遠端存取。</span><span class="sxs-lookup"><span data-stu-id="c47a8-129">You don't have tooopen any inbound connections through your firewall toogive your users remote access.</span></span> 
* <span data-ttu-id="c47a8-130">**符合成本效益**</span><span class="sxs-lookup"><span data-stu-id="c47a8-130">**Cost-effective**</span></span>
   * <span data-ttu-id="c47a8-131">應用程式 Proxy 可 hello 雲端中，因此可以節省時間和金錢。</span><span class="sxs-lookup"><span data-stu-id="c47a8-131">Application Proxy works in hello cloud, so you can save time and money.</span></span> <span data-ttu-id="c47a8-132">在內部部署解決方案通常需要您 tooset 組成，而維護 Dmz 中，邊緣的伺服器或其他複雜的基礎結構。</span><span class="sxs-lookup"><span data-stu-id="c47a8-132">On-premises solutions typically require you tooset up and maintain DMZs, edge servers, or other complex infrastructures.</span></span>  

## <a name="what-kind-of-applications-work-with-application-proxy"></a><span data-ttu-id="c47a8-133">哪種應用程式可與應用程式 Proxy 搭配運作？</span><span class="sxs-lookup"><span data-stu-id="c47a8-133">What kind of applications work with Application Proxy?</span></span>
<span data-ttu-id="c47a8-134">透過 Azure AD 應用程式 Proxy，您可以存取不同類型的內部應用程式︰</span><span class="sxs-lookup"><span data-stu-id="c47a8-134">With Azure AD Application Proxy you can access different types of internal applications:</span></span>

* <span data-ttu-id="c47a8-135">使用[整合式 Windows 驗證](active-directory-application-proxy-sso-using-kcd.md)來進行驗證的 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="c47a8-135">Web applications that use [Integrated Windows Authentication](active-directory-application-proxy-sso-using-kcd.md) for authentication</span></span>  
* <span data-ttu-id="c47a8-136">使用表單架構或[標頭型](application-proxy-ping-access.md)存取的 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="c47a8-136">Web applications that use form-based or [header-based](application-proxy-ping-access.md) access</span></span>  
* <span data-ttu-id="c47a8-137">Web 應用程式開發介面，您想要在不同裝置上的 tooexpose toorich 應用程式</span><span class="sxs-lookup"><span data-stu-id="c47a8-137">Web APIs that you want tooexpose toorich applications on different devices</span></span>  
* <span data-ttu-id="c47a8-138">裝載在[遠端桌面閘道](application-proxy-publish-remote-desktop.md)之後的應用程式</span><span class="sxs-lookup"><span data-stu-id="c47a8-138">Applications hosted behind a [Remote Desktop Gateway](application-proxy-publish-remote-desktop.md)</span></span>  
* <span data-ttu-id="c47a8-139">豐富型用戶端應用程式與 hello Active Directory 驗證程式庫 (ADAL) 整合</span><span class="sxs-lookup"><span data-stu-id="c47a8-139">Rich client apps that are integrated with hello Active Directory Authentication Library (ADAL)</span></span>

## <a name="how-does-application-proxy-work"></a><span data-ttu-id="c47a8-140">Application Proxy 的運作方式為何？</span><span class="sxs-lookup"><span data-stu-id="c47a8-140">How does Application Proxy work?</span></span>
<span data-ttu-id="c47a8-141">您需要 tooconfigure toomake 應用程式 Proxy 工作的兩個元件： 連接器和外部端點。</span><span class="sxs-lookup"><span data-stu-id="c47a8-141">There are two components that you need tooconfigure toomake Application Proxy work: a connector and an external endpoint.</span></span> 

<span data-ttu-id="c47a8-142">hello 連接器是輕量型的代理程式位於內部網路的 Windows 伺服器上。</span><span class="sxs-lookup"><span data-stu-id="c47a8-142">hello connector is a lightweight agent that sits on a Windows Server inside your network.</span></span> <span data-ttu-id="c47a8-143">hello 連接器有助於 hello 流量從 hello hello 雲端 tooyour 應用程式在內部部署中的應用程式 Proxy 服務。</span><span class="sxs-lookup"><span data-stu-id="c47a8-143">hello connector facilitates hello traffic flow from hello Application Proxy service in hello cloud tooyour application on-premises.</span></span> <span data-ttu-id="c47a8-144">它只會使用輸出連線，因此您尚未 tooopen 任何輸入連接埠，或將任何項目放在 hello 周邊網路。</span><span class="sxs-lookup"><span data-stu-id="c47a8-144">It only uses outbound connections, so you don't have tooopen any inbound ports or put anything in hello DMZ.</span></span> <span data-ttu-id="c47a8-145">hello 連接器是無狀態，並視 hello 雲端提取資訊。</span><span class="sxs-lookup"><span data-stu-id="c47a8-145">hello connectors are stateless and pull information from hello cloud as necessary.</span></span> <span data-ttu-id="c47a8-146">如需連接器的詳細資訊，例如如何負載平衡和驗證，請參閱[了解 Azure AD 應用程式 Proxy 連接器](application-proxy-understand-connectors.md)。</span><span class="sxs-lookup"><span data-stu-id="c47a8-146">For more information about connectors, like how they load-balance and authenticate, see [Understand Azure AD Application Proxy connectors](application-proxy-understand-connectors.md).</span></span> 

<span data-ttu-id="c47a8-147">hello 外部端點會是您的使用者如何到達您的應用程式網路外部。</span><span class="sxs-lookup"><span data-stu-id="c47a8-147">hello external endpoint is how your users reach your applications while outside of your network.</span></span> <span data-ttu-id="c47a8-148">它們可以是瀏覽直接 tooan 外部 URL，以決定時，或它們可以透過 hello MyApps 入口網站存取 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c47a8-148">They can either go directly tooan external URL that you determine, or they can access hello application through hello MyApps portal.</span></span> <span data-ttu-id="c47a8-149">當使用者前往 tooone 這些端點時，它們在 Azure AD 進行驗證，然後透過進行路由傳送嗨連接器 toohello 在內部部署應用程式。</span><span class="sxs-lookup"><span data-stu-id="c47a8-149">When users go tooone of these endpoints, they authenticate in Azure AD and then are routed through hello connector toohello on-premises application.</span></span>

 ![Azure AD 應用程式 Proxy 圖表](./media/active-directory-application-proxy-get-started/azureappproxxy.png)

1. <span data-ttu-id="c47a8-151">hello 使用者存取透過 hello 應用程式 Proxy 服務的 hello 應用程式，並會導向的 toohello Azure AD 登入頁面 tooauthenticate。</span><span class="sxs-lookup"><span data-stu-id="c47a8-151">hello user accesses hello application through hello Application Proxy service and is directed toohello Azure AD sign-in page tooauthenticate.</span></span>
2. <span data-ttu-id="c47a8-152">在成功登入之後，會產生語彙基元，並將其傳送 toohello 用戶端裝置中。</span><span class="sxs-lookup"><span data-stu-id="c47a8-152">After a successful sign-in, a token is generated and sent toohello client device.</span></span>
3. <span data-ttu-id="c47a8-153">hello 用戶端會傳送 hello 語彙基元 toohello 應用程式 Proxy 服務，擷取 hello 使用者主要名稱 (UPN) 和安全性主體名稱 (SPN)，從 hello 權杖，然後會引導 hello 要求 toohello 應用程式 Proxy 連接器。</span><span class="sxs-lookup"><span data-stu-id="c47a8-153">hello client sends hello token toohello Application Proxy service, which retrieves hello user principal name (UPN) and security principal name (SPN) from hello token, then directs hello request toohello Application Proxy connector.</span></span>
4. <span data-ttu-id="c47a8-154">如果您已設定單一登入，hello 連接器執行代表 hello 使用者所需的任何其他驗證。</span><span class="sxs-lookup"><span data-stu-id="c47a8-154">If you have configured single sign-on, hello connector performs any additional authentication required on behalf of hello user.</span></span>
5. <span data-ttu-id="c47a8-155">hello 連接器會傳送 hello 要求 toohello 在內部部署應用程式。</span><span class="sxs-lookup"><span data-stu-id="c47a8-155">hello connector sends hello request toohello on-premises application.</span></span>  
6. <span data-ttu-id="c47a8-156">透過應用程式 Proxy 服務和連接器 toohello 使用者會傳送 hello 回應。</span><span class="sxs-lookup"><span data-stu-id="c47a8-156">hello response is sent through Application Proxy service and connector toohello user.</span></span>

### <a name="single-sign-on"></a><span data-ttu-id="c47a8-157">單一登入</span><span class="sxs-lookup"><span data-stu-id="c47a8-157">Single sign-on</span></span>
<span data-ttu-id="c47a8-158">Azure AD 應用程式 Proxy 提供單一登入 (SSO) tooapplications 使用整合式 Windows 驗證 (IWA) 」 或 「 宣告感知應用程式。</span><span class="sxs-lookup"><span data-stu-id="c47a8-158">Azure AD Application Proxy provides single sign-on (SSO) tooapplications that use Integrated Windows Authentication (IWA), or claims-aware applications.</span></span> <span data-ttu-id="c47a8-159">如果您的應用程式使用 IWA，應用程式 Proxy 會模擬使用 Kerberos 限制委派 tooprovide SSO hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="c47a8-159">If your application uses IWA, Application Proxy impersonates hello user using Kerberos Constrained Delegation tooprovide SSO.</span></span> <span data-ttu-id="c47a8-160">如果您有 Azure Active Directory 的信任的宣告感知應用程式時，SSO 運作，因為已由 Azure AD 驗證 hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="c47a8-160">If you have a claims-aware application that trusts Azure Active Directory, SSO works because hello user was already authenticated by Azure AD.</span></span>

<span data-ttu-id="c47a8-161">如需有關 Kerberos 的詳細資訊，請參閱[所有您想要關於 Kerberos 限制委派 (KCD) tooknow](https://blogs.technet.microsoft.com/applicationproxyblog/2015/09/21/all-you-want-to-know-about-kerberos-constrained-delegation-kcd)。</span><span class="sxs-lookup"><span data-stu-id="c47a8-161">For more information about Kerberos, see [All you want tooknow about Kerberos Constrained Delegation (KCD)](https://blogs.technet.microsoft.com/applicationproxyblog/2015/09/21/all-you-want-to-know-about-kerberos-constrained-delegation-kcd).</span></span>

### <a name="managing-apps"></a><span data-ttu-id="c47a8-162">管理應用程式</span><span class="sxs-lookup"><span data-stu-id="c47a8-162">Managing apps</span></span>
<span data-ttu-id="c47a8-163">其中一個應用程式發佈應用程式 proxy 時，您可以像是其他任何企業應用程式在 hello Azure 入口網站中加以管理。</span><span class="sxs-lookup"><span data-stu-id="c47a8-163">One your app is published with Application Proxy, you can manage it like any other enterprise app in hello Azure portal.</span></span> <span data-ttu-id="c47a8-164">您可以使用 Azure Active Directory 安全性功能，例如條件式存取和兩步驟驗證、 控制使用者的權限，以及自訂應用程式的商標 hello。</span><span class="sxs-lookup"><span data-stu-id="c47a8-164">You can use Azure Active Directory security features like conditional access and two-step verification, control user permissions, and customize hello branding for your app.</span></span> 

## <a name="get-started"></a><span data-ttu-id="c47a8-165">開始使用</span><span class="sxs-lookup"><span data-stu-id="c47a8-165">Get started</span></span>

<span data-ttu-id="c47a8-166">設定 Application Proxy 之前，確定您有支援的 [Azure Active Directory 版本](https://azure.microsoft.com/pricing/details/active-directory/)，以及您是全域管理員的 Azure AD 目錄。</span><span class="sxs-lookup"><span data-stu-id="c47a8-166">Before you configure Application Proxy, make sure you have a supported [Azure Active Directory edition](https://azure.microsoft.com/pricing/details/active-directory/) and an Azure AD directory for which you are a global administrator.</span></span>

<span data-ttu-id="c47a8-167">開始使用 Application Proxy 有兩個步驟：</span><span class="sxs-lookup"><span data-stu-id="c47a8-167">Get started with Application Proxy in two steps:</span></span>

1. <span data-ttu-id="c47a8-168">[啟用應用程式 Proxy 及設定 hello 連接器](active-directory-application-proxy-enable.md)。</span><span class="sxs-lookup"><span data-stu-id="c47a8-168">[Enable Application Proxy and configure hello connector](active-directory-application-proxy-enable.md).</span></span>    
2. <span data-ttu-id="c47a8-169">[發行應用程式](active-directory-application-proxy-publish.md)-使用 hello 快速、 簡易的精靈 tooget 已發行，而且可存取您在內部部署應用程式從遠端。</span><span class="sxs-lookup"><span data-stu-id="c47a8-169">[Publish applications](active-directory-application-proxy-publish.md) - use hello quick and easy wizard tooget your on-premises apps published and accessible remotely.</span></span>

## <a name="whats-next"></a><span data-ttu-id="c47a8-170">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c47a8-170">What's next?</span></span>
<span data-ttu-id="c47a8-171">您發佈第一個應用程式後，應用程式 Proxy 還有其他更多用途：</span><span class="sxs-lookup"><span data-stu-id="c47a8-171">Once you publish your first app, there's a lot more you can do with Application Proxy:</span></span>

* [<span data-ttu-id="c47a8-172">啟用單一登入</span><span class="sxs-lookup"><span data-stu-id="c47a8-172">Enable single-sign on</span></span>](active-directory-application-proxy-sso-using-kcd.md)
* [<span data-ttu-id="c47a8-173">使用您自己的網域名稱發行應用程式</span><span class="sxs-lookup"><span data-stu-id="c47a8-173">Publish applications using your own domain name</span></span>](active-directory-application-proxy-custom-domains.md)
* [<span data-ttu-id="c47a8-174">了解 Azure AD 應用程式 Proxy 連接器</span><span class="sxs-lookup"><span data-stu-id="c47a8-174">Learn about Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)
* [<span data-ttu-id="c47a8-175">使用現有的內部部署 Proxy 伺服器</span><span class="sxs-lookup"><span data-stu-id="c47a8-175">Working with existing on-premises Proxy servers</span></span>](application-proxy-working-with-proxy-servers.md) 
* [<span data-ttu-id="c47a8-176">設定自訂首頁</span><span class="sxs-lookup"><span data-stu-id="c47a8-176">Set a custom home page</span></span>](application-proxy-office365-app-launcher.md)

<span data-ttu-id="c47a8-177">如 hello 最新消息和更新，請參閱 hello[應用程式 Proxy 部落格](http://blogs.technet.com/b/applicationproxyblog/)</span><span class="sxs-lookup"><span data-stu-id="c47a8-177">For hello latest news and updates, check out hello [Application Proxy blog](http://blogs.technet.com/b/applicationproxyblog/)</span></span>

