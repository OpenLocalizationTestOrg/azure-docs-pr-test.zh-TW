---
title: "搭配 CORS 使用 Azure CDN | Microsoft Docs"
description: "了解如何使用 Azure 內容傳遞網路 (CDN) 搭配跨來源資源共用 (CORS)。"
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 86740a96-4269-4060-aba3-a69f00e6f14e
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 7070397f6e69b21add75bad8220f0b8ebe36d266
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="using-azure-cdn-with-cors"></a><span data-ttu-id="6985d-103">搭配 CORS 使用 Azure CDN</span><span class="sxs-lookup"><span data-stu-id="6985d-103">Using Azure CDN with CORS</span></span>
## <a name="what-is-cors"></a><span data-ttu-id="6985d-104">CORS 是什麼？</span><span class="sxs-lookup"><span data-stu-id="6985d-104">What is CORS?</span></span>
<span data-ttu-id="6985d-105">CORS (Cross Origin Resource Sharing；跨來源資源共用) 是一項 HTTP 功能，可讓在某個網域下執行的 Web 應用程式存取其他網域中的資源。</span><span class="sxs-lookup"><span data-stu-id="6985d-105">CORS (Cross Origin Resource Sharing) is an HTTP feature that enables a web application running under one domain to access resources in another domain.</span></span> <span data-ttu-id="6985d-106">為了減少跨網站指令碼攻擊的可能性，所有現代網頁瀏覽器都實作稱為 [Same-Origin Policy (同源原則)](http://www.w3.org/Security/wiki/Same_Origin_Policy)的安全性限制。</span><span class="sxs-lookup"><span data-stu-id="6985d-106">In order to reduce the possibility of cross-site scripting attacks, all modern web browsers implement a security restriction known as [same-origin policy](http://www.w3.org/Security/wiki/Same_Origin_Policy).</span></span>  <span data-ttu-id="6985d-107">這樣可以防止網頁呼叫其他網域中的 API。</span><span class="sxs-lookup"><span data-stu-id="6985d-107">This prevents a web page from calling APIs in a different domain.</span></span>  <span data-ttu-id="6985d-108">CORS 提供安全的方式來允許從一個來源 (來源網域) 呼叫其他來源中的 API。</span><span class="sxs-lookup"><span data-stu-id="6985d-108">CORS provides a secure way to allow one origin (the origin domain) to call APIs in another origin.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="6985d-109">運作方式</span><span class="sxs-lookup"><span data-stu-id="6985d-109">How it works</span></span>
<span data-ttu-id="6985d-110">CORS 要求有兩種類型，*簡單要求*和*複雜要求*。</span><span class="sxs-lookup"><span data-stu-id="6985d-110">There are two types of CORS requests, *simple requests* and *complex requests.*</span></span>

### <a name="for-simple-requests"></a><span data-ttu-id="6985d-111">對於簡單要求︰</span><span class="sxs-lookup"><span data-stu-id="6985d-111">For simple requests:</span></span>

1. <span data-ttu-id="6985d-112">瀏覽器會傳送有額外**來源** HTTP 要求標頭的 CORS 要求。</span><span class="sxs-lookup"><span data-stu-id="6985d-112">The browser sends the CORS request with an additional **Origin** HTTP request header.</span></span> <span data-ttu-id="6985d-113">此標頭的值是提供父頁面的來源，是以*通訊協定*、*網域*和*連接埠*的組合來定義的。</span><span class="sxs-lookup"><span data-stu-id="6985d-113">The value of this header is the origin that served the parent page, which is defined as the combination of *protocol,* *domain,* and *port.*</span></span>  <span data-ttu-id="6985d-114">當來自 https://www.contoso.com 的頁面嘗試存取位於 fabrikam.com 來源的使用者資料時，會將以下要求標頭傳送到 fabrikam.com：</span><span class="sxs-lookup"><span data-stu-id="6985d-114">When a page from https://www.contoso.com attempts to access a user's data in the fabrikam.com origin, the following request header would be sent to fabrikam.com:</span></span>

   `Origin: https://www.contoso.com`

2. <span data-ttu-id="6985d-115">該伺服器的回應可能是下列其中一項：</span><span class="sxs-lookup"><span data-stu-id="6985d-115">The server may respond with any of the following:</span></span>

   * <span data-ttu-id="6985d-116">回應中的 **Access-Control-Allow-Origin** 標頭指出所允許的來源網站。</span><span class="sxs-lookup"><span data-stu-id="6985d-116">An **Access-Control-Allow-Origin** header in its response indicating which origin site is allowed.</span></span> <span data-ttu-id="6985d-117">例如：</span><span class="sxs-lookup"><span data-stu-id="6985d-117">For example:</span></span>

     `Access-Control-Allow-Origin: https://www.contoso.com`

   * <span data-ttu-id="6985d-118">HTTP 錯誤碼 (例如 403)；如果伺服器在檢查 Origin 標頭之後，不允許跨來源要求，則會出現此錯誤碼</span><span class="sxs-lookup"><span data-stu-id="6985d-118">An HTTP error code such as 403 if the server does not allow the cross-origin request after checking the Origin header</span></span>

   * <span data-ttu-id="6985d-119">**Access-Control-Allow-Origin** 標頭包含允許所有來源的萬用字元：</span><span class="sxs-lookup"><span data-stu-id="6985d-119">An **Access-Control-Allow-Origin** header with a wildcard that allows all origins:</span></span>

     `Access-Control-Allow-Origin: *`

### <a name="for-complex-requests"></a><span data-ttu-id="6985d-120">對於複雜要求︰</span><span class="sxs-lookup"><span data-stu-id="6985d-120">For complex requests:</span></span>

<span data-ttu-id="6985d-121">複雜要求指的是瀏覽器在傳送實際 CORS 要求之前，必須先傳送*預檢要求* (也就是預備探查) 的 CORS 要求。</span><span class="sxs-lookup"><span data-stu-id="6985d-121">A complex request is a CORS request where the browser is required to send a *preflight request* (i.e. a preliminary probe) before sending the actual CORS request.</span></span> <span data-ttu-id="6985d-122">如果原始 CORS 可以處理，而且是對相同 URL 的 `OPTIONS` 要求，那麼預檢要求會要求伺服器權限。</span><span class="sxs-lookup"><span data-stu-id="6985d-122">The preflight request asks the server permission if the original CORS request can proceed and is an `OPTIONS` request to the same URL.</span></span>

> [!TIP]
> <span data-ttu-id="6985d-123">如需 CORS 流程和常見陷阱的詳細資訊，請參閱 [REST API 的 CORS 指南 (英文)](https://www.moesif.com/blog/technical/cors/Authoritative-Guide-to-CORS-Cross-Origin-Resource-Sharing-for-REST-APIs/)。</span><span class="sxs-lookup"><span data-stu-id="6985d-123">For more details on CORS flows and common pitfalls, view the [Guide to CORS for REST APIs](https://www.moesif.com/blog/technical/cors/Authoritative-Guide-to-CORS-Cross-Origin-Resource-Sharing-for-REST-APIs/).</span></span>
>
>

## <a name="wildcard-or-single-origin-scenarios"></a><span data-ttu-id="6985d-124">萬用字元或單一來源的狀況</span><span class="sxs-lookup"><span data-stu-id="6985d-124">Wildcard or single origin scenarios</span></span>
<span data-ttu-id="6985d-125">當 **Access-Control-Allow-Origin** 標頭設為萬用字元 (\*) 或單一來源時，Azure CDN 上的 CORS 不需要額外設定就會自動生效。</span><span class="sxs-lookup"><span data-stu-id="6985d-125">CORS on Azure CDN will work automatically with no additional configuration when the **Access-Control-Allow-Origin** header is set to wildcard (*) or a single origin.</span></span>  <span data-ttu-id="6985d-126">CDN 會快取第一個回應，且後續的要求將使用相同的標頭。</span><span class="sxs-lookup"><span data-stu-id="6985d-126">The CDN will cache the first response and subsequent requests will use the same header.</span></span>

<span data-ttu-id="6985d-127">如果在您的來源上設定 CORS 之前已經向 CDN 發出要求，您必須清除您端點內容上的內容，以重新載入包含 **Access-Control-Allow-Origin** 標頭的內容。</span><span class="sxs-lookup"><span data-stu-id="6985d-127">If requests have already been made to the CDN prior to CORS being set on the your origin, you will need to purge content on your endpoint content to reload the content with the **Access-Control-Allow-Origin** header.</span></span>

## <a name="multiple-origin-scenarios"></a><span data-ttu-id="6985d-128">多重來源的狀況</span><span class="sxs-lookup"><span data-stu-id="6985d-128">Multiple origin scenarios</span></span>
<span data-ttu-id="6985d-129">如果您要針對 CORS 允許使用特定清單中的來源，則會稍微複雜一點。</span><span class="sxs-lookup"><span data-stu-id="6985d-129">If you need to allow a specific list of origins to be allowed for CORS, things get a little more complicated.</span></span> <span data-ttu-id="6985d-130">問題會在 CDN 快取第一個 CORS 來源的 **Access-Control-Allow-Origin** 標頭時發生。</span><span class="sxs-lookup"><span data-stu-id="6985d-130">The problem occurs when the CDN caches the **Access-Control-Allow-Origin** header for the first CORS origin.</span></span>  <span data-ttu-id="6985d-131">當其他 CORS 來源發出後續要求時，CDN 會提供已快取的 **Access-Control-Allow-Origin** 標頭，而此標頭會不相符。</span><span class="sxs-lookup"><span data-stu-id="6985d-131">When a different CORS origin makes a subsequent request, the CDN will serve the cached **Access-Control-Allow-Origin** header, which won't match.</span></span>  <span data-ttu-id="6985d-132">有幾個方法可以修正此問題。</span><span class="sxs-lookup"><span data-stu-id="6985d-132">There are several ways to correct this.</span></span>

### <a name="azure-cdn-premium-from-verizon"></a><span data-ttu-id="6985d-133">來自 Verizon 的 Azure CDN 進階</span><span class="sxs-lookup"><span data-stu-id="6985d-133">Azure CDN Premium from Verizon</span></span>
<span data-ttu-id="6985d-134">完成此作業的最佳方法是使用「來自 Verizon 的 Azure CDN 進階」 ，它會公開一些進階功能。</span><span class="sxs-lookup"><span data-stu-id="6985d-134">The best way to enable this is to use **Azure CDN Premium from Verizon**, which exposes some advanced functionality.</span></span> 

<span data-ttu-id="6985d-135">您必須 [建立規則](cdn-rules-engine.md) 來檢查要求的 **Origin** 標頭。</span><span class="sxs-lookup"><span data-stu-id="6985d-135">You'll need to [create a rule](cdn-rules-engine.md) to check the **Origin** header on the request.</span></span>  <span data-ttu-id="6985d-136">如果是有效的來源，您的規則將使用要求中提供的來源設定 **Access-Control-Allow-Origin** 標頭。</span><span class="sxs-lookup"><span data-stu-id="6985d-136">If it's a valid origin, your rule will set the **Access-Control-Allow-Origin** header with the origin provided in the request.</span></span>  <span data-ttu-id="6985d-137">如果 **Origin** 中指定的來源是不允許的，您的規則應會忽略 **Access-Control-Allow-Origin** 標頭，這將導致瀏覽器拒絕要求。</span><span class="sxs-lookup"><span data-stu-id="6985d-137">If the origin specified in the **Origin** header is not allowed, your rule should omit the **Access-Control-Allow-Origin** header which will cause the browser to reject the request.</span></span> 

<span data-ttu-id="6985d-138">使用規則引擎來這樣做的方法有兩種。</span><span class="sxs-lookup"><span data-stu-id="6985d-138">There are two ways to do this with the rules engine.</span></span>  <span data-ttu-id="6985d-139">在這兩種情況下，會完全忽略來自檔案原始伺服器的 **Access-Control-Allow-Origin** 標頭，而允許的 CORS 來源會完全由 CDN 的規則引擎來管理。</span><span class="sxs-lookup"><span data-stu-id="6985d-139">In both cases, the **Access-Control-Allow-Origin** header from the file's origin server is completely ignored, the CDN's rules engine completely manages the allowed CORS origins.</span></span>

#### <a name="one-regular-expression-with-all-valid-origins"></a><span data-ttu-id="6985d-140">包含所有有效來源的規則運算式</span><span class="sxs-lookup"><span data-stu-id="6985d-140">One regular expression with all valid origins</span></span>
<span data-ttu-id="6985d-141">在此情況下，您會建立包含您要允許使用之所有來源的規則運算式。</span><span class="sxs-lookup"><span data-stu-id="6985d-141">In this case, you'll create a regular expression that includes all of the origins you want to allow:</span></span> 

    https?:\/\/(www\.contoso\.com|contoso\.com|www\.microsoft\.com|microsoft.com\.com)$

> [!TIP]
> <span data-ttu-id="6985d-142">**來自 Verizon 的 Azure CDN** 會使用 [Perl 相容的規則運算式](http://pcre.org/)做為其規則運算式的引擎。</span><span class="sxs-lookup"><span data-stu-id="6985d-142">**Azure CDN from Verizon** uses [Perl Compatible Regular Expressions](http://pcre.org/) as its engine for regular expressions.</span></span>  <span data-ttu-id="6985d-143">您可以使用像 [Regular Expressions 101](https://regex101.com/) 這樣的工具來驗證您的規則運算式。</span><span class="sxs-lookup"><span data-stu-id="6985d-143">You can use a tool like [Regular Expressions 101](https://regex101.com/) to validate your regular expression.</span></span>  <span data-ttu-id="6985d-144">請注意，規則運算式中的「/」字元是有效的，不需要逸出，不過將該字元逸出被視為是最佳做法，且某些規則運算式驗證程式也預期將它逸出。</span><span class="sxs-lookup"><span data-stu-id="6985d-144">Note that the "/" character is valid in regular expressions and doesn't need to be escaped, however, escaping that character is considered a best practice and is expected by some regex validators.</span></span>
> 
> 

<span data-ttu-id="6985d-145">如果規則運算式相符，您的規則會將來自來源的 **Access-Control-Allow-Origin** 標頭 (如果有) 取代為傳送該要求的來源。</span><span class="sxs-lookup"><span data-stu-id="6985d-145">If the regular expression matches, your rule will replace the **Access-Control-Allow-Origin** header (if any) from the origin with the origin that sent the request.</span></span>  <span data-ttu-id="6985d-146">您也可以加入額外的 CORS 標頭，例如 **Access-Control-Allow-Methods**。</span><span class="sxs-lookup"><span data-stu-id="6985d-146">You can also add additional CORS headers, such as **Access-Control-Allow-Methods**.</span></span>

![包含規則運算式的規則範例](./media/cdn-cors/cdn-cors-regex.png)

#### <a name="request-header-rule-for-each-origin"></a><span data-ttu-id="6985d-148">針對每個來源要求標頭規則</span><span class="sxs-lookup"><span data-stu-id="6985d-148">Request header rule for each origin.</span></span>
<span data-ttu-id="6985d-149">除了規則運算式之外，您也可以使用**要求標頭萬用字元**[比對條件](https://msdn.microsoft.com/library/mt757336.aspx#Anchor_1)，針對每個要允許的來源建立個別規則。</span><span class="sxs-lookup"><span data-stu-id="6985d-149">Rather than regular expressions, you can instead create a separate rule for each origin you wish to allow using the **Request Header Wildcard** [match condition](https://msdn.microsoft.com/library/mt757336.aspx#Anchor_1).</span></span> <span data-ttu-id="6985d-150">如同規則運算式方法一樣，也是僅由規則引擎設定 CORS 標頭。</span><span class="sxs-lookup"><span data-stu-id="6985d-150">As with the regular expression method, the rules engine alone sets the CORS headers.</span></span> 

![不含規則運算式的規則範例](./media/cdn-cors/cdn-cors-no-regex.png)

> [!TIP]
> <span data-ttu-id="6985d-152">在上述範例中，萬用字元 (*) 的作用是告訴規則引擎 HTTP 和 HTTPS 兩者都要比對。</span><span class="sxs-lookup"><span data-stu-id="6985d-152">In the example above, the use of the wildcard character * tells the rules engine to match both HTTP and HTTPS.</span></span>
> 
> 

### <a name="azure-cdn-standard"></a><span data-ttu-id="6985d-153">Azure CDN 標準</span><span class="sxs-lookup"><span data-stu-id="6985d-153">Azure CDN Standard</span></span>
<span data-ttu-id="6985d-154">在 Azure CDN 標準設定檔上，在不使用萬用字元來源情況下允許多重來源的唯一機制是使用 [查詢字串快取](cdn-query-string.md)。</span><span class="sxs-lookup"><span data-stu-id="6985d-154">On Azure CDN Standard profiles, the only mechanism to allow for multiple origins without the use of the wildcard origin is to use [query string caching](cdn-query-string.md).</span></span>  <span data-ttu-id="6985d-155">您需要啟用 CDN 端點的查詢字串設定，然後針對來自每個允許之網域的查詢使用唯一的查詢字串。</span><span class="sxs-lookup"><span data-stu-id="6985d-155">You need to enable query string setting for the CDN endpoint and then use a unique query string for requests from each allowed domain.</span></span> <span data-ttu-id="6985d-156">這樣做將使 CDN 針對每個唯一的查詢字串快取個別物件。</span><span class="sxs-lookup"><span data-stu-id="6985d-156">Doing this will result in the CDN caching a separate object for each unique query string.</span></span> <span data-ttu-id="6985d-157">但是這不是最理想的方法，因為它會導致在 CDN 上快取同一個檔案的多個複本。</span><span class="sxs-lookup"><span data-stu-id="6985d-157">This approach is not ideal, however, as it will result in multiple copies of the same file cached on the CDN.</span></span>  

