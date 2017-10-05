---
title: "使用雙步驟驗證的 Azure MFA 登入 | Microsoft Docs"
description: "本頁面將指引您移至何處才能看到 Azure MFA 可用的各種登入方法。"
keywords: "使用者驗證, 登入經驗, 使用行動電話登入, 使用辦公室電話登入"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: b310b762-471b-4b26-887a-a321c9e81d46
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/02/2017
ms.author: kgremban
ms.reviewer: librown
ms.custom: end-user
ms.openlocfilehash: d12115be61ca00dfb86dd822ccae9f9096fa796a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="the-sign-in-experience-with-azure-multi-factor-authentication"></a><span data-ttu-id="89e45-104">Azure Multi-Factor Authentication 的登入體驗</span><span class="sxs-lookup"><span data-stu-id="89e45-104">The sign-in experience with Azure Multi-Factor Authentication</span></span>
> [!NOTE]
> <span data-ttu-id="89e45-105">本文的目的逐步解說典型的登入體驗。</span><span class="sxs-lookup"><span data-stu-id="89e45-105">The purpose of this article is to walk through a typical sign-in experience.</span></span> <span data-ttu-id="89e45-106">如需登入的說明或疑難排解問題，請參閱 [使用 Azure Multi-Factor Authentication 時碰到困難](multi-factor-authentication-end-user-troubleshoot.md)。</span><span class="sxs-lookup"><span data-stu-id="89e45-106">For help with signing in, or to troubleshoot problems, see [Having trouble with Azure Multi-Factor Authentication](multi-factor-authentication-end-user-troubleshoot.md).</span></span>

## <a name="what-will-your-sign-in-experience-be"></a><span data-ttu-id="89e45-107">您的登入體驗將會如何？</span><span class="sxs-lookup"><span data-stu-id="89e45-107">What will your sign-in experience be?</span></span>
<span data-ttu-id="89e45-108">您的登入體驗會根據您選擇來做為第二個要素的項目而不同︰撥打電話、驗證應用程式或簡訊。</span><span class="sxs-lookup"><span data-stu-id="89e45-108">Your sign-in experience differs depending on what you choose to use as your second factor: a phone call, an authentication app, or texts.</span></span> <span data-ttu-id="89e45-109">選擇最符合您的情況的一個選項：</span><span class="sxs-lookup"><span data-stu-id="89e45-109">Choose the option that best describes what you are doing:</span></span>

| <span data-ttu-id="89e45-110">您要如何登入？</span><span class="sxs-lookup"><span data-stu-id="89e45-110">How do you sign in?</span></span> | 
| --- |
| [<span data-ttu-id="89e45-111">透過電話撥打我的行動或辦公室電話</span><span class="sxs-lookup"><span data-stu-id="89e45-111">With a phone call to my mobile or office phone</span></span>](#signing-in-with-a-phone-call) |
| [<span data-ttu-id="89e45-112">傳送簡訊到我的行動電話號碼</span><span class="sxs-lookup"><span data-stu-id="89e45-112">With a text to my mobile phone</span></span>](#signing-in-with-a-text-message)
| [<span data-ttu-id="89e45-113">從 Microsoft 驗證器應用程式使用通知</span><span class="sxs-lookup"><span data-stu-id="89e45-113">With notifications from the Microsoft Authenticator app</span></span>](#signing-in-with-the-microsoft-authenticator-app-using-notification) |
| [<span data-ttu-id="89e45-114">從 Microsoft 驗證器應用程式使用驗證碼</span><span class="sxs-lookup"><span data-stu-id="89e45-114">With verification codes from the Microsoft Authenticator app</span></span>](#signing-in-with-the-microsoft-authenticator-app-using-verification-code) |
| [<span data-ttu-id="89e45-115">使用替代方法，因為現在無法使用我慣用的方法</span><span class="sxs-lookup"><span data-stu-id="89e45-115">With an alternate method, because I can't use my preferred method right now</span></span>](#signing-in-with-an-alternate-method) |

## <a name="signing-in-with-a-phone-call"></a><span data-ttu-id="89e45-116">透過撥打電話來登入</span><span class="sxs-lookup"><span data-stu-id="89e45-116">Signing in with a phone call</span></span>
<span data-ttu-id="89e45-117">下列資訊將說明透過撥打您的行動或辦公室電話來進行雙步驟驗證體驗。</span><span class="sxs-lookup"><span data-stu-id="89e45-117">The following information describes the two-step verification experience with a call to your mobile or office phone.</span></span>

1. <span data-ttu-id="89e45-118">使用您的使用者名稱和密碼登入應用程式或服務，例如 Office 365。</span><span class="sxs-lookup"><span data-stu-id="89e45-118">Sign in to an application or service such as Office 365 using your username and password.</span></span>  
2. <span data-ttu-id="89e45-119">Microsoft 打電話給您。</span><span class="sxs-lookup"><span data-stu-id="89e45-119">Microsoft calls you.</span></span>  
3. <span data-ttu-id="89e45-120">請接聽電話並按 # 鍵。</span><span class="sxs-lookup"><span data-stu-id="89e45-120">Answer the phone and hit the # key.</span></span>  

## <a name="signing-in-with-a-text-message"></a><span data-ttu-id="89e45-121">透過簡訊登入</span><span class="sxs-lookup"><span data-stu-id="89e45-121">Signing in with a text message</span></span>
<span data-ttu-id="89e45-122">下列資訊將說明透過傳送簡訊到您的行動電話來進行雙步驟驗證體驗：</span><span class="sxs-lookup"><span data-stu-id="89e45-122">The following information describes the two-step verification experience with a text message to your mobile phone:</span></span>

1. <span data-ttu-id="89e45-123">使用您的使用者名稱和密碼登入應用程式或服務，例如 Office 365。</span><span class="sxs-lookup"><span data-stu-id="89e45-123">Sign in to an application or service such as Office 365 using your username and password.</span></span> 
2. <span data-ttu-id="89e45-124">Microsoft 會傳送包含數字代碼的簡訊給您。</span><span class="sxs-lookup"><span data-stu-id="89e45-124">Microsoft sends you a text message that contains a number code.</span></span> 
3. <span data-ttu-id="89e45-125">請在登入頁面上提供的方塊中輸入此代碼。</span><span class="sxs-lookup"><span data-stu-id="89e45-125">Enter the code in the box provided on the sign-in page.</span></span> 

## <a name="signing-in-with-the-microsoft-authenticator-app"></a><span data-ttu-id="89e45-126">使用 Microsoft 驗證器應用程式登入</span><span class="sxs-lookup"><span data-stu-id="89e45-126">Signing in with the Microsoft Authenticator app</span></span> 
<span data-ttu-id="89e45-127">下列資訊將說明使用 Microsoft Authenticator 應用程式進行雙步驟驗證的體驗。</span><span class="sxs-lookup"><span data-stu-id="89e45-127">The following information describes the experience of using the Microsoft Authenticator app for two-step verifications.</span></span> <span data-ttu-id="89e45-128">應用程式有兩種不同的使用方式。</span><span class="sxs-lookup"><span data-stu-id="89e45-128">There are two different ways to use the app.</span></span> <span data-ttu-id="89e45-129">您可以在裝置上接收推送通知，或是開啟應用程式以取得驗證碼。</span><span class="sxs-lookup"><span data-stu-id="89e45-129">You can receive push notifications on your device, or you can open the app to get a verification code.</span></span>

### <a name="to-sign-in-with-a-notification-from-the-microsoft-authenticator-app"></a><span data-ttu-id="89e45-130">從 Microsoft 驗證器應用程式使用通知登入</span><span class="sxs-lookup"><span data-stu-id="89e45-130">To sign in with a notification from the Microsoft Authenticator app</span></span>
1. <span data-ttu-id="89e45-131">使用您的使用者名稱和密碼登入應用程式或服務，例如 Office 365。</span><span class="sxs-lookup"><span data-stu-id="89e45-131">Sign in to an application or service such as Office 365 using your username and password.</span></span>
2. <span data-ttu-id="89e45-132">Microsoft 會將通知傳送到您裝置上的 Microsoft 驗證器應用程式。</span><span class="sxs-lookup"><span data-stu-id="89e45-132">Microsoft sends a notification to the Microsoft Authenticator app on your device.</span></span>

  ![Microsoft 傳送通知](./media/multi-factor-authentication-end-user-signin/notify.png)

3. <span data-ttu-id="89e45-134">在電話上開啟通知，然後選取 [驗證] 鍵。</span><span class="sxs-lookup"><span data-stu-id="89e45-134">Open the notification on your phone and select the **Verify** key.</span></span> <span data-ttu-id="89e45-135">如果貴公司要求 PIN，在此處輸入。</span><span class="sxs-lookup"><span data-stu-id="89e45-135">If your company requires a PIN, enter it here.</span></span>
4. <span data-ttu-id="89e45-136">您現在應已登入。</span><span class="sxs-lookup"><span data-stu-id="89e45-136">You should now be signed in.</span></span>

### <a name="to-sign-in-using-a-verification-code-with-the-microsoft-authenticator-app"></a><span data-ttu-id="89e45-137">使用驗證碼登入 Microsoft 驗證器應用程式</span><span class="sxs-lookup"><span data-stu-id="89e45-137">To sign in using a verification code with the Microsoft Authenticator app</span></span>

<span data-ttu-id="89e45-138">如果您使用 Microsoft Authenticator 應用程式取得驗證碼，則當您開啟應用程式時，會在您的帳戶名稱下面看到一個數字。</span><span class="sxs-lookup"><span data-stu-id="89e45-138">If you use the Microsoft Authenticator app to get verification codes, then when you open the app you see a number under your account name.</span></span> <span data-ttu-id="89e45-139">這個數字每 30 秒會變更一次，所以您不會使用相同的數字兩次。</span><span class="sxs-lookup"><span data-stu-id="89e45-139">This number changes every 30 seconds so that you don't use the same number twice.</span></span> <span data-ttu-id="89e45-140">當系統要求您輸入驗證碼時，開啟應用程式並使用當下所顯示的任何數字。</span><span class="sxs-lookup"><span data-stu-id="89e45-140">When you're asked for a verification code, open the app and use whatever number is currently displayed.</span></span> 

1. <span data-ttu-id="89e45-141">使用您的使用者名稱和密碼登入應用程式或服務，例如 Office 365。</span><span class="sxs-lookup"><span data-stu-id="89e45-141">Sign in to an application or service such as Office 365 using your username and password.</span></span>
2. <span data-ttu-id="89e45-142">Microsoft 提示您輸入驗證碼。</span><span class="sxs-lookup"><span data-stu-id="89e45-142">Microsoft prompts you for a verification code.</span></span>

  ![輸入驗證碼](./media/multi-factor-authentication-end-user-signin/verify3.png)

3. <span data-ttu-id="89e45-144">在電話上開啟 Microsoft 驗證器應用程式，並在登入的方塊中輸入驗證碼。</span><span class="sxs-lookup"><span data-stu-id="89e45-144">Open the Microsoft Authenticator app on your phone and enter the code in the box where you are signing in.</span></span>

## <a name="signing-in-with-an-alternate-method"></a><span data-ttu-id="89e45-145">使用替代方法登入</span><span class="sxs-lookup"><span data-stu-id="89e45-145">Signing in with an alternate method</span></span>
<span data-ttu-id="89e45-146">有時候您設定做為慣用驗證方法的電話或裝置不在手邊。</span><span class="sxs-lookup"><span data-stu-id="89e45-146">Sometimes you don't have the phone or device that you set up as your preferred verification method.</span></span> <span data-ttu-id="89e45-147">這種情況就是為什麼我們建議您為帳戶設定備份方法。</span><span class="sxs-lookup"><span data-stu-id="89e45-147">This situation is why we recommend that you set up backup methods for your account.</span></span> <span data-ttu-id="89e45-148">下一節示範當主要方法無法使用時，如何使用替代方法進行登入。</span><span class="sxs-lookup"><span data-stu-id="89e45-148">The following section shows you how to sign in with an alternate method when your primary method may not be available.</span></span>

1. <span data-ttu-id="89e45-149">使用您的使用者名稱和密碼登入應用程式或服務，例如 Office 365。</span><span class="sxs-lookup"><span data-stu-id="89e45-149">Sign in to an application or service such as Office 365 using your username and password.</span></span>
2. <span data-ttu-id="89e45-150">選取 [使用不同的驗證選項]。</span><span class="sxs-lookup"><span data-stu-id="89e45-150">Select **Use a different verification option**.</span></span> <span data-ttu-id="89e45-151">根據您已設定的驗證選項數量而定，您會看到不同的驗證選項。</span><span class="sxs-lookup"><span data-stu-id="89e45-151">You see different verification options based on how many you have setup.</span></span>
3. <span data-ttu-id="89e45-152">選擇替代方法並且登入。</span><span class="sxs-lookup"><span data-stu-id="89e45-152">Choose an alternate method and sign in.</span></span>

  ![使用替代方法](./media/multi-factor-authentication-end-user-signin/alt.png)

## <a name="next-steps"></a><span data-ttu-id="89e45-154">後續步驟</span><span class="sxs-lookup"><span data-stu-id="89e45-154">Next steps</span></span>

<span data-ttu-id="89e45-155">如果您碰到雙步驟驗證登入的問題，可從[使用 Azure Multi-Factor Authentication 時碰到困難](multi-factor-authentication-end-user-troubleshoot.md)獲得詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="89e45-155">If you have problems signing in with two-step verification, get more information at [Having trouble with Azure Multi-Factor Authentication](multi-factor-authentication-end-user-troubleshoot.md).</span></span>

<span data-ttu-id="89e45-156">了解如何[管理雙步驟驗證設定](multi-factor-authentication-end-user-manage-settings.md)。</span><span class="sxs-lookup"><span data-stu-id="89e45-156">Learn how to [Manage your two-step verification settings](multi-factor-authentication-end-user-manage-settings.md).</span></span>

<span data-ttu-id="89e45-157">了解如何[開始使用 Microsoft 驗證器應用程式](microsoft-authenticator-app-how-to.md)，如此一來，因此您可以使用通知登入，而不是經由文字訊息和來電。</span><span class="sxs-lookup"><span data-stu-id="89e45-157">Find out how to [Get started with the Microsoft Authenticator app](microsoft-authenticator-app-how-to.md) so that you can use notifications to sign in, instead of texts and phone calls.</span></span> 