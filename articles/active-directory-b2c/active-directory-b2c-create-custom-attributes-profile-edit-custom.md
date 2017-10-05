---
title: "Azure Active Directory B2C︰將自有屬性新增到自訂原則並用於設定檔編輯 | Microsoft Docs"
description: "逐步解說如何使用擴充屬性、自訂屬性，並將其包含在使用者介面中"
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
ms.openlocfilehash: 67c9f6eca18e2dd77e00b8bc8c7bcc546ea3936e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="azure-active-directory-b2c-creating-and-using-custom-attributes-in-a-custom-profile-edit-policy"></a><span data-ttu-id="fd430-103">Azure Active Directory B2C︰在自訂設定檔編輯原則中建立和使用自訂屬性</span><span class="sxs-lookup"><span data-stu-id="fd430-103">Azure Active Directory B2C: Creating and using custom attributes in a custom profile edit policy</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="fd430-104">在本文中，您會在 Azure AD B2C 目錄中建立自訂屬性，並使用這個新屬性來作為設定檔編輯使用者旅程圖中的自訂宣告。</span><span class="sxs-lookup"><span data-stu-id="fd430-104">In this article, you create a custom attribute in your Azure AD B2C directory and use this new attribute as a custom claim in the profile edit user journey.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fd430-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="fd430-105">Prerequisites</span></span>

<span data-ttu-id="fd430-106">完成[開始使用自訂原則](active-directory-b2c-get-started-custom.md)一文中的步驟。</span><span class="sxs-lookup"><span data-stu-id="fd430-106">Complete the steps in the article [Getting Started with Custom Policies](active-directory-b2c-get-started-custom.md).</span></span>

## <a name="use-custom-attributes-to-collect-information-about-your-customers-in-azure-active-directory-b2c-using-custom-policies"></a><span data-ttu-id="fd430-107">使用自訂屬性，以透過自訂原則來收集您的客戶在 Azure Active Directory B2C 中的相關資訊</span><span class="sxs-lookup"><span data-stu-id="fd430-107">Use custom attributes to collect information about your customers in Azure Active Directory B2C using custom policies</span></span>
<span data-ttu-id="fd430-108">您的 Azure Active Directory (Azure AD) B2C 目錄隨附一組內建屬性：名字、姓氏、城市、郵遞區號、userPrincipalName 等等。您通常必須建立自有屬性。</span><span class="sxs-lookup"><span data-stu-id="fd430-108">Your Azure Active Directory (Azure AD) B2C directory comes with a built-in set of attributes: Given Name, Surname, City, Postal Code, userPrincipalName, etc.  You often need to create your own attributes.</span></span>  <span data-ttu-id="fd430-109">例如：</span><span class="sxs-lookup"><span data-stu-id="fd430-109">For example:</span></span>
* <span data-ttu-id="fd430-110">面對客戶的應用程式需要保有「LoyaltyNumber」之類的屬性。</span><span class="sxs-lookup"><span data-stu-id="fd430-110">A customer-facing application needs to persist an attribute such as "LoyaltyNumber."</span></span>
* <span data-ttu-id="fd430-111">識別提供者擁有必須儲存的唯一使用者識別碼，例如「uniqueUserGUID」。</span><span class="sxs-lookup"><span data-stu-id="fd430-111">An identity provider has a unique user identifier that must be saved such as "uniqueUserGUID.""</span></span>
* <span data-ttu-id="fd430-112">自訂使用者旅程需要保有使用者的狀態，例如「migrationStatus」。</span><span class="sxs-lookup"><span data-stu-id="fd430-112">A custom user journey needs to persist the state of user such as "migrationStatus."</span></span>

<span data-ttu-id="fd430-113">Azure AD B2C 可讓您擴充每個使用者帳戶所儲存的屬性組合。</span><span class="sxs-lookup"><span data-stu-id="fd430-113">With Azure AD B2C, you can extend the set of attributes stored on each user account.</span></span> <span data-ttu-id="fd430-114">您也可以使用 [Azure AD Graph API](active-directory-b2c-devquickstarts-graph-dotnet.md)讀取和寫入這些屬性。</span><span class="sxs-lookup"><span data-stu-id="fd430-114">You can also read and write these attributes by using the [Azure AD Graph API](active-directory-b2c-devquickstarts-graph-dotnet.md).</span></span>

<span data-ttu-id="fd430-115">擴充屬性會擴充目錄中的使用者物件結構描述。</span><span class="sxs-lookup"><span data-stu-id="fd430-115">Extension properties extend the schema of the user objects in the directory.</span></span>  <span data-ttu-id="fd430-116">條款擴充屬性、自訂屬性及自訂宣告在本文內容中係指相同的動作，且名稱會根據內容 (應用程式、物件、原則) 而有所不同。</span><span class="sxs-lookup"><span data-stu-id="fd430-116">The terms extension property, custom attribute and custom claim refer to the same thing in the context of this article and the name varies depending on the context (application, object, policy).</span></span>

<span data-ttu-id="fd430-117">擴充屬性只能註冊在應用程式物件上，即使這些屬性可能包含使用者的資料也是如此。</span><span class="sxs-lookup"><span data-stu-id="fd430-117">Extension properties can only be registered on an Application object even though they may contain data for a User.</span></span> <span data-ttu-id="fd430-118">屬性會附加至應用程式。</span><span class="sxs-lookup"><span data-stu-id="fd430-118">The property is attached to the application.</span></span> <span data-ttu-id="fd430-119">應用程式物件必須取得寫入權限才能註冊擴充屬性。</span><span class="sxs-lookup"><span data-stu-id="fd430-119">The Application object must be granted write access to register an extension property.</span></span> <span data-ttu-id="fd430-120">任何單一物件均可寫入 100 個擴充屬性 (所有類型和所有應用程式皆可)。</span><span class="sxs-lookup"><span data-stu-id="fd430-120">100 Extension properties (across ALL types and ALL applications) can be written to any single object.</span></span> <span data-ttu-id="fd430-121">擴充屬性會新增到目標目錄類型，而且在 Azure AD B2C 目錄租用戶中會立即變成可供存取。</span><span class="sxs-lookup"><span data-stu-id="fd430-121">Extension properties are added to the target directory type and becomes immediately accessible in the Azure AD B2C directory tenant.</span></span>
<span data-ttu-id="fd430-122">如果您刪除應用程式，則這些擴充屬性以及其中包含之所有使用者的資料也會全部移除。</span><span class="sxs-lookup"><span data-stu-id="fd430-122">If the application is deleted, those Extension properties along with any data contained in them for all users are also removed.</span></span> <span data-ttu-id="fd430-123">如果應用程式刪除擴充屬性，則擴充屬性會從目標目錄物件上移除，並且會將值刪除。</span><span class="sxs-lookup"><span data-stu-id="fd430-123">If an extension property is deleted by the Application, it is removed on the target directory objects, and the values deleted.</span></span>

<span data-ttu-id="fd430-124">擴充屬性只存在於租用戶中已註冊之應用程式的內容裡。</span><span class="sxs-lookup"><span data-stu-id="fd430-124">Extension properties exist only in the context of a registered  Application in the tenant.</span></span> <span data-ttu-id="fd430-125">該應用程式的物件識別碼必須包含在使用該識別碼的 TechnicalProfile 中。</span><span class="sxs-lookup"><span data-stu-id="fd430-125">The object id of that Application must be included in the TechnicalProfile that use it.</span></span>

>[!NOTE]
><span data-ttu-id="fd430-126">Azure AD B2C 目錄通常包含名為 `b2c-extensions-app` 的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="fd430-126">The Azure AD B2C directory typically includes a Web App named `b2c-extensions-app`.</span></span>  <span data-ttu-id="fd430-127">此應用程式主要是供 b2c 內建原則用在透過 Azure 入口網站所建立的自訂宣告中。</span><span class="sxs-lookup"><span data-stu-id="fd430-127">This application is primarily used by the b2c built-in  policies for the custom claims created via the Azure portal.</span></span>  <span data-ttu-id="fd430-128">使用此應用程式來為 b2c 自訂原則註冊擴充屬性的建議，僅適用於進階使用者。</span><span class="sxs-lookup"><span data-stu-id="fd430-128">Using this application to register extensions for b2c custom policies is recommended only for advanced users.</span></span>  <span data-ttu-id="fd430-129">相關指示包含在本文的＜後續步驟＞一節中。</span><span class="sxs-lookup"><span data-stu-id="fd430-129">Instructions for this are included in the Next Steps section in this article.</span></span>


## <a name="creating-a-new-application-to-store-the-extension-properties"></a><span data-ttu-id="fd430-130">建立新的應用程式來儲存擴充屬性</span><span class="sxs-lookup"><span data-stu-id="fd430-130">Creating a new application to store the extension properties</span></span>

1. <span data-ttu-id="fd430-131">開啟瀏覽工作階段並瀏覽至 [Azure 入口網站](https://portal.azure.com)，然後使用您想要設定之 B2C 目錄的系統管理認證來登入。</span><span class="sxs-lookup"><span data-stu-id="fd430-131">Open a browsing session and navigate to the [Azure porta](https://portal.azure.com) and sign in with administrative credentials of the B2C Directory you wish to configure.</span></span>
1. <span data-ttu-id="fd430-132">在左方的導覽功能表中，按一下 [Azure Active Directory]。</span><span class="sxs-lookup"><span data-stu-id="fd430-132">Click **Azure Active Directory** on the left navigation menu.</span></span> <span data-ttu-id="fd430-133">您可能需要選取 [更多服務 >] 才能找到它。</span><span class="sxs-lookup"><span data-stu-id="fd430-133">You may need to find it by selecting More services>.</span></span>
1. <span data-ttu-id="fd430-134">選取 [應用程式註冊]，然後按一下 [新增應用程式註冊]</span><span class="sxs-lookup"><span data-stu-id="fd430-134">Select **App registrations** and click **New application registration**</span></span>
1. <span data-ttu-id="fd430-135">提供下列建議項目︰</span><span class="sxs-lookup"><span data-stu-id="fd430-135">Provide the following recommended entries:</span></span>
  * <span data-ttu-id="fd430-136">指定 Web 應用程式的名稱：**WebApp-GraphAPI-DirectoryExtensions**</span><span class="sxs-lookup"><span data-stu-id="fd430-136">Specify a name for the web application: **WebApp-GraphAPI-DirectoryExtensions**</span></span>
  * <span data-ttu-id="fd430-137">應用程式類型︰Web 應用程式/API</span><span class="sxs-lookup"><span data-stu-id="fd430-137">Application type: Web app/API</span></span>
  * <span data-ttu-id="fd430-138">登入 URL：https://{tenantName}.onmicrosoft.com/WebApp-GraphAPI-DirectoryExtensions</span><span class="sxs-lookup"><span data-stu-id="fd430-138">Sign-on URL:https://{tenantName}.onmicrosoft.com/WebApp-GraphAPI-DirectoryExtensions</span></span>
1. <span data-ttu-id="fd430-139">選取 **[建立]。</span><span class="sxs-lookup"><span data-stu-id="fd430-139">Select **Create.</span></span> <span data-ttu-id="fd430-140">[通知] 中會出現成功完成</span><span class="sxs-lookup"><span data-stu-id="fd430-140">Successful completion appears in the **notifications**</span></span>
1. <span data-ttu-id="fd430-141">選取新建立的 Web 應用程式：**WebApp-GraphAPI-DirectoryExtensions**</span><span class="sxs-lookup"><span data-stu-id="fd430-141">Select the newly created web application: **WebApp-GraphAPI-DirectoryExtensions**</span></span>
1. <span data-ttu-id="fd430-142">選取 [設定]：**必要權限**</span><span class="sxs-lookup"><span data-stu-id="fd430-142">Select Settings: **Required permissions**</span></span>
1. <span data-ttu-id="fd430-143">選取 API [Windows Active Directory]</span><span class="sxs-lookup"><span data-stu-id="fd430-143">Select API **Windows Active Directory**</span></span>
1. <span data-ttu-id="fd430-144">在 [應用程式權限] 中標上核取記號：**讀取及寫入目錄資料**，然後**儲存**</span><span class="sxs-lookup"><span data-stu-id="fd430-144">Place a checkmark in Application Permissions: **Read and write directory data**, and **Save**</span></span>
1. <span data-ttu-id="fd430-145">選擇 [授與權限]，然後確認 [是]。</span><span class="sxs-lookup"><span data-stu-id="fd430-145">Choose **Grant permissions** and confirm **Yes**.</span></span>
1. <span data-ttu-id="fd430-146">將來自 WebApp-GraphAPI-DirectoryExtensions>Settings>Properties> 的下列識別碼複製到剪貼簿並儲存</span><span class="sxs-lookup"><span data-stu-id="fd430-146">Copy to your clipboard and save the following identifiers from WebApp-GraphAPI-DirectoryExtensions>Settings>Properties></span></span>
*  <span data-ttu-id="fd430-147">**應用程式識別碼**。</span><span class="sxs-lookup"><span data-stu-id="fd430-147">**Application ID** .</span></span> <span data-ttu-id="fd430-148">範例： `103ee0e6-f92d-4183-b576-8c3739027780`</span><span class="sxs-lookup"><span data-stu-id="fd430-148">Example: `103ee0e6-f92d-4183-b576-8c3739027780`</span></span>
* <span data-ttu-id="fd430-149">**物件識別碼**。</span><span class="sxs-lookup"><span data-stu-id="fd430-149">**Object ID**.</span></span> <span data-ttu-id="fd430-150">範例： `80d8296a-da0a-49ee-b6ab-fd232aa45201`</span><span class="sxs-lookup"><span data-stu-id="fd430-150">Example: `80d8296a-da0a-49ee-b6ab-fd232aa45201`</span></span>



## <a name="modifying-your-custom-policy-to-add-the-applicationobjectid"></a><span data-ttu-id="fd430-151">修改您的自訂原則以新增 ApplicationObjectId</span><span class="sxs-lookup"><span data-stu-id="fd430-151">Modifying your custom policy to add the ApplicationObjectId</span></span>

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
><span data-ttu-id="fd430-152"><TechnicalProfile Id="AAD-Common"> 是指「通用」，因為其元素會包含在其中，且會透過下列元素而重複使用在所有的 Azure Active Directory TechnicalProfiles 中︰`<IncludeTechnicalProfile ReferenceId="AAD-Common" />`</span><span class="sxs-lookup"><span data-stu-id="fd430-152">The <TechnicalProfile Id="AAD-Common"> is referred to as "common" because its elements are included in and reused in all the Azure Active Directory TechnicalProfiles by using the element: `<IncludeTechnicalProfile ReferenceId="AAD-Common" />`</span></span>

>[!NOTE]
><span data-ttu-id="fd430-153">當 TechnicalProfile 第一次寫入新建立的擴充屬性中時，您可能會遇到一次性錯誤。</span><span class="sxs-lookup"><span data-stu-id="fd430-153">When the TechnicalProfile writes for the first time to the newly created extension property, you may experience a one-time error.</span></span>  <span data-ttu-id="fd430-154">第一次使用時，會建立擴充屬性。</span><span class="sxs-lookup"><span data-stu-id="fd430-154">The extension property is created the first time it is used.</span></span>  

## <a name="using-the-new-extension-property--custom-attribute-in-a-user-journey"></a><span data-ttu-id="fd430-155">在使用者旅程中使用新的擴充屬性/自訂屬性</span><span class="sxs-lookup"><span data-stu-id="fd430-155">Using the new extension property / custom attribute in a user journey</span></span>


1. <span data-ttu-id="fd430-156">開啟信賴憑證者 (RP) 檔案，此檔案會描述您的原則編輯使用者旅程。</span><span class="sxs-lookup"><span data-stu-id="fd430-156">Open the Relying Party(RP) file that describes your policy edit user journey.</span></span>  <span data-ttu-id="fd430-157">如果您要開始，我們的建議可能是直接從 Azure 入口網站中的 [Azure B2C 自訂原則] 區段，下載您已設定的 RP-PolicyEdit 檔案版本。</span><span class="sxs-lookup"><span data-stu-id="fd430-157">If you are starting out, it may be advisable to download your already configured version of the RP-PolicyEdit file directly from the Azure B2C Custom Policy section in the Azure portal.</span></span>  <span data-ttu-id="fd430-158">或者，您也可以從儲存體資料夾開啟 XML 檔案。</span><span class="sxs-lookup"><span data-stu-id="fd430-158">Alternatively, open your XML file from your storage folder.</span></span>
2. <span data-ttu-id="fd430-159">新增自訂宣告 `loyaltyId`。</span><span class="sxs-lookup"><span data-stu-id="fd430-159">Add a custom claim `loyaltyId`.</span></span>  <span data-ttu-id="fd430-160">藉由在 `<RelyingParty>` 元素中包含自訂宣告，它就會以參數形式傳遞至 UserJourney TechnicalProfiles，並包含在應用程式的權杖中。</span><span class="sxs-lookup"><span data-stu-id="fd430-160">By including the custom claim in the `<RelyingParty>` element, it is passed as a parameter to the UserJourney TechnicalProfiles and included in the token for the application.</span></span>
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
3. <span data-ttu-id="fd430-161">在 `<ClaimsSchema>` 元素內的擴充原則檔 `TrustFrameworkExtensions.xml` 新增宣告定義，如下所示。</span><span class="sxs-lookup"><span data-stu-id="fd430-161">Add a claim definition to the Extension policy file  `TrustFrameworkExtensions.xml` inside the `<ClaimsSchema>` element as shown.</span></span>
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
4. <span data-ttu-id="fd430-162">在基底原則檔 `TrustFrameworkBase.xml` 中新增相同的宣告定義。</span><span class="sxs-lookup"><span data-stu-id="fd430-162">Add the same claim definition to the Base policy file `TrustFrameworkBase.xml`.</span></span>  
><span data-ttu-id="fd430-163">通常不需同時在基底原則檔和擴充原則檔中新增 `ClaimType` 定義，不過，由於接下來的步驟會將 extension_loyaltyId 新增到基底原則檔的 TechnicalProfiles 中，因此原則驗證器將拒絕上傳沒有此項目的基底原則檔。</span><span class="sxs-lookup"><span data-stu-id="fd430-163">Adding a `ClaimType` definition in both the base and the extensions file is normally not necessary, however since the next steps will add the extension_loyaltyId to TechnicalProfiles in the Base file, the policy validator will reject the upload of the base file without it.</span></span>
><span data-ttu-id="fd430-164">追蹤 TrustFrameworkBase.xml 檔案中名為「ProfileEdit」之使用者旅程圖的執行情形可能有用。</span><span class="sxs-lookup"><span data-stu-id="fd430-164">It may be useful to trace the execution of the user journey named "ProfileEdit" in the TrustFrameworkBase.xml file.</span></span>  <span data-ttu-id="fd430-165">請在編輯器中搜尋相同名稱的使用者旅程，並注意到協調流程步驟 5 會叫用 TechnicalProfileReferenceID="SelfAsserted-ProfileUpdate"。</span><span class="sxs-lookup"><span data-stu-id="fd430-165">Search for the user journey of the same name in your editor and observe that Orchestration Step 5 invokes the TechnicalProfileReferenceID="SelfAsserted-ProfileUpdate".</span></span>  <span data-ttu-id="fd430-166">搜尋並檢查此 TechnicalProfile 以熟悉流程。</span><span class="sxs-lookup"><span data-stu-id="fd430-166">Search and inspect this TechnicalProfile to familiarize yourself with the flow.</span></span>
5. <span data-ttu-id="fd430-167">在 TechnicalProfile "SelfAsserted-ProfileUpdate" 中新增 loyaltyId 來作為輸入和輸出宣告</span><span class="sxs-lookup"><span data-stu-id="fd430-167">Add loyaltyId as input and output claim in the TechnicalProfile "SelfAsserted-ProfileUpdate"</span></span>
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

            <!-- Optional claims. These claims are collected from the user and can be modified. Any claim added here should be updated in the
                 ValidationTechnicalProfile referenced below so it can be written to directory after being updateed by the user, i.e. AAD-UserWriteProfileUsingObjectId. -->
            <InputClaim ClaimTypeReferenceId="givenName" />
            <InputClaim ClaimTypeReferenceId="surname" />
            <InputClaim ClaimTypeReferenceId="extension_loyaltyId"/>
          </InputClaims>
          <OutputClaims>
            <!-- Required claims -->
            <OutputClaim ClaimTypeReferenceId="executed-SelfAsserted-Input" DefaultValue="true" />

            <!-- Optional claims. These claims are collected from the user and can be modified. Any claim added here should be updated in the
                 ValidationTechnicalProfile referenced below so it can be written to directory after being updateed by the user, i.e. AAD-UserWriteProfileUsingObjectId. -->
            <OutputClaim ClaimTypeReferenceId="givenName" />
            <OutputClaim ClaimTypeReferenceId="surname" />
            <OutputClaim ClaimTypeReferenceId="extension_loyaltyId"/>
          </OutputClaims>
          <ValidationTechnicalProfiles>
            <ValidationTechnicalProfile ReferenceId="AAD-UserWriteProfileUsingObjectId" />
          </ValidationTechnicalProfiles>
        </TechnicalProfile>
```
6. <span data-ttu-id="fd430-168">在 TechnicalProfile "AAD-UserWriteProfileUsingObjectId" 中新增宣告，針對目錄中的目前使用者將宣告值保存在擴充屬性中。</span><span class="sxs-lookup"><span data-stu-id="fd430-168">Add claim in TechnicalProfile "AAD-UserWriteProfileUsingObjectId" to persist the value of the claim in the extension property, for the current user in the directory.</span></span>
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
7. <span data-ttu-id="fd430-169">在 TechnicalProfile "AAD-UserReadUsingObjectId" 中新增宣告，以在每次使用者登入時讀取擴充屬性的值。</span><span class="sxs-lookup"><span data-stu-id="fd430-169">Add claim in TechnicalProfile "AAD-UserReadUsingObjectId" to read the value of the extension attribute every time a user logs in.</span></span> <span data-ttu-id="fd430-170">到目前為止，只有本機帳戶的流程已變更 TechnicalProfiles。</span><span class="sxs-lookup"><span data-stu-id="fd430-170">Thus far the TechnicalProfiles have been changed in the flow of local accounts only.</span></span>  <span data-ttu-id="fd430-171">如果您需要將新屬性用在社交/同盟帳戶的流程中，就必須變更一組不同的 TechnicalProfiles。</span><span class="sxs-lookup"><span data-stu-id="fd430-171">If the new attribute is desired in the flow of a social/federated account, a different set of TechnicalProfiles needs to be changed.</span></span> <span data-ttu-id="fd430-172">請參閱後續步驟。</span><span class="sxs-lookup"><span data-stu-id="fd430-172">See Next Steps.</span></span>

```xml
<!-- The following technical profile is used to read data after user authenticates. -->
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
><span data-ttu-id="fd430-173">IncludeTechnicalProfile 元素會將 AAD-Common 的所有元素新增到這個 TechnicalProfile。</span><span class="sxs-lookup"><span data-stu-id="fd430-173">The IncludeTechnicalProfile element adds all the elements of AAD-Common to this TechnicalProfile.</span></span>

## <a name="test-the-custom-policy-using-run-now"></a><span data-ttu-id="fd430-174">使用 [立即執行] 測試自訂原則</span><span class="sxs-lookup"><span data-stu-id="fd430-174">Test the custom policy using "Run Now"</span></span>
1. <span data-ttu-id="fd430-175">開啟 [Azure AD B2C] 刀鋒視窗，然後巡覽至 [識別體驗架構] > [自訂原則]。</span><span class="sxs-lookup"><span data-stu-id="fd430-175">Open the **Azure AD B2C Blade** and navigate to **Identity Experience Framework > Custom policies**.</span></span>
1. <span data-ttu-id="fd430-176">選取您上傳的自訂原則，按一下 [立即執行] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="fd430-176">Select the custom policy that you uploaded, and click the **Run now** button.</span></span>
1. <span data-ttu-id="fd430-177">您應該可以使用電子郵件地址註冊。</span><span class="sxs-lookup"><span data-stu-id="fd430-177">You should be able to sign up using an email address.</span></span>

<span data-ttu-id="fd430-178">傳送回應用程式的識別碼權杖，會以自訂宣告的形式來包含新的擴充屬性，且此宣告前面會加上 extension_loyaltyId。</span><span class="sxs-lookup"><span data-stu-id="fd430-178">The  id token sent back to your application includes the new extension property as a custom claim preceded by extension_loyaltyId.</span></span> <span data-ttu-id="fd430-179">請參閱範例。</span><span class="sxs-lookup"><span data-stu-id="fd430-179">See example.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="fd430-180">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fd430-180">Next steps</span></span>

<span data-ttu-id="fd430-181">藉由變更下列 TechnicalProfiles，將新宣告新增至社交帳戶登入的流程。</span><span class="sxs-lookup"><span data-stu-id="fd430-181">Add the new claim to the flows for social account logins by changing the TechnicalProfiles listed.</span></span> <span data-ttu-id="fd430-182">社交/同盟帳戶登入會使用這兩個 TechnicalProfiles，以 alternativeSecurityId 作為使用者物件的定位器來寫入和讀取使用者資料。</span><span class="sxs-lookup"><span data-stu-id="fd430-182">These two TechnicalProfiles are used by social/federated account logins to write and read the user data using the alternativeSecurityId as the locator of the user object.</span></span>
```
  <TechnicalProfile Id="AAD-UserWriteUsingAlternativeSecurityId">

  <TechnicalProfile Id="AAD-UserReadUsingAlternativeSecurityId">
```

<span data-ttu-id="fd430-183">使用內建和自訂原則之間的相同擴充屬性。</span><span class="sxs-lookup"><span data-stu-id="fd430-183">Using the same extension attributes between built-in and custom policies.</span></span>
<span data-ttu-id="fd430-184">當您透過入口網站體驗新增擴充屬性 (也稱為自訂屬性) 時，系統會使用存在於每個 b2c 租用戶中的 **b2c-extensions-app 來註冊這些屬性。</span><span class="sxs-lookup"><span data-stu-id="fd430-184">When you add extension attributes (aka custom attributes) via the portal experience, those attributes are registered using the **b2c-extensions-app that exists in every b2c tenant.</span></span>  <span data-ttu-id="fd430-185">若要在自訂原則中使用這些擴充屬性：</span><span class="sxs-lookup"><span data-stu-id="fd430-185">To use these extension attributes in your custom policy:</span></span>
1. <span data-ttu-id="fd430-186">在 portal.azure.com 中的 b2c 租用戶內，巡覽至 **Azure Active Directory** 並選取 [應用程式註冊]</span><span class="sxs-lookup"><span data-stu-id="fd430-186">Within your b2c tenant in portal.azure.com, navigate to **Azure Active Directory** and select **App registrations**</span></span>
2. <span data-ttu-id="fd430-187">尋找您的 **b2c-extensions-app** 並加以選取</span><span class="sxs-lookup"><span data-stu-id="fd430-187">Find your **b2c-extensions-app** and select it</span></span>
3. <span data-ttu-id="fd430-188">在 [基本資訊] 之下，記錄 [應用程式識別碼] 和 [物件識別碼]</span><span class="sxs-lookup"><span data-stu-id="fd430-188">Under 'Essentials' record the **Application ID** and the **Object ID**</span></span>
4. <span data-ttu-id="fd430-189">將它們包含在您的 AAD-Common Technical 設定檔中繼資料中，如下所示：</span><span class="sxs-lookup"><span data-stu-id="fd430-189">Include them in your AAD-Common Technical profile metadata like as follows:</span></span>

```xml
    <ClaimsProviders>
        <ClaimsProvider>
              <DisplayName>Azure Active Directory</DisplayName>
            <TechnicalProfile Id="AAD-Common">
              <DisplayName>Azure Active Directory</DisplayName>
              <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.AzureActiveDirectoryProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
              <!-- Provide objectId and appId before using extension properties. -->
              <Metadata>
                <Item Key="ApplicationObjectId">insert objectId here</Item> <!-- This is the "Object ID" from the "b2c-extensions-app"-->
                <Item Key="ClientId">insert appId here</Item> <!--This is the "Application ID" from the "b2c-extensions-app"-->
              </Metadata>
```

<span data-ttu-id="fd430-190">若要與入口網站體驗保持一致性，請先使用入口網站 UI 建立這些屬性，「然後」在自訂原則中使用它們。</span><span class="sxs-lookup"><span data-stu-id="fd430-190">To keep consistency with the portal experience, create these attributes using the portal UI *before* you use them in your custom policies.</span></span>  <span data-ttu-id="fd430-191">當您在入口網站中建立屬性 "ActivationStatus" 時，您必須參考它，如下所示：</span><span class="sxs-lookup"><span data-stu-id="fd430-191">When you create an attribute "ActivationStatus" in the portal, you must refer to it as follows:</span></span>

```
extension_ActivationStatus in the custom policy
extension_<app-guid>_ActivationStatus via the Graph API.
```


## <a name="reference"></a><span data-ttu-id="fd430-192">參考</span><span class="sxs-lookup"><span data-stu-id="fd430-192">Reference</span></span>

* <span data-ttu-id="fd430-193">**技術設定檔 (TP)** 是一個元素類型，您可以將它想作是「函式」，而它可定義端點的名稱、其中繼資料、其通訊協定，並詳細說明身分識別體驗架構所應該執行的宣告交換。</span><span class="sxs-lookup"><span data-stu-id="fd430-193">A **Technical Profile (TP)** is an element type that can be thought of as a *function* that defines an endpoint’s name, its metadata, its protocol, and details the exchange of claims that the Identity Experience Framework should perform.</span></span>  <span data-ttu-id="fd430-194">當這個「函式」在協調流程步驟中或從另一個 TechnicalProfile 呼叫時，呼叫端會提供 InputClaims 和 OutputClaims 來作為參數。</span><span class="sxs-lookup"><span data-stu-id="fd430-194">When this *function* is called in an orchestration step or from another TechnicalProfile, the InputClaims and OutputClaims are provided as parameters by the caller.</span></span>


* <span data-ttu-id="fd430-195">如需擴充屬性的完整處理方式，請參閱[目錄結構描述擴充 | 圖形 API 概念](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions) \(英文\) 一文</span><span class="sxs-lookup"><span data-stu-id="fd430-195">For full treatment on extension properties, see the article [DIRECTORY SCHEMA EXTENSIONS | GRAPH API CONCEPTS](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions)</span></span>

>[!NOTE]
><span data-ttu-id="fd430-196">圖形 API 中的擴充屬性會使用 `extension_ApplicationObjectID_attributename` 慣例來命名。</span><span class="sxs-lookup"><span data-stu-id="fd430-196">Extension attributes in Graph API are named using the convention `extension_ApplicationObjectID_attributename`.</span></span> <span data-ttu-id="fd430-197">自訂原則會將擴充屬性稱為 extension_attributename，因此會省略 XML 中的 ApplicationObjectId</span><span class="sxs-lookup"><span data-stu-id="fd430-197">Custom policies refer to extensions attributes as extension_attributename, thus omitting the ApplicationObjectId in the XML</span></span>
