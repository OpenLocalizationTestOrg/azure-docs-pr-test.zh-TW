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
ms.openlocfilehash: 8f5703d15766f221517cd89352d41685652d32d6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-b2c-manage-sso-and-token-customization-with-custom-policies"></a><span data-ttu-id="407da-102">Azure Active Directory B2C：使用自訂原則來管理 SSO 和權杖自訂</span><span class="sxs-lookup"><span data-stu-id="407da-102">Azure Active Directory B2C: Manage SSO and token customization with custom policies</span></span>
<span data-ttu-id="407da-103">使用自訂原則所提供給您的控制項和透過內建原則所取到的控制項相同，均可讓您控制權杖、工作階段和單一登入 (SSO) 組態。</span><span class="sxs-lookup"><span data-stu-id="407da-103">Using custom policies provides you the same control over your token, session and single sign-on (SSO) configurations as through built-in policies.</span></span>  <span data-ttu-id="407da-104">若要了解每個設定的功用，請參閱[這裡](#active-directory-b2c-token-session-sso)的文件。</span><span class="sxs-lookup"><span data-stu-id="407da-104">To learn what each setting does, please see the documentation [here](#active-directory-b2c-token-session-sso).</span></span>

## <a name="token-lifetimes-and-claims-configuration"></a><span data-ttu-id="407da-105">權杖存留期和宣告組態</span><span class="sxs-lookup"><span data-stu-id="407da-105">Token lifetimes and claims configuration</span></span>
<span data-ttu-id="407da-106">若要變更權杖存留期的設定，您必須在想要影響之原則的信賴憑證者中，新增 `<ClaimsProviders>`元素。</span><span class="sxs-lookup"><span data-stu-id="407da-106">To change the settings on your token lifetimes, you need to add a `<ClaimsProviders>` element in the relying party file of the policy you want to impact.</span></span>  <span data-ttu-id="407da-107">`<ClaimsProviders>` 元素是 `<TrustFrameworkPolicy>` 的子系。</span><span class="sxs-lookup"><span data-stu-id="407da-107">The `<ClaimsProviders>` element is a child of the `<TrustFrameworkPolicy>`.</span></span>  <span data-ttu-id="407da-108">您必須在其中放入會影響權杖存留期的資訊。</span><span class="sxs-lookup"><span data-stu-id="407da-108">Inside you'll need to put the information that affects your token lifetimes.</span></span>  <span data-ttu-id="407da-109">XML 看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="407da-109">The XML looks like this:</span></span>

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

<span data-ttu-id="407da-110">**存取權杖存留期** 使用 Key="token_lifetime_secs" (以秒為單位) 修改 `<Item>` 內的值，即可變更存取權杖存留期。</span><span class="sxs-lookup"><span data-stu-id="407da-110">**Access token lifetimes** The access token lifetime can be changed by modifying the value inside the `<Item>` with the Key="token_lifetime_secs" in seconds.</span></span>  <span data-ttu-id="407da-111">內建的預設值為 3600 秒 (60 分鐘)。</span><span class="sxs-lookup"><span data-stu-id="407da-111">The default value in built-in is 3600 seconds (60 minutes).</span></span>

<span data-ttu-id="407da-112">**識別碼權杖存留期** 使用 Key="id_token_lifetime_secs" (以秒為單位) 修改 `<Item>` 內的值，即可變更識別碼權杖存留期。</span><span class="sxs-lookup"><span data-stu-id="407da-112">**ID token lifetime** The ID token lifetime can be changed by modifying the value inside the `<Item>` with the Key="id_token_lifetime_secs" in seconds.</span></span>  <span data-ttu-id="407da-113">內建的預設值為 3600 秒 (60 分鐘)。</span><span class="sxs-lookup"><span data-stu-id="407da-113">The default value in built-in is 3600 seconds (60 minutes).</span></span>

<span data-ttu-id="407da-114">**重新整理權杖存留期** 使用 Key="refresh_token_lifetime_secs" (以秒為單位) 修改 `<Item>` 內的值，即可變更重新整理權杖存留期。</span><span class="sxs-lookup"><span data-stu-id="407da-114">**Refresh token lifetime** The refresh token lifetime can be changed by modifying the value inside the `<Item>` with the Key="refresh_token_lifetime_secs" in seconds.</span></span>  <span data-ttu-id="407da-115">內建的預設值為 1209600 秒 (14 天)。</span><span class="sxs-lookup"><span data-stu-id="407da-115">The default value in built-in is 1209600 seconds (14 days).</span></span>

<span data-ttu-id="407da-116">**重新整理權杖滑動時間範圍存留期** 如果您想要對重新整理權杖設定滑動時間範圍存留期，請使用 Key="rolling_refresh_token_lifetime_secs" (以秒為單位) 修改 `<Item>` 內的值。</span><span class="sxs-lookup"><span data-stu-id="407da-116">**Refresh token sliding window lifetime** If you would like to set a sliding window lifetime to your refresh token, modify the value inside `<Item>` with the Key="rolling_refresh_token_lifetime_secs" in seconds.</span></span>  <span data-ttu-id="407da-117">內建的預設值為 7776000 (90 天)。</span><span class="sxs-lookup"><span data-stu-id="407da-117">The default value in built-in is 7776000 (90 days).</span></span>  <span data-ttu-id="407da-118">如果您不想要強制執行滑動時間範圍存留期，請將此行改為︰</span><span class="sxs-lookup"><span data-stu-id="407da-118">If you don't want to enfore a sliding window lifetime, replace this line with:</span></span>
```XML
<Item Key="allow_infinite_rolling_refresh_token">True</Item>
```

<span data-ttu-id="407da-119">**簽發者 (iss) 宣告** 如果您想要變更簽發者 (iss) 宣告，請使用 Key="IssuanceClaimPattern" 修改 `<Item>` 內的值。</span><span class="sxs-lookup"><span data-stu-id="407da-119">**Issuer (iss) claim** If you want to change the Issuer (iss) claim, modify the value inside the `<Item>` with the Key="IssuanceClaimPattern".</span></span>  <span data-ttu-id="407da-120">適用的值為 `AuthorityAndTenantGuid` 和 `AuthorityWithTfp`。</span><span class="sxs-lookup"><span data-stu-id="407da-120">The applicable values are `AuthorityAndTenantGuid` and `AuthorityWithTfp`.</span></span>

<span data-ttu-id="407da-121">**設定代表原則識別碼的宣告** 用來設定此值的選項為 TFP (信任架構原則) 和 ACR (驗證內容參考)。</span><span class="sxs-lookup"><span data-stu-id="407da-121">**Setting claim representing policy ID** The options for setting this value are TFP (trust framework policy) and ACR (authentication context reference).</span></span>  
<span data-ttu-id="407da-122">我們的建議是將此值設定為 TFP，若要這樣做，請確定 Key="AuthenticationContextReferenceClaimPattern" 的 `<Item>` 存在，且值為 `None`。</span><span class="sxs-lookup"><span data-stu-id="407da-122">We recommend setting this to TFP, to do this, ensure the `<Item>` with the Key="AuthenticationContextReferenceClaimPattern" exists and the value is `None`.</span></span>
<span data-ttu-id="407da-123">在您的 `<OutputClaims>` 項目中，新增這個元素︰</span><span class="sxs-lookup"><span data-stu-id="407da-123">In your `<OutputClaims>` item, add this element:</span></span>
```XML
<OutputClaim ClaimTypeReferenceId="trustFrameworkPolicy" Required="true" DefaultValue="{policy}" />
```
<span data-ttu-id="407da-124">若設定為 ACR，則請移除 Key="AuthenticationContextReferenceClaimPattern" 的 `<Item>`。</span><span class="sxs-lookup"><span data-stu-id="407da-124">For ACR, remove the `<Item>` with the Key="AuthenticationContextReferenceClaimPattern".</span></span>

<span data-ttu-id="407da-125">**主體 (子) 宣告** 此選項的預設值為 ObjectID，如果您想要將此值切換為 `Not Supported`，請執行下列動作︰</span><span class="sxs-lookup"><span data-stu-id="407da-125">**Subject (sub) claim** This option is defaulted to ObjectID, if you would like to switch this to `Not Supported`, do the following:</span></span>

<span data-ttu-id="407da-126">換掉此行</span><span class="sxs-lookup"><span data-stu-id="407da-126">Replace this line</span></span> 
```XML
<OutputClaim ClaimTypeReferenceId="objectId" PartnerClaimType="sub" />
```
<span data-ttu-id="407da-127">改用這行︰</span><span class="sxs-lookup"><span data-stu-id="407da-127">with this line:</span></span>
```XML
<OutputClaim ClaimTypeReferenceId="sub" />
```

## <a name="session-behavior-and-sso"></a><span data-ttu-id="407da-128">工作階段行為和 SSO</span><span class="sxs-lookup"><span data-stu-id="407da-128">Session behavior and SSO</span></span>
<span data-ttu-id="407da-129">若要變更工作階段行為和 SSO 組態，您必須在 `<RelyingParty>` 元素內新增 `<UserJourneyBehaviors>` 元素。</span><span class="sxs-lookup"><span data-stu-id="407da-129">To change your session behavior and SSO configurations, you need to add a `<UserJourneyBehaviors>` element inside of the `<RelyingParty>` element.</span></span>  <span data-ttu-id="407da-130">`<UserJourneyBehaviors>` 元素必須緊接在 `<DefaultUserJourney>` 之後。</span><span class="sxs-lookup"><span data-stu-id="407da-130">The `<UserJourneyBehaviors>` element must immediately follow the `<DefaultUserJourney>`.</span></span>  <span data-ttu-id="407da-131">`<UserJourneyBehavors>` 元素的內部看起來應該像這樣︰</span><span class="sxs-lookup"><span data-stu-id="407da-131">The inside of your `<UserJourneyBehavors>` element should look like this:</span></span>

```XML
<UserJourneyBehaviors>
   <SingleSignOn Scope="Application" />
   <SessionExpiryType>Absolute</SessionExpiryType>
   <SessionExpiryInSeconds>86400</SessionExpiryInSeconds>
</UserJourneyBehaviors>
```
<span data-ttu-id="407da-132">**單一登入 (SSO) 組態** 若要變更單一登入組態，您必須修改 `<SingleSignOn>` 的值。</span><span class="sxs-lookup"><span data-stu-id="407da-132">**Single sign-on (SSO) configuration** To change the single sign-on configuration, you need to modify the value of `<SingleSignOn>`.</span></span>  <span data-ttu-id="407da-133">適用的值為 `Tenant`、`Application`、`Policy` 和 `Disabled`。</span><span class="sxs-lookup"><span data-stu-id="407da-133">The applicable values are `Tenant`, `Application`, `Policy` and `Disabled`.</span></span> 

<span data-ttu-id="407da-134">**Web 應用程式工作階段存留期 (分鐘)** 若要變更 Web 應用程式工作階段存留期，您必須修改 `<SessionExpiryInSeconds>` 元素的值。</span><span class="sxs-lookup"><span data-stu-id="407da-134">**Web app session lifetime (minutes)** To change the the web app session lifetime, you need to modify value of the `<SessionExpiryInSeconds>` element.</span></span>  <span data-ttu-id="407da-135">內建原則的預設值為 86400 秒 (1440 分鐘)。</span><span class="sxs-lookup"><span data-stu-id="407da-135">The default value in built-in policies is 86400 seconds (1440 minutes).</span></span>

<span data-ttu-id="407da-136">**Web 應用程式工作階段逾時** 若要變更 Web 應用程式工作階段逾時，您必須修改 `<SessionExpiryType>` 的值。</span><span class="sxs-lookup"><span data-stu-id="407da-136">**Web app session timeout** To change the web app session timeout, you need to modify the value of `<SessionExpiryType>`.</span></span>  <span data-ttu-id="407da-137">適用的值為 `Absolute` 和 `Rolling`。</span><span class="sxs-lookup"><span data-stu-id="407da-137">The applicable values are `Absolute` and `Rolling`.</span></span>
