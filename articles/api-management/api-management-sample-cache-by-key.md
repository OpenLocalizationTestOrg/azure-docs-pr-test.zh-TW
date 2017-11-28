---
title: "aaaCustom 快取在 Azure API 管理"
description: "了解 toocache 在 Azure API 管理中的索引鍵的項目"
services: api-management
documentationcenter: 
author: darrelmiller
manager: erikre
editor: 
ms.assetid: 772bc8dd-5cda-41c4-95bf-b9f6f052bc85
ms.service: api-management
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 681380743c8c96af5d0a8e25948a8c0663e9fd35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="custom-caching-in-azure-api-management"></a><span data-ttu-id="be977-103">在 Azure API 管理中自訂快取</span><span class="sxs-lookup"><span data-stu-id="be977-103">Custom caching in Azure API Management</span></span>
<span data-ttu-id="be977-104">Azure API 管理服務已內建支援[快取 HTTP 回應](api-management-howto-cache.md)hello 索引鍵使用 hello 資源 URL。</span><span class="sxs-lookup"><span data-stu-id="be977-104">Azure API Management service has built-in support for [HTTP response caching](api-management-howto-cache.md) using hello resource URL as hello key.</span></span> <span data-ttu-id="be977-105">hello 金鑰就可以修改的要求標頭使用 hello`vary-by`屬性。</span><span class="sxs-lookup"><span data-stu-id="be977-105">hello key can be modified by request headers using hello `vary-by` properties.</span></span> <span data-ttu-id="be977-106">這適用於快取整個 HTTP 回應 （也稱為表示法），但有時候很有用的 toojust 快取的表示法的部分。</span><span class="sxs-lookup"><span data-stu-id="be977-106">This is useful for caching entire HTTP responses (aka representations), but sometimes it is useful toojust cache a portion of a representation.</span></span> <span data-ttu-id="be977-107">新的 hello[快取查閱值](https://msdn.microsoft.com/library/azure/dn894086.aspx#GetFromCacheByKey)和[快取存放區值](https://msdn.microsoft.com/library/azure/dn894086.aspx#StoreToCacheByKey)原則提供 hello 能力 toostore 並擷取任意內部原則定義的資料。</span><span class="sxs-lookup"><span data-stu-id="be977-107">hello new [cache-lookup-value](https://msdn.microsoft.com/library/azure/dn894086.aspx#GetFromCacheByKey) and [cache-store-value](https://msdn.microsoft.com/library/azure/dn894086.aspx#StoreToCacheByKey) policies provide hello ability toostore and retrieve arbitrary pieces of data from within policy definitions.</span></span> <span data-ttu-id="be977-108">這項功能也會將先前導入的值 toohello[傳送要求](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest)原則因為您現在可以快取從外部服務的回應。</span><span class="sxs-lookup"><span data-stu-id="be977-108">This ability also adds value toohello previously introduced [send-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) policy because you can now cache responses from external services.</span></span>

## <a name="architecture"></a><span data-ttu-id="be977-109">架構</span><span class="sxs-lookup"><span data-stu-id="be977-109">Architecture</span></span>
<span data-ttu-id="be977-110">API 管理服務會使用共用每個租用戶資料快取，以便為您 toomultiple 單位向上延展您仍可以存取 toohello 相同快取資料。</span><span class="sxs-lookup"><span data-stu-id="be977-110">API Management service uses a shared per-tenant data cache so that, as you scale up toomultiple units you will still get access toohello same cached data.</span></span> <span data-ttu-id="be977-111">不過，使用多區域部署時有個 hello 區域內的獨立快取。</span><span class="sxs-lookup"><span data-stu-id="be977-111">However, when working with a multi-region deployment there are independent caches within each of hello regions.</span></span> <span data-ttu-id="be977-112">到期 toothis，務必 toonot hello 快取視為資料存放區，其所在的部分資訊片段 hello 唯一來源。</span><span class="sxs-lookup"><span data-stu-id="be977-112">Due toothis, it is important toonot treat hello cache as a data store, where it is hello only source of some piece of information.</span></span> <span data-ttu-id="be977-113">如果您未，並稍後決定 tootake 優點 hello 多區域部署時，客戶與旅行的使用者可能會遺失存取 toothat 快取資料。</span><span class="sxs-lookup"><span data-stu-id="be977-113">If you did, and later decided tootake advantage of hello multi-region deployment, then customers with users that travel may lose access toothat cached data.</span></span>

## <a name="fragment-caching"></a><span data-ttu-id="be977-114">片段快取</span><span class="sxs-lookup"><span data-stu-id="be977-114">Fragment caching</span></span>
<span data-ttu-id="be977-115">有某些情況下，其中傳回的回應包含某些部分是高度耗費資源的 toodetermine，還會在合理的時間的保留全新的資料。</span><span class="sxs-lookup"><span data-stu-id="be977-115">There are certain cases where responses being returned contain some portion of data that is expensive toodetermine and yet remains fresh for a reasonable amount of time.</span></span> <span data-ttu-id="be977-116">以航空公司建立的服務為例，服務提供航班訂位、航班狀態等相關資訊。如果 hello 使用者所屬的 hello airlines 點程式，他們也會擁有與 tootheir 目前狀態和累積的里程數資訊。</span><span class="sxs-lookup"><span data-stu-id="be977-116">As an example, consider a service built by an airline that provides information relating flight reservations, flight status, etc. If hello user is a member of hello airlines points program, they would also have information relating tootheir current status and mileage accumulated.</span></span> <span data-ttu-id="be977-117">此使用者相關的資訊可能會儲存在不同的系統，但它可能會希望 tooinclude 它在回應中傳回有關航班狀態和保留項目。</span><span class="sxs-lookup"><span data-stu-id="be977-117">This user-related information might be stored in a different system, but it may be desirable tooinclude it in responses returned about flight status and reservations.</span></span> <span data-ttu-id="be977-118">這可以用稱為｢片段快取｣的程序做到。</span><span class="sxs-lookup"><span data-stu-id="be977-118">This can be done using a process called fragment caching.</span></span> <span data-ttu-id="be977-119">hello 主要的表示法可從傳回使用某種類型的語彙基元 tooindicate 其中 hello 與使用者相關的資訊插入 toobe hello 原始伺服器。</span><span class="sxs-lookup"><span data-stu-id="be977-119">hello primary representation can be returned from hello origin server using some kind of token tooindicate where hello user-related information is toobe inserted.</span></span> 

<span data-ttu-id="be977-120">請考慮下列 JSON 回應從後端應用程式開發介面的 hello。</span><span class="sxs-lookup"><span data-stu-id="be977-120">Consider hello following JSON response from a backend API.</span></span>

```json
{
  "airline" : "Air Canada",
  "flightno" : "871",
  "status" : "ontime",
  "gate" : "B40",
  "terminal" : "2A",
  "userprofile" : "$userprofile$"
}  
```

<span data-ttu-id="be977-121">在 `/userprofile/{userid}` 的次要資源看起來像，</span><span class="sxs-lookup"><span data-stu-id="be977-121">And secondary resource at `/userprofile/{userid}` that looks like,</span></span>

```json
{ "username" : "Bob Smith", "Status" : "Gold" }
```

<span data-ttu-id="be977-122">在訂單 toodetermine hello 適當的使用者資訊 tooinclude，我們需要 tooidentify hello 終端使用者是。</span><span class="sxs-lookup"><span data-stu-id="be977-122">In order toodetermine hello appropriate user information tooinclude, we need tooidentify who hello end user is.</span></span> <span data-ttu-id="be977-123">這個機制取決於實作。</span><span class="sxs-lookup"><span data-stu-id="be977-123">This mechanism is implementation dependent.</span></span> <span data-ttu-id="be977-124">例如，我使用 hello`Subject`宣告的`JWT`語彙基元。</span><span class="sxs-lookup"><span data-stu-id="be977-124">As an example, I am using hello `Subject` claim of a `JWT` token.</span></span> 

```xml
<set-variable
  name="enduserid"
  value="@(context.Request.Headers.GetValueOrDefault("Authorization","").Split(' ')[1].AsJwt()?.Subject)" />
```

<span data-ttu-id="be977-125">我們會將這個 `enduserid` 值儲存在內容變數中供稍後使用。</span><span class="sxs-lookup"><span data-stu-id="be977-125">We store this `enduserid` value in a context variable for later use.</span></span> <span data-ttu-id="be977-126">如果已擷取 hello 使用者資訊並儲存在 hello 快取中前一個要求，就 toodetermine hello 下一個步驟。</span><span class="sxs-lookup"><span data-stu-id="be977-126">hello next step is toodetermine if a previous request has already retrieved hello user information and stored it in hello cache.</span></span> <span data-ttu-id="be977-127">為此，我們使用 hello`cache-lookup-value`原則。</span><span class="sxs-lookup"><span data-stu-id="be977-127">For this we use hello `cache-lookup-value` policy.</span></span>

```xml
<cache-lookup-value
key="@("userprofile-" + context.Variables["enduserid"])"
variable-name="userprofile" />
```

<span data-ttu-id="be977-128">如果對應 toohello 索引鍵值，則否 hello 快取中沒有任何項目`userprofile`內容變數將會建立。</span><span class="sxs-lookup"><span data-stu-id="be977-128">If there is no entry in hello cache that corresponds toohello key value, then no `userprofile` context variable will be created.</span></span> <span data-ttu-id="be977-129">我們會檢查使用 hello hello 查閱 hello 成功`choose`控制流程原則。</span><span class="sxs-lookup"><span data-stu-id="be977-129">We check hello success of hello lookup using hello `choose` control flow policy.</span></span>

```xml
<choose>
    <when condition="@(!context.Variables.ContainsKey("userprofile"))">
        <!-- If hello userprofile context variable doesn’t exist, make an HTTP request tooretrieve it.  -->
    </when>
</choose>
```

<span data-ttu-id="be977-130">如果 hello`userprofile`內容變數不存在，則我們會持續 toohave toomake HTTP 要求 tooretrieve 它。</span><span class="sxs-lookup"><span data-stu-id="be977-130">If hello `userprofile` context variable doesn’t exist, then we are going toohave toomake an HTTP request tooretrieve it.</span></span>

```xml
<send-request
  mode="new"
  response-variable-name="userprofileresponse"
  timeout="10"
  ignore-error="true">

  <!-- Build a URL that points toohello profile for hello current end-user -->
  <set-url>@(new Uri(new Uri("https://apimairlineapi.azurewebsites.net/UserProfile/"),
      (string)context.Variables["enduserid"]).AbsoluteUri)
  </set-url>
  <set-method>GET</set-method>
</send-request>
```

<span data-ttu-id="be977-131">我們使用 hello `enduserid` tooconstruct hello URL toohello 使用者設定檔資源。</span><span class="sxs-lookup"><span data-stu-id="be977-131">We use hello `enduserid` tooconstruct hello URL toohello user profile resource.</span></span> <span data-ttu-id="be977-132">一旦 hello 回應，我們可以拉出 hello 回應 hello 本文文字，並將它儲存回內容變數。</span><span class="sxs-lookup"><span data-stu-id="be977-132">Once we have hello response, we can pull hello body text out of hello response and store it back into a context variable.</span></span>

```xml
<set-variable
    name="userprofile"
    value="@(((IResponse)context.Variables["userprofileresponse"]).Body.As<string>())" />
```

<span data-ttu-id="be977-133">tooavoid 我們需要 toomake 此 HTTP 要求，hello 相同的使用者發出另一個要求時，我們可以儲存 hello 使用者設定檔在 hello 快取中。</span><span class="sxs-lookup"><span data-stu-id="be977-133">tooavoid us having toomake this HTTP request again, when hello same user makes another request, we can store hello user profile in hello cache.</span></span>

```xml
<cache-store-value
    key="@("userprofile-" + context.Variables["enduserid"])"
    value="@((string)context.Variables["userprofile"])" duration="100000" />
```

<span data-ttu-id="be977-134">我們使用 hello 完全相同索引鍵我們原本嘗試 tooretrieve hello 快取中儲存 hello 值使用。</span><span class="sxs-lookup"><span data-stu-id="be977-134">We store hello value in hello cache using hello exact same key that we originally attempted tooretrieve it with.</span></span> <span data-ttu-id="be977-135">hello，我們選擇 toostore hello 值的持續時間應根據頻率 hello 資訊變更以及如何容錯被使用者 tooout 的日期資訊。</span><span class="sxs-lookup"><span data-stu-id="be977-135">hello duration that we choose toostore hello value should be based on how often hello information changes and how tolerant users are tooout of date information.</span></span> 

<span data-ttu-id="be977-136">重要 toorealize，從 hello 快取擷取仍然是跨處理序、 網路要求，並可能還是可以加入數十毫秒 toohello 要求。</span><span class="sxs-lookup"><span data-stu-id="be977-136">It is important toorealize that retrieving from hello cache is still an out-of-process, network request and potentially can still add tens of milliseconds toohello request.</span></span> <span data-ttu-id="be977-137">決定 hello 使用者設定檔資訊花的時間大幅多於，到期 tooneeding toodo 資料庫查詢或從多個後端的彙總資訊時，就會開始 hello 優點。</span><span class="sxs-lookup"><span data-stu-id="be977-137">hello benefits come when determining hello user profile information takes significantly longer than that due tooneeding toodo database queries or aggregate information from multiple back-ends.</span></span>

<span data-ttu-id="be977-138">hello hello 程序中的最後一個步驟是 tooupdate hello 傳回我們的使用者設定檔資訊的回應。</span><span class="sxs-lookup"><span data-stu-id="be977-138">hello final step in hello process is tooupdate hello returned response with our user profile information.</span></span>

```xml
<!-- Update response body with user profile-->
<find-and-replace
    from='"$userprofile$"'
    to="@((string)context.Variables["userprofile"])" />
```

<span data-ttu-id="be977-139">選取了 tooinclude hello 引號當成 hello token 的一部分，以便 hello 回應 hello 取代不會發生，即使是仍然有效的 JSON。</span><span class="sxs-lookup"><span data-stu-id="be977-139">I chose tooinclude hello quotation marks as part of hello token so that even when hello replace doesn’t occur, hello response was still valid JSON.</span></span> <span data-ttu-id="be977-140">這是主要 toomake 偵錯更容易。</span><span class="sxs-lookup"><span data-stu-id="be977-140">This was primarily toomake debugging easier.</span></span>

<span data-ttu-id="be977-141">一旦您將一起結合所有這些步驟，hello 最終結果會是看起來像 hello 下列其中一個原則。</span><span class="sxs-lookup"><span data-stu-id="be977-141">Once you combine all these steps together, hello end result is a policy that looks like hello following one.</span></span>

```xml
<policies>
    <inbound>
        <!-- How you determine user identity is application dependent -->
        <set-variable
          name="enduserid"
          value="@(context.Request.Headers.GetValueOrDefault("Authorization","").Split(' ')[1].AsJwt()?.Subject)" />

        <!--Look for userprofile for this user in hello cache -->
        <cache-lookup-value
          key="@("userprofile-" + context.Variables["enduserid"])"
          variable-name="userprofile" />

        <!-- If we don’t find it in hello cache, make a request for it and store it -->
        <choose>
            <when condition="@(!context.Variables.ContainsKey("userprofile"))">
                <!-- Make HTTP request tooget user profile -->
                <send-request
                  mode="new"
                  response-variable-name="userprofileresponse"
                  timeout="10"
                  ignore-error="true">

                   <!-- Build a URL that points toohello profile for hello current end-user -->
                    <set-url>@(new Uri(new Uri("https://apimairlineapi.azurewebsites.net/UserProfile/"),(string)context.Variables["enduserid"]).AbsoluteUri)</set-url>
                    <set-method>GET</set-method>
                </send-request>

                <!-- Store response body in context variable -->
                <set-variable
                  name="userprofile"
                  value="@(((IResponse)context.Variables["userprofileresponse"]).Body.As<string>())" />

                <!-- Store result in cache -->
                <cache-store-value
                  key="@("userprofile-" + context.Variables["enduserid"])"
                  value="@((string)context.Variables["userprofile"])"
                  duration="100000" />
            </when>
        </choose>
        <base />
    </inbound>
    <outbound>
        <!-- Update response body with user profile-->
        <find-and-replace
              from='"$userprofile$"'
              to="@((string)context.Variables["userprofile"])" />
        <base />
    </outbound>
</policies>
```

<span data-ttu-id="be977-142">此快取的方法主要使用在網站中，HTML 組成 hello 伺服器端上，讓它可以轉譯成單一頁面。</span><span class="sxs-lookup"><span data-stu-id="be977-142">This caching approach is primarily used in web sites where HTML is composed on hello server side so that it can be rendered as a single page.</span></span> <span data-ttu-id="be977-143">不過，它也可以用於應用程式開發介面，用戶端無法執行動作用戶端端 HTTP 快取，或最好不 tooput hello 用戶端上的該項責任。</span><span class="sxs-lookup"><span data-stu-id="be977-143">However, it can also be useful in APIs where clients cannot do client side HTTP caching or it is desirable not tooput that responsibility on hello client.</span></span>

<span data-ttu-id="be977-144">此同類的片段快取也可以透過使用 Redis 快取伺服器 hello 後端 web 伺服器上，不過，使用 hello API 管理服務 tooperform 這項工作時，快取的 hello 片段來自不同的後端比 hello主要的回應。</span><span class="sxs-lookup"><span data-stu-id="be977-144">This same kind of fragment caching can also be done on hello backend web servers using a Redis caching server, however, using hello API Management service tooperform this work is useful when hello cached fragments are coming from different back-ends than hello primary responses.</span></span>

## <a name="transparent-versioning"></a><span data-ttu-id="be977-145">透明的版本設定</span><span class="sxs-lookup"><span data-stu-id="be977-145">Transparent versioning</span></span>
<span data-ttu-id="be977-146">一般作法是讓多個不同的實作版本支援在任何時候 API toobe。</span><span class="sxs-lookup"><span data-stu-id="be977-146">It is common practice for multiple different implementation versions of an API toobe supported at any one time.</span></span> <span data-ttu-id="be977-147">這可能是 toosupport 不同環境，例如開發、 測試、 生產等，或者可能是 toosupport API 取用者 toomigrate toonewer 版本 hello API toogive 時間的較舊的版本。</span><span class="sxs-lookup"><span data-stu-id="be977-147">This is perhaps toosupport different environments, like dev, test, production, etc, or it may be toosupport older versions of hello API toogive time for API consumers toomigrate toonewer versions.</span></span> 

<span data-ttu-id="be977-148">此改為需要從用戶端開發人員 toochange hello Url 的其中一個方法 toohandling`/v1/customers`太`/v2/customers`也無需 toostore hello 取用者的設定檔資料中的 hello API 版本他們目前想 toouse 呼叫適當的 hello後端 URL。</span><span class="sxs-lookup"><span data-stu-id="be977-148">One approach toohandling this instead of requiring client developers toochange hello URLs from `/v1/customers` too`/v2/customers` is toostore in hello consumer’s profile data which version of hello API they currently wish toouse and call hello appropriate backend URL.</span></span> <span data-ttu-id="be977-149">在訂單 toodetermine hello 正確的後端 URL toocall 特定用戶端，就需要 tooquery 某些組態資料。</span><span class="sxs-lookup"><span data-stu-id="be977-149">In order toodetermine hello correct backend URL toocall for a particular client, it is necessary tooquery some configuration data.</span></span> <span data-ttu-id="be977-150">藉由快取此設定資料，我們可以最小化 hello 執行這項執行此查詢的效能帶來負面影響。</span><span class="sxs-lookup"><span data-stu-id="be977-150">By caching this configuration data, we can minimize hello performance penalty of doing this lookup.</span></span>

<span data-ttu-id="be977-151">hello 第一個步驟是 toodetermine hello 識別項使用 tooconfigure hello 所需的版本。</span><span class="sxs-lookup"><span data-stu-id="be977-151">hello first step is toodetermine hello identifier used tooconfigure hello desired version.</span></span> <span data-ttu-id="be977-152">在此範例中，選取了 tooassociate hello 版本 toohello 產品訂用帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="be977-152">In this example, I chose tooassociate hello version toohello product subscription key.</span></span> 

```xml
<set-variable name="clientid" value="@(context.Subscription.Key)" />
```

<span data-ttu-id="be977-153">我們接著執行快取查閱 toosee，如果我們已經有擷取 hello 所需的用戶端版本。</span><span class="sxs-lookup"><span data-stu-id="be977-153">We then do a cache lookup toosee if we already have retrieved hello desired client version.</span></span>

```xml
<cache-lookup-value
key="@("clientversion-" + context.Variables["clientid"])"
variable-name="clientversion" />
```

<span data-ttu-id="be977-154">然後我們會檢查 toosee 如果我們找不到它在 hello 快取中。</span><span class="sxs-lookup"><span data-stu-id="be977-154">Then we check toosee if we did not find it in hello cache.</span></span>

```xml
<choose>
    <when condition="@(!context.Variables.ContainsKey("clientversion"))">
```

<span data-ttu-id="be977-155">如果沒有，就去擷取它。</span><span class="sxs-lookup"><span data-stu-id="be977-155">If we didn’t then we go and retrieve it.</span></span>

```xml
<send-request
    mode="new"
    response-variable-name="clientconfiguresponse"
    timeout="10"
    ignore-error="true">
            <set-url>@(new Uri(new Uri(context.Api.ServiceUrl.ToString() + "api/ClientConfig/"),(string)context.Variables["clientid"]).AbsoluteUri)</set-url>
            <set-method>GET</set-method>
</send-request>
```

<span data-ttu-id="be977-156">擷取 hello 回應 hello 回應本文文字。</span><span class="sxs-lookup"><span data-stu-id="be977-156">Extract hello response body text from hello response.</span></span>

```xml
<set-variable
      name="clientversion"
      value="@(((IResponse)context.Variables["clientconfiguresponse"]).Body.As<string>())" />
```

<span data-ttu-id="be977-157">請將它儲存回在 hello 快取供未來使用。</span><span class="sxs-lookup"><span data-stu-id="be977-157">Store it back in hello cache for future use.</span></span>

```xml
<cache-store-value
      key="@("clientversion-" + context.Variables["clientid"])"
      value="@((string)context.Variables["clientversion"])"
      duration="100000" />
```

<span data-ttu-id="be977-158">與最後更新 hello 後端 URL tooselect hello 版本 hello hello 用戶端所需的服務。</span><span class="sxs-lookup"><span data-stu-id="be977-158">And finally update hello back-end URL tooselect hello version of hello service desired by hello client.</span></span>

```xml
<set-backend-service
      base-url="@(context.Api.ServiceUrl.ToString() + "api/" + (string)context.Variables["clientversion"] + "/")" />
```

<span data-ttu-id="be977-159">hello 完全原則如下所示。</span><span class="sxs-lookup"><span data-stu-id="be977-159">hello completely policy is as follows.</span></span>

```xml
<inbound>
    <base />
    <set-variable name="clientid" value="@(context.Subscription.Key)" />
    <cache-lookup-value key="@("clientversion-" + context.Variables["clientid"])" variable-name="clientversion" />

    <!-- If we don’t find it in hello cache, make a request for it and store it -->
    <choose>
        <when condition="@(!context.Variables.ContainsKey("clientversion"))">
            <send-request mode="new" response-variable-name="clientconfiguresponse" timeout="10" ignore-error="true">
                <set-url>@(new Uri(new Uri(context.Api.ServiceUrl.ToString() + "api/ClientConfig/"),(string)context.Variables["clientid"]).AbsoluteUri)</set-url>
                <set-method>GET</set-method>
            </send-request>
            <!-- Store response body in context variable -->
            <set-variable name="clientversion" value="@(((IResponse)context.Variables["clientconfiguresponse"]).Body.As<string>())" />
            <!-- Store result in cache -->
            <cache-store-value key="@("clientversion-" + context.Variables["clientid"])" value="@((string)context.Variables["clientversion"])" duration="100000" />
        </when>
    </choose>
    <set-backend-service base-url="@(context.Api.ServiceUrl.ToString() + "api/" + (string)context.Variables["clientversion"] + "/")" />
</inbound>
```

<span data-ttu-id="be977-160">啟用後端版本由用戶端不需要 tooupdate 和重新部署用戶端存取 API 取用者 tootransparently 控制是一種精緻的解決方案，解決許多應用程式開發介面版本設定問題。</span><span class="sxs-lookup"><span data-stu-id="be977-160">Enabling API consumers tootransparently control which backend version is being accessed by clients without having tooupdate and redeploy clients is a elegant solution that addresses many API versioning concerns.</span></span>

## <a name="tenant-isolation"></a><span data-ttu-id="be977-161">租用戶隔離</span><span class="sxs-lookup"><span data-stu-id="be977-161">Tenant Isolation</span></span>
<span data-ttu-id="be977-162">在大型、多租用戶的部署中，有些公司會在後端硬體的不同部署上建立不同的租用戶群組。</span><span class="sxs-lookup"><span data-stu-id="be977-162">In larger, multi-tenant deployments some companies create separate groups of tenants on distinct deployments of backend hardware.</span></span> <span data-ttu-id="be977-163">這會將 hello hello 後端上的硬體問題所影響的客戶數目降到最低。</span><span class="sxs-lookup"><span data-stu-id="be977-163">This minimizes hello number of customers who are impacted by a hardware issue on hello backend.</span></span> <span data-ttu-id="be977-164">它也可讓新的軟體版本 toobe 階段中推出。</span><span class="sxs-lookup"><span data-stu-id="be977-164">It also enables new software versions toobe rolled out in stages.</span></span> <span data-ttu-id="be977-165">在理想情況下這個後端架構應該是透明的 tooAPI 取用者。</span><span class="sxs-lookup"><span data-stu-id="be977-165">Ideally this backend architecture should be transparent tooAPI consumers.</span></span> <span data-ttu-id="be977-166">這可以來達成類似的方式 tootransparent 版本控制中因為它根據 hello 操作 hello 後端 URL 使用每個應用程式開發介面的索引鍵的設定狀態的相同技巧。</span><span class="sxs-lookup"><span data-stu-id="be977-166">This can be achieved in a similar way tootransparent versioning because it is based on hello same technique of manipulating hello backend URL using configuration state per API key.</span></span>  

<span data-ttu-id="be977-167">而不是傳回 hello API 的每個訂用帳戶金鑰的慣用的版本，您將會傳回有關租用戶指派 toohello 硬體群組識別項。</span><span class="sxs-lookup"><span data-stu-id="be977-167">Instead of returning a preferred version of hello API for each subscription key, you would return an identifier that relates a tenant toohello assigned hardware group.</span></span> <span data-ttu-id="be977-168">該識別碼可以是使用的 tooconstruct hello 適當的後端 URL。</span><span class="sxs-lookup"><span data-stu-id="be977-168">That identifier can be used tooconstruct hello appropriate backend URL.</span></span>

## <a name="summary"></a><span data-ttu-id="be977-169">摘要</span><span class="sxs-lookup"><span data-stu-id="be977-169">Summary</span></span>
<span data-ttu-id="be977-170">hello 自由 toouse hello Azure API 管理快取來儲存任何種類的資料可讓您能夠有效率地存取 tooconfiguration 資料可能會影響 hello 方式處理傳入的要求。</span><span class="sxs-lookup"><span data-stu-id="be977-170">hello freedom toouse hello Azure API management cache for storing any kind of data enables efficient access tooconfiguration data that can affect hello way an inbound request is processed.</span></span> <span data-ttu-id="be977-171">它也可以使用的 toostore 資料片段可以擴大從後端 API 傳回的回應。</span><span class="sxs-lookup"><span data-stu-id="be977-171">It can also be used toostore data fragments that can augment responses, returned from a backend API.</span></span>

## <a name="next-steps"></a><span data-ttu-id="be977-172">後續步驟</span><span class="sxs-lookup"><span data-stu-id="be977-172">Next steps</span></span>
<span data-ttu-id="be977-173">請提供您的意見 hello Disqus 執行緒中取得此主題是否有目前可能會有這些原則已啟用，或如果沒有案例希望 tooachieve，但不要覺得其他案例。</span><span class="sxs-lookup"><span data-stu-id="be977-173">Please give us your feedback in hello Disqus thread for this topic if there are other scenarios that these policies have enabled for you, or if there are scenarios you would like tooachieve but do not feel are currently possible.</span></span>

