---
title: "aaaLearn 有關 hello 不同權杖與宣告類型，Azure AD 支援 |Microsoft 文件"
description: "了解和評估 hello SAML 2.0 和 JSON Web Token (JWT) 權杖發行的 Azure Active Directory (AAD) 中的 hello 宣告指南"
documentationcenter: na
author: dstrockis
services: active-directory
manager: mbaldwin
editor: 
ms.assetid: 166aa18e-1746-4c5e-b382-68338af921e2
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/08/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: c512894476613e94d86a994c32a8459d6cf00fbd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-token-reference"></a>Azure AD 權杖參考
Azure Active Directory (Azure AD) 發出的幾種類型的安全性權杖中的每個驗證流程的 hello 處理。 本文件說明 hello 格式、 安全性的特性，以及每種類型的語彙基元的內容。

## <a name="types-of-tokens"></a>權杖的類型
Azure AD 支援 hello [OAuth 2.0 授權通訊協定](active-directory-protocols-oauth-code.md)，其使用 access_tokens 和 refresh_tokens。  它也支援驗證和登入透過[OpenID Connect](active-directory-protocols-openid-connect-code.md)，其中導入了第三種類型的語彙基元，hello id_token。  每個權杖都是以「持有人權杖」表示。

承載權杖是輕巧型的安全性權杖會授與 hello"bearer"存取 tooa 受保護資源。 就這個意義而言，hello"bearer"是指可出示 hello 語彙基元任何一方。 中就需要使用 Azure AD 的驗證順序 tooreceive 持有人權杖，還是必須採取步驟 toosecure hello 語彙基元，tooprevent 攔截非預期的合作對象。 因為持有者權杖沒有使用這些內建機制 tooprevent 未經授權的合作對象，它們必須在安全的通道，例如傳輸層安全性 (HTTPS) 傳輸。 如果持有人權杖傳送 hello 清除中時，攔截 hello 攻擊可以是使用的 tooacquire hello 語彙基元，並取得未經授權的存取 tooa 受保護的資源。 hello 儲存或快取持有者權杖供以後使用時，適用相同的安全性原則。 務必確定您的應用程式以安全的方式傳輸和儲存持有人權杖。 關於持有者權杖的其他安全性考量，請參閱 [RFC 6750 第 5 節](http://tools.ietf.org/html/rfc6750)。

許多 hello Azure AD 所簽發的權杖會實作為 JSON Web 語彙基元或 Jwt。  JWT 是一種精簡的 URL 安全方法，可在兩方之間傳輸資訊。  Jwt 中所包含的 hello 資訊稱為 「 宣告 」 或判斷提示的資訊關於 hello 承載和 hello 權杖的主體。  在 Jwt 的 hello 宣告會被編碼和傳輸序列化的 JSON 物件。  因為 hello Azure AD 所簽發的 Jwt 簽章，但不是會加密，就可以輕鬆地檢查 JWT hello 內容，以進行偵錯。  有數個工具可以進行這項操作，例如 [jwt.calebb.net](http://jwt.calebb.net)。 如需有關 Jwt 的詳細資訊，請參閱 toohello [JWT 規格](http://self-issued.info/docs/draft-ietf-oauth-json-web-token.html)。

## <a name="idtokens"></a>Id_tokens
Id_tokens 是您的應用程式使用 [OpenID Connect](active-directory-protocols-openid-connect-code.md) 執行驗證時收到的一種登入安全性權杖形式。  表示為[Jwt](#types-of-tokens)，而且包含可用於 hello 使用者登入您的應用程式的宣告。  可用於 hello 宣告 id_token 做適當通常用來顯示帳戶資訊，或在應用程式中進行存取控制決定。

Id_token 已簽署，但這次不加密。  當您的應用程式收到 id_token 時，它必須[驗證 hello 簽章](#validating-tokens)tooprove hello 權杖的真實性，並驗證 hello 語彙基元 tooprove 中的幾個宣告其有效性。  hello 宣告驗證的應用程式而異案例的需求，但有一些[常見的宣告驗證](#validating-tokens)您的應用程式必須在每個案例中執行。

Hello id_tokens 宣告，以及範例 id_token 遵循節的資訊，請參閱。  請注意，在 id_tokens hello 宣告不會傳回任何特定順序。  此外，新的宣告可以隨時引進 id_token 中 - 您的應用程式不會在引進新的宣告時中斷。  hello 下列清單包含您的應用程式可以可靠地解譯在 hello 撰寫本文時的 hello 宣告。  如果需要更多詳細資料位於 hello [OpenID Connect 規格](http://openid.net/specs/openid-connect-core-1_0.html)。

#### <a name="sample-idtoken"></a>範例 id_token
```
eyJ0eXAiOiJKV1QiLCJhbGciOiJub25lIn0.eyJhdWQiOiIyZDRkMTFhMi1mODE0LTQ2YTctODkwYS0yNzRhNzJhNzMwOWUiLCJpc3MiOiJodHRwczovL3N0cy53aW5kb3dzLm5ldC83ZmU4MTQ0Ny1kYTU3LTQzODUtYmVjYi02ZGU1N2YyMTQ3N2UvIiwiaWF0IjoxMzg4NDQwODYzLCJuYmYiOjEzODg0NDA4NjMsImV4cCI6MTM4ODQ0NDc2MywidmVyIjoiMS4wIiwidGlkIjoiN2ZlODE0NDctZGE1Ny00Mzg1LWJlY2ItNmRlNTdmMjE0NzdlIiwib2lkIjoiNjgzODlhZTItNjJmYS00YjE4LTkxZmUtNTNkZDEwOWQ3NGY1IiwidXBuIjoiZnJhbmttQGNvbnRvc28uY29tIiwidW5pcXVlX25hbWUiOiJmcmFua21AY29udG9zby5jb20iLCJzdWIiOiJKV3ZZZENXUGhobHBTMVpzZjd5WVV4U2hVd3RVbTV5elBtd18talgzZkhZIiwiZmFtaWx5X25hbWUiOiJNaWxsZXIiLCJnaXZlbl9uYW1lIjoiRnJhbmsifQ.
```

> [!TIP]
> 練習中，請再試一次檢查由將其貼在 hello 範例 id_token hello 宣告[calebb.net](http://jwt.calebb.net)。
> 
> 

#### <a name="claims-in-idtokens"></a>id_tokens 中的宣告
> [!div class="mx-codeBreakAll"]
| JWT 宣告 | Name | 說明 |
| --- | --- | --- |
| `appid` |應用程式識別碼 |識別正在使用 hello 語彙基元 tooaccess 資源的 hello 應用程式。 hello 應用程式可以做為本身，或代表使用者。 hello 應用程式識別碼通常代表應用程式物件，但它也可以在 Azure AD 中代表的服務主體物件。 <br><br> **範例 JWT 值**： <br> `"appid":"15CB020F-3984-482A-864D-1D92265E8268"` |
| `aud` |對象 |hello 預期收件者的 hello 語彙基元。 收到 hello 語彙基元的 hello 應用程式必須確認 hello 適用對象值正確無誤，並拒絕任何適用於不同對象的權杖。 <br><br> **範例 SAML 值**： <br> `<AudienceRestriction>`<br>`<Audience>`<br>`https://contoso.com`<br>`</Audience>`<br>`</AudienceRestriction>` <br><br> **範例 JWT 值**： <br> `"aud":"https://contoso.com"` |
| `appidacr` |應用程式驗證內容類別參考 |指出 hello 用戶端的驗證方式。 為公用的用戶端 hello 值為 0。 如果使用用戶端識別碼和用戶端密碼，hello 值為 1。 <br><br> **範例 JWT 值**： <br> `"appidacr": "0"` |
| `acr` |驗證內容類別參考 |表示 hello 主體的驗證方式，為相對於的 toohello hello 應用程式驗證內容類別參考宣告中的用戶端。 值為"0"表示 hello 使用者驗證不符合 ISO/IEC 29115 的 hello 需求。 <br><br> **範例 JWT 值**： <br> `"acr": "0"` |
| 驗證即刻 |記錄 hello 當驗證發生日期和時間。 <br><br> **範例 SAML 值**： <br> `<AuthnStatement AuthnInstant="2011-12-29T05:35:22.000Z">` | |
| `amr` |驗證方法 |識別 hello hello 權杖主體的驗證方式。 <br><br> **範例 SAML 值**： <br> `<AuthnContextClassRef>`<br>`http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod/password`<br>`</AuthnContextClassRef>` <br><br> **範例 JWT 值**：`“amr”: ["pwd"]` |
| `given_name` |名字 |Hello Azure AD 使用者物件上設定為提供 hello 第一次或 「"指定的 hello 使用者名稱。 <br><br> **範例 SAML 值**： <br> `<Attribute Name=”http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname”>`<br>`<AttributeValue>Frank<AttributeValue>` <br><br> **範例 JWT 值**： <br> `"given_name": "Frank"` |
| `groups` |群組 |提供物件識別碼，以代表 hello 主體的群組成員資格。 這些值是唯一 （請參閱物件識別碼），可安全地用於管理存取權，例如強制執行授權 tooaccess 資源。 針對每個應用程式，透過 hello hello 應用程式資訊清單的"groupMembershipClaims"屬性未設定 hello hello 群組宣告中包含的群組。 Null 值將會排除所有群組，"SecurityGroup" 值只會包含 Active Directory 安全性群組成員資格，而 "All" 值將會包含安全性群組和 Office 365 通訊群組清單。 <br><br> **範例 SAML 值**： <br> `<Attribute Name="http://schemas.microsoft.com/ws/2008/06/identity/claims/groups">`<br>`<AttributeValue>07dd8a60-bf6d-4e17-8844-230b77145381</AttributeValue>` <br><br> **範例 JWT 值**： <br> `“groups”: ["0e129f5b-6b0a-4944-982d-f776045632af", … ]` |
| `idp` |識別提供者 |記錄 hello 驗證 hello hello 權杖主體的身分識別提供者。 這個值會是相同 toohello hello 除非 hello 使用者帳戶位於不同的租用戶比 hello 簽發者的宣告簽發者值。 <br><br> **範例 SAML 值**： <br> `<Attribute Name=” http://schemas.microsoft.com/identity/claims/identityprovider”>`<br>`<AttributeValue>https://sts.windows.net/cbb1a5ac-f33b-45fa-9bf5-f37db0fed422/<AttributeValue>` <br><br> **範例 JWT 值**： <br> `"idp":”https://sts.windows.net/cbb1a5ac-f33b-45fa-9bf5-f37db0fed422/”` |
| `iat` |IssuedAt |會儲存哪些 hello 權杖的發出 hello 時間。 它通常是使用的 toomeasure 權杖的有效性。 <br><br> **範例 SAML 值**： <br> `<Assertion ID="_d5ec7a9b-8d8f-4b44-8c94-9812612142be" IssueInstant="2014-01-06T20:20:23.085Z" Version="2.0" xmlns="urn:oasis:names:tc:SAML:2.0:assertion">` <br><br> **範例 JWT 值**： <br> `"iat": 1390234181` |
| `iss` |簽發者 |識別 hello 安全性權杖服務 (STS) 的建構，並且傳回 hello 語彙基元。 在 Azure AD 傳回的 hello 語彙基元，hello 簽發者會是 sts.windows.net。 hello hello Issuer 宣告值中的 GUID 是 hello hello Azure AD 目錄租用戶識別碼。 hello 租用戶識別碼是不變且可靠的 hello 目錄識別碼。 <br><br> **範例 SAML 值**： <br> `<Issuer>https://sts.windows.net/cbb1a5ac-f33b-45fa-9bf5-f37db0fed422/</Issuer>` <br><br> **範例 JWT 值**： <br>  `"iss":”https://sts.windows.net/cbb1a5ac-f33b-45fa-9bf5-f37db0fed422/”` |
| `family_name` |姓氏 |Hello Azure AD 使用者物件中所定義，請提供 hello 姓氏、 姓氏或 hello 使用者的姓氏。 <br><br> **範例 SAML 值**： <br> `<Attribute Name=” http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname”>`<br>`<AttributeValue>Miller<AttributeValue>` <br><br> **範例 JWT 值**： <br> `"family_name": "Miller"` |
| `unique_name` |名稱 |提供人類可讀取的值，以識別 hello 主體 hello 語彙基元。 此值並不一定都 toobe 租用戶內的唯一是設計的 toobe 只用於顯示用途。 <br><br> **範例 SAML 值**： <br> `<Attribute Name=”http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name”>`<br>`<AttributeValue>frankm@contoso.com<AttributeValue>` <br><br> **範例 JWT 值**： <br> `"unique_name": "frankm@contoso.com"` |
| `oid` |物件識別碼 |包含 Azure AD 中物件的唯一識別碼。 這個值不可變，而且無法重新指派或重複使用。 使用查詢 tooAzure AD 中的 hello 物件識別碼 tooidentify 物件。 <br><br> **範例 SAML 值**： <br> `<Attribute Name="http://schemas.microsoft.com/identity/claims/objectidentifier">`<br>`<AttributeValue>528b2ac2-aa9c-45e1-88d4-959b53bc7dd0<AttributeValue>` <br><br> **範例 JWT 值**： <br> `"oid":"528b2ac2-aa9c-45e1-88d4-959b53bc7dd0"` |
| `roles` |角色 |代表 hello 主體的所有應用程式角色已獲得同時以直接或間接透過群組成員資格，而且可以是使用以角色為基礎的 tooenforce 存取控制。 應用程式角色會定義以每個應用程式為基礎，透過 hello `appRoles` hello 應用程式資訊清單的屬性。 hello`value`每個應用程式角色的內容會出現在 hello 角色宣告中的 hello 值。 <br><br> **範例 SAML 值**： <br> `<Attribute Name="http://schemas.microsoft.com/ws/2008/06/identity/claims/role">`<br>`<AttributeValue>Admin</AttributeValue>` <br><br> **範例 JWT 值**： <br> `“roles”: ["Admin", … ]` |
| `scp` |Scope |指出 hello 模擬權限授與 toohello 用戶端應用程式。 hello 預設權限是`user_impersonation`。 hello 的 hello 保護資源的擁有者可以在 Azure AD 中註冊其他的值。 <br><br> **範例 JWT 值**： <br> `"scp": "user_impersonation"` |
| `sub` |主旨 |識別哪些 hello 權杖判斷提示的相關資訊，例如應用程式使用者 hello hello 主體。 此值不可變且無法重新指派或重複使用，所以它可以是使用的 tooperform 授權檢查安全。 因為 hello 主體一律存在於 hello 語彙基元 hello Azure AD 發出，我們建議您在一般用途的授權系統中使用此值。 <br> `SubjectConfirmation` 不是宣告。 本主題描述如何確認已 hello 權杖主體的 hello。 `Bearer`表示該 hello 主旨確認 hello 權杖的持有者。 <br><br> **範例 SAML 值**： <br> `<Subject>`<br>`<NameID>S40rgb3XjhFTv6EQTETkEzcgVmToHKRkZUIsJlmLdVc</NameID>`<br>`<SubjectConfirmation Method="urn:oasis:names:tc:SAML:2.0:cm:bearer" />`<br>`</Subject>` <br><br> **範例 JWT 值**： <br> `"sub":"92d0312b-26b9-4887-a338-7b00fb3c5eab"` |
| `tid` |租用戶識別碼 |識別發出 hello 語彙基元的 hello 目錄租用戶的不可變、 不可重複使用識別碼。 您可以使用此值 tooaccess 租用戶專屬目錄資源的多租用戶應用程式中。 例如，您可以使用此值 tooidentify hello 租用戶中呼叫 toohello Graph API。 <br><br> **範例 SAML 值**： <br> `<Attribute Name=”http://schemas.microsoft.com/identity/claims/tenantid”>`<br>`<AttributeValue>cbb1a5ac-f33b-45fa-9bf5-f37db0fed422<AttributeValue>` <br><br> **範例 JWT 值**： <br> `"tid":"cbb1a5ac-f33b-45fa-9bf5-f37db0fed422"` |
| `nbf`、`exp` |權杖存留期 |定義權杖的有效 hello 時間間隔。 驗證 hello 權杖的 hello 服務應該確認該 hello 目前的日期是在 hello 權杖存留期，否則應該拒絕 hello 語彙基元。 hello 服務可能會允許總時鐘時間 （「 時間偏差 」） 的任何差異超過 hello 權杖存留期範圍 tooaccount toofive 分鐘之間 Azure AD 與 hello 服務。 <br><br> **範例 SAML 值**： <br> `<Conditions`<br>`NotBefore="2013-03-18T21:32:51.261Z"`<br>`NotOnOrAfter="2013-03-18T22:32:51.261Z"`<br>`>` <br><br> **範例 JWT 值**： <br> `"nbf":1363289634, "exp":1363293234` |
| `upn` |使用者主體名稱 |存放區 hello hello 使用者主體的使用者名稱。<br><br> **範例 JWT 值**： <br> `"upn": frankm@contoso.com` |
| `ver` |版本 |儲存 hello 語彙基元 hello 版本號碼。 <br><br> **範例 JWT 值**： <br> `"ver": "1.0"` |

## <a name="access-tokens"></a>存取權杖
驗證成功後，Azure AD 會傳回存取權杖，它可以是使用的 tooaccess 受保護的資源。 base 64 編碼的 JSON Web Token (JWT)，並且可以檢查其內容，執行透過解碼器 hello 存取權杖。

如果您的應用程式只*使用*存取權杖 tooget 存取 tooAPIs，您可以 （而且也應該） 將存取權杖視為完全不透明-它們是您的應用程式可以在 HTTP 要求中傳遞 tooresources 這只是字串。

當您要求存取權杖時，Azure AD 也會傳回有關 hello 存取權杖，供您的應用程式使用一些中繼資料。  這項資訊包括 hello hello 存取權杖和 hello 範圍，它是有效的到期時間。  這可讓您的應用程式 tooperform 智慧型存取權杖快取而不需要 tooparse 開啟本身 hello 存取權杖。

如果您的應用程式是使用 HTTP 要求中需要存取權杖的 Azure AD 保護的 API，然後您應該執行驗證，並檢查您收到 hello 語彙基元。 您的應用程式應該執行使用 tooaccess 資源之前，先驗證 hello 存取權杖。 如需有關驗證的詳細資訊，請參閱[驗證權杖](#validating-tokens)。  
如需如何 toodo 這與.NET，請參閱詳細資料[保護 Web 應用程式開發介面使用從 Azure AD 的持有者權杖](active-directory-devquickstarts-webapi-dotnet.md)。

## <a name="refresh-tokens"></a>重新整理權杖

重新整理權杖是安全性權杖，您的應用程式可以使用 tooacquire 新存取語彙基元中 OAuth 2.0 流程。  它可以代表使用者允許您的應用程式 tooachieve 長期存取 tooresources 而不需要由 hello 使用者互動。

重新整理權杖屬於多資源權杖。  這是重新整理權杖收到權杖要求期間的存取權杖 tooa 完全不同的資源，可用來兌換一個資源的 toosay。 toodo 如此，組 hello `resource` hello 要求 toohello 中的參數的目標資源。

重新整理權杖是完全不透明 tooyour 應用程式。 它們是長時間執行，但您的應用程式應該不會寫入任何時段將持續重新整理權杖的 tooexpect。  重新整理權杖可能會因為各種原因而隨時失效。  只有您的應用程式 tooknow 如果重新整理權杖是有效的方式為 tooattempt tooredeem hello 它藉由權杖要求 tooAzure AD 權杖端點。

當您兌換新存取權杖重新整理權杖時，您會收到新的重新整理權杖 hello 權杖回應中。  您應該儲存 hello 剛發行的重新整理權杖，取代 hello hello 要求中使用。  這將保證您的重新整理權杖盡可能長期保持有效。

## <a name="validating-tokens"></a>驗證權杖

順序 toovalidate id_token 或 access_token，在您的應用程式應該先驗證這兩個 hello 權杖的簽章與 hello 宣告。 順序 toovalidate 存取語彙基元，在您的應用程式也應該驗證 hello 簽發者、 觀眾 hello 和 hello 簽署權杖。 這些需要 toobe 驗證 hello OpenID 探索文件中的 hello 值。 例如，hello 租用戶獨立 hello 文件的版本是位於[https://login.microsoftonline.com/common/.well-known/openid-configuration](https://login.microsoftonline.com/common/.well-known/openid-configuration)。 Azure AD 中介軟體已驗證存取權杖的內建功能，您可以瀏覽我們[範例](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-code-samples)hello 選擇語言的其中一個 toofind。 如需有關如何 tooexplicitly 驗證 JWT 權杖中的詳細資訊，請參閱 hello[手動 JWT 驗證範例](https://github.com/Azure-Samples/active-directory-dotnet-webapi-manual-jwt-validation)。  

我們提供程式庫和程式碼範例，示範如何 tooeasily 處理權杖驗證-hello 下方資訊只供想 toounderstand hello 基礎程序的任何人。  另外還有多個協力廠商開放原始碼程式庫可用於 JWT 驗證 - 幾乎每個平台和語言都有至少一個選項。 如需有關 Azure AD 驗證程式庫和程式碼範例的詳細資訊，請參閱 [Azure AD 驗證程式庫](active-directory-authentication-libraries.md)。

#### <a name="validating-hello-signature"></a>驗證 hello 簽章

JWT 包含三個區段，並以 hello 分隔`.`字元。  hello 第一個區段稱為 hello**標頭**，第二個為 hello hello**主體**，和第三個為 hello hello**簽章**。  hello 簽章區段，讓它可以信任的應用程式，可以是 hello 語彙基元使用的 toovalidate hello 真確性。

Azure AD 所簽發的權杖是使用業界標準非對稱式加密演算法 (例如 RSA 256) 進行簽署。 hello hello JWT 標頭包含 hello 索引鍵的相關資訊，並使用 toosign hello token 的加密方法：

```
{
  "typ": "JWT",
  "alg": "RS256",
  "x5t": "kriMPdmBvx68skT8-mPAB3BseeA"
}
```

hello`alg`宣告表示已使用的 toosign hello 語彙基元，同時 hello 的 hello 演算法`x5t`宣告表示 hello 特定的公用金鑰是使用的 toosign hello 語彙基元。

在任何指定的時間點，Azure AD 可能會使用一組特定公開-私密金鑰組的其中一個金鑰組來簽署 id_token。 Azure AD 旋轉 hello 可能索引鍵集中，定期執行，因此您的應用程式應撰寫的 toohandle 這些金鑰會自動變更。  合理的頻率 toocheck 更新 toohello： 公開金鑰的 Azure AD 使用的是每隔 24 小時。

您可以取得簽署金鑰資料需要 toovalidate hello 簽章使用 hello OpenID Connect 中繼資料文件位於 hello:

```
https://login.microsoftonline.com/common/.well-known/openid-configuration
```

> [!TIP]
> 在瀏覽器中嘗試此 URL！
> 
> 

此中繼資料文件是 hello 的資訊的包含數項有用，例如 hello 位置各種端點所需執行 OpenID Connect 驗證的 JSON 物件。  

它也包含`jwks_uri`，讓 hello 組之公開金鑰的 hello 位置使用 toosign 語彙基元。  hello JSON 文件位於 hello`jwks_uri`包含所有 hello 公開金鑰資訊在該特定時間點的使用中。  您的應用程式可以使用 hello `kid` hello JWT 標頭 tooselect 本文件的公開金鑰已使用的 toosign 中宣告之特定 token。  然後，它可以執行 hello 正確的公用金鑰和 hello 指定的演算法所使用的簽章驗證。

執行簽章驗證 hello 範圍外的這份文件-有許多開放原始碼程式庫，可協助您執行這項操作，如有必要。

#### <a name="validating-hello-claims"></a>驗證 hello 宣告

當您的應用程式收到的權杖 （id_token 時使用者登入或在 hello HTTP 要求中的承載權杖存取權杖） 它也應該執行對 hello 宣告少數檢查 hello 權杖中。  包含但不限於：

* hello**觀眾**宣告-hello 語彙基元的 tooverify 已預定的 toobe 指定 tooyour 應用程式。
* hello**不早於**和**到期時間**宣告-hello 語彙基元的 tooverify 尚未過期。
* hello**簽發者**宣告-hello 語彙基元的 tooverify 確實由 Azure AD 發出 tooyour 應用程式。
* hello **Nonce** -toomitigate 權杖重新執行攻擊。
* 不勝枚舉...

您的應用程式應該執行的識別碼權杖的宣告驗證的完整清單，請參閱 toohello [OpenID Connect 規格](http://openid.net/specs/openid-connect-core-1_0.html#IDTokenValidation)。 Hello 預期這些宣告的值的詳細資料會包含在 hello 上述[id_token 區段](#id-tokens)> 一節。

## <a name="sample-tokens"></a>權杖範例

本節顯示 Azure AD 所傳回的 SAML 和 JWT 權杖範例。 這些範例可讓您查看內容中的 hello 宣告。

### <a name="saml-token"></a>SAML 權杖

這是典型的 SAML 權杖範例。

    <?xml version="1.0" encoding="UTF-8"?>
    <t:RequestSecurityTokenResponse xmlns:t="http://schemas.xmlsoap.org/ws/2005/02/trust">
      <t:Lifetime>
        <wsu:Created xmlns:wsu="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-utility-1.0.xsd">2014-12-24T05:15:47.060Z</wsu:Created>
        <wsu:Expires xmlns:wsu="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-utility-1.0.xsd">2014-12-24T06:15:47.060Z</wsu:Expires>
      </t:Lifetime>
      <wsp:AppliesTo xmlns:wsp="http://schemas.xmlsoap.org/ws/2004/09/policy">
        <EndpointReference xmlns="http://www.w3.org/2005/08/addressing">
          <Address>https://contoso.onmicrosoft.com/MyWebApp</Address>
        </EndpointReference>
      </wsp:AppliesTo>
      <t:RequestedSecurityToken>
        <Assertion xmlns="urn:oasis:names:tc:SAML:2.0:assertion" ID="_3ef08993-846b-41de-99df-b7f3ff77671b" IssueInstant="2014-12-24T05:20:47.060Z" Version="2.0">
          <Issuer>https://sts.windows.net/b9411234-09af-49c2-b0c3-653adc1f376e/</Issuer>
          <ds:Signature xmlns:ds="http://www.w3.org/2000/09/xmldsig#">
            <ds:SignedInfo>
              <ds:CanonicalizationMethod Algorithm="http://www.w3.org/2001/10/xml-exc-c14n#" />
              <ds:SignatureMethod Algorithm="http://www.w3.org/2001/04/xmldsig-more#rsa-sha256" />
              <ds:Reference URI="#_3ef08993-846b-41de-99df-b7f3ff77671b">
                <ds:Transforms>
                  <ds:Transform Algorithm="http://www.w3.org/2000/09/xmldsig#enveloped-signature" />
                  <ds:Transform Algorithm="http://www.w3.org/2001/10/xml-exc-c14n#" />
                </ds:Transforms>
                <ds:DigestMethod Algorithm="http://www.w3.org/2001/04/xmlenc#sha256" />
                <ds:DigestValue>cV1J580U1pD24hEyGuAxrbtgROVyghCqI32UkER/nDY=</ds:DigestValue>
              </ds:Reference>
            </ds:SignedInfo>
            <ds:SignatureValue>j+zPf6mti8Rq4Kyw2NU2nnu0pbJU1z5bR/zDaKaO7FCTdmjUzAvIVfF8pspVR6CbzcYM3HOAmLhuWmBkAAk6qQUBmKsw+XlmF/pB/ivJFdgZSLrtlBs1P/WBV3t04x6fRW4FcIDzh8KhctzJZfS5wGCfYw95er7WJxJi0nU41d7j5HRDidBoXgP755jQu2ZER7wOYZr6ff+ha+/Aj3UMw+8ZtC+WCJC3yyENHDAnp2RfgdElJal68enn668fk8pBDjKDGzbNBO6qBgFPaBT65YvE/tkEmrUxdWkmUKv3y7JWzUYNMD9oUlut93UTyTAIGOs5fvP9ZfK2vNeMVJW7Xg==</ds:SignatureValue>
            <KeyInfo xmlns="http://www.w3.org/2000/09/xmldsig#">
              <X509Data>
                <X509Certificate>MIIDPjCCAabcAwIBAgIQsRiM0jheFZhKk49YD0SK1TAJBgUrDgMCHQUAMC0xKzApBgNVBAMTImFjY291bnRzLmFjY2Vzc2NvbnRyb2wud2luZG93cy5uZXQwHhcNMTQwMTAxMDcwMDAwWhcNMTYwMTAxMDcwMDAwWjAtMSswKQYDVQQDEyJhY2NvdW50cy5hY2Nlc3Njb250cm9sLndpbmRvd3MubmV0MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAkSCWg6q9iYxvJE2NIhSyOiKvqoWCO2GFipgH0sTSAs5FalHQosk9ZNTztX0ywS/AHsBeQPqYygfYVJL6/EgzVuwRk5txr9e3n1uml94fLyq/AXbwo9yAduf4dCHTP8CWR1dnDR+Qnz/4PYlWVEuuHHONOw/blbfdMjhY+C/BYM2E3pRxbohBb3x//CfueV7ddz2LYiH3wjz0QS/7kjPiNCsXcNyKQEOTkbHFi3mu0u13SQwNddhcynd/GTgWN8A+6SN1r4hzpjFKFLbZnBt77ACSiYx+IHK4Mp+NaVEi5wQtSsjQtI++XsokxRDqYLwus1I1SihgbV/STTg5enufuwIDAQABo2IwYDBeBgNVHQEEVzBVgBDLebM6bK3BjWGqIBrBNFeNoS8wLTErMCkGA1UEAxMiYWNjb3VudHMuYWNjZXNzY29udHJvbC53aW5kb3dzLm5ldIIQsRiM0jheFZhKk49YD0SK1TAJBgUrDgMCHQUAA4IBAQCJ4JApryF77EKC4zF5bUaBLQHQ1PNtA1uMDbdNVGKCmSp8M65b8h0NwlIjGGGy/unK8P6jWFdm5IlZ0YPTOgzcRZguXDPj7ajyvlVEQ2K2ICvTYiRQqrOhEhZMSSZsTKXFVwNfW6ADDkN3bvVOVbtpty+nBY5UqnI7xbcoHLZ4wYD251uj5+lo13YLnsVrmQ16NCBYq2nQFNPuNJw6t3XUbwBHXpF46aLT1/eGf/7Xx6iy8yPJX4DyrpFTutDz882RWofGEO5t4Cw+zZg70dJ/hH/ODYRMorfXEW+8uKmXMKmX2wyxMKvfiPbTy5LmAU8Jvjs2tLg4rOBcXWLAIarZ</X509Certificate>
              </X509Data>
            </KeyInfo>
          </ds:Signature>
          <Subject>
            <NameID Format="urn:oasis:names:tc:SAML:2.0:nameid-format:persistent">m_H3naDei2LNxUmEcWd0BZlNi_jVET1pMLR6iQSuYmo</NameID>
            <SubjectConfirmation Method="urn:oasis:names:tc:SAML:2.0:cm:bearer" />
          </Subject>
          <Conditions NotBefore="2014-12-24T05:15:47.060Z" NotOnOrAfter="2014-12-24T06:15:47.060Z">
            <AudienceRestriction>
              <Audience>https://contoso.onmicrosoft.com/MyWebApp</Audience>
            </AudienceRestriction>
          </Conditions>
          <AttributeStatement>
            <Attribute Name="http://schemas.microsoft.com/identity/claims/objectidentifier">
              <AttributeValue>a1addde8-e4f9-4571-ad93-3059e3750d23</AttributeValue>
            </Attribute>
            <Attribute Name="http://schemas.microsoft.com/identity/claims/tenantid">
              <AttributeValue>b9411234-09af-49c2-b0c3-653adc1f376e</AttributeValue>
            </Attribute>
            <Attribute Name="http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name">
              <AttributeValue>sample.admin@contoso.onmicrosoft.com</AttributeValue>
            </Attribute>
            <Attribute Name="http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname">
              <AttributeValue>Admin</AttributeValue>
            </Attribute>
            <Attribute Name="http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname">
              <AttributeValue>Sample</AttributeValue>
            </Attribute>
            <Attribute Name="http://schemas.microsoft.com/ws/2008/06/identity/claims/groups">
              <AttributeValue>5581e43f-6096-41d4-8ffa-04e560bab39d</AttributeValue>
              <AttributeValue>07dd8a89-bf6d-4e81-8844-230b77145381</AttributeValue>
              <AttributeValue>0e129f4g-6b0a-4944-982d-f776000632af</AttributeValue>
              <AttributeValue>3ee07328-52ef-4739-a89b-109708c22fb5</AttributeValue>
              <AttributeValue>329k14b3-1851-4b94-947f-9a4dacb595f4</AttributeValue>
              <AttributeValue>6e32c650-9b0a-4491-b429-6c60d2ca9a42</AttributeValue>
              <AttributeValue>f3a169a7-9a58-4e8f-9d47-b70029v07424</AttributeValue>
              <AttributeValue>8e2c86b2-b1ad-476d-9574-544d155aa6ff</AttributeValue>
              <AttributeValue>1bf80264-ff24-4866-b22c-6212e5b9a847</AttributeValue>
              <AttributeValue>4075f9c3-072d-4c32-b542-03e6bc678f3e</AttributeValue>
              <AttributeValue>76f80527-f2cd-46f4-8c52-8jvd8bc749b1</AttributeValue>
              <AttributeValue>0ba31460-44d0-42b5-b90c-47b3fcc48e35</AttributeValue>
              <AttributeValue>edd41703-8652-4948-94a7-2d917bba7667</AttributeValue>
            </Attribute>
            <Attribute Name="http://schemas.microsoft.com/identity/claims/identityprovider">
              <AttributeValue>https://sts.windows.net/b9411234-09af-49c2-b0c3-653adc1f376e/</AttributeValue>
            </Attribute>
          </AttributeStatement>
          <AuthnStatement AuthnInstant="2014-12-23T18:51:11.000Z">
            <AuthnContext>
              <AuthnContextClassRef>urn:oasis:names:tc:SAML:2.0:ac:classes:Password</AuthnContextClassRef>
            </AuthnContext>
          </AuthnStatement>
        </Assertion>
      </t:RequestedSecurityToken>
      <t:RequestedAttachedReference>
        <SecurityTokenReference xmlns="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-secext-1.0.xsd" xmlns:d3p1="http://docs.oasis-open.org/wss/oasis-wss-wssecurity-secext-1.1.xsd" d3p1:TokenType="http://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.1#SAMLV2.0">
          <KeyIdentifier ValueType="http://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.1#SAMLID">_3ef08993-846b-41de-99df-b7f3ff77671b</KeyIdentifier>
        </SecurityTokenReference>
      </t:RequestedAttachedReference>
      <t:RequestedUnattachedReference>
        <SecurityTokenReference xmlns="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-secext-1.0.xsd" xmlns:d3p1="http://docs.oasis-open.org/wss/oasis-wss-wssecurity-secext-1.1.xsd" d3p1:TokenType="http://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.1#SAMLV2.0">
          <KeyIdentifier ValueType="http://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.1#SAMLID">_3ef08993-846b-41de-99df-b7f3ff77671b</KeyIdentifier>
        </SecurityTokenReference>
      </t:RequestedUnattachedReference>
      <t:TokenType>http://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.1#SAMLV2.0</t:TokenType>
      <t:RequestType>http://schemas.xmlsoap.org/ws/2005/02/trust/Issue</t:RequestType>
      <t:KeyType>http://schemas.xmlsoap.org/ws/2005/05/identity/NoProofKey</t:KeyType>
    </t:RequestSecurityTokenResponse>

### <a name="jwt-token---user-impersonation"></a>JWT 權杖 - 使用者模擬
這是在授權碼授與流程中使用的典型 JSON Web 權杖 (JWT) 範例。
在加法 tooclaims hello 語彙基元包含版本號碼中的**ver**和**appidacr**，hello 驗證內容類別參考，即表示 hello 用戶端的驗證方式。 為公用的用戶端 hello 值為 0。 如果使用用戶端識別碼或用戶端密碼，hello 值為 1。

    {
     typ: "JWT",
     alg: "RS256",
     x5t: "kriMPdmBvx68skT8-mPAB3BseeA"
    }.
    {
     aud: "https://contoso.onmicrosoft.com/scratchservice",
     iss: "https://sts.windows.net/b9411234-09af-49c2-b0c3-653adc1f376e/",
     iat: 1416968588,
     nbf: 1416968588,
     exp: 1416972488,
     ver: "1.0",
     tid: "b9411234-09af-49c2-b0c3-653adc1f376e",
     amr: [
      "pwd"
     ],
     roles: [
      "Admin"
     ],
     oid: "6526e123-0ff9-4fec-ae64-a8d5a77cf287",
     upn: "sample.user@contoso.onmicrosoft.com",
     unique_name: "sample.user@contoso.onmicrosoft.com",
     sub: "yf8C5e_VRkR1egGxJSDt5_olDFay6L5ilBA81hZhQEI",
     family_name: "User",
     given_name: "Sample",
     groups: [
      "0e129f6b-6b0a-4944-982d-f776000632af",
      "323b13b3-1851-4b94-947f-9a4dacb595f4",
      "6e32c250-9b0a-4491-b429-6c60d2ca9a42",
      "f3a161a7-9a58-4e8f-9d47-b70022a07424",
      "8d4c81b2-b1ad-476d-9574-544d155aa6ff",
      "1bf80164-ff24-4866-b19c-6212e5b9a847",
      "76f80127-f2cd-46f4-8c52-8edd8bc749b1",
      "0ba27160-44d0-42b5-b90c-47b3fcc48e35"
     ],
     appid: "b075ddef-0efa-123b-997b-de1337c29185",
     appidacr: "1",
     scp: "user_impersonation",
     acr: "1"
    }.

## <a name="related-content"></a>相關內容
* 請參閱 hello Azure AD Graph[原則作業](https://msdn.microsoft.com/library/azure/ad/graph/api/policy-operations)和 hello[原則實體](https://msdn.microsoft.com/library/azure/ad/graph/api/entity-and-complex-type-reference#policy-entity)，toolearn 更多關於管理透過 hello Azure AD Graph API 的權杖存留期原則。
* 如需透過 PowerShell Cmdlet 管理原則的詳細資訊和範例，包括範例，請參閱[在 Azure AD 中設定權杖存留期](../active-directory-configurable-token-lifetimes.md)。 
