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
ms.openlocfilehash: 07c7f3ad066c735054cb339f6e09aa4d7d23f23a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="quickstart-azure-ad-self-service-password-reset"></a><span data-ttu-id="55a44-103">快速入門︰Azure AD 自助式密碼重設</span><span class="sxs-lookup"><span data-stu-id="55a44-103">Quickstart: Azure AD self-service password reset</span></span>

> [!IMPORTANT]
> <span data-ttu-id="55a44-104">**您來到此處是因為有登入問題嗎？**</span><span class="sxs-lookup"><span data-stu-id="55a44-104">**Are you here because you're having problems signing in?**</span></span> <span data-ttu-id="55a44-105">若是如此， [以下是如何變更和重設密碼的說明](active-directory-passwords-update-your-own-password.md)。</span><span class="sxs-lookup"><span data-stu-id="55a44-105">If so, [here's how you can change and reset your own password](active-directory-passwords-update-your-own-password.md).</span></span>

## <a name="rapidly-deploy-self-service-password-reset"></a><span data-ttu-id="55a44-106">快速部署自助式密碼重設</span><span class="sxs-lookup"><span data-stu-id="55a44-106">Rapidly deploy self-service password reset</span></span>

<span data-ttu-id="55a44-107">自助式密碼重設 (SSPR) 提供了簡單的方法，讓 IT 系統管理員准許使用者重設或解除鎖定其密碼或帳戶。</span><span class="sxs-lookup"><span data-stu-id="55a44-107">Self-service password reset (SSPR) offers a simple means for IT administrators to empower users to reset or unlock their passwords or accounts.</span></span> <span data-ttu-id="55a44-108">系統包含詳細的報告，以追蹤使用者何時使用系統與通知來警示您誤用或濫用。</span><span class="sxs-lookup"><span data-stu-id="55a44-108">The system includes detailed reporting to track when users use the system along with notifications to alert you to misuse or abuse.</span></span>

<span data-ttu-id="55a44-109">本指南假設您已經有有效的試用或經過授權的 Azure AD 租用戶。</span><span class="sxs-lookup"><span data-stu-id="55a44-109">This guide assumes you already have a working trial or licensed Azure AD tenant.</span></span> <span data-ttu-id="55a44-110">如果您需要設定 Azure AD 的說明，請參閱[開始使用 Azure AD](https://azure.microsoft.com/trial/get-started-active-directory/)一文。</span><span class="sxs-lookup"><span data-stu-id="55a44-110">If you need help setting up Azure AD, see the article [Getting Started with Azure AD](https://azure.microsoft.com/trial/get-started-active-directory/).</span></span>

1. <span data-ttu-id="55a44-111">從現有的 Azure AD 租用戶，選取 [密碼重設]</span><span class="sxs-lookup"><span data-stu-id="55a44-111">From your existing Azure AD tenant, select **"Password reset"**</span></span>

2. <span data-ttu-id="55a44-112">從 [屬性] 畫面的 [已啟用自助式密碼重設] 之下選擇下列其中一項：</span><span class="sxs-lookup"><span data-stu-id="55a44-112">From the **"Properties"** screen, under the option "Self Service Password Reset Enabled" choose one of the following</span></span>
    * <span data-ttu-id="55a44-113">沒有人 - 沒有人能夠使用 SSPR 功能</span><span class="sxs-lookup"><span data-stu-id="55a44-113">Nobody - No one is able to use SSPR functionality</span></span>
    * <span data-ttu-id="55a44-114">群組 - 只有您所選的特定 Azure AD 群組成員能夠使用 SSPR 功能</span><span class="sxs-lookup"><span data-stu-id="55a44-114">A group - Only members of a specific Azure AD group that you choose are able to use SSPR functionality</span></span>
    * <span data-ttu-id="55a44-115">每個人 - 在您的 Azure AD 租用戶中具有帳戶的所有使用者都能夠使用 SSPR 功能</span><span class="sxs-lookup"><span data-stu-id="55a44-115">Everybody - All users with accounts in your Azure AD tenant are able to use SSPR functionality</span></span>

3. <span data-ttu-id="55a44-116">從 [驗證方法] 畫面選擇：</span><span class="sxs-lookup"><span data-stu-id="55a44-116">From the **"Authentication methods"** screen choose</span></span>
    * <span data-ttu-id="55a44-117">需要重設的方法數 - 我們最少支援一種方法或最多支援兩種方法</span><span class="sxs-lookup"><span data-stu-id="55a44-117">Number of methods required to reset - We support a minimum of one or a maximum of two</span></span>
    * <span data-ttu-id="55a44-118">使用者可用的方法 - 我們至少需要一種方法，但是有額外的選擇可用也沒關係</span><span class="sxs-lookup"><span data-stu-id="55a44-118">Methods available to users - We need at least one but it never hurts to have an extra choice available</span></span>
        * <span data-ttu-id="55a44-119">**電子郵件**可透過使用者設定的驗證電子郵件地址代碼傳送電子郵件</span><span class="sxs-lookup"><span data-stu-id="55a44-119">**Email** sends an email with a code to the user's configured authentication email address</span></span>
        * <span data-ttu-id="55a44-120">**行動電話**可讓使用者選擇使用其設定的行動電話號碼代碼來接收電話或簡訊</span><span class="sxs-lookup"><span data-stu-id="55a44-120">**Mobile Phone** gives the user the choice to receive a call or text with a code to their configured mobile phone number</span></span>
        * <span data-ttu-id="55a44-121">**辦公室電話**可透過使用者設定的辦公室電話號碼代碼打電話給使用者</span><span class="sxs-lookup"><span data-stu-id="55a44-121">**Office Phone** calls the user with a code to their configured office phone number</span></span>
        * <span data-ttu-id="55a44-122">**安全性問題**會要求您選擇：</span><span class="sxs-lookup"><span data-stu-id="55a44-122">**Security Questions** requires you to choose</span></span>
            * <span data-ttu-id="55a44-123">註冊所需的問題數 - 註冊成功的最低限度，這表示使用者可以選擇回答更多問題來建立可提取的問題集區。</span><span class="sxs-lookup"><span data-stu-id="55a44-123">Number of questions required to register - The minimum for successful registration, meaning a user can choose to answer more to create a pool of questions to pull from.</span></span> <span data-ttu-id="55a44-124">這個選項可以設定為 3 到 5 個問題，而且必須大於或等於重設所需的問題數目。</span><span class="sxs-lookup"><span data-stu-id="55a44-124">This option can be set from 3-5 and must be greater than or equal to the number of questions required to reset.</span></span>
                * <span data-ttu-id="55a44-125">選取安全性問題時按一下 [自訂] 按鈕，即可新增自訂問題</span><span class="sxs-lookup"><span data-stu-id="55a44-125">Custom questions can be added by clicking the "Custom" button when selecting security questions</span></span>
            * <span data-ttu-id="55a44-126">重設所需的問題數 - 可以設定為在允許重設或解除鎖定使用者密碼之前，需正確回答的 3 到 5 個問題。</span><span class="sxs-lookup"><span data-stu-id="55a44-126">Number of questions required to reset - Can be set from 3-5 questions to be answered correctly before allowing a users password to be reset or unlocked.</span></span>

4. <span data-ttu-id="55a44-127">建議︰[自訂] 可讓您變更「連絡系統管理員」連結，以指向您定義的網頁或電子郵件地址</span><span class="sxs-lookup"><span data-stu-id="55a44-127">RECOMMENDED: **"Customization"** allows you to change the "Contact your administrator" link to point to a page or email address you define</span></span>

5. <span data-ttu-id="55a44-128">選擇性︰[註冊] 畫面會提供系統管理員下列選項︰</span><span class="sxs-lookup"><span data-stu-id="55a44-128">OPTIONAL: The **"Registration"** screen provides administrators the options for:</span></span>
    * <span data-ttu-id="55a44-129">登入時要求使用者註冊</span><span class="sxs-lookup"><span data-stu-id="55a44-129">Require users to register when signing in</span></span>
    * <span data-ttu-id="55a44-130">要求使用者重新確認其驗證資訊的等候天數</span><span class="sxs-lookup"><span data-stu-id="55a44-130">Number of days before users are asked to reconfirm their authentication information</span></span>

6. <span data-ttu-id="55a44-131">選擇性︰[通知] 畫面會提供系統管理員下列選項︰</span><span class="sxs-lookup"><span data-stu-id="55a44-131">OPTIONAL: The **"Notification"** screen provides administrators the options to:</span></span>
    * <span data-ttu-id="55a44-132">通知使用者密碼重設</span><span class="sxs-lookup"><span data-stu-id="55a44-132">Notify users on password resets</span></span>
    * <span data-ttu-id="55a44-133">當其他系統管理員重設其密碼時通知所有系統管理員</span><span class="sxs-lookup"><span data-stu-id="55a44-133">Notify all admins when other admins reset their password</span></span>

<span data-ttu-id="55a44-134">**此時，您已為 Azure AD 租用戶設定 SSPR**。</span><span class="sxs-lookup"><span data-stu-id="55a44-134">**At this point, you have configured SSPR for your Azure AD tenant**.</span></span> <span data-ttu-id="55a44-135">您可以在此停止，或繼續設定將密碼同步處理至內部部署 AD 網域。</span><span class="sxs-lookup"><span data-stu-id="55a44-135">You can stop here or continue on to configure synchronization of passwords to an on-premises AD domain.</span></span>

> [!NOTE]
> <span data-ttu-id="55a44-136">以使用者並非系統管理員測試 SSPR，因為 Microsoft 會強制執行 Azure 系統管理員類型帳戶的強式驗證需求。</span><span class="sxs-lookup"><span data-stu-id="55a44-136">Test SSPR with a user and not an administrator as Microsoft enforces strong authentication requirements for Azure administrator type accounts.</span></span> <span data-ttu-id="55a44-137">如需有關系統管理員密碼原則的詳細資訊，請參閱我們的[密碼原則文章](active-directory-passwords-policy.md#administrator-password-policy-differences)。</span><span class="sxs-lookup"><span data-stu-id="55a44-137">For more information regarding the administrator password policy, see our [password policy article](active-directory-passwords-policy.md#administrator-password-policy-differences).</span></span>

## <a name="configure-synchronization-to-existing-identity-source"></a><span data-ttu-id="55a44-138">設定現有身分識別來源的同步處理</span><span class="sxs-lookup"><span data-stu-id="55a44-138">Configure synchronization to existing identity source</span></span>

<span data-ttu-id="55a44-139">若要啟用內部部署身分識別同步處理至 Azure AD，您必須在您組織中的伺服器上安裝及設定 [Azure AD Connect](./connect/active-directory-aadconnect.md)。</span><span class="sxs-lookup"><span data-stu-id="55a44-139">To enable on-premises identity synchronization to Azure AD, you need to install and configure [Azure AD Connect](./connect/active-directory-aadconnect.md) on a server in your organization.</span></span> <span data-ttu-id="55a44-140">此應用程式會將您現有身分識別來源的使用者和群組同步到您的 Azure AD 租用戶。</span><span class="sxs-lookup"><span data-stu-id="55a44-140">This application handles synchronizing users and groups from your existing identity source to your Azure AD tenant.</span></span>

* [<span data-ttu-id="55a44-141">從 DirSync 或 Azure AD Sync 升級至 Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="55a44-141">Upgrade from DirSync or Azure AD Sync to Azure AD Connect</span></span>](./connect/active-directory-aadconnect-dirsync-deprecated.md)
* [<span data-ttu-id="55a44-142">使用快速設定開始使用 Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="55a44-142">Getting started with Azure AD Connect using express settings</span></span>](./connect/active-directory-aadconnect-get-started-express.md)
* <span data-ttu-id="55a44-143">[設定密碼回寫](active-directory-passwords-writeback.md#configuring-password-writeback)以將密碼從 Azure AD 回寫到您的內部部署目錄。</span><span class="sxs-lookup"><span data-stu-id="55a44-143">[Configure password writeback](active-directory-passwords-writeback.md#configuring-password-writeback) to write passwords from Azure AD back to your on-premises directory.</span></span>

## <a name="disabling-self-service-password-reset"></a><span data-ttu-id="55a44-144">停用自助式密碼重設</span><span class="sxs-lookup"><span data-stu-id="55a44-144">Disabling self-service password reset</span></span>

<span data-ttu-id="55a44-145">停用自助式密碼重設很簡單，只要開啟 Azure AD 租用戶並移至 [密碼重設]、[屬性] > 選擇 [已啟用自助式密碼重設] 之下的 [無]。</span><span class="sxs-lookup"><span data-stu-id="55a44-145">Disabling self-service password reset is as simple as opening your Azure AD tenant and going to **Password Reset > Properties** > choose **None** under **Self Service Password Reset Enabled**</span></span>

### <a name="learn-more"></a><span data-ttu-id="55a44-146">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="55a44-146">Learn more</span></span>
<span data-ttu-id="55a44-147">下列連結提供有關使用 Azure AD 重設密碼的其他資訊</span><span class="sxs-lookup"><span data-stu-id="55a44-147">The following links provide additional information regarding password reset using Azure AD</span></span>

* <span data-ttu-id="55a44-148">[**授權**](active-directory-passwords-licensing.md) - 設定 Azure AD 授權</span><span class="sxs-lookup"><span data-stu-id="55a44-148">[**Licensing**](active-directory-passwords-licensing.md) - Configure your Azure AD Licensing</span></span>
* <span data-ttu-id="55a44-149">[**資料**](active-directory-passwords-data.md) -了解所需的資料以及如何將它使用於密碼管理</span><span class="sxs-lookup"><span data-stu-id="55a44-149">[**Data**](active-directory-passwords-data.md) - Understand the data that is required and how it is used for password management</span></span>
* <span data-ttu-id="55a44-150">[**推出**](active-directory-passwords-best-practices.md) - 使用此處提供的指引來規劃 SSPR 並將它部署至使用者</span><span class="sxs-lookup"><span data-stu-id="55a44-150">[**Rollout**](active-directory-passwords-best-practices.md) - Plan and deploy SSPR to your users using the guidance found here</span></span>
* <span data-ttu-id="55a44-151">[**自訂**](active-directory-passwords-customize.md) - 為您的公司自訂 SSPR 體驗的外觀及操作方式。</span><span class="sxs-lookup"><span data-stu-id="55a44-151">[**Customize**](active-directory-passwords-customize.md) - Customize the look and feel of the SSPR experience for your company.</span></span>
* <span data-ttu-id="55a44-152">[**原則**](active-directory-passwords-policy.md) - 了解並設定 Azure AD 密碼原則</span><span class="sxs-lookup"><span data-stu-id="55a44-152">[**Policy**](active-directory-passwords-policy.md) - Understand and set Azure AD password policies</span></span>
* <span data-ttu-id="55a44-153">[**報告**](active-directory-passwords-reporting.md) - 探索您的使用者是否、何時、何地存取 SSPR 功能</span><span class="sxs-lookup"><span data-stu-id="55a44-153">[**Reporting**](active-directory-passwords-reporting.md) - Discover if, when, and where your users are accessing SSPR functionality</span></span>
* <span data-ttu-id="55a44-154">[**技術性深入探討**](active-directory-passwords-how-it-works.md) - 深入探索以了解其運作方式</span><span class="sxs-lookup"><span data-stu-id="55a44-154">[**Technical Deep Dive**](active-directory-passwords-how-it-works.md) - Go behind the curtain to understand how it works</span></span>
* <span data-ttu-id="55a44-155">[**常見問題集**](active-directory-passwords-faq.md) - 如何？</span><span class="sxs-lookup"><span data-stu-id="55a44-155">[**Frequently Asked Questions**](active-directory-passwords-faq.md) - How?</span></span> <span data-ttu-id="55a44-156">原因為何？</span><span class="sxs-lookup"><span data-stu-id="55a44-156">Why?</span></span> <span data-ttu-id="55a44-157">何事？</span><span class="sxs-lookup"><span data-stu-id="55a44-157">What?</span></span> <span data-ttu-id="55a44-158">何地？</span><span class="sxs-lookup"><span data-stu-id="55a44-158">Where?</span></span> <span data-ttu-id="55a44-159">何人？</span><span class="sxs-lookup"><span data-stu-id="55a44-159">Who?</span></span> <span data-ttu-id="55a44-160">何時？</span><span class="sxs-lookup"><span data-stu-id="55a44-160">When?</span></span> <span data-ttu-id="55a44-161">- -您一直想要詢問之問題的答案</span><span class="sxs-lookup"><span data-stu-id="55a44-161">- Answers to questions you always wanted to ask</span></span>
* <span data-ttu-id="55a44-162">[**疑難排解**](active-directory-passwords-troubleshoot.md) - 了解如何解決我們看到的 SSPR 常見問題</span><span class="sxs-lookup"><span data-stu-id="55a44-162">[**Troubleshoot**](active-directory-passwords-troubleshoot.md) - Learn how to resolve common issues that we see with SSPR</span></span>

## <a name="next-steps"></a><span data-ttu-id="55a44-163">後續步驟</span><span class="sxs-lookup"><span data-stu-id="55a44-163">Next steps</span></span>

<span data-ttu-id="55a44-164">在本快速入門中，您已學到如何為您的使用者設定自助式密碼重設。</span><span class="sxs-lookup"><span data-stu-id="55a44-164">In this quickstart, you’ve learned how to configure self-service password reset for your users.</span></span> <span data-ttu-id="55a44-165">若要繼續在 Azure 入口網站完成這些步驟，請遵循以下的入口網站連結。</span><span class="sxs-lookup"><span data-stu-id="55a44-165">To continue to the Azure portal to complete these steps follow the link below to the portal.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="55a44-166">啟用自助密碼重設</span><span class="sxs-lookup"><span data-stu-id="55a44-166">Enable self-service password reset</span></span>](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/PasswordReset)

