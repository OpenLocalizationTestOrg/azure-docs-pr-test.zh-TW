---
title: "常見問題集︰Azure AD SSPR | Microsoft Docs"
description: "有關 Azure AD 自助式密碼重設的常見問題集。"
services: active-directory
keywords: "Active directory 密碼管理, 密碼管理, Azure AD 自助式密碼重設"
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
ms.openlocfilehash: b3fab99ff9fab5bc67fa70113dc5b06fac775b09
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="password-management-frequently-asked-questions"></a><span data-ttu-id="2b57f-104">密碼管理常見問題集</span><span class="sxs-lookup"><span data-stu-id="2b57f-104">Password management frequently asked questions</span></span>

<span data-ttu-id="2b57f-105">以下是與密碼重設相關之所有事項的一些常見問題。</span><span class="sxs-lookup"><span data-stu-id="2b57f-105">The following are some frequently asked questions for all things related to password reset.</span></span>

<span data-ttu-id="2b57f-106">如果您有關於 Azure AD 和自助式密碼重設的一般問題，但在這裡找不到答案，您可以在 [Azure Ad 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WindowsAzureAD)尋求社群協助。</span><span class="sxs-lookup"><span data-stu-id="2b57f-106">If you have a general question about Azure AD and self-service password reset, that is not answered here, you can ask the community for assistance on the [Azure Ad forums](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WindowsAzureAD).</span></span> <span data-ttu-id="2b57f-107">社群的成員包括工程師、產品經理、MVP 和 IT 專業人員。</span><span class="sxs-lookup"><span data-stu-id="2b57f-107">Members of the community include Engineers, Product Managers, MVPs, and fellow IT Professionals.</span></span>

<span data-ttu-id="2b57f-108">此常見問題集分成下列各節：</span><span class="sxs-lookup"><span data-stu-id="2b57f-108">This FAQ is split into the following sections:</span></span>

* [<span data-ttu-id="2b57f-109">**密碼重設註冊的相關問題**</span><span class="sxs-lookup"><span data-stu-id="2b57f-109">**Questions about Password Reset Registration**</span></span>](#password-reset-registration)
* [<span data-ttu-id="2b57f-110">**密碼重設的相關問題**</span><span class="sxs-lookup"><span data-stu-id="2b57f-110">**Questions about Password Reset**</span></span>](#password-reset)
* [<span data-ttu-id="2b57f-111">**密碼變更的相關問題**</span><span class="sxs-lookup"><span data-stu-id="2b57f-111">**Questions about Password Change**</span></span>](#password-change)
* [<span data-ttu-id="2b57f-112">**密碼管理報告的相關問題**</span><span class="sxs-lookup"><span data-stu-id="2b57f-112">**Questions about password management Reports**</span></span>](#password-management-reports)
* [<span data-ttu-id="2b57f-113">**密碼回寫的相關問題**</span><span class="sxs-lookup"><span data-stu-id="2b57f-113">**Questions about password writeback**</span></span>](#password-writeback)

## <a name="password-reset-registration"></a><span data-ttu-id="2b57f-114">密碼重設註冊</span><span class="sxs-lookup"><span data-stu-id="2b57f-114">Password reset registration</span></span>
* <span data-ttu-id="2b57f-115">**問：我的使用者是否可以註冊自己的密碼重設資料？**</span><span class="sxs-lookup"><span data-stu-id="2b57f-115">**Q:  Can my users register their own password reset data?**</span></span>

  > <span data-ttu-id="2b57f-116">**答：**是，只要已啟用密碼重設功能且使用者已獲得授權，他們就可以前往位於 http://aka.ms/ssprsetup 的「密碼重設註冊」入口網站來註冊其驗證資訊。</span><span class="sxs-lookup"><span data-stu-id="2b57f-116">**A:** Yes, as long as password reset is enabled and they are licensed, they can go to the Password Reset Registration portal at http://aka.ms/ssprsetup to register their authentication information.</span></span> <span data-ttu-id="2b57f-117">使用者也可以前往位於 http://myapps.microsoft.com 的存取面板，按一下 [設定檔] 索引標籤，然後按一下 [註冊密碼重設] 選項，來進行註冊。</span><span class="sxs-lookup"><span data-stu-id="2b57f-117">Users can also register by going to the access panel at http://myapps.microsoft.com, clicking the profile tab, and clicking the Register for Password Reset option.</span></span>
  >
  >
* <span data-ttu-id="2b57f-118">**問：我是否可以代表我的使用者定義密碼重設資料？**</span><span class="sxs-lookup"><span data-stu-id="2b57f-118">**Q:  Can I define password reset data on behalf of my users?**</span></span>

  > <span data-ttu-id="2b57f-119">**答：**是，您可以透過 Azure AD Connect、PowerShell、[Azure 入口網站](https://portal.azure.com) 或 Office Admin 入口網站來進行此動作。</span><span class="sxs-lookup"><span data-stu-id="2b57f-119">**A:** Yes, you can do so with Azure AD Connect, PowerShell, the [Azure portal](https://portal.azure.com), or the Office Admin portal.</span></span> <span data-ttu-id="2b57f-120">如需詳細資訊，請參閱 [Azure AD 自助式密碼重設所用的資料](active-directory-passwords-data.md)一文。</span><span class="sxs-lookup"><span data-stu-id="2b57f-120">For more information, see the article [Data used by Azure AD Self-Service Password Reset](active-directory-passwords-data.md).</span></span>
  >
  >
* <span data-ttu-id="2b57f-121">**問：我是否可以從內部部署環境同步處理安全性問題的資料？**</span><span class="sxs-lookup"><span data-stu-id="2b57f-121">**Q:  Can I synchronize data for security questions from on premises?**</span></span>

  > <span data-ttu-id="2b57f-122">**答：** 目前無法這麼做。</span><span class="sxs-lookup"><span data-stu-id="2b57f-122">**A:** This is not possible today.</span></span>
  >
  >
* <span data-ttu-id="2b57f-123">**問：我的使用者是否可以用讓其他使用者看不到資料的方式來註冊該資料？**</span><span class="sxs-lookup"><span data-stu-id="2b57f-123">**Q:  Can my users register data in such a way that other users cannot see this data?**</span></span>

  > <span data-ttu-id="2b57f-124">**答：**是，當使用者使用「密碼重設註冊入口網站」來註冊資料時，該資料會儲存到私密的驗證欄位中，只有「全域管理員」和使用者能夠看見。</span><span class="sxs-lookup"><span data-stu-id="2b57f-124">**A:** Yes, when users register data using the Password Reset Registration Portal it is saved into private authentication fields that are only visible by Global Administrators and the user.</span></span>
    >
    > [!NOTE]
    > <span data-ttu-id="2b57f-125">如果 **Azure 系統管理員帳戶**註冊其驗證電話號碼，該號碼也會填入行動電話欄位中並顯示出來。</span><span class="sxs-lookup"><span data-stu-id="2b57f-125">If an **Azure Administrator account** registers their authentication phone number it is also populated into the mobile phone field and is visible.</span></span>
    >
  >
  >
* <span data-ttu-id="2b57f-126">**問：我的使用者是否必須先註冊才能使用密碼重設？**</span><span class="sxs-lookup"><span data-stu-id="2b57f-126">**Q:  Do my users have to be registered before they can use password reset?**</span></span>

  > <span data-ttu-id="2b57f-127">**答：**否，如果您代表使用者定義足夠的驗證資訊，使用者就不需要註冊。</span><span class="sxs-lookup"><span data-stu-id="2b57f-127">**A:** No, if you define enough authentication information on their behalf, users do not have to register.</span></span> <span data-ttu-id="2b57f-128">只要您已正確地格式化儲存在目錄中適當欄位的資料，密碼重設就能運作。</span><span class="sxs-lookup"><span data-stu-id="2b57f-128">Password reset works as long as you have properly formatted data stored in the appropriate fields in the directory.</span></span>
  >
  >
* <span data-ttu-id="2b57f-129">**問：我是否可以代表我的使用者同步處理或設定驗證電話、驗證電子郵件或備用驗證電話欄位？**</span><span class="sxs-lookup"><span data-stu-id="2b57f-129">**Q:  Can I synchronize or set the Authentication Phone, Authentication Email or Alternate Authentication Phone fields on behalf of my users?**</span></span>

  > <span data-ttu-id="2b57f-130">**答：** 目前無法這麼做。</span><span class="sxs-lookup"><span data-stu-id="2b57f-130">**A:** This is not possible today.</span></span>
  >
  >
* <span data-ttu-id="2b57f-131">**問：註冊入口網站如何得知要對我的使用者顯示哪些選項？**</span><span class="sxs-lookup"><span data-stu-id="2b57f-131">**Q:  How does the registration portal know which options to show my users?**</span></span>

  > <span data-ttu-id="2b57f-132">**答：**密碼重設註冊入口網站只會顯示您為使用者啟用的選項。</span><span class="sxs-lookup"><span data-stu-id="2b57f-132">**A:** The password reset registration portal only shows the options that you have enabled for your users.</span></span> <span data-ttu-id="2b57f-133">在目錄的 [設定] 索引標籤的 [使用者密碼重設原則] 區段之下可以找到這些選項。</span><span class="sxs-lookup"><span data-stu-id="2b57f-133">These options are found under the User Password Reset Policy section of your directory’s Configure tab.</span></span> <span data-ttu-id="2b57f-134">例如，這表示如果您未啟用安全性問題，使用者便無法註冊該選項。</span><span class="sxs-lookup"><span data-stu-id="2b57f-134">For example, this means that if you do not enable security questions, then users are not able to register for that option.</span></span>
  >
  >
* <span data-ttu-id="2b57f-135">**問：使用者何時會被視為已註冊？**</span><span class="sxs-lookup"><span data-stu-id="2b57f-135">**Q:  When is a user considered registered?**</span></span>

  > <span data-ttu-id="2b57f-136">**答︰**使用者至少已註冊您在 [Azure 入口網站](https://portal.azure.com)中設定的 [重設所需的方法數目]，才算完成 SSPR 註冊。</span><span class="sxs-lookup"><span data-stu-id="2b57f-136">**A:** A user is considered registered for SSPR when they have registered at least the **Number of methods required to reset** that you have set in the [Azure portal](https://portal.azure.com).</span></span>
  >
  >
## <a name="password-reset"></a><span data-ttu-id="2b57f-137">密碼重設</span><span class="sxs-lookup"><span data-stu-id="2b57f-137">Password reset</span></span>
* <span data-ttu-id="2b57f-138">**問：密碼重設之後，我應該等待多久才能收到電子郵件、SMS 或來電？**</span><span class="sxs-lookup"><span data-stu-id="2b57f-138">**Q:  How long should I wait to receive an email, SMS, or phone call from password reset?**</span></span>

  > <span data-ttu-id="2b57f-139">**答：**電子郵件、SMS 訊息及電話應該在 1 分鐘內即可送達，正常的情形下為 5-20 秒。</span><span class="sxs-lookup"><span data-stu-id="2b57f-139">**A:** Email, SMS messages, and phone calls should arrive in under one minute, with the normal case being 5-20 seconds.</span></span>
    ><span data-ttu-id="2b57f-140">如果您未在此時間範圍內收到通知︰</span><span class="sxs-lookup"><span data-stu-id="2b57f-140">If you do not receive the notification in this time frame:</span></span>
        > * <span data-ttu-id="2b57f-141">檢查您的垃圾郵件資料夾。</span><span class="sxs-lookup"><span data-stu-id="2b57f-141">Check your junk folder.</span></span>
        > * <span data-ttu-id="2b57f-142">檢查正在聯繫的數字或電子郵件是您預期的項目。</span><span class="sxs-lookup"><span data-stu-id="2b57f-142">Check the number or email being contacted is the one you expect.</span></span>
        > * <span data-ttu-id="2b57f-143">檢查目錄中的驗證資料是否正確地格式化。</span><span class="sxs-lookup"><span data-stu-id="2b57f-143">Check the authentication data in the directory is correctly formatted.</span></span>
                >     * <span data-ttu-id="2b57f-144">範例："+1 4255551234" 或 "user@contoso.com"</span><span class="sxs-lookup"><span data-stu-id="2b57f-144">Example: "+1 4255551234" or "user@contoso.com"</span></span>
  >
  >
* <span data-ttu-id="2b57f-145">**問：密碼重設支援哪些語言？**</span><span class="sxs-lookup"><span data-stu-id="2b57f-145">**Q:  What languages are supported by password reset?**</span></span>

  > <span data-ttu-id="2b57f-146">**答：**密碼重設 UI、SMS 訊息及語音通話都已採用 Office 365 支援的相同語言當地語系化。</span><span class="sxs-lookup"><span data-stu-id="2b57f-146">**A:** The password reset UI, SMS messages, and voice calls are localized in the same languages that are supported in Office 365.</span></span>
  >
  >
* <span data-ttu-id="2b57f-147">**問：當我在目錄的 [設定] 索引標籤中設定組織商標時，哪個密碼重設體驗部分會有商標？**</span><span class="sxs-lookup"><span data-stu-id="2b57f-147">**Q:  What parts of the password reset experience get branded when I set organizational branding in my directory’s configure tab?**</span></span>

  > <span data-ttu-id="2b57f-148">**答：**密碼重設入口網站會顯示您的組織商標，並且讓您設定「連絡您的系統管理員」連結以指向自訂的電子郵件或 URL。</span><span class="sxs-lookup"><span data-stu-id="2b57f-148">**A:** The password reset portal shows your organizational logo and allows you to configure the Contact your administrator link to point to a custom email or URL.</span></span> <span data-ttu-id="2b57f-149">密碼重設所傳送的任何電子郵件都會包含您的組織商標、顏色、電子郵件內文中的名稱，以及自訂的寄件者名稱。</span><span class="sxs-lookup"><span data-stu-id="2b57f-149">Any email that gets sent by password reset includes your organization’s logo, colors, name in the body of the email, and customized from name.</span></span>
  >
  >
* <span data-ttu-id="2b57f-150">**問：如何教育我的使用者要在哪裡重設其密碼？**</span><span class="sxs-lookup"><span data-stu-id="2b57f-150">**Q:  How can I educate my users about where to go to reset their passwords?**</span></span>

  > <span data-ttu-id="2b57f-151">**答：**您可以將使用者直接帶往 https://passwordreset.microsoftonline.com ，也可以指示他們按一下可在任何工作或學校登入頁面上找到的「無法存取您的帳戶」連結。</span><span class="sxs-lookup"><span data-stu-id="2b57f-151">**A:** You can send your users to https://passwordreset.microsoftonline.com directly, or you can instruct them to click the **Can’t access your account link** found on any Work or School sign-in page.</span></span> <span data-ttu-id="2b57f-152">您也可以在使用者方便存取的地方發佈這些連結。</span><span class="sxs-lookup"><span data-stu-id="2b57f-152">You can also publish these links in a place easily accessible to your users.</span></span>
  >
  >
* <span data-ttu-id="2b57f-153">**問：我是否可以從行動裝置使用此頁面？**</span><span class="sxs-lookup"><span data-stu-id="2b57f-153">**Q:  Can I use this page from a mobile device?**</span></span>

  > <span data-ttu-id="2b57f-154">**答：** 是，此頁面可在行動裝置上運作。</span><span class="sxs-lookup"><span data-stu-id="2b57f-154">**A:** Yes, this page works on mobile devices.</span></span>
  >
  >
* <span data-ttu-id="2b57f-155">**問：當使用者重設其密碼時，您是否支援將本機 Active Directory 帳戶解除鎖定？**</span><span class="sxs-lookup"><span data-stu-id="2b57f-155">**Q:  Do you support unlocking local active directory accounts when users reset their passwords?**</span></span>

  > <span data-ttu-id="2b57f-156">**答：**是，當使用者重設其密碼並使用 Azure AD Connect 部署密碼回寫時，該使用者的帳戶會在其重設密碼時自動解除鎖定。</span><span class="sxs-lookup"><span data-stu-id="2b57f-156">**A:** Yes, when a user resets their password and password writeback has been deployed using Azure AD Connect, that user’s account is automatically unlocked when they reset their password.</span></span>
  >
  >
* <span data-ttu-id="2b57f-157">**問：我要如何將密碼重設直接整合到我使用者的桌面登入體驗？**</span><span class="sxs-lookup"><span data-stu-id="2b57f-157">**Q:  How can I integrate password reset directly into my user’s desktop sign-in experience?**</span></span>

  > <span data-ttu-id="2b57f-158">**答：**如果您是 Azure AD Premium 客戶，您不需要額外成本即可安裝 Microsoft Identity Manager，並且部署內部部署密碼重設解決方案，以符合這項需求。</span><span class="sxs-lookup"><span data-stu-id="2b57f-158">**A:** If you are an Azure AD Premium customer, you can install Microsoft Identity Manager at no additional cost and deploy the on-premises password reset solution to meet this requirement.</span></span>
  >
  >
* <span data-ttu-id="2b57f-159">**問：我是否可以針對不同的地區設定，設定不同的安全性問題？**</span><span class="sxs-lookup"><span data-stu-id="2b57f-159">**Q:  Can I set different security questions for different locales?**</span></span>

  > <span data-ttu-id="2b57f-160">**答：** 目前無法這麼做。</span><span class="sxs-lookup"><span data-stu-id="2b57f-160">**A:** This is not possible today.</span></span>
  >
  >
* <span data-ttu-id="2b57f-161">**問：我們可以為安全性問題驗證選項設定多少問題？**</span><span class="sxs-lookup"><span data-stu-id="2b57f-161">**Q:  How many questions can we configure for the Security Questions authentication option?**</span></span>

  > <span data-ttu-id="2b57f-162">**答：**您可以在 [Azure 入口網站](https://portal.azure.com)中設定最多 20 個自訂安全性問題。</span><span class="sxs-lookup"><span data-stu-id="2b57f-162">**A:** You can configure up to 20 custom security questions in the [Azure portal](https://portal.azure.com).</span></span>
  >
  >
* <span data-ttu-id="2b57f-163">**問：安全性問題的長度限制為何？**</span><span class="sxs-lookup"><span data-stu-id="2b57f-163">**Q:  How long may security questions be?**</span></span>

  > <span data-ttu-id="2b57f-164">**答：** 安全性問題的長度可以介於 3 到 200 個字元之間。</span><span class="sxs-lookup"><span data-stu-id="2b57f-164">**A:** Security questions may be between 3 and 200 characters long.</span></span>
  >
  >
* <span data-ttu-id="2b57f-165">**問：安全性問題答案的長度限制為何？**</span><span class="sxs-lookup"><span data-stu-id="2b57f-165">**Q:  How long may answers to security questions be?**</span></span>

  > <span data-ttu-id="2b57f-166">**答：** 答案的長度可以介於 3 到 40 個字元之間。</span><span class="sxs-lookup"><span data-stu-id="2b57f-166">**A:** Answers may be 3 to 40 characters long.</span></span>
  >
  >
* <span data-ttu-id="2b57f-167">**問：重複的安全性問題答案是否會遭到拒絕？**</span><span class="sxs-lookup"><span data-stu-id="2b57f-167">**Q:  Are duplicate answers to security questions rejected?**</span></span>

  > <span data-ttu-id="2b57f-168">**答：** 是，我們會拒絕重複的安全性問題答案。</span><span class="sxs-lookup"><span data-stu-id="2b57f-168">**A:** Yes, we reject duplicate answers to security questions.</span></span>
  >
  >
* <span data-ttu-id="2b57f-169">**問：使用者是否可以多次註冊相同的安全性問題？**</span><span class="sxs-lookup"><span data-stu-id="2b57f-169">**Q:  May a user register the same security question more than once?**</span></span>

  > <span data-ttu-id="2b57f-170">**答：**否，使用者註冊一旦特定的問題，便不可以再次註冊該問題。</span><span class="sxs-lookup"><span data-stu-id="2b57f-170">**A:** No, once a user registers a particular question, they may not register for that question a second time.</span></span>
  >
  >
* <span data-ttu-id="2b57f-171">**問：是否可以針對註冊和重設設定安全性問題的最小限制？**</span><span class="sxs-lookup"><span data-stu-id="2b57f-171">**Q:  Is it possible to set a minimum limit of security questions for registration and reset?**</span></span>

  > <span data-ttu-id="2b57f-172">**答：** 是，可以針對註冊設定一個限制，針對重設設定另一個限制。</span><span class="sxs-lookup"><span data-stu-id="2b57f-172">**A:** Yes, one limit can be set for registration and another for reset.</span></span> <span data-ttu-id="2b57f-173">註冊可能需要 3-5 個安全性問題，重設也需要 3-5 個安全性問題。</span><span class="sxs-lookup"><span data-stu-id="2b57f-173">3-5 security questions may be required for registration and 3-5 may be required for reset.</span></span>
  >
  >
* <span data-ttu-id="2b57f-174">**問：如果使用者註冊的問題數目超過重設所需的問題數目上限，在重設期間會如何選取安全性問題？**</span><span class="sxs-lookup"><span data-stu-id="2b57f-174">**Q:  If a user has registered more than the maximum number of questions required to reset, how are security questions selected during reset?**</span></span>

  > <span data-ttu-id="2b57f-175">**答：**會在使用者已註冊的問題總數當中隨機選取 N 個安全性問題，其中 N 是 [重設所需的問題數目]。</span><span class="sxs-lookup"><span data-stu-id="2b57f-175">**A:** N security questions are selected at random out of the total number of questions a user has registered for, where N is the **Number of questions required to reset**.</span></span> <span data-ttu-id="2b57f-176">例如，如果使用者已註冊 5 個安全性問題，但是重設只需要 3 個，則會在 5 個問題當中隨機選取 3 個並且在重設時顯示。</span><span class="sxs-lookup"><span data-stu-id="2b57f-176">For example, if a user has 5 security questions registered, but only 3 are required to reset, 3 of the 5 are selected randomly and presented at reset.</span></span> <span data-ttu-id="2b57f-177">如果使用者回答問題的答案錯誤，則選取程序會重新發生以避免問題 Hammering。</span><span class="sxs-lookup"><span data-stu-id="2b57f-177">If the user gets the answers to the questions wrong, the selection process reoccurs to prevent question hammering.</span></span>
  >
  >
* <span data-ttu-id="2b57f-178">**問：您是否禁止使用者在短時間內嘗試多次密碼重設？**</span><span class="sxs-lookup"><span data-stu-id="2b57f-178">**Q:  Do you prevent users from attempting password reset many times in a short time period?**</span></span>

  > <span data-ttu-id="2b57f-179">**答：**是，密碼重設有一些內建的安全性功能，以防止濫用。</span><span class="sxs-lookup"><span data-stu-id="2b57f-179">**A:** Yes, there are security features built into password reset to protect from misuse.</span></span> <span data-ttu-id="2b57f-180">使用者在一個小時之內只能嘗試 5 次密碼重設，否則會鎖定 24 小時。</span><span class="sxs-lookup"><span data-stu-id="2b57f-180">Users may only try 5 password reset attempts within an hour before being locked out for 24 hours.</span></span> <span data-ttu-id="2b57f-181">使用者在一個小時之內只能嘗試驗證電話號碼 5 次，否則會鎖定 24 小時。</span><span class="sxs-lookup"><span data-stu-id="2b57f-181">Users may only try to validate a phone number 5 times within an hour before being locked out for 24 hours.</span></span> <span data-ttu-id="2b57f-182">使用者在一個小時之內只能嘗試單一驗證方法 5 次，否則會鎖定 24 小時。</span><span class="sxs-lookup"><span data-stu-id="2b57f-182">Users may only try a single authentication method 5 times within an hour before being locked out for 24 hours.</span></span>
  >
  >
* <span data-ttu-id="2b57f-183">**問：電子郵件和 SMS 單次密碼的有效期限是多久？**</span><span class="sxs-lookup"><span data-stu-id="2b57f-183">**Q:  For how long are the email and SMS one-time passcode valid?**</span></span>

  > <span data-ttu-id="2b57f-184">**答：** 密碼重設的工作階段存留期為 105 分鐘。</span><span class="sxs-lookup"><span data-stu-id="2b57f-184">**A:** The session lifetime for password reset is 105 minutes.</span></span> <span data-ttu-id="2b57f-185">從密碼重設作業開始，使用者有 105 分鐘可以重設其密碼。</span><span class="sxs-lookup"><span data-stu-id="2b57f-185">From the beginning of the password reset operation, the user has 105 minutes to reset their password.</span></span> <span data-ttu-id="2b57f-186">這段時間之後，電子郵件和 SMS 單次密碼就會無效。</span><span class="sxs-lookup"><span data-stu-id="2b57f-186">The email and SMS one-time passcode are invalid after this time period expires.</span></span>
  >
  >

## <a name="password-change"></a><span data-ttu-id="2b57f-187">密碼變更</span><span class="sxs-lookup"><span data-stu-id="2b57f-187">Password change</span></span>
* <span data-ttu-id="2b57f-188">**問︰我的使用者應該到何處變更密碼？**</span><span class="sxs-lookup"><span data-stu-id="2b57f-188">**Q:  Where should my users go to change their passwords?**</span></span>

  > <span data-ttu-id="2b57f-189">**答︰**使用者可以在出現個人資料圖片或圖示的任何位置變更密碼 (例如操作 [Office 365](https://portal.office.com) 或[存取面板](https://myapps.microsoft.com)時的右上角)。</span><span class="sxs-lookup"><span data-stu-id="2b57f-189">**A:** Users may change their passwords anywhere they see their profile picture or icon (like in the upper right corner of their [Office 365](https://portal.office.com) or [Access Panel](https://myapps.microsoft.com) experiences.</span></span> <span data-ttu-id="2b57f-190">使用者可以從[存取面板個人資料頁面](https://account.activedirectory.windowsazure.com/r#/profile)變更密碼。</span><span class="sxs-lookup"><span data-stu-id="2b57f-190">Users may change their passwords from the [Access Panel profile page](https://account.activedirectory.windowsazure.com/r#/profile).</span></span> <span data-ttu-id="2b57f-191">如果使用者的密碼已過期，Azure AD 登入畫面也可能自動要求使用者變更密碼。</span><span class="sxs-lookup"><span data-stu-id="2b57f-191">Users may also be asked to change their passwords automatically at the Azure AD sign-in screen if their passwords have expired.</span></span> <span data-ttu-id="2b57f-192">最後，如果使用者想要變更密碼，可以直接瀏覽至 [Azure AD 密碼變更入口網站](https://account.activedirectory.windowsazure.com/ChangePassword.aspx)。</span><span class="sxs-lookup"><span data-stu-id="2b57f-192">Finally, users may navigate to the [Azure AD Password Change Portal](https://account.activedirectory.windowsazure.com/ChangePassword.aspx) directly if they wish to change their passwords.</span></span>
  >
  >
* <span data-ttu-id="2b57f-193">**問︰當使用者的內部部署密碼過期時，Office 入口網站會加以通知嗎？**</span><span class="sxs-lookup"><span data-stu-id="2b57f-193">**Q:  Can my users be notified in the Office Portal when their on-premises password expires?**</span></span>

  > <span data-ttu-id="2b57f-194">**答︰**如果您使用 ADFS，依照此處的指示進行就會收到通知：[使用 ADFS 傳送密碼原則宣告](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configure-ad-fs-to-send-password-expiry-claims?f=255&MSPPError=-2147217396)。</span><span class="sxs-lookup"><span data-stu-id="2b57f-194">**A:** This is possible today if you are using ADFS by following the instructions here: [Sending Password Policy Claims with ADFS](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configure-ad-fs-to-send-password-expiry-claims?f=255&MSPPError=-2147217396).</span></span> <span data-ttu-id="2b57f-195">如果您使用密碼雜湊同步處理，則目前還不可能。</span><span class="sxs-lookup"><span data-stu-id="2b57f-195">If you are using password hash synchronization, this is not possible today.</span></span> <span data-ttu-id="2b57f-196">這是因為我們不會從內部部署來同步處理密碼原則，所以無法在雲端操作過程中發佈到期通知。</span><span class="sxs-lookup"><span data-stu-id="2b57f-196">This is because we do not sync password policies from on-premises, so it is not possible for us to post expiry notifications to cloud experiences.</span></span> <span data-ttu-id="2b57f-197">在任一情況下，也可以[使用 PowerShell 通知使用者密碼即將到期](https://social.technet.microsoft.com/wiki/contents/articles/23313.notify-active-directory-users-about-password-expiry-using-powershell.aspx)。</span><span class="sxs-lookup"><span data-stu-id="2b57f-197">In either case, it is also possible to [notify users whose passwords are about to expire by using PowerShell](https://social.technet.microsoft.com/wiki/contents/articles/23313.notify-active-directory-users-about-password-expiry-using-powershell.aspx).</span></span>
  >
  >

## <a name="password-management-reports"></a><span data-ttu-id="2b57f-198">密碼管理報告</span><span class="sxs-lookup"><span data-stu-id="2b57f-198">Password management reports</span></span>
* <span data-ttu-id="2b57f-199">**問：資料需要多久的時間才會顯示在密碼管理報告上？**</span><span class="sxs-lookup"><span data-stu-id="2b57f-199">**Q:  How long does it take for data to show up on the password management reports?**</span></span>

  > <span data-ttu-id="2b57f-200">**答：** 資料應該會在 5-10 分鐘內顯示在密碼管理報告上。</span><span class="sxs-lookup"><span data-stu-id="2b57f-200">**A:** Data should appear on the password management reports within 5-10 minutes.</span></span> <span data-ttu-id="2b57f-201">某些情況下，可能會花費多達一小時才顯示。</span><span class="sxs-lookup"><span data-stu-id="2b57f-201">It some instances it may take up to an hour to appear.</span></span>
  >
  >
* <span data-ttu-id="2b57f-202">**問：我要如何篩選密碼管理報告？**</span><span class="sxs-lookup"><span data-stu-id="2b57f-202">**Q:  How can I filter the password management reports?**</span></span>

  > <span data-ttu-id="2b57f-203">**答：**您可以在接近報告頂端處，按一下欄標籤最右邊的小放大鏡圖示，以篩選密碼管理報告。</span><span class="sxs-lookup"><span data-stu-id="2b57f-203">**A:** You can filter the password management reports by clicking the small magnifying glass to the extreme right of the column labels, near the top of the report.</span></span> <span data-ttu-id="2b57f-204">如果您想要做更豐富的篩選，您可以將報告下載到 excel，並建立樞紐分析表。</span><span class="sxs-lookup"><span data-stu-id="2b57f-204">If you want to do richer filtering, you can download the report to excel and create a pivot table.</span></span>
  >
  >
* <span data-ttu-id="2b57f-205">**問：密碼管理報告中最多可以儲存多少事件？**</span><span class="sxs-lookup"><span data-stu-id="2b57f-205">**Q: What is the maximum number of events are stored in the password management reports?**</span></span>

  > <span data-ttu-id="2b57f-206">**答：**密碼管理報告中最多可以儲存 75,000 個密碼重設或密碼重設註冊事件，最多可回溯 30 天。</span><span class="sxs-lookup"><span data-stu-id="2b57f-206">**A:** Up to 75,000 password reset or password reset registration events are stored in the password management reports, spanning back up to 30 days.</span></span>  <span data-ttu-id="2b57f-207">我們正在擴展此數目，以包含更多的事件。</span><span class="sxs-lookup"><span data-stu-id="2b57f-207">We are working to expand this number to include more events.</span></span>
  >
  >
* <span data-ttu-id="2b57f-208">**問：密碼管理報告可以回溯到多久以前？**</span><span class="sxs-lookup"><span data-stu-id="2b57f-208">**Q:  How far back do the password management reports go?**</span></span>

  > <span data-ttu-id="2b57f-209">**答：** 密碼管理報告會顯示過去 30 天內發生的作業。</span><span class="sxs-lookup"><span data-stu-id="2b57f-209">**A:** The password management reports show operations occurring within the last 30 days.</span></span> <span data-ttu-id="2b57f-210">現在，如果您需要封存這項資料，您可以定期下載報告並將它們儲存在不同的位置。</span><span class="sxs-lookup"><span data-stu-id="2b57f-210">For now, if you need to archive this data, you can download the reports periodically and save them in a separate location.</span></span>
  >
  >
* <span data-ttu-id="2b57f-211">**問：密碼管理報告可以顯示的資料列是否有數目上限？**</span><span class="sxs-lookup"><span data-stu-id="2b57f-211">**Q:  Is there a maximum number of rows that can appear on the password management reports?**</span></span>

  > <span data-ttu-id="2b57f-212">**答：**是，不論是在 UI 中顯示或是下載，任一密碼管理報告最多只能顯示 75,000 個資料列。</span><span class="sxs-lookup"><span data-stu-id="2b57f-212">**A:** Yes, a maximum of 75,000 rows may appear on either of the password management reports, whether they are being shown in the UI or being downloaded.</span></span>
  >
  >
* <span data-ttu-id="2b57f-213">**問：是否有可用來存取密碼重設或註冊報告資料的 API？**</span><span class="sxs-lookup"><span data-stu-id="2b57f-213">**Q:  Is there an API to access the password reset or registration reporting data?**</span></span>

  > <span data-ttu-id="2b57f-214">**答：**是，請參閱下列文件，以了解如何存取密碼重設報告資料流。</span><span class="sxs-lookup"><span data-stu-id="2b57f-214">**A:** Yes, see the following documentation to learn how you can access the password reset reporting data stream.</span></span>  <span data-ttu-id="2b57f-215">[了解如何以程式設計方式存取密碼重設報告事件](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent)。</span><span class="sxs-lookup"><span data-stu-id="2b57f-215">[Learn how to access password reset reporting events programmatically](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent).</span></span>
  >
  >

## <a name="password-writeback"></a><span data-ttu-id="2b57f-216">密碼回寫</span><span class="sxs-lookup"><span data-stu-id="2b57f-216">Password writeback</span></span>
* <span data-ttu-id="2b57f-217">**問：密碼回寫如何在幕後運作？**</span><span class="sxs-lookup"><span data-stu-id="2b57f-217">**Q:  How does password writeback work behind the scenes?**</span></span>

  > <span data-ttu-id="2b57f-218">**答：**請參閱[密碼回寫的運作方式](active-directory-passwords-writeback.md)，以了解啟用「密碼回寫」時會發生的情況，以及資料如何透過系統回流到您的內部部署環境。</span><span class="sxs-lookup"><span data-stu-id="2b57f-218">**A:** See [How password writeback works](active-directory-passwords-writeback.md) for an explanation of what happens when you enable password writeback, and how data flows through the system back into your on-premises environment.</span></span>
  >
  >
* <span data-ttu-id="2b57f-219">**問：密碼回寫需要多久時間才會運作？是否有像是使用密碼雜湊同步處理的同步處理延遲？**</span><span class="sxs-lookup"><span data-stu-id="2b57f-219">**Q:  How long does password writeback take to work?  Is there a synchronization delay like with password hash sync?**</span></span>

  > <span data-ttu-id="2b57f-220">**答：**密碼回寫會立即進行。</span><span class="sxs-lookup"><span data-stu-id="2b57f-220">**A:** Password writeback is instant.</span></span> <span data-ttu-id="2b57f-221">它是同步管線，基本上的運作與密碼雜湊同步處理不同。</span><span class="sxs-lookup"><span data-stu-id="2b57f-221">It is a synchronous pipeline that works fundamentally differently than password hash synchronization.</span></span> <span data-ttu-id="2b57f-222">密碼回寫可以讓使用者即時取得密碼重設或變更作業成功的回應。</span><span class="sxs-lookup"><span data-stu-id="2b57f-222">Password writeback allows users to get real-time feedback about the success of their password reset or change operation.</span></span> <span data-ttu-id="2b57f-223">成功回寫密碼的平均時間低於 500 毫秒。</span><span class="sxs-lookup"><span data-stu-id="2b57f-223">The average time for a successful writeback of a password is under 500 ms.</span></span>
  >
  >
* <span data-ttu-id="2b57f-224">**問︰如果我的內部部署帳戶已停用，這對我的雲端帳戶/存取有何影響？**</span><span class="sxs-lookup"><span data-stu-id="2b57f-224">**Q:  If my on-premises account is disabled, how is my cloud account/access affected?**</span></span>

  > <span data-ttu-id="2b57f-225">**答︰**如果您的內部部署識別碼已停用，您的雲端識別碼/存取也會透過 AAD Connect 在下一個同步處理間隔 (預設每隔 30 分鐘) 停用。</span><span class="sxs-lookup"><span data-stu-id="2b57f-225">**A:** If your on-premises ID is disabled, your cloud ID/access will also be disabled at the next sync interval via AAD Connect byt default this is every 30 minutes.</span></span>
  >
  >
* <span data-ttu-id="2b57f-226">**問︰如果我的內部部署帳戶受到內部部署 Active Directory 密碼原則限制，則當我變更密碼時 SSPR 是否會遵守此原則時？**</span><span class="sxs-lookup"><span data-stu-id="2b57f-226">**Q:  If my on-premises account is constrained by an on-premises Active Directory password policy, does SSPR obey this policy when I change the password?**</span></span>

  > <span data-ttu-id="2b57f-227">**答︰**是，SSPR 會依循並遵守內部部署 AD 密碼原則，包括一般的 AD 網域密碼原則，以及任何以特定使用者為目標而定義的細微密碼原則。</span><span class="sxs-lookup"><span data-stu-id="2b57f-227">**A:** Yes, SSPR relies on and abides by the on-premises AD password policy, including typical AD domain password policy, as well as any defined fine grained password policies targeted to a given user.</span></span>
  >
  >
* <span data-ttu-id="2b57f-228">**問：密碼回寫適用於哪些類型的帳戶？**</span><span class="sxs-lookup"><span data-stu-id="2b57f-228">**Q:  What types of accounts does password writeback work for?**</span></span>

  > <span data-ttu-id="2b57f-229">**答：**密碼回寫適用於「同盟」和「密碼雜湊同步」使用者。</span><span class="sxs-lookup"><span data-stu-id="2b57f-229">**A:** Password writeback works for Federated and Password Hash Synchronized users.</span></span>
  >
  >
* <span data-ttu-id="2b57f-230">**問：密碼回寫是否會強制執行我的網域密碼原則？**</span><span class="sxs-lookup"><span data-stu-id="2b57f-230">**Q:  Does password writeback enforce my domain’s password policies?**</span></span>

  > <span data-ttu-id="2b57f-231">**答：**是，密碼回寫會強制執行密碼使用期限、歷程記錄、複雜度、篩選及任何其他您可能在本機網域中的密碼上適當加諸的限制。</span><span class="sxs-lookup"><span data-stu-id="2b57f-231">**A:** Yes, password writeback enforces password age, history, complexity, filters, and any other restriction you may put in place on passwords in your local domain.</span></span>
  >
  >
* <span data-ttu-id="2b57f-232">**問：密碼回寫是否安全？我要如何確定不會受到駭客入侵？**</span><span class="sxs-lookup"><span data-stu-id="2b57f-232">**Q:  Is password writeback secure?  How can I be sure I won’t get hacked?**</span></span>

  > <span data-ttu-id="2b57f-233">**答：**是，密碼回寫很安全。</span><span class="sxs-lookup"><span data-stu-id="2b57f-233">**A:** Yes, password writeback is secure.</span></span> <span data-ttu-id="2b57f-234">若要進一步了解密碼回寫服務所實作的 4 層安全性，請參閱＜密碼回寫的運作方式＞中的[密碼回寫的安全性模型](active-directory-passwords-writeback.md#password-writeback-security-model)一節。</span><span class="sxs-lookup"><span data-stu-id="2b57f-234">To read more about the four layers of security implemented by the password writeback service, check out the [Password writeback security model](active-directory-passwords-writeback.md#password-writeback-security-model) section in How password writeback works.</span></span>
  >
  >

## <a name="next-steps"></a><span data-ttu-id="2b57f-235">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2b57f-235">Next steps</span></span>

<span data-ttu-id="2b57f-236">下列連結提供有關使用 Azure AD 重設密碼的其他資訊</span><span class="sxs-lookup"><span data-stu-id="2b57f-236">The following links provide additional information regarding password reset using Azure AD</span></span>

* <span data-ttu-id="2b57f-237">[**快速入門**](active-directory-passwords-getting-started.md) - 開始執行 Azure AD 自助式密碼管理</span><span class="sxs-lookup"><span data-stu-id="2b57f-237">[**Quick Start**](active-directory-passwords-getting-started.md) - Get up and running with Azure AD self service password management</span></span> 
* <span data-ttu-id="2b57f-238">[**授權**](active-directory-passwords-licensing.md) - 設定 Azure AD 授權</span><span class="sxs-lookup"><span data-stu-id="2b57f-238">[**Licensing**](active-directory-passwords-licensing.md) - Configure your Azure AD Licensing</span></span>
* <span data-ttu-id="2b57f-239">[**資料**](active-directory-passwords-data.md) -了解所需的資料以及如何將它使用於密碼管理</span><span class="sxs-lookup"><span data-stu-id="2b57f-239">[**Data**](active-directory-passwords-data.md) - Understand the data that is required and how it is used for password management</span></span>
* <span data-ttu-id="2b57f-240">[**推出**](active-directory-passwords-best-practices.md) - 使用此處提供的指引來規劃 SSPR 並將它部署至使用者</span><span class="sxs-lookup"><span data-stu-id="2b57f-240">[**Rollout**](active-directory-passwords-best-practices.md) - Plan and deploy SSPR to your users using the guidance found here</span></span>
* <span data-ttu-id="2b57f-241">[**自訂**](active-directory-passwords-customize.md) - 為您的公司自訂 SSPR 體驗的外觀與風格。</span><span class="sxs-lookup"><span data-stu-id="2b57f-241">[**Customize**](active-directory-passwords-customize.md) - Customize the look and feel of the SSPR experience for your company.</span></span>
* <span data-ttu-id="2b57f-242">[**報告**](active-directory-passwords-reporting.md) - 探索您的使用者是否、何時、何地存取 SSPR 功能</span><span class="sxs-lookup"><span data-stu-id="2b57f-242">[**Reporting**](active-directory-passwords-reporting.md) - Discover if, when, and where your users are accessing SSPR functionality</span></span>
* <span data-ttu-id="2b57f-243">[**原則**](active-directory-passwords-policy.md) - 了解並設定 Azure AD 密碼原則</span><span class="sxs-lookup"><span data-stu-id="2b57f-243">[**Policy**](active-directory-passwords-policy.md) - Understand and set Azure AD password policies</span></span>
* <span data-ttu-id="2b57f-244">[**密碼回寫**](active-directory-passwords-writeback.md) - 密碼回寫如何用在您的內部部署目錄</span><span class="sxs-lookup"><span data-stu-id="2b57f-244">[**Password Writeback**](active-directory-passwords-writeback.md) - How does password writeback work with your on-premises directory</span></span>
* <span data-ttu-id="2b57f-245">[**技術性深入探討**](active-directory-passwords-how-it-works.md) - 深入探索以了解其運作方式</span><span class="sxs-lookup"><span data-stu-id="2b57f-245">[**Technical Deep Dive**](active-directory-passwords-how-it-works.md) - Go behind the curtain to understand how it works</span></span>
* <span data-ttu-id="2b57f-246">[**疑難排解**](active-directory-passwords-troubleshoot.md) - 了解如何解決我們看到的 SSPR 常見問題</span><span class="sxs-lookup"><span data-stu-id="2b57f-246">[**Troubleshoot**](active-directory-passwords-troubleshoot.md) - Learn how to resolve common issues that we see with SSPR</span></span>
