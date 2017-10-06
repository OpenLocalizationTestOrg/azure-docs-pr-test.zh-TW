---
title: "Azure Active Directory 中的應用程式、權限及同意 | Microsoft Docs"
description: "Azure AD Connect 會整合您的內部部署目錄與 Azure Active Directory。 這可讓您與 Azure AD 整合 Office 365、 Azure 和 SaaS 應用程式的通用識別身分的 tooprovide。"
keywords: "什麼是 Azure AD Connect，簡介 tooAzure AD，應用程式，安裝 active directory"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 25897cc4-7687-49b6-b0d5-71f51302b6b1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/31/2017
ms.author: billmath
ms.reviewer: jesakowi
ms.custom: oldportal;it-pro;
ms.openlocfilehash: af0c2669199736fdb41e85876a7e3a7064e80770
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="apps-permissions-and-consent-in-azure-active-directory"></a><span data-ttu-id="27796-105">Azure Active Directory 中的應用程式、權限及同意</span><span class="sxs-lookup"><span data-stu-id="27796-105">Apps, permissions, and consent in Azure Active Directory</span></span>
<span data-ttu-id="27796-106">Azure Active directory，您可以新增應用程式 tooyour 目錄。</span><span class="sxs-lookup"><span data-stu-id="27796-106">Within Azure Active Directory, you can add applications tooyour directory.</span></span>  <span data-ttu-id="27796-107">hello 應用程式的應用程式的 hello 類型而有所不同。</span><span class="sxs-lookup"><span data-stu-id="27796-107">hello applications can vary depending on hello type of application.</span></span>  <span data-ttu-id="27796-108">tooview hello 傳統入口網站中的應用程式選取目錄，然後選擇 [應用程式。</span><span class="sxs-lookup"><span data-stu-id="27796-108">tooview applications in hello classic portal, select a directory and choose applications.</span></span>

![](media/active-directory-apps-permissions-consent/apps1.png)

> [!IMPORTANT]
> <span data-ttu-id="27796-109">Microsoft 建議您管理 Azure AD 使用 hello [Azure AD 系統管理中心](https://aad.portal.azure.com)hello 在 Azure 入口網站，而不是使用 hello 這個文件中參考的 Azure 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="27796-109">Microsoft recommends that you manage Azure AD using hello [Azure AD admin center](https://aad.portal.azure.com) in hello Azure portal instead of using hello Azure classic portal referenced in this article.</span></span>

## <a name="types-of-apps"></a><span data-ttu-id="27796-110">應用程式類型</span><span class="sxs-lookup"><span data-stu-id="27796-110">Types of apps</span></span>

1. <span data-ttu-id="27796-111">**單一租用戶應用程式**</span><span class="sxs-lookup"><span data-stu-id="27796-111">**Single-tenant apps**</span></span> </br>
    - <span data-ttu-id="27796-112">**單一租用戶應用程式**-通常稱為 tooas 的特定業務 (LOB) 應用程式。</span><span class="sxs-lookup"><span data-stu-id="27796-112">**Single-tenant apps** - Often referred tooas line-of-business (LOB) apps.</span></span> <span data-ttu-id="27796-113">這是您組織內其他人開發自己的應用程式，並希望使用者在 toohello 應用程式中的 hello 組織 toobe 無法 toosign hello 情況。</span><span class="sxs-lookup"><span data-stu-id="27796-113">This is hello case where someone within your organization develops their own app, and would like users in hello organization toobe able toosign in toohello app.</span></span>
    ![](media/active-directory-apps-permissions-consent/apps2.png)
    - <span data-ttu-id="27796-114">**應用程式 Proxy 應用程式**-時由內部部署應用程式與 Azure AD 應用程式 Proxy、 公開 （expose） 單一租用戶應用程式會在您的租用戶 （在加法 toohello 應用程式 Proxy 服務) 中註冊。</span><span class="sxs-lookup"><span data-stu-id="27796-114">**App Proxy apps** - When you expose an on-prem application with Azure AD App Proxy, a single-tenant app is registered in your tenant (in addition toohello App Proxy service).</span></span> <span data-ttu-id="27796-115">此應用程式便是代表所有雲端互動 (例如驗證) 之內部部署應用程式的項目 </span><span class="sxs-lookup"><span data-stu-id="27796-115">This app is what represents your on-prem application for all cloud interactions (for example, authentication).</span></span> <span data-ttu-id="27796-116">(應用程式 Proxy 需要 Azure AD Basic 或更高版本)。</span><span class="sxs-lookup"><span data-stu-id="27796-116">(App Proxy requires Azure AD Basic or higher.)</span></span>


2. <span data-ttu-id="27796-117">**多租用戶應用程式**</span><span class="sxs-lookup"><span data-stu-id="27796-117">**Multi-tenant apps**</span></span>
    - <span data-ttu-id="27796-118">**多租用戶應用程式的其他人可以同意**-類似太 「 單一租用戶應用程式，您的組織開發 」。</span><span class="sxs-lookup"><span data-stu-id="27796-118">**Multi-tenant apps which others can consent to** - similar too“single-tenant apps that your organization develops”.</span></span> <span data-ttu-id="27796-119">hello （除了 hello 應用程式本身中的 hello 邏輯） 的主要差異在於來自其他租用戶的使用者也可以同意 tooand toohello 應用程式中的符號。</span><span class="sxs-lookup"><span data-stu-id="27796-119">hello main difference (besides hello logic in hello app itself) is that users from other tenants can also consent tooand sign in toohello app.</span></span></br>
    ![](media/active-directory-apps-permissions-consent/apps4.png)
    - <span data-ttu-id="27796-120">**其他人開發、且 Contoso 可同意的多租用戶應用程式** </span><span class="sxs-lookup"><span data-stu-id="27796-120">**Multi-tenant apps others develop, which Contoso can consent to**.</span></span> <span data-ttu-id="27796-121">(或簡稱「已同意的應用程式」)。這是 「 您的組織開發多租用戶應用程式 」 的 hello 缺陷。</span><span class="sxs-lookup"><span data-stu-id="27796-121">(Or “consented apps”, for short.) This is hello flip side of “multi-tenant apps your organization develops”.</span></span> <span data-ttu-id="27796-122">另一個組織正在開發多租用戶應用程式時您組織的使用者可同意 toohello 應用程式，然後登入 tooit。</span><span class="sxs-lookup"><span data-stu-id="27796-122">When another organization develops a multi-tenant app, users of your organization can consent toohello app and sign in tooit.</span></span>
    - <span data-ttu-id="27796-123">**Microsoft 第一方應用程式** - 代表 Microsoft 服務的應用程式。</span><span class="sxs-lookup"><span data-stu-id="27796-123">**Microsoft first-party apps** - Apps that represent Microsoft services.</span></span> <span data-ttu-id="27796-124">您申請 hello 服務的 hello 事實有驅動同意。</span><span class="sxs-lookup"><span data-stu-id="27796-124">Consent is driven by hello fact that you sign up for hello service.</span></span> <span data-ttu-id="27796-125">有時候沒有特殊的 UX 和特定的第一方應用程式通常在建立原則，以存取 toohello 應用程式時所使用的邏輯。</span><span class="sxs-lookup"><span data-stu-id="27796-125">There is sometimes special UX and logic for certain first-party apps that is often used when establishing policies around access toohello app.</span></span></br>
    ![](media/active-directory-apps-permissions-consent/apps3.png)
    - <span data-ttu-id="27796-126">**預先整合應用程式**-應用程式用於 hello Azure AD App 資源庫，您可以加入 tooyour 目錄 tooprovide 單一登入 （和在某些情況下，佈建） toopopular SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="27796-126">**Pre-integrated apps** - Apps available in hello Azure AD App Gallery, which you can add tooyour directory tooprovide single sign-on (and in some cases, provisioning) toopopular SaaS apps.</span></span>
    - <span data-ttu-id="27796-127">**Azure AD 單一登入**：可透過 SAML 2.0 或 OpenID Connect 等受支援登入通訊協定來與 Azure AD 整合之應用程式的「真實」SSO。</span><span class="sxs-lookup"><span data-stu-id="27796-127">**Azure AD single sign-on**: “Real” SSO, for apps that can be integrated with Azure AD, through a supported sign-in protocol such as SAML 2.0 or OpenID Connect.</span></span> <span data-ttu-id="27796-128">hello 精靈將引導您完成設定。</span><span class="sxs-lookup"><span data-stu-id="27796-128">hello wizard walks you through setting it up.</span></span>
    - <span data-ttu-id="27796-129">**密碼單一登入**: Azure AD 會安全地儲存 hello 應用程式中，hello 使用者的認證和 hello 認證會 「 插入 」 hello 登入表單的 hello Azure AD 應用程式存取瀏覽器延伸模組。</span><span class="sxs-lookup"><span data-stu-id="27796-129">**Password single sign-on**: Azure AD securely stores hello user’s credentials for hello app, and hello credentials are “injected” into hello sign-in form by hello Azure AD App Access browser extension.</span></span> <span data-ttu-id="27796-130">也稱為「密碼儲存庫存」。</span><span class="sxs-lookup"><span data-stu-id="27796-130">Also known as “password vaulting”.</span></span>

## <a name="permissions"></a><span data-ttu-id="27796-131">權限</span><span class="sxs-lookup"><span data-stu-id="27796-131">Permissions</span></span>

<span data-ttu-id="27796-132">應用程式註冊時，執行 hello (也就是 hello developer) 的應用程式註冊的 hello 使用者定義的權限 hello 應用程式需要存取，以及哪些資源。</span><span class="sxs-lookup"><span data-stu-id="27796-132">When an app is registered, hello user performing hello app registration (that is, hello developer) defines which permissions hello app needs access to, and which resources.</span></span> <span data-ttu-id="27796-133">（hello 資源是，本身定義為其他應用程式）。例如，有人建置 mail 閱讀應用程式中，會說明其應用程式需要 hello 資源 「 Office 365 Exchange Online"hello"hello 登入的使用者身分存取信箱 」 權限：</span><span class="sxs-lookup"><span data-stu-id="27796-133">(hello resources are, themselves, defined as other apps.) For example, someone building a mail reader app, would state that their app requires hello “Access mailboxes as hello signed-in user” permission in hello “Office 365 Exchange Online” resource:</span></span>
    
![](media/active-directory-apps-permissions-consent/apps6.png)

<span data-ttu-id="27796-134">為了讓一個應用程式 （hello 用戶端） toorequest 從另一個應用程式 （hello 資源） 的特定權限，hello hello 資源應用程式的開發人員會定義存在的 hello 權限。</span><span class="sxs-lookup"><span data-stu-id="27796-134">In order for one app (hello client) toorequest a certain permission from another app (hello resource), hello developer of hello resource app defines hello permissions that exist.</span></span> <span data-ttu-id="27796-135">在本例中，Microsoft hello hello 「 Office 365 Exchange 連線 」 資源應用程式擁有者已定義名為 「 hello 登入的使用者身分存取信箱 」 權限。</span><span class="sxs-lookup"><span data-stu-id="27796-135">In our example, Microsoft, hello owner of hello “Office 365 Exchange Online” resource app, have defined a permission named “Access mailboxes as hello signed-in user”.</span></span>

<span data-ttu-id="27796-136">在定義的權限，hello 應用程式開發人員必須定義如果 hello 權限可以同意，或者是否需要獲得管理員同意。</span><span class="sxs-lookup"><span data-stu-id="27796-136">When defining permissions, hello app developer must define if hello permission can be consented to, or if it requires admin consent.</span></span> <span data-ttu-id="27796-137">這可讓開發人員 tooallow 使用者 tooconsent 上自己 tooapps 要求只低敏感度權限，但是需要系統管理員 tooconsent toomore 機密權限。</span><span class="sxs-lookup"><span data-stu-id="27796-137">This allows developers tooallow users tooconsent on their own tooapps requesting only low-sensitivity permissions, but require admins tooconsent toomore sensitive permissions.</span></span> <span data-ttu-id="27796-138">例如，hello"Azure Active Directory"資源應用程式，具有已定義，所以使用者可同意 tooapps，要求的有限的唯讀權限。</span><span class="sxs-lookup"><span data-stu-id="27796-138">For example, hello “Azure Active Directory” resource app, has been defined, so users can consent tooapps, requesting limited read-only permissions.</span></span>  <span data-ttu-id="27796-139">不過，行使系統管理員同意則需要完整讀取權限和所有寫入權限。</span><span class="sxs-lookup"><span data-stu-id="27796-139">However, admin consent is required for full read permissions, and all write permissions.</span></span>

<span data-ttu-id="27796-140">因為原生用戶端未經過驗證，因此定義為原生用戶端應用程式的應用程式只能要求委派的權限。</span><span class="sxs-lookup"><span data-stu-id="27796-140">Because native clients are not authenticated, an app defined as a native client app can only request delegated permissions.</span></span> <span data-ttu-id="27796-141">這表示在取得權杖時一律必須由實際使用者涉入。</span><span class="sxs-lookup"><span data-stu-id="27796-141">This means that there must always be an actual user involved when obtaining a token.</span></span> <span data-ttu-id="27796-142">在取得存取權杖時，Web 應用程式和 Web API (機密用戶端) 一律必須向 Azure AD 驗證。</span><span class="sxs-lookup"><span data-stu-id="27796-142">Web apps and web APIs (confidential clients), must always authenticate with Azure AD when getting an access token.</span></span> <span data-ttu-id="27796-143">這表示他們也擁有 hello 可能會要求僅限應用程式的權限。</span><span class="sxs-lookup"><span data-stu-id="27796-143">Meaning they also have hello possibility of requesting app-only permissions.</span></span> <span data-ttu-id="27796-144">例如，如果一個後端服務需要 tooauthenticate tooanother 後端服務。</span><span class="sxs-lookup"><span data-stu-id="27796-144">For example, if one back-end service needs tooauthenticate tooanother back-end service.</span></span> <span data-ttu-id="27796-145">要求僅限應用程式權限的應用程式一律需要系統管理員的同意。</span><span class="sxs-lookup"><span data-stu-id="27796-145">Applications requesting app-only permissions always require administrator consent.</span></span>

<span data-ttu-id="27796-146">摘要︰</span><span class="sxs-lookup"><span data-stu-id="27796-146">Summarizing:</span></span>



- <span data-ttu-id="27796-147">（用戶端） 的應用程式狀態 （資源） 的其他應用程式所需要的 hello 權限。</span><span class="sxs-lookup"><span data-stu-id="27796-147">An app (client) states hello permissions it needs for other apps (resources).</span></span>
- <span data-ttu-id="27796-148">（資源） 的應用程式狀態時公開的 tooother 應用程式 （用戶端） 的權限。</span><span class="sxs-lookup"><span data-stu-id="27796-148">An app (resource) states what permissions are exposed tooother apps (clients).</span></span>
- <span data-ttu-id="27796-149">權限可以是僅限應用程式權限或委派的權限。</span><span class="sxs-lookup"><span data-stu-id="27796-149">A permission can be an app-only permission, or a delegated permission.</span></span>
- <span data-ttu-id="27796-150">委派的權限可以標示為「允許使用者同意」或「需要系統管理員同意」。</span><span class="sxs-lookup"><span data-stu-id="27796-150">A delegated permission can be marked as “allows user consent”, or “requires admin consent”.</span></span>
- <span data-ttu-id="27796-151">應用程式的行為會為用戶端 （藉由宣告它需要權限 tooa 資源），做為資源 （藉由宣告它所公開的權限），或兩者。</span><span class="sxs-lookup"><span data-stu-id="27796-151">An app can behave as a client (by declaring that it needs permissions tooa resource), as a resource (by declaring which permissions it exposes), or as both.</span></span>

## <a name="controls"></a><span data-ttu-id="27796-152">控制</span><span class="sxs-lookup"><span data-stu-id="27796-152">Controls</span></span>

<span data-ttu-id="27796-153">hello 以下是不同的系統管理員 hello 控制項，可供所有這種行為的清單。</span><span class="sxs-lookup"><span data-stu-id="27796-153">hello following is a list of hello different admin controls available for all this behavior.</span></span> <span data-ttu-id="27796-154">控制項可以存取 hello 從傳統入口網站中的 hello 系統管理員設定 hello 目錄下。</span><span class="sxs-lookup"><span data-stu-id="27796-154">hello admin controls can be accessed in hello classic portal from configure under hello directory.</span></span>

![](media/active-directory-apps-permissions-consent/apps7.png)

<span data-ttu-id="27796-155">在 [hello Azure 入口網站中，在**管理**，**使用者設定**。</span><span class="sxs-lookup"><span data-stu-id="27796-155">In hello Azure portal, under **manage**, **user settings**.</span></span>

![](media/active-directory-apps-permissions-consent/apps11.png)



- <span data-ttu-id="27796-156">您可以控制使用者是否可以同意 tooapps:</span><span class="sxs-lookup"><span data-stu-id="27796-156">You can control whether users can consent tooapps:</span></span>

<span data-ttu-id="27796-157">在 [hello 傳統入口網站，選取 [**使用者可以給予應用程式的權限 tooaccess 其資料。**
![](media/active-directory-apps-permissions-consent/apps8.png)</span><span class="sxs-lookup"><span data-stu-id="27796-157">In hello classic portal, select **Users may give applications permissions tooaccess their data.**
![](media/active-directory-apps-permissions-consent/apps8.png)</span></span>

<span data-ttu-id="27796-158">在 [hello Azure 入口網站，選取 [**使用者可以允許其資料應用程式 tooaccess**。</span><span class="sxs-lookup"><span data-stu-id="27796-158">In hello Azure portal, select **users can allow apps tooaccess their data**.</span></span>
![](media/active-directory-apps-permissions-consent/apps12.png)



- <span data-ttu-id="27796-159">您可以控制使用者是否可以註冊他們自己的單一租用戶 LOB 應用程式： 在 hello 傳統入口網站選取**使用者可以新增整合的應用程式。**
![](media/active-directory-apps-permissions-consent/apps9.png)</span><span class="sxs-lookup"><span data-stu-id="27796-159">You can control whether users can register their own single-tenant LOB apps: In hello classic portal select **Users may add integrated applications.**
![](media/active-directory-apps-permissions-consent/apps9.png)</span></span>

<span data-ttu-id="27796-160">在 [hello Azure 入口網站，選取 [**使用者可以允許其資料應用程式 tooaccess**。</span><span class="sxs-lookup"><span data-stu-id="27796-160">In hello Azure portal, select **users can allow apps tooaccess their data**.</span></span>
![](media/active-directory-apps-permissions-consent/apps13.png)

>[!NOTE]
><span data-ttu-id="27796-161">即使您允許使用者 tooregister 單一租用戶 LOB 應用程式，會有 toowhat 可以註冊的限制。</span><span class="sxs-lookup"><span data-stu-id="27796-161">Even if you do allow users tooregister single-tenant LOB apps, there are limits toowhat can be registered.</span></span>  
><span data-ttu-id="27796-162">例如，不是目錄管理員的開發人員。</span><span class="sxs-lookup"><span data-stu-id="27796-162">For example, developers who are not directory admins.</span></span>
>
>- <span data-ttu-id="27796-163">使用者無法讓單一租用戶應用程式變成多租用戶應用程式。</span><span class="sxs-lookup"><span data-stu-id="27796-163">Users cannot make a single-tenant app a multi-tenant app.</span></span>
>- <span data-ttu-id="27796-164">當登錄單一租用戶的 LOB 應用程式，使用者無法要求僅限應用程式的權限 tooother 應用程式。</span><span class="sxs-lookup"><span data-stu-id="27796-164">When registering single-tenant LOB apps, users cannot request app-only permissions tooother apps.</span></span>
>- <span data-ttu-id="27796-165">當登錄單一租用戶的 LOB 應用程式，使用者無法要求委派的權限 tooother 應用程式，如果這些權限需要系統管理員同意。</span><span class="sxs-lookup"><span data-stu-id="27796-165">When registering single-tenant LOB apps, users cannot request delegated permissions tooother apps if those permissions require admin consent.</span></span>
>- <span data-ttu-id="27796-166">使用者無法進行變更 tooapps，它們不是擁有者。</span><span class="sxs-lookup"><span data-stu-id="27796-166">Users cannot make changes tooapps that they are not owners of.</span></span>



- <span data-ttu-id="27796-167">您可以控制使用者是否可以自行新增使用密碼 SSO 的預先整合應用程式 (也稱為「密碼儲存庫存」) ![](media/active-directory-apps-permissions-consent/apps10.png)</span><span class="sxs-lookup"><span data-stu-id="27796-167">You can control whether users can themselves add pre-integrated apps that use password SSO (aka “password vaulting”) ![](media/active-directory-apps-permissions-consent/apps10.png)</span></span>



- <span data-ttu-id="27796-168">您可以控制在哪些情況下可以存取應用程式 (也就是條件式存取)。</span><span class="sxs-lookup"><span data-stu-id="27796-168">You can control under which conditions applications can be accessed (that is, conditional access).</span></span> <span data-ttu-id="27796-169">請注意這適用於 toohello 用戶端應用程式和 toohello 資源應用程式。</span><span class="sxs-lookup"><span data-stu-id="27796-169">Be aware this applies both toohello client app and toohello resource app.</span></span> <span data-ttu-id="27796-170">因此，假設您設定條件式存取原則，指出該 hello 「 Office 365 Exchange Online"的應用程式只能存取從相容的電腦。</span><span class="sxs-lookup"><span data-stu-id="27796-170">So, say you set a conditional access policy that says that hello “Office 365 Exchange Online” app can only be accessed from machines, which are compliant.</span></span>  <span data-ttu-id="27796-171">使用者嘗試 toouse 會要求權限 tooExchange 線上的用戶端應用程式時，此原則也會啟動。</span><span class="sxs-lookup"><span data-stu-id="27796-171">This policy will also kick in when a user attempts toouse a client app which requests permissions tooExchange Online.</span></span>



- <span data-ttu-id="27796-172">您必須在其中應用程式已獲得同意的 tooand 正在使用哪些的可見性。</span><span class="sxs-lookup"><span data-stu-id="27796-172">You have visibility into which apps have been consented tooand which ones are being used.</span></span>

1.  <span data-ttu-id="27796-173">當使用者同意時 tooan 應用程式時，ServicePrincipal 物件會建立 hello 租用戶中。</span><span class="sxs-lookup"><span data-stu-id="27796-173">When a user consents tooan app, a ServicePrincipal object is created in hello tenant.</span></span> <span data-ttu-id="27796-174">Hello 稽核報表中包含 ServicePrincipal 建立。</span><span class="sxs-lookup"><span data-stu-id="27796-174">ServicePrincipal creation is included in hello audit report.</span></span>
2.  <span data-ttu-id="27796-175">使用者登入活動報表會告訴您哪些應用程式 hello 使用者登入。</span><span class="sxs-lookup"><span data-stu-id="27796-175">User sign-in activity reports tell you which app hello user is signing in to.</span></span> 

## <a name="example"></a><span data-ttu-id="27796-176">範例</span><span class="sxs-lookup"><span data-stu-id="27796-176">Example</span></span>

<span data-ttu-id="27796-177">例如，讓我們來看 hello"FabrikamMail 適用於 Office 365 」 應用程式，您已注意到您的租用戶中的使用者所登入至其中。</span><span class="sxs-lookup"><span data-stu-id="27796-177">As an example, let’s take hello “FabrikamMail for Office 365” app, which you’ve noticed users in your tenant are signing in to.</span></span> <span data-ttu-id="27796-178">「FabrikamMail」是 Android 版的郵件讀取程式應用程式，由「Fabrikam, Inc.」所發行。</span><span class="sxs-lookup"><span data-stu-id="27796-178">“FabrikamMail” is a mail reader app for Android, published by “Fabrikam, Inc.”.</span></span> <span data-ttu-id="27796-179">這屬於 hello"多租用戶應用程式其他開發，Contoso 同意 」。</span><span class="sxs-lookup"><span data-stu-id="27796-179">This falls into hello “multi-tenant apps other develop, which Contoso can consent to”.</span></span>

<span data-ttu-id="27796-180">如果使用者允許 tooconsent，他們取得同意提示 hello 第一次登入：![](media/active-directory-apps-permissions-consent/apps14.png)</span><span class="sxs-lookup"><span data-stu-id="27796-180">If users are allowed tooconsent, they get a consent prompt hello first time they sign in: ![](media/active-directory-apps-permissions-consent/apps14.png)</span></span>

<span data-ttu-id="27796-181">「 存取您的信箱 」 為 「 Office 365 Exchange 連線 」 （也就是交換） 所公開的 hello"hello 登入的使用者身分存取信箱 」 權限的 hello 面對使用者的同意字串。</span><span class="sxs-lookup"><span data-stu-id="27796-181">“Access your mailboxes” is hello user-facing consent string for hello “Access mailboxes as hello signed-in user” permission exposed by “Office 365 Exchange Online” (that is, Exchange).</span></span>

<span data-ttu-id="27796-182">您可以看見 hello 權限適用於 Exchange （hello 資源），已加入您註冊 Office 365 時查閱 hello ServicePrincipal 物件。</span><span class="sxs-lookup"><span data-stu-id="27796-182">You can see hello permissions by looking up hello ServicePrincipal object for Exchange (hello resource), which was added when you signed up for Office 365.</span></span> <span data-ttu-id="27796-183">在您的租用戶，以用於記錄不同的選項和組態中，您可以將 hello ServicePrincipal 物件的 hello 應用程式 」 執行個體 」。</span><span class="sxs-lookup"><span data-stu-id="27796-183">You can think of hello ServicePrincipal object of an “instance” of hello app in your tenant, which is used for recording different options and configurations.</span></span>  <span data-ttu-id="27796-184">您可以看到此使用 hello`Get-AzureADServicePrincipal`在 PowerShell 中。</span><span class="sxs-lookup"><span data-stu-id="27796-184">You can see this by using hello `Get-AzureADServicePrincipal` in PowerShell.</span></span>

    PS C:\> Get-AzureADServicePrincipal -ObjectId 383f7b97-6754-4d3d-9474-3908ebcba1c6 | fl *
    
    DeletionTimeStamp         : 
    ObjectId                  : 383f7b97-6754-4d3d-9474-3908ebcba1c6
    ObjectType                : ServicePrincipal
    AccountEnabled            : True
    AppDisplayName            : Office 365 Exchange Online
    AppId                     : 00000002-0000-0ff1-ce00-000000000000
    AppOwnerTenantId          : 
    AppRoleAssignmentRequired : False
    AppRoles                  : {...}
    DisplayName               : Microsoft.Exchange
    ErrorUrl                  : 
    Homepage                  : 
    KeyCredentials            : {}
    LogoutUrl                 : 
    Oauth2Permissions         : {...
                                , class OAuth2Permission {
                                  AdminConsentDescription : Allows hello app toohave hello same access toomailboxes as hello signed-in user via Exchange Web Services.
                                  AdminConsentDisplayName : Access mailboxes as hello signed-in user via Exchange Web Services
                                  Id                      : 3b5f3d61-589b-4a3c-a359-5dd4b5ee5bd5
                                  IsEnabled               : True
                                  Type                    : User
                                  UserConsentDescription  : Allows hello app full access tooyour mailboxes on your behalf.
                                  UserConsentDisplayName  : Access your mailboxes
                                  Value                   : full_access_as_user
                                },
                                ...}
    PasswordCredentials       : {}
    PublisherName             : 
    ReplyUrl                  : 
    SamlMetadataUrl           : 
    ServicePrincipalNames     : {00000002-0000-0ff1-ce00-000000000000/outlook.office365.com, 00000002-0000-0ff1-ce00-000000000000/mail.office365.com, 00000002-0000-0ff1-ce00-000000000000/outlook.com, 
                                00000002-0000-0ff1-ce00-000000000000/*.outlook.com...}
    Tags                      : {}

<span data-ttu-id="27796-185">Hello 使用者按一下 [接受] 時，就會起始同意。</span><span class="sxs-lookup"><span data-stu-id="27796-185">Consent is initiated when hello user clicks “Accept”.</span></span> <span data-ttu-id="27796-186">首先，「 FabrikamMail 適用於 Office 365 」 的 ServicePrincipal 物件就會建立 hello 租用戶中。</span><span class="sxs-lookup"><span data-stu-id="27796-186">First, a ServicePrincipal object for “FabrikamMail for Office 365” is created in hello tenant.</span></span> <span data-ttu-id="27796-187">hello ServicePrincipal 看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="27796-187">hello ServicePrincipal looks something like this:</span></span>

    PS C:\> Get-AzureADServicePrincipal -SearchString "FabrikamMail for Office 365" | fl *
    
    DeletionTimeStamp         : 
    ObjectId                  : a8b16333-851d-42e8-acd2-eac155849b37
    ObjectType                : ServicePrincipal
    AccountEnabled            : True
    AppDisplayName            : FabrikamMail for Office 365
    AppId                     : aba7c072-2267-4031-8960-e7a2db6e0590
    AppOwnerTenantId          : 4a4076e0-a70f-41c6-b819-6f9c4a86df89
    AppRoleAssignmentRequired : False
    AppRoles                  : {}
    DisplayName               : FabrikamMail for Office 365
    ErrorUrl                  : 
    Homepage                  : 
    KeyCredentials            : {}
    LogoutUrl                 : 
    Oauth2Permissions         : {}
    PasswordCredentials       : {}
    PublisherName             : Fabrikam, Inc.
    ReplyUrl                  : 
    SamlMetadataUrl           : 
    ServicePrincipalNames     : {aba7c072-2267-4031-8960-e7a2db6e0590}
    Tags                      : {WindowsAzureActiveDirectoryIntegratedApp}

<span data-ttu-id="27796-188">同意 tooan 應用程式 Oauth2PermissionGrant 之間建立連結 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="27796-188">Consenting tooan app creates an Oauth2PermissionGrant link between hello following:</span></span>
  
- <span data-ttu-id="27796-189">hello 使用者物件</span><span class="sxs-lookup"><span data-stu-id="27796-189">hello user object</span></span>
- <span data-ttu-id="27796-190">hello 用戶端應用程式 ServicePrincipalName (SPN)</span><span class="sxs-lookup"><span data-stu-id="27796-190">hello client apps ServicePrincipalName (SPN)</span></span>
- <span data-ttu-id="27796-191">hello 資源應用程式 ServicePrincipalName (SPN)</span><span class="sxs-lookup"><span data-stu-id="27796-191">hello resource apps ServicePrincipalName (SPN)</span></span>
- <span data-ttu-id="27796-192">在 [hello 資源應用程式的權限。</span><span class="sxs-lookup"><span data-stu-id="27796-192">permissions in hello resource app.</span></span>  

<span data-ttu-id="27796-193">FabrikamMail hello 案例，它看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="27796-193">In hello case of FabrikamMail, it looks something like this:</span></span>

    PS C:\> Get-AzureADUserOAuth2PermissionGrant -ObjectId ddiggle@aadpremiumlab.onmicrosoft.com | fl *
    
    ClientId    : a8b16333-851d-42e8-acd2-eac155849b37
    ConsentType : Principal
    ExpiryTime  : 05/15/2017 07:02:39 AM
    ObjectId    : M2OxqB2F6EKs0urBVYSbN5d7PzhUZz1NlH25COvLocbJjoxkUFfRQauryBKwBWet
    PrincipalId : 648c8ec9-5750-41d1-abab-c812b00567ad
    ResourceId  : 383f7b97-6754-4d3d-9474-3908ebcba1c6
    Scope       : full_access_as_user
    StartTime   : 01/01/0001 12:00:00 AM

<span data-ttu-id="27796-194">(**ClientId** FabrikamMail 的服務主體的物件識別碼 (hello 取得剛建立的其中一個)， **PrincipalId** hello 使用者物件識別碼 （hello 使用者同意）， **ResourceId**是交換的服務主體的物件識別碼，範圍是已同意的交換中的 hello 權限)。</span><span class="sxs-lookup"><span data-stu-id="27796-194">(**ClientId** is FabrikamMail’s service principal object ID (hello one that just got created), **PrincipalId** is hello user object ID (of hello user who consented), **ResourceId** is Exchange’s service principal object ID, Scope is hello permission in Exchange that was consented to).</span></span>

<span data-ttu-id="27796-195">如果使用者不允許 tooconsent，就會看到指出該權限的螢幕為必要。</span><span class="sxs-lookup"><span data-stu-id="27796-195">If users are not allowed tooconsent, they will see a screen that says that permission is required.</span></span>

