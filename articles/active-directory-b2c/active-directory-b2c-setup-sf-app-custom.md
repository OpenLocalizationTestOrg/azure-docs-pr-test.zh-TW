---
title: "Azure Active Directory B2C︰使用自訂原則新增 Salesforce SAML 提供者 | Microsoft Docs"
description: "深入了解如何建立及管理 Azure Active Directory B2C 自訂原則。"
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
ms.openlocfilehash: 269cbd80fb6e861fa8588025eec70b6c6e2890d7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-b2c-sign-in-by-using-salesforce-accounts-via-saml"></a><span data-ttu-id="7fb54-103">Azure Active Directory B2C︰使用 Salesforce 帳戶透過 SAML 來登入</span><span class="sxs-lookup"><span data-stu-id="7fb54-103">Azure Active Directory B2C: Sign in by using Salesforce accounts via SAML</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="7fb54-104">本文將說明如何使用[自訂原則](active-directory-b2c-overview-custom.md)設定特定 Salesforce 組織的使用者登入。</span><span class="sxs-lookup"><span data-stu-id="7fb54-104">This article shows you how to use [custom policies](active-directory-b2c-overview-custom.md) to set up sign-in for users from a specific Salesforce organization.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7fb54-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="7fb54-105">Prerequisites</span></span>

### <a name="azure-ad-b2c-setup"></a><span data-ttu-id="7fb54-106">Azure AD B2C 設定</span><span class="sxs-lookup"><span data-stu-id="7fb54-106">Azure AD B2C setup</span></span>

<span data-ttu-id="7fb54-107">請確定您已完成示範如何在 Azure Active Directory B2C (Azure AD B2C) 中[開始使用自訂原則](active-directory-b2c-get-started-custom.md)的所有步驟。</span><span class="sxs-lookup"><span data-stu-id="7fb54-107">Ensure that you have completed all of the steps that show you how to [get started with custom policies](active-directory-b2c-get-started-custom.md) in Azure Active Directory B2C (Azure AD B2C).</span></span>

<span data-ttu-id="7fb54-108">其中包含：</span><span class="sxs-lookup"><span data-stu-id="7fb54-108">These include:</span></span>

* <span data-ttu-id="7fb54-109">建立 Azure AD B2C 租用戶。</span><span class="sxs-lookup"><span data-stu-id="7fb54-109">Create an Azure AD B2C tenant.</span></span>
* <span data-ttu-id="7fb54-110">建立 Azure AD B2C 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7fb54-110">Create an Azure AD B2C application.</span></span>
* <span data-ttu-id="7fb54-111">註冊兩個原則引擎應用程式。</span><span class="sxs-lookup"><span data-stu-id="7fb54-111">Register two policy engine applications.</span></span>
* <span data-ttu-id="7fb54-112">設定金鑰。</span><span class="sxs-lookup"><span data-stu-id="7fb54-112">Set up keys.</span></span>
* <span data-ttu-id="7fb54-113">設定入門套件。</span><span class="sxs-lookup"><span data-stu-id="7fb54-113">Set up the starter pack.</span></span>

### <a name="salesforce-setup"></a><span data-ttu-id="7fb54-114">Salesforce 設定</span><span class="sxs-lookup"><span data-stu-id="7fb54-114">Salesforce setup</span></span>

<span data-ttu-id="7fb54-115">在本文中，我們假設您已經完成下列作業：</span><span class="sxs-lookup"><span data-stu-id="7fb54-115">In this article, we assume that you have already done the following:</span></span>

* <span data-ttu-id="7fb54-116">註冊 Salesforce 帳戶。</span><span class="sxs-lookup"><span data-stu-id="7fb54-116">Signed up for a Salesforce account.</span></span> <span data-ttu-id="7fb54-117">您可以註冊[免費的開發人員版本帳戶](https://developer.salesforce.com/signup)。</span><span class="sxs-lookup"><span data-stu-id="7fb54-117">You can sign up for a [free Developer Edition account](https://developer.salesforce.com/signup).</span></span>
* <span data-ttu-id="7fb54-118">為您的 Salesforce 組織[設定網域](https://help.salesforce.com/articleView?id=domain_name_setup.htm&language=en_US&type=0)。</span><span class="sxs-lookup"><span data-stu-id="7fb54-118">[Set up a My Domain](https://help.salesforce.com/articleView?id=domain_name_setup.htm&language=en_US&type=0) for your Salesforce organization.</span></span>

## <a name="set-up-salesforce-so-users-can-federate"></a><span data-ttu-id="7fb54-119">設定 Salesforce，讓使用者可以建立同盟</span><span class="sxs-lookup"><span data-stu-id="7fb54-119">Set up Salesforce so users can federate</span></span>

<span data-ttu-id="7fb54-120">若要協助 Azure AD B2C 與 Salesforce 通訊，您必須取得 Salesforce 中繼資料 URL。</span><span class="sxs-lookup"><span data-stu-id="7fb54-120">To help Azure AD B2C communicate with Salesforce, you need to get the Salesforce metadata URL.</span></span>

### <a name="set-up-salesforce-as-an-identity-provider"></a><span data-ttu-id="7fb54-121">將 Salesforce 設定為識別提供者</span><span class="sxs-lookup"><span data-stu-id="7fb54-121">Set up Salesforce as an identity provider</span></span>

> [!NOTE]
> <span data-ttu-id="7fb54-122">在本文中，我們假設您使用 [Salesforce Lightning 經驗](https://developer.salesforce.com/page/Lightning_Experience_FAQ)。</span><span class="sxs-lookup"><span data-stu-id="7fb54-122">In this article, we assume you are using [Salesforce Lightning Experience](https://developer.salesforce.com/page/Lightning_Experience_FAQ).</span></span>

1. <span data-ttu-id="7fb54-123">[登入 Salesforce](https://login.salesforce.com/)。</span><span class="sxs-lookup"><span data-stu-id="7fb54-123">[Sign in to Salesforce](https://login.salesforce.com/).</span></span> 
2. <span data-ttu-id="7fb54-124">在左側功能表的 [設定] 下，展開 [身分識別]，然後按一下 [識別提供者]。</span><span class="sxs-lookup"><span data-stu-id="7fb54-124">On the left menu, under **Settings**, expand **Identity**, and then click **Identity Provider**.</span></span>
3. <span data-ttu-id="7fb54-125">按一下 [啟用識別提供者]。</span><span class="sxs-lookup"><span data-stu-id="7fb54-125">Click **Enable Identity Provider**.</span></span>
4. <span data-ttu-id="7fb54-126">在 [選取憑證] 下，選取您想要讓 Salesforce 在與 Azure AD B2C 通訊時使用的憑證。</span><span class="sxs-lookup"><span data-stu-id="7fb54-126">Under **Select the certificate**, select the certificate you want Salesforce to use to communicate with Azure AD B2C.</span></span> <span data-ttu-id="7fb54-127">(您可以使用預設憑證。)按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="7fb54-127">(You can use the default certificate.) Click **Save**.</span></span> 

### <a name="create-a-connected-app-in-salesforce"></a><span data-ttu-id="7fb54-128">在 Salesforce 中建立連線應用程式</span><span class="sxs-lookup"><span data-stu-id="7fb54-128">Create a connected app in Salesforce</span></span>

1. <span data-ttu-id="7fb54-129">在 [識別提供者] 分頁中，移至 [服務提供者]。</span><span class="sxs-lookup"><span data-stu-id="7fb54-129">On the **Identity Provider** page, go to **Service Providers**.</span></span>
2. <span data-ttu-id="7fb54-130">按一下 [現在透過連線應用程式建立服務提供者]**。**按一下這裡。</span><span class="sxs-lookup"><span data-stu-id="7fb54-130">Click **Service Providers are now created via Connected Apps. Click here.**</span></span>
3. <span data-ttu-id="7fb54-131">在 [基本資訊] 下，為連線應用程式輸入必要值。</span><span class="sxs-lookup"><span data-stu-id="7fb54-131">Under **Basic Information**,  enter the required values for your connected app.</span></span>
4. <span data-ttu-id="7fb54-132">在 [Web 應用程式設定] 下，選取 [啟用 SAML] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="7fb54-132">Under **Web App Settings**, select the **Enable SAML** check box.</span></span>
5. <span data-ttu-id="7fb54-133">在 [實體識別碼] 欄位中，輸入下列 URL。</span><span class="sxs-lookup"><span data-stu-id="7fb54-133">In the **Entity ID** field, enter the following URL.</span></span> <span data-ttu-id="7fb54-134">請確定您取代 `tenantName` 的值。</span><span class="sxs-lookup"><span data-stu-id="7fb54-134">Ensure that you replace the value for `tenantName`.</span></span>
      ```
      https://login.microsoftonline.com/te/tenantName.onmicrosoft.com/B2C_1A_TrustFrameworkBase
      ```
6. <span data-ttu-id="7fb54-135">在 [ACS URL] 欄位中，輸入下列 URL。</span><span class="sxs-lookup"><span data-stu-id="7fb54-135">In the **ACS URL** field, enter the following URL.</span></span> <span data-ttu-id="7fb54-136">請確定您取代 `tenantName` 的值。</span><span class="sxs-lookup"><span data-stu-id="7fb54-136">Ensure that you replace the value for `tenantName`.</span></span>
      ```
      https://login.microsoftonline.com/te/tenantName.onmicrosoft.com/B2C_1A_TrustFrameworkBase/samlp/sso/assertionconsumer
      ```
7. <span data-ttu-id="7fb54-137">將所有其他設定保留預設值。</span><span class="sxs-lookup"><span data-stu-id="7fb54-137">Leave the default values for all other settings.</span></span>
8. <span data-ttu-id="7fb54-138">捲動到清單底部，然後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="7fb54-138">Scroll to the bottom of the list, and then click **Save**.</span></span>

### <a name="get-the-metadata-url"></a><span data-ttu-id="7fb54-139">取得中繼資料 URL</span><span class="sxs-lookup"><span data-stu-id="7fb54-139">Get the metadata URL</span></span>

1. <span data-ttu-id="7fb54-140">在連線應用程式的概觀分頁上，按一下 [管理]。</span><span class="sxs-lookup"><span data-stu-id="7fb54-140">On the overview page of your connected app, click **Manage**.</span></span>
2. <span data-ttu-id="7fb54-141">複製**中繼資料探索端點**的值，並將其儲存。</span><span class="sxs-lookup"><span data-stu-id="7fb54-141">Copy the value for **Metadata Discovery Endpoint**, and then save it.</span></span> <span data-ttu-id="7fb54-142">您將在本文稍後使用它。</span><span class="sxs-lookup"><span data-stu-id="7fb54-142">You'll use it later in this article.</span></span>

### <a name="set-up-salesforce-users-to-federate"></a><span data-ttu-id="7fb54-143">設定 Salesforce 使用者以建立同盟</span><span class="sxs-lookup"><span data-stu-id="7fb54-143">Set up Salesforce users to federate</span></span>

1. <span data-ttu-id="7fb54-144">在連線應用程式的 [管理] 分頁上，移至 [設定檔]。</span><span class="sxs-lookup"><span data-stu-id="7fb54-144">On the **Manage** page of your connected app, go to **Profiles**.</span></span>
2. <span data-ttu-id="7fb54-145">按一下 [管理設定檔]。</span><span class="sxs-lookup"><span data-stu-id="7fb54-145">Click **Manage Profiles**.</span></span>
3. <span data-ttu-id="7fb54-146">選取您想要與 Azure AD B2C 建立同盟的設定檔 (或使用者群組)。</span><span class="sxs-lookup"><span data-stu-id="7fb54-146">Select the profiles (or groups of users) that you want to federate with Azure AD B2C.</span></span> <span data-ttu-id="7fb54-147">身為系統管理員，選取 [系統管理員] 核取方塊，以便使用您的 Salesforce 帳戶建立同盟。</span><span class="sxs-lookup"><span data-stu-id="7fb54-147">As a system administrator, select the **System Administrator** check box, so that you can federate by using your Salesforce account.</span></span>

## <a name="generate-a-signing-certificate-for-azure-ad-b2c"></a><span data-ttu-id="7fb54-148">產生 Azure AD B2C 的簽署憑證</span><span class="sxs-lookup"><span data-stu-id="7fb54-148">Generate a signing certificate for Azure AD B2C</span></span>

<span data-ttu-id="7fb54-149">傳送至 Salesforce 的要求需要 Azure AD B2C 簽署。</span><span class="sxs-lookup"><span data-stu-id="7fb54-149">Requests sent to Salesforce need to be signed by Azure AD B2C.</span></span> <span data-ttu-id="7fb54-150">若要產生簽署憑證，請開啟 Azure PowerShell，然後執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="7fb54-150">To generate a signing certificate, open Azure PowerShell, and then run the following commands.</span></span>

> [!NOTE]
> <span data-ttu-id="7fb54-151">請確定您更新前兩行的租用戶名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="7fb54-151">Make sure that you update the tenant name and password in the top two lines.</span></span>

```PowerShell
$tenantName = "<YOUR TENANT NAME>.onmicrosoft.com"
$pwdText = "<YOUR PASSWORD HERE>"

$Cert = New-SelfSignedCertificate -CertStoreLocation Cert:\CurrentUser\My -DnsName "SamlIdp.$tenantName" -Subject "B2C SAML Signing Cert" -HashAlgorithm SHA256 -KeySpec Signature -KeyLength 2048

$pwd = ConvertTo-SecureString -String $pwdText -Force -AsPlainText

Export-PfxCertificate -Cert $Cert -FilePath .\B2CSigningCert.pfx -Password $pwd
```

## <a name="add-the-saml-signing-certificate-to-azure-ad-b2c"></a><span data-ttu-id="7fb54-152">將 SAML 簽署憑證新增至 Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="7fb54-152">Add the SAML signing certificate to Azure AD B2C</span></span>

<span data-ttu-id="7fb54-153">將簽署憑證上傳至 Azure AD B2C 租用戶：</span><span class="sxs-lookup"><span data-stu-id="7fb54-153">Upload the signing certificate to your Azure AD B2C tenant:</span></span> 

1. <span data-ttu-id="7fb54-154">移至您的 Azure AD B2C 租用戶。</span><span class="sxs-lookup"><span data-stu-id="7fb54-154">Go to your Azure AD B2C tenant.</span></span> <span data-ttu-id="7fb54-155">按一下 [設定]  >  [身分識別體驗架構]  >  [原則金鑰]。</span><span class="sxs-lookup"><span data-stu-id="7fb54-155">Click **Settings** > **Identity Experience Framework** > **Policy Keys**.</span></span>
2. <span data-ttu-id="7fb54-156">按一下 [+新增]，然後：</span><span class="sxs-lookup"><span data-stu-id="7fb54-156">Click **+Add**, and then:</span></span>
    1. <span data-ttu-id="7fb54-157">按一下 [選項]  >  [上傳]。</span><span class="sxs-lookup"><span data-stu-id="7fb54-157">Click **Options** > **Upload**.</span></span>
    2. <span data-ttu-id="7fb54-158">輸入**名稱** (例如，SAMLSigningCert)。</span><span class="sxs-lookup"><span data-stu-id="7fb54-158">Enter a **Name** (for example, SAMLSigningCert).</span></span> <span data-ttu-id="7fb54-159">金鑰名稱前面會自動新增前置詞 B2C_1A_。</span><span class="sxs-lookup"><span data-stu-id="7fb54-159">The prefix *B2C_1A_* is automatically added to the name of your key.</span></span>
    3. <span data-ttu-id="7fb54-160">若要選取您的憑證，請選取 [上傳檔案控制項]。</span><span class="sxs-lookup"><span data-stu-id="7fb54-160">To select your certificate, select **upload file control**.</span></span> 
    4. <span data-ttu-id="7fb54-161">輸入您在 PowerShell 指令碼中設定的憑證密碼。</span><span class="sxs-lookup"><span data-stu-id="7fb54-161">Enter the certificate's password that you set in the PowerShell script.</span></span>
3. <span data-ttu-id="7fb54-162">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="7fb54-162">Click **Create**.</span></span>
4. <span data-ttu-id="7fb54-163">請確認您已建立金鑰 (例如，B2C_1A_SAMLSigningCert)。</span><span class="sxs-lookup"><span data-stu-id="7fb54-163">Verify that you've created a key (for example, B2C_1A_SAMLSigningCert).</span></span> <span data-ttu-id="7fb54-164">記下完整名稱 (包括 B2C_1A_)。</span><span class="sxs-lookup"><span data-stu-id="7fb54-164">Take note of the full name (including *B2C_1A_*).</span></span> <span data-ttu-id="7fb54-165">您將在原則稍後參考這個金鑰。</span><span class="sxs-lookup"><span data-stu-id="7fb54-165">You will refer to this key later in the policy.</span></span>

## <a name="create-the-salesforce-saml-claims-provider-in-your-base-policy"></a><span data-ttu-id="7fb54-166">在基底原則中建立 Salesforce SAML 宣告提供者</span><span class="sxs-lookup"><span data-stu-id="7fb54-166">Create the Salesforce SAML claims provider in your base policy</span></span>

<span data-ttu-id="7fb54-167">您需要將 Salesforce 定義為宣告提供者，使用者才能使用 Salesforce 登入。</span><span class="sxs-lookup"><span data-stu-id="7fb54-167">You need to define Salesforce as a claims provider so users can sign in by using Salesforce.</span></span> <span data-ttu-id="7fb54-168">換句話說，您需要指定將與 Azure AD B2C 通訊的端點。</span><span class="sxs-lookup"><span data-stu-id="7fb54-168">In other words, you need to specify the endpoint that Azure AD B2C will communicate with.</span></span> <span data-ttu-id="7fb54-169">此端點將提供一組宣告，由 Azure AD B2C 用來確認特定使用者已驗證。</span><span class="sxs-lookup"><span data-stu-id="7fb54-169">The endpoint will *provide* a set of *claims* that Azure AD B2C uses to verify that a specific user has authenticated.</span></span> <span data-ttu-id="7fb54-170">若要完成這個操作，您可以在原則的擴充檔案中為 Salesforce 新增 `<ClaimsProvider>`：</span><span class="sxs-lookup"><span data-stu-id="7fb54-170">To do this, add a `<ClaimsProvider>` for Salesforce in the extension file of your policy:</span></span>

1. <span data-ttu-id="7fb54-171">在您的工作目錄中開啟擴充檔案 (TrustFrameworkExtensions.xml)。</span><span class="sxs-lookup"><span data-stu-id="7fb54-171">In your working directory, open the extension file (TrustFrameworkExtensions.xml).</span></span>
2. <span data-ttu-id="7fb54-172">找出區段 `<ClaimsProviders>`。</span><span class="sxs-lookup"><span data-stu-id="7fb54-172">Find the `<ClaimsProviders>` section.</span></span> <span data-ttu-id="7fb54-173">如果不存在，請在根節點下建立。</span><span class="sxs-lookup"><span data-stu-id="7fb54-173">If it does not exist, create it under the root node.</span></span>
3. <span data-ttu-id="7fb54-174">新增 `<ClaimsProvider>`：</span><span class="sxs-lookup"><span data-stu-id="7fb54-174">Add a new `<ClaimsProvider>`:</span></span>

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

<span data-ttu-id="7fb54-175">在 `<ClaimsProvider>` 節點下：</span><span class="sxs-lookup"><span data-stu-id="7fb54-175">Under the `<ClaimsProvider>` node:</span></span>

1. <span data-ttu-id="7fb54-176">將 `<ClaimsProvider>` 的值變更為可以讓 `<Domain>` 與其他識別提供者有所區別的唯一值。</span><span class="sxs-lookup"><span data-stu-id="7fb54-176">Change the value for `<Domain>` to a unique value that distinguishes `<ClaimsProvider>` from other identity providers.</span></span>
2. <span data-ttu-id="7fb54-177">將 `<DisplayName>` 的值更新為宣告提供者的顯示名稱。</span><span class="sxs-lookup"><span data-stu-id="7fb54-177">Update the value for `<DisplayName>` to a display name for the claims provider.</span></span> <span data-ttu-id="7fb54-178">目前不使用此值。</span><span class="sxs-lookup"><span data-stu-id="7fb54-178">Currently, this value is not used.</span></span>

### <a name="update-the-technical-profile"></a><span data-ttu-id="7fb54-179">更新技術設定檔</span><span class="sxs-lookup"><span data-stu-id="7fb54-179">Update the technical profile</span></span>

<span data-ttu-id="7fb54-180">若要從 Salesforce 取得 SAML 權杖，請定義 Azure AD B2C 用來與 Azure Active Directory (Azure AD) 進行通訊的通訊協定。</span><span class="sxs-lookup"><span data-stu-id="7fb54-180">To get a SAML token from Salesforce, define the protocols that Azure AD B2C will use to communicate with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="7fb54-181">在 `<ClaimsProvider>` 的 `<TechnicalProfile>` 元素中，執行這個動作：</span><span class="sxs-lookup"><span data-stu-id="7fb54-181">Do this in the `<TechnicalProfile>` element of `<ClaimsProvider>`:</span></span>

1. <span data-ttu-id="7fb54-182">更新 `<TechnicalProfile>` 節點的識別碼。</span><span class="sxs-lookup"><span data-stu-id="7fb54-182">Update the ID of the `<TechnicalProfile>` node.</span></span> <span data-ttu-id="7fb54-183">此識別碼可讓原則的其他部分參考此技術設定檔。</span><span class="sxs-lookup"><span data-stu-id="7fb54-183">This ID is used to refer to this technical profile from other parts of the policy.</span></span>
2. <span data-ttu-id="7fb54-184">更新 `<DisplayName>` 的值。</span><span class="sxs-lookup"><span data-stu-id="7fb54-184">Update the value for `<DisplayName>`.</span></span> <span data-ttu-id="7fb54-185">這個值會顯示在登入分頁的登入按鈕上。</span><span class="sxs-lookup"><span data-stu-id="7fb54-185">This value is displayed on the sign-in button on your sign-in page.</span></span>
3. <span data-ttu-id="7fb54-186">更新 `<Description>` 的值。</span><span class="sxs-lookup"><span data-stu-id="7fb54-186">Update the value for `<Description>`.</span></span>
4. <span data-ttu-id="7fb54-187">Salesforce 使用 SAML 2.0 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="7fb54-187">Salesforce uses the SAML 2.0 protocol.</span></span> <span data-ttu-id="7fb54-188">請確認 `<Protocol>` 的值是 **SAML2**。</span><span class="sxs-lookup"><span data-stu-id="7fb54-188">Ensure that the value for `<Protocol>` is **SAML2**.</span></span>

<span data-ttu-id="7fb54-189">更新上述 XML 的 `<Metadata>` 區段，以反映特定 Salesforce 帳戶的設定。</span><span class="sxs-lookup"><span data-stu-id="7fb54-189">Update the `<Metadata>` section in the preceding XML to reflect the settings for your specific Salesforce account.</span></span> <span data-ttu-id="7fb54-190">在 XML 中，更新中繼資料值︰</span><span class="sxs-lookup"><span data-stu-id="7fb54-190">In the XML, update the metadata values:</span></span>

1. <span data-ttu-id="7fb54-191">使用您稍早複製的 Salesforce 中繼資料 URL 更新 `<Item Key="PartnerEntity">` 的值。</span><span class="sxs-lookup"><span data-stu-id="7fb54-191">Update the value of `<Item Key="PartnerEntity">` with the Salesforce metadata URL you copied earlier.</span></span> <span data-ttu-id="7fb54-192">其具備下列格式：</span><span class="sxs-lookup"><span data-stu-id="7fb54-192">It has the following format:</span></span> 

    `https://contoso-dev-ed.my.salesforce.com/.well-known/samlidp/connectedapp.xml`

2. <span data-ttu-id="7fb54-193">在 `<CryptographicKeys>` 區段中，將 `StorageReferenceId` 的執行個體值更新為簽署憑證的金鑰名稱 (例如，B2C_1A_SAMLSigningCert)。</span><span class="sxs-lookup"><span data-stu-id="7fb54-193">In the `<CryptographicKeys>` section, update the value for both instances of `StorageReferenceId` to the name of the key of your signing certificate (for example, B2C_1A_SAMLSigningCert).</span></span>

### <a name="upload-the-extension-file-for-verification"></a><span data-ttu-id="7fb54-194">上傳擴充檔案準備驗證</span><span class="sxs-lookup"><span data-stu-id="7fb54-194">Upload the extension file for verification</span></span>

<span data-ttu-id="7fb54-195">您的原則現在已設定，因此 Azure AD B2C 知道與 Salesforce 的通訊方式。</span><span class="sxs-lookup"><span data-stu-id="7fb54-195">Your policy is now configured so that Azure AD B2C knows how to communicate with Salesforce.</span></span> <span data-ttu-id="7fb54-196">嘗試上傳原則的擴充檔案，以確認到目前為止沒有任何問題。</span><span class="sxs-lookup"><span data-stu-id="7fb54-196">Try uploading the extension file of your policy, to verify that there aren't any issues so far.</span></span> <span data-ttu-id="7fb54-197">若要上傳原則的擴充檔案：</span><span class="sxs-lookup"><span data-stu-id="7fb54-197">To upload the extension file of your policy:</span></span>

1. <span data-ttu-id="7fb54-198">在 Azure AD B2C 租用戶中，移至 [所有原則] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="7fb54-198">In your Azure AD B2C tenant, go to the **All Policies** blade.</span></span>
2. <span data-ttu-id="7fb54-199">選取 [覆寫已存在的原則] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="7fb54-199">Select the **Overwrite the policy if it exists** check box.</span></span>
3. <span data-ttu-id="7fb54-200">上傳擴充檔案 (TrustFrameworkExtensions.xml)。</span><span class="sxs-lookup"><span data-stu-id="7fb54-200">Upload the extension file (TrustFrameworkExtensions.xml).</span></span> <span data-ttu-id="7fb54-201">請確定它不會驗證失敗。</span><span class="sxs-lookup"><span data-stu-id="7fb54-201">Ensure that it doesn't fail validation.</span></span>

## <a name="register-the-salesforce-saml-claims-provider-to-a-user-journey"></a><span data-ttu-id="7fb54-202">向使用者旅程圖註冊 Salesforce SAML 宣告提供者</span><span class="sxs-lookup"><span data-stu-id="7fb54-202">Register the Salesforce SAML claims provider to a user journey</span></span>

<span data-ttu-id="7fb54-203">接下來，將 Salesforce SAML 識別提供者新增至其中一個使用者旅程圖。</span><span class="sxs-lookup"><span data-stu-id="7fb54-203">Next, add the Salesforce SAML identity provider to one of your user journeys.</span></span> <span data-ttu-id="7fb54-204">目前，識別提供者已設定，但還未出現在任何使用者註冊或登入分頁中。</span><span class="sxs-lookup"><span data-stu-id="7fb54-204">At this point, the identity provider has been set up, but it’s not available on any of the user sign-up or sign-in pages.</span></span> <span data-ttu-id="7fb54-205">若要將識別提供者新增至登入分頁上，首先，建立現有範本使用者旅程圖的複本。</span><span class="sxs-lookup"><span data-stu-id="7fb54-205">To add the identity provider to a sign-in page, first, create a duplicate of an existing template user journey.</span></span> <span data-ttu-id="7fb54-206">然後修改範本，讓它也有 Azure AD 識別提供者。</span><span class="sxs-lookup"><span data-stu-id="7fb54-206">Then, modify the template so that it also has the Azure AD identity provider.</span></span>

1. <span data-ttu-id="7fb54-207">開啟原則的基本檔案 (例如，TrustFrameworkBase.xml)。</span><span class="sxs-lookup"><span data-stu-id="7fb54-207">Open the base file of your policy (for example, TrustFrameworkBase.xml).</span></span>
2. <span data-ttu-id="7fb54-208">尋找 `<UserJourneys>` 元素，然後複製含有 Id="SignUpOrSignIn" 的整個 `<UserJourney>`。</span><span class="sxs-lookup"><span data-stu-id="7fb54-208">Find the `<UserJourneys>` element, and then copy the entire `<UserJourney>` value, including Id=”SignUpOrSignIn”.</span></span>
3. <span data-ttu-id="7fb54-209">開啟擴充檔案 (例如，TrustFrameworkExtensions.xml)。</span><span class="sxs-lookup"><span data-stu-id="7fb54-209">Open the extension file (for example, TrustFrameworkExtensions.xml).</span></span> <span data-ttu-id="7fb54-210">尋找 `<UserJourneys>` 元素。</span><span class="sxs-lookup"><span data-stu-id="7fb54-210">Find the `<UserJourneys>` element.</span></span> <span data-ttu-id="7fb54-211">如果元素不存在，請建立。</span><span class="sxs-lookup"><span data-stu-id="7fb54-211">If the element doesn't exist, create one.</span></span>
4. <span data-ttu-id="7fb54-212">貼上複製的整個 `<UserJourney>` 作為 `<UserJourneys>` 元素的子元素。</span><span class="sxs-lookup"><span data-stu-id="7fb54-212">Paste the entire copied `<UserJourney>` as a child of the `<UserJourneys>` element.</span></span>
5. <span data-ttu-id="7fb54-213">重新命名新 `<UserJourney>` 的識別碼 (例如，SignUpOrSignUsingContoso)。</span><span class="sxs-lookup"><span data-stu-id="7fb54-213">Rename the ID of the new `<UserJourney>` (for example, SignUpOrSignUsingContoso).</span></span>

### <a name="display-the-identity-provider-button"></a><span data-ttu-id="7fb54-214">顯示識別提供者按鈕</span><span class="sxs-lookup"><span data-stu-id="7fb54-214">Display the identity provider button</span></span>

<span data-ttu-id="7fb54-215">`<ClaimsProviderSelection>` 元素類似於註冊或登入分頁上的識別提供者按鈕。</span><span class="sxs-lookup"><span data-stu-id="7fb54-215">The `<ClaimsProviderSelection>` element is analogous to an identity provider button on a sign-up or sign-in page.</span></span> <span data-ttu-id="7fb54-216">新增 Salesforce 的 `<ClaimsProviderSelection>` 元素後，當使用者移至此分頁時，將會出現新的按鈕。</span><span class="sxs-lookup"><span data-stu-id="7fb54-216">By adding an `<ClaimsProviderSelection>` element for Salesforce, a new button appears when a user goes to this page.</span></span> <span data-ttu-id="7fb54-217">若要顯示識別提供者按鈕：</span><span class="sxs-lookup"><span data-stu-id="7fb54-217">To display the identity provider button:</span></span>

1. <span data-ttu-id="7fb54-218">在您剛才建立的 `<UserJourney>` 中，尋找含有 `Order="1"` 的 `<OrchestrationStep>`。</span><span class="sxs-lookup"><span data-stu-id="7fb54-218">In the `<UserJourney>` that you created, find the `<OrchestrationStep>` with `Order="1"`.</span></span>
2. <span data-ttu-id="7fb54-219">新增下列 XML：</span><span class="sxs-lookup"><span data-stu-id="7fb54-219">Add the following XML:</span></span>

    ```XML
    <ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
    ```

3. <span data-ttu-id="7fb54-220">將 `TargetClaimsExchangeId` 設定為邏輯值。</span><span class="sxs-lookup"><span data-stu-id="7fb54-220">Set `TargetClaimsExchangeId` to a logical value.</span></span> <span data-ttu-id="7fb54-221">建議您與其他人一樣，遵循相同的慣例 (例如，\[ClaimProviderName\]Exchange)。</span><span class="sxs-lookup"><span data-stu-id="7fb54-221">We recommend following the same convention as others (for example, *\[ClaimProviderName\]Exchange*).</span></span>

### <a name="link-the-identity-provider-button-to-an-action"></a><span data-ttu-id="7fb54-222">將識別提供者按鈕連結至動作</span><span class="sxs-lookup"><span data-stu-id="7fb54-222">Link the identity provider button to an action</span></span>

<span data-ttu-id="7fb54-223">現在已備妥識別提供者按鈕，您需要將它連結至動作。</span><span class="sxs-lookup"><span data-stu-id="7fb54-223">Now that you have an identity provider button in place, link it to an action.</span></span> <span data-ttu-id="7fb54-224">在此案例中，動作是讓 Azure AD B2C 與 Salesforce 通訊以接收 SAML 權杖。</span><span class="sxs-lookup"><span data-stu-id="7fb54-224">In this case, the action is for Azure AD B2C to communicate with Salesforce to receive a SAML token.</span></span> <span data-ttu-id="7fb54-225">作法是連結 Salesforce SAML 宣告提供者的技術設定檔：</span><span class="sxs-lookup"><span data-stu-id="7fb54-225">You can do this by linking the technical profile for your Salesforce SAML claims provider:</span></span>

1. <span data-ttu-id="7fb54-226">在 `<UserJourney>` 節點中，尋找含有 `Order="2"` 的 `<OrchestrationStep>`。</span><span class="sxs-lookup"><span data-stu-id="7fb54-226">In the `<UserJourney>` node, find the `<OrchestrationStep>` with `Order="2"`.</span></span>
2. <span data-ttu-id="7fb54-227">新增下列 XML：</span><span class="sxs-lookup"><span data-stu-id="7fb54-227">Add the following XML:</span></span>

    ```XML
    <ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="ContosoProfile" />
    ```

3. <span data-ttu-id="7fb54-228">將 `Id` 更新為您稍早用於 `TargetClaimsExchangeId` 的相同值。</span><span class="sxs-lookup"><span data-stu-id="7fb54-228">Update `Id` to the same value that you used earlier for `TargetClaimsExchangeId`.</span></span>
4. <span data-ttu-id="7fb54-229">將 `TechnicalProfileReferenceId` 更新為您稍早建立之技術設定檔的 `Id` (例如，ContosoProfile)。</span><span class="sxs-lookup"><span data-stu-id="7fb54-229">Update `TechnicalProfileReferenceId` to the `Id` of the technical profile you created earlier (for example, ContosoProfile).</span></span>

### <a name="upload-the-updated-extension-file"></a><span data-ttu-id="7fb54-230">上傳更新的擴充檔案</span><span class="sxs-lookup"><span data-stu-id="7fb54-230">Upload the updated extension file</span></span>

<span data-ttu-id="7fb54-231">您已修改擴充檔案。</span><span class="sxs-lookup"><span data-stu-id="7fb54-231">You are done modifying the extension file.</span></span> <span data-ttu-id="7fb54-232">儲存並上傳這個檔案。</span><span class="sxs-lookup"><span data-stu-id="7fb54-232">Save and upload this file.</span></span> <span data-ttu-id="7fb54-233">請確定所有驗證都成功。</span><span class="sxs-lookup"><span data-stu-id="7fb54-233">Ensure that all validations succeed.</span></span>

### <a name="update-the-relying-party-file"></a><span data-ttu-id="7fb54-234">更新信賴憑證者檔案</span><span class="sxs-lookup"><span data-stu-id="7fb54-234">Update the relying party file</span></span>

<span data-ttu-id="7fb54-235">接下來，更新信賴憑證者 (RP) 檔案，此檔案將起始您剛才建立的使用者旅程圖：</span><span class="sxs-lookup"><span data-stu-id="7fb54-235">Next, update the relying party (RP) file that initiates the user journey that you created:</span></span>

1. <span data-ttu-id="7fb54-236">在您的工作目錄中建立一份 SignUpOrSignIn.xml 複本。</span><span class="sxs-lookup"><span data-stu-id="7fb54-236">Make a copy of SignUpOrSignIn.xml in your working directory.</span></span> <span data-ttu-id="7fb54-237">然後，將它重新命名 (例如，SignUpOrSignInWithAAD.xml)。</span><span class="sxs-lookup"><span data-stu-id="7fb54-237">Then, rename it (for example, SignUpOrSignInWithAAD.xml).</span></span>
2. <span data-ttu-id="7fb54-238">開啟新檔案，將 `<TrustFrameworkPolicy>` 的 `PolicyId` 屬性更新成唯一值。</span><span class="sxs-lookup"><span data-stu-id="7fb54-238">Open the new file and update the `PolicyId` attribute for `<TrustFrameworkPolicy>` with a unique value.</span></span> <span data-ttu-id="7fb54-239">這會成為您的原則名稱 (例如，SignUpOrSignInWithAAD)。</span><span class="sxs-lookup"><span data-stu-id="7fb54-239">This is the name of your policy (for example, SignUpOrSignInWithAAD).</span></span>
3. <span data-ttu-id="7fb54-240">修改 `<DefaultUserJourney>` 中的 `ReferenceId` 屬性，以符合您建立之新使用者旅程圖的 `Id` (例如，SignUpOrSignUsingContoso)。</span><span class="sxs-lookup"><span data-stu-id="7fb54-240">Modify the `ReferenceId` attribute in `<DefaultUserJourney>` to match the `Id` of the new user journey that you created (for example, SignUpOrSignUsingContoso).</span></span>
4. <span data-ttu-id="7fb54-241">儲存變更然後上傳檔案。</span><span class="sxs-lookup"><span data-stu-id="7fb54-241">Save your changes, and then upload the file.</span></span>

## <a name="test-and-troubleshoot"></a><span data-ttu-id="7fb54-242">測試及疑難排解</span><span class="sxs-lookup"><span data-stu-id="7fb54-242">Test and troubleshoot</span></span>

<span data-ttu-id="7fb54-243">若要測試您剛才上傳的自訂原則，在 Azure 入口網站中，移至原則刀鋒視窗，然後按一下 [立即執行]。</span><span class="sxs-lookup"><span data-stu-id="7fb54-243">To test the custom policy that you just uploaded, in the Azure portal, go to the policy blade, and then click **Run now**.</span></span> <span data-ttu-id="7fb54-244">如果失敗，請參閱[針對自訂原則進行疑難排解](active-directory-b2c-troubleshoot-custom.md)。</span><span class="sxs-lookup"><span data-stu-id="7fb54-244">If it fails, see [Troubleshoot custom policies](active-directory-b2c-troubleshoot-custom.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7fb54-245">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7fb54-245">Next steps</span></span>

<span data-ttu-id="7fb54-246">請將意見反應寄到 [AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com)。</span><span class="sxs-lookup"><span data-stu-id="7fb54-246">Provide feedback to [AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com).</span></span>
