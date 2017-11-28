---
title: "aaaAzure MFA 登入具有雙步驟驗證 |Microsoft 文件"
description: "此頁面將提供您指引 toogo toosee hello 各種登入方法可使用 Azure MFA 的位置。"
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
ms.openlocfilehash: fcd5eb5e8426eda537db9e099bf247bde29c195b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="hello-sign-in-experience-with-azure-multi-factor-authentication"></a><span data-ttu-id="4df6f-104">hello 登入體驗與 Azure Multi-factor Authentication</span><span class="sxs-lookup"><span data-stu-id="4df6f-104">hello sign-in experience with Azure Multi-Factor Authentication</span></span>
> [!NOTE]
> <span data-ttu-id="4df6f-105">hello 本文的目的是 toowalk 透過典型的登入體驗。</span><span class="sxs-lookup"><span data-stu-id="4df6f-105">hello purpose of this article is toowalk through a typical sign-in experience.</span></span> <span data-ttu-id="4df6f-106">登入，或 tootroubleshoot 問題的說明，請參閱[遇到 Azure Multi-factor Authentication](multi-factor-authentication-end-user-troubleshoot.md)。</span><span class="sxs-lookup"><span data-stu-id="4df6f-106">For help with signing in, or tootroubleshoot problems, see [Having trouble with Azure Multi-Factor Authentication](multi-factor-authentication-end-user-troubleshoot.md).</span></span>

## <a name="what-will-your-sign-in-experience-be"></a><span data-ttu-id="4df6f-107">您的登入體驗將會如何？</span><span class="sxs-lookup"><span data-stu-id="4df6f-107">What will your sign-in experience be?</span></span>
<span data-ttu-id="4df6f-108">根據您選擇的 toouse 做為您的第二個因素與您登入體驗： 電話、 驗證應用程式或文字。</span><span class="sxs-lookup"><span data-stu-id="4df6f-108">Your sign-in experience differs depending on what you choose toouse as your second factor: a phone call, an authentication app, or texts.</span></span> <span data-ttu-id="4df6f-109">選擇最能描述您進行的 hello 選項：</span><span class="sxs-lookup"><span data-stu-id="4df6f-109">Choose hello option that best describes what you are doing:</span></span>

| <span data-ttu-id="4df6f-110">您要如何登入？</span><span class="sxs-lookup"><span data-stu-id="4df6f-110">How do you sign in?</span></span> | 
| --- |
| [<span data-ttu-id="4df6f-111">使用電話 toomy 行動電話或辦公室電話</span><span class="sxs-lookup"><span data-stu-id="4df6f-111">With a phone call toomy mobile or office phone</span></span>](#signing-in-with-a-phone-call) |
| [<span data-ttu-id="4df6f-112">與文字 toomy 行動電話</span><span class="sxs-lookup"><span data-stu-id="4df6f-112">With a text toomy mobile phone</span></span>](#signing-in-with-a-text-message)
| [<span data-ttu-id="4df6f-113">來自 hello Microsoft 驗證器應用程式通知</span><span class="sxs-lookup"><span data-stu-id="4df6f-113">With notifications from hello Microsoft Authenticator app</span></span>](#signing-in-with-the-microsoft-authenticator-app-using-notification) |
| [<span data-ttu-id="4df6f-114">與從 hello Microsoft 驗證器應用程式的驗證碼</span><span class="sxs-lookup"><span data-stu-id="4df6f-114">With verification codes from hello Microsoft Authenticator app</span></span>](#signing-in-with-the-microsoft-authenticator-app-using-verification-code) |
| [<span data-ttu-id="4df6f-115">使用替代方法，因為現在無法使用我慣用的方法</span><span class="sxs-lookup"><span data-stu-id="4df6f-115">With an alternate method, because I can't use my preferred method right now</span></span>](#signing-in-with-an-alternate-method) |

## <a name="signing-in-with-a-phone-call"></a><span data-ttu-id="4df6f-116">透過撥打電話來登入</span><span class="sxs-lookup"><span data-stu-id="4df6f-116">Signing in with a phone call</span></span>
<span data-ttu-id="4df6f-117">hello 下列資訊描述 hello 雙步驟驗證經驗與呼叫 tooyour 行動或辦公室電話。</span><span class="sxs-lookup"><span data-stu-id="4df6f-117">hello following information describes hello two-step verification experience with a call tooyour mobile or office phone.</span></span>

1. <span data-ttu-id="4df6f-118">登入 tooan 應用程式或服務，例如 Office 365 使用您的使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="4df6f-118">Sign in tooan application or service such as Office 365 using your username and password.</span></span>  
2. <span data-ttu-id="4df6f-119">Microsoft 打電話給您。</span><span class="sxs-lookup"><span data-stu-id="4df6f-119">Microsoft calls you.</span></span>  
3. <span data-ttu-id="4df6f-120">接聽 hello 電話並按 hello # 鍵。</span><span class="sxs-lookup"><span data-stu-id="4df6f-120">Answer hello phone and hit hello # key.</span></span>  

## <a name="signing-in-with-a-text-message"></a><span data-ttu-id="4df6f-121">透過簡訊登入</span><span class="sxs-lookup"><span data-stu-id="4df6f-121">Signing in with a text message</span></span>
<span data-ttu-id="4df6f-122">hello 下列資訊描述 hello 雙步驟驗證經驗，只要使用文字訊息 tooyour 行動電話：</span><span class="sxs-lookup"><span data-stu-id="4df6f-122">hello following information describes hello two-step verification experience with a text message tooyour mobile phone:</span></span>

1. <span data-ttu-id="4df6f-123">登入 tooan 應用程式或服務，例如 Office 365 使用您的使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="4df6f-123">Sign in tooan application or service such as Office 365 using your username and password.</span></span> 
2. <span data-ttu-id="4df6f-124">Microsoft 會傳送包含數字代碼的簡訊給您。</span><span class="sxs-lookup"><span data-stu-id="4df6f-124">Microsoft sends you a text message that contains a number code.</span></span> 
3. <span data-ttu-id="4df6f-125">Hello 登入頁面上提供的 hello 方塊中輸入 hello 程式碼。</span><span class="sxs-lookup"><span data-stu-id="4df6f-125">Enter hello code in hello box provided on hello sign-in page.</span></span> 

## <a name="signing-in-with-hello-microsoft-authenticator-app"></a><span data-ttu-id="4df6f-126">登入 hello Microsoft 驗證器應用程式</span><span class="sxs-lookup"><span data-stu-id="4df6f-126">Signing in with hello Microsoft Authenticator app</span></span> 
<span data-ttu-id="4df6f-127">hello 下列資訊描述 hello 體驗 hello Microsoft 驗證器應用程式使用的兩步驟驗證。</span><span class="sxs-lookup"><span data-stu-id="4df6f-127">hello following information describes hello experience of using hello Microsoft Authenticator app for two-step verifications.</span></span> <span data-ttu-id="4df6f-128">有兩個不同的方式 toouse hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4df6f-128">There are two different ways toouse hello app.</span></span> <span data-ttu-id="4df6f-129">您可以在您的裝置上接收推播通知，或者您可以開啟 hello 應用程式 tooget 驗證碼。</span><span class="sxs-lookup"><span data-stu-id="4df6f-129">You can receive push notifications on your device, or you can open hello app tooget a verification code.</span></span>

### <a name="toosign-in-with-a-notification-from-hello-microsoft-authenticator-app"></a><span data-ttu-id="4df6f-130">toosign 入是來自 hello Microsoft 驗證器應用程式通知</span><span class="sxs-lookup"><span data-stu-id="4df6f-130">toosign in with a notification from hello Microsoft Authenticator app</span></span>
1. <span data-ttu-id="4df6f-131">登入 tooan 應用程式或服務，例如 Office 365 使用您的使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="4df6f-131">Sign in tooan application or service such as Office 365 using your username and password.</span></span>
2. <span data-ttu-id="4df6f-132">Microsoft 會傳送通知 toohello Microsoft Authenticator 應用程式在裝置上。</span><span class="sxs-lookup"><span data-stu-id="4df6f-132">Microsoft sends a notification toohello Microsoft Authenticator app on your device.</span></span>

  ![Microsoft 傳送通知](./media/multi-factor-authentication-end-user-signin/notify.png)

3. <span data-ttu-id="4df6f-134">在您的電話和選取 hello 開啟 hello 通知**確認**索引鍵。</span><span class="sxs-lookup"><span data-stu-id="4df6f-134">Open hello notification on your phone and select hello **Verify** key.</span></span> <span data-ttu-id="4df6f-135">如果貴公司要求 PIN，在此處輸入。</span><span class="sxs-lookup"><span data-stu-id="4df6f-135">If your company requires a PIN, enter it here.</span></span>
4. <span data-ttu-id="4df6f-136">您現在應已登入。</span><span class="sxs-lookup"><span data-stu-id="4df6f-136">You should now be signed in.</span></span>

### <a name="toosign-in-using-a-verification-code-with-hello-microsoft-authenticator-app"></a><span data-ttu-id="4df6f-137">toosign 在 hello Microsoft Authenticator 應用程式中使用驗證碼</span><span class="sxs-lookup"><span data-stu-id="4df6f-137">toosign in using a verification code with hello Microsoft Authenticator app</span></span>

<span data-ttu-id="4df6f-138">如果您使用 hello Microsoft 驗證器應用程式 tooget 驗證碼，然後當您開啟 hello 應用程式時您看到一些在您的帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="4df6f-138">If you use hello Microsoft Authenticator app tooget verification codes, then when you open hello app you see a number under your account name.</span></span> <span data-ttu-id="4df6f-139">這個數字變更每隔 30 秒，讓您不使用的 hello 兩次相同數字。</span><span class="sxs-lookup"><span data-stu-id="4df6f-139">This number changes every 30 seconds so that you don't use hello same number twice.</span></span> <span data-ttu-id="4df6f-140">當詢問驗證程式碼時，開啟 hello 應用程式，並使用目前顯示的任何數字。</span><span class="sxs-lookup"><span data-stu-id="4df6f-140">When you're asked for a verification code, open hello app and use whatever number is currently displayed.</span></span> 

1. <span data-ttu-id="4df6f-141">登入 tooan 應用程式或服務，例如 Office 365 使用您的使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="4df6f-141">Sign in tooan application or service such as Office 365 using your username and password.</span></span>
2. <span data-ttu-id="4df6f-142">Microsoft 提示您輸入驗證碼。</span><span class="sxs-lookup"><span data-stu-id="4df6f-142">Microsoft prompts you for a verification code.</span></span>

  ![輸入驗證碼](./media/multi-factor-authentication-end-user-signin/verify3.png)

3. <span data-ttu-id="4df6f-144">開啟 hello 手機上的 Microsoft 驗證器應用程式，並在您要登入的 hello 方塊中輸入 hello 程式碼。</span><span class="sxs-lookup"><span data-stu-id="4df6f-144">Open hello Microsoft Authenticator app on your phone and enter hello code in hello box where you are signing in.</span></span>

## <a name="signing-in-with-an-alternate-method"></a><span data-ttu-id="4df6f-145">使用替代方法登入</span><span class="sxs-lookup"><span data-stu-id="4df6f-145">Signing in with an alternate method</span></span>
<span data-ttu-id="4df6f-146">有時候，您不需要 hello 電話或裝置，您將設定為慣用的驗證方法。</span><span class="sxs-lookup"><span data-stu-id="4df6f-146">Sometimes you don't have hello phone or device that you set up as your preferred verification method.</span></span> <span data-ttu-id="4df6f-147">這種情況就是為什麼我們建議您為帳戶設定備份方法。</span><span class="sxs-lookup"><span data-stu-id="4df6f-147">This situation is why we recommend that you set up backup methods for your account.</span></span> <span data-ttu-id="4df6f-148">hello 下節將說明如何 toosign 使用替代方法時可能無法使用主要方法。</span><span class="sxs-lookup"><span data-stu-id="4df6f-148">hello following section shows you how toosign in with an alternate method when your primary method may not be available.</span></span>

1. <span data-ttu-id="4df6f-149">登入 tooan 應用程式或服務，例如 Office 365 使用您的使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="4df6f-149">Sign in tooan application or service such as Office 365 using your username and password.</span></span>
2. <span data-ttu-id="4df6f-150">選取 [使用不同的驗證選項]。</span><span class="sxs-lookup"><span data-stu-id="4df6f-150">Select **Use a different verification option**.</span></span> <span data-ttu-id="4df6f-151">根據您已設定的驗證選項數量而定，您會看到不同的驗證選項。</span><span class="sxs-lookup"><span data-stu-id="4df6f-151">You see different verification options based on how many you have setup.</span></span>
3. <span data-ttu-id="4df6f-152">選擇替代方法並且登入。</span><span class="sxs-lookup"><span data-stu-id="4df6f-152">Choose an alternate method and sign in.</span></span>

  ![使用替代方法](./media/multi-factor-authentication-end-user-signin/alt.png)

## <a name="next-steps"></a><span data-ttu-id="4df6f-154">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4df6f-154">Next steps</span></span>

<span data-ttu-id="4df6f-155">如果您碰到雙步驟驗證登入的問題，可從[使用 Azure Multi-Factor Authentication 時碰到困難](multi-factor-authentication-end-user-troubleshoot.md)獲得詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="4df6f-155">If you have problems signing in with two-step verification, get more information at [Having trouble with Azure Multi-Factor Authentication](multi-factor-authentication-end-user-troubleshoot.md).</span></span>

<span data-ttu-id="4df6f-156">了解如何太[管理兩步驟驗證設定](multi-factor-authentication-end-user-manage-settings.md)。</span><span class="sxs-lookup"><span data-stu-id="4df6f-156">Learn how too[Manage your two-step verification settings](multi-factor-authentication-end-user-manage-settings.md).</span></span>

<span data-ttu-id="4df6f-157">了解如何太[hello Microsoft 驗證器應用程式使用者入門](microsoft-authenticator-app-how-to.md)，讓您可以使用通知 toosign 中，而不是文字和撥打電話。</span><span class="sxs-lookup"><span data-stu-id="4df6f-157">Find out how too[Get started with hello Microsoft Authenticator app](microsoft-authenticator-app-how-to.md) so that you can use notifications toosign in, instead of texts and phone calls.</span></span> 
