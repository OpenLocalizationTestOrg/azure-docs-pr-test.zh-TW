---
title: "Azure Active Directory 中的 aaaConfigurable 權杖存留期 |Microsoft 文件"
description: "了解 Azure AD 所簽發 tooset 權杖的存留期的方式。"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 06f5b317-053e-44c3-aaaa-cf07d8692735
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: billmath
ms.custom: aaddev
ms.reviewer: anchitn
ms.openlocfilehash: 0d4c8545981c5463cc7c95f669167bbc38230123
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configurable-token-lifetimes-in-azure-active-directory-public-preview"></a>Azure Active Directory 中可設定的權杖存留期 (公開預覽版)
您可以指定 hello Azure Active Directory (Azure AD) 所簽發的權杖存留期。 不論是針對組織中所有的應用程式、針對多租用戶 (多組織) 應用程式，還是針對組織中特定的服務主體，都可以設定權杖存留期。

> [!NOTE]
> 這項功能目前為公開預覽版。 準備 toorevert 或移除任何變更。 公開預覽期間的任何 Azure Active Directory 訂用帳戶中使用 hello 功能。 不過，通常可以使用 hello 功能時，可能需要某些層面 hello 功能[Azure Active Directory Premium](active-directory-get-started-premium.md)訂用帳戶。
>
>

在 Azure AD 中，原則物件代表在組織中個別應用程式或所有應用程式上強制執行的一組規則。 每種原則類型有唯一的結構，以一組套用的 tooobjects toowhich 與其相關的屬性。

您可以指定為 hello 預設原則的原則，為您的組織。 hello 原則會套用的 tooany hello 組織中的應用程式，只要它不會覆寫優先順序較高的原則。 您也可以指派原則 toospecific 應用程式。 hello 依優先順序因原則類型。


## <a name="token-types"></a>權杖類型

您可以針對重新整理權杖、存取權杖、工作階段權杖及識別碼權杖設定權杖存留期原則。

### <a name="access-tokens"></a>存取權杖
用戶端使用存取權杖 tooaccess 受保護的資源。 存取權杖僅可用於特定使用者、用戶端及資源的組合。 存取權杖是不可撤銷的，在到期之前都會一直有效。 惡意執行者若已取得存取權杖，便可在權杖的存留期範圍內使用該權杖。 調整 hello 存留期的存取語彙基元是改善系統效能之間的取捨，而且增加 hello 一段時間的 hello 用戶端會保留存取，完成 hello 使用者帳戶已停用。 改善的系統效能，來減少用戶端需要 tooacquire 全新的存取語彙基元的 hello 次數來達成。

### <a name="refresh-tokens"></a>重新整理權杖
當用戶端取得存取權杖 tooaccess 受保護的資源時，hello 用戶端會收到重新整理權杖和存取權杖。 hello 重新整理權杖時，使用的 tooobtain 新存取/重新整理語彙基元組 hello 目前存取權杖到期。 重新整理權杖是使用者和用戶端的繫結的 tooa 組合。 重新整理權杖可予以撤銷，並每次使用 hello 語彙基元時，會檢查 hello 權杖的有效性。

它是重要 toomake 機密用戶端和公用的用戶端之間的差異。 如需不同類型用戶端的詳細資訊，請參閱 [RFC 6749](https://tools.ietf.org/html/rfc6749#section-2.1)。

#### <a name="token-lifetimes-with-confidential-client-refresh-tokens"></a>具有機密用戶端重新整理權杖的權杖存留期
機密用戶端是可以安全地儲存用戶端密碼的應用程式。 它們可以證明要求即將從 hello 用戶端應用程式，而不是從惡意動作項目。 例如，web 應用程式是機密用戶端，因為它可以在 hello web 伺服器上儲存用戶端密碼。 它不是公開的。 由於這些流程更安全，hello 發行的 toothese 流程會重新整理權杖的預設存留時間`until-revoked`，就無法變更使用原則，而且不會撤銷上自願密碼重設。

#### <a name="token-lifetimes-with-public-client-refresh-tokens"></a>具有公開用戶端重新整理權杖的權杖存留期

公開用戶端無法安全地儲存用戶端密碼。 例如，iOS/Android 應用程式無法模糊化 hello 資源擁有者，從密碼，因此它會被視為公用的用戶端。 您可以設定原則資源 tooprevent 重新整理權杖從公用用戶端無法取得新的存取權/重新整理 token 組的指定時間之前。 (toodo，使用 hello 重新整理語彙基元非作用中時間上限 屬性。)您也可以使用原則 tooset 不再接受超過 hello 重新整理權杖的期限。 (toodo，使用 hello 重新整理權杖的最大 Age 屬性。)您可以調整時間和頻率 hello 使用者是必要的 tooreenter 認證，而不是以無訊息模式需要，使用公用的用戶端應用程式時重新整理語彙基元 toocontrol hello 存留期。

### <a name="id-tokens"></a>ID 權杖
ID 權杖會傳遞 toowebsites 和原生用戶端。 識別碼權杖包含使用者的設定檔資訊。 ID 語彙基元是繫結的 tooa 特定的使用者和用戶端的組合。 識別碼權杖在到期前都會被視為有效。 通常，web 應用程式符合使用者的 hello 使用者發出 hello 應用程式 toohello 存留期的 hello 的 ID 語彙基元中的工作階段存留期。 您可以調整 hello 存留期的 ID 語彙基元 toocontrol 頻率 hello web 應用程式到期 hello 應用程式工作階段和它需要 hello 使用者 toobe （以無訊息模式或以互動方式），重新驗證與 Azure AD 的頻率。

### <a name="single-sign-on-session-tokens"></a>單一登入工作階段權杖
當使用者向 Azure AD，並選取 hello**讓我保持登**核取方塊，單一登入 (SSO) 會建立工作階段與 hello 使用者的瀏覽器和 Azure AD。 hello SSO 語彙基元，hello 形式 cookie，代表此工作階段。 請注意該 hello SSO 工作階段權杖不是繫結的 tooa 特定資源/用戶端應用程式。 SSO 工作階段權杖是可撤銷的，而每次使用這些權杖時，系統都會檢查其有效性。

Azure AD 會使用兩種 SSO 工作階段權杖︰持續性和非持續性。 持續性工作階段權杖會儲存為永續性 cookie，由 hello 瀏覽器。 非持續性工作階段權杖是儲存為工作階段 Cookie。 （工作階段 cookie 會終結 hello 瀏覽器關閉時）。

非持續性工作階段權杖有 24 小時的存留期。 持續性權杖有 180 天的存留期。 SSO 的工作階段權杖用在其有效期間內，任何時候 hello 有效期間已擴充，另一個 24 小時或 180 天，視 hello 語彙基元類型而定。 如果未在 SSO 工作階段權杖的有效期內使用此權杖，系統就會將其視為過期而不再接受它。

您可以使用原則 tooset hello 後的時間超出哪些 hello 不再接受工作階段權杖發行 hello 第一個工作階段權杖。 (toodo，使用 hello 工作階段權杖的最大 Age 屬性。)您可以調整使用者時間和頻率是必要的 tooreenter 認證，而不是以無訊息模式驗證，使用 web 應用程式時的工作階段權杖的 toocontrol hello 存留期。

### <a name="token-lifetime-policy-properties"></a>權杖存留期原則屬性
權杖存留期原則是一種包含權杖存留期規則的原則物件。 使用 hello 原則 toocontrol hello 屬性會指定權杖存留期。 如果沒有原則設定，hello 系統會強制執行 hello 預設存留時間值。

### <a name="configurable-token-lifetime-properties"></a>可設定的權杖存留期屬性
| 屬性 | 原則屬性字串 | 影響 | 預設值 | 最小值 | 最大值 |
| --- | --- | --- | --- | --- | --- |
| 存取權杖存留期 |AccessTokenLifetime |存取權杖、識別碼權杖、SAML2 權杖 |1 小時 |10 分鐘 |1 天 |
| 重新整理權杖最大閒置時間 |MaxInactiveTime |重新整理權杖 |14 天 |10 分鐘 |90 天 |
| 單一要素重新整理權杖最大壽命 |MaxAgeSingleFactor |重新整理權杖 (適用於任何使用者) |直到撤銷為止 |10 分鐘 |直到撤銷為止<sup>1</sup> |
| 多重要素重新整理權杖最大壽命 |MaxAgeMultiFactor |重新整理權杖 (適用於任何使用者) |直到撤銷為止 |10 分鐘 |直到撤銷為止<sup>1</sup> |
| 單一要素工作階段權杖最大壽命 |MaxAgeSessionSingleFactor<sup>2</sup> |工作階段權杖 (持續性和非持續性) |直到撤銷為止 |10 分鐘 |直到撤銷為止<sup>1</sup> |
| 多重要素工作階段權杖最大壽命 |MaxAgeSessionMultiFactor<sup>3</sup> |工作階段權杖 (持續性和非持續性) |直到撤銷為止 |10 分鐘 |直到撤銷為止<sup>1</sup> |

* <sup>1</sup>365 天是 hello 明確的長度上限可設定這些屬性。
* <sup>2</sup>如果**MaxAgeSessionSingleFactor**未設定，這個值會採用 hello **MaxAgeSingleFactor**值。 如果設定這兩個參數，hello 屬性會接受 hello （直到層已撤銷） 的預設值。
* <sup>3</sup>如果**MaxAgeSessionMultiFactor**未設定，這個值會採用 hello **MaxAgeMultiFactor**值。 如果設定這兩個參數，hello 屬性會接受 hello （直到層已撤銷） 的預設值。

### <a name="exceptions"></a>例外狀況
| 屬性 | 影響 | 預設值 |
| --- | --- | --- |
| 重新整理權杖最大壽命 (針對沒有足夠撤銷資訊的同盟使用者簽發<sup>1</sup>) |重新整理權杖 (針對沒有足夠撤銷資訊的同盟使用者簽發<sup>1</sup>) |12 小時 |
| 重新整理權杖最大閒置時間 (針對機密用戶端簽發) |重新整理權杖 (針對機密用戶端簽發) |90 天 |
| 重新整理權杖最大壽命 (針對機密用戶端簽發) |重新整理權杖 (針對機密用戶端簽發) |直到撤銷為止 |

* <sup>1</sup>擁有足夠的撤銷資訊包括不需要任何使用者的同盟使用者 hello"LastPasswordChangeTimestamp 」 進行同步處理的屬性。 這些使用者會獲得這個簡短的最大存留期，因為 AAD 時，無法 tooverify toorevoke 的語彙基元繫結的 tooan 舊的認證 （例如密碼已變更），和必須檢查上一步中更頻繁地 tooensure hello 使用者和相關聯的語彙基元仍在理想的永久性。 tooimprove 此體驗，租用戶系統管理員必須確定正在同步處理 hello"LastPasswordChangeTimestamp"屬性 （這可以設定 hello 使用者物件使用 Powershell 或透過 AADSync）。

### <a name="policy-evaluation-and-prioritization"></a>原則評估及優先順序
您可以建立並再指派 權杖存留期原則 tooa 特定應用程式、 tooyour 組織和 tooservice 主體。 多個原則可能會套用 tooa 特定應用程式。 hello 生效的權杖存留期原則遵守下列規則：

* 如果原則已明確指派 toohello 服務主體，它會強制執行。
* 如果沒有原則明確指派的 toohello 服務主體，會強制執行原則明確指派 toohello 總公司 hello 服務主體。
* 如果沒有原則明確指派 toohello 服務主體或 toohello 組織，hello 分派 toohello 應用程式的原則會強制執行。
* 如果沒有原則已被指派 toohello 服務主體、 hello 組織或 hello 應用程式物件，hello 的預設值會強制執行。 (請參閱中的 hello 表格[可設定權杖存留期屬性](#configurable-token-lifetime-properties)。)

如需 hello 應用程式與服務主體物件間的關聯性的詳細資訊，請參閱[應用程式與 Azure Active Directory 中的服務主體物件](active-directory-application-objects.md)。

在使用 hello 語彙基元的 hello 階段評估權杖的有效性。 具有 hello 正在存取的 hello 應用程式上的高優先順序的 hello 原則才會生效。

> [!NOTE]
> 以下是範例案例。
>
> 使用者想 tooaccess 兩個 web 應用程式： Web 應用程式 A 和 Web 應用程式 b。
> 
> 因素：
> * 這兩個 web 應用程式處於 hello 相同父系的組織。
> * 具有工作階段權杖最短使用期限八個小時的權杖存留期原則 1 是設為 hello 父組織的預設值。
> * Web 應用程式的一般使用 web 應用程式，而且不是連結的 tooany 原則。
> * Web 應用程式 B 適用於高度機密的程序。 其服務主體是連結的 tooToken 存留期原則 2，其具有工作階段權杖保留時間上限為 30 分鐘。
>
> 在下午 12:00，hello 使用者啟動新的瀏覽器工作階段並嘗試 tooaccess Web 應用程式 a hello 使用者已重新導向的 tooAzure AD，並要求 toosign 中。 這會建立具有工作階段權杖 hello 瀏覽器中的 cookie。 hello 使用者是以允許 hello 使用者 tooaccess hello 應用程式識別碼權杖重新導向後的 tooWeb 應用程式 A。
>
> 在 12:15 PM hello 的使用者嘗試 tooaccess Web 應用程式 b hello 瀏覽器重新導向 tooAzure AD，它會偵測 hello 工作階段 cookie。 Web 應用程式 B 的服務主體是連結的 tooToken 存留期原則 2，但它也是有預設的權杖存留期原則 1 hello 父組織的一部分。 權杖存留期原則 2 會生效，因為原則連結的 tooservice 主體具有的優先順序高於組織預設原則。 hello 工作階段權杖核發的原始內 hello 過去 30 分鐘內，因此被視為有效。 重新導向後 tooWeb 應用程式 B 授與存取權的 ID 語彙基元與 hello 使用者。
>
> 在下午 1:00，hello 嘗試 tooaccess Web 應用程式 a hello 使用者已重新導向的 tooAzure AD。 Web 應用程式的不是連結的 tooany 原則，但因為它是在組織中與預設的權杖存留期原則 1 時，該原則會生效。 偵測到 hello 初次發行 hello 內最後八小時的工作階段 cookie。 hello 使用者是以無訊息模式重新導向後 tooWeb 應用程式 A 與新的 ID 語彙基元。 hello 使用者不是必要的 tooauthenticate。
>
> 立即 hello 使用者之後，嘗試 tooaccess Web 應用程式 b hello 使用者會是重新導向的 tooAzure AD。 與先前一樣，權杖存留期原則 2 會生效。 Hello 使用者因為 hello 語彙基元簽發 30 分鐘以上，會提示的 tooreenter 他們登入認證。 會簽發全新的工作階段權杖和識別碼權杖。 hello 使用者可以存取 Web 應用程式 b。
>
>

## <a name="configurable-policy-property-details"></a>可設定的原則屬性詳細資料
### <a name="access-token-lifetime"></a>存取權杖存留期
**字串：**AccessTokenLifetime

**影像：**存取權杖、識別碼權杖

**摘要：**此原則可控制將此資源的存取權杖和識別碼權杖視為有效的期限。 減少 hello 存取權杖存留期屬性，可減少 hello 風險的存取權杖或正由惡意的動作項目延伸的一段時間的 ID 語彙基元。 （無法撤銷這些語彙基元）。hello 代價是，效能受到負面影響，因為 hello 權杖有 toobe 更常被取代。

### <a name="refresh-token-max-inactive-time"></a>重新整理權杖最大閒置時間
**字串︰**MaxInactiveTime

**影響：**重新整理權杖

**摘要：**此原則會控制多久重新整理權杖前可保留在用戶端也無法再使用它 tooretrieve 新存取/重新整理語彙基元組嘗試 tooaccess 此資源時。 通常使用重新整理權杖時，會傳回新的重新整理權杖，因為這項原則會防止存取，如果 hello 用戶端會嘗試的 tooaccess hello 期間使用 hello 目前的重新整理語彙基元的任何資源指定的時間。

此原則會強制未使用其用戶端 tooreauthenticate tooretrieve 新的重新整理權杖上的使用者。

tooa 比 hello 單一因素語彙基元保留時間上限較低的值和 hello Multi-factor 重新整理語彙基元保留時間上限屬性必須設定 hello 重新整理語彙基元非作用中時間上限 屬性。

### <a name="single-factor-refresh-token-max-age"></a>單一要素重新整理權杖最大壽命
**字串︰**MaxAgeSingleFactor

**影響：**重新整理權杖

**摘要：**此原則可控制如何長時間的使用者可以使用新的重新整理語彙基元 tooget 存取/重新整理 token 組它們上次驗證之後已成功使用單一因素。 Hello 使用者的使用者驗證並接收新的重新整理語彙基元之後，可以使用 hello 重新整理權杖流程 hello 指定的時間週期。 （這是 true，只要未撤銷 hello 目前的重新整理權杖，並不處於未使用的時間超過 hello 未使用的時間）。此時，hello 使用者是強制的 tooreauthenticate tooreceive 新的重新整理權杖。

減少最大存留期 hello 強制使用者 tooauthenticate 頻率。 因為單一因素驗證多重要素驗證比更不安全，建議您將設定這個屬性 tooa 值也就是等於 tooor 小於 hello Multi-factor 重新整理語彙基元保留時間上限 屬性。

### <a name="multi-factor-refresh-token-max-age"></a>多重要素重新整理權杖最大壽命
**字串︰**MaxAgeMultiFactor

**影響：**重新整理權杖

**摘要：**此原則可控制如何長時間的使用者可以使用新的重新整理語彙基元 tooget 存取/重新整理 token 組它們上次驗證之後已成功使用多因素。 Hello 使用者的使用者驗證並接收新的重新整理語彙基元之後，可以使用 hello 重新整理權杖流程 hello 指定的時間週期。 （這是 true，只要未撤銷 hello 目前的重新整理權杖，並不是未使用的時間超過 hello 未使用的時間）。此時，會強制使用者 tooreauthenticate tooreceive 新的重新整理權杖。

減少最大存留期 hello 強制使用者 tooauthenticate 頻率。 因為單一因素驗證多重要素驗證比更不安全，我們建議您設定為大於 hello 單一因素重新整理語彙基元保留時間上限 屬性等於 tooor 這個屬性 tooa 值。

### <a name="single-factor-session-token-max-age"></a>單一要素工作階段權杖最大壽命
**字串︰**MaxAgeSessionSingleFactor

**影響：**工作階段權杖 (持續性和非持續性)

**摘要：**這個原則會控制多久的使用者可以使用工作階段權杖 tooget，新的識別碼和工作階段語彙基元之後它們上次驗證成功使用單一因素。 Hello 使用者的使用者驗證並接收新的工作階段語彙基元之後，可以使用 hello 工作階段權杖流程 hello 指定的時間週期。 （這是 true，只要 hello 目前工作階段 token 未撤銷，且尚未過期。）Hello 指定一段時間之後，hello 使用者是強制的 tooreauthenticate tooreceive 新的工作階段權杖。

減少最大存留期 hello 強制使用者 tooauthenticate 頻率。 因為單一因素驗證多重要素驗證比更不安全，我們建議您設定這個屬性 tooa 值等於 tooor 不超過 hello Multi-factor 工作階段權杖的最大年齡屬性。

### <a name="multi-factor-session-token-max-age"></a>多重要素工作階段權杖最大壽命
**字串︰**MaxAgeSessionMultiFactor

**影響：**工作階段權杖 (持續性和非持續性)

**摘要：**這個原則會控制多久的使用者可以使用新識別碼和工作階段語彙基元之後的工作階段權杖的 tooget hello 它們藉由使用多因素驗證成功的最後一次。 Hello 使用者的使用者驗證並接收新的工作階段語彙基元之後，可以使用 hello 工作階段權杖流程 hello 指定的時間週期。 （這是 true，只要 hello 目前工作階段 token 未撤銷，且尚未過期。）Hello 指定一段時間之後，hello 使用者是強制的 tooreauthenticate tooreceive 新的工作階段權杖。

減少最大存留期 hello 強制使用者 tooauthenticate 頻率。 因為單一因素驗證多重要素驗證比更不安全，我們建議您設定為大於 hello 單一因素工作階段權杖的最大 Age 屬性等於 tooor 這個屬性 tooa 值。

## <a name="example-token-lifetime-policies"></a>範例權杖存留期原則
當您為應用程式、服務主體及您整體組織建立及管理權杖存留期時，在 Azure AD 中許多案例都是可能的。 在本節中，我們將逐步解說一些常見的原則案例，這些案例可以協助您強制實行下列各項的新規則：

* 權杖存留期
* 權杖最大閒置時間
* 權杖最大壽命

在 hello 範例中，您可以了解如何：

* 管理組織的預設原則
* 為 Web 登入建立原則
* 針對呼叫 Web API 的原生應用程式建立原則
* 管理進階原則

### <a name="prerequisites"></a>必要條件
Hello 遵循範例，在您建立、 更新連結，並刪除應用程式、 服務主體與整個組織的原則。 如果您是新 tooAzure AD，我們建議您了解[tooget 的 Azure AD 的租用戶](active-directory-howto-tenant.md)繼續這些範例之前。  

tooget 啟動，請勿 hello 下列步驟：

1. 下載最新的 hello [Azure AD PowerShell 模組公開預覽版本](https://www.powershellgallery.com/packages/AzureADPreview)。
2. 執行 hello`Connect`命令 toosign tooyour Azure AD 系統管理員帳戶中的。 您每次啟動新的工作階段時執行此命令。

    ```PowerShell
    Connect-AzureAD -Confirm
    ```

3. toosee 命令已建立您的組織，執行下列的 hello 中的所有原則。 在下列案例的 hello 的大部分作業之後執行此命令。 執行 hello 命令也可協助您取得 hello * * * * 的原則。

    ```PowerShell
    Get-AzureADPolicy
    ```

### <a name="example-manage-an-organizations-default-policy"></a>範例：管理組織的預設原則
在此範例中，您會建立可讓使用者在您整個組織中降低登入頻率的原則。 toodo，建立單一因素重新整理語彙基元，這會套用到您的組織的權杖存留期原則。 hello 原則是在您的組織和 tooeach 還沒有原則設定的服務主體的套用的 tooevery 應用程式。

1. 建立權杖存留期原則。

    1.  設定重新整理權杖單一因素 hello 太"直到-撤銷。 」 hello 權杖尚未過期，直到已撤銷存取權。 建立 hello 遵循原則定義：

        ```PowerShell
        @('{
            "TokenLifetimePolicy":
            {
                "Version":1,
                "MaxAgeSingleFactor":"until-revoked"
            }
        }')
        ```

    2.  toocreate hello 原則，執行下列命令的 hello:

        ```PowerShell
        New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1, "MaxAgeSingleFactor":"until-revoked"}}') -DisplayName "OrganizationDefaultPolicyScenario" -IsOrganizationDefault $true -Type "TokenLifetimePolicy"
        ```

    3.  toosee 您新的原則和 tooget hello 原則的**ObjectId**，請執行 hello 下列命令：

        ```PowerShell
        Get-AzureADPolicy
        ```

2. 更新 hello 原則。

    您可能會決定您設定在此範例中的 hello 第一個原則不是因為您的服務需要完全相同。 tooset 兩天內，在您重新整理權杖單一因素 tooexpire 執行 hello 下列命令：

    ```PowerShell
    Set-AzureADPolicy -Id <ObjectId FROM GET COMMAND> -DisplayName "OrganizationDefaultPolicyUpdatedScenario" -Definition @('{"TokenLifetimePolicy":{"Version":1,"MaxAgeSingleFactor":"2.00:00:00"}}')
    ```

### <a name="example-create-a-policy-for-web-sign-in"></a>範例：為 Web 登入建立原則

在此範例中，您可以建立原則，要求使用者 tooauthenticate 更頻繁地在您 web 應用程式。 此原則設定的 hello 存取 ID 語彙基元的 hello 存留期和 hello 的 web 應用程式的多因素工作階段權杖 toohello 服務主體的最大存留期。

1. 建立權杖存留期原則。

    此原則，如 web 登入設定 hello 存取/識別碼權杖存留期和 hello 最大的單一因素工作階段權杖的存留期 tootwo 小時。

    1.  toocreate hello 原則，執行下列命令：

        ```PowerShell
        New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1,"AccessTokenLifetime":"02:00:00","MaxAgeSessionSingleFactor":"02:00:00"}}') -DisplayName "WebPolicyScenario" -IsOrganizationDefault $false -Type "TokenLifetimePolicy"
        ```

    2.  toosee 您新的原則和 tooget hello 原則**ObjectId**，請執行 hello 下列命令：

        ```PowerShell
        Get-AzureADPolicy
        ```

2.  指派 hello 原則 tooyour 服務主體。 您也需要 tooget hello **ObjectId**服務主體。 

    1.  toosee 貴組織的所有服務主體中，您可以查詢[Microsoft Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity)。 或者，在[Azure AD Graph 總管](https://graphexplorer.cloudapp.net/)，登入 tooyour Azure AD 帳戶。

    2.  當您擁有 hello **ObjectId**您的服務主體，執行下列命令的 hello:

        ```PowerShell
        Add-AzureADServicePrincipalPolicy -Id <ObjectId of hello ServicePrincipal> -RefObjectId <ObjectId of hello Policy>
        ```


### <a name="example-create-a-policy-for-a-native-app-that-calls-a-web-api"></a>範例：針對呼叫 Web API 的原生應用程式建立原則
在此範例中，您可以建立原則，經常要求使用者 tooauthenticate 較少。 hello 原則也以增加 hello hello 使用者必須重新驗證之前，使用者可以是作用中的時間量。 hello 原則會套用的 toohello web API。 當 hello 原生應用程式要求 hello 做為資源的 web API 時，會套用此原則。

1. 建立權杖存留期原則。

    1.  toocreate web API，執行下列命令的 hello 嚴格的原則：

        ```PowerShell
        New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1,"MaxInactiveTime":"30.00:00:00","MaxAgeMultiFactor":"until-revoked","MaxAgeSingleFactor":"180.00:00:00"}}') -DisplayName "WebApiDefaultPolicyScenario" -IsOrganizationDefault $false -Type "TokenLifetimePolicy"
        ```

    2.  toosee 您新的原則和 tooget hello 原則**ObjectId**，請執行 hello 下列命令：

        ```PowerShell
        Get-AzureADPolicy
        ```

2. 指派 hello 原則 tooyour web API。 您也需要 tooget hello **ObjectId**應用程式。 hello 您的應用程式的最佳方式 toofind **ObjectId**為 toouse hello [Azure 入口網站](https://portal.azure.com/)。

   當您擁有 hello **ObjectId**應用程式，執行下列命令的 hello:

        ```PowerShell
        Add-AzureADApplicationPolicy -Id <ObjectId of hello Application> -RefObjectId <ObjectId of hello Policy>
        ```


### <a name="example-manage-an-advanced-policy"></a>範例：管理進階原則
在此範例中，您可以建立幾個原則，toolearn hello 優先順序系統的運作方式。 您也可以了解如何 toomanage 是套用的 tooseveral 物件的多個原則。

1. 建立權杖存留期原則。

    1.  toocreate 設定 hello 單一因素重新整理權杖的存留期 too30 天數，執行下列命令的 hello 的組織預設原則：

        ```PowerShell
        New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1,"MaxAgeSingleFactor":"30.00:00:00"}}') -DisplayName "ComplexPolicyScenario" -IsOrganizationDefault $true -Type "TokenLifetimePolicy"
        ```

    2.  toosee 您新的原則和 tooget hello 原則的**ObjectId**，請執行 hello 下列命令：

        ```PowerShell
        Get-AzureADPolicy
        ```

2. 指派 hello 原則 tooa 服務主體。

    現在，您有套用 toohello 整個組織的原則。 您可能希望 toopreserve 這 30 天的特定服務主體，但變更 hello 組織預設原則 toohello 上限 」 直到-撤銷。 」

    1.  toosee 貴組織的所有服務主體中，您可以查詢[Microsoft Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity)。 或者，在 [Azure AD Graph 總管](https://graphexplorer.cloudapp.net/)，使用您的 Azure AD 帳戶登入。

    2.  當您擁有 hello **ObjectId**您的服務主體，執行下列命令的 hello:

            ```PowerShell
            Add-AzureADServicePrincipalPolicy -Id <ObjectId of hello ServicePrincipal> -RefObjectId <ObjectId of hello Policy>
            ```
        
3. 設定 hello `IsOrganizationDefault` toofalse 加上旗標：

    ```PowerShell
    Set-AzureADPolicy -Id <ObjectId of Policy> -DisplayName "ComplexPolicyScenario" -IsOrganizationDefault $false
    ```

4. 建立新的組織預設原則：

    ```PowerShell
    New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1,"MaxAgeSingleFactor":"until-revoked"}}') -DisplayName "ComplexPolicyScenarioTwo" -IsOrganizationDefault $true -Type "TokenLifetimePolicy"
    ```

    您現在可以 hello 原始原則連結的 tooyour 服務主體，而且 hello 新原則設定為您組織的預設原則。 它是重要 tooremember，套用原則 tooservice 主體優先於組織的預設原則。

## <a name="cmdlet-reference"></a>Cmdlet 參考

### <a name="manage-policies"></a>管理原則

您可以使用下列 cmdlet toomanage 原則 hello。

#### <a name="new-azureadpolicy"></a>New-AzureADPolicy

建立新的原則。

```PowerShell
New-AzureADPolicy -Definition <Array of Rules> -DisplayName <Name of Policy> -IsOrganizationDefault <boolean> -Type <Policy Type>
```

| 參數 | 說明 | 範例 |
| --- | --- | --- |
| <code>&#8209;Definition</code> |其中包含所有 hello 原則的規則 stringified JSON 陣列。 | `-Definition @('{"TokenLifetimePolicy":{"Version":1,"MaxInactiveTime":"20:00:00"}}')` |
| <code>&#8209;DisplayName</code> |Hello 原則名稱的字串。 |`-DisplayName "MyTokenPolicy"` |
| <code>&#8209;IsOrganizationDefault</code> |如果為 true，請為 hello 組織的預設原則設定 hello 原則。 如果為 false，則不會執行任何動作。 |`-IsOrganizationDefault $true` |
| <code>&#8209;Type</code> |原則類型。 針對權杖存留期，請一律使用 "TokenLifetimePolicy"。 | `-Type "TokenLifetimePolicy"` |
| <code>&#8209;AlternativeIdentifier</code> [選用] |設定替代識別碼 hello 原則。 |`-AlternativeIdentifier "myAltId"` |

</br></br>

#### <a name="get-azureadpolicy"></a>Get-AzureADPolicy
取得所有 Azure AD 原則或指定的原則。

```PowerShell
Get-AzureADPolicy
```

| 參數 | 說明 | 範例 |
| --- | --- | --- |
| <code>&#8209;Id</code> [選用] |**ObjectId (Id)** hello 原則，您想要。 |`-Id <ObjectId of Policy>` |

</br></br>

#### <a name="get-azureadpolicyappliedobject"></a>Get-AzureADPolicyAppliedObject
取得所有應用程式和服務主體的連結的 tooa 原則。

```PowerShell
Get-AzureADPolicyAppliedObject -Id <ObjectId of Policy>
```

| 參數 | 說明 | 範例 |
| --- | --- | --- |
| <code>&#8209;Id</code> |**ObjectId (Id)** hello 原則，您想要。 |`-Id <ObjectId of Policy>` |

</br></br>

#### <a name="set-azureadpolicy"></a>Set-AzureADPolicy
更新現有的原則。

```PowerShell
Set-AzureADPolicy -Id <ObjectId of Policy> -DisplayName <string>
```

| 參數 | 說明 | 範例 |
| --- | --- | --- |
| <code>&#8209;Id</code> |**ObjectId (Id)** hello 原則，您想要。 |`-Id <ObjectId of Policy>` |
| <code>&#8209;DisplayName</code> |Hello 原則名稱的字串。 |`-DisplayName "MyTokenPolicy"` |
| <code>&#8209;Definition</code> [選用] |其中包含所有 hello 原則的規則 stringified JSON 陣列。 |`-Definition @('{"TokenLifetimePolicy":{"Version":1,"MaxInactiveTime":"20:00:00"}}')` |
| <code>&#8209;IsOrganizationDefault</code> [選用] |如果為 true，請為 hello 組織的預設原則設定 hello 原則。 如果為 false，則不會執行任何動作。 |`-IsOrganizationDefault $true` |
| <code>&#8209;Type</code> [選用] |原則類型。 針對權杖存留期，請一律使用 "TokenLifetimePolicy"。 |`-Type "TokenLifetimePolicy"` |
| <code>&#8209;AlternativeIdentifier</code> [選用] |設定替代識別碼 hello 原則。 |`-AlternativeIdentifier "myAltId"` |

</br></br>

#### <a name="remove-azureadpolicy"></a>Remove-AzureADPolicy
刪除 hello 指定原則。

```PowerShell
 Remove-AzureADPolicy -Id <ObjectId of Policy>
```

| 參數 | 說明 | 範例 |
| --- | --- | --- |
| <code>&#8209;Id</code> |**ObjectId (Id)** hello 原則，您想要。 | `-Id <ObjectId of Policy>` |

</br></br>

### <a name="application-policies"></a>應用程式原則
您可以使用下列指令程式的應用程式原則的 hello。</br></br>

#### <a name="add-azureadapplicationpolicy"></a>Add-AzureADApplicationPolicy
連結 hello 指定原則 tooan 應用程式。

```PowerShell
Add-AzureADApplicationPolicy -Id <ObjectId of Application> -RefObjectId <ObjectId of Policy>
```

| 參數 | 說明 | 範例 |
| --- | --- | --- |
| <code>&#8209;Id</code> |**ObjectId (Id)** hello 應用程式。 | `-Id <ObjectId of Application>` |
| <code>&#8209;RefObjectId</code> |**ObjectId**的 hello 原則。 | `-RefObjectId <ObjectId of Policy>` |

</br></br>

#### <a name="get-azureadapplicationpolicy"></a>Get-AzureADApplicationPolicy
取得 hello 原則指派 tooan 應用程式。

```PowerShell
Get-AzureADApplicationPolicy -Id <ObjectId of Application>
```

| 參數 | 說明 | 範例 |
| --- | --- | --- |
| <code>&#8209;Id</code> |**ObjectId (Id)** hello 應用程式。 | `-Id <ObjectId of Application>` |

</br></br>

#### <a name="remove-azureadapplicationpolicy"></a>Remove-AzureADApplicationPolicy
從應用程式移除原則。

```PowerShell
Remove-AzureADApplicationPolicy -Id <ObjectId of Application> -PolicyId <ObjectId of Policy>
```

| 參數 | 說明 | 範例 |
| --- | --- | --- |
| <code>&#8209;Id</code> |**ObjectId (Id)** hello 應用程式。 | `-Id <ObjectId of Application>` |
| <code>&#8209;PolicyId</code> |**ObjectId**的 hello 原則。 | `-PolicyId <ObjectId of Policy>` |

</br></br>

### <a name="service-principal-policies"></a>服務主體原則
您可以使用下列指令程式的服務主體原則中的 hello。

#### <a name="add-azureadserviceprincipalpolicy"></a>Add-AzureADServicePrincipalPolicy
連結 hello 指定的原則 tooa 服務主體。

```PowerShell
Add-AzureADServicePrincipalPolicy -Id <ObjectId of ServicePrincipal> -RefObjectId <ObjectId of Policy>
```

| 參數 | 說明 | 範例 |
| --- | --- | --- |
| <code>&#8209;Id</code> |**ObjectId (Id)** hello 應用程式。 | `-Id <ObjectId of Application>` |
| <code>&#8209;RefObjectId</code> |**ObjectId**的 hello 原則。 | `-RefObjectId <ObjectId of Policy>` |

</br></br>

#### <a name="get-azureadserviceprincipalpolicy"></a>Get-AzureADServicePrincipalPolicy
取得任何原則連結的 toohello 指定的服務主體。

```PowerShell
Get-AzureADServicePrincipalPolicy -Id <ObjectId of ServicePrincipal>
```

| 參數 | 說明 | 範例 |
| --- | --- | --- |
| <code>&#8209;Id</code> |**ObjectId (Id)** hello 應用程式。 | `-Id <ObjectId of Application>` |

</br></br>

#### <a name="remove-azureadserviceprincipalpolicy"></a>Remove-AzureADServicePrincipalPolicy
從 hello 指定的服務主體移除 hello 原則。

```PowerShell
Remove-AzureADServicePrincipalPolicy -Id <ObjectId of ServicePrincipal>  -PolicyId <ObjectId of Policy>
```

| 參數 | 說明 | 範例 |
| --- | --- | --- |
| <code>&#8209;Id</code> |**ObjectId (Id)** hello 應用程式。 | `-Id <ObjectId of Application>` |
| <code>&#8209;PolicyId</code> |**ObjectId**的 hello 原則。 | `-PolicyId <ObjectId of Policy>` |
