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
# <a name="walkthrough-integrate-rest-api-claims-exchanges-in-your-azure-ad-b2c-user-journey-as-validation-on-user-input"></a>逐步解說︰將 REST API 宣告交換整合到 Azure AD B2C 使用者旅程圖中以作為使用者輸入的驗證

hello 識別體驗架構 (IEF) 構成 Azure Active Directory B2C (Azure AD B2C) 可讓 hello 身分識別開發人員 toointegrate 與 rest 式 API，在使用者之旅互動。  

在本逐步解說 hello 最後，將無法 toocreate 互動 RESTful 服務的 Azure AD B2C 使用者旅程。

hello IEF 宣告中傳送資料，並接收回宣告中的資料。 hello hello 應用程式開發介面互動：

- 可設計為 REST API 宣告交換，或作為在協調流程步驟內發生的驗證設定檔。
- 通常會驗證來自 hello 使用者輸入。 如果已拒絕來自 hello 使用者 hello 值，hello 使用者可以再試一次 tooenter hello 機會 tooreturn 錯誤訊息的有效值。

您也可以設計一個步驟是協調流程的 hello 互動。 如需詳細資訊，請參閱[逐步解說︰將 REST API 宣告交換整合到 Azure AD B2C 使用者旅程圖中以作為協調流程步驟](active-directory-b2c-rest-api-step-custom.md)。

Hello 驗證設定檔範例，我們將使用 hello 設定檔編輯使用者之旅 ProfileEdit.xml hello 入門組件檔案中。

提供由 hello 設定檔中的 hello 使用者編輯不是排除清單的一部分，我們可以確認該 hello 名稱。

## <a name="prerequisites"></a>必要條件

- Sign-up/登入中, 所述的本機帳戶的 Azure AD B2C 租用戶設定 toocomplete[入門](active-directory-b2c-get-started-custom.md)。
- 使用 REST API 端點 toointeract。 針對這個逐步解說，我們設定了名為 [WingTipGames](https://wingtipgamesb2c.azurewebsites.net/) 的示範網站，其中含有一個 REST API 服務。

## <a name="step-1-prepare-hello-rest-api-function"></a>步驟 1： 準備 hello REST API 函式

> [!NOTE]
> 安裝程式的 REST API 函式是在這篇文章 hello 範圍之外。 [Azure 函數](https://docs.microsoft.com/azure/azure-functions/functions-reference)toocreate hello 雲端中的 rest 式服務提供絕佳的工具組。

我們建立了一個 Azure 函式，來接收它預期作為 `playerTag` 的宣告。 hello 函式會驗證是否存在於此宣告。 您可以存取中的 hello 完整的 Azure 函式程式碼[GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples)。

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

hello IEF 預期 hello`userMessage`宣告該 hello Azure 函式傳回。 這個宣告會以字串 toohello 使用者如果 hello 驗證失敗，例如在上述範例中的 hello 傳回 「 409 衝突 」 狀態時。

## <a name="step-2-configure-hello-restful-api-claims-exchange-as-a-technical-profile-in-your-trustframeworkextensionsxml-file"></a>步驟 2： 設定 hello RESTful API 宣告交換為技術 TrustFrameworkExtensions.xml 檔案中設定檔

技術的設定檔是 hello 的 hello exchange 以 hello RESTful 服務所需的完整設定。 開啟 hello TrustFrameworkExtensions.xml 檔案並加入下列 XML 程式碼片段 hello hello`<ClaimsProviders>`項目。

> [!NOTE]
> 在下列 XML，RESTful 的提供者的 hello`Version=1.0.0.0`即稱為 hello 通訊協定。 將其視為與 hello 外部服務互動的 hello 函式。 <!-- TODO: A full definition of hello schema can be found...link tooRESTful Provider schema definition>-->

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

hello`InputClaims`項目會定義會將傳送嗨 IEF toohello REST 服務的 hello 宣告。 在此範例中，hello hello 宣告的內容`givenName`傳送 toohello REST 服務，做為`playerTag`。 在此範例中，不預期 IEF hello 回宣告。 相反地，它會等待回應 hello REST 服務，根據它所收到 hello 狀態碼的行為模式。

## <a name="step-3-include-hello-restful-service-claims-exchange-in-self-asserted-technical-profile-where-you-want-toovalidate-hello-user-input"></a>步驟 3: Hello RESTful 服務宣告交換納入自我判斷提示技術的設定檔想 toovalidate hello 使用者輸入

hello hello 驗證步驟的最常見的用法是在 hello 與使用者之間的互動。 Hello 使用者所在預期的 tooprovide 輸入的所有互動都都有*自我判斷提示設定檔技術*。 此範例中，我們將 hello 驗證 toohello 自助 Asserted ProfileUpdate 技術設定檔。 這是 hello 信賴憑證者的合作對象 (RP) 原則檔 hello 技術設定檔`Profile Edit`使用。

自我判斷提示設定檔技術 tooadd hello 宣告 exchange toohello:

1. 開啟 hello TrustFrameworkBase.xml 檔案，並搜尋`<TechnicalProfile Id="SelfAsserted-ProfileUpdate">`。
2. 檢閱 hello 此技術的設定檔組態。 觀察 hello exchange 與 hello 使用者視為 hello 使用者 （輸入宣告） 的系統會要求的宣告和宣告，就應該從 hello 自我判斷提示提供者 （輸出宣告） 的定義方式。
3. 搜尋 `TechnicalProfileReferenceId="SelfAsserted-ProfileUpdate`，並注意系統會叫用此設定檔來作為 `<UserJourney Id="ProfileEdit">` 的協調流程步驟 6。

## <a name="step-4-upload-and-test-hello-profile-edit-rp-policy-file"></a>步驟 4： 上傳和測試 hello 設定檔編輯 RP 原則檔

1. 上傳 hello hello TrustFrameworkExtensions.xml 檔案新版本。
2. 使用**立即執行**tootest hello 設定檔編輯 RP 原則檔案。
3. 藉由提供的其中一個 hello 現有名稱 (例如，mcvinny) 測試 hello 驗證，在 hello**名字**欄位。 如果所有項目已正確設定時，您應該會收到通知 hello 使用者 hello player 標記已在使用的訊息。

## <a name="next-steps"></a>後續步驟

[修改 hello 設定檔編輯和使用者註冊 toogather 額外資訊從您的使用者](active-directory-b2c-create-custom-attributes-profile-edit-custom.md)

[逐步解說︰將 REST API 宣告交換整合到 Azure AD B2C 使用者旅程圖中以作為協調流程步驟](active-directory-b2c-rest-api-step-custom.md)
