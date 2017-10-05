---
title: "如何為內部部署應用程式提供安全的遠端存取"
description: "涵蓋如何使用 Azure AD 應用程式 Proxy 為您的內部部署應用程式提供安全的遠端存取。"
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
ms.openlocfilehash: 67f7f5b8d411d11c97a8666d1bfc3c0c5f1174ce
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-provide-secure-remote-access-to-on-premises-applications"></a><span data-ttu-id="8b2b4-103">如何為內部部署應用程式提供安全的遠端存取</span><span class="sxs-lookup"><span data-stu-id="8b2b4-103">How to provide secure remote access to on-premises applications</span></span>

<span data-ttu-id="8b2b4-104">現今的員工想要隨時隨地都能在任何裝置發揮生產力。</span><span class="sxs-lookup"><span data-stu-id="8b2b4-104">Employees today want to be productive at any place, at any time, and from any device.</span></span> <span data-ttu-id="8b2b4-105">他們想要在自己的裝置上工作，不論這些裝置是平板電腦、手機或膝上型電腦。</span><span class="sxs-lookup"><span data-stu-id="8b2b4-105">They want to work on their own devices, whether they be tablets, phones, or laptops.</span></span> <span data-ttu-id="8b2b4-106">而且他們期望能夠存取其所有的應用程式︰雲端中的 SaaS 應用程式以及內部部署的公司應用程式。</span><span class="sxs-lookup"><span data-stu-id="8b2b4-106">And they expect to be able to access all their applications, both SaaS apps in the cloud and corporate apps on-premises.</span></span> <span data-ttu-id="8b2b4-107">傳統上，提供內部部署應用程式的存取權會涉及虛擬私人網路 (VPN) 或非軍事區 (DMZ)。</span><span class="sxs-lookup"><span data-stu-id="8b2b4-107">Providing access to on-premises applications has traditionally involved virtual private networks (VPNs) or demilitarized zones (DMZs).</span></span> <span data-ttu-id="8b2b4-108">這些解決方案不僅複雜且難以確保安全，而且設定及管理成本也很高。</span><span class="sxs-lookup"><span data-stu-id="8b2b4-108">Not only are these solutions complex and hard to make secure, but they are costly to set up and manage.</span></span>

<span data-ttu-id="8b2b4-109">還有更好的辦法！</span><span class="sxs-lookup"><span data-stu-id="8b2b4-109">There is a better way!</span></span>

<span data-ttu-id="8b2b4-110">在行動至上、雲端至上的世界裡，現代化的員工需要現代化的遠端存取解決方案。</span><span class="sxs-lookup"><span data-stu-id="8b2b4-110">A modern workforce in the mobile-first, cloud-first world needs a modern remote access solution.</span></span> <span data-ttu-id="8b2b4-111">Azure AD 應用程式 Proxy 是 Azure Active Directory 的一項功能，並提供遠端存取做為服務。</span><span class="sxs-lookup"><span data-stu-id="8b2b4-111">Azure AD Application Proxy is a feature of Azure Active Directory that offers remote access as a service.</span></span> <span data-ttu-id="8b2b4-112">這表示它很容易部署、使用和管理。</span><span class="sxs-lookup"><span data-stu-id="8b2b4-112">That means it's easy to deploy, use, and manage.</span></span>

[!INCLUDE [identity](../../includes/azure-ad-licenses.md)]

## <a name="what-is-azure-active-directory-application-proxy"></a><span data-ttu-id="8b2b4-113">什麼是 Azure Active Directory 應用程式 Proxy？</span><span class="sxs-lookup"><span data-stu-id="8b2b4-113">What is Azure Active Directory Application Proxy?</span></span>
<span data-ttu-id="8b2b4-114">Azure AD 應用程式 Proxy 針對 Web 應用程式託管的內部部署，提供單一登入 (SSO) 及安全的遠端存取。</span><span class="sxs-lookup"><span data-stu-id="8b2b4-114">Azure AD Application Proxy provides single sign-on (SSO) and secure remote access for web applications hosted on-premises.</span></span> <span data-ttu-id="8b2b4-115">您想要發佈的部份應用程式包括 SharePoint 網站、Outlook Web Access 或您擁有的其他任何 LOB Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8b2b4-115">Some apps you would want to publish include SharePoint sites, Outlook Web Access, or any other LOB web applications you have.</span></span> <span data-ttu-id="8b2b4-116">這些內部部署 Web 應用程式會與 Azure AD (O365 所使用的相同身分識別和控制平台) 整合。</span><span class="sxs-lookup"><span data-stu-id="8b2b4-116">These on-premises web applications are integrated with Azure AD, the same identity and control platform that is used by O365.</span></span> <span data-ttu-id="8b2b4-117">終端使用者可以使用和 O365 以及其他與 Azure AD 整合之 SaaS 應用程式相同的存取方式，來存取內部部署應用程式。</span><span class="sxs-lookup"><span data-stu-id="8b2b4-117">End users can access your on-premises applications the same way they access O365 and other SaaS apps integrated with Azure AD.</span></span> <span data-ttu-id="8b2b4-118">您不需要變更網路基礎結構，或需要 VPN 才能為使用者提供此解決方案。</span><span class="sxs-lookup"><span data-stu-id="8b2b4-118">You don't need to change the network infrastructure or require VPN to provide this solution for your users.</span></span>

## <a name="why-is-application-proxy-a-better-solution"></a><span data-ttu-id="8b2b4-119">為什麼應用程式 Proxy 是較佳的解決方案？</span><span class="sxs-lookup"><span data-stu-id="8b2b4-119">Why is Application Proxy a better solution?</span></span>
<span data-ttu-id="8b2b4-120">Azure AD 應用程式 Proxy 可對所有內部部署應用程式提供簡單、安全且符合成本效益的遠端存取解決方案。</span><span class="sxs-lookup"><span data-stu-id="8b2b4-120">Azure AD Application Proxy provides a simple, secure, and cost-effective remote access solution to all your on-premises applications.</span></span>

<span data-ttu-id="8b2b4-121">Azure AD 應用程式 Proxy：</span><span class="sxs-lookup"><span data-stu-id="8b2b4-121">Azure AD Application Proxy is:</span></span>

* <span data-ttu-id="8b2b4-122">**簡單**</span><span class="sxs-lookup"><span data-stu-id="8b2b4-122">**Simple**</span></span>
   * <span data-ttu-id="8b2b4-123">您不需要變更或更新應用程式，即可使用應用程式 Proxy。</span><span class="sxs-lookup"><span data-stu-id="8b2b4-123">You don't need to change or update your applications to work with Application Proxy.</span></span> 
   * <span data-ttu-id="8b2b4-124">使用者享有一致的驗證體驗。</span><span class="sxs-lookup"><span data-stu-id="8b2b4-124">Your users get a consistent authentication experience.</span></span> <span data-ttu-id="8b2b4-125">使用者可以使用 MyApps 入口網站，對於雲端中的 SaaS 應用程式和內部部署的應用程式取得單一登入。</span><span class="sxs-lookup"><span data-stu-id="8b2b4-125">They can use the MyApps portal to get single sign-on to both SaaS apps in the cloud and your apps on-premises.</span></span> 
* <span data-ttu-id="8b2b4-126">**安全**</span><span class="sxs-lookup"><span data-stu-id="8b2b4-126">**Secure**</span></span>
   * <span data-ttu-id="8b2b4-127">當您使用 Azure AD 應用程式 Proxy 發佈應用程式時，您可以利用 Azure 中豐富的授權控制項和安全性分析。</span><span class="sxs-lookup"><span data-stu-id="8b2b4-127">When you publish your apps using Azure AD Application Proxy, you can take advantage of the rich authorization controls and security analytics in Azure.</span></span> <span data-ttu-id="8b2b4-128">您會取得雲端級別安全性和 Azure 安全性功能，例如條件式存取和雙步驟驗證。</span><span class="sxs-lookup"><span data-stu-id="8b2b4-128">You get cloud-scale security and Azure security features like conditional access and two-step verification.</span></span>
   * <span data-ttu-id="8b2b4-129">您不需要開啟透過防火牆的任何輸入連線，為使用者提供遠端存取。</span><span class="sxs-lookup"><span data-stu-id="8b2b4-129">You don't have to open any inbound connections through your firewall to give your users remote access.</span></span> 
* <span data-ttu-id="8b2b4-130">**符合成本效益**</span><span class="sxs-lookup"><span data-stu-id="8b2b4-130">**Cost-effective**</span></span>
   * <span data-ttu-id="8b2b4-131">應用程式 Proxy 在雲端中運作，因此可以節省時間和金錢。</span><span class="sxs-lookup"><span data-stu-id="8b2b4-131">Application Proxy works in the cloud, so you can save time and money.</span></span> <span data-ttu-id="8b2b4-132">內部部署解決方案則一般需要您設定及維護 DMZ、Edge Server 或其他複雜的基礎結構。</span><span class="sxs-lookup"><span data-stu-id="8b2b4-132">On-premises solutions typically require you to set up and maintain DMZs, edge servers, or other complex infrastructures.</span></span>  

## <a name="what-kind-of-applications-work-with-application-proxy"></a><span data-ttu-id="8b2b4-133">哪種應用程式可與應用程式 Proxy 搭配運作？</span><span class="sxs-lookup"><span data-stu-id="8b2b4-133">What kind of applications work with Application Proxy?</span></span>
<span data-ttu-id="8b2b4-134">透過 Azure AD 應用程式 Proxy，您可以存取不同類型的內部應用程式︰</span><span class="sxs-lookup"><span data-stu-id="8b2b4-134">With Azure AD Application Proxy you can access different types of internal applications:</span></span>

* <span data-ttu-id="8b2b4-135">使用[整合式 Windows 驗證](active-directory-application-proxy-sso-using-kcd.md)來進行驗證的 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="8b2b4-135">Web applications that use [Integrated Windows Authentication](active-directory-application-proxy-sso-using-kcd.md) for authentication</span></span>  
* <span data-ttu-id="8b2b4-136">使用表單架構或[標頭型](application-proxy-ping-access.md)存取的 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="8b2b4-136">Web applications that use form-based or [header-based](application-proxy-ping-access.md) access</span></span>  
* <span data-ttu-id="8b2b4-137">您想要公開給不同裝置上豐富應用程式的 Web API</span><span class="sxs-lookup"><span data-stu-id="8b2b4-137">Web APIs that you want to expose to rich applications on different devices</span></span>  
* <span data-ttu-id="8b2b4-138">裝載在[遠端桌面閘道](application-proxy-publish-remote-desktop.md)之後的應用程式</span><span class="sxs-lookup"><span data-stu-id="8b2b4-138">Applications hosted behind a [Remote Desktop Gateway](application-proxy-publish-remote-desktop.md)</span></span>  
* <span data-ttu-id="8b2b4-139">與 Active Directory Authentication Library (ADAL) 整合的豐富型用戶端應用程式</span><span class="sxs-lookup"><span data-stu-id="8b2b4-139">Rich client apps that are integrated with the Active Directory Authentication Library (ADAL)</span></span>

## <a name="how-does-application-proxy-work"></a><span data-ttu-id="8b2b4-140">Application Proxy 的運作方式為何？</span><span class="sxs-lookup"><span data-stu-id="8b2b4-140">How does Application Proxy work?</span></span>
<span data-ttu-id="8b2b4-141">需要設定才能使 Application Proxy 運作的兩個元件：連接器和外部端點。</span><span class="sxs-lookup"><span data-stu-id="8b2b4-141">There are two components that you need to configure to make Application Proxy work: a connector and an external endpoint.</span></span> 

<span data-ttu-id="8b2b4-142">連接器是位於網路內部 Windows 伺服器上的輕量型代理程式。</span><span class="sxs-lookup"><span data-stu-id="8b2b4-142">The connector is a lightweight agent that sits on a Windows Server inside your network.</span></span> <span data-ttu-id="8b2b4-143">連接器有助於從雲端中的 Application Proxy 服務到應用程式內部部署的流量流程。</span><span class="sxs-lookup"><span data-stu-id="8b2b4-143">The connector facilitates the traffic flow from the Application Proxy service in the cloud to your application on-premises.</span></span> <span data-ttu-id="8b2b4-144">連接器僅使用輸出連線，因此您不需要開啟任何輸入連接埠，或在 DMZ 中放置任何物件。</span><span class="sxs-lookup"><span data-stu-id="8b2b4-144">It only uses outbound connections, so you don't have to open any inbound ports or put anything in the DMZ.</span></span> <span data-ttu-id="8b2b4-145">連接器是無狀態的，且在必要時會從雲端提取資訊。</span><span class="sxs-lookup"><span data-stu-id="8b2b4-145">The connectors are stateless and pull information from the cloud as necessary.</span></span> <span data-ttu-id="8b2b4-146">如需連接器的詳細資訊，例如如何負載平衡和驗證，請參閱[了解 Azure AD 應用程式 Proxy 連接器](application-proxy-understand-connectors.md)。</span><span class="sxs-lookup"><span data-stu-id="8b2b4-146">For more information about connectors, like how they load-balance and authenticate, see [Understand Azure AD Application Proxy connectors](application-proxy-understand-connectors.md).</span></span> 

<span data-ttu-id="8b2b4-147">外部端點是使用者在網路外部聯繫應用程式的方式。</span><span class="sxs-lookup"><span data-stu-id="8b2b4-147">The external endpoint is how your users reach your applications while outside of your network.</span></span> <span data-ttu-id="8b2b4-148">外部端點可以直接存取您決定的外部 URL，也可以透過 MyApps 入口網站存取應用程式。</span><span class="sxs-lookup"><span data-stu-id="8b2b4-148">They can either go directly to an external URL that you determine, or they can access the application through the MyApps portal.</span></span> <span data-ttu-id="8b2b4-149">使用者存取這些端點的其中一個時，會在 Azure AD 中進行驗證，然後透過連接器路由至內部部署應用程式。</span><span class="sxs-lookup"><span data-stu-id="8b2b4-149">When users go to one of these endpoints, they authenticate in Azure AD and then are routed through the connector to the on-premises application.</span></span>

 ![Azure AD 應用程式 Proxy 圖表](./media/active-directory-application-proxy-get-started/azureappproxxy.png)

1. <span data-ttu-id="8b2b4-151">使用者會透過應用程式 Proxy 服務存取應用程式，然後被導向 Azure AD 登入頁面進行驗證。</span><span class="sxs-lookup"><span data-stu-id="8b2b4-151">The user accesses the application through the Application Proxy service and is directed to the Azure AD sign-in page to authenticate.</span></span>
2. <span data-ttu-id="8b2b4-152">成功登入之後，系統會產生權杖並傳送給用戶端裝置。</span><span class="sxs-lookup"><span data-stu-id="8b2b4-152">After a successful sign-in, a token is generated and sent to the client device.</span></span>
3. <span data-ttu-id="8b2b4-153">用戶端會將權杖傳送至應用程式 Proxy 服務，該服務會取出權杖的使用者主體名稱 (UPN) 和安全性主體名稱 (SPN)，然後將要求導向至應用程式 Proxy 連接器。</span><span class="sxs-lookup"><span data-stu-id="8b2b4-153">The client sends the token to the Application Proxy service, which retrieves the user principal name (UPN) and security principal name (SPN) from the token, then directs the request to the Application Proxy connector.</span></span>
4. <span data-ttu-id="8b2b4-154">如果您已設定單一登入，則連接器會代表使用者執行其他任何所需的驗證。</span><span class="sxs-lookup"><span data-stu-id="8b2b4-154">If you have configured single sign-on, the connector performs any additional authentication required on behalf of the user.</span></span>
5. <span data-ttu-id="8b2b4-155">連接器會將要求傳送至內部部署應用程式。</span><span class="sxs-lookup"><span data-stu-id="8b2b4-155">The connector sends the request to the on-premises application.</span></span>  
6. <span data-ttu-id="8b2b4-156">回應會透過應用程式 Proxy 服務與連接器傳送給使用者。</span><span class="sxs-lookup"><span data-stu-id="8b2b4-156">The response is sent through Application Proxy service and connector to the user.</span></span>

### <a name="single-sign-on"></a><span data-ttu-id="8b2b4-157">單一登入</span><span class="sxs-lookup"><span data-stu-id="8b2b4-157">Single sign-on</span></span>
<span data-ttu-id="8b2b4-158">Azure AD 應用程式 Proxy 會針對使用整合式 Windows 驗證 (IWA) 的應用程式或宣告感知應用程式提供單一登入 (SSO)。</span><span class="sxs-lookup"><span data-stu-id="8b2b4-158">Azure AD Application Proxy provides single sign-on (SSO) to applications that use Integrated Windows Authentication (IWA), or claims-aware applications.</span></span> <span data-ttu-id="8b2b4-159">如果您的應用程式使用 IWA，應用程式 Proxy 會模擬使用 Kerberos 限制委派的使用者來提供 SSO。</span><span class="sxs-lookup"><span data-stu-id="8b2b4-159">If your application uses IWA, Application Proxy impersonates the user using Kerberos Constrained Delegation to provide SSO.</span></span> <span data-ttu-id="8b2b4-160">如果您具有信任 Azure Active Directory 的宣告感知應用程式，則可以使用 SSO，因為使用者已由 Azure AD 驗證。</span><span class="sxs-lookup"><span data-stu-id="8b2b4-160">If you have a claims-aware application that trusts Azure Active Directory, SSO works because the user was already authenticated by Azure AD.</span></span>

<span data-ttu-id="8b2b4-161">如需有關 Kerberos 的詳細資訊，請參閱[有關 Kerberos 限制委派 (KCD) 您想要知道的一切](https://blogs.technet.microsoft.com/applicationproxyblog/2015/09/21/all-you-want-to-know-about-kerberos-constrained-delegation-kcd)。</span><span class="sxs-lookup"><span data-stu-id="8b2b4-161">For more information about Kerberos, see [All you want to know about Kerberos Constrained Delegation (KCD)](https://blogs.technet.microsoft.com/applicationproxyblog/2015/09/21/all-you-want-to-know-about-kerberos-constrained-delegation-kcd).</span></span>

### <a name="managing-apps"></a><span data-ttu-id="8b2b4-162">管理應用程式</span><span class="sxs-lookup"><span data-stu-id="8b2b4-162">Managing apps</span></span>
<span data-ttu-id="8b2b4-163">應用程式隨同 Application Proxy 發佈後，即可管理該應用程式，如同管理 Azure 入口網站中的其他任何企業應用程式一般。</span><span class="sxs-lookup"><span data-stu-id="8b2b4-163">One your app is published with Application Proxy, you can manage it like any other enterprise app in the Azure portal.</span></span> <span data-ttu-id="8b2b4-164">您可以使用 Azure Active Directory 安全性功能，例如條件式存取和雙步驟驗證、控制使用者權限，以及自訂您應用程式的商標。</span><span class="sxs-lookup"><span data-stu-id="8b2b4-164">You can use Azure Active Directory security features like conditional access and two-step verification, control user permissions, and customize the branding for your app.</span></span> 

## <a name="get-started"></a><span data-ttu-id="8b2b4-165">開始使用</span><span class="sxs-lookup"><span data-stu-id="8b2b4-165">Get started</span></span>

<span data-ttu-id="8b2b4-166">設定 Application Proxy 之前，確定您有支援的 [Azure Active Directory 版本](https://azure.microsoft.com/pricing/details/active-directory/)，以及您是全域管理員的 Azure AD 目錄。</span><span class="sxs-lookup"><span data-stu-id="8b2b4-166">Before you configure Application Proxy, make sure you have a supported [Azure Active Directory edition](https://azure.microsoft.com/pricing/details/active-directory/) and an Azure AD directory for which you are a global administrator.</span></span>

<span data-ttu-id="8b2b4-167">開始使用 Application Proxy 有兩個步驟：</span><span class="sxs-lookup"><span data-stu-id="8b2b4-167">Get started with Application Proxy in two steps:</span></span>

1. <span data-ttu-id="8b2b4-168">[啟用應用程式 Proxy 並設定連接器](active-directory-application-proxy-enable.md)。</span><span class="sxs-lookup"><span data-stu-id="8b2b4-168">[Enable Application Proxy and configure the connector](active-directory-application-proxy-enable.md).</span></span>    
2. <span data-ttu-id="8b2b4-169">[發佈應用程式](active-directory-application-proxy-publish.md) ：使用快速且簡單的精靈發佈內部部署應用程式並提供遠端存取。</span><span class="sxs-lookup"><span data-stu-id="8b2b4-169">[Publish applications](active-directory-application-proxy-publish.md) - use the quick and easy wizard to get your on-premises apps published and accessible remotely.</span></span>

## <a name="whats-next"></a><span data-ttu-id="8b2b4-170">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8b2b4-170">What's next?</span></span>
<span data-ttu-id="8b2b4-171">您發佈第一個應用程式後，應用程式 Proxy 還有其他更多用途：</span><span class="sxs-lookup"><span data-stu-id="8b2b4-171">Once you publish your first app, there's a lot more you can do with Application Proxy:</span></span>

* [<span data-ttu-id="8b2b4-172">啟用單一登入</span><span class="sxs-lookup"><span data-stu-id="8b2b4-172">Enable single-sign on</span></span>](active-directory-application-proxy-sso-using-kcd.md)
* [<span data-ttu-id="8b2b4-173">使用您自己的網域名稱發行應用程式</span><span class="sxs-lookup"><span data-stu-id="8b2b4-173">Publish applications using your own domain name</span></span>](active-directory-application-proxy-custom-domains.md)
* [<span data-ttu-id="8b2b4-174">了解 Azure AD 應用程式 Proxy 連接器</span><span class="sxs-lookup"><span data-stu-id="8b2b4-174">Learn about Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)
* [<span data-ttu-id="8b2b4-175">使用現有的內部部署 Proxy 伺服器</span><span class="sxs-lookup"><span data-stu-id="8b2b4-175">Working with existing on-premises Proxy servers</span></span>](application-proxy-working-with-proxy-servers.md) 
* [<span data-ttu-id="8b2b4-176">設定自訂首頁</span><span class="sxs-lookup"><span data-stu-id="8b2b4-176">Set a custom home page</span></span>](application-proxy-office365-app-launcher.md)

<span data-ttu-id="8b2b4-177">如需最新消息，請查閱 [應用程式 Proxy 部落格](http://blogs.technet.com/b/applicationproxyblog/)</span><span class="sxs-lookup"><span data-stu-id="8b2b4-177">For the latest news and updates, check out the [Application Proxy blog](http://blogs.technet.com/b/applicationproxyblog/)</span></span>

