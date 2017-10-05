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
ms.openlocfilehash: 8b9c120815473b25140b8717f8fdd539c97ebb04
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="customize-azure-ad-functionality-for-self-service-password-reset"></a><span data-ttu-id="5d5b7-103">自訂 Azure AD 的自助式密碼重設功能</span><span class="sxs-lookup"><span data-stu-id="5d5b7-103">Customize Azure AD functionality for Self-Service Password Reset</span></span>

<span data-ttu-id="5d5b7-104">IT 專業人員期待部署自助式密碼重設可以自訂體驗以符合他們的使用者需求。</span><span class="sxs-lookup"><span data-stu-id="5d5b7-104">IT Professionals looking to deploy self-service password reset can customize the experience to match their users.</span></span>

## <a name="customize-the-contact-your-administrator-link"></a><span data-ttu-id="5d5b7-105">自訂「連絡您的系統管理員」連結</span><span class="sxs-lookup"><span data-stu-id="5d5b7-105">Customize the contact your administrator link</span></span>

<span data-ttu-id="5d5b7-106">即使未啟用 SSPR，使用者在密碼重設入口網站上仍會看到「連絡您的系統管理員」連結。</span><span class="sxs-lookup"><span data-stu-id="5d5b7-106">Even if SSPR is not enabled users still a "contact your administrator" link on the password reset portal.</span></span>  <span data-ttu-id="5d5b7-107">按一下此連結會寄電子郵件給系統管理員，請他協助關變更使用者的密碼。</span><span class="sxs-lookup"><span data-stu-id="5d5b7-107">Clicking this link emails your administrators asking for assistance in changing the user's password.</span></span> <span data-ttu-id="5d5b7-108">這封電子郵件會依下列順序傳送給下列收件者︰</span><span class="sxs-lookup"><span data-stu-id="5d5b7-108">This email is sent to the following recipients in the following order:</span></span>

1. <span data-ttu-id="5d5b7-109">如果已指派**密碼系統管理員**角色，具有此角色的系統管理員會收到通知</span><span class="sxs-lookup"><span data-stu-id="5d5b7-109">If the **Password administrator** role is assigned, administrators with this role are notified</span></span>
2. <span data-ttu-id="5d5b7-110">如果未指派密碼系統管理員，則具有**使用者系統管理員**角色的系統管理員會收到通知</span><span class="sxs-lookup"><span data-stu-id="5d5b7-110">If no Password administrators are assigned, then administrators with the **User administrator** role are notified</span></span>
3. <span data-ttu-id="5d5b7-111">如果上述角色都未指派，則**全域管理員**會收到通知</span><span class="sxs-lookup"><span data-stu-id="5d5b7-111">If neither of the previous roles were assigned, then **Global administrators** are notified</span></span>

<span data-ttu-id="5d5b7-112">在所有情況下，最多 100 位收件者會收到通知。</span><span class="sxs-lookup"><span data-stu-id="5d5b7-112">In all cases, a maximum of 100 recipients are notified.</span></span>

<span data-ttu-id="5d5b7-113">若要進一步了解不同的系統管理員角色，以及如何指派他們，請參閱文件[在 Azure Active Directory 中指派系統管理員角色](active-directory-assign-admin-roles.md)</span><span class="sxs-lookup"><span data-stu-id="5d5b7-113">To find out more about the different administrator roles and how to assign them see the document [Assigning administrator roles in Azure Active Directory](active-directory-assign-admin-roles.md)</span></span>

### <a name="disable-contact-your-administrator-emails"></a><span data-ttu-id="5d5b7-114">停用「連絡您的系統管理員」電子郵件</span><span class="sxs-lookup"><span data-stu-id="5d5b7-114">Disable contact your administrator emails</span></span>

<span data-ttu-id="5d5b7-115">如果您的組織不想讓系統管理員收到有關密碼重設要求的通知，則可以啟用下列設定</span><span class="sxs-lookup"><span data-stu-id="5d5b7-115">If your organization does not want administrators notified about password reset requests, the following configuration can be enabled</span></span>

* <span data-ttu-id="5d5b7-116">對所有使用者啟用自助式密碼重設。</span><span class="sxs-lookup"><span data-stu-id="5d5b7-116">Enable self-service password reset for all end users.</span></span> <span data-ttu-id="5d5b7-117">此選項位於 [密碼重設] > [屬性] 下。</span><span class="sxs-lookup"><span data-stu-id="5d5b7-117">This option is under **Password Reset > Properties**.</span></span>
    * <span data-ttu-id="5d5b7-118">如果您不想讓使用者重設其自己的密碼，您可以將存取範圍設為空的群組，**但我們不建議使用此選項**。</span><span class="sxs-lookup"><span data-stu-id="5d5b7-118">If you do not wish users to reset their own passwords, you can scope access to an empty group **we do not recommend this option**.</span></span>
* <span data-ttu-id="5d5b7-119">自訂技術服務人員連結，以提供可讓使用者取得協助的 Web URL 或 mailto︰位址。</span><span class="sxs-lookup"><span data-stu-id="5d5b7-119">Customize the helpdesk link to provide a web URL or mailto: address that users can use to get assistance.</span></span> <span data-ttu-id="5d5b7-120">此選項位於 [密碼重設] > [自訂] > [自訂的技術服務人員電子郵件或 URL] 下。</span><span class="sxs-lookup"><span data-stu-id="5d5b7-120">This option is under **Password Reset > Customization > Custom helpdesk email or URL**.</span></span>

## <a name="customize-adfs-sign-in-page-for-sspr"></a><span data-ttu-id="5d5b7-121">為 SSPR 自訂 ADFS 登入頁面</span><span class="sxs-lookup"><span data-stu-id="5d5b7-121">Customize ADFS sign-in page for SSPR</span></span>

<span data-ttu-id="5d5b7-122">ADFS 系統管理員可以使用在[新增登入分頁描述](https://docs.microsoft.com/windows-server/identity/ad-fs/operations/add-sign-in-page-description)一文中找到的指引，將連結新增至他們的登入分頁。</span><span class="sxs-lookup"><span data-stu-id="5d5b7-122">ADFS Administrators can add a link to their sign-in page using the guidance found in the article [Add sign-in page description](https://docs.microsoft.com/windows-server/identity/ad-fs/operations/add-sign-in-page-description).</span></span>

<span data-ttu-id="5d5b7-123">使用 ADFS 伺服器上接續的命令，將連結新增至 ADFS，讓使用者直接輸入自助式密碼重設工作流程。</span><span class="sxs-lookup"><span data-stu-id="5d5b7-123">Using the command that follows on your ADFS server adds a link to the ADFS login page allowing users to enter the self-service password reset workflow directly.</span></span>

``` Set-ADFSGlobalWebContent -SigninPageDescriptionText "<p><A href=’https://passwordreset.microsoftonline.com’>Can’t access your account?</A></p>" ```

## <a name="customize-the-sign-in-and-access-panel-look-and-feel"></a><span data-ttu-id="5d5b7-124">自訂登入和存取面板的外觀與風格</span><span class="sxs-lookup"><span data-stu-id="5d5b7-124">Customize the sign-in and access panel look and feel</span></span>

<span data-ttu-id="5d5b7-125">當您的使用者存取登入頁面時，您可以自訂隨著登入頁面影像一起出現的標誌，以符合您的公司商標。</span><span class="sxs-lookup"><span data-stu-id="5d5b7-125">When your users access the login page, you can customize the logo that appears along with the sign-in page image to fit your company branding.</span></span>

<span data-ttu-id="5d5b7-126">下列情況會顯示這些圖形︰</span><span class="sxs-lookup"><span data-stu-id="5d5b7-126">These graphics are shown in the following circumstances:</span></span>

* <span data-ttu-id="5d5b7-127">使用者輸入其使用者名稱之後</span><span class="sxs-lookup"><span data-stu-id="5d5b7-127">After a user types their username</span></span>
* <span data-ttu-id="5d5b7-128">使用者存取自訂的 url</span><span class="sxs-lookup"><span data-stu-id="5d5b7-128">User accesses customized url</span></span>
    * <span data-ttu-id="5d5b7-129">將 "whr" 參數傳遞至密碼重設頁面，例如 "https://login.microsoftonline.com/?whr=contoso.com"</span><span class="sxs-lookup"><span data-stu-id="5d5b7-129">By passing the "whr" parameter to the password reset page, like "https://login.microsoftonline.com/?whr=contoso.com"</span></span>
    * <span data-ttu-id="5d5b7-130">將 "username" 參數傳遞至密碼重設頁面，例如 "https://login.microsoftonline.com/?username=admin@contoso.com"</span><span class="sxs-lookup"><span data-stu-id="5d5b7-130">By passing the "username" parameter to the password reset page, like "https://login.microsoftonline.com/?username=admin@contoso.com"</span></span>

### <a name="graphics-details"></a><span data-ttu-id="5d5b7-131">圖形的詳細資料</span><span class="sxs-lookup"><span data-stu-id="5d5b7-131">Graphics details</span></span>

<span data-ttu-id="5d5b7-132">下列設定可讓您變更登入頁面的視覺特性，您可以在 [Azure Active Directory]、[公司商標]、[編輯公司商標] 下找到這些設定</span><span class="sxs-lookup"><span data-stu-id="5d5b7-132">The following settings allow you to change the visual characteristics of the sign-in page and can be found under **Azure Active Directory**, **Company branding**, **Edit company branding**</span></span>

* <span data-ttu-id="5d5b7-133">登入頁面影像應該是 PNG 或 JPG 檔案 1420x1200 像素，不能大於 500KB。</span><span class="sxs-lookup"><span data-stu-id="5d5b7-133">Sign-in page image should be a PNG or JPG file 1420x1200 pixels and no larger than 500KB.</span></span> <span data-ttu-id="5d5b7-134">建議大約 200 KB 即可，效果最佳。</span><span class="sxs-lookup"><span data-stu-id="5d5b7-134">We recommend it to be around 200 KB for best results.</span></span>
* <span data-ttu-id="5d5b7-135">登入分頁背景色彩在高延遲連線時使用，必須是 RGB 十六進位格式。</span><span class="sxs-lookup"><span data-stu-id="5d5b7-135">Sign-in page background color is used when on high-latency connections and must be in the RGB hex format.</span></span>
* <span data-ttu-id="5d5b7-136">橫幅影像應該是 PNG 或 JPG 檔案 60x280 像素，不能大於 10 KB。</span><span class="sxs-lookup"><span data-stu-id="5d5b7-136">Banner image should be a PNG or JPG file 60x280 pixels and no larger than 10 KB.</span></span>
* <span data-ttu-id="5d5b7-137">正方形標誌 (一般和深色佈景主題) PNG 或 JPG 240x240 (可調整大小)，不能大於 10 KB。</span><span class="sxs-lookup"><span data-stu-id="5d5b7-137">Square logo (normal and dark theme) PNG or JPG 240x240 (resizable) no larger than 10 KB.</span></span>

### <a name="sign-in-text-options"></a><span data-ttu-id="5d5b7-138">登入文字選項</span><span class="sxs-lookup"><span data-stu-id="5d5b7-138">Sign-in text options</span></span>

<span data-ttu-id="5d5b7-139">下列設定可讓您將組織的相關文字新增至登入頁面。</span><span class="sxs-lookup"><span data-stu-id="5d5b7-139">The following settings allow you to add text to the sign-in page relevant to your organization.</span></span> <span data-ttu-id="5d5b7-140">您可以在 [Azure Active Directory]、[公司商標]、[編輯公司商標] 下找到這些設定</span><span class="sxs-lookup"><span data-stu-id="5d5b7-140">These settings can be found under **Azure Active Directory**, **Company branding**, **Edit company branding**</span></span>

* <span data-ttu-id="5d5b7-141">[使用者名稱提示] 會以更適合使用者的文字取代範例文字 someone@example.com，當支援內部和外部使用者時，建議保留預設值</span><span class="sxs-lookup"><span data-stu-id="5d5b7-141">**User name hint** replaces the example text of someone@example.com with something more appropriate for your users, recommended to be left default when supporting internal and external users</span></span>
* <span data-ttu-id="5d5b7-142">[登入頁面文字] 的長度最多 256 個字元。</span><span class="sxs-lookup"><span data-stu-id="5d5b7-142">**Sign-in page text** is a maximum of 256 characters in length.</span></span> <span data-ttu-id="5d5b7-143">此文字會出現在使用者登入線上的任何地方，也出現在 Windows 10 的 Azure AD Join 體驗中。</span><span class="sxs-lookup"><span data-stu-id="5d5b7-143">This text appears anywhere your users login online, and in the Azure AD Join experience on Windows 10.</span></span> <span data-ttu-id="5d5b7-144">使用此文字作為給使用者的使用條款、指示和提示。</span><span class="sxs-lookup"><span data-stu-id="5d5b7-144">Use this text for terms of use, instructions, and tips for your users.</span></span> <span data-ttu-id="5d5b7-145">**任何人都可以看到您的登入頁面，請勿在此處提供任何機密資訊。**</span><span class="sxs-lookup"><span data-stu-id="5d5b7-145">**Anyone can see your sign-in page so do not provide any sensitive information here.**</span></span>

### <a name="keep-me-signed-in-disabled"></a><span data-ttu-id="5d5b7-146">已停用 [讓我保持登入]</span><span class="sxs-lookup"><span data-stu-id="5d5b7-146">Keep me signed in disabled</span></span>

<span data-ttu-id="5d5b7-147">[已停用讓我保持登入] 選項可讓使用者在關閉又重新開啟瀏覽器視窗時，保持登入狀態。</span><span class="sxs-lookup"><span data-stu-id="5d5b7-147">The option "Keep me signed in disabled" allows users to remain signed in when they close and reopen their browser window.</span></span> <span data-ttu-id="5d5b7-148">這個選項不會影響工作階段存留期。</span><span class="sxs-lookup"><span data-stu-id="5d5b7-148">This option does not impact session lifetimes.</span></span> <span data-ttu-id="5d5b7-149">您可以在 [Azure Active Directory] > [公司商標] > [編輯公司商標] 下找到此設定。</span><span class="sxs-lookup"><span data-stu-id="5d5b7-149">This setting is found under **Azure Active Directory > Company branding > Edit company branding**.</span></span>

<span data-ttu-id="5d5b7-150">使用者必須能夠勾選此方塊，才能使用 SharePoint Online 和 Office 2010 的某些功能。</span><span class="sxs-lookup"><span data-stu-id="5d5b7-150">Some features of SharePoint Online and Office 2010 have a dependency on users being able to check this box.</span></span> <span data-ttu-id="5d5b7-151">如果您隱藏此選項時，使用者可能會收到其他非預期的登入提示。</span><span class="sxs-lookup"><span data-stu-id="5d5b7-151">If you hide this option, users may get additional and unexpected sign-in prompts.</span></span>

### <a name="directory-name"></a><span data-ttu-id="5d5b7-152">目錄名稱</span><span class="sxs-lookup"><span data-stu-id="5d5b7-152">Directory name</span></span>

<span data-ttu-id="5d5b7-153">您可以在 [Azure Active Directory] > [屬性] 下變更名稱屬性，讓入口網站和自動通訊中顯示好記的組織名稱。</span><span class="sxs-lookup"><span data-stu-id="5d5b7-153">You can change the name attribute under **Azure Active Directory > Properties** to show a friendly organization name seen in the portal and automated communications.</span></span> <span data-ttu-id="5d5b7-154">這個選項最常以如下的自動化電子郵件形式出現</span><span class="sxs-lookup"><span data-stu-id="5d5b7-154">This option is most visible in the form of automated emails in the forms that follow</span></span>

* <span data-ttu-id="5d5b7-155">「Microsoft 代表 CONTOSO 示範」電子郵件中的易記名稱</span><span class="sxs-lookup"><span data-stu-id="5d5b7-155">Friendly name in email “Microsoft on behalf of CONTOSO demo”</span></span>
* <span data-ttu-id="5d5b7-156">「CONTOSO 示範帳戶電子郵件驗證碼」電子郵件的主旨列</span><span class="sxs-lookup"><span data-stu-id="5d5b7-156">Subject line in email “CONTOSO demo account email verification code”</span></span>

## <a name="next-steps"></a><span data-ttu-id="5d5b7-157">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5d5b7-157">Next steps</span></span>

<span data-ttu-id="5d5b7-158">下列連結提供有關使用 Azure AD 重設密碼的其他資訊</span><span class="sxs-lookup"><span data-stu-id="5d5b7-158">The following links provide additional information regarding password reset using Azure AD</span></span>

* <span data-ttu-id="5d5b7-159">[**快速入門**](active-directory-passwords-getting-started.md) - 開始執行 Azure AD 自助式密碼管理</span><span class="sxs-lookup"><span data-stu-id="5d5b7-159">[**Quick Start**](active-directory-passwords-getting-started.md) - Get up and running with Azure AD self service password management</span></span> 
* <span data-ttu-id="5d5b7-160">[**授權**](active-directory-passwords-licensing.md) - 設定 Azure AD 授權</span><span class="sxs-lookup"><span data-stu-id="5d5b7-160">[**Licensing**](active-directory-passwords-licensing.md) - Configure your Azure AD Licensing</span></span>
* <span data-ttu-id="5d5b7-161">[**資料**](active-directory-passwords-data.md) -了解所需的資料以及如何將它使用於密碼管理</span><span class="sxs-lookup"><span data-stu-id="5d5b7-161">[**Data**](active-directory-passwords-data.md) - Understand the data that is required and how it is used for password management</span></span>
* <span data-ttu-id="5d5b7-162">[**推出**](active-directory-passwords-best-practices.md) - 使用此處提供的指引來規劃 SSPR 並部署給使用者</span><span class="sxs-lookup"><span data-stu-id="5d5b7-162">[**Rollout**](active-directory-passwords-best-practices.md) - Plan and deploy SSPR to your users using the guidance found here</span></span>
* <span data-ttu-id="5d5b7-163">[**原則**](active-directory-passwords-policy.md) - 了解並設定 Azure AD 密碼原則</span><span class="sxs-lookup"><span data-stu-id="5d5b7-163">[**Policy**](active-directory-passwords-policy.md) - Understand and set Azure AD password policies</span></span>
* <span data-ttu-id="5d5b7-164">[**密碼回寫**](active-directory-passwords-writeback.md) - 密碼回寫如何使用您的內部部署目錄</span><span class="sxs-lookup"><span data-stu-id="5d5b7-164">[**Password Writeback**](active-directory-passwords-writeback.md) - How does password writeback work with your on-premises directory</span></span>
* <span data-ttu-id="5d5b7-165">[**報告**](active-directory-passwords-reporting.md) - 探索您的使用者是否、何時、何地存取 SSPR 功能</span><span class="sxs-lookup"><span data-stu-id="5d5b7-165">[**Reporting**](active-directory-passwords-reporting.md) - Discover if, when, and where your users are accessing SSPR functionality</span></span>
* <span data-ttu-id="5d5b7-166">[**技術性深入探討**](active-directory-passwords-how-it-works.md) - 深入探索以了解其運作方式</span><span class="sxs-lookup"><span data-stu-id="5d5b7-166">[**Technical Deep Dive**](active-directory-passwords-how-it-works.md) - Go behind the curtain to understand how it works</span></span>
* <span data-ttu-id="5d5b7-167">[**常見問題集**](active-directory-passwords-faq.md) - 如何？</span><span class="sxs-lookup"><span data-stu-id="5d5b7-167">[**Frequently Asked Questions**](active-directory-passwords-faq.md) - How?</span></span> <span data-ttu-id="5d5b7-168">原因為何？</span><span class="sxs-lookup"><span data-stu-id="5d5b7-168">Why?</span></span> <span data-ttu-id="5d5b7-169">何事？</span><span class="sxs-lookup"><span data-stu-id="5d5b7-169">What?</span></span> <span data-ttu-id="5d5b7-170">何地？</span><span class="sxs-lookup"><span data-stu-id="5d5b7-170">Where?</span></span> <span data-ttu-id="5d5b7-171">何人？</span><span class="sxs-lookup"><span data-stu-id="5d5b7-171">Who?</span></span> <span data-ttu-id="5d5b7-172">何時？</span><span class="sxs-lookup"><span data-stu-id="5d5b7-172">When?</span></span> <span data-ttu-id="5d5b7-173">- -您一直想要詢問之問題的答案</span><span class="sxs-lookup"><span data-stu-id="5d5b7-173">- Answers to questions you always wanted to ask</span></span>
* <span data-ttu-id="5d5b7-174">[**疑難排解**](active-directory-passwords-troubleshoot.md) - 了解如何解決我們看到的 SSPR 常見問題</span><span class="sxs-lookup"><span data-stu-id="5d5b7-174">[**Troubleshoot**](active-directory-passwords-troubleshoot.md) - Learn how to resolve common issues that we see with SSPR</span></span>

