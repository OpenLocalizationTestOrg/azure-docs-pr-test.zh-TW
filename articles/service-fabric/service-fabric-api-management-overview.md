---
title: "Azure Service Fabric 搭配 API 管理概觀 | Microsoft Docs"
description: "本文是使用「Azure API 管理」作為 Service Fabric 應用程式閘道的簡介。"
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 96176149-69bb-4b06-a72e-ebbfea84454b
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/22/2017
ms.author: vturecek
ms.openlocfilehash: a3eedacac5efb53f82e46a56285713dece56ffe8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="service-fabric-with-azure-api-management-overview"></a><span data-ttu-id="e499a-103">Service Fabric 搭配 Azure API 管理概觀</span><span class="sxs-lookup"><span data-stu-id="e499a-103">Service Fabric with Azure API Management overview</span></span>

<span data-ttu-id="e499a-104">雲端應用程式通常需要前端閘道來為使用者、裝置或其他應用程式提供單一輸入點。</span><span class="sxs-lookup"><span data-stu-id="e499a-104">Cloud applications typically need a front-end gateway to provide a single point of ingress for users, devices, or other applications.</span></span> <span data-ttu-id="e499a-105">在 Service Fabric 中，閘道可以是任何無狀態服務 (例如 [ASP.NET Core 應用程式](service-fabric-reliable-services-communication-aspnetcore.md))，或是為流量輸入設計的另一個服務 (例如[事件中樞](https://docs.microsoft.com/azure/event-hubs/)、[IoT 中樞](https://docs.microsoft.com/azure/iot-hub/)或 [Azure API 管理](https://docs.microsoft.com/azure/api-management/))。</span><span class="sxs-lookup"><span data-stu-id="e499a-105">In Service Fabric, a gateway can be any stateless service such as an [ASP.NET Core application](service-fabric-reliable-services-communication-aspnetcore.md), or another service designed for traffic ingress, such as [Event Hubs](https://docs.microsoft.com/azure/event-hubs/), [IoT Hub](https://docs.microsoft.com/azure/iot-hub/), or [Azure API Management](https://docs.microsoft.com/azure/api-management/).</span></span>

<span data-ttu-id="e499a-106">本文是使用「Azure API 管理」作為 Service Fabric 應用程式閘道的簡介。</span><span class="sxs-lookup"><span data-stu-id="e499a-106">This article is an introduction to using Azure API Management as a gateway to your Service Fabric applications.</span></span> <span data-ttu-id="e499a-107">「API 管理」直接與 Service Fabric 整合，可讓您將具有一組豐富路由規則的 API 發佈至後端 Service Fabric 服務。</span><span class="sxs-lookup"><span data-stu-id="e499a-107">API Management integrates directly with Service Fabric, allowing you to publish APIs with a rich set of routing rules to your back-end Service Fabric services.</span></span> 

## <a name="architecture"></a><span data-ttu-id="e499a-108">架構</span><span class="sxs-lookup"><span data-stu-id="e499a-108">Architecture</span></span>
<span data-ttu-id="e499a-109">常見的 Service Fabric 架構會使用單頁 Web 應用程式，此應用程式會對公開 HTTP API 的後端服務發出 HTTP 呼叫。</span><span class="sxs-lookup"><span data-stu-id="e499a-109">A common Service Fabric architecture uses a single-page web application that makes HTTP calls to back-end services that expose HTTP APIs.</span></span> <span data-ttu-id="e499a-110">[Service Fabric 快速入門範例應用程式](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)說明此架構的範例。</span><span class="sxs-lookup"><span data-stu-id="e499a-110">The [Service Fabric getting-started sample application](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started) shows an example of this architecture.</span></span>

<span data-ttu-id="e499a-111">在此案例中，無狀態 Web 服務會作為進入 Service Fabric 應用程式的閘道。</span><span class="sxs-lookup"><span data-stu-id="e499a-111">In this scenario, a stateless web service serves as the gateway into the Service Fabric application.</span></span> <span data-ttu-id="e499a-112">此方法需要您撰寫一個 Web 服務，此服務必須能夠作為 HTTP 要求的 Proxy 來將這些要求傳送到後端服務，如下圖所示：</span><span class="sxs-lookup"><span data-stu-id="e499a-112">This approach requires you to write a web service that can proxy HTTP requests to back-end services, as shown in the following diagram:</span></span>

![Service Fabric 搭配 Azure API 管理拓撲概觀][sf-web-app-stateless-gateway]

<span data-ttu-id="e499a-114">隨著應用程式越來越複雜，必須在各式各樣後端服務前呈現 API 的閘道也越來越複雜。</span><span class="sxs-lookup"><span data-stu-id="e499a-114">As applications grow in complexity, so do the gateways that must present an API in front of myriad back-end services.</span></span> <span data-ttu-id="e499a-115">「Azure API 管理」已設計成讓您花費最少的功夫，即可處理具有路由規則、存取控制、速率限制、監視、事件記錄及回應快取功能的複雜 API。</span><span class="sxs-lookup"><span data-stu-id="e499a-115">Azure API Management is designed to handle complex APIs with routing rules, access control, rate limiting, monitoring, event logging, and response caching with minimal work on your part.</span></span> <span data-ttu-id="e499a-116">「Azure API 管理」支援 Service Fabric 服務探索、分割區解析及複本選取，能夠以智能方式將要求直接路由傳送到 Service Fabric 中的後端服務，讓您無須撰寫自己的無狀態 API 閘道。</span><span class="sxs-lookup"><span data-stu-id="e499a-116">Azure API Management supports Service Fabric service discovery, partition resolution, and replica selection to intelligently route requests directly to back-end services in Service Fabric so you don't have to write your own stateless API gateway.</span></span> 

<span data-ttu-id="e499a-117">在此案例中，仍然是透過 Web 服務來提供 Web UI，以及透過「Azure API 管理」來管理和路由傳送 HTTP API 呼叫，如下圖所示：</span><span class="sxs-lookup"><span data-stu-id="e499a-117">In this scenario, the web UI is still served through a web service, while HTTP API calls are managed and routed through Azure API Management, as shown in the following diagram:</span></span>

![Service Fabric 搭配 Azure API 管理拓撲概觀][sf-apim-web-app]

## <a name="application-scenarios"></a><span data-ttu-id="e499a-119">應用程式案例</span><span class="sxs-lookup"><span data-stu-id="e499a-119">Application scenarios</span></span>

<span data-ttu-id="e499a-120">Service Fabric 中的服務可以是無狀態或具狀態服務，並且可使用下列三種配置之一來加以分割：單一、int-64 範圍及具名。</span><span class="sxs-lookup"><span data-stu-id="e499a-120">Services in Service Fabric may be either stateless or stateful, and they may be partitioned using one of three schemes: singleton, int-64 range, and named.</span></span> <span data-ttu-id="e499a-121">服務端點解析需要識別特定服務執行個體的特定分割區。</span><span class="sxs-lookup"><span data-stu-id="e499a-121">Service endpoint resolution requires identifying a specific partition of a specific service instance.</span></span> <span data-ttu-id="e499a-122">解析服務的端點時，必須同時指定服務執行個體名稱 (例如 `fabric:/myapp/myservice`) 和服務的特定分割區，但單一分割區的情況除外。</span><span class="sxs-lookup"><span data-stu-id="e499a-122">When resolving an endpoint of a service, both the service instance name (for example, `fabric:/myapp/myservice`) as well as the specific partition of the service must be specified, except in the case of singleton partition.</span></span>

<span data-ttu-id="e499a-123">「Azure API 管理」可以與無狀態服務、具狀態服務及任何資料分割配置的任意組合搭配使用。</span><span class="sxs-lookup"><span data-stu-id="e499a-123">Azure API Management can be used with any combination of stateless services, stateful services, and any partitioning scheme.</span></span>

## <a name="send-traffic-to-a-stateless-service"></a><span data-ttu-id="e499a-124">將流量傳送到無狀態服務</span><span class="sxs-lookup"><span data-stu-id="e499a-124">Send traffic to a stateless service</span></span>

<span data-ttu-id="e499a-125">在最簡單的案例中，會將流量轉送到無狀態服務執行個體。</span><span class="sxs-lookup"><span data-stu-id="e499a-125">In the simplest case, traffic is forwarded to a stateless service instance.</span></span> <span data-ttu-id="e499a-126">為了達成此目的，「API 管理」作業會包含一個具有 Service Fabric 後端的輸入處理原則，此後端會對應至 Service Fabric 後端中特定的無狀態服務執行個體。</span><span class="sxs-lookup"><span data-stu-id="e499a-126">To achieve this, an API Management operation contains an inbound processing policy with a Service Fabric back-end that maps to a specific stateless service instance in the Service Fabric back-end.</span></span> <span data-ttu-id="e499a-127">系統會將傳送到該服務的要求傳送到該無狀態服務執行個體地隨機複本。</span><span class="sxs-lookup"><span data-stu-id="e499a-127">Requests sent to that service are sent to a random replica of the stateless service instance.</span></span>

#### <a name="example"></a><span data-ttu-id="e499a-128">範例</span><span class="sxs-lookup"><span data-stu-id="e499a-128">Example</span></span>
<span data-ttu-id="e499a-129">在以下案例中，Service Fabric 應用程式包含一個名為 `fabric:/app/fooservice` 的無狀態服務，此服務會公開內部 HTTP API。</span><span class="sxs-lookup"><span data-stu-id="e499a-129">In the following scenario, a Service Fabric application contains a stateless service named `fabric:/app/fooservice`, that exposes an internal HTTP API.</span></span> <span data-ttu-id="e499a-130">此服務執行個體名稱為已知的名稱，可直接以硬式編碼編寫在「API 管理」輸入處理原則中。</span><span class="sxs-lookup"><span data-stu-id="e499a-130">The service instance name is well known and can be hard-coded directly in the API Management inbound processing policy.</span></span> 

![Service Fabric 搭配 Azure API 管理拓撲概觀][sf-apim-static-stateless]

## <a name="send-traffic-to-a-stateful-service"></a><span data-ttu-id="e499a-132">將流量傳送到具狀態服務</span><span class="sxs-lookup"><span data-stu-id="e499a-132">Send traffic to a stateful service</span></span>

<span data-ttu-id="e499a-133">與無狀態服務案例類似，系統可以將流量轉送到具狀態服務執行個體。</span><span class="sxs-lookup"><span data-stu-id="e499a-133">Similar to the stateless service scenario, traffic can be forwarded to a stateful service instance.</span></span> <span data-ttu-id="e499a-134">在此情況下，「API 管理」作業會包含一個具有 Service Fabric 後端的輸入處理原則，此後端會將要求對應至特定「具狀態」服務執行個體的特定分割區。</span><span class="sxs-lookup"><span data-stu-id="e499a-134">In this case, an API Management operation contains an inbound processing policy with a Service Fabric back-end that maps a request to a specific partition of a specific *stateful* service instance.</span></span> <span data-ttu-id="e499a-135">與每個要求對應的分割區是使用來自傳入 HTTP 要求的一些輸入資料 (例如 URL 路徑中的值) 透過 Lambda 方法計算來得出的。</span><span class="sxs-lookup"><span data-stu-id="e499a-135">The partition to map each request to is computed via a lambda method using some input from the incoming HTTP request, such as a value in the URL path.</span></span> <span data-ttu-id="e499a-136">您可以將原則設定為只將要求傳送到主要複本，或針對讀取作業傳送到隨機複本。</span><span class="sxs-lookup"><span data-stu-id="e499a-136">The policy may be configured to send requests to the primary replica only, or to a random replica for read operations.</span></span>

#### <a name="example"></a><span data-ttu-id="e499a-137">範例</span><span class="sxs-lookup"><span data-stu-id="e499a-137">Example</span></span>

<span data-ttu-id="e499a-138">在以下案例中，Service Fabric 應用程式包含一個名為 `fabric:/app/userservice` 的已分割具狀態服務，此服務會公開內部 HTTP API。</span><span class="sxs-lookup"><span data-stu-id="e499a-138">In the following scenario, a Service Fabric application contains a partitioned stateful service named `fabric:/app/userservice` that exposes an internal HTTP API.</span></span> <span data-ttu-id="e499a-139">此服務執行個體名稱為已知的名稱，可直接以硬式編碼編寫在「API 管理」輸入處理原則中。</span><span class="sxs-lookup"><span data-stu-id="e499a-139">The service instance name is well known and can be hard-coded directly in the API Management inbound processing policy.</span></span>  

<span data-ttu-id="e499a-140">此服務是以 Int64 資料分割配置來分割的，此配置具有兩個分割區及跨 `Int64.MinValue` 到 `Int64.MaxValue` 的索引鍵範圍。</span><span class="sxs-lookup"><span data-stu-id="e499a-140">The service is partitioned using the Int64 partition scheme with two partitions and a key range that spans `Int64.MinValue` to `Int64.MaxValue`.</span></span> <span data-ttu-id="e499a-141">後端原則會透過將 URL 要求路徑中提供的 `id` 值轉換成 64 位元整數，來計算出一個在該範圍內的分割區索引鍵，不過這裡可以使用任何演算法來計算分割區索引鍵。</span><span class="sxs-lookup"><span data-stu-id="e499a-141">The back-end policy computes a partition key within that range by converting the `id` value provided in the URL request path to a 64-bit integer, although any algorithm can be used here to compute the partition key.</span></span> 

![Service Fabric 搭配 Azure API 管理拓撲概觀][sf-apim-static-stateful]

## <a name="send-traffic-to-multiple-stateless-services"></a><span data-ttu-id="e499a-143">將流量傳送到多個無狀態服務</span><span class="sxs-lookup"><span data-stu-id="e499a-143">Send traffic to multiple stateless services</span></span>

<span data-ttu-id="e499a-144">在較進階的案例中，您可以定義一個將要求對應至多個服務執行個體的「API 管理」作業。</span><span class="sxs-lookup"><span data-stu-id="e499a-144">In more advanced scenarios, you can define an API Management operation that maps requests to more than one service instance.</span></span> <span data-ttu-id="e499a-145">在此情況下，每個作業都會包含一個原則，此原則會根據來自傳入 HTTP 要求的值 (例如 URL 路徑或查詢字串) 將要求對應至特定的服務執行個體，而在具狀態服務的案例中，則是會對應至服務執行個體內的分割區。</span><span class="sxs-lookup"><span data-stu-id="e499a-145">In this case, each operation contains a policy that maps requests to a specific service instance based on values from the incoming HTTP request, such as the URL path or query string, and in the case of stateful services, a partition within the service instance.</span></span> 

<span data-ttu-id="e499a-146">為了達成此目的，「API 管理」作業會包含一個具有 Service Fabric 後端的輸入處理原則，此後端會根據從傳入 HTTP 要求擷取到的值，對應至 Service Fabric 後端中的無狀態服務執行個體。</span><span class="sxs-lookup"><span data-stu-id="e499a-146">To achieve this, an API Management operation contains an inbound processing policy with a Service Fabric back-end that maps to a stateless service instance in the Service Fabric back-end based on values retrieved from the incoming HTTP request.</span></span> <span data-ttu-id="e499a-147">系統會將對服務執行個體發出的要求傳送到服務執行個體的隨機複本。</span><span class="sxs-lookup"><span data-stu-id="e499a-147">Requests to a service instance are sent to a random replica of the service instance.</span></span>

#### <a name="example"></a><span data-ttu-id="e499a-148">範例</span><span class="sxs-lookup"><span data-stu-id="e499a-148">Example</span></span>

<span data-ttu-id="e499a-149">在此範例中，會為應用程式的每個使用者都建立一個新的無狀態服務，其中會使用下列公式為這些服務執行個體動態產生名稱：</span><span class="sxs-lookup"><span data-stu-id="e499a-149">In this example, a new stateless service instance is created for each user of an application with a dynamically generated name using the following formula:</span></span>
 
 - `fabric:/app/users/<username>`

 <span data-ttu-id="e499a-150">每個服務都具有唯一的名稱，但並無法事先得知這些名稱，因為是根據使用者或系統管理員的輸入來建立服務，所以無法以硬式編碼編寫在 APIM 原則或路由規則中。</span><span class="sxs-lookup"><span data-stu-id="e499a-150">Each service has a unique name, but the names are not known up-front because the services are created in response to user or admin input and thus cannot be hard-coded into APIM policies or routing rules.</span></span> <span data-ttu-id="e499a-151">取而代之的是，會在後端原則定義中，從 URL 要求路徑中提供的 `name` 值產生作為要求傳送目的地的服務名稱。</span><span class="sxs-lookup"><span data-stu-id="e499a-151">Instead, the name of the service to which to send a request is generated in the back-end policy definition from the `name` value provided in the URL request path.</span></span> <span data-ttu-id="e499a-152">例如：</span><span class="sxs-lookup"><span data-stu-id="e499a-152">For example:</span></span>

  - <span data-ttu-id="e499a-153">對 `/api/users/foo` 發出的要求會路由傳送到服務執行個體 `fabric:/app/users/foo`</span><span class="sxs-lookup"><span data-stu-id="e499a-153">A request to `/api/users/foo` is routed to service instance `fabric:/app/users/foo`</span></span>
  - <span data-ttu-id="e499a-154">對 `/api/users/bar` 發出的要求會路由傳送到服務執行個體 `fabric:/app/users/bar`</span><span class="sxs-lookup"><span data-stu-id="e499a-154">A request to `/api/users/bar` is routed to service instance `fabric:/app/users/bar`</span></span>

![Service Fabric 搭配 Azure API 管理拓撲概觀][sf-apim-dynamic-stateless]

## <a name="send-traffic-to-multiple-stateful-services"></a><span data-ttu-id="e499a-156">將流量傳送到多個具狀態服務</span><span class="sxs-lookup"><span data-stu-id="e499a-156">Send traffic to multiple stateful services</span></span>

<span data-ttu-id="e499a-157">與無狀態服務範例類似，「API 管理」可以將要求對應至多個「具狀態」服務執行個體，在此情況下，您可能也需要為每個具狀態服務執行個體執行分割區解析。</span><span class="sxs-lookup"><span data-stu-id="e499a-157">Similar to the stateless service example, an API Management operation can map requests to more than one **stateful** service instance, in which case you also may need to perform partition resolution for each stateful service instance.</span></span>

<span data-ttu-id="e499a-158">為了達成此目的，「API 管理」作業會包含一個具有 Service Fabric 後端的輸入處理原則，此後端會根據從傳入 HTTP 要求擷取到的值，對應至 Service Fabric 後端中的具狀態服務執行個體。</span><span class="sxs-lookup"><span data-stu-id="e499a-158">To achieve this, an API Management operation contains an inbound processing policy with a Service Fabric back-end that maps to a stateful service instance in the Service Fabric back-end based on values retrieved from the incoming HTTP request.</span></span> <span data-ttu-id="e499a-159">除了將要求對應至特定服務執行個體之外，也可以將要求對應至服務執行個體內的特定分割區，以及視需要對應至分割區內的主要複本或隨機次要複本。</span><span class="sxs-lookup"><span data-stu-id="e499a-159">In addition to mapping a request to specific service instance, the request can also be mapped to a specific partition within the service instance, and optionally to either the primary replica or a random secondary replica within the partition.</span></span>

#### <a name="example"></a><span data-ttu-id="e499a-160">範例</span><span class="sxs-lookup"><span data-stu-id="e499a-160">Example</span></span>

<span data-ttu-id="e499a-161">在此範例中，會為應用程式的每個使用者都建立一個新的具狀態服務，其中會使用下列公式為這些服務執行個體動態產生名稱：</span><span class="sxs-lookup"><span data-stu-id="e499a-161">In this example, a new stateful service instance is created for each user of the application with a dynamically generated name using the following formula:</span></span>
 
 - `fabric:/app/users/<username>`

 <span data-ttu-id="e499a-162">每個服務都具有唯一的名稱，但並無法事先得知這些名稱，因為是根據使用者或系統管理員的輸入來建立服務，所以無法以硬式編碼編寫在 APIM 原則或路由規則中。</span><span class="sxs-lookup"><span data-stu-id="e499a-162">Each service has a unique name, but the names are not known up-front because the services are created in response to user or admin input and thus cannot be hard-coded into APIM policies or routing rules.</span></span> <span data-ttu-id="e499a-163">取而代之的是，會在後端原則定義中，從 URL 要求路徑中提供的 `name` 值產生作為要求傳送目的地的服務名稱。</span><span class="sxs-lookup"><span data-stu-id="e499a-163">Instead, the name of the service to which to send a request is generated in the back-end policy definition from the `name` value provided the URL request path.</span></span> <span data-ttu-id="e499a-164">例如：</span><span class="sxs-lookup"><span data-stu-id="e499a-164">For example:</span></span>

  - <span data-ttu-id="e499a-165">對 `/api/users/foo` 發出的要求會路由傳送到服務執行個體 `fabric:/app/users/foo`</span><span class="sxs-lookup"><span data-stu-id="e499a-165">A request to `/api/users/foo` is routed to service instance `fabric:/app/users/foo`</span></span>
  - <span data-ttu-id="e499a-166">對 `/api/users/bar` 發出的要求會路由傳送到服務執行個體 `fabric:/app/users/bar`</span><span class="sxs-lookup"><span data-stu-id="e499a-166">A request to `/api/users/bar` is routed to service instance `fabric:/app/users/bar`</span></span>

<span data-ttu-id="e499a-167">每個服務執行個體也是以 Int64 資料分割配置來分割的，此配置具有兩個分割區及跨 `Int64.MinValue` 到 `Int64.MaxValue` 的索引鍵範圍。</span><span class="sxs-lookup"><span data-stu-id="e499a-167">Each service instance is also partitioned using the Int64 partition scheme with two partitions and a key range that spans `Int64.MinValue` to `Int64.MaxValue`.</span></span> <span data-ttu-id="e499a-168">後端原則會透過將 URL 要求路徑中提供的 `id` 值轉換成 64 位元整數，來計算出一個在該範圍內的分割區索引鍵，不過這裡可以使用任何演算法來計算分割區索引鍵。</span><span class="sxs-lookup"><span data-stu-id="e499a-168">The back-end policy computes a partition key within that range by converting the `id` value provided in the URL request path to a 64-bit integer, although any algorithm can be used here to compute the partition key.</span></span> 

![Service Fabric 搭配 Azure API 管理拓撲概觀][sf-apim-dynamic-stateful]

## <a name="next-steps"></a><span data-ttu-id="e499a-170">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e499a-170">Next steps</span></span>

<span data-ttu-id="e499a-171">依照[快速入門指南](service-fabric-api-management-quick-start.md)來設定您第一個搭配「API 管理」的 Service Fabric 叢集，並透過「API 管理」將要求傳送到您的服務。</span><span class="sxs-lookup"><span data-stu-id="e499a-171">Follow the [quick start guide](service-fabric-api-management-quick-start.md) to set up your first Service Fabric cluster with API Management and flow requests through API Management to your services.</span></span>

<!-- links -->

<!-- pics -->
[sf-apim-web-app]: ./media/service-fabric-api-management-overview/sf-apim-web-app.png
[sf-web-app-stateless-gateway]: ./media/service-fabric-api-management-overview/sf-web-app-stateless-gateway.png
[sf-apim-static-stateless]: ./media/service-fabric-api-management-overview/sf-apim-static-stateless.png
[sf-apim-static-stateful]: ./media/service-fabric-api-management-overview/sf-apim-static-stateful.png
[sf-apim-dynamic-stateless]: ./media/service-fabric-api-management-overview/sf-apim-dynamic-stateless.png
[sf-apim-dynamic-stateful]: ./media/service-fabric-api-management-overview/sf-apim-dynamic-stateful.png