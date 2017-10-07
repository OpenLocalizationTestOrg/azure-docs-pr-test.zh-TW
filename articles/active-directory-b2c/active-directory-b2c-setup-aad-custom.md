---
title: "Azure Active Directory B2C︰使用自訂原則新增 Azure AD 提供者 | Microsoft Docs"
description: "深入了解 Azure Active Directory B2C 自訂原則"
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 31f0dfe5-1ad0-4a25-a53b-8acc71bcea72
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/04/2017
ms.author: parakhj
ms.openlocfilehash: 9b0c32086cebc171d91da2e7bfb48136723ccd4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-sign-in-by-using-azure-ad-accounts"></a><span data-ttu-id="767ad-103">Azure Active Directory B2C︰使用 Azure AD 帳戶登入</span><span class="sxs-lookup"><span data-stu-id="767ad-103">Azure Active Directory B2C: Sign in by using Azure AD accounts</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="767ad-104">本文章向您示範如何 tooenable 登入使用者從特定的 Azure Active Directory (Azure AD) 組織透過 hello 使用[自訂原則](active-directory-b2c-overview-custom.md)。</span><span class="sxs-lookup"><span data-stu-id="767ad-104">This article shows you how tooenable sign-in for users from a specific Azure Active Directory (Azure AD) organization through hello use of [custom policies](active-directory-b2c-overview-custom.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="767ad-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="767ad-105">Prerequisites</span></span>

<span data-ttu-id="767ad-106">完整的 hello 步驟 hello[開始使用自訂原則](active-directory-b2c-get-started-custom.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="767ad-106">Complete hello steps in hello [Getting started with custom policies](active-directory-b2c-get-started-custom.md) article.</span></span>

<span data-ttu-id="767ad-107">這些步驟包括：</span><span class="sxs-lookup"><span data-stu-id="767ad-107">These steps include:</span></span>

1. <span data-ttu-id="767ad-108">建立 Azure Active Directory B2C (Azure AD B2C) 租用戶。</span><span class="sxs-lookup"><span data-stu-id="767ad-108">Creating an Azure Active Directory B2C (Azure AD B2C) tenant.</span></span>
2. <span data-ttu-id="767ad-109">建立 Azure AD B2C 應用程式。</span><span class="sxs-lookup"><span data-stu-id="767ad-109">Creating an Azure AD B2C application.</span></span>
3. <span data-ttu-id="767ad-110">註冊兩個原則引擎應用程式。</span><span class="sxs-lookup"><span data-stu-id="767ad-110">Registering two policy-engine applications.</span></span>
4. <span data-ttu-id="767ad-111">設定金鑰。</span><span class="sxs-lookup"><span data-stu-id="767ad-111">Setting up keys.</span></span>
5. <span data-ttu-id="767ad-112">設定 hello 入門套件。</span><span class="sxs-lookup"><span data-stu-id="767ad-112">Setting up hello starter pack.</span></span>

## <a name="create-an-azure-ad-app"></a><span data-ttu-id="767ad-113">建立 Azure AD 應用程式</span><span class="sxs-lookup"><span data-stu-id="767ad-113">Create an Azure AD app</span></span>

<span data-ttu-id="767ad-114">tooenable 登入的使用者從特定 Azure AD 組織中，您需要 tooregister hello 組織的 Azure AD 租用戶內的應用程式。</span><span class="sxs-lookup"><span data-stu-id="767ad-114">tooenable sign-in for users from a specific Azure AD organization, you need tooregister an application within hello organizational Azure AD tenant.</span></span>

>[!NOTE]
> <span data-ttu-id="767ad-115">我們使用"contoso.com"hello 組織的 Azure AD 租用戶和 「 fabrikamb2c.onmicrosoft.com"做為在下列指示的 hello hello Azure AD B2C 租用戶。</span><span class="sxs-lookup"><span data-stu-id="767ad-115">We use "contoso.com" for hello organizational Azure AD tenant and "fabrikamb2c.onmicrosoft.com" as hello Azure AD B2C tenant in hello following instructions.</span></span>

1. <span data-ttu-id="767ad-116">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="767ad-116">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="767ad-117">在 hello 頂端列中，選取您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="767ad-117">On hello top bar, select your account.</span></span> <span data-ttu-id="767ad-118">從 hello**目錄**清單中，選擇您想要 tooregister hello 組織的 Azure AD 租用戶應用程式 (contoso.com)。</span><span class="sxs-lookup"><span data-stu-id="767ad-118">From hello **Directory** list, choose hello organizational Azure AD tenant where you want tooregister your application (contoso.com).</span></span>
1. <span data-ttu-id="767ad-119">選取**更多服務**在 hello 左的窗格中，並搜尋 「 應用程式註冊 」。</span><span class="sxs-lookup"><span data-stu-id="767ad-119">Select **More services** in hello left pane, and search for "App registrations."</span></span>
1. <span data-ttu-id="767ad-120">選取 [新增應用程式註冊]。</span><span class="sxs-lookup"><span data-stu-id="767ad-120">Select **New application registration**.</span></span>
1. <span data-ttu-id="767ad-121">輸入應用程式的名稱 (例如，`Azure AD B2C App`)。</span><span class="sxs-lookup"><span data-stu-id="767ad-121">Enter a name for your application (for example, `Azure AD B2C App`).</span></span>
1. <span data-ttu-id="767ad-122">選取**Web 應用程式 / 應用程式開發介面**hello 應用程式類型。</span><span class="sxs-lookup"><span data-stu-id="767ad-122">Select **Web app / API** for hello application type.</span></span>
1. <span data-ttu-id="767ad-123">如**登入 URL**，輸入下列 URL，hello 其中`yourtenant`取代為您的 Azure AD B2C 租用戶的 hello 名稱 (`fabrikamb2c.onmicrosoft.com`):</span><span class="sxs-lookup"><span data-stu-id="767ad-123">For **Sign-on URL**, enter hello following URL, where `yourtenant` is replaced by hello name of your Azure AD B2C tenant (`fabrikamb2c.onmicrosoft.com`):</span></span>

    ```
    https://login.microsoftonline.com/te/yourtenant.onmicrosoft.com/oauth2/authresp
    ```

1. <span data-ttu-id="767ad-124">儲存 hello 應用程式識別碼。</span><span class="sxs-lookup"><span data-stu-id="767ad-124">Save hello application ID.</span></span>
1. <span data-ttu-id="767ad-125">選取新建立的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="767ad-125">Select hello newly created application.</span></span>
1. <span data-ttu-id="767ad-126">在 hello**設定**刀鋒視窗中，選取**金鑰**。</span><span class="sxs-lookup"><span data-stu-id="767ad-126">Under hello **Settings** blade, select **Keys**.</span></span>
1. <span data-ttu-id="767ad-127">建立新的金鑰並且儲存。</span><span class="sxs-lookup"><span data-stu-id="767ad-127">Create a new key, and save it.</span></span> <span data-ttu-id="767ad-128">您可以將在 hello hello 下一節中的步驟。</span><span class="sxs-lookup"><span data-stu-id="767ad-128">You will use it in hello steps in hello next section.</span></span>

## <a name="add-hello-azure-ad-key-tooazure-ad-b2c"></a><span data-ttu-id="767ad-129">新增金鑰 tooAzure AD B2C hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="767ad-129">Add hello Azure AD key tooAzure AD B2C</span></span>

<span data-ttu-id="767ad-130">您在 Azure AD B2C 租用戶中需要 toostore hello contoso.com 應用程式金鑰。</span><span class="sxs-lookup"><span data-stu-id="767ad-130">You need toostore hello contoso.com application key in your Azure AD B2C tenant.</span></span> <span data-ttu-id="767ad-131">toodo 這樣：</span><span class="sxs-lookup"><span data-stu-id="767ad-131">toodo this:</span></span>
1. <span data-ttu-id="767ad-132">移 tooyour Azure AD B2C 租用戶，然後選取**B2C 設定** > **身分識別體驗架構** > **原則機碼**。</span><span class="sxs-lookup"><span data-stu-id="767ad-132">Go tooyour Azure AD B2C tenant, and select **B2C Settings** > **Identity Experience Framework** > **Policy Keys**.</span></span>
1. <span data-ttu-id="767ad-133">選取 [+新增]。</span><span class="sxs-lookup"><span data-stu-id="767ad-133">Select **+Add**.</span></span>
1. <span data-ttu-id="767ad-134">選取或輸入這些選項：</span><span class="sxs-lookup"><span data-stu-id="767ad-134">Select or enter these options:</span></span>
   * <span data-ttu-id="767ad-135">選取 [手動]。</span><span class="sxs-lookup"><span data-stu-id="767ad-135">Select **Manual**.</span></span>
   * <span data-ttu-id="767ad-136">針對 [名稱]，選擇與您的 Azure AD 租用戶名稱相符的名稱 (例如，`ContosoAppSecret`)。</span><span class="sxs-lookup"><span data-stu-id="767ad-136">For **Name**, choose a name that matches your Azure AD tenant name (for example, `ContosoAppSecret`).</span></span>  <span data-ttu-id="767ad-137">hello 前置詞`B2C_1A_`會自動加入 toohello 金鑰的名稱。</span><span class="sxs-lookup"><span data-stu-id="767ad-137">hello prefix `B2C_1A_` is added automatically toohello name of your key.</span></span>
   * <span data-ttu-id="767ad-138">將應用程式金鑰貼在 hello**密碼**方塊。</span><span class="sxs-lookup"><span data-stu-id="767ad-138">Paste your application key in hello **Secret** box.</span></span>
   * <span data-ttu-id="767ad-139">選取 [簽章]。</span><span class="sxs-lookup"><span data-stu-id="767ad-139">Select **Signature**.</span></span>
1. <span data-ttu-id="767ad-140">選取 [ **建立**]。</span><span class="sxs-lookup"><span data-stu-id="767ad-140">Select **Create**.</span></span>
1. <span data-ttu-id="767ad-141">確認您已建立 hello 金鑰`B2C_1A_ContosoAppSecret`。</span><span class="sxs-lookup"><span data-stu-id="767ad-141">Confirm that you've created hello key `B2C_1A_ContosoAppSecret`.</span></span>


## <a name="add-a-claims-provider-in-your-base-policy"></a><span data-ttu-id="767ad-142">在基本原則中新增宣告提供者</span><span class="sxs-lookup"><span data-stu-id="767ad-142">Add a claims provider in your base policy</span></span>

<span data-ttu-id="767ad-143">如果您希望使用者 toosign 使用 Azure AD，您會需要 toodefine Azure AD 的宣告提供者。</span><span class="sxs-lookup"><span data-stu-id="767ad-143">If you want users toosign in by using Azure AD, you need toodefine Azure AD as a claims provider.</span></span> <span data-ttu-id="767ad-144">換句話說，您需要 toospecify Azure AD B2C 將與其通訊的端點。</span><span class="sxs-lookup"><span data-stu-id="767ad-144">In other words, you need toospecify an endpoint that Azure AD B2C will communicate with.</span></span> <span data-ttu-id="767ad-145">hello 端點會提供一組特定的使用者已驗證的 Azure AD B2C tooverify 所使用的宣告。</span><span class="sxs-lookup"><span data-stu-id="767ad-145">hello endpoint will provide a set of claims that are used by Azure AD B2C tooverify that a specific user has authenticated.</span></span> 

<span data-ttu-id="767ad-146">您可以定義 Azure AD 的宣告提供者加入 Azure AD toohello`<ClaimsProvider>`原則的 hello 延伸模組檔案中的節點：</span><span class="sxs-lookup"><span data-stu-id="767ad-146">You can define Azure AD as a claims provider by adding Azure AD toohello `<ClaimsProvider>` node in hello extension file of your policy:</span></span>

1. <span data-ttu-id="767ad-147">從您的工作目錄中開啟 hello 延伸模組檔案 (TrustFrameworkExtensions.xml)。</span><span class="sxs-lookup"><span data-stu-id="767ad-147">Open hello extension file (TrustFrameworkExtensions.xml) from your working directory.</span></span>
1. <span data-ttu-id="767ad-148">尋找 hello `<ClaimsProviders>` > 一節。</span><span class="sxs-lookup"><span data-stu-id="767ad-148">Find hello `<ClaimsProviders>` section.</span></span> <span data-ttu-id="767ad-149">如果不存在，請將它加入 hello 根節點下。</span><span class="sxs-lookup"><span data-stu-id="767ad-149">If it does not exist, add it under hello root node.</span></span>
1. <span data-ttu-id="767ad-150">新增 `<ClaimsProvider>` 節點，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="767ad-150">Add a new `<ClaimsProvider>` node as follows:</span></span>

    ```XML
    <ClaimsProvider>
        <Domain>Contoso</Domain>
        <DisplayName>Login using Contoso</DisplayName>
        <TechnicalProfiles>
            <TechnicalProfile Id="ContosoProfile">
                <DisplayName>Contoso Employee</DisplayName>
                <Description>Login with your Contoso account</Description>
                <Protocol Name="OpenIdConnect"/>
                <OutputTokenFormat>JWT</OutputTokenFormat>
                <Metadata>
                    <Item Key="METADATA">https://login.windows.net/contoso.com/.well-known/openid-configuration</Item>
                    <Item Key="ProviderName">https://sts.windows.net/00000000-0000-0000-0000-000000000000/</Item>
                    <Item Key="client_id">00000000-0000-0000-0000-000000000000</Item>
                    <Item Key="IdTokenAudience">00000000-0000-0000-0000-000000000000</Item>
                    <Item Key="response_types">id_token</Item>
                    <Item Key="UsePolicyInRedirectUri">false</Item>
                </Metadata>
                <CryptographicKeys>
                    <Key Id="client_secret" StorageReferenceId="B2C_1A_ContosoAppSecret"/>
                </CryptographicKeys>
                <OutputClaims>
                    <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="oid"/>
                    <OutputClaim ClaimTypeReferenceId="tenantId" PartnerClaimType="tid"/>
                    <OutputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="given_name" />
                    <OutputClaim ClaimTypeReferenceId="surName" PartnerClaimType="family_name" />
                    <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="name" />
                    <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="contosoAuthentication" />
                    <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="AzureADContoso" />
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

1. <span data-ttu-id="767ad-151">在 hello`<ClaimsProvider>`節點中，更新 hello 值`<Domain>`tooa 唯一值，可以是使用的 toodistinguish 它來自其他身分識別提供者。</span><span class="sxs-lookup"><span data-stu-id="767ad-151">Under hello `<ClaimsProvider>` node, update hello value for `<Domain>` tooa unique value that can be used toodistinguish it from other identity providers.</span></span>
1. <span data-ttu-id="767ad-152">在 hello`<ClaimsProvider>`節點中，更新 hello 值`<DisplayName>`hello tooa 易記名稱宣告提供者。</span><span class="sxs-lookup"><span data-stu-id="767ad-152">Under hello `<ClaimsProvider>` node, update hello value for `<DisplayName>` tooa friendly name for hello claims provider.</span></span> <span data-ttu-id="767ad-153">目前不使用此值。</span><span class="sxs-lookup"><span data-stu-id="767ad-153">This value is not currently used.</span></span>

### <a name="update-hello-technical-profile"></a><span data-ttu-id="767ad-154">更新 hello 技術設定檔</span><span class="sxs-lookup"><span data-stu-id="767ad-154">Update hello technical profile</span></span>

<span data-ttu-id="767ad-155">tooget hello Azure AD 端點中的語彙基元，您需要 Azure AD B2C，應該使用 Azure AD 使用 toocommunicate toodefine hello 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="767ad-155">tooget a token from hello Azure AD endpoint, you need toodefine hello protocols that Azure AD B2C should use toocommunicate with Azure AD.</span></span> <span data-ttu-id="767ad-156">這是內部 hello`<TechnicalProfile>`元素`<ClaimsProvider>`。</span><span class="sxs-lookup"><span data-stu-id="767ad-156">This is done inside hello `<TechnicalProfile>` element of  `<ClaimsProvider>`.</span></span>
1. <span data-ttu-id="767ad-157">更新 hello 識別碼 hello`<TechnicalProfile>`節點。</span><span class="sxs-lookup"><span data-stu-id="767ad-157">Update hello ID of hello `<TechnicalProfile>` node.</span></span> <span data-ttu-id="767ad-158">這個識別碼是使用的 toorefer toothis 技術 hello 原則的其他部分的設定檔。</span><span class="sxs-lookup"><span data-stu-id="767ad-158">This ID is used toorefer toothis technical profile from other parts of hello policy.</span></span>
1. <span data-ttu-id="767ad-159">更新 hello 值`<DisplayName>`。</span><span class="sxs-lookup"><span data-stu-id="767ad-159">Update hello value for `<DisplayName>`.</span></span> <span data-ttu-id="767ad-160">此值將會顯示 hello 登入 5d; 按鈕登入畫面上。</span><span class="sxs-lookup"><span data-stu-id="767ad-160">This value will be displayed on hello sign-in button on your sign-in screen.</span></span>
1. <span data-ttu-id="767ad-161">更新 hello 值`<Description>`。</span><span class="sxs-lookup"><span data-stu-id="767ad-161">Update hello value for `<Description>`.</span></span>
1. <span data-ttu-id="767ad-162">Azure AD 使用 hello OpenID Connect 通訊協定，因此請確定該 hello 值`<Protocol>`是`"OpenIdConnect"`。</span><span class="sxs-lookup"><span data-stu-id="767ad-162">Azure AD uses hello OpenID Connect protocol, so ensure that hello value for `<Protocol>` is `"OpenIdConnect"`.</span></span>

<span data-ttu-id="767ad-163">您需要 tooupdate hello `<Metadata>` hello XML 檔案中的區段參考 tooearlier tooreflect hello 組態設定您的特定 Azure AD 租用戶。</span><span class="sxs-lookup"><span data-stu-id="767ad-163">You need tooupdate hello `<Metadata>` section in hello XML file referred tooearlier tooreflect hello configuration settings for your specific Azure AD tenant.</span></span> <span data-ttu-id="767ad-164">在 hello XML 檔案中，更新 hello 中繼資料值，如下所示：</span><span class="sxs-lookup"><span data-stu-id="767ad-164">In hello XML file, update hello metadata values as follows:</span></span>

1. <span data-ttu-id="767ad-165">設定`<Item Key="METADATA">`太`https://login.windows.net/yourAzureADtenant/.well-known/openid-configuration`，其中`yourAzureADtenant`是您的 Azure AD 租用戶名稱 (contoso.com)。</span><span class="sxs-lookup"><span data-stu-id="767ad-165">Set `<Item Key="METADATA">` too`https://login.windows.net/yourAzureADtenant/.well-known/openid-configuration`, where `yourAzureADtenant` is your Azure AD tenant name (contoso.com).</span></span>
1. <span data-ttu-id="767ad-166">開啟您的瀏覽器並前往 toohello`METADATA`剛更新的 URL。</span><span class="sxs-lookup"><span data-stu-id="767ad-166">Open your browser and go toohello `METADATA` URL that you just updated.</span></span>
1. <span data-ttu-id="767ad-167">在 hello 瀏覽器中，尋找 hello 'issuer' 物件並將其值複製。</span><span class="sxs-lookup"><span data-stu-id="767ad-167">In hello browser, look for hello 'issuer' object and copy its value.</span></span> <span data-ttu-id="767ad-168">看起來應該像 hello 下列： `https://sts.windows.net/{tenantId}/`。</span><span class="sxs-lookup"><span data-stu-id="767ad-168">It should look like hello following: `https://sts.windows.net/{tenantId}/`.</span></span>
1. <span data-ttu-id="767ad-169">貼上 hello 值`<Item Key="ProviderName">`hello XML 檔案中。</span><span class="sxs-lookup"><span data-stu-id="767ad-169">Paste hello value for `<Item Key="ProviderName">` in hello XML file.</span></span>
1. <span data-ttu-id="767ad-170">設定`<Item Key="client_id">`toohello 從 hello 應用程式註冊的應用程式識別碼。</span><span class="sxs-lookup"><span data-stu-id="767ad-170">Set `<Item Key="client_id">` toohello application ID from hello app registration.</span></span>
1. <span data-ttu-id="767ad-171">設定`<Item Key="IdTokenAudience">`toohello 從 hello 應用程式註冊的應用程式識別碼。</span><span class="sxs-lookup"><span data-stu-id="767ad-171">Set `<Item Key="IdTokenAudience">` toohello application ID from hello app registration.</span></span>
1. <span data-ttu-id="767ad-172">請確認`<Item Key="response_types">`設定得`id_token`。</span><span class="sxs-lookup"><span data-stu-id="767ad-172">Ensure that `<Item Key="response_types">` is set too`id_token`.</span></span>
1. <span data-ttu-id="767ad-173">請確認`<Item Key="UsePolicyInRedirectUri">`設定得`false`。</span><span class="sxs-lookup"><span data-stu-id="767ad-173">Ensure that `<Item Key="UsePolicyInRedirectUri">` is set too`false`.</span></span>

<span data-ttu-id="767ad-174">您也需要您您 Azure AD B2C 租用戶 toohello Azure AD 中註冊的 toolink hello Azure AD 密碼`<ClaimsProvider>`資訊：</span><span class="sxs-lookup"><span data-stu-id="767ad-174">You also need toolink hello Azure AD secret that you registered in your Azure AD B2C tenant toohello Azure AD `<ClaimsProvider>` information:</span></span>

* <span data-ttu-id="767ad-175">在 hello `<CryptographicKeys>` hello 前面 XML 檔案中區段中，更新 hello 值`StorageReferenceId`toohello 參考識別碼所定義的 hello 密碼 (比方說， `ContosoAppSecret`)。</span><span class="sxs-lookup"><span data-stu-id="767ad-175">In hello `<CryptographicKeys>` section in hello preceding XML file, update hello value for `StorageReferenceId` toohello reference ID of hello secret that you defined (for example, `ContosoAppSecret`).</span></span>

### <a name="upload-hello-extension-file-for-verification"></a><span data-ttu-id="767ad-176">上傳 hello 進行驗證的延伸模組檔案</span><span class="sxs-lookup"><span data-stu-id="767ad-176">Upload hello extension file for verification</span></span>

<span data-ttu-id="767ad-177">現在，您已設定您的原則，讓 Azure AD B2C 知道如何與 Azure AD 目錄 toocommunicate。</span><span class="sxs-lookup"><span data-stu-id="767ad-177">By now, you have configured your policy so that Azure AD B2C knows how toocommunicate with your Azure AD directory.</span></span> <span data-ttu-id="767ad-178">嘗試上傳它不會有任何問題到目前為止您原則只 tooconfirm hello 延伸模組檔案。</span><span class="sxs-lookup"><span data-stu-id="767ad-178">Try uploading hello extension file of your policy just tooconfirm that it doesn't have any issues so far.</span></span> <span data-ttu-id="767ad-179">toodo 因此：</span><span class="sxs-lookup"><span data-stu-id="767ad-179">toodo so:</span></span>

1. <span data-ttu-id="767ad-180">開啟 hello**所有原則**刀鋒視窗，您的 Azure AD B2C 租用戶中。</span><span class="sxs-lookup"><span data-stu-id="767ad-180">Open hello **All Policies** blade in your Azure AD B2C tenant.</span></span>
1. <span data-ttu-id="767ad-181">檢查 hello**如果存在的話，請覆寫 hello 原則**方塊。</span><span class="sxs-lookup"><span data-stu-id="767ad-181">Check hello **Overwrite hello policy if it exists** box.</span></span>
1. <span data-ttu-id="767ad-182">上傳 hello 延伸模組檔案 (TrustFrameworkExtensions.xml)，並確保不導致 hello 驗證失敗。</span><span class="sxs-lookup"><span data-stu-id="767ad-182">Upload hello extension file (TrustFrameworkExtensions.xml), and ensure that it does not fail hello validation.</span></span>

## <a name="register-hello-azure-ad-claims-provider-tooa-user-journey"></a><span data-ttu-id="767ad-183">註冊 hello Azure AD 的宣告提供者 tooa 使用者旅程</span><span class="sxs-lookup"><span data-stu-id="767ad-183">Register hello Azure AD claims provider tooa user journey</span></span>

<span data-ttu-id="767ad-184">您現在需要 tooadd hello Azure AD 身分識別提供者 tooone 的使用者皆。</span><span class="sxs-lookup"><span data-stu-id="767ad-184">You now need tooadd hello Azure AD identity provider tooone of your user journeys.</span></span> <span data-ttu-id="767ad-185">此時，hello 身分識別提供者已設定，但不是可在任何 hello sign-up/登入畫面。</span><span class="sxs-lookup"><span data-stu-id="767ad-185">At this point, hello identity provider has been set up, but it’s not available in any of hello sign-up/sign-in screens.</span></span> <span data-ttu-id="767ad-186">toomake 可用，我們將建立的現有的範本使用者作業，複製並修改它，讓它也有 hello Azure AD 身分識別提供者：</span><span class="sxs-lookup"><span data-stu-id="767ad-186">toomake it available, we will create a duplicate of an existing template user journey, and then modify it so that it also has hello Azure AD identity provider:</span></span>

1. <span data-ttu-id="767ad-187">開啟 hello 原則 (例如，TrustFrameworkBase.xml) 的基底的檔案。</span><span class="sxs-lookup"><span data-stu-id="767ad-187">Open hello base file of your policy (for example, TrustFrameworkBase.xml).</span></span>
1. <span data-ttu-id="767ad-188">尋找 hello`<UserJourneys>`整個項目，並複製 hello`<UserJourney>`節點包含`Id="SignUpOrSignIn"`。</span><span class="sxs-lookup"><span data-stu-id="767ad-188">Find hello `<UserJourneys>` element and copy hello entire `<UserJourney>` node that includes `Id="SignUpOrSignIn"`.</span></span>
1. <span data-ttu-id="767ad-189">開啟 hello 延伸模組檔案 (例如，TrustFrameworkExtensions.xml)，並尋找 hello`<UserJourneys>`項目。</span><span class="sxs-lookup"><span data-stu-id="767ad-189">Open hello extension file (for example, TrustFrameworkExtensions.xml) and find hello `<UserJourneys>` element.</span></span> <span data-ttu-id="767ad-190">如果 hello 項目不存在，請加入一個參考。</span><span class="sxs-lookup"><span data-stu-id="767ad-190">If hello element doesn't exist, add one.</span></span>
1. <span data-ttu-id="767ad-191">貼上 hello 整個`<UserJourney>`您複製 hello 的子系的節點`<UserJourneys>`項目。</span><span class="sxs-lookup"><span data-stu-id="767ad-191">Paste hello entire `<UserJourney>` node that you copied as a child of hello `<UserJourneys>` element.</span></span>
1. <span data-ttu-id="767ad-192">重新命名的新使用者旅程 hello hello 識別碼 (例如，重新命名為`SignUpOrSignUsingContoso`)。</span><span class="sxs-lookup"><span data-stu-id="767ad-192">Rename hello ID of hello new user journey (for example, rename as `SignUpOrSignUsingContoso`).</span></span>

### <a name="display-hello-button"></a><span data-ttu-id="767ad-193">顯示 hello 「 按鈕 」</span><span class="sxs-lookup"><span data-stu-id="767ad-193">Display hello "button"</span></span>

<span data-ttu-id="767ad-194">hello`<ClaimsProviderSelection>`項目是 sign-up/登入畫面上的類似 tooan 身分識別提供者 按鈕。</span><span class="sxs-lookup"><span data-stu-id="767ad-194">hello `<ClaimsProviderSelection>` element is analogous tooan identity provider button on a sign-up/sign-in screen.</span></span> <span data-ttu-id="767ad-195">如果您將加入`<ClaimsProviderSelection>`Azure AD 的項目，新的按鈕顯示落在 hello 頁面上的使用者。</span><span class="sxs-lookup"><span data-stu-id="767ad-195">If you add a `<ClaimsProviderSelection>` element for Azure AD, a new button shows up when a user lands on hello page.</span></span> <span data-ttu-id="767ad-196">tooadd 這個項目：</span><span class="sxs-lookup"><span data-stu-id="767ad-196">tooadd this element:</span></span>

1. <span data-ttu-id="767ad-197">尋找 hello`<OrchestrationStep>`節點包含`Order="1"`hello 您剛才建立的使用者歷程中。</span><span class="sxs-lookup"><span data-stu-id="767ad-197">Find hello `<OrchestrationStep>` node that includes `Order="1"` in hello user journey that you just created.</span></span>
1. <span data-ttu-id="767ad-198">加入下列 hello:</span><span class="sxs-lookup"><span data-stu-id="767ad-198">Add hello following:</span></span>

    ```XML
    <ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
    ```

1. <span data-ttu-id="767ad-199">設定`TargetClaimsExchangeId`tooan 適當的值。</span><span class="sxs-lookup"><span data-stu-id="767ad-199">Set `TargetClaimsExchangeId` tooan appropriate value.</span></span> <span data-ttu-id="767ad-200">我們建議下列 hello 相同慣例與其他人：  *\[ClaimProviderName\]Exchange*。</span><span class="sxs-lookup"><span data-stu-id="767ad-200">We recommend following hello same convention as others: *\[ClaimProviderName\]Exchange*.</span></span>

### <a name="link-hello-button-tooan-action"></a><span data-ttu-id="767ad-201">連結 hello 按鈕 tooan 動作</span><span class="sxs-lookup"><span data-stu-id="767ad-201">Link hello button tooan action</span></span>

<span data-ttu-id="767ad-202">既然您已備妥 按鈕，您需要 toolink 它 tooan 動作。</span><span class="sxs-lookup"><span data-stu-id="767ad-202">Now that you have a button in place, you need toolink it tooan action.</span></span> <span data-ttu-id="767ad-203">hello 動作，在此情況下，為 Azure AD B2C toocommunicate 與 Azure AD tooreceive 語彙基元。</span><span class="sxs-lookup"><span data-stu-id="767ad-203">hello action, in this case, is for Azure AD B2C toocommunicate with Azure AD tooreceive a token.</span></span> <span data-ttu-id="767ad-204">連結 hello 按鈕 tooan 動作連結的 Azure AD 的宣告提供者的 hello 技術設定檔：</span><span class="sxs-lookup"><span data-stu-id="767ad-204">Link hello button tooan action by linking hello technical profile for your Azure AD claims provider:</span></span>

1. <span data-ttu-id="767ad-205">尋找 hello`<OrchestrationStep>`包含`Order="2"`在 hello`<UserJourney>`節點。</span><span class="sxs-lookup"><span data-stu-id="767ad-205">Find hello `<OrchestrationStep>` that includes `Order="2"` in hello `<UserJourney>` node.</span></span>
1. <span data-ttu-id="767ad-206">加入下列 hello:</span><span class="sxs-lookup"><span data-stu-id="767ad-206">Add hello following:</span></span>

    ```XML
    <ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="ContosoProfile" />
    ```

1. <span data-ttu-id="767ad-207">更新`Id`toohello 相同值的`TargetClaimsExchangeId`hello 前面一節中。</span><span class="sxs-lookup"><span data-stu-id="767ad-207">Update `Id` toohello same value as that of `TargetClaimsExchangeId` in hello preceding section.</span></span>
1. <span data-ttu-id="767ad-208">更新`TechnicalProfileReferenceId`toohello 識別碼 hello 技術分析您稍早建立 (ContosoProfile)。</span><span class="sxs-lookup"><span data-stu-id="767ad-208">Update `TechnicalProfileReferenceId` toohello ID of hello technical profile you created earlier (ContosoProfile).</span></span>

### <a name="upload-hello-updated-extension-file"></a><span data-ttu-id="767ad-209">上傳 hello 更新延伸模組檔案</span><span class="sxs-lookup"><span data-stu-id="767ad-209">Upload hello updated extension file</span></span>

<span data-ttu-id="767ad-210">您已完成修改 hello 延伸模組檔案。</span><span class="sxs-lookup"><span data-stu-id="767ad-210">You are done modifying hello extension file.</span></span> <span data-ttu-id="767ad-211">將其儲存。</span><span class="sxs-lookup"><span data-stu-id="767ad-211">Save it.</span></span> <span data-ttu-id="767ad-212">然後上傳 hello 檔案，並確保所有驗證都成功。</span><span class="sxs-lookup"><span data-stu-id="767ad-212">Then upload hello file, and ensure that all validations succeed.</span></span>

### <a name="update-hello-rp-file"></a><span data-ttu-id="767ad-213">更新 hello RP 檔案</span><span class="sxs-lookup"><span data-stu-id="767ad-213">Update hello RP file</span></span>

<span data-ttu-id="767ad-214">您現在需要 tooupdate hello 信賴憑證者 (rp) 檔案將會起始 hello 您剛才建立的使用者歷程：</span><span class="sxs-lookup"><span data-stu-id="767ad-214">You now need tooupdate hello relying party (RP) file that will initiate hello user journey that you just created:</span></span>

1. <span data-ttu-id="767ad-215">在您的工作目錄中建立一份 SignUpOrSignIn.xml，並將它重新命名 （例如，將它重新命名 tooSignUpOrSignInWithAAD.xml）。</span><span class="sxs-lookup"><span data-stu-id="767ad-215">Make a copy of SignUpOrSignIn.xml in your working directory, and rename it (for example, rename it tooSignUpOrSignInWithAAD.xml).</span></span>
1. <span data-ttu-id="767ad-216">開啟 hello 新檔案並更新 hello`PolicyId`屬性`<TrustFrameworkPolicy>`包含唯一值 (例如，SignUpOrSignInWithAAD)。</span><span class="sxs-lookup"><span data-stu-id="767ad-216">Open hello new file and update hello `PolicyId` attribute for `<TrustFrameworkPolicy>` with a unique value (for example, SignUpOrSignInWithAAD).</span></span> <br> <span data-ttu-id="767ad-217">這將是原則的 hello 名稱 (例如，B2C\_1A\_SignUpOrSignInWithAAD)。</span><span class="sxs-lookup"><span data-stu-id="767ad-217">This will be hello name of your policy (for example, B2C\_1A\_SignUpOrSignInWithAAD).</span></span>
1. <span data-ttu-id="767ad-218">修改 hello`ReferenceId`屬性`<DefaultUserJourney>`hello 建立 (SignUpOrSignUsingContoso) 的新使用者旅程 toomatch hello 識別碼。</span><span class="sxs-lookup"><span data-stu-id="767ad-218">Modify hello `ReferenceId` attribute in `<DefaultUserJourney>` toomatch hello ID of hello new user journey that you created (SignUpOrSignUsingContoso).</span></span>
1. <span data-ttu-id="767ad-219">儲存您的變更，並上傳 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="767ad-219">Save your changes, and upload hello file.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="767ad-220">疑難排解</span><span class="sxs-lookup"><span data-stu-id="767ad-220">Troubleshooting</span></span>

<span data-ttu-id="767ad-221">測試 hello 剛剛上傳藉由開啟其刀鋒視窗中按的自訂原則**立即執行**。</span><span class="sxs-lookup"><span data-stu-id="767ad-221">Test hello custom policy that you just uploaded by opening its blade and clicking **Run now**.</span></span> <span data-ttu-id="767ad-222">toodiagnose 問題、 閱讀[疑難排解](active-directory-b2c-troubleshoot-custom.md)。</span><span class="sxs-lookup"><span data-stu-id="767ad-222">toodiagnose problems, read about [troubleshooting](active-directory-b2c-troubleshoot-custom.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="767ad-223">後續步驟</span><span class="sxs-lookup"><span data-stu-id="767ad-223">Next steps</span></span>

<span data-ttu-id="767ad-224">提供意見反應太[AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com)。</span><span class="sxs-lookup"><span data-stu-id="767ad-224">Provide feedback too[AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com).</span></span>
