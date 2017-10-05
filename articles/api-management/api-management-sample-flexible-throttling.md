---
title: "以 Azure API 管理進行進階要求節流"
description: "了解如何使用 Azure API 管理來建立及套用彈性配額和速率限制原則。"
services: api-management
documentationcenter: 
author: darrelmiller
manager: erikre
editor: 
ms.assetid: fc813a65-7793-4c17-8bb9-e387838193ae
ms.service: api-management
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 35375e599891a9443a91c4c3a8657e8c9c48c7b5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="advanced-request-throttling-with-azure-api-management"></a><span data-ttu-id="3791d-103">以 Azure API 管理進行進階要求節流</span><span class="sxs-lookup"><span data-stu-id="3791d-103">Advanced request throttling with Azure API Management</span></span>
<span data-ttu-id="3791d-104">能夠節流傳入要求是 Azure API 管理的重要角色。</span><span class="sxs-lookup"><span data-stu-id="3791d-104">Being able to throttle incoming requests is a key role of Azure API Management.</span></span> <span data-ttu-id="3791d-105">藉由控制要求的速率或傳輸的要求/資料總量，API 管理讓 API 提供者能夠保護其 API 不被濫用，並建立不同 API 產品層級的價值。</span><span class="sxs-lookup"><span data-stu-id="3791d-105">Either by controlling the rate of requests or the total requests/data transferred, API Management allows API providers to protect their APIs from abuse and create value for different API product tiers.</span></span>

## <a name="product-based-throttling"></a><span data-ttu-id="3791d-106">依產品節流</span><span class="sxs-lookup"><span data-stu-id="3791d-106">Product based throttling</span></span>
<span data-ttu-id="3791d-107">到目前為止，速率節流功能侷限於特定產品訂閱的限定範圍 (基本上是索引鍵)，是在 API 管理發行者入口網站中定義。</span><span class="sxs-lookup"><span data-stu-id="3791d-107">To date, the rate throttling capabilities have been limited to being scoped to a particular Product subscription (essentially a key), defined in the API Management publisher portal.</span></span> <span data-ttu-id="3791d-108">這可用來讓 API 提供者將限制套用至註冊使用其 API 的開發人員，不過，舉例來說，它無法協助節流 API 的個別使用者。</span><span class="sxs-lookup"><span data-stu-id="3791d-108">This is useful for the API provider to apply limits on the developers who have signed up to use their API, however, it does not help, for example, in throttling individual end-users of the API.</span></span> <span data-ttu-id="3791d-109">想讓開發人員的應用程式的單一使用者取用整個配額，並讓開發人員的其他客戶無法使用應用程式，是有可能的。</span><span class="sxs-lookup"><span data-stu-id="3791d-109">It is possible that for single user of the developer's application to consume the entire quota and then prevent other customers of the developer from being able to use the application.</span></span> <span data-ttu-id="3791d-110">同樣的，數個產生大量要求的客戶可能會限制偶爾使用者的存取權。</span><span class="sxs-lookup"><span data-stu-id="3791d-110">Also, several customers who might generate a high volume of requests may limit access to occasional users.</span></span>

## <a name="custom-key-based-throttling"></a><span data-ttu-id="3791d-111">依自訂索引鍵節流</span><span class="sxs-lookup"><span data-stu-id="3791d-111">Custom key based throttling</span></span>
<span data-ttu-id="3791d-112">新的 [rate-limit-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) 和 [quota-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) 原則提供明顯更有彈性的流量控制解決方案。</span><span class="sxs-lookup"><span data-stu-id="3791d-112">The new [rate-limit-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) and [quota-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) policies provide a significantly more flexible solution to traffic control.</span></span> <span data-ttu-id="3791d-113">這些新原則可讓您定義運算式，以識別將用來追蹤流量使用的索引鍵。</span><span class="sxs-lookup"><span data-stu-id="3791d-113">These new policies allow you to define expressions to identify the keys that will be used to track traffic usage.</span></span> <span data-ttu-id="3791d-114">其運作的方式用範例來說明最簡單。</span><span class="sxs-lookup"><span data-stu-id="3791d-114">The way this works is easiest illustrated with an example.</span></span> 

## <a name="ip-address-throttling"></a><span data-ttu-id="3791d-115">IP 位址節流</span><span class="sxs-lookup"><span data-stu-id="3791d-115">IP Address throttling</span></span>
<span data-ttu-id="3791d-116">下列原則會限制單一用戶端 IP 位址每一分鐘只有 10 個呼叫，等於每個月總數為 1,000,000 個呼叫和 10,000 KB 頻寬。</span><span class="sxs-lookup"><span data-stu-id="3791d-116">The following policies restrict a single client IP address to only 10 calls every minute, with a total of 1,000,000 calls and 10,000 kilobytes of bandwidth per month.</span></span> 

```xml
<rate-limit-by-key  calls="10"
          renewal-period="60"
          counter-key="@(context.Request.IpAddress)" />

<quota-by-key calls="1000000"
          bandwidth="10000"
          renewal-period="2629800"
          counter-key="@(context.Request.IpAddress)" />
```

<span data-ttu-id="3791d-117">如果網際網路上的所有用戶端皆使用唯一 IP 位址，這是可能是限制使用者使用量的有效方式。</span><span class="sxs-lookup"><span data-stu-id="3791d-117">If all clients on the Internet used a unique IP address, this might be an effective way of limiting usage by user.</span></span> <span data-ttu-id="3791d-118">不過，很有可能多個使用者共用單一公用 IP 位址，因為他們透過 NAT 裝置存取網際網路。</span><span class="sxs-lookup"><span data-stu-id="3791d-118">However, it is quite likely that multiple users will sharing a single public IP address due to them accessing the Internet via a NAT device.</span></span> <span data-ttu-id="3791d-119">儘管如此，對允許未驗證存取的 API 來說， `IpAddress` 可能是最佳選項。</span><span class="sxs-lookup"><span data-stu-id="3791d-119">Despite this, for APIs that allow unauthenticated access the `IpAddress` might be the best option.</span></span>

## <a name="user-identity-throttling"></a><span data-ttu-id="3791d-120">使用者身分識別節流</span><span class="sxs-lookup"><span data-stu-id="3791d-120">User identity throttling</span></span>
<span data-ttu-id="3791d-121">如果使用者經過驗證，則可以根據該名使用者的唯一身分識別產生節流索引鍵。</span><span class="sxs-lookup"><span data-stu-id="3791d-121">If an end user is authenticated then a throttling key can be generated based on information that uniquely identifies an that user.</span></span>

```xml
<rate-limit-by-key calls="10"
    renewal-period="60"
    counter-key="@(context.Request.Headers.GetValueOrDefault("Authorization","").AsJwt()?.Subject)" />
```

<span data-ttu-id="3791d-122">在此範例中，我們要擷取授權的標頭，將它轉換成 `JWT` 物件，並使用權杖的主體來識別使用者，並使用它做速率限制索引鍵。</span><span class="sxs-lookup"><span data-stu-id="3791d-122">In this example we extract the Authorization header, convert it to `JWT` object and use the subject of the token to identify the user and use that as the rate limiting key.</span></span> <span data-ttu-id="3791d-123">如果使用者身分識別是儲存在 `JWT` 中做為其中一個宣告，則該值可用於它的位置。</span><span class="sxs-lookup"><span data-stu-id="3791d-123">If the user identity is stored in the `JWT` as one of the other claims then that value could be used in its place.</span></span>

## <a name="combined-policies"></a><span data-ttu-id="3791d-124">結合的原則</span><span class="sxs-lookup"><span data-stu-id="3791d-124">Combined policies</span></span>
<span data-ttu-id="3791d-125">雖然新的節流原則比現有節流原則提供更多的控制，但仍會有結合兩種功能的值。</span><span class="sxs-lookup"><span data-stu-id="3791d-125">Although the new throttling policies provide more control than the existing throttling policies, there is still value combining both capabilities.</span></span> <span data-ttu-id="3791d-126">依產品訂用帳戶金鑰 ([依訂用帳戶限制呼叫率](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate)和[依訂用帳戶設定使用量配額](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota)) 進行節流是一種根據使用量層級收費、讓 API 創造獲利的絕佳方式。</span><span class="sxs-lookup"><span data-stu-id="3791d-126">Throttling by product subscription key ([Limit call rate by subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) and [Set usage quota by subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota)) is a great way to enable monetizing of an API by charging based on usage levels.</span></span> <span data-ttu-id="3791d-127">更精細的依使用者控制節流則和其互補，並防止一位使用者的行為降低另一位使用者的體驗。</span><span class="sxs-lookup"><span data-stu-id="3791d-127">The finer grained control of being able to throttle by user is complementary and prevents one user's behavior from degrading the experience of another.</span></span> 

## <a name="client-driven-throttling"></a><span data-ttu-id="3791d-128">用戶端導向節流</span><span class="sxs-lookup"><span data-stu-id="3791d-128">Client driven throttling</span></span>
<span data-ttu-id="3791d-129">若使用 [原則運算式](https://msdn.microsoft.com/library/azure/dn910913.aspx)定義節流索引鍵，則是由 API 提供者選擇如何設定節流的範圍。</span><span class="sxs-lookup"><span data-stu-id="3791d-129">When the throttling key is defined using a [policy expression](https://msdn.microsoft.com/library/azure/dn910913.aspx), then it is the API provider that is choosing how the throttling is scoped.</span></span> <span data-ttu-id="3791d-130">不過，開發人員可能想要控制他們對自己的客戶的速率限制。</span><span class="sxs-lookup"><span data-stu-id="3791d-130">However, a developer might want to control how they rate limit their own customers.</span></span> <span data-ttu-id="3791d-131">API 提供者可以藉由導入自訂標頭來做到這一點，以允許開發人員的用戶端應用程式與 API 通訊索引鍵。</span><span class="sxs-lookup"><span data-stu-id="3791d-131">This could be enabled by the API provider by introducing a custom header to allow the developer's client application to communicate the key to the API.</span></span>

```xml
<rate-limit-by-key calls="100"
          renewal-period="60"
          counter-key="@(request.Headers.GetValueOrDefault("Rate-Key",""))"/>
```

<span data-ttu-id="3791d-132">這可讓開發人員的用戶端應用程式選擇要如何建立速率限制索引鍵。</span><span class="sxs-lookup"><span data-stu-id="3791d-132">This enables the developer's client application to choose how they want to create the rate limiting key.</span></span> <span data-ttu-id="3791d-133">加上一些巧思，用戶端開發人員可以透過配置索引鍵組給使用者和輪流使用索引鍵，建立自己的速率層。</span><span class="sxs-lookup"><span data-stu-id="3791d-133">With a little bit of ingenuity a client developer could create their own rate tiers by allocating sets of keys to users and rotating the key usage.</span></span>

## <a name="summary"></a><span data-ttu-id="3791d-134">Summary</span><span class="sxs-lookup"><span data-stu-id="3791d-134">Summary</span></span>
<span data-ttu-id="3791d-135">Azure API 管理提供速率和配額節流，不但能保護您的 API 服務，並為您的 API 服務增加價值。</span><span class="sxs-lookup"><span data-stu-id="3791d-135">Azure API Management provides rate and quote throttling to both protect and add value to your API service.</span></span> <span data-ttu-id="3791d-136">新的節流原則與自訂範圍規則，可讓您更精細的控制這些原則，進而讓您的客戶建置更好的應用程式。</span><span class="sxs-lookup"><span data-stu-id="3791d-136">The new throttling policies with custom scoping rules allow you finer grained control over those policies to enable your customers to build even better applications.</span></span> <span data-ttu-id="3791d-137">本文中的範例示範如何使用這些新原則，分別使用用戶端 IP 位址、使用者身分識別及用戶端產生值來製造速率限制索引鍵。</span><span class="sxs-lookup"><span data-stu-id="3791d-137">The examples in this article demonstrate the use of these new policies by manufacturing rate limiting keys with client IP addresses, user identity, and client generated values.</span></span> <span data-ttu-id="3791d-138">不過，訊息中還有許多其他部份可以利用，例如使用者代理程式、URL 路徑片段、訊息大小。</span><span class="sxs-lookup"><span data-stu-id="3791d-138">However, there are many other parts of the message that could be used such as user agent, URL path fragments, message size.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3791d-139">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3791d-139">Next steps</span></span>
<span data-ttu-id="3791d-140">敬請不吝賜教在 Disqus 的本主題系列中提供意見。</span><span class="sxs-lookup"><span data-stu-id="3791d-140">Please give us your feedback in the Disqus thread for this topic.</span></span> <span data-ttu-id="3791d-141">我們很想知道其他在您的案例中是合理選擇的可能索引鍵值。</span><span class="sxs-lookup"><span data-stu-id="3791d-141">It would be great to hear about other potential key values that have been a logical choice in your scenarios.</span></span>

## <a name="watch-a-video-overview-of-these-policies"></a><span data-ttu-id="3791d-142">觀看這些原則的影片概觀</span><span class="sxs-lookup"><span data-stu-id="3791d-142">Watch a video overview of these policies</span></span>
<span data-ttu-id="3791d-143">如需有關本文中所涵蓋的 [rate-limit-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) 和 [quota-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) 原則的詳細資訊，請觀看以下影片。</span><span class="sxs-lookup"><span data-stu-id="3791d-143">For more information on the [rate-limit-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) and [quota-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) policies covered in this article, please watch the following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Advanced-Request-Throttling-with-Azure-API-Management/player]
> 
> 

