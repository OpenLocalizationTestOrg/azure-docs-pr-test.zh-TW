---
title: "Azure Active Directory B2C︰使用自訂原則新增 Salesforce SAML 提供者 | Microsoft Docs"
description: "深入了解如何 toocreate 和管理 Azure Active Directory B2C 的自訂原則。"
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: d7f4143f-cd7c-4939-91a8-231a4104dc2c
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 06/11/2017
ms.author: parakhj
ms.openlocfilehash: f14c9d96980ff124110db7cfb58bf7cd81750b7c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-sign-in-by-using-salesforce-accounts-via-saml"></a><span data-ttu-id="138ad-103">Azure Active Directory B2C︰使用 Salesforce 帳戶透過 SAML 來登入</span><span class="sxs-lookup"><span data-stu-id="138ad-103">Azure Active Directory B2C: Sign in by using Salesforce accounts via SAML</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="138ad-104">本文章將示範如何 toouse[自訂原則](active-directory-b2c-overview-custom.md)tooset 組成特定的 Salesforce 組織中使用者的登入。</span><span class="sxs-lookup"><span data-stu-id="138ad-104">This article shows you how toouse [custom policies](active-directory-b2c-overview-custom.md) tooset up sign-in for users from a specific Salesforce organization.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="138ad-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="138ad-105">Prerequisites</span></span>

### <a name="azure-ad-b2c-setup"></a><span data-ttu-id="138ad-106">Azure AD B2C 設定</span><span class="sxs-lookup"><span data-stu-id="138ad-106">Azure AD B2C setup</span></span>

<span data-ttu-id="138ad-107">請確定您已完成所有可為您示範如何太 hello 步驟[開始使用自訂原則](active-directory-b2c-get-started-custom.md)中 Azure Active Directory B2C (Azure AD B2C)。</span><span class="sxs-lookup"><span data-stu-id="138ad-107">Ensure that you have completed all of hello steps that show you how too[get started with custom policies](active-directory-b2c-get-started-custom.md) in Azure Active Directory B2C (Azure AD B2C).</span></span>

<span data-ttu-id="138ad-108">其中包含：</span><span class="sxs-lookup"><span data-stu-id="138ad-108">These include:</span></span>

* <span data-ttu-id="138ad-109">建立 Azure AD B2C 租用戶。</span><span class="sxs-lookup"><span data-stu-id="138ad-109">Create an Azure AD B2C tenant.</span></span>
* <span data-ttu-id="138ad-110">建立 Azure AD B2C 應用程式。</span><span class="sxs-lookup"><span data-stu-id="138ad-110">Create an Azure AD B2C application.</span></span>
* <span data-ttu-id="138ad-111">註冊兩個原則引擎應用程式。</span><span class="sxs-lookup"><span data-stu-id="138ad-111">Register two policy engine applications.</span></span>
* <span data-ttu-id="138ad-112">設定金鑰。</span><span class="sxs-lookup"><span data-stu-id="138ad-112">Set up keys.</span></span>
* <span data-ttu-id="138ad-113">設定 hello 入門套件。</span><span class="sxs-lookup"><span data-stu-id="138ad-113">Set up hello starter pack.</span></span>

### <a name="salesforce-setup"></a><span data-ttu-id="138ad-114">Salesforce 設定</span><span class="sxs-lookup"><span data-stu-id="138ad-114">Salesforce setup</span></span>

<span data-ttu-id="138ad-115">在本文中，我們假設您已完成 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="138ad-115">In this article, we assume that you have already done hello following:</span></span>

* <span data-ttu-id="138ad-116">註冊 Salesforce 帳戶。</span><span class="sxs-lookup"><span data-stu-id="138ad-116">Signed up for a Salesforce account.</span></span> <span data-ttu-id="138ad-117">您可以註冊[免費的開發人員版本帳戶](https://developer.salesforce.com/signup)。</span><span class="sxs-lookup"><span data-stu-id="138ad-117">You can sign up for a [free Developer Edition account](https://developer.salesforce.com/signup).</span></span>
* <span data-ttu-id="138ad-118">為您的 Salesforce 組織[設定網域](https://help.salesforce.com/articleView?id=domain_name_setup.htm&language=en_US&type=0)。</span><span class="sxs-lookup"><span data-stu-id="138ad-118">[Set up a My Domain](https://help.salesforce.com/articleView?id=domain_name_setup.htm&language=en_US&type=0) for your Salesforce organization.</span></span>

## <a name="set-up-salesforce-so-users-can-federate"></a><span data-ttu-id="138ad-119">設定 Salesforce，讓使用者可以建立同盟</span><span class="sxs-lookup"><span data-stu-id="138ad-119">Set up Salesforce so users can federate</span></span>

<span data-ttu-id="138ad-120">toohelp 與 Salesforce 的 Azure AD B2C 通訊，您需要 tooget hello Salesforce 中繼資料 URL。</span><span class="sxs-lookup"><span data-stu-id="138ad-120">toohelp Azure AD B2C communicate with Salesforce, you need tooget hello Salesforce metadata URL.</span></span>

### <a name="set-up-salesforce-as-an-identity-provider"></a><span data-ttu-id="138ad-121">將 Salesforce 設定為識別提供者</span><span class="sxs-lookup"><span data-stu-id="138ad-121">Set up Salesforce as an identity provider</span></span>

> [!NOTE]
> <span data-ttu-id="138ad-122">在本文中，我們假設您使用 [Salesforce Lightning 經驗](https://developer.salesforce.com/page/Lightning_Experience_FAQ)。</span><span class="sxs-lookup"><span data-stu-id="138ad-122">In this article, we assume you are using [Salesforce Lightning Experience](https://developer.salesforce.com/page/Lightning_Experience_FAQ).</span></span>

1. <span data-ttu-id="138ad-123">[登入 tooSalesforce](https://login.salesforce.com/)。</span><span class="sxs-lookup"><span data-stu-id="138ad-123">[Sign in tooSalesforce](https://login.salesforce.com/).</span></span> 
2. <span data-ttu-id="138ad-124">於 hello 上左功能表中，在**設定**，依序展開**識別**，然後按一下**身分識別提供者**。</span><span class="sxs-lookup"><span data-stu-id="138ad-124">On hello left menu, under **Settings**, expand **Identity**, and then click **Identity Provider**.</span></span>
3. <span data-ttu-id="138ad-125">按一下 [啟用識別提供者]。</span><span class="sxs-lookup"><span data-stu-id="138ad-125">Click **Enable Identity Provider**.</span></span>
4. <span data-ttu-id="138ad-126">在下**選取 hello 憑證**，選取您想要使用 Azure AD B2C Salesforce toouse toocommunicate hello 憑證。</span><span class="sxs-lookup"><span data-stu-id="138ad-126">Under **Select hello certificate**, select hello certificate you want Salesforce toouse toocommunicate with Azure AD B2C.</span></span> <span data-ttu-id="138ad-127">（您可以使用 hello 預設憑證）。按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="138ad-127">(You can use hello default certificate.) Click **Save**.</span></span> 

### <a name="create-a-connected-app-in-salesforce"></a><span data-ttu-id="138ad-128">在 Salesforce 中建立連線應用程式</span><span class="sxs-lookup"><span data-stu-id="138ad-128">Create a connected app in Salesforce</span></span>

1. <span data-ttu-id="138ad-129">在 hello**身分識別提供者**頁面上，移過**服務提供者**。</span><span class="sxs-lookup"><span data-stu-id="138ad-129">On hello **Identity Provider** page, go too**Service Providers**.</span></span>
2. <span data-ttu-id="138ad-130">按一下 [現在透過連線應用程式建立服務提供者]**。**按一下這裡。</span><span class="sxs-lookup"><span data-stu-id="138ad-130">Click **Service Providers are now created via Connected Apps. Click here.**</span></span>
3. <span data-ttu-id="138ad-131">在下**基本資訊**，輸入您已連線的應用程式所需的 hello 值。</span><span class="sxs-lookup"><span data-stu-id="138ad-131">Under **Basic Information**,  enter hello required values for your connected app.</span></span>
4. <span data-ttu-id="138ad-132">在下**Web 應用程式設定**，選取 hello**啟用 SAML**核取方塊。</span><span class="sxs-lookup"><span data-stu-id="138ad-132">Under **Web App Settings**, select hello **Enable SAML** check box.</span></span>
5. <span data-ttu-id="138ad-133">在 hello**實體識別碼**欄位中，輸入下列 URL 的 hello。</span><span class="sxs-lookup"><span data-stu-id="138ad-133">In hello **Entity ID** field, enter hello following URL.</span></span> <span data-ttu-id="138ad-134">請確定您取代 hello 值`tenantName`。</span><span class="sxs-lookup"><span data-stu-id="138ad-134">Ensure that you replace hello value for `tenantName`.</span></span>
      ```
      https://login.microsoftonline.com/te/tenantName.onmicrosoft.com/B2C_1A_TrustFrameworkBase
      ```
6. <span data-ttu-id="138ad-135">在 hello **ACS URL**欄位中，輸入下列 URL 的 hello。</span><span class="sxs-lookup"><span data-stu-id="138ad-135">In hello **ACS URL** field, enter hello following URL.</span></span> <span data-ttu-id="138ad-136">請確定您取代 hello 值`tenantName`。</span><span class="sxs-lookup"><span data-stu-id="138ad-136">Ensure that you replace hello value for `tenantName`.</span></span>
      ```
      https://login.microsoftonline.com/te/tenantName.onmicrosoft.com/B2C_1A_TrustFrameworkBase/samlp/sso/assertionconsumer
      ```
7. <span data-ttu-id="138ad-137">保留所有其他設定的 hello 預設值。</span><span class="sxs-lookup"><span data-stu-id="138ad-137">Leave hello default values for all other settings.</span></span>
8. <span data-ttu-id="138ad-138">捲動 toohello hello 清單底部，然後按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="138ad-138">Scroll toohello bottom of hello list, and then click **Save**.</span></span>

### <a name="get-hello-metadata-url"></a><span data-ttu-id="138ad-139">取得 hello 中繼資料 URL</span><span class="sxs-lookup"><span data-stu-id="138ad-139">Get hello metadata URL</span></span>

1. <span data-ttu-id="138ad-140">在您連接的應用程式的 hello 概觀頁面上，按一下 **管理**。</span><span class="sxs-lookup"><span data-stu-id="138ad-140">On hello overview page of your connected app, click **Manage**.</span></span>
2. <span data-ttu-id="138ad-141">複製 hello 值**中繼資料探索端點**，並將其儲存。</span><span class="sxs-lookup"><span data-stu-id="138ad-141">Copy hello value for **Metadata Discovery Endpoint**, and then save it.</span></span> <span data-ttu-id="138ad-142">您將在本文稍後使用它。</span><span class="sxs-lookup"><span data-stu-id="138ad-142">You'll use it later in this article.</span></span>

### <a name="set-up-salesforce-users-toofederate"></a><span data-ttu-id="138ad-143">設定 Salesforce 使用者 toofederate</span><span class="sxs-lookup"><span data-stu-id="138ad-143">Set up Salesforce users toofederate</span></span>

1. <span data-ttu-id="138ad-144">在 hello**管理**頁面已連線的應用程式移過**設定檔**。</span><span class="sxs-lookup"><span data-stu-id="138ad-144">On hello **Manage** page of your connected app, go too**Profiles**.</span></span>
2. <span data-ttu-id="138ad-145">按一下 [管理設定檔]。</span><span class="sxs-lookup"><span data-stu-id="138ad-145">Click **Manage Profiles**.</span></span>
3. <span data-ttu-id="138ad-146">Hello 設定檔 （或使用者群組） 選取您想使用 Azure AD B2C toofederate。</span><span class="sxs-lookup"><span data-stu-id="138ad-146">Select hello profiles (or groups of users) that you want toofederate with Azure AD B2C.</span></span> <span data-ttu-id="138ad-147">身為系統管理員，選取 hello**系統管理員**核取方塊，以便您可以使用您的 Salesforce 帳戶同盟。</span><span class="sxs-lookup"><span data-stu-id="138ad-147">As a system administrator, select hello **System Administrator** check box, so that you can federate by using your Salesforce account.</span></span>

## <a name="generate-a-signing-certificate-for-azure-ad-b2c"></a><span data-ttu-id="138ad-148">產生 Azure AD B2C 的簽署憑證</span><span class="sxs-lookup"><span data-stu-id="138ad-148">Generate a signing certificate for Azure AD B2C</span></span>

<span data-ttu-id="138ad-149">由 Azure AD B2C 簽署 tooSalesforce 需要 toobe 傳送要求。</span><span class="sxs-lookup"><span data-stu-id="138ad-149">Requests sent tooSalesforce need toobe signed by Azure AD B2C.</span></span> <span data-ttu-id="138ad-150">toogenerate 簽署的憑證，開啟 Azure PowerShell，然後再執行下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="138ad-150">toogenerate a signing certificate, open Azure PowerShell, and then run hello following commands.</span></span>

> [!NOTE]
> <span data-ttu-id="138ad-151">請確定您更新 hello 頂端的兩行程式碼中 hello 租用戶名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="138ad-151">Make sure that you update hello tenant name and password in hello top two lines.</span></span>

```PowerShell
$tenantName = "<YOUR TENANT NAME>.onmicrosoft.com"
$pwdText = "<YOUR PASSWORD HERE>"

$Cert = New-SelfSignedCertificate -CertStoreLocation Cert:\CurrentUser\My -DnsName "SamlIdp.$tenantName" -Subject "B2C SAML Signing Cert" -HashAlgorithm SHA256 -KeySpec Signature -KeyLength 2048

$pwd = ConvertTo-SecureString -String $pwdText -Force -AsPlainText

Export-PfxCertificate -Cert $Cert -FilePath .\B2CSigningCert.pfx -Password $pwd
```

## <a name="add-hello-saml-signing-certificate-tooazure-ad-b2c"></a><span data-ttu-id="138ad-152">新增 hello SAML 簽章憑證 tooAzure AD B2C</span><span class="sxs-lookup"><span data-stu-id="138ad-152">Add hello SAML signing certificate tooAzure AD B2C</span></span>

<span data-ttu-id="138ad-153">上傳簽署的憑證 tooyour Azure AD B2C 租用戶的 hello:</span><span class="sxs-lookup"><span data-stu-id="138ad-153">Upload hello signing certificate tooyour Azure AD B2C tenant:</span></span> 

1. <span data-ttu-id="138ad-154">移 tooyour Azure AD B2C 租用戶。</span><span class="sxs-lookup"><span data-stu-id="138ad-154">Go tooyour Azure AD B2C tenant.</span></span> <span data-ttu-id="138ad-155">按一下 [設定]  >  [身分識別體驗架構]  >  [原則金鑰]。</span><span class="sxs-lookup"><span data-stu-id="138ad-155">Click **Settings** > **Identity Experience Framework** > **Policy Keys**.</span></span>
2. <span data-ttu-id="138ad-156">按一下 [+新增]，然後：</span><span class="sxs-lookup"><span data-stu-id="138ad-156">Click **+Add**, and then:</span></span>
    1. <span data-ttu-id="138ad-157">按一下 [選項]  >  [上傳]。</span><span class="sxs-lookup"><span data-stu-id="138ad-157">Click **Options** > **Upload**.</span></span>
    2. <span data-ttu-id="138ad-158">輸入**名稱** (例如，SAMLSigningCert)。</span><span class="sxs-lookup"><span data-stu-id="138ad-158">Enter a **Name** (for example, SAMLSigningCert).</span></span> <span data-ttu-id="138ad-159">hello 前置詞*B2C_1A_*會自動加入 toohello 金鑰的名稱。</span><span class="sxs-lookup"><span data-stu-id="138ad-159">hello prefix *B2C_1A_* is automatically added toohello name of your key.</span></span>
    3. <span data-ttu-id="138ad-160">tooselect 憑證，請選取**上傳檔案控制項**。</span><span class="sxs-lookup"><span data-stu-id="138ad-160">tooselect your certificate, select **upload file control**.</span></span> 
    4. <span data-ttu-id="138ad-161">輸入您在 hello PowerShell 指令碼中設定的 hello 憑證的密碼。</span><span class="sxs-lookup"><span data-stu-id="138ad-161">Enter hello certificate's password that you set in hello PowerShell script.</span></span>
3. <span data-ttu-id="138ad-162">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="138ad-162">Click **Create**.</span></span>
4. <span data-ttu-id="138ad-163">請確認您已建立金鑰 (例如，B2C_1A_SAMLSigningCert)。</span><span class="sxs-lookup"><span data-stu-id="138ad-163">Verify that you've created a key (for example, B2C_1A_SAMLSigningCert).</span></span> <span data-ttu-id="138ad-164">記下 hello 完整名稱 (包括*B2C_1A_*)。</span><span class="sxs-lookup"><span data-stu-id="138ad-164">Take note of hello full name (including *B2C_1A_*).</span></span> <span data-ttu-id="138ad-165">您將參考 toothis 稍後 hello 原則中的索引鍵。</span><span class="sxs-lookup"><span data-stu-id="138ad-165">You will refer toothis key later in hello policy.</span></span>

## <a name="create-hello-salesforce-saml-claims-provider-in-your-base-policy"></a><span data-ttu-id="138ad-166">建立基底原則中的 hello Salesforce SAML 宣告提供者</span><span class="sxs-lookup"><span data-stu-id="138ad-166">Create hello Salesforce SAML claims provider in your base policy</span></span>

<span data-ttu-id="138ad-167">您需要 toodefine Salesforce 的宣告提供者，使用者可以使用登入 Salesforce。</span><span class="sxs-lookup"><span data-stu-id="138ad-167">You need toodefine Salesforce as a claims provider so users can sign in by using Salesforce.</span></span> <span data-ttu-id="138ad-168">換句話說，您需要 Azure AD B2C 將與其通訊的 toospecify hello 端點。</span><span class="sxs-lookup"><span data-stu-id="138ad-168">In other words, you need toospecify hello endpoint that Azure AD B2C will communicate with.</span></span> <span data-ttu-id="138ad-169">hello 端點將*提供*一組*宣告*Azure AD B2C 使用特定的使用者已驗證的 tooverify。</span><span class="sxs-lookup"><span data-stu-id="138ad-169">hello endpoint will *provide* a set of *claims* that Azure AD B2C uses tooverify that a specific user has authenticated.</span></span> <span data-ttu-id="138ad-170">toodo，新增`<ClaimsProvider>`salesforce 原則的 hello 延伸模組檔案中：</span><span class="sxs-lookup"><span data-stu-id="138ad-170">toodo this, add a `<ClaimsProvider>` for Salesforce in hello extension file of your policy:</span></span>

1. <span data-ttu-id="138ad-171">在您的工作目錄中開啟 hello 延伸模組檔案 (TrustFrameworkExtensions.xml)。</span><span class="sxs-lookup"><span data-stu-id="138ad-171">In your working directory, open hello extension file (TrustFrameworkExtensions.xml).</span></span>
2. <span data-ttu-id="138ad-172">尋找 hello `<ClaimsProviders>` > 一節。</span><span class="sxs-lookup"><span data-stu-id="138ad-172">Find hello `<ClaimsProviders>` section.</span></span> <span data-ttu-id="138ad-173">如果不存在，則會建立 hello 根節點下。</span><span class="sxs-lookup"><span data-stu-id="138ad-173">If it does not exist, create it under hello root node.</span></span>
3. <span data-ttu-id="138ad-174">新增 `<ClaimsProvider>`：</span><span class="sxs-lookup"><span data-stu-id="138ad-174">Add a new `<ClaimsProvider>`:</span></span>

    ```XML
    <ClaimsProvider>
      <Domain>salesforce</Domain>
      <DisplayName>Salesforce</DisplayName>
      <TechnicalProfiles>
        <TechnicalProfile Id="salesforce">
          <DisplayName>Salesforce</DisplayName>
          <Description>Login with your Salesforce account</Description>
          <Protocol Name="SAML2"/>
          <Metadata>
            <Item Key="RequestsSigned">false</Item>
            <Item Key="WantsEncryptedAssertions">false</Item>
            <Item Key="WantsSignedAssertions">false</Item>
            <Item Key="PartnerEntity">https://contoso-dev-ed.my.salesforce.com/.well-known/samlidp.xml</Item>
          </Metadata>
          <CryptographicKeys>
            <Key Id="SamlAssertionSigning" StorageReferenceId="B2C_1A_SAMLSigningCert"/>
            <Key Id="SamlMessageSigning" StorageReferenceId="B2C_1A_SAMLSigningCert"/>
          </CryptographicKeys>
          <OutputClaims>
            <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="userId"/>
            <OutputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="given_name"/>
            <OutputClaim ClaimTypeReferenceId="surname" PartnerClaimType="family_name"/>
            <OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="email"/>
            <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="username"/>
            <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="externalIdp"/>
            <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="SAMLIdp" />
          </OutputClaims>
          <OutputClaimsTransformations>
            <OutputClaimsTransformation ReferenceId="CreateRandomUPNUserName"/>
            <OutputClaimsTransformation ReferenceId="CreateUserPrincipalName"/>
            <OutputClaimsTransformation ReferenceId="CreateAlternativeSecurityId"/>
            <OutputClaimsTransformation ReferenceId="CreateSubjectClaimFromAlternativeSecurityId"/>
          </OutputClaimsTransformations>
          <UseTechnicalProfileForSessionManagement ReferenceId="SM-Noop"/>
        </TechnicalProfile>
      </TechnicalProfiles>
    </ClaimsProvider>
    ```

<span data-ttu-id="138ad-175">在 hello`<ClaimsProvider>`節點：</span><span class="sxs-lookup"><span data-stu-id="138ad-175">Under hello `<ClaimsProvider>` node:</span></span>

1. <span data-ttu-id="138ad-176">變更 hello 值`<Domain>`tooa 區別的唯一值`<ClaimsProvider>`來自其他身分識別提供者。</span><span class="sxs-lookup"><span data-stu-id="138ad-176">Change hello value for `<Domain>` tooa unique value that distinguishes `<ClaimsProvider>` from other identity providers.</span></span>
2. <span data-ttu-id="138ad-177">更新 hello 值`<DisplayName>`tooa hello 的顯示名稱宣告提供者。</span><span class="sxs-lookup"><span data-stu-id="138ad-177">Update hello value for `<DisplayName>` tooa display name for hello claims provider.</span></span> <span data-ttu-id="138ad-178">目前不使用此值。</span><span class="sxs-lookup"><span data-stu-id="138ad-178">Currently, this value is not used.</span></span>

### <a name="update-hello-technical-profile"></a><span data-ttu-id="138ad-179">更新 hello 技術設定檔</span><span class="sxs-lookup"><span data-stu-id="138ad-179">Update hello technical profile</span></span>

<span data-ttu-id="138ad-180">tooget SAML 權杖中來自 Salesforce，定義 Azure AD B2C 將 Azure Active Directory (Azure AD) 搭配使用 toocommunicate hello 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="138ad-180">tooget a SAML token from Salesforce, define hello protocols that Azure AD B2C will use toocommunicate with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="138ad-181">這樣在 hello`<TechnicalProfile>`元素`<ClaimsProvider>`:</span><span class="sxs-lookup"><span data-stu-id="138ad-181">Do this in hello `<TechnicalProfile>` element of `<ClaimsProvider>`:</span></span>

1. <span data-ttu-id="138ad-182">更新 hello 識別碼 hello`<TechnicalProfile>`節點。</span><span class="sxs-lookup"><span data-stu-id="138ad-182">Update hello ID of hello `<TechnicalProfile>` node.</span></span> <span data-ttu-id="138ad-183">這個識別碼是使用的 toorefer toothis 技術 hello 原則的其他部分的設定檔。</span><span class="sxs-lookup"><span data-stu-id="138ad-183">This ID is used toorefer toothis technical profile from other parts of hello policy.</span></span>
2. <span data-ttu-id="138ad-184">更新 hello 值`<DisplayName>`。</span><span class="sxs-lookup"><span data-stu-id="138ad-184">Update hello value for `<DisplayName>`.</span></span> <span data-ttu-id="138ad-185">這個值會顯示在 hello 登入您的登入頁面上按鈕。</span><span class="sxs-lookup"><span data-stu-id="138ad-185">This value is displayed on hello sign-in button on your sign-in page.</span></span>
3. <span data-ttu-id="138ad-186">更新 hello 值`<Description>`。</span><span class="sxs-lookup"><span data-stu-id="138ad-186">Update hello value for `<Description>`.</span></span>
4. <span data-ttu-id="138ad-187">Salesforce 使用 hello SAML 2.0 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="138ad-187">Salesforce uses hello SAML 2.0 protocol.</span></span> <span data-ttu-id="138ad-188">請確定該 hello 值`<Protocol>`是**SAML2**。</span><span class="sxs-lookup"><span data-stu-id="138ad-188">Ensure that hello value for `<Protocol>` is **SAML2**.</span></span>

<span data-ttu-id="138ad-189">更新 hello `<Metadata>` hello 前面 XML tooreflect hello 設定特定的 Salesforce 帳戶中一節。</span><span class="sxs-lookup"><span data-stu-id="138ad-189">Update hello `<Metadata>` section in hello preceding XML tooreflect hello settings for your specific Salesforce account.</span></span> <span data-ttu-id="138ad-190">在 hello XML，更新 hello 中繼資料值：</span><span class="sxs-lookup"><span data-stu-id="138ad-190">In hello XML, update hello metadata values:</span></span>

1. <span data-ttu-id="138ad-191">更新 hello 值`<Item Key="PartnerEntity">`以您先前複製的 hello Salesforce 中繼資料 URL。</span><span class="sxs-lookup"><span data-stu-id="138ad-191">Update hello value of `<Item Key="PartnerEntity">` with hello Salesforce metadata URL you copied earlier.</span></span> <span data-ttu-id="138ad-192">它有下列格式的 hello:</span><span class="sxs-lookup"><span data-stu-id="138ad-192">It has hello following format:</span></span> 

    `https://contoso-dev-ed.my.salesforce.com/.well-known/samlidp/connectedapp.xml`

2. <span data-ttu-id="138ad-193">在 hello`<CryptographicKeys>`區段中，兩個執行個體的更新 hello 值`StorageReferenceId`toohello hello 索引鍵，您的簽署憑證 (例如，B2C_1A_SAMLSigningCert) 的名稱。</span><span class="sxs-lookup"><span data-stu-id="138ad-193">In hello `<CryptographicKeys>` section, update hello value for both instances of `StorageReferenceId` toohello name of hello key of your signing certificate (for example, B2C_1A_SAMLSigningCert).</span></span>

### <a name="upload-hello-extension-file-for-verification"></a><span data-ttu-id="138ad-194">上傳 hello 進行驗證的延伸模組檔案</span><span class="sxs-lookup"><span data-stu-id="138ad-194">Upload hello extension file for verification</span></span>

<span data-ttu-id="138ad-195">您的原則現在已設定，讓 Azure AD B2C 知道如何與 Salesforce toocommunicate。</span><span class="sxs-lookup"><span data-stu-id="138ad-195">Your policy is now configured so that Azure AD B2C knows how toocommunicate with Salesforce.</span></span> <span data-ttu-id="138ad-196">嘗試上傳您的原則，並不包含任何問題為止 tooverify hello 延伸模組檔案。</span><span class="sxs-lookup"><span data-stu-id="138ad-196">Try uploading hello extension file of your policy, tooverify that there aren't any issues so far.</span></span> <span data-ttu-id="138ad-197">原則的 tooupload hello 延伸模組檔案：</span><span class="sxs-lookup"><span data-stu-id="138ad-197">tooupload hello extension file of your policy:</span></span>

1. <span data-ttu-id="138ad-198">在 您的 Azure AD B2C 租用戶移 toohello**所有原則**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="138ad-198">In your Azure AD B2C tenant, go toohello **All Policies** blade.</span></span>
2. <span data-ttu-id="138ad-199">選取 hello**如果存在的話，請覆寫 hello 原則**核取方塊。</span><span class="sxs-lookup"><span data-stu-id="138ad-199">Select hello **Overwrite hello policy if it exists** check box.</span></span>
3. <span data-ttu-id="138ad-200">上傳 hello 延伸模組檔案 (TrustFrameworkExtensions.xml)。</span><span class="sxs-lookup"><span data-stu-id="138ad-200">Upload hello extension file (TrustFrameworkExtensions.xml).</span></span> <span data-ttu-id="138ad-201">請確定它不會驗證失敗。</span><span class="sxs-lookup"><span data-stu-id="138ad-201">Ensure that it doesn't fail validation.</span></span>

## <a name="register-hello-salesforce-saml-claims-provider-tooa-user-journey"></a><span data-ttu-id="138ad-202">註冊 hello Salesforce SAML 宣告提供者 tooa 使用者旅程</span><span class="sxs-lookup"><span data-stu-id="138ad-202">Register hello Salesforce SAML claims provider tooa user journey</span></span>

<span data-ttu-id="138ad-203">接下來，新增的使用者皆 Salesforce SAML 身分識別提供者 tooone hello。</span><span class="sxs-lookup"><span data-stu-id="138ad-203">Next, add hello Salesforce SAML identity provider tooone of your user journeys.</span></span> <span data-ttu-id="138ad-204">此時，hello 身分識別提供者已設定，但它並不適用於任何 hello 使用者註冊或登入頁面。</span><span class="sxs-lookup"><span data-stu-id="138ad-204">At this point, hello identity provider has been set up, but it’s not available on any of hello user sign-up or sign-in pages.</span></span> <span data-ttu-id="138ad-205">tooadd hello 身分識別提供者 tooa 登入頁面上，首先，建立現有的範本使用者旅程的重複。</span><span class="sxs-lookup"><span data-stu-id="138ad-205">tooadd hello identity provider tooa sign-in page, first, create a duplicate of an existing template user journey.</span></span> <span data-ttu-id="138ad-206">然後，修改 hello 範本，讓它也有 hello Azure AD 身分識別提供者。</span><span class="sxs-lookup"><span data-stu-id="138ad-206">Then, modify hello template so that it also has hello Azure AD identity provider.</span></span>

1. <span data-ttu-id="138ad-207">開啟 hello 原則 (例如，TrustFrameworkBase.xml) 的基底的檔案。</span><span class="sxs-lookup"><span data-stu-id="138ad-207">Open hello base file of your policy (for example, TrustFrameworkBase.xml).</span></span>
2. <span data-ttu-id="138ad-208">尋找 hello`<UserJourneys>`項目，然後按一下 複製 hello 整個`<UserJourney>`值，包括 Id ="SignUpOrSignIn"。</span><span class="sxs-lookup"><span data-stu-id="138ad-208">Find hello `<UserJourneys>` element, and then copy hello entire `<UserJourney>` value, including Id=”SignUpOrSignIn”.</span></span>
3. <span data-ttu-id="138ad-209">開啟 hello 延伸模組檔案 (例如，TrustFrameworkExtensions.xml)。</span><span class="sxs-lookup"><span data-stu-id="138ad-209">Open hello extension file (for example, TrustFrameworkExtensions.xml).</span></span> <span data-ttu-id="138ad-210">尋找 hello`<UserJourneys>`項目。</span><span class="sxs-lookup"><span data-stu-id="138ad-210">Find hello `<UserJourneys>` element.</span></span> <span data-ttu-id="138ad-211">如果 hello 項目不存在，請建立一個。</span><span class="sxs-lookup"><span data-stu-id="138ad-211">If hello element doesn't exist, create one.</span></span>
4. <span data-ttu-id="138ad-212">貼上 hello 整個複製`<UserJourney>`做為子系的 hello`<UserJourneys>`項目。</span><span class="sxs-lookup"><span data-stu-id="138ad-212">Paste hello entire copied `<UserJourney>` as a child of hello `<UserJourneys>` element.</span></span>
5. <span data-ttu-id="138ad-213">重新命名新的 hello hello 識別碼`<UserJourney>`(例如，SignUpOrSignUsingContoso)。</span><span class="sxs-lookup"><span data-stu-id="138ad-213">Rename hello ID of hello new `<UserJourney>` (for example, SignUpOrSignUsingContoso).</span></span>

### <a name="display-hello-identity-provider-button"></a><span data-ttu-id="138ad-214">顯示 hello 身分識別提供者 按鈕</span><span class="sxs-lookup"><span data-stu-id="138ad-214">Display hello identity provider button</span></span>

<span data-ttu-id="138ad-215">hello`<ClaimsProviderSelection>`項目是在註冊或登入頁面類似 tooan 身分識別提供者 按鈕。</span><span class="sxs-lookup"><span data-stu-id="138ad-215">hello `<ClaimsProviderSelection>` element is analogous tooan identity provider button on a sign-up or sign-in page.</span></span> <span data-ttu-id="138ad-216">藉由新增`<ClaimsProviderSelection>`salesforce 的項目，新的按鈕會顯示當使用者 toothis 頁面。</span><span class="sxs-lookup"><span data-stu-id="138ad-216">By adding an `<ClaimsProviderSelection>` element for Salesforce, a new button appears when a user goes toothis page.</span></span> <span data-ttu-id="138ad-217">toodisplay hello 身分識別提供者按鈕：</span><span class="sxs-lookup"><span data-stu-id="138ad-217">toodisplay hello identity provider button:</span></span>

1. <span data-ttu-id="138ad-218">在 hello`<UserJourney>`您所建立，在此找到 hello`<OrchestrationStep>`與`Order="1"`。</span><span class="sxs-lookup"><span data-stu-id="138ad-218">In hello `<UserJourney>` that you created, find hello `<OrchestrationStep>` with `Order="1"`.</span></span>
2. <span data-ttu-id="138ad-219">加入下列 XML 的 hello:</span><span class="sxs-lookup"><span data-stu-id="138ad-219">Add hello following XML:</span></span>

    ```XML
    <ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
    ```

3. <span data-ttu-id="138ad-220">設定`TargetClaimsExchangeId`tooa 邏輯值。</span><span class="sxs-lookup"><span data-stu-id="138ad-220">Set `TargetClaimsExchangeId` tooa logical value.</span></span> <span data-ttu-id="138ad-221">我們建議下列 hello 相同慣例與其他人 (例如，  *\[ClaimProviderName\]Exchange*)。</span><span class="sxs-lookup"><span data-stu-id="138ad-221">We recommend following hello same convention as others (for example, *\[ClaimProviderName\]Exchange*).</span></span>

### <a name="link-hello-identity-provider-button-tooan-action"></a><span data-ttu-id="138ad-222">連結 hello 身分識別提供者按鈕 tooan 動作</span><span class="sxs-lookup"><span data-stu-id="138ad-222">Link hello identity provider button tooan action</span></span>

<span data-ttu-id="138ad-223">既然您已備妥身分識別提供者 按鈕，請將它連結 tooan 動作。</span><span class="sxs-lookup"><span data-stu-id="138ad-223">Now that you have an identity provider button in place, link it tooan action.</span></span> <span data-ttu-id="138ad-224">在此情況下，hello 動作是 Azure AD B2C toocommunicate 與 Salesforce tooreceive SAML 權杖。</span><span class="sxs-lookup"><span data-stu-id="138ad-224">In this case, hello action is for Azure AD B2C toocommunicate with Salesforce tooreceive a SAML token.</span></span> <span data-ttu-id="138ad-225">您可以藉由連結 hello 技術設定檔的 Salesforce SAML 宣告提供者：</span><span class="sxs-lookup"><span data-stu-id="138ad-225">You can do this by linking hello technical profile for your Salesforce SAML claims provider:</span></span>

1. <span data-ttu-id="138ad-226">在 hello`<UserJourney>`節點、 尋找 hello`<OrchestrationStep>`與`Order="2"`。</span><span class="sxs-lookup"><span data-stu-id="138ad-226">In hello `<UserJourney>` node, find hello `<OrchestrationStep>` with `Order="2"`.</span></span>
2. <span data-ttu-id="138ad-227">加入下列 XML 的 hello:</span><span class="sxs-lookup"><span data-stu-id="138ad-227">Add hello following XML:</span></span>

    ```XML
    <ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="ContosoProfile" />
    ```

3. <span data-ttu-id="138ad-228">更新`Id`toohello 相同的值，是您稍早用於`TargetClaimsExchangeId`。</span><span class="sxs-lookup"><span data-stu-id="138ad-228">Update `Id` toohello same value that you used earlier for `TargetClaimsExchangeId`.</span></span>
4. <span data-ttu-id="138ad-229">更新`TechnicalProfileReferenceId`toohello `Id` hello 技術的設定檔您稍早建立 (例如，ContosoProfile)。</span><span class="sxs-lookup"><span data-stu-id="138ad-229">Update `TechnicalProfileReferenceId` toohello `Id` of hello technical profile you created earlier (for example, ContosoProfile).</span></span>

### <a name="upload-hello-updated-extension-file"></a><span data-ttu-id="138ad-230">上傳 hello 更新延伸模組檔案</span><span class="sxs-lookup"><span data-stu-id="138ad-230">Upload hello updated extension file</span></span>

<span data-ttu-id="138ad-231">您已完成修改 hello 延伸模組檔案。</span><span class="sxs-lookup"><span data-stu-id="138ad-231">You are done modifying hello extension file.</span></span> <span data-ttu-id="138ad-232">儲存並上傳這個檔案。</span><span class="sxs-lookup"><span data-stu-id="138ad-232">Save and upload this file.</span></span> <span data-ttu-id="138ad-233">請確定所有驗證都成功。</span><span class="sxs-lookup"><span data-stu-id="138ad-233">Ensure that all validations succeed.</span></span>

### <a name="update-hello-relying-party-file"></a><span data-ttu-id="138ad-234">更新 hello 信賴憑證者的合作對象檔案</span><span class="sxs-lookup"><span data-stu-id="138ad-234">Update hello relying party file</span></span>

<span data-ttu-id="138ad-235">接下來，更新 hello 信賴憑證者 (rp) 檔案來起始 hello 您所建立的使用者歷程：</span><span class="sxs-lookup"><span data-stu-id="138ad-235">Next, update hello relying party (RP) file that initiates hello user journey that you created:</span></span>

1. <span data-ttu-id="138ad-236">在您的工作目錄中建立一份 SignUpOrSignIn.xml 複本。</span><span class="sxs-lookup"><span data-stu-id="138ad-236">Make a copy of SignUpOrSignIn.xml in your working directory.</span></span> <span data-ttu-id="138ad-237">然後，將它重新命名 (例如，SignUpOrSignInWithAAD.xml)。</span><span class="sxs-lookup"><span data-stu-id="138ad-237">Then, rename it (for example, SignUpOrSignInWithAAD.xml).</span></span>
2. <span data-ttu-id="138ad-238">開啟 hello 新檔案並更新 hello`PolicyId`屬性`<TrustFrameworkPolicy>`包含唯一值。</span><span class="sxs-lookup"><span data-stu-id="138ad-238">Open hello new file and update hello `PolicyId` attribute for `<TrustFrameworkPolicy>` with a unique value.</span></span> <span data-ttu-id="138ad-239">這是原則的您 (例如，SignUpOrSignInWithAAD) hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="138ad-239">This is hello name of your policy (for example, SignUpOrSignInWithAAD).</span></span>
3. <span data-ttu-id="138ad-240">修改 hello`ReferenceId`屬性`<DefaultUserJourney>`toomatch hello `Id` hello 新使用者作業 （例如 SignUpOrSignUsingContoso） 建立。</span><span class="sxs-lookup"><span data-stu-id="138ad-240">Modify hello `ReferenceId` attribute in `<DefaultUserJourney>` toomatch hello `Id` of hello new user journey that you created (for example, SignUpOrSignUsingContoso).</span></span>
4. <span data-ttu-id="138ad-241">儲存您的變更，然後上傳 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="138ad-241">Save your changes, and then upload hello file.</span></span>

## <a name="test-and-troubleshoot"></a><span data-ttu-id="138ad-242">測試及疑難排解</span><span class="sxs-lookup"><span data-stu-id="138ad-242">Test and troubleshoot</span></span>

<span data-ttu-id="138ad-243">tootest hello 自訂原則，您只要上傳，hello Azure 入口網站中 toohello 原則 刀鋒視窗的 **立即執行**。</span><span class="sxs-lookup"><span data-stu-id="138ad-243">tootest hello custom policy that you just uploaded, in hello Azure portal, go toohello policy blade, and then click **Run now**.</span></span> <span data-ttu-id="138ad-244">如果失敗，請參閱[針對自訂原則進行疑難排解](active-directory-b2c-troubleshoot-custom.md)。</span><span class="sxs-lookup"><span data-stu-id="138ad-244">If it fails, see [Troubleshoot custom policies](active-directory-b2c-troubleshoot-custom.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="138ad-245">後續步驟</span><span class="sxs-lookup"><span data-stu-id="138ad-245">Next steps</span></span>

<span data-ttu-id="138ad-246">提供意見反應太[AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com)。</span><span class="sxs-lookup"><span data-stu-id="138ad-246">Provide feedback too[AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com).</span></span>
