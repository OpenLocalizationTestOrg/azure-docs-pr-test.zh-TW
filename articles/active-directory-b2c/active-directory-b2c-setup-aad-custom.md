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
ms.openlocfilehash: 6c073d70debfdc3560405955d65fa9ccaa7d8b1f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-b2c-sign-in-by-using-azure-ad-accounts"></a><span data-ttu-id="642ea-103">Azure Active Directory B2C︰使用 Azure AD 帳戶登入</span><span class="sxs-lookup"><span data-stu-id="642ea-103">Azure Active Directory B2C: Sign in by using Azure AD accounts</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="642ea-104">本文將說明如何使用[自訂原則](active-directory-b2c-overview-custom.md)讓特定 Azure Active Directory (Azure AD) 組織的使用者登入。</span><span class="sxs-lookup"><span data-stu-id="642ea-104">This article shows you how to enable sign-in for users from a specific Azure Active Directory (Azure AD) organization through the use of [custom policies](active-directory-b2c-overview-custom.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="642ea-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="642ea-105">Prerequisites</span></span>

<span data-ttu-id="642ea-106">完成[開始使用自訂原則](active-directory-b2c-get-started-custom.md)一文中的步驟。</span><span class="sxs-lookup"><span data-stu-id="642ea-106">Complete the steps in the [Getting started with custom policies](active-directory-b2c-get-started-custom.md) article.</span></span>

<span data-ttu-id="642ea-107">這些步驟包括：</span><span class="sxs-lookup"><span data-stu-id="642ea-107">These steps include:</span></span>

1. <span data-ttu-id="642ea-108">建立 Azure Active Directory B2C (Azure AD B2C) 租用戶。</span><span class="sxs-lookup"><span data-stu-id="642ea-108">Creating an Azure Active Directory B2C (Azure AD B2C) tenant.</span></span>
2. <span data-ttu-id="642ea-109">建立 Azure AD B2C 應用程式。</span><span class="sxs-lookup"><span data-stu-id="642ea-109">Creating an Azure AD B2C application.</span></span>
3. <span data-ttu-id="642ea-110">註冊兩個原則引擎應用程式。</span><span class="sxs-lookup"><span data-stu-id="642ea-110">Registering two policy-engine applications.</span></span>
4. <span data-ttu-id="642ea-111">設定金鑰。</span><span class="sxs-lookup"><span data-stu-id="642ea-111">Setting up keys.</span></span>
5. <span data-ttu-id="642ea-112">設定入門套件。</span><span class="sxs-lookup"><span data-stu-id="642ea-112">Setting up the starter pack.</span></span>

## <a name="create-an-azure-ad-app"></a><span data-ttu-id="642ea-113">建立 Azure AD 應用程式</span><span class="sxs-lookup"><span data-stu-id="642ea-113">Create an Azure AD app</span></span>

<span data-ttu-id="642ea-114">若要讓特定 Azure AD 組織的使用者登入，您需要在組織 Azure AD 租用戶內註冊應用程式。</span><span class="sxs-lookup"><span data-stu-id="642ea-114">To enable sign-in for users from a specific Azure AD organization, you need to register an application within the organizational Azure AD tenant.</span></span>

>[!NOTE]
> <span data-ttu-id="642ea-115">我們在下列指示中使用 "contoso.com" 作為組織的 Azure AD 租用戶，以及使用 "fabrikamb2c.onmicrosoft.com" 作為 Azure AD B2C 租用戶。</span><span class="sxs-lookup"><span data-stu-id="642ea-115">We use "contoso.com" for the organizational Azure AD tenant and "fabrikamb2c.onmicrosoft.com" as the Azure AD B2C tenant in the following instructions.</span></span>

1. <span data-ttu-id="642ea-116">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="642ea-116">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="642ea-117">在頂端列上，選取您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="642ea-117">On the top bar, select your account.</span></span> <span data-ttu-id="642ea-118">從 [目錄] 清單中，選擇您要註冊應用程式的組織 Azure AD 租用戶 (contoso.com)。</span><span class="sxs-lookup"><span data-stu-id="642ea-118">From the **Directory** list, choose the organizational Azure AD tenant where you want to register your application (contoso.com).</span></span>
1. <span data-ttu-id="642ea-119">選取左側窗格中的 [更多服務]，然後搜尋「應用程式註冊」。</span><span class="sxs-lookup"><span data-stu-id="642ea-119">Select **More services** in the left pane, and search for "App registrations."</span></span>
1. <span data-ttu-id="642ea-120">選取 [新增應用程式註冊]。</span><span class="sxs-lookup"><span data-stu-id="642ea-120">Select **New application registration**.</span></span>
1. <span data-ttu-id="642ea-121">輸入應用程式的名稱 (例如，`Azure AD B2C App`)。</span><span class="sxs-lookup"><span data-stu-id="642ea-121">Enter a name for your application (for example, `Azure AD B2C App`).</span></span>
1. <span data-ttu-id="642ea-122">選取 [Web 應用程式/API] 作為應用程式類型。</span><span class="sxs-lookup"><span data-stu-id="642ea-122">Select **Web app / API** for the application type.</span></span>
1. <span data-ttu-id="642ea-123">針對 [登入 URL]，輸入下列 URL，其中 `yourtenant` 由 Azure AD B2C 租用戶的名稱 (`fabrikamb2c.onmicrosoft.com`) 取代：</span><span class="sxs-lookup"><span data-stu-id="642ea-123">For **Sign-on URL**, enter the following URL, where `yourtenant` is replaced by the name of your Azure AD B2C tenant (`fabrikamb2c.onmicrosoft.com`):</span></span>

    ```
    https://login.microsoftonline.com/te/yourtenant.onmicrosoft.com/oauth2/authresp
    ```

1. <span data-ttu-id="642ea-124">儲存應用程式識別碼。</span><span class="sxs-lookup"><span data-stu-id="642ea-124">Save the application ID.</span></span>
1. <span data-ttu-id="642ea-125">選取新建立的應用程式。</span><span class="sxs-lookup"><span data-stu-id="642ea-125">Select the newly created application.</span></span>
1. <span data-ttu-id="642ea-126">在 [設定] 刀鋒視窗下，選取 [金鑰]。</span><span class="sxs-lookup"><span data-stu-id="642ea-126">Under the **Settings** blade, select **Keys**.</span></span>
1. <span data-ttu-id="642ea-127">建立新的金鑰並且儲存。</span><span class="sxs-lookup"><span data-stu-id="642ea-127">Create a new key, and save it.</span></span> <span data-ttu-id="642ea-128">您在下一節中的步驟將會用到它。</span><span class="sxs-lookup"><span data-stu-id="642ea-128">You will use it in the steps in the next section.</span></span>

## <a name="add-the-azure-ad-key-to-azure-ad-b2c"></a><span data-ttu-id="642ea-129">將 Azure AD 金鑰新增至 Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="642ea-129">Add the Azure AD key to Azure AD B2C</span></span>

<span data-ttu-id="642ea-130">您需要將 contoso.com 應用程式金鑰儲存在 Azure AD B2C 租用戶中。</span><span class="sxs-lookup"><span data-stu-id="642ea-130">You need to store the contoso.com application key in your Azure AD B2C tenant.</span></span> <span data-ttu-id="642ea-131">作法：</span><span class="sxs-lookup"><span data-stu-id="642ea-131">To do this:</span></span>
1. <span data-ttu-id="642ea-132">移至您的 Azure AD B2C 租用戶，並選取 [B2C 設定]  >  [身分識別體驗架構]  >  [原則金鑰]。</span><span class="sxs-lookup"><span data-stu-id="642ea-132">Go to your Azure AD B2C tenant, and select **B2C Settings** > **Identity Experience Framework** > **Policy Keys**.</span></span>
1. <span data-ttu-id="642ea-133">選取 [+新增]。</span><span class="sxs-lookup"><span data-stu-id="642ea-133">Select **+Add**.</span></span>
1. <span data-ttu-id="642ea-134">選取或輸入這些選項：</span><span class="sxs-lookup"><span data-stu-id="642ea-134">Select or enter these options:</span></span>
   * <span data-ttu-id="642ea-135">選取 [手動]。</span><span class="sxs-lookup"><span data-stu-id="642ea-135">Select **Manual**.</span></span>
   * <span data-ttu-id="642ea-136">針對 [名稱]，選擇與您的 Azure AD 租用戶名稱相符的名稱 (例如，`ContosoAppSecret`)。</span><span class="sxs-lookup"><span data-stu-id="642ea-136">For **Name**, choose a name that matches your Azure AD tenant name (for example, `ContosoAppSecret`).</span></span>  <span data-ttu-id="642ea-137">金鑰名稱前面會自動新增前置詞 `B2C_1A_`。</span><span class="sxs-lookup"><span data-stu-id="642ea-137">The prefix `B2C_1A_` is added automatically to the name of your key.</span></span>
   * <span data-ttu-id="642ea-138">在 [祕密] 方塊中貼上您的應用程式金鑰。</span><span class="sxs-lookup"><span data-stu-id="642ea-138">Paste your application key in the **Secret** box.</span></span>
   * <span data-ttu-id="642ea-139">選取 [簽章]。</span><span class="sxs-lookup"><span data-stu-id="642ea-139">Select **Signature**.</span></span>
1. <span data-ttu-id="642ea-140">選取 [ **建立**]。</span><span class="sxs-lookup"><span data-stu-id="642ea-140">Select **Create**.</span></span>
1. <span data-ttu-id="642ea-141">確認您已建立金鑰 `B2C_1A_ContosoAppSecret`。</span><span class="sxs-lookup"><span data-stu-id="642ea-141">Confirm that you've created the key `B2C_1A_ContosoAppSecret`.</span></span>


## <a name="add-a-claims-provider-in-your-base-policy"></a><span data-ttu-id="642ea-142">在基本原則中新增宣告提供者</span><span class="sxs-lookup"><span data-stu-id="642ea-142">Add a claims provider in your base policy</span></span>

<span data-ttu-id="642ea-143">如果想要讓使用者使用 Azure AD 登入，您需要將 Azure AD 定義為宣告提供者。</span><span class="sxs-lookup"><span data-stu-id="642ea-143">If you want users to sign in by using Azure AD, you need to define Azure AD as a claims provider.</span></span> <span data-ttu-id="642ea-144">換句話說，您需要指定將與 Azure AD B2C 通訊的端點。</span><span class="sxs-lookup"><span data-stu-id="642ea-144">In other words, you need to specify an endpoint that Azure AD B2C will communicate with.</span></span> <span data-ttu-id="642ea-145">此端點將提供一組宣告，由 Azure AD B2C 用來確認特定使用者已驗證。</span><span class="sxs-lookup"><span data-stu-id="642ea-145">The endpoint will provide a set of claims that are used by Azure AD B2C to verify that a specific user has authenticated.</span></span> 

<span data-ttu-id="642ea-146">您可以藉由將 Azure AD 新增至原則之擴充檔案中的 `<ClaimsProvider>` 節點，以將 Azure AD 定義為宣告提供者：</span><span class="sxs-lookup"><span data-stu-id="642ea-146">You can define Azure AD as a claims provider by adding Azure AD to the `<ClaimsProvider>` node in the extension file of your policy:</span></span>

1. <span data-ttu-id="642ea-147">從您的工作目錄中開啟擴充檔案 (TrustFrameworkExtensions.xml)。</span><span class="sxs-lookup"><span data-stu-id="642ea-147">Open the extension file (TrustFrameworkExtensions.xml) from your working directory.</span></span>
1. <span data-ttu-id="642ea-148">找出區段 `<ClaimsProviders>`。</span><span class="sxs-lookup"><span data-stu-id="642ea-148">Find the `<ClaimsProviders>` section.</span></span> <span data-ttu-id="642ea-149">如果不存在，請在根節點下新增。</span><span class="sxs-lookup"><span data-stu-id="642ea-149">If it does not exist, add it under the root node.</span></span>
1. <span data-ttu-id="642ea-150">新增 `<ClaimsProvider>` 節點，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="642ea-150">Add a new `<ClaimsProvider>` node as follows:</span></span>

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

1. <span data-ttu-id="642ea-151">在 `<ClaimsProvider>` 節點下，將 `<Domain>` 的值更新為可以與其他識別提供者有所區別的唯一值。</span><span class="sxs-lookup"><span data-stu-id="642ea-151">Under the `<ClaimsProvider>` node, update the value for `<Domain>` to a unique value that can be used to distinguish it from other identity providers.</span></span>
1. <span data-ttu-id="642ea-152">在 `<ClaimsProvider>` 節點下，將 `<DisplayName>` 的值更新為宣告提供者的易記名稱。</span><span class="sxs-lookup"><span data-stu-id="642ea-152">Under the `<ClaimsProvider>` node, update the value for `<DisplayName>` to a friendly name for the claims provider.</span></span> <span data-ttu-id="642ea-153">目前不使用此值。</span><span class="sxs-lookup"><span data-stu-id="642ea-153">This value is not currently used.</span></span>

### <a name="update-the-technical-profile"></a><span data-ttu-id="642ea-154">更新技術設定檔</span><span class="sxs-lookup"><span data-stu-id="642ea-154">Update the technical profile</span></span>

<span data-ttu-id="642ea-155">若要從 Azure AD 端點取得權杖，您需要定義 Azure AD B2C 應該用來與 Azure AD 進行通訊的通訊協定。</span><span class="sxs-lookup"><span data-stu-id="642ea-155">To get a token from the Azure AD endpoint, you need to define the protocols that Azure AD B2C should use to communicate with Azure AD.</span></span> <span data-ttu-id="642ea-156">這是在 `<ClaimsProvider>` 的 `<TechnicalProfile>` 元素內完成。</span><span class="sxs-lookup"><span data-stu-id="642ea-156">This is done inside the `<TechnicalProfile>` element of  `<ClaimsProvider>`.</span></span>
1. <span data-ttu-id="642ea-157">更新 `<TechnicalProfile>` 節點的識別碼。</span><span class="sxs-lookup"><span data-stu-id="642ea-157">Update the ID of the `<TechnicalProfile>` node.</span></span> <span data-ttu-id="642ea-158">此識別碼可讓原則的其他部分參考此技術設定檔。</span><span class="sxs-lookup"><span data-stu-id="642ea-158">This ID is used to refer to this technical profile from other parts of the policy.</span></span>
1. <span data-ttu-id="642ea-159">更新 `<DisplayName>` 的值。</span><span class="sxs-lookup"><span data-stu-id="642ea-159">Update the value for `<DisplayName>`.</span></span> <span data-ttu-id="642ea-160">這個值會顯示在登入畫面的登入按鈕上。</span><span class="sxs-lookup"><span data-stu-id="642ea-160">This value will be displayed on the sign-in button on your sign-in screen.</span></span>
1. <span data-ttu-id="642ea-161">更新 `<Description>` 的值。</span><span class="sxs-lookup"><span data-stu-id="642ea-161">Update the value for `<Description>`.</span></span>
1. <span data-ttu-id="642ea-162">Azure AD 使用 OpenID Connect 通訊協定，因此請確定 `<Protocol>` 是 `"OpenIdConnect"`。</span><span class="sxs-lookup"><span data-stu-id="642ea-162">Azure AD uses the OpenID Connect protocol, so ensure that the value for `<Protocol>` is `"OpenIdConnect"`.</span></span>

<span data-ttu-id="642ea-163">您必須更新稍早參考之 XML 檔案中的 `<Metadata>` 區段，以反映特定 Azure AD 租用戶的組態設定。</span><span class="sxs-lookup"><span data-stu-id="642ea-163">You need to update the `<Metadata>` section in the XML file referred to earlier to reflect the configuration settings for your specific Azure AD tenant.</span></span> <span data-ttu-id="642ea-164">在 XML 檔案中，更新中繼資料值，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="642ea-164">In the XML file, update the metadata values as follows:</span></span>

1. <span data-ttu-id="642ea-165">將 `<Item Key="METADATA">` 設定為 `https://login.windows.net/yourAzureADtenant/.well-known/openid-configuration`，其中 `yourAzureADtenant` 是您的 Azure AD 租用戶名稱 (contoso.com)。</span><span class="sxs-lookup"><span data-stu-id="642ea-165">Set `<Item Key="METADATA">` to `https://login.windows.net/yourAzureADtenant/.well-known/openid-configuration`, where `yourAzureADtenant` is your Azure AD tenant name (contoso.com).</span></span>
1. <span data-ttu-id="642ea-166">開啟瀏覽器並移至剛更新的 `METADATA` URL。</span><span class="sxs-lookup"><span data-stu-id="642ea-166">Open your browser and go to the `METADATA` URL that you just updated.</span></span>
1. <span data-ttu-id="642ea-167">在瀏覽器中，尋找 'issuer' 物件並複製其值。</span><span class="sxs-lookup"><span data-stu-id="642ea-167">In the browser, look for the 'issuer' object and copy its value.</span></span> <span data-ttu-id="642ea-168">如下所示：`https://sts.windows.net/{tenantId}/`。</span><span class="sxs-lookup"><span data-stu-id="642ea-168">It should look like the following: `https://sts.windows.net/{tenantId}/`.</span></span>
1. <span data-ttu-id="642ea-169">將 `<Item Key="ProviderName">` 的值貼到 XML 檔案中。</span><span class="sxs-lookup"><span data-stu-id="642ea-169">Paste the value for `<Item Key="ProviderName">` in the XML file.</span></span>
1. <span data-ttu-id="642ea-170">將 `<Item Key="client_id">` 設定為應用程式註冊時的應用程式識別碼。</span><span class="sxs-lookup"><span data-stu-id="642ea-170">Set `<Item Key="client_id">` to the application ID from the app registration.</span></span>
1. <span data-ttu-id="642ea-171">將 `<Item Key="IdTokenAudience">` 設定為應用程式註冊時的應用程式識別碼。</span><span class="sxs-lookup"><span data-stu-id="642ea-171">Set `<Item Key="IdTokenAudience">` to the application ID from the app registration.</span></span>
1. <span data-ttu-id="642ea-172">確定 `<Item Key="response_types">` 設定為 `id_token`。</span><span class="sxs-lookup"><span data-stu-id="642ea-172">Ensure that `<Item Key="response_types">` is set to `id_token`.</span></span>
1. <span data-ttu-id="642ea-173">確定 `<Item Key="UsePolicyInRedirectUri">` 設定為 `false`。</span><span class="sxs-lookup"><span data-stu-id="642ea-173">Ensure that `<Item Key="UsePolicyInRedirectUri">` is set to `false`.</span></span>

<span data-ttu-id="642ea-174">您也需要將您在 Azure AD B2C 租用戶中註冊的 Azure AD 祕密連結至 Azure AD `<ClaimsProvider>` 資訊：</span><span class="sxs-lookup"><span data-stu-id="642ea-174">You also need to link the Azure AD secret that you registered in your Azure AD B2C tenant to the Azure AD `<ClaimsProvider>` information:</span></span>

* <span data-ttu-id="642ea-175">在上述 XML 檔案的 `<CryptographicKeys>` 區段中，將 `StorageReferenceId` 的值更新為您定義之祕密的參考識別碼 (例如，`ContosoAppSecret`)。</span><span class="sxs-lookup"><span data-stu-id="642ea-175">In the `<CryptographicKeys>` section in the preceding XML file, update the value for `StorageReferenceId` to the reference ID of the secret that you defined (for example, `ContosoAppSecret`).</span></span>

### <a name="upload-the-extension-file-for-verification"></a><span data-ttu-id="642ea-176">上傳擴充檔案準備驗證</span><span class="sxs-lookup"><span data-stu-id="642ea-176">Upload the extension file for verification</span></span>

<span data-ttu-id="642ea-177">現在，您應該已設定原則，所以 Azure AD B2C 知道如何與 Azure AD 目錄進行通訊。</span><span class="sxs-lookup"><span data-stu-id="642ea-177">By now, you have configured your policy so that Azure AD B2C knows how to communicate with your Azure AD directory.</span></span> <span data-ttu-id="642ea-178">嘗試上傳原則的擴充檔案，這只是為了確認它到目前為止沒有任何問題。</span><span class="sxs-lookup"><span data-stu-id="642ea-178">Try uploading the extension file of your policy just to confirm that it doesn't have any issues so far.</span></span> <span data-ttu-id="642ea-179">若要這樣做：</span><span class="sxs-lookup"><span data-stu-id="642ea-179">To do so:</span></span>

1. <span data-ttu-id="642ea-180">開啟 Azure AD B2C 租用戶中的 [所有原則] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="642ea-180">Open the **All Policies** blade in your Azure AD B2C tenant.</span></span>
1. <span data-ttu-id="642ea-181">勾選 [覆寫已存在的原則] 方塊。</span><span class="sxs-lookup"><span data-stu-id="642ea-181">Check the **Overwrite the policy if it exists** box.</span></span>
1. <span data-ttu-id="642ea-182">上傳擴充檔案 (TrustFrameworkExtensions.xml)，並確定它通過驗證。</span><span class="sxs-lookup"><span data-stu-id="642ea-182">Upload the extension file (TrustFrameworkExtensions.xml), and ensure that it does not fail the validation.</span></span>

## <a name="register-the-azure-ad-claims-provider-to-a-user-journey"></a><span data-ttu-id="642ea-183">向使用者旅程圖註冊 Azure AD 宣告提供者</span><span class="sxs-lookup"><span data-stu-id="642ea-183">Register the Azure AD claims provider to a user journey</span></span>

<span data-ttu-id="642ea-184">您現在需要將 Azure AD 識別提供者新增至其中一個使用者旅程圖。</span><span class="sxs-lookup"><span data-stu-id="642ea-184">You now need to add the Azure AD identity provider to one of your user journeys.</span></span> <span data-ttu-id="642ea-185">目前，識別提供者已設定，但還未出現在任何註冊/登入畫面中。</span><span class="sxs-lookup"><span data-stu-id="642ea-185">At this point, the identity provider has been set up, but it’s not available in any of the sign-up/sign-in screens.</span></span> <span data-ttu-id="642ea-186">為了這樣做，我們將建立現有範本使用者旅程圖的複本，然後將它修改成也有 Azure AD 識別提供者：</span><span class="sxs-lookup"><span data-stu-id="642ea-186">To make it available, we will create a duplicate of an existing template user journey, and then modify it so that it also has the Azure AD identity provider:</span></span>

1. <span data-ttu-id="642ea-187">開啟原則的基本檔案 (例如，TrustFrameworkBase.xml)。</span><span class="sxs-lookup"><span data-stu-id="642ea-187">Open the base file of your policy (for example, TrustFrameworkBase.xml).</span></span>
1. <span data-ttu-id="642ea-188">尋找 `<UserJourneys>` 元素，並複製含有 `Id="SignUpOrSignIn"` 的整個 `<UserJourney>`。</span><span class="sxs-lookup"><span data-stu-id="642ea-188">Find the `<UserJourneys>` element and copy the entire `<UserJourney>` node that includes `Id="SignUpOrSignIn"`.</span></span>
1. <span data-ttu-id="642ea-189">開啟擴充檔案 (例如，TrustFrameworkExtensions.xml)，並尋找 `<UserJourneys>` 元素。</span><span class="sxs-lookup"><span data-stu-id="642ea-189">Open the extension file (for example, TrustFrameworkExtensions.xml) and find the `<UserJourneys>` element.</span></span> <span data-ttu-id="642ea-190">如果此元素不存在，請新增。</span><span class="sxs-lookup"><span data-stu-id="642ea-190">If the element doesn't exist, add one.</span></span>
1. <span data-ttu-id="642ea-191">貼上您複製的整個 `<UserJourney>` 節點作為 `<UserJourneys>` 元素的子元素。</span><span class="sxs-lookup"><span data-stu-id="642ea-191">Paste the entire `<UserJourney>` node that you copied as a child of the `<UserJourneys>` element.</span></span>
1. <span data-ttu-id="642ea-192">重新命名新使用者旅程圖的識別碼 (例如，重新命名為 `SignUpOrSignUsingContoso`)。</span><span class="sxs-lookup"><span data-stu-id="642ea-192">Rename the ID of the new user journey (for example, rename as `SignUpOrSignUsingContoso`).</span></span>

### <a name="display-the-button"></a><span data-ttu-id="642ea-193">顯示「按鈕」</span><span class="sxs-lookup"><span data-stu-id="642ea-193">Display the "button"</span></span>

<span data-ttu-id="642ea-194">`<ClaimsProviderSelection>` 元素類似於註冊/登入畫面上的識別提供者按鈕。</span><span class="sxs-lookup"><span data-stu-id="642ea-194">The `<ClaimsProviderSelection>` element is analogous to an identity provider button on a sign-up/sign-in screen.</span></span> <span data-ttu-id="642ea-195">如果您新增 Azure AD 的 `<ClaimsProviderSelection>` 元素，當使用者登陸頁面時，會出現新的按鈕。</span><span class="sxs-lookup"><span data-stu-id="642ea-195">If you add a `<ClaimsProviderSelection>` element for Azure AD, a new button shows up when a user lands on the page.</span></span> <span data-ttu-id="642ea-196">若要新增此元素：</span><span class="sxs-lookup"><span data-stu-id="642ea-196">To add this element:</span></span>

1. <span data-ttu-id="642ea-197">在您剛剛建立的使用者旅程圖中，尋找包含 `Order="1"` 的 `<OrchestrationStep>` 節點。</span><span class="sxs-lookup"><span data-stu-id="642ea-197">Find the `<OrchestrationStep>` node that includes `Order="1"` in the user journey that you just created.</span></span>
1. <span data-ttu-id="642ea-198">新增下列內容：</span><span class="sxs-lookup"><span data-stu-id="642ea-198">Add the following:</span></span>

    ```XML
    <ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
    ```

1. <span data-ttu-id="642ea-199">將 `TargetClaimsExchangeId` 設定為適當的值。</span><span class="sxs-lookup"><span data-stu-id="642ea-199">Set `TargetClaimsExchangeId` to an appropriate value.</span></span> <span data-ttu-id="642ea-200">建議您與其他人一樣，遵循相同的慣例：\[ClaimProviderName\]Exchange。</span><span class="sxs-lookup"><span data-stu-id="642ea-200">We recommend following the same convention as others: *\[ClaimProviderName\]Exchange*.</span></span>

### <a name="link-the-button-to-an-action"></a><span data-ttu-id="642ea-201">將按鈕連結至動作</span><span class="sxs-lookup"><span data-stu-id="642ea-201">Link the button to an action</span></span>

<span data-ttu-id="642ea-202">現在已備妥按鈕，您需要將它連結至動作。</span><span class="sxs-lookup"><span data-stu-id="642ea-202">Now that you have a button in place, you need to link it to an action.</span></span> <span data-ttu-id="642ea-203">在此案例中，動作是讓 Azure AD B2C 與 Azure AD 通訊以接收權杖。</span><span class="sxs-lookup"><span data-stu-id="642ea-203">The action, in this case, is for Azure AD B2C to communicate with Azure AD to receive a token.</span></span> <span data-ttu-id="642ea-204">藉由連結 Azure AD 宣告提供者的技術設定檔，將按鈕連結至動作：</span><span class="sxs-lookup"><span data-stu-id="642ea-204">Link the button to an action by linking the technical profile for your Azure AD claims provider:</span></span>

1. <span data-ttu-id="642ea-205">尋找 `<OrchestrationStep>`，它在 `<UserJourney>` 節點中包含 `Order="2"`。</span><span class="sxs-lookup"><span data-stu-id="642ea-205">Find the `<OrchestrationStep>` that includes `Order="2"` in the `<UserJourney>` node.</span></span>
1. <span data-ttu-id="642ea-206">新增下列內容：</span><span class="sxs-lookup"><span data-stu-id="642ea-206">Add the following:</span></span>

    ```XML
    <ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="ContosoProfile" />
    ```

1. <span data-ttu-id="642ea-207">將 `Id` 更新為與上一節中之 `TargetClaimsExchangeId` 相同的值。</span><span class="sxs-lookup"><span data-stu-id="642ea-207">Update `Id` to the same value as that of `TargetClaimsExchangeId` in the preceding section.</span></span>
1. <span data-ttu-id="642ea-208">將 `TechnicalProfileReferenceId` 更新為您稍早建立之技術設定檔的識別碼 (ContosoProfile)。</span><span class="sxs-lookup"><span data-stu-id="642ea-208">Update `TechnicalProfileReferenceId` to the ID of the technical profile you created earlier (ContosoProfile).</span></span>

### <a name="upload-the-updated-extension-file"></a><span data-ttu-id="642ea-209">上傳更新的擴充檔案</span><span class="sxs-lookup"><span data-stu-id="642ea-209">Upload the updated extension file</span></span>

<span data-ttu-id="642ea-210">您已修改擴充檔案。</span><span class="sxs-lookup"><span data-stu-id="642ea-210">You are done modifying the extension file.</span></span> <span data-ttu-id="642ea-211">將其儲存。</span><span class="sxs-lookup"><span data-stu-id="642ea-211">Save it.</span></span> <span data-ttu-id="642ea-212">然後上傳檔案，並確保所有驗證都成功。</span><span class="sxs-lookup"><span data-stu-id="642ea-212">Then upload the file, and ensure that all validations succeed.</span></span>

### <a name="update-the-rp-file"></a><span data-ttu-id="642ea-213">更新 RP 檔案</span><span class="sxs-lookup"><span data-stu-id="642ea-213">Update the RP file</span></span>

<span data-ttu-id="642ea-214">您現在需要更新信賴憑證者 (RP) 檔案，此檔案將起始您剛才建立的使用者旅程圖：</span><span class="sxs-lookup"><span data-stu-id="642ea-214">You now need to update the relying party (RP) file that will initiate the user journey that you just created:</span></span>

1. <span data-ttu-id="642ea-215">將 SignUpOrSignIn.xml 複製到您的工作目錄，並重新命名 (例如，將它重新命名為 SignUpOrSignInWithAAD.xml)。</span><span class="sxs-lookup"><span data-stu-id="642ea-215">Make a copy of SignUpOrSignIn.xml in your working directory, and rename it (for example, rename it to SignUpOrSignInWithAAD.xml).</span></span>
1. <span data-ttu-id="642ea-216">開啟新檔案，將 `<TrustFrameworkPolicy>` 的 `PolicyId` 屬性更新成唯一值 (例如，SignUpOrSignInWithAAD)。</span><span class="sxs-lookup"><span data-stu-id="642ea-216">Open the new file and update the `PolicyId` attribute for `<TrustFrameworkPolicy>` with a unique value (for example, SignUpOrSignInWithAAD).</span></span> <br> <span data-ttu-id="642ea-217">這會成為您的原則名稱 (例如，B2C\_1A\_SignUpOrSignInWithAAD)。</span><span class="sxs-lookup"><span data-stu-id="642ea-217">This will be the name of your policy (for example, B2C\_1A\_SignUpOrSignInWithAAD).</span></span>
1. <span data-ttu-id="642ea-218">修改 `<DefaultUserJourney>` 中的 `ReferenceId` 屬性，以符合您建立之新使用者旅程圖的識別碼 (例如，SignUpOrSignUsingContoso)。</span><span class="sxs-lookup"><span data-stu-id="642ea-218">Modify the `ReferenceId` attribute in `<DefaultUserJourney>` to match the ID of the new user journey that you created (SignUpOrSignUsingContoso).</span></span>
1. <span data-ttu-id="642ea-219">儲存變更並上傳檔案。</span><span class="sxs-lookup"><span data-stu-id="642ea-219">Save your changes, and upload the file.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="642ea-220">疑難排解</span><span class="sxs-lookup"><span data-stu-id="642ea-220">Troubleshooting</span></span>

<span data-ttu-id="642ea-221">測試您剛才上傳的自訂原則，方法是開啟其刀鋒視窗，然後按一下 [立即執行]。</span><span class="sxs-lookup"><span data-stu-id="642ea-221">Test the custom policy that you just uploaded by opening its blade and clicking **Run now**.</span></span> <span data-ttu-id="642ea-222">若要診斷問題，請參閱[疑難排解](active-directory-b2c-troubleshoot-custom.md)。</span><span class="sxs-lookup"><span data-stu-id="642ea-222">To diagnose problems, read about [troubleshooting](active-directory-b2c-troubleshoot-custom.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="642ea-223">後續步驟</span><span class="sxs-lookup"><span data-stu-id="642ea-223">Next steps</span></span>

<span data-ttu-id="642ea-224">請將意見反應寄到 [AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com)。</span><span class="sxs-lookup"><span data-stu-id="642ea-224">Provide feedback to [AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com).</span></span>
