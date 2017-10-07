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
ms.openlocfilehash: dfcd0106616218c84d23920b124bed5b202cdd6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="register-for-self-service-password-reset"></a><span data-ttu-id="e24b3-103">註冊自助式密碼重設</span><span class="sxs-lookup"><span data-stu-id="e24b3-103">Register for self-service password reset</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e24b3-104">**您來到此處是因為有登入問題嗎？**</span><span class="sxs-lookup"><span data-stu-id="e24b3-104">**Are you here because you're having problems signing in?**</span></span> <span data-ttu-id="e24b3-105">若是如此， [以下是如何變更和重設密碼的說明](active-directory-passwords-update-your-own-password.md)。</span><span class="sxs-lookup"><span data-stu-id="e24b3-105">If so, [here's how you can change and reset your own password](active-directory-passwords-update-your-own-password.md).</span></span>

<span data-ttu-id="e24b3-106">以一般使用者，您可以重設密碼或解除鎖定帳戶而不需要使用自助式密碼重設 (SSPR) toospeak tooa 人員。</span><span class="sxs-lookup"><span data-stu-id="e24b3-106">As an end user, you can reset your password or unlock your account without having toospeak tooa person using self-service password reset (SSPR).</span></span> <span data-ttu-id="e24b3-107">您可以使用這項功能之前，您尚未 tooregister 驗證方法，或確認已填入您的系統管理員的 hello 預先定義的驗證方法。</span><span class="sxs-lookup"><span data-stu-id="e24b3-107">Before you can use this functionality, you have tooregister authentication methods or confirm hello predefined authentication methods your administrator has populated.</span></span>

## <a name="register-or-confirm-authentication-data-with-sspr"></a><span data-ttu-id="e24b3-108">使用 SSPR 註冊或確認驗證資料</span><span class="sxs-lookup"><span data-stu-id="e24b3-108">Register or confirm authentication data with SSPR</span></span>

1. <span data-ttu-id="e24b3-109">在您的裝置，然後移至 toohello hello 開啟網頁瀏覽器[密碼重設註冊頁面](http://aka.ms/ssprsetup)</span><span class="sxs-lookup"><span data-stu-id="e24b3-109">Open hello web browser on your device and go toohello [password reset registration page](http://aka.ms/ssprsetup)</span></span>
2. <span data-ttu-id="e24b3-110">輸入您的使用者名稱和您系統管理員所提供的密碼</span><span class="sxs-lookup"><span data-stu-id="e24b3-110">Enter your username and password provided by your administrator</span></span>
3. <span data-ttu-id="e24b3-111">根據您的 IT 人員如何設定項目、 一個或多個 hello 下列選項可供您 tooconfigure，並確認。</span><span class="sxs-lookup"><span data-stu-id="e24b3-111">Depending on how your IT staff have configured things, one or more of hello following options are available for you tooconfigure and verify.</span></span> <span data-ttu-id="e24b3-112">您的系統管理員可能會填入這一點為您他們有權限 toouse hello 資訊。</span><span class="sxs-lookup"><span data-stu-id="e24b3-112">Your administrator may populate some of this for you if they have your permission toouse hello information.</span></span>
    * <span data-ttu-id="e24b3-113">辦公室電話是只能夠 toobe 管理員所設定</span><span class="sxs-lookup"><span data-stu-id="e24b3-113">Office phone is only able toobe set by your administrator</span></span>
    * <span data-ttu-id="e24b3-114">驗證電話應設定 tooanother，您必須存取 toolike 行動電話可以接收簡訊或電話的電話號碼。</span><span class="sxs-lookup"><span data-stu-id="e24b3-114">Authentication Phone should be set tooanother phone number you would have access toolike a cell phone that can receive a text or call.</span></span>
    * <span data-ttu-id="e24b3-115">驗證電子郵件應該設定 tooan 替代電子郵件地址，您可以存取 hello 密碼的情況下，您需要 tooreset。</span><span class="sxs-lookup"><span data-stu-id="e24b3-115">Authentication Email should be set tooan alternate email address that you can access without hello password you need tooreset.</span></span>
    * <span data-ttu-id="e24b3-116">安全性問題，可讓您的問題，您的系統管理員已核准您 tooanswer 的清單。</span><span class="sxs-lookup"><span data-stu-id="e24b3-116">Security Questions gives you a list of questions your administrator has approved for you tooanswer.</span></span> <span data-ttu-id="e24b3-117">您不可能使用的 hello 相同問題或回答一次以上。</span><span class="sxs-lookup"><span data-stu-id="e24b3-117">You may not use hello same question or answer more than once.</span></span>
4. <span data-ttu-id="e24b3-118">提供並確認您的系統管理員所需的 hello 資訊。</span><span class="sxs-lookup"><span data-stu-id="e24b3-118">Provide and verify hello information required by your administrator.</span></span> <span data-ttu-id="e24b3-119">如果使用多個選項，則我們建議您註冊多個方法 tooprovide 彈性，無法使用另一種方法時 (範例： 出差而無法 tooaccess 您的辦公室電話)</span><span class="sxs-lookup"><span data-stu-id="e24b3-119">If more than one option is available, we suggest that you register multiple methods tooprovide flexibility when another method is unavailable (Example: Traveling and unable tooaccess your office phone)</span></span>

    <span data-ttu-id="e24b3-120">![註冊驗證方法，並按一下 [完成]][Register]</span><span class="sxs-lookup"><span data-stu-id="e24b3-120">![Register authentication methods and click finish][Register]</span></span>

5. <span data-ttu-id="e24b3-121">當完成步驟 4 時選擇**完成**，而且您現在可以 toouse 自助式密碼重設時需要 tooin hello 未來。</span><span class="sxs-lookup"><span data-stu-id="e24b3-121">When done with step 4 choose **finish** and you will now be able toouse self-service password reset when you need tooin hello future.</span></span>

<span data-ttu-id="e24b3-122">如果您輸入 hello 驗證電話或驗證電子郵件中的資料，它是不可見 hello 全域目錄中。</span><span class="sxs-lookup"><span data-stu-id="e24b3-122">If you enter data in hello Authentication Phone or Authentication Email, it is not visible in hello global directory.</span></span> <span data-ttu-id="e24b3-123">hello 的人才可以看到此資料包括您和您的系統管理員。</span><span class="sxs-lookup"><span data-stu-id="e24b3-123">hello only people who can see this data are you and your administrators.</span></span> <span data-ttu-id="e24b3-124">只有您可以看到 hello 回答 tooyour 安全性問題。</span><span class="sxs-lookup"><span data-stu-id="e24b3-124">Only you can see hello answers tooyour Security Questions.</span></span>

<span data-ttu-id="e24b3-125">系統管理員可能需要您 tooconfirm 驗證方法在一段時間 toomake 確定仍有 hello 註冊適當的方法。</span><span class="sxs-lookup"><span data-stu-id="e24b3-125">Administrators may require you tooconfirm your authentication methods after a period of time toomake sure you still have hello appropriate methods registered.</span></span>

## <a name="common-problems-and-their-solutions"></a><span data-ttu-id="e24b3-126">常見問題及其解決方案</span><span class="sxs-lookup"><span data-stu-id="e24b3-126">Common problems and their solutions</span></span>

 <span data-ttu-id="e24b3-127">以下提供一些常見的錯誤案例及其解決方案：</span><span class="sxs-lookup"><span data-stu-id="e24b3-127">Here are some common error cases and their solutions:</span></span>

| <span data-ttu-id="e24b3-128">錯誤案例</span><span class="sxs-lookup"><span data-stu-id="e24b3-128">Error Case</span></span>| <span data-ttu-id="e24b3-129">您看到什麼錯誤訊息？</span><span class="sxs-lookup"><span data-stu-id="e24b3-129">What error do you see?</span></span>| <span data-ttu-id="e24b3-130">方案</span><span class="sxs-lookup"><span data-stu-id="e24b3-130">Solution</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e24b3-131">在輸入我的使用者 ID 後，出現了「請連絡您的系統管理員」頁面</span><span class="sxs-lookup"><span data-stu-id="e24b3-131">I get a "please contact your administrator" page after entering my user ID</span></span> | <span data-ttu-id="e24b3-132">請連絡您的系統管理員</span><span class="sxs-lookup"><span data-stu-id="e24b3-132">Please contact your administrator</span></span> <br> <br> <span data-ttu-id="e24b3-133">我們偵測到您的使用者帳戶密碼未受到 Microsoft 管理。</span><span class="sxs-lookup"><span data-stu-id="e24b3-133">We've detected that your user account password is not managed by Microsoft.</span></span> <span data-ttu-id="e24b3-134">如此一來，我們目前無法 tooautomatically 重設密碼。</span><span class="sxs-lookup"><span data-stu-id="e24b3-134">As a result, we are unable tooautomatically reset your password.</span></span> <br> <br> <span data-ttu-id="e24b3-135">您需要 toocontact 您的 IT 人員尋求進一步的協助。</span><span class="sxs-lookup"><span data-stu-id="e24b3-135">You need toocontact your IT staff for any further assistance.</span></span> | <span data-ttu-id="e24b3-136">您會看到此訊息，因為您的 IT 人員管理您的密碼在內部部署環境中並不允許您 tooreset 的密碼，無法存取您帳戶的連結。</span><span class="sxs-lookup"><span data-stu-id="e24b3-136">You are seeing this message because your IT staff manages your password in your on-premises environment and does not allow you tooreset your password from the Can't access your account link.</span></span> <br> <br> <span data-ttu-id="e24b3-137">tooreset 您的密碼，請連絡您的 IT 人員直接的說明，以及讓他們知道您想 tooreset 您的密碼，因此它們可以讓您啟用此功能。</span><span class="sxs-lookup"><span data-stu-id="e24b3-137">tooreset your password,  contact your IT staff directly for help, and let them know you want tooreset your password so they can enable this feature for you.</span></span>|
| <span data-ttu-id="e24b3-138">在輸入我的使用者 ID 後，出現了「您的帳戶未啟用密碼重設」錯誤</span><span class="sxs-lookup"><span data-stu-id="e24b3-138">I get a "your account is not enabled for password reset" error after entering my user ID</span></span> | <span data-ttu-id="e24b3-139">您的帳戶未啟用密碼重設功能</span><span class="sxs-lookup"><span data-stu-id="e24b3-139">Your account is not enabled for password reset</span></span> <br> <br> <span data-ttu-id="e24b3-140">很抱歉，IT 人員還沒將您的帳戶設定用於此服務。</span><span class="sxs-lookup"><span data-stu-id="e24b3-140">We're sorry, but your IT staff has not set up your account for use with this service.</span></span> <br> <br> <span data-ttu-id="e24b3-141">如果您想要的話，我們可以請連絡系統管理員可以在您的組織 tooreset 您的密碼。</span><span class="sxs-lookup"><span data-stu-id="e24b3-141">If you'd like, we can contact an administrator in your organization tooreset your password for you.</span></span> | <span data-ttu-id="e24b3-142">您會看到此訊息，因為您的 IT 人員尚未啟用密碼重設為從您的組織無法存取您帳戶的連結，或未授權您 toouse hello 功能。</span><span class="sxs-lookup"><span data-stu-id="e24b3-142">You are seeing this message because your IT staff has not enabled password reset for your organization from the Can't access your account link, or hasn't licensed you toouse hello feature.</span></span> <br> <br> <span data-ttu-id="e24b3-143">tooreset 您的密碼，按一下連絡人管理員連結 toosend 電子郵件 tooyour 公司的 IT 人員，並且讓他們知道您將 tooreset 希望您的密碼，因此，它們可以讓您啟用此功能。</span><span class="sxs-lookup"><span data-stu-id="e24b3-143">tooreset your password, click the contact an administrator link toosend an email tooyour company's IT staff, and let them know you want tooreset your password so they can enable this feature for you.</span></span> |
| <span data-ttu-id="e24b3-144">在輸入我的使用者 ID 後，出現了「我們無法驗證您的帳戶」錯誤</span><span class="sxs-lookup"><span data-stu-id="e24b3-144">I get a "we could not verify your account" error after entering my user ID</span></span> | <span data-ttu-id="e24b3-145">我們無法驗證您的帳戶</span><span class="sxs-lookup"><span data-stu-id="e24b3-145">We could not verify your account</span></span> <br> <br> <span data-ttu-id="e24b3-146">如果您想要的話，我們可以請連絡系統管理員可以在您的組織 tooreset 您的密碼。</span><span class="sxs-lookup"><span data-stu-id="e24b3-146">If you'd like, we can contact an administrator in your organization tooreset your password for you.</span></span> | <span data-ttu-id="e24b3-147">您會看到此訊息，因為您已啟用密碼重設，但您沒有註冊 toouse hello 服務。</span><span class="sxs-lookup"><span data-stu-id="e24b3-147">You are seeing this message because you are enabled for password reset, but you have not registered toouse hello service.</span></span> <span data-ttu-id="e24b3-148">tooregister 密碼重設，您已重新取得存取 tooyour 帳戶之後，請移 toohttp://aka.ms/ssprsetup。</span><span class="sxs-lookup"><span data-stu-id="e24b3-148">tooregister for password reset, go toohttp://aka.ms/ssprsetup after you have regained access tooyour account.</span></span> <br> <br> <span data-ttu-id="e24b3-149">tooreset 您的密碼，按一下連絡人管理員連結 toosend 電子郵件 tooyour 公司的 IT 人員。</span><span class="sxs-lookup"><span data-stu-id="e24b3-149">tooreset your password, click the contact an administrator link toosend an email tooyour company's IT staff.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e24b3-150">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e24b3-150">Next Steps</span></span>

* [<span data-ttu-id="e24b3-151">如何 toochange 您使用自助式密碼重設密碼</span><span class="sxs-lookup"><span data-stu-id="e24b3-151">How toochange your password using self-service password reset</span></span>](active-directory-passwords-update-your-own-password.md)
* [<span data-ttu-id="e24b3-152">密碼重設註冊頁面</span><span class="sxs-lookup"><span data-stu-id="e24b3-152">Password reset registration page</span></span>](http://aka.ms/ssprsetup)
* [<span data-ttu-id="e24b3-153">密碼重設入口網站</span><span class="sxs-lookup"><span data-stu-id="e24b3-153">Password reset portal</span></span>](https://passwordreset.microsoftonline.com/)
* [<span data-ttu-id="e24b3-154">無法登入 tooyour Microsoft 帳戶</span><span class="sxs-lookup"><span data-stu-id="e24b3-154">Can't sign in tooyour Microsoft account</span></span>](https://support.microsoft.com/help/12429/microsoft-account-sign-in-cant)

[Register]: ./media/active-directory-passwords-reset-register/register-2-methods.png "顯示已註冊方法及完成按鈕的密碼重設註冊頁面"

