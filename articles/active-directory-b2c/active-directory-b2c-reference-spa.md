---
title: "Azure Active Directory B2C：使用隱含流程的單一頁面應用程式 | Microsoft Docs"
description: "了解如何 toobuild 單一頁面應用程式直接使用 OAuth 2.0 隱含流程與 Azure Active Directory B2C。"
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: a45cc74c-a37e-453f-b08b-af75855e0792
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: parakhj
ms.openlocfilehash: 5e52abc18fe545f0f6d1745cdb2ea42c5b2698cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-single-page-app-sign-in-by-using-oauth-20-implicit-flow"></a>Azure AD B2C：使用 OAuth 2.0 隱含流程的單一頁面應用程式登入

> [!NOTE]
> 這項功能處於預覽狀態。
> 

許多新式應用程式都有一個單頁應用程式前端，主要是以 JavaScript 撰寫。 通常，hello 撰寫應用程式的使用，如 AngularJS、 Ember.js 或 Durandal 架構。 主要在瀏覽器上執行的單一頁面應用程式和其他 JavaScript 應用程式，在驗證時會面臨一些額外的挑戰：

* 這些應用程式的 hello 安全性特性會明顯不同於傳統伺服器為基礎的 web 應用程式。
* 許多授權伺服器與識別提供者不支援跨原始來源資源共用 (CORS) 要求。
* 停用完整網頁瀏覽器重新導向遠離 hello 應用程式可能會大幅侵入性功能 toohello 使用者經驗。

toosupport 這些應用程式，Azure Active Directory B2C (Azure AD B2C) 會使用 hello OAuth 2.0 隱含流程。 hello OAuth 2.0 授權隱含授與流程述[區段 hello OAuth 2.0 規格的 4.2](http://tools.ietf.org/html/rfc6749)。 在隱含流程中，hello 應用程式接收權杖，直接從 hello Azure Active Directory (Azure AD) 授權端點，沒有任何伺服器對伺服器交換。 所有的驗證邏輯和工作階段處理會將完全 hello JavaScript 用戶端，而其他的頁面重新導向不放。

Azure AD B2C 擴充 hello 標準 OAuth 2.0 隱含流程 toomore 比簡單驗證及授權。 Azure AD B2C 導入了 hello[原則參數](active-directory-b2c-reference-policies.md)。 Hello 原則參數，您可以使用 OAuth 2.0 tooadd 使用者體驗 tooyour 應用程式，例如註冊、 登入及管理設定檔。 在本文中，我們為您示範如何 toouse hello 隱含流程和 Azure AD tooimplement 每個在單一頁面應用程式中的這些體驗。 toohelp 開始使用，看看我們[Node.js](https://github.com/Azure-Samples/active-directory-b2c-javascript-singlepageapp-nodejs-webapi)和[MICROSOFT.NET](https://github.com/Azure-Samples/active-directory-b2c-javascript-singlepageapp-dotnet-webapi)範例。

在本文中的 hello 範例 HTTP 要求，我們使用我們的範例 Azure AD B2C 目錄**fabrikamb2c.onmicrosoft.com**。此外，也會使用我們的範例應用程式和原則。 您可以嘗試 hello 要求您自己使用這些值，或您可以取代您自己的值。
了解如何太[取得自己的 Azure AD B2C 目錄、 應用程式，以及原則](#use-your-own-b2c-tenant)。


## <a name="protocol-diagram"></a>通訊協定圖表

hello 隱含登入流程看起來像下列圖 hello。 本文稍後 hello 詳細說明每個步驟。

![OpenID Connect 區隔線](../media/active-directory-v2-flows/convergence_scenarios_implicit.png)

## <a name="send-authentication-requests"></a>傳送驗證要求
當您的 web 應用程式需要 tooauthenticate hello 使用者，並執行原則時，它會導向 hello 使用者 toohello`/authorize`端點。 這是 hello 互動式部份 hello 流程其中 hello 使用者採取動作，視 hello 原則而定。 hello 使用者取得 ID 權杖從 hello Azure AD 端點。

在這項要求，hello 用戶端表示在 hello`scope`它需要從 hello 使用者 tooacquire 參數 hello 權限。 在 hello`p`參數，它會指出 hello 原則 tooexecute。 hello 下列三個範例 （使用分行符號來提高可讀性） 使用不同的原則。 tooget 的風格的每個要求的運作方式，然後嘗試貼上 hello 要求，到瀏覽器，並執行它。

### <a name="use-a-sign-in-policy"></a>使用登入原則
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=id_token+token
&redirect_uri=https%3A%2F%2Faadb2cplayground.azurewebsites.net%2F
&response_mode=fragment
&scope=openid%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&nonce=12345
&p=b2c_1_sign_in
```

### <a name="use-a-sign-up-policy"></a>使用註冊原則
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=id_token+token
&redirect_uri=https%3A%2F%2Faadb2cplayground.azurewebsites.net%2F
&response_mode=fragment
&scope=openid%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&nonce=12345
&p=b2c_1_sign_up
```

### <a name="use-an-edit-profile-policy"></a>使用編輯設定檔原則
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=id_token+token
&redirect_uri=https%3A%2F%2Faadb2cplayground.azurewebsites.net%2F
&response_mode=fragment
&scope=openid%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&nonce=12345
&p=b2c_1_edit_profile
```

| 參數 | 必要？ | 說明 |
| --- | --- | --- |
| client_id |必要 |hello 應用程式識別碼指派 tooyour 應用程式在 hello [Azure 入口網站](https://portal.azure.com)。 |
| response_type |必要 |必須包含 OpenID Connect 登入的 `id_token` 。 它也可以包含 hello 回應類型`token`。 如果您使用`token`，您的應用程式可以立即從 hello 接收存取權杖授權端點，而不需要進行第二個要求 toohello，授權端點。  如果您使用 hello`token`回應類型、 hello`scope`參數必須包含的範圍，指出哪些資源 tooissue hello 語彙基元。 |
| redirect_uri |建議 |hello 重新導向的應用程式，可以傳送及接收您的應用程式驗證回應的 URI。 它必須完全符合其中一個 hello 重新導向您在 hello 入口網站註冊 Uri 不同之處在於它必須以 URL 編碼。 |
| response_mode |建議 |指定 hello 方法 toouse toosend hello 產生語彙基元後 tooyour 應用程式。  針對隱含流程，請使用 `fragment`。 |
| scope |必要 |範圍的空格分隔清單。 單一領域值會表示 tooAzure AD 這兩個要求的 hello 權限。 hello`openid`範圍表示權限 toosign hello hello 表單的 ID 語彙基元中的 hello 使用者相關的使用者，以及如何取得資料中。 （我們將討論這更本文稍後 hello。）hello`offline_access`範圍都是選擇性的 web 應用程式。 它表示您的應用程式必須重新整理權杖的存留期長存取 tooresources。 |
| state |建議 |包含在 hello 要求也 hello 權杖回應中傳回的值。 它可以是您想要 toouse 任何內容的字串。 通常，會使用隨機產生的唯一值，tooprevent 跨網站要求偽造攻擊。 hello 狀態也是使用的 tooencode 資訊 hello 應用程式中的 hello 使用者狀態的相關發生 hello 驗證要求之前，像是 hello 頁面它們都上。 |
| nonce |必要 |值，包含在資料包含在 hello 產生的 ID 語彙基元宣告的形式 hello 要求 （由 hello 應用程式所產生）。 hello 應用程式然後確認此值 toomitigate 權杖重新執行攻擊。 通常，hello 值會是隨機的唯一字串，可以使用的 tooidentify hello 原點的 hello 要求。 |
| p |必要 |hello 原則 tooexecute。 它的 hello 的名稱會在您的 Azure AD B2C 租用戶中建立的原則。 hello 原則名稱值開頭應該是**b2c\_1\_**。 如需詳細資訊，請參閱 [Azure AD B2C 內建原則](active-directory-b2c-reference-policies.md)。 |
| prompt |選用 |使用者互動所需的 hello 型別。 目前，hello 唯一有效的值是`login`。 這會強制 hello 使用者 tooenter 他們的認證在該要求。 單一登入將沒有作用。 |

此時，會要求 hello 使用者 toocomplete hello 原則的工作流程。 這可能涉及 hello 使用者輸入使用者名稱和密碼，登入社交身分識別，註冊 hello 目錄或任何其他步驟數目。 使用者動作取決於定義 hello 原則的方式。

Hello 使用者完成 hello 原則之後，Azure AD 傳回的回應 tooyour 應用程式，在您所使用的 hello 值`redirect_uri`。 它會使用 hello 中指定的 hello 方法`response_mode`參數。 每個 hello 使用者動作案例，獨立於上次執行所執行的 hello 原則 hello 回應是完全 hello 相同。

### <a name="successful-response"></a>成功回應
成功的回應使用`response_mode=fragment`和`response_type=id_token+token`hello 下列程式碼，分行符號以利閱讀看起來像：

```
GET https://aadb2cplayground.azurewebsites.net/#
access_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
&token_type=Bearer
&expires_in=3599
&scope="90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6 offline_access",
&id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
&state=arbitrary_data_you_sent_earlier
```

| 參數 | 說明 |
| --- | --- |
| access_token |hello hello 應用程式要求存取權杖。  hello 存取權杖不應解碼或檢查。 其可被視為不透明的字串。 |
| token_type |hello 語彙基元型別值。 hello 只能輸入 Azure AD 支援的承載。 |
| expires_in |hello hello 存取權杖的時間長度 （以秒為單位） 無效。 |
| scope |hello 語彙基元的 hello 範圍無效。 您也可以使用範圍 toocache 語彙基元供以後使用。 |
| id_token |hello hello 應用程式要求的 ID 語彙基元。 您可以使用 hello ID 語彙基元 tooverify hello 使用者的身分識別，並開始與 hello 使用者工作階段。 如需 ID 語彙基元和其內容的詳細資訊，請參閱 hello [Azure AD B2C 權杖參照](active-directory-b2c-reference-tokens.md)。 |
| state |如果`state`參數包含在 hello 要求 hello 相同的值應該會出現在 hello 回應。 hello 應用程式應該確認該 hello `state` hello 要求和回應中的值完全相同。 |

### <a name="error-response"></a>錯誤回應
錯誤回應也可以為傳送 toohello 重新導向 URI，如此 hello 應用程式可以適當處理這些：

```
GET https://aadb2cplayground.azurewebsites.net/#
error=access_denied
&error_description=the+user+canceled+the+authentication
&state=arbitrary_data_you_can_receive_in_the_response
```

| 參數 | 說明 |
| --- | --- |
| 錯誤 |錯誤碼字串使用 tooclassify 類型發生的錯誤。 您也可以使用 hello 錯誤碼的錯誤處理。 |
| error_description |特定的錯誤訊息，可協助您找出 hello 的驗證錯誤的根本原因。 |
| state |請參閱 hello hello 上述資料表中的完整描述。 如果`state`參數包含在 hello 要求 hello 相同的值應該會出現在 hello 回應。 hello 應用程式應該確認該 hello `state` hello 要求和回應中的值完全相同。|

## <a name="validate-hello-id-token"></a>驗證 hello 的 ID 語彙基元
接收的 ID 語彙基元不足夠 tooauthenticate hello 使用者。 您必須驗證 hello 識別碼權杖之簽章，並確認每個應用程式需求的 hello 權杖中的 hello 宣告。 使用 azure AD B2C [JSON Web 權杖 (Jwt)](http://self-issued.info/docs/draft-ietf-oauth-json-web-token.html)和公用金鑰密碼編譯 toosign 語彙基元，並確認都有效。

許多開放原始碼程式庫無法驗證 Jwt，您可以根據 hello 語言偏好 toouse。 建議您探索可用的開放原始碼程式庫，而不是實作您自己的驗證邏輯。 您可以使用 hello 資訊在此發行項 toohelp 您了解 tooproperly 如何使用這些程式庫。

Azure AD B2C 具有 OpenID Connect 中繼資料端點。 應用程式可以在執行階段使用 hello 端點 toofetch Azure AD B2C 資訊。 這項資訊包括端點、權杖內容和權杖簽署金鑰。 您的 Azure AD B2C 租用戶中的每個原則都有一份 JSON 中繼資料文件。 例如，hello hello b2c_1_sign_in 原則 hello fabrikamb2c.onmicrosoft.com 租用戶中的中繼資料文件的位置是：

`https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/v2.0/.well-known/openid-configuration?p=b2c_1_sign_in`

此設定文件的 hello 屬性的其中一個為 hello `jwks_uri`。 相同的原則會被的 hello 的 hello 值：

`https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/discovery/v2.0/keys?p=b2c_1_sign_in`

toodetermine 哪些原則已使用的 toosign ID 權杖 （和其中 toofetch hello 從中繼資料），有兩個選項。 首先，hello 原則名稱包含在 hello`acr`中宣告`id_token`。 如需 tooparse hello 從 ID 權杖的宣告資訊，請參閱 hello [Azure AD B2C 權杖參照](active-directory-b2c-reference-tokens.md)。 另一個選擇是 tooencode hello hello 值中的 hello 原則`state`發出 hello 要求時的參數。 然後，解碼 hello`state`參數 toodetermine 用哪一個原則。 任一種方法都有效。

您已取得 hello 從 hello OpenID Connect 的中繼資料端點的中繼資料文件之後，您可以使用 hello RSA 256 （位於此端點） 的公開金鑰 toovalidate hello 簽章的 hello 的 ID 語彙基元。 此端點可能隨時會列出多個金鑰，每個都由 `kid` 所識別。 hello 標頭`id_token`也包含`kid`宣告。 它會指出哪個這些按鍵已使用的 toosign hello ID 語彙基元。 如需詳細資訊，包括了解[驗證權杖](active-directory-b2c-reference-tokens.md#token-validation)，請參閱 hello [Azure AD B2C 權杖參照](active-directory-b2c-reference-tokens.md)。
<!--TODO: Improve hello information on this-->

驗證簽章 hello hello 的 ID 語彙基元之後，數個宣告需要驗證。 例如：

* 驗證 hello`nonce`宣告 tooprevent 權杖重新執行攻擊。 其值必須為 hello 登入要求中指定的內容。
* 驗證 hello`aud`宣告 hello 的 ID 語彙基元的 tooensure 發行的應用程式。 其值必須為您的應用程式的 hello 應用程式識別碼。
* 驗證 hello`iat`和`exp`hello 的 ID 語彙基元的 tooensure 尚未過期的宣告。

在 hello 詳細地說明數個您應該執行的多個驗證[OpenID 連線核心規格](http://openid.net/specs/openid-connect-core-1_0.html)。Toovalidate 額外的宣告，也可以根據您的案例。 一些常見的驗證包括：

* 確保該 hello 使用者或組織已註冊 hello 應用程式。
* 確保該 hello 使用者具有適當的權限及權限。
* 確保驗證方式有一定的強度，例如使用 Azure Multi-Factor Authentication。

如需 ID 權杖中的 hello 宣告的詳細資訊，請參閱 hello [Azure AD B2C 權杖參照](active-directory-b2c-reference-tokens.md)。

您已完全驗證 hello 的 ID 語彙基元之後，您可以開始工作階段與 hello 使用者。 在應用程式中使用 hello 宣告在 hello ID 語彙基元 tooobtain hello 使用者資訊。 這項資訊可以用於顯示、記錄、授權等等。

## <a name="get-access-tokens"></a>取得存取權杖
如果您的 web 應用程式需求 toodo 是 hello 唯一執行原則，您可以略過 hello 接下來的章節。 適用於只有 tooweb 應用程式，需要驗證的 toomake 呼叫 tooa web API 的受保護的和 Azure AD B2C 的 hello 下列各節中的 hello 資訊。

既然您已登入 hello tooyour 單一頁面應用程式中的使用者，您可以呼叫 web Api 受到 Azure AD 取得存取權杖。 即使您已經使用 hello 收到權杖`token`回應類型，您可以使用此方法 tooacquire 語彙基元的其他資源不需要再次重新導向 hello 使用者 toosign 中的。

在典型的 web 應用程式流程中，您需要執行此動作藉由要求 toohello`/token`端點。  不過，hello 端點會不支援 CORS 要求，因此讓 AJAX 呼叫 tooget 並重新整理權杖不是可行。 相反地，您可以隱藏 HTML iframe 項目 tooget 新權杖使用 hello 隱含流程其他 web 應用程式開發介面。 以下是範例 (內含換行符號以利閱讀)：

```

https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=token
&redirect_uri=https%3A%2F%2Faadb2cplayground.azurewebsites.net%2F
&scope=https%3A%2F%2Fapi.contoso.com%2Ftasks.read
&response_mode=fragment
&state=arbitrary_data_you_can_receive_in_the_response
&nonce=12345
&prompt=none
&domain_hint=organizations
&login_hint=myuser@mycompany.com
&p=b2c_1_sign_in
```

| 參數 | 必要？ | 說明 |
| --- | --- | --- |
| client_id |必要 |hello 應用程式識別碼指派 tooyour 應用程式在 hello [Azure 入口網站](https://portal.azure.com)。 |
| response_type |必要 |必須包含 OpenID Connect 登入的 `id_token` 。  它也可以包含 hello 回應類型`token`。 如果您使用`token`這裡，您的應用程式可以立即存取權杖從接收 hello 授權端點，而不需要進行第二個要求 toohello，授權端點。 如果您使用 hello`token`回應類型、 hello`scope`參數必須包含的範圍，指出哪些資源 tooissue hello 語彙基元。 |
| redirect_uri |建議 |hello 重新導向的應用程式，可以傳送及接收您的應用程式驗證回應的 URI。 它必須完全符合 hello 重新導向 Uri 您 hello 入口網站中註冊的其中一個不同之處在於它必須以 URL 編碼。 |
| scope |必要 |範圍的空格分隔清單。  取得權杖，包含預期的 hello 資源所需的所有領域。 |
| response_mode |建議 |指定 hello 方法是使用的 toosend hello 產生語彙基元後 tooyour 應用程式。  可以是 `query`、`form_post` 或 `fragment`。 |
| state |建議 |包含在 hello 要求 hello 權杖回應中傳回的值。  它可以是您想要 toouse 任何內容的字串。  通常，會使用隨機產生的唯一值，tooprevent 跨網站要求偽造攻擊。  發生 hello 驗證要求之前，hello 狀態也是使用的 tooencode hello 應用程式中的 hello 使用者狀態資訊。 例如，已在 hello 頁面或檢視 hello 使用者。 |
| nonce |必要 |值，包含在 hello 要求中，隨附於 hello 產生的 ID 語彙基元宣告的形式 hello 應用程式所產生。  hello 應用程式然後確認此值 toomitigate 權杖重新執行攻擊。 通常，hello 值是可識別 hello hello 要求來源的隨機的唯一字串。 |
| prompt |必要 |toorefresh 和 get 語彙基元中隱藏的 iframe，使用`prompt=none`hello iframe 的 tooensure 不會不會卡在 hello 登入頁面上，並立即傳回。 |
| login_hint |必要 |在隱藏的 iframe，toorefresh 和 get 語彙基元中 hello 使用者可能必須在指定時間的多個工作階段之間此提示 toodistinguish 包含 hello hello 使用者名稱。 您可以從較早的登入擷取 hello 使用者名稱，使用 hello`preferred_username`宣告。 |
| domain_hint |必要 |可以是 `consumers` 或 `organizations`。  重新整理，並且在隱藏的 iframe 中取得權杖，您必須包含 hello `domain_hint` hello 要求中的值。  擷取 hello `tid` hello ID 語彙基元的先前登入 toodetermine 將來自宣告的值 toouse。  如果 hello`tid`宣告值是`9188040d-6c67-4c5b-b112-36a304b66dad`，使用`domain_hint=consumers`。  否則，使用 `domain_hint=organizations`。 |

所設定的 hello`prompt=none`參數，此要求是成功或失敗，並傳回 tooyour 應用程式。  成功的回應會傳送 tooyour 應用程式在 hello 指示重新導向 URI，使用 hello 中指定的 hello 方法`response_mode`參數。

### <a name="successful-response"></a>成功回應
使用 `response_mode=fragment` 的成功回應看起來像這樣：

```
GET https://aadb2cplayground.azurewebsites.net/#
access_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
&state=arbitrary_data_you_sent_earlier
&token_type=Bearer
&expires_in=3599
&scope=https%3A%2F%2Fapi.contoso.com%2Ftasks.read
```

| 參數 | 說明 |
| --- | --- |
| access_token |hello hello 應用程式要求的語彙基元。 |
| token_type |hello 語彙基元型別一律為持有者。 |
| state |如果`state`參數包含在 hello 要求 hello 相同的值應該會出現在 hello 回應。 hello 應用程式應該確認該 hello `state` hello 要求和回應中的值完全相同。 |
| expires_in |多久 hello 存取權杖是有效 （以秒為單位）。 |
| scope |hello 存取權杖的 hello 範圍無效。 |

### <a name="error-response"></a>錯誤回應
錯誤回應也可以為傳送 toohello 重新導向 URI，如此 hello 應用程式可以適當處理這些。  針對 `prompt=none`，預期的錯誤看起來像這樣：

```
GET https://aadb2cplayground.azurewebsites.net/#
error=user_authentication_required
&error_description=the+request+could+not+be+completed+silently
```

| 參數 | 說明 |
| --- | --- |
| 錯誤 |使用的 tooclassify 類型發生的錯誤可能會發生錯誤的程式碼字串。 您也可以使用 hello 字串 tooreact tooerrors。 |
| error_description |特定的錯誤訊息，可協助您找出 hello 的驗證錯誤的根本原因。 |

如果您收到這個錯誤 hello iframe 要求中，hello 使用者必須以互動方式登入一次 tooretrieve 新權杖。 您可以利用對應用程式有意義的方式來處理此錯誤。

## <a name="refresh-tokens"></a>重新整理權杖
識別碼權杖和存取權杖都會在短期內過期。 您的應用程式必須準備的 toorefresh 這些定期語彙基元。  toorefresh 任一類型的權杖中，執行 hello 同一個隱藏的 iframe 要求我們使用了先前範例中使用 hello`prompt=none`參數 toocontrol Azure AD 的步驟。  新的 tooreceive`id_token`值，是確定 toouse`response_type=id_token`和`scope=openid`，和`nonce`參數。

## <a name="send-a-sign-out-request"></a>傳送登出要求
當您想 toosign hello 使用者登出 hello 應用程式時，重新導向 hello 使用者 tooAzure AD toosign 出。如果不這麼做，hello 使用者可能無法 tooreauthenticate tooyour 應用程式，而不需重新輸入其認證。 這是因為使用者將擁有有效的 Azure AD 單一登入工作階段。

您可以只是重新導向 hello 使用者 toohello`end_session_endpoint`也就是相同的 OpenID Connect 中繼資料文件中所述的列在 hello[驗證 hello ID 語彙基元](#validate-the-id-token)。 例如：

```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/logout?
p=b2c_1_sign_in
&post_logout_redirect_uri=https%3A%2F%2Faadb2cplayground.azurewebsites.net%2F
```

| 參數 | 必要？ | 說明 |
| --- | --- | --- |
| p |必要 |hello 原則 toouse toosign hello 使用者登出您的應用程式。 |
| post_logout_redirect_uri |建議 |hello URL hello 使用者應重新導向的 tooafter 成功登出。如果您未包含，Azure AD B2C 會顯示一般訊息 toohello 使用者。 |

> [!NOTE]
> 導向 hello 使用者 toohello`end_session_endpoint`清除 hello 使用者單一登入狀態與 Azure AD B2C 部分。 不過，它不會簽署 hello 使用者登出 hello 使用者社交身分識別提供者工作階段。 如果 hello 使用者選取 hello 相同識別提供者在後續登入時，hello 使用者會重新驗證，而不需輸入他們的認證。 如果使用者想 toosign 超出您的 Azure AD B2C 應用程式時，它不一定表示他們想 toocompletely 登出他們的 Facebook 帳戶，例如。 不過，為本機帳戶，hello 使用者工作階段即將結束正確。
> 
> 

## <a name="use-your-own-azure-ad-b2c-tenant"></a>使用您自己的 Azure AD B2C 租用戶
這些要求，完成的 tootry hello 下列三個步驟。 取代您自己的值與本文章中我們使用 hello 範例值：

1. [建立 Azure AD B2C 租用戶](active-directory-b2c-get-started.md)。 Hello 要求中使用您的租用戶的 hello 名稱。
2. [建立應用程式](active-directory-b2c-app-registration.md)tooobtain 應用程式識別碼和`redirect_uri`值。 在應用程式中加入 Web 應用程式或 Web API。 (選擇性) 您可以建立應用程式祕密。
3. [建立您的原則](active-directory-b2c-reference-policies.md)tooobtain 原則名稱。

## <a name="samples"></a>範例

* [使用 Node.js 建立單一頁面應用程式](https://github.com/Azure-Samples/active-directory-b2c-javascript-singlepageapp-nodejs-webapi) \(英文\)
* [使用 .NET 建立單一頁面應用程式](https://github.com/Azure-Samples/active-directory-b2c-javascript-singlepageapp-dotnet-webapi) \(英文\)

