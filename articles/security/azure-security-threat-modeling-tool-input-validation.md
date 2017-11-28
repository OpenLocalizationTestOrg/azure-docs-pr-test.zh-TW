---
title: "輸入驗證 - Microsoft 威脅模型化工具 - Azure | Microsoft Docs"
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
ms.openlocfilehash: b7ce6f353cf8cf48d5fb038ee77b0d3fdae16fb7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="security-frame-input-validation--mitigations"></a><span data-ttu-id="a8e7f-103">安全性架構︰輸入驗證 | 風險降低</span><span class="sxs-lookup"><span data-stu-id="a8e7f-103">Security Frame: Input Validation | Mitigations</span></span> 
| <span data-ttu-id="a8e7f-104">產品/服務</span><span class="sxs-lookup"><span data-stu-id="a8e7f-104">Product/Service</span></span> | <span data-ttu-id="a8e7f-105">文章</span><span class="sxs-lookup"><span data-stu-id="a8e7f-105">Article</span></span> |
| --------------- | ------- |
| <span data-ttu-id="a8e7f-106">**Web 應用程式**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-106">**Web Application**</span></span> | <ul><li>[<span data-ttu-id="a8e7f-107">停用所有使用未受信任樣式表之轉換的 XSLT 指令碼</span><span class="sxs-lookup"><span data-stu-id="a8e7f-107">Disable XSLT scripting for all transforms using untrusted style sheets</span></span>](#disable-xslt)</li><li>[<span data-ttu-id="a8e7f-108">確定可能包含使用者可控制內容的每個頁面都選擇不要自動探查 MIME</span><span class="sxs-lookup"><span data-stu-id="a8e7f-108">Ensure that each page that could contain user controllable content opts out of automatic MIME sniffing</span></span>](#out-sniffing)</li><li>[<span data-ttu-id="a8e7f-109">強化或停用 XML 實體解析</span><span class="sxs-lookup"><span data-stu-id="a8e7f-109">Harden or Disable XML Entity Resolution</span></span>](#xml-resolution)</li><li>[<span data-ttu-id="a8e7f-110">利用 http.sys 的應用程式會執行 URL 標準化驗證</span><span class="sxs-lookup"><span data-stu-id="a8e7f-110">Applications utilizing http.sys perform URL canonicalization verification</span></span>](#app-verification)</li><li>[<span data-ttu-id="a8e7f-111">確定在接受使用者的檔案時已備妥適當的控制</span><span class="sxs-lookup"><span data-stu-id="a8e7f-111">Ensure appropriate controls are in place when accepting files from users</span></span>](#controls-users)</li><li>[<span data-ttu-id="a8e7f-112">確定 Web 應用程式有使用 type-safe 參數來存取資料</span><span class="sxs-lookup"><span data-stu-id="a8e7f-112">Ensure that type-safe parameters are used in Web Application for data access</span></span>](#typesafe)</li><li>[<span data-ttu-id="a8e7f-113">使用個別的模型繫結類別或繫結篩選清單來防止 MVC 大量指派弱點</span><span class="sxs-lookup"><span data-stu-id="a8e7f-113">Use separate model binding classes or binding filter lists to prevent MVC mass assignment vulnerability</span></span>](#binding-mvc)</li><li>[<span data-ttu-id="a8e7f-114">先將未受信任的 Web 輸出編碼再進行轉譯</span><span class="sxs-lookup"><span data-stu-id="a8e7f-114">Encode untrusted web output prior to rendering</span></span>](#rendering)</li><li>[<span data-ttu-id="a8e7f-115">對所有字串類型的模型屬性執行輸入驗證和篩選</span><span class="sxs-lookup"><span data-stu-id="a8e7f-115">Perform input validation and filtering on all string type Model properties</span></span>](#typemodel)</li><li>[<span data-ttu-id="a8e7f-116">應該對接受所有字元的表單欄位 (例如 RTF 編輯器) 套用清理</span><span class="sxs-lookup"><span data-stu-id="a8e7f-116">Sanitization should be applied on form fields that accept all characters, e.g, rich text editor</span></span>](#richtext)</li><li>[<span data-ttu-id="a8e7f-117">請勿將沒有內建編碼的 DOM 元素指派給接收器</span><span class="sxs-lookup"><span data-stu-id="a8e7f-117">Do not assign DOM elements to sinks that do not have inbuilt encoding</span></span>](#inbuilt-encode)</li><li>[<span data-ttu-id="a8e7f-118">驗證應用程式內的所有重新導向皆已關閉或安全完成</span><span class="sxs-lookup"><span data-stu-id="a8e7f-118">Validate all redirects within the application are closed or done safely</span></span>](#redirect-safe)</li><li>[<span data-ttu-id="a8e7f-119">對控制器方法所接受的所有字串類型參數實作輸入驗證</span><span class="sxs-lookup"><span data-stu-id="a8e7f-119">Implement input validation on all string type parameters accepted by Controller methods</span></span>](#string-method)</li><li>[<span data-ttu-id="a8e7f-120">為規則運算式處理設定逾時上限以防止因規則運算式不正確而導致 DoS</span><span class="sxs-lookup"><span data-stu-id="a8e7f-120">Set upper limit timeout for regular expression processing to prevent DoS due to bad regular expressions</span></span>](#dos-expression)</li><li>[<span data-ttu-id="a8e7f-121">避免在 Razor 檢視中使用 Html.Raw</span><span class="sxs-lookup"><span data-stu-id="a8e7f-121">Avoid using Html.Raw in Razor views</span></span>](#html-razor)</li></ul> | 
| <span data-ttu-id="a8e7f-122">**資料庫**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-122">**Database**</span></span> | <ul><li>[<span data-ttu-id="a8e7f-123">請勿在預存程序中使用動態查詢</span><span class="sxs-lookup"><span data-stu-id="a8e7f-123">Do not use dynamic queries in stored procedures</span></span>](#stored-proc)</li></ul> |
| <span data-ttu-id="a8e7f-124">**Web API**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-124">**Web API**</span></span> | <ul><li>[<span data-ttu-id="a8e7f-125">確定 Web API 方法已完成模型驗證</span><span class="sxs-lookup"><span data-stu-id="a8e7f-125">Ensure that model validation is done on Web API methods</span></span>](#validation-api)</li><li>[<span data-ttu-id="a8e7f-126">對 Web API 方法所接受的所有字串類型參數實作輸入驗證</span><span class="sxs-lookup"><span data-stu-id="a8e7f-126">Implement input validation on all string type parameters accepted by Web API methods</span></span>](#string-api)</li><li>[<span data-ttu-id="a8e7f-127">確定 Web API 有使用 type-safe 參數來存取資料</span><span class="sxs-lookup"><span data-stu-id="a8e7f-127">Ensure that type-safe parameters are used in Web API for data access</span></span>](#typesafe-api)</li></ul> | 
| <span data-ttu-id="a8e7f-128">**Azure Document DB**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-128">**Azure Document DB**</span></span> | <ul><li>[<span data-ttu-id="a8e7f-129">針對 DocumentDB 使用參數化 SQL 查詢</span><span class="sxs-lookup"><span data-stu-id="a8e7f-129">Use parametrized SQL queries for DocumentDB</span></span>](#sql-docdb)</li></ul> | 
| <span data-ttu-id="a8e7f-130">**WCF**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-130">**WCF**</span></span> | <ul><li>[<span data-ttu-id="a8e7f-131">透過結構描述繫結驗證 WCF 輸入</span><span class="sxs-lookup"><span data-stu-id="a8e7f-131">WCF Input validation through Schema binding</span></span>](#schema-binding)</li><li>[<span data-ttu-id="a8e7f-132">透過參數偵測器驗證 WCF 輸入</span><span class="sxs-lookup"><span data-stu-id="a8e7f-132">WCF- Input validation through Parameter Inspectors</span></span>](#parameters)</li></ul> |

## <span data-ttu-id="a8e7f-133"><a id="disable-xslt"></a>停用所有使用未受信任樣式表之轉換的 XSLT 指令碼</span><span class="sxs-lookup"><span data-stu-id="a8e7f-133"><a id="disable-xslt"></a>Disable XSLT scripting for all transforms using untrusted style sheets</span></span>

| <span data-ttu-id="a8e7f-134">Title</span><span class="sxs-lookup"><span data-stu-id="a8e7f-134">Title</span></span>                   | <span data-ttu-id="a8e7f-135">詳細資料</span><span class="sxs-lookup"><span data-stu-id="a8e7f-135">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="a8e7f-136">**元件**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-136">**Component**</span></span>               | <span data-ttu-id="a8e7f-137">Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="a8e7f-137">Web Application</span></span> | 
| <span data-ttu-id="a8e7f-138">**SDL 階段**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-138">**SDL Phase**</span></span>               | <span data-ttu-id="a8e7f-139">建置</span><span class="sxs-lookup"><span data-stu-id="a8e7f-139">Build</span></span> |  
| <span data-ttu-id="a8e7f-140">**適用的技術**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-140">**Applicable Technologies**</span></span> | <span data-ttu-id="a8e7f-141">泛型</span><span class="sxs-lookup"><span data-stu-id="a8e7f-141">Generic</span></span> |
| <span data-ttu-id="a8e7f-142">**屬性**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-142">**Attributes**</span></span>              | <span data-ttu-id="a8e7f-143">N/A</span><span class="sxs-lookup"><span data-stu-id="a8e7f-143">N/A</span></span>  |
| <span data-ttu-id="a8e7f-144">**參考**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-144">**References**</span></span>              | <span data-ttu-id="a8e7f-145">[XSLT 安全性](https://msdn.microsoft.com/library/ms763800(v=vs.85).aspx)、[XsltSettings.EnableScript 屬性](http://msdn.microsoft.com/library/system.xml.xsl.xsltsettings.enablescript.aspx)</span><span class="sxs-lookup"><span data-stu-id="a8e7f-145">[XSLT Security](https://msdn.microsoft.com/library/ms763800(v=vs.85).aspx), [XsltSettings.EnableScript Property](http://msdn.microsoft.com/library/system.xml.xsl.xsltsettings.enablescript.aspx)</span></span> |
| <span data-ttu-id="a8e7f-146">**步驟**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-146">**Steps**</span></span> | <span data-ttu-id="a8e7f-147">XSLT 支援在使用 `<msxml:script>` 元素的樣式表內編寫指令碼。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-147">XSLT supports scripting inside style sheets using the `<msxml:script>` element.</span></span> <span data-ttu-id="a8e7f-148">這可讓自訂函式用於 XSLT 轉換。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-148">This allows custom functions to be used in an XSLT transformation.</span></span> <span data-ttu-id="a8e7f-149">指令碼會在執行轉換的程序內容下執行。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-149">The script is executed under the context of the process performing the transform.</span></span> <span data-ttu-id="a8e7f-150">在未受信任的環境時必須停用 XSLT 指令碼，以防止執行未受信任的程式碼。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-150">XSLT script must be disabled when in an untrusted environment to prevent execution of untrusted code.</span></span> <span data-ttu-id="a8e7f-151">如果使用 .NET：預設會停用 XSLT 指令碼；不過，您必須確認它尚未透過 `XsltSettings.EnableScript` 屬性加以明確啟用。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-151">*If using .NET:* XSLT scripting is disabled by default; however, you must ensure that it has not been explicitly enabled through the `XsltSettings.EnableScript` property.</span></span>|

### <a name="example"></a><span data-ttu-id="a8e7f-152">範例</span><span class="sxs-lookup"><span data-stu-id="a8e7f-152">Example</span></span> 

```C#
XsltSettings settings = new XsltSettings();
settings.EnableScript = true; // WRONG: THIS SHOULD BE SET TO false
```

### <a name="example"></a><span data-ttu-id="a8e7f-153">範例</span><span class="sxs-lookup"><span data-stu-id="a8e7f-153">Example</span></span>
<span data-ttu-id="a8e7f-154">如果使用 MSXML 6.0，預設會停用 XSLT 指令碼；不過，您必須確認它尚未透過 XML DOM 物件屬性 AllowXsltScript 加以明確啟用。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-154">If you are using using MSXML 6.0, XSLT scripting is disabled by default; however, you must ensure that it has not been explicitly enabled through the XML DOM object property AllowXsltScript.</span></span> 

```C#
doc.setProperty("AllowXsltScript", true); // WRONG: THIS SHOULD BE SET TO false
```

### <a name="example"></a><span data-ttu-id="a8e7f-155">範例</span><span class="sxs-lookup"><span data-stu-id="a8e7f-155">Example</span></span>
<span data-ttu-id="a8e7f-156">如果您使用 MSXML 5 或較低版本，預設會啟用 XSLT 指令碼，因此您必須明確地加以停用。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-156">If you are using MSXML 5 or below, XSLT scripting is enabled by default and you must explicitly disable it.</span></span> <span data-ttu-id="a8e7f-157">請將 XML DOM 物件屬性 AllowXsltScript 設為 false。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-157">Set the XML DOM object property AllowXsltScript to false.</span></span> 

```C#
doc.setProperty("AllowXsltScript", false); // CORRECT. Setting to false disables XSLT scripting.
```

## <span data-ttu-id="a8e7f-158"><a id="out-sniffing"></a>確定可能包含使用者可控制內容的每個頁面都選擇不要自動探查 MIME</span><span class="sxs-lookup"><span data-stu-id="a8e7f-158"><a id="out-sniffing"></a>Ensure that each page that could contain user controllable content opts out of automatic MIME sniffing</span></span>

| <span data-ttu-id="a8e7f-159">Title</span><span class="sxs-lookup"><span data-stu-id="a8e7f-159">Title</span></span>                   | <span data-ttu-id="a8e7f-160">詳細資料</span><span class="sxs-lookup"><span data-stu-id="a8e7f-160">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="a8e7f-161">**元件**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-161">**Component**</span></span>               | <span data-ttu-id="a8e7f-162">Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="a8e7f-162">Web Application</span></span> | 
| <span data-ttu-id="a8e7f-163">**SDL 階段**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-163">**SDL Phase**</span></span>               | <span data-ttu-id="a8e7f-164">建置</span><span class="sxs-lookup"><span data-stu-id="a8e7f-164">Build</span></span> |  
| <span data-ttu-id="a8e7f-165">**適用的技術**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-165">**Applicable Technologies**</span></span> | <span data-ttu-id="a8e7f-166">泛型</span><span class="sxs-lookup"><span data-stu-id="a8e7f-166">Generic</span></span> |
| <span data-ttu-id="a8e7f-167">**屬性**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-167">**Attributes**</span></span>              | <span data-ttu-id="a8e7f-168">N/A</span><span class="sxs-lookup"><span data-stu-id="a8e7f-168">N/A</span></span>  |
| <span data-ttu-id="a8e7f-169">**參考**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-169">**References**</span></span>              | [<span data-ttu-id="a8e7f-170">IE8 安全性單元五 - 完善的保護</span><span class="sxs-lookup"><span data-stu-id="a8e7f-170">IE8 Security Part V - Comprehensive Protection</span></span>](http://blogs.msdn.com/ie/archive/2008/07/02/ie8-security-part-v-comprehensive-protection.aspx)  |
| <span data-ttu-id="a8e7f-171">**步驟**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-171">**Steps**</span></span> | <p><span data-ttu-id="a8e7f-172">對於可能包含使用者可控制內容的每個頁面，您必須使用 HTTP 標頭 `X-Content-Type-Options:nosniff`。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-172">For each page that could contain user controllable content, you must use the HTTP Header `X-Content-Type-Options:nosniff`.</span></span> <span data-ttu-id="a8e7f-173">若要符合此需求，您可以單獨針對可能包含使用者可控制內容的頁面逐頁設定此必要標頭，或者，您也可以針對應用程式中的所有頁面全域設定此標頭。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-173">To comply with this requirement, you can either set the required header page by page for only those pages that might contain user-controllable content, or you can set it globally for all pages in the application.</span></span></p><p><span data-ttu-id="a8e7f-174">從 Web 伺服器傳遞過來之檔案的每個類型都有相關聯的 [MIME 類型](http://en.wikipedia.org/wiki/Mime_type) (也稱為「內容類型」)，以描述內容的本質 (也就是影像、文字、應用程式等)</span><span class="sxs-lookup"><span data-stu-id="a8e7f-174">Each type of file delivered from a web server has an associated [MIME type](http://en.wikipedia.org/wiki/Mime_type) (also called a *content-type*) that describes the nature of the content (that is, image, text, application, etc.)</span></span></p><p><span data-ttu-id="a8e7f-175">X-Content-Type-Options 標頭是可讓開發人員指定不應對其內容探查 MIME 的 HTTP 標頭。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-175">The X-Content-Type-Options header is an HTTP header that allows developers to specify that their content should not be MIME-sniffed.</span></span> <span data-ttu-id="a8e7f-176">此標頭是設計用來降低 MIME 探查攻擊的風險。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-176">This header is designed to mitigate MIME-Sniffing attacks.</span></span> <span data-ttu-id="a8e7f-177">Internet Explorer 8 (IE8) 已新增對此標頭的支援</span><span class="sxs-lookup"><span data-stu-id="a8e7f-177">Support for this header was added in Internet Explorer 8 (IE8)</span></span></p><p><span data-ttu-id="a8e7f-178">只有 Internet Explorer 8 (IE8) 的使用者能夠受益於 X-Content-Type-Options。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-178">Only users of Internet Explorer 8 (IE8) will benefit from X-Content-Type-Options.</span></span> <span data-ttu-id="a8e7f-179">舊版 Internet Explorer 目前不採用 X-Content-Type-Options 標頭</span><span class="sxs-lookup"><span data-stu-id="a8e7f-179">Previous versions of Internet Explorer do not currently respect the X-Content-Type-Options header</span></span></p><p><span data-ttu-id="a8e7f-180">Internet Explorer 8 (和更新版本) 是主要瀏覽器中唯一實作了可選擇不要 MIME 探查功能的瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-180">Internet Explorer 8 (and later) are the only major browsers to implement a MIME-sniffing opt-out feature.</span></span> <span data-ttu-id="a8e7f-181">當其他主要瀏覽器 (Firefox、Safari、Chrome) 實作了類似功能時，我們會更新這項建議，使其也包含這些瀏覽器的語法</span><span class="sxs-lookup"><span data-stu-id="a8e7f-181">If and when other major browsers (Firefox, Safari, Chrome) implement similar features, this recommendation will be updated to include syntax for those browsers as well</span></span></p>|

### <a name="example"></a><span data-ttu-id="a8e7f-182">範例</span><span class="sxs-lookup"><span data-stu-id="a8e7f-182">Example</span></span>
<span data-ttu-id="a8e7f-183">若要為應用程式中的所有頁面全域啟用必要標頭，您可以執行下列其中一項︰</span><span class="sxs-lookup"><span data-stu-id="a8e7f-183">To enable the required header globally for all pages in the application, you can do one of the following:</span></span> 

* <span data-ttu-id="a8e7f-184">如果應用程式是由 Internet Information Services (IIS) 7 所裝載，請在 web.config 檔案中新增標頭</span><span class="sxs-lookup"><span data-stu-id="a8e7f-184">Add the header in the web.config file if the application is hosted by Internet Information Services (IIS) 7</span></span> 

```
<system.webServer> 
  <httpProtocol> 
    <customHeaders> 
      <add name=""X-Content-Type-Options"" value=""nosniff""/>
    </customHeaders>
  </httpProtocol>
</system.webServer> 
```

* <span data-ttu-id="a8e7f-185">透過全域 Application\_BeginRequest 新增標頭</span><span class="sxs-lookup"><span data-stu-id="a8e7f-185">Add the header through the global Application\_BeginRequest</span></span> 

``` 
void Application_BeginRequest(object sender, EventArgs e)
{
  this.Response.Headers[""X-Content-Type-Options""] = ""nosniff"";
} 
```

* <span data-ttu-id="a8e7f-186">實作自訂 HTTP 模組</span><span class="sxs-lookup"><span data-stu-id="a8e7f-186">Implement custom HTTP module</span></span> 

``` 
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
        if (application.Response.Headers[""X-Content-Type-Options ""] != null) 
          return; 
        application.Response.Headers.Add(""X-Content-Type-Options "", ""nosniff""); 
      } 
  } 

``` 

* <span data-ttu-id="a8e7f-187">您可以透過將必要標頭新增至個別回應，來單獨針對特定頁面啟用此標頭︰</span><span class="sxs-lookup"><span data-stu-id="a8e7f-187">You can enable the required header only for specific pages by adding it to individual responses:</span></span> 

```
this.Response.Headers[""X-Content-Type-Options""] = ""nosniff""; 
``` 

## <span data-ttu-id="a8e7f-188"><a id="xml-resolution"></a>強化或停用 XML 實體解析</span><span class="sxs-lookup"><span data-stu-id="a8e7f-188"><a id="xml-resolution"></a>Harden or Disable XML Entity Resolution</span></span>

| <span data-ttu-id="a8e7f-189">Title</span><span class="sxs-lookup"><span data-stu-id="a8e7f-189">Title</span></span>                   | <span data-ttu-id="a8e7f-190">詳細資料</span><span class="sxs-lookup"><span data-stu-id="a8e7f-190">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="a8e7f-191">**元件**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-191">**Component**</span></span>               | <span data-ttu-id="a8e7f-192">Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="a8e7f-192">Web Application</span></span> | 
| <span data-ttu-id="a8e7f-193">**SDL 階段**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-193">**SDL Phase**</span></span>               | <span data-ttu-id="a8e7f-194">建置</span><span class="sxs-lookup"><span data-stu-id="a8e7f-194">Build</span></span> |  
| <span data-ttu-id="a8e7f-195">**適用的技術**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-195">**Applicable Technologies**</span></span> | <span data-ttu-id="a8e7f-196">泛型</span><span class="sxs-lookup"><span data-stu-id="a8e7f-196">Generic</span></span> |
| <span data-ttu-id="a8e7f-197">**屬性**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-197">**Attributes**</span></span>              | <span data-ttu-id="a8e7f-198">N/A</span><span class="sxs-lookup"><span data-stu-id="a8e7f-198">N/A</span></span>  |
| <span data-ttu-id="a8e7f-199">**參考**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-199">**References**</span></span>              | <span data-ttu-id="a8e7f-200">[XML 實體擴充](http://capec.mitre.org/data/definitions/197.html)、[XML 阻斷服務攻擊與防禦](http://msdn.microsoft.com/magazine/ee335713.aspx)、[MSXML 安全性概觀](http://msdn.microsoft.com/library/ms754611(v=VS.85).aspx)、[保護 MSXML 程式碼的最佳作法](http://msdn.microsoft.com/library/ms759188(VS.85).aspx)、[NSXMLParserDelegate 通訊協定參考](http://developer.apple.com/library/ios/#documentation/cocoa/reference/NSXMLParserDelegate_Protocol/Reference/Reference.html)、[解析外部參考](https://msdn.microsoft.com/library/5fcwybb2.aspx)</span><span class="sxs-lookup"><span data-stu-id="a8e7f-200">[XML Entity Expansion](http://capec.mitre.org/data/definitions/197.html), [XML Denial of Service Attacks and Defenses](http://msdn.microsoft.com/magazine/ee335713.aspx), [MSXML Security Overview](http://msdn.microsoft.com/library/ms754611(v=VS.85).aspx), [Best Practices for Securing MSXML Code](http://msdn.microsoft.com/library/ms759188(VS.85).aspx), [NSXMLParserDelegate Protocol Reference](http://developer.apple.com/library/ios/#documentation/cocoa/reference/NSXMLParserDelegate_Protocol/Reference/Reference.html), [Resolving External References](https://msdn.microsoft.com/library/5fcwybb2.aspx)</span></span> |
| <span data-ttu-id="a8e7f-201">**步驟**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-201">**Steps**</span></span>| <p><span data-ttu-id="a8e7f-202">雖然未被廣泛使用，但有一項 XML 功能可讓 XML 剖析器使用在文件本身內或從外部來源所定義的值，來擴充巨集實體。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-202">Although it is not widely used, there is a feature of XML that allows the XML parser to expand macro entities with values defined either within the document itself or from external sources.</span></span> <span data-ttu-id="a8e7f-203">例如，文件可能會使用值 "Microsoft" 定義實體 "companyname"，以便在每次文件中出現文字 "&companyname;" 時，就自動以文字 Microsoft 加以取代。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-203">For example, the document might define an entity "companyname" with the value "Microsoft," so that every time the text "&companyname;" appears in the document, it is automatically replaced with the text Microsoft.</span></span> <span data-ttu-id="a8e7f-204">或者，文件可能會定義參考外部 Web 服務的實體 "MSFTStock"，以擷取 Microsoft 股票的目前股價。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-204">Or, the document might define an entity "MSFTStock" that references an external web service to fetch the current value of Microsoft stock.</span></span></p><p><span data-ttu-id="a8e7f-205">然後，每當文件中出現 "&MSFTStock;" 時，就自動以目前股價加以取代。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-205">Then any time "&MSFTStock;" appears in the document, it is automatically replaced with the current stock price.</span></span> <span data-ttu-id="a8e7f-206">不過，這項功能可能會遭到濫用，來造成阻斷服務 (DoS) 狀況。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-206">However, this functionality can be abused to create denial of service (DoS) conditions.</span></span> <span data-ttu-id="a8e7f-207">攻擊者可以巢狀多個實體以建立會在系統上所有可用的記憶體消耗指數擴充 XML 定。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-207">An attacker can nest multiple entities to create an exponential expansion XML bomb that consumes all available memory on the system.</span></span> </p><p><span data-ttu-id="a8e7f-208">或者，他也可以建立外部參考，以往回串流無限量的資料，或讓執行緒停止回應。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-208">Alternatively, he can create an external reference that streams back an infinite amount of data or that simply hangs the thread.</span></span> <span data-ttu-id="a8e7f-209">因此，所有小組必須完全停用其應用程式並未使用的內部及/或外部 XML 實體解析，或以手動方式限制可供應用程式取用來解析實體的記憶體和時間量 (如果這項功能有其絕對必要)。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-209">As a result, all teams must disable internal and/or external XML entity resolution entirely if their application does not use it, or manually limit the amount of memory and time that the application can consume for entity resolution if this functionality is absolutely necessary.</span></span> <span data-ttu-id="a8e7f-210">如果應用程式不需要解析實體，則請停用。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-210">If entity resolution is not required by your application, then disable it.</span></span> </p>|

### <a name="example"></a><span data-ttu-id="a8e7f-211">範例</span><span class="sxs-lookup"><span data-stu-id="a8e7f-211">Example</span></span>
<span data-ttu-id="a8e7f-212">針對 .NET Framework 程式碼，您可以使用下列方法︰</span><span class="sxs-lookup"><span data-stu-id="a8e7f-212">For .NET Framework code, you can use the following approaches:</span></span>

```C#
XmlTextReader reader = new XmlTextReader(stream);
reader.ProhibitDtd = true;

XmlReaderSettings settings = new XmlReaderSettings();
settings.ProhibitDtd = true;
XmlReader reader = XmlReader.Create(stream, settings);

// for .NET 4
XmlReaderSettings settings = new XmlReaderSettings();
settings.DtdProcessing = DtdProcessing.Prohibit;
XmlReader reader = XmlReader.Create(stream, settings);
```
<span data-ttu-id="a8e7f-213">請注意，`ProhibitDtd` 在 `XmlReaderSettings` 中的預設值為 true，但在 `XmlTextReader` 中則為 false。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-213">Note that the default value of `ProhibitDtd` in `XmlReaderSettings` is true, but in `XmlTextReader` it is false.</span></span> <span data-ttu-id="a8e7f-214">如果您使用 XmlReaderSettings，則不需要將 ProhibitDtd 明確設為 true，但為了安全起見，建議您這麼做。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-214">If you are using XmlReaderSettings, you do not need to set ProhibitDtd to true explicitly, but it is recommended for safety sake that you do.</span></span> <span data-ttu-id="a8e7f-215">也請注意，XmlDocument 類別預設會允許解析實體。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-215">Also note that the XmlDocument class allows entity resolution by default.</span></span> 

### <a name="example"></a><span data-ttu-id="a8e7f-216">範例</span><span class="sxs-lookup"><span data-stu-id="a8e7f-216">Example</span></span>
<span data-ttu-id="a8e7f-217">若要停用 XmlDocuments 的實體解析，請使用 Load 方法的 `XmlDocument.Load(XmlReader)` 多載，並在 XmlReader 引數中設定適當屬性以停用解析，如下列程式碼所示︰</span><span class="sxs-lookup"><span data-stu-id="a8e7f-217">To disable entity resolution for XmlDocuments, use the `XmlDocument.Load(XmlReader)` overload of the Load method and set the appropriate properties in the XmlReader argument to disable resolution, as illustrated in the following code:</span></span> 

```C#
XmlReaderSettings settings = new XmlReaderSettings();
settings.ProhibitDtd = true;
XmlReader reader = XmlReader.Create(stream, settings);
XmlDocument doc = new XmlDocument();
doc.Load(reader);
```

### <a name="example"></a><span data-ttu-id="a8e7f-218">範例</span><span class="sxs-lookup"><span data-stu-id="a8e7f-218">Example</span></span>
<span data-ttu-id="a8e7f-219">如果應用程式無法停用實體解析，請根據應用程式的需求將 XmlReaderSettings.MaxCharactersFromEntities 屬性設為合理的值。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-219">If disabling entity resolution is not possible for your application, set the XmlReaderSettings.MaxCharactersFromEntities property to a reasonable value according to your application's needs.</span></span> <span data-ttu-id="a8e7f-220">這會限制潛在指數擴張 DoS 攻擊所會造成的影響。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-220">This will limit the impact of potential exponential expansion DoS attacks.</span></span> <span data-ttu-id="a8e7f-221">下列程式碼提供此方法的範例︰</span><span class="sxs-lookup"><span data-stu-id="a8e7f-221">The following code provides an example of this approach:</span></span> 

```C#
XmlReaderSettings settings = new XmlReaderSettings();
settings.ProhibitDtd = false;
settings.MaxCharactersFromEntities = 1000;
XmlReader reader = XmlReader.Create(stream, settings);
```

### <a name="example"></a><span data-ttu-id="a8e7f-222">範例</span><span class="sxs-lookup"><span data-stu-id="a8e7f-222">Example</span></span>
<span data-ttu-id="a8e7f-223">如果您需要解析內嵌實體，但不需要解析外部實體，請將 XmlReaderSettings.XmlResolver 屬性設為 null。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-223">If you need to resolve inline entities but do not need to resolve external entities, set the XmlReaderSettings.XmlResolver property to null.</span></span> <span data-ttu-id="a8e7f-224">例如：</span><span class="sxs-lookup"><span data-stu-id="a8e7f-224">For example:</span></span> 

```C#
XmlReaderSettings settings = new XmlReaderSettings();
settings.ProhibitDtd = false;
settings.MaxCharactersFromEntities = 1000;
settings.XmlResolver = null;
XmlReader reader = XmlReader.Create(stream, settings);
```
<span data-ttu-id="a8e7f-225">請注意，在 MSXML6 中，ProhibitDTD 預設會設為 true (停用 DTD 處理)。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-225">Note that in MSXML6, ProhibitDTD is set to true (disabling DTD processing) by default.</span></span> <span data-ttu-id="a8e7f-226">針對 Apple OSX/iOS 程式碼，您可以使用的 XML 剖析器有兩個︰NSXMLParser 和 libXML2。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-226">For Apple OSX/iOS code, there are two XML parsers you can use: NSXMLParser and libXML2.</span></span> 

## <span data-ttu-id="a8e7f-227"><a id="app-verification"></a>利用 http.sys 的應用程式會執行 URL 標準化驗證</span><span class="sxs-lookup"><span data-stu-id="a8e7f-227"><a id="app-verification"></a>Applications utilizing http.sys perform URL canonicalization verification</span></span>

| <span data-ttu-id="a8e7f-228">Title</span><span class="sxs-lookup"><span data-stu-id="a8e7f-228">Title</span></span>                   | <span data-ttu-id="a8e7f-229">詳細資料</span><span class="sxs-lookup"><span data-stu-id="a8e7f-229">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="a8e7f-230">**元件**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-230">**Component**</span></span>               | <span data-ttu-id="a8e7f-231">Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="a8e7f-231">Web Application</span></span> | 
| <span data-ttu-id="a8e7f-232">**SDL 階段**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-232">**SDL Phase**</span></span>               | <span data-ttu-id="a8e7f-233">建置</span><span class="sxs-lookup"><span data-stu-id="a8e7f-233">Build</span></span> |  
| <span data-ttu-id="a8e7f-234">**適用的技術**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-234">**Applicable Technologies**</span></span> | <span data-ttu-id="a8e7f-235">泛型</span><span class="sxs-lookup"><span data-stu-id="a8e7f-235">Generic</span></span> |
| <span data-ttu-id="a8e7f-236">**屬性**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-236">**Attributes**</span></span>              | <span data-ttu-id="a8e7f-237">N/A</span><span class="sxs-lookup"><span data-stu-id="a8e7f-237">N/A</span></span>  |
| <span data-ttu-id="a8e7f-238">**參考**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-238">**References**</span></span>              | <span data-ttu-id="a8e7f-239">N/A</span><span class="sxs-lookup"><span data-stu-id="a8e7f-239">N/A</span></span>  |
| <span data-ttu-id="a8e7f-240">**步驟**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-240">**Steps**</span></span> | <p><span data-ttu-id="a8e7f-241">任何使用 http.sys 的應用程式皆應遵循下列指導方針︰</span><span class="sxs-lookup"><span data-stu-id="a8e7f-241">Any application that uses http.sys should follow these guidelines:</span></span></p><ul><li><span data-ttu-id="a8e7f-242">將 URL 長度限制在不超過 16,384 個字元 (ASCII 或 Unicode)。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-242">Limit the URL length to no more than 16,384 characters (ASCII or Unicode).</span></span> <span data-ttu-id="a8e7f-243">這是以預設 Internet Information Services (IIS) 6 設定為基礎的 URL 長度絕對上限。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-243">This is the absolute maximum URL length based on the default Internet Information Services (IIS) 6 setting.</span></span> <span data-ttu-id="a8e7f-244">網站長度應盡可能不超過此上限</span><span class="sxs-lookup"><span data-stu-id="a8e7f-244">Websites should strive for a length shorter than this if possible</span></span></li><li><span data-ttu-id="a8e7f-245">使用標準的 .NET Framework 檔案 I/O 類別 (例如 FileStream)，因為這些類別會利用 .NET FX 中的標準化規則</span><span class="sxs-lookup"><span data-stu-id="a8e7f-245">Use the standard .NET Framework file I/O classes (such as FileStream) as these will take advantage of the canonicalization rules in the .NET FX</span></span></li><li><span data-ttu-id="a8e7f-246">明確建置已知檔案名稱的允許清單</span><span class="sxs-lookup"><span data-stu-id="a8e7f-246">Explicitly build an allow-list of known filenames</span></span></li><li><span data-ttu-id="a8e7f-247">明確拒絕不會提供 UrlScan 拒絕的已知檔案類型︰exe、bat、cmd、com、htw、ida、idq、htr、idc、shtm[l]、stm、printer、ini、pol、dat 檔案</span><span class="sxs-lookup"><span data-stu-id="a8e7f-247">Explicitly reject known filetypes you will not serve UrlScan rejects: exe, bat, cmd, com, htw, ida, idq, htr, idc, shtm[l], stm, printer, ini, pol, dat files</span></span></li><li><span data-ttu-id="a8e7f-248">捕捉下列例外狀況：</span><span class="sxs-lookup"><span data-stu-id="a8e7f-248">Catch the following exceptions:</span></span><ul><li><span data-ttu-id="a8e7f-249">System.ArgumentException (針對裝置名稱)</span><span class="sxs-lookup"><span data-stu-id="a8e7f-249">System.ArgumentException (for device names)</span></span></li><li><span data-ttu-id="a8e7f-250">System.NotSupportedException (針對資料串流)</span><span class="sxs-lookup"><span data-stu-id="a8e7f-250">System.NotSupportedException (for data streams)</span></span></li><li><span data-ttu-id="a8e7f-251">System.IO.FileNotFoundException (針對無效的逸出檔名)</span><span class="sxs-lookup"><span data-stu-id="a8e7f-251">System.IO.FileNotFoundException (for invalid escaped filenames)</span></span></li><li><span data-ttu-id="a8e7f-252">System.IO.DirectoryNotFoundException (針對無效的逸出目錄)</span><span class="sxs-lookup"><span data-stu-id="a8e7f-252">System.IO.DirectoryNotFoundException (for invalid escaped dirs)</span></span></li></ul></li><li><span data-ttu-id="a8e7f-253">「請勿」對外呼叫 Win32 檔案 I/O API。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-253">*Do not* call out to Win32 file I/O APIs.</span></span> <span data-ttu-id="a8e7f-254">針對無效的 URL，正常傳回 400 錯誤給使用者，並記錄實際錯誤。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-254">On an invalid URL gracefully return a 400 error to the user, and log the real error.</span></span></li></ul>|

## <span data-ttu-id="a8e7f-255"><a id="controls-users"></a>確定在接受使用者的檔案時已備妥適當的控制</span><span class="sxs-lookup"><span data-stu-id="a8e7f-255"><a id="controls-users"></a>Ensure appropriate controls are in place when accepting files from users</span></span>

| <span data-ttu-id="a8e7f-256">Title</span><span class="sxs-lookup"><span data-stu-id="a8e7f-256">Title</span></span>                   | <span data-ttu-id="a8e7f-257">詳細資料</span><span class="sxs-lookup"><span data-stu-id="a8e7f-257">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="a8e7f-258">**元件**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-258">**Component**</span></span>               | <span data-ttu-id="a8e7f-259">Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="a8e7f-259">Web Application</span></span> | 
| <span data-ttu-id="a8e7f-260">**SDL 階段**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-260">**SDL Phase**</span></span>               | <span data-ttu-id="a8e7f-261">建置</span><span class="sxs-lookup"><span data-stu-id="a8e7f-261">Build</span></span> |  
| <span data-ttu-id="a8e7f-262">**適用的技術**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-262">**Applicable Technologies**</span></span> | <span data-ttu-id="a8e7f-263">泛型</span><span class="sxs-lookup"><span data-stu-id="a8e7f-263">Generic</span></span> |
| <span data-ttu-id="a8e7f-264">**屬性**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-264">**Attributes**</span></span>              | <span data-ttu-id="a8e7f-265">N/A</span><span class="sxs-lookup"><span data-stu-id="a8e7f-265">N/A</span></span>  |
| <span data-ttu-id="a8e7f-266">**參考**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-266">**References**</span></span>              | <span data-ttu-id="a8e7f-267">[不受限制的檔案上傳](https://www.owasp.org/index.php/Unrestricted_File_Upload)、[檔案簽章資料表](http://www.garykessler.net/library/file_sigs.html)</span><span class="sxs-lookup"><span data-stu-id="a8e7f-267">[Unrestricted File Upload](https://www.owasp.org/index.php/Unrestricted_File_Upload), [File Signature Table](http://www.garykessler.net/library/file_sigs.html)</span></span> |
| <span data-ttu-id="a8e7f-268">**步驟**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-268">**Steps**</span></span> | <p><span data-ttu-id="a8e7f-269">對應用程式來說，上傳的檔案就代表著重大風險。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-269">Uploaded files represent a significant risk to applications.</span></span></p><p><span data-ttu-id="a8e7f-270">許多攻擊的第一步就是將一些程式碼放到所要攻擊的系統。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-270">The first step in many attacks is to get some code to the system to be attacked.</span></span> <span data-ttu-id="a8e7f-271">然後，攻擊行動只需要找到方法來執行程式碼即可。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-271">Then the attack only needs to find a way to get the code executed.</span></span> <span data-ttu-id="a8e7f-272">使用檔案上傳可幫助攻擊者完成第一步。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-272">Using a file upload helps the attacker accomplish the first step.</span></span> <span data-ttu-id="a8e7f-273">檔案上傳不受限制的後果各不相同，可能是系統遭到完整接管、檔案系統或資料庫超載、將攻擊行動轉送到後端系統，或者就只是損毀這麼簡單。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-273">The consequences of unrestricted file upload can vary, including complete system takeover, an overloaded file system or database, forwarding attacks to back-end systems, and simple defacement.</span></span></p><p><span data-ttu-id="a8e7f-274">一切取決於應用程式會怎麼處理上傳的檔案，尤其是會儲存在哪裡。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-274">It depends on what the application does with the uploaded file and especially where it is stored.</span></span> <span data-ttu-id="a8e7f-275">伺服器端缺少驗證上傳檔案的動作。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-275">Server side validation of file uploads is missing.</span></span> <span data-ttu-id="a8e7f-276">請針對檔案上傳功能實作下列安全性控制︰</span><span class="sxs-lookup"><span data-stu-id="a8e7f-276">Following security controls should be implemented for File Upload functionality:</span></span></p><ul><li><span data-ttu-id="a8e7f-277">副檔名檢查 (只應接受一組有效的允許檔案類型)</span><span class="sxs-lookup"><span data-stu-id="a8e7f-277">File Extension check (only a valid set of allowed file type should be accepted)</span></span></li><li><span data-ttu-id="a8e7f-278">檔案大小上限</span><span class="sxs-lookup"><span data-stu-id="a8e7f-278">Maximum file size limit</span></span></li><li><span data-ttu-id="a8e7f-279">檔案不應上傳至 Web 根目錄；上傳位置應該是非系統磁碟機上的目錄</span><span class="sxs-lookup"><span data-stu-id="a8e7f-279">File should not be uploaded to webroot; the location should be a directory on non-system drive</span></span></li><li><span data-ttu-id="a8e7f-280">應遵循命名慣例，讓上傳的檔案以隨機方式命名，以避免覆寫檔案</span><span class="sxs-lookup"><span data-stu-id="a8e7f-280">Naming convention should be followed, such that the uploaded file name have some randomness, so as to prevent file overwrites</span></span></li><li><span data-ttu-id="a8e7f-281">應先對檔案進行防毒掃描再將其寫入磁碟</span><span class="sxs-lookup"><span data-stu-id="a8e7f-281">Files should be scanned for anti-virus before writing to the disk</span></span></li><li><span data-ttu-id="a8e7f-282">確保會驗證檔案名稱和其他任何中繼資料 (例如，檔案路徑) 中是否有惡意字元</span><span class="sxs-lookup"><span data-stu-id="a8e7f-282">Ensure that the file name and any other metadata (e.g., file path) are validated for malicious characters</span></span></li><li><span data-ttu-id="a8e7f-283">應檢查檔案格式簽章，以防止使用者上傳偽裝的檔案 (例如，將副檔名改為 txt 以上傳 exe 檔案)</span><span class="sxs-lookup"><span data-stu-id="a8e7f-283">File format signature should be checked, to prevent a user from uploading a masqueraded file (e.g., uploading an exe file by changing extension to txt)</span></span></li></ul>| 

### <a name="example"></a><span data-ttu-id="a8e7f-284">範例</span><span class="sxs-lookup"><span data-stu-id="a8e7f-284">Example</span></span>
<span data-ttu-id="a8e7f-285">如需上述最後一點關於檔案格式簽章驗證的資訊，請參閱下面的類別以了解詳情︰</span><span class="sxs-lookup"><span data-stu-id="a8e7f-285">For the last point regarding file format signature validation, refer to the class below for details:</span></span> 

```C#
        private static Dictionary<string, List<byte[]>> fileSignature = new Dictionary<string, List<byte[]>>
                    {
                    { ".DOC", new List<byte[]> { new byte[] { 0xD0, 0xCF, 0x11, 0xE0, 0xA1, 0xB1, 0x1A, 0xE1 } } },
                    { ".DOCX", new List<byte[]> { new byte[] { 0x50, 0x4B, 0x03, 0x04 } } },
                    { ".PDF", new List<byte[]> { new byte[] { 0x25, 0x50, 0x44, 0x46 } } },
                    { ".ZIP", new List<byte[]> 
                                            {
                                              new byte[] { 0x50, 0x4B, 0x03, 0x04 },
                                              new byte[] { 0x50, 0x4B, 0x4C, 0x49, 0x54, 0x55 },
                                              new byte[] { 0x50, 0x4B, 0x53, 0x70, 0x58 },
                                              new byte[] { 0x50, 0x4B, 0x05, 0x06 },
                                              new byte[] { 0x50, 0x4B, 0x07, 0x08 },
                                              new byte[] { 0x57, 0x69, 0x6E, 0x5A, 0x69, 0x70 }
                                                }
                                            },
                    { ".PNG", new List<byte[]> { new byte[] { 0x89, 0x50, 0x4E, 0x47, 0x0D, 0x0A, 0x1A, 0x0A } } },
                    { ".JPG", new List<byte[]>
                                    {
                                              new byte[] { 0xFF, 0xD8, 0xFF, 0xE0 },
                                              new byte[] { 0xFF, 0xD8, 0xFF, 0xE1 },
                                              new byte[] { 0xFF, 0xD8, 0xFF, 0xE8 }
                                    }
                                    },
                    { ".JPEG", new List<byte[]>
                                        { 
                                            new byte[] { 0xFF, 0xD8, 0xFF, 0xE0 },
                                            new byte[] { 0xFF, 0xD8, 0xFF, 0xE2 },
                                            new byte[] { 0xFF, 0xD8, 0xFF, 0xE3 }
                                        }
                                        },
                    { ".XLS", new List<byte[]>
                                            {
                                              new byte[] { 0xD0, 0xCF, 0x11, 0xE0, 0xA1, 0xB1, 0x1A, 0xE1 },
                                              new byte[] { 0x09, 0x08, 0x10, 0x00, 0x00, 0x06, 0x05, 0x00 },
                                              new byte[] { 0xFD, 0xFF, 0xFF, 0xFF }
                                            }
                                            },
                    { ".XLSX", new List<byte[]> { new byte[] { 0x50, 0x4B, 0x03, 0x04 } } },
                    { ".GIF", new List<byte[]> { new byte[] { 0x47, 0x49, 0x46, 0x38 } } }
                };

        public static bool IsValidFileExtension(string fileName, byte[] fileData, byte[] allowedChars)
        {
            if (string.IsNullOrEmpty(fileName) || fileData == null || fileData.Length == 0)
            {
                return false;
            }

            bool flag = false;
            string ext = Path.GetExtension(fileName);
            if (string.IsNullOrEmpty(ext))
            {
                return false;
            }

            ext = ext.ToUpperInvariant();

            if (ext.Equals(".TXT") || ext.Equals(".CSV") || ext.Equals(".PRN"))
            {
                foreach (byte b in fileData)
                {
                    if (b > 0x7F)
                    {
                        if (allowedChars != null)
                        {
                            if (!allowedChars.Contains(b))
                            {
                                return false;
                            }
                        }
                        else
                        {
                            return false;
                        }
                    }
                }

                return true;
            }

            if (!fileSignature.ContainsKey(ext))
            {
                return true;
            }

            List<byte[]> sig = fileSignature[ext];
            foreach (byte[] b in sig)
            {
                var curFileSig = new byte[b.Length];
                Array.Copy(fileData, curFileSig, b.Length);
                if (curFileSig.SequenceEqual(b))
                {
                    flag = true;
                    break;
                }
            }

            return flag;
        }
```

## <span data-ttu-id="a8e7f-286"><a id="typesafe"></a>確定 Web 應用程式有使用 type-safe 參數來存取資料</span><span class="sxs-lookup"><span data-stu-id="a8e7f-286"><a id="typesafe"></a>Ensure that type-safe parameters are used in Web Application for data access</span></span>

| <span data-ttu-id="a8e7f-287">Title</span><span class="sxs-lookup"><span data-stu-id="a8e7f-287">Title</span></span>                   | <span data-ttu-id="a8e7f-288">詳細資料</span><span class="sxs-lookup"><span data-stu-id="a8e7f-288">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="a8e7f-289">**元件**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-289">**Component**</span></span>               | <span data-ttu-id="a8e7f-290">Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="a8e7f-290">Web Application</span></span> | 
| <span data-ttu-id="a8e7f-291">**SDL 階段**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-291">**SDL Phase**</span></span>               | <span data-ttu-id="a8e7f-292">建置</span><span class="sxs-lookup"><span data-stu-id="a8e7f-292">Build</span></span> |  
| <span data-ttu-id="a8e7f-293">**適用的技術**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-293">**Applicable Technologies**</span></span> | <span data-ttu-id="a8e7f-294">泛型</span><span class="sxs-lookup"><span data-stu-id="a8e7f-294">Generic</span></span> |
| <span data-ttu-id="a8e7f-295">**屬性**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-295">**Attributes**</span></span>              | <span data-ttu-id="a8e7f-296">N/A</span><span class="sxs-lookup"><span data-stu-id="a8e7f-296">N/A</span></span>  |
| <span data-ttu-id="a8e7f-297">**參考**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-297">**References**</span></span>              | <span data-ttu-id="a8e7f-298">N/A</span><span class="sxs-lookup"><span data-stu-id="a8e7f-298">N/A</span></span>  |
| <span data-ttu-id="a8e7f-299">**步驟**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-299">**Steps**</span></span> | <p><span data-ttu-id="a8e7f-300">如果您使用參數集合，SQL 會將輸入視為常值而非可執行程式碼。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-300">If you use the Parameters collection, SQL treats the input is as a literal value rather then as executable code.</span></span> <span data-ttu-id="a8e7f-301">參數集合可用來對輸入資料強制執行類型和長度條件約束。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-301">The Parameters collection can be used to enforce type and length constraints on input data.</span></span> <span data-ttu-id="a8e7f-302">超出範圍的值會觸發例外狀況。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-302">Values outside of the range trigger an exception.</span></span> <span data-ttu-id="a8e7f-303">如果未使用 type-safe SQL 參數，攻擊者或許就能執行內嵌於未經篩選之輸入中的插入式攻擊。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-303">If type-safe SQL parameters are not used, attackers might be able to execute injection attacks that are embedded in the unfiltered input.</span></span></p><p><span data-ttu-id="a8e7f-304">請在建構 SQL 查詢時使用 type-safe 參數，以避免未經篩選的輸入中可能發生的 SQL 插入式攻擊。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-304">Use type safe parameters when constructing SQL queries to avoid possible SQL injection attacks that can occur with unfiltered input.</span></span> <span data-ttu-id="a8e7f-305">type-safe 參數可與預存程序和動態 SQL 陳述式搭配使用。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-305">You can use type safe parameters with stored procedures and with dynamic SQL statements.</span></span> <span data-ttu-id="a8e7f-306">資料庫會將參數視為常值而非可執行程式碼。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-306">Parameters are treated as literal values by the database and not as executable code.</span></span> <span data-ttu-id="a8e7f-307">參數的類型和長度也會受到檢查。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-307">Parameters are also checked for type and length.</span></span></p>|

### <a name="example"></a><span data-ttu-id="a8e7f-308">範例</span><span class="sxs-lookup"><span data-stu-id="a8e7f-308">Example</span></span> 
<span data-ttu-id="a8e7f-309">下列程式碼示範如何在呼叫預存程序時，搭配使用 type-safe 參數與 SqlParameterCollection。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-309">The following code shows how to use type safe parameters with the SqlParameterCollection when calling a stored procedure.</span></span> 

```C#
using System.Data;
using System.Data.SqlClient;

using (SqlConnection connection = new SqlConnection(connectionString))
{ 
DataSet userDataset = new DataSet(); 
SqlDataAdapter myCommand = new SqlDataAdapter(LoginStoredProcedure", connection); 
myCommand.SelectCommand.CommandType = CommandType.StoredProcedure; 
myCommand.SelectCommand.Parameters.Add("@au_id", SqlDbType.VarChar, 11); 
myCommand.SelectCommand.Parameters["@au_id"].Value = SSN.Text; 
myCommand.Fill(userDataset);
}  
```
<span data-ttu-id="a8e7f-310">在上述程式碼範例中，輸入值不能超過 11 個字元。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-310">In the preceding code example, the input value cannot be longer than 11 characters.</span></span> <span data-ttu-id="a8e7f-311">如果資料不符合參數所定義的類型或長度，SqlParameter 類別就會擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-311">If the data does not conform to the type or length defined by the parameter, the SqlParameter class throws an exception.</span></span> 

## <span data-ttu-id="a8e7f-312"><a id="binding-mvc"></a>使用個別的模型繫結類別或繫結篩選清單來防止 MVC 大量指派弱點</span><span class="sxs-lookup"><span data-stu-id="a8e7f-312"><a id="binding-mvc"></a>Use separate model binding classes or binding filter lists to prevent MVC mass assignment vulnerability</span></span>

| <span data-ttu-id="a8e7f-313">Title</span><span class="sxs-lookup"><span data-stu-id="a8e7f-313">Title</span></span>                   | <span data-ttu-id="a8e7f-314">詳細資料</span><span class="sxs-lookup"><span data-stu-id="a8e7f-314">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="a8e7f-315">**元件**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-315">**Component**</span></span>               | <span data-ttu-id="a8e7f-316">Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="a8e7f-316">Web Application</span></span> | 
| <span data-ttu-id="a8e7f-317">**SDL 階段**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-317">**SDL Phase**</span></span>               | <span data-ttu-id="a8e7f-318">建置</span><span class="sxs-lookup"><span data-stu-id="a8e7f-318">Build</span></span> |  
| <span data-ttu-id="a8e7f-319">**適用的技術**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-319">**Applicable Technologies**</span></span> | <span data-ttu-id="a8e7f-320">MVC5、MVC6</span><span class="sxs-lookup"><span data-stu-id="a8e7f-320">MVC5, MVC6</span></span> |
| <span data-ttu-id="a8e7f-321">**屬性**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-321">**Attributes**</span></span>              | <span data-ttu-id="a8e7f-322">N/A</span><span class="sxs-lookup"><span data-stu-id="a8e7f-322">N/A</span></span>  |
| <span data-ttu-id="a8e7f-323">**參考**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-323">**References**</span></span>              | <span data-ttu-id="a8e7f-324">[中繼資料屬性](http://msdn.microsoft.com/library/system.componentmodel.dataannotations.metadatatypeattribute)、[公用金鑰安全性弱點和風險降低](https://github.com/blog/1068-public-key-security-vulnerability-and-mitigation)、[在 ASP.NET MVC 中大量指派的完整指南](http://odetocode.com/Blogs/scott/archive/2012/03/11/complete-guide-to-mass-assignment-in-asp-net-mvc.aspx)、[使用 MVC 開始使用 EF](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application#overpost)</span><span class="sxs-lookup"><span data-stu-id="a8e7f-324">[Metadata Attributes](http://msdn.microsoft.com/library/system.componentmodel.dataannotations.metadatatypeattribute), [Public Key Security Vulnerability And Mitigation](https://github.com/blog/1068-public-key-security-vulnerability-and-mitigation), [Complete Guide to Mass Assignment in ASP.NET MVC](http://odetocode.com/Blogs/scott/archive/2012/03/11/complete-guide-to-mass-assignment-in-asp-net-mvc.aspx), [Getting Started with EF using MVC](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application#overpost)</span></span> |
| <span data-ttu-id="a8e7f-325">**步驟**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-325">**Steps**</span></span> | <ul><li><span data-ttu-id="a8e7f-326">**我應該在何時尋找 over-posting 弱點？-** over-posting 弱點可能發生在您從使用者輸入繫結模型類別的任何位置。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-326">**When should I look for over-posting vulnerabilities? -** Over-posting vulnerabilities can occur any place you bind model classes from user input.</span></span> <span data-ttu-id="a8e7f-327">MVC 等架構可在自訂 .NET 類別中代表使用者資料，包括純舊 CLR 物件 (POCO)。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-327">Frameworks like MVC can represent user data in custom .NET classes, including Plain Old CLR Objects (POCOs).</span></span> <span data-ttu-id="a8e7f-328">MVC 會自動在這些模型類別中填入要求中的資料，以方便代表要處理的使用者輸入。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-328">MVC automatically populates these model classes with data from the request, providing a convenient representation for dealing with user input.</span></span> <span data-ttu-id="a8e7f-329">當這些類別包括不應該由使用者設定的屬性時，應用程式很容易遭受 over-posting 攻擊，因而允許使用者控制應用程式永遠不會需要的資料。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-329">When these classes include properties that should not be set by the user, the application can be vulnerable to over-posting attacks, which allow user control of data that the application never intended.</span></span> <span data-ttu-id="a8e7f-330">和 MVC 模型繫結一樣，Entity Framework 等物件/關聯式對應程式之類的資料庫存取技術，通常也支援使用 POCO 物件來代表資料庫資料。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-330">Like MVC model binding, database access technologies such as object/relational mappers like Entity Framework often also support using POCO objects to represent database data.</span></span> <span data-ttu-id="a8e7f-331">這些資料模型類別同樣能代表要處理的資料庫資料，就和 MVC 在處理使用者輸入時一樣。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-331">These data model classes provide the same convenience in dealing with database data as MVC does in dealing with user input.</span></span> <span data-ttu-id="a8e7f-332">因為 MVC 和資料庫都支援類似模型，例如 POCO 物件，想要將相同的類別重複用於這兩種用途似乎是輕鬆無比的事。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-332">Because both MVC and the database support similar models, like POCO objects, it seems easy to reuse the same classes for both purposes.</span></span> <span data-ttu-id="a8e7f-333">這種作法無法保持關注點分離，而這一塊區域通常也會讓模型繫結能夠接觸到非預期屬性，而實現 over-posting 攻擊。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-333">This practice fails to preserve separation of concerns, and it is one common area where unintended properties are exposed to model binding, enabling over-posting attacks.</span></span></li><li><span data-ttu-id="a8e7f-334">**為何不該使用未經篩選的資料庫模型類別來做為 MVC 動作的參數？-** 因為 MVC 模型繫結會在該類別繫結任何項目。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-334">**Why shouldn't I use my unfiltered database model classes as parameters to my MVC actions? -** Because MVC model binding will bind anything in that class.</span></span> <span data-ttu-id="a8e7f-335">即使資料未出現在檢視中，惡意使用者也可以傳送內含此資料的 HTTP 要求，MVC 會很樂意繫結它，因為您的動作說明資料庫類別是它應該接受做為使用者輸入的資料外觀。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-335">Even if the data does not appear in your view, a malicious user can send an HTTP request with this data included, and MVC will gladly bind it because your action says that database class is the shape of data it should accept for user input.</span></span></li><li><span data-ttu-id="a8e7f-336">**為何我該關心用於模型繫結的外觀？-** 搭配過度廣泛的模型使用 ASP.NET MVC 模型繫結，會讓應用程式暴露在 over-posting 攻擊範圍內。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-336">**Why should I care about the shape used for model binding? -** Using ASP.NET MVC model binding with overly broad models exposes an application to over-posting attacks.</span></span> <span data-ttu-id="a8e7f-337">over-posting 可讓攻擊者將應用程式資料的使用範圍變更為開發人員預定用途之外，例如覆寫某商品的價格或帳戶的安全性權限。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-337">Over-posting could enable attackers to change application data beyond what the developer intended, such as overriding the price for an item or the security privileges for an account.</span></span> <span data-ttu-id="a8e7f-338">應用程式應使用動作專屬的繫結模型 (或特別允許的屬性篩選清單) 來提供明確合約，規定要透過模型繫結允許哪些不受信任的輸入。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-338">Applications should use action-specific binding models (or specific allowed property filter lists) to provide an explicit contract for what untrusted input to allow via model binding.</span></span></li><li><span data-ttu-id="a8e7f-339">**要擁有個別的繫結模型是否只要複製程式碼即可？-** 否，此作業和關注點分離有關。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-339">**Is having separate binding models just duplicating code? -** No, it is a matter of separation of concerns.</span></span> <span data-ttu-id="a8e7f-340">若您在動作方法中重複使用資料庫模型，就表示該類別中的屬性 (或子屬性) 可供使用者在 HTTP 要求中設定。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-340">If you reuse database models in action methods, you are saying any property (or sub-property) in that class can be set by the user in an HTTP request.</span></span> <span data-ttu-id="a8e7f-341">如果您不想讓 MVC 這麼做，就需要使用篩選清單或個別的類別外觀來告訴 MVC 哪些資料可以來自使用者輸入。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-341">If that is not what you want MVC to do, you need a filter list or a separate class shape to show MVC what data can come from user input instead.</span></span></li><li><span data-ttu-id="a8e7f-342">**如果我有專門用於使用者輸入的繫結模型，我是否必須複製我所有的資料註解屬性？-** 不一定。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-342">**If I have separate binding models for user input, do I have to duplicate all my data annotation attributes? -** Not necessarily.</span></span> <span data-ttu-id="a8e7f-343">您可以在資料庫模型類別上使用 MetadataTypeAttribute 來連結至模型繫結類別上的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-343">You can use MetadataTypeAttribute on the database model class to link to the metadata on a model binding class.</span></span> <span data-ttu-id="a8e7f-344">但請注意，MetadataTypeAttribute 所參考的類型必須是參考類型的子集 (可以有較少屬性，但不得超過)。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-344">Just note that the type referenced by the MetadataTypeAttribute must be a subset of the referencing type (it can have fewer properties, but not more).</span></span></li><li><span data-ttu-id="a8e7f-345">**在使用者輸入模型和資料庫模型之間來回移動資料很麻煩。是否可以使用反映功能直接複製所有屬性？-** 是。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-345">**Moving data back and forth between user input models and database models is tedious. Can I just copy over all properties using reflection? -** Yes.</span></span> <span data-ttu-id="a8e7f-346">繫結模型中唯一會出現的屬性，是您已確定可安全做為使用者輸入的屬性。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-346">The only properties that appear in the binding models are the ones you have determined to be safe for user input.</span></span> <span data-ttu-id="a8e7f-347">沒有任何安全性方面的理由可阻止您使用反映功能來複製這兩個模型之間共同存在的所有屬性。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-347">There is no security reason that prevents using reflection to copy over all properties that exist in common between these two models.</span></span></li><li><span data-ttu-id="a8e7f-348">**您認為 [Bind(Exclude ="â€¦")] 如何。我能否使用此方法而不使用個別的繫結模型？-** 不建議使用這個方法。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-348">**What about [Bind(Exclude ="â€¦")]. Can I use that instead of having separate binding models? -** This approach is not recommended.</span></span> <span data-ttu-id="a8e7f-349">使用 [Bind(Exclude ="â€¦")] 表示任何新的屬性預設都是可繫結的。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-349">Using [Bind(Exclude ="â€¦")] means that any new property is bindable by default.</span></span> <span data-ttu-id="a8e7f-350">當您新增屬性時，有一個必須記得才能讓一切保持安全的額外步驟，而非讓設計預設就保持安全。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-350">When a new property is added, there is an extra step to remember to keep things secure, rather than having the design be secure by default.</span></span> <span data-ttu-id="a8e7f-351">依靠開發人員在每次新增屬性時檢查這份清單是件危險的事。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-351">Depending on the developer checking this list every time a property is added is risky.</span></span></li><li><span data-ttu-id="a8e7f-352">**[Bind(Include ="â€¦")] 適用於編輯作業嗎？-** 否。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-352">**Is [Bind(Include ="â€¦")] useful for Edit operations? -** No.</span></span> <span data-ttu-id="a8e7f-353">[Bind(Include ="â€¦")] 僅適用於插入樣式的作業 (新增資料)。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-353">[Bind(Include ="â€¦")] is only suitable for INSERT-style operations (adding new data).</span></span> <span data-ttu-id="a8e7f-354">若為更新樣式的作業 (修改現有資料)，請使用另一種方法，例如擁有個別的繫結模型，或將允許屬性的明確清單傳遞給 UpdateModel 或 TryUpdateModel。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-354">For UPDATE-style operations (revising existing data), use another approach, like having separate binding models or passing an explicit list of allowed properties to UpdateModel or TryUpdateModel.</span></span> <span data-ttu-id="a8e7f-355">在編輯作業上新增 [Bind(Include ="â€¦")] 屬性表示 MVC 會建立物件執行個體，並只設定列出的屬性，而讓其他所有屬性保持預設值。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-355">Adding a [Bind(Include ="â€¦")] attribute on an Edit operation means that MVC will create an object instance and set only the listed properties, leaving all others at their default values.</span></span> <span data-ttu-id="a8e7f-356">當資料存留下來時，便會完全取代現有實體，將任何遭忽略屬性的值重設為預設值。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-356">When the data is persisted, it will entirely replace the existing entity, resetting the values for any omitted properties to their defaults.</span></span> <span data-ttu-id="a8e7f-357">例如，若編輯作業上的 [Bind(Include ="â€¦")] 屬性中忽略 IsAdmin，透過這個動作編輯名稱的任何使用者都會重設為 IsAdmin = false (經過編輯的使用者會失去系統管理員狀態)。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-357">For example, if IsAdmin was omitted from a [Bind(Include ="â€¦")] attribute on an Edit operation, any user whose name was edited via this action would be reset to IsAdmin = false (any edited user would lose administrator status).</span></span> <span data-ttu-id="a8e7f-358">如果您想要防止更新某些屬性，請使用上述其他方法的其中一個。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-358">If you want to prevent updates to certain properties, use one of the other approaches above.</span></span> <span data-ttu-id="a8e7f-359">請注意，某些版本的 MVC 工具會對編輯作業上的 [Bind(Include ="â€¦")] 產生控制器類別，並表示從該清單中移除屬性會防止 over-posting 攻擊。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-359">Note that some versions of MVC tooling generate controller classes with [Bind(Include ="â€¦")] on Edit actions and imply that removing a property from that list will prevent over-posting attacks.</span></span> <span data-ttu-id="a8e7f-360">但如上所述，該方法不會如預期運作，反而會將所忽略屬性中的任何資料重設為預設值。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-360">However, as described above, that approach does not work as intended and instead will reset any data in the omitted properties to their default values.</span></span></li><li><span data-ttu-id="a8e7f-361">**針對建立作業使用 [Bind(Include ="â€¦")] 而非使用個別繫結模型，是否有需要注意的事項？-** 是。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-361">**For Create operations, are there any caveats using [Bind(Include ="â€¦")] rather than separate binding models? -** Yes.</span></span> <span data-ttu-id="a8e7f-362">首先，這個方法不適用於編輯案例，需要維護兩種不同方法來降低所有 over-posting 弱點。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-362">First this approach does not work for Edit scenarios, requiring maintaining two separate approaches for mitigating all over-posting vulnerabilities.</span></span> <span data-ttu-id="a8e7f-363">其次，不同的繫結模型會在用於使用者輸入的外觀和用於持續性的外觀之間強制執行關注點分離，[Bind(Include ="â€¦")] 則不會這麼做。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-363">Second, separate binding models enforce separation of concerns between the shape used for user input and the shape used for persistence, something [Bind(Include ="â€¦")] does not do.</span></span> <span data-ttu-id="a8e7f-364">第三，請注意 [Bind(Include ="â€¦")] 只能處理最上層屬性；您不能在屬性中只允許部分子屬性 (例如 "Details.Name")。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-364">Third, note that [Bind(Include ="â€¦")] can only handle top-level properties; you cannot allow only portions of sub-properties (such as "Details.Name") in the attribute.</span></span> <span data-ttu-id="a8e7f-365">最後，或許也是最重要的，使用 [Bind(Include ="â€¦")] 會在類別用於模型繫結的時候新增必須記得的額外步驟。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-365">Finally, and perhaps most importantly, using [Bind(Include ="â€¦")] adds an extra step that must be remembered any time the class is used for model binding.</span></span> <span data-ttu-id="a8e7f-366">如果新的動作方法直接繫結至資料類別，而忘記包含 [Bind(Include ="â€¦")] 屬性，則會很容易遭受 over-posting 攻擊，因此 [Bind(Include ="â€¦")] 方法依預設會較不安全。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-366">If a new action method binds to the data class directly and forgets to include a [Bind(Include ="â€¦")] attribute, it can be vulnerable to over-posting attacks, so the [Bind(Include ="â€¦")] approach is somewhat less secure by default.</span></span> <span data-ttu-id="a8e7f-367">如果您使用 [Bind(Include ="â€¦")]，請注意一律要記得在每次資料類別做為動作方法參數時指定它。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-367">If you use [Bind(Include ="â€¦")], take care always to remember to specify it every time your data classes appear as action method parameters.</span></span></li><li><span data-ttu-id="a8e7f-368">**針對建立作業，若在模型類別本身放置 [Bind(Include ="â€¦")] 屬性，您認為如何？這種方法不能讓我不再需要記得在每個動作方法放置此屬性嗎？-** 這種方法在某些情況下有用。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-368">**For Create operations, what about putting the [Bind(Include ="â€¦")] attribute on the model class itself? Does not this approach avoid the need to remember putting the attribute on every action method? -** This approach works in some cases.</span></span> <span data-ttu-id="a8e7f-369">在模型類型本身 (而非在使用這個類別的動作參數上) 使用 [Bind(Include ="â€¦")]，確實不再需要記得於每個動作方法加上 [Bind(Include ="â€¦")] 屬性。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-369">Using [Bind(Include ="â€¦")] on the model type itself (rather than on action parameters using this class), does avoid the need to remember to include the [Bind(Include ="â€¦")] attribute on every action method.</span></span> <span data-ttu-id="a8e7f-370">直接在類別上使用此屬性實際上會為此類別建立不同的介面區域，以供繫結模型。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-370">Using the attribute directly on the class effectively creates a separate surface area of this class for model binding purposes.</span></span> <span data-ttu-id="a8e7f-371">不過，此方法只允許在每個模型類別上使用一個模型繫結外觀。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-371">However, this approach only allows for one model binding shape per model class.</span></span> <span data-ttu-id="a8e7f-372">如果某個動作方法需要允許某欄位進行模型繫結 (例如，會更新使用者角色的僅限系統管理員動作)，而其他動作需要防止此欄位進行模型繫結，這個方法就無法運作。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-372">If one action method needs to allow model binding of a field (for example, an administrator-only action that updates user roles) and other actions need to prevent model binding of this field, this approach will not work.</span></span> <span data-ttu-id="a8e7f-373">每個類別只能有一個模型繫結外觀；如果不同的動作需要不同的模型繫結外觀，則必須在動作方法上使用不同的模型繫結類別或不同的 [Bind(Include ="â€¦")] 屬性，來表示這些不同的外觀。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-373">Each class can only have one model binding shape; if different actions need different model binding shapes, they need to represent these separate shapes using either separate model binding classes or separate [Bind(Include ="â€¦")] attributes on the action methods.</span></span></li><li><span data-ttu-id="a8e7f-374">**何謂繫結模型？它們是和檢視模型相同的概念嗎？-** 這兩者是有相關性的概念。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-374">**What are binding models? Are they the same thing as view models? -** These are two related concepts.</span></span> <span data-ttu-id="a8e7f-375">繫結模型一詞是指動作中所使用的模型類別是參數清單 (從 MVC 模型繫結傳遞至動作方法的外觀)。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-375">The term binding model refers to a model class used in an action is parameter list (the shape passed from MVC model binding to the action method).</span></span> <span data-ttu-id="a8e7f-376">檢視模型一詞則是指從動作方法傳遞至檢視的模型類別。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-376">The term view model refers to a model class passed from an action method to a view.</span></span> <span data-ttu-id="a8e7f-377">要將資料從動作方法傳遞至檢視時，通常會使用檢視專屬模型這個方法。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-377">Using a view-specific model is a common approach for passing data from an action method to a view.</span></span> <span data-ttu-id="a8e7f-378">通常，此圖形也是適用於模型繫結，而且詞彙檢視模型可以用來參考兩個地方使用的相同模型。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-378">Often, this shape is also suitable for model binding, and the term view model can be used to refer the same model used in both places.</span></span> <span data-ttu-id="a8e7f-379">準確地說，此程序專門討論繫結模型，將重點放在傳遞給動作的外觀，而這對於大量指派來說很重要。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-379">To be precise, this procedure talks specifically about binding models, focusing on the shape passed to the action, which is what matters for mass assignment purposes.</span></span></li></ul>| 

## <span data-ttu-id="a8e7f-380"><a id="rendering"></a>先將未受信任的 Web 輸出編碼再進行轉譯</span><span class="sxs-lookup"><span data-stu-id="a8e7f-380"><a id="rendering"></a>Encode untrusted web output prior to rendering</span></span>

| <span data-ttu-id="a8e7f-381">Title</span><span class="sxs-lookup"><span data-stu-id="a8e7f-381">Title</span></span>                   | <span data-ttu-id="a8e7f-382">詳細資料</span><span class="sxs-lookup"><span data-stu-id="a8e7f-382">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="a8e7f-383">**元件**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-383">**Component**</span></span>               | <span data-ttu-id="a8e7f-384">Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="a8e7f-384">Web Application</span></span> | 
| <span data-ttu-id="a8e7f-385">**SDL 階段**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-385">**SDL Phase**</span></span>               | <span data-ttu-id="a8e7f-386">建置</span><span class="sxs-lookup"><span data-stu-id="a8e7f-386">Build</span></span> |  
| <span data-ttu-id="a8e7f-387">**適用的技術**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-387">**Applicable Technologies**</span></span> | <span data-ttu-id="a8e7f-388">泛型、Web Form、MVC5、MVC6</span><span class="sxs-lookup"><span data-stu-id="a8e7f-388">Generic, Web Forms, MVC5, MVC6</span></span> |
| <span data-ttu-id="a8e7f-389">**屬性**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-389">**Attributes**</span></span>              | <span data-ttu-id="a8e7f-390">N/A</span><span class="sxs-lookup"><span data-stu-id="a8e7f-390">N/A</span></span>  |
| <span data-ttu-id="a8e7f-391">**參考**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-391">**References**</span></span>              | <span data-ttu-id="a8e7f-392">[如何在 ASP.NET 中防止跨網站指令碼](http://msdn.microsoft.com/library/ms998274.aspx)、[跨網站指令碼](http://cwe.mitre.org/data/definitions/79.html)、[XSS (跨網站指令碼) 防護功能提要](https://www.owasp.org/index.php/XSS_(Cross_Site_Scripting)_Prevention_Cheat_Sheet)</span><span class="sxs-lookup"><span data-stu-id="a8e7f-392">[How to prevent Cross-site scripting in ASP.NET](http://msdn.microsoft.com/library/ms998274.aspx), [Cross-site Scripting](http://cwe.mitre.org/data/definitions/79.html), [XSS (Cross Site Scripting) Prevention Cheat Sheet](https://www.owasp.org/index.php/XSS_(Cross_Site_Scripting)_Prevention_Cheat_Sheet)</span></span> |
| <span data-ttu-id="a8e7f-393">**步驟**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-393">**Steps**</span></span> | <span data-ttu-id="a8e7f-394">跨網站指令碼 (通常縮寫為 XSS) 是針對線上服務或從 Web 取用輸入之任何應用程式/元件的攻擊媒介。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-394">Cross-site scripting (commonly abbreviated as XSS) is an attack vector for online services or any application/component that consumes input from the web.</span></span> <span data-ttu-id="a8e7f-395">XSS 弱點可能會讓攻擊者透過易受攻擊的 Web 應用程式，對其他使用者的電腦執行指令碼。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-395">XSS vulnerabilities may allow an attacker to execute script on another user's machine through a vulnerable web application.</span></span> <span data-ttu-id="a8e7f-396">惡意指令碼可用來竊取 Cookie 或是透過 JavaScript 竄改受害者的電腦。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-396">Malicious scripts can be used to steal cookies and otherwise tamper with a victim's machine through JavaScript.</span></span> <span data-ttu-id="a8e7f-397">若要預防 XSS，您可以驗證使用者輸入、確保其格式正確無誤並先加以編碼，再轉譯於網頁中。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-397">XSS is prevented by validating user input, ensuring it is well formed and encoding before it is rendered in a web page.</span></span> <span data-ttu-id="a8e7f-398">使用 Web Protection Library 即可進行輸入驗證和輸出編碼。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-398">Input validation and output encoding can be done by using Web Protection Library.</span></span> <span data-ttu-id="a8e7f-399">若為 Managed 程式碼 (C\#、VB.net 等)，請根據為使用者輸入建立資訊清單的內容，使用一個或多個來自 Web Protection (Anti-XSS) Library 的適當編碼方法︰</span><span class="sxs-lookup"><span data-stu-id="a8e7f-399">For Managed code (C\#, VB.net, etc.), use one or more appropriate encoding methods from the Web Protection (Anti-XSS) Library, depending on the context where the user input gets manifested:</span></span>| 

### <a name="example"></a><span data-ttu-id="a8e7f-400">範例</span><span class="sxs-lookup"><span data-stu-id="a8e7f-400">Example</span></span>

```C#
* Encoder.HtmlEncode 
* Encoder.HtmlAttributeEncode 
* Encoder.JavaScriptEncode 
* Encoder.UrlEncode
* Encoder.VisualBasicScriptEncode 
* Encoder.XmlEncode 
* Encoder.XmlAttributeEncode 
* Encoder.CssEncode 
* Encoder.LdapEncode 
```

## <span data-ttu-id="a8e7f-401"><a id="typemodel"></a>對所有字串類型的模型屬性執行輸入驗證和篩選</span><span class="sxs-lookup"><span data-stu-id="a8e7f-401"><a id="typemodel"></a>Perform input validation and filtering on all string type Model properties</span></span>

| <span data-ttu-id="a8e7f-402">Title</span><span class="sxs-lookup"><span data-stu-id="a8e7f-402">Title</span></span>                   | <span data-ttu-id="a8e7f-403">詳細資料</span><span class="sxs-lookup"><span data-stu-id="a8e7f-403">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="a8e7f-404">**元件**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-404">**Component**</span></span>               | <span data-ttu-id="a8e7f-405">Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="a8e7f-405">Web Application</span></span> | 
| <span data-ttu-id="a8e7f-406">**SDL 階段**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-406">**SDL Phase**</span></span>               | <span data-ttu-id="a8e7f-407">建置</span><span class="sxs-lookup"><span data-stu-id="a8e7f-407">Build</span></span> |  
| <span data-ttu-id="a8e7f-408">**適用的技術**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-408">**Applicable Technologies**</span></span> | <span data-ttu-id="a8e7f-409">泛型、MVC5、MVC6</span><span class="sxs-lookup"><span data-stu-id="a8e7f-409">Generic, MVC5, MVC6</span></span> |
| <span data-ttu-id="a8e7f-410">**屬性**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-410">**Attributes**</span></span>              | <span data-ttu-id="a8e7f-411">N/A</span><span class="sxs-lookup"><span data-stu-id="a8e7f-411">N/A</span></span>  |
| <span data-ttu-id="a8e7f-412">**參考**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-412">**References**</span></span>              | <span data-ttu-id="a8e7f-413">[新增驗證](http://www.asp.net/mvc/overview/getting-started/introduction/adding-validation)、[驗證 MVC 應用程式中的模型資料](http://msdn.microsoft.com/library/dd410404(v=vs.90).aspx)、[ASP.NET MVC 應用程式的指導原則](http://msdn.microsoft.com/magazine/dd942822.aspx)</span><span class="sxs-lookup"><span data-stu-id="a8e7f-413">[Adding Validation](http://www.asp.net/mvc/overview/getting-started/introduction/adding-validation), [Validating Model Data in an MVC Application](http://msdn.microsoft.com/library/dd410404(v=vs.90).aspx), [Guiding Principles For Your ASP.NET MVC Applications](http://msdn.microsoft.com/magazine/dd942822.aspx)</span></span> |
| <span data-ttu-id="a8e7f-414">**步驟**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-414">**Steps**</span></span> | <p><span data-ttu-id="a8e7f-415">所有輸入參數都必須先驗證再用於應用程式，以確保應用程式不受惡意使用者輸入所危害。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-415">All the input parameters must be validated before they are used in the application to ensure that the application is safeguarded against malicious user inputs.</span></span> <span data-ttu-id="a8e7f-416">請採取白名單驗證策略，在伺服器端上使用規則運算式驗證來驗證輸入值。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-416">Validate the input values using regular expression validations on server side with a whitelist validation strategy.</span></span> <span data-ttu-id="a8e7f-417">傳遞至方法的未清理使用者輸入/參數會造成程式碼插入弱點。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-417">Unsanitized user inputs / parameters passed to the methods can cause code injection vulnerabilities.</span></span></p><p><span data-ttu-id="a8e7f-418">對於 Web 應用程式，進入點還可能包括表單欄位、QueryStrings、Cookie、HTTP 標頭和 Web 服務參數。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-418">For web applications, entry points can also include form fields, QueryStrings, cookies, HTTP headers, and web service parameters.</span></span></p><p><span data-ttu-id="a8e7f-419">在繫結模型時，必須執行下列輸入驗證檢查︰</span><span class="sxs-lookup"><span data-stu-id="a8e7f-419">The following input validation checks must be performed upon model binding:</span></span></p><ul><li><span data-ttu-id="a8e7f-420">模型屬性應該使用 RegularExpression 註解來加以註解，以便接受允許的字元和最大允許長度</span><span class="sxs-lookup"><span data-stu-id="a8e7f-420">The model properties should be annotated with RegularExpression annotation, for accepting allowed characters and maximum permissible length</span></span></li><li><span data-ttu-id="a8e7f-421">控制器方法應該執行 ModelState 有效性</span><span class="sxs-lookup"><span data-stu-id="a8e7f-421">The controller methods should perform ModelState validity</span></span></li></ul>|

## <span data-ttu-id="a8e7f-422"><a id="richtext"></a>應該對接受所有字元的表單欄位 (例如 RTF 編輯器) 套用清理</span><span class="sxs-lookup"><span data-stu-id="a8e7f-422"><a id="richtext"></a>Sanitization should be applied on form fields that accept all characters, e.g, rich text editor</span></span>

| <span data-ttu-id="a8e7f-423">Title</span><span class="sxs-lookup"><span data-stu-id="a8e7f-423">Title</span></span>                   | <span data-ttu-id="a8e7f-424">詳細資料</span><span class="sxs-lookup"><span data-stu-id="a8e7f-424">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="a8e7f-425">**元件**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-425">**Component**</span></span>               | <span data-ttu-id="a8e7f-426">Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="a8e7f-426">Web Application</span></span> | 
| <span data-ttu-id="a8e7f-427">**SDL 階段**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-427">**SDL Phase**</span></span>               | <span data-ttu-id="a8e7f-428">建置</span><span class="sxs-lookup"><span data-stu-id="a8e7f-428">Build</span></span> |  
| <span data-ttu-id="a8e7f-429">**適用的技術**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-429">**Applicable Technologies**</span></span> | <span data-ttu-id="a8e7f-430">泛型</span><span class="sxs-lookup"><span data-stu-id="a8e7f-430">Generic</span></span> |
| <span data-ttu-id="a8e7f-431">**屬性**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-431">**Attributes**</span></span>              | <span data-ttu-id="a8e7f-432">N/A</span><span class="sxs-lookup"><span data-stu-id="a8e7f-432">N/A</span></span>  |
| <span data-ttu-id="a8e7f-433">**參考**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-433">**References**</span></span>              | <span data-ttu-id="a8e7f-434">[將不安全的輸入編碼](https://msdn.microsoft.com/library/ff647397.aspx#paght000003_step3)， [HTML 清理程式](https://github.com/mganss/HtmlSanitizer)</span><span class="sxs-lookup"><span data-stu-id="a8e7f-434">[Encode Unsafe Input](https://msdn.microsoft.com/library/ff647397.aspx#paght000003_step3), [HTML Sanitizer](https://github.com/mganss/HtmlSanitizer)</span></span> |
| <span data-ttu-id="a8e7f-435">**步驟**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-435">**Steps**</span></span> | <p><span data-ttu-id="a8e7f-436">找出您想要使用的所有靜態標記標籤。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-436">Identify all static markup tags that you want to use.</span></span> <span data-ttu-id="a8e7f-437">常見的作法是將格式限制為安全的 HTML 元素，例如 `<b>`(粗體) 和 `<i>` (斜體)。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-437">A common practice is to restrict formatting to safe HTML elements, such as `<b>` (bold) and `<i>` (italic).</span></span></p><p><span data-ttu-id="a8e7f-438">在寫入資料前，先對它進行 HTML 編碼。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-438">Before writing the data, HTML-encode it.</span></span> <span data-ttu-id="a8e7f-439">此動作可讓惡意指令碼變得安全，因為這會讓它以文字形式進行處理，而不是以可執行程式碼的形式。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-439">This makes any malicious script safe by causing it to be handled as text, not as executable code.</span></span></p><ol><li><span data-ttu-id="a8e7f-440">將 ValidateRequest ="false" 屬性新增至 @ Page 指示詞，以停用 ASP.NET 要求驗證</span><span class="sxs-lookup"><span data-stu-id="a8e7f-440">Disable ASP.NET request validation by the adding the ValidateRequest="false" attribute to the @ Page directive</span></span></li><li><span data-ttu-id="a8e7f-441">使用 HtmlEncode 方法將字串輸入編碼</span><span class="sxs-lookup"><span data-stu-id="a8e7f-441">Encode the string input with the HtmlEncode method</span></span></li><li><span data-ttu-id="a8e7f-442">使用 StringBuilder 並呼叫其取代方法，選擇性移除您想要允許之 HTML 元素上的編碼</span><span class="sxs-lookup"><span data-stu-id="a8e7f-442">Use a StringBuilder and call its Replace method to selectively remove the encoding on the HTML elements that you want to permit</span></span></li></ol><p><span data-ttu-id="a8e7f-443">參考中的頁面會藉由設定 `ValidateRequest="false"` 來停用 ASP.NET 要求驗證。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-443">The page-in the references disables ASP.NET request validation by setting `ValidateRequest="false"`.</span></span> <span data-ttu-id="a8e7f-444">它會對輸入進行 HTML 編碼，並選擇性地允許 `<b>` 和 `<i>`。或者，也可以使用 .NET 程式庫來清理 HTML。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-444">It HTML-encodes the input and selectively allows the `<b>` and `<i>` Alternatively, a .NET library for HTML sanitization may also be used.</span></span></p><p><span data-ttu-id="a8e7f-445">HtmlSanitizer 是用來從可能會導致 XSS 攻擊的建構中清理 HTML 片段和文件的 .NET 程式庫。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-445">HtmlSanitizer is a .NET library for cleaning HTML fragments and documents from constructs that can lead to XSS attacks.</span></span> <span data-ttu-id="a8e7f-446">它會使用 AngleSharp 來剖析、操作及轉譯 HTML 與 CSS。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-446">It uses AngleSharp to parse, manipulate, and render HTML and CSS.</span></span> <span data-ttu-id="a8e7f-447">HtmlSanitizer 可使用 NuGet 套件的形式來安裝，並可視需要透過相關 HTML 或 CSS 清理方法，在伺服器端上傳遞使用者輸入。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-447">HtmlSanitizer can be installed as a NuGet package, and the user input can be passed through relevant HTML or CSS sanitization methods, as applicable, on the server side.</span></span> <span data-ttu-id="a8e7f-448">請注意，只有在迫不得已時才可考慮使用清理做為安全性控制方法。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-448">Please note that Sanitization as a security control should be considered only as a last option.</span></span></p><p><span data-ttu-id="a8e7f-449">輸入驗證和輸出編碼會是較佳的安全性控制方法。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-449">Input validation and Output Encoding are considered better security controls.</span></span></p> |

## <span data-ttu-id="a8e7f-450"><a id="inbuilt-encode"></a>請勿將沒有內建編碼的 DOM 元素指派給接收器</span><span class="sxs-lookup"><span data-stu-id="a8e7f-450"><a id="inbuilt-encode"></a>Do not assign DOM elements to sinks that do not have inbuilt encoding</span></span>

| <span data-ttu-id="a8e7f-451">Title</span><span class="sxs-lookup"><span data-stu-id="a8e7f-451">Title</span></span>                   | <span data-ttu-id="a8e7f-452">詳細資料</span><span class="sxs-lookup"><span data-stu-id="a8e7f-452">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="a8e7f-453">**元件**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-453">**Component**</span></span>               | <span data-ttu-id="a8e7f-454">Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="a8e7f-454">Web Application</span></span> | 
| <span data-ttu-id="a8e7f-455">**SDL 階段**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-455">**SDL Phase**</span></span>               | <span data-ttu-id="a8e7f-456">建置</span><span class="sxs-lookup"><span data-stu-id="a8e7f-456">Build</span></span> |  
| <span data-ttu-id="a8e7f-457">**適用的技術**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-457">**Applicable Technologies**</span></span> | <span data-ttu-id="a8e7f-458">泛型</span><span class="sxs-lookup"><span data-stu-id="a8e7f-458">Generic</span></span> |
| <span data-ttu-id="a8e7f-459">**屬性**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-459">**Attributes**</span></span>              | <span data-ttu-id="a8e7f-460">N/A</span><span class="sxs-lookup"><span data-stu-id="a8e7f-460">N/A</span></span>  |
| <span data-ttu-id="a8e7f-461">**參考**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-461">**References**</span></span>              | <span data-ttu-id="a8e7f-462">N/A</span><span class="sxs-lookup"><span data-stu-id="a8e7f-462">N/A</span></span>  |
| <span data-ttu-id="a8e7f-463">**步驟**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-463">**Steps**</span></span> | <span data-ttu-id="a8e7f-464">許多 javascript 函式預設不會進行編碼。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-464">Many javascript functions don't do encoding by default.</span></span> <span data-ttu-id="a8e7f-465">透過這類函式將不受信任的輸入指派至 DOM 元素時，可能會導致執行跨網站指令碼 (XSS)。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-465">When assigning untrusted input to DOM elements via such functions, may result in cross site script (XSS) executions.</span></span>| 

### <a name="example"></a><span data-ttu-id="a8e7f-466">範例</span><span class="sxs-lookup"><span data-stu-id="a8e7f-466">Example</span></span>
<span data-ttu-id="a8e7f-467">以下是不安全的範例︰</span><span class="sxs-lookup"><span data-stu-id="a8e7f-467">Following are insecure examples:</span></span> 

```
document.getElementByID("div1").innerHtml = value;
$("#userName").html(res.Name);
return $('<div/>').html(value)
$('body').append(resHTML);   
```
<span data-ttu-id="a8e7f-468">請勿使用 `innerHtml`；而應使用 `innerText`。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-468">Don't use `innerHtml`; instead use `innerText`.</span></span> <span data-ttu-id="a8e7f-469">同樣地，不要使用 `$("#elm").html()`，而應使用 `$("#elm").text()`</span><span class="sxs-lookup"><span data-stu-id="a8e7f-469">Similarly, instead of `$("#elm").html()`, use `$("#elm").text()`</span></span> 

## <span data-ttu-id="a8e7f-470"><a id="redirect-safe"></a>驗證應用程式內的所有重新導向皆已關閉或安全完成</span><span class="sxs-lookup"><span data-stu-id="a8e7f-470"><a id="redirect-safe"></a>Validate all redirects within the application are closed or done safely</span></span>

| <span data-ttu-id="a8e7f-471">Title</span><span class="sxs-lookup"><span data-stu-id="a8e7f-471">Title</span></span>                   | <span data-ttu-id="a8e7f-472">詳細資料</span><span class="sxs-lookup"><span data-stu-id="a8e7f-472">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="a8e7f-473">**元件**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-473">**Component**</span></span>               | <span data-ttu-id="a8e7f-474">Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="a8e7f-474">Web Application</span></span> | 
| <span data-ttu-id="a8e7f-475">**SDL 階段**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-475">**SDL Phase**</span></span>               | <span data-ttu-id="a8e7f-476">建置</span><span class="sxs-lookup"><span data-stu-id="a8e7f-476">Build</span></span> |  
| <span data-ttu-id="a8e7f-477">**適用的技術**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-477">**Applicable Technologies**</span></span> | <span data-ttu-id="a8e7f-478">泛型</span><span class="sxs-lookup"><span data-stu-id="a8e7f-478">Generic</span></span> |
| <span data-ttu-id="a8e7f-479">**屬性**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-479">**Attributes**</span></span>              | <span data-ttu-id="a8e7f-480">N/A</span><span class="sxs-lookup"><span data-stu-id="a8e7f-480">N/A</span></span>  |
| <span data-ttu-id="a8e7f-481">**參考**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-481">**References**</span></span>              | [<span data-ttu-id="a8e7f-482">OAuth 2.0 授權架構 - 開啟重新導向程式</span><span class="sxs-lookup"><span data-stu-id="a8e7f-482">The OAuth 2.0 Authorization Framework - Open Redirectors</span></span>](http://tools.ietf.org/html/rfc6749#section-10.15) |
| <span data-ttu-id="a8e7f-483">**步驟**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-483">**Steps**</span></span> | <p><span data-ttu-id="a8e7f-484">要求重新導向至使用者所提供位置的應用程式設計，必須將可能的重新導向目標限制在預先定義的「安全」網站或網域清單。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-484">Application design requiring redirection to a user-supplied location must constrain the possible redirection targets to a predefined "safe" list of sites or domains.</span></span> <span data-ttu-id="a8e7f-485">應用程式中的所有重新導向都必須是封閉/安全的。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-485">All redirects in the application must be closed/safe.</span></span></p><p><span data-ttu-id="a8e7f-486">作法：</span><span class="sxs-lookup"><span data-stu-id="a8e7f-486">To do this:</span></span></p><ul><li><span data-ttu-id="a8e7f-487">找出所有重新導向</span><span class="sxs-lookup"><span data-stu-id="a8e7f-487">Identify all redirects</span></span></li><li><span data-ttu-id="a8e7f-488">為每個重新導向實作適當的風險降低措施。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-488">Implement an appropriate mitigation for each redirect.</span></span> <span data-ttu-id="a8e7f-489">適當的風險降低措施包括重新導向允許清單或使用者確認。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-489">Appropriate mitigations include redirect whitelist or user confirmation.</span></span> <span data-ttu-id="a8e7f-490">如果具有開啟重新導向弱點的網站或服務使用 Facebook/OAuth/OpenID 身分識別提供者，攻擊者便可竊取使用者的登入權杖，然後假扮該使用者。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-490">If a web site or service with an open redirect vulnerability uses Facebook/OAuth/OpenID identity providers, an attacker can steal a user's logon token and impersonate that user.</span></span> <span data-ttu-id="a8e7f-491">這是使用 OAuth 時的固有風險，在 RFC 6749「OAuth 2.0 授權架構」的 10.15 節「開啟重新導向」有其記載。同樣地，魚叉式網路釣魚攻擊也會使用開啟重新導向來入侵取得使用者的認證</span><span class="sxs-lookup"><span data-stu-id="a8e7f-491">This is an inherent risk when using OAuth, which is documented in RFC 6749 "The OAuth 2.0 Authorization Framework", Section 10.15 "Open Redirects" Similarly, users' credentials can be compromised by spear phishing attacks using open redirects</span></span></li></ul>|

## <span data-ttu-id="a8e7f-492"><a id="string-method"></a>對控制器方法所接受的所有字串類型參數實作輸入驗證</span><span class="sxs-lookup"><span data-stu-id="a8e7f-492"><a id="string-method"></a>Implement input validation on all string type parameters accepted by Controller methods</span></span>

| <span data-ttu-id="a8e7f-493">Title</span><span class="sxs-lookup"><span data-stu-id="a8e7f-493">Title</span></span>                   | <span data-ttu-id="a8e7f-494">詳細資料</span><span class="sxs-lookup"><span data-stu-id="a8e7f-494">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="a8e7f-495">**元件**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-495">**Component**</span></span>               | <span data-ttu-id="a8e7f-496">Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="a8e7f-496">Web Application</span></span> | 
| <span data-ttu-id="a8e7f-497">**SDL 階段**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-497">**SDL Phase**</span></span>               | <span data-ttu-id="a8e7f-498">建置</span><span class="sxs-lookup"><span data-stu-id="a8e7f-498">Build</span></span> |  
| <span data-ttu-id="a8e7f-499">**適用的技術**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-499">**Applicable Technologies**</span></span> | <span data-ttu-id="a8e7f-500">泛型、MVC5、MVC6</span><span class="sxs-lookup"><span data-stu-id="a8e7f-500">Generic, MVC5, MVC6</span></span> |
| <span data-ttu-id="a8e7f-501">**屬性**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-501">**Attributes**</span></span>              | <span data-ttu-id="a8e7f-502">N/A</span><span class="sxs-lookup"><span data-stu-id="a8e7f-502">N/A</span></span>  |
| <span data-ttu-id="a8e7f-503">**參考**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-503">**References**</span></span>              | <span data-ttu-id="a8e7f-504">[驗證 MVC 應用程式中的模型資料](http://msdn.microsoft.com/library/dd410404(v=vs.90).aspx)、[ASP.NET MVC 應用程式的指導原則](http://msdn.microsoft.com/magazine/dd942822.aspx)</span><span class="sxs-lookup"><span data-stu-id="a8e7f-504">[Validating Model Data in an MVC Application](http://msdn.microsoft.com/library/dd410404(v=vs.90).aspx), [Guiding Principles For Your ASP.NET MVC Applications](http://msdn.microsoft.com/magazine/dd942822.aspx)</span></span> |
| <span data-ttu-id="a8e7f-505">**步驟**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-505">**Steps**</span></span> | <span data-ttu-id="a8e7f-506">對於只接受基本資料類型而不接受模型來做為引數的方法，應該使用規則運算式進行輸入驗證。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-506">For methods that just accept primitive data type, and not models as argument,input validation using Regular Expression should be done.</span></span> <span data-ttu-id="a8e7f-507">在此，Regex.IsMatch 應搭配使用有效的 regex 模式。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-507">Here Regex.IsMatch should be used with a valid regex pattern.</span></span> <span data-ttu-id="a8e7f-508">如果輸入不符合指定的規則運算式，就不該再繼續進行控制，而且應該顯示關於驗證失敗的適當警告。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-508">If the input doesn't match the specified Regular Expression, control should not proceed further, and an adequate warning regarding validation failure should be displayed.</span></span>| 

## <span data-ttu-id="a8e7f-509"><a id="dos-expression"></a>為規則運算式處理設定逾時上限以防止因規則運算式不正確而導致 DoS</span><span class="sxs-lookup"><span data-stu-id="a8e7f-509"><a id="dos-expression"></a>Set upper limit timeout for regular expression processing to prevent DoS due to bad regular expressions</span></span>

| <span data-ttu-id="a8e7f-510">Title</span><span class="sxs-lookup"><span data-stu-id="a8e7f-510">Title</span></span>                   | <span data-ttu-id="a8e7f-511">詳細資料</span><span class="sxs-lookup"><span data-stu-id="a8e7f-511">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="a8e7f-512">**元件**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-512">**Component**</span></span>               | <span data-ttu-id="a8e7f-513">Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="a8e7f-513">Web Application</span></span> | 
| <span data-ttu-id="a8e7f-514">**SDL 階段**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-514">**SDL Phase**</span></span>               | <span data-ttu-id="a8e7f-515">建置</span><span class="sxs-lookup"><span data-stu-id="a8e7f-515">Build</span></span> |  
| <span data-ttu-id="a8e7f-516">**適用的技術**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-516">**Applicable Technologies**</span></span> | <span data-ttu-id="a8e7f-517">泛型、Web Form、MVC5、MVC6</span><span class="sxs-lookup"><span data-stu-id="a8e7f-517">Generic, Web Forms, MVC5, MVC6</span></span>  |
| <span data-ttu-id="a8e7f-518">**屬性**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-518">**Attributes**</span></span>              | <span data-ttu-id="a8e7f-519">N/A</span><span class="sxs-lookup"><span data-stu-id="a8e7f-519">N/A</span></span>  |
| <span data-ttu-id="a8e7f-520">**參考**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-520">**References**</span></span>              | [<span data-ttu-id="a8e7f-521">DefaultRegexMatchTimeout 屬性</span><span class="sxs-lookup"><span data-stu-id="a8e7f-521">DefaultRegexMatchTimeout Property </span></span>](https://msdn.microsoft.com/library/system.web.configuration.httpruntimesection.defaultregexmatchtimeout.aspx) |
| <span data-ttu-id="a8e7f-522">**步驟**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-522">**Steps**</span></span> | <span data-ttu-id="a8e7f-523">若要確保以錯誤格式建立的規則運算式不會遭受阻斷服務攻擊，而造成大量回溯，請設定全域的預設逾時。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-523">To ensure denial of service attacks against badly created regular expressions, that cause a lot of backtracking, set the global default timeout.</span></span> <span data-ttu-id="a8e7f-524">如果處理時間超過所定義的上限，便會擲回逾時例外狀況。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-524">If the processing time takes longer than the defined upper limit, it would throw a Timeout exception.</span></span> <span data-ttu-id="a8e7f-525">若未做任何設定，則逾時時間是無限。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-525">If nothing is configured, the timeout would be infinite.</span></span>| 

### <a name="example"></a><span data-ttu-id="a8e7f-526">範例</span><span class="sxs-lookup"><span data-stu-id="a8e7f-526">Example</span></span>
<span data-ttu-id="a8e7f-527">例如，下列組態會在處理時間超過 5 秒時擲回 RegexMatchTimeoutException︰</span><span class="sxs-lookup"><span data-stu-id="a8e7f-527">For example, the following configuration will throw a RegexMatchTimeoutException, if the processing takes more than 5 seconds:</span></span> 

```C#
<httpRuntime targetFramework="4.5" defaultRegexMatchTimeout="00:00:05" />
```

## <span data-ttu-id="a8e7f-528"><a id="html-razor"></a>避免在 Razor 檢視中使用 Html.Raw</span><span class="sxs-lookup"><span data-stu-id="a8e7f-528"><a id="html-razor"></a>Avoid using Html.Raw in Razor views</span></span>

| <span data-ttu-id="a8e7f-529">Title</span><span class="sxs-lookup"><span data-stu-id="a8e7f-529">Title</span></span>                   | <span data-ttu-id="a8e7f-530">詳細資料</span><span class="sxs-lookup"><span data-stu-id="a8e7f-530">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="a8e7f-531">**元件**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-531">**Component**</span></span>               | <span data-ttu-id="a8e7f-532">Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="a8e7f-532">Web Application</span></span> | 
| <span data-ttu-id="a8e7f-533">**SDL 階段**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-533">**SDL Phase**</span></span>               | <span data-ttu-id="a8e7f-534">建置</span><span class="sxs-lookup"><span data-stu-id="a8e7f-534">Build</span></span> |  
| <span data-ttu-id="a8e7f-535">**適用的技術**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-535">**Applicable Technologies**</span></span> | <span data-ttu-id="a8e7f-536">MVC5、MVC6</span><span class="sxs-lookup"><span data-stu-id="a8e7f-536">MVC5, MVC6</span></span> |
| <span data-ttu-id="a8e7f-537">**屬性**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-537">**Attributes**</span></span>              | <span data-ttu-id="a8e7f-538">N/A</span><span class="sxs-lookup"><span data-stu-id="a8e7f-538">N/A</span></span>  |
| <span data-ttu-id="a8e7f-539">**參考**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-539">**References**</span></span>              | <span data-ttu-id="a8e7f-540">N/A</span><span class="sxs-lookup"><span data-stu-id="a8e7f-540">N/A</span></span>  |
| <span data-ttu-id="a8e7f-541">步驟</span><span class="sxs-lookup"><span data-stu-id="a8e7f-541">Step</span></span> | <span data-ttu-id="a8e7f-542">ASP.Net 網頁 (Razor) 會執行自動 HTML 編碼。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-542">ASP.Net WebPages (Razor) perform automatic HTML encoding.</span></span> <span data-ttu-id="a8e7f-543">內嵌程式碼區塊 (@ blocks) 所列印的所有字串會自動進行 HTML 編碼。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-543">All strings printed by embedded code nuggets (@ blocks) are automatically HTML-encoded.</span></span> <span data-ttu-id="a8e7f-544">不過，在叫用 `HtmlHelper.Raw` 方法時，它會傳回非 HTML 編碼的標記。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-544">However, when `HtmlHelper.Raw` Method is invoked, it returns markup that is not HTML encoded.</span></span> <span data-ttu-id="a8e7f-545">如果使用 `Html.Raw()` 協助程式方法，它會略過 Razor 所提供的自動編碼保護。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-545">If `Html.Raw()` helper method is used, it bypasses the automatic encoding protection that Razor provides.</span></span>|

### <a name="example"></a><span data-ttu-id="a8e7f-546">範例</span><span class="sxs-lookup"><span data-stu-id="a8e7f-546">Example</span></span>
<span data-ttu-id="a8e7f-547">以下是不安全的範例︰</span><span class="sxs-lookup"><span data-stu-id="a8e7f-547">Following is an insecure example:</span></span> 

```C#
<div class="form-group">
            @Html.Raw(Model.AccountConfirmText)
        </div>
        <div class="form-group">
            @Html.Raw(Model.PaymentConfirmText)
        </div>
</div>
```
<span data-ttu-id="a8e7f-548">除非您需要顯示標記，否則請勿使用 `Html.Raw()`。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-548">Do not use `Html.Raw()` unless you need to display markup.</span></span> <span data-ttu-id="a8e7f-549">這個方法不會隱含執行輸出編碼。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-549">This method does not perform output encoding implicitly.</span></span> <span data-ttu-id="a8e7f-550">請使用其他 ASP.NET 協助程式，例如 `@Html.DisplayFor()`</span><span class="sxs-lookup"><span data-stu-id="a8e7f-550">Use other ASP.NET helpers e.g., `@Html.DisplayFor()`</span></span> 

## <span data-ttu-id="a8e7f-551"><a id="stored-proc"></a>請勿在預存程序中使用動態查詢</span><span class="sxs-lookup"><span data-stu-id="a8e7f-551"><a id="stored-proc"></a>Do not use dynamic queries in stored procedures</span></span>

| <span data-ttu-id="a8e7f-552">Title</span><span class="sxs-lookup"><span data-stu-id="a8e7f-552">Title</span></span>                   | <span data-ttu-id="a8e7f-553">詳細資料</span><span class="sxs-lookup"><span data-stu-id="a8e7f-553">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="a8e7f-554">**元件**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-554">**Component**</span></span>               | <span data-ttu-id="a8e7f-555">資料庫</span><span class="sxs-lookup"><span data-stu-id="a8e7f-555">Database</span></span> | 
| <span data-ttu-id="a8e7f-556">**SDL 階段**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-556">**SDL Phase**</span></span>               | <span data-ttu-id="a8e7f-557">建置</span><span class="sxs-lookup"><span data-stu-id="a8e7f-557">Build</span></span> |  
| <span data-ttu-id="a8e7f-558">**適用的技術**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-558">**Applicable Technologies**</span></span> | <span data-ttu-id="a8e7f-559">泛型</span><span class="sxs-lookup"><span data-stu-id="a8e7f-559">Generic</span></span> |
| <span data-ttu-id="a8e7f-560">**屬性**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-560">**Attributes**</span></span>              | <span data-ttu-id="a8e7f-561">N/A</span><span class="sxs-lookup"><span data-stu-id="a8e7f-561">N/A</span></span>  |
| <span data-ttu-id="a8e7f-562">**參考**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-562">**References**</span></span>              | <span data-ttu-id="a8e7f-563">N/A</span><span class="sxs-lookup"><span data-stu-id="a8e7f-563">N/A</span></span>  |
| <span data-ttu-id="a8e7f-564">**步驟**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-564">**Steps**</span></span> | <p><span data-ttu-id="a8e7f-565">SQL 插入式攻擊利用輸入驗證弱點在資料庫中執行任意命令。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-565">A SQL injection attack exploits vulnerabilities in input validation to run arbitrary commands in the database.</span></span> <span data-ttu-id="a8e7f-566">當您的應用程式使用輸入來建構動態 SQL 陳述式以存取資料庫時，便可能發生此弱點。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-566">It can occur when your application uses input to construct dynamic SQL statements to access the database.</span></span> <span data-ttu-id="a8e7f-567">如果您的程式碼使用預存程序來傳遞包含原始使用者輸入的字串，也可能發生此弱點。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-567">It can also occur if your code uses stored procedures that are passed strings that contain raw user input.</span></span> <span data-ttu-id="a8e7f-568">攻擊者使用 SQL 插入式攻擊，即可在資料庫中執行任意命令。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-568">Using the SQL injection attack, the attacker can execute arbitrary commands in the database.</span></span> <span data-ttu-id="a8e7f-569">所有 SQL 陳述式 (包括預存程序的 SQL 陳述式) 都必須予以參數化。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-569">All SQL statements (including the SQL statements in stored procedures) must be parameterized.</span></span> <span data-ttu-id="a8e7f-570">參數化的 SQL 陳述式會接受對 SQL 具有特殊意義的字元 (例如單引號) 而不會有任何問題，因為它們屬於強型別。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-570">Parameterized SQL statements will accept characters that have special meaning to SQL (like single quote) without problems because they are strongly typed.</span></span> |

### <a name="example"></a><span data-ttu-id="a8e7f-571">範例</span><span class="sxs-lookup"><span data-stu-id="a8e7f-571">Example</span></span>
<span data-ttu-id="a8e7f-572">以下是不安全的動態預存程序範例︰</span><span class="sxs-lookup"><span data-stu-id="a8e7f-572">Following is an example of insecure dynamic Stored Procedure:</span></span> 

```C#
CREATE PROCEDURE [dbo].[uspGetProductsByCriteria]
(
  @productName nvarchar(200) = NULL,
  @startPrice float = NULL,
  @endPrice float = NULL
)
AS
 BEGIN
  DECLARE @sql nvarchar(max)
  SELECT @sql = ' SELECT ProductID, ProductName, Description, UnitPrice, ImagePath' +
       ' FROM dbo.Products WHERE 1 = 1 '
       PRINT @sql
  IF @productName IS NOT NULL
     SELECT @sql = @sql + ' AND ProductName LIKE ''%' + @productName + '%'''
  IF @startPrice IS NOT NULL
     SELECT @sql = @sql + ' AND UnitPrice > ''' + CONVERT(VARCHAR(10),@startPrice) + ''''
  IF @endPrice IS NOT NULL
     SELECT @sql = @sql + ' AND UnitPrice < ''' + CONVERT(VARCHAR(10),@endPrice) + ''''

  PRINT @sql
  EXEC(@sql)
 END
```

### <a name="example"></a><span data-ttu-id="a8e7f-573">範例</span><span class="sxs-lookup"><span data-stu-id="a8e7f-573">Example</span></span>
<span data-ttu-id="a8e7f-574">以下是以安全方式實作的相同預存程序︰</span><span class="sxs-lookup"><span data-stu-id="a8e7f-574">Following is the same stored procedure implemented securely:</span></span> 
```C#
CREATE PROCEDURE [dbo].[uspGetProductsByCriteriaSecure]
(
             @productName nvarchar(200) = NULL,
             @startPrice float = NULL,
             @endPrice float = NULL
)
AS
       BEGIN
             SELECT ProductID, ProductName, Description, UnitPrice, ImagePath
             FROM dbo.Products where
             (@productName IS NULL or ProductName like '%'+ @productName +'%')
             AND
             (@startPrice IS NULL or UnitPrice > @startPrice)
             AND
             (@endPrice IS NULL or UnitPrice < @endPrice)         
       END
```

## <span data-ttu-id="a8e7f-575"><a id="validation-api"></a>確定 Web API 方法已完成模型驗證</span><span class="sxs-lookup"><span data-stu-id="a8e7f-575"><a id="validation-api"></a>Ensure that model validation is done on Web API methods</span></span>

| <span data-ttu-id="a8e7f-576">Title</span><span class="sxs-lookup"><span data-stu-id="a8e7f-576">Title</span></span>                   | <span data-ttu-id="a8e7f-577">詳細資料</span><span class="sxs-lookup"><span data-stu-id="a8e7f-577">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="a8e7f-578">**元件**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-578">**Component**</span></span>               | <span data-ttu-id="a8e7f-579">Web API</span><span class="sxs-lookup"><span data-stu-id="a8e7f-579">Web API</span></span> | 
| <span data-ttu-id="a8e7f-580">**SDL 階段**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-580">**SDL Phase**</span></span>               | <span data-ttu-id="a8e7f-581">建置</span><span class="sxs-lookup"><span data-stu-id="a8e7f-581">Build</span></span> |  
| <span data-ttu-id="a8e7f-582">**適用的技術**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-582">**Applicable Technologies**</span></span> | <span data-ttu-id="a8e7f-583">MVC5、MVC6</span><span class="sxs-lookup"><span data-stu-id="a8e7f-583">MVC5, MVC6</span></span> |
| <span data-ttu-id="a8e7f-584">**屬性**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-584">**Attributes**</span></span>              | <span data-ttu-id="a8e7f-585">N/A</span><span class="sxs-lookup"><span data-stu-id="a8e7f-585">N/A</span></span>  |
| <span data-ttu-id="a8e7f-586">**參考**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-586">**References**</span></span>              | [<span data-ttu-id="a8e7f-587">ASP.NET Web API 中的模型驗證</span><span class="sxs-lookup"><span data-stu-id="a8e7f-587">Model Validation in ASP.NET Web API </span></span>](http://www.asp.net/web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api) |
| <span data-ttu-id="a8e7f-588">**步驟**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-588">**Steps**</span></span> | <span data-ttu-id="a8e7f-589">當用戶端傳送資料到 Web API 時，必須先驗證資料再進行任何處理。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-589">When a client sends data to a web API, it is mandatory to validate the data before doing any processing.</span></span> <span data-ttu-id="a8e7f-590">對於可接受模型做為輸入的 ASP.NET Web API，請在模型上使用資料註解，以對模型屬性設定驗證規則。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-590">For ASP.NET Web APIs which accept models as input, use data annotations on models to set validation rules on the properties of the model.</span></span>|

### <a name="example"></a><span data-ttu-id="a8e7f-591">範例</span><span class="sxs-lookup"><span data-stu-id="a8e7f-591">Example</span></span>
<span data-ttu-id="a8e7f-592">下列程式碼示範相同案例︰</span><span class="sxs-lookup"><span data-stu-id="a8e7f-592">The following code demonstrates the same:</span></span> 

```C#
using System.ComponentModel.DataAnnotations;

namespace MyApi.Models
{
    public class Product
    {
        public int Id { get; set; }
        [Required]
        [RegularExpression(@"^[a-zA-Z0-9]*$", ErrorMessage="Only alphanumeric characters are allowed.")]
        public string Name { get; set; }
        public decimal Price { get; set; }
        [Range(0, 999)]
        public double Weight { get; set; }
    }
}
```

### <a name="example"></a><span data-ttu-id="a8e7f-593">範例</span><span class="sxs-lookup"><span data-stu-id="a8e7f-593">Example</span></span>
<span data-ttu-id="a8e7f-594">在 API 控制器的動作方法中，模型的有效性必須明確檢查，如下所示：</span><span class="sxs-lookup"><span data-stu-id="a8e7f-594">In the action method of the API controllers, validity of the model has to be explicitly checked as shown below:</span></span> 

```C#
namespace MyApi.Controllers
{
    public class ProductsController : ApiController
    {
        public HttpResponseMessage Post(Product product)
        {
            if (ModelState.IsValid)
            {
                // Do something with the product (not shown).

                return new HttpResponseMessage(HttpStatusCode.OK);
            }
            else
            {
                return Request.CreateErrorResponse(HttpStatusCode.BadRequest, ModelState);
            }
        }
    }
}
```

## <span data-ttu-id="a8e7f-595"><a id="string-api"></a>對 Web API 方法所接受的所有字串類型參數實作輸入驗證</span><span class="sxs-lookup"><span data-stu-id="a8e7f-595"><a id="string-api"></a>Implement input validation on all string type parameters accepted by Web API methods</span></span>

| <span data-ttu-id="a8e7f-596">Title</span><span class="sxs-lookup"><span data-stu-id="a8e7f-596">Title</span></span>                   | <span data-ttu-id="a8e7f-597">詳細資料</span><span class="sxs-lookup"><span data-stu-id="a8e7f-597">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="a8e7f-598">**元件**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-598">**Component**</span></span>               | <span data-ttu-id="a8e7f-599">Web API</span><span class="sxs-lookup"><span data-stu-id="a8e7f-599">Web API</span></span> | 
| <span data-ttu-id="a8e7f-600">**SDL 階段**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-600">**SDL Phase**</span></span>               | <span data-ttu-id="a8e7f-601">建置</span><span class="sxs-lookup"><span data-stu-id="a8e7f-601">Build</span></span> |  
| <span data-ttu-id="a8e7f-602">**適用的技術**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-602">**Applicable Technologies**</span></span> | <span data-ttu-id="a8e7f-603">泛型、MVC 5、MVC 6</span><span class="sxs-lookup"><span data-stu-id="a8e7f-603">Generic, MVC 5, MVC 6</span></span> |
| <span data-ttu-id="a8e7f-604">**屬性**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-604">**Attributes**</span></span>              | <span data-ttu-id="a8e7f-605">N/A</span><span class="sxs-lookup"><span data-stu-id="a8e7f-605">N/A</span></span>  |
| <span data-ttu-id="a8e7f-606">**參考**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-606">**References**</span></span>              | <span data-ttu-id="a8e7f-607">[驗證 MVC 應用程式中的模型資料](http://msdn.microsoft.com/library/dd410404(v=vs.90).aspx)、[ASP.NET MVC 應用程式的指導原則](http://msdn.microsoft.com/magazine/dd942822.aspx)</span><span class="sxs-lookup"><span data-stu-id="a8e7f-607">[Validating Model Data in an MVC Application](http://msdn.microsoft.com/library/dd410404(v=vs.90).aspx), [Guiding Principles For Your ASP.NET MVC Applications](http://msdn.microsoft.com/magazine/dd942822.aspx)</span></span> |
| <span data-ttu-id="a8e7f-608">**步驟**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-608">**Steps**</span></span> | <span data-ttu-id="a8e7f-609">對於只接受基本資料類型而不接受模型來做為引數的方法，應該使用規則運算式進行輸入驗證。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-609">For methods that just accept primitive data type, and not models as argument,input validation using Regular Expression should be done.</span></span> <span data-ttu-id="a8e7f-610">在此，Regex.IsMatch 應搭配使用有效的 regex 模式。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-610">Here Regex.IsMatch should be used with a valid regex pattern.</span></span> <span data-ttu-id="a8e7f-611">如果輸入不符合指定的規則運算式，就不該再繼續進行控制，而且應該顯示關於驗證失敗的適當警告。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-611">If the input doesn't match the specified Regular Expression, control should not proceed further, and an adequate warning regarding validation failure should be displayed.</span></span>|

## <span data-ttu-id="a8e7f-612"><a id="typesafe-api"></a>確定 Web API 有使用 type-safe 參數來存取資料</span><span class="sxs-lookup"><span data-stu-id="a8e7f-612"><a id="typesafe-api"></a>Ensure that type-safe parameters are used in Web API for data access</span></span>

| <span data-ttu-id="a8e7f-613">Title</span><span class="sxs-lookup"><span data-stu-id="a8e7f-613">Title</span></span>                   | <span data-ttu-id="a8e7f-614">詳細資料</span><span class="sxs-lookup"><span data-stu-id="a8e7f-614">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="a8e7f-615">**元件**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-615">**Component**</span></span>               | <span data-ttu-id="a8e7f-616">Web API</span><span class="sxs-lookup"><span data-stu-id="a8e7f-616">Web API</span></span> | 
| <span data-ttu-id="a8e7f-617">**SDL 階段**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-617">**SDL Phase**</span></span>               | <span data-ttu-id="a8e7f-618">建置</span><span class="sxs-lookup"><span data-stu-id="a8e7f-618">Build</span></span> |  
| <span data-ttu-id="a8e7f-619">**適用的技術**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-619">**Applicable Technologies**</span></span> | <span data-ttu-id="a8e7f-620">泛型</span><span class="sxs-lookup"><span data-stu-id="a8e7f-620">Generic</span></span> |
| <span data-ttu-id="a8e7f-621">**屬性**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-621">**Attributes**</span></span>              | <span data-ttu-id="a8e7f-622">N/A</span><span class="sxs-lookup"><span data-stu-id="a8e7f-622">N/A</span></span>  |
| <span data-ttu-id="a8e7f-623">**參考**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-623">**References**</span></span>              | <span data-ttu-id="a8e7f-624">N/A</span><span class="sxs-lookup"><span data-stu-id="a8e7f-624">N/A</span></span>  |
| <span data-ttu-id="a8e7f-625">**步驟**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-625">**Steps**</span></span> | <p><span data-ttu-id="a8e7f-626">如果您使用參數集合，SQL 會將輸入視為常值而非可執行程式碼。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-626">If you use the Parameters collection, SQL treats the input is as a literal value rather then as executable code.</span></span> <span data-ttu-id="a8e7f-627">參數集合可用來對輸入資料強制執行類型和長度條件約束。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-627">The Parameters collection can be used to enforce type and length constraints on input data.</span></span> <span data-ttu-id="a8e7f-628">超出範圍的值會觸發例外狀況。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-628">Values outside of the range trigger an exception.</span></span> <span data-ttu-id="a8e7f-629">如果未使用 type-safe SQL 參數，攻擊者或許就能執行內嵌於未經篩選之輸入中的插入式攻擊。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-629">If type-safe SQL parameters are not used, attackers might be able to execute injection attacks that are embedded in the unfiltered input.</span></span></p><p><span data-ttu-id="a8e7f-630">請在建構 SQL 查詢時使用 type-safe 參數，以避免未經篩選的輸入中可能發生的 SQL 插入式攻擊。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-630">Use type safe parameters when constructing SQL queries to avoid possible SQL injection attacks that can occur with unfiltered input.</span></span> <span data-ttu-id="a8e7f-631">type-safe 參數可與預存程序和動態 SQL 陳述式搭配使用。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-631">You can use type safe parameters with stored procedures and with dynamic SQL statements.</span></span> <span data-ttu-id="a8e7f-632">資料庫會將參數視為常值而非可執行程式碼。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-632">Parameters are treated as literal values by the database and not as executable code.</span></span> <span data-ttu-id="a8e7f-633">參數的類型和長度也會受到檢查。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-633">Parameters are also checked for type and length.</span></span></p>|

### <a name="example"></a><span data-ttu-id="a8e7f-634">範例</span><span class="sxs-lookup"><span data-stu-id="a8e7f-634">Example</span></span>
<span data-ttu-id="a8e7f-635">下列程式碼示範如何在呼叫預存程序時，搭配使用 type-safe 參數與 SqlParameterCollection。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-635">The following code shows how to use type safe parameters with the SqlParameterCollection when calling a stored procedure.</span></span> 

```C#
using System.Data;
using System.Data.SqlClient;

using (SqlConnection connection = new SqlConnection(connectionString))
{ 
DataSet userDataset = new DataSet(); 
SqlDataAdapter myCommand = new SqlDataAdapter(LoginStoredProcedure", connection); 
myCommand.SelectCommand.CommandType = CommandType.StoredProcedure; 
myCommand.SelectCommand.Parameters.Add("@au_id", SqlDbType.VarChar, 11); 
myCommand.SelectCommand.Parameters["@au_id"].Value = SSN.Text; 
myCommand.Fill(userDataset);
}  
```
<span data-ttu-id="a8e7f-636">在上述程式碼範例中，輸入值不能超過 11 個字元。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-636">In the preceding code example, the input value cannot be longer than 11 characters.</span></span> <span data-ttu-id="a8e7f-637">如果資料不符合參數所定義的類型或長度，SqlParameter 類別就會擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-637">If the data does not conform to the type or length defined by the parameter, the SqlParameter class throws an exception.</span></span> 

## <span data-ttu-id="a8e7f-638"><a id="sql-docdb"></a>針對 Cosmos DB 使用參數化 SQL 查詢</span><span class="sxs-lookup"><span data-stu-id="a8e7f-638"><a id="sql-docdb"></a>Use parametrized SQL queries for Cosmos DB</span></span>

| <span data-ttu-id="a8e7f-639">Title</span><span class="sxs-lookup"><span data-stu-id="a8e7f-639">Title</span></span>                   | <span data-ttu-id="a8e7f-640">詳細資料</span><span class="sxs-lookup"><span data-stu-id="a8e7f-640">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="a8e7f-641">**元件**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-641">**Component**</span></span>               | <span data-ttu-id="a8e7f-642">Azure Document DB</span><span class="sxs-lookup"><span data-stu-id="a8e7f-642">Azure Document DB</span></span> | 
| <span data-ttu-id="a8e7f-643">**SDL 階段**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-643">**SDL Phase**</span></span>               | <span data-ttu-id="a8e7f-644">建置</span><span class="sxs-lookup"><span data-stu-id="a8e7f-644">Build</span></span> |  
| <span data-ttu-id="a8e7f-645">**適用的技術**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-645">**Applicable Technologies**</span></span> | <span data-ttu-id="a8e7f-646">泛型</span><span class="sxs-lookup"><span data-stu-id="a8e7f-646">Generic</span></span> |
| <span data-ttu-id="a8e7f-647">**屬性**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-647">**Attributes**</span></span>              | <span data-ttu-id="a8e7f-648">N/A</span><span class="sxs-lookup"><span data-stu-id="a8e7f-648">N/A</span></span>  |
| <span data-ttu-id="a8e7f-649">**參考**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-649">**References**</span></span>              | [<span data-ttu-id="a8e7f-650">在 DocumentDB 中宣佈 SQL 參數化</span><span class="sxs-lookup"><span data-stu-id="a8e7f-650">Announcing SQL Parameterization in DocumentDB</span></span>](https://azure.microsoft.com/blog/announcing-sql-parameterization-in-documentdb/) |
| <span data-ttu-id="a8e7f-651">**步驟**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-651">**Steps**</span></span> | <span data-ttu-id="a8e7f-652">雖然 DocumentDB 只支援唯讀查詢，但如果查詢是藉由串連使用者輸入來建構，仍可以發動 SQL 插入式攻擊。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-652">Although DocumentDB only supports read-only queries, SQL injection is still possible if queries are constructed by concatenating with user input.</span></span> <span data-ttu-id="a8e7f-653">使用者只要藉由編寫惡意 SQL 查詢，即可在相同集合內存取他們不該能夠存取的資料。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-653">It might be possible for a user to gain access to data they shouldn’t be accessing within the same collection by crafting malicious SQL queries.</span></span> <span data-ttu-id="a8e7f-654">如果查詢是根據使用者輸入所建構而成，請使用參數化的 SQL 查詢。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-654">Use parameterized SQL queries if queries are constructed based on user input.</span></span> |

## <span data-ttu-id="a8e7f-655"><a id="schema-binding"></a>透過結構描述繫結驗證 WCF 輸入</span><span class="sxs-lookup"><span data-stu-id="a8e7f-655"><a id="schema-binding"></a>WCF Input validation through Schema binding</span></span>

| <span data-ttu-id="a8e7f-656">Title</span><span class="sxs-lookup"><span data-stu-id="a8e7f-656">Title</span></span>                   | <span data-ttu-id="a8e7f-657">詳細資料</span><span class="sxs-lookup"><span data-stu-id="a8e7f-657">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="a8e7f-658">**元件**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-658">**Component**</span></span>               | <span data-ttu-id="a8e7f-659">WCF</span><span class="sxs-lookup"><span data-stu-id="a8e7f-659">WCF</span></span> | 
| <span data-ttu-id="a8e7f-660">**SDL 階段**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-660">**SDL Phase**</span></span>               | <span data-ttu-id="a8e7f-661">建置</span><span class="sxs-lookup"><span data-stu-id="a8e7f-661">Build</span></span> |  
| <span data-ttu-id="a8e7f-662">**適用的技術**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-662">**Applicable Technologies**</span></span> | <span data-ttu-id="a8e7f-663">泛型、NET Framework 3</span><span class="sxs-lookup"><span data-stu-id="a8e7f-663">Generic, NET Framework 3</span></span> |
| <span data-ttu-id="a8e7f-664">**屬性**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-664">**Attributes**</span></span>              | <span data-ttu-id="a8e7f-665">N/A</span><span class="sxs-lookup"><span data-stu-id="a8e7f-665">N/A</span></span>  |
| <span data-ttu-id="a8e7f-666">**參考**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-666">**References**</span></span>              | [<span data-ttu-id="a8e7f-667">MSDN</span><span class="sxs-lookup"><span data-stu-id="a8e7f-667">MSDN</span></span>](https://msdn.microsoft.com/library/ff647820.aspx) |
| <span data-ttu-id="a8e7f-668">**步驟**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-668">**Steps**</span></span> | <p><span data-ttu-id="a8e7f-669">缺少驗證機制會導致不同類型的插入式攻擊。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-669">Lack of validation leads to different type injection attacks.</span></span></p><p><span data-ttu-id="a8e7f-670">訊息驗證代表 WCF 應用程式保護措施中的一條防禦線。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-670">Message validation represents one line of defense in the protection of your WCF application.</span></span> <span data-ttu-id="a8e7f-671">利用這個方法，您可以使用結構描述來驗證訊息，以防止惡意用戶端攻擊 WCF 服務作業。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-671">With this approach, you validate messages using schemas to protect WCF service operations from attack by a malicious client.</span></span> <span data-ttu-id="a8e7f-672">驗證用戶端所收到的所有訊息可防止用戶端遭到惡意服務攻擊。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-672">Validate all messages received by the client to protect the client from attack by a malicious service.</span></span> <span data-ttu-id="a8e7f-673">訊息驗證可讓您在作業取用訊息合約或資料合約時驗證訊息，使用參數驗證則無法這麼做。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-673">Message validation makes it possible to validate messages when operations consume message contracts or data contracts, which cannot be done using parameter validation.</span></span> <span data-ttu-id="a8e7f-674">訊息驗證可讓您在結構描述內建立驗證邏輯，進而提供更大的彈性並縮減開發時間。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-674">Message validation allows you to create validation logic inside schemas, thereby providing more flexibility and reducing development time.</span></span> <span data-ttu-id="a8e7f-675">結構描述可以重複使用到組織中的不同應用程式，而為如何代表資料建立標準。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-675">Schemas can be reused across different applications inside the organization, creating standards for data representation.</span></span> <span data-ttu-id="a8e7f-676">此外，在它們取用涉及代表商務邏輯之合約的更複雜資料類型時，訊息驗證可讓您保護作業。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-676">Additionally, message validation allows you to protect operations when they consume more complex data types involving contracts representing business logic.</span></span></p><p><span data-ttu-id="a8e7f-677">若要執行訊息驗證，您可以先建置結構描述來代表服務的作業和這些作業所取用的資料類型。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-677">To perform message validation, you first build a schema that represents the operations of your service and the data types consumed by those operations.</span></span> <span data-ttu-id="a8e7f-678">然後，您可以建立 .NET 類別來實作自訂用戶端訊息偵測器和自訂發送器訊息偵測器，以驗證服務所傳送/接收的訊息。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-678">You then create a .NET class that implements a custom client message inspector and custom dispatcher message inspector to validate the messages sent/received to/from the service.</span></span> <span data-ttu-id="a8e7f-679">接下來，您可以實作自訂端點行為，在用戶端和服務上啟用訊息驗證。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-679">Next, you implement a custom endpoint behavior to enable message validation on both the client and the service.</span></span> <span data-ttu-id="a8e7f-680">最後，您可以對類別實作自訂組態元素，以便您可以在服務或用戶端的組態檔中，公開擴充的自訂端點行為</span><span class="sxs-lookup"><span data-stu-id="a8e7f-680">Finally, you implement a custom configuration element on the class that allows you to expose the extended custom endpoint behavior in the configuration file of the service or the client"</span></span></p>|

## <span data-ttu-id="a8e7f-681"><a id="parameters"></a>透過參數偵測器驗證 WCF 輸入</span><span class="sxs-lookup"><span data-stu-id="a8e7f-681"><a id="parameters"></a>WCF- Input validation through Parameter Inspectors</span></span>

| <span data-ttu-id="a8e7f-682">Title</span><span class="sxs-lookup"><span data-stu-id="a8e7f-682">Title</span></span>                   | <span data-ttu-id="a8e7f-683">詳細資料</span><span class="sxs-lookup"><span data-stu-id="a8e7f-683">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="a8e7f-684">**元件**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-684">**Component**</span></span>               | <span data-ttu-id="a8e7f-685">WCF</span><span class="sxs-lookup"><span data-stu-id="a8e7f-685">WCF</span></span> | 
| <span data-ttu-id="a8e7f-686">**SDL 階段**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-686">**SDL Phase**</span></span>               | <span data-ttu-id="a8e7f-687">建置</span><span class="sxs-lookup"><span data-stu-id="a8e7f-687">Build</span></span> |  
| <span data-ttu-id="a8e7f-688">**適用的技術**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-688">**Applicable Technologies**</span></span> | <span data-ttu-id="a8e7f-689">泛型、NET Framework 3</span><span class="sxs-lookup"><span data-stu-id="a8e7f-689">Generic, NET Framework 3</span></span> |
| <span data-ttu-id="a8e7f-690">**屬性**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-690">**Attributes**</span></span>              | <span data-ttu-id="a8e7f-691">N/A</span><span class="sxs-lookup"><span data-stu-id="a8e7f-691">N/A</span></span>  |
| <span data-ttu-id="a8e7f-692">**參考**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-692">**References**</span></span>              | [<span data-ttu-id="a8e7f-693">MSDN</span><span class="sxs-lookup"><span data-stu-id="a8e7f-693">MSDN</span></span>](https://msdn.microsoft.com/library/ff647875.aspx) |
| <span data-ttu-id="a8e7f-694">**步驟**</span><span class="sxs-lookup"><span data-stu-id="a8e7f-694">**Steps**</span></span> | <p><span data-ttu-id="a8e7f-695">輸入和資料驗證代表 WCF 應用程式保護措施中的一條重要防禦線。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-695">Input and data validation represents one important line of defense in the protection of your WCF application.</span></span> <span data-ttu-id="a8e7f-696">您應該驗證 WCF 服務作業中公開的所有參數，以防止服務遭受惡意用戶端攻擊。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-696">You should validate all parameters exposed in WCF service operations to protect the service from attack by a malicious client.</span></span> <span data-ttu-id="a8e7f-697">相反地，您還應該驗證用戶端所收到的所有傳回值，以防止用戶端遭受惡意服務攻擊</span><span class="sxs-lookup"><span data-stu-id="a8e7f-697">Conversely, you should also validate all return values received by the client to protect the client from attack by a malicious service</span></span></p><p><span data-ttu-id="a8e7f-698">WCF 會提供不同的擴充點，讓您藉由建立自訂擴充功能來自訂 WCF 執行階段行為。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-698">WCF provides different extensibility points that allow you to customize the WCF runtime behavior by creating custom extensions.</span></span> <span data-ttu-id="a8e7f-699">訊息偵測器和參數偵測器這兩個擴充性機制可用來加強對用戶端和服務之間所傳遞之資料的控制力。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-699">Message Inspectors and Parameter Inspectors are two extensibility mechanisms used to gain greater control over the data passing between a client and a service.</span></span> <span data-ttu-id="a8e7f-700">您應該使用參數偵測器來驗證輸入，而只將訊息偵測器用於當您需要檢查流入及流出服務的整個訊息時。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-700">You should use parameter inspectors for input validation and use message inspectors only when you need to inspect the entire message flowing in and out of a service.</span></span></p><p><span data-ttu-id="a8e7f-701">若要執行輸入驗證，您需要建置 .NET 類別，並實作自訂參數偵測器，以對服務中的作業參數進行驗證。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-701">To perform input validation, you will build a .NET class and implement a custom parameter inspector in order to validate parameters on operations in your service.</span></span> <span data-ttu-id="a8e7f-702">接著，您需要實作自訂端點行為，在用戶端和服務上啟用驗證。</span><span class="sxs-lookup"><span data-stu-id="a8e7f-702">You will then implement a custom endpoint behavior to enable validation on both the client and the service.</span></span> <span data-ttu-id="a8e7f-703">最後，您可以對類別實作自訂組態元素，以便您可以在服務或用戶端的組態檔中，公開擴充的自訂端點行為</span><span class="sxs-lookup"><span data-stu-id="a8e7f-703">Finally, you will implement a custom configuration element on the class that allows you to expose the extended custom endpoint behavior in the configuration file of the service or the client</span></span></p>|
