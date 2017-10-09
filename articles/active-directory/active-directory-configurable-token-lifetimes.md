---
title: "Azure Active Directory 中的 aaaConfigurable 權杖存留期 |Microsoft 文件"
description: "了解 Azure AD 所簽發 tooset 權杖的存留期的方式。"
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
ms.openlocfilehash: 0d4c8545981c5463cc7c95f669167bbc38230123
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configurable-token-lifetimes-in-azure-active-directory-public-preview"></a><span data-ttu-id="398ee-103">Azure Active Directory 中可設定的權杖存留期 (公開預覽版)</span><span class="sxs-lookup"><span data-stu-id="398ee-103">Configurable token lifetimes in Azure Active Directory (Public Preview)</span></span>
<span data-ttu-id="398ee-104">您可以指定 hello Azure Active Directory (Azure AD) 所簽發的權杖存留期。</span><span class="sxs-lookup"><span data-stu-id="398ee-104">You can specify hello lifetime of a token issued by Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="398ee-105">不論是針對組織中所有的應用程式、針對多租用戶 (多組織) 應用程式，還是針對組織中特定的服務主體，都可以設定權杖存留期。</span><span class="sxs-lookup"><span data-stu-id="398ee-105">You can set token lifetimes for all apps in your organization, for a multi-tenant (multi-organization) application, or for a specific service principal in your organization.</span></span>

> [!NOTE]
> <span data-ttu-id="398ee-106">這項功能目前為公開預覽版。</span><span class="sxs-lookup"><span data-stu-id="398ee-106">This capability currently is in Public Preview.</span></span> <span data-ttu-id="398ee-107">準備 toorevert 或移除任何變更。</span><span class="sxs-lookup"><span data-stu-id="398ee-107">Be prepared toorevert or remove any changes.</span></span> <span data-ttu-id="398ee-108">公開預覽期間的任何 Azure Active Directory 訂用帳戶中使用 hello 功能。</span><span class="sxs-lookup"><span data-stu-id="398ee-108">hello feature is available in any Azure Active Directory subscription during Public Preview.</span></span> <span data-ttu-id="398ee-109">不過，通常可以使用 hello 功能時，可能需要某些層面 hello 功能[Azure Active Directory Premium](active-directory-get-started-premium.md)訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="398ee-109">However, when hello feature becomes generally available, some aspects of hello feature might require an [Azure Active Directory Premium](active-directory-get-started-premium.md) subscription.</span></span>
>
>

<span data-ttu-id="398ee-110">在 Azure AD 中，原則物件代表在組織中個別應用程式或所有應用程式上強制執行的一組規則。</span><span class="sxs-lookup"><span data-stu-id="398ee-110">In Azure AD, a policy object represents a set of rules that are enforced on individual applications or on all applications in an organization.</span></span> <span data-ttu-id="398ee-111">每種原則類型有唯一的結構，以一組套用的 tooobjects toowhich 與其相關的屬性。</span><span class="sxs-lookup"><span data-stu-id="398ee-111">Each policy type has a unique structure, with a set of properties that are applied tooobjects toowhich they are assigned.</span></span>

<span data-ttu-id="398ee-112">您可以指定為 hello 預設原則的原則，為您的組織。</span><span class="sxs-lookup"><span data-stu-id="398ee-112">You can designate a policy as hello default policy for your organization.</span></span> <span data-ttu-id="398ee-113">hello 原則會套用的 tooany hello 組織中的應用程式，只要它不會覆寫優先順序較高的原則。</span><span class="sxs-lookup"><span data-stu-id="398ee-113">hello policy is applied tooany application in hello organization, as long as it is not overridden by a policy with a higher priority.</span></span> <span data-ttu-id="398ee-114">您也可以指派原則 toospecific 應用程式。</span><span class="sxs-lookup"><span data-stu-id="398ee-114">You also can assign a policy toospecific applications.</span></span> <span data-ttu-id="398ee-115">hello 依優先順序因原則類型。</span><span class="sxs-lookup"><span data-stu-id="398ee-115">hello order of priority varies by policy type.</span></span>


## <a name="token-types"></a><span data-ttu-id="398ee-116">權杖類型</span><span class="sxs-lookup"><span data-stu-id="398ee-116">Token types</span></span>

<span data-ttu-id="398ee-117">您可以針對重新整理權杖、存取權杖、工作階段權杖及識別碼權杖設定權杖存留期原則。</span><span class="sxs-lookup"><span data-stu-id="398ee-117">You can set token lifetime policies for refresh tokens, access tokens, session tokens, and ID tokens.</span></span>

### <a name="access-tokens"></a><span data-ttu-id="398ee-118">存取權杖</span><span class="sxs-lookup"><span data-stu-id="398ee-118">Access tokens</span></span>
<span data-ttu-id="398ee-119">用戶端使用存取權杖 tooaccess 受保護的資源。</span><span class="sxs-lookup"><span data-stu-id="398ee-119">Clients use access tokens tooaccess a protected resource.</span></span> <span data-ttu-id="398ee-120">存取權杖僅可用於特定使用者、用戶端及資源的組合。</span><span class="sxs-lookup"><span data-stu-id="398ee-120">An access token can be used only for a specific combination of user, client, and resource.</span></span> <span data-ttu-id="398ee-121">存取權杖是不可撤銷的，在到期之前都會一直有效。</span><span class="sxs-lookup"><span data-stu-id="398ee-121">Access tokens cannot be revoked and are valid until their expiry.</span></span> <span data-ttu-id="398ee-122">惡意執行者若已取得存取權杖，便可在權杖的存留期範圍內使用該權杖。</span><span class="sxs-lookup"><span data-stu-id="398ee-122">A malicious actor that has obtained an access token can use it for extent of its lifetime.</span></span> <span data-ttu-id="398ee-123">調整 hello 存留期的存取語彙基元是改善系統效能之間的取捨，而且增加 hello 一段時間的 hello 用戶端會保留存取，完成 hello 使用者帳戶已停用。</span><span class="sxs-lookup"><span data-stu-id="398ee-123">Adjusting hello lifetime of an access token is a trade-off between improving system performance and increasing hello amount of time that hello client retains access after hello user’s account is disabled.</span></span> <span data-ttu-id="398ee-124">改善的系統效能，來減少用戶端需要 tooacquire 全新的存取語彙基元的 hello 次數來達成。</span><span class="sxs-lookup"><span data-stu-id="398ee-124">Improved system performance is achieved by reducing hello number of times a client needs tooacquire a fresh access token.</span></span>

### <a name="refresh-tokens"></a><span data-ttu-id="398ee-125">重新整理權杖</span><span class="sxs-lookup"><span data-stu-id="398ee-125">Refresh tokens</span></span>
<span data-ttu-id="398ee-126">當用戶端取得存取權杖 tooaccess 受保護的資源時，hello 用戶端會收到重新整理權杖和存取權杖。</span><span class="sxs-lookup"><span data-stu-id="398ee-126">When a client acquires an access token tooaccess a protected resource, hello client receives both a refresh token and an access token.</span></span> <span data-ttu-id="398ee-127">hello 重新整理權杖時，使用的 tooobtain 新存取/重新整理語彙基元組 hello 目前存取權杖到期。</span><span class="sxs-lookup"><span data-stu-id="398ee-127">hello refresh token is used tooobtain new access/refresh token pairs when hello current access token expires.</span></span> <span data-ttu-id="398ee-128">重新整理權杖是使用者和用戶端的繫結的 tooa 組合。</span><span class="sxs-lookup"><span data-stu-id="398ee-128">A refresh token is bound tooa combination of user and client.</span></span> <span data-ttu-id="398ee-129">重新整理權杖可予以撤銷，並每次使用 hello 語彙基元時，會檢查 hello 權杖的有效性。</span><span class="sxs-lookup"><span data-stu-id="398ee-129">A refresh token can be revoked, and hello token's validity is checked every time hello token is used.</span></span>

<span data-ttu-id="398ee-130">它是重要 toomake 機密用戶端和公用的用戶端之間的差異。</span><span class="sxs-lookup"><span data-stu-id="398ee-130">It's important toomake a distinction between confidential clients and public clients.</span></span> <span data-ttu-id="398ee-131">如需不同類型用戶端的詳細資訊，請參閱 [RFC 6749](https://tools.ietf.org/html/rfc6749#section-2.1)。</span><span class="sxs-lookup"><span data-stu-id="398ee-131">For more information about different types of clients, see [RFC 6749](https://tools.ietf.org/html/rfc6749#section-2.1).</span></span>

#### <a name="token-lifetimes-with-confidential-client-refresh-tokens"></a><span data-ttu-id="398ee-132">具有機密用戶端重新整理權杖的權杖存留期</span><span class="sxs-lookup"><span data-stu-id="398ee-132">Token lifetimes with confidential client refresh tokens</span></span>
<span data-ttu-id="398ee-133">機密用戶端是可以安全地儲存用戶端密碼的應用程式。</span><span class="sxs-lookup"><span data-stu-id="398ee-133">Confidential clients are applications that can securely store a client password (secret).</span></span> <span data-ttu-id="398ee-134">它們可以證明要求即將從 hello 用戶端應用程式，而不是從惡意動作項目。</span><span class="sxs-lookup"><span data-stu-id="398ee-134">They can prove that requests are coming from hello client application and not from a malicious actor.</span></span> <span data-ttu-id="398ee-135">例如，web 應用程式是機密用戶端，因為它可以在 hello web 伺服器上儲存用戶端密碼。</span><span class="sxs-lookup"><span data-stu-id="398ee-135">For example, a web app is a confidential client because it can store a client secret on hello web server.</span></span> <span data-ttu-id="398ee-136">它不是公開的。</span><span class="sxs-lookup"><span data-stu-id="398ee-136">It is not exposed.</span></span> <span data-ttu-id="398ee-137">由於這些流程更安全，hello 發行的 toothese 流程會重新整理權杖的預設存留時間`until-revoked`，就無法變更使用原則，而且不會撤銷上自願密碼重設。</span><span class="sxs-lookup"><span data-stu-id="398ee-137">Because these flows are more secure, hello default lifetimes of refresh tokens issued toothese flows is `until-revoked`, cannot be changed by using policy, and will not be revoked on voluntary password resets.</span></span>

#### <a name="token-lifetimes-with-public-client-refresh-tokens"></a><span data-ttu-id="398ee-138">具有公開用戶端重新整理權杖的權杖存留期</span><span class="sxs-lookup"><span data-stu-id="398ee-138">Token lifetimes with public client refresh tokens</span></span>

<span data-ttu-id="398ee-139">公開用戶端無法安全地儲存用戶端密碼。</span><span class="sxs-lookup"><span data-stu-id="398ee-139">Public clients cannot securely store a client password (secret).</span></span> <span data-ttu-id="398ee-140">例如，iOS/Android 應用程式無法模糊化 hello 資源擁有者，從密碼，因此它會被視為公用的用戶端。</span><span class="sxs-lookup"><span data-stu-id="398ee-140">For example, an iOS/Android app cannot obfuscate a secret from hello resource owner, so it is considered a public client.</span></span> <span data-ttu-id="398ee-141">您可以設定原則資源 tooprevent 重新整理權杖從公用用戶端無法取得新的存取權/重新整理 token 組的指定時間之前。</span><span class="sxs-lookup"><span data-stu-id="398ee-141">You can set policies on resources tooprevent refresh tokens from public clients older than a specified period from obtaining a new access/refresh token pair.</span></span> <span data-ttu-id="398ee-142">(toodo，使用 hello 重新整理語彙基元非作用中時間上限 屬性。)您也可以使用原則 tooset 不再接受超過 hello 重新整理權杖的期限。</span><span class="sxs-lookup"><span data-stu-id="398ee-142">(toodo this, use hello Refresh Token Max Inactive Time property.) You also can use policies tooset a period beyond which hello refresh tokens are no longer accepted.</span></span> <span data-ttu-id="398ee-143">(toodo，使用 hello 重新整理權杖的最大 Age 屬性。)您可以調整時間和頻率 hello 使用者是必要的 tooreenter 認證，而不是以無訊息模式需要，使用公用的用戶端應用程式時重新整理語彙基元 toocontrol hello 存留期。</span><span class="sxs-lookup"><span data-stu-id="398ee-143">(toodo this, use hello Refresh Token Max Age property.) You can adjust hello lifetime of a refresh token toocontrol when and how often hello user is required tooreenter credentials, instead of being silently reauthenticated, when using a public client application.</span></span>

### <a name="id-tokens"></a><span data-ttu-id="398ee-144">ID 權杖</span><span class="sxs-lookup"><span data-stu-id="398ee-144">ID tokens</span></span>
<span data-ttu-id="398ee-145">ID 權杖會傳遞 toowebsites 和原生用戶端。</span><span class="sxs-lookup"><span data-stu-id="398ee-145">ID tokens are passed toowebsites and native clients.</span></span> <span data-ttu-id="398ee-146">識別碼權杖包含使用者的設定檔資訊。</span><span class="sxs-lookup"><span data-stu-id="398ee-146">ID tokens contain profile information about a user.</span></span> <span data-ttu-id="398ee-147">ID 語彙基元是繫結的 tooa 特定的使用者和用戶端的組合。</span><span class="sxs-lookup"><span data-stu-id="398ee-147">An ID token is bound tooa specific combination of user and client.</span></span> <span data-ttu-id="398ee-148">識別碼權杖在到期前都會被視為有效。</span><span class="sxs-lookup"><span data-stu-id="398ee-148">ID tokens are considered valid until their expiry.</span></span> <span data-ttu-id="398ee-149">通常，web 應用程式符合使用者的 hello 使用者發出 hello 應用程式 toohello 存留期的 hello 的 ID 語彙基元中的工作階段存留期。</span><span class="sxs-lookup"><span data-stu-id="398ee-149">Usually, a web application matches a user’s session lifetime in hello application toohello lifetime of hello ID token issued for hello user.</span></span> <span data-ttu-id="398ee-150">您可以調整 hello 存留期的 ID 語彙基元 toocontrol 頻率 hello web 應用程式到期 hello 應用程式工作階段和它需要 hello 使用者 toobe （以無訊息模式或以互動方式），重新驗證與 Azure AD 的頻率。</span><span class="sxs-lookup"><span data-stu-id="398ee-150">You can adjust hello lifetime of an ID token toocontrol how often hello web application expires hello application session, and how often it requires hello user toobe reauthenticated with Azure AD (either silently or interactively).</span></span>

### <a name="single-sign-on-session-tokens"></a><span data-ttu-id="398ee-151">單一登入工作階段權杖</span><span class="sxs-lookup"><span data-stu-id="398ee-151">Single sign-on session tokens</span></span>
<span data-ttu-id="398ee-152">當使用者向 Azure AD，並選取 hello**讓我保持登**核取方塊，單一登入 (SSO) 會建立工作階段與 hello 使用者的瀏覽器和 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="398ee-152">When a user authenticates with Azure AD and selects hello **Keep me signed in** check box, a single sign-on session (SSO) is established with hello user’s browser and Azure AD.</span></span> <span data-ttu-id="398ee-153">hello SSO 語彙基元，hello 形式 cookie，代表此工作階段。</span><span class="sxs-lookup"><span data-stu-id="398ee-153">hello SSO token, in hello form of a cookie, represents this session.</span></span> <span data-ttu-id="398ee-154">請注意該 hello SSO 工作階段權杖不是繫結的 tooa 特定資源/用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="398ee-154">Note that hello SSO session token is not bound tooa specific resource/client application.</span></span> <span data-ttu-id="398ee-155">SSO 工作階段權杖是可撤銷的，而每次使用這些權杖時，系統都會檢查其有效性。</span><span class="sxs-lookup"><span data-stu-id="398ee-155">SSO session tokens can be revoked, and their validity is checked every time they are used.</span></span>

<span data-ttu-id="398ee-156">Azure AD 會使用兩種 SSO 工作階段權杖︰持續性和非持續性。</span><span class="sxs-lookup"><span data-stu-id="398ee-156">Azure AD uses two kinds of SSO session tokens: persistent and nonpersistent.</span></span> <span data-ttu-id="398ee-157">持續性工作階段權杖會儲存為永續性 cookie，由 hello 瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="398ee-157">Persistent session tokens are stored as persistent cookies by hello browser.</span></span> <span data-ttu-id="398ee-158">非持續性工作階段權杖是儲存為工作階段 Cookie。</span><span class="sxs-lookup"><span data-stu-id="398ee-158">Nonpersistent session tokens are stored as session cookies.</span></span> <span data-ttu-id="398ee-159">（工作階段 cookie 會終結 hello 瀏覽器關閉時）。</span><span class="sxs-lookup"><span data-stu-id="398ee-159">(Session cookies are destroyed when hello browser is closed.)</span></span>

<span data-ttu-id="398ee-160">非持續性工作階段權杖有 24 小時的存留期。</span><span class="sxs-lookup"><span data-stu-id="398ee-160">Nonpersistent session tokens have a lifetime of 24 hours.</span></span> <span data-ttu-id="398ee-161">持續性權杖有 180 天的存留期。</span><span class="sxs-lookup"><span data-stu-id="398ee-161">Persistent tokens have a lifetime of 180 days.</span></span> <span data-ttu-id="398ee-162">SSO 的工作階段權杖用在其有效期間內，任何時候 hello 有效期間已擴充，另一個 24 小時或 180 天，視 hello 語彙基元類型而定。</span><span class="sxs-lookup"><span data-stu-id="398ee-162">Any time an SSO session token is used within its validity period, hello validity period is extended another 24 hours or 180 days, depending on hello token type.</span></span> <span data-ttu-id="398ee-163">如果未在 SSO 工作階段權杖的有效期內使用此權杖，系統就會將其視為過期而不再接受它。</span><span class="sxs-lookup"><span data-stu-id="398ee-163">If an SSO session token is not used within its validity period, it is considered expired and is no longer accepted.</span></span>

<span data-ttu-id="398ee-164">您可以使用原則 tooset hello 後的時間超出哪些 hello 不再接受工作階段權杖發行 hello 第一個工作階段權杖。</span><span class="sxs-lookup"><span data-stu-id="398ee-164">You can use a policy tooset hello time after hello first session token was issued beyond which hello session token is no longer accepted.</span></span> <span data-ttu-id="398ee-165">(toodo，使用 hello 工作階段權杖的最大 Age 屬性。)您可以調整使用者時間和頻率是必要的 tooreenter 認證，而不是以無訊息模式驗證，使用 web 應用程式時的工作階段權杖的 toocontrol hello 存留期。</span><span class="sxs-lookup"><span data-stu-id="398ee-165">(toodo this, use hello Session Token Max Age property.) You can adjust hello lifetime of a session token toocontrol when and how often a user is required tooreenter credentials, instead of being silently authenticated, when using a web application.</span></span>

### <a name="token-lifetime-policy-properties"></a><span data-ttu-id="398ee-166">權杖存留期原則屬性</span><span class="sxs-lookup"><span data-stu-id="398ee-166">Token lifetime policy properties</span></span>
<span data-ttu-id="398ee-167">權杖存留期原則是一種包含權杖存留期規則的原則物件。</span><span class="sxs-lookup"><span data-stu-id="398ee-167">A token lifetime policy is a type of policy object that contains token lifetime rules.</span></span> <span data-ttu-id="398ee-168">使用 hello 原則 toocontrol hello 屬性會指定權杖存留期。</span><span class="sxs-lookup"><span data-stu-id="398ee-168">Use hello properties of hello policy toocontrol specified token lifetimes.</span></span> <span data-ttu-id="398ee-169">如果沒有原則設定，hello 系統會強制執行 hello 預設存留時間值。</span><span class="sxs-lookup"><span data-stu-id="398ee-169">If no policy is set, hello system enforces hello default lifetime value.</span></span>

### <a name="configurable-token-lifetime-properties"></a><span data-ttu-id="398ee-170">可設定的權杖存留期屬性</span><span class="sxs-lookup"><span data-stu-id="398ee-170">Configurable token lifetime properties</span></span>
| <span data-ttu-id="398ee-171">屬性</span><span class="sxs-lookup"><span data-stu-id="398ee-171">Property</span></span> | <span data-ttu-id="398ee-172">原則屬性字串</span><span class="sxs-lookup"><span data-stu-id="398ee-172">Policy property string</span></span> | <span data-ttu-id="398ee-173">影響</span><span class="sxs-lookup"><span data-stu-id="398ee-173">Affects</span></span> | <span data-ttu-id="398ee-174">預設值</span><span class="sxs-lookup"><span data-stu-id="398ee-174">Default</span></span> | <span data-ttu-id="398ee-175">最小值</span><span class="sxs-lookup"><span data-stu-id="398ee-175">Minimum</span></span> | <span data-ttu-id="398ee-176">最大值</span><span class="sxs-lookup"><span data-stu-id="398ee-176">Maximum</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="398ee-177">存取權杖存留期</span><span class="sxs-lookup"><span data-stu-id="398ee-177">Access Token Lifetime</span></span> |<span data-ttu-id="398ee-178">AccessTokenLifetime</span><span class="sxs-lookup"><span data-stu-id="398ee-178">AccessTokenLifetime</span></span> |<span data-ttu-id="398ee-179">存取權杖、識別碼權杖、SAML2 權杖</span><span class="sxs-lookup"><span data-stu-id="398ee-179">Access tokens, ID tokens, SAML2 tokens</span></span> |<span data-ttu-id="398ee-180">1 小時</span><span class="sxs-lookup"><span data-stu-id="398ee-180">1 hour</span></span> |<span data-ttu-id="398ee-181">10 分鐘</span><span class="sxs-lookup"><span data-stu-id="398ee-181">10 minutes</span></span> |<span data-ttu-id="398ee-182">1 天</span><span class="sxs-lookup"><span data-stu-id="398ee-182">1 day</span></span> |
| <span data-ttu-id="398ee-183">重新整理權杖最大閒置時間</span><span class="sxs-lookup"><span data-stu-id="398ee-183">Refresh Token Max Inactive Time</span></span> |<span data-ttu-id="398ee-184">MaxInactiveTime</span><span class="sxs-lookup"><span data-stu-id="398ee-184">MaxInactiveTime</span></span> |<span data-ttu-id="398ee-185">重新整理權杖</span><span class="sxs-lookup"><span data-stu-id="398ee-185">Refresh tokens</span></span> |<span data-ttu-id="398ee-186">14 天</span><span class="sxs-lookup"><span data-stu-id="398ee-186">14 days</span></span> |<span data-ttu-id="398ee-187">10 分鐘</span><span class="sxs-lookup"><span data-stu-id="398ee-187">10 minutes</span></span> |<span data-ttu-id="398ee-188">90 天</span><span class="sxs-lookup"><span data-stu-id="398ee-188">90 days</span></span> |
| <span data-ttu-id="398ee-189">單一要素重新整理權杖最大壽命</span><span class="sxs-lookup"><span data-stu-id="398ee-189">Single-Factor Refresh Token Max Age</span></span> |<span data-ttu-id="398ee-190">MaxAgeSingleFactor</span><span class="sxs-lookup"><span data-stu-id="398ee-190">MaxAgeSingleFactor</span></span> |<span data-ttu-id="398ee-191">重新整理權杖 (適用於任何使用者)</span><span class="sxs-lookup"><span data-stu-id="398ee-191">Refresh tokens (for any users)</span></span> |<span data-ttu-id="398ee-192">直到撤銷為止</span><span class="sxs-lookup"><span data-stu-id="398ee-192">Until-revoked</span></span> |<span data-ttu-id="398ee-193">10 分鐘</span><span class="sxs-lookup"><span data-stu-id="398ee-193">10 minutes</span></span> |<span data-ttu-id="398ee-194">直到撤銷為止<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="398ee-194">Until-revoked<sup>1</sup></span></span> |
| <span data-ttu-id="398ee-195">多重要素重新整理權杖最大壽命</span><span class="sxs-lookup"><span data-stu-id="398ee-195">Multi-Factor Refresh Token Max Age</span></span> |<span data-ttu-id="398ee-196">MaxAgeMultiFactor</span><span class="sxs-lookup"><span data-stu-id="398ee-196">MaxAgeMultiFactor</span></span> |<span data-ttu-id="398ee-197">重新整理權杖 (適用於任何使用者)</span><span class="sxs-lookup"><span data-stu-id="398ee-197">Refresh tokens (for any users)</span></span> |<span data-ttu-id="398ee-198">直到撤銷為止</span><span class="sxs-lookup"><span data-stu-id="398ee-198">Until-revoked</span></span> |<span data-ttu-id="398ee-199">10 分鐘</span><span class="sxs-lookup"><span data-stu-id="398ee-199">10 minutes</span></span> |<span data-ttu-id="398ee-200">直到撤銷為止<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="398ee-200">Until-revoked<sup>1</sup></span></span> |
| <span data-ttu-id="398ee-201">單一要素工作階段權杖最大壽命</span><span class="sxs-lookup"><span data-stu-id="398ee-201">Single-Factor Session Token Max Age</span></span> |<span data-ttu-id="398ee-202">MaxAgeSessionSingleFactor<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="398ee-202">MaxAgeSessionSingleFactor<sup>2</sup></span></span> |<span data-ttu-id="398ee-203">工作階段權杖 (持續性和非持續性)</span><span class="sxs-lookup"><span data-stu-id="398ee-203">Session tokens (persistent and nonpersistent)</span></span> |<span data-ttu-id="398ee-204">直到撤銷為止</span><span class="sxs-lookup"><span data-stu-id="398ee-204">Until-revoked</span></span> |<span data-ttu-id="398ee-205">10 分鐘</span><span class="sxs-lookup"><span data-stu-id="398ee-205">10 minutes</span></span> |<span data-ttu-id="398ee-206">直到撤銷為止<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="398ee-206">Until-revoked<sup>1</sup></span></span> |
| <span data-ttu-id="398ee-207">多重要素工作階段權杖最大壽命</span><span class="sxs-lookup"><span data-stu-id="398ee-207">Multi-Factor Session Token Max Age</span></span> |<span data-ttu-id="398ee-208">MaxAgeSessionMultiFactor<sup>3</sup></span><span class="sxs-lookup"><span data-stu-id="398ee-208">MaxAgeSessionMultiFactor<sup>3</sup></span></span> |<span data-ttu-id="398ee-209">工作階段權杖 (持續性和非持續性)</span><span class="sxs-lookup"><span data-stu-id="398ee-209">Session tokens (persistent and nonpersistent)</span></span> |<span data-ttu-id="398ee-210">直到撤銷為止</span><span class="sxs-lookup"><span data-stu-id="398ee-210">Until-revoked</span></span> |<span data-ttu-id="398ee-211">10 分鐘</span><span class="sxs-lookup"><span data-stu-id="398ee-211">10 minutes</span></span> |<span data-ttu-id="398ee-212">直到撤銷為止<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="398ee-212">Until-revoked<sup>1</sup></span></span> |

* <span data-ttu-id="398ee-213"><sup>1</sup>365 天是 hello 明確的長度上限可設定這些屬性。</span><span class="sxs-lookup"><span data-stu-id="398ee-213"><sup>1</sup>365 days is hello maximum explicit length that can be set for these attributes.</span></span>
* <span data-ttu-id="398ee-214"><sup>2</sup>如果**MaxAgeSessionSingleFactor**未設定，這個值會採用 hello **MaxAgeSingleFactor**值。</span><span class="sxs-lookup"><span data-stu-id="398ee-214"><sup>2</sup>If  **MaxAgeSessionSingleFactor** is not set, this value takes hello **MaxAgeSingleFactor** value.</span></span> <span data-ttu-id="398ee-215">如果設定這兩個參數，hello 屬性會接受 hello （直到層已撤銷） 的預設值。</span><span class="sxs-lookup"><span data-stu-id="398ee-215">If neither parameter is set, hello property takes hello default value (until-revoked).</span></span>
* <span data-ttu-id="398ee-216"><sup>3</sup>如果**MaxAgeSessionMultiFactor**未設定，這個值會採用 hello **MaxAgeMultiFactor**值。</span><span class="sxs-lookup"><span data-stu-id="398ee-216"><sup>3</sup>If  **MaxAgeSessionMultiFactor** is not set, this value takes hello **MaxAgeMultiFactor** value.</span></span> <span data-ttu-id="398ee-217">如果設定這兩個參數，hello 屬性會接受 hello （直到層已撤銷） 的預設值。</span><span class="sxs-lookup"><span data-stu-id="398ee-217">If neither parameter is set, hello property takes hello default value (until-revoked).</span></span>

### <a name="exceptions"></a><span data-ttu-id="398ee-218">例外狀況</span><span class="sxs-lookup"><span data-stu-id="398ee-218">Exceptions</span></span>
| <span data-ttu-id="398ee-219">屬性</span><span class="sxs-lookup"><span data-stu-id="398ee-219">Property</span></span> | <span data-ttu-id="398ee-220">影響</span><span class="sxs-lookup"><span data-stu-id="398ee-220">Affects</span></span> | <span data-ttu-id="398ee-221">預設值</span><span class="sxs-lookup"><span data-stu-id="398ee-221">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="398ee-222">重新整理權杖最大壽命 (針對沒有足夠撤銷資訊的同盟使用者簽發<sup>1</sup>)</span><span class="sxs-lookup"><span data-stu-id="398ee-222">Refresh Token Max Age (issued for federated users who have insufficient revocation information<sup>1</sup>)</span></span> |<span data-ttu-id="398ee-223">重新整理權杖 (針對沒有足夠撤銷資訊的同盟使用者簽發<sup>1</sup>)</span><span class="sxs-lookup"><span data-stu-id="398ee-223">Refresh tokens (issued for federated users who have insufficient revocation information<sup>1</sup>)</span></span> |<span data-ttu-id="398ee-224">12 小時</span><span class="sxs-lookup"><span data-stu-id="398ee-224">12 hours</span></span> |
| <span data-ttu-id="398ee-225">重新整理權杖最大閒置時間 (針對機密用戶端簽發)</span><span class="sxs-lookup"><span data-stu-id="398ee-225">Refresh Token Max Inactive Time (issued for confidential clients)</span></span> |<span data-ttu-id="398ee-226">重新整理權杖 (針對機密用戶端簽發)</span><span class="sxs-lookup"><span data-stu-id="398ee-226">Refresh tokens (issued for confidential clients)</span></span> |<span data-ttu-id="398ee-227">90 天</span><span class="sxs-lookup"><span data-stu-id="398ee-227">90 days</span></span> |
| <span data-ttu-id="398ee-228">重新整理權杖最大壽命 (針對機密用戶端簽發)</span><span class="sxs-lookup"><span data-stu-id="398ee-228">Refresh Token Max Age (issued for confidential clients)</span></span> |<span data-ttu-id="398ee-229">重新整理權杖 (針對機密用戶端簽發)</span><span class="sxs-lookup"><span data-stu-id="398ee-229">Refresh tokens (issued for confidential clients)</span></span> |<span data-ttu-id="398ee-230">直到撤銷為止</span><span class="sxs-lookup"><span data-stu-id="398ee-230">Until-revoked</span></span> |

* <span data-ttu-id="398ee-231"><sup>1</sup>擁有足夠的撤銷資訊包括不需要任何使用者的同盟使用者 hello"LastPasswordChangeTimestamp 」 進行同步處理的屬性。</span><span class="sxs-lookup"><span data-stu-id="398ee-231"><sup>1</sup>Federated users who have insufficient revocation information include any users who do not have hello "LastPasswordChangeTimestamp" attribute synced.</span></span> <span data-ttu-id="398ee-232">這些使用者會獲得這個簡短的最大存留期，因為 AAD 時，無法 tooverify toorevoke 的語彙基元繫結的 tooan 舊的認證 （例如密碼已變更），和必須檢查上一步中更頻繁地 tooensure hello 使用者和相關聯的語彙基元仍在理想的永久性。</span><span class="sxs-lookup"><span data-stu-id="398ee-232">These users are given this short Max Age because AAD is unable tooverify when toorevoke tokens that are tied tooan old credential (such as a password that has been changed) and must check back in more frequently tooensure that hello user and associated tokens are still in good standing.</span></span> <span data-ttu-id="398ee-233">tooimprove 此體驗，租用戶系統管理員必須確定正在同步處理 hello"LastPasswordChangeTimestamp"屬性 （這可以設定 hello 使用者物件使用 Powershell 或透過 AADSync）。</span><span class="sxs-lookup"><span data-stu-id="398ee-233">tooimprove this experience, tenant admins must ensure that they are syncing hello “LastPasswordChangeTimestamp” attribute (this can be set on hello user object using Powershell or through AADSync).</span></span>

### <a name="policy-evaluation-and-prioritization"></a><span data-ttu-id="398ee-234">原則評估及優先順序</span><span class="sxs-lookup"><span data-stu-id="398ee-234">Policy evaluation and prioritization</span></span>
<span data-ttu-id="398ee-235">您可以建立並再指派 權杖存留期原則 tooa 特定應用程式、 tooyour 組織和 tooservice 主體。</span><span class="sxs-lookup"><span data-stu-id="398ee-235">You can create and then assign a token lifetime policy tooa specific application, tooyour organization, and tooservice principals.</span></span> <span data-ttu-id="398ee-236">多個原則可能會套用 tooa 特定應用程式。</span><span class="sxs-lookup"><span data-stu-id="398ee-236">Multiple policies might apply tooa specific application.</span></span> <span data-ttu-id="398ee-237">hello 生效的權杖存留期原則遵守下列規則：</span><span class="sxs-lookup"><span data-stu-id="398ee-237">hello token lifetime policy that takes effect follows these rules:</span></span>

* <span data-ttu-id="398ee-238">如果原則已明確指派 toohello 服務主體，它會強制執行。</span><span class="sxs-lookup"><span data-stu-id="398ee-238">If a policy is explicitly assigned toohello service principal, it is enforced.</span></span>
* <span data-ttu-id="398ee-239">如果沒有原則明確指派的 toohello 服務主體，會強制執行原則明確指派 toohello 總公司 hello 服務主體。</span><span class="sxs-lookup"><span data-stu-id="398ee-239">If no policy is explicitly assigned toohello service principal, a policy explicitly assigned toohello parent organization of hello service principal is enforced.</span></span>
* <span data-ttu-id="398ee-240">如果沒有原則明確指派 toohello 服務主體或 toohello 組織，hello 分派 toohello 應用程式的原則會強制執行。</span><span class="sxs-lookup"><span data-stu-id="398ee-240">If no policy is explicitly assigned toohello service principal or toohello organization, hello policy assigned toohello application is enforced.</span></span>
* <span data-ttu-id="398ee-241">如果沒有原則已被指派 toohello 服務主體、 hello 組織或 hello 應用程式物件，hello 的預設值會強制執行。</span><span class="sxs-lookup"><span data-stu-id="398ee-241">If no policy has been assigned toohello service principal, hello organization, or hello application object, hello default values is enforced.</span></span> <span data-ttu-id="398ee-242">(請參閱中的 hello 表格[可設定權杖存留期屬性](#configurable-token-lifetime-properties)。)</span><span class="sxs-lookup"><span data-stu-id="398ee-242">(See hello table in [Configurable token lifetime properties](#configurable-token-lifetime-properties).)</span></span>

<span data-ttu-id="398ee-243">如需 hello 應用程式與服務主體物件間的關聯性的詳細資訊，請參閱[應用程式與 Azure Active Directory 中的服務主體物件](active-directory-application-objects.md)。</span><span class="sxs-lookup"><span data-stu-id="398ee-243">For more information about hello relationship between application objects and service principal objects, see [Application and service principal objects in Azure Active Directory](active-directory-application-objects.md).</span></span>

<span data-ttu-id="398ee-244">在使用 hello 語彙基元的 hello 階段評估權杖的有效性。</span><span class="sxs-lookup"><span data-stu-id="398ee-244">A token’s validity is evaluated at hello time hello token is used.</span></span> <span data-ttu-id="398ee-245">具有 hello 正在存取的 hello 應用程式上的高優先順序的 hello 原則才會生效。</span><span class="sxs-lookup"><span data-stu-id="398ee-245">hello policy with hello highest priority on hello application that is being accessed takes effect.</span></span>

> [!NOTE]
> <span data-ttu-id="398ee-246">以下是範例案例。</span><span class="sxs-lookup"><span data-stu-id="398ee-246">Here's an example scenario.</span></span>
>
> <span data-ttu-id="398ee-247">使用者想 tooaccess 兩個 web 應用程式： Web 應用程式 A 和 Web 應用程式 b。</span><span class="sxs-lookup"><span data-stu-id="398ee-247">A user wants tooaccess two web applications: Web Application A and Web Application B.</span></span>
> 
> <span data-ttu-id="398ee-248">因素：</span><span class="sxs-lookup"><span data-stu-id="398ee-248">Factors:</span></span>
> * <span data-ttu-id="398ee-249">這兩個 web 應用程式處於 hello 相同父系的組織。</span><span class="sxs-lookup"><span data-stu-id="398ee-249">Both web applications are in hello same parent organization.</span></span>
> * <span data-ttu-id="398ee-250">具有工作階段權杖最短使用期限八個小時的權杖存留期原則 1 是設為 hello 父組織的預設值。</span><span class="sxs-lookup"><span data-stu-id="398ee-250">Token Lifetime Policy 1 with a Session Token Max Age of eight hours is set as hello parent organization’s default.</span></span>
> * <span data-ttu-id="398ee-251">Web 應用程式的一般使用 web 應用程式，而且不是連結的 tooany 原則。</span><span class="sxs-lookup"><span data-stu-id="398ee-251">Web Application A is a regular-use web application and isn’t linked tooany policies.</span></span>
> * <span data-ttu-id="398ee-252">Web 應用程式 B 適用於高度機密的程序。</span><span class="sxs-lookup"><span data-stu-id="398ee-252">Web Application B is used for highly sensitive processes.</span></span> <span data-ttu-id="398ee-253">其服務主體是連結的 tooToken 存留期原則 2，其具有工作階段權杖保留時間上限為 30 分鐘。</span><span class="sxs-lookup"><span data-stu-id="398ee-253">Its service principal is linked tooToken Lifetime Policy 2, which has a Session Token Max Age of 30 minutes.</span></span>
>
> <span data-ttu-id="398ee-254">在下午 12:00，hello 使用者啟動新的瀏覽器工作階段並嘗試 tooaccess Web 應用程式 a hello 使用者已重新導向的 tooAzure AD，並要求 toosign 中。</span><span class="sxs-lookup"><span data-stu-id="398ee-254">At 12:00 PM, hello user starts a new browser session and tries tooaccess Web Application A. hello user is redirected tooAzure AD and is asked toosign in.</span></span> <span data-ttu-id="398ee-255">這會建立具有工作階段權杖 hello 瀏覽器中的 cookie。</span><span class="sxs-lookup"><span data-stu-id="398ee-255">This creates a cookie that has a session token in hello browser.</span></span> <span data-ttu-id="398ee-256">hello 使用者是以允許 hello 使用者 tooaccess hello 應用程式識別碼權杖重新導向後的 tooWeb 應用程式 A。</span><span class="sxs-lookup"><span data-stu-id="398ee-256">hello user is redirected back tooWeb Application A with an ID token that allows hello user tooaccess hello application.</span></span>
>
> <span data-ttu-id="398ee-257">在 12:15 PM hello 的使用者嘗試 tooaccess Web 應用程式 b hello 瀏覽器重新導向 tooAzure AD，它會偵測 hello 工作階段 cookie。</span><span class="sxs-lookup"><span data-stu-id="398ee-257">At 12:15 PM, hello user tries tooaccess Web Application B. hello browser redirects tooAzure AD, which detects hello session cookie.</span></span> <span data-ttu-id="398ee-258">Web 應用程式 B 的服務主體是連結的 tooToken 存留期原則 2，但它也是有預設的權杖存留期原則 1 hello 父組織的一部分。</span><span class="sxs-lookup"><span data-stu-id="398ee-258">Web Application B’s service principal is linked tooToken Lifetime Policy 2, but it's also part of hello parent organization, with default Token Lifetime Policy 1.</span></span> <span data-ttu-id="398ee-259">權杖存留期原則 2 會生效，因為原則連結的 tooservice 主體具有的優先順序高於組織預設原則。</span><span class="sxs-lookup"><span data-stu-id="398ee-259">Token Lifetime Policy 2 takes effect because policies linked tooservice principals have a higher priority than organization default policies.</span></span> <span data-ttu-id="398ee-260">hello 工作階段權杖核發的原始內 hello 過去 30 分鐘內，因此被視為有效。</span><span class="sxs-lookup"><span data-stu-id="398ee-260">hello session token was originally issued within hello last 30 minutes, so it is considered valid.</span></span> <span data-ttu-id="398ee-261">重新導向後 tooWeb 應用程式 B 授與存取權的 ID 語彙基元與 hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="398ee-261">hello user is redirected back tooWeb Application B with an ID token that grants them access.</span></span>
>
> <span data-ttu-id="398ee-262">在下午 1:00，hello 嘗試 tooaccess Web 應用程式 a hello 使用者已重新導向的 tooAzure AD。</span><span class="sxs-lookup"><span data-stu-id="398ee-262">At 1:00 PM, hello user tries tooaccess Web Application A. hello user is redirected tooAzure AD.</span></span> <span data-ttu-id="398ee-263">Web 應用程式的不是連結的 tooany 原則，但因為它是在組織中與預設的權杖存留期原則 1 時，該原則會生效。</span><span class="sxs-lookup"><span data-stu-id="398ee-263">Web Application A is not linked tooany policies, but because it is in an organization with default Token Lifetime Policy 1, that policy takes effect.</span></span> <span data-ttu-id="398ee-264">偵測到 hello 初次發行 hello 內最後八小時的工作階段 cookie。</span><span class="sxs-lookup"><span data-stu-id="398ee-264">hello session cookie that was originally issued within hello last eight hours is detected.</span></span> <span data-ttu-id="398ee-265">hello 使用者是以無訊息模式重新導向後 tooWeb 應用程式 A 與新的 ID 語彙基元。</span><span class="sxs-lookup"><span data-stu-id="398ee-265">hello user is silently redirected back tooWeb Application A with a new ID token.</span></span> <span data-ttu-id="398ee-266">hello 使用者不是必要的 tooauthenticate。</span><span class="sxs-lookup"><span data-stu-id="398ee-266">hello user is not required tooauthenticate.</span></span>
>
> <span data-ttu-id="398ee-267">立即 hello 使用者之後，嘗試 tooaccess Web 應用程式 b hello 使用者會是重新導向的 tooAzure AD。</span><span class="sxs-lookup"><span data-stu-id="398ee-267">Immediately afterward, hello user tries tooaccess Web Application B. hello user is redirected tooAzure AD.</span></span> <span data-ttu-id="398ee-268">與先前一樣，權杖存留期原則 2 會生效。</span><span class="sxs-lookup"><span data-stu-id="398ee-268">As before, Token Lifetime Policy 2 takes effect.</span></span> <span data-ttu-id="398ee-269">Hello 使用者因為 hello 語彙基元簽發 30 分鐘以上，會提示的 tooreenter 他們登入認證。</span><span class="sxs-lookup"><span data-stu-id="398ee-269">Because hello token was issued more than 30 minutes ago, hello user is prompted tooreenter their sign-in credentials.</span></span> <span data-ttu-id="398ee-270">會簽發全新的工作階段權杖和識別碼權杖。</span><span class="sxs-lookup"><span data-stu-id="398ee-270">A brand-new session token and ID token are issued.</span></span> <span data-ttu-id="398ee-271">hello 使用者可以存取 Web 應用程式 b。</span><span class="sxs-lookup"><span data-stu-id="398ee-271">hello user can then access Web Application B.</span></span>
>
>

## <a name="configurable-policy-property-details"></a><span data-ttu-id="398ee-272">可設定的原則屬性詳細資料</span><span class="sxs-lookup"><span data-stu-id="398ee-272">Configurable policy property details</span></span>
### <a name="access-token-lifetime"></a><span data-ttu-id="398ee-273">存取權杖存留期</span><span class="sxs-lookup"><span data-stu-id="398ee-273">Access Token Lifetime</span></span>
<span data-ttu-id="398ee-274">**字串：**AccessTokenLifetime</span><span class="sxs-lookup"><span data-stu-id="398ee-274">**String:** AccessTokenLifetime</span></span>

<span data-ttu-id="398ee-275">**影像：**存取權杖、識別碼權杖</span><span class="sxs-lookup"><span data-stu-id="398ee-275">**Affects:** Access tokens, ID tokens</span></span>

<span data-ttu-id="398ee-276">**摘要：**此原則可控制將此資源的存取權杖和識別碼權杖視為有效的期限。</span><span class="sxs-lookup"><span data-stu-id="398ee-276">**Summary:** This policy controls how long access and ID tokens for this resource are considered valid.</span></span> <span data-ttu-id="398ee-277">減少 hello 存取權杖存留期屬性，可減少 hello 風險的存取權杖或正由惡意的動作項目延伸的一段時間的 ID 語彙基元。</span><span class="sxs-lookup"><span data-stu-id="398ee-277">Reducing hello Access Token Lifetime property mitigates hello risk of an access token or ID token being used by a malicious actor for an extended period of time.</span></span> <span data-ttu-id="398ee-278">（無法撤銷這些語彙基元）。hello 代價是，效能受到負面影響，因為 hello 權杖有 toobe 更常被取代。</span><span class="sxs-lookup"><span data-stu-id="398ee-278">(These tokens cannot be revoked.) hello trade-off is that performance is adversely affected, because hello tokens have toobe replaced more often.</span></span>

### <a name="refresh-token-max-inactive-time"></a><span data-ttu-id="398ee-279">重新整理權杖最大閒置時間</span><span class="sxs-lookup"><span data-stu-id="398ee-279">Refresh Token Max Inactive Time</span></span>
<span data-ttu-id="398ee-280">**字串︰**MaxInactiveTime</span><span class="sxs-lookup"><span data-stu-id="398ee-280">**String:** MaxInactiveTime</span></span>

<span data-ttu-id="398ee-281">**影響：**重新整理權杖</span><span class="sxs-lookup"><span data-stu-id="398ee-281">**Affects:** Refresh tokens</span></span>

<span data-ttu-id="398ee-282">**摘要：**此原則會控制多久重新整理權杖前可保留在用戶端也無法再使用它 tooretrieve 新存取/重新整理語彙基元組嘗試 tooaccess 此資源時。</span><span class="sxs-lookup"><span data-stu-id="398ee-282">**Summary:** This policy controls how old a refresh token can be before a client can no longer use it tooretrieve a new access/refresh token pair when attempting tooaccess this resource.</span></span> <span data-ttu-id="398ee-283">通常使用重新整理權杖時，會傳回新的重新整理權杖，因為這項原則會防止存取，如果 hello 用戶端會嘗試的 tooaccess hello 期間使用 hello 目前的重新整理語彙基元的任何資源指定的時間。</span><span class="sxs-lookup"><span data-stu-id="398ee-283">Because a new refresh token usually is returned when a refresh token is used, this policy prevents access if hello client tries tooaccess any resource by using hello current refresh token during hello specified period of time.</span></span>

<span data-ttu-id="398ee-284">此原則會強制未使用其用戶端 tooreauthenticate tooretrieve 新的重新整理權杖上的使用者。</span><span class="sxs-lookup"><span data-stu-id="398ee-284">This policy forces users who have not been active on their client tooreauthenticate tooretrieve a new refresh token.</span></span>

<span data-ttu-id="398ee-285">tooa 比 hello 單一因素語彙基元保留時間上限較低的值和 hello Multi-factor 重新整理語彙基元保留時間上限屬性必須設定 hello 重新整理語彙基元非作用中時間上限 屬性。</span><span class="sxs-lookup"><span data-stu-id="398ee-285">hello Refresh Token Max Inactive Time property must be set tooa lower value than hello Single-Factor Token Max Age and hello Multi-Factor Refresh Token Max Age properties.</span></span>

### <a name="single-factor-refresh-token-max-age"></a><span data-ttu-id="398ee-286">單一要素重新整理權杖最大壽命</span><span class="sxs-lookup"><span data-stu-id="398ee-286">Single-Factor Refresh Token Max Age</span></span>
<span data-ttu-id="398ee-287">**字串︰**MaxAgeSingleFactor</span><span class="sxs-lookup"><span data-stu-id="398ee-287">**String:** MaxAgeSingleFactor</span></span>

<span data-ttu-id="398ee-288">**影響：**重新整理權杖</span><span class="sxs-lookup"><span data-stu-id="398ee-288">**Affects:** Refresh tokens</span></span>

<span data-ttu-id="398ee-289">**摘要：**此原則可控制如何長時間的使用者可以使用新的重新整理語彙基元 tooget 存取/重新整理 token 組它們上次驗證之後已成功使用單一因素。</span><span class="sxs-lookup"><span data-stu-id="398ee-289">**Summary:** This policy controls how long a user can use a refresh token tooget a new access/refresh token pair after they last authenticated successfully by using only a single factor.</span></span> <span data-ttu-id="398ee-290">Hello 使用者的使用者驗證並接收新的重新整理語彙基元之後，可以使用 hello 重新整理權杖流程 hello 指定的時間週期。</span><span class="sxs-lookup"><span data-stu-id="398ee-290">After a user authenticates and receives a new refresh token, hello user can use hello refresh token flow for hello specified period of time.</span></span> <span data-ttu-id="398ee-291">（這是 true，只要未撤銷 hello 目前的重新整理權杖，並不處於未使用的時間超過 hello 未使用的時間）。此時，hello 使用者是強制的 tooreauthenticate tooreceive 新的重新整理權杖。</span><span class="sxs-lookup"><span data-stu-id="398ee-291">(This is true as long as hello current refresh token is not revoked, and it is not left unused for longer than hello inactive time.) At that point, hello user is forced tooreauthenticate tooreceive a new refresh token.</span></span>

<span data-ttu-id="398ee-292">減少最大存留期 hello 強制使用者 tooauthenticate 頻率。</span><span class="sxs-lookup"><span data-stu-id="398ee-292">Reducing hello max age forces users tooauthenticate more often.</span></span> <span data-ttu-id="398ee-293">因為單一因素驗證多重要素驗證比更不安全，建議您將設定這個屬性 tooa 值也就是等於 tooor 小於 hello Multi-factor 重新整理語彙基元保留時間上限 屬性。</span><span class="sxs-lookup"><span data-stu-id="398ee-293">Because single-factor authentication is considered less secure than multi-factor authentication, we recommend that you set this property tooa value that is equal tooor lesser than hello Multi-Factor Refresh Token Max Age property.</span></span>

### <a name="multi-factor-refresh-token-max-age"></a><span data-ttu-id="398ee-294">多重要素重新整理權杖最大壽命</span><span class="sxs-lookup"><span data-stu-id="398ee-294">Multi-Factor Refresh Token Max Age</span></span>
<span data-ttu-id="398ee-295">**字串︰**MaxAgeMultiFactor</span><span class="sxs-lookup"><span data-stu-id="398ee-295">**String:** MaxAgeMultiFactor</span></span>

<span data-ttu-id="398ee-296">**影響：**重新整理權杖</span><span class="sxs-lookup"><span data-stu-id="398ee-296">**Affects:** Refresh tokens</span></span>

<span data-ttu-id="398ee-297">**摘要：**此原則可控制如何長時間的使用者可以使用新的重新整理語彙基元 tooget 存取/重新整理 token 組它們上次驗證之後已成功使用多因素。</span><span class="sxs-lookup"><span data-stu-id="398ee-297">**Summary:** This policy controls how long a user can use a refresh token tooget a new access/refresh token pair after they last authenticated successfully by using multiple factors.</span></span> <span data-ttu-id="398ee-298">Hello 使用者的使用者驗證並接收新的重新整理語彙基元之後，可以使用 hello 重新整理權杖流程 hello 指定的時間週期。</span><span class="sxs-lookup"><span data-stu-id="398ee-298">After a user authenticates and receives a new refresh token, hello user can use hello refresh token flow for hello specified period of time.</span></span> <span data-ttu-id="398ee-299">（這是 true，只要未撤銷 hello 目前的重新整理權杖，並不是未使用的時間超過 hello 未使用的時間）。此時，會強制使用者 tooreauthenticate tooreceive 新的重新整理權杖。</span><span class="sxs-lookup"><span data-stu-id="398ee-299">(This is true as long as hello current refresh token is not revoked, and it is not unused for longer than hello inactive time.) At that point, users are forced tooreauthenticate tooreceive a new refresh token.</span></span>

<span data-ttu-id="398ee-300">減少最大存留期 hello 強制使用者 tooauthenticate 頻率。</span><span class="sxs-lookup"><span data-stu-id="398ee-300">Reducing hello max age forces users tooauthenticate more often.</span></span> <span data-ttu-id="398ee-301">因為單一因素驗證多重要素驗證比更不安全，我們建議您設定為大於 hello 單一因素重新整理語彙基元保留時間上限 屬性等於 tooor 這個屬性 tooa 值。</span><span class="sxs-lookup"><span data-stu-id="398ee-301">Because single-factor authentication is considered less secure than multi-factor authentication, we recommend that you set this property tooa value that is equal tooor greater than hello Single-Factor Refresh Token Max Age property.</span></span>

### <a name="single-factor-session-token-max-age"></a><span data-ttu-id="398ee-302">單一要素工作階段權杖最大壽命</span><span class="sxs-lookup"><span data-stu-id="398ee-302">Single-Factor Session Token Max Age</span></span>
<span data-ttu-id="398ee-303">**字串︰**MaxAgeSessionSingleFactor</span><span class="sxs-lookup"><span data-stu-id="398ee-303">**String:** MaxAgeSessionSingleFactor</span></span>

<span data-ttu-id="398ee-304">**影響：**工作階段權杖 (持續性和非持續性)</span><span class="sxs-lookup"><span data-stu-id="398ee-304">**Affects:** Session tokens (persistent and nonpersistent)</span></span>

<span data-ttu-id="398ee-305">**摘要：**這個原則會控制多久的使用者可以使用工作階段權杖 tooget，新的識別碼和工作階段語彙基元之後它們上次驗證成功使用單一因素。</span><span class="sxs-lookup"><span data-stu-id="398ee-305">**Summary:** This policy controls how long a user can use a session token tooget a new ID and session token after they last authenticated successfully by using only a single factor.</span></span> <span data-ttu-id="398ee-306">Hello 使用者的使用者驗證並接收新的工作階段語彙基元之後，可以使用 hello 工作階段權杖流程 hello 指定的時間週期。</span><span class="sxs-lookup"><span data-stu-id="398ee-306">After a user authenticates and receives a new session token, hello user can use hello session token flow for hello specified period of time.</span></span> <span data-ttu-id="398ee-307">（這是 true，只要 hello 目前工作階段 token 未撤銷，且尚未過期。）Hello 指定一段時間之後，hello 使用者是強制的 tooreauthenticate tooreceive 新的工作階段權杖。</span><span class="sxs-lookup"><span data-stu-id="398ee-307">(This is true as long as hello current session token is not revoked and has not expired.) After hello specified period of time, hello user is forced tooreauthenticate tooreceive a new session token.</span></span>

<span data-ttu-id="398ee-308">減少最大存留期 hello 強制使用者 tooauthenticate 頻率。</span><span class="sxs-lookup"><span data-stu-id="398ee-308">Reducing hello max age forces users tooauthenticate more often.</span></span> <span data-ttu-id="398ee-309">因為單一因素驗證多重要素驗證比更不安全，我們建議您設定這個屬性 tooa 值等於 tooor 不超過 hello Multi-factor 工作階段權杖的最大年齡屬性。</span><span class="sxs-lookup"><span data-stu-id="398ee-309">Because single-factor authentication is considered less secure than multi-factor authentication, we recommend that you set this property tooa value that is equal tooor less than hello Multi-Factor Session Token Max Age property.</span></span>

### <a name="multi-factor-session-token-max-age"></a><span data-ttu-id="398ee-310">多重要素工作階段權杖最大壽命</span><span class="sxs-lookup"><span data-stu-id="398ee-310">Multi-Factor Session Token Max Age</span></span>
<span data-ttu-id="398ee-311">**字串︰**MaxAgeSessionMultiFactor</span><span class="sxs-lookup"><span data-stu-id="398ee-311">**String:** MaxAgeSessionMultiFactor</span></span>

<span data-ttu-id="398ee-312">**影響：**工作階段權杖 (持續性和非持續性)</span><span class="sxs-lookup"><span data-stu-id="398ee-312">**Affects:** Session tokens (persistent and nonpersistent)</span></span>

<span data-ttu-id="398ee-313">**摘要：**這個原則會控制多久的使用者可以使用新識別碼和工作階段語彙基元之後的工作階段權杖的 tooget hello 它們藉由使用多因素驗證成功的最後一次。</span><span class="sxs-lookup"><span data-stu-id="398ee-313">**Summary:** This policy controls how long a user can use a session token tooget a new ID and session token after hello last time they authenticated successfully by using multiple factors.</span></span> <span data-ttu-id="398ee-314">Hello 使用者的使用者驗證並接收新的工作階段語彙基元之後，可以使用 hello 工作階段權杖流程 hello 指定的時間週期。</span><span class="sxs-lookup"><span data-stu-id="398ee-314">After a user authenticates and receives a new session token, hello user can use hello session token flow for hello specified period of time.</span></span> <span data-ttu-id="398ee-315">（這是 true，只要 hello 目前工作階段 token 未撤銷，且尚未過期。）Hello 指定一段時間之後，hello 使用者是強制的 tooreauthenticate tooreceive 新的工作階段權杖。</span><span class="sxs-lookup"><span data-stu-id="398ee-315">(This is true as long as hello current session token is not revoked and has not expired.) After hello specified period of time, hello user is forced tooreauthenticate tooreceive a new session token.</span></span>

<span data-ttu-id="398ee-316">減少最大存留期 hello 強制使用者 tooauthenticate 頻率。</span><span class="sxs-lookup"><span data-stu-id="398ee-316">Reducing hello max age forces users tooauthenticate more often.</span></span> <span data-ttu-id="398ee-317">因為單一因素驗證多重要素驗證比更不安全，我們建議您設定為大於 hello 單一因素工作階段權杖的最大 Age 屬性等於 tooor 這個屬性 tooa 值。</span><span class="sxs-lookup"><span data-stu-id="398ee-317">Because single-factor authentication is considered less secure than multi-factor authentication, we recommend that you set this property tooa value that is equal tooor greater than hello Single-Factor Session Token Max Age property.</span></span>

## <a name="example-token-lifetime-policies"></a><span data-ttu-id="398ee-318">範例權杖存留期原則</span><span class="sxs-lookup"><span data-stu-id="398ee-318">Example token lifetime policies</span></span>
<span data-ttu-id="398ee-319">當您為應用程式、服務主體及您整體組織建立及管理權杖存留期時，在 Azure AD 中許多案例都是可能的。</span><span class="sxs-lookup"><span data-stu-id="398ee-319">Many scenarios are possible in Azure AD when you can create and manage token lifetimes for apps, service principals, and your overall organization.</span></span> <span data-ttu-id="398ee-320">在本節中，我們將逐步解說一些常見的原則案例，這些案例可以協助您強制實行下列各項的新規則：</span><span class="sxs-lookup"><span data-stu-id="398ee-320">In this section, we walk through a few common policy scenarios that can help you impose new rules for:</span></span>

* <span data-ttu-id="398ee-321">權杖存留期</span><span class="sxs-lookup"><span data-stu-id="398ee-321">Token Lifetime</span></span>
* <span data-ttu-id="398ee-322">權杖最大閒置時間</span><span class="sxs-lookup"><span data-stu-id="398ee-322">Token Max Inactive Time</span></span>
* <span data-ttu-id="398ee-323">權杖最大壽命</span><span class="sxs-lookup"><span data-stu-id="398ee-323">Token Max Age</span></span>

<span data-ttu-id="398ee-324">在 hello 範例中，您可以了解如何：</span><span class="sxs-lookup"><span data-stu-id="398ee-324">In hello examples, you can learn how to:</span></span>

* <span data-ttu-id="398ee-325">管理組織的預設原則</span><span class="sxs-lookup"><span data-stu-id="398ee-325">Manage an organization's default policy</span></span>
* <span data-ttu-id="398ee-326">為 Web 登入建立原則</span><span class="sxs-lookup"><span data-stu-id="398ee-326">Create a policy for web sign-in</span></span>
* <span data-ttu-id="398ee-327">針對呼叫 Web API 的原生應用程式建立原則</span><span class="sxs-lookup"><span data-stu-id="398ee-327">Create a policy for a native app that calls a web API</span></span>
* <span data-ttu-id="398ee-328">管理進階原則</span><span class="sxs-lookup"><span data-stu-id="398ee-328">Manage an advanced policy</span></span>

### <a name="prerequisites"></a><span data-ttu-id="398ee-329">必要條件</span><span class="sxs-lookup"><span data-stu-id="398ee-329">Prerequisites</span></span>
<span data-ttu-id="398ee-330">Hello 遵循範例，在您建立、 更新連結，並刪除應用程式、 服務主體與整個組織的原則。</span><span class="sxs-lookup"><span data-stu-id="398ee-330">In hello following examples, you create, update, link, and delete policies for apps, service principals, and your overall organization.</span></span> <span data-ttu-id="398ee-331">如果您是新 tooAzure AD，我們建議您了解[tooget 的 Azure AD 的租用戶](active-directory-howto-tenant.md)繼續這些範例之前。</span><span class="sxs-lookup"><span data-stu-id="398ee-331">If you are new tooAzure AD, we recommend that you learn about [how tooget an Azure AD tenant](active-directory-howto-tenant.md) before you proceed with these examples.</span></span>  

<span data-ttu-id="398ee-332">tooget 啟動，請勿 hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="398ee-332">tooget started, do hello following steps:</span></span>

1. <span data-ttu-id="398ee-333">下載最新的 hello [Azure AD PowerShell 模組公開預覽版本](https://www.powershellgallery.com/packages/AzureADPreview)。</span><span class="sxs-lookup"><span data-stu-id="398ee-333">Download hello latest [Azure AD PowerShell Module Public Preview release](https://www.powershellgallery.com/packages/AzureADPreview).</span></span>
2. <span data-ttu-id="398ee-334">執行 hello`Connect`命令 toosign tooyour Azure AD 系統管理員帳戶中的。</span><span class="sxs-lookup"><span data-stu-id="398ee-334">Run hello `Connect` command toosign in tooyour Azure AD admin account.</span></span> <span data-ttu-id="398ee-335">您每次啟動新的工作階段時執行此命令。</span><span class="sxs-lookup"><span data-stu-id="398ee-335">Run this command each time you start a new session.</span></span>

    ```PowerShell
    Connect-AzureAD -Confirm
    ```

3. <span data-ttu-id="398ee-336">toosee 命令已建立您的組織，執行下列的 hello 中的所有原則。</span><span class="sxs-lookup"><span data-stu-id="398ee-336">toosee all policies that have been created in your organization, run hello following command.</span></span> <span data-ttu-id="398ee-337">在下列案例的 hello 的大部分作業之後執行此命令。</span><span class="sxs-lookup"><span data-stu-id="398ee-337">Run this command after most operations in hello following scenarios.</span></span> <span data-ttu-id="398ee-338">執行 hello 命令也可協助您取得 hello * * * * 的原則。</span><span class="sxs-lookup"><span data-stu-id="398ee-338">Running hello command also helps you get hello ** ** of your policies.</span></span>

    ```PowerShell
    Get-AzureADPolicy
    ```

### <a name="example-manage-an-organizations-default-policy"></a><span data-ttu-id="398ee-339">範例：管理組織的預設原則</span><span class="sxs-lookup"><span data-stu-id="398ee-339">Example: Manage an organization's default policy</span></span>
<span data-ttu-id="398ee-340">在此範例中，您會建立可讓使用者在您整個組織中降低登入頻率的原則。</span><span class="sxs-lookup"><span data-stu-id="398ee-340">In this example, you create a policy that lets your users sign in less frequently across your entire organization.</span></span> <span data-ttu-id="398ee-341">toodo，建立單一因素重新整理語彙基元，這會套用到您的組織的權杖存留期原則。</span><span class="sxs-lookup"><span data-stu-id="398ee-341">toodo this, create a token lifetime policy for Single-Factor Refresh Tokens, which is applied across your organization.</span></span> <span data-ttu-id="398ee-342">hello 原則是在您的組織和 tooeach 還沒有原則設定的服務主體的套用的 tooevery 應用程式。</span><span class="sxs-lookup"><span data-stu-id="398ee-342">hello policy is applied tooevery application in your organization, and tooeach service principal that doesn’t already have a policy set.</span></span>

1. <span data-ttu-id="398ee-343">建立權杖存留期原則。</span><span class="sxs-lookup"><span data-stu-id="398ee-343">Create a token lifetime policy.</span></span>

    1.  <span data-ttu-id="398ee-344">設定重新整理權杖單一因素 hello 太"直到-撤銷。 」</span><span class="sxs-lookup"><span data-stu-id="398ee-344">Set hello Single-Factor Refresh Token too"until-revoked."</span></span> <span data-ttu-id="398ee-345">hello 權杖尚未過期，直到已撤銷存取權。</span><span class="sxs-lookup"><span data-stu-id="398ee-345">hello token doesn't expire until access is revoked.</span></span> <span data-ttu-id="398ee-346">建立 hello 遵循原則定義：</span><span class="sxs-lookup"><span data-stu-id="398ee-346">Create hello following policy definition:</span></span>

        ```PowerShell
        @('{
            "TokenLifetimePolicy":
            {
                "Version":1,
                "MaxAgeSingleFactor":"until-revoked"
            }
        }')
        ```

    2.  <span data-ttu-id="398ee-347">toocreate hello 原則，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="398ee-347">toocreate hello policy, run hello following command:</span></span>

        ```PowerShell
        New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1, "MaxAgeSingleFactor":"until-revoked"}}') -DisplayName "OrganizationDefaultPolicyScenario" -IsOrganizationDefault $true -Type "TokenLifetimePolicy"
        ```

    3.  <span data-ttu-id="398ee-348">toosee 您新的原則和 tooget hello 原則的**ObjectId**，請執行 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="398ee-348">toosee your new policy, and tooget hello policy's **ObjectId**, run hello following command:</span></span>

        ```PowerShell
        Get-AzureADPolicy
        ```

2. <span data-ttu-id="398ee-349">更新 hello 原則。</span><span class="sxs-lookup"><span data-stu-id="398ee-349">Update hello policy.</span></span>

    <span data-ttu-id="398ee-350">您可能會決定您設定在此範例中的 hello 第一個原則不是因為您的服務需要完全相同。</span><span class="sxs-lookup"><span data-stu-id="398ee-350">You might decide that hello first policy you set in this example is not as strict as your service requires.</span></span> <span data-ttu-id="398ee-351">tooset 兩天內，在您重新整理權杖單一因素 tooexpire 執行 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="398ee-351">tooset your Single-Factor Refresh Token tooexpire in two days, run hello following command:</span></span>

    ```PowerShell
    Set-AzureADPolicy -Id <ObjectId FROM GET COMMAND> -DisplayName "OrganizationDefaultPolicyUpdatedScenario" -Definition @('{"TokenLifetimePolicy":{"Version":1,"MaxAgeSingleFactor":"2.00:00:00"}}')
    ```

### <a name="example-create-a-policy-for-web-sign-in"></a><span data-ttu-id="398ee-352">範例：為 Web 登入建立原則</span><span class="sxs-lookup"><span data-stu-id="398ee-352">Example: Create a policy for web sign-in</span></span>

<span data-ttu-id="398ee-353">在此範例中，您可以建立原則，要求使用者 tooauthenticate 更頻繁地在您 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="398ee-353">In this example, you create a policy that requires users tooauthenticate more frequently in your web app.</span></span> <span data-ttu-id="398ee-354">此原則設定的 hello 存取 ID 語彙基元的 hello 存留期和 hello 的 web 應用程式的多因素工作階段權杖 toohello 服務主體的最大存留期。</span><span class="sxs-lookup"><span data-stu-id="398ee-354">This policy sets hello lifetime of hello access/ID tokens and hello max age of a multi-factor session token toohello service principal of your web app.</span></span>

1. <span data-ttu-id="398ee-355">建立權杖存留期原則。</span><span class="sxs-lookup"><span data-stu-id="398ee-355">Create a token lifetime policy.</span></span>

    <span data-ttu-id="398ee-356">此原則，如 web 登入設定 hello 存取/識別碼權杖存留期和 hello 最大的單一因素工作階段權杖的存留期 tootwo 小時。</span><span class="sxs-lookup"><span data-stu-id="398ee-356">This policy, for web sign-in, sets hello access/ID token lifetime and hello max single-factor session token age tootwo hours.</span></span>

    1.  <span data-ttu-id="398ee-357">toocreate hello 原則，執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="398ee-357">toocreate hello policy, run this command:</span></span>

        ```PowerShell
        New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1,"AccessTokenLifetime":"02:00:00","MaxAgeSessionSingleFactor":"02:00:00"}}') -DisplayName "WebPolicyScenario" -IsOrganizationDefault $false -Type "TokenLifetimePolicy"
        ```

    2.  <span data-ttu-id="398ee-358">toosee 您新的原則和 tooget hello 原則**ObjectId**，請執行 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="398ee-358">toosee your new policy, and tooget hello policy **ObjectId**, run hello following command:</span></span>

        ```PowerShell
        Get-AzureADPolicy
        ```

2.  <span data-ttu-id="398ee-359">指派 hello 原則 tooyour 服務主體。</span><span class="sxs-lookup"><span data-stu-id="398ee-359">Assign hello policy tooyour service principal.</span></span> <span data-ttu-id="398ee-360">您也需要 tooget hello **ObjectId**服務主體。</span><span class="sxs-lookup"><span data-stu-id="398ee-360">You also need tooget hello **ObjectId** of your service principal.</span></span> 

    1.  <span data-ttu-id="398ee-361">toosee 貴組織的所有服務主體中，您可以查詢[Microsoft Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity)。</span><span class="sxs-lookup"><span data-stu-id="398ee-361">toosee all your organization's service principals, you can query [Microsoft Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity).</span></span> <span data-ttu-id="398ee-362">或者，在[Azure AD Graph 總管](https://graphexplorer.cloudapp.net/)，登入 tooyour Azure AD 帳戶。</span><span class="sxs-lookup"><span data-stu-id="398ee-362">Or, in [Azure AD Graph Explorer](https://graphexplorer.cloudapp.net/), sign in tooyour Azure AD account.</span></span>

    2.  <span data-ttu-id="398ee-363">當您擁有 hello **ObjectId**您的服務主體，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="398ee-363">When you have hello **ObjectId** of your service principal, run hello following command:</span></span>

        ```PowerShell
        Add-AzureADServicePrincipalPolicy -Id <ObjectId of hello ServicePrincipal> -RefObjectId <ObjectId of hello Policy>
        ```


### <a name="example-create-a-policy-for-a-native-app-that-calls-a-web-api"></a><span data-ttu-id="398ee-364">範例：針對呼叫 Web API 的原生應用程式建立原則</span><span class="sxs-lookup"><span data-stu-id="398ee-364">Example: Create a policy for a native app that calls a web API</span></span>
<span data-ttu-id="398ee-365">在此範例中，您可以建立原則，經常要求使用者 tooauthenticate 較少。</span><span class="sxs-lookup"><span data-stu-id="398ee-365">In this example, you create a policy that requires users tooauthenticate less frequently.</span></span> <span data-ttu-id="398ee-366">hello 原則也以增加 hello hello 使用者必須重新驗證之前，使用者可以是作用中的時間量。</span><span class="sxs-lookup"><span data-stu-id="398ee-366">hello policy also lengthens hello amount of time a user can be inactive before hello user must reauthenticate.</span></span> <span data-ttu-id="398ee-367">hello 原則會套用的 toohello web API。</span><span class="sxs-lookup"><span data-stu-id="398ee-367">hello policy is applied toohello web API.</span></span> <span data-ttu-id="398ee-368">當 hello 原生應用程式要求 hello 做為資源的 web API 時，會套用此原則。</span><span class="sxs-lookup"><span data-stu-id="398ee-368">When hello native app requests hello web API as a resource, this policy is applied.</span></span>

1. <span data-ttu-id="398ee-369">建立權杖存留期原則。</span><span class="sxs-lookup"><span data-stu-id="398ee-369">Create a token lifetime policy.</span></span>

    1.  <span data-ttu-id="398ee-370">toocreate web API，執行下列命令的 hello 嚴格的原則：</span><span class="sxs-lookup"><span data-stu-id="398ee-370">toocreate a strict policy for a web API, run hello following command:</span></span>

        ```PowerShell
        New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1,"MaxInactiveTime":"30.00:00:00","MaxAgeMultiFactor":"until-revoked","MaxAgeSingleFactor":"180.00:00:00"}}') -DisplayName "WebApiDefaultPolicyScenario" -IsOrganizationDefault $false -Type "TokenLifetimePolicy"
        ```

    2.  <span data-ttu-id="398ee-371">toosee 您新的原則和 tooget hello 原則**ObjectId**，請執行 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="398ee-371">toosee your new policy, and tooget hello policy **ObjectId**, run hello following command:</span></span>

        ```PowerShell
        Get-AzureADPolicy
        ```

2. <span data-ttu-id="398ee-372">指派 hello 原則 tooyour web API。</span><span class="sxs-lookup"><span data-stu-id="398ee-372">Assign hello policy tooyour web API.</span></span> <span data-ttu-id="398ee-373">您也需要 tooget hello **ObjectId**應用程式。</span><span class="sxs-lookup"><span data-stu-id="398ee-373">You also need tooget hello **ObjectId** of your application.</span></span> <span data-ttu-id="398ee-374">hello 您的應用程式的最佳方式 toofind **ObjectId**為 toouse hello [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="398ee-374">hello best way toofind your app's **ObjectId** is toouse hello [Azure portal](https://portal.azure.com/).</span></span>

   <span data-ttu-id="398ee-375">當您擁有 hello **ObjectId**應用程式，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="398ee-375">When you have hello **ObjectId** of your app, run hello following command:</span></span>

        ```PowerShell
        Add-AzureADApplicationPolicy -Id <ObjectId of hello Application> -RefObjectId <ObjectId of hello Policy>
        ```


### <a name="example-manage-an-advanced-policy"></a><span data-ttu-id="398ee-376">範例：管理進階原則</span><span class="sxs-lookup"><span data-stu-id="398ee-376">Example: Manage an advanced policy</span></span>
<span data-ttu-id="398ee-377">在此範例中，您可以建立幾個原則，toolearn hello 優先順序系統的運作方式。</span><span class="sxs-lookup"><span data-stu-id="398ee-377">In this example, you create a few policies, toolearn how hello priority system works.</span></span> <span data-ttu-id="398ee-378">您也可以了解如何 toomanage 是套用的 tooseveral 物件的多個原則。</span><span class="sxs-lookup"><span data-stu-id="398ee-378">You also can learn how toomanage multiple policies that are applied tooseveral objects.</span></span>

1. <span data-ttu-id="398ee-379">建立權杖存留期原則。</span><span class="sxs-lookup"><span data-stu-id="398ee-379">Create a token lifetime policy.</span></span>

    1.  <span data-ttu-id="398ee-380">toocreate 設定 hello 單一因素重新整理權杖的存留期 too30 天數，執行下列命令的 hello 的組織預設原則：</span><span class="sxs-lookup"><span data-stu-id="398ee-380">toocreate an organization default policy that sets hello Single-Factor Refresh Token lifetime too30 days, run hello following command:</span></span>

        ```PowerShell
        New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1,"MaxAgeSingleFactor":"30.00:00:00"}}') -DisplayName "ComplexPolicyScenario" -IsOrganizationDefault $true -Type "TokenLifetimePolicy"
        ```

    2.  <span data-ttu-id="398ee-381">toosee 您新的原則和 tooget hello 原則的**ObjectId**，請執行 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="398ee-381">toosee your new policy, and tooget hello policy's **ObjectId**, run hello following command:</span></span>

        ```PowerShell
        Get-AzureADPolicy
        ```

2. <span data-ttu-id="398ee-382">指派 hello 原則 tooa 服務主體。</span><span class="sxs-lookup"><span data-stu-id="398ee-382">Assign hello policy tooa service principal.</span></span>

    <span data-ttu-id="398ee-383">現在，您有套用 toohello 整個組織的原則。</span><span class="sxs-lookup"><span data-stu-id="398ee-383">Now, you have a policy that applies toohello entire organization.</span></span> <span data-ttu-id="398ee-384">您可能希望 toopreserve 這 30 天的特定服務主體，但變更 hello 組織預設原則 toohello 上限 」 直到-撤銷。 」</span><span class="sxs-lookup"><span data-stu-id="398ee-384">You might want toopreserve this 30-day policy for a specific service principal, but change hello organization default policy toohello upper limit of "until-revoked."</span></span>

    1.  <span data-ttu-id="398ee-385">toosee 貴組織的所有服務主體中，您可以查詢[Microsoft Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity)。</span><span class="sxs-lookup"><span data-stu-id="398ee-385">toosee all your organization's service principals, you can query [Microsoft Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity).</span></span> <span data-ttu-id="398ee-386">或者，在 [Azure AD Graph 總管](https://graphexplorer.cloudapp.net/)，使用您的 Azure AD 帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="398ee-386">Or, in [Azure AD Graph Explorer](https://graphexplorer.cloudapp.net/), sign in by using your Azure AD account.</span></span>

    2.  <span data-ttu-id="398ee-387">當您擁有 hello **ObjectId**您的服務主體，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="398ee-387">When you have hello **ObjectId** of your service principal, run hello following command:</span></span>

            ```PowerShell
            Add-AzureADServicePrincipalPolicy -Id <ObjectId of hello ServicePrincipal> -RefObjectId <ObjectId of hello Policy>
            ```
        
3. <span data-ttu-id="398ee-388">設定 hello `IsOrganizationDefault` toofalse 加上旗標：</span><span class="sxs-lookup"><span data-stu-id="398ee-388">Set hello `IsOrganizationDefault` flag toofalse:</span></span>

    ```PowerShell
    Set-AzureADPolicy -Id <ObjectId of Policy> -DisplayName "ComplexPolicyScenario" -IsOrganizationDefault $false
    ```

4. <span data-ttu-id="398ee-389">建立新的組織預設原則：</span><span class="sxs-lookup"><span data-stu-id="398ee-389">Create a new organization default policy:</span></span>

    ```PowerShell
    New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1,"MaxAgeSingleFactor":"until-revoked"}}') -DisplayName "ComplexPolicyScenarioTwo" -IsOrganizationDefault $true -Type "TokenLifetimePolicy"
    ```

    <span data-ttu-id="398ee-390">您現在可以 hello 原始原則連結的 tooyour 服務主體，而且 hello 新原則設定為您組織的預設原則。</span><span class="sxs-lookup"><span data-stu-id="398ee-390">You now have hello original policy linked tooyour service principal, and hello new policy is set as your organization default policy.</span></span> <span data-ttu-id="398ee-391">它是重要 tooremember，套用原則 tooservice 主體優先於組織的預設原則。</span><span class="sxs-lookup"><span data-stu-id="398ee-391">It's important tooremember that policies applied tooservice principals have priority over organization default policies.</span></span>

## <a name="cmdlet-reference"></a><span data-ttu-id="398ee-392">Cmdlet 參考</span><span class="sxs-lookup"><span data-stu-id="398ee-392">Cmdlet reference</span></span>

### <a name="manage-policies"></a><span data-ttu-id="398ee-393">管理原則</span><span class="sxs-lookup"><span data-stu-id="398ee-393">Manage policies</span></span>

<span data-ttu-id="398ee-394">您可以使用下列 cmdlet toomanage 原則 hello。</span><span class="sxs-lookup"><span data-stu-id="398ee-394">You can use hello following cmdlets toomanage policies.</span></span>

#### <a name="new-azureadpolicy"></a><span data-ttu-id="398ee-395">New-AzureADPolicy</span><span class="sxs-lookup"><span data-stu-id="398ee-395">New-AzureADPolicy</span></span>

<span data-ttu-id="398ee-396">建立新的原則。</span><span class="sxs-lookup"><span data-stu-id="398ee-396">Creates a new policy.</span></span>

```PowerShell
New-AzureADPolicy -Definition <Array of Rules> -DisplayName <Name of Policy> -IsOrganizationDefault <boolean> -Type <Policy Type>
```

| <span data-ttu-id="398ee-397">參數</span><span class="sxs-lookup"><span data-stu-id="398ee-397">Parameters</span></span> | <span data-ttu-id="398ee-398">說明</span><span class="sxs-lookup"><span data-stu-id="398ee-398">Description</span></span> | <span data-ttu-id="398ee-399">範例</span><span class="sxs-lookup"><span data-stu-id="398ee-399">Example</span></span> |
| --- | --- | --- |
| <code>&#8209;Definition</code> |<span data-ttu-id="398ee-400">其中包含所有 hello 原則的規則 stringified JSON 陣列。</span><span class="sxs-lookup"><span data-stu-id="398ee-400">Array of stringified JSON that contains all hello policy's rules.</span></span> | `-Definition @('{"TokenLifetimePolicy":{"Version":1,"MaxInactiveTime":"20:00:00"}}')` |
| <code>&#8209;DisplayName</code> |<span data-ttu-id="398ee-401">Hello 原則名稱的字串。</span><span class="sxs-lookup"><span data-stu-id="398ee-401">String of hello policy name.</span></span> |`-DisplayName "MyTokenPolicy"` |
| <code>&#8209;IsOrganizationDefault</code> |<span data-ttu-id="398ee-402">如果為 true，請為 hello 組織的預設原則設定 hello 原則。</span><span class="sxs-lookup"><span data-stu-id="398ee-402">If true, sets hello policy as hello organization's default policy.</span></span> <span data-ttu-id="398ee-403">如果為 false，則不會執行任何動作。</span><span class="sxs-lookup"><span data-stu-id="398ee-403">If false, does nothing.</span></span> |`-IsOrganizationDefault $true` |
| <code>&#8209;Type</code> |<span data-ttu-id="398ee-404">原則類型。</span><span class="sxs-lookup"><span data-stu-id="398ee-404">Type of policy.</span></span> <span data-ttu-id="398ee-405">針對權杖存留期，請一律使用 "TokenLifetimePolicy"。</span><span class="sxs-lookup"><span data-stu-id="398ee-405">For token lifetimes, always use "TokenLifetimePolicy."</span></span> | `-Type "TokenLifetimePolicy"` |
| <span data-ttu-id="398ee-406"><code>&#8209;AlternativeIdentifier</code> [選用]</span><span class="sxs-lookup"><span data-stu-id="398ee-406"><code>&#8209;AlternativeIdentifier</code> [Optional]</span></span> |<span data-ttu-id="398ee-407">設定替代識別碼 hello 原則。</span><span class="sxs-lookup"><span data-stu-id="398ee-407">Sets an alternative ID for hello policy.</span></span> |`-AlternativeIdentifier "myAltId"` |

</br></br>

#### <a name="get-azureadpolicy"></a><span data-ttu-id="398ee-408">Get-AzureADPolicy</span><span class="sxs-lookup"><span data-stu-id="398ee-408">Get-AzureADPolicy</span></span>
<span data-ttu-id="398ee-409">取得所有 Azure AD 原則或指定的原則。</span><span class="sxs-lookup"><span data-stu-id="398ee-409">Gets all Azure AD policies or a specified policy.</span></span>

```PowerShell
Get-AzureADPolicy
```

| <span data-ttu-id="398ee-410">參數</span><span class="sxs-lookup"><span data-stu-id="398ee-410">Parameters</span></span> | <span data-ttu-id="398ee-411">說明</span><span class="sxs-lookup"><span data-stu-id="398ee-411">Description</span></span> | <span data-ttu-id="398ee-412">範例</span><span class="sxs-lookup"><span data-stu-id="398ee-412">Example</span></span> |
| --- | --- | --- |
| <span data-ttu-id="398ee-413"><code>&#8209;Id</code> [選用]</span><span class="sxs-lookup"><span data-stu-id="398ee-413"><code>&#8209;Id</code> [Optional]</span></span> |<span data-ttu-id="398ee-414">**ObjectId (Id)** hello 原則，您想要。</span><span class="sxs-lookup"><span data-stu-id="398ee-414">**ObjectId (Id)** of hello policy you want.</span></span> |`-Id <ObjectId of Policy>` |

</br></br>

#### <a name="get-azureadpolicyappliedobject"></a><span data-ttu-id="398ee-415">Get-AzureADPolicyAppliedObject</span><span class="sxs-lookup"><span data-stu-id="398ee-415">Get-AzureADPolicyAppliedObject</span></span>
<span data-ttu-id="398ee-416">取得所有應用程式和服務主體的連結的 tooa 原則。</span><span class="sxs-lookup"><span data-stu-id="398ee-416">Gets all apps and service principals that are linked tooa policy.</span></span>

```PowerShell
Get-AzureADPolicyAppliedObject -Id <ObjectId of Policy>
```

| <span data-ttu-id="398ee-417">參數</span><span class="sxs-lookup"><span data-stu-id="398ee-417">Parameters</span></span> | <span data-ttu-id="398ee-418">說明</span><span class="sxs-lookup"><span data-stu-id="398ee-418">Description</span></span> | <span data-ttu-id="398ee-419">範例</span><span class="sxs-lookup"><span data-stu-id="398ee-419">Example</span></span> |
| --- | --- | --- |
| <code>&#8209;Id</code> |<span data-ttu-id="398ee-420">**ObjectId (Id)** hello 原則，您想要。</span><span class="sxs-lookup"><span data-stu-id="398ee-420">**ObjectId (Id)** of hello policy you want.</span></span> |`-Id <ObjectId of Policy>` |

</br></br>

#### <a name="set-azureadpolicy"></a><span data-ttu-id="398ee-421">Set-AzureADPolicy</span><span class="sxs-lookup"><span data-stu-id="398ee-421">Set-AzureADPolicy</span></span>
<span data-ttu-id="398ee-422">更新現有的原則。</span><span class="sxs-lookup"><span data-stu-id="398ee-422">Updates an existing policy.</span></span>

```PowerShell
Set-AzureADPolicy -Id <ObjectId of Policy> -DisplayName <string>
```

| <span data-ttu-id="398ee-423">參數</span><span class="sxs-lookup"><span data-stu-id="398ee-423">Parameters</span></span> | <span data-ttu-id="398ee-424">說明</span><span class="sxs-lookup"><span data-stu-id="398ee-424">Description</span></span> | <span data-ttu-id="398ee-425">範例</span><span class="sxs-lookup"><span data-stu-id="398ee-425">Example</span></span> |
| --- | --- | --- |
| <code>&#8209;Id</code> |<span data-ttu-id="398ee-426">**ObjectId (Id)** hello 原則，您想要。</span><span class="sxs-lookup"><span data-stu-id="398ee-426">**ObjectId (Id)** of hello policy you want.</span></span> |`-Id <ObjectId of Policy>` |
| <code>&#8209;DisplayName</code> |<span data-ttu-id="398ee-427">Hello 原則名稱的字串。</span><span class="sxs-lookup"><span data-stu-id="398ee-427">String of hello policy name.</span></span> |`-DisplayName "MyTokenPolicy"` |
| <span data-ttu-id="398ee-428"><code>&#8209;Definition</code> [選用]</span><span class="sxs-lookup"><span data-stu-id="398ee-428"><code>&#8209;Definition</code> [Optional]</span></span> |<span data-ttu-id="398ee-429">其中包含所有 hello 原則的規則 stringified JSON 陣列。</span><span class="sxs-lookup"><span data-stu-id="398ee-429">Array of stringified JSON that contains all hello policy's rules.</span></span> |`-Definition @('{"TokenLifetimePolicy":{"Version":1,"MaxInactiveTime":"20:00:00"}}')` |
| <span data-ttu-id="398ee-430"><code>&#8209;IsOrganizationDefault</code> [選用]</span><span class="sxs-lookup"><span data-stu-id="398ee-430"><code>&#8209;IsOrganizationDefault</code> [Optional]</span></span> |<span data-ttu-id="398ee-431">如果為 true，請為 hello 組織的預設原則設定 hello 原則。</span><span class="sxs-lookup"><span data-stu-id="398ee-431">If true, sets hello policy as hello organization's default policy.</span></span> <span data-ttu-id="398ee-432">如果為 false，則不會執行任何動作。</span><span class="sxs-lookup"><span data-stu-id="398ee-432">If false, does nothing.</span></span> |`-IsOrganizationDefault $true` |
| <span data-ttu-id="398ee-433"><code>&#8209;Type</code> [選用]</span><span class="sxs-lookup"><span data-stu-id="398ee-433"><code>&#8209;Type</code> [Optional]</span></span> |<span data-ttu-id="398ee-434">原則類型。</span><span class="sxs-lookup"><span data-stu-id="398ee-434">Type of policy.</span></span> <span data-ttu-id="398ee-435">針對權杖存留期，請一律使用 "TokenLifetimePolicy"。</span><span class="sxs-lookup"><span data-stu-id="398ee-435">For token lifetimes, always use "TokenLifetimePolicy."</span></span> |`-Type "TokenLifetimePolicy"` |
| <span data-ttu-id="398ee-436"><code>&#8209;AlternativeIdentifier</code> [選用]</span><span class="sxs-lookup"><span data-stu-id="398ee-436"><code>&#8209;AlternativeIdentifier</code> [Optional]</span></span> |<span data-ttu-id="398ee-437">設定替代識別碼 hello 原則。</span><span class="sxs-lookup"><span data-stu-id="398ee-437">Sets an alternative ID for hello policy.</span></span> |`-AlternativeIdentifier "myAltId"` |

</br></br>

#### <a name="remove-azureadpolicy"></a><span data-ttu-id="398ee-438">Remove-AzureADPolicy</span><span class="sxs-lookup"><span data-stu-id="398ee-438">Remove-AzureADPolicy</span></span>
<span data-ttu-id="398ee-439">刪除 hello 指定原則。</span><span class="sxs-lookup"><span data-stu-id="398ee-439">Deletes hello specified policy.</span></span>

```PowerShell
 Remove-AzureADPolicy -Id <ObjectId of Policy>
```

| <span data-ttu-id="398ee-440">參數</span><span class="sxs-lookup"><span data-stu-id="398ee-440">Parameters</span></span> | <span data-ttu-id="398ee-441">說明</span><span class="sxs-lookup"><span data-stu-id="398ee-441">Description</span></span> | <span data-ttu-id="398ee-442">範例</span><span class="sxs-lookup"><span data-stu-id="398ee-442">Example</span></span> |
| --- | --- | --- |
| <code>&#8209;Id</code> |<span data-ttu-id="398ee-443">**ObjectId (Id)** hello 原則，您想要。</span><span class="sxs-lookup"><span data-stu-id="398ee-443">**ObjectId (Id)** of hello policy you want.</span></span> | `-Id <ObjectId of Policy>` |

</br></br>

### <a name="application-policies"></a><span data-ttu-id="398ee-444">應用程式原則</span><span class="sxs-lookup"><span data-stu-id="398ee-444">Application policies</span></span>
<span data-ttu-id="398ee-445">您可以使用下列指令程式的應用程式原則的 hello。</span><span class="sxs-lookup"><span data-stu-id="398ee-445">You can use hello following cmdlets for application policies.</span></span></br></br>

#### <a name="add-azureadapplicationpolicy"></a><span data-ttu-id="398ee-446">Add-AzureADApplicationPolicy</span><span class="sxs-lookup"><span data-stu-id="398ee-446">Add-AzureADApplicationPolicy</span></span>
<span data-ttu-id="398ee-447">連結 hello 指定原則 tooan 應用程式。</span><span class="sxs-lookup"><span data-stu-id="398ee-447">Links hello specified policy tooan application.</span></span>

```PowerShell
Add-AzureADApplicationPolicy -Id <ObjectId of Application> -RefObjectId <ObjectId of Policy>
```

| <span data-ttu-id="398ee-448">參數</span><span class="sxs-lookup"><span data-stu-id="398ee-448">Parameters</span></span> | <span data-ttu-id="398ee-449">說明</span><span class="sxs-lookup"><span data-stu-id="398ee-449">Description</span></span> | <span data-ttu-id="398ee-450">範例</span><span class="sxs-lookup"><span data-stu-id="398ee-450">Example</span></span> |
| --- | --- | --- |
| <code>&#8209;Id</code> |<span data-ttu-id="398ee-451">**ObjectId (Id)** hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="398ee-451">**ObjectId (Id)** of hello application.</span></span> | `-Id <ObjectId of Application>` |
| <code>&#8209;RefObjectId</code> |<span data-ttu-id="398ee-452">**ObjectId**的 hello 原則。</span><span class="sxs-lookup"><span data-stu-id="398ee-452">**ObjectId** of hello policy.</span></span> | `-RefObjectId <ObjectId of Policy>` |

</br></br>

#### <a name="get-azureadapplicationpolicy"></a><span data-ttu-id="398ee-453">Get-AzureADApplicationPolicy</span><span class="sxs-lookup"><span data-stu-id="398ee-453">Get-AzureADApplicationPolicy</span></span>
<span data-ttu-id="398ee-454">取得 hello 原則指派 tooan 應用程式。</span><span class="sxs-lookup"><span data-stu-id="398ee-454">Gets hello policy that is assigned tooan application.</span></span>

```PowerShell
Get-AzureADApplicationPolicy -Id <ObjectId of Application>
```

| <span data-ttu-id="398ee-455">參數</span><span class="sxs-lookup"><span data-stu-id="398ee-455">Parameters</span></span> | <span data-ttu-id="398ee-456">說明</span><span class="sxs-lookup"><span data-stu-id="398ee-456">Description</span></span> | <span data-ttu-id="398ee-457">範例</span><span class="sxs-lookup"><span data-stu-id="398ee-457">Example</span></span> |
| --- | --- | --- |
| <code>&#8209;Id</code> |<span data-ttu-id="398ee-458">**ObjectId (Id)** hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="398ee-458">**ObjectId (Id)** of hello application.</span></span> | `-Id <ObjectId of Application>` |

</br></br>

#### <a name="remove-azureadapplicationpolicy"></a><span data-ttu-id="398ee-459">Remove-AzureADApplicationPolicy</span><span class="sxs-lookup"><span data-stu-id="398ee-459">Remove-AzureADApplicationPolicy</span></span>
<span data-ttu-id="398ee-460">從應用程式移除原則。</span><span class="sxs-lookup"><span data-stu-id="398ee-460">Removes a policy from an application.</span></span>

```PowerShell
Remove-AzureADApplicationPolicy -Id <ObjectId of Application> -PolicyId <ObjectId of Policy>
```

| <span data-ttu-id="398ee-461">參數</span><span class="sxs-lookup"><span data-stu-id="398ee-461">Parameters</span></span> | <span data-ttu-id="398ee-462">說明</span><span class="sxs-lookup"><span data-stu-id="398ee-462">Description</span></span> | <span data-ttu-id="398ee-463">範例</span><span class="sxs-lookup"><span data-stu-id="398ee-463">Example</span></span> |
| --- | --- | --- |
| <code>&#8209;Id</code> |<span data-ttu-id="398ee-464">**ObjectId (Id)** hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="398ee-464">**ObjectId (Id)** of hello application.</span></span> | `-Id <ObjectId of Application>` |
| <code>&#8209;PolicyId</code> |<span data-ttu-id="398ee-465">**ObjectId**的 hello 原則。</span><span class="sxs-lookup"><span data-stu-id="398ee-465">**ObjectId** of hello policy.</span></span> | `-PolicyId <ObjectId of Policy>` |

</br></br>

### <a name="service-principal-policies"></a><span data-ttu-id="398ee-466">服務主體原則</span><span class="sxs-lookup"><span data-stu-id="398ee-466">Service principal policies</span></span>
<span data-ttu-id="398ee-467">您可以使用下列指令程式的服務主體原則中的 hello。</span><span class="sxs-lookup"><span data-stu-id="398ee-467">You can use hello following cmdlets for service principal policies.</span></span>

#### <a name="add-azureadserviceprincipalpolicy"></a><span data-ttu-id="398ee-468">Add-AzureADServicePrincipalPolicy</span><span class="sxs-lookup"><span data-stu-id="398ee-468">Add-AzureADServicePrincipalPolicy</span></span>
<span data-ttu-id="398ee-469">連結 hello 指定的原則 tooa 服務主體。</span><span class="sxs-lookup"><span data-stu-id="398ee-469">Links hello specified policy tooa service principal.</span></span>

```PowerShell
Add-AzureADServicePrincipalPolicy -Id <ObjectId of ServicePrincipal> -RefObjectId <ObjectId of Policy>
```

| <span data-ttu-id="398ee-470">參數</span><span class="sxs-lookup"><span data-stu-id="398ee-470">Parameters</span></span> | <span data-ttu-id="398ee-471">說明</span><span class="sxs-lookup"><span data-stu-id="398ee-471">Description</span></span> | <span data-ttu-id="398ee-472">範例</span><span class="sxs-lookup"><span data-stu-id="398ee-472">Example</span></span> |
| --- | --- | --- |
| <code>&#8209;Id</code> |<span data-ttu-id="398ee-473">**ObjectId (Id)** hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="398ee-473">**ObjectId (Id)** of hello application.</span></span> | `-Id <ObjectId of Application>` |
| <code>&#8209;RefObjectId</code> |<span data-ttu-id="398ee-474">**ObjectId**的 hello 原則。</span><span class="sxs-lookup"><span data-stu-id="398ee-474">**ObjectId** of hello policy.</span></span> | `-RefObjectId <ObjectId of Policy>` |

</br></br>

#### <a name="get-azureadserviceprincipalpolicy"></a><span data-ttu-id="398ee-475">Get-AzureADServicePrincipalPolicy</span><span class="sxs-lookup"><span data-stu-id="398ee-475">Get-AzureADServicePrincipalPolicy</span></span>
<span data-ttu-id="398ee-476">取得任何原則連結的 toohello 指定的服務主體。</span><span class="sxs-lookup"><span data-stu-id="398ee-476">Gets any policy linked toohello specified service principal.</span></span>

```PowerShell
Get-AzureADServicePrincipalPolicy -Id <ObjectId of ServicePrincipal>
```

| <span data-ttu-id="398ee-477">參數</span><span class="sxs-lookup"><span data-stu-id="398ee-477">Parameters</span></span> | <span data-ttu-id="398ee-478">說明</span><span class="sxs-lookup"><span data-stu-id="398ee-478">Description</span></span> | <span data-ttu-id="398ee-479">範例</span><span class="sxs-lookup"><span data-stu-id="398ee-479">Example</span></span> |
| --- | --- | --- |
| <code>&#8209;Id</code> |<span data-ttu-id="398ee-480">**ObjectId (Id)** hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="398ee-480">**ObjectId (Id)** of hello application.</span></span> | `-Id <ObjectId of Application>` |

</br></br>

#### <a name="remove-azureadserviceprincipalpolicy"></a><span data-ttu-id="398ee-481">Remove-AzureADServicePrincipalPolicy</span><span class="sxs-lookup"><span data-stu-id="398ee-481">Remove-AzureADServicePrincipalPolicy</span></span>
<span data-ttu-id="398ee-482">從 hello 指定的服務主體移除 hello 原則。</span><span class="sxs-lookup"><span data-stu-id="398ee-482">Removes hello policy from hello specified service principal.</span></span>

```PowerShell
Remove-AzureADServicePrincipalPolicy -Id <ObjectId of ServicePrincipal>  -PolicyId <ObjectId of Policy>
```

| <span data-ttu-id="398ee-483">參數</span><span class="sxs-lookup"><span data-stu-id="398ee-483">Parameters</span></span> | <span data-ttu-id="398ee-484">說明</span><span class="sxs-lookup"><span data-stu-id="398ee-484">Description</span></span> | <span data-ttu-id="398ee-485">範例</span><span class="sxs-lookup"><span data-stu-id="398ee-485">Example</span></span> |
| --- | --- | --- |
| <code>&#8209;Id</code> |<span data-ttu-id="398ee-486">**ObjectId (Id)** hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="398ee-486">**ObjectId (Id)** of hello application.</span></span> | `-Id <ObjectId of Application>` |
| <code>&#8209;PolicyId</code> |<span data-ttu-id="398ee-487">**ObjectId**的 hello 原則。</span><span class="sxs-lookup"><span data-stu-id="398ee-487">**ObjectId** of hello policy.</span></span> | `-PolicyId <ObjectId of Policy>` |
