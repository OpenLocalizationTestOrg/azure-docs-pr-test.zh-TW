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
# <a name="azure-active-directory-b2c-creating-and-using-custom-attributes-in-a-custom-profile-edit-policy"></a><span data-ttu-id="7f1ca-103">Azure Active Directory B2C︰在自訂設定檔編輯原則中建立和使用自訂屬性</span><span class="sxs-lookup"><span data-stu-id="7f1ca-103">Azure Active Directory B2C: Creating and using custom attributes in a custom profile edit policy</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="7f1ca-104">本文中，您在 Azure AD B2C 目錄中建立的自訂屬性，並做為自訂宣告 hello 設定檔編輯使用者旅程中使用這個新屬性。</span><span class="sxs-lookup"><span data-stu-id="7f1ca-104">In this article, you create a custom attribute in your Azure AD B2C directory and use this new attribute as a custom claim in hello profile edit user journey.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7f1ca-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="7f1ca-105">Prerequisites</span></span>

<span data-ttu-id="7f1ca-106">Hello 文件中的步驟完成 hello[開始使用自訂原則](active-directory-b2c-get-started-custom.md)。</span><span class="sxs-lookup"><span data-stu-id="7f1ca-106">Complete hello steps in hello article [Getting Started with Custom Policies](active-directory-b2c-get-started-custom.md).</span></span>

## <a name="use-custom-attributes-toocollect-information-about-your-customers-in-azure-active-directory-b2c-using-custom-policies"></a><span data-ttu-id="7f1ca-107">使用您的客戶，在 Azure Active Directory B2C 中使用自訂原則的自訂屬性 toocollect 資訊</span><span class="sxs-lookup"><span data-stu-id="7f1ca-107">Use custom attributes toocollect information about your customers in Azure Active Directory B2C using custom policies</span></span>
<span data-ttu-id="7f1ca-108">您的 Azure Active Directory (Azure AD) B2C 目錄隨附一組內建屬性：名字、姓氏、城市、郵遞區號、userPrincipalName 等等。您通常需要 toocreate 您自己的屬性。</span><span class="sxs-lookup"><span data-stu-id="7f1ca-108">Your Azure Active Directory (Azure AD) B2C directory comes with a built-in set of attributes: Given Name, Surname, City, Postal Code, userPrincipalName, etc.  You often need toocreate your own attributes.</span></span>  <span data-ttu-id="7f1ca-109">例如：</span><span class="sxs-lookup"><span data-stu-id="7f1ca-109">For example:</span></span>
* <span data-ttu-id="7f1ca-110">客戶對向應用程式需要 toopersist 屬性，例如"LoyaltyNumber。 」</span><span class="sxs-lookup"><span data-stu-id="7f1ca-110">A customer-facing application needs toopersist an attribute such as "LoyaltyNumber."</span></span>
* <span data-ttu-id="7f1ca-111">識別提供者擁有必須儲存的唯一使用者識別碼，例如「uniqueUserGUID」。</span><span class="sxs-lookup"><span data-stu-id="7f1ca-111">An identity provider has a unique user identifier that must be saved such as "uniqueUserGUID.""</span></span>
* <span data-ttu-id="7f1ca-112">自訂使用者之旅需要 toopersist hello 狀態的使用者，例如"migrationStatus。 」</span><span class="sxs-lookup"><span data-stu-id="7f1ca-112">A custom user journey needs toopersist hello state of user such as "migrationStatus."</span></span>

<span data-ttu-id="7f1ca-113">您可以使用 Azure AD B2C，擴充 hello 組儲存在每個使用者帳戶上的屬性。</span><span class="sxs-lookup"><span data-stu-id="7f1ca-113">With Azure AD B2C, you can extend hello set of attributes stored on each user account.</span></span> <span data-ttu-id="7f1ca-114">您也可以讀取和寫入這些屬性使用 hello [Azure AD Graph API](active-directory-b2c-devquickstarts-graph-dotnet.md)。</span><span class="sxs-lookup"><span data-stu-id="7f1ca-114">You can also read and write these attributes by using hello [Azure AD Graph API](active-directory-b2c-devquickstarts-graph-dotnet.md).</span></span>

<span data-ttu-id="7f1ca-115">擴充功能屬性擴充 hello hello hello 目錄中的使用者物件的結構描述。</span><span class="sxs-lookup"><span data-stu-id="7f1ca-115">Extension properties extend hello schema of hello user objects in hello directory.</span></span>  <span data-ttu-id="7f1ca-116">hello 條款延伸模組屬性，並自訂屬性和自訂宣告，請參閱的 toohello hello 這個發行項與 hello 名稱內容中有相同的動作而異 hello 內容 （應用程式、 物件、 原則）。</span><span class="sxs-lookup"><span data-stu-id="7f1ca-116">hello terms extension property, custom attribute and custom claim refer toohello same thing in hello context of this article and hello name varies depending on hello context (application, object, policy).</span></span>

<span data-ttu-id="7f1ca-117">擴充屬性只能註冊在應用程式物件上，即使這些屬性可能包含使用者的資料也是如此。</span><span class="sxs-lookup"><span data-stu-id="7f1ca-117">Extension properties can only be registered on an Application object even though they may contain data for a User.</span></span> <span data-ttu-id="7f1ca-118">hello 屬性是附加的 toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7f1ca-118">hello property is attached toohello application.</span></span> <span data-ttu-id="7f1ca-119">hello 應用程式物件必須授與的寫入權限 tooregister 延伸模組屬性。</span><span class="sxs-lookup"><span data-stu-id="7f1ca-119">hello Application object must be granted write access tooregister an extension property.</span></span> <span data-ttu-id="7f1ca-120">100 個擴充功能屬性 （跨越所有類型和所有應用程式） 可以寫入 tooany 單一物件。</span><span class="sxs-lookup"><span data-stu-id="7f1ca-120">100 Extension properties (across ALL types and ALL applications) can be written tooany single object.</span></span> <span data-ttu-id="7f1ca-121">擴充功能屬性會加入 toohello 目標目錄類型，並可立即存取 hello Azure AD B2C 目錄租用戶中。</span><span class="sxs-lookup"><span data-stu-id="7f1ca-121">Extension properties are added toohello target directory type and becomes immediately accessible in hello Azure AD B2C directory tenant.</span></span>
<span data-ttu-id="7f1ca-122">如果刪除 hello 應用程式時，也會移除這些擴充功能屬性，以及它們對所有使用者所包含的任何資料。</span><span class="sxs-lookup"><span data-stu-id="7f1ca-122">If hello application is deleted, those Extension properties along with any data contained in them for all users are also removed.</span></span> <span data-ttu-id="7f1ca-123">如果 hello 應用程式刪除擴充功能屬性，則它也會移除上 hello hello 刪除的值和目標目錄物件。</span><span class="sxs-lookup"><span data-stu-id="7f1ca-123">If an extension property is deleted by hello Application, it is removed on hello target directory objects, and hello values deleted.</span></span>

<span data-ttu-id="7f1ca-124">擴充功能屬性只存在於 hello hello 租用戶中註冊的應用程式內容。</span><span class="sxs-lookup"><span data-stu-id="7f1ca-124">Extension properties exist only in hello context of a registered  Application in hello tenant.</span></span> <span data-ttu-id="7f1ca-125">hello 物件識別碼，該應用程式必須包含在 hello TechnicalProfile 使用它。</span><span class="sxs-lookup"><span data-stu-id="7f1ca-125">hello object id of that Application must be included in hello TechnicalProfile that use it.</span></span>

>[!NOTE]
><span data-ttu-id="7f1ca-126">hello Azure AD B2C 目錄通常會包含名為 Web 應用程式`b2c-extensions-app`。</span><span class="sxs-lookup"><span data-stu-id="7f1ca-126">hello Azure AD B2C directory typically includes a Web App named `b2c-extensions-app`.</span></span>  <span data-ttu-id="7f1ca-127">此應用程式主要用於由 hello b2c 內建原則 hello 透過 hello Azure 入口網站建立的自訂宣告。</span><span class="sxs-lookup"><span data-stu-id="7f1ca-127">This application is primarily used by hello b2c built-in  policies for hello custom claims created via hello Azure portal.</span></span>  <span data-ttu-id="7f1ca-128">建議使用此應用程式 tooregister 副檔名 b2c 自訂原則僅適用於進階使用者。</span><span class="sxs-lookup"><span data-stu-id="7f1ca-128">Using this application tooregister extensions for b2c custom policies is recommended only for advanced users.</span></span>  <span data-ttu-id="7f1ca-129">Hello 本文章中的後續步驟 > 一節中包含這個指示。</span><span class="sxs-lookup"><span data-stu-id="7f1ca-129">Instructions for this are included in hello Next Steps section in this article.</span></span>


## <a name="creating-a-new-application-toostore-hello-extension-properties"></a><span data-ttu-id="7f1ca-130">建立新的應用程式 toostore hello 擴充功能屬性</span><span class="sxs-lookup"><span data-stu-id="7f1ca-130">Creating a new application toostore hello extension properties</span></span>

1. <span data-ttu-id="7f1ca-131">開啟瀏覽工作階段並瀏覽 toohello [Azure porta](https://portal.azure.com)並以 hello 想 tooconfigure B2C 目錄的系統管理認證登入。</span><span class="sxs-lookup"><span data-stu-id="7f1ca-131">Open a browsing session and navigate toohello [Azure porta](https://portal.azure.com) and sign in with administrative credentials of hello B2C Directory you wish tooconfigure.</span></span>
1. <span data-ttu-id="7f1ca-132">按一下**Azure Active Directory** hello 左的導覽功能表上。</span><span class="sxs-lookup"><span data-stu-id="7f1ca-132">Click **Azure Active Directory** on hello left navigation menu.</span></span> <span data-ttu-id="7f1ca-133">您可能需要的 toofind 它藉由選取多服務 >。</span><span class="sxs-lookup"><span data-stu-id="7f1ca-133">You may need toofind it by selecting More services>.</span></span>
1. <span data-ttu-id="7f1ca-134">選取 應用程式註冊，然後按一下新增應用程式註冊</span><span class="sxs-lookup"><span data-stu-id="7f1ca-134">Select **App registrations** and click **New application registration**</span></span>
1. <span data-ttu-id="7f1ca-135">提供 hello 下列建議的項目：</span><span class="sxs-lookup"><span data-stu-id="7f1ca-135">Provide hello following recommended entries:</span></span>
  * <span data-ttu-id="7f1ca-136">指定 hello web 應用程式的名稱： **WebApp-GraphAPI-DirectoryExtensions**</span><span class="sxs-lookup"><span data-stu-id="7f1ca-136">Specify a name for hello web application: **WebApp-GraphAPI-DirectoryExtensions**</span></span>
  * <span data-ttu-id="7f1ca-137">應用程式類型︰Web 應用程式/API</span><span class="sxs-lookup"><span data-stu-id="7f1ca-137">Application type: Web app/API</span></span>
  * <span data-ttu-id="7f1ca-138">登入 URL：https://{tenantName}.onmicrosoft.com/WebApp-GraphAPI-DirectoryExtensions</span><span class="sxs-lookup"><span data-stu-id="7f1ca-138">Sign-on URL:https://{tenantName}.onmicrosoft.com/WebApp-GraphAPI-DirectoryExtensions</span></span>
1. <span data-ttu-id="7f1ca-139">選取 **[建立]。</span><span class="sxs-lookup"><span data-stu-id="7f1ca-139">Select **Create.</span></span> <span data-ttu-id="7f1ca-140">成功完成，會出現在 hello**通知**</span><span class="sxs-lookup"><span data-stu-id="7f1ca-140">Successful completion appears in hello **notifications**</span></span>
1. <span data-ttu-id="7f1ca-141">選取新建立的 hello web 應用程式： **WebApp-GraphAPI-DirectoryExtensions**</span><span class="sxs-lookup"><span data-stu-id="7f1ca-141">Select hello newly created web application: **WebApp-GraphAPI-DirectoryExtensions**</span></span>
1. <span data-ttu-id="7f1ca-142">選取 [設定]：**必要權限**</span><span class="sxs-lookup"><span data-stu-id="7f1ca-142">Select Settings: **Required permissions**</span></span>
1. <span data-ttu-id="7f1ca-143">選取 API [Windows Active Directory]</span><span class="sxs-lookup"><span data-stu-id="7f1ca-143">Select API **Windows Active Directory**</span></span>
1. <span data-ttu-id="7f1ca-144">在 [應用程式權限] 中標上核取記號：**讀取及寫入目錄資料**，然後**儲存**</span><span class="sxs-lookup"><span data-stu-id="7f1ca-144">Place a checkmark in Application Permissions: **Read and write directory data**, and **Save**</span></span>
1. <span data-ttu-id="7f1ca-145">選擇 [授與權限]，然後確認 [是]。</span><span class="sxs-lookup"><span data-stu-id="7f1ca-145">Choose **Grant permissions** and confirm **Yes**.</span></span>
1. <span data-ttu-id="7f1ca-146">複製 tooyour 剪貼簿並儲存 hello WebApp-GraphAPI-DirectoryExtensions 中的下列識別項 > 設定 > 屬性 ></span><span class="sxs-lookup"><span data-stu-id="7f1ca-146">Copy tooyour clipboard and save hello following identifiers from WebApp-GraphAPI-DirectoryExtensions>Settings>Properties></span></span>
*  <span data-ttu-id="7f1ca-147">**應用程式識別碼**。</span><span class="sxs-lookup"><span data-stu-id="7f1ca-147">**Application ID** .</span></span> <span data-ttu-id="7f1ca-148">範例： `103ee0e6-f92d-4183-b576-8c3739027780`</span><span class="sxs-lookup"><span data-stu-id="7f1ca-148">Example: `103ee0e6-f92d-4183-b576-8c3739027780`</span></span>
* <span data-ttu-id="7f1ca-149">**物件識別碼**。</span><span class="sxs-lookup"><span data-stu-id="7f1ca-149">**Object ID**.</span></span> <span data-ttu-id="7f1ca-150">範例： `80d8296a-da0a-49ee-b6ab-fd232aa45201`</span><span class="sxs-lookup"><span data-stu-id="7f1ca-150">Example: `80d8296a-da0a-49ee-b6ab-fd232aa45201`</span></span>



## <a name="modifying-your-custom-policy-tooadd-hello-applicationobjectid"></a><span data-ttu-id="7f1ca-151">修改您的自訂原則 tooadd hello ApplicationObjectId</span><span class="sxs-lookup"><span data-stu-id="7f1ca-151">Modifying your custom policy tooadd hello ApplicationObjectId</span></span>

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
><span data-ttu-id="7f1ca-152">hello<TechnicalProfile Id="AAD-Common">是參照的 tooas 「 公用 」，因為其項目會包含在中，使用 hello 元素中所有 hello Azure Active Directory TechnicalProfiles 重複使用：`<IncludeTechnicalProfile ReferenceId="AAD-Common" />`</span><span class="sxs-lookup"><span data-stu-id="7f1ca-152">hello <TechnicalProfile Id="AAD-Common"> is referred tooas "common" because its elements are included in and reused in all hello Azure Active Directory TechnicalProfiles by using hello element: `<IncludeTechnicalProfile ReferenceId="AAD-Common" />`</span></span>

>[!NOTE]
><span data-ttu-id="7f1ca-153">Hello TechnicalProfile 寫入 hello 第一次 toohello 新建立的延伸模組屬性，您可能會遇到一次性的錯誤。</span><span class="sxs-lookup"><span data-stu-id="7f1ca-153">When hello TechnicalProfile writes for hello first time toohello newly created extension property, you may experience a one-time error.</span></span>  <span data-ttu-id="7f1ca-154">hello 延伸模組屬性會使用它的第一次建立 hello。</span><span class="sxs-lookup"><span data-stu-id="7f1ca-154">hello extension property is created hello first time it is used.</span></span>  

## <a name="using-hello-new-extension-property--custom-attribute-in-a-user-journey"></a><span data-ttu-id="7f1ca-155">使用新延伸模組屬性 hello / 使用者旅程中的自訂屬性</span><span class="sxs-lookup"><span data-stu-id="7f1ca-155">Using hello new extension property / custom attribute in a user journey</span></span>


1. <span data-ttu-id="7f1ca-156">開啟 hello 信賴憑證者 Party(RP) 檔案，其中描述您的原則中編輯使用者的旅程。</span><span class="sxs-lookup"><span data-stu-id="7f1ca-156">Open hello Relying Party(RP) file that describes your policy edit user journey.</span></span>  <span data-ttu-id="7f1ca-157">如果您要啟動，它可能會建議 toodownload 您已設定的 hello RP PolicyEdit 版本檔案直接從 hello Azure B2C 自訂原則 hello Azure 入口網站 」 一節。</span><span class="sxs-lookup"><span data-stu-id="7f1ca-157">If you are starting out, it may be advisable toodownload your already configured version of hello RP-PolicyEdit file directly from hello Azure B2C Custom Policy section in hello Azure portal.</span></span>  <span data-ttu-id="7f1ca-158">或者，您也可以從儲存體資料夾開啟 XML 檔案。</span><span class="sxs-lookup"><span data-stu-id="7f1ca-158">Alternatively, open your XML file from your storage folder.</span></span>
2. <span data-ttu-id="7f1ca-159">新增自訂宣告 `loyaltyId`。</span><span class="sxs-lookup"><span data-stu-id="7f1ca-159">Add a custom claim `loyaltyId`.</span></span>  <span data-ttu-id="7f1ca-160">藉由 hello 自訂宣告在 hello`<RelyingParty>`項目，它是做為參數 toohello UserJourney TechnicalProfiles 傳遞，而且包含在 hello 應用程式的 hello 語彙基元。</span><span class="sxs-lookup"><span data-stu-id="7f1ca-160">By including hello custom claim in hello `<RelyingParty>` element, it is passed as a parameter toohello UserJourney TechnicalProfiles and included in hello token for hello application.</span></span>
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
3. <span data-ttu-id="7f1ca-161">新增宣告定義 toohello 延伸原則檔`TrustFrameworkExtensions.xml`內 hello`<ClaimsSchema>`項目所示。</span><span class="sxs-lookup"><span data-stu-id="7f1ca-161">Add a claim definition toohello Extension policy file  `TrustFrameworkExtensions.xml` inside hello `<ClaimsSchema>` element as shown.</span></span>
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
4. <span data-ttu-id="7f1ca-162">新增 hello 相同宣告定義 toohello 基底原則檔`TrustFrameworkBase.xml`。</span><span class="sxs-lookup"><span data-stu-id="7f1ca-162">Add hello same claim definition toohello Base policy file `TrustFrameworkBase.xml`.</span></span>  
><span data-ttu-id="7f1ca-163">加入`ClaimType`hello 基底和 hello 延伸模組檔案中的定義為通常不必要的不過 hello 原則驗證程式因為 hello 接下來的步驟會加入 hello extension_loyaltyId tooTechnicalProfiles hello 基底檔案中，將會拒絕 hello 上傳hello 沒有它的基底檔案。</span><span class="sxs-lookup"><span data-stu-id="7f1ca-163">Adding a `ClaimType` definition in both hello base and hello extensions file is normally not necessary, however since hello next steps will add hello extension_loyaltyId tooTechnicalProfiles in hello Base file, hello policy validator will reject hello upload of hello base file without it.</span></span>
><span data-ttu-id="7f1ca-164">可能很有用的 tootrace hello 執行名為"ProfileEdit"hello TrustFrameworkBase.xml 檔案中的 hello 使用者之旅。</span><span class="sxs-lookup"><span data-stu-id="7f1ca-164">It may be useful tootrace hello execution of hello user journey named "ProfileEdit" in hello TrustFrameworkBase.xml file.</span></span>  <span data-ttu-id="7f1ca-165">搜尋的 hello 相同您編輯器中的名稱，並觀察協調流程步驟 5 叫用 hello TechnicalProfileReferenceID hello 使用者之旅 ="SelfAsserted ProfileUpdate"。</span><span class="sxs-lookup"><span data-stu-id="7f1ca-165">Search for hello user journey of hello same name in your editor and observe that Orchestration Step 5 invokes hello TechnicalProfileReferenceID="SelfAsserted-ProfileUpdate".</span></span>  <span data-ttu-id="7f1ca-166">搜尋並自行檢查此 TechnicalProfile toofamiliarize，與 hello 流量。</span><span class="sxs-lookup"><span data-stu-id="7f1ca-166">Search and inspect this TechnicalProfile toofamiliarize yourself with hello flow.</span></span>
5. <span data-ttu-id="7f1ca-167">加入輸入和輸出宣告在 hello TechnicalProfile"SelfAsserted ProfileUpdate"loyaltyId</span><span class="sxs-lookup"><span data-stu-id="7f1ca-167">Add loyaltyId as input and output claim in hello TechnicalProfile "SelfAsserted-ProfileUpdate"</span></span>
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
6. <span data-ttu-id="7f1ca-168">加入 TechnicalProfile"AAD UserWriteProfileUsingObjectId"toopersist hello 宣告的值為 hello hello 延伸模組屬性，在 hello hello 目錄中的目前使用者的宣告。</span><span class="sxs-lookup"><span data-stu-id="7f1ca-168">Add claim in TechnicalProfile "AAD-UserWriteProfileUsingObjectId" toopersist hello value of hello claim in hello extension property, for hello current user in hello directory.</span></span>
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
7. <span data-ttu-id="7f1ca-169">每次使用者登入時，新增宣告 TechnicalProfile"AAD UserReadUsingObjectId"tooread hello 值 hello 延伸模組屬性中。</span><span class="sxs-lookup"><span data-stu-id="7f1ca-169">Add claim in TechnicalProfile "AAD-UserReadUsingObjectId" tooread hello value of hello extension attribute every time a user logs in.</span></span> <span data-ttu-id="7f1ca-170">到目前為止 hello TechnicalProfiles hello 流程只使用本機帳戶中已變更。</span><span class="sxs-lookup"><span data-stu-id="7f1ca-170">Thus far hello TechnicalProfiles have been changed in hello flow of local accounts only.</span></span>  <span data-ttu-id="7f1ca-171">如果想要使用 hello 新屬性的社交/同盟帳戶 hello 資料流程中，一組不同的 TechnicalProfiles 需要 toobe 變更。</span><span class="sxs-lookup"><span data-stu-id="7f1ca-171">If hello new attribute is desired in hello flow of a social/federated account, a different set of TechnicalProfiles needs toobe changed.</span></span> <span data-ttu-id="7f1ca-172">請參閱後續步驟。</span><span class="sxs-lookup"><span data-stu-id="7f1ca-172">See Next Steps.</span></span>

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
><span data-ttu-id="7f1ca-173">hello IncludeTechnicalProfile 項目會加入所有 AAD-通用 toothis TechnicalProfile hello 項目。</span><span class="sxs-lookup"><span data-stu-id="7f1ca-173">hello IncludeTechnicalProfile element adds all hello elements of AAD-Common toothis TechnicalProfile.</span></span>

## <a name="test-hello-custom-policy-using-run-now"></a><span data-ttu-id="7f1ca-174">測試 hello 「 立即執行 」 使用的自訂原則</span><span class="sxs-lookup"><span data-stu-id="7f1ca-174">Test hello custom policy using "Run Now"</span></span>
1. <span data-ttu-id="7f1ca-175">開啟 hello **Azure AD B2C 刀鋒視窗**並瀏覽過**身分識別體驗架構 > 自訂原則**。</span><span class="sxs-lookup"><span data-stu-id="7f1ca-175">Open hello **Azure AD B2C Blade** and navigate too**Identity Experience Framework > Custom policies**.</span></span>
1. <span data-ttu-id="7f1ca-176">選取您上傳，hello 自訂原則，然後按一下 hello**立即執行** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7f1ca-176">Select hello custom policy that you uploaded, and click hello **Run now** button.</span></span>
1. <span data-ttu-id="7f1ca-177">您應該能夠 toosign 使用電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="7f1ca-177">You should be able toosign up using an email address.</span></span>

<span data-ttu-id="7f1ca-178">hello id 權杖送回 tooyour 應用程式加上 extension_loyaltyId 自訂宣告的形式包含 hello 新延伸模組屬性。</span><span class="sxs-lookup"><span data-stu-id="7f1ca-178">hello  id token sent back tooyour application includes hello new extension property as a custom claim preceded by extension_loyaltyId.</span></span> <span data-ttu-id="7f1ca-179">請參閱範例。</span><span class="sxs-lookup"><span data-stu-id="7f1ca-179">See example.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="7f1ca-180">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7f1ca-180">Next steps</span></span>

<span data-ttu-id="7f1ca-181">藉由變更的 hello TechnicalProfiles 列出新增 hello 新宣告 toohello 流程社交帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="7f1ca-181">Add hello new claim toohello flows for social account logins by changing hello TechnicalProfiles listed.</span></span> <span data-ttu-id="7f1ca-182">這些兩個 TechnicalProfiles 是由身分證/同盟帳戶登入 toowrite 和使用讀取 hello 使用者資料使用 hello alternativeSecurityId hello hello 使用者物件的定位器。</span><span class="sxs-lookup"><span data-stu-id="7f1ca-182">These two TechnicalProfiles are used by social/federated account logins toowrite and read hello user data using hello alternativeSecurityId as hello locator of hello user object.</span></span>
```
  <TechnicalProfile Id="AAD-UserWriteUsingAlternativeSecurityId">

  <TechnicalProfile Id="AAD-UserReadUsingAlternativeSecurityId">
```

<span data-ttu-id="7f1ca-183">使用 hello 內建和自訂原則之間的相同擴充功能屬性。</span><span class="sxs-lookup"><span data-stu-id="7f1ca-183">Using hello same extension attributes between built-in and custom policies.</span></span>
<span data-ttu-id="7f1ca-184">當您將透過 hello 入口網站體驗的延伸模組屬性 （也稱為自訂屬性） 時，這些屬性會註冊使用 hello * * b2c 擴充功能-應用程式存在於每個 b2c 租用戶。</span><span class="sxs-lookup"><span data-stu-id="7f1ca-184">When you add extension attributes (aka custom attributes) via hello portal experience, those attributes are registered using hello **b2c-extensions-app that exists in every b2c tenant.</span></span>  <span data-ttu-id="7f1ca-185">toouse 您自訂的原則中的這些延伸屬性：</span><span class="sxs-lookup"><span data-stu-id="7f1ca-185">toouse these extension attributes in your custom policy:</span></span>
1. <span data-ttu-id="7f1ca-186">B2c 租用戶的 portal.azure.com，內瀏覽過**Azure Active Directory**選取**應用程式註冊**</span><span class="sxs-lookup"><span data-stu-id="7f1ca-186">Within your b2c tenant in portal.azure.com, navigate too**Azure Active Directory** and select **App registrations**</span></span>
2. <span data-ttu-id="7f1ca-187">尋找您的 **b2c-extensions-app** 並加以選取</span><span class="sxs-lookup"><span data-stu-id="7f1ca-187">Find your **b2c-extensions-app** and select it</span></span>
3. <span data-ttu-id="7f1ca-188">在 'Essentials' 記錄 hello**應用程式識別碼**和 hello**物件識別碼**</span><span class="sxs-lookup"><span data-stu-id="7f1ca-188">Under 'Essentials' record hello **Application ID** and hello **Object ID**</span></span>
4. <span data-ttu-id="7f1ca-189">將它們包含在您的 AAD-Common Technical 設定檔中繼資料中，如下所示：</span><span class="sxs-lookup"><span data-stu-id="7f1ca-189">Include them in your AAD-Common Technical profile metadata like as follows:</span></span>

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

<span data-ttu-id="7f1ca-190">tookeep 一致性與 hello 入口網站體驗，建立這些屬性使用 hello 入口網站 UI*之前*您自訂的原則中使用它們。</span><span class="sxs-lookup"><span data-stu-id="7f1ca-190">tookeep consistency with hello portal experience, create these attributes using hello portal UI *before* you use them in your custom policies.</span></span>  <span data-ttu-id="7f1ca-191">當您建立屬性 」 ActivationStatus"hello 入口網站中時，您必須參考 tooit，如下所示：</span><span class="sxs-lookup"><span data-stu-id="7f1ca-191">When you create an attribute "ActivationStatus" in hello portal, you must refer tooit as follows:</span></span>

```
extension_ActivationStatus in hello custom policy
extension_<app-guid>_ActivationStatus via hello Graph API.
```


## <a name="reference"></a><span data-ttu-id="7f1ca-192">參考</span><span class="sxs-lookup"><span data-stu-id="7f1ca-192">Reference</span></span>

* <span data-ttu-id="7f1ca-193">A**技術設定檔 (TP)**是項目類型，可以視為*函式*來定義端點名稱、 它的中繼資料、 它的通訊協定，詳細資料 hello exchange 的 hello 身分識別的宣告應該執行體驗架構。</span><span class="sxs-lookup"><span data-stu-id="7f1ca-193">A **Technical Profile (TP)** is an element type that can be thought of as a *function* that defines an endpoint’s name, its metadata, its protocol, and details hello exchange of claims that hello Identity Experience Framework should perform.</span></span>  <span data-ttu-id="7f1ca-194">當這*函式*在協調流程的步驟中，或從另一個 TechnicalProfile，hello InputClaims OutputClaims 會提供和做為參數 hello 呼叫端呼叫。</span><span class="sxs-lookup"><span data-stu-id="7f1ca-194">When this *function* is called in an orchestration step or from another TechnicalProfile, hello InputClaims and OutputClaims are provided as parameters by hello caller.</span></span>


* <span data-ttu-id="7f1ca-195">完整的擴充屬性的處理方式，請參閱 hello 文章[目錄結構描述擴充功能 |GRAPH API 概念](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions)</span><span class="sxs-lookup"><span data-stu-id="7f1ca-195">For full treatment on extension properties, see hello article [DIRECTORY SCHEMA EXTENSIONS | GRAPH API CONCEPTS](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions)</span></span>

>[!NOTE]
><span data-ttu-id="7f1ca-196">Graph API 中的擴充屬性的命名慣例 hello `extension_ApplicationObjectID_attributename`。</span><span class="sxs-lookup"><span data-stu-id="7f1ca-196">Extension attributes in Graph API are named using hello convention `extension_ApplicationObjectID_attributename`.</span></span> <span data-ttu-id="7f1ca-197">自訂原則中參考 extension_attributename，因此省略 hello XML 中的 hello ApplicationObjectId tooextensions 屬性</span><span class="sxs-lookup"><span data-stu-id="7f1ca-197">Custom policies refer tooextensions attributes as extension_attributename, thus omitting hello ApplicationObjectId in hello XML</span></span>
