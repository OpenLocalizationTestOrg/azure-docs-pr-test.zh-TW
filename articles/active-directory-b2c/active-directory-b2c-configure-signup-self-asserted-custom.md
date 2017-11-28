---
title: "Azure Active Directory B2C︰修改自訂原則中的註冊並設定自我判斷提示提供者"
description: "逐步解說中的加入宣告 toosign 註冊及設定 hello 使用者輸入"
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
ms.openlocfilehash: c31d737263fef3e771bdf451b809b0ca522c8fe0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-modify-sign-up-tooadd-new-claims-and-configure-user-input"></a><span data-ttu-id="9d78f-103">Azure Active Directory B2C： 修改註冊 tooadd 新宣告，並設定使用者輸入。</span><span class="sxs-lookup"><span data-stu-id="9d78f-103">Azure Active Directory B2C: Modify sign up tooadd new claims and configure user input.</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="9d78f-104">在本文中，您將加入新使用者提供項目 （宣告） tooyour 註冊使用者的旅程。</span><span class="sxs-lookup"><span data-stu-id="9d78f-104">In this article, you will add a new user provided entry (a claim) tooyour signup user journey.</span></span>  <span data-ttu-id="9d78f-105">您將為下拉式清單中，設定 hello 項目，並定義在必要時。</span><span class="sxs-lookup"><span data-stu-id="9d78f-105">You will configure hello entry as a dropdown, and define if it is required.</span></span>

<span data-ttu-id="9d78f-106">編輯 Sipi tootrigger 測試遞交。</span><span class="sxs-lookup"><span data-stu-id="9d78f-106">Edited by Sipi tootrigger test handoff.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9d78f-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="9d78f-107">Prerequisites</span></span>

* <span data-ttu-id="9d78f-108">Hello 文件中的步驟完成 hello[開始使用自訂原則](active-directory-b2c-get-started-custom.md)。</span><span class="sxs-lookup"><span data-stu-id="9d78f-108">Complete hello steps in hello article [Getting Started with Custom Policies](active-directory-b2c-get-started-custom.md).</span></span>  <span data-ttu-id="9d78f-109">測試 hello 註冊/登入使用者之旅 toosignup 新的本機帳戶，才能繼續。</span><span class="sxs-lookup"><span data-stu-id="9d78f-109">Test hello signup/signin user journey toosignup a new local account before proceeding.</span></span>


<span data-ttu-id="9d78f-110">透過註冊/登入就能從使用者收集初始資料。</span><span class="sxs-lookup"><span data-stu-id="9d78f-110">Gathering initial data from your users is achieved via signup/signin.</span></span>  <span data-ttu-id="9d78f-111">其他宣告則可在稍後透過設定檔編輯使用者旅程來收集。</span><span class="sxs-lookup"><span data-stu-id="9d78f-111">Additional claims can be gathered later via profile edit user journeys.</span></span> <span data-ttu-id="9d78f-112">Azure AD B2C 收集資訊直接 hello 使用者以互動方式，每當 hello 身分識別體驗架構會使用其`selfasserted provider`。</span><span class="sxs-lookup"><span data-stu-id="9d78f-112">Anytime Azure AD B2C gathers information directly from hello user interactively, hello Identity Experience Framework uses its `selfasserted provider`.</span></span> <span data-ttu-id="9d78f-113">hello 步驟套用隨時使用此提供者。</span><span class="sxs-lookup"><span data-stu-id="9d78f-113">hello steps below apply anytime this provider is used.</span></span>


## <a name="define-hello-claim-its-display-name-and-hello-user-input-type"></a><span data-ttu-id="9d78f-114">定義 hello 宣告、 顯示名稱和 hello 使用者輸入類型</span><span class="sxs-lookup"><span data-stu-id="9d78f-114">Define hello claim, its display name and hello user input type</span></span>
<span data-ttu-id="9d78f-115">可讓 hello 使用者尋求他們的城市。</span><span class="sxs-lookup"><span data-stu-id="9d78f-115">Lets ask hello user for their city.</span></span>  <span data-ttu-id="9d78f-116">新增下列項目 toohello hello `<ClaimsSchema>` hello TrustFrameWorkExtensions 原則檔中的項目：</span><span class="sxs-lookup"><span data-stu-id="9d78f-116">Add hello following element toohello `<ClaimsSchema>` element in hello TrustFrameWorkExtensions policy file:</span></span>

```xml
<ClaimType Id="city">
  <DisplayName>city</DisplayName>
  <DataType>string</DataType>
  <UserHelpText>Your city</UserHelpText>
  <UserInputType>TextBox</UserInputType>
</ClaimType>
```
<span data-ttu-id="9d78f-117">有其他選擇，您可以在此處 toocustomize hello 宣告。</span><span class="sxs-lookup"><span data-stu-id="9d78f-117">There are additional choices you can make here toocustomize hello claim.</span></span>  <span data-ttu-id="9d78f-118">針對完整的結構描述，請參閱 toohello**識別體驗架構技術參照指南**。</span><span class="sxs-lookup"><span data-stu-id="9d78f-118">For a full schema, refer toohello **Identity Experience Framework Technical Reference Guide**.</span></span>  <span data-ttu-id="9d78f-119">本指南即將發行在 hello 參考一節。</span><span class="sxs-lookup"><span data-stu-id="9d78f-119">This guide will be published soon in hello reference section.</span></span>

* <span data-ttu-id="9d78f-120">`<DisplayName>`是字串，定義使用者互動 hello*標籤*</span><span class="sxs-lookup"><span data-stu-id="9d78f-120">`<DisplayName>` is a string that defines hello user-facing *label*</span></span>

* <span data-ttu-id="9d78f-121">`<UserHelpText>`有助於了解什麼是必要的 hello 使用者</span><span class="sxs-lookup"><span data-stu-id="9d78f-121">`<UserHelpText>` helps hello user understand what is required</span></span>

* <span data-ttu-id="9d78f-122">`<UserInputType>`hello 下列四個選項反白顯示如下：</span><span class="sxs-lookup"><span data-stu-id="9d78f-122">`<UserInputType>` has hello following four options highlighted below:</span></span>
    * `TextBox`
```xml
<ClaimType Id="city">
  <DisplayName>city where you work</DisplayName>
  <DataType>string</DataType>
  <UserHelpText>Your city</UserHelpText>
  <UserInputType>TextBox</UserInputType>
</ClaimType>
```

    * <span data-ttu-id="9d78f-123">`RadioSingleSelectduration` - 強制讓您只能選取單一項目。</span><span class="sxs-lookup"><span data-stu-id="9d78f-123">`RadioSingleSelectduration` - Enforces a single selection.</span></span>
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

    * <span data-ttu-id="9d78f-124">`DropdownSingleSelect`-允許 hello 選取有效的值。</span><span class="sxs-lookup"><span data-stu-id="9d78f-124">`DropdownSingleSelect` - Allows hello selection of only valid value.</span></span>

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


* <span data-ttu-id="9d78f-126">`CheckboxMultiSelect`允許的一個或多個值的 hello 選取範圍。</span><span class="sxs-lookup"><span data-stu-id="9d78f-126">`CheckboxMultiSelect` Allows for hello selection of one or more values.</span></span>

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

## <a name="add-hello-claim-toohello-sign-upsign-in-user-journey"></a><span data-ttu-id="9d78f-128">新增 hello 宣告 toohello 登向上/登入使用者之旅</span><span class="sxs-lookup"><span data-stu-id="9d78f-128">Add hello claim toohello sign up/sign in user journey</span></span>

1. <span data-ttu-id="9d78f-129">新增 hello 的宣告則為`<OutputClaim ClaimTypeReferenceId="city"/>`toohello TechnicalProfile `LocalAccountSignUpWithLogonEmail` （hello TrustFrameworkBase 原則檔中找到）。</span><span class="sxs-lookup"><span data-stu-id="9d78f-129">Add hello claim as an `<OutputClaim ClaimTypeReferenceId="city"/>` toohello TechnicalProfile `LocalAccountSignUpWithLogonEmail` (found in hello TrustFrameworkBase policy file).</span></span>  <span data-ttu-id="9d78f-130">請注意此 TechnicalProfile 使用 hello SelfAssertedAttributeProvider。</span><span class="sxs-lookup"><span data-stu-id="9d78f-130">Note this TechnicalProfile uses hello SelfAssertedAttributeProvider.</span></span>

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
      <!-- Optional claims, toobe collected from hello user -->
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

2. <span data-ttu-id="9d78f-131">加入做為 hello 宣告 toohello AAD UserWriteUsingLogonEmail `<PersistedClaim ClaimTypeReferenceId="city" />` toowrite hello 宣告 toohello AAD 目錄之後收集來自 hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="9d78f-131">Add hello claim toohello AAD-UserWriteUsingLogonEmail as a `<PersistedClaim ClaimTypeReferenceId="city" />` toowrite hello claim toohello AAD directory after collecting it from hello user.</span></span> <span data-ttu-id="9d78f-132">如果您偏好不 toopersist hello 宣告 hello 目錄中的供日後使用，您可能會略過此步驟。</span><span class="sxs-lookup"><span data-stu-id="9d78f-132">You may skip this step if you prefer not toopersist hello claim in hello directory for future use.</span></span>

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

3. <span data-ttu-id="9d78f-133">新增 hello 宣告 toohello TechnicalProfile 讀取 hello 目錄中，當使用者登入為`<OutputClaim ClaimTypeReferenceId="city" />`</span><span class="sxs-lookup"><span data-stu-id="9d78f-133">Add hello claim toohello TechnicalProfile that reads from hello directory when a user logs in as an `<OutputClaim ClaimTypeReferenceId="city" />`</span></span>

  ```xml
  <TechnicalProfile Id="AAD-UserReadUsingEmailAddress">
    <Metadata>
      <Item Key="Operation">Read</Item>
      <Item Key="RaiseErrorIfClaimsPrincipalDoesNotExist">true</Item>
      <Item Key="UserMessageIfClaimsPrincipalDoesNotExist">An account could not be found for hello provided user ID.</Item>
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

4. <span data-ttu-id="9d78f-134">新增 hello `<OutputClaim ClaimTypeReferenceId="city" />` toohello RP 原則檔讓此宣告 toohello 應用程式中傳送 hello 語彙基元後成功的使用者之旅 SignUporSignIn.xml。</span><span class="sxs-lookup"><span data-stu-id="9d78f-134">Add hello `<OutputClaim ClaimTypeReferenceId="city" />` toohello RP policy file SignUporSignIn.xml so this claim is sent toohello application in hello token after a successful user journey.</span></span>

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

## <a name="test-hello-custom-policy-using-run-now"></a><span data-ttu-id="9d78f-135">測試 hello 「 立即執行 」 使用的自訂原則</span><span class="sxs-lookup"><span data-stu-id="9d78f-135">Test hello custom policy using "Run Now"</span></span>

1. <span data-ttu-id="9d78f-136">開啟 hello **Azure AD B2C 刀鋒視窗**並瀏覽過**身分識別體驗架構 > 自訂原則**。</span><span class="sxs-lookup"><span data-stu-id="9d78f-136">Open hello **Azure AD B2C Blade** and navigate too**Identity Experience Framework > Custom policies**.</span></span>
2. <span data-ttu-id="9d78f-137">選取您上傳，hello 自訂原則，然後按一下 hello**立即執行** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="9d78f-137">Select hello custom policy that you uploaded, and click hello **Run now** button.</span></span>
3. <span data-ttu-id="9d78f-138">您應該能夠 toosign 使用電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="9d78f-138">You should be able toosign up using an email address.</span></span>

<span data-ttu-id="9d78f-139">在測試模式中的 hello 註冊畫面應該看起來類似 toothis:</span><span class="sxs-lookup"><span data-stu-id="9d78f-139">hello signup screen in test mode should look similar toothis:</span></span>

![修改過的註冊選項螢幕擷取畫面](./media/active-directory-b2c-configure-signup-self-asserted-custom/signup-with-city-claim-dropdown-example.png)

  <span data-ttu-id="9d78f-141">hello 語彙基元後 tooyour 應用程式現在包含 hello`city`宣告如下所示</span><span class="sxs-lookup"><span data-stu-id="9d78f-141">hello token back tooyour application will now include hello `city` claim as shown below</span></span>
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

## <a name="optional-remove-email-verification-from-signup-journey"></a><span data-ttu-id="9d78f-142">選擇性：移除註冊旅程中的電子郵件驗證</span><span class="sxs-lookup"><span data-stu-id="9d78f-142">Optional: Remove email verification from signup journey</span></span>

<span data-ttu-id="9d78f-143">tooskip 電子郵件驗證，hello 原則作者可選擇 tooremove `PartnerClaimType="Verified.Email"`。</span><span class="sxs-lookup"><span data-stu-id="9d78f-143">tooskip email verification, hello policy author can choose tooremove `PartnerClaimType="Verified.Email"`.</span></span> <span data-ttu-id="9d78f-144">hello 電子郵件地址將所需但未經過驗證，除非 「 要求 」 = true 會移除。</span><span class="sxs-lookup"><span data-stu-id="9d78f-144">hello email address will be required but not verified, unless “Required” = true is removed.</span></span>  <span data-ttu-id="9d78f-145">請仔細想清楚此選項是否適用於您的使用案例！</span><span class="sxs-lookup"><span data-stu-id="9d78f-145">Carefully consider if this option is right for your use cases!</span></span>

<span data-ttu-id="9d78f-146">驗證預設會在 hello 啟用電子郵件`<TechnicalProfile Id="LocalAccountSignUpWithLogonEmail">`hello 入門組件中的 hello TrustFrameworkBase 原則檔中：</span><span class="sxs-lookup"><span data-stu-id="9d78f-146">Verified email is enabled by default in hello `<TechnicalProfile Id="LocalAccountSignUpWithLogonEmail">` in hello TrustFrameworkBase policy file in hello starter pack:</span></span>
```xml
<OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="Verified.Email" Required="true" />
```

## <a name="next-steps"></a><span data-ttu-id="9d78f-147">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9d78f-147">Next steps</span></span>

<span data-ttu-id="9d78f-148">藉由變更 TechnicalProfiles 下面所列的 hello 加入 hello 新宣告 toohello 流程社交帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="9d78f-148">Add hello new claim toohello flows for social account logins by changing hello TechnicalProfiles listed below.</span></span> <span data-ttu-id="9d78f-149">這些是使用社交/同盟帳戶登入 toowrite，讀取使用 hello alternativeSecurityId hello 定位器 hello 使用者資料。</span><span class="sxs-lookup"><span data-stu-id="9d78f-149">These are used by social/federated account logins toowrite and read hello user data using hello alternativeSecurityId as hello locator.</span></span>
```xml
<TechnicalProfile Id="AAD-UserWriteUsingAlternativeSecurityId">
<TechnicalProfile Id="AAD-UserReadUsingAlternativeSecurityId">
```
