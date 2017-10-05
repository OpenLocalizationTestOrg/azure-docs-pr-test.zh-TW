---
title: "Azure Active Directory B2C：使用 REST API 宣告交換作為驗證 | Microsoft Docs"
description: "Azure Active Directory B2C 自訂原則的主題"
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
ms.openlocfilehash: eb44a0d2234c9ee3801d8b3a1655d877aa2f4fef
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="walkthrough-integrate-rest-api-claims-exchanges-in-your-azure-ad-b2c-user-journey-as-validation-on-user-input"></a><span data-ttu-id="2e14a-103">逐步解說︰將 REST API 宣告交換整合到 Azure AD B2C 使用者旅程圖中以作為使用者輸入的驗證</span><span class="sxs-lookup"><span data-stu-id="2e14a-103">Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as validation on user input</span></span>

<span data-ttu-id="2e14a-104">構成 Azure Active Directory B2C (Azure AD B2C) 基礎的識別體驗架構 (IEF)，可讓身分識別開發人員於使用者旅程圖中整合與 RESTful API 的互動。</span><span class="sxs-lookup"><span data-stu-id="2e14a-104">The Identity Experience Framework (IEF) that underlies Azure Active Directory B2C (Azure AD B2C) enables the identity developer to integrate an interaction with a RESTful API in a user journey.</span></span>  

<span data-ttu-id="2e14a-105">在本逐步解說結束時，您將能建立與 RESTful 服務互動的 Azure AD B2C 使用者旅程圖。</span><span class="sxs-lookup"><span data-stu-id="2e14a-105">At the end of this walkthrough, you will be able to create an Azure AD B2C user journey that interacts with RESTful services.</span></span>

<span data-ttu-id="2e14a-106">IEF 會在宣告中傳送資料，並在宣告中收到傳回的資料。</span><span class="sxs-lookup"><span data-stu-id="2e14a-106">The IEF sends data in claims and receives data back in claims.</span></span> <span data-ttu-id="2e14a-107">與 API 的互動：</span><span class="sxs-lookup"><span data-stu-id="2e14a-107">The interaction with the API:</span></span>

- <span data-ttu-id="2e14a-108">可設計為 REST API 宣告交換，或作為在協調流程步驟內發生的驗證設定檔。</span><span class="sxs-lookup"><span data-stu-id="2e14a-108">Can be designed as a REST API claims exchange or as a validation profile, which happens inside an orchestration step.</span></span>
- <span data-ttu-id="2e14a-109">通常會驗證使用者的輸入。</span><span class="sxs-lookup"><span data-stu-id="2e14a-109">Typically validates input from the user.</span></span> <span data-ttu-id="2e14a-110">如果系統拒絕使用者輸入的值，使用者可再次試著輸入有效值，但系統可能會傳回錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="2e14a-110">If the value from the user is rejected, the user can try again to enter a valid value with the opportunity to return an error message.</span></span>

<span data-ttu-id="2e14a-111">您也可以將互動設計為協調流程步驟。</span><span class="sxs-lookup"><span data-stu-id="2e14a-111">You can also design the interaction as an orchestration step.</span></span> <span data-ttu-id="2e14a-112">如需詳細資訊，請參閱[逐步解說︰將 REST API 宣告交換整合到 Azure AD B2C 使用者旅程圖中以作為協調流程步驟](active-directory-b2c-rest-api-step-custom.md)。</span><span class="sxs-lookup"><span data-stu-id="2e14a-112">For more information, see [Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as an orchestration step](active-directory-b2c-rest-api-step-custom.md).</span></span>

<span data-ttu-id="2e14a-113">至於驗證設定檔範例，我們將使用入門套件檔案 ProfileEdit.xml 中的設定檔編輯使用者旅程圖。</span><span class="sxs-lookup"><span data-stu-id="2e14a-113">For the validation profile example, we will use the profile edit user journey in the starter pack file ProfileEdit.xml.</span></span>

<span data-ttu-id="2e14a-114">我們可以驗證使用者在設定檔編輯中所提供的名稱不在排除清單中。</span><span class="sxs-lookup"><span data-stu-id="2e14a-114">We can verify that the name provided by the user in the profile edit is not part of an exclusion list.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2e14a-115">必要條件</span><span class="sxs-lookup"><span data-stu-id="2e14a-115">Prerequisites</span></span>

- <span data-ttu-id="2e14a-116">如[開始使用](active-directory-b2c-get-started-custom.md)所述，設定為完成本機帳戶註冊/登入的 Azure AD B2C 租用戶。</span><span class="sxs-lookup"><span data-stu-id="2e14a-116">An Azure AD B2C tenant configured to complete a local account sign-up/sign-in, as described in [Getting started](active-directory-b2c-get-started-custom.md).</span></span>
- <span data-ttu-id="2e14a-117">要互動的 REST API 端點。</span><span class="sxs-lookup"><span data-stu-id="2e14a-117">A REST API endpoint to interact with.</span></span> <span data-ttu-id="2e14a-118">針對這個逐步解說，我們設定了名為 [WingTipGames](https://wingtipgamesb2c.azurewebsites.net/) 的示範網站，其中含有一個 REST API 服務。</span><span class="sxs-lookup"><span data-stu-id="2e14a-118">For this walkthrough, we've set up a demo site called [WingTipGames](https://wingtipgamesb2c.azurewebsites.net/) with a REST API service.</span></span>

## <a name="step-1-prepare-the-rest-api-function"></a><span data-ttu-id="2e14a-119">步驟 1：準備 REST API 函式</span><span class="sxs-lookup"><span data-stu-id="2e14a-119">Step 1: Prepare the REST API function</span></span>

> [!NOTE]
> <span data-ttu-id="2e14a-120">REST API 函式的設定不在本文討論範圍內。</span><span class="sxs-lookup"><span data-stu-id="2e14a-120">Setup of REST API functions is outside the scope of this article.</span></span> <span data-ttu-id="2e14a-121">[Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-reference) 提供了絕佳的工具組，供您在雲端建立 RESTful 服務。</span><span class="sxs-lookup"><span data-stu-id="2e14a-121">[Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-reference) provides an excellent toolkit to create RESTful services in the cloud.</span></span>

<span data-ttu-id="2e14a-122">我們建立了一個 Azure 函式，來接收它預期作為 `playerTag` 的宣告。</span><span class="sxs-lookup"><span data-stu-id="2e14a-122">We have created an Azure function that receives a claim that it expects as `playerTag`.</span></span> <span data-ttu-id="2e14a-123">此函式會驗證此宣告是否存在。</span><span class="sxs-lookup"><span data-stu-id="2e14a-123">The function validates whether this claim exists.</span></span> <span data-ttu-id="2e14a-124">您可以在 [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples) 中取得完整的 Azure 函式程式碼。</span><span class="sxs-lookup"><span data-stu-id="2e14a-124">You can access the complete Azure function code in [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).</span></span>

```csharp
if (requestContentAsJObject.playerTag == null)
{
  return request.CreateResponse(HttpStatusCode.BadRequest);
}

var playerTag = ((string) requestContentAsJObject.playerTag).ToLower();

if (playerTag == "mcvinny" || playerTag == "msgates123" || playerTag == "revcottonmarcus")
{
  return request.CreateResponse<ResponseContent>(
    HttpStatusCode.Conflict,
    new ResponseContent
    {
      version = "1.0.0",
      status = (int) HttpStatusCode.Conflict,
      userMessage = $"The player tag '{requestContentAsJObject.playerTag}' is already used."
    },
    new JsonMediaTypeFormatter(),
    "application/json");
}

return request.CreateResponse(HttpStatusCode.OK);
```

<span data-ttu-id="2e14a-125">IEF 預期 Azure 函式會傳回 `userMessage` 宣告。</span><span class="sxs-lookup"><span data-stu-id="2e14a-125">The IEF expects the `userMessage` claim that the Azure function returns.</span></span> <span data-ttu-id="2e14a-126">如果驗證失敗，即會以字串形式為使用者呈現此宣告，例如，當上述範例中傳回 409 衝突狀態時。</span><span class="sxs-lookup"><span data-stu-id="2e14a-126">This claim will be presented as a string to the user if the validation fails, such as when a 409 conflict status is returned in the preceding example.</span></span>

## <a name="step-2-configure-the-restful-api-claims-exchange-as-a-technical-profile-in-your-trustframeworkextensionsxml-file"></a><span data-ttu-id="2e14a-127">步驟 2：在 TrustFrameworkExtensions.xml 檔案中，將 RESTful API 宣告交換設為技術設定檔</span><span class="sxs-lookup"><span data-stu-id="2e14a-127">Step 2: Configure the RESTful API claims exchange as a technical profile in your TrustFrameworkExtensions.xml file</span></span>

<span data-ttu-id="2e14a-128">技術設定檔是 RESTful 服務所需之交換的完整設定。</span><span class="sxs-lookup"><span data-stu-id="2e14a-128">A technical profile is the full configuration of the exchange desired with the RESTful service.</span></span> <span data-ttu-id="2e14a-129">開啟 TrustFrameworkExtensions.xml 檔案，然後在 `<ClaimsProviders>` 元素內加入下列 XML 程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="2e14a-129">Open the TrustFrameworkExtensions.xml file and add the following XML snippet inside the `<ClaimsProviders>` element.</span></span>

> [!NOTE]
> <span data-ttu-id="2e14a-130">在下列 XML 中，會將 RESTful 提供者 `Version=1.0.0.0` 描述為通訊協定。</span><span class="sxs-lookup"><span data-stu-id="2e14a-130">In the following XML, RESTful provider `Version=1.0.0.0` is described as the protocol.</span></span> <span data-ttu-id="2e14a-131">請將它視為要與外部服務互動的函式。</span><span class="sxs-lookup"><span data-stu-id="2e14a-131">Consider it as the function that will interact with the external service.</span></span> <!-- TODO: A full definition of the schema can be found...link to RESTful Provider schema definition>-->

```xml
<ClaimsProvider>
    <DisplayName>REST APIs</DisplayName>
    <TechnicalProfiles>
        <TechnicalProfile Id="AzureFunctions-CheckPlayerTagWebHook">
            <DisplayName>Check Player Tag Web Hook Azure Function</DisplayName>
            <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.RestfulProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
            <Metadata>
                <Item Key="ServiceUrl">https://wingtipb2cfuncs.azurewebsites.net/api/CheckPlayerTagWebHook?code=L/05YRSpojU0nECzM4Tp3LjBiA2ZGh3kTwwp1OVV7m0SelnvlRVLCg==</Item>
                <Item Key="AuthenticationType">None</Item>
                <Item Key="SendClaimsIn">Body</Item>
            </Metadata>
            <InputClaims>
                <InputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="playerTag" />
            </InputClaims>
            <UseTechnicalProfileForSessionManagement ReferenceId="SM-Noop" />
        </TechnicalProfile>
        <TechnicalProfile Id="SelfAsserted-ProfileUpdate">
            <ValidationTechnicalProfiles>
                <ValidationTechnicalProfile ReferenceId="AzureFunctions-CheckPlayerTagWebHook" />
            </ValidationTechnicalProfiles>
        </TechnicalProfile>
    </TechnicalProfiles>
</ClaimsProvider>
```

<span data-ttu-id="2e14a-132">`InputClaims` 元素會定義將從 IEF 傳送至 REST 服務的宣告。</span><span class="sxs-lookup"><span data-stu-id="2e14a-132">The `InputClaims` element defines the claims that will be sent from the IEF to the REST service.</span></span> <span data-ttu-id="2e14a-133">在此範例中，會將 `givenName` 宣告的內容傳送至 REST 服務以作為 `playerTag`。</span><span class="sxs-lookup"><span data-stu-id="2e14a-133">In this example, the contents of the claim `givenName` will be sent to the REST service as `playerTag`.</span></span> <span data-ttu-id="2e14a-134">在此範例中，IEF 不會預期傳回的宣告。</span><span class="sxs-lookup"><span data-stu-id="2e14a-134">In this example, the IEF does not expect claims back.</span></span> <span data-ttu-id="2e14a-135">相反地，它會等待來自 REST 服務的回應，並根據它接收的狀態碼採取動作。</span><span class="sxs-lookup"><span data-stu-id="2e14a-135">Instead, it waits for a response from the REST service and acts based on the status codes that it receives.</span></span>

## <a name="step-3-include-the-restful-service-claims-exchange-in-self-asserted-technical-profile-where-you-want-to-validate-the-user-input"></a><span data-ttu-id="2e14a-136">步驟 3：在您想要用來驗證使用者輸入的自我判斷技術設定檔中加入 RESTful 服務宣告交換</span><span class="sxs-lookup"><span data-stu-id="2e14a-136">Step 3: Include the RESTful service claims exchange in self-asserted technical profile where you want to validate the user input</span></span>

<span data-ttu-id="2e14a-137">驗證步驟最常用於與使用者互動。</span><span class="sxs-lookup"><span data-stu-id="2e14a-137">The most common use of the validation step is in the interaction with a user.</span></span> <span data-ttu-id="2e14a-138">使用者應該在其中提供輸入的所有互動就是「自我判斷的技術設定檔」。</span><span class="sxs-lookup"><span data-stu-id="2e14a-138">All interactions where the user is expected to provide input are *self-asserted technical profiles*.</span></span> <span data-ttu-id="2e14a-139">在此範例中，我們會將此驗證新增到 Self-Asserted-ProfileUpdate 技術設定檔。</span><span class="sxs-lookup"><span data-stu-id="2e14a-139">For this example, we will add the validation to the Self-Asserted-ProfileUpdate technical profile.</span></span> <span data-ttu-id="2e14a-140">這是信賴憑證者 (RP) 原則檔案 `Profile Edit` 使用的技術設定檔。</span><span class="sxs-lookup"><span data-stu-id="2e14a-140">This is the technical profile that the relying party (RP) policy file `Profile Edit` uses.</span></span>

<span data-ttu-id="2e14a-141">在自我判斷的技術設定檔中新增宣告交換：</span><span class="sxs-lookup"><span data-stu-id="2e14a-141">To add the claims exchange to the self-asserted technical profile:</span></span>

1. <span data-ttu-id="2e14a-142">開啟 TrustFrameworkBase.xml 檔案，並搜尋 `<TechnicalProfile Id="SelfAsserted-ProfileUpdate">`。</span><span class="sxs-lookup"><span data-stu-id="2e14a-142">Open the TrustFrameworkBase.xml file and search for `<TechnicalProfile Id="SelfAsserted-ProfileUpdate">`.</span></span>
2. <span data-ttu-id="2e14a-143">檢閱此技術設定檔的設定。</span><span class="sxs-lookup"><span data-stu-id="2e14a-143">Review the configuration of this technical profile.</span></span> <span data-ttu-id="2e14a-144">觀察與使用者所進行的交換如何定義為向使用者要求的宣告 (輸入宣告)，以及如何定義為應該從自我判斷提供者傳回的宣告 (輸出宣告)。</span><span class="sxs-lookup"><span data-stu-id="2e14a-144">Observe how the exchange with the user is defined as claims that will be asked of the user (input claims) and claims that will be expected back from the self-asserted provider (output claims).</span></span>
3. <span data-ttu-id="2e14a-145">搜尋 `TechnicalProfileReferenceId="SelfAsserted-ProfileUpdate`，並注意系統會叫用此設定檔來作為 `<UserJourney Id="ProfileEdit">` 的協調流程步驟 6。</span><span class="sxs-lookup"><span data-stu-id="2e14a-145">Search for `TechnicalProfileReferenceId="SelfAsserted-ProfileUpdate`, and notice that this profile is invoked as orchestration step 6 of `<UserJourney Id="ProfileEdit">`.</span></span>

## <a name="step-4-upload-and-test-the-profile-edit-rp-policy-file"></a><span data-ttu-id="2e14a-146">步驟 4：上傳和測試設定檔編輯 RP 原則檔案</span><span class="sxs-lookup"><span data-stu-id="2e14a-146">Step 4: Upload and test the profile edit RP policy file</span></span>

1. <span data-ttu-id="2e14a-147">上傳新版的 TrustFrameworkExtensions.xml 檔案。</span><span class="sxs-lookup"><span data-stu-id="2e14a-147">Upload the new version of the TrustFrameworkExtensions.xml file.</span></span>
2. <span data-ttu-id="2e14a-148">使用**立即執行**來測試設定檔編輯 RP 原則檔案。</span><span class="sxs-lookup"><span data-stu-id="2e14a-148">Use **Run now** to test the profile edit RP policy file.</span></span>
3. <span data-ttu-id="2e14a-149">在 [名字] 欄位中提供一個現有名稱 (例如︰mcvinny) 來測試驗證。</span><span class="sxs-lookup"><span data-stu-id="2e14a-149">Test the validation by providing one of the existing names (for example, mcvinny) in the **Given Name** field.</span></span> <span data-ttu-id="2e14a-150">如果一切設定皆正確，您應該會收到訊息，通知使用者，該玩家標記已在使用中。</span><span class="sxs-lookup"><span data-stu-id="2e14a-150">If everything is set up correctly, you should receive a message that notifies the user that the player tag is already used.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2e14a-151">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2e14a-151">Next steps</span></span>

[<span data-ttu-id="2e14a-152">修改設定檔編輯和使用者註冊以從使用者收集其他資訊</span><span class="sxs-lookup"><span data-stu-id="2e14a-152">Modify the profile edit and user registration to gather additional information from your users</span></span>](active-directory-b2c-create-custom-attributes-profile-edit-custom.md)

[<span data-ttu-id="2e14a-153">逐步解說︰將 REST API 宣告交換整合到 Azure AD B2C 使用者旅程圖中以作為協調流程步驟</span><span class="sxs-lookup"><span data-stu-id="2e14a-153">Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as an orchestration step</span></span>](active-directory-b2c-rest-api-step-custom.md)
