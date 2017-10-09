---
title: "Azure Active Directory B2C︰使用自訂原則新增 Google+ 作為 OAuth2 識別提供者"
description: "透過 OAuth2 通訊協定使用 Google+ 作為識別提供者的範例"
services: active-directory-b2c
documentationcenter: 
author: yoelhor
manager: joroja
editor: 
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 08/04/2017
ms.author: yoelh
ms.openlocfilehash: 4feff21979c9c3b3b12c7a1cae4db0121d1bd79b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-add-google-as-an-oauth2-identity-provider-using-custom-policies"></a><span data-ttu-id="7fda0-103">Azure Active Directory B2C︰使用自訂原則新增 Google+ 作為 OAuth2 識別提供者</span><span class="sxs-lookup"><span data-stu-id="7fda0-103">Azure Active Directory B2C: Add Google+ as an OAuth2 identity provider using custom policies</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="7fda0-104">本指南也說明如何 tooenable 登入的使用者從透過 hello 使用 Google + 帳戶[自訂原則](active-directory-b2c-overview-custom.md)。</span><span class="sxs-lookup"><span data-stu-id="7fda0-104">This guide shows you how tooenable sign-in for users from Google+ account through hello use of [custom policies](active-directory-b2c-overview-custom.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7fda0-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="7fda0-105">Prerequisites</span></span>

<span data-ttu-id="7fda0-106">完整的 hello 步驟 hello[開始使用自訂原則](active-directory-b2c-get-started-custom.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="7fda0-106">Complete hello steps in hello [Getting started with custom policies](active-directory-b2c-get-started-custom.md) article.</span></span>

<span data-ttu-id="7fda0-107">這些步驟包括：</span><span class="sxs-lookup"><span data-stu-id="7fda0-107">These steps include:</span></span>

1.  <span data-ttu-id="7fda0-108">建立 Google+ 帳戶應用程式。</span><span class="sxs-lookup"><span data-stu-id="7fda0-108">Creating a Google+ account application.</span></span>
2.  <span data-ttu-id="7fda0-109">加入 hello Google + 帳戶應用程式金鑰 tooAzure AD B2C</span><span class="sxs-lookup"><span data-stu-id="7fda0-109">Adding hello Google+ account application key tooAzure AD B2C</span></span>
3.  <span data-ttu-id="7fda0-110">新增宣告提供者 tooa 原則</span><span class="sxs-lookup"><span data-stu-id="7fda0-110">Adding claims provider tooa policy</span></span>
4.  <span data-ttu-id="7fda0-111">註冊 hello Google + 帳戶宣告提供者 tooa 使用者旅程</span><span class="sxs-lookup"><span data-stu-id="7fda0-111">Registering hello Google+ account claims provider tooa user journey</span></span>
5.  <span data-ttu-id="7fda0-112">上傳 hello 原則 tooan Azure AD B2C 租用戶，並進行測試</span><span class="sxs-lookup"><span data-stu-id="7fda0-112">Uploading hello policy tooan Azure AD B2C tenant and test it</span></span>

## <a name="create-a-google-account-application"></a><span data-ttu-id="7fda0-113">建立 Google+ 帳戶應用程式</span><span class="sxs-lookup"><span data-stu-id="7fda0-113">Create a Google+ account application</span></span>
<span data-ttu-id="7fda0-114">toouse Google + B2C Azure Active Directory (Azure AD) 中的身分識別提供者，您需要 toocreate Google + 應用程式和提供 hello 正確的參數。</span><span class="sxs-lookup"><span data-stu-id="7fda0-114">toouse Google+ as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a Google+ application and supply it with hello right parameters.</span></span> <span data-ttu-id="7fda0-115">您可以在這裡註冊 Google+ 應用程式：[https://accounts.google.com/SignUp](https://accounts.google.com/SignUp)</span><span class="sxs-lookup"><span data-stu-id="7fda0-115">You can register a Google+ application here: [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp)</span></span>

1.  <span data-ttu-id="7fda0-116">移 toohello [Google 開發人員主控台](https://console.developers.google.com/)並以您的 Google + 帳戶認證登入。</span><span class="sxs-lookup"><span data-stu-id="7fda0-116">Go toohello [Google Developers Console](https://console.developers.google.com/) and sign in with your Google+ account credentials.</span></span>
2.  <span data-ttu-id="7fda0-117">按一下 [建立專案]，輸入 [專案名稱]，接著按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="7fda0-117">Click **Create project**, enter a **Project name**, and then click **Create**.</span></span>

3.  <span data-ttu-id="7fda0-118">按一下 hello**專案功能表**。</span><span class="sxs-lookup"><span data-stu-id="7fda0-118">Click on hello **Projects menu**.</span></span>

    ![Google+ 帳戶 - 選取專案](media/active-directory-b2c-custom-setup-goog-idp/goog-add-new-app1.png)

4.  <span data-ttu-id="7fda0-120">按一下 hello  **+**   按鈕。</span><span class="sxs-lookup"><span data-stu-id="7fda0-120">Click on hello **+** button.</span></span>

    ![Google+ 帳戶 - 建立新的專案](media/active-directory-b2c-custom-setup-goog-idp//goog-add-new-app2.png)

5.  <span data-ttu-id="7fda0-122">輸入 專案名稱，然後按一下建立。</span><span class="sxs-lookup"><span data-stu-id="7fda0-122">Enter a **Project name**, and then click **Create**.</span></span>

    ![Google+ 帳戶 - 新增專案](media/active-directory-b2c-custom-setup-goog-idp//goog-app-name.png)

6.  <span data-ttu-id="7fda0-124">等候 hello 專案已就緒，然後按一下 hello**專案功能表**。</span><span class="sxs-lookup"><span data-stu-id="7fda0-124">Wait until hello project is ready and click on hello **Projects menu**.</span></span>

    ![Google + 帳戶-等候新的專案準備好 toouse](media/active-directory-b2c-custom-setup-goog-idp//goog-select-app1.png)

7.  <span data-ttu-id="7fda0-126">按一下專案名稱。</span><span class="sxs-lookup"><span data-stu-id="7fda0-126">Click on your project name.</span></span>

    ![Google + 帳戶-選取 hello 新專案](media/active-directory-b2c-custom-setup-goog-idp//goog-select-app2.png)

8.  <span data-ttu-id="7fda0-128">按一下**API Manager** ，然後按一下**認證**在 hello 左瀏覽。</span><span class="sxs-lookup"><span data-stu-id="7fda0-128">Click **API Manager** and then click **Credentials** in hello left navigation.</span></span>
9.  <span data-ttu-id="7fda0-129">按一下 hello **OAuth 同意畫面**hello 頂端的索引標籤。</span><span class="sxs-lookup"><span data-stu-id="7fda0-129">Click hello **OAuth consent screen** tab at hello top.</span></span>

    ![Google+ 帳戶 - 設定 OAuth 同意畫面](media/active-directory-b2c-custom-setup-goog-idp/goog-add-cred.png)

10.  <span data-ttu-id="7fda0-131">選取或指定有效的**電子郵件地址**、提供**產品名稱**，然後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="7fda0-131">Select or specify a valid **Email address**, provide a **Product name**, and click **Save**.</span></span>

    ![Google+ - 應用程式認證](media/active-directory-b2c-custom-setup-goog-idp/goog-consent-screen.png)

11.  <span data-ttu-id="7fda0-133">按一下 [新增認證]，然後選擇 [OAuth 用戶端識別碼]。</span><span class="sxs-lookup"><span data-stu-id="7fda0-133">Click **New credentials** and then choose **OAuth client ID**.</span></span>

    ![Google+ - 建立新的應用程式認證](media/active-directory-b2c-custom-setup-goog-idp/goog-add-oauth2-client-id.png)

12.  <span data-ttu-id="7fda0-135">在 [應用程式類型] 下方，選取 [Web 應用程式]。</span><span class="sxs-lookup"><span data-stu-id="7fda0-135">Under **Application type**, select **Web application**.</span></span>

    ![Google+ - 選取應用程式類型](media/active-directory-b2c-custom-setup-goog-idp/goog-web-app.png)

13.  <span data-ttu-id="7fda0-137">提供**名稱**針對您的應用程式中，輸入`https://login.microsoftonline.com`在 hello**授權 JavaScript origins**欄位，和`https://login.microsoftonline.com/te/{tenant}/oauth2/authresp`在 hello**授權重新導向 Uri**欄位。</span><span class="sxs-lookup"><span data-stu-id="7fda0-137">Provide a **Name** for your application, enter `https://login.microsoftonline.com` in hello **Authorized JavaScript origins** field, and `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in hello **Authorized redirect URIs** field.</span></span> <span data-ttu-id="7fda0-138">使用您的租用戶名稱 (例如 contosob2c.onmicrosoft.com) 來取代 **{tenant}**。</span><span class="sxs-lookup"><span data-stu-id="7fda0-138">Replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span> <span data-ttu-id="7fda0-139">hello **{tenant}**值會區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="7fda0-139">hello **{tenant}** value is case-sensitive.</span></span> <span data-ttu-id="7fda0-140">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="7fda0-140">Click **Create**.</span></span>

    ![Google+ - 提供授權的 JavaScript 來源及重新導向 URI](media/active-directory-b2c-custom-setup-goog-idp/goog-create-client-id.png)

14.  <span data-ttu-id="7fda0-142">複製的 hello 值**用戶端識別碼**和**用戶端密碼**。</span><span class="sxs-lookup"><span data-stu-id="7fda0-142">Copy hello values of **Client Id** and **Client secret**.</span></span> <span data-ttu-id="7fda0-143">您需要這兩個 tooconfigure Google + 身分識別提供者租用戶中。</span><span class="sxs-lookup"><span data-stu-id="7fda0-143">You need both tooconfigure Google+ as an identity provider in your tenant.</span></span> <span data-ttu-id="7fda0-144">**用戶端密碼** 是重要的安全性認證。</span><span class="sxs-lookup"><span data-stu-id="7fda0-144">**Client secret** is an important security credential.</span></span>

    ![Google +-複製 hello 值的用戶端識別碼和用戶端密碼](media/active-directory-b2c-custom-setup-goog-idp/goog-client-secret.png)

## <a name="add-hello-google-account-application-key-tooazure-ad-b2c"></a><span data-ttu-id="7fda0-146">新增 hello Google + 帳戶應用程式金鑰 tooAzure AD B2C</span><span class="sxs-lookup"><span data-stu-id="7fda0-146">Add hello Google+ account application key tooAzure AD B2C</span></span>
<span data-ttu-id="7fda0-147">同盟與 Google + 帳戶會代表 hello 應用程式需要 Google + 帳戶 tootrust Azure AD B2C 用戶端密碼。</span><span class="sxs-lookup"><span data-stu-id="7fda0-147">Federation with Google+ accounts requires a client secret for Google+ account tootrust Azure AD B2C on behalf of hello application.</span></span> <span data-ttu-id="7fda0-148">您需要 toostore Azure AD B2C 租用戶中的您 Google + 應用程式密碼：</span><span class="sxs-lookup"><span data-stu-id="7fda0-148">You need toostore your Google+ application secret in Azure AD B2C tenant:</span></span>  

1.  <span data-ttu-id="7fda0-149">移 tooyour Azure AD B2C 租用戶，然後選取**B2C 設定** > **身分識別體驗架構**</span><span class="sxs-lookup"><span data-stu-id="7fda0-149">Go tooyour Azure AD B2C tenant, and select **B2C Settings** > **Identity Experience Framework**</span></span>
2.  <span data-ttu-id="7fda0-150">選取**原則機碼**tooview hello 金鑰用於您的租用戶。</span><span class="sxs-lookup"><span data-stu-id="7fda0-150">Select **Policy Keys** tooview hello keys available in your tenant.</span></span>
3.  <span data-ttu-id="7fda0-151">按一下 [+新增]。</span><span class="sxs-lookup"><span data-stu-id="7fda0-151">Click **+Add**.</span></span>
4.  <span data-ttu-id="7fda0-152">針對 [選項] 使用 [手動]。</span><span class="sxs-lookup"><span data-stu-id="7fda0-152">For **Options**, use **Manual**.</span></span>
5.  <span data-ttu-id="7fda0-153">針對 [名稱] 使用 `GoogleSecret`。</span><span class="sxs-lookup"><span data-stu-id="7fda0-153">For **Name**, use `GoogleSecret`.</span></span>  
    <span data-ttu-id="7fda0-154">hello 前置詞`B2C_1A_`可能會自動加入。</span><span class="sxs-lookup"><span data-stu-id="7fda0-154">hello prefix `B2C_1A_` might be added automatically.</span></span>
6.  <span data-ttu-id="7fda0-155">在 hello**密碼**方塊中，輸入您的 Microsoft 應用程式密碼，從 https://apps.dev.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="7fda0-155">In hello **Secret** box, enter your Microsoft application secret from https://apps.dev.microsoft.com</span></span>
7.  <span data-ttu-id="7fda0-156">針對 [金鑰使用方法] 使用 [簽章]。</span><span class="sxs-lookup"><span data-stu-id="7fda0-156">For **Key usage**, use **Signature**.</span></span>
8.  <span data-ttu-id="7fda0-157">按一下 [建立] </span><span class="sxs-lookup"><span data-stu-id="7fda0-157">Click **Create**</span></span>
9.  <span data-ttu-id="7fda0-158">確認您已建立 hello 金鑰`B2C_1A_GoogleSecret`。</span><span class="sxs-lookup"><span data-stu-id="7fda0-158">Confirm that you've created hello key `B2C_1A_GoogleSecret`.</span></span>

## <a name="add-a-claims-provider-in-your-extension-policy"></a><span data-ttu-id="7fda0-159">在擴充原則中新增宣告提供者</span><span class="sxs-lookup"><span data-stu-id="7fda0-159">Add a claims provider in your extension policy</span></span>

<span data-ttu-id="7fda0-160">如果您希望使用者 toosign 使用 Google + 帳戶，您會需要 toodefine Google + 帳戶做為宣告提供者。</span><span class="sxs-lookup"><span data-stu-id="7fda0-160">If you want users toosign in by using Google+ account, you need toodefine Google+ account as a claims provider.</span></span> <span data-ttu-id="7fda0-161">換句話說，您需要 toospecify 與 Azure AD B2C 通訊的端點。</span><span class="sxs-lookup"><span data-stu-id="7fda0-161">In other words, you need toospecify an endpoint that Azure AD B2C communicates with.</span></span> <span data-ttu-id="7fda0-162">hello 端點提供一組特定的使用者已驗證的 Azure AD B2C tooverify 所使用的宣告。</span><span class="sxs-lookup"><span data-stu-id="7fda0-162">hello endpoint provides a set of claims that are used by Azure AD B2C tooverify that a specific user has authenticated.</span></span>

<span data-ttu-id="7fda0-163">定義 Google+ 帳戶作為宣告提供者，方法是在擴充原則檔案中新增 `<ClaimsProvider>` 節點：</span><span class="sxs-lookup"><span data-stu-id="7fda0-163">Define Google+ Account as a claims provider, by adding `<ClaimsProvider>` node in your extension policy file:</span></span>

1.  <span data-ttu-id="7fda0-164">從您的工作目錄中開啟 hello 擴充原則檔 (TrustFrameworkExtensions.xml)。</span><span class="sxs-lookup"><span data-stu-id="7fda0-164">Open hello extension policy file (TrustFrameworkExtensions.xml) from your working directory.</span></span> <span data-ttu-id="7fda0-165">如果您需要 XML 編輯器，請[試用 Visual Studio 程式碼](https://code.visualstudio.com/download)，這是一個輕巧的跨平台編輯器。</span><span class="sxs-lookup"><span data-stu-id="7fda0-165">If you need an XML editor, [try Visual Studio Code](https://code.visualstudio.com/download), a lightweight cross-platform editor.</span></span>
2.  <span data-ttu-id="7fda0-166">尋找 hello`<ClaimsProviders>`區段</span><span class="sxs-lookup"><span data-stu-id="7fda0-166">Find hello `<ClaimsProviders>` section</span></span>
3.  <span data-ttu-id="7fda0-167">加入下列 XML 程式碼片段在 hello hello`ClaimsProviders`項目和取代`client_id`與 Google + 帳戶應用程式用戶端識別碼 hello 檔案在儲存之前的值。</span><span class="sxs-lookup"><span data-stu-id="7fda0-167">Add hello following XML snippet under hello `ClaimsProviders` element and replace `client_id` value with your Google+ account application client ID before saving hello file.</span></span>  

```xml
<ClaimsProvider>
    <Domain>google.com</Domain>
    <DisplayName>Google</DisplayName>
    <TechnicalProfiles>
    <TechnicalProfile Id="Google-OAUTH">
        <DisplayName>Google</DisplayName>
        <Protocol Name="OAuth2" />
        <Metadata>
        <Item Key="ProviderName">google</Item>
        <Item Key="authorization_endpoint">https://accounts.google.com/o/oauth2/auth</Item>
        <Item Key="AccessTokenEndpoint">https://accounts.google.com/o/oauth2/token</Item>
        <Item Key="ClaimsEndpoint">https://www.googleapis.com/oauth2/v1/userinfo</Item>
        <Item Key="scope">email</Item>
        <Item Key="HttpBinding">POST</Item>
        <Item Key="UsePolicyInRedirectUri">0</Item>
        <Item Key="client_id">Your Google+ application ID</Item>
        </Metadata>
        <CryptographicKeys>
        <Key Id="client_secret" StorageReferenceId="B2C_1A_GoogleSecret" />
        </CryptographicKeys>
        <OutputClaims>
        <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="id" />
        <OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="email" />
        <OutputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="given_name" />
        <OutputClaim ClaimTypeReferenceId="surname" PartnerClaimType="family_name" />
        <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="name" />
        <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="google.com" />
        <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="socialIdpAuthentication" />
        </OutputClaims>
        <OutputClaimsTransformations>
        <OutputClaimsTransformation ReferenceId="CreateRandomUPNUserName" />
        <OutputClaimsTransformation ReferenceId="CreateUserPrincipalName" />
        <OutputClaimsTransformation ReferenceId="CreateAlternativeSecurityId" />
        <OutputClaimsTransformation ReferenceId="CreateSubjectClaimFromAlternativeSecurityId" />
        </OutputClaimsTransformations>
        <UseTechnicalProfileForSessionManagement ReferenceId="SM-SocialLogin" />
        <ErrorHandlers>
        <ErrorHandler>
            <ErrorResponseFormat>json</ErrorResponseFormat>
            <ResponseMatch>$[?(@@.error == 'invalid_grant')]</ResponseMatch>
            <Action>Reauthenticate</Action>
            <!--In case of authorization code used error, we don't want hello user tooselect his account again.-->
            <!--AdditionalRequestParameters Key="prompt">select_account</AdditionalRequestParameters-->
        </ErrorHandler>
        </ErrorHandlers>
    </TechnicalProfile>
    </TechnicalProfiles>
</ClaimsProvider>
```

## <a name="register-hello-google-account-claims-provider-toosign-up-or-sign-in-user-journey"></a><span data-ttu-id="7fda0-168">註冊 hello Google + 帳戶宣告提供者 tooSign 註冊或登入使用者之旅</span><span class="sxs-lookup"><span data-stu-id="7fda0-168">Register hello Google+ account claims provider tooSign up or Sign in user journey</span></span>

<span data-ttu-id="7fda0-169">已設定 hello 身分識別提供者。</span><span class="sxs-lookup"><span data-stu-id="7fda0-169">hello identity provider has been set up.</span></span>  <span data-ttu-id="7fda0-170">不過，它不是可在任何 hello sign-up/登入畫面。</span><span class="sxs-lookup"><span data-stu-id="7fda0-170">However, it is not available in any of hello sign-up/sign-in screens.</span></span> <span data-ttu-id="7fda0-171">Hello Google + 帳戶身分識別提供者 tooyour 將使用者加入`SignUpOrSignIn`使用者之旅。</span><span class="sxs-lookup"><span data-stu-id="7fda0-171">Add hello Google+ account identity provider tooyour user `SignUpOrSignIn` user journey.</span></span> <span data-ttu-id="7fda0-172">toomake 它可用，我們建立的現有的範本使用者旅程重複。</span><span class="sxs-lookup"><span data-stu-id="7fda0-172">toomake it available, we create a duplicate of an existing template user journey.</span></span>  <span data-ttu-id="7fda0-173">然後我們新增 hello Google + 帳戶身分識別提供者：</span><span class="sxs-lookup"><span data-stu-id="7fda0-173">Then we add hello Google+ account identity provider:</span></span>

>[!NOTE]
>
><span data-ttu-id="7fda0-174">如果您要複製 hello`<UserJourneys>`項目從您的原則 toohello 延伸模組檔案 (TrustFrameworkExtensions.xml) 的基底的檔案，您可以略過 toothis > 一節。</span><span class="sxs-lookup"><span data-stu-id="7fda0-174">If you copied hello `<UserJourneys>` element from base file of your policy toohello extension file (TrustFrameworkExtensions.xml), you can skip toothis section.</span></span>

1.  <span data-ttu-id="7fda0-175">開啟 hello 原則 (例如，TrustFrameworkBase.xml) 的基底的檔案。</span><span class="sxs-lookup"><span data-stu-id="7fda0-175">Open hello base file of your policy (for example, TrustFrameworkBase.xml).</span></span>
2.  <span data-ttu-id="7fda0-176">尋找 hello`<UserJourneys>`項目，並複製 hello 整個內容`<UserJourneys>`節點。</span><span class="sxs-lookup"><span data-stu-id="7fda0-176">Find hello `<UserJourneys>` element and copy hello entire content of `<UserJourneys>` node.</span></span>
3.  <span data-ttu-id="7fda0-177">開啟 hello 延伸模組檔案 (例如，TrustFrameworkExtensions.xml)，並尋找 hello`<UserJourneys>`項目。</span><span class="sxs-lookup"><span data-stu-id="7fda0-177">Open hello extension file (for example, TrustFrameworkExtensions.xml) and find hello `<UserJourneys>` element.</span></span> <span data-ttu-id="7fda0-178">如果 hello 項目不存在，請加入一個參考。</span><span class="sxs-lookup"><span data-stu-id="7fda0-178">If hello element doesn't exist, add one.</span></span>
4.  <span data-ttu-id="7fda0-179">貼上 hello 整個內容`<UserJournesy>`您複製 hello 的子系的節點`<UserJourneys>`項目。</span><span class="sxs-lookup"><span data-stu-id="7fda0-179">Paste hello entire content of `<UserJournesy>` node that you copied as a child of hello `<UserJourneys>` element.</span></span>

### <a name="display-hello-button"></a><span data-ttu-id="7fda0-180">顯示 hello 按鈕</span><span class="sxs-lookup"><span data-stu-id="7fda0-180">Display hello button</span></span>
<span data-ttu-id="7fda0-181">hello`<ClaimsProviderSelections>`項目會定義 hello 宣告提供者選擇的選項清單以及它們的順序。</span><span class="sxs-lookup"><span data-stu-id="7fda0-181">hello `<ClaimsProviderSelections>` element defines hello list of claims provider selection options and their order.</span></span>  <span data-ttu-id="7fda0-182">`<ClaimsProviderSelection>`項目是 sign-up/登入頁面上的類似 tooan 身分識別提供者按鈕。</span><span class="sxs-lookup"><span data-stu-id="7fda0-182">`<ClaimsProviderSelection>` element is analogous tooan identity provider button on a sign-up/sign-in page.</span></span> <span data-ttu-id="7fda0-183">如果您將加入`<ClaimsProviderSelection>`Google + 帳戶項目，新的按鈕顯示落在 hello 頁面上的使用者。</span><span class="sxs-lookup"><span data-stu-id="7fda0-183">If you add a `<ClaimsProviderSelection>` element for Google+ account, a new button shows up when a user lands on hello page.</span></span> <span data-ttu-id="7fda0-184">tooadd 這個項目：</span><span class="sxs-lookup"><span data-stu-id="7fda0-184">tooadd this element:</span></span>

1.  <span data-ttu-id="7fda0-185">尋找 hello`<UserJourney>`節點包含`Id="SignUpOrSignIn"`hello 您複製的使用者歷程中。</span><span class="sxs-lookup"><span data-stu-id="7fda0-185">Find hello `<UserJourney>` node that includes `Id="SignUpOrSignIn"` in hello user journey that you copied.</span></span>
2.  <span data-ttu-id="7fda0-186">找出 hello`<OrchestrationStep>`包含的節點`Order="1"`</span><span class="sxs-lookup"><span data-stu-id="7fda0-186">Locate hello `<OrchestrationStep>` node that includes `Order="1"`</span></span>
3.  <span data-ttu-id="7fda0-187">在 `<ClaimsProviderSelections>` 節點下，新增下列 XML 程式碼片段：</span><span class="sxs-lookup"><span data-stu-id="7fda0-187">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="GoogleExchange" />
```

### <a name="link-hello-button-tooan-action"></a><span data-ttu-id="7fda0-188">連結 hello 按鈕 tooan 動作</span><span class="sxs-lookup"><span data-stu-id="7fda0-188">Link hello button tooan action</span></span>
<span data-ttu-id="7fda0-189">既然您已備妥 按鈕，您需要 toolink 它 tooan 動作。</span><span class="sxs-lookup"><span data-stu-id="7fda0-189">Now that you have a button in place, you need toolink it tooan action.</span></span> <span data-ttu-id="7fda0-190">hello 動作，在此情況下，為 Azure AD B2C toocommunicate 與 Google + 帳戶 tooreceive 語彙基元。</span><span class="sxs-lookup"><span data-stu-id="7fda0-190">hello action, in this case, is for Azure AD B2C toocommunicate with Google+ account tooreceive a token.</span></span>

1.  <span data-ttu-id="7fda0-191">尋找 hello`<OrchestrationStep>`包含`Order="2"`在 hello`<UserJourney>`節點。</span><span class="sxs-lookup"><span data-stu-id="7fda0-191">Find hello `<OrchestrationStep>` that includes `Order="2"` in hello `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="7fda0-192">在 `<ClaimsExchanges>` 節點下，新增下列 XML 程式碼片段：</span><span class="sxs-lookup"><span data-stu-id="7fda0-192">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="GoogleExchange" TechnicalProfileReferenceId="Google-OAUTH" />
```

>[!NOTE]
>
> * <span data-ttu-id="7fda0-193">請確定 hello`Id`具有相同的值為 hello `TargetClaimsExchangeId` hello 前面一節中</span><span class="sxs-lookup"><span data-stu-id="7fda0-193">Ensure hello `Id` has hello same value as that of `TargetClaimsExchangeId` in hello preceding section</span></span>
> * <span data-ttu-id="7fda0-194">請確定`TechnicalProfileReferenceId`設定您建立舊版 (Google-OAUTH) toohello 技術設定檔的識別碼。</span><span class="sxs-lookup"><span data-stu-id="7fda0-194">Ensure `TechnicalProfileReferenceId` ID is set toohello technical profile you created earlier (Google-OAUTH).</span></span>

## <a name="upload-hello-policy-tooyour-tenant"></a><span data-ttu-id="7fda0-195">上傳 hello 原則 tooyour 租用戶</span><span class="sxs-lookup"><span data-stu-id="7fda0-195">Upload hello policy tooyour tenant</span></span>
1.  <span data-ttu-id="7fda0-196">在 hello [Azure 入口網站](https://portal.azure.com)，切換至 hello[內容，您的 Azure AD B2C 租用戶](active-directory-b2c-navigate-to-b2c-context.md)，並開啟 hello **Azure AD B2C**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="7fda0-196">In hello [Azure portal](https://portal.azure.com), switch into hello [context of your Azure AD B2C tenant](active-directory-b2c-navigate-to-b2c-context.md), and open hello **Azure AD B2C** blade.</span></span>
2.  <span data-ttu-id="7fda0-197">選取 [識別體驗架構]。</span><span class="sxs-lookup"><span data-stu-id="7fda0-197">Select **Identity Experience Framework**.</span></span>
3.  <span data-ttu-id="7fda0-198">開啟 hello**所有原則**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="7fda0-198">Open hello **All Policies** blade.</span></span>
4.  <span data-ttu-id="7fda0-199">選取 [上傳原則]。</span><span class="sxs-lookup"><span data-stu-id="7fda0-199">Select **Upload Policy**.</span></span>
5.  <span data-ttu-id="7fda0-200">請檢查**如果存在的話，請覆寫 hello 原則**方塊。</span><span class="sxs-lookup"><span data-stu-id="7fda0-200">Check **Overwrite hello policy if it exists** box.</span></span>
6.  <span data-ttu-id="7fda0-201">**上傳**TrustFrameworkExtensions.xml，並確定它不會通過 hello 驗證</span><span class="sxs-lookup"><span data-stu-id="7fda0-201">**Upload** TrustFrameworkExtensions.xml and ensure that it does not fail hello validation</span></span>

## <a name="test-hello-custom-policy-by-using-run-now"></a><span data-ttu-id="7fda0-202">使用 立即執行測試 hello 自訂原則</span><span class="sxs-lookup"><span data-stu-id="7fda0-202">Test hello custom policy by using Run Now</span></span>
1.  <span data-ttu-id="7fda0-203">開啟**Azure AD B2C 設定**並移過**身分識別體驗架構**。</span><span class="sxs-lookup"><span data-stu-id="7fda0-203">Open **Azure AD B2C Settings** and go too**Identity Experience Framework**.</span></span>

    >[!NOTE]
    >
    >    <span data-ttu-id="7fda0-204">**現在就執行**需要至少一個應用程式 toobe 預先 hello 租用戶上。</span><span class="sxs-lookup"><span data-stu-id="7fda0-204">**Run now** requires at least one application toobe preregistered on hello tenant.</span></span> 
    >    <span data-ttu-id="7fda0-205">如何 tooregister 應用程式，請參閱的 toolearn hello Azure AD B2C[開始](active-directory-b2c-get-started.md)文章或 hello[應用程式註冊](active-directory-b2c-app-registration.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="7fda0-205">toolearn how tooregister applications, see hello Azure AD B2C [Get started](active-directory-b2c-get-started.md) article or hello [Application registration](active-directory-b2c-app-registration.md) article.</span></span>


2.  <span data-ttu-id="7fda0-206">開啟**B2C_1A_signup_signin**，hello 上載的信賴憑證者 (rp) 自訂原則。</span><span class="sxs-lookup"><span data-stu-id="7fda0-206">Open **B2C_1A_signup_signin**, hello relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="7fda0-207">選取 [立即執行]。</span><span class="sxs-lookup"><span data-stu-id="7fda0-207">Select **Run now**.</span></span>
3.  <span data-ttu-id="7fda0-208">您應該能夠使用 Google + 帳戶 toosign。</span><span class="sxs-lookup"><span data-stu-id="7fda0-208">You should be able toosign in using Google+ account.</span></span>

## <a name="optional-register-hello-google-account-claims-provider-tooprofile-edit-user-journey"></a><span data-ttu-id="7fda0-209">[選用]註冊 hello Google + 帳戶宣告提供者 tooProfile 編輯使用者旅程</span><span class="sxs-lookup"><span data-stu-id="7fda0-209">[Optional] Register hello Google+ account claims provider tooProfile-Edit user journey</span></span>
<span data-ttu-id="7fda0-210">您可能會想 tooadd hello Google + 帳戶身分識別提供者也 tooyour 使用者`ProfileEdit`使用者之旅。</span><span class="sxs-lookup"><span data-stu-id="7fda0-210">You may want tooadd hello Google+ account identity provider also tooyour user `ProfileEdit` user journey.</span></span> <span data-ttu-id="7fda0-211">toomake 提供，我們可以重覆 hello 最後的兩個步驟：</span><span class="sxs-lookup"><span data-stu-id="7fda0-211">toomake it available, we repeat hello last two steps:</span></span>

### <a name="display-hello-button"></a><span data-ttu-id="7fda0-212">顯示 hello 按鈕</span><span class="sxs-lookup"><span data-stu-id="7fda0-212">Display hello button</span></span>
1.  <span data-ttu-id="7fda0-213">開啟 hello 原則 (例如，TrustFrameworkExtensions.xml) 的延伸模組檔案。</span><span class="sxs-lookup"><span data-stu-id="7fda0-213">Open hello extension file of your policy (for example, TrustFrameworkExtensions.xml).</span></span>
2.  <span data-ttu-id="7fda0-214">尋找 hello`<UserJourney>`節點包含`Id="ProfileEdit"`hello 您複製的使用者歷程中。</span><span class="sxs-lookup"><span data-stu-id="7fda0-214">Find hello `<UserJourney>` node that includes `Id="ProfileEdit"` in hello user journey that you copied.</span></span>
3.  <span data-ttu-id="7fda0-215">找出 hello`<OrchestrationStep>`包含的節點`Order="1"`</span><span class="sxs-lookup"><span data-stu-id="7fda0-215">Locate hello `<OrchestrationStep>` node that includes `Order="1"`</span></span>
4.  <span data-ttu-id="7fda0-216">在 `<ClaimsProviderSelections>` 節點下，新增下列 XML 程式碼片段：</span><span class="sxs-lookup"><span data-stu-id="7fda0-216">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="GoogleExchange" />
```

### <a name="link-hello-button-tooan-action"></a><span data-ttu-id="7fda0-217">連結 hello 按鈕 tooan 動作</span><span class="sxs-lookup"><span data-stu-id="7fda0-217">Link hello button tooan action</span></span>
1.  <span data-ttu-id="7fda0-218">尋找 hello`<OrchestrationStep>`包含`Order="2"`在 hello`<UserJourney>`節點。</span><span class="sxs-lookup"><span data-stu-id="7fda0-218">Find hello `<OrchestrationStep>` that includes `Order="2"` in hello `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="7fda0-219">在 `<ClaimsExchanges>` 節點下，新增下列 XML 程式碼片段：</span><span class="sxs-lookup"><span data-stu-id="7fda0-219">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="GoogleExchange" TechnicalProfileReferenceId="Google-OAUTH" />
```

### <a name="test-hello-custom-profile-edit-policy-by-using-run-now"></a><span data-ttu-id="7fda0-220">使用 立即執行測試 hello 自訂設定檔編輯原則</span><span class="sxs-lookup"><span data-stu-id="7fda0-220">Test hello custom Profile-Edit policy by using Run Now</span></span>

1.  <span data-ttu-id="7fda0-221">開啟**Azure AD B2C 設定**並移過**身分識別體驗架構**。</span><span class="sxs-lookup"><span data-stu-id="7fda0-221">Open **Azure AD B2C Settings** and go too**Identity Experience Framework**.</span></span>
2.  <span data-ttu-id="7fda0-222">開啟**B2C_1A_ProfileEdit**，hello 上載的信賴憑證者 (rp) 自訂原則。</span><span class="sxs-lookup"><span data-stu-id="7fda0-222">Open **B2C_1A_ProfileEdit**, hello relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="7fda0-223">選取 [立即執行]。</span><span class="sxs-lookup"><span data-stu-id="7fda0-223">Select **Run now**.</span></span>
3.  <span data-ttu-id="7fda0-224">您應該能夠使用 Google + 帳戶 toosign。</span><span class="sxs-lookup"><span data-stu-id="7fda0-224">You should be able toosign in using Google+ account.</span></span>

## <a name="download-hello-complete-policy-files"></a><span data-ttu-id="7fda0-225">下載 hello 完整的原則檔案</span><span class="sxs-lookup"><span data-stu-id="7fda0-225">Download hello complete policy files</span></span>
<span data-ttu-id="7fda0-226">選擇性： 我們建議您建置您使用您自己的自訂原則檔完成的 hello 開始使用自訂原則逐步執行，而不是使用這些範例檔案之後的案例。</span><span class="sxs-lookup"><span data-stu-id="7fda0-226">Optional: We recommend you build your scenario using your own Custom policy files after completing hello Getting Started with Custom Policies walk through instead of using these sample files.</span></span>  [<span data-ttu-id="7fda0-227">參考的範例原則檔案</span><span class="sxs-lookup"><span data-stu-id="7fda0-227">Sample policy files for reference</span></span>](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-setup-goog-app)
