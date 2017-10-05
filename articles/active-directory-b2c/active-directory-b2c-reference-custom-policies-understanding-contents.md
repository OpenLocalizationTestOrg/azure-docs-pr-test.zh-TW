---
title: "Azure Active Directory B2C：了解入門套件的自訂原則 | Microsoft Docs"
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
ms.openlocfilehash: 9847bcfcc139a769847678c1cca6a8b9c3a30e93
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="understanding-the-custom-policies-of-the-azure-ad-b2c-custom-policy-starter-pack"></a><span data-ttu-id="b4188-103">了解 Azure AD B2C 自訂原則入門套件的自訂原則</span><span class="sxs-lookup"><span data-stu-id="b4188-103">Understanding the custom policies of the Azure AD B2C Custom Policy starter pack</span></span>

<span data-ttu-id="b4188-104">本節會列出**入門套件**隨附之 B2C_1A_base 原則的所有核心元素，此原則也可用來透過繼承 B2C_1A_base_extensions 原則來撰寫您自己的原則。</span><span class="sxs-lookup"><span data-stu-id="b4188-104">This section lists all the core elements of the B2C_1A_base policy that comes with the **Starter Pack** and that is leveraged for authoring your own policies through the inheritance of the *B2C_1A_base_extensions policy*.</span></span>

<span data-ttu-id="b4188-105">因此，本節會特別著重在已定義的宣告類型、宣告轉換、內容定義、宣告提供者與其技術設定檔，以及核心的使用者旅程。</span><span class="sxs-lookup"><span data-stu-id="b4188-105">As such, it more particularly focusses on the already defined claim types, claims transformations, content definitions, claims providers with their technical profile(s), and the core user journeys.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b4188-106">Microsoft 對於以下所提供的資訊不做任何明示或暗示的保證。</span><span class="sxs-lookup"><span data-stu-id="b4188-106">Microsoft makes no warranties, express or implied, with respect to the information provided hereafter.</span></span> <span data-ttu-id="b4188-107">任何時候 (GA 當下、之前或之後) 皆有可能導入變更。</span><span class="sxs-lookup"><span data-stu-id="b4188-107">Changes may be introduced at any time, before GA time, at GA time, or after.</span></span>

<span data-ttu-id="b4188-108">您自己的原則和 B2C_1A_base_extensions 原則都可以覆寫這些定義，並視需要提供其他定義來擴充此父系原則。</span><span class="sxs-lookup"><span data-stu-id="b4188-108">Both your own policies and the B2C_1A_base_extensions policy can override these definitions and extend this parent policy by providing additional ones as needed.</span></span>

<span data-ttu-id="b4188-109">B2C_1A_base 原則的核心元素是宣告類型、宣告轉換及內容定義。</span><span class="sxs-lookup"><span data-stu-id="b4188-109">The core elements of the *B2C_1A_base policy* are claim types, claims transformations, and content definitions.</span></span> <span data-ttu-id="b4188-110">您可以很容易地在您自己的原則和 B2C_1A_base_extensions 原則中參考這些元素。</span><span class="sxs-lookup"><span data-stu-id="b4188-110">These elements can susceptible to be referenced in your own policies as well as in the *B2C_1A_base_extensions policy*.</span></span>

## <a name="claims-schemas"></a><span data-ttu-id="b4188-111">宣告結構描述</span><span class="sxs-lookup"><span data-stu-id="b4188-111">Claims schemas</span></span>

<span data-ttu-id="b4188-112">此宣告結構描述分為三個部分︰</span><span class="sxs-lookup"><span data-stu-id="b4188-112">This claims schemas is divided into three sections:</span></span>

1.  <span data-ttu-id="b4188-113">第一個部分會列出所需的最小宣告，以便使用者旅程能正常運作。</span><span class="sxs-lookup"><span data-stu-id="b4188-113">A first section that lists the minimum claims that are required for the user journeys to work properly.</span></span>
2.  <span data-ttu-id="b4188-114">第二個部分會列出所需的宣告，以便查詢字串參數和其他特殊參數能傳遞至其他宣告提供者，尤其是 login.microsoftonline.com 以便進行驗證。</span><span class="sxs-lookup"><span data-stu-id="b4188-114">A second section that lists the claims required for query string parameters and other special parameters to be passed to other claims providers, especially login.microsoftonline.com for authentication.</span></span> <span data-ttu-id="b4188-115">**請勿修改這些宣告**。</span><span class="sxs-lookup"><span data-stu-id="b4188-115">**Please do not modify these claims**.</span></span>
3.  <span data-ttu-id="b4188-116">最後，第三個部分會列出其他任何選擇性宣告，這些宣告可從使用者收集而來、儲存在目錄中，以及在登入期間於權杖中傳送。</span><span class="sxs-lookup"><span data-stu-id="b4188-116">And eventually a third section that lists any additional, optional claims that can be collected from the user, stored in the directory and sent in tokens during sign in.</span></span> <span data-ttu-id="b4188-117">要從使用者收集而來和/或要在權杖中傳送的新宣告類型可以新增到這個部分。</span><span class="sxs-lookup"><span data-stu-id="b4188-117">New claims type to be collected from the user and/or sent in the token can be added in this section.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b4188-118">對於某些宣告 (例如密碼和使用者名稱)，宣告結構描述會含有限制。</span><span class="sxs-lookup"><span data-stu-id="b4188-118">The claims schema contains restrictions on certain claims such as passwords and usernames.</span></span> <span data-ttu-id="b4188-119">信任架構 (TF) 原則會將 Azure AD 視為其他宣告提供者，此原則的所有限制會在進階原則中模型化。</span><span class="sxs-lookup"><span data-stu-id="b4188-119">The Trust Framework (TF) policy treats Azure AD as any other claims provider and all its restrictions are modelled in the premium policy.</span></span> <span data-ttu-id="b4188-120">原則經過修改後即可新增更多限制，或使用另一個宣告提供者來儲存認證，但該提供者會有它自己的限制。</span><span class="sxs-lookup"><span data-stu-id="b4188-120">A policy could be modified to add more restrictions, or use another claims provider for credential storage which will have its own restrictions.</span></span>

<span data-ttu-id="b4188-121">以下列出可用的宣告類型。</span><span class="sxs-lookup"><span data-stu-id="b4188-121">The available claim types are listed below.</span></span>

### <a name="claims-that-are-required-for-the-user-journeys"></a><span data-ttu-id="b4188-122">使用者旅程所需的宣告</span><span class="sxs-lookup"><span data-stu-id="b4188-122">Claims that are required for the user journeys</span></span>

<span data-ttu-id="b4188-123">需要有下列宣告才能讓使用者旅程正常運作︰</span><span class="sxs-lookup"><span data-stu-id="b4188-123">The following claims are required for user journeys to work properly:</span></span>

| <span data-ttu-id="b4188-124">宣告類型</span><span class="sxs-lookup"><span data-stu-id="b4188-124">Claims type</span></span> | <span data-ttu-id="b4188-125">說明</span><span class="sxs-lookup"><span data-stu-id="b4188-125">Description</span></span> |
|-------------|-------------|
| <span data-ttu-id="b4188-126">UserId</span><span class="sxs-lookup"><span data-stu-id="b4188-126">*UserId*</span></span> | <span data-ttu-id="b4188-127">使用者名稱</span><span class="sxs-lookup"><span data-stu-id="b4188-127">Username</span></span> |
| <span data-ttu-id="b4188-128">signInName</span><span class="sxs-lookup"><span data-stu-id="b4188-128">*signInName*</span></span> | <span data-ttu-id="b4188-129">登入名稱</span><span class="sxs-lookup"><span data-stu-id="b4188-129">Sign in name</span></span> |
| <span data-ttu-id="b4188-130">tenantId</span><span class="sxs-lookup"><span data-stu-id="b4188-130">*tenantId*</span></span> | <span data-ttu-id="b4188-131">Azure AD B2C 進階版中使用者物件的租用戶識別碼 (ID)</span><span class="sxs-lookup"><span data-stu-id="b4188-131">Tenant identifier (ID) of the user object in Azure AD B2C Premium</span></span> |
| <span data-ttu-id="b4188-132">objectId</span><span class="sxs-lookup"><span data-stu-id="b4188-132">*objectId*</span></span> | <span data-ttu-id="b4188-133">Azure AD B2C 進階版中使用者物件的物件識別碼 (ID)</span><span class="sxs-lookup"><span data-stu-id="b4188-133">Object identifier (ID) of the user object in Azure AD B2C Premium</span></span> |
| <span data-ttu-id="b4188-134">*password*</span><span class="sxs-lookup"><span data-stu-id="b4188-134">*password*</span></span> | <span data-ttu-id="b4188-135">密碼</span><span class="sxs-lookup"><span data-stu-id="b4188-135">Password</span></span> |
| <span data-ttu-id="b4188-136">newPassword</span><span class="sxs-lookup"><span data-stu-id="b4188-136">*newPassword*</span></span> | |
| <span data-ttu-id="b4188-137">reenterPassword</span><span class="sxs-lookup"><span data-stu-id="b4188-137">*reenterPassword*</span></span> | |
| <span data-ttu-id="b4188-138">passwordPolicies</span><span class="sxs-lookup"><span data-stu-id="b4188-138">*passwordPolicies*</span></span> | <span data-ttu-id="b4188-139">Azure AD B2C 進階版用來決定密碼強度、到期日等規定的密碼原則。</span><span class="sxs-lookup"><span data-stu-id="b4188-139">Password policies used by Azure AD B2C Premium to determine password strength, expiry, etc.</span></span> |
| <span data-ttu-id="b4188-140">*sub*</span><span class="sxs-lookup"><span data-stu-id="b4188-140">*sub*</span></span> | |
| <span data-ttu-id="b4188-141">alternativeSecurityId</span><span class="sxs-lookup"><span data-stu-id="b4188-141">*alternativeSecurityId*</span></span> | |
| <span data-ttu-id="b4188-142">identityProvider</span><span class="sxs-lookup"><span data-stu-id="b4188-142">*identityProvider*</span></span> | |
| <span data-ttu-id="b4188-143">displayName</span><span class="sxs-lookup"><span data-stu-id="b4188-143">*displayName*</span></span> | |
| <span data-ttu-id="b4188-144">strongAuthenticationPhoneNumber</span><span class="sxs-lookup"><span data-stu-id="b4188-144">*strongAuthenticationPhoneNumber*</span></span> | <span data-ttu-id="b4188-145">使用者的電話號碼</span><span class="sxs-lookup"><span data-stu-id="b4188-145">User's telephone number</span></span> |
| <span data-ttu-id="b4188-146">Verified.strongAuthenticationPhoneNumber</span><span class="sxs-lookup"><span data-stu-id="b4188-146">*Verified.strongAuthenticationPhoneNumber*</span></span> | |
| <span data-ttu-id="b4188-147">email</span><span class="sxs-lookup"><span data-stu-id="b4188-147">*email*</span></span> | <span data-ttu-id="b4188-148">可用來連絡使用者的電子郵件地址</span><span class="sxs-lookup"><span data-stu-id="b4188-148">Email address that can be used to contact the user</span></span> |
| <span data-ttu-id="b4188-149">signInNamesInfo.emailAddress</span><span class="sxs-lookup"><span data-stu-id="b4188-149">*signInNamesInfo.emailAddress*</span></span> | <span data-ttu-id="b4188-150">使用者可用來登入的電子郵件地址</span><span class="sxs-lookup"><span data-stu-id="b4188-150">Email address that the user can use to sign in</span></span> |
| <span data-ttu-id="b4188-151">otherMails</span><span class="sxs-lookup"><span data-stu-id="b4188-151">*otherMails*</span></span> | <span data-ttu-id="b4188-152">可用來連絡使用者的電子郵件地址</span><span class="sxs-lookup"><span data-stu-id="b4188-152">Email addresses that can be used to contact the user</span></span> |
| <span data-ttu-id="b4188-153">userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="b4188-153">*userPrincipalName*</span></span> | <span data-ttu-id="b4188-154">Azure AD B2C 進階版中所儲存的使用者名稱</span><span class="sxs-lookup"><span data-stu-id="b4188-154">Username as stored in the Azure AD B2C Premium</span></span> |
| <span data-ttu-id="b4188-155">upnUserName</span><span class="sxs-lookup"><span data-stu-id="b4188-155">*upnUserName*</span></span> | <span data-ttu-id="b4188-156">用來建立使用者主體名稱的使用者名稱</span><span class="sxs-lookup"><span data-stu-id="b4188-156">Username for creating user principal name</span></span> |
| <span data-ttu-id="b4188-157">mailNickName</span><span class="sxs-lookup"><span data-stu-id="b4188-157">*mailNickName*</span></span> | <span data-ttu-id="b4188-158">Azure AD B2C 進階版中所儲存的使用者郵件別名</span><span class="sxs-lookup"><span data-stu-id="b4188-158">User's mail nick name as stored in the Azure AD B2C Premium</span></span> |
| <span data-ttu-id="b4188-159">newUser</span><span class="sxs-lookup"><span data-stu-id="b4188-159">*newUser*</span></span> | |
| <span data-ttu-id="b4188-160">executed-SelfAsserted-Input</span><span class="sxs-lookup"><span data-stu-id="b4188-160">*executed-SelfAsserted-Input*</span></span> | <span data-ttu-id="b4188-161">此宣告會指出屬性是否收集自使用者</span><span class="sxs-lookup"><span data-stu-id="b4188-161">Claim that specifies whether attributes were collected from the user</span></span> |
| <span data-ttu-id="b4188-162">executed-PhoneFactor-Input</span><span class="sxs-lookup"><span data-stu-id="b4188-162">*executed-PhoneFactor-Input*</span></span> | <span data-ttu-id="b4188-163">此宣告會指出新的電話號碼是否收集自使用者</span><span class="sxs-lookup"><span data-stu-id="b4188-163">Claim that specifies whether a new phone number was collected from the user</span></span> |
| <span data-ttu-id="b4188-164">authenticationSource</span><span class="sxs-lookup"><span data-stu-id="b4188-164">*authenticationSource*</span></span> | <span data-ttu-id="b4188-165">指出使用者是在社交識別提供者、login.microsoftonline.com 還是本機帳戶進行驗證的</span><span class="sxs-lookup"><span data-stu-id="b4188-165">Specifies whether the user was authenticated at Social Identity Provider, login.microsoftonline.com, or local account</span></span> |

### <a name="claims-required-for-query-string-parameters-and-other-special-parameters"></a><span data-ttu-id="b4188-166">查詢字串參數和其他特殊參數所需的宣告</span><span class="sxs-lookup"><span data-stu-id="b4188-166">Claims required for query string parameters and other special parameters</span></span>

<span data-ttu-id="b4188-167">必須有下列宣告才能將特殊參數 (包括某些查詢字串參數) 傳遞給其他宣告提供者︰</span><span class="sxs-lookup"><span data-stu-id="b4188-167">The following claims are required to pass on special parameters (including some query string parameters) to other claims providers:</span></span>

| <span data-ttu-id="b4188-168">宣告類型</span><span class="sxs-lookup"><span data-stu-id="b4188-168">Claims type</span></span> | <span data-ttu-id="b4188-169">說明</span><span class="sxs-lookup"><span data-stu-id="b4188-169">Description</span></span> |
|-------------|-------------|
| <span data-ttu-id="b4188-170">nux</span><span class="sxs-lookup"><span data-stu-id="b4188-170">*nux*</span></span> | <span data-ttu-id="b4188-171">傳遞給本機帳戶以向 login.microsoftonline.com 進行驗證的特殊參數</span><span class="sxs-lookup"><span data-stu-id="b4188-171">Special parameter passed for local account authentication to login.microsoftonline.com</span></span> |
| <span data-ttu-id="b4188-172">nca</span><span class="sxs-lookup"><span data-stu-id="b4188-172">*nca*</span></span> | <span data-ttu-id="b4188-173">傳遞給本機帳戶以向 login.microsoftonline.com 進行驗證的特殊參數</span><span class="sxs-lookup"><span data-stu-id="b4188-173">Special parameter passed for local account authentication to login.microsoftonline.com</span></span> |
| <span data-ttu-id="b4188-174">prompt</span><span class="sxs-lookup"><span data-stu-id="b4188-174">*prompt*</span></span> | <span data-ttu-id="b4188-175">傳遞給本機帳戶以向 login.microsoftonline.com 進行驗證的特殊參數</span><span class="sxs-lookup"><span data-stu-id="b4188-175">Special parameter passed for local account authentication to login.microsoftonline.com</span></span> |
| <span data-ttu-id="b4188-176">mkt</span><span class="sxs-lookup"><span data-stu-id="b4188-176">*mkt*</span></span> | <span data-ttu-id="b4188-177">傳遞給本機帳戶以向 login.microsoftonline.com 進行驗證的特殊參數</span><span class="sxs-lookup"><span data-stu-id="b4188-177">Special parameter passed for local account authentication to login.microsoftonline.com</span></span> |
| <span data-ttu-id="b4188-178">lc</span><span class="sxs-lookup"><span data-stu-id="b4188-178">*lc*</span></span> | <span data-ttu-id="b4188-179">傳遞給本機帳戶以向 login.microsoftonline.com 進行驗證的特殊參數</span><span class="sxs-lookup"><span data-stu-id="b4188-179">Special parameter passed for local account authentication to login.microsoftonline.com</span></span> |
| <span data-ttu-id="b4188-180">grant_type</span><span class="sxs-lookup"><span data-stu-id="b4188-180">*grant_type*</span></span> | <span data-ttu-id="b4188-181">傳遞給本機帳戶以向 login.microsoftonline.com 進行驗證的特殊參數</span><span class="sxs-lookup"><span data-stu-id="b4188-181">Special parameter passed for local account authentication to login.microsoftonline.com</span></span> |
| <span data-ttu-id="b4188-182">scope</span><span class="sxs-lookup"><span data-stu-id="b4188-182">*scope*</span></span> | <span data-ttu-id="b4188-183">傳遞給本機帳戶以向 login.microsoftonline.com 進行驗證的特殊參數</span><span class="sxs-lookup"><span data-stu-id="b4188-183">Special parameter passed for local account authentication to login.microsoftonline.com</span></span> |
| <span data-ttu-id="b4188-184">client_id</span><span class="sxs-lookup"><span data-stu-id="b4188-184">*client_id*</span></span> | <span data-ttu-id="b4188-185">傳遞給本機帳戶以向 login.microsoftonline.com 進行驗證的特殊參數</span><span class="sxs-lookup"><span data-stu-id="b4188-185">Special parameter passed for local account authentication to login.microsoftonline.com</span></span> |
| <span data-ttu-id="b4188-186">objectIdFromSession</span><span class="sxs-lookup"><span data-stu-id="b4188-186">*objectIdFromSession*</span></span> | <span data-ttu-id="b4188-187">預設工作階段管理提供者所提供的參數，用以指出物件識別碼是從 SSO 工作階段擷取來的</span><span class="sxs-lookup"><span data-stu-id="b4188-187">Parameter provided by the default session management provider to indicate that the object id has been retrieved from an SSO session</span></span> |
| <span data-ttu-id="b4188-188">isActiveMFASession</span><span class="sxs-lookup"><span data-stu-id="b4188-188">*isActiveMFASession*</span></span> | <span data-ttu-id="b4188-189">MFA 工作階段管理所提供的參數，用以指出使用者具有作用中的 MFA 工作階段</span><span class="sxs-lookup"><span data-stu-id="b4188-189">Parameter provided by the MFA session management to indicate that the user has an active MFA session</span></span> |

### <a name="additional-optional-claims-that-can-be-collected"></a><span data-ttu-id="b4188-190">其他可以收集的 (選擇性) 宣告</span><span class="sxs-lookup"><span data-stu-id="b4188-190">Additional (optional) claims that can be collected</span></span>

<span data-ttu-id="b4188-191">下列宣告是可以從使用者收集而來、儲存在目錄中，以及在權杖中傳送的其他宣告。</span><span class="sxs-lookup"><span data-stu-id="b4188-191">The following claims are additional claims that can be collected from the users, stored in the directory, and sent in the token.</span></span> <span data-ttu-id="b4188-192">如先前所述，您可以將其他宣告新增至此清單。</span><span class="sxs-lookup"><span data-stu-id="b4188-192">As outlined before, additional claims can be added to this list.</span></span>

| <span data-ttu-id="b4188-193">宣告類型</span><span class="sxs-lookup"><span data-stu-id="b4188-193">Claims type</span></span> | <span data-ttu-id="b4188-194">說明</span><span class="sxs-lookup"><span data-stu-id="b4188-194">Description</span></span> |
|-------------|-------------|
| <span data-ttu-id="b4188-195">givenName</span><span class="sxs-lookup"><span data-stu-id="b4188-195">*givenName*</span></span> | <span data-ttu-id="b4188-196">使用者的名字 (也就是第一個名字)</span><span class="sxs-lookup"><span data-stu-id="b4188-196">User's given name (also known as first name)</span></span> |
| <span data-ttu-id="b4188-197">surname</span><span class="sxs-lookup"><span data-stu-id="b4188-197">*surname*</span></span> | <span data-ttu-id="b4188-198">使用者的姓氏</span><span class="sxs-lookup"><span data-stu-id="b4188-198">User's surname (also known as family name or last name)</span></span> |
| <span data-ttu-id="b4188-199">Extension_picture</span><span class="sxs-lookup"><span data-stu-id="b4188-199">*Extension_picture*</span></span> | <span data-ttu-id="b4188-200">使用者的社交網站相片</span><span class="sxs-lookup"><span data-stu-id="b4188-200">User's picture from social</span></span> |

## <a name="claim-transformations"></a><span data-ttu-id="b4188-201">宣告轉換</span><span class="sxs-lookup"><span data-stu-id="b4188-201">Claim transformations</span></span>

<span data-ttu-id="b4188-202">以下列出可用的宣告轉換。</span><span class="sxs-lookup"><span data-stu-id="b4188-202">The available claim transformations are listed below.</span></span>

| <span data-ttu-id="b4188-203">宣告轉換</span><span class="sxs-lookup"><span data-stu-id="b4188-203">Claim transformation</span></span> | <span data-ttu-id="b4188-204">說明</span><span class="sxs-lookup"><span data-stu-id="b4188-204">Description</span></span> |
|----------------------|-------------|
| <span data-ttu-id="b4188-205">CreateOtherMailsFromEmail</span><span class="sxs-lookup"><span data-stu-id="b4188-205">*CreateOtherMailsFromEmail*</span></span> | |
| <span data-ttu-id="b4188-206">CreateRandomUPNUserName</span><span class="sxs-lookup"><span data-stu-id="b4188-206">*CreateRandomUPNUserName*</span></span> | |
| <span data-ttu-id="b4188-207">CreateUserPrincipalName</span><span class="sxs-lookup"><span data-stu-id="b4188-207">*CreateUserPrincipalName*</span></span> | |
| <span data-ttu-id="b4188-208">CreateSubjectClaimFromObjectID</span><span class="sxs-lookup"><span data-stu-id="b4188-208">*CreateSubjectClaimFromObjectID*</span></span> | |
| <span data-ttu-id="b4188-209">CreateSubjectClaimFromAlternativeSecurityId</span><span class="sxs-lookup"><span data-stu-id="b4188-209">*CreateSubjectClaimFromAlternativeSecurityId*</span></span> | |
| <span data-ttu-id="b4188-210">CreateAlternativeSecurityId</span><span class="sxs-lookup"><span data-stu-id="b4188-210">*CreateAlternativeSecurityId*</span></span> | |

## <a name="content-definitions"></a><span data-ttu-id="b4188-211">內容定義</span><span class="sxs-lookup"><span data-stu-id="b4188-211">Content definitions</span></span>

<span data-ttu-id="b4188-212">本節說明 B2C_1A_base 原則中已經宣告的內容定義。</span><span class="sxs-lookup"><span data-stu-id="b4188-212">This section describes the content definitions already declared in the *B2C_1A_base* policy.</span></span> <span data-ttu-id="b4188-213">您可以視需要輕易地在您自己的原則和 B2C_1A_base_extensions 原則中，參考、覆寫和/或擴充這些內容定義。</span><span class="sxs-lookup"><span data-stu-id="b4188-213">These content definitions are susceptible to be referenced, overridden, and/or extended as needed in your own policies as well as in the *B2C_1A_base_extensions* policy.</span></span>

| <span data-ttu-id="b4188-214">宣告提供者</span><span class="sxs-lookup"><span data-stu-id="b4188-214">Claims provider</span></span> | <span data-ttu-id="b4188-215">說明</span><span class="sxs-lookup"><span data-stu-id="b4188-215">Description</span></span> |
|-----------------|-------------|
| <span data-ttu-id="b4188-216">*Facebook*</span><span class="sxs-lookup"><span data-stu-id="b4188-216">*Facebook*</span></span> | |
| <span data-ttu-id="b4188-217">本機帳戶登入</span><span class="sxs-lookup"><span data-stu-id="b4188-217">*Local Account SignIn*</span></span> | |
| <span data-ttu-id="b4188-218">PhoneFactor</span><span class="sxs-lookup"><span data-stu-id="b4188-218">*PhoneFactor*</span></span> | |
| <span data-ttu-id="b4188-219">*Azure Active Directory*</span><span class="sxs-lookup"><span data-stu-id="b4188-219">*Azure Active Directory*</span></span> | |
| <span data-ttu-id="b4188-220">自我判斷提示</span><span class="sxs-lookup"><span data-stu-id="b4188-220">*Self Asserted*</span></span> | |
| <span data-ttu-id="b4188-221">本機帳戶</span><span class="sxs-lookup"><span data-stu-id="b4188-221">*Local Account*</span></span> | |
| <span data-ttu-id="b4188-222">*工作階段管理*</span><span class="sxs-lookup"><span data-stu-id="b4188-222">*Session Management*</span></span> | |
| <span data-ttu-id="b4188-223">Trustframework 原則引擎</span><span class="sxs-lookup"><span data-stu-id="b4188-223">*Trustframework Policy Engine*</span></span> | |
| <span data-ttu-id="b4188-224">TechnicalProfiles</span><span class="sxs-lookup"><span data-stu-id="b4188-224">*TechnicalProfiles*</span></span> | |
| <span data-ttu-id="b4188-225">權杖簽發者</span><span class="sxs-lookup"><span data-stu-id="b4188-225">*Token Issuer*</span></span> | |

## <a name="technical-profiles"></a><span data-ttu-id="b4188-226">技術設定檔</span><span class="sxs-lookup"><span data-stu-id="b4188-226">Technical profiles</span></span>

<span data-ttu-id="b4188-227">本節說明 B2C_1A_base 原則中每個宣告提供者已經宣告的技術設定檔。</span><span class="sxs-lookup"><span data-stu-id="b4188-227">This section depicts the technical profiles already declared per claim provider in the *B2C_1A_base* policy.</span></span> <span data-ttu-id="b4188-228">您可以視需要輕易地在您自己的原則和 B2C_1A_base_extensions 原則中，進一步參考、覆寫和/或擴充這些技術設定檔。</span><span class="sxs-lookup"><span data-stu-id="b4188-228">These technical profiles are susceptible to be further referenced, overridden, and/or extended as needed in your own policies as well as in the *B2C_1A_base_extensions* policy.</span></span>

### <a name="technical-profiles-for-facebook"></a><span data-ttu-id="b4188-229">Facebook 的技術設定檔</span><span class="sxs-lookup"><span data-stu-id="b4188-229">Technical profiles for Facebook</span></span>

| <span data-ttu-id="b4188-230">技術設定檔</span><span class="sxs-lookup"><span data-stu-id="b4188-230">Technical profile</span></span> | <span data-ttu-id="b4188-231">說明</span><span class="sxs-lookup"><span data-stu-id="b4188-231">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="b4188-232">Facebook-OAUTH</span><span class="sxs-lookup"><span data-stu-id="b4188-232">*Facebook-OAUTH*</span></span> | |

### <a name="technical-profiles-for-local-account-signin"></a><span data-ttu-id="b4188-233">本機帳戶登入的技術設定檔</span><span class="sxs-lookup"><span data-stu-id="b4188-233">Technical profiles for Local Account Signin</span></span>

| <span data-ttu-id="b4188-234">技術設定檔</span><span class="sxs-lookup"><span data-stu-id="b4188-234">Technical profile</span></span> | <span data-ttu-id="b4188-235">說明</span><span class="sxs-lookup"><span data-stu-id="b4188-235">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="b4188-236">Login-NonInteractive</span><span class="sxs-lookup"><span data-stu-id="b4188-236">*Login-NonInteractive*</span></span> | |

### <a name="technical-profiles-for-phone-factor"></a><span data-ttu-id="b4188-237">PhoneFactor 的技術設定檔</span><span class="sxs-lookup"><span data-stu-id="b4188-237">Technical profiles for Phone Factor</span></span>

| <span data-ttu-id="b4188-238">技術設定檔</span><span class="sxs-lookup"><span data-stu-id="b4188-238">Technical profile</span></span> | <span data-ttu-id="b4188-239">說明</span><span class="sxs-lookup"><span data-stu-id="b4188-239">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="b4188-240">PhoneFactor-Input</span><span class="sxs-lookup"><span data-stu-id="b4188-240">*PhoneFactor-Input*</span></span> | |
| <span data-ttu-id="b4188-241">PhoneFactor-InputOrVerify</span><span class="sxs-lookup"><span data-stu-id="b4188-241">*PhoneFactor-InputOrVerify*</span></span> | |
| <span data-ttu-id="b4188-242">PhoneFactor-Verify</span><span class="sxs-lookup"><span data-stu-id="b4188-242">*PhoneFactor-Verify*</span></span> | |

### <a name="technical-profiles-for-azure-active-directory"></a><span data-ttu-id="b4188-243">Azure Active Directory 的技術設定檔</span><span class="sxs-lookup"><span data-stu-id="b4188-243">Technical profiles for Azure Active Directory</span></span>

| <span data-ttu-id="b4188-244">技術設定檔</span><span class="sxs-lookup"><span data-stu-id="b4188-244">Technical profile</span></span> | <span data-ttu-id="b4188-245">說明</span><span class="sxs-lookup"><span data-stu-id="b4188-245">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="b4188-246">AAD-Common</span><span class="sxs-lookup"><span data-stu-id="b4188-246">*AAD-Common*</span></span> | <span data-ttu-id="b4188-247">其他 AAD-xxx 技術設定檔所包含的技術設定檔</span><span class="sxs-lookup"><span data-stu-id="b4188-247">Technical profile included by the other AAD-xxx technical profiles</span></span> |
| <span data-ttu-id="b4188-248">AAD-UserWriteUsingAlternativeSecurityId</span><span class="sxs-lookup"><span data-stu-id="b4188-248">*AAD-UserWriteUsingAlternativeSecurityId*</span></span> | <span data-ttu-id="b4188-249">社交登入的技術設定檔</span><span class="sxs-lookup"><span data-stu-id="b4188-249">Technical profile for social logins</span></span> |
| <span data-ttu-id="b4188-250">AAD-UserReadUsingAlternativeSecurityId</span><span class="sxs-lookup"><span data-stu-id="b4188-250">*AAD-UserReadUsingAlternativeSecurityId*</span></span> | <span data-ttu-id="b4188-251">社交登入的技術設定檔</span><span class="sxs-lookup"><span data-stu-id="b4188-251">Technical profile for social logins</span></span> |
| <span data-ttu-id="b4188-252">AAD-UserReadUsingAlternativeSecurityId-NoError</span><span class="sxs-lookup"><span data-stu-id="b4188-252">*AAD-UserReadUsingAlternativeSecurityId-NoError*</span></span> | <span data-ttu-id="b4188-253">社交登入的技術設定檔</span><span class="sxs-lookup"><span data-stu-id="b4188-253">Technical profile for social logins</span></span> |
| <span data-ttu-id="b4188-254">AAD-UserWritePasswordUsingLogonEmail</span><span class="sxs-lookup"><span data-stu-id="b4188-254">*AAD-UserWritePasswordUsingLogonEmail*</span></span> | <span data-ttu-id="b4188-255">本機帳戶的技術設定檔</span><span class="sxs-lookup"><span data-stu-id="b4188-255">Technical profile for local accounts</span></span> |
| <span data-ttu-id="b4188-256">AAD-UserReadUsingEmailAddress</span><span class="sxs-lookup"><span data-stu-id="b4188-256">*AAD-UserReadUsingEmailAddress*</span></span> | <span data-ttu-id="b4188-257">本機帳戶的技術設定檔</span><span class="sxs-lookup"><span data-stu-id="b4188-257">Technical profile for local accounts</span></span> |
| <span data-ttu-id="b4188-258">AAD-UserWriteProfileUsingObjectId</span><span class="sxs-lookup"><span data-stu-id="b4188-258">*AAD-UserWriteProfileUsingObjectId*</span></span> | <span data-ttu-id="b4188-259">可供使用 objectId 來更新使用者記錄的技術設定檔</span><span class="sxs-lookup"><span data-stu-id="b4188-259">Technical profile for updating user record using objectId</span></span> |
| <span data-ttu-id="b4188-260">AAD-UserWritePhoneNumberUsingObjectId</span><span class="sxs-lookup"><span data-stu-id="b4188-260">*AAD-UserWritePhoneNumberUsingObjectId*</span></span> | <span data-ttu-id="b4188-261">可供使用 objectId 來更新使用者記錄的技術設定檔</span><span class="sxs-lookup"><span data-stu-id="b4188-261">Technical profile for updating user record using objectId</span></span> |
| <span data-ttu-id="b4188-262">AAD-UserWritePasswordUsingObjectId</span><span class="sxs-lookup"><span data-stu-id="b4188-262">*AAD-UserWritePasswordUsingObjectId*</span></span> | <span data-ttu-id="b4188-263">可供使用 objectId 來更新使用者記錄的技術設定檔</span><span class="sxs-lookup"><span data-stu-id="b4188-263">Technical profile for updating user record using objectId</span></span> |
| <span data-ttu-id="b4188-264">AAD-UserReadUsingObjectId</span><span class="sxs-lookup"><span data-stu-id="b4188-264">*AAD-UserReadUsingObjectId*</span></span> | <span data-ttu-id="b4188-265">此技術設定檔可用來在驗證使用者後讀取資料</span><span class="sxs-lookup"><span data-stu-id="b4188-265">Technical profile is used to read data after user authenticates</span></span> |

### <a name="technical-profiles-for-self-asserted"></a><span data-ttu-id="b4188-266">自我判斷提示的技術設定檔</span><span class="sxs-lookup"><span data-stu-id="b4188-266">Technical profiles for Self Asserted</span></span>

| <span data-ttu-id="b4188-267">技術設定檔</span><span class="sxs-lookup"><span data-stu-id="b4188-267">Technical profile</span></span> | <span data-ttu-id="b4188-268">說明</span><span class="sxs-lookup"><span data-stu-id="b4188-268">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="b4188-269">SelfAsserted-Social</span><span class="sxs-lookup"><span data-stu-id="b4188-269">*SelfAsserted-Social*</span></span> | |
| <span data-ttu-id="b4188-270">SelfAsserted-ProfileUpdate</span><span class="sxs-lookup"><span data-stu-id="b4188-270">*SelfAsserted-ProfileUpdate*</span></span> | |

### <a name="technical-profiles-for-local-account"></a><span data-ttu-id="b4188-271">本機帳戶的技術設定檔</span><span class="sxs-lookup"><span data-stu-id="b4188-271">Technical profiles for Local Account</span></span>

| <span data-ttu-id="b4188-272">技術設定檔</span><span class="sxs-lookup"><span data-stu-id="b4188-272">Technical profile</span></span> | <span data-ttu-id="b4188-273">說明</span><span class="sxs-lookup"><span data-stu-id="b4188-273">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="b4188-274">LocalAccountSignUpWithLogonEmail</span><span class="sxs-lookup"><span data-stu-id="b4188-274">*LocalAccountSignUpWithLogonEmail*</span></span> | |

### <a name="technical-profiles-for-session-management"></a><span data-ttu-id="b4188-275">工作階段管理的技術設定檔</span><span class="sxs-lookup"><span data-stu-id="b4188-275">Technical profiles for Session Management</span></span>

| <span data-ttu-id="b4188-276">技術設定檔</span><span class="sxs-lookup"><span data-stu-id="b4188-276">Technical profile</span></span> | <span data-ttu-id="b4188-277">說明</span><span class="sxs-lookup"><span data-stu-id="b4188-277">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="b4188-278">SM-Noop</span><span class="sxs-lookup"><span data-stu-id="b4188-278">*SM-Noop*</span></span> | |
| <span data-ttu-id="b4188-279">SM-AAD</span><span class="sxs-lookup"><span data-stu-id="b4188-279">*SM-AAD*</span></span> | |
| <span data-ttu-id="b4188-280">SM-SocialSignup</span><span class="sxs-lookup"><span data-stu-id="b4188-280">*SM-SocialSignup*</span></span> | <span data-ttu-id="b4188-281">設定檔名稱將會用來區分註冊與登入的 AAD 工作階段</span><span class="sxs-lookup"><span data-stu-id="b4188-281">Profile name is being used to disambiguate AAD session between sign up and sign in</span></span> |
| <span data-ttu-id="b4188-282">SM-SocialLogin</span><span class="sxs-lookup"><span data-stu-id="b4188-282">*SM-SocialLogin*</span></span> | |
| <span data-ttu-id="b4188-283">SM-MFA</span><span class="sxs-lookup"><span data-stu-id="b4188-283">*SM-MFA*</span></span> | |

### <a name="technical-profiles-for-trustframework-policy-engine-technicalprofiles"></a><span data-ttu-id="b4188-284">Trustframework 原則引擎 TechnicalProfiles 的技術設定檔</span><span class="sxs-lookup"><span data-stu-id="b4188-284">Technical profiles for Trustframework Policy Engine TechnicalProfiles</span></span>

<span data-ttu-id="b4188-285">**Trustframework 原則引擎 TechnicalProfiles** 宣告提供者目前沒有已定義的技術設定檔。</span><span class="sxs-lookup"><span data-stu-id="b4188-285">Currently, no technical profiles are defined for the **Trustframework Policy Engine TechnicalProfiles** claims provider.</span></span>

### <a name="technical-profiles-for-token-issuer"></a><span data-ttu-id="b4188-286">權杖簽發者的技術設定檔</span><span class="sxs-lookup"><span data-stu-id="b4188-286">Technical profiles for Token Issuer</span></span>

| <span data-ttu-id="b4188-287">技術設定檔</span><span class="sxs-lookup"><span data-stu-id="b4188-287">Technical profile</span></span> | <span data-ttu-id="b4188-288">說明</span><span class="sxs-lookup"><span data-stu-id="b4188-288">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="b4188-289">JwtIssuer</span><span class="sxs-lookup"><span data-stu-id="b4188-289">*JwtIssuer*</span></span> | |

## <a name="user-journeys"></a><span data-ttu-id="b4188-290">使用者旅程</span><span class="sxs-lookup"><span data-stu-id="b4188-290">User journeys</span></span>

<span data-ttu-id="b4188-291">本節說明 B2C_1A_base 原則中已經宣告的使用者旅程。</span><span class="sxs-lookup"><span data-stu-id="b4188-291">This section depicts the user journeys already declared in the *B2C_1A_base* policy.</span></span> <span data-ttu-id="b4188-292">您可以視需要輕易地在您自己的原則和 B2C_1A_base_extensions 原則中，進一步參考、覆寫和/或擴充這些使用者旅程。</span><span class="sxs-lookup"><span data-stu-id="b4188-292">These user journeys are susceptible to be further referenced, overridden, and/or extended as needed in your own policies as well as in the *B2C_1A_base_extensions* policy.</span></span>

| <span data-ttu-id="b4188-293">使用者旅程</span><span class="sxs-lookup"><span data-stu-id="b4188-293">User journey</span></span> | <span data-ttu-id="b4188-294">說明</span><span class="sxs-lookup"><span data-stu-id="b4188-294">Description</span></span> |
|--------------|-------------|
| <span data-ttu-id="b4188-295">SignUp</span><span class="sxs-lookup"><span data-stu-id="b4188-295">*SignUp*</span></span> | |
| <span data-ttu-id="b4188-296">SignIn</span><span class="sxs-lookup"><span data-stu-id="b4188-296">*SignIn*</span></span> | |
| <span data-ttu-id="b4188-297">SignUpOrSignIn</span><span class="sxs-lookup"><span data-stu-id="b4188-297">*SignUpOrSignIn*</span></span> | |
| <span data-ttu-id="b4188-298">EditProfile</span><span class="sxs-lookup"><span data-stu-id="b4188-298">*EditProfile*</span></span> | |
| <span data-ttu-id="b4188-299">PasswordReset</span><span class="sxs-lookup"><span data-stu-id="b4188-299">*PasswordReset*</span></span> | |
