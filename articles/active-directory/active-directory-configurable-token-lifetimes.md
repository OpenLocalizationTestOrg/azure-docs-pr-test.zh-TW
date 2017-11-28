---
title: "Azure Active Directory 中可設定的權杖存留期 | Microsoft Docs"
description: "了解如何設定 Azure AD 所簽發的權杖存留期。"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 06f5b317-053e-44c3-aaaa-cf07d8692735
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: billmath
ms.custom: aaddev
ms.reviewer: anchitn
ms.openlocfilehash: d23721eba308096a05211eb6e26e1338a69cae0c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="configurable-token-lifetimes-in-azure-active-directory-public-preview"></a><span data-ttu-id="f469a-103">Azure Active Directory 中可設定的權杖存留期 (公開預覽版)</span><span class="sxs-lookup"><span data-stu-id="f469a-103">Configurable token lifetimes in Azure Active Directory (Public Preview)</span></span>
<span data-ttu-id="f469a-104">您可以指定 Azure Active Directory (Azure AD) 所簽發的權杖存留期。</span><span class="sxs-lookup"><span data-stu-id="f469a-104">You can specify the lifetime of a token issued by Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="f469a-105">不論是針對組織中所有的應用程式、針對多租用戶 (多組織) 應用程式，還是針對組織中特定的服務主體，都可以設定權杖存留期。</span><span class="sxs-lookup"><span data-stu-id="f469a-105">You can set token lifetimes for all apps in your organization, for a multi-tenant (multi-organization) application, or for a specific service principal in your organization.</span></span>

> [!NOTE]
> <span data-ttu-id="f469a-106">這項功能目前為公開預覽版。</span><span class="sxs-lookup"><span data-stu-id="f469a-106">This capability currently is in Public Preview.</span></span> <span data-ttu-id="f469a-107">您應做好將任何變更還原或移除的準備。</span><span class="sxs-lookup"><span data-stu-id="f469a-107">Be prepared to revert or remove any changes.</span></span> <span data-ttu-id="f469a-108">公用預覽版期間功能可用於任何 Azure Active Directory 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="f469a-108">The feature is available in any Azure Active Directory subscription during Public Preview.</span></span> <span data-ttu-id="f469a-109">不過，當功能正式推出時，功能的某些層面可能需要 [Azure Active Directory Premium](active-directory-get-started-premium.md) 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="f469a-109">However, when the feature becomes generally available, some aspects of the feature might require an [Azure Active Directory Premium](active-directory-get-started-premium.md) subscription.</span></span>
>
>

<span data-ttu-id="f469a-110">在 Azure AD 中，原則物件代表在組織中個別應用程式或所有應用程式上強制執行的一組規則。</span><span class="sxs-lookup"><span data-stu-id="f469a-110">In Azure AD, a policy object represents a set of rules that are enforced on individual applications or on all applications in an organization.</span></span> <span data-ttu-id="f469a-111">每個原則類型都具有包含一組屬性的獨特結構，這些屬性會套用至它們已被指派的物件。</span><span class="sxs-lookup"><span data-stu-id="f469a-111">Each policy type has a unique structure, with a set of properties that are applied to objects to which they are assigned.</span></span>

<span data-ttu-id="f469a-112">您可以為您的組織指定原則做為預設原則。</span><span class="sxs-lookup"><span data-stu-id="f469a-112">You can designate a policy as the default policy for your organization.</span></span> <span data-ttu-id="f469a-113">只要此原則不被優先順序更高的原則覆寫，就會套用至組織中的任何應用程式。</span><span class="sxs-lookup"><span data-stu-id="f469a-113">The policy is applied to any application in the organization, as long as it is not overridden by a policy with a higher priority.</span></span> <span data-ttu-id="f469a-114">您也可以將原則指派給特定應用程式。</span><span class="sxs-lookup"><span data-stu-id="f469a-114">You also can assign a policy to specific applications.</span></span> <span data-ttu-id="f469a-115">優先順序會因原則類型而異。</span><span class="sxs-lookup"><span data-stu-id="f469a-115">The order of priority varies by policy type.</span></span>


## <a name="token-types"></a><span data-ttu-id="f469a-116">權杖類型</span><span class="sxs-lookup"><span data-stu-id="f469a-116">Token types</span></span>

<span data-ttu-id="f469a-117">您可以針對重新整理權杖、存取權杖、工作階段權杖及識別碼權杖設定權杖存留期原則。</span><span class="sxs-lookup"><span data-stu-id="f469a-117">You can set token lifetime policies for refresh tokens, access tokens, session tokens, and ID tokens.</span></span>

### <a name="access-tokens"></a><span data-ttu-id="f469a-118">存取權杖</span><span class="sxs-lookup"><span data-stu-id="f469a-118">Access tokens</span></span>
<span data-ttu-id="f469a-119">用戶端會使用存取權杖來存取受保護的資源。</span><span class="sxs-lookup"><span data-stu-id="f469a-119">Clients use access tokens to access a protected resource.</span></span> <span data-ttu-id="f469a-120">存取權杖僅可用於特定使用者、用戶端及資源的組合。</span><span class="sxs-lookup"><span data-stu-id="f469a-120">An access token can be used only for a specific combination of user, client, and resource.</span></span> <span data-ttu-id="f469a-121">存取權杖是不可撤銷的，在到期之前都會一直有效。</span><span class="sxs-lookup"><span data-stu-id="f469a-121">Access tokens cannot be revoked and are valid until their expiry.</span></span> <span data-ttu-id="f469a-122">惡意執行者若已取得存取權杖，便可在權杖的存留期範圍內使用該權杖。</span><span class="sxs-lookup"><span data-stu-id="f469a-122">A malicious actor that has obtained an access token can use it for extent of its lifetime.</span></span> <span data-ttu-id="f469a-123">調整存取權杖存留期是在改進系統效能與增加用戶端在使用者帳戶停用後保留存取權的時間，這兩者之間所做的一項權衡取捨。</span><span class="sxs-lookup"><span data-stu-id="f469a-123">Adjusting the lifetime of an access token is a trade-off between improving system performance and increasing the amount of time that the client retains access after the user’s account is disabled.</span></span> <span data-ttu-id="f469a-124">系統效能的改進是藉由減少用戶端需要取得新存取權杖的次數來達成。</span><span class="sxs-lookup"><span data-stu-id="f469a-124">Improved system performance is achieved by reducing the number of times a client needs to acquire a fresh access token.</span></span>

### <a name="refresh-tokens"></a><span data-ttu-id="f469a-125">重新整理權杖</span><span class="sxs-lookup"><span data-stu-id="f469a-125">Refresh tokens</span></span>
<span data-ttu-id="f469a-126">當用戶端取得存取權杖來存取受保護的資源時，用戶端會同時收到重新整理權杖和存取權杖。</span><span class="sxs-lookup"><span data-stu-id="f469a-126">When a client acquires an access token to access a protected resource, the client receives both a refresh token and an access token.</span></span> <span data-ttu-id="f469a-127">當存取權杖到期時，可以使用重新整理權杖來取得一組新的存取/重新整理權杖。</span><span class="sxs-lookup"><span data-stu-id="f469a-127">The refresh token is used to obtain new access/refresh token pairs when the current access token expires.</span></span> <span data-ttu-id="f469a-128">重新整理權杖會繫結至使用者與用戶端組合。</span><span class="sxs-lookup"><span data-stu-id="f469a-128">A refresh token is bound to a combination of user and client.</span></span> <span data-ttu-id="f469a-129">重新整理權杖可予以撤銷，每次使用權杖時，會檢查權杖的有效性。</span><span class="sxs-lookup"><span data-stu-id="f469a-129">A refresh token can be revoked, and the token's validity is checked every time the token is used.</span></span>

<span data-ttu-id="f469a-130">區別機密用戶端與公開用戶端相當重要。</span><span class="sxs-lookup"><span data-stu-id="f469a-130">It's important to make a distinction between confidential clients and public clients.</span></span> <span data-ttu-id="f469a-131">如需不同類型用戶端的詳細資訊，請參閱 [RFC 6749](https://tools.ietf.org/html/rfc6749#section-2.1)。</span><span class="sxs-lookup"><span data-stu-id="f469a-131">For more information about different types of clients, see [RFC 6749](https://tools.ietf.org/html/rfc6749#section-2.1).</span></span>

#### <a name="token-lifetimes-with-confidential-client-refresh-tokens"></a><span data-ttu-id="f469a-132">具有機密用戶端重新整理權杖的權杖存留期</span><span class="sxs-lookup"><span data-stu-id="f469a-132">Token lifetimes with confidential client refresh tokens</span></span>
<span data-ttu-id="f469a-133">機密用戶端是可以安全地儲存用戶端密碼的應用程式。</span><span class="sxs-lookup"><span data-stu-id="f469a-133">Confidential clients are applications that can securely store a client password (secret).</span></span> <span data-ttu-id="f469a-134">它們可以證明要求是來自用戶端應用程式，而不是來自惡意的執行者。</span><span class="sxs-lookup"><span data-stu-id="f469a-134">They can prove that requests are coming from the client application and not from a malicious actor.</span></span> <span data-ttu-id="f469a-135">例如，Web 應用程式是機密用戶端，因為它可在 Web 伺服器上儲存用戶端密碼。</span><span class="sxs-lookup"><span data-stu-id="f469a-135">For example, a web app is a confidential client because it can store a client secret on the web server.</span></span> <span data-ttu-id="f469a-136">它不是公開的。</span><span class="sxs-lookup"><span data-stu-id="f469a-136">It is not exposed.</span></span> <span data-ttu-id="f469a-137">因為這些流程較安全，所以簽發給這些流程的重新整理權杖預設存留期為 `until-revoked`、無法使用原則來變更，而且將不會在自發性密碼重設中撤銷。</span><span class="sxs-lookup"><span data-stu-id="f469a-137">Because these flows are more secure, the default lifetimes of refresh tokens issued to these flows is `until-revoked`, cannot be changed by using policy, and will not be revoked on voluntary password resets.</span></span>

#### <a name="token-lifetimes-with-public-client-refresh-tokens"></a><span data-ttu-id="f469a-138">具有公開用戶端重新整理權杖的權杖存留期</span><span class="sxs-lookup"><span data-stu-id="f469a-138">Token lifetimes with public client refresh tokens</span></span>

<span data-ttu-id="f469a-139">公開用戶端無法安全地儲存用戶端密碼。</span><span class="sxs-lookup"><span data-stu-id="f469a-139">Public clients cannot securely store a client password (secret).</span></span> <span data-ttu-id="f469a-140">例如，iOS/Android 應用程式無法模糊來自資源擁有者的密碼，因此被視為公開用戶端。</span><span class="sxs-lookup"><span data-stu-id="f469a-140">For example, an iOS/Android app cannot obfuscate a secret from the resource owner, so it is considered a public client.</span></span> <span data-ttu-id="f469a-141">您可以在資源上設定原則，讓來自公開用戶端的重新整理權杖只要超過指定的期間，便無法取得一組新的存取/重新整理權杖。</span><span class="sxs-lookup"><span data-stu-id="f469a-141">You can set policies on resources to prevent refresh tokens from public clients older than a specified period from obtaining a new access/refresh token pair.</span></span> <span data-ttu-id="f469a-142">(若要這樣做，請使用「重新整理權杖最大閒置時間」屬性)。您也可以使用原則來設定期間，超過該期間就不會再接受重新整理權杖。</span><span class="sxs-lookup"><span data-stu-id="f469a-142">(To do this, use the Refresh Token Max Inactive Time property.) You also can use policies to set a period beyond which the refresh tokens are no longer accepted.</span></span> <span data-ttu-id="f469a-143">(若要這樣做，請使用「重新整理權杖最大壽命」屬性)。您可以調整重新整理權杖的存留期，以控制當使用者使用公開用戶端應用程式時，必須在何時及隔多久重新輸入一次認證，而不是以無訊息方式重新驗證。</span><span class="sxs-lookup"><span data-stu-id="f469a-143">(To do this, use the Refresh Token Max Age property.) You can adjust the lifetime of a refresh token to control when and how often the user is required to reenter credentials, instead of being silently reauthenticated, when using a public client application.</span></span>

### <a name="id-tokens"></a><span data-ttu-id="f469a-144">ID 權杖</span><span class="sxs-lookup"><span data-stu-id="f469a-144">ID tokens</span></span>
<span data-ttu-id="f469a-145">識別碼權杖會傳遞至網站與原生用戶端。</span><span class="sxs-lookup"><span data-stu-id="f469a-145">ID tokens are passed to websites and native clients.</span></span> <span data-ttu-id="f469a-146">識別碼權杖包含使用者的設定檔資訊。</span><span class="sxs-lookup"><span data-stu-id="f469a-146">ID tokens contain profile information about a user.</span></span> <span data-ttu-id="f469a-147">識別碼權杖會繫結至特定的使用者與用戶端組合。</span><span class="sxs-lookup"><span data-stu-id="f469a-147">An ID token is bound to a specific combination of user and client.</span></span> <span data-ttu-id="f469a-148">識別碼權杖在到期前都會被視為有效。</span><span class="sxs-lookup"><span data-stu-id="f469a-148">ID tokens are considered valid until their expiry.</span></span> <span data-ttu-id="f469a-149">通常，Web 應用程式會將應用程式中的使用者工作階段存留期，與針對該使用者簽發之識別碼權杖的存留期做比對。</span><span class="sxs-lookup"><span data-stu-id="f469a-149">Usually, a web application matches a user’s session lifetime in the application to the lifetime of the ID token issued for the user.</span></span> <span data-ttu-id="f469a-150">您可以調整識別碼權杖的存留期，以控制 Web 應用程式讓應用程式工作階段到期並要求使用者重新向 Azure AD 進行驗證 (以無訊息方式或以互動方式) 的頻率。</span><span class="sxs-lookup"><span data-stu-id="f469a-150">You can adjust the lifetime of an ID token to control how often the web application expires the application session, and how often it requires the user to be reauthenticated with Azure AD (either silently or interactively).</span></span>

### <a name="single-sign-on-session-tokens"></a><span data-ttu-id="f469a-151">單一登入工作階段權杖</span><span class="sxs-lookup"><span data-stu-id="f469a-151">Single sign-on session tokens</span></span>
<span data-ttu-id="f469a-152">當使用者向 Azure AD 進行驗證並勾選 [讓我保持登入] 核取方塊時，系統會在使用者的瀏覽器和 Azure AD 建立單一登入工作階段 (SSO)。</span><span class="sxs-lookup"><span data-stu-id="f469a-152">When a user authenticates with Azure AD and selects the **Keep me signed in** check box, a single sign-on session (SSO) is established with the user’s browser and Azure AD.</span></span> <span data-ttu-id="f469a-153">SSO 權杖 (採用 Cookie 的形式) 即代表此工作階段。</span><span class="sxs-lookup"><span data-stu-id="f469a-153">The SSO token, in the form of a cookie, represents this session.</span></span> <span data-ttu-id="f469a-154">請注意，SSO 工作階段權杖不會繫結至特定的資源/用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="f469a-154">Note that the SSO session token is not bound to a specific resource/client application.</span></span> <span data-ttu-id="f469a-155">SSO 工作階段權杖是可撤銷的，而每次使用這些權杖時，系統都會檢查其有效性。</span><span class="sxs-lookup"><span data-stu-id="f469a-155">SSO session tokens can be revoked, and their validity is checked every time they are used.</span></span>

<span data-ttu-id="f469a-156">Azure AD 會使用兩種 SSO 工作階段權杖︰持續性和非持續性。</span><span class="sxs-lookup"><span data-stu-id="f469a-156">Azure AD uses two kinds of SSO session tokens: persistent and nonpersistent.</span></span> <span data-ttu-id="f469a-157">持續性工作階段權杖是由瀏覽器儲存為持續性 Cookie。</span><span class="sxs-lookup"><span data-stu-id="f469a-157">Persistent session tokens are stored as persistent cookies by the browser.</span></span> <span data-ttu-id="f469a-158">非持續性工作階段權杖是儲存為工作階段 Cookie。</span><span class="sxs-lookup"><span data-stu-id="f469a-158">Nonpersistent session tokens are stored as session cookies.</span></span> <span data-ttu-id="f469a-159">(工作階段 Cookie 會在瀏覽器關閉時終結)。</span><span class="sxs-lookup"><span data-stu-id="f469a-159">(Session cookies are destroyed when the browser is closed.)</span></span>

<span data-ttu-id="f469a-160">非持續性工作階段權杖有 24 小時的存留期。</span><span class="sxs-lookup"><span data-stu-id="f469a-160">Nonpersistent session tokens have a lifetime of 24 hours.</span></span> <span data-ttu-id="f469a-161">持續性權杖有 180 天的存留期。</span><span class="sxs-lookup"><span data-stu-id="f469a-161">Persistent tokens have a lifetime of 180 days.</span></span> <span data-ttu-id="f469a-162">只要在 SSO 工作階段權杖的有效期內使用此權杖，有效期就會再延長 24 小時或 180 天，取決於權杖類型。</span><span class="sxs-lookup"><span data-stu-id="f469a-162">Any time an SSO session token is used within its validity period, the validity period is extended another 24 hours or 180 days, depending on the token type.</span></span> <span data-ttu-id="f469a-163">如果未在 SSO 工作階段權杖的有效期內使用此權杖，系統就會將其視為過期而不再接受它。</span><span class="sxs-lookup"><span data-stu-id="f469a-163">If an SSO session token is not used within its validity period, it is considered expired and is no longer accepted.</span></span>

<span data-ttu-id="f469a-164">您可以使用原則來設定第一個工作階段權杖簽發之後的時間，超出該時間就不會再接受工作階段權杖。</span><span class="sxs-lookup"><span data-stu-id="f469a-164">You can use a policy to set the time after the first session token was issued beyond which the session token is no longer accepted.</span></span> <span data-ttu-id="f469a-165">(若要這樣做，請使用「工作階段權杖最大壽命」屬性)。您可以調整工作階段權杖的存留期，以控制當使用者使用 Web 應用程式時，必須在何時及隔多久重新輸入一次認證，而不是以無訊息方式重新驗證。</span><span class="sxs-lookup"><span data-stu-id="f469a-165">(To do this, use the Session Token Max Age property.) You can adjust the lifetime of a session token to control when and how often a user is required to reenter credentials, instead of being silently authenticated, when using a web application.</span></span>

### <a name="token-lifetime-policy-properties"></a><span data-ttu-id="f469a-166">權杖存留期原則屬性</span><span class="sxs-lookup"><span data-stu-id="f469a-166">Token lifetime policy properties</span></span>
<span data-ttu-id="f469a-167">權杖存留期原則是一種包含權杖存留期規則的原則物件。</span><span class="sxs-lookup"><span data-stu-id="f469a-167">A token lifetime policy is a type of policy object that contains token lifetime rules.</span></span> <span data-ttu-id="f469a-168">使用原則的屬性來控制指定的權杖存留期。</span><span class="sxs-lookup"><span data-stu-id="f469a-168">Use the properties of the policy to control specified token lifetimes.</span></span> <span data-ttu-id="f469a-169">如果未設定任何原則，系統就會強制執行預設存留期值。</span><span class="sxs-lookup"><span data-stu-id="f469a-169">If no policy is set, the system enforces the default lifetime value.</span></span>

### <a name="configurable-token-lifetime-properties"></a><span data-ttu-id="f469a-170">可設定的權杖存留期屬性</span><span class="sxs-lookup"><span data-stu-id="f469a-170">Configurable token lifetime properties</span></span>
| <span data-ttu-id="f469a-171">屬性</span><span class="sxs-lookup"><span data-stu-id="f469a-171">Property</span></span> | <span data-ttu-id="f469a-172">原則屬性字串</span><span class="sxs-lookup"><span data-stu-id="f469a-172">Policy property string</span></span> | <span data-ttu-id="f469a-173">影響</span><span class="sxs-lookup"><span data-stu-id="f469a-173">Affects</span></span> | <span data-ttu-id="f469a-174">預設值</span><span class="sxs-lookup"><span data-stu-id="f469a-174">Default</span></span> | <span data-ttu-id="f469a-175">最小值</span><span class="sxs-lookup"><span data-stu-id="f469a-175">Minimum</span></span> | <span data-ttu-id="f469a-176">最大值</span><span class="sxs-lookup"><span data-stu-id="f469a-176">Maximum</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="f469a-177">存取權杖存留期</span><span class="sxs-lookup"><span data-stu-id="f469a-177">Access Token Lifetime</span></span> |<span data-ttu-id="f469a-178">AccessTokenLifetime</span><span class="sxs-lookup"><span data-stu-id="f469a-178">AccessTokenLifetime</span></span> |<span data-ttu-id="f469a-179">存取權杖、識別碼權杖、SAML2 權杖</span><span class="sxs-lookup"><span data-stu-id="f469a-179">Access tokens, ID tokens, SAML2 tokens</span></span> |<span data-ttu-id="f469a-180">1 小時</span><span class="sxs-lookup"><span data-stu-id="f469a-180">1 hour</span></span> |<span data-ttu-id="f469a-181">10 分鐘</span><span class="sxs-lookup"><span data-stu-id="f469a-181">10 minutes</span></span> |<span data-ttu-id="f469a-182">1 天</span><span class="sxs-lookup"><span data-stu-id="f469a-182">1 day</span></span> |
| <span data-ttu-id="f469a-183">重新整理權杖最大閒置時間</span><span class="sxs-lookup"><span data-stu-id="f469a-183">Refresh Token Max Inactive Time</span></span> |<span data-ttu-id="f469a-184">MaxInactiveTime</span><span class="sxs-lookup"><span data-stu-id="f469a-184">MaxInactiveTime</span></span> |<span data-ttu-id="f469a-185">重新整理權杖</span><span class="sxs-lookup"><span data-stu-id="f469a-185">Refresh tokens</span></span> |<span data-ttu-id="f469a-186">14 天</span><span class="sxs-lookup"><span data-stu-id="f469a-186">14 days</span></span> |<span data-ttu-id="f469a-187">10 分鐘</span><span class="sxs-lookup"><span data-stu-id="f469a-187">10 minutes</span></span> |<span data-ttu-id="f469a-188">90 天</span><span class="sxs-lookup"><span data-stu-id="f469a-188">90 days</span></span> |
| <span data-ttu-id="f469a-189">單一要素重新整理權杖最大壽命</span><span class="sxs-lookup"><span data-stu-id="f469a-189">Single-Factor Refresh Token Max Age</span></span> |<span data-ttu-id="f469a-190">MaxAgeSingleFactor</span><span class="sxs-lookup"><span data-stu-id="f469a-190">MaxAgeSingleFactor</span></span> |<span data-ttu-id="f469a-191">重新整理權杖 (適用於任何使用者)</span><span class="sxs-lookup"><span data-stu-id="f469a-191">Refresh tokens (for any users)</span></span> |<span data-ttu-id="f469a-192">直到撤銷為止</span><span class="sxs-lookup"><span data-stu-id="f469a-192">Until-revoked</span></span> |<span data-ttu-id="f469a-193">10 分鐘</span><span class="sxs-lookup"><span data-stu-id="f469a-193">10 minutes</span></span> |<span data-ttu-id="f469a-194">直到撤銷為止<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="f469a-194">Until-revoked<sup>1</sup></span></span> |
| <span data-ttu-id="f469a-195">多重要素重新整理權杖最大壽命</span><span class="sxs-lookup"><span data-stu-id="f469a-195">Multi-Factor Refresh Token Max Age</span></span> |<span data-ttu-id="f469a-196">MaxAgeMultiFactor</span><span class="sxs-lookup"><span data-stu-id="f469a-196">MaxAgeMultiFactor</span></span> |<span data-ttu-id="f469a-197">重新整理權杖 (適用於任何使用者)</span><span class="sxs-lookup"><span data-stu-id="f469a-197">Refresh tokens (for any users)</span></span> |<span data-ttu-id="f469a-198">直到撤銷為止</span><span class="sxs-lookup"><span data-stu-id="f469a-198">Until-revoked</span></span> |<span data-ttu-id="f469a-199">10 分鐘</span><span class="sxs-lookup"><span data-stu-id="f469a-199">10 minutes</span></span> |<span data-ttu-id="f469a-200">直到撤銷為止<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="f469a-200">Until-revoked<sup>1</sup></span></span> |
| <span data-ttu-id="f469a-201">單一要素工作階段權杖最大壽命</span><span class="sxs-lookup"><span data-stu-id="f469a-201">Single-Factor Session Token Max Age</span></span> |<span data-ttu-id="f469a-202">MaxAgeSessionSingleFactor<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="f469a-202">MaxAgeSessionSingleFactor<sup>2</sup></span></span> |<span data-ttu-id="f469a-203">工作階段權杖 (持續性和非持續性)</span><span class="sxs-lookup"><span data-stu-id="f469a-203">Session tokens (persistent and nonpersistent)</span></span> |<span data-ttu-id="f469a-204">直到撤銷為止</span><span class="sxs-lookup"><span data-stu-id="f469a-204">Until-revoked</span></span> |<span data-ttu-id="f469a-205">10 分鐘</span><span class="sxs-lookup"><span data-stu-id="f469a-205">10 minutes</span></span> |<span data-ttu-id="f469a-206">直到撤銷為止<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="f469a-206">Until-revoked<sup>1</sup></span></span> |
| <span data-ttu-id="f469a-207">多重要素工作階段權杖最大壽命</span><span class="sxs-lookup"><span data-stu-id="f469a-207">Multi-Factor Session Token Max Age</span></span> |<span data-ttu-id="f469a-208">MaxAgeSessionMultiFactor<sup>3</sup></span><span class="sxs-lookup"><span data-stu-id="f469a-208">MaxAgeSessionMultiFactor<sup>3</sup></span></span> |<span data-ttu-id="f469a-209">工作階段權杖 (持續性和非持續性)</span><span class="sxs-lookup"><span data-stu-id="f469a-209">Session tokens (persistent and nonpersistent)</span></span> |<span data-ttu-id="f469a-210">直到撤銷為止</span><span class="sxs-lookup"><span data-stu-id="f469a-210">Until-revoked</span></span> |<span data-ttu-id="f469a-211">10 分鐘</span><span class="sxs-lookup"><span data-stu-id="f469a-211">10 minutes</span></span> |<span data-ttu-id="f469a-212">直到撤銷為止<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="f469a-212">Until-revoked<sup>1</sup></span></span> |

* <span data-ttu-id="f469a-213"><sup>1</sup>針對這些屬性，可設定的明確時間長度上限為 365 天。</span><span class="sxs-lookup"><span data-stu-id="f469a-213"><sup>1</sup>365 days is the maximum explicit length that can be set for these attributes.</span></span>
* <span data-ttu-id="f469a-214"><sup>2</sup>如果未設定 **MaxAgeSessionSingleFactor**，則此值會採用 **MaxAgeSingleFactor** 值。</span><span class="sxs-lookup"><span data-stu-id="f469a-214"><sup>2</sup>If  **MaxAgeSessionSingleFactor** is not set, this value takes the **MaxAgeSingleFactor** value.</span></span> <span data-ttu-id="f469a-215">如果兩個參數都未設定，此屬性就會接受預設值 (即直到撤銷為止)。</span><span class="sxs-lookup"><span data-stu-id="f469a-215">If neither parameter is set, the property takes the default value (until-revoked).</span></span>
* <span data-ttu-id="f469a-216"><sup>3</sup>如果未設定 **MaxAgeSessionMultiFactor**，則此值會採用 **MaxAgeMultiFactor** 值。</span><span class="sxs-lookup"><span data-stu-id="f469a-216"><sup>3</sup>If  **MaxAgeSessionMultiFactor** is not set, this value takes the **MaxAgeMultiFactor** value.</span></span> <span data-ttu-id="f469a-217">如果兩個參數都未設定，此屬性就會接受預設值 (即直到撤銷為止)。</span><span class="sxs-lookup"><span data-stu-id="f469a-217">If neither parameter is set, the property takes the default value (until-revoked).</span></span>

### <a name="exceptions"></a><span data-ttu-id="f469a-218">例外狀況</span><span class="sxs-lookup"><span data-stu-id="f469a-218">Exceptions</span></span>
| <span data-ttu-id="f469a-219">屬性</span><span class="sxs-lookup"><span data-stu-id="f469a-219">Property</span></span> | <span data-ttu-id="f469a-220">影響</span><span class="sxs-lookup"><span data-stu-id="f469a-220">Affects</span></span> | <span data-ttu-id="f469a-221">預設值</span><span class="sxs-lookup"><span data-stu-id="f469a-221">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f469a-222">重新整理權杖最大壽命 (針對沒有足夠撤銷資訊的同盟使用者簽發<sup>1</sup>)</span><span class="sxs-lookup"><span data-stu-id="f469a-222">Refresh Token Max Age (issued for federated users who have insufficient revocation information<sup>1</sup>)</span></span> |<span data-ttu-id="f469a-223">重新整理權杖 (針對沒有足夠撤銷資訊的同盟使用者簽發<sup>1</sup>)</span><span class="sxs-lookup"><span data-stu-id="f469a-223">Refresh tokens (issued for federated users who have insufficient revocation information<sup>1</sup>)</span></span> |<span data-ttu-id="f469a-224">12 小時</span><span class="sxs-lookup"><span data-stu-id="f469a-224">12 hours</span></span> |
| <span data-ttu-id="f469a-225">重新整理權杖最大閒置時間 (針對機密用戶端簽發)</span><span class="sxs-lookup"><span data-stu-id="f469a-225">Refresh Token Max Inactive Time (issued for confidential clients)</span></span> |<span data-ttu-id="f469a-226">重新整理權杖 (針對機密用戶端簽發)</span><span class="sxs-lookup"><span data-stu-id="f469a-226">Refresh tokens (issued for confidential clients)</span></span> |<span data-ttu-id="f469a-227">90 天</span><span class="sxs-lookup"><span data-stu-id="f469a-227">90 days</span></span> |
| <span data-ttu-id="f469a-228">重新整理權杖最大壽命 (針對機密用戶端簽發)</span><span class="sxs-lookup"><span data-stu-id="f469a-228">Refresh Token Max Age (issued for confidential clients)</span></span> |<span data-ttu-id="f469a-229">重新整理權杖 (針對機密用戶端簽發)</span><span class="sxs-lookup"><span data-stu-id="f469a-229">Refresh tokens (issued for confidential clients)</span></span> |<span data-ttu-id="f469a-230">直到撤銷為止</span><span class="sxs-lookup"><span data-stu-id="f469a-230">Until-revoked</span></span> |

* <span data-ttu-id="f469a-231"><sup>1</sup>沒有足夠撤銷資訊的同盟使用者包括任何未同步 "LastPasswordChangeTimestamp" 屬性的使用者。</span><span class="sxs-lookup"><span data-stu-id="f469a-231"><sup>1</sup>Federated users who have insufficient revocation information include any users who do not have the "LastPasswordChangeTimestamp" attribute synced.</span></span> <span data-ttu-id="f469a-232">這些使用者只有這個很短的「最大壽命」，因為 AAD 無法確認何時該撤銷繫結至舊認證的權杖 (例如已變更的密碼)，所以必須更頻繁地回頭檢查，以確定使用者和相關聯的權杖仍然有效。</span><span class="sxs-lookup"><span data-stu-id="f469a-232">These users are given this short Max Age because AAD is unable to verify when to revoke tokens that are tied to an old credential (such as a password that has been changed) and must check back in more frequently to ensure that the user and associated tokens are still in good standing.</span></span> <span data-ttu-id="f469a-233">若要改善這項體驗，租用戶管理員必須確定他們已同步 "LastPasswordChangeTimestamp" 屬性 (這可以使用 Powershell 或透過 AADSync 在使用者物件上設定)。</span><span class="sxs-lookup"><span data-stu-id="f469a-233">To improve this experience, tenant admins must ensure that they are syncing the “LastPasswordChangeTimestamp” attribute (this can be set on the user object using Powershell or through AADSync).</span></span>

### <a name="policy-evaluation-and-prioritization"></a><span data-ttu-id="f469a-234">原則評估及優先順序</span><span class="sxs-lookup"><span data-stu-id="f469a-234">Policy evaluation and prioritization</span></span>
<span data-ttu-id="f469a-235">您可以建立權杖存留期原則然後將其指派給特定的應用程式、您的組織和服務主體。</span><span class="sxs-lookup"><span data-stu-id="f469a-235">You can create and then assign a token lifetime policy to a specific application, to your organization, and to service principals.</span></span> <span data-ttu-id="f469a-236">多個原則可以套用至特定應用程式。</span><span class="sxs-lookup"><span data-stu-id="f469a-236">Multiple policies might apply to a specific application.</span></span> <span data-ttu-id="f469a-237">生效的權杖存留期原則會遵循下列規則：</span><span class="sxs-lookup"><span data-stu-id="f469a-237">The token lifetime policy that takes effect follows these rules:</span></span>

* <span data-ttu-id="f469a-238">如果已將原則明確指派給服務主體，就會強制執行該原則。</span><span class="sxs-lookup"><span data-stu-id="f469a-238">If a policy is explicitly assigned to the service principal, it is enforced.</span></span>
* <span data-ttu-id="f469a-239">如果未將任何原則明確指派給服務主體，則會強制執行指派給該服務主體之父組織的原則。</span><span class="sxs-lookup"><span data-stu-id="f469a-239">If no policy is explicitly assigned to the service principal, a policy explicitly assigned to the parent organization of the service principal is enforced.</span></span>
* <span data-ttu-id="f469a-240">如果未將任何原則明確指派給服務主體或組織，則會強制執行指派給應用程式的原則。</span><span class="sxs-lookup"><span data-stu-id="f469a-240">If no policy is explicitly assigned to the service principal or to the organization, the policy assigned to the application is enforced.</span></span>
* <span data-ttu-id="f469a-241">如果未將任何原則明確指派給服務主體、組織或應用程式物件，將會強制執行預設值。</span><span class="sxs-lookup"><span data-stu-id="f469a-241">If no policy has been assigned to the service principal, the organization, or the application object, the default values is enforced.</span></span> <span data-ttu-id="f469a-242">(請參閱[可設定的權杖存留期屬性](#configurable-token-lifetime-properties)中的表格。)</span><span class="sxs-lookup"><span data-stu-id="f469a-242">(See the table in [Configurable token lifetime properties](#configurable-token-lifetime-properties).)</span></span>

<span data-ttu-id="f469a-243">如需有關應用程式物件與服務主體物件之間關係的詳細資訊，請參閱 [Azure Active Directory 中的應用程式和服務主體物件](active-directory-application-objects.md)。</span><span class="sxs-lookup"><span data-stu-id="f469a-243">For more information about the relationship between application objects and service principal objects, see [Application and service principal objects in Azure Active Directory](active-directory-application-objects.md).</span></span>

<span data-ttu-id="f469a-244">使用權杖時，系統便會評估權杖的有效性。</span><span class="sxs-lookup"><span data-stu-id="f469a-244">A token’s validity is evaluated at the time the token is used.</span></span> <span data-ttu-id="f469a-245">在所要存取之應用程式上優先順序最高的原則會生效。</span><span class="sxs-lookup"><span data-stu-id="f469a-245">The policy with the highest priority on the application that is being accessed takes effect.</span></span>

> [!NOTE]
> <span data-ttu-id="f469a-246">以下是範例案例。</span><span class="sxs-lookup"><span data-stu-id="f469a-246">Here's an example scenario.</span></span>
>
> <span data-ttu-id="f469a-247">使用者想要存取兩個 Web 應用程式︰Web 應用程式 A 和 Web 應用程式 B。</span><span class="sxs-lookup"><span data-stu-id="f469a-247">A user wants to access two web applications: Web Application A and Web Application B.</span></span>
> 
> <span data-ttu-id="f469a-248">因素：</span><span class="sxs-lookup"><span data-stu-id="f469a-248">Factors:</span></span>
> * <span data-ttu-id="f469a-249">兩個 Web 應用程式都在相同的父組織中。</span><span class="sxs-lookup"><span data-stu-id="f469a-249">Both web applications are in the same parent organization.</span></span>
> * <span data-ttu-id="f469a-250">「工作階段權杖最大壽命」為 8 小時的權杖存留期原則 1 已設定為父組織的預設值。</span><span class="sxs-lookup"><span data-stu-id="f469a-250">Token Lifetime Policy 1 with a Session Token Max Age of eight hours is set as the parent organization’s default.</span></span>
> * <span data-ttu-id="f469a-251">Web 應用程式 A 是一個一般用途 Web 應用程式且未與任何原則連結。</span><span class="sxs-lookup"><span data-stu-id="f469a-251">Web Application A is a regular-use web application and isn’t linked to any policies.</span></span>
> * <span data-ttu-id="f469a-252">Web 應用程式 B 適用於高度機密的程序。</span><span class="sxs-lookup"><span data-stu-id="f469a-252">Web Application B is used for highly sensitive processes.</span></span> <span data-ttu-id="f469a-253">其服務主體會連結至權杖存留期原則 2，其「工作階段權杖最大壽命」為 30 分鐘。</span><span class="sxs-lookup"><span data-stu-id="f469a-253">Its service principal is linked to Token Lifetime Policy 2, which has a Session Token Max Age of 30 minutes.</span></span>
>
> <span data-ttu-id="f469a-254">在下午 12:00，使用者啟動新的瀏覽器工作階段並嘗試存取 Web 應用程式 A。系統會將使用者重新導向到 Azure AD 並要求使用者登入。</span><span class="sxs-lookup"><span data-stu-id="f469a-254">At 12:00 PM, the user starts a new browser session and tries to access Web Application A. The user is redirected to Azure AD and is asked to sign in.</span></span> <span data-ttu-id="f469a-255">這會在瀏覽器中建立一個帶有工作階段權杖的 Cookie。</span><span class="sxs-lookup"><span data-stu-id="f469a-255">This creates a cookie that has a session token in the browser.</span></span> <span data-ttu-id="f469a-256">系統會將使用者重新導向回 Web 應用程式 A，其中會提供一個可讓使用者存取該應用程式的識別碼權杖。</span><span class="sxs-lookup"><span data-stu-id="f469a-256">The user is redirected back to Web Application A with an ID token that allows the user to access the application.</span></span>
>
> <span data-ttu-id="f469a-257">接著，在下午 12:15，使用者嘗試存取 Web 應用程式 B。瀏覽器會重新導向到 Azure AD 來偵測工作階段 Cookie。</span><span class="sxs-lookup"><span data-stu-id="f469a-257">At 12:15 PM, the user tries to access Web Application B. The browser redirects to Azure AD, which detects the session cookie.</span></span> <span data-ttu-id="f469a-258">Web 應用程式 B 的服務主體會與權杖存留期原則 2 連結，但同時也是帶有預設權杖存留期原則 1 之父組織的一部分。</span><span class="sxs-lookup"><span data-stu-id="f469a-258">Web Application B’s service principal is linked to Token Lifetime Policy 2, but it's also part of the parent organization, with default Token Lifetime Policy 1.</span></span> <span data-ttu-id="f469a-259">權杖存留期原則 2 會生效，因為與服務主體連結之原則的優先順序高於組織預設原則。</span><span class="sxs-lookup"><span data-stu-id="f469a-259">Token Lifetime Policy 2 takes effect because policies linked to service principals have a higher priority than organization default policies.</span></span> <span data-ttu-id="f469a-260">工作階段權杖原先是在過去 30 分鐘內簽發的，因此被視為有效。</span><span class="sxs-lookup"><span data-stu-id="f469a-260">The session token was originally issued within the last 30 minutes, so it is considered valid.</span></span> <span data-ttu-id="f469a-261">系統會將使用者重新導向回 Web 應用程式 B，其中會提供一個授與使用者存取權的識別碼權杖。</span><span class="sxs-lookup"><span data-stu-id="f469a-261">The user is redirected back to Web Application B with an ID token that grants them access.</span></span>
>
> <span data-ttu-id="f469a-262">在下午 1:00，使用者嘗試存取 Web 應用程式 A。系統會將使用者重新導向到 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="f469a-262">At 1:00 PM, the user tries to access Web Application A. The user is redirected to Azure AD.</span></span> <span data-ttu-id="f469a-263">Web 應用程式 A 並未與任何原則連結，但由於它位於帶有預設權杖存留期原則 1 的組織中，因此該原則會生效。</span><span class="sxs-lookup"><span data-stu-id="f469a-263">Web Application A is not linked to any policies, but because it is in an organization with default Token Lifetime Policy 1, that policy takes effect.</span></span> <span data-ttu-id="f469a-264">偵測到原先在過去八小時內簽發的工作階段 Cookie。</span><span class="sxs-lookup"><span data-stu-id="f469a-264">The session cookie that was originally issued within the last eight hours is detected.</span></span> <span data-ttu-id="f469a-265">系統會以無訊息模式將使用者重新導向回具有新識別碼權杖的 Web 應用程式 A。</span><span class="sxs-lookup"><span data-stu-id="f469a-265">The user is silently redirected back to Web Application A with a new ID token.</span></span> <span data-ttu-id="f469a-266">使用者不需要驗證。</span><span class="sxs-lookup"><span data-stu-id="f469a-266">The user is not required to authenticate.</span></span>
>
> <span data-ttu-id="f469a-267">使用者立即嘗試存取 Web 應用程式 B。系統會將使用者重新導向到 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="f469a-267">Immediately afterward, the user tries to access Web Application B. The user is redirected to Azure AD.</span></span> <span data-ttu-id="f469a-268">與先前一樣，權杖存留期原則 2 會生效。</span><span class="sxs-lookup"><span data-stu-id="f469a-268">As before, Token Lifetime Policy 2 takes effect.</span></span> <span data-ttu-id="f469a-269">因為權杖已簽發 30 分鐘以上，系統會提示使用者重新輸入其登入認證。</span><span class="sxs-lookup"><span data-stu-id="f469a-269">Because the token was issued more than 30 minutes ago, the user is prompted to reenter their sign-in credentials.</span></span> <span data-ttu-id="f469a-270">會簽發全新的工作階段權杖和識別碼權杖。</span><span class="sxs-lookup"><span data-stu-id="f469a-270">A brand-new session token and ID token are issued.</span></span> <span data-ttu-id="f469a-271">接著，使用者便可存取 Web 應用程式 B。</span><span class="sxs-lookup"><span data-stu-id="f469a-271">The user can then access Web Application B.</span></span>
>
>

## <a name="configurable-policy-property-details"></a><span data-ttu-id="f469a-272">可設定的原則屬性詳細資料</span><span class="sxs-lookup"><span data-stu-id="f469a-272">Configurable policy property details</span></span>
### <a name="access-token-lifetime"></a><span data-ttu-id="f469a-273">存取權杖存留期</span><span class="sxs-lookup"><span data-stu-id="f469a-273">Access Token Lifetime</span></span>
<span data-ttu-id="f469a-274">**字串：**AccessTokenLifetime</span><span class="sxs-lookup"><span data-stu-id="f469a-274">**String:** AccessTokenLifetime</span></span>

<span data-ttu-id="f469a-275">**影像：**存取權杖、識別碼權杖</span><span class="sxs-lookup"><span data-stu-id="f469a-275">**Affects:** Access tokens, ID tokens</span></span>

<span data-ttu-id="f469a-276">**摘要：**此原則可控制將此資源的存取權杖和識別碼權杖視為有效的期限。</span><span class="sxs-lookup"><span data-stu-id="f469a-276">**Summary:** This policy controls how long access and ID tokens for this resource are considered valid.</span></span> <span data-ttu-id="f469a-277">減少存取權杖存留期屬性可減輕存取權杖或識別碼權杖被惡意執行者長時間使用的風險。</span><span class="sxs-lookup"><span data-stu-id="f469a-277">Reducing the Access Token Lifetime property mitigates the risk of an access token or ID token being used by a malicious actor for an extended period of time.</span></span> <span data-ttu-id="f469a-278">(無法撤銷這些權杖。)缺點是效能會受到負面影響，因為需要更常取代權杖。</span><span class="sxs-lookup"><span data-stu-id="f469a-278">(These tokens cannot be revoked.) The trade-off is that performance is adversely affected, because the tokens have to be replaced more often.</span></span>

### <a name="refresh-token-max-inactive-time"></a><span data-ttu-id="f469a-279">重新整理權杖最大閒置時間</span><span class="sxs-lookup"><span data-stu-id="f469a-279">Refresh Token Max Inactive Time</span></span>
<span data-ttu-id="f469a-280">**字串︰**MaxInactiveTime</span><span class="sxs-lookup"><span data-stu-id="f469a-280">**String:** MaxInactiveTime</span></span>

<span data-ttu-id="f469a-281">**影響：**重新整理權杖</span><span class="sxs-lookup"><span data-stu-id="f469a-281">**Affects:** Refresh tokens</span></span>

<span data-ttu-id="f469a-282">**摘要：**此原則可控制在簽發重新整理權杖多久之後，用戶端才不能在嘗試存取此資源時，再使用該權杖來擷取一組新的存取權杖/重新整理權杖。</span><span class="sxs-lookup"><span data-stu-id="f469a-282">**Summary:** This policy controls how old a refresh token can be before a client can no longer use it to retrieve a new access/refresh token pair when attempting to access this resource.</span></span> <span data-ttu-id="f469a-283">因為使用重新整理權杖時通常會傳回一個新的重新整理權杖，因此，如果用戶端在指定時間期間使用目前重新整理權杖，嘗試存取任何資源，這個原則會阻止存取。</span><span class="sxs-lookup"><span data-stu-id="f469a-283">Because a new refresh token usually is returned when a refresh token is used, this policy prevents access if the client tries to access any resource by using the current refresh token during the specified period of time.</span></span>

<span data-ttu-id="f469a-284">此原則會強制尚未在其用戶端上變成作用中的使用者必須重新驗證，才能擷取新的重新整理權杖。</span><span class="sxs-lookup"><span data-stu-id="f469a-284">This policy forces users who have not been active on their client to reauthenticate to retrieve a new refresh token.</span></span>

<span data-ttu-id="f469a-285">「重新整理權杖最大閒置時間」屬性必須設定成低於「單一要素權杖最大壽命」和「多重要素重新整理權杖最大壽命」屬性的值。</span><span class="sxs-lookup"><span data-stu-id="f469a-285">The Refresh Token Max Inactive Time property must be set to a lower value than the Single-Factor Token Max Age and the Multi-Factor Refresh Token Max Age properties.</span></span>

### <a name="single-factor-refresh-token-max-age"></a><span data-ttu-id="f469a-286">單一要素重新整理權杖最大壽命</span><span class="sxs-lookup"><span data-stu-id="f469a-286">Single-Factor Refresh Token Max Age</span></span>
<span data-ttu-id="f469a-287">**字串︰**MaxAgeSingleFactor</span><span class="sxs-lookup"><span data-stu-id="f469a-287">**String:** MaxAgeSingleFactor</span></span>

<span data-ttu-id="f469a-288">**影響：**重新整理權杖</span><span class="sxs-lookup"><span data-stu-id="f469a-288">**Affects:** Refresh tokens</span></span>

<span data-ttu-id="f469a-289">**摘要︰**此原則可控制使用者在上次僅以單一要素成功驗證之後，可以持續多久使用重新整理權杖來取得一組新的存取/重新整理權杖。</span><span class="sxs-lookup"><span data-stu-id="f469a-289">**Summary:** This policy controls how long a user can use a refresh token to get a new access/refresh token pair after they last authenticated successfully by using only a single factor.</span></span> <span data-ttu-id="f469a-290">使用者驗證並接收新的重新整理權杖之後，使用者可以使用重新整理權杖流程一段指定的時間。</span><span class="sxs-lookup"><span data-stu-id="f469a-290">After a user authenticates and receives a new refresh token, the user can use the refresh token flow for the specified period of time.</span></span> <span data-ttu-id="f469a-291">(只要目前重新整理權杖未撤銷，且未使用的時間不超過非作用中的時間，這個情形就成立。)到那時，系統將會強制使用者必須重新驗證，才能收到新的重新整理權杖。</span><span class="sxs-lookup"><span data-stu-id="f469a-291">(This is true as long as the current refresh token is not revoked, and it is not left unused for longer than the inactive time.) At that point, the user is forced to reauthenticate to receive a new refresh token.</span></span>

<span data-ttu-id="f469a-292">縮短最大壽命將會強制使用者更頻繁地進行驗證。</span><span class="sxs-lookup"><span data-stu-id="f469a-292">Reducing the max age forces users to authenticate more often.</span></span> <span data-ttu-id="f469a-293">因為單一要素驗證的安全性被視為比多重要素驗證低，因此建議將此屬性設定為等於或小於「多重要素重新整理權杖最大壽命」屬性的值。</span><span class="sxs-lookup"><span data-stu-id="f469a-293">Because single-factor authentication is considered less secure than multi-factor authentication, we recommend that you set this property to a value that is equal to or lesser than the Multi-Factor Refresh Token Max Age property.</span></span>

### <a name="multi-factor-refresh-token-max-age"></a><span data-ttu-id="f469a-294">多重要素重新整理權杖最大壽命</span><span class="sxs-lookup"><span data-stu-id="f469a-294">Multi-Factor Refresh Token Max Age</span></span>
<span data-ttu-id="f469a-295">**字串︰**MaxAgeMultiFactor</span><span class="sxs-lookup"><span data-stu-id="f469a-295">**String:** MaxAgeMultiFactor</span></span>

<span data-ttu-id="f469a-296">**影響：**重新整理權杖</span><span class="sxs-lookup"><span data-stu-id="f469a-296">**Affects:** Refresh tokens</span></span>

<span data-ttu-id="f469a-297">**摘要︰**此原則可控制使用者在上次使用多重要素成功驗證之後，可以持續多久使用重新整理權杖來取得一組新的存取/重新整理權杖。</span><span class="sxs-lookup"><span data-stu-id="f469a-297">**Summary:** This policy controls how long a user can use a refresh token to get a new access/refresh token pair after they last authenticated successfully by using multiple factors.</span></span> <span data-ttu-id="f469a-298">使用者驗證並接收新的重新整理權杖之後，使用者可以使用重新整理權杖流程一段指定的時間。</span><span class="sxs-lookup"><span data-stu-id="f469a-298">After a user authenticates and receives a new refresh token, the user can use the refresh token flow for the specified period of time.</span></span> <span data-ttu-id="f469a-299">(只要目前重新整理權杖未撤銷，且未使用的時間不超過非作用中的時間，這個情形就成立。)到那時，系統將會強制使用者必須重新驗證，才能收到新的重新整理權杖。</span><span class="sxs-lookup"><span data-stu-id="f469a-299">(This is true as long as the current refresh token is not revoked, and it is not unused for longer than the inactive time.) At that point, users are forced to reauthenticate to receive a new refresh token.</span></span>

<span data-ttu-id="f469a-300">縮短最大壽命將會強制使用者更頻繁地進行驗證。</span><span class="sxs-lookup"><span data-stu-id="f469a-300">Reducing the max age forces users to authenticate more often.</span></span> <span data-ttu-id="f469a-301">因為單一要素驗證的安全性被視為比多重要素驗證低，因此建議將此屬性設定為等於或大於「單一要素重新整理權杖最大壽命」屬性的值。</span><span class="sxs-lookup"><span data-stu-id="f469a-301">Because single-factor authentication is considered less secure than multi-factor authentication, we recommend that you set this property to a value that is equal to or greater than the Single-Factor Refresh Token Max Age property.</span></span>

### <a name="single-factor-session-token-max-age"></a><span data-ttu-id="f469a-302">單一要素工作階段權杖最大壽命</span><span class="sxs-lookup"><span data-stu-id="f469a-302">Single-Factor Session Token Max Age</span></span>
<span data-ttu-id="f469a-303">**字串︰**MaxAgeSessionSingleFactor</span><span class="sxs-lookup"><span data-stu-id="f469a-303">**String:** MaxAgeSessionSingleFactor</span></span>

<span data-ttu-id="f469a-304">**影響：**工作階段權杖 (持續性和非持續性)</span><span class="sxs-lookup"><span data-stu-id="f469a-304">**Affects:** Session tokens (persistent and nonpersistent)</span></span>

<span data-ttu-id="f469a-305">**摘要︰**此原則可控制使用者在上次僅以單一要素成功驗證之後，可以持續多久使用工作階段權杖來取得新的識別碼和工作階段權杖。</span><span class="sxs-lookup"><span data-stu-id="f469a-305">**Summary:** This policy controls how long a user can use a session token to get a new ID and session token after they last authenticated successfully by using only a single factor.</span></span> <span data-ttu-id="f469a-306">使用者驗證並接收新的工作階段權杖之後，使用者可以使用工作階段權杖流程一段指定的時間。</span><span class="sxs-lookup"><span data-stu-id="f469a-306">After a user authenticates and receives a new session token, the user can use the session token flow for the specified period of time.</span></span> <span data-ttu-id="f469a-307">(只要目前的工作階段權杖未撤銷且未過期，這個情形就成立。)在指定的時間期間之後，系統會強制使用者重新驗證以接收新的工作階段權杖。</span><span class="sxs-lookup"><span data-stu-id="f469a-307">(This is true as long as the current session token is not revoked and has not expired.) After the specified period of time, the user is forced to reauthenticate to receive a new session token.</span></span>

<span data-ttu-id="f469a-308">縮短最大壽命將會強制使用者更頻繁地進行驗證。</span><span class="sxs-lookup"><span data-stu-id="f469a-308">Reducing the max age forces users to authenticate more often.</span></span> <span data-ttu-id="f469a-309">因為單一要素驗證的安全性被視為比多重要素驗證低，因此建議將此屬性設定為等於或小於「多重要素工作階段權杖最大壽命」屬性的值。</span><span class="sxs-lookup"><span data-stu-id="f469a-309">Because single-factor authentication is considered less secure than multi-factor authentication, we recommend that you set this property to a value that is equal to or less than the Multi-Factor Session Token Max Age property.</span></span>

### <a name="multi-factor-session-token-max-age"></a><span data-ttu-id="f469a-310">多重要素工作階段權杖最大壽命</span><span class="sxs-lookup"><span data-stu-id="f469a-310">Multi-Factor Session Token Max Age</span></span>
<span data-ttu-id="f469a-311">**字串︰**MaxAgeSessionMultiFactor</span><span class="sxs-lookup"><span data-stu-id="f469a-311">**String:** MaxAgeSessionMultiFactor</span></span>

<span data-ttu-id="f469a-312">**影響：**工作階段權杖 (持續性和非持續性)</span><span class="sxs-lookup"><span data-stu-id="f469a-312">**Affects:** Session tokens (persistent and nonpersistent)</span></span>

<span data-ttu-id="f469a-313">**摘要︰**此原則可控制使用者在上次以多重要素成功驗證之後，可以持續多久使用工作階段權杖來取得新的識別碼和工作階段權杖。</span><span class="sxs-lookup"><span data-stu-id="f469a-313">**Summary:** This policy controls how long a user can use a session token to get a new ID and session token after the last time they authenticated successfully by using multiple factors.</span></span> <span data-ttu-id="f469a-314">使用者驗證並接收新的工作階段權杖之後，使用者可以使用工作階段權杖流程一段指定的時間。</span><span class="sxs-lookup"><span data-stu-id="f469a-314">After a user authenticates and receives a new session token, the user can use the session token flow for the specified period of time.</span></span> <span data-ttu-id="f469a-315">(只要目前的工作階段權杖未撤銷且未過期，這個情形就成立。)在指定的時間期間之後，系統會強制使用者重新驗證以接收新的工作階段權杖。</span><span class="sxs-lookup"><span data-stu-id="f469a-315">(This is true as long as the current session token is not revoked and has not expired.) After the specified period of time, the user is forced to reauthenticate to receive a new session token.</span></span>

<span data-ttu-id="f469a-316">縮短最大壽命將會強制使用者更頻繁地進行驗證。</span><span class="sxs-lookup"><span data-stu-id="f469a-316">Reducing the max age forces users to authenticate more often.</span></span> <span data-ttu-id="f469a-317">因為單一要素驗證的安全性被視為比多重要素驗證低，因此建議將此屬性設定為等於或大於「單一要素工作階段權杖最大壽命」屬性的值。</span><span class="sxs-lookup"><span data-stu-id="f469a-317">Because single-factor authentication is considered less secure than multi-factor authentication, we recommend that you set this property to a value that is equal to or greater than the Single-Factor Session Token Max Age property.</span></span>

## <a name="example-token-lifetime-policies"></a><span data-ttu-id="f469a-318">範例權杖存留期原則</span><span class="sxs-lookup"><span data-stu-id="f469a-318">Example token lifetime policies</span></span>
<span data-ttu-id="f469a-319">當您為應用程式、服務主體及您整體組織建立及管理權杖存留期時，在 Azure AD 中許多案例都是可能的。</span><span class="sxs-lookup"><span data-stu-id="f469a-319">Many scenarios are possible in Azure AD when you can create and manage token lifetimes for apps, service principals, and your overall organization.</span></span> <span data-ttu-id="f469a-320">在本節中，我們將逐步解說一些常見的原則案例，這些案例可以協助您強制實行下列各項的新規則：</span><span class="sxs-lookup"><span data-stu-id="f469a-320">In this section, we walk through a few common policy scenarios that can help you impose new rules for:</span></span>

* <span data-ttu-id="f469a-321">權杖存留期</span><span class="sxs-lookup"><span data-stu-id="f469a-321">Token Lifetime</span></span>
* <span data-ttu-id="f469a-322">權杖最大閒置時間</span><span class="sxs-lookup"><span data-stu-id="f469a-322">Token Max Inactive Time</span></span>
* <span data-ttu-id="f469a-323">權杖最大壽命</span><span class="sxs-lookup"><span data-stu-id="f469a-323">Token Max Age</span></span>

<span data-ttu-id="f469a-324">在範例中，您可以了解如何︰</span><span class="sxs-lookup"><span data-stu-id="f469a-324">In the examples, you can learn how to:</span></span>

* <span data-ttu-id="f469a-325">管理組織的預設原則</span><span class="sxs-lookup"><span data-stu-id="f469a-325">Manage an organization's default policy</span></span>
* <span data-ttu-id="f469a-326">為 Web 登入建立原則</span><span class="sxs-lookup"><span data-stu-id="f469a-326">Create a policy for web sign-in</span></span>
* <span data-ttu-id="f469a-327">針對呼叫 Web API 的原生應用程式建立原則</span><span class="sxs-lookup"><span data-stu-id="f469a-327">Create a policy for a native app that calls a web API</span></span>
* <span data-ttu-id="f469a-328">管理進階原則</span><span class="sxs-lookup"><span data-stu-id="f469a-328">Manage an advanced policy</span></span>

### <a name="prerequisites"></a><span data-ttu-id="f469a-329">必要條件</span><span class="sxs-lookup"><span data-stu-id="f469a-329">Prerequisites</span></span>
<span data-ttu-id="f469a-330">在下列範例中，您建立、更新連結，並刪除應用程式、服務主體和您整體組織的原則。</span><span class="sxs-lookup"><span data-stu-id="f469a-330">In the following examples, you create, update, link, and delete policies for apps, service principals, and your overall organization.</span></span> <span data-ttu-id="f469a-331">如果您是 Azure AD 的新手，我們建議您先深入了解[如何取得 Azure AD 租用戶](active-directory-howto-tenant.md)，然後再利用這些範例繼續進行。</span><span class="sxs-lookup"><span data-stu-id="f469a-331">If you are new to Azure AD, we recommend that you learn about [how to get an Azure AD tenant](active-directory-howto-tenant.md) before you proceed with these examples.</span></span>  

<span data-ttu-id="f469a-332">若要開始使用，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="f469a-332">To get started, do the following steps:</span></span>

1. <span data-ttu-id="f469a-333">下載最新的 [Azure AD PowerShell 模組公開預覽版本](https://www.powershellgallery.com/packages/AzureADPreview)。</span><span class="sxs-lookup"><span data-stu-id="f469a-333">Download the latest [Azure AD PowerShell Module Public Preview release](https://www.powershellgallery.com/packages/AzureADPreview).</span></span>
2. <span data-ttu-id="f469a-334">執行 `Connect` 命令以登入您的 Azure AD 管理帳戶。</span><span class="sxs-lookup"><span data-stu-id="f469a-334">Run the `Connect` command to sign in to your Azure AD admin account.</span></span> <span data-ttu-id="f469a-335">您每次啟動新的工作階段時執行此命令。</span><span class="sxs-lookup"><span data-stu-id="f469a-335">Run this command each time you start a new session.</span></span>

    ```PowerShell
    Connect-AzureAD -Confirm
    ```

3. <span data-ttu-id="f469a-336">若要查看在組織中建立的所有原則，請執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="f469a-336">To see all policies that have been created in your organization, run the following command.</span></span> <span data-ttu-id="f469a-337">在下列案例中的大多數操作之後，執行此命令。</span><span class="sxs-lookup"><span data-stu-id="f469a-337">Run this command after most operations in the following scenarios.</span></span> <span data-ttu-id="f469a-338">執行命令也會協助您取得原則的 ** **。</span><span class="sxs-lookup"><span data-stu-id="f469a-338">Running the command also helps you get the ** ** of your policies.</span></span>

    ```PowerShell
    Get-AzureADPolicy
    ```

### <a name="example-manage-an-organizations-default-policy"></a><span data-ttu-id="f469a-339">範例：管理組織的預設原則</span><span class="sxs-lookup"><span data-stu-id="f469a-339">Example: Manage an organization's default policy</span></span>
<span data-ttu-id="f469a-340">在此範例中，您會建立可讓使用者在您整個組織中降低登入頻率的原則。</span><span class="sxs-lookup"><span data-stu-id="f469a-340">In this example, you create a policy that lets your users sign in less frequently across your entire organization.</span></span> <span data-ttu-id="f469a-341">為了這樣做，我們將為「單一要素重新整理權杖」建立一個在整個組織套用的權杖存留期原則。</span><span class="sxs-lookup"><span data-stu-id="f469a-341">To do this, create a token lifetime policy for Single-Factor Refresh Tokens, which is applied across your organization.</span></span> <span data-ttu-id="f469a-342">此原則套用至您組織中的每個應用程式，以及每個尚未設定原則的服務主體。</span><span class="sxs-lookup"><span data-stu-id="f469a-342">The policy is applied to every application in your organization, and to each service principal that doesn’t already have a policy set.</span></span>

1. <span data-ttu-id="f469a-343">建立權杖存留期原則。</span><span class="sxs-lookup"><span data-stu-id="f469a-343">Create a token lifetime policy.</span></span>

    1.  <span data-ttu-id="f469a-344">將單一要素重新整理權杖設為「直到撤銷為止」。</span><span class="sxs-lookup"><span data-stu-id="f469a-344">Set the Single-Factor Refresh Token to "until-revoked."</span></span> <span data-ttu-id="f469a-345">權杖不會過期直到存取權被撤銷。</span><span class="sxs-lookup"><span data-stu-id="f469a-345">The token doesn't expire until access is revoked.</span></span> <span data-ttu-id="f469a-346">建立下列原則定義︰</span><span class="sxs-lookup"><span data-stu-id="f469a-346">Create the following policy definition:</span></span>

        ```PowerShell
        @('{
            "TokenLifetimePolicy":
            {
                "Version":1,
                "MaxAgeSingleFactor":"until-revoked"
            }
        }')
        ```

    2.  <span data-ttu-id="f469a-347">若要建立原則，請執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="f469a-347">To create the policy, run the following command:</span></span>

        ```PowerShell
        New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1, "MaxAgeSingleFactor":"until-revoked"}}') -DisplayName "OrganizationDefaultPolicyScenario" -IsOrganizationDefault $true -Type "TokenLifetimePolicy"
        ```

    3.  <span data-ttu-id="f469a-348">若要查看您的新原則並取得原則的 **ObjectId**，請執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="f469a-348">To see your new policy, and to get the policy's **ObjectId**, run the following command:</span></span>

        ```PowerShell
        Get-AzureADPolicy
        ```

2. <span data-ttu-id="f469a-349">更新原則。</span><span class="sxs-lookup"><span data-stu-id="f469a-349">Update the policy.</span></span>

    <span data-ttu-id="f469a-350">您可能會決定您在此範例中設定的第一個原則不若您的服務所需的那樣嚴格。</span><span class="sxs-lookup"><span data-stu-id="f469a-350">You might decide that the first policy you set in this example is not as strict as your service requires.</span></span> <span data-ttu-id="f469a-351">若要設定單一要素重新整理權杖在兩天內過期，請執行下列命令︰</span><span class="sxs-lookup"><span data-stu-id="f469a-351">To set your Single-Factor Refresh Token to expire in two days, run the following command:</span></span>

    ```PowerShell
    Set-AzureADPolicy -Id <ObjectId FROM GET COMMAND> -DisplayName "OrganizationDefaultPolicyUpdatedScenario" -Definition @('{"TokenLifetimePolicy":{"Version":1,"MaxAgeSingleFactor":"2.00:00:00"}}')
    ```

### <a name="example-create-a-policy-for-web-sign-in"></a><span data-ttu-id="f469a-352">範例：為 Web 登入建立原則</span><span class="sxs-lookup"><span data-stu-id="f469a-352">Example: Create a policy for web sign-in</span></span>

<span data-ttu-id="f469a-353">在此範例中，您建立會要求使用者提高驗證頻率來登入 Web 應用程式的原則。</span><span class="sxs-lookup"><span data-stu-id="f469a-353">In this example, you create a policy that requires users to authenticate more frequently in your web app.</span></span> <span data-ttu-id="f469a-354">此原則會為 Web 應用程式的服務主體設定存取權杖/識別碼權杖的存留期及多重要素工作階段權杖的最大壽命。</span><span class="sxs-lookup"><span data-stu-id="f469a-354">This policy sets the lifetime of the access/ID tokens and the max age of a multi-factor session token to the service principal of your web app.</span></span>

1. <span data-ttu-id="f469a-355">建立權杖存留期原則。</span><span class="sxs-lookup"><span data-stu-id="f469a-355">Create a token lifetime policy.</span></span>

    <span data-ttu-id="f469a-356">這個 Web 登入原則會將存取權杖/識別碼權杖的存留期及單一要素工作階段權杖最大壽命設定為 2 小時。</span><span class="sxs-lookup"><span data-stu-id="f469a-356">This policy, for web sign-in, sets the access/ID token lifetime and the max single-factor session token age to two hours.</span></span>

    1.  <span data-ttu-id="f469a-357">若要建立原則，請執行此命令：</span><span class="sxs-lookup"><span data-stu-id="f469a-357">To create the policy, run this command:</span></span>

        ```PowerShell
        New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1,"AccessTokenLifetime":"02:00:00","MaxAgeSessionSingleFactor":"02:00:00"}}') -DisplayName "WebPolicyScenario" -IsOrganizationDefault $false -Type "TokenLifetimePolicy"
        ```

    2.  <span data-ttu-id="f469a-358">若要查看您的新原則並取得原則的 **ObjectId**，請執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="f469a-358">To see your new policy, and to get the policy **ObjectId**, run the following command:</span></span>

        ```PowerShell
        Get-AzureADPolicy
        ```

2.  <span data-ttu-id="f469a-359">將原則指派給服務主體。</span><span class="sxs-lookup"><span data-stu-id="f469a-359">Assign the policy to your service principal.</span></span> <span data-ttu-id="f469a-360">您也需要取得服務主體的 **ObjectId**。</span><span class="sxs-lookup"><span data-stu-id="f469a-360">You also need to get the **ObjectId** of your service principal.</span></span> 

    1.  <span data-ttu-id="f469a-361">若要查看您組織的所有服務主體，您可以查詢 [Microsoft Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity)。</span><span class="sxs-lookup"><span data-stu-id="f469a-361">To see all your organization's service principals, you can query [Microsoft Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity).</span></span> <span data-ttu-id="f469a-362">或者，在 [Azure AD Graph 總管](https://graphexplorer.cloudapp.net/)，登入您的 Azure AD 帳戶。</span><span class="sxs-lookup"><span data-stu-id="f469a-362">Or, in [Azure AD Graph Explorer](https://graphexplorer.cloudapp.net/), sign in to your Azure AD account.</span></span>

    2.  <span data-ttu-id="f469a-363">當您有服務主體的 **ObjectId** 時，執行下列命令︰</span><span class="sxs-lookup"><span data-stu-id="f469a-363">When you have the **ObjectId** of your service principal, run the following command:</span></span>

        ```PowerShell
        Add-AzureADServicePrincipalPolicy -Id <ObjectId of the ServicePrincipal> -RefObjectId <ObjectId of the Policy>
        ```


### <a name="example-create-a-policy-for-a-native-app-that-calls-a-web-api"></a><span data-ttu-id="f469a-364">範例：針對呼叫 Web API 的原生應用程式建立原則</span><span class="sxs-lookup"><span data-stu-id="f469a-364">Example: Create a policy for a native app that calls a web API</span></span>
<span data-ttu-id="f469a-365">在此範例中，您建立會要求使用者減少驗證頻率的原則。</span><span class="sxs-lookup"><span data-stu-id="f469a-365">In this example, you create a policy that requires users to authenticate less frequently.</span></span> <span data-ttu-id="f469a-366">原則也會延長使用者必須重新驗證之前，可以是非使用中的時間量。</span><span class="sxs-lookup"><span data-stu-id="f469a-366">The policy also lengthens the amount of time a user can be inactive before the user must reauthenticate.</span></span> <span data-ttu-id="f469a-367">原則會套用到 Web API。</span><span class="sxs-lookup"><span data-stu-id="f469a-367">The policy is applied to the web API.</span></span> <span data-ttu-id="f469a-368">當原生應用程式要求 Web API 做為資源時，會套用此原則。</span><span class="sxs-lookup"><span data-stu-id="f469a-368">When the native app requests the web API as a resource, this policy is applied.</span></span>

1. <span data-ttu-id="f469a-369">建立權杖存留期原則。</span><span class="sxs-lookup"><span data-stu-id="f469a-369">Create a token lifetime policy.</span></span>

    1.  <span data-ttu-id="f469a-370">若要為 Web API 建立嚴格的原則，請執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="f469a-370">To create a strict policy for a web API, run the following command:</span></span>

        ```PowerShell
        New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1,"MaxInactiveTime":"30.00:00:00","MaxAgeMultiFactor":"until-revoked","MaxAgeSingleFactor":"180.00:00:00"}}') -DisplayName "WebApiDefaultPolicyScenario" -IsOrganizationDefault $false -Type "TokenLifetimePolicy"
        ```

    2.  <span data-ttu-id="f469a-371">若要查看您的新原則並取得原則的 **ObjectId**，請執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="f469a-371">To see your new policy, and to get the policy **ObjectId**, run the following command:</span></span>

        ```PowerShell
        Get-AzureADPolicy
        ```

2. <span data-ttu-id="f469a-372">將原則指派給 Web API。</span><span class="sxs-lookup"><span data-stu-id="f469a-372">Assign the policy to your web API.</span></span> <span data-ttu-id="f469a-373">您也需要取得應用程式的 **ObjectId**。</span><span class="sxs-lookup"><span data-stu-id="f469a-373">You also need to get the **ObjectId** of your application.</span></span> <span data-ttu-id="f469a-374">尋找您應用程式之 **ObjectId** 的最佳方式就是使用 [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="f469a-374">The best way to find your app's **ObjectId** is to use the [Azure portal](https://portal.azure.com/).</span></span>

   <span data-ttu-id="f469a-375">有了應用程式的 **ObjectId** 之後，請執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="f469a-375">When you have the **ObjectId** of your app, run the following command:</span></span>

        ```PowerShell
        Add-AzureADApplicationPolicy -Id <ObjectId of the Application> -RefObjectId <ObjectId of the Policy>
        ```


### <a name="example-manage-an-advanced-policy"></a><span data-ttu-id="f469a-376">範例：管理進階原則</span><span class="sxs-lookup"><span data-stu-id="f469a-376">Example: Manage an advanced policy</span></span>
<span data-ttu-id="f469a-377">在此範例中，您建立幾個原則，以了解優先順序系統的運作方式。</span><span class="sxs-lookup"><span data-stu-id="f469a-377">In this example, you create a few policies, to learn how the priority system works.</span></span> <span data-ttu-id="f469a-378">您也可以了解如何管理會套用至數個物件的多個原則。</span><span class="sxs-lookup"><span data-stu-id="f469a-378">You also can learn how to manage multiple policies that are applied to several objects.</span></span>

1. <span data-ttu-id="f469a-379">建立權杖存留期原則。</span><span class="sxs-lookup"><span data-stu-id="f469a-379">Create a token lifetime policy.</span></span>

    1.  <span data-ttu-id="f469a-380">若要建立一個將「單一要素重新整理權杖」存留期設定為 30 天的組織預設原則，請執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="f469a-380">To create an organization default policy that sets the Single-Factor Refresh Token lifetime to 30 days, run the following command:</span></span>

        ```PowerShell
        New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1,"MaxAgeSingleFactor":"30.00:00:00"}}') -DisplayName "ComplexPolicyScenario" -IsOrganizationDefault $true -Type "TokenLifetimePolicy"
        ```

    2.  <span data-ttu-id="f469a-381">若要查看您的新原則並取得原則的 **ObjectId**，請執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="f469a-381">To see your new policy, and to get the policy's **ObjectId**, run the following command:</span></span>

        ```PowerShell
        Get-AzureADPolicy
        ```

2. <span data-ttu-id="f469a-382">將原則指派給服務主體。</span><span class="sxs-lookup"><span data-stu-id="f469a-382">Assign the policy to a service principal.</span></span>

    <span data-ttu-id="f469a-383">現在，您具有原則，該原則套用到整個組織。</span><span class="sxs-lookup"><span data-stu-id="f469a-383">Now, you have a policy that applies to the entire organization.</span></span> <span data-ttu-id="f469a-384">您可能想要針對特定的服務主體保留這個 30 天原則，但是將組織預設原則變更為上限「直到撤銷為止」。</span><span class="sxs-lookup"><span data-stu-id="f469a-384">You might want to preserve this 30-day policy for a specific service principal, but change the organization default policy to the upper limit of "until-revoked."</span></span>

    1.  <span data-ttu-id="f469a-385">若要查看您組織的所有服務主體，您可以查詢 [Microsoft Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity)。</span><span class="sxs-lookup"><span data-stu-id="f469a-385">To see all your organization's service principals, you can query [Microsoft Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity).</span></span> <span data-ttu-id="f469a-386">或者，在 [Azure AD Graph 總管](https://graphexplorer.cloudapp.net/)，使用您的 Azure AD 帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="f469a-386">Or, in [Azure AD Graph Explorer](https://graphexplorer.cloudapp.net/), sign in by using your Azure AD account.</span></span>

    2.  <span data-ttu-id="f469a-387">當您有服務主體的 **ObjectId** 時，執行下列命令︰</span><span class="sxs-lookup"><span data-stu-id="f469a-387">When you have the **ObjectId** of your service principal, run the following command:</span></span>

            ```PowerShell
            Add-AzureADServicePrincipalPolicy -Id <ObjectId of the ServicePrincipal> -RefObjectId <ObjectId of the Policy>
            ```
        
3. <span data-ttu-id="f469a-388">將 `IsOrganizationDefault` 旗標設為 false：</span><span class="sxs-lookup"><span data-stu-id="f469a-388">Set the `IsOrganizationDefault` flag to false:</span></span>

    ```PowerShell
    Set-AzureADPolicy -Id <ObjectId of Policy> -DisplayName "ComplexPolicyScenario" -IsOrganizationDefault $false
    ```

4. <span data-ttu-id="f469a-389">建立新的組織預設原則：</span><span class="sxs-lookup"><span data-stu-id="f469a-389">Create a new organization default policy:</span></span>

    ```PowerShell
    New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1,"MaxAgeSingleFactor":"until-revoked"}}') -DisplayName "ComplexPolicyScenarioTwo" -IsOrganizationDefault $true -Type "TokenLifetimePolicy"
    ```

    <span data-ttu-id="f469a-390">現在，原始原則已連結至您的服務主體，且新原則已設定為您的組織預設原則。</span><span class="sxs-lookup"><span data-stu-id="f469a-390">You now have the original policy linked to your service principal, and the new policy is set as your organization default policy.</span></span> <span data-ttu-id="f469a-391">請務必記住，套用至服務主體的原則優先順序會高於組織預設原則。</span><span class="sxs-lookup"><span data-stu-id="f469a-391">It's important to remember that policies applied to service principals have priority over organization default policies.</span></span>

## <a name="cmdlet-reference"></a><span data-ttu-id="f469a-392">Cmdlet 參考</span><span class="sxs-lookup"><span data-stu-id="f469a-392">Cmdlet reference</span></span>

### <a name="manage-policies"></a><span data-ttu-id="f469a-393">管理原則</span><span class="sxs-lookup"><span data-stu-id="f469a-393">Manage policies</span></span>

<span data-ttu-id="f469a-394">您可以使用下列 Cmdlet 來管理原則。</span><span class="sxs-lookup"><span data-stu-id="f469a-394">You can use the following cmdlets to manage policies.</span></span>

#### <a name="new-azureadpolicy"></a><span data-ttu-id="f469a-395">New-AzureADPolicy</span><span class="sxs-lookup"><span data-stu-id="f469a-395">New-AzureADPolicy</span></span>

<span data-ttu-id="f469a-396">建立新的原則。</span><span class="sxs-lookup"><span data-stu-id="f469a-396">Creates a new policy.</span></span>

```PowerShell
New-AzureADPolicy -Definition <Array of Rules> -DisplayName <Name of Policy> -IsOrganizationDefault <boolean> -Type <Policy Type>
```

| <span data-ttu-id="f469a-397">參數</span><span class="sxs-lookup"><span data-stu-id="f469a-397">Parameters</span></span> | <span data-ttu-id="f469a-398">說明</span><span class="sxs-lookup"><span data-stu-id="f469a-398">Description</span></span> | <span data-ttu-id="f469a-399">範例</span><span class="sxs-lookup"><span data-stu-id="f469a-399">Example</span></span> |
| --- | --- | --- |
| <code>&#8209;Definition</code> |<span data-ttu-id="f469a-400">字串化 JSON 的陣列，包含所有原則的規則。</span><span class="sxs-lookup"><span data-stu-id="f469a-400">Array of stringified JSON that contains all the policy's rules.</span></span> | `-Definition @('{"TokenLifetimePolicy":{"Version":1,"MaxInactiveTime":"20:00:00"}}')` |
| <code>&#8209;DisplayName</code> |<span data-ttu-id="f469a-401">原則名稱的字串。</span><span class="sxs-lookup"><span data-stu-id="f469a-401">String of the policy name.</span></span> |`-DisplayName "MyTokenPolicy"` |
| <code>&#8209;IsOrganizationDefault</code> |<span data-ttu-id="f469a-402">如果為 true，就會將原則設定為組織的預設原則。</span><span class="sxs-lookup"><span data-stu-id="f469a-402">If true, sets the policy as the organization's default policy.</span></span> <span data-ttu-id="f469a-403">如果為 false，則不會執行任何動作。</span><span class="sxs-lookup"><span data-stu-id="f469a-403">If false, does nothing.</span></span> |`-IsOrganizationDefault $true` |
| <code>&#8209;Type</code> |<span data-ttu-id="f469a-404">原則類型。</span><span class="sxs-lookup"><span data-stu-id="f469a-404">Type of policy.</span></span> <span data-ttu-id="f469a-405">針對權杖存留期，請一律使用 "TokenLifetimePolicy"。</span><span class="sxs-lookup"><span data-stu-id="f469a-405">For token lifetimes, always use "TokenLifetimePolicy."</span></span> | `-Type "TokenLifetimePolicy"` |
| <span data-ttu-id="f469a-406"><code>&#8209;AlternativeIdentifier</code> [選用]</span><span class="sxs-lookup"><span data-stu-id="f469a-406"><code>&#8209;AlternativeIdentifier</code> [Optional]</span></span> |<span data-ttu-id="f469a-407">設定原則的替代識別碼。</span><span class="sxs-lookup"><span data-stu-id="f469a-407">Sets an alternative ID for the policy.</span></span> |`-AlternativeIdentifier "myAltId"` |

</br></br>

#### <a name="get-azureadpolicy"></a><span data-ttu-id="f469a-408">Get-AzureADPolicy</span><span class="sxs-lookup"><span data-stu-id="f469a-408">Get-AzureADPolicy</span></span>
<span data-ttu-id="f469a-409">取得所有 Azure AD 原則或指定的原則。</span><span class="sxs-lookup"><span data-stu-id="f469a-409">Gets all Azure AD policies or a specified policy.</span></span>

```PowerShell
Get-AzureADPolicy
```

| <span data-ttu-id="f469a-410">參數</span><span class="sxs-lookup"><span data-stu-id="f469a-410">Parameters</span></span> | <span data-ttu-id="f469a-411">說明</span><span class="sxs-lookup"><span data-stu-id="f469a-411">Description</span></span> | <span data-ttu-id="f469a-412">範例</span><span class="sxs-lookup"><span data-stu-id="f469a-412">Example</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f469a-413"><code>&#8209;Id</code> [選用]</span><span class="sxs-lookup"><span data-stu-id="f469a-413"><code>&#8209;Id</code> [Optional]</span></span> |<span data-ttu-id="f469a-414">您想要之原則的 **ObjectId (Id)**。</span><span class="sxs-lookup"><span data-stu-id="f469a-414">**ObjectId (Id)** of the policy you want.</span></span> |`-Id <ObjectId of Policy>` |

</br></br>

#### <a name="get-azureadpolicyappliedobject"></a><span data-ttu-id="f469a-415">Get-AzureADPolicyAppliedObject</span><span class="sxs-lookup"><span data-stu-id="f469a-415">Get-AzureADPolicyAppliedObject</span></span>
<span data-ttu-id="f469a-416">取得與原則連結的所有應用程式和服務主體。</span><span class="sxs-lookup"><span data-stu-id="f469a-416">Gets all apps and service principals that are linked to a policy.</span></span>

```PowerShell
Get-AzureADPolicyAppliedObject -Id <ObjectId of Policy>
```

| <span data-ttu-id="f469a-417">參數</span><span class="sxs-lookup"><span data-stu-id="f469a-417">Parameters</span></span> | <span data-ttu-id="f469a-418">說明</span><span class="sxs-lookup"><span data-stu-id="f469a-418">Description</span></span> | <span data-ttu-id="f469a-419">範例</span><span class="sxs-lookup"><span data-stu-id="f469a-419">Example</span></span> |
| --- | --- | --- |
| <code>&#8209;Id</code> |<span data-ttu-id="f469a-420">您想要之原則的 **ObjectId (Id)**。</span><span class="sxs-lookup"><span data-stu-id="f469a-420">**ObjectId (Id)** of the policy you want.</span></span> |`-Id <ObjectId of Policy>` |

</br></br>

#### <a name="set-azureadpolicy"></a><span data-ttu-id="f469a-421">Set-AzureADPolicy</span><span class="sxs-lookup"><span data-stu-id="f469a-421">Set-AzureADPolicy</span></span>
<span data-ttu-id="f469a-422">更新現有的原則。</span><span class="sxs-lookup"><span data-stu-id="f469a-422">Updates an existing policy.</span></span>

```PowerShell
Set-AzureADPolicy -Id <ObjectId of Policy> -DisplayName <string>
```

| <span data-ttu-id="f469a-423">參數</span><span class="sxs-lookup"><span data-stu-id="f469a-423">Parameters</span></span> | <span data-ttu-id="f469a-424">說明</span><span class="sxs-lookup"><span data-stu-id="f469a-424">Description</span></span> | <span data-ttu-id="f469a-425">範例</span><span class="sxs-lookup"><span data-stu-id="f469a-425">Example</span></span> |
| --- | --- | --- |
| <code>&#8209;Id</code> |<span data-ttu-id="f469a-426">您想要之原則的 **ObjectId (Id)**。</span><span class="sxs-lookup"><span data-stu-id="f469a-426">**ObjectId (Id)** of the policy you want.</span></span> |`-Id <ObjectId of Policy>` |
| <code>&#8209;DisplayName</code> |<span data-ttu-id="f469a-427">原則名稱的字串。</span><span class="sxs-lookup"><span data-stu-id="f469a-427">String of the policy name.</span></span> |`-DisplayName "MyTokenPolicy"` |
| <span data-ttu-id="f469a-428"><code>&#8209;Definition</code> [選用]</span><span class="sxs-lookup"><span data-stu-id="f469a-428"><code>&#8209;Definition</code> [Optional]</span></span> |<span data-ttu-id="f469a-429">字串化 JSON 的陣列，包含所有原則的規則。</span><span class="sxs-lookup"><span data-stu-id="f469a-429">Array of stringified JSON that contains all the policy's rules.</span></span> |`-Definition @('{"TokenLifetimePolicy":{"Version":1,"MaxInactiveTime":"20:00:00"}}')` |
| <span data-ttu-id="f469a-430"><code>&#8209;IsOrganizationDefault</code> [選用]</span><span class="sxs-lookup"><span data-stu-id="f469a-430"><code>&#8209;IsOrganizationDefault</code> [Optional]</span></span> |<span data-ttu-id="f469a-431">如果為 true，就會將原則設定為組織的預設原則。</span><span class="sxs-lookup"><span data-stu-id="f469a-431">If true, sets the policy as the organization's default policy.</span></span> <span data-ttu-id="f469a-432">如果為 false，則不會執行任何動作。</span><span class="sxs-lookup"><span data-stu-id="f469a-432">If false, does nothing.</span></span> |`-IsOrganizationDefault $true` |
| <span data-ttu-id="f469a-433"><code>&#8209;Type</code> [選用]</span><span class="sxs-lookup"><span data-stu-id="f469a-433"><code>&#8209;Type</code> [Optional]</span></span> |<span data-ttu-id="f469a-434">原則類型。</span><span class="sxs-lookup"><span data-stu-id="f469a-434">Type of policy.</span></span> <span data-ttu-id="f469a-435">針對權杖存留期，請一律使用 "TokenLifetimePolicy"。</span><span class="sxs-lookup"><span data-stu-id="f469a-435">For token lifetimes, always use "TokenLifetimePolicy."</span></span> |`-Type "TokenLifetimePolicy"` |
| <span data-ttu-id="f469a-436"><code>&#8209;AlternativeIdentifier</code> [選用]</span><span class="sxs-lookup"><span data-stu-id="f469a-436"><code>&#8209;AlternativeIdentifier</code> [Optional]</span></span> |<span data-ttu-id="f469a-437">設定原則的替代識別碼。</span><span class="sxs-lookup"><span data-stu-id="f469a-437">Sets an alternative ID for the policy.</span></span> |`-AlternativeIdentifier "myAltId"` |

</br></br>

#### <a name="remove-azureadpolicy"></a><span data-ttu-id="f469a-438">Remove-AzureADPolicy</span><span class="sxs-lookup"><span data-stu-id="f469a-438">Remove-AzureADPolicy</span></span>
<span data-ttu-id="f469a-439">刪除指定的原則。</span><span class="sxs-lookup"><span data-stu-id="f469a-439">Deletes the specified policy.</span></span>

```PowerShell
 Remove-AzureADPolicy -Id <ObjectId of Policy>
```

| <span data-ttu-id="f469a-440">參數</span><span class="sxs-lookup"><span data-stu-id="f469a-440">Parameters</span></span> | <span data-ttu-id="f469a-441">說明</span><span class="sxs-lookup"><span data-stu-id="f469a-441">Description</span></span> | <span data-ttu-id="f469a-442">範例</span><span class="sxs-lookup"><span data-stu-id="f469a-442">Example</span></span> |
| --- | --- | --- |
| <code>&#8209;Id</code> |<span data-ttu-id="f469a-443">您想要之原則的 **ObjectId (Id)**。</span><span class="sxs-lookup"><span data-stu-id="f469a-443">**ObjectId (Id)** of the policy you want.</span></span> | `-Id <ObjectId of Policy>` |

</br></br>

### <a name="application-policies"></a><span data-ttu-id="f469a-444">應用程式原則</span><span class="sxs-lookup"><span data-stu-id="f469a-444">Application policies</span></span>
<span data-ttu-id="f469a-445">您可以針對應用程式原則使用下列 Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="f469a-445">You can use the following cmdlets for application policies.</span></span></br></br>

#### <a name="add-azureadapplicationpolicy"></a><span data-ttu-id="f469a-446">Add-AzureADApplicationPolicy</span><span class="sxs-lookup"><span data-stu-id="f469a-446">Add-AzureADApplicationPolicy</span></span>
<span data-ttu-id="f469a-447">將指定的原則連結至應用程式。</span><span class="sxs-lookup"><span data-stu-id="f469a-447">Links the specified policy to an application.</span></span>

```PowerShell
Add-AzureADApplicationPolicy -Id <ObjectId of Application> -RefObjectId <ObjectId of Policy>
```

| <span data-ttu-id="f469a-448">參數</span><span class="sxs-lookup"><span data-stu-id="f469a-448">Parameters</span></span> | <span data-ttu-id="f469a-449">說明</span><span class="sxs-lookup"><span data-stu-id="f469a-449">Description</span></span> | <span data-ttu-id="f469a-450">範例</span><span class="sxs-lookup"><span data-stu-id="f469a-450">Example</span></span> |
| --- | --- | --- |
| <code>&#8209;Id</code> |<span data-ttu-id="f469a-451">應用程式的 **ObjectId (Id)**。</span><span class="sxs-lookup"><span data-stu-id="f469a-451">**ObjectId (Id)** of the application.</span></span> | `-Id <ObjectId of Application>` |
| <code>&#8209;RefObjectId</code> |<span data-ttu-id="f469a-452">原則的 **ObjectId**。</span><span class="sxs-lookup"><span data-stu-id="f469a-452">**ObjectId** of the policy.</span></span> | `-RefObjectId <ObjectId of Policy>` |

</br></br>

#### <a name="get-azureadapplicationpolicy"></a><span data-ttu-id="f469a-453">Get-AzureADApplicationPolicy</span><span class="sxs-lookup"><span data-stu-id="f469a-453">Get-AzureADApplicationPolicy</span></span>
<span data-ttu-id="f469a-454">取得指派給應用程式的原則。</span><span class="sxs-lookup"><span data-stu-id="f469a-454">Gets the policy that is assigned to an application.</span></span>

```PowerShell
Get-AzureADApplicationPolicy -Id <ObjectId of Application>
```

| <span data-ttu-id="f469a-455">參數</span><span class="sxs-lookup"><span data-stu-id="f469a-455">Parameters</span></span> | <span data-ttu-id="f469a-456">說明</span><span class="sxs-lookup"><span data-stu-id="f469a-456">Description</span></span> | <span data-ttu-id="f469a-457">範例</span><span class="sxs-lookup"><span data-stu-id="f469a-457">Example</span></span> |
| --- | --- | --- |
| <code>&#8209;Id</code> |<span data-ttu-id="f469a-458">應用程式的 **ObjectId (Id)**。</span><span class="sxs-lookup"><span data-stu-id="f469a-458">**ObjectId (Id)** of the application.</span></span> | `-Id <ObjectId of Application>` |

</br></br>

#### <a name="remove-azureadapplicationpolicy"></a><span data-ttu-id="f469a-459">Remove-AzureADApplicationPolicy</span><span class="sxs-lookup"><span data-stu-id="f469a-459">Remove-AzureADApplicationPolicy</span></span>
<span data-ttu-id="f469a-460">從應用程式移除原則。</span><span class="sxs-lookup"><span data-stu-id="f469a-460">Removes a policy from an application.</span></span>

```PowerShell
Remove-AzureADApplicationPolicy -Id <ObjectId of Application> -PolicyId <ObjectId of Policy>
```

| <span data-ttu-id="f469a-461">參數</span><span class="sxs-lookup"><span data-stu-id="f469a-461">Parameters</span></span> | <span data-ttu-id="f469a-462">說明</span><span class="sxs-lookup"><span data-stu-id="f469a-462">Description</span></span> | <span data-ttu-id="f469a-463">範例</span><span class="sxs-lookup"><span data-stu-id="f469a-463">Example</span></span> |
| --- | --- | --- |
| <code>&#8209;Id</code> |<span data-ttu-id="f469a-464">應用程式的 **ObjectId (Id)**。</span><span class="sxs-lookup"><span data-stu-id="f469a-464">**ObjectId (Id)** of the application.</span></span> | `-Id <ObjectId of Application>` |
| <code>&#8209;PolicyId</code> |<span data-ttu-id="f469a-465">原則的 **ObjectId**。</span><span class="sxs-lookup"><span data-stu-id="f469a-465">**ObjectId** of the policy.</span></span> | `-PolicyId <ObjectId of Policy>` |

</br></br>

### <a name="service-principal-policies"></a><span data-ttu-id="f469a-466">服務主體原則</span><span class="sxs-lookup"><span data-stu-id="f469a-466">Service principal policies</span></span>
<span data-ttu-id="f469a-467">您可以針對服務主體原則使用下列 Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="f469a-467">You can use the following cmdlets for service principal policies.</span></span>

#### <a name="add-azureadserviceprincipalpolicy"></a><span data-ttu-id="f469a-468">Add-AzureADServicePrincipalPolicy</span><span class="sxs-lookup"><span data-stu-id="f469a-468">Add-AzureADServicePrincipalPolicy</span></span>
<span data-ttu-id="f469a-469">將指定的原則連結至服務主體。</span><span class="sxs-lookup"><span data-stu-id="f469a-469">Links the specified policy to a service principal.</span></span>

```PowerShell
Add-AzureADServicePrincipalPolicy -Id <ObjectId of ServicePrincipal> -RefObjectId <ObjectId of Policy>
```

| <span data-ttu-id="f469a-470">參數</span><span class="sxs-lookup"><span data-stu-id="f469a-470">Parameters</span></span> | <span data-ttu-id="f469a-471">說明</span><span class="sxs-lookup"><span data-stu-id="f469a-471">Description</span></span> | <span data-ttu-id="f469a-472">範例</span><span class="sxs-lookup"><span data-stu-id="f469a-472">Example</span></span> |
| --- | --- | --- |
| <code>&#8209;Id</code> |<span data-ttu-id="f469a-473">應用程式的 **ObjectId (Id)**。</span><span class="sxs-lookup"><span data-stu-id="f469a-473">**ObjectId (Id)** of the application.</span></span> | `-Id <ObjectId of Application>` |
| <code>&#8209;RefObjectId</code> |<span data-ttu-id="f469a-474">原則的 **ObjectId**。</span><span class="sxs-lookup"><span data-stu-id="f469a-474">**ObjectId** of the policy.</span></span> | `-RefObjectId <ObjectId of Policy>` |

</br></br>

#### <a name="get-azureadserviceprincipalpolicy"></a><span data-ttu-id="f469a-475">Get-AzureADServicePrincipalPolicy</span><span class="sxs-lookup"><span data-stu-id="f469a-475">Get-AzureADServicePrincipalPolicy</span></span>
<span data-ttu-id="f469a-476">取得與指定的服務主體連結的任何原則。</span><span class="sxs-lookup"><span data-stu-id="f469a-476">Gets any policy linked to the specified service principal.</span></span>

```PowerShell
Get-AzureADServicePrincipalPolicy -Id <ObjectId of ServicePrincipal>
```

| <span data-ttu-id="f469a-477">參數</span><span class="sxs-lookup"><span data-stu-id="f469a-477">Parameters</span></span> | <span data-ttu-id="f469a-478">說明</span><span class="sxs-lookup"><span data-stu-id="f469a-478">Description</span></span> | <span data-ttu-id="f469a-479">範例</span><span class="sxs-lookup"><span data-stu-id="f469a-479">Example</span></span> |
| --- | --- | --- |
| <code>&#8209;Id</code> |<span data-ttu-id="f469a-480">應用程式的 **ObjectId (Id)**。</span><span class="sxs-lookup"><span data-stu-id="f469a-480">**ObjectId (Id)** of the application.</span></span> | `-Id <ObjectId of Application>` |

</br></br>

#### <a name="remove-azureadserviceprincipalpolicy"></a><span data-ttu-id="f469a-481">Remove-AzureADServicePrincipalPolicy</span><span class="sxs-lookup"><span data-stu-id="f469a-481">Remove-AzureADServicePrincipalPolicy</span></span>
<span data-ttu-id="f469a-482">從指定的服務主體移除原則。</span><span class="sxs-lookup"><span data-stu-id="f469a-482">Removes the policy from the specified service principal.</span></span>

```PowerShell
Remove-AzureADServicePrincipalPolicy -Id <ObjectId of ServicePrincipal>  -PolicyId <ObjectId of Policy>
```

| <span data-ttu-id="f469a-483">參數</span><span class="sxs-lookup"><span data-stu-id="f469a-483">Parameters</span></span> | <span data-ttu-id="f469a-484">說明</span><span class="sxs-lookup"><span data-stu-id="f469a-484">Description</span></span> | <span data-ttu-id="f469a-485">範例</span><span class="sxs-lookup"><span data-stu-id="f469a-485">Example</span></span> |
| --- | --- | --- |
| <code>&#8209;Id</code> |<span data-ttu-id="f469a-486">應用程式的 **ObjectId (Id)**。</span><span class="sxs-lookup"><span data-stu-id="f469a-486">**ObjectId (Id)** of the application.</span></span> | `-Id <ObjectId of Application>` |
| <code>&#8209;PolicyId</code> |<span data-ttu-id="f469a-487">原則的 **ObjectId**。</span><span class="sxs-lookup"><span data-stu-id="f469a-487">**ObjectId** of the policy.</span></span> | `-PolicyId <ObjectId of Policy>` |
