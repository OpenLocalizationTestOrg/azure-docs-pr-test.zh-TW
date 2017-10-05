---
title: "將應用程式加入至 Azure Active Directory 的方式"
description: "本文將說明如何將應用程式加入至 Azure Active Directory 的執行個體。"
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
ms.openlocfilehash: 6ffcfcb7ed071a12b0b3495ad534fd00f6d6ad99
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-and-why-applications-are-added-to-azure-ad"></a><span data-ttu-id="b010c-103">將應用程式加入至 Azure AD 的方式和原因</span><span class="sxs-lookup"><span data-stu-id="b010c-103">How and why applications are added to Azure AD</span></span>
<span data-ttu-id="b010c-104">在 Azure Active Directory 的執行個體中檢視應用程式清單時，最初令人感到困惑的其中一件事情是了解應用程式的來源以及其存在目的。</span><span class="sxs-lookup"><span data-stu-id="b010c-104">One of the initially puzzling things when viewing a list of applications in your instance of Azure Active Directory is understanding where the applications came from and why they are there.</span></span>  <span data-ttu-id="b010c-105">本文將提供應用程式如何在目錄中呈現的高階概觀，並提供內容來協助您了解應用程式如何出現在您的目錄中。</span><span class="sxs-lookup"><span data-stu-id="b010c-105">This article will provide a high level overview of how applications are represented in the directory and provide you with context that will assist you in understanding how an application came to be in your directory.</span></span>

## <a name="what-services-does-azure-ad-provide-to-applications"></a><span data-ttu-id="b010c-106">Azure AD 對應用程式提供哪些服務？</span><span class="sxs-lookup"><span data-stu-id="b010c-106">What services does Azure AD provide to applications?</span></span>
<span data-ttu-id="b010c-107">將應用程式加入至 Azure AD，即可利用一或多個其所提供的服務。</span><span class="sxs-lookup"><span data-stu-id="b010c-107">Applications are added to Azure AD to leverage one or more of the services it provides.</span></span>  <span data-ttu-id="b010c-108">這些服務包括：</span><span class="sxs-lookup"><span data-stu-id="b010c-108">Those services include:</span></span>

* <span data-ttu-id="b010c-109">應用程式驗證與授權</span><span class="sxs-lookup"><span data-stu-id="b010c-109">App authentication and authorization</span></span>
* <span data-ttu-id="b010c-110">使用者驗證與授權</span><span class="sxs-lookup"><span data-stu-id="b010c-110">User authentication & authorization</span></span>
* <span data-ttu-id="b010c-111">使用同盟或密碼的單一登入 (SSO)</span><span class="sxs-lookup"><span data-stu-id="b010c-111">Single sign-on (SSO) using federation or password</span></span>
* <span data-ttu-id="b010c-112">使用者佈建與同步處理</span><span class="sxs-lookup"><span data-stu-id="b010c-112">User provisioning & synchronization</span></span>
* <span data-ttu-id="b010c-113">角色型存取控制。使用目錄來定義應用程式角色，才能在應用程式中執行角色型授權檢查。</span><span class="sxs-lookup"><span data-stu-id="b010c-113">Role-based access control; Use the directory to define application roles to perform roles based authorization checks in an app.</span></span>
* <span data-ttu-id="b010c-114">oAuth 授權服務 (Office 365 和其他 Microsoft 應用程式會用它來授與對 API/資源的存取權限)。</span><span class="sxs-lookup"><span data-stu-id="b010c-114">oAuth authorization services (used by Office 365 and other Microsoft apps to authorize access to APIs/resources.)</span></span>
* <span data-ttu-id="b010c-115">應用程式發佈與 Proxy。將應用程式從私人網路發佈到網際網路</span><span class="sxs-lookup"><span data-stu-id="b010c-115">Application publishing & proxy; Publish an app from a private network to the internet</span></span>

## <a name="how-are-applications-represented-in-the-directory"></a><span data-ttu-id="b010c-116">目錄中呈現應用程式的方式？</span><span class="sxs-lookup"><span data-stu-id="b010c-116">How are applications represented in the directory?</span></span>
<span data-ttu-id="b010c-117">在 Azure AD 中，應用程式會透過 2 種物件呈現：應用程式物件和服務主體物件。</span><span class="sxs-lookup"><span data-stu-id="b010c-117">Applications are represented in the Azure AD using 2 objects: an application object and a service principal object.</span></span>  <span data-ttu-id="b010c-118">在「家用」/「擁有者」或「發佈」目錄下註冊的一個應用程式物件，和在其運作的每個目錄中代表應用程式的一個或多個服務主體物件。</span><span class="sxs-lookup"><span data-stu-id="b010c-118">There is one application object, registered in a "home"/"owner" or "publishing" directory and one or more service principal objects representing the application in every directory in which it acts.</span></span>  

<span data-ttu-id="b010c-119">應用程式物件說明該應用程式與 Azure AD (多租用戶服務) 之間的關係，而且可能包含下列任何項目：(注意：這不是完整清單。)</span><span class="sxs-lookup"><span data-stu-id="b010c-119">The application object describes the app to Azure AD (the multi-tenant service) and may include any of the following: (*Note*: This is not an exhaustive list.)</span></span>

* <span data-ttu-id="b010c-120">名稱、標誌和發行者</span><span class="sxs-lookup"><span data-stu-id="b010c-120">Name, Logo & Publisher</span></span>
* <span data-ttu-id="b010c-121">密碼 (用來驗證應用程式的對稱和/或非對稱金鑰)</span><span class="sxs-lookup"><span data-stu-id="b010c-121">Secrets (symmetric and/or asymmetric keys used to authenticate the app)</span></span>
* <span data-ttu-id="b010c-122">API 相依性 (oAuth)</span><span class="sxs-lookup"><span data-stu-id="b010c-122">API dependencies (oAuth)</span></span>
* <span data-ttu-id="b010c-123">API/資源/發佈範圍 (oAuth)</span><span class="sxs-lookup"><span data-stu-id="b010c-123">APIs/resources/scopes published (oAuth)</span></span>
* <span data-ttu-id="b010c-124">應用程式角色 (RBAC)</span><span class="sxs-lookup"><span data-stu-id="b010c-124">App roles (RBAC)</span></span>
* <span data-ttu-id="b010c-125">SSO 中繼資料和組態 (SSO)</span><span class="sxs-lookup"><span data-stu-id="b010c-125">SSO metadata and configuration (SSO)</span></span>
* <span data-ttu-id="b010c-126">使用者佈建中繼資料和組態</span><span class="sxs-lookup"><span data-stu-id="b010c-126">User provisioning metadata and configuration</span></span>
* <span data-ttu-id="b010c-127">Proxy 中繼資料和組態</span><span class="sxs-lookup"><span data-stu-id="b010c-127">Proxy metadata and configuration</span></span>

<span data-ttu-id="b010c-128">在每個應用程式運作的目錄中 (包括其主目錄)，服務主體會是應用程式的記錄。</span><span class="sxs-lookup"><span data-stu-id="b010c-128">The service principal is a record of the application in every directory, where the application acts including its home directory.</span></span>  <span data-ttu-id="b010c-129">服務主體：</span><span class="sxs-lookup"><span data-stu-id="b010c-129">The service principal:</span></span>

* <span data-ttu-id="b010c-130">透過應用程式識別碼屬性參考回至應用程式物件</span><span class="sxs-lookup"><span data-stu-id="b010c-130">Refers back to an application object via the app id property</span></span>
* <span data-ttu-id="b010c-131">記錄本機使用者和群組應用程式角色指派</span><span class="sxs-lookup"><span data-stu-id="b010c-131">Records local user and group app-role assignments</span></span>
* <span data-ttu-id="b010c-132">記錄本機使用者和授與應用程式的系統管理員權限</span><span class="sxs-lookup"><span data-stu-id="b010c-132">Records local user and admin permissions granted to the app</span></span>
  * <span data-ttu-id="b010c-133">例如：應用程式存取特定使用者電子郵件的權限</span><span class="sxs-lookup"><span data-stu-id="b010c-133">For example: permission for the app to access a particular users email</span></span>
* <span data-ttu-id="b010c-134">記錄本機原則，包括條件式存取原則</span><span class="sxs-lookup"><span data-stu-id="b010c-134">Records local policies including conditional access policy</span></span>
* <span data-ttu-id="b010c-135">記錄應用程式的本機替代本機設定</span><span class="sxs-lookup"><span data-stu-id="b010c-135">Records local alternate local settings for an app</span></span>
  * <span data-ttu-id="b010c-136">宣告轉換規則</span><span class="sxs-lookup"><span data-stu-id="b010c-136">Claims transformation rules</span></span>
  * <span data-ttu-id="b010c-137">屬性對應 (使用者佈建)</span><span class="sxs-lookup"><span data-stu-id="b010c-137">Attribute mappings (User provisioning)</span></span>
  * <span data-ttu-id="b010c-138">租用戶特定應用程式角色 (如果應用程式支援自訂角色)</span><span class="sxs-lookup"><span data-stu-id="b010c-138">Tenant specific app roles (if the app supports custom roles)</span></span>
  * <span data-ttu-id="b010c-139">名稱/標誌</span><span class="sxs-lookup"><span data-stu-id="b010c-139">Name/Logo</span></span>

### <a name="a-diagram-of-application-objects-and-service-principals-across-directories"></a><span data-ttu-id="b010c-140">目錄間的應用程式物件和服務主體圖表</span><span class="sxs-lookup"><span data-stu-id="b010c-140">A diagram of application objects and service principals across directories</span></span>
![說明應用程式物件和服務主體如何與現有 Azure AD 執行個體共存的圖表。][apps_service_principals_directory]

<span data-ttu-id="b010c-142">從以上圖表可以清楚得知。</span><span class="sxs-lookup"><span data-stu-id="b010c-142">As you can see from the diagram above.</span></span>  <span data-ttu-id="b010c-143">Microsoft 會在內部 (左側) 維護兩個它用來發佈應用程式的目錄。</span><span class="sxs-lookup"><span data-stu-id="b010c-143">Microsoft maintains two directories internally (on the left) it uses to publish applications.</span></span>

* <span data-ttu-id="b010c-144">一個用於 Microsoft 應用程式 (Microsoft 服務目錄)</span><span class="sxs-lookup"><span data-stu-id="b010c-144">One for Microsoft Apps (Microsoft services directory)</span></span>
* <span data-ttu-id="b010c-145">一個用於預先整合的協力廠商應用程式 (應用程式庫目錄)</span><span class="sxs-lookup"><span data-stu-id="b010c-145">One for pre-integrated 3rd Party Apps (App Gallery directory)</span></span>

<span data-ttu-id="b010c-146">與 Azure AD 整合的應用程式發行者/供應商必須具有發佈目錄。</span><span class="sxs-lookup"><span data-stu-id="b010c-146">Application publishers/vendors who integrate with Azure AD are required to have a publishing directory.</span></span>  <span data-ttu-id="b010c-147">(某些 SAAS 目錄)。</span><span class="sxs-lookup"><span data-stu-id="b010c-147">(Some SAAS Directory).</span></span>

<span data-ttu-id="b010c-148">自行新增的應用程式包括：</span><span class="sxs-lookup"><span data-stu-id="b010c-148">Applications that you add yourself include:</span></span>

* <span data-ttu-id="b010c-149">自行開發的應用程式 (與 AAD 整合)</span><span class="sxs-lookup"><span data-stu-id="b010c-149">Apps you developed (integrated with AAD)</span></span>
* <span data-ttu-id="b010c-150">為單一登入而進行連線的應用程式</span><span class="sxs-lookup"><span data-stu-id="b010c-150">Apps you connected for single-sign-on</span></span>
* <span data-ttu-id="b010c-151">使用 Azure AD 應用程式 Proxy 發佈的應用程式。</span><span class="sxs-lookup"><span data-stu-id="b010c-151">Apps you published using the Azure AD application proxy.</span></span>

### <a name="a-couple-of-notes-and-exceptions"></a><span data-ttu-id="b010c-152">幾個附註和例外狀況</span><span class="sxs-lookup"><span data-stu-id="b010c-152">A couple of notes and exceptions</span></span>
* <span data-ttu-id="b010c-153">並非所有的服務主體都會指回應用程式物件。</span><span class="sxs-lookup"><span data-stu-id="b010c-153">Not all service principals point back to application objects.</span></span>  <span data-ttu-id="b010c-154">是嗎？</span><span class="sxs-lookup"><span data-stu-id="b010c-154">Huh?</span></span> <span data-ttu-id="b010c-155">原先建置 Azure AD 時提供給應用程式的服務受到更多的限制，而且服務主體足以建立應用程式身分識別。</span><span class="sxs-lookup"><span data-stu-id="b010c-155">When Azure AD was originally built the services provided to applications were much more limited and the service principal was sufficient for establishing an app identity.</span></span>  <span data-ttu-id="b010c-156">原先服務主體的功能狀況接近 Windows Server Active Directory 服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="b010c-156">The original service principal was closer in shape to the Windows Server Active Directory service account.</span></span>  <span data-ttu-id="b010c-157">基於這個原因，您還是可以使用 Azure AD PowerShell 來建立服務主體，而無需先建立應用程式物件。</span><span class="sxs-lookup"><span data-stu-id="b010c-157">For this reason it's still possible to create service principals using the Azure AD PowerShell without first creating an application object.</span></span>  <span data-ttu-id="b010c-158">Graph API 需要應用程式物件才能建立服務主體。</span><span class="sxs-lookup"><span data-stu-id="b010c-158">The Graph API requires an app object before creating a service principal.</span></span>
* <span data-ttu-id="b010c-159">並非所有上述資訊目前都處於以程式設計方式公開的狀態。</span><span class="sxs-lookup"><span data-stu-id="b010c-159">Not all of the information described above is currently exposed programmatically.</span></span>  <span data-ttu-id="b010c-160">以下功能僅適用於 UI：</span><span class="sxs-lookup"><span data-stu-id="b010c-160">The following are only available in the UI:</span></span>
  * <span data-ttu-id="b010c-161">宣告轉換規則</span><span class="sxs-lookup"><span data-stu-id="b010c-161">Claims transformation rules</span></span>
  * <span data-ttu-id="b010c-162">屬性對應 (使用者佈建)</span><span class="sxs-lookup"><span data-stu-id="b010c-162">Attribute mappings (User provisioning)</span></span>
* <span data-ttu-id="b010c-163">如需服務主體與應用程式物件的詳細資訊，請參閱 Azure AD Graph REST API 參考文件。</span><span class="sxs-lookup"><span data-stu-id="b010c-163">For more detailed information on the service principal and application objects please refer to the Azure AD Graph REST API reference documentation.</span></span>  <span data-ttu-id="b010c-164">*提示*：目前可用的 Azure AD 結構描述參考中，Azure AD Graph API 文件是最有用的資源。</span><span class="sxs-lookup"><span data-stu-id="b010c-164">*Hint*: The Azure AD Graph API documentation is the closest thing to a schema reference for Azure AD that's currently available.</span></span>  
  * [<span data-ttu-id="b010c-165">應用程式</span><span class="sxs-lookup"><span data-stu-id="b010c-165">Application</span></span>](https://msdn.microsoft.com/library/azure/dn151677.aspx)
  * [<span data-ttu-id="b010c-166">服務主體</span><span class="sxs-lookup"><span data-stu-id="b010c-166">Service Principal</span></span>](https://msdn.microsoft.com/library/azure/dn194452.aspx)

## <a name="how-are-apps-added-to-my-azure-ad-instance"></a><span data-ttu-id="b010c-167">如何將應用程式加入 Azure AD 執行個體？</span><span class="sxs-lookup"><span data-stu-id="b010c-167">How are apps added to my Azure AD instance?</span></span>
<span data-ttu-id="b010c-168">有很多方式可以將應用程式加入 Azure AD：</span><span class="sxs-lookup"><span data-stu-id="b010c-168">There are many ways an app can be added to Azure AD:</span></span>

* <span data-ttu-id="b010c-169">從 [Azure Active Directory 應用程式庫](https://azure.microsoft.com/updates/azure-active-directory-over-1000-apps/)</span><span class="sxs-lookup"><span data-stu-id="b010c-169">Add an app from the [Azure Active Directory App Gallery](https://azure.microsoft.com/updates/azure-active-directory-over-1000-apps/)</span></span>
* <span data-ttu-id="b010c-170">註冊/登入與 Azure Active Directory 整合的協力廠商應用程式 (例如：[Smartsheet](https://app.smartsheet.com/b/home) 或 [DocuSign](https://www.docusign.net/member/MemberLogin.aspx))</span><span class="sxs-lookup"><span data-stu-id="b010c-170">Sign up/into a 3rd Party App integrated with Azure Active Directory (For example: [Smartsheet](https://app.smartsheet.com/b/home) or [DocuSign](https://www.docusign.net/member/MemberLogin.aspx))</span></span>
  * <span data-ttu-id="b010c-171">註冊/登入期間，系統會要求使用者提供應用程式的存取權限，才能存取其設定檔及其他權限。</span><span class="sxs-lookup"><span data-stu-id="b010c-171">During sign up/in users are asked to give permission to the app to access their profile and other permissions.</span></span>  <span data-ttu-id="b010c-172">做出同意動作的第一個人會造成代表應用程式的服務主體被新增至目錄。</span><span class="sxs-lookup"><span data-stu-id="b010c-172">The first person to give consent causes a service principal representing the app to be added to the directory.</span></span>
* <span data-ttu-id="b010c-173">註冊/登入 Microsoft 線上服務 (如 [Office 365](http://products.office.com/)</span><span class="sxs-lookup"><span data-stu-id="b010c-173">Sign up/into Microsoft online services like [Office 365](http://products.office.com/)</span></span>
  * <span data-ttu-id="b010c-174">訂閱或開始試用 Office 365 時，目錄中會建立一或多個服務主體，代表用來傳遞所有 Office 365 相關功能的各種服務。</span><span class="sxs-lookup"><span data-stu-id="b010c-174">When you subscribe to Office 365 or begin a trial one or more service principals are created in the directory representing the various services that are used to deliver all of the functionality associated with Office 365.</span></span>
  * <span data-ttu-id="b010c-175">某些 Office 365 服務(如 SharePoint) 會持續建立服務主體，以允許元件之間的安全通訊，包括工作流程。</span><span class="sxs-lookup"><span data-stu-id="b010c-175">Some Office 365 services like SharePoint create service principals on an on-going basis to allow secure communication between components including workflows.</span></span>
* <span data-ttu-id="b010c-176">在「Azure 管理入口網站」中新增您正在開發的應用程式，請參閱：https://msdn.microsoft.com/library/azure/dn132599.aspx</span><span class="sxs-lookup"><span data-stu-id="b010c-176">Add an app you're developing in the Azure Management Portal see: https://msdn.microsoft.com/library/azure/dn132599.aspx</span></span>
* <span data-ttu-id="b010c-177">新增您使用 Visual Studio 開發的應用程式，請參閱：</span><span class="sxs-lookup"><span data-stu-id="b010c-177">Add an app you're developing using Visual Studio see:</span></span>
  * [<span data-ttu-id="b010c-178">ASP.Net 驗證方法</span><span class="sxs-lookup"><span data-stu-id="b010c-178">ASP.Net Authentication Methods</span></span>](http://www.asp.net/visual-studio/overview/2013/creating-web-projects-in-visual-studio#orgauthoptions)
  * [<span data-ttu-id="b010c-179">連接的服務</span><span class="sxs-lookup"><span data-stu-id="b010c-179">Connected Services</span></span>](http://blogs.msdn.com/b/visualstudio/archive/2014/11/19/connecting-to-cloud-services.aspx)
* <span data-ttu-id="b010c-180">新增應用程式來使用 [Azure AD 應用程式 Proxy](https://msdn.microsoft.com/library/azure/dn768219.aspx)</span><span class="sxs-lookup"><span data-stu-id="b010c-180">Add an app to use to use the [Azure AD Application Proxy](https://msdn.microsoft.com/library/azure/dn768219.aspx)</span></span>
* <span data-ttu-id="b010c-181">連接應用程式進行使用 SAML 或密碼 SSO 的單一登入</span><span class="sxs-lookup"><span data-stu-id="b010c-181">Connect an app for single sign on using SAML or Password SSO</span></span>
* <span data-ttu-id="b010c-182">許多其他項目，包括在 Azure 中的各種開發人員經驗和/在跨開發人員中心的 API 總管體驗</span><span class="sxs-lookup"><span data-stu-id="b010c-182">Many others including various developer experiences in Azure and/in API explorer experiences across developer centers</span></span>

## <a name="who-has-permission-to-add-applications-to-my-azure-ad-instance"></a><span data-ttu-id="b010c-183">誰有權將應用程式加入我的 Azure AD 執行個體？</span><span class="sxs-lookup"><span data-stu-id="b010c-183">Who has permission to add applications to my Azure AD instance?</span></span>
<span data-ttu-id="b010c-184">只有全域系統管理員可以：</span><span class="sxs-lookup"><span data-stu-id="b010c-184">Only global administrators can:</span></span>

* <span data-ttu-id="b010c-185">從 Azure AD 應用程式庫 (預先整合的協力廠商應用程式) 新增應用程式</span><span class="sxs-lookup"><span data-stu-id="b010c-185">Add apps from the Azure AD app gallery (pre-integrated 3rd Party Apps)</span></span>
* <span data-ttu-id="b010c-186">使用 Azure AD 應用程式 Proxy 來發佈應用程式</span><span class="sxs-lookup"><span data-stu-id="b010c-186">Publish an app using the Azure AD Application Proxy</span></span>

<span data-ttu-id="b010c-187">您目錄中的所有使用者都有權新增其所開發的應用程式，並自行決定要共用哪些應用程式，以及提供哪些應用程式存取其組織資料的權限。</span><span class="sxs-lookup"><span data-stu-id="b010c-187">All users in your directory have rights to add applications that they are developing and discretion over which applications they share/give access to their organizational data.</span></span>  <span data-ttu-id="b010c-188">*請記住，使用者註冊/登入應用程式和授與權限可能會導致系統建立服務主體。*</span><span class="sxs-lookup"><span data-stu-id="b010c-188">*Remember user sign up/in to an app and granting permissions may result in a service principal being created.*</span></span>

<span data-ttu-id="b010c-189">剛聽到時您可能會有些疑慮，但請記住下列要點：</span><span class="sxs-lookup"><span data-stu-id="b010c-189">This might initially sound concerning, but keep the following in mind:</span></span>

* <span data-ttu-id="b010c-190">在無需在目錄中註冊/記錄應用程式的情況下，應用程式能夠利用 Windows Server Active Directory 進行使用者驗證已有數年的時間。</span><span class="sxs-lookup"><span data-stu-id="b010c-190">Apps have been able to leverage Windows Server Active Directory for user authentication for many years without requiring the application to be registered/recorded in the directory.</span></span>  <span data-ttu-id="b010c-191">現在組織已提高可見度，您可以知道究竟有多少個應用程式正在使用目錄以及使用目的為何。</span><span class="sxs-lookup"><span data-stu-id="b010c-191">Now the organization will have improved visibility to exactly how many apps are using the directory and what for.</span></span>
* <span data-ttu-id="b010c-192">不需要系統管理導向的應用程式發佈/註冊程序。</span><span class="sxs-lookup"><span data-stu-id="b010c-192">No need for admin driven app publishing/registration process.</span></span>  <span data-ttu-id="b010c-193">有了 Active Directory Federation Services，系統管理員很有可能必須代表開發人員，將應用程式新增為信賴憑證者。</span><span class="sxs-lookup"><span data-stu-id="b010c-193">With Active Directory Federation Services it was likely that an admin had to add an app as a relying party on behalf of developers.</span></span>  <span data-ttu-id="b010c-194">現在開發人員可以自助。</span><span class="sxs-lookup"><span data-stu-id="b010c-194">Now developers can self-service.</span></span>
* <span data-ttu-id="b010c-195">基於商業用途，使用者使用其組織帳戶登入/註冊應用程式是件好事。</span><span class="sxs-lookup"><span data-stu-id="b010c-195">Users signing in/up to apps using their organization accounts for business purposes is a good thing.</span></span>  <span data-ttu-id="b010c-196">如果使用者之後離開組織，他們將無法在先前所使用的應用程式中存取帳戶。</span><span class="sxs-lookup"><span data-stu-id="b010c-196">If they subsequently leave the organization they will lose access to their account in the application they were using.</span></span>
* <span data-ttu-id="b010c-197">記錄哪些資料與哪些應用程式共用是件好事。</span><span class="sxs-lookup"><span data-stu-id="b010c-197">Having a record of what data was shared with which application is a good thing.</span></span>  <span data-ttu-id="b010c-198">資料比以往更容易進行傳輸，且清楚記錄哪些人員與哪些應用程式共用哪些資料會很有用。</span><span class="sxs-lookup"><span data-stu-id="b010c-198">Data is more transportable than ever and having a clear record of who shared what data with which applications is useful.</span></span>
* <span data-ttu-id="b010c-199">使用 Azure AD for oAuth 的應用程式可確切決定使用者可以授與應用程式哪些權限，以及哪些權限需要系統管理員的同意。</span><span class="sxs-lookup"><span data-stu-id="b010c-199">Apps who use Azure AD for oAuth decide exactly what permissions that users are able to grant to applications and which permissions require an admin to agree to.</span></span>  <span data-ttu-id="b010c-200">不言而喻，唯有系統管理員可以同意較大範圍且更重要的權限。</span><span class="sxs-lookup"><span data-stu-id="b010c-200">It should go without saying that only admins can consent to larger scopes and more significant permissions.</span></span>
* <span data-ttu-id="b010c-201">新增使用者和允許應用程式存取其資料屬於稽核事件，可讓您在 Azure 管理入口網站中檢視稽核報告，進而決定將應用程式加入目錄的方式。</span><span class="sxs-lookup"><span data-stu-id="b010c-201">Users adding and allowing apps to access their data are audited events so you can view the Audit Reports within the Azure Managment portal to determine how an app was added to the directory.</span></span>

<span data-ttu-id="b010c-202">**附註：** *Microsoft 本身使用預設組態進行運作已有幾個月的時間了。*</span><span class="sxs-lookup"><span data-stu-id="b010c-202">**Note:** *Microsoft itself has been operating using the default configuration for many months now.*</span></span>

<span data-ttu-id="b010c-203">說了這麼多，您可能可以防止使用者在目錄中新增應用程式，以及在對與應用程式共用哪些資訊上行使同意權，方法是修改 Azure 管理入口網站中的目錄組態。</span><span class="sxs-lookup"><span data-stu-id="b010c-203">With all of that said it is possible to prevent users in your directory from adding applications and from exercising discretion over what information they share with applications by modifying Directory configuration in the Azure Management portal.</span></span>  <span data-ttu-id="b010c-204">在 Azure 管理入口網站中，您可以在目錄的 [設定] 索引標籤上存取下列組態。</span><span class="sxs-lookup"><span data-stu-id="b010c-204">The following configuration can be accessed within the Azure Management portal on your Directory's "Configure" tab.</span></span>

![進行整合式應用程式設定的 UI 螢幕擷取畫面][app_settings]

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="b010c-206">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b010c-206">Next steps</span></span>
<span data-ttu-id="b010c-207">深入了解如何將應用程式加入 Azure AD，以及如何設定應用程式的服務。</span><span class="sxs-lookup"><span data-stu-id="b010c-207">Learn more about how to add applications to Azure AD and how to configure services for apps.</span></span>

* <span data-ttu-id="b010c-208">開發人員： [了解如何整合應用程式與 AAD](https://msdn.microsoft.com/library/azure/dn151122.aspx)</span><span class="sxs-lookup"><span data-stu-id="b010c-208">Developers: [Learn how to integrate an application with AAD](https://msdn.microsoft.com/library/azure/dn151122.aspx)</span></span>
* <span data-ttu-id="b010c-209">開發人員：[檢閱在 GitHub 上與 Azure Active Directory 整合的應用程式範例程式碼](https://github.com/AzureADSamples)</span><span class="sxs-lookup"><span data-stu-id="b010c-209">Developers: [Review sample code for apps integrated with Azure Active Directory on GitHub](https://github.com/AzureADSamples)</span></span>
* <span data-ttu-id="b010c-210">開發人員和 IT 專業人員： [檢閱 Azure Active Directory Graph API 的 REST API 文件](https://msdn.microsoft.com/library/azure/hh974478.aspx)</span><span class="sxs-lookup"><span data-stu-id="b010c-210">Developers and IT Pros: [Review the REST API documentation for the Azure Active Directory Graph API](https://msdn.microsoft.com/library/azure/hh974478.aspx)</span></span>
* <span data-ttu-id="b010c-211">IT 專業人員： [了解如何使用應用程式庫的 Azure Active Directory 預先整合應用程式](https://msdn.microsoft.com/library/azure/dn308590.aspx)</span><span class="sxs-lookup"><span data-stu-id="b010c-211">IT Pros: [Learn how to use Azure Active Directory pre-integrated applications from the App Gallery](https://msdn.microsoft.com/library/azure/dn308590.aspx)</span></span>
* <span data-ttu-id="b010c-212">IT 專業人員： [尋找設定特定預先整合應用程式的教學課程](https://msdn.microsoft.com/library/azure/dn893637.aspx)</span><span class="sxs-lookup"><span data-stu-id="b010c-212">IT Pros: [Find tutorials for configuring specific pre-integrated apps](https://msdn.microsoft.com/library/azure/dn893637.aspx)</span></span>
* <span data-ttu-id="b010c-213">IT 專業人員： [了解如何使用 Azure Active Directory 應用程式 Proxy 發佈應用程式](https://msdn.microsoft.com/library/azure/dn768219.aspx)</span><span class="sxs-lookup"><span data-stu-id="b010c-213">IT Pros: [Learn how to publish an app using the Azure Active Directory Application Proxy](https://msdn.microsoft.com/library/azure/dn768219.aspx)</span></span>

## <a name="see-also"></a><span data-ttu-id="b010c-214">另請參閱</span><span class="sxs-lookup"><span data-stu-id="b010c-214">See also</span></span>
* [<span data-ttu-id="b010c-215">Article Index for Application Management in Azure Active Directory (Azure Active Directory 中應用程式管理的文件索引)</span><span class="sxs-lookup"><span data-stu-id="b010c-215">Article Index for Application Management in Azure Active Directory</span></span>](../active-directory-apps-index.md)

<!--Image references-->
[apps_service_principals_directory]:../media/active-directory-how-applications-are-added/HowAppsAreAddedToAAD.jpg
[app_settings]:../media/active-directory-how-applications-are-added/IntegratedAppSettings.jpg
