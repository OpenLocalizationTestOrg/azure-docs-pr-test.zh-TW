---
title: "Azure CDN 與 CORS aaaUsing |Microsoft 文件"
description: "了解如何 toouse hello Azure 內容傳遞網路 (CDN) toowith 跨原始資源共用 (CORS)。"
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
ms.openlocfilehash: 6c743b56c32a2d3aacc9a77094cb87d61b95d2f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-cdn-with-cors"></a><span data-ttu-id="351ad-103">搭配 CORS 使用 Azure CDN</span><span class="sxs-lookup"><span data-stu-id="351ad-103">Using Azure CDN with CORS</span></span>
## <a name="what-is-cors"></a><span data-ttu-id="351ad-104">CORS 是什麼？</span><span class="sxs-lookup"><span data-stu-id="351ad-104">What is CORS?</span></span>
<span data-ttu-id="351ad-105">CORS （跨原始資源共用） 是一種 HTTP 功能，可讓 web 應用程式執行另一個網域中的下一個網域 tooaccess 資源。</span><span class="sxs-lookup"><span data-stu-id="351ad-105">CORS (Cross Origin Resource Sharing) is an HTTP feature that enables a web application running under one domain tooaccess resources in another domain.</span></span> <span data-ttu-id="351ad-106">在訂單 tooreduce hello 跨網站指令碼攻擊的可能性，所有現代化 web 瀏覽器實作稱為安全性限制[相同來源原則](http://www.w3.org/Security/wiki/Same_Origin_Policy)。</span><span class="sxs-lookup"><span data-stu-id="351ad-106">In order tooreduce hello possibility of cross-site scripting attacks, all modern web browsers implement a security restriction known as [same-origin policy](http://www.w3.org/Security/wiki/Same_Origin_Policy).</span></span>  <span data-ttu-id="351ad-107">這樣可以防止網頁呼叫其他網域中的 API。</span><span class="sxs-lookup"><span data-stu-id="351ad-107">This prevents a web page from calling APIs in a different domain.</span></span>  <span data-ttu-id="351ad-108">CORS 提供安全的方式 tooallow 一個原始主機 （hello 原始網域） toocall 應用程式開發介面中另一個來源。</span><span class="sxs-lookup"><span data-stu-id="351ad-108">CORS provides a secure way tooallow one origin (hello origin domain) toocall APIs in another origin.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="351ad-109">運作方式</span><span class="sxs-lookup"><span data-stu-id="351ad-109">How it works</span></span>
<span data-ttu-id="351ad-110">CORS 要求有兩種類型，*簡單要求*和*複雜要求*。</span><span class="sxs-lookup"><span data-stu-id="351ad-110">There are two types of CORS requests, *simple requests* and *complex requests.*</span></span>

### <a name="for-simple-requests"></a><span data-ttu-id="351ad-111">對於簡單要求︰</span><span class="sxs-lookup"><span data-stu-id="351ad-111">For simple requests:</span></span>

1. <span data-ttu-id="351ad-112">hello 瀏覽器傳送 hello CORS 要求具有其他**原點**HTTP 要求標頭。</span><span class="sxs-lookup"><span data-stu-id="351ad-112">hello browser sends hello CORS request with an additional **Origin** HTTP request header.</span></span> <span data-ttu-id="351ad-113">此標頭的 hello 值是服務的定義為 hello 組合 hello 父系分頁的 hello 原點*通訊協定，* *網域*和*連接埠。*</span><span class="sxs-lookup"><span data-stu-id="351ad-113">hello value of this header is hello origin that served hello parent page, which is defined as hello combination of *protocol,* *domain,* and *port.*</span></span>  <span data-ttu-id="351ad-114">當頁面從 https://www.contoso.com 嘗試 tooaccess hello fabrikam.com 原點中的使用者資料時，下列要求標頭的 hello 就會傳送 toofabrikam.com:</span><span class="sxs-lookup"><span data-stu-id="351ad-114">When a page from https://www.contoso.com attempts tooaccess a user's data in hello fabrikam.com origin, hello following request header would be sent toofabrikam.com:</span></span>

   `Origin: https://www.contoso.com`

2. <span data-ttu-id="351ad-115">hello 伺服器可能回應 hello 下列任何一項：</span><span class="sxs-lookup"><span data-stu-id="351ad-115">hello server may respond with any of hello following:</span></span>

   * <span data-ttu-id="351ad-116">回應中的 **Access-Control-Allow-Origin** 標頭指出所允許的來源網站。</span><span class="sxs-lookup"><span data-stu-id="351ad-116">An **Access-Control-Allow-Origin** header in its response indicating which origin site is allowed.</span></span> <span data-ttu-id="351ad-117">例如：</span><span class="sxs-lookup"><span data-stu-id="351ad-117">For example:</span></span>

     `Access-Control-Allow-Origin: https://www.contoso.com`

   * <span data-ttu-id="351ad-118">HTTP 錯誤碼 403 例如如果 hello 伺服器不允許檢查 hello Origin 標頭之後的 hello 跨原始要求</span><span class="sxs-lookup"><span data-stu-id="351ad-118">An HTTP error code such as 403 if hello server does not allow hello cross-origin request after checking hello Origin header</span></span>

   * <span data-ttu-id="351ad-119">**Access-Control-Allow-Origin** 標頭包含允許所有來源的萬用字元：</span><span class="sxs-lookup"><span data-stu-id="351ad-119">An **Access-Control-Allow-Origin** header with a wildcard that allows all origins:</span></span>

     `Access-Control-Allow-Origin: *`

### <a name="for-complex-requests"></a><span data-ttu-id="351ad-120">對於複雜要求︰</span><span class="sxs-lookup"><span data-stu-id="351ad-120">For complex requests:</span></span>

<span data-ttu-id="351ad-121">複雜的要求是 CORS 要求其中 hello 瀏覽器需要的 toosend*預檢要求*（也就是初步探查） 傳送嗨實際 CORS 要求之前。</span><span class="sxs-lookup"><span data-stu-id="351ad-121">A complex request is a CORS request where hello browser is required toosend a *preflight request* (i.e. a preliminary probe) before sending hello actual CORS request.</span></span> <span data-ttu-id="351ad-122">hello 預檢要求會要求 hello server 權限是否 hello 原始 CORS 要求可以繼續執行，且未`OPTIONS`要求 toohello 相同的 URL。</span><span class="sxs-lookup"><span data-stu-id="351ad-122">hello preflight request asks hello server permission if hello original CORS request can proceed and is an `OPTIONS` request toohello same URL.</span></span>

> [!TIP]
> <span data-ttu-id="351ad-123">如需有關 CORS 流程和常見的問題的詳細資訊，請檢視 hello [REST api 引導 tooCORS](https://www.moesif.com/blog/technical/cors/Authoritative-Guide-to-CORS-Cross-Origin-Resource-Sharing-for-REST-APIs/)。</span><span class="sxs-lookup"><span data-stu-id="351ad-123">For more details on CORS flows and common pitfalls, view hello [Guide tooCORS for REST APIs](https://www.moesif.com/blog/technical/cors/Authoritative-Guide-to-CORS-Cross-Origin-Resource-Sharing-for-REST-APIs/).</span></span>
>
>

## <a name="wildcard-or-single-origin-scenarios"></a><span data-ttu-id="351ad-124">萬用字元或單一來源的狀況</span><span class="sxs-lookup"><span data-stu-id="351ad-124">Wildcard or single origin scenarios</span></span>
<span data-ttu-id="351ad-125">在 Azure CDN 的 CORS 會自動運作，不需要額外的組態時 hello**存取控制-允許-原始**toowildcard （*） 或單一來源，設定標頭。</span><span class="sxs-lookup"><span data-stu-id="351ad-125">CORS on Azure CDN will work automatically with no additional configuration when hello **Access-Control-Allow-Origin** header is set toowildcard (*) or a single origin.</span></span>  <span data-ttu-id="351ad-126">hello CDN 將會快取 hello 第一個回應，且後續要求將會使用 hello 相同的標頭。</span><span class="sxs-lookup"><span data-stu-id="351ad-126">hello CDN will cache hello first response and subsequent requests will use hello same header.</span></span>

<span data-ttu-id="351ad-127">如果要求已完成您的原點 hello 上會設定 toohello CDN 先前 tooCORS，您將需要 toopurge 內容上您的端點內容 tooreload hello 內容以 hello**存取控制-允許-原始**標頭。</span><span class="sxs-lookup"><span data-stu-id="351ad-127">If requests have already been made toohello CDN prior tooCORS being set on hello your origin, you will need toopurge content on your endpoint content tooreload hello content with hello **Access-Control-Allow-Origin** header.</span></span>

## <a name="multiple-origin-scenarios"></a><span data-ttu-id="351ad-128">多重來源的狀況</span><span class="sxs-lookup"><span data-stu-id="351ad-128">Multiple origin scenarios</span></span>
<span data-ttu-id="351ad-129">如果您需要 tooallow origins toobe CORS 所允許的特定清單，事情就得較複雜。</span><span class="sxs-lookup"><span data-stu-id="351ad-129">If you need tooallow a specific list of origins toobe allowed for CORS, things get a little more complicated.</span></span> <span data-ttu-id="351ad-130">hello 問題發生於 hello CDN 快取 hello**存取控制-允許-原始**hello 第一個 CORS 原始的標頭。</span><span class="sxs-lookup"><span data-stu-id="351ad-130">hello problem occurs when hello CDN caches hello **Access-Control-Allow-Origin** header for hello first CORS origin.</span></span>  <span data-ttu-id="351ad-131">Hello CDN 時不同的 CORS 原始後續要求，將服務快取的 hello**存取控制-允許-原始**標頭，並不相符。</span><span class="sxs-lookup"><span data-stu-id="351ad-131">When a different CORS origin makes a subsequent request, hello CDN will serve hello cached **Access-Control-Allow-Origin** header, which won't match.</span></span>  <span data-ttu-id="351ad-132">有數種方式 toocorrect 這。</span><span class="sxs-lookup"><span data-stu-id="351ad-132">There are several ways toocorrect this.</span></span>

### <a name="azure-cdn-premium-from-verizon"></a><span data-ttu-id="351ad-133">來自 Verizon 的 Azure CDN 進階</span><span class="sxs-lookup"><span data-stu-id="351ad-133">Azure CDN Premium from Verizon</span></span>
<span data-ttu-id="351ad-134">hello 最佳方式 tooenable 這是 toouse **Verizon 從 Azure CDN Premium**，而這會公開一些進階功能。</span><span class="sxs-lookup"><span data-stu-id="351ad-134">hello best way tooenable this is toouse **Azure CDN Premium from Verizon**, which exposes some advanced functionality.</span></span> 

<span data-ttu-id="351ad-135">您必須太[建立規則](cdn-rules-engine.md)toocheck hello**原點**hello 要求標頭。</span><span class="sxs-lookup"><span data-stu-id="351ad-135">You'll need too[create a rule](cdn-rules-engine.md) toocheck hello **Origin** header on hello request.</span></span>  <span data-ttu-id="351ad-136">如果它是有效的來源，您的規則將會設定 hello**存取控制-允許-原始**hello 要求中提供的 hello origin 標頭。</span><span class="sxs-lookup"><span data-stu-id="351ad-136">If it's a valid origin, your rule will set hello **Access-Control-Allow-Origin** header with hello origin provided in hello request.</span></span>  <span data-ttu-id="351ad-137">如果在 hello 指定 hello 原點**原點**標頭不允許，您的規則應該省略 hello**存取控制-允許-原始**這會導致 hello 瀏覽器 tooreject hello 要求標頭。</span><span class="sxs-lookup"><span data-stu-id="351ad-137">If hello origin specified in hello **Origin** header is not allowed, your rule should omit hello **Access-Control-Allow-Origin** header which will cause hello browser tooreject hello request.</span></span> 

<span data-ttu-id="351ad-138">有兩種方式 toodo 這與 hello 規則引擎。</span><span class="sxs-lookup"><span data-stu-id="351ad-138">There are two ways toodo this with hello rules engine.</span></span>  <span data-ttu-id="351ad-139">在這兩種情況下，hello**存取控制-允許-原始**從 hello 檔案的原始伺服器的標頭會完全忽略，hello CDN 規則引擎便會完全管理 hello 允許出處 CORS。</span><span class="sxs-lookup"><span data-stu-id="351ad-139">In both cases, hello **Access-Control-Allow-Origin** header from hello file's origin server is completely ignored, hello CDN's rules engine completely manages hello allowed CORS origins.</span></span>

#### <a name="one-regular-expression-with-all-valid-origins"></a><span data-ttu-id="351ad-140">包含所有有效來源的規則運算式</span><span class="sxs-lookup"><span data-stu-id="351ad-140">One regular expression with all valid origins</span></span>
<span data-ttu-id="351ad-141">在此情況下，您將建立規則運算式，其中包含所有 hello origins 想 tooallow:</span><span class="sxs-lookup"><span data-stu-id="351ad-141">In this case, you'll create a regular expression that includes all of hello origins you want tooallow:</span></span> 

    https?:\/\/(www\.contoso\.com|contoso\.com|www\.microsoft\.com|microsoft.com\.com)$

> [!TIP]
> <span data-ttu-id="351ad-142">**來自 Verizon 的 Azure CDN** 會使用 [Perl 相容的規則運算式](http://pcre.org/)做為其規則運算式的引擎。</span><span class="sxs-lookup"><span data-stu-id="351ad-142">**Azure CDN from Verizon** uses [Perl Compatible Regular Expressions](http://pcre.org/) as its engine for regular expressions.</span></span>  <span data-ttu-id="351ad-143">您可以使用這類工具[規則運算式 101](https://regex101.com/) toovalidate 規則運算式。</span><span class="sxs-lookup"><span data-stu-id="351ad-143">You can use a tool like [Regular Expressions 101](https://regex101.com/) toovalidate your regular expression.</span></span>  <span data-ttu-id="351ad-144">請注意，hello"/"字元在規則運算式中有效，而且不需要逸出 toobe，不過，逸出該字元會被視為最佳作法和某些 regex 驗證程式所預期的。</span><span class="sxs-lookup"><span data-stu-id="351ad-144">Note that hello "/" character is valid in regular expressions and doesn't need toobe escaped, however, escaping that character is considered a best practice and is expected by some regex validators.</span></span>
> 
> 

<span data-ttu-id="351ad-145">Hello 規則運算式比對，如果您的規則將會取代 hello**存取控制-允許-原始**與 hello 要求傳送嗨原點的 hello 原始標題 （如果有的話）。</span><span class="sxs-lookup"><span data-stu-id="351ad-145">If hello regular expression matches, your rule will replace hello **Access-Control-Allow-Origin** header (if any) from hello origin with hello origin that sent hello request.</span></span>  <span data-ttu-id="351ad-146">您也可以加入額外的 CORS 標頭，例如 **Access-Control-Allow-Methods**。</span><span class="sxs-lookup"><span data-stu-id="351ad-146">You can also add additional CORS headers, such as **Access-Control-Allow-Methods**.</span></span>

![包含規則運算式的規則範例](./media/cdn-cors/cdn-cors-regex.png)

#### <a name="request-header-rule-for-each-origin"></a><span data-ttu-id="351ad-148">針對每個來源要求標頭規則</span><span class="sxs-lookup"><span data-stu-id="351ad-148">Request header rule for each origin.</span></span>
<span data-ttu-id="351ad-149">而不是規則運算式中，您可以改為建立個別的每個來源規則您想使用 hello tooallow**要求標頭萬用字元**[符合條件](https://msdn.microsoft.com/library/mt757336.aspx#Anchor_1)。</span><span class="sxs-lookup"><span data-stu-id="351ad-149">Rather than regular expressions, you can instead create a separate rule for each origin you wish tooallow using hello **Request Header Wildcard** [match condition](https://msdn.microsoft.com/library/mt757336.aspx#Anchor_1).</span></span> <span data-ttu-id="351ad-150">為使用 hello 規則運算式方法時，hello 規則引擎單獨集 hello CORS 標頭。</span><span class="sxs-lookup"><span data-stu-id="351ad-150">As with hello regular expression method, hello rules engine alone sets hello CORS headers.</span></span> 

![不含規則運算式的規則範例](./media/cdn-cors/cdn-cors-no-regex.png)

> [!TIP]
> <span data-ttu-id="351ad-152">Hello 上述範例中，在 hello hello 萬用字元使用 * 告訴 hello 規則引擎 toomatch HTTP 和 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="351ad-152">In hello example above, hello use of hello wildcard character * tells hello rules engine toomatch both HTTP and HTTPS.</span></span>
> 
> 

### <a name="azure-cdn-standard"></a><span data-ttu-id="351ad-153">Azure CDN 標準</span><span class="sxs-lookup"><span data-stu-id="351ad-153">Azure CDN Standard</span></span>
<span data-ttu-id="351ad-154">在 Azure CDN 標準設定檔，hello 只有多個來源，而不需 hello hello 萬用字元原點使用的機制 tooallow toouse[查詢字串快取](cdn-query-string.md)。</span><span class="sxs-lookup"><span data-stu-id="351ad-154">On Azure CDN Standard profiles, hello only mechanism tooallow for multiple origins without hello use of hello wildcard origin is toouse [query string caching](cdn-query-string.md).</span></span>  <span data-ttu-id="351ad-155">您要 hello CDN 端點 tooenable 查詢字串設定，以及接著要求從每個允許的網域使用唯一的查詢字串。</span><span class="sxs-lookup"><span data-stu-id="351ad-155">You need tooenable query string setting for hello CDN endpoint and then use a unique query string for requests from each allowed domain.</span></span> <span data-ttu-id="351ad-156">如此一來，將會導致 hello CDN 快取每個唯一的查詢字串的個別物件。</span><span class="sxs-lookup"><span data-stu-id="351ad-156">Doing this will result in hello CDN caching a separate object for each unique query string.</span></span> <span data-ttu-id="351ad-157">這個方法並不理想，不過，因為它會導致多個副本 hello 相同檔案快取上 hello CDN。</span><span class="sxs-lookup"><span data-stu-id="351ad-157">This approach is not ideal, however, as it will result in multiple copies of hello same file cached on hello CDN.</span></span>  

