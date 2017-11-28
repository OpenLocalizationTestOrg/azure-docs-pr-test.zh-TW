---
title: "OAuth 授權碼流程 aaaAzure AD v2.0 |Microsoft 文件"
description: "建立 web 應用程式使用 Azure AD 的 hello OAuth 2.0 驗證通訊協定的實作。"
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: ae1d7d86-7098-468c-aa32-20df0a10ee3d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: dee58f2f5c627fef35cae279349728c3c7bf9421
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# v2.0 通訊協定 - OAuth 2.0 授權碼流程
hello OAuth 2.0 授權碼授與可以用於安裝在裝置 toogain 存取 tooprotected 資源，例如 web Api 的應用程式。  使用的 OAuth 2.0 的 hello 應用程式模型 v2.0 的實作，您可以加入登入及應用程式開發介面存取 tooyour 行動及桌面應用程式。  本指南是與語言無關，並說明如何 toosend 和接收 HTTP 訊息，而不使用任何我們開放原始碼程式庫。

> [!NOTE]
> 並非所有的 Azure Active Directory 案例和功能都受到 hello v2.0 端點。  toodetermine 如果應該使用 hello v2.0 端點，閱讀有關[v2.0 限制](active-directory-v2-limitations.md)。
> 
> 

hello OAuth 2.0 授權碼流程所述在[區段 hello OAuth 2.0 規格的 4.1](http://tools.ietf.org/html/rfc6749)。  它是使用的 tooperform 驗證和授權的應用程式類型，包括 hello 大部分[web 應用程式](active-directory-v2-flows.md#web-apps)和[原生安裝的應用程式](active-directory-v2-flows.md#mobile-and-native-apps)。  它可讓 toosecurely 取得 access_tokens 可以是使用的 tooaccess 資源使用 hello v2.0 端點保護應用程式。  

## 通訊協定圖表
在高層級，原生/行動裝置應用程式的 hello 整個驗證流程的位元外觀如下：

![OAuth 授權碼流程](../../media/active-directory-v2-flows/convergence_scenarios_native.png)

## 要求授權碼
hello 授權碼流程的開頭 hello 用戶端導向 hello 使用者 toohello`/authorize`端點。  在要求中，hello 用戶端指出它需要從 hello 使用者 tooacquire hello 權限：

```
// Line breaks for legibility only

https://login.microsoftonline.com/{tenant}/oauth2/v2.0/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&response_type=code
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&response_mode=query
&scope=openid%20offline_access%20https%3A%2F%2Fgraph.microsoft.com%2Fmail.read
&state=12345
```

> [!TIP]
> 按一下下方 tooexecute hello 連結，此要求 ！ 登入之後，您的瀏覽器應該重新導向太`https://localhost/myapp/`與`code`hello 網址列中。
> <a href="https://login.microsoftonline.com/common/oauth2/v2.0/authorize?client_id=6731de76-14a6-49ae-97bc-6eba6914391e&response_type=code&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F&response_mode=query&scope=openid%20offline_access%20https%3A%2F%2Fgraph.microsoft.com%2Fmail.read&state=12345" target="_blank">https://login.microsoftonline.com/common/oauth2/v2.0/authorize...</a>
> 
> 

| 參數 |  | 說明 |
| --- | --- | --- |
| tenant |必要 |hello `{tenant}` hello hello 要求路徑中的值可以是使用的 toocontrol 可以登入 hello 應用程式。  hello 允許的值為`common`， `organizations`， `consumers`，和租用戶識別碼。  如需更多詳細資訊，請參閱 [通訊協定基本概念](active-directory-v2-protocols.md#endpoints)。 |
| client_id |必要 |hello 該 hello 註冊入口網站的應用程式識別碼 ([apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)) 指派給您的應用程式。 |
| response_type |必要 |必須包含`code`的 hello 授權碼流程。 |
| redirect_uri |建議使用 |hello redirect_uri 應用程式，可以傳送及接收您的應用程式驗證回應。  它必須完全符合其中一個 hello redirect_uris 您註冊 hello 入口網站，但它必須是 url 編碼。  原生和行動應用程式，您應該使用 hello 預設值是`https://login.microsoftonline.com/common/oauth2/nativeclient`。 |
| scope |必要 |以空格分隔的清單[範圍](active-directory-v2-scopes.md)您想要的 hello 使用者 tooconsent。 |
| response_mode |建議使用 |指定應該使用的 toosend hello 產生語彙基元後 tooyour 應用程式的 hello 方法。  可以是 `query` 或 `form_post`。 |
| state |建議使用 |Hello 權杖回應中也會傳回的 hello 要求中包含一個值。  其可以是您想要之任何內容的字串。  隨機產生的唯一值通常用於 [防止跨站台偽造要求攻擊](http://tools.ietf.org/html/rfc6749#section-10.12)。  之前發生 hello 驗證要求，例如 hello 頁面或檢視上 hello 狀態也會使用的 tooencode hello 應用程式中的 hello 使用者狀態資訊。 |
| prompt |選用 |指出 hello 類型所需使用者互動。  只有在這個階段的有效值為 'none'、 '登入' hello' 表示同意 '。  `prompt=login`強制 hello 使用者 tooenter 將該要求時，停止單一登入認證。  `prompt=none`是 hello 相反-它可確保該 hello 使用者不提供任何互動式提示恕不另行通知。  如果 hello 無法完成要求，以無訊息方式透過單一登入，hello v2.0 端點會傳回錯誤。  `prompt=consent`將觸發程序 hello OAuth 同意對話方塊之後 hello 使用者登入時，要求 hello 使用者 toogrant 權限 toohello 應用程式。 |
| login_hint |選用 |可以是使用的 toopre 填滿 hello 使用者名稱/電子郵件地址欄位的 hello 登入頁面 hello 使用者，如果您知道事先其使用者名稱。  通常應用程式會使用此參數重新在驗證期間，從先前的登入需要擷取 hello 使用者名稱使用 hello`preferred_username`宣告。 |
| domain_hint |選用 |可以是 `consumers` 或 `organizations` 其中一個。  如果包含，它會略過 hello 電子郵件為基礎的探索程序的使用者經歷了在 hello v2.0 登入頁面上，導致 tooa 稍微簡化使用者經驗。  通常應用程式會使用重新在驗證期間，此參數以擷取 hello`tid`從先前的登入。  如果 hello`tid`宣告值是`9188040d-6c67-4c5b-b112-36a304b66dad`，您應該使用`domain_hint=consumers`。  否則，使用 `domain_hint=organizations`。 |

Hello 使用者將會在此時，系統要求 tooenter 其認證和驗證完成 hello。  hello v2.0 端點也會確保該 hello 使用者同意 toohello hello 中指出的權限`scope`查詢參數。  如果 hello 使用者不同意 tooany 權限，它會要求 hello 使用者 tooconsent toohello 所需的權限。  [這裡提供權限、同意與多租用戶應用程式](active-directory-v2-scopes.md)的詳細資料。

一旦 hello 使用者驗證，並授與同意，hello v2.0 端點會傳回回應 tooyour 應用程式，在指出的 hello `redirect_uri`，使用 hello 中指定的 hello 方法`response_mode`參數。

#### 成功回應
使用 `response_mode=query` 的成功回應如下所示：

```
GET https://login.microsoftonline.com/common/oauth2/nativeclient?
code=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...
&state=12345
```

| 參數 | 說明 |
| --- | --- |
| code |hello authorization_code hello 要求的應用程式。 hello 應用程式可以使用 hello 目標資源的 hello 授權程式碼 toorequest 存取權杖。  Authorization_code 的有效期很短，通常約 10 分鐘後即到期。 |
| state |如果在 hello 要求中，相同的值應該會出現在 hello 回應 hello 包含狀態參數。 hello 應用程式應該確認 hello 要求和回應中的 hello 狀態值完全相同。 |

#### 錯誤回應
錯誤回應也可能會傳送 toohello`redirect_uri`讓 hello 應用程式可以適當地處理：

```
GET https://login.microsoftonline.com/common/oauth2/nativeclient?
error=access_denied
&error_description=the+user+canceled+the+authentication
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
| server_error |hello 伺服器發生未預期的錯誤。 |重試 hello 要求。 這些錯誤可能是由暫時性狀況所引起。 hello 用戶端應用程式可能會詳述 toohello 使用者其回應，因為暫時錯誤而延遲。 |
| temporarily_unavailable |hello 伺服器就會暫時太忙碌 toohandle hello 要求。 |重試 hello 要求。 hello 用戶端應用程式可能會詳述 toohello 使用者其回應，因為暫時的狀況而延遲。 |
| invalid_resource |hello 目標資源無效，因為它不存在、 Azure AD 無法找到它，或是未正確設定。 |這表示 hello 資源存在，是否尚未設定 hello 租用戶中。 hello 應用程式可以提示指示安裝 hello 應用程式，並將它加入 tooAzure AD hello 的使用者。 |

## 要求存取權杖
既然您已取得 authorization_code，且已被授與權限 hello 使用者，您可以兌換 hello`code`如`access_token`toohello 需要資源，請傳送`POST`要求 toohello`/token`端點：

```
// Line breaks for legibility only

POST /{tenant}/oauth2/v2.0/token HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&scope=https%3A%2F%2Fgraph.microsoft.com%2Fmail.read
&code=OAAABAAAAiL9Kn2Z27UubvWFPbm0gLWQJVzCTE9UkP3pSx1aXxUjq3n8b2JRLk4OxVXr...
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&grant_type=authorization_code
&client_secret=JqQX2PNo9bpM0uEihUPzyrh    // NOTE: Only required for web apps
```

> [!TIP]
> 嘗試在 Postman 中執行這項要求！ (請不要忘記 tooreplace hello `code`) [![郵差中執行](./media/active-directory-v2-protocols-oauth-code/runInPostman.png)](https://app.getpostman.com/run-collection/8f5715ec514865a07e6a)
> 
> 

| 參數 |  | 說明 |
| --- | --- | --- |
| tenant |必要 |hello `{tenant}` hello hello 要求路徑中的值可以是使用的 toocontrol 可以登入 hello 應用程式。  hello 允許的值為`common`， `organizations`， `consumers`，和租用戶識別碼。  如需更多詳細資訊，請參閱 [通訊協定基本概念](active-directory-v2-protocols.md#endpoints)。 |
| client_id |必要 |hello 該 hello 註冊入口網站的應用程式識別碼 ([apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)) 指派給您的應用程式。 |
| grant_type |必要 |必須是`authorization_code`的 hello 授權碼流程。 |
| scope |必要 |範圍的空格分隔清單。  在這個階段中必須對等 tooor hello 領域的子集要求 hello 第一個階段中要求 hello 範圍。  如果這個要求中指定的 hello 範圍會跨越多個資源伺服器，hello v2.0 端點會傳回指定 hello 第一個範圍中的 hello 資源語彙基元。  如需範圍的詳細說明，請參閱太[權限、 同意，以及範圍](active-directory-v2-scopes.md)。 |
| code |必要 |貴用戶取得 hello 流程 hello 第一個階段中的 hello authorization_code。 |
| redirect_uri |必要 |hello 相同的已使用的 tooacquire hello authorization_code redirect_uri 值。 |
| client_secret |Web Apps 所需 |您已在 hello 應用程式註冊入口網站應用程式的 hello 應用程式密碼。  其不應用於原生應用程式，因為裝置無法穩當地儲存 client_secret。  需要 web 應用程式和 web Api，其具有 hello 能力 toostore hello client_secret 安全地 hello 伺服器端上。 |

#### 成功回應
成功的權杖回應如下：

```
{
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...",
    "token_type": "Bearer",
    "expires_in": 3599,
    "scope": "https%3A%2F%2Fgraph.microsoft.com%2Fmail.read",
    "refresh_token": "AwABAAAAvPM1KaPlrEqdFSBzjqfTGAMxZGUTdM0t4B4...",
    "id_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJub25lIn0.eyJhdWQiOiIyZDRkMTFhMi1mODE0LTQ2YTctOD...",
}
```
| 參數 | 說明 |
| --- | --- |
| access_token |hello 要求的存取權杖。 hello 應用程式可以使用這個受保護資源，例如 web API 的語彙基元 tooauthenticate toohello。 |
| token_type |表示 hello 語彙基元型別值。 hello Azure AD 支援的類型是持有者 |
| expires_in |多久 hello 存取權杖是有效 （以秒為單位）。 |
| scope |hello access_token 的 hello 範圍無效。 |
| refresh_token |OAuth 2.0 重新整理權杖。 hello 應用程式可以使用此權杖 hello 目前存取語彙基元過期之後，取得其他存取權杖。  Refresh_tokens 存留較久，而且可以使用的 tooretain 存取 tooresources 很長的時間。  如需詳細資訊，請參閱 toohello [v2.0 權杖參照](active-directory-v2-tokens.md)。 |
| id_token |不帶正負號的 JSON Web Token (JWT)。 hello 應用程式可以 base64Url 解碼 hello hello 使用者登入此語彙基元 toorequest 資訊區段。 hello 應用程式可以快取 hello 值，並顯示它們，但它不應依賴它們的任何授權或安全性界限。  如需 id_tokens 詳細資訊，請參閱 hello [v2.0 端點權杖參照](active-directory-v2-tokens.md)。 |

#### 錯誤回應
錯誤回應格式如下：

```
{
  "error": "invalid_scope",
  "error_description": "AADSTS70011: hello provided value for hello input parameter 'scope' is not valid. hello scope https://foo.microsoft.com/mail.read is not valid.\r\nTrace ID: 255d1aef-8c98-452f-ac51-23d051240864\r\nCorrelation ID: fb3d2015-bc17-4bb9-bb85-30c5cf1aaaa7\r\nTimestamp: 2016-01-09 02:02:12Z",
  "error_codes": [
    70011
  ],
  "timestamp": "2016-01-09 02:02:12Z",
  "trace_id": "255d1aef-8c98-452f-ac51-23d051240864",
  "correlation_id": "fb3d2015-bc17-4bb9-bb85-30c5cf1aaaa7"
}
```

| 參數 | 說明 |
| --- | --- |
| 錯誤 |錯誤的程式碼字串是使用的 tooclassify 類型之錯誤的發生，且可以使用的 tooreact tooerrors。 |
| error_description |特定的錯誤訊息，可協助開發人員會識別 hello 的驗證錯誤的根本原因。 |
| error_codes |有助於診斷的 STS 特定錯誤碼清單。 |
| timestamp |hello hello 錯誤發生的時間。 |
| trace_id |可協助診斷中的 hello 要求的唯一識別碼。 |
| correlation_id |元件可協助診斷中的 hello 要求的唯一識別碼。 |

#### 權杖端點錯誤的錯誤碼
| 錯誤碼 | 說明 | 用戶端動作 |
| --- | --- | --- |
| invalid_request |通訊協定錯誤，例如遺漏必要的參數。 |修正，然後再重新送出 hello 要求 |
| invalid_grant |hello 授權碼無效，或已過期。 |再試一次新的要求 toohello`/authorize`端點 |
| unauthorized_client |hello 驗證的用戶端未獲得授權 toouse 此授權授與類型。 |這通常就會發生 hello 用戶端應用程式未在 Azure AD 中註冊，或未加入 toohello 使用者的 Azure AD 租用戶。 hello 應用程式可以提示指示安裝 hello 應用程式，並將它加入 tooAzure AD hello 的使用者。 |
| invalid_client |用戶端驗證失敗。 |找不到有效的 hello 用戶端認證。 toofix，hello 應用程式系統管理員更新 hello 認證。 |
| unsupported_grant_type |hello 授權伺服器不支援 hello 授權授與類型。 |變更 hello 授與 hello 要求中的型別。 這種類型的錯誤應該只會在開發期間發生，並且會在初始測試期間偵測出來。 |
| invalid_resource |hello 目標資源無效，因為它不存在、 Azure AD 無法找到它，或是未正確設定。 |這表示 hello 資源存在，是否尚未設定 hello 租用戶中。 hello 應用程式可以提示指示安裝 hello 應用程式，並將它加入 tooAzure AD hello 的使用者。 |
| interaction_required |hello 要求需要使用者互動。 例如，必須進行其他驗證步驟。 |重試以 hello hello 要求相同的資源。 |
| temporarily_unavailable |hello 伺服器就會暫時太忙碌 toohandle hello 要求。 |重試 hello 要求。 hello 用戶端應用程式可能會詳述 toohello 使用者其回應，因為暫時的狀況而延遲。 |

## 使用 hello 存取權杖
既然您已成功取得`access_token`，您可以使用 hello 語彙基元要求 tooWeb 應用程式開發介面中併入 hello`Authorization`標頭：

> [!TIP]
> 在 Postman 中執行這項要求！ (取代 hello`Authorization`標頭第一個) [![郵差中執行](./media/active-directory-v2-protocols-oauth-code/runInPostman.png)](https://app.getpostman.com/run-collection/8f5715ec514865a07e6a)
> 
> 

```
GET /v1.0/me/messages
Host: https://graph.microsoft.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
```

## 重新整理 hello 存取權杖
Access_tokens 很短存在，而且您必須重新整理它們之後過期 toocontinue 存取資源。  您可以藉由送出另一個`POST`要求 toohello`/token`端點，此時提供 hello`refresh_token`而不是 hello `code`:

```
// Line breaks for legibility only

POST /{tenant}/oauth2/v2.0/token HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&scope=https%3A%2F%2Fgraph.microsoft.com%2Fmail.read
&refresh_token=OAAABAAAAiL9Kn2Z27UubvWFPbm0gLWQJVzCTE9UkP3pSx1aXxUjq...
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&grant_type=refresh_token
&client_secret=JqQX2PNo9bpM0uEihUPzyrh      // NOTE: Only required for web apps
```

> [!TIP]
> 嘗試在 Postman 中執行這項要求！ (請不要忘記 tooreplace hello `refresh_token`) [![郵差中執行](./media/active-directory-v2-protocols-oauth-code/runInPostman.png)](https://app.getpostman.com/run-collection/8f5715ec514865a07e6a)
> 
> 

| 參數 |  | 說明 |
| --- | --- | --- |
| tenant |必要 |hello `{tenant}` hello hello 要求路徑中的值可以是使用的 toocontrol 可以登入 hello 應用程式。  hello 允許的值為`common`， `organizations`， `consumers`，和租用戶識別碼。  如需更多詳細資訊，請參閱 [通訊協定基本概念](active-directory-v2-protocols.md#endpoints)。 |
| client_id |必要 |hello 該 hello 註冊入口網站的應用程式識別碼 ([apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)) 指派給您的應用程式。 |
| grant_type |必要 |必須是`refresh_token`個 hello 授權碼流程的此階段。 |
| scope |必要 |範圍的空格分隔清單。  在這個階段中必須對等 tooor hello 領域的子集要求在 hello 原始 authorization_code 要求階段要求 hello 範圍。  如果這個要求中指定的 hello 範圍會跨越多個資源伺服器，hello v2.0 端點會傳回指定 hello 第一個範圍中的 hello 資源語彙基元。  如需範圍的詳細說明，請參閱太[權限、 同意，以及範圍](active-directory-v2-scopes.md)。 |
| refresh_token |必要 |貴用戶取得 hello 流程 hello 第二個階段中的 hello refresh_token。 |
| redirect_uri |必要 |hello 相同的已使用的 tooacquire hello authorization_code redirect_uri 值。 |
| client_secret |Web Apps 所需 |您已在 hello 應用程式註冊入口網站應用程式的 hello 應用程式密碼。  其不應用於原生應用程式，因為裝置無法穩當地儲存 client_secret。  需要 web 應用程式和 web Api，其具有 hello 能力 toostore hello client_secret 安全地 hello 伺服器端上。 |

#### 成功回應
成功的權杖回應如下：

```
{
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...",
    "token_type": "Bearer",
    "expires_in": 3599,
    "scope": "https%3A%2F%2Fgraph.microsoft.com%2Fmail.read",
    "refresh_token": "AwABAAAAvPM1KaPlrEqdFSBzjqfTGAMxZGUTdM0t4B4...",
    "id_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJub25lIn0.eyJhdWQiOiIyZDRkMTFhMi1mODE0LTQ2YTctOD...",
}
```
| 參數 | 說明 |
| --- | --- |
| access_token |hello 要求的存取權杖。 hello 應用程式可以使用這個受保護資源，例如 web API 的語彙基元 tooauthenticate toohello。 |
| token_type |表示 hello 語彙基元型別值。 hello Azure AD 支援的類型是持有者 |
| expires_in |多久 hello 存取權杖是有效 （以秒為單位）。 |
| scope |hello access_token 的 hello 範圍無效。 |
| refresh_token |新的 OAuth 2.0 重新整理權杖。 您應該取代 hello 舊的重新整理權杖與這個最新取得的重新整理語彙基元 tooensure 重新整理權杖會保持有效一樣長。 |
| id_token |不帶正負號的 JSON Web Token (JWT)。 hello 應用程式可以 base64Url 解碼 hello hello 使用者登入此語彙基元 toorequest 資訊區段。 hello 應用程式可以快取 hello 值，並顯示它們，但它不應依賴它們的任何授權或安全性界限。  如需 id_tokens 詳細資訊，請參閱 hello [v2.0 端點權杖參照](active-directory-v2-tokens.md)。 |

#### 錯誤回應
```
{
  "error": "invalid_scope",
  "error_description": "AADSTS70011: hello provided value for hello input parameter 'scope' is not valid. hello scope https://foo.microsoft.com/mail.read is not valid.\r\nTrace ID: 255d1aef-8c98-452f-ac51-23d051240864\r\nCorrelation ID: fb3d2015-bc17-4bb9-bb85-30c5cf1aaaa7\r\nTimestamp: 2016-01-09 02:02:12Z",
  "error_codes": [
    70011
  ],
  "timestamp": "2016-01-09 02:02:12Z",
  "trace_id": "255d1aef-8c98-452f-ac51-23d051240864",
  "correlation_id": "fb3d2015-bc17-4bb9-bb85-30c5cf1aaaa7"
}
```

| 參數 | 說明 |
| --- | --- |
| 錯誤 |錯誤的程式碼字串是使用的 tooclassify 類型之錯誤的發生，且可以使用的 tooreact tooerrors。 |
| error_description |特定的錯誤訊息，可協助開發人員會識別 hello 的驗證錯誤的根本原因。 |
| error_codes |有助於診斷的 STS 特定錯誤碼清單。 |
| timestamp |hello hello 錯誤發生的時間。 |
| trace_id |可協助診斷中的 hello 要求的唯一識別碼。 |
| correlation_id |元件可協助診斷中的 hello 要求的唯一識別碼。 |

如需 hello 錯誤碼和建議動作，用戶端 hello 的說明，請參閱[錯誤碼的權杖端點錯誤](#error-codes-for-token-endpoint-errors)。

