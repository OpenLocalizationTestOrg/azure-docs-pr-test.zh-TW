---
title: "aaaHow 應用程式會加入 tooAzure Active Directory。"
description: "本文說明如何將應用程式加入 Azure Active Directory tooan 執行個體。"
services: active-directory
documentationcenter: 
author: shoatman
manager: kbrint
editor: 
ms.assetid: 3321d130-f2a8-4e38-b35e-0959693f3576
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/09/2016
ms.author: shoatman
ms.custom: aaddev
ms.openlocfilehash: 3ca710c58a403b52e8b728202ad9010f4873bcea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-and-why-applications-are-added-tooazure-ad"></a><span data-ttu-id="53997-103">將應用程式如何及為何加入 tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="53997-103">How and why applications are added tooAzure AD</span></span>
<span data-ttu-id="53997-104">其中一個 hello 最初令人感到困惑項目在您的 Azure Active Directory 執行個體中檢視應用程式的清單時了解 hello 應用程式的來源，以及為何發生。</span><span class="sxs-lookup"><span data-stu-id="53997-104">One of hello initially puzzling things when viewing a list of applications in your instance of Azure Active Directory is understanding where hello applications came from and why they are there.</span></span>  <span data-ttu-id="53997-105">這篇文章會提供應用程式都可以在 hello 目錄和您提供可協助您了解如何應用程式的來源目錄中的 toobe 內容的方式的高層級概觀。</span><span class="sxs-lookup"><span data-stu-id="53997-105">This article will provide a high level overview of how applications are represented in hello directory and provide you with context that will assist you in understanding how an application came toobe in your directory.</span></span>

## <a name="what-services-does-azure-ad-provide-tooapplications"></a><span data-ttu-id="53997-106">有哪些服務 Azure AD 提供 tooapplications？</span><span class="sxs-lookup"><span data-stu-id="53997-106">What services does Azure AD provide tooapplications?</span></span>
<span data-ttu-id="53997-107">應用程式會加入 tooAzure AD tooleverage 一或多個 hello 它所提供的服務。</span><span class="sxs-lookup"><span data-stu-id="53997-107">Applications are added tooAzure AD tooleverage one or more of hello services it provides.</span></span>  <span data-ttu-id="53997-108">這些服務包括：</span><span class="sxs-lookup"><span data-stu-id="53997-108">Those services include:</span></span>

* <span data-ttu-id="53997-109">應用程式驗證與授權</span><span class="sxs-lookup"><span data-stu-id="53997-109">App authentication and authorization</span></span>
* <span data-ttu-id="53997-110">使用者驗證與授權</span><span class="sxs-lookup"><span data-stu-id="53997-110">User authentication & authorization</span></span>
* <span data-ttu-id="53997-111">使用同盟或密碼的單一登入 (SSO)</span><span class="sxs-lookup"><span data-stu-id="53997-111">Single sign-on (SSO) using federation or password</span></span>
* <span data-ttu-id="53997-112">使用者佈建與同步處理</span><span class="sxs-lookup"><span data-stu-id="53997-112">User provisioning & synchronization</span></span>
* <span data-ttu-id="53997-113">以角色為基礎的存取控制。使用 hello 目錄 toodefine 應用程式角色 tooperform 角色為基礎的應用程式中的授權檢查。</span><span class="sxs-lookup"><span data-stu-id="53997-113">Role-based access control; Use hello directory toodefine application roles tooperform roles based authorization checks in an app.</span></span>
* <span data-ttu-id="53997-114">oAuth 授權服務 （使用 Office 365 和其他 Microsoft 應用程式 tooauthorize 存取 tooAPIs/資源）。</span><span class="sxs-lookup"><span data-stu-id="53997-114">oAuth authorization services (used by Office 365 and other Microsoft apps tooauthorize access tooAPIs/resources.)</span></span>
* <span data-ttu-id="53997-115">發佈應用程式與 proxy;發行應用程式從私人網路 toohello 網際網路</span><span class="sxs-lookup"><span data-stu-id="53997-115">Application publishing & proxy; Publish an app from a private network toohello internet</span></span>

## <a name="how-are-applications-represented-in-hello-directory"></a><span data-ttu-id="53997-116">應用程式代表 hello 目錄中的？</span><span class="sxs-lookup"><span data-stu-id="53997-116">How are applications represented in hello directory?</span></span>
<span data-ttu-id="53997-117">代表 hello 2 的物件，使用 Azure AD 中應用程式： 應用程式物件與服務主體物件。</span><span class="sxs-lookup"><span data-stu-id="53997-117">Applications are represented in hello Azure AD using 2 objects: an application object and a service principal object.</span></span>  <span data-ttu-id="53997-118">一個應用程式物件，註冊中 「 家用 」 / 「 擁有者 」 或 「 發行 」 目錄以及一個或多個服務主體物件，表示它會每個目錄中的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="53997-118">There is one application object, registered in a "home"/"owner" or "publishing" directory and one or more service principal objects representing hello application in every directory in which it acts.</span></span>  

<span data-ttu-id="53997-119">hello 應用程式物件描述 hello 應用程式 tooAzure AD （hello 多租用戶的服務），而且可能包括 hello 下列任何一項: (*注意*： 這不是獨占清單。)</span><span class="sxs-lookup"><span data-stu-id="53997-119">hello application object describes hello app tooAzure AD (hello multi-tenant service) and may include any of hello following: (*Note*: This is not an exhaustive list.)</span></span>

* <span data-ttu-id="53997-120">名稱、標誌和發行者</span><span class="sxs-lookup"><span data-stu-id="53997-120">Name, Logo & Publisher</span></span>
* <span data-ttu-id="53997-121">密碼 （對稱和/或非對稱金鑰會用 tooauthenticate hello 應用程式）</span><span class="sxs-lookup"><span data-stu-id="53997-121">Secrets (symmetric and/or asymmetric keys used tooauthenticate hello app)</span></span>
* <span data-ttu-id="53997-122">API 相依性 (oAuth)</span><span class="sxs-lookup"><span data-stu-id="53997-122">API dependencies (oAuth)</span></span>
* <span data-ttu-id="53997-123">API/資源/發佈範圍 (oAuth)</span><span class="sxs-lookup"><span data-stu-id="53997-123">APIs/resources/scopes published (oAuth)</span></span>
* <span data-ttu-id="53997-124">應用程式角色 (RBAC)</span><span class="sxs-lookup"><span data-stu-id="53997-124">App roles (RBAC)</span></span>
* <span data-ttu-id="53997-125">SSO 中繼資料和組態 (SSO)</span><span class="sxs-lookup"><span data-stu-id="53997-125">SSO metadata and configuration (SSO)</span></span>
* <span data-ttu-id="53997-126">使用者佈建中繼資料和組態</span><span class="sxs-lookup"><span data-stu-id="53997-126">User provisioning metadata and configuration</span></span>
* <span data-ttu-id="53997-127">Proxy 中繼資料和組態</span><span class="sxs-lookup"><span data-stu-id="53997-127">Proxy metadata and configuration</span></span>

<span data-ttu-id="53997-128">hello 服務主要是每個 hello 應用程式會包括其主目錄的目錄中的 hello 應用程式的記錄。</span><span class="sxs-lookup"><span data-stu-id="53997-128">hello service principal is a record of hello application in every directory, where hello application acts including its home directory.</span></span>  <span data-ttu-id="53997-129">hello 服務主體：</span><span class="sxs-lookup"><span data-stu-id="53997-129">hello service principal:</span></span>

* <span data-ttu-id="53997-130">是指回 tooan 應用程式物件，透過 hello 應用程式 id 屬性</span><span class="sxs-lookup"><span data-stu-id="53997-130">Refers back tooan application object via hello app id property</span></span>
* <span data-ttu-id="53997-131">記錄本機使用者和群組應用程式角色指派</span><span class="sxs-lookup"><span data-stu-id="53997-131">Records local user and group app-role assignments</span></span>
* <span data-ttu-id="53997-132">記錄本機使用者和系統管理員權限授與 toohello 應用程式</span><span class="sxs-lookup"><span data-stu-id="53997-132">Records local user and admin permissions granted toohello app</span></span>
  * <span data-ttu-id="53997-133">例如： hello 應用程式 tooaccess 特定使用者的電子郵件的權限</span><span class="sxs-lookup"><span data-stu-id="53997-133">For example: permission for hello app tooaccess a particular users email</span></span>
* <span data-ttu-id="53997-134">記錄本機原則，包括條件式存取原則</span><span class="sxs-lookup"><span data-stu-id="53997-134">Records local policies including conditional access policy</span></span>
* <span data-ttu-id="53997-135">記錄應用程式的本機替代本機設定</span><span class="sxs-lookup"><span data-stu-id="53997-135">Records local alternate local settings for an app</span></span>
  * <span data-ttu-id="53997-136">宣告轉換規則</span><span class="sxs-lookup"><span data-stu-id="53997-136">Claims transformation rules</span></span>
  * <span data-ttu-id="53997-137">屬性對應 (使用者佈建)</span><span class="sxs-lookup"><span data-stu-id="53997-137">Attribute mappings (User provisioning)</span></span>
  * <span data-ttu-id="53997-138">（如果 hello 應用程式支援的自訂角色），租用戶特定的應用程式角色</span><span class="sxs-lookup"><span data-stu-id="53997-138">Tenant specific app roles (if hello app supports custom roles)</span></span>
  * <span data-ttu-id="53997-139">名稱/標誌</span><span class="sxs-lookup"><span data-stu-id="53997-139">Name/Logo</span></span>

### <a name="a-diagram-of-application-objects-and-service-principals-across-directories"></a><span data-ttu-id="53997-140">目錄間的應用程式物件和服務主體圖表</span><span class="sxs-lookup"><span data-stu-id="53997-140">A diagram of application objects and service principals across directories</span></span>
![說明應用程式物件和服務主體如何與現有 Azure AD 執行個體共存的圖表。][apps_service_principals_directory]

<span data-ttu-id="53997-142">您可以從 hello 上圖中看到。</span><span class="sxs-lookup"><span data-stu-id="53997-142">As you can see from hello diagram above.</span></span>  <span data-ttu-id="53997-143">Microsoft 會維護兩個目錄內部 （左側 hello），它使用 toopublish 應用程式。</span><span class="sxs-lookup"><span data-stu-id="53997-143">Microsoft maintains two directories internally (on hello left) it uses toopublish applications.</span></span>

* <span data-ttu-id="53997-144">一個用於 Microsoft 應用程式 (Microsoft 服務目錄)</span><span class="sxs-lookup"><span data-stu-id="53997-144">One for Microsoft Apps (Microsoft services directory)</span></span>
* <span data-ttu-id="53997-145">一個用於預先整合的協力廠商應用程式 (應用程式庫目錄)</span><span class="sxs-lookup"><span data-stu-id="53997-145">One for pre-integrated 3rd Party Apps (App Gallery directory)</span></span>

<span data-ttu-id="53997-146">應用程式的發行者/廠商與 Azure AD 整合所需的 toohave 發行目錄。</span><span class="sxs-lookup"><span data-stu-id="53997-146">Application publishers/vendors who integrate with Azure AD are required toohave a publishing directory.</span></span>  <span data-ttu-id="53997-147">(某些 SAAS 目錄)。</span><span class="sxs-lookup"><span data-stu-id="53997-147">(Some SAAS Directory).</span></span>

<span data-ttu-id="53997-148">自行新增的應用程式包括：</span><span class="sxs-lookup"><span data-stu-id="53997-148">Applications that you add yourself include:</span></span>

* <span data-ttu-id="53997-149">自行開發的應用程式 (與 AAD 整合)</span><span class="sxs-lookup"><span data-stu-id="53997-149">Apps you developed (integrated with AAD)</span></span>
* <span data-ttu-id="53997-150">為單一登入而進行連線的應用程式</span><span class="sxs-lookup"><span data-stu-id="53997-150">Apps you connected for single-sign-on</span></span>
* <span data-ttu-id="53997-151">使用發行的應用程式 hello Azure AD 應用程式 proxy。</span><span class="sxs-lookup"><span data-stu-id="53997-151">Apps you published using hello Azure AD application proxy.</span></span>

### <a name="a-couple-of-notes-and-exceptions"></a><span data-ttu-id="53997-152">幾個附註和例外狀況</span><span class="sxs-lookup"><span data-stu-id="53997-152">A couple of notes and exceptions</span></span>
* <span data-ttu-id="53997-153">並非所有的服務主體點後 tooapplication 物件。</span><span class="sxs-lookup"><span data-stu-id="53997-153">Not all service principals point back tooapplication objects.</span></span>  <span data-ttu-id="53997-154">是嗎？</span><span class="sxs-lookup"><span data-stu-id="53997-154">Huh?</span></span> <span data-ttu-id="53997-155">最初是建立 Azure AD 時 hello 服務會提供更多限制 tooapplications 所以 hello 服務主體已足夠完成建立應用程式識別。</span><span class="sxs-lookup"><span data-stu-id="53997-155">When Azure AD was originally built hello services provided tooapplications were much more limited and hello service principal was sufficient for establishing an app identity.</span></span>  <span data-ttu-id="53997-156">hello 原始服務主體已更接近圖形 toohello Windows Server Active Directory 服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="53997-156">hello original service principal was closer in shape toohello Windows Server Active Directory service account.</span></span>  <span data-ttu-id="53997-157">基於這個理由，就仍然可以 toocreate 服務主體使用 hello Azure AD PowerShell，而不需要第一個建立的應用程式物件。</span><span class="sxs-lookup"><span data-stu-id="53997-157">For this reason it's still possible toocreate service principals using hello Azure AD PowerShell without first creating an application object.</span></span>  <span data-ttu-id="53997-158">hello Graph API 要求的應用程式物件之前建立服務主體。</span><span class="sxs-lookup"><span data-stu-id="53997-158">hello Graph API requires an app object before creating a service principal.</span></span>
* <span data-ttu-id="53997-159">並非所有的 hello 上面所述的資訊目前是以程式設計方式公開。</span><span class="sxs-lookup"><span data-stu-id="53997-159">Not all of hello information described above is currently exposed programmatically.</span></span>  <span data-ttu-id="53997-160">只有 hello 下列 hello UI 中的項目：</span><span class="sxs-lookup"><span data-stu-id="53997-160">hello following are only available in hello UI:</span></span>
  * <span data-ttu-id="53997-161">宣告轉換規則</span><span class="sxs-lookup"><span data-stu-id="53997-161">Claims transformation rules</span></span>
  * <span data-ttu-id="53997-162">屬性對應 (使用者佈建)</span><span class="sxs-lookup"><span data-stu-id="53997-162">Attribute mappings (User provisioning)</span></span>
* <span data-ttu-id="53997-163">如需詳細資訊的詳細資訊 hello 服務主體和應用程式物件，請參閱 toohello Azure AD Graph REST API 參考文件。</span><span class="sxs-lookup"><span data-stu-id="53997-163">For more detailed information on hello service principal and application objects please refer toohello Azure AD Graph REST API reference documentation.</span></span>  <span data-ttu-id="53997-164">*提示*: hello Azure AD Graph API 文件是目前可用的 Azure AD 的 hello 最接近的動作 tooa 結構描述參考。</span><span class="sxs-lookup"><span data-stu-id="53997-164">*Hint*: hello Azure AD Graph API documentation is hello closest thing tooa schema reference for Azure AD that's currently available.</span></span>  
  * [<span data-ttu-id="53997-165">應用程式</span><span class="sxs-lookup"><span data-stu-id="53997-165">Application</span></span>](https://msdn.microsoft.com/library/azure/dn151677.aspx)
  * [<span data-ttu-id="53997-166">服務主體</span><span class="sxs-lookup"><span data-stu-id="53997-166">Service Principal</span></span>](https://msdn.microsoft.com/library/azure/dn194452.aspx)

## <a name="how-are-apps-added-toomy-azure-ad-instance"></a><span data-ttu-id="53997-167">應用程式如何加入 toomy Azure AD 執行個體？</span><span class="sxs-lookup"><span data-stu-id="53997-167">How are apps added toomy Azure AD instance?</span></span>
<span data-ttu-id="53997-168">有許多方法可加入應用程式 tooAzure AD:</span><span class="sxs-lookup"><span data-stu-id="53997-168">There are many ways an app can be added tooAzure AD:</span></span>

* <span data-ttu-id="53997-169">新增應用程式從 hello [Azure Active Directory 應用程式庫](https://azure.microsoft.com/updates/azure-active-directory-over-1000-apps/)</span><span class="sxs-lookup"><span data-stu-id="53997-169">Add an app from hello [Azure Active Directory App Gallery](https://azure.microsoft.com/updates/azure-active-directory-over-1000-apps/)</span></span>
* <span data-ttu-id="53997-170">註冊/登入與 Azure Active Directory 整合的協力廠商應用程式 (例如：[Smartsheet](https://app.smartsheet.com/b/home) 或 [DocuSign](https://www.docusign.net/member/MemberLogin.aspx))</span><span class="sxs-lookup"><span data-stu-id="53997-170">Sign up/into a 3rd Party App integrated with Azure Active Directory (For example: [Smartsheet](https://app.smartsheet.com/b/home) or [DocuSign](https://www.docusign.net/member/MemberLogin.aspx))</span></span>
  * <span data-ttu-id="53997-171">在向上/使用者在註冊時為問的 toogive 權限 toohello 應用程式 tooaccess 其設定檔和其他權限。</span><span class="sxs-lookup"><span data-stu-id="53997-171">During sign up/in users are asked toogive permission toohello app tooaccess their profile and other permissions.</span></span>  <span data-ttu-id="53997-172">第一個人 toogive hello 同意原因代表 hello 應用程式 toobe 加入的 toohello 目錄服務主體。</span><span class="sxs-lookup"><span data-stu-id="53997-172">hello first person toogive consent causes a service principal representing hello app toobe added toohello directory.</span></span>
* <span data-ttu-id="53997-173">註冊/登入 Microsoft 線上服務 (如 [Office 365](http://products.office.com/)</span><span class="sxs-lookup"><span data-stu-id="53997-173">Sign up/into Microsoft online services like [Office 365](http://products.office.com/)</span></span>
  * <span data-ttu-id="53997-174">當您訂閱 tooOffice 365 開始試用版的一個或多個服務主體的建立 hello 目錄代表 hello 使用的 toodeliver hello 功能的所有 Office 365 與相關聯的各種服務。</span><span class="sxs-lookup"><span data-stu-id="53997-174">When you subscribe tooOffice 365 or begin a trial one or more service principals are created in hello directory representing hello various services that are used toodeliver all of hello functionality associated with Office 365.</span></span>
  * <span data-ttu-id="53997-175">某些的 Office 365 服務，例如 SharePoint 上持續 tooallow 之間的通訊安全包括工作流程的元件建立服務主體。</span><span class="sxs-lookup"><span data-stu-id="53997-175">Some Office 365 services like SharePoint create service principals on an on-going basis tooallow secure communication between components including workflows.</span></span>
* <span data-ttu-id="53997-176">Hello，請參閱 Azure 管理入口網站中新增您正在開發應用程式： https://msdn.microsoft.com/library/azure/dn132599.aspx</span><span class="sxs-lookup"><span data-stu-id="53997-176">Add an app you're developing in hello Azure Management Portal see: https://msdn.microsoft.com/library/azure/dn132599.aspx</span></span>
* <span data-ttu-id="53997-177">新增您使用 Visual Studio 開發的應用程式，請參閱：</span><span class="sxs-lookup"><span data-stu-id="53997-177">Add an app you're developing using Visual Studio see:</span></span>
  * [<span data-ttu-id="53997-178">ASP.Net 驗證方法</span><span class="sxs-lookup"><span data-stu-id="53997-178">ASP.Net Authentication Methods</span></span>](http://www.asp.net/visual-studio/overview/2013/creating-web-projects-in-visual-studio#orgauthoptions)
  * [<span data-ttu-id="53997-179">連接的服務</span><span class="sxs-lookup"><span data-stu-id="53997-179">Connected Services</span></span>](http://blogs.msdn.com/b/visualstudio/archive/2014/11/19/connecting-to-cloud-services.aspx)
* <span data-ttu-id="53997-180">新增應用程式 toouse toouse hello [Azure AD Application Proxy](https://msdn.microsoft.com/library/azure/dn768219.aspx)</span><span class="sxs-lookup"><span data-stu-id="53997-180">Add an app toouse toouse hello [Azure AD Application Proxy](https://msdn.microsoft.com/library/azure/dn768219.aspx)</span></span>
* <span data-ttu-id="53997-181">連接應用程式進行使用 SAML 或密碼 SSO 的單一登入</span><span class="sxs-lookup"><span data-stu-id="53997-181">Connect an app for single sign on using SAML or Password SSO</span></span>
* <span data-ttu-id="53997-182">許多其他項目，包括在 Azure 中的各種開發人員經驗和/在跨開發人員中心的 API 總管體驗</span><span class="sxs-lookup"><span data-stu-id="53997-182">Many others including various developer experiences in Azure and/in API explorer experiences across developer centers</span></span>

## <a name="who-has-permission-tooadd-applications-toomy-azure-ad-instance"></a><span data-ttu-id="53997-183">誰有權限 tooadd 應用程式 toomy Azure AD 執行個體？</span><span class="sxs-lookup"><span data-stu-id="53997-183">Who has permission tooadd applications toomy Azure AD instance?</span></span>
<span data-ttu-id="53997-184">只有全域系統管理員可以：</span><span class="sxs-lookup"><span data-stu-id="53997-184">Only global administrators can:</span></span>

* <span data-ttu-id="53997-185">新增應用程式從 hello Azure AD app 資源庫 （預先整合第 3 個合作對象應用程式）</span><span class="sxs-lookup"><span data-stu-id="53997-185">Add apps from hello Azure AD app gallery (pre-integrated 3rd Party Apps)</span></span>
* <span data-ttu-id="53997-186">發行應用程式使用 Azure AD Application Proxy hello</span><span class="sxs-lookup"><span data-stu-id="53997-186">Publish an app using hello Azure AD Application Proxy</span></span>

<span data-ttu-id="53997-187">您的目錄中的所有使用者都有權限 tooadd 應用程式所開發並自行決定哪些應用程式透過它們共用/授與存取 tootheir 組織資料。</span><span class="sxs-lookup"><span data-stu-id="53997-187">All users in your directory have rights tooadd applications that they are developing and discretion over which applications they share/give access tootheir organizational data.</span></span>  <span data-ttu-id="53997-188">*請記住向上/tooan 應用程式中的使用者登，並授與權限可能會導致服務主體所建立。*</span><span class="sxs-lookup"><span data-stu-id="53997-188">*Remember user sign up/in tooan app and granting permissions may result in a service principal being created.*</span></span>

<span data-ttu-id="53997-189">這個可能一開始音效有關，但保留 hello 下列幾點：</span><span class="sxs-lookup"><span data-stu-id="53997-189">This might initially sound concerning, but keep hello following in mind:</span></span>

* <span data-ttu-id="53997-190">應用程式已能夠 tooleverage Windows Server Active Directory 進行使用者驗證，而不需要在 hello 目錄中註冊/記錄 hello 應用程式 toobe 多年。</span><span class="sxs-lookup"><span data-stu-id="53997-190">Apps have been able tooleverage Windows Server Active Directory for user authentication for many years without requiring hello application toobe registered/recorded in hello directory.</span></span>  <span data-ttu-id="53997-191">現在 hello 組織會改善可視性 tooexactly 多少應用程式使用了 hello 目錄和苦頭 for。</span><span class="sxs-lookup"><span data-stu-id="53997-191">Now hello organization will have improved visibility tooexactly how many apps are using hello directory and what for.</span></span>
* <span data-ttu-id="53997-192">不需要系統管理導向的應用程式發佈/註冊程序。</span><span class="sxs-lookup"><span data-stu-id="53997-192">No need for admin driven app publishing/registration process.</span></span>  <span data-ttu-id="53997-193">Active Directory Federation Services 與可能的系統管理員必須 tooadd 應用程式做為信賴憑證者的合作對象代表開發人員。</span><span class="sxs-lookup"><span data-stu-id="53997-193">With Active Directory Federation Services it was likely that an admin had tooadd an app as a relying party on behalf of developers.</span></span>  <span data-ttu-id="53997-194">現在開發人員可以自助。</span><span class="sxs-lookup"><span data-stu-id="53997-194">Now developers can self-service.</span></span>
* <span data-ttu-id="53997-195">簽章在/總 tooapps 基於商業用途使用其組織帳戶的使用者是個好方法。</span><span class="sxs-lookup"><span data-stu-id="53997-195">Users signing in/up tooapps using their organization accounts for business purposes is a good thing.</span></span>  <span data-ttu-id="53997-196">如果後續離開 hello 組織，他們將會遺失存取 tootheir 帳戶 hello 應用程式正在使用中。</span><span class="sxs-lookup"><span data-stu-id="53997-196">If they subsequently leave hello organization they will lose access tootheir account in hello application they were using.</span></span>
* <span data-ttu-id="53997-197">記錄哪些資料與哪些應用程式共用是件好事。</span><span class="sxs-lookup"><span data-stu-id="53997-197">Having a record of what data was shared with which application is a good thing.</span></span>  <span data-ttu-id="53997-198">資料比以往更容易進行傳輸，且清楚記錄哪些人員與哪些應用程式共用哪些資料會很有用。</span><span class="sxs-lookup"><span data-stu-id="53997-198">Data is more transportable than ever and having a clear record of who shared what data with which applications is useful.</span></span>
* <span data-ttu-id="53997-199">使用 Azure AD 的 oAuth 應用程式決定完全權限，使用者可以 toogrant tooapplications 而哪些權限需要以系統管理員 tooagree。</span><span class="sxs-lookup"><span data-stu-id="53997-199">Apps who use Azure AD for oAuth decide exactly what permissions that users are able toogrant tooapplications and which permissions require an admin tooagree to.</span></span>  <span data-ttu-id="53997-200">您應該很指出只有系統管理員可以同意 toolarger 範圍和更重要的權限。</span><span class="sxs-lookup"><span data-stu-id="53997-200">It should go without saying that only admins can consent toolarger scopes and more significant permissions.</span></span>
* <span data-ttu-id="53997-201">加入並讓其資料是應用程式 tooaccess 稽核事件，讓您可以檢視內 hello Azure Managment 入口 toodetermine hello 稽核報告的使用者應用程式新增的方式 toohello 目錄。</span><span class="sxs-lookup"><span data-stu-id="53997-201">Users adding and allowing apps tooaccess their data are audited events so you can view hello Audit Reports within hello Azure Managment portal toodetermine how an app was added toohello directory.</span></span>

<span data-ttu-id="53997-202">**注意：** *Microsoft 本身已運作，現在有許多個月使用 hello 預設組態。*</span><span class="sxs-lookup"><span data-stu-id="53997-202">**Note:** *Microsoft itself has been operating using hello default configuration for many months now.*</span></span>

<span data-ttu-id="53997-203">與所有作業，稱為很可能 tooprevent 您目錄中使用者加入應用程式和執行自行決定對他們與應用程式中藉由修改 hello Azure 管理入口網站中的目錄設定共用哪些資訊。</span><span class="sxs-lookup"><span data-stu-id="53997-203">With all of that said it is possible tooprevent users in your directory from adding applications and from exercising discretion over what information they share with applications by modifying Directory configuration in hello Azure Management portal.</span></span>  <span data-ttu-id="53997-204">hello 下列設定可存取您目錄中的 「 設定 」 索引標籤上的 hello Azure 管理入口網站中。</span><span class="sxs-lookup"><span data-stu-id="53997-204">hello following configuration can be accessed within hello Azure Management portal on your Directory's "Configure" tab.</span></span>

![Hello UI 來設定整合式應用程式設定的螢幕擷取畫面][app_settings]

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="53997-206">後續步驟</span><span class="sxs-lookup"><span data-stu-id="53997-206">Next steps</span></span>
<span data-ttu-id="53997-207">深入了解如何 tooadd 應用程式 tooAzure AD 與 tooconfigure 如何服務應用程式。</span><span class="sxs-lookup"><span data-stu-id="53997-207">Learn more about how tooadd applications tooAzure AD and how tooconfigure services for apps.</span></span>

* <span data-ttu-id="53997-208">開發人員：[深入了解如何 toointegrate aad 應用程式](https://msdn.microsoft.com/library/azure/dn151122.aspx)</span><span class="sxs-lookup"><span data-stu-id="53997-208">Developers: [Learn how toointegrate an application with AAD](https://msdn.microsoft.com/library/azure/dn151122.aspx)</span></span>
* <span data-ttu-id="53997-209">開發人員：[檢閱在 GitHub 上與 Azure Active Directory 整合的應用程式範例程式碼](https://github.com/AzureADSamples)</span><span class="sxs-lookup"><span data-stu-id="53997-209">Developers: [Review sample code for apps integrated with Azure Active Directory on GitHub](https://github.com/AzureADSamples)</span></span>
* <span data-ttu-id="53997-210">開發人員和 IT 專業人員：[檢閱 hello hello Azure Active Directory Graph API 的 REST API 文件集](https://msdn.microsoft.com/library/azure/hh974478.aspx)</span><span class="sxs-lookup"><span data-stu-id="53997-210">Developers and IT Pros: [Review hello REST API documentation for hello Azure Active Directory Graph API](https://msdn.microsoft.com/library/azure/hh974478.aspx)</span></span>
* <span data-ttu-id="53997-211">IT 專業人員：[深入了解如何 toouse Azure Active Directory 預先整合應用程式從 hello 應用程式庫](https://msdn.microsoft.com/library/azure/dn308590.aspx)</span><span class="sxs-lookup"><span data-stu-id="53997-211">IT Pros: [Learn how toouse Azure Active Directory pre-integrated applications from hello App Gallery](https://msdn.microsoft.com/library/azure/dn308590.aspx)</span></span>
* <span data-ttu-id="53997-212">IT 專業人員： [尋找設定特定預先整合應用程式的教學課程](https://msdn.microsoft.com/library/azure/dn893637.aspx)</span><span class="sxs-lookup"><span data-stu-id="53997-212">IT Pros: [Find tutorials for configuring specific pre-integrated apps](https://msdn.microsoft.com/library/azure/dn893637.aspx)</span></span>
* <span data-ttu-id="53997-213">IT 專業人員：[深入了解如何使用應用程式的 toopublish hello Azure Active Directory 應用程式 Proxy](https://msdn.microsoft.com/library/azure/dn768219.aspx)</span><span class="sxs-lookup"><span data-stu-id="53997-213">IT Pros: [Learn how toopublish an app using hello Azure Active Directory Application Proxy](https://msdn.microsoft.com/library/azure/dn768219.aspx)</span></span>

## <a name="see-also"></a><span data-ttu-id="53997-214">另請參閱</span><span class="sxs-lookup"><span data-stu-id="53997-214">See also</span></span>
* [<span data-ttu-id="53997-215">Article Index for Application Management in Azure Active Directory (Azure Active Directory 中應用程式管理的文件索引)</span><span class="sxs-lookup"><span data-stu-id="53997-215">Article Index for Application Management in Azure Active Directory</span></span>](../active-directory-apps-index.md)

<!--Image references-->
[apps_service_principals_directory]:../media/active-directory-how-applications-are-added/HowAppsAreAddedToAAD.jpg
[app_settings]:../media/active-directory-how-applications-are-added/IntegratedAppSettings.jpg
