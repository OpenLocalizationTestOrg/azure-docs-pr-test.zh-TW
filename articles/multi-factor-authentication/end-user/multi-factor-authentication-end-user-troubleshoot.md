---
title: "針對雙步驟驗證進行疑難排解 | Microsoft Docs"
description: "本文件將提供如果使用者使用 Azure Multi-Factor Authentication 遇到問題時，該怎麼辦的資訊。"
services: multi-factor-authentication
keywords: "多重要素驗證用戶端, 驗證的問題, 相互關聯識別碼"
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 8f3aef42-7f66-4656-a7cd-d25a971cb9eb
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: end-user
ms.openlocfilehash: e4b59efd12a64f58634b66590cf6999cc9e68eb6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="get-help-with-two-step-verification"></a><span data-ttu-id="49c98-104">取得雙步驟驗證的說明</span><span class="sxs-lookup"><span data-stu-id="49c98-104">Get help with two-step verification</span></span>
<span data-ttu-id="49c98-105">本文回答人們最常詢問有關雙步驟驗證的問題。</span><span class="sxs-lookup"><span data-stu-id="49c98-105">This article answers the most common questions that people ask about two-step verification.</span></span> 

## <a name="why-do-i-have-to-perform-two-step-verification-can-i-turn-it-off"></a><span data-ttu-id="49c98-106">為什麼必須執行雙步驟驗證？</span><span class="sxs-lookup"><span data-stu-id="49c98-106">Why do I have to perform two-step verification?</span></span> <span data-ttu-id="49c98-107">可以將它關閉嗎？</span><span class="sxs-lookup"><span data-stu-id="49c98-107">Can I turn it off?</span></span>

<span data-ttu-id="49c98-108">雙步驟驗證是貴組織選擇用來保護您帳戶的安全性功能。</span><span class="sxs-lookup"><span data-stu-id="49c98-108">Two-step verification is a security feature that your organization chose to use to protect your accounts.</span></span> <span data-ttu-id="49c98-109">它比只是使用密碼更安全，因為它依賴兩種形式的驗證：您知道和您擁有的東西。</span><span class="sxs-lookup"><span data-stu-id="49c98-109">It's more secure than just a password, because it relies on two forms of authentication: something you know, and something you have with you.</span></span> <span data-ttu-id="49c98-110">您知道的就是密碼。</span><span class="sxs-lookup"><span data-stu-id="49c98-110">The something you know is your password.</span></span> <span data-ttu-id="49c98-111">您擁有的是您通常帶在身邊的手機或裝置。</span><span class="sxs-lookup"><span data-stu-id="49c98-111">The something you have with you is a phone or device that you commonly have with you.</span></span> <span data-ttu-id="49c98-112">當您的帳戶受到雙步驟驗證時，這表示惡意駭客如果以某種方式取得您的密碼，也無法以您的身分登入，因為他們無法存取您的手機。</span><span class="sxs-lookup"><span data-stu-id="49c98-112">When your account is protected with two-step verification, that means that a malicious hacker can't sign in as you if they get your password somehow because they don't have access to your phone, too.</span></span> 

<span data-ttu-id="49c98-113">Microsoft 提供了雙步驟驗證，但您的組織選擇使用該功能。</span><span class="sxs-lookup"><span data-stu-id="49c98-113">Microsoft offers two-step verification, but your organization chooses to use the feature.</span></span> <span data-ttu-id="49c98-114">如果您的 IT 部門要求您，您無法選擇取消使用，就像是您無法選擇取消使用密碼來保護您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="49c98-114">You can't opt out if your IT department requires it of you, just like you can't opt out of using a password to protect your account.</span></span> 

<span data-ttu-id="49c98-115">如果您已為您的個人 Microsoft 帳戶開啟雙步驟驗證，而且想要變更設定，請改為閱讀[關於雙步驟驗證](https://support.microsoft.com/help/12408/microsoft-account-about-two-step-verification)。</span><span class="sxs-lookup"><span data-stu-id="49c98-115">If you have two-step verification turned on for your personal Microsoft account and want to change your settings, read [About two-step verification](https://support.microsoft.com/help/12408/microsoft-account-about-two-step-verification) instead.</span></span> 

## <a name="i-dont-have-my-phone-with-me-today"></a><span data-ttu-id="49c98-116">我今天沒帶手機</span><span class="sxs-lookup"><span data-stu-id="49c98-116">I don't have my phone with me today</span></span>

<span data-ttu-id="49c98-117">有些天您會將手機留在家裡，但仍需要登入工作。</span><span class="sxs-lookup"><span data-stu-id="49c98-117">Some days you leave your phone at home, but still need to sign in at work.</span></span> <span data-ttu-id="49c98-118">您首先應該嘗試使用不同的驗證方法登入。</span><span class="sxs-lookup"><span data-stu-id="49c98-118">The first thing you should try is signing in with a different verification method.</span></span> <span data-ttu-id="49c98-119">當您註冊雙步驟驗證時，是否有設定多個手機號碼？</span><span class="sxs-lookup"><span data-stu-id="49c98-119">When you registered for two-step verification, did you set up more than one phone number?</span></span> <span data-ttu-id="49c98-120">若要嘗試以不同的方法登入，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="49c98-120">To try signing in with a different method, follow these steps:</span></span>

1. <span data-ttu-id="49c98-121">像平常一樣登入。</span><span class="sxs-lookup"><span data-stu-id="49c98-121">Sign in as you normally would.</span></span>
2. <span data-ttu-id="49c98-122">當雙步驟驗證頁面開啟時，選擇 [使用其他驗證選項]。</span><span class="sxs-lookup"><span data-stu-id="49c98-122">When the two-step verification page opens, choose **Use a different verification option**.</span></span>

   ![不同的驗證方式](./media/multi-factor-authentication-end-user-troubleshoot/diff_option.png)

3. <span data-ttu-id="49c98-124">選取您想要使用的驗證選項。</span><span class="sxs-lookup"><span data-stu-id="49c98-124">Select the verification option you want to use.</span></span>
4. <span data-ttu-id="49c98-125">繼續雙步驟驗證。</span><span class="sxs-lookup"><span data-stu-id="49c98-125">Continue with two-step verification.</span></span>

<span data-ttu-id="49c98-126">如果您沒有看到 [使用其他驗證選項] 連結，則表示您在第一次登錄雙步驟驗證時並未設定另一種方法。</span><span class="sxs-lookup"><span data-stu-id="49c98-126">If you don't see the **Use a different verification option** link, then that means you didn't set up alternative methods when you first registered for two-step verification.</span></span> <span data-ttu-id="49c98-127">請連絡您的 IT 部門以取得協助，登入您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="49c98-127">Contact your IT department to get help signing in to your account.</span></span> <span data-ttu-id="49c98-128">一旦您登入，請務必[管理您的設定](multi-factor-authentication-end-user-manage-settings.md)，為下次新增額外的驗證方法。</span><span class="sxs-lookup"><span data-stu-id="49c98-128">Once you're signed in, make sure to [manage your settings](multi-factor-authentication-end-user-manage-settings.md) to add additional verification methods for next time.</span></span> 

<span data-ttu-id="49c98-129">如果您看到 [使用其他驗證選項] 連結，但也無法存取您的替代方法，請連絡您的 IT 部門以取得協助，登入您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="49c98-129">If you do see the **Use a different verification option** link, but you don't have access to your alternative methods either, contact your IT department to get help signing in to your account.</span></span> 

## <a name="i-lost-my-phone-or-got-a-new-number"></a><span data-ttu-id="49c98-130">我遺失手機，或是有了號碼</span><span class="sxs-lookup"><span data-stu-id="49c98-130">I lost my phone or got a new number</span></span>
<span data-ttu-id="49c98-131">有兩種方式可以取回您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="49c98-131">There are two ways to get back in to your account.</span></span> <span data-ttu-id="49c98-132">第一種是使用備用驗證電話號碼登入 (如果已設定)。</span><span class="sxs-lookup"><span data-stu-id="49c98-132">The first is to sign in using your alternate authentication phone number, if you have set one up.</span></span> <span data-ttu-id="49c98-133">第二種是要求您的 IT 部門清除您的設定。</span><span class="sxs-lookup"><span data-stu-id="49c98-133">The second is to ask your IT department to clear your settings.</span></span>

<span data-ttu-id="49c98-134">如果您的手機遺失或遭竊，也建議告知您的 IT 部門，讓他們能重設您的應用程式密碼，並清除任何已記住的裝置。</span><span class="sxs-lookup"><span data-stu-id="49c98-134">If your phone was lost or stolen, we also recommend that you tell your IT department so they can reset your app passwords and clear any remembered devices.</span></span> 

### <a name="use-an-alternate-phone-number"></a><span data-ttu-id="49c98-135">使用備用電話號碼</span><span class="sxs-lookup"><span data-stu-id="49c98-135">Use an alternate phone number</span></span>
<span data-ttu-id="49c98-136">如果您已設定多個驗證選項 (包含不同裝置上的次要電話號碼或驗證器應用程式)，則可以使用其中一個選項來登入。</span><span class="sxs-lookup"><span data-stu-id="49c98-136">If you have set up multiple verification options, including a secondary phone number or an authenticator app on a different device, you can use one of them to sign in.</span></span>

<span data-ttu-id="49c98-137">若要使用備用電話號碼登入，請遵循下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="49c98-137">To sign in using the alternate phone number, follow these steps:</span></span>

1. <span data-ttu-id="49c98-138">像平常一樣登入。</span><span class="sxs-lookup"><span data-stu-id="49c98-138">Sign in as you normally would.</span></span>
2. <span data-ttu-id="49c98-139">系統提示進一步驗證您的帳戶時，請選擇 [使用不同的驗證選項]。</span><span class="sxs-lookup"><span data-stu-id="49c98-139">When prompted to further verify your account, choose **Use a different verification option**.</span></span>
   
   ![不同的驗證方式](./media/multi-factor-authentication-end-user-troubleshoot/diff_option.png)

3. <span data-ttu-id="49c98-141">選取您具有存取權的手機號碼或裝置。</span><span class="sxs-lookup"><span data-stu-id="49c98-141">Select the phone number or device that you have access to.</span></span>
4. <span data-ttu-id="49c98-142">取回您的帳戶之後，請[管理您的設定](multi-factor-authentication-end-user-manage-settings.md)以變更您的驗證電話號碼。</span><span class="sxs-lookup"><span data-stu-id="49c98-142">After you're back in your account, [manage your settings](multi-factor-authentication-end-user-manage-settings.md) to change your authentication phone number.</span></span>

### <a name="clear-your-settings"></a><span data-ttu-id="49c98-143">清除您的設定</span><span class="sxs-lookup"><span data-stu-id="49c98-143">Clear your settings</span></span>
<span data-ttu-id="49c98-144">如果您尚未設定次要驗證手機號碼，則需要連絡 IT 部門來尋求協助。</span><span class="sxs-lookup"><span data-stu-id="49c98-144">If you have not configured a secondary authentication phone number, you have to contact your IT department for help.</span></span> <span data-ttu-id="49c98-145">請他們清除您的帳戶，因此，在下次登入時，系統會提示您重新[註冊雙步驟驗證](multi-factor-authentication-end-user-first-time.md)。</span><span class="sxs-lookup"><span data-stu-id="49c98-145">Have them clear your settings so the next time you sign in, you will be prompted to [register for two-step verification](multi-factor-authentication-end-user-first-time.md) again.</span></span>

## <a name="i-am-not-receiving-a-text-or-call-on-my-phone"></a><span data-ttu-id="49c98-146">我的手機沒收到簡訊或來電</span><span class="sxs-lookup"><span data-stu-id="49c98-146">I am not receiving a text or call on my phone</span></span>
<span data-ttu-id="49c98-147">有幾個原因您可能會嘗試登入，而不是收到簡訊或來電。</span><span class="sxs-lookup"><span data-stu-id="49c98-147">There are several reasons why you may try to sign in, but not receive the text or phone call.</span></span> <span data-ttu-id="49c98-148">如果您的手機過去成功收到過簡訊或來電，則這可能是電話提供者問題，而非帳戶問題。</span><span class="sxs-lookup"><span data-stu-id="49c98-148">If you've successfully received texts or phone calls to your phone in the past, then this is probably an issue with the phone provider, not your account.</span></span> <span data-ttu-id="49c98-149">請確定您的手機收訊良好，而且，如果您嘗試接收文字訊息，請確定您能夠接收文字訊息。</span><span class="sxs-lookup"><span data-stu-id="49c98-149">Make sure that you have good cell signal, and if you are trying to receive a text message make sure that you are able to recieve text messages.</span></span> <span data-ttu-id="49c98-150">要求朋友打電話給您，或是傳送簡訊作為測試。</span><span class="sxs-lookup"><span data-stu-id="49c98-150">Ask a friend to call you or text you as a test.</span></span> 

<span data-ttu-id="49c98-151">如果您已經等待幾分鐘的時間還沒收到文字或通話，則進入您帳戶的最快速方法是嘗試不同的選項。</span><span class="sxs-lookup"><span data-stu-id="49c98-151">If you've waited several minutes for a text or call, the fastest way to get into your account is to try a different option.</span></span>

1. <span data-ttu-id="49c98-152">在等候您驗證的頁面上，選取 [使用不同的驗證選項]。</span><span class="sxs-lookup"><span data-stu-id="49c98-152">Select **Use a different verification option** on the page that's waiting for your verification.</span></span>
   
    ![不同的驗證方式](./media/multi-factor-authentication-end-user-troubleshoot/diff_option.png)
2. <span data-ttu-id="49c98-154">選取您想要使用的電話號碼或傳遞方法。</span><span class="sxs-lookup"><span data-stu-id="49c98-154">Select the phone number or delivery method you want to use.</span></span>
   
    <span data-ttu-id="49c98-155">如果收到多個驗證碼，請使用最新的驗證碼。</span><span class="sxs-lookup"><span data-stu-id="49c98-155">If you received multiple verification codes, use the newest one.</span></span>

<span data-ttu-id="49c98-156">如果您未設定其他方法，請連絡 IT 部門並要求他們清除您的設定。</span><span class="sxs-lookup"><span data-stu-id="49c98-156">If you don’t have another method configured, contact your IT department and ask them to clear your settings.</span></span> <span data-ttu-id="49c98-157">下次登入時，系統會提示您再次[設定多重要素驗證](multi-factor-authentication-end-user-first-time.md)。</span><span class="sxs-lookup"><span data-stu-id="49c98-157">The next time you sign in, you will be prompted to [set up multi-factor authentication](multi-factor-authentication-end-user-first-time.md) again.</span></span>

<span data-ttu-id="49c98-158">如果您經常因手機收訊不良而延遲，則建議在智慧型手機上使用 [Microsoft Authenticator 應用程式](microsoft-authenticator-app-how-to.md)。</span><span class="sxs-lookup"><span data-stu-id="49c98-158">If you often have delays due to bad cell signal, we recommend you use the [Microsoft Authenticator app](microsoft-authenticator-app-how-to.md) on your smartphone.</span></span> <span data-ttu-id="49c98-159">應用程式可以產生您用來登入的隨機安全驗證碼，而且這些代碼不需要任何手機訊號或網際網路連接。</span><span class="sxs-lookup"><span data-stu-id="49c98-159">The app can generate random security codes that you use to sign in, and these codes don't require any cell signal or internet connection.</span></span>

## <a name="app-passwords-are-not-working"></a><span data-ttu-id="49c98-160">應用程式密碼無效</span><span class="sxs-lookup"><span data-stu-id="49c98-160">App passwords are not working</span></span>
<span data-ttu-id="49c98-161">首先，請確定您輸入的是正確的應用程式密碼。</span><span class="sxs-lookup"><span data-stu-id="49c98-161">First, make sure that you have entered the app password correctly.</span></span> <span data-ttu-id="49c98-162">產生的應用程式密碼會取代您的一般密碼，但僅適用於不支援雙步驟驗證的較舊桌面應用程式。</span><span class="sxs-lookup"><span data-stu-id="49c98-162">The generated app password replaces your normal password, but only for older desktop applications that don't support two-step verification.</span></span> <span data-ttu-id="49c98-163">如果仍無法登入，請嘗試登入並[建立新的應用程式密碼](multi-factor-authentication-end-user-app-passwords.md)。</span><span class="sxs-lookup"><span data-stu-id="49c98-163">If it still isn't working, try signing-in and [create a new app password](multi-factor-authentication-end-user-app-passwords.md).</span></span>  <span data-ttu-id="49c98-164">如果還是無法登入，請連絡 IT 部門，要求他們[刪除您現有的應用程式密碼](../multi-factor-authentication-manage-users-and-devices.md)，然後建立新的密碼。</span><span class="sxs-lookup"><span data-stu-id="49c98-164">If it still doesn't work, contact your IT department and have them [delete your existing app passwords](../multi-factor-authentication-manage-users-and-devices.md) and then you can create a new one.</span></span>

## <a name="i-didnt-find-an-answer-to-my-problem"></a><span data-ttu-id="49c98-165">我找不到我問題的解答。</span><span class="sxs-lookup"><span data-stu-id="49c98-165">I didn't find an answer to my problem.</span></span>
<span data-ttu-id="49c98-166">如果您嘗試過這些疑難排解步驟，但仍在遭遇問題，請連絡您的 IT 部門。</span><span class="sxs-lookup"><span data-stu-id="49c98-166">If you've tried these troubleshooting steps but are still running into problems, contact your IT department.</span></span> <span data-ttu-id="49c98-167">他們應該可以協助您。</span><span class="sxs-lookup"><span data-stu-id="49c98-167">They should be able to assist you.</span></span>

## <a name="related-topics"></a><span data-ttu-id="49c98-168">相關主題</span><span class="sxs-lookup"><span data-stu-id="49c98-168">Related topics</span></span>
* [<span data-ttu-id="49c98-169">管理您的雙步驟驗證設定</span><span class="sxs-lookup"><span data-stu-id="49c98-169">Manage your settings for two-step verification</span></span>](multi-factor-authentication-end-user-manage-settings.md)  
* [<span data-ttu-id="49c98-170">Microsoft Authenticator 應用程式常見問題集</span><span class="sxs-lookup"><span data-stu-id="49c98-170">Microsoft Authenticator application FAQ</span></span>](microsoft-authenticator-app-faq.md)

