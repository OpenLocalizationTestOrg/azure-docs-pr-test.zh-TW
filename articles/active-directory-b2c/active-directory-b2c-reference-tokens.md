---
title: "Azure Active Directory B2C：權杖參考 | Microsoft Docs"
description: "在 Azure Active Directory B2C 發出的 token hello 類型"
services: active-directory-b2c
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 6df79878-65cb-4dfc-98bb-2b328055bc2e
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/17/2017
ms.author: dastrock
ms.openlocfilehash: 776bc88cc0308875ac6e576f19ac9edf50319d08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-token-reference"></a>Azure AD B2C：權杖參考
Azure Active Directory B2C (Azure AD B2C) 會在處理每個[驗證流程](active-directory-b2c-apps.md)時發出數種安全性權杖。 本文件說明 hello 格式、 安全性的特性，以及每種類型的語彙基元的內容。

## <a name="types-of-tokens"></a>權杖的類型
Azure AD B2C 支援 hello [OAuth 2.0 授權通訊協定](active-directory-b2c-reference-protocols.md)，是會利用這兩者的存取權杖和重新整理權杖。 它也支援驗證和登入透過[OpenID Connect](active-directory-b2c-reference-protocols.md)，其中導入了第三種類型的語彙基元： hello 的 ID 語彙基元。 每個權杖都是以持有人權杖表示。

承載權杖是輕巧型的安全性權杖會授與 hello"bearer"存取 tooa 受保護資源。 hello 持有者是指可出示 hello 語彙基元任何一方。 Azure AD 必須先驗證合作對象，才能接收持有人權杖。 但是，它在 hello 必要步驟不會採用 toosecure 傳輸和儲存體中的 hello 語彙基元可以攔截和使用的非預期的合作對象。 某些安全性權杖有內建的機制，可防止未授權的合作對象使用它們，但持有人權杖沒有這項機制。 它們必須在安全的通道 (例如傳輸層安全性 (HTTPS)) 中傳輸。

持有人權杖傳輸到外部安全通道，如果惡意人士可以使用攔截攻擊 tooacquire hello 語彙基元，並使用它 toogain 未經授權存取 tooa 受保護的資源。 當您儲存或快取供稍後使用持有者權杖時，適用相同的安全性原則的 hello。 務必確定您的應用程式以安全的方式傳輸和儲存持有人權杖。

如需持有人權杖的其他安全性考量，請參閱 [RFC 6750 第 5 節](http://tools.ietf.org/html/rfc6750)。

許多 Azure AD B2C 發出的 hello 權杖會實作為 JSON web 權杖 (Jwt)。 JWT 是一種精簡的 URL 安全方法，可在兩方之間傳輸資訊。 JWT 包含稱為宣告的資訊。 這些是 hello 持有者的相關資訊的判斷提示和 hello 權杖主體的 hello。 在 Jwt 的 hello 宣告是編碼和傳輸序列化的 JSON 物件。 因為 hello Azure AD B2C 所發出的 Jwt 是簽署，但是不會加密，您可以輕鬆地檢查 JWT toodebug hello 內容它。 有一些工具可以這樣做，包括 [calebb.net](http://calebb.net)。 如需 Jwt 的詳細資訊，請參閱太[JWT 規格](http://self-issued.info/docs/draft-ietf-oauth-json-web-token.html)。

### <a name="id-tokens"></a>ID 權杖
ID 語彙基元是一種安全性權杖，您的應用程式接收來自 Azure AD B2C hello`authorize`和`token`端點。 ID 語彙基元會表示為[Jwt](#types-of-tokens)，且其中包含您可以在應用程式中使用 tooidentify 使用者的宣告。 ID 語彙基元時取自 hello`authorize`端點，這些通常是使用的 toosign 使用者 tooweb 應用程式中。 ID 語彙基元時取自 hello`token`端點，它們可以傳送 HTTP 要求中的 hello 的兩個元件之間進行通訊時相同應用程式或服務。 根據您的需要，您可以使用 hello 宣告識別碼權杖中。 它們是常用的 toodisplay 帳戶資訊或 toomake 存取控制決定應用程式中。  

識別碼權杖已簽署，但目前未加密。 當您的應用程式或應用程式開發介面接收 ID 語彙基元時，它必須[驗證 hello 簽章](#token-validation)hello 語彙基元的 tooprove 是真確的。 您的應用程式或應用程式開發介面也必須驗證中是有效的 hello 語彙基元 tooprove 幾個宣告。 根據 hello 案例的需求，hello 宣告驗證的應用程式可能會不同，但您的應用程式必須執行一些[常見的宣告驗證](#token-validation)在每個案例。

#### <a name="sample-id-token"></a>範例 ID 權杖
```
// Line breaks for display purposes only

eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsImtpZCI6IklkVG9rZW5TaWduaW5nS2V5Q29udGFpbmVyIn0.
eyJleHAiOjE0NDIzNjAwMzQsIm5iZiI6MTQ0MjM1NjQzNCwidmVyIjoiMS4wIiwiaXNzIjoiaHR0cHM6Ly9s
b2dpbi5taWNyb3NvZnRvbmxpbmUuY29tLzc3NTUyN2ZmLTlhMzctNDMwNy04YjNkLWNjMzExZjU4ZDkyNS92
Mi4wLyIsImFjciI6ImIyY18xX3NpZ25faW5fc3RvY2siLCJzdWIiOiJOb3Qgc3VwcG9ydGVkIGN1cnJlbnRs
eS4gVXNlIG9pZCBjbGFpbS4iLCJhdWQiOiI5MGMwZmU2My1iY2YyLTQ0ZDUtOGZiNy1iOGJiYzBiMjlkYzYi
LCJpYXQiOjE0NDIzNTY0MzQsImF1dGhfdGltZSI6MTQ0MjM1NjQzNCwiaWRwIjoiZmFjZWJvb2suY29tIn0.
h-uiKcrT882pSKUtWCpj-_3b3vPs3bOWsESAhPMrL-iIIacKc6_uZrWxaWvIYkLra5czBcGKWrYwrAC8ZvQe
DJWZ50WXQrZYODEW1OUwzaD_I1f1HE0c2uvaWdGXBpDEVdsD3ExKaFlKGjFR2V7F-fPThkVDdKmkUDQX3bVc
yyj2V2nlCQ9jd7aGnokTPfLfpOjuIrTsAdPcGpe5hfSEuwYDmqOJjGs9Jp1f-eSNEiCDQOaTBSvr479L5ptP
XWeQZyX2SypN05Rjr05bjZh3j70ZUimiocfJzjibeoDCaQTz907yAg91WYuFOrQxb-5BaUoR7K-O7vxr2M-_
CQhoFA

```

### <a name="access-tokens"></a>存取權杖
存取語彙基元也是一種安全性權杖，您的應用程式接收來自 Azure AD B2C hello`authorize`和`token`端點。 存取語彙基元也會表示為[Jwt](#types-of-tokens)，且其中包含您可以使用 tooidentify hello 授與權限 tooyour 應用程式開發介面的宣告。 存取權杖已簽署，但目前未加密。 存取權杖應該使用的 tooprovide 存取 tooAPIs 和資源伺服器。 深入了解如何太[使用存取權杖](active-directory-b2c-access-tokens.md)。 

當您的 API 接收存取權杖時，它必須[驗證 hello 簽章](#token-validation)hello 語彙基元的 tooprove 是真確的。 您的 API 也必須驗證中是有效的 hello 語彙基元 tooprove 幾個宣告。 根據 hello 案例的需求，hello 宣告驗證的應用程式可能會不同，但您的應用程式必須執行一些[常見的宣告驗證](#token-validation)在每個案例。

### <a name="claims-in-id-and-access-tokens"></a>識別碼和存取權杖中的宣告
當您使用 Azure AD B2C 時，您會有更細微的控制您的語彙基元的 hello 內容。 您可以設定[原則](active-directory-b2c-reference-policies.md)toosend 特定設定的應用程式需要其作業的宣告中的使用者資料。 這些宣告可以包含標準的屬性，例如 hello 使用者`displayName`和`emailAddress`。 其中也可以包含您在 B2C 目錄中可定義的 [自訂使用者屬性](active-directory-b2c-reference-custom-attr.md) 。 您收到的每個識別碼權杖和存取權杖都會包含一組特定的安全性相關宣告。 您的應用程式可以使用 toosecurely 驗證的使用者和要求這些宣告。

請注意，任何特定順序將不會傳回識別碼權杖中的 hello 宣告。 此外，隨時都可以在 ID 權杖中加入新的宣告。 加入新的宣告時，您的應用程式不會損壞。 以下是您預期 tooexist，Azure AD B2C 所發出的識別碼和存取權杖中的 hello 宣告。 其他任何宣告都由原則決定。 練習中，請再試一次檢查透過將其貼的 hello 範例識別碼權杖中的 hello 宣告[calebb.net](http://calebb.net)。 詳細資訊，可以在 hello [OpenID Connect 規格](http://openid.net/specs/openid-connect-core-1_0.html)。

| 名稱 | 宣告 | 範例值 | 說明 |
| --- | --- | --- | --- |
| 對象 |`aud` |`90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6` |Audience 宣告識別 hello 語彙基元的 hello 預期收件的者。 Azure AD B2C，如 hello 適用對象會是您的應用程式的應用程式識別碼，為指派的 tooyour hello 應用程式註冊入口網站中的應用程式。 您的應用程式應該驗證此值，並拒絕 hello 語彙基元，如果不符合。 |
| 簽發者 |`iss` |`https://login.microsoftonline.com/775527ff-9a37-4307-8b3d-cc311f58d925/v2.0/` |此宣告識別 hello 安全性權杖服務 (STS) 的建構，並且傳回 hello 語彙基元。 它也可以識別 hello Azure AD 目錄中的 hello 驗證使用者。 您的應用程式應該先驗證 hello issuer 宣告 hello 語彙基元的 tooensure 來自 hello Azure Active Directory v2.0 端點。 |
| 發出時間 |`iat` |`1438535543` |此宣告是 hello 的 hello 權杖的發出的時間，表示在 epoch 時間。 |
| 到期時間 |`exp` |`1438539443` |hello 逾期時間宣告是 hello 時間在哪一個 hello 權杖就會變成無效，表示在 epoch 時間。 您的應用程式應該使用此宣告 tooverify hello 的有效性 hello 權杖存留期。 |
| 生效時間 |`nbf` |`1438535543` |此宣告是在哪一個 hello 權杖就會變成無效，會在 epoch 時間中表示的 hello 時間。 這是通常 hello 相同 hello 時間 hello 語彙基元已發行。 您的應用程式應該使用此宣告 tooverify hello 的有效性 hello 權杖存留期。 |
| 版本 |`ver` |`1.0` |Azure AD 所定義，這會是 hello 的 ID 語彙基元，hello 版本。 |
| 代碼雜湊 |`c_hash` |`SGCPtt01wxwfgnYZy2VJtQ` |OAuth 2.0 授權碼連同發出 hello 語彙基元時，才雜湊程式碼一併併入 ID 語彙基元。 雜湊程式碼可以使用的 toovalidate hello 真實性的授權碼。 如需有關如何 tooperform 這項驗證，請參閱 hello [OpenID Connect 規格](http://openid.net/specs/openid-connect-core-1_0.html)。  |
| 存取權杖雜湊 |`at_hash` |`SGCPtt01wxwfgnYZy2VJtQ` |存取語彙基元的雜湊隨附於 ID 權杖，才會在 OAuth 2.0 存取權杖以及核發 hello 權杖。 存取語彙基元的雜湊可以是使用的 toovalidate hello 真實性的存取權杖。 如需有關如何 tooperform 這項驗證，請參閱 hello [OpenID Connect 規格](http://openid.net/specs/openid-connect-core-1_0.html)  |
| Nonce |`nonce` |`12345` |Nonce 是一種策略使用 toomitigate 權杖重新執行攻擊。 您的應用程式可以利用 hello 授權要求中指定的 nonce`nonce`查詢參數。 您提供 hello 要求中的 hello 值將會發出未經修改的 hello`nonce`只 ID 權杖的宣告。 這可讓您的應用程式 tooverify hello 值，它指定 hello 要求時，其使用指定的 ID 語彙基元關聯 hello 應用程式工作階段的 hello 值。 您的應用程式應該執行這項驗證 hello 識別碼權杖驗證程序期間。 |
| 主旨 |`sub` |`884408e1-2918-4cz0-b12d-3aa027d7563b` |這是 hello 主體的 hello 權杖判斷提示的相關資訊，例如 hello 使用者應用程式。 這個值不可變，而且無法重新指派或重複使用。 它可以使用的 tooperform 授權檢查，例如 hello 語彙基元時使用的 tooaccess 資源。 根據預設，hello 主體宣告會填入 hello 目錄中的 hello 使用者 hello 物件識別碼。 詳細資訊，請參閱 toolearn [Azure Active Directory B2C： 語彙基元、 session 和單一登入組態](active-directory-b2c-token-session-sso.md)。 |
| 驗證內容類別參考 |`acr` |不適用 |目前未使用，除非在 hello 案例的較舊的原則。 詳細資訊，請參閱 toolearn [Azure Active Directory B2C： 語彙基元、 session 和單一登入組態](active-directory-b2c-token-session-sso.md)。 |
| 信任架構原則 |`tfp` |`b2c_1_sign_in` |這是 hello hello 原則的已使用的 tooacquire hello ID 語彙基元名稱。 |
| 驗證期間 |`auth_time` |`1438535543` |此宣告是 hello 時間的使用者最後一個輸入的認證，以表示 epoch 時間。 |

### <a name="refresh-tokens"></a>重新整理權杖
重新整理權杖是安全性權杖，應用程式可以使用新識別碼語彙基元 tooacquire 及存取權杖的 OAuth 2.0 流程中。 它們提供您的應用程式與長期存取 tooresources 代表使用者而不需要與這些使用者互動。

tooreceive 重新整理權杖，權杖的回應中，您的應用程式必須要求 hello`offline_acesss`範圍。 深入了解 hello toolearn`offline_access`範圍，請參閱 toohello [Azure AD B2C 通訊協定參考](active-directory-b2c-reference-protocols.md)。

重新整理權杖，而且將永遠為，完全不透明 tooyour 應用程式。 它們是由 Azure AD 所簽發，只能由 Azure AD 檢查和解譯。 它們是長時間執行，但不是會寫入您的應用程式並重新整理權杖將持續一段特定時間的 hello 預期情況。 重新整理權杖可能會因為各種原因而隨時失效。 只有您的應用程式 tooknow 如果重新整理權杖是有效的方式為 tooattempt tooredeem hello 它藉由權杖要求 tooAzure AD。

當您兌換新權杖重新整理權杖 (如果您的應用程式授與 hello 和`offline_access`範圍)，您將收到新的重新整理權杖的 hello 權杖回應。 您應該儲存 hello 剛發行的重新整理權杖。 它應該取代您先前使用 hello 要求中的 hello 重新整理權杖。 這有助於保證您的重新整理權杖盡可能長期保持有效。

## <a name="token-validation"></a>權杖驗證
toovalidate 語彙基元，您的應用程式應該檢查 hello 簽章和 hello 權杖的宣告。

視您偏好的語言而定，有許多開放原始碼程式庫可用來驗證 JWT。 我們建議您探索這些選項，而不是實作您自己的驗證邏輯。 本指南中的 hello 資訊可協助您了解 tooproperly 使用這些程式庫。

### <a name="validate-hello-signature"></a>驗證 hello 簽章
JWT 包含三個區段，以 hello 分隔`.`字元。 hello 第一個區段是 hello*標頭*，hello 第二種是 hello*主體*，和 hello 第三個為 hello*簽章*。 hello 簽章區段，讓它可以信任的應用程式，可以是 hello 語彙基元使用的 toovalidate hello 真確性。

Azure AD B2C 權杖是經由業界標準非對稱式加密演算法 (例如 RSA 256) 進行簽署。 hello 語彙基元 hello 標頭包含 hello 索引鍵的相關資訊，並使用 toosign hello token 的加密方法：

```
{
        "typ": "JWT",
        "alg": "RS256",
        "kid": "GvnPApfWMdLRi8PDmisFn7bprKg"
}
```

hello`alg`宣告表示已使用的 toosign hello 語彙基元的 hello 演算法。 hello`kid`宣告表示 hello 特定的公用金鑰是使用的 toosign hello 語彙基元。

無論何時，Azure AD 都能使用任何一組特定的公開-私密金鑰組來簽署權杖。 Azure AD 會定期旋轉 hello 組可能的索引鍵，因此您的應用程式應撰寫的 toohandle 這些金鑰會自動變更。 合理的頻率 toocheck 更新 toohello： 公開金鑰的 Azure AD 使用的是每隔 24 小時。

Azure AD B2C 具有 OpenID Connect 中繼資料端點。 這可讓應用程式在執行階段 關於 Azure AD B2C toofetch 資訊。 這項資訊包括端點、權杖內容和權杖簽署金鑰。 您的 B2C 目錄包含每個原則的 JSON 中繼資料文件。 例如，hello 中繼資料文件以 hello`b2c_1_sign_in`中的原則`fabrikamb2c.onmicrosoft.com`位於：

```
https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/v2.0/.well-known/openid-configuration?p=b2c_1_sign_in
```

`fabrikamb2c.onmicrosoft.com`hello B2C 目錄使用 tooauthenticate hello 使用者，會和`b2c_1_sign_in`hello 原則使用 tooacquire hello 語彙基元。 toodetermine 哪些原則已使用的 toosign 語彙基元 （和其中 toogo toofetch hello 中繼資料），有兩個選項。 首先，hello 原則名稱包含在 hello `acr` hello 權杖中宣告。 您可以剖析從 base 64 解碼 hello 主體所的 hello 本文 hello JWT 的宣告和 hello 還原序列化 JSON 字串而產生。 hello`acr`宣告將會是 hello hello 原則的已使用的 tooissue hello 語彙基元名稱。  另一個選擇是 tooencode hello hello 值中的 hello 原則`state`時發出 hello 要求然後解碼的 toodetermine 哪些原則已使用的參數。 任一種方法都有效。

hello 中繼資料文件是資訊的 JSON 物件，其中包含數項有用。 這些包括 hello 的位置 hello 端點需要 tooperform OpenID Connect 驗證。 其中也包括`jwks_uri`，可讓 hello hello 組之公開金鑰是使用的 toosign 語彙基元的位置。 此處，提供該位置，但它是最佳的 toofetch hello 位置以動態方式使用 hello 中繼資料文件並剖析出`jwks_uri`:

```
https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/discovery/v2.0/keys?p=b2c_1_sign_in
```

hello JSON 文件位於此 URL 包含所有 hello 公開金鑰資訊在特定時間點的使用中。 您的應用程式可以使用 hello `kid` hello JWT 標頭 tooselect hello 公開金鑰中所使用的 toosign hello JSON 文件中宣告之特定 token。 它然後可以使用正確的公用金鑰 hello 和 hello 指定的演算法，以執行簽章驗證。

描述 tooperform 簽章驗證的這份文件的 hello 範圍外的方式。 許多開放原始碼程式庫是與此資料庫，如果您需要的可用 toohelp。

### <a name="validate-hello-claims"></a>驗證 hello 宣告
當您的應用程式或應用程式開發介面接收 ID 語彙基元時，它也應該執行對 hello 宣告數個檢查 hello 的 ID 語彙基元中。 包含但不限於：

* hello**觀眾**宣告： 這樣會確認該 hello ID 語彙基元已預定的 toobe 指定 tooyour 應用程式。
* hello**不早於**和**到期時間**宣告： 這些確認該 hello 識別碼權杖尚未過期。
* hello**簽發者**宣告： 這樣會確認該 hello 語彙基元由 Azure AD 發出 tooyour 應用程式。
* hello **nonce**： 這是權杖重新執行攻擊的風險降低的策略。

如需驗證您的應用程式應該執行的完整清單，請參閱 toohello [OpenID Connect 規格](https://openid.net)。 Hello 預期這些宣告的值的詳細資料會包含在 hello 上述[語彙基元區段](#types-of-tokens)。  

## <a name="token-lifetimes"></a>權杖存留期
hello 後權杖存留期會提供 toofurther 知識。 當您開發及偵錯應用程式時，它們可以協助您。 請注意，您的應用程式不應該寫入 tooexpect 任何這些存留期 tooremain 常數。 它們會變更。 深入了解 hello[自訂權杖的存留期](active-directory-b2c-token-session-sso.md)在 Azure AD B2C。

| 權杖 | 存留期 | 說明 |
| --- | --- | --- |
| ID 權杖 |一小時 |ID 權杖的有效期通常為 1 小時。 您的 web 應用程式可以使用此存留期 toomaintain 它自己的工作階段的使用者 （建議選項）。 您也可以選擇不同的工作階段存留期。 如果您的應用程式需要 tooget 新的 ID 語彙基元，它只需 toomake 新的登入要求 tooAzure AD。 如果使用者具有 Azure AD 的有效的瀏覽器工作階段，該使用者可能不需要的 tooenter 認證一次。 |
| 重新整理權杖 |向上 too14 天 |單一重新整理權杖的有效期最多 14 天。 不過，重新整理權杖可能會基於許多因素而隨時失效。 您的應用程式應該繼續 tootry toouse 重新整理權杖，直到 hello 要求失敗，或您的應用程式取代新 hello 重新整理權杖。 重新整理權杖也成為如果 90 天內有自從上次 hello 使用者輸入的認證無效。 |
| 授權碼 |五分鐘 |授權碼是刻意設計成短期。 它們應在收到時立即兌換成存取權杖、ID 權杖或重新整理權杖。 |

