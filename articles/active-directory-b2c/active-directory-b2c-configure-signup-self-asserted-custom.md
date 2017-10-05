---
title: "Azure Active Directory B2C︰修改自訂原則中的註冊並設定自我判斷提示提供者"
description: "逐步解說如何在註冊中新增宣告並設定使用者輸入"
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: tbd
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/29/2017
ms.author: joroja
ms.openlocfilehash: 64b9d904d7d070052e125b479f4719d208c9ff85
ms.sourcegitcommit: b0af2a2cf44101a1b1ff41bd2ad795eaef29612a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/28/2017
---
# <a name="azure-active-directory-b2c-modify-sign-up-to-add-new-claims-and-configure-user-input"></a><span data-ttu-id="7a9f2-103">Azure Active Directory B2C︰修改註冊以新增宣告並設定使用者輸入。</span><span class="sxs-lookup"><span data-stu-id="7a9f2-103">Azure Active Directory B2C: Modify sign up to add new claims and configure user input.</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="7a9f2-104">在本文中，您會在您的註冊使用者旅程中新增使用者所提供的輸入 (宣告)。</span><span class="sxs-lookup"><span data-stu-id="7a9f2-104">In this article, you will add a new user provided entry (a claim) to your signup user journey.</span></span>  <span data-ttu-id="7a9f2-105">您會將輸入設定為下拉式清單，並定義它是否為必要項目。</span><span class="sxs-lookup"><span data-stu-id="7a9f2-105">You will configure the entry as a dropdown, and define if it is required.</span></span>

<span data-ttu-id="7a9f2-106">編輯 Sipi 觸發測試遞交。</span><span class="sxs-lookup"><span data-stu-id="7a9f2-106">Edited by Sipi to trigger test handoff.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7a9f2-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="7a9f2-107">Prerequisites</span></span>

* <span data-ttu-id="7a9f2-108">完成[開始使用自訂原則](active-directory-b2c-get-started-custom.md)一文中的步驟。</span><span class="sxs-lookup"><span data-stu-id="7a9f2-108">Complete the steps in the article [Getting Started with Custom Policies](active-directory-b2c-get-started-custom.md).</span></span>  <span data-ttu-id="7a9f2-109">測試註冊/登入使用者旅程以註冊新的本機帳戶，再繼續進行。</span><span class="sxs-lookup"><span data-stu-id="7a9f2-109">Test the signup/signin user journey to signup a new local account before proceeding.</span></span>


<span data-ttu-id="7a9f2-110">透過註冊/登入就能從使用者收集初始資料。</span><span class="sxs-lookup"><span data-stu-id="7a9f2-110">Gathering initial data from your users is achieved via signup/signin.</span></span>  <span data-ttu-id="7a9f2-111">其他宣告則可在稍後透過設定檔編輯使用者旅程來收集。</span><span class="sxs-lookup"><span data-stu-id="7a9f2-111">Additional claims can be gathered later via profile edit user journeys.</span></span> <span data-ttu-id="7a9f2-112">每當 Azure AD B2C 以互動方式直接從使用者收集資訊時，身分識別體驗架構會使用其 `selfasserted provider`。</span><span class="sxs-lookup"><span data-stu-id="7a9f2-112">Anytime Azure AD B2C gathers information directly from the user interactively, the Identity Experience Framework uses its `selfasserted provider`.</span></span> <span data-ttu-id="7a9f2-113">只要使用此提供者就適用下列步驟。</span><span class="sxs-lookup"><span data-stu-id="7a9f2-113">The steps below apply anytime this provider is used.</span></span>


## <a name="define-the-claim-its-display-name-and-the-user-input-type"></a><span data-ttu-id="7a9f2-114">定義宣告、其顯示名稱和使用者輸入類型</span><span class="sxs-lookup"><span data-stu-id="7a9f2-114">Define the claim, its display name and the user input type</span></span>
<span data-ttu-id="7a9f2-115">讓我們要求使用者輸入他們的所在城市。</span><span class="sxs-lookup"><span data-stu-id="7a9f2-115">Lets ask the user for their city.</span></span>  <span data-ttu-id="7a9f2-116">在 TrustFrameWorkExtensions 原則檔的 `<ClaimsSchema>` 元素中新增下列元素︰</span><span class="sxs-lookup"><span data-stu-id="7a9f2-116">Add the following element to the `<ClaimsSchema>` element in the TrustFrameWorkExtensions policy file:</span></span>

```xml
<ClaimType Id="city">
  <DisplayName>city</DisplayName>
  <DataType>string</DataType>
  <UserHelpText>Your city</UserHelpText>
  <UserInputType>TextBox</UserInputType>
</ClaimType>
```
<span data-ttu-id="7a9f2-117">您也可以在這裡進行其他選擇以自訂宣告。</span><span class="sxs-lookup"><span data-stu-id="7a9f2-117">There are additional choices you can make here to customize the claim.</span></span>  <span data-ttu-id="7a9f2-118">如需完整的結構描述，請參閱**身分識別體驗架構技術參考指南**。</span><span class="sxs-lookup"><span data-stu-id="7a9f2-118">For a full schema, refer to the **Identity Experience Framework Technical Reference Guide**.</span></span>  <span data-ttu-id="7a9f2-119">本指南很快就會發佈到參考區段中。</span><span class="sxs-lookup"><span data-stu-id="7a9f2-119">This guide will be published soon in the reference section.</span></span>

* <span data-ttu-id="7a9f2-120">`<DisplayName>` 是一個字串，會定義使用者端的「標籤」</span><span class="sxs-lookup"><span data-stu-id="7a9f2-120">`<DisplayName>` is a string that defines the user-facing *label*</span></span>

* <span data-ttu-id="7a9f2-121">`<UserHelpText>` 可協助使用者了解所需項目</span><span class="sxs-lookup"><span data-stu-id="7a9f2-121">`<UserHelpText>` helps the user understand what is required</span></span>

* <span data-ttu-id="7a9f2-122">`<UserInputType>` 有下面四個特別點出的選項︰</span><span class="sxs-lookup"><span data-stu-id="7a9f2-122">`<UserInputType>` has the following four options highlighted below:</span></span>
    * `TextBox`
```xml
<ClaimType Id="city">
  <DisplayName>city where you work</DisplayName>
  <DataType>string</DataType>
  <UserHelpText>Your city</UserHelpText>
  <UserInputType>TextBox</UserInputType>
</ClaimType>
```

    * <span data-ttu-id="7a9f2-123">`RadioSingleSelectduration` - 強制讓您只能選取單一項目。</span><span class="sxs-lookup"><span data-stu-id="7a9f2-123">`RadioSingleSelectduration` - Enforces a single selection.</span></span>
```xml
<ClaimType Id="city">
  <DisplayName>city where you work</DisplayName>
  <DataType>string</DataType>
  <UserInputType>RadioSingleSelect</UserInputType>
  <Restriction>
    <Enumeration Text="Bellevue" Value="bellevue" SelectByDefault="false" />
    <Enumeration Text="Redmond" Value="redmond" SelectByDefault="false" />
    <Enumeration Text="Kirkland" Value="kirkland" SelectByDefault="false" />
  </Restriction>
</ClaimType>
```

    * <span data-ttu-id="7a9f2-124">`DropdownSingleSelect` - 只允許選取有效值。</span><span class="sxs-lookup"><span data-stu-id="7a9f2-124">`DropdownSingleSelect` - Allows the selection of only valid value.</span></span>

![下拉式清單選項的螢幕擷取畫面](./media/active-directory-b2c-configure-signup-self-asserted-custom/dropdown-menu-example.png)


```xml
<ClaimType Id="city">
  <DisplayName>city where you work</DisplayName>
  <DataType>string</DataType>
  <UserInputType>DropdownSingleSelect</UserInputType>
  <Restriction>
    <Enumeration Text="Bellevue" Value="bellevue" SelectByDefault="false" />
    <Enumeration Text="Redmond" Value="redmond" SelectByDefault="false" />
    <Enumeration Text="Kirkland" Value="kirkland" SelectByDefault="false" />
  </Restriction>
</ClaimType>
```


* <span data-ttu-id="7a9f2-126">`CheckboxMultiSelect` 允許選取一個或多個值。</span><span class="sxs-lookup"><span data-stu-id="7a9f2-126">`CheckboxMultiSelect` Allows for the selection of one or more values.</span></span>

![多重選取選項的螢幕擷取畫面](./media/active-directory-b2c-configure-signup-self-asserted-custom/multiselect-menu-example.png)


```xml
<ClaimType Id="city">
  <DisplayName>Receive updates from which cities?</DisplayName>
  <DataType>string</DataType>
  <UserInputType>CheckboxMultiSelect</UserInputType>
  <Restriction>
    <Enumeration Text="Bellevue" Value="bellevue" SelectByDefault="false" />
    <Enumeration Text="Redmond" Value="redmond" SelectByDefault="false" />
    <Enumeration Text="Kirkland" Value="kirkland" SelectByDefault="false" />
  </Restriction>
</ClaimType>
```

## <a name="add-the-claim-to-the-sign-upsign-in-user-journey"></a><span data-ttu-id="7a9f2-128">將宣告新增至在使用者旅程的註冊/登入</span><span class="sxs-lookup"><span data-stu-id="7a9f2-128">Add the claim to the sign up/sign in user journey</span></span>

1. <span data-ttu-id="7a9f2-129">以 `<OutputClaim ClaimTypeReferenceId="city"/>` 的形式將宣告新增至 TechnicalProfile `LocalAccountSignUpWithLogonEmail` (可在 TrustFrameworkBase 原則檔中找到)。</span><span class="sxs-lookup"><span data-stu-id="7a9f2-129">Add the claim as an `<OutputClaim ClaimTypeReferenceId="city"/>` to the TechnicalProfile `LocalAccountSignUpWithLogonEmail` (found in the TrustFrameworkBase policy file).</span></span>  <span data-ttu-id="7a9f2-130">請注意，此 TechnicalProfile 使用 SelfAssertedAttributeProvider。</span><span class="sxs-lookup"><span data-stu-id="7a9f2-130">Note this TechnicalProfile uses the SelfAssertedAttributeProvider.</span></span>

  ```xml
  <TechnicalProfile Id="LocalAccountSignUpWithLogonEmail">
    <DisplayName>Email signup</DisplayName>
    <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.SelfAssertedAttributeProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
    <Metadata>
      <Item Key="IpAddressClaimReferenceId">IpAddress</Item>
      <Item Key="ContentDefinitionReferenceId">api.localaccountsignup</Item>
      <Item Key="language.button_continue">Create</Item>
    </Metadata>
    <CryptographicKeys>
      <Key Id="issuer_secret" StorageReferenceId="TokenSigningKeyContainer" />
    </CryptographicKeys>
    <InputClaims>
      <InputClaim ClaimTypeReferenceId="email" />
    </InputClaims>
    <OutputClaims>
      <OutputClaim ClaimTypeReferenceId="objectId" />
      <OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="Verified.Email" Required="true" />
      <OutputClaim ClaimTypeReferenceId="newPassword" Required="true" />
      <OutputClaim ClaimTypeReferenceId="reenterPassword" Required="true" />
      <OutputClaim ClaimTypeReferenceId="executed-SelfAsserted-Input" DefaultValue="true" />
      <OutputClaim ClaimTypeReferenceId="authenticationSource" />
      <OutputClaim ClaimTypeReferenceId="newUser" />
      <!-- Optional claims, to be collected from the user -->
      <OutputClaim ClaimTypeReferenceId="givenName" />
      <OutputClaim ClaimTypeReferenceId="surName" />
      <OutputClaim ClaimTypeReferenceId="city"/>
    </OutputClaims>
    <ValidationTechnicalProfiles>
      <ValidationTechnicalProfile ReferenceId="AAD-UserWriteUsingLogonEmail" />
    </ValidationTechnicalProfiles>
    <UseTechnicalProfileForSessionManagement ReferenceId="SM-AAD" />
  </TechnicalProfile>
  ```

2. <span data-ttu-id="7a9f2-131">以 `<PersistedClaim ClaimTypeReferenceId="city" />` 的形式將宣告新增至 AAD-UserWriteUsingLogonEmail，以在收集使用者的宣告後將宣告寫入到 AAD 目錄。</span><span class="sxs-lookup"><span data-stu-id="7a9f2-131">Add the claim to the AAD-UserWriteUsingLogonEmail as a `<PersistedClaim ClaimTypeReferenceId="city" />` to write the claim to the AAD directory after collecting it from the user.</span></span> <span data-ttu-id="7a9f2-132">如果您不想在目錄中保留宣告以供日後使用，則可略過此步驟。</span><span class="sxs-lookup"><span data-stu-id="7a9f2-132">You may skip this step if you prefer not to persist the claim in the directory for future use.</span></span>

  ```xml
  <!-- Technical profiles for local accounts -->
  <TechnicalProfile Id="AAD-UserWriteUsingLogonEmail">
    <Metadata>
      <Item Key="Operation">Write</Item>
      <Item Key="RaiseErrorIfClaimsPrincipalAlreadyExists">true</Item>
    </Metadata>
    <IncludeInSso>false</IncludeInSso>
    <InputClaims>
      <InputClaim ClaimTypeReferenceId="email" PartnerClaimType="signInNames.emailAddress" Required="true" />
    </InputClaims>
    <PersistedClaims>
      <!-- Required claims -->
      <PersistedClaim ClaimTypeReferenceId="email" PartnerClaimType="signInNames.emailAddress" />
      <PersistedClaim ClaimTypeReferenceId="newPassword" PartnerClaimType="password" />
      <PersistedClaim ClaimTypeReferenceId="displayName" DefaultValue="unknown" />
      <PersistedClaim ClaimTypeReferenceId="passwordPolicies" DefaultValue="DisablePasswordExpiration" />
      <!-- Optional claims. -->
      <PersistedClaim ClaimTypeReferenceId="givenName" />
      <PersistedClaim ClaimTypeReferenceId="surname" />
      <PersistedClaim ClaimTypeReferenceId="city" />
    </PersistedClaims>
    <OutputClaims>
      <OutputClaim ClaimTypeReferenceId="objectId" />
      <OutputClaim ClaimTypeReferenceId="newUser" PartnerClaimType="newClaimsPrincipalCreated" />
      <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="localAccountAuthentication" />
      <OutputClaim ClaimTypeReferenceId="userPrincipalName" />
      <OutputClaim ClaimTypeReferenceId="signInNames.emailAddress" />
    </OutputClaims>
    <IncludeTechnicalProfile ReferenceId="AAD-Common" />
    <UseTechnicalProfileForSessionManagement ReferenceId="SM-AAD" />
  </TechnicalProfile>
  ```

3. <span data-ttu-id="7a9f2-133">以 `<OutputClaim ClaimTypeReferenceId="city" />` 的形式將宣告新增至 TechnicalProfile，以在使用者登入時從目錄中讀取此宣告</span><span class="sxs-lookup"><span data-stu-id="7a9f2-133">Add the claim to the TechnicalProfile that reads from the directory when a user logs in as an `<OutputClaim ClaimTypeReferenceId="city" />`</span></span>

  ```xml
  <TechnicalProfile Id="AAD-UserReadUsingEmailAddress">
    <Metadata>
      <Item Key="Operation">Read</Item>
      <Item Key="RaiseErrorIfClaimsPrincipalDoesNotExist">true</Item>
      <Item Key="UserMessageIfClaimsPrincipalDoesNotExist">An account could not be found for the provided user ID.</Item>
    </Metadata>
    <IncludeInSso>false</IncludeInSso>
    <InputClaims>
      <InputClaim ClaimTypeReferenceId="email" PartnerClaimType="signInNames" Required="true" />
    </InputClaims>
    <OutputClaims>
      <!-- Required claims -->
      <OutputClaim ClaimTypeReferenceId="objectId" />
      <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="localAccountAuthentication" />
      <!-- Optional claims -->
      <OutputClaim ClaimTypeReferenceId="userPrincipalName" />
      <OutputClaim ClaimTypeReferenceId="displayName" />
      <OutputClaim ClaimTypeReferenceId="otherMails" />
      <OutputClaim ClaimTypeReferenceId="signInNames.emailAddress" />
      <OutputClaim ClaimTypeReferenceId="city" />
    </OutputClaims>
    <IncludeTechnicalProfile ReferenceId="AAD-Common" />
  </TechnicalProfile>
  ```

4. <span data-ttu-id="7a9f2-134">將 `<OutputClaim ClaimTypeReferenceId="city" />` 新增至 RP 原則檔案 SignUporSignIn.xml，讓系統在使用者旅程成功後將這個宣告傳送至權杖中的應用程式。</span><span class="sxs-lookup"><span data-stu-id="7a9f2-134">Add the `<OutputClaim ClaimTypeReferenceId="city" />` to the RP policy file SignUporSignIn.xml so this claim is sent to the application in the token after a successful user journey.</span></span>

  ```xml
  <RelyingParty>
    <DefaultUserJourney ReferenceId="SignUpOrSignIn" />
    <TechnicalProfile Id="PolicyProfile">
      <DisplayName>PolicyProfile</DisplayName>
      <Protocol Name="OpenIdConnect" />
      <OutputClaims>
        <OutputClaim ClaimTypeReferenceId="displayName" />
        <OutputClaim ClaimTypeReferenceId="givenName" />
        <OutputClaim ClaimTypeReferenceId="surname" />
        <OutputClaim ClaimTypeReferenceId="email" />
        <OutputClaim ClaimTypeReferenceId="objectId" PartnerClaimType="sub"/>
        <OutputClaim ClaimTypeReferenceId="identityProvider" />
        <OutputClaim ClaimTypeReferenceId="city" />
      </OutputClaims>
      <SubjectNamingInfo ClaimType="sub" />
    </TechnicalProfile>
  </RelyingParty>
  ```

## <a name="test-the-custom-policy-using-run-now"></a><span data-ttu-id="7a9f2-135">使用 [立即執行] 測試自訂原則</span><span class="sxs-lookup"><span data-stu-id="7a9f2-135">Test the custom policy using "Run Now"</span></span>

1. <span data-ttu-id="7a9f2-136">開啟 [Azure AD B2C] 刀鋒視窗，然後巡覽至 [識別體驗架構] > [自訂原則]。</span><span class="sxs-lookup"><span data-stu-id="7a9f2-136">Open the **Azure AD B2C Blade** and navigate to **Identity Experience Framework > Custom policies**.</span></span>
2. <span data-ttu-id="7a9f2-137">選取您上傳的自訂原則，按一下 [立即執行] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7a9f2-137">Select the custom policy that you uploaded, and click the **Run now** button.</span></span>
3. <span data-ttu-id="7a9f2-138">您應該可以使用電子郵件地址註冊。</span><span class="sxs-lookup"><span data-stu-id="7a9f2-138">You should be able to sign up using an email address.</span></span>

<span data-ttu-id="7a9f2-139">測試模式中的註冊畫面看起來應該像這樣：</span><span class="sxs-lookup"><span data-stu-id="7a9f2-139">The signup screen in test mode should look similar to this:</span></span>

![修改過的註冊選項螢幕擷取畫面](./media/active-directory-b2c-configure-signup-self-asserted-custom/signup-with-city-claim-dropdown-example.png)

  <span data-ttu-id="7a9f2-141">傳回到應用程式的權杖現在會包含 `city` 宣告，如下所示</span><span class="sxs-lookup"><span data-stu-id="7a9f2-141">The token back to your application will now include the `city` claim as shown below</span></span>
```json
{
  "exp": 1493596822,
  "nbf": 1493593222,
  "ver": "1.0",
  "iss": "https://login.microsoftonline.com/f06c2fe8-709f-4030-85dc-38a4bfd9e82d/v2.0/",
  "sub": "9c2a3a9e-ac65-4e46-a12d-9557b63033a9",
  "aud": "4e87c1dd-e5f5-4ac8-8368-bc6a98751b8b",
  "acr": "b2c_1a_trustf_signup_signin",
  "nonce": "defaultNonce",
  "iat": 1493593222,
  "auth_time": 1493593222,
  "email": "joe@outlook.com",
  "given_name": "Joe",
  "family_name": "Ras",
  "city": "Bellevue",
  "name": "unknown"
}
```

## <a name="optional-remove-email-verification-from-signup-journey"></a><span data-ttu-id="7a9f2-142">選擇性：移除註冊旅程中的電子郵件驗證</span><span class="sxs-lookup"><span data-stu-id="7a9f2-142">Optional: Remove email verification from signup journey</span></span>

<span data-ttu-id="7a9f2-143">若要略過電子郵件驗證，原則的作者可以選擇移除 `PartnerClaimType="Verified.Email"`。</span><span class="sxs-lookup"><span data-stu-id="7a9f2-143">To skip email verification, the policy author can choose to remove `PartnerClaimType="Verified.Email"`.</span></span> <span data-ttu-id="7a9f2-144">除非您移除 “Required” = true，否則電子郵件地址雖為必要項目，但不會進行驗證。</span><span class="sxs-lookup"><span data-stu-id="7a9f2-144">The email address will be required but not verified, unless “Required” = true is removed.</span></span>  <span data-ttu-id="7a9f2-145">請仔細想清楚此選項是否適用於您的使用案例！</span><span class="sxs-lookup"><span data-stu-id="7a9f2-145">Carefully consider if this option is right for your use cases!</span></span>

<span data-ttu-id="7a9f2-146">入門套件中 TrustFrameworkBase 原則檔案的 `<TechnicalProfile Id="LocalAccountSignUpWithLogonEmail">` 預設會啟用驗證的電子郵件︰</span><span class="sxs-lookup"><span data-stu-id="7a9f2-146">Verified email is enabled by default in the `<TechnicalProfile Id="LocalAccountSignUpWithLogonEmail">` in the TrustFrameworkBase policy file in the starter pack:</span></span>
```xml
<OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="Verified.Email" Required="true" />
```

## <a name="next-steps"></a><span data-ttu-id="7a9f2-147">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7a9f2-147">Next steps</span></span>

<span data-ttu-id="7a9f2-148">藉由變更下列 TechnicalProfiles，將新的宣告新增至社交帳戶登入的的流程。</span><span class="sxs-lookup"><span data-stu-id="7a9f2-148">Add the new claim to the flows for social account logins by changing the TechnicalProfiles listed below.</span></span> <span data-ttu-id="7a9f2-149">社交/同盟帳戶登入會使用這些項目，以 alternativeSecurityId 作為定位器來寫入和讀取使用者資料。</span><span class="sxs-lookup"><span data-stu-id="7a9f2-149">These are used by social/federated account logins to write and read the user data using the alternativeSecurityId as the locator.</span></span>
```xml
<TechnicalProfile Id="AAD-UserWriteUsingAlternativeSecurityId">
<TechnicalProfile Id="AAD-UserReadUsingAlternativeSecurityId">
```
