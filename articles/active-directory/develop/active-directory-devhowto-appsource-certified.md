---
title: "如何讓 AppSource 取得 Azure Active Directory (AD) 認證 | Microsoft Docs"
description: "有關如何讓應用程式 AppSource 取得 Azure Active Directory 認證的詳細資料。"
services: active-directory
documentationcenter: 
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 21206407-49f8-4c0b-84d1-c25e17cd4183
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/03/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: d8e2f8fc19ff879e6a7b632f033fd0ed9d77392a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-get-appsource-certified-for-azure-active-directory"></a><span data-ttu-id="7c4d2-103">如何讓 AppSource 取得 Azure Active Directory 認證</span><span class="sxs-lookup"><span data-stu-id="7c4d2-103">How to get AppSource Certified for Azure Active Directory</span></span>
<span data-ttu-id="7c4d2-104">[Microsoft AppSource](https://appsource.microsoft.com/) 是企業用戶探索、嘗試，及管理企業營運 SaaS 應用程式 (獨立 SaaS 和現有 Microsoft SaaS 產品的附加元件) 的目的地。</span><span class="sxs-lookup"><span data-stu-id="7c4d2-104">[Microsoft AppSource](https://appsource.microsoft.com/) is a destination for business users to discover, try, and manage line-of-business SaaS applications (standalone SaaS and add-on to existing Microsoft SaaS products).</span></span>

<span data-ttu-id="7c4d2-105">若要列出 AppSource 上獨立的 SaaS 應用程式，您的應用程式必須接受來自具備 Azure Active Directory 之任何公司或組織的公司帳戶的單一登入。</span><span class="sxs-lookup"><span data-stu-id="7c4d2-105">To list a standalone SaaS application on AppSource, your application must accept single sign-on from work accounts from any company or organization that has Azure Active Directory.</span></span> <span data-ttu-id="7c4d2-106">登入流程必須使用 [OpenID Connect](./active-directory-protocols-openid-connect-code.md) 或 [OAuth 2.0](./active-directory-protocols-oauth-code.md) 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="7c4d2-106">The sign-in process must use the [OpenID Connect](./active-directory-protocols-openid-connect-code.md) or [OAuth 2.0](./active-directory-protocols-oauth-code.md) protocols.</span></span> <span data-ttu-id="7c4d2-107">AppSource 認證不接受 SAML 整合。</span><span class="sxs-lookup"><span data-stu-id="7c4d2-107">SAML integration is not accepted for AppSource certification.</span></span>

## <a name="guides-and-code-samples"></a><span data-ttu-id="7c4d2-108">指南與程式碼範例</span><span class="sxs-lookup"><span data-stu-id="7c4d2-108">Guides and code samples</span></span>
<span data-ttu-id="7c4d2-109">如果您想要了解如何使用 Open ID connect 將您的應用程式與 Azure Active Directory 整合，請遵循 [Azure Active Directory 開發人員指南](./active-directory-developers-guide.md#get-started "開始使用適用於開發人員的 Azure AD") 中的指南和程式碼範例。</span><span class="sxs-lookup"><span data-stu-id="7c4d2-109">If you want to learn about how to integrate your application with Azure Active Directory using Open ID connect, follow our guides and code samples in the [Azure Active Directory developer's guide](./active-directory-developers-guide.md#get-started "Get Started with Azure AD for developers").</span></span>

## <a name="multi-tenant-applications"></a><span data-ttu-id="7c4d2-110">多租用戶應用程式</span><span class="sxs-lookup"><span data-stu-id="7c4d2-110">Multi-tenant applications</span></span>

<span data-ttu-id="7c4d2-111">此應用程式接受來自具備 Azure Active Directory 之公司或組織的使用者的單一登入，不需要稱為*多租用戶應用程式*的個別執行個體、設定或部署。</span><span class="sxs-lookup"><span data-stu-id="7c4d2-111">An application that accepts sign-ins from users from any company or organization that have Azure Active Directory without requiring a separate instance, configuration, or deployment is known as a *multi-tenant application*.</span></span> <span data-ttu-id="7c4d2-112">AppSource 建議應用程式實行多重租用，以啟用*單鍵*免費試用體驗。</span><span class="sxs-lookup"><span data-stu-id="7c4d2-112">AppSource recommends that applications implement multi-tenancy to enable the *single-click* free trial experience.</span></span>

<span data-ttu-id="7c4d2-113">若要在您的應用程式上啟用多重租用：</span><span class="sxs-lookup"><span data-stu-id="7c4d2-113">In order to enable multi-tenancy on your application:</span></span>
- <span data-ttu-id="7c4d2-114">在 [Azure 入口網站](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps) 的應用程式註冊資訊中，將 `Multi-Tenanted` 屬性設為 `Yes` (依預設，Azure 入口網站中建立的應用程式會設為*單一租用戶*)</span><span class="sxs-lookup"><span data-stu-id="7c4d2-114">Set `Multi-Tenanted` property to `Yes` on your application registration's information in the [Azure Portal](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps) (by default, applications created in the Azure Portal are configured as *single-tenant*)</span></span>
- <span data-ttu-id="7c4d2-115">更新您的程式碼，以傳送要求至 '`common`' 端點 (將來自 *https://login.microsoftonline.com/{yourtenant}* 的端點更新為 *https://login.microsoftonline.com/common*)</span><span class="sxs-lookup"><span data-stu-id="7c4d2-115">Update your code to send requests to the '`common`' endpoint (update the endpoint from *https://login.microsoftonline.com/{yourtenant}* to *https://login.microsoftonline.com/common*)</span></span>
- <span data-ttu-id="7c4d2-116">在特定平台上 (例如 ASP.NET)，您還需要更新程式碼，以接受多個簽發者</span><span class="sxs-lookup"><span data-stu-id="7c4d2-116">For some platforms, like ASP.NET, you need also to update your code to accept multiple issuers</span></span>

<span data-ttu-id="7c4d2-117">如需多重租用的詳細資訊，請參閱：[如何使用多租用戶應用程式模式登入任何 Azure Active Directory (AD) 使用者](./active-directory-devhowto-multi-tenant-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="7c4d2-117">For more information about multi-tenancy, see: [How to sign in any Azure Active Directory (AD) user using the multi-tenant application pattern](./active-directory-devhowto-multi-tenant-overview.md).</span></span>

### <a name="single-tenant-applications"></a><span data-ttu-id="7c4d2-118">單一租用戶應用程式</span><span class="sxs-lookup"><span data-stu-id="7c4d2-118">Single-tenant applications</span></span>
<span data-ttu-id="7c4d2-119">此應用程式僅接受來自定義之 Azure Active Directory 執行個體 (稱為*單一租用戶應用程式*) 的使用者登入。</span><span class="sxs-lookup"><span data-stu-id="7c4d2-119">Applications that only accept sign-ins from users of a defined Azure Active Directory instance are known as *single-tenant application*.</span></span> <span data-ttu-id="7c4d2-120">將每個使用者以*來賓帳戶*的身分新增至應用程式註冊的 Azure Active Directory 執行個體之後，外部使用者 (包括來自其他組織的公司或學校帳戶，或個人帳戶) 可以登入單一租用戶應用程式。</span><span class="sxs-lookup"><span data-stu-id="7c4d2-120">External users (including Work or School accounts from other organizations, or personal account) can sign in to a single-tenant application after adding each user as *guest account* to the Azure Active Directory instance that the application is registered.</span></span> <span data-ttu-id="7c4d2-121">您可以透過 [*Azure AD B2B 共同作業*](../active-directory-b2b-what-is-azure-ad-b2b.md)將使用者以來賓帳戶的身分新增至 Azure Active Directory - 而且可以使用[程式設計的方式](../active-directory-b2b-code-samples.md)來完成。</span><span class="sxs-lookup"><span data-stu-id="7c4d2-121">You can add users as guest accounts to an Azure Active Directory via the [*Azure AD B2B collaboration*](../active-directory-b2b-what-is-azure-ad-b2b.md) - and it can be done [programatically](../active-directory-b2b-code-samples.md).</span></span> <span data-ttu-id="7c4d2-122">當您以來賓帳戶的身分，將使用者新增至 Azure Active Directory 時，會向使用者寄送邀請電子郵件，使用者必須按一下邀請電子郵件中的連結，才可接受邀請。</span><span class="sxs-lookup"><span data-stu-id="7c4d2-122">When you add a user as guest account to an Azure Active Directory, an invitation email is sent to the user, who has to accept the invitation by clicking on the link in the invitation email.</span></span> <span data-ttu-id="7c4d2-123">如果傳送邀請給邀請組織中的其他使用者也屬於合作夥伴組織的成員，則不需要接受邀請即可登入。</span><span class="sxs-lookup"><span data-stu-id="7c4d2-123">Invitations that are sent to an additional user in an inviting organization that is also a member of the partner organization are not required to accept an invitation to sign in.</span></span>

<span data-ttu-id="7c4d2-124">單一租用戶應用程式可啟用*與我連絡*體驗，但如果您想要啟用 AppSource 建議的單鍵/免費試用體驗，可改在您的應用程式上啟用多重租用。</span><span class="sxs-lookup"><span data-stu-id="7c4d2-124">Single-tenant applications can enable the *Contact Me* experience, but if you want to enable the single-click/ free trial experience that AppSource recommends, enable multi-tenancy on your application instead.</span></span>


## <a name="appsource-trial-experiences"></a><span data-ttu-id="7c4d2-125">AppSource 試用體驗</span><span class="sxs-lookup"><span data-stu-id="7c4d2-125">AppSource trial experiences</span></span>

### <a name="free-trial-customer-led-trial-experience"></a><span data-ttu-id="7c4d2-126">免費試用 (以客戶為導向的試用體驗)</span><span class="sxs-lookup"><span data-stu-id="7c4d2-126">Free Trial (Customer-led trial experience)</span></span> 
<span data-ttu-id="7c4d2-127">*以客戶為導向的試用*是 AppSource 建議的體驗，因為可提供單鍵存取至您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="7c4d2-127">The *customer-led trial* is the experience that AppSource recommends as it offers a single-click access to your application.</span></span> <span data-ttu-id="7c4d2-128">這項體驗看起來如下圖：</span><span class="sxs-lookup"><span data-stu-id="7c4d2-128">Below an illustration of how this experience looks like:</span></span><br/><br/>

<table >
<tr>
    <td valign="top" width="33%">1.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step1.png" width="85%"/><ul><li><span data-ttu-id="7c4d2-129">使用者會在 AppSource 網站中尋找您的應用程式</span><span class="sxs-lookup"><span data-stu-id="7c4d2-129">User finds your application in AppSource Web Site</span></span></li><li><span data-ttu-id="7c4d2-130">選取 [免費試用] 選項</span><span class="sxs-lookup"><span data-stu-id="7c4d2-130">Selects ‘Free trial’ option</span></span></li></ul></td>
    <td valign="top" width="33%">2.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step2.png" width="85%" /><ul><li><span data-ttu-id="7c4d2-131">AppSource 將使用者重新導向至網站中的 URL</span><span class="sxs-lookup"><span data-stu-id="7c4d2-131">AppSource redirects user to a URL in your web site</span></span></li><li><span data-ttu-id="7c4d2-132">您的網站會自動啟動<i>單一登入</i>流程 (在頁面載入時)</span><span class="sxs-lookup"><span data-stu-id="7c4d2-132">Your web site starts the <i>single-sign-on</i> process automatically (on page load)</span></span></li></ul></td>
    <td valign="top" width="33%">3.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step3.png" width="85%"/><ul><li><span data-ttu-id="7c4d2-133">使用者已重新導向至 Microsoft 登入頁面</span><span class="sxs-lookup"><span data-stu-id="7c4d2-133">User is redirected to Microsoft Sign-in page</span></span></li><li><span data-ttu-id="7c4d2-134">使用者提供認證以登入</span><span class="sxs-lookup"><span data-stu-id="7c4d2-134">User provides credentials to sign in</span></span></li></ul></td>
</tr>
<tr>
    <td valign="top" width="33%">4.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step4.png" width="85%"/><ul><li><span data-ttu-id="7c4d2-135">使用者同意您的應用程式</span><span class="sxs-lookup"><span data-stu-id="7c4d2-135">User gives consent for your application</span></span></li></ul></td>
    <td valign="top" width="33%">5.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step5.png" width="85%"/><ul><li><span data-ttu-id="7c4d2-136">登入完成，而且使用者已重新導向回到您的網站</span><span class="sxs-lookup"><span data-stu-id="7c4d2-136">Sign-in completes and user is redirected back to your web site</span></span></li><li><span data-ttu-id="7c4d2-137">使用者啟動免費試用</span><span class="sxs-lookup"><span data-stu-id="7c4d2-137">User starts the free trial</span></span></li></ul></td>
    <td></td>
</tr>
</table>

### <a name="contact-me-partner-led-trial-experience"></a><span data-ttu-id="7c4d2-138">與我連絡 (以合作夥伴為導向的試用體驗)</span><span class="sxs-lookup"><span data-stu-id="7c4d2-138">Contact Me (Partner-led trial experience)</span></span>
<span data-ttu-id="7c4d2-139">需要手動或長期操作來佈建使用者/公司時，可使用*合作夥伴試用體驗*：例如，您的應用程式需要佈建虛擬機器、資料庫執行個體，或需要很多時間完成的作業的時候。</span><span class="sxs-lookup"><span data-stu-id="7c4d2-139">The *partner trial experience* can be used when a manual or a long-term operation needs to happen to provision the user/ company: for example, your application needs to provision virtual machines, database instances, or operations that take much time to complete.</span></span> <span data-ttu-id="7c4d2-140">在此情況下，使用者選取 [要求試用] 按鈕並填寫表單之後，AppSource 會傳送給您使用者的連絡資訊。</span><span class="sxs-lookup"><span data-stu-id="7c4d2-140">In this case, after user selects the *'Request Trial'* button and fills out a form, AppSource sends you the user's contact information.</span></span> <span data-ttu-id="7c4d2-141">收到此資訊後，您將佈建環境，並將如何存取試用體驗的指示傳送給使用者：</span><span class="sxs-lookup"><span data-stu-id="7c4d2-141">Upon receiving this information, you then provision the environment and send the instructions to the user on how to access the trial experience:</span></span><br/><br/>

<table valign="top">
<tr>
    <td valign="top" width="33%">1.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step1.png" width="85%"/><ul><li><span data-ttu-id="7c4d2-142">使用者會在 AppSource 網站中尋找您的應用程式</span><span class="sxs-lookup"><span data-stu-id="7c4d2-142">User finds your application in AppSource web site</span></span></li><li><span data-ttu-id="7c4d2-143">選取 [與我連絡] 選項</span><span class="sxs-lookup"><span data-stu-id="7c4d2-143">Selects ‘Contact Me’ option</span></span></li></ul></td>
    <td valign="top" width="33%">2.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step2.png" width="85%"/><ul><li><span data-ttu-id="7c4d2-144">將連絡人資訊填入表單</span><span class="sxs-lookup"><span data-stu-id="7c4d2-144">Fills out a form with contact information</span></span></li></ul></td>
     <td valign="top" width="33%">3.<br/><br/>
        <table bgcolor="#f7f7f7">
        <tr>
            <td><img src="media/active-directory-devhowto-appsource-certified/UserContact.png" width="55%"/></td>
            <td><span data-ttu-id="7c4d2-145">您會收到使用者資訊</span><span class="sxs-lookup"><span data-stu-id="7c4d2-145">You receive user information</span></span></td>
        </tr>
        <tr>
            <td><img src="media/active-directory-devhowto-appsource-certified/SetupEnv.png" width="55%"/></td>
            <td><span data-ttu-id="7c4d2-146">設定環境</span><span class="sxs-lookup"><span data-stu-id="7c4d2-146">Setup environment</span></span></td>
        </tr>
        <tr>
            <td><img src="media/active-directory-devhowto-appsource-certified/ContactCustomer.png" width="55%"/></td>
            <td><span data-ttu-id="7c4d2-147">連絡使用者試用資訊</span><span class="sxs-lookup"><span data-stu-id="7c4d2-147">Contact user with trial info</span></span></td>
        </tr>
        </table><br/><br/>
        <ul><li><span data-ttu-id="7c4d2-148">您收到使用者資訊並設定試用執行個體</span><span class="sxs-lookup"><span data-stu-id="7c4d2-148">You receive user's information and setup trial instance</span></span></li><li><span data-ttu-id="7c4d2-149">將存取您應用程式的超連結傳送給使用者</span><span class="sxs-lookup"><span data-stu-id="7c4d2-149">You send the hyperlink to access your application to the user</span></span></li></ul>
    </td>
</tr>
<tr>
    <td valign="top" width="33%">4.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step3.png" width="85%"/><ul><li><span data-ttu-id="7c4d2-150">使用者存取您的應用程式，並完成單一登入流程</span><span class="sxs-lookup"><span data-stu-id="7c4d2-150">User accesses your application and complete the single-sign-on process</span></span></li></ul></td>
    <td valign="top" width="33%">5.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step4.png" width="85%"/><ul><li><span data-ttu-id="7c4d2-151">使用者同意您的應用程式</span><span class="sxs-lookup"><span data-stu-id="7c4d2-151">User gives consent for your application</span></span></li></ul></td>
    <td valign="top" width="33%">6.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step5.png" width="85%"/><ul><li><span data-ttu-id="7c4d2-152">登入完成，而且使用者已重新導向回到您的網站</span><span class="sxs-lookup"><span data-stu-id="7c4d2-152">Sign-in completes and user is redirected back to your web site</span></span></li><li><span data-ttu-id="7c4d2-153">使用者啟動免費試用</span><span class="sxs-lookup"><span data-stu-id="7c4d2-153">User starts the free trial</span></span></li></ul></td>
   
</tr>
</table>

### <a name="more-information"></a><span data-ttu-id="7c4d2-154">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="7c4d2-154">More information</span></span>
<span data-ttu-id="7c4d2-155">如需 AppSource 試用體驗的詳細資訊，請參閱[這段影片](https://aka.ms/trialexperienceforwebapps)。</span><span class="sxs-lookup"><span data-stu-id="7c4d2-155">For more information about the AppSource trial experience, see [this video](https://aka.ms/trialexperienceforwebapps).</span></span> 
 
## <a name="next-steps"></a><span data-ttu-id="7c4d2-156">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7c4d2-156">Next Steps</span></span>

- <span data-ttu-id="7c4d2-157">如需建立支援 Azure Active Directory 登入之應用程式的詳細資訊，請參閱 [Azure AD 的驗證案例](https://docs.microsoft.com/azure/active-directory/develop/active-directory-authentication-scenarios)</span><span class="sxs-lookup"><span data-stu-id="7c4d2-157">For more information on building applications that support Azure Active Directory sign-ins, see [Authentication Scenarios for Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-authentication-scenarios)</span></span> 

- <span data-ttu-id="7c4d2-158">如需如何列出 AppSource 中的 SaaS 應用程式的資訊，請參閱 [AppSource 合作夥伴資訊](https://appsource.microsoft.com/partners)</span><span class="sxs-lookup"><span data-stu-id="7c4d2-158">For information on how to list your SaaS application in AppSource, go see [AppSource Partner Information](https://appsource.microsoft.com/partners)</span></span>


## <a name="get-support"></a><span data-ttu-id="7c4d2-159">取得支援</span><span class="sxs-lookup"><span data-stu-id="7c4d2-159">Get Support</span></span>
<span data-ttu-id="7c4d2-160">對於 Azure Active Directory 整合，我們使用 [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-active-directory) 與社群，以提供支援。</span><span class="sxs-lookup"><span data-stu-id="7c4d2-160">For Azure Active Directory integration, we use [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-active-directory) with the community to provide support.</span></span> 

<span data-ttu-id="7c4d2-161">我們強烈建議您先在 Stack Overflow 上詢問您的問題，並瀏覽現有的問題，以查看先前是否有人已提出您的問題。</span><span class="sxs-lookup"><span data-stu-id="7c4d2-161">We highly recommend you ask your questions on Stack Overflow first and browse existing issues to see if someone has asked your question before.</span></span> <span data-ttu-id="7c4d2-162">請確定您的問題或意見已標記為 `[azure-active-directory]`。</span><span class="sxs-lookup"><span data-stu-id="7c4d2-162">Make sure that your questions or comments are tagged with `[azure-active-directory]`.</span></span>

<span data-ttu-id="7c4d2-163">使用下列意見區段來提供意見反應，並協助我們改善及設計我們的內容。</span><span class="sxs-lookup"><span data-stu-id="7c4d2-163">Use the following comments section to provide feedback and help us refine and shape our content.</span></span>

<!--Reference style links -->
[AAD-Auth-Scenarios]: ./active-directory-authentication-scenarios.md
[AAD-Auth-Scenarios-Browser-To-WebApp]: ./active-directory-authentication-scenarios.md#web-browser-to-web-application
[AAD-Dev-Guide]: ./active-directory-developers-guide.md
[AAD-Howto-Multitenant-Overview]: ./active-directory-devhowto-multi-tenant-overview.md
[AAD-QuickStart-Web-Apps]: ./active-directory-developers-guide.md#get-started


<!--Image references-->