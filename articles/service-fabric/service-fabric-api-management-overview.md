---
title: "API 管理概觀 aaaAzure Service Fabric |Microsoft 文件"
description: "本文是簡介 toousing Azure API 管理做為閘道 tooyour Service Fabric 應用程式。"
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
ms.openlocfilehash: f01dc570a11e68cd4a2d878abbe6019e209e2f5b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-with-azure-api-management-overview"></a><span data-ttu-id="05f7a-103">Service Fabric 搭配 Azure API 管理概觀</span><span class="sxs-lookup"><span data-stu-id="05f7a-103">Service Fabric with Azure API Management overview</span></span>

<span data-ttu-id="05f7a-104">雲端應用程式通常會需要為使用者、 裝置或其他應用程式前端閘道 tooprovide 輸入的單一點。</span><span class="sxs-lookup"><span data-stu-id="05f7a-104">Cloud applications typically need a front-end gateway tooprovide a single point of ingress for users, devices, or other applications.</span></span> <span data-ttu-id="05f7a-105">在 Service Fabric 中，閘道可以是任何無狀態服務 (例如 [ASP.NET Core 應用程式](service-fabric-reliable-services-communication-aspnetcore.md))，或是為流量輸入設計的另一個服務 (例如[事件中樞](https://docs.microsoft.com/azure/event-hubs/)、[IoT 中樞](https://docs.microsoft.com/azure/iot-hub/)或 [Azure API 管理](https://docs.microsoft.com/azure/api-management/))。</span><span class="sxs-lookup"><span data-stu-id="05f7a-105">In Service Fabric, a gateway can be any stateless service such as an [ASP.NET Core application](service-fabric-reliable-services-communication-aspnetcore.md), or another service designed for traffic ingress, such as [Event Hubs](https://docs.microsoft.com/azure/event-hubs/), [IoT Hub](https://docs.microsoft.com/azure/iot-hub/), or [Azure API Management](https://docs.microsoft.com/azure/api-management/).</span></span>

<span data-ttu-id="05f7a-106">本文是簡介 toousing Azure API 管理做為閘道 tooyour Service Fabric 應用程式。</span><span class="sxs-lookup"><span data-stu-id="05f7a-106">This article is an introduction toousing Azure API Management as a gateway tooyour Service Fabric applications.</span></span> <span data-ttu-id="05f7a-107">API 管理直接整合服務的網狀架構，可讓您使用一組豐富的路由規則 tooyour 後端 Service Fabric 服務 toopublish 應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="05f7a-107">API Management integrates directly with Service Fabric, allowing you toopublish APIs with a rich set of routing rules tooyour back-end Service Fabric services.</span></span> 

## <a name="architecture"></a><span data-ttu-id="05f7a-108">架構</span><span class="sxs-lookup"><span data-stu-id="05f7a-108">Architecture</span></span>
<span data-ttu-id="05f7a-109">常見的 Service Fabric 架構會使用會 HTTP 呼叫 HTTP Api 所公開的 tooback 後端服務的單一頁面的 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="05f7a-109">A common Service Fabric architecture uses a single-page web application that makes HTTP calls tooback-end services that expose HTTP APIs.</span></span> <span data-ttu-id="05f7a-110">hello [Service Fabric 快速入門範例應用程式](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)顯示這個架構的範例。</span><span class="sxs-lookup"><span data-stu-id="05f7a-110">hello [Service Fabric getting-started sample application](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started) shows an example of this architecture.</span></span>

<span data-ttu-id="05f7a-111">在此案例中，無狀態的 web 服務可做為 hello 閘道到 hello Service Fabric 應用程式。</span><span class="sxs-lookup"><span data-stu-id="05f7a-111">In this scenario, a stateless web service serves as hello gateway into hello Service Fabric application.</span></span> <span data-ttu-id="05f7a-112">這個方法會要求 toowrite 可以 proxy HTTP 的 web 服務要求 tooback 後端服務，hello 下列圖表所示：</span><span class="sxs-lookup"><span data-stu-id="05f7a-112">This approach requires you toowrite a web service that can proxy HTTP requests tooback-end services, as shown in hello following diagram:</span></span>

![Service Fabric 搭配 Azure API 管理拓撲概觀][sf-web-app-stateless-gateway]

<span data-ttu-id="05f7a-114">當應用程式變得更複雜，因此請勿 hello 必須出示前面無數的後端服務 API 的閘道。</span><span class="sxs-lookup"><span data-stu-id="05f7a-114">As applications grow in complexity, so do hello gateways that must present an API in front of myriad back-end services.</span></span> <span data-ttu-id="05f7a-115">Azure API 管理是設計的 toohandle 複雜應用程式開發介面與路由規則、 存取控制、 速率限制、 監視、 事件記錄和與您的組件上的最少工作快取回應。</span><span class="sxs-lookup"><span data-stu-id="05f7a-115">Azure API Management is designed toohandle complex APIs with routing rules, access control, rate limiting, monitoring, event logging, and response caching with minimal work on your part.</span></span> <span data-ttu-id="05f7a-116">Azure API 管理支援 Service Fabric 服務探索，資料分割的解析度，以及複本選取 toointelligently 路由要求直接 tooback 後端服務，Service Fabric 中的，您無需 toowrite 無狀態應用程式開發介面閘道。</span><span class="sxs-lookup"><span data-stu-id="05f7a-116">Azure API Management supports Service Fabric service discovery, partition resolution, and replica selection toointelligently route requests directly tooback-end services in Service Fabric so you don't have toowrite your own stateless API gateway.</span></span> 

<span data-ttu-id="05f7a-117">在此案例中，hello 的 web UI 仍能繼續服務透過 web 服務，而 HTTP API 呼叫和管理的裝置 hello 下列圖表所示，透過 Azure API 管理中，路由傳送：</span><span class="sxs-lookup"><span data-stu-id="05f7a-117">In this scenario, hello web UI is still served through a web service, while HTTP API calls are managed and routed through Azure API Management, as shown in hello following diagram:</span></span>

![Service Fabric 搭配 Azure API 管理拓撲概觀][sf-apim-web-app]

## <a name="application-scenarios"></a><span data-ttu-id="05f7a-119">應用程式案例</span><span class="sxs-lookup"><span data-stu-id="05f7a-119">Application scenarios</span></span>

<span data-ttu-id="05f7a-120">Service Fabric 中的服務可以是無狀態或具狀態服務，並且可使用下列三種配置之一來加以分割：單一、int-64 範圍及具名。</span><span class="sxs-lookup"><span data-stu-id="05f7a-120">Services in Service Fabric may be either stateless or stateful, and they may be partitioned using one of three schemes: singleton, int-64 range, and named.</span></span> <span data-ttu-id="05f7a-121">服務端點解析需要識別特定服務執行個體的特定分割區。</span><span class="sxs-lookup"><span data-stu-id="05f7a-121">Service endpoint resolution requires identifying a specific partition of a specific service instance.</span></span> <span data-ttu-id="05f7a-122">當解析服務的端點，同時 hello 服務執行個體名稱 (例如， `fabric:/myapp/myservice`) 也必須指定 hello hello 服務的特定分割區，除非在 hello 案例的單一資料分割。</span><span class="sxs-lookup"><span data-stu-id="05f7a-122">When resolving an endpoint of a service, both hello service instance name (for example, `fabric:/myapp/myservice`) as well as hello specific partition of hello service must be specified, except in hello case of singleton partition.</span></span>

<span data-ttu-id="05f7a-123">「Azure API 管理」可以與無狀態服務、具狀態服務及任何資料分割配置的任意組合搭配使用。</span><span class="sxs-lookup"><span data-stu-id="05f7a-123">Azure API Management can be used with any combination of stateless services, stateful services, and any partitioning scheme.</span></span>

## <a name="send-traffic-tooa-stateless-service"></a><span data-ttu-id="05f7a-124">傳送流量 tooa 無狀態服務</span><span class="sxs-lookup"><span data-stu-id="05f7a-124">Send traffic tooa stateless service</span></span>

<span data-ttu-id="05f7a-125">在 hello 最簡單的情況下，會將流量轉送 tooa 無狀態服務執行個體。</span><span class="sxs-lookup"><span data-stu-id="05f7a-125">In hello simplest case, traffic is forwarded tooa stateless service instance.</span></span> <span data-ttu-id="05f7a-126">tooachieve，API 管理作業包含與 Service Fabric 後端對應 tooa hello Service Fabric 後端中的特定無狀態服務執行個體的輸入的處理原則。</span><span class="sxs-lookup"><span data-stu-id="05f7a-126">tooachieve this, an API Management operation contains an inbound processing policy with a Service Fabric back-end that maps tooa specific stateless service instance in hello Service Fabric back-end.</span></span> <span data-ttu-id="05f7a-127">傳送 toothat 服務的要求會傳送 hello 無狀態服務執行個體的 tooa 隨機複本。</span><span class="sxs-lookup"><span data-stu-id="05f7a-127">Requests sent toothat service are sent tooa random replica of hello stateless service instance.</span></span>

#### <a name="example"></a><span data-ttu-id="05f7a-128">範例</span><span class="sxs-lookup"><span data-stu-id="05f7a-128">Example</span></span>
<span data-ttu-id="05f7a-129">在下列案例中的 hello，Service Fabric 應用程式包含名為無狀態服務`fabric:/app/fooservice`，會公開內部的 HTTP API。</span><span class="sxs-lookup"><span data-stu-id="05f7a-129">In hello following scenario, a Service Fabric application contains a stateless service named `fabric:/app/fooservice`, that exposes an internal HTTP API.</span></span> <span data-ttu-id="05f7a-130">hello 服務執行個體名稱是已知，而且可以是硬式編碼直接 hello 輸入的處理的 API 管理原則。</span><span class="sxs-lookup"><span data-stu-id="05f7a-130">hello service instance name is well known and can be hard-coded directly in hello API Management inbound processing policy.</span></span> 

![Service Fabric 搭配 Azure API 管理拓撲概觀][sf-apim-static-stateless]

## <a name="send-traffic-tooa-stateful-service"></a><span data-ttu-id="05f7a-132">傳送流量 tooa 具狀態服務</span><span class="sxs-lookup"><span data-stu-id="05f7a-132">Send traffic tooa stateful service</span></span>

<span data-ttu-id="05f7a-133">類似的 toohello 無狀態服務案例中，流量可轉送 tooa 可設定狀態的服務執行個體。</span><span class="sxs-lookup"><span data-stu-id="05f7a-133">Similar toohello stateless service scenario, traffic can be forwarded tooa stateful service instance.</span></span> <span data-ttu-id="05f7a-134">API 管理作業在此情況下，包含與 Service Fabric 後端對應的要求 tooa 特定分割區特定的輸入的處理原則*可設定狀態*服務執行個體。</span><span class="sxs-lookup"><span data-stu-id="05f7a-134">In this case, an API Management operation contains an inbound processing policy with a Service Fabric back-end that maps a request tooa specific partition of a specific *stateful* service instance.</span></span> <span data-ttu-id="05f7a-135">透過使用某些 lambda 方法計算每個要求 toois hello 分割 toomap 輸入 hello 傳入 HTTP 要求，例如 hello 中的值從 URL 路徑。</span><span class="sxs-lookup"><span data-stu-id="05f7a-135">hello partition toomap each request toois computed via a lambda method using some input from hello incoming HTTP request, such as a value in hello URL path.</span></span> <span data-ttu-id="05f7a-136">hello 原則可能是設定的 toosend 要求 toohello 主要複本或 tooa 隨機複本用於讀取作業。</span><span class="sxs-lookup"><span data-stu-id="05f7a-136">hello policy may be configured toosend requests toohello primary replica only, or tooa random replica for read operations.</span></span>

#### <a name="example"></a><span data-ttu-id="05f7a-137">範例</span><span class="sxs-lookup"><span data-stu-id="05f7a-137">Example</span></span>

<span data-ttu-id="05f7a-138">在下列案例中的 hello，Service Fabric 應用程式包含名為資料分割的可設定狀態服務`fabric:/app/userservice`會公開內部的 HTTP API。</span><span class="sxs-lookup"><span data-stu-id="05f7a-138">In hello following scenario, a Service Fabric application contains a partitioned stateful service named `fabric:/app/userservice` that exposes an internal HTTP API.</span></span> <span data-ttu-id="05f7a-139">hello 服務執行個體名稱是已知，而且可以是硬式編碼直接 hello 輸入的處理的 API 管理原則。</span><span class="sxs-lookup"><span data-stu-id="05f7a-139">hello service instance name is well known and can be hard-coded directly in hello API Management inbound processing policy.</span></span>  

<span data-ttu-id="05f7a-140">hello 服務已分割使用 hello Int64 資料分割配置，且兩個資料分割和索引鍵的範圍跨越`Int64.MinValue`太`Int64.MaxValue`。</span><span class="sxs-lookup"><span data-stu-id="05f7a-140">hello service is partitioned using hello Int64 partition scheme with two partitions and a key range that spans `Int64.MinValue` too`Int64.MaxValue`.</span></span> <span data-ttu-id="05f7a-141">hello 後端原則會計算該範圍內的資料分割索引鍵轉換 hello `id` hello URL 要求路徑 tooa 64 位元整數，雖然任何演算法可以使用這裡 toocompute hello 資料分割索引鍵所提供的值。</span><span class="sxs-lookup"><span data-stu-id="05f7a-141">hello back-end policy computes a partition key within that range by converting hello `id` value provided in hello URL request path tooa 64-bit integer, although any algorithm can be used here toocompute hello partition key.</span></span> 

![Service Fabric 搭配 Azure API 管理拓撲概觀][sf-apim-static-stateful]

## <a name="send-traffic-toomultiple-stateless-services"></a><span data-ttu-id="05f7a-143">將流量傳送 toomultiple 無狀態服務</span><span class="sxs-lookup"><span data-stu-id="05f7a-143">Send traffic toomultiple stateless services</span></span>

<span data-ttu-id="05f7a-144">在更進階的情況下，您可以定義對應要求 toomore 與一個服務執行個體的 API 管理作業。</span><span class="sxs-lookup"><span data-stu-id="05f7a-144">In more advanced scenarios, you can define an API Management operation that maps requests toomore than one service instance.</span></span> <span data-ttu-id="05f7a-145">在此情況下，每個作業包含對應 tooa 特定服務執行個體根據值 hello 傳入 HTTP 要求，例如 hello URL 路徑或查詢字串，並在 hello 案例中可設定狀態服務，從 hello 服務執行個體內的資料分割的要求原則.</span><span class="sxs-lookup"><span data-stu-id="05f7a-145">In this case, each operation contains a policy that maps requests tooa specific service instance based on values from hello incoming HTTP request, such as hello URL path or query string, and in hello case of stateful services, a partition within hello service instance.</span></span> 

<span data-ttu-id="05f7a-146">tooachieve 此作業包含與 Service Fabric 後端對應 tooa hello Service Fabric 後端根據擷取自 hello 傳入 HTTP 要求的值中的無狀態服務執行個體的輸入的處理原則的 API 管理。</span><span class="sxs-lookup"><span data-stu-id="05f7a-146">tooachieve this, an API Management operation contains an inbound processing policy with a Service Fabric back-end that maps tooa stateless service instance in hello Service Fabric back-end based on values retrieved from hello incoming HTTP request.</span></span> <span data-ttu-id="05f7a-147">要求 tooa 服務執行個體，會傳送 hello 服務執行個體的 tooa 隨機複本。</span><span class="sxs-lookup"><span data-stu-id="05f7a-147">Requests tooa service instance are sent tooa random replica of hello service instance.</span></span>

#### <a name="example"></a><span data-ttu-id="05f7a-148">範例</span><span class="sxs-lookup"><span data-stu-id="05f7a-148">Example</span></span>

<span data-ttu-id="05f7a-149">在此範例中，是每個使用者的應用程式以使用下列公式的 hello 動態產生的名稱建立新的無狀態服務執行個體：</span><span class="sxs-lookup"><span data-stu-id="05f7a-149">In this example, a new stateless service instance is created for each user of an application with a dynamically generated name using hello following formula:</span></span>
 
 - `fabric:/app/users/<username>`

 <span data-ttu-id="05f7a-150">每個服務都有唯一的名稱，但 hello 名稱未知的初期因為 hello 服務會在回應 toouser 中建立或管理輸入，因此無法硬式編碼成 APIM 原則或路由規則。</span><span class="sxs-lookup"><span data-stu-id="05f7a-150">Each service has a unique name, but hello names are not known up-front because hello services are created in response toouser or admin input and thus cannot be hard-coded into APIM policies or routing rules.</span></span> <span data-ttu-id="05f7a-151">而從 hello hello 後端原則定義中產生 hello 服務 toowhich toosend 要求 hello 名稱`name`hello URL 要求路徑中提供的值。</span><span class="sxs-lookup"><span data-stu-id="05f7a-151">Instead, hello name of hello service toowhich toosend a request is generated in hello back-end policy definition from hello `name` value provided in hello URL request path.</span></span> <span data-ttu-id="05f7a-152">例如：</span><span class="sxs-lookup"><span data-stu-id="05f7a-152">For example:</span></span>

  - <span data-ttu-id="05f7a-153">A 要求太`/api/users/foo`路由的 tooservice 執行個體`fabric:/app/users/foo`</span><span class="sxs-lookup"><span data-stu-id="05f7a-153">A request too`/api/users/foo` is routed tooservice instance `fabric:/app/users/foo`</span></span>
  - <span data-ttu-id="05f7a-154">A 要求太`/api/users/bar`路由的 tooservice 執行個體`fabric:/app/users/bar`</span><span class="sxs-lookup"><span data-stu-id="05f7a-154">A request too`/api/users/bar` is routed tooservice instance `fabric:/app/users/bar`</span></span>

![Service Fabric 搭配 Azure API 管理拓撲概觀][sf-apim-dynamic-stateless]

## <a name="send-traffic-toomultiple-stateful-services"></a><span data-ttu-id="05f7a-156">將流量傳送 toomultiple 可設定狀態服務</span><span class="sxs-lookup"><span data-stu-id="05f7a-156">Send traffic toomultiple stateful services</span></span>

<span data-ttu-id="05f7a-157">類似 toohello 無狀態服務的範例，可以將對應作業 API 管理要求比 toomore**可設定狀態**服務執行個體，在此情況下您也可能就需要 tooperform 分割解析為每個可設定狀態的服務執行個體。</span><span class="sxs-lookup"><span data-stu-id="05f7a-157">Similar toohello stateless service example, an API Management operation can map requests toomore than one **stateful** service instance, in which case you also may need tooperform partition resolution for each stateful service instance.</span></span>

<span data-ttu-id="05f7a-158">tooachieve 此作業包含與 Service Fabric 後端對應 tooa hello Service Fabric 後端根據擷取自 hello 傳入 HTTP 要求的值中的可設定狀態的服務執行個體的輸入的處理原則的 API 管理。</span><span class="sxs-lookup"><span data-stu-id="05f7a-158">tooachieve this, an API Management operation contains an inbound processing policy with a Service Fabric back-end that maps tooa stateful service instance in hello Service Fabric back-end based on values retrieved from hello incoming HTTP request.</span></span> <span data-ttu-id="05f7a-159">此外 toomapping 要求 toospecific 服務執行個體，hello 要求也可以是對應的 tooa 內 hello 服務執行個體，並選擇性地 tooeither hello 主要複本的特定資料分割或 hello 磁碟分割內的隨機次要複本。</span><span class="sxs-lookup"><span data-stu-id="05f7a-159">In addition toomapping a request toospecific service instance, hello request can also be mapped tooa specific partition within hello service instance, and optionally tooeither hello primary replica or a random secondary replica within hello partition.</span></span>

#### <a name="example"></a><span data-ttu-id="05f7a-160">範例</span><span class="sxs-lookup"><span data-stu-id="05f7a-160">Example</span></span>

<span data-ttu-id="05f7a-161">在此範例中，新的可設定狀態的服務執行個體使用動態產生的名稱使用下列公式的 hello hello 應用程式的每位使用者建立：</span><span class="sxs-lookup"><span data-stu-id="05f7a-161">In this example, a new stateful service instance is created for each user of hello application with a dynamically generated name using hello following formula:</span></span>
 
 - `fabric:/app/users/<username>`

 <span data-ttu-id="05f7a-162">每個服務都有唯一的名稱，但 hello 名稱未知的初期因為 hello 服務會在回應 toouser 中建立或管理輸入，因此無法硬式編碼成 APIM 原則或路由規則。</span><span class="sxs-lookup"><span data-stu-id="05f7a-162">Each service has a unique name, but hello names are not known up-front because hello services are created in response toouser or admin input and thus cannot be hard-coded into APIM policies or routing rules.</span></span> <span data-ttu-id="05f7a-163">而從 hello hello 後端原則定義中產生 hello 服務 toowhich toosend 要求 hello 名稱`name`提供值 hello URL 要求路徑。</span><span class="sxs-lookup"><span data-stu-id="05f7a-163">Instead, hello name of hello service toowhich toosend a request is generated in hello back-end policy definition from hello `name` value provided hello URL request path.</span></span> <span data-ttu-id="05f7a-164">例如：</span><span class="sxs-lookup"><span data-stu-id="05f7a-164">For example:</span></span>

  - <span data-ttu-id="05f7a-165">A 要求太`/api/users/foo`路由的 tooservice 執行個體`fabric:/app/users/foo`</span><span class="sxs-lookup"><span data-stu-id="05f7a-165">A request too`/api/users/foo` is routed tooservice instance `fabric:/app/users/foo`</span></span>
  - <span data-ttu-id="05f7a-166">A 要求太`/api/users/bar`路由的 tooservice 執行個體`fabric:/app/users/bar`</span><span class="sxs-lookup"><span data-stu-id="05f7a-166">A request too`/api/users/bar` is routed tooservice instance `fabric:/app/users/bar`</span></span>

<span data-ttu-id="05f7a-167">每個服務執行個體也分割使用 hello Int64 資料分割配置，且兩個資料分割和索引鍵的範圍跨越`Int64.MinValue`太`Int64.MaxValue`。</span><span class="sxs-lookup"><span data-stu-id="05f7a-167">Each service instance is also partitioned using hello Int64 partition scheme with two partitions and a key range that spans `Int64.MinValue` too`Int64.MaxValue`.</span></span> <span data-ttu-id="05f7a-168">hello 後端原則會計算該範圍內的資料分割索引鍵轉換 hello `id` hello URL 要求路徑 tooa 64 位元整數，雖然任何演算法可以使用這裡 toocompute hello 資料分割索引鍵所提供的值。</span><span class="sxs-lookup"><span data-stu-id="05f7a-168">hello back-end policy computes a partition key within that range by converting hello `id` value provided in hello URL request path tooa 64-bit integer, although any algorithm can be used here toocompute hello partition key.</span></span> 

![Service Fabric 搭配 Azure API 管理拓撲概觀][sf-apim-dynamic-stateful]

## <a name="next-steps"></a><span data-ttu-id="05f7a-170">後續步驟</span><span class="sxs-lookup"><span data-stu-id="05f7a-170">Next steps</span></span>

<span data-ttu-id="05f7a-171">請遵循 hello[快速入門指南](service-fabric-api-management-quick-start.md)tooset 註冊您的第一個 Service Fabric 叢集 API 管理和流程透過 API 管理 tooyour 服務要求。</span><span class="sxs-lookup"><span data-stu-id="05f7a-171">Follow hello [quick start guide](service-fabric-api-management-quick-start.md) tooset up your first Service Fabric cluster with API Management and flow requests through API Management tooyour services.</span></span>

<!-- links -->

<!-- pics -->
[sf-apim-web-app]: ./media/service-fabric-api-management-overview/sf-apim-web-app.png
[sf-web-app-stateless-gateway]: ./media/service-fabric-api-management-overview/sf-web-app-stateless-gateway.png
[sf-apim-static-stateless]: ./media/service-fabric-api-management-overview/sf-apim-static-stateless.png
[sf-apim-static-stateful]: ./media/service-fabric-api-management-overview/sf-apim-static-stateful.png
[sf-apim-dynamic-stateless]: ./media/service-fabric-api-management-overview/sf-apim-dynamic-stateless.png
[sf-apim-dynamic-stateful]: ./media/service-fabric-api-management-overview/sf-apim-dynamic-stateful.png