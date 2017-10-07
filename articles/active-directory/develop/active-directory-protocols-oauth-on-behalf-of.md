---
title: "使用 OAuth2.0 上-on-behalf-of 草稿規格 aaaAzure AD 服務 tooservice auth |Microsoft 文件"
description: "本文說明如何： toouse HTTP 訊息 tooimplement 服務 tooservice 驗證使用 hello OAuth2.0 代表的流程。"
services: active-directory
documentationcenter: .net
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 09f6f318-e88b-4024-9ee1-e7f09fb19a82
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 55b7fcfe6c0223bddedd8d8fa2defcb5769b43c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# 服務 tooservice 呼叫 hello 代表的資料流程中使用委派的使用者識別
OAuth 2.0 On-Behalf-Of 流程 hello 做 hello 實務應用程式要叫用服務/web API，又需要 toocall 另一個服務/web API。 hello 概念是 toopropagate hello 委派使用者識別與透過 hello 要求鏈的權限。 Hello 中介層服務進行驗證的 toomake 要求 toohello 下游服務，它會代表 hello 使用者需要 toosecure 從 Azure Active Directory (Azure AD)，存取權杖。

## 代理者流程圖
假設該 hello 使用者已驗證的應用程式使用 hello [OAuth 2.0 授權碼授與流程](active-directory-protocols-oauth-code.md)。 此時，hello 應用程式會有存取語彙基元 (語彙基元 A) 與 hello 使用者宣告和同意 tooaccess hello 中間層 web 應用程式開發介面 (API A)。 現在，應用程式開發介面的需要 toomake 已驗證的要求 toohello 下游 web 應用程式開發介面 (API B)。

hello 遵照的步驟，構成 hello 代表的流程，並說明，請參閱下列圖表中的 hello hello 協助。

![OAuth2.0 代理者流程](media/active-directory-protocols-oauth-on-behalf-of/active-directory-protocols-oauth-on-behalf-of-flow.png)


1. hello 用戶端應用程式會要求 tooAPI 與 hello 語彙基元 a。
2. 應用程式開發介面的驗證 toohello Azure AD 權杖發行端點，並要求權杖 tooaccess API b。
3. hello Azure AD 權杖發行端點會驗證與權杖的應用程式開發介面的認證和問題 hello API B （語彙基元 B） 的存取權杖。
4. hello 權杖 B hello 要求 tooAPI B.hello 授權標頭中設定
5. 應用程式開發介面 b 所傳回資料從受保護資源的 hello

## 在 Azure AD 中註冊 hello 應用程式及服務
在 Azure AD 中註冊 hello 用戶端應用程式和 hello 中介層服務。
### 註冊 hello 中介層服務
1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. Hello 頂端列上，按一下您的帳戶，並在 hello**目錄**清單中，選擇您希望 tooregister 您的應用程式的 hello Active Directory 租用戶。
3. 按一下**更服務**在 hello 左側瀏覽，然後選擇  **Azure Active Directory**。
4. 按一下 [應用程式註冊]，然後選擇 [新應用程式註冊]。
5. 輸入 hello 應用程式的易記名稱並選取 hello 應用程式類型。 登入 URL 組 hello 或重新導向 URL toohello 基底 URL，請根據 hello 應用程式類型。 按一下**建立**toocreate hello 應用程式。
6. 當您還在 hello Azure 入口網站中，選擇您的應用程式，然後按一下**設定**。 從 hello 設定] 功能表，選擇 [**金鑰**和加入的機碼-選取金鑰的持續時間的 1 年或 2 年。 儲存此頁面、 hello 機碼值將會顯示、 複製和 hello 值儲存在安全的位置，而您必須在您實作-此索引鍵更新 tooconfigure hello 應用程式設定此機碼值不會顯示一次，也可以擷取任何其他方法，請記錄它，只要是可見的 hello Azure 入口網站。

### 註冊 hello 用戶端應用程式
1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. Hello 頂端列上，按一下您的帳戶，並在 hello**目錄**清單中，選擇您希望 tooregister 您的應用程式的 hello Active Directory 租用戶。
3. 按一下**更服務**在 hello 左側瀏覽，然後選擇  **Azure Active Directory**。
4. 按一下 [應用程式註冊]，然後選擇 [新應用程式註冊]。
5. 輸入 hello 應用程式的易記名稱並選取 hello 應用程式類型。 登入 URL 組 hello 或重新導向 URL toohello 基底 URL，請根據 hello 應用程式類型。 按一下**建立**toocreate hello 應用程式。
6. 設定權限，您的應用程式-hello 設定 功能表中，選擇 hello**必要的權限**區段中，按一下**新增**，然後**選取應用程式開發介面**，和型別 hello在 hello 文字方塊中的 hello 中介層服務的名稱。 接著，按一下 [選取權限] 並選取 [存取*服務名稱*]。

### 設定已知的用戶端應用程式
在此案例中，hello 中介層服務會有任何使用者互動 tooobtain hello 使用者的同意 tooaccess hello 下游應用程式開發介面。 因此，hello 下游應用程式開發介面必須呈現選項 toogrant 存取 toohello 前方 hello 同意步驟，在驗證期間的一部分。
tooachieve tooexplicitly 繫結 hello 用戶端應用程式的註冊 Azure AD 中的 hello 中介層服務，會合併在單一對話方塊所需的 hello 用戶端和中介層的 hello 同意 hello 註冊下方，遵循 hello 的步驟。
1. 瀏覽 toohello 中介層服務註冊，並按一下**資訊清單**tooopen hello 資訊清單編輯器。
2. 在 hello 資訊清單中，找出 hello`knownClientApplications`陣列屬性，並新增 hello hello 用戶端應用程式的用戶端識別碼做為項目。
3. 按一下儲存按鈕 hello 儲存 hello 資訊清單。

## 服務 tooservice 存取權杖要求
toorequest 存取權杖，請以下列參數的 hello 的 HTTP POST toohello 租用戶特定 Azure AD 端點。

```
https://login.microsoftonline.com/<tenant>/oauth2/token
```
有兩種情況下，根據 hello 用戶端應用程式是否選擇 toobe 受到共用的密碼或憑證。

### 第一種情況︰使用共用密碼的存取權杖要求
當使用共用的密碼時，服務對服務存取權杖要求包含下列參數的 hello:

| 參數 |  | 說明 |
| --- | --- | --- |
| grant_type |必要 | hello 的 hello 語彙基元要求類型。 使用 JWT 的要求，hello 值必須是**urn: ietf:params:oauth:grant-型別： jwt-承載**。 |
| assertion |必要 | hello hello 要求中所使用的 hello 權杖值。 |
| client_id |必要 | hello 應用程式識別碼期間，指派 toohello 呼叫服務的 Azure AD 註冊。 toofind hello 應用程式識別碼 hello Azure 管理入口網站中的按一下**Active Directory**，按一下 hello 目錄，然後按一下hello 應用程式名稱。 |
| client_secret |必要 | 在 Azure AD 中呼叫服務的 hello 註冊 hello 索引鍵。 這個值應該注意在 hello 次註冊。 |
| resource |必要 | hello hello 接收服務 （受保護的資源） 應用程式識別碼 URI。 toofind hello 應用程式識別碼 URI，在 hello Azure 管理入口網站中，按一下**Active Directory**，按一下 hello 目錄中，按一下 hello 應用程式名稱，按一下**所有設定**，然後按一下**屬性**. |
| requested_token_use |必要 | 指定應該如何處理 hello 要求。 Hello 代表的流程，在 hello 值必須是**on_behalf_of**。 |
| scope |必要 | 並以空格分隔 hello 權杖要求的範圍清單。 OpenID connect，hello 範圍**openid**必須指定。|

#### 範例
hello 下列 HTTP POST 要求 hello https://graph.windows.net web API 的存取權杖。 hello`client_id`識別 hello 要求 hello 存取權杖的服務。

```
// line breaks for legibility only

POST /oauth2/token HTTP/1.1
Host: login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

grant_type=urn%3Aietf%3Aparams%3Aoauth%3Agrant-type%3Ajwt-bearer
&client_id=625391af-c675-43e5-8e44-edd3e30ceb15
&client_secret=0Y1W%2BY3yYb3d9N8vSjvm8WrGzVZaAaHbHHcGbcgG%2BoI%3D
&resource=https%3A%2F%2Fgraph.windows.net
&assertion=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6InowMzl6ZHNGdWl6cEJmQlZLMVRuMjVRSFlPMCIsImtpZCI6InowMzl6ZHNGdWl6cEJmQlZLMVRuMjVRSFlPMCJ9.eyJhdWQiOiJodHRwczovL2Rkb2JhbGlhbm91dGxvb2sub25taWNyb3NvZnQuY29tLzE5MjNmODYyLWU2ZGMtNDFhMy04MWRhLTgwMmJhZTAwYWY2ZCIsImlzcyI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzI2MDM5Y2NlLTQ4OWQtNDAwMi04MjkzLTViMGM1MTM0ZWFjYi8iLCJpYXQiOjE0OTM0MjMxNTIsIm5iZiI6MTQ5MzQyMzE1MiwiZXhwIjoxNDkzNDY2NjUyLCJhY3IiOiIxIiwiYWlvIjoiWTJaZ1lCRFF2aTlVZEc0LzM0L3dpQndqbjhYeVp4YmR1TFhmVE1QeG8yYlN2elgreHBVQSIsImFtciI6WyJwd2QiXSwiYXBwaWQiOiJiMzE1MDA3OS03YmViLTQxN2YtYTA2YS0zZmRjNzhjMzI1NDUiLCJhcHBpZGFjciI6IjAiLCJlX2V4cCI6MzAyNDAwLCJmYW1pbHlfbmFtZSI6IlRlc3QiLCJnaXZlbl9uYW1lIjoiTmF2eWEiLCJpcGFkZHIiOiIxNjcuMjIwLjEuMTc3IiwibmFtZSI6Ik5hdnlhIFRlc3QiLCJvaWQiOiIxY2Q0YmNhYy1iODA4LTQyM2EtOWUyZi04MjdmYmIxYmI3MzkiLCJwbGF0ZiI6IjMiLCJzY3AiOiJ1c2VyX2ltcGVyc29uYXRpb24iLCJzdWIiOiJEVXpYbkdKMDJIUk0zRW5pbDFxdjZCakxTNUllQy0tQ2ZpbzRxS1MzNEc4IiwidGlkIjoiMjYwMzljY2UtNDg5ZC00MDAyLTgyOTMtNWIwYzUxMzRlYWNiIiwidW5pcXVlX25hbWUiOiJuYXZ5YUBkZG9iYWxpYW5vdXRsb29rLm9ubWljcm9zb2Z0LmNvbSIsInVwbiI6Im5hdnlhQGRkb2JhbGlhbm91dGxvb2sub25taWNyb3NvZnQuY29tIiwidmVyIjoiMS4wIn0.R-Ke-XO7lK0r5uLwxB8g5CrcPAwRln5SccJCfEjU6IUqpqcjWcDzeDdNOySiVPDU_ZU5knJmzRCF8fcjFtPsaA4R7vdIEbDuOur15FXSvE8FvVSjP_49OH6hBYqoSUAslN3FMfbO6Z8YfCIY4tSOB2I6ahQ_x4ZWFWglC3w5mK-_4iX81bqi95eV4RUKefUuHhQDXtWhrSgIEC0YiluMvA4TnaJdLq_tWXIc4_Tq_KfpkvI004ONKgU7EAMEr1wZ4aDcJV2yf22gQ1sCSig6EGSTmmzDuEPsYiyd4NhidRZJP4HiiQh-hePBQsgcSgYGvz9wC6n57ufYKh2wm_Ti3Q
&requested_token_use=on_behalf_of
&scope=openid
```

### 第二種情況︰使用憑證的存取權杖要求
使用憑證服務對服務存取權杖要求包含下列參數的 hello:

| 參數 |  | 說明 |
| --- | --- | --- |
| grant_type |必要 | hello 的 hello 語彙基元要求類型。 使用 JWT 的要求，hello 值必須是**urn: ietf:params:oauth:grant-型別： jwt-承載**。 |
| assertion |必要 | hello hello 要求中所使用的 hello 權杖值。 |
| client_id |必要 | hello 應用程式識別碼期間，指派 toohello 呼叫服務的 Azure AD 註冊。 toofind hello 應用程式識別碼 hello Azure 管理入口網站中的按一下**Active Directory**，按一下 hello 目錄，然後按一下hello 應用程式名稱。 |
| client_assertion_type |必要 |hello 值必須是`urn:ietf:params:oauth:client-assertion-type:jwt-bearer` |
| client_assertion |必要 | 判斷提示 （JSON Web 權杖），您需要 toocreate hello 以簽署憑證，您會註冊為您的應用程式的認證。  閱讀有關[憑證認證](active-directory-certificate-credentials.md)toolearn 如何 tooregister hello 判斷提示您憑證和 hello 的格式。|
| resource |必要 | hello hello 接收服務 （受保護的資源） 應用程式識別碼 URI。 toofind hello 應用程式識別碼 URI，在 hello Azure 管理入口網站中，按一下**Active Directory**，按一下 hello 目錄中，按一下 hello 應用程式名稱，按一下**所有設定**，然後按一下**屬性**. |
| requested_token_use |必要 | 指定應該如何處理 hello 要求。 Hello 代表的流程，在 hello 值必須是**on_behalf_of**。 |
| scope |必要 | 並以空格分隔 hello 權杖要求的範圍清單。 OpenID connect，hello 範圍**openid**必須指定。|

請注意，hello 參數幾乎 hello 與 hello 大小寫的 hello 要求相同的共用密碼之處在於會以兩個參數取代 hello client_secret 參數： client_assertion_type 和 client_assertion。

#### 範例
hello 下列 HTTP POST 要求的憑證的 hello https://graph.windows.net web API 的存取權杖。 hello`client_id`識別 hello 要求 hello 存取權杖的服務。

```
// line breaks for legibility only

POST /oauth2/token HTTP/1.1
Host: login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

grant_type=urn%3Aietf%3Aparams%3Aoauth%3Agrant-type%3Ajwt-bearer
&client_id=625391af-c675-43e5-8e44-edd3e30ceb15
&client_assertion_type=urn%3Aietf%3Aparams%3Aoauth%3Aclient-assertion-type%3Ajwt-bearer
&client_assertion=eyJhbGciOiJSUzI1NiIsIng1dCI6Imd4OHRHeXN5amNScUtqRlBuZDdSRnd2d1pJMCJ9.eyJ{a lot of characters here}M8U3bSUKKJDEg
&resource=https%3A%2F%2Fgraph.windows.net
&assertion=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6InowMzl6ZHNGdWl6cEJmQlZLMVRuMjVRSFlPMCIsImtpZCI6InowMzl6ZHNGdWl6cEJmQlZLMVRuMjVRSFlPMCJ9.eyJhdWQiOiJodHRwczovL2Rkb2JhbGlhbm91dGxvb2sub25taWNyb3NvZnQuY29tLzE5MjNmODYyLWU2ZGMtNDFhMy04MWRhLTgwMmJhZTAwYWY2ZCIsImlzcyI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzI2MDM5Y2NlLTQ4OWQtNDAwMi04MjkzLTViMGM1MTM0ZWFjYi8iLCJpYXQiOjE0OTM0MjMxNTIsIm5iZiI6MTQ5MzQyMzE1MiwiZXhwIjoxNDkzNDY2NjUyLCJhY3IiOiIxIiwiYWlvIjoiWTJaZ1lCRFF2aTlVZEc0LzM0L3dpQndqbjhYeVp4YmR1TFhmVE1QeG8yYlN2elgreHBVQSIsImFtciI6WyJwd2QiXSwiYXBwaWQiOiJiMzE1MDA3OS03YmViLTQxN2YtYTA2YS0zZmRjNzhjMzI1NDUiLCJhcHBpZGFjciI6IjAiLCJlX2V4cCI6MzAyNDAwLCJmYW1pbHlfbmFtZSI6IlRlc3QiLCJnaXZlbl9uYW1lIjoiTmF2eWEiLCJpcGFkZHIiOiIxNjcuMjIwLjEuMTc3IiwibmFtZSI6Ik5hdnlhIFRlc3QiLCJvaWQiOiIxY2Q0YmNhYy1iODA4LTQyM2EtOWUyZi04MjdmYmIxYmI3MzkiLCJwbGF0ZiI6IjMiLCJzY3AiOiJ1c2VyX2ltcGVyc29uYXRpb24iLCJzdWIiOiJEVXpYbkdKMDJIUk0zRW5pbDFxdjZCakxTNUllQy0tQ2ZpbzRxS1MzNEc4IiwidGlkIjoiMjYwMzljY2UtNDg5ZC00MDAyLTgyOTMtNWIwYzUxMzRlYWNiIiwidW5pcXVlX25hbWUiOiJuYXZ5YUBkZG9iYWxpYW5vdXRsb29rLm9ubWljcm9zb2Z0LmNvbSIsInVwbiI6Im5hdnlhQGRkb2JhbGlhbm91dGxvb2sub25taWNyb3NvZnQuY29tIiwidmVyIjoiMS4wIn0.R-Ke-XO7lK0r5uLwxB8g5CrcPAwRln5SccJCfEjU6IUqpqcjWcDzeDdNOySiVPDU_ZU5knJmzRCF8fcjFtPsaA4R7vdIEbDuOur15FXSvE8FvVSjP_49OH6hBYqoSUAslN3FMfbO6Z8YfCIY4tSOB2I6ahQ_x4ZWFWglC3w5mK-_4iX81bqi95eV4RUKefUuHhQDXtWhrSgIEC0YiluMvA4TnaJdLq_tWXIc4_Tq_KfpkvI004ONKgU7EAMEr1wZ4aDcJV2yf22gQ1sCSig6EGSTmmzDuEPsYiyd4NhidRZJP4HiiQh-hePBQsgcSgYGvz9wC6n57ufYKh2wm_Ti3Q
&requested_token_use=on_behalf_of
&scope=openid
```

## 服務 tooservice 存取權杖回應
成功回應是以下列參數的 hello 的 JSON OAuth 2.0 回應。

| 參數 | 說明 |
| --- | --- |
| token_type |表示 hello 語彙基元型別值。 hello Azure AD 支援的類型**承載**。 如需承載權杖的詳細資訊，請參閱 hello [OAuth 2.0 授權架構： 承載權杖用法 (RFC 6750)](http://www.rfc-editor.org/rfc/rfc6750.txt)。 |
| scope |hello hello 語彙基元中授與的存取範圍。 |
| expires_in |hello 長度的時間 hello 存取權杖是有效 （以秒為單位）。 |
| expires_on |hello hello 存取權杖到期的時間。 hello 日期以 hello 的秒數表示從 1970年-01-01T0:0:0Z UTC 直到 hello 到期時間。 這個值是使用的 toodetermine hello 存留期，快取權杖。 |
| resource |hello hello 接收服務 （受保護的資源） 應用程式識別碼 URI。 |
| access_token |hello 要求的存取權杖。 呼叫服務的 hello 可以使用這個語彙基元 tooauthenticate toohello 接收服務。 |
| id_token |hello 要求的 id 語彙基元。 呼叫服務的 hello 可以使用此 tooverify hello 使用者身分識別，並開始與 hello 使用者工作階段。 |
| refresh_token |hello hello 要求的存取權杖重新整理權杖。 呼叫服務的 hello 後可以使用這個語彙基元 toorequest 另一個存取權杖 hello 目前存取權杖到期。 |

### 成功回應範例
hello 下列範例顯示 hello https://graph.windows.net web API 的存取權杖的成功回應 tooa 要求。

```
{
    "token_type":"Bearer",
    "scope":"User.Read",
    "expires_in":"43482",
    "ext_expires_in":"302683",
    "expires_on":"1493466951",
    "not_before":"1493423168",
    "resource":"https://graph.windows.net",
    "access_token":"eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6InowMzl6ZHNGdWl6cEJmQlZLMVRuMjVRSFlPMCIsImtpZCI6InowMzl6ZHNGdWl6cEJmQlZLMVRuMjVRSFlPMCJ9.eyJhdWQiOiJodHRwczovL2dyYXBoLndpbmRvd3MubmV0IiwiaXNzIjoiaHR0cHM6Ly9zdHMud2luZG93cy5uZXQvMjYwMzljY2UtNDg5ZC00MDAyLTgyOTMtNWIwYzUxMzRlYWNiLyIsImlhdCI6MTQ5MzQyMzE2OCwibmJmIjoxNDkzNDIzMTY4LCJleHAiOjE0OTM0NjY5NTEsImFjciI6IjEiLCJhaW8iOiJBU1FBMi84REFBQUE1NnZGVmp0WlNjNWdBVWwrY1Z0VFpyM0VvV2NvZEoveWV1S2ZqcTZRdC9NPSIsImFtciI6WyJwd2QiXSwiYXBwaWQiOiI2MjUzOTFhZi1jNjc1LTQzZTUtOGU0NC1lZGQzZTMwY2ViMTUiLCJhcHBpZGFjciI6IjEiLCJlX2V4cCI6MzAyNjgzLCJmYW1pbHlfbmFtZSI6IlRlc3QiLCJnaXZlbl9uYW1lIjoiTmF2eWEiLCJpcGFkZHIiOiIxNjcuMjIwLjEuMTc3IiwibmFtZSI6Ik5hdnlhIFRlc3QiLCJvaWQiOiIxY2Q0YmNhYy1iODA4LTQyM2EtOWUyZi04MjdmYmIxYmI3MzkiLCJwbGF0ZiI6IjMiLCJwdWlkIjoiMTAwMzNGRkZBMTJFRDdGRSIsInNjcCI6IlVzZXIuUmVhZCIsInN1YiI6IjNKTUlaSWJlYTc1R2hfWHdDN2ZzX0JDc3kxa1l1ekZKLTUyVm1Zd0JuM3ciLCJ0aWQiOiIyNjAzOWNjZS00ODlkLTQwMDItODI5My01YjBjNTEzNGVhY2IiLCJ1bmlxdWVfbmFtZSI6Im5hdnlhQGRkb2JhbGlhbm91dGxvb2sub25taWNyb3NvZnQuY29tIiwidXBuIjoibmF2eWFAZGRvYmFsaWFub3V0bG9vay5vbm1pY3Jvc29mdC5jb20iLCJ1dGkiOiJ4Q3dmemhhLVAwV0pRT0x4Q0dnS0FBIiwidmVyIjoiMS4wIn0.cqmUVjfVbqWsxJLUI1Z4FRx1mNQAHP-L0F4EMN09r8FY9bIKeO-0q1eTdP11Nkj_k4BmtaZsTcK_mUygdMqEp9AfyVyA1HYvokcgGCW_Z6DMlVGqlIU4ssEkL9abgl1REHElPhpwBFFBBenOk9iHddD1GddTn6vJbKC3qAaNM5VarjSPu50bVvCrqKNvFixTb5bbdnSz-Qr6n6ACiEimiI1aNOPR2DeKUyWBPaQcU5EAK0ef5IsVJC1yaYDlAcUYIILMDLCD9ebjsy0t9pj_7lvjzUSrbMdSCCdzCqez_MSNxrk1Nu9AecugkBYp3UVUZOIyythVrj6-sVvLZKUutQ",
    "refresh_token":"AQABAAAAAABnfiG-mA6NTae7CdWW7QfdjKGu9-t1scy_TDEmLi4eLQMjJGt_nAoVu6A4oSu1KsRiz8XyQIPKQxSGfbf2FoSK-hm2K8TYzbJuswYusQpJaHUQnSqEvdaCeFuqXHBv84wjFhuanzF9dQZB_Ng5za9xKlUENrNtlq9XuLNVKzxEyeUM7JyxzdY7JiEphWImwgOYf6II316d0Z6-H3oYsFezf4Xsjz-MOBYEov0P64UaB5nJMvDyApV-NWpgklLASfNoSPGb67Bc02aFRZrm4kLk-xTl6eKE6hSo0XU2z2t70stFJDxvNQobnvNHrAmBaHWPAcC3FGwFnBOojpZB2tzG1gLEbmdROVDp8kHEYAwnRK947Py12fJNKExUdN0njmXrKxNZ_fEM33LHW1Tf4kMX_GvNmbWHtBnIyG0w5emb-b54ef5AwV5_tGUeivTCCysgucEc-S7G8Cz0xNJ_BOiM_4bAv9iFmrm9STkltpz0-Tftg8WKmaJiC0xXj6uTf4ZkX79mJJIuuM7XP4ARIcLpkktyg2Iym9jcZqymRkGH2Rm9sxBwC4eeZXM7M5a7TJ-5CqOdfuE3sBPq40RdEWMFLcrAzFvP0VDR8NKHIrPR1AcUruat9DETmTNJukdlJN3O41nWdZOVoJM-uKN3uz2wQ2Ld1z0Mb9_6YfMox9KTJNzRzcL52r4V_y3kB6ekaOZ9wQ3HxGBQ4zFt-2U0mSszIAA",
    "id_token":"eyJ0eXAiOiJKV1QiLCJhbGciOiJub25lIn0.eyJhdWQiOiI2MjUzOTFhZi1jNjc1LTQzZTUtOGU0NC1lZGQzZTMwY2ViMTUiLCJpc3MiOiJodHRwczovL3N0cy53aW5kb3dzLm5ldC8yNjAzOWNjZS00ODlkLTQwMDItODI5My01YjBjNTEzNGVhY2IvIiwiaWF0IjoxNDkzNDIzMTY4LCJuYmYiOjE0OTM0MjMxNjgsImV4cCI6MTQ5MzQ2Njk1MSwiYW1yIjpbInB3ZCJdLCJmYW1pbHlfbmFtZSI6IlRlc3QiLCJnaXZlbl9uYW1lIjoiTmF2eWEiLCJpcGFkZHIiOiIxNjcuMjIwLjEuMTc3IiwibmFtZSI6Ik5hdnlhIFRlc3QiLCJvaWQiOiIxY2Q0YmNhYy1iODA4LTQyM2EtOWUyZi04MjdmYmIxYmI3MzkiLCJwbGF0ZiI6IjMiLCJzdWIiOiJEVXpYbkdKMDJIUk0zRW5pbDFxdjZCakxTNUllQy0tQ2ZpbzRxS1MzNEc4IiwidGlkIjoiMjYwMzljY2UtNDg5ZC00MDAyLTgyOTMtNWIwYzUxMzRlYWNiIiwidW5pcXVlX25hbWUiOiJuYXZ5YUBkZG9iYWxpYW5vdXRsb29rLm9ubWljcm9zb2Z0LmNvbSIsInVwbiI6Im5hdnlhQGRkb2JhbGlhbm91dGxvb2sub25taWNyb3NvZnQuY29tIiwidXRpIjoieEN3ZnpoYS1QMFdKUU9MeENHZ0tBQSIsInZlciI6IjEuMCJ9."
}
```

### 錯誤回應範例
錯誤回應會傳回 Azure AD 權杖端點時，嘗試 tooacquire 存取權杖的 hello 下游應用程式開發介面，如果 hello 下游應用程式開發介面具有條件式存取原則，例如設於其上的多因素驗證。 hello 中介層服務應該出現此錯誤 toohello 用戶端應用程式以便 hello 用戶端應用程式可以提供 hello 使用者互動 toosatisfy hello 條件式存取原則。

```
{
    "error":"interaction_required",
    "error_description":"AADSTS50079: Due tooa configuration change made by your administrator, or because you moved tooa new location, you must enroll in multi-factor authentication tooaccess 'bf8d80f9-9098-4972-b203-500f535113b1'.\r\nTrace ID: b72a68c3-0926-4b8e-bc35-3150069c2800\r\nCorrelation ID: 73d656cf-54b1-4eb2-b429-26d8165a52d7\r\nTimestamp: 2017-05-01 22:43:20Z",
    "error_codes":[50079],
    "timestamp":"2017-05-01 22:43:20Z",
    "trace_id":"b72a68c3-0926-4b8e-bc35-3150069c2800",
    "correlation_id":"73d656cf-54b1-4eb2-b429-26d8165a52d7",
    "claims":"{\"access_token\":{\"polids\":{\"essential\":true,\"values\":[\"9ab03e19-ed42-4168-b6b7-7001fb3e933a\"]}}}"
}
```

## 使用 hello 保護資源的存取語彙基元 tooaccess hello
現在 hello 中介層服務可以使用 hello 驗證權杖取得上述 toomake 要求 toohello 下游 web API 中，設定 hello 語彙基元所 hello`Authorization`標頭。

### 範例
```
GET /me?api-version=2013-11-08 HTTP/1.1
Host: graph.windows.net
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6InowMzl6ZHNGdWl6cEJmQlZLMVRuMjVRSFlPMCIsImtpZCI6InowMzl6ZHNGdWl6cEJmQlZLMVRuMjVRSFlPMCJ9.eyJhdWQiOiJodHRwczovL2dyYXBoLndpbmRvd3MubmV0IiwiaXNzIjoiaHR0cHM6Ly9zdHMud2luZG93cy5uZXQvMjYwMzljY2UtNDg5ZC00MDAyLTgyOTMtNWIwYzUxMzRlYWNiLyIsImlhdCI6MTQ5MzQyMzE2OCwibmJmIjoxNDkzNDIzMTY4LCJleHAiOjE0OTM0NjY5NTEsImFjciI6IjEiLCJhaW8iOiJBU1FBMi84REFBQUE1NnZGVmp0WlNjNWdBVWwrY1Z0VFpyM0VvV2NvZEoveWV1S2ZqcTZRdC9NPSIsImFtciI6WyJwd2QiXSwiYXBwaWQiOiI2MjUzOTFhZi1jNjc1LTQzZTUtOGU0NC1lZGQzZTMwY2ViMTUiLCJhcHBpZGFjciI6IjEiLCJlX2V4cCI6MzAyNjgzLCJmYW1pbHlfbmFtZSI6IlRlc3QiLCJnaXZlbl9uYW1lIjoiTmF2eWEiLCJpcGFkZHIiOiIxNjcuMjIwLjEuMTc3IiwibmFtZSI6Ik5hdnlhIFRlc3QiLCJvaWQiOiIxY2Q0YmNhYy1iODA4LTQyM2EtOWUyZi04MjdmYmIxYmI3MzkiLCJwbGF0ZiI6IjMiLCJwdWlkIjoiMTAwMzNGRkZBMTJFRDdGRSIsInNjcCI6IlVzZXIuUmVhZCIsInN1YiI6IjNKTUlaSWJlYTc1R2hfWHdDN2ZzX0JDc3kxa1l1ekZKLTUyVm1Zd0JuM3ciLCJ0aWQiOiIyNjAzOWNjZS00ODlkLTQwMDItODI5My01YjBjNTEzNGVhY2IiLCJ1bmlxdWVfbmFtZSI6Im5hdnlhQGRkb2JhbGlhbm91dGxvb2sub25taWNyb3NvZnQuY29tIiwidXBuIjoibmF2eWFAZGRvYmFsaWFub3V0bG9vay5vbm1pY3Jvc29mdC5jb20iLCJ1dGkiOiJ4Q3dmemhhLVAwV0pRT0x4Q0dnS0FBIiwidmVyIjoiMS4wIn0.cqmUVjfVbqWsxJLUI1Z4FRx1mNQAHP-L0F4EMN09r8FY9bIKeO-0q1eTdP11Nkj_k4BmtaZsTcK_mUygdMqEp9AfyVyA1HYvokcgGCW_Z6DMlVGqlIU4ssEkL9abgl1REHElPhpwBFFBBenOk9iHddD1GddTn6vJbKC3qAaNM5VarjSPu50bVvCrqKNvFixTb5bbdnSz-Qr6n6ACiEimiI1aNOPR2DeKUyWBPaQcU5EAK0ef5IsVJC1yaYDlAcUYIILMDLCD9ebjsy0t9pj_7lvjzUSrbMdSCCdzCqez_MSNxrk1Nu9AecugkBYp3UVUZOIyythVrj6-sVvLZKUutQ
```

## 後續步驟
深入了解 hello OAuth 2.0 通訊協定和另一個方式 tooperform 服務 tooservice 驗證使用用戶端認證。
* [使用 Azure ad 的 OAuth 2.0 用戶端認證授與服務 tooservice 驗證](active-directory-protocols-oauth-service-to-service.md)
* [Azure AD 中的 OAuth 2.0](active-directory-protocols-oauth-code.md)
