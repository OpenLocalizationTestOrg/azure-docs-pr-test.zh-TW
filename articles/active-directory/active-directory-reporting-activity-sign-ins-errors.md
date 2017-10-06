---
title: "aaaSign 入活動報表中的錯誤碼 hello Azure Active Directory 入口網站 |Microsoft 文件"
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
ms.openlocfilehash: a0ca5b706bfeb0c7ce669712468a083a394712b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-activity-report-error-codes-in-hello-azure-active-directory-portal"></a><span data-ttu-id="9c297-103">登入活動報表中的錯誤碼 hello Azure Active Directory 入口網站</span><span class="sxs-lookup"><span data-stu-id="9c297-103">Sign-in activity report error codes in hello Azure Active Directory portal</span></span>

<span data-ttu-id="9c297-104">Hello hello 使用者登入報表所提供的資訊，您可以找到解答 tooquestions，例如：</span><span class="sxs-lookup"><span data-stu-id="9c297-104">With hello information provided by hello user sign-ins report, you find answers tooquestions such as:</span></span>

- <span data-ttu-id="9c297-105">誰已使用 Azure Active Directory 登入？</span><span class="sxs-lookup"><span data-stu-id="9c297-105">Who has signed-in using Azure Active Directory?</span></span>
- <span data-ttu-id="9c297-106">已登入哪些應用程式？</span><span class="sxs-lookup"><span data-stu-id="9c297-106">Which apps were signed into?</span></span>
- <span data-ttu-id="9c297-107">哪些登入失敗，原因為何？</span><span class="sxs-lookup"><span data-stu-id="9c297-107">Which sign-ins were failures and if so why?</span></span>

<span data-ttu-id="9c297-108">此主題列出 hello 錯誤代碼和 hello 相關的說明。</span><span class="sxs-lookup"><span data-stu-id="9c297-108">This topic lists hello error codes and hello related descriptions.</span></span> 

## <a name="how-can-i-display-failed-sign-ins"></a><span data-ttu-id="9c297-109">如何顯示失敗的登入？</span><span class="sxs-lookup"><span data-stu-id="9c297-109">How can I display failed sign-ins?</span></span> 

<span data-ttu-id="9c297-110">第一個項目點 tooall 登入活動資料**[登入](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/SignIns)**在 hello**活動**區段**Azure Active**。</span><span class="sxs-lookup"><span data-stu-id="9c297-110">Your first entry point tooall sign-in activities data is **[Sign-ins](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/SignIns)** in hello **Activity** section of **Azure Active**.</span></span>


<span data-ttu-id="9c297-111">![登入活動](./media/active-directory-reporting-activity-sign-ins-errors/61.png "登入活動")</span><span class="sxs-lookup"><span data-stu-id="9c297-111">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins-errors/61.png "Sign-in activity")</span></span>


<span data-ttu-id="9c297-112">在登入報告中，您可以選取 [失敗] 作為 [登入狀態]，以顯示所有失敗的登入。</span><span class="sxs-lookup"><span data-stu-id="9c297-112">In your sign-ins report, you can display all failed sign-ins by selecting **Failure** as **Sign-in status**.</span></span>


<span data-ttu-id="9c297-113">![登入活動](./media/active-directory-reporting-activity-sign-ins-errors/06.png "登入活動")</span><span class="sxs-lookup"><span data-stu-id="9c297-113">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins-errors/06.png "Sign-in activity")</span></span>

<span data-ttu-id="9c297-114">按一下即可顯示 hello 清單中的項目，開啟 hello**活動詳細資料： 登入**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="9c297-114">Clicking an item in hello displayed list, opens hello **Activity Details: Sign-ins** blade.</span></span> <span data-ttu-id="9c297-115">這個檢視可提供您所有 Azure Active Directory 追蹤有關登入，包括 hello hello 詳細資料**登入錯誤碼**和**失敗原因**。</span><span class="sxs-lookup"><span data-stu-id="9c297-115">This view provides you with all hello details that Azure Active Directory tracks about sign-ins, including hello **sign-in error code** and a **failure reason**.</span></span>

<span data-ttu-id="9c297-116">![登入活動](./media/active-directory-reporting-activity-sign-ins-errors/05.png "登入活動")</span><span class="sxs-lookup"><span data-stu-id="9c297-116">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins-errors/05.png "Sign-in activity")</span></span>


<span data-ttu-id="9c297-117">做為替代 toousing hello Azure 入口網站 tooaccess hello 登入資料，您也可以使用 hello[報告 API](active-directory-reporting-api-getting-started-azure-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="9c297-117">As an alternative toousing hello Azure portal tooaccess hello sign-ins data, you can also use hello [reporting API](active-directory-reporting-api-getting-started-azure-portal.md).</span></span>


<span data-ttu-id="9c297-118">hello 下列章節提供您的所有可能的錯誤和 hello 的完整概觀與相關說明。</span><span class="sxs-lookup"><span data-stu-id="9c297-118">hello following section provides you with a complete overview of all possible errors and hello related descriptions.</span></span> 

## <a name="error-codes"></a><span data-ttu-id="9c297-119">錯誤碼</span><span class="sxs-lookup"><span data-stu-id="9c297-119">Error codes</span></span>

| <span data-ttu-id="9c297-120">錯誤</span><span class="sxs-lookup"><span data-stu-id="9c297-120">Error</span></span>| <span data-ttu-id="9c297-121">說明</span><span class="sxs-lookup"><span data-stu-id="9c297-121">Description</span></span> |
| --- | --- |
| <span data-ttu-id="9c297-122">50001</span><span class="sxs-lookup"><span data-stu-id="9c297-122">50001</span></span>| <span data-ttu-id="9c297-123">名為 Y 的 hello 租用戶中找不到名為 X hello 服務主體。這種情況 hello 應用程式尚未安裝的 hello hello 租用戶系統管理員。</span><span class="sxs-lookup"><span data-stu-id="9c297-123">hello service principal named X was not found in hello tenant named Y. This can happen if hello application has not been installed by hello administrator of hello tenant.</span></span> <span data-ttu-id="9c297-124">或資源主體 hello 目錄中找不到或無效</span><span class="sxs-lookup"><span data-stu-id="9c297-124">Or Resource principal was not found in hello directory or is invalid</span></span>|
| <span data-ttu-id="9c297-125">50008</span><span class="sxs-lookup"><span data-stu-id="9c297-125">50008</span></span>| <span data-ttu-id="9c297-126">SAML 判斷提示已遺失或 hello 權杖中的設定不正確。</span><span class="sxs-lookup"><span data-stu-id="9c297-126">SAML assertion are missing or misconfigured in hello token.</span></span>|
| <span data-ttu-id="9c297-127">50011</span><span class="sxs-lookup"><span data-stu-id="9c297-127">50011</span></span>| <span data-ttu-id="9c297-128">hello 回覆地址遺漏、 設定不正確或不符合設定的 hello 應用程式的回覆位址。</span><span class="sxs-lookup"><span data-stu-id="9c297-128">hello reply address is missing, misconfigured or does not match reply addresses configured for hello application.</span></span>|
| <span data-ttu-id="9c297-129">50053</span><span class="sxs-lookup"><span data-stu-id="9c297-129">50053</span></span>| <span data-ttu-id="9c297-130">帳戶已鎖定，因為嘗試太多次使用不正確的使用者識別碼或密碼中 toosign 的使用者。</span><span class="sxs-lookup"><span data-stu-id="9c297-130">Account is locked because user tried toosign in too many times with an incorrect user ID or password.</span></span>|
| <span data-ttu-id="9c297-131">50054</span><span class="sxs-lookup"><span data-stu-id="9c297-131">50054</span></span>| <span data-ttu-id="9c297-132">使用舊密碼進行驗證。</span><span class="sxs-lookup"><span data-stu-id="9c297-132">Old password is used for authentication.</span></span>|
| <span data-ttu-id="9c297-133">50055</span><span class="sxs-lookup"><span data-stu-id="9c297-133">50055</span></span>| <span data-ttu-id="9c297-134">無效的密碼，或輸入的密碼過期。</span><span class="sxs-lookup"><span data-stu-id="9c297-134">Invalid password, entered expired password.</span></span>|
| <span data-ttu-id="9c297-135">50057</span><span class="sxs-lookup"><span data-stu-id="9c297-135">50057</span></span>| <span data-ttu-id="9c297-136">使用者帳戶已停用。</span><span class="sxs-lookup"><span data-stu-id="9c297-136">User account is disabled.</span></span>|
| <span data-ttu-id="9c297-137">50058</span><span class="sxs-lookup"><span data-stu-id="9c297-137">50058</span></span>| <span data-ttu-id="9c297-138">提供給租用戶中未找到或使用者的認證或無訊息的登入要求已傳送但沒有使用者登入或服務是無法 tooauthenticate hello 使用者之間不找到使用者的身分識別的任何資訊。</span><span class="sxs-lookup"><span data-stu-id="9c297-138">No information about user's identity is found among provided credentials or User was not found in tenant or A silent sign-in request was sent but no user is signed in or Service was unable tooauthenticate hello user.</span></span>|
| <span data-ttu-id="9c297-139">50074</span><span class="sxs-lookup"><span data-stu-id="9c297-139">50074</span></span>| <span data-ttu-id="9c297-140">強式驗證 (第二個因素) 是必要的</span><span class="sxs-lookup"><span data-stu-id="9c297-140">Strong Authentication (second factor) is required</span></span>|
| <span data-ttu-id="9c297-141">50079</span><span class="sxs-lookup"><span data-stu-id="9c297-141">50079</span></span>| <span data-ttu-id="9c297-142">使用者需要 tooenroll 第二因素驗證</span><span class="sxs-lookup"><span data-stu-id="9c297-142">User needs tooenroll for second factor authentication</span></span>|
| <span data-ttu-id="9c297-143">50126</span><span class="sxs-lookup"><span data-stu-id="9c297-143">50126</span></span>| <span data-ttu-id="9c297-144">使用者名稱、密碼無效，或內部部署使用者名稱或密碼無效。</span><span class="sxs-lookup"><span data-stu-id="9c297-144">Invalid username or password or Invalid on-premise username or password.</span></span>|
| <span data-ttu-id="9c297-145">50131</span><span class="sxs-lookup"><span data-stu-id="9c297-145">50131</span></span>| <span data-ttu-id="9c297-146">使用於各種條件式存取錯誤。</span><span class="sxs-lookup"><span data-stu-id="9c297-146">Used in various conditional access errors.</span></span> <span data-ttu-id="9c297-147">例如不正確的 Windows 裝置狀態時，它會要求封鎖，因為 toosuspicious 活動、 存取原則和安全性原則決策。</span><span class="sxs-lookup"><span data-stu-id="9c297-147">E.g Bad Windows device state, request blocked due toosuspicious activity, access policy and security policy decisions.</span></span>|
| <span data-ttu-id="9c297-148">50133</span><span class="sxs-lookup"><span data-stu-id="9c297-148">50133</span></span>| <span data-ttu-id="9c297-149">工作階段到期 tooexpiration 或最近變更的密碼無效。</span><span class="sxs-lookup"><span data-stu-id="9c297-149">Session is invalid due tooexpiration or recent password change.</span></span>|
| <span data-ttu-id="9c297-150">50144</span><span class="sxs-lookup"><span data-stu-id="9c297-150">50144</span></span>| <span data-ttu-id="9c297-151">使用者的 Active Directory 密碼已到期。</span><span class="sxs-lookup"><span data-stu-id="9c297-151">User's Active Directory password has expired.</span></span>|
| <span data-ttu-id="9c297-152">65001</span><span class="sxs-lookup"><span data-stu-id="9c297-152">65001</span></span>| <span data-ttu-id="9c297-153">X 的應用程式沒有權限 tooaccess 應用程式 Y 或 hello 權限已被撤銷。</span><span class="sxs-lookup"><span data-stu-id="9c297-153">Application X doesn't have permission tooaccess application Y or hello permission has been revoked.</span></span> <span data-ttu-id="9c297-154">或 hello 使用者或系統管理員不同意 toouse hello 應用程式識別碼 x 傳送此使用者與資源的互動式授權要求。</span><span class="sxs-lookup"><span data-stu-id="9c297-154">Or hello user or administrator has not consented toouse hello application with ID X. Send an interactive authorization request for this user and resource.</span></span> <span data-ttu-id="9c297-155">Hello 使用者或系統管理員不同意 toouse hello 應用程式識別碼 x 傳送授權要求 tooyour 租用戶系統管理員 tooact 具有代表 hello 應用程式或者： 資源的 Y: Z。</span><span class="sxs-lookup"><span data-stu-id="9c297-155">Or hello user or administrator has not consented toouse hello application with ID X. Send an authorization request tooyour tenant admin tooact on behalf of hello App : Y for Resource : Z.</span></span>|
| <span data-ttu-id="9c297-156">65005</span><span class="sxs-lookup"><span data-stu-id="9c297-156">65005</span></span>| <span data-ttu-id="9c297-157">hello 應用程式所需資源存取清單未包含 hello 資源可探索的應用程式或 hello 用戶端應用程式已要求存取 tooresource 其中並未指定於其所需的資源存取清單或 Graph 服務傳回不正確要求或找不到資源。</span><span class="sxs-lookup"><span data-stu-id="9c297-157">hello application required resource access list does not contain applications discoverable by hello resource or hello client application has requested access tooresource which was not specified in its required resource access list or Graph service returned bad request or resource not found.</span></span>|
| <span data-ttu-id="9c297-158">70001</span><span class="sxs-lookup"><span data-stu-id="9c297-158">70001</span></span>| <span data-ttu-id="9c297-159">名為 Y 的 hello 租用戶中找不到名為 X hello 應用程式。這可以發生如果 hello 應用程式尚未安裝的 hello hello 租用戶或已獲得同意的 tooby 的系統管理員 hello 租用戶中的任何使用者。</span><span class="sxs-lookup"><span data-stu-id="9c297-159">hello application named X was not found in hello tenant named Y. This can happen if hello application has not been installed by hello administrator of hello tenant or consented tooby any user in hello tenant.</span></span> <span data-ttu-id="9c297-160">您可能會傳送驗證要求 toohello 錯誤租用戶。</span><span class="sxs-lookup"><span data-stu-id="9c297-160">You might have sent your authentication request toohello wrong tenant.</span></span>|
| <span data-ttu-id="9c297-161">80001</span><span class="sxs-lookup"><span data-stu-id="9c297-161">80001</span></span>| <span data-ttu-id="9c297-162">沒有可用的驗證代理程式。</span><span class="sxs-lookup"><span data-stu-id="9c297-162">No Authentication Agent available.</span></span>|
| <span data-ttu-id="9c297-163">80002</span><span class="sxs-lookup"><span data-stu-id="9c297-163">80002</span></span>| <span data-ttu-id="9c297-164">驗證代理程式的密碼驗證要求已逾時。</span><span class="sxs-lookup"><span data-stu-id="9c297-164">Authentication Agent's password validation request timed out.</span></span>|
| <span data-ttu-id="9c297-165">80003</span><span class="sxs-lookup"><span data-stu-id="9c297-165">80003</span></span>| <span data-ttu-id="9c297-166">驗證代理程式收到的回應無效。</span><span class="sxs-lookup"><span data-stu-id="9c297-166">Invalid response received by Authentication Agent.</span></span>|
| <span data-ttu-id="9c297-167">80004</span><span class="sxs-lookup"><span data-stu-id="9c297-167">80004</span></span>| <span data-ttu-id="9c297-168">登入要求中使用的使用者主體名稱 (UPN) 不正確。</span><span class="sxs-lookup"><span data-stu-id="9c297-168">Incorrect User Principal Name (UPN) used in sign-in request.</span></span>|
| <span data-ttu-id="9c297-169">80005</span><span class="sxs-lookup"><span data-stu-id="9c297-169">80005</span></span>| <span data-ttu-id="9c297-170">驗證代理程式：發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="9c297-170">Authentication Agent: Error occurred.</span></span>|
| <span data-ttu-id="9c297-171">80007</span><span class="sxs-lookup"><span data-stu-id="9c297-171">80007</span></span>| <span data-ttu-id="9c297-172">驗證代理程式無法 tooconnect tooActive 目錄。</span><span class="sxs-lookup"><span data-stu-id="9c297-172">Authentication Agent unable tooconnect tooActive Directory.</span></span>|
| <span data-ttu-id="9c297-173">80010</span><span class="sxs-lookup"><span data-stu-id="9c297-173">80010</span></span>| <span data-ttu-id="9c297-174">驗證代理程式無法 toodecrypt 密碼。</span><span class="sxs-lookup"><span data-stu-id="9c297-174">Authentication Agent unable toodecrypt password.</span></span>|
| <span data-ttu-id="9c297-175">81001</span><span class="sxs-lookup"><span data-stu-id="9c297-175">81001</span></span>| <span data-ttu-id="9c297-176">使用者的 Kerberos 票證太大。</span><span class="sxs-lookup"><span data-stu-id="9c297-176">User's Kerberos ticket is too large.</span></span>|
| <span data-ttu-id="9c297-177">81002</span><span class="sxs-lookup"><span data-stu-id="9c297-177">81002</span></span>| <span data-ttu-id="9c297-178">無法 toovalidate 使用者的 Kerberos 票證。</span><span class="sxs-lookup"><span data-stu-id="9c297-178">Unable toovalidate user's Kerberos ticket.</span></span>|
| <span data-ttu-id="9c297-179">81003</span><span class="sxs-lookup"><span data-stu-id="9c297-179">81003</span></span>| <span data-ttu-id="9c297-180">無法 toovalidate 使用者的 Kerberos 票證。</span><span class="sxs-lookup"><span data-stu-id="9c297-180">Unable toovalidate user's Kerberos ticket.</span></span>|
| <span data-ttu-id="9c297-181">81004</span><span class="sxs-lookup"><span data-stu-id="9c297-181">81004</span></span>| <span data-ttu-id="9c297-182">Kerberos 驗證嘗試失敗。</span><span class="sxs-lookup"><span data-stu-id="9c297-182">Kerberos authentication attempt failed.</span></span>|
| <span data-ttu-id="9c297-183">81008</span><span class="sxs-lookup"><span data-stu-id="9c297-183">81008</span></span>| <span data-ttu-id="9c297-184">無法 toovalidate 使用者的 Kerberos 票證。</span><span class="sxs-lookup"><span data-stu-id="9c297-184">Unable toovalidate user's Kerberos ticket.</span></span>|
| <span data-ttu-id="9c297-185">81009</span><span class="sxs-lookup"><span data-stu-id="9c297-185">81009</span></span>| <span data-ttu-id="9c297-186">無法 toovalidate 使用者的 Kerberos 票證。</span><span class="sxs-lookup"><span data-stu-id="9c297-186">Unable toovalidate user's Kerberos ticket.</span></span>|
| <span data-ttu-id="9c297-187">81010</span><span class="sxs-lookup"><span data-stu-id="9c297-187">81010</span></span>| <span data-ttu-id="9c297-188">無縫式 SSO 失敗，因為 hello 使用者的 Kerberos 票證已過期或無效。</span><span class="sxs-lookup"><span data-stu-id="9c297-188">Seamless SSO failed because hello user's Kerberos ticket has expired or is invalid.</span></span>|
| <span data-ttu-id="9c297-189">81011</span><span class="sxs-lookup"><span data-stu-id="9c297-189">81011</span></span>| <span data-ttu-id="9c297-190">無法 toofind hello 使用者的 Kerberos 票證中的資訊為基礎的使用者物件。</span><span class="sxs-lookup"><span data-stu-id="9c297-190">Unable toofind user object based on information in hello user's Kerberos ticket.</span></span>|
| <span data-ttu-id="9c297-191">81012</span><span class="sxs-lookup"><span data-stu-id="9c297-191">81012</span></span>| <span data-ttu-id="9c297-192">嘗試 toosign tooAzure AD 中的 hello 使用者所登入 hello 裝置 hello 使用者不同。</span><span class="sxs-lookup"><span data-stu-id="9c297-192">hello user trying toosign in tooAzure AD is different from hello user signed into hello device.</span></span>|
| <span data-ttu-id="9c297-193">81013</span><span class="sxs-lookup"><span data-stu-id="9c297-193">81013</span></span>| <span data-ttu-id="9c297-194">無法 toofind hello 使用者的 Kerberos 票證中的資訊為基礎的使用者物件。</span><span class="sxs-lookup"><span data-stu-id="9c297-194">Unable toofind user object based on information in hello user's Kerberos ticket.</span></span>|
| <span data-ttu-id="9c297-195">90014</span><span class="sxs-lookup"><span data-stu-id="9c297-195">90014</span></span>| <span data-ttu-id="9c297-196">預期的欄位不存在於 hello 認證時，在各種情況下使用。</span><span class="sxs-lookup"><span data-stu-id="9c297-196">Used in various cases when an expected field is not present in hello credential.</span></span>|
| <span data-ttu-id="9c297-197">90093</span><span class="sxs-lookup"><span data-stu-id="9c297-197">90093</span></span>| <span data-ttu-id="9c297-198">傳回錯誤碼禁止 hello 要求的圖形。</span><span class="sxs-lookup"><span data-stu-id="9c297-198">Graph returned with forbidden error code for hello request.</span></span>|



## <a name="next-steps"></a><span data-ttu-id="9c297-199">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9c297-199">Next steps</span></span>

<span data-ttu-id="9c297-200">如需詳細資訊，請參閱 hello[登入活動報表 hello Azure Active Directory 入口網站中的](active-directory-reporting-activity-sign-ins.md)。</span><span class="sxs-lookup"><span data-stu-id="9c297-200">For more details, see hello [Sign-in activity reports in hello Azure Active Directory portal](active-directory-reporting-activity-sign-ins.md).</span></span>

