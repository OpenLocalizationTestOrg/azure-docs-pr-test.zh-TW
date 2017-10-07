---
title: "Azure Active Directory B2C： 新增您自己的屬性 toocustom 原則，並使用設定檔編輯 |Microsoft 文件"
description: "逐步解說如何使用擴充功能屬性，自訂屬性，以及包含在 hello 使用者介面"
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: 
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 08/04/2017
ms.author: joroja
ms.openlocfilehash: 8cc9c6a38d7652797ba54a3e02078ac2bf4a693b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-creating-and-using-custom-attributes-in-a-custom-profile-edit-policy"></a>Azure Active Directory B2C︰在自訂設定檔編輯原則中建立和使用自訂屬性

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

本文中，您在 Azure AD B2C 目錄中建立的自訂屬性，並做為自訂宣告 hello 設定檔編輯使用者旅程中使用這個新屬性。

## <a name="prerequisites"></a>必要條件

Hello 文件中的步驟完成 hello[開始使用自訂原則](active-directory-b2c-get-started-custom.md)。

## <a name="use-custom-attributes-toocollect-information-about-your-customers-in-azure-active-directory-b2c-using-custom-policies"></a>使用您的客戶，在 Azure Active Directory B2C 中使用自訂原則的自訂屬性 toocollect 資訊
您的 Azure Active Directory (Azure AD) B2C 目錄隨附一組內建屬性：名字、姓氏、城市、郵遞區號、userPrincipalName 等等。您通常需要 toocreate 您自己的屬性。  例如：
* 客戶對向應用程式需要 toopersist 屬性，例如"LoyaltyNumber。 」
* 識別提供者擁有必須儲存的唯一使用者識別碼，例如「uniqueUserGUID」。
* 自訂使用者之旅需要 toopersist hello 狀態的使用者，例如"migrationStatus。 」

您可以使用 Azure AD B2C，擴充 hello 組儲存在每個使用者帳戶上的屬性。 您也可以讀取和寫入這些屬性使用 hello [Azure AD Graph API](active-directory-b2c-devquickstarts-graph-dotnet.md)。

擴充功能屬性擴充 hello hello hello 目錄中的使用者物件的結構描述。  hello 條款延伸模組屬性，並自訂屬性和自訂宣告，請參閱的 toohello hello 這個發行項與 hello 名稱內容中有相同的動作而異 hello 內容 （應用程式、 物件、 原則）。

擴充屬性只能註冊在應用程式物件上，即使這些屬性可能包含使用者的資料也是如此。 hello 屬性是附加的 toohello 應用程式。 hello 應用程式物件必須授與的寫入權限 tooregister 延伸模組屬性。 100 個擴充功能屬性 （跨越所有類型和所有應用程式） 可以寫入 tooany 單一物件。 擴充功能屬性會加入 toohello 目標目錄類型，並可立即存取 hello Azure AD B2C 目錄租用戶中。
如果刪除 hello 應用程式時，也會移除這些擴充功能屬性，以及它們對所有使用者所包含的任何資料。 如果 hello 應用程式刪除擴充功能屬性，則它也會移除上 hello hello 刪除的值和目標目錄物件。

擴充功能屬性只存在於 hello hello 租用戶中註冊的應用程式內容。 hello 物件識別碼，該應用程式必須包含在 hello TechnicalProfile 使用它。

>[!NOTE]
>hello Azure AD B2C 目錄通常會包含名為 Web 應用程式`b2c-extensions-app`。  此應用程式主要用於由 hello b2c 內建原則 hello 透過 hello Azure 入口網站建立的自訂宣告。  建議使用此應用程式 tooregister 副檔名 b2c 自訂原則僅適用於進階使用者。  Hello 本文章中的後續步驟 > 一節中包含這個指示。


## <a name="creating-a-new-application-toostore-hello-extension-properties"></a>建立新的應用程式 toostore hello 擴充功能屬性

1. 開啟瀏覽工作階段並瀏覽 toohello [Azure porta](https://portal.azure.com)並以 hello 想 tooconfigure B2C 目錄的系統管理認證登入。
1. 按一下**Azure Active Directory** hello 左的導覽功能表上。 您可能需要的 toofind 它藉由選取多服務 >。
1. 選取 應用程式註冊，然後按一下新增應用程式註冊
1. 提供 hello 下列建議的項目：
  * 指定 hello web 應用程式的名稱： **WebApp-GraphAPI-DirectoryExtensions**
  * 應用程式類型︰Web 應用程式/API
  * 登入 URL：https://{tenantName}.onmicrosoft.com/WebApp-GraphAPI-DirectoryExtensions
1. 選取 **[建立]。 成功完成，會出現在 hello**通知**
1. 選取新建立的 hello web 應用程式： **WebApp-GraphAPI-DirectoryExtensions**
1. 選取 [設定]：**必要權限**
1. 選取 API [Windows Active Directory]
1. 在 [應用程式權限] 中標上核取記號：**讀取及寫入目錄資料**，然後**儲存**
1. 選擇 [授與權限]，然後確認 [是]。
1. 複製 tooyour 剪貼簿並儲存 hello WebApp-GraphAPI-DirectoryExtensions 中的下列識別項 > 設定 > 屬性 >
*  **應用程式識別碼**。 範例： `103ee0e6-f92d-4183-b576-8c3739027780`
* **物件識別碼**。 範例： `80d8296a-da0a-49ee-b6ab-fd232aa45201`



## <a name="modifying-your-custom-policy-tooadd-hello-applicationobjectid"></a>修改您的自訂原則 tooadd hello ApplicationObjectId

```xml
    <ClaimsProviders>
        <ClaimsProvider>
              <DisplayName>Azure Active Directory</DisplayName>
            <TechnicalProfile Id="AAD-Common">
              <DisplayName>Azure Active Directory</DisplayName>
              <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.AzureActiveDirectoryProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
              <!-- Provide objectId and appId before using extension properties. -->
              <Metadata>
                <Item Key="ApplicationObjectId">insert objectId here</Item>
                <Item Key="ClientId">insert appId here</Item>
              </Metadata>
            <!-- End of changes -->
              <CryptographicKeys>
                <Key Id="issuer_secret" StorageReferenceId="TokenSigningKeyContainer" />
              </CryptographicKeys>
              <IncludeInSso>false</IncludeInSso>
              <UseTechnicalProfileForSessionManagement ReferenceId="SM-Noop" />
            </TechnicalProfile>
        </ClaimsProvider>
    </ClaimsProviders>
```

>[!NOTE]
>hello<TechnicalProfile Id="AAD-Common">是參照的 tooas 「 公用 」，因為其項目會包含在中，使用 hello 元素中所有 hello Azure Active Directory TechnicalProfiles 重複使用：`<IncludeTechnicalProfile ReferenceId="AAD-Common" />`

>[!NOTE]
>Hello TechnicalProfile 寫入 hello 第一次 toohello 新建立的延伸模組屬性，您可能會遇到一次性的錯誤。  hello 延伸模組屬性會使用它的第一次建立 hello。  

## <a name="using-hello-new-extension-property--custom-attribute-in-a-user-journey"></a>使用新延伸模組屬性 hello / 使用者旅程中的自訂屬性


1. 開啟 hello 信賴憑證者 Party(RP) 檔案，其中描述您的原則中編輯使用者的旅程。  如果您要啟動，它可能會建議 toodownload 您已設定的 hello RP PolicyEdit 版本檔案直接從 hello Azure B2C 自訂原則 hello Azure 入口網站 」 一節。  或者，您也可以從儲存體資料夾開啟 XML 檔案。
2. 新增自訂宣告 `loyaltyId`。  藉由 hello 自訂宣告在 hello`<RelyingParty>`項目，它是做為參數 toohello UserJourney TechnicalProfiles 傳遞，而且包含在 hello 應用程式的 hello 語彙基元。
```xml
<RelyingParty>
   <DefaultUserJourney ReferenceId="ProfileEdit" />
   <TechnicalProfile Id="PolicyProfile">
     <DisplayName>PolicyProfile</DisplayName>
     <Protocol Name="OpenIdConnect" />
     <OutputClaims>
       <OutputClaim ClaimTypeReferenceId="objectId" PartnerClaimType="sub"/>
       <OutputClaim ClaimTypeReferenceId="city" />

       <OutputClaim ClaimTypeReferenceId="extension_loyaltyId" />

     </OutputClaims>
     <SubjectNamingInfo ClaimType="sub" />
   </TechnicalProfile>
 </RelyingParty>
 ```
3. 新增宣告定義 toohello 延伸原則檔`TrustFrameworkExtensions.xml`內 hello`<ClaimsSchema>`項目所示。
```xml
<ClaimsSchema>
        <ClaimType Id="extension_loyaltyId">
            <DisplayName>Loyalty Identification Tag</DisplayName>
            <DataType>string</DataType>
            <UserHelpText>Your loyalty number from your membership card</UserHelpText>
            <UserInputType>TextBox</UserInputType>
        </ClaimType>
</ClaimsSchema>
```
4. 新增 hello 相同宣告定義 toohello 基底原則檔`TrustFrameworkBase.xml`。  
>加入`ClaimType`hello 基底和 hello 延伸模組檔案中的定義為通常不必要的不過 hello 原則驗證程式因為 hello 接下來的步驟會加入 hello extension_loyaltyId tooTechnicalProfiles hello 基底檔案中，將會拒絕 hello 上傳hello 沒有它的基底檔案。
>可能很有用的 tootrace hello 執行名為"ProfileEdit"hello TrustFrameworkBase.xml 檔案中的 hello 使用者之旅。  搜尋的 hello 相同您編輯器中的名稱，並觀察協調流程步驟 5 叫用 hello TechnicalProfileReferenceID hello 使用者之旅 ="SelfAsserted ProfileUpdate"。  搜尋並自行檢查此 TechnicalProfile toofamiliarize，與 hello 流量。
5. 加入輸入和輸出宣告在 hello TechnicalProfile"SelfAsserted ProfileUpdate"loyaltyId
```xml
<TechnicalProfile Id="SelfAsserted-ProfileUpdate">
          <DisplayName>User ID signup</DisplayName>
          <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.SelfAssertedAttributeProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
          <Metadata>
            <Item Key="ContentDefinitionReferenceId">api.selfasserted.profileupdate</Item>
          </Metadata>
          <IncludeInSso>false</IncludeInSso>
          <InputClaims>

            <InputClaim ClaimTypeReferenceId="alternativeSecurityId" />
            <InputClaim ClaimTypeReferenceId="userPrincipalName" />

            <!-- Optional claims. These claims are collected from hello user and can be modified. Any claim added here should be updated in the
                 ValidationTechnicalProfile referenced below so it can be written toodirectory after being updateed by hello user, i.e. AAD-UserWriteProfileUsingObjectId. -->
            <InputClaim ClaimTypeReferenceId="givenName" />
            <InputClaim ClaimTypeReferenceId="surname" />
            <InputClaim ClaimTypeReferenceId="extension_loyaltyId"/>
          </InputClaims>
          <OutputClaims>
            <!-- Required claims -->
            <OutputClaim ClaimTypeReferenceId="executed-SelfAsserted-Input" DefaultValue="true" />

            <!-- Optional claims. These claims are collected from hello user and can be modified. Any claim added here should be updated in the
                 ValidationTechnicalProfile referenced below so it can be written toodirectory after being updateed by hello user, i.e. AAD-UserWriteProfileUsingObjectId. -->
            <OutputClaim ClaimTypeReferenceId="givenName" />
            <OutputClaim ClaimTypeReferenceId="surname" />
            <OutputClaim ClaimTypeReferenceId="extension_loyaltyId"/>
          </OutputClaims>
          <ValidationTechnicalProfiles>
            <ValidationTechnicalProfile ReferenceId="AAD-UserWriteProfileUsingObjectId" />
          </ValidationTechnicalProfiles>
        </TechnicalProfile>
```
6. 加入 TechnicalProfile"AAD UserWriteProfileUsingObjectId"toopersist hello 宣告的值為 hello hello 延伸模組屬性，在 hello hello 目錄中的目前使用者的宣告。
```xml
<TechnicalProfile Id="AAD-UserWriteProfileUsingObjectId">
          <Metadata>
            <Item Key="Operation">Write</Item>
            <Item Key="RaiseErrorIfClaimsPrincipalAlreadyExists">false</Item>
            <Item Key="RaiseErrorIfClaimsPrincipalDoesNotExist">true</Item>
          </Metadata>
          <IncludeInSso>false</IncludeInSso>
          <InputClaims>
            <InputClaim ClaimTypeReferenceId="objectId" Required="true" />
          </InputClaims>
          <PersistedClaims>
            <!-- Required claims -->
            <PersistedClaim ClaimTypeReferenceId="objectId" />

            <!-- Optional claims -->
            <PersistedClaim ClaimTypeReferenceId="givenName" />
            <PersistedClaim ClaimTypeReferenceId="surname" />
            <PersistedClaim ClaimTypeReferenceId="extension_loyaltyId" />

          </PersistedClaims>
          <IncludeTechnicalProfile ReferenceId="AAD-Common" />
        </TechnicalProfile>
```
7. 每次使用者登入時，新增宣告 TechnicalProfile"AAD UserReadUsingObjectId"tooread hello 值 hello 延伸模組屬性中。 到目前為止 hello TechnicalProfiles hello 流程只使用本機帳戶中已變更。  如果想要使用 hello 新屬性的社交/同盟帳戶 hello 資料流程中，一組不同的 TechnicalProfiles 需要 toobe 變更。 請參閱後續步驟。

```xml
<!-- hello following technical profile is used tooread data after user authenticates. -->
     <TechnicalProfile Id="AAD-UserReadUsingObjectId">
       <Metadata>
         <Item Key="Operation">Read</Item>
         <Item Key="RaiseErrorIfClaimsPrincipalDoesNotExist">true</Item>
       </Metadata>
       <IncludeInSso>false</IncludeInSso>
       <InputClaims>
         <InputClaim ClaimTypeReferenceId="objectId" Required="true" />
       </InputClaims>
       <OutputClaims>
         <!-- Optional claims -->
         <OutputClaim ClaimTypeReferenceId="signInNames.emailAddress" />
         <OutputClaim ClaimTypeReferenceId="displayName" />
         <OutputClaim ClaimTypeReferenceId="otherMails" />
         <OutputClaim ClaimTypeReferenceId="givenName" />
         <OutputClaim ClaimTypeReferenceId="surname" />
         <OutputClaim ClaimTypeReferenceId="extension_loyaltyId" />
       </OutputClaims>
       <IncludeTechnicalProfile ReferenceId="AAD-Common" />
     </TechnicalProfile>
```


>[!IMPORTANT]
>hello IncludeTechnicalProfile 項目會加入所有 AAD-通用 toothis TechnicalProfile hello 項目。

## <a name="test-hello-custom-policy-using-run-now"></a>測試 hello 「 立即執行 」 使用的自訂原則
1. 開啟 hello **Azure AD B2C 刀鋒視窗**並瀏覽過**身分識別體驗架構 > 自訂原則**。
1. 選取您上傳，hello 自訂原則，然後按一下 hello**立即執行** 按鈕。
1. 您應該能夠 toosign 使用電子郵件地址。

hello id 權杖送回 tooyour 應用程式加上 extension_loyaltyId 自訂宣告的形式包含 hello 新延伸模組屬性。 請參閱範例。

```
{
  "exp": 1493585187,
  "nbf": 1493581587,
  "ver": "1.0",
  "iss": "https://login.microsoftonline.com/f06c2fe8-709f-4030-85dc-38a4bfd9e82d/v2.0/",
  "sub": "a58e7c6c-7535-4074-93da-b0023fbaf3ac",
  "aud": "4e87c1dd-e5f5-4ac8-8368-bc6a98751b8b",
  "acr": "b2c_1a_trustframeworkprofileedit",
  "nonce": "defaultNonce",
  "iat": 1493581587,
  "auth_time": 1493581587,
  "extension_loyaltyId": "abc",
  "city": "Redmond"
}
```

## <a name="next-steps"></a>後續步驟

藉由變更的 hello TechnicalProfiles 列出新增 hello 新宣告 toohello 流程社交帳戶登入。 這些兩個 TechnicalProfiles 是由身分證/同盟帳戶登入 toowrite 和使用讀取 hello 使用者資料使用 hello alternativeSecurityId hello hello 使用者物件的定位器。
```
  <TechnicalProfile Id="AAD-UserWriteUsingAlternativeSecurityId">

  <TechnicalProfile Id="AAD-UserReadUsingAlternativeSecurityId">
```

使用 hello 內建和自訂原則之間的相同擴充功能屬性。
當您將透過 hello 入口網站體驗的延伸模組屬性 （也稱為自訂屬性） 時，這些屬性會註冊使用 hello * * b2c 擴充功能-應用程式存在於每個 b2c 租用戶。  toouse 您自訂的原則中的這些延伸屬性：
1. B2c 租用戶的 portal.azure.com，內瀏覽過**Azure Active Directory**選取**應用程式註冊**
2. 尋找您的 **b2c-extensions-app** 並加以選取
3. 在 'Essentials' 記錄 hello**應用程式識別碼**和 hello**物件識別碼**
4. 將它們包含在您的 AAD-Common Technical 設定檔中繼資料中，如下所示：

```xml
    <ClaimsProviders>
        <ClaimsProvider>
              <DisplayName>Azure Active Directory</DisplayName>
            <TechnicalProfile Id="AAD-Common">
              <DisplayName>Azure Active Directory</DisplayName>
              <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.AzureActiveDirectoryProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
              <!-- Provide objectId and appId before using extension properties. -->
              <Metadata>
                <Item Key="ApplicationObjectId">insert objectId here</Item> <!-- This is hello "Object ID" from hello "b2c-extensions-app"-->
                <Item Key="ClientId">insert appId here</Item> <!--This is hello "Application ID" from hello "b2c-extensions-app"-->
              </Metadata>
```

tookeep 一致性與 hello 入口網站體驗，建立這些屬性使用 hello 入口網站 UI*之前*您自訂的原則中使用它們。  當您建立屬性 」 ActivationStatus"hello 入口網站中時，您必須參考 tooit，如下所示：

```
extension_ActivationStatus in hello custom policy
extension_<app-guid>_ActivationStatus via hello Graph API.
```


## <a name="reference"></a>參考

* A**技術設定檔 (TP)**是項目類型，可以視為*函式*來定義端點名稱、 它的中繼資料、 它的通訊協定，詳細資料 hello exchange 的 hello 身分識別的宣告應該執行體驗架構。  當這*函式*在協調流程的步驟中，或從另一個 TechnicalProfile，hello InputClaims OutputClaims 會提供和做為參數 hello 呼叫端呼叫。


* 完整的擴充屬性的處理方式，請參閱 hello 文章[目錄結構描述擴充功能 |GRAPH API 概念](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions)

>[!NOTE]
>Graph API 中的擴充屬性的命名慣例 hello `extension_ApplicationObjectID_attributename`。 自訂原則中參考 extension_attributename，因此省略 hello XML 中的 hello ApplicationObjectId tooextensions 屬性
