---
title: "推出︰Azure AD SSPR | Microsoft Docs"
description: "成功推出 Azure AD 自助式密碼重設的祕訣"
services: active-directory
keywords: 
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: f8cd7e68-2c8e-4f30-b326-b22b16de9787
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: 73d31679b38ff009a767335adaebc49fbc5a75b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="roll-out-password-reset-for-users"></a><span data-ttu-id="eef8c-103">為使用者推出密碼重設</span><span class="sxs-lookup"><span data-stu-id="eef8c-103">Roll out password reset for users</span></span>

<span data-ttu-id="eef8c-104">大部分的客戶步驟 hello 遵循 tooensure SSPR 功能 smooth 首度發行。</span><span class="sxs-lookup"><span data-stu-id="eef8c-104">Most customers follow hello steps that follow tooensure a smooth rollout of SSPR functionality.</span></span>

1. [<span data-ttu-id="eef8c-105">在您的目錄中啟用密碼重設</span><span class="sxs-lookup"><span data-stu-id="eef8c-105">Enable password reset in your directory</span></span>](active-directory-passwords-getting-started.md)
2. [<span data-ttu-id="eef8c-106">設定密碼回寫的內部部署 AD 權限</span><span class="sxs-lookup"><span data-stu-id="eef8c-106">Configure on-premises AD permissions for password writeback</span></span>](active-directory-passwords-how-it-works.md#active-directory-permissions)
3. <span data-ttu-id="eef8c-107">[設定密碼回寫](active-directory-passwords-writeback.md#configuring-password-writeback)toowrite 從 Azure AD 的密碼回 tooyour 在內部部署目錄</span><span class="sxs-lookup"><span data-stu-id="eef8c-107">[Configure password writeback](active-directory-passwords-writeback.md#configuring-password-writeback) toowrite passwords from Azure AD back tooyour on-premises directory</span></span>
4. [<span data-ttu-id="eef8c-108">指派和驗證所需的授權</span><span class="sxs-lookup"><span data-stu-id="eef8c-108">Assign and verify required licenses</span></span>](active-directory-passwords-licensing.md)
5. <span data-ttu-id="eef8c-109">如果您想 tooroll 出逐漸增加，您可以選擇性地限制密碼重設使用者 tooroll 出 hello 功能 tooa 群組緩時變經過一段時間。</span><span class="sxs-lookup"><span data-stu-id="eef8c-109">If you want tooroll out gradually, you can optionally limit password reset tooa group of users tooroll out hello feature slowly over time.</span></span> <span data-ttu-id="eef8c-110">這設定 hello toodo**自助密碼重設啟用服務**切換從**可否**太**群組**並選取 密碼重設安全性群組 tooenable。</span><span class="sxs-lookup"><span data-stu-id="eef8c-110">toodo this set hello **Self Service Password Reset Enabled** toggle from **Everybody** too**A group** and select a security group tooenable for password reset.</span></span> <span data-ttu-id="eef8c-111">hello 這個群組的成員都必須擁有指派的授權 toothem 和是很好的方法 tooenable[授權群組](active-directory-passwords-licensing.md#enable-group-or-user-based-licensing)。</span><span class="sxs-lookup"><span data-stu-id="eef8c-111">hello members of this group must all have licenses assigned toothem and is a great way tooenable [Group Based Licensing](active-directory-passwords-licensing.md#enable-group-or-user-based-licensing).</span></span>
6. <span data-ttu-id="eef8c-112">填入 hello 最小一組[驗證資料](active-directory-passwords-data.md)，根據您的原則。</span><span class="sxs-lookup"><span data-stu-id="eef8c-112">Populate hello minimum set of [Authentication Data](active-directory-passwords-data.md), based on your policy.</span></span>
7. <span data-ttu-id="eef8c-113">告訴使用者如何傳送指示 tooshow toouse SSPR，它們如何 tooregister 以及 tooreset。</span><span class="sxs-lookup"><span data-stu-id="eef8c-113">Teach your users how toouse SSPR, by sending them instructions tooshow them how tooregister and how tooreset.</span></span>
    > [!NOTE]
    > <span data-ttu-id="eef8c-114">以使用者並非系統管理員測試 SSPR，因為 Microsoft 會強制執行 Azure 系統管理員類型帳戶的強式驗證需求。</span><span class="sxs-lookup"><span data-stu-id="eef8c-114">Test SSPR with a user and not an administrator as Microsoft enforces strong authentication requirements for Azure administrator type accounts.</span></span> <span data-ttu-id="eef8c-115">如需有關 hello 系統管理員密碼原則的詳細資訊，請參閱我們[深入探討文章](active-directory-passwords-how-it-works.md)。</span><span class="sxs-lookup"><span data-stu-id="eef8c-115">For more information regarding hello administrator password policy, see our [deep dive article](active-directory-passwords-how-it-works.md).</span></span>

8. <span data-ttu-id="eef8c-116">您可以選擇在任何時間點，tooenforce 註冊，並要求使用者 tooreconfirm 一段時間之後其驗證資訊。</span><span class="sxs-lookup"><span data-stu-id="eef8c-116">You can choose tooenforce registration at any point, and require users tooreconfirm their authentication information after a certain period of time.</span></span> <span data-ttu-id="eef8c-117">如果您不想您使用者 toohave tooregister，您可以[部署密碼重設而不需要使用者註冊](active-directory-passwords-data.md)。</span><span class="sxs-lookup"><span data-stu-id="eef8c-117">If you don't want your users toohave tooregister, you can [deploy password reset without requiring end-user registration](active-directory-passwords-data.md).</span></span>
9. <span data-ttu-id="eef8c-118">經過一段時間，檢閱 使用者註冊並使用藉由檢視 hello[報告 Azure AD 所提供](active-directory-passwords-reporting.md)。</span><span class="sxs-lookup"><span data-stu-id="eef8c-118">Over time, review users registering and using by viewing hello [reporting provided by Azure AD](active-directory-passwords-reporting.md).</span></span>

## <a name="email-based-rollout"></a><span data-ttu-id="eef8c-119">以電子郵件為基礎的啟用</span><span class="sxs-lookup"><span data-stu-id="eef8c-119">Email-based rollout</span></span>

<span data-ttu-id="eef8c-120">許多客戶發現電子郵件宣傳活動中的，簡單 toouse 指示是 hello 最簡單方式 tooget 使用者 toouse SSPR。</span><span class="sxs-lookup"><span data-stu-id="eef8c-120">Many customers find an email campaign, with simple toouse instructions, is hello easiest way tooget users toouse SSPR.</span></span> [<span data-ttu-id="eef8c-121">我們已經建立三個簡單的電子郵件，您可以使用為範本 toohelp 中首度發行。</span><span class="sxs-lookup"><span data-stu-id="eef8c-121">We have created three simple emails that you can use as templates toohelp in your rollout.</span></span>](https://onedrive.live.com/?authkey=%21AD5ZP%2D8RyJ2Cc6M&id=A0B59A91C740AB16%2125063&cid=A0B59A91C740AB16)

* <span data-ttu-id="eef8c-122">**即將登場**電子郵件範本 toobe hello 週數或天數首度發行 toolet 使用者知道他們需要 toodo 項目中使用。</span><span class="sxs-lookup"><span data-stu-id="eef8c-122">**Coming Soon** email template toobe used in hello weeks or days before rollout toolet users know they need toodo something.</span></span>
* <span data-ttu-id="eef8c-123">**現在可用**電子郵件範本使用 toobe hello 啟動 toodrive 使用者 tooregister 天數，並確認其驗證資料，在需要時，他們即可使用 SSPR。</span><span class="sxs-lookup"><span data-stu-id="eef8c-123">**Available Now** email template toobe used hello day of launch toodrive users tooregister and confirm their authentication data so they can use SSPR when they need it.</span></span>
* <span data-ttu-id="eef8c-124">**登入，以提醒**之後部署 tooremind 使用者 tooregister 電子郵件的幾天 tooweeks 的範本，並確認其驗證資料。</span><span class="sxs-lookup"><span data-stu-id="eef8c-124">**Sign up Reminder** email template for a few days tooweeks after deployment tooremind users tooregister and confirm their authentication data.</span></span>

## <a name="creating-your-own-password-portal"></a><span data-ttu-id="eef8c-125">建立您自己的密碼入口網站</span><span class="sxs-lookup"><span data-stu-id="eef8c-125">Creating your own password portal</span></span>

<span data-ttu-id="eef8c-126">許多較大客戶選擇 toohost 網頁，並建立 DNS 項目，例如 https://passwords.contoso.com 的根目錄。它們會填入此頁面的連結 toohello Azure AD 密碼重設，密碼重設註冊、 密碼變更入口網站及其他組織特定資訊。</span><span class="sxs-lookup"><span data-stu-id="eef8c-126">Many of our larger customers choose toohost webpage and create a root DNS entry, like https://passwords.contoso.com. They populate this page with links toohello Azure AD password reset, password reset registration, password change portals, and other organization-specific information.</span></span> <span data-ttu-id="eef8c-127">在任何電子郵件通訊或廣告傳單做出，您送出，您可以再包含品牌文數，使用者可以前往 toowhen 它們需要 toouse hello 服務的 URL。</span><span class="sxs-lookup"><span data-stu-id="eef8c-127">In any email communications or fliers, you send out, you can then include a branded, memorable, URL that users can go toowhen they need toouse hello services.</span></span>

* <span data-ttu-id="eef8c-128">密碼重設入口網站 - https://passwordreset.microsoftonline.com/</span><span class="sxs-lookup"><span data-stu-id="eef8c-128">Password reset portal - https://passwordreset.microsoftonline.com/</span></span>
* <span data-ttu-id="eef8c-129">密碼重設註冊入口網站 - http://aka.ms/ssprsetup</span><span class="sxs-lookup"><span data-stu-id="eef8c-129">Password reset registration portal - http://aka.ms/ssprsetup</span></span>
* <span data-ttu-id="eef8c-130">密碼變更入口網站 - https://account.activedirectory.windowsazure.com/ChangePassword.aspx</span><span class="sxs-lookup"><span data-stu-id="eef8c-130">Password change portal - https://account.activedirectory.windowsazure.com/ChangePassword.aspx</span></span>

## <a name="using-enforced-registration"></a><span data-ttu-id="eef8c-131">使用強制註冊</span><span class="sxs-lookup"><span data-stu-id="eef8c-131">Using enforced registration</span></span>

<span data-ttu-id="eef8c-132">如果您想要使用者 tooregister 密碼重設，您可以強制它們 tooregister 登入使用 Azure AD 時。</span><span class="sxs-lookup"><span data-stu-id="eef8c-132">If you want your users tooregister for password reset, you can force them tooregister when they sign in using Azure AD.</span></span> <span data-ttu-id="eef8c-133">您可以啟用此選項，從您的目錄**密碼重設**刀鋒視窗，藉由啟用 hello**需要使用者在登入時的 tooRegister**選項 hello**註冊**索引標籤。</span><span class="sxs-lookup"><span data-stu-id="eef8c-133">You can enable this option from your directory’s **Password reset** blade by enabling hello **Require Users tooRegister when Signing in** option on hello **Registration** tab.</span></span>

<span data-ttu-id="eef8c-134">系統管理員可以在一段時間之後使用者 toore 註冊要求設定 hello**數天之後使用者, 詢問 tooreconfirm 其驗證資訊**介於 0-730 天。</span><span class="sxs-lookup"><span data-stu-id="eef8c-134">Administrators can require users toore-register after a period of time by setting hello **Number of days before users are asked tooreconfirm their authentication information** between 0-730 days.</span></span>

<span data-ttu-id="eef8c-135">啟用此選項之後，簽署的使用者會看到訊息，通知他們管理員要求它們 tooverify 其驗證資訊。</span><span class="sxs-lookup"><span data-stu-id="eef8c-135">After you enable this option, users signing will see a message that informs them their administrator has required them tooverify their authentication information.</span></span>

## <a name="populate-authentication-data"></a><span data-ttu-id="eef8c-136">填入驗證資料</span><span class="sxs-lookup"><span data-stu-id="eef8c-136">Populate authentication data</span></span>

<span data-ttu-id="eef8c-137">如果您[設為您的使用者的驗證資料](active-directory-passwords-data.md)，則使用者不需要密碼重設，就能 toouse SSPR tooregister。</span><span class="sxs-lookup"><span data-stu-id="eef8c-137">If you [populate authentication data for your users](active-directory-passwords-data.md), then users do not need tooregister for password reset before being able toouse SSPR.</span></span> <span data-ttu-id="eef8c-138">只要使用者擁有 hello 驗證定義的資料符合您定義 hello 密碼重設原則，使用者會無法 tooreset 他們的密碼。</span><span class="sxs-lookup"><span data-stu-id="eef8c-138">As long as users have hello authentication data defined that meets hello password reset policy you have defined, users are able tooreset their passwords.</span></span>

## <a name="disabling-self-service-password-reset"></a><span data-ttu-id="eef8c-139">停用自助式密碼重設</span><span class="sxs-lookup"><span data-stu-id="eef8c-139">Disabling self-service password reset</span></span>

<span data-ttu-id="eef8c-140">停用自助式密碼重設的很簡單，開啟 Azure AD 租用戶，並將太**密碼重設**，**屬性**，然後選擇**沒有人**下**自助密碼重設啟用**</span><span class="sxs-lookup"><span data-stu-id="eef8c-140">Disabling self-service password reset is as simple as opening your Azure AD tenant and going too**Password Reset**, **Properties**, and choosing **Nobody** under **Self Service Password Reset Enabled**</span></span>

## <a name="next-steps"></a><span data-ttu-id="eef8c-141">後續步驟</span><span class="sxs-lookup"><span data-stu-id="eef8c-141">Next steps</span></span>

<span data-ttu-id="eef8c-142">hello 下列連結提供有關密碼重設使用 Azure AD 的其他資訊</span><span class="sxs-lookup"><span data-stu-id="eef8c-142">hello following links provide additional information regarding password reset using Azure AD</span></span>

* <span data-ttu-id="eef8c-143">[**快速入門**](active-directory-passwords-getting-started.md) - 開始執行 Azure AD 自助式密碼管理</span><span class="sxs-lookup"><span data-stu-id="eef8c-143">[**Quick Start**](active-directory-passwords-getting-started.md) - Get up and running with Azure AD self service password management</span></span> 
* <span data-ttu-id="eef8c-144">[**授權**](active-directory-passwords-licensing.md) - 設定 Azure AD 授權</span><span class="sxs-lookup"><span data-stu-id="eef8c-144">[**Licensing**](active-directory-passwords-licensing.md) - Configure your Azure AD Licensing</span></span>
* <span data-ttu-id="eef8c-145">[**資料**](active-directory-passwords-data.md) -了解所需的 hello 資料及如何使用密碼管理</span><span class="sxs-lookup"><span data-stu-id="eef8c-145">[**Data**](active-directory-passwords-data.md) - Understand hello data that is required and how it is used for password management</span></span>
* <span data-ttu-id="eef8c-146">[**自訂**](active-directory-passwords-customize.md) -自訂的 hello SSPR 體驗您的公司 hello 外觀與風格。</span><span class="sxs-lookup"><span data-stu-id="eef8c-146">[**Customize**](active-directory-passwords-customize.md) - Customize hello look and feel of hello SSPR experience for your company.</span></span>
* <span data-ttu-id="eef8c-147">[**原則**](active-directory-passwords-policy.md) - 了解並設定 Azure AD 密碼原則</span><span class="sxs-lookup"><span data-stu-id="eef8c-147">[**Policy**](active-directory-passwords-policy.md) - Understand and set Azure AD password policies</span></span>
* <span data-ttu-id="eef8c-148">[**密碼回寫**](active-directory-passwords-writeback.md) - 密碼回寫如何使用您的內部部署目錄</span><span class="sxs-lookup"><span data-stu-id="eef8c-148">[**Password Writeback**](active-directory-passwords-writeback.md) - How does password writeback work with your on-premises directory</span></span>
* <span data-ttu-id="eef8c-149">[**報告**](active-directory-passwords-reporting.md) - 探索您的使用者是否、何時、何地存取 SSPR 功能</span><span class="sxs-lookup"><span data-stu-id="eef8c-149">[**Reporting**](active-directory-passwords-reporting.md) - Discover if, when, and where your users are accessing SSPR functionality</span></span>
* <span data-ttu-id="eef8c-150">[**技術的深入探討**](active-directory-passwords-how-it-works.md) -hello 帘 toounderstand 後方移它的運作方式</span><span class="sxs-lookup"><span data-stu-id="eef8c-150">[**Technical Deep Dive**](active-directory-passwords-how-it-works.md) - Go behind hello curtain toounderstand how it works</span></span>
* <span data-ttu-id="eef8c-151">[**常見問題集**](active-directory-passwords-faq.md) - 如何？</span><span class="sxs-lookup"><span data-stu-id="eef8c-151">[**Frequently Asked Questions**](active-directory-passwords-faq.md) - How?</span></span> <span data-ttu-id="eef8c-152">原因為何？</span><span class="sxs-lookup"><span data-stu-id="eef8c-152">Why?</span></span> <span data-ttu-id="eef8c-153">何事？</span><span class="sxs-lookup"><span data-stu-id="eef8c-153">What?</span></span> <span data-ttu-id="eef8c-154">何地？</span><span class="sxs-lookup"><span data-stu-id="eef8c-154">Where?</span></span> <span data-ttu-id="eef8c-155">何人？</span><span class="sxs-lookup"><span data-stu-id="eef8c-155">Who?</span></span> <span data-ttu-id="eef8c-156">何時？</span><span class="sxs-lookup"><span data-stu-id="eef8c-156">When?</span></span> <span data-ttu-id="eef8c-157">-回答您總是想 tooask tooquestions</span><span class="sxs-lookup"><span data-stu-id="eef8c-157">- Answers tooquestions you always wanted tooask</span></span>
* <span data-ttu-id="eef8c-158">[**疑難排解**](active-directory-passwords-troubleshoot.md) -了解如何 tooresolve 常見問題，我們會看到與 SSPR</span><span class="sxs-lookup"><span data-stu-id="eef8c-158">[**Troubleshoot**](active-directory-passwords-troubleshoot.md) - Learn how tooresolve common issues that we see with SSPR</span></span>
