---
title: "Azure Active Directory 入口網站中的登入活動報告錯誤碼 | Microsoft Docs"
description: "登入活動報告錯誤碼參考。"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 4b18127b-d1d0-4bdc-8f9c-6a4c991c5f75
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 2a1b7b87df2cd8fa2e98f217480b46f5f6334297
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/29/2017
---
# <a name="sign-in-activity-report-error-codes-in-the-azure-active-directory-portal"></a><span data-ttu-id="0c7ec-103">Azure Active Directory 入口網站中的登入活動報告錯誤碼</span><span class="sxs-lookup"><span data-stu-id="0c7ec-103">Sign-in activity report error codes in the Azure Active Directory portal</span></span>

<span data-ttu-id="0c7ec-104">利用使用者登入報告所提供的資訊，您可以找到下列問題的解答︰</span><span class="sxs-lookup"><span data-stu-id="0c7ec-104">With the information provided by the user sign-ins report, you find answers to questions such as:</span></span>

- <span data-ttu-id="0c7ec-105">誰已使用 Azure Active Directory 登入？</span><span class="sxs-lookup"><span data-stu-id="0c7ec-105">Who has signed-in using Azure Active Directory?</span></span>
- <span data-ttu-id="0c7ec-106">已登入哪些應用程式？</span><span class="sxs-lookup"><span data-stu-id="0c7ec-106">Which apps were signed into?</span></span>
- <span data-ttu-id="0c7ec-107">哪些登入失敗，原因為何？</span><span class="sxs-lookup"><span data-stu-id="0c7ec-107">Which sign-ins were failures and if so why?</span></span>

<span data-ttu-id="0c7ec-108">本主題列出錯誤碼及相關說明。</span><span class="sxs-lookup"><span data-stu-id="0c7ec-108">This topic lists the error codes and the related descriptions.</span></span> 

## <a name="how-can-i-display-failed-sign-ins"></a><span data-ttu-id="0c7ec-109">如何顯示失敗的登入？</span><span class="sxs-lookup"><span data-stu-id="0c7ec-109">How can I display failed sign-ins?</span></span> 

<span data-ttu-id="0c7ec-110">所有登入活動資料的第一個進入點是 **Azure Active** 的 [活動] 區段中的[登 入](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/SignIns)。</span><span class="sxs-lookup"><span data-stu-id="0c7ec-110">Your first entry point to all sign-in activities data is **[Sign-ins](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/SignIns)** in the **Activity** section of **Azure Active**.</span></span>


<span data-ttu-id="0c7ec-111">![登入活動](./media/active-directory-reporting-activity-sign-ins-errors/61.png "登入活動")</span><span class="sxs-lookup"><span data-stu-id="0c7ec-111">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins-errors/61.png "Sign-in activity")</span></span>


<span data-ttu-id="0c7ec-112">在登入報告中，您可以選取 [失敗] 作為 [登入狀態]，以顯示所有失敗的登入。</span><span class="sxs-lookup"><span data-stu-id="0c7ec-112">In your sign-ins report, you can display all failed sign-ins by selecting **Failure** as **Sign-in status**.</span></span>


<span data-ttu-id="0c7ec-113">![登入活動](./media/active-directory-reporting-activity-sign-ins-errors/06.png "登入活動")</span><span class="sxs-lookup"><span data-stu-id="0c7ec-113">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins-errors/06.png "Sign-in activity")</span></span>

<span data-ttu-id="0c7ec-114">按一下所顯示清單中的項目，會開啟 [活動詳細資料：登入] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="0c7ec-114">Clicking an item in the displayed list, opens the **Activity Details: Sign-ins** blade.</span></span> <span data-ttu-id="0c7ec-115">此檢視提供 Azure Active Directory 追蹤的所有登入詳細資料，包括 [登入錯誤碼] 和 [失敗原因]。</span><span class="sxs-lookup"><span data-stu-id="0c7ec-115">This view provides you with all the details that Azure Active Directory tracks about sign-ins, including the **sign-in error code** and a **failure reason**.</span></span>

<span data-ttu-id="0c7ec-116">![登入活動](./media/active-directory-reporting-activity-sign-ins-errors/05.png "登入活動")</span><span class="sxs-lookup"><span data-stu-id="0c7ec-116">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins-errors/05.png "Sign-in activity")</span></span>


<span data-ttu-id="0c7ec-117">除了使用 Azure 入口網站來存取登入資料以外，您也可以使用[報告 API](active-directory-reporting-api-getting-started-azure-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="0c7ec-117">As an alternative to using the Azure portal to access the sign-ins data, you can also use the [reporting API](active-directory-reporting-api-getting-started-azure-portal.md).</span></span>


<span data-ttu-id="0c7ec-118">下一節提供所有可能錯誤的完整概觀以及相關的說明。</span><span class="sxs-lookup"><span data-stu-id="0c7ec-118">The following section provides you with a complete overview of all possible errors and the related descriptions.</span></span> 

## <a name="error-codes"></a><span data-ttu-id="0c7ec-119">錯誤碼</span><span class="sxs-lookup"><span data-stu-id="0c7ec-119">Error codes</span></span>

| <span data-ttu-id="0c7ec-120">錯誤</span><span class="sxs-lookup"><span data-stu-id="0c7ec-120">Error</span></span>| <span data-ttu-id="0c7ec-121">說明</span><span class="sxs-lookup"><span data-stu-id="0c7ec-121">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0c7ec-122">50001</span><span class="sxs-lookup"><span data-stu-id="0c7ec-122">50001</span></span>| <span data-ttu-id="0c7ec-123">在名為 Y 的租用戶中找不到名為 X 的服務主體。如果租用戶的系統管理員尚未安裝此應用程式，也可能會發生此錯誤。</span><span class="sxs-lookup"><span data-stu-id="0c7ec-123">The service principal named X was not found in the tenant named Y. This can happen if the application has not been installed by the administrator of the tenant.</span></span> <span data-ttu-id="0c7ec-124">或在目錄中找不到資源主體或為無效</span><span class="sxs-lookup"><span data-stu-id="0c7ec-124">Or Resource principal was not found in the directory or is invalid</span></span>|
| <span data-ttu-id="0c7ec-125">50008</span><span class="sxs-lookup"><span data-stu-id="0c7ec-125">50008</span></span>| <span data-ttu-id="0c7ec-126">權杖中的 SAML 判斷提示遺漏或設定不正確。</span><span class="sxs-lookup"><span data-stu-id="0c7ec-126">SAML assertion are missing or misconfigured in the token.</span></span>|
| <span data-ttu-id="0c7ec-127">50011</span><span class="sxs-lookup"><span data-stu-id="0c7ec-127">50011</span></span>| <span data-ttu-id="0c7ec-128">回覆位址遺漏、設定不正確或不符合為應用程式設定的回覆位址。</span><span class="sxs-lookup"><span data-stu-id="0c7ec-128">The reply address is missing, misconfigured or does not match reply addresses configured for the application.</span></span>|
| <span data-ttu-id="0c7ec-129">50053</span><span class="sxs-lookup"><span data-stu-id="0c7ec-129">50053</span></span>| <span data-ttu-id="0c7ec-130">帳戶遭到鎖定，因為使用者嘗試使用不正確的使用者識別碼或密碼登入太多次。</span><span class="sxs-lookup"><span data-stu-id="0c7ec-130">Account is locked because user tried to sign in too many times with an incorrect user ID or password.</span></span>|
| <span data-ttu-id="0c7ec-131">50054</span><span class="sxs-lookup"><span data-stu-id="0c7ec-131">50054</span></span>| <span data-ttu-id="0c7ec-132">使用舊密碼進行驗證。</span><span class="sxs-lookup"><span data-stu-id="0c7ec-132">Old password is used for authentication.</span></span>|
| <span data-ttu-id="0c7ec-133">50055</span><span class="sxs-lookup"><span data-stu-id="0c7ec-133">50055</span></span>| <span data-ttu-id="0c7ec-134">無效的密碼，或輸入的密碼過期。</span><span class="sxs-lookup"><span data-stu-id="0c7ec-134">Invalid password, entered expired password.</span></span>|
| <span data-ttu-id="0c7ec-135">50057</span><span class="sxs-lookup"><span data-stu-id="0c7ec-135">50057</span></span>| <span data-ttu-id="0c7ec-136">使用者帳戶已停用。</span><span class="sxs-lookup"><span data-stu-id="0c7ec-136">User account is disabled.</span></span>|
| <span data-ttu-id="0c7ec-137">50058</span><span class="sxs-lookup"><span data-stu-id="0c7ec-137">50058</span></span>| <span data-ttu-id="0c7ec-138">在所提供的認證中找不到使用者的身分識別相關資訊，或在租用戶中找不到使用者，或已傳送無訊息的登入要求，但沒有使用者登入或服務無法驗證使用者。</span><span class="sxs-lookup"><span data-stu-id="0c7ec-138">No information about user's identity is found among provided credentials or User was not found in tenant or A silent sign-in request was sent but no user is signed in or Service was unable to authenticate the user.</span></span>|
| <span data-ttu-id="0c7ec-139">50074</span><span class="sxs-lookup"><span data-stu-id="0c7ec-139">50074</span></span>| <span data-ttu-id="0c7ec-140">強式驗證 (第二個因素) 是必要的</span><span class="sxs-lookup"><span data-stu-id="0c7ec-140">Strong Authentication (second factor) is required</span></span>|
| <span data-ttu-id="0c7ec-141">50079</span><span class="sxs-lookup"><span data-stu-id="0c7ec-141">50079</span></span>| <span data-ttu-id="0c7ec-142">使用者需要註冊第二個因素驗證</span><span class="sxs-lookup"><span data-stu-id="0c7ec-142">User needs to enroll for second factor authentication</span></span>|
| <span data-ttu-id="0c7ec-143">50126</span><span class="sxs-lookup"><span data-stu-id="0c7ec-143">50126</span></span>| <span data-ttu-id="0c7ec-144">使用者名稱、密碼無效，或內部部署使用者名稱或密碼無效。</span><span class="sxs-lookup"><span data-stu-id="0c7ec-144">Invalid username or password or Invalid on-premise username or password.</span></span>|
| <span data-ttu-id="0c7ec-145">50131</span><span class="sxs-lookup"><span data-stu-id="0c7ec-145">50131</span></span>| <span data-ttu-id="0c7ec-146">使用於各種條件式存取錯誤。</span><span class="sxs-lookup"><span data-stu-id="0c7ec-146">Used in various conditional access errors.</span></span> <span data-ttu-id="0c7ec-147">例如，不正確的 Windows 裝置狀態，要求因為可疑的活動、存取原則和安全性原則決策而遭到封鎖。</span><span class="sxs-lookup"><span data-stu-id="0c7ec-147">E.g Bad Windows device state, request blocked due to suspicious activity, access policy and security policy decisions.</span></span>|
| <span data-ttu-id="0c7ec-148">50133</span><span class="sxs-lookup"><span data-stu-id="0c7ec-148">50133</span></span>| <span data-ttu-id="0c7ec-149">工作階段因為到期或近期密碼變更而無效。</span><span class="sxs-lookup"><span data-stu-id="0c7ec-149">Session is invalid due to expiration or recent password change.</span></span>|
| <span data-ttu-id="0c7ec-150">50144</span><span class="sxs-lookup"><span data-stu-id="0c7ec-150">50144</span></span>| <span data-ttu-id="0c7ec-151">使用者的 Active Directory 密碼已到期。</span><span class="sxs-lookup"><span data-stu-id="0c7ec-151">User's Active Directory password has expired.</span></span>|
| <span data-ttu-id="0c7ec-152">65001</span><span class="sxs-lookup"><span data-stu-id="0c7ec-152">65001</span></span>| <span data-ttu-id="0c7ec-153">應用程式 X 沒有存取應用程式 Y 的權限，或已撤銷此權限。</span><span class="sxs-lookup"><span data-stu-id="0c7ec-153">Application X doesn't have permission to access application Y or the permission has been revoked.</span></span> <span data-ttu-id="0c7ec-154">或者，使用者或系統管理員尚未同意使用識別碼為 X 的應用程式。針對此使用者和資源傳送互動式授權要求。</span><span class="sxs-lookup"><span data-stu-id="0c7ec-154">Or The user or administrator has not consented to use the application with ID X. Send an interactive authorization request for this user and resource.</span></span> <span data-ttu-id="0c7ec-155">或者，使用者或系統管理員尚未同意使用識別碼為 X 的應用程式。將授權要求傳送給租用戶管理員，以代表應用程式 Y 對資源 Z 採取行動。</span><span class="sxs-lookup"><span data-stu-id="0c7ec-155">Or The user or administrator has not consented to use the application with ID X. Send an authorization request to your tenant admin to act on behalf of the App : Y for Resource : Z.</span></span>|
| <span data-ttu-id="0c7ec-156">65005</span><span class="sxs-lookup"><span data-stu-id="0c7ec-156">65005</span></span>| <span data-ttu-id="0c7ec-157">應用程式所需資源存取清單不包含資源可探索的應用程式，或用戶端應用程式已要求存取未在其所需資源存取清單中指定的資源，或 Graph 服務傳回不正確的要求或找不到資源。</span><span class="sxs-lookup"><span data-stu-id="0c7ec-157">The application required resource access list does not contain applications discoverable by the resource or The client application has requested access to resource which was not specified in its required resource access list or Graph service returned bad request or resource not found.</span></span>|
| <span data-ttu-id="0c7ec-158">70001</span><span class="sxs-lookup"><span data-stu-id="0c7ec-158">70001</span></span>| <span data-ttu-id="0c7ec-159">在名為 Y 的租用戶中找不到名為 X 的應用程式。如果租用戶的系統管理員尚未安裝此應用程式或租用戶中的任何使用者尚未同意使用此應用程式，也可能會發生此錯誤。</span><span class="sxs-lookup"><span data-stu-id="0c7ec-159">The application named X was not found in the tenant named Y. This can happen if the application has not been installed by the administrator of the tenant or consented to by any user in the tenant.</span></span> <span data-ttu-id="0c7ec-160">您可能會將驗證要求傳送至錯誤的租用戶。</span><span class="sxs-lookup"><span data-stu-id="0c7ec-160">You might have sent your authentication request to the wrong tenant.</span></span>|
| <span data-ttu-id="0c7ec-161">80001</span><span class="sxs-lookup"><span data-stu-id="0c7ec-161">80001</span></span>| <span data-ttu-id="0c7ec-162">沒有可用的驗證代理程式。</span><span class="sxs-lookup"><span data-stu-id="0c7ec-162">No Authentication Agent available.</span></span>|
| <span data-ttu-id="0c7ec-163">80002</span><span class="sxs-lookup"><span data-stu-id="0c7ec-163">80002</span></span>| <span data-ttu-id="0c7ec-164">驗證代理程式的密碼驗證要求已逾時。</span><span class="sxs-lookup"><span data-stu-id="0c7ec-164">Authentication Agent's password validation request timed out.</span></span>|
| <span data-ttu-id="0c7ec-165">80003</span><span class="sxs-lookup"><span data-stu-id="0c7ec-165">80003</span></span>| <span data-ttu-id="0c7ec-166">驗證代理程式收到的回應無效。</span><span class="sxs-lookup"><span data-stu-id="0c7ec-166">Invalid response received by Authentication Agent.</span></span>|
| <span data-ttu-id="0c7ec-167">80004</span><span class="sxs-lookup"><span data-stu-id="0c7ec-167">80004</span></span>| <span data-ttu-id="0c7ec-168">登入要求中使用的使用者主體名稱 (UPN) 不正確。</span><span class="sxs-lookup"><span data-stu-id="0c7ec-168">Incorrect User Principal Name (UPN) used in sign-in request.</span></span>|
| <span data-ttu-id="0c7ec-169">80005</span><span class="sxs-lookup"><span data-stu-id="0c7ec-169">80005</span></span>| <span data-ttu-id="0c7ec-170">驗證代理程式：發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="0c7ec-170">Authentication Agent: Error occurred.</span></span>|
| <span data-ttu-id="0c7ec-171">80007</span><span class="sxs-lookup"><span data-stu-id="0c7ec-171">80007</span></span>| <span data-ttu-id="0c7ec-172">驗證代理程式無法連線至 Active Directory。</span><span class="sxs-lookup"><span data-stu-id="0c7ec-172">Authentication Agent unable to connect to Active Directory.</span></span>|
| <span data-ttu-id="0c7ec-173">80010</span><span class="sxs-lookup"><span data-stu-id="0c7ec-173">80010</span></span>| <span data-ttu-id="0c7ec-174">驗證代理程式無法連線將密碼解密。</span><span class="sxs-lookup"><span data-stu-id="0c7ec-174">Authentication Agent unable to decrypt password.</span></span>|
| <span data-ttu-id="0c7ec-175">81001</span><span class="sxs-lookup"><span data-stu-id="0c7ec-175">81001</span></span>| <span data-ttu-id="0c7ec-176">使用者的 Kerberos 票證太大。</span><span class="sxs-lookup"><span data-stu-id="0c7ec-176">User's Kerberos ticket is too large.</span></span>|
| <span data-ttu-id="0c7ec-177">81002</span><span class="sxs-lookup"><span data-stu-id="0c7ec-177">81002</span></span>| <span data-ttu-id="0c7ec-178">無法驗證使用者的 Kerberos 票證。</span><span class="sxs-lookup"><span data-stu-id="0c7ec-178">Unable to validate user's Kerberos ticket.</span></span>|
| <span data-ttu-id="0c7ec-179">81003</span><span class="sxs-lookup"><span data-stu-id="0c7ec-179">81003</span></span>| <span data-ttu-id="0c7ec-180">無法驗證使用者的 Kerberos 票證。</span><span class="sxs-lookup"><span data-stu-id="0c7ec-180">Unable to validate user's Kerberos ticket.</span></span>|
| <span data-ttu-id="0c7ec-181">81004</span><span class="sxs-lookup"><span data-stu-id="0c7ec-181">81004</span></span>| <span data-ttu-id="0c7ec-182">Kerberos 驗證嘗試失敗。</span><span class="sxs-lookup"><span data-stu-id="0c7ec-182">Kerberos authentication attempt failed.</span></span>|
| <span data-ttu-id="0c7ec-183">81008</span><span class="sxs-lookup"><span data-stu-id="0c7ec-183">81008</span></span>| <span data-ttu-id="0c7ec-184">無法驗證使用者的 Kerberos 票證。</span><span class="sxs-lookup"><span data-stu-id="0c7ec-184">Unable to validate user's Kerberos ticket.</span></span>|
| <span data-ttu-id="0c7ec-185">81009</span><span class="sxs-lookup"><span data-stu-id="0c7ec-185">81009</span></span>| <span data-ttu-id="0c7ec-186">無法驗證使用者的 Kerberos 票證。</span><span class="sxs-lookup"><span data-stu-id="0c7ec-186">Unable to validate user's Kerberos ticket.</span></span>|
| <span data-ttu-id="0c7ec-187">81010</span><span class="sxs-lookup"><span data-stu-id="0c7ec-187">81010</span></span>| <span data-ttu-id="0c7ec-188">無縫式 SSO 失敗，因為使用者的 Kerberos 票證已過期或無效。</span><span class="sxs-lookup"><span data-stu-id="0c7ec-188">Seamless SSO failed because the user's Kerberos ticket has expired or is invalid.</span></span>|
| <span data-ttu-id="0c7ec-189">81011</span><span class="sxs-lookup"><span data-stu-id="0c7ec-189">81011</span></span>| <span data-ttu-id="0c7ec-190">找不到以使用者的 Kerberos 票證中資訊為基礎的使用者物件。</span><span class="sxs-lookup"><span data-stu-id="0c7ec-190">Unable to find user object based on information in the user's Kerberos ticket.</span></span>|
| <span data-ttu-id="0c7ec-191">81012</span><span class="sxs-lookup"><span data-stu-id="0c7ec-191">81012</span></span>| <span data-ttu-id="0c7ec-192">嘗試登入 Azure AD 的使用者與登入裝置的使用者不同。</span><span class="sxs-lookup"><span data-stu-id="0c7ec-192">The user trying to sign in to Azure AD is different from the user signed into the device.</span></span>|
| <span data-ttu-id="0c7ec-193">81013</span><span class="sxs-lookup"><span data-stu-id="0c7ec-193">81013</span></span>| <span data-ttu-id="0c7ec-194">找不到以使用者的 Kerberos 票證中資訊為基礎的使用者物件。</span><span class="sxs-lookup"><span data-stu-id="0c7ec-194">Unable to find user object based on information in the user's Kerberos ticket.</span></span>|
| <span data-ttu-id="0c7ec-195">90014</span><span class="sxs-lookup"><span data-stu-id="0c7ec-195">90014</span></span>| <span data-ttu-id="0c7ec-196">當認證中未出現預期的欄位時，使用於各種情況。</span><span class="sxs-lookup"><span data-stu-id="0c7ec-196">Used in various cases when an expected field is not present in the credential.</span></span>|
| <span data-ttu-id="0c7ec-197">90093</span><span class="sxs-lookup"><span data-stu-id="0c7ec-197">90093</span></span>| <span data-ttu-id="0c7ec-198">傳回的圖表包含要求的禁止錯誤碼。</span><span class="sxs-lookup"><span data-stu-id="0c7ec-198">Graph returned with forbidden error code for the request.</span></span>|



## <a name="next-steps"></a><span data-ttu-id="0c7ec-199">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0c7ec-199">Next steps</span></span>

<span data-ttu-id="0c7ec-200">如需詳細資訊，請參閱 [Azure Active Directory 入口網站中的登入活動報告](active-directory-reporting-activity-sign-ins.md)。</span><span class="sxs-lookup"><span data-stu-id="0c7ec-200">For more details, see the [Sign-in activity reports in the Azure Active Directory portal](active-directory-reporting-activity-sign-ins.md).</span></span>

