---
title: "aaaHow tooget AppSource 通過 Azure Active Directory |Microsoft 文件"
description: "上如何 tooget AppSource 應用程式通過 Azure Active Directory 的詳細資料。"
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
ms.openlocfilehash: e9f07e9220afcba1120b987122fe770fe5225eed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooget-appsource-certified-for-azure-active-directory"></a><span data-ttu-id="4d11e-103">如何為 Azure Active Directory 的 tooget AppSource 認證</span><span class="sxs-lookup"><span data-stu-id="4d11e-103">How tooget AppSource Certified for Azure Active Directory</span></span>
<span data-ttu-id="4d11e-104">[Microsoft AppSource](https://appsource.microsoft.com/)是目的地商務使用者 toodiscover，再試一次，以及管理 SaaS 應用程式的特定業務 （獨立 SaaS 和附加元件 tooexisting Microsoft SaaS 產品）。</span><span class="sxs-lookup"><span data-stu-id="4d11e-104">[Microsoft AppSource](https://appsource.microsoft.com/) is a destination for business users toodiscover, try, and manage line-of-business SaaS applications (standalone SaaS and add-on tooexisting Microsoft SaaS products).</span></span>

<span data-ttu-id="4d11e-105">toolist 獨立 AppSource 的 SaaS 應用程式，您的應用程式必須接受單一登入來自任何的公司或組織有 Azure Active Directory 的工作帳戶。</span><span class="sxs-lookup"><span data-stu-id="4d11e-105">toolist a standalone SaaS application on AppSource, your application must accept single sign-on from work accounts from any company or organization that has Azure Active Directory.</span></span> <span data-ttu-id="4d11e-106">hello 登入程序必須使用 hello [OpenID Connect](./active-directory-protocols-openid-connect-code.md)或[OAuth 2.0](./active-directory-protocols-oauth-code.md)通訊協定。</span><span class="sxs-lookup"><span data-stu-id="4d11e-106">hello sign-in process must use hello [OpenID Connect](./active-directory-protocols-openid-connect-code.md) or [OAuth 2.0](./active-directory-protocols-oauth-code.md) protocols.</span></span> <span data-ttu-id="4d11e-107">AppSource 認證不接受 SAML 整合。</span><span class="sxs-lookup"><span data-stu-id="4d11e-107">SAML integration is not accepted for AppSource certification.</span></span>

## <a name="guides-and-code-samples"></a><span data-ttu-id="4d11e-108">指南與程式碼範例</span><span class="sxs-lookup"><span data-stu-id="4d11e-108">Guides and code samples</span></span>
<span data-ttu-id="4d11e-109">如果您想 toolearn 關於如何 toointegrate 使用 Open ID 的 Azure Active Directory 的應用程式連接時，依照我們的指南和程式碼範例在 hello [Azure Active Directory 開發人員手冊 》](./active-directory-developers-guide.md#get-started "快速入門適用於開發人員的 azure AD")。</span><span class="sxs-lookup"><span data-stu-id="4d11e-109">If you want toolearn about how toointegrate your application with Azure Active Directory using Open ID connect, follow our guides and code samples in hello [Azure Active Directory developer's guide](./active-directory-developers-guide.md#get-started "Get Started with Azure AD for developers").</span></span>

## <a name="multi-tenant-applications"></a><span data-ttu-id="4d11e-110">多租用戶應用程式</span><span class="sxs-lookup"><span data-stu-id="4d11e-110">Multi-tenant applications</span></span>

<span data-ttu-id="4d11e-111">此應用程式接受來自具備 Azure Active Directory 之公司或組織的使用者的單一登入，不需要稱為*多租用戶應用程式*的個別執行個體、設定或部署。</span><span class="sxs-lookup"><span data-stu-id="4d11e-111">An application that accepts sign-ins from users from any company or organization that have Azure Active Directory without requiring a separate instance, configuration, or deployment is known as a *multi-tenant application*.</span></span> <span data-ttu-id="4d11e-112">AppSource 建議應用程式中實作多租用戶 tooenable hello*單鍵*免費的試用經驗。</span><span class="sxs-lookup"><span data-stu-id="4d11e-112">AppSource recommends that applications implement multi-tenancy tooenable hello *single-click* free trial experience.</span></span>

<span data-ttu-id="4d11e-113">在訂單 tooenable 多租用戶應用程式：</span><span class="sxs-lookup"><span data-stu-id="4d11e-113">In order tooenable multi-tenancy on your application:</span></span>
- <span data-ttu-id="4d11e-114">設定`Multi-Tenanted`屬性太`Yes`上您的應用程式登錄資訊中 hello [Azure 入口網站](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps)(根據預設，在 hello Azure 入口網站中建立的應用程式設定為*單一租用戶*)</span><span class="sxs-lookup"><span data-stu-id="4d11e-114">Set `Multi-Tenanted` property too`Yes` on your application registration's information in hello [Azure Portal](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps) (by default, applications created in hello Azure Portal are configured as *single-tenant*)</span></span>
- <span data-ttu-id="4d11e-115">更新您的程式碼 toosend 要求 toohello '`common`' 端點 (更新 hello 端點從*https://login.microsoftonline.com/ {yourtenant}*太*https://login.microsoftonline.com/common*)</span><span class="sxs-lookup"><span data-stu-id="4d11e-115">Update your code toosend requests toohello '`common`' endpoint (update hello endpoint from *https://login.microsoftonline.com/{yourtenant}* too*https://login.microsoftonline.com/common*)</span></span>
- <span data-ttu-id="4d11e-116">對於某些平台，像 ASP.NET，您也需要 tooupdate 程式碼 tooaccept 多個簽發者</span><span class="sxs-lookup"><span data-stu-id="4d11e-116">For some platforms, like ASP.NET, you need also tooupdate your code tooaccept multiple issuers</span></span>

<span data-ttu-id="4d11e-117">如需多租用戶的詳細資訊，請參閱：[如何在任何 Azure Active Directory (AD) 使用者使用 toosign hello 多租用戶應用程式模式](./active-directory-devhowto-multi-tenant-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="4d11e-117">For more information about multi-tenancy, see: [How toosign in any Azure Active Directory (AD) user using hello multi-tenant application pattern](./active-directory-devhowto-multi-tenant-overview.md).</span></span>

### <a name="single-tenant-applications"></a><span data-ttu-id="4d11e-118">單一租用戶應用程式</span><span class="sxs-lookup"><span data-stu-id="4d11e-118">Single-tenant applications</span></span>
<span data-ttu-id="4d11e-119">此應用程式僅接受來自定義之 Azure Active Directory 執行個體 (稱為*單一租用戶應用程式*) 的使用者登入。</span><span class="sxs-lookup"><span data-stu-id="4d11e-119">Applications that only accept sign-ins from users of a defined Azure Active Directory instance are known as *single-tenant application*.</span></span> <span data-ttu-id="4d11e-120">外部使用者 （包括來自其他組織中，工作或學校帳戶或個人帳戶） 登入 tooa 單一租用戶應用程式之後，加入每個使用者為*guest 帳戶*toohello Azure Active Directory 執行個體hello 應用程式註冊。</span><span class="sxs-lookup"><span data-stu-id="4d11e-120">External users (including Work or School accounts from other organizations, or personal account) can sign in tooa single-tenant application after adding each user as *guest account* toohello Azure Active Directory instance that hello application is registered.</span></span> <span data-ttu-id="4d11e-121">您可以將使用者新增為來賓帳戶 tooan Azure Active Directory 透過 hello [ *Azure AD B2B 共同作業*](../active-directory-b2b-what-is-azure-ad-b2b.md)位，且可完成[以程式設計方式控制程式](../active-directory-b2b-code-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="4d11e-121">You can add users as guest accounts tooan Azure Active Directory via hello [*Azure AD B2B collaboration*](../active-directory-b2b-what-is-azure-ad-b2b.md) - and it can be done [programatically](../active-directory-b2b-code-samples.md).</span></span> <span data-ttu-id="4d11e-122">當您將使用者新增為來賓帳戶 tooan Azure Active Directory 時，邀請電子郵件傳送 toohello，具有使用者 tooaccept hello 邀請 hello 邀請電子郵件中的 hello 連結上按一下。</span><span class="sxs-lookup"><span data-stu-id="4d11e-122">When you add a user as guest account tooan Azure Active Directory, an invitation email is sent toohello user, who has tooaccept hello invitation by clicking on hello link in hello invitation email.</span></span> <span data-ttu-id="4d11e-123">邀請傳送 tooan 額外的使用者，同時也是 hello 夥伴組織的成員邀請組織中是不必要的 tooaccept 中的邀請 toosign。</span><span class="sxs-lookup"><span data-stu-id="4d11e-123">Invitations that are sent tooan additional user in an inviting organization that is also a member of hello partner organization are not required tooaccept an invitation toosign in.</span></span>

<span data-ttu-id="4d11e-124">單一租用戶應用程式可以啟用 hello*與我連絡*體驗，但如果您想 tooenable hello 單鍵 / 免費的試用經驗 AppSource 建議時，啟用您的應用程式上的多租用戶改為。</span><span class="sxs-lookup"><span data-stu-id="4d11e-124">Single-tenant applications can enable hello *Contact Me* experience, but if you want tooenable hello single-click/ free trial experience that AppSource recommends, enable multi-tenancy on your application instead.</span></span>


## <a name="appsource-trial-experiences"></a><span data-ttu-id="4d11e-125">AppSource 試用體驗</span><span class="sxs-lookup"><span data-stu-id="4d11e-125">AppSource trial experiences</span></span>

### <a name="free-trial-customer-led-trial-experience"></a><span data-ttu-id="4d11e-126">免費試用 (以客戶為導向的試用體驗)</span><span class="sxs-lookup"><span data-stu-id="4d11e-126">Free Trial (Customer-led trial experience)</span></span> 
<span data-ttu-id="4d11e-127">hello*客戶導致試用*AppSource 建議，因為提供的單鍵存取 tooyour 應用程式的 hello 體驗。</span><span class="sxs-lookup"><span data-stu-id="4d11e-127">hello *customer-led trial* is hello experience that AppSource recommends as it offers a single-click access tooyour application.</span></span> <span data-ttu-id="4d11e-128">這項體驗看起來如下圖：</span><span class="sxs-lookup"><span data-stu-id="4d11e-128">Below an illustration of how this experience looks like:</span></span><br/><br/>

<table >
<tr>
    <td valign="top" width="33%">1.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step1.png" width="85%"/><ul><li><span data-ttu-id="4d11e-129">使用者會在 AppSource 網站中尋找您的應用程式</span><span class="sxs-lookup"><span data-stu-id="4d11e-129">User finds your application in AppSource Web Site</span></span></li><li><span data-ttu-id="4d11e-130">選取 [免費試用] 選項</span><span class="sxs-lookup"><span data-stu-id="4d11e-130">Selects ‘Free trial’ option</span></span></li></ul></td>
    <td valign="top" width="33%">2.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step2.png" width="85%" /><ul><li><span data-ttu-id="4d11e-131">AppSource 重新導向使用者 tooa URL 在您的網站</span><span class="sxs-lookup"><span data-stu-id="4d11e-131">AppSource redirects user tooa URL in your web site</span></span></li><li><span data-ttu-id="4d11e-132">您的網站啟動 hello<i>單一登入</i>自動 （在頁面載入） 處理序</span><span class="sxs-lookup"><span data-stu-id="4d11e-132">Your web site starts hello <i>single-sign-on</i> process automatically (on page load)</span></span></li></ul></td>
    <td valign="top" width="33%">3.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step3.png" width="85%"/><ul><li><span data-ttu-id="4d11e-133">使用者已重新導向的 tooMicrosoft 登入頁面</span><span class="sxs-lookup"><span data-stu-id="4d11e-133">User is redirected tooMicrosoft Sign-in page</span></span></li><li><span data-ttu-id="4d11e-134">使用者提供認證 toosign 中</span><span class="sxs-lookup"><span data-stu-id="4d11e-134">User provides credentials toosign in</span></span></li></ul></td>
</tr>
<tr>
    <td valign="top" width="33%">4.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step4.png" width="85%"/><ul><li><span data-ttu-id="4d11e-135">使用者同意您的應用程式</span><span class="sxs-lookup"><span data-stu-id="4d11e-135">User gives consent for your application</span></span></li></ul></td>
    <td valign="top" width="33%">5.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step5.png" width="85%"/><ul><li><span data-ttu-id="4d11e-136">登入完成，而且使用者為重新導向後 tooyour 網站</span><span class="sxs-lookup"><span data-stu-id="4d11e-136">Sign-in completes and user is redirected back tooyour web site</span></span></li><li><span data-ttu-id="4d11e-137">使用者啟動 hello 免費試用版</span><span class="sxs-lookup"><span data-stu-id="4d11e-137">User starts hello free trial</span></span></li></ul></td>
    <td></td>
</tr>
</table>

### <a name="contact-me-partner-led-trial-experience"></a><span data-ttu-id="4d11e-138">與我連絡 (以合作夥伴為導向的試用體驗)</span><span class="sxs-lookup"><span data-stu-id="4d11e-138">Contact Me (Partner-led trial experience)</span></span>
<span data-ttu-id="4d11e-139">hello*夥伴的試用經驗*可用時手動 」 或 「 長期作業需要 toohappen tooprovision hello 使用者 / 公司： 例如，您的應用程式需要 tooprovision 虛擬機器資料庫執行個體，或花太多時間 toocomplete 的作業。</span><span class="sxs-lookup"><span data-stu-id="4d11e-139">hello *partner trial experience* can be used when a manual or a long-term operation needs toohappen tooprovision hello user/ company: for example, your application needs tooprovision virtual machines, database instances, or operations that take much time toocomplete.</span></span> <span data-ttu-id="4d11e-140">在此情況下之後使用者選取 hello,*要求試用*按鈕，然後填寫表單，AppSource 傳送 hello 使用者的連絡資訊。</span><span class="sxs-lookup"><span data-stu-id="4d11e-140">In this case, after user selects hello *'Request Trial'* button and fills out a form, AppSource sends you hello user's contact information.</span></span> <span data-ttu-id="4d11e-141">在收到這項資訊，然後佈建 hello 環境並傳送 hello 指示 toohello 使用者如何 tooaccess hello 的試用經驗：</span><span class="sxs-lookup"><span data-stu-id="4d11e-141">Upon receiving this information, you then provision hello environment and send hello instructions toohello user on how tooaccess hello trial experience:</span></span><br/><br/>

<table valign="top">
<tr>
    <td valign="top" width="33%">1.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step1.png" width="85%"/><ul><li><span data-ttu-id="4d11e-142">使用者會在 AppSource 網站中尋找您的應用程式</span><span class="sxs-lookup"><span data-stu-id="4d11e-142">User finds your application in AppSource web site</span></span></li><li><span data-ttu-id="4d11e-143">選取 [與我連絡] 選項</span><span class="sxs-lookup"><span data-stu-id="4d11e-143">Selects ‘Contact Me’ option</span></span></li></ul></td>
    <td valign="top" width="33%">2.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step2.png" width="85%"/><ul><li><span data-ttu-id="4d11e-144">將連絡人資訊填入表單</span><span class="sxs-lookup"><span data-stu-id="4d11e-144">Fills out a form with contact information</span></span></li></ul></td>
     <td valign="top" width="33%">3.<br/><br/>
        <table bgcolor="#f7f7f7">
        <tr>
            <td><img src="media/active-directory-devhowto-appsource-certified/UserContact.png" width="55%"/></td>
            <td><span data-ttu-id="4d11e-145">您會收到使用者資訊</span><span class="sxs-lookup"><span data-stu-id="4d11e-145">You receive user information</span></span></td>
        </tr>
        <tr>
            <td><img src="media/active-directory-devhowto-appsource-certified/SetupEnv.png" width="55%"/></td>
            <td><span data-ttu-id="4d11e-146">設定環境</span><span class="sxs-lookup"><span data-stu-id="4d11e-146">Setup environment</span></span></td>
        </tr>
        <tr>
            <td><img src="media/active-directory-devhowto-appsource-certified/ContactCustomer.png" width="55%"/></td>
            <td><span data-ttu-id="4d11e-147">連絡使用者試用資訊</span><span class="sxs-lookup"><span data-stu-id="4d11e-147">Contact user with trial info</span></span></td>
        </tr>
        </table><br/><br/>
        <ul><li><span data-ttu-id="4d11e-148">您收到使用者資訊並設定試用執行個體</span><span class="sxs-lookup"><span data-stu-id="4d11e-148">You receive user's information and setup trial instance</span></span></li><li><span data-ttu-id="4d11e-149">您傳送嗨超連結 tooaccess toohello 應用程式的使用者</span><span class="sxs-lookup"><span data-stu-id="4d11e-149">You send hello hyperlink tooaccess your application toohello user</span></span></li></ul>
    </td>
</tr>
<tr>
    <td valign="top" width="33%">4.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step3.png" width="85%"/><ul><li><span data-ttu-id="4d11e-150">使用者存取您的應用程式和單一登入程序完成 hello</span><span class="sxs-lookup"><span data-stu-id="4d11e-150">User accesses your application and complete hello single-sign-on process</span></span></li></ul></td>
    <td valign="top" width="33%">5.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step4.png" width="85%"/><ul><li><span data-ttu-id="4d11e-151">使用者同意您的應用程式</span><span class="sxs-lookup"><span data-stu-id="4d11e-151">User gives consent for your application</span></span></li></ul></td>
    <td valign="top" width="33%">6.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step5.png" width="85%"/><ul><li><span data-ttu-id="4d11e-152">登入完成，而且使用者為重新導向後 tooyour 網站</span><span class="sxs-lookup"><span data-stu-id="4d11e-152">Sign-in completes and user is redirected back tooyour web site</span></span></li><li><span data-ttu-id="4d11e-153">使用者啟動 hello 免費試用版</span><span class="sxs-lookup"><span data-stu-id="4d11e-153">User starts hello free trial</span></span></li></ul></td>
   
</tr>
</table>

### <a name="more-information"></a><span data-ttu-id="4d11e-154">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="4d11e-154">More information</span></span>
<span data-ttu-id="4d11e-155">如需 hello AppSource 試用體驗的詳細資訊，請參閱[這段影片](https://aka.ms/trialexperienceforwebapps)。</span><span class="sxs-lookup"><span data-stu-id="4d11e-155">For more information about hello AppSource trial experience, see [this video](https://aka.ms/trialexperienceforwebapps).</span></span> 
 
## <a name="next-steps"></a><span data-ttu-id="4d11e-156">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4d11e-156">Next Steps</span></span>

- <span data-ttu-id="4d11e-157">如需建立支援 Azure Active Directory 登入之應用程式的詳細資訊，請參閱 [Azure AD 的驗證案例](https://docs.microsoft.com/azure/active-directory/develop/active-directory-authentication-scenarios)</span><span class="sxs-lookup"><span data-stu-id="4d11e-157">For more information on building applications that support Azure Active Directory sign-ins, see [Authentication Scenarios for Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-authentication-scenarios)</span></span> 

- <span data-ttu-id="4d11e-158">如需有關如何 toolist SaaS 應用程式中 AppSource，請查看詳細[AppSource 合作夥伴資訊](https://appsource.microsoft.com/partners)</span><span class="sxs-lookup"><span data-stu-id="4d11e-158">For information on how toolist your SaaS application in AppSource, go see [AppSource Partner Information](https://appsource.microsoft.com/partners)</span></span>


## <a name="get-support"></a><span data-ttu-id="4d11e-159">取得支援</span><span class="sxs-lookup"><span data-stu-id="4d11e-159">Get Support</span></span>
<span data-ttu-id="4d11e-160">Azure Active Directory 整合，我們使用[堆疊溢位](http://stackoverflow.com/questions/tagged/azure-active-directory)與 hello 社群 tooprovide 支援。</span><span class="sxs-lookup"><span data-stu-id="4d11e-160">For Azure Active Directory integration, we use [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-active-directory) with hello community tooprovide support.</span></span> 

<span data-ttu-id="4d11e-161">我們強烈建議您先詢問您的問題的堆疊溢位，並瀏覽現有問題 toosee，如果其他人已提出您的問題之前。</span><span class="sxs-lookup"><span data-stu-id="4d11e-161">We highly recommend you ask your questions on Stack Overflow first and browse existing issues toosee if someone has asked your question before.</span></span> <span data-ttu-id="4d11e-162">請確定您的問題或意見已標記為 `[azure-active-directory]`。</span><span class="sxs-lookup"><span data-stu-id="4d11e-162">Make sure that your questions or comments are tagged with `[azure-active-directory]`.</span></span>

<span data-ttu-id="4d11e-163">使用下列註解區段 tooprovide 意見反應的 hello，並協助我們改善並圖形內容。</span><span class="sxs-lookup"><span data-stu-id="4d11e-163">Use hello following comments section tooprovide feedback and help us refine and shape our content.</span></span>

<!--Reference style links -->
[AAD-Auth-Scenarios]: ./active-directory-authentication-scenarios.md
[AAD-Auth-Scenarios-Browser-To-WebApp]: ./active-directory-authentication-scenarios.md#web-browser-to-web-application
[AAD-Dev-Guide]: ./active-directory-developers-guide.md
[AAD-Howto-Multitenant-Overview]: ./active-directory-devhowto-multi-tenant-overview.md
[AAD-QuickStart-Web-Apps]: ./active-directory-developers-guide.md#get-started


<!--Image references-->