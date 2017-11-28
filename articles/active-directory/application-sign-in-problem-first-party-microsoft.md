---
title: "登入 tooa Microsoft 應用程式的 aaaProblems |Microsoft 文件"
description: "疑難排解 toofirst 合作對象 Microsoft 應用程式使用 （例如 Office 365) 的 Azure AD 在登入時所面臨的常見問題"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 35849ca8dbaa909d17b6d0da572f5c11041a8559
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
## <a name="problems-signing-in-tooa-microsoft-application"></a><span data-ttu-id="2e28a-103">登入 tooa Microsoft 應用程式的問題</span><span class="sxs-lookup"><span data-stu-id="2e28a-103">Problems signing in tooa Microsoft application</span></span>

<span data-ttu-id="2e28a-104">Microsoft 應用程式 (如 Office 365 Exchange、SharePoint、Yammer 等) 在指派與管理方面，比第三方 SaaS 應用程式或與 Azure AD 整合以單一登入的其他應用程式略為困難。</span><span class="sxs-lookup"><span data-stu-id="2e28a-104">Microsoft Applications (like Office 365 Exchange, SharePoint, Yammer, etc.) are assigned and managed a bit differently than 3rd party SaaS applications or other applications you integrate with Azure AD for single sign on.</span></span>

<span data-ttu-id="2e28a-105">有三種主要方式，使用者也可以取得存取 tooa Microsoft 發行的應用程式。</span><span class="sxs-lookup"><span data-stu-id="2e28a-105">There are three main ways that a user can get access tooa Microsoft-published application.</span></span>

-   <span data-ttu-id="2e28a-106">Hello Office 365 或其他付費的套件中的應用程式，會授與使用者存取透過**授權指派**任一直接 tootheir 使用者帳戶，或透過使用我們的群組為基礎的授權指派功能的群組。</span><span class="sxs-lookup"><span data-stu-id="2e28a-106">For applications in hello Office 365 or other paid suites, users are granted access through **license assignment** either directly tootheir user account, or through a group using our group-based license assignment capability.</span></span>

-   <span data-ttu-id="2e28a-107">對於應用程式，Microsoft 或第三個合作對象發行自由每個人都能 toouse，使用者可能會被授與存取透過**使用者同意**。</span><span class="sxs-lookup"><span data-stu-id="2e28a-107">For applications that Microsoft or a Third Party publishes freely for anyone toouse, users may be granted access through **user consent**.</span></span> <span data-ttu-id="2e28a-108">This0 表示他們登入 toohello 應用程式與 Azure AD 工作或學校帳戶，並允許它 toohave 存取 toosome 有限的一組資料上他們的帳戶。</span><span class="sxs-lookup"><span data-stu-id="2e28a-108">This0 means that they sign in toohello application with their Azure AD Work or School account and allow it toohave access toosome limited set of data on their account.</span></span>

-   <span data-ttu-id="2e28a-109">對於應用程式，Microsoft 或第 3 合作對象發行自由每個人都能 toouse，可能也會授與使用者存取透過**系統管理員的同意**。</span><span class="sxs-lookup"><span data-stu-id="2e28a-109">For applications that Microsoft or a 3rd Party publishes freely for anyone toouse, users may also be granted access through **administrator consent**.</span></span> <span data-ttu-id="2e28a-110">這表示系統管理員所判斷可能每個人都可以在 hello 組織中，使用 hello 應用程式，讓他們登入具有全域管理員帳戶的 toohello 應用程式，並授與存取 tooeveryone hello 組織中。</span><span class="sxs-lookup"><span data-stu-id="2e28a-110">This means that an administrator has determined hello application may be used by everyone in hello organization, so they sign in toohello application with a Global Administrator account and grant access tooeveryone in hello organization.</span></span>

<span data-ttu-id="2e28a-111">tootroubleshoot 您的問題，以 hello 開頭[一般問題區域與應用程式存取 tooconsider](#general-problem-areas-with-application-access-to-consider) ，然後讀取 hello[逐步解說： 步驟 tootroubleshoot Microsoft 應用程式存取](#walkthrough-steps-to-troubleshoot-microsoft-application-access)tooget 到 hello 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="2e28a-111">tootroubleshoot your issue, start with hello [General Problem Areas with Application Access tooconsider](#general-problem-areas-with-application-access-to-consider) and then read hello [Walkthrough: Steps tootroubleshoot Microsoft Application access](#walkthrough-steps-to-troubleshoot-microsoft-application-access) tooget into hello details.</span></span>

## <a name="general-problem-areas-with-application-access-tooconsider"></a><span data-ttu-id="2e28a-112">應用程式存取 tooconsider 的一般問題區域</span><span class="sxs-lookup"><span data-stu-id="2e28a-112">General Problem Areas with Application Access tooconsider</span></span>

<span data-ttu-id="2e28a-113">以下是一般的問題區域，如果您有其中 toostart，但我們建議您閱讀 hello 逐步解說 tooget 移快速了解可以切入 hello 的清單：[逐步解說： 步驟 tootroubleshoot Microsoft 應用程式存取](#walkthrough-steps-to-troubleshoot-microsoft-application-access).</span><span class="sxs-lookup"><span data-stu-id="2e28a-113">Below is a list of hello general problem areas that you can drill into if you have an idea of where toostart, but we recommend you read hello walkthrough tooget going quickly: [Walkthrough: Steps tootroubleshoot Microsoft Application access](#walkthrough-steps-to-troubleshoot-microsoft-application-access).</span></span>

-   [<span data-ttu-id="2e28a-114">Hello 使用者帳戶的問題</span><span class="sxs-lookup"><span data-stu-id="2e28a-114">Problems with hello user’s account</span></span>](#problems-with-the-users-account)

-   [<span data-ttu-id="2e28a-115">群組的問題</span><span class="sxs-lookup"><span data-stu-id="2e28a-115">Problems with groups</span></span>](#problems-with-groups)

-   [<span data-ttu-id="2e28a-116">條件式存取原則的問題</span><span class="sxs-lookup"><span data-stu-id="2e28a-116">Problems with conditional access policies</span></span>](#problems-with-conditional-access-policies)

-   [<span data-ttu-id="2e28a-117">應用程式同意的問題</span><span class="sxs-lookup"><span data-stu-id="2e28a-117">Problems with application consent</span></span>](#problems-with-application-consent)

## <a name="steps-tootroubleshoot-microsoft-application-access"></a><span data-ttu-id="2e28a-118">步驟 tootroubleshoot Microsoft 應用程式存取</span><span class="sxs-lookup"><span data-stu-id="2e28a-118">Steps tootroubleshoot Microsoft Application access</span></span>

<span data-ttu-id="2e28a-119">下面是一些常見的問題同仁時遇到使用者無法登入 tooa Microsoft 應用程式。</span><span class="sxs-lookup"><span data-stu-id="2e28a-119">Below are some common issues folks run into when their users cannot sign in tooa Microsoft application.</span></span>

-   <span data-ttu-id="2e28a-120">一般會先發出 toocheck</span><span class="sxs-lookup"><span data-stu-id="2e28a-120">General issues toocheck first</span></span>

  * <span data-ttu-id="2e28a-121">請確定 hello 使用者登入 toohello**更正 URL**並不是本機應用程式的 URL。</span><span class="sxs-lookup"><span data-stu-id="2e28a-121">Make sure hello user is signing in toohello **correct URL** and not a local application URL.</span></span>

  * <span data-ttu-id="2e28a-122">請確定 hello 使用者帳戶是**並未鎖定。**</span><span class="sxs-lookup"><span data-stu-id="2e28a-122">Make sure hello user’s account is **not locked out.**</span></span>

  * <span data-ttu-id="2e28a-123">請確定 hello**使用者帳戶存在**Azure Active Directory 中。</span><span class="sxs-lookup"><span data-stu-id="2e28a-123">Make sure hello **user’s account exists** in Azure Active Directory.</span></span> [<span data-ttu-id="2e28a-124">檢查 Azure Active Directory 中是否存在使用者帳戶</span><span class="sxs-lookup"><span data-stu-id="2e28a-124">Check if a user account exists in Azure Active Directory</span></span>](#problems-with-the-users-account)

  * <span data-ttu-id="2e28a-125">請確定 hello 使用者帳戶是**啟用**的登入。[檢查使用者帳戶的狀態](#problems-with-the-users-account)</span><span class="sxs-lookup"><span data-stu-id="2e28a-125">Make sure hello user’s account is **enabled** for sign ins. [Check a user’s account status](#problems-with-the-users-account)</span></span>

  * <span data-ttu-id="2e28a-126">請確定 hello 使用者的**密碼未過期或遺失。**</span><span class="sxs-lookup"><span data-stu-id="2e28a-126">Make sure hello user’s **password is not expired or forgotten.**</span></span> <span data-ttu-id="2e28a-127">[重設使用者密碼](#reset-a-users-password)或[啟用自助式密碼重設](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started)</span><span class="sxs-lookup"><span data-stu-id="2e28a-127">[Reset a user’s password](#reset-a-users-password) or [Enable self-service password reset](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started)</span></span>

   * <span data-ttu-id="2e28a-128">確定 **Multi-Factor Authentication** 未封鎖使用者存取。</span><span class="sxs-lookup"><span data-stu-id="2e28a-128">Make sure **Multi-Factor Authentication** is not blocking user access.</span></span> <span data-ttu-id="2e28a-129">[檢查使用者的多重要素驗證狀態](#check-a-users-multi-factor-authentication-status)或[檢查使用者的驗證連絡資訊](#check-a-users-authentication-contact-info)</span><span class="sxs-lookup"><span data-stu-id="2e28a-129">[Check a user’s multi-factor authentication status](#check-a-users-multi-factor-authentication-status) or [Check a user’s authentication contact info](#check-a-users-authentication-contact-info)</span></span>

   * <span data-ttu-id="2e28a-130">確定**條件式存取原則**或**身分識別保護**原則未封鎖使用者存取。</span><span class="sxs-lookup"><span data-stu-id="2e28a-130">Make sure a **Conditional Access policy** or **Identity Protection** policy is not blocking user access.</span></span> <span data-ttu-id="2e28a-131">[檢查特定條件式存取原則](#problems-with-conditional-access-policies)、[檢查特定應用程式條件式存取原則](#check-a-specific-applications-conditional-access-policy)或[停用特定條件式存取原則](#disable-a-specific-conditional-access-policy)</span><span class="sxs-lookup"><span data-stu-id="2e28a-131">[Check a specific conditional access policy](#problems-with-conditional-access-policies) or [Check a specific application’s conditional access policy](#check-a-specific-applications-conditional-access-policy) or [Disable a specific conditional access policy](#disable-a-specific-conditional-access-policy)</span></span>

   * <span data-ttu-id="2e28a-132">請確定使用者的**驗證連絡人資訊**已啟動 toodate tooallow Multi-factor Authentication 或條件式存取原則 toobe 強制執行。</span><span class="sxs-lookup"><span data-stu-id="2e28a-132">Make sure that a user’s **authentication contact info** is up toodate tooallow Multi-Factor Authentication or Conditional Access policies toobe enforced.</span></span> <span data-ttu-id="2e28a-133">[檢查使用者的多重要素驗證狀態](#check-a-users-multi-factor-authentication-status)或[檢查使用者的驗證連絡資訊](#check-a-users-authentication-contact-info)</span><span class="sxs-lookup"><span data-stu-id="2e28a-133">[Check a user’s multi-factor authentication status](#check-a-users-multi-factor-authentication-status) or [Check a user’s authentication contact info](#check-a-users-authentication-contact-info)</span></span>

-   <span data-ttu-id="2e28a-134">如**Microsoft** **需要授權的應用程式**（例如 Office365)，以下是一些特定的問題 toocheck 並非 hello 上述的一般問題：</span><span class="sxs-lookup"><span data-stu-id="2e28a-134">For **Microsoft** **applications that require a license** (like Office365), here are some specific issues toocheck once you have ruled out hello general issues above:</span></span>

   * <span data-ttu-id="2e28a-135">請確認 hello 使用者或已**指派授權。**</span><span class="sxs-lookup"><span data-stu-id="2e28a-135">Ensure hello user or has a **license assigned.**</span></span> <span data-ttu-id="2e28a-136">[檢查使用者獲指派的授權](#check-a-users-assigned-licenses)或[檢查群組獲指派的授權](#check-a-groups-assigned-licenses)</span><span class="sxs-lookup"><span data-stu-id="2e28a-136">[Check a user’s assigned licenses](#check-a-users-assigned-licenses) or [Check a group’s assigned licenses](#check-a-groups-assigned-licenses)</span></span>

   * <span data-ttu-id="2e28a-137">如果 hello 授權為**指派 tooa** **靜態群組**，確保該 hello**使用者所屬的**該群組。</span><span class="sxs-lookup"><span data-stu-id="2e28a-137">If hello license is **assigned tooa** **static group**, ensure that hello **user is a member** of that group.</span></span> [<span data-ttu-id="2e28a-138">檢查使用者的群組成員資格</span><span class="sxs-lookup"><span data-stu-id="2e28a-138">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

   * <span data-ttu-id="2e28a-139">如果 hello 授權為**指派 tooa** **動態群組**，確保該 hello**動態群組規則已正確設定**。</span><span class="sxs-lookup"><span data-stu-id="2e28a-139">If hello license is **assigned tooa** **dynamic group**, ensure that hello **dynamic group rule is set correctly**.</span></span> [<span data-ttu-id="2e28a-140">檢查動態群組成員資格準則</span><span class="sxs-lookup"><span data-stu-id="2e28a-140">Check a dynamic group’s membership criteria</span></span>](#check-a-dynamic-groups-membership-criteria)

   * <span data-ttu-id="2e28a-141">如果 hello 授權為**指派 tooa** **動態群組**，確定該 hello 動態群組擁有**完成處理**其成員資格，以及該 hello**使用者成員**（這可能需要一些時間）。</span><span class="sxs-lookup"><span data-stu-id="2e28a-141">If hello license is **assigned tooa** **dynamic group**, ensure that hello dynamic group has **finished processing** its membership and that hello **user is a member** (this can take some time).</span></span> [<span data-ttu-id="2e28a-142">檢查使用者的群組成員資格</span><span class="sxs-lookup"><span data-stu-id="2e28a-142">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

   *  <span data-ttu-id="2e28a-143">一旦您確定 hello 授權指派，請確定 hello 授權**過期**。</span><span class="sxs-lookup"><span data-stu-id="2e28a-143">Once you make sure hello license is assigned, make sure hello license is **not expired**.</span></span>

   *  <span data-ttu-id="2e28a-144">請確定 hello 授權**hello 應用程式**他們存取的。</span><span class="sxs-lookup"><span data-stu-id="2e28a-144">Make sure hello license is **for hello application** they are accessing.</span></span>

-   <span data-ttu-id="2e28a-145">如**Microsoft** **應用程式不需要授權的**，以下是一些其他項目 toocheck:</span><span class="sxs-lookup"><span data-stu-id="2e28a-145">For **Microsoft** **applications that don’t require a license**, here are some other things toocheck:</span></span>

   * <span data-ttu-id="2e28a-146">如果 hello 應用程式要求**使用者層級權限**（例如 「 存取這位使用者的信箱 」），請確定該 hello 使用者登入 toohello 應用程式，且已經執行**使用者層級同意作業** toolet hello 應用程式存取其資料。</span><span class="sxs-lookup"><span data-stu-id="2e28a-146">If hello application is requesting **user-level permissions** (for example “Access this user’s mailbox”), make sure that hello user has signed in toohello application and has performed a **user-level consent operation** toolet hello application access her data.</span></span>

   * <span data-ttu-id="2e28a-147">如果 hello 應用程式要求**系統管理員層級權限**（例如 「 存取所有使用者的信箱 」），請確定已執行 全域管理員**上的系統管理員層級同意作業代表所有使用者**hello 組織中。</span><span class="sxs-lookup"><span data-stu-id="2e28a-147">If hello application is requesting **administrator-level permissions** (for example “Access all user’s mailboxes”), make sure that a Global Administrator has performed an **administrator-level consent operation on behalf of all users** in hello organization.</span></span>

## <a name="problems-with-hello-users-account"></a><span data-ttu-id="2e28a-148">Hello 使用者帳戶的問題</span><span class="sxs-lookup"><span data-stu-id="2e28a-148">Problems with hello user’s account</span></span>

<span data-ttu-id="2e28a-149">因為 tooa 問題指派 toohello 應用程式的使用者，可能會封鎖應用程式存取。</span><span class="sxs-lookup"><span data-stu-id="2e28a-149">Application access can be blocked due tooa problem with a user that is assigned toohello application.</span></span> <span data-ttu-id="2e28a-150">以下是針對使用者和其帳戶設定進行疑難排解的一些方法︰</span><span class="sxs-lookup"><span data-stu-id="2e28a-150">Below are some ways you can troubleshoot and solve problems with users and their account settings:</span></span>

-   [<span data-ttu-id="2e28a-151">檢查 Azure Active Directory 中是否存在使用者帳戶</span><span class="sxs-lookup"><span data-stu-id="2e28a-151">Check if a user account exists in Azure Active Directory</span></span>](#check-if-a-user-account-exists-in-azure-active-directory)

-   [<span data-ttu-id="2e28a-152">檢查使用者帳戶的狀態</span><span class="sxs-lookup"><span data-stu-id="2e28a-152">Check a user’s account status</span></span>](#check-a-users-account-status)

-   [<span data-ttu-id="2e28a-153">重設使用者的密碼</span><span class="sxs-lookup"><span data-stu-id="2e28a-153">Reset a user’s password</span></span>](#reset-a-users-password)

-   [<span data-ttu-id="2e28a-154">啟用自助密碼重設</span><span class="sxs-lookup"><span data-stu-id="2e28a-154">Enable self-service password reset</span></span>](#enable-self-service-password-reset)

-   [<span data-ttu-id="2e28a-155">檢查使用者的多重要素驗證狀態</span><span class="sxs-lookup"><span data-stu-id="2e28a-155">Check a user’s multi-factor authentication status</span></span>](#check-a-users-multi-factor-authentication-status)

-   [<span data-ttu-id="2e28a-156">檢查使用者的驗證連絡資訊</span><span class="sxs-lookup"><span data-stu-id="2e28a-156">Check a user’s authentication contact info</span></span>](#check-a-users-authentication-contact-info)

-   [<span data-ttu-id="2e28a-157">檢查使用者的群組成員資格</span><span class="sxs-lookup"><span data-stu-id="2e28a-157">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

-   [<span data-ttu-id="2e28a-158">檢查使用者獲指派的授權</span><span class="sxs-lookup"><span data-stu-id="2e28a-158">Check a user’s assigned licenses</span></span>](#check-a-users-assigned-licenses)

-   [<span data-ttu-id="2e28a-159">指派授權至使用者</span><span class="sxs-lookup"><span data-stu-id="2e28a-159">Assign a user a license</span></span>](#assign-a-user-a-license)

### <a name="check-if-a-user-account-exists-in-azure-active-directory"></a><span data-ttu-id="2e28a-160">檢查 Azure Active Directory 中是否存在使用者帳戶</span><span class="sxs-lookup"><span data-stu-id="2e28a-160">Check if a user account exists in Azure Active Directory</span></span>

<span data-ttu-id="2e28a-161">toocheck 使用者帳戶是否存在，請遵循下列 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="2e28a-161">toocheck if a user’s account is present, follow hello steps below:</span></span>

1.  <span data-ttu-id="2e28a-162">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員。**</span><span class="sxs-lookup"><span data-stu-id="2e28a-162">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="2e28a-163">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="2e28a-163">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="2e28a-164">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="2e28a-164">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="2e28a-165">按一下**使用者和群組**hello 瀏覽功能表中。</span><span class="sxs-lookup"><span data-stu-id="2e28a-165">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="2e28a-166">按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="2e28a-166">click **All users**.</span></span>

6.  <span data-ttu-id="2e28a-167">**搜尋**hello 您感興趣的使用者和**按一下 hello 列**tooselect。</span><span class="sxs-lookup"><span data-stu-id="2e28a-167">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="2e28a-168">檢查確定它們看起來如您預期且不會遺失任何資料的 hello 使用者物件 toobe hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="2e28a-168">Check hello properties of hello user object toobe sure that they look as you expect and no data is missing.</span></span>

### <a name="check-a-users-account-status"></a><span data-ttu-id="2e28a-169">檢查使用者帳戶的狀態</span><span class="sxs-lookup"><span data-stu-id="2e28a-169">Check a user’s account status</span></span>

<span data-ttu-id="2e28a-170">toocheck 使用者的帳戶狀態，請遵循下列步驟 hello:</span><span class="sxs-lookup"><span data-stu-id="2e28a-170">toocheck a user’s account status, follow hello steps below:</span></span>

1.  <span data-ttu-id="2e28a-171">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員。**</span><span class="sxs-lookup"><span data-stu-id="2e28a-171">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="2e28a-172">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="2e28a-172">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="2e28a-173">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="2e28a-173">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="2e28a-174">按一下**使用者和群組**hello 瀏覽功能表中。</span><span class="sxs-lookup"><span data-stu-id="2e28a-174">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="2e28a-175">按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="2e28a-175">click **All users**.</span></span>

6.  <span data-ttu-id="2e28a-176">**搜尋**hello 您感興趣的使用者和**按一下 hello 列**tooselect。</span><span class="sxs-lookup"><span data-stu-id="2e28a-176">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="2e28a-177">按一下 [設定檔]。</span><span class="sxs-lookup"><span data-stu-id="2e28a-177">click **Profile**.</span></span>

8.  <span data-ttu-id="2e28a-178">在下**設定**確定**區塊登入**設定得**否**。</span><span class="sxs-lookup"><span data-stu-id="2e28a-178">Under **Settings** ensure that **Block sign in** is set too**No**.</span></span>

### <a name="reset-a-users-password"></a><span data-ttu-id="2e28a-179">重設使用者的密碼</span><span class="sxs-lookup"><span data-stu-id="2e28a-179">Reset a user’s password</span></span>

<span data-ttu-id="2e28a-180">tooreset 使用者的密碼，後續 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="2e28a-180">tooreset a user’s password, follow hello steps below:</span></span>

1.  <span data-ttu-id="2e28a-181">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員。**</span><span class="sxs-lookup"><span data-stu-id="2e28a-181">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="2e28a-182">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="2e28a-182">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="2e28a-183">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="2e28a-183">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="2e28a-184">按一下**使用者和群組**hello 瀏覽功能表中。</span><span class="sxs-lookup"><span data-stu-id="2e28a-184">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="2e28a-185">按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="2e28a-185">click **All users**.</span></span>

6.  <span data-ttu-id="2e28a-186">**搜尋**hello 您感興趣的使用者和**按一下 hello 列**tooselect。</span><span class="sxs-lookup"><span data-stu-id="2e28a-186">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="2e28a-187">按一下 hello**重設密碼**在 hello hello 使用者 刀鋒視窗頂端的按鈕。</span><span class="sxs-lookup"><span data-stu-id="2e28a-187">click hello **Reset password** button at hello top of hello user blade.</span></span>

8.  <span data-ttu-id="2e28a-188">按一下 hello**重設密碼**按鈕 hello**重設密碼**刀鋒視窗中出現。</span><span class="sxs-lookup"><span data-stu-id="2e28a-188">click hello **Reset password** button on hello **Reset password** blade that appears.</span></span>

9.  <span data-ttu-id="2e28a-189">複製 hello**暫時密碼**或**輸入新密碼**hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="2e28a-189">Copy hello **temporary password** or **enter a new password** for hello user.</span></span>

10. <span data-ttu-id="2e28a-190">這個新的密碼 toohello 使用者進行通訊，它們是必要的 toochange 他們下一步 在此密碼登入 tooAzure Active Directory。</span><span class="sxs-lookup"><span data-stu-id="2e28a-190">Communicate this new password toohello user, they be required toochange this password during their next sign in tooAzure Active Directory.</span></span>

### <a name="enable-self-service-password-reset"></a><span data-ttu-id="2e28a-191">啟用自助式密碼重設</span><span class="sxs-lookup"><span data-stu-id="2e28a-191">Enable self-service password reset</span></span>

<span data-ttu-id="2e28a-192">tooenable 自助式密碼重設，請遵循下列的 hello 部署步驟：</span><span class="sxs-lookup"><span data-stu-id="2e28a-192">tooenable self-service password reset, follow hello deployment steps below:</span></span>

-   [<span data-ttu-id="2e28a-193">啟用使用者 tooreset 其 Azure Active Directory 密碼</span><span class="sxs-lookup"><span data-stu-id="2e28a-193">Enable users tooreset their Azure Active Directory passwords</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-their-azure-ad-passwords)

-   [<span data-ttu-id="2e28a-194">啟用使用者 tooreset 或變更其 Active Directory 內部部署密碼</span><span class="sxs-lookup"><span data-stu-id="2e28a-194">Enable users tooreset or change their Active Directory on-premises passwords</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-or-change-their-ad-passwords)

### <a name="check-a-users-multi-factor-authentication-status"></a><span data-ttu-id="2e28a-195">檢查使用者的多重要素驗證狀態</span><span class="sxs-lookup"><span data-stu-id="2e28a-195">Check a user’s multi-factor authentication status</span></span>

<span data-ttu-id="2e28a-196">toocheck 使用者的多重要素驗證狀態，後續 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="2e28a-196">toocheck a user’s multi-factor authentication status, follow hello steps below:</span></span>

1.  <span data-ttu-id="2e28a-197">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員。**</span><span class="sxs-lookup"><span data-stu-id="2e28a-197">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="2e28a-198">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="2e28a-198">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="2e28a-199">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="2e28a-199">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="2e28a-200">按一下**使用者和群組**hello 瀏覽功能表中。</span><span class="sxs-lookup"><span data-stu-id="2e28a-200">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="2e28a-201">按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="2e28a-201">click **All users**.</span></span>

6.  <span data-ttu-id="2e28a-202">按一下 hello **Multi-factor Authentication**在 hello hello 刀鋒視窗頂端的按鈕。</span><span class="sxs-lookup"><span data-stu-id="2e28a-202">click hello **Multi-Factor Authentication** button at hello top of hello blade.</span></span>

7.  <span data-ttu-id="2e28a-203">一次 hello**多因素驗證管理網站**載入，請確定您是在 hello**使用者** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="2e28a-203">Once hello **Multi-Factor Authentication Administration Portal** loads, ensure you are on hello **Users** tab.</span></span>

8.  <span data-ttu-id="2e28a-204">Hello 的使用者清單中尋找 hello 使用者搜尋、 篩選或排序。</span><span class="sxs-lookup"><span data-stu-id="2e28a-204">Find hello user in hello list of users by searching, filtering, or sorting.</span></span>

9.  <span data-ttu-id="2e28a-205">選取 hello 使用者的使用者清單，hello 和**啟用**，**停用**，或**強制**所需的多因素驗證。</span><span class="sxs-lookup"><span data-stu-id="2e28a-205">Select hello user from hello list of users and **Enable**, **Disable**, or **Enforce** multi-factor authentication as desired.</span></span>

  * <span data-ttu-id="2e28a-206">**請注意**： 如果使用者存在於**強制**狀態時，您可能設定太**已停用**暫時 toolet 它們放回其帳戶。</span><span class="sxs-lookup"><span data-stu-id="2e28a-206">**Note**: If a user is in an **Enforced** state, you may set them too**Disabled** temporarily toolet them back into their account.</span></span> <span data-ttu-id="2e28a-207">當它們位於上一步時，您可以變更其狀態太**啟用**再次 toorequire 它們 toore 註冊他們的連絡資訊在其下一步 期間登入。</span><span class="sxs-lookup"><span data-stu-id="2e28a-207">Once they are back in, you can then change their state too**Enabled** again toorequire them toore-register their contact information during their next sign in.</span></span> <span data-ttu-id="2e28a-208">或者，您可以依照 hello 中的 hello 步驟[檢查使用者的驗證連絡人資訊](#check-a-users-authentication-contact-info)tooverify 或設定此資料。</span><span class="sxs-lookup"><span data-stu-id="2e28a-208">Alternatively, you can follow hello steps in hello [Check a user’s authentication contact info](#check-a-users-authentication-contact-info) tooverify or set this data for them.</span></span>

### <a name="check-a-users-authentication-contact-info"></a><span data-ttu-id="2e28a-209">檢查使用者的驗證連絡資訊</span><span class="sxs-lookup"><span data-stu-id="2e28a-209">Check a user’s authentication contact info</span></span>

<span data-ttu-id="2e28a-210">toocheck 位使用者的驗證連絡資訊用於多重要素驗證、 條件式存取、 識別身分保護和重設密碼，請遵循下列 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="2e28a-210">toocheck a user’s authentication contact info used for Multi-factor authentication, Conditional Access, Identity Protection, and Password Reset, follow hello steps below:</span></span>

1.  <span data-ttu-id="2e28a-211">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員。**</span><span class="sxs-lookup"><span data-stu-id="2e28a-211">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="2e28a-212">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="2e28a-212">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="2e28a-213">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="2e28a-213">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="2e28a-214">按一下**使用者和群組**hello 瀏覽功能表中。</span><span class="sxs-lookup"><span data-stu-id="2e28a-214">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="2e28a-215">按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="2e28a-215">click **All users**.</span></span>

6.  <span data-ttu-id="2e28a-216">**搜尋**hello 您感興趣的使用者和**按一下 hello 列**tooselect。</span><span class="sxs-lookup"><span data-stu-id="2e28a-216">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="2e28a-217">按一下 [設定檔]。</span><span class="sxs-lookup"><span data-stu-id="2e28a-217">click **Profile**.</span></span>

8.  <span data-ttu-id="2e28a-218">向下捲動太**驗證連絡人資訊**。</span><span class="sxs-lookup"><span data-stu-id="2e28a-218">Scroll down too**Authentication contact info**.</span></span>

9.  <span data-ttu-id="2e28a-219">**檢閱**視 hello 資料註冊 hello 使用者和更新。</span><span class="sxs-lookup"><span data-stu-id="2e28a-219">**Review** hello data registered for hello user and update as needed.</span></span>

### <a name="check-a-users-group-memberships"></a><span data-ttu-id="2e28a-220">檢查使用者的群組成員資格</span><span class="sxs-lookup"><span data-stu-id="2e28a-220">Check a user’s group memberships</span></span>

<span data-ttu-id="2e28a-221">toocheck 使用者的群組成員資格，請遵循下列步驟 hello:</span><span class="sxs-lookup"><span data-stu-id="2e28a-221">toocheck a user’s group memberships, follow hello steps below:</span></span>

1.  <span data-ttu-id="2e28a-222">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員。**</span><span class="sxs-lookup"><span data-stu-id="2e28a-222">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="2e28a-223">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="2e28a-223">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="2e28a-224">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="2e28a-224">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="2e28a-225">按一下**使用者和群組**hello 瀏覽功能表中。</span><span class="sxs-lookup"><span data-stu-id="2e28a-225">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="2e28a-226">按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="2e28a-226">click **All users**.</span></span>

6.  <span data-ttu-id="2e28a-227">**搜尋**hello 您感興趣的使用者和**按一下 hello 列**tooselect。</span><span class="sxs-lookup"><span data-stu-id="2e28a-227">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="2e28a-228">按一下**群組**toosee 以分組 hello 使用者隸屬。</span><span class="sxs-lookup"><span data-stu-id="2e28a-228">click **Groups** toosee which groups hello user is a member of.</span></span>

### <a name="check-a-users-assigned-licenses"></a><span data-ttu-id="2e28a-229">檢查使用者獲指派的授權</span><span class="sxs-lookup"><span data-stu-id="2e28a-229">Check a user’s assigned licenses</span></span>

<span data-ttu-id="2e28a-230">toocheck 使用者的指派授權，後續 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="2e28a-230">toocheck a user’s assigned licenses, follow hello steps below:</span></span>

1.  <span data-ttu-id="2e28a-231">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員。**</span><span class="sxs-lookup"><span data-stu-id="2e28a-231">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="2e28a-232">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="2e28a-232">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="2e28a-233">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="2e28a-233">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="2e28a-234">按一下**使用者和群組**hello 瀏覽功能表中。</span><span class="sxs-lookup"><span data-stu-id="2e28a-234">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="2e28a-235">按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="2e28a-235">click **All users**.</span></span>

6.  <span data-ttu-id="2e28a-236">**搜尋**hello 您感興趣的使用者和**按一下 hello 列**tooselect。</span><span class="sxs-lookup"><span data-stu-id="2e28a-236">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="2e28a-237">按一下**授權**toosee 授權 hello 使用者目前已指派。</span><span class="sxs-lookup"><span data-stu-id="2e28a-237">click **Licenses** toosee which licenses hello user currently has assigned.</span></span>

### <a name="assign-a-user-a-license"></a><span data-ttu-id="2e28a-238">指派授權至使用者</span><span class="sxs-lookup"><span data-stu-id="2e28a-238">Assign a user a license</span></span> 

<span data-ttu-id="2e28a-239">tooassign 授權 tooa 使用者，請遵循下列 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="2e28a-239">tooassign a license tooa user, follow hello steps below:</span></span>

1.  <span data-ttu-id="2e28a-240">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員。**</span><span class="sxs-lookup"><span data-stu-id="2e28a-240">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="2e28a-241">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="2e28a-241">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="2e28a-242">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="2e28a-242">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="2e28a-243">按一下**使用者和群組**hello 瀏覽功能表中。</span><span class="sxs-lookup"><span data-stu-id="2e28a-243">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="2e28a-244">按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="2e28a-244">click **All users**.</span></span>

6.  <span data-ttu-id="2e28a-245">**搜尋**hello 您感興趣的使用者和**按一下 hello 列**tooselect。</span><span class="sxs-lookup"><span data-stu-id="2e28a-245">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="2e28a-246">按一下**授權**toosee 授權 hello 使用者目前已指派。</span><span class="sxs-lookup"><span data-stu-id="2e28a-246">click **Licenses** toosee which licenses hello user currently has assigned.</span></span>

8.  <span data-ttu-id="2e28a-247">按一下 hello**指派** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="2e28a-247">click hello **Assign** button.</span></span>

9.  <span data-ttu-id="2e28a-248">選取**一或多個產品**hello 清單中的可用產品。</span><span class="sxs-lookup"><span data-stu-id="2e28a-248">Select **one or more products** from hello list of available products.</span></span>

10. <span data-ttu-id="2e28a-249">**選擇性**按一下 hello**指派選項**項目 toogranularly 指派產品。</span><span class="sxs-lookup"><span data-stu-id="2e28a-249">**Optional** click hello **assignment options** item toogranularly assign products.</span></span> <span data-ttu-id="2e28a-250">完成時按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="2e28a-250">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="2e28a-251">按一下 hello**指派**按鈕 tooassign 這些授權 toothis 使用者。</span><span class="sxs-lookup"><span data-stu-id="2e28a-251">Click hello **Assign** button tooassign these licenses toothis user.</span></span>

## <a name="problems-with-groups"></a><span data-ttu-id="2e28a-252">群組的問題</span><span class="sxs-lookup"><span data-stu-id="2e28a-252">Problems with groups</span></span>

<span data-ttu-id="2e28a-253">應用程式存取權可以指派 toohello 應用程式群組 tooa 時發生問題。 因為被封鎖。</span><span class="sxs-lookup"><span data-stu-id="2e28a-253">Application access can be blocked due tooa problem with a group that is assigned toohello application.</span></span> <span data-ttu-id="2e28a-254">以下是為群組和群組成員資格問題疑難排解的一些方法︰</span><span class="sxs-lookup"><span data-stu-id="2e28a-254">Below are some ways you can troubleshoot and solve problems with groups and group memberships:</span></span>

-   [<span data-ttu-id="2e28a-255">檢查群組成員資格</span><span class="sxs-lookup"><span data-stu-id="2e28a-255">Check a group’s membership</span></span>](#check-a-groups-membership)

-   [<span data-ttu-id="2e28a-256">檢查動態群組成員資格準則</span><span class="sxs-lookup"><span data-stu-id="2e28a-256">Check a dynamic group’s membership criteria</span></span>](#check-a-dynamic-groups-membership-criteria)

-   [<span data-ttu-id="2e28a-257">檢查群組獲指派的授權</span><span class="sxs-lookup"><span data-stu-id="2e28a-257">Check a group’s assigned licenses</span></span>](#check-a-groups-assigned-licenses)

-   [<span data-ttu-id="2e28a-258">重新處理群組的授權</span><span class="sxs-lookup"><span data-stu-id="2e28a-258">Reprocess a group’s licenses</span></span>](#reprocess-a-groups-licenses)

-   [<span data-ttu-id="2e28a-259">指派授權至群組</span><span class="sxs-lookup"><span data-stu-id="2e28a-259">Assign a group a license</span></span>](#assign-a-group-a-license)

### <a name="check-a-groups-membership"></a><span data-ttu-id="2e28a-260">檢查群組成員資格</span><span class="sxs-lookup"><span data-stu-id="2e28a-260">Check a group’s membership</span></span>

<span data-ttu-id="2e28a-261">toocheck 群組的成員資格，後續 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="2e28a-261">toocheck a group’s membership, follow hello steps below:</span></span>

1.  <span data-ttu-id="2e28a-262">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員。**</span><span class="sxs-lookup"><span data-stu-id="2e28a-262">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="2e28a-263">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="2e28a-263">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="2e28a-264">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="2e28a-264">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="2e28a-265">按一下**使用者和群組**hello 瀏覽功能表中。</span><span class="sxs-lookup"><span data-stu-id="2e28a-265">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="2e28a-266">按一下 [所有群組]。</span><span class="sxs-lookup"><span data-stu-id="2e28a-266">click **All groups**.</span></span>

6.  <span data-ttu-id="2e28a-267">**搜尋**hello 您感興趣的群組和**按一下 hello 列**tooselect。</span><span class="sxs-lookup"><span data-stu-id="2e28a-267">**Search** for hello group you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="2e28a-268">按一下**成員**tooreview hello 清單的使用者指派 toothis 群組。</span><span class="sxs-lookup"><span data-stu-id="2e28a-268">click **Members** tooreview hello list of users assigned toothis group.</span></span>

### <a name="check-a-dynamic-groups-membership-criteria"></a><span data-ttu-id="2e28a-269">檢查動態群組成員資格準則</span><span class="sxs-lookup"><span data-stu-id="2e28a-269">Check a dynamic group’s membership criteria</span></span> 

<span data-ttu-id="2e28a-270">toocheck 動態群組成員資格準則，請遵循下列 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="2e28a-270">toocheck a dynamic group’s membership criteria, follow hello steps below:</span></span>

1.  <span data-ttu-id="2e28a-271">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員。**</span><span class="sxs-lookup"><span data-stu-id="2e28a-271">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="2e28a-272">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="2e28a-272">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="2e28a-273">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="2e28a-273">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="2e28a-274">按一下**使用者和群組**hello 瀏覽功能表中。</span><span class="sxs-lookup"><span data-stu-id="2e28a-274">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="2e28a-275">按一下 [所有群組]。</span><span class="sxs-lookup"><span data-stu-id="2e28a-275">click **All groups**.</span></span>

6.  <span data-ttu-id="2e28a-276">**搜尋**hello 您感興趣的群組和**按一下 hello 列**tooselect。</span><span class="sxs-lookup"><span data-stu-id="2e28a-276">**Search** for hello group you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="2e28a-277">按一下 [動態成員資格規則]。</span><span class="sxs-lookup"><span data-stu-id="2e28a-277">click **Dynamic membership rules.**</span></span>

8.  <span data-ttu-id="2e28a-278">檢閱 hello**簡單**或**進階**規則為此群組定義，並確定 hello 使用者想 toobe 此群組的成員符合這些準則。</span><span class="sxs-lookup"><span data-stu-id="2e28a-278">Review hello **simple** or **advanced** rule defined for this group and ensure that hello user you want toobe a member of this group meets these criteria.</span></span>

### <a name="check-a-groups-assigned-licenses"></a><span data-ttu-id="2e28a-279">檢查群組獲指派的授權</span><span class="sxs-lookup"><span data-stu-id="2e28a-279">Check a group’s assigned licenses</span></span>

<span data-ttu-id="2e28a-280">toocheck 群組的指派授權，後續 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="2e28a-280">toocheck a group’s assigned licenses, follow hello steps below:</span></span>

1.  <span data-ttu-id="2e28a-281">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員。**</span><span class="sxs-lookup"><span data-stu-id="2e28a-281">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="2e28a-282">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="2e28a-282">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="2e28a-283">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="2e28a-283">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="2e28a-284">按一下**使用者和群組**hello 瀏覽功能表中。</span><span class="sxs-lookup"><span data-stu-id="2e28a-284">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="2e28a-285">按一下 [所有群組]。</span><span class="sxs-lookup"><span data-stu-id="2e28a-285">click **All groups**.</span></span>

6.  <span data-ttu-id="2e28a-286">**搜尋**hello 您感興趣的群組和**按一下 hello 列**tooselect。</span><span class="sxs-lookup"><span data-stu-id="2e28a-286">**Search** for hello group you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="2e28a-287">按一下**授權**toosee 授權 hello 群組目前已指派。</span><span class="sxs-lookup"><span data-stu-id="2e28a-287">click **Licenses** toosee which licenses hello group currently has assigned.</span></span>

### <a name="reprocess-a-groups-licenses"></a><span data-ttu-id="2e28a-288">重新處理群組的授權</span><span class="sxs-lookup"><span data-stu-id="2e28a-288">Reprocess a group’s licenses</span></span>

<span data-ttu-id="2e28a-289">tooreprocess 群組的指派授權，後續 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="2e28a-289">tooreprocess a group’s assigned licenses, follow hello steps below:</span></span>

1.  <span data-ttu-id="2e28a-290">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員。**</span><span class="sxs-lookup"><span data-stu-id="2e28a-290">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="2e28a-291">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="2e28a-291">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="2e28a-292">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="2e28a-292">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="2e28a-293">按一下**使用者和群組**hello 瀏覽功能表中。</span><span class="sxs-lookup"><span data-stu-id="2e28a-293">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="2e28a-294">按一下 [所有群組]。</span><span class="sxs-lookup"><span data-stu-id="2e28a-294">click **All groups**.</span></span>

6.  <span data-ttu-id="2e28a-295">**搜尋**hello 您感興趣的群組和**按一下 hello 列**tooselect。</span><span class="sxs-lookup"><span data-stu-id="2e28a-295">**Search** for hello group you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="2e28a-296">按一下**授權**toosee 授權 hello 群組目前已指派。</span><span class="sxs-lookup"><span data-stu-id="2e28a-296">click **Licenses** toosee which licenses hello group currently has assigned.</span></span>

8.  <span data-ttu-id="2e28a-297">按一下 hello**重新處理**按鈕 tooensure hello 指派授權 toothis 群組的成員，都是最新。</span><span class="sxs-lookup"><span data-stu-id="2e28a-297">click hello **Reprocess** button tooensure that hello licenses assigned toothis group’s members are up-to-date.</span></span> <span data-ttu-id="2e28a-298">這可能需要很長的時間，取決於 hello 大小和複雜度 hello 群組。</span><span class="sxs-lookup"><span data-stu-id="2e28a-298">This may take a long time, depending on hello size and complexity of hello group.</span></span>

   >[!NOTE]
   ><span data-ttu-id="2e28a-299">toodo 這速度更快，請考慮暫時直接指派授權 toohello 使用者。</span><span class="sxs-lookup"><span data-stu-id="2e28a-299">toodo this faster, consider temporarily assigning a license toohello user directly.</span></span> <span data-ttu-id="2e28a-300">[指派授權至使用者](#problems-with-application-consent)。</span><span class="sxs-lookup"><span data-stu-id="2e28a-300">[Assign a user a license](#problems-with-application-consent).</span></span>
   >
   >

### <a name="assign-a-group-a-license"></a><span data-ttu-id="2e28a-301">指派授權至群組</span><span class="sxs-lookup"><span data-stu-id="2e28a-301">Assign a group a license</span></span>

<span data-ttu-id="2e28a-302">tooassign 授權 tooa 群組，請遵循下列 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="2e28a-302">tooassign a license tooa group, follow hello steps below:</span></span>

1.  <span data-ttu-id="2e28a-303">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員。**</span><span class="sxs-lookup"><span data-stu-id="2e28a-303">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="2e28a-304">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="2e28a-304">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="2e28a-305">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="2e28a-305">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="2e28a-306">按一下**使用者和群組**hello 瀏覽功能表中。</span><span class="sxs-lookup"><span data-stu-id="2e28a-306">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="2e28a-307">按一下 [所有群組]。</span><span class="sxs-lookup"><span data-stu-id="2e28a-307">click **All groups**.</span></span>

6.  <span data-ttu-id="2e28a-308">**搜尋**hello 您感興趣的群組和**按一下 hello 列**tooselect。</span><span class="sxs-lookup"><span data-stu-id="2e28a-308">**Search** for hello group you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="2e28a-309">按一下**授權**toosee 授權 hello 群組目前已指派。</span><span class="sxs-lookup"><span data-stu-id="2e28a-309">click **Licenses** toosee which licenses hello group currently has assigned.</span></span>

8.  <span data-ttu-id="2e28a-310">按一下 hello**指派** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="2e28a-310">click hello **Assign** button.</span></span>

9.  <span data-ttu-id="2e28a-311">選取**一或多個產品**hello 清單中的可用產品。</span><span class="sxs-lookup"><span data-stu-id="2e28a-311">Select **one or more products** from hello list of available products.</span></span>

10. <span data-ttu-id="2e28a-312">**選擇性**按一下 hello**指派選項**項目 toogranularly 指派產品。</span><span class="sxs-lookup"><span data-stu-id="2e28a-312">**Optional** click hello **assignment options** item toogranularly assign products.</span></span> <span data-ttu-id="2e28a-313">完成時按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="2e28a-313">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="2e28a-314">按一下 hello**指派**按鈕 tooassign 這些授權 toothis 群組。</span><span class="sxs-lookup"><span data-stu-id="2e28a-314">Click hello **Assign** button tooassign these licenses toothis group.</span></span> <span data-ttu-id="2e28a-315">這可能需要很長的時間，取決於 hello 大小和複雜度 hello 群組。</span><span class="sxs-lookup"><span data-stu-id="2e28a-315">This may take a long time, depending on hello size and complexity of hello group.</span></span>

   >[!NOTE]
   ><span data-ttu-id="2e28a-316">toodo 這速度更快，請考慮暫時直接指派授權 toohello 使用者。</span><span class="sxs-lookup"><span data-stu-id="2e28a-316">toodo this faster, consider temporarily assigning a license toohello user directly.</span></span> <span data-ttu-id="2e28a-317">[指派授權至使用者](#problems-with-application-consent)。</span><span class="sxs-lookup"><span data-stu-id="2e28a-317">[Assign a user a license](#problems-with-application-consent).</span></span>
   > 
   >

## <a name="problems-with-conditional-access-policies"></a><span data-ttu-id="2e28a-318">條件式存取原則的問題</span><span class="sxs-lookup"><span data-stu-id="2e28a-318">Problems with conditional access policies</span></span>

### <a name="check-a-specific-conditional-access-policy"></a><span data-ttu-id="2e28a-319">檢查特定的條件式存取原則</span><span class="sxs-lookup"><span data-stu-id="2e28a-319">Check a specific conditional access policy</span></span>

<span data-ttu-id="2e28a-320">toocheck 或驗證的單一條件式存取原則：</span><span class="sxs-lookup"><span data-stu-id="2e28a-320">toocheck or validate a single conditional access policy:</span></span>

1.  <span data-ttu-id="2e28a-321">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員。**</span><span class="sxs-lookup"><span data-stu-id="2e28a-321">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="2e28a-322">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="2e28a-322">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="2e28a-323">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="2e28a-323">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="2e28a-324">按一下**企業應用程式**hello 瀏覽功能表中。</span><span class="sxs-lookup"><span data-stu-id="2e28a-324">click **Enterprise applications** in hello navigation menu.</span></span>

5.  <span data-ttu-id="2e28a-325">按一下 hello**條件式存取**瀏覽項目。</span><span class="sxs-lookup"><span data-stu-id="2e28a-325">click hello **Conditional access** navigation item.</span></span>

6.  <span data-ttu-id="2e28a-326">按一下您感興趣檢查 hello 原則。</span><span class="sxs-lookup"><span data-stu-id="2e28a-326">click hello policy you are interested in inspecting.</span></span>

7.  <span data-ttu-id="2e28a-327">檢查有無特定的條件、指派，或其他可能會封鎖使用者存取的設定。</span><span class="sxs-lookup"><span data-stu-id="2e28a-327">Review that there are no specific conditions, assignments, or other settings which may be blocking user access.</span></span>

   >[!NOTE]
   ><span data-ttu-id="2e28a-328">您可能希望 tootemporarily 停用此原則 tooensure，則會不影響符號集 toodo 如此，組 hello**啟用原則**太切換**否**按一下 hello**儲存**按鈕.</span><span class="sxs-lookup"><span data-stu-id="2e28a-328">You may wish tootemporarily disable this policy tooensure it is not affecting sign ins. toodo this, set hello **Enable policy** toggle too**No** and click hello **Save** button.</span></span>
   >
   >

### <a name="check-a-specific-applications-conditional-access-policy"></a><span data-ttu-id="2e28a-329">檢查特定應用程式的條件式存取原則</span><span class="sxs-lookup"><span data-stu-id="2e28a-329">Check a specific application’s conditional access policy</span></span>

<span data-ttu-id="2e28a-330">toocheck 或驗證單一應用程式的目前設定的條件式存取原則：</span><span class="sxs-lookup"><span data-stu-id="2e28a-330">toocheck or validate a single application’s currently configured conditional access policy:</span></span>

1.  <span data-ttu-id="2e28a-331">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員。**</span><span class="sxs-lookup"><span data-stu-id="2e28a-331">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="2e28a-332">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="2e28a-332">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="2e28a-333">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="2e28a-333">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="2e28a-334">按一下**企業應用程式**hello 瀏覽功能表中。</span><span class="sxs-lookup"><span data-stu-id="2e28a-334">click **Enterprise applications** in hello navigation menu.</span></span>

5.  <span data-ttu-id="2e28a-335">按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="2e28a-335">click **All applications**.</span></span>

6.  <span data-ttu-id="2e28a-336">搜尋您感興趣，或 hello 使用者 「 hello 」 應用程式正在嘗試 toosign tooby 應用程式中的顯示名稱或應用程式的識別碼。</span><span class="sxs-lookup"><span data-stu-id="2e28a-336">Search for hello application you are interested in, or hello user is attempting toosign in tooby application display name or application id.</span></span>

     >[!NOTE]
     ><span data-ttu-id="2e28a-337">如果您沒有看到您所需的 hello 應用程式，按一下 hello**篩選**按鈕，然後依序展開 hello hello 清單範圍太**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="2e28a-337">If you don’t see hello application you are looking for, click hello **Filter** button and expand hello scope of hello list too**All applications**.</span></span> <span data-ttu-id="2e28a-338">如果您想 toosee 更多資料行，請按一下 hello**資料行**按鈕 tooadd 應用程式的其他詳細資料。</span><span class="sxs-lookup"><span data-stu-id="2e28a-338">If you want toosee more columns, click hello **Columns** button tooadd additional details for your applications.</span></span>
     >
     >

7.  <span data-ttu-id="2e28a-339">按一下 hello**條件式存取**瀏覽項目。</span><span class="sxs-lookup"><span data-stu-id="2e28a-339">click hello **Conditional access** navigation item.</span></span>

8.  <span data-ttu-id="2e28a-340">按一下您感興趣檢查 hello 原則。</span><span class="sxs-lookup"><span data-stu-id="2e28a-340">click hello policy you are interested in inspecting.</span></span>

9.  <span data-ttu-id="2e28a-341">檢查有無特定的條件、指派，或其他可能會封鎖使用者存取的設定。</span><span class="sxs-lookup"><span data-stu-id="2e28a-341">Review that there are no specific conditions, assignments, or other settings which may be blocking user access.</span></span>

     >[!NOTE]
     ><span data-ttu-id="2e28a-342">您可能希望 tootemporarily 停用此原則 tooensure，則會不影響符號集 toodo 如此，組 hello**啟用原則**太切換**否**按一下 hello**儲存**按鈕.</span><span class="sxs-lookup"><span data-stu-id="2e28a-342">You may wish tootemporarily disable this policy tooensure it is not affecting sign ins. toodo this, set hello **Enable policy** toggle too**No** and click hello **Save** button.</span></span>
     >
     >

### <a name="disable-a-specific-conditional-access-policy"></a><span data-ttu-id="2e28a-343">停用特定的條件式存取原則</span><span class="sxs-lookup"><span data-stu-id="2e28a-343">Disable a specific conditional access policy</span></span>

<span data-ttu-id="2e28a-344">toocheck 或驗證的單一條件式存取原則：</span><span class="sxs-lookup"><span data-stu-id="2e28a-344">toocheck or validate a single conditional access policy:</span></span>

1.  <span data-ttu-id="2e28a-345">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員。**</span><span class="sxs-lookup"><span data-stu-id="2e28a-345">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="2e28a-346">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="2e28a-346">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="2e28a-347">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="2e28a-347">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="2e28a-348">按一下**企業應用程式**hello 瀏覽功能表中。</span><span class="sxs-lookup"><span data-stu-id="2e28a-348">click **Enterprise applications** in hello navigation menu.</span></span>

5.  <span data-ttu-id="2e28a-349">按一下 hello**條件式存取**瀏覽項目。</span><span class="sxs-lookup"><span data-stu-id="2e28a-349">click hello **Conditional access** navigation item.</span></span>

6.  <span data-ttu-id="2e28a-350">按一下您感興趣檢查 hello 原則。</span><span class="sxs-lookup"><span data-stu-id="2e28a-350">click hello policy you are interested in inspecting.</span></span>

7.  <span data-ttu-id="2e28a-351">停用 hello 原則所設定的 hello**啟用原則**太切換**否**按一下 hello**儲存** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="2e28a-351">Disable hello policy by setting hello **Enable policy** toggle too**No** and click hello **Save** button.</span></span>

## <a name="problems-with-application-consent"></a><span data-ttu-id="2e28a-352">應用程式同意的問題</span><span class="sxs-lookup"><span data-stu-id="2e28a-352">Problems with application consent</span></span>

<span data-ttu-id="2e28a-353">因為尚未發生 hello 適當的權限同意作業，可能會封鎖應用程式的存取。</span><span class="sxs-lookup"><span data-stu-id="2e28a-353">Application access can be blocked because hello proper permissions consent operation has not occurred.</span></span> <span data-ttu-id="2e28a-354">以下提供一些方式，可讓您疑難排解並解決應用程式同意問題：</span><span class="sxs-lookup"><span data-stu-id="2e28a-354">Below are some ways you can troubleshoot and solve application consent issues:</span></span>

-   [<span data-ttu-id="2e28a-355">執行使用者層級同意作業</span><span class="sxs-lookup"><span data-stu-id="2e28a-355">Perform a user-level consent operation</span></span>](#perform-a-user-level-consent-operation)

-   [<span data-ttu-id="2e28a-356">為任何應用程式執行系統管理員層級同意作業</span><span class="sxs-lookup"><span data-stu-id="2e28a-356">Perform administrator-level consent operation for any application</span></span>](#perform-administrator-level-consent-operation-for-any-application)

-   [<span data-ttu-id="2e28a-357">為單一租用戶應用程式執行系統管理員層級同意</span><span class="sxs-lookup"><span data-stu-id="2e28a-357">Perform administrator-level consent for a single-tenant application</span></span>](#perform-administrator-level-consent-for-a-single-tenant-application)

-   [<span data-ttu-id="2e28a-358">為多租用戶應用程式執行系統管理員層級同意</span><span class="sxs-lookup"><span data-stu-id="2e28a-358">Perform administrator-level consent for a multi-tenant application</span></span>](#perform-administrator-level-consent-for-a-multi-tenant-application)

### <a name="perform-a-user-level-consent-operation"></a><span data-ttu-id="2e28a-359">執行使用者層級同意作業</span><span class="sxs-lookup"><span data-stu-id="2e28a-359">Perform a user-level consent operation</span></span>

-   <span data-ttu-id="2e28a-360">任何開啟連接的識別碼已啟用應用程式要求的權限，瀏覽 toohello 應用程式的登入畫面執行 hello 登入使用者的使用者同意層級 toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="2e28a-360">For any Open ID Connect-enabled application that requests permissions, navigating toohello application’s sign in screen performs a user level consent toohello application for hello signed-in user.</span></span>

-   <span data-ttu-id="2e28a-361">如果您想 toodo 此以程式設計的方式，請參閱[要求個別的使用者同意](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#requesting-individual-user-consent)。</span><span class="sxs-lookup"><span data-stu-id="2e28a-361">If you wish toodo this programmatically, see [Requesting individual user consent](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#requesting-individual-user-consent).</span></span>

### <a name="perform-administrator-level-consent-operation-for-any-application"></a><span data-ttu-id="2e28a-362">為任何應用程式執行系統管理員層級同意作業</span><span class="sxs-lookup"><span data-stu-id="2e28a-362">Perform administrator-level consent operation for any application</span></span>

-   <span data-ttu-id="2e28a-363">如**僅使用 hello V1 應用程式模型所開發的應用程式**，您可以藉由新增強制此系統管理員的同意層級 toooccur"**？ 提示 = admin\_同意**"toohello 結尾應用程式的登入 URL。</span><span class="sxs-lookup"><span data-stu-id="2e28a-363">For **only applications developed using hello V1 application model**, you can force this administrator level consent toooccur by adding “**?prompt=admin\_consent**” toohello end of an application’s sign in URL.</span></span>

-   <span data-ttu-id="2e28a-364">如**任何使用 hello V2 應用程式模型開發的應用程式**，您可以強制此系統管理員層級同意 toooccur hello 指示下 hello**要求 hello 權限的目錄系統管理員**區段[使用 hello 系統管理員同意端點](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint)。</span><span class="sxs-lookup"><span data-stu-id="2e28a-364">For **any application developed using hello V2 application model**, you can enforce this administrator-level consent toooccur by following hello instructions under hello **Request hello permissions from a directory admin** section of [Using hello admin consent endpoint](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span></span>

### <a name="perform-administrator-level-consent-for-a-single-tenant-application"></a><span data-ttu-id="2e28a-365">為單一租用戶應用程式執行系統管理員層級同意</span><span class="sxs-lookup"><span data-stu-id="2e28a-365">Perform administrator-level consent for a single-tenant application</span></span>

-   <span data-ttu-id="2e28a-366">如**單一租用戶應用程式**，來要求權限 （類似您所開發，或在您的組織擁有），您可以執行**系統管理層級同意**代表所有作業使用者的全域管理員身分登入，然後按一下 hello**授與權限**按鈕上方的 hello hello**應用程式登錄-&gt;所有應用程式-&gt;選取應用程式&gt;必要的使用權限**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="2e28a-366">For **single-tenant applications** that request permissions (like those you are developing or own in your organization), you can perform an **administrative-level consent** operation on behalf of all users by signing in as a Global Administrator and clicking on hello **Grant permissions** button at hello top of hello **Application Registry -&gt; All Applications -&gt; Select an App -&gt; Required Permissions** blade.</span></span>

-   <span data-ttu-id="2e28a-367">如**任何使用 hello V1 或 V2 應用程式模型開發的應用程式**，您可以強制此系統管理員層級同意 toooccur hello 指示下 hello**要求從 hello 權限目錄管理員**區段[使用 hello 系統管理員同意端點](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint)。</span><span class="sxs-lookup"><span data-stu-id="2e28a-367">For **any application developed using hello V1 or V2 application model**, you can enforce this administrator-level consent toooccur by following hello instructions under hello **Request hello permissions from a directory admin** section of [Using hello admin consent endpoint](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span></span>

### <a name="perform-administrator-level-consent-for-a-multi-tenant-application"></a><span data-ttu-id="2e28a-368">為多租用戶應用程式執行系統管理員層級同意</span><span class="sxs-lookup"><span data-stu-id="2e28a-368">Perform administrator-level consent for a multi-tenant application</span></span>

-   <span data-ttu-id="2e28a-369">適用於要求權限的**多租用戶應用程式** (例如第三方或 Microsoft 開發的應用程式)：您可以執行**系統管理員層級同意**作業。</span><span class="sxs-lookup"><span data-stu-id="2e28a-369">For **multi-tenant applications** that request permissions (like an application a third party, or Microsoft, develops), you can perform an **administrative-level consent** operation.</span></span> <span data-ttu-id="2e28a-370">全域管理員身分登入，並按一下 hello**授與權限**hello 下的按鈕**企業應用程式-&gt;所有應用程式-&gt;選取應用程式-&gt;權限**刀鋒視窗 (可立即)。</span><span class="sxs-lookup"><span data-stu-id="2e28a-370">Sign in as a Global Administrator and clicking on hello **Grant permissions** button under hello **Enterprise Applications -&gt; All Applications -&gt; Select an App -&gt; Permissions** blade (available soon).</span></span>

-   <span data-ttu-id="2e28a-371">您也可以強制此系統管理員層級同意 toooccur hello 指示下 hello **hello 權限要求目錄管理員從**區段[使用 hello 系統管理員同意端點](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span><span class="sxs-lookup"><span data-stu-id="2e28a-371">You can also enforce this administrator-level consent toooccur by following hello instructions under hello **Request hello permissions from a directory admin** section of [Using hello admin consent endpoint](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2e28a-372">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2e28a-372">Next steps</span></span>
[<span data-ttu-id="2e28a-373">使用 hello 系統管理員同意端點</span><span class="sxs-lookup"><span data-stu-id="2e28a-373">Using hello admin consent endpoint</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint)

