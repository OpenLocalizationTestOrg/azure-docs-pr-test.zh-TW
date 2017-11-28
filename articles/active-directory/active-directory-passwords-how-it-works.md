---
title: "深入探討︰Azure AD SSPR | Microsoft Docs"
description: "Azure AD 自助式密碼重設深入探討"
services: active-directory
keywords: 
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 618c5908-5bf6-4f0d-bf88-5168dfb28a88
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: c177192bbe69d179a25d174b06a0813ec28e2615
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="self-service-password-reset-in-azure-ad-deep-dive"></a><span data-ttu-id="e6aaf-103">Azure AD 中的自助式密碼重設深入探討</span><span class="sxs-lookup"><span data-stu-id="e6aaf-103">Self-service password reset in Azure AD deep dive</span></span>

<span data-ttu-id="e6aaf-104">SSPR 的運作方式</span><span class="sxs-lookup"><span data-stu-id="e6aaf-104">How does SSPR work?</span></span> <span data-ttu-id="e6aaf-105">該選項什麼 hello 介面中？</span><span class="sxs-lookup"><span data-stu-id="e6aaf-105">What does that option mean in hello interface?</span></span> <span data-ttu-id="e6aaf-106">繼續閱讀 toofind 深入了解 Azure AD 自助式密碼重設。</span><span class="sxs-lookup"><span data-stu-id="e6aaf-106">Continue reading toofind out more about Azure AD self-service password reset.</span></span>

## <a name="how-does-hello-password-reset-portal-work"></a><span data-ttu-id="e6aaf-107">如何 hello 密碼重設入口網站的工作</span><span class="sxs-lookup"><span data-stu-id="e6aaf-107">How does hello password reset portal work</span></span>

<span data-ttu-id="e6aaf-108">當使用者巡覽 toohello 密碼重設入口網站時，工作流程會開始 toodetermine:</span><span class="sxs-lookup"><span data-stu-id="e6aaf-108">When a user navigates toohello password reset portal, a workflow is kicked off toodetermine:</span></span>

   * <span data-ttu-id="e6aaf-109">如何當地語系化 hello 頁面？</span><span class="sxs-lookup"><span data-stu-id="e6aaf-109">How should hello page be localized?</span></span>
   * <span data-ttu-id="e6aaf-110">是有效的 hello 使用者帳戶？</span><span class="sxs-lookup"><span data-stu-id="e6aaf-110">Is hello user account valid?</span></span>
   * <span data-ttu-id="e6aaf-111">Hello 使用者並屬於組織為何？</span><span class="sxs-lookup"><span data-stu-id="e6aaf-111">What organization does hello user belong to?</span></span>
   * <span data-ttu-id="e6aaf-112">其中被管理 hello 使用者的密碼嗎？</span><span class="sxs-lookup"><span data-stu-id="e6aaf-112">Where hello user’s password is managed?</span></span>
   * <span data-ttu-id="e6aaf-113">是 hello 使用者授權的 toouse hello 功能？</span><span class="sxs-lookup"><span data-stu-id="e6aaf-113">Is hello user licensed toouse hello feature?</span></span>


<span data-ttu-id="e6aaf-114">閱讀下列有關 hello hello 密碼重設頁面背後的邏輯 toolearn 的 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="e6aaf-114">Read through hello steps below toolearn about hello logic behind hello password reset page.</span></span>

1. <span data-ttu-id="e6aaf-115">使用者按一下 hello 無法存取您帳戶的連結，或直接進入太[https://passwordreset.microsoftonline.com](https://passwordreset.microsoftonline.com)。</span><span class="sxs-lookup"><span data-stu-id="e6aaf-115">User clicks hello Can’t access your account link or goes directly too[https://passwordreset.microsoftonline.com](https://passwordreset.microsoftonline.com).</span></span>
2. <span data-ttu-id="e6aaf-116">基礎上 hello 瀏覽器地區設定 hello hello 適當的語言呈現體驗。</span><span class="sxs-lookup"><span data-stu-id="e6aaf-116">Based on hello browser locale hello experience is rendered in hello appropriate language.</span></span> <span data-ttu-id="e6aaf-117">hello 密碼重設體驗已當地語系化成 Office 365 支援 hello 相同的語言。</span><span class="sxs-lookup"><span data-stu-id="e6aaf-117">hello password reset experience is localized into hello same languages as Office 365 supports.</span></span>
3. <span data-ttu-id="e6aaf-118">使用者輸入使用者識別碼並通過文字驗證。</span><span class="sxs-lookup"><span data-stu-id="e6aaf-118">User enters a user id and passes a captcha.</span></span>
4. <span data-ttu-id="e6aaf-119">Azure AD 會驗證 hello 使用者是否能 toouse 執行 hello 下列這項功能：</span><span class="sxs-lookup"><span data-stu-id="e6aaf-119">Azure AD verifies if hello user is able toouse this feature by doing hello following:</span></span>
   * <span data-ttu-id="e6aaf-120">會檢查該 hello 使用者已啟用這項功能並指派的 Azure AD 授權。</span><span class="sxs-lookup"><span data-stu-id="e6aaf-120">Checks that hello user has this feature enabled and an Azure AD license assigned.</span></span>
     * <span data-ttu-id="e6aaf-121">Hello 使用者並沒有啟用這項功能或將授權指派，hello 使用者是否要求 toocontact 其系統管理員 tooreset 他們的密碼。</span><span class="sxs-lookup"><span data-stu-id="e6aaf-121">If hello user does not have this feature enabled or a license assigned, hello user is asked toocontact their administrator tooreset their password.</span></span>
   * <span data-ttu-id="e6aaf-122">會檢查該 hello 使用者已在系統管理員原則根據帳戶中定義的 hello 正確驗證題目資料。</span><span class="sxs-lookup"><span data-stu-id="e6aaf-122">Checks that hello user has hello right challenge data defined on their account in accordance with administrator policy.</span></span>
     * <span data-ttu-id="e6aaf-123">如果原則要求只有一個挑戰，則會確保該 hello 使用者已定義至少一個 hello hello 系統管理員原則啟用的驗證題目 hello 適當的資料。</span><span class="sxs-lookup"><span data-stu-id="e6aaf-123">If policy requires only one challenge, then it is ensured that hello user has hello appropriate data defined for at least one of hello challenges enabled by hello administrator policy.</span></span>
       * <span data-ttu-id="e6aaf-124">如果 hello 使用者未設定，然後 hello 使用者是建議使用的 toocontact 其系統管理員 tooreset 他們的密碼。</span><span class="sxs-lookup"><span data-stu-id="e6aaf-124">If hello user is not configured, then hello user is advised toocontact their administrator tooreset their password.</span></span>
     * <span data-ttu-id="e6aaf-125">如果 hello 原則需要兩個驗證題目，則會確保該 hello 使用者已針對至少兩個 hello hello 系統管理員原則啟用的驗證題目，定義 hello 適當資料。</span><span class="sxs-lookup"><span data-stu-id="e6aaf-125">If hello policy requires two challenges, then it is ensured that hello user has hello appropriate data defined for at least two of hello challenges enabled by hello administrator policy.</span></span>
       * <span data-ttu-id="e6aaf-126">如果未設定 hello 使用者，則我們 hello 使用者是建議使用的 toocontact 其系統管理員 tooreset 他們的密碼。</span><span class="sxs-lookup"><span data-stu-id="e6aaf-126">If hello user is not configured, then we hello user is advised toocontact their administrator tooreset their password.</span></span>
   * <span data-ttu-id="e6aaf-127">檢查是否 hello 使用者的密碼由內部部署管理 （同盟或密碼雜湊同步處理）。</span><span class="sxs-lookup"><span data-stu-id="e6aaf-127">Checks if hello user’s password is managed on premises (federated or password hash synchronized).</span></span>
     * <span data-ttu-id="e6aaf-128">如果已部署回寫 hello 使用者的密碼由內部部署管理，hello 使用者允許 tooproceed tooauthenticate 和重設其密碼。</span><span class="sxs-lookup"><span data-stu-id="e6aaf-128">If writeback is deployed and hello user’s password is managed on premises, then hello user is allowed tooproceed tooauthenticate and reset their password.</span></span>
     * <span data-ttu-id="e6aaf-129">如果未部署回寫，而且 hello 使用者的密碼由內部部署管理，則 hello 使用者是要求其系統管理員 tooreset toocontact 他們的密碼。</span><span class="sxs-lookup"><span data-stu-id="e6aaf-129">If writeback is not deployed and hello user’s password is managed on premises, then hello user is asked toocontact their administrator tooreset their password.</span></span>
5. <span data-ttu-id="e6aaf-130">如果它由決定該 hello 使用者 toosuccessfully 重設其密碼，然後會引導 hello 使用者 hello 重設程序完成。</span><span class="sxs-lookup"><span data-stu-id="e6aaf-130">If it is determined that hello user is able toosuccessfully reset their password, then hello user is guided through hello reset process.</span></span>

## <a name="authentication-methods"></a><span data-ttu-id="e6aaf-131">驗證方法</span><span class="sxs-lookup"><span data-stu-id="e6aaf-131">Authentication methods</span></span>

<span data-ttu-id="e6aaf-132">如果已啟用自助式密碼重設 (SSPR)，您必須選取至少一個 hello 下列驗證方法的選項。</span><span class="sxs-lookup"><span data-stu-id="e6aaf-132">If Self-Service Password Reset (SSPR) is enabled, you must select at least one of hello following options for authentication methods.</span></span> <span data-ttu-id="e6aaf-133">我們強烈建議選擇至少兩個驗證方法，您的使用者才有更大的彈性。</span><span class="sxs-lookup"><span data-stu-id="e6aaf-133">We highly recommend choosing at least two authentication methods so that your users have more flexibility.</span></span>

* <span data-ttu-id="e6aaf-134">電子郵件</span><span class="sxs-lookup"><span data-stu-id="e6aaf-134">Email</span></span>
* <span data-ttu-id="e6aaf-135">行動電話</span><span class="sxs-lookup"><span data-stu-id="e6aaf-135">Mobile Phone</span></span>
* <span data-ttu-id="e6aaf-136">辦公室電話</span><span class="sxs-lookup"><span data-stu-id="e6aaf-136">Office Phone</span></span>
* <span data-ttu-id="e6aaf-137">安全性問題</span><span class="sxs-lookup"><span data-stu-id="e6aaf-137">Security Questions</span></span>

### <a name="what-fields-are-used-in-hello-directory-for-authentication-data"></a><span data-ttu-id="e6aaf-138">哪些欄位用於 hello 目錄中驗證資料</span><span class="sxs-lookup"><span data-stu-id="e6aaf-138">What fields are used in hello directory for authentication data</span></span>

* <span data-ttu-id="e6aaf-139">辦公室電話對應 tooOffice 電話</span><span class="sxs-lookup"><span data-stu-id="e6aaf-139">Office Phone corresponds tooOffice Phone</span></span>
    * <span data-ttu-id="e6aaf-140">使用者會無法 tooset 這欄位本身必須由系統管理員</span><span class="sxs-lookup"><span data-stu-id="e6aaf-140">Users are unable tooset this field themselves it must be defined by an administrator</span></span>
* <span data-ttu-id="e6aaf-141">行動電話對應 tooeither （不可見） 的驗證電話或行動電話 （可見）</span><span class="sxs-lookup"><span data-stu-id="e6aaf-141">Mobile Phone corresponds tooeither Authentication Phone (not publicly visible) or Mobile Phone (publicly visible)</span></span>
    * <span data-ttu-id="e6aaf-142">hello 服務驗證電話會首先尋找，然後就會回到 tooMobile 電話如果不存在</span><span class="sxs-lookup"><span data-stu-id="e6aaf-142">hello service looks for Authentication Phone first, then falls back tooMobile Phone if not present</span></span>
* <span data-ttu-id="e6aaf-143">替代電子郵件地址對應 tooeither 驗證電子郵件 （不可見） 或替代電子郵件</span><span class="sxs-lookup"><span data-stu-id="e6aaf-143">Alternate Email Address corresponds tooeither Authentication Email (not publicly visible) or Alternate Email</span></span>
    * <span data-ttu-id="e6aaf-144">hello 服務驗證電子郵件的第一次，看起來則會失敗後 tooAlternate 電子郵件</span><span class="sxs-lookup"><span data-stu-id="e6aaf-144">hello service looks for Authentication Email first, then fails back tooAlternate Email</span></span>

<span data-ttu-id="e6aaf-145">根據預設，只有 hello 雲端屬性辦公室電話和行動電話會同步處理 tooyour 雲端目錄，從您的內部部署目錄的驗證資料。</span><span class="sxs-lookup"><span data-stu-id="e6aaf-145">By default, only hello cloud attributes Office Phone and Mobile Phone are synchronized tooyour cloud directory from your on-premises directory for authentication data.</span></span>

<span data-ttu-id="e6aaf-146">使用者可以只重設其密碼，才有 hello 驗證方法中的資料該 hello 系統管理員已啟用，且要求。</span><span class="sxs-lookup"><span data-stu-id="e6aaf-146">Users can only reset their password if they have data present in hello authentication methods that hello administrator has enabled and requires.</span></span>

<span data-ttu-id="e6aaf-147">如果使用者不想其行動電話號碼 toobe 可見 hello 目錄中，但還是希望像 toouse 它密碼重設，系統管理員應填入 hello 目錄中，然後填入 hello 使用者應該其**驗證電話**屬性透過 hello[密碼重設註冊入口網站](http://aka.ms/ssprsetup)。</span><span class="sxs-lookup"><span data-stu-id="e6aaf-147">If users do not want their mobile phone number toobe visible in hello directory but would still like toouse it for password reset, administrators should not populate it in hello directory and hello user should then populate their **Authentication Phone** attribute via hello [password reset registration portal](http://aka.ms/ssprsetup).</span></span> <span data-ttu-id="e6aaf-148">系統管理員可以查看這項資訊在 hello 使用者設定檔，但它不在其他位置發行。</span><span class="sxs-lookup"><span data-stu-id="e6aaf-148">Administrators can see this information in hello user's profile but it is not published elsewhere.</span></span> <span data-ttu-id="e6aaf-149">如果 Azure 系統管理員帳戶註冊其驗證電話號碼時，它會擴展到 hello 行動電話欄位，同時會顯示。</span><span class="sxs-lookup"><span data-stu-id="e6aaf-149">If an Azure Administrator account registers their authentication phone number, it is populated into hello mobile phone field and is visible.</span></span>

### <a name="number-of-authentication-methods-required"></a><span data-ttu-id="e6aaf-150">必要驗證方法數目</span><span class="sxs-lookup"><span data-stu-id="e6aaf-150">Number of authentication methods required</span></span>

<span data-ttu-id="e6aaf-151">此選項會決定 hello 的使用者必須通過 tooreset hello 可用的驗證方法數目下限或解除鎖定其密碼，而且可以設定 tooeither 1 或 2。</span><span class="sxs-lookup"><span data-stu-id="e6aaf-151">This option determines hello minimum number of hello available authentication methods a user must go through tooreset or unlock their password and can be set tooeither 1 or 2.</span></span>

<span data-ttu-id="e6aaf-152">使用者可以選擇 toosupply 個驗證方法，如果有啟用 hello 系統管理員。</span><span class="sxs-lookup"><span data-stu-id="e6aaf-152">Users can choose toosupply more authentication methods if they are enabled by hello administrator.</span></span>

<span data-ttu-id="e6aaf-153">如果使用者沒有已註冊的 hello 最小必要方法，就會看到錯誤頁面，會將他們導向 toorequest 管理員 tooreset 他們的密碼。</span><span class="sxs-lookup"><span data-stu-id="e6aaf-153">If a user does not have hello minimum required methods registered, they see an error page that directs them toorequest an administrator tooreset their password.</span></span>

### <a name="how-secure-are-my-security-questions"></a><span data-ttu-id="e6aaf-154">我的安全性問題有多安全</span><span class="sxs-lookup"><span data-stu-id="e6aaf-154">How secure are my security questions</span></span>

<span data-ttu-id="e6aaf-155">如果您使用安全性問題，我們建議它們使用另一個方法為它們可能會比其他方法更不安全因為有些人可能知道 hello 答案 tooanother 使用者問題。</span><span class="sxs-lookup"><span data-stu-id="e6aaf-155">If you use security questions, we recommend them in use with another method as they can be less secure than other methods since some people may know hello answers tooanother users questions.</span></span>

> [!NOTE] 
> <span data-ttu-id="e6aaf-156">安全性問題 hello 目錄中使用者物件上儲存非公開且安全的方式，而且可以只由使用者回答登錄期間。</span><span class="sxs-lookup"><span data-stu-id="e6aaf-156">Security questions are stored privately and securely on a user object in hello directory and can only be answered by users during registration.</span></span> <span data-ttu-id="e6aaf-157">沒有方法可讓系統管理員 tooread 或修改使用者問題或回答。</span><span class="sxs-lookup"><span data-stu-id="e6aaf-157">There is no way for an administrator tooread or modify a users questions or answers.</span></span>
>

### <a name="security-question-localization"></a><span data-ttu-id="e6aaf-158">安全性問題當地語系化</span><span class="sxs-lookup"><span data-stu-id="e6aaf-158">Security question localization</span></span>

<span data-ttu-id="e6aaf-159">所有預先定義的問題，請遵循已當地語系化為 hello 整組 hello 使用者的瀏覽器地區設定為基礎的 Office 365 語言。</span><span class="sxs-lookup"><span data-stu-id="e6aaf-159">All predefined questions that follow are localized into hello full set of Office 365 languages based on hello user's browser locale.</span></span>

* <span data-ttu-id="e6aaf-160">您在哪個城市遇見第一個配偶/伴侶？</span><span class="sxs-lookup"><span data-stu-id="e6aaf-160">In what city did you meet your first spouse/partner?</span></span>
* <span data-ttu-id="e6aaf-161">您的父母在哪個城市相遇？</span><span class="sxs-lookup"><span data-stu-id="e6aaf-161">In what city did your parents meet?</span></span>
* <span data-ttu-id="e6aaf-162">您最親近的手足住在哪個城市？</span><span class="sxs-lookup"><span data-stu-id="e6aaf-162">In what city does your nearest sibling live?</span></span>
* <span data-ttu-id="e6aaf-163">您的父親在哪個城市出生？</span><span class="sxs-lookup"><span data-stu-id="e6aaf-163">In what city was your father born?</span></span>
* <span data-ttu-id="e6aaf-164">您的第一份工作是在哪個城市？</span><span class="sxs-lookup"><span data-stu-id="e6aaf-164">In what city was your first job?</span></span>
* <span data-ttu-id="e6aaf-165">您的母親在哪個城市出生？</span><span class="sxs-lookup"><span data-stu-id="e6aaf-165">In what city was your mother born?</span></span>
* <span data-ttu-id="e6aaf-166">您在哪個城市渡過 2000 年的新年？</span><span class="sxs-lookup"><span data-stu-id="e6aaf-166">What city were you in on New Year's 2000?</span></span>
* <span data-ttu-id="e6aaf-167">什麼是最喜愛的老師在高 hello 姓氏 * 學校？</span><span class="sxs-lookup"><span data-stu-id="e6aaf-167">What is hello last name of your favorite teacher in high * school?</span></span>
* <span data-ttu-id="e6aaf-168">什麼是您套用的入學的 hello 名稱 toobut 不參加？</span><span class="sxs-lookup"><span data-stu-id="e6aaf-168">What is hello name of a college you applied toobut didn't attend?</span></span>
* <span data-ttu-id="e6aaf-169">Hello 地方您您第一場婚宴 hello 名稱是什麼？</span><span class="sxs-lookup"><span data-stu-id="e6aaf-169">What is hello name of hello place in which you held your first wedding reception?</span></span>
* <span data-ttu-id="e6aaf-170">您父親的中間名是什麼？</span><span class="sxs-lookup"><span data-stu-id="e6aaf-170">What is your father's middle name?</span></span>
* <span data-ttu-id="e6aaf-171">您最愛的食物是什麼？</span><span class="sxs-lookup"><span data-stu-id="e6aaf-171">What is your favorite food?</span></span>
* <span data-ttu-id="e6aaf-172">您外婆的姓名為何？</span><span class="sxs-lookup"><span data-stu-id="e6aaf-172">What is your maternal grandmother's first and last name?</span></span>
* <span data-ttu-id="e6aaf-173">您母親的中間名是什麼？</span><span class="sxs-lookup"><span data-stu-id="e6aaf-173">What is your mother's middle name?</span></span>
* <span data-ttu-id="e6aaf-174">您最年長手足的生日月份和年度為何？</span><span class="sxs-lookup"><span data-stu-id="e6aaf-174">What is your oldest sibling's birthday month and year?</span></span> <span data-ttu-id="e6aaf-175">(例如 1985 年 11 月)</span><span class="sxs-lookup"><span data-stu-id="e6aaf-175">(e.g. November 1985)</span></span>
* <span data-ttu-id="e6aaf-176">您最年長手足的中間名是什麼？</span><span class="sxs-lookup"><span data-stu-id="e6aaf-176">What is your oldest sibling's middle name?</span></span>
* <span data-ttu-id="e6aaf-177">您祖父的姓名為何？</span><span class="sxs-lookup"><span data-stu-id="e6aaf-177">What is your paternal grandfather's first and last name?</span></span>
* <span data-ttu-id="e6aaf-178">您最年幼手足的中間名稱是什麼？</span><span class="sxs-lookup"><span data-stu-id="e6aaf-178">What is your youngest sibling's middle name?</span></span>
* <span data-ttu-id="e6aaf-179">您六年級時就讀哪間學校？</span><span class="sxs-lookup"><span data-stu-id="e6aaf-179">What school did you attend for sixth grade?</span></span>
* <span data-ttu-id="e6aaf-180">什麼是第一次的 hello 名字童年最佳朋友的？</span><span class="sxs-lookup"><span data-stu-id="e6aaf-180">What was hello first and last name of your childhood best friend?</span></span>
* <span data-ttu-id="e6aaf-181">什麼是第一次的 hello 名字您的第一個配偶？</span><span class="sxs-lookup"><span data-stu-id="e6aaf-181">What was hello first and last name of your first significant other?</span></span>
* <span data-ttu-id="e6aaf-182">您最喜愛的小學老師的 hello 姓是什麼？</span><span class="sxs-lookup"><span data-stu-id="e6aaf-182">What was hello last name of your favorite grade school teacher?</span></span>
* <span data-ttu-id="e6aaf-183">第一個汽車或機車的 hello 廠牌和型號是什麼？</span><span class="sxs-lookup"><span data-stu-id="e6aaf-183">What was hello make and model of your first car or motorcycle?</span></span>
* <span data-ttu-id="e6aaf-184">Hello 您參加第一所學校 hello 名字是什麼？</span><span class="sxs-lookup"><span data-stu-id="e6aaf-184">What was hello name of hello first school you attended?</span></span>
* <span data-ttu-id="e6aaf-185">您已出生 hello 醫院 hello 名是什麼？</span><span class="sxs-lookup"><span data-stu-id="e6aaf-185">What was hello name of hello hospital in which you were born?</span></span>
* <span data-ttu-id="e6aaf-186">Hello 街道的第一個兒時家用 hello 名字是什麼？</span><span class="sxs-lookup"><span data-stu-id="e6aaf-186">What was hello name of hello street of your first childhood home?</span></span>
* <span data-ttu-id="e6aaf-187">您的童年英雄的 hello 名字是什麼？</span><span class="sxs-lookup"><span data-stu-id="e6aaf-187">What was hello name of your childhood hero?</span></span>
* <span data-ttu-id="e6aaf-188">最愛娃娃 hello 名字是什麼？</span><span class="sxs-lookup"><span data-stu-id="e6aaf-188">What was hello name of your favorite stuffed animal?</span></span>
* <span data-ttu-id="e6aaf-189">您第一隻寵物的 hello 名字是什麼？</span><span class="sxs-lookup"><span data-stu-id="e6aaf-189">What was hello name of your first pet?</span></span>
* <span data-ttu-id="e6aaf-190">您童年時期的綽號是什麼？</span><span class="sxs-lookup"><span data-stu-id="e6aaf-190">What was your childhood nickname?</span></span>
* <span data-ttu-id="e6aaf-191">您中學最喜愛的運動是什麼？</span><span class="sxs-lookup"><span data-stu-id="e6aaf-191">What was your favorite sport in high school?</span></span>
* <span data-ttu-id="e6aaf-192">您的第一份工作是什麼？</span><span class="sxs-lookup"><span data-stu-id="e6aaf-192">What was your first job?</span></span>
* <span data-ttu-id="e6aaf-193">什麼是 hello 您兒時電話號碼的末 4 碼？</span><span class="sxs-lookup"><span data-stu-id="e6aaf-193">What were hello last four digits of your childhood telephone number?</span></span>
* <span data-ttu-id="e6aaf-194">長大時，所希望 toobe 時小時候？</span><span class="sxs-lookup"><span data-stu-id="e6aaf-194">When you were young, what did you want toobe when you grew up?</span></span>
* <span data-ttu-id="e6aaf-195">Hello 您遇最知名的人物是誰？</span><span class="sxs-lookup"><span data-stu-id="e6aaf-195">Who is hello most famous person you have ever met?</span></span>

### <a name="custom-security-questions"></a><span data-ttu-id="e6aaf-196">自訂安全性問題</span><span class="sxs-lookup"><span data-stu-id="e6aaf-196">Custom security questions</span></span>

<span data-ttu-id="e6aaf-197">自訂安全性問題不會針對不同的地區設定進行當地語系化。</span><span class="sxs-lookup"><span data-stu-id="e6aaf-197">Custom security questions are not localized for different locales.</span></span> <span data-ttu-id="e6aaf-198">所有自訂問題會顯示在 [hello 會在 hello 系統管理使用者介面中輸入，即使 hello 使用者的瀏覽器地區設定是不同的語言相同。</span><span class="sxs-lookup"><span data-stu-id="e6aaf-198">All custom questions are displayed in hello same language they are entered in hello administrative user interface even if hello user's browser locale is different.</span></span> <span data-ttu-id="e6aaf-199">如果您需要當地語系化的問題，請使用 hello 預先定義的問題。</span><span class="sxs-lookup"><span data-stu-id="e6aaf-199">If you need localized questions, please use hello predefined questions.</span></span>

<span data-ttu-id="e6aaf-200">hello 與自訂安全性問題的最大長度為 200 個字元。</span><span class="sxs-lookup"><span data-stu-id="e6aaf-200">hello maximum length of a custom security question is 200 characters.</span></span>

### <a name="security-question-requirements"></a><span data-ttu-id="e6aaf-201">安全性問題需求</span><span class="sxs-lookup"><span data-stu-id="e6aaf-201">Security question requirements</span></span>

* <span data-ttu-id="e6aaf-202">答案字元限制下限為 3 個字元。</span><span class="sxs-lookup"><span data-stu-id="e6aaf-202">Minimum answer character limit is 3 characters</span></span>
* <span data-ttu-id="e6aaf-203">答案字元限制上限為 40 個字元。</span><span class="sxs-lookup"><span data-stu-id="e6aaf-203">Maximum answer character limit is 40 characters</span></span>
* <span data-ttu-id="e6aaf-204">使用者不會回答相同問題一次以上的 hello</span><span class="sxs-lookup"><span data-stu-id="e6aaf-204">Users may not answer hello same question more than one time</span></span>
* <span data-ttu-id="e6aaf-205">使用者可能不會提供 hello 相同回答 toomore 比一個問題</span><span class="sxs-lookup"><span data-stu-id="e6aaf-205">Users may not provide hello same answer toomore than one question</span></span>
* <span data-ttu-id="e6aaf-206">任何字元集可能會使用的 toodefine 問題和答案包括 Unicode 字元</span><span class="sxs-lookup"><span data-stu-id="e6aaf-206">Any character set may be used toodefine questions and answers including Unicode characters</span></span>
* <span data-ttu-id="e6aaf-207">hello 定義的問題數必須大於或等於 toohello 問題需要 tooregister 數目</span><span class="sxs-lookup"><span data-stu-id="e6aaf-207">hello number of questions defined must be greater than or equal toohello number of questions required tooregister</span></span>

## <a name="registration"></a><span data-ttu-id="e6aaf-208">註冊</span><span class="sxs-lookup"><span data-stu-id="e6aaf-208">Registration</span></span>

### <a name="require-users-tooregister-when-signing-in"></a><span data-ttu-id="e6aaf-209">在登入時，要求使用者 tooregister</span><span class="sxs-lookup"><span data-stu-id="e6aaf-209">Require users tooregister when signing in</span></span>

<span data-ttu-id="e6aaf-210">啟用此選項需要使用者啟用密碼重設 toocomplete hello 密碼重設註冊登入時使用中的 Azure AD toosign 遵循類似 tooapplications:</span><span class="sxs-lookup"><span data-stu-id="e6aaf-210">Enabling this option requires a user who is enabled for password reset toocomplete hello password reset registration if they login tooapplications using Azure AD toosign in like those that follow:</span></span>

* <span data-ttu-id="e6aaf-211">Office 365</span><span class="sxs-lookup"><span data-stu-id="e6aaf-211">Office 365</span></span>
* <span data-ttu-id="e6aaf-212">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="e6aaf-212">Azure portal</span></span>
* <span data-ttu-id="e6aaf-213">存取面板</span><span class="sxs-lookup"><span data-stu-id="e6aaf-213">Access Panel</span></span>
* <span data-ttu-id="e6aaf-214">同盟應用程式</span><span class="sxs-lookup"><span data-stu-id="e6aaf-214">Federated applications</span></span>
* <span data-ttu-id="e6aaf-215">使用 Azure AD 自訂應用程式</span><span class="sxs-lookup"><span data-stu-id="e6aaf-215">Custom applications using Azure AD</span></span>

<span data-ttu-id="e6aaf-216">停用這項功能仍然可讓使用者 toomanually 註冊他們的連絡資訊造訪[http://aka.ms/ssprsetup](http://aka.ms/ssprsetup)或按一下 hello**註冊密碼重設**hello 底下的連結hello 存取面板中的設定檔索引標籤。</span><span class="sxs-lookup"><span data-stu-id="e6aaf-216">Disabling this feature will still allow users toomanually register their contact information by visiting [http://aka.ms/ssprsetup](http://aka.ms/ssprsetup) or by clicking hello **register for password reset** link under hello profile tab in hello access panel.</span></span>

> [!NOTE]
> <span data-ttu-id="e6aaf-217">使用者可以按一下 [取消] 5d; 或關閉 hello 視窗關閉 hello 密碼重設註冊入口網站，但每次完成註冊之後才登入時提示。</span><span class="sxs-lookup"><span data-stu-id="e6aaf-217">Users can dismiss hello password reset registration portal by clicking cancel or closing hello window but are prompted each time they login until they complete registration.</span></span>
>

### <a name="number-of-days-before-users-are-asked-tooreconfirm-their-authentication-information"></a><span data-ttu-id="e6aaf-218">數天之後使用者, 詢問 tooreconfirm 其驗證資訊</span><span class="sxs-lookup"><span data-stu-id="e6aaf-218">Number of days before users are asked tooreconfirm their authentication information</span></span>

<span data-ttu-id="e6aaf-219">此選項可決定 hello 期間設定和 reconfirming 驗證資訊之間的時間和才可使用啟用 hello**在登入時，要求使用者 tooregister**選項。</span><span class="sxs-lookup"><span data-stu-id="e6aaf-219">This option determines hello period of time between setting and reconfirming authentication information and is only available if you enable hello **require users tooregister when signing in** option.</span></span>

<span data-ttu-id="e6aaf-220">有效值為 0-730 天 0 表示絕對不會要求使用者 tooreconfirm 其驗證資訊</span><span class="sxs-lookup"><span data-stu-id="e6aaf-220">Valid values are 0-730 days with 0 meaning never ask users tooreconfirm their authentication information</span></span>

## <a name="notifications"></a><span data-ttu-id="e6aaf-221">通知</span><span class="sxs-lookup"><span data-stu-id="e6aaf-221">Notifications</span></span>

### <a name="notify-users-on-password-resets"></a><span data-ttu-id="e6aaf-222">通知使用者密碼重設</span><span class="sxs-lookup"><span data-stu-id="e6aaf-222">Notify users on password resets</span></span>

<span data-ttu-id="e6aaf-223">如果此選項設定 tooyes，正在重設其密碼的 hello 使用者接收電子郵件通知他們的已變更其密碼透過 hello SSPR 入口 tootheir 主要和備用電子郵件地址檔案在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="e6aaf-223">If this option is set tooyes, then hello user who is resetting their password receives an email notifying them that their password has been changed via hello SSPR portal tootheir primary and alternate email addresses on file in Azure AD.</span></span> <span data-ttu-id="e6aaf-224">沒有人會接獲此重設事件的通知。</span><span class="sxs-lookup"><span data-stu-id="e6aaf-224">No one else is notified of this reset event.</span></span>

### <a name="notify-all-admins-when-other-admins-reset-their-passwords"></a><span data-ttu-id="e6aaf-225">當其他系統管理員重設其密碼時通知所有系統管理員</span><span class="sxs-lookup"><span data-stu-id="e6aaf-225">Notify all admins when other admins reset their passwords</span></span>

<span data-ttu-id="e6aaf-226">如果此選項設定 tooyes，則**所有系統管理員**接收通知其他系統管理員已經使用 SSPR 密碼的 Azure AD 中的檔案上的電子郵件 tootheir 主要電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="e6aaf-226">If this option is set tooyes, then **all administrators** receive an email tootheir primary email address on file in Azure AD notifying them that another administrator has changed their password using SSPR.</span></span>

<span data-ttu-id="e6aaf-227">範例︰環境中有四個系統管理員。</span><span class="sxs-lookup"><span data-stu-id="e6aaf-227">Example: There are four administrators in an environment.</span></span> <span data-ttu-id="e6aaf-228">系統管理員 "A" 使用 SSPR 重設其密碼。</span><span class="sxs-lookup"><span data-stu-id="e6aaf-228">Administrator "A" resets their password using SSPR.</span></span> <span data-ttu-id="e6aaf-229">系統管理員 B、C 和 D 收到一封電子郵件，警示他們發生此狀況。</span><span class="sxs-lookup"><span data-stu-id="e6aaf-229">Administrators B, C, and D receive an email alerting them of this happening.</span></span>

## <a name="on-premises-integration"></a><span data-ttu-id="e6aaf-230">內部部署整合</span><span class="sxs-lookup"><span data-stu-id="e6aaf-230">On-premises integration</span></span>

<span data-ttu-id="e6aaf-231">如果您已安裝、設定及啟用 Azure AD Connect，您會有其他的內部部署整合選項。</span><span class="sxs-lookup"><span data-stu-id="e6aaf-231">If you have installed, configured, and enabled Azure AD Connect you will have additional options for on-premises integrations.</span></span>

### <a name="write-back-passwords-tooyour-on-premises-directory"></a><span data-ttu-id="e6aaf-232">回寫密碼 tooyour 在內部部署目錄</span><span class="sxs-lookup"><span data-stu-id="e6aaf-232">Write back passwords tooyour on-premises directory</span></span>

<span data-ttu-id="e6aaf-233">控制啟用此目錄密碼回寫，而且如果回寫上，指出 hello hello 在內部部署回寫服務狀態。</span><span class="sxs-lookup"><span data-stu-id="e6aaf-233">Controls whether or not password writeback is enabled for this directory and, if writeback is on, indicates hello status of hello on-premises writeback service.</span></span> <span data-ttu-id="e6aaf-234">這非常有用，如果您想 tootemporarily 停用 hello 密碼回寫，而不需重新設定 Azure AD Connect。</span><span class="sxs-lookup"><span data-stu-id="e6aaf-234">This is useful if you want tootemporarily disable hello password writeback without re-configuring Azure AD Connect.</span></span>

* <span data-ttu-id="e6aaf-235">如果 hello 切換是集 tooyes 回寫會啟用，與同盟和密碼雜湊同步處理的使用者都能 tooreset 他們的密碼。</span><span class="sxs-lookup"><span data-stu-id="e6aaf-235">If hello switch is set tooyes, then writeback will be enabled, and federated and password hash synchronized users will be able tooreset their passwords.</span></span>
* <span data-ttu-id="e6aaf-236">如果 hello 切換是集 toono 回寫會停用，與同盟和密碼雜湊同步處理使用者並不會無法 tooreset 他們的密碼。</span><span class="sxs-lookup"><span data-stu-id="e6aaf-236">If hello switch is set toono, then writeback will be disabled, and federated and password hash synchronized users will not be able tooreset their passwords.</span></span>

### <a name="allow-users-toounlock-accounts-without-resetting-their-password"></a><span data-ttu-id="e6aaf-237">允許使用者 toounlock 帳戶，而不重設其密碼</span><span class="sxs-lookup"><span data-stu-id="e6aaf-237">Allow users toounlock accounts without resetting their password</span></span>

<span data-ttu-id="e6aaf-238">指定造訪 hello 密碼重設入口網站的使用者應該是給定的 hello 選項 toounlock 其內部部署 Active Directory 帳戶，而不重設其密碼。</span><span class="sxs-lookup"><span data-stu-id="e6aaf-238">Designates whether or not users who visit hello password reset portal should be given hello option toounlock their on-premises Active Directory accounts without resetting their password.</span></span> <span data-ttu-id="e6aaf-239">根據預設，Azure AD 會一律解除鎖定帳戶執行密碼重設時，此設定可讓您 tooseparate 這兩項作業。</span><span class="sxs-lookup"><span data-stu-id="e6aaf-239">By default, Azure AD will always unlock accounts when performing a password reset, this setting allows you tooseparate those two operations.</span></span> 

* <span data-ttu-id="e6aaf-240">如果設定太"yes"，則使用者將會是給定的 hello 選項 tooreset 其密碼和解除鎖定 hello 帳戶或 toounlock 而不重設 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="e6aaf-240">If set too“yes”, then users will be given hello option tooreset their password and unlock hello account, or toounlock without resetting hello password.</span></span>
* <span data-ttu-id="e6aaf-241">如果設定太"no"，然後使用者才能夠 tooperform 結合的密碼重設和帳戶解除鎖定作業。</span><span class="sxs-lookup"><span data-stu-id="e6aaf-241">If set too“no”, then users will only be able tooperform a combined password reset and account unlock operation.</span></span>

## <a name="network-requirements"></a><span data-ttu-id="e6aaf-242">網路需求</span><span class="sxs-lookup"><span data-stu-id="e6aaf-242">Network requirements</span></span>

### <a name="firewall-rules"></a><span data-ttu-id="e6aaf-243">防火牆規則</span><span class="sxs-lookup"><span data-stu-id="e6aaf-243">Firewall rules</span></span>

[<span data-ttu-id="e6aaf-244">Microsoft Office URL 和 IP 位址清單</span><span class="sxs-lookup"><span data-stu-id="e6aaf-244">List of Microsoft Office URLs and IP addresses</span></span>](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2)

<span data-ttu-id="e6aaf-245">Azure AD Connect 1.1.443.0 版和更新版本，您需要的輸出 HTTPS 存取 toohello 下列</span><span class="sxs-lookup"><span data-stu-id="e6aaf-245">For Azure AD Connect version 1.1.443.0 and above, you need outbound HTTPS access toohello following</span></span>
* <span data-ttu-id="e6aaf-246">passwordreset.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="e6aaf-246">passwordreset.microsoftonline.com</span></span>
* <span data-ttu-id="e6aaf-247">servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="e6aaf-247">servicebus.windows.net</span></span>

<span data-ttu-id="e6aaf-248">對於更細微的存取，您可以找到 hello 更新 Microsoft Azure Datacenter IP 範圍，更新每個星期三並放入效果 hello 下列清單星期一[這裡](https://www.microsoft.com/download/details.aspx?id=41653)。</span><span class="sxs-lookup"><span data-stu-id="e6aaf-248">For more granular access, you can find hello updated list of Microsoft Azure Datacenter IP Ranges that is updated every Wednesday and put into effect hello following Monday [here](https://www.microsoft.com/download/details.aspx?id=41653).</span></span>

### <a name="idle-connection-timeouts"></a><span data-ttu-id="e6aaf-249">閒置連線逾時</span><span class="sxs-lookup"><span data-stu-id="e6aaf-249">Idle connection timeouts</span></span>

<span data-ttu-id="e6aaf-250">hello Azure AD Connect 工具會傳送定期 ping/keepalives tooServiceBus 端點 tooensure hello 連線保持運作。</span><span class="sxs-lookup"><span data-stu-id="e6aaf-250">hello Azure AD Connect tool sends periodic pings/keepalives tooServiceBus endpoints tooensure that hello connections stay alive.</span></span> <span data-ttu-id="e6aaf-251">應該 hello 工具偵測到太多連線會遭到刪除，它會自動增加 ping toohello 端點的 hello 頻率。</span><span class="sxs-lookup"><span data-stu-id="e6aaf-251">Should hello tool detect that too many connections are being killed, it will automatically increase hello frequency of pings toohello endpoint.</span></span> <span data-ttu-id="e6aaf-252">hello 最低 'ping 時間間隔' 卸除 toois 1 ping 每隔 60 秒，不過，我們強烈建議 proxy/防火牆允許閒置連接 toopersist，至少 2-3 分鐘。</span><span class="sxs-lookup"><span data-stu-id="e6aaf-252">hello lowest 'ping intervals' drops toois 1 ping every 60 seconds, however, we strongly advise that proxies/firewalls allow idle connections toopersist for at least 2-3 minutes.</span></span> <span data-ttu-id="e6aaf-253">*針對較舊版本，建議 4 分鐘以上。</span><span class="sxs-lookup"><span data-stu-id="e6aaf-253">*For older versions, we suggest four minutes or more.</span></span>

## <a name="active-directory-permissions"></a><span data-ttu-id="e6aaf-254">Active Directory 權限</span><span class="sxs-lookup"><span data-stu-id="e6aaf-254">Active Directory permissions</span></span>

<span data-ttu-id="e6aaf-255">hello hello Azure AD Connect 公用程式中指定的帳戶必須具有重設密碼、 變更密碼、 lockoutTime，寫入權限和寫入權限 pwdLastSet，擴充權限的任一個 hello 根物件**每個網域**該樹系中**或**hello 使用者 Ou 上您想 toobe SSPR 範圍中的。</span><span class="sxs-lookup"><span data-stu-id="e6aaf-255">hello account specified in hello Azure AD Connect utility must have Reset Password, Change Password, Write Permissions on lockoutTime, and Write Permissions on pwdLastSet, extended rights on either hello root object of **each domain** in that forest **OR** on hello user OUs you wish toobe in scope for SSPR.</span></span>

<span data-ttu-id="e6aaf-256">如果您不確定上述何種帳戶 hello 參考、 開啟 hello Azure Active Directory Connect 組態 UI，然後按一下 hello 檢視目前的組態選項。</span><span class="sxs-lookup"><span data-stu-id="e6aaf-256">If you are not sure what account hello above refers to, open hello Azure Active Directory Connect configuration UI and click hello View current configuration option.</span></span> <span data-ttu-id="e6aaf-257">hello 帳戶，您需要 tooadd 權限 toois 列在 [同步處理目錄]</span><span class="sxs-lookup"><span data-stu-id="e6aaf-257">hello account you need tooadd permission toois listed under "Synchronized Directories"</span></span>

<span data-ttu-id="e6aaf-258">設定這些權限允許該樹系中的 hello MA 服務帳戶的每個樹系 toomanage 密碼的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="e6aaf-258">Setting these permissions allows hello MA service account for each forest toomanage passwords on behalf of user accounts within that forest.</span></span> <span data-ttu-id="e6aaf-259">**如果您並未 tooassign 這些權限，然後，即使回寫 toobe 正確設定，使用者嘗試 toomanage hello 雲端從其內部部署密碼時，就會發生錯誤。**</span><span class="sxs-lookup"><span data-stu-id="e6aaf-259">**If you neglect tooassign these permissions, then, even though writeback appears toobe configured correctly, users encounter errors when attempting toomanage their on-premises passwords from hello cloud.**</span></span>

> [!NOTE]
> <span data-ttu-id="e6aaf-260">它可能會佔用 tooan 小時或更多您的目錄中的這些權限 tooreplicate tooall 物件。</span><span class="sxs-lookup"><span data-stu-id="e6aaf-260">It could take up tooan hour or more for these permissions tooreplicate tooall objects in your directory.</span></span>
>

<span data-ttu-id="e6aaf-261">tooset hello 的密碼回寫 toooccur 的適當權限</span><span class="sxs-lookup"><span data-stu-id="e6aaf-261">tooset up hello appropriate permissions for password writeback toooccur</span></span>

1. <span data-ttu-id="e6aaf-262">使用具有 hello 適當網域管理權限的帳戶開啟 [Active Directory 使用者和電腦</span><span class="sxs-lookup"><span data-stu-id="e6aaf-262">Open Active Directory Users and Computers with an account that has hello appropriate domain administration permissions</span></span>
2. <span data-ttu-id="e6aaf-263">從 hello 檢視] 功能表中，確定已開啟 [進階功能</span><span class="sxs-lookup"><span data-stu-id="e6aaf-263">From hello View menu, make sure Advanced Features is turned on</span></span>
3. <span data-ttu-id="e6aaf-264">在 hello 左面板中，以滑鼠右鍵按一下代表 hello hello 網域根目錄的 hello 物件，然後選擇屬性</span><span class="sxs-lookup"><span data-stu-id="e6aaf-264">In hello left panel, right-click hello object that represents hello root of hello domain and choose properties</span></span>
    * <span data-ttu-id="e6aaf-265">Hello 安全性] 索引標籤</span><span class="sxs-lookup"><span data-stu-id="e6aaf-265">Click hello Security tab</span></span>
    * <span data-ttu-id="e6aaf-266">然後按一下 [進階]。</span><span class="sxs-lookup"><span data-stu-id="e6aaf-266">Then click Advanced.</span></span>
4. <span data-ttu-id="e6aaf-267">Hello 權限] 索引標籤中，按一下 [新增]</span><span class="sxs-lookup"><span data-stu-id="e6aaf-267">From hello Permissions tab, click Add</span></span>
5. <span data-ttu-id="e6aaf-268">挑選 hello 太 （從 Azure AD Connect 的安裝程式） 會被套用權限的帳戶</span><span class="sxs-lookup"><span data-stu-id="e6aaf-268">Pick hello account that permissions are being applied too(from Azure AD Connect setup)</span></span>
6. <span data-ttu-id="e6aaf-269">在 [hello 適用於 toodrop 下拉方塊中選取 [子系的使用者物件</span><span class="sxs-lookup"><span data-stu-id="e6aaf-269">In hello Applies toodrop down box select Descendent User objects</span></span>
7. <span data-ttu-id="e6aaf-270">權限] 底下的核取 hello 下列 hello 方塊</span><span class="sxs-lookup"><span data-stu-id="e6aaf-270">Under permissions check hello boxes for hello following</span></span>
    * <span data-ttu-id="e6aaf-271">未過期密碼</span><span class="sxs-lookup"><span data-stu-id="e6aaf-271">Unexpire-Password</span></span>
    * <span data-ttu-id="e6aaf-272">重設密碼</span><span class="sxs-lookup"><span data-stu-id="e6aaf-272">Reset Password</span></span>
    * <span data-ttu-id="e6aaf-273">變更密碼</span><span class="sxs-lookup"><span data-stu-id="e6aaf-273">Change Password</span></span>
    * <span data-ttu-id="e6aaf-274">寫入 lockoutTime</span><span class="sxs-lookup"><span data-stu-id="e6aaf-274">Write lockoutTime</span></span>
    * <span data-ttu-id="e6aaf-275">寫入 pwdLastSet</span><span class="sxs-lookup"><span data-stu-id="e6aaf-275">Write pwdLastSet</span></span>
8. <span data-ttu-id="e6aaf-276">按一下 tooapply 套用/確定]，再結束任何開啟的對話方塊。</span><span class="sxs-lookup"><span data-stu-id="e6aaf-276">Click Apply/OK through tooapply and exit any open dialog boxes.</span></span>

## <a name="how-does-password-reset-work-for-b2b-users"></a><span data-ttu-id="e6aaf-277">B2B 使用者的密碼重設運作方式</span><span class="sxs-lookup"><span data-stu-id="e6aaf-277">How does password reset work for B2B users?</span></span>
<span data-ttu-id="e6aaf-278">所有 B2B 組態完全支援密碼重設和變更。</span><span class="sxs-lookup"><span data-stu-id="e6aaf-278">Password reset and change are fully supported with all B2B configurations.</span></span>  <span data-ttu-id="e6aaf-279">閱讀下列 hello 三個明確 B2B 案例支援密碼重設。</span><span class="sxs-lookup"><span data-stu-id="e6aaf-279">Read below for hello three explicit B2B cases supported by password reset.</span></span>

1. <span data-ttu-id="e6aaf-280">**從現有的 Azure AD 租用戶與夥伴組織的使用者**-如果您使用合作的 hello 組織有現有的 Azure AD 租用戶，我們**採用該租用戶中已啟用的任何密碼重設原則**。</span><span class="sxs-lookup"><span data-stu-id="e6aaf-280">**Users from a partner org with an existing Azure AD tenant** - If hello organization you are partnering with has an existing Azure AD tenant, we **respect whatever password reset policies are enabled in that tenant**.</span></span> <span data-ttu-id="e6aaf-281">中的密碼重設 toowork、 hello 夥伴組織僅需要 toomake 確定已啟用 Azure AD SSPR，也就是對 O365 的客戶不另收費用，而且可以啟用依照下列步驟 hello 我們[開始使用密碼管理](https://azure.microsoft.com/documentation/articles/active-directory-passwords-getting-started/#enable-users-to-reset-or-change-their-aad-passwords)指南。</span><span class="sxs-lookup"><span data-stu-id="e6aaf-281">For password reset toowork, hello partner organization just needs toomake sure Azure AD SSPR is enabled, which is no additional charge for O365 customers, and can be enabled by following hello steps in our [Getting Started with Password Management](https://azure.microsoft.com/documentation/articles/active-directory-passwords-getting-started/#enable-users-to-reset-or-change-their-aad-passwords) guide.</span></span>
2. <span data-ttu-id="e6aaf-282">**使用者註冊使用[自助式註冊](active-directory-self-service-signup.md)** -如果您以合作的 hello 組織使用 hello[自助式註冊](active-directory-self-service-signup.md)功能 tooget 入租用戶，我們會讓它們具有重設hello 電子郵件註冊它們。</span><span class="sxs-lookup"><span data-stu-id="e6aaf-282">**Users who signed up using [self-service sign-up](active-directory-self-service-signup.md)** - If hello organization you are partnering with used hello [self-service sign-up](active-directory-self-service-signup.md) feature tooget into a tenant, we let them reset with hello email they registered.</span></span>
3. <span data-ttu-id="e6aaf-283">**B2B 使用者**-使用 hello 新建立的任何新 B2B 使用者[Azure AD B2B 功能](active-directory-b2b-what-is-azure-ad-b2b.md)也會無法 tooreset hello 其註冊過程 hello 邀請的電子郵件與密碼。</span><span class="sxs-lookup"><span data-stu-id="e6aaf-283">**B2B users** - Any new B2B users created using hello new [Azure AD B2B capabilities](active-directory-b2b-what-is-azure-ad-b2b.md) will also be able tooreset their passwords with hello email they registered during hello invite process.</span></span>

<span data-ttu-id="e6aaf-284">tootest 與其中一個夥伴的使用者，請移 toohttp://passwordreset.microsoftonline.com。</span><span class="sxs-lookup"><span data-stu-id="e6aaf-284">tootest this, go toohttp://passwordreset.microsoftonline.com with one of these partner users.</span></span> <span data-ttu-id="e6aaf-285">只要他們定義了替代電子郵件或驗證電子郵件，密碼重設就會如預期般運作。</span><span class="sxs-lookup"><span data-stu-id="e6aaf-285">As long as they have an alternate email or authentication email defined, password reset works as expected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e6aaf-286">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e6aaf-286">Next steps</span></span>

<span data-ttu-id="e6aaf-287">hello 下列連結提供有關密碼重設使用 Azure AD 的其他資訊</span><span class="sxs-lookup"><span data-stu-id="e6aaf-287">hello following links provide additional information regarding password reset using Azure AD</span></span>

* <span data-ttu-id="e6aaf-288">[**快速入門**](active-directory-passwords-getting-started.md) - 開始執行 Azure AD 自助式密碼管理</span><span class="sxs-lookup"><span data-stu-id="e6aaf-288">[**Quick Start**](active-directory-passwords-getting-started.md) - Get up and running with Azure AD self service password management</span></span> 
* <span data-ttu-id="e6aaf-289">[**授權**](active-directory-passwords-licensing.md) - 設定 Azure AD 授權</span><span class="sxs-lookup"><span data-stu-id="e6aaf-289">[**Licensing**](active-directory-passwords-licensing.md) - Configure your Azure AD Licensing</span></span>
* <span data-ttu-id="e6aaf-290">[**資料**](active-directory-passwords-data.md) -了解所需的 hello 資料及如何使用密碼管理</span><span class="sxs-lookup"><span data-stu-id="e6aaf-290">[**Data**](active-directory-passwords-data.md) - Understand hello data that is required and how it is used for password management</span></span>
* <span data-ttu-id="e6aaf-291">[**首度發行**](active-directory-passwords-best-practices.md) -計劃和部署 SSPR tooyour 使用者 hello 指引，請參閱</span><span class="sxs-lookup"><span data-stu-id="e6aaf-291">[**Rollout**](active-directory-passwords-best-practices.md) - Plan and deploy SSPR tooyour users using hello guidance found here</span></span>
* <span data-ttu-id="e6aaf-292">[**原則**](active-directory-passwords-policy.md) - 了解並設定 Azure AD 密碼原則</span><span class="sxs-lookup"><span data-stu-id="e6aaf-292">[**Policy**](active-directory-passwords-policy.md) - Understand and set Azure AD password policies</span></span>
* <span data-ttu-id="e6aaf-293">[**密碼回寫**](active-directory-passwords-writeback.md) - 密碼回寫如何使用您的內部部署目錄</span><span class="sxs-lookup"><span data-stu-id="e6aaf-293">[**Password Writeback**](active-directory-passwords-writeback.md) - How does password writeback work with your on-premises directory</span></span>
* <span data-ttu-id="e6aaf-294">[**自訂**](active-directory-passwords-customize.md) -自訂的 hello SSPR 體驗您的公司 hello 外觀與風格。</span><span class="sxs-lookup"><span data-stu-id="e6aaf-294">[**Customize**](active-directory-passwords-customize.md) - Customize hello look and feel of hello SSPR experience for your company.</span></span>
* <span data-ttu-id="e6aaf-295">[**報告**](active-directory-passwords-reporting.md) - 探索您的使用者是否、何時、何地存取 SSPR 功能</span><span class="sxs-lookup"><span data-stu-id="e6aaf-295">[**Reporting**](active-directory-passwords-reporting.md) - Discover if, when, and where your users are accessing SSPR functionality</span></span>
* <span data-ttu-id="e6aaf-296">[**常見問題集**](active-directory-passwords-faq.md) - 如何？</span><span class="sxs-lookup"><span data-stu-id="e6aaf-296">[**Frequently Asked Questions**](active-directory-passwords-faq.md) - How?</span></span> <span data-ttu-id="e6aaf-297">原因為何？</span><span class="sxs-lookup"><span data-stu-id="e6aaf-297">Why?</span></span> <span data-ttu-id="e6aaf-298">何事？</span><span class="sxs-lookup"><span data-stu-id="e6aaf-298">What?</span></span> <span data-ttu-id="e6aaf-299">何地？</span><span class="sxs-lookup"><span data-stu-id="e6aaf-299">Where?</span></span> <span data-ttu-id="e6aaf-300">何人？</span><span class="sxs-lookup"><span data-stu-id="e6aaf-300">Who?</span></span> <span data-ttu-id="e6aaf-301">何時？</span><span class="sxs-lookup"><span data-stu-id="e6aaf-301">When?</span></span> <span data-ttu-id="e6aaf-302">-回答您總是想 tooask tooquestions</span><span class="sxs-lookup"><span data-stu-id="e6aaf-302">- Answers tooquestions you always wanted tooask</span></span>
* <span data-ttu-id="e6aaf-303">[**疑難排解**](active-directory-passwords-troubleshoot.md) -了解如何 tooresolve 常見問題，我們會看到與 SSPR</span><span class="sxs-lookup"><span data-stu-id="e6aaf-303">[**Troubleshoot**](active-directory-passwords-troubleshoot.md) - Learn how tooresolve common issues that we see with SSPR</span></span>

