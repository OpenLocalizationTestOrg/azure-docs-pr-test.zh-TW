---
title: "授權碼流程 - Azure AD B2C | Microsoft Docs"
description: "了解 toobuild web 應用程式使用 Azure AD B2C 和 OpenID Connect 的驗證通訊協定。"
services: active-directory-b2c
documentationcenter: 
author: saeedakhter-msft
manager: krassk
editor: parakhj
ms.assetid: c371aaab-813a-4317-97df-b62e2f53d865
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/16/2017
ms.author: saeedakhter-msft
ms.openlocfilehash: 6bf9d37310bd45b39bda346441413556f9fd4fdc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-oauth-20-authorization-code-flow"></a>Azure Active Directory B2C：OAuth 2.0 授權碼流程
您可以安裝在裝置 toogain 存取 tooprotected 資源，例如 web Api 的應用程式中使用 hello OAuth 2.0 授權碼授與。 藉由使用 Azure Active Directory B2C hello (Azure AD B2C) 實作的 OAuth 2.0，您可以加入註冊、 登入，以及其他身分識別管理工作 tooyour 行動及桌面應用程式。 這篇文章是與語言無關。 Hello 文章說明如何 toosend 和接收 HTTP 訊息，而不使用任何的開放原始碼程式庫。

<!-- TODO: Need link toolibraries -->

hello OAuth 2.0 授權碼流程述[區段 hello OAuth 2.0 規格的 4.1](http://tools.ietf.org/html/rfc6749)。 在大多數應用程式類型中 (包括 [Web 應用程式](active-directory-b2c-apps.md#web-apps)和[原生安裝的應用程式](active-directory-b2c-apps.md#mobile-and-native-apps))，您可以利用它來執行驗證及授權作業。 您可以使用 OAuth 2.0 取得授權碼流程 toosecurely hello*存取權杖*您的應用程式，它可以是受保護的使用的 tooaccess 資源[授權伺服器](active-directory-b2c-reference-protocols.md#the-basics)。

本文著重在 hello**公用用戶端**OAuth 2.0 授權碼流程。 公開用戶端是密碼的不能信任的 toosecurely 任何用戶端應用程式維持 hello 完整性的密碼。 這包括行動裝置應用程式、 傳統型應用程式，以及基本上和任何應用程式在裝置上執行需要 tooget 存取權杖。 

> [!NOTE]
> tooadd 身分識別管理 tooa web 應用程式使用 Azure AD B2C 使用[OpenID Connect](active-directory-b2c-reference-oidc.md)而不是 OAuth 2.0。

Azure AD B2C 擴充 hello 標準 OAuth 2.0 流動 toodo 超過簡單驗證及授權。 它會導致 hello[原則參數](active-directory-b2c-reference-policies.md)。 使用內建原則，您可以使用 OAuth 2.0 tooadd 使用者體驗 tooyour 應用程式，例如註冊、 登入及管理設定檔。 在本文中，我們會示範如何 toouse OAuth 2.0 和原則 tooimplement 其中每一項發生在原生應用程式中。 我們也會示範如何 tooget 存取權杖來存取 web 應用程式開發介面。

在本文中的 hello 範例 HTTP 要求，我們使用我們的範例 Azure AD B2C 目錄**fabrikamb2c.onmicrosoft.com**。此外，也會使用我們的範例應用程式和原則。 您可以嘗試 hello 要求您自己使用這些值，或您可以取代您自己的值。
了解如何太[取得自己的 Azure AD B2C 目錄、 應用程式，以及原則](#use-your-own-azure-ad-b2c-directory)。

## <a name="1-get-an-authorization-code"></a>1.取得授權碼
hello 授權碼流程的開頭 hello 用戶端導向 hello 使用者 toohello`/authorize`端點。 這是 hello 互動式屬於 hello 流程 hello 使用者會採取動作。 在這項要求，hello 用戶端表示在 hello`scope`它需要從 hello 使用者 tooacquire 參數 hello 權限。 在 [hello`p`參數，它會指出 hello 原則 tooexecute。 hello 下列三個範例 （使用分行符號來提高可讀性） 使用不同的原則。

### <a name="use-a-sign-in-policy"></a>使用登入原則
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=code
&redirect_uri=urn%3Aietf%3Awg%3Aoauth%3A2.0%3Aoob
&response_mode=query
&scope=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&p=b2c_1_sign_in
```

### <a name="use-a-sign-up-policy"></a>使用註冊原則
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=code
&redirect_uri=urn%3Aietf%3Awg%3Aoauth%3A2.0%3Aoob
&response_mode=query
&scope=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&p=b2c_1_sign_up
```

### <a name="use-an-edit-profile-policy"></a>使用編輯設定檔原則
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=code
&redirect_uri=urn%3Aietf%3Awg%3Aoauth%3A2.0%3Aoob
&response_mode=query
&scope=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&p=b2c_1_edit_profile
```

| 參數 | 必要？ | 說明 |
| --- | --- | --- |
| client_id |必要 |hello 應用程式識別碼指派 tooyour 應用程式在 hello [Azure 入口網站](https://portal.azure.com)。 |
| response_type |必要 |hello 回應類型，其中必須包括`code`的 hello 授權碼流程。 |
| redirect_uri |必要 |hello 重新導向的應用程式，其中傳送及接收您的應用程式驗證回應的 URI。 它必須完全符合其中一個 hello 重新導向您在 hello 入口網站註冊 Uri 不同之處在於它必須以 URL 編碼。 |
| scope |必要 |範圍的空格分隔清單。 單一領域值會指出 tooAzure Active Directory (Azure AD) 這兩個要求的 hello 權限。 使用識別碼 hello 範圍表示您的應用程式需要的存取 token，也可以用您自己的服務或 web API，因為所代表的 hello 用戶端 hello 相同的用戶端識別碼。  hello`offline_access`範圍表示您的應用程式需要重新整理權杖，如 tooresources 長時間執行的存取。 您也可以使用 hello`openid`範圍 toorequest 從 Azure AD B2C ID 語彙基元。 |
| response_mode |建議 |您使用 toosend hello 產生授權程式碼後 tooyour 應用程式的 hello 方法。 可以是 `query`、`form_post` 或 `fragment`。 |
| state |建議 |包含在 hello 要求 hello 權杖回應中傳回的值。 它可以是您想要 toouse 任何內容的字串。 通常會使用隨機產生的唯一值，tooprevent 跨網站要求偽造攻擊。 發生 hello 驗證要求之前，hello 狀態也是使用的 tooencode hello 應用程式中的 hello 使用者狀態資訊。 比方說，hello 頁面 hello 使用者，或 hello 所執行的原則。 |
| p |必要 |執行的 hello 原則。 它的 hello 的名稱會在您的 Azure AD B2C 目錄中建立的原則。 hello 原則名稱值開頭應該是**b2c\_1\_**。 toolearn 解原則，請參閱[內建原則，Azure AD B2C](active-directory-b2c-reference-policies.md)。 |
| prompt |選用 |使用者互動所需的 hello 型別。 目前，hello 唯一有效的值是`login`，強制 hello 使用者 tooenter 該要求其認證。 單一登入將沒有作用。 |

此時，會要求 hello 使用者 toocomplete hello 原則的工作流程。 這可能涉及 hello 使用者輸入使用者名稱和密碼，登入社交身分識別，註冊 hello 目錄或任何其他步驟數目。 使用者動作取決於定義 hello 原則的方式。

Hello 使用者完成 hello 原則之後，Azure AD 傳回的回應 tooyour 應用程式，在您所使用的 hello 值`redirect_uri`。 它會使用 hello 中指定的 hello 方法`response_mode`參數。 每個 hello 使用者動作案例，獨立於上次執行所執行的 hello 原則 hello 回應是完全 hello 相同。

使用 `response_mode=query` 的成功回應如下所示：

```
GET urn:ietf:wg:oauth:2.0:oob?
code=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...        // hello authorization_code, truncated
&state=arbitrary_data_you_can_receive_in_the_response                // hello value provided in hello request
```

| 參數 | 說明 |
| --- | --- |
| code |hello hello 應用程式要求授權碼。 hello 應用程式可用於目標資源的 hello 授權程式碼 toorequest 存取權杖。 授權碼的存留期很短。 通常會在大約 10 分鐘後過期。 |
| state |請參閱 hello hello 前面一節中的 hello 資料表中的完整描述。 如果`state`參數包含在 hello 要求 hello 相同的值應該會出現在 hello 回應。 hello 應用程式應該確認該 hello `state` hello 要求和回應中的值完全相同。 |

錯誤回應也可以為傳送 toohello 重新導向 URI，如此 hello 應用程式可以適當處理這些：

```
GET urn:ietf:wg:oauth:2.0:oob?
error=access_denied
&error_description=The+user+has+cancelled+entering+self-asserted+information
&state=arbitrary_data_you_can_receive_in_the_response
```

| 參數 | 說明 |
| --- | --- |
| 錯誤 |您可以使用 tooclassify hello 類型發生之錯誤的錯誤程式碼字串。 您也可以使用 hello 字串 tooreact tooerrors。 |
| error_description |特定的錯誤訊息，可協助您找出 hello 的驗證錯誤的根本原因。 |
| state |請參閱 hello hello 上述資料表中的完整描述。 如果`state`參數包含在 hello 要求 hello 相同的值應該會出現在 hello 回應。 hello 應用程式應該確認該 hello `state` hello 要求和回應中的值完全相同。 |

## <a name="2-get-a-token"></a>2.取得權杖
既然您已取得授權碼，您可以兌換 hello`code`的語彙基元 toohello 主要資源由傳送 POST 要求 toohello`/token`端點。 在 Azure AD B2C，hello 您可以要求的語彙基元的資源是您的應用程式本身的後端 web 應用程式開發介面。 用於要求權杖 tooyourself hello 慣例是的 toouse 應用程式的用戶端識別碼 hello 範圍為：

```
POST fabrikamb2c.onmicrosoft.com/oauth2/v2.0/token?p=b2c_1_sign_in HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

grant_type=authorization_code&client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6&scope=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6 offline_access&code=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...&redirect_uri=urn:ietf:wg:oauth:2.0:oob

```

| 參數 | 必要？ | 說明 |
| --- | --- | --- |
| p |必要 |hello 原則來使用的 tooacquire hello 授權程式碼。 您無法在此要求中使用不同的原則。 請注意，您將加入這個參數 toohello*查詢字串*而非在 hello POST 本文。 |
| client_id |必要 |hello 應用程式識別碼指派 tooyour 應用程式在 hello [Azure 入口網站](https://portal.azure.com)。 |
| grant_type |必要 |hello 的授與的類型。 Hello 授權碼流程，hello 授與類型必須是`authorization_code`。 |
| scope |建議 |範圍的空格分隔清單。 單一領域值會表示 tooAzure AD 這兩個要求的 hello 權限。 使用識別碼 hello 範圍表示您的應用程式需要的存取 token，也可以用您自己的服務或 web API，因為所代表的 hello 用戶端 hello 相同的用戶端識別碼。  hello`offline_access`範圍表示您的應用程式需要重新整理權杖，如 tooresources 長時間執行的存取。  您也可以使用 hello`openid`範圍 toorequest 從 Azure AD B2C ID 語彙基元。 |
| code |必要 |貴用戶取得 hello 流程 hello 第一個階段中的 hello 授權碼。 |
| redirect_uri |必要 |hello 重新導向 hello 您收到 hello 授權程式碼的應用程式的 URI。 |

成功的權杖回應如下所示：

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
| token_type |hello 語彙基元型別值。 hello 只能輸入 Azure AD 支援的承載。 |
| access_token |hello 簽署 JSON Web Token (JWT) 要求。 |
| scope |hello 語彙基元的 hello 範圍無效。 您也可以使用範圍 toocache 語彙基元供以後使用。 |
| expires_in |hello hello 權杖的時間長度 （以秒為單位） 無效。 |
| refresh_token |OAuth 2.0 重新整理權杖。 hello 目前的語彙基元過期之後，hello 應用程式可以使用這個語彙基元 tooacquire 其他語彙基元。 重新整理權杖是長期權杖。 您可以使用它們 tooretain 存取 tooresources 很長的時間。 如需詳細資訊，請參閱 hello [Azure AD B2C 權杖參照](active-directory-b2c-reference-tokens.md)。 |

錯誤回應如下所示：

```
{
    "error": "access_denied",
    "error_description": "hello user revoked access toohello app.",
}
```

| 參數 | 說明 |
| --- | --- |
| 錯誤 |您可以使用 tooclassify hello 類型發生之錯誤的錯誤程式碼字串。 您也可以使用 hello 字串 tooreact tooerrors。 |
| error_description |特定的錯誤訊息，可協助您找出 hello 的驗證錯誤的根本原因。 |

## <a name="3-use-hello-token"></a>3.使用 hello 語彙基元
既然您已成功取得存取權杖，您可以使用要求 tooyour 後端 web 應用程式開發介面的 hello 語彙基元併入 hello`Authorization`標頭：

```
GET /tasks
Host: https://mytaskwebapi.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
```

## <a name="4-refresh-hello-token"></a>4.重新整理 hello 語彙基元
存取權杖和識別碼權杖的存留期短暫。 在到期之後，您必須重新整理它們 toocontinue tooaccess 資源。 toodo，送出另一個的 POST 要求 toohello`/token`端點。 此時，提供 hello`refresh_token`而不是 hello `code`:

```
POST fabrikamb2c.onmicrosoft.com/oauth2/v2.0/token?p=b2c_1_sign_in HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

grant_type=refresh_token&client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6&scope=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6 offline_access&refresh_token=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...&redirect_uri=urn:ietf:wg:oauth:2.0:oob
```

| 參數 | 必要？ | 說明 |
| --- | --- | --- |
| p |必要 |已使用的 tooacquire hello 原始重新整理權杖的 hello 原則。 您無法在此要求中使用不同的原則。 請注意，您將加入這個參數 toohello*查詢字串*而非在 hello POST 本文。 |
| client_id |建議 |hello 應用程式識別碼指派 tooyour 應用程式在 hello [Azure 入口網站](https://portal.azure.com)。 |
| grant_type |必要 |hello 的授與的類型。 Hello 授與類型必須是個 hello 授權碼流程的這個階段， `refresh_token`。 |
| scope |建議 |範圍的空格分隔清單。 單一領域值會表示 tooAzure AD 這兩個要求的 hello 權限。 使用識別碼 hello 範圍表示您的應用程式需要的存取 token，也可以用您自己的服務或 web API，因為所代表的 hello 用戶端 hello 相同的用戶端識別碼。  hello`offline_access`範圍表示您的應用程式，將會需要長時間執行的存取 tooresources 重新整理權杖。  您也可以使用 hello`openid`範圍 toorequest 從 Azure AD B2C ID 語彙基元。 |
| redirect_uri |選用 |hello 重新導向 hello 您收到 hello 授權程式碼的應用程式的 URI。 |
| refresh_token |必要 |hello 原始重新整理語彙基元，貴用戶取得 hello 流程 hello 第二個階段中。 |

成功的權杖回應如下所示：

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
| token_type |hello 語彙基元型別值。 hello 只能輸入 Azure AD 支援的承載。 |
| access_token |hello 簽署您要求的 JWT。 |
| scope |hello 語彙基元的 hello 範圍無效。 您也可以使用 hello 範圍 toocache 語彙基元供以後使用。 |
| expires_in |hello hello 權杖的時間長度 （以秒為單位） 無效。 |
| refresh_token |OAuth 2.0 重新整理權杖。 hello 目前的語彙基元過期之後，hello 應用程式可以使用這個語彙基元 tooacquire 其他語彙基元。 重新整理權杖存留較久，而且可以使用的 tooretain 存取 tooresources 很長的時間。 如需詳細資訊，請參閱 hello [Azure AD B2C 權杖參照](active-directory-b2c-reference-tokens.md)。 |

錯誤回應如下所示：

```
{
    "error": "access_denied",
    "error_description": "hello user revoked access toohello app.",
}
```

| 參數 | 說明 |
| --- | --- |
| 錯誤 |您可以使用 tooclassify 類型發生之錯誤的錯誤程式碼字串。 您也可以使用 hello 字串 tooreact tooerrors。 |
| error_description |特定的錯誤訊息，可協助您找出 hello 的驗證錯誤的根本原因。 |

## <a name="use-your-own-azure-ad-b2c-directory"></a>使用您自己的 Azure AD B2C 目錄
tootry 這些要求自行完成 hello 遵循的步驟。 我們使用您自己的值與本文章中的 hello 範例值取代。

1. [建立 Azure AD B2C 目錄](active-directory-b2c-get-started.md)。 Hello 要求中使用 hello 目錄的名稱。
2. [建立應用程式](active-directory-b2c-app-registration.md)tooobtain 應用程式識別碼和重新導向 URI。 在您的應用程式中包含原生用戶端。
3. [建立您的原則](active-directory-b2c-reference-policies.md)tooobtain 原則名稱。

