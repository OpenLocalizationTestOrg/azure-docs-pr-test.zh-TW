---
title: "Azure 管理-Microsoft 威脅模型化工具-aaaException |Microsoft 文件"
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
ms.openlocfilehash: 247096c10deeca94ebb9b19df7ba60e442ca1e4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-exception-management--mitigations"></a>安全性架構︰例外狀況管理 | 風險降低 
| 產品/服務 | 文章 |
| --------------- | ------- |
| **WCF** | <ul><li>[WCF - 請勿在組態檔中包含 serviceDebug 節點](#servicedebug)</li><li>[WCF - 請勿在組態檔中包含 serviceMetadata 節點](#servicemetadata)</li></ul> |
| **Web API** | <ul><li>[確定有在 ASP.NET Web API 中正確處理例外狀況](#exception)</li></ul> |
| **Web 應用程式** | <ul><li>[請勿在錯誤訊息中公開安全性詳細資料](#messages)</li><li>[實作預設的錯誤處理頁面](#default)</li><li>[在 IIS 中設定的部署方法 tooRetail](#deployment)</li><li>[例外狀況應安全地失敗](#fail)</li></ul> |

## <a id="servicedebug"></a>WCF - 請勿在組態檔中包含 serviceDebug 節點

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | WCF | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型、NET Framework 3 |
| **屬性**              | N/A  |
| **參考**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx)、[Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html) |
| **步驟** | Windows Communication Framework (WCF) 服務可以設定的 tooexpose 偵錯資訊。 偵錯資訊不應用於生產環境。 hello`<serviceDebug>`標記定義 hello 偵錯資訊的功能是否已啟用 WCF 服務。 如果 hello 屬性 includeExceptionDetailInFaults 設定 tootrue，例外狀況資訊從 hello 應用程式將會傳回 tooclients。 攻擊者可以利用 hello 他們會取得從偵錯輸出 toomount 攻擊目標 hello framework、 資料庫或 hello 應用程式所使用的其他資源的其他資訊。 |

### <a name="example"></a>範例
hello 下列組態檔包含 hello`<serviceDebug>`標記： 
```
<configuration> 
<system.serviceModel> 
<behaviors> 
<serviceBehaviors> 
<behavior name=""MyServiceBehavior""> 
<serviceDebug includeExceptionDetailInFaults=""True"" httpHelpPageEnabled=""True""/> 
... 
```
停用偵錯資訊置於 hello 服務。 這可藉由移除 hello`<serviceDebug>`從您的應用程式組態檔的標記。 

## <a id="servicemetadata"></a>WCF - 請勿在組態檔中包含 serviceMetadata 節點

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | WCF | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | 泛型、NET Framework 3 |
| **參考**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx)、[Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html) |
| **步驟** | 公開服務的相關資訊，可提供與重要深入了解它們如何利用 hello 服務的攻擊者。 hello`<serviceMetadata>`標記啟用 hello 中繼資料發行功能。 服務中繼資料可能包含不應開放存取的敏感性資訊。 最小值，只允許 tooaccess hello 中繼資料，並確認不必要的資訊不會公開受信任的使用者。 更棒的是，完全停用 hello 能力 toopublish 中繼資料。 安全的 WCF 組態將不會包含 hello`<serviceMetadata>`標記。 |

## <a id="exception"></a>確定有在 ASP.NET Web API 中正確處理例外狀況

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Web API | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | MVC 5、MVC 6 |
| **屬性**              | N/A  |
| **參考**              | [ASP.NET Web API 中的例外狀況處理](http://www.asp.net/web-api/overview/error-handling/exception-handling)、[ASP.NET Web API 中的模型驗證](http://www.asp.net/web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api) |
| **步驟** | 根據預設，ASP.NET Web API 中大多數未攔截到的例外狀況會轉譯成狀態碼為 `500, Internal Server Error` 的 HTTP 回應|

### <a name="example"></a>範例
hello API，所傳回的 toocontrol hello 狀態碼`HttpResponseException`可以使用如下所示： 
```C#
public Product GetProduct(int id)
{
    Product item = repository.Get(id);
    if (item == null)
    {
        throw new HttpResponseException(HttpStatusCode.NotFound);
    }
    return item;
}
```

### <a name="example"></a>範例
進一步控制 hello 例外狀況的回應，hello`HttpResponseMessage`可以使用類別，如下所示： 
```C#
public Product GetProduct(int id)
{
    Product item = repository.Get(id);
    if (item == null)
    {
        var resp = new HttpResponseMessage(HttpStatusCode.NotFound)
        {
            Content = new StringContent(string.Format("No product with ID = {0}", id)),
            ReasonPhrase = "Product ID Not Found"
        }
        throw new HttpResponseException(resp);
    }
    return item;
}
```
toocatch 未處理的例外狀況，不是 hello 型別`HttpResponseException`，可以使用例外狀況篩選條件。 例外狀況篩選條件實作 hello`System.Web.Http.Filters.IExceptionFilter`介面。 最簡單方式 toowrite hello 例外狀況篩選條件是從 hello tooderive`System.Web.Http.Filters.ExceptionFilterAttribute`類別並覆寫 hello OnException 方法。 

### <a name="example"></a>範例
以下是會將 `NotImplementedException` 例外狀況轉換成 HTTP 狀態碼 `501, Not Implemented` 的篩選： 
```C#
namespace ProductStore.Filters
{
    using System;
    using System.Net;
    using System.Net.Http;
    using System.Web.Http.Filters;

    public class NotImplExceptionFilterAttribute : ExceptionFilterAttribute 
    {
        public override void OnException(HttpActionExecutedContext context)
        {
            if (context.Exception is NotImplementedException)
            {
                context.Response = new HttpResponseMessage(HttpStatusCode.NotImplemented);
            }
        }
    }
}
```

有數種方式 tooregister Web API 的例外狀況篩選條件：
- 透過動作
- 透過控制器
- 全域

### <a name="example"></a>範例
tooapply hello 篩選 tooa 特定動作，為屬性 toohello 動作加入 hello 篩選： 
```C#
public class ProductsController : ApiController
{
    [NotImplExceptionFilter]
    public Contact GetContact(int id)
    {
        throw new NotImplementedException("This method is not implemented");
    }
}
```
### <a name="example"></a>範例
hello 上之動作的 tooapply hello 篩選 tooall `controller`，做為屬性 toohello 加入 hello 篩選`controller`類別： 

```C#
[NotImplExceptionFilter]
public class ProductsController : ApiController
{
    // ...
}
```

### <a name="example"></a>範例
tooapply hello 全域篩選 tooall Web API 控制器，將執行個體的 hello 篩選 toohello`GlobalConfiguration.Configuration.Filters`集合。 在此集合中的例外狀況篩選條件套用 tooany Web API 控制器動作。 
```C#
GlobalConfiguration.Configuration.Filters.Add(
    new ProductStore.NotImplExceptionFilterAttribute());
```

### <a name="example"></a>範例
模型驗證 hello 模型狀態可以傳遞 tooCreateErrorResponse 方法如下所示： 
```C#
public HttpResponseMessage PostProduct(Product item)
{
    if (!ModelState.IsValid)
    {
        return Request.CreateErrorResponse(HttpStatusCode.BadRequest, ModelState);
    }
    // Implementation not shown...
}
```

如需詳細資訊，關於例外狀況處理 hello 參考一節中的 hello 連結和 ASP.Net Web API 中的模型驗證檢查 

## <a id="messages"></a>請勿在錯誤訊息中公開安全性詳細資料

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Web 應用程式 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | N/A  |
| **步驟** | <p>一般錯誤訊息會提供直接 toohello 使用者但不包含機密的應用程式資料。 敏感性資料的範例包括︰</p><ul><li>伺服器名稱</li><li>連接字串</li><li>使用者名稱</li><li>密碼</li><li>SQL 程序</li><li>動態 SQL 失敗的詳細資料</li><li>堆疊追蹤和程式碼行</li><li>儲存在記憶體中的變數</li><li>磁碟機和資料夾的位置</li><li>應用程式的安裝點</li><li>主機組態設定</li><li>其他內部應用程式詳細資料</li></ul><p>捕捉應用程式中的所有錯誤並提供泛型錯誤訊息，以及啟用 IIS 中的自訂錯誤，將有助於避免資訊外洩。 SQL Server 資料庫和.NET 例外狀況處理、 在其他錯誤處理架構，會特別的詳細資訊，非常有用的 tooa 惡意使用者程式碼剖析應用程式。 無法直接顯示 hello 的類別內容衍生自 hello.NET 例外狀況類別，並確定您有適當的例外狀況處理，好讓不小心未預期的例外狀況直接引發 toohello 使用者執行。</p><ul><li>提供一般錯誤訊息直接 toohello 取出離開直接在 hello 例外狀況/錯誤訊息中找到的特定詳細資料的使用者</li><li>不顯示 hello 內容.NET 例外狀況類別直接 toohello 使用者嗎</li><li>設陷所有錯誤訊息，並視通知 hello 使用者透過一般錯誤訊息傳送的 toohello 應用程式用戶端</li><li>不會公開 hello 內容 hello 例外狀況類別直接 toohello 使用者特別 hello 傳回的值從`.ToString()`，或 hello hello 訊息或 StackTrace 屬性值。 安全地記錄此資訊並顯示更無害的訊息 toohello 使用者</li></ul>|

## <a id="default"></a>實作預設的錯誤處理頁面

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Web 應用程式 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | [編輯 ASP.NET 錯誤頁面設定對話方塊](https://technet.microsoft.com/library/dd569096(WS.10).aspx) |
| **步驟** | <p>當 ASP.NET 應用程式失敗並造成 HTTP/1.x 500 內部伺服器錯誤時，或當功能組態 (例如要求篩選) 避免顯示頁面時，就會產生錯誤訊息。 系統管理員可以選擇 hello 應用程式應該會顯示易記訊息 toohello 用戶端、 詳細的錯誤訊息 toohello 用戶端或詳細的錯誤訊息 toolocalhost 只。 hello <customErrors> hello web.config 中的標記具有三種模式：</p><ul><li>**開啟︰**指定要啟用自訂錯誤。 如果未指定任何 defaultRedirect 屬性，則使用者會看到泛型錯誤。 hello 自訂錯誤會顯示 toohello 遠端用戶端和 toohello 本機主機</li><li>**關閉︰**指定要停用自訂錯誤。 hello 詳細的 ASP.NET 錯誤會顯示 toohello 遠端用戶端和 toohello 本機主機</li><li>**RemoteOnly:**指定自訂的錯誤會顯示只有 toohello 遠端用戶端，以及 ASP.NET 錯誤會顯示 toohello 本機主機。 這是 hello 預設值</li></ul><p>開啟 hello `web.config` hello 應用程式/網站的檔案，並確定 hello 標記有 `<customErrors mode="RemoteOnly" />`或`<customErrors mode="On" />`定義。</p>|

## <a id="deployment"></a>在 IIS 中設定的部署方法 tooRetail

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Web 應用程式 | 
| **SDL 階段**               | 部署 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | [部署元素 (ASP.NET 設定結構描述)](https://msdn.microsoft.com/library/ms228298(VS.80).aspx) |
| **步驟** | <p>hello`<deployment retail>`交換器適用於實際執行的 IIS 伺服器。 這個參數是使用的 toohelp 應用程式執行與 hello 最佳效能，並停用 leakages hello 在頁面上，停用 hello 能力 toodisplay 應用程式的能力 toogenerate 追蹤輸出的最少安全性資訊詳細錯誤訊息 tooend 使用者，並停用 hello 偵錯參數。</p><p>在開發期間，經常會啟用專供開發人員使用的參數和選項，例如失敗要求追蹤和偵錯。 建議您在任何實際執行伺服器上的 hello 部署方法，設定 tooretail。 開啟 hello machine.config 檔案，並確定`<deployment retail="true" />`會設定 tootrue。</p>|

## <a id="fail"></a>例外狀況應安全地失敗

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Web 應用程式 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | [安全地失敗](https://www.owasp.org/index.php/Fail_securely) |
| **步驟** | 應用程式應安全地失敗。 任何會傳回布林值的方法 (根據所做出的特定決策) 皆應小心地建立例外狀況區塊。 有許多到期，請在 hello 例外狀況區塊會寫入時後果 toowhich 安全性問題蔓延的邏輯錯誤。|

### <a name="example"></a>範例
```C#
        public static bool ValidateDomain(string pathToValidate, Uri currentUrl)
        {
            try
            {
                if (!string.IsNullOrWhiteSpace(pathToValidate))
                {
                    var domain = RetrieveDomain(currentUrl);
                    var replyPath = new Uri(pathToValidate);
                    var replyDomain = RetrieveDomain(replyPath);

                    if (string.Compare(domain, replyDomain, StringComparison.OrdinalIgnoreCase) != 0)
                    {
                        //// Adding additional check tooenable CMS urls if they are not hosted on same domain.
                        if (!string.IsNullOrWhiteSpace(Utilities.CmsBase))
                        {
                            var cmsDomain = RetrieveDomain(new Uri(Utilities.Base.Trim()));
                            if (string.Compare(cmDomain, replyDomain, StringComparison.OrdinalIgnoreCase) != 0)
                            {
                                return false;
                            }
                            else
                            {
                                return true;
                            }
                        }

                        return false;
                    }
                }

                return true;
            }
            catch (UriFormatException ex)
            {
                LogHelper.LogException("Utilities:ValidateDomain", ex);
                return true;
            }
        }
```
方法的上方 hello 一定會傳回 True，如果某些例外狀況。 如果 hello 終端使用者提供的格式不正確的 URL，hello 瀏覽器方面，但 hello`Uri()`建構函式不會這將會擲回例外狀況，以及應採取 hello 犧牲者 toohello 有效但格式不正確的 URL。 
