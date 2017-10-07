---
title: "Active Directory aaaAzure v2.0 範圍、 權限和同意 |Microsoft 文件"
description: "在 Azure AD hello v2.0 端點使用，包括領域、 權限和同意授權的描述。"
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 8f98cbf0-a71d-4e34-babf-e644ad9ff423
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 5721d368c435868bfb4ae91cff7fbb9bc4a79b66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="scopes-permissions-and-consent-in-hello-azure-active-directory-v20-endpoint"></a>範圍、 權限，以及在 hello Azure Active Directory v2.0 端點中同意
與 Azure Active Directory (Azure AD) 整合的應用程式會遵循一種授權模型，可讓使用者控制應用程式存取他們資料的方式。 已更新 hello v2.0 實作 hello 的授權模型，並在應用程式必須與 Azure AD 互動的方式變更。 本文涵蓋 hello 基本概念，這個授權模型，包括領域、 權限和同意。

> [!NOTE]
> hello v2.0 端點不支援所有的 Azure Active Directory 的案例和功能。 toodetermine 是否應該使用 hello v2.0 端點，閱讀有關[v2.0 限制](active-directory-v2-limitations.md)。
>
>

## <a name="scopes-and-permissions"></a>範圍和權限
Azure AD 實作 hello [OAuth 2.0](active-directory-v2-protocols.md)授權通訊協定。 OAuth 2.0 是一種可讓協力廠商應用程式代表使用者存取 Web 主控資源的方法。 任何與 Azure AD 整合的 Web 主控資源都具有資源識別碼 (或稱「應用程式識別碼 URI」)。 例如，Microsoft 的 Web 主控資源包括：

* hello Office 365 整合 Mail API:`https://outlook.office.com`
* hello Azure AD Graph API:`https://graph.windows.net`
* Microsoft Graph：`https://graph.microsoft.com`

hello 也適用於已整合 Azure AD 與任何第三方資源。 下列任何資源也可以定義一組權限可以使用的 toodivide hello 功能，該資源為較小區塊。 例如， [Microsoft Graph](https://graph.microsoft.io)已定義的權限 toodo hello 下列工作，和其他項目：

* 讀取使用者的行事曆
* 寫入 tooa 使用者的行事曆
* 以使用者身分傳送郵件

藉由定義這些類型的權限，hello 資源都有其資料和 hello 資料會公開方式更細微的控制。 協力廠商應用程式可以向應用程式使用者要求這些權限。 hello 應用程式使用者必須核准 hello 權限，才能代表 hello 使用者可採取動作 hello 應用程式。 切割成較小的權限集的 hello 資源的功能，由協力廠商應用程式可以是內建的 toorequest 只有 hello 特定權限所需 tooperform 其函式。 應用程式使用者可以知道應用程式將使用的確切方式其資料，並且可更確信該 hello 應用程式的行為不被用於惡意用途使用。

在 Azure AD 和 OAuth 中，這些類型的權限也稱為「範圍」。 它們有時也會參照的 tooas *oAuth2Permissions*。 在 Azure AD 中範圍會以字串值表示。 繼續 hello Microsoft Graph 範例，每個權限的 hello 範圍值是：

* 使用 `Calendar.Read` 來讀取使用者的行事曆
* 您可以使用撰寫 tooa 使用者的行事曆`Mail.ReadWrite`
* 使用 `Mail.Send` 來以使用者身分傳送郵件

應用程式可以藉由指定要求 toohello v2.0 端點中的 hello 範圍要求這些權限。

## <a name="openid-connect-scopes"></a>OpenId Connect 範圍
OpenID Connect hello v2.0 實作具有少數妥善定義的範圍，不會套用 tooa 特定資源： `openid`， `email`， `profile`，和`offline_access`。

### <a name="openid"></a>openid
如果應用程式執行登入使用[OpenID Connect](active-directory-v2-protocols.md)，則必須要求 hello`openid`範圍。 hello `openid` hello 工作帳戶的範圍顯示 hello 「 將您登入 」 權限的同意頁面和 hello 個人 Microsoft 帳戶的同意頁面為 hello"檢視您的設定檔及連接 tooapps 和使用您的 Microsoft 帳戶的服務 」 的權限。 這個權限，應用程式可以接收 hello 使用者的唯一識別碼 hello hello 形式`sub`宣告。 同時也提供 hello 應用程式存取 toohello 使用者資訊端點。 hello`openid`在 hello v2.0 權杖端點 tooacquire ID 語彙基元，它可以是使用的 toosecure HTTP 呼叫的應用程式的不同元件之間，就可以使用範圍。

### <a name="email"></a>電子郵件
hello`email`範圍可以搭配 hello`openid`領域和任何其他項目。 它提供 hello 應用程式存取 toohello 使用者的主要電子郵件地址 hello hello 形式`email`宣告。 hello`email`宣告已包含在權杖中，只有電子郵件地址是 hello 使用者帳戶，但不一定 hello 案例相關聯。 如果它使用 hello`email`範圍內，您的應用程式應該準備 toohandle 的案例中的 hello`email`宣告不存在於 hello 語彙基元。

### <a name="profile"></a>設定檔
hello`profile`範圍可以搭配 hello`openid`領域和任何其他項目。 它提供 hello 應用程式存取 tooa 大量的 hello 使用者的相關資訊。 它可以存取的 hello 資訊包括但不是會受限於至 hello 使用者的名字、 姓氏、 慣用的使用者名稱和物件識別碼。 Hello 設定檔宣告 hello id_tokens 參數中使用特定使用者的完整清單，請參閱 hello [v2.0 權杖參考](active-directory-v2-tokens.md)。

### <a name="offlineaccess"></a>offline_access
hello [ `offline_access`範圍](http://openid.net/specs/openid-connect-core-1_0.html#OfflineAccess)代表 hello 使用者提供您的應用程式存取 tooresources 相當長的時間。 在 hello 工作帳戶的同意頁面上，此範圍會顯示為 hello 「 隨時存取您的資料 」 的權限。 在 hello 個人 Microsoft 帳戶的同意頁面上，它會出現如下 hello 「 隨時存取您的資訊 」 權限。 當使用者核准 hello`offline_access`範圍內，您的應用程式可以接收來自 hello v2.0 權杖端點的重新整理權杖。 重新整理權杖是長期權杖。 您的應用程式可以在舊存取權杖到期時取得新的存取權杖。

如果您的應用程式沒有要求 hello`offline_access`範圍，它不會收到重新整理權杖。 這表示當兌換授權碼中 hello [OAuth 2.0 授權碼流程](active-directory-v2-protocols.md)，您將會收到只存取權杖來自 hello`/token`端點。 hello 存取權杖是有效的短時間。 hello 存取權杖通常會在一小時後到期。 此時，您的應用程式需要 tooredirect hello 使用者回復 toohello`/authorize`端點 tooget 新的授權碼。 這個重新導向，根據 hello 類型的應用程式，在 hello 使用者可能會再次需要 tooenter 他們的認證，或再次同意 toopermissions。

如需有關如何在 tooget 並使用重新整理權杖的詳細資訊，請參閱 hello [v2.0 通訊協定參考](active-directory-v2-protocols.md)。

## <a name="requesting-individual-user-consent"></a>要求個別使用者同意
在[OpenID Connect 或 OAuth 2.0](active-directory-v2-protocols.md)授權要求時，應用程式可以要求 hello 權限需要使用 hello`scope`查詢參數。 例如，當使用者登入時 tooan 應用程式，hello 應用程式將要求傳送 hello （使用加上換行以利閱讀） 下列範例類似：

```
GET https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&response_type=code
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&response_mode=query
&scope=
https%3A%2F%2Fgraph.microsoft.com%2Fcalendar.read%20
https%3A%2F%2Fgraph.microsoft.com%2Fmail.send
&state=12345
```

hello`scope`參數是以空格分隔清單的範圍 hello 應用程式的要求。 每個範圍會以附加 hello 範圍值 toohello 資源的識別項 (hello 應用程式識別碼 URI)。 在 hello 要求範例中，hello 應用程式需要使用權限 tooread hello 使用者的行事曆和 hello 使用者的身分傳送郵件。

Hello v2.0 端點 hello 使用者輸入其認證之後，會檢查的相符記錄*使用者同意*。 如果不同意 hello 使用者的 hello tooany 要求的權限在過去，hello hello v2.0 端點要求 hello 使用者 toogrant hello 要求的權限。

![工作帳戶同意](../../media/active-directory-v2-flows/work_account_consent.png)

當 hello 使用者核准 hello 權限時，如此 hello 使用者不需要 tooconsent 再次在後續的帳戶登入記錄 hello 同意。

## <a name="requesting-consent-for-an-entire-tenant"></a>要求整個租用戶的同意
通常，在組織購買的授權或訂用帳戶的應用程式，hello 組織會想為其員工 toofully 佈建 hello 應用程式。 此程序的一部分，系統管理員可以將同意授與 hello 應用程式 tooact 代表任何員工。 如果 hello 系統管理員授與 hello 整個租用戶的同意，hello 組織的員工就不會看見 hello 應用程式的同意頁面。

toorequest 同意的租用戶，您的應用程式中的所有使用者都可以使用 hello 系統管理員同意端點。

## <a name="admin-restricted-scopes"></a>受系統管理員限制的範圍
可以設定 hello Microsoft 生態系統中的某些高權限得*管理員限制*。 這類的範圍的範例包括下列權限的 hello:

* 使用 `Directory.Read` 來讀取組織的目錄資料
* 您可以使用撰寫資料 tooan 組織的目錄`Directory.ReadWrite`
* 使用 `Groups.Read.All` 來讀取組織目錄中的安全性群組

雖然取用者使用者集可能會授與應用程式存取 toothis 種類的資料，組織的使用者權限授與存取 toohello 相同設定的公司的機密資料。 如果您的應用程式會要求這些權限的存取 tooone 從組織的使用者，hello 使用者會收到錯誤訊息，指出它們不是授權的 tooconsent tooyour 應用程式的權限。

如果您的應用程式需要存取組織 tooadmin 限制領域，您應該要求它們直接從公司系統管理員，也使用 hello 系統管理員同意端點一節所說明。

當系統管理員授與這些權限透過 hello 系統管理員同意端點時，授與同意 hello 租用戶中的所有使用者。

## <a name="using-hello-admin-consent-endpoint"></a>使用 hello 系統管理員同意端點
如果您依照這些步驟，您的應用程式便能針對租用戶中所有的使用者收集權限，包括受系統管理員限制的範圍。 toosee 實作 hello 步驟的程式碼範例，請參閱 「 hello[管理員限制範圍範例](https://github.com/Azure-Samples/active-directory-dotnet-admin-restricted-scopes-v2)。

### <a name="request-hello-permissions-in-hello-app-registration-portal"></a>要求在 hello 應用程式註冊入口網站中的 hello 權限
1. 移 tooyour 應用程式在 hello[應用程式註冊入口網站](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)，或[建立應用程式](active-directory-v2-app-registration.md)如果尚未這麼做。
2. 找出 hello **Microsoft Graph 權限**區段，然後再新增您的應用程式所需的 hello 權限。
3. 請確定您**儲存**hello 應用程式註冊。

### <a name="recommended-sign-hello-user-in-tooyour-app"></a>建議使用： 號 hello 使用者 tooyour 應用程式中
一般而言，當您建置應用程式時，會使用 hello 系統管理員同意端點，hello 應用程式所需的頁面或檢視中的 hello 系統管理員可以核准 hello 應用程式的權限。 此頁面可以是 hello 應用程式註冊流程的一部分，一部分 hello 應用程式的設定，或它可以是專用，「 連接 」 流程。 在許多情況下，是合理的 hello 應用程式 tooshow 這 「 連接 」 檢視只能在使用者登入工作或學校的 Microsoft 帳戶之後。

當您登入時 hello tooyour 應用程式中的使用者時，您可以識別 hello 組織 toowhich hello 管理員所屬之前要求他們 tooapprove hello 必要的權限。 雖然這並非絕對必要，但這麼做可協助您為組織使用者建立更直覺式的體驗。 在後續的 toosign hello 使用者我們[v2.0 通訊協定教學課程](active-directory-v2-protocols.md)。

### <a name="request-hello-permissions-from-a-directory-admin"></a>從目錄管理員要求 hello 權限
當您準備好 toorequest 貴組織的管理員權限時，您可以重新導向 hello 使用者 toohello v2.0*系統管理員同意端點*。

```
// Line breaks are for legibility only.

GET https://login.microsoftonline.com/{tenant}/adminconsent?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&state=12345
&redirect_uri=http://localhost/myapp/permissions
```

```
// Pro tip: Try pasting hello below request in a browser!
```

```
https://login.microsoftonline.com/common/adminconsent?client_id=6731de76-14a6-49ae-97bc-6eba6914391e&state=12345&redirect_uri=http://localhost/myapp/permissions
```

| 參數 | 條件 | 說明 |
| --- | --- | --- |
| tenant |必要 |您想要從 toorequest 權限 hello 目錄租用戶。 可以採用 GUID 或易記名稱格式。 |
| client_id |必要 |hello 應用程式識別碼的 hello[應用程式註冊入口網站](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)指派 tooyour 應用程式。 |
| redirect_uri |必要 |hello 重新導向您想要針對應用程式 toohandle 傳送 hello 回應 toobe 的 URI。 它必須完全符合其中一個 hello 重新導向您 hello 應用程式註冊入口網站中註冊的 Uri。 |
| state |建議 |Hello 權杖回應中也會傳回的 hello 要求中包含一個值。 它可以是您想要的任何內容的字串。 發生 hello 驗證要求，例如 hello 頁面或檢視上之前，請使用 hello 應用程式中的 hello 使用者的狀態相關的 hello 狀態 tooencode 資訊。 |

此時，Azure AD 需要租用戶系統管理員 toosign toocomplete hello 要求中。 hello 系統管理員要求的 tooapprove 所有 hello 您要求的 hello 應用程式註冊入口網站中的應用程式的權限。

#### <a name="successful-response"></a>成功回應
如果 hello 系統管理員核准 hello 應用程式的權限，成功的回應 hello 看起來像這樣：

```
GET http://localhost/myapp/permissions?tenant=a8990e1f-ff32-408a-9f8e-78d3b9139b95&state=state=12345&admin_consent=True
```

| 參數 | 說明 |
| --- | --- | --- |
| tenant |hello 目錄租用戶授與您的應用程式 hello 權限要求，GUID 格式。 |
| state |將傳回 hello 權杖回應中的 hello 要求中包含一個值。 它可以是您想要的任何內容的字串。 hello 狀態是使用的 tooencode hello 應用程式中的 hello 使用者狀態資訊之前發生 hello 驗證要求，例如 hello 頁面或檢視上。 |
| admin_consent |將太**true**。 |

#### <a name="error-response"></a>錯誤回應
如果 hello 系統管理員不會核准 hello 應用程式的權限，hello 失敗回應看起來像這樣：

```
GET http://localhost/myapp/permissions?error=permission_denied&error_description=The+admin+canceled+the+request
```

| 參數 | 說明 |
| --- | --- | --- |
| 錯誤 |錯誤的程式碼字串是使用的 tooclassify 類型之錯誤的發生，且可以使用的 tooreact tooerrors。 |
| error_description |特定的錯誤訊息，可協助開發人員識別 hello 根本原因的錯誤。 |

收到 hello 系統管理員同意端點的成功回應之後，您的應用程式已取得它所要求的 hello 權限。 接下來，您可以要求您想要的 hello 資源語彙基元。

## <a name="using-permissions"></a>使用權限
Hello 使用者同意 toopermissions 應用程式之後，您的應用程式可以取得存取權杖，代表您的應用程式的權限 tooaccess 某些容量中的資源。 存取權杖可僅針對單一資源，但編碼 hello 存取權杖內為您的應用程式已被授與該資源的每個權限。 tooacquire 存取權杖，您的應用程式可以進行要求 toohello v2.0 權杖端點，就像這樣：

```
POST common/oauth2/v2.0/token HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/json

{
    "grant_type": "authorization_code",
    "client_id": "6731de76-14a6-49ae-97bc-6eba6914391e",
    "scope": "https://outlook.office.com/mail.read https://outlook.office.com/mail.send",
    "code": "AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq..."
    "redirect_uri": "https://localhost/myapp",
    "client_secret": "zc53fwe80980293klaj9823"  // NOTE: Only required for web apps
}
```

您可以使用 hello 產生的存取權杖中 HTTP 要求 toohello 資源。 它會可靠地指出 toohello 資源應用程式有 hello 適當的權限 tooperform 特定工作。  

如需有關 hello OAuth 2.0 通訊協定，以及如何 tooget 存取權杖，請參閱 hello [v2.0 端點通訊協定參考](active-directory-v2-protocols.md)。
