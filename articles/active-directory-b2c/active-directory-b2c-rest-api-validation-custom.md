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
ms.openlocfilehash: cec6c6e110514a8bbe0e0780f36738ff21ae2f00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-integrate-rest-api-claims-exchanges-in-your-azure-ad-b2c-user-journey-as-validation-on-user-input"></a><span data-ttu-id="3acee-103">逐步解說︰將 REST API 宣告交換整合到 Azure AD B2C 使用者旅程圖中以作為使用者輸入的驗證</span><span class="sxs-lookup"><span data-stu-id="3acee-103">Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as validation on user input</span></span>

<span data-ttu-id="3acee-104">hello 識別體驗架構 (IEF) 構成 Azure Active Directory B2C (Azure AD B2C) 可讓 hello 身分識別開發人員 toointegrate 與 rest 式 API，在使用者之旅互動。</span><span class="sxs-lookup"><span data-stu-id="3acee-104">hello Identity Experience Framework (IEF) that underlies Azure Active Directory B2C (Azure AD B2C) enables hello identity developer toointegrate an interaction with a RESTful API in a user journey.</span></span>  

<span data-ttu-id="3acee-105">在本逐步解說 hello 最後，將無法 toocreate 互動 RESTful 服務的 Azure AD B2C 使用者旅程。</span><span class="sxs-lookup"><span data-stu-id="3acee-105">At hello end of this walkthrough, you will be able toocreate an Azure AD B2C user journey that interacts with RESTful services.</span></span>

<span data-ttu-id="3acee-106">hello IEF 宣告中傳送資料，並接收回宣告中的資料。</span><span class="sxs-lookup"><span data-stu-id="3acee-106">hello IEF sends data in claims and receives data back in claims.</span></span> <span data-ttu-id="3acee-107">hello hello 應用程式開發介面互動：</span><span class="sxs-lookup"><span data-stu-id="3acee-107">hello interaction with hello API:</span></span>

- <span data-ttu-id="3acee-108">可設計為 REST API 宣告交換，或作為在協調流程步驟內發生的驗證設定檔。</span><span class="sxs-lookup"><span data-stu-id="3acee-108">Can be designed as a REST API claims exchange or as a validation profile, which happens inside an orchestration step.</span></span>
- <span data-ttu-id="3acee-109">通常會驗證來自 hello 使用者輸入。</span><span class="sxs-lookup"><span data-stu-id="3acee-109">Typically validates input from hello user.</span></span> <span data-ttu-id="3acee-110">如果已拒絕來自 hello 使用者 hello 值，hello 使用者可以再試一次 tooenter hello 機會 tooreturn 錯誤訊息的有效值。</span><span class="sxs-lookup"><span data-stu-id="3acee-110">If hello value from hello user is rejected, hello user can try again tooenter a valid value with hello opportunity tooreturn an error message.</span></span>

<span data-ttu-id="3acee-111">您也可以設計一個步驟是協調流程的 hello 互動。</span><span class="sxs-lookup"><span data-stu-id="3acee-111">You can also design hello interaction as an orchestration step.</span></span> <span data-ttu-id="3acee-112">如需詳細資訊，請參閱[逐步解說︰將 REST API 宣告交換整合到 Azure AD B2C 使用者旅程圖中以作為協調流程步驟](active-directory-b2c-rest-api-step-custom.md)。</span><span class="sxs-lookup"><span data-stu-id="3acee-112">For more information, see [Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as an orchestration step](active-directory-b2c-rest-api-step-custom.md).</span></span>

<span data-ttu-id="3acee-113">Hello 驗證設定檔範例，我們將使用 hello 設定檔編輯使用者之旅 ProfileEdit.xml hello 入門組件檔案中。</span><span class="sxs-lookup"><span data-stu-id="3acee-113">For hello validation profile example, we will use hello profile edit user journey in hello starter pack file ProfileEdit.xml.</span></span>

<span data-ttu-id="3acee-114">提供由 hello 設定檔中的 hello 使用者編輯不是排除清單的一部分，我們可以確認該 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="3acee-114">We can verify that hello name provided by hello user in hello profile edit is not part of an exclusion list.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3acee-115">必要條件</span><span class="sxs-lookup"><span data-stu-id="3acee-115">Prerequisites</span></span>

- <span data-ttu-id="3acee-116">Sign-up/登入中, 所述的本機帳戶的 Azure AD B2C 租用戶設定 toocomplete[入門](active-directory-b2c-get-started-custom.md)。</span><span class="sxs-lookup"><span data-stu-id="3acee-116">An Azure AD B2C tenant configured toocomplete a local account sign-up/sign-in, as described in [Getting started](active-directory-b2c-get-started-custom.md).</span></span>
- <span data-ttu-id="3acee-117">使用 REST API 端點 toointeract。</span><span class="sxs-lookup"><span data-stu-id="3acee-117">A REST API endpoint toointeract with.</span></span> <span data-ttu-id="3acee-118">針對這個逐步解說，我們設定了名為 [WingTipGames](https://wingtipgamesb2c.azurewebsites.net/) 的示範網站，其中含有一個 REST API 服務。</span><span class="sxs-lookup"><span data-stu-id="3acee-118">For this walkthrough, we've set up a demo site called [WingTipGames](https://wingtipgamesb2c.azurewebsites.net/) with a REST API service.</span></span>

## <a name="step-1-prepare-hello-rest-api-function"></a><span data-ttu-id="3acee-119">步驟 1： 準備 hello REST API 函式</span><span class="sxs-lookup"><span data-stu-id="3acee-119">Step 1: Prepare hello REST API function</span></span>

> [!NOTE]
> <span data-ttu-id="3acee-120">安裝程式的 REST API 函式是在這篇文章 hello 範圍之外。</span><span class="sxs-lookup"><span data-stu-id="3acee-120">Setup of REST API functions is outside hello scope of this article.</span></span> <span data-ttu-id="3acee-121">[Azure 函數](https://docs.microsoft.com/azure/azure-functions/functions-reference)toocreate hello 雲端中的 rest 式服務提供絕佳的工具組。</span><span class="sxs-lookup"><span data-stu-id="3acee-121">[Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-reference) provides an excellent toolkit toocreate RESTful services in hello cloud.</span></span>

<span data-ttu-id="3acee-122">我們建立了一個 Azure 函式，來接收它預期作為 `playerTag` 的宣告。</span><span class="sxs-lookup"><span data-stu-id="3acee-122">We have created an Azure function that receives a claim that it expects as `playerTag`.</span></span> <span data-ttu-id="3acee-123">hello 函式會驗證是否存在於此宣告。</span><span class="sxs-lookup"><span data-stu-id="3acee-123">hello function validates whether this claim exists.</span></span> <span data-ttu-id="3acee-124">您可以存取中的 hello 完整的 Azure 函式程式碼[GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples)。</span><span class="sxs-lookup"><span data-stu-id="3acee-124">You can access hello complete Azure function code in [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).</span></span>

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
      userMessage = $"hello player tag '{requestContentAsJObject.playerTag}' is already used."
    },
    new JsonMediaTypeFormatter(),
    "application/json");
}

return request.CreateResponse(HttpStatusCode.OK);
```

<span data-ttu-id="3acee-125">hello IEF 預期 hello`userMessage`宣告該 hello Azure 函式傳回。</span><span class="sxs-lookup"><span data-stu-id="3acee-125">hello IEF expects hello `userMessage` claim that hello Azure function returns.</span></span> <span data-ttu-id="3acee-126">這個宣告會以字串 toohello 使用者如果 hello 驗證失敗，例如在上述範例中的 hello 傳回 「 409 衝突 」 狀態時。</span><span class="sxs-lookup"><span data-stu-id="3acee-126">This claim will be presented as a string toohello user if hello validation fails, such as when a 409 conflict status is returned in hello preceding example.</span></span>

## <a name="step-2-configure-hello-restful-api-claims-exchange-as-a-technical-profile-in-your-trustframeworkextensionsxml-file"></a><span data-ttu-id="3acee-127">步驟 2： 設定 hello RESTful API 宣告交換為技術 TrustFrameworkExtensions.xml 檔案中設定檔</span><span class="sxs-lookup"><span data-stu-id="3acee-127">Step 2: Configure hello RESTful API claims exchange as a technical profile in your TrustFrameworkExtensions.xml file</span></span>

<span data-ttu-id="3acee-128">技術的設定檔是 hello 的 hello exchange 以 hello RESTful 服務所需的完整設定。</span><span class="sxs-lookup"><span data-stu-id="3acee-128">A technical profile is hello full configuration of hello exchange desired with hello RESTful service.</span></span> <span data-ttu-id="3acee-129">開啟 hello TrustFrameworkExtensions.xml 檔案並加入下列 XML 程式碼片段 hello hello`<ClaimsProviders>`項目。</span><span class="sxs-lookup"><span data-stu-id="3acee-129">Open hello TrustFrameworkExtensions.xml file and add hello following XML snippet inside hello `<ClaimsProviders>` element.</span></span>

> [!NOTE]
> <span data-ttu-id="3acee-130">在下列 XML，RESTful 的提供者的 hello`Version=1.0.0.0`即稱為 hello 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="3acee-130">In hello following XML, RESTful provider `Version=1.0.0.0` is described as hello protocol.</span></span> <span data-ttu-id="3acee-131">將其視為與 hello 外部服務互動的 hello 函式。</span><span class="sxs-lookup"><span data-stu-id="3acee-131">Consider it as hello function that will interact with hello external service.</span></span> <!-- TODO: A full definition of hello schema can be found...link tooRESTful Provider schema definition>-->

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

<span data-ttu-id="3acee-132">hello`InputClaims`項目會定義會將傳送嗨 IEF toohello REST 服務的 hello 宣告。</span><span class="sxs-lookup"><span data-stu-id="3acee-132">hello `InputClaims` element defines hello claims that will be sent from hello IEF toohello REST service.</span></span> <span data-ttu-id="3acee-133">在此範例中，hello hello 宣告的內容`givenName`傳送 toohello REST 服務，做為`playerTag`。</span><span class="sxs-lookup"><span data-stu-id="3acee-133">In this example, hello contents of hello claim `givenName` will be sent toohello REST service as `playerTag`.</span></span> <span data-ttu-id="3acee-134">在此範例中，不預期 IEF hello 回宣告。</span><span class="sxs-lookup"><span data-stu-id="3acee-134">In this example, hello IEF does not expect claims back.</span></span> <span data-ttu-id="3acee-135">相反地，它會等待回應 hello REST 服務，根據它所收到 hello 狀態碼的行為模式。</span><span class="sxs-lookup"><span data-stu-id="3acee-135">Instead, it waits for a response from hello REST service and acts based on hello status codes that it receives.</span></span>

## <a name="step-3-include-hello-restful-service-claims-exchange-in-self-asserted-technical-profile-where-you-want-toovalidate-hello-user-input"></a><span data-ttu-id="3acee-136">步驟 3: Hello RESTful 服務宣告交換納入自我判斷提示技術的設定檔想 toovalidate hello 使用者輸入</span><span class="sxs-lookup"><span data-stu-id="3acee-136">Step 3: Include hello RESTful service claims exchange in self-asserted technical profile where you want toovalidate hello user input</span></span>

<span data-ttu-id="3acee-137">hello hello 驗證步驟的最常見的用法是在 hello 與使用者之間的互動。</span><span class="sxs-lookup"><span data-stu-id="3acee-137">hello most common use of hello validation step is in hello interaction with a user.</span></span> <span data-ttu-id="3acee-138">Hello 使用者所在預期的 tooprovide 輸入的所有互動都都有*自我判斷提示設定檔技術*。</span><span class="sxs-lookup"><span data-stu-id="3acee-138">All interactions where hello user is expected tooprovide input are *self-asserted technical profiles*.</span></span> <span data-ttu-id="3acee-139">此範例中，我們將 hello 驗證 toohello 自助 Asserted ProfileUpdate 技術設定檔。</span><span class="sxs-lookup"><span data-stu-id="3acee-139">For this example, we will add hello validation toohello Self-Asserted-ProfileUpdate technical profile.</span></span> <span data-ttu-id="3acee-140">這是 hello 信賴憑證者的合作對象 (RP) 原則檔 hello 技術設定檔`Profile Edit`使用。</span><span class="sxs-lookup"><span data-stu-id="3acee-140">This is hello technical profile that hello relying party (RP) policy file `Profile Edit` uses.</span></span>

<span data-ttu-id="3acee-141">自我判斷提示設定檔技術 tooadd hello 宣告 exchange toohello:</span><span class="sxs-lookup"><span data-stu-id="3acee-141">tooadd hello claims exchange toohello self-asserted technical profile:</span></span>

1. <span data-ttu-id="3acee-142">開啟 hello TrustFrameworkBase.xml 檔案，並搜尋`<TechnicalProfile Id="SelfAsserted-ProfileUpdate">`。</span><span class="sxs-lookup"><span data-stu-id="3acee-142">Open hello TrustFrameworkBase.xml file and search for `<TechnicalProfile Id="SelfAsserted-ProfileUpdate">`.</span></span>
2. <span data-ttu-id="3acee-143">檢閱 hello 此技術的設定檔組態。</span><span class="sxs-lookup"><span data-stu-id="3acee-143">Review hello configuration of this technical profile.</span></span> <span data-ttu-id="3acee-144">觀察 hello exchange 與 hello 使用者視為 hello 使用者 （輸入宣告） 的系統會要求的宣告和宣告，就應該從 hello 自我判斷提示提供者 （輸出宣告） 的定義方式。</span><span class="sxs-lookup"><span data-stu-id="3acee-144">Observe how hello exchange with hello user is defined as claims that will be asked of hello user (input claims) and claims that will be expected back from hello self-asserted provider (output claims).</span></span>
3. <span data-ttu-id="3acee-145">搜尋 `TechnicalProfileReferenceId="SelfAsserted-ProfileUpdate`，並注意系統會叫用此設定檔來作為 `<UserJourney Id="ProfileEdit">` 的協調流程步驟 6。</span><span class="sxs-lookup"><span data-stu-id="3acee-145">Search for `TechnicalProfileReferenceId="SelfAsserted-ProfileUpdate`, and notice that this profile is invoked as orchestration step 6 of `<UserJourney Id="ProfileEdit">`.</span></span>

## <a name="step-4-upload-and-test-hello-profile-edit-rp-policy-file"></a><span data-ttu-id="3acee-146">步驟 4： 上傳和測試 hello 設定檔編輯 RP 原則檔</span><span class="sxs-lookup"><span data-stu-id="3acee-146">Step 4: Upload and test hello profile edit RP policy file</span></span>

1. <span data-ttu-id="3acee-147">上傳 hello hello TrustFrameworkExtensions.xml 檔案新版本。</span><span class="sxs-lookup"><span data-stu-id="3acee-147">Upload hello new version of hello TrustFrameworkExtensions.xml file.</span></span>
2. <span data-ttu-id="3acee-148">使用**立即執行**tootest hello 設定檔編輯 RP 原則檔案。</span><span class="sxs-lookup"><span data-stu-id="3acee-148">Use **Run now** tootest hello profile edit RP policy file.</span></span>
3. <span data-ttu-id="3acee-149">藉由提供的其中一個 hello 現有名稱 (例如，mcvinny) 測試 hello 驗證，在 hello**名字**欄位。</span><span class="sxs-lookup"><span data-stu-id="3acee-149">Test hello validation by providing one of hello existing names (for example, mcvinny) in hello **Given Name** field.</span></span> <span data-ttu-id="3acee-150">如果所有項目已正確設定時，您應該會收到通知 hello 使用者 hello player 標記已在使用的訊息。</span><span class="sxs-lookup"><span data-stu-id="3acee-150">If everything is set up correctly, you should receive a message that notifies hello user that hello player tag is already used.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3acee-151">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3acee-151">Next steps</span></span>

[<span data-ttu-id="3acee-152">修改 hello 設定檔編輯和使用者註冊 toogather 額外資訊從您的使用者</span><span class="sxs-lookup"><span data-stu-id="3acee-152">Modify hello profile edit and user registration toogather additional information from your users</span></span>](active-directory-b2c-create-custom-attributes-profile-edit-custom.md)

[<span data-ttu-id="3acee-153">逐步解說︰將 REST API 宣告交換整合到 Azure AD B2C 使用者旅程圖中以作為協調流程步驟</span><span class="sxs-lookup"><span data-stu-id="3acee-153">Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as an orchestration step</span></span>](active-directory-b2c-rest-api-step-custom.md)
