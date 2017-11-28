---
title: "藉由限制租用戶-Azure aaaManage 存取 toocloud 應用程式 |Microsoft 文件"
description: "如何 toouse 租用戶限制 toomanage 哪些使用者可以存取應用程式會根據其 Azure AD 租用戶。"
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
ms.openlocfilehash: 6470fa217738b29104353ae17a2f53216f825c19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-tenant-restrictions-toomanage-access-toosaas-cloud-applications"></a><span data-ttu-id="5383b-103">使用租用戶限制 toomanage access tooSaaS 雲端應用程式</span><span class="sxs-lookup"><span data-stu-id="5383b-103">Use Tenant Restrictions toomanage access tooSaaS cloud applications</span></span>

<span data-ttu-id="5383b-104">強調安全性的大型組織想 toomove toocloud 服務，例如 Office 365，但是使用者只可以存取的需求 tooknow 核准資源。</span><span class="sxs-lookup"><span data-stu-id="5383b-104">Large organizations that emphasize security want toomove toocloud services like Office 365, but need tooknow that their users only can access approved resources.</span></span> <span data-ttu-id="5383b-105">傳統上，公司網域名稱或 IP 位址時限制他們想要 toomanage 存取。</span><span class="sxs-lookup"><span data-stu-id="5383b-105">Traditionally, companies restrict domain names or IP addresses when they want toomanage access.</span></span> <span data-ttu-id="5383b-106">在 SaaS 應用程式裝載於公用雲端而在共用網域名稱 (例如 outlook.office.com 和 login.microsoftonline.com) 上執行的環境中，這個方法行不通。封鎖這些位址，會讓使用者無法存取 hello 網站上的 Outlook 完全，而不只限制它們 tooapproved 身分識別和資源。</span><span class="sxs-lookup"><span data-stu-id="5383b-106">This approach fails in a world where SaaS apps are hosted in a public cloud, running on shared domain names like outlook.office.com and login.microsoftonline.com. Blocking these addresses would keep users from accessing Outlook on hello web entirely, instead of merely restricting them tooapproved identities and resources.</span></span>

<span data-ttu-id="5383b-107">Azure Active Directory 的方案 toothis 挑戰是名為租用戶限制的功能。</span><span class="sxs-lookup"><span data-stu-id="5383b-107">Azure Active Directory's solution toothis challenge is a feature called Tenant Restrictions.</span></span> <span data-ttu-id="5383b-108">租用戶限制可讓組織 toocontrol 存取 tooSaaS 雲端應用程式，根據 hello Azure AD 租用戶 hello 進行單一登入的應用程式使用。</span><span class="sxs-lookup"><span data-stu-id="5383b-108">Tenant Restrictions enables organizations toocontrol access tooSaaS cloud applications, based on hello Azure AD tenant hello applications use for single sign-on.</span></span> <span data-ttu-id="5383b-109">比方說，您可能想 tooallow 存取 tooyour 組織的 Office 365 應用程式，同時防止這些相同的應用程式存取 tooother 組織的執行個體。</span><span class="sxs-lookup"><span data-stu-id="5383b-109">For example, you may want tooallow access tooyour organization’s Office 365 applications, while preventing access tooother organizations’ instances of these same applications.</span></span>  

<span data-ttu-id="5383b-110">租用戶限制提供組織 hello 能力 toospecify hello 清單的使用者允許 tooaccess 租用戶。</span><span class="sxs-lookup"><span data-stu-id="5383b-110">Tenant Restrictions gives organizations hello ability toospecify hello list of tenants that their users are permitted tooaccess.</span></span> <span data-ttu-id="5383b-111">然後 azure AD 只授與存取 toothese 允許租用戶。</span><span class="sxs-lookup"><span data-stu-id="5383b-111">Azure AD then only grants access toothese permitted tenants.</span></span>

<span data-ttu-id="5383b-112">本文著重 for Office 365 租用戶的限制，但 hello 功能應搭配使用新式驗證通訊協定與 Azure AD 進行單一登入任何 SaaS 雲端應用程式。</span><span class="sxs-lookup"><span data-stu-id="5383b-112">This article focuses on Tenant Restrictions for Office 365, but hello feature should work with any SaaS cloud app that uses modern authentication protocols with Azure AD for single sign-on.</span></span> <span data-ttu-id="5383b-113">如果您使用的 SaaS 應用程式使用不同的 Azure AD 租用戶從 Office 365 所使用的 hello 租用戶，請確定所有必要的允許租用戶。</span><span class="sxs-lookup"><span data-stu-id="5383b-113">If you use SaaS apps with a different Azure AD tenant from hello tenant used by Office 365, make sure that all required tenants are permitted.</span></span> <span data-ttu-id="5383b-114">如需有關 SaaS 雲端應用程式的詳細資訊，請參閱 hello [Active Directory Marketplace](https://azure.microsoft.com/en-us/marketplace/active-directory/)。</span><span class="sxs-lookup"><span data-stu-id="5383b-114">For more information about SaaS cloud apps, see hello [Active Directory Marketplace](https://azure.microsoft.com/en-us/marketplace/active-directory/).</span></span>

## <a name="how-it-works"></a><span data-ttu-id="5383b-115">運作方式</span><span class="sxs-lookup"><span data-stu-id="5383b-115">How it works</span></span>

<span data-ttu-id="5383b-116">hello 整體解決方案包含下列元件的 hello:</span><span class="sxs-lookup"><span data-stu-id="5383b-116">hello overall solution comprises hello following components:</span></span> 

1. <span data-ttu-id="5383b-117">**Azure AD** – 如果 hello `Restrict-Access-To-Tenants: <permitted tenant list>` hello 問題安全性語彙基元允許租用戶僅存在，Azure AD。</span><span class="sxs-lookup"><span data-stu-id="5383b-117">**Azure AD** – If hello `Restrict-Access-To-Tenants: <permitted tenant list>` is present, Azure AD only issues security tokens for hello permitted tenants.</span></span> 

2. <span data-ttu-id="5383b-118">**在內部部署 proxy 伺服器基礎結構**– proxy 裝置能夠 SSL 檢查，設定的 tooinsert hello 標頭，其中包含的 hello 清單允許排入流量的 Azure AD 的租用戶。</span><span class="sxs-lookup"><span data-stu-id="5383b-118">**On-premises proxy server infrastructure** – a proxy device capable of SSL inspection, configured tooinsert hello header containing hello list of permitted tenants into traffic destined for Azure AD.</span></span> 

3. <span data-ttu-id="5383b-119">**用戶端軟體**– toosupport 租用戶的限制，用戶端軟體必須要求權杖直接從 Azure AD，使流量可以攔截 hello proxy 基礎結構。</span><span class="sxs-lookup"><span data-stu-id="5383b-119">**Client software** – toosupport Tenant Restrictions, client software must request tokens directly from Azure AD, so that traffic can be intercepted by hello proxy infrastructure.</span></span> <span data-ttu-id="5383b-120">目前瀏覽器型 Office 365 應用程式和使用新式驗證 (例如 OAuth 2.0) 的 Office 用戶端都支援「租用戶限制」。</span><span class="sxs-lookup"><span data-stu-id="5383b-120">Tenant Restrictions is currently supported by browser-based Office 365 applications and by Office clients when modern authentication (like OAuth 2.0) is used.</span></span> 

4. <span data-ttu-id="5383b-121">**新式驗證**– 雲端服務必須使用新式驗證 toouse 租用戶限制，並封鎖存取 tooall 非允許租用戶。</span><span class="sxs-lookup"><span data-stu-id="5383b-121">**Modern Authentication** – cloud services must use modern authentication toouse Tenant Restrictions and block access tooall non-permitted tenants.</span></span> <span data-ttu-id="5383b-122">Office 365 的雲端服務必須是預設設定的 toouse 新式驗證通訊協定。</span><span class="sxs-lookup"><span data-stu-id="5383b-122">Office 365 cloud services must be configured toouse modern authentication protocols by default.</span></span> <span data-ttu-id="5383b-123">Hello 最新的 Office 365 新式驗證支援的資訊，請參閱[更新 Office 365 新式驗證](https://blogs.office.com/2015/11/19/updated-office-365-modern-authentication-public-preview/)。</span><span class="sxs-lookup"><span data-stu-id="5383b-123">For hello latest information on Office 365 support for modern authentication, read [Updated Office 365 modern authentication](https://blogs.office.com/2015/11/19/updated-office-365-modern-authentication-public-preview/).</span></span>

<span data-ttu-id="5383b-124">hello 下列圖表說明 hello 高層級的流量。</span><span class="sxs-lookup"><span data-stu-id="5383b-124">hello following diagram illustrates hello high-level traffic flow.</span></span> <span data-ttu-id="5383b-125">SSL 檢查時，才需要在流量 tooAzure AD、 不 toohello Office 365 雲端服務。</span><span class="sxs-lookup"><span data-stu-id="5383b-125">SSL inspection is only required on traffic tooAzure AD, not toohello Office 365 cloud services.</span></span> <span data-ttu-id="5383b-126">這個差別是很重要的因為驗證 tooAzure AD hello 流量磁碟區通常遠比流量磁碟區 tooSaaS 應用程式，例如 Exchange Online 和 SharePoint Online。</span><span class="sxs-lookup"><span data-stu-id="5383b-126">This distinction is important because hello traffic volume for authentication tooAzure AD is typically much lower than traffic volume tooSaaS applications like Exchange Online and SharePoint Online.</span></span>

![租用戶限制流量流程 - 圖表](./media/active-directory-tenant-restrictions/traffic-flow.png)

## <a name="set-up-tenant-restrictions"></a><span data-ttu-id="5383b-128">設定租用戶限制</span><span class="sxs-lookup"><span data-stu-id="5383b-128">Set up Tenant Restrictions</span></span>

<span data-ttu-id="5383b-129">有兩個步驟 tooget 入門租用戶的限制。</span><span class="sxs-lookup"><span data-stu-id="5383b-129">There are two steps tooget started with Tenant Restrictions.</span></span> <span data-ttu-id="5383b-130">hello 第一個步驟是確定您的用戶端可以連接 toohello 右位址 toomake。</span><span class="sxs-lookup"><span data-stu-id="5383b-130">hello first step is toomake sure that your clients can connect toohello right addresses.</span></span> <span data-ttu-id="5383b-131">hello 第二種是 tooconfigure proxy 基礎結構。</span><span class="sxs-lookup"><span data-stu-id="5383b-131">hello second is tooconfigure your proxy infrastructure.</span></span>

### <a name="urls-and-ip-addresses"></a><span data-ttu-id="5383b-132">URL 和 IP 位址</span><span class="sxs-lookup"><span data-stu-id="5383b-132">URLs and IP addresses</span></span>

<span data-ttu-id="5383b-133">toouse 租用戶的限制，您的用戶端必須能夠 tooconnect toohello 下列 Azure AD Url tooauthenticate: login.microsoftonline.com、 login.microsoft.com 和 login.windows.net。</span><span class="sxs-lookup"><span data-stu-id="5383b-133">toouse Tenant Restrictions, your clients must be able tooconnect toohello following Azure AD URLs tooauthenticate: login.microsoftonline.com, login.microsoft.com, and login.windows.net.</span></span> <span data-ttu-id="5383b-134">此外，tooaccess Office 365，您的用戶端也必須能夠 tooconnect toohello Fqdn/Url 和 IP 位址中定義[Office 365 Url 與 IP 位址範圍](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2)。</span><span class="sxs-lookup"><span data-stu-id="5383b-134">Additionally, tooaccess Office 365, your clients must also be able tooconnect toohello FQDNs/URLs and IP addresses defined in [Office 365 URLs and IP address ranges](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2).</span></span> 

### <a name="proxy-configuration-and-requirements"></a><span data-ttu-id="5383b-135">Proxy 組態和需求</span><span class="sxs-lookup"><span data-stu-id="5383b-135">Proxy configuration and requirements</span></span>

<span data-ttu-id="5383b-136">下列組態的 hello 是透過 proxy 基礎結構的必要的 tooenable 租用戶的限制。</span><span class="sxs-lookup"><span data-stu-id="5383b-136">hello following configuration is required tooenable Tenant Restrictions through your proxy infrastructure.</span></span> <span data-ttu-id="5383b-137">本指南是泛型，所以您應該參閱 tooyour proxy 廠商的文件的特定實作步驟。</span><span class="sxs-lookup"><span data-stu-id="5383b-137">This guidance is generic, so you should refer tooyour proxy vendor’s documentation for specific implementation steps.</span></span>

#### <a name="prerequisites"></a><span data-ttu-id="5383b-138">必要條件</span><span class="sxs-lookup"><span data-stu-id="5383b-138">Prerequisites</span></span>

- <span data-ttu-id="5383b-139">hello proxy 必須是能夠 tooperform SSL 攔截、 HTTP 標頭插入與篩選目的地使用 Fqdn/Url。</span><span class="sxs-lookup"><span data-stu-id="5383b-139">hello proxy must be able tooperform SSL interception, HTTP header insertion, and filter destinations using FQDNs/URLs.</span></span> 

- <span data-ttu-id="5383b-140">用戶端必須信任 hello 出示 hello proxy 進行 SSL 通訊的憑證鏈結。</span><span class="sxs-lookup"><span data-stu-id="5383b-140">Clients must trust hello certificate chain presented by hello proxy for SSL communications.</span></span> <span data-ttu-id="5383b-141">例如，如果使用來自內部的 PKI 憑證，hello 內部發行根憑證授權單位憑證必須受信任。</span><span class="sxs-lookup"><span data-stu-id="5383b-141">For example, if certificates from an internal PKI are used, hello internal issuing root certificate authority certificate must be trusted.</span></span>

- <span data-ttu-id="5383b-142">此功能隨附於 Office 365 訂閱，但如果您想 toouse 租用戶限制 toocontrol 存取 tooother SaaS 應用程式然後 Azure AD Premium 1 授權所需。</span><span class="sxs-lookup"><span data-stu-id="5383b-142">This feature is included in Office 365 subscriptions, but if you want toouse Tenant Restrictions toocontrol access tooother SaaS apps then Azure AD Premium 1 licenses are required.</span></span>

#### <a name="configuration"></a><span data-ttu-id="5383b-143">組態</span><span class="sxs-lookup"><span data-stu-id="5383b-143">Configuration</span></span>

<span data-ttu-id="5383b-144">針對每個連入要求 toologin.microsoftonline.com、 login.microsoft.com，並且 login.windows.net 上插入兩個 HTTP 標頭：*限制的存取-到-租用戶*和*限制存取內容*。</span><span class="sxs-lookup"><span data-stu-id="5383b-144">For each incoming request toologin.microsoftonline.com, login.microsoft.com, and login.windows.net, insert two HTTP headers: *Restrict-Access-To-Tenants* and *Restrict-Access-Context*.</span></span>

<span data-ttu-id="5383b-145">hello 標頭應該包括下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="5383b-145">hello headers should include hello following elements:</span></span> 
- <span data-ttu-id="5383b-146">如*限制的存取-到-租用戶*，值為\<允許租用戶清單\>，這是以逗號分隔的清單要 tooallow 使用者 tooaccess 的租用戶。</span><span class="sxs-lookup"><span data-stu-id="5383b-146">For *Restrict-Access-To-Tenants*, a value of \<permitted tenant list\>, which is a comma-separated list of tenants you want tooallow users tooaccess.</span></span> <span data-ttu-id="5383b-147">任何已向租用戶的網域可以是使用的 tooidentify hello 租用戶，這份清單中。</span><span class="sxs-lookup"><span data-stu-id="5383b-147">Any domain that is registered with a tenant can be used tooidentify hello tenant in this list.</span></span> <span data-ttu-id="5383b-148">例如，toopermit 存取 tooboth Contoso 和 Fabrikam 租用戶，hello 名稱/值組看起來像是：`Restrict-Access-To-Tenants: contoso.onmicrosoft.com,fabrikam.onmicrosoft.com`</span><span class="sxs-lookup"><span data-stu-id="5383b-148">For example, toopermit access tooboth Contoso and Fabrikam tenants, hello name/value pair looks like:  `Restrict-Access-To-Tenants: contoso.onmicrosoft.com,fabrikam.onmicrosoft.com`</span></span> 
- <span data-ttu-id="5383b-149">如*限制存取內容*，單一目錄識別碼，宣告的租用戶已設定 hello 租用戶限制的值。</span><span class="sxs-lookup"><span data-stu-id="5383b-149">For *Restrict-Access-Context*, a value of a single directory ID, declaring which tenant is setting hello Tenant Restrictions.</span></span> <span data-ttu-id="5383b-150">例如，toodeclare Contoso 做為設定 hello 租用戶限制原則的 hello 租用戶，hello 名稱/值組看起來像：`Restrict-Access-Context: 456ff232-35l2-5h23-b3b3-3236w0826f3d`</span><span class="sxs-lookup"><span data-stu-id="5383b-150">For example, toodeclare Contoso as hello tenant that set hello Tenant Restrictions policy, hello name/value pair looks like: `Restrict-Access-Context: 456ff232-35l2-5h23-b3b3-3236w0826f3d`</span></span>  

> [!TIP]
> <span data-ttu-id="5383b-151">您可以找到您目錄的識別碼在 hello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="5383b-151">You can find your directory ID in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="5383b-152">請以系統管理員身分登入，選取 [Azure Active Directory]，然後選取 [屬性]。</span><span class="sxs-lookup"><span data-stu-id="5383b-152">Sign in as an administrator, select **Azure Active Directory**, then select **Properties**.</span></span>

<span data-ttu-id="5383b-153">tooprevent 使用者從自己的 HTTP 標頭插入與未經核准的租用戶，hello proxy 需要 tooreplace hello 限制的存取-到-租用戶標頭如果它已存在於 hello 連入要求中。</span><span class="sxs-lookup"><span data-stu-id="5383b-153">tooprevent users from inserting their own HTTP header with non-approved tenants, hello proxy needs tooreplace hello Restrict-Access-To-Tenants header if it is already present in hello incoming request.</span></span> 

<span data-ttu-id="5383b-154">用戶端必須強制的 toouse hello proxy 要求 toologin.microsoftonline.com、 login.microsoft.com，和 login.windows.net。</span><span class="sxs-lookup"><span data-stu-id="5383b-154">Clients must be forced toouse hello proxy for all requests toologin.microsoftonline.com, login.microsoft.com, and login.windows.net.</span></span> <span data-ttu-id="5383b-155">例如，如果 PAC 檔案使用的 toodirect 用戶端 toouse hello proxy，使用者應該不能 tooedit 或停用 hello PAC 檔案。</span><span class="sxs-lookup"><span data-stu-id="5383b-155">For example, if PAC files are used toodirect clients toouse hello proxy, end users should not be able tooedit or disable hello PAC files.</span></span>

## <a name="hello-user-experience"></a><span data-ttu-id="5383b-156">hello 使用者經驗</span><span class="sxs-lookup"><span data-stu-id="5383b-156">hello user experience</span></span>

<span data-ttu-id="5383b-157">此區段會顯示 hello 經驗的使用者和系統管理員 」。</span><span class="sxs-lookup"><span data-stu-id="5383b-157">This section shows hello experience for both end users and admins.</span></span>

### <a name="end-user-experience"></a><span data-ttu-id="5383b-158">使用者體驗</span><span class="sxs-lookup"><span data-stu-id="5383b-158">End-user experience</span></span>

<span data-ttu-id="5383b-159">範例使用者在 hello contoso 公司網路，但正嘗試 tooaccess hello Fabrikam 共用 SaaS 應用程式執行個體類似 Outlook 線上。</span><span class="sxs-lookup"><span data-stu-id="5383b-159">An example user is on hello Contoso network, but is trying tooaccess hello Fabrikam instance of a shared SaaS application like Outlook online.</span></span> <span data-ttu-id="5383b-160">如果該執行個體不允許租用戶 Contoso，hello 使用者會看到下列頁面的 hello:</span><span class="sxs-lookup"><span data-stu-id="5383b-160">If Contoso is a non-permitted tenant for that instance, hello user sees hello following page:</span></span>

![針對非允許之租用戶中使用者的拒絕存取頁面](./media/active-directory-tenant-restrictions/end-user-denied.png)

### <a name="admin-experience"></a><span data-ttu-id="5383b-162">管理員體驗</span><span class="sxs-lookup"><span data-stu-id="5383b-162">Admin experience</span></span>

<span data-ttu-id="5383b-163">雖然 hello 公司 proxy 基礎結構上完成租用戶限制的設定，系統管理員可直接存取 hello Azure 入口網站中的 hello 租用戶限制報表。</span><span class="sxs-lookup"><span data-stu-id="5383b-163">While configuration of Tenant Restrictions is done on hello corporate proxy infrastructure, admins can access hello Tenant Restrictions reports in hello Azure portal directly.</span></span> <span data-ttu-id="5383b-164">tooview hello 報告，toohello Azure Active Directory 概觀 頁面上，然後查看 其他的功能 底下。</span><span class="sxs-lookup"><span data-stu-id="5383b-164">tooview hello reports, go toohello Azure Active Directory Overview page, then look under ‘Other capabilities’.</span></span>

<span data-ttu-id="5383b-165">hello hello 租用戶系統管理員指定為 hello 受限存取內容的租用戶可以使用此報表 toosee，由於 hello 而封鎖所有的登入租用戶限制原則，包括使用 hello 身分識別，而且 hello 目標目錄識別碼。</span><span class="sxs-lookup"><span data-stu-id="5383b-165">hello admin for hello tenant specified as hello Restricted-Access-Context tenant can use this report toosee all sign-ins blocked because of hello Tenant Restrictions policy, including hello identity used and hello target directory ID.</span></span>

![使用登入嘗試限制的 Azure 入口網站 tooview hello](./media/active-directory-tenant-restrictions/portal-report.png)

<span data-ttu-id="5383b-167">其他跟報表一樣 hello Azure 入口網站中，您可以使用報表的篩選器 toospecify hello 範圍。</span><span class="sxs-lookup"><span data-stu-id="5383b-167">Like other reports in hello Azure portal, you can use filters toospecify hello scope of your report.</span></span> <span data-ttu-id="5383b-168">您可以依據特定使用者、應用程式、用戶端或時間間隔進行篩選。</span><span class="sxs-lookup"><span data-stu-id="5383b-168">You can filter on a specific user, application, client, or time interval.</span></span>

## <a name="office-365-support"></a><span data-ttu-id="5383b-169">Office 365 支援</span><span class="sxs-lookup"><span data-stu-id="5383b-169">Office 365 support</span></span>

<span data-ttu-id="5383b-170">Office 365 應用程式必須符合兩個準則 toofully 支援租用戶的限制：</span><span class="sxs-lookup"><span data-stu-id="5383b-170">Office 365 applications must meet two criteria toofully support Tenant Restrictions:</span></span>

1. <span data-ttu-id="5383b-171">使用 hello 用戶端支援新式驗證</span><span class="sxs-lookup"><span data-stu-id="5383b-171">hello client used supports modern authentication</span></span>
2. <span data-ttu-id="5383b-172">新式驗證會啟用為 hello 雲端服務的 hello 預設驗證通訊協定。</span><span class="sxs-lookup"><span data-stu-id="5383b-172">Modern authentication is enabled as hello default authentication protocol for hello cloud service.</span></span>

<span data-ttu-id="5383b-173">請參閱太[更新 Office 365 新式驗證](https://blogs.office.com/2015/11/19/updated-office-365-modern-authentication-public-preview/)hello 最新的 office 用戶端目前支援新式驗證的資訊。</span><span class="sxs-lookup"><span data-stu-id="5383b-173">Refer too[Updated Office 365 modern authentication](https://blogs.office.com/2015/11/19/updated-office-365-modern-authentication-public-preview/) for hello latest information on which Office clients currently support modern authentication.</span></span> <span data-ttu-id="5383b-174">該頁面也包含連結 tooinstructions 啟用新式驗證等特定 Exchange Online Skype for Business Online 租用戶。</span><span class="sxs-lookup"><span data-stu-id="5383b-174">That page also includes links tooinstructions for enabling modern authentication on specific Exchange Online and Skype for Business Online tenants.</span></span> <span data-ttu-id="5383b-175">SharePoint Online 中已經預設啟用新式驗證。</span><span class="sxs-lookup"><span data-stu-id="5383b-175">Modern authentication is already enabled by default in SharePoint Online.</span></span>

<span data-ttu-id="5383b-176">Office 365 瀏覽器型應用程式目前支援租用戶限制 (hello Office 入口網站中，Yammer，SharePoint 網站、 Outlook hello Web 等。)。</span><span class="sxs-lookup"><span data-stu-id="5383b-176">Tenant Restrictions is currently supported by Office 365 browser-based applications (hello Office Portal, Yammer, SharePoint sites, Outlook on hello Web, etc.).</span></span> <span data-ttu-id="5383b-177">針對豐富型用戶端 (Outlook、商務用 Skype、Word、Excel、PowerPoint 等)，只有在使用新式驗證的情況下，才能強制執行「租用戶限制」。</span><span class="sxs-lookup"><span data-stu-id="5383b-177">For thick clients (Outlook, Skype for Business, Word, Excel, PowerPoint, etc.) Tenant Restrictions can only be enforced when modern authentication is used.</span></span>  

<span data-ttu-id="5383b-178">Outlook 及 Skype 支援新式驗證的商務用戶端針對租用戶的仍能 toouse 傳統通訊協定不啟用新式驗證，有效地略過租用戶的限制。</span><span class="sxs-lookup"><span data-stu-id="5383b-178">Outlook and Skype for Business clients that support modern authentication are still able toouse legacy protocols against tenants where modern authentication is not enabled, effectively bypassing Tenant Restrictions.</span></span> <span data-ttu-id="5383b-179">在 Windows 上的 outlook，客戶可能選擇 tooimplement 限制防止使用者加入未經核准的郵件帳戶 tootheir 設定檔。</span><span class="sxs-lookup"><span data-stu-id="5383b-179">For Outlook on Windows, customers may choose tooimplement restrictions preventing end users from adding non-approved mail accounts tootheir profiles.</span></span> <span data-ttu-id="5383b-180">例如，請參閱 hello[防止新增非預設 Exchange 帳戶](http://gpsearch.azurewebsites.net/default.aspx?ref=1)群組原則設定。</span><span class="sxs-lookup"><span data-stu-id="5383b-180">For example, see hello [Prevent adding non-default Exchange accounts](http://gpsearch.azurewebsites.net/default.aspx?ref=1) group policy setting.</span></span> <span data-ttu-id="5383b-181">對於非 Windows 平台上的 Outlook 與所有平台上的商務用 Skype，目前尚未完整支援租用戶限制。</span><span class="sxs-lookup"><span data-stu-id="5383b-181">For Outlook on non-Windows platforms, and for Skype for Business on all platforms, full support for Tenant Restrictions is not currently available.</span></span>

## <a name="testing"></a><span data-ttu-id="5383b-182">測試</span><span class="sxs-lookup"><span data-stu-id="5383b-182">Testing</span></span>

<span data-ttu-id="5383b-183">如果您想出租用戶限制 tootry 供整個組織中實作之前，有兩個選項： 主控件為基礎的方法，使用 Fiddler 或 proxy 設定的分段首度發行工具。</span><span class="sxs-lookup"><span data-stu-id="5383b-183">If you want tootry out Tenant Restrictions before implementing it for your whole organization, there are two options: a host-based approach using a tool like Fiddler, or a staged rollout of proxy settings.</span></span>

### <a name="fiddler-for-a-host-based-approach"></a><span data-ttu-id="5383b-184">適用於主機型方法的 Fiddler</span><span class="sxs-lookup"><span data-stu-id="5383b-184">Fiddler for a host-based approach</span></span>

<span data-ttu-id="5383b-185">Fiddler 是免費的 web 偵錯 proxy 可使用的 toocapture 和修改包括插入 HTTP 標頭的 HTTP/HTTPS 流量。</span><span class="sxs-lookup"><span data-stu-id="5383b-185">Fiddler is a free web debugging proxy that can be used toocapture and modify HTTP/HTTPS traffic, including inserting HTTP headers.</span></span> <span data-ttu-id="5383b-186">tooconfigure Fiddler tootest 租用戶的限制，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="5383b-186">tooconfigure Fiddler tootest Tenant Restrictions, perform hello following steps:</span></span>

1.  <span data-ttu-id="5383b-187">[下載並安裝 Fiddler](http://www.telerik.com/fiddler)。</span><span class="sxs-lookup"><span data-stu-id="5383b-187">[Download and install Fiddler](http://www.telerik.com/fiddler).</span></span>
2.  <span data-ttu-id="5383b-188">Fiddler toodecrypt HTTPS 流量，設定每個[Fiddler 的說明 」 文件](http://docs.telerik.com/fiddler/Configure-Fiddler/Tasks/DecryptHTTPS)。</span><span class="sxs-lookup"><span data-stu-id="5383b-188">Configure Fiddler toodecrypt HTTPS traffic, per [Fiddler’s help documentation](http://docs.telerik.com/fiddler/Configure-Fiddler/Tasks/DecryptHTTPS).</span></span>
3.  <span data-ttu-id="5383b-189">設定 Fiddler tooinsert hello*限制的存取-到-租用戶*和*限制存取內容*標頭使用自訂規則：</span><span class="sxs-lookup"><span data-stu-id="5383b-189">Configure Fiddler tooinsert hello *Restrict-Access-To-Tenants* and *Restrict-Access-Context* headers using custom rules:</span></span>
  1. <span data-ttu-id="5383b-190">在 hello Fiddler Web Debugger 工具中，選取 hello**規則**功能表，然後選取**自訂規則...**</span><span class="sxs-lookup"><span data-stu-id="5383b-190">In hello Fiddler Web Debugger tool, select hello **Rules** menu and select **Customize Rules…**</span></span> <span data-ttu-id="5383b-191">tooopen hello CustomRules 檔案。</span><span class="sxs-lookup"><span data-stu-id="5383b-191">tooopen hello CustomRules file.</span></span>
  2. <span data-ttu-id="5383b-192">新增下列在 hello hello 開頭的行 hello *OnBeforeRequest*函式。</span><span class="sxs-lookup"><span data-stu-id="5383b-192">Add hello following lines at hello beginning of hello *OnBeforeRequest* function.</span></span> <span data-ttu-id="5383b-193">使用與您租用戶一起註冊的網域來取代 \<tenant domain\>，例如 contoso.onmicrosoft.com。使用您租用戶的 Azure AD GUID 識別碼來取代 \<directory ID\>。</span><span class="sxs-lookup"><span data-stu-id="5383b-193">Replace \<tenant domain\> with a domain registered with your tenant, for example, contoso.onmicrosoft.com. Replace \<directory ID\> with your tenant's Azure AD GUID identifier.</span></span>

  ```
  if (oSession.HostnameIs("login.microsoftonline.com") || oSession.HostnameIs("login.microsoft.com") || oSession.HostnameIs("login.windows.net")){      oSession.oRequest["Restrict-Access-To-Tenants"] = "<tenant domain>";      oSession.oRequest["Restrict-Access-Context"] = "<directory ID>";}
  ```

  <span data-ttu-id="5383b-194">如果您需要 tooallow 多個租用戶，請使用逗號 tooseparate hello 租用戶名稱。</span><span class="sxs-lookup"><span data-stu-id="5383b-194">If you need tooallow multiple tenants, use a comma tooseparate hello tenant names.</span></span> <span data-ttu-id="5383b-195">例如：</span><span class="sxs-lookup"><span data-stu-id="5383b-195">For example:</span></span>

  ```
  oSession.oRequest["Restrict-Access-To-Tenants"] = "contoso.onmicrosoft.com,fabrikam.onmicrosoft.com";
  ```

4. <span data-ttu-id="5383b-196">儲存並關閉 hello CustomRules 檔案。</span><span class="sxs-lookup"><span data-stu-id="5383b-196">Save and close hello CustomRules file.</span></span>

<span data-ttu-id="5383b-197">設定 Fiddler 之後，您可以擷取的流量將 toohello**檔案**功能表，然後選取**擷取流量**。</span><span class="sxs-lookup"><span data-stu-id="5383b-197">After you configure Fiddler, you can capture traffic by going toohello **File** menu and selecting **Capture Traffic**.</span></span>

### <a name="staged-rollout-of-proxy-settings"></a><span data-ttu-id="5383b-198">分段推出 Proxy 設定</span><span class="sxs-lookup"><span data-stu-id="5383b-198">Staged rollout of proxy settings</span></span>

<span data-ttu-id="5383b-199">根據 hello proxy 基礎結構的功能，您可能會無法 toostage hello 首度發行的設定 tooyour 使用者。</span><span class="sxs-lookup"><span data-stu-id="5383b-199">Depending on hello capabilities of your proxy infrastructure, you may be able toostage hello rollout of settings tooyour users.</span></span> <span data-ttu-id="5383b-200">以下是一些可供考量的概略選項：</span><span class="sxs-lookup"><span data-stu-id="5383b-200">Here are a couple high-level options for consideration:</span></span>

1.  <span data-ttu-id="5383b-201">使用 PAC 檔案 toopoint 測試使用者 tooa 測試 proxy 基礎結構，而一般使用者繼續 toouse hello 生產 proxy 基礎結構。</span><span class="sxs-lookup"><span data-stu-id="5383b-201">Use PAC files toopoint test users tooa test proxy infrastructure, while normal users continue toouse hello production proxy infrastructure.</span></span>
2.  <span data-ttu-id="5383b-202">有些 Proxy 伺服器可以使用群組來支援不同的組態。</span><span class="sxs-lookup"><span data-stu-id="5383b-202">Some proxy servers may support different configurations using groups.</span></span>

<span data-ttu-id="5383b-203">如需特定詳細資料，請參閱 tooyour proxy 伺服器文件集。</span><span class="sxs-lookup"><span data-stu-id="5383b-203">Refer tooyour proxy server documentation for specific details.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5383b-204">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5383b-204">Next steps</span></span>

- <span data-ttu-id="5383b-205">閱讀[更新的 Office 365 新式驗證 (英文)](https://blogs.office.com/2015/11/19/updated-office-365-modern-authentication-public-preview/)</span><span class="sxs-lookup"><span data-stu-id="5383b-205">Read about [Updated Office 365 modern authentication](https://blogs.office.com/2015/11/19/updated-office-365-modern-authentication-public-preview/)</span></span>

- <span data-ttu-id="5383b-206">檢閱 hello [Office 365 Url 與 IP 位址範圍](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2)</span><span class="sxs-lookup"><span data-stu-id="5383b-206">Review hello [Office 365 URLs and IP address ranges](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2)</span></span>
