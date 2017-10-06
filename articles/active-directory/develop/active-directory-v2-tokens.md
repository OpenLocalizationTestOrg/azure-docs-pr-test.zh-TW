---
title: "aaaAzure Active Directory v2.0 權杖參考 |Microsoft 文件"
description: "hello 類型的權杖與 hello Azure AD v2.0 端點所發出的宣告"
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: dc58c282-9684-4b38-b151-f3e079f034fd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 29eb5c3402aeae302ee7c6234488520495f85904
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-v20-tokens-reference"></a>Azure Active Directory v2.0 權杖參考
hello Azure Active Directory (Azure AD) v2.0 端點發出幾種類型的安全性權杖，在每個[驗證流程](active-directory-v2-flows.md)。 此參考描述 hello 格式、 安全性的特性，以及每種類型的語彙基元的內容。

> [!NOTE]
> hello v2.0 端點不支援所有的 Azure Active Directory 的案例和功能。 toodetermine 是否應該使用 hello v2.0 端點，閱讀有關[v2.0 限制](active-directory-v2-limitations.md)。
>
>

## <a name="types-of-tokens"></a>權杖的類型
hello v2.0 端點支援 hello [OAuth 2.0 授權通訊協定](active-directory-v2-protocols.md)，它會使用存取權杖和重新整理權杖。 hello v2.0 端點也支援驗證和登入透過[OpenID Connect](active-directory-v2-protocols.md)。 OpenID Connect 導入了第三種類型的語彙基元，hello ID 語彙基元。 這些權杖中的每一個都是以「持有人」權杖來表示。

承載權杖是輕巧型的安全性權杖會授與 hello 承載存取 tooa 受保護資源。 hello 持有者是指可出示 hello 語彙基元任何一方。 雖然合作對象必須向 Azure AD tooreceive hello 持有者權杖，如果步驟在傳輸與儲存期間不會採用 toosecure hello 語彙基元，它可以攔截和使用非預期的合作對象。 某些安全性權杖有內建機制 tooprevent 未經授權的合作對象不使用它們，但持有人權杖。 持有人權杖必須在安全的通道 (例如傳輸層安全性 (HTTPS)) 中傳輸。 如果沒有這種類型的安全性傳輸持有者權杖，惡意的合作對象無法使用"攔截攻擊"tooacquire hello 語彙基元，並使用它未經授權的存取 tooa 受保護的資源。 hello 儲存或快取持有者權杖供以後使用時，適用相同的安全性原則。 請一律確保您的應用程式以安全的方式傳輸和儲存持有人權杖。 如需了解持有人權杖的更多安全性考量，請參閱 [RFC 6750 第 5 節](http://tools.ietf.org/html/rfc6750)。

許多 hello hello v2.0 端點所發出的權杖會實作為 JSON Web 權杖 (Jwt)。 JWT 是兩個合作對象之間的壓縮、 URL 安全的方式 tootransfer 資訊。 JWT 中的 hello 資訊稱為*宣告*。 它是 hello 持有者的相關資訊的判斷提示和 hello 權杖的主體。 JWT 中的 hello 宣告是編碼，以及如何序列化為傳輸的 JavaScript Object Notation (JSON) 物件。 由於 hello Jwt 發給 hello v2.0 端點簽署，但是不會加密，因此，您可以輕鬆地檢查 JWT hello 內容以進行偵錯。 如需 Jwt 的詳細資訊，請參閱 hello [JWT 規格](http://self-issued.info/docs/draft-ietf-oauth-json-web-token.html)。

### <a name="id-tokens"></a>ID 權杖
識別碼權杖是您的應用程式使用 [OpenID Connect](active-directory-v2-protocols.md) 來執行驗證時所收到的一種登入安全性權杖形式。 ID 語彙基元會表示為[Jwt](#types-of-tokens)，且其中包含您可以在 tooyour 應用程式中使用 toosign hello 使用者的宣告。 您可以使用 hello 宣告中的 ID 語彙基元，以各種方式。 一般而言，系統管理員 」 應用程式中使用識別碼權杖 toodisplay 帳戶資訊或 toomake 存取控制決定。 hello v2.0 端點發出 ID 語彙基元，其具有一組一致的宣告，不論 hello 登入的使用者類型只能有一個的類型。 hello 格式和內容的 ID 語彙基元是個人的 Microsoft 帳戶使用者和工作或學校帳戶 hello 相同。

目前識別碼權杖已簽署但未加密。 當您的應用程式收到的 ID 語彙基元時，它必須[驗證 hello 簽章](#validating-tokens)tooprove hello 權杖的真實性，並驗證 hello 語彙基元 tooprove 中的幾個宣告其有效性。 hello 宣告驗證的應用程式而異案例的需求，但您的應用程式必須執行一些[常見的宣告驗證](#validating-tokens)在每個案例。

我們提供 hello 有關中的識別碼權杖中宣告的完整詳細資料 hello 下列各節，此外 tooa 範例 ID 語彙基元。 請注意，識別碼權杖中的宣告不會以特定順序傳回。 此外，隨時都可以在識別碼權杖中導入新的宣告。 導入新宣告時，您的應用程式應該不會發生中斷的現象。 hello 下列清單包含您的應用程式目前可以可靠地解譯的 hello 宣告。 您可以找到更多詳細資料中 hello [OpenID Connect 規格](http://openid.net/specs/openid-connect-core-1_0.html)。

#### <a name="sample-id-token"></a>範例 ID 權杖
```
eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsImtpZCI6Ik1uQ19WWmNBVGZNNXBPWWlKSE1iYTlnb0VLWSJ9.eyJhdWQiOiI2NzMxZGU3Ni0xNGE2LTQ5YWUtOTdiYy02ZWJhNjkxNDM5MWUiLCJpc3MiOiJodHRwczovL2xvZ2luLm1pY3Jvc29mdG9ubGluZS5jb20vYjk0MTk4MTgtMDlhZi00OWMyLWIwYzMtNjUzYWRjMWYzNzZlL3YyLjAiLCJpYXQiOjE0NTIyODUzMzEsIm5iZiI6MTQ1MjI4NTMzMSwiZXhwIjoxNDUyMjg5MjMxLCJuYW1lIjoiQmFiZSBSdXRoIiwibm9uY2UiOiIxMjM0NSIsIm9pZCI6ImExZGJkZGU4LWU0ZjktNDU3MS1hZDkzLTMwNTllMzc1MGQyMyIsInByZWZlcnJlZF91c2VybmFtZSI6InRoZWdyZWF0YmFtYmlub0BueXkub25taWNyb3NvZnQuY29tIiwic3ViIjoiTUY0Zi1nZ1dNRWppMTJLeW5KVU5RWnBoYVVUdkxjUXVnNWpkRjJubDAxUSIsInRpZCI6ImI5NDE5ODE4LTA5YWYtNDljMi1iMGMzLTY1M2FkYzFmMzc2ZSIsInZlciI6IjIuMCJ9.p_rYdrtJ1oCmgDBggNHB9O38KTnLCMGbMDODdirdmZbmJcTHiZDdtTc-hguu3krhbtOsoYM2HJeZM3Wsbp_YcfSKDY--X_NobMNsxbT7bqZHxDnA2jTMyrmt5v2EKUnEeVtSiJXyO3JWUq9R0dO-m4o9_8jGP6zHtR62zLaotTBYHmgeKpZgTFB9WtUq8DVdyMn_HSvQEfz-LWqckbcTwM_9RNKoGRVk38KChVJo4z5LkksYRarDo8QgQ7xEKmYmPvRr_I7gvM2bmlZQds2OeqWLB1NSNbFZqyFOCgYn3bAQ-nEQSKwBaA36jYGPOVG2r2Qv1uKcpSOxzxaQybzYpQ
```

> [!TIP]
> 作法，tooinspect hello 宣告在 hello 範例識別碼權杖中，貼上到 hello 範例識別碼權杖[calebb.net](http://calebb.net/)。
>
>

#### <a name="claims-in-id-tokens"></a>ID 權杖中的宣告
| 名稱 | 宣告 | 範例值 | 說明 |
| --- | --- | --- | --- |
| audience |`aud` |`6731de76-14a6-49ae-97bc-6eba6914391e` |識別 hello 預期收件者的 hello 語彙基元。 在 ID 權杖 hello 對象會是指派 tooyour hello Microsoft 應用程式註冊入口網站中的應用程式的應用程式的應用程式識別碼。 您的應用程式應該驗證此值，並拒絕 hello 語彙基元，如果 hello 值不相符。 |
| 簽發者 |`iss` |`https://login.microsoftonline.com/b9419818-09af-49c2-b0c3-653adc1f376e/v2.0 ` |識別 hello 安全性權杖服務 (STS) 建構，並傳回 hello 語彙基元和 hello Azure AD 租用戶中的 hello 驗證使用者。 您的應用程式應該先驗證 hello issuer 宣告 hello 語彙基元的 tooensure 來自 hello v2.0 端點。 它也應該使用的登入 toohello 應用程式的租用戶 hello 宣告 toorestrict hello 集合 hello GUID 部分。 hello 指出該 hello 使用者的 GUID 就是取用者的使用者帳戶是在 microsoft `9188040d-6c67-4c5b-b112-36a304b66dad`。 |
| 簽發時間 |`iat` |`1452285331` |hello 的 hello 權杖的發出時間，表示在 epoch 時間。 |
| 到期時間 |`exp` |`1452289231` |hello 時間在哪一個 hello 權杖就會變成無效，表示在 epoch 時間。 您的應用程式應該使用此宣告 tooverify hello 的有效性 hello 權杖存留期。 |
| 生效時間 |`nbf` |`1452285331` |hello 的 hello 權杖生效的時間，表示在 epoch 時間。 它是通常為 hello 發行時間 hello 相同。 您的應用程式應該使用此宣告 tooverify hello 的有效性 hello 權杖存留期。 |
| 版本 |`ver` |`2.0` |hello hello 識別碼權杖，Azure AD 所定義的版本。 Hello v2.0 端點，hello 值是`2.0`。 |
| 租用戶識別碼 |`tid` |`b9419818-09af-49c2-b0c3-653adc1f376e` |代表 hello 使用者的 hello Azure AD 租用戶的 GUID 是從。 公司及學校帳戶 hello GUID 是組織的所屬 hello hello 使用者識別碼 hello 固定租用戶。 Hello 值就是個人的帳戶， `9188040d-6c67-4c5b-b112-36a304b66dad`。 hello`profile`範圍無須在順序 tooreceive 此宣告。 |
| 代碼雜湊 |`c_hash` |`SGCPtt01wxwfgnYZy2VJtQ` |hello 的 ID 語彙基元發行使用 OAuth 2.0 授權碼時，才 hello 程式碼的雜湊一併併入 ID 語彙基元。 它可以是使用的 toovalidate hello 真實性的授權碼。 如需有關執行此驗證的詳細資訊，請參閱 hello [OpenID Connect 規格](http://openid.net/specs/openid-connect-core-1_0.html)。 |
| 存取權杖雜湊 |`at_hash` |`SGCPtt01wxwfgnYZy2VJtQ` |hello 的 ID 語彙基元發出以 OAuth 2.0 存取權杖時，才 hello 存取語彙基元雜湊一併併入 ID 語彙基元。 它可以是使用的 toovalidate hello 真實性的存取權杖。 如需有關執行此驗證的詳細資訊，請參閱 hello [OpenID Connect 規格](http://openid.net/specs/openid-connect-core-1_0.html)。 |
| nonce |`nonce` |`12345` |hello nonce 是一種策略的緩和權杖重新執行攻擊。 您的應用程式可以利用 hello 授權要求中指定的 nonce`nonce`查詢參數。 您提供 hello 要求中的 hello 值，就會發出在 hello ID 語彙基元的`nonce`未經修改的宣告。 您的應用程式可以確認它指定 hello 要求時，其使用特定的 ID 語彙基元關聯 hello 應用程式工作階段的 hello 值 hello 值。 您的應用程式應該執行這項驗證 hello 識別碼權杖驗證程序期間。 |
| 名稱 |`name` |`Babe Ruth` |hello 名稱宣告會提供人類看得懂的值，識別 hello 權杖主體的 hello。 hello 值不保證唯一的它是可變動的而且是 toobe 設計 toobe 只用於顯示用途。 hello`profile`範圍無須在順序 tooreceive 此宣告。 |
| 電子郵件 |`email` |`thegreatbambino@nyy.onmicrosoft.com` |如果有的話，hello 使用者帳戶，與相關聯的 hello 主要電子郵件地址。 其值是可變動的，並且可能隨著時間改變。 hello`email`範圍無須在順序 tooreceive 此宣告。 |
| 慣用的使用者名稱 |`preferred_username` |`thegreatbambino@nyy.onmicrosoft.com` |hello 代表 hello v2.0 端點中的 hello 使用者的主要使用者名稱。 它可以是電子郵件地址、電話號碼或未指定格式的一般使用者名稱。 其值是可變動的，並且可能隨著時間改變。 hello`profile`範圍無須在順序 tooreceive 此宣告。 |
| 主旨 |`sub` |`MF4f-ggWMEji12KynJUNQZphaUTvLcQug5jdF2nl01Q` | hello 主體的 hello 權杖判斷提示的相關資訊，例如 hello 使用者應用程式。 這個值不可變，而且無法重新指派或重複使用。 它可以使用的 tooperform 授權檢查，例如當 hello 語彙基元是使用的 tooaccess 資源，並可用來當做資料庫資料表中的索引鍵。 因為 hello 主體一律存在於 hello 語彙基元的 Azure AD 會發出，我們建議您在一般用途的授權系統中使用此值。 hello 主旨，不過，這會為成對識別碼-它是唯一的 tooa 特定應用程式識別碼。  因此，如果單一使用者登入兩個不同的應用程式使用兩個不同的用戶端識別碼，這些應用程式會收到 hello 主體宣告的兩個不同的值。  視您的架構和隱私權需求而定，這不一定是您想要的。 |
| 物件識別碼 |`oid` |`a1dbdde8-e4f9-4571-ad93-3059e3750d23` | hello 程式物件的不可變識別碼 hello Microsoft 身分識別系統中，在此情況下，使用者帳戶。  它也可以使用的 tooperform 授權檢查安全無虞地並做為資料庫資料表中的索引鍵。 這個識別碼可唯一識別 hello 使用者，跨應用程式-兩個不同的應用程式登入相同的使用者將會收到的 hello hello 相同值在 hello`oid`宣告。  這表示 tooMicrosoft 線上服務，例如 hello Microsoft Graph 進行查詢時，可以使用它。  hello Microsoft Graph 會傳回這個識別碼，表示為 hello`id`屬性指定的使用者帳戶。  因為 hello`oid`可讓多個應用程式 toocorrelate 使用者 hello`profile`範圍無須在順序 tooreceive 此宣告。 請注意，是否單一使用者存在於多個租用戶，hello 使用者，將會包含每個租用戶中是不同的物件識別碼-視為不同的帳戶，即使 hello 使用者登入每個帳戶與 hello 相同的認證。 |

### <a name="access-tokens"></a>存取權杖
目前，可以取用 hello v2.0 端點所發出的存取權杖，只供 Microsoft 服務。 您的應用程式應該不需要 tooperform 任何驗證或檢查存取權杖的任何 hello 目前支援的案例。 您可以將存取權杖視為完全不透明。 它們是您的應用程式，可以在 HTTP 要求中傳遞 tooMicrosoft 只是字串。

在未來，hello v2.0 附近的 hello 端點將介紹您應用程式 tooreceive 存取權杖的 hello 能力，從其他用戶端。 在這段時間，將會更新這個參考主題中的 hello 資訊 hello 資訊，您需要您的應用程式 tooperform 存取權杖的驗證和其他類似的工作。

當您從 hello v2.0 端點要求存取權杖時，hello v2.0 端點也會傳回應用程式 toouse hello 存取權杖的相關中繼資料。 這項資訊包括 hello hello 存取權杖和 hello 範圍，它是有效的到期時間。 您的應用程式會使用此中繼資料 tooperform 智慧型權杖快取存取而不需要自行 tooparse 開啟 hello 存取權杖。

### <a name="refresh-tokens"></a>重新整理權杖
重新整理權杖是安全性權杖，您的應用程式可以使用 tooget 新存取語彙基元中 OAuth 2.0 流程。 您的應用程式可以使用代表使用者重新整理語彙基元 tooachieve 長期存取 tooresources，而不需要與 hello 使用者互動。

重新整理權杖屬於多資源權杖。 一個資源的權杖要求期間收到重新整理權杖可用來兌換存取權杖 tooa 完全不同的資源。

tooreceive 重新整理權杖的回應中的您的應用程式必須要求，以及被授與 hello`offline_acesss`範圍。 深入了解 hello toolearn`offline_access`範圍，請參閱 hello[同意和範圍](active-directory-v2-scopes.md)發行項。

重新整理權杖，而且永遠會為，完全不透明 tooyour 應用程式。 它們所發行的 hello Azure AD v2.0 端點和可只檢查及 hello v2.0 端點所解譯。 它們是長時間執行，但您的應用程式應該不會寫入任何時段將持續重新整理權杖的 tooexpect。 重新整理權杖可能會因為各種原因而隨時失效。 只有您的應用程式 tooknow 如果重新整理權杖是有效的方式為 tooattempt tooredeem hello 它藉由權杖要求 toohello v2.0 端點。

當您兌換新存取權杖的重新整理語彙基元 (如果您的應用程式已被授與 hello 和`offline_access`範圍)，hello 權杖回應中收到新的重新整理權杖。 將 hello 剛發行的重新整理語彙基元，tooreplace hello 使用儲存在 hello 要求。 這可保證您的重新整理權杖儘可能長期保持有效。

## <a name="validating-tokens"></a>驗證權杖
目前，hello 只應該在需要您的應用程式的權杖驗證 tooperform 正在驗證 ID 語彙基元。 toovalidate ID 權杖，您的應用程式應該先驗證 hello 識別碼權杖中的兩個 hello ID 權杖簽章與 hello 宣告。

<!-- TODO: Link -->
Microsoft 提供程式庫和程式碼範例，示範您如何 tooeasily 處理權杖驗證。 在 hello 下一步 區段中，我們將描述 hello 基礎程序。 此外，也有數個協力廠商開放原始碼程式庫可用於 JWT 驗證。 幾乎每個平台和語言都有至少一個程式庫選項。

### <a name="validate-hello-signature"></a>驗證 hello 簽章
JWT 包含三個區段，並以 hello 分隔`.`字元。 hello 第一個區段稱為 hello*標頭*，hello 第二個區段為 hello*主體*，和 hello 第三個區段為 hello*簽章*。 hello 簽章區段，讓它可以信任的應用程式，可以是 hello 的 ID 語彙基元使用的 toovalidate hello 真確性。

ID 權杖是經由業界標準非對稱式加密演算法 (例如 RSA 256) 進行簽署。 hello 的標頭 hello 的 ID 語彙基元擁有 hello 索引鍵的相關資訊，並使用 toosign hello token 的加密方法。 例如：

```
{
  "typ": "JWT",
  "alg": "RS256",
  "kid": "MnC_VZcATfM5pOYiJHMba9goEKY"
}
```

hello`alg`宣告表示已使用的 toosign hello 語彙基元的 hello 演算法。 hello`kid`宣告表示已使用的 toosign hello 語彙基元的 hello 公用金鑰。

在任何時間，hello v2.0 端點可能會使用任何一組特定的公開-私密金鑰組簽署 ID 語彙基元。 hello v2.0 端點定期旋轉 hello 可能索引鍵集中，因此您的應用程式應撰寫的 toohandle 這些金鑰會自動變更。 合理的頻率 toocheck 更新 toohello 公開金鑰 hello v2.0 端點所使用的是每隔 24 小時。

您可以取得簽章使用 hello OpenID Connect 中繼資料文件位於需要 toovalidate hello 簽章的金鑰資料的 hello:

```
https://login.microsoftonline.com/common/v2.0/.well-known/openid-configuration
```

> [!TIP]
> 在瀏覽器中的 hello URL 再試一次 ！
>
>

此中繼資料文件是 hello 的資訊的有數項有用，例如 hello 位置的不同端點的驗證所需的 OpenID Connect 的 JSON 物件。  hello 文件也包含*jwks_uri*，讓 hello 組之公開金鑰的 hello 位置使用 toosign 語彙基元。 位於 hello jwks_uri hello JSON 文件的所有 hello 公用金鑰資訊正在使用中。 您的應用程式可以使用 hello`kid`宣告中的這份文件中的公開金鑰已使用的 toosign hello JWT 標頭 tooselect 語彙基元。 然後會使用正確的公用金鑰 hello 和 hello 指定的演算法執行簽章驗證。

執行簽章驗證是 hello 範圍外的這份文件。 許多開放原始碼程式庫會提供 toohelp 您與此。

### <a name="validate-hello-claims"></a>驗證 hello 宣告
當您的應用程式收到的 ID 語彙基元，在使用者登入時，它也應該執行對 hello 宣告少數檢查 hello 的 ID 語彙基元中。 包含但不限於：

* **對象**宣告 hello 的 ID 語彙基元的 tooverify 已預定的 toobe 指定 tooyour 應用程式
* **不能早**和**到期時間**宣告 hello 的 ID 語彙基元的 tooverify 尚未過期。
* **簽發者**宣告 hello 語彙基元的 tooverify hello v2.0 端點所發出 tooyour 應用程式
* **Nonce** - 作為權杖重新執行攻擊的緩和措施

宣告驗證，您的應用程式應執行的完整清單，請參閱 hello [OpenID Connect 規格](http://openid.net/specs/openid-connect-core-1_0.html#IDTokenValidation)。

這些宣告的 hello 預期值的詳細資料會包含在 hello [ID 權杖](# ID tokens)> 一節。

## <a name="token-lifetimes"></a>權杖存留期
我們提供下列僅供貴的權杖存留期的 hello。 hello 資訊可能有助於在您開發及偵錯應用程式。 您的應用程式不應該寫入 tooexpect 任何這些存留期 tooremain 常數。 權杖存留期可以而且將會隨時變更。

| 權杖 | 存留期 | 說明 |
| --- | --- | --- |
| 識別碼權杖 (工作或學校帳戶) |1 小時 |識別碼權杖的有效期通常為 1 小時。 您的 web 應用程式可以使用這個相同的存留期 toomaintain 自己的工作階段與 hello 使用者 （建議），或者您可以選擇完全不同的工作階段存留期。 如果您的應用程式需要 tooget 新的 ID 語彙基元，它需要新的登入 toomake toohello v2.0 授權端點的要求。 如果 hello 使用者擁有有效的瀏覽器工作階段與 hello v2.0 端點，hello 使用者可能不是必要的 tooenter 其認證一次。 |
| 識別碼權杖 (個人帳戶) |24 小時 |個人帳戶的識別碼權杖有效期通常為 24 小時。 您的 web 應用程式可以使用這個相同的存留期 toomaintain 自己的工作階段與 hello 使用者 （建議），或者您可以選擇完全不同的工作階段存留期。 如果您的應用程式需要 tooget 新的 ID 語彙基元，它需要新的登入 toomake toohello v2.0 授權端點的要求。 如果 hello 使用者擁有有效的瀏覽器工作階段與 hello v2.0 端點，hello 使用者可能不是必要的 tooenter 其認證一次。 |
| 存取權杖 (工作或學校帳戶) |1 小時 |以語彙基元回應 hello 語彙基元的中繼資料的一部分。 |
| 存取權杖 (個人帳戶) |1 小時 |以語彙基元回應 hello 語彙基元的中繼資料的一部分。 可以為代表個人帳戶簽發的存取權杖設定不同的存留期，但通常是一小時。 |
| 重新整理權杖 (工作或學校帳戶) |向上 too14 天 |單一重新整理權杖的有效期最多 14 天。 不過，hello 重新整理權杖可能會變成無效隨時基於各種原因，因此您的應用程式應該繼續 tootry toouse 重新整理權杖，直到它失敗，或直到您的應用程式會將它取代新的重新整理權杖。 重新整理權杖也會變成無效，如果已經 90 天 hello 使用者輸入其認證。 |
| 重新整理權杖 (個人帳戶) |Too1 年 |單一重新整理權杖的有效期最多 1 年。 不過，hello 重新整理權杖可能在任何時間，因為各種原因而變成無效，因此您的應用程式應該繼續 tootry toouse 重新整理權杖，直到它失敗。 |
| 授權碼 (工作或學校帳戶) |10 分鐘 |授權碼刻意存留較短，而且應該立即贖回存取權杖和重新整理權杖時收到 hello 語彙基元。 |
| 授權碼 (個人帳戶) |5 分鐘 |授權碼刻意存留較短，而且應該立即贖回存取權杖和重新整理權杖時收到 hello 語彙基元。 代表個人帳戶簽發的授權碼是供單次使用。 |
