---
title: "如何與 Azure Active Directory 整合 | Microsoft 文件"
description: "與 Azure Active Directory 整合的優點和所需資源指南。"
services: active-directory
documentationcenter: dev-center-name
author: bryanla
manager: mbaldwin
editor: 
ms.assetid: d13bba54-96bd-4b81-bee9-c8025ffa1648
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/27/2017
ms.author: bryanla
ms.custom: aaddev
ms.openlocfilehash: ecd398f9d7e3557c0d85c08b051d8436789ea94b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="integrating-with-azure-active-directory"></a><span data-ttu-id="1f4c6-103">與 Azure Active Directory 整合</span><span class="sxs-lookup"><span data-stu-id="1f4c6-103">Integrating with Azure Active Directory</span></span>
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="1f4c6-104">Azure Active Directory 為組織提供企業等級的雲端應用程式身分識別管理。</span><span class="sxs-lookup"><span data-stu-id="1f4c6-104">Azure Active Directory provides organizations with enterprise-grade identity management for cloud applications.</span></span>  <span data-ttu-id="1f4c6-105">Azure AD 整合提供使用者簡化的登入程序，並可協助您的應用程式符合 IT 原則。</span><span class="sxs-lookup"><span data-stu-id="1f4c6-105">Azure AD integration gives your users a streamlined sign-in experience, and helps your application conform to IT policy.</span></span>

## <a name="how-to-integrate"></a><span data-ttu-id="1f4c6-106">如何整合</span><span class="sxs-lookup"><span data-stu-id="1f4c6-106">How To Integrate</span></span>
<span data-ttu-id="1f4c6-107">整合應用程式與 Azure AD 的方式有幾種。</span><span class="sxs-lookup"><span data-stu-id="1f4c6-107">There are several ways for your application to integrate with Azure AD.</span></span>  <span data-ttu-id="1f4c6-108">充分利用適合您應用程式使用的這些案例。</span><span class="sxs-lookup"><span data-stu-id="1f4c6-108">Take advantage of as many or as few of these scenarios as is appropriate for your application.</span></span>

### <a name="support-azure-ad-as-a-way-to-sign-in-to-your-application"></a><span data-ttu-id="1f4c6-109">支援 Azure AD 作為登入應用程式的方式</span><span class="sxs-lookup"><span data-stu-id="1f4c6-109">Support Azure AD as a Way to Sign In to Your Application</span></span>
<span data-ttu-id="1f4c6-110">**減少登入的不便，並降低支援成本。**</span><span class="sxs-lookup"><span data-stu-id="1f4c6-110">**Reduce sign in friction and reduce support costs.**</span></span> <span data-ttu-id="1f4c6-111">透過使用 Azure AD 來登入您的應用程式，您的使用者會少一個要記住的名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="1f4c6-111">By using Azure AD to sign in to your application, your users won't have one more name and password to remember.</span></span>  <span data-ttu-id="1f4c6-112">身為開發人員，您會少一個要儲存及保護的密碼。</span><span class="sxs-lookup"><span data-stu-id="1f4c6-112">As a developer, you'll have one less password to store and protect.</span></span>  <span data-ttu-id="1f4c6-113">單單無需處理忘記密碼重設就可以省下大量時間與金錢。</span><span class="sxs-lookup"><span data-stu-id="1f4c6-113">Not having to handle forgotten password resets may be a significant savings alone.</span></span>  <span data-ttu-id="1f4c6-114">Azure AD 支援部分世界上最受歡迎雲端應用程式 (包括 Office 365 和 Microsoft Azure) 的登入。</span><span class="sxs-lookup"><span data-stu-id="1f4c6-114">Azure AD powers sign in for some of the world's most popular cloud applications, including Office 365 and Microsoft Azure.</span></span>  <span data-ttu-id="1f4c6-115">有來自數百萬個組織的數百萬名使用者，可能是您的使用者已經登入 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="1f4c6-115">With hundreds of millions users from millions of organizations, chances are your user is already signed in to Azure AD.</span></span>  <span data-ttu-id="1f4c6-116">深入了解[新增 Azure AD 登入支援](active-directory-authentication-scenarios.md)。</span><span class="sxs-lookup"><span data-stu-id="1f4c6-116">Learn more about [adding support for Azure AD sign in](active-directory-authentication-scenarios.md).</span></span>

<span data-ttu-id="1f4c6-117">**簡化應用程式的註冊程序。**</span><span class="sxs-lookup"><span data-stu-id="1f4c6-117">**Simplify sign up for your application.**</span></span>  <span data-ttu-id="1f4c6-118">註冊應用程式的過程中，Azure AD 會寄出使用者的基本資訊，讓您可以預先填入註冊表單，或者完全不需要用到。</span><span class="sxs-lookup"><span data-stu-id="1f4c6-118">During sign up for your application, Azure AD can send essential information about a user so that you can pre-fill your sign up form or eliminate it completely.</span></span>  <span data-ttu-id="1f4c6-119">使用者可以透過類似社交媒體和行動應用程式所使用的常見同意程序，使用其 Azure AD 帳戶來註冊應用程式。</span><span class="sxs-lookup"><span data-stu-id="1f4c6-119">Users can sign up for your application using their Azure AD account via a familiar consent experience similar to those found in social media and mobile applications.</span></span>  <span data-ttu-id="1f4c6-120">任何使用者都可以註冊並登入已與 Azure AD 整合的應用程式，而無需 IT 人員的介入。</span><span class="sxs-lookup"><span data-stu-id="1f4c6-120">Any user can sign up and sign in to an application that is integrated with Azure AD without requiring IT involvement.</span></span>  <span data-ttu-id="1f4c6-121">深入了解[註冊應用程式以進行 Azure AD 帳戶登入](../../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md)。</span><span class="sxs-lookup"><span data-stu-id="1f4c6-121">Learn more about [signing-up your application for Azure AD Account login](../../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).</span></span>

### <a name="browse-for-users-manage-user-provisioning-and-control-access-to-your-application"></a><span data-ttu-id="1f4c6-122">瀏覽以尋找使用者、管理使用者佈建，及控制存取應用程式</span><span class="sxs-lookup"><span data-stu-id="1f4c6-122">Browse for Users, Manage User Provisioning, and Control Access to Your Application</span></span>
<span data-ttu-id="1f4c6-123">**瀏覽以尋找目錄中的使用者。**</span><span class="sxs-lookup"><span data-stu-id="1f4c6-123">**Browse for users in the directory.**</span></span>  <span data-ttu-id="1f4c6-124">邀請他人或授與存取權限時，與其要求使用者輸入電子郵件位址，您可以使用 Graph API 來協助使用者搜尋及瀏覽以尋找組織中的其他人。</span><span class="sxs-lookup"><span data-stu-id="1f4c6-124">Use the Graph API to help users search and browse for other people in their organization when inviting others or granting access, instead of requiring them to type email addresses.</span></span>  <span data-ttu-id="1f4c6-125">使用者可以使用常見的通訊錄樣式介面進行瀏覽，包括檢視組織階層的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="1f4c6-125">Users can browse using a familiar address book style interface, including viewing the details of the organizational hierarchy.</span></span>  <span data-ttu-id="1f4c6-126">深入了解[圖形 API](active-directory-graph-api.md)。</span><span class="sxs-lookup"><span data-stu-id="1f4c6-126">Learn more about the [Graph API](active-directory-graph-api.md).</span></span>

<span data-ttu-id="1f4c6-127">**重複使用您的客戶已經在管理的 Active Directory 群組與通訊群組清單。**</span><span class="sxs-lookup"><span data-stu-id="1f4c6-127">**Re-use Active Directory groups and distribution lists your customer is already managing.**</span></span>  <span data-ttu-id="1f4c6-128">Azure AD 包含您的客戶已經用於電子郵件通訊群組和管理存取的群組。</span><span class="sxs-lookup"><span data-stu-id="1f4c6-128">Azure AD contains the groups that your customer is already using for email distribution and managing access.</span></span>  <span data-ttu-id="1f4c6-129">使用 Graph API，與其要求您的客戶在應用程式中建立和管理一組個別的群組，您可以重複使用這些群組。</span><span class="sxs-lookup"><span data-stu-id="1f4c6-129">Using the Graph API, re-use these groups instead of requiring your customer to create and manage a separate set of groups in your application.</span></span>  <span data-ttu-id="1f4c6-130">群組資訊也可以透過登入權杖傳送至您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="1f4c6-130">Group information can also be sent to your application in sign in tokens.</span></span>  <span data-ttu-id="1f4c6-131">深入了解[圖形 API](active-directory-graph-api.md)。</span><span class="sxs-lookup"><span data-stu-id="1f4c6-131">Learn more about the [Graph API](active-directory-graph-api.md).</span></span>

<span data-ttu-id="1f4c6-132">**使用 Azure AD 來控制有權存取應用程式的人員。**</span><span class="sxs-lookup"><span data-stu-id="1f4c6-132">**Use Azure AD to control who has access to your application.**</span></span>  <span data-ttu-id="1f4c6-133">系統管理員和 Azure AD 中的應用程式擁有者可以將應用程式的存取權限指派給特定使用者和群組。</span><span class="sxs-lookup"><span data-stu-id="1f4c6-133">Administrators and application owners in Azure AD can assign access to applications to specific users and groups.</span></span>  <span data-ttu-id="1f4c6-134">使用 Graph API，您可以讀取這份清單並用它來控制資源的佈建和取消佈建，以及應用程式內的存取。</span><span class="sxs-lookup"><span data-stu-id="1f4c6-134">Using the Graph API, you can read this list and use it to control provisioning and de-provisioning of resources and access within your application.</span></span>

<span data-ttu-id="1f4c6-135">**使用 Azure AD 進行角色型存取控制。**</span><span class="sxs-lookup"><span data-stu-id="1f4c6-135">**Use Azure AD for Roles Based Access Control.**</span></span>  <span data-ttu-id="1f4c6-136">系統管理員和應用程式擁有者可以將使用者和群組指派至您在 Azure AD 中註冊應用程式時所定義的角色。</span><span class="sxs-lookup"><span data-stu-id="1f4c6-136">Administrators and application owners can assign users and groups to roles that you define when you register your application in Azure AD.</span></span>  <span data-ttu-id="1f4c6-137">角色資訊會透過登入權杖傳送至您的應用程式，並可使用 Graph API 進行讀取。</span><span class="sxs-lookup"><span data-stu-id="1f4c6-137">Role information is sent to your application in sign in tokens and can also be read using the Graph API.</span></span>  <span data-ttu-id="1f4c6-138">深入了解 [使用 Azure AD 進行授權](http://blogs.technet.com/b/ad/archive/2014/12/18/azure-active-directory-now-with-group-claims-and-application-roles.aspx)。</span><span class="sxs-lookup"><span data-stu-id="1f4c6-138">Learn more about [using Azure AD for authorization](http://blogs.technet.com/b/ad/archive/2014/12/18/azure-active-directory-now-with-group-claims-and-application-roles.aspx).</span></span>

### <a name="get-access-to-users-profile-calendar-email-contacts-files-and-more"></a><span data-ttu-id="1f4c6-139">取得使用者設定檔、行事曆、電子郵件、連絡人、檔案及其他等存取權限</span><span class="sxs-lookup"><span data-stu-id="1f4c6-139">Get Access to User's Profile, Calendar, Email, Contacts, Files, and More</span></span>
<span data-ttu-id="1f4c6-140">**Azure AD 是 Office 365 和其他 Microsoft 商務服務的授權伺服器。**</span><span class="sxs-lookup"><span data-stu-id="1f4c6-140">**Azure AD is the authorization server for Office 365 and other Microsoft business services.**</span></span>  <span data-ttu-id="1f4c6-141">如果您的應用程式支援 Azure AD 登入，或支援使用 OAuth 2.0 將目前使用者帳戶連結至 Azure AD 使用者帳戶，則您可以要求使用者設定檔、行事曆、電子郵件、連絡人、檔案及其他資訊的讀取和寫入存取權限。</span><span class="sxs-lookup"><span data-stu-id="1f4c6-141">If you support Azure AD for sign in to your application or support linking your current user accounts to Azure AD user accounts using OAuth 2.0, you can request read and write access to a user's profile, calendar, email, contacts, files, and other information.</span></span>  <span data-ttu-id="1f4c6-142">您可以順利地將事件寫入使用者的行事曆，並讀取檔案或將檔案寫入使用者的 OneDrive。</span><span class="sxs-lookup"><span data-stu-id="1f4c6-142">You can seamlessly write events to user's calendar, and read or write files to their OneDrive.</span></span>  <span data-ttu-id="1f4c6-143">深入了解 [存取 Office 365 API](https://msdn.microsoft.com/office/office365/howto/platform-development-overview)。</span><span class="sxs-lookup"><span data-stu-id="1f4c6-143">Learn more about [accessing the Office 365 APIs](https://msdn.microsoft.com/office/office365/howto/platform-development-overview).</span></span>

### <a name="promote-your-application-in-the-azure-and-office-365-marketplaces"></a><span data-ttu-id="1f4c6-144">在 Azure 和 Office 365 Marketplace 中推廣您的應用程式</span><span class="sxs-lookup"><span data-stu-id="1f4c6-144">Promote Your Application in the Azure and Office 365 Marketplaces</span></span>
<span data-ttu-id="1f4c6-145">**將您的應用程式擴廣到數百萬個已使用 Azure AD 的組織。**</span><span class="sxs-lookup"><span data-stu-id="1f4c6-145">**Promote your application to the millions of organizations who are already using Azure AD.**</span></span>  <span data-ttu-id="1f4c6-146">搜尋和瀏覽 Marketplace 的使用者已經使用一或多項雲端服務，讓他們成為合格的雲端服務客戶。</span><span class="sxs-lookup"><span data-stu-id="1f4c6-146">Users who search and browse these marketplaces are already using one or more cloud services, making them qualified cloud service customers.</span></span>  <span data-ttu-id="1f4c6-147">深入了解如何在 [Azure Marketplace](https://azure.microsoft.com/marketplace/partner-program/)中推廣您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="1f4c6-147">Learn more about promoting your application in [the Azure Marketplace](https://azure.microsoft.com/marketplace/partner-program/).</span></span>

<span data-ttu-id="1f4c6-148">**當使用者註冊您的應用程式時，它便會出現在其 Azure AD 存取面板和 Office 365 應用程式啟動程式中。**</span><span class="sxs-lookup"><span data-stu-id="1f4c6-148">**When users sign up for your application, it will appear in their Azure AD access panel and Office 365 app launcher.**</span></span>  <span data-ttu-id="1f4c6-149">使用者將能夠迅速且輕鬆地返回您的應用程式，以增加使用者參與度。</span><span class="sxs-lookup"><span data-stu-id="1f4c6-149">Users will be able to quickly and easily return to your application later, improving user engagement.</span></span>  <span data-ttu-id="1f4c6-150">深入了解 [Azure AD 存取面板](../active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="1f4c6-150">Learn more about the [Azure AD access panel](../active-directory-saas-access-panel-introduction.md).</span></span>

### <a name="secure-device-to-service-and-service-to-service-communication"></a><span data-ttu-id="1f4c6-151">保護裝置對服務和服務對服務通訊的安全</span><span class="sxs-lookup"><span data-stu-id="1f4c6-151">Secure Device-to-Service and Service-to-Service Communication</span></span>
<span data-ttu-id="1f4c6-152">**使用 Azure AD 進行服務和裝置的身分識別管理，可減少您需要撰寫的程式碼，並可讓 IT 管理存取權限。**</span><span class="sxs-lookup"><span data-stu-id="1f4c6-152">**Using Azure AD for identity management of services and devices reduces the code you need to write and enables IT to manage access.**</span></span>  <span data-ttu-id="1f4c6-153">服務與裝置可以使用 OAuth 取得 Azure AD 的權杖，並使用這些權杖來存取 Web API。</span><span class="sxs-lookup"><span data-stu-id="1f4c6-153">Services and devices can get tokens from Azure AD using OAuth and use those tokens to access web APIs.</span></span>  <span data-ttu-id="1f4c6-154">使用 Azure AD，您可以避免撰寫複雜的驗證程式碼。</span><span class="sxs-lookup"><span data-stu-id="1f4c6-154">Using Azure AD you can avoid writing complex authentication code.</span></span>  <span data-ttu-id="1f4c6-155">因為服務和裝置的身分識別會儲存在 Azure AD 中，IT 可以在同一個地方管理金鑰和撤銷，而無需在您的應用程式中分別執行此動作。</span><span class="sxs-lookup"><span data-stu-id="1f4c6-155">Since the identities of the services and devices are stored in Azure AD, IT can manage keys and revocation in one place instead of having to do this separately in your application.</span></span>

## <a name="benefits-of-integration"></a><span data-ttu-id="1f4c6-156">整合的優點</span><span class="sxs-lookup"><span data-stu-id="1f4c6-156">Benefits of Integration</span></span>
<span data-ttu-id="1f4c6-157">與 Azure AD 整合帶來您無需撰寫額外程式碼的優點。</span><span class="sxs-lookup"><span data-stu-id="1f4c6-157">Integration with Azure AD comes with benefits that do not require you to write additional code.</span></span>

### <a name="integration-with-enterprise-identity-management"></a><span data-ttu-id="1f4c6-158">與企業身分識別管理整合</span><span class="sxs-lookup"><span data-stu-id="1f4c6-158">Integration with Enterprise Identity Management</span></span>
<span data-ttu-id="1f4c6-159">**協助您的應用程式符合 IT 原則。**</span><span class="sxs-lookup"><span data-stu-id="1f4c6-159">**Help your application comply with IT policies.**</span></span>  <span data-ttu-id="1f4c6-160">組織會將其企業身分識別管理系統與 Azure AD 整合，所以當某人離開組織時，它們會自動喪失對應用程式的存取權限，而且 IT 無需採取額外步驟。</span><span class="sxs-lookup"><span data-stu-id="1f4c6-160">Organizations integrate their enterprise identity management systems with Azure AD, so when a person leaves an organization, they will automatically lose access to your application without IT needing to take extra steps.</span></span>  <span data-ttu-id="1f4c6-161">IT 可以管理誰可以存取您的應用程式，並判斷需要哪些存取原則 (例如，多因素驗證)，以降低撰寫程式碼以符合複雜公司原則的需求。</span><span class="sxs-lookup"><span data-stu-id="1f4c6-161">IT can manage who can access your application and determine what access policies are required - for example multi-factor authentication - reducing your need to write code to comply with complex corporate policies.</span></span>  <span data-ttu-id="1f4c6-162">Azure AD 提供系統管理員詳盡的稽核記錄，內容包括登入應用程式的使用者，以便 IT 可以追蹤使用情況。</span><span class="sxs-lookup"><span data-stu-id="1f4c6-162">Azure AD provides administrators with a detailed audit log of who signed in to your application so IT can track usage.</span></span>

<span data-ttu-id="1f4c6-163">**Azure AD 將 Active Directory 延伸到雲端，讓您的應用程式可以與 AD 整合。**</span><span class="sxs-lookup"><span data-stu-id="1f4c6-163">**Azure AD extends Active Directory to the cloud so that your application can integrate with AD.**</span></span>  <span data-ttu-id="1f4c6-164">世界各地許多組織使用 Active Directory 作為其主要登入和身分識別管理系統，並要求他們的應用程式使用 AD。</span><span class="sxs-lookup"><span data-stu-id="1f4c6-164">Many organizations around the world use Active Directory as their principal sign-in and identity management system, and require their applications to work with AD.</span></span>  <span data-ttu-id="1f4c6-165">與 Azure AD 整合即可將 Active Directory 和您的應用程式整合。</span><span class="sxs-lookup"><span data-stu-id="1f4c6-165">Integrating with Azure AD integrates your app with Active Directory.</span></span>

### <a name="advanced-security-features"></a><span data-ttu-id="1f4c6-166">進階的安全性功能</span><span class="sxs-lookup"><span data-stu-id="1f4c6-166">Advanced Security Features</span></span>
<span data-ttu-id="1f4c6-167">**多因素驗證。**</span><span class="sxs-lookup"><span data-stu-id="1f4c6-167">**Multi-factor authentication.**</span></span>  <span data-ttu-id="1f4c6-168">Azure AD 提供原生多因素驗證。</span><span class="sxs-lookup"><span data-stu-id="1f4c6-168">Azure AD provides native multi-factor authentication.</span></span>  <span data-ttu-id="1f4c6-169">IT 系統管理員可以要求多因素驗證才能存取應用程式，因此您無需自行撰寫這項支援的程式碼。</span><span class="sxs-lookup"><span data-stu-id="1f4c6-169">IT administrators can require multi-factor authentication to access your application, so that you do not have to code this support yourself.</span></span>  <span data-ttu-id="1f4c6-170">深入了解 [多因素驗證](https://azure.microsoft.com/documentation/services/multi-factor-authentication/)。</span><span class="sxs-lookup"><span data-stu-id="1f4c6-170">Learn more about [Multi-Factor Authentication](https://azure.microsoft.com/documentation/services/multi-factor-authentication/).</span></span>

<span data-ttu-id="1f4c6-171">**登入偵測異常。**</span><span class="sxs-lookup"><span data-stu-id="1f4c6-171">**Anomalous sign in detection.**</span></span>  <span data-ttu-id="1f4c6-172">Azure AD 每天處理超過 10 億個登入，同時使用機器學習演算法來偵測可疑活動，並向 IT 系統管理員通知可能發生的問題。</span><span class="sxs-lookup"><span data-stu-id="1f4c6-172">Azure AD processes more than a billion sign-ins a day, while using machine learning algorithms to detect suspicious activity and notify IT administrators of possible problems.</span></span>  <span data-ttu-id="1f4c6-173">藉由支援 Azure AD 登入，您的應用程式便會獲得這項保護的好處。</span><span class="sxs-lookup"><span data-stu-id="1f4c6-173">By supporting Azure AD sign-in, your application gets the benefit of this protection.</span></span> <span data-ttu-id="1f4c6-174">深入了解[檢視 Azure Active Directory 存取報告](../active-directory-view-access-usage-reports.md)。</span><span class="sxs-lookup"><span data-stu-id="1f4c6-174">Learn more about [viewing Azure Active Directory access report](../active-directory-view-access-usage-reports.md).</span></span>

<span data-ttu-id="1f4c6-175">**條件式存取。**</span><span class="sxs-lookup"><span data-stu-id="1f4c6-175">**Conditional access.**</span></span>  <span data-ttu-id="1f4c6-176">除了多因素驗證，系統管理員還可以要求使用者在登入您的應用程式之前必須符合特定條件。</span><span class="sxs-lookup"><span data-stu-id="1f4c6-176">In addition to multi-factor authentication, administrators can require specific conditions be met before users can sign-in to your application.</span></span>  <span data-ttu-id="1f4c6-177">可以設定的條件包括用戶端裝置的 IP 位址範圍、指定群組的成員資格，以及用於存取的裝置狀態。</span><span class="sxs-lookup"><span data-stu-id="1f4c6-177">Conditions that can be set include the IP address range of client devices, membership in specified groups, and the state of the device being used for access.</span></span>  <span data-ttu-id="1f4c6-178">深入了解 [Azure Active Directory 條件式存取](../active-directory-conditional-access.md)。</span><span class="sxs-lookup"><span data-stu-id="1f4c6-178">Learn more about [Azure Active Directory conditional access](../active-directory-conditional-access.md).</span></span>

### <a name="easy-development"></a><span data-ttu-id="1f4c6-179">容易開發</span><span class="sxs-lookup"><span data-stu-id="1f4c6-179">Easy Development</span></span>
<span data-ttu-id="1f4c6-180">**業界標準通訊協定。**</span><span class="sxs-lookup"><span data-stu-id="1f4c6-180">**Industry standard protocols.**</span></span>  <span data-ttu-id="1f4c6-181">Microsoft 致力於支援業界標準。</span><span class="sxs-lookup"><span data-stu-id="1f4c6-181">Microsoft is committed to supporting industry standards.</span></span>  <span data-ttu-id="1f4c6-182">Azure AD 支援 SAML 2.0、OpenID Connect 1.0、OAuth 2.0 和 WS 同盟 1.2 驗證通訊協定。</span><span class="sxs-lookup"><span data-stu-id="1f4c6-182">Azure AD supports the SAML 2.0, OpenID Connect 1.0, OAuth 2.0, and WS-Federation 1.2 authentication protocols.</span></span>  <span data-ttu-id="1f4c6-183">Graph API 屬於 OData 4.0 標準。</span><span class="sxs-lookup"><span data-stu-id="1f4c6-183">The Graph API is OData 4.0 compliant.</span></span>  <span data-ttu-id="1f4c6-184">如果您的應用程式已經支援 SAML 2.0 或 OpenID Connect 1.0 通訊協定的同盟登入，那新增 Azure AD 支援便相當直接。</span><span class="sxs-lookup"><span data-stu-id="1f4c6-184">If your application already supports the SAML 2.0 or OpenID Connect 1.0 protocols for federated sign in, adding support for Azure AD can be straightforward.</span></span>  <span data-ttu-id="1f4c6-185">深入了解 [Azure AD 支援的驗證通訊協定](active-directory-authentication-protocols.md)。</span><span class="sxs-lookup"><span data-stu-id="1f4c6-185">Learn more about [Azure AD supported authentication protocols](active-directory-authentication-protocols.md).</span></span>

<span data-ttu-id="1f4c6-186">**開放原始碼程式庫。**</span><span class="sxs-lookup"><span data-stu-id="1f4c6-186">**Open source libraries.**</span></span>  <span data-ttu-id="1f4c6-187">Microsoft 針對常用的語言和平台提供完整支援的開放原始碼程式庫，進而加快開發速度。</span><span class="sxs-lookup"><span data-stu-id="1f4c6-187">Microsoft provides fully supported open source libraries for popular languages and platforms to speed development.</span></span>  <span data-ttu-id="1f4c6-188">原始碼採用 Apache 2.0 授權，您可以任何分岔以及貢獻回饋給專案。</span><span class="sxs-lookup"><span data-stu-id="1f4c6-188">The source code is licensed under Apache 2.0, and you are free to fork and contribute back to the projects.</span></span>  <span data-ttu-id="1f4c6-189">深入了解 [Azure AD 驗證程式庫](active-directory-authentication-libraries.md)。</span><span class="sxs-lookup"><span data-stu-id="1f4c6-189">Learn more about [Azure AD authentication libraries](active-directory-authentication-libraries.md).</span></span>

### <a name="worldwide-presence-and-high-availability"></a><span data-ttu-id="1f4c6-190">全球的目前狀態和高可用性</span><span class="sxs-lookup"><span data-stu-id="1f4c6-190">Worldwide Presence and High Availability</span></span>
<span data-ttu-id="1f4c6-191">**Azure AD 會在世界各地的資料中心內進行部署，並受到全天候的管理和監控。**</span><span class="sxs-lookup"><span data-stu-id="1f4c6-191">**Azure AD is deployed in datacenters around the world and is managed and monitored around the clock.**</span></span>  <span data-ttu-id="1f4c6-192">Azure AD 是適用於 Microsoft Azure 和 Office 365 的身分識別管理系統，並在世界各地的 28 個資料中心內進行部署。</span><span class="sxs-lookup"><span data-stu-id="1f4c6-192">Azure AD is the identity management system for Microsoft Azure and Office 365 and is deployed in 28 datacenters around the world.</span></span>  <span data-ttu-id="1f4c6-193">保證將目錄資料複寫到至少三個資料中心。</span><span class="sxs-lookup"><span data-stu-id="1f4c6-193">Directory data is guaranteed to be replicated to at least three datacenters.</span></span>  <span data-ttu-id="1f4c6-194">全域負載平衡器會確保使用者可存取包含其資料的最接近 Azure AD 複本，並在偵測到問題時，自動將要求重新路由到其他資料中心。</span><span class="sxs-lookup"><span data-stu-id="1f4c6-194">Global load balancers ensure users access the closest copy of Azure AD containing their data, and automatically re-route requests to other datacenters if a problem is detected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1f4c6-195">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1f4c6-195">Next Steps</span></span>
<span data-ttu-id="1f4c6-196">[開始撰寫程式碼](active-directory-developers-guide.md#get-started)</span><span class="sxs-lookup"><span data-stu-id="1f4c6-196">[Get started writing code](active-directory-developers-guide.md#get-started).</span></span>

[<span data-ttu-id="1f4c6-197">使用 Azure AD 登入使用者</span><span class="sxs-lookup"><span data-stu-id="1f4c6-197">Sign Users In Using Azure AD</span></span>](active-directory-authentication-scenarios.md)
