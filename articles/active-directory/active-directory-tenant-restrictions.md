---
title: "透過限制租用戶管理對雲端應用程式的存取 | Microsoft Docs"
description: "如何使用「租用戶限制」以根據使用者的 Azure AD 租用戶來管理可存取應用程式的使用者。"
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: kgremban
ms.openlocfilehash: 7288f8fa173f8018570cd17aa7274f56a4eead41
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-tenant-restrictions-to-manage-access-to-saas-cloud-applications"></a><span data-ttu-id="b6c47-103">使用租用戶限制來管理對 SaaS 雲端應用程式的存取</span><span class="sxs-lookup"><span data-stu-id="b6c47-103">Use Tenant Restrictions to manage access to SaaS cloud applications</span></span>

<span data-ttu-id="b6c47-104">注重安全性的大型組織想要移到 Office 365 之類的雲端服務，但需要確知其使用者只能存取獲得核准的資源。</span><span class="sxs-lookup"><span data-stu-id="b6c47-104">Large organizations that emphasize security want to move to cloud services like Office 365, but need to know that their users only can access approved resources.</span></span> <span data-ttu-id="b6c47-105">傳統上，當公司想要管理存取時，會限制網域名稱或 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="b6c47-105">Traditionally, companies restrict domain names or IP addresses when they want to manage access.</span></span> <span data-ttu-id="b6c47-106">在 SaaS 應用程式裝載於公用雲端而在共用網域名稱 (例如 outlook.office.com 和 login.microsoftonline.com) 上執行的環境中，這個方法行不通。</span><span class="sxs-lookup"><span data-stu-id="b6c47-106">This approach fails in a world where SaaS apps are hosted in a public cloud, running on shared domain names like outlook.office.com and login.microsoftonline.com.</span></span> <span data-ttu-id="b6c47-107">封鎖這些位址會讓使用者無法存取整個網路上的 Outlook，而不僅是限制他們只能存取已核准的身分識別和資源。</span><span class="sxs-lookup"><span data-stu-id="b6c47-107">Blocking these addresses would keep users from accessing Outlook on the web entirely, instead of merely restricting them to approved identities and resources.</span></span>

<span data-ttu-id="b6c47-108">Azure Active Directory 對這項挑戰所提出的解決方案是一個稱為「租用戶限制」的功能。</span><span class="sxs-lookup"><span data-stu-id="b6c47-108">Azure Active Directory's solution to this challenge is a feature called Tenant Restrictions.</span></span> <span data-ttu-id="b6c47-109">「租用戶限制」可讓組織根據應用程式用於單一登入的 Azure AD 租用戶來控制對 SaaS 雲端應用程式的存取。</span><span class="sxs-lookup"><span data-stu-id="b6c47-109">Tenant Restrictions enables organizations to control access to SaaS cloud applications, based on the Azure AD tenant the applications use for single sign-on.</span></span> <span data-ttu-id="b6c47-110">例如，您可能想要允許使用者存取您組織的 Office 365 應用程式，但又防止他們存取其他組織的這些相同應用程式執行個體。</span><span class="sxs-lookup"><span data-stu-id="b6c47-110">For example, you may want to allow access to your organization’s Office 365 applications, while preventing access to other organizations’ instances of these same applications.</span></span>  

<span data-ttu-id="b6c47-111">「租用戶限制」可讓組織指定允許其使用者存取的租用戶清單。</span><span class="sxs-lookup"><span data-stu-id="b6c47-111">Tenant Restrictions gives organizations the ability to specify the list of tenants that their users are permitted to access.</span></span> <span data-ttu-id="b6c47-112">Azure AD 接著便可只授與對這些已允許之租用戶的存取權。</span><span class="sxs-lookup"><span data-stu-id="b6c47-112">Azure AD then only grants access to these permitted tenants.</span></span>

<span data-ttu-id="b6c47-113">本文將焦點放在 Office 365 的「租用戶限制」，但此功能應該適用於使用新式驗證通訊協定搭配 Azure AD 來進行單一登入的所有 SaaS 雲端應用程式。</span><span class="sxs-lookup"><span data-stu-id="b6c47-113">This article focuses on Tenant Restrictions for Office 365, but the feature should work with any SaaS cloud app that uses modern authentication protocols with Azure AD for single sign-on.</span></span> <span data-ttu-id="b6c47-114">如果您使用 SaaS 應用程式搭配與 Office 365 所用租用戶不同的 Azure AD 租用戶，請務必核准所有必要的租用戶。</span><span class="sxs-lookup"><span data-stu-id="b6c47-114">If you use SaaS apps with a different Azure AD tenant from the tenant used by Office 365, make sure that all required tenants are permitted.</span></span> <span data-ttu-id="b6c47-115">如需有關 SaaS 雲端應用程式的詳細資訊，請參閱 [Active Directory Marketplace](https://azure.microsoft.com/en-us/marketplace/active-directory/)。</span><span class="sxs-lookup"><span data-stu-id="b6c47-115">For more information about SaaS cloud apps, see the [Active Directory Marketplace](https://azure.microsoft.com/en-us/marketplace/active-directory/).</span></span>

## <a name="how-it-works"></a><span data-ttu-id="b6c47-116">運作方式</span><span class="sxs-lookup"><span data-stu-id="b6c47-116">How it works</span></span>

<span data-ttu-id="b6c47-117">整體解決方案包含下列元件：</span><span class="sxs-lookup"><span data-stu-id="b6c47-117">The overall solution comprises the following components:</span></span> 

1. <span data-ttu-id="b6c47-118">**Azure AD** – 如果有 `Restrict-Access-To-Tenants: <permitted tenant list>` 存在，Azure AD 便只會針對已允許的租用戶發出安全性權杖。</span><span class="sxs-lookup"><span data-stu-id="b6c47-118">**Azure AD** – If the `Restrict-Access-To-Tenants: <permitted tenant list>` is present, Azure AD only issues security tokens for the permitted tenants.</span></span> 

2. <span data-ttu-id="b6c47-119">**內部部署 Proxy 伺服器基礎結構** – 一個能夠執行 SSL 檢查的 Proxy 裝置，經設定後能將包含已允許之租用戶清單的標頭插入目的地為 Azure AD 的流量中。</span><span class="sxs-lookup"><span data-stu-id="b6c47-119">**On-premises proxy server infrastructure** – a proxy device capable of SSL inspection, configured to insert the header containing the list of permitted tenants into traffic destined for Azure AD.</span></span> 

3. <span data-ttu-id="b6c47-120">**用戶端軟體** – 為了支援「租用戶限制」，用戶端軟體必須直接從 Azure AD 要求權杖，以便 Proxy 基礎結構能夠攔截流量。</span><span class="sxs-lookup"><span data-stu-id="b6c47-120">**Client software** – to support Tenant Restrictions, client software must request tokens directly from Azure AD, so that traffic can be intercepted by the proxy infrastructure.</span></span> <span data-ttu-id="b6c47-121">目前瀏覽器型 Office 365 應用程式和使用新式驗證 (例如 OAuth 2.0) 的 Office 用戶端都支援「租用戶限制」。</span><span class="sxs-lookup"><span data-stu-id="b6c47-121">Tenant Restrictions is currently supported by browser-based Office 365 applications and by Office clients when modern authentication (like OAuth 2.0) is used.</span></span> 

4. <span data-ttu-id="b6c47-122">**新式驗證** – 雲端服務必須使用新式驗證，才能使用「租用戶限制」並封鎖對所有非允許之租用戶的存取。</span><span class="sxs-lookup"><span data-stu-id="b6c47-122">**Modern Authentication** – cloud services must use modern authentication to use Tenant Restrictions and block access to all non-permitted tenants.</span></span> <span data-ttu-id="b6c47-123">必須將 Office 365 雲端服務設定為預設使用新式驗證通訊協定。</span><span class="sxs-lookup"><span data-stu-id="b6c47-123">Office 365 cloud services must be configured to use modern authentication protocols by default.</span></span> <span data-ttu-id="b6c47-124">如需有關 Office 365 對新式驗證之支援的最新資訊，請參閱[更新的 Office 365 新式驗證 (英文)](https://blogs.office.com/2015/11/19/updated-office-365-modern-authentication-public-preview/)。</span><span class="sxs-lookup"><span data-stu-id="b6c47-124">For the latest information on Office 365 support for modern authentication, read [Updated Office 365 modern authentication](https://blogs.office.com/2015/11/19/updated-office-365-modern-authentication-public-preview/).</span></span>

<span data-ttu-id="b6c47-125">下圖說明概略的流量流程。</span><span class="sxs-lookup"><span data-stu-id="b6c47-125">The following diagram illustrates the high-level traffic flow.</span></span> <span data-ttu-id="b6c47-126">只有傳送到 Azure AD 的流量才需要進行 SSL 檢查，傳送到 Office 365 雲端服務的流量則不需要。</span><span class="sxs-lookup"><span data-stu-id="b6c47-126">SSL inspection is only required on traffic to Azure AD, not to the Office 365 cloud services.</span></span> <span data-ttu-id="b6c47-127">這項區別很重要，因為傳送到 Azure AD 以進行驗證的流量通常比傳送到 SaaS 應用程式 (例如 Exchange Online 和 SharePoint Online) 的流量少很多。</span><span class="sxs-lookup"><span data-stu-id="b6c47-127">This distinction is important because the traffic volume for authentication to Azure AD is typically much lower than traffic volume to SaaS applications like Exchange Online and SharePoint Online.</span></span>

![租用戶限制流量流程 - 圖表](./media/active-directory-tenant-restrictions/traffic-flow.png)

## <a name="set-up-tenant-restrictions"></a><span data-ttu-id="b6c47-129">設定租用戶限制</span><span class="sxs-lookup"><span data-stu-id="b6c47-129">Set up Tenant Restrictions</span></span>

<span data-ttu-id="b6c47-130">開始使用「租用戶限制」的步驟有兩個。</span><span class="sxs-lookup"><span data-stu-id="b6c47-130">There are two steps to get started with Tenant Restrictions.</span></span> <span data-ttu-id="b6c47-131">第一個步驟是確定您的用戶端可以連線到正確的位址。</span><span class="sxs-lookup"><span data-stu-id="b6c47-131">The first step is to make sure that your clients can connect to the right addresses.</span></span> <span data-ttu-id="b6c47-132">第二個步驟是設定您的 Proxy 基礎結構。</span><span class="sxs-lookup"><span data-stu-id="b6c47-132">The second is to configure your proxy infrastructure.</span></span>

### <a name="urls-and-ip-addresses"></a><span data-ttu-id="b6c47-133">URL 和 IP 位址</span><span class="sxs-lookup"><span data-stu-id="b6c47-133">URLs and IP addresses</span></span>

<span data-ttu-id="b6c47-134">若要使用「租用戶限制」，您的用戶端必須要能夠連線到下列 Azure AD URL 來進行驗證：login.microsoftonline.com、login.microsoft.com 及 login.windows.net。</span><span class="sxs-lookup"><span data-stu-id="b6c47-134">To use Tenant Restrictions, your clients must be able to connect to the following Azure AD URLs to authenticate: login.microsoftonline.com, login.microsoft.com, and login.windows.net.</span></span> <span data-ttu-id="b6c47-135">此外，若要存取 Office 365，您的用戶端必須也要能夠連線到 [Office 365 URL 與 IP 位址範圍](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2)中所定義的 FQDN/URL 和 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="b6c47-135">Additionally, to access Office 365, your clients must also be able to connect to the FQDNs/URLs and IP addresses defined in [Office 365 URLs and IP address ranges](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2).</span></span> 

### <a name="proxy-configuration-and-requirements"></a><span data-ttu-id="b6c47-136">Proxy 組態和需求</span><span class="sxs-lookup"><span data-stu-id="b6c47-136">Proxy configuration and requirements</span></span>

<span data-ttu-id="b6c47-137">以下是透過 Proxy 基礎結構啟用「租用戶限制」的必要組態。</span><span class="sxs-lookup"><span data-stu-id="b6c47-137">The following configuration is required to enable Tenant Restrictions through your proxy infrastructure.</span></span> <span data-ttu-id="b6c47-138">本指導方針是通用的，因此如需了解特定的實作步驟，您應該參考您 Proxy 廠商的文件。</span><span class="sxs-lookup"><span data-stu-id="b6c47-138">This guidance is generic, so you should refer to your proxy vendor’s documentation for specific implementation steps.</span></span>

#### <a name="prerequisites"></a><span data-ttu-id="b6c47-139">必要條件</span><span class="sxs-lookup"><span data-stu-id="b6c47-139">Prerequisites</span></span>

- <span data-ttu-id="b6c47-140">Proxy 必須要能夠執行 SSL 攔截、HTTP 標頭插入，以及使用 FQDN/URL 來篩選目的地。</span><span class="sxs-lookup"><span data-stu-id="b6c47-140">The proxy must be able to perform SSL interception, HTTP header insertion, and filter destinations using FQDNs/URLs.</span></span> 

- <span data-ttu-id="b6c47-141">用戶端必須信任 Proxy 針對 SSL 通訊所出示的憑證鏈結。</span><span class="sxs-lookup"><span data-stu-id="b6c47-141">Clients must trust the certificate chain presented by the proxy for SSL communications.</span></span> <span data-ttu-id="b6c47-142">例如，如果使用來自內部 PKI 的憑證，就必須信任內部發行的根憑證授權單位憑證。</span><span class="sxs-lookup"><span data-stu-id="b6c47-142">For example, if certificates from an internal PKI are used, the internal issuing root certificate authority certificate must be trusted.</span></span>

- <span data-ttu-id="b6c47-143">Office 365 訂用帳戶中已包含此功能，但如果您想要使用「租用戶限制」來控制對其他 SaaS 應用程式的存取，則需要 Azure AD「進階 1」授權。</span><span class="sxs-lookup"><span data-stu-id="b6c47-143">This feature is included in Office 365 subscriptions, but if you want to use Tenant Restrictions to control access to other SaaS apps then Azure AD Premium 1 licenses are required.</span></span>

#### <a name="configuration"></a><span data-ttu-id="b6c47-144">組態</span><span class="sxs-lookup"><span data-stu-id="b6c47-144">Configuration</span></span>

<span data-ttu-id="b6c47-145">針對每個傳送到 login.microsoftonline.com、login.microsoft.com 及 login.windows.net 的連入要求，請插入兩個 HTTP 標頭：*Restrict-Access-To-Tenants* 和 *Restrict-Access-Context*。</span><span class="sxs-lookup"><span data-stu-id="b6c47-145">For each incoming request to login.microsoftonline.com, login.microsoft.com, and login.windows.net, insert two HTTP headers: *Restrict-Access-To-Tenants* and *Restrict-Access-Context*.</span></span>

<span data-ttu-id="b6c47-146">這些標頭應該包含下列元素︰</span><span class="sxs-lookup"><span data-stu-id="b6c47-146">The headers should include the following elements:</span></span> 
- <span data-ttu-id="b6c47-147">就 *Restrict-Access-To-Tenants* 而言，需包含 \<permitted tenant list\> 的值，這是您想要允許使用者存取的租用戶清單 (以逗號分隔)。</span><span class="sxs-lookup"><span data-stu-id="b6c47-147">For *Restrict-Access-To-Tenants*, a value of \<permitted tenant list\>, which is a comma-separated list of tenants you want to allow users to access.</span></span> <span data-ttu-id="b6c47-148">與租用戶一起註冊的任何網域都可用來在此清單中識別該租用戶。</span><span class="sxs-lookup"><span data-stu-id="b6c47-148">Any domain that is registered with a tenant can be used to identify the tenant in this list.</span></span> <span data-ttu-id="b6c47-149">例如，若要允許存取 Contoso 和 Fabrikam 租用戶，名稱/值組看起來會像這樣：`Restrict-Access-To-Tenants: contoso.onmicrosoft.com,fabrikam.onmicrosoft.com`</span><span class="sxs-lookup"><span data-stu-id="b6c47-149">For example, to permit access to both Contoso and Fabrikam tenants, the name/value pair looks like:  `Restrict-Access-To-Tenants: contoso.onmicrosoft.com,fabrikam.onmicrosoft.com`</span></span> 
- <span data-ttu-id="b6c47-150">就 *Restrict-Access-Context* 而言，需包含單一目錄識別碼的值，用來宣告設定「租用戶限制」的是哪一個租用戶。</span><span class="sxs-lookup"><span data-stu-id="b6c47-150">For *Restrict-Access-Context*, a value of a single directory ID, declaring which tenant is setting the Tenant Restrictions.</span></span> <span data-ttu-id="b6c47-151">例如，若要宣告 Contoso 是設定「租用戶限制」原則的租用戶，名稱/值組看起來會像這樣：`Restrict-Access-Context: 456ff232-35l2-5h23-b3b3-3236w0826f3d`</span><span class="sxs-lookup"><span data-stu-id="b6c47-151">For example, to declare Contoso as the tenant that set the Tenant Restrictions policy, the name/value pair looks like: `Restrict-Access-Context: 456ff232-35l2-5h23-b3b3-3236w0826f3d`</span></span>  

> [!TIP]
> <span data-ttu-id="b6c47-152">您可以在 [Azure 入口網站](https://portal.azure.com)中找到您的目錄識別碼。</span><span class="sxs-lookup"><span data-stu-id="b6c47-152">You can find your directory ID in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="b6c47-153">請以系統管理員身分登入，選取 [Azure Active Directory]，然後選取 [屬性]。</span><span class="sxs-lookup"><span data-stu-id="b6c47-153">Sign in as an administrator, select **Azure Active Directory**, then select **Properties**.</span></span>

<span data-ttu-id="b6c47-154">若要防止使用者插入自己的含有非核准租用戶的 HTTP 標頭，Proxy 就必須在連入要求中已經有 Restrict-Access-To-Tenants 標頭時取代此標頭。</span><span class="sxs-lookup"><span data-stu-id="b6c47-154">To prevent users from inserting their own HTTP header with non-approved tenants, the proxy needs to replace the Restrict-Access-To-Tenants header if it is already present in the incoming request.</span></span> 

<span data-ttu-id="b6c47-155">必須強制用戶端針對所有傳送到 login.microsoftonline.com、login.microsoft.com 及 login.windows.net 的要求使用 Proxy。</span><span class="sxs-lookup"><span data-stu-id="b6c47-155">Clients must be forced to use the proxy for all requests to login.microsoftonline.com, login.microsoft.com, and login.windows.net.</span></span> <span data-ttu-id="b6c47-156">例如，如果使用 PAC 檔案來指示用戶端使用 Proxy，使用者應該要不能夠編輯或停用 PAC 檔案。</span><span class="sxs-lookup"><span data-stu-id="b6c47-156">For example, if PAC files are used to direct clients to use the proxy, end users should not be able to edit or disable the PAC files.</span></span>

## <a name="the-user-experience"></a><span data-ttu-id="b6c47-157">使用者體驗</span><span class="sxs-lookup"><span data-stu-id="b6c47-157">The user experience</span></span>

<span data-ttu-id="b6c47-158">本節說明使用者和系統管理員的體驗。</span><span class="sxs-lookup"><span data-stu-id="b6c47-158">This section shows the experience for both end users and admins.</span></span>

### <a name="end-user-experience"></a><span data-ttu-id="b6c47-159">使用者體驗</span><span class="sxs-lookup"><span data-stu-id="b6c47-159">End-user experience</span></span>

<span data-ttu-id="b6c47-160">範例使用者位於 Contoso 網路上，但正在嘗試存取 Fabrikam 的共用 SaaS 應用程式執行個體 (例如 Outlook Online)。</span><span class="sxs-lookup"><span data-stu-id="b6c47-160">An example user is on the Contoso network, but is trying to access the Fabrikam instance of a shared SaaS application like Outlook online.</span></span> <span data-ttu-id="b6c47-161">如果 Contoso 不是該執行個體所允許的租用戶，使用者就會看到以下頁面：</span><span class="sxs-lookup"><span data-stu-id="b6c47-161">If Contoso is a non-permitted tenant for that instance, the user sees the following page:</span></span>

![針對非允許之租用戶中使用者的拒絕存取頁面](./media/active-directory-tenant-restrictions/end-user-denied.png)

### <a name="admin-experience"></a><span data-ttu-id="b6c47-163">管理員體驗</span><span class="sxs-lookup"><span data-stu-id="b6c47-163">Admin experience</span></span>

<span data-ttu-id="b6c47-164">雖然設定「租用戶限制」時是在公司 Proxy 基礎結構上完成設定，但系統管理員可以直接在 Azure 入口網站中存取「租用戶限制」報告。</span><span class="sxs-lookup"><span data-stu-id="b6c47-164">While configuration of Tenant Restrictions is done on the corporate proxy infrastructure, admins can access the Tenant Restrictions reports in the Azure portal directly.</span></span> <span data-ttu-id="b6c47-165">若要檢視這些報告，請移至 Azure Active Directory 的 [概觀] 頁面，然後查看 [其他功能] 底下。</span><span class="sxs-lookup"><span data-stu-id="b6c47-165">To view the reports, go to the Azure Active Directory Overview page, then look under ‘Other capabilities’.</span></span>

<span data-ttu-id="b6c47-166">租用戶如果被指定為 Restricted-Access-Context 租用戶，其系統管理員便可以使用此報告來查看所有因「租用戶限制」原則而遭封鎖的登入，包括所使用的身分識別及租用戶目錄識別碼。</span><span class="sxs-lookup"><span data-stu-id="b6c47-166">The admin for the tenant specified as the Restricted-Access-Context tenant can use this report to see all sign-ins blocked because of the Tenant Restrictions policy, including the identity used and the target directory ID.</span></span>

![使用 Azure 入口網站來檢視受限制的登入嘗試](./media/active-directory-tenant-restrictions/portal-report.png)

<span data-ttu-id="b6c47-168">與 Azure 入口網站中的其他報告相同，您可以使用篩選來指定報告的範圍。</span><span class="sxs-lookup"><span data-stu-id="b6c47-168">Like other reports in the Azure portal, you can use filters to specify the scope of your report.</span></span> <span data-ttu-id="b6c47-169">您可以依據特定使用者、應用程式、用戶端或時間間隔進行篩選。</span><span class="sxs-lookup"><span data-stu-id="b6c47-169">You can filter on a specific user, application, client, or time interval.</span></span>

## <a name="office-365-support"></a><span data-ttu-id="b6c47-170">Office 365 支援</span><span class="sxs-lookup"><span data-stu-id="b6c47-170">Office 365 support</span></span>

<span data-ttu-id="b6c47-171">Office 365 應用程式必須符合兩項準則，才能完全支援「租用戶限制」：</span><span class="sxs-lookup"><span data-stu-id="b6c47-171">Office 365 applications must meet two criteria to fully support Tenant Restrictions:</span></span>

1. <span data-ttu-id="b6c47-172">所使用的用戶端支援新式驗證</span><span class="sxs-lookup"><span data-stu-id="b6c47-172">The client used supports modern authentication</span></span>
2. <span data-ttu-id="b6c47-173">啟用新式驗證作為雲端服務的預設驗證通訊協定。</span><span class="sxs-lookup"><span data-stu-id="b6c47-173">Modern authentication is enabled as the default authentication protocol for the cloud service.</span></span>

<span data-ttu-id="b6c47-174">如需有關哪些 Office 用戶端目前支援新式驗證的最新資訊，請參閱[更新的 Office 365 新式驗證 (英文)](https://blogs.office.com/2015/11/19/updated-office-365-modern-authentication-public-preview/)。</span><span class="sxs-lookup"><span data-stu-id="b6c47-174">Refer to [Updated Office 365 modern authentication](https://blogs.office.com/2015/11/19/updated-office-365-modern-authentication-public-preview/) for the latest information on which Office clients currently support modern authentication.</span></span> <span data-ttu-id="b6c47-175">該頁面也包含在特定 Exchange Online 和「商務用 Skype Online」租用戶上啟用新式驗證的指示連結。</span><span class="sxs-lookup"><span data-stu-id="b6c47-175">That page also includes links to instructions for enabling modern authentication on specific Exchange Online and Skype for Business Online tenants.</span></span> <span data-ttu-id="b6c47-176">SharePoint Online 中已經預設啟用新式驗證。</span><span class="sxs-lookup"><span data-stu-id="b6c47-176">Modern authentication is already enabled by default in SharePoint Online.</span></span>

<span data-ttu-id="b6c47-177">目前 Office 365 瀏覽器型應用程式 (Office Portal、Yammer、SharePoint 網站、Outlook 網頁版等) 都支援「租用戶限制」。</span><span class="sxs-lookup"><span data-stu-id="b6c47-177">Tenant Restrictions is currently supported by Office 365 browser-based applications (the Office Portal, Yammer, SharePoint sites, Outlook on the Web, etc.).</span></span> <span data-ttu-id="b6c47-178">針對豐富型用戶端 (Outlook、商務用 Skype、Word、Excel、PowerPoint 等)，只有在使用新式驗證的情況下，才能強制執行「租用戶限制」。</span><span class="sxs-lookup"><span data-stu-id="b6c47-178">For thick clients (Outlook, Skype for Business, Word, Excel, PowerPoint, etc.) Tenant Restrictions can only be enforced when modern authentication is used.</span></span>  

<span data-ttu-id="b6c47-179">支援新式驗證的 Outlook 和「商務用 Skype」用戶端仍然能夠針對未啟用新式驗證的租用戶使用傳統通訊協定，有效地略過「租用戶限制」。</span><span class="sxs-lookup"><span data-stu-id="b6c47-179">Outlook and Skype for Business clients that support modern authentication are still able to use legacy protocols against tenants where modern authentication is not enabled, effectively bypassing Tenant Restrictions.</span></span> <span data-ttu-id="b6c47-180">針對 Windows 上的 Outlook，客戶可以選擇實作可防止使用者將非已核准郵件帳戶新增至其設定檔的限制。</span><span class="sxs-lookup"><span data-stu-id="b6c47-180">For Outlook on Windows, customers may choose to implement restrictions preventing end users from adding non-approved mail accounts to their profiles.</span></span> <span data-ttu-id="b6c47-181">例如，請參閱[防止新增非預設 Exchange 帳戶](http://gpsearch.azurewebsites.net/default.aspx?ref=1)群組原則設定。</span><span class="sxs-lookup"><span data-stu-id="b6c47-181">For example, see the [Prevent adding non-default Exchange accounts](http://gpsearch.azurewebsites.net/default.aspx?ref=1) group policy setting.</span></span> <span data-ttu-id="b6c47-182">對於非 Windows 平台上的 Outlook 與所有平台上的商務用 Skype，目前尚未完整支援租用戶限制。</span><span class="sxs-lookup"><span data-stu-id="b6c47-182">For Outlook on non-Windows platforms, and for Skype for Business on all platforms, full support for Tenant Restrictions is not currently available.</span></span>

## <a name="testing"></a><span data-ttu-id="b6c47-183">測試</span><span class="sxs-lookup"><span data-stu-id="b6c47-183">Testing</span></span>

<span data-ttu-id="b6c47-184">如果您想要先試用「租用戶限制」，然後才為整個組織實作此功能，則有兩個選項：運用使用 Fiddler 這類工具的主機型方法，或是分段推出 Proxy 設定。</span><span class="sxs-lookup"><span data-stu-id="b6c47-184">If you want to try out Tenant Restrictions before implementing it for your whole organization, there are two options: a host-based approach using a tool like Fiddler, or a staged rollout of proxy settings.</span></span>

### <a name="fiddler-for-a-host-based-approach"></a><span data-ttu-id="b6c47-185">適用於主機型方法的 Fiddler</span><span class="sxs-lookup"><span data-stu-id="b6c47-185">Fiddler for a host-based approach</span></span>

<span data-ttu-id="b6c47-186">Fiddler 是一個免費的 Web 偵錯 Proxy，可用來擷取和修改 HTTP/HTTPS 流量，包括插入 HTTP 標頭。</span><span class="sxs-lookup"><span data-stu-id="b6c47-186">Fiddler is a free web debugging proxy that can be used to capture and modify HTTP/HTTPS traffic, including inserting HTTP headers.</span></span> <span data-ttu-id="b6c47-187">若要設定 Fiddler 以測試「租用戶限制」，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="b6c47-187">To configure Fiddler to test Tenant Restrictions, perform the following steps:</span></span>

1.  <span data-ttu-id="b6c47-188">[下載並安裝 Fiddler](http://www.telerik.com/fiddler)。</span><span class="sxs-lookup"><span data-stu-id="b6c47-188">[Download and install Fiddler](http://www.telerik.com/fiddler).</span></span>
2.  <span data-ttu-id="b6c47-189">依照 [Fiddler 的說明文件 (英文)](http://docs.telerik.com/fiddler/Configure-Fiddler/Tasks/DecryptHTTPS) 操作，設定 Fiddler 以將 HTTPS 流量解密。</span><span class="sxs-lookup"><span data-stu-id="b6c47-189">Configure Fiddler to decrypt HTTPS traffic, per [Fiddler’s help documentation](http://docs.telerik.com/fiddler/Configure-Fiddler/Tasks/DecryptHTTPS).</span></span>
3.  <span data-ttu-id="b6c47-190">設定 Fiddler 以使用自訂規則來插入 *Restrict-Access-To-Tenants* 和 *Restrict-Access-Context* 標頭：</span><span class="sxs-lookup"><span data-stu-id="b6c47-190">Configure Fiddler to insert the *Restrict-Access-To-Tenants* and *Restrict-Access-Context* headers using custom rules:</span></span>
  1. <span data-ttu-id="b6c47-191">在「Fiddler Web 偵錯工具」中，選取 [Rules] \(規則) 功能表，然後選取 [Customize Rules] \(自訂規則)</span><span class="sxs-lookup"><span data-stu-id="b6c47-191">In the Fiddler Web Debugger tool, select the **Rules** menu and select **Customize Rules…**</span></span> <span data-ttu-id="b6c47-192">以開啟 CustomRules 檔案。</span><span class="sxs-lookup"><span data-stu-id="b6c47-192">to open the CustomRules file.</span></span>
  2. <span data-ttu-id="b6c47-193">在 *OnBeforeRequest* 函式開頭新增下列幾行。</span><span class="sxs-lookup"><span data-stu-id="b6c47-193">Add the following lines at the beginning of the *OnBeforeRequest* function.</span></span> <span data-ttu-id="b6c47-194">使用與您租用戶一起註冊的網域來取代 \<tenant domain\>，例如 contoso.onmicrosoft.com。</span><span class="sxs-lookup"><span data-stu-id="b6c47-194">Replace \<tenant domain\> with a domain registered with your tenant, for example, contoso.onmicrosoft.com.</span></span> <span data-ttu-id="b6c47-195">使用您租用戶的 Azure AD GUID 識別碼來取代 \<directory ID\>。</span><span class="sxs-lookup"><span data-stu-id="b6c47-195">Replace \<directory ID\> with your tenant's Azure AD GUID identifier.</span></span>

  ```
  if (oSession.HostnameIs("login.microsoftonline.com") || oSession.HostnameIs("login.microsoft.com") || oSession.HostnameIs("login.windows.net")){      oSession.oRequest["Restrict-Access-To-Tenants"] = "<tenant domain>";      oSession.oRequest["Restrict-Access-Context"] = "<directory ID>";}
  ```

  <span data-ttu-id="b6c47-196">如果您需要允許多個租用戶，請使用逗號來分隔租用戶名稱。</span><span class="sxs-lookup"><span data-stu-id="b6c47-196">If you need to allow multiple tenants, use a comma to separate the tenant names.</span></span> <span data-ttu-id="b6c47-197">例如：</span><span class="sxs-lookup"><span data-stu-id="b6c47-197">For example:</span></span>

  ```
  oSession.oRequest["Restrict-Access-To-Tenants"] = "contoso.onmicrosoft.com,fabrikam.onmicrosoft.com";
  ```

4. <span data-ttu-id="b6c47-198">儲存並關閉 CustomRules 檔案。</span><span class="sxs-lookup"><span data-stu-id="b6c47-198">Save and close the CustomRules file.</span></span>

<span data-ttu-id="b6c47-199">設定 Fiddler 之後，您可以移至 [File] \(檔案) 功能表並選取 [Capture Traffic] \(擷取流量)，來擷取流量。</span><span class="sxs-lookup"><span data-stu-id="b6c47-199">After you configure Fiddler, you can capture traffic by going to the **File** menu and selecting **Capture Traffic**.</span></span>

### <a name="staged-rollout-of-proxy-settings"></a><span data-ttu-id="b6c47-200">分段推出 Proxy 設定</span><span class="sxs-lookup"><span data-stu-id="b6c47-200">Staged rollout of proxy settings</span></span>

<span data-ttu-id="b6c47-201">視您 Proxy 基礎結構的功能而定，您可能可以向使用者分段推出設定。</span><span class="sxs-lookup"><span data-stu-id="b6c47-201">Depending on the capabilities of your proxy infrastructure, you may be able to stage the rollout of settings to your users.</span></span> <span data-ttu-id="b6c47-202">以下是一些可供考量的概略選項：</span><span class="sxs-lookup"><span data-stu-id="b6c47-202">Here are a couple high-level options for consideration:</span></span>

1.  <span data-ttu-id="b6c47-203">使用 PAC 檔案將測試使用者指向測試 Proxy 基礎結構，同時又讓一般使用者繼續使用生產環境 Proxy 基礎結構。</span><span class="sxs-lookup"><span data-stu-id="b6c47-203">Use PAC files to point test users to a test proxy infrastructure, while normal users continue to use the production proxy infrastructure.</span></span>
2.  <span data-ttu-id="b6c47-204">有些 Proxy 伺服器可以使用群組來支援不同的組態。</span><span class="sxs-lookup"><span data-stu-id="b6c47-204">Some proxy servers may support different configurations using groups.</span></span>

<span data-ttu-id="b6c47-205">如需具體的詳細資料，請參閱您的 Proxy 伺服器文件。</span><span class="sxs-lookup"><span data-stu-id="b6c47-205">Refer to your proxy server documentation for specific details.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b6c47-206">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b6c47-206">Next steps</span></span>

- <span data-ttu-id="b6c47-207">閱讀[更新的 Office 365 新式驗證 (英文)](https://blogs.office.com/2015/11/19/updated-office-365-modern-authentication-public-preview/)</span><span class="sxs-lookup"><span data-stu-id="b6c47-207">Read about [Updated Office 365 modern authentication](https://blogs.office.com/2015/11/19/updated-office-365-modern-authentication-public-preview/)</span></span>

- <span data-ttu-id="b6c47-208">檢閱 [Office 365 URL 與 IP 位址範圍](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2)</span><span class="sxs-lookup"><span data-stu-id="b6c47-208">Review the [Office 365 URLs and IP address ranges](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2)</span></span>
