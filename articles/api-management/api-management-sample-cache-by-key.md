---
title: "在 Azure API 管理中自訂快取"
description: "了解如何在 Azure API 管理中依索引鍵快取項目"
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
ms.openlocfilehash: f5d5f44e34fbcd122a10be0ca5b3001760c4c64d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="custom-caching-in-azure-api-management"></a><span data-ttu-id="8db65-103">在 Azure API 管理中自訂快取</span><span class="sxs-lookup"><span data-stu-id="8db65-103">Custom caching in Azure API Management</span></span>
<span data-ttu-id="8db65-104">Azure API 管理服務以資源 URL 做為索引鍵，內建對 [HTTP 回應的快取](api-management-howto-cache.md) 的支援。</span><span class="sxs-lookup"><span data-stu-id="8db65-104">Azure API Management service has built-in support for [HTTP response caching](api-management-howto-cache.md) using the resource URL as the key.</span></span> <span data-ttu-id="8db65-105">可以在要求標頭中使用 `vary-by` 屬性修改索引鍵。</span><span class="sxs-lookup"><span data-stu-id="8db65-105">The key can be modified by request headers using the `vary-by` properties.</span></span> <span data-ttu-id="8db65-106">這很適合用於快取整個 HTTP 回應 (也稱為｢表示法｣)，但是有時候也很適合用於只快取部分表示法。</span><span class="sxs-lookup"><span data-stu-id="8db65-106">This is useful for caching entire HTTP responses (aka representations), but sometimes it is useful to just cache a portion of a representation.</span></span> <span data-ttu-id="8db65-107">新的 [cache-lookup-value](https://msdn.microsoft.com/library/azure/dn894086.aspx#GetFromCacheByKey) 和 [cache-store-value](https://msdn.microsoft.com/library/azure/dn894086.aspx#StoreToCacheByKey) 原則提供了可儲存及擷取原則定義中任意資料的能力。</span><span class="sxs-lookup"><span data-stu-id="8db65-107">The new [cache-lookup-value](https://msdn.microsoft.com/library/azure/dn894086.aspx#GetFromCacheByKey) and [cache-store-value](https://msdn.microsoft.com/library/azure/dn894086.aspx#StoreToCacheByKey) policies provide the ability to store and retrieve arbitrary pieces of data from within policy definitions.</span></span> <span data-ttu-id="8db65-108">這個能力也讓先前推出的 [send-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) 原則更有價值，因為您現在可以快取外部服務的回應。</span><span class="sxs-lookup"><span data-stu-id="8db65-108">This ability also adds value to the previously introduced [send-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) policy because you can now cache responses from external services.</span></span>

## <a name="architecture"></a><span data-ttu-id="8db65-109">架構</span><span class="sxs-lookup"><span data-stu-id="8db65-109">Architecture</span></span>
<span data-ttu-id="8db65-110">API 管理服務使用共用的個別租用戶資料快取，所以，當您相應增加為多個單位時，您仍可以存取相同的快取資料。</span><span class="sxs-lookup"><span data-stu-id="8db65-110">API Management service uses a shared per-tenant data cache so that, as you scale up to multiple units you will still get access to the same cached data.</span></span> <span data-ttu-id="8db65-111">不過，使用多區域部署時，在每個區域內有獨立的快取。</span><span class="sxs-lookup"><span data-stu-id="8db65-111">However, when working with a multi-region deployment there are independent caches within each of the regions.</span></span> <span data-ttu-id="8db65-112">由於這個原因，切勿將快取視為資料存放區，資料存放區是部分資訊片段的唯一來源。</span><span class="sxs-lookup"><span data-stu-id="8db65-112">Due to this, it is important to not treat the cache as a data store, where it is the only source of some piece of information.</span></span> <span data-ttu-id="8db65-113">如果您這麼做，之後又決定要採用多區域部署，擁有旅遊使用者的客戶可能會失去該快取資料的存取權。</span><span class="sxs-lookup"><span data-stu-id="8db65-113">If you did, and later decided to take advantage of the multi-region deployment, then customers with users that travel may lose access to that cached data.</span></span>

## <a name="fragment-caching"></a><span data-ttu-id="8db65-114">片段快取</span><span class="sxs-lookup"><span data-stu-id="8db65-114">Fragment caching</span></span>
<span data-ttu-id="8db65-115">在某些案例中，傳回的回應包含的某些資料不但判斷代價昂貴，而且還會保留一段合理的長時間。</span><span class="sxs-lookup"><span data-stu-id="8db65-115">There are certain cases where responses being returned contain some portion of data that is expensive to determine and yet remains fresh for a reasonable amount of time.</span></span> <span data-ttu-id="8db65-116">以航空公司建立的服務為例，服務提供航班訂位、航班狀態等相關資訊。如果使用者是航空公司集點方案的會員，他們也會擁有與其目前狀態和累積里程的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="8db65-116">As an example, consider a service built by an airline that provides information relating flight reservations, flight status, etc. If the user is a member of the airlines points program, they would also have information relating to their current status and mileage accumulated.</span></span> <span data-ttu-id="8db65-117">這些使用者相關資訊可能儲存在不同的系統中，但有可能需要包含在航班狀態和訂位相關的傳回回應中。</span><span class="sxs-lookup"><span data-stu-id="8db65-117">This user-related information might be stored in a different system, but it may be desirable to include it in responses returned about flight status and reservations.</span></span> <span data-ttu-id="8db65-118">這可以用稱為｢片段快取｣的程序做到。</span><span class="sxs-lookup"><span data-stu-id="8db65-118">This can be done using a process called fragment caching.</span></span> <span data-ttu-id="8db65-119">可從原始伺服器傳回主要的表示法，並使用某種權杖來指示要將使用者相關資訊插入何處。</span><span class="sxs-lookup"><span data-stu-id="8db65-119">The primary representation can be returned from the origin server using some kind of token to indicate where the user-related information is to be inserted.</span></span> 

<span data-ttu-id="8db65-120">考慮下列來自後端 API 的 JSON 回應。</span><span class="sxs-lookup"><span data-stu-id="8db65-120">Consider the following JSON response from a backend API.</span></span>

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

<span data-ttu-id="8db65-121">在 `/userprofile/{userid}` 的次要資源看起來像，</span><span class="sxs-lookup"><span data-stu-id="8db65-121">And secondary resource at `/userprofile/{userid}` that looks like,</span></span>

```json
{ "username" : "Bob Smith", "Status" : "Gold" }
```

<span data-ttu-id="8db65-122">為了決定要包含的適當使用者資訊，我們需要找出使用者是誰。</span><span class="sxs-lookup"><span data-stu-id="8db65-122">In order to determine the appropriate user information to include, we need to identify who the end user is.</span></span> <span data-ttu-id="8db65-123">這個機制取決於實作。</span><span class="sxs-lookup"><span data-stu-id="8db65-123">This mechanism is implementation dependent.</span></span> <span data-ttu-id="8db65-124">例如，我使用 `JWT` 權杖的 `Subject` 宣告。</span><span class="sxs-lookup"><span data-stu-id="8db65-124">As an example, I am using the `Subject` claim of a `JWT` token.</span></span> 

```xml
<set-variable
  name="enduserid"
  value="@(context.Request.Headers.GetValueOrDefault("Authorization","").Split(' ')[1].AsJwt()?.Subject)" />
```

<span data-ttu-id="8db65-125">我們會將這個 `enduserid` 值儲存在內容變數中供稍後使用。</span><span class="sxs-lookup"><span data-stu-id="8db65-125">We store this `enduserid` value in a context variable for later use.</span></span> <span data-ttu-id="8db65-126">下一個步驟是判斷先前的要求是否已擷取使用者資訊並將其儲存在快取中。</span><span class="sxs-lookup"><span data-stu-id="8db65-126">The next step is to determine if a previous request has already retrieved the user information and stored it in the cache.</span></span> <span data-ttu-id="8db65-127">我們的做法是使用 `cache-lookup-value` 原則。</span><span class="sxs-lookup"><span data-stu-id="8db65-127">For this we use the `cache-lookup-value` policy.</span></span>

```xml
<cache-lookup-value
key="@("userprofile-" + context.Variables["enduserid"])"
variable-name="userprofile" />
```

<span data-ttu-id="8db65-128">如果回應索引鍵值的快取中沒有任何項目，則不會建立 `userprofile` 內容變數。</span><span class="sxs-lookup"><span data-stu-id="8db65-128">If there is no entry in the cache that corresponds to the key value, then no `userprofile` context variable will be created.</span></span> <span data-ttu-id="8db65-129">我們使用 `choose` 控制流程原則來檢查查詢是否成功。</span><span class="sxs-lookup"><span data-stu-id="8db65-129">We check the success of the lookup using the `choose` control flow policy.</span></span>

```xml
<choose>
    <when condition="@(!context.Variables.ContainsKey("userprofile"))">
        <!-- If the userprofile context variable doesn’t exist, make an HTTP request to retrieve it.  -->
    </when>
</choose>
```

<span data-ttu-id="8db65-130">如果 `userprofile` 內容變數不存在，我們就要發出 HTTP 要求來擷取它。</span><span class="sxs-lookup"><span data-stu-id="8db65-130">If the `userprofile` context variable doesn’t exist, then we are going to have to make an HTTP request to retrieve it.</span></span>

```xml
<send-request
  mode="new"
  response-variable-name="userprofileresponse"
  timeout="10"
  ignore-error="true">

  <!-- Build a URL that points to the profile for the current end-user -->
  <set-url>@(new Uri(new Uri("https://apimairlineapi.azurewebsites.net/UserProfile/"),
      (string)context.Variables["enduserid"]).AbsoluteUri)
  </set-url>
  <set-method>GET</set-method>
</send-request>
```

<span data-ttu-id="8db65-131">我們使用 `enduserid` 來建構使用者設定檔資源的 URL。</span><span class="sxs-lookup"><span data-stu-id="8db65-131">We use the `enduserid` to construct the URL to the user profile resource.</span></span> <span data-ttu-id="8db65-132">一旦得到回應，我們可以提取回應的本文文字，並將它存回內容變數。</span><span class="sxs-lookup"><span data-stu-id="8db65-132">Once we have the response, we can pull the body text out of the response and store it back into a context variable.</span></span>

```xml
<set-variable
    name="userprofile"
    value="@(((IResponse)context.Variables["userprofileresponse"]).Body.As<string>())" />
```

<span data-ttu-id="8db65-133">為了避免我們需要再次發出這個 HTTP 要求，當相同使用者進行另一個要求時，我們可以將使用者設定檔儲存在快取中。</span><span class="sxs-lookup"><span data-stu-id="8db65-133">To avoid us having to make this HTTP request again, when the same user makes another request, we can store the user profile in the cache.</span></span>

```xml
<cache-store-value
    key="@("userprofile-" + context.Variables["enduserid"])"
    value="@((string)context.Variables["userprofile"])" duration="100000" />
```

<span data-ttu-id="8db65-134">我們使用我們原先嘗試擷取值時完全相同的索引鍵，將值儲存在快取中。</span><span class="sxs-lookup"><span data-stu-id="8db65-134">We store the value in the cache using the exact same key that we originally attempted to retrieve it with.</span></span> <span data-ttu-id="8db65-135">我們選擇的值儲存持續時間，應該根據資訊變更的經常性以及使用者對過期資訊的容忍度。</span><span class="sxs-lookup"><span data-stu-id="8db65-135">The duration that we choose to store the value should be based on how often the information changes and how tolerant users are to out of date information.</span></span> 

<span data-ttu-id="8db65-136">重要的是要了解，從快取擷取仍然是程序外的網路要求，並可能使要求的時間增加數十毫秒。</span><span class="sxs-lookup"><span data-stu-id="8db65-136">It is important to realize that retrieving from the cache is still an out-of-process, network request and potentially can still add tens of milliseconds to the request.</span></span> <span data-ttu-id="8db65-137">當判斷使用者設定檔資訊要花很長的時間，遠超過需要執行資料庫查詢或從多個後端彙總資訊的時間時，其優點就會顯現出來。</span><span class="sxs-lookup"><span data-stu-id="8db65-137">The benefits come when determining the user profile information takes significantly longer than that due to needing to do database queries or aggregate information from multiple back-ends.</span></span>

<span data-ttu-id="8db65-138">此程序的最後一個步驟是以我們的使用者設定檔資訊更新傳回的回應。</span><span class="sxs-lookup"><span data-stu-id="8db65-138">The final step in the process is to update the returned response with our user profile information.</span></span>

```xml
<!-- Update response body with user profile-->
<find-and-replace
    from='"$userprofile$"'
    to="@((string)context.Variables["userprofile"])" />
```

<span data-ttu-id="8db65-139">我選擇在權杖中使用引號，這樣一來，即使取代沒有發生，回應仍是有效的 JSON。</span><span class="sxs-lookup"><span data-stu-id="8db65-139">I chose to include the quotation marks as part of the token so that even when the replace doesn’t occur, the response was still valid JSON.</span></span> <span data-ttu-id="8db65-140">這麼做主要是讓偵錯更容易。</span><span class="sxs-lookup"><span data-stu-id="8db65-140">This was primarily to make debugging easier.</span></span>

<span data-ttu-id="8db65-141">將這些步驟全部結合在一起後，最終結果是看起來像以下這個的原則。</span><span class="sxs-lookup"><span data-stu-id="8db65-141">Once you combine all these steps together, the end result is a policy that looks like the following one.</span></span>

```xml
<policies>
    <inbound>
        <!-- How you determine user identity is application dependent -->
        <set-variable
          name="enduserid"
          value="@(context.Request.Headers.GetValueOrDefault("Authorization","").Split(' ')[1].AsJwt()?.Subject)" />

        <!--Look for userprofile for this user in the cache -->
        <cache-lookup-value
          key="@("userprofile-" + context.Variables["enduserid"])"
          variable-name="userprofile" />

        <!-- If we don’t find it in the cache, make a request for it and store it -->
        <choose>
            <when condition="@(!context.Variables.ContainsKey("userprofile"))">
                <!-- Make HTTP request to get user profile -->
                <send-request
                  mode="new"
                  response-variable-name="userprofileresponse"
                  timeout="10"
                  ignore-error="true">

                   <!-- Build a URL that points to the profile for the current end-user -->
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

<span data-ttu-id="8db65-142">此快取方法主要用於 HTML 是在伺服器端組成的網站，讓 HTML 可以轉譯成單一頁面。</span><span class="sxs-lookup"><span data-stu-id="8db65-142">This caching approach is primarily used in web sites where HTML is composed on the server side so that it can be rendered as a single page.</span></span> <span data-ttu-id="8db65-143">不過，它也適用於用戶端無法執行用戶端 HTTP 快取的 API，或是不想將此責任放在用戶端的情況。</span><span class="sxs-lookup"><span data-stu-id="8db65-143">However, it can also be useful in APIs where clients cannot do client side HTTP caching or it is desirable not to put that responsibility on the client.</span></span>

<span data-ttu-id="8db65-144">此種片段快取也可以在使用 Redis 快取伺服器的後端 Web 伺服器上進行，不過，當快取的片段來自不同後端而非主要回應時，使用 API 管理服務來執行這項工作便很實用。</span><span class="sxs-lookup"><span data-stu-id="8db65-144">This same kind of fragment caching can also be done on the backend web servers using a Redis caching server, however, using the API Management service to perform this work is useful when the cached fragments are coming from different back-ends than the primary responses.</span></span>

## <a name="transparent-versioning"></a><span data-ttu-id="8db65-145">透明的版本設定</span><span class="sxs-lookup"><span data-stu-id="8db65-145">Transparent versioning</span></span>
<span data-ttu-id="8db65-146">隨時支援多個不同實作版本的 API 是常見的做法。</span><span class="sxs-lookup"><span data-stu-id="8db65-146">It is common practice for multiple different implementation versions of an API to be supported at any one time.</span></span> <span data-ttu-id="8db65-147">這或許是為了支援不同的環境，像是開發、測試、生產等，或為了支援舊版的 API 讓 API 取用者有時間移轉到較新版本。</span><span class="sxs-lookup"><span data-stu-id="8db65-147">This is perhaps to support different environments, like dev, test, production, etc, or it may be to support older versions of the API to give time for API consumers to migrate to newer versions.</span></span> 

<span data-ttu-id="8db65-148">其中一種做法是將取用者目前想使用的 API 版本儲存在取用者的設定檔資料中，並呼叫適當的後端 URL，而不需要用戶端開發人員將 URL 從 `/v1/customers` 變更為 `/v2/customers`。</span><span class="sxs-lookup"><span data-stu-id="8db65-148">One approach to handling this instead of requiring client developers to change the URLs from `/v1/customers` to `/v2/customers` is to store in the consumer’s profile data which version of the API they currently wish to use and call the appropriate backend URL.</span></span> <span data-ttu-id="8db65-149">為了判斷特定用戶端要呼叫的正確後端 URL，必須查詢某些組態資料。</span><span class="sxs-lookup"><span data-stu-id="8db65-149">In order to determine the correct backend URL to call for a particular client, it is necessary to query some configuration data.</span></span> <span data-ttu-id="8db65-150">透過快取這項組態資料，我們可以減少執行此查詢的效能負面影響。</span><span class="sxs-lookup"><span data-stu-id="8db65-150">By caching this configuration data, we can minimize the performance penalty of doing this lookup.</span></span>

<span data-ttu-id="8db65-151">第一個步驟是判斷用來設定所需版本的識別碼。</span><span class="sxs-lookup"><span data-stu-id="8db65-151">The first step is to determine the identifier used to configure the desired version.</span></span> <span data-ttu-id="8db65-152">在此範例中，我選擇將版本關聯至產品訂用帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="8db65-152">In this example, I chose to associate the version to the product subscription key.</span></span> 

```xml
<set-variable name="clientid" value="@(context.Subscription.Key)" />
```

<span data-ttu-id="8db65-153">然後，我們執行快取查閱，以查看我們是否已經擷取所需的用戶端版本。</span><span class="sxs-lookup"><span data-stu-id="8db65-153">We then do a cache lookup to see if we already have retrieved the desired client version.</span></span>

```xml
<cache-lookup-value
key="@("clientversion-" + context.Variables["clientid"])"
variable-name="clientversion" />
```

<span data-ttu-id="8db65-154">接著，我們找找看在快取中有沒有它。</span><span class="sxs-lookup"><span data-stu-id="8db65-154">Then we check to see if we did not find it in the cache.</span></span>

```xml
<choose>
    <when condition="@(!context.Variables.ContainsKey("clientversion"))">
```

<span data-ttu-id="8db65-155">如果沒有，就去擷取它。</span><span class="sxs-lookup"><span data-stu-id="8db65-155">If we didn’t then we go and retrieve it.</span></span>

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

<span data-ttu-id="8db65-156">從回應中擷取回應本文文字。</span><span class="sxs-lookup"><span data-stu-id="8db65-156">Extract the response body text from the response.</span></span>

```xml
<set-variable
      name="clientversion"
      value="@(((IResponse)context.Variables["clientconfiguresponse"]).Body.As<string>())" />
```

<span data-ttu-id="8db65-157">將它存回快取中供日後使用。</span><span class="sxs-lookup"><span data-stu-id="8db65-157">Store it back in the cache for future use.</span></span>

```xml
<cache-store-value
      key="@("clientversion-" + context.Variables["clientid"])"
      value="@((string)context.Variables["clientversion"])"
      duration="100000" />
```

<span data-ttu-id="8db65-158">最後，更新後端 URL 以選取用戶端所需的服務版本。</span><span class="sxs-lookup"><span data-stu-id="8db65-158">And finally update the back-end URL to select the version of the service desired by the client.</span></span>

```xml
<set-backend-service
      base-url="@(context.Api.ServiceUrl.ToString() + "api/" + (string)context.Variables["clientversion"] + "/")" />
```

<span data-ttu-id="8db65-159">完整的原則看起來如下。</span><span class="sxs-lookup"><span data-stu-id="8db65-159">The completely policy is as follows.</span></span>

```xml
<inbound>
    <base />
    <set-variable name="clientid" value="@(context.Subscription.Key)" />
    <cache-lookup-value key="@("clientversion-" + context.Variables["clientid"])" variable-name="clientversion" />

    <!-- If we don’t find it in the cache, make a request for it and store it -->
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

<span data-ttu-id="8db65-160">讓 API 取用者能夠直接控制用戶端不需要更新和重新部署用戶端就可以存取哪一個後端版本，是一種簡潔的解決辦法，能夠解決許多 API 版本設定的問題。</span><span class="sxs-lookup"><span data-stu-id="8db65-160">Enabling API consumers to transparently control which backend version is being accessed by clients without having to update and redeploy clients is a elegant solution that addresses many API versioning concerns.</span></span>

## <a name="tenant-isolation"></a><span data-ttu-id="8db65-161">租用戶隔離</span><span class="sxs-lookup"><span data-stu-id="8db65-161">Tenant Isolation</span></span>
<span data-ttu-id="8db65-162">在大型、多租用戶的部署中，有些公司會在後端硬體的不同部署上建立不同的租用戶群組。</span><span class="sxs-lookup"><span data-stu-id="8db65-162">In larger, multi-tenant deployments some companies create separate groups of tenants on distinct deployments of backend hardware.</span></span> <span data-ttu-id="8db65-163">這樣可以降低後端硬體問題所影響的客戶數目。</span><span class="sxs-lookup"><span data-stu-id="8db65-163">This minimizes the number of customers who are impacted by a hardware issue on the backend.</span></span> <span data-ttu-id="8db65-164">也可以將新的軟體版本分階段推動。</span><span class="sxs-lookup"><span data-stu-id="8db65-164">It also enables new software versions to be rolled out in stages.</span></span> <span data-ttu-id="8db65-165">在理想情況下，對 API 取用者來說這個後端架構應該是透明的。</span><span class="sxs-lookup"><span data-stu-id="8db65-165">Ideally this backend architecture should be transparent to API consumers.</span></span> <span data-ttu-id="8db65-166">其做法類似於透明的版本設定，因為它根據相同的後端 URL 操作技巧，使用每個 API 金鑰的組態狀態。</span><span class="sxs-lookup"><span data-stu-id="8db65-166">This can be achieved in a similar way to transparent versioning because it is based on the same technique of manipulating the backend URL using configuration state per API key.</span></span>  

<span data-ttu-id="8db65-167">您將會傳回將租用戶與指派之硬體群組建立關聯的識別碼，而不是傳回每個訂用帳戶金鑰的 API 慣用的版本。</span><span class="sxs-lookup"><span data-stu-id="8db65-167">Instead of returning a preferred version of the API for each subscription key, you would return an identifier that relates a tenant to the assigned hardware group.</span></span> <span data-ttu-id="8db65-168">這個識別碼可以用來建構適當的後端 URL。</span><span class="sxs-lookup"><span data-stu-id="8db65-168">That identifier can be used to construct the appropriate backend URL.</span></span>

## <a name="summary"></a><span data-ttu-id="8db65-169">Summary</span><span class="sxs-lookup"><span data-stu-id="8db65-169">Summary</span></span>
<span data-ttu-id="8db65-170">能夠自由地使用 Azure API 管理快取來儲存任何種類的資料，可讓您有效率地存取組態資料，而這些資料可能會影響輸入要求的處理方式。</span><span class="sxs-lookup"><span data-stu-id="8db65-170">The freedom to use the Azure API management cache for storing any kind of data enables efficient access to configuration data that can affect the way an inbound request is processed.</span></span> <span data-ttu-id="8db65-171">上述快取也可以用來儲存資料片段，此種片段可以增加從後端 API 傳回的回應。</span><span class="sxs-lookup"><span data-stu-id="8db65-171">It can also be used to store data fragments that can augment responses, returned from a backend API.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8db65-172">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8db65-172">Next steps</span></span>
<span data-ttu-id="8db65-173">如果這些原則為您達成其他案例，或是有案例您想要達成但認為目前無法執行，敬請不吝賜教在 Disqus 的本主題系列中提供意見。</span><span class="sxs-lookup"><span data-stu-id="8db65-173">Please give us your feedback in the Disqus thread for this topic if there are other scenarios that these policies have enabled for you, or if there are scenarios you would like to achieve but do not feel are currently possible.</span></span>

