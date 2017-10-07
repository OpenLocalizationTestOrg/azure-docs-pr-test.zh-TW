---
title: "使用 OpenID Connect 的 Web 登入 - Azure AD B2C | Microsoft Docs"
description: "藉由使用 hello Azure Active Directory 實作 hello OpenID Connect 的驗證通訊協定建置 web 應用程式"
services: active-directory-b2c
documentationcenter: 
author: saeedakhter-msft
manager: krassk
editor: parakhj
ms.assetid: 21d420c8-3c10-4319-b681-adf2e89e7ede
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/16/2017
ms.author: saeedakhter-msft
ms.openlocfilehash: 89e9cfa28e4e5c34304aea355cca2dd0c4b42abc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-web-sign-in-with-openid-connect"></a>Azure Active Directory B2C：利用 OpenID Connect 的 Web 登入
OpenID Connect 是之上 OAuth 2.0，可以使用的 toosecurely 登入 tooweb 應用程式使用者的驗證通訊協定。 藉由使用 Azure Active Directory B2C hello OpenID Connect (Azure AD B2C) 實作，您可以將外包註冊、 登入和您的 web 應用程式 tooAzure Active Directory (Azure AD) 中的其他身分識別管理體驗。 本指南也說明如何 toodo 因此語言無關的方式。 它會描述如何 toosend 和接收 HTTP 訊息，而不使用任何我們開放原始碼程式庫。

[OpenID Connect](http://openid.net/specs/openid-connect-core-1_0.html)擴充 hello OAuth 2.0*授權*通訊協定，用來做*驗證*通訊協定。 這可讓您 tooperform 單一登入使用 OAuth。 它引進 hello 概念*ID 語彙基元*，這是安全性權杖，可讓 hello 用戶端 tooverify hello hello 使用者的身分識別，並取得 hello 使用者的基本設定檔資訊。

因為它可延伸 OAuth 2.0，它也可讓應用程式取得 toosecurely*存取權杖*。 您可以使用受保護的 access_tokens tooaccess 資源[授權伺服器](active-directory-b2c-reference-protocols.md#the-basics)。 如果您要建置的 Web 應用程式是裝載在伺服器上，且必須透過瀏覽器來存取，我們建議您使用 OpenID Connect。 如果您使用 Azure AD B2C 想 tooadd 身分識別管理 tooyour 行動或桌面應用程式，您應該使用[OAuth 2.0](active-directory-b2c-reference-oauth-code.md)而不是 OpenID Connect。

Azure AD B2C 擴充 hello 標準 OpenID Connect 通訊協定 toodo 多個簡單驗證及授權。 它會導致 hello[原則參數](active-directory-b2c-reference-policies.md)，可讓您 toouse OpenID Connect tooadd 使用者體驗-例如註冊、 登入及管理設定檔-tooyour 應用程式。 在這裡，我們為您示範如何 toouse OpenID Connect 和原則 tooimplement 每一種 web 應用程式中發生。 我們也會顯示您如何 tooget 存取權杖來存取 web 應用程式開發介面。

hello 下一節中的 hello 範例 HTTP 要求會使用我們的範例 B2C 目錄、 fabrikamb2c.onmicrosoft.com，以及我們的範例應用程式、 https://aadb2cplayground.azurewebsites.net 和原則。 您可以隨意 tootry 出 hello，要求您自己使用這些值，或您可以使用您自己取代它們。
了解如何太[取得自己 B2C 租用戶、 應用程式，以及原則](#use-your-own-b2c-directory)。

## <a name="send-authentication-requests"></a>傳送驗證要求
當您的 web 應用程式需要 tooauthenticate hello 使用者，並執行原則時，它可以直接 hello 使用者 toohello`/authorize`端點。 這是 hello 互動式部份 hello 流程其中 hello 使用者採取動作，視 hello 原則而定。

在此要求中，hello 用戶端指出它需要 hello hello 使用者 tooacquire hello 權限`scope`hello 中的參數和 hello 原則 tooexecute`p`參數。 三個範例會提供在 hello 下列各節 （使用分行符號來提高可讀性），每個使用不同的原則。 tooget 的風格的每個要求的運作方式，然後嘗試貼上 hello 要求，到瀏覽器，並執行它。

#### <a name="use-a-sign-in-policy"></a>使用登入原則
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=code+id_token
&redirect_uri=https%3A%2F%2Faadb2cplayground.azurewebsites.net%2F
&response_mode=form_post
&scope=openid%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&nonce=12345
&p=b2c_1_sign_in
```

#### <a name="use-a-sign-up-policy"></a>使用註冊原則
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=code+id_token
&redirect_uri=https%3A%2F%2Faadb2cplayground.azurewebsites.net%2F
&response_mode=form_post
&scope=openid%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&nonce=12345
&p=b2c_1_sign_up
```

#### <a name="use-an-edit-profile-policy"></a>使用編輯設定檔原則
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=code+id_token
&redirect_uri=https%3A%2F%2Faadb2cplayground.azurewebsites.net%2F
&response_mode=form_post
&scope=openid%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&nonce=12345
&p=b2c_1_edit_profile
```

| 參數 | 必要？ | 說明 |
| --- | --- | --- |
| client_id |必要 |hello 應用程式識別碼的 hello [Azure 入口網站](https://portal.azure.com/)指派 tooyour 應用程式。 |
| response_type |必要 |hello 回應類型，其中必須包括 OpenID connect 的 ID 語彙基元。 如果您的 Web 應用程式也需要權杖來呼叫 Web API，則可以使用 `code+id_token`，如同這裡的作法。 |
| redirect_uri |建議 |hello`redirect_uri`應用程式，可以傳送及接收您的應用程式驗證回應的參數。 它必須完全符合其中一個 hello`redirect_uri`您註冊 hello 入口網站中，不同之處在於它必須是 URL 編碼的參數。 |
| scope |必要 |範圍的空格分隔清單。 單一領域值會指出 tooAzure AD 要求這兩個權限。 hello`openid`範圍表示權限 toosign hello hello 表單的 ID 語彙基元 (詳細 toocome 這在本文稍後 hello) 中的 hello 使用者相關的使用者，以及如何取得資料中。 hello`offline_access`範圍都是選擇性的 web 應用程式。 它會指出您的應用程式將需要*重新整理權杖*如 tooresources 長時間執行的存取。 |
| response_mode |建議 |hello 應該使用的 toosend hello 產生授權程式碼後 tooyour 應用程式的方法。 它可以是 `query`、`form_post` 或 `fragment`。  hello`form_post`最佳安全性的建議回應模式。 |
| state |建議 |也會傳回 hello 權杖回應中的 hello 要求中包含一個值。 它可以是您所想要內容中的字串。 隨機產生的唯一值通常用於防止跨站台要求偽造攻擊。 之前發生 hello 驗證要求，例如 hello 頁上 hello 狀態也會使用的 tooencode hello 應用程式中的 hello 使用者狀態資訊。 |
| nonce |必要 |值，包含在資料將會包含在 hello 產生的 ID 語彙基元宣告的形式 hello 要求 （由 hello 應用程式所產生）。 hello 應用程式然後確認此值 toomitigate 權杖重新執行攻擊。 hello 值通常是隨機的唯一字串可能是使用的 tooidentify hello 原點的 hello 要求。 |
| p |必要 |將執行的 hello 原則。 它是原則的 hello 的名稱 B2C 租用戶中建立。 hello 原則名稱值開頭應該是`b2c\_1\_`。 了解原則與 hello[可延伸原則架構](active-directory-b2c-reference-policies.md)。 |
| prompt |選用 |使用者互動所需的 hello 型別。 hello 唯一有效的值，這次是`login`，強制 hello 使用者 tooenter 他們在該要求的認證。 單一登入將沒有作用。 |

此時，會要求 hello 使用者 toocomplete hello 原則的工作流程。 這可能涉及 hello 使用者輸入使用者名稱和密碼，登入社交身分識別，註冊 hello 目錄或其他任何數字的步驟，根據 hello 原則的定義方式。

Hello 使用者完成 hello 原則之後，Azure AD 會傳回回應 tooyour 應用程式，在指出的 hello`redirect_uri`參數，藉由指定 hello 中的 hello 方法`response_mode`參數。 hello 回應 hello 上述情況下，獨立於 hello 原則執行的每個 hello 相同。

使用 `response_mode=fragment` 的成功回應如下所示：

```
GET https://aadb2cplayground.azurewebsites.net/#
id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
&code=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...
&state=arbitrary_data_you_can_receive_in_the_response
```

| 參數 | 說明 |
| --- | --- |
| id_token |hello hello 應用程式要求的 ID 語彙基元。 您可以使用 hello ID 語彙基元 tooverify hello 使用者的身分識別，並開始與 hello 使用者工作階段。 ID 語彙基元和其內容的更多詳細資料會包含在 hello [Azure AD B2C 權杖參照](active-directory-b2c-reference-tokens.md)。 |
| code |hello 授權碼 hello 應用程式要求，如果您使用`response_type=code+id_token`。 hello 應用程式可用於目標資源的 hello 授權程式碼 toorequest 存取權杖。 授權碼的存留期很短。 通常會在大約 10 分鐘後過期。 |
| state |如果`state`參數包含在 hello 要求 hello 相同的值應該會出現在 hello 回應。 hello 應用程式應該確認該 hello `state` hello 要求和回應中的值完全相同。 |

錯誤回應也可以傳送 toohello`redirect_uri`參數，該 hello 應用程式可以適當地處理：

```
GET https://aadb2cplayground.azurewebsites.net/#
error=access_denied
&error_description=the+user+canceled+the+authentication
&state=arbitrary_data_you_can_receive_in_the_response
```

| 參數 | 說明 |
| --- | --- |
| 錯誤 |錯誤發生，而它可以是使用的 tooreact tooerrors 使用的 tooclassify 類型可能會錯誤程式碼字串。 |
| error_description |特定的錯誤訊息，可協助開發人員會識別 hello 的驗證錯誤的根本原因。 |
| state |請參閱本節中的 hello 第一個資料表中的 hello 完整描述。 如果`state`參數包含在 hello 要求 hello 相同的值應該會出現在 hello 回應。 hello 應用程式應該確認該 hello `state` hello 要求和回應中的值完全相同。 |

## <a name="validate-hello-id-token"></a>驗證 hello 的 ID 語彙基元
只接收 ID 語彙基元不足夠 tooauthenticate hello 使用者。 您必須驗證 hello 識別碼權杖之簽章，並確認每個應用程式需求的 hello 權杖中的 hello 宣告。 使用 azure AD B2C [JSON Web 權杖 (Jwt)](http://self-issued.info/docs/draft-ietf-oauth-json-web-token.html)和公用金鑰密碼編譯 toosign 語彙基元，並確認都有效。

視您偏好的語言而定，有許多針對驗證 JWT 的開放原始碼程式庫可用。 我們建議您探索這些程式庫，而不是實作您自己的驗證邏輯。 這裡 hello 資訊將有助於釐清 tooproperly 如何使用這些程式庫。

Azure AD B2C 所擁有的 OpenID Connect 中繼資料端點，可讓應用程式 toofetch 資訊需 Azure AD B2C 在執行階段。 這項資訊包括端點、權杖內容和權杖簽署金鑰。 您的 B2C 租用戶中的每個原則都有一份 JSON 中繼資料文件。 例如，hello 中繼資料文件以 hello`b2c_1_sign_in`中的原則`fabrikamb2c.onmicrosoft.com`位於：

`https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/v2.0/.well-known/openid-configuration?p=b2c_1_sign_in`

此設定文件的 hello 屬性的其中一個是`jwks_uri`，其值會是相同的原則中的 hello:

`https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/discovery/v2.0/keys?p=b2c_1_sign_in`。

toodetermine 哪些原則已用 ID 權杖簽章 （以及從 toofetch hello 中繼資料的位置），您有兩個選項。 首先，hello 原則名稱包含在 hello `acr` hello 識別碼權杖中宣告。 如需 tooparse hello 從 ID 權杖的宣告資訊，請參閱 hello [Azure AD B2C 權杖參照](active-directory-b2c-reference-tokens.md)。 另一個選擇是 tooencode hello hello 值中的 hello 原則`state`時發出 hello 要求然後解碼的 toodetermine 哪些原則已使用的參數。 任一種方法都有效。

您已取得 hello 從 hello OpenID Connect 的中繼資料端點的中繼資料文件之後，您可以使用 hello RSA 256 公用金鑰 （也就是位於此端點） 的 hello 的 ID 語彙基元 toovalidate hello 簽章。 此端點隨時都可能列出多個金鑰，每個金鑰都由 `kid` 宣告所識別。 hello hello 的 ID 語彙基元的標頭也包含`kid`宣告，表示已使用的 toosign hello ID 語彙基元的這些索引鍵。 如需詳細資訊，請參閱 hello [Azure AD B2C 權杖參照](active-directory-b2c-reference-tokens.md)(hello 區段上[驗證權杖](active-directory-b2c-reference-tokens.md#token-validation)，尤其)。
<!--TODO: Improve hello information on this-->

您已驗證的 hello 的 ID 語彙基元的 hello 簽章之後，有數個您需要 tooverify 的宣告。 例如：

* 您應該驗證 hello`nonce`宣告 tooprevent 權杖重新執行攻擊。 其值必須為 hello 登入要求中指定的內容。
* 您應該驗證 hello`aud`宣告 hello 的 ID 語彙基元的 tooensure 發行的應用程式。 其值必須為您的應用程式的 hello 應用程式識別碼。
* 您應該驗證 hello`iat`和`exp`hello 的 ID 語彙基元的 tooensure 尚未過期的宣告。

另外還有數個您應該執行的驗證。 在 hello 詳細說明這些[OpenID 連線核心規格](http://openid.net/specs/openid-connect-core-1_0.html)。Toovalidate 額外的宣告，也可以根據您的案例。 一些常見的驗證包括：

* 確保的 hello 使用者組織已註冊 hello 應用程式。
* 確保該 hello 使用者具有適當的授權/權限。
* 確保驗證方式有一定的強度，例如 Azure Multi-Factor Authentication。

如需有關識別碼權杖中的 hello 宣告的詳細資訊，請參閱 hello [Azure AD B2C 權杖參照](active-directory-b2c-reference-tokens.md)。

您已驗證 hello 的 ID 語彙基元之後，您可以開始工作階段與 hello 使用者。 您可以在 hello ID 語彙基元 tooobtain hello 使用者資訊，您的應用程式中使用 hello 宣告。 這項資訊的用途包括顯示、記錄和授權。

## <a name="get-a-token"></a>取得權杖
如果您需要您的 web 應用程式 tooonly 執行原則，您可以略過 hello 接下來的章節。 這些區段分別是需要 toomake 驗證呼叫 tooa web API，也會受 Azure AD B2C 適用的唯一 tooweb 應用程式。

您可以兌換 hello 貴用戶取得的授權碼 (使用`response_type=code+id_token`) 權杖 toohello 所需資源，藉由傳送`POST`要求 toohello`/token`端點。 目前，hello 您可以要求的語彙基元的資源是您的應用程式本身的後端 web 應用程式開發介面。 要求語彙基元 tooyourself hello 慣例是的 toouse 應用程式的用戶端識別碼 hello 範圍為：

```
POST fabrikamb2c.onmicrosoft.com/oauth2/v2.0/token?p=b2c_1_sign_in HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

grant_type=authorization_code&client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6&scope=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6 offline_access&code=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...&redirect_uri=urn:ietf:wg:oauth:2.0:oob&client_secret=<your-application-secret>

```

| 參數 | 必要？ | 說明 |
| --- | --- | --- |
| p |必要 |hello 原則來使用的 tooacquire hello 授權程式碼。 您無法在此要求中使用不同的原則。 請注意，您會加入這個參數 toohello 查詢字串，不 toohello`POST`主體。 |
| client_id |必要 |hello 應用程式識別碼的 hello [Azure 入口網站](https://portal.azure.com/)指派 tooyour 應用程式。 |
| grant_type |必要 |hello 的授與，必須是類型`authorization_code`的 hello 授權碼流程。 |
| scope |建議 |範圍的空格分隔清單。 單一領域值會指出 tooAzure AD 要求這兩個權限。 hello`openid`範圍表示權限 toosign hello hello id_token 參數形式的 hello 使用者相關的使用者，以及如何取得資料中。 它可以是使用的 tooget 語彙基元 tooyour 應用程式本身的後端 web 應用程式開發介面，由 hello 表示相同的應用程式識別碼 hello 用戶端。 hello`offline_access`範圍表示您的應用程式，將會需要長時間執行的存取 tooresources 重新整理權杖。 |
| code |必要 |貴用戶取得 hello 流程 hello 第一個階段中的 hello 授權碼。 |
| redirect_uri |必要 |hello `redirect_uri` hello 應用程式，您收到 hello 授權程式碼的參數。 |
| client_secret |必要 |您在 hello 中產生的 hello 應用程式密碼[Azure 入口網站](https://portal.azure.com/)。 這個應用程式密碼是重要的安全性構件， 您應該要用安全的方法把它儲存在您的伺服器上。 您也應該定期輪換此用戶端祕密。 |

成功的權杖回應看起來如下：

```
{
    "not_before": "1442340812",
    "token_type": "Bearer",
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...",
    "scope": "90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6 offline_access",
    "expires_in": "3600",
    "refresh_token": "AAQfQmvuDy8WtUv-sd0TBwWVQs1rC-Lfxa_NDkLqpg50Cxp5Dxj0VPF1mx2Z...",
}
```
| 參數 | 說明 |
| --- | --- |
| not_before |hello 時間在哪一個 hello 語彙基元會被視為有效的在 epoch 時間。 |
| token_type |hello 語彙基元型別值。 hello Azure AD 支援的類型`Bearer`。 |
| access_token |hello 簽署 JWT 權杖要求。 |
| scope |hello 的 hello 權杖是有效的範圍。 這些可用來快取權杖，供以後使用。 |
| expires_in |hello hello 存取權杖的時間長度 （以秒為單位） 無效。 |
| refresh_token |OAuth 2.0 重新整理權杖。 hello 目前的語彙基元過期之後，hello 應用程式可以使用這個語彙基元 tooacquire 其他語彙基元。 重新整理權杖存留較久，而且可以是使用的 tooretain 存取 tooresources 很長的時間。 如需詳細資訊，請參閱 toohello [B2C 權杖參照](active-directory-b2c-reference-tokens.md)。 請注意，您必須擁有使用 hello 範圍`offline_access`在 hello 授權和語彙基元要求順序 tooreceive 中重新整理權杖。 |

錯誤回應看起來如下：

```
{
    "error": "access_denied",
    "error_description": "hello user revoked access toohello app.",
}
```

| 參數 | 說明 |
| --- | --- |
| 錯誤 |錯誤發生，而它可以是使用的 tooreact tooerrors 使用的 tooclassify 類型可能會錯誤程式碼字串。 |
| error_description |特定的錯誤訊息，可協助開發人員會識別 hello 的驗證錯誤的根本原因。 |

## <a name="use-hello-token"></a>使用 hello 語彙基元
既然您已成功取得存取權杖，您可以使用要求 tooyour 後端 web 應用程式開發介面的 hello 語彙基元併入 hello`Authorization`標頭：

```
GET /tasks
Host: https://mytaskwebapi.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
```

## <a name="refresh-hello-token"></a>重新整理 hello 語彙基元
識別碼權杖只會短暫存在。 在到期 toocontinue 所能 tooaccess 資源之後，您必須更新它們。 您可以藉由送出另一個`POST`要求 toohello`/token`端點。 此時，提供 hello`refresh_token`參數而 hello`code`參數：

```
POST fabrikamb2c.onmicrosoft.com/oauth2/v2.0/token?p=b2c_1_sign_in HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

grant_type=refresh_token&client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6&scope=openid offline_access&refresh_token=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...&redirect_uri=urn:ietf:wg:oauth:2.0:oob&client_secret=<your-application-secret>
```

| 參數 | 必要 | 說明 |
| --- | --- | --- |
| p |必要 |已使用的 tooacquire hello 原始重新整理權杖的 hello 原則。 您無法在此要求中使用不同的原則。 請注意，您會加入這個參數 toohello 查詢字串、 toohello POST 本文。 |
| client_id |必要 |hello 應用程式識別碼的 hello [Azure 入口網站](https://portal.azure.com/)指派 tooyour 應用程式。 |
| grant_type |必要 |授與，必須重新整理權杖的此階段的 hello 授權碼流程 hello 型別。 |
| scope |建議 |範圍的空格分隔清單。 單一領域值會指出 tooAzure AD 要求這兩個權限。 hello`openid`範圍表示權限 toosign hello hello 表單的 ID 語彙基元中的 hello 使用者相關的使用者，以及如何取得資料中。 它可以是使用的 tooget 語彙基元 tooyour 應用程式本身的後端 web 應用程式開發介面，由 hello 表示相同的應用程式識別碼 hello 用戶端。 hello`offline_access`範圍表示您的應用程式，將會需要長時間執行的存取 tooresources 重新整理權杖。 |
| redirect_uri |建議 |hello `redirect_uri` hello 應用程式，您收到 hello 授權程式碼的參數。 |
| refresh_token |必要 |hello 原始重新整理語彙基元，貴用戶取得 hello 流程 hello 第二個階段中。 請注意，您必須擁有使用 hello 範圍`offline_access`在 hello 授權和語彙基元要求順序 tooreceive 中重新整理權杖。 |
| client_secret |必要 |您在 hello 中產生的 hello 應用程式密碼[Azure 入口網站](https://portal.azure.com/)。 這個應用程式密碼是重要的安全性構件， 您應該要用安全的方法把它儲存在您的伺服器上。 您也應該定期輪換此用戶端祕密。 |

成功的權杖回應看起來如下：

```
{
    "not_before": "1442340812",
    "token_type": "Bearer",
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...",
    "scope": "90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6 offline_access",
    "expires_in": "3600",
    "refresh_token": "AAQfQmvuDy8WtUv-sd0TBwWVQs1rC-Lfxa_NDkLqpg50Cxp5Dxj0VPF1mx2Z...",
}
```
| 參數 | 說明 |
| --- | --- |
| not_before |hello 時間在哪一個 hello 語彙基元會被視為有效的在 epoch 時間。 |
| token_type |hello 語彙基元型別值。 hello Azure AD 支援的類型`Bearer`。 |
| access_token |hello 簽署 JWT 權杖要求。 |
| scope |hello 語彙基元的 hello 範圍是有效的它可以用來快取權杖供以後使用。 |
| expires_in |hello hello 存取權杖的時間長度 （以秒為單位） 無效。 |
| refresh_token |OAuth 2.0 重新整理權杖。 hello 目前的語彙基元過期之後，hello 應用程式可以使用這個語彙基元 tooacquire 其他語彙基元。  重新整理權杖存留較久，而且可以是使用的 tooretain 存取 tooresources 很長的時間。 如需詳細資訊，請參閱 toohello [B2C 權杖參照](active-directory-b2c-reference-tokens.md)。 |

錯誤回應看起來如下：

```
{
    "error": "access_denied",
    "error_description": "hello user revoked access toohello app.",
}
```

| 參數 | 說明 |
| --- | --- |
| 錯誤 |錯誤發生，而它可以是使用的 tooreact tooerrors 使用的 tooclassify 類型可能會錯誤程式碼字串。 |
| error_description |特定的錯誤訊息，可協助開發人員會識別 hello 的驗證錯誤的根本原因。 |

## <a name="send-a-sign-out-request"></a>傳送登出要求
當您想 toosign hello 使用者登出 hello 應用程式時，您的應用程式 cookie 是不足 tooclear 或否則結束 hello 與 hello 使用者的工作階段。 您也必須重新導向 hello 使用者 tooAzure AD toosign 出。如果您讓容錯 toodo，hello 使用者可能無法 tooreauthenticate tooyour 應用程式，而不需重新輸入其認證。 這是因為使用者將擁有有效的 Azure AD 單一登入工作階段。

您可以只是重新導向 hello 使用者 toohello `end_session` hello OpenID Connect 的中繼資料文件中所列的端點稍早所述 hello 「 驗證 hello 的 ID 語彙基元 」 一節：

```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/logout?
p=b2c_1_sign_in
&post_logout_redirect_uri=https%3A%2F%2Faadb2cplayground.azurewebsites.net%2F
```

| 參數 | 必要？ | 說明 |
| --- | --- | --- |
| p |必要 |您要從您的應用程式的 toouse toosign hello 使用者 hello 原則。 |
| post_logout_redirect_uri |建議 |hello URL hello 使用者應重新導向的 tooafter 成功登出。如果您未包含，Azure AD B2C 顯示 hello 使用者一般訊息。 |

> [!NOTE]
> 雖然導向 hello 使用者 toohello`end_session`端點將會清除某些 hello 使用者單一登入狀態與 Azure AD B2C，它都不會簽署 hello 使用者登出其社交身分識別提供者 (IDP) 工作階段。 如果 hello 使用者選取相同的 IDP hello 在後續登入時，他們將會重新驗證，而不需輸入他們的認證。 如果使用者想 toosign B2C 應用程式時，它不一定表示他們想 toosign 超出其 Facebook 帳戶。 不過，在 hello 案例中的本機帳戶，hello 使用者工作階段即將結束正確。
> 
> 

## <a name="use-your-own-b2c-tenant"></a>使用您自己的 B2C 租用戶
如果您想 tootry 這些要求自行，您必須先執行這三個步驟，並接著取代稍早所述，使用您自己的 hello 範例值：

1. [建立 B2C 租用戶](active-directory-b2c-get-started.md)，並使用您的租用戶的 hello 名稱 hello 要求中。
2. [建立應用程式](active-directory-b2c-app-registration.md)tooobtain 應用程式識別碼。 在應用程式中加入 Web 應用程式/Web API。 也可以選擇建立應用程式祕密。
3. [建立您的原則](active-directory-b2c-reference-policies.md)tooobtain 原則名稱。

