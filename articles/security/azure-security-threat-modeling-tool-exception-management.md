---
title: "例外狀況管理 - Microsoft 威脅模型化工具 - Azure | Microsoft Docs"
description: "降低威脅模型化工具所暴露的威脅"
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
ms.openlocfilehash: bbf357b902474a1812eb7a5a2c914d0c8b91934b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="security-frame-exception-management--mitigations"></a><span data-ttu-id="d78f1-103">安全性架構︰例外狀況管理 | 風險降低</span><span class="sxs-lookup"><span data-stu-id="d78f1-103">Security Frame: Exception Management | Mitigations</span></span> 
| <span data-ttu-id="d78f1-104">產品/服務</span><span class="sxs-lookup"><span data-stu-id="d78f1-104">Product/Service</span></span> | <span data-ttu-id="d78f1-105">文章</span><span class="sxs-lookup"><span data-stu-id="d78f1-105">Article</span></span> |
| --------------- | ------- |
| <span data-ttu-id="d78f1-106">**WCF**</span><span class="sxs-lookup"><span data-stu-id="d78f1-106">**WCF**</span></span> | <ul><li>[<span data-ttu-id="d78f1-107">WCF - 請勿在組態檔中包含 serviceDebug 節點</span><span class="sxs-lookup"><span data-stu-id="d78f1-107">WCF- Do not include serviceDebug node in configuration file</span></span>](#servicedebug)</li><li>[<span data-ttu-id="d78f1-108">WCF - 請勿在組態檔中包含 serviceMetadata 節點</span><span class="sxs-lookup"><span data-stu-id="d78f1-108">WCF- Do not include serviceMetadata node in configuration file</span></span>](#servicemetadata)</li></ul> |
| <span data-ttu-id="d78f1-109">**Web API**</span><span class="sxs-lookup"><span data-stu-id="d78f1-109">**Web API**</span></span> | <ul><li>[<span data-ttu-id="d78f1-110">確定有在 ASP.NET Web API 中正確處理例外狀況</span><span class="sxs-lookup"><span data-stu-id="d78f1-110">Ensure that proper exception handling is done in ASP.NET Web API </span></span>](#exception)</li></ul> |
| <span data-ttu-id="d78f1-111">**Web 應用程式**</span><span class="sxs-lookup"><span data-stu-id="d78f1-111">**Web Application**</span></span> | <ul><li>[<span data-ttu-id="d78f1-112">請勿在錯誤訊息中公開安全性詳細資料</span><span class="sxs-lookup"><span data-stu-id="d78f1-112">Do not expose security details in error messages </span></span>](#messages)</li><li>[<span data-ttu-id="d78f1-113">實作預設的錯誤處理頁面</span><span class="sxs-lookup"><span data-stu-id="d78f1-113">Implement Default error handling page </span></span>](#default)</li><li>[<span data-ttu-id="d78f1-114">設定要在 IIS 中零售的部署方法</span><span class="sxs-lookup"><span data-stu-id="d78f1-114">Set Deployment Method to Retail in IIS</span></span>](#deployment)</li><li>[<span data-ttu-id="d78f1-115">例外狀況應安全地失敗</span><span class="sxs-lookup"><span data-stu-id="d78f1-115">Exceptions should fail safely</span></span>](#fail)</li></ul> |

## <span data-ttu-id="d78f1-116"><a id="servicedebug"></a>WCF - 請勿在組態檔中包含 serviceDebug 節點</span><span class="sxs-lookup"><span data-stu-id="d78f1-116"><a id="servicedebug"></a>WCF- Do not include serviceDebug node in configuration file</span></span>

| <span data-ttu-id="d78f1-117">Title</span><span class="sxs-lookup"><span data-stu-id="d78f1-117">Title</span></span>                   | <span data-ttu-id="d78f1-118">詳細資料</span><span class="sxs-lookup"><span data-stu-id="d78f1-118">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="d78f1-119">**元件**</span><span class="sxs-lookup"><span data-stu-id="d78f1-119">**Component**</span></span>               | <span data-ttu-id="d78f1-120">WCF</span><span class="sxs-lookup"><span data-stu-id="d78f1-120">WCF</span></span> | 
| <span data-ttu-id="d78f1-121">**SDL 階段**</span><span class="sxs-lookup"><span data-stu-id="d78f1-121">**SDL Phase**</span></span>               | <span data-ttu-id="d78f1-122">建置</span><span class="sxs-lookup"><span data-stu-id="d78f1-122">Build</span></span> |  
| <span data-ttu-id="d78f1-123">**適用的技術**</span><span class="sxs-lookup"><span data-stu-id="d78f1-123">**Applicable Technologies**</span></span> | <span data-ttu-id="d78f1-124">泛型、NET Framework 3</span><span class="sxs-lookup"><span data-stu-id="d78f1-124">Generic, NET Framework 3</span></span> |
| <span data-ttu-id="d78f1-125">**屬性**</span><span class="sxs-lookup"><span data-stu-id="d78f1-125">**Attributes**</span></span>              | <span data-ttu-id="d78f1-126">N/A</span><span class="sxs-lookup"><span data-stu-id="d78f1-126">N/A</span></span>  |
| <span data-ttu-id="d78f1-127">**參考**</span><span class="sxs-lookup"><span data-stu-id="d78f1-127">**References**</span></span>              | <span data-ttu-id="d78f1-128">[MSDN](https://msdn.microsoft.com/library/ff648500.aspx)、[Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html)</span><span class="sxs-lookup"><span data-stu-id="d78f1-128">[MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html)</span></span> |
| <span data-ttu-id="d78f1-129">**步驟**</span><span class="sxs-lookup"><span data-stu-id="d78f1-129">**Steps**</span></span> | <span data-ttu-id="d78f1-130">Windows Communication Framework (WCF) 服務可以設定為公開偵錯資訊。</span><span class="sxs-lookup"><span data-stu-id="d78f1-130">Windows Communication Framework (WCF) services can be configured to expose debugging information.</span></span> <span data-ttu-id="d78f1-131">偵錯資訊不應用於生產環境。</span><span class="sxs-lookup"><span data-stu-id="d78f1-131">Debug information should not be used in production environments.</span></span> <span data-ttu-id="d78f1-132">`<serviceDebug>` 標籤可定義是否啟用 WCF 服務的偵錯資訊功能。</span><span class="sxs-lookup"><span data-stu-id="d78f1-132">The `<serviceDebug>` tag defines whether the debug information feature is enabled for a WCF service.</span></span> <span data-ttu-id="d78f1-133">如果屬性 includeExceptionDetailInFaults 設為 true，來自應用程式的例外狀況資訊會傳回給用戶端。</span><span class="sxs-lookup"><span data-stu-id="d78f1-133">If the attribute includeExceptionDetailInFaults is set to true, exception information from the application will be returned to clients.</span></span> <span data-ttu-id="d78f1-134">攻擊者可以利用他們從偵錯輸出取得的其他資訊，裝載以架構、資料庫或應用程式所用其他資源做為目標的攻擊。</span><span class="sxs-lookup"><span data-stu-id="d78f1-134">Attackers can leverage the additional information they gain from debugging output to mount attacks targeted on the framework, database, or other resources used by the application.</span></span> |

### <a name="example"></a><span data-ttu-id="d78f1-135">範例</span><span class="sxs-lookup"><span data-stu-id="d78f1-135">Example</span></span>
<span data-ttu-id="d78f1-136">下列組態檔包含 `<serviceDebug>` 標籤︰</span><span class="sxs-lookup"><span data-stu-id="d78f1-136">The following configuration file includes the `<serviceDebug>` tag:</span></span> 
```
<configuration> 
<system.serviceModel> 
<behaviors> 
<serviceBehaviors> 
<behavior name=""MyServiceBehavior""> 
<serviceDebug includeExceptionDetailInFaults=""True"" httpHelpPageEnabled=""True""/> 
... 
```
<span data-ttu-id="d78f1-137">停用服務中的偵錯資訊。</span><span class="sxs-lookup"><span data-stu-id="d78f1-137">Disable debugging information in the service.</span></span> <span data-ttu-id="d78f1-138">這可藉由從應用程式組態檔移除 `<serviceDebug>` 標籤來完成。</span><span class="sxs-lookup"><span data-stu-id="d78f1-138">This can be accomplished by removing the `<serviceDebug>` tag from your application's configuration file.</span></span> 

## <span data-ttu-id="d78f1-139"><a id="servicemetadata"></a>WCF - 請勿在組態檔中包含 serviceMetadata 節點</span><span class="sxs-lookup"><span data-stu-id="d78f1-139"><a id="servicemetadata"></a>WCF- Do not include serviceMetadata node in configuration file</span></span>

| <span data-ttu-id="d78f1-140">Title</span><span class="sxs-lookup"><span data-stu-id="d78f1-140">Title</span></span>                   | <span data-ttu-id="d78f1-141">詳細資料</span><span class="sxs-lookup"><span data-stu-id="d78f1-141">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="d78f1-142">**元件**</span><span class="sxs-lookup"><span data-stu-id="d78f1-142">**Component**</span></span>               | <span data-ttu-id="d78f1-143">WCF</span><span class="sxs-lookup"><span data-stu-id="d78f1-143">WCF</span></span> | 
| <span data-ttu-id="d78f1-144">**SDL 階段**</span><span class="sxs-lookup"><span data-stu-id="d78f1-144">**SDL Phase**</span></span>               | <span data-ttu-id="d78f1-145">建置</span><span class="sxs-lookup"><span data-stu-id="d78f1-145">Build</span></span> |  
| <span data-ttu-id="d78f1-146">**適用的技術**</span><span class="sxs-lookup"><span data-stu-id="d78f1-146">**Applicable Technologies**</span></span> | <span data-ttu-id="d78f1-147">泛型</span><span class="sxs-lookup"><span data-stu-id="d78f1-147">Generic</span></span> |
| <span data-ttu-id="d78f1-148">**屬性**</span><span class="sxs-lookup"><span data-stu-id="d78f1-148">**Attributes**</span></span>              | <span data-ttu-id="d78f1-149">泛型、NET Framework 3</span><span class="sxs-lookup"><span data-stu-id="d78f1-149">Generic, NET Framework 3</span></span> |
| <span data-ttu-id="d78f1-150">**參考**</span><span class="sxs-lookup"><span data-stu-id="d78f1-150">**References**</span></span>              | <span data-ttu-id="d78f1-151">[MSDN](https://msdn.microsoft.com/library/ff648500.aspx)、[Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html)</span><span class="sxs-lookup"><span data-stu-id="d78f1-151">[MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html)</span></span> |
| <span data-ttu-id="d78f1-152">**步驟**</span><span class="sxs-lookup"><span data-stu-id="d78f1-152">**Steps**</span></span> | <span data-ttu-id="d78f1-153">對外公開的服務相關資訊可提供重要見解給攻擊者，讓其了解如何利用服務。</span><span class="sxs-lookup"><span data-stu-id="d78f1-153">Publicly exposing information about a service can provide attackers with valuable insight into how they might exploit the service.</span></span> <span data-ttu-id="d78f1-154">`<serviceMetadata>` 標籤會啟用中繼資料發佈功能。</span><span class="sxs-lookup"><span data-stu-id="d78f1-154">The `<serviceMetadata>` tag enables the metadata publishing feature.</span></span> <span data-ttu-id="d78f1-155">服務中繼資料可能包含不應開放存取的敏感性資訊。</span><span class="sxs-lookup"><span data-stu-id="d78f1-155">Service metadata could contain sensitive information that should not be publicly accessible.</span></span> <span data-ttu-id="d78f1-156">至少，請只允許受信任使用者存取中繼資料，並確定不會公開不必要的資訊。</span><span class="sxs-lookup"><span data-stu-id="d78f1-156">At a minimum, only allow trusted users to access the metadata and ensure that unnecessary information is not exposed.</span></span> <span data-ttu-id="d78f1-157">最好是完全停用發佈中繼資料的功能。</span><span class="sxs-lookup"><span data-stu-id="d78f1-157">Better yet, entirely disable the ability to publish metadata.</span></span> <span data-ttu-id="d78f1-158">安全的 WCF 組態不會包含 `<serviceMetadata>` 標籤。</span><span class="sxs-lookup"><span data-stu-id="d78f1-158">A safe WCF configuration will not contain the `<serviceMetadata>` tag.</span></span> |

## <span data-ttu-id="d78f1-159"><a id="exception"></a>確定有在 ASP.NET Web API 中正確處理例外狀況</span><span class="sxs-lookup"><span data-stu-id="d78f1-159"><a id="exception"></a>Ensure that proper exception handling is done in ASP.NET Web API</span></span>

| <span data-ttu-id="d78f1-160">Title</span><span class="sxs-lookup"><span data-stu-id="d78f1-160">Title</span></span>                   | <span data-ttu-id="d78f1-161">詳細資料</span><span class="sxs-lookup"><span data-stu-id="d78f1-161">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="d78f1-162">**元件**</span><span class="sxs-lookup"><span data-stu-id="d78f1-162">**Component**</span></span>               | <span data-ttu-id="d78f1-163">Web API</span><span class="sxs-lookup"><span data-stu-id="d78f1-163">Web API</span></span> | 
| <span data-ttu-id="d78f1-164">**SDL 階段**</span><span class="sxs-lookup"><span data-stu-id="d78f1-164">**SDL Phase**</span></span>               | <span data-ttu-id="d78f1-165">建置</span><span class="sxs-lookup"><span data-stu-id="d78f1-165">Build</span></span> |  
| <span data-ttu-id="d78f1-166">**適用的技術**</span><span class="sxs-lookup"><span data-stu-id="d78f1-166">**Applicable Technologies**</span></span> | <span data-ttu-id="d78f1-167">MVC 5、MVC 6</span><span class="sxs-lookup"><span data-stu-id="d78f1-167">MVC 5, MVC 6</span></span> |
| <span data-ttu-id="d78f1-168">**屬性**</span><span class="sxs-lookup"><span data-stu-id="d78f1-168">**Attributes**</span></span>              | <span data-ttu-id="d78f1-169">N/A</span><span class="sxs-lookup"><span data-stu-id="d78f1-169">N/A</span></span>  |
| <span data-ttu-id="d78f1-170">**參考**</span><span class="sxs-lookup"><span data-stu-id="d78f1-170">**References**</span></span>              | <span data-ttu-id="d78f1-171">[ASP.NET Web API 中的例外狀況處理](http://www.asp.net/web-api/overview/error-handling/exception-handling)、[ASP.NET Web API 中的模型驗證](http://www.asp.net/web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api)</span><span class="sxs-lookup"><span data-stu-id="d78f1-171">[Exception Handling in ASP.NET Web API](http://www.asp.net/web-api/overview/error-handling/exception-handling), [Model Validation in ASP.NET Web API](http://www.asp.net/web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api)</span></span> |
| <span data-ttu-id="d78f1-172">**步驟**</span><span class="sxs-lookup"><span data-stu-id="d78f1-172">**Steps**</span></span> | <span data-ttu-id="d78f1-173">根據預設，ASP.NET Web API 中大多數未攔截到的例外狀況會轉譯成狀態碼為 `500, Internal Server Error` 的 HTTP 回應</span><span class="sxs-lookup"><span data-stu-id="d78f1-173">By default, most uncaught exceptions in ASP.NET Web API are translated into an HTTP response with status code `500, Internal Server Error`</span></span>|

### <a name="example"></a><span data-ttu-id="d78f1-174">範例</span><span class="sxs-lookup"><span data-stu-id="d78f1-174">Example</span></span>
<span data-ttu-id="d78f1-175">若要控制 API 傳回的狀態碼，可如下所示使用 `HttpResponseException`︰</span><span class="sxs-lookup"><span data-stu-id="d78f1-175">To control the status code returned by the API, `HttpResponseException` can be used as shown below:</span></span> 
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

### <a name="example"></a><span data-ttu-id="d78f1-176">範例</span><span class="sxs-lookup"><span data-stu-id="d78f1-176">Example</span></span>
<span data-ttu-id="d78f1-177">若要進一步控制例外狀況回應，可如下所示使用 `HttpResponseMessage` 類別︰</span><span class="sxs-lookup"><span data-stu-id="d78f1-177">For further control on the exception response, the `HttpResponseMessage` class can be used as shown below:</span></span> 
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
<span data-ttu-id="d78f1-178">若要攔截類型不是 `HttpResponseException` 的未處理例外狀況，可使用例外狀況篩選。</span><span class="sxs-lookup"><span data-stu-id="d78f1-178">To catch unhandled exceptions that are not of the type `HttpResponseException`, Exception Filters can be used.</span></span> <span data-ttu-id="d78f1-179">例外狀況篩選會實作 `System.Web.Http.Filters.IExceptionFilter` 介面。</span><span class="sxs-lookup"><span data-stu-id="d78f1-179">Exception filters implement the `System.Web.Http.Filters.IExceptionFilter` interface.</span></span> <span data-ttu-id="d78f1-180">撰寫例外狀況篩選的最簡單方式是從 `System.Web.Http.Filters.ExceptionFilterAttribute` 類別衍生並覆寫 OnException 方法。</span><span class="sxs-lookup"><span data-stu-id="d78f1-180">The simplest way to write an exception filter is to derive from the `System.Web.Http.Filters.ExceptionFilterAttribute` class and override the OnException method.</span></span> 

### <a name="example"></a><span data-ttu-id="d78f1-181">範例</span><span class="sxs-lookup"><span data-stu-id="d78f1-181">Example</span></span>
<span data-ttu-id="d78f1-182">以下是會將 `NotImplementedException` 例外狀況轉換成 HTTP 狀態碼 `501, Not Implemented` 的篩選：</span><span class="sxs-lookup"><span data-stu-id="d78f1-182">Here is a filter that converts `NotImplementedException` exceptions into HTTP status code `501, Not Implemented`:</span></span> 
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

<span data-ttu-id="d78f1-183">有數種方式可以註冊 Web API 例外狀況篩選︰</span><span class="sxs-lookup"><span data-stu-id="d78f1-183">There are several ways to register a Web API exception filter:</span></span>
- <span data-ttu-id="d78f1-184">透過動作</span><span class="sxs-lookup"><span data-stu-id="d78f1-184">By action</span></span>
- <span data-ttu-id="d78f1-185">透過控制器</span><span class="sxs-lookup"><span data-stu-id="d78f1-185">By controller</span></span>
- <span data-ttu-id="d78f1-186">全域</span><span class="sxs-lookup"><span data-stu-id="d78f1-186">Globally</span></span>

### <a name="example"></a><span data-ttu-id="d78f1-187">範例</span><span class="sxs-lookup"><span data-stu-id="d78f1-187">Example</span></span>
<span data-ttu-id="d78f1-188">若要將篩選套用至特定動作，請在動作中新增篩選來做為屬性︰</span><span class="sxs-lookup"><span data-stu-id="d78f1-188">To apply the filter to a specific action, add the filter as an attribute to the action:</span></span> 
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
### <a name="example"></a><span data-ttu-id="d78f1-189">範例</span><span class="sxs-lookup"><span data-stu-id="d78f1-189">Example</span></span>
<span data-ttu-id="d78f1-190">若要將篩選套用至 `controller` 上的所有動作，請在 `controller` 類別中新增篩選來做為屬性︰</span><span class="sxs-lookup"><span data-stu-id="d78f1-190">To apply the filter to all of the actions on a `controller`, add the filter as an attribute to the `controller` class:</span></span> 

```C#
[NotImplExceptionFilter]
public class ProductsController : ApiController
{
    // ...
}
```

### <a name="example"></a><span data-ttu-id="d78f1-191">範例</span><span class="sxs-lookup"><span data-stu-id="d78f1-191">Example</span></span>
<span data-ttu-id="d78f1-192">若要將篩選全域套用至所有 Web API 控制器，請在 `GlobalConfiguration.Configuration.Filters` 集合中新增篩選執行個體。</span><span class="sxs-lookup"><span data-stu-id="d78f1-192">To apply the filter globally to all Web API controllers, add an instance of the filter to the `GlobalConfiguration.Configuration.Filters` collection.</span></span> <span data-ttu-id="d78f1-193">此集合中的例外狀況篩選會套用至任何 Web API 控制器動作。</span><span class="sxs-lookup"><span data-stu-id="d78f1-193">Exception filters in this collection apply to any Web API controller action.</span></span> 
```C#
GlobalConfiguration.Configuration.Filters.Add(
    new ProductStore.NotImplExceptionFilterAttribute());
```

### <a name="example"></a><span data-ttu-id="d78f1-194">範例</span><span class="sxs-lookup"><span data-stu-id="d78f1-194">Example</span></span>
<span data-ttu-id="d78f1-195">若要驗證模型，可將模型狀態傳遞至 CreateErrorResponse 方法，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="d78f1-195">For model validation, the model state can be passed to CreateErrorResponse method as shown below:</span></span> 
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

<span data-ttu-id="d78f1-196">請參閱 [參考] 區段中的連結，以取得在 ASP.Net Web API 中處理例外狀況和驗證模型的其他詳細資料</span><span class="sxs-lookup"><span data-stu-id="d78f1-196">Check the links in the references section for additional details about exceptional handling and model validation in ASP.Net Web API</span></span> 

## <span data-ttu-id="d78f1-197"><a id="messages"></a>請勿在錯誤訊息中公開安全性詳細資料</span><span class="sxs-lookup"><span data-stu-id="d78f1-197"><a id="messages"></a>Do not expose security details in error messages</span></span>

| <span data-ttu-id="d78f1-198">Title</span><span class="sxs-lookup"><span data-stu-id="d78f1-198">Title</span></span>                   | <span data-ttu-id="d78f1-199">詳細資料</span><span class="sxs-lookup"><span data-stu-id="d78f1-199">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="d78f1-200">**元件**</span><span class="sxs-lookup"><span data-stu-id="d78f1-200">**Component**</span></span>               | <span data-ttu-id="d78f1-201">Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="d78f1-201">Web Application</span></span> | 
| <span data-ttu-id="d78f1-202">**SDL 階段**</span><span class="sxs-lookup"><span data-stu-id="d78f1-202">**SDL Phase**</span></span>               | <span data-ttu-id="d78f1-203">建置</span><span class="sxs-lookup"><span data-stu-id="d78f1-203">Build</span></span> |  
| <span data-ttu-id="d78f1-204">**適用的技術**</span><span class="sxs-lookup"><span data-stu-id="d78f1-204">**Applicable Technologies**</span></span> | <span data-ttu-id="d78f1-205">泛型</span><span class="sxs-lookup"><span data-stu-id="d78f1-205">Generic</span></span> |
| <span data-ttu-id="d78f1-206">**屬性**</span><span class="sxs-lookup"><span data-stu-id="d78f1-206">**Attributes**</span></span>              | <span data-ttu-id="d78f1-207">N/A</span><span class="sxs-lookup"><span data-stu-id="d78f1-207">N/A</span></span>  |
| <span data-ttu-id="d78f1-208">**參考**</span><span class="sxs-lookup"><span data-stu-id="d78f1-208">**References**</span></span>              | <span data-ttu-id="d78f1-209">N/A</span><span class="sxs-lookup"><span data-stu-id="d78f1-209">N/A</span></span>  |
| <span data-ttu-id="d78f1-210">**步驟**</span><span class="sxs-lookup"><span data-stu-id="d78f1-210">**Steps**</span></span> | <p><span data-ttu-id="d78f1-211">泛型錯誤訊息會直接提供給使用者，但不會包含敏感性應用程式資料。</span><span class="sxs-lookup"><span data-stu-id="d78f1-211">Generic error messages are provided directly to the user without including sensitive application data.</span></span> <span data-ttu-id="d78f1-212">敏感性資料的範例包括︰</span><span class="sxs-lookup"><span data-stu-id="d78f1-212">Examples of sensitive data include:</span></span></p><ul><li><span data-ttu-id="d78f1-213">伺服器名稱</span><span class="sxs-lookup"><span data-stu-id="d78f1-213">Server names</span></span></li><li><span data-ttu-id="d78f1-214">連接字串</span><span class="sxs-lookup"><span data-stu-id="d78f1-214">Connection strings</span></span></li><li><span data-ttu-id="d78f1-215">使用者名稱</span><span class="sxs-lookup"><span data-stu-id="d78f1-215">Usernames</span></span></li><li><span data-ttu-id="d78f1-216">密碼</span><span class="sxs-lookup"><span data-stu-id="d78f1-216">Passwords</span></span></li><li><span data-ttu-id="d78f1-217">SQL 程序</span><span class="sxs-lookup"><span data-stu-id="d78f1-217">SQL procedures</span></span></li><li><span data-ttu-id="d78f1-218">動態 SQL 失敗的詳細資料</span><span class="sxs-lookup"><span data-stu-id="d78f1-218">Details of dynamic SQL failures</span></span></li><li><span data-ttu-id="d78f1-219">堆疊追蹤和程式碼行</span><span class="sxs-lookup"><span data-stu-id="d78f1-219">Stack trace and lines of code</span></span></li><li><span data-ttu-id="d78f1-220">儲存在記憶體中的變數</span><span class="sxs-lookup"><span data-stu-id="d78f1-220">Variables stored in memory</span></span></li><li><span data-ttu-id="d78f1-221">磁碟機和資料夾的位置</span><span class="sxs-lookup"><span data-stu-id="d78f1-221">Drive and folder locations</span></span></li><li><span data-ttu-id="d78f1-222">應用程式的安裝點</span><span class="sxs-lookup"><span data-stu-id="d78f1-222">Application install points</span></span></li><li><span data-ttu-id="d78f1-223">主機組態設定</span><span class="sxs-lookup"><span data-stu-id="d78f1-223">Host configuration settings</span></span></li><li><span data-ttu-id="d78f1-224">其他內部應用程式詳細資料</span><span class="sxs-lookup"><span data-stu-id="d78f1-224">Other internal application details</span></span></li></ul><p><span data-ttu-id="d78f1-225">捕捉應用程式中的所有錯誤並提供泛型錯誤訊息，以及啟用 IIS 中的自訂錯誤，將有助於避免資訊外洩。</span><span class="sxs-lookup"><span data-stu-id="d78f1-225">Trapping all errors within an application and providing generic error messages, as well as enabling custom errors within IIS will help prevent information disclosure.</span></span> <span data-ttu-id="d78f1-226">除了錯誤處理架構外，SQL Server 資料庫和 .NET 例外狀況處理尤其詳盡，非常適合用於在應用程式中剖析惡意使用者。</span><span class="sxs-lookup"><span data-stu-id="d78f1-226">SQL Server database and .NET Exception handling, among other error handling architectures, are especially verbose and extremely useful to a malicious user profiling your application.</span></span> <span data-ttu-id="d78f1-227">請勿直接顯示衍生自 .NET 例外狀況類別的類別內容，並確定您有適當的例外狀況處理手段，以便不會直接對使用者意外產生非預期的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="d78f1-227">Do not directly display the contents of a class derived from the .NET Exception class, and ensure that you have proper exception handling so that an unexpected exception isn't inadvertently raised directly to the user.</span></span></p><ul><li><span data-ttu-id="d78f1-228">直接提供泛型錯誤訊息給使用者，此訊息是從直接在例外狀況/錯誤訊息中找到的特定詳細資料所抽離出來</span><span class="sxs-lookup"><span data-stu-id="d78f1-228">Provide generic error messages directly to the user that abstract away specific details found directly in the exception/error message</span></span></li><li><span data-ttu-id="d78f1-229">請勿直接向使用者顯示 .NET 例外狀況類別的內容</span><span class="sxs-lookup"><span data-stu-id="d78f1-229">Do not display the contents of a .NET exception class directly to the user</span></span></li><li><span data-ttu-id="d78f1-230">捕捉所有錯誤訊息，並在情況允許時，透過傳送至應用程式用戶端的泛型錯誤訊息通知使用者</span><span class="sxs-lookup"><span data-stu-id="d78f1-230">Trap all error messages and if appropriate inform the user via a generic error message sent to the application client</span></span></li><li><span data-ttu-id="d78f1-231">請勿直接對使用者顯示例外狀況類別的內容，特別是來自 `.ToString()` 的傳回值，或是 Message 或 StackTrace 屬性的值。</span><span class="sxs-lookup"><span data-stu-id="d78f1-231">Do not expose the contents of the Exception class directly to the user, especially the return value from `.ToString()`, or the values of the Message or StackTrace properties.</span></span> <span data-ttu-id="d78f1-232">安全地記錄這項資訊，並向使用者顯示較無害的訊息</span><span class="sxs-lookup"><span data-stu-id="d78f1-232">Securely log this information and display a more innocuous message to the user</span></span></li></ul>|

## <span data-ttu-id="d78f1-233"><a id="default"></a>實作預設的錯誤處理頁面</span><span class="sxs-lookup"><span data-stu-id="d78f1-233"><a id="default"></a>Implement Default error handling page</span></span>

| <span data-ttu-id="d78f1-234">Title</span><span class="sxs-lookup"><span data-stu-id="d78f1-234">Title</span></span>                   | <span data-ttu-id="d78f1-235">詳細資料</span><span class="sxs-lookup"><span data-stu-id="d78f1-235">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="d78f1-236">**元件**</span><span class="sxs-lookup"><span data-stu-id="d78f1-236">**Component**</span></span>               | <span data-ttu-id="d78f1-237">Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="d78f1-237">Web Application</span></span> | 
| <span data-ttu-id="d78f1-238">**SDL 階段**</span><span class="sxs-lookup"><span data-stu-id="d78f1-238">**SDL Phase**</span></span>               | <span data-ttu-id="d78f1-239">建置</span><span class="sxs-lookup"><span data-stu-id="d78f1-239">Build</span></span> |  
| <span data-ttu-id="d78f1-240">**適用的技術**</span><span class="sxs-lookup"><span data-stu-id="d78f1-240">**Applicable Technologies**</span></span> | <span data-ttu-id="d78f1-241">泛型</span><span class="sxs-lookup"><span data-stu-id="d78f1-241">Generic</span></span> |
| <span data-ttu-id="d78f1-242">**屬性**</span><span class="sxs-lookup"><span data-stu-id="d78f1-242">**Attributes**</span></span>              | <span data-ttu-id="d78f1-243">N/A</span><span class="sxs-lookup"><span data-stu-id="d78f1-243">N/A</span></span>  |
| <span data-ttu-id="d78f1-244">**參考**</span><span class="sxs-lookup"><span data-stu-id="d78f1-244">**References**</span></span>              | <span data-ttu-id="d78f1-245">[編輯 ASP.NET 錯誤頁面設定對話方塊](https://technet.microsoft.com/library/dd569096(WS.10).aspx)</span><span class="sxs-lookup"><span data-stu-id="d78f1-245">[Edit ASP.NET Error Pages Settings Dialog Box](https://technet.microsoft.com/library/dd569096(WS.10).aspx)</span></span> |
| <span data-ttu-id="d78f1-246">**步驟**</span><span class="sxs-lookup"><span data-stu-id="d78f1-246">**Steps**</span></span> | <p><span data-ttu-id="d78f1-247">當 ASP.NET 應用程式失敗並造成 HTTP/1.x 500 內部伺服器錯誤時，或當功能組態 (例如要求篩選) 避免顯示頁面時，就會產生錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="d78f1-247">When an ASP.NET application fails and causes an HTTP/1.x 500 Internal Server Error, or a feature configuration (such as Request Filtering) prevents a page from being displayed, an error message will be generated.</span></span> <span data-ttu-id="d78f1-248">系統管理員可以選擇應用程式應該對用戶端顯示容易理解的訊息、對用戶端顯示詳細的錯誤訊息，或只對本機主機顯示詳細的錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="d78f1-248">Administrators can choose whether or not the application should display a friendly message to the client, detailed error message to the client, or detailed error message to localhost only.</span></span> <span data-ttu-id="d78f1-249">web.config 中的 <customErrors> 標籤有三種模式︰</span><span class="sxs-lookup"><span data-stu-id="d78f1-249">The <customErrors> tag in the web.config has three modes:</span></span></p><ul><li><span data-ttu-id="d78f1-250">**開啟︰**指定要啟用自訂錯誤。</span><span class="sxs-lookup"><span data-stu-id="d78f1-250">**On:** Specifies that custom errors are enabled.</span></span> <span data-ttu-id="d78f1-251">如果未指定任何 defaultRedirect 屬性，則使用者會看到泛型錯誤。</span><span class="sxs-lookup"><span data-stu-id="d78f1-251">If no defaultRedirect attribute is specified, users see a generic error.</span></span> <span data-ttu-id="d78f1-252">自訂錯誤會顯示給遠端用戶端和本機主機</span><span class="sxs-lookup"><span data-stu-id="d78f1-252">The custom errors are shown to the remote clients and to the local host</span></span></li><li><span data-ttu-id="d78f1-253">**關閉︰**指定要停用自訂錯誤。</span><span class="sxs-lookup"><span data-stu-id="d78f1-253">**Off:** Specifies that custom errors are disabled.</span></span> <span data-ttu-id="d78f1-254">詳細的 ASP.NET 錯誤會顯示給遠端用戶端和本機主機</span><span class="sxs-lookup"><span data-stu-id="d78f1-254">The detailed ASP.NET errors are shown to the remote clients and to the local host</span></span></li><li><span data-ttu-id="d78f1-255">**RemoteOnly：**指定自訂錯誤只顯示給遠端用戶端，而將 ASP.NET 錯誤顯示給本機主機。</span><span class="sxs-lookup"><span data-stu-id="d78f1-255">**RemoteOnly:** Specifies that custom errors are shown only to the remote clients, and that ASP.NET errors are shown to the local host.</span></span> <span data-ttu-id="d78f1-256">這是預設值</span><span class="sxs-lookup"><span data-stu-id="d78f1-256">This is the default value</span></span></li></ul><p><span data-ttu-id="d78f1-257">開啟應用程式/網站的 `web.config` 檔案，並確定標籤已定義 `<customErrors mode="RemoteOnly" />` 或 `<customErrors mode="On" />`。</span><span class="sxs-lookup"><span data-stu-id="d78f1-257">Open the `web.config` file for the application/site and ensure that the tag has either `<customErrors mode="RemoteOnly" />` or `<customErrors mode="On" />` defined.</span></span></p>|

## <span data-ttu-id="d78f1-258"><a id="deployment"></a>設定要在 IIS 中零售的部署方法</span><span class="sxs-lookup"><span data-stu-id="d78f1-258"><a id="deployment"></a>Set Deployment Method to Retail in IIS</span></span>

| <span data-ttu-id="d78f1-259">Title</span><span class="sxs-lookup"><span data-stu-id="d78f1-259">Title</span></span>                   | <span data-ttu-id="d78f1-260">詳細資料</span><span class="sxs-lookup"><span data-stu-id="d78f1-260">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="d78f1-261">**元件**</span><span class="sxs-lookup"><span data-stu-id="d78f1-261">**Component**</span></span>               | <span data-ttu-id="d78f1-262">Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="d78f1-262">Web Application</span></span> | 
| <span data-ttu-id="d78f1-263">**SDL 階段**</span><span class="sxs-lookup"><span data-stu-id="d78f1-263">**SDL Phase**</span></span>               | <span data-ttu-id="d78f1-264">部署</span><span class="sxs-lookup"><span data-stu-id="d78f1-264">Deployment</span></span> |  
| <span data-ttu-id="d78f1-265">**適用的技術**</span><span class="sxs-lookup"><span data-stu-id="d78f1-265">**Applicable Technologies**</span></span> | <span data-ttu-id="d78f1-266">泛型</span><span class="sxs-lookup"><span data-stu-id="d78f1-266">Generic</span></span> |
| <span data-ttu-id="d78f1-267">**屬性**</span><span class="sxs-lookup"><span data-stu-id="d78f1-267">**Attributes**</span></span>              | <span data-ttu-id="d78f1-268">N/A</span><span class="sxs-lookup"><span data-stu-id="d78f1-268">N/A</span></span>  |
| <span data-ttu-id="d78f1-269">**參考**</span><span class="sxs-lookup"><span data-stu-id="d78f1-269">**References**</span></span>              | <span data-ttu-id="d78f1-270">[部署元素 (ASP.NET 設定結構描述)](https://msdn.microsoft.com/library/ms228298(VS.80).aspx)</span><span class="sxs-lookup"><span data-stu-id="d78f1-270">[deployment Element (ASP.NET Settings Schema)](https://msdn.microsoft.com/library/ms228298(VS.80).aspx)</span></span> |
| <span data-ttu-id="d78f1-271">**步驟**</span><span class="sxs-lookup"><span data-stu-id="d78f1-271">**Steps**</span></span> | <p><span data-ttu-id="d78f1-272">`<deployment retail>` 參數是要供生產 IIS 伺服器使用。</span><span class="sxs-lookup"><span data-stu-id="d78f1-272">The `<deployment retail>` switch is intended for use by production IIS servers.</span></span> <span data-ttu-id="d78f1-273">這個參數可用來協助應用程式以最佳效能和最低安全性資訊外洩可能性來執行，方法是停用應用程式對頁面產生追蹤輸出的能力、停用對使用者顯示詳細錯誤訊息的能力，以及停用偵錯參數。</span><span class="sxs-lookup"><span data-stu-id="d78f1-273">This switch is used to help applications run with the best possible performance and least possible security information leakages by disabling the application's ability to generate trace output on a page, disabling the ability to display detailed error messages to end users, and disabling the debug switch.</span></span></p><p><span data-ttu-id="d78f1-274">在開發期間，經常會啟用專供開發人員使用的參數和選項，例如失敗要求追蹤和偵錯。</span><span class="sxs-lookup"><span data-stu-id="d78f1-274">Often times, switches and options that are developer-focused, such as failed request tracing and debugging, are enabled during active development.</span></span> <span data-ttu-id="d78f1-275">建議您將任何生產伺服器上的部署方法設為零售。</span><span class="sxs-lookup"><span data-stu-id="d78f1-275">It is recommended that the deployment method on any production server be set to retail.</span></span> <span data-ttu-id="d78f1-276">開啟 machine.config 檔，並確定 `<deployment retail="true" />` 維持設定為 true。</span><span class="sxs-lookup"><span data-stu-id="d78f1-276">open the machine.config file and ensure that `<deployment retail="true" />` remains set to true.</span></span></p>|

## <span data-ttu-id="d78f1-277"><a id="fail"></a>例外狀況應安全地失敗</span><span class="sxs-lookup"><span data-stu-id="d78f1-277"><a id="fail"></a>Exceptions should fail safely</span></span>

| <span data-ttu-id="d78f1-278">Title</span><span class="sxs-lookup"><span data-stu-id="d78f1-278">Title</span></span>                   | <span data-ttu-id="d78f1-279">詳細資料</span><span class="sxs-lookup"><span data-stu-id="d78f1-279">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="d78f1-280">**元件**</span><span class="sxs-lookup"><span data-stu-id="d78f1-280">**Component**</span></span>               | <span data-ttu-id="d78f1-281">Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="d78f1-281">Web Application</span></span> | 
| <span data-ttu-id="d78f1-282">**SDL 階段**</span><span class="sxs-lookup"><span data-stu-id="d78f1-282">**SDL Phase**</span></span>               | <span data-ttu-id="d78f1-283">建置</span><span class="sxs-lookup"><span data-stu-id="d78f1-283">Build</span></span> |  
| <span data-ttu-id="d78f1-284">**適用的技術**</span><span class="sxs-lookup"><span data-stu-id="d78f1-284">**Applicable Technologies**</span></span> | <span data-ttu-id="d78f1-285">泛型</span><span class="sxs-lookup"><span data-stu-id="d78f1-285">Generic</span></span> |
| <span data-ttu-id="d78f1-286">**屬性**</span><span class="sxs-lookup"><span data-stu-id="d78f1-286">**Attributes**</span></span>              | <span data-ttu-id="d78f1-287">N/A</span><span class="sxs-lookup"><span data-stu-id="d78f1-287">N/A</span></span>  |
| <span data-ttu-id="d78f1-288">**參考**</span><span class="sxs-lookup"><span data-stu-id="d78f1-288">**References**</span></span>              | [<span data-ttu-id="d78f1-289">安全地失敗</span><span class="sxs-lookup"><span data-stu-id="d78f1-289">Fail securely</span></span>](https://www.owasp.org/index.php/Fail_securely) |
| <span data-ttu-id="d78f1-290">**步驟**</span><span class="sxs-lookup"><span data-stu-id="d78f1-290">**Steps**</span></span> | <span data-ttu-id="d78f1-291">應用程式應安全地失敗。</span><span class="sxs-lookup"><span data-stu-id="d78f1-291">Application should fail safely.</span></span> <span data-ttu-id="d78f1-292">任何會傳回布林值的方法 (根據所做出的特定決策) 皆應小心地建立例外狀況區塊。</span><span class="sxs-lookup"><span data-stu-id="d78f1-292">Any method that returns a Boolean value, based on which certain decision is made, should have exception block carefully created.</span></span> <span data-ttu-id="d78f1-293">若草率撰寫例外狀況區塊，會因為不知不覺潛入的安全性問題而產生許多邏輯錯誤。</span><span class="sxs-lookup"><span data-stu-id="d78f1-293">There are lot of logical errors due to which security issues creep in, when the exception block is written carelessly.</span></span>|

### <a name="example"></a><span data-ttu-id="d78f1-294">範例</span><span class="sxs-lookup"><span data-stu-id="d78f1-294">Example</span></span>
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
                        //// Adding additional check to enable CMS urls if they are not hosted on same domain.
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
<span data-ttu-id="d78f1-295">如果發生某些例外狀況，上述方法一律會傳回 True。</span><span class="sxs-lookup"><span data-stu-id="d78f1-295">The above method will always return True, if some exception happens.</span></span> <span data-ttu-id="d78f1-296">如果使用者提供格式不正確的 URL，瀏覽器加以採用但 `Uri()` 建構函式未採用，就會擲回例外狀況，並將受害者導向有效但格式不正確的 URL。</span><span class="sxs-lookup"><span data-stu-id="d78f1-296">If the end user provides a malformed URL, that the browser respects, but the `Uri()` constructor doesn't, this will throw an exception, and the victim will be taken to the valid but malformed URL.</span></span> 