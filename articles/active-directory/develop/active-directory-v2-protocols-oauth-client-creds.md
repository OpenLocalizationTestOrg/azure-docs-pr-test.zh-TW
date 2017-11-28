---
title: "Azure AD aaaUse v2.0 tooaccess 保護不需要使用者互動的資源 |Microsoft 文件"
description: "建立 web 應用程式藉由使用 Azure AD hello hello OAuth 2.0 驗證通訊協定的實作。"
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 9b7cfbd7-f89f-4e33-aff2-414edd584b07
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 0003ec836d633a5466c48033adedac1108f27203
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# Azure Active Directory v2.0 和 hello OAuth 2.0 用戶端認證流程
您可以使用 hello [OAuth 2.0 用戶端認證授與](http://tools.ietf.org/html/rfc6749#section-4.4)，有時稱為*兩腳 OAuth*，使用的應用程式的 hello 識別 tooaccess web 資源。 這種類型的授權通常用於必須在 hello 背景，而不需立即與使用者互動中執行的伺服器對伺服器互動。 這些類型的應用程式通常會參考的 tooas*精靈*或*服務帳戶*。

> [!NOTE]
> hello v2.0 端點不支援所有的 Azure Active Directory 的案例和功能。 toodetermine 是否應該使用 hello v2.0 端點，閱讀有關[v2.0 限制](active-directory-v2-limitations.md)。
>
>

在較為典型的 hello*三腳 OAuth*，用戶端應用程式是代表特定使用者授與權限 tooaccess 資源。 hello 權限從 hello 使用者 toohello 應用程式，通常是在 hello 委派[同意](active-directory-v2-scopes.md)程序。 不過，在 hello 用戶端認證流程中，權限會授與直接 toohello 應用程式本身。 當 hello 應用程式提出的權杖 tooa 資源時，hello 資源會強制 hello 應用程式本身具有授權 tooperform 動作，而且不該 hello 使用者已授權。

## 通訊協定圖表
hello 整個用戶端認證流程看起來類似 toohello 下圖。 我們將描述每個 hello 本文中稍後的步驟。

![用戶端認證流程](../../media/active-directory-v2-flows/convergence_scenarios_client_creds.png)

## 取得直接授權
應用程式通常會接收直接授權 tooaccess 資源中有兩種： 透過在 hello 資源存取控制清單 (ACL) 或 Azure Active Directory (Azure AD) 中的應用程式的權限指派。 這兩種方法是在 Azure AD 中最常見的 hello 而且我們建議它們的用戶端與執行 hello 用戶端認證流程的資源。 資源可以選擇 tooauthorize 其用戶端中的其他方式，不過。 每個資源伺服器，可以選擇最有意義 hello 其應用程式的 hello 方法。

### 存取控制清單
資源提供者可能會根據它所知的「應用程式識別碼」清單，強制執行授權檢查並授與特定層級的存取權。 當 hello 資源從 hello v2.0 端點接收到權杖時，它可以解碼 hello 語彙基元，並從 hello 擷取 hello 用戶端應用程式識別碼`appid`和`iss`宣告。 然後它會比較 hello 應用程式對它所維護的 ACL。 hello ACL 的資料粒度和資源之間可能會大幅不同方法。

常見使用案例是的 toouse ACL toorun 測試 web 應用程式或 Web api。 hello Web API 可能會授與完整權限 tooa 特定用戶端的子集。 hello API，toorun 端對端測試建立測試用戶端取得語彙基元從 hello v2.0 端點，然後將它們傳送 toohello 應用程式開發介面。 hello 應用程式開發介面，然後檢查 hello ACL hello 測試 toohello API 的完整功能的完整存取權的用戶端應用程式識別碼。 如果您使用這種 ACL，請務必 toovalidate 不僅 hello 呼叫者的`appid`值。 也會驗證該 hello `iss` hello 語彙基元的值是受信任。

這種類型是授權的很常見的精靈和需要 tooaccess 資料取用者的使用者具有個人 Microsoft 帳戶所擁有的服務帳戶。 針對組織所擁有的資料，我們建議您取得必要的授權 hello 透過應用程式權限。

### 應用程式權限
而不是使用 Acl，您可以使用應用程式開發介面 tooexpose 一組應用程式權限。 應用程式權限已獲得 tooan 應用程式，組織的系統管理員，可以使用只有 tooaccess 資料擁有該組織的員工。 例如，Microsoft Graph 會公開數個應用程式的權限 toodo hello 下列：

* 讀取所有信箱中的郵件
* 讀取和寫入所有信箱中的郵件
* 以任何使用者身分傳送郵件
* 讀取目錄資料

如需有關應用程式權限的詳細資訊，請移太[Microsoft Graph](https://graph.microsoft.io)。

toouse 應用程式中的應用程式權限 hello 我們在 hello 下一節中討論的步驟。

#### 要求在 hello 應用程式註冊入口網站中的 hello 權限
1. 移 tooyour 應用程式在 hello[應用程式註冊入口網站](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)，或[建立應用程式](active-directory-v2-app-registration.md)，如果您還沒有這麼做。 您將需要 toouse 至少一個應用程式密碼，當您建立您的應用程式。
2. 找出 hello**應用程式的直接權限**區段，然後再新增您的應用程式所需的 hello 權限。
3. **儲存**hello 應用程式註冊。

#### 建議使用： 號 hello 使用者 tooyour 應用程式中
一般來說，當您建置的應用程式使用應用程式權限，hello 應用程式需要頁面或檢視的 hello 系統管理員核准 hello 應用程式的權限。 此頁面可以屬於 hello 應用程式的登入流程，hello 應用程式設定的一部分，或可以是專用，「 連接 」 流程。 在許多情況下，是合理的 hello 應用程式 tooshow 這 「 連接 」 檢視只能在使用者登入工作或學校的 Microsoft 帳戶之後。

如果您簽署 hello tooyour 應用程式中的使用者，您可以識別 hello 組織 toowhich hello 使用者所屬之前您詢問 hello 使用者 tooapprove hello 應用程式權限。 雖然這並非絕對必要，但這麼做可協助您為使用者建立更直覺式的體驗。 在後續的 toosign hello 使用者我們[v2.0 通訊協定教學課程](active-directory-v2-protocols.md)。

#### 從目錄管理員要求 hello 權限
當您準備好 toorequest hello 組織的系統管理員權限時，您可以重新導向 hello 使用者 toohello v2.0*系統管理員同意端點*。

```
// Line breaks are for legibility only.

GET https://login.microsoftonline.com/{tenant}/adminconsent?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&state=12345
&redirect_uri=http://localhost/myapp/permissions
```

```
// Pro tip: Try pasting hello following request in a browser!
```

```
https://login.microsoftonline.com/common/adminconsent?client_id=6731de76-14a6-49ae-97bc-6eba6914391e&state=12345&redirect_uri=http://localhost/myapp/permissions
```

| 參數 | 條件 | 說明 |
| --- | --- | --- |
| tenant |必要 |您想要從 toorequest 權限 hello 目錄租用戶。 這可以採用 GUID 或易記名稱格式。 如果您不知道哪個租用戶 hello 使用者所屬的 tooand 想的 toolet 它們使用任何租用戶使用登入`common`。 |
| client_id |必要 |hello 應用程式識別碼的 hello[應用程式註冊入口網站](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)指派 tooyour 應用程式。 |
| redirect_uri |必要 |hello 重新導向您想要針對應用程式 toohandle 傳送 hello 回應 toobe 的 URI。 它必須完全符合其中一個 hello 重新導向您在 hello 入口網站註冊 Uri 不同之處在於它必須是 URL 編碼，而且可以有其他路徑區段。 |
| state |建議 |包含在 hello 要求也 hello 權杖回應中傳回的值。 它可以是您所想要內容中的字串。 hello 狀態是使用的 tooencode hello 應用程式中的 hello 使用者狀態資訊之前發生 hello 驗證要求，例如 hello 頁面或檢視上。 |

此時，Azure AD 會強制執行只租用戶系統管理員可登入 toocomplete hello 要求。 hello 系統管理員將會詢問的 tooapprove 所有 hello 您要求的 hello 應用程式註冊入口網站中的應用程式的直接的應用程式權限。

##### 成功回應
如果 hello 系統管理員核准 hello 應用程式的權限，成功的回應 hello 看起來像這樣：

```
GET http://localhost/myapp/permissions?tenant=a8990e1f-ff32-408a-9f8e-78d3b9139b95&state=state=12345&admin_consent=True
```

| 參數 | 說明 |
| --- | --- | --- |
| tenant |hello 目錄租用戶授與您的應用程式 hello 權限的要求，GUID 格式。 |
| state |包含在 hello 要求也 hello 權杖回應中傳回的值。 它可以是您所想要內容中的字串。 hello 狀態是使用的 tooencode hello 應用程式中的 hello 使用者狀態資訊之前發生 hello 驗證要求，例如 hello 頁面或檢視上。 |
| admin_consent |設定得**true**。 |

##### 錯誤回應
如果 hello 系統管理員不會核准 hello 應用程式的權限，hello 失敗回應看起來像這樣：

```
GET http://localhost/myapp/permissions?error=permission_denied&error_description=The+admin+canceled+the+request
```

| 參數 | 說明 |
| --- | --- | --- |
| 錯誤 |您可以使用 tooclassify 類型錯誤的程式碼字串的錯誤，但您可以使用 tooreact tooerrors。 |
| error_description |特定的錯誤訊息，可協助您找出 hello 根本原因的錯誤。 |

收到 hello 應用程式佈建端點的成功回應之後，您的應用程式已取得要求的 hello 直接應用程式權限。 現在您可以要求您想要的 hello 資源語彙基元。

## 取得權杖
您已取得 hello 必要的授權應用程式之後，繼續進行 api 取得存取權杖。 tooget 使用 hello 用戶端認證授與的語彙基元傳送 POST 要求 toohello `/token` v2.0 端點：

### 第一種情況︰使用共用密碼的存取權杖要求

```
POST /common/oauth2/v2.0/token HTTP/1.1
Host: login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

client_id=535fb089-9ff3-47b6-9bfb-4f1264799865&scope=https%3A%2F%2Fgraph.microsoft.com%2F.default&client_secret=qWgdYAmab0YSkuL1qKv5bPX&grant_type=client_credentials
```

```
curl -X POST -H "Content-Type: application/x-www-form-urlencoded" -d 'client_id=535fb089-9ff3-47b6-9bfb-4f1264799865&scope=https%3A%2F%2Fgraph.microsoft.com%2F.default&client_secret=qWgdYAmab0YSkuL1qKv5bPX&grant_type=client_credentials' 'https://login.microsoftonline.com/common/oauth2/v2.0/token'
```

| 參數 | 條件 | 說明 |
| --- | --- | --- |
| client_id |必要 |hello 應用程式識別碼的 hello[應用程式註冊入口網站](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)指派 tooyour 應用程式。 |
| scope |必要 |傳遞的 hello hello 值`scope`這個要求中的參數應該是 hello 資源識別元 (應用程式識別碼 URI) 與 hello 貼附，依您想要的 hello 資源`.default`後置詞。 例如 hello Microsoft Graph hello 值是`https://graph.microsoft.com/.default`。 這個值會通知所有 hello 直接應用程式的權限您已設定您的應用程式，它應該都發出 hello 與您想要的 hello 資源相關聯的語彙基元 toouse hello v2.0 端點。 |
| client_secret |必要 |hello 您產生 hello 應用程式註冊入口網站中的應用程式的應用程式密碼。 |
| grant_type |必要 |必須是 `client_credentials`。 |

### 第二種情況︰使用憑證的存取權杖要求

```
POST /common/oauth2/v2.0/token HTTP/1.1
Host: login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

scope=https%3A%2F%2Fgraph.microsoft.com%2F.default&client_id=97e0a5b7-d745-40b6-94fe-5f77d35c6e05&client_assertion_type=urn%3Aietf%3Aparams%3Aoauth%3Aclient-assertion-type%3Ajwt-bearer&client_assertion=eyJhbGciOiJSUzI1NiIsIng1dCI6Imd4OHRHeXN5amNScUtqRlBuZDdSRnd2d1pJMCJ9.eyJ{a lot of characters here}M8U3bSUKKJDEg&grant_type=client_credentials
```

| 參數 | 條件 | 說明 |
| --- | --- | --- |
| client_id |必要 |hello 應用程式識別碼的 hello[應用程式註冊入口網站](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)指派 tooyour 應用程式。 |
| scope |必要 |傳遞的 hello hello 值`scope`這個要求中的參數應該是 hello 資源識別元 (應用程式識別碼 URI) 與 hello 貼附，依您想要的 hello 資源`.default`後置詞。 例如 hello Microsoft Graph hello 值是`https://graph.microsoft.com/.default`。 這個值會通知所有 hello 直接應用程式的權限您已設定您的應用程式，它應該都發出 hello 與您想要的 hello 資源相關聯的語彙基元 toouse hello v2.0 端點。 |
| client_assertion_type |必要 |hello 值必須是`urn:ietf:params:oauth:client-assertion-type:jwt-bearer` |
| client_assertion |必要 | 判斷提示 （JSON Web 權杖），您需要 toocreate hello 以簽署憑證，您會註冊為您的應用程式的認證。 閱讀有關[憑證認證](active-directory-certificate-credentials.md)toolearn 如何 tooregister hello 判斷提示您憑證和 hello 的格式。|
| grant_type |必要 |必須是 `client_credentials`。 |

請注意，hello 參數幾乎 hello 與 hello 大小寫的 hello 要求相同的共用密碼之處在於會以兩個參數取代 hello client_secret 參數： client_assertion_type 和 client_assertion。

### 成功回應
成功的回應看起來會像這樣：

```
{
  "token_type": "Bearer",
  "expires_in": 3599,
  "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWmNBVGZNNXBP..."
}
```

| 參數 | 說明 |
| --- | --- |
| access_token |hello 要求的存取權杖。 hello 應用程式可以使用這個受保護資源，例如 tooa Web API 的語彙基元 tooauthenticate toohello。 |
| token_type |表示 hello 語彙基元型別值。 hello Azure AD 支援的類型`bearer`。 |
| expires_in |多久 hello 存取權杖是有效 （以秒為單位）。 |

### 錯誤回應
錯誤回應看起來像這樣：

```
{
  "error": "invalid_scope",
  "error_description": "AADSTS70011: hello provided value for hello input parameter 'scope' is not valid. hello scope https://foo.microsoft.com/.default is not valid.\r\nTrace ID: 255d1aef-8c98-452f-ac51-23d051240864\r\nCorrelation ID: fb3d2015-bc17-4bb9-bb85-30c5cf1aaaa7\r\nTimestamp: 2016-01-09 02:02:12Z",
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
| 錯誤 |您可以使用的錯誤，就會發生，並 tooreact tooerrors tooclassify 類型錯誤的程式碼字串。 |
| error_description |特定的錯誤訊息，以幫助您識別 hello 的驗證錯誤的根本原因。 |
| error_codes |可協助進行診斷的 STS 特定錯誤碼清單。 |
| timestamp |hello hello 錯誤發生的時間。 |
| trace_id |可以幫助診斷的 hello 要求的唯一識別碼。 |
| correlation_id |可協助進行診斷，在元件上的 hello 要求的唯一識別碼。 |

## 使用權杖
現在您已取得語彙基元，使用 hello 語彙基元 toomake 要求 toohello 資源。 Hello 權杖過期時，重複 hello 要求 toohello`/token`端點 tooacquire 全新的存取語彙基元。

```
GET /v1.0/me/messages
Host: https://graph.microsoft.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
```

```
// Pro tip: Try hello following command! (Replace hello token with your own.)
```

```
curl -X GET -H "Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q" 'https://graph.microsoft.com/v1.0/me/messages'
```

## 程式碼範例
toosee 範例應用程式的實作 hello 用戶端認證授與，使用 hello 系統管理員同意端點，請參閱我們[v2.0 協助程式程式碼範例](https://github.com/Azure-Samples/active-directory-dotnet-daemon-v2)。
