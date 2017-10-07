---
title: "aaaChanges toohello Azure AD v2.0 端點 |Microsoft 文件"
description: "Toohello 應用程式模型 v2.0 公用預覽通訊協定所進行的變更的描述。"
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: e6c5b891-0b5d-47dc-8184-5d0ef6a1a006
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/16/2016
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: d7b28a481e12d5dbbc4a10110193bdbd754f4929
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="important-updates-toohello-v20-authentication-protocols"></a>重要的更新 toohello v2.0 驗證通訊協定
開發人員請注意！ 透過 hello 接下來的兩週，我們會提出一些更新 tooour v2.0 驗證通訊協定，這可能表示重大我們預覽期間，您已撰寫的任何應用程式的變更。  

## <a name="who-does-this-affect"></a>那些人會受到影響？
已寫入 toouse hello v2.0 任何應用程式建立聚合式驗證端點

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize
```

可以找到更多資訊 hello v2.0 端點上的[這裡](active-directory-appmodel-v2-overview.md)。

如果您已建立應用程式由撰寫程式碼直接 toohello v2.0 通訊協定，使用 hello v2.0 端點使用任何我們 OpenID Connect 或 OAuth web middlewares 或使用其他第 3 個合作對象文件庫 tooperform 驗證，您應該備妥 tootest 專案和產生如有必要的變更。

## <a name="who-doesnt-this-affect"></a>那些人不會受到影響？
已寫入 hello 實際執行 Azure AD 驗證端點，針對任何應用程式

```
https://login.microsoftonline.com/common/oauth2/authorize
```

此通訊協定一定都是如此，並且不會發生任何變更。

此外，如果您的應用程式**只**使用我們的 ADAL 程式庫 tooperform 驗證，您將不會動用 toochange。  ADAL 具有受防護 hello 變更您的應用程式。  

## <a name="what-are-hello-changes"></a>Hello 變更有哪些？
### <a name="removing-hello-x5t-value-from-jwt-headers"></a>JWT 標頭中移除 hello x5t 值
hello v2.0 端點會使用 JWT 權杖，其中包含相關 hello 語彙基元的相關中繼資料的標頭參數區段。  如果解碼其中我們目前 Jwt 的 hello 標頭時，您會發現像這樣：

```
{ 
    "type": "JWT",
    "alg": "RS256",
    "x5t": "MnC_VZcATfM5pOYiJHMba9goEKY",
    "kid": "MnC_VZcATfM5pOYiJHMba9goEKY"
}
```

這兩個 hello"x5t"和"限 kid"屬性，指定 hello 公開金鑰，應該使用的 toovalidate hello 權杖之簽章，因為從 hello OpenID Connect 的中繼資料端點擷取。

hello 這裡，我們正在進行的變更是 tooremove hello"x5t"屬性。  您可以繼續 toouse hello 相同機制 toovalidate 語彙基元，但應該只信任 hello"限 kid"屬性 tooretrieve hello 正確公開金鑰，以指定在 hello OpenID Connect 通訊協定。 

> [!IMPORTANT]
> **您的工作： 請確定您的應用程式不相依於是否存在 hello hello x5t 值。**
> 
> 

### <a name="removing-profileinfo"></a>移除 profile_info
先前，hello v2.0 端點具有已傳回 base64 編碼的 JSON 物件中呼叫的權杖回應`profile_info`。  當從 hello v2.0 端點要求存取權杖要求傳送到：

```
https://login.microsoftonline.com/common/oauth2/v2.0/token
```

hello 回應 hello 下列 JSON 物件的樣子：

```
{ 
    "token_type": "Bearer",
    "expires_in": 3599,
    "scope": "https://outlook.office.com/mail.read",
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...",
    "refresh_token": "OAAABAAAAiL9Kn2Z27UubvWFPbm0gL...",
    "profile_info": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...",
}
```

hello `profile_info` hello 使用者登入 hello 應用程式的顯示名稱、 名字、 姓氏、 電子郵件地址、 識別碼和等等的值包含資訊。  主要 hello`profile_info`用於權杖快取和顯示用途。

我們現在要移除 hello`profile_info`值-但別擔心，我們仍提供此資訊 toodevelopers，在稍有不同的地方。  而不是`profile_info`，現在會傳回 hello v2.0 端點`id_token`中每個權杖的回應：

```
{ 
    "token_type": "Bearer",
    "expires_in": 3599,
    "scope": "https://outlook.office.com/mail.read",
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...",
    "refresh_token": "OAAABAAAAiL9Kn2Z27UubvWFPbm0gL...",
    "id_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...",
}
```

您可以解碼並剖析 hello id_token tooretrieve hello profile_info 從收到的相同資訊。  hello id_token 是 JSON Web Token (JWT)，與 OpenID Connect 所指定的內容。  hello 這麼做的程式碼應該非常類似，您只需要 tooextract hello 中間區段 （hello 主體） 的 hello id_token 和 base64 解碼 tooaccess hello JSON 物件內。

透過 hello 接下來的兩週，您應撰寫您的應用程式 tooretrieve hello 的使用者資訊從任一 hello`id_token`或`profile_info`; 兩者中較存在。  如此一來當 hello 變更時，您的應用程式順暢地處理從 hello 轉換`profile_info`太`id_token`不中斷。

> [!IMPORTANT]
> **您的工作： 請確定您的應用程式不相依於是否存在 hello hello`profile_info`值。**
> 
> 

### <a name="removing-idtokenexpiresin"></a>移除 id_token_expires_in
類似太`profile_info`，我們也想要移除 hello`id_token_expires_in`回應中的參數。  Hello v2.0 端點之前，會傳回的值`id_token_expires_in`以及每個 id_token 回應，例如在授權回應：

```
https://myapp.com?id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...&id_token_expires_in=3599...
```

或權杖回應中：

```
{ 
    "token_type": "Bearer",
    "id_token_expires_in": 3599,
    "scope": "openid",
    "id_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...",
    "refresh_token": "OAAABAAAAiL9Kn2Z27UubvWFPbm0gL...",
    "profile_info": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...",
}
```

hello`id_token_expires_in`值會指出 hello hello id_token 仍然為有效的秒數。  現在，我們會移除 hello`id_token_expires_in`完全值。  相反地，您可以使用 hello OpenID Connect 標準`nbf`和`exp`宣告 id_token tooexamine hello 有效性。  請參閱 hello [v2.0 權杖參照](active-directory-v2-tokens.md)如需有關這些宣告。

> [!IMPORTANT]
> **您的工作： 請確定您的應用程式不相依於是否存在 hello hello`id_token_expires_in`值。**
> 
> 

### <a name="changing-hello-claims-returned-by-scopeopenid"></a>變更 hello 宣告範圍傳回 = openid
這項變更將最重要 – hello 事實上，它會影響使用 hello v2.0 端點幾乎每個應用程式。  許多應用程式傳送要求 toohello v2.0 端點使用 hello`openid`範圍，例如：

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=...
&redirect_uri=...
&response_mode=form_post
&response_type=id_token
&scope=openid offline_access https://outlook.office.com/mail.read
```

今天，當 hello 使用者授與同意，以便 hello`openid`範圍內，您的應用程式接收豐富的 hello 使用者資訊以產生 id_token hello。  這些宣告可以包含其名稱、慣用的使用者名稱、電子郵件地址、物件識別碼等等。

在此更新中，我們會變更 hello 資訊時，該 hello`openid`範圍可以提供您的應用程式的存取權，toobetter comform 以 hello OpenID Connect 的規格。  hello`openid`範圍會只允許應用程式 toosign hello 使用者中，並在 hello 收到 hello 使用者應用程式特定識別項`sub`hello id_token 的宣告。  hello id_token 中的宣告，以只 hello`openid`範圍授與將抹除任何個人識別資訊。  範例 id_token 宣告為：

```
{ 
    "aud": "580e250c-8f26-49d0-bee8-1c078add1609",
    "iss": "https://login.microsoftonline.com/b9410318-09af-49c2-b0c3-653adc1f376e/v2.0 ",
    "iat": 1449520283,
    "nbf": 1449520283,
    "exp": 1449524183,
    "nonce": "12345",
    "sub": "MF4f-ggWMEji12KynJUNQZphaUTvLcQug5jdF2nl01Q",
    "tid": "b9410318-09af-49c2-b0c3-653adc1f376e",
    "ver": "2.0",
}
```

如果您想 tooobtain 個人識別資訊 (PII) 有關 hello 使用者應用程式中，您的應用程式必須 toorequest hello 使用者從其他權限。  我們採用兩個新領域的支援從 hello OpenID Connect 規格 – hello`email`和`profile`範圍 – 可讓您 toodo 因此。

* hello`email`範圍是非常簡單，因為它可讓您的應用程式存取 toohello 使用者的主要電子郵件地址，透過 hello `email` hello id_token 中宣告。  請注意該 hello`email`宣告不一定會出現在 id_tokens – 它將只會包含如果有的話，在 hello 使用者設定檔。
* hello`profile`範圍可以提供您的應用程式存取 tooall hello 使用者 – 其名稱、 慣用的使用者名稱，其他基本資訊的物件識別碼，等等。

這可讓您 toocode 您的應用程式，以最少洩漏的方式 – 您可以要求 hello 使用者只要 hello 組的應用程式需要 toodo 其工作的資訊。  如果您想取得 hello 目前接收您的應用程式的使用者資訊的一組完整的 toocontinue，授權要求中應包含所有的三個範圍：

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=...
&redirect_uri=...
&response_mode=form_post
&response_type=id_token
&scope=openid profile email offline_access https://outlook.office.com/mail.read
```

您的應用程式可以開始傳送嗨`email`和`profile`立即範圍和 hello v2.0 端點會將接受這些兩個範圍，並開始視要求來自使用者的權限。  但是 hello 變更中的 hello 的 hello 解譯`openid`範圍不會生效幾週。

> [!IMPORTANT]
> **您的工作： 新增 hello`profile`和`email`範圍，如果您的應用程式需要 hello 使用者的相關資訊。**  請注意，ADAL 預設會在要求中同時包含這些權限。 
> 
> 

### <a name="removing-hello-issuer-trailing-slash"></a>正在移除 hello 簽發者結尾斜線。
Hello 簽發者值，這個值會顯示在權杖中的 hello v2.0 端點之前，花費了 hello 表單

```
https://login.microsoftonline.com/{some-guid}/v2.0/
```

其中 hello guid 為 hello 發行 hello 語彙基元的 hello Azure AD 租用戶的 tenantId。  這些變更，變成 hello 簽發者值

```
https://login.microsoftonline.com/{some-guid}/v2.0 
```

在這兩個語彙基元和 hello OpenID Connect 探索文件中。

> [!IMPORTANT]
> **您的工作： 請確定您的應用程式簽發者驗證期間會接受 hello 簽發者值與並沒有尾端斜線。**
> 
> 

## <a name="why-change"></a>為何變更？
hello 來介紹這些變更的主要動機是 toobe 與 hello OpenID Connect 標準規格相容。  透過 OpenID Connect 標準，我們希望 toominimize 差異整合 Microsoft 識別服務與 hello 產業中的其他身分識別服務。  我們想要 tooenable 開發人員 toouse 他們最愛的開放原始碼的驗證程式庫而不需要 tooalter hello 文件庫 tooaccommodate Microsoft 差異。

## <a name="what-can-you-do"></a>您該怎麼辦？
目前，您可以開始進行所有的 hello 變更上面所述。  您應該立即：

1. **移除任何相依性 hello `x5t` header 參數。**
2. **正常處理從 hello 轉換`profile_info`太`id_token`權杖回應中。**
3. **移除任何相依性 hello`id_token_expires_in`回應參數。**
4. **新增 hello`profile`和`email`範圍 tooyour 應用程式如果您的應用程式需要基本使用者的資訊。**
5. **在權杖中接受包含或不含結尾斜線的簽發者值。**

我們[v2.0 通訊協定文件](active-directory-v2-protocols.md)已經過更新的 tooreflect 這些變更，因此您可以使用它做為參考，幫助您更新您的程式碼。

如果您在 hello hello 變更範圍上有任何進一步的問題，請隨時可用 tooreach out toous 在 Twitter 上@AzureAD。

## <a name="how-often-will-protocol-changes-occur"></a>通訊協定變更發生頻率為何？
我們未預期任何進一步重大變更 toohello 驗證通訊協定。  我們會刻意結合在一起到一個發行這些變更，所以您不需要 toogo 透過這種類型的更新程序再次隨時推出。  當然，我們會繼續 tooadd 功能 toohello 交集 v2.0 驗證服務，您可以利用，但這些變更應該附加與中斷現有的程式碼。

最後，我們希望 toosay 感謝您試用事項 hello 預覽期間。  hello 深入資訊和體驗的我們早期採用者一兩為止，而且我們希望您的意見與想法，您將會繼續 tooshare。

祝各位編碼程式愉快！

Microsoft 身分識別除法 hello

