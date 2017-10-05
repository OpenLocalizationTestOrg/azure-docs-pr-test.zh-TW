---
title: "使用 Azure API 管理、事件中樞和 Runscope 監視 API | Microsoft Docs"
description: "藉由連接「Azure API 管理」、「Azure 事件中樞」和 Runscope 來進行 HTTP 記錄和監視，示範 log-to-eventhub 原則的範例應用程式"
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
ms.openlocfilehash: 70ee752c5639c90f77dde104ce85eec0a1062300
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="monitor-your-apis-with-azure-api-management-event-hubs-and-runscope"></a><span data-ttu-id="f308e-103">利用 Azure API 管理、事件中樞及 Runscope 監視您的 API</span><span class="sxs-lookup"><span data-stu-id="f308e-103">Monitor your APIs with Azure API Management, Event Hubs and Runscope</span></span>
<span data-ttu-id="f308e-104">[API 管理服務](api-management-key-concepts.md) 提供許多功能，以增強傳送至 HTTP API 之 HTTP 要求的處理。</span><span class="sxs-lookup"><span data-stu-id="f308e-104">The [API Management service](api-management-key-concepts.md) provides many capabilities to enhance the processing of HTTP requests sent to your HTTP API.</span></span> <span data-ttu-id="f308e-105">不過，要求和回應的存在都是暫時的。</span><span class="sxs-lookup"><span data-stu-id="f308e-105">However, the existence of the requests and responses are transient.</span></span> <span data-ttu-id="f308e-106">提出要求並透過 API 管理服務送到您的後端 API。</span><span class="sxs-lookup"><span data-stu-id="f308e-106">The request is made and it flows through the API Management service to your backend API.</span></span> <span data-ttu-id="f308e-107">您的 API 會處理此要求，而回應會傳回給 API 取用者。</span><span class="sxs-lookup"><span data-stu-id="f308e-107">Your API processes the request and a response flows back through to the API consumer.</span></span> <span data-ttu-id="f308e-108">API 管理服務會保留一些重要的 API 相關統計資料，以顯示在發佈者入口網站儀表板上，但除此之外，詳細資料會消失。</span><span class="sxs-lookup"><span data-stu-id="f308e-108">The API Management service keeps some important statistics about the APIs for display in the Publisher portal dashboard, but beyond that, the details are gone.</span></span>

<span data-ttu-id="f308e-109">藉由在「API 管理」服務中使用 [log-to-eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) [原則](api-management-howto-policies.md)，您便可以將任何來自要求和回應的詳細資料傳送到 [Azure 事件中樞](../event-hubs/event-hubs-what-is-event-hubs.md)。</span><span class="sxs-lookup"><span data-stu-id="f308e-109">By using the [log-to-eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) [policy](api-management-howto-policies.md) in the API Management service you can send any details from the request and response to an [Azure Event Hub](../event-hubs/event-hubs-what-is-event-hubs.md).</span></span> <span data-ttu-id="f308e-110">您想要從傳送到您的 API 的 HTTP 訊息產生事件的原因包羅萬象。</span><span class="sxs-lookup"><span data-stu-id="f308e-110">There are a variety of reasons why you may want to generate events from HTTP messages being sent to your APIs.</span></span> <span data-ttu-id="f308e-111">範例包括更新稽核線索、使用量分析、例外狀況警示和協力廠商整合。</span><span class="sxs-lookup"><span data-stu-id="f308e-111">Some examples include audit trail of updates, usage analytics, exception alerting and 3rd party integrations.</span></span>   

<span data-ttu-id="f308e-112">本文將示範如何擷取整個 HTTP 要求和回應訊息、將它傳送到事件中樞，然後將該訊息轉送給可提供 HTTP 記錄和監視服務的協力廠商服務。</span><span class="sxs-lookup"><span data-stu-id="f308e-112">This article demonstrates how to capture the entire HTTP request and response message, send it to an Event Hub and then relay that message to a third party service that provides HTTP logging and monitoring services.</span></span>

## <a name="why-send-from-api-management-service"></a><span data-ttu-id="f308e-113">為什麼要從 API 管理服務傳送？</span><span class="sxs-lookup"><span data-stu-id="f308e-113">Why Send From API Management Service?</span></span>
<span data-ttu-id="f308e-114">您可以撰寫可插入 HTTP API 架構的 HTTP 中介軟體，以擷取 HTTP 要求和回應並將其饋送至記錄和監視系統。</span><span class="sxs-lookup"><span data-stu-id="f308e-114">It is possible to write HTTP middleware that can plug into HTTP API frameworks to capture HTTP requests and responses and feed them into logging and monitoring systems.</span></span> <span data-ttu-id="f308e-115">此方法的缺點是 HTTP 中介軟體必須整合到後端 API 中，而且必須符合 API 的平台。</span><span class="sxs-lookup"><span data-stu-id="f308e-115">The downside to this approach is the HTTP middleware needs to be integrated into the backend API and must match the platform of the API.</span></span> <span data-ttu-id="f308e-116">如果有多個 API，則每個 API 都必須部署中介軟體。</span><span class="sxs-lookup"><span data-stu-id="f308e-116">If there are multiple APIs then each one must deploy the middleware.</span></span> <span data-ttu-id="f308e-117">後端 API 無法升級通常有一些原因。</span><span class="sxs-lookup"><span data-stu-id="f308e-117">Often there are reasons why backend APIs cannot be updated.</span></span>

<span data-ttu-id="f308e-118">使用 Azure API 管理服務來與記錄基礎結構整合，提供了一個集中式且平台獨立的解決方案。</span><span class="sxs-lookup"><span data-stu-id="f308e-118">Using the Azure API Management service to integrate with logging infrastructure provides a centralized and platform-independent solution.</span></span> <span data-ttu-id="f308e-119">在某種程度上藉助 Azure API 管理的 [異地複寫](api-management-howto-deploy-multi-region.md) 功能，也可加以擴充。</span><span class="sxs-lookup"><span data-stu-id="f308e-119">It is also scalable, in part due to the [geo-replication](api-management-howto-deploy-multi-region.md) capabilities of Azure API Management.</span></span>

## <a name="why-send-to-an-azure-event-hub"></a><span data-ttu-id="f308e-120">為什麼要傳送到 Azure 事件中樞？</span><span class="sxs-lookup"><span data-stu-id="f308e-120">Why send to an Azure Event Hub?</span></span>
<span data-ttu-id="f308e-121">合理提問，為何建立 Azure 事件中樞專屬的原則？</span><span class="sxs-lookup"><span data-stu-id="f308e-121">It is a reasonable to ask, why create a policy that is specific to Azure Event Hubs?</span></span> <span data-ttu-id="f308e-122">我可能想要在許多不同的地方記錄我的要求。</span><span class="sxs-lookup"><span data-stu-id="f308e-122">There are many different places where I might want to log my requests.</span></span> <span data-ttu-id="f308e-123">為什麼不能直接將要求傳送到最終目的地？</span><span class="sxs-lookup"><span data-stu-id="f308e-123">Why not just send the requests directly to the final destination?</span></span>  <span data-ttu-id="f308e-124">這是一個選項。</span><span class="sxs-lookup"><span data-stu-id="f308e-124">That is an option.</span></span> <span data-ttu-id="f308e-125">不過，從 API 管理服務提出記錄要求時，就必須考慮記錄訊息對 API 效能有何影響。</span><span class="sxs-lookup"><span data-stu-id="f308e-125">However, when making logging requests from an API management service, it is necessary to consider how logging messages will impact the performance of the API.</span></span> <span data-ttu-id="f308e-126">增加系統元件的可用執行個體或利用異地複寫功能，可以處理逐漸增加的負載。</span><span class="sxs-lookup"><span data-stu-id="f308e-126">Gradual increases in load can be handled by increasing available instances of system components or by taking advantage of geo-replication.</span></span> <span data-ttu-id="f308e-127">不過，如果記錄基礎結構的要求開始變慢而低於負載，則流量短期突增可能會導致大幅延遲要求。</span><span class="sxs-lookup"><span data-stu-id="f308e-127">However, short spikes in traffic can cause requests to be significantly delayed if requests to logging infrastructure start to slow under load.</span></span>

<span data-ttu-id="f308e-128">Azure 事件中樞已設計用來輸入大量資料，其能夠處理的事件數目遠高於大部分 API 所處理的 HTTP 要求數目。</span><span class="sxs-lookup"><span data-stu-id="f308e-128">The Azure Event Hubs is designed to ingress huge volumes of data, with capacity for dealing with a far higher number of events than the number of HTTP requests most APIs process.</span></span> <span data-ttu-id="f308e-129">事件中樞可做為您的 API 管理服務與基礎結構之間有點複雜的緩衝區，將會儲存及處理訊息。</span><span class="sxs-lookup"><span data-stu-id="f308e-129">The Event Hub acts as a kind of sophisticated buffer between your API management service and the infrastructure that will store and process the messages.</span></span> <span data-ttu-id="f308e-130">這可確保您的 API 效能不會因為記錄基礎結構而受到影響。</span><span class="sxs-lookup"><span data-stu-id="f308e-130">This ensures that your API performance will not suffer due to the logging infrastructure.</span></span>  

<span data-ttu-id="f308e-131">資料一旦傳遞至事件中樞，就會保存起來並等待事件中樞取用者進行處理。</span><span class="sxs-lookup"><span data-stu-id="f308e-131">Once the data has been passed to an Event Hub it is persisted and will wait for Event Hub consumers to process it.</span></span> <span data-ttu-id="f308e-132">事件中樞不在乎其處理方式，而只在乎如何確保成功傳遞訊息。</span><span class="sxs-lookup"><span data-stu-id="f308e-132">The Event Hub does not care how it will be processed, it just cares about making sure the message will be successfully delivered.</span></span>     

<span data-ttu-id="f308e-133">事件中樞能夠將事件串流至多個取用者群組。</span><span class="sxs-lookup"><span data-stu-id="f308e-133">Event Hubs have the ability to stream events to multiple consumer groups.</span></span> <span data-ttu-id="f308e-134">如此一來，即可由完全不同的系統來處理事件。</span><span class="sxs-lookup"><span data-stu-id="f308e-134">This allows events to be processed by completely different systems.</span></span> <span data-ttu-id="f308e-135">這麼做能夠支援許多整合案例，而不會對在 API 管理服務中處理 API 要求造成額外延遲，因為只需要產生一個事件。</span><span class="sxs-lookup"><span data-stu-id="f308e-135">This enables supporting many integration scenarios without putting addition delays on the processing of the API request within the API Management service as only one event needs to be generated.</span></span>

## <a name="a-policy-to-send-applicationhttp-messages"></a><span data-ttu-id="f308e-136">用來傳送應用程式/http 訊息的原則</span><span class="sxs-lookup"><span data-stu-id="f308e-136">A policy to send application/http messages</span></span>
<span data-ttu-id="f308e-137">事件中樞接受簡單字串形式的事件資料。</span><span class="sxs-lookup"><span data-stu-id="f308e-137">An Event Hub accepts event data as a simple string.</span></span> <span data-ttu-id="f308e-138">該字串的內容完全由您決定。</span><span class="sxs-lookup"><span data-stu-id="f308e-138">The contents of that string are completely up to you.</span></span> <span data-ttu-id="f308e-139">若要能夠封裝 HTTP 要求並將它傳送至事件中樞，我們需要以要求或回應資訊來格式化字串。</span><span class="sxs-lookup"><span data-stu-id="f308e-139">To be able to package up an HTTP request and send it off to Event Hubs we need to format the string with the request or response information.</span></span> <span data-ttu-id="f308e-140">在這類情況下，如果有我們可重複使用的現有格式，我們就不需要撰寫自己的剖析程式碼。</span><span class="sxs-lookup"><span data-stu-id="f308e-140">In situations like this, if there is an existing format we can reuse, then we may not have to write our own parsing code.</span></span> <span data-ttu-id="f308e-141">一開始，我考慮使用 [HAR](http://www.softwareishard.com/blog/har-12-spec/) 來傳送 HTTP 要求和回應。</span><span class="sxs-lookup"><span data-stu-id="f308e-141">Initially I considered using the [HAR](http://www.softwareishard.com/blog/har-12-spec/) for sending HTTP requests and responses.</span></span> <span data-ttu-id="f308e-142">不過，這種格式最適合用於儲存 JSON 格式的一連串 HTTP 要求。</span><span class="sxs-lookup"><span data-stu-id="f308e-142">However, this format is optimized for storing a sequence of HTTP requests in a JSON based format.</span></span> <span data-ttu-id="f308e-143">其中包含了一些必要元素，讓透過網路傳遞 HTTP 訊息的案例增加了不必要的複雜度。</span><span class="sxs-lookup"><span data-stu-id="f308e-143">It contained a number of mandatory elements that added unnecessary complexity for the scenario of passing the HTTP message over the wire.</span></span>  

<span data-ttu-id="f308e-144">替代選項是使用如 HTTP 規格 [RFC 7230](http://tools.ietf.org/html/rfc7230) 中所述的 `application/http` 媒體類型。</span><span class="sxs-lookup"><span data-stu-id="f308e-144">An alternative option was to use the `application/http` media type as described in the HTTP specification [RFC 7230](http://tools.ietf.org/html/rfc7230).</span></span> <span data-ttu-id="f308e-145">此媒體類型會使用與透過網路用來實際傳送 HTTP 訊息完全相同的格式，但整個訊息可以放在另一個 HTTP 要求的本文中。</span><span class="sxs-lookup"><span data-stu-id="f308e-145">This media type uses the exact same format that is used to actually send HTTP messages over the wire, but the entire message can be put in the body of another HTTP request.</span></span> <span data-ttu-id="f308e-146">在我們的案例中，我們只是會以此本文做為我們的訊息來傳送到事件中樞。</span><span class="sxs-lookup"><span data-stu-id="f308e-146">In our case we are just going to use the body as our message to send to Event Hubs.</span></span> <span data-ttu-id="f308e-147">[Microsoft ASP.NET Web API 2.2 用戶端](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Client/)程式庫中有一個剖析器，可以剖析此格式並將它轉換成原生 `HttpRequestMessage` 和 `HttpResponseMessage` 物件，相當方便。</span><span class="sxs-lookup"><span data-stu-id="f308e-147">Conveniently, there is a parser that exists in [Microsoft ASP.NET Web API 2.2 Client](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Client/) libraries that can parse this format and convert it into the native `HttpRequestMessage` and `HttpResponseMessage` objects.</span></span>

<span data-ttu-id="f308e-148">為了能夠建立此訊息，我們需要在 Azure API 管理中利用以 C# 為基礎的 [原則運算式](https://msdn.microsoft.com/library/azure/dn910913.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="f308e-148">To be able to create this message we need to take advantage of C# based [Policy expressions](https://msdn.microsoft.com/library/azure/dn910913.aspx) in Azure API Management.</span></span> <span data-ttu-id="f308e-149">以下是可將 HTTP 要求訊息傳送到 Azure 事件中樞的原則。</span><span class="sxs-lookup"><span data-stu-id="f308e-149">Here is the policy which sends a HTTP request message to Azure Event Hubs.</span></span>

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

### <a name="policy-declaration"></a><span data-ttu-id="f308e-150">原則宣告</span><span class="sxs-lookup"><span data-stu-id="f308e-150">Policy declaration</span></span>
<span data-ttu-id="f308e-151">此原則運算式有一些值得一提的特別之處。</span><span class="sxs-lookup"><span data-stu-id="f308e-151">There a few particular things worth mentioning about this policy expression.</span></span> <span data-ttu-id="f308e-152">log-to-eventhub 原則有一個名為 logger-id 的屬性，這是指已在 API 管理服務中建立的記錄器名稱。</span><span class="sxs-lookup"><span data-stu-id="f308e-152">The log-to-eventhub policy has an attribute called logger-id which refers to the name of logger that has been created within the API Management service.</span></span> <span data-ttu-id="f308e-153">在 [如何在 Azure API 管理中將事件記錄至 Azure 事件中樞](api-management-howto-log-event-hubs.md)文件中可以找到如何在 API 管理服務中設定事件中樞記錄器的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="f308e-153">The details of how to setup an Event Hub logger in the API Management service can be found in the document [How to log events to Azure Event Hubs in Azure API Management](api-management-howto-log-event-hubs.md).</span></span> <span data-ttu-id="f308e-154">第二個屬性是一個選擇性參數，其指示事件中樞要在哪個資料分割中儲存訊息。</span><span class="sxs-lookup"><span data-stu-id="f308e-154">The second attribute is an optional parameter that instructs Event Hubs which partition to store the message in.</span></span> <span data-ttu-id="f308e-155">事件中樞使用資料分割來達到延展性，而且需要至少兩個資料分割。</span><span class="sxs-lookup"><span data-stu-id="f308e-155">Event Hubs use partitions to enable scalabilty and require a minimum of two.</span></span> <span data-ttu-id="f308e-156">只保證在一個資料分割內的訊息會依序傳遞。</span><span class="sxs-lookup"><span data-stu-id="f308e-156">The ordered delivery of messages is only guaranteed within a partition.</span></span> <span data-ttu-id="f308e-157">如果我們未指示事件中樞要在哪一個資料分割中放置訊息，它會使用循環配置資源演算法來分散負載。</span><span class="sxs-lookup"><span data-stu-id="f308e-157">If we do not instruct Event Hub in which partition to place the message, it will use a round-robin algorithm to distribute the load.</span></span> <span data-ttu-id="f308e-158">不過，這可能導致一些訊息未依順序處理。</span><span class="sxs-lookup"><span data-stu-id="f308e-158">However, that may cause some of our messages to be processed out of order.</span></span>  

### <a name="partitions"></a><span data-ttu-id="f308e-159">分割數</span><span class="sxs-lookup"><span data-stu-id="f308e-159">Partitions</span></span>
<span data-ttu-id="f308e-160">若要確保我們的訊息依序傳遞給取用者並利用資料分割的負載分散功能，我選擇將 HTTP 要求訊息傳送到一個資料分割，將 HTTP 回應訊息傳送到第二個資料分割。</span><span class="sxs-lookup"><span data-stu-id="f308e-160">To ensure our messages are delivered to consumers in order and take advantage of the load distribution capability of partitions, I chose to send HTTP request messages to one partition and HTTP response messages to a second partition.</span></span> <span data-ttu-id="f308e-161">如此可確保負載平均分散，而且我們可以保證所有要求和所有回應都會依序取用。</span><span class="sxs-lookup"><span data-stu-id="f308e-161">This will ensure an even load distribution and we can guarantee that all requests will be consumed in order and all responses will be consumed in order.</span></span> <span data-ttu-id="f308e-162">回應有可能在對應要求之前取用，但這不成問題，因為我們有不同的機制可讓要求與回應相互關聯，而且我們知道要求一律會出現在回應之前。</span><span class="sxs-lookup"><span data-stu-id="f308e-162">It is possible for a response to be consumed before the corresponding request, but as that is not a problem as we have a different mechanism for correlating requests to responses and we know that requests always come before responses.</span></span>

### <a name="http-payloads"></a><span data-ttu-id="f308e-163">HTTP 裝載</span><span class="sxs-lookup"><span data-stu-id="f308e-163">HTTP payloads</span></span>
<span data-ttu-id="f308e-164">在建置 `requestLine` 之後，我們會查看是否應該截斷要求本文。</span><span class="sxs-lookup"><span data-stu-id="f308e-164">After building the `requestLine` we check to see if the request body should be truncated.</span></span> <span data-ttu-id="f308e-165">要求本文會被截斷成只有 1024 個字元。</span><span class="sxs-lookup"><span data-stu-id="f308e-165">The request body is truncated to only 1024.</span></span> <span data-ttu-id="f308e-166">您可以增加此值，不過個別的事件中樞訊息受限於 256 KB，因此有些 HTTP 訊息本文可能會無法放入單一訊息中。</span><span class="sxs-lookup"><span data-stu-id="f308e-166">This could be increased, however individual Event Hub messages are limited to 256KB, so it is likely that some HTTP message bodies will not fit in a single message.</span></span> <span data-ttu-id="f308e-167">進行記錄和分析時，可以從 HTTP 要求行和標頭衍生大量資訊。</span><span class="sxs-lookup"><span data-stu-id="f308e-167">When doing logging and analytics a significant amount of information can be derived from just the HTTP request line and headers.</span></span> <span data-ttu-id="f308e-168">此外，許多 API 要求只會傳回小型本文，所以相較於降低傳輸、處理和儲存成本來保留所有的本文內容，截斷大型本文所造成的資訊值遺失相當微小。</span><span class="sxs-lookup"><span data-stu-id="f308e-168">Also, many API requests only return small bodies and so the loss of information value by truncating large bodies is fairly minimal in comparison to the reduction in transfer, processing and storage costs to keep all body contents.</span></span> <span data-ttu-id="f308e-169">有關處理本文的最後一個注意事項，就是我們必須將 `true` 傳遞至 As<string>() 方法，因為我們正在閱讀本文內容，但也希望後端 API 能夠讀取本文。</span><span class="sxs-lookup"><span data-stu-id="f308e-169">One final note about processing the body is that we need to pass `true` to the As<string>() method because we are reading the body contents, but was also want the backend API to be able to read the body.</span></span> <span data-ttu-id="f308e-170">我們將 true 傳遞至這個方法，造成本文進行緩衝處理，以便第二次讀取本文。</span><span class="sxs-lookup"><span data-stu-id="f308e-170">By passing true to this method we cause the body to be buffered so that it can be read a second time.</span></span> <span data-ttu-id="f308e-171">一定要留意您的 API 是否上傳極大型檔案或使用長輪詢。</span><span class="sxs-lookup"><span data-stu-id="f308e-171">This is important to be aware of if you have an API that does uploading of very large files or uses long polling.</span></span> <span data-ttu-id="f308e-172">在這些情況下，最好完全避免讀取本文。</span><span class="sxs-lookup"><span data-stu-id="f308e-172">In these cases it would be best to avoid reading the body at all.</span></span>   

### <a name="http-headers"></a><span data-ttu-id="f308e-173">HTTP 標頭</span><span class="sxs-lookup"><span data-stu-id="f308e-173">HTTP headers</span></span>
<span data-ttu-id="f308e-174">HTTP 標頭可以直接轉換成採用簡單索引鍵/值組格式的訊息格式。</span><span class="sxs-lookup"><span data-stu-id="f308e-174">HTTP Headers can be simply transferred over into the message format in a simple key/value pair format.</span></span> <span data-ttu-id="f308e-175">我們已選擇刪除某些安全性機密欄位，以避免不必要地洩漏認證資訊。</span><span class="sxs-lookup"><span data-stu-id="f308e-175">We have chosen to strip out certain security sensitive fields, to avoid unnecessarily leaking credential information.</span></span> <span data-ttu-id="f308e-176">API 金鑰及其他認證不太可能用於分析。</span><span class="sxs-lookup"><span data-stu-id="f308e-176">It is unlikely that API keys and other credentials would be used for analytics purposes.</span></span> <span data-ttu-id="f308e-177">如果我們想要分析使用者及其使用的特定產品，我們可以從 `context` 物件取得該方式，然後將它加入至訊息。</span><span class="sxs-lookup"><span data-stu-id="f308e-177">If we wish to do analysis on the user and the particular product they are using then we could get that from the `context` object and add that to the message.</span></span>     

### <a name="message-metadata"></a><span data-ttu-id="f308e-178">訊息中繼資料</span><span class="sxs-lookup"><span data-stu-id="f308e-178">Message Metadata</span></span>
<span data-ttu-id="f308e-179">建立要傳送至事件中樞的完整訊息時，第一行實際上不屬於 `application/http` 訊息。</span><span class="sxs-lookup"><span data-stu-id="f308e-179">When building the complete message to send to the event hub, the first line is not actually part of the `application/http` message.</span></span> <span data-ttu-id="f308e-180">第一行是額外的中繼資料，由訊息是要求或回應訊息以及用來使回應與要求相互關聯的訊息識別碼所組成。</span><span class="sxs-lookup"><span data-stu-id="f308e-180">The first line is additional metadata consisting of whether the message is a request or response message and a message id which is used to correlate requests to responses.</span></span> <span data-ttu-id="f308e-181">使用如下所示的另一個原則，即可建立訊息識別碼：</span><span class="sxs-lookup"><span data-stu-id="f308e-181">The message id is created by using another policy that looks like this:</span></span>

```xml
<set-variable name="message-id" value="@(Guid.NewGuid())" />
```

<span data-ttu-id="f308e-182">我們可能已建立要求訊息，將它儲存在變數中，直到傳回回應為止，然後只不過將要求和回應當作單一訊息傳送。</span><span class="sxs-lookup"><span data-stu-id="f308e-182">We could have created the request message, stored that in a variable until the response was returned and then simply sent the request and response as a single message.</span></span> <span data-ttu-id="f308e-183">不過，獨立傳送要求和回應並使用訊息識別碼讓兩者相互關聯，我們便可取得訊息大小方面的更多彈性，還能夠利用多個資料分割並同時維護訊息順序，而要求將會更快出現在我們的記錄儀表板中。</span><span class="sxs-lookup"><span data-stu-id="f308e-183">However, by sending the request and response independently and using a message id to correlate the two, we get a bit more flexibility in the message size, the ability to take advantage of multiple partitions whilst maintaining message order and the request will appear in our logging dashboard sooner.</span></span> <span data-ttu-id="f308e-184">在某些情況下，有效的回應也可能永遠不會傳送到事件中樞，這可能是因為 API 管理服務發生嚴重要求錯誤，但我們仍有這一筆要求記錄。</span><span class="sxs-lookup"><span data-stu-id="f308e-184">There also may be some scenarios where a valid response is never sent to the event hub, possibly due to a fatal request error in the API Management service, but we still will have a record of the request.</span></span>

<span data-ttu-id="f308e-185">用於傳送回應 HTTP 訊息的原則看起來非常類似要求，所以完整的原則組態如下所示：</span><span class="sxs-lookup"><span data-stu-id="f308e-185">The policy to send the response HTTP message looks very similar to the request and so the complete policy configuration looks like this:</span></span>

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

<span data-ttu-id="f308e-186">`set-variable` 原則會建立一個可供 `<inbound>` 區段和 `<outbound>` 區段中的 `log-to-eventhub` 原則存取的值。</span><span class="sxs-lookup"><span data-stu-id="f308e-186">The `set-variable` policy creates a value that is accessible by both the `log-to-eventhub` policy in the `<inbound>` section and the `<outbound>` section.</span></span>  

## <a name="receiving-events-from-event-hubs"></a><span data-ttu-id="f308e-187">從事件中樞接收事件</span><span class="sxs-lookup"><span data-stu-id="f308e-187">Receiving events from Event Hubs</span></span>
<span data-ttu-id="f308e-188">使用 [AMQP 通訊協定](http://www.amqp.org/)可從 Azure 事件中樞接收事件。</span><span class="sxs-lookup"><span data-stu-id="f308e-188">Events from Azure Event Hub are received using the [AMQP protocol](http://www.amqp.org/).</span></span> <span data-ttu-id="f308e-189">Microsoft 服務匯流排團隊已提供用戶端程式庫，以便取用事件。</span><span class="sxs-lookup"><span data-stu-id="f308e-189">The Microsoft Service Bus team have made client libraries available to make the consuming events easier.</span></span> <span data-ttu-id="f308e-190">支援兩種不同的方法：一個方法是成為「直接取用者」，另一個方法是使用 `EventProcessorHost` 類別。</span><span class="sxs-lookup"><span data-stu-id="f308e-190">There are two different approaches supported, one is being a *Direct Consumer* and the other is using the `EventProcessorHost` class.</span></span> <span data-ttu-id="f308e-191">在 [事件中樞程式設計指南](../event-hubs/event-hubs-programming-guide.md)中可找到這兩種方法的範例。</span><span class="sxs-lookup"><span data-stu-id="f308e-191">Examples of these two approaches can be found in the [Event Hubs Programming Guide](../event-hubs/event-hubs-programming-guide.md).</span></span> <span data-ttu-id="f308e-192">簡而言之，差別在於：`Direct Consumer` 給您完整控制權，而 `EventProcessorHost` 會替您做一些繁雜工作，但會假設您將如何處理這些事件。</span><span class="sxs-lookup"><span data-stu-id="f308e-192">The short version of the differences is, `Direct Consumer` gives you complete control and the `EventProcessorHost` does some of the plumbing work for you but makes certain assumptions about how you will process those events.</span></span>  

### <a name="eventprocessorhost"></a><span data-ttu-id="f308e-193">EventProcessorHost</span><span class="sxs-lookup"><span data-stu-id="f308e-193">EventProcessorHost</span></span>
<span data-ttu-id="f308e-194">在此範例中，我們將使用 `EventProcessorHost` 以求簡化，但是它可能不是此特定案例的最佳選擇。</span><span class="sxs-lookup"><span data-stu-id="f308e-194">In this sample, we will use the `EventProcessorHost` for simplicity, however it may not the best choice for this particular scenario.</span></span> <span data-ttu-id="f308e-195">`EventProcessorHost` 會努力確定您不必擔心特定事件處理器類別內的執行緒問題。</span><span class="sxs-lookup"><span data-stu-id="f308e-195">`EventProcessorHost` does the hard work of making sure you don't have to worry about threading issues within a particular event processor class.</span></span> <span data-ttu-id="f308e-196">不過，在我們的案例中，我們只是將訊息轉換成另一種格式，並使用非同步方法將它傳遞到另一個服務。</span><span class="sxs-lookup"><span data-stu-id="f308e-196">However, in our scenario, we are simply converting the message to another format and passing it along to another service using an async method.</span></span> <span data-ttu-id="f308e-197">不需要更新共用狀態，因此沒有執行緒問題的風險。</span><span class="sxs-lookup"><span data-stu-id="f308e-197">There is no need for updating shared state and therefore no risk of threading issues.</span></span> <span data-ttu-id="f308e-198">在大部分的情況下， `EventProcessorHost` 可能是最佳選擇，當然也是比較容易的選項。</span><span class="sxs-lookup"><span data-stu-id="f308e-198">For most scenarios, `EventProcessorHost` is probably the best choice and it is certainly the easier option.</span></span>     

### <a name="ieventprocessor"></a><span data-ttu-id="f308e-199">IEventProcessor</span><span class="sxs-lookup"><span data-stu-id="f308e-199">IEventProcessor</span></span>
<span data-ttu-id="f308e-200">使用 `EventProcessorHost` 時的中心概念是建立 `IEventProcessor` 介面的實作，其中包含 `ProcessEventAsync` 方法。</span><span class="sxs-lookup"><span data-stu-id="f308e-200">The central concept when using `EventProcessorHost` is to create a an implementation of the `IEventProcessor` interface which contains the method `ProcessEventAsync`.</span></span> <span data-ttu-id="f308e-201">該方法的本質如下所示：</span><span class="sxs-lookup"><span data-stu-id="f308e-201">The essence of that method is shown here:</span></span>

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

<span data-ttu-id="f308e-202">系統會將 EventData 物件清單傳遞至此方法，而我們會逐一查看該清單。</span><span class="sxs-lookup"><span data-stu-id="f308e-202">A list of EventData objects are passed into the method and we iterate over that list.</span></span> <span data-ttu-id="f308e-203">每個方法的位元組會被剖析為 HttpMessage 物件，而該物件會傳遞至 IHttpMessageProcessor 的執行個體。</span><span class="sxs-lookup"><span data-stu-id="f308e-203">The bytes of each method are parsed into a HttpMessage object and that object is passed to an instance of IHttpMessageProcessor.</span></span>

### <a name="httpmessage"></a><span data-ttu-id="f308e-204">HttpMessage</span><span class="sxs-lookup"><span data-stu-id="f308e-204">HttpMessage</span></span>
<span data-ttu-id="f308e-205">`HttpMessage` 執行個體包含三個資料片段：</span><span class="sxs-lookup"><span data-stu-id="f308e-205">The `HttpMessage` instance contains three pieces of data:</span></span>

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

<span data-ttu-id="f308e-206">`HttpMessage` 執行個體包含 `MessageId` GUID，它可讓我們將 HTTP 要求連接到對應的 HTTP 回應和一個布林值 (以識別物件是否包含 HttpRequestMessage 和 HttpResponseMessage 的執行個體)。</span><span class="sxs-lookup"><span data-stu-id="f308e-206">The `HttpMessage` instance contains a `MessageId` GUID that allows us to connect the HTTP request to the corresponding HTTP response and a boolean value that identifies if the object contains an instance of a HttpRequestMessage and HttpResponseMessage.</span></span> <span data-ttu-id="f308e-207">從 `System.Net.Http` 使用內建 HTTP 類別，我才能夠利用 `System.Net.Http.Formatting` 內含的 `application/http` 剖析程式碼。</span><span class="sxs-lookup"><span data-stu-id="f308e-207">By using the built in HTTP classes from `System.Net.Http`, I was able to take advantage of the `application/http` parsing code that is included in `System.Net.Http.Formatting`.</span></span>  

### <a name="ihttpmessageprocessor"></a><span data-ttu-id="f308e-208">IHttpMessageProcessor</span><span class="sxs-lookup"><span data-stu-id="f308e-208">IHttpMessageProcessor</span></span>
<span data-ttu-id="f308e-209">`HttpMessage` 執行個體會接著轉送到 `IHttpMessageProcessor` 的實作，這是我所建立的介面，用於分離事件的接收及解譯與 Azure 事件中樞及其實際處理。</span><span class="sxs-lookup"><span data-stu-id="f308e-209">The `HttpMessage` instance is then forwarded to implementation of `IHttpMessageProcessor` which is an interface I created to decouple the receiving and interpretation of the event from Azure Event Hub and the actual processing of it.</span></span>

## <a name="forwarding-the-http-message"></a><span data-ttu-id="f308e-210">轉送 HTTP 訊息</span><span class="sxs-lookup"><span data-stu-id="f308e-210">Forwarding the HTTP message</span></span>
<span data-ttu-id="f308e-211">在此範例中，我認為將 HTTP 要求推送至 [Runscope](http://www.runscope.com)很有趣。</span><span class="sxs-lookup"><span data-stu-id="f308e-211">For this sample, I decided it would be interesting to push the HTTP Request over to [Runscope](http://www.runscope.com).</span></span> <span data-ttu-id="f308e-212">Runscope 是專門從事 HTTP 偵錯、記錄和監視的雲端架構服務。</span><span class="sxs-lookup"><span data-stu-id="f308e-212">Runscope is a cloud based service that specializes in HTTP debugging, logging and monitoring.</span></span> <span data-ttu-id="f308e-213">該服務有免費層，因此可輕易試用，它可讓我們即時看到流經 API 管理服務的 HTTP 要求。</span><span class="sxs-lookup"><span data-stu-id="f308e-213">They have a free tier, so it is easy to try and it allows us to see the HTTP requests in real-time flowing through our API Management service.</span></span>

<span data-ttu-id="f308e-214">`IHttpMessageProcessor` 實作如下所示：</span><span class="sxs-lookup"><span data-stu-id="f308e-214">The `IHttpMessageProcessor` implementation looks like this,</span></span>

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
       _Logger.LogDebug("Request sent to Runscope");
   }
}
```

<span data-ttu-id="f308e-215">我能夠利用 [Runscope 的現有用戶端程式庫](http://www.nuget.org/packages/Runscope.net.hapikit/0.9.0-alpha)，所以可輕鬆地將 `HttpRequestMessage` 和 `HttpResponseMessage` 執行個體推送到它們的服務中。</span><span class="sxs-lookup"><span data-stu-id="f308e-215">I was able to take advantage of an [existing client library for Runscope](http://www.nuget.org/packages/Runscope.net.hapikit/0.9.0-alpha) that makes it easy to push `HttpRequestMessage` and `HttpResponseMessage` instances up into their service.</span></span> <span data-ttu-id="f308e-216">若要存取 Runscope API，您需有一個帳戶和 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="f308e-216">In order to access the Runscope API you will need an account and an API Key.</span></span> <span data-ttu-id="f308e-217">在 [建立應用程式來存取 Runscope API](http://blog.runscope.com/posts/creating-applications-to-access-the-runscope-api) 螢幕錄製影片中可找到取得 API 金鑰的指示。</span><span class="sxs-lookup"><span data-stu-id="f308e-217">Instructions for getting an API key can be found in the [Creating Applications to Access Runscope API](http://blog.runscope.com/posts/creating-applications-to-access-the-runscope-api) screencast.</span></span>

## <a name="complete-sample"></a><span data-ttu-id="f308e-218">完整範例</span><span class="sxs-lookup"><span data-stu-id="f308e-218">Complete sample</span></span>
<span data-ttu-id="f308e-219">範例的[原始程式碼](https://github.com/darrelmiller/ApimEventProcessor)和測試位於 GitHub 上。</span><span class="sxs-lookup"><span data-stu-id="f308e-219">The [source code](https://github.com/darrelmiller/ApimEventProcessor) and tests for the sample are on GitHub.</span></span> <span data-ttu-id="f308e-220">您將需要 [API 管理服務](api-management-get-started.md)、[已連接的事件中樞](api-management-howto-log-event-hubs.md)及[儲存體帳戶](../storage/common/storage-create-storage-account.md)，才能自行執行此範例。</span><span class="sxs-lookup"><span data-stu-id="f308e-220">You will need an [API Management Service](api-management-get-started.md), [a connected Event Hub](api-management-howto-log-event-hubs.md), and a [Storage Account](../storage/common/storage-create-storage-account.md) to run the sample for yourself.</span></span>   

<span data-ttu-id="f308e-221">此範例只是簡單的主控台應用程式，可接聽來自事件中樞的事件，將它們轉換為 `HttpRequestMessage` 和 `HttpResponseMessage` 物件，然後再轉送到 Runscope API。</span><span class="sxs-lookup"><span data-stu-id="f308e-221">The sample is just a simple Console application that listens for events coming from Event Hub, converts them into a `HttpRequestMessage` and `HttpResponseMessage` objects and then forwards them on to the Runscope API.</span></span>

<span data-ttu-id="f308e-222">在下列動畫影像中，您可以看見正在開發人員入口網站中對 API 提出的要求、顯示正在接收、處理和轉送訊息的主控台應用程式，然後是顯示在 Runscope 流量偵測器中的要求和回應。</span><span class="sxs-lookup"><span data-stu-id="f308e-222">In the following animated image, you can see a request being made to an API in the Developer Portal, the Console application showing the message being received, processed and forwarded and then the request and response showing up in the Runscope Traffic inspector.</span></span>

![示範將要求轉送到 Runscope](./media/api-management-log-to-eventhub-sample/apim-eventhub-runscope.gif)

## <a name="summary"></a><span data-ttu-id="f308e-224">Summary</span><span class="sxs-lookup"><span data-stu-id="f308e-224">Summary</span></span>
<span data-ttu-id="f308e-225">Azure API 管理服務提供了一個理想位置，可供擷取您的 API 的雙向 HTTP 流量。</span><span class="sxs-lookup"><span data-stu-id="f308e-225">Azure API Management service provides an ideal place to capture the HTTP traffic travelling to and from your APIs.</span></span> <span data-ttu-id="f308e-226">Azure 事件中樞是一個可高度擴充、低成本的解決方案，用來擷取該流量並將它饋送到次要處理系統中，以便進行記錄、監視和其他複雜的分析。</span><span class="sxs-lookup"><span data-stu-id="f308e-226">Azure Event Hubs is a highly scalable, low cost solution for capturing that traffic and feeding it into secondary processing systems for logging, monitoring and other sophisticated analytics.</span></span> <span data-ttu-id="f308e-227">連接到協力廠商監視系統 (像是 Runscope) 就像數十行程式碼一樣簡單。</span><span class="sxs-lookup"><span data-stu-id="f308e-227">Connecting to 3rd party traffic monitoring systems like Runscope is a simple as a few dozen lines of code.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f308e-228">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f308e-228">Next steps</span></span>
* <span data-ttu-id="f308e-229">深入了解 Azure 事件中樞</span><span class="sxs-lookup"><span data-stu-id="f308e-229">Learn more about Azure Event Hubs</span></span>
  * [<span data-ttu-id="f308e-230">開始使用 Azure 事件中樞</span><span class="sxs-lookup"><span data-stu-id="f308e-230">Get started with Azure Event Hubs</span></span>](../event-hubs/event-hubs-c-getstarted-send.md)
  * [<span data-ttu-id="f308e-231">使用 EventProcessorHost 接收訊息</span><span class="sxs-lookup"><span data-stu-id="f308e-231">Receive messages with EventProcessorHost</span></span>](../event-hubs/event-hubs-dotnet-standard-getstarted-receive-eph.md)
  * [<span data-ttu-id="f308e-232">事件中樞程式設計指南</span><span class="sxs-lookup"><span data-stu-id="f308e-232">Event Hubs programming guide</span></span>](../event-hubs/event-hubs-programming-guide.md)
* <span data-ttu-id="f308e-233">深入了解 API 管理和事件中樞的整合</span><span class="sxs-lookup"><span data-stu-id="f308e-233">Learn more about API Management and Event Hubs integration</span></span>
  * [<span data-ttu-id="f308e-234">如何將事件記錄到 Azure API 管理中的 Azure 事件中樞</span><span class="sxs-lookup"><span data-stu-id="f308e-234">How to log events to Azure Event Hubs in Azure API Management</span></span>](api-management-howto-log-event-hubs.md)
  * [<span data-ttu-id="f308e-235">記錄器實體參考</span><span class="sxs-lookup"><span data-stu-id="f308e-235">Logger entity reference</span></span>](https://msdn.microsoft.com/library/azure/mt592020.aspx)
  * [<span data-ttu-id="f308e-236">log-to-eventhub 原則參考</span><span class="sxs-lookup"><span data-stu-id="f308e-236">log-to-eventhub policy reference</span></span>](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub)
