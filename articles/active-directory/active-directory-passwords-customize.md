---
title: "自訂︰Azure AD SSPR | Microsoft Docs"
description: "Azure AD 自助式密碼重設的自訂選項"
services: active-directory
keywords: 
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: 4762fffef040f9b409355f9ee0e8cc593e3eea0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="customize-azure-ad-functionality-for-self-service-password-reset"></a><span data-ttu-id="253b1-103">自訂 Azure AD 的自助式密碼重設功能</span><span class="sxs-lookup"><span data-stu-id="253b1-103">Customize Azure AD functionality for Self-Service Password Reset</span></span>

<span data-ttu-id="253b1-104">IT 專業人員尋找 toodeploy 自助式密碼重設可以自訂 hello 經驗 toomatch 他們的使用者。</span><span class="sxs-lookup"><span data-stu-id="253b1-104">IT Professionals looking toodeploy self-service password reset can customize hello experience toomatch their users.</span></span>

## <a name="customize-hello-contact-your-administrator-link"></a><span data-ttu-id="253b1-105">自訂 hello，請連絡您的系統管理員連結</span><span class="sxs-lookup"><span data-stu-id="253b1-105">Customize hello contact your administrator link</span></span>

<span data-ttu-id="253b1-106">即使 SSPR 不是啟用的使用者仍 「 連絡您的系統管理員 」 連結 hello 密碼重設入口網站。</span><span class="sxs-lookup"><span data-stu-id="253b1-106">Even if SSPR is not enabled users still a "contact your administrator" link on hello password reset portal.</span></span>  <span data-ttu-id="253b1-107">按一下此連結以電子郵件傳送您的系統管理員請求協助變更 hello 使用者的密碼。</span><span class="sxs-lookup"><span data-stu-id="253b1-107">Clicking this link emails your administrators asking for assistance in changing hello user's password.</span></span> <span data-ttu-id="253b1-108">這封電子郵件會傳送 toohello 遵循 hello 順序中的收件者：</span><span class="sxs-lookup"><span data-stu-id="253b1-108">This email is sent toohello following recipients in hello following order:</span></span>

1. <span data-ttu-id="253b1-109">如果 hello**密碼管理員**角色指派，請與此角色的系統管理員通知</span><span class="sxs-lookup"><span data-stu-id="253b1-109">If hello **Password administrator** role is assigned, administrators with this role are notified</span></span>
2. <span data-ttu-id="253b1-110">如果沒有密碼管理員指派，然後系統管理員以 hello**使用者系統管理員**角色會收到通知</span><span class="sxs-lookup"><span data-stu-id="253b1-110">If no Password administrators are assigned, then administrators with hello **User administrator** role are notified</span></span>
3. <span data-ttu-id="253b1-111">如果任一 hello 先前兩個角色指派，然後**全域管理員**會收到通知</span><span class="sxs-lookup"><span data-stu-id="253b1-111">If neither of hello previous roles were assigned, then **Global administrators** are notified</span></span>

<span data-ttu-id="253b1-112">在所有情況下，最多 100 位收件者會收到通知。</span><span class="sxs-lookup"><span data-stu-id="253b1-112">In all cases, a maximum of 100 recipients are notified.</span></span>

<span data-ttu-id="253b1-113">深入了解 hello 不同的系統管理員角色，以及如何加以查看的 tooassign hello 文件 toofind[指派 Azure Active Directory 中的系統管理員角色](active-directory-assign-admin-roles.md)</span><span class="sxs-lookup"><span data-stu-id="253b1-113">toofind out more about hello different administrator roles and how tooassign them see hello document [Assigning administrator roles in Azure Active Directory](active-directory-assign-admin-roles.md)</span></span>

### <a name="disable-contact-your-administrator-emails"></a><span data-ttu-id="253b1-114">停用「連絡您的系統管理員」電子郵件</span><span class="sxs-lookup"><span data-stu-id="253b1-114">Disable contact your administrator emails</span></span>

<span data-ttu-id="253b1-115">如果您的組織不想收到有關密碼的通知的系統管理員重設要求，hello 下列組態可啟用</span><span class="sxs-lookup"><span data-stu-id="253b1-115">If your organization does not want administrators notified about password reset requests, hello following configuration can be enabled</span></span>

* <span data-ttu-id="253b1-116">對所有使用者啟用自助式密碼重設。</span><span class="sxs-lookup"><span data-stu-id="253b1-116">Enable self-service password reset for all end users.</span></span> <span data-ttu-id="253b1-117">此選項位於 [密碼重設] > [屬性] 下。</span><span class="sxs-lookup"><span data-stu-id="253b1-117">This option is under **Password Reset > Properties**.</span></span>
    * <span data-ttu-id="253b1-118">如果您不想使用者 tooreset 自己的密碼，您可以為範圍存取 tooan 空群組**我們不建議您使用這個選項**。</span><span class="sxs-lookup"><span data-stu-id="253b1-118">If you do not wish users tooreset their own passwords, you can scope access tooan empty group **we do not recommend this option**.</span></span>
* <span data-ttu-id="253b1-119">自訂 hello 服務台連結 tooprovide web URL 或 mailto： 使用者可以使用 tooget 協助的位址。</span><span class="sxs-lookup"><span data-stu-id="253b1-119">Customize hello helpdesk link tooprovide a web URL or mailto: address that users can use tooget assistance.</span></span> <span data-ttu-id="253b1-120">此選項位於 [密碼重設] > [自訂] > [自訂的技術服務人員電子郵件或 URL] 下。</span><span class="sxs-lookup"><span data-stu-id="253b1-120">This option is under **Password Reset > Customization > Custom helpdesk email or URL**.</span></span>

## <a name="customize-adfs-sign-in-page-for-sspr"></a><span data-ttu-id="253b1-121">為 SSPR 自訂 ADFS 登入頁面</span><span class="sxs-lookup"><span data-stu-id="253b1-121">Customize ADFS sign-in page for SSPR</span></span>

<span data-ttu-id="253b1-122">ADFS 系統管理員可以新增連結 tootheir 登入頁面在 hello 文章中找到的 hello 指引[新增登入頁面描述](https://docs.microsoft.com/windows-server/identity/ad-fs/operations/add-sign-in-page-description)。</span><span class="sxs-lookup"><span data-stu-id="253b1-122">ADFS Administrators can add a link tootheir sign-in page using hello guidance found in hello article [Add sign-in page description](https://docs.microsoft.com/windows-server/identity/ad-fs/operations/add-sign-in-page-description).</span></span>

<span data-ttu-id="253b1-123">使用接在 ADFS 伺服器的 hello 命令加上允許使用者 tooenter hello 自助式密碼重設工作流程的直接連結 toohello ADFS 登入頁面。</span><span class="sxs-lookup"><span data-stu-id="253b1-123">Using hello command that follows on your ADFS server adds a link toohello ADFS login page allowing users tooenter hello self-service password reset workflow directly.</span></span>

``` Set-ADFSGlobalWebContent -SigninPageDescriptionText "<p><A href=’https://passwordreset.microsoftonline.com’>Can’t access your account?</A></p>" ```

## <a name="customize-hello-sign-in-and-access-panel-look-and-feel"></a><span data-ttu-id="253b1-124">自訂 hello 登入及存取面板的外觀及操作</span><span class="sxs-lookup"><span data-stu-id="253b1-124">Customize hello sign-in and access panel look and feel</span></span>

<span data-ttu-id="253b1-125">當您的使用者存取 hello 登入頁面時，您可以自訂 hello 標誌出現 hello 登入頁面影像 toofit 以及公司商標。</span><span class="sxs-lookup"><span data-stu-id="253b1-125">When your users access hello login page, you can customize hello logo that appears along with hello sign-in page image toofit your company branding.</span></span>

<span data-ttu-id="253b1-126">這些圖形會顯示在下列情況下的 hello:</span><span class="sxs-lookup"><span data-stu-id="253b1-126">These graphics are shown in hello following circumstances:</span></span>

* <span data-ttu-id="253b1-127">使用者輸入其使用者名稱之後</span><span class="sxs-lookup"><span data-stu-id="253b1-127">After a user types their username</span></span>
* <span data-ttu-id="253b1-128">使用者存取自訂的 url</span><span class="sxs-lookup"><span data-stu-id="253b1-128">User accesses customized url</span></span>
    * <span data-ttu-id="253b1-129">由傳送嗨"whr"參數 toohello 密碼重設頁面上，像是 「 https://login.microsoftonline.com/?whr=contoso.com"</span><span class="sxs-lookup"><span data-stu-id="253b1-129">By passing hello "whr" parameter toohello password reset page, like "https://login.microsoftonline.com/?whr=contoso.com"</span></span>
    * <span data-ttu-id="253b1-130">由傳送嗨"username"參數 toohello 重設密碼] 頁面上，例如"https://login.microsoftonline.com/?username=admin@contoso.com"</span><span class="sxs-lookup"><span data-stu-id="253b1-130">By passing hello "username" parameter toohello password reset page, like "https://login.microsoftonline.com/?username=admin@contoso.com"</span></span>

### <a name="graphics-details"></a><span data-ttu-id="253b1-131">圖形的詳細資料</span><span class="sxs-lookup"><span data-stu-id="253b1-131">Graphics details</span></span>

<span data-ttu-id="253b1-132">hello 下列設定 toochange hello 視覺特性 hello 登入頁面可讓您和您可以找到**Azure Active Directory**，**公司商標**，**編輯公司商標**</span><span class="sxs-lookup"><span data-stu-id="253b1-132">hello following settings allow you toochange hello visual characteristics of hello sign-in page and can be found under **Azure Active Directory**, **Company branding**, **Edit company branding**</span></span>

* <span data-ttu-id="253b1-133">登入頁面影像應該是 PNG 或 JPG 檔案 1420x1200 像素，不能大於 500KB。</span><span class="sxs-lookup"><span data-stu-id="253b1-133">Sign-in page image should be a PNG or JPG file 1420x1200 pixels and no larger than 500KB.</span></span> <span data-ttu-id="253b1-134">我們建議 toobe 約 200 KB 為了獲得最佳結果。</span><span class="sxs-lookup"><span data-stu-id="253b1-134">We recommend it toobe around 200 KB for best results.</span></span>
* <span data-ttu-id="253b1-135">登入頁面背景色彩時高延遲的連接上使用，而且必須以 hello RGB 十六進位格式。</span><span class="sxs-lookup"><span data-stu-id="253b1-135">Sign-in page background color is used when on high-latency connections and must be in hello RGB hex format.</span></span>
* <span data-ttu-id="253b1-136">橫幅影像應該是 PNG 或 JPG 檔案 60x280 像素，不能大於 10 KB。</span><span class="sxs-lookup"><span data-stu-id="253b1-136">Banner image should be a PNG or JPG file 60x280 pixels and no larger than 10 KB.</span></span>
* <span data-ttu-id="253b1-137">正方形標誌 (一般和深色佈景主題) PNG 或 JPG 240x240 (可調整大小)，不能大於 10 KB。</span><span class="sxs-lookup"><span data-stu-id="253b1-137">Square logo (normal and dark theme) PNG or JPG 240x240 (resizable) no larger than 10 KB.</span></span>

### <a name="sign-in-text-options"></a><span data-ttu-id="253b1-138">登入文字選項</span><span class="sxs-lookup"><span data-stu-id="253b1-138">Sign-in text options</span></span>

<span data-ttu-id="253b1-139">hello 下列設定可讓您 tooadd 文字 toohello 登入頁面相關 tooyour 組織。</span><span class="sxs-lookup"><span data-stu-id="253b1-139">hello following settings allow you tooadd text toohello sign-in page relevant tooyour organization.</span></span> <span data-ttu-id="253b1-140">您可以在 [Azure Active Directory]、[公司商標]、[編輯公司商標] 下找到這些設定</span><span class="sxs-lookup"><span data-stu-id="253b1-140">These settings can be found under **Azure Active Directory**, **Company branding**, **Edit company branding**</span></span>

* <span data-ttu-id="253b1-141">**使用者名稱提示**取代 hello 範例文字someone@example.com一些較適合您的使用者，使用時，建議使用 toobe 左的預設支援的內部和外部使用者</span><span class="sxs-lookup"><span data-stu-id="253b1-141">**User name hint** replaces hello example text of someone@example.com with something more appropriate for your users, recommended toobe left default when supporting internal and external users</span></span>
* <span data-ttu-id="253b1-142">[登入頁面文字] 的長度最多 256 個字元。</span><span class="sxs-lookup"><span data-stu-id="253b1-142">**Sign-in page text** is a maximum of 256 characters in length.</span></span> <span data-ttu-id="253b1-143">任何位置，連線，且在 hello Windows 10 上體驗 Azure AD Join，此文字會出現您的使用者登入。</span><span class="sxs-lookup"><span data-stu-id="253b1-143">This text appears anywhere your users login online, and in hello Azure AD Join experience on Windows 10.</span></span> <span data-ttu-id="253b1-144">使用此文字作為給使用者的使用條款、指示和提示。</span><span class="sxs-lookup"><span data-stu-id="253b1-144">Use this text for terms of use, instructions, and tips for your users.</span></span> <span data-ttu-id="253b1-145">**任何人都可以看到您的登入頁面，請勿在此處提供任何機密資訊。**</span><span class="sxs-lookup"><span data-stu-id="253b1-145">**Anyone can see your sign-in page so do not provide any sensitive information here.**</span></span>

### <a name="keep-me-signed-in-disabled"></a><span data-ttu-id="253b1-146">已停用 [讓我保持登入]</span><span class="sxs-lookup"><span data-stu-id="253b1-146">Keep me signed in disabled</span></span>

<span data-ttu-id="253b1-147">hello 選項 「 讓我保持登入已停用 」 可讓使用者 tooremain 關閉並重新開啟其瀏覽器視窗時，登入。</span><span class="sxs-lookup"><span data-stu-id="253b1-147">hello option "Keep me signed in disabled" allows users tooremain signed in when they close and reopen their browser window.</span></span> <span data-ttu-id="253b1-148">這個選項不會影響工作階段存留期。</span><span class="sxs-lookup"><span data-stu-id="253b1-148">This option does not impact session lifetimes.</span></span> <span data-ttu-id="253b1-149">您可以在 [Azure Active Directory] > [公司商標] > [編輯公司商標] 下找到此設定。</span><span class="sxs-lookup"><span data-stu-id="253b1-149">This setting is found under **Azure Active Directory > Company branding > Edit company branding**.</span></span>

<span data-ttu-id="253b1-150">SharePoint Online 和 Office 2010 的某些功能會有相依性的使用者可以 toocheck 此方塊。</span><span class="sxs-lookup"><span data-stu-id="253b1-150">Some features of SharePoint Online and Office 2010 have a dependency on users being able toocheck this box.</span></span> <span data-ttu-id="253b1-151">如果您隱藏此選項時，使用者可能會收到其他非預期的登入提示。</span><span class="sxs-lookup"><span data-stu-id="253b1-151">If you hide this option, users may get additional and unexpected sign-in prompts.</span></span>

### <a name="directory-name"></a><span data-ttu-id="253b1-152">目錄名稱</span><span class="sxs-lookup"><span data-stu-id="253b1-152">Directory name</span></span>

<span data-ttu-id="253b1-153">您可以變更下的 hello name 屬性**Azure Active Directory > 屬性**tooshow 易記的組織名稱出現在 hello 入口網站，且自動化的通訊。</span><span class="sxs-lookup"><span data-stu-id="253b1-153">You can change hello name attribute under **Azure Active Directory > Properties** tooshow a friendly organization name seen in hello portal and automated communications.</span></span> <span data-ttu-id="253b1-154">這個選項是最明顯 hello hello 表單，請依照下列中的自動化電子郵件格式</span><span class="sxs-lookup"><span data-stu-id="253b1-154">This option is most visible in hello form of automated emails in hello forms that follow</span></span>

* <span data-ttu-id="253b1-155">「Microsoft 代表 CONTOSO 示範」電子郵件中的易記名稱</span><span class="sxs-lookup"><span data-stu-id="253b1-155">Friendly name in email “Microsoft on behalf of CONTOSO demo”</span></span>
* <span data-ttu-id="253b1-156">「CONTOSO 示範帳戶電子郵件驗證碼」電子郵件的主旨列</span><span class="sxs-lookup"><span data-stu-id="253b1-156">Subject line in email “CONTOSO demo account email verification code”</span></span>

## <a name="next-steps"></a><span data-ttu-id="253b1-157">後續步驟</span><span class="sxs-lookup"><span data-stu-id="253b1-157">Next steps</span></span>

<span data-ttu-id="253b1-158">hello 下列連結提供有關密碼重設使用 Azure AD 的其他資訊</span><span class="sxs-lookup"><span data-stu-id="253b1-158">hello following links provide additional information regarding password reset using Azure AD</span></span>

* <span data-ttu-id="253b1-159">[**快速入門**](active-directory-passwords-getting-started.md) - 開始執行 Azure AD 自助式密碼管理</span><span class="sxs-lookup"><span data-stu-id="253b1-159">[**Quick Start**](active-directory-passwords-getting-started.md) - Get up and running with Azure AD self service password management</span></span> 
* <span data-ttu-id="253b1-160">[**授權**](active-directory-passwords-licensing.md) - 設定 Azure AD 授權</span><span class="sxs-lookup"><span data-stu-id="253b1-160">[**Licensing**](active-directory-passwords-licensing.md) - Configure your Azure AD Licensing</span></span>
* <span data-ttu-id="253b1-161">[**資料**](active-directory-passwords-data.md) -了解所需的 hello 資料及如何使用密碼管理</span><span class="sxs-lookup"><span data-stu-id="253b1-161">[**Data**](active-directory-passwords-data.md) - Understand hello data that is required and how it is used for password management</span></span>
* <span data-ttu-id="253b1-162">[**首度發行**](active-directory-passwords-best-practices.md) -計劃和部署 SSPR tooyour 使用者 hello 指引，請參閱</span><span class="sxs-lookup"><span data-stu-id="253b1-162">[**Rollout**](active-directory-passwords-best-practices.md) - Plan and deploy SSPR tooyour users using hello guidance found here</span></span>
* <span data-ttu-id="253b1-163">[**原則**](active-directory-passwords-policy.md) - 了解並設定 Azure AD 密碼原則</span><span class="sxs-lookup"><span data-stu-id="253b1-163">[**Policy**](active-directory-passwords-policy.md) - Understand and set Azure AD password policies</span></span>
* <span data-ttu-id="253b1-164">[**密碼回寫**](active-directory-passwords-writeback.md) - 密碼回寫如何使用您的內部部署目錄</span><span class="sxs-lookup"><span data-stu-id="253b1-164">[**Password Writeback**](active-directory-passwords-writeback.md) - How does password writeback work with your on-premises directory</span></span>
* <span data-ttu-id="253b1-165">[**報告**](active-directory-passwords-reporting.md) - 探索您的使用者是否、何時、何地存取 SSPR 功能</span><span class="sxs-lookup"><span data-stu-id="253b1-165">[**Reporting**](active-directory-passwords-reporting.md) - Discover if, when, and where your users are accessing SSPR functionality</span></span>
* <span data-ttu-id="253b1-166">[**技術的深入探討**](active-directory-passwords-how-it-works.md) -hello 帘 toounderstand 後方移它的運作方式</span><span class="sxs-lookup"><span data-stu-id="253b1-166">[**Technical Deep Dive**](active-directory-passwords-how-it-works.md) - Go behind hello curtain toounderstand how it works</span></span>
* <span data-ttu-id="253b1-167">[**常見問題集**](active-directory-passwords-faq.md) - 如何？</span><span class="sxs-lookup"><span data-stu-id="253b1-167">[**Frequently Asked Questions**](active-directory-passwords-faq.md) - How?</span></span> <span data-ttu-id="253b1-168">原因為何？</span><span class="sxs-lookup"><span data-stu-id="253b1-168">Why?</span></span> <span data-ttu-id="253b1-169">何事？</span><span class="sxs-lookup"><span data-stu-id="253b1-169">What?</span></span> <span data-ttu-id="253b1-170">何地？</span><span class="sxs-lookup"><span data-stu-id="253b1-170">Where?</span></span> <span data-ttu-id="253b1-171">何人？</span><span class="sxs-lookup"><span data-stu-id="253b1-171">Who?</span></span> <span data-ttu-id="253b1-172">何時？</span><span class="sxs-lookup"><span data-stu-id="253b1-172">When?</span></span> <span data-ttu-id="253b1-173">-回答您總是想 tooask tooquestions</span><span class="sxs-lookup"><span data-stu-id="253b1-173">- Answers tooquestions you always wanted tooask</span></span>
* <span data-ttu-id="253b1-174">[**疑難排解**](active-directory-passwords-troubleshoot.md) -了解如何 tooresolve 常見問題，我們會看到與 SSPR</span><span class="sxs-lookup"><span data-stu-id="253b1-174">[**Troubleshoot**](active-directory-passwords-troubleshoot.md) - Learn how tooresolve common issues that we see with SSPR</span></span>

