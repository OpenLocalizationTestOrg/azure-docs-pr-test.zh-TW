---
title: "Azure Active Directory B2C：使用自訂原則來管理 SSO 和權杖自訂 | Microsoft Docs"
description: 
services: active-directory-b2c
documentationcenter: 
author: sama
ms.assetid: eec4d418-453f-4755-8b30-5ed997841b56
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 05/02/2017
ms.author: sama
ms.openlocfilehash: b65271a22c77ea41eeec2126e4a3ad24364edd17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-manage-sso-and-token-customization-with-custom-policies"></a><span data-ttu-id="399ac-102">Azure Active Directory B2C：使用自訂原則來管理 SSO 和權杖自訂</span><span class="sxs-lookup"><span data-stu-id="399ac-102">Azure Active Directory B2C: Manage SSO and token customization with custom policies</span></span>
<span data-ttu-id="399ac-103">使用自訂原則，提供您透過內建原則 hello 相同控制您的語彙基元、 工作階段和單一登入 (SSO) 組態。</span><span class="sxs-lookup"><span data-stu-id="399ac-103">Using custom policies provides you hello same control over your token, session and single sign-on (SSO) configurations as through built-in policies.</span></span>  <span data-ttu-id="399ac-104">toolearn 存在每個設定為何，請參閱 hello 文件[這裡](#active-directory-b2c-token-session-sso)。</span><span class="sxs-lookup"><span data-stu-id="399ac-104">toolearn what each setting does, please see hello documentation [here](#active-directory-b2c-token-session-sso).</span></span>

## <a name="token-lifetimes-and-claims-configuration"></a><span data-ttu-id="399ac-105">權杖存留期和宣告組態</span><span class="sxs-lookup"><span data-stu-id="399ac-105">Token lifetimes and claims configuration</span></span>
<span data-ttu-id="399ac-106">toochange hello 設定後權杖的存留期間，您需要 tooadd`<ClaimsProviders>`元素要 tooimpact hello 信賴憑證者合作對象檔案中的 hello 原則。</span><span class="sxs-lookup"><span data-stu-id="399ac-106">toochange hello settings on your token lifetimes, you need tooadd a `<ClaimsProviders>` element in hello relying party file of hello policy you want tooimpact.</span></span>  <span data-ttu-id="399ac-107">hello`<ClaimsProviders>`元素是子系的 hello `<TrustFrameworkPolicy>`。</span><span class="sxs-lookup"><span data-stu-id="399ac-107">hello `<ClaimsProviders>` element is a child of hello `<TrustFrameworkPolicy>`.</span></span>  <span data-ttu-id="399ac-108">內部，您將需要 tooput hello 資訊會影響您的權杖存留期。</span><span class="sxs-lookup"><span data-stu-id="399ac-108">Inside you'll need tooput hello information that affects your token lifetimes.</span></span>  <span data-ttu-id="399ac-109">hello XML 看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="399ac-109">hello XML looks like this:</span></span>

```XML
<ClaimsProviders>
   <ClaimsProvider>
      <DisplayName>Token Issuer</DisplayName>
      <TechnicalProfiles>
         <TechnicalProfile Id="JwtIssuer">
            <Metadata>
               <Item Key="token_lifetime_secs">3600</Item>
               <Item Key="id_token_lifetime_secs">3600</Item>
               <Item Key="refresh_token_lifetime_secs">1209600</Item>
               <Item Key="rolling_refresh_token_lifetime_secs">7776000</Item>
               <Item Key="IssuanceClaimPattern">AuthorityAndTenantGuid</Item>
               <Item Key="AuthenticationContextReferenceClaimPattern">None</Item>
            </Metadata>
         </TechnicalProfile>
      </TechnicalProfiles>
   </ClaimsProvider>
</ClaimsProviders>
```

<span data-ttu-id="399ac-110">**存取權杖存留期**hello 的存取權杖存留期可以透過修改 hello hello 內的值變更`<Item>`以 hello Key ="token_lifetime_secs 」，以秒為單位。</span><span class="sxs-lookup"><span data-stu-id="399ac-110">**Access token lifetimes** hello access token lifetime can be changed by modifying hello value inside hello `<Item>` with hello Key="token_lifetime_secs" in seconds.</span></span>  <span data-ttu-id="399ac-111">hello 中內建的預設值為 3600 秒 （60 分鐘）。</span><span class="sxs-lookup"><span data-stu-id="399ac-111">hello default value in built-in is 3600 seconds (60 minutes).</span></span>

<span data-ttu-id="399ac-112">**識別碼權杖存留期**hello 識別碼權杖存留期可以透過修改 hello hello 內的值變更`<Item>`以 hello Key ="id_token_lifetime_secs 」，以秒為單位。</span><span class="sxs-lookup"><span data-stu-id="399ac-112">**ID token lifetime** hello ID token lifetime can be changed by modifying hello value inside hello `<Item>` with hello Key="id_token_lifetime_secs" in seconds.</span></span>  <span data-ttu-id="399ac-113">hello 中內建的預設值為 3600 秒 （60 分鐘）。</span><span class="sxs-lookup"><span data-stu-id="399ac-113">hello default value in built-in is 3600 seconds (60 minutes).</span></span>

<span data-ttu-id="399ac-114">**重新整理權杖存留期**要變更 hello 重新整理權杖存留期，請修改內 hello 的 hello 值`<Item>`以 hello Key ="refresh_token_lifetime_secs 」，以秒為單位。</span><span class="sxs-lookup"><span data-stu-id="399ac-114">**Refresh token lifetime** hello refresh token lifetime can be changed by modifying hello value inside hello `<Item>` with hello Key="refresh_token_lifetime_secs" in seconds.</span></span>  <span data-ttu-id="399ac-115">hello 中內建的預設值為 1209600 秒 （14 天）。</span><span class="sxs-lookup"><span data-stu-id="399ac-115">hello default value in built-in is 1209600 seconds (14 days).</span></span>

<span data-ttu-id="399ac-116">**重新整理權杖的滑動視窗存留期**如果您想要 tooset 滑動視窗存留期 tooyour 重新整理權杖，修改內 hello 值`<Item>`以 hello Key ="rolling_refresh_token_lifetime_secs 」，以秒為單位。</span><span class="sxs-lookup"><span data-stu-id="399ac-116">**Refresh token sliding window lifetime** If you would like tooset a sliding window lifetime tooyour refresh token, modify hello value inside `<Item>` with hello Key="rolling_refresh_token_lifetime_secs" in seconds.</span></span>  <span data-ttu-id="399ac-117">hello 中內建的預設值是 7776000 （90 天）。</span><span class="sxs-lookup"><span data-stu-id="399ac-117">hello default value in built-in is 7776000 (90 days).</span></span>  <span data-ttu-id="399ac-118">如果您不想 tooenfore 滑動視窗存留期，取代與這行：</span><span class="sxs-lookup"><span data-stu-id="399ac-118">If you don't want tooenfore a sliding window lifetime, replace this line with:</span></span>
```XML
<Item Key="allow_infinite_rolling_refresh_token">True</Item>
```

<span data-ttu-id="399ac-119">**簽發者 (iss) 宣告**如果您想 toochange hello 簽發者 (iss) 宣告，請修改 hello 值內 hello`<Item>`以 hello 索引鍵 ="IssuanceClaimPattern"。</span><span class="sxs-lookup"><span data-stu-id="399ac-119">**Issuer (iss) claim** If you want toochange hello Issuer (iss) claim, modify hello value inside hello `<Item>` with hello Key="IssuanceClaimPattern".</span></span>  <span data-ttu-id="399ac-120">hello 適用值為`AuthorityAndTenantGuid`和`AuthorityWithTfp`。</span><span class="sxs-lookup"><span data-stu-id="399ac-120">hello applicable values are `AuthorityAndTenantGuid` and `AuthorityWithTfp`.</span></span>

<span data-ttu-id="399ac-121">**設定宣告代表原則識別碼**hello 選項將此值設定為 TFP （信任架構原則） 和 ACR （驗證內容參考）。</span><span class="sxs-lookup"><span data-stu-id="399ac-121">**Setting claim representing policy ID** hello options for setting this value are TFP (trust framework policy) and ACR (authentication context reference).</span></span>  
<span data-ttu-id="399ac-122">我們建議此 tooTFP，toodo 將此設定，請確定 hello`<Item>`以 hello Key ="AuthenticationContextReferenceClaimPattern 」 存在，而且是 hello 值`None`。</span><span class="sxs-lookup"><span data-stu-id="399ac-122">We recommend setting this tooTFP, toodo this, ensure hello `<Item>` with hello Key="AuthenticationContextReferenceClaimPattern" exists and hello value is `None`.</span></span>
<span data-ttu-id="399ac-123">在您的 `<OutputClaims>` 項目中，新增這個元素︰</span><span class="sxs-lookup"><span data-stu-id="399ac-123">In your `<OutputClaims>` item, add this element:</span></span>
```XML
<OutputClaim ClaimTypeReferenceId="trustFrameworkPolicy" Required="true" DefaultValue="{policy}" />
```
<span data-ttu-id="399ac-124">ACR，移除 hello`<Item>`以 hello Key ="AuthenticationContextReferenceClaimPattern"。</span><span class="sxs-lookup"><span data-stu-id="399ac-124">For ACR, remove hello `<Item>` with hello Key="AuthenticationContextReferenceClaimPattern".</span></span>

<span data-ttu-id="399ac-125">**主體 (sub) 宣告**時，此選項預設 tooObjectID，如果您想要 tooswitch 這太`Not Supported`，請勿遵循 hello:</span><span class="sxs-lookup"><span data-stu-id="399ac-125">**Subject (sub) claim** This option is defaulted tooObjectID, if you would like tooswitch this too`Not Supported`, do hello following:</span></span>

<span data-ttu-id="399ac-126">換掉此行</span><span class="sxs-lookup"><span data-stu-id="399ac-126">Replace this line</span></span> 
```XML
<OutputClaim ClaimTypeReferenceId="objectId" PartnerClaimType="sub" />
```
<span data-ttu-id="399ac-127">改用這行︰</span><span class="sxs-lookup"><span data-stu-id="399ac-127">with this line:</span></span>
```XML
<OutputClaim ClaimTypeReferenceId="sub" />
```

## <a name="session-behavior-and-sso"></a><span data-ttu-id="399ac-128">工作階段行為和 SSO</span><span class="sxs-lookup"><span data-stu-id="399ac-128">Session behavior and SSO</span></span>
<span data-ttu-id="399ac-129">toochange 您的工作階段行為和 SSO 組態，您需要 tooadd `<UserJourneyBehaviors>` hello 內的項目`<RelyingParty>`項目。</span><span class="sxs-lookup"><span data-stu-id="399ac-129">toochange your session behavior and SSO configurations, you need tooadd a `<UserJourneyBehaviors>` element inside of hello `<RelyingParty>` element.</span></span>  <span data-ttu-id="399ac-130">hello`<UserJourneyBehaviors>`項目必須緊接在 hello `<DefaultUserJourney>`。</span><span class="sxs-lookup"><span data-stu-id="399ac-130">hello `<UserJourneyBehaviors>` element must immediately follow hello `<DefaultUserJourney>`.</span></span>  <span data-ttu-id="399ac-131">hello 內您`<UserJourneyBehavors>`項目應該看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="399ac-131">hello inside of your `<UserJourneyBehavors>` element should look like this:</span></span>

```XML
<UserJourneyBehaviors>
   <SingleSignOn Scope="Application" />
   <SessionExpiryType>Absolute</SessionExpiryType>
   <SessionExpiryInSeconds>86400</SessionExpiryInSeconds>
</UserJourneyBehaviors>
```
<span data-ttu-id="399ac-132">**單一登入 (SSO) 組態**toochange hello 單一登入設定中，您需要 toomodify hello 值`<SingleSignOn>`。</span><span class="sxs-lookup"><span data-stu-id="399ac-132">**Single sign-on (SSO) configuration** toochange hello single sign-on configuration, you need toomodify hello value of `<SingleSignOn>`.</span></span>  <span data-ttu-id="399ac-133">hello 適用值為`Tenant`， `Application`，`Policy`和`Disabled`。</span><span class="sxs-lookup"><span data-stu-id="399ac-133">hello applicable values are `Tenant`, `Application`, `Policy` and `Disabled`.</span></span> 

<span data-ttu-id="399ac-134">**Web 應用程式工作階段存留期 （分鐘）** toochange hello hello web 應用程式工作階段存留期，您需要的 hello toomodify 值`<SessionExpiryInSeconds>`項目。</span><span class="sxs-lookup"><span data-stu-id="399ac-134">**Web app session lifetime (minutes)** toochange hello hello web app session lifetime, you need toomodify value of hello `<SessionExpiryInSeconds>` element.</span></span>  <span data-ttu-id="399ac-135">內建的原則中的 hello 預設值為 86400 秒 （1440 分鐘）。</span><span class="sxs-lookup"><span data-stu-id="399ac-135">hello default value in built-in policies is 86400 seconds (1440 minutes).</span></span>

<span data-ttu-id="399ac-136">**Web 應用程式工作階段逾時**toochange hello web 應用程式工作階段逾時，您需要 toomodify hello 值`<SessionExpiryType>`。</span><span class="sxs-lookup"><span data-stu-id="399ac-136">**Web app session timeout** toochange hello web app session timeout, you need toomodify hello value of `<SessionExpiryType>`.</span></span>  <span data-ttu-id="399ac-137">hello 適用值為`Absolute`和`Rolling`。</span><span class="sxs-lookup"><span data-stu-id="399ac-137">hello applicable values are `Absolute` and `Rolling`.</span></span>
