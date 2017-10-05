---
title: "Azure Active Directory 中的應用程式、權限及同意 | Microsoft Docs"
description: "Azure AD Connect 會整合您的內部部署目錄與 Azure Active Directory。 這可讓您為與 Azure AD 整合的 Office 365、Azure 和 SaaS 應用程式提供通用身分識別。"
keywords: "Azure AD 簡介, 應用程式, 何謂 Azure AD Connect, 安裝 active directory"
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
ms.openlocfilehash: 6f6baf5e1538fb280a899065c64ca5688473c04a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="apps-permissions-and-consent-in-azure-active-directory"></a><span data-ttu-id="dffa3-105">Azure Active Directory 中的應用程式、權限及同意</span><span class="sxs-lookup"><span data-stu-id="dffa3-105">Apps, permissions, and consent in Azure Active Directory</span></span>
<span data-ttu-id="dffa3-106">在 Azure Active Directory 內，您可以在目錄中新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="dffa3-106">Within Azure Active Directory, you can add applications to your directory.</span></span>  <span data-ttu-id="dffa3-107">應用程式可能會根據應用程式類型而有所不同。</span><span class="sxs-lookup"><span data-stu-id="dffa3-107">The applications can vary depending on the type of application.</span></span>  <span data-ttu-id="dffa3-108">若要在傳統入口網站中檢視應用程式，請選取目錄並選擇應用程式。</span><span class="sxs-lookup"><span data-stu-id="dffa3-108">To view applications in the classic portal, select a directory and choose applications.</span></span>

![](media/active-directory-apps-permissions-consent/apps1.png)

> [!IMPORTANT]
> <span data-ttu-id="dffa3-109">Microsoft 建議您使用 Azure 入口網站中的 [Azure AD 系統管理中心](https://aad.portal.azure.com)來管理 Azure AD，而不要使用本文所提及的 Azure 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="dffa3-109">Microsoft recommends that you manage Azure AD using the [Azure AD admin center](https://aad.portal.azure.com) in the Azure portal instead of using the Azure classic portal referenced in this article.</span></span>

## <a name="types-of-apps"></a><span data-ttu-id="dffa3-110">應用程式類型</span><span class="sxs-lookup"><span data-stu-id="dffa3-110">Types of apps</span></span>

1. <span data-ttu-id="dffa3-111">**單一租用戶應用程式**</span><span class="sxs-lookup"><span data-stu-id="dffa3-111">**Single-tenant apps**</span></span> </br>
    - <span data-ttu-id="dffa3-112">**單一租用戶應用程式** - 通常稱為企業營運 (LOB) 應用程式。</span><span class="sxs-lookup"><span data-stu-id="dffa3-112">**Single-tenant apps** - Often referred to as line-of-business (LOB) apps.</span></span> <span data-ttu-id="dffa3-113">這是組織內的某人開發了自己的應用程式，並希望組織中的使用者能夠登入應用程式的情況。</span><span class="sxs-lookup"><span data-stu-id="dffa3-113">This is the case where someone within your organization develops their own app, and would like users in the organization to be able to sign in to the app.</span></span>
    ![](media/active-directory-apps-permissions-consent/apps2.png)
    - <span data-ttu-id="dffa3-114">**應用程式 Proxy 應用程式** - 當您使用 Azure AD 應用程式 Proxy 公開內部部署應用程式時，便會在租用戶中註冊單一租用戶應用程式 (以及應用程式 Proxy 服務)。</span><span class="sxs-lookup"><span data-stu-id="dffa3-114">**App Proxy apps** - When you expose an on-prem application with Azure AD App Proxy, a single-tenant app is registered in your tenant (in addition to the App Proxy service).</span></span> <span data-ttu-id="dffa3-115">此應用程式便是代表所有雲端互動 (例如驗證) 之內部部署應用程式的項目 </span><span class="sxs-lookup"><span data-stu-id="dffa3-115">This app is what represents your on-prem application for all cloud interactions (for example, authentication).</span></span> <span data-ttu-id="dffa3-116">(應用程式 Proxy 需要 Azure AD Basic 或更高版本)。</span><span class="sxs-lookup"><span data-stu-id="dffa3-116">(App Proxy requires Azure AD Basic or higher.)</span></span>


2. <span data-ttu-id="dffa3-117">**多租用戶應用程式**</span><span class="sxs-lookup"><span data-stu-id="dffa3-117">**Multi-tenant apps**</span></span>
    - <span data-ttu-id="dffa3-118">**其他人可同意的多租用戶應用程式** - 類似於「組織開發的單一租用戶應用程式」。</span><span class="sxs-lookup"><span data-stu-id="dffa3-118">**Multi-tenant apps which others can consent to** - similar to “single-tenant apps that your organization develops”.</span></span> <span data-ttu-id="dffa3-119">主要差異 (除了應用程式本身的邏輯外) 是其他租用戶的使用者也可以同意並登入應用程式。</span><span class="sxs-lookup"><span data-stu-id="dffa3-119">The main difference (besides the logic in the app itself) is that users from other tenants can also consent to and sign in to the app.</span></span></br>
    ![](media/active-directory-apps-permissions-consent/apps4.png)
    - <span data-ttu-id="dffa3-120">**其他人開發、且 Contoso 可同意的多租用戶應用程式** </span><span class="sxs-lookup"><span data-stu-id="dffa3-120">**Multi-tenant apps others develop, which Contoso can consent to**.</span></span> <span data-ttu-id="dffa3-121">(或簡稱「已同意的應用程式」)。這是「組織所開發之多租用戶應用程式」的缺點。</span><span class="sxs-lookup"><span data-stu-id="dffa3-121">(Or “consented apps”, for short.) This is the flip side of “multi-tenant apps your organization develops”.</span></span> <span data-ttu-id="dffa3-122">當另一個組織開發了多租用戶應用程式時，您組織的使用者可以同意應用程式並進行登入。</span><span class="sxs-lookup"><span data-stu-id="dffa3-122">When another organization develops a multi-tenant app, users of your organization can consent to the app and sign in to it.</span></span>
    - <span data-ttu-id="dffa3-123">**Microsoft 第一方應用程式** - 代表 Microsoft 服務的應用程式。</span><span class="sxs-lookup"><span data-stu-id="dffa3-123">**Microsoft first-party apps** - Apps that represent Microsoft services.</span></span> <span data-ttu-id="dffa3-124">您註冊服務的事實便代表同意。</span><span class="sxs-lookup"><span data-stu-id="dffa3-124">Consent is driven by the fact that you sign up for the service.</span></span> <span data-ttu-id="dffa3-125">某些第一方應用程式有時候會有在建立關於應用程式的存取原則時常會使用的特殊 UX 和邏輯。</span><span class="sxs-lookup"><span data-stu-id="dffa3-125">There is sometimes special UX and logic for certain first-party apps that is often used when establishing policies around access to the app.</span></span></br>
    ![](media/active-directory-apps-permissions-consent/apps3.png)
    - <span data-ttu-id="dffa3-126">**預先整合的應用程式** - Azure AD 應用程式庫中可用的應用程式，您可以新增至目錄以對熱門的 SaaS 應用程式提供單一登入 (以及在某些情況下提供佈建)。</span><span class="sxs-lookup"><span data-stu-id="dffa3-126">**Pre-integrated apps** - Apps available in the Azure AD App Gallery, which you can add to your directory to provide single sign-on (and in some cases, provisioning) to popular SaaS apps.</span></span>
    - <span data-ttu-id="dffa3-127">**Azure AD 單一登入**：可透過 SAML 2.0 或 OpenID Connect 等受支援登入通訊協定來與 Azure AD 整合之應用程式的「真實」SSO。</span><span class="sxs-lookup"><span data-stu-id="dffa3-127">**Azure AD single sign-on**: “Real” SSO, for apps that can be integrated with Azure AD, through a supported sign-in protocol such as SAML 2.0 or OpenID Connect.</span></span> <span data-ttu-id="dffa3-128">精靈會引導您完成設定。</span><span class="sxs-lookup"><span data-stu-id="dffa3-128">The wizard walks you through setting it up.</span></span>
    - <span data-ttu-id="dffa3-129">**密碼單一登入**：Azure AD 會安全地儲存應用程式的使用者認證，並由 Azure AD 應用程式存取瀏覽器延伸模組將認證「插入」至登入表單。</span><span class="sxs-lookup"><span data-stu-id="dffa3-129">**Password single sign-on**: Azure AD securely stores the user’s credentials for the app, and the credentials are “injected” into the sign-in form by the Azure AD App Access browser extension.</span></span> <span data-ttu-id="dffa3-130">也稱為「密碼儲存庫存」。</span><span class="sxs-lookup"><span data-stu-id="dffa3-130">Also known as “password vaulting”.</span></span>

## <a name="permissions"></a><span data-ttu-id="dffa3-131">權限</span><span class="sxs-lookup"><span data-stu-id="dffa3-131">Permissions</span></span>

<span data-ttu-id="dffa3-132">在註冊應用程式時，執行應用程式註冊的使用者 (也就是開發人員) 會定義應用程式需要存取的權限，以及哪些資源 </span><span class="sxs-lookup"><span data-stu-id="dffa3-132">When an app is registered, the user performing the app registration (that is, the developer) defines which permissions the app needs access to, and which resources.</span></span> <span data-ttu-id="dffa3-133">(資源本身會定義為其他應用程式)。比方說，建置郵件讀取程式應用程式的某人會指出，其應用程式需要「Office 365 Exchange Online」資源的「以登入使用者身分存取信箱」的權限︰</span><span class="sxs-lookup"><span data-stu-id="dffa3-133">(The resources are, themselves, defined as other apps.) For example, someone building a mail reader app, would state that their app requires the “Access mailboxes as the signed-in user” permission in the “Office 365 Exchange Online” resource:</span></span>
    
![](media/active-directory-apps-permissions-consent/apps6.png)

<span data-ttu-id="dffa3-134">為了讓某個應用程式 (用戶端) 從另一個應用程式 (資源) 要求特定權限，資源應用程式的開發人員會定義存在的權限。</span><span class="sxs-lookup"><span data-stu-id="dffa3-134">In order for one app (the client) to request a certain permission from another app (the resource), the developer of the resource app defines the permissions that exist.</span></span> <span data-ttu-id="dffa3-135">在我們的範例中，「Office 365 Exchange Online」資源應用程式的擁有者 (Microsoft) 已定義名為「以登入使用者身分存取信箱」的權限。</span><span class="sxs-lookup"><span data-stu-id="dffa3-135">In our example, Microsoft, the owner of the “Office 365 Exchange Online” resource app, have defined a permission named “Access mailboxes as the signed-in user”.</span></span>

<span data-ttu-id="dffa3-136">在定義權限時，應用程式開發人員必須定義是否可以同意權限，或權限是否需要系統管理員同意。</span><span class="sxs-lookup"><span data-stu-id="dffa3-136">When defining permissions, the app developer must define if the permission can be consented to, or if it requires admin consent.</span></span> <span data-ttu-id="dffa3-137">這可讓開發人員允許使用者自行同意只要求了低敏感度權限的應用程式，但敏感度更高的權限則需要系統管理員同意。</span><span class="sxs-lookup"><span data-stu-id="dffa3-137">This allows developers to allow users to consent on their own to apps requesting only low-sensitivity permissions, but require admins to consent to more sensitive permissions.</span></span> <span data-ttu-id="dffa3-138">比方說，「Azure Active Directory」資源應用程式已定義完成，因此使用者可以同意要求有限唯讀權限的應用程式。</span><span class="sxs-lookup"><span data-stu-id="dffa3-138">For example, the “Azure Active Directory” resource app, has been defined, so users can consent to apps, requesting limited read-only permissions.</span></span>  <span data-ttu-id="dffa3-139">不過，行使系統管理員同意則需要完整讀取權限和所有寫入權限。</span><span class="sxs-lookup"><span data-stu-id="dffa3-139">However, admin consent is required for full read permissions, and all write permissions.</span></span>

<span data-ttu-id="dffa3-140">因為原生用戶端未經過驗證，因此定義為原生用戶端應用程式的應用程式只能要求委派的權限。</span><span class="sxs-lookup"><span data-stu-id="dffa3-140">Because native clients are not authenticated, an app defined as a native client app can only request delegated permissions.</span></span> <span data-ttu-id="dffa3-141">這表示在取得權杖時一律必須由實際使用者涉入。</span><span class="sxs-lookup"><span data-stu-id="dffa3-141">This means that there must always be an actual user involved when obtaining a token.</span></span> <span data-ttu-id="dffa3-142">在取得存取權杖時，Web 應用程式和 Web API (機密用戶端) 一律必須向 Azure AD 驗證。</span><span class="sxs-lookup"><span data-stu-id="dffa3-142">Web apps and web APIs (confidential clients), must always authenticate with Azure AD when getting an access token.</span></span> <span data-ttu-id="dffa3-143">這表示它們也有可能會要求僅限應用程式的權限。</span><span class="sxs-lookup"><span data-stu-id="dffa3-143">Meaning they also have the possibility of requesting app-only permissions.</span></span> <span data-ttu-id="dffa3-144">例如，如果某個後端服務需要向另一個後端服務驗證。</span><span class="sxs-lookup"><span data-stu-id="dffa3-144">For example, if one back-end service needs to authenticate to another back-end service.</span></span> <span data-ttu-id="dffa3-145">要求僅限應用程式權限的應用程式一律需要系統管理員的同意。</span><span class="sxs-lookup"><span data-stu-id="dffa3-145">Applications requesting app-only permissions always require administrator consent.</span></span>

<span data-ttu-id="dffa3-146">摘要︰</span><span class="sxs-lookup"><span data-stu-id="dffa3-146">Summarizing:</span></span>



- <span data-ttu-id="dffa3-147">應用程式 (用戶端) 會指出其所需的其他應用程式 (資源) 權限。</span><span class="sxs-lookup"><span data-stu-id="dffa3-147">An app (client) states the permissions it needs for other apps (resources).</span></span>
- <span data-ttu-id="dffa3-148">應用程式 (資源) 會指出要對其他應用程式 (用戶端) 公開哪些權限。</span><span class="sxs-lookup"><span data-stu-id="dffa3-148">An app (resource) states what permissions are exposed to other apps (clients).</span></span>
- <span data-ttu-id="dffa3-149">權限可以是僅限應用程式權限或委派的權限。</span><span class="sxs-lookup"><span data-stu-id="dffa3-149">A permission can be an app-only permission, or a delegated permission.</span></span>
- <span data-ttu-id="dffa3-150">委派的權限可以標示為「允許使用者同意」或「需要系統管理員同意」。</span><span class="sxs-lookup"><span data-stu-id="dffa3-150">A delegated permission can be marked as “allows user consent”, or “requires admin consent”.</span></span>
- <span data-ttu-id="dffa3-151">應用程式可以做為用戶端 (藉由宣告其需要資源的權限)、做為資源 (藉由宣告其公開的權限) 或同時做為兩者。</span><span class="sxs-lookup"><span data-stu-id="dffa3-151">An app can behave as a client (by declaring that it needs permissions to a resource), as a resource (by declaring which permissions it exposes), or as both.</span></span>

## <a name="controls"></a><span data-ttu-id="dffa3-152">控制</span><span class="sxs-lookup"><span data-stu-id="dffa3-152">Controls</span></span>

<span data-ttu-id="dffa3-153">以下是所有這種行為可用之不同系統管理員控制的清單。</span><span class="sxs-lookup"><span data-stu-id="dffa3-153">The following is a list of the different admin controls available for all this behavior.</span></span> <span data-ttu-id="dffa3-154">在傳統入口網站中，可以透過在目錄下進行設定，來存取系統管理員控制。</span><span class="sxs-lookup"><span data-stu-id="dffa3-154">The admin controls can be accessed in the classic portal from configure under the directory.</span></span>

![](media/active-directory-apps-permissions-consent/apps7.png)

<span data-ttu-id="dffa3-155">在 Azure 入口網站中，於 [管理]、[使用者設定] 下。</span><span class="sxs-lookup"><span data-stu-id="dffa3-155">In the Azure portal, under **manage**, **user settings**.</span></span>

![](media/active-directory-apps-permissions-consent/apps11.png)



- <span data-ttu-id="dffa3-156">您可以控制使用者是否可以同意應用程式︰</span><span class="sxs-lookup"><span data-stu-id="dffa3-156">You can control whether users can consent to apps:</span></span>

<span data-ttu-id="dffa3-157">在傳統入口網站中，選取 [使用者可以賦予應用程式存取其資料的權限]。
![](media/active-directory-apps-permissions-consent/apps8.png)</span><span class="sxs-lookup"><span data-stu-id="dffa3-157">In the classic portal, select **Users may give applications permissions to access their data.**
![](media/active-directory-apps-permissions-consent/apps8.png)</span></span>

<span data-ttu-id="dffa3-158">在 Azure 入口網站中，選取 [使用者可以允許應用程式存取其資料]。</span><span class="sxs-lookup"><span data-stu-id="dffa3-158">In the Azure portal, select **users can allow apps to access their data**.</span></span>
![](media/active-directory-apps-permissions-consent/apps12.png)



- <span data-ttu-id="dffa3-159">您可以控制使用者是否可以註冊自己的單一租用戶 LOB 應用程式︰在傳統入口網站中，選取 [使用者可以新增整合的應用程式]。
![](media/active-directory-apps-permissions-consent/apps9.png)</span><span class="sxs-lookup"><span data-stu-id="dffa3-159">You can control whether users can register their own single-tenant LOB apps: In the classic portal select **Users may add integrated applications.**
![](media/active-directory-apps-permissions-consent/apps9.png)</span></span>

<span data-ttu-id="dffa3-160">在 Azure 入口網站中，選取 [使用者可以允許應用程式存取其資料]。</span><span class="sxs-lookup"><span data-stu-id="dffa3-160">In the Azure portal, select **users can allow apps to access their data**.</span></span>
![](media/active-directory-apps-permissions-consent/apps13.png)

>[!NOTE]
><span data-ttu-id="dffa3-161">即使您已允許使用者註冊單一租用戶 LOB 應用程式，所能註冊的項目仍會有限制。</span><span class="sxs-lookup"><span data-stu-id="dffa3-161">Even if you do allow users to register single-tenant LOB apps, there are limits to what can be registered.</span></span>  
><span data-ttu-id="dffa3-162">例如，不是目錄管理員的開發人員。</span><span class="sxs-lookup"><span data-stu-id="dffa3-162">For example, developers who are not directory admins.</span></span>
>
>- <span data-ttu-id="dffa3-163">使用者無法讓單一租用戶應用程式變成多租用戶應用程式。</span><span class="sxs-lookup"><span data-stu-id="dffa3-163">Users cannot make a single-tenant app a multi-tenant app.</span></span>
>- <span data-ttu-id="dffa3-164">在註冊單一租用戶 LOB 應用程式時，使用者無法要求其他應用程式的僅限應用程式權限。</span><span class="sxs-lookup"><span data-stu-id="dffa3-164">When registering single-tenant LOB apps, users cannot request app-only permissions to other apps.</span></span>
>- <span data-ttu-id="dffa3-165">在註冊單一租用戶 LOB 應用程式時，如果其他應用程式的委派權限需要系統管理員同意，使用者就無法要求這些權限。</span><span class="sxs-lookup"><span data-stu-id="dffa3-165">When registering single-tenant LOB apps, users cannot request delegated permissions to other apps if those permissions require admin consent.</span></span>
>- <span data-ttu-id="dffa3-166">使用者無法變更他們未擁有的應用程式。</span><span class="sxs-lookup"><span data-stu-id="dffa3-166">Users cannot make changes to apps that they are not owners of.</span></span>



- <span data-ttu-id="dffa3-167">您可以控制使用者是否可以自行新增使用密碼 SSO 的預先整合應用程式 (也稱為「密碼儲存庫存」) ![](media/active-directory-apps-permissions-consent/apps10.png)</span><span class="sxs-lookup"><span data-stu-id="dffa3-167">You can control whether users can themselves add pre-integrated apps that use password SSO (aka “password vaulting”) ![](media/active-directory-apps-permissions-consent/apps10.png)</span></span>



- <span data-ttu-id="dffa3-168">您可以控制在哪些情況下可以存取應用程式 (也就是條件式存取)。</span><span class="sxs-lookup"><span data-stu-id="dffa3-168">You can control under which conditions applications can be accessed (that is, conditional access).</span></span> <span data-ttu-id="dffa3-169">請注意，這一點同時適用於用戶端應用程式和資源應用程式。</span><span class="sxs-lookup"><span data-stu-id="dffa3-169">Be aware this applies both to the client app and to the resource app.</span></span> <span data-ttu-id="dffa3-170">因此，假設您設定了條件式存取原則，其指出「Office 365 Exchange Online」應用程式只能從相容的機器存取。</span><span class="sxs-lookup"><span data-stu-id="dffa3-170">So, say you set a conditional access policy that says that the “Office 365 Exchange Online” app can only be accessed from machines, which are compliant.</span></span>  <span data-ttu-id="dffa3-171">當使用者嘗試使用會要求 Exchange Online 權限的用戶端應用程式時，此原則也會適用。</span><span class="sxs-lookup"><span data-stu-id="dffa3-171">This policy will also kick in when a user attempts to use a client app which requests permissions to Exchange Online.</span></span>



- <span data-ttu-id="dffa3-172">您可以看到已同意的應用程式以及正在使用的應用程式。</span><span class="sxs-lookup"><span data-stu-id="dffa3-172">You have visibility into which apps have been consented to and which ones are being used.</span></span>

1.  <span data-ttu-id="dffa3-173">當使用者同意應用程式時，租用戶中會建立 ServicePrincipal 物件。</span><span class="sxs-lookup"><span data-stu-id="dffa3-173">When a user consents to an app, a ServicePrincipal object is created in the tenant.</span></span> <span data-ttu-id="dffa3-174">稽核報告中包含 ServicePrincipal 建立。</span><span class="sxs-lookup"><span data-stu-id="dffa3-174">ServicePrincipal creation is included in the audit report.</span></span>
2.  <span data-ttu-id="dffa3-175">使用者登入活動報告會告訴您使用者所登入的應用程式。</span><span class="sxs-lookup"><span data-stu-id="dffa3-175">User sign-in activity reports tell you which app the user is signing in to.</span></span> 

## <a name="example"></a><span data-ttu-id="dffa3-176">範例</span><span class="sxs-lookup"><span data-stu-id="dffa3-176">Example</span></span>

<span data-ttu-id="dffa3-177">舉例來說，我們來看看您已經注意到租用戶中之使用者所登入的「FabrikamMail for Office 365」應用程式。</span><span class="sxs-lookup"><span data-stu-id="dffa3-177">As an example, let’s take the “FabrikamMail for Office 365” app, which you’ve noticed users in your tenant are signing in to.</span></span> <span data-ttu-id="dffa3-178">「FabrikamMail」是 Android 版的郵件讀取程式應用程式，由「Fabrikam, Inc.」所發行。</span><span class="sxs-lookup"><span data-stu-id="dffa3-178">“FabrikamMail” is a mail reader app for Android, published by “Fabrikam, Inc.”.</span></span> <span data-ttu-id="dffa3-179">這屬於「其他人開發、且 Contoso 可同意的多租用戶應用程式」。</span><span class="sxs-lookup"><span data-stu-id="dffa3-179">This falls into the “multi-tenant apps other develop, which Contoso can consent to”.</span></span>

<span data-ttu-id="dffa3-180">如果允許使用者同意，系統會在他們第一次登入時看到同意提示︰![](media/active-directory-apps-permissions-consent/apps14.png)</span><span class="sxs-lookup"><span data-stu-id="dffa3-180">If users are allowed to consent, they get a consent prompt the first time they sign in: ![](media/active-directory-apps-permissions-consent/apps14.png)</span></span>

<span data-ttu-id="dffa3-181">「存取您的信箱」是「Office 365 Exchange Online」(也就是 Exchange) 所公開之「以登入使用者身分存取信箱」權限的使用者端同意字串。</span><span class="sxs-lookup"><span data-stu-id="dffa3-181">“Access your mailboxes” is the user-facing consent string for the “Access mailboxes as the signed-in user” permission exposed by “Office 365 Exchange Online” (that is, Exchange).</span></span>

<span data-ttu-id="dffa3-182">藉由查閱在註冊 Office 365 時所新增的 Exchange ServicePrincipal 物件 (資源)，您可以看到權限。</span><span class="sxs-lookup"><span data-stu-id="dffa3-182">You can see the permissions by looking up the ServicePrincipal object for Exchange (the resource), which was added when you signed up for Office 365.</span></span> <span data-ttu-id="dffa3-183">您可以將 ServicePrincipal 物件看作是應用程式在租用戶中的「執行個體」，其可用來記錄不同的選項和組態。</span><span class="sxs-lookup"><span data-stu-id="dffa3-183">You can think of the ServicePrincipal object of an “instance” of the app in your tenant, which is used for recording different options and configurations.</span></span>  <span data-ttu-id="dffa3-184">您可以在 PowerShell 中使用 `Get-AzureADServicePrincipal` 來查看此項目。</span><span class="sxs-lookup"><span data-stu-id="dffa3-184">You can see this by using the `Get-AzureADServicePrincipal` in PowerShell.</span></span>

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
                                  AdminConsentDescription : Allows the app to have the same access to mailboxes as the signed-in user via Exchange Web Services.
                                  AdminConsentDisplayName : Access mailboxes as the signed-in user via Exchange Web Services
                                  Id                      : 3b5f3d61-589b-4a3c-a359-5dd4b5ee5bd5
                                  IsEnabled               : True
                                  Type                    : User
                                  UserConsentDescription  : Allows the app full access to your mailboxes on your behalf.
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

<span data-ttu-id="dffa3-185">當使用者按一下 [接受] 時，便會起始同意。</span><span class="sxs-lookup"><span data-stu-id="dffa3-185">Consent is initiated when the user clicks “Accept”.</span></span> <span data-ttu-id="dffa3-186">首先，「FabrikamMail for Office 365」的 ServicePrincipal 物件會建立於租用戶中。</span><span class="sxs-lookup"><span data-stu-id="dffa3-186">First, a ServicePrincipal object for “FabrikamMail for Office 365” is created in the tenant.</span></span> <span data-ttu-id="dffa3-187">ServicePrincipal 看起來像這樣︰</span><span class="sxs-lookup"><span data-stu-id="dffa3-187">The ServicePrincipal looks something like this:</span></span>

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

<span data-ttu-id="dffa3-188">同意應用程式會在下列項目之間建立 Oauth2PermissionGrant 連結︰</span><span class="sxs-lookup"><span data-stu-id="dffa3-188">Consenting to an app creates an Oauth2PermissionGrant link between the following:</span></span>
  
- <span data-ttu-id="dffa3-189">使用者物件</span><span class="sxs-lookup"><span data-stu-id="dffa3-189">the user object</span></span>
- <span data-ttu-id="dffa3-190">用戶端應用程式 ServicePrincipalName (SPN)</span><span class="sxs-lookup"><span data-stu-id="dffa3-190">the client apps ServicePrincipalName (SPN)</span></span>
- <span data-ttu-id="dffa3-191">資源應用程式 ServicePrincipalName (SPN)</span><span class="sxs-lookup"><span data-stu-id="dffa3-191">the resource apps ServicePrincipalName (SPN)</span></span>
- <span data-ttu-id="dffa3-192">資源應用程式中的權限。</span><span class="sxs-lookup"><span data-stu-id="dffa3-192">permissions in the resource app.</span></span>  

<span data-ttu-id="dffa3-193">若為 FabrikamMail，它看起來像這樣︰</span><span class="sxs-lookup"><span data-stu-id="dffa3-193">In the case of FabrikamMail, it looks something like this:</span></span>

    PS C:\> Get-AzureADUserOAuth2PermissionGrant -ObjectId ddiggle@aadpremiumlab.onmicrosoft.com | fl *
    
    ClientId    : a8b16333-851d-42e8-acd2-eac155849b37
    ConsentType : Principal
    ExpiryTime  : 05/15/2017 07:02:39 AM
    ObjectId    : M2OxqB2F6EKs0urBVYSbN5d7PzhUZz1NlH25COvLocbJjoxkUFfRQauryBKwBWet
    PrincipalId : 648c8ec9-5750-41d1-abab-c812b00567ad
    ResourceId  : 383f7b97-6754-4d3d-9474-3908ebcba1c6
    Scope       : full_access_as_user
    StartTime   : 01/01/0001 12:00:00 AM

<span data-ttu-id="dffa3-194">(**ClientId** 是 FabrikamMail 的服務主體物件識別碼 (剛剛建立的)，**PrincipalId** 是 (已同意之使用者的) 使用者物件識別碼，**ResourceId** 是 Exchange 的服務主體物件識別碼，Scope 是已同意之 Exchange 中的權限)。</span><span class="sxs-lookup"><span data-stu-id="dffa3-194">(**ClientId** is FabrikamMail’s service principal object ID (the one that just got created), **PrincipalId** is the user object ID (of the user who consented), **ResourceId** is Exchange’s service principal object ID, Scope is the permission in Exchange that was consented to).</span></span>

<span data-ttu-id="dffa3-195">如果不允許使用者同意，他們就會看到一個畫面，指出需要有權限。</span><span class="sxs-lookup"><span data-stu-id="dffa3-195">If users are not allowed to consent, they will see a screen that says that permission is required.</span></span>

