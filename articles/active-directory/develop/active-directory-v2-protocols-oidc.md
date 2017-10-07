---
title: "Active Directory v2.0 和 hello OpenID Connect 通訊協定 aaaAzure |Microsoft 文件"
description: "建立 web 應用程式藉由使用 Azure AD hello v2.0 實作 hello OpenID Connect 的驗證通訊協定。"
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: a4875997-3aac-4e4c-b7fe-2b4b829151ce
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/08/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 277bb406dbb24ccefb09e4e4c928f0421755cf61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# Azure Active Directory v2.0 和 hello OpenID Connect 通訊協定
OpenID Connect 是，您可以使用 toosecurely 登使用者 tooa web 應用程式中的 OAuth 2.0 驗證通訊協定。 當您使用的 OpenID Connect 的 hello v2.0 端點的實作時，您可以加入登入，並從應用程式開發介面存取 tooyour web 應用程式。 在本文中，我們會示範如何 toodo 這與語言無關。 我們將描述如何 toosend 和接收 HTTP 訊息，而不使用任何 Microsoft 的開放原始碼程式庫。

> [!NOTE]
> hello v2.0 端點不支援所有的 Azure Active Directory 的案例和功能。 toodetermine 是否應該使用 hello v2.0 端點，閱讀有關[v2.0 限制](active-directory-v2-limitations.md)。
> 
> 

[OpenID Connect](http://openid.net/specs/openid-connect-core-1_0.html)擴充 hello OAuth 2.0*授權*做為通訊協定 toouse*驗證*通訊協定，以便您可以執行單一登入使用 OAuth。 OpenID Connect 引進 hello 概念*ID 語彙基元*，這是安全性權杖，允許 hello 用戶端 hello 使用者 tooverify hello 身分識別。 hello 的 ID 語彙基元也會取得 hello 使用者的基本設定檔資訊。 OpenID Connect 可延伸 OAuth 2.0，因為應用程式可以安全地取得*存取權杖*，可能會受到使用的 tooaccess 資源[授權伺服器](active-directory-v2-protocols.md#the-basics)。 如果您要建置裝載於伺服器上且透過瀏覽器存取的 [Web 應用程式](active-directory-v2-flows.md#web-apps)，建議您使用 OpenID Connect。

## 通訊協定圖表：登入
hello 最基本的登入流程有 hello hello 下圖所示的步驟。 我們會在本文中詳細說明每個步驟。

![OpenID Connect 通訊協定：登入](../../media/active-directory-v2-flows/convergence_scenarios_webapp.png)

## 擷取 hello OpenID Connect 的中繼資料文件
OpenID Connect 描述中繼資料文件，其中包含大部分的 hello 資訊所需的應用程式 tooperform 登入。 這包括 hello Url toouse 和 hello 的 hello 服務的公開金鑰簽署金鑰的位置等資訊。 Hello v2.0 端點，這是 hello OpenID Connect 中繼資料文件，您應該使用：

```
https://login.microsoftonline.com/{tenant}/v2.0/.well-known/openid-configuration
```

hello`{tenant}`可以採用四個值的其中一個：

| 值 | 說明 |
| --- | --- |
| `common` |使用者使用個人 Microsoft 帳戶和 Azure Active Directory (Azure AD) 中的工作或學校帳戶可以登入 toohello 應用程式。 |
| `organizations` |只有具有使用者工作或學校帳戶向 Azure AD 登入 toohello 應用程式。 |
| `consumers` |只有使用個人 Microsoft 帳戶的使用者可以登入 toohello 應用程式。 |
| `8eaef023-2b34-4da1-9baa-8bc8c9d6a490` 或 `contoso.onmicrosoft.com` |只有使用者的工作或學校帳戶，從特定的 Azure AD 租用戶可以登入 toohello 應用程式。 Hello 好記的網域名稱的 hello Azure AD 租用戶，或是可以用 hello 租用戶的 GUID 識別碼。 |

hello 中繼資料是簡單的 JavaScript Object Notation (JSON) 文件。 請參閱下列的範例程式碼片段的 hello。 hello 片段的內容中完整說明 hello [OpenID Connect 規格](https://openid.net)。

```
{
  "authorization_endpoint": "https:\/\/login.microsoftonline.com\/common\/oauth2\/v2.0\/authorize",
  "token_endpoint": "https:\/\/login.microsoftonline.com\/common\/oauth2\/v2.0\/token",
  "token_endpoint_auth_methods_supported": [
    "client_secret_post",
    "private_key_jwt"
  ],
  "jwks_uri": "https:\/\/login.microsoftonline.com\/common\/discovery\/v2.0\/keys",

  ...

}
```

一般而言，您可使用此中繼資料文件 tooconfigure OpenID Connect 文件庫或 SDK。hello 程式庫會使用 hello 中繼資料 toodo 其工作。 不過，如果您不使用建置前 OpenID Connect 文件庫，您可以遵循本文章 tooperform 登入 web 應用程式中的 hello 其餘部分中的 hello 步驟使用 hello v2.0 端點。

## 傳送 hello 登入要求
當您的 web 應用程式需要 tooauthenticate hello 使用者時，它可以直接 hello 使用者 toohello`/authorize`端點。 這個要求是類似 toohello 第一個階段 hello [OAuth 2.0 授權碼流程](active-directory-v2-protocols-oauth-code.md)，與這些重要的區別：

* hello 要求必須包含 hello`openid`範圍中 hello`scope`參數。
* hello`response_type`參數必須包含`id_token`。
* hello 要求必須包含 hello`nonce`參數。

例如：

```
// Line breaks are for legibility only.

GET https://login.microsoftonline.com/{tenant}/oauth2/v2.0/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&response_type=id_token
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&response_mode=form_post
&scope=openid
&state=12345
&nonce=678910
```

> [!TIP]
> 按一下下列連結 tooexecute hello 這個要求。 登入之後，您的瀏覽器會重新導向的 toohttps://localhost/myapp/，與 hello 網址列中的 ID 語彙基元。 請注意，此要求會使用 `response_mode=query` (僅限用於示範)。 建議您使用 `response_mode=form_post`。
> <a href="https://login.microsoftonline.com/common/oauth2/v2.0/authorize?client_id=6731de76-14a6-49ae-97bc-6eba6914391e&response_type=id_token&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F&scope=openid&response_mode=query&state=12345&nonce=678910" target="_blank">https://login.microsoftonline.com/common/oauth2/v2.0/authorize...</a>
> 
> 

| 參數 | 條件 | 說明 |
| --- | --- | --- |
| tenant |必要 |您可以使用 hello `{tenant}` hello hello 要求 toocontrol 可以登入 toohello 應用程式路徑中的值。 hello 允許的值為`common`， `organizations`， `consumers`，和租用戶識別碼。 如需詳細資訊，請參閱[通訊協定基本概念](active-directory-v2-protocols.md#endpoints)。 |
| client_id |必要 |hello 應用程式識別碼的 hello[應用程式註冊入口網站](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)指派 tooyour 應用程式。 |
| response_type |必要 |必須包含 OpenID Connect 登入的 `id_token` 。 它也可能包含其他 `response_types` 值，例如 `code`。 |
| redirect_uri |建議 |hello 重新導向的應用程式，可以傳送及接收您的應用程式驗證回應的 URI。 它必須完全符合其中一個不同之處在於它必須是 URL 在 hello 入口網站註冊的 Uri 編碼的 hello 重新導向。 |
| scope |必要 |範圍的空格分隔清單。 OpenID Connect，它必須包含 hello 範圍`openid`，會轉譯為 hello 同意 UI 中的 toohello 「 將您登入 」 權限。 您也可以在此要求中包含其他範圍來要求同意。 |
| nonce |必要 |值，包含在 hello 要求中，由 hello 應用程式，將會包含在 hello 產生 id_token 值宣告的形式產生。 hello 應用程式可以驗證這個值 toomitigate 權杖重新執行攻擊。 hello 值通常是隨機的唯一字串，可以使用的 tooidentify hello 原點的 hello 要求。 |
| response_mode |建議 |指定應該使用的 toosend hello 產生授權程式碼後 tooyour 應用程式的 hello 方法。 可以是 `query`、`form_post` 或 `fragment` 其中一個。 Web 應用程式，我們建議使用`response_mode=form_post`，tooensure hello 語彙基元 tooyour 應用程式的最安全傳輸。 |
| state |建議 |將傳回 hello 權杖回應中的 hello 要求中包含一個值。 它可以是您想要的任何內容的字串。 隨機產生的唯一值通常用太[防止跨網站要求偽造攻擊](http://tools.ietf.org/html/rfc6749#section-10.12)。 hello 狀態也是使用的 tooencode hello 應用程式中的 hello 使用者狀態資訊之前發生 hello 驗證要求，例如 hello 頁面或檢視 hello 使用者時間為。 |
| prompt |選用 |指出 hello 類型所需使用者互動。 hello 只有有效的值此時為`login`， `none`，和`consent`。 hello`prompt=login`宣告強制 hello 使用者 tooenter 他們的認證，該要求，執行單一登入的否定運算。 hello`prompt=none`宣告為 hello 相反。 這個宣告可確保該 hello 使用者不提供任何互動式提示恕不另行通知。 如果 hello 無法完成要求，以無訊息方式透過單一登入，hello v2.0 端點會傳回錯誤。 hello`prompt=consent`宣告 hello 使用者登入之後，觸發程序 hello OAuth 同意對話方塊。 hello 對話方塊會要求 hello 使用者 toogrant 權限 toohello 應用程式。 |
| login_hint |選用 |如果您知道事先 hello 使用者名稱，您可以使用此參數 toopre 填滿 hello 使用者名稱和電子郵件地址欄位的 hello 登入頁面 hello 使用者。 通常，應用程式會使用這個參數重新在驗證期間，已從先前的登入使用 hello 解壓縮 hello 使用者名稱之後`preferred_username`宣告。 |
| domain_hint |選用 |此值可以是 `consumers` 或 `organizations`。 如果包含，它會略過 hello 電子郵件為基礎的探索程序的 hello 使用者經歷了在 hello v2.0 登入頁面上，以稍微更流暢的使用者體驗。 通常，應用程式會使用此參數在重新驗證期間擷取 hello`tid`來自 hello ID 權杖宣告。 如果 hello`tid`宣告值是`9188040d-6c67-4c5b-b112-36a304b66dad`，使用`domain_hint=consumers`。 否則，使用 `domain_hint=organizations`。 |

此時，hello 使用者是提示的 tooenter 其認證與 hello 完成驗證。 hello v2.0 端點驗證該 hello 使用者同意 toohello hello 中指出的權限`scope`查詢參數。 如果 hello 使用者不同意這些權限的 tooany，hello v2.0 端點就會提示 hello 使用者 tooconsent toohello 所需的權限。 您可以深入了解[權限、同意及多租用戶應用程式](active-directory-v2-scopes.md)。

Hello 使用者驗證，並授與同意之後，在 hello 回應 tooyour 應用程式指示 hello v2.0 端點傳回重新導向 URI 使用 hello 中指定的 hello 方法`response_mode`參數。

### 成功回應
使用 `response_mode=form_post` 時的成功回應看起來像這樣：

```
POST /myapp/ HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded

id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWmNB...&state=12345
```

| 參數 | 說明 |
| --- | --- |
| id_token |hello hello 應用程式要求的 ID 語彙基元。 您可以使用 hello`id_token`參數 tooverify hello 使用者的身分識別，並開始與 hello 使用者工作階段。 如需有關識別碼語彙基元和其內容的詳細資訊，請參閱 hello [v2.0 端點權杖參考](active-directory-v2-tokens.md)。 |
| state |如果`state`參數包含在 hello 要求 hello 相同的值應該會出現在 hello 回應。 hello 應用程式應該確認 hello 要求和回應中的 hello 狀態值完全相同。 |

### 錯誤回應
錯誤回應可能也會傳送 toohello 重新導向 URI，好讓 hello 應用程式可以處理它們。 錯誤回應看起來像這樣：

```
POST /myapp/ HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded

error=access_denied&error_description=the+user+canceled+the+authentication
```

| 參數 | 說明 |
| --- | --- |
| 錯誤 |您可以使用的錯誤，就會發生，並 tooreact tooerrors tooclassify 類型錯誤的程式碼字串。 |
| error_description |特定的錯誤訊息，可協助您找出 hello 的驗證錯誤的根本原因。 |

### 授權端點錯誤的錯誤碼
hello 下表描述可以在 hello 中傳回的錯誤碼`error`hello 錯誤回應參數：

| 錯誤碼 | 說明 | 用戶端動作 |
| --- | --- | --- |
| invalid_request |通訊協定錯誤，例如遺漏必要的參數。 |修正，然後再重新送出 hello 要求。 這是通常在初始測試期間擷取到的開發錯誤。 |
| unauthorized_client |hello 用戶端應用程式無法要求授權碼。 |這通常就會發生 hello 用戶端應用程式未在 Azure AD 中註冊，或未加入 toohello 使用者的 Azure AD 租用戶。 hello 應用程式可以提示 hello 與指示 tooinstall hello 應用程式的使用者，並將它加入 tooAzure AD。 |
| access_denied |hello 資源擁有者拒絕同意。 |hello 用戶端應用程式可以通知 hello 使用者除非 hello 使用者同意，否則無法繼續進行。 |
| unsupported_response_type |hello 授權伺服器不支援在 hello 要求中的 hello 回應類型。 |修正，然後再重新送出 hello 要求。 這是通常在初始測試期間擷取到的開發錯誤。 |
| server_error |hello 伺服器發生未預期的錯誤。 |重試 hello 要求。 這些錯誤可能是由暫時性狀況所引起。 hello 用戶端應用程式可能會詳述 toohello 使用者其回應，因為 tooa 暫時錯誤而延遲。 |
| temporarily_unavailable |hello 伺服器就會暫時太忙碌 toohandle hello 要求。 |重試 hello 要求。 hello 用戶端應用程式可能會詳述 toohello 使用者其回應，因為 tooa 暫時性狀況而延遲。 |
| invalid_resource |hello 目標資源無效，因為它不存在、 Azure AD 無法找到它，或是未正確設定。 |這表示，hello 資源存在，是否尚未設定 hello 租用戶中。 hello 應用程式可以提示指示安裝 hello 應用程式，並將它加入 tooAzure AD hello 的使用者。 |

## 驗證 hello 的 ID 語彙基元
接收的 ID 語彙基元不足夠 tooauthenticate hello 使用者。 您也必須驗證 hello 識別碼權杖之簽章，並確認每個應用程式需求的 hello 權杖中的 hello 宣告。 hello v2.0 端點會使用[JSON Web 權杖 (Jwt)](http://self-issued.info/docs/draft-ietf-oauth-json-web-token.html)和公用金鑰密碼編譯 toosign 語彙基元，並確認都有效。

您可以選擇 toovalidate hello ID 語彙基元中用戶端程式碼，但常見的作法是 toosend hello ID 語彙基元 tooa 後端伺服器，並執行那里 hello 驗證。 您已驗證的 hello 的 ID 語彙基元的 hello 簽章後，您需要 tooverify 少數的宣告。 如需詳細資訊，包括更多有關[驗證權杖](active-directory-v2-tokens.md#validating-tokens)和[簽署金鑰變換的相關重要資訊](active-directory-v2-tokens.md#validating-tokens)，請參閱 hello [v2.0 權杖參考](active-directory-v2-tokens.md)。 我們建議使用程式庫 tooparse，且驗證權杖。 大多數語言和平台至少會有這些程式庫其中之一可用。
<!--TODO: Improve hello information on this-->

您也可能會想 toovalidate 其他宣告、 根據您的案例。 一些常見的驗證包括：

* 請確認 hello 使用者或組織已註冊 hello 應用程式。
* 確認該 hello 使用者是否擁有必要的授權或權限。
* 確保已進行特定強度的驗證，例如多重要素驗證。

如需 ID 權杖中的 hello 宣告的詳細資訊，請參閱 hello [v2.0 端點權杖參考](active-directory-v2-tokens.md)。

您已完全驗證 hello 的 ID 語彙基元之後，您可以開始工作階段與 hello 使用者。 使用 hello 宣告在 hello ID 語彙基元 tooget 應用程式中的 hello 使用者資訊。 您可以使用這項資訊來顯示、記錄、授權等等。

## 傳送登出要求
當您想 toosign 出 hello 使用者從您的應用程式時，它並不足夠 tooclear 應用程式的 cookie 或否則結束 hello 使用者工作階段。 您也必須重新導向 hello 使用者 toohello v2.0 端點 toosign 出。如果不這麼做，hello 使用者重新會驗證 tooyour 應用程式不需要輸入其認證，因為它們會有效單一登入工作階段與 hello v2.0 端點。

您可以重新導向 hello 使用者 toohello `end_session_endpoint` hello OpenID Connect 的中繼資料文件中所列：

```
GET https://login.microsoftonline.com/common/oauth2/v2.0/logout?
post_logout_redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
```

| 參數 | 條件 | 說明 |
| ----------------------- | ------------------------------- | ------------ |
| post_logout_redirect_uri | 建議 | 已成功登出重新導向的 tooafter hello 使用者的 hello URL。如果不包含 hello 參數，則 hello 使用者會顯示 hello v2.0 端點所產生的泛型訊息。 此 URL 必須符合其中一個應用程式在 hello 應用程式註冊入口網站註冊 Uri 的 hello 重新導向。  |

## 單一登出
當您重新導向 hello 使用者 toohello `end_session_endpoint`，hello v2.0 端點會清除從 hello 瀏覽器的 hello 使用者的工作階段。 不過，hello 使用者仍然可能會簽署 tooother 的應用程式使用 Microsoft 帳戶進行驗證。 tooenable 同時 hello v2.0 端點出這些應用程式 toosign hello 使用者傳送註冊 HTTP GET 要求 toohello `LogoutUrl` hello 的所有應用程式的 hello 使用者目前登入。 應用程式必須藉由清除任何工作階段，可識別 hello 使用者，並傳回回應 toothis 要求`200`回應。  如果想 toosupport 單一登登出您的應用程式中，您必須實作這類`LogoutUrl`在您的應用程式程式碼中。  您可以設定 hello`LogoutUrl`從 hello 應用程式註冊入口網站。

## 通訊協定圖表：權杖取得
許多 web 應用程式會需要使用 OAuth toonot 登 hello 中唯一的使用者，但也 tooaccess 代表 hello 使用者的 web 服務。 此案例中結合 OpenID Connect 使用者同時取得授權時發生的驗證程式碼，您可以使用 tooget 存取語彙基元如果您使用 hello OAuth 授權碼流程。

hello 完整 OpenID Connect 登入和權杖取得流程看起來類似 toohello 下圖。 我們將描述 hello hello 發行項的下一章節詳細說明每個步驟。

![OpenID Connect 通訊協定：權杖取得](../../media/active-directory-v2-flows/convergence_scenarios_webapp_webapi.png)

## 取得存取權杖
tooacquire 存取權杖，修改 hello 登入要求：

```
// Line breaks are for legibility only.

GET https://login.microsoftonline.com/{tenant}/oauth2/v2.0/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e        // Your registered Application ID
&response_type=id_token%20code
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F       // Your registered redirect URI, URL encoded
&response_mode=form_post                              // 'query', 'form_post', or 'fragment'
&scope=openid%20                                      // Include both 'openid' and scopes that your app needs  
offline_access%20                                         
https%3A%2F%2Fgraph.microsoft.com%2Fmail.read
&state=12345                                          // Any value, provided by your app
&nonce=678910                                         // Any value, provided by your app
```

> [!TIP]
> 按一下下列連結 tooexecute hello 這個要求。 登入之後，您的瀏覽器是 ID 語彙基元與 hello 網址列中的程式碼的重新導向的 toohttps://localhost/myapp/。 請注意，此要求會使用 `response_mode=query` (僅限用於示範)。 建議您使用 `response_mode=form_post`。
> <a href="https://login.microsoftonline.com/common/oauth2/v2.0/authorize?client_id=6731de76-14a6-49ae-97bc-6eba6914391e&response_type=id_token%20code&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F&response_mode=query&scope=openid%20offline_access%20https%3A%2F%2Fgraph.microsoft.com%2Fmail.read&state=12345&nonce=678910" target="_blank">https://login.microsoftonline.com/common/oauth2/v2.0/authorize...</a>
> 
> 

藉由包含權限範圍，hello 要求中和使用`response_type=id_token code`，hello v2.0 端點可確保該 hello 使用者同意 toohello hello 中指出的權限`scope`查詢參數。 它會傳回存取權杖的授權碼 tooyour 應用程式 tooexchange。

### 成功回應
使用 `response_mode=form_post` 的成功回應看起來像這樣：

```
POST /myapp/ HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded

id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWmNB...&code=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...&state=12345
```

| 參數 | 說明 |
| --- | --- |
| id_token |hello hello 應用程式要求的 ID 語彙基元。 您可以使用 hello ID 語彙基元 tooverify hello 使用者的身分識別，並開始與 hello 使用者工作階段。 您可以在 hello 找到 ID 語彙基元和其內容的更多詳細[v2.0 端點權杖參考](active-directory-v2-tokens.md)。 |
| code |hello hello 應用程式要求授權碼。 hello 應用程式可以使用 hello 目標資源的 hello 授權程式碼 toorequest 存取權杖。 授權碼的存留期很短。 授權碼的有效期通常大約是 10 分鐘。 |
| state |如果在 hello 要求中，相同的值應該會出現在 hello 回應 hello 包含狀態參數。 hello 應用程式應該確認 hello 要求和回應中的 hello 狀態值完全相同。 |

### 錯誤回應
錯誤回應可能也會傳送 toohello 重新導向 URI 以便 hello 應用程式可以適當處理這些。 錯誤回應看起來像這樣：

```
POST /myapp/ HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded

error=access_denied&error_description=the+user+canceled+the+authentication
```

| 參數 | 說明 |
| --- | --- |
| 錯誤 |您可以使用的錯誤，就會發生，並 tooreact tooerrors tooclassify 類型錯誤的程式碼字串。 |
| error_description |特定的錯誤訊息，可協助您找出 hello 的驗證錯誤的根本原因。 |

如需可能的錯誤碼說明及建議的用戶端回應，請參閱[授權端點錯誤的錯誤碼](#error-codes-for-authorization-endpoint-errors)。

當您擁有授權碼及 ID 語彙基元時，您可以 hello 使用者登入，並代表它取得存取權杖。 toosign hello 中的使用者，您必須驗證 hello 的 ID 語彙基元[確實依](#validate-the-id-token)。 tooget 存取權杖，請依照下列中所述的 hello 步驟我們[OAuth 通訊協定文件](active-directory-v2-protocols-oauth-code.md#request-an-access-token)。
