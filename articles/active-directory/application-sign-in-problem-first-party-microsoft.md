---
title: "登入 Microsoft 應用程式的問題 | Microsoft Docs"
description: "為使用 Azure AD 登入第一方 Microsoft 應用程式 (如 Office 365) 時遇到的問題疑難排解"
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
ms.openlocfilehash: 5638434270ee82d2b9737ea8eed8b5a8c62f7121
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
## <a name="problems-signing-in-to-a-microsoft-application"></a><span data-ttu-id="b3579-103">登入 Microsoft 應用程式的問題</span><span class="sxs-lookup"><span data-stu-id="b3579-103">Problems signing in to a Microsoft application</span></span>

<span data-ttu-id="b3579-104">Microsoft 應用程式 (如 Office 365 Exchange、SharePoint、Yammer 等) 在指派與管理方面，比第三方 SaaS 應用程式或與 Azure AD 整合以單一登入的其他應用程式略為困難。</span><span class="sxs-lookup"><span data-stu-id="b3579-104">Microsoft Applications (like Office 365 Exchange, SharePoint, Yammer, etc.) are assigned and managed a bit differently than 3rd party SaaS applications or other applications you integrate with Azure AD for single sign on.</span></span>

<span data-ttu-id="b3579-105">使用者有三種方式可取得 Microsoft 所發佈應用程式的存取權。</span><span class="sxs-lookup"><span data-stu-id="b3579-105">There are three main ways that a user can get access to a Microsoft-published application.</span></span>

-   <span data-ttu-id="b3579-106">對於 Office 365 或其他付費套件中的應用程式，會透過**指派授權**直接指派至使用者帳戶，或使用我們的群組授權指派功能來透過群組，將存取權授與使用者。</span><span class="sxs-lookup"><span data-stu-id="b3579-106">For applications in the Office 365 or other paid suites, users are granted access through **license assignment** either directly to their user account, or through a group using our group-based license assignment capability.</span></span>

-   <span data-ttu-id="b3579-107">對於 Microsoft 或第三方免費發佈給任何人使用的應用程式，會透過**使用者同意**將存取權授與使用者。</span><span class="sxs-lookup"><span data-stu-id="b3579-107">For applications that Microsoft or a Third Party publishes freely for anyone to use, users may be granted access through **user consent**.</span></span> <span data-ttu-id="b3579-108">這表示使用者透過其 Azure AD 工作或學校帳戶登入應用程式，並允許應用程式能夠存取其帳戶的某些受限制資料集。</span><span class="sxs-lookup"><span data-stu-id="b3579-108">This0 means that they sign in to the application with their Azure AD Work or School account and allow it to have access to some limited set of data on their account.</span></span>

-   <span data-ttu-id="b3579-109">對於 Microsoft 或第三方免費發佈給任何人使用的應用程式，也可透過**系統管理員同意**將存取權授與使用者。</span><span class="sxs-lookup"><span data-stu-id="b3579-109">For applications that Microsoft or a 3rd Party publishes freely for anyone to use, users may also be granted access through **administrator consent**.</span></span> <span data-ttu-id="b3579-110">這表示系統管理員已決定組織中的每個人都能使用該應用程式，因此系統管理員使用全域管理員帳戶身分登入應用程式，並將存取權授與組織中的每個人。</span><span class="sxs-lookup"><span data-stu-id="b3579-110">This means that an administrator has determined the application may be used by everyone in the organization, so they sign in to the application with a Global Administrator account and grant access to everyone in the organization.</span></span>

<span data-ttu-id="b3579-111">若要為您的問題疑難排解，請先從[一般應用程式存取問題考量事項](#general-problem-areas-with-application-access-to-consider)開始，然後參閱[逐步解說：Microsoft 應用程式存取疑難排解步驟](#walkthrough-steps-to-troubleshoot-microsoft-application-access)以了解詳細資料。</span><span class="sxs-lookup"><span data-stu-id="b3579-111">To troubleshoot your issue, start with the [General Problem Areas with Application Access to consider](#general-problem-areas-with-application-access-to-consider) and then read the [Walkthrough: Steps to troubleshoot Microsoft Application access](#walkthrough-steps-to-troubleshoot-microsoft-application-access) to get into the details.</span></span>

## <a name="general-problem-areas-with-application-access-to-consider"></a><span data-ttu-id="b3579-112">一般應用程式存取問題考量事項</span><span class="sxs-lookup"><span data-stu-id="b3579-112">General Problem Areas with Application Access to consider</span></span>

<span data-ttu-id="b3579-113">以下為一般問題清單，如果您知道從何處開始疑難排解，您可以從這個清單向下切入，但建議您參閱以下的逐步解說以快速進行：[逐步解說：Microsoft 應用程式存取疑難排解步驟](#walkthrough-steps-to-troubleshoot-microsoft-application-access)。</span><span class="sxs-lookup"><span data-stu-id="b3579-113">Below is a list of the general problem areas that you can drill into if you have an idea of where to start, but we recommend you read the walkthrough to get going quickly: [Walkthrough: Steps to troubleshoot Microsoft Application access](#walkthrough-steps-to-troubleshoot-microsoft-application-access).</span></span>

-   [<span data-ttu-id="b3579-114">使用者帳戶的問題</span><span class="sxs-lookup"><span data-stu-id="b3579-114">Problems with the user’s account</span></span>](#problems-with-the-users-account)

-   [<span data-ttu-id="b3579-115">群組的問題</span><span class="sxs-lookup"><span data-stu-id="b3579-115">Problems with groups</span></span>](#problems-with-groups)

-   [<span data-ttu-id="b3579-116">條件式存取原則的問題</span><span class="sxs-lookup"><span data-stu-id="b3579-116">Problems with conditional access policies</span></span>](#problems-with-conditional-access-policies)

-   [<span data-ttu-id="b3579-117">應用程式同意的問題</span><span class="sxs-lookup"><span data-stu-id="b3579-117">Problems with application consent</span></span>](#problems-with-application-consent)

## <a name="steps-to-troubleshoot-microsoft-application-access"></a><span data-ttu-id="b3579-118">Microsoft 應用程式存取疑難排解步驟</span><span class="sxs-lookup"><span data-stu-id="b3579-118">Steps to troubleshoot Microsoft Application access</span></span>

<span data-ttu-id="b3579-119">以下是一些使用者無法登入 Microsoft 應用程式的常見問題。</span><span class="sxs-lookup"><span data-stu-id="b3579-119">Below are some common issues folks run into when their users cannot sign in to a Microsoft application.</span></span>

-   <span data-ttu-id="b3579-120">首先檢查的一般問題</span><span class="sxs-lookup"><span data-stu-id="b3579-120">General issues to check first</span></span>

  * <span data-ttu-id="b3579-121">確定使用者登入的是**正確的 URL**，不是本機應用程式 URL。</span><span class="sxs-lookup"><span data-stu-id="b3579-121">Make sure the user is signing in to the **correct URL** and not a local application URL.</span></span>

  * <span data-ttu-id="b3579-122">確定使用者的帳戶**未鎖定**。</span><span class="sxs-lookup"><span data-stu-id="b3579-122">Make sure the user’s account is **not locked out.**</span></span>

  * <span data-ttu-id="b3579-123">確定 Azure Active Directory 中**有使用者的帳戶存在**。</span><span class="sxs-lookup"><span data-stu-id="b3579-123">Make sure the **user’s account exists** in Azure Active Directory.</span></span> [<span data-ttu-id="b3579-124">檢查 Azure Active Directory 中是否存在使用者帳戶</span><span class="sxs-lookup"><span data-stu-id="b3579-124">Check if a user account exists in Azure Active Directory</span></span>](#problems-with-the-users-account)

  * <span data-ttu-id="b3579-125">確定使用者的帳戶**已啟用**可供登入。</span><span class="sxs-lookup"><span data-stu-id="b3579-125">Make sure the user’s account is **enabled** for sign ins.</span></span> [<span data-ttu-id="b3579-126">檢查使用者帳戶的狀態</span><span class="sxs-lookup"><span data-stu-id="b3579-126">Check a user’s account status</span></span>](#problems-with-the-users-account)

  * <span data-ttu-id="b3579-127">確定使用者的**密碼未過期或忘記**。</span><span class="sxs-lookup"><span data-stu-id="b3579-127">Make sure the user’s **password is not expired or forgotten.**</span></span> <span data-ttu-id="b3579-128">[重設使用者密碼](#reset-a-users-password)或[啟用自助式密碼重設](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started)</span><span class="sxs-lookup"><span data-stu-id="b3579-128">[Reset a user’s password](#reset-a-users-password) or [Enable self-service password reset](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started)</span></span>

   * <span data-ttu-id="b3579-129">確定 **Multi-Factor Authentication** 未封鎖使用者存取。</span><span class="sxs-lookup"><span data-stu-id="b3579-129">Make sure **Multi-Factor Authentication** is not blocking user access.</span></span> <span data-ttu-id="b3579-130">[檢查使用者的多重要素驗證狀態](#check-a-users-multi-factor-authentication-status)或[檢查使用者的驗證連絡資訊](#check-a-users-authentication-contact-info)</span><span class="sxs-lookup"><span data-stu-id="b3579-130">[Check a user’s multi-factor authentication status](#check-a-users-multi-factor-authentication-status) or [Check a user’s authentication contact info](#check-a-users-authentication-contact-info)</span></span>

   * <span data-ttu-id="b3579-131">確定**條件式存取原則**或**身分識別保護**原則未封鎖使用者存取。</span><span class="sxs-lookup"><span data-stu-id="b3579-131">Make sure a **Conditional Access policy** or **Identity Protection** policy is not blocking user access.</span></span> <span data-ttu-id="b3579-132">[檢查特定條件式存取原則](#problems-with-conditional-access-policies)、[檢查特定應用程式條件式存取原則](#check-a-specific-applications-conditional-access-policy)或[停用特定條件式存取原則](#disable-a-specific-conditional-access-policy)</span><span class="sxs-lookup"><span data-stu-id="b3579-132">[Check a specific conditional access policy](#problems-with-conditional-access-policies) or [Check a specific application’s conditional access policy](#check-a-specific-applications-conditional-access-policy) or [Disable a specific conditional access policy](#disable-a-specific-conditional-access-policy)</span></span>

   * <span data-ttu-id="b3579-133">確定使用者的**驗證連絡資訊**為最新版本，而可強制執行 Multi-Factor Authentication 或條件式存取原則。</span><span class="sxs-lookup"><span data-stu-id="b3579-133">Make sure that a user’s **authentication contact info** is up to date to allow Multi-Factor Authentication or Conditional Access policies to be enforced.</span></span> <span data-ttu-id="b3579-134">[檢查使用者的多重要素驗證狀態](#check-a-users-multi-factor-authentication-status)或[檢查使用者的驗證連絡資訊](#check-a-users-authentication-contact-info)</span><span class="sxs-lookup"><span data-stu-id="b3579-134">[Check a user’s multi-factor authentication status](#check-a-users-multi-factor-authentication-status) or [Check a user’s authentication contact info](#check-a-users-authentication-contact-info)</span></span>

-   <span data-ttu-id="b3579-135">對於需要授權的 **Microsoft** **應用程式** (如 Office365)，以下是一些當您排除上述一般問題後要檢查的特定問題：</span><span class="sxs-lookup"><span data-stu-id="b3579-135">For **Microsoft** **applications that require a license** (like Office365), here are some specific issues to check once you have ruled out the general issues above:</span></span>

   * <span data-ttu-id="b3579-136">確定使用者已獲**授權指派**。</span><span class="sxs-lookup"><span data-stu-id="b3579-136">Ensure the user or has a **license assigned.**</span></span> <span data-ttu-id="b3579-137">[檢查使用者獲指派的授權](#check-a-users-assigned-licenses)或[檢查群組獲指派的授權](#check-a-groups-assigned-licenses)</span><span class="sxs-lookup"><span data-stu-id="b3579-137">[Check a user’s assigned licenses](#check-a-users-assigned-licenses) or [Check a group’s assigned licenses](#check-a-groups-assigned-licenses)</span></span>

   * <span data-ttu-id="b3579-138">如果將授權**指派至****靜態群組**，請確定**使用者屬於**該群組。</span><span class="sxs-lookup"><span data-stu-id="b3579-138">If the license is **assigned to a** **static group**, ensure that the **user is a member** of that group.</span></span> [<span data-ttu-id="b3579-139">檢查使用者的群組成員資格</span><span class="sxs-lookup"><span data-stu-id="b3579-139">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

   * <span data-ttu-id="b3579-140">如果授權**指派至****動態群組**，請確定**動態群組規則設定正確**。</span><span class="sxs-lookup"><span data-stu-id="b3579-140">If the license is **assigned to a** **dynamic group**, ensure that the **dynamic group rule is set correctly**.</span></span> [<span data-ttu-id="b3579-141">檢查動態群組成員資格準則</span><span class="sxs-lookup"><span data-stu-id="b3579-141">Check a dynamic group’s membership criteria</span></span>](#check-a-dynamic-groups-membership-criteria)

   * <span data-ttu-id="b3579-142">如果授權**指派至****動態群組**，請確定動態群組已**完成處理**其成員資格，且**使用者為成員** (這可能需要一些時間)。</span><span class="sxs-lookup"><span data-stu-id="b3579-142">If the license is **assigned to a** **dynamic group**, ensure that the dynamic group has **finished processing** its membership and that the **user is a member** (this can take some time).</span></span> [<span data-ttu-id="b3579-143">檢查使用者的群組成員資格</span><span class="sxs-lookup"><span data-stu-id="b3579-143">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

   *  <span data-ttu-id="b3579-144">一旦您確定授權已指派，請確定授權**尚未過期**。</span><span class="sxs-lookup"><span data-stu-id="b3579-144">Once you make sure the license is assigned, make sure the license is **not expired**.</span></span>

   *  <span data-ttu-id="b3579-145">確定授權適用於目前正在存取的**應用程式**。</span><span class="sxs-lookup"><span data-stu-id="b3579-145">Make sure the license is **for the application** they are accessing.</span></span>

-   <span data-ttu-id="b3579-146">對於不需要授權的 **Microsoft** **應用程式**，以下為其他的檢查事項：</span><span class="sxs-lookup"><span data-stu-id="b3579-146">For **Microsoft** **applications that don’t require a license**, here are some other things to check:</span></span>

   * <span data-ttu-id="b3579-147">如果應用程式要求的是**使用者層級權限** (例如「存取此使用者的信箱」)，請確定使用者已登入該應用程式，並已執行**使用者層級同意作業**，讓應用程式可存取其資料。</span><span class="sxs-lookup"><span data-stu-id="b3579-147">If the application is requesting **user-level permissions** (for example “Access this user’s mailbox”), make sure that the user has signed in to the application and has performed a **user-level consent operation** to let the application access her data.</span></span>

   * <span data-ttu-id="b3579-148">如果應用程式要求的是**系統管理員層級權限** (例如「存取所有使用者的信箱」)，請確定全域管理員已**代表組織中所有使用者執行系統管理員層級同意作業**。</span><span class="sxs-lookup"><span data-stu-id="b3579-148">If the application is requesting **administrator-level permissions** (for example “Access all user’s mailboxes”), make sure that a Global Administrator has performed an **administrator-level consent operation on behalf of all users** in the organization.</span></span>

## <a name="problems-with-the-users-account"></a><span data-ttu-id="b3579-149">使用者帳戶的問題</span><span class="sxs-lookup"><span data-stu-id="b3579-149">Problems with the user’s account</span></span>

<span data-ttu-id="b3579-150">當指派至應用程式的使用者有問題時，可封鎖應用程式存取權。</span><span class="sxs-lookup"><span data-stu-id="b3579-150">Application access can be blocked due to a problem with a user that is assigned to the application.</span></span> <span data-ttu-id="b3579-151">以下是針對使用者和其帳戶設定進行疑難排解的一些方法︰</span><span class="sxs-lookup"><span data-stu-id="b3579-151">Below are some ways you can troubleshoot and solve problems with users and their account settings:</span></span>

-   [<span data-ttu-id="b3579-152">檢查 Azure Active Directory 中是否存在使用者帳戶</span><span class="sxs-lookup"><span data-stu-id="b3579-152">Check if a user account exists in Azure Active Directory</span></span>](#check-if-a-user-account-exists-in-azure-active-directory)

-   [<span data-ttu-id="b3579-153">檢查使用者帳戶的狀態</span><span class="sxs-lookup"><span data-stu-id="b3579-153">Check a user’s account status</span></span>](#check-a-users-account-status)

-   [<span data-ttu-id="b3579-154">重設使用者的密碼</span><span class="sxs-lookup"><span data-stu-id="b3579-154">Reset a user’s password</span></span>](#reset-a-users-password)

-   [<span data-ttu-id="b3579-155">啟用自助密碼重設</span><span class="sxs-lookup"><span data-stu-id="b3579-155">Enable self-service password reset</span></span>](#enable-self-service-password-reset)

-   [<span data-ttu-id="b3579-156">檢查使用者的多重要素驗證狀態</span><span class="sxs-lookup"><span data-stu-id="b3579-156">Check a user’s multi-factor authentication status</span></span>](#check-a-users-multi-factor-authentication-status)

-   [<span data-ttu-id="b3579-157">檢查使用者的驗證連絡資訊</span><span class="sxs-lookup"><span data-stu-id="b3579-157">Check a user’s authentication contact info</span></span>](#check-a-users-authentication-contact-info)

-   [<span data-ttu-id="b3579-158">檢查使用者的群組成員資格</span><span class="sxs-lookup"><span data-stu-id="b3579-158">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

-   [<span data-ttu-id="b3579-159">檢查使用者獲指派的授權</span><span class="sxs-lookup"><span data-stu-id="b3579-159">Check a user’s assigned licenses</span></span>](#check-a-users-assigned-licenses)

-   [<span data-ttu-id="b3579-160">指派授權至使用者</span><span class="sxs-lookup"><span data-stu-id="b3579-160">Assign a user a license</span></span>](#assign-a-user-a-license)

### <a name="check-if-a-user-account-exists-in-azure-active-directory"></a><span data-ttu-id="b3579-161">檢查 Azure Active Directory 中是否存在使用者帳戶</span><span class="sxs-lookup"><span data-stu-id="b3579-161">Check if a user account exists in Azure Active Directory</span></span>

<span data-ttu-id="b3579-162">若要檢查使用者的帳戶是否存在，請依照下列步驟執行：</span><span class="sxs-lookup"><span data-stu-id="b3579-162">To check if a user’s account is present, follow the steps below:</span></span>

1.  <span data-ttu-id="b3579-163">開啟 [**Azure 入口網站**](https://portal.azure.com/)，以**全域管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="b3579-163">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="b3579-164">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="b3579-164">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="b3579-165">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="b3579-165">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="b3579-166">按一下瀏覽功能表中的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="b3579-166">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="b3579-167">按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="b3579-167">click **All users**.</span></span>

6.  <span data-ttu-id="b3579-168">**搜尋**您感興趣的使用者，**按一下資料列**選取該使用者。</span><span class="sxs-lookup"><span data-stu-id="b3579-168">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="b3579-169">檢查使用者物件的屬性，確定符合您的預期，沒有遺失資料。</span><span class="sxs-lookup"><span data-stu-id="b3579-169">Check the properties of the user object to be sure that they look as you expect and no data is missing.</span></span>

### <a name="check-a-users-account-status"></a><span data-ttu-id="b3579-170">檢查使用者帳戶的狀態</span><span class="sxs-lookup"><span data-stu-id="b3579-170">Check a user’s account status</span></span>

<span data-ttu-id="b3579-171">若要檢查使用者帳戶的狀態，請依照下列步驟執行：</span><span class="sxs-lookup"><span data-stu-id="b3579-171">To check a user’s account status, follow the steps below:</span></span>

1.  <span data-ttu-id="b3579-172">開啟 [**Azure 入口網站**](https://portal.azure.com/)，以**全域管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="b3579-172">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="b3579-173">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="b3579-173">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="b3579-174">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="b3579-174">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="b3579-175">按一下瀏覽功能表中的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="b3579-175">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="b3579-176">按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="b3579-176">click **All users**.</span></span>

6.  <span data-ttu-id="b3579-177">**搜尋**您感興趣的使用者，**按一下資料列**選取該使用者。</span><span class="sxs-lookup"><span data-stu-id="b3579-177">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="b3579-178">按一下 [設定檔]。</span><span class="sxs-lookup"><span data-stu-id="b3579-178">click **Profile**.</span></span>

8.  <span data-ttu-id="b3579-179">在 [設定] 下，確定 [封鎖登入] 設為 [否]。</span><span class="sxs-lookup"><span data-stu-id="b3579-179">Under **Settings** ensure that **Block sign in** is set to **No**.</span></span>

### <a name="reset-a-users-password"></a><span data-ttu-id="b3579-180">重設使用者的密碼</span><span class="sxs-lookup"><span data-stu-id="b3579-180">Reset a user’s password</span></span>

<span data-ttu-id="b3579-181">若要重設使用者的密碼，請依照下列步驟執行：</span><span class="sxs-lookup"><span data-stu-id="b3579-181">To reset a user’s password, follow the steps below:</span></span>

1.  <span data-ttu-id="b3579-182">開啟 [**Azure 入口網站**](https://portal.azure.com/)，以**全域管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="b3579-182">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="b3579-183">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="b3579-183">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="b3579-184">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="b3579-184">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="b3579-185">按一下瀏覽功能表中的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="b3579-185">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="b3579-186">按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="b3579-186">click **All users**.</span></span>

6.  <span data-ttu-id="b3579-187">**搜尋**您感興趣的使用者，**按一下資料列**選取該使用者。</span><span class="sxs-lookup"><span data-stu-id="b3579-187">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="b3579-188">按一下使用者刀鋒視窗頂端的 [重設密碼]按鈕。</span><span class="sxs-lookup"><span data-stu-id="b3579-188">click the **Reset password** button at the top of the user blade.</span></span>

8.  <span data-ttu-id="b3579-189">在出現的 [重設密碼] 刀鋒視窗上，按一下 [重設密碼] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b3579-189">click the **Reset password** button on the **Reset password** blade that appears.</span></span>

9.  <span data-ttu-id="b3579-190">為使用者複製**暫時密碼**或**輸入新密碼**。</span><span class="sxs-lookup"><span data-stu-id="b3579-190">Copy the **temporary password** or **enter a new password** for the user.</span></span>

10. <span data-ttu-id="b3579-191">將這個新的密碼告知使用者，他們下次登入 Azure Active Directory 時必須變更此密碼。</span><span class="sxs-lookup"><span data-stu-id="b3579-191">Communicate this new password to the user, they be required to change this password during their next sign in to Azure Active Directory.</span></span>

### <a name="enable-self-service-password-reset"></a><span data-ttu-id="b3579-192">啟用自助式密碼重設</span><span class="sxs-lookup"><span data-stu-id="b3579-192">Enable self-service password reset</span></span>

<span data-ttu-id="b3579-193">若要啟用自助式密碼重設，請遵循下列部署步驟︰</span><span class="sxs-lookup"><span data-stu-id="b3579-193">To enable self-service password reset, follow the deployment steps below:</span></span>

-   [<span data-ttu-id="b3579-194">讓使用者重設其 Azure Active Directory 密碼</span><span class="sxs-lookup"><span data-stu-id="b3579-194">Enable users to reset their Azure Active Directory passwords</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-their-azure-ad-passwords)

-   [<span data-ttu-id="b3579-195">讓使用者重設或變更其 Active Directory 內部部署密碼</span><span class="sxs-lookup"><span data-stu-id="b3579-195">Enable users to reset or change their Active Directory on-premises passwords</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-or-change-their-ad-passwords)

### <a name="check-a-users-multi-factor-authentication-status"></a><span data-ttu-id="b3579-196">檢查使用者的多重要素驗證狀態</span><span class="sxs-lookup"><span data-stu-id="b3579-196">Check a user’s multi-factor authentication status</span></span>

<span data-ttu-id="b3579-197">若要檢查使用者的多重要素驗證狀態，請依照下列步驟執行：</span><span class="sxs-lookup"><span data-stu-id="b3579-197">To check a user’s multi-factor authentication status, follow the steps below:</span></span>

1.  <span data-ttu-id="b3579-198">開啟 [**Azure 入口網站**](https://portal.azure.com/)，以**全域管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="b3579-198">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="b3579-199">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="b3579-199">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="b3579-200">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="b3579-200">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="b3579-201">按一下瀏覽功能表中的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="b3579-201">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="b3579-202">按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="b3579-202">click **All users**.</span></span>

6.  <span data-ttu-id="b3579-203">按一下刀鋒視窗頂端的 [Multi-Factor Authentication] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b3579-203">click the **Multi-Factor Authentication** button at the top of the blade.</span></span>

7.  <span data-ttu-id="b3579-204">當 **Multi-Factor Authentication 管理網站**載入後，請確定您位於 [使用者] 索引標籤上。</span><span class="sxs-lookup"><span data-stu-id="b3579-204">Once the **Multi-Factor Authentication Administration Portal** loads, ensure you are on the **Users** tab.</span></span>

8.  <span data-ttu-id="b3579-205">在使用者清單中搜尋、篩選或排序來尋找使用者。</span><span class="sxs-lookup"><span data-stu-id="b3579-205">Find the user in the list of users by searching, filtering, or sorting.</span></span>

9.  <span data-ttu-id="b3579-206">從使用者清單中選取使用者，然後視需要 [啟用]、[停用] 或 [強制執行] 多重要素驗證。</span><span class="sxs-lookup"><span data-stu-id="b3579-206">Select the user from the list of users and **Enable**, **Disable**, or **Enforce** multi-factor authentication as desired.</span></span>

  * <span data-ttu-id="b3579-207">**注意**：如果使用者處理 [已強制] 狀態，您可以暫時將他們設為 [已停用]，讓他們回到各自的帳戶。</span><span class="sxs-lookup"><span data-stu-id="b3579-207">**Note**: If a user is in an **Enforced** state, you may set them to **Disabled** temporarily to let them back into their account.</span></span> <span data-ttu-id="b3579-208">退回之後，您可以再次將其狀態變更為 [已啟用]，以要求他們在下次登入時重新註冊連絡資訊。</span><span class="sxs-lookup"><span data-stu-id="b3579-208">Once they are back in, you can then change their state to **Enabled** again to require them to re-register their contact information during their next sign in.</span></span> <span data-ttu-id="b3579-209">或者，您可以依照[檢查使用者的驗證連絡資訊](#check-a-users-authentication-contact-info)中的步驟，為他們確認或設定此資料。</span><span class="sxs-lookup"><span data-stu-id="b3579-209">Alternatively, you can follow the steps in the [Check a user’s authentication contact info](#check-a-users-authentication-contact-info) to verify or set this data for them.</span></span>

### <a name="check-a-users-authentication-contact-info"></a><span data-ttu-id="b3579-210">檢查使用者的驗證連絡資訊</span><span class="sxs-lookup"><span data-stu-id="b3579-210">Check a user’s authentication contact info</span></span>

<span data-ttu-id="b3579-211">若要檢查用於多重要素驗證、條件式存取、身分識別保護和密碼重設的使用者驗證連絡資訊，請依照下列步驟執行︰</span><span class="sxs-lookup"><span data-stu-id="b3579-211">To check a user’s authentication contact info used for Multi-factor authentication, Conditional Access, Identity Protection, and Password Reset, follow the steps below:</span></span>

1.  <span data-ttu-id="b3579-212">開啟 [**Azure 入口網站**](https://portal.azure.com/)，以**全域管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="b3579-212">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="b3579-213">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="b3579-213">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="b3579-214">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="b3579-214">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="b3579-215">按一下瀏覽功能表中的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="b3579-215">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="b3579-216">按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="b3579-216">click **All users**.</span></span>

6.  <span data-ttu-id="b3579-217">**搜尋**您感興趣的使用者，**按一下資料列**選取該使用者。</span><span class="sxs-lookup"><span data-stu-id="b3579-217">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="b3579-218">按一下 [設定檔]。</span><span class="sxs-lookup"><span data-stu-id="b3579-218">click **Profile**.</span></span>

8.  <span data-ttu-id="b3579-219">向下捲動至 [驗證連絡資訊]。</span><span class="sxs-lookup"><span data-stu-id="b3579-219">Scroll down to **Authentication contact info**.</span></span>

9.  <span data-ttu-id="b3579-220">**檢閱**使用者註冊的資料，並視需要予以更新。</span><span class="sxs-lookup"><span data-stu-id="b3579-220">**Review** the data registered for the user and update as needed.</span></span>

### <a name="check-a-users-group-memberships"></a><span data-ttu-id="b3579-221">檢查使用者的群組成員資格</span><span class="sxs-lookup"><span data-stu-id="b3579-221">Check a user’s group memberships</span></span>

<span data-ttu-id="b3579-222">若要檢查使用者的群組成員資格，請依照下列步驟執行：</span><span class="sxs-lookup"><span data-stu-id="b3579-222">To check a user’s group memberships, follow the steps below:</span></span>

1.  <span data-ttu-id="b3579-223">開啟 [**Azure 入口網站**](https://portal.azure.com/)，以**全域管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="b3579-223">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="b3579-224">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="b3579-224">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="b3579-225">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="b3579-225">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="b3579-226">按一下瀏覽功能表中的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="b3579-226">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="b3579-227">按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="b3579-227">click **All users**.</span></span>

6.  <span data-ttu-id="b3579-228">**搜尋**您感興趣的使用者，**按一下資料列**選取該使用者。</span><span class="sxs-lookup"><span data-stu-id="b3579-228">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="b3579-229">按一下 [群組]，查看使用者是哪些群組的成員。</span><span class="sxs-lookup"><span data-stu-id="b3579-229">click **Groups** to see which groups the user is a member of.</span></span>

### <a name="check-a-users-assigned-licenses"></a><span data-ttu-id="b3579-230">檢查使用者獲指派的授權</span><span class="sxs-lookup"><span data-stu-id="b3579-230">Check a user’s assigned licenses</span></span>

<span data-ttu-id="b3579-231">若要檢查使用者獲指派的授權，請依照下列步驟執行：</span><span class="sxs-lookup"><span data-stu-id="b3579-231">To check a user’s assigned licenses, follow the steps below:</span></span>

1.  <span data-ttu-id="b3579-232">開啟 [**Azure 入口網站**](https://portal.azure.com/)，以**全域管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="b3579-232">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="b3579-233">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="b3579-233">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="b3579-234">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="b3579-234">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="b3579-235">按一下瀏覽功能表中的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="b3579-235">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="b3579-236">按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="b3579-236">click **All users**.</span></span>

6.  <span data-ttu-id="b3579-237">**搜尋**您感興趣的使用者，**按一下資料列**選取該使用者。</span><span class="sxs-lookup"><span data-stu-id="b3579-237">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="b3579-238">按一下 [授權]，查看使用者目前已指派的授權。</span><span class="sxs-lookup"><span data-stu-id="b3579-238">click **Licenses** to see which licenses the user currently has assigned.</span></span>

### <a name="assign-a-user-a-license"></a><span data-ttu-id="b3579-239">指派授權至使用者</span><span class="sxs-lookup"><span data-stu-id="b3579-239">Assign a user a license</span></span> 

<span data-ttu-id="b3579-240">若要指派授權至使用者，請依照下列步驟執行︰</span><span class="sxs-lookup"><span data-stu-id="b3579-240">To assign a license to a user, follow the steps below:</span></span>

1.  <span data-ttu-id="b3579-241">開啟 [**Azure 入口網站**](https://portal.azure.com/)，以**全域管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="b3579-241">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="b3579-242">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="b3579-242">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="b3579-243">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="b3579-243">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="b3579-244">按一下瀏覽功能表中的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="b3579-244">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="b3579-245">按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="b3579-245">click **All users**.</span></span>

6.  <span data-ttu-id="b3579-246">**搜尋**您感興趣的使用者，**按一下資料列**選取該使用者。</span><span class="sxs-lookup"><span data-stu-id="b3579-246">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="b3579-247">按一下 [授權]，查看使用者目前已指派的授權。</span><span class="sxs-lookup"><span data-stu-id="b3579-247">click **Licenses** to see which licenses the user currently has assigned.</span></span>

8.  <span data-ttu-id="b3579-248">按一下 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b3579-248">click the **Assign** button.</span></span>

9.  <span data-ttu-id="b3579-249">從可用產品清單中選取**一或多個產品**。</span><span class="sxs-lookup"><span data-stu-id="b3579-249">Select **one or more products** from the list of available products.</span></span>

10. <span data-ttu-id="b3579-250">(**選擇性**) 按一下 [指派選項] 項目，更細微地指派產品。</span><span class="sxs-lookup"><span data-stu-id="b3579-250">**Optional** click the **assignment options** item to granularly assign products.</span></span> <span data-ttu-id="b3579-251">完成時按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="b3579-251">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="b3579-252">按一下 [指派] 按鈕，將這些授權指派至這位使用者。</span><span class="sxs-lookup"><span data-stu-id="b3579-252">Click the **Assign** button to assign these licenses to this user.</span></span>

## <a name="problems-with-groups"></a><span data-ttu-id="b3579-253">群組的問題</span><span class="sxs-lookup"><span data-stu-id="b3579-253">Problems with groups</span></span>

<span data-ttu-id="b3579-254">當指派至應用程式的群組有問題時，可封鎖應用程式存取權。</span><span class="sxs-lookup"><span data-stu-id="b3579-254">Application access can be blocked due to a problem with a group that is assigned to the application.</span></span> <span data-ttu-id="b3579-255">以下是為群組和群組成員資格問題疑難排解的一些方法︰</span><span class="sxs-lookup"><span data-stu-id="b3579-255">Below are some ways you can troubleshoot and solve problems with groups and group memberships:</span></span>

-   [<span data-ttu-id="b3579-256">檢查群組成員資格</span><span class="sxs-lookup"><span data-stu-id="b3579-256">Check a group’s membership</span></span>](#check-a-groups-membership)

-   [<span data-ttu-id="b3579-257">檢查動態群組成員資格準則</span><span class="sxs-lookup"><span data-stu-id="b3579-257">Check a dynamic group’s membership criteria</span></span>](#check-a-dynamic-groups-membership-criteria)

-   [<span data-ttu-id="b3579-258">檢查群組獲指派的授權</span><span class="sxs-lookup"><span data-stu-id="b3579-258">Check a group’s assigned licenses</span></span>](#check-a-groups-assigned-licenses)

-   [<span data-ttu-id="b3579-259">重新處理群組的授權</span><span class="sxs-lookup"><span data-stu-id="b3579-259">Reprocess a group’s licenses</span></span>](#reprocess-a-groups-licenses)

-   [<span data-ttu-id="b3579-260">指派授權至群組</span><span class="sxs-lookup"><span data-stu-id="b3579-260">Assign a group a license</span></span>](#assign-a-group-a-license)

### <a name="check-a-groups-membership"></a><span data-ttu-id="b3579-261">檢查群組成員資格</span><span class="sxs-lookup"><span data-stu-id="b3579-261">Check a group’s membership</span></span>

<span data-ttu-id="b3579-262">若要檢查群組的成員資格，請依照下列步驟執行：</span><span class="sxs-lookup"><span data-stu-id="b3579-262">To check a group’s membership, follow the steps below:</span></span>

1.  <span data-ttu-id="b3579-263">開啟 [**Azure 入口網站**](https://portal.azure.com/)，以**全域管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="b3579-263">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="b3579-264">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="b3579-264">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="b3579-265">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="b3579-265">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="b3579-266">按一下瀏覽功能表中的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="b3579-266">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="b3579-267">按一下 [所有群組]。</span><span class="sxs-lookup"><span data-stu-id="b3579-267">click **All groups**.</span></span>

6.  <span data-ttu-id="b3579-268">**搜尋**您感興趣的群組，然後**按一下資料列**加以選取。</span><span class="sxs-lookup"><span data-stu-id="b3579-268">**Search** for the group you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="b3579-269">按一下 [成員] 以檢閱已指派至此群組的使用者清單。</span><span class="sxs-lookup"><span data-stu-id="b3579-269">click **Members** to review the list of users assigned to this group.</span></span>

### <a name="check-a-dynamic-groups-membership-criteria"></a><span data-ttu-id="b3579-270">檢查動態群組成員資格準則</span><span class="sxs-lookup"><span data-stu-id="b3579-270">Check a dynamic group’s membership criteria</span></span> 

<span data-ttu-id="b3579-271">若要檢查動態群組的成員資格準則，請依照下列步驟執行：</span><span class="sxs-lookup"><span data-stu-id="b3579-271">To check a dynamic group’s membership criteria, follow the steps below:</span></span>

1.  <span data-ttu-id="b3579-272">開啟 [**Azure 入口網站**](https://portal.azure.com/)，以**全域管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="b3579-272">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="b3579-273">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="b3579-273">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="b3579-274">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="b3579-274">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="b3579-275">按一下瀏覽功能表中的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="b3579-275">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="b3579-276">按一下 [所有群組]。</span><span class="sxs-lookup"><span data-stu-id="b3579-276">click **All groups**.</span></span>

6.  <span data-ttu-id="b3579-277">**搜尋**您感興趣的群組，然後**按一下資料列**加以選取。</span><span class="sxs-lookup"><span data-stu-id="b3579-277">**Search** for the group you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="b3579-278">按一下 [動態成員資格規則]。</span><span class="sxs-lookup"><span data-stu-id="b3579-278">click **Dynamic membership rules.**</span></span>

8.  <span data-ttu-id="b3579-279">檢閱為此群組定義的**簡單**或 **進階**規則，確定您要成為此群組成員的使用者符合這些準則。</span><span class="sxs-lookup"><span data-stu-id="b3579-279">Review the **simple** or **advanced** rule defined for this group and ensure that the user you want to be a member of this group meets these criteria.</span></span>

### <a name="check-a-groups-assigned-licenses"></a><span data-ttu-id="b3579-280">檢查群組獲指派的授權</span><span class="sxs-lookup"><span data-stu-id="b3579-280">Check a group’s assigned licenses</span></span>

<span data-ttu-id="b3579-281">若要檢查群組獲指派的授權，請依照下列步驟執行：</span><span class="sxs-lookup"><span data-stu-id="b3579-281">To check a group’s assigned licenses, follow the steps below:</span></span>

1.  <span data-ttu-id="b3579-282">開啟 [**Azure 入口網站**](https://portal.azure.com/)，以**全域管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="b3579-282">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="b3579-283">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="b3579-283">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="b3579-284">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="b3579-284">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="b3579-285">按一下瀏覽功能表中的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="b3579-285">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="b3579-286">按一下 [所有群組]。</span><span class="sxs-lookup"><span data-stu-id="b3579-286">click **All groups**.</span></span>

6.  <span data-ttu-id="b3579-287">**搜尋**您感興趣的群組，然後**按一下資料列**加以選取。</span><span class="sxs-lookup"><span data-stu-id="b3579-287">**Search** for the group you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="b3579-288">按一下 [授權]，以查看目前已指派至群組的授權。</span><span class="sxs-lookup"><span data-stu-id="b3579-288">click **Licenses** to see which licenses the group currently has assigned.</span></span>

### <a name="reprocess-a-groups-licenses"></a><span data-ttu-id="b3579-289">重新處理群組的授權</span><span class="sxs-lookup"><span data-stu-id="b3579-289">Reprocess a group’s licenses</span></span>

<span data-ttu-id="b3579-290">若要重新處理群組獲指派的授權，請依照下列步驟執行：</span><span class="sxs-lookup"><span data-stu-id="b3579-290">To reprocess a group’s assigned licenses, follow the steps below:</span></span>

1.  <span data-ttu-id="b3579-291">開啟 [**Azure 入口網站**](https://portal.azure.com/)，以**全域管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="b3579-291">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="b3579-292">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="b3579-292">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="b3579-293">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="b3579-293">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="b3579-294">按一下瀏覽功能表中的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="b3579-294">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="b3579-295">按一下 [所有群組]。</span><span class="sxs-lookup"><span data-stu-id="b3579-295">click **All groups**.</span></span>

6.  <span data-ttu-id="b3579-296">**搜尋**您感興趣的群組，然後**按一下資料列**加以選取。</span><span class="sxs-lookup"><span data-stu-id="b3579-296">**Search** for the group you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="b3579-297">按一下 [授權]，以查看目前已指派至群組的授權。</span><span class="sxs-lookup"><span data-stu-id="b3579-297">click **Licenses** to see which licenses the group currently has assigned.</span></span>

8.  <span data-ttu-id="b3579-298">按一下 [重新處理] 按鈕，以確定指派至此群組成員的授權是最新的。</span><span class="sxs-lookup"><span data-stu-id="b3579-298">click the **Reprocess** button to ensure that the licenses assigned to this group’s members are up-to-date.</span></span> <span data-ttu-id="b3579-299">根據群組的大小和複雜度，這可能需要很長的時間。</span><span class="sxs-lookup"><span data-stu-id="b3579-299">This may take a long time, depending on the size and complexity of the group.</span></span>

   >[!NOTE]
   ><span data-ttu-id="b3579-300">若要更快速執行此作業，請考慮暫時將授權直接指派至使用者。</span><span class="sxs-lookup"><span data-stu-id="b3579-300">To do this faster, consider temporarily assigning a license to the user directly.</span></span> <span data-ttu-id="b3579-301">[指派授權至使用者](#problems-with-application-consent)。</span><span class="sxs-lookup"><span data-stu-id="b3579-301">[Assign a user a license](#problems-with-application-consent).</span></span>
   >
   >

### <a name="assign-a-group-a-license"></a><span data-ttu-id="b3579-302">指派授權至群組</span><span class="sxs-lookup"><span data-stu-id="b3579-302">Assign a group a license</span></span>

<span data-ttu-id="b3579-303">若要將授權指派至群組，請依照下列步驟執行：</span><span class="sxs-lookup"><span data-stu-id="b3579-303">To assign a license to a group, follow the steps below:</span></span>

1.  <span data-ttu-id="b3579-304">開啟 [**Azure 入口網站**](https://portal.azure.com/)，以**全域管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="b3579-304">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="b3579-305">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="b3579-305">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="b3579-306">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="b3579-306">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="b3579-307">按一下瀏覽功能表中的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="b3579-307">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="b3579-308">按一下 [所有群組]。</span><span class="sxs-lookup"><span data-stu-id="b3579-308">click **All groups**.</span></span>

6.  <span data-ttu-id="b3579-309">**搜尋**您感興趣的群組，然後**按一下資料列**加以選取。</span><span class="sxs-lookup"><span data-stu-id="b3579-309">**Search** for the group you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="b3579-310">按一下 [授權]，以查看目前已指派至群組的授權。</span><span class="sxs-lookup"><span data-stu-id="b3579-310">click **Licenses** to see which licenses the group currently has assigned.</span></span>

8.  <span data-ttu-id="b3579-311">按一下 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b3579-311">click the **Assign** button.</span></span>

9.  <span data-ttu-id="b3579-312">從可用產品清單中選取**一或多個產品**。</span><span class="sxs-lookup"><span data-stu-id="b3579-312">Select **one or more products** from the list of available products.</span></span>

10. <span data-ttu-id="b3579-313">(**選擇性**) 按一下 [指派選項] 項目，更細微地指派產品。</span><span class="sxs-lookup"><span data-stu-id="b3579-313">**Optional** click the **assignment options** item to granularly assign products.</span></span> <span data-ttu-id="b3579-314">完成時按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="b3579-314">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="b3579-315">按一下 [指派] 按鈕，將這些授權指派至這個群組。</span><span class="sxs-lookup"><span data-stu-id="b3579-315">Click the **Assign** button to assign these licenses to this group.</span></span> <span data-ttu-id="b3579-316">根據群組的大小和複雜度，這可能需要很長的時間。</span><span class="sxs-lookup"><span data-stu-id="b3579-316">This may take a long time, depending on the size and complexity of the group.</span></span>

   >[!NOTE]
   ><span data-ttu-id="b3579-317">若要更快速執行此作業，請考慮暫時將授權直接指派至使用者。</span><span class="sxs-lookup"><span data-stu-id="b3579-317">To do this faster, consider temporarily assigning a license to the user directly.</span></span> <span data-ttu-id="b3579-318">[指派授權至使用者](#problems-with-application-consent)。</span><span class="sxs-lookup"><span data-stu-id="b3579-318">[Assign a user a license](#problems-with-application-consent).</span></span>
   > 
   >

## <a name="problems-with-conditional-access-policies"></a><span data-ttu-id="b3579-319">條件式存取原則的問題</span><span class="sxs-lookup"><span data-stu-id="b3579-319">Problems with conditional access policies</span></span>

### <a name="check-a-specific-conditional-access-policy"></a><span data-ttu-id="b3579-320">檢查特定的條件式存取原則</span><span class="sxs-lookup"><span data-stu-id="b3579-320">Check a specific conditional access policy</span></span>

<span data-ttu-id="b3579-321">若要檢查或驗證單一條件式存取原則︰</span><span class="sxs-lookup"><span data-stu-id="b3579-321">To check or validate a single conditional access policy:</span></span>

1.  <span data-ttu-id="b3579-322">開啟 [**Azure 入口網站**](https://portal.azure.com/)，以**全域管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="b3579-322">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="b3579-323">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="b3579-323">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="b3579-324">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="b3579-324">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="b3579-325">按一下瀏覽功能表中的 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="b3579-325">click **Enterprise applications** in the navigation menu.</span></span>

5.  <span data-ttu-id="b3579-326">按一下 [條件式存取] 瀏覽項目。</span><span class="sxs-lookup"><span data-stu-id="b3579-326">click the **Conditional access** navigation item.</span></span>

6.  <span data-ttu-id="b3579-327">按一下您想要檢查的原則。</span><span class="sxs-lookup"><span data-stu-id="b3579-327">click the policy you are interested in inspecting.</span></span>

7.  <span data-ttu-id="b3579-328">檢查有無特定的條件、指派，或其他可能會封鎖使用者存取的設定。</span><span class="sxs-lookup"><span data-stu-id="b3579-328">Review that there are no specific conditions, assignments, or other settings which may be blocking user access.</span></span>

   >[!NOTE]
   ><span data-ttu-id="b3579-329">您可能會想要暫時停用此原則，以確保不會影響登入。</span><span class="sxs-lookup"><span data-stu-id="b3579-329">You may wish to temporarily disable this policy to ensure it is not affecting sign ins.</span></span> <span data-ttu-id="b3579-330">若要這麼做，請設定 [啟用原則] 切換至 [否]，然後按一下 [儲存] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b3579-330">To do this, set the **Enable policy** toggle to **No** and click the **Save** button.</span></span>
   >
   >

### <a name="check-a-specific-applications-conditional-access-policy"></a><span data-ttu-id="b3579-331">檢查特定應用程式的條件式存取原則</span><span class="sxs-lookup"><span data-stu-id="b3579-331">Check a specific application’s conditional access policy</span></span>

<span data-ttu-id="b3579-332">若要檢查或驗證單一應用程式目前設定的條件式存取原則︰</span><span class="sxs-lookup"><span data-stu-id="b3579-332">To check or validate a single application’s currently configured conditional access policy:</span></span>

1.  <span data-ttu-id="b3579-333">開啟 [**Azure 入口網站**](https://portal.azure.com/)，以**全域管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="b3579-333">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="b3579-334">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="b3579-334">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="b3579-335">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="b3579-335">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="b3579-336">按一下瀏覽功能表中的 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="b3579-336">click **Enterprise applications** in the navigation menu.</span></span>

5.  <span data-ttu-id="b3579-337">按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="b3579-337">click **All applications**.</span></span>

6.  <span data-ttu-id="b3579-338">搜尋您感興趣的應用程式，或依應用程式顯示名稱或應用程式識別碼搜尋使用者嘗試登入的應用程式。</span><span class="sxs-lookup"><span data-stu-id="b3579-338">Search for the application you are interested in, or the user is attempting to sign in to by application display name or application id.</span></span>

     >[!NOTE]
     ><span data-ttu-id="b3579-339">如果您看不到正在尋找的應用程式，請按一下 [篩選] 按鈕，然後將清單範圍展開至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="b3579-339">If you don’t see the application you are looking for, click the **Filter** button and expand the scope of the list to **All applications**.</span></span> <span data-ttu-id="b3579-340">如果您想要看到更多的資料行，請按一下 [資料行] 按鈕為應用程式新增其他詳細資料。</span><span class="sxs-lookup"><span data-stu-id="b3579-340">If you want to see more columns, click the **Columns** button to add additional details for your applications.</span></span>
     >
     >

7.  <span data-ttu-id="b3579-341">按一下 [條件式存取] 瀏覽項目。</span><span class="sxs-lookup"><span data-stu-id="b3579-341">click the **Conditional access** navigation item.</span></span>

8.  <span data-ttu-id="b3579-342">按一下您想要檢查的原則。</span><span class="sxs-lookup"><span data-stu-id="b3579-342">click the policy you are interested in inspecting.</span></span>

9.  <span data-ttu-id="b3579-343">檢查有無特定的條件、指派，或其他可能會封鎖使用者存取的設定。</span><span class="sxs-lookup"><span data-stu-id="b3579-343">Review that there are no specific conditions, assignments, or other settings which may be blocking user access.</span></span>

     >[!NOTE]
     ><span data-ttu-id="b3579-344">您可能會想要暫時停用此原則，以確保不會影響登入。</span><span class="sxs-lookup"><span data-stu-id="b3579-344">You may wish to temporarily disable this policy to ensure it is not affecting sign ins.</span></span> <span data-ttu-id="b3579-345">若要這麼做，請設定 [啟用原則] 切換至 [否]，然後按一下 [儲存] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b3579-345">To do this, set the **Enable policy** toggle to **No** and click the **Save** button.</span></span>
     >
     >

### <a name="disable-a-specific-conditional-access-policy"></a><span data-ttu-id="b3579-346">停用特定的條件式存取原則</span><span class="sxs-lookup"><span data-stu-id="b3579-346">Disable a specific conditional access policy</span></span>

<span data-ttu-id="b3579-347">若要檢查或驗證單一條件式存取原則︰</span><span class="sxs-lookup"><span data-stu-id="b3579-347">To check or validate a single conditional access policy:</span></span>

1.  <span data-ttu-id="b3579-348">開啟 [**Azure 入口網站**](https://portal.azure.com/)，以**全域管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="b3579-348">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="b3579-349">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="b3579-349">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="b3579-350">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="b3579-350">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="b3579-351">按一下瀏覽功能表中的 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="b3579-351">click **Enterprise applications** in the navigation menu.</span></span>

5.  <span data-ttu-id="b3579-352">按一下 [條件式存取] 瀏覽項目。</span><span class="sxs-lookup"><span data-stu-id="b3579-352">click the **Conditional access** navigation item.</span></span>

6.  <span data-ttu-id="b3579-353">按一下您想要檢查的原則。</span><span class="sxs-lookup"><span data-stu-id="b3579-353">click the policy you are interested in inspecting.</span></span>

7.  <span data-ttu-id="b3579-354">設定 [啟用原則] 切換至 [否] 以停用原則，然後按一下 [儲存] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b3579-354">Disable the policy by setting the **Enable policy** toggle to **No** and click the **Save** button.</span></span>

## <a name="problems-with-application-consent"></a><span data-ttu-id="b3579-355">應用程式同意的問題</span><span class="sxs-lookup"><span data-stu-id="b3579-355">Problems with application consent</span></span>

<span data-ttu-id="b3579-356">由於未進行適當的權限同意作業，因此會阻止應用程式存取。</span><span class="sxs-lookup"><span data-stu-id="b3579-356">Application access can be blocked because the proper permissions consent operation has not occurred.</span></span> <span data-ttu-id="b3579-357">以下提供一些方式，可讓您疑難排解並解決應用程式同意問題：</span><span class="sxs-lookup"><span data-stu-id="b3579-357">Below are some ways you can troubleshoot and solve application consent issues:</span></span>

-   [<span data-ttu-id="b3579-358">執行使用者層級同意作業</span><span class="sxs-lookup"><span data-stu-id="b3579-358">Perform a user-level consent operation</span></span>](#perform-a-user-level-consent-operation)

-   [<span data-ttu-id="b3579-359">為任何應用程式執行系統管理員層級同意作業</span><span class="sxs-lookup"><span data-stu-id="b3579-359">Perform administrator-level consent operation for any application</span></span>](#perform-administrator-level-consent-operation-for-any-application)

-   [<span data-ttu-id="b3579-360">為單一租用戶應用程式執行系統管理員層級同意</span><span class="sxs-lookup"><span data-stu-id="b3579-360">Perform administrator-level consent for a single-tenant application</span></span>](#perform-administrator-level-consent-for-a-single-tenant-application)

-   [<span data-ttu-id="b3579-361">為多租用戶應用程式執行系統管理員層級同意</span><span class="sxs-lookup"><span data-stu-id="b3579-361">Perform administrator-level consent for a multi-tenant application</span></span>](#perform-administrator-level-consent-for-a-multi-tenant-application)

### <a name="perform-a-user-level-consent-operation"></a><span data-ttu-id="b3579-362">執行使用者層級同意作業</span><span class="sxs-lookup"><span data-stu-id="b3579-362">Perform a user-level consent operation</span></span>

-   <span data-ttu-id="b3579-363">對於任何已啟用 Open ID Connect 且要求權限的應用程式，若瀏覽至應用程式的登入畫面，會為登入的使用者執行對該應用程式的使用者層級同意。</span><span class="sxs-lookup"><span data-stu-id="b3579-363">For any Open ID Connect-enabled application that requests permissions, navigating to the application’s sign in screen performs a user level consent to the application for the signed-in user.</span></span>

-   <span data-ttu-id="b3579-364">如果您想要以程式設計方式執行這項作業，請參閱[要求個別使用者同意](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#requesting-individual-user-consent)。</span><span class="sxs-lookup"><span data-stu-id="b3579-364">If you wish to do this programmatically, see [Requesting individual user consent](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#requesting-individual-user-consent).</span></span>

### <a name="perform-administrator-level-consent-operation-for-any-application"></a><span data-ttu-id="b3579-365">為任何應用程式執行系統管理員層級同意作業</span><span class="sxs-lookup"><span data-stu-id="b3579-365">Perform administrator-level consent operation for any application</span></span>

-   <span data-ttu-id="b3579-366">**僅適用於使用 V1 應用程式模型開發的應用程式**：您可以將 “**?prompt=admin\_consent**” 新增至應用程式登入 URL 的結尾，來強制進行此系統管理員層級同意。</span><span class="sxs-lookup"><span data-stu-id="b3579-366">For **only applications developed using the V1 application model**, you can force this administrator level consent to occur by adding “**?prompt=admin\_consent**” to the end of an application’s sign in URL.</span></span>

-   <span data-ttu-id="b3579-367">**適用於任何使用 V2 應用程式模型開發的應用程式**：您可以依照[使用系統管理員同意端點](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint)中**向目錄管理員要求權限**一節的指示，強制進行此系統管理員層級同意。</span><span class="sxs-lookup"><span data-stu-id="b3579-367">For **any application developed using the V2 application model**, you can enforce this administrator-level consent to occur by following the instructions under the **Request the permissions from a directory admin** section of [Using the admin consent endpoint](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span></span>

### <a name="perform-administrator-level-consent-for-a-single-tenant-application"></a><span data-ttu-id="b3579-368">為單一租用戶應用程式執行系統管理員層級同意</span><span class="sxs-lookup"><span data-stu-id="b3579-368">Perform administrator-level consent for a single-tenant application</span></span>

-   <span data-ttu-id="b3579-369">適用於要求權限的**單一租用戶應用程式** (例如您正在開發或您在組織中擁有的應用程式)：您可以代表所有的使用者執行**系統管理員層級同意**作業，做法是以全域管理員身分登入，然後按一下 [應用程式登錄] -&gt; [所有應用程式] -&gt; [選取應用程式] -&gt; [必要權限] 刀鋒視窗頂端的 [授與權限] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b3579-369">For **single-tenant applications** that request permissions (like those you are developing or own in your organization), you can perform an **administrative-level consent** operation on behalf of all users by signing in as a Global Administrator and clicking on the **Grant permissions** button at the top of the **Application Registry -&gt; All Applications -&gt; Select an App -&gt; Required Permissions** blade.</span></span>

-   <span data-ttu-id="b3579-370">**適用於任何使用 V1 或 V2 應用程式模型開發的應用程式**：您可以依照[使用系統管理員同意端點](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint)中**向目錄管理員要求權限**一節的指示，強制進行此系統管理員層級同意。</span><span class="sxs-lookup"><span data-stu-id="b3579-370">For **any application developed using the V1 or V2 application model**, you can enforce this administrator-level consent to occur by following the instructions under the **Request the permissions from a directory admin** section of [Using the admin consent endpoint](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span></span>

### <a name="perform-administrator-level-consent-for-a-multi-tenant-application"></a><span data-ttu-id="b3579-371">為多租用戶應用程式執行系統管理員層級同意</span><span class="sxs-lookup"><span data-stu-id="b3579-371">Perform administrator-level consent for a multi-tenant application</span></span>

-   <span data-ttu-id="b3579-372">適用於要求權限的**多租用戶應用程式** (例如第三方或 Microsoft 開發的應用程式)：您可以執行**系統管理員層級同意**作業。</span><span class="sxs-lookup"><span data-stu-id="b3579-372">For **multi-tenant applications** that request permissions (like an application a third party, or Microsoft, develops), you can perform an **administrative-level consent** operation.</span></span> <span data-ttu-id="b3579-373">以全域管理員身分登入，然後按一下 [企業應用程式] -&gt; [所有應用程式] -&gt; [選取應用程式] -&gt; [權限] 刀鋒視窗 (即將推出) 下方的 [授與權限] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b3579-373">Sign in as a Global Administrator and clicking on the **Grant permissions** button under the **Enterprise Applications -&gt; All Applications -&gt; Select an App -&gt; Permissions** blade (available soon).</span></span>

-   <span data-ttu-id="b3579-374">您也可以依照[使用系統管理員同意端點](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint)中**向目錄管理員要求權限**一節的指示，強制進行系統管理員層級同意。</span><span class="sxs-lookup"><span data-stu-id="b3579-374">You can also enforce this administrator-level consent to occur by following the instructions under the **Request the permissions from a directory admin** section of [Using the admin consent endpoint](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b3579-375">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b3579-375">Next steps</span></span>
[<span data-ttu-id="b3579-376">使用系統管理員同意端點</span><span class="sxs-lookup"><span data-stu-id="b3579-376">Using the admin consent endpoint</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint)

