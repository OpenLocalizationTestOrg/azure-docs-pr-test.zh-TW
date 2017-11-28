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
# <a name="security-frame-exception-management--mitigations"></a><span data-ttu-id="1ee73-103">安全性架構︰例外狀況管理 | 風險降低</span><span class="sxs-lookup"><span data-stu-id="1ee73-103">Security Frame: Exception Management | Mitigations</span></span> 
| <span data-ttu-id="1ee73-104">產品/服務</span><span class="sxs-lookup"><span data-stu-id="1ee73-104">Product/Service</span></span> | <span data-ttu-id="1ee73-105">文章</span><span class="sxs-lookup"><span data-stu-id="1ee73-105">Article</span></span> |
| --------------- | ------- |
| <span data-ttu-id="1ee73-106">**WCF**</span><span class="sxs-lookup"><span data-stu-id="1ee73-106">**WCF**</span></span> | <ul><li>[<span data-ttu-id="1ee73-107">WCF - 請勿在組態檔中包含 serviceDebug 節點</span><span class="sxs-lookup"><span data-stu-id="1ee73-107">WCF- Do not include serviceDebug node in configuration file</span></span>](#servicedebug)</li><li>[<span data-ttu-id="1ee73-108">WCF - 請勿在組態檔中包含 serviceMetadata 節點</span><span class="sxs-lookup"><span data-stu-id="1ee73-108">WCF- Do not include serviceMetadata node in configuration file</span></span>](#servicemetadata)</li></ul> |
| <span data-ttu-id="1ee73-109">**Web API**</span><span class="sxs-lookup"><span data-stu-id="1ee73-109">**Web API**</span></span> | <ul><li>[<span data-ttu-id="1ee73-110">確定有在 ASP.NET Web API 中正確處理例外狀況</span><span class="sxs-lookup"><span data-stu-id="1ee73-110">Ensure that proper exception handling is done in ASP.NET Web API </span></span>](#exception)</li></ul> |
| <span data-ttu-id="1ee73-111">**Web 應用程式**</span><span class="sxs-lookup"><span data-stu-id="1ee73-111">**Web Application**</span></span> | <ul><li>[<span data-ttu-id="1ee73-112">請勿在錯誤訊息中公開安全性詳細資料</span><span class="sxs-lookup"><span data-stu-id="1ee73-112">Do not expose security details in error messages </span></span>](#messages)</li><li>[<span data-ttu-id="1ee73-113">實作預設的錯誤處理頁面</span><span class="sxs-lookup"><span data-stu-id="1ee73-113">Implement Default error handling page </span></span>](#default)</li><li>[<span data-ttu-id="1ee73-114">在 IIS 中設定的部署方法 tooRetail</span><span class="sxs-lookup"><span data-stu-id="1ee73-114">Set Deployment Method tooRetail in IIS</span></span>](#deployment)</li><li>[<span data-ttu-id="1ee73-115">例外狀況應安全地失敗</span><span class="sxs-lookup"><span data-stu-id="1ee73-115">Exceptions should fail safely</span></span>](#fail)</li></ul> |

## <span data-ttu-id="1ee73-116"><a id="servicedebug"></a>WCF - 請勿在組態檔中包含 serviceDebug 節點</span><span class="sxs-lookup"><span data-stu-id="1ee73-116"><a id="servicedebug"></a>WCF- Do not include serviceDebug node in configuration file</span></span>

| <span data-ttu-id="1ee73-117">Title</span><span class="sxs-lookup"><span data-stu-id="1ee73-117">Title</span></span>                   | <span data-ttu-id="1ee73-118">詳細資料</span><span class="sxs-lookup"><span data-stu-id="1ee73-118">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="1ee73-119">**元件**</span><span class="sxs-lookup"><span data-stu-id="1ee73-119">**Component**</span></span>               | <span data-ttu-id="1ee73-120">WCF</span><span class="sxs-lookup"><span data-stu-id="1ee73-120">WCF</span></span> | 
| <span data-ttu-id="1ee73-121">**SDL 階段**</span><span class="sxs-lookup"><span data-stu-id="1ee73-121">**SDL Phase**</span></span>               | <span data-ttu-id="1ee73-122">建置</span><span class="sxs-lookup"><span data-stu-id="1ee73-122">Build</span></span> |  
| <span data-ttu-id="1ee73-123">**適用的技術**</span><span class="sxs-lookup"><span data-stu-id="1ee73-123">**Applicable Technologies**</span></span> | <span data-ttu-id="1ee73-124">泛型、NET Framework 3</span><span class="sxs-lookup"><span data-stu-id="1ee73-124">Generic, NET Framework 3</span></span> |
| <span data-ttu-id="1ee73-125">**屬性**</span><span class="sxs-lookup"><span data-stu-id="1ee73-125">**Attributes**</span></span>              | <span data-ttu-id="1ee73-126">N/A</span><span class="sxs-lookup"><span data-stu-id="1ee73-126">N/A</span></span>  |
| <span data-ttu-id="1ee73-127">**參考**</span><span class="sxs-lookup"><span data-stu-id="1ee73-127">**References**</span></span>              | <span data-ttu-id="1ee73-128">[MSDN](https://msdn.microsoft.com/library/ff648500.aspx)、[Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html)</span><span class="sxs-lookup"><span data-stu-id="1ee73-128">[MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html)</span></span> |
| <span data-ttu-id="1ee73-129">**步驟**</span><span class="sxs-lookup"><span data-stu-id="1ee73-129">**Steps**</span></span> | <span data-ttu-id="1ee73-130">Windows Communication Framework (WCF) 服務可以設定的 tooexpose 偵錯資訊。</span><span class="sxs-lookup"><span data-stu-id="1ee73-130">Windows Communication Framework (WCF) services can be configured tooexpose debugging information.</span></span> <span data-ttu-id="1ee73-131">偵錯資訊不應用於生產環境。</span><span class="sxs-lookup"><span data-stu-id="1ee73-131">Debug information should not be used in production environments.</span></span> <span data-ttu-id="1ee73-132">hello`<serviceDebug>`標記定義 hello 偵錯資訊的功能是否已啟用 WCF 服務。</span><span class="sxs-lookup"><span data-stu-id="1ee73-132">hello `<serviceDebug>` tag defines whether hello debug information feature is enabled for a WCF service.</span></span> <span data-ttu-id="1ee73-133">如果 hello 屬性 includeExceptionDetailInFaults 設定 tootrue，例外狀況資訊從 hello 應用程式將會傳回 tooclients。</span><span class="sxs-lookup"><span data-stu-id="1ee73-133">If hello attribute includeExceptionDetailInFaults is set tootrue, exception information from hello application will be returned tooclients.</span></span> <span data-ttu-id="1ee73-134">攻擊者可以利用 hello 他們會取得從偵錯輸出 toomount 攻擊目標 hello framework、 資料庫或 hello 應用程式所使用的其他資源的其他資訊。</span><span class="sxs-lookup"><span data-stu-id="1ee73-134">Attackers can leverage hello additional information they gain from debugging output toomount attacks targeted on hello framework, database, or other resources used by hello application.</span></span> |

### <a name="example"></a><span data-ttu-id="1ee73-135">範例</span><span class="sxs-lookup"><span data-stu-id="1ee73-135">Example</span></span>
<span data-ttu-id="1ee73-136">hello 下列組態檔包含 hello`<serviceDebug>`標記：</span><span class="sxs-lookup"><span data-stu-id="1ee73-136">hello following configuration file includes hello `<serviceDebug>` tag:</span></span> 
```
<configuration> 
<system.serviceModel> 
<behaviors> 
<serviceBehaviors> 
<behavior name=""MyServiceBehavior""> 
<serviceDebug includeExceptionDetailInFaults=""True"" httpHelpPageEnabled=""True""/> 
... 
```
<span data-ttu-id="1ee73-137">停用偵錯資訊置於 hello 服務。</span><span class="sxs-lookup"><span data-stu-id="1ee73-137">Disable debugging information in hello service.</span></span> <span data-ttu-id="1ee73-138">這可藉由移除 hello`<serviceDebug>`從您的應用程式組態檔的標記。</span><span class="sxs-lookup"><span data-stu-id="1ee73-138">This can be accomplished by removing hello `<serviceDebug>` tag from your application's configuration file.</span></span> 

## <span data-ttu-id="1ee73-139"><a id="servicemetadata"></a>WCF - 請勿在組態檔中包含 serviceMetadata 節點</span><span class="sxs-lookup"><span data-stu-id="1ee73-139"><a id="servicemetadata"></a>WCF- Do not include serviceMetadata node in configuration file</span></span>

| <span data-ttu-id="1ee73-140">Title</span><span class="sxs-lookup"><span data-stu-id="1ee73-140">Title</span></span>                   | <span data-ttu-id="1ee73-141">詳細資料</span><span class="sxs-lookup"><span data-stu-id="1ee73-141">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="1ee73-142">**元件**</span><span class="sxs-lookup"><span data-stu-id="1ee73-142">**Component**</span></span>               | <span data-ttu-id="1ee73-143">WCF</span><span class="sxs-lookup"><span data-stu-id="1ee73-143">WCF</span></span> | 
| <span data-ttu-id="1ee73-144">**SDL 階段**</span><span class="sxs-lookup"><span data-stu-id="1ee73-144">**SDL Phase**</span></span>               | <span data-ttu-id="1ee73-145">建置</span><span class="sxs-lookup"><span data-stu-id="1ee73-145">Build</span></span> |  
| <span data-ttu-id="1ee73-146">**適用的技術**</span><span class="sxs-lookup"><span data-stu-id="1ee73-146">**Applicable Technologies**</span></span> | <span data-ttu-id="1ee73-147">泛型</span><span class="sxs-lookup"><span data-stu-id="1ee73-147">Generic</span></span> |
| <span data-ttu-id="1ee73-148">**屬性**</span><span class="sxs-lookup"><span data-stu-id="1ee73-148">**Attributes**</span></span>              | <span data-ttu-id="1ee73-149">泛型、NET Framework 3</span><span class="sxs-lookup"><span data-stu-id="1ee73-149">Generic, NET Framework 3</span></span> |
| <span data-ttu-id="1ee73-150">**參考**</span><span class="sxs-lookup"><span data-stu-id="1ee73-150">**References**</span></span>              | <span data-ttu-id="1ee73-151">[MSDN](https://msdn.microsoft.com/library/ff648500.aspx)、[Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html)</span><span class="sxs-lookup"><span data-stu-id="1ee73-151">[MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html)</span></span> |
| <span data-ttu-id="1ee73-152">**步驟**</span><span class="sxs-lookup"><span data-stu-id="1ee73-152">**Steps**</span></span> | <span data-ttu-id="1ee73-153">公開服務的相關資訊，可提供與重要深入了解它們如何利用 hello 服務的攻擊者。</span><span class="sxs-lookup"><span data-stu-id="1ee73-153">Publicly exposing information about a service can provide attackers with valuable insight into how they might exploit hello service.</span></span> <span data-ttu-id="1ee73-154">hello`<serviceMetadata>`標記啟用 hello 中繼資料發行功能。</span><span class="sxs-lookup"><span data-stu-id="1ee73-154">hello `<serviceMetadata>` tag enables hello metadata publishing feature.</span></span> <span data-ttu-id="1ee73-155">服務中繼資料可能包含不應開放存取的敏感性資訊。</span><span class="sxs-lookup"><span data-stu-id="1ee73-155">Service metadata could contain sensitive information that should not be publicly accessible.</span></span> <span data-ttu-id="1ee73-156">最小值，只允許 tooaccess hello 中繼資料，並確認不必要的資訊不會公開受信任的使用者。</span><span class="sxs-lookup"><span data-stu-id="1ee73-156">At a minimum, only allow trusted users tooaccess hello metadata and ensure that unnecessary information is not exposed.</span></span> <span data-ttu-id="1ee73-157">更棒的是，完全停用 hello 能力 toopublish 中繼資料。</span><span class="sxs-lookup"><span data-stu-id="1ee73-157">Better yet, entirely disable hello ability toopublish metadata.</span></span> <span data-ttu-id="1ee73-158">安全的 WCF 組態將不會包含 hello`<serviceMetadata>`標記。</span><span class="sxs-lookup"><span data-stu-id="1ee73-158">A safe WCF configuration will not contain hello `<serviceMetadata>` tag.</span></span> |

## <span data-ttu-id="1ee73-159"><a id="exception"></a>確定有在 ASP.NET Web API 中正確處理例外狀況</span><span class="sxs-lookup"><span data-stu-id="1ee73-159"><a id="exception"></a>Ensure that proper exception handling is done in ASP.NET Web API</span></span>

| <span data-ttu-id="1ee73-160">Title</span><span class="sxs-lookup"><span data-stu-id="1ee73-160">Title</span></span>                   | <span data-ttu-id="1ee73-161">詳細資料</span><span class="sxs-lookup"><span data-stu-id="1ee73-161">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="1ee73-162">**元件**</span><span class="sxs-lookup"><span data-stu-id="1ee73-162">**Component**</span></span>               | <span data-ttu-id="1ee73-163">Web API</span><span class="sxs-lookup"><span data-stu-id="1ee73-163">Web API</span></span> | 
| <span data-ttu-id="1ee73-164">**SDL 階段**</span><span class="sxs-lookup"><span data-stu-id="1ee73-164">**SDL Phase**</span></span>               | <span data-ttu-id="1ee73-165">建置</span><span class="sxs-lookup"><span data-stu-id="1ee73-165">Build</span></span> |  
| <span data-ttu-id="1ee73-166">**適用的技術**</span><span class="sxs-lookup"><span data-stu-id="1ee73-166">**Applicable Technologies**</span></span> | <span data-ttu-id="1ee73-167">MVC 5、MVC 6</span><span class="sxs-lookup"><span data-stu-id="1ee73-167">MVC 5, MVC 6</span></span> |
| <span data-ttu-id="1ee73-168">**屬性**</span><span class="sxs-lookup"><span data-stu-id="1ee73-168">**Attributes**</span></span>              | <span data-ttu-id="1ee73-169">N/A</span><span class="sxs-lookup"><span data-stu-id="1ee73-169">N/A</span></span>  |
| <span data-ttu-id="1ee73-170">**參考**</span><span class="sxs-lookup"><span data-stu-id="1ee73-170">**References**</span></span>              | <span data-ttu-id="1ee73-171">[ASP.NET Web API 中的例外狀況處理](http://www.asp.net/web-api/overview/error-handling/exception-handling)、[ASP.NET Web API 中的模型驗證](http://www.asp.net/web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api)</span><span class="sxs-lookup"><span data-stu-id="1ee73-171">[Exception Handling in ASP.NET Web API](http://www.asp.net/web-api/overview/error-handling/exception-handling), [Model Validation in ASP.NET Web API](http://www.asp.net/web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api)</span></span> |
| <span data-ttu-id="1ee73-172">**步驟**</span><span class="sxs-lookup"><span data-stu-id="1ee73-172">**Steps**</span></span> | <span data-ttu-id="1ee73-173">根據預設，ASP.NET Web API 中大多數未攔截到的例外狀況會轉譯成狀態碼為 `500, Internal Server Error` 的 HTTP 回應</span><span class="sxs-lookup"><span data-stu-id="1ee73-173">By default, most uncaught exceptions in ASP.NET Web API are translated into an HTTP response with status code `500, Internal Server Error`</span></span>|

### <a name="example"></a><span data-ttu-id="1ee73-174">範例</span><span class="sxs-lookup"><span data-stu-id="1ee73-174">Example</span></span>
<span data-ttu-id="1ee73-175">hello API，所傳回的 toocontrol hello 狀態碼`HttpResponseException`可以使用如下所示：</span><span class="sxs-lookup"><span data-stu-id="1ee73-175">toocontrol hello status code returned by hello API, `HttpResponseException` can be used as shown below:</span></span> 
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

### <a name="example"></a><span data-ttu-id="1ee73-176">範例</span><span class="sxs-lookup"><span data-stu-id="1ee73-176">Example</span></span>
<span data-ttu-id="1ee73-177">進一步控制 hello 例外狀況的回應，hello`HttpResponseMessage`可以使用類別，如下所示：</span><span class="sxs-lookup"><span data-stu-id="1ee73-177">For further control on hello exception response, hello `HttpResponseMessage` class can be used as shown below:</span></span> 
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
<span data-ttu-id="1ee73-178">toocatch 未處理的例外狀況，不是 hello 型別`HttpResponseException`，可以使用例外狀況篩選條件。</span><span class="sxs-lookup"><span data-stu-id="1ee73-178">toocatch unhandled exceptions that are not of hello type `HttpResponseException`, Exception Filters can be used.</span></span> <span data-ttu-id="1ee73-179">例外狀況篩選條件實作 hello`System.Web.Http.Filters.IExceptionFilter`介面。</span><span class="sxs-lookup"><span data-stu-id="1ee73-179">Exception filters implement hello `System.Web.Http.Filters.IExceptionFilter` interface.</span></span> <span data-ttu-id="1ee73-180">最簡單方式 toowrite hello 例外狀況篩選條件是從 hello tooderive`System.Web.Http.Filters.ExceptionFilterAttribute`類別並覆寫 hello OnException 方法。</span><span class="sxs-lookup"><span data-stu-id="1ee73-180">hello simplest way toowrite an exception filter is tooderive from hello `System.Web.Http.Filters.ExceptionFilterAttribute` class and override hello OnException method.</span></span> 

### <a name="example"></a><span data-ttu-id="1ee73-181">範例</span><span class="sxs-lookup"><span data-stu-id="1ee73-181">Example</span></span>
<span data-ttu-id="1ee73-182">以下是會將 `NotImplementedException` 例外狀況轉換成 HTTP 狀態碼 `501, Not Implemented` 的篩選：</span><span class="sxs-lookup"><span data-stu-id="1ee73-182">Here is a filter that converts `NotImplementedException` exceptions into HTTP status code `501, Not Implemented`:</span></span> 
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

<span data-ttu-id="1ee73-183">有數種方式 tooregister Web API 的例外狀況篩選條件：</span><span class="sxs-lookup"><span data-stu-id="1ee73-183">There are several ways tooregister a Web API exception filter:</span></span>
- <span data-ttu-id="1ee73-184">透過動作</span><span class="sxs-lookup"><span data-stu-id="1ee73-184">By action</span></span>
- <span data-ttu-id="1ee73-185">透過控制器</span><span class="sxs-lookup"><span data-stu-id="1ee73-185">By controller</span></span>
- <span data-ttu-id="1ee73-186">全域</span><span class="sxs-lookup"><span data-stu-id="1ee73-186">Globally</span></span>

### <a name="example"></a><span data-ttu-id="1ee73-187">範例</span><span class="sxs-lookup"><span data-stu-id="1ee73-187">Example</span></span>
<span data-ttu-id="1ee73-188">tooapply hello 篩選 tooa 特定動作，為屬性 toohello 動作加入 hello 篩選：</span><span class="sxs-lookup"><span data-stu-id="1ee73-188">tooapply hello filter tooa specific action, add hello filter as an attribute toohello action:</span></span> 
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
### <a name="example"></a><span data-ttu-id="1ee73-189">範例</span><span class="sxs-lookup"><span data-stu-id="1ee73-189">Example</span></span>
<span data-ttu-id="1ee73-190">hello 上之動作的 tooapply hello 篩選 tooall `controller`，做為屬性 toohello 加入 hello 篩選`controller`類別：</span><span class="sxs-lookup"><span data-stu-id="1ee73-190">tooapply hello filter tooall of hello actions on a `controller`, add hello filter as an attribute toohello `controller` class:</span></span> 

```C#
[NotImplExceptionFilter]
public class ProductsController : ApiController
{
    // ...
}
```

### <a name="example"></a><span data-ttu-id="1ee73-191">範例</span><span class="sxs-lookup"><span data-stu-id="1ee73-191">Example</span></span>
<span data-ttu-id="1ee73-192">tooapply hello 全域篩選 tooall Web API 控制器，將執行個體的 hello 篩選 toohello`GlobalConfiguration.Configuration.Filters`集合。</span><span class="sxs-lookup"><span data-stu-id="1ee73-192">tooapply hello filter globally tooall Web API controllers, add an instance of hello filter toohello `GlobalConfiguration.Configuration.Filters` collection.</span></span> <span data-ttu-id="1ee73-193">在此集合中的例外狀況篩選條件套用 tooany Web API 控制器動作。</span><span class="sxs-lookup"><span data-stu-id="1ee73-193">Exception filters in this collection apply tooany Web API controller action.</span></span> 
```C#
GlobalConfiguration.Configuration.Filters.Add(
    new ProductStore.NotImplExceptionFilterAttribute());
```

### <a name="example"></a><span data-ttu-id="1ee73-194">範例</span><span class="sxs-lookup"><span data-stu-id="1ee73-194">Example</span></span>
<span data-ttu-id="1ee73-195">模型驗證 hello 模型狀態可以傳遞 tooCreateErrorResponse 方法如下所示：</span><span class="sxs-lookup"><span data-stu-id="1ee73-195">For model validation, hello model state can be passed tooCreateErrorResponse method as shown below:</span></span> 
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

<span data-ttu-id="1ee73-196">如需詳細資訊，關於例外狀況處理 hello 參考一節中的 hello 連結和 ASP.Net Web API 中的模型驗證檢查</span><span class="sxs-lookup"><span data-stu-id="1ee73-196">Check hello links in hello references section for additional details about exceptional handling and model validation in ASP.Net Web API</span></span> 

## <span data-ttu-id="1ee73-197"><a id="messages"></a>請勿在錯誤訊息中公開安全性詳細資料</span><span class="sxs-lookup"><span data-stu-id="1ee73-197"><a id="messages"></a>Do not expose security details in error messages</span></span>

| <span data-ttu-id="1ee73-198">Title</span><span class="sxs-lookup"><span data-stu-id="1ee73-198">Title</span></span>                   | <span data-ttu-id="1ee73-199">詳細資料</span><span class="sxs-lookup"><span data-stu-id="1ee73-199">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="1ee73-200">**元件**</span><span class="sxs-lookup"><span data-stu-id="1ee73-200">**Component**</span></span>               | <span data-ttu-id="1ee73-201">Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="1ee73-201">Web Application</span></span> | 
| <span data-ttu-id="1ee73-202">**SDL 階段**</span><span class="sxs-lookup"><span data-stu-id="1ee73-202">**SDL Phase**</span></span>               | <span data-ttu-id="1ee73-203">建置</span><span class="sxs-lookup"><span data-stu-id="1ee73-203">Build</span></span> |  
| <span data-ttu-id="1ee73-204">**適用的技術**</span><span class="sxs-lookup"><span data-stu-id="1ee73-204">**Applicable Technologies**</span></span> | <span data-ttu-id="1ee73-205">泛型</span><span class="sxs-lookup"><span data-stu-id="1ee73-205">Generic</span></span> |
| <span data-ttu-id="1ee73-206">**屬性**</span><span class="sxs-lookup"><span data-stu-id="1ee73-206">**Attributes**</span></span>              | <span data-ttu-id="1ee73-207">N/A</span><span class="sxs-lookup"><span data-stu-id="1ee73-207">N/A</span></span>  |
| <span data-ttu-id="1ee73-208">**參考**</span><span class="sxs-lookup"><span data-stu-id="1ee73-208">**References**</span></span>              | <span data-ttu-id="1ee73-209">N/A</span><span class="sxs-lookup"><span data-stu-id="1ee73-209">N/A</span></span>  |
| <span data-ttu-id="1ee73-210">**步驟**</span><span class="sxs-lookup"><span data-stu-id="1ee73-210">**Steps**</span></span> | <p><span data-ttu-id="1ee73-211">一般錯誤訊息會提供直接 toohello 使用者但不包含機密的應用程式資料。</span><span class="sxs-lookup"><span data-stu-id="1ee73-211">Generic error messages are provided directly toohello user without including sensitive application data.</span></span> <span data-ttu-id="1ee73-212">敏感性資料的範例包括︰</span><span class="sxs-lookup"><span data-stu-id="1ee73-212">Examples of sensitive data include:</span></span></p><ul><li><span data-ttu-id="1ee73-213">伺服器名稱</span><span class="sxs-lookup"><span data-stu-id="1ee73-213">Server names</span></span></li><li><span data-ttu-id="1ee73-214">連接字串</span><span class="sxs-lookup"><span data-stu-id="1ee73-214">Connection strings</span></span></li><li><span data-ttu-id="1ee73-215">使用者名稱</span><span class="sxs-lookup"><span data-stu-id="1ee73-215">Usernames</span></span></li><li><span data-ttu-id="1ee73-216">密碼</span><span class="sxs-lookup"><span data-stu-id="1ee73-216">Passwords</span></span></li><li><span data-ttu-id="1ee73-217">SQL 程序</span><span class="sxs-lookup"><span data-stu-id="1ee73-217">SQL procedures</span></span></li><li><span data-ttu-id="1ee73-218">動態 SQL 失敗的詳細資料</span><span class="sxs-lookup"><span data-stu-id="1ee73-218">Details of dynamic SQL failures</span></span></li><li><span data-ttu-id="1ee73-219">堆疊追蹤和程式碼行</span><span class="sxs-lookup"><span data-stu-id="1ee73-219">Stack trace and lines of code</span></span></li><li><span data-ttu-id="1ee73-220">儲存在記憶體中的變數</span><span class="sxs-lookup"><span data-stu-id="1ee73-220">Variables stored in memory</span></span></li><li><span data-ttu-id="1ee73-221">磁碟機和資料夾的位置</span><span class="sxs-lookup"><span data-stu-id="1ee73-221">Drive and folder locations</span></span></li><li><span data-ttu-id="1ee73-222">應用程式的安裝點</span><span class="sxs-lookup"><span data-stu-id="1ee73-222">Application install points</span></span></li><li><span data-ttu-id="1ee73-223">主機組態設定</span><span class="sxs-lookup"><span data-stu-id="1ee73-223">Host configuration settings</span></span></li><li><span data-ttu-id="1ee73-224">其他內部應用程式詳細資料</span><span class="sxs-lookup"><span data-stu-id="1ee73-224">Other internal application details</span></span></li></ul><p><span data-ttu-id="1ee73-225">捕捉應用程式中的所有錯誤並提供泛型錯誤訊息，以及啟用 IIS 中的自訂錯誤，將有助於避免資訊外洩。</span><span class="sxs-lookup"><span data-stu-id="1ee73-225">Trapping all errors within an application and providing generic error messages, as well as enabling custom errors within IIS will help prevent information disclosure.</span></span> <span data-ttu-id="1ee73-226">SQL Server 資料庫和.NET 例外狀況處理、 在其他錯誤處理架構，會特別的詳細資訊，非常有用的 tooa 惡意使用者程式碼剖析應用程式。</span><span class="sxs-lookup"><span data-stu-id="1ee73-226">SQL Server database and .NET Exception handling, among other error handling architectures, are especially verbose and extremely useful tooa malicious user profiling your application.</span></span> <span data-ttu-id="1ee73-227">無法直接顯示 hello 的類別內容衍生自 hello.NET 例外狀況類別，並確定您有適當的例外狀況處理，好讓不小心未預期的例外狀況直接引發 toohello 使用者執行。</span><span class="sxs-lookup"><span data-stu-id="1ee73-227">Do not directly display hello contents of a class derived from hello .NET Exception class, and ensure that you have proper exception handling so that an unexpected exception isn't inadvertently raised directly toohello user.</span></span></p><ul><li><span data-ttu-id="1ee73-228">提供一般錯誤訊息直接 toohello 取出離開直接在 hello 例外狀況/錯誤訊息中找到的特定詳細資料的使用者</span><span class="sxs-lookup"><span data-stu-id="1ee73-228">Provide generic error messages directly toohello user that abstract away specific details found directly in hello exception/error message</span></span></li><li><span data-ttu-id="1ee73-229">不顯示 hello 內容.NET 例外狀況類別直接 toohello 使用者嗎</span><span class="sxs-lookup"><span data-stu-id="1ee73-229">Do not display hello contents of a .NET exception class directly toohello user</span></span></li><li><span data-ttu-id="1ee73-230">設陷所有錯誤訊息，並視通知 hello 使用者透過一般錯誤訊息傳送的 toohello 應用程式用戶端</span><span class="sxs-lookup"><span data-stu-id="1ee73-230">Trap all error messages and if appropriate inform hello user via a generic error message sent toohello application client</span></span></li><li><span data-ttu-id="1ee73-231">不會公開 hello 內容 hello 例外狀況類別直接 toohello 使用者特別 hello 傳回的值從`.ToString()`，或 hello hello 訊息或 StackTrace 屬性值。</span><span class="sxs-lookup"><span data-stu-id="1ee73-231">Do not expose hello contents of hello Exception class directly toohello user, especially hello return value from `.ToString()`, or hello values of hello Message or StackTrace properties.</span></span> <span data-ttu-id="1ee73-232">安全地記錄此資訊並顯示更無害的訊息 toohello 使用者</span><span class="sxs-lookup"><span data-stu-id="1ee73-232">Securely log this information and display a more innocuous message toohello user</span></span></li></ul>|

## <span data-ttu-id="1ee73-233"><a id="default"></a>實作預設的錯誤處理頁面</span><span class="sxs-lookup"><span data-stu-id="1ee73-233"><a id="default"></a>Implement Default error handling page</span></span>

| <span data-ttu-id="1ee73-234">Title</span><span class="sxs-lookup"><span data-stu-id="1ee73-234">Title</span></span>                   | <span data-ttu-id="1ee73-235">詳細資料</span><span class="sxs-lookup"><span data-stu-id="1ee73-235">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="1ee73-236">**元件**</span><span class="sxs-lookup"><span data-stu-id="1ee73-236">**Component**</span></span>               | <span data-ttu-id="1ee73-237">Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="1ee73-237">Web Application</span></span> | 
| <span data-ttu-id="1ee73-238">**SDL 階段**</span><span class="sxs-lookup"><span data-stu-id="1ee73-238">**SDL Phase**</span></span>               | <span data-ttu-id="1ee73-239">建置</span><span class="sxs-lookup"><span data-stu-id="1ee73-239">Build</span></span> |  
| <span data-ttu-id="1ee73-240">**適用的技術**</span><span class="sxs-lookup"><span data-stu-id="1ee73-240">**Applicable Technologies**</span></span> | <span data-ttu-id="1ee73-241">泛型</span><span class="sxs-lookup"><span data-stu-id="1ee73-241">Generic</span></span> |
| <span data-ttu-id="1ee73-242">**屬性**</span><span class="sxs-lookup"><span data-stu-id="1ee73-242">**Attributes**</span></span>              | <span data-ttu-id="1ee73-243">N/A</span><span class="sxs-lookup"><span data-stu-id="1ee73-243">N/A</span></span>  |
| <span data-ttu-id="1ee73-244">**參考**</span><span class="sxs-lookup"><span data-stu-id="1ee73-244">**References**</span></span>              | <span data-ttu-id="1ee73-245">[編輯 ASP.NET 錯誤頁面設定對話方塊](https://technet.microsoft.com/library/dd569096(WS.10).aspx)</span><span class="sxs-lookup"><span data-stu-id="1ee73-245">[Edit ASP.NET Error Pages Settings Dialog Box](https://technet.microsoft.com/library/dd569096(WS.10).aspx)</span></span> |
| <span data-ttu-id="1ee73-246">**步驟**</span><span class="sxs-lookup"><span data-stu-id="1ee73-246">**Steps**</span></span> | <p><span data-ttu-id="1ee73-247">當 ASP.NET 應用程式失敗並造成 HTTP/1.x 500 內部伺服器錯誤時，或當功能組態 (例如要求篩選) 避免顯示頁面時，就會產生錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="1ee73-247">When an ASP.NET application fails and causes an HTTP/1.x 500 Internal Server Error, or a feature configuration (such as Request Filtering) prevents a page from being displayed, an error message will be generated.</span></span> <span data-ttu-id="1ee73-248">系統管理員可以選擇 hello 應用程式應該會顯示易記訊息 toohello 用戶端、 詳細的錯誤訊息 toohello 用戶端或詳細的錯誤訊息 toolocalhost 只。</span><span class="sxs-lookup"><span data-stu-id="1ee73-248">Administrators can choose whether or not hello application should display a friendly message toohello client, detailed error message toohello client, or detailed error message toolocalhost only.</span></span> <span data-ttu-id="1ee73-249">hello <customErrors> hello web.config 中的標記具有三種模式：</span><span class="sxs-lookup"><span data-stu-id="1ee73-249">hello <customErrors> tag in hello web.config has three modes:</span></span></p><ul><li><span data-ttu-id="1ee73-250">**開啟︰**指定要啟用自訂錯誤。</span><span class="sxs-lookup"><span data-stu-id="1ee73-250">**On:** Specifies that custom errors are enabled.</span></span> <span data-ttu-id="1ee73-251">如果未指定任何 defaultRedirect 屬性，則使用者會看到泛型錯誤。</span><span class="sxs-lookup"><span data-stu-id="1ee73-251">If no defaultRedirect attribute is specified, users see a generic error.</span></span> <span data-ttu-id="1ee73-252">hello 自訂錯誤會顯示 toohello 遠端用戶端和 toohello 本機主機</span><span class="sxs-lookup"><span data-stu-id="1ee73-252">hello custom errors are shown toohello remote clients and toohello local host</span></span></li><li><span data-ttu-id="1ee73-253">**關閉︰**指定要停用自訂錯誤。</span><span class="sxs-lookup"><span data-stu-id="1ee73-253">**Off:** Specifies that custom errors are disabled.</span></span> <span data-ttu-id="1ee73-254">hello 詳細的 ASP.NET 錯誤會顯示 toohello 遠端用戶端和 toohello 本機主機</span><span class="sxs-lookup"><span data-stu-id="1ee73-254">hello detailed ASP.NET errors are shown toohello remote clients and toohello local host</span></span></li><li><span data-ttu-id="1ee73-255">**RemoteOnly:**指定自訂的錯誤會顯示只有 toohello 遠端用戶端，以及 ASP.NET 錯誤會顯示 toohello 本機主機。</span><span class="sxs-lookup"><span data-stu-id="1ee73-255">**RemoteOnly:** Specifies that custom errors are shown only toohello remote clients, and that ASP.NET errors are shown toohello local host.</span></span> <span data-ttu-id="1ee73-256">這是 hello 預設值</span><span class="sxs-lookup"><span data-stu-id="1ee73-256">This is hello default value</span></span></li></ul><p><span data-ttu-id="1ee73-257">開啟 hello `web.config` hello 應用程式/網站的檔案，並確定 hello 標記有 `<customErrors mode="RemoteOnly" />`或`<customErrors mode="On" />`定義。</span><span class="sxs-lookup"><span data-stu-id="1ee73-257">Open hello `web.config` file for hello application/site and ensure that hello tag has either `<customErrors mode="RemoteOnly" />` or `<customErrors mode="On" />` defined.</span></span></p>|

## <span data-ttu-id="1ee73-258"><a id="deployment"></a>在 IIS 中設定的部署方法 tooRetail</span><span class="sxs-lookup"><span data-stu-id="1ee73-258"><a id="deployment"></a>Set Deployment Method tooRetail in IIS</span></span>

| <span data-ttu-id="1ee73-259">Title</span><span class="sxs-lookup"><span data-stu-id="1ee73-259">Title</span></span>                   | <span data-ttu-id="1ee73-260">詳細資料</span><span class="sxs-lookup"><span data-stu-id="1ee73-260">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="1ee73-261">**元件**</span><span class="sxs-lookup"><span data-stu-id="1ee73-261">**Component**</span></span>               | <span data-ttu-id="1ee73-262">Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="1ee73-262">Web Application</span></span> | 
| <span data-ttu-id="1ee73-263">**SDL 階段**</span><span class="sxs-lookup"><span data-stu-id="1ee73-263">**SDL Phase**</span></span>               | <span data-ttu-id="1ee73-264">部署</span><span class="sxs-lookup"><span data-stu-id="1ee73-264">Deployment</span></span> |  
| <span data-ttu-id="1ee73-265">**適用的技術**</span><span class="sxs-lookup"><span data-stu-id="1ee73-265">**Applicable Technologies**</span></span> | <span data-ttu-id="1ee73-266">泛型</span><span class="sxs-lookup"><span data-stu-id="1ee73-266">Generic</span></span> |
| <span data-ttu-id="1ee73-267">**屬性**</span><span class="sxs-lookup"><span data-stu-id="1ee73-267">**Attributes**</span></span>              | <span data-ttu-id="1ee73-268">N/A</span><span class="sxs-lookup"><span data-stu-id="1ee73-268">N/A</span></span>  |
| <span data-ttu-id="1ee73-269">**參考**</span><span class="sxs-lookup"><span data-stu-id="1ee73-269">**References**</span></span>              | <span data-ttu-id="1ee73-270">[部署元素 (ASP.NET 設定結構描述)](https://msdn.microsoft.com/library/ms228298(VS.80).aspx)</span><span class="sxs-lookup"><span data-stu-id="1ee73-270">[deployment Element (ASP.NET Settings Schema)](https://msdn.microsoft.com/library/ms228298(VS.80).aspx)</span></span> |
| <span data-ttu-id="1ee73-271">**步驟**</span><span class="sxs-lookup"><span data-stu-id="1ee73-271">**Steps**</span></span> | <p><span data-ttu-id="1ee73-272">hello`<deployment retail>`交換器適用於實際執行的 IIS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="1ee73-272">hello `<deployment retail>` switch is intended for use by production IIS servers.</span></span> <span data-ttu-id="1ee73-273">這個參數是使用的 toohelp 應用程式執行與 hello 最佳效能，並停用 leakages hello 在頁面上，停用 hello 能力 toodisplay 應用程式的能力 toogenerate 追蹤輸出的最少安全性資訊詳細錯誤訊息 tooend 使用者，並停用 hello 偵錯參數。</span><span class="sxs-lookup"><span data-stu-id="1ee73-273">This switch is used toohelp applications run with hello best possible performance and least possible security information leakages by disabling hello application's ability toogenerate trace output on a page, disabling hello ability toodisplay detailed error messages tooend users, and disabling hello debug switch.</span></span></p><p><span data-ttu-id="1ee73-274">在開發期間，經常會啟用專供開發人員使用的參數和選項，例如失敗要求追蹤和偵錯。</span><span class="sxs-lookup"><span data-stu-id="1ee73-274">Often times, switches and options that are developer-focused, such as failed request tracing and debugging, are enabled during active development.</span></span> <span data-ttu-id="1ee73-275">建議您在任何實際執行伺服器上的 hello 部署方法，設定 tooretail。</span><span class="sxs-lookup"><span data-stu-id="1ee73-275">It is recommended that hello deployment method on any production server be set tooretail.</span></span> <span data-ttu-id="1ee73-276">開啟 hello machine.config 檔案，並確定`<deployment retail="true" />`會設定 tootrue。</span><span class="sxs-lookup"><span data-stu-id="1ee73-276">open hello machine.config file and ensure that `<deployment retail="true" />` remains set tootrue.</span></span></p>|

## <span data-ttu-id="1ee73-277"><a id="fail"></a>例外狀況應安全地失敗</span><span class="sxs-lookup"><span data-stu-id="1ee73-277"><a id="fail"></a>Exceptions should fail safely</span></span>

| <span data-ttu-id="1ee73-278">Title</span><span class="sxs-lookup"><span data-stu-id="1ee73-278">Title</span></span>                   | <span data-ttu-id="1ee73-279">詳細資料</span><span class="sxs-lookup"><span data-stu-id="1ee73-279">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="1ee73-280">**元件**</span><span class="sxs-lookup"><span data-stu-id="1ee73-280">**Component**</span></span>               | <span data-ttu-id="1ee73-281">Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="1ee73-281">Web Application</span></span> | 
| <span data-ttu-id="1ee73-282">**SDL 階段**</span><span class="sxs-lookup"><span data-stu-id="1ee73-282">**SDL Phase**</span></span>               | <span data-ttu-id="1ee73-283">建置</span><span class="sxs-lookup"><span data-stu-id="1ee73-283">Build</span></span> |  
| <span data-ttu-id="1ee73-284">**適用的技術**</span><span class="sxs-lookup"><span data-stu-id="1ee73-284">**Applicable Technologies**</span></span> | <span data-ttu-id="1ee73-285">泛型</span><span class="sxs-lookup"><span data-stu-id="1ee73-285">Generic</span></span> |
| <span data-ttu-id="1ee73-286">**屬性**</span><span class="sxs-lookup"><span data-stu-id="1ee73-286">**Attributes**</span></span>              | <span data-ttu-id="1ee73-287">N/A</span><span class="sxs-lookup"><span data-stu-id="1ee73-287">N/A</span></span>  |
| <span data-ttu-id="1ee73-288">**參考**</span><span class="sxs-lookup"><span data-stu-id="1ee73-288">**References**</span></span>              | [<span data-ttu-id="1ee73-289">安全地失敗</span><span class="sxs-lookup"><span data-stu-id="1ee73-289">Fail securely</span></span>](https://www.owasp.org/index.php/Fail_securely) |
| <span data-ttu-id="1ee73-290">**步驟**</span><span class="sxs-lookup"><span data-stu-id="1ee73-290">**Steps**</span></span> | <span data-ttu-id="1ee73-291">應用程式應安全地失敗。</span><span class="sxs-lookup"><span data-stu-id="1ee73-291">Application should fail safely.</span></span> <span data-ttu-id="1ee73-292">任何會傳回布林值的方法 (根據所做出的特定決策) 皆應小心地建立例外狀況區塊。</span><span class="sxs-lookup"><span data-stu-id="1ee73-292">Any method that returns a Boolean value, based on which certain decision is made, should have exception block carefully created.</span></span> <span data-ttu-id="1ee73-293">有許多到期，請在 hello 例外狀況區塊會寫入時後果 toowhich 安全性問題蔓延的邏輯錯誤。</span><span class="sxs-lookup"><span data-stu-id="1ee73-293">There are lot of logical errors due toowhich security issues creep in, when hello exception block is written carelessly.</span></span>|

### <a name="example"></a><span data-ttu-id="1ee73-294">範例</span><span class="sxs-lookup"><span data-stu-id="1ee73-294">Example</span></span>
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
<span data-ttu-id="1ee73-295">方法的上方 hello 一定會傳回 True，如果某些例外狀況。</span><span class="sxs-lookup"><span data-stu-id="1ee73-295">hello above method will always return True, if some exception happens.</span></span> <span data-ttu-id="1ee73-296">如果 hello 終端使用者提供的格式不正確的 URL，hello 瀏覽器方面，但 hello`Uri()`建構函式不會這將會擲回例外狀況，以及應採取 hello 犧牲者 toohello 有效但格式不正確的 URL。</span><span class="sxs-lookup"><span data-stu-id="1ee73-296">If hello end user provides a malformed URL, that hello browser respects, but hello `Uri()` constructor doesn't, this will throw an exception, and hello victim will be taken toohello valid but malformed URL.</span></span> 
