---
title: "Azure Active Directory B2C： 了解 hello 入門組件的自訂原則 |Microsoft 文件"
description: "Azure Active Directory B2C 自訂原則的主題"
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: rojasja
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/25/2017
ms.author: joroja
ms.openlocfilehash: 3484e8cc6fa6a9d57c2aa14c0cc9616065892d10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-hello-custom-policies-of-hello-azure-ad-b2c-custom-policy-starter-pack"></a><span data-ttu-id="0d7ad-103">了解 hello hello Azure AD B2C 自訂原則入門組件的自訂原則</span><span class="sxs-lookup"><span data-stu-id="0d7ad-103">Understanding hello custom policies of hello Azure AD B2C Custom Policy starter pack</span></span>

<span data-ttu-id="0d7ad-104">此區段會列出所有 hello 核心項目所隨附 hello hello B2C_1A_base 原則**入門套件**和，可用來撰寫您自己的原則，透過的 hello hello 繼承*B2C_1A_base_擴充功能原則*。</span><span class="sxs-lookup"><span data-stu-id="0d7ad-104">This section lists all hello core elements of hello B2C_1A_base policy that comes with hello **Starter Pack** and that is leveraged for authoring your own policies through hello inheritance of hello *B2C_1A_base_extensions policy*.</span></span>

<span data-ttu-id="0d7ad-105">因此，它多特別著重於 hello 已經定義過了宣告類型、 宣告轉換、 內容定義、 宣告提供者與他們技術下列設定檔，而 hello 核心使用者皆。</span><span class="sxs-lookup"><span data-stu-id="0d7ad-105">As such, it more particularly focusses on hello already defined claim types, claims transformations, content definitions, claims providers with their technical profile(s), and hello core user journeys.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0d7ad-106">Microsoft 不做任何明示明示或默示，以下提供尊重 toohello 資訊。</span><span class="sxs-lookup"><span data-stu-id="0d7ad-106">Microsoft makes no warranties, express or implied, with respect toohello information provided hereafter.</span></span> <span data-ttu-id="0d7ad-107">任何時候 (GA 當下、之前或之後) 皆有可能導入變更。</span><span class="sxs-lookup"><span data-stu-id="0d7ad-107">Changes may be introduced at any time, before GA time, at GA time, or after.</span></span>

<span data-ttu-id="0d7ad-108">您自己的原則和 hello B2C_1A_base_extensions 原則可以覆寫這些定義，並視需要提供額外的擴充此父原則。</span><span class="sxs-lookup"><span data-stu-id="0d7ad-108">Both your own policies and hello B2C_1A_base_extensions policy can override these definitions and extend this parent policy by providing additional ones as needed.</span></span>

<span data-ttu-id="0d7ad-109">hello hello 核心項目*B2C_1A_base 原則*是宣告類型、 宣告轉換和內容的定義。</span><span class="sxs-lookup"><span data-stu-id="0d7ad-109">hello core elements of hello *B2C_1A_base policy* are claim types, claims transformations, and content definitions.</span></span> <span data-ttu-id="0d7ad-110">這些項目可以很容易遭受 hello 與您自己以及的原則中所參考的 toobe *B2C_1A_base_extensions 原則*。</span><span class="sxs-lookup"><span data-stu-id="0d7ad-110">These elements can susceptible toobe referenced in your own policies as well as in hello *B2C_1A_base_extensions policy*.</span></span>

## <a name="claims-schemas"></a><span data-ttu-id="0d7ad-111">宣告結構描述</span><span class="sxs-lookup"><span data-stu-id="0d7ad-111">Claims schemas</span></span>

<span data-ttu-id="0d7ad-112">此宣告結構描述分為三個部分︰</span><span class="sxs-lookup"><span data-stu-id="0d7ad-112">This claims schemas is divided into three sections:</span></span>

1.  <span data-ttu-id="0d7ad-113">第一個區段會列出所需的 hello 使用者皆 toowork 正確 hello 最小宣告。</span><span class="sxs-lookup"><span data-stu-id="0d7ad-113">A first section that lists hello minimum claims that are required for hello user journeys toowork properly.</span></span>
2.  <span data-ttu-id="0d7ad-114">第二個區段列出 hello 所需的查詢字串參數的宣告，和其他特殊參數 toobe 傳遞 tooother 宣告提供者，特別是 login.microsoftonline.com 進行驗證。</span><span class="sxs-lookup"><span data-stu-id="0d7ad-114">A second section that lists hello claims required for query string parameters and other special parameters toobe passed tooother claims providers, especially login.microsoftonline.com for authentication.</span></span> <span data-ttu-id="0d7ad-115">**請勿修改這些宣告**。</span><span class="sxs-lookup"><span data-stu-id="0d7ad-115">**Please do not modify these claims**.</span></span>
3.  <span data-ttu-id="0d7ad-116">和第三個區段會列出任何額外的選擇性宣告可收集來自 hello 使用者最後 hello 目錄中儲存並登入期間傳送權杖中。</span><span class="sxs-lookup"><span data-stu-id="0d7ad-116">And eventually a third section that lists any additional, optional claims that can be collected from hello user, stored in hello directory and sent in tokens during sign in.</span></span> <span data-ttu-id="0d7ad-117">本節中，可以加入新宣告型別 toobe hello 使用者從收集及/或傳送嗨權杖中。</span><span class="sxs-lookup"><span data-stu-id="0d7ad-117">New claims type toobe collected from hello user and/or sent in hello token can be added in this section.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0d7ad-118">hello 宣告結構描述包含某些宣告，例如密碼和使用者名稱的限制。</span><span class="sxs-lookup"><span data-stu-id="0d7ad-118">hello claims schema contains restrictions on certain claims such as passwords and usernames.</span></span> <span data-ttu-id="0d7ad-119">hello 信任架構 (TF) 原則會視為其他宣告提供者中的 Azure AD 和其所有的限制會在 hello premium 原則和模型化。</span><span class="sxs-lookup"><span data-stu-id="0d7ad-119">hello Trust Framework (TF) policy treats Azure AD as any other claims provider and all its restrictions are modelled in hello premium policy.</span></span> <span data-ttu-id="0d7ad-120">原則可以修改的 tooadd 更多的限制，或其他宣告提供者用於認證存放裝置，將有它自己的限制。</span><span class="sxs-lookup"><span data-stu-id="0d7ad-120">A policy could be modified tooadd more restrictions, or use another claims provider for credential storage which will have its own restrictions.</span></span>

<span data-ttu-id="0d7ad-121">hello 可用宣告類型如下所示。</span><span class="sxs-lookup"><span data-stu-id="0d7ad-121">hello available claim types are listed below.</span></span>

### <a name="claims-that-are-required-for-hello-user-journeys"></a><span data-ttu-id="0d7ad-122">所需的 hello 使用者皆宣告</span><span class="sxs-lookup"><span data-stu-id="0d7ad-122">Claims that are required for hello user journeys</span></span>

<span data-ttu-id="0d7ad-123">hello 下列宣告所需的使用者皆 toowork 正確：</span><span class="sxs-lookup"><span data-stu-id="0d7ad-123">hello following claims are required for user journeys toowork properly:</span></span>

| <span data-ttu-id="0d7ad-124">宣告類型</span><span class="sxs-lookup"><span data-stu-id="0d7ad-124">Claims type</span></span> | <span data-ttu-id="0d7ad-125">說明</span><span class="sxs-lookup"><span data-stu-id="0d7ad-125">Description</span></span> |
|-------------|-------------|
| <span data-ttu-id="0d7ad-126">UserId</span><span class="sxs-lookup"><span data-stu-id="0d7ad-126">*UserId*</span></span> | <span data-ttu-id="0d7ad-127">使用者名稱</span><span class="sxs-lookup"><span data-stu-id="0d7ad-127">Username</span></span> |
| <span data-ttu-id="0d7ad-128">signInName</span><span class="sxs-lookup"><span data-stu-id="0d7ad-128">*signInName*</span></span> | <span data-ttu-id="0d7ad-129">登入名稱</span><span class="sxs-lookup"><span data-stu-id="0d7ad-129">Sign in name</span></span> |
| <span data-ttu-id="0d7ad-130">tenantId</span><span class="sxs-lookup"><span data-stu-id="0d7ad-130">*tenantId*</span></span> | <span data-ttu-id="0d7ad-131">在 Azure AD B2C Premium hello 使用者物件的租用戶識別碼 (ID)</span><span class="sxs-lookup"><span data-stu-id="0d7ad-131">Tenant identifier (ID) of hello user object in Azure AD B2C Premium</span></span> |
| <span data-ttu-id="0d7ad-132">objectId</span><span class="sxs-lookup"><span data-stu-id="0d7ad-132">*objectId*</span></span> | <span data-ttu-id="0d7ad-133">在 Azure AD B2C Premium hello 使用者物件的物件識別碼 (ID)</span><span class="sxs-lookup"><span data-stu-id="0d7ad-133">Object identifier (ID) of hello user object in Azure AD B2C Premium</span></span> |
| <span data-ttu-id="0d7ad-134">*password*</span><span class="sxs-lookup"><span data-stu-id="0d7ad-134">*password*</span></span> | <span data-ttu-id="0d7ad-135">密碼</span><span class="sxs-lookup"><span data-stu-id="0d7ad-135">Password</span></span> |
| <span data-ttu-id="0d7ad-136">newPassword</span><span class="sxs-lookup"><span data-stu-id="0d7ad-136">*newPassword*</span></span> | |
| <span data-ttu-id="0d7ad-137">reenterPassword</span><span class="sxs-lookup"><span data-stu-id="0d7ad-137">*reenterPassword*</span></span> | |
| <span data-ttu-id="0d7ad-138">passwordPolicies</span><span class="sxs-lookup"><span data-stu-id="0d7ad-138">*passwordPolicies*</span></span> | <span data-ttu-id="0d7ad-139">Azure AD B2C Premium toodetermine 密碼強度、 到期和其他內容所使用的密碼原則。</span><span class="sxs-lookup"><span data-stu-id="0d7ad-139">Password policies used by Azure AD B2C Premium toodetermine password strength, expiry, etc.</span></span> |
| <span data-ttu-id="0d7ad-140">*sub*</span><span class="sxs-lookup"><span data-stu-id="0d7ad-140">*sub*</span></span> | |
| <span data-ttu-id="0d7ad-141">alternativeSecurityId</span><span class="sxs-lookup"><span data-stu-id="0d7ad-141">*alternativeSecurityId*</span></span> | |
| <span data-ttu-id="0d7ad-142">identityProvider</span><span class="sxs-lookup"><span data-stu-id="0d7ad-142">*identityProvider*</span></span> | |
| <span data-ttu-id="0d7ad-143">displayName</span><span class="sxs-lookup"><span data-stu-id="0d7ad-143">*displayName*</span></span> | |
| <span data-ttu-id="0d7ad-144">strongAuthenticationPhoneNumber</span><span class="sxs-lookup"><span data-stu-id="0d7ad-144">*strongAuthenticationPhoneNumber*</span></span> | <span data-ttu-id="0d7ad-145">使用者的電話號碼</span><span class="sxs-lookup"><span data-stu-id="0d7ad-145">User's telephone number</span></span> |
| <span data-ttu-id="0d7ad-146">Verified.strongAuthenticationPhoneNumber</span><span class="sxs-lookup"><span data-stu-id="0d7ad-146">*Verified.strongAuthenticationPhoneNumber*</span></span> | |
| <span data-ttu-id="0d7ad-147">email</span><span class="sxs-lookup"><span data-stu-id="0d7ad-147">*email*</span></span> | <span data-ttu-id="0d7ad-148">可以使用的 toocontact hello 使用者的電子郵件地址</span><span class="sxs-lookup"><span data-stu-id="0d7ad-148">Email address that can be used toocontact hello user</span></span> |
| <span data-ttu-id="0d7ad-149">signInNamesInfo.emailAddress</span><span class="sxs-lookup"><span data-stu-id="0d7ad-149">*signInNamesInfo.emailAddress*</span></span> | <span data-ttu-id="0d7ad-150">可用在 toosign hello 使用者的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="0d7ad-150">Email address that hello user can use toosign in</span></span> |
| <span data-ttu-id="0d7ad-151">otherMails</span><span class="sxs-lookup"><span data-stu-id="0d7ad-151">*otherMails*</span></span> | <span data-ttu-id="0d7ad-152">可以使用的 toocontact hello 使用者的電子郵件地址</span><span class="sxs-lookup"><span data-stu-id="0d7ad-152">Email addresses that can be used toocontact hello user</span></span> |
| <span data-ttu-id="0d7ad-153">userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="0d7ad-153">*userPrincipalName*</span></span> | <span data-ttu-id="0d7ad-154">Hello Azure AD B2C Premium 中所儲存的使用者名稱</span><span class="sxs-lookup"><span data-stu-id="0d7ad-154">Username as stored in hello Azure AD B2C Premium</span></span> |
| <span data-ttu-id="0d7ad-155">upnUserName</span><span class="sxs-lookup"><span data-stu-id="0d7ad-155">*upnUserName*</span></span> | <span data-ttu-id="0d7ad-156">用來建立使用者主體名稱的使用者名稱</span><span class="sxs-lookup"><span data-stu-id="0d7ad-156">Username for creating user principal name</span></span> |
| <span data-ttu-id="0d7ad-157">mailNickName</span><span class="sxs-lookup"><span data-stu-id="0d7ad-157">*mailNickName*</span></span> | <span data-ttu-id="0d7ad-158">使用者的郵件 nick 名稱儲存在 Azure AD B2C Premium hello</span><span class="sxs-lookup"><span data-stu-id="0d7ad-158">User's mail nick name as stored in hello Azure AD B2C Premium</span></span> |
| <span data-ttu-id="0d7ad-159">newUser</span><span class="sxs-lookup"><span data-stu-id="0d7ad-159">*newUser*</span></span> | |
| <span data-ttu-id="0d7ad-160">executed-SelfAsserted-Input</span><span class="sxs-lookup"><span data-stu-id="0d7ad-160">*executed-SelfAsserted-Input*</span></span> | <span data-ttu-id="0d7ad-161">指定屬性是否已收集來自 hello 使用者宣告</span><span class="sxs-lookup"><span data-stu-id="0d7ad-161">Claim that specifies whether attributes were collected from hello user</span></span> |
| <span data-ttu-id="0d7ad-162">executed-PhoneFactor-Input</span><span class="sxs-lookup"><span data-stu-id="0d7ad-162">*executed-PhoneFactor-Input*</span></span> | <span data-ttu-id="0d7ad-163">指定新的電話號碼是否收集來自 hello 使用者宣告</span><span class="sxs-lookup"><span data-stu-id="0d7ad-163">Claim that specifies whether a new phone number was collected from hello user</span></span> |
| <span data-ttu-id="0d7ad-164">authenticationSource</span><span class="sxs-lookup"><span data-stu-id="0d7ad-164">*authenticationSource*</span></span> | <span data-ttu-id="0d7ad-165">指定是否 hello 使用者已驗證在社交身分識別提供者、 login.microsoftonline.com 或本機帳戶</span><span class="sxs-lookup"><span data-stu-id="0d7ad-165">Specifies whether hello user was authenticated at Social Identity Provider, login.microsoftonline.com, or local account</span></span> |

### <a name="claims-required-for-query-string-parameters-and-other-special-parameters"></a><span data-ttu-id="0d7ad-166">查詢字串參數和其他特殊參數所需的宣告</span><span class="sxs-lookup"><span data-stu-id="0d7ad-166">Claims required for query string parameters and other special parameters</span></span>

<span data-ttu-id="0d7ad-167">hello 下列宣告是特殊的參數 （包括某些查詢字串參數） tooother 宣告提供者上的必要的 toopass:</span><span class="sxs-lookup"><span data-stu-id="0d7ad-167">hello following claims are required toopass on special parameters (including some query string parameters) tooother claims providers:</span></span>

| <span data-ttu-id="0d7ad-168">宣告類型</span><span class="sxs-lookup"><span data-stu-id="0d7ad-168">Claims type</span></span> | <span data-ttu-id="0d7ad-169">說明</span><span class="sxs-lookup"><span data-stu-id="0d7ad-169">Description</span></span> |
|-------------|-------------|
| <span data-ttu-id="0d7ad-170">nux</span><span class="sxs-lookup"><span data-stu-id="0d7ad-170">*nux*</span></span> | <span data-ttu-id="0d7ad-171">特殊的本機帳戶驗證 toologin.microsoftonline.com 傳遞的參數</span><span class="sxs-lookup"><span data-stu-id="0d7ad-171">Special parameter passed for local account authentication toologin.microsoftonline.com</span></span> |
| <span data-ttu-id="0d7ad-172">nca</span><span class="sxs-lookup"><span data-stu-id="0d7ad-172">*nca*</span></span> | <span data-ttu-id="0d7ad-173">特殊的本機帳戶驗證 toologin.microsoftonline.com 傳遞的參數</span><span class="sxs-lookup"><span data-stu-id="0d7ad-173">Special parameter passed for local account authentication toologin.microsoftonline.com</span></span> |
| <span data-ttu-id="0d7ad-174">prompt</span><span class="sxs-lookup"><span data-stu-id="0d7ad-174">*prompt*</span></span> | <span data-ttu-id="0d7ad-175">特殊的本機帳戶驗證 toologin.microsoftonline.com 傳遞的參數</span><span class="sxs-lookup"><span data-stu-id="0d7ad-175">Special parameter passed for local account authentication toologin.microsoftonline.com</span></span> |
| <span data-ttu-id="0d7ad-176">mkt</span><span class="sxs-lookup"><span data-stu-id="0d7ad-176">*mkt*</span></span> | <span data-ttu-id="0d7ad-177">特殊的本機帳戶驗證 toologin.microsoftonline.com 傳遞的參數</span><span class="sxs-lookup"><span data-stu-id="0d7ad-177">Special parameter passed for local account authentication toologin.microsoftonline.com</span></span> |
| <span data-ttu-id="0d7ad-178">lc</span><span class="sxs-lookup"><span data-stu-id="0d7ad-178">*lc*</span></span> | <span data-ttu-id="0d7ad-179">特殊的本機帳戶驗證 toologin.microsoftonline.com 傳遞的參數</span><span class="sxs-lookup"><span data-stu-id="0d7ad-179">Special parameter passed for local account authentication toologin.microsoftonline.com</span></span> |
| <span data-ttu-id="0d7ad-180">grant_type</span><span class="sxs-lookup"><span data-stu-id="0d7ad-180">*grant_type*</span></span> | <span data-ttu-id="0d7ad-181">特殊的本機帳戶驗證 toologin.microsoftonline.com 傳遞的參數</span><span class="sxs-lookup"><span data-stu-id="0d7ad-181">Special parameter passed for local account authentication toologin.microsoftonline.com</span></span> |
| <span data-ttu-id="0d7ad-182">scope</span><span class="sxs-lookup"><span data-stu-id="0d7ad-182">*scope*</span></span> | <span data-ttu-id="0d7ad-183">特殊的本機帳戶驗證 toologin.microsoftonline.com 傳遞的參數</span><span class="sxs-lookup"><span data-stu-id="0d7ad-183">Special parameter passed for local account authentication toologin.microsoftonline.com</span></span> |
| <span data-ttu-id="0d7ad-184">client_id</span><span class="sxs-lookup"><span data-stu-id="0d7ad-184">*client_id*</span></span> | <span data-ttu-id="0d7ad-185">特殊的本機帳戶驗證 toologin.microsoftonline.com 傳遞的參數</span><span class="sxs-lookup"><span data-stu-id="0d7ad-185">Special parameter passed for local account authentication toologin.microsoftonline.com</span></span> |
| <span data-ttu-id="0d7ad-186">objectIdFromSession</span><span class="sxs-lookup"><span data-stu-id="0d7ad-186">*objectIdFromSession*</span></span> | <span data-ttu-id="0d7ad-187">已擷取 hello 預設工作階段管理提供者 tooindicate hello 物件識別碼，所提供的參數，從 SSO 工作階段</span><span class="sxs-lookup"><span data-stu-id="0d7ad-187">Parameter provided by hello default session management provider tooindicate that hello object id has been retrieved from an SSO session</span></span> |
| <span data-ttu-id="0d7ad-188">isActiveMFASession</span><span class="sxs-lookup"><span data-stu-id="0d7ad-188">*isActiveMFASession*</span></span> | <span data-ttu-id="0d7ad-189">參數所提供 hello MFA 工作階段管理 tooindicate hello 使用者具有作用中的 MFA 工作階段</span><span class="sxs-lookup"><span data-stu-id="0d7ad-189">Parameter provided by hello MFA session management tooindicate that hello user has an active MFA session</span></span> |

### <a name="additional-optional-claims-that-can-be-collected"></a><span data-ttu-id="0d7ad-190">其他可以收集的 (選擇性) 宣告</span><span class="sxs-lookup"><span data-stu-id="0d7ad-190">Additional (optional) claims that can be collected</span></span>

<span data-ttu-id="0d7ad-191">hello 下列宣告會從 hello 使用者收集的其他宣告儲存在 hello 目錄中，並傳送嗨權杖中。</span><span class="sxs-lookup"><span data-stu-id="0d7ad-191">hello following claims are additional claims that can be collected from hello users, stored in hello directory, and sent in hello token.</span></span> <span data-ttu-id="0d7ad-192">如之前所述，新增額外宣告可以是 toothis 清單。</span><span class="sxs-lookup"><span data-stu-id="0d7ad-192">As outlined before, additional claims can be added toothis list.</span></span>

| <span data-ttu-id="0d7ad-193">宣告類型</span><span class="sxs-lookup"><span data-stu-id="0d7ad-193">Claims type</span></span> | <span data-ttu-id="0d7ad-194">說明</span><span class="sxs-lookup"><span data-stu-id="0d7ad-194">Description</span></span> |
|-------------|-------------|
| <span data-ttu-id="0d7ad-195">givenName</span><span class="sxs-lookup"><span data-stu-id="0d7ad-195">*givenName*</span></span> | <span data-ttu-id="0d7ad-196">使用者的名字 (也就是第一個名字)</span><span class="sxs-lookup"><span data-stu-id="0d7ad-196">User's given name (also known as first name)</span></span> |
| <span data-ttu-id="0d7ad-197">surname</span><span class="sxs-lookup"><span data-stu-id="0d7ad-197">*surname*</span></span> | <span data-ttu-id="0d7ad-198">使用者的姓氏</span><span class="sxs-lookup"><span data-stu-id="0d7ad-198">User's surname (also known as family name or last name)</span></span> |
| <span data-ttu-id="0d7ad-199">Extension_picture</span><span class="sxs-lookup"><span data-stu-id="0d7ad-199">*Extension_picture*</span></span> | <span data-ttu-id="0d7ad-200">使用者的社交網站相片</span><span class="sxs-lookup"><span data-stu-id="0d7ad-200">User's picture from social</span></span> |

## <a name="claim-transformations"></a><span data-ttu-id="0d7ad-201">宣告轉換</span><span class="sxs-lookup"><span data-stu-id="0d7ad-201">Claim transformations</span></span>

<span data-ttu-id="0d7ad-202">hello 可用宣告轉換如下所示。</span><span class="sxs-lookup"><span data-stu-id="0d7ad-202">hello available claim transformations are listed below.</span></span>

| <span data-ttu-id="0d7ad-203">宣告轉換</span><span class="sxs-lookup"><span data-stu-id="0d7ad-203">Claim transformation</span></span> | <span data-ttu-id="0d7ad-204">說明</span><span class="sxs-lookup"><span data-stu-id="0d7ad-204">Description</span></span> |
|----------------------|-------------|
| <span data-ttu-id="0d7ad-205">CreateOtherMailsFromEmail</span><span class="sxs-lookup"><span data-stu-id="0d7ad-205">*CreateOtherMailsFromEmail*</span></span> | |
| <span data-ttu-id="0d7ad-206">CreateRandomUPNUserName</span><span class="sxs-lookup"><span data-stu-id="0d7ad-206">*CreateRandomUPNUserName*</span></span> | |
| <span data-ttu-id="0d7ad-207">CreateUserPrincipalName</span><span class="sxs-lookup"><span data-stu-id="0d7ad-207">*CreateUserPrincipalName*</span></span> | |
| <span data-ttu-id="0d7ad-208">CreateSubjectClaimFromObjectID</span><span class="sxs-lookup"><span data-stu-id="0d7ad-208">*CreateSubjectClaimFromObjectID*</span></span> | |
| <span data-ttu-id="0d7ad-209">CreateSubjectClaimFromAlternativeSecurityId</span><span class="sxs-lookup"><span data-stu-id="0d7ad-209">*CreateSubjectClaimFromAlternativeSecurityId*</span></span> | |
| <span data-ttu-id="0d7ad-210">CreateAlternativeSecurityId</span><span class="sxs-lookup"><span data-stu-id="0d7ad-210">*CreateAlternativeSecurityId*</span></span> | |

## <a name="content-definitions"></a><span data-ttu-id="0d7ad-211">內容定義</span><span class="sxs-lookup"><span data-stu-id="0d7ad-211">Content definitions</span></span>

<span data-ttu-id="0d7ad-212">本章節描述 hello hello 中已經宣告過的內容定義*B2C_1A_base*原則。</span><span class="sxs-lookup"><span data-stu-id="0d7ad-212">This section describes hello content definitions already declared in hello *B2C_1A_base* policy.</span></span> <span data-ttu-id="0d7ad-213">這些內容的定義是很容易遭受 toobe 參考、 覆寫時，及/或擴充視需要在您的原則也如同 hello *B2C_1A_base_extensions*原則。</span><span class="sxs-lookup"><span data-stu-id="0d7ad-213">These content definitions are susceptible toobe referenced, overridden, and/or extended as needed in your own policies as well as in hello *B2C_1A_base_extensions* policy.</span></span>

| <span data-ttu-id="0d7ad-214">宣告提供者</span><span class="sxs-lookup"><span data-stu-id="0d7ad-214">Claims provider</span></span> | <span data-ttu-id="0d7ad-215">說明</span><span class="sxs-lookup"><span data-stu-id="0d7ad-215">Description</span></span> |
|-----------------|-------------|
| <span data-ttu-id="0d7ad-216">*Facebook*</span><span class="sxs-lookup"><span data-stu-id="0d7ad-216">*Facebook*</span></span> | |
| <span data-ttu-id="0d7ad-217">本機帳戶登入</span><span class="sxs-lookup"><span data-stu-id="0d7ad-217">*Local Account SignIn*</span></span> | |
| <span data-ttu-id="0d7ad-218">PhoneFactor</span><span class="sxs-lookup"><span data-stu-id="0d7ad-218">*PhoneFactor*</span></span> | |
| <span data-ttu-id="0d7ad-219">*Azure Active Directory*</span><span class="sxs-lookup"><span data-stu-id="0d7ad-219">*Azure Active Directory*</span></span> | |
| <span data-ttu-id="0d7ad-220">自我判斷提示</span><span class="sxs-lookup"><span data-stu-id="0d7ad-220">*Self Asserted*</span></span> | |
| <span data-ttu-id="0d7ad-221">本機帳戶</span><span class="sxs-lookup"><span data-stu-id="0d7ad-221">*Local Account*</span></span> | |
| <span data-ttu-id="0d7ad-222">*工作階段管理*</span><span class="sxs-lookup"><span data-stu-id="0d7ad-222">*Session Management*</span></span> | |
| <span data-ttu-id="0d7ad-223">Trustframework 原則引擎</span><span class="sxs-lookup"><span data-stu-id="0d7ad-223">*Trustframework Policy Engine*</span></span> | |
| <span data-ttu-id="0d7ad-224">TechnicalProfiles</span><span class="sxs-lookup"><span data-stu-id="0d7ad-224">*TechnicalProfiles*</span></span> | |
| <span data-ttu-id="0d7ad-225">權杖簽發者</span><span class="sxs-lookup"><span data-stu-id="0d7ad-225">*Token Issuer*</span></span> | |

## <a name="technical-profiles"></a><span data-ttu-id="0d7ad-226">技術設定檔</span><span class="sxs-lookup"><span data-stu-id="0d7ad-226">Technical profiles</span></span>

<span data-ttu-id="0d7ad-227">本章節描述 hello 技術設定檔已宣告每個宣告提供者在 hello *B2C_1A_base*原則。</span><span class="sxs-lookup"><span data-stu-id="0d7ad-227">This section depicts hello technical profiles already declared per claim provider in hello *B2C_1A_base* policy.</span></span> <span data-ttu-id="0d7ad-228">這些技術的設定檔是很容易遭受 toobe 進一步參考、 覆寫時，及/或擴充視需要在您的原則也如同 hello *B2C_1A_base_extensions*原則。</span><span class="sxs-lookup"><span data-stu-id="0d7ad-228">These technical profiles are susceptible toobe further referenced, overridden, and/or extended as needed in your own policies as well as in hello *B2C_1A_base_extensions* policy.</span></span>

### <a name="technical-profiles-for-facebook"></a><span data-ttu-id="0d7ad-229">Facebook 的技術設定檔</span><span class="sxs-lookup"><span data-stu-id="0d7ad-229">Technical profiles for Facebook</span></span>

| <span data-ttu-id="0d7ad-230">技術設定檔</span><span class="sxs-lookup"><span data-stu-id="0d7ad-230">Technical profile</span></span> | <span data-ttu-id="0d7ad-231">說明</span><span class="sxs-lookup"><span data-stu-id="0d7ad-231">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="0d7ad-232">Facebook-OAUTH</span><span class="sxs-lookup"><span data-stu-id="0d7ad-232">*Facebook-OAUTH*</span></span> | |

### <a name="technical-profiles-for-local-account-signin"></a><span data-ttu-id="0d7ad-233">本機帳戶登入的技術設定檔</span><span class="sxs-lookup"><span data-stu-id="0d7ad-233">Technical profiles for Local Account Signin</span></span>

| <span data-ttu-id="0d7ad-234">技術設定檔</span><span class="sxs-lookup"><span data-stu-id="0d7ad-234">Technical profile</span></span> | <span data-ttu-id="0d7ad-235">說明</span><span class="sxs-lookup"><span data-stu-id="0d7ad-235">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="0d7ad-236">Login-NonInteractive</span><span class="sxs-lookup"><span data-stu-id="0d7ad-236">*Login-NonInteractive*</span></span> | |

### <a name="technical-profiles-for-phone-factor"></a><span data-ttu-id="0d7ad-237">PhoneFactor 的技術設定檔</span><span class="sxs-lookup"><span data-stu-id="0d7ad-237">Technical profiles for Phone Factor</span></span>

| <span data-ttu-id="0d7ad-238">技術設定檔</span><span class="sxs-lookup"><span data-stu-id="0d7ad-238">Technical profile</span></span> | <span data-ttu-id="0d7ad-239">說明</span><span class="sxs-lookup"><span data-stu-id="0d7ad-239">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="0d7ad-240">PhoneFactor-Input</span><span class="sxs-lookup"><span data-stu-id="0d7ad-240">*PhoneFactor-Input*</span></span> | |
| <span data-ttu-id="0d7ad-241">PhoneFactor-InputOrVerify</span><span class="sxs-lookup"><span data-stu-id="0d7ad-241">*PhoneFactor-InputOrVerify*</span></span> | |
| <span data-ttu-id="0d7ad-242">PhoneFactor-Verify</span><span class="sxs-lookup"><span data-stu-id="0d7ad-242">*PhoneFactor-Verify*</span></span> | |

### <a name="technical-profiles-for-azure-active-directory"></a><span data-ttu-id="0d7ad-243">Azure Active Directory 的技術設定檔</span><span class="sxs-lookup"><span data-stu-id="0d7ad-243">Technical profiles for Azure Active Directory</span></span>

| <span data-ttu-id="0d7ad-244">技術設定檔</span><span class="sxs-lookup"><span data-stu-id="0d7ad-244">Technical profile</span></span> | <span data-ttu-id="0d7ad-245">說明</span><span class="sxs-lookup"><span data-stu-id="0d7ad-245">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="0d7ad-246">AAD-Common</span><span class="sxs-lookup"><span data-stu-id="0d7ad-246">*AAD-Common*</span></span> | <span data-ttu-id="0d7ad-247">所包含的設定檔技術 hello 其他 AAD xxx 技術的設定檔</span><span class="sxs-lookup"><span data-stu-id="0d7ad-247">Technical profile included by hello other AAD-xxx technical profiles</span></span> |
| <span data-ttu-id="0d7ad-248">AAD-UserWriteUsingAlternativeSecurityId</span><span class="sxs-lookup"><span data-stu-id="0d7ad-248">*AAD-UserWriteUsingAlternativeSecurityId*</span></span> | <span data-ttu-id="0d7ad-249">社交登入的技術設定檔</span><span class="sxs-lookup"><span data-stu-id="0d7ad-249">Technical profile for social logins</span></span> |
| <span data-ttu-id="0d7ad-250">AAD-UserReadUsingAlternativeSecurityId</span><span class="sxs-lookup"><span data-stu-id="0d7ad-250">*AAD-UserReadUsingAlternativeSecurityId*</span></span> | <span data-ttu-id="0d7ad-251">社交登入的技術設定檔</span><span class="sxs-lookup"><span data-stu-id="0d7ad-251">Technical profile for social logins</span></span> |
| <span data-ttu-id="0d7ad-252">AAD-UserReadUsingAlternativeSecurityId-NoError</span><span class="sxs-lookup"><span data-stu-id="0d7ad-252">*AAD-UserReadUsingAlternativeSecurityId-NoError*</span></span> | <span data-ttu-id="0d7ad-253">社交登入的技術設定檔</span><span class="sxs-lookup"><span data-stu-id="0d7ad-253">Technical profile for social logins</span></span> |
| <span data-ttu-id="0d7ad-254">AAD-UserWritePasswordUsingLogonEmail</span><span class="sxs-lookup"><span data-stu-id="0d7ad-254">*AAD-UserWritePasswordUsingLogonEmail*</span></span> | <span data-ttu-id="0d7ad-255">本機帳戶的技術設定檔</span><span class="sxs-lookup"><span data-stu-id="0d7ad-255">Technical profile for local accounts</span></span> |
| <span data-ttu-id="0d7ad-256">AAD-UserReadUsingEmailAddress</span><span class="sxs-lookup"><span data-stu-id="0d7ad-256">*AAD-UserReadUsingEmailAddress*</span></span> | <span data-ttu-id="0d7ad-257">本機帳戶的技術設定檔</span><span class="sxs-lookup"><span data-stu-id="0d7ad-257">Technical profile for local accounts</span></span> |
| <span data-ttu-id="0d7ad-258">AAD-UserWriteProfileUsingObjectId</span><span class="sxs-lookup"><span data-stu-id="0d7ad-258">*AAD-UserWriteProfileUsingObjectId*</span></span> | <span data-ttu-id="0d7ad-259">可供使用 objectId 來更新使用者記錄的技術設定檔</span><span class="sxs-lookup"><span data-stu-id="0d7ad-259">Technical profile for updating user record using objectId</span></span> |
| <span data-ttu-id="0d7ad-260">AAD-UserWritePhoneNumberUsingObjectId</span><span class="sxs-lookup"><span data-stu-id="0d7ad-260">*AAD-UserWritePhoneNumberUsingObjectId*</span></span> | <span data-ttu-id="0d7ad-261">可供使用 objectId 來更新使用者記錄的技術設定檔</span><span class="sxs-lookup"><span data-stu-id="0d7ad-261">Technical profile for updating user record using objectId</span></span> |
| <span data-ttu-id="0d7ad-262">AAD-UserWritePasswordUsingObjectId</span><span class="sxs-lookup"><span data-stu-id="0d7ad-262">*AAD-UserWritePasswordUsingObjectId*</span></span> | <span data-ttu-id="0d7ad-263">可供使用 objectId 來更新使用者記錄的技術設定檔</span><span class="sxs-lookup"><span data-stu-id="0d7ad-263">Technical profile for updating user record using objectId</span></span> |
| <span data-ttu-id="0d7ad-264">AAD-UserReadUsingObjectId</span><span class="sxs-lookup"><span data-stu-id="0d7ad-264">*AAD-UserReadUsingObjectId*</span></span> | <span data-ttu-id="0d7ad-265">技術的設定檔是使用的 tooread 後，資料會驗證使用者</span><span class="sxs-lookup"><span data-stu-id="0d7ad-265">Technical profile is used tooread data after user authenticates</span></span> |

### <a name="technical-profiles-for-self-asserted"></a><span data-ttu-id="0d7ad-266">自我判斷提示的技術設定檔</span><span class="sxs-lookup"><span data-stu-id="0d7ad-266">Technical profiles for Self Asserted</span></span>

| <span data-ttu-id="0d7ad-267">技術設定檔</span><span class="sxs-lookup"><span data-stu-id="0d7ad-267">Technical profile</span></span> | <span data-ttu-id="0d7ad-268">說明</span><span class="sxs-lookup"><span data-stu-id="0d7ad-268">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="0d7ad-269">SelfAsserted-Social</span><span class="sxs-lookup"><span data-stu-id="0d7ad-269">*SelfAsserted-Social*</span></span> | |
| <span data-ttu-id="0d7ad-270">SelfAsserted-ProfileUpdate</span><span class="sxs-lookup"><span data-stu-id="0d7ad-270">*SelfAsserted-ProfileUpdate*</span></span> | |

### <a name="technical-profiles-for-local-account"></a><span data-ttu-id="0d7ad-271">本機帳戶的技術設定檔</span><span class="sxs-lookup"><span data-stu-id="0d7ad-271">Technical profiles for Local Account</span></span>

| <span data-ttu-id="0d7ad-272">技術設定檔</span><span class="sxs-lookup"><span data-stu-id="0d7ad-272">Technical profile</span></span> | <span data-ttu-id="0d7ad-273">說明</span><span class="sxs-lookup"><span data-stu-id="0d7ad-273">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="0d7ad-274">LocalAccountSignUpWithLogonEmail</span><span class="sxs-lookup"><span data-stu-id="0d7ad-274">*LocalAccountSignUpWithLogonEmail*</span></span> | |

### <a name="technical-profiles-for-session-management"></a><span data-ttu-id="0d7ad-275">工作階段管理的技術設定檔</span><span class="sxs-lookup"><span data-stu-id="0d7ad-275">Technical profiles for Session Management</span></span>

| <span data-ttu-id="0d7ad-276">技術設定檔</span><span class="sxs-lookup"><span data-stu-id="0d7ad-276">Technical profile</span></span> | <span data-ttu-id="0d7ad-277">說明</span><span class="sxs-lookup"><span data-stu-id="0d7ad-277">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="0d7ad-278">SM-Noop</span><span class="sxs-lookup"><span data-stu-id="0d7ad-278">*SM-Noop*</span></span> | |
| <span data-ttu-id="0d7ad-279">SM-AAD</span><span class="sxs-lookup"><span data-stu-id="0d7ad-279">*SM-AAD*</span></span> | |
| <span data-ttu-id="0d7ad-280">SM-SocialSignup</span><span class="sxs-lookup"><span data-stu-id="0d7ad-280">*SM-SocialSignup*</span></span> | <span data-ttu-id="0d7ad-281">設定檔名稱是正在登之間使用的 toodisambiguate AAD 工作階段設定和登入</span><span class="sxs-lookup"><span data-stu-id="0d7ad-281">Profile name is being used toodisambiguate AAD session between sign up and sign in</span></span> |
| <span data-ttu-id="0d7ad-282">SM-SocialLogin</span><span class="sxs-lookup"><span data-stu-id="0d7ad-282">*SM-SocialLogin*</span></span> | |
| <span data-ttu-id="0d7ad-283">SM-MFA</span><span class="sxs-lookup"><span data-stu-id="0d7ad-283">*SM-MFA*</span></span> | |

### <a name="technical-profiles-for-trustframework-policy-engine-technicalprofiles"></a><span data-ttu-id="0d7ad-284">Trustframework 原則引擎 TechnicalProfiles 的技術設定檔</span><span class="sxs-lookup"><span data-stu-id="0d7ad-284">Technical profiles for Trustframework Policy Engine TechnicalProfiles</span></span>

<span data-ttu-id="0d7ad-285">目前，沒有技術的設定檔定義 hello **Trustframework 原則引擎 TechnicalProfiles**宣告提供者。</span><span class="sxs-lookup"><span data-stu-id="0d7ad-285">Currently, no technical profiles are defined for hello **Trustframework Policy Engine TechnicalProfiles** claims provider.</span></span>

### <a name="technical-profiles-for-token-issuer"></a><span data-ttu-id="0d7ad-286">權杖簽發者的技術設定檔</span><span class="sxs-lookup"><span data-stu-id="0d7ad-286">Technical profiles for Token Issuer</span></span>

| <span data-ttu-id="0d7ad-287">技術設定檔</span><span class="sxs-lookup"><span data-stu-id="0d7ad-287">Technical profile</span></span> | <span data-ttu-id="0d7ad-288">說明</span><span class="sxs-lookup"><span data-stu-id="0d7ad-288">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="0d7ad-289">JwtIssuer</span><span class="sxs-lookup"><span data-stu-id="0d7ad-289">*JwtIssuer*</span></span> | |

## <a name="user-journeys"></a><span data-ttu-id="0d7ad-290">使用者旅程</span><span class="sxs-lookup"><span data-stu-id="0d7ad-290">User journeys</span></span>

<span data-ttu-id="0d7ad-291">本章節描述 hello hello 中已經宣告過的使用者皆*B2C_1A_base*原則。</span><span class="sxs-lookup"><span data-stu-id="0d7ad-291">This section depicts hello user journeys already declared in hello *B2C_1A_base* policy.</span></span> <span data-ttu-id="0d7ad-292">這些使用者皆會受到 toobe 進一步參考、 覆寫時，及/或擴充視需要在您的原則也如同 hello *B2C_1A_base_extensions*原則。</span><span class="sxs-lookup"><span data-stu-id="0d7ad-292">These user journeys are susceptible toobe further referenced, overridden, and/or extended as needed in your own policies as well as in hello *B2C_1A_base_extensions* policy.</span></span>

| <span data-ttu-id="0d7ad-293">使用者旅程</span><span class="sxs-lookup"><span data-stu-id="0d7ad-293">User journey</span></span> | <span data-ttu-id="0d7ad-294">說明</span><span class="sxs-lookup"><span data-stu-id="0d7ad-294">Description</span></span> |
|--------------|-------------|
| <span data-ttu-id="0d7ad-295">SignUp</span><span class="sxs-lookup"><span data-stu-id="0d7ad-295">*SignUp*</span></span> | |
| <span data-ttu-id="0d7ad-296">SignIn</span><span class="sxs-lookup"><span data-stu-id="0d7ad-296">*SignIn*</span></span> | |
| <span data-ttu-id="0d7ad-297">SignUpOrSignIn</span><span class="sxs-lookup"><span data-stu-id="0d7ad-297">*SignUpOrSignIn*</span></span> | |
| <span data-ttu-id="0d7ad-298">EditProfile</span><span class="sxs-lookup"><span data-stu-id="0d7ad-298">*EditProfile*</span></span> | |
| <span data-ttu-id="0d7ad-299">PasswordReset</span><span class="sxs-lookup"><span data-stu-id="0d7ad-299">*PasswordReset*</span></span> | |
