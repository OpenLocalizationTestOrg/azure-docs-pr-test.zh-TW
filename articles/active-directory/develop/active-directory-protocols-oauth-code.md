---
title: "aaaUnderstand hello Azure ad 的 OAuth 2.0 授權碼流程 |Microsoft 文件"
description: "本文說明如何 toouse HTTP 訊息 tooauthorize 存取 tooweb 應用程式和 web 應用程式開發介面使用 Azure Active Directory 和 OAuth 2.0 的租用戶中。"
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: de3412cb-5fde-4eca-903a-4e9c74db68f2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/08/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 4a6fe67d786a5fcb87d1059c2e94ba0c88d26cd3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# 授權存取 tooweb 應用程式使用 OAuth 2.0 和 Azure Active Directory
Azure Active Directory (Azure AD) 會使用 OAuth 2.0 tooenable 您 tooauthorize 存取 tooweb 應用程式與 Azure AD 租用戶中的 web Api。 本指南是與語言無關，並說明如何 toosend 和接收 HTTP 訊息，而不使用任何我們開放原始碼程式庫。

hello OAuth 2.0 授權碼流程述[區段 hello OAuth 2.0 規格的 4.1](https://tools.ietf.org/html/rfc6749#section-4.1)。 它是使用的 tooperform 驗證和授權的大部分的應用程式類型，包括 web 應用程式和原生安裝的應用程式。

[!INCLUDE [active-directory-protocols-getting-started](../../../includes/active-directory-protocols-getting-started.md)]

## OAuth 2.0 授權流程
在高層級，應用程式的 hello 整個授權流程有點外觀如下：

![OAuth 授權碼流程](media/active-directory-protocols-oauth-code/active-directory-oauth-code-flow-native-app.png)

## 要求授權碼
hello 授權碼流程的開頭 hello 用戶端導向 hello 使用者 toohello`/authorize`端點。 在要求中，hello 用戶端指出它需要從 hello 使用者 tooacquire hello 權限。 您可以從 Azure 傳統入口網站中的應用程式頁面中 hello 取得 hello OAuth 2.0 端點**檢視端點**抽屜 hello 底部的按鈕。

```
// Line breaks for legibility only

https://login.microsoftonline.com/{tenant}/oauth2/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&response_type=code
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&response_mode=query
&resource=https%3A%2F%2Fservice.contoso.com%2F
&state=12345
```

| 參數 |  | 說明 |
| --- | --- | --- |
| tenant |必要 |hello `{tenant}` hello hello 要求路徑中的值可以是使用的 toocontrol 可以登入 hello 應用程式。  hello 允許的值為租用戶識別碼，例如`8eaef023-2b34-4da1-9baa-8bc8c9d6a490`或`contoso.onmicrosoft.com`或`common`租用戶獨立語彙基元 |
| client_id |必要 |hello 應用程式識別碼指派的 tooyour 應用程式時向 Azure AD 註冊。 您可以將它找到 hello Azure 入口網站中。 按一下**Active Directory**，按一下 hello 目錄、 選擇 hello 應用程式，然後按**設定** |
| response_type |必要 |必須包含`code`的 hello 授權碼流程。 |
| redirect_uri |建議使用 |hello redirect_uri 應用程式，可以傳送及接收您的應用程式驗證回應。  它必須完全符合其中一個 hello redirect_uris 您註冊 hello 入口網站，但它必須是 url 編碼。  原生和行動應用程式，您應該使用 hello 預設值是`urn:ietf:wg:oauth:2.0:oob`。 |
| response_mode |建議使用 |指定應該使用的 toosend hello 產生語彙基元後 tooyour 應用程式的 hello 方法。  可以是 `query` 或 `form_post`。 |
| state |建議使用 |也會傳回 hello 權杖回應中的 hello 要求中包含一個值。 隨機產生的唯一值通常用於 [防止跨站台偽造要求攻擊](http://tools.ietf.org/html/rfc6749#section-10.12)。  之前發生 hello 驗證要求，例如 hello 頁面或檢視上 hello 狀態也會使用的 tooencode hello 應用程式中的 hello 使用者狀態資訊。 |
| resource |選用 |hello hello web API （受保護的資源） 應用程式識別碼 URI。 按一下 toofind hello hello Azure 入口網站中的 hello web API，應用程式識別碼 URI **Active Directory**、 按一下 hello 目錄，按一下 hello 應用程式，然後按一下**設定**。 |
| prompt |選用 |表示 hello 類型所需使用者互動。<p> 有效值為： <p> *登入*: hello 使用者應該提示的 tooreauthenticate。 <p> *同意*： 使用者同意已被授與，但其必須 toobe 更新。 hello 使用者應該提示的 tooconsent。 <p> *admin_consent*： 系統管理員應該是代表其組織中的所有使用者的提示的 tooconsent |
| login_hint |選用 |如果您知道事先其使用者名稱，可能會使用的 toopre 填滿 hello 使用者名稱/電子郵件地址欄位 hello 登入頁面的 hello 使用者。  通常應用程式使用此參數在重新驗證，從先前的登入需要擷取 hello 使用者名稱時使用 hello`preferred_username`宣告。 |
| domain_hint |選用 |提供有關在 hello 租用戶或網域的 hello 使用者應該使用 toosign 中。 hello domain_hint hello 值為 hello 租用戶的已註冊的網域。 如果 hello 租用戶同盟的 tooan 在內部部署目錄，AAD 重新導向 toohello 指定的租用戶同盟伺服器。 |

> [!NOTE]
> 如果組織中的 hello 使用者，hello 組織的系統管理員可以同意或代表 hello 使用者，拒絕或允許 hello 使用者 tooconsent。 hello 使用者 hello 管理員的許可之下時，才可以 hello 選項 tooconsent。
>
>

此時，hello 會要求使用者 tooenter 他們的認證和同意 toohello 權限所示 hello`scope`查詢參數。 一旦 hello 使用者驗證，並授與同意，Azure AD 會傳送回應 tooyour 應用程式在 hello`redirect_uri`在要求中的位址。

### 成功回應
成功的回應看起來可能像這樣︰

```
GET  HTTP/1.1 302 Found
Location: http://localhost/myapp/?code= AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrqqf_ZT_p5uEAEJJ_nZ3UmphWygRNy2C3jJ239gV_DBnZ2syeg95Ki-374WHUP-i3yIhv5i-7KU2CEoPXwURQp6IVYMw-DjAOzn7C3JCu5wpngXmbZKtJdWmiBzHpcO2aICJPu1KvJrDLDP20chJBXzVYJtkfjviLNNW7l7Y3ydcHDsBRKZc3GuMQanmcghXPyoDg41g8XbwPudVh7uCmUponBQpIhbuffFP_tbV8SNzsPoFz9CLpBCZagJVXeqWoYMPe2dSsPiLO9Alf_YIe5zpi-zY4C3aLw5g9at35eZTfNd0gBRpR5ojkMIcZZ6IgAA&session_state=7B29111D-C220-4263-99AB-6F6E135D75EF&state=D79E5777-702E-4260-9A62-37F75FF22CCE
```

| 參數 | 說明 |
| --- | --- |
| admin_consent |hello 值為 True，如果系統管理員同意 tooa 同意要求提示表示同意。 |
| code |hello hello 應用程式要求授權碼。 hello 應用程式可以使用 hello 目標資源的 hello 授權程式碼 toorequest 存取權杖。 |
| session_state |可識別 hello 目前使用者工作階段的唯一值。 這個值是 GUID，但應視為不檢查即傳遞的不透明值。 |
| state |如果在 hello 要求中，相同的值應該會出現在 hello 回應 hello 包含狀態參數。 它是 hello 要求和回應中的 hello 狀態值完全相同，才能使用 hello 回應 hello 應用程式 tooverify 的好作法。 這有助於 toodetect[跨網站要求偽造 (CSRF) 攻擊](https://tools.ietf.org/html/rfc6749#section-10.12)對 hello 用戶端。 |

### 錯誤回應
錯誤回應也可能會傳送 toohello `redirect_uri` ，好讓 hello 應用程式可以適當地處理。

```
GET http://localhost:12345/?
error=access_denied
&error_description=the+user+canceled+the+authentication
```

| 參數 | 說明 |
| --- | --- |
| 錯誤 |Hello 的區段 5.2 中定義的錯誤碼值[OAuth 2.0 授權架構](http://tools.ietf.org/html/rfc6749)。 hello 下表描述 hello Azure AD 會傳回錯誤碼。 |
| error_description |Hello 錯誤的更詳細的描述。 此訊息不是 toobe 方便使用者讀取為主。 |
| state |hello 狀態值是隨機產生的非重複使用值為 hello 要求中傳送，並傳回在 hello 回應 tooprevent 跨網站要求偽造 (CSRF) 攻擊。 |

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

## 使用 hello 授權程式碼 toorequest 存取權杖
現在，您已取得授權碼，並已被授與權限 hello 使用者，您可以藉由傳送 POST 要求 toohello 兌換 hello 程式碼存取預期的語彙基元 toohello 資源`/token`端點：

```
// Line breaks for legibility only

POST /{tenant}/oauth2/token HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded
grant_type=authorization_code
&client_id=2d4d11a2-f814-46a7-890a-274a72a7309e
&code=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrqqf_ZT_p5uEAEJJ_nZ3UmphWygRNy2C3jJ239gV_DBnZ2syeg95Ki-374WHUP-i3yIhv5i-7KU2CEoPXwURQp6IVYMw-DjAOzn7C3JCu5wpngXmbZKtJdWmiBzHpcO2aICJPu1KvJrDLDP20chJBXzVYJtkfjviLNNW7l7Y3ydcHDsBRKZc3GuMQanmcghXPyoDg41g8XbwPudVh7uCmUponBQpIhbuffFP_tbV8SNzsPoFz9CLpBCZagJVXeqWoYMPe2dSsPiLO9Alf_YIe5zpi-zY4C3aLw5g9at35eZTfNd0gBRpR5ojkMIcZZ6IgAA
&redirect_uri=https%3A%2F%2Flocalhost%2Fmyapp%2F
&resource=https%3A%2F%2Fservice.contoso.com%2F
&client_secret=p@ssw0rd

//NOTE: client_secret only required for web apps
```

| 參數 |  | 說明 |
| --- | --- | --- |
| tenant |必要 |hello `{tenant}` hello hello 要求路徑中的值可以是使用的 toocontrol 可以登入 hello 應用程式。  hello 允許的值為租用戶識別碼，例如`8eaef023-2b34-4da1-9baa-8bc8c9d6a490`或`contoso.onmicrosoft.com`或`common`租用戶獨立語彙基元 |
| client_id |必要 |hello 應用程式識別碼指派的 tooyour 應用程式時向 Azure AD 註冊。 您可以將它找到 hello Azure 傳統入口網站中。 按一下**Active Directory**，按一下 hello 目錄、 選擇 hello 應用程式，然後按**設定** |
| grant_type |必要 |必須是`authorization_code`的 hello 授權碼流程。 |
| code |必要 |hello`authorization_code`貴用戶取得 hello 前一節中， |
| redirect_uri |必要 |hello 相同`redirect_uri`值，已使用的 tooacquire hello `authorization_code`。 |
| client_secret |Web Apps 所需 |您已在 hello 應用程式註冊入口網站應用程式的 hello 應用程式密碼。  其不應用於原生應用程式，因為裝置無法穩當地儲存 client_secret。  它是必要的 web 應用程式和 web Api，其具有 hello 能力 toostore hello `client_secret` hello 伺服器端上安全的方式。 |
| resource |如果在授權碼要求中指定，則為必要，否則為選擇性 |hello hello web API （受保護的資源） 應用程式識別碼 URI。 |

toofind hello 應用程式識別碼 URI，在 hello Azure 管理入口網站中，按一下**Active Directory**、 按一下 hello 目錄、 按一下 hello 應用程式，然後按一下**設定**。

### 成功回應
Azure AD 在成功回應時會傳回存取權杖。 toominimize 網路呼叫 hello 用戶端應用程式和與其相關的延遲、 hello 用戶端應用程式應該快取存取權杖 hello OAuth 2.0 回應中指定的 hello 權杖存留期。 toodetermine hello 權杖存留期，使用任一 hello`expires_in`或`expires_on`參數值。

如果 web API 資源傳回`invalid_token`錯誤程式碼，這可能表示 hello 資源已判定該 hello token 已過期。 如果 hello 用戶端和資源的時鐘時間不同 （稱為 「 時間偏差 」），hello 資源可能會考慮 hello 語彙基元 toobe hello 語彙基元都會從 hello 用戶端快取前就已過期。 如果發生這種情況，清除 hello 語彙基元從 hello 快取，即使它是仍在其計算的存留期內。

成功的回應看起來可能像這樣︰

```
{
  "access_token": " eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1THdqcHdBSk9NOW4tQSJ9.eyJhdWQiOiJodHRwczovL3NlcnZpY2UuY29udG9zby5jb20vIiwiaXNzIjoiaHR0cHM6Ly9zdHMud2luZG93cy5uZXQvN2ZlODE0NDctZGE1Ny00Mzg1LWJlY2ItNmRlNTdmMjE0NzdlLyIsImlhdCI6MTM4ODQ0MDg2MywibmJmIjoxMzg4NDQwODYzLCJleHAiOjEzODg0NDQ3NjMsInZlciI6IjEuMCIsInRpZCI6IjdmZTgxNDQ3LWRhNTctNDM4NS1iZWNiLTZkZTU3ZjIxNDc3ZSIsIm9pZCI6IjY4Mzg5YWUyLTYyZmEtNGIxOC05MWZlLTUzZGQxMDlkNzRmNSIsInVwbiI6ImZyYW5rbUBjb250b3NvLmNvbSIsInVuaXF1ZV9uYW1lIjoiZnJhbmttQGNvbnRvc28uY29tIiwic3ViIjoiZGVOcUlqOUlPRTlQV0pXYkhzZnRYdDJFYWJQVmwwQ2o4UUFtZWZSTFY5OCIsImZhbWlseV9uYW1lIjoiTWlsbGVyIiwiZ2l2ZW5fbmFtZSI6IkZyYW5rIiwiYXBwaWQiOiIyZDRkMTFhMi1mODE0LTQ2YTctODkwYS0yNzRhNzJhNzMwOWUiLCJhcHBpZGFjciI6IjAiLCJzY3AiOiJ1c2VyX2ltcGVyc29uYXRpb24iLCJhY3IiOiIxIn0.JZw8jC0gptZxVC-7l5sFkdnJgP3_tRjeQEPgUn28XctVe3QqmheLZw7QVZDPCyGycDWBaqy7FLpSekET_BftDkewRhyHk9FW_KeEz0ch2c3i08NGNDbr6XYGVayNuSesYk5Aw_p3ICRlUV1bqEwk-Jkzs9EEkQg4hbefqJS6yS1HoV_2EsEhpd_wCQpxK89WPs3hLYZETRJtG5kvCCEOvSHXmDE6eTHGTnEgsIk--UlPe275Dvou4gEAwLofhLDQbMSjnlV5VLsjimNBVcSRFShoxmQwBJR_b2011Y5IuD6St5zPnzruBbZYkGNurQK63TJPWmRd3mbJsGM0mf3CUQ",
  "token_type": "Bearer",
  "expires_in": "3600",
  "expires_on": "1388444763",
  "resource": "https://service.contoso.com/",
  "refresh_token": "AwABAAAAvPM1KaPlrEqdFSBzjqfTGAMxZGUTdM0t4B4rTfgV29ghDOHRc2B-C_hHeJaJICqjZ3mY2b_YNqmf9SoAylD1PycGCB90xzZeEDg6oBzOIPfYsbDWNf621pKo2Q3GGTHYlmNfwoc-OlrxK69hkha2CF12azM_NYhgO668yfcUl4VBbiSHZyd1NVZG5QTIOcbObu3qnLutbpadZGAxqjIbMkQ2bQS09fTrjMBtDE3D6kSMIodpCecoANon9b0LATkpitimVCrl-NyfN3oyG4ZCWu18M9-vEou4Sq-1oMDzExgAf61noxzkNiaTecM-Ve5cq6wHqYQjfV9DOz4lbceuYCAA",
  "scope": "https%3A%2F%2Fgraph.microsoft.com%2Fmail.read",
  "id_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJub25lIn0.eyJhdWQiOiIyZDRkMTFhMi1mODE0LTQ2YTctODkwYS0yNzRhNzJhNzMwOWUiLCJpc3MiOiJodHRwczovL3N0cy53aW5kb3dzLm5ldC83ZmU4MTQ0Ny1kYTU3LTQzODUtYmVjYi02ZGU1N2YyMTQ3N2UvIiwiaWF0IjoxMzg4NDQwODYzLCJuYmYiOjEzODg0NDA4NjMsImV4cCI6MTM4ODQ0NDc2MywidmVyIjoiMS4wIiwidGlkIjoiN2ZlODE0NDctZGE1Ny00Mzg1LWJlY2ItNmRlNTdmMjE0NzdlIiwib2lkIjoiNjgzODlhZTItNjJmYS00YjE4LTkxZmUtNTNkZDEwOWQ3NGY1IiwidXBuIjoiZnJhbmttQGNvbnRvc28uY29tIiwidW5pcXVlX25hbWUiOiJmcmFua21AY29udG9zby5jb20iLCJzdWIiOiJKV3ZZZENXUGhobHBTMVpzZjd5WVV4U2hVd3RVbTV5elBtd18talgzZkhZIiwiZmFtaWx5X25hbWUiOiJNaWxsZXIiLCJnaXZlbl9uYW1lIjoiRnJhbmsifQ."
}

```

| 參數 | 說明 |
| --- | --- |
| access_token |hello 要求的存取權杖。 hello 應用程式可以使用這個受保護資源，例如 web API 的語彙基元 tooauthenticate toohello。 |
| token_type |表示 hello 語彙基元型別值。 hello 只能輸入 Azure AD 支援的承載。 如需持有人權杖的詳細資訊，請參閱 [OAuth2.0 授權架構︰持有人權杖用法 (RFC 6750)](http://www.rfc-editor.org/rfc/rfc6750.txt) |
| expires_in |多久 hello 存取權杖是有效 （以秒為單位）。 |
| expires_on |hello hello 存取權杖到期的時間。 hello 日期以 hello 的秒數表示從 1970年-01-01T0:0:0Z UTC 直到 hello 到期時間。 這個值是使用的 toodetermine hello 存留期，快取權杖。 |
| resource |hello hello web API （受保護的資源） 應用程式識別碼 URI。 |
| scope |模擬權限授與 toohello 用戶端應用程式。 hello 預設權限是`user_impersonation`。 hello 的 hello 保護資源的擁有者可以在 Azure AD 中註冊其他的值。 |
| refresh_token |OAuth 2.0 重新整理權杖。 hello 目前存取權杖到期後，hello 應用程式可以使用這個語彙基元 tooacquire 其他存取權杖。  重新整理權杖存留較久，而且可以使用的 tooretain 存取 tooresources 很長的時間。 |
| id_token |不帶正負號的 JSON Web Token (JWT)。 hello 應用程式可以 base64Url 解碼 hello hello 使用者登入此語彙基元 toorequest 資訊區段。 hello 應用程式可以快取 hello 值，並顯示它們，但它不應依賴它們的任何授權或安全性界限。 |

### JWT 權杖宣告
hello JWT 權杖中的 hello hello 值`id_token`參數可以解碼為下列宣告 hello:

```
{
 "typ": "JWT",
 "alg": "none"
}.
{
 "aud": "2d4d11a2-f814-46a7-890a-274a72a7309e",
 "iss": "https://sts.windows.net/7fe81447-da57-4385-becb-6de57f21477e/",
 "iat": 1388440863,
 "nbf": 1388440863,
 "exp": 1388444763,
 "ver": "1.0",
 "tid": "7fe81447-da57-4385-becb-6de57f21477e",
 "oid": "68389ae2-62fa-4b18-91fe-53dd109d74f5",
 "upn": "frank@contoso.com",
 "unique_name": "frank@contoso.com",
 "sub": "JWvYdCWPhhlpS1Zsf7yYUxShUwtUm5yzPmw_-jX3fHY",
 "family_name": "Miller",
 "given_name": "Frank"
}.
```

如需有關 JSON web 權杖的詳細資訊，請參閱 hello [JWT IETF 草稿規格](http://go.microsoft.com/fwlink/?LinkId=392344)。 如需有關 hello 語彙基元類型及宣告的詳細資訊，請閱讀[支援權杖和宣告類型](active-directory-token-and-claims.md)

hello`id_token`參數包含下列宣告類型的 hello:

| 宣告類型 | 說明 |
| --- | --- |
| aud |Hello 語彙基元的對象。 Hello 觀眾 hello 語彙基元簽發 tooa 用戶端應用程式時，為 hello `client_id` hello 用戶端。 |
| exp |到期時間。 hello hello 權杖到期的時間。 Hello 語彙基元 toobe 有效，hello 目前日期/時間必須小於或等於 toohello`exp`值。 hello 次會表示秒數 hello 從 1970 年 1 月 1 日 (1970年-01-01T0:0:0Z) UTC 直到 hello 時間 hello 權杖的發出。 |
| family_name |使用者的姓氏。 hello 應用程式可以顯示此值。 |
| given_name |使用者的名字。 hello 應用程式可以顯示此值。 |
| iat |發出時間。 hello hello JWT 時所發出的時間。 hello 次會表示秒數 hello 從 1970 年 1 月 1 日 (1970年-01-01T0:0:0Z) UTC 直到 hello 時間 hello 權杖的發出。 |
| iss |識別 hello 權杖簽發者 |
| nbf |生效時間。 hello hello 權杖生效的時間。 針對 hello 語彙基元 toobe 有效，hello 目前日期/時間必須大於或等於 toohello Nbf 值。 hello 次會表示秒數 hello 從 1970 年 1 月 1 日 (1970年-01-01T0:0:0Z) UTC 直到 hello 時間 hello 權杖的發出。 |
| oid |在 Azure AD 中的 hello 使用者物件的物件識別碼 (ID)。 |
| sub |權杖主旨識別碼。 這是 hello 語彙基元的 hello 使用者描述持續性不變的識別碼。 請在快取邏輯中使用此值。 |
| tid |租用戶的權杖 hello hello Azure AD 租用戶識別碼 (ID)。 |
| unique_name |唯一識別碼，可以顯示的 toohello 使用者。 這通常是使用者主體名稱 (UPN)。 |
| upn |Hello 使用者的使用者主體名稱。 |
| ver |版本。 hello hello JWT 權杖中，通常為 1.0 版。 |

### 錯誤回應
hello 權杖發行端點錯誤會 HTTP 錯誤碼，，因為 hello 用戶端呼叫直接 hello 權杖發行端點。 此外 toohello HTTP 狀態碼，hello Azure AD 權杖發行端點也會傳回 JSON 文件，以描述 hello 錯誤的物件。

範例錯誤回應看起來可能像這樣︰

```
{
  "error": "invalid_grant",
  "error_description": "AADSTS70002: Error validating credentials. AADSTS70008: hello provided authorization code or refresh token is expired. Send a new interactive authorization request for this user and resource.\r\nTrace ID: 3939d04c-d7ba-42bf-9cb7-1e5854cdce9e\r\nCorrelation ID: a8125194-2dc8-4078-90ba-7b6592a7f231\r\nTimestamp: 2016-04-11 18:00:12Z",
  "error_codes": [
    70002,
    70008
  ],
  "timestamp": "2016-04-11 18:00:12Z",
  "trace_id": "3939d04c-d7ba-42bf-9cb7-1e5854cdce9e",
  "correlation_id": "a8125194-2dc8-4078-90ba-7b6592a7f231"
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

#### HTTP 狀態碼
hello 下表列出 hello 權杖發行端點傳回的 hello HTTP 狀態碼。 在某些情況下，hello 錯誤碼足夠 toodescribe hello 回應，但如果沒有錯誤，您需要 tooparse hello 隨附的 JSON 文件，並檢查其錯誤碼。

| HTTP 代碼 | 說明 |
| --- | --- |
| 400 |預設的 HTTP 代碼。 在大部分情況下使用，且通常是因為 tooa 格式不正確的要求。 修正，然後再重新送出 hello 要求。 |
| 401 |驗證失敗。 例如，hello 要求缺少 hello client_secret 參數。 |
| 403 |授權失敗。 例如，hello 使用者沒有權限 tooaccess hello 資源。 |
| 500 |在 hello 服務發生內部錯誤。 重試 hello 要求。 |

#### 權杖端點錯誤的錯誤碼
| 錯誤碼 | 說明 | 用戶端動作 |
| --- | --- | --- |
| invalid_request |通訊協定錯誤，例如遺漏必要的參數。 |修正，然後再重新送出 hello 要求 |
| invalid_grant |hello 授權碼無效，或已過期。 |再試一次新的要求 toohello`/authorize`端點 |
| unauthorized_client |hello 驗證的用戶端未獲得授權 toouse 此授權授與類型。 |這通常就會發生 hello 用戶端應用程式未在 Azure AD 中註冊，或未加入 toohello 使用者的 Azure AD 租用戶。 hello 應用程式可以提示指示安裝 hello 應用程式，並將它加入 tooAzure AD hello 的使用者。 |
| invalid_client |用戶端驗證失敗。 |找不到有效的 hello 用戶端認證。 toofix，hello 應用程式系統管理員更新 hello 認證。 |
| unsupported_grant_type |hello 授權伺服器不支援 hello 授權授與類型。 |變更 hello 授與 hello 要求中的型別。 這種類型的錯誤應該只會在開發期間發生，並且會在初始測試期間偵測出來。 |
| invalid_resource |hello 目標資源無效，因為它不存在、 Azure AD 無法找到它，或是未正確設定。 |這表示 hello 資源存在，是否尚未設定 hello 租用戶中。 hello 應用程式可以提示指示安裝 hello 應用程式，並將它加入 tooAzure AD hello 的使用者。 |
| interaction_required |hello 要求需要使用者互動。 例如，必須進行其他驗證步驟。 | 而不是非互動式要求，再試一次 hello 的互動式授權要求相同資源。 |
| temporarily_unavailable |hello 伺服器就會暫時太忙碌 toohandle hello 要求。 |重試 hello 要求。 hello 用戶端應用程式可能會詳述 toohello 使用者其回應，因為 tooa 暫時性狀況而延遲。 |

## 使用 hello 存取語彙基元 tooaccess hello 資源
既然您已成功取得`access_token`，您可以使用 hello 語彙基元要求 tooWeb Api 中併入 hello`Authorization`標頭。 hello [RFC 6750](http://www.rfc-editor.org/rfc/rfc6750.txt)規格說明如何在 HTTP 要求 tooaccess toouse 持有者權杖受保護資源。

### 範例要求
```
GET /data HTTP/1.1
Host: service.contoso.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1THdqcHdBSk9NOW4tQSJ9.eyJhdWQiOiJodHRwczovL3NlcnZpY2UuY29udG9zby5jb20vIiwiaXNzIjoiaHR0cHM6Ly9zdHMud2luZG93cy5uZXQvN2ZlODE0NDctZGE1Ny00Mzg1LWJlY2ItNmRlNTdmMjE0NzdlLyIsImlhdCI6MTM4ODQ0MDg2MywibmJmIjoxMzg4NDQwODYzLCJleHAiOjEzODg0NDQ3NjMsInZlciI6IjEuMCIsInRpZCI6IjdmZTgxNDQ3LWRhNTctNDM4NS1iZWNiLTZkZTU3ZjIxNDc3ZSIsIm9pZCI6IjY4Mzg5YWUyLTYyZmEtNGIxOC05MWZlLTUzZGQxMDlkNzRmNSIsInVwbiI6ImZyYW5rbUBjb250b3NvLmNvbSIsInVuaXF1ZV9uYW1lIjoiZnJhbmttQGNvbnRvc28uY29tIiwic3ViIjoiZGVOcUlqOUlPRTlQV0pXYkhzZnRYdDJFYWJQVmwwQ2o4UUFtZWZSTFY5OCIsImZhbWlseV9uYW1lIjoiTWlsbGVyIiwiZ2l2ZW5fbmFtZSI6IkZyYW5rIiwiYXBwaWQiOiIyZDRkMTFhMi1mODE0LTQ2YTctODkwYS0yNzRhNzJhNzMwOWUiLCJhcHBpZGFjciI6IjAiLCJzY3AiOiJ1c2VyX2ltcGVyc29uYXRpb24iLCJhY3IiOiIxIn0.JZw8jC0gptZxVC-7l5sFkdnJgP3_tRjeQEPgUn28XctVe3QqmheLZw7QVZDPCyGycDWBaqy7FLpSekET_BftDkewRhyHk9FW_KeEz0ch2c3i08NGNDbr6XYGVayNuSesYk5Aw_p3ICRlUV1bqEwk-Jkzs9EEkQg4hbefqJS6yS1HoV_2EsEhpd_wCQpxK89WPs3hLYZETRJtG5kvCCEOvSHXmDE6eTHGTnEgsIk--UlPe275Dvou4gEAwLofhLDQbMSjnlV5VLsjimNBVcSRFShoxmQwBJR_b2011Y5IuD6St5zPnzruBbZYkGNurQK63TJPWmRd3mbJsGM0mf3CUQ
```

### 錯誤回應
實作 RFC 6750 的受保護資源會發出 HTTP 狀態碼。 如果 hello 要求不包含驗證認證或遺漏權杖，hello 回應 hello 包含`WWW-Authenticate`標頭。 當要求失敗時，hello 資源伺服器會以 hello HTTP 狀態碼和錯誤碼回應。

hello 的範例如下的不成功的回應 hello 用戶端要求不包含 hello 持有者權杖：

```
HTTP/1.1 401 Unauthorized
WWW-Authenticate: Bearer authorization_uri="https://login.microsoftonline.com/contoso.com/oauth2/authorize",  error="invalid_token",  error_description="hello access token is missing.",
```

#### 錯誤參數
| 參數 | 說明 |
| --- | --- |
| authorization_uri |hello hello 授權伺服器的 URI （實體端點）。 作為查閱索引鍵 tooget hello 伺服器從探索端點的詳細資訊，也會使用此值。 <p><p> hello 用戶端必須驗證該 hello 授權伺服器是否受信任。 Hello 資源受 Azure AD，時足夠 tooverify hello URL 開頭 https://login.microsoftonline.com 或另一個 Azure AD 支援的主機名稱。 租用戶特定資源應該一律會傳回租用戶特定授權 URI。 |
| 錯誤 |Hello 的區段 5.2 中定義的錯誤碼值[OAuth 2.0 授權架構](http://tools.ietf.org/html/rfc6749)。 |
| error_description |Hello 錯誤的更詳細的描述。 此訊息不是 toobe 方便使用者讀取為主。 |
| resource_id |傳回 hello hello 資源的唯一識別項。 hello 用戶端應用程式可以使用這個識別碼，做為 hello hello 值`resource`hello 資源權杖要求時的參數。 <p><p> 是很重要的 hello 用戶端應用程式 tooverify 此值，否則，惡意的服務可能無法 tooinduce**提升權限**攻擊 <p><p> 建議的策略，防止攻擊是 hello 的 tooverify hello`resource_id`相符項目 hello hello web API URL 的基底所存取。 例如，如果正在存取 https://service.contoso.com/data，hello`resource_id`可以是 htttps://service.contoso.com/。 hello 用戶端應用程式必須拒絕`resource_id`的開頭不是 hello 基底 URL 除非有可靠的替代方法 tooverify hello 識別碼。 |

#### 持有人配置錯誤碼
hello RFC 6750 規格會定義下列的使用中 hello 回應 hello WWW 驗證標頭和承載配置的資源錯誤 hello。

| HTTP 狀態碼 | 錯誤碼 | 說明 | 用戶端動作 |
| --- | --- | --- | --- |
| 400 |invalid_request |hello 要求格式不正確。 例如，它可能會遺失參數或使用兩次 hello 相同的參數。 |修正 hello 錯誤，然後重試 hello 要求。 這種類型的錯誤應該只會在開發期間發生，並且會在初始測試中偵測出來。 |
| 401 |invalid_token |hello 存取權杖遺漏、 無效或已被撤銷。 hello hello error_description 參數值會提供其他詳細資料。 |來自 hello 授權伺服器要求新權杖。 如果 hello 新權杖失敗，發生未預期的錯誤。 傳送錯誤訊息 toohello 使用者，並在隨機延遲之後重試。 |
| 403 |insufficient_scope |hello 存取權杖不包含 hello 模擬權限需要的 tooaccess hello 資源。 |傳送新的授權要求 toohello 授權端點。 如果 hello 回應包含 hello 範圍參數，使用 hello 要求 toohello 資源 hello 範圍值。 |
| 403 |insufficient_access |hello 權杖主體的 hello 沒有所需的 tooaccess hello 資源 hello 權限。 |提示 hello 使用者 toouse 不同的帳戶或 toorequest 權限 toohello 指定的資源。 |

## 重新整理 hello 存取權杖
存取權杖存留較短，並在到期 toocontinue 存取資源後必須重新整理。 您可以重新整理 hello`access_token`藉由送出另一個`POST`要求 toohello`/token`端點，但提供 hello 這次`refresh_token`而不是 hello `code`。

重新整理權杖並沒有指定的存留期。 一般而言，重新整理權杖的 hello 存留期是較長。 不過，在某些情況下中, 重新整理權杖過期、 遭到撤銷，或缺乏足夠的權限所需的 hello 動作。 您的應用程式需要 tooexpect 和控制代碼正確 hello 權杖發行端點所傳回的錯誤。

當您收到具有重新整理權杖錯誤的回應時，捨棄 hello 目前的重新整理權杖並要求新的授權碼或存取權杖。 特別是，使用重新整理權杖時在 hello 授權碼授與流程中，如果您收到的回應以 hello`interaction_required`或`invalid_grant`錯誤碼、 捨棄 hello 重新整理權杖並要求新的授權碼。

範例要求 toohello**租用戶專屬**端點 (您也可以使用 hello**常見**端點) tooget 使用重新整理權杖的新存取權杖看起來像這樣：

```
// Line breaks for legibility only

POST /{tenant}/oauth2/token HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&refresh_token=OAAABAAAAiL9Kn2Z27UubvWFPbm0gLWQJVzCTE9UkP3pSx1aXxUjq...
&grant_type=refresh_token
&resource=https%3A%2F%2Fservice.contoso.com%2F
&client_secret=JqQX2PNo9bpM0uEihUPzyrh    // NOTE: Only required for web apps
```

### 成功回應
成功的權杖回應如下：

```
{
  "token_type": "Bearer",
  "expires_in": "3600",
  "expires_on": "1460404526",
  "resource": "https://service.contoso.com/",
  "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1THdqcHdBSk9NOW4tQSJ9.eyJhdWQiOiJodHRwczovL3NlcnZpY2UuY29udG9zby5jb20vIiwiaXNzIjoiaHR0cHM6Ly9zdHMud2luZG93cy5uZXQvN2ZlODE0NDctZGE1Ny00Mzg1LWJlY2ItNmRlNTdmMjE0NzdlLyIsImlhdCI6MTM4ODQ0MDg2MywibmJmIjoxMzg4NDQwODYzLCJleHAiOjEzODg0NDQ3NjMsInZlciI6IjEuMCIsInRpZCI6IjdmZTgxNDQ3LWRhNTctNDM4NS1iZWNiLTZkZTU3ZjIxNDc3ZSIsIm9pZCI6IjY4Mzg5YWUyLTYyZmEtNGIxOC05MWZlLTUzZGQxMDlkNzRmNSIsInVwbiI6ImZyYW5rbUBjb250b3NvLmNvbSIsInVuaXF1ZV9uYW1lIjoiZnJhbmttQGNvbnRvc28uY29tIiwic3ViIjoiZGVOcUlqOUlPRTlQV0pXYkhzZnRYdDJFYWJQVmwwQ2o4UUFtZWZSTFY5OCIsImZhbWlseV9uYW1lIjoiTWlsbGVyIiwiZ2l2ZW5fbmFtZSI6IkZyYW5rIiwiYXBwaWQiOiIyZDRkMTFhMi1mODE0LTQ2YTctODkwYS0yNzRhNzJhNzMwOWUiLCJhcHBpZGFjciI6IjAiLCJzY3AiOiJ1c2VyX2ltcGVyc29uYXRpb24iLCJhY3IiOiIxIn0.JZw8jC0gptZxVC-7l5sFkdnJgP3_tRjeQEPgUn28XctVe3QqmheLZw7QVZDPCyGycDWBaqy7FLpSekET_BftDkewRhyHk9FW_KeEz0ch2c3i08NGNDbr6XYGVayNuSesYk5Aw_p3ICRlUV1bqEwk-Jkzs9EEkQg4hbefqJS6yS1HoV_2EsEhpd_wCQpxK89WPs3hLYZETRJtG5kvCCEOvSHXmDE6eTHGTnEgsIk--UlPe275Dvou4gEAwLofhLDQbMSjnlV5VLsjimNBVcSRFShoxmQwBJR_b2011Y5IuD6St5zPnzruBbZYkGNurQK63TJPWmRd3mbJsGM0mf3CUQ",
  "refresh_token": "AwABAAAAv YNqmf9SoAylD1PycGCB90xzZeEDg6oBzOIPfYsbDWNf621pKo2Q3GGTHYlmNfwoc-OlrxK69hkha2CF12azM_NYhgO668yfcUl4VBbiSHZyd1NVZG5QTIOcbObu3qnLutbpadZGAxqjIbMkQ2bQS09fTrjMBtDE3D6kSMIodpCecoANon9b0LATkpitimVCrl PM1KaPlrEqdFSBzjqfTGAMxZGUTdM0t4B4rTfgV29ghDOHRc2B-C_hHeJaJICqjZ3mY2b_YNqmf9SoAylD1PycGCB90xzZeEDg6oBzOIPfYsbDWNf621pKo2Q3GGTHYlmNfwoc-OlrxK69hkha2CF12azM_NYhgO668yfmVCrl-NyfN3oyG4ZCWu18M9-vEou4Sq-1oMDzExgAf61noxzkNiaTecM-Ve5cq6wHqYQjfV9DOz4lbceuYCAA"
}
```
| 參數 | 說明 |
| --- | --- |
| token_type |hello 權杖的型別。 hello 只支援值是**承載**。 |
| expires_in |hello 剩餘 hello 權杖存留期 （秒）。 一般值為 3600 (1 小時)。 |
| expires_on |hello 語彙基元過期 hello 日期和時間在其上。 hello 日期以 hello 的秒數表示從 1970年-01-01T0:0:0Z UTC 直到 hello 到期時間。 |
| resource |識別 hello 保護資源的 hello 存取權杖可以是使用的 tooaccess。 |
| scope |模擬權限授與 toohello 原生用戶端應用程式。 hello 預設權限是**user_impersonation**。 hello hello 目標資源的擁有者可以在 Azure AD 中註冊替代值。 |
| access_token |hello 新存取權杖要求。 |
| refresh_token |新的 OAuth 2.0 refresh_token 這個回應 hello 一個到期時，可能是使用的 toorequest 新存取權杖。 |

### 錯誤回應
範例錯誤回應看起來可能像這樣︰

```
{
  "error": "invalid_resource",
  "error_description": "AADSTS50001: hello application named https://foo.microsoft.com/mail.read was not found in hello tenant named 295e01fc-0c56-4ac3-ac57-5d0ed568f872.  This can happen if hello application has not been installed by hello administrator of hello tenant or consented tooby any user in hello tenant.  You might have sent your authentication request toohello wrong tenant.\r\nTrace ID: ef1f89f6-a14f-49de-9868-61bd4072f0a9\r\nCorrelation ID: b6908274-2c58-4e91-aea9-1f6b9c99347c\r\nTimestamp: 2016-04-11 18:59:01Z",
  "error_codes": [
    50001
  ],
  "timestamp": "2016-04-11 18:59:01Z",
  "trace_id": "ef1f89f6-a14f-49de-9868-61bd4072f0a9",
  "correlation_id": "b6908274-2c58-4e91-aea9-1f6b9c99347c"
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
