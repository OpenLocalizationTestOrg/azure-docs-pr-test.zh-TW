---
title: "Azure Active Directory B2C︰使用自訂原則新增 Microsoft 帳戶 (MSA) 作為識別提供者"
description: "透過 OpenID 連線 (OIDC) 通訊協定使用 Microsoft 作為識別提供者的範例"
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
ms.openlocfilehash: 577ac612f69015e6790f2fa9f2cfb42c2b524b55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-add-microsoft-account-msa-as-an-identity-provider-using-custom-policies"></a><span data-ttu-id="700db-103">Azure Active Directory B2C︰使用自訂原則新增 Microsoft 帳戶 (MSA) 作為識別提供者</span><span class="sxs-lookup"><span data-stu-id="700db-103">Azure Active Directory B2C: Add Microsoft Account (MSA) as an identity provider using custom policies</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="700db-104">本文章將示範如何 tooenable 登入的使用者，從 Microsoft 帳戶 (MSA) 藉由使用 hello[自訂原則](active-directory-b2c-overview-custom.md)。</span><span class="sxs-lookup"><span data-stu-id="700db-104">This article shows you how tooenable sign-in for users from Microsoft account (MSA) through hello use of [custom policies](active-directory-b2c-overview-custom.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="700db-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="700db-105">Prerequisites</span></span>
<span data-ttu-id="700db-106">完整的 hello 步驟 hello[開始使用自訂原則](active-directory-b2c-get-started-custom.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="700db-106">Complete hello steps in hello [Getting started with custom policies](active-directory-b2c-get-started-custom.md) article.</span></span>

<span data-ttu-id="700db-107">這些步驟包括：</span><span class="sxs-lookup"><span data-stu-id="700db-107">These steps include:</span></span>

1.  <span data-ttu-id="700db-108">建立 Microsoft 帳戶應用程式。</span><span class="sxs-lookup"><span data-stu-id="700db-108">Creating a Microsoft account application.</span></span>
2.  <span data-ttu-id="700db-109">加入 hello Microsoft 帳戶應用程式金鑰 tooAzure AD B2C</span><span class="sxs-lookup"><span data-stu-id="700db-109">Adding hello Microsoft account application key tooAzure AD B2C</span></span>
3.  <span data-ttu-id="700db-110">新增宣告提供者 tooa 原則</span><span class="sxs-lookup"><span data-stu-id="700db-110">Adding claims provider tooa policy</span></span>
4.  <span data-ttu-id="700db-111">註冊 hello Microsoft 帳戶宣告提供者 tooa 使用者旅程</span><span class="sxs-lookup"><span data-stu-id="700db-111">Registering hello Microsoft Account claims provider tooa user journey</span></span>
5.  <span data-ttu-id="700db-112">上傳 hello 原則 tooan Azure AD B2C 租用戶，並進行測試</span><span class="sxs-lookup"><span data-stu-id="700db-112">Uploading hello policy tooan Azure AD B2C tenant and test it</span></span>

## <a name="create-a-microsoft-account-application"></a><span data-ttu-id="700db-113">建立 Microsoft 帳戶應用程式</span><span class="sxs-lookup"><span data-stu-id="700db-113">Create a Microsoft account application</span></span>
<span data-ttu-id="700db-114">身分識別提供者，在 Azure Active Directory (Azure AD) B2C 的 toouse Microsoft 帳戶，您需要 toocreate Microsoft 帳戶應用程式，並提供與 hello 正確的參數。</span><span class="sxs-lookup"><span data-stu-id="700db-114">toouse Microsoft account as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a Microsoft account application and supply it with hello right parameters.</span></span> <span data-ttu-id="700db-115">您需要 Microsoft 帳戶。</span><span class="sxs-lookup"><span data-stu-id="700db-115">You need a Microsoft account.</span></span> <span data-ttu-id="700db-116">如果您沒有該帳戶，請瀏覽 [https://www.live.com/](https://www.live.com/)。</span><span class="sxs-lookup"><span data-stu-id="700db-116">If you don’t have one, visit [https://www.live.com/](https://www.live.com/).</span></span>

1.  <span data-ttu-id="700db-117">移 toohello [Microsoft 應用程式註冊入口網站](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)並以您的 Microsoft 帳戶認證登入。</span><span class="sxs-lookup"><span data-stu-id="700db-117">Go toohello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) and sign in with your Microsoft account credentials.</span></span>
2.  <span data-ttu-id="700db-118">按一下 [新增應用程式] 。</span><span class="sxs-lookup"><span data-stu-id="700db-118">Click **Add an app**.</span></span>

    ![Microsoft 帳戶 - 新增應用程式](media/active-directory-b2c-custom-setup-ms-account-idp/msa-add-new-app.png)

3.  <span data-ttu-id="700db-120">提供應用程式的 [名稱]、[連絡人電子郵件]、取消核取 [讓我們幫助您開始]，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="700db-120">Provide a **Name** for your application, **Contact email**, uncheck **Let us help you get started** and click **Create**.</span></span>

    ![Microsoft 帳戶 - 註冊您的應用程式](media/active-directory-b2c-custom-setup-ms-account-idp/msa-app-name.png)

4.  <span data-ttu-id="700db-122">複製 hello 值**應用程式識別碼**。您需要它 tooconfigure Microsoft 帳戶做為身分識別提供者租用戶中。</span><span class="sxs-lookup"><span data-stu-id="700db-122">Copy hello value of **Application Id**. You need it tooconfigure Microsoft account as an identity provider in your tenant.</span></span>

    ![Microsoft 帳戶-應用程式識別碼的值複製 hello](media/active-directory-b2c-custom-setup-ms-account-idp/msa-app-id.png)

5.  <span data-ttu-id="700db-124">按一下 [新增平台]</span><span class="sxs-lookup"><span data-stu-id="700db-124">Click on **Add platform**</span></span>

    ![Microsoft 帳戶 - 新增平台](media/active-directory-b2c-custom-setup-ms-account-idp/msa-add-platform.png)

6.  <span data-ttu-id="700db-126">從 hello 平台清單中選擇**Web**。</span><span class="sxs-lookup"><span data-stu-id="700db-126">From hello platform list, choose **Web**.</span></span>

    ![Microsoft 帳戶-hello 平台清單中選擇 Web](media/active-directory-b2c-custom-setup-ms-account-idp/msa-web.png)

7.  <span data-ttu-id="700db-128">輸入`https://login.microsoftonline.com/te/{tenant}/oauth2/authresp`在 hello**重新導向 Uri**欄位。</span><span class="sxs-lookup"><span data-stu-id="700db-128">Enter `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in hello **Redirect URIs** field.</span></span> <span data-ttu-id="700db-129">使用您的租用戶名稱 (例如 contosob2c.onmicrosoft.com) 來取代 **{tenant}**。</span><span class="sxs-lookup"><span data-stu-id="700db-129">Replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span>

    ![Microsoft 帳戶 - 設定重新導向 URL](media/active-directory-b2c-custom-setup-ms-account-idp/msa-redirect-url.png)

8.  <span data-ttu-id="700db-131">按一下**產生新的密碼**下 hello**應用程式密碼**> 一節。</span><span class="sxs-lookup"><span data-stu-id="700db-131">Click on **Generate New Password** under hello **Application Secrets** section.</span></span> <span data-ttu-id="700db-132">複製顯示在螢幕上的 hello 新密碼。</span><span class="sxs-lookup"><span data-stu-id="700db-132">Copy hello new password displayed on screen.</span></span> <span data-ttu-id="700db-133">您需要它 tooconfigure Microsoft 帳戶做為身分識別提供者租用戶中。</span><span class="sxs-lookup"><span data-stu-id="700db-133">You need it tooconfigure Microsoft account as an identity provider in your tenant.</span></span> <span data-ttu-id="700db-134">此密碼是重要的安全性認證。</span><span class="sxs-lookup"><span data-stu-id="700db-134">This password is an important security credential.</span></span>

    ![Microsoft 帳戶 - 產生新密碼](media/active-directory-b2c-custom-setup-ms-account-idp/msa-generate-new-password.png)

    ![Microsoft 帳戶-複製 hello 新密碼](media/active-directory-b2c-custom-setup-ms-account-idp/msa-new-password.png)

9.  <span data-ttu-id="700db-137">指出核取 hello 方塊**Live SDK 支援**下 hello**進階選項**> 一節。</span><span class="sxs-lookup"><span data-stu-id="700db-137">Check hello box that says **Live SDK support** under hello **Advanced Options** section.</span></span> <span data-ttu-id="700db-138">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="700db-138">Click **Save**.</span></span>

    ![Microsoft 帳戶 - Live SDK 支援](media/active-directory-b2c-custom-setup-ms-account-idp/msa-live-sdk-support.png)

## <a name="add-hello-microsoft-account-application-key-tooazure-ad-b2c"></a><span data-ttu-id="700db-140">新增 hello Microsoft 帳戶應用程式金鑰 tooAzure AD B2C</span><span class="sxs-lookup"><span data-stu-id="700db-140">Add hello Microsoft account application key tooAzure AD B2C</span></span>
<span data-ttu-id="700db-141">使用 Microsoft 帳戶的同盟需要 Microsoft 帳戶 tootrust Azure AD B2C 代表 hello 應用程式用戶端密碼。</span><span class="sxs-lookup"><span data-stu-id="700db-141">Federation with Microsoft accounts requires a client secret for Microsoft account tootrust Azure AD B2C on behalf of hello application.</span></span> <span data-ttu-id="700db-142">Azure AD B2C 租用戶中的您 Microsoft 帳戶應用程式 secert 需要 toostore:</span><span class="sxs-lookup"><span data-stu-id="700db-142">You need toostore your Microsoft account application secert in Azure AD B2C tenant:</span></span>   

1.  <span data-ttu-id="700db-143">移 tooyour Azure AD B2C 租用戶，然後選取**B2C 設定** > **身分識別體驗架構**</span><span class="sxs-lookup"><span data-stu-id="700db-143">Go tooyour Azure AD B2C tenant, and select **B2C Settings** > **Identity Experience Framework**</span></span>
2.  <span data-ttu-id="700db-144">選取**原則機碼**tooview hello 金鑰用於您的租用戶。</span><span class="sxs-lookup"><span data-stu-id="700db-144">Select **Policy Keys** tooview hello keys available in your tenant.</span></span>
3.  <span data-ttu-id="700db-145">按一下 [+新增]。</span><span class="sxs-lookup"><span data-stu-id="700db-145">Click **+Add**.</span></span>
4.  <span data-ttu-id="700db-146">針對 [選項] 使用 [手動]。</span><span class="sxs-lookup"><span data-stu-id="700db-146">For **Options**, use **Manual**.</span></span>
5.  <span data-ttu-id="700db-147">針對 [名稱] 使用 `MSASecret`。</span><span class="sxs-lookup"><span data-stu-id="700db-147">For **Name**, use `MSASecret`.</span></span>  
    <span data-ttu-id="700db-148">hello 前置詞`B2C_1A_`可能會自動加入。</span><span class="sxs-lookup"><span data-stu-id="700db-148">hello prefix `B2C_1A_` might be added automatically.</span></span>
6.  <span data-ttu-id="700db-149">在 hello**密碼**方塊中，輸入您的 Microsoft 應用程式密碼，從 https://apps.dev.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="700db-149">In hello **Secret** box, enter your Microsoft application secret from https://apps.dev.microsoft.com</span></span>
7.  <span data-ttu-id="700db-150">針對 [金鑰使用方法] 使用 [簽章]。</span><span class="sxs-lookup"><span data-stu-id="700db-150">For **Key usage**, use **Signature**.</span></span>
8.  <span data-ttu-id="700db-151">按一下 [建立] </span><span class="sxs-lookup"><span data-stu-id="700db-151">Click **Create**</span></span>
9.  <span data-ttu-id="700db-152">確認您已建立 hello 金鑰`B2C_1A_MSASecret`。</span><span class="sxs-lookup"><span data-stu-id="700db-152">Confirm that you've created hello key `B2C_1A_MSASecret`.</span></span>

## <a name="add-a-claims-provider-in-your-extension-policy"></a><span data-ttu-id="700db-153">在擴充原則中新增宣告提供者</span><span class="sxs-lookup"><span data-stu-id="700db-153">Add a claims provider in your extension policy</span></span>
<span data-ttu-id="700db-154">如果您希望使用者 toosign 使用 Microsoft 帳戶，您會需要的宣告提供者 toodefine Microsoft 帳戶。</span><span class="sxs-lookup"><span data-stu-id="700db-154">If you want users toosign in by using Microsoft Account, you need toodefine Microsoft Account as a claims provider.</span></span> <span data-ttu-id="700db-155">換句話說，您需要 toospecify 與 Azure AD B2C 通訊的端點。</span><span class="sxs-lookup"><span data-stu-id="700db-155">In other words, you need toospecify an endpoint that Azure AD B2C communicates with.</span></span> <span data-ttu-id="700db-156">hello 端點提供一組特定的使用者已驗證的 Azure AD B2C tooverify 所使用的宣告。</span><span class="sxs-lookup"><span data-stu-id="700db-156">hello endpoint provides a set of claims that are used by Azure AD B2C tooverify that a specific user has authenticated.</span></span>

<span data-ttu-id="700db-157">定義 Microsoft 帳戶作為宣告提供者，方法是在擴充原則檔案中新增 `<ClaimsProvider>` 節點：</span><span class="sxs-lookup"><span data-stu-id="700db-157">Define Microsoft Account as a claims provider, by adding `<ClaimsProvider>` node in your extension policy file:</span></span>

1.  <span data-ttu-id="700db-158">從您的工作目錄中開啟 hello 擴充原則檔 (TrustFrameworkExtensions.xml)。</span><span class="sxs-lookup"><span data-stu-id="700db-158">Open hello extension policy file (TrustFrameworkExtensions.xml) from your working directory.</span></span> <span data-ttu-id="700db-159">如果您需要 XML 編輯器，請[試用 Visual Studio 程式碼](https://code.visualstudio.com/download)，這是一個輕巧的跨平台編輯器。</span><span class="sxs-lookup"><span data-stu-id="700db-159">If you need an XML editor, [try Visual Studio Code](https://code.visualstudio.com/download), a lightweight cross-platform editor.</span></span>
2.  <span data-ttu-id="700db-160">尋找 hello`<ClaimsProviders>`區段</span><span class="sxs-lookup"><span data-stu-id="700db-160">Find hello `<ClaimsProviders>` section</span></span>
3.  <span data-ttu-id="700db-161">加入下列 XML 程式碼片段在 hello`ClaimsProviders`項目：</span><span class="sxs-lookup"><span data-stu-id="700db-161">Add following XML snippet under hello `ClaimsProviders` element:</span></span>

    ```xml
<ClaimsProvider>
    <Domain>live.com</Domain>
    <DisplayName>Microsoft Account</DisplayName>
    <TechnicalProfiles>
    <TechnicalProfile Id="MSA-OIDC">
        <DisplayName>Microsoft Account</DisplayName>
        <Protocol Name="OpenIdConnect" />
        <Metadata>
        <Item Key="ProviderName">https://login.live.com</Item>
        <Item Key="METADATA">https://login.live.com/.well-known/openid-configuration</Item>
        <Item Key="response_types">code</Item>
        <Item Key="response_mode">form_post</Item>
        <Item Key="scope">openid profile email</Item>
        <Item Key="HttpBinding">POST</Item>
        <Item Key="UsePolicyInRedirectUri">0</Item>
        <Item Key="client_id">Your Microsoft application client id</Item>
        </Metadata>
    <CryptographicKeys>
        <Key Id="client_secret" StorageReferenceId="B2C_1A_MSASecret" />
    </CryptographicKeys>
    <OutputClaims>
        <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="live.com" />
        <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="socialIdpAuthentication" />
        <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="sub" />
        <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="name" />
        <OutputClaim ClaimTypeReferenceId="email" />
        </OutputClaims>
        <OutputClaimsTransformations>
        <OutputClaimsTransformation ReferenceId="CreateRandomUPNUserName" />
        <OutputClaimsTransformation ReferenceId="CreateUserPrincipalName" />
        <OutputClaimsTransformation ReferenceId="CreateAlternativeSecurityId" />
        <OutputClaimsTransformation ReferenceId="CreateSubjectClaimFromAlternativeSecurityId" />
        </OutputClaimsTransformations>
        <UseTechnicalProfileForSessionManagement ReferenceId="SM-SocialLogin" />
    </TechnicalProfile>
    </TechnicalProfiles>
</ClaimsProvider>
```

4.  <span data-ttu-id="700db-162">使用您的 Microsoft 帳戶應用程式用戶端識別碼來取代 `client_id` 值</span><span class="sxs-lookup"><span data-stu-id="700db-162">Replace `client_id` value with your Microsoft Account application client Id</span></span>

5.  <span data-ttu-id="700db-163">儲存 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="700db-163">Save hello file.</span></span>

## <a name="register-hello-microsoft-account-claims-provider-toosign-up-or-sign-in-user-journey"></a><span data-ttu-id="700db-164">註冊 hello Microsoft 帳戶宣告提供者 tooSign 註冊或登入使用者之旅</span><span class="sxs-lookup"><span data-stu-id="700db-164">Register hello Microsoft Account claims provider tooSign up or Sign-in user journey</span></span>

<span data-ttu-id="700db-165">此時，hello 身分識別提供者已設定，但不是可在任何 hello sign-up/登入畫面。</span><span class="sxs-lookup"><span data-stu-id="700db-165">At this point, hello identity provider has been set up, but it’s not available in any of hello sign-up/sign-in screens.</span></span> <span data-ttu-id="700db-166">現在您需要 tooadd hello Microsoft 帳戶身分識別提供者 tooyour 使用者`SignUpOrSignIn`使用者之旅。</span><span class="sxs-lookup"><span data-stu-id="700db-166">Now you need tooadd hello Microsoft Account identity provider tooyour user `SignUpOrSignIn` user journey.</span></span> <span data-ttu-id="700db-167">toomake 它可用，我們建立的現有的範本使用者旅程重複。</span><span class="sxs-lookup"><span data-stu-id="700db-167">toomake it available, we create a duplicate of an existing template user journey.</span></span>  <span data-ttu-id="700db-168">然後我們會加入 hello Microsoft 帳戶的身分識別提供者：</span><span class="sxs-lookup"><span data-stu-id="700db-168">Then we add hello Microsoft Account identity provider:</span></span>

> [!NOTE]
>
><span data-ttu-id="700db-169">如果您先前複製 hello`<UserJourneys>`基底檔案的原則 toohello 延伸模組檔案中的項目`TrustFrameworkExtensions.xml`，您可以略過 toothis > 一節。</span><span class="sxs-lookup"><span data-stu-id="700db-169">If you previously copied hello `<UserJourneys>` element from base file of your policy toohello extension file `TrustFrameworkExtensions.xml`, you can skip toothis section.</span></span>

1.  <span data-ttu-id="700db-170">開啟 hello 原則 (例如，TrustFrameworkBase.xml) 的基底的檔案。</span><span class="sxs-lookup"><span data-stu-id="700db-170">Open hello base file of your policy (for example, TrustFrameworkBase.xml).</span></span>
2.  <span data-ttu-id="700db-171">尋找 hello`<UserJourneys>`項目，並複製 hello 整個內容`<UserJourneys>`節點。</span><span class="sxs-lookup"><span data-stu-id="700db-171">Find hello `<UserJourneys>` element and copy hello entire content of `<UserJourneys>` node.</span></span>
3.  <span data-ttu-id="700db-172">開啟 hello 延伸模組檔案 (例如，TrustFrameworkExtensions.xml)，並尋找 hello`<UserJourneys>`項目。</span><span class="sxs-lookup"><span data-stu-id="700db-172">Open hello extension file (for example, TrustFrameworkExtensions.xml) and find hello `<UserJourneys>` element.</span></span> <span data-ttu-id="700db-173">如果 hello 項目不存在，請加入一個參考。</span><span class="sxs-lookup"><span data-stu-id="700db-173">If hello element doesn't exist, add one.</span></span>
4.  <span data-ttu-id="700db-174">貼上 hello 整個內容`<UserJournesy>`您複製 hello 的子系的節點`<UserJourneys>`項目。</span><span class="sxs-lookup"><span data-stu-id="700db-174">Paste hello entire content of `<UserJournesy>` node that you copied as a child of hello `<UserJourneys>` element.</span></span>

### <a name="display-hello-button"></a><span data-ttu-id="700db-175">顯示 hello 按鈕</span><span class="sxs-lookup"><span data-stu-id="700db-175">Display hello button</span></span>
<span data-ttu-id="700db-176">hello`<ClaimsProviderSelections>`項目會定義 hello 宣告提供者選擇的選項清單以及它們的順序。</span><span class="sxs-lookup"><span data-stu-id="700db-176">hello `<ClaimsProviderSelections>` element defines hello list of claims provider selection options and their order.</span></span>  <span data-ttu-id="700db-177">`<ClaimsProviderSelection>`項目是 sign-up/登入頁面上的類似 tooan 身分識別提供者按鈕。</span><span class="sxs-lookup"><span data-stu-id="700db-177">`<ClaimsProviderSelection>` element is analogous tooan identity provider button on a sign-up/sign-in page.</span></span> <span data-ttu-id="700db-178">如果您將加入`<ClaimsProviderSelection>`的 Microsoft 帳戶的項目，新的按鈕顯示落在 hello 頁面上的使用者。</span><span class="sxs-lookup"><span data-stu-id="700db-178">If you add a `<ClaimsProviderSelection>` element for Microsoft account, a new button shows up when a user lands on hello page.</span></span> <span data-ttu-id="700db-179">tooadd 這個項目：</span><span class="sxs-lookup"><span data-stu-id="700db-179">tooadd this element:</span></span>

1.  <span data-ttu-id="700db-180">尋找 hello`<UserJourney>`節點包含`Id="SignUpOrSignIn"`hello 您複製的使用者歷程中。</span><span class="sxs-lookup"><span data-stu-id="700db-180">Find hello `<UserJourney>` node that includes `Id="SignUpOrSignIn"` in hello user journey that you copied.</span></span>
2.  <span data-ttu-id="700db-181">找出 hello`<OrchestrationStep>`包含的節點`Order="1"`</span><span class="sxs-lookup"><span data-stu-id="700db-181">Locate hello `<OrchestrationStep>` node that includes `Order="1"`</span></span>
3.  <span data-ttu-id="700db-182">在 `<ClaimsProviderSelections>` 節點下，新增下列 XML 程式碼片段：</span><span class="sxs-lookup"><span data-stu-id="700db-182">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="MSAExchange" />
```

### <a name="link-hello-button-tooan-action"></a><span data-ttu-id="700db-183">連結 hello 按鈕 tooan 動作</span><span class="sxs-lookup"><span data-stu-id="700db-183">Link hello button tooan action</span></span>
<span data-ttu-id="700db-184">既然您已備妥 按鈕，您需要 toolink 它 tooan 動作。</span><span class="sxs-lookup"><span data-stu-id="700db-184">Now that you have a button in place, you need toolink it tooan action.</span></span> <span data-ttu-id="700db-185">hello 動作，在此情況下，為 Microsoft 帳戶 tooreceive 與 Azure AD B2C toocommunicate 語彙基元。</span><span class="sxs-lookup"><span data-stu-id="700db-185">hello action, in this case, is for Azure AD B2C toocommunicate with Microsoft Account tooreceive a token.</span></span> <span data-ttu-id="700db-186">藉由連結的 Microsoft 帳戶的宣告提供者的 hello 技術設定檔連結 hello 按鈕 tooan 動作：</span><span class="sxs-lookup"><span data-stu-id="700db-186">Link hello button tooan action by linking hello technical profile for your Microsoft Account claims provider:</span></span>

1.  <span data-ttu-id="700db-187">尋找 hello`<OrchestrationStep>`包含`Order="2"`在 hello`<UserJourney>`節點。</span><span class="sxs-lookup"><span data-stu-id="700db-187">Find hello `<OrchestrationStep>` that includes `Order="2"` in hello `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="700db-188">在 `<ClaimsExchanges>` 節點下，新增下列 XML 程式碼片段：</span><span class="sxs-lookup"><span data-stu-id="700db-188">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="MSAExchange" TechnicalProfileReferenceId="MSA-OIDC" />
```

> [!NOTE]
>
>   * <span data-ttu-id="700db-189">請確定 hello`Id`具有相同的值為 hello `TargetClaimsExchangeId` hello 前面一節中</span><span class="sxs-lookup"><span data-stu-id="700db-189">Ensure hello `Id` has hello same value as that of `TargetClaimsExchangeId` in hello preceding section</span></span>
>   * <span data-ttu-id="700db-190">請確定`TechnicalProfileReferenceId`設定您建立舊版 (MSA-OIDC) toohello 技術設定檔的識別碼。</span><span class="sxs-lookup"><span data-stu-id="700db-190">Ensure `TechnicalProfileReferenceId` ID is set toohello technical profile you created earlier (MSA-OIDC).</span></span>

## <a name="upload-hello-policy-tooyour-tenant"></a><span data-ttu-id="700db-191">上傳 hello 原則 tooyour 租用戶</span><span class="sxs-lookup"><span data-stu-id="700db-191">Upload hello policy tooyour tenant</span></span>
1.  <span data-ttu-id="700db-192">在 hello [Azure 入口網站](https://portal.azure.com)，切換至 hello[內容，您的 Azure AD B2C 租用戶](active-directory-b2c-navigate-to-b2c-context.md)，並開啟 hello **Azure AD B2C**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="700db-192">In hello [Azure portal](https://portal.azure.com), switch into hello [context of your Azure AD B2C tenant](active-directory-b2c-navigate-to-b2c-context.md), and open hello **Azure AD B2C** blade.</span></span>
2.  <span data-ttu-id="700db-193">選取 [識別體驗架構]。</span><span class="sxs-lookup"><span data-stu-id="700db-193">Select **Identity Experience Framework**.</span></span>
3.  <span data-ttu-id="700db-194">開啟 hello**所有原則**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="700db-194">Open hello **All Policies** blade.</span></span>
4.  <span data-ttu-id="700db-195">選取 [上傳原則]。</span><span class="sxs-lookup"><span data-stu-id="700db-195">Select **Upload Policy**.</span></span>
5.  <span data-ttu-id="700db-196">請檢查**如果存在的話，請覆寫 hello 原則**方塊。</span><span class="sxs-lookup"><span data-stu-id="700db-196">Check **Overwrite hello policy if it exists** box.</span></span>
6.  <span data-ttu-id="700db-197">**上傳**TrustFrameworkExtensions.xml，並確定它不會通過 hello 驗證</span><span class="sxs-lookup"><span data-stu-id="700db-197">**Upload** TrustFrameworkExtensions.xml and ensure that it does not fail hello validation</span></span>

## <a name="test-hello-custom-policy-by-using-run-now"></a><span data-ttu-id="700db-198">使用 立即執行測試 hello 自訂原則</span><span class="sxs-lookup"><span data-stu-id="700db-198">Test hello custom policy by using Run Now</span></span>

1.  <span data-ttu-id="700db-199">開啟**Azure AD B2C 設定**並移過**身分識別體驗架構**。</span><span class="sxs-lookup"><span data-stu-id="700db-199">Open **Azure AD B2C Settings** and go too**Identity Experience Framework**.</span></span>
> [!NOTE]
>
><span data-ttu-id="700db-200">**現在就執行**需要至少一個應用程式 toobe 預先 hello 租用戶上。</span><span class="sxs-lookup"><span data-stu-id="700db-200">**Run now** requires at least one application toobe preregistered on hello tenant.</span></span> <span data-ttu-id="700db-201">如何 tooregister 應用程式，請參閱的 toolearn hello Azure AD B2C[開始](active-directory-b2c-get-started.md)文章或 hello[應用程式註冊](active-directory-b2c-app-registration.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="700db-201">toolearn how tooregister applications, see hello Azure AD B2C [Get started](active-directory-b2c-get-started.md) article or hello [Application registration](active-directory-b2c-app-registration.md) article.</span></span>
2.  <span data-ttu-id="700db-202">開啟**B2C_1A_signup_signin**，hello 上載的信賴憑證者 (rp) 自訂原則。</span><span class="sxs-lookup"><span data-stu-id="700db-202">Open **B2C_1A_signup_signin**, hello relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="700db-203">選取 [立即執行]。</span><span class="sxs-lookup"><span data-stu-id="700db-203">Select **Run now**.</span></span>
3.  <span data-ttu-id="700db-204">您應該能夠 toosign 中使用的 Microsoft 帳戶。</span><span class="sxs-lookup"><span data-stu-id="700db-204">You should be able toosign in using Microsoft account.</span></span>

## <a name="optional-register-hello-microsoft-account-claims-provider-tooprofile-edit-user-journey"></a><span data-ttu-id="700db-205">[選用]註冊 hello Microsoft 帳戶宣告提供者 tooProfile 編輯使用者旅程</span><span class="sxs-lookup"><span data-stu-id="700db-205">[Optional] Register hello Microsoft Account claims provider tooProfile-Edit user journey</span></span>
<span data-ttu-id="700db-206">您可能會想 tooadd hello Microsoft 帳戶身分識別提供者也 tooyour 使用者`ProfileEdit`使用者之旅。</span><span class="sxs-lookup"><span data-stu-id="700db-206">You may want tooadd hello Microsoft Account identity provider also tooyour user `ProfileEdit` user journey.</span></span> <span data-ttu-id="700db-207">toomake 提供，我們可以重覆 hello 最後的兩個步驟：</span><span class="sxs-lookup"><span data-stu-id="700db-207">toomake it available, we repeat hello last two steps:</span></span>

### <a name="display-hello-button"></a><span data-ttu-id="700db-208">顯示 hello 按鈕</span><span class="sxs-lookup"><span data-stu-id="700db-208">Display hello button</span></span>
1.  <span data-ttu-id="700db-209">開啟 hello 原則 (例如，TrustFrameworkExtensions.xml) 的延伸模組檔案。</span><span class="sxs-lookup"><span data-stu-id="700db-209">Open hello extension file of your policy (for example, TrustFrameworkExtensions.xml).</span></span>
2.  <span data-ttu-id="700db-210">尋找 hello`<UserJourney>`節點包含`Id="ProfileEdit"`hello 您複製的使用者歷程中。</span><span class="sxs-lookup"><span data-stu-id="700db-210">Find hello `<UserJourney>` node that includes `Id="ProfileEdit"` in hello user journey that you copied.</span></span>
3.  <span data-ttu-id="700db-211">找出 hello`<OrchestrationStep>`包含的節點`Order="1"`</span><span class="sxs-lookup"><span data-stu-id="700db-211">Locate hello `<OrchestrationStep>` node that includes `Order="1"`</span></span>
4.  <span data-ttu-id="700db-212">在 `<ClaimsProviderSelections>` 節點下，新增下列 XML 程式碼片段：</span><span class="sxs-lookup"><span data-stu-id="700db-212">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="MSAExchange" />
```

### <a name="link-hello-button-tooan-action"></a><span data-ttu-id="700db-213">連結 hello 按鈕 tooan 動作</span><span class="sxs-lookup"><span data-stu-id="700db-213">Link hello button tooan action</span></span>
1.  <span data-ttu-id="700db-214">尋找 hello`<OrchestrationStep>`包含`Order="2"`在 hello`<UserJourney>`節點。</span><span class="sxs-lookup"><span data-stu-id="700db-214">Find hello `<OrchestrationStep>` that includes `Order="2"` in hello `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="700db-215">在 `<ClaimsExchanges>` 節點下，新增下列 XML 程式碼片段：</span><span class="sxs-lookup"><span data-stu-id="700db-215">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="MSAExchange" TechnicalProfileReferenceId="MSA-OIDC" />
```

### <a name="test-hello-custom-profile-edit-policy-by-using-run-now"></a><span data-ttu-id="700db-216">使用 立即執行測試 hello 自訂設定檔編輯原則</span><span class="sxs-lookup"><span data-stu-id="700db-216">Test hello custom Profile-Edit policy by using Run Now</span></span>
1.  <span data-ttu-id="700db-217">開啟**Azure AD B2C 設定**並移過**身分識別體驗架構**。</span><span class="sxs-lookup"><span data-stu-id="700db-217">Open **Azure AD B2C Settings** and go too**Identity Experience Framework**.</span></span>
2.  <span data-ttu-id="700db-218">開啟**B2C_1A_ProfileEdit**，hello 上載的信賴憑證者 (rp) 自訂原則。</span><span class="sxs-lookup"><span data-stu-id="700db-218">Open **B2C_1A_ProfileEdit**, hello relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="700db-219">選取 [立即執行]。</span><span class="sxs-lookup"><span data-stu-id="700db-219">Select **Run now**.</span></span>
3.  <span data-ttu-id="700db-220">您應該能夠 toosign 中使用的 Microsoft 帳戶。</span><span class="sxs-lookup"><span data-stu-id="700db-220">You should be able toosign in using Microsoft account.</span></span>

## <a name="download-hello-complete-policy-files"></a><span data-ttu-id="700db-221">下載 hello 完整的原則檔案</span><span class="sxs-lookup"><span data-stu-id="700db-221">Download hello complete policy files</span></span>
<span data-ttu-id="700db-222">選擇性： 我們建議您建置您使用您自己的自訂原則檔完成的 hello 開始使用自訂原則逐步執行，而不是使用這些範例檔案之後的案例。</span><span class="sxs-lookup"><span data-stu-id="700db-222">Optional: We recommend you build your scenario using your own Custom policy files after completing hello Getting Started with Custom Policies walk through instead of using these sample files.</span></span>  [<span data-ttu-id="700db-223">參考的範例原則檔案</span><span class="sxs-lookup"><span data-stu-id="700db-223">Sample policy files for reference</span></span>](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-setup-msa-app)
