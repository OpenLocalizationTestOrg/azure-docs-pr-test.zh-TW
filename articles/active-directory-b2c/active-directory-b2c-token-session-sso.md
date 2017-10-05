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
ms.openlocfilehash: 4442174a857681adff33001e660809ec7d47ad7d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-token-session-and-single-sign-on-configuration"></a><span data-ttu-id="27860-103">Azure Active Directory B2C：權杖、工作階段及單一登入設定</span><span class="sxs-lookup"><span data-stu-id="27860-103">Azure Active Directory B2C: Token, session and single sign-on configuration</span></span>
<span data-ttu-id="27860-104">這項功能可讓您以 [每個原則為基礎](active-directory-b2c-reference-policies.md)，針對以下項目進行精細控制︰</span><span class="sxs-lookup"><span data-stu-id="27860-104">This feature gives you fine-grained control, on a [per-policy basis](active-directory-b2c-reference-policies.md), of:</span></span>

1. <span data-ttu-id="27860-105">Azure Active Directory (Azure AD) B2C 所發出之安全性權杖的存留期。</span><span class="sxs-lookup"><span data-stu-id="27860-105">Lifetimes of security tokens emitted by Azure Active Directory (Azure AD) B2C.</span></span>
2. <span data-ttu-id="27860-106">由 Azure AD B2C 管理之 Web 應用程式工作階段的存留期。</span><span class="sxs-lookup"><span data-stu-id="27860-106">Lifetimes of web application sessions managed by Azure AD B2C.</span></span>
3. <span data-ttu-id="27860-107">Azure AD B2C 所發出之安全性權杖中的重要宣告格式。</span><span class="sxs-lookup"><span data-stu-id="27860-107">Formats of important claims in the security tokens emitted by Azure AD B2C.</span></span>
4. <span data-ttu-id="27860-108">B2C 租用戶中跨越多個應用程式和原則的單一登入 (SSO) 行為。</span><span class="sxs-lookup"><span data-stu-id="27860-108">Single sign-on (SSO) behavior across multiple apps and policies in your B2C tenant.</span></span>

<span data-ttu-id="27860-109">您可以在 B2C 租用戶中使用這項功能，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="27860-109">You can use this feature in your B2C tenant as follows:</span></span>

1. <span data-ttu-id="27860-110">遵循下列步驟以 [瀏覽至 B2C 功能刀鋒視窗](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) (位於 Azure 入口網站上)。</span><span class="sxs-lookup"><span data-stu-id="27860-110">Follow these steps to [navigate to the B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on the Azure portal.</span></span>
2. <span data-ttu-id="27860-111">按一下 [登入原則] 。</span><span class="sxs-lookup"><span data-stu-id="27860-111">Click **Sign-in policies**.</span></span> <span data-ttu-id="27860-112">*附註︰這項功能適用於任何原則類型，並不限於**登入原則***。</span><span class="sxs-lookup"><span data-stu-id="27860-112">*Note: You can use this feature on any policy type, not just on **Sign-in policies***.</span></span>
3. <span data-ttu-id="27860-113">按一下原則以予以開啟。</span><span class="sxs-lookup"><span data-stu-id="27860-113">Open a policy by clicking it.</span></span> <span data-ttu-id="27860-114">例如，按一下 [B2C_1_SiIn]。</span><span class="sxs-lookup"><span data-stu-id="27860-114">For example, click on **B2C_1_SiIn**.</span></span>
4. <span data-ttu-id="27860-115">按一下刀鋒視窗頂端的 [編輯]  。</span><span class="sxs-lookup"><span data-stu-id="27860-115">Click **Edit** at the top of the blade.</span></span>
5. <span data-ttu-id="27860-116">按一下 [權杖、工作階段及單一登入設定]。</span><span class="sxs-lookup"><span data-stu-id="27860-116">Click **Token, session & single sign-on config**.</span></span>
6. <span data-ttu-id="27860-117">變更需要的項目。</span><span class="sxs-lookup"><span data-stu-id="27860-117">Make your desired changes.</span></span> <span data-ttu-id="27860-118">了解後續章節中的可用屬性。</span><span class="sxs-lookup"><span data-stu-id="27860-118">Learn about available properties in subsequent sections.</span></span>
7. <span data-ttu-id="27860-119">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="27860-119">Click **OK**.</span></span>
8. <span data-ttu-id="27860-120">按一下刀鋒視窗頂端的 [儲存]  。</span><span class="sxs-lookup"><span data-stu-id="27860-120">Click **Save** on the top of the blade.</span></span>

## <a name="token-lifetimes-configuration"></a><span data-ttu-id="27860-121">權杖存留期組態</span><span class="sxs-lookup"><span data-stu-id="27860-121">Token lifetimes configuration</span></span>
<span data-ttu-id="27860-122">Azure AD B2C 支援以 [OAuth 2.0 授權通訊協定](active-directory-b2c-reference-protocols.md) 來啟用受保護資源的安全存取。</span><span class="sxs-lookup"><span data-stu-id="27860-122">Azure AD B2C supports the [OAuth 2.0 authorization protocol](active-directory-b2c-reference-protocols.md) for enabling secure access to protected resources.</span></span> <span data-ttu-id="27860-123">為了實作這項支援，Azure AD B2C 會發出各種 [安全性權杖](active-directory-b2c-reference-tokens.md)。</span><span class="sxs-lookup"><span data-stu-id="27860-123">To implement this support, Azure AD B2C emits various [security tokens](active-directory-b2c-reference-tokens.md).</span></span> <span data-ttu-id="27860-124">以下是可用來管理 Azure AD B2C 所發出之安全性權杖存留期的屬性︰</span><span class="sxs-lookup"><span data-stu-id="27860-124">These are the properties you can use to manage lifetimes of security tokens emitted by Azure AD B2C:</span></span>

* <span data-ttu-id="27860-125">**存取和識別碼權杖存留期 (分鐘)**：用來存取受保護資源之 OAuth 2.0 持有人權杖的存留期。</span><span class="sxs-lookup"><span data-stu-id="27860-125">**Access & ID token lifetimes (minutes)**: The lifetime of the OAuth 2.0 bearer token used to gain access to a protected resource.</span></span> <span data-ttu-id="27860-126">Azure AD B2C 目前只能發出識別碼權杖。</span><span class="sxs-lookup"><span data-stu-id="27860-126">Azure AD B2C issues only ID tokens at this time.</span></span> <span data-ttu-id="27860-127">當我們加入存取權杖的支援時，這個值也會套用至存取權杖。</span><span class="sxs-lookup"><span data-stu-id="27860-127">This value would apply to access tokens as well, when we add support for them.</span></span>
  * <span data-ttu-id="27860-128">預設值 = 60 分鐘。</span><span class="sxs-lookup"><span data-stu-id="27860-128">Default = 60 minutes.</span></span>
  * <span data-ttu-id="27860-129">最小值 (含) = 5 分鐘。</span><span class="sxs-lookup"><span data-stu-id="27860-129">Minimum (inclusive) = 5 minutes.</span></span>
  * <span data-ttu-id="27860-130">最大值 (含) = 1440 分鐘。</span><span class="sxs-lookup"><span data-stu-id="27860-130">Maximum (inclusive) = 1440 minutes.</span></span>
* <span data-ttu-id="27860-131">**重新整理權杖存留期 (天)`offline_access`︰重新整理權杖可用來取得新存取權限或識別碼權杖 (如果您的應用程式已獲得** 範圍的授權，也可以選擇性地取得新重新整理權杖) 的最大期間。</span><span class="sxs-lookup"><span data-stu-id="27860-131">**Refresh token lifetime (days)**: The maximum time period before which a refresh token can be used to acquire a new access or ID token (and optionally, a new refresh token, if your application had been granted the `offline_access` scope).</span></span>
  * <span data-ttu-id="27860-132">預設值 = 14 天。</span><span class="sxs-lookup"><span data-stu-id="27860-132">Default = 14 days.</span></span>
  * <span data-ttu-id="27860-133">最小值 (含) = 1 天。</span><span class="sxs-lookup"><span data-stu-id="27860-133">Minimum (inclusive) = 1 day.</span></span>
  * <span data-ttu-id="27860-134">最大值 (含) = 90 天。</span><span class="sxs-lookup"><span data-stu-id="27860-134">Maximum (inclusive) = 90 days.</span></span>
* <span data-ttu-id="27860-135">**重新整理權杖滑動視窗存留期 (天)**︰這段時間結束後，無論應用程式取得之最新重新整理權杖的有效期間為何，使用者都必須重新驗證。</span><span class="sxs-lookup"><span data-stu-id="27860-135">**Refresh token sliding window lifetime (days)**: After this time period elapses the user is forced to re-authenticate, irrespective of the validity period of the most recent refresh token acquired by the application.</span></span> <span data-ttu-id="27860-136">唯有將參數設定為 [受限制] 時才能提供。</span><span class="sxs-lookup"><span data-stu-id="27860-136">It can only be provided if the switch is set to **Bounded**.</span></span> <span data-ttu-id="27860-137">它必須大於或等於 [重新整理權杖存留期 (天)]  值。</span><span class="sxs-lookup"><span data-stu-id="27860-137">It needs to be greater than or equal to the **Refresh token lifetime (days)** value.</span></span> <span data-ttu-id="27860-138">如果將參數設定為 [無限制] ，您便無法提供特定的值。</span><span class="sxs-lookup"><span data-stu-id="27860-138">If the switch is set to **Unbounded**, you cannot provide a specific value.</span></span>
  * <span data-ttu-id="27860-139">預設值 = 90 天。</span><span class="sxs-lookup"><span data-stu-id="27860-139">Default = 90 days.</span></span>
  * <span data-ttu-id="27860-140">最小值 (含) = 1 天。</span><span class="sxs-lookup"><span data-stu-id="27860-140">Minimum (inclusive) = 1 day.</span></span>
  * <span data-ttu-id="27860-141">最大值 (含) = 365 天。</span><span class="sxs-lookup"><span data-stu-id="27860-141">Maximum (inclusive) = 365 days.</span></span>

<span data-ttu-id="27860-142">以下是幾個可以透過這些屬性實現的使用案例︰</span><span class="sxs-lookup"><span data-stu-id="27860-142">These are a couple of use cases that you can enable using these properties:</span></span>

* <span data-ttu-id="27860-143">只要使用者在行動應用程式中持續保持作用狀態，便允許他們無限期地維持應用程式的登入狀態。</span><span class="sxs-lookup"><span data-stu-id="27860-143">Allow a user to stay signed into a mobile application indefinitely, as long as he or she is continually active on the application.</span></span> <span data-ttu-id="27860-144">透過在登入原則中將 [重新整理權杖滑動視窗存留期 (天)] 參數設定為 [無限制]，您可以實現此案例。</span><span class="sxs-lookup"><span data-stu-id="27860-144">You can do this by setting the **Refresh token sliding window lifetime (days)** switch to **Unbounded** in your sign-in policy.</span></span>
* <span data-ttu-id="27860-145">請設定適當的存取權杖存留期，以滿足業界的安全性和循規規範。</span><span class="sxs-lookup"><span data-stu-id="27860-145">Meet your industry's security and compliance requirements by setting the appropriate access token lifetimes.</span></span>

    > [!NOTE]
    > <span data-ttu-id="27860-146">這些設定不適用於密碼重設原則。</span><span class="sxs-lookup"><span data-stu-id="27860-146">These settings are not available for password reset policies.</span></span>
    > 
    > 

## <a name="token-compatibility-settings"></a><span data-ttu-id="27860-147">權杖相容性設定</span><span class="sxs-lookup"><span data-stu-id="27860-147">Token compatibility settings</span></span>
<span data-ttu-id="27860-148">我們對 Azure AD B2C 所發出之安全性權杖中的重要宣告進行了格式變更。</span><span class="sxs-lookup"><span data-stu-id="27860-148">We made formatting changes to important claims in security tokens emitted by Azure AD B2C.</span></span> <span data-ttu-id="27860-149">這都是為了改善我們的標準通訊協定支援，以及獲得更佳的協力廠商身分識別程式庫互通性。</span><span class="sxs-lookup"><span data-stu-id="27860-149">This was done to improve our standard protocol support and for better interoperability with third-party identity libraries.</span></span> <span data-ttu-id="27860-150">不過，為了避免破壞現有的應用程式，我們建立了下列可讓客戶視需要選擇加入的屬性︰</span><span class="sxs-lookup"><span data-stu-id="27860-150">However, to avoid breaking existing apps, we created the following properties to allow customers to opt-in as needed:</span></span>

* <span data-ttu-id="27860-151">**簽發者 (iss) 宣告**︰這會識別發出權杖的 Azure AD B2C 租用戶。</span><span class="sxs-lookup"><span data-stu-id="27860-151">**Issuer (iss) claim**: This identifies the Azure AD B2C tenant that issued the token.</span></span>
  * <span data-ttu-id="27860-152">`https://login.microsoftonline.com/{B2C tenant GUID}/v2.0/`︰這是預設值。</span><span class="sxs-lookup"><span data-stu-id="27860-152">`https://login.microsoftonline.com/{B2C tenant GUID}/v2.0/`: This is the default value.</span></span>
  * <span data-ttu-id="27860-153">`https://login.microsoftonline.com/tfp/{B2C tenant GUID}/{Policy ID}/v2.0/`︰此值包括 B2C 租用戶和權杖要求中所用原則的識別碼。</span><span class="sxs-lookup"><span data-stu-id="27860-153">`https://login.microsoftonline.com/tfp/{B2C tenant GUID}/{Policy ID}/v2.0/`: This value includes IDs for both the B2C tenant and the policy used in the token request.</span></span> <span data-ttu-id="27860-154">如果您的應用程式或程式庫需要符合 Azure AD B2C 與 [OpenID Connect Discovery 1.0 規格](http://openid.net/specs/openid-connect-discovery-1_0.html)，請使用此值。</span><span class="sxs-lookup"><span data-stu-id="27860-154">If your app or library needs Azure AD B2C to be compliant with the [OpenID Connect Discovery 1.0 spec](http://openid.net/specs/openid-connect-discovery-1_0.html), use this value.</span></span>
* <span data-ttu-id="27860-155">**主體 (子) 宣告**：這可識別權杖判斷提示其相關資訊的主體，亦即使用者。</span><span class="sxs-lookup"><span data-stu-id="27860-155">**Subject (sub) claim**: This identifies the entity, i.e., the user, for which the token asserts information.</span></span>
  * <span data-ttu-id="27860-156">**ObjectID**：這是預設值。</span><span class="sxs-lookup"><span data-stu-id="27860-156">**ObjectID**: This is the default value.</span></span> <span data-ttu-id="27860-157">它會將目錄中使用者的物件識別碼填入權杖中的 `sub` 宣告。</span><span class="sxs-lookup"><span data-stu-id="27860-157">It populates the object ID of the user in the directory into the `sub` claim in the token.</span></span>
  * <span data-ttu-id="27860-158">**不支援**︰這僅針對回溯相容性提供，我們建議您儘可能切換到 **ObjectID**。</span><span class="sxs-lookup"><span data-stu-id="27860-158">**Not supported**: This is only provided for backward-compatibility, and we recommend that you switch to **ObjectID** as soon as you are able to.</span></span>
* <span data-ttu-id="27860-159">**代表原則識別碼的宣告**︰這會識別其中填入權杖要求中所用原則識別碼的宣告類型。</span><span class="sxs-lookup"><span data-stu-id="27860-159">**Claim representing policy ID**: This identifies the claim type into which the policy ID used in the token request is populated.</span></span>
  * <span data-ttu-id="27860-160">**tfp**︰這是預設值。</span><span class="sxs-lookup"><span data-stu-id="27860-160">**tfp**: This is the default value.</span></span>
  * <span data-ttu-id="27860-161">**acr**︰這僅針對回溯相容性提供，我們建議您儘可能切換到 `tfp`。</span><span class="sxs-lookup"><span data-stu-id="27860-161">**acr**: This is only provided for backward-compatibility, and we recommend that you switch to `tfp` as soon as you are able to.</span></span>

## <a name="session-behavior"></a><span data-ttu-id="27860-162">工作階段行為</span><span class="sxs-lookup"><span data-stu-id="27860-162">Session behavior</span></span>
<span data-ttu-id="27860-163">Azure AD B2C 支援以 [OpenID Connect 驗證通訊協定](active-directory-b2c-reference-oidc.md) 啟用 Web 應用程式的安全登入。</span><span class="sxs-lookup"><span data-stu-id="27860-163">Azure AD B2C supports the [OpenID Connect authentication protocol](active-directory-b2c-reference-oidc.md) for enabling secure sign-in to web applications.</span></span> <span data-ttu-id="27860-164">以下是可用來管理 Web 應用程式工作階段的屬性︰</span><span class="sxs-lookup"><span data-stu-id="27860-164">These are the properties you can use to manage web application sessions:</span></span>

* <span data-ttu-id="27860-165">**Web 應用程式工作階段存留期 (分鐘)**︰在成功通過驗證時，儲存於使用者瀏覽器上的 Azure AD B2C 工作階段 Cookie 存留期。</span><span class="sxs-lookup"><span data-stu-id="27860-165">**Web app session lifetime (minutes)**: The lifetime of Azure AD B2C's session cookie stored on the user's browser upon successful authentication.</span></span>
  * <span data-ttu-id="27860-166">預設值 = 1440 分鐘。</span><span class="sxs-lookup"><span data-stu-id="27860-166">Default = 1440 minutes.</span></span>
  * <span data-ttu-id="27860-167">最小值 (含) = 15 分鐘。</span><span class="sxs-lookup"><span data-stu-id="27860-167">Minimum (inclusive) = 15 minutes.</span></span>
  * <span data-ttu-id="27860-168">最大值 (含) = 1440 分鐘。</span><span class="sxs-lookup"><span data-stu-id="27860-168">Maximum (inclusive) = 1440 minutes.</span></span>
* <span data-ttu-id="27860-169">**Web 應用程式工作階段逾時**︰如果將此參數設定為 [絕對]，使用者必須在 [Web 應用程式工作階段存留期 (分鐘)] 指定的期間結束後重新驗證。</span><span class="sxs-lookup"><span data-stu-id="27860-169">**Web app session timeout**: If this switch is set to **Absolute**, the user is forced to re-authenticate after the time period specified by **Web app session lifetime (minutes)** elapses.</span></span> <span data-ttu-id="27860-170">如果將此參數設定為 **[循環]** \(預設設定)，只要使用者在 Web 應用程式中持續保持作用狀態，他們便能維持登入狀態。</span><span class="sxs-lookup"><span data-stu-id="27860-170">If this switch is set to **Rolling** (the default setting), the user remains signed in as long as the user is continually active in your web application.</span></span>

<span data-ttu-id="27860-171">以下是幾個可以透過這些屬性實現的使用案例︰</span><span class="sxs-lookup"><span data-stu-id="27860-171">These are a couple of use cases that you can enable using these properties:</span></span>

* <span data-ttu-id="27860-172">請設定適當的 Web 應用程式工作階段存留期，以滿足業界的安全性和循規規範。</span><span class="sxs-lookup"><span data-stu-id="27860-172">Meet your industry's security and compliance requirements by setting the appropriate web application session lifetimes.</span></span>
* <span data-ttu-id="27860-173">當使用者與 Web 應用程式之高度安全組件的互動達到設定期間後，請強制他們重新驗證。</span><span class="sxs-lookup"><span data-stu-id="27860-173">Force re-authentication after a set time period during a user's interaction with a high-security part of your web application.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="27860-174">這些設定不適用於密碼重設原則。</span><span class="sxs-lookup"><span data-stu-id="27860-174">These settings are not available for password reset policies.</span></span>
    > 
    > 

## <a name="single-sign-on-sso-configuration"></a><span data-ttu-id="27860-175">單一登入組態</span><span class="sxs-lookup"><span data-stu-id="27860-175">Single sign-on (SSO) configuration</span></span>
<span data-ttu-id="27860-176">如果您的 B2C 租用戶中有多個應用程式和原則，可以使用 **單一登入設定** 屬性來管理使用者與它們之間的互動。</span><span class="sxs-lookup"><span data-stu-id="27860-176">If you have multiple applications and policies in your B2C tenant, you can manage user interactions across them using the **Single sign-on configuration** property.</span></span> <span data-ttu-id="27860-177">您可以將屬性配置為以下任一設定︰</span><span class="sxs-lookup"><span data-stu-id="27860-177">You can set the property to one of the following settings:</span></span>

* <span data-ttu-id="27860-178">**租用戶**：這是預設設定。</span><span class="sxs-lookup"><span data-stu-id="27860-178">**Tenant**: This is the default setting.</span></span> <span data-ttu-id="27860-179">此設定可允許 B2C 租用戶中的多個應用程式和原則共用同一個使用者工作階段。</span><span class="sxs-lookup"><span data-stu-id="27860-179">Using this setting allows multiple applications and policies in your B2C tenant to share the same user session.</span></span> <span data-ttu-id="27860-180">例如，一旦使用者登入應用程式 Contoso Shopping 後，他或她就可以在存取另一個應用程式 Contoso Pharmacy 時順暢地登入。</span><span class="sxs-lookup"><span data-stu-id="27860-180">For example, once a user signs into an application, Contoso Shopping, he or she can also seamlessly sign into another one, Contoso Pharmacy, upon accessing it.</span></span>
* <span data-ttu-id="27860-181">**應用程式**︰可讓您保留應用程式專用的使用者工作階段，不受其他應用程式所限制。</span><span class="sxs-lookup"><span data-stu-id="27860-181">**Application**: This allows you to maintain a user session exclusively for an application, independent of other applications.</span></span> <span data-ttu-id="27860-182">例如，如果您想讓使用者登入 Contoso Pharmacy (使用相同的認證)，即使他或她已登入 Contoso Shopping (同一個 B2C 租用戶上的另一個應用程式)。</span><span class="sxs-lookup"><span data-stu-id="27860-182">For example, if you want the user to sign in to Contoso Pharmacy (with the same credentials), even if he or she is already signed into Contoso Shopping, another application on the same B2C tenant.</span></span> 
* <span data-ttu-id="27860-183">**原則**︰可讓您保留原則專用的使用者工作階段，不論使用該使用者工作階段的應用程式為何。</span><span class="sxs-lookup"><span data-stu-id="27860-183">**Policy**: This allows you to maintain a user session exclusively for a policy, independent of the applications using it.</span></span> <span data-ttu-id="27860-184">例如，如果使用者已登入並完成多重要素驗證 (MFA) 步驟，只要與原則繫結的工作階段未過期，他們就可以取得多個應用程式較高安全性之組件的存取權限。</span><span class="sxs-lookup"><span data-stu-id="27860-184">For example, if the user has already signed in and completed a multi factor authentication (MFA) step, he or she can be given access to higher-security parts of multiple applications as long as the session tied to the policy doesn't expire.</span></span>
* <span data-ttu-id="27860-185">**已停用**︰強制使用者在每次原則執行時都必須完成整個使用者旅程。</span><span class="sxs-lookup"><span data-stu-id="27860-185">**Disabled**: This forces the user to run through the entire user journey on every execution of the policy.</span></span> <span data-ttu-id="27860-186">例如，這可讓多位使用者登入您的應用程式 (在共用桌面案例中)，即使有一位使用者在整段期間都保持登入狀態，也不受影響。</span><span class="sxs-lookup"><span data-stu-id="27860-186">For example, this will allow multiple users to sign up to your application (in a shared desktop scenario), even while a single user remains signed in during the whole time.</span></span>

    > [!NOTE]
    > <span data-ttu-id="27860-187">這些設定不適用於密碼重設原則。</span><span class="sxs-lookup"><span data-stu-id="27860-187">These settings are not available for password reset policies.</span></span>
    > 
    > 

