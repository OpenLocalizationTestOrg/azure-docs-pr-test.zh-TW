---
title: "Azure AD：SSPR 註冊 | Microsoft Docs"
description: "註冊 Azure AD 自助式密碼重設的驗證資料"
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
ms.date: 08/07/2017
ms.author: joflore
ms.custom: end-user
ms.openlocfilehash: b701172c2345313e236a037f5aa16939cfaac440
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="register-for-self-service-password-reset"></a><span data-ttu-id="5adde-103">註冊自助式密碼重設</span><span class="sxs-lookup"><span data-stu-id="5adde-103">Register for self-service password reset</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5adde-104">**您來到此處是因為有登入問題嗎？**</span><span class="sxs-lookup"><span data-stu-id="5adde-104">**Are you here because you're having problems signing in?**</span></span> <span data-ttu-id="5adde-105">若是如此， [以下是如何變更和重設密碼的說明](active-directory-passwords-update-your-own-password.md)。</span><span class="sxs-lookup"><span data-stu-id="5adde-105">If so, [here's how you can change and reset your own password](active-directory-passwords-update-your-own-password.md).</span></span>

<span data-ttu-id="5adde-106">身為一般使用者，您可以重設密碼或解除鎖定您的帳戶，而不需使用自助式密碼重設 (SSPR) 與人員對話。</span><span class="sxs-lookup"><span data-stu-id="5adde-106">As an end user, you can reset your password or unlock your account without having to speak to a person using self-service password reset (SSPR).</span></span> <span data-ttu-id="5adde-107">在您可以使用這項功能之前，您必須註冊驗證方法，或確認您系統管理員已填入的預先定義驗證方法。</span><span class="sxs-lookup"><span data-stu-id="5adde-107">Before you can use this functionality, you have to register authentication methods or confirm the predefined authentication methods your administrator has populated.</span></span>

## <a name="register-or-confirm-authentication-data-with-sspr"></a><span data-ttu-id="5adde-108">使用 SSPR 註冊或確認驗證資料</span><span class="sxs-lookup"><span data-stu-id="5adde-108">Register or confirm authentication data with SSPR</span></span>

1. <span data-ttu-id="5adde-109">開啟您裝置的 web 瀏覽器並移至[密碼重設註冊頁面](http://aka.ms/ssprsetup)</span><span class="sxs-lookup"><span data-stu-id="5adde-109">Open the web browser on your device and go to the [password reset registration page](http://aka.ms/ssprsetup)</span></span>
2. <span data-ttu-id="5adde-110">輸入您的使用者名稱和您系統管理員所提供的密碼</span><span class="sxs-lookup"><span data-stu-id="5adde-110">Enter your username and password provided by your administrator</span></span>
3. <span data-ttu-id="5adde-111">視您的 IT 人員如何如何設定而定，下列一或多個選項可供您設定及驗證。</span><span class="sxs-lookup"><span data-stu-id="5adde-111">Depending on how your IT staff have configured things, one or more of the following options are available for you to configure and verify.</span></span> <span data-ttu-id="5adde-112">如果您的系統管理員有權限使用資訊，他們可能會為您填入部分資訊。</span><span class="sxs-lookup"><span data-stu-id="5adde-112">Your administrator may populate some of this for you if they have your permission to use the information.</span></span>
    * <span data-ttu-id="5adde-113">只有您的系統管理員可以設定辦公室電話</span><span class="sxs-lookup"><span data-stu-id="5adde-113">Office phone is only able to be set by your administrator</span></span>
    * <span data-ttu-id="5adde-114">[驗證電話] 應設定為另一個您可存取的電話號碼，如可以接收簡訊或電話的行動電話。</span><span class="sxs-lookup"><span data-stu-id="5adde-114">Authentication Phone should be set to another phone number you would have access to like a cell phone that can receive a text or call.</span></span>
    * <span data-ttu-id="5adde-115">[驗證電子郵件] 應設定為您可以存取而不需要重設密碼的替代電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="5adde-115">Authentication Email should be set to an alternate email address that you can access without the password you need to reset.</span></span>
    * <span data-ttu-id="5adde-116">[安全性問題] 可提供一份您系統管理員已核准的問題清單以供您回答。</span><span class="sxs-lookup"><span data-stu-id="5adde-116">Security Questions gives you a list of questions your administrator has approved for you to answer.</span></span> <span data-ttu-id="5adde-117">您不可以使用相同的問題或回答一次以上。</span><span class="sxs-lookup"><span data-stu-id="5adde-117">You may not use the same question or answer more than once.</span></span>
4. <span data-ttu-id="5adde-118">提供並確認您的系統管理員所需的資訊。</span><span class="sxs-lookup"><span data-stu-id="5adde-118">Provide and verify the information required by your administrator.</span></span> <span data-ttu-id="5adde-119">如果可使用多個選項，我們建議您註冊多個方法，以當另一種方法無法使用時提供彈性 (範例︰出差而無法存取您的辦公室電話)</span><span class="sxs-lookup"><span data-stu-id="5adde-119">If more than one option is available, we suggest that you register multiple methods to provide flexibility when another method is unavailable (Example: Traveling and unable to access your office phone)</span></span>

    <span data-ttu-id="5adde-120">![註冊驗證方法，並按一下 [完成]][Register]</span><span class="sxs-lookup"><span data-stu-id="5adde-120">![Register authentication methods and click finish][Register]</span></span>

5. <span data-ttu-id="5adde-121">當完成步驟 4 時，選擇 [完成]現在您便可以在未來需要時使用自助式密碼重設。</span><span class="sxs-lookup"><span data-stu-id="5adde-121">When done with step 4 choose **finish** and you will now be able to use self-service password reset when you need to in the future.</span></span>

<span data-ttu-id="5adde-122">如果您在驗證電話或驗證電子郵件中輸入資料，在全域目錄中會看不見。</span><span class="sxs-lookup"><span data-stu-id="5adde-122">If you enter data in the Authentication Phone or Authentication Email, it is not visible in the global directory.</span></span> <span data-ttu-id="5adde-123">您和您的系統管理員是唯一可以看到此資料的人員。</span><span class="sxs-lookup"><span data-stu-id="5adde-123">The only people who can see this data are you and your administrators.</span></span> <span data-ttu-id="5adde-124">只有您可以查看您安全性問題的答案。</span><span class="sxs-lookup"><span data-stu-id="5adde-124">Only you can see the answers to your Security Questions.</span></span>

<span data-ttu-id="5adde-125">系統管理員在一段時間後可能會要求您確認驗證方法，確定您仍有適當的已註冊方法。</span><span class="sxs-lookup"><span data-stu-id="5adde-125">Administrators may require you to confirm your authentication methods after a period of time to make sure you still have the appropriate methods registered.</span></span>

## <a name="common-problems-and-their-solutions"></a><span data-ttu-id="5adde-126">常見問題及其解決方案</span><span class="sxs-lookup"><span data-stu-id="5adde-126">Common problems and their solutions</span></span>

 <span data-ttu-id="5adde-127">以下提供一些常見的錯誤案例及其解決方案：</span><span class="sxs-lookup"><span data-stu-id="5adde-127">Here are some common error cases and their solutions:</span></span>

| <span data-ttu-id="5adde-128">錯誤案例</span><span class="sxs-lookup"><span data-stu-id="5adde-128">Error Case</span></span>| <span data-ttu-id="5adde-129">您看到什麼錯誤訊息？</span><span class="sxs-lookup"><span data-stu-id="5adde-129">What error do you see?</span></span>| <span data-ttu-id="5adde-130">方案</span><span class="sxs-lookup"><span data-stu-id="5adde-130">Solution</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5adde-131">在輸入我的使用者 ID 後，出現了「請連絡您的系統管理員」頁面</span><span class="sxs-lookup"><span data-stu-id="5adde-131">I get a "please contact your administrator" page after entering my user ID</span></span> | <span data-ttu-id="5adde-132">請連絡您的系統管理員</span><span class="sxs-lookup"><span data-stu-id="5adde-132">Please contact your administrator</span></span> <br> <br> <span data-ttu-id="5adde-133">我們偵測到您的使用者帳戶密碼未受到 Microsoft 管理。</span><span class="sxs-lookup"><span data-stu-id="5adde-133">We've detected that your user account password is not managed by Microsoft.</span></span> <span data-ttu-id="5adde-134">因此，我們無法自動重設您的密碼。</span><span class="sxs-lookup"><span data-stu-id="5adde-134">As a result, we are unable to automatically reset your password.</span></span> <br> <br> <span data-ttu-id="5adde-135">您必須連絡 IT 人員以尋求進一步的協助。</span><span class="sxs-lookup"><span data-stu-id="5adde-135">You need to contact your IT staff for any further assistance.</span></span> | <span data-ttu-id="5adde-136">您之所以看到此訊息，是因為 IT 人員在內部部署環境中管理您的密碼，而不允許您從 [無法存取您的帳戶] 連結重設您的密碼。</span><span class="sxs-lookup"><span data-stu-id="5adde-136">You are seeing this message because your IT staff manages your password in your on-premises environment and does not allow you to reset your password from the Can't access your account link.</span></span> <br> <br> <span data-ttu-id="5adde-137">若要重設密碼，請直接向 IT 人員尋求協助，讓他們了解您想要重設密碼，而為您啟用這項功能。</span><span class="sxs-lookup"><span data-stu-id="5adde-137">To reset your password,  contact your IT staff directly for help, and let them know you want to reset your password so they can enable this feature for you.</span></span>|
| <span data-ttu-id="5adde-138">在輸入我的使用者 ID 後，出現了「您的帳戶未啟用密碼重設」錯誤</span><span class="sxs-lookup"><span data-stu-id="5adde-138">I get a "your account is not enabled for password reset" error after entering my user ID</span></span> | <span data-ttu-id="5adde-139">您的帳戶未啟用密碼重設功能</span><span class="sxs-lookup"><span data-stu-id="5adde-139">Your account is not enabled for password reset</span></span> <br> <br> <span data-ttu-id="5adde-140">很抱歉，IT 人員還沒將您的帳戶設定用於此服務。</span><span class="sxs-lookup"><span data-stu-id="5adde-140">We're sorry, but your IT staff has not set up your account for use with this service.</span></span> <br> <br> <span data-ttu-id="5adde-141">如果您願意，我們可以連絡貴組織的系統管理員來為您重設密碼。</span><span class="sxs-lookup"><span data-stu-id="5adde-141">If you'd like, we can contact an administrator in your organization to reset your password for you.</span></span> | <span data-ttu-id="5adde-142">您之所以看到此訊息，是因為 IT 人員尚未針對您的組織啟用從 [無法存取您的帳戶] 連結重設密碼的功能，或尚未授權您使用該功能。</span><span class="sxs-lookup"><span data-stu-id="5adde-142">You are seeing this message because your IT staff has not enabled password reset for your organization from the Can't access your account link, or hasn't licensed you to use the feature.</span></span> <br> <br> <span data-ttu-id="5adde-143">若要重設密碼，請按一下 [連絡系統管理員] 連結以傳送電子郵件給公司的 IT 人員，讓他們了解您想要重設密碼，而為您啟用這項功能。</span><span class="sxs-lookup"><span data-stu-id="5adde-143">To reset your password, click the contact an administrator link to send an email to your company's IT staff, and let them know you want to reset your password so they can enable this feature for you.</span></span> |
| <span data-ttu-id="5adde-144">在輸入我的使用者 ID 後，出現了「我們無法驗證您的帳戶」錯誤</span><span class="sxs-lookup"><span data-stu-id="5adde-144">I get a "we could not verify your account" error after entering my user ID</span></span> | <span data-ttu-id="5adde-145">我們無法驗證您的帳戶</span><span class="sxs-lookup"><span data-stu-id="5adde-145">We could not verify your account</span></span> <br> <br> <span data-ttu-id="5adde-146">如果您願意，我們可以連絡貴組織的系統管理員來為您重設密碼。</span><span class="sxs-lookup"><span data-stu-id="5adde-146">If you'd like, we can contact an administrator in your organization to reset your password for you.</span></span> | <span data-ttu-id="5adde-147">您之所以看到此訊息，是因為您已啟用密碼重設，但並未註冊使用此服務。</span><span class="sxs-lookup"><span data-stu-id="5adde-147">You are seeing this message because you are enabled for password reset, but you have not registered to use the service.</span></span> <span data-ttu-id="5adde-148">若要註冊密碼重設，請在重新取得帳戶存取權後移至 http://aka.ms/ssprsetup。</span><span class="sxs-lookup"><span data-stu-id="5adde-148">To register for password reset, go to http://aka.ms/ssprsetup after you have regained access to your account.</span></span> <br> <br> <span data-ttu-id="5adde-149">若要重設密碼，請按一下 [連絡系統管理員] 連結，以傳送電子郵件給公司的 IT 人員。</span><span class="sxs-lookup"><span data-stu-id="5adde-149">To reset your password, click the contact an administrator link to send an email to your company's IT staff.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5adde-150">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5adde-150">Next Steps</span></span>

* [<span data-ttu-id="5adde-151">如何使用自助式密碼重設變更您的密碼</span><span class="sxs-lookup"><span data-stu-id="5adde-151">How to change your password using self-service password reset</span></span>](active-directory-passwords-update-your-own-password.md)
* [<span data-ttu-id="5adde-152">密碼重設註冊頁面</span><span class="sxs-lookup"><span data-stu-id="5adde-152">Password reset registration page</span></span>](http://aka.ms/ssprsetup)
* [<span data-ttu-id="5adde-153">密碼重設入口網站</span><span class="sxs-lookup"><span data-stu-id="5adde-153">Password reset portal</span></span>](https://passwordreset.microsoftonline.com/)
* [<span data-ttu-id="5adde-154">無法登入 Microsoft 帳戶</span><span class="sxs-lookup"><span data-stu-id="5adde-154">Can't sign in to your Microsoft account</span></span>](https://support.microsoft.com/help/12429/microsoft-account-sign-in-cant)

<span data-ttu-id="5adde-155">[Register]: ./media/active-directory-passwords-reset-register/register-2-methods.png "顯示已註冊方法及完成按鈕的密碼重設註冊頁面"</span><span class="sxs-lookup"><span data-stu-id="5adde-155">[Register]: ./media/active-directory-passwords-reset-register/register-2-methods.png "Password reset registration page showing registered methods and finish button"</span></span>

