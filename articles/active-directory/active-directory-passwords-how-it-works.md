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
ms.openlocfilehash: 0fa05ee6a2df13845024e770a82f50ab7f75bafd
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="self-service-password-reset-in-azure-ad-deep-dive"></a><span data-ttu-id="14b5c-103">Azure AD 中的自助式密碼重設深入探討</span><span class="sxs-lookup"><span data-stu-id="14b5c-103">Self-service password reset in Azure AD deep dive</span></span>

<span data-ttu-id="14b5c-104">SSPR 的運作方式</span><span class="sxs-lookup"><span data-stu-id="14b5c-104">How does SSPR work?</span></span> <span data-ttu-id="14b5c-105">該選項在介面中的意義為何？</span><span class="sxs-lookup"><span data-stu-id="14b5c-105">What does that option mean in the interface?</span></span> <span data-ttu-id="14b5c-106">繼續閱讀以深入了解 Azure AD 自助式密碼重設。</span><span class="sxs-lookup"><span data-stu-id="14b5c-106">Continue reading to find out more about Azure AD self-service password reset.</span></span>

## <a name="how-does-the-password-reset-portal-work"></a><span data-ttu-id="14b5c-107">密碼重設入口網站的運作方式</span><span class="sxs-lookup"><span data-stu-id="14b5c-107">How does the password reset portal work</span></span>

<span data-ttu-id="14b5c-108">當使用者瀏覽至密碼重設入口網站時，工作流程就會開始判斷︰</span><span class="sxs-lookup"><span data-stu-id="14b5c-108">When a user navigates to the password reset portal, a workflow is kicked off to determine:</span></span>

   * <span data-ttu-id="14b5c-109">如何將頁面當地語系化？</span><span class="sxs-lookup"><span data-stu-id="14b5c-109">How should the page be localized?</span></span>
   * <span data-ttu-id="14b5c-110">使用者帳戶是否有效？</span><span class="sxs-lookup"><span data-stu-id="14b5c-110">Is the user account valid?</span></span>
   * <span data-ttu-id="14b5c-111">使用者屬於哪個組織？</span><span class="sxs-lookup"><span data-stu-id="14b5c-111">What organization does the user belong to?</span></span>
   * <span data-ttu-id="14b5c-112">何處管理使用者的密碼？</span><span class="sxs-lookup"><span data-stu-id="14b5c-112">Where the user’s password is managed?</span></span>
   * <span data-ttu-id="14b5c-113">使用者是否已獲得授權使用此功能？</span><span class="sxs-lookup"><span data-stu-id="14b5c-113">Is the user licensed to use the feature?</span></span>


<span data-ttu-id="14b5c-114">請看完下列步驟，以了解密碼重設頁面背後的邏輯。</span><span class="sxs-lookup"><span data-stu-id="14b5c-114">Read through the steps below to learn about the logic behind the password reset page.</span></span>

1. <span data-ttu-id="14b5c-115">使用者按一下 [無法存取帳戶] 連結或直接移至 [https://passwordreset.microsoftonline.com](https://passwordreset.microsoftonline.com)。</span><span class="sxs-lookup"><span data-stu-id="14b5c-115">User clicks the Can’t access your account link or goes directly to [https://passwordreset.microsoftonline.com](https://passwordreset.microsoftonline.com).</span></span>
2. <span data-ttu-id="14b5c-116">根據瀏覽器的地區設定，此體驗會以適當的語言呈現。</span><span class="sxs-lookup"><span data-stu-id="14b5c-116">Based on the browser locale the experience is rendered in the appropriate language.</span></span> <span data-ttu-id="14b5c-117">密碼重設體驗會當地語系化為 Office 365 支援的相同語言。</span><span class="sxs-lookup"><span data-stu-id="14b5c-117">The password reset experience is localized into the same languages as Office 365 supports.</span></span>
3. <span data-ttu-id="14b5c-118">使用者輸入使用者識別碼並通過文字驗證。</span><span class="sxs-lookup"><span data-stu-id="14b5c-118">User enters a user id and passes a captcha.</span></span>
4. <span data-ttu-id="14b5c-119">Azure AD 執行下列動作，驗證使用者是否能夠使用這項功能：</span><span class="sxs-lookup"><span data-stu-id="14b5c-119">Azure AD verifies if the user is able to use this feature by doing the following:</span></span>
   * <span data-ttu-id="14b5c-120">檢查使用者是否已啟用這項功能，並已獲得 Azure AD 授權。</span><span class="sxs-lookup"><span data-stu-id="14b5c-120">Checks that the user has this feature enabled and an Azure AD license assigned.</span></span>
     * <span data-ttu-id="14b5c-121">如果使用者未啟用這項功能或未獲得授權，便會要求使用者連絡其系統管理員來重設其密碼。</span><span class="sxs-lookup"><span data-stu-id="14b5c-121">If the user does not have this feature enabled or a license assigned, the user is asked to contact their administrator to reset their password.</span></span>
   * <span data-ttu-id="14b5c-122">檢查使用者是否已按照系統管理員原則在其帳戶上定義正確的查問資料。</span><span class="sxs-lookup"><span data-stu-id="14b5c-122">Checks that the user has the right challenge data defined on their account in accordance with administrator policy.</span></span>
     * <span data-ttu-id="14b5c-123">如果原則只需要一項查問，則表示使用者必定已針對系統管理員原則所啟用的至少一項查問定義適當的資料。</span><span class="sxs-lookup"><span data-stu-id="14b5c-123">If policy requires only one challenge, then it is ensured that the user has the appropriate data defined for at least one of the challenges enabled by the administrator policy.</span></span>
       * <span data-ttu-id="14b5c-124">如果使用者未進行設定，便會建議使用者連絡其系統管理員來重設其密碼。</span><span class="sxs-lookup"><span data-stu-id="14b5c-124">If the user is not configured, then the user is advised to contact their administrator to reset their password.</span></span>
     * <span data-ttu-id="14b5c-125">如果原則需要兩項查問，則表示使用者必定已針對系統管理員原則所啟用的至少兩項查問定義適當的資料。</span><span class="sxs-lookup"><span data-stu-id="14b5c-125">If the policy requires two challenges, then it is ensured that the user has the appropriate data defined for at least two of the challenges enabled by the administrator policy.</span></span>
       * <span data-ttu-id="14b5c-126">如果使用者未進行設定，我們便會建議使用者連絡其系統管理員來重設其密碼。</span><span class="sxs-lookup"><span data-stu-id="14b5c-126">If the user is not configured, then we the user is advised to contact their administrator to reset their password.</span></span>
   * <span data-ttu-id="14b5c-127">檢查使用者的密碼是否在內部部署進行管理 (同盟或密碼雜湊同步)。</span><span class="sxs-lookup"><span data-stu-id="14b5c-127">Checks if the user’s password is managed on premises (federated or password hash synchronized).</span></span>
     * <span data-ttu-id="14b5c-128">如果在內部部署中有部署回寫和管理使用者的密碼，則允許使用者進行驗證及重設其密碼。</span><span class="sxs-lookup"><span data-stu-id="14b5c-128">If writeback is deployed and the user’s password is managed on premises, then the user is allowed to proceed to authenticate and reset their password.</span></span>
     * <span data-ttu-id="14b5c-129">如果在內部部署中未部署回寫但有管理使用者的密碼，則會要求使用者連絡其系統管理員來重設其密碼。</span><span class="sxs-lookup"><span data-stu-id="14b5c-129">If writeback is not deployed and the user’s password is managed on premises, then the user is asked to contact their administrator to reset their password.</span></span>
5. <span data-ttu-id="14b5c-130">如果判斷使用者能夠成功重設其密碼，則會引導使用者完成重設程序。</span><span class="sxs-lookup"><span data-stu-id="14b5c-130">If it is determined that the user is able to successfully reset their password, then the user is guided through the reset process.</span></span>

## <a name="authentication-methods"></a><span data-ttu-id="14b5c-131">驗證方法</span><span class="sxs-lookup"><span data-stu-id="14b5c-131">Authentication methods</span></span>

<span data-ttu-id="14b5c-132">如果已啟用自助式密碼重設 (SSPR)，您必須針對驗證方法至少選取下面其中一個選項。</span><span class="sxs-lookup"><span data-stu-id="14b5c-132">If Self-Service Password Reset (SSPR) is enabled, you must select at least one of the following options for authentication methods.</span></span> <span data-ttu-id="14b5c-133">我們強烈建議選擇至少兩個驗證方法，您的使用者才有更大的彈性。</span><span class="sxs-lookup"><span data-stu-id="14b5c-133">We highly recommend choosing at least two authentication methods so that your users have more flexibility.</span></span>

* <span data-ttu-id="14b5c-134">電子郵件</span><span class="sxs-lookup"><span data-stu-id="14b5c-134">Email</span></span>
* <span data-ttu-id="14b5c-135">行動電話</span><span class="sxs-lookup"><span data-stu-id="14b5c-135">Mobile Phone</span></span>
* <span data-ttu-id="14b5c-136">辦公室電話</span><span class="sxs-lookup"><span data-stu-id="14b5c-136">Office Phone</span></span>
* <span data-ttu-id="14b5c-137">安全性問題</span><span class="sxs-lookup"><span data-stu-id="14b5c-137">Security Questions</span></span>

### <a name="what-fields-are-used-in-the-directory-for-authentication-data"></a><span data-ttu-id="14b5c-138">哪些欄位使用於驗證資料的目錄中</span><span class="sxs-lookup"><span data-stu-id="14b5c-138">What fields are used in the directory for authentication data</span></span>

* <span data-ttu-id="14b5c-139">辦公室電話對應至辦公室電話</span><span class="sxs-lookup"><span data-stu-id="14b5c-139">Office Phone corresponds to Office Phone</span></span>
    * <span data-ttu-id="14b5c-140">使用者本身無法設定此欄位，該欄位必須由系統管理員定義</span><span class="sxs-lookup"><span data-stu-id="14b5c-140">Users are unable to set this field themselves it must be defined by an administrator</span></span>
* <span data-ttu-id="14b5c-141">行動電話對應至驗證電話 (非公開可見) 或行動電話 (公開可見)</span><span class="sxs-lookup"><span data-stu-id="14b5c-141">Mobile Phone corresponds to either Authentication Phone (not publicly visible) or Mobile Phone (publicly visible)</span></span>
    * <span data-ttu-id="14b5c-142">服務會先尋找驗證電話，如果找不到，則會退回到行動電話</span><span class="sxs-lookup"><span data-stu-id="14b5c-142">The service looks for Authentication Phone first, then falls back to Mobile Phone if not present</span></span>
* <span data-ttu-id="14b5c-143">替代電子郵件地址對應至驗證電子郵件 (非公開可見) 或替代電子郵件</span><span class="sxs-lookup"><span data-stu-id="14b5c-143">Alternate Email Address corresponds to either Authentication Email (not publicly visible) or Alternate Email</span></span>
    * <span data-ttu-id="14b5c-144">服務會先尋找驗證電子郵件，然後退回到替代電子郵件</span><span class="sxs-lookup"><span data-stu-id="14b5c-144">The service looks for Authentication Email first, then fails back to Alternate Email</span></span>

<span data-ttu-id="14b5c-145">依預設，只有雲端屬性辦公室電話和行動電話會從驗證資料的內部部署目錄同步處理至您的雲端目錄。</span><span class="sxs-lookup"><span data-stu-id="14b5c-145">By default, only the cloud attributes Office Phone and Mobile Phone are synchronized to your cloud directory from your on-premises directory for authentication data.</span></span>

<span data-ttu-id="14b5c-146">使用者只有在系統管理員已啟用且要求的驗證方法中有資料存在時，才能夠重設其密碼。</span><span class="sxs-lookup"><span data-stu-id="14b5c-146">Users can only reset their password if they have data present in the authentication methods that the administrator has enabled and requires.</span></span>

<span data-ttu-id="14b5c-147">如果使用者不想要在目錄中顯示行動電話號碼，但仍想要將它使用於密碼重設，系統管理員不得在目錄中填入該行動電話號碼，而使用者應透過[密碼重設註冊入口網站](http://aka.ms/ssprsetup)填入其 [驗證電話] 屬性。</span><span class="sxs-lookup"><span data-stu-id="14b5c-147">If users do not want their mobile phone number to be visible in the directory but would still like to use it for password reset, administrators should not populate it in the directory and the user should then populate their **Authentication Phone** attribute via the [password reset registration portal](http://aka.ms/ssprsetup).</span></span> <span data-ttu-id="14b5c-148">系統管理員可以在使用者的設定檔中看到此資訊，但該資訊不會發佈在其他地方。</span><span class="sxs-lookup"><span data-stu-id="14b5c-148">Administrators can see this information in the user's profile but it is not published elsewhere.</span></span> <span data-ttu-id="14b5c-149">如果 Azure 系統管理員帳戶註冊其驗證電話號碼，該號碼會填入行動電話欄位中並顯示出來。</span><span class="sxs-lookup"><span data-stu-id="14b5c-149">If an Azure Administrator account registers their authentication phone number, it is populated into the mobile phone field and is visible.</span></span>

### <a name="number-of-authentication-methods-required"></a><span data-ttu-id="14b5c-150">必要驗證方法數目</span><span class="sxs-lookup"><span data-stu-id="14b5c-150">Number of authentication methods required</span></span>

<span data-ttu-id="14b5c-151">此選項可判斷使用者必須通過才能重設或將其密碼解除鎖定的可用驗證方法數目下限，並可設定為 1 或 2。</span><span class="sxs-lookup"><span data-stu-id="14b5c-151">This option determines the minimum number of the available authentication methods a user must go through to reset or unlock their password and can be set to either 1 or 2.</span></span>

<span data-ttu-id="14b5c-152">使用者可以選擇提供更多驗證方法 (如果是由系統管理員啟用)。</span><span class="sxs-lookup"><span data-stu-id="14b5c-152">Users can choose to supply more authentication methods if they are enabled by the administrator.</span></span>

<span data-ttu-id="14b5c-153">如果使用者並未註冊所需的最少方法，他們會看到錯誤頁面，引導他們要求系統管理員重設其密碼。</span><span class="sxs-lookup"><span data-stu-id="14b5c-153">If a user does not have the minimum required methods registered, they see an error page that directs them to request an administrator to reset their password.</span></span>

### <a name="how-secure-are-my-security-questions"></a><span data-ttu-id="14b5c-154">我的安全性問題有多安全</span><span class="sxs-lookup"><span data-stu-id="14b5c-154">How secure are my security questions</span></span>

<span data-ttu-id="14b5c-155">如果您使用安全性問題，我們建議搭配其他方法使用這些問題，因為它們可能會比其他方法更不安全，原因是有些人可能知道其他使用者問題的答案。</span><span class="sxs-lookup"><span data-stu-id="14b5c-155">If you use security questions, we recommend them in use with another method as they can be less secure than other methods since some people may know the answers to another users questions.</span></span>

> [!NOTE] 
> <span data-ttu-id="14b5c-156">安全性問題會私密且安全地儲存在目錄中的使用者物件上，只能在註冊期間由使用者回答。</span><span class="sxs-lookup"><span data-stu-id="14b5c-156">Security questions are stored privately and securely on a user object in the directory and can only be answered by users during registration.</span></span> <span data-ttu-id="14b5c-157">系統管理員無法讀取或修改使用者問題或答案。</span><span class="sxs-lookup"><span data-stu-id="14b5c-157">There is no way for an administrator to read or modify a users questions or answers.</span></span>
>

### <a name="security-question-localization"></a><span data-ttu-id="14b5c-158">安全性問題當地語系化</span><span class="sxs-lookup"><span data-stu-id="14b5c-158">Security question localization</span></span>

<span data-ttu-id="14b5c-159">下列所有預先定義的問題會依據使用者的瀏覽器地區設定，當地語系化成完整的 O365 語言集。</span><span class="sxs-lookup"><span data-stu-id="14b5c-159">All predefined questions that follow are localized into the full set of Office 365 languages based on the user's browser locale.</span></span>

* <span data-ttu-id="14b5c-160">您在哪個城市遇見第一個配偶/伴侶？</span><span class="sxs-lookup"><span data-stu-id="14b5c-160">In what city did you meet your first spouse/partner?</span></span>
* <span data-ttu-id="14b5c-161">您的父母在哪個城市相遇？</span><span class="sxs-lookup"><span data-stu-id="14b5c-161">In what city did your parents meet?</span></span>
* <span data-ttu-id="14b5c-162">您最親近的手足住在哪個城市？</span><span class="sxs-lookup"><span data-stu-id="14b5c-162">In what city does your nearest sibling live?</span></span>
* <span data-ttu-id="14b5c-163">您的父親在哪個城市出生？</span><span class="sxs-lookup"><span data-stu-id="14b5c-163">In what city was your father born?</span></span>
* <span data-ttu-id="14b5c-164">您的第一份工作是在哪個城市？</span><span class="sxs-lookup"><span data-stu-id="14b5c-164">In what city was your first job?</span></span>
* <span data-ttu-id="14b5c-165">您的母親在哪個城市出生？</span><span class="sxs-lookup"><span data-stu-id="14b5c-165">In what city was your mother born?</span></span>
* <span data-ttu-id="14b5c-166">您在哪個城市渡過 2000 年的新年？</span><span class="sxs-lookup"><span data-stu-id="14b5c-166">What city were you in on New Year's 2000?</span></span>
* <span data-ttu-id="14b5c-167">您最喜愛的中學老師姓什麼？</span><span class="sxs-lookup"><span data-stu-id="14b5c-167">What is the last name of your favorite teacher in high * school?</span></span>
* <span data-ttu-id="14b5c-168">您已申請但未就讀的大專名稱為何？</span><span class="sxs-lookup"><span data-stu-id="14b5c-168">What is the name of a college you applied to but didn't attend?</span></span>
* <span data-ttu-id="14b5c-169">您舉辦第一次婚宴的地點名稱為何？</span><span class="sxs-lookup"><span data-stu-id="14b5c-169">What is the name of the place in which you held your first wedding reception?</span></span>
* <span data-ttu-id="14b5c-170">您父親的中間名是什麼？</span><span class="sxs-lookup"><span data-stu-id="14b5c-170">What is your father's middle name?</span></span>
* <span data-ttu-id="14b5c-171">您最愛的食物是什麼？</span><span class="sxs-lookup"><span data-stu-id="14b5c-171">What is your favorite food?</span></span>
* <span data-ttu-id="14b5c-172">您外婆的姓名為何？</span><span class="sxs-lookup"><span data-stu-id="14b5c-172">What is your maternal grandmother's first and last name?</span></span>
* <span data-ttu-id="14b5c-173">您母親的中間名是什麼？</span><span class="sxs-lookup"><span data-stu-id="14b5c-173">What is your mother's middle name?</span></span>
* <span data-ttu-id="14b5c-174">您最年長手足的生日月份和年度為何？</span><span class="sxs-lookup"><span data-stu-id="14b5c-174">What is your oldest sibling's birthday month and year?</span></span> <span data-ttu-id="14b5c-175">(例如 1985 年 11 月)</span><span class="sxs-lookup"><span data-stu-id="14b5c-175">(e.g. November 1985)</span></span>
* <span data-ttu-id="14b5c-176">您最年長手足的中間名是什麼？</span><span class="sxs-lookup"><span data-stu-id="14b5c-176">What is your oldest sibling's middle name?</span></span>
* <span data-ttu-id="14b5c-177">您祖父的姓名為何？</span><span class="sxs-lookup"><span data-stu-id="14b5c-177">What is your paternal grandfather's first and last name?</span></span>
* <span data-ttu-id="14b5c-178">您最年幼手足的中間名稱是什麼？</span><span class="sxs-lookup"><span data-stu-id="14b5c-178">What is your youngest sibling's middle name?</span></span>
* <span data-ttu-id="14b5c-179">您六年級時就讀哪間學校？</span><span class="sxs-lookup"><span data-stu-id="14b5c-179">What school did you attend for sixth grade?</span></span>
* <span data-ttu-id="14b5c-180">您童年最要好朋友的姓名為何？</span><span class="sxs-lookup"><span data-stu-id="14b5c-180">What was the first and last name of your childhood best friend?</span></span>
* <span data-ttu-id="14b5c-181">您第一個密友的姓名為何？</span><span class="sxs-lookup"><span data-stu-id="14b5c-181">What was the first and last name of your first significant other?</span></span>
* <span data-ttu-id="14b5c-182">您最喜愛的小學老師姓什麼？</span><span class="sxs-lookup"><span data-stu-id="14b5c-182">What was the last name of your favorite grade school teacher?</span></span>
* <span data-ttu-id="14b5c-183">第一輛汽車或機車的製造商和型號為何？</span><span class="sxs-lookup"><span data-stu-id="14b5c-183">What was the make and model of your first car or motorcycle?</span></span>
* <span data-ttu-id="14b5c-184">您就讀的第一所學校名稱為何？</span><span class="sxs-lookup"><span data-stu-id="14b5c-184">What was the name of the first school you attended?</span></span>
* <span data-ttu-id="14b5c-185">您出生的醫院名稱為何？</span><span class="sxs-lookup"><span data-stu-id="14b5c-185">What was the name of the hospital in which you were born?</span></span>
* <span data-ttu-id="14b5c-186">您兒時第一個家的街道名稱為何？</span><span class="sxs-lookup"><span data-stu-id="14b5c-186">What was the name of the street of your first childhood home?</span></span>
* <span data-ttu-id="14b5c-187">您的童年英雄名稱為何？</span><span class="sxs-lookup"><span data-stu-id="14b5c-187">What was the name of your childhood hero?</span></span>
* <span data-ttu-id="14b5c-188">您最喜愛的娃娃名稱為何？</span><span class="sxs-lookup"><span data-stu-id="14b5c-188">What was the name of your favorite stuffed animal?</span></span>
* <span data-ttu-id="14b5c-189">您第一隻寵物的名稱為何？</span><span class="sxs-lookup"><span data-stu-id="14b5c-189">What was the name of your first pet?</span></span>
* <span data-ttu-id="14b5c-190">您童年時期的綽號是什麼？</span><span class="sxs-lookup"><span data-stu-id="14b5c-190">What was your childhood nickname?</span></span>
* <span data-ttu-id="14b5c-191">您中學最喜愛的運動是什麼？</span><span class="sxs-lookup"><span data-stu-id="14b5c-191">What was your favorite sport in high school?</span></span>
* <span data-ttu-id="14b5c-192">您的第一份工作是什麼？</span><span class="sxs-lookup"><span data-stu-id="14b5c-192">What was your first job?</span></span>
* <span data-ttu-id="14b5c-193">您兒時電話號碼的末四碼是什麼？</span><span class="sxs-lookup"><span data-stu-id="14b5c-193">What were the last four digits of your childhood telephone number?</span></span>
* <span data-ttu-id="14b5c-194">在您年輕時，您長大想做什麼？</span><span class="sxs-lookup"><span data-stu-id="14b5c-194">When you were young, what did you want to be when you grew up?</span></span>
* <span data-ttu-id="14b5c-195">您遇過最有名的人物是誰？</span><span class="sxs-lookup"><span data-stu-id="14b5c-195">Who is the most famous person you have ever met?</span></span>

### <a name="custom-security-questions"></a><span data-ttu-id="14b5c-196">自訂安全性問題</span><span class="sxs-lookup"><span data-stu-id="14b5c-196">Custom security questions</span></span>

<span data-ttu-id="14b5c-197">自訂安全性問題不會針對不同的地區設定進行當地語系化。</span><span class="sxs-lookup"><span data-stu-id="14b5c-197">Custom security questions are not localized for different locales.</span></span> <span data-ttu-id="14b5c-198">所有自訂問題會以您在系統管理使用者介面中輸入它們的語言顯示，即使使用者的瀏覽器地區設定不同。</span><span class="sxs-lookup"><span data-stu-id="14b5c-198">All custom questions are displayed in the same language they are entered in the administrative user interface even if the user's browser locale is different.</span></span> <span data-ttu-id="14b5c-199">如果您需要已當地語系化的問題，請使用預先定義的問題。</span><span class="sxs-lookup"><span data-stu-id="14b5c-199">If you need localized questions, please use the predefined questions.</span></span>

<span data-ttu-id="14b5c-200">自訂安全性問題的長度上限為 200 個字元。</span><span class="sxs-lookup"><span data-stu-id="14b5c-200">The maximum length of a custom security question is 200 characters.</span></span>

### <a name="security-question-requirements"></a><span data-ttu-id="14b5c-201">安全性問題需求</span><span class="sxs-lookup"><span data-stu-id="14b5c-201">Security question requirements</span></span>

* <span data-ttu-id="14b5c-202">答案字元限制下限為 3 個字元。</span><span class="sxs-lookup"><span data-stu-id="14b5c-202">Minimum answer character limit is 3 characters</span></span>
* <span data-ttu-id="14b5c-203">答案字元限制上限為 40 個字元。</span><span class="sxs-lookup"><span data-stu-id="14b5c-203">Maximum answer character limit is 40 characters</span></span>
* <span data-ttu-id="14b5c-204">使用者不能回答相同的問題一次以上。</span><span class="sxs-lookup"><span data-stu-id="14b5c-204">Users may not answer the same question more than one time</span></span>
* <span data-ttu-id="14b5c-205">使用者不能對一個以上的問題提供相同的答案。</span><span class="sxs-lookup"><span data-stu-id="14b5c-205">Users may not provide the same answer to more than one question</span></span>
* <span data-ttu-id="14b5c-206">可以使用任何字元集來定義問題和答案 (包括 Unicode 字元)。</span><span class="sxs-lookup"><span data-stu-id="14b5c-206">Any character set may be used to define questions and answers including Unicode characters</span></span>
* <span data-ttu-id="14b5c-207">定義的的問題數目必須大於或等於註冊所需的問題數目。</span><span class="sxs-lookup"><span data-stu-id="14b5c-207">The number of questions defined must be greater than or equal to the number of questions required to register</span></span>

## <a name="registration"></a><span data-ttu-id="14b5c-208">註冊</span><span class="sxs-lookup"><span data-stu-id="14b5c-208">Registration</span></span>

### <a name="require-users-to-register-when-signing-in"></a><span data-ttu-id="14b5c-209">登入時要求使用者註冊</span><span class="sxs-lookup"><span data-stu-id="14b5c-209">Require users to register when signing in</span></span>

<span data-ttu-id="14b5c-210">如果已啟用密碼重設的使用者使用 Azure AD 登入應用程式，進而登入下列各項，則啟用此選項會要求他們完成密碼重設註冊︰</span><span class="sxs-lookup"><span data-stu-id="14b5c-210">Enabling this option requires a user who is enabled for password reset to complete the password reset registration if they login to applications using Azure AD to sign in like those that follow:</span></span>

* <span data-ttu-id="14b5c-211">Office 365</span><span class="sxs-lookup"><span data-stu-id="14b5c-211">Office 365</span></span>
* <span data-ttu-id="14b5c-212">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="14b5c-212">Azure portal</span></span>
* <span data-ttu-id="14b5c-213">存取面板</span><span class="sxs-lookup"><span data-stu-id="14b5c-213">Access Panel</span></span>
* <span data-ttu-id="14b5c-214">同盟應用程式</span><span class="sxs-lookup"><span data-stu-id="14b5c-214">Federated applications</span></span>
* <span data-ttu-id="14b5c-215">使用 Azure AD 自訂應用程式</span><span class="sxs-lookup"><span data-stu-id="14b5c-215">Custom applications using Azure AD</span></span>

<span data-ttu-id="14b5c-216">停用這項功能仍可讓使用者手動註冊其連絡資訊，方法是造訪 [http://aka.ms/ssprsetup](http://aka.ms/ssprsetup) 或按一下存取面板中 [設定檔] 索引標籤底下的**註冊密碼重設**連結。</span><span class="sxs-lookup"><span data-stu-id="14b5c-216">Disabling this feature will still allow users to manually register their contact information by visiting [http://aka.ms/ssprsetup](http://aka.ms/ssprsetup) or by clicking the **register for password reset** link under the profile tab in the access panel.</span></span>

> [!NOTE]
> <span data-ttu-id="14b5c-217">使用者可以按一下 [取消] 或關閉視窗來關閉密碼重設註冊入口網站，但每次登入時都會出現提示，直到他們完成註冊為止。</span><span class="sxs-lookup"><span data-stu-id="14b5c-217">Users can dismiss the password reset registration portal by clicking cancel or closing the window but are prompted each time they login until they complete registration.</span></span>
>

### <a name="number-of-days-before-users-are-asked-to-reconfirm-their-authentication-information"></a><span data-ttu-id="14b5c-218">要求使用者重新確認其驗證資訊的等候天數</span><span class="sxs-lookup"><span data-stu-id="14b5c-218">Number of days before users are asked to reconfirm their authentication information</span></span>

<span data-ttu-id="14b5c-219">此選項可決定設定和重新確認驗證資訊之間的期間，且只有在您啟用 [登入時要求使用者註冊] 選項才可以使用。</span><span class="sxs-lookup"><span data-stu-id="14b5c-219">This option determines the period of time between setting and reconfirming authentication information and is only available if you enable the **require users to register when signing in** option.</span></span>

<span data-ttu-id="14b5c-220">有效值為 0-730 天，0 表示從未要求使用者重新確認其驗證資訊</span><span class="sxs-lookup"><span data-stu-id="14b5c-220">Valid values are 0-730 days with 0 meaning never ask users to reconfirm their authentication information</span></span>

## <a name="notifications"></a><span data-ttu-id="14b5c-221">通知</span><span class="sxs-lookup"><span data-stu-id="14b5c-221">Notifications</span></span>

### <a name="notify-users-on-password-resets"></a><span data-ttu-id="14b5c-222">通知使用者密碼重設</span><span class="sxs-lookup"><span data-stu-id="14b5c-222">Notify users on password resets</span></span>

<span data-ttu-id="14b5c-223">如果此選項設定為 [是]，則正在重設其密碼的使用者會收到一封電子郵件 (送至 Azure AD 中歸檔的主要和替代電子郵件地址)，通知他們已透過 SSPR 入口網站其密碼變更。</span><span class="sxs-lookup"><span data-stu-id="14b5c-223">If this option is set to yes, then the user who is resetting their password receives an email notifying them that their password has been changed via the SSPR portal to their primary and alternate email addresses on file in Azure AD.</span></span> <span data-ttu-id="14b5c-224">沒有人會接獲此重設事件的通知。</span><span class="sxs-lookup"><span data-stu-id="14b5c-224">No one else is notified of this reset event.</span></span>

### <a name="notify-all-admins-when-other-admins-reset-their-passwords"></a><span data-ttu-id="14b5c-225">當其他系統管理員重設其密碼時通知所有系統管理員</span><span class="sxs-lookup"><span data-stu-id="14b5c-225">Notify all admins when other admins reset their passwords</span></span>

<span data-ttu-id="14b5c-226">如果此選項設定為 [是]，則**所有系統管理員**會收到一封電子郵件 (送至 Azure AD 中歸檔的主要電子郵件地址)，通知他們其他系統管理員已使用 SSPR 變更其密碼。</span><span class="sxs-lookup"><span data-stu-id="14b5c-226">If this option is set to yes, then **all administrators** receive an email to their primary email address on file in Azure AD notifying them that another administrator has changed their password using SSPR.</span></span>

<span data-ttu-id="14b5c-227">範例︰環境中有四個系統管理員。</span><span class="sxs-lookup"><span data-stu-id="14b5c-227">Example: There are four administrators in an environment.</span></span> <span data-ttu-id="14b5c-228">系統管理員 "A" 使用 SSPR 重設其密碼。</span><span class="sxs-lookup"><span data-stu-id="14b5c-228">Administrator "A" resets their password using SSPR.</span></span> <span data-ttu-id="14b5c-229">系統管理員 B、C 和 D 收到一封電子郵件，警示他們發生此狀況。</span><span class="sxs-lookup"><span data-stu-id="14b5c-229">Administrators B, C, and D receive an email alerting them of this happening.</span></span>

## <a name="on-premises-integration"></a><span data-ttu-id="14b5c-230">內部部署整合</span><span class="sxs-lookup"><span data-stu-id="14b5c-230">On-premises integration</span></span>

<span data-ttu-id="14b5c-231">如果您已安裝、設定及啟用 Azure AD Connect，您會有其他的內部部署整合選項。</span><span class="sxs-lookup"><span data-stu-id="14b5c-231">If you have installed, configured, and enabled Azure AD Connect you will have additional options for on-premises integrations.</span></span>

### <a name="write-back-passwords-to-your-on-premises-directory"></a><span data-ttu-id="14b5c-232">將密碼寫回至內部部署目錄</span><span class="sxs-lookup"><span data-stu-id="14b5c-232">Write back passwords to your on-premises directory</span></span>

<span data-ttu-id="14b5c-233">控制是否對此目錄啟用密碼回寫，如果回寫開啟，則表示內部部署回寫服務的狀態。</span><span class="sxs-lookup"><span data-stu-id="14b5c-233">Controls whether or not password writeback is enabled for this directory and, if writeback is on, indicates the status of the on-premises writeback service.</span></span> <span data-ttu-id="14b5c-234">如果您想要暫時停用密碼回寫，而不重新設定 Azure AD Connect，此設定就很有用。</span><span class="sxs-lookup"><span data-stu-id="14b5c-234">This is useful if you want to temporarily disable the password writeback without re-configuring Azure AD Connect.</span></span>

* <span data-ttu-id="14b5c-235">如果此參數設定為 [是]，則回寫會啟用，而且同盟和密碼雜湊同步使用者可以重設其密碼。</span><span class="sxs-lookup"><span data-stu-id="14b5c-235">If the switch is set to yes, then writeback will be enabled, and federated and password hash synchronized users will be able to reset their passwords.</span></span>
* <span data-ttu-id="14b5c-236">如果此參數設定為 [否]，則回寫會停用，而且同盟和密碼雜湊同步使用者將無法重設其密碼。</span><span class="sxs-lookup"><span data-stu-id="14b5c-236">If the switch is set to no, then writeback will be disabled, and federated and password hash synchronized users will not be able to reset their passwords.</span></span>

### <a name="allow-users-to-unlock-accounts-without-resetting-their-password"></a><span data-ttu-id="14b5c-237">允許使用者在不重設密碼的情況下解除鎖定帳戶</span><span class="sxs-lookup"><span data-stu-id="14b5c-237">Allow users to unlock accounts without resetting their password</span></span>

<span data-ttu-id="14b5c-238">指定是否應為瀏覽密碼重設入口網站的使用者提供選項，讓他們在不重設密碼的情況下解除鎖定內部部署的 Active Directory 帳戶。</span><span class="sxs-lookup"><span data-stu-id="14b5c-238">Designates whether or not users who visit the password reset portal should be given the option to unlock their on-premises Active Directory accounts without resetting their password.</span></span> <span data-ttu-id="14b5c-239">根據預設，Azure AD 執行密碼重設時會一律解除鎖定帳戶，此設定可讓您區隔這兩項作業。</span><span class="sxs-lookup"><span data-stu-id="14b5c-239">By default, Azure AD will always unlock accounts when performing a password reset, this setting allows you to separate those two operations.</span></span> 

* <span data-ttu-id="14b5c-240">如果設為「是」，會提供使用者重設其密碼以解除鎖定帳戶的選項，或是在不重設密碼的情況下解除鎖定的選項。</span><span class="sxs-lookup"><span data-stu-id="14b5c-240">If set to “yes”, then users will be given the option to reset their password and unlock the account, or to unlock without resetting the password.</span></span>
* <span data-ttu-id="14b5c-241">如果設定為「否」，使用者將只能執行合併的密碼重設和帳戶解除鎖定作業。</span><span class="sxs-lookup"><span data-stu-id="14b5c-241">If set to “no”, then users will only be able to perform a combined password reset and account unlock operation.</span></span>

## <a name="network-requirements"></a><span data-ttu-id="14b5c-242">網路需求</span><span class="sxs-lookup"><span data-stu-id="14b5c-242">Network requirements</span></span>

### <a name="firewall-rules"></a><span data-ttu-id="14b5c-243">防火牆規則</span><span class="sxs-lookup"><span data-stu-id="14b5c-243">Firewall rules</span></span>

[<span data-ttu-id="14b5c-244">Microsoft Office URL 和 IP 位址清單</span><span class="sxs-lookup"><span data-stu-id="14b5c-244">List of Microsoft Office URLs and IP addresses</span></span>](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2)

<span data-ttu-id="14b5c-245">對於 Azure AD Connect 1.1.443.0 版和更新版本，您需要擁有下列各項的輸出 HTTPS 存取權：</span><span class="sxs-lookup"><span data-stu-id="14b5c-245">For Azure AD Connect version 1.1.443.0 and above, you need outbound HTTPS access to the following</span></span>
* <span data-ttu-id="14b5c-246">passwordreset.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="14b5c-246">passwordreset.microsoftonline.com</span></span>
* <span data-ttu-id="14b5c-247">servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="14b5c-247">servicebus.windows.net</span></span>

<span data-ttu-id="14b5c-248">如需更細微的存取，您可以在[這裡](https://www.microsoft.com/download/details.aspx?id=41653)找到已更新的 Microsoft Azure 資料中心 IP 範圍清單，該清單會每個星期三進行更新並在下一個星期一生效。</span><span class="sxs-lookup"><span data-stu-id="14b5c-248">For more granular access, you can find the updated list of Microsoft Azure Datacenter IP Ranges that is updated every Wednesday and put into effect the following Monday [here](https://www.microsoft.com/download/details.aspx?id=41653).</span></span>

### <a name="idle-connection-timeouts"></a><span data-ttu-id="14b5c-249">閒置連線逾時</span><span class="sxs-lookup"><span data-stu-id="14b5c-249">Idle connection timeouts</span></span>

<span data-ttu-id="14b5c-250">Azure AD Connect 工具會傳送定期 ping/keepalives 至服務匯流排端點，以確保連線保持作用中。</span><span class="sxs-lookup"><span data-stu-id="14b5c-250">The Azure AD Connect tool sends periodic pings/keepalives to ServiceBus endpoints to ensure that the connections stay alive.</span></span> <span data-ttu-id="14b5c-251">工具偵測到太多的連線應該被終止時，它就會自動增加 ping 至端點的頻率。</span><span class="sxs-lookup"><span data-stu-id="14b5c-251">Should the tool detect that too many connections are being killed, it will automatically increase the frequency of pings to the endpoint.</span></span> <span data-ttu-id="14b5c-252">最低「ping 間隔」會下滑至每隔 60 秒 1 ping，不過，我們強烈建議讓 proxy/防火牆允許保存閒置連線至少 2-3 分鐘。</span><span class="sxs-lookup"><span data-stu-id="14b5c-252">The lowest 'ping intervals' drops to is 1 ping every 60 seconds, however, we strongly advise that proxies/firewalls allow idle connections to persist for at least 2-3 minutes.</span></span> <span data-ttu-id="14b5c-253">*針對較舊版本，建議 4 分鐘以上。</span><span class="sxs-lookup"><span data-stu-id="14b5c-253">*For older versions, we suggest four minutes or more.</span></span>

## <a name="active-directory-permissions"></a><span data-ttu-id="14b5c-254">Active Directory 權限</span><span class="sxs-lookup"><span data-stu-id="14b5c-254">Active Directory permissions</span></span>

<span data-ttu-id="14b5c-255">Azure AD Connect 公用程式中指定的帳戶必須具有重設密碼、變更密碼、lockoutTime 寫入權限和 pwdLastSet 寫入權限，以及該樹系中**每個網域**之根物件**或**您希望在 SSPR 範圍內之使用者 OU 的延伸權限。</span><span class="sxs-lookup"><span data-stu-id="14b5c-255">The account specified in the Azure AD Connect utility must have Reset Password, Change Password, Write Permissions on lockoutTime, and Write Permissions on pwdLastSet, extended rights on either the root object of **each domain** in that forest **OR** on the user OUs you wish to be in scope for SSPR.</span></span>

<span data-ttu-id="14b5c-256">如果您不確定上述指的是哪些帳戶，請開啟 Azure Active Directory Connect 組態 UI，然後按一下 [檢視目前的組態] 選項。</span><span class="sxs-lookup"><span data-stu-id="14b5c-256">If you are not sure what account the above refers to, open the Azure Active Directory Connect configuration UI and click the View current configuration option.</span></span> <span data-ttu-id="14b5c-257">您需要新增權限的帳戶會列在 [已同步處理的目錄] 底下。</span><span class="sxs-lookup"><span data-stu-id="14b5c-257">The account you need to add permission to is listed under "Synchronized Directories"</span></span>

<span data-ttu-id="14b5c-258">設定這些權限會允許每個樹系的 MA 服務帳戶代表該樹系內的使用者帳戶管理密碼。</span><span class="sxs-lookup"><span data-stu-id="14b5c-258">Setting these permissions allows the MA service account for each forest to manage passwords on behalf of user accounts within that forest.</span></span> <span data-ttu-id="14b5c-259">**如果您沒有指定這些權限，則即使回寫看起來設定正確，使用者在嘗試從雲端管理其內部部署密碼時還是會遇到錯誤。**</span><span class="sxs-lookup"><span data-stu-id="14b5c-259">**If you neglect to assign these permissions, then, even though writeback appears to be configured correctly, users encounter errors when attempting to manage their on-premises passwords from the cloud.**</span></span>

> [!NOTE]
> <span data-ttu-id="14b5c-260">最多可能需要一小時讓這些權限複寫至您的目錄中的所有物件。</span><span class="sxs-lookup"><span data-stu-id="14b5c-260">It could take up to an hour or more for these permissions to replicate to all objects in your directory.</span></span>
>

<span data-ttu-id="14b5c-261">若要設定適當權限以進行密碼回寫：</span><span class="sxs-lookup"><span data-stu-id="14b5c-261">To set up the appropriate permissions for password writeback to occur</span></span>

1. <span data-ttu-id="14b5c-262">以具有適當網域管理權限的帳戶開啟 [Active Directory 使用者和電腦]。</span><span class="sxs-lookup"><span data-stu-id="14b5c-262">Open Active Directory Users and Computers with an account that has the appropriate domain administration permissions</span></span>
2. <span data-ttu-id="14b5c-263">從 [檢視] 功能表，確定 [進階功能] 已開啟。</span><span class="sxs-lookup"><span data-stu-id="14b5c-263">From the View menu, make sure Advanced Features is turned on</span></span>
3. <span data-ttu-id="14b5c-264">在左面板中，以滑鼠右鍵按一下代表網域根目錄的物件並選擇屬性。</span><span class="sxs-lookup"><span data-stu-id="14b5c-264">In the left panel, right-click the object that represents the root of the domain and choose properties</span></span>
    * <span data-ttu-id="14b5c-265">按一下 [安全性] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="14b5c-265">Click the Security tab</span></span>
    * <span data-ttu-id="14b5c-266">然後按一下 [進階]。</span><span class="sxs-lookup"><span data-stu-id="14b5c-266">Then click Advanced.</span></span>
4. <span data-ttu-id="14b5c-267">從 [權限] 索引標籤，按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="14b5c-267">From the Permissions tab, click Add</span></span>
5. <span data-ttu-id="14b5c-268">挑選權限套用至的帳戶 (從 Azure AD Connect 安裝程式)</span><span class="sxs-lookup"><span data-stu-id="14b5c-268">Pick the account that permissions are being applied to (from Azure AD Connect setup)</span></span>
6. <span data-ttu-id="14b5c-269">在 [套用至] 下拉式方塊中選取 [下階使用者] 物件。</span><span class="sxs-lookup"><span data-stu-id="14b5c-269">In the Applies to drop down box select Descendent User objects</span></span>
7. <span data-ttu-id="14b5c-270">在 [權限] 下，核取下列方塊：</span><span class="sxs-lookup"><span data-stu-id="14b5c-270">Under permissions check the boxes for the following</span></span>
    * <span data-ttu-id="14b5c-271">未過期密碼</span><span class="sxs-lookup"><span data-stu-id="14b5c-271">Unexpire-Password</span></span>
    * <span data-ttu-id="14b5c-272">重設密碼</span><span class="sxs-lookup"><span data-stu-id="14b5c-272">Reset Password</span></span>
    * <span data-ttu-id="14b5c-273">變更密碼</span><span class="sxs-lookup"><span data-stu-id="14b5c-273">Change Password</span></span>
    * <span data-ttu-id="14b5c-274">寫入 lockoutTime</span><span class="sxs-lookup"><span data-stu-id="14b5c-274">Write lockoutTime</span></span>
    * <span data-ttu-id="14b5c-275">寫入 pwdLastSet</span><span class="sxs-lookup"><span data-stu-id="14b5c-275">Write pwdLastSet</span></span>
8. <span data-ttu-id="14b5c-276">依序按一下 [套用] / [確定] 進行套用並結束開啟的對話方塊。</span><span class="sxs-lookup"><span data-stu-id="14b5c-276">Click Apply/OK through to apply and exit any open dialog boxes.</span></span>

## <a name="how-does-password-reset-work-for-b2b-users"></a><span data-ttu-id="14b5c-277">B2B 使用者的密碼重設運作方式</span><span class="sxs-lookup"><span data-stu-id="14b5c-277">How does password reset work for B2B users?</span></span>
<span data-ttu-id="14b5c-278">所有 B2B 組態完全支援密碼重設和變更。</span><span class="sxs-lookup"><span data-stu-id="14b5c-278">Password reset and change are fully supported with all B2B configurations.</span></span>  <span data-ttu-id="14b5c-279">閱讀以下內容，以了解密碼重設支援的 3 個明確 B2B 案例。</span><span class="sxs-lookup"><span data-stu-id="14b5c-279">Read below for the three explicit B2B cases supported by password reset.</span></span>

1. <span data-ttu-id="14b5c-280">**來自具備現有 Azure AD 租用戶之合作夥伴組織的使用者** - 如果您合作的組織具備現有的 Azure AD 租用戶，我們會**遵守該租用戶中啟用的任何密碼重設原則**。</span><span class="sxs-lookup"><span data-stu-id="14b5c-280">**Users from a partner org with an existing Azure AD tenant** - If the organization you are partnering with has an existing Azure AD tenant, we **respect whatever password reset policies are enabled in that tenant**.</span></span> <span data-ttu-id="14b5c-281">若要讓密碼重設運作，合作夥伴組織只需要確定 Azure AD SSPR 已啟用，O365 客戶不須另外付費即可使用該功能，而且可以依照[開始使用密碼管理](https://azure.microsoft.com/documentation/articles/active-directory-passwords-getting-started/#enable-users-to-reset-or-change-their-aad-passwords)指南中的步驟加以啟用。</span><span class="sxs-lookup"><span data-stu-id="14b5c-281">For password reset to work, the partner organization just needs to make sure Azure AD SSPR is enabled, which is no additional charge for O365 customers, and can be enabled by following the steps in our [Getting Started with Password Management](https://azure.microsoft.com/documentation/articles/active-directory-passwords-getting-started/#enable-users-to-reset-or-change-their-aad-passwords) guide.</span></span>
2. <span data-ttu-id="14b5c-282">**使用[自助式註冊](active-directory-self-service-signup.md)**功能註冊的使用者 - 如果您合作的組織使用[自助式註冊](active-directory-self-service-signup.md)功能進入租用戶，我們會讓他們利用其註冊的電子郵件進行重設。</span><span class="sxs-lookup"><span data-stu-id="14b5c-282">**Users who signed up using [self-service sign-up](active-directory-self-service-signup.md)** - If the organization you are partnering with used the [self-service sign-up](active-directory-self-service-signup.md) feature to get into a tenant, we let them reset with the email they registered.</span></span>
3. <span data-ttu-id="14b5c-283">**B2B 使用者** - 任何使用新的 [Azure AD B2B 功能](active-directory-b2b-what-is-azure-ad-b2b.md)建立的新 B2B 使用者，也能夠利用其在邀請程序期間註冊的電子郵件重設其密碼。</span><span class="sxs-lookup"><span data-stu-id="14b5c-283">**B2B users** - Any new B2B users created using the new [Azure AD B2B capabilities](active-directory-b2b-what-is-azure-ad-b2b.md) will also be able to reset their passwords with the email they registered during the invite process.</span></span>

<span data-ttu-id="14b5c-284">若要測試此項，只要隨著其中一個合作夥伴使用者移至 http://passwordreset.microsoftonline.com 即可。</span><span class="sxs-lookup"><span data-stu-id="14b5c-284">To test this, go to http://passwordreset.microsoftonline.com with one of these partner users.</span></span> <span data-ttu-id="14b5c-285">只要他們定義了替代電子郵件或驗證電子郵件，密碼重設就會如預期般運作。</span><span class="sxs-lookup"><span data-stu-id="14b5c-285">As long as they have an alternate email or authentication email defined, password reset works as expected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="14b5c-286">後續步驟</span><span class="sxs-lookup"><span data-stu-id="14b5c-286">Next steps</span></span>

<span data-ttu-id="14b5c-287">下列連結提供有關使用 Azure AD 重設密碼的其他資訊</span><span class="sxs-lookup"><span data-stu-id="14b5c-287">The following links provide additional information regarding password reset using Azure AD</span></span>

* <span data-ttu-id="14b5c-288">[**快速入門**](active-directory-passwords-getting-started.md) - 開始執行 Azure AD 自助式密碼管理</span><span class="sxs-lookup"><span data-stu-id="14b5c-288">[**Quick Start**](active-directory-passwords-getting-started.md) - Get up and running with Azure AD self service password management</span></span> 
* <span data-ttu-id="14b5c-289">[**授權**](active-directory-passwords-licensing.md) - 設定 Azure AD 授權</span><span class="sxs-lookup"><span data-stu-id="14b5c-289">[**Licensing**](active-directory-passwords-licensing.md) - Configure your Azure AD Licensing</span></span>
* <span data-ttu-id="14b5c-290">[**資料**](active-directory-passwords-data.md) -了解所需的資料以及如何將它使用於密碼管理</span><span class="sxs-lookup"><span data-stu-id="14b5c-290">[**Data**](active-directory-passwords-data.md) - Understand the data that is required and how it is used for password management</span></span>
* <span data-ttu-id="14b5c-291">[**推出**](active-directory-passwords-best-practices.md) - 使用此處提供的指引來規劃 SSPR 並部署給使用者</span><span class="sxs-lookup"><span data-stu-id="14b5c-291">[**Rollout**](active-directory-passwords-best-practices.md) - Plan and deploy SSPR to your users using the guidance found here</span></span>
* <span data-ttu-id="14b5c-292">[**原則**](active-directory-passwords-policy.md) - 了解並設定 Azure AD 密碼原則</span><span class="sxs-lookup"><span data-stu-id="14b5c-292">[**Policy**](active-directory-passwords-policy.md) - Understand and set Azure AD password policies</span></span>
* <span data-ttu-id="14b5c-293">[**密碼回寫**](active-directory-passwords-writeback.md) - 密碼回寫如何用在您的內部部署目錄</span><span class="sxs-lookup"><span data-stu-id="14b5c-293">[**Password Writeback**](active-directory-passwords-writeback.md) - How does password writeback work with your on-premises directory</span></span>
* <span data-ttu-id="14b5c-294">[**自訂**](active-directory-passwords-customize.md) - 為您的公司自訂 SSPR 體驗的外觀與風格。</span><span class="sxs-lookup"><span data-stu-id="14b5c-294">[**Customize**](active-directory-passwords-customize.md) - Customize the look and feel of the SSPR experience for your company.</span></span>
* <span data-ttu-id="14b5c-295">[**報告**](active-directory-passwords-reporting.md) - 探索您的使用者是否、何時、何地存取 SSPR 功能</span><span class="sxs-lookup"><span data-stu-id="14b5c-295">[**Reporting**](active-directory-passwords-reporting.md) - Discover if, when, and where your users are accessing SSPR functionality</span></span>
* <span data-ttu-id="14b5c-296">[**常見問題集**](active-directory-passwords-faq.md) - 如何？</span><span class="sxs-lookup"><span data-stu-id="14b5c-296">[**Frequently Asked Questions**](active-directory-passwords-faq.md) - How?</span></span> <span data-ttu-id="14b5c-297">原因為何？</span><span class="sxs-lookup"><span data-stu-id="14b5c-297">Why?</span></span> <span data-ttu-id="14b5c-298">何事？</span><span class="sxs-lookup"><span data-stu-id="14b5c-298">What?</span></span> <span data-ttu-id="14b5c-299">何地？</span><span class="sxs-lookup"><span data-stu-id="14b5c-299">Where?</span></span> <span data-ttu-id="14b5c-300">何人？</span><span class="sxs-lookup"><span data-stu-id="14b5c-300">Who?</span></span> <span data-ttu-id="14b5c-301">何時？</span><span class="sxs-lookup"><span data-stu-id="14b5c-301">When?</span></span> <span data-ttu-id="14b5c-302">- -您一直想要詢問之問題的答案</span><span class="sxs-lookup"><span data-stu-id="14b5c-302">- Answers to questions you always wanted to ask</span></span>
* <span data-ttu-id="14b5c-303">[**疑難排解**](active-directory-passwords-troubleshoot.md) - 了解如何解決我們看到的 SSPR 常見問題</span><span class="sxs-lookup"><span data-stu-id="14b5c-303">[**Troubleshoot**](active-directory-passwords-troubleshoot.md) - Learn how to resolve common issues that we see with SSPR</span></span>

