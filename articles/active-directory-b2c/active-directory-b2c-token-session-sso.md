---
title: "Azure Active Directory B2C︰權杖、工作階段及單一登入設定 | Microsoft Docs"
description: "Azure Active Directory B2C 中的權杖、工作階段及單一登入組態"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: e78e6344-0089-49bf-8c7b-5f634326f58c
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/26/2017
ms.author: swkrish
ms.openlocfilehash: 63325ed97a7363723c97ee3a992046ebb5592662
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-token-session-and-single-sign-on-configuration"></a><span data-ttu-id="8e6aa-103">Azure Active Directory B2C：權杖、工作階段及單一登入設定</span><span class="sxs-lookup"><span data-stu-id="8e6aa-103">Azure Active Directory B2C: Token, session and single sign-on configuration</span></span>
<span data-ttu-id="8e6aa-104">這項功能可讓您以 [每個原則為基礎](active-directory-b2c-reference-policies.md)，針對以下項目進行精細控制︰</span><span class="sxs-lookup"><span data-stu-id="8e6aa-104">This feature gives you fine-grained control, on a [per-policy basis](active-directory-b2c-reference-policies.md), of:</span></span>

1. <span data-ttu-id="8e6aa-105">Azure Active Directory (Azure AD) B2C 所發出之安全性權杖的存留期。</span><span class="sxs-lookup"><span data-stu-id="8e6aa-105">Lifetimes of security tokens emitted by Azure Active Directory (Azure AD) B2C.</span></span>
2. <span data-ttu-id="8e6aa-106">由 Azure AD B2C 管理之 Web 應用程式工作階段的存留期。</span><span class="sxs-lookup"><span data-stu-id="8e6aa-106">Lifetimes of web application sessions managed by Azure AD B2C.</span></span>
3. <span data-ttu-id="8e6aa-107">重要 hello Azure AD B2C 所發出的安全性權杖中宣告的格式。</span><span class="sxs-lookup"><span data-stu-id="8e6aa-107">Formats of important claims in hello security tokens emitted by Azure AD B2C.</span></span>
4. <span data-ttu-id="8e6aa-108">B2C 租用戶中跨越多個應用程式和原則的單一登入 (SSO) 行為。</span><span class="sxs-lookup"><span data-stu-id="8e6aa-108">Single sign-on (SSO) behavior across multiple apps and policies in your B2C tenant.</span></span>

<span data-ttu-id="8e6aa-109">您可以在 B2C 租用戶中使用這項功能，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="8e6aa-109">You can use this feature in your B2C tenant as follows:</span></span>

1. <span data-ttu-id="8e6aa-110">請遵循下列步驟太[瀏覽 toohello B2C 功能刀鋒視窗](active-directory-b2c-app-registration.md#navigate-to-b2c-settings)hello Azure 入口網站上。</span><span class="sxs-lookup"><span data-stu-id="8e6aa-110">Follow these steps too[navigate toohello B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on hello Azure portal.</span></span>
2. <span data-ttu-id="8e6aa-111">按一下 [登入原則] 。</span><span class="sxs-lookup"><span data-stu-id="8e6aa-111">Click **Sign-in policies**.</span></span> <span data-ttu-id="8e6aa-112">*附註︰這項功能適用於任何原則類型，並不限於**登入原則***。</span><span class="sxs-lookup"><span data-stu-id="8e6aa-112">*Note: You can use this feature on any policy type, not just on **Sign-in policies***.</span></span>
3. <span data-ttu-id="8e6aa-113">按一下原則以予以開啟。</span><span class="sxs-lookup"><span data-stu-id="8e6aa-113">Open a policy by clicking it.</span></span> <span data-ttu-id="8e6aa-114">例如，按一下 [B2C_1_SiIn]。</span><span class="sxs-lookup"><span data-stu-id="8e6aa-114">For example, click on **B2C_1_SiIn**.</span></span>
4. <span data-ttu-id="8e6aa-115">按一下**編輯**在 hello hello 刀鋒視窗最上方。</span><span class="sxs-lookup"><span data-stu-id="8e6aa-115">Click **Edit** at hello top of hello blade.</span></span>
5. <span data-ttu-id="8e6aa-116">按一下 [權杖、工作階段及單一登入設定]。</span><span class="sxs-lookup"><span data-stu-id="8e6aa-116">Click **Token, session & single sign-on config**.</span></span>
6. <span data-ttu-id="8e6aa-117">變更需要的項目。</span><span class="sxs-lookup"><span data-stu-id="8e6aa-117">Make your desired changes.</span></span> <span data-ttu-id="8e6aa-118">了解後續章節中的可用屬性。</span><span class="sxs-lookup"><span data-stu-id="8e6aa-118">Learn about available properties in subsequent sections.</span></span>
7. <span data-ttu-id="8e6aa-119">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="8e6aa-119">Click **OK**.</span></span>
8. <span data-ttu-id="8e6aa-120">按一下**儲存**hello 頂端 hello 刀鋒視窗上。</span><span class="sxs-lookup"><span data-stu-id="8e6aa-120">Click **Save** on hello top of hello blade.</span></span>

## <a name="token-lifetimes-configuration"></a><span data-ttu-id="8e6aa-121">權杖存留期組態</span><span class="sxs-lookup"><span data-stu-id="8e6aa-121">Token lifetimes configuration</span></span>
<span data-ttu-id="8e6aa-122">Azure AD B2C 支援 hello [OAuth 2.0 授權通訊協定](active-directory-b2c-reference-protocols.md)啟用存取 tooprotected 保護資源的安全。</span><span class="sxs-lookup"><span data-stu-id="8e6aa-122">Azure AD B2C supports hello [OAuth 2.0 authorization protocol](active-directory-b2c-reference-protocols.md) for enabling secure access tooprotected resources.</span></span> <span data-ttu-id="8e6aa-123">tooimplement 各種就會發出這項支援，Azure AD B2C[安全性語彙基元](active-directory-b2c-reference-tokens.md)。</span><span class="sxs-lookup"><span data-stu-id="8e6aa-123">tooimplement this support, Azure AD B2C emits various [security tokens](active-directory-b2c-reference-tokens.md).</span></span> <span data-ttu-id="8e6aa-124">這些是您可以使用 Azure AD B2C 所發出的安全性權杖的 toomanage 存留期的 hello 屬性：</span><span class="sxs-lookup"><span data-stu-id="8e6aa-124">These are hello properties you can use toomanage lifetimes of security tokens emitted by Azure AD B2C:</span></span>

* <span data-ttu-id="8e6aa-125">**存取與 ID 權杖存留期 （分鐘）**: hello OAuth 2.0 承載權杖使用的 toogain 存取 tooa hello 存留期間受保護資源。</span><span class="sxs-lookup"><span data-stu-id="8e6aa-125">**Access & ID token lifetimes (minutes)**: hello lifetime of hello OAuth 2.0 bearer token used toogain access tooa protected resource.</span></span> <span data-ttu-id="8e6aa-126">Azure AD B2C 目前只能發出識別碼權杖。</span><span class="sxs-lookup"><span data-stu-id="8e6aa-126">Azure AD B2C issues only ID tokens at this time.</span></span> <span data-ttu-id="8e6aa-127">這個值會套用 tooaccess 語彙基元，當我們將支援加以新增。</span><span class="sxs-lookup"><span data-stu-id="8e6aa-127">This value would apply tooaccess tokens as well, when we add support for them.</span></span>
  * <span data-ttu-id="8e6aa-128">預設值 = 60 分鐘。</span><span class="sxs-lookup"><span data-stu-id="8e6aa-128">Default = 60 minutes.</span></span>
  * <span data-ttu-id="8e6aa-129">最小值 (含) = 5 分鐘。</span><span class="sxs-lookup"><span data-stu-id="8e6aa-129">Minimum (inclusive) = 5 minutes.</span></span>
  * <span data-ttu-id="8e6aa-130">最大值 (含) = 1440 分鐘。</span><span class="sxs-lookup"><span data-stu-id="8e6aa-130">Maximum (inclusive) = 1440 minutes.</span></span>
* <span data-ttu-id="8e6aa-131">**重新整理權杖存留期 （天數）**: hello 之前重新整理語彙基元可以用的 tooacquire 的最大的時間期間，新的存取或 ID 語彙基元 (並選擇性地新重新整理權杖，如果您的應用程式已被授與 hello`offline_access`範圍)。</span><span class="sxs-lookup"><span data-stu-id="8e6aa-131">**Refresh token lifetime (days)**: hello maximum time period before which a refresh token can be used tooacquire a new access or ID token (and optionally, a new refresh token, if your application had been granted hello `offline_access` scope).</span></span>
  * <span data-ttu-id="8e6aa-132">預設值 = 14 天。</span><span class="sxs-lookup"><span data-stu-id="8e6aa-132">Default = 14 days.</span></span>
  * <span data-ttu-id="8e6aa-133">最小值 (含) = 1 天。</span><span class="sxs-lookup"><span data-stu-id="8e6aa-133">Minimum (inclusive) = 1 day.</span></span>
  * <span data-ttu-id="8e6aa-134">最大值 (含) = 90 天。</span><span class="sxs-lookup"><span data-stu-id="8e6aa-134">Maximum (inclusive) = 90 days.</span></span>
* <span data-ttu-id="8e6aa-135">**重新整理權杖的滑動視窗存留期 （天數）**： 這個時間期間過後 hello 使用者強制的 toore 後的驗證，不論 hello hello hello 應用程式來取得最新重新整理權杖的有效期間。</span><span class="sxs-lookup"><span data-stu-id="8e6aa-135">**Refresh token sliding window lifetime (days)**: After this time period elapses hello user is forced toore-authenticate, irrespective of hello validity period of hello most recent refresh token acquired by hello application.</span></span> <span data-ttu-id="8e6aa-136">它可以只提供已設定太 hello 參數，如果**已繫結**。</span><span class="sxs-lookup"><span data-stu-id="8e6aa-136">It can only be provided if hello switch is set too**Bounded**.</span></span> <span data-ttu-id="8e6aa-137">需要 toobe 大於或等於 toohello**重新整理權杖的存留期 （天數）**值。</span><span class="sxs-lookup"><span data-stu-id="8e6aa-137">It needs toobe greater than or equal toohello **Refresh token lifetime (days)** value.</span></span> <span data-ttu-id="8e6aa-138">如果設定太 hello 參數**Unbounded**，您不能提供精確的值。</span><span class="sxs-lookup"><span data-stu-id="8e6aa-138">If hello switch is set too**Unbounded**, you cannot provide a specific value.</span></span>
  * <span data-ttu-id="8e6aa-139">預設值 = 90 天。</span><span class="sxs-lookup"><span data-stu-id="8e6aa-139">Default = 90 days.</span></span>
  * <span data-ttu-id="8e6aa-140">最小值 (含) = 1 天。</span><span class="sxs-lookup"><span data-stu-id="8e6aa-140">Minimum (inclusive) = 1 day.</span></span>
  * <span data-ttu-id="8e6aa-141">最大值 (含) = 365 天。</span><span class="sxs-lookup"><span data-stu-id="8e6aa-141">Maximum (inclusive) = 365 days.</span></span>

<span data-ttu-id="8e6aa-142">以下是幾個可以透過這些屬性實現的使用案例︰</span><span class="sxs-lookup"><span data-stu-id="8e6aa-142">These are a couple of use cases that you can enable using these properties:</span></span>

* <span data-ttu-id="8e6aa-143">只要他或她會持續作用中 hello 應用程式可讓使用者 toostay 無限期地登入行動應用程式。</span><span class="sxs-lookup"><span data-stu-id="8e6aa-143">Allow a user toostay signed into a mobile application indefinitely, as long as he or she is continually active on hello application.</span></span> <span data-ttu-id="8e6aa-144">您可以透過設定 hello**重新整理權杖滑動視窗存留期 （天數）**太切換**Unbounded**在您登入的原則。</span><span class="sxs-lookup"><span data-stu-id="8e6aa-144">You can do this by setting hello **Refresh token sliding window lifetime (days)** switch too**Unbounded** in your sign-in policy.</span></span>
* <span data-ttu-id="8e6aa-145">藉由設定 hello 適當的存取權杖存留期符合您的業界安全性與相容性需求。</span><span class="sxs-lookup"><span data-stu-id="8e6aa-145">Meet your industry's security and compliance requirements by setting hello appropriate access token lifetimes.</span></span>

    > [!NOTE]
    > <span data-ttu-id="8e6aa-146">這些設定不適用於密碼重設原則。</span><span class="sxs-lookup"><span data-stu-id="8e6aa-146">These settings are not available for password reset policies.</span></span>
    > 
    > 

## <a name="token-compatibility-settings"></a><span data-ttu-id="8e6aa-147">權杖相容性設定</span><span class="sxs-lookup"><span data-stu-id="8e6aa-147">Token compatibility settings</span></span>
<span data-ttu-id="8e6aa-148">我們在 Azure AD B2C 所發出的安全性權杖進行格式化變更 tooimportant 宣告。</span><span class="sxs-lookup"><span data-stu-id="8e6aa-148">We made formatting changes tooimportant claims in security tokens emitted by Azure AD B2C.</span></span> <span data-ttu-id="8e6aa-149">這是完成 tooimprove 我們的標準通訊協定支援和更佳的互通性與協力廠商身分識別的程式庫。</span><span class="sxs-lookup"><span data-stu-id="8e6aa-149">This was done tooimprove our standard protocol support and for better interoperability with third-party identity libraries.</span></span> <span data-ttu-id="8e6aa-150">不過，tooavoid 中斷現有的應用程式，我們會建立下列屬性 tooallow 客戶 tooopt-視 hello:</span><span class="sxs-lookup"><span data-stu-id="8e6aa-150">However, tooavoid breaking existing apps, we created hello following properties tooallow customers tooopt-in as needed:</span></span>

* <span data-ttu-id="8e6aa-151">**簽發者 (iss) 宣告**： 這會識別發出權杖 hello hello Azure AD B2C 租用戶。</span><span class="sxs-lookup"><span data-stu-id="8e6aa-151">**Issuer (iss) claim**: This identifies hello Azure AD B2C tenant that issued hello token.</span></span>
  * <span data-ttu-id="8e6aa-152">`https://login.microsoftonline.com/{B2C tenant GUID}/v2.0/`： 這是 hello 預設值。</span><span class="sxs-lookup"><span data-stu-id="8e6aa-152">`https://login.microsoftonline.com/{B2C tenant GUID}/v2.0/`: This is hello default value.</span></span>
  * <span data-ttu-id="8e6aa-153">`https://login.microsoftonline.com/tfp/{B2C tenant GUID}/{Policy ID}/v2.0/`： 這個值會包含識別碼 hello B2C 租用戶和 hello 原則 hello 權杖要求中使用。</span><span class="sxs-lookup"><span data-stu-id="8e6aa-153">`https://login.microsoftonline.com/tfp/{B2C tenant GUID}/{Policy ID}/v2.0/`: This value includes IDs for both hello B2C tenant and hello policy used in hello token request.</span></span> <span data-ttu-id="8e6aa-154">如果您的應用程式庫需要 Azure AD B2C toobe 符合 hello [OpenID Connect 探索 1.0 規格](http://openid.net/specs/openid-connect-discovery-1_0.html)，使用此值。</span><span class="sxs-lookup"><span data-stu-id="8e6aa-154">If your app or library needs Azure AD B2C toobe compliant with hello [OpenID Connect Discovery 1.0 spec](http://openid.net/specs/openid-connect-discovery-1_0.html), use this value.</span></span>
* <span data-ttu-id="8e6aa-155">**主體 (sub) 宣告**： 這會識別 hello 實體，也就是 hello 使用者，哪些 hello 權杖判斷提示資訊。</span><span class="sxs-lookup"><span data-stu-id="8e6aa-155">**Subject (sub) claim**: This identifies hello entity, i.e., hello user, for which hello token asserts information.</span></span>
  * <span data-ttu-id="8e6aa-156">**ObjectID**： 這是 hello 預設值。</span><span class="sxs-lookup"><span data-stu-id="8e6aa-156">**ObjectID**: This is hello default value.</span></span> <span data-ttu-id="8e6aa-157">Hello 物件識別碼 hello 目錄中的 hello 使用者填入 hello `sub` hello 權杖中宣告。</span><span class="sxs-lookup"><span data-stu-id="8e6aa-157">It populates hello object ID of hello user in hello directory into hello `sub` claim in hello token.</span></span>
  * <span data-ttu-id="8e6aa-158">**不支援**： 這只會提供回溯相容性，並建議您改用太**ObjectID**只要能夠。</span><span class="sxs-lookup"><span data-stu-id="8e6aa-158">**Not supported**: This is only provided for backward-compatibility, and we recommend that you switch too**ObjectID** as soon as you are able to.</span></span>
* <span data-ttu-id="8e6aa-159">**宣告表示原則識別碼**： 這會識別 hello 到哪一個 hello hello 權杖要求中所用的原則識別碼已填入的宣告類型。</span><span class="sxs-lookup"><span data-stu-id="8e6aa-159">**Claim representing policy ID**: This identifies hello claim type into which hello policy ID used in hello token request is populated.</span></span>
  * <span data-ttu-id="8e6aa-160">**tfp**： 這是 hello 預設值。</span><span class="sxs-lookup"><span data-stu-id="8e6aa-160">**tfp**: This is hello default value.</span></span>
  * <span data-ttu-id="8e6aa-161">**acr**： 這只會提供回溯相容性，並建議您改用太`tfp`只要能夠。</span><span class="sxs-lookup"><span data-stu-id="8e6aa-161">**acr**: This is only provided for backward-compatibility, and we recommend that you switch too`tfp` as soon as you are able to.</span></span>

## <a name="session-behavior"></a><span data-ttu-id="8e6aa-162">工作階段行為</span><span class="sxs-lookup"><span data-stu-id="8e6aa-162">Session behavior</span></span>
<span data-ttu-id="8e6aa-163">Azure AD B2C 支援 hello [OpenID Connect 的驗證通訊協定](active-directory-b2c-reference-oidc.md)用於啟用安全登入 tooweb 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8e6aa-163">Azure AD B2C supports hello [OpenID Connect authentication protocol](active-directory-b2c-reference-oidc.md) for enabling secure sign-in tooweb applications.</span></span> <span data-ttu-id="8e6aa-164">這些是您可以使用 toomanage web 應用程式工作階段的 hello 屬性：</span><span class="sxs-lookup"><span data-stu-id="8e6aa-164">These are hello properties you can use toomanage web application sessions:</span></span>

* <span data-ttu-id="8e6aa-165">**Web 應用程式工作階段存留期 （分鐘）**: hello 存留期的 Azure AD B2C 的工作階段 cookie 儲存在驗證成功後的 hello 使用者的瀏覽器上。</span><span class="sxs-lookup"><span data-stu-id="8e6aa-165">**Web app session lifetime (minutes)**: hello lifetime of Azure AD B2C's session cookie stored on hello user's browser upon successful authentication.</span></span>
  * <span data-ttu-id="8e6aa-166">預設值 = 1440 分鐘。</span><span class="sxs-lookup"><span data-stu-id="8e6aa-166">Default = 1440 minutes.</span></span>
  * <span data-ttu-id="8e6aa-167">最小值 (含) = 15 分鐘。</span><span class="sxs-lookup"><span data-stu-id="8e6aa-167">Minimum (inclusive) = 15 minutes.</span></span>
  * <span data-ttu-id="8e6aa-168">最大值 (含) = 1440 分鐘。</span><span class="sxs-lookup"><span data-stu-id="8e6aa-168">Maximum (inclusive) = 1440 minutes.</span></span>
* <span data-ttu-id="8e6aa-169">**Web 應用程式工作階段逾時**： 如果此參數設定太**絕對**，hello 使用者是強制的 toore-hello 所指定的時間週期之後驗證**Web 應用程式工作階段存留期 （分鐘）**經過。</span><span class="sxs-lookup"><span data-stu-id="8e6aa-169">**Web app session timeout**: If this switch is set too**Absolute**, hello user is forced toore-authenticate after hello time period specified by **Web app session lifetime (minutes)** elapses.</span></span> <span data-ttu-id="8e6aa-170">如果這個參數設定得**循環**(hello 預設設定)，hello 使用者仍登入，只要 hello 使用者為 web 應用程式中持續作用中。</span><span class="sxs-lookup"><span data-stu-id="8e6aa-170">If this switch is set too**Rolling** (hello default setting), hello user remains signed in as long as hello user is continually active in your web application.</span></span>

<span data-ttu-id="8e6aa-171">以下是幾個可以透過這些屬性實現的使用案例︰</span><span class="sxs-lookup"><span data-stu-id="8e6aa-171">These are a couple of use cases that you can enable using these properties:</span></span>

* <span data-ttu-id="8e6aa-172">符合產業的安全性與相容性需求設定 hello 適當的 web 應用程式工作階段存留期。</span><span class="sxs-lookup"><span data-stu-id="8e6aa-172">Meet your industry's security and compliance requirements by setting hello appropriate web application session lifetimes.</span></span>
* <span data-ttu-id="8e6aa-173">當使用者與 Web 應用程式之高度安全組件的互動達到設定期間後，請強制他們重新驗證。</span><span class="sxs-lookup"><span data-stu-id="8e6aa-173">Force re-authentication after a set time period during a user's interaction with a high-security part of your web application.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="8e6aa-174">這些設定不適用於密碼重設原則。</span><span class="sxs-lookup"><span data-stu-id="8e6aa-174">These settings are not available for password reset policies.</span></span>
    > 
    > 

## <a name="single-sign-on-sso-configuration"></a><span data-ttu-id="8e6aa-175">單一登入組態</span><span class="sxs-lookup"><span data-stu-id="8e6aa-175">Single sign-on (SSO) configuration</span></span>
<span data-ttu-id="8e6aa-176">如果您有多個應用程式和原則 B2C 租用戶中，您可以在它們之間管理使用者互動使用 hello**單一登入組態**屬性。</span><span class="sxs-lookup"><span data-stu-id="8e6aa-176">If you have multiple applications and policies in your B2C tenant, you can manage user interactions across them using hello **Single sign-on configuration** property.</span></span> <span data-ttu-id="8e6aa-177">您可以設定下列設定的 hello 的 hello 屬性 tooone:</span><span class="sxs-lookup"><span data-stu-id="8e6aa-177">You can set hello property tooone of hello following settings:</span></span>

* <span data-ttu-id="8e6aa-178">**租用戶**： 這是 hello 預設值。</span><span class="sxs-lookup"><span data-stu-id="8e6aa-178">**Tenant**: This is hello default setting.</span></span> <span data-ttu-id="8e6aa-179">使用此設定可讓多個應用程式和原則 B2C 租用戶中 tooshare hello 相同的使用者工作階段。</span><span class="sxs-lookup"><span data-stu-id="8e6aa-179">Using this setting allows multiple applications and policies in your B2C tenant tooshare hello same user session.</span></span> <span data-ttu-id="8e6aa-180">例如，一旦使用者登入應用程式 Contoso Shopping 後，他或她就可以在存取另一個應用程式 Contoso Pharmacy 時順暢地登入。</span><span class="sxs-lookup"><span data-stu-id="8e6aa-180">For example, once a user signs into an application, Contoso Shopping, he or she can also seamlessly sign into another one, Contoso Pharmacy, upon accessing it.</span></span>
* <span data-ttu-id="8e6aa-181">**應用程式**： 這可讓您 toomaintain 專用的應用程式中，獨立於其他應用程式的使用者工作階段。</span><span class="sxs-lookup"><span data-stu-id="8e6aa-181">**Application**: This allows you toomaintain a user session exclusively for an application, independent of other applications.</span></span> <span data-ttu-id="8e6aa-182">例如，如果您想要在 tooContoso 藥局 hello 使用者 toosign (hello 與相同的認證)，即使他或她會登入 Contoso 購物，另一個應用程式上 hello 相同 B2C 租用戶。</span><span class="sxs-lookup"><span data-stu-id="8e6aa-182">For example, if you want hello user toosign in tooContoso Pharmacy (with hello same credentials), even if he or she is already signed into Contoso Shopping, another application on hello same B2C tenant.</span></span> 
* <span data-ttu-id="8e6aa-183">**原則**： 這可讓您 toomaintain 專用的原則，獨立於 hello 應用程式使用的使用者工作階段。</span><span class="sxs-lookup"><span data-stu-id="8e6aa-183">**Policy**: This allows you toomaintain a user session exclusively for a policy, independent of hello applications using it.</span></span> <span data-ttu-id="8e6aa-184">例如，如果 hello 使用者已登入並完成多重要素驗證 (MFA) 步驟，他或她可以獲得 access toohigher 安全性組件的多個應用程式，只要 hello 繫結工作階段 toohello 原則不會過期。</span><span class="sxs-lookup"><span data-stu-id="8e6aa-184">For example, if hello user has already signed in and completed a multi factor authentication (MFA) step, he or she can be given access toohigher-security parts of multiple applications as long as hello session tied toohello policy doesn't expire.</span></span>
* <span data-ttu-id="8e6aa-185">**已停用**： 這會透過 hello 整個使用者之旅 hello 使用者 toorun 強制在每次執行 hello 原則。</span><span class="sxs-lookup"><span data-stu-id="8e6aa-185">**Disabled**: This forces hello user toorun through hello entire user journey on every execution of hello policy.</span></span> <span data-ttu-id="8e6aa-186">比方說，這可讓多個使用者 toosign tooyour 應用程式 （在中共用桌面的案例），甚至在單一使用者仍為 hello 整個期間已登入。</span><span class="sxs-lookup"><span data-stu-id="8e6aa-186">For example, this will allow multiple users toosign up tooyour application (in a shared desktop scenario), even while a single user remains signed in during hello whole time.</span></span>

    > [!NOTE]
    > <span data-ttu-id="8e6aa-187">這些設定不適用於密碼重設原則。</span><span class="sxs-lookup"><span data-stu-id="8e6aa-187">These settings are not available for password reset policies.</span></span>
    > 
    > 

