---
title: "Azure 管理-Microsoft 威脅模型化工具-aaaSession |Microsoft 文件"
description: "hello 威脅模型化工具中公開的威脅防護功能"
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: 915ffae3f775ca6902fcfb93e7e1952ce85612f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-session-management--articles"></a>安全性架構︰工作階段管理 | 文章 
| 產品/服務 | 文章 |
| --------------- | ------- |
| **Azure AD**    | <ul><li>[在使用 Azure AD 時以 ADAL 方法實作適當的登出](#logout-adal)</li></ul> |
| IoT 裝置 | <ul><li>[為產生的 SaS 權杖使用有限的存留期](#finite-tokens)</li></ul> |
| **Azure Document DB** | <ul><li>[為產生的資源權杖使用最短的權杖存留期](#resource-tokens)</li></ul> |
| **ADFS** | <ul><li>[在使用 ADFS 時以 WsFederation 方法實作適當的登出](#wsfederation-logout)</li></ul> |
| **Identity Server** | <ul><li>[在使用 Identity Server 時實作適當的登出](#proper-logout)</li></ul> |
| **Web 應用程式** | <ul><li>[透過 HTTPS 使用的應用程式必須使用安全 Cookie](#https-secure-cookies)</li><li>[所有 http 型應用程式只應在定義 Cookie 時指定 http](#cookie-definition)</li><li>[避免 ASP.NET 網頁上發生跨網站偽造要求 (CSRF) 攻擊](#csrf-asp)</li><li>[設定工作階段的閒置存留期](#inactivity-lifetime)</li><li>[實作從 hello 應用程式的適當登出](#proper-app-logout)</li></ul> |
| **Web API** | <ul><li>[避免 ASP.NET Web API 上發生跨網站偽造要求 (CSRF) 攻擊](#csrf-api)</li></ul> |

## <a id="logout-adal"></a>在使用 Azure AD 時以 ADAL 方法實作適當的登出

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Azure AD | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | N/A  |
| **步驟** | Hello 應用程式依賴 Azure AD 所發出存取權杖，如果應該呼叫 hello 登出事件處理常式 |

### <a name="example"></a>範例
```C#
HttpContext.GetOwinContext().Authentication.SignOut(OpenIdConnectAuthenticationDefaults.AuthenticationType, CookieAuthenticationDefaults.AuthenticationType)
```

### <a name="example"></a>範例
它應該也會藉由呼叫 Session.Abandon() 方法終結使用者的工作階段。 下列方法顯示使用者登出的安全實作︰
```C#
    [HttpPost]
        [ValidateAntiForgeryToken]
        public void LogOff()
        {
            string userObjectID = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier").Value;
            AuthenticationContext authContext = new AuthenticationContext(Authority + TenantId, new NaiveSessionCache(userObjectID));
            authContext.TokenCache.Clear();
            Session.Clear();
            Session.Abandon();
            Response.SetCookie(new HttpCookie("ASP.NET_SessionId", string.Empty));
            HttpContext.GetOwinContext().Authentication.SignOut(
                OpenIdConnectAuthenticationDefaults.AuthenticationType,
                CookieAuthenticationDefaults.AuthenticationType);
        } 
```

## <a id="finite-tokens"></a>為產生的 SaS 權杖使用有限的存留期

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | IoT 裝置 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | N/A  |
| **步驟** | 產生驗證 tooAzure IoT 中樞的 SaS 權杖應具有有限到期時間。 保留 hello SaS 權杖存留期 tooa 最小 toolimit hello 一段時間就可以重新執行以防 hello 語彙基元會隨即受到危害。|

## <a id="resource-tokens"></a>為產生的資源權杖使用最短的權杖存留期

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Azure Document DB | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | N/A  |
| **步驟** | 減少 hello timespan 的所需的資源權杖 tooa 最小值。 資源權杖有 1 小時的預設有效時間範圍。|

## <a id="wsfederation-logout"></a>在使用 ADFS 時以 WsFederation 方法實作適當的登出

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | ADFS | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | N/A  |
| **步驟** | 如果 hello 應用程式依賴 ADFS 所發出的 STS 權杖，hello 登出事件處理常式應該呼叫 WSFederationAuthenticationModule.FederatedSignOut() 方法 toolog 出 hello 使用者。 也 hello 目前工作階段應該予以終結，且應重設並 nullified hello 工作階段語彙基元值。|

### <a name="example"></a>範例
```C#
        [HttpPost, ValidateAntiForgeryToken]
        [Authorization]
        public ActionResult SignOut(string redirectUrl)
        {
            if (!this.User.Identity.IsAuthenticated)
            {
                return this.View("LogOff", null);
            }

            // Removes hello user profile.
            this.Session.Clear();
            this.Session.Abandon();
            HttpContext.Current.Response.Cookies.Add(new System.Web.HttpCookie("ASP.NET_SessionId", string.Empty)
                {
                    Expires = DateTime.Now.AddDays(-1D),
                    Secure = true,
                    HttpOnly = true
                });

            // Signs out at hello specified security token service (STS) by using hello WS-Federation protocol.
            Uri signOutUrl = new Uri(FederatedAuthentication.WSFederationAuthenticationModule.Issuer);
            Uri replyUrl = new Uri(FederatedAuthentication.WSFederationAuthenticationModule.Realm);
            if (!string.IsNullOrEmpty(redirectUrl))
            {
                replyUrl = new Uri(FederatedAuthentication.WSFederationAuthenticationModule.Realm + redirectUrl);
            }
           //     Signs out of hello current session and raises hello appropriate events.
            var authModule = FederatedAuthentication.WSFederationAuthenticationModule;
            authModule.SignOut(false);
        //     Signs out at hello specified security token service (STS) by using hello WS-Federation
        //     protocol.            
            WSFederationAuthenticationModule.FederatedSignOut(signOutUrl, replyUrl);
            return new RedirectResult(redirectUrl);
        }
```

## <a id="proper-logout"></a>在使用 Identity Server 時實作適當的登出

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Identity Server | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | [IdentityServer3-同盟登出](https://identityserver.github.io/Documentation/docsv2/advanced/federated-signout.html) |
| **步驟** | IdentityServer 支援 hello 能力 toofederate 外部識別提供者。 當使用者登出上游的身分識別提供者時，根據 hello 通訊協定，它可能 tooreceive 通知時可能 hello 使用者登出時。它可讓 IdentityServer toonotify 讓它們也可以登入其用戶端 hello 使用者登出。請檢查 hello hello 實作詳細資料的參考 > 一節中的 hello 文件集。|

## <a id="https-secure-cookies"></a>透過 HTTPS 使用的應用程式必須使用安全 Cookie

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Web 應用程式 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | EnvironmentType - OnPrem |
| **參考**              | [httpCookies 元素 (ASP.NET 設定結構描述)](http://msdn.microsoft.com/library/ms228262(v=vs.100).aspx)、[HttpCookie.Secure 屬性](http://msdn.microsoft.com/library/system.web.httpcookie.secure.aspx) |
| **步驟** | Cookie 通常是只會存取 toohello 才權杖的網域。 不幸的是，hello 的 「 網域 」 的定義不包含 hello 通訊協定，因此透過 HTTP 存取是透過 HTTPS 的 cookie。 hello 「 安全 」 屬性會指出 toohello hello cookie 的瀏覽器只應該可以使用透過 HTTPS。 請透過 HTTPS 設定的所有 cookie 都使用 hello**安全**屬性。 hello 需求可以藉由設定 hello requireSSL 屬性 tootrue 強制 hello web.config 檔案中。 它是 hello 慣用的方法，因為它將會強制執行 hello**安全**屬性的所有目前和未來 cookie hello 需要 toomake 沒有任何額外的程式碼變更。|

### <a name="example"></a>範例
```C#
<configuration>
  <system.web>
    <httpCookies requireSSL="true"/>
  </system.web>
</configuration>
```
即使 HTTP 是使用的 tooaccess hello 應用程式會強制執行 hello 設定。 如果使用 HTTP tooaccess hello 應用程式，並且讓 hello hello 應用程式因為 hello cookie 會以 hello 安全屬性和 hello 瀏覽器設定不會傳送它們的設定符號 toohello 應用程式。

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Web 應用程式 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | Web Form、MVC5 |
| **屬性**              | EnvironmentType - OnPrem |
| **參考**              | N/A  |
| **步驟** | 設定中的 requireSSL tooTrue 當 hello web 應用程式是 hello 信賴憑證者的合作對象，而且 hello IdP ADFS 伺服器時，可以設定 hello FedAuth 語彙基元的安全屬性`system.identityModel.services`web.config 的區段：|

### <a name="example"></a>範例
```C#
  <system.identityModel.services>
    <federationConfiguration>
      <!-- Set requireSsl=true; domain=application domain name used by FedAuth cookies (Ex: .gdinfra.com); -->
      <cookieHandler requireSsl="true" persistentSessionLifetime="0.0:20:0" />
    ....  
    </federationConfiguration>
  </system.identityModel.services>
```

## <a id="cookie-definition"></a>所有 http 型應用程式只應在定義 Cookie 時指定 http

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Web 應用程式 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | [安全 Cookie 屬性](https://en.wikipedia.org/wiki/HTTP_cookie#Secure_cookie) |
| **步驟** | toomitigate hello 風險資訊洩露跨網站指令碼 (XSS) 攻擊的新屬性-httpOnly-已導入了的 toocookies 和支援的所有主要瀏覽器。 hello 屬性會指定 cookie 不是可透過指令碼存取。 藉由使用 HttpOnly cookie，web 應用程式會降低 hello 可能性 hello cookie 中包含機密資訊可以透過指令碼遭竊，並且傳送 tooan 攻擊者的網站。 |

### <a name="example"></a>範例
所有以 HTTP 為基礎的應用程式使用 cookie 應該在 hello cookie 定義中，指定 HttpOnly 藉由實作下列 web.config 中的組態：
```XML
<system.web>
.
.
   <httpCookies requireSSL="false" httpOnlyCookies="true"/>
.
.
</system.web>
```

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Web 應用程式 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | Web Form |
| **屬性**              | N/A  |
| **參考**              | [FormsAuthentication.RequireSSL 屬性](https://msdn.microsoft.com/library/system.web.security.formsauthentication.requiressl.aspx) |
| **步驟** | hello RequireSSL 屬性值是使用 hello requireSSL 屬性 hello 組態項目之 hello ASP.NET 應用程式的組態檔中設定。 您可以指定 hello Web.config 檔案中的 ASP.NET 應用程式是否 SSL （安全通訊端層） 是必要的 tooreturn hello 表單驗證 cookie toohello 伺服器設定 hello requireSSL 屬性。|

### <a name="example"></a>範例 
hello 下列程式碼範例會設定 hello requireSSL 屬性 hello Web.config 檔案中。
```XML
<authentication mode="Forms">
  <forms loginUrl="member_login.aspx" cookieless="UseCookies" requireSSL="true"/>
</authentication>
```

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Web 應用程式 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | MVC5 |
| **屬性**              | EnvironmentType - OnPrem |
| **參考**              | [Windows Identity Foundation (WIF) 組態 - 單元二](https://blogs.msdn.microsoft.com/alikl/2011/02/01/windows-identity-foundation-wif-configuration-part-ii-cookiehandler-chunkedcookiehandler-customcookiehandler/) |
| **步驟** | FedAuth cookie 的 tooset httpOnly 屬性 hideFromCsript 屬性值應該設定 tooTrue。 |

### <a name="example"></a>範例
下列組態會顯示 hello 正確的組態：
```XML
<federatedAuthentication>
<cookieHandler mode="Custom"
                       hideFromScript="true"
                       name="FedAuth"
                       path="/"
                       requireSsl="true"
                       persistentSessionLifetime="25">
</cookieHandler>
</federatedAuthentication>
```

## <a id="csrf-asp"></a>避免 ASP.NET 網頁上發生跨網站偽造要求 (CSRF) 攻擊

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Web 應用程式 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | N/A  |
| **步驟** | 跨站台要求偽造 （CSRF 或 XSRF） 是一種攻擊，攻擊者可以按照 hello 安全性內容中的網站上不同的使用者建立之工作階段的動作。 hello 目標 toomodify 或刪除的內容，如果目標的網站 hello 完全依賴工作階段 cookie tooauthenticate 接收的要求。 攻擊者取得不同使用者的瀏覽器 tooload 命令使用的 URL 從易受攻擊的站台所在 hello 使用者已經登入，以利用這項弱點。 有很多種，例如藉由主控不同的網站，載入資源從 hello 弱點的伺服器或取得 hello 使用者 tooclick 連結攻擊者 toodo 的。 如果 hello 伺服器傳送其他語彙基元 toohello 用戶端，需要 hello 用戶端 tooinclude 中所有未來的要求，該語彙基元，並確認所有未來的要求，包括相關 toohello 目前工作階段，例如由語彙基元，就可以避免 hello 攻擊使用 ASP.NET AntiForgeryToken hello 或 ViewState。 |

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Web 應用程式 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | MVC5、MVC6 |
| **屬性**              | N/A  |
| **參考**              | [在 ASP.NET MVC 和網頁中防止 XSRF/CSRF](http://www.asp.net/mvc/overview/security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages) |
| **步驟** | 反 CSRF 和 ASP.NET MVC form-使用 hello`AntiForgeryToken`檢視上的協助程式方法; put `Html.AntiForgeryToken()` hello 表單，例如，|

### <a name="example"></a>範例
```C#
@using (Html.BeginForm("UserProfile", "SubmitUpdate")) { 
    @Html.ValidationSummary(true) 
    @Html.AntiForgeryToken()
    <fieldset> 
```

### <a name="example"></a>範例
```C#
<form action="/UserProfile/SubmitUpdate" method="post">
    <input name="__RequestVerificationToken" type="hidden" value="saTFWpkKN0BYazFtN6c4YbZAmsEwG0srqlUqqloi/fVgeV2ciIFVmelvzwRZpArs" />
    <!-- rest of form goes here -->
</form>
```

### <a name="example"></a>範例
在 hello 相同的時間，Html.AntiForgeryToken() 提供 hello 訪客 cookie 呼叫 __RequestVerificationToken，以相同的值 hello 隨機的 hidden 值如上所示為 hello。 接下來，toovalidate 連入的表單張貼加入 hello [ValidateAntiForgeryToken] 篩選 toohello 目標動作方法。 例如：
```
[ValidateAntiForgeryToken]
public ViewResult SubmitUpdate()
{
// ... etc.
}
```
授權篩選會確認︰
* hello 連入要求具有稱為 __RequestVerificationToken cookie
* hello 傳入的要求有`Request.Form`呼叫 __RequestVerificationToken 的項目
* 這些 cookie 和`Request.Form`假設所有的值符合目前、 hello 要求會透過正常。 但如果沒有，則授權會失敗並出現訊息「未提供必要的防偽權杖或權杖無效」。 

### <a name="example"></a>範例
反 CSRF 和 AJAX: hello 表單語彙基元可能 AJAX 要求的問題，因為 AJAX 要求可能會傳送 JSON 資料，HTML 表單資料。 一個解決方案是自訂的 HTTP 標頭中的 toosend hello 語彙基元。 hello 下列程式碼會使用 Razor 語法 toogenerate hello token，然後新增 hello 語彙基元 tooan AJAX 要求。 
```C#
<script>
    @functions{
        public string TokenHeaderValue()
        {
            string cookieToken, formToken;
            AntiForgery.GetTokens(null, out cookieToken, out formToken);
            return cookieToken + ":" + formToken;                
        }
    }

    $.ajax("api/values", {
        type: "post",
        contentType: "application/json",
        data: {  }, // JSON data goes here
        dataType: "json",
        headers: {
            'RequestVerificationToken': '@TokenHeaderValue()'
        }
    });
</script>
```

### <a name="example"></a>範例
當您處理 hello 要求時，請從 hello 要求標頭中擷取 hello 語彙基元。 然後呼叫 hello AntiForgery.Validate 方法 toovalidate hello 語彙基元。 hello Validate 方法會擲回例外狀況，如果 hello 語彙基元無效。
```C#
void ValidateRequestHeader(HttpRequestMessage request)
{
    string cookieToken = "";
    string formToken = "";

    IEnumerable<string> tokenHeaders;
    if (request.Headers.TryGetValues("RequestVerificationToken", out tokenHeaders))
    {
        string[] tokens = tokenHeaders.First().Split(':');
        if (tokens.Length == 2)
        {
            cookieToken = tokens[0].Trim();
            formToken = tokens[1].Trim();
        }
    }
    AntiForgery.Validate(cookieToken, formToken);
}
```

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Web 應用程式 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | Web Form |
| **屬性**              | N/A  |
| **參考**              | [需要利用的 ASP.NET 內建功能 tooFend 關閉 Web 攻擊](https://msdn.microsoft.com/library/ms972969.aspx#securitybarriers_topic2) |
| **步驟** | 藉由設定 ViewStateUserKey tooa 隨機字串而異的每個使用者-使用者識別碼，就可以緩解 CSRF 攻擊 WebForm 基礎應用程式中的，或更棒的是，工作階段識別碼。 基於諸多技術和社交方面的原因，工作階段識別碼會比較適合，因為工作階段識別碼無法預料、會逾時，而且會隨每個使用者而有所不同。|

### <a name="example"></a>範例
以下是您在所有的網頁需要 toohave hello 程式碼：
```C#
void Page_Init (object sender, EventArgs e) {
   ViewStateUserKey = Session.SessionID;
   :
}
```

## <a id="inactivity-lifetime"></a>設定工作階段的閒置存留期

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Web 應用程式 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | [HttpSessionState.Timeout 屬性](https://msdn.microsoft.com/library/system.web.sessionstate.httpsessionstate.timeout(v=vs.110).aspx) |
| **步驟** | 工作階段逾時表示 hello 事件時所發生使用者不會執行任何動作在網站上在間隔內 （web 伺服器所定義）。 hello 事件，在伺服器端上的，變更 hello 使用者工作階段 too'invalid hello 狀態 ' （例如 「 不使用不再 」），並指示 hello web 伺服器 toodestroy 它 （刪除到它所包含的所有資料）。 hello 下列程式碼範例會設定 hello 逾時工作階段屬性 too15 分鐘數 hello Web.config 檔案中。|

### <a name="example"></a>範例
```XML 程式碼 <configuration> <system.web> <sessionState mode="InProc" cookieless="true" timeout="15" /> </system.web> </configuration>
```

## <a id="threat-detection"></a>Enable Threat detection on Azure SQL
```

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Web 應用程式 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | Web Form |
| **屬性**              | N/A  |
| **參考**              | [用於驗證的表單元素 (ASP.NET 設定結構描述)](https://msdn.microsoft.com/library/1d3t3c61(v=vs.100).aspx) |
| **步驟** | 設定表單驗證票證 cookie 逾時 too15 hello 分鐘|

### <a name="example"></a>範例
```XML 程式碼 <forms  name=".ASPXAUTH" loginUrl="login.aspx"  defaultUrl="default.aspx" protection="All" timeout="15" path="/" requireSSL="true" slidingExpiration="true"/>
</forms>
```

| Title                   | Details      |
| ----------------------- | ------------ |
| **Component**               | Web Application | 
| **SDL Phase**               | Build |  
| **Applicable Technologies** | Web Forms, MVC5 |
| **Attributes**              | EnvironmentType - OnPrem |
| **References**              | [asdeqa](https://skf.azurewebsites.net/Mitigations/Details/wefr) |
| **Steps** | When hello web application is Relying Party and ADFS is hello STS, hello lifetime of hello authentication cookies - FedAuth tokens - can be set by hello following configuration in web.config:|

### Example
```XML
  <system.identityModel.services>
    <federationConfiguration>
      <!-- Set requireSsl=true; domain=application domain name used by FedAuth cookies (Ex: .gdinfra.com); -->
      <cookieHandler requireSsl="true" persistentSessionLifetime="0.0:15:0" />
      <!-- Set requireHttps=true; -->
      <wsFederation passiveRedirectEnabled="true" issuer="http://localhost:39529/" realm="https://localhost:44302/" reply="https://localhost:44302/" requireHttps="true"/>
      <!--
      Use hello code below tooenable encryption-decryption of claims received from ADFS. Thumbprint value varies based on hello certificate being used.
      <serviceCertificate>
        <certificateReference findValue="4FBBBA33A1D11A9022A5BF3492FF83320007686A" storeLocation="LocalMachine" storeName="My" x509FindType="FindByThumbprint" />
      </serviceCertificate>
      -->
    </federationConfiguration>
  </system.identityModel.services>
```

### <a name="example"></a>範例
也 hello too15 應該設定發行 SAML 宣告權杖的存留期的 ADFS 分鐘，執行下列 powershell 命令 hello ADFS 伺服器上的 hello:
```C#
Set-ADFSRelyingPartyTrust -TargetName “<RelyingPartyWebApp>” -ClaimsProviderName @(“Active Directory”) -TokenLifetime 15 -AlwaysRequireAuthentication $true
```

## <a id="proper-app-logout"></a>實作從 hello 應用程式的適當登出

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Web 應用程式 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | N/A  |
| **步驟** | 當使用者按下登出按鈕時執行適當登出從 hello 的應用程式。 在登出時，應用程式應終結使用者的工作階段，同時重設工作階段 Cookie 值並讓其變成空值，以及重設驗證 cookie 值並讓其變成空值。 此外，當多個工作階段繫結的 tooa 單一使用者身分識別時，它們必須共同結束 hello 伺服器端逾時或登出。 最後，請確定每個頁面都可使用登出功能。 |

## <a id="csrf-api"></a>避免 ASP.NET Web API 上發生跨網站偽造要求 (CSRF) 攻擊

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Web API | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | N/A  |
| **步驟** | 跨站台要求偽造 （CSRF 或 XSRF） 是一種攻擊，攻擊者可以按照 hello 安全性內容中的網站上不同的使用者建立之工作階段的動作。 hello 目標 toomodify 或刪除的內容，如果目標的網站 hello 完全依賴工作階段 cookie tooauthenticate 接收的要求。 攻擊者取得不同使用者的瀏覽器 tooload 命令使用的 URL 從易受攻擊的站台所在 hello 使用者已經登入，以利用這項弱點。 有很多種，例如藉由主控不同的網站，載入資源從 hello 弱點的伺服器或取得 hello 使用者 tooclick 連結攻擊者 toodo 的。 如果 hello 伺服器傳送其他語彙基元 toohello 用戶端，需要 hello 用戶端 tooinclude 中所有未來的要求，該語彙基元，並確認所有未來的要求，包括相關 toohello 目前工作階段，例如由語彙基元，就可以避免 hello 攻擊使用 ASP.NET AntiForgeryToken hello 或 ViewState。 |

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Web API | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | MVC5、MVC6 |
| **屬性**              | N/A  |
| **參考**              | [避免 ASP.NET Web API 中發生跨網站偽造要求 (CSRF) 攻擊](http://www.asp.net/web-api/overview/security/preventing-cross-site-request-forgery-csrf-attacks) |
| **步驟** | 反 CSRF 和 AJAX: hello 表單語彙基元可能 AJAX 要求的問題，因為 AJAX 要求可能會傳送 JSON 資料，HTML 表單資料。 一個解決方案是自訂的 HTTP 標頭中的 toosend hello 語彙基元。 hello 下列程式碼會使用 Razor 語法 toogenerate hello token，然後新增 hello 語彙基元 tooan AJAX 要求。 |

### <a name="example"></a>範例
```Javascript
<script>
    @functions{
        public string TokenHeaderValue()
        {
            string cookieToken, formToken;
            AntiForgery.GetTokens(null, out cookieToken, out formToken);
            return cookieToken + ":" + formToken;                
        }
    }
    $.ajax("api/values", {
        type: "post",
        contentType: "application/json",
        data: {  }, // JSON data goes here
        dataType: "json",
        headers: {
            'RequestVerificationToken': '@TokenHeaderValue()'
        }
    });
</script>
```

### <a name="example"></a>範例
當您處理 hello 要求時，請從 hello 要求標頭中擷取 hello 語彙基元。 然後呼叫 hello AntiForgery.Validate 方法 toovalidate hello 語彙基元。 hello Validate 方法會擲回例外狀況，如果 hello 語彙基元無效。
```C#
void ValidateRequestHeader(HttpRequestMessage request)
{
    string cookieToken = "";
    string formToken = "";

    IEnumerable<string> tokenHeaders;
    if (request.Headers.TryGetValues("RequestVerificationToken", out tokenHeaders))
    {
        string[] tokens = tokenHeaders.First().Split(':');
        if (tokens.Length == 2)
        {
            cookieToken = tokens[0].Trim();
            formToken = tokens[1].Trim();
        }
    }
    AntiForgery.Validate(cookieToken, formToken);
}
```

### <a name="example"></a>範例
反 CSRF 和 ASP.NET MVC form-使用 hello AntiForgeryToken 檢視; 上的協助程式方法例如，將 Html.AntiForgeryToken() 放入 hello 表單
```C#
@using (Html.BeginForm("UserProfile", "SubmitUpdate")) { 
    @Html.ValidationSummary(true) 
    @Html.AntiForgeryToken()
    <fieldset> 
}
```

### <a name="example"></a>範例
hello 上述範例中會輸出 hello 下列類似：
```C#
<form action="/UserProfile/SubmitUpdate" method="post">
    <input name="__RequestVerificationToken" type="hidden" value="saTFWpkKN0BYazFtN6c4YbZAmsEwG0srqlUqqloi/fVgeV2ciIFVmelvzwRZpArs" />
    <!-- rest of form goes here -->
</form>
```

### <a name="example"></a>範例
在 hello 相同的時間，Html.AntiForgeryToken() 提供 hello 訪客 cookie 呼叫 __RequestVerificationToken，以相同的值 hello 隨機的 hidden 值如上所示為 hello。 接下來，toovalidate 連入的表單張貼加入 hello [ValidateAntiForgeryToken] 篩選 toohello 目標動作方法。 例如：
```
[ValidateAntiForgeryToken]
public ViewResult SubmitUpdate()
{
// ... etc.
}
```
授權篩選會確認︰
* hello 連入要求具有稱為 __RequestVerificationToken cookie
* hello 傳入的要求有`Request.Form`呼叫 __RequestVerificationToken 的項目
* 這些 cookie 和`Request.Form`假設所有的值符合目前、 hello 要求會透過正常。 但如果沒有，則授權會失敗並出現訊息「未提供必要的防偽權杖或權杖無效」。

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Web API | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | MVC5、MVC6 |
| **屬性**              | 識別提供者 - ADFS、識別提供者 - Azure AD |
| **參考**              | [在 ASP.NET Web API 2.2 中使用個別帳戶和本機登入保護 Web API](http://www.asp.net/web-api/overview/security/individual-accounts-in-web-api) |
| **步驟** | 如果 hello Web API 受到使用 OAuth 2.0，則預期持有人權杖授權要求標頭和授與存取 toohello 要求中，只有當 hello 權杖是有效的。 不同於以 cookie 為基礎的驗證，瀏覽器不要附加 hello 持有人權杖 toorequests。 hello 要求用戶端必須 tooexplicitly 附加 hello 要求標頭中的 hello 持有人權杖。 因此，對於使用 OAuth 2.0 來保護的 ASP.NET Web API，會將持有人權杖視為 CSRF 攻擊的防禦手段。 請注意，是否 hello MVC 部分 hello 應用程式會使用表單驗證 (也就是使用 cookie)，防偽語彙基元會有 toobe hello MVC web 應用程式使用。 |

### <a name="example"></a>範例
hello Web API 有 toobe 通知 toorely 僅限持有者權杖，而不是在 cookie。 由下列組態中的 hello`WebApiConfig.Register`方法: '' C-sharp 程式碼設定。SuppressDefaultHostAuthentication();組態。Filters.Add (新 HostAuthenticationFilter(OAuthDefaults.AuthenticationType));
```
hello SuppressDefaultHostAuthentication method tells Web API tooignore any authentication that happens before hello request reaches hello Web API pipeline, either by IIS or by OWIN middleware. That way, we can restrict Web API tooauthenticate only using bearer tokens.
