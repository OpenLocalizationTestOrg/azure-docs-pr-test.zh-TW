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
ms.openlocfilehash: d04a9efeb3b35421aa605cadb2aa25f656a4d515
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="password-management-frequently-asked-questions"></a><span data-ttu-id="3f45a-104">密碼管理常見問題集</span><span class="sxs-lookup"><span data-stu-id="3f45a-104">Password management frequently asked questions</span></span>

<span data-ttu-id="3f45a-105">hello 下列是一些常見問題的一切相關 toopassword 重設。</span><span class="sxs-lookup"><span data-stu-id="3f45a-105">hello following are some frequently asked questions for all things related toopassword reset.</span></span>

<span data-ttu-id="3f45a-106">如果您有關於 Azure AD 的一般問題和自助式密碼重設，未在此處找到答案，您可以要求 hello 社群協助在 hello [Azure Ad 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WindowsAzureAD)。</span><span class="sxs-lookup"><span data-stu-id="3f45a-106">If you have a general question about Azure AD and self-service password reset, that is not answered here, you can ask hello community for assistance on hello [Azure Ad forums](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WindowsAzureAD).</span></span> <span data-ttu-id="3f45a-107">Hello 社群的成員包括工程師，產品經理、 professional，Mvp 和夥伴 IT 專業人員。</span><span class="sxs-lookup"><span data-stu-id="3f45a-107">Members of hello community include Engineers, Product Managers, MVPs, and fellow IT Professionals.</span></span>

<span data-ttu-id="3f45a-108">此常見問題集分成下列各節的 hello:</span><span class="sxs-lookup"><span data-stu-id="3f45a-108">This FAQ is split into hello following sections:</span></span>

* [<span data-ttu-id="3f45a-109">**密碼重設註冊的相關問題**</span><span class="sxs-lookup"><span data-stu-id="3f45a-109">**Questions about Password Reset Registration**</span></span>](#password-reset-registration)
* [<span data-ttu-id="3f45a-110">**密碼重設的相關問題**</span><span class="sxs-lookup"><span data-stu-id="3f45a-110">**Questions about Password Reset**</span></span>](#password-reset)
* [<span data-ttu-id="3f45a-111">**密碼變更的相關問題**</span><span class="sxs-lookup"><span data-stu-id="3f45a-111">**Questions about Password Change**</span></span>](#password-change)
* [<span data-ttu-id="3f45a-112">**密碼管理報告的相關問題**</span><span class="sxs-lookup"><span data-stu-id="3f45a-112">**Questions about password management Reports**</span></span>](#password-management-reports)
* [<span data-ttu-id="3f45a-113">**密碼回寫的相關問題**</span><span class="sxs-lookup"><span data-stu-id="3f45a-113">**Questions about password writeback**</span></span>](#password-writeback)

## <a name="password-reset-registration"></a><span data-ttu-id="3f45a-114">密碼重設註冊</span><span class="sxs-lookup"><span data-stu-id="3f45a-114">Password reset registration</span></span>
* <span data-ttu-id="3f45a-115">**問：我的使用者是否可以註冊自己的密碼重設資料？**</span><span class="sxs-lookup"><span data-stu-id="3f45a-115">**Q:  Can my users register their own password reset data?**</span></span>

  > <span data-ttu-id="3f45a-116">**答：**是的只要已啟用密碼重設，且他們已獲得授權，他們可以移 toohello 密碼重設註冊入口網站則位於 http://aka.ms/ssprsetup tooregister 其驗證資訊。</span><span class="sxs-lookup"><span data-stu-id="3f45a-116">**A:** Yes, as long as password reset is enabled and they are licensed, they can go toohello Password Reset Registration portal at http://aka.ms/ssprsetup tooregister their authentication information.</span></span> <span data-ttu-id="3f45a-117">按一下 hello 設定檔 索引標籤，然後按一下 hello 註冊密碼重設選項移 toohello 存取面板 http://myapps.microsoft.com，也可以註冊使用者。</span><span class="sxs-lookup"><span data-stu-id="3f45a-117">Users can also register by going toohello access panel at http://myapps.microsoft.com, clicking hello profile tab, and clicking hello Register for Password Reset option.</span></span>
  >
  >
* <span data-ttu-id="3f45a-118">**問：我是否可以代表我的使用者定義密碼重設資料？**</span><span class="sxs-lookup"><span data-stu-id="3f45a-118">**Q:  Can I define password reset data on behalf of my users?**</span></span>

  > <span data-ttu-id="3f45a-119">**答：**是，您可以使用 Azure AD Connect，PowerShell hello [Azure 入口網站](https://portal.azure.com)，或 hello Office 管理入口網站。</span><span class="sxs-lookup"><span data-stu-id="3f45a-119">**A:** Yes, you can do so with Azure AD Connect, PowerShell, hello [Azure portal](https://portal.azure.com), or hello Office Admin portal.</span></span> <span data-ttu-id="3f45a-120">如需詳細資訊，請參閱 hello 文章[使用 Azure AD 自助式密碼重設資料](active-directory-passwords-data.md)。</span><span class="sxs-lookup"><span data-stu-id="3f45a-120">For more information, see hello article [Data used by Azure AD Self-Service Password Reset](active-directory-passwords-data.md).</span></span>
  >
  >
* <span data-ttu-id="3f45a-121">**問：我是否可以從內部部署環境同步處理安全性問題的資料？**</span><span class="sxs-lookup"><span data-stu-id="3f45a-121">**Q:  Can I synchronize data for security questions from on premises?**</span></span>

  > <span data-ttu-id="3f45a-122">**答：** 目前無法這麼做。</span><span class="sxs-lookup"><span data-stu-id="3f45a-122">**A:** This is not possible today.</span></span>
  >
  >
* <span data-ttu-id="3f45a-123">**問：我的使用者是否可以用讓其他使用者看不到資料的方式來註冊該資料？**</span><span class="sxs-lookup"><span data-stu-id="3f45a-123">**Q:  Can my users register data in such a way that other users cannot see this data?**</span></span>

  > <span data-ttu-id="3f45a-124">**答：**是的當使用者註冊使用 hello 密碼重設註冊入口網站儲存到，才會顯示由全域管理員和 hello 使用者的私用的驗證欄位的資料。</span><span class="sxs-lookup"><span data-stu-id="3f45a-124">**A:** Yes, when users register data using hello Password Reset Registration Portal it is saved into private authentication fields that are only visible by Global Administrators and hello user.</span></span>
    >
    > [!NOTE]
    > <span data-ttu-id="3f45a-125">如果**Azure 系統管理員帳戶**註冊它也會填入 hello 行動電話欄位，並會顯示其驗證電話號碼。</span><span class="sxs-lookup"><span data-stu-id="3f45a-125">If an **Azure Administrator account** registers their authentication phone number it is also populated into hello mobile phone field and is visible.</span></span>
    >
  >
  >
* <span data-ttu-id="3f45a-126">**問： 我的使用者沒有 toobe 註冊才能使用密碼重設嗎？**</span><span class="sxs-lookup"><span data-stu-id="3f45a-126">**Q:  Do my users have toobe registered before they can use password reset?**</span></span>

  > <span data-ttu-id="3f45a-127">**答：**否，如果您定義足夠驗證的資訊代表它們時，使用者不需要 tooregister。</span><span class="sxs-lookup"><span data-stu-id="3f45a-127">**A:** No, if you define enough authentication information on their behalf, users do not have tooregister.</span></span> <span data-ttu-id="3f45a-128">密碼重設運作，只要您已正確格式化 hello hello 目錄中的適當欄位中儲存的資料。</span><span class="sxs-lookup"><span data-stu-id="3f45a-128">Password reset works as long as you have properly formatted data stored in hello appropriate fields in hello directory.</span></span>
  >
  >
* <span data-ttu-id="3f45a-129">**問： 可以同步處理或代表使用者設定 hello 驗證電話、 驗證電子郵件或 備用驗證電話欄位？**</span><span class="sxs-lookup"><span data-stu-id="3f45a-129">**Q:  Can I synchronize or set hello Authentication Phone, Authentication Email or Alternate Authentication Phone fields on behalf of my users?**</span></span>

  > <span data-ttu-id="3f45a-130">**答：** 目前無法這麼做。</span><span class="sxs-lookup"><span data-stu-id="3f45a-130">**A:** This is not possible today.</span></span>
  >
  >
* <span data-ttu-id="3f45a-131">**問： 如何 hello 註冊入口網站知道哪些選項 tooshow 我的使用者？**</span><span class="sxs-lookup"><span data-stu-id="3f45a-131">**Q:  How does hello registration portal know which options tooshow my users?**</span></span>

  > <span data-ttu-id="3f45a-132">**答：** hello 密碼重設註冊入口網站，只顯示 hello 使用者啟用的選項。</span><span class="sxs-lookup"><span data-stu-id="3f45a-132">**A:** hello password reset registration portal only shows hello options that you have enabled for your users.</span></span> <span data-ttu-id="3f45a-133">下 hello 您目錄中的 設定 索引標籤的 使用者密碼重設原則 > 一節找到這些選項。比方說，這表示，如果尚未啟用安全性問題，使用者便不能 tooregister 該選項。</span><span class="sxs-lookup"><span data-stu-id="3f45a-133">These options are found under hello User Password Reset Policy section of your directory’s Configure tab. For example, this means that if you do not enable security questions, then users are not able tooregister for that option.</span></span>
  >
  >
* <span data-ttu-id="3f45a-134">**問：使用者何時會被視為已註冊？**</span><span class="sxs-lookup"><span data-stu-id="3f45a-134">**Q:  When is a user considered registered?**</span></span>

  > <span data-ttu-id="3f45a-135">**答：**使用者已註冊 SSPR 時完成註冊會視為至少 hello**方法需要 tooreset 數目**您已設定在 hello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="3f45a-135">**A:** A user is considered registered for SSPR when they have registered at least hello **Number of methods required tooreset** that you have set in hello [Azure portal](https://portal.azure.com).</span></span>
  >
  >
## <a name="password-reset"></a><span data-ttu-id="3f45a-136">密碼重設</span><span class="sxs-lookup"><span data-stu-id="3f45a-136">Password reset</span></span>
* <span data-ttu-id="3f45a-137">**問： 要我等候 tooreceive 電子郵件、 簡訊或電話，從密碼重設？**</span><span class="sxs-lookup"><span data-stu-id="3f45a-137">**Q:  How long should I wait tooreceive an email, SMS, or phone call from password reset?**</span></span>

  > <span data-ttu-id="3f45a-138">**答：**電子郵件、 簡訊和電話應該與 hello 一般案例 5-20 秒到達在一分鐘。</span><span class="sxs-lookup"><span data-stu-id="3f45a-138">**A:** Email, SMS messages, and phone calls should arrive in under one minute, with hello normal case being 5-20 seconds.</span></span>
    ><span data-ttu-id="3f45a-139">如果您沒有在此時段中收到 hello 通知：</span><span class="sxs-lookup"><span data-stu-id="3f45a-139">If you do not receive hello notification in this time frame:</span></span>
        > * <span data-ttu-id="3f45a-140">檢查您的垃圾郵件資料夾。</span><span class="sxs-lookup"><span data-stu-id="3f45a-140">Check your junk folder.</span></span>
        > * <span data-ttu-id="3f45a-141">核取 hello 號碼或電子郵件連絡是您預期一個 hello。</span><span class="sxs-lookup"><span data-stu-id="3f45a-141">Check hello number or email being contacted is hello one you expect.</span></span>
        > * <span data-ttu-id="3f45a-142">請檢查 hello 目錄中的 hello 驗證資料已正確地格式化。</span><span class="sxs-lookup"><span data-stu-id="3f45a-142">Check hello authentication data in hello directory is correctly formatted.</span></span>
                >     * <span data-ttu-id="3f45a-143">範例："+1 4255551234" 或 "user@contoso.com"</span><span class="sxs-lookup"><span data-stu-id="3f45a-143">Example: "+1 4255551234" or "user@contoso.com"</span></span>
  >
  >
* <span data-ttu-id="3f45a-144">**問：密碼重設支援哪些語言？**</span><span class="sxs-lookup"><span data-stu-id="3f45a-144">**Q:  What languages are supported by password reset?**</span></span>

  > <span data-ttu-id="3f45a-145">**答：** hello 密碼重設 UI、 簡訊及語音電話已當地語系化 hello Office 365 中支援的語言相同。</span><span class="sxs-lookup"><span data-stu-id="3f45a-145">**A:** hello password reset UI, SMS messages, and voice calls are localized in hello same languages that are supported in Office 365.</span></span>
  >
  >
* <span data-ttu-id="3f45a-146">**問： hello 密碼重設體驗的哪些部分取得品牌時設定組織商標我的目錄中的 [設定] 索引標籤嗎？**</span><span class="sxs-lookup"><span data-stu-id="3f45a-146">**Q:  What parts of hello password reset experience get branded when I set organizational branding in my directory’s configure tab?**</span></span>

  > <span data-ttu-id="3f45a-147">**答：** hello 密碼重設入口網站會顯示您組織的標誌，並可讓您 tooconfigure hello，請連絡系統管理員連結 toopoint tooa 自訂電子郵件或 URL。</span><span class="sxs-lookup"><span data-stu-id="3f45a-147">**A:** hello password reset portal shows your organizational logo and allows you tooconfigure hello Contact your administrator link toopoint tooa custom email or URL.</span></span> <span data-ttu-id="3f45a-148">密碼重設所傳送的任何電子郵件 hello 電子郵件、 hello 主體中包含您組織的標誌、 色彩、 名稱和自訂的名稱。</span><span class="sxs-lookup"><span data-stu-id="3f45a-148">Any email that gets sent by password reset includes your organization’s logo, colors, name in hello body of hello email, and customized from name.</span></span>
  >
  >
* <span data-ttu-id="3f45a-149">**問： 如何引導使用者有關在哪裡 toogo tooreset 他們的密碼？**</span><span class="sxs-lookup"><span data-stu-id="3f45a-149">**Q:  How can I educate my users about where toogo tooreset their passwords?**</span></span>

  > <span data-ttu-id="3f45a-150">**答：**您可以直接傳送使用者 toohttps://passwordreset.microsoftonline.com 或指示 tooclick hello**無法存取您的帳戶連結**任何工作或學校登入頁面上找到。</span><span class="sxs-lookup"><span data-stu-id="3f45a-150">**A:** You can send your users toohttps://passwordreset.microsoftonline.com directly, or you can instruct them tooclick hello **Can’t access your account link** found on any Work or School sign-in page.</span></span> <span data-ttu-id="3f45a-151">您也可以在進行更容易存取 tooyour 使用者發佈這些連結。</span><span class="sxs-lookup"><span data-stu-id="3f45a-151">You can also publish these links in a place easily accessible tooyour users.</span></span>
  >
  >
* <span data-ttu-id="3f45a-152">**問：我是否可以從行動裝置使用此頁面？**</span><span class="sxs-lookup"><span data-stu-id="3f45a-152">**Q:  Can I use this page from a mobile device?**</span></span>

  > <span data-ttu-id="3f45a-153">**答：** 是，此頁面可在行動裝置上運作。</span><span class="sxs-lookup"><span data-stu-id="3f45a-153">**A:** Yes, this page works on mobile devices.</span></span>
  >
  >
* <span data-ttu-id="3f45a-154">**問：當使用者重設其密碼時，您是否支援將本機 Active Directory 帳戶解除鎖定？**</span><span class="sxs-lookup"><span data-stu-id="3f45a-154">**Q:  Do you support unlocking local active directory accounts when users reset their passwords?**</span></span>

  > <span data-ttu-id="3f45a-155">**答：**是，當使用者重設其密碼並使用 Azure AD Connect 部署密碼回寫時，該使用者的帳戶會在其重設密碼時自動解除鎖定。</span><span class="sxs-lookup"><span data-stu-id="3f45a-155">**A:** Yes, when a user resets their password and password writeback has been deployed using Azure AD Connect, that user’s account is automatically unlocked when they reset their password.</span></span>
  >
  >
* <span data-ttu-id="3f45a-156">**問：我要如何將密碼重設直接整合到我使用者的桌面登入體驗？**</span><span class="sxs-lookup"><span data-stu-id="3f45a-156">**Q:  How can I integrate password reset directly into my user’s desktop sign-in experience?**</span></span>

  > <span data-ttu-id="3f45a-157">**答：**如果您是 Azure AD Premium 客戶，您可以安裝 Microsoft Identity Manager 不需額外成本，並部署 hello 在內部部署密碼重設解決方案 toomeet 這項需求。</span><span class="sxs-lookup"><span data-stu-id="3f45a-157">**A:** If you are an Azure AD Premium customer, you can install Microsoft Identity Manager at no additional cost and deploy hello on-premises password reset solution toomeet this requirement.</span></span>
  >
  >
* <span data-ttu-id="3f45a-158">**問：我是否可以針對不同的地區設定，設定不同的安全性問題？**</span><span class="sxs-lookup"><span data-stu-id="3f45a-158">**Q:  Can I set different security questions for different locales?**</span></span>

  > <span data-ttu-id="3f45a-159">**答：** 目前無法這麼做。</span><span class="sxs-lookup"><span data-stu-id="3f45a-159">**A:** This is not possible today.</span></span>
  >
  >
* <span data-ttu-id="3f45a-160">**問： 如何許多問題我們可以設定 hello 安全性問題驗證選項？**</span><span class="sxs-lookup"><span data-stu-id="3f45a-160">**Q:  How many questions can we configure for hello Security Questions authentication option?**</span></span>

  > <span data-ttu-id="3f45a-161">**答：** hello too20 自訂安全性問題，您可以設定[Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="3f45a-161">**A:** You can configure up too20 custom security questions in hello [Azure portal](https://portal.azure.com).</span></span>
  >
  >
* <span data-ttu-id="3f45a-162">**問：安全性問題的長度限制為何？**</span><span class="sxs-lookup"><span data-stu-id="3f45a-162">**Q:  How long may security questions be?**</span></span>

  > <span data-ttu-id="3f45a-163">**答：** 安全性問題的長度可以介於 3 到 200 個字元之間。</span><span class="sxs-lookup"><span data-stu-id="3f45a-163">**A:** Security questions may be between 3 and 200 characters long.</span></span>
  >
  >
* <span data-ttu-id="3f45a-164">**問： 保留時間長度可能答案 toosecurity 問題？**</span><span class="sxs-lookup"><span data-stu-id="3f45a-164">**Q:  How long may answers toosecurity questions be?**</span></span>

  > <span data-ttu-id="3f45a-165">**答：**答案可能是 3 too40 個字元長。</span><span class="sxs-lookup"><span data-stu-id="3f45a-165">**A:** Answers may be 3 too40 characters long.</span></span>
  >
  >
* <span data-ttu-id="3f45a-166">**問： 會拒絕重複回答 toosecurity 問題嗎？**</span><span class="sxs-lookup"><span data-stu-id="3f45a-166">**Q:  Are duplicate answers toosecurity questions rejected?**</span></span>

  > <span data-ttu-id="3f45a-167">**答：**是，我們會拒絕重複回答 toosecurity 問題。</span><span class="sxs-lookup"><span data-stu-id="3f45a-167">**A:** Yes, we reject duplicate answers toosecurity questions.</span></span>
  >
  >
* <span data-ttu-id="3f45a-168">**問： 可能是使用者在暫存 hello 相同的安全性問題一次以上嗎？**</span><span class="sxs-lookup"><span data-stu-id="3f45a-168">**Q:  May a user register hello same security question more than once?**</span></span>

  > <span data-ttu-id="3f45a-169">**答：**否，使用者註冊一旦特定的問題，便不可以再次註冊該問題。</span><span class="sxs-lookup"><span data-stu-id="3f45a-169">**A:** No, once a user registers a particular question, they may not register for that question a second time.</span></span>
  >
  >
* <span data-ttu-id="3f45a-170">**問： 是否可能 tooset 最低限制的註冊和重設的安全性問題？**</span><span class="sxs-lookup"><span data-stu-id="3f45a-170">**Q:  Is it possible tooset a minimum limit of security questions for registration and reset?**</span></span>

  > <span data-ttu-id="3f45a-171">**答：** 是，可以針對註冊設定一個限制，針對重設設定另一個限制。</span><span class="sxs-lookup"><span data-stu-id="3f45a-171">**A:** Yes, one limit can be set for registration and another for reset.</span></span> <span data-ttu-id="3f45a-172">註冊可能需要 3-5 個安全性問題，重設也需要 3-5 個安全性問題。</span><span class="sxs-lookup"><span data-stu-id="3f45a-172">3-5 security questions may be required for registration and 3-5 may be required for reset.</span></span>
  >
  >
* <span data-ttu-id="3f45a-173">**問： 如果使用者已註冊多個 hello 問題需要 tooreset 數目上限，如何選取安全性問題重設期間？**</span><span class="sxs-lookup"><span data-stu-id="3f45a-173">**Q:  If a user has registered more than hello maximum number of questions required tooreset, how are security questions selected during reset?**</span></span>

  > <span data-ttu-id="3f45a-174">**答：** N 安全性問題中隨機選取超出 hello 問題總數，使用者所註冊的其中 N 是 hello**問題需要 tooreset 數目**。</span><span class="sxs-lookup"><span data-stu-id="3f45a-174">**A:** N security questions are selected at random out of hello total number of questions a user has registered for, where N is hello **Number of questions required tooreset**.</span></span> <span data-ttu-id="3f45a-175">例如，如果使用者具有 5 個安全性問題註冊，但只有 3 需要的 tooreset，hello 5 的 3 會隨機選取，並顯示在重設。</span><span class="sxs-lookup"><span data-stu-id="3f45a-175">For example, if a user has 5 security questions registered, but only 3 are required tooreset, 3 of hello 5 are selected randomly and presented at reset.</span></span> <span data-ttu-id="3f45a-176">如果 hello 使用者 hello 答案 toohello 問題錯誤，又重新出現 hello 選取程序 tooprevent 問題被破解。</span><span class="sxs-lookup"><span data-stu-id="3f45a-176">If hello user gets hello answers toohello questions wrong, hello selection process reoccurs tooprevent question hammering.</span></span>
  >
  >
* <span data-ttu-id="3f45a-177">**問：您是否禁止使用者在短時間內嘗試多次密碼重設？**</span><span class="sxs-lookup"><span data-stu-id="3f45a-177">**Q:  Do you prevent users from attempting password reset many times in a short time period?**</span></span>

  > <span data-ttu-id="3f45a-178">**答：**是，有密碼重設 tooprotect 免遭不當使用內建的安全性功能。</span><span class="sxs-lookup"><span data-stu-id="3f45a-178">**A:** Yes, there are security features built into password reset tooprotect from misuse.</span></span> <span data-ttu-id="3f45a-179">使用者在一個小時之內只能嘗試 5 次密碼重設，否則會鎖定 24 小時。</span><span class="sxs-lookup"><span data-stu-id="3f45a-179">Users may only try 5 password reset attempts within an hour before being locked out for 24 hours.</span></span> <span data-ttu-id="3f45a-180">使用者只能嘗試 toovalidate 電話號碼 5 次，一小時就會被鎖定 24 小時內。</span><span class="sxs-lookup"><span data-stu-id="3f45a-180">Users may only try toovalidate a phone number 5 times within an hour before being locked out for 24 hours.</span></span> <span data-ttu-id="3f45a-181">使用者在一個小時之內只能嘗試單一驗證方法 5 次，否則會鎖定 24 小時。</span><span class="sxs-lookup"><span data-stu-id="3f45a-181">Users may only try a single authentication method 5 times within an hour before being locked out for 24 hours.</span></span>
  >
  >
* <span data-ttu-id="3f45a-182">**問： 為何 hello 電子郵件和簡訊的單次密碼有效？**</span><span class="sxs-lookup"><span data-stu-id="3f45a-182">**Q:  For how long are hello email and SMS one-time passcode valid?**</span></span>

  > <span data-ttu-id="3f45a-183">**答：** hello 密碼重設工作階段存留期為 105 分鐘。</span><span class="sxs-lookup"><span data-stu-id="3f45a-183">**A:** hello session lifetime for password reset is 105 minutes.</span></span> <span data-ttu-id="3f45a-184">從 hello hello 開頭密碼重設作業、 hello 使用者 105 分鐘 tooreset 他們的密碼。</span><span class="sxs-lookup"><span data-stu-id="3f45a-184">From hello beginning of hello password reset operation, hello user has 105 minutes tooreset their password.</span></span> <span data-ttu-id="3f45a-185">hello 電子郵件和簡訊的單次密碼是無效的這段時間之後。</span><span class="sxs-lookup"><span data-stu-id="3f45a-185">hello email and SMS one-time passcode are invalid after this time period expires.</span></span>
  >
  >

## <a name="password-change"></a><span data-ttu-id="3f45a-186">密碼變更</span><span class="sxs-lookup"><span data-stu-id="3f45a-186">Password change</span></span>
* <span data-ttu-id="3f45a-187">**問： 我的使用者應 toochange 他們的密碼？**</span><span class="sxs-lookup"><span data-stu-id="3f45a-187">**Q:  Where should my users go toochange their passwords?**</span></span>

  > <span data-ttu-id="3f45a-188">**答：**使用者可能會變更其密碼任何位置看到他們的設定檔圖片或圖示 (如同在 hello 右上角的其[Office 365](https://portal.office.com)或[存取面板](https://myapps.microsoft.com)發生。</span><span class="sxs-lookup"><span data-stu-id="3f45a-188">**A:** Users may change their passwords anywhere they see their profile picture or icon (like in hello upper right corner of their [Office 365](https://portal.office.com) or [Access Panel](https://myapps.microsoft.com) experiences.</span></span> <span data-ttu-id="3f45a-189">使用者可能會變更其密碼，從 hello[存取面板設定檔頁面](https://account.activedirectory.windowsazure.com/r#/profile)。</span><span class="sxs-lookup"><span data-stu-id="3f45a-189">Users may change their passwords from hello [Access Panel profile page](https://account.activedirectory.windowsazure.com/r#/profile).</span></span> <span data-ttu-id="3f45a-190">使用者也可能要求 toochange 他們的密碼會自動在 hello Azure AD 登入畫面，如果他們的密碼已過期。</span><span class="sxs-lookup"><span data-stu-id="3f45a-190">Users may also be asked toochange their passwords automatically at hello Azure AD sign-in screen if their passwords have expired.</span></span> <span data-ttu-id="3f45a-191">最後，使用者可能瀏覽 toohello [Azure AD 密碼變更入口網站](https://account.activedirectory.windowsazure.com/ChangePassword.aspx)直接如果他們想 toochange 他們的密碼。</span><span class="sxs-lookup"><span data-stu-id="3f45a-191">Finally, users may navigate toohello [Azure AD Password Change Portal](https://account.activedirectory.windowsazure.com/ChangePassword.aspx) directly if they wish toochange their passwords.</span></span>
  >
  >
* <span data-ttu-id="3f45a-192">**問： 是否可以我的使用者通知的 hello Office 入口網站在內部部署密碼到期時？**</span><span class="sxs-lookup"><span data-stu-id="3f45a-192">**Q:  Can my users be notified in hello Office Portal when their on-premises password expires?**</span></span>

  > <span data-ttu-id="3f45a-193">**答：**這是可能今天如果您使用 ADFS hello 遵循指示：[傳送密碼原則宣告使用 ADFS](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configure-ad-fs-to-send-password-expiry-claims?f=255&MSPPError=-2147217396)。</span><span class="sxs-lookup"><span data-stu-id="3f45a-193">**A:** This is possible today if you are using ADFS by following hello instructions here: [Sending Password Policy Claims with ADFS](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configure-ad-fs-to-send-password-expiry-claims?f=255&MSPPError=-2147217396).</span></span> <span data-ttu-id="3f45a-194">如果您使用密碼雜湊同步處理，則目前還不可能。</span><span class="sxs-lookup"><span data-stu-id="3f45a-194">If you are using password hash synchronization, this is not possible today.</span></span> <span data-ttu-id="3f45a-195">這是因為我們無法同步處理從內部部署密碼原則，所以不讓我們 toopost 到期通知 toocloud 遇到。</span><span class="sxs-lookup"><span data-stu-id="3f45a-195">This is because we do not sync password policies from on-premises, so it is not possible for us toopost expiry notifications toocloud experiences.</span></span> <span data-ttu-id="3f45a-196">在任一情況下，也可能會太[通知的使用者其密碼即將使用 PowerShell tooexpire](https://social.technet.microsoft.com/wiki/contents/articles/23313.notify-active-directory-users-about-password-expiry-using-powershell.aspx)。</span><span class="sxs-lookup"><span data-stu-id="3f45a-196">In either case, it is also possible too[notify users whose passwords are about tooexpire by using PowerShell](https://social.technet.microsoft.com/wiki/contents/articles/23313.notify-active-directory-users-about-password-expiry-using-powershell.aspx).</span></span>
  >
  >

## <a name="password-management-reports"></a><span data-ttu-id="3f45a-197">密碼管理報告</span><span class="sxs-lookup"><span data-stu-id="3f45a-197">Password management reports</span></span>
* <span data-ttu-id="3f45a-198">**問： 如何花費時間的總 hello 密碼管理報表上的資料 tooshow？**</span><span class="sxs-lookup"><span data-stu-id="3f45a-198">**Q:  How long does it take for data tooshow up on hello password management reports?**</span></span>

  > <span data-ttu-id="3f45a-199">**答：**資料應該在 hello 密碼管理報表上會出現在 5-10 分鐘內。</span><span class="sxs-lookup"><span data-stu-id="3f45a-199">**A:** Data should appear on hello password management reports within 5-10 minutes.</span></span> <span data-ttu-id="3f45a-200">它可能佔用 tooan 小時 tooappear 某些執行個體。</span><span class="sxs-lookup"><span data-stu-id="3f45a-200">It some instances it may take up tooan hour tooappear.</span></span>
  >
  >
* <span data-ttu-id="3f45a-201">**問： 如何可以篩選 hello 密碼管理報表？**</span><span class="sxs-lookup"><span data-stu-id="3f45a-201">**Q:  How can I filter hello password management reports?**</span></span>

  > <span data-ttu-id="3f45a-202">**答：**您可以按一下 hello hello 報表頂端附近的 hello 資料行標籤的 hello 小型的放大鏡 toohello 最右側，以篩選 hello 密碼管理報表。</span><span class="sxs-lookup"><span data-stu-id="3f45a-202">**A:** You can filter hello password management reports by clicking hello small magnifying glass toohello extreme right of hello column labels, near hello top of hello report.</span></span> <span data-ttu-id="3f45a-203">如果您想 toodo 更複雜的篩選，您可以下載 hello 報表 tooexcel 並建立樞紐分析表。</span><span class="sxs-lookup"><span data-stu-id="3f45a-203">If you want toodo richer filtering, you can download hello report tooexcel and create a pivot table.</span></span>
  >
  >
* <span data-ttu-id="3f45a-204">**問： 什麼是 hello 最大事件數目會儲存在 hello 密碼管理報表？**</span><span class="sxs-lookup"><span data-stu-id="3f45a-204">**Q: What is hello maximum number of events are stored in hello password management reports?**</span></span>

  > <span data-ttu-id="3f45a-205">**答：**向上 too75，000 密碼重設或密碼重設註冊事件會儲存在 hello 密碼管理報表跨越備份 too30 天。</span><span class="sxs-lookup"><span data-stu-id="3f45a-205">**A:** Up too75,000 password reset or password reset registration events are stored in hello password management reports, spanning back up too30 days.</span></span>  <span data-ttu-id="3f45a-206">我們正在 tooexpand 這個數字 tooinclude 更多的事件。</span><span class="sxs-lookup"><span data-stu-id="3f45a-206">We are working tooexpand this number tooinclude more events.</span></span>
  >
  >
* <span data-ttu-id="3f45a-207">**問： 如何久 hello 密碼管理報表怎麼做？**</span><span class="sxs-lookup"><span data-stu-id="3f45a-207">**Q:  How far back do hello password management reports go?**</span></span>

  > <span data-ttu-id="3f45a-208">**答：** hello 密碼管理報告 hello 中發生的過去 30 天內顯示作業。</span><span class="sxs-lookup"><span data-stu-id="3f45a-208">**A:** hello password management reports show operations occurring within hello last 30 days.</span></span> <span data-ttu-id="3f45a-209">現在，如果您需要 tooarchive 這項資料，您可以定期下載 hello 報表並將它們儲存在不同的位置。</span><span class="sxs-lookup"><span data-stu-id="3f45a-209">For now, if you need tooarchive this data, you can download hello reports periodically and save them in a separate location.</span></span>
  >
  >
* <span data-ttu-id="3f45a-210">**問： 是否有可能會出現在 hello 密碼管理報表的資料列的數目上限？**</span><span class="sxs-lookup"><span data-stu-id="3f45a-210">**Q:  Is there a maximum number of rows that can appear on hello password management reports?**</span></span>

  > <span data-ttu-id="3f45a-211">**答：**是，75000 資料列最多可能會出現在 hello 密碼管理報表，其中是否顯示在 hello UI 或透過下載。</span><span class="sxs-lookup"><span data-stu-id="3f45a-211">**A:** Yes, a maximum of 75,000 rows may appear on either of hello password management reports, whether they are being shown in hello UI or being downloaded.</span></span>
  >
  >
* <span data-ttu-id="3f45a-212">**問： 是否有應用程式開發介面 tooaccess hello 密碼重設或註冊報表資料？**</span><span class="sxs-lookup"><span data-stu-id="3f45a-212">**Q:  Is there an API tooaccess hello password reset or registration reporting data?**</span></span>

  > <span data-ttu-id="3f45a-213">**答：** [是]，請參閱 hello 下列文件 toolearn 如何存取 hello 密碼重設報表的資料流。</span><span class="sxs-lookup"><span data-stu-id="3f45a-213">**A:** Yes, see hello following documentation toolearn how you can access hello password reset reporting data stream.</span></span>  <span data-ttu-id="3f45a-214">[了解如何 tooaccess 密碼重設報告事件以程式設計方式](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent)。</span><span class="sxs-lookup"><span data-stu-id="3f45a-214">[Learn how tooaccess password reset reporting events programmatically](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent).</span></span>
  >
  >

## <a name="password-writeback"></a><span data-ttu-id="3f45a-215">密碼回寫</span><span class="sxs-lookup"><span data-stu-id="3f45a-215">Password writeback</span></span>
* <span data-ttu-id="3f45a-216">**問： 密碼回寫如何 hello 幕後運作？**</span><span class="sxs-lookup"><span data-stu-id="3f45a-216">**Q:  How does password writeback work behind hello scenes?**</span></span>

  > <span data-ttu-id="3f45a-217">**答：**看到[密碼回寫的運作方式](active-directory-passwords-writeback.md)進行說明內容後，當您啟用密碼回寫，以及資料流動的方式透過 hello 系統回到內部部署環境。</span><span class="sxs-lookup"><span data-stu-id="3f45a-217">**A:** See [How password writeback works](active-directory-passwords-writeback.md) for an explanation of what happens when you enable password writeback, and how data flows through hello system back into your on-premises environment.</span></span>
  >
  >
* <span data-ttu-id="3f45a-218">**問： 如何長密碼回寫會採用 toowork？是否有像是使用密碼雜湊同步處理的同步處理延遲？**</span><span class="sxs-lookup"><span data-stu-id="3f45a-218">**Q:  How long does password writeback take toowork?  Is there a synchronization delay like with password hash sync?**</span></span>

  > <span data-ttu-id="3f45a-219">**答：**密碼回寫會立即進行。</span><span class="sxs-lookup"><span data-stu-id="3f45a-219">**A:** Password writeback is instant.</span></span> <span data-ttu-id="3f45a-220">它是同步管線，基本上的運作與密碼雜湊同步處理不同。</span><span class="sxs-lookup"><span data-stu-id="3f45a-220">It is a synchronous pipeline that works fundamentally differently than password hash synchronization.</span></span> <span data-ttu-id="3f45a-221">密碼回寫可讓的使用者 tooget 即時意見 hello 成功的密碼重設或變更作業。</span><span class="sxs-lookup"><span data-stu-id="3f45a-221">Password writeback allows users tooget real-time feedback about hello success of their password reset or change operation.</span></span> <span data-ttu-id="3f45a-222">hello 的密碼成功回寫的平均時間不超過 500 毫秒。</span><span class="sxs-lookup"><span data-stu-id="3f45a-222">hello average time for a successful writeback of a password is under 500 ms.</span></span>
  >
  >
* <span data-ttu-id="3f45a-223">**問︰如果我的內部部署帳戶已停用，這對我的雲端帳戶/存取有何影響？**</span><span class="sxs-lookup"><span data-stu-id="3f45a-223">**Q:  If my on-premises account is disabled, how is my cloud account/access affected?**</span></span>

  > <span data-ttu-id="3f45a-224">**答：**已停用您在內部部署的識別碼，就也在 hello 下一個同步處理間隔透過 AAD Connect byt 預設停用識別碼/存取您雲端這是每隔 30 分鐘。</span><span class="sxs-lookup"><span data-stu-id="3f45a-224">**A:** If your on-premises ID is disabled, your cloud ID/access will also be disabled at hello next sync interval via AAD Connect byt default this is every 30 minutes.</span></span>
  >
  >
* <span data-ttu-id="3f45a-225">**問： 如果我在內部部署的帳戶由內部部署 Active Directory 密碼原則限制，沒有 SSPR 遵守此原則時變更 hello 密碼嗎？**</span><span class="sxs-lookup"><span data-stu-id="3f45a-225">**Q:  If my on-premises account is constrained by an on-premises Active Directory password policy, does SSPR obey this policy when I change hello password?**</span></span>

  > <span data-ttu-id="3f45a-226">**答：** SSPR 依賴的是，並遵守 hello 內部部署 AD 密碼原則，包括一般的 AD 網域密碼原則，以及任何已定義更細緻的密碼原則目標 tooa 指定使用者。</span><span class="sxs-lookup"><span data-stu-id="3f45a-226">**A:** Yes, SSPR relies on and abides by hello on-premises AD password policy, including typical AD domain password policy, as well as any defined fine grained password policies targeted tooa given user.</span></span>
  >
  >
* <span data-ttu-id="3f45a-227">**問：密碼回寫適用於哪些類型的帳戶？**</span><span class="sxs-lookup"><span data-stu-id="3f45a-227">**Q:  What types of accounts does password writeback work for?**</span></span>

  > <span data-ttu-id="3f45a-228">**答：**密碼回寫適用於「同盟」和「密碼雜湊同步」使用者。</span><span class="sxs-lookup"><span data-stu-id="3f45a-228">**A:** Password writeback works for Federated and Password Hash Synchronized users.</span></span>
  >
  >
* <span data-ttu-id="3f45a-229">**問：密碼回寫是否會強制執行我的網域密碼原則？**</span><span class="sxs-lookup"><span data-stu-id="3f45a-229">**Q:  Does password writeback enforce my domain’s password policies?**</span></span>

  > <span data-ttu-id="3f45a-230">**答：**是，密碼回寫會強制執行密碼使用期限、歷程記錄、複雜度、篩選及任何其他您可能在本機網域中的密碼上適當加諸的限制。</span><span class="sxs-lookup"><span data-stu-id="3f45a-230">**A:** Yes, password writeback enforces password age, history, complexity, filters, and any other restriction you may put in place on passwords in your local domain.</span></span>
  >
  >
* <span data-ttu-id="3f45a-231">**問：密碼回寫是否安全？我要如何確定不會受到駭客入侵？**</span><span class="sxs-lookup"><span data-stu-id="3f45a-231">**Q:  Is password writeback secure?  How can I be sure I won’t get hacked?**</span></span>

  > <span data-ttu-id="3f45a-232">**答：**是，密碼回寫很安全。</span><span class="sxs-lookup"><span data-stu-id="3f45a-232">**A:** Yes, password writeback is secure.</span></span> <span data-ttu-id="3f45a-233">hello 密碼回寫服務所實作的 tooread 深入了解 hello 四個層級的安全性，請簽出 hello[密碼回寫安全性模型](active-directory-passwords-writeback.md#password-writeback-security-model)密碼回寫的運作方式 > 一節。</span><span class="sxs-lookup"><span data-stu-id="3f45a-233">tooread more about hello four layers of security implemented by hello password writeback service, check out hello [Password writeback security model](active-directory-passwords-writeback.md#password-writeback-security-model) section in How password writeback works.</span></span>
  >
  >

## <a name="next-steps"></a><span data-ttu-id="3f45a-234">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3f45a-234">Next steps</span></span>

<span data-ttu-id="3f45a-235">hello 下列連結提供有關密碼重設使用 Azure AD 的其他資訊</span><span class="sxs-lookup"><span data-stu-id="3f45a-235">hello following links provide additional information regarding password reset using Azure AD</span></span>

* <span data-ttu-id="3f45a-236">[**快速入門**](active-directory-passwords-getting-started.md) - 開始執行 Azure AD 自助式密碼管理</span><span class="sxs-lookup"><span data-stu-id="3f45a-236">[**Quick Start**](active-directory-passwords-getting-started.md) - Get up and running with Azure AD self service password management</span></span> 
* <span data-ttu-id="3f45a-237">[**授權**](active-directory-passwords-licensing.md) - 設定 Azure AD 授權</span><span class="sxs-lookup"><span data-stu-id="3f45a-237">[**Licensing**](active-directory-passwords-licensing.md) - Configure your Azure AD Licensing</span></span>
* <span data-ttu-id="3f45a-238">[**資料**](active-directory-passwords-data.md) -了解所需的 hello 資料及如何使用密碼管理</span><span class="sxs-lookup"><span data-stu-id="3f45a-238">[**Data**](active-directory-passwords-data.md) - Understand hello data that is required and how it is used for password management</span></span>
* <span data-ttu-id="3f45a-239">[**首度發行**](active-directory-passwords-best-practices.md) -計劃和部署 SSPR tooyour 使用者 hello 指引，請參閱</span><span class="sxs-lookup"><span data-stu-id="3f45a-239">[**Rollout**](active-directory-passwords-best-practices.md) - Plan and deploy SSPR tooyour users using hello guidance found here</span></span>
* <span data-ttu-id="3f45a-240">[**自訂**](active-directory-passwords-customize.md) -自訂的 hello SSPR 體驗您的公司 hello 外觀與風格。</span><span class="sxs-lookup"><span data-stu-id="3f45a-240">[**Customize**](active-directory-passwords-customize.md) - Customize hello look and feel of hello SSPR experience for your company.</span></span>
* <span data-ttu-id="3f45a-241">[**報告**](active-directory-passwords-reporting.md) - 探索您的使用者是否、何時、何地存取 SSPR 功能</span><span class="sxs-lookup"><span data-stu-id="3f45a-241">[**Reporting**](active-directory-passwords-reporting.md) - Discover if, when, and where your users are accessing SSPR functionality</span></span>
* <span data-ttu-id="3f45a-242">[**原則**](active-directory-passwords-policy.md) - 了解並設定 Azure AD 密碼原則</span><span class="sxs-lookup"><span data-stu-id="3f45a-242">[**Policy**](active-directory-passwords-policy.md) - Understand and set Azure AD password policies</span></span>
* <span data-ttu-id="3f45a-243">[**密碼回寫**](active-directory-passwords-writeback.md) - 密碼回寫如何使用您的內部部署目錄</span><span class="sxs-lookup"><span data-stu-id="3f45a-243">[**Password Writeback**](active-directory-passwords-writeback.md) - How does password writeback work with your on-premises directory</span></span>
* <span data-ttu-id="3f45a-244">[**技術的深入探討**](active-directory-passwords-how-it-works.md) -hello 帘 toounderstand 後方移它的運作方式</span><span class="sxs-lookup"><span data-stu-id="3f45a-244">[**Technical Deep Dive**](active-directory-passwords-how-it-works.md) - Go behind hello curtain toounderstand how it works</span></span>
* <span data-ttu-id="3f45a-245">[**疑難排解**](active-directory-passwords-troubleshoot.md) -了解如何 tooresolve 常見問題，我們會看到與 SSPR</span><span class="sxs-lookup"><span data-stu-id="3f45a-245">[**Troubleshoot**](active-directory-passwords-troubleshoot.md) - Learn how tooresolve common issues that we see with SSPR</span></span>
