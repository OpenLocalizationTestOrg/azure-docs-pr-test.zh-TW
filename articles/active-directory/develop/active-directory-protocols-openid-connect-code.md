---
title: "aaaUnderstand hello Azure AD 中的 OpenID Connect 驗證程式碼流程 |Microsoft 文件"
description: "本文說明如何 toouse HTTP 訊息 tooauthorize 存取 tooweb 應用程式和 web 應用程式開發介面使用 Azure Active Directory 和 OpenID Connect 的租用戶中。"
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 29142f7e-d862-4076-9a1a-ecae5bcd9d9b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/08/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: fafd8ab906ee576c584fec2ef1e9de83ddb1f6e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# 授權存取 tooweb 應用程式使用 OpenID Connect 和 Azure Active Directory
[OpenID Connect](http://openid.net/specs/openid-connect-core-1_0.html)是簡單的身分識別層之上 hello OAuth 2.0 通訊協定。 OAuth 2.0 定義機制 tooobtain 並用**存取權杖**tooaccess 受保護的資源，但它們不會定義標準方法 tooprovide 身分識別資訊。 OpenID Connect 實作驗證做為副檔名 toohello OAuth 2.0 授權程序。 它提供有關 hello 形式 hello 終端使用者資訊`id_token`，它會確認 hello hello 使用者識別，並提供 hello 使用者的基本設定檔資訊。

如果您要建置的 Web 應用程式是裝載於伺服器且透過瀏覽器存取，建議使用 OpenID Connect。


[!INCLUDE [active-directory-protocols-getting-started](../../../includes/active-directory-protocols-getting-started.md)] 

## 使用 OpenID Connect 驗證流程
hello 最基本登入流程包含下列步驟的 hello-每個詳細資料，如下所述。

![OpenId Connect 驗證流程](media/active-directory-protocols-openid-connect-code/active-directory-oauth-code-flow-web-app.png)

## OpenID Connect 中繼資料文件

OpenID Connect 描述中繼資料文件，其中包含大部分的 hello 資訊所需的應用程式 tooperform 登入。 這包括 hello Url toouse 和 hello 的 hello 服務的公開金鑰簽署金鑰的位置等資訊。 hello OpenID Connect 的中繼資料文件，請參閱：

```
https://login.microsoftonline.com/{tenant}/.well-known/openid-configuration
```
hello 中繼資料是簡單的 JavaScript Object Notation (JSON) 文件。 請參閱下列的範例程式碼片段的 hello。 hello 片段的內容中完整說明 hello [OpenID Connect 規格](https://openid.net)。

```
{
    "authorization_endpoint": "https://login.microsoftonline.com/common/oauth2/authorize",
    "token_endpoint": "https://login.microsoftonline.com/common/oauth2/token",
    "token_endpoint_auth_methods_supported":
    [
        "client_secret_post",
        "private_key_jwt"
    ],
    "jwks_uri": "https://login.microsoftonline.com/common/discovery/keys"
    
    ...
}
```

## 傳送 hello 登入要求
當您的 web 應用程式需要 tooauthenticate hello 使用者時，必須將導向 hello 使用者 toohello`/authorize`端點。 這個要求是類似 toohello 第一個階段 hello [OAuth 2.0 授權碼流程](active-directory-protocols-oauth-code.md)，有幾個重要的區別：

* hello 要求必須包含 hello 範圍`openid`在 hello`scope`參數。
* hello`response_type`參數必須包含`id_token`。
* hello 要求必須包含 hello`nonce`參數。

因此範例要求會看起來像這樣：

```
// Line breaks for legibility only

GET https://login.microsoftonline.com/{tenant}/oauth2/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&response_type=id_token
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&response_mode=form_post
&scope=openid
&state=12345
&nonce=7362CAEA-9CA5-4B43-9BA3-34D7C303EBA7
```

| 參數 |  | 說明 |
| --- | --- | --- |
| tenant |必要 |hello `{tenant}` hello hello 要求路徑中的值可以是使用的 toocontrol 可以登入 hello 應用程式。  hello 允許的值為租用戶識別碼，例如`8eaef023-2b34-4da1-9baa-8bc8c9d6a490`或`contoso.onmicrosoft.com`或`common`租用戶獨立語彙基元 |
| client_id |必要 |hello 應用程式識別碼指派的 tooyour 應用程式時向 Azure AD 註冊。 您可以將它找到 hello Azure 入口網站中。 按一下**Azure Active Directory**，按一下 **應用程式註冊**、 選擇 hello 應用程式，以及找出 hello 應用程式頁面上的應用程式識別碼 hello。 |
| response_type |必要 |必須包含 OpenID Connect 登入的 `id_token` 。  它也可能包含其他 response_types，例如 `code`。 |
| scope |必要 |範圍的空格分隔清單。  OpenID Connect，它必須包含 hello 範圍`openid`，會轉譯為 hello 同意 UI 中的 toohello 「 將您登入 」 權限。  您也可以在此要求中包含其他範圍以要求同意。 |
| nonce |必要 |值，包含在產生 hello hello 應用程式所產生的 hello 要求中包含`id_token`宣告的形式。  hello 應用程式然後確認此值 toomitigate 權杖重新執行攻擊。  hello 值通常是隨機的唯一字串或可以是使用的 tooidentify hello 原點的 hello 要求的 GUID。 |
| redirect_uri |建議使用 |hello redirect_uri 應用程式，可以傳送及接收您的應用程式驗證回應。  它必須完全符合其中一個 hello redirect_uris 您註冊 hello 入口網站，但它必須是 url 編碼。 |
| response_mode |建議使用 |指定應該使用的 toosend hello 產生 authorization_code 後 tooyour 應用程式的 hello 方法。  支援的值為 `form_post` (*HTTP 表單公佈*) 或 `fragment` (*URL 片段*)。  Web 應用程式，我們建議使用`response_mode=form_post`tooensure hello 語彙基元 tooyour 應用程式的最安全傳輸。 |
| state |建議使用 |包含在 hello 要求 hello 權杖回應中傳回的值。  其可以是您想要之任何內容的字串。  隨機產生的唯一值通常用於 [防止跨站台偽造要求攻擊](http://tools.ietf.org/html/rfc6749#section-10.12)。  之前發生 hello 驗證要求，例如 hello 頁面或檢視上 hello 狀態也會使用的 tooencode hello 應用程式中的 hello 使用者狀態資訊。 |
| prompt |選用 |指出 hello 類型所需使用者互動。  目前，hello 只有有效的值為 'none'、 ' 登入' 和 '同意'。  `prompt=login`該要求停止單一登入上強制 hello 使用者 tooenter 他們的認證。  `prompt=none`hello 相反-它會確保該 hello 使用者不提供任何互動式提示擔保。  如果 hello 無法完成要求，以無訊息方式透過單一登入，hello 端點會傳回錯誤。  `prompt=consent`觸發 hello OAuth 同意對話方塊之後 hello 使用者登入時，要求 hello 使用者 toogrant 權限 toohello 應用程式。 |
| login_hint |選用 |如果您知道事先其使用者名稱，可能會使用的 toopre 填滿 hello 使用者名稱/電子郵件地址欄位 hello 登入頁面的 hello 使用者。  通常應用程式使用此參數在重新驗證，從先前的登入需要擷取 hello 使用者名稱時使用 hello`preferred_username`宣告。 |

此時，hello 使用者是他們的認證與完整 hello 驗證要求 tooenter。

### 範例回應
範例回應 hello 使用者驗證之後，可能看起來像這樣：

```
POST /myapp/ HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded

id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWmNB...&state=12345
```

| 參數 | 說明 |
| --- | --- |
| id_token |hello`id_token`要求該 hello 應用程式。 您可以使用 hello `id_token` tooverify hello 使用者的身分識別，並開始與 hello 使用者工作階段。 |
| state |也會傳回 hello 權杖回應中的 hello 要求中包含一個值。 隨機產生的唯一值通常用於 [防止跨站台偽造要求攻擊](http://tools.ietf.org/html/rfc6749#section-10.12)。  之前發生 hello 驗證要求，例如 hello 頁面或檢視上 hello 狀態也會使用的 tooencode hello 應用程式中的 hello 使用者狀態資訊。 |

### 錯誤回應
錯誤回應也可能會傳送 toohello`redirect_uri`讓 hello 應用程式可以適當地處理：

```
POST /myapp/ HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded

error=access_denied&error_description=the+user+canceled+the+authentication
```

| 參數 | 說明 |
| --- | --- |
| 錯誤 |錯誤的程式碼字串是使用的 tooclassify 類型之錯誤的發生，且可以使用的 tooreact tooerrors。 |
| error_description |特定的錯誤訊息，可協助開發人員會識別 hello 的驗證錯誤的根本原因。 |

#### 授權端點錯誤的錯誤碼
hello 以下表格說明 hello 各種 hello 中可傳回的錯誤碼`error`hello 錯誤回應的參數。

| 錯誤碼 | 說明 | 用戶端動作 |
| --- | --- | --- |
| invalid_request |通訊協定錯誤，例如遺漏必要的參數。 |修正，然後再重新送出 hello 要求。 這是通常會在初始測試期間擷取到的開發錯誤。 |
| unauthorized_client |hello 用戶端應用程式不允許 toorequest 授權碼。 |這通常就會發生 hello 用戶端應用程式未在 Azure AD 中註冊，或未加入 toohello 使用者的 Azure AD 租用戶。 hello 應用程式可以提示指示安裝 hello 應用程式，並將它加入 tooAzure AD hello 的使用者。 |
| access_denied |資源擁有者拒絕同意 |hello 用戶端應用程式可以通知 hello 使用者除非 hello 使用者同意，否則無法繼續進行。 |
| unsupported_response_type |hello 授權伺服器不支援在 hello 要求中的 hello 回應類型。 |修正，然後再重新送出 hello 要求。 這是通常會在初始測試期間擷取到的開發錯誤。 |
| server_error |hello 伺服器發生未預期的錯誤。 |重試 hello 要求。 這些錯誤可能是由暫時性狀況所引起。 hello 用戶端應用程式可能會詳述 toohello 使用者其回應，因為 tooa 暫時錯誤而延遲。 |
| temporarily_unavailable |hello 伺服器就會暫時太忙碌 toohandle hello 要求。 |重試 hello 要求。 hello 用戶端應用程式可能會詳述 toohello 使用者其回應，因為 tooa 暫時性狀況而延遲。 |
| invalid_resource |hello 目標資源無效，因為它不存在、 Azure AD 無法找到它，或是未正確設定。 |這表示 hello 資源存在，是否尚未設定 hello 租用戶中。 hello 應用程式可以提示指示安裝 hello 應用程式，並將它加入 tooAzure AD hello 的使用者。 |

## 驗證 hello id_token
只接收`id_token`不足夠 tooauthenticate hello 使用者; 您必須驗證 hello 簽章，並確認在 hello hello 宣告`id_token`根據每個應用程式的需求。 hello Azure AD 端點使用 JSON Web 權杖 (Jwt) 和公開金鑰加密 toosign 語彙基元，並確認它們都有效。

您可以選擇 toovalidate hello`id_token`中用戶端程式碼，但常見作法是將 toosend hello `id_token` tooa 後端伺服器並執行那里 hello 驗證。 一旦您已驗證簽章 hello hello `id_token`，有幾個您所需要的 tooverify 的宣告。

您可能也想 toovalidate 宣告的其他宣告根據您的案例。 一些常見的驗證包括：

* 確保 hello 使用者組織已註冊 hello 應用程式。
* 確保以下人員 hello 使用者擁有適當的授權/權限
* 確保驗證具有特定強度，例如多重要素驗證。

一旦您已驗證 hello `id_token`，您可以開始與 hello 使用者的工作階段，並使用 hello 宣告在 hello `id_token` tooobtain hello 使用者應用程式中的資訊。 這項資訊可以用於顯示、記錄、授權等等。如需有關 hello 語彙基元類型及宣告的詳細資訊，請閱讀[支援權杖和宣告類型](active-directory-token-and-claims.md)。

## 傳送登出要求
當您想 toosign hello 使用者登出 hello 應用程式時，您的應用程式 cookie 是沒有足夠權限 tooclear 或否則結束 hello 與 hello 使用者的工作階段。  您也必須重新導向 hello 使用者 toohello`end_session_endpoint`的登出。如果您因此無法 toodo，hello 使用者將能夠 tooreauthenticate tooyour 應用程式，而不需輸入其認證，因為它們會有效單一登入工作階段與 hello Azure AD 端點。

您可以只是重新導向 hello 使用者 toohello `end_session_endpoint` hello OpenID Connect 的中繼資料文件中所列：

```
GET https://login.microsoftonline.com/common/oauth2/logout?
post_logout_redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F

```

| 參數 |  | 說明 |
| --- | --- | --- |
| post_logout_redirect_uri |建議使用 |hello 使用者 hello URL 應該會重新導向的 tooafter 成功登出。  如果未包含，hello 使用者會顯示一般的訊息。 |

## 單一登出
當您重新導向 hello 使用者 toohello `end_session_endpoint`，Azure AD 會清除從 hello 瀏覽器的 hello 使用者的工作階段。 不過，hello 使用者仍然可能會簽署 tooother 的應用程式使用 Azure AD 進行驗證。 tooenable 這些應用程式 toosign 同時 hello 使用者登出，Azure AD 會傳送給註冊 HTTP GET 要求 toohello `LogoutUrl` hello 的所有應用程式的 hello 使用者目前登入。 應用程式必須藉由清除任何工作階段，可識別 hello 使用者，並傳回回應 toothis 要求`200`回應。  如果想 toosupport 單一登登出您的應用程式中，您必須實作這類`LogoutUrl`在您的應用程式程式碼中。  您可以設定 hello`LogoutUrl`從 hello Azure 入口網站：

1. 瀏覽 toohello [Azure 入口網站](https://portal.azure.com)。
2. 在您的帳戶在 hello 右上角的 hello 頁面，即可選擇您的 Active Directory。
3. 從 hello 左邊導覽面板中，選擇  **Azure Active Directory**，然後選擇 **應用程式註冊**並選取您的應用程式。
4. 按一下**屬性**並尋找 hello**登出 URL**文字方塊。 

## 權杖取得
許多 web 應用程式需要 toonot 登 hello 中唯一的使用者，但也存取代表該使用者使用 OAuth web 服務。 此案例中進行使用者驗證時同時取得結合 OpenID Connect`authorization_code`可以使用的 tooget`access_tokens`使用 hello OAuth 授權碼流程。

## 取得存取權杖
tooacquire 存取權杖，您需要 toomodify hello 登入要求，從上方：

```
// Line breaks for legibility only

GET https://login.microsoftonline.com/{tenant}/oauth2/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e        // Your registered Application Id
&response_type=id_token+code
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F       // Your registered Redirect Uri, url encoded
&response_mode=form_post                              // form_post', or 'fragment'
&scope=openid
&resource=https%3A%2F%2Fservice.contoso.com%2F                                     
&state=12345                                          // Any value, provided by your app
&nonce=678910                                         // Any value, provided by your app
```

包括 hello 要求中的權限範圍，並使用`response_type=code+id_token`，hello`authorize`端點可確保該 hello 使用者同意 toohello hello 中指出的權限`scope`查詢參數，並傳回您的應用程式授權碼tooexchange 存取權杖。

### 成功回應
使用 `response_mode=form_post` 的成功回應如下所示：

```
POST /myapp/ HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded

id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWmNB...&code=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...&state=12345
```

| 參數 | 說明 |
| --- | --- |
| id_token |hello`id_token`要求該 hello 應用程式。 您可以使用 hello `id_token` tooverify hello 使用者的身分識別，並開始與 hello 使用者工作階段。 |
| code |hello authorization_code hello 要求的應用程式。 hello 應用程式可以使用 hello 目標資源的 hello 授權程式碼 toorequest 存取權杖。 authorization_code 的有效期很短，通常約 10 分鐘後即到期。 |
| state |如果在 hello 要求中，相同的值應該會出現在 hello 回應 hello 包含狀態參數。 hello 應用程式應該確認 hello 要求和回應中的 hello 狀態值完全相同。 |

### 錯誤回應
錯誤回應也可能會傳送 toohello`redirect_uri`讓 hello 應用程式可以適當地處理：

```
POST /myapp/ HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded

error=access_denied&error_description=the+user+canceled+the+authentication
```

| 參數 | 說明 |
| --- | --- |
| 錯誤 |錯誤的程式碼字串是使用的 tooclassify 類型之錯誤的發生，且可以使用的 tooreact tooerrors。 |
| error_description |特定的錯誤訊息，可協助開發人員會識別 hello 的驗證錯誤的根本原因。 |

如需 hello 可能錯誤碼和其建議用戶端動作的說明，請參閱[授權端點發生錯誤的錯誤代碼](#error-codes-for-authorization-endpoint-errors)。

一旦授權`code`和`id_token`，您可以 hello 使用者登入，並代表它取得存取權杖。  toosign hello 中的使用者，您必須驗證 hello`id_token`完全如上面所述。 tooget 存取權杖，您可以依照 hello [使用 hello 授權程式碼 toorequest 存取權杖] 區段中所述的 hello 步驟我們[OAuth 通訊協定文件](active-directory-protocols-oauth-code.md)。
