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
ms.openlocfilehash: daa5f9f6a4c9cf5eb20ffe02368444682c0ccb42
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="roll-out-password-reset-for-users"></a><span data-ttu-id="4c711-103">為使用者推出密碼重設</span><span class="sxs-lookup"><span data-stu-id="4c711-103">Roll out password reset for users</span></span>

<span data-ttu-id="4c711-104">大部分的客戶都會遵循下列步驟，以確保順利推出 SSPR 功能。</span><span class="sxs-lookup"><span data-stu-id="4c711-104">Most customers follow the steps that follow to ensure a smooth rollout of SSPR functionality.</span></span>

1. [<span data-ttu-id="4c711-105">在您的目錄中啟用密碼重設</span><span class="sxs-lookup"><span data-stu-id="4c711-105">Enable password reset in your directory</span></span>](active-directory-passwords-getting-started.md)
2. [<span data-ttu-id="4c711-106">設定密碼回寫的內部部署 AD 權限</span><span class="sxs-lookup"><span data-stu-id="4c711-106">Configure on-premises AD permissions for password writeback</span></span>](active-directory-passwords-how-it-works.md#active-directory-permissions)
3. <span data-ttu-id="4c711-107">[設定密碼回寫](active-directory-passwords-writeback.md#configuring-password-writeback)以將密碼從 Azure AD 回寫到您的內部部署目錄</span><span class="sxs-lookup"><span data-stu-id="4c711-107">[Configure password writeback](active-directory-passwords-writeback.md#configuring-password-writeback) to write passwords from Azure AD back to your on-premises directory</span></span>
4. [<span data-ttu-id="4c711-108">指派和驗證所需的授權</span><span class="sxs-lookup"><span data-stu-id="4c711-108">Assign and verify required licenses</span></span>](active-directory-passwords-licensing.md)
5. <span data-ttu-id="4c711-109">如果您想要逐步推出，可以選擇性地將密碼重設限制於某個使用者群組，以漸進方式推出此功能。</span><span class="sxs-lookup"><span data-stu-id="4c711-109">If you want to roll out gradually, you can optionally limit password reset to a group of users to roll out the feature slowly over time.</span></span> <span data-ttu-id="4c711-110">若要這麼做，請將 [已啟用自助式密碼重設] 切換開關從 [每個人] 設定為 [群組]，然後選取要啟用密碼重設的安全性群組。</span><span class="sxs-lookup"><span data-stu-id="4c711-110">To do this set the **Self Service Password Reset Enabled** toggle from **Everybody** to **A group** and select a security group to enable for password reset.</span></span> <span data-ttu-id="4c711-111">此群組的成員都必須有指派給他們的授權，而這是啟用[以群組為基礎的授權](active-directory-passwords-licensing.md#enable-group-or-user-based-licensing)的好方法。</span><span class="sxs-lookup"><span data-stu-id="4c711-111">The members of this group must all have licenses assigned to them and is a great way to enable [Group Based Licensing](active-directory-passwords-licensing.md#enable-group-or-user-based-licensing).</span></span>
6. <span data-ttu-id="4c711-112">根據您的原則，填入最小的[驗證資料](active-directory-passwords-data.md)集。</span><span class="sxs-lookup"><span data-stu-id="4c711-112">Populate the minimum set of [Authentication Data](active-directory-passwords-data.md), based on your policy.</span></span>
7. <span data-ttu-id="4c711-113">將如何註冊及如何重設的指示傳送給使用者，教導他們如何使用 SSPR。</span><span class="sxs-lookup"><span data-stu-id="4c711-113">Teach your users how to use SSPR, by sending them instructions to show them how to register and how to reset.</span></span>
    > [!NOTE]
    > <span data-ttu-id="4c711-114">以使用者並非系統管理員測試 SSPR，因為 Microsoft 會強制執行 Azure 系統管理員類型帳戶的強式驗證需求。</span><span class="sxs-lookup"><span data-stu-id="4c711-114">Test SSPR with a user and not an administrator as Microsoft enforces strong authentication requirements for Azure administrator type accounts.</span></span> <span data-ttu-id="4c711-115">如需有關系統管理員密碼原則的詳細資訊，請參閱我們的[深入探討文章](active-directory-passwords-how-it-works.md)。</span><span class="sxs-lookup"><span data-stu-id="4c711-115">For more information regarding the administrator password policy, see our [deep dive article](active-directory-passwords-how-it-works.md).</span></span>

8. <span data-ttu-id="4c711-116">您可以選擇在任何時間點強制註冊，並要求使用者在一段時間後重新確認其驗證資訊。</span><span class="sxs-lookup"><span data-stu-id="4c711-116">You can choose to enforce registration at any point, and require users to reconfirm their authentication information after a certain period of time.</span></span> <span data-ttu-id="4c711-117">如果您不希望使用者必須註冊，您可以[部署密碼重設而不要求使用者註冊](active-directory-passwords-data.md)。</span><span class="sxs-lookup"><span data-stu-id="4c711-117">If you don't want your users to have to register, you can [deploy password reset without requiring end-user registration](active-directory-passwords-data.md).</span></span>
9. <span data-ttu-id="4c711-118">經過一段時間，藉由檢視 [Azure AD 所提供的報告](active-directory-passwords-reporting.md)，來檢閱使用者的註冊和使用情形。</span><span class="sxs-lookup"><span data-stu-id="4c711-118">Over time, review users registering and using by viewing the [reporting provided by Azure AD](active-directory-passwords-reporting.md).</span></span>

## <a name="email-based-rollout"></a><span data-ttu-id="4c711-119">以電子郵件為基礎的啟用</span><span class="sxs-lookup"><span data-stu-id="4c711-119">Email-based rollout</span></span>

<span data-ttu-id="4c711-120">許多客戶發現電子郵件行銷活動 (包含易於使用的指示)，這是讓使用者使用 SSPR 的最簡單方法。</span><span class="sxs-lookup"><span data-stu-id="4c711-120">Many customers find an email campaign, with simple to use instructions, is the easiest way to get users to use SSPR.</span></span> [<span data-ttu-id="4c711-121">我們建立了三個可以作為範本的簡單電子郵件，以協助您推出。</span><span class="sxs-lookup"><span data-stu-id="4c711-121">We have created three simple emails that you can use as templates to help in your rollout.</span></span>](https://onedrive.live.com/?authkey=%21AD5ZP%2D8RyJ2Cc6M&id=A0B59A91C740AB16%2125063&cid=A0B59A91C740AB16)

* <span data-ttu-id="4c711-122">**即將推出**電子郵件範本，可使用於推出前幾週或前幾天，讓使用者知道他們需要執行一些動作。</span><span class="sxs-lookup"><span data-stu-id="4c711-122">**Coming Soon** email template to be used in the weeks or days before rollout to let users know they need to do something.</span></span>
* <span data-ttu-id="4c711-123">**立即可用**電子郵件範本，可在推出當天驅使使用者註冊並確認其驗證資料，以便他們在需要時使用 SSPR。</span><span class="sxs-lookup"><span data-stu-id="4c711-123">**Available Now** email template to be used the day of launch to drive users to register and confirm their authentication data so they can use SSPR when they need it.</span></span>
* <span data-ttu-id="4c711-124">**註冊提醒**電子郵件範本，可在部署後幾天以至幾週提醒使用者進行註冊並確認其驗證資料。</span><span class="sxs-lookup"><span data-stu-id="4c711-124">**Sign up Reminder** email template for a few days to weeks after deployment to remind users to register and confirm their authentication data.</span></span>

## <a name="creating-your-own-password-portal"></a><span data-ttu-id="4c711-125">建立您自己的密碼入口網站</span><span class="sxs-lookup"><span data-stu-id="4c711-125">Creating your own password portal</span></span>

<span data-ttu-id="4c711-126">很多大型客戶都選擇裝載網頁並建立 DNS 根項目，例如 https://passwords.contoso.com。</span><span class="sxs-lookup"><span data-stu-id="4c711-126">Many of our larger customers choose to host webpage and create a root DNS entry, like https://passwords.contoso.com.</span></span> <span data-ttu-id="4c711-127">他們會在此頁面中填入 Azure AD 密碼重設、密碼重設註冊、密碼變更入口網站和其他組織特定資訊的連結。</span><span class="sxs-lookup"><span data-stu-id="4c711-127">They populate this page with links to the Azure AD password reset, password reset registration, password change portals, and other organization-specific information.</span></span> <span data-ttu-id="4c711-128">您送出的任何電子郵件或傳單都可以包含一個品牌化、令人印象深刻的 URL，使用者可以在需要使用服務時前往該 URL。</span><span class="sxs-lookup"><span data-stu-id="4c711-128">In any email communications or fliers, you send out, you can then include a branded, memorable, URL that users can go to when they need to use the services.</span></span>

* <span data-ttu-id="4c711-129">密碼重設入口網站 - https://passwordreset.microsoftonline.com/</span><span class="sxs-lookup"><span data-stu-id="4c711-129">Password reset portal - https://passwordreset.microsoftonline.com/</span></span>
* <span data-ttu-id="4c711-130">密碼重設註冊入口網站 - http://aka.ms/ssprsetup</span><span class="sxs-lookup"><span data-stu-id="4c711-130">Password reset registration portal - http://aka.ms/ssprsetup</span></span>
* <span data-ttu-id="4c711-131">密碼變更入口網站 - https://account.activedirectory.windowsazure.com/ChangePassword.aspx</span><span class="sxs-lookup"><span data-stu-id="4c711-131">Password change portal - https://account.activedirectory.windowsazure.com/ChangePassword.aspx</span></span>

## <a name="using-enforced-registration"></a><span data-ttu-id="4c711-132">使用強制註冊</span><span class="sxs-lookup"><span data-stu-id="4c711-132">Using enforced registration</span></span>

<span data-ttu-id="4c711-133">如果您希望使用者註冊密碼重設，可以強制他們在使用 Azure AD 登入時進行註冊。</span><span class="sxs-lookup"><span data-stu-id="4c711-133">If you want your users to register for password reset, you can force them to register when they sign in using Azure AD.</span></span> <span data-ttu-id="4c711-134">您可以從目錄的 [密碼重設] 刀鋒視窗啟用此選項，方法是啟用 [註冊] 索引標籤上的 [要求使用者在登入時註冊] 選項。</span><span class="sxs-lookup"><span data-stu-id="4c711-134">You can enable this option from your directory’s **Password reset** blade by enabling the **Require Users to Register when Signing in** option on the **Registration** tab.</span></span>

<span data-ttu-id="4c711-135">系統管理員可以將 [要求使用者重新確認其驗證資訊的等候天數] 設定為 0-730 天，要求使用者在一段時間後重新註冊。</span><span class="sxs-lookup"><span data-stu-id="4c711-135">Administrators can require users to re-register after a period of time by setting the **Number of days before users are asked to reconfirm their authentication information** between 0-730 days.</span></span>

<span data-ttu-id="4c711-136">啟用此選項之後，使用者會在登入時會看到一則訊息，告知系統管理員已要求他們確認其驗證資訊。</span><span class="sxs-lookup"><span data-stu-id="4c711-136">After you enable this option, users signing will see a message that informs them their administrator has required them to verify their authentication information.</span></span>

## <a name="populate-authentication-data"></a><span data-ttu-id="4c711-137">填入驗證資料</span><span class="sxs-lookup"><span data-stu-id="4c711-137">Populate authentication data</span></span>

<span data-ttu-id="4c711-138">如果您[為使用者填入驗證資料](active-directory-passwords-data.md)，則使用者不需要先註冊密碼重設，就能夠使用 SSPR。</span><span class="sxs-lookup"><span data-stu-id="4c711-138">If you [populate authentication data for your users](active-directory-passwords-data.md), then users do not need to register for password reset before being able to use SSPR.</span></span> <span data-ttu-id="4c711-139">只要使用者定義的驗證資料符合您定義的密碼重設原則，使用者就能夠重設其密碼。</span><span class="sxs-lookup"><span data-stu-id="4c711-139">As long as users have the authentication data defined that meets the password reset policy you have defined, users are able to reset their passwords.</span></span>

## <a name="disabling-self-service-password-reset"></a><span data-ttu-id="4c711-140">停用自助式密碼重設</span><span class="sxs-lookup"><span data-stu-id="4c711-140">Disabling self-service password reset</span></span>

<span data-ttu-id="4c711-141">停用自助式密碼重設很簡單，只要開啟 Azure AD 租用戶並移至 [密碼重設]、[屬性]，然後選擇 [已啟用自助式密碼重設]之下的 [沒有人]。</span><span class="sxs-lookup"><span data-stu-id="4c711-141">Disabling self-service password reset is as simple as opening your Azure AD tenant and going to **Password Reset**, **Properties**, and choosing **Nobody** under **Self Service Password Reset Enabled**</span></span>

## <a name="next-steps"></a><span data-ttu-id="4c711-142">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4c711-142">Next steps</span></span>

<span data-ttu-id="4c711-143">下列連結提供有關使用 Azure AD 重設密碼的其他資訊</span><span class="sxs-lookup"><span data-stu-id="4c711-143">The following links provide additional information regarding password reset using Azure AD</span></span>

* <span data-ttu-id="4c711-144">[**快速入門**](active-directory-passwords-getting-started.md) - 開始執行 Azure AD 自助式密碼管理</span><span class="sxs-lookup"><span data-stu-id="4c711-144">[**Quick Start**](active-directory-passwords-getting-started.md) - Get up and running with Azure AD self service password management</span></span> 
* <span data-ttu-id="4c711-145">[**授權**](active-directory-passwords-licensing.md) - 設定 Azure AD 授權</span><span class="sxs-lookup"><span data-stu-id="4c711-145">[**Licensing**](active-directory-passwords-licensing.md) - Configure your Azure AD Licensing</span></span>
* <span data-ttu-id="4c711-146">[**資料**](active-directory-passwords-data.md) -了解所需的資料以及如何將它使用於密碼管理</span><span class="sxs-lookup"><span data-stu-id="4c711-146">[**Data**](active-directory-passwords-data.md) - Understand the data that is required and how it is used for password management</span></span>
* <span data-ttu-id="4c711-147">[**自訂**](active-directory-passwords-customize.md) - 為您的公司自訂 SSPR 體驗的外觀及操作方式。</span><span class="sxs-lookup"><span data-stu-id="4c711-147">[**Customize**](active-directory-passwords-customize.md) - Customize the look and feel of the SSPR experience for your company.</span></span>
* <span data-ttu-id="4c711-148">[**原則**](active-directory-passwords-policy.md) - 了解並設定 Azure AD 密碼原則</span><span class="sxs-lookup"><span data-stu-id="4c711-148">[**Policy**](active-directory-passwords-policy.md) - Understand and set Azure AD password policies</span></span>
* <span data-ttu-id="4c711-149">[**密碼回寫**](active-directory-passwords-writeback.md) - 密碼回寫如何使用您的內部部署目錄</span><span class="sxs-lookup"><span data-stu-id="4c711-149">[**Password Writeback**](active-directory-passwords-writeback.md) - How does password writeback work with your on-premises directory</span></span>
* <span data-ttu-id="4c711-150">[**報告**](active-directory-passwords-reporting.md) - 探索您的使用者是否、何時、何地存取 SSPR 功能</span><span class="sxs-lookup"><span data-stu-id="4c711-150">[**Reporting**](active-directory-passwords-reporting.md) - Discover if, when, and where your users are accessing SSPR functionality</span></span>
* <span data-ttu-id="4c711-151">[**技術性深入探討**](active-directory-passwords-how-it-works.md) - 深入探索以了解其運作方式</span><span class="sxs-lookup"><span data-stu-id="4c711-151">[**Technical Deep Dive**](active-directory-passwords-how-it-works.md) - Go behind the curtain to understand how it works</span></span>
* <span data-ttu-id="4c711-152">[**常見問題集**](active-directory-passwords-faq.md) - 如何？</span><span class="sxs-lookup"><span data-stu-id="4c711-152">[**Frequently Asked Questions**](active-directory-passwords-faq.md) - How?</span></span> <span data-ttu-id="4c711-153">原因為何？</span><span class="sxs-lookup"><span data-stu-id="4c711-153">Why?</span></span> <span data-ttu-id="4c711-154">何事？</span><span class="sxs-lookup"><span data-stu-id="4c711-154">What?</span></span> <span data-ttu-id="4c711-155">何地？</span><span class="sxs-lookup"><span data-stu-id="4c711-155">Where?</span></span> <span data-ttu-id="4c711-156">何人？</span><span class="sxs-lookup"><span data-stu-id="4c711-156">Who?</span></span> <span data-ttu-id="4c711-157">何時？</span><span class="sxs-lookup"><span data-stu-id="4c711-157">When?</span></span> <span data-ttu-id="4c711-158">- -您一直想要詢問之問題的答案</span><span class="sxs-lookup"><span data-stu-id="4c711-158">- Answers to questions you always wanted to ask</span></span>
* <span data-ttu-id="4c711-159">[**疑難排解**](active-directory-passwords-troubleshoot.md) - 了解如何解決我們看到的 SSPR 常見問題</span><span class="sxs-lookup"><span data-stu-id="4c711-159">[**Troubleshoot**](active-directory-passwords-troubleshoot.md) - Learn how to resolve common issues that we see with SSPR</span></span>