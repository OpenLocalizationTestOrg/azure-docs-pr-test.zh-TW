---
title: "Azure API 管理、 事件中樞與 Runscope Api aaaMonitor |Microsoft 文件"
description: "示範連接的 Azure API 管理、 Azure 事件中樞與 http 記錄與監控 Runscope hello 記錄到事件中樞原則的範例應用程式"
services: api-management
documentationcenter: 
author: darrelmiller
manager: erikre
editor: 
ms.assetid: c528cf6f-5f16-4a06-beea-fa1207541a47
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 7456a2436f3a2d7b815b70b65fca9481d39c5fe9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-your-apis-with-azure-api-management-event-hubs-and-runscope"></a><span data-ttu-id="e9dd3-103">利用 Azure API 管理、事件中樞及 Runscope 監視您的 API</span><span class="sxs-lookup"><span data-stu-id="e9dd3-103">Monitor your APIs with Azure API Management, Event Hubs and Runscope</span></span>
<span data-ttu-id="e9dd3-104">hello [API 管理服務](api-management-key-concepts.md)提供許多功能 tooenhance hello 處理 HTTP 要求傳送 tooyour HTTP API。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-104">hello [API Management service](api-management-key-concepts.md) provides many capabilities tooenhance hello processing of HTTP requests sent tooyour HTTP API.</span></span> <span data-ttu-id="e9dd3-105">不過，hello 存在的 hello 要求和回應是暫時性。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-105">However, hello existence of hello requests and responses are transient.</span></span> <span data-ttu-id="e9dd3-106">hello 要求，其流經 hello API 管理服務 tooyour 後端應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-106">hello request is made and it flows through hello API Management service tooyour backend API.</span></span> <span data-ttu-id="e9dd3-107">您的 API 處理 hello 要求和回應回流經 toohello API 取用者。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-107">Your API processes hello request and a response flows back through toohello API consumer.</span></span> <span data-ttu-id="e9dd3-108">hello API 管理服務可供顯示 hello 應用程式開發介面的相關的一些重要統計資料 hello 發行者入口網站儀表板中，但除此之外、 hello 詳細資料都已消失。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-108">hello API Management service keeps some important statistics about hello APIs for display in hello Publisher portal dashboard, but beyond that, hello details are gone.</span></span>

<span data-ttu-id="e9dd3-109">使用 hello[記錄-eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) [原則](api-management-howto-policies.md)hello API 管理服務中您可以傳送任何詳細資料，從 hello 要求和回應 tooan [Azure 事件中心](../event-hubs/event-hubs-what-is-event-hubs.md)。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-109">By using hello [log-to-eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) [policy](api-management-howto-policies.md) in hello API Management service you can send any details from hello request and response tooan [Azure Event Hub](../event-hubs/event-hubs-what-is-event-hubs.md).</span></span> <span data-ttu-id="e9dd3-110">有各種為什麼您可能想要 toogenerate 來自傳送 tooyour Api HTTP 訊息的原因。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-110">There are a variety of reasons why you may want toogenerate events from HTTP messages being sent tooyour APIs.</span></span> <span data-ttu-id="e9dd3-111">範例包括更新稽核線索、使用量分析、例外狀況警示和協力廠商整合。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-111">Some examples include audit trail of updates, usage analytics, exception alerting and 3rd party integrations.</span></span>   

<span data-ttu-id="e9dd3-112">本文示範如何 toocapture hello 整個 HTTP 要求和回應訊息，傳送 tooan 事件中心資料，然後轉送該訊息 tooa 協力廠商服務提供 HTTP 記錄和監視 windows 服務。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-112">This article demonstrates how toocapture hello entire HTTP request and response message, send it tooan Event Hub and then relay that message tooa third party service that provides HTTP logging and monitoring services.</span></span>

## <a name="why-send-from-api-management-service"></a><span data-ttu-id="e9dd3-113">為什麼要從 API 管理服務傳送？</span><span class="sxs-lookup"><span data-stu-id="e9dd3-113">Why Send From API Management Service?</span></span>
<span data-ttu-id="e9dd3-114">很可能 toowrite HTTP 中介軟體，可以插入 HTTP API 架構 toocapture HTTP 要求和回應和送入記錄和監視系統。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-114">It is possible toowrite HTTP middleware that can plug into HTTP API frameworks toocapture HTTP requests and responses and feed them into logging and monitoring systems.</span></span> <span data-ttu-id="e9dd3-115">hello 缺點 toothis 方法是 hello HTTP 中介軟體需要 toobe 整合至 hello 後端應用程式開發介面，而且必須符合 hello API hello 平台。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-115">hello downside toothis approach is hello HTTP middleware needs toobe integrated into hello backend API and must match hello platform of hello API.</span></span> <span data-ttu-id="e9dd3-116">如果有多個 Api 每個必須部署 hello 中介軟體。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-116">If there are multiple APIs then each one must deploy hello middleware.</span></span> <span data-ttu-id="e9dd3-117">後端 API 無法升級通常有一些原因。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-117">Often there are reasons why backend APIs cannot be updated.</span></span>

<span data-ttu-id="e9dd3-118">Hello Azure API 管理服務 toointegrate 使用記錄基礎結構提供集中式且平台無關的解決方案。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-118">Using hello Azure API Management service toointegrate with logging infrastructure provides a centralized and platform-independent solution.</span></span> <span data-ttu-id="e9dd3-119">它也是可擴充的因為部分 toohello[地理複寫](api-management-howto-deploy-multi-region.md)Azure API 管理的功能。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-119">It is also scalable, in part due toohello [geo-replication](api-management-howto-deploy-multi-region.md) capabilities of Azure API Management.</span></span>

## <a name="why-send-tooan-azure-event-hub"></a><span data-ttu-id="e9dd3-120">為什麼要傳送 tooan Azure 事件中心？</span><span class="sxs-lookup"><span data-stu-id="e9dd3-120">Why send tooan Azure Event Hub?</span></span>
<span data-ttu-id="e9dd3-121">它是合理的 tooask，為什麼要建立特定 tooAzure 事件中心的原則嗎？</span><span class="sxs-lookup"><span data-stu-id="e9dd3-121">It is a reasonable tooask, why create a policy that is specific tooAzure Event Hubs?</span></span> <span data-ttu-id="e9dd3-122">有許多不同的地方，我想要 toolog 我的要求。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-122">There are many different places where I might want toolog my requests.</span></span> <span data-ttu-id="e9dd3-123">為什麼不只傳送 hello 直接要求 toohello 最終目的地？</span><span class="sxs-lookup"><span data-stu-id="e9dd3-123">Why not just send hello requests directly toohello final destination?</span></span>  <span data-ttu-id="e9dd3-124">這是一個選項。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-124">That is an option.</span></span> <span data-ttu-id="e9dd3-125">不過，當進行記錄要求從 API 管理服務，它會需要 tooconsider 記錄訊息會如何影響 hello API hello 效能。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-125">However, when making logging requests from an API management service, it is necessary tooconsider how logging messages will impact hello performance of hello API.</span></span> <span data-ttu-id="e9dd3-126">增加系統元件的可用執行個體或利用異地複寫功能，可以處理逐漸增加的負載。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-126">Gradual increases in load can be handled by increasing available instances of system components or by taking advantage of geo-replication.</span></span> <span data-ttu-id="e9dd3-127">不過，簡短的流量尖峰，可能會造成要求 toobe 大幅延遲如果要求 toologging 基礎結構啟動 tooslow 負載。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-127">However, short spikes in traffic can cause requests toobe significantly delayed if requests toologging infrastructure start tooslow under load.</span></span>

<span data-ttu-id="e9dd3-128">hello Azure 事件中心設計的 tooingress 龐大資料磁碟區，與容量，以處理遠編號的事件高於 hello 數目的 HTTP 要求大部分的應用程式開發介面處理程序。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-128">hello Azure Event Hubs is designed tooingress huge volumes of data, with capacity for dealing with a far higher number of events than hello number of HTTP requests most APIs process.</span></span> <span data-ttu-id="e9dd3-129">事件中心 hello 做為一種您 API 管理服務和 hello 基礎結構將會儲存及處理 hello 訊息之間有複雜的緩衝區。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-129">hello Event Hub acts as a kind of sophisticated buffer between your API management service and hello infrastructure that will store and process hello messages.</span></span> <span data-ttu-id="e9dd3-130">這可確保不會因為 toohello 記錄基礎結構降低您的應用程式開發介面效能。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-130">This ensures that your API performance will not suffer due toohello logging infrastructure.</span></span>  

<span data-ttu-id="e9dd3-131">一旦 hello 資料已傳送 tooan 事件中心，它會持續保留，並將等候事件中樞取用者 tooprocess 它。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-131">Once hello data has been passed tooan Event Hub it is persisted and will wait for Event Hub consumers tooprocess it.</span></span> <span data-ttu-id="e9dd3-132">事件中心 hello 不在意如何處理，它只重視並確定將會成功傳送 hello 訊息。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-132">hello Event Hub does not care how it will be processed, it just cares about making sure hello message will be successfully delivered.</span></span>     

<span data-ttu-id="e9dd3-133">事件中心有 hello 能力 toostream 事件 toomultiple 取用者群組。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-133">Event Hubs have hello ability toostream events toomultiple consumer groups.</span></span> <span data-ttu-id="e9dd3-134">這可讓事件 toobe 完全不同的系統所處理。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-134">This allows events toobe processed by completely different systems.</span></span> <span data-ttu-id="e9dd3-135">這可讓支援不需將加入延遲放在只有一個事件需求產生 toobe hello 處理 hello API 管理服務中的 hello API 要求的許多整合案例。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-135">This enables supporting many integration scenarios without putting addition delays on hello processing of hello API request within hello API Management service as only one event needs toobe generated.</span></span>

## <a name="a-policy-toosend-applicationhttp-messages"></a><span data-ttu-id="e9dd3-136">原則 toosend http 應用程式/訊息</span><span class="sxs-lookup"><span data-stu-id="e9dd3-136">A policy toosend application/http messages</span></span>
<span data-ttu-id="e9dd3-137">事件中樞接受簡單字串形式的事件資料。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-137">An Event Hub accepts event data as a simple string.</span></span> <span data-ttu-id="e9dd3-138">該字串 hello 內容都已完全啟動 tooyou。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-138">hello contents of that string are completely up tooyou.</span></span> <span data-ttu-id="e9dd3-139">toobe 無法 toopackage HTTP 要求和傳送關閉 tooEvent 集線器我們需要 tooformat hello 字串 hello 要求或回應資訊。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-139">toobe able toopackage up an HTTP request and send it off tooEvent Hubs we need tooformat hello string with hello request or response information.</span></span> <span data-ttu-id="e9dd3-140">在這種情況下，如果沒有現有的格式，我們可以重複使用，然後我們可能不需要 toowrite 自己剖析的程式碼。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-140">In situations like this, if there is an existing format we can reuse, then we may not have toowrite our own parsing code.</span></span> <span data-ttu-id="e9dd3-141">一開始我視為使用 hello [HAR](http://www.softwareishard.com/blog/har-12-spec/)傳送 HTTP 要求和回應。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-141">Initially I considered using hello [HAR](http://www.softwareishard.com/blog/har-12-spec/) for sending HTTP requests and responses.</span></span> <span data-ttu-id="e9dd3-142">不過，這種格式最適合用於儲存 JSON 格式的一連串 HTTP 要求。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-142">However, this format is optimized for storing a sequence of HTTP requests in a JSON based format.</span></span> <span data-ttu-id="e9dd3-143">它包含必要的項目加入不必要的複雜性 hello 案例中的 hello wire 上傳送 hello HTTP 訊息數。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-143">It contained a number of mandatory elements that added unnecessary complexity for hello scenario of passing hello HTTP message over hello wire.</span></span>  

<span data-ttu-id="e9dd3-144">可用的替代選項是 toouse hello`application/http`媒體類型 hello HTTP 規格中所述[RFC 7230](http://tools.ietf.org/html/rfc7230)。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-144">An alternative option was toouse hello `application/http` media type as described in hello HTTP specification [RFC 7230](http://tools.ietf.org/html/rfc7230).</span></span> <span data-ttu-id="e9dd3-145">這個媒體類型會使用完全相同格式也就是使用的 tooactually 傳送 HTTP 訊息上 hello 傳輸，但 hello 整個訊息可以放置 hello 另一個的 HTTP 要求主體中的 hello。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-145">This media type uses hello exact same format that is used tooactually send HTTP messages over hello wire, but hello entire message can be put in hello body of another HTTP request.</span></span> <span data-ttu-id="e9dd3-146">在我們的案例只我們 toouse hello 主體為我們訊息 toosend tooEvent 集線器。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-146">In our case we are just going toouse hello body as our message toosend tooEvent Hubs.</span></span> <span data-ttu-id="e9dd3-147">為了方便起見，已存在於的剖析器[Microsoft ASP.NET Web API 2.2 用戶端](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Client/)程式庫可以剖析此格式，並將它轉換成 hello 原生`HttpRequestMessage`和`HttpResponseMessage`物件。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-147">Conveniently, there is a parser that exists in [Microsoft ASP.NET Web API 2.2 Client](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Client/) libraries that can parse this format and convert it into hello native `HttpRequestMessage` and `HttpResponseMessage` objects.</span></span>

<span data-ttu-id="e9dd3-148">toobe 無法 toocreate 這則訊息，我們需要 tootake 利用 C# 基礎[原則運算式](https://msdn.microsoft.com/library/azure/dn910913.aspx)在 Azure API 管理。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-148">toobe able toocreate this message we need tootake advantage of C# based [Policy expressions](https://msdn.microsoft.com/library/azure/dn910913.aspx) in Azure API Management.</span></span> <span data-ttu-id="e9dd3-149">以下是將傳送 HTTP 要求訊息 tooAzure 事件中心 hello 原則。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-149">Here is hello policy which sends a HTTP request message tooAzure Event Hubs.</span></span>

```xml
<log-to-eventhub logger-id="conferencelogger" partition-id="0">
@{
   var requestLine = string.Format("{0} {1} HTTP/1.1\r\n",
                                               context.Request.Method,
                                               context.Request.Url.Path + context.Request.Url.QueryString);

   var body = context.Request.Body?.As<string>(true);
   if (body != null && body.Length > 1024)
   {
       body = body.Substring(0, 1024);
   }

   var headers = context.Request.Headers
                          .Where(h => h.Key != "Authorization" && h.Key != "Ocp-Apim-Subscription-Key")
                          .Select(h => string.Format("{0}: {1}", h.Key, String.Join(", ", h.Value)))
                          .ToArray<string>();

   var headerString = (headers.Any()) ? string.Join("\r\n", headers) + "\r\n" : string.Empty;

   return "request:"   + context.Variables["message-id"] + "\n"
                       + requestLine + headerString + "\r\n" + body;
}
</log-to-eventhub>
```

### <a name="policy-declaration"></a><span data-ttu-id="e9dd3-150">原則宣告</span><span class="sxs-lookup"><span data-stu-id="e9dd3-150">Policy declaration</span></span>
<span data-ttu-id="e9dd3-151">此原則運算式有一些值得一提的特別之處。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-151">There a few particular things worth mentioning about this policy expression.</span></span> <span data-ttu-id="e9dd3-152">hello 記錄到事件中樞原則都有稱為記錄器識別碼指的是 toohello 未 hello API 管理服務中建立的記錄器名稱的屬性。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-152">hello log-to-eventhub policy has an attribute called logger-id which refers toohello name of logger that has been created within hello API Management service.</span></span> <span data-ttu-id="e9dd3-153">詳細資料的方式 toosetup hello API 管理服務中的事件中樞記錄器可以找到 hello 文件中的 hello[如何 toolog 事件 tooAzure Azure API 管理中的事件中樞](api-management-howto-log-event-hubs.md)。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-153">hello details of how toosetup an Event Hub logger in hello API Management service can be found in hello document [How toolog events tooAzure Event Hubs in Azure API Management](api-management-howto-log-event-hubs.md).</span></span> <span data-ttu-id="e9dd3-154">hello 第二個屬性是選擇性參數，指示事件中心中的資料分割 toostore hello 訊息。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-154">hello second attribute is an optional parameter that instructs Event Hubs which partition toostore hello message in.</span></span> <span data-ttu-id="e9dd3-155">事件中心使用資料分割 tooenable scalabilty，而且需要至少有兩個。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-155">Event Hubs use partitions tooenable scalabilty and require a minimum of two.</span></span> <span data-ttu-id="e9dd3-156">依序傳遞訊息的 hello 只保證在資料分割中。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-156">hello ordered delivery of messages is only guaranteed within a partition.</span></span> <span data-ttu-id="e9dd3-157">如果我們無法執行指示事件中心，資料分割 tooplace hello 訊息，則會使用循環配置資源演算法 toodistribute hello 負載。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-157">If we do not instruct Event Hub in which partition tooplace hello message, it will use a round-robin algorithm toodistribute hello load.</span></span> <span data-ttu-id="e9dd3-158">但是，可能會導致某些不按順序處理我們訊息 toobe。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-158">However, that may cause some of our messages toobe processed out of order.</span></span>  

### <a name="partitions"></a><span data-ttu-id="e9dd3-159">分割數</span><span class="sxs-lookup"><span data-stu-id="e9dd3-159">Partitions</span></span>
<span data-ttu-id="e9dd3-160">tooensure tooconsumers 會依序傳遞訊息，並利用 hello 負載散發功能的資料分割，我選擇 toosend HTTP 要求訊息 tooone 磁碟分割及 HTTP 回應訊息 tooa 第二個資料分割。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-160">tooensure our messages are delivered tooconsumers in order and take advantage of hello load distribution capability of partitions, I chose toosend HTTP request messages tooone partition and HTTP response messages tooa second partition.</span></span> <span data-ttu-id="e9dd3-161">如此可確保負載平均分散，而且我們可以保證所有要求和所有回應都會依序取用。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-161">This will ensure an even load distribution and we can guarantee that all requests will be consumed in order and all responses will be consumed in order.</span></span> <span data-ttu-id="e9dd3-162">很可能讓取用 hello 對應的要求，再回應 toobe 但，並不是問題，因為我們有不同的機制，相互關聯的要求 tooresponses 以及我們已經知道要求一律前面回應。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-162">It is possible for a response toobe consumed before hello corresponding request, but as that is not a problem as we have a different mechanism for correlating requests tooresponses and we know that requests always come before responses.</span></span>

### <a name="http-payloads"></a><span data-ttu-id="e9dd3-163">HTTP 裝載</span><span class="sxs-lookup"><span data-stu-id="e9dd3-163">HTTP payloads</span></span>
<span data-ttu-id="e9dd3-164">在建置 hello 之後`requestLine`我們檢查 toosee hello 要求主體應該會被截斷。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-164">After building hello `requestLine` we check toosee if hello request body should be truncated.</span></span> <span data-ttu-id="e9dd3-165">hello 要求主體是被截斷的 tooonly 1024。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-165">hello request body is truncated tooonly 1024.</span></span> <span data-ttu-id="e9dd3-166">這可能會增加，個別的事件中樞訊息不過是有限的 too256KB，因此很可能在某些 HTTP 訊息委員將未納入單一訊息。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-166">This could be increased, however individual Event Hub messages are limited too256KB, so it is likely that some HTTP message bodies will not fit in a single message.</span></span> <span data-ttu-id="e9dd3-167">進行記錄和分析大量的資訊時，都可以衍生自剛 hello HTTP 要求行和標頭。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-167">When doing logging and analytics a significant amount of information can be derived from just hello HTTP request line and headers.</span></span> <span data-ttu-id="e9dd3-168">此外，許多應用程式開發介面要求只會傳回小型的內文和 hello 遺失的資訊值，藉由截斷大型主體是相當基本比較 toohello 減少在傳送中，因此處理和儲存體成本 tookeep 所有本文內容。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-168">Also, many API requests only return small bodies and so hello loss of information value by truncating large bodies is fairly minimal in comparison toohello reduction in transfer, processing and storage costs tookeep all body contents.</span></span> <span data-ttu-id="e9dd3-169">最後一個處理 hello 本文的相關注意事項是，我們需要 toopass`true`為 toohello<string>（） 方法因為我們會閱讀 hello 本文內容，但卻是也想 hello 後端 API toobe 無法 tooread hello 主體。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-169">One final note about processing hello body is that we need toopass `true` toohello As<string>() method because we are reading hello body contents, but was also want hello backend API toobe able tooread hello body.</span></span> <span data-ttu-id="e9dd3-170">藉由傳遞 true toothis 方法，我們會導致 hello 主體 toobe 緩衝處理，使它能夠讀取第二次的內容。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-170">By passing true toothis method we cause hello body toobe buffered so that it can be read a second time.</span></span> <span data-ttu-id="e9dd3-171">這是重要 toobe 注意如果您有未上傳的極大型的檔案，或使用長輪詢的 API。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-171">This is important toobe aware of if you have an API that does uploading of very large files or uses long polling.</span></span> <span data-ttu-id="e9dd3-172">在這些情況下將最佳 tooavoid 讀取 hello 主體。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-172">In these cases it would be best tooavoid reading hello body at all.</span></span>   

### <a name="http-headers"></a><span data-ttu-id="e9dd3-173">HTTP 標頭</span><span class="sxs-lookup"><span data-stu-id="e9dd3-173">HTTP headers</span></span>
<span data-ttu-id="e9dd3-174">HTTP 標頭可以只透過傳送 hello 訊息格式，以簡單的索引鍵/值組格式。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-174">HTTP Headers can be simply transferred over into hello message format in a simple key/value pair format.</span></span> <span data-ttu-id="e9dd3-175">我們已選擇特定安全性 toostrip 機密欄位，tooavoid 不必要地洩漏認證資訊。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-175">We have chosen toostrip out certain security sensitive fields, tooavoid unnecessarily leaking credential information.</span></span> <span data-ttu-id="e9dd3-176">API 金鑰及其他認證不太可能用於分析。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-176">It is unlikely that API keys and other credentials would be used for analytics purposes.</span></span> <span data-ttu-id="e9dd3-177">如果我們想 toodo 分析 hello 使用者和特定產品的 hello 他們使用，則我們無法取得從 hello`context`物件，並將該 toohello 訊息。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-177">If we wish toodo analysis on hello user and hello particular product they are using then we could get that from hello `context` object and add that toohello message.</span></span>     

### <a name="message-metadata"></a><span data-ttu-id="e9dd3-178">訊息中繼資料</span><span class="sxs-lookup"><span data-stu-id="e9dd3-178">Message Metadata</span></span>
<span data-ttu-id="e9dd3-179">建置時 hello 完整訊息 toosend toohello 事件中樞，hello 第一行不是實際的部份 hello`application/http`訊息。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-179">When building hello complete message toosend toohello event hub, hello first line is not actually part of hello `application/http` message.</span></span> <span data-ttu-id="e9dd3-180">hello 第一行會組成 hello 訊息是否為要求或回應訊息的其他中繼資料，以及訊息識別碼是使用的 toocorrelate 要求 tooresponses。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-180">hello first line is additional metadata consisting of whether hello message is a request or response message and a message id which is used toocorrelate requests tooresponses.</span></span> <span data-ttu-id="e9dd3-181">建立 hello 訊息識別碼並使用另一個原則，看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="e9dd3-181">hello message id is created by using another policy that looks like this:</span></span>

```xml
<set-variable name="message-id" value="@(Guid.NewGuid())" />
```

<span data-ttu-id="e9dd3-182">我們無法建立儲存在變數中，直到 hello 回應，已傳回並在然後只要 hello 要求和回應以傳送單一訊息的 hello 要求訊息。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-182">We could have created hello request message, stored that in a variable until hello response was returned and then simply sent hello request and response as a single message.</span></span> <span data-ttu-id="e9dd3-183">不過，透過獨立地傳送 hello 要求和回應，並使用訊息識別碼 toocorrelate hello 兩個，我們得到更多的彈性 hello 訊息大小、 hello 能力 tootake 利用多個資料分割維護訊息順序和 hello 儘管要求會出現在記錄儀表板更快。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-183">However, by sending hello request and response independently and using a message id toocorrelate hello two, we get a bit more flexibility in hello message size, hello ability tootake advantage of multiple partitions whilst maintaining message order and hello request will appear in our logging dashboard sooner.</span></span> <span data-ttu-id="e9dd3-184">也可能會有某些情況下，有效的回應永遠不會傳送 toohello 事件中樞，可能是因為 hello API 管理服務，tooa 嚴重的要求發生錯誤，但我們仍會有 hello 要求的記錄。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-184">There also may be some scenarios where a valid response is never sent toohello event hub, possibly due tooa fatal request error in hello API Management service, but we still will have a record of hello request.</span></span>

<span data-ttu-id="e9dd3-185">hello 原則 toosend hello 回應 HTTP 訊息看起來非常類似 toohello 要求，並讓 hello 完成原則組態看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="e9dd3-185">hello policy toosend hello response HTTP message looks very similar toohello request and so hello complete policy configuration looks like this:</span></span>

```xml
<policies>
  <inbound>
      <set-variable name="message-id" value="@(Guid.NewGuid())" />
      <log-to-eventhub logger-id="conferencelogger" partition-id="0">
      @{
          var requestLine = string.Format("{0} {1} HTTP/1.1\r\n",
                                                      context.Request.Method,
                                                      context.Request.Url.Path + context.Request.Url.QueryString);

          var body = context.Request.Body?.As<string>(true);
          if (body != null && body.Length > 1024)
          {
              body = body.Substring(0, 1024);
          }

          var headers = context.Request.Headers
                               .Where(h => h.Key != "Authorization" && h.Key != "Ocp-Apim-Subscription-Key")
                               .Select(h => string.Format("{0}: {1}", h.Key, String.Join(", ", h.Value)))
                               .ToArray<string>();

          var headerString = (headers.Any()) ? string.Join("\r\n", headers) + "\r\n" : string.Empty;

          return "request:"   + context.Variables["message-id"] + "\n"
                              + requestLine + headerString + "\r\n" + body;
      }
  </log-to-eventhub>
  </inbound>
  <backend>
      <forward-request follow-redirects="true" />
  </backend>
  <outbound>
      <log-to-eventhub logger-id="conferencelogger" partition-id="1">
      @{
          var statusLine = string.Format("HTTP/1.1 {0} {1}\r\n",
                                              context.Response.StatusCode,
                                              context.Response.StatusReason);

          var body = context.Response.Body?.As<string>(true);
          if (body != null && body.Length > 1024)
          {
              body = body.Substring(0, 1024);
          }

          var headers = context.Response.Headers
                                          .Select(h => string.Format("{0}: {1}", h.Key, String.Join(", ", h.Value)))
                                          .ToArray<string>();

          var headerString = (headers.Any()) ? string.Join("\r\n", headers) + "\r\n" : string.Empty;

          return "response:"  + context.Variables["message-id"] + "\n"
                              + statusLine + headerString + "\r\n" + body;
     }
  </log-to-eventhub>
  </outbound>
</policies>
```

<span data-ttu-id="e9dd3-186">hello`set-variable`原則會建立值，可以存取這兩個 hello`log-to-eventhub`中 hello 原則`<inbound>`區段和 hello `<outbound>` > 一節。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-186">hello `set-variable` policy creates a value that is accessible by both hello `log-to-eventhub` policy in hello `<inbound>` section and hello `<outbound>` section.</span></span>  

## <a name="receiving-events-from-event-hubs"></a><span data-ttu-id="e9dd3-187">從事件中樞接收事件</span><span class="sxs-lookup"><span data-stu-id="e9dd3-187">Receiving events from Event Hubs</span></span>
<span data-ttu-id="e9dd3-188">從 Azure 事件中心的事件接收使用 hello [AMQP 通訊協定](http://www.amqp.org/)。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-188">Events from Azure Event Hub are received using hello [AMQP protocol](http://www.amqp.org/).</span></span> <span data-ttu-id="e9dd3-189">hello Microsoft 服務匯流排團隊已進行用戶端程式庫可用 toomake hello 取用事件更容易。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-189">hello Microsoft Service Bus team have made client libraries available toomake hello consuming events easier.</span></span> <span data-ttu-id="e9dd3-190">有兩種不同的方法，支援，其中一個正在*直接取用者*且 hello 其他使用 hello`EventProcessorHost`類別。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-190">There are two different approaches supported, one is being a *Direct Consumer* and hello other is using hello `EventProcessorHost` class.</span></span> <span data-ttu-id="e9dd3-191">這兩種方法的範例可以在 hello[事件中心程式設計指南](../event-hubs/event-hubs-programming-guide.md)。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-191">Examples of these two approaches can be found in hello [Event Hubs Programming Guide](../event-hubs/event-hubs-programming-guide.md).</span></span> <span data-ttu-id="e9dd3-192">hello 簡短版本 hello 差異是，`Direct Consumer`可讓您完全控制與 hello`EventProcessorHost`沒有某些 hello 配管工作，但可以讓假設您將處理這些事件的方式。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-192">hello short version of hello differences is, `Direct Consumer` gives you complete control and hello `EventProcessorHost` does some of hello plumbing work for you but makes certain assumptions about how you will process those events.</span></span>  

### <a name="eventprocessorhost"></a><span data-ttu-id="e9dd3-193">EventProcessorHost</span><span class="sxs-lookup"><span data-stu-id="e9dd3-193">EventProcessorHost</span></span>
<span data-ttu-id="e9dd3-194">在此範例中，我們將使用 hello`EventProcessorHost`為了簡單起見，不過它可能不 hello 這個特定案例的最佳選擇。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-194">In this sample, we will use hello `EventProcessorHost` for simplicity, however it may not hello best choice for this particular scenario.</span></span> <span data-ttu-id="e9dd3-195">`EventProcessorHost`沒有 hello 費力並確定您沒有 tooworry 關於執行緒特定的事件處理器類別內的問題。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-195">`EventProcessorHost` does hello hard work of making sure you don't have tooworry about threading issues within a particular event processor class.</span></span> <span data-ttu-id="e9dd3-196">不過，在我們的案例中，我們會直接轉換 hello 訊息 tooanother 格式和傳遞 tooanother 服務使用的非同步方法。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-196">However, in our scenario, we are simply converting hello message tooanother format and passing it along tooanother service using an async method.</span></span> <span data-ttu-id="e9dd3-197">不需要更新共用狀態，因此沒有執行緒問題的風險。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-197">There is no need for updating shared state and therefore no risk of threading issues.</span></span> <span data-ttu-id="e9dd3-198">大部分情況下，`EventProcessorHost`很可能是 hello 最佳選擇，而且很近 hello 更容易選項。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-198">For most scenarios, `EventProcessorHost` is probably hello best choice and it is certainly hello easier option.</span></span>     

### <a name="ieventprocessor"></a><span data-ttu-id="e9dd3-199">IEventProcessor</span><span class="sxs-lookup"><span data-stu-id="e9dd3-199">IEventProcessor</span></span>
<span data-ttu-id="e9dd3-200">當使用 hello 中心概念`EventProcessorHost`是 toocreate hello 的實作`IEventProcessor`包含 hello 方法介面`ProcessEventAsync`。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-200">hello central concept when using `EventProcessorHost` is toocreate a an implementation of hello `IEventProcessor` interface which contains hello method `ProcessEventAsync`.</span></span> <span data-ttu-id="e9dd3-201">該方法的 hello 本質如下所示：</span><span class="sxs-lookup"><span data-stu-id="e9dd3-201">hello essence of that method is shown here:</span></span>

```c#
async Task IEventProcessor.ProcessEventsAsync(PartitionContext context, IEnumerable<EventData> messages)
{

   foreach (EventData eventData in messages)
   {
       _Logger.LogInfo(string.Format("Event received from partition: {0} - {1}", context.Lease.PartitionId,eventData.PartitionKey));

       try
       {
           var httpMessage = HttpMessage.Parse(eventData.GetBodyStream());
           await _MessageContentProcessor.ProcessHttpMessage(httpMessage);
       }
       catch (Exception ex)
       {
           _Logger.LogError(ex.Message);
       }
   }
    ... checkpointing code snipped ...
}
```

<span data-ttu-id="e9dd3-202">EventData 物件清單會傳遞至 hello 方法，並且我們逐一該清單。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-202">A list of EventData objects are passed into hello method and we iterate over that list.</span></span> <span data-ttu-id="e9dd3-203">hello 位元組，每個方法會剖析成 HttpMessage 物件，該物件會傳遞 IHttpMessageProcessor tooan 執行個體。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-203">hello bytes of each method are parsed into a HttpMessage object and that object is passed tooan instance of IHttpMessageProcessor.</span></span>

### <a name="httpmessage"></a><span data-ttu-id="e9dd3-204">HttpMessage</span><span class="sxs-lookup"><span data-stu-id="e9dd3-204">HttpMessage</span></span>
<span data-ttu-id="e9dd3-205">hello`HttpMessage`執行個體包含三個資料片段：</span><span class="sxs-lookup"><span data-stu-id="e9dd3-205">hello `HttpMessage` instance contains three pieces of data:</span></span>

```c#
public class HttpMessage
{
   public Guid MessageId { get; set; }
   public bool IsRequest { get; set; }
   public HttpRequestMessage HttpRequestMessage { get; set; }
   public HttpResponseMessage HttpResponseMessage { get; set; }

... parsing code snipped ...

}
```

<span data-ttu-id="e9dd3-206">hello`HttpMessage`執行個體會包含`MessageId`tooconnect hello HTTP 要求 toohello 對應的 HTTP 回應和布林值，可讓我們的 GUID 識別如果 hello 物件包含執行個體的 HttpRequestMessage，HttpResponseMessage。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-206">hello `HttpMessage` instance contains a `MessageId` GUID that allows us tooconnect hello HTTP request toohello corresponding HTTP response and a boolean value that identifies if hello object contains an instance of a HttpRequestMessage and HttpResponseMessage.</span></span> <span data-ttu-id="e9dd3-207">使用 HTTP 類別，從內建的 hello `System.Net.Http`，已無法 tootake 優點 hello`application/http`剖析程式碼中包含`System.Net.Http.Formatting`。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-207">By using hello built in HTTP classes from `System.Net.Http`, I was able tootake advantage of hello `application/http` parsing code that is included in `System.Net.Http.Formatting`.</span></span>  

### <a name="ihttpmessageprocessor"></a><span data-ttu-id="e9dd3-208">IHttpMessageProcessor</span><span class="sxs-lookup"><span data-stu-id="e9dd3-208">IHttpMessageProcessor</span></span>
<span data-ttu-id="e9dd3-209">hello`HttpMessage`執行個體然後轉送的 tooimplementation`IHttpMessageProcessor`這是我建立 toodecouple hello 接收和解譯的 hello 事件從 Azure 事件中樞與 hello 實際處理它的介面。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-209">hello `HttpMessage` instance is then forwarded tooimplementation of `IHttpMessageProcessor` which is an interface I created toodecouple hello receiving and interpretation of hello event from Azure Event Hub and hello actual processing of it.</span></span>

## <a name="forwarding-hello-http-message"></a><span data-ttu-id="e9dd3-210">轉送 hello HTTP 訊息</span><span class="sxs-lookup"><span data-stu-id="e9dd3-210">Forwarding hello HTTP message</span></span>
<span data-ttu-id="e9dd3-211">此範例中，我決定很有趣 toopush hello HTTP 要求透過太[Runscope](http://www.runscope.com)。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-211">For this sample, I decided it would be interesting toopush hello HTTP Request over too[Runscope](http://www.runscope.com).</span></span> <span data-ttu-id="e9dd3-212">Runscope 是專門從事 HTTP 偵錯、記錄和監視的雲端架構服務。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-212">Runscope is a cloud based service that specializes in HTTP debugging, logging and monitoring.</span></span> <span data-ttu-id="e9dd3-213">它們有免費層次中，因此容易 tootry 且它可讓我們 toosee hello HTTP 要求中即時流經我們的 API 管理服務。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-213">They have a free tier, so it is easy tootry and it allows us toosee hello HTTP requests in real-time flowing through our API Management service.</span></span>

<span data-ttu-id="e9dd3-214">hello`IHttpMessageProcessor`實作看起來像這樣，</span><span class="sxs-lookup"><span data-stu-id="e9dd3-214">hello `IHttpMessageProcessor` implementation looks like this,</span></span>

```c#
public class RunscopeHttpMessageProcessor : IHttpMessageProcessor
{
   private HttpClient _HttpClient;
   private ILogger _Logger;
   private string _BucketKey;
   public RunscopeHttpMessageProcessor(HttpClient httpClient, ILogger logger)
   {
       _HttpClient = httpClient;
       var key = Environment.GetEnvironmentVariable("APIMEVENTS-RUNSCOPE-KEY", EnvironmentVariableTarget.User);
       _HttpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("bearer", key);
       _HttpClient.BaseAddress = new Uri("https://api.runscope.com");
       _BucketKey = Environment.GetEnvironmentVariable("APIMEVENTS-RUNSCOPE-BUCKET", EnvironmentVariableTarget.User);
       _Logger = logger;
   }

   public async Task ProcessHttpMessage(HttpMessage message)
   {
       var runscopeMessage = new RunscopeMessage()
       {
           UniqueIdentifier = message.MessageId
       };

       if (message.IsRequest)
       {
           _Logger.LogInfo("Sending HTTP request " + message.MessageId.ToString());
           runscopeMessage.Request = await RunscopeRequest.CreateFromAsync(message.HttpRequestMessage);
       }
       else
       {
           _Logger.LogInfo("Sending HTTP response " + message.MessageId.ToString());
           runscopeMessage.Response = await RunscopeResponse.CreateFromAsync(message.HttpResponseMessage);
       }

       var messagesLink = new MessagesLink() { Method = HttpMethod.Post };
       messagesLink.BucketKey = _BucketKey;
       messagesLink.RunscopeMessage = runscopeMessage;
       var runscopeResponse = await _HttpClient.SendAsync(messagesLink.CreateRequest());
       _Logger.LogDebug("Request sent tooRunscope");
   }
}
```

<span data-ttu-id="e9dd3-215">我已能 tootake 利用[Runscope 現有用戶端程式庫](http://www.nuget.org/packages/Runscope.net.hapikit/0.9.0-alpha)，能讓您輕鬆 toopush`HttpRequestMessage`和`HttpResponseMessage`到他們的服務執行個體上。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-215">I was able tootake advantage of an [existing client library for Runscope](http://www.nuget.org/packages/Runscope.net.hapikit/0.9.0-alpha) that makes it easy toopush `HttpRequestMessage` and `HttpResponseMessage` instances up into their service.</span></span> <span data-ttu-id="e9dd3-216">順序 tooaccess hello Runscope API，您將需要帳戶和 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-216">In order tooaccess hello Runscope API you will need an account and an API Key.</span></span> <span data-ttu-id="e9dd3-217">取得 API 金鑰可指示 hello[建立應用程式 tooAccess Runscope API](http://blog.runscope.com/posts/creating-applications-to-access-the-runscope-api)錄影畫面。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-217">Instructions for getting an API key can be found in hello [Creating Applications tooAccess Runscope API](http://blog.runscope.com/posts/creating-applications-to-access-the-runscope-api) screencast.</span></span>

## <a name="complete-sample"></a><span data-ttu-id="e9dd3-218">完整範例</span><span class="sxs-lookup"><span data-stu-id="e9dd3-218">Complete sample</span></span>
<span data-ttu-id="e9dd3-219">hello[原始程式碼](https://github.com/darrelmiller/ApimEventProcessor)而 hello 範例的測試是在 GitHub 上。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-219">hello [source code](https://github.com/darrelmiller/ApimEventProcessor) and tests for hello sample are on GitHub.</span></span> <span data-ttu-id="e9dd3-220">您將需要[API 管理服務](api-management-get-started.md)，[連接的事件中樞](api-management-howto-log-event-hubs.md)，和[儲存體帳戶](../storage/common/storage-create-storage-account.md)自行 toorun hello 範例。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-220">You will need an [API Management Service](api-management-get-started.md), [a connected Event Hub](api-management-howto-log-event-hubs.md), and a [Storage Account](../storage/common/storage-create-storage-account.md) toorun hello sample for yourself.</span></span>   

<span data-ttu-id="e9dd3-221">hello 範例是只是簡單主控台應用程式所接聽的事件來自事件中心，將轉換到`HttpRequestMessage`和`HttpResponseMessage`物件，然後再將它們轉送 toohello Runscope 應用程式開發介面上。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-221">hello sample is just a simple Console application that listens for events coming from Event Hub, converts them into a `HttpRequestMessage` and `HttpResponseMessage` objects and then forwards them on toohello Runscope API.</span></span>

<span data-ttu-id="e9dd3-222">在 hello 下列動畫的影像，您可以看到提出的要求正在進行 tooan API 在 hello 開發人員入口網站，hello 主控台應用程式顯示 hello 訊息接收、 處理和轉送，然後 hello 要求和回應 hello Runscope 流量中顯示偵測器。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-222">In hello following animated image, you can see a request being made tooan API in hello Developer Portal, hello Console application showing hello message being received, processed and forwarded and then hello request and response showing up in hello Runscope Traffic inspector.</span></span>

![要求正在轉送 tooRunscope 的示範](./media/api-management-log-to-eventhub-sample/apim-eventhub-runscope.gif)

## <a name="summary"></a><span data-ttu-id="e9dd3-224">摘要</span><span class="sxs-lookup"><span data-stu-id="e9dd3-224">Summary</span></span>
<span data-ttu-id="e9dd3-225">Azure API 管理服務會提供從您的應用程式開發介面移動 tooand 好 toocapture hello HTTP 流量。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-225">Azure API Management service provides an ideal place toocapture hello HTTP traffic travelling tooand from your APIs.</span></span> <span data-ttu-id="e9dd3-226">Azure 事件中樞是一個可高度擴充、低成本的解決方案，用來擷取該流量並將它饋送到次要處理系統中，以便進行記錄、監視和其他複雜的分析。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-226">Azure Event Hubs is a highly scalable, low cost solution for capturing that traffic and feeding it into secondary processing systems for logging, monitoring and other sophisticated analytics.</span></span> <span data-ttu-id="e9dd3-227">連接 too3rd 合作對象流量監視系統，例如 Runscope 數十種少量的程式碼做為簡單。</span><span class="sxs-lookup"><span data-stu-id="e9dd3-227">Connecting too3rd party traffic monitoring systems like Runscope is a simple as a few dozen lines of code.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e9dd3-228">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e9dd3-228">Next steps</span></span>
* <span data-ttu-id="e9dd3-229">深入了解 Azure 事件中樞</span><span class="sxs-lookup"><span data-stu-id="e9dd3-229">Learn more about Azure Event Hubs</span></span>
  * [<span data-ttu-id="e9dd3-230">開始使用 Azure 事件中樞</span><span class="sxs-lookup"><span data-stu-id="e9dd3-230">Get started with Azure Event Hubs</span></span>](../event-hubs/event-hubs-c-getstarted-send.md)
  * [<span data-ttu-id="e9dd3-231">使用 EventProcessorHost 接收訊息</span><span class="sxs-lookup"><span data-stu-id="e9dd3-231">Receive messages with EventProcessorHost</span></span>](../event-hubs/event-hubs-dotnet-standard-getstarted-receive-eph.md)
  * [<span data-ttu-id="e9dd3-232">事件中樞程式設計指南</span><span class="sxs-lookup"><span data-stu-id="e9dd3-232">Event Hubs programming guide</span></span>](../event-hubs/event-hubs-programming-guide.md)
* <span data-ttu-id="e9dd3-233">深入了解 API 管理和事件中樞的整合</span><span class="sxs-lookup"><span data-stu-id="e9dd3-233">Learn more about API Management and Event Hubs integration</span></span>
  * [<span data-ttu-id="e9dd3-234">如何 toolog 事件 tooAzure Azure API 管理中的事件中樞</span><span class="sxs-lookup"><span data-stu-id="e9dd3-234">How toolog events tooAzure Event Hubs in Azure API Management</span></span>](api-management-howto-log-event-hubs.md)
  * [<span data-ttu-id="e9dd3-235">記錄器實體參考</span><span class="sxs-lookup"><span data-stu-id="e9dd3-235">Logger entity reference</span></span>](https://msdn.microsoft.com/library/azure/mt592020.aspx)
  * [<span data-ttu-id="e9dd3-236">log-to-eventhub 原則參考</span><span class="sxs-lookup"><span data-stu-id="e9dd3-236">log-to-eventhub policy reference</span></span>](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub)
