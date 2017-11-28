---
title: "Azure Active Directory B2C：使用 REST API 宣告交換作為協調流程步驟 | Microsoft Docs"
description: "關於已與 API 整合之 Azure Active Directory B2C 自訂原則的主題"
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: rojasja
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/24/2017
ms.author: joroja
ms.openlocfilehash: 90a495029f48d70232ef3f99de4ea4d351395aa7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-integrate-rest-api-claims-exchanges-in-your-azure-ad-b2c-user-journey-as-an-orchestration-step"></a><span data-ttu-id="97493-103">逐步解說︰將 REST API 宣告交換整合到 Azure AD B2C 使用者旅程圖中以作為協調流程步驟</span><span class="sxs-lookup"><span data-stu-id="97493-103">Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as an orchestration step</span></span>

<span data-ttu-id="97493-104">hello 識別體驗架構 (IEF) 構成 Azure Active Directory B2C (Azure AD B2C) 可讓 hello 身分識別開發人員 toointegrate 與 rest 式 API，在使用者之旅互動。</span><span class="sxs-lookup"><span data-stu-id="97493-104">hello Identity Experience Framework (IEF) that underlies Azure Active Directory B2C (Azure AD B2C) enables hello identity developer toointegrate an interaction with a RESTful API in a user journey.</span></span>  

<span data-ttu-id="97493-105">在本逐步解說 hello 最後，將無法 toocreate 互動 RESTful 服務的 Azure AD B2C 使用者旅程。</span><span class="sxs-lookup"><span data-stu-id="97493-105">At hello end of this walkthrough, you will be able toocreate an Azure AD B2C user journey that interacts with RESTful services.</span></span>

<span data-ttu-id="97493-106">hello IEF 宣告中傳送資料，並接收回宣告中的資料。</span><span class="sxs-lookup"><span data-stu-id="97493-106">hello IEF sends data in claims and receives data back in claims.</span></span> <span data-ttu-id="97493-107">hello REST API 宣告 exchange:</span><span class="sxs-lookup"><span data-stu-id="97493-107">hello REST API claims exchange:</span></span>

- <span data-ttu-id="97493-108">可以設計成協調流程步驟。</span><span class="sxs-lookup"><span data-stu-id="97493-108">Can be designed as an orchestration step.</span></span>
- <span data-ttu-id="97493-109">可以觸發外部動作。</span><span class="sxs-lookup"><span data-stu-id="97493-109">Can trigger an external action.</span></span> <span data-ttu-id="97493-110">例如，它可以在外部資料庫中記錄一個事件。</span><span class="sxs-lookup"><span data-stu-id="97493-110">For instance, it can log an event in an external database.</span></span>
- <span data-ttu-id="97493-111">可以是使用的 toofetch 的值，然後將它儲存在 hello 使用者資料庫。</span><span class="sxs-lookup"><span data-stu-id="97493-111">Can be used toofetch a value and then store it in hello user database.</span></span>

<span data-ttu-id="97493-112">您可以使用收到 hello 宣告稍後 toochange hello 流程的執行。</span><span class="sxs-lookup"><span data-stu-id="97493-112">You can use hello received claims later toochange hello flow of execution.</span></span>

<span data-ttu-id="97493-113">您也可以設計 hello 互動身分驗證設定檔。</span><span class="sxs-lookup"><span data-stu-id="97493-113">You can also design hello interaction as a validation profile.</span></span> <span data-ttu-id="97493-114">如需詳細資訊，請參閱[逐步解說︰將 REST API 宣告交換整合到 Azure AD B2C 使用者旅程圖中以作為使用者輸入的驗證](active-directory-b2c-rest-api-validation-custom.md)。</span><span class="sxs-lookup"><span data-stu-id="97493-114">For more information, see [Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as validation on user input](active-directory-b2c-rest-api-validation-custom.md).</span></span>

<span data-ttu-id="97493-115">當使用者執行設定檔編輯時，我們想要則 hello 案例：</span><span class="sxs-lookup"><span data-stu-id="97493-115">hello scenario is that when a user performs a profile edit, we want to:</span></span>

1. <span data-ttu-id="97493-116">查閱外部系統中的 hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="97493-116">Look up hello user in an external system.</span></span>
2. <span data-ttu-id="97493-117">收到 hello 縣 （市） 在已註冊該使用者。</span><span class="sxs-lookup"><span data-stu-id="97493-117">Get hello city where that user is registered.</span></span>
3. <span data-ttu-id="97493-118">傳回當做宣告該屬性 toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="97493-118">Return that attribute toohello application as a claim.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="97493-119">必要條件</span><span class="sxs-lookup"><span data-stu-id="97493-119">Prerequisites</span></span>

- <span data-ttu-id="97493-120">Sign-up/登入中, 所述的本機帳戶的 Azure AD B2C 租用戶設定 toocomplete[入門](active-directory-b2c-get-started-custom.md)。</span><span class="sxs-lookup"><span data-stu-id="97493-120">An Azure AD B2C tenant configured toocomplete a local account sign-up/sign-in, as described in [Getting started](active-directory-b2c-get-started-custom.md).</span></span>
- <span data-ttu-id="97493-121">使用 REST API 端點 toointeract。</span><span class="sxs-lookup"><span data-stu-id="97493-121">A REST API endpoint toointeract with.</span></span> <span data-ttu-id="97493-122">本逐步解說使用簡單的 Azure 函式應用程式 Webhook 作為範例。</span><span class="sxs-lookup"><span data-stu-id="97493-122">This walkthrough uses a simple Azure function app webhook as an example.</span></span>
- <span data-ttu-id="97493-123">*建議*： 完整 hello [REST API 宣告交換逐步解說中的為每個驗證步驟](active-directory-b2c-rest-api-validation-custom.md)。</span><span class="sxs-lookup"><span data-stu-id="97493-123">*Recommended*: Complete hello [REST API claims exchange walkthrough as a validation step](active-directory-b2c-rest-api-validation-custom.md).</span></span>

## <a name="step-1-prepare-hello-rest-api-function"></a><span data-ttu-id="97493-124">步驟 1： 準備 hello REST API 函式</span><span class="sxs-lookup"><span data-stu-id="97493-124">Step 1: Prepare hello REST API function</span></span>

> [!NOTE]
> <span data-ttu-id="97493-125">安裝程式的 REST API 函式是在這篇文章 hello 範圍之外。</span><span class="sxs-lookup"><span data-stu-id="97493-125">Setup of REST API functions is outside hello scope of this article.</span></span> <span data-ttu-id="97493-126">[Azure 函數](https://docs.microsoft.com/azure/azure-functions/functions-reference)toocreate hello 雲端中的 rest 式服務提供絕佳的工具組。</span><span class="sxs-lookup"><span data-stu-id="97493-126">[Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-reference) provides an excellent toolkit toocreate RESTful services in hello cloud.</span></span>

<span data-ttu-id="97493-127">我們已將接收的宣告稱為 Azure 函式設定`email`，然後傳回 hello 宣告和`city`hello 分派值是`Redmond`。</span><span class="sxs-lookup"><span data-stu-id="97493-127">We have set up an Azure function that receives a claim called `email`, and then returns hello claim `city` with hello assigned value of `Redmond`.</span></span> <span data-ttu-id="97493-128">hello 範例 Azure 函式位於[GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples)。</span><span class="sxs-lookup"><span data-stu-id="97493-128">hello sample Azure function is on [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).</span></span>

<span data-ttu-id="97493-129">hello `userMessage` hello Azure 函式傳回的宣告是選擇性的在此內容中，而且 hello IEF 將會忽略它。</span><span class="sxs-lookup"><span data-stu-id="97493-129">hello `userMessage` claim that hello Azure function returns is optional in this context, and hello IEF will ignore it.</span></span> <span data-ttu-id="97493-130">您可以使用它的訊息傳遞 toohello 應用程式，並稍後所述 toohello 使用者。</span><span class="sxs-lookup"><span data-stu-id="97493-130">You can potentially use it as a message passed toohello application and presented toohello user later.</span></span>

```csharp
if (requestContentAsJObject.email == null)
{
    return request.CreateResponse(HttpStatusCode.BadRequest);
}

var email = ((string) requestContentAsJObject.email).ToLower();

return request.CreateResponse<ResponseContent>(
    HttpStatusCode.OK,
    new ResponseContent
    {
        version = "1.0.0",
        status = (int) HttpStatusCode.OK,
        userMessage = "User Found",
        city = "Redmond"
    },
    new JsonMediaTypeFormatter(),
    "application/json");
```

<span data-ttu-id="97493-131">Azure 的函式應用程式可容易 tooget hello 函式 URL，包括 hello 識別碼 hello 特定函式。</span><span class="sxs-lookup"><span data-stu-id="97493-131">An Azure function app makes it easy tooget hello function URL, which includes hello identifier of hello specific function.</span></span> <span data-ttu-id="97493-132">在此情況下，hello URL 是： https://wingtipb2cfuncs.azurewebsites.net/api/LookUpLoyaltyWebHook?code=MQuG7BIE3eXBaCZ/YCfY1SHabm55HEphpNLmh1OP3hdfHkvI2QwPrw==。</span><span class="sxs-lookup"><span data-stu-id="97493-132">In this case, hello URL is: https://wingtipb2cfuncs.azurewebsites.net/api/LookUpLoyaltyWebHook?code=MQuG7BIE3eXBaCZ/YCfY1SHabm55HEphpNLmh1OP3hdfHkvI2QwPrw==.</span></span> <span data-ttu-id="97493-133">您可以使用它來測試。</span><span class="sxs-lookup"><span data-stu-id="97493-133">You can use it for testing.</span></span>

## <a name="step-2-configure-hello-restful-api-claims-exchange-as-a-technical-profile-in-your-trustframeworextensionsxml-file"></a><span data-ttu-id="97493-134">步驟 2： 設定 hello RESTful API 宣告交換為技術 TrustFrameworExtensions.xml 檔案中設定檔</span><span class="sxs-lookup"><span data-stu-id="97493-134">Step 2: Configure hello RESTful API claims exchange as a technical profile in your TrustFrameworExtensions.xml file</span></span>

<span data-ttu-id="97493-135">技術的設定檔是 hello 的 hello exchange 以 hello RESTful 服務所需的完整設定。</span><span class="sxs-lookup"><span data-stu-id="97493-135">A technical profile is hello full configuration of hello exchange desired with hello RESTful service.</span></span> <span data-ttu-id="97493-136">開啟 hello TrustFrameworkExtensions.xml 檔案並加入下列 XML 程式碼片段 hello hello`<ClaimsProvider>`項目。</span><span class="sxs-lookup"><span data-stu-id="97493-136">Open hello TrustFrameworkExtensions.xml file and add hello following XML snippet inside hello `<ClaimsProvider>` element.</span></span>

> [!NOTE]
> <span data-ttu-id="97493-137">在下列 XML，RESTful 的提供者的 hello`Version=1.0.0.0`即稱為 hello 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="97493-137">In hello following XML, RESTful provider `Version=1.0.0.0` is described as hello protocol.</span></span> <span data-ttu-id="97493-138">將其視為與 hello 外部服務互動的 hello 函式。</span><span class="sxs-lookup"><span data-stu-id="97493-138">Consider it as hello function that will interact with hello external service.</span></span> <!-- TODO: A full definition of hello schema can be found...link tooRESTful Provider schema definition>-->

```XML
<ClaimsProvider>
    <DisplayName>REST APIs</DisplayName>
    <TechnicalProfiles>
        <TechnicalProfile Id="AzureFunctions-LookUpLoyaltyWebHook">
            <DisplayName>Check LookUpLoyalty Web Hook Azure Function</DisplayName>
            <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.RestfulProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
            <Metadata>
                <Item Key="ServiceUrl">https://wingtipb2cfuncs.azurewebsites.net/api/LookUpLoyaltyWebHook?code=MQuG7BIE3eXBaCZ/YCfY1SHabm55HEphpNLmh1OP3hdfHkvI2QwPrw==</Item>
                <Item Key="AuthenticationType">None</Item>
                <Item Key="SendClaimsIn">Body</Item>
            </Metadata>
            <InputClaims>
                <InputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="email" />
            </InputClaims>
            <OutputClaims>
                <OutputClaim ClaimTypeReferenceId="city" PartnerClaimType="city" />
            </OutputClaims>
            <UseTechnicalProfileForSessionManagement ReferenceId="SM-Noop" />
        </TechnicalProfile>
    </TechnicalProfiles>
</ClaimsProvider>
```

<span data-ttu-id="97493-139">hello`<InputClaims>`項目會定義會將傳送嗨 IEF toohello REST 服務的 hello 宣告。</span><span class="sxs-lookup"><span data-stu-id="97493-139">hello `<InputClaims>` element defines hello claims that will be sent from hello IEF toohello REST service.</span></span> <span data-ttu-id="97493-140">在此範例中，hello hello 宣告的內容`givenName`toohello REST 服務以傳送 hello 宣告`email`。</span><span class="sxs-lookup"><span data-stu-id="97493-140">In this example, hello contents of hello claim `givenName` will be sent toohello REST service as hello claim `email`.</span></span>  

<span data-ttu-id="97493-141">hello`<OutputClaims>`項目會定義 hello 宣告該 hello IEF 就會預期收到來自 hello REST 服務。</span><span class="sxs-lookup"><span data-stu-id="97493-141">hello `<OutputClaims>` element defines hello claims that hello IEF will expect from hello REST service.</span></span> <span data-ttu-id="97493-142">Hello 數目所接收的宣告，不論 hello IEF 將會使用僅限於識別這裡。</span><span class="sxs-lookup"><span data-stu-id="97493-142">Regardless of hello number of claims that are received, hello IEF will use only those identified here.</span></span> <span data-ttu-id="97493-143">在此範例中，宣告收到`city`將對應的 tooan IEF 宣告呼叫`city`。</span><span class="sxs-lookup"><span data-stu-id="97493-143">In this example, a claim received as `city` will be mapped tooan IEF claim called `city`.</span></span>

## <a name="step-3-add-hello-new-claim-city-toohello-schema-of-your-trustframeworkextensionsxml-file"></a><span data-ttu-id="97493-144">步驟 3： 加入 hello 新宣告`city`toohello TrustFrameworkExtensions.xml 檔案結構描述</span><span class="sxs-lookup"><span data-stu-id="97493-144">Step 3: Add hello new claim `city` toohello schema of your TrustFrameworkExtensions.xml file</span></span>

<span data-ttu-id="97493-145">hello 宣告`city`尚未定義任何地方我們的結構描述中。</span><span class="sxs-lookup"><span data-stu-id="97493-145">hello claim `city` is not yet defined anywhere in our schema.</span></span> <span data-ttu-id="97493-146">因此，加入在 hello 項目內定義`<BuildingBlocks>`。</span><span class="sxs-lookup"><span data-stu-id="97493-146">So, add a definition inside hello element `<BuildingBlocks>`.</span></span> <span data-ttu-id="97493-147">您可以找到這個 hello hello TrustFrameworkExtensions.xml 檔案開頭處的項目。</span><span class="sxs-lookup"><span data-stu-id="97493-147">You can find this element at hello beginning of hello TrustFrameworkExtensions.xml file.</span></span>

```XML
<BuildingBlocks>
    <!--hello claimtype city must be added toohello TrustFrameworkPolicy-->
    <!-- You can add new claims in hello BASE file Section III, or in hello extensions file-->
    <ClaimsSchema>
        <ClaimType Id="city">
            <DisplayName>City</DisplayName>
            <DataType>string</DataType>
            <UserHelpText>Your city</UserHelpText>
            <UserInputType>TextBox</UserInputType>
        </ClaimType>
    </ClaimsSchema>
</BuildingBlocks>
```

## <a name="step-4-include-hello-rest-service-claims-exchange-as-an-orchestration-step-in-your-profile-edit-user-journey-in-trustframeworkextensionsxml"></a><span data-ttu-id="97493-148">步驟 4： 為協調流程中的步驟設定檔編輯使用者旅程中 TrustFrameworkExtensions.xml 包含 hello REST 服務宣告交換</span><span class="sxs-lookup"><span data-stu-id="97493-148">Step 4: Include hello REST service claims exchange as an orchestration step in your profile edit user journey in TrustFrameworkExtensions.xml</span></span>

<span data-ttu-id="97493-149">將步驟加入 toohello 設定檔編輯使用者之旅，hello 使用者之後，驗證 （協調流程的步驟 1-4 hello 下列 XML 中），且 hello 使用者提供更新的 hello 設定檔資訊 （步驟 5）。</span><span class="sxs-lookup"><span data-stu-id="97493-149">Add a step toohello profile edit user journey, after hello user has been authenticated (orchestration steps 1-4 in hello following XML) and hello user has provided hello updated profile information (step 5).</span></span>

> [!NOTE]
> <span data-ttu-id="97493-150">有許多的使用案例，其中 hello REST API 呼叫可用來當作協調流程步驟。</span><span class="sxs-lookup"><span data-stu-id="97493-150">There are many use cases where hello REST API call can be used as an orchestration step.</span></span> <span data-ttu-id="97493-151">在協調流程的步驟中，它可用來當作更新 tooan 外部系統使用者順利完成的工作，像是第一次註冊之後，或為設定檔更新 tookeep 資訊同步。</span><span class="sxs-lookup"><span data-stu-id="97493-151">As an orchestration step, it can be used as an update tooan external system after a user has successfully completed a task like first-time registration, or as a profile update tookeep information synchronized.</span></span> <span data-ttu-id="97493-152">在此情況下，它是使用的 tooaugment hello 資訊之後，編輯 hello 設定檔中提供 toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="97493-152">In this case, it's used tooaugment hello information provided toohello application after hello profile edit.</span></span>

<span data-ttu-id="97493-153">複製 hello 設定檔編輯使用者之旅 XML 程式碼從 hello TrustFrameworkBase.xml tooyour TrustFrameworkExtensions.xml 檔案內 hello`<UserJourneys>`項目。</span><span class="sxs-lookup"><span data-stu-id="97493-153">Copy hello profile edit user journey XML code from hello TrustFrameworkBase.xml file tooyour TrustFrameworkExtensions.xml file inside hello `<UserJourneys>` element.</span></span> <span data-ttu-id="97493-154">請在 步驟 6 hello 修改。</span><span class="sxs-lookup"><span data-stu-id="97493-154">Then make hello modification under step 6.</span></span>

```XML
<OrchestrationStep Order="6" Type="ClaimsExchange">
    <ClaimsExchanges>
        <ClaimsExchange Id="GetLoyaltyData" TechnicalProfileReferenceId="AzureFunctions-LookUpLoyaltyWebHook" />
    </ClaimsExchanges>
</OrchestrationStep>
```

> [!IMPORTANT]
> <span data-ttu-id="97493-155">如果 hello 順序不符合您的版本，請確定您以 hello 步驟 hello 之前插入 hello 程式碼`ClaimsExchange`類型`SendClaims`。</span><span class="sxs-lookup"><span data-stu-id="97493-155">If hello order does not match your version, make sure that you insert hello code as hello step before hello `ClaimsExchange` type `SendClaims`.</span></span>

<span data-ttu-id="97493-156">hello hello 使用者作業的最終 XML 看起來應該像這樣：</span><span class="sxs-lookup"><span data-stu-id="97493-156">hello final XML for hello user journey should look like this:</span></span>

```XML
<UserJourney Id="ProfileEdit">
    <OrchestrationSteps>
        <OrchestrationStep Order="1" Type="ClaimsProviderSelection" ContentDefinitionReferenceId="api.idpselections">
            <ClaimsProviderSelections>
                <ClaimsProviderSelection TargetClaimsExchangeId="FacebookExchange" />
                <ClaimsProviderSelection TargetClaimsExchangeId="LocalAccountSigninEmailExchange" />
            </ClaimsProviderSelections>
        </OrchestrationStep>
        <OrchestrationStep Order="2" Type="ClaimsExchange">
            <ClaimsExchanges>
                <ClaimsExchange Id="FacebookExchange" TechnicalProfileReferenceId="Facebook-OAUTH" />
                <ClaimsExchange Id="LocalAccountSigninEmailExchange" TechnicalProfileReferenceId="SelfAsserted-LocalAccountSignin-Email" />
            </ClaimsExchanges>
        </OrchestrationStep>
        <OrchestrationStep Order="3" Type="ClaimsExchange">
            <Preconditions>
                <Precondition Type="ClaimEquals" ExecuteActionsIf="true">
                    <Value>authenticationSource</Value>
                    <Value>localAccountAuthentication</Value>
                    <Action>SkipThisOrchestrationStep</Action>
                </Precondition>
            </Preconditions>
            <ClaimsExchanges>
                <ClaimsExchange Id="AADUserRead" TechnicalProfileReferenceId="AAD-UserReadUsingAlternativeSecurityId" />
            </ClaimsExchanges>
        </OrchestrationStep>
        <OrchestrationStep Order="4" Type="ClaimsExchange">
            <Preconditions>
                <Precondition Type="ClaimEquals" ExecuteActionsIf="true">
                    <Value>authenticationSource</Value>
                    <Value>socialIdpAuthentication</Value>
                    <Action>SkipThisOrchestrationStep</Action>
                </Precondition>
            </Preconditions>
            <ClaimsExchanges>
                <ClaimsExchange Id="AADUserReadWithObjectId" TechnicalProfileReferenceId="AAD-UserReadUsingObjectId" />
            </ClaimsExchanges>
        </OrchestrationStep>
        <OrchestrationStep Order="5" Type="ClaimsExchange">
            <ClaimsExchanges>
                <ClaimsExchange Id="B2CUserProfileUpdateExchange" TechnicalProfileReferenceId="SelfAsserted-ProfileUpdate" />
            </ClaimsExchanges>
        </OrchestrationStep>
        <!-- Add a step 6 toohello user journey before hello JWT token is created-->
        <OrchestrationStep Order="6" Type="ClaimsExchange">
            <ClaimsExchanges>
                <ClaimsExchange Id="GetLoyaltyData" TechnicalProfileReferenceId="AzureFunctions-LookUpLoyaltyWebHook" />
            </ClaimsExchanges>
        </OrchestrationStep>
        <OrchestrationStep Order="7" Type="SendClaims" CpimIssuerTechnicalProfileReferenceId="JwtIssuer" />
    </OrchestrationSteps>
    <ClientDefinition ReferenceId="DefaultWeb" />
</UserJourney>
```

## <a name="step-5-add-hello-claim-city-tooyour-relying-party-policy-file-so-hello-claim-is-sent-tooyour-application"></a><span data-ttu-id="97493-157">步驟 5： 加入 hello 宣告`city`tooyour 信賴憑證者的合作對象原則檔案，因此會傳送 hello 宣告 tooyour 應用程式</span><span class="sxs-lookup"><span data-stu-id="97493-157">Step 5: Add hello claim `city` tooyour relying party policy file so hello claim is sent tooyour application</span></span>

<span data-ttu-id="97493-158">編輯您 ProfileEdit.xml 信賴憑證者的合作對象 (RP) 檔和修改 hello`<TechnicalProfile Id="PolicyProfile">`元素 tooadd hello 下列： `<OutputClaim ClaimTypeReferenceId="city" />`。</span><span class="sxs-lookup"><span data-stu-id="97493-158">Edit your ProfileEdit.xml relying party (RP) file and modify hello `<TechnicalProfile Id="PolicyProfile">` element tooadd hello following: `<OutputClaim ClaimTypeReferenceId="city" />`.</span></span>

<span data-ttu-id="97493-159">您將加入 hello 新宣告之後，hello 技術設定檔看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="97493-159">After you add hello new claim, hello technical profile looks like this:</span></span>

```XML
<DisplayName>PolicyProfile</DisplayName>
    <Protocol Name="OpenIdConnect" />
    <OutputClaims>
      <OutputClaim ClaimTypeReferenceId="objectId" PartnerClaimType="sub"/>
      <OutputClaim ClaimTypeReferenceId="city" />
    </OutputClaims>
    <SubjectNamingInfo ClaimType="sub" />
</TechnicalProfile>
```

## <a name="step-6-upload-your-changes-and-test"></a><span data-ttu-id="97493-160">步驟 6：上傳您的變更和測試</span><span class="sxs-lookup"><span data-stu-id="97493-160">Step 6: Upload your changes and test</span></span>

<span data-ttu-id="97493-161">覆寫 hello 現有 hello 原則版本。</span><span class="sxs-lookup"><span data-stu-id="97493-161">Overwrite hello existing versions of hello policy.</span></span>

1.  <span data-ttu-id="97493-162">(選擇性:)儲存 hello 現有版本 （下載） 的延伸模組檔案後再繼續。</span><span class="sxs-lookup"><span data-stu-id="97493-162">(Optional:) Save hello existing version (by downloading) of your extensions file before you proceed.</span></span> <span data-ttu-id="97493-163">tookeep hello 初始複雜性低，我們建議您不要上傳多個版本的 hello 延伸模組檔案。</span><span class="sxs-lookup"><span data-stu-id="97493-163">tookeep hello initial complexity low, we recommend that you do not upload multiple versions of hello extensions file.</span></span>
2.  <span data-ttu-id="97493-164">(選擇性:)藉由變更命名新版 hello 原則編輯檔案的 hello 原則識別碼 hello `PolicyId="B2C_1A_TrustFrameworkProfileEdit"`。</span><span class="sxs-lookup"><span data-stu-id="97493-164">(Optional:) Rename hello new version of hello policy ID for hello policy edit file by changing   `PolicyId="B2C_1A_TrustFrameworkProfileEdit"`.</span></span>
3.  <span data-ttu-id="97493-165">上傳 hello 延伸模組檔案。</span><span class="sxs-lookup"><span data-stu-id="97493-165">Upload hello extensions file.</span></span>
4.  <span data-ttu-id="97493-166">Hello 原則編輯 RP 檔案上傳。</span><span class="sxs-lookup"><span data-stu-id="97493-166">Upload hello policy edit RP file.</span></span>
5.  <span data-ttu-id="97493-167">使用**立即執行**tootest hello 原則。</span><span class="sxs-lookup"><span data-stu-id="97493-167">Use **Run Now** tootest hello policy.</span></span> <span data-ttu-id="97493-168">Hello IEF 檢閱 hello 語彙基元傳回 toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="97493-168">Review hello token that hello IEF returns toohello application.</span></span>

<span data-ttu-id="97493-169">如果所有項目已正確設定時，hello 權杖會包含 hello 新宣告`city`，hello 值`Redmond`。</span><span class="sxs-lookup"><span data-stu-id="97493-169">If everything is set up correctly, hello token will include hello new claim `city`, with hello value `Redmond`.</span></span>

```JSON
{
  "exp": 1493053292,
  "nbf": 1493049692,
  "ver": "1.0",
  "iss": "https://login.microsoftonline.com/f06c2fe8-709f-4030-85dc-38a4bfd9e82d/v2.0/",
  "sub": "a58e7c6c-7535-4074-93da-b0023fbaf3ac",
  "aud": "4e87c1dd-e5f5-4ac8-8368-bc6a98751b8b",
  "acr": "b2c_1a_trustframeworkprofileedit",
  "nonce": "defaultNonce",
  "iat": 1493049692,
  "auth_time": 1493049692,
  "city": "Redmond"
}
```

## <a name="next-steps"></a><span data-ttu-id="97493-170">後續步驟</span><span class="sxs-lookup"><span data-stu-id="97493-170">Next steps</span></span>

[<span data-ttu-id="97493-171">使用 REST API 來作為驗證步驟</span><span class="sxs-lookup"><span data-stu-id="97493-171">Use a REST API as a validation step</span></span>](active-directory-b2c-rest-api-validation-custom.md)

[<span data-ttu-id="97493-172">修改 hello 設定檔編輯 toogather 的其他資訊從您的使用者</span><span class="sxs-lookup"><span data-stu-id="97493-172">Modify hello profile edit toogather additional information from your users</span></span>](active-directory-b2c-create-custom-attributes-profile-edit-custom.md)
