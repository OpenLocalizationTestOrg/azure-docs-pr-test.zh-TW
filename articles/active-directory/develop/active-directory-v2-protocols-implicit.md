---
title: "使用 Azure AD hello v2.0 隱含流程 aaaSecure 單一頁面應用程式 |Microsoft 文件"
description: "建立 web 應用程式的單一頁面應用程式中使用 Azure AD 的 v2.0 實作 hello 隱含流程。"
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 3605931f-dc24-4910-bb50-5375defec6a8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 2cdce4eee88be4af54966d15204b79fa4992a58e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# 2.0 版通訊協定-SPAs 使用 hello 隱含流程
與 hello v2.0 端點，您可以登入您的單一頁面應用程式與個人和工作/學校帳戶，從 Microsoft 的使用者。  單一網頁和其他 JavaScript 應用程式中執行的主要是有趣的一些挑戰時的瀏覽器字體它有 tooauthentication:

* 這些應用程式的 hello 安全性特性會明顯不同於傳統伺服器為基礎的 web 應用程式。
* 許多授權伺服器與身分識別提供者不支援 CORS 要求。
* 完整的網頁瀏覽器重新導向遠離 hello 應用程式變得特別侵入性功能 toohello 使用者經驗。

這些應用程式 (認為： AngularJS、 Ember.js、 React.js，等等) Azure AD 支援 hello OAuth 2.0 隱含授予流程。  hello 隱含流程述 hello [OAuth 2.0 規格](http://tools.ietf.org/html/rfc6749#section-4.2)。  其主要的好處是，它可讓 hello 應用程式 tooget 語彙基元從 Azure AD 而不需執行後端伺服器的認證交換。  這可以讓使用者 hello hello 應用程式 toosign、 維護工作階段，以及取得全部都在 hello 用戶端 JavaScript 程式碼內的語彙基元 tooother web Api。  特別是大約使用隱含流程 hello-時，並納入考量的幾個重要的安全性考量 tootake[用戶端](http://tools.ietf.org/html/rfc6749#section-10.3)和[使用者模擬](http://tools.ietf.org/html/rfc6749#section-10.3)。

如果您希望 toouse hello 隱含流程和 Azure AD tooadd 驗證 tooyour JavaScript 應用程式，我們建議您使用我們的開放原始碼 JavaScript 程式庫， [adal.js](https://github.com/AzureAD/azure-activedirectory-library-for-js)。  有幾個 AngularJS 教學課程[這裡](active-directory-appmodel-v2-overview.md#getting-started)toohelp 您立即開始。  

不過，如果您想使用 toouse 文件庫中單一頁面應用程式，並將傳送通訊協定訊息自己，請遵循 hello 下列的一般步驟。

> [!NOTE]
> 並非所有的 Azure Active Directory 案例和功能都受到 hello v2.0 端點。  toodetermine 如果應該使用 hello v2.0 端點，閱讀有關[v2.0 限制](active-directory-v2-limitations.md)。
> 
> 

## 通訊協定圖表
hello 整個隱含的登入流程看起來類似下面的-hello 步驟詳述於下面的詳細資料。

![OpenId Connect 區隔線](../../media/active-directory-v2-flows/convergence_scenarios_implicit.png)

## 傳送 hello 登入要求
tooinitially 登入您的應用程式 hello 使用者，您可以傳送[OpenID Connect](active-directory-v2-protocols-oidc.md)授權要求，以及如何取得`id_token`從 hello v2.0 端點：

```
// Line breaks for legibility only

https://login.microsoftonline.com/{tenant}/oauth2/v2.0/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&response_type=id_token+token
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&scope=openid%20https%3A%2F%2Fgraph.microsoft.com%2Fmail.read
&response_mode=fragment
&state=12345
&nonce=678910
```

> [!TIP]
> 按一下下方 tooexecute hello 連結，此要求 ！ 登入之後，您的瀏覽器應該重新導向太`https://localhost/myapp/`與`id_token`hello 網址列中。
> <a href="https://login.microsoftonline.com/common/oauth2/v2.0/authorize?client_id=6731de76-14a6-49ae-97bc-6eba6914391e&response_type=id_token+token&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F&scope=openid%20https%3A%2F%2Fgraph.microsoft.com%2Fmail.read&response_mode=fragment&state=12345&nonce=678910" target="_blank">https://login.microsoftonline.com/common/oauth2/v2.0/authorize...</a>
> 
> 

| 參數 |  | 說明 |
| --- | --- | --- |
| tenant |必要 |hello `{tenant}` hello hello 要求路徑中的值可以是使用的 toocontrol 可以登入 hello 應用程式。  hello 允許的值為`common`， `organizations`， `consumers`，和租用戶識別碼。  如需更多詳細資訊，請參閱 [通訊協定基本概念](active-directory-v2-protocols.md#endpoints)。 |
| client_id |必要 |hello 該 hello 註冊入口網站的應用程式識別碼 ([apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)) 指派給您的應用程式。 |
| response_type |必要 |必須包含 OpenID Connect 登入的 `id_token` 。  它也可以包含 hello response_type `token`。 使用`token`這裡可讓您的應用程式 tooreceive hello 立即存取權杖授權端點，而不需要的 toomake 第二個要求 toohello 授權端點。  如果您使用 hello `token` response_type，hello`scope`參數必須包含範圍，指出哪些資源 tooissue hello 語彙基元。 |
| redirect_uri |建議使用 |hello redirect_uri 應用程式，可以傳送及接收您的應用程式驗證回應。  它必須完全符合其中一個 hello redirect_uris 您註冊 hello 入口網站，但它必須是 url 編碼。 |
| scope |必要 |範圍的空格分隔清單。  OpenID Connect，它必須包含 hello 範圍`openid`，會轉譯為 hello 同意 UI 中的 toohello 「 將您登入 」 權限。  （選擇性） 您可能也想 tooinclude hello`email`或`profile`[範圍](active-directory-v2-scopes.md)獲得存取 tooadditional 使用者資料。  您也可能要求同意 toovarious 資源在此要求中包含其他範圍。 |
| response_mode |建議使用 |指定應該使用的 toosend hello 產生語彙基元後 tooyour 應用程式的 hello 方法。  應該是`fragment`hello 隱含流程。 |
| state |建議使用 |Hello 權杖回應中也會傳回的 hello 要求中包含一個值。  其可以是您想要之任何內容的字串。  隨機產生的唯一值通常用於 [防止跨站台偽造要求攻擊](http://tools.ietf.org/html/rfc6749#section-10.12)。  之前發生 hello 驗證要求，例如 hello 頁面或檢視上 hello 狀態也會使用的 tooencode hello 應用程式中的 hello 使用者狀態資訊。 |
| nonce |必要 |值，包含在 hello 要求中，將會包含在宣告的形式 hello 產生 id_token hello 應用程式所產生。  hello 應用程式然後確認此值 toomitigate 權杖重新執行攻擊。  hello 值通常是隨機的唯一字串，可以使用的 tooidentify hello 原點的 hello 要求。 |
| prompt |選用 |指出 hello 類型所需使用者互動。  只有在這個階段的有效值為 'none'、 '登入' hello' 表示同意 '。  `prompt=login`強制 hello 使用者 tooenter 將該要求時，停止單一登入認證。  `prompt=none`是 hello 相反-它可確保該 hello 使用者不提供任何互動式提示恕不另行通知。  如果 hello 無法完成要求，以無訊息方式透過單一登入，hello v2.0 端點會傳回錯誤。  `prompt=consent`將觸發程序 hello OAuth 同意對話方塊之後 hello 使用者登入時，要求 hello 使用者 toogrant 權限 toohello 應用程式。 |
| login_hint |選用 |可以是使用的 toopre 填滿 hello 使用者名稱/電子郵件地址欄位的 hello 登入頁面 hello 使用者，如果您知道事先其使用者名稱。  通常應用程式會使用此參數重新在驗證期間，從先前的登入需要擷取 hello 使用者名稱使用 hello`preferred_username`宣告。 |
| domain_hint |選用 |可以是 `consumers` 或 `organizations` 其中一個。  如果包含，它會略過 hello 電子郵件為基礎的探索程序的使用者經歷了在 hello v2.0 登入頁面上，導致 tooa 稍微簡化使用者經驗。  通常應用程式會使用重新在驗證期間，此參數以擷取 hello `tid` hello id_token 將來自宣告。  如果 hello`tid`宣告值是`9188040d-6c67-4c5b-b112-36a304b66dad`，您應該使用`domain_hint=consumers`。  否則，使用 `domain_hint=organizations`。 |

Hello 使用者將會在此時，系統要求 tooenter 其認證和驗證完成 hello。  hello v2.0 端點也會確保該 hello 使用者同意 toohello hello 中指出的權限`scope`查詢參數。  如果 hello 使用者不同意 tooany 權限，它會要求 hello 使用者 tooconsent toohello 所需的權限。  [這裡提供權限、同意與多租用戶應用程式](active-directory-v2-scopes.md)的詳細資料。

一旦 hello 使用者驗證，並授與同意，hello v2.0 端點會傳回回應 tooyour 應用程式，在指出的 hello `redirect_uri`，使用 hello 中指定的 hello 方法`response_mode`參數。

#### 成功回應
成功的回應使用`response_mode=fragment`和`response_type=id_token+token`hello 下列程式碼，分行符號以利閱讀看起來像：

```
GET https://localhost/myapp/#
access_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
&token_type=Bearer
&expires_in=3599
&scope=https%3a%2f%2fgraph.microsoft.com%2fmail.read 
&id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
&state=12345
```

| 參數 | 說明 |
| --- | --- |
| access_token |如果 `response_type` 包含 `token` 則納入。 hello hello 要求，應用程式的存取權杖在此情況下的 hello Microsoft Graph。  hello 存取權杖不應解碼或檢查，可以將它視為不透明的字串。 |
| token_type |如果 `response_type` 包含 `token` 則納入。  一律為 `Bearer`。 |
| expires_in |如果 `response_type` 包含 `token` 則納入。  指出 hello hello 權杖是有效的快取用途的秒數。 |
| scope |如果 `response_type` 包含 `token` 則納入。  指出 hello 範圍的 hello access_token 才有效。 |
| id_token |hello id_token hello 要求的應用程式。 您可以使用 hello id_token tooverify hello 使用者的身分識別，並開始與 hello 使用者工作階段。  Id_tokens 和其內容的更多詳細資料包含在 hello [v2.0 端點權杖參照](active-directory-v2-tokens.md)。 |
| state |如果在 hello 要求中，相同的值應該會出現在 hello 回應 hello 包含狀態參數。 hello 應用程式應該確認 hello 要求和回應中的 hello 狀態值完全相同。 |

#### 錯誤回應
錯誤回應也可能會傳送 toohello`redirect_uri`讓 hello 應用程式可以適當地處理：

```
GET https://localhost/myapp/#
error=access_denied
&error_description=the+user+canceled+the+authentication
```

| 參數 | 說明 |
| --- | --- |
| 錯誤 |錯誤的程式碼字串是使用的 tooclassify 類型之錯誤的發生，且可以使用的 tooreact tooerrors。 |
| error_description |特定的錯誤訊息，可協助開發人員會識別 hello 的驗證錯誤的根本原因。 |

## 驗證 hello id_token
只接收 id_token 不足夠 tooauthenticate hello 使用者;您必須驗證 hello id_token 簽章，並確認每個應用程式需求的 hello 權杖中的 hello 宣告。  hello v2.0 端點會使用[JSON Web 權杖 (Jwt)](http://self-issued.info/docs/draft-ietf-oauth-json-web-token.html)和公用金鑰密碼編譯 toosign 語彙基元，並確認都有效。

您可以選擇 toovalidate hello`id_token`中用戶端程式碼，但常見作法是將 toosend hello `id_token` tooa 後端伺服器並執行那里 hello 驗證。  一旦您已驗證的 hello id_token hello 簽章，有幾個您將會需要的 tooverify 的宣告。  請參閱 hello [v2.0 權杖參照](active-directory-v2-tokens.md)如需詳細資訊，包括[驗證語彙基元](active-directory-v2-tokens.md#validating-tokens)和[重要資訊有關簽署金鑰變換](active-directory-v2-tokens.md#validating-tokens)。  我們建議利用程式庫來剖析和驗證權杖 - 對於大部分語言和平台至少有一個可用。
<!--TODO: Improve hello information on this-->

您可能也想 toovalidate 宣告的其他宣告根據您的案例。  一些常見的驗證包括：

* 確保 hello 使用者組織已註冊 hello 應用程式。
* 確保以下人員 hello 使用者擁有適當的授權/權限
* 確保驗證具有特定強度，例如多重要素驗證。

如需有關在 id_token hello 宣告的詳細資訊，請參閱 hello [v2.0 端點權杖參照](active-directory-v2-tokens.md)。

一旦您已完全驗證 hello id_token，您可以開始與 hello 使用者工作階段，並使用 hello id_token tooobtain hello 使用者資訊中的 hello 宣告，在您的應用程式。  這項資訊可以用於顯示、記錄、授權等等。

## 取得存取權杖
既然您已簽署 hello 使用者到單一頁面應用程式，您可以取得存取權杖呼叫 web Api 受到 Azure AD，例如 hello [Microsoft Graph](https://graph.microsoft.io)。  即使您已經收到的權杖使用 hello `token` response_type，您可以使用此方法 tooacquire 語彙基元 tooadditional 資源不用 tooredirect hello 使用者 toosign 一次。

在 hello 正常 OpenID Connect/OAuth 流程中，您需要執行此動作藉由要求 toohello v2.0`/token`端點。  不過，hello v2.0 端點會不支援 CORS 要求，因此讓 AJAX 呼叫 tooget 並重新整理語彙基元超出 hello 問題。  相反地，您可以使用隱藏的 iframe tooget 新權杖中的 hello 隱含流程，其他 web 應用程式開發介面： 

```
// Line breaks for legibility only

https://login.microsoftonline.com/{tenant}/oauth2/v2.0/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&response_type=token
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&scope=https%3A%2F%2Fgraph.microsoft.com%2Fmail.read&response_mode=fragment
&state=12345&nonce=678910
&prompt=none
&domain_hint=organizations
&login_hint=myuser@mycompany.com
```

> [!TIP]
> 嘗試複製和貼入瀏覽器索引標籤下方要求 hello ！ (請不要忘記 tooreplace hello`domain_hint`和 hello `login_hint` hello 與值可修正您的使用者的值)
> 
> 

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize?client_id=6731de76-14a6-49ae-97bc-6eba6914391e&response_type=token&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F&scope=https%3A%2F%2Fgraph.microsoft.com%2Fmail.read&response_mode=fragment&state=12345&nonce=678910&prompt=none&domain_hint={{consumers-or-organizations}}&login_hint={{your-username}}
```

| 參數 |  | 說明 |
| --- | --- | --- |
| tenant |必要 |hello `{tenant}` hello hello 要求路徑中的值可以是使用的 toocontrol 可以登入 hello 應用程式。  hello 允許的值為`common`， `organizations`， `consumers`，和租用戶識別碼。  如需更多詳細資訊，請參閱 [通訊協定基本概念](active-directory-v2-protocols.md#endpoints)。 |
| client_id |必要 |hello 該 hello 註冊入口網站的應用程式識別碼 ([apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)) 指派給您的應用程式。 |
| response_type |必要 |必須包含 OpenID Connect 登入的 `id_token` 。  它也可能包含其他 response_types，例如 `code`。 |
| redirect_uri |建議使用 |hello redirect_uri 應用程式，可以傳送及接收您的應用程式驗證回應。  它必須完全符合其中一個 hello redirect_uris 您註冊 hello 入口網站，但它必須是 url 編碼。 |
| scope |必要 |範圍的空格分隔清單。  如需入門語彙基元，包含所有[範圍](active-directory-v2-scopes.md)感興趣的 hello 資源所需。 |
| response_mode |建議使用 |指定應該使用的 toosend hello 產生語彙基元後 tooyour 應用程式的 hello 方法。  可以是 `query`、`form_post` 或 `fragment` 其中一個。 |
| state |建議使用 |Hello 權杖回應中也會傳回的 hello 要求中包含一個值。  其可以是您想要之任何內容的字串。  隨機產生的唯一值通常用於防止跨站台要求偽造攻擊。  之前發生 hello 驗證要求，例如 hello 頁面或檢視上 hello 狀態也會使用的 tooencode hello 應用程式中的 hello 使用者狀態資訊。 |
| nonce |必要 |值，包含在 hello 要求中，將會包含在宣告的形式 hello 產生 id_token hello 應用程式所產生。  hello 應用程式然後確認此值 toomitigate 權杖重新執行攻擊。  hello 值通常是隨機的唯一字串，可以使用的 tooidentify hello 原點的 hello 要求。 |
| prompt |必要 |重新整理 （& s） 在隱藏的 iframe 中取得權杖，您應該使用`prompt=none`hello iframe 的 tooensure 不在 hello v2.0 登入頁面上，不會停止回應，並立即傳回。 |
| login_hint |必要 |重新整理 （& s） 在隱藏的 iframe 中取得權杖，您必須包含 hello hello 使用者名稱中 hello 使用者在時間中，可能會有特定時點的多個工作階段之間的順序 toodistinguish 此提示中。 您可以擷取 hello 使用者名稱，從先前的登入使用 hello`preferred_username`宣告。 |
| domain_hint |必要 |可以是 `consumers` 或 `organizations` 其中一個。  重新整理 （& s） 在隱藏的 iframe 中取得權杖，您必須包含 hello domain_hint hello 要求中。  您應該擷取 hello`tid`從先前的登入 toodetermine 的 hello id_token 哪些值 toouse 的宣告。  如果 hello`tid`宣告值是`9188040d-6c67-4c5b-b112-36a304b66dad`，您應該使用`domain_hint=consumers`。  否則，使用 `domain_hint=organizations`。 |

謝謝 toohello`prompt=none`參數，此要求會是成功或失敗立即，並傳回 tooyour 應用程式。  成功的回應將 tooyour 應用程式傳送 hello 指示在`redirect_uri`，使用 hello 中指定的 hello 方法`response_mode`參數。

#### 成功回應
使用 `response_mode=fragment` 的成功回應如下所示：

```
GET https://localhost/myapp/#
access_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
&state=12345
&token_type=Bearer
&expires_in=3599
&scope=https%3A%2F%2Fgraph.windows.net%2Fdirectory.read
```

| 參數 | 說明 |
| --- | --- |
| access_token |hello hello 應用程式要求的語彙基元。 |
| token_type |一律為 `Bearer`。 |
| state |如果在 hello 要求中，相同的值應該會出現在 hello 回應 hello 包含狀態參數。 hello 應用程式應該確認 hello 要求和回應中的 hello 狀態值完全相同。 |
| expires_in |多久 hello 存取權杖是有效 （以秒為單位）。 |
| scope |hello 存取權杖的 hello 範圍無效。 |

#### 錯誤回應
錯誤回應也可能會傳送 toohello`redirect_uri`讓 hello 應用程式可以適當地處理。  中的 hello 案例`prompt=none`，將會發生預期的錯誤：

```
GET https://localhost/myapp/#
error=user_authentication_required
&error_description=the+request+could+not+be+completed+silently
```

| 參數 | 說明 |
| --- | --- |
| 錯誤 |錯誤的程式碼字串是使用的 tooclassify 類型之錯誤的發生，且可以使用的 tooreact tooerrors。 |
| error_description |特定的錯誤訊息，可協助開發人員會識別 hello 的驗證錯誤的根本原因。 |

如果您收到這個錯誤 hello iframe 要求中，hello 使用者必須以互動方式登入一次 tooretrieve 新權杖。  您可以選擇 toohandle 此情況下，無論最適合您的應用程式中。

## 重新整理權杖
同時`id_token`s 和`access_token`s 會在一段時間後過期，因此您的應用程式必須準備 toorefresh 這些語彙基元定期。  輸入的語彙基元 toorefresh，您可以執行 hello corresponding 使用 hello 的同一個隱藏的 iframe 要求`prompt=none`參數 toocontrol Azure AD 的行為。  如果您想要新 tooreceive `id_token`，是確定 toouse`response_type=id_token`和`scope=openid`，以及`nonce`參數。

## 傳送登出要求
hello OpenIdConnect`end_session_endpoint`可讓您的應用程式 toosend hello v2.0 端點所設定的使用者工作階段和清除 cookie 要求 toohello v2.0 端點 tooend。  toofully 登入將使用者登出 web 應用程式，您的應用程式應該結束自己的工作階段與 hello 使用者 （通常是藉由清除 權杖快取或卸除 cookie），並再重新導向至 hello 瀏覽器：

```
https://login.microsoftonline.com/{tenant}/oauth2/v2.0/logout?post_logout_redirect_uri=https://localhost/myapp/
```

| 參數 |  | 說明 |
| --- | --- | --- |
| tenant |必要 |hello `{tenant}` hello hello 要求路徑中的值可以是使用的 toocontrol 可以登入 hello 應用程式。  hello 允許的值為`common`， `organizations`， `consumers`，和租用戶識別碼。  如需更多詳細資訊，請參閱 [通訊協定基本概念](active-directory-v2-protocols.md#endpoints)。 |
| post_logout_redirect_uri | 建議使用 | hello，hello 使用者應該傳回 URL，tooafter 登出完成。 此值必須符合其中一個 hello 重新導向 Uri 註冊 hello 應用程式。 如果未包含，hello 使用者將會顯示一般訊息 hello v2.0 端點。 |
