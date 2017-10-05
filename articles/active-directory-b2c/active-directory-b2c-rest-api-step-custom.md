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
ms.openlocfilehash: dc319c97e64e55861b84cc3943667418077a05d8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="walkthrough-integrate-rest-api-claims-exchanges-in-your-azure-ad-b2c-user-journey-as-an-orchestration-step"></a><span data-ttu-id="9f819-103">逐步解說︰將 REST API 宣告交換整合到 Azure AD B2C 使用者旅程圖中以作為協調流程步驟</span><span class="sxs-lookup"><span data-stu-id="9f819-103">Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as an orchestration step</span></span>

<span data-ttu-id="9f819-104">構成 Azure Active Directory B2C (Azure AD B2C) 基礎的識別體驗架構 (IEF)，可讓身分識別開發人員於使用者旅程圖中整合與 RESTful API 的互動。</span><span class="sxs-lookup"><span data-stu-id="9f819-104">The Identity Experience Framework (IEF) that underlies Azure Active Directory B2C (Azure AD B2C) enables the identity developer to integrate an interaction with a RESTful API in a user journey.</span></span>  

<span data-ttu-id="9f819-105">在本逐步解說結束時，您將能建立與 RESTful 服務互動的 Azure AD B2C 使用者旅程圖。</span><span class="sxs-lookup"><span data-stu-id="9f819-105">At the end of this walkthrough, you will be able to create an Azure AD B2C user journey that interacts with RESTful services.</span></span>

<span data-ttu-id="9f819-106">IEF 會在宣告中傳送資料，並在宣告中收到傳回的資料。</span><span class="sxs-lookup"><span data-stu-id="9f819-106">The IEF sends data in claims and receives data back in claims.</span></span> <span data-ttu-id="9f819-107">REST API 宣告交換：</span><span class="sxs-lookup"><span data-stu-id="9f819-107">The REST API claims exchange:</span></span>

- <span data-ttu-id="9f819-108">可以設計成協調流程步驟。</span><span class="sxs-lookup"><span data-stu-id="9f819-108">Can be designed as an orchestration step.</span></span>
- <span data-ttu-id="9f819-109">可以觸發外部動作。</span><span class="sxs-lookup"><span data-stu-id="9f819-109">Can trigger an external action.</span></span> <span data-ttu-id="9f819-110">例如，它可以在外部資料庫中記錄一個事件。</span><span class="sxs-lookup"><span data-stu-id="9f819-110">For instance, it can log an event in an external database.</span></span>
- <span data-ttu-id="9f819-111">可用來擷取值，然後將它存放在使用者資料庫中。</span><span class="sxs-lookup"><span data-stu-id="9f819-111">Can be used to fetch a value and then store it in the user database.</span></span>

<span data-ttu-id="9f819-112">您稍後可以使用接收的宣告來變更執行流程。</span><span class="sxs-lookup"><span data-stu-id="9f819-112">You can use the received claims later to change the flow of execution.</span></span>

<span data-ttu-id="9f819-113">您也可以將互動設計成驗證設定檔。</span><span class="sxs-lookup"><span data-stu-id="9f819-113">You can also design the interaction as a validation profile.</span></span> <span data-ttu-id="9f819-114">如需詳細資訊，請參閱[逐步解說︰將 REST API 宣告交換整合到 Azure AD B2C 使用者旅程圖中以作為使用者輸入的驗證](active-directory-b2c-rest-api-validation-custom.md)。</span><span class="sxs-lookup"><span data-stu-id="9f819-114">For more information, see [Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as validation on user input](active-directory-b2c-rest-api-validation-custom.md).</span></span>

<span data-ttu-id="9f819-115">有個案例是，當使用者執行設定檔編輯時，我們想要：</span><span class="sxs-lookup"><span data-stu-id="9f819-115">The scenario is that when a user performs a profile edit, we want to:</span></span>

1. <span data-ttu-id="9f819-116">查閱外部系統中的使用者。</span><span class="sxs-lookup"><span data-stu-id="9f819-116">Look up the user in an external system.</span></span>
2. <span data-ttu-id="9f819-117">取得註冊該使用者的城市。</span><span class="sxs-lookup"><span data-stu-id="9f819-117">Get the city where that user is registered.</span></span>
3. <span data-ttu-id="9f819-118">以宣告形式將該屬性傳回應用程式。</span><span class="sxs-lookup"><span data-stu-id="9f819-118">Return that attribute to the application as a claim.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9f819-119">必要條件</span><span class="sxs-lookup"><span data-stu-id="9f819-119">Prerequisites</span></span>

- <span data-ttu-id="9f819-120">如[開始使用](active-directory-b2c-get-started-custom.md)所述，設定為完成本機帳戶註冊/登入的 Azure AD B2C 租用戶。</span><span class="sxs-lookup"><span data-stu-id="9f819-120">An Azure AD B2C tenant configured to complete a local account sign-up/sign-in, as described in [Getting started](active-directory-b2c-get-started-custom.md).</span></span>
- <span data-ttu-id="9f819-121">要互動的 REST API 端點。</span><span class="sxs-lookup"><span data-stu-id="9f819-121">A REST API endpoint to interact with.</span></span> <span data-ttu-id="9f819-122">本逐步解說使用簡單的 Azure 函式應用程式 Webhook 作為範例。</span><span class="sxs-lookup"><span data-stu-id="9f819-122">This walkthrough uses a simple Azure function app webhook as an example.</span></span>
- <span data-ttu-id="9f819-123">*建議*︰完成 [REST API 宣告交換逐步解說以作為驗證步驟](active-directory-b2c-rest-api-validation-custom.md)。</span><span class="sxs-lookup"><span data-stu-id="9f819-123">*Recommended*: Complete the [REST API claims exchange walkthrough as a validation step](active-directory-b2c-rest-api-validation-custom.md).</span></span>

## <a name="step-1-prepare-the-rest-api-function"></a><span data-ttu-id="9f819-124">步驟 1：準備 REST API 函式</span><span class="sxs-lookup"><span data-stu-id="9f819-124">Step 1: Prepare the REST API function</span></span>

> [!NOTE]
> <span data-ttu-id="9f819-125">REST API 函式的設定不在本文討論範圍內。</span><span class="sxs-lookup"><span data-stu-id="9f819-125">Setup of REST API functions is outside the scope of this article.</span></span> <span data-ttu-id="9f819-126">[Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-reference) 提供了絕佳的工具組，供您在雲端建立 RESTful 服務。</span><span class="sxs-lookup"><span data-stu-id="9f819-126">[Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-reference) provides an excellent toolkit to create RESTful services in the cloud.</span></span>

<span data-ttu-id="9f819-127">我們設定了 Azure 函式來接收名為 `email` 的宣告，然後傳回指派值為 `Redmond` 的宣告 `city`。</span><span class="sxs-lookup"><span data-stu-id="9f819-127">We have set up an Azure function that receives a claim called `email`, and then returns the claim `city` with the assigned value of `Redmond`.</span></span> <span data-ttu-id="9f819-128">範例 Azure 函式位於 [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples) 上。</span><span class="sxs-lookup"><span data-stu-id="9f819-128">The sample Azure function is on [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).</span></span>

<span data-ttu-id="9f819-129">在此內容中，Azure 函式所傳回的 `userMessage` 宣告是選擇性的，IEF 將予以略過。</span><span class="sxs-lookup"><span data-stu-id="9f819-129">The `userMessage` claim that the Azure function returns is optional in this context, and the IEF will ignore it.</span></span> <span data-ttu-id="9f819-130">您可以選擇使用它作為訊息，以便稍後傳遞給應用程式並向使用者呈現。</span><span class="sxs-lookup"><span data-stu-id="9f819-130">You can potentially use it as a message passed to the application and presented to the user later.</span></span>

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

<span data-ttu-id="9f819-131">Azure 函式應用程式可讓您輕鬆地取得函式 URL，此 URL 中包含特定函式的識別碼。</span><span class="sxs-lookup"><span data-stu-id="9f819-131">An Azure function app makes it easy to get the function URL, which includes the identifier of the specific function.</span></span> <span data-ttu-id="9f819-132">在此案例中，URL 是︰https://wingtipb2cfuncs.azurewebsites.net/api/LookUpLoyaltyWebHook?code=MQuG7BIE3eXBaCZ/YCfY1SHabm55HEphpNLmh1OP3hdfHkvI2QwPrw==。</span><span class="sxs-lookup"><span data-stu-id="9f819-132">In this case, the URL is: https://wingtipb2cfuncs.azurewebsites.net/api/LookUpLoyaltyWebHook?code=MQuG7BIE3eXBaCZ/YCfY1SHabm55HEphpNLmh1OP3hdfHkvI2QwPrw==.</span></span> <span data-ttu-id="9f819-133">您可以使用它來測試。</span><span class="sxs-lookup"><span data-stu-id="9f819-133">You can use it for testing.</span></span>

## <a name="step-2-configure-the-restful-api-claims-exchange-as-a-technical-profile-in-your-trustframeworextensionsxml-file"></a><span data-ttu-id="9f819-134">步驟 2：在 TrustFrameworExtensions.xml 檔案中，將 RESTful API 宣告交換設為技術設定檔</span><span class="sxs-lookup"><span data-stu-id="9f819-134">Step 2: Configure the RESTful API claims exchange as a technical profile in your TrustFrameworExtensions.xml file</span></span>

<span data-ttu-id="9f819-135">技術設定檔是 RESTful 服務所需之交換的完整設定。</span><span class="sxs-lookup"><span data-stu-id="9f819-135">A technical profile is the full configuration of the exchange desired with the RESTful service.</span></span> <span data-ttu-id="9f819-136">開啟 TrustFrameworkExtensions.xml 檔案，然後在 `<ClaimsProvider>` 元素內加入下列 XML 程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="9f819-136">Open the TrustFrameworkExtensions.xml file and add the following XML snippet inside the `<ClaimsProvider>` element.</span></span>

> [!NOTE]
> <span data-ttu-id="9f819-137">在下列 XML 中，會將 RESTful 提供者 `Version=1.0.0.0` 描述為通訊協定。</span><span class="sxs-lookup"><span data-stu-id="9f819-137">In the following XML, RESTful provider `Version=1.0.0.0` is described as the protocol.</span></span> <span data-ttu-id="9f819-138">請將它視為要與外部服務互動的函式。</span><span class="sxs-lookup"><span data-stu-id="9f819-138">Consider it as the function that will interact with the external service.</span></span> <!-- TODO: A full definition of the schema can be found...link to RESTful Provider schema definition>-->

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

<span data-ttu-id="9f819-139">`<InputClaims>` 元素會定義將從 IEF 傳送至 REST 服務的宣告。</span><span class="sxs-lookup"><span data-stu-id="9f819-139">The `<InputClaims>` element defines the claims that will be sent from the IEF to the REST service.</span></span> <span data-ttu-id="9f819-140">在此範例中，會將 `givenName` 宣告的內容傳送至 REST 服務以作為宣告 `email`。</span><span class="sxs-lookup"><span data-stu-id="9f819-140">In this example, the contents of the claim `givenName` will be sent to the REST service as the claim `email`.</span></span>  

<span data-ttu-id="9f819-141">`<OutputClaims>` 元素會定義 IEF 預期要從 REST 服務收到的宣告。</span><span class="sxs-lookup"><span data-stu-id="9f819-141">The `<OutputClaims>` element defines the claims that the IEF will expect from the REST service.</span></span> <span data-ttu-id="9f819-142">不論收到多少宣告，IEF 只會使用這裡所識別的宣告。</span><span class="sxs-lookup"><span data-stu-id="9f819-142">Regardless of the number of claims that are received, the IEF will use only those identified here.</span></span> <span data-ttu-id="9f819-143">在此範例中，以 `city` 形式收到的宣告會對應到名為 `city` 的 IEF 宣告。</span><span class="sxs-lookup"><span data-stu-id="9f819-143">In this example, a claim received as `city` will be mapped to an IEF claim called `city`.</span></span>

## <a name="step-3-add-the-new-claim-city-to-the-schema-of-your-trustframeworkextensionsxml-file"></a><span data-ttu-id="9f819-144">步驟 3：將新的宣告 `city` 新增至 TrustFrameworkExtensions.xml 檔案的結構描述</span><span class="sxs-lookup"><span data-stu-id="9f819-144">Step 3: Add the new claim `city` to the schema of your TrustFrameworkExtensions.xml file</span></span>

<span data-ttu-id="9f819-145">宣告 `city` 尚未在結構描述的其他地方加以定義。</span><span class="sxs-lookup"><span data-stu-id="9f819-145">The claim `city` is not yet defined anywhere in our schema.</span></span> <span data-ttu-id="9f819-146">因此，請在元素 `<BuildingBlocks>` 內部新增定義。</span><span class="sxs-lookup"><span data-stu-id="9f819-146">So, add a definition inside the element `<BuildingBlocks>`.</span></span> <span data-ttu-id="9f819-147">您可以在 TrustFrameworkExtensions.xml 檔案開頭處找到此元素。</span><span class="sxs-lookup"><span data-stu-id="9f819-147">You can find this element at the beginning of the TrustFrameworkExtensions.xml file.</span></span>

```XML
<BuildingBlocks>
    <!--The claimtype city must be added to the TrustFrameworkPolicy-->
    <!-- You can add new claims in the BASE file Section III, or in the extensions file-->
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

## <a name="step-4-include-the-rest-service-claims-exchange-as-an-orchestration-step-in-your-profile-edit-user-journey-in-trustframeworkextensionsxml"></a><span data-ttu-id="9f819-148">步驟 4：在 TrustFrameworkExtensions.xml 的設定檔編輯使用者旅程圖中，將 REST 服務宣告交換納入為協調流程步驟</span><span class="sxs-lookup"><span data-stu-id="9f819-148">Step 4: Include the REST service claims exchange as an orchestration step in your profile edit user journey in TrustFrameworkExtensions.xml</span></span>

<span data-ttu-id="9f819-149">在使用者通過驗證之後新增設定檔編輯使用者旅程圖的步驟 (下列 XML 中的協調流程步驟 1-4)，而且使用者已提供更新的設定檔資訊 (步驟 5)。</span><span class="sxs-lookup"><span data-stu-id="9f819-149">Add a step to the profile edit user journey, after the user has been authenticated (orchestration steps 1-4 in the following XML) and the user has provided the updated profile information (step 5).</span></span>

> [!NOTE]
> <span data-ttu-id="9f819-150">有許多使用案例都可將 REST API 呼叫用來作為協調流程步驟。</span><span class="sxs-lookup"><span data-stu-id="9f819-150">There are many use cases where the REST API call can be used as an orchestration step.</span></span> <span data-ttu-id="9f819-151">作為協調流程步驟，它可在使用者成功完成工作 (例如首次註冊) 後作為外部系統的更新，或作為設定檔更新以讓資訊保持同步。</span><span class="sxs-lookup"><span data-stu-id="9f819-151">As an orchestration step, it can be used as an update to an external system after a user has successfully completed a task like first-time registration, or as a profile update to keep information synchronized.</span></span> <span data-ttu-id="9f819-152">在此情況下，它會用來加強設定檔編輯之後提供給應用程式的資訊。</span><span class="sxs-lookup"><span data-stu-id="9f819-152">In this case, it's used to augment the information provided to the application after the profile edit.</span></span>

<span data-ttu-id="9f819-153">將設定檔編輯使用者旅程圖 XML 程式碼從 TrustFrameworkBase.xml 檔案複製到 `<UserJourneys>` 元素內的 TrustFrameworkExtensions.xml 檔案。</span><span class="sxs-lookup"><span data-stu-id="9f819-153">Copy the profile edit user journey XML code from the TrustFrameworkBase.xml file to your TrustFrameworkExtensions.xml file inside the `<UserJourneys>` element.</span></span> <span data-ttu-id="9f819-154">然後在步驟 6 中進行修改。</span><span class="sxs-lookup"><span data-stu-id="9f819-154">Then make the modification under step 6.</span></span>

```XML
<OrchestrationStep Order="6" Type="ClaimsExchange">
    <ClaimsExchanges>
        <ClaimsExchange Id="GetLoyaltyData" TechnicalProfileReferenceId="AzureFunctions-LookUpLoyaltyWebHook" />
    </ClaimsExchanges>
</OrchestrationStep>
```

> [!IMPORTANT]
> <span data-ttu-id="9f819-155">如果操作順序不符合您的版本，請確定和該步驟一樣在 `ClaimsExchange` 類型 `SendClaims` 前插入程式碼。</span><span class="sxs-lookup"><span data-stu-id="9f819-155">If the order does not match your version, make sure that you insert the code as the step before the `ClaimsExchange` type `SendClaims`.</span></span>

<span data-ttu-id="9f819-156">使用者旅程圖的最終 XML 看起來應該像這樣：</span><span class="sxs-lookup"><span data-stu-id="9f819-156">The final XML for the user journey should look like this:</span></span>

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
        <!-- Add a step 6 to the user journey before the JWT token is created-->
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

## <a name="step-5-add-the-claim-city-to-your-relying-party-policy-file-so-the-claim-is-sent-to-your-application"></a><span data-ttu-id="9f819-157">步驟 5：將宣告 `city` 新增至您的信賴憑證者原則檔案，以便將宣告傳送至您的應用程式</span><span class="sxs-lookup"><span data-stu-id="9f819-157">Step 5: Add the claim `city` to your relying party policy file so the claim is sent to your application</span></span>

<span data-ttu-id="9f819-158">請編輯您的 ProfileEdit.xml 信賴憑證者 (RP) 檔案，並修改 `<TechnicalProfile Id="PolicyProfile">` 元素以新增下列內容︰`<OutputClaim ClaimTypeReferenceId="city" />`。</span><span class="sxs-lookup"><span data-stu-id="9f819-158">Edit your ProfileEdit.xml relying party (RP) file and modify the `<TechnicalProfile Id="PolicyProfile">` element to add the following: `<OutputClaim ClaimTypeReferenceId="city" />`.</span></span>

<span data-ttu-id="9f819-159">新增宣告之後，技術設定檔看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="9f819-159">After you add the new claim, the technical profile looks like this:</span></span>

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

## <a name="step-6-upload-your-changes-and-test"></a><span data-ttu-id="9f819-160">步驟 6：上傳您的變更和測試</span><span class="sxs-lookup"><span data-stu-id="9f819-160">Step 6: Upload your changes and test</span></span>

<span data-ttu-id="9f819-161">覆寫現有的原則版本。</span><span class="sxs-lookup"><span data-stu-id="9f819-161">Overwrite the existing versions of the policy.</span></span>

1.  <span data-ttu-id="9f819-162">(選擇性：) 繼續之前，請先儲存擴充檔案的現有版本 (透過下載)。</span><span class="sxs-lookup"><span data-stu-id="9f819-162">(Optional:) Save the existing version (by downloading) of your extensions file before you proceed.</span></span> <span data-ttu-id="9f819-163">建議您不要上傳多個擴充檔案版本，以免一開始的複雜性太高。</span><span class="sxs-lookup"><span data-stu-id="9f819-163">To keep the initial complexity low, we recommend that you do not upload multiple versions of the extensions file.</span></span>
2.  <span data-ttu-id="9f819-164">(選擇性：) 藉由變更 `PolicyId="B2C_1A_TrustFrameworkProfileEdit"`，來為原則編輯檔案重新命名原則識別碼的新版本。</span><span class="sxs-lookup"><span data-stu-id="9f819-164">(Optional:) Rename the new version of the policy ID for the policy edit file by changing   `PolicyId="B2C_1A_TrustFrameworkProfileEdit"`.</span></span>
3.  <span data-ttu-id="9f819-165">上傳擴充檔案。</span><span class="sxs-lookup"><span data-stu-id="9f819-165">Upload the extensions file.</span></span>
4.  <span data-ttu-id="9f819-166">上傳原則編輯 RP 檔案。</span><span class="sxs-lookup"><span data-stu-id="9f819-166">Upload the policy edit RP file.</span></span>
5.  <span data-ttu-id="9f819-167">使用 [立即執行] 來測試原則。</span><span class="sxs-lookup"><span data-stu-id="9f819-167">Use **Run Now** to test the policy.</span></span> <span data-ttu-id="9f819-168">檢閱 IEF 傳回給應用程式的權杖。</span><span class="sxs-lookup"><span data-stu-id="9f819-168">Review the token that the IEF returns to the application.</span></span>

<span data-ttu-id="9f819-169">如果一切設定皆正確，權杖會包含新的宣告 `city`，且值為 `Redmond`。</span><span class="sxs-lookup"><span data-stu-id="9f819-169">If everything is set up correctly, the token will include the new claim `city`, with the value `Redmond`.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="9f819-170">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9f819-170">Next steps</span></span>

[<span data-ttu-id="9f819-171">使用 REST API 來作為驗證步驟</span><span class="sxs-lookup"><span data-stu-id="9f819-171">Use a REST API as a validation step</span></span>](active-directory-b2c-rest-api-validation-custom.md)

[<span data-ttu-id="9f819-172">修改設定檔編輯以從使用者收集其他資訊</span><span class="sxs-lookup"><span data-stu-id="9f819-172">Modify the profile edit to gather additional information from your users</span></span>](active-directory-b2c-create-custom-attributes-profile-edit-custom.md)
