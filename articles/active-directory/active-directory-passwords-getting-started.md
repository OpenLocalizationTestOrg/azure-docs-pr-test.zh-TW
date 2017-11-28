---
title: "快速入門︰Azure AD SSPR | Microsoft Docs"
description: "快速部署 Azure AD 自助式密碼重設"
services: active-directory
keywords: 
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: bde8799f-0b42-446a-ad95-7ebb374c3bec
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/07/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: 4fed3a1c690fd6423ee5d3e5baef690d8896fbe9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-azure-ad-self-service-password-reset"></a><span data-ttu-id="b0af2-103">快速入門︰Azure AD 自助式密碼重設</span><span class="sxs-lookup"><span data-stu-id="b0af2-103">Quickstart: Azure AD self-service password reset</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b0af2-104">**您來到此處是因為有登入問題嗎？**</span><span class="sxs-lookup"><span data-stu-id="b0af2-104">**Are you here because you're having problems signing in?**</span></span> <span data-ttu-id="b0af2-105">若是如此， [以下是如何變更和重設密碼的說明](active-directory-passwords-update-your-own-password.md)。</span><span class="sxs-lookup"><span data-stu-id="b0af2-105">If so, [here's how you can change and reset your own password](active-directory-passwords-update-your-own-password.md).</span></span>

## <a name="rapidly-deploy-self-service-password-reset"></a><span data-ttu-id="b0af2-106">快速部署自助式密碼重設</span><span class="sxs-lookup"><span data-stu-id="b0af2-106">Rapidly deploy self-service password reset</span></span>

<span data-ttu-id="b0af2-107">自助式密碼重設 (SSPR) 提供簡單的方法，用於 IT 系統管理員 tooempower 使用者 tooreset 或其密碼或帳戶解除鎖定。</span><span class="sxs-lookup"><span data-stu-id="b0af2-107">Self-service password reset (SSPR) offers a simple means for IT administrators tooempower users tooreset or unlock their passwords or accounts.</span></span> <span data-ttu-id="b0af2-108">hello 系統包含詳細的報告 tootrack 當使用者使用 hello 系統，以及通知 tooalert 您 toomisuse 或濫用。</span><span class="sxs-lookup"><span data-stu-id="b0af2-108">hello system includes detailed reporting tootrack when users use hello system along with notifications tooalert you toomisuse or abuse.</span></span>

<span data-ttu-id="b0af2-109">本指南假設您已經有有效的試用或經過授權的 Azure AD 租用戶。</span><span class="sxs-lookup"><span data-stu-id="b0af2-109">This guide assumes you already have a working trial or licensed Azure AD tenant.</span></span> <span data-ttu-id="b0af2-110">如果您需要設定 Azure AD 的說明，請參閱 hello 文章[開始使用 Azure AD](https://azure.microsoft.com/trial/get-started-active-directory/)。</span><span class="sxs-lookup"><span data-stu-id="b0af2-110">If you need help setting up Azure AD, see hello article [Getting Started with Azure AD](https://azure.microsoft.com/trial/get-started-active-directory/).</span></span>

1. <span data-ttu-id="b0af2-111">從現有的 Azure AD 租用戶，選取 [密碼重設]</span><span class="sxs-lookup"><span data-stu-id="b0af2-111">From your existing Azure AD tenant, select **"Password reset"**</span></span>

2. <span data-ttu-id="b0af2-112">從 hello **「 屬性 」**畫面中的，「 自助密碼重設啟用服務 」 選擇 hello 下列其中一種 hello 選項底下</span><span class="sxs-lookup"><span data-stu-id="b0af2-112">From hello **"Properties"** screen, under hello option "Self Service Password Reset Enabled" choose one of hello following</span></span>
    * <span data-ttu-id="b0af2-113">沒有人-沒有一個是可以 toouse SSPR 功能</span><span class="sxs-lookup"><span data-stu-id="b0af2-113">Nobody - No one is able toouse SSPR functionality</span></span>
    * <span data-ttu-id="b0af2-114">您選擇的群組-只有特定的 Azure AD 的成員群組都可以 toouse SSPR 功能</span><span class="sxs-lookup"><span data-stu-id="b0af2-114">A group - Only members of a specific Azure AD group that you choose are able toouse SSPR functionality</span></span>
    * <span data-ttu-id="b0af2-115">每個人的帳戶在 Azure AD 租用戶中使用的所有使用者都能 toouse SSPR 功能</span><span class="sxs-lookup"><span data-stu-id="b0af2-115">Everybody - All users with accounts in your Azure AD tenant are able toouse SSPR functionality</span></span>

3. <span data-ttu-id="b0af2-116">從 hello **「 驗證方法 」**選擇畫面</span><span class="sxs-lookup"><span data-stu-id="b0af2-116">From hello **"Authentication methods"** screen choose</span></span>
    * <span data-ttu-id="b0af2-117">所需的方法數目 tooreset-我們支援至少有一個或兩個最大值</span><span class="sxs-lookup"><span data-stu-id="b0af2-117">Number of methods required tooreset - We support a minimum of one or a maximum of two</span></span>
    * <span data-ttu-id="b0af2-118">方法可用 toousers-我們至少需要一個，但永遠不會損及 toohave 可用的額外選項</span><span class="sxs-lookup"><span data-stu-id="b0af2-118">Methods available toousers - We need at least one but it never hurts toohave an extra choice available</span></span>
        * <span data-ttu-id="b0af2-119">**電子郵件**會傳送一封電子郵件與程式碼 toohello 使用者所設定的驗證電子郵件地址</span><span class="sxs-lookup"><span data-stu-id="b0af2-119">**Email** sends an email with a code toohello user's configured authentication email address</span></span>
        * <span data-ttu-id="b0af2-120">**行動電話**提供 hello 使用者 hello 選擇 tooreceive 呼叫或使用程式碼 tootheir 文字設定行動電話號碼</span><span class="sxs-lookup"><span data-stu-id="b0af2-120">**Mobile Phone** gives hello user hello choice tooreceive a call or text with a code tootheir configured mobile phone number</span></span>
        * <span data-ttu-id="b0af2-121">**辦公室電話**呼叫 hello 使用者與程式碼 tootheir 設定辦公室電話號碼</span><span class="sxs-lookup"><span data-stu-id="b0af2-121">**Office Phone** calls hello user with a code tootheir configured office phone number</span></span>
        * <span data-ttu-id="b0af2-122">**安全性問題**toochoose 會要求您</span><span class="sxs-lookup"><span data-stu-id="b0af2-122">**Security Questions** requires you toochoose</span></span>
            * <span data-ttu-id="b0af2-123">所需的問題數目 tooregister-hello 最小值為登錄成功，這表示使用者可以選擇 tooanswer 集區的質疑 toopull 從多個 toocreate。</span><span class="sxs-lookup"><span data-stu-id="b0af2-123">Number of questions required tooregister - hello minimum for successful registration, meaning a user can choose tooanswer more toocreate a pool of questions toopull from.</span></span> <span data-ttu-id="b0af2-124">此選項可設定為 3-5，且必須大於或等於 toohello 問題需要 tooreset 數目。</span><span class="sxs-lookup"><span data-stu-id="b0af2-124">This option can be set from 3-5 and must be greater than or equal toohello number of questions required tooreset.</span></span>
                * <span data-ttu-id="b0af2-125">依序按一下 hello 「 自訂 」 按鈕，僅選擇安全性問題時可以加入自訂的問題</span><span class="sxs-lookup"><span data-stu-id="b0af2-125">Custom questions can be added by clicking hello "Custom" button when selecting security questions</span></span>
            * <span data-ttu-id="b0af2-126">所需的問題 tooreset-可設定為 3-5 問題 toobe 允許解除鎖定或重設使用者密碼 toobe 之前正確解答。</span><span class="sxs-lookup"><span data-stu-id="b0af2-126">Number of questions required tooreset - Can be set from 3-5 questions toobe answered correctly before allowing a users password toobe reset or unlocked.</span></span>

4. <span data-ttu-id="b0af2-127">建議使用： **「 自訂 」** toochange hello 「 連絡您的系統管理員 」 連結 toopoint tooa 頁面或電子郵件地址您定義可讓您</span><span class="sxs-lookup"><span data-stu-id="b0af2-127">RECOMMENDED: **"Customization"** allows you toochange hello "Contact your administrator" link toopoint tooa page or email address you define</span></span>

5. <span data-ttu-id="b0af2-128">選擇性： hello **「 註冊 」**畫面會提供系統管理員的 hello 選項：</span><span class="sxs-lookup"><span data-stu-id="b0af2-128">OPTIONAL: hello **"Registration"** screen provides administrators hello options for:</span></span>
    * <span data-ttu-id="b0af2-129">在登入時，要求使用者 tooregister</span><span class="sxs-lookup"><span data-stu-id="b0af2-129">Require users tooregister when signing in</span></span>
    * <span data-ttu-id="b0af2-130">數天之後使用者, 詢問 tooreconfirm 其驗證資訊</span><span class="sxs-lookup"><span data-stu-id="b0af2-130">Number of days before users are asked tooreconfirm their authentication information</span></span>

6. <span data-ttu-id="b0af2-131">選擇性： hello **「 通知 」**畫面會提供系統管理員 hello 選項：</span><span class="sxs-lookup"><span data-stu-id="b0af2-131">OPTIONAL: hello **"Notification"** screen provides administrators hello options to:</span></span>
    * <span data-ttu-id="b0af2-132">通知使用者密碼重設</span><span class="sxs-lookup"><span data-stu-id="b0af2-132">Notify users on password resets</span></span>
    * <span data-ttu-id="b0af2-133">當其他系統管理員重設其密碼時通知所有系統管理員</span><span class="sxs-lookup"><span data-stu-id="b0af2-133">Notify all admins when other admins reset their password</span></span>

<span data-ttu-id="b0af2-134">**此時，您已為 Azure AD 租用戶設定 SSPR**。</span><span class="sxs-lookup"><span data-stu-id="b0af2-134">**At this point, you have configured SSPR for your Azure AD tenant**.</span></span> <span data-ttu-id="b0af2-135">您可以在此停止或繼續的 tooconfigure 密碼 tooan 的同步處理內部部署 AD 網域。</span><span class="sxs-lookup"><span data-stu-id="b0af2-135">You can stop here or continue on tooconfigure synchronization of passwords tooan on-premises AD domain.</span></span>

> [!NOTE]
> <span data-ttu-id="b0af2-136">以使用者並非系統管理員測試 SSPR，因為 Microsoft 會強制執行 Azure 系統管理員類型帳戶的強式驗證需求。</span><span class="sxs-lookup"><span data-stu-id="b0af2-136">Test SSPR with a user and not an administrator as Microsoft enforces strong authentication requirements for Azure administrator type accounts.</span></span> <span data-ttu-id="b0af2-137">如需有關 hello 系統管理員密碼原則的詳細資訊，請參閱我們[密碼原則文章](active-directory-passwords-policy.md#administrator-password-policy-differences)。</span><span class="sxs-lookup"><span data-stu-id="b0af2-137">For more information regarding hello administrator password policy, see our [password policy article](active-directory-passwords-policy.md#administrator-password-policy-differences).</span></span>

## <a name="configure-synchronization-tooexisting-identity-source"></a><span data-ttu-id="b0af2-138">設定同步處理 tooexisting 識別來源</span><span class="sxs-lookup"><span data-stu-id="b0af2-138">Configure synchronization tooexisting identity source</span></span>

<span data-ttu-id="b0af2-139">tooenable 內部部署身分識別同步處理 tooAzure AD，您需要 tooinstall，以及設定[Azure AD Connect](./connect/active-directory-aadconnect.md)貴組織中的伺服器上。</span><span class="sxs-lookup"><span data-stu-id="b0af2-139">tooenable on-premises identity synchronization tooAzure AD, you need tooinstall and configure [Azure AD Connect](./connect/active-directory-aadconnect.md) on a server in your organization.</span></span> <span data-ttu-id="b0af2-140">這個應用程式會同步處理使用者和群組的現有識別來源 tooyour Azure AD 租用戶。</span><span class="sxs-lookup"><span data-stu-id="b0af2-140">This application handles synchronizing users and groups from your existing identity source tooyour Azure AD tenant.</span></span>

* [<span data-ttu-id="b0af2-141">從 DirSync 或 Azure AD Sync tooAzure 升級 AD Connect</span><span class="sxs-lookup"><span data-stu-id="b0af2-141">Upgrade from DirSync or Azure AD Sync tooAzure AD Connect</span></span>](./connect/active-directory-aadconnect-dirsync-deprecated.md)
* [<span data-ttu-id="b0af2-142">使用快速設定開始使用 Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="b0af2-142">Getting started with Azure AD Connect using express settings</span></span>](./connect/active-directory-aadconnect-get-started-express.md)
* <span data-ttu-id="b0af2-143">[設定密碼回寫](active-directory-passwords-writeback.md#configuring-password-writeback)toowrite 從 Azure AD 的密碼回 tooyour 在內部部署目錄。</span><span class="sxs-lookup"><span data-stu-id="b0af2-143">[Configure password writeback](active-directory-passwords-writeback.md#configuring-password-writeback) toowrite passwords from Azure AD back tooyour on-premises directory.</span></span>

## <a name="disabling-self-service-password-reset"></a><span data-ttu-id="b0af2-144">停用自助式密碼重設</span><span class="sxs-lookup"><span data-stu-id="b0af2-144">Disabling self-service password reset</span></span>

<span data-ttu-id="b0af2-145">停用自助式密碼重設的很簡單，開啟 Azure AD 租用戶，並將太**密碼重設 > 屬性**> 選擇**無**下**自助密碼重設已啟用**</span><span class="sxs-lookup"><span data-stu-id="b0af2-145">Disabling self-service password reset is as simple as opening your Azure AD tenant and going too**Password Reset > Properties** > choose **None** under **Self Service Password Reset Enabled**</span></span>

### <a name="learn-more"></a><span data-ttu-id="b0af2-146">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="b0af2-146">Learn more</span></span>
<span data-ttu-id="b0af2-147">hello 下列連結提供有關密碼重設使用 Azure AD 的其他資訊</span><span class="sxs-lookup"><span data-stu-id="b0af2-147">hello following links provide additional information regarding password reset using Azure AD</span></span>

* <span data-ttu-id="b0af2-148">[**授權**](active-directory-passwords-licensing.md) - 設定 Azure AD 授權</span><span class="sxs-lookup"><span data-stu-id="b0af2-148">[**Licensing**](active-directory-passwords-licensing.md) - Configure your Azure AD Licensing</span></span>
* <span data-ttu-id="b0af2-149">[**資料**](active-directory-passwords-data.md) -了解所需的 hello 資料及如何使用密碼管理</span><span class="sxs-lookup"><span data-stu-id="b0af2-149">[**Data**](active-directory-passwords-data.md) - Understand hello data that is required and how it is used for password management</span></span>
* <span data-ttu-id="b0af2-150">[**首度發行**](active-directory-passwords-best-practices.md) -計劃和部署 SSPR tooyour 使用者 hello 指引，請參閱</span><span class="sxs-lookup"><span data-stu-id="b0af2-150">[**Rollout**](active-directory-passwords-best-practices.md) - Plan and deploy SSPR tooyour users using hello guidance found here</span></span>
* <span data-ttu-id="b0af2-151">[**自訂**](active-directory-passwords-customize.md) -自訂的 hello SSPR 體驗您的公司 hello 外觀與風格。</span><span class="sxs-lookup"><span data-stu-id="b0af2-151">[**Customize**](active-directory-passwords-customize.md) - Customize hello look and feel of hello SSPR experience for your company.</span></span>
* <span data-ttu-id="b0af2-152">[**原則**](active-directory-passwords-policy.md) - 了解並設定 Azure AD 密碼原則</span><span class="sxs-lookup"><span data-stu-id="b0af2-152">[**Policy**](active-directory-passwords-policy.md) - Understand and set Azure AD password policies</span></span>
* <span data-ttu-id="b0af2-153">[**報告**](active-directory-passwords-reporting.md) - 探索您的使用者是否、何時、何地存取 SSPR 功能</span><span class="sxs-lookup"><span data-stu-id="b0af2-153">[**Reporting**](active-directory-passwords-reporting.md) - Discover if, when, and where your users are accessing SSPR functionality</span></span>
* <span data-ttu-id="b0af2-154">[**技術的深入探討**](active-directory-passwords-how-it-works.md) -hello 帘 toounderstand 後方移它的運作方式</span><span class="sxs-lookup"><span data-stu-id="b0af2-154">[**Technical Deep Dive**](active-directory-passwords-how-it-works.md) - Go behind hello curtain toounderstand how it works</span></span>
* <span data-ttu-id="b0af2-155">[**常見問題集**](active-directory-passwords-faq.md) - 如何？</span><span class="sxs-lookup"><span data-stu-id="b0af2-155">[**Frequently Asked Questions**](active-directory-passwords-faq.md) - How?</span></span> <span data-ttu-id="b0af2-156">原因為何？</span><span class="sxs-lookup"><span data-stu-id="b0af2-156">Why?</span></span> <span data-ttu-id="b0af2-157">何事？</span><span class="sxs-lookup"><span data-stu-id="b0af2-157">What?</span></span> <span data-ttu-id="b0af2-158">何地？</span><span class="sxs-lookup"><span data-stu-id="b0af2-158">Where?</span></span> <span data-ttu-id="b0af2-159">何人？</span><span class="sxs-lookup"><span data-stu-id="b0af2-159">Who?</span></span> <span data-ttu-id="b0af2-160">何時？</span><span class="sxs-lookup"><span data-stu-id="b0af2-160">When?</span></span> <span data-ttu-id="b0af2-161">-回答您總是想 tooask tooquestions</span><span class="sxs-lookup"><span data-stu-id="b0af2-161">- Answers tooquestions you always wanted tooask</span></span>
* <span data-ttu-id="b0af2-162">[**疑難排解**](active-directory-passwords-troubleshoot.md) -了解如何 tooresolve 常見問題，我們會看到與 SSPR</span><span class="sxs-lookup"><span data-stu-id="b0af2-162">[**Troubleshoot**](active-directory-passwords-troubleshoot.md) - Learn how tooresolve common issues that we see with SSPR</span></span>

## <a name="next-steps"></a><span data-ttu-id="b0af2-163">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b0af2-163">Next steps</span></span>

<span data-ttu-id="b0af2-164">本快速入門中，您學到如何 tooconfigure 自助式密碼重設為您的使用者。</span><span class="sxs-lookup"><span data-stu-id="b0af2-164">In this quickstart, you’ve learned how tooconfigure self-service password reset for your users.</span></span> <span data-ttu-id="b0af2-165">toocontinue toohello 遵循這些步驟的 Azure 入口網站 toocomplete hello toohello 入口網站下方的連結。</span><span class="sxs-lookup"><span data-stu-id="b0af2-165">toocontinue toohello Azure portal toocomplete these steps follow hello link below toohello portal.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b0af2-166">啟用自助密碼重設</span><span class="sxs-lookup"><span data-stu-id="b0af2-166">Enable self-service password reset</span></span>](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/PasswordReset)

