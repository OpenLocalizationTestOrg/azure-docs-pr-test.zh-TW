---
title: "使用 ASP.NET Core 的服務通訊 |Microsoft Docs"
description: "了解如何在無狀態和具狀態的 Reliable Services 中使用 ASP.NET Core。"
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 8aa4668d-cbb6-4225-bd2d-ab5925a868f2
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 05/02/2017
ms.author: vturecek
ms.openlocfilehash: 8ac4d409f7363e8b4ae98be659a627ac8db8d787
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="aspnet-core-in-service-fabric-reliable-services"></a><span data-ttu-id="bd12e-103">Service Fabric Reliable Services 中的 ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="bd12e-103">ASP.NET Core in Service Fabric Reliable Services</span></span>

<span data-ttu-id="bd12e-104">ASP.NET Core 是新的開放原始碼和跨平台架構，可建置現代化雲端網際網路連線的應用程式，例如 web 應用程式、IoT 應用程式，以及行動後端。</span><span class="sxs-lookup"><span data-stu-id="bd12e-104">ASP.NET Core is a new open-source and cross-platform framework for building modern cloud-based Internet-connected applications, such as web apps, IoT apps, and mobile backends.</span></span> 

<span data-ttu-id="bd12e-105">本文是深度指南，說明使用**Microsoft.ServiceFabric.AspNetCore.*** NuGet 套件集在Service Fabric Reliable Services 中裝載 ASP.NET Core 服務。</span><span class="sxs-lookup"><span data-stu-id="bd12e-105">This article is an in-depth guide to hosting ASP.NET Core services in Service Fabric Reliable Services using the **Microsoft.ServiceFabric.AspNetCore.*** set of NuGet packages.</span></span>

<span data-ttu-id="bd12e-106">如需 Service Fabric 中 ASP.NET Core 的簡介教學課程，以及如何安裝開發環境設定的指示，請參閱[使用 ASP.NET Core 為應用程式建置 Web 前端應用程式](service-fabric-add-a-web-frontend.md)。</span><span class="sxs-lookup"><span data-stu-id="bd12e-106">For an introductory tutorial on ASP.NET Core in Service Fabric and instructions on getting your development environment set up, see [Building a web front-end for your application using ASP.NET Core](service-fabric-add-a-web-frontend.md).</span></span>

<span data-ttu-id="bd12e-107">本文的其餘部分假設您十分熟悉 ASP.NET Core。</span><span class="sxs-lookup"><span data-stu-id="bd12e-107">The rest of this article assumes you are already familiar with ASP.NET Core.</span></span> <span data-ttu-id="bd12e-108">如果不是，我們建議您閱讀 [ASP.NET Core 基礎](https://docs.microsoft.com/aspnet/core/fundamentals/index)。</span><span class="sxs-lookup"><span data-stu-id="bd12e-108">If not, we recommend reading through the [ASP.NET Core fundamentals](https://docs.microsoft.com/aspnet/core/fundamentals/index).</span></span>

## <a name="aspnet-core-in-the-service-fabric-environment"></a><span data-ttu-id="bd12e-109">Service Fabric 環境中的 ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="bd12e-109">ASP.NET Core in the Service Fabric environment</span></span>

<span data-ttu-id="bd12e-110">雖然 ASP.NET Core 應用程式可以在 .NET Core 或完整的 .NET Framework 上執行，但 Service Fabric 服務目前只能在完整 .NET Framework 上執行。</span><span class="sxs-lookup"><span data-stu-id="bd12e-110">While ASP.NET Core apps can run on .NET Core or on the full .NET Framework, Service Fabric services currently can only run on the full .NET Framework.</span></span> <span data-ttu-id="bd12e-111">這表示當您建置 ASP.NET Core Service Fabric 服務時，仍必須指定完整的 .NET Framework。</span><span class="sxs-lookup"><span data-stu-id="bd12e-111">This means when you build an ASP.NET  Core Service Fabric service, you must still target the full .NET Framework.</span></span>

<span data-ttu-id="bd12e-112">可在 Service Fabric 中以兩種方式使用 ASP.NET Core︰</span><span class="sxs-lookup"><span data-stu-id="bd12e-112">ASP.NET Core can be used in two different ways in Service Fabric:</span></span>
 - <span data-ttu-id="bd12e-113">**裝載作為客體可執行檔**。</span><span class="sxs-lookup"><span data-stu-id="bd12e-113">**Hosted as a guest executable**.</span></span> <span data-ttu-id="bd12e-114">這主要用於在 Service Fabric 上執行現有的 ASP.NET Core 應用程式而無須變更程式碼。</span><span class="sxs-lookup"><span data-stu-id="bd12e-114">This is primarily used to run existing ASP.NET Core applications on Service Fabric with no code changes.</span></span>
 - <span data-ttu-id="bd12e-115">**在 Reliable Service 內部執行**.</span><span class="sxs-lookup"><span data-stu-id="bd12e-115">**Run inside a Reliable Service**.</span></span> <span data-ttu-id="bd12e-116">這可與 Service Fabric 執行階段更緊密整合，並可允許具狀態 ASP.NET Core 服務。</span><span class="sxs-lookup"><span data-stu-id="bd12e-116">This allows better integration with the Service Fabric runtime and allows stateful ASP.NET Core services.</span></span>

<span data-ttu-id="bd12e-117">本文的其餘部分將說明如何使用隨附於 Service Fabric SDK 的 ASP.NET Core 整合元件，在 Reliable Service 內部使用 ASP.NET Core。</span><span class="sxs-lookup"><span data-stu-id="bd12e-117">The rest of this article explains how to use ASP.NET Core inside a Reliable Service using the ASP.NET Core integration components that ship with the Service Fabric SDK.</span></span> 

## <a name="service-fabric-service-hosting"></a><span data-ttu-id="bd12e-118">Service Fabric 服務裝載</span><span class="sxs-lookup"><span data-stu-id="bd12e-118">Service Fabric service hosting</span></span>

<span data-ttu-id="bd12e-119">在 Service Fabric 中，您服務的一或多個執行個體及/或複本會在服務主機處理序中執行，這是執行您的服務程式碼的可執行檔。</span><span class="sxs-lookup"><span data-stu-id="bd12e-119">In Service Fabric, one or more instances and/or replicas of your service run in a *service host process*, an executable file that runs your service code.</span></span> <span data-ttu-id="bd12e-120">您身為服務作者，擁有服務主機處理序，且 Service Fabric 會為您啟動及監視。</span><span class="sxs-lookup"><span data-stu-id="bd12e-120">You, as a service author, own the service host process and Service Fabric activates and monitors it for you.</span></span>

<span data-ttu-id="bd12e-121">傳統 ASP.NET (直到 MVC 5) 已透過 System.Web.dll 與 IIS 緊密結合。</span><span class="sxs-lookup"><span data-stu-id="bd12e-121">Traditional ASP.NET (up to MVC 5) is tightly coupled to IIS through System.Web.dll.</span></span> <span data-ttu-id="bd12e-122">ASP.NET Core 能區別網頁伺服器與 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="bd12e-122">ASP.NET Core provides a separation between the web server and your web application.</span></span> <span data-ttu-id="bd12e-123">這可讓 web 應用程式在不同的 web 伺服器之間具有可攜性，也可讓 web 伺服器自我裝載，這表示您的 web 伺服器可以在自己的程序中啟動，而不是在專用的 web 伺服器軟體所擁有的處理序 (例如 IIS) 中啟動。</span><span class="sxs-lookup"><span data-stu-id="bd12e-123">This allows web applications to be portable between different web servers and also allows web servers to be *self-hosted*, which means you can start a web server in your own process, as opposed to a process that is owned by dedicated web server software such as IIS.</span></span> 

<span data-ttu-id="bd12e-124">為了將 Service Fabric 服務和 ASP.NET 結合為客體可執行檔或結合至 Reliable Service 之中，您必須能夠在服務主機處理序中啟動 ASP.NET。</span><span class="sxs-lookup"><span data-stu-id="bd12e-124">In order to combine a Service Fabric service and ASP.NET, either as a guest executable or in a Reliable Service, you must be able to start ASP.NET inside your service host process.</span></span> <span data-ttu-id="bd12e-125">ASP.NET Core 自我裝載可讓您執行這項操作。</span><span class="sxs-lookup"><span data-stu-id="bd12e-125">ASP.NET Core self-hosting allows you to do this.</span></span>

## <a name="hosting-aspnet-core-in-a-reliable-service"></a><span data-ttu-id="bd12e-126">在 Reliable Service 中裝載 ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="bd12e-126">Hosting ASP.NET Core in a Reliable Service</span></span>
<span data-ttu-id="bd12e-127">一般而言，自我裝載的 ASP.NET Core 應用程式會在應用程式的進入點建立 WebHost，例如 `Program.cs` 方法中的 `static void Main()`。</span><span class="sxs-lookup"><span data-stu-id="bd12e-127">Typically, self-hosted ASP.NET Core applications create a WebHost in an application's entry point, such as the `static void Main()` method in `Program.cs`.</span></span> <span data-ttu-id="bd12e-128">在此情況下，WebHost 的生命週期會繫結至處理序的生命週期。</span><span class="sxs-lookup"><span data-stu-id="bd12e-128">In this case, the lifecycle of the WebHost is bound to the lifecycle of the process.</span></span>

![在處理序中裝載 ASP.NET Core][0]

<span data-ttu-id="bd12e-130">不過，應用程式進入點不是在 Reliable Service 中建立 WebHost 的正確位置，因為應用程式進入點僅用來使用 Service Fabric 執行階段登錄服務類型，因此它可能會建立該服務類型的執行個體。</span><span class="sxs-lookup"><span data-stu-id="bd12e-130">However, the application entry point is not the right place to create a WebHost in a Reliable Service, because the application entry point is only used to register a service type with the Service Fabric runtime, so that it may create instances of that service type.</span></span> <span data-ttu-id="bd12e-131">WebHost 應該建立在 Reliable Service 之內。</span><span class="sxs-lookup"><span data-stu-id="bd12e-131">The WebHost should be created in a Reliable Service itself.</span></span> <span data-ttu-id="bd12e-132">在服務主機處理序中，服務執行個體及/或複本可以通過多個生命週期。</span><span class="sxs-lookup"><span data-stu-id="bd12e-132">Within the service host process, service instances and/or replicas can go through multiple lifecycles.</span></span> 

<span data-ttu-id="bd12e-133">Reliable Service 執行個體是由您衍生自 `StatelessService` 或 `StatefulService` 的服務類別代表。</span><span class="sxs-lookup"><span data-stu-id="bd12e-133">A Reliable Service instance is represented by your service class deriving from `StatelessService` or `StatefulService`.</span></span> <span data-ttu-id="bd12e-134">服務的通訊堆疊包含在您服務類別中的 `ICommunicationListener` 實作。</span><span class="sxs-lookup"><span data-stu-id="bd12e-134">The communication stack for a service is contained in an `ICommunicationListener` implementation in your service class.</span></span> <span data-ttu-id="bd12e-135">`Microsoft.ServiceFabric.Services.AspNetCore.*` NuGet 封裝包含 `ICommunicationListener` 的實作，可在 Reliable Service 中啟動和管理 Kestrel 或 WebListener 的 ASP.NET Core WebHost。</span><span class="sxs-lookup"><span data-stu-id="bd12e-135">The `Microsoft.ServiceFabric.Services.AspNetCore.*` NuGet packages contain implementations of `ICommunicationListener` that start and manage the ASP.NET Core WebHost for either Kestrel or WebListener in a Reliable Service.</span></span>

![在 Reliable Service 中裝載 ASP.NET Core][1]

## <a name="aspnet-core-icommunicationlisteners"></a><span data-ttu-id="bd12e-137">ASP.NET Core ICommunicationListeners</span><span class="sxs-lookup"><span data-stu-id="bd12e-137">ASP.NET Core ICommunicationListeners</span></span>
<span data-ttu-id="bd12e-138">`Microsoft.ServiceFabric.Services.AspNetCore.*` NuGet 套件中 Kestrel 和 WebListener 的 `ICommunicationListener` 實作有類似的使用模式，但針對每個 web 伺服器執行的動作稍有不同。</span><span class="sxs-lookup"><span data-stu-id="bd12e-138">The `ICommunicationListener` implementations for Kestrel and WebListener in the  `Microsoft.ServiceFabric.Services.AspNetCore.*` NuGet packages have similar use patterns but perform slightly different actions specific to each web server.</span></span> 

<span data-ttu-id="bd12e-139">這兩種通訊接聽程式都會提供使用下列引數的建構函式︰</span><span class="sxs-lookup"><span data-stu-id="bd12e-139">Both communication listeners provide a constructor that takes the following arguments:</span></span>
 - <span data-ttu-id="bd12e-140">**`ServiceContext serviceContext`**包含關於執行服務資訊的 `ServiceContext` 物件。</span><span class="sxs-lookup"><span data-stu-id="bd12e-140">**`ServiceContext serviceContext`**: The `ServiceContext` object that contains information about the running service.</span></span>
 - <span data-ttu-id="bd12e-141">**`string endpointName`**：在 ServiceManifest.xml 中的 `Endpoint` 組態名稱。</span><span class="sxs-lookup"><span data-stu-id="bd12e-141">**`string endpointName`**: the name of an `Endpoint` configuration in ServiceManifest.xml.</span></span> <span data-ttu-id="bd12e-142">這是兩個通訊接聽程式主要的不同之處︰WebListener **需要** `Endpoint` 組態，而 Kestrel 不需要。</span><span class="sxs-lookup"><span data-stu-id="bd12e-142">This is primarily where the two communication listeners differ: WebListener **requires** an `Endpoint` configuration, while Kestrel does not.</span></span>
 - <span data-ttu-id="bd12e-143">**`Func<string, AspNetCoreCommunicationListener, IWebHost> build`**：您所實作並在其中建立並傳回 `IWebHost` 的 lambda。</span><span class="sxs-lookup"><span data-stu-id="bd12e-143">**`Func<string, AspNetCoreCommunicationListener, IWebHost> build`**: a lambda that you implement in which you create and return an `IWebHost`.</span></span> <span data-ttu-id="bd12e-144">這可讓您以您通常會在 ASP.NET Core 應用程式的方式設定 `IWebHost`。</span><span class="sxs-lookup"><span data-stu-id="bd12e-144">This allows you to configure `IWebHost` the way you normally would in an ASP.NET Core application.</span></span> <span data-ttu-id="bd12e-145">Lambda 提供為您根據 Service Fabric 整合選項所產生的 URL 和您提供的 `Endpoint` 組態。</span><span class="sxs-lookup"><span data-stu-id="bd12e-145">The lambda provides a URL which is generated for you depending on the Service Fabric integration options you use and the `Endpoint` configuration you provide.</span></span> <span data-ttu-id="bd12e-146">然後該 URL 可以修改或依現狀使用以啟動 web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="bd12e-146">That URL can then be modified or used as-is to start the web server.</span></span>

## <a name="service-fabric-integration-middleware"></a><span data-ttu-id="bd12e-147">Service Fabric 整合中介軟體</span><span class="sxs-lookup"><span data-stu-id="bd12e-147">Service Fabric integration middleware</span></span>
<span data-ttu-id="bd12e-148">`Microsoft.ServiceFabric.Services.AspNetCore` NuGet 套件包含 `IWebHostBuilder` 上的 `UseServiceFabricIntegration` 擴充方法，其會新增 Service Fabric 的中介軟體。</span><span class="sxs-lookup"><span data-stu-id="bd12e-148">The `Microsoft.ServiceFabric.Services.AspNetCore` NuGet package includes the `UseServiceFabricIntegration` extension method on `IWebHostBuilder` that adds Service Fabric-aware middleware.</span></span> <span data-ttu-id="bd12e-149">此中介軟體會設定 Kestrel 或 WebListener `ICommunicationListener`，以使用 Service Fabric 命名服務註冊唯一服務 URL，然後驗證用戶端要求以確保用戶端連線至正確的服務。</span><span class="sxs-lookup"><span data-stu-id="bd12e-149">This middleware configures the Kestrel or WebListener `ICommunicationListener` to register a unique service URL with the Service Fabric Naming Service and then validates client requests to ensure clients are connecting to the right service.</span></span> <span data-ttu-id="bd12e-150">這在共用主機環境 (例如 Service Fabric) 中是必要的，其中多個 web 應用程式可以在相同的實體或虛擬機器上執行，但請勿使用唯一的主機名稱，以避免用戶端不小心連線到錯誤的服務。</span><span class="sxs-lookup"><span data-stu-id="bd12e-150">This is necessary in a shared-host environment such as Service Fabric, where multiple web applications can run on the same physical or virtual machine but do not use unique host names, to prevent clients from mistakenly connecting to the wrong service.</span></span> <span data-ttu-id="bd12e-151">此案例會在下一節中詳細說明。</span><span class="sxs-lookup"><span data-stu-id="bd12e-151">This scenario is described in more detail in the next section.</span></span>

### <a name="a-case-of-mistaken-identity"></a><span data-ttu-id="bd12e-152">誤用身分識別的案例</span><span class="sxs-lookup"><span data-stu-id="bd12e-152">A case of mistaken identity</span></span>
<span data-ttu-id="bd12e-153">不論通訊協定，服務複本會接聽唯一 IP:port 組合。</span><span class="sxs-lookup"><span data-stu-id="bd12e-153">Service replicas, regardless of protocol, listen on a unique IP:port combination.</span></span> <span data-ttu-id="bd12e-154">一旦服務複本開始在 IP:port 端點上接聽，它會向 Service Fabric 命名服務報告該端點位址，用戶端或其他服務可以在其中探索。</span><span class="sxs-lookup"><span data-stu-id="bd12e-154">Once a service replica has started listening on an IP:port endpoint, it reports that endpoint address to the Service Fabric Naming Service where it can be discovered by clients or other services.</span></span> <span data-ttu-id="bd12e-155">如果服務使用動態指派的應用程式連接埠，服務複本可能會針對先前碰巧位於相同實體或虛擬機器上的其他服務，而誤用其 IP:port 端點。</span><span class="sxs-lookup"><span data-stu-id="bd12e-155">If services use dynamically-assigned application ports, a service replica may coincidentally use the same IP:port endpoint of another service that was previously on the same physical or virtual machine.</span></span> <span data-ttu-id="bd12e-156">這可能會造成用戶端不小心連線至錯誤的服務。</span><span class="sxs-lookup"><span data-stu-id="bd12e-156">This can cause a client to mistakely connect to the wrong service.</span></span> <span data-ttu-id="bd12e-157">如果以下一連串事件發生，則可能發生這個情況︰</span><span class="sxs-lookup"><span data-stu-id="bd12e-157">This can happen if the following sequence of events occur:</span></span>

 1. <span data-ttu-id="bd12e-158">服務 A 透過 HTTP 接聽 10.0.0.1:30000。</span><span class="sxs-lookup"><span data-stu-id="bd12e-158">Service A listens on 10.0.0.1:30000 over HTTP.</span></span> 
 2. <span data-ttu-id="bd12e-159">用戶端解析服務 A 並取得位址 10.0.0.1:30000</span><span class="sxs-lookup"><span data-stu-id="bd12e-159">Client resolves Service A and gets address 10.0.0.1:30000</span></span>
 3. <span data-ttu-id="bd12e-160">服務 A 移到另一個節點。</span><span class="sxs-lookup"><span data-stu-id="bd12e-160">Service A moves to a different node.</span></span>
 4. <span data-ttu-id="bd12e-161">服務 B 置於 10.0.0.1 且碰巧使用相同的連接埠 30000。</span><span class="sxs-lookup"><span data-stu-id="bd12e-161">Service B is placed on 10.0.0.1 and coincidentally uses the same port 30000.</span></span>
 5. <span data-ttu-id="bd12e-162">用戶端使用快取的位址 10.0.0.1:30000 嘗試連線到服務 A。</span><span class="sxs-lookup"><span data-stu-id="bd12e-162">Client attempts to connect to service A with cached address 10.0.0.1:30000.</span></span>
 6. <span data-ttu-id="bd12e-163">用戶端現在已成功連接至 B，不瞭解其連線到錯誤的服務。</span><span class="sxs-lookup"><span data-stu-id="bd12e-163">Client is now successfully connected to service B not realizing it is connected to the wrong service.</span></span>

<span data-ttu-id="bd12e-164">這會不定時造成 難以診斷的 Bug。</span><span class="sxs-lookup"><span data-stu-id="bd12e-164">This can cause bugs at random times that can be difficult to diagnose.</span></span> 

### <a name="using-unique-service-urls"></a><span data-ttu-id="bd12e-165">使用唯一的服務 URL</span><span class="sxs-lookup"><span data-stu-id="bd12e-165">Using unique service URLs</span></span>
<span data-ttu-id="bd12e-166">若要避免這個問題，服務可以使用唯一識別碼將端點張貼至命名服務，並在用戶端要求期間驗證該唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="bd12e-166">To prevent this, services can post an endpoint to the Naming Service with a unique identifier, and then validate that unique identifier during client requests.</span></span> <span data-ttu-id="bd12e-167">這在非惡意租用戶受信任環境中的服務之間為合作式動作。</span><span class="sxs-lookup"><span data-stu-id="bd12e-167">This is a cooperative action between services in a non-hostile-tenant trusted environment.</span></span> <span data-ttu-id="bd12e-168">這在惡意租用戶環境中不會提供安全服務驗證。</span><span class="sxs-lookup"><span data-stu-id="bd12e-168">This does not provide secure service authentication in a hostile-tenant environment.</span></span>

<span data-ttu-id="bd12e-169">在受信任環境中，由 `UseServiceFabricIntegration` 法所新增的中介軟體會自動將唯一識別項附加到已張貼至命名服務的地址，並在每個要求上驗證該識別項。</span><span class="sxs-lookup"><span data-stu-id="bd12e-169">In a trusted environment, the middleware that's added by the `UseServiceFabricIntegration` method automatically appends a unique identifier to the address that is posted to the Naming Service and validates that identifier on each request.</span></span> <span data-ttu-id="bd12e-170">如果識別項不符合，中介軟體會立即傳回 HTTP 410 不存在的回應。</span><span class="sxs-lookup"><span data-stu-id="bd12e-170">If the identifier does not match, the middleware immediately returns an HTTP 410 Gone response.</span></span>

<span data-ttu-id="bd12e-171">使用動態指派連接埠的服務應該要使用此中介軟體。</span><span class="sxs-lookup"><span data-stu-id="bd12e-171">Services that use a dynamically-assigned port should make use of this middleware.</span></span>

<span data-ttu-id="bd12e-172">使用固定的唯一連接埠之服務在合作的環境中沒有這個問題。</span><span class="sxs-lookup"><span data-stu-id="bd12e-172">Services that use a fixed unique port do not have this problem in a cooperative environment.</span></span> <span data-ttu-id="bd12e-173">固定的唯一連接埠通常是用於對外開放的服務，需要用戶端應用程式連線的知名通訊埠。</span><span class="sxs-lookup"><span data-stu-id="bd12e-173">A fixed unique port is typically used for externally-facing services that need a well-known port for client applications to connect to.</span></span> <span data-ttu-id="bd12e-174">例如，大部分對網際網路開放的 web 應用程式會使用 web 瀏覽器連接的連接埠 80 或 443。</span><span class="sxs-lookup"><span data-stu-id="bd12e-174">For example, most Internet-facing web applications will use port 80 or 443 for web browser connections.</span></span> <span data-ttu-id="bd12e-175">在此情況下，不應該啟用唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="bd12e-175">In this case, the unique identifier should not be enabled.</span></span>

<span data-ttu-id="bd12e-176">下圖顯示已啟用中介軟體的要求流程︰</span><span class="sxs-lookup"><span data-stu-id="bd12e-176">The following diagram shows the request flow with the middleware enabled:</span></span>

![Service Fabric ASP.NET Core 整合][2]

<span data-ttu-id="bd12e-178">Kestrel 和 WebListener `ICommunicationListener` 實作以完全相同的方式使用這項機制。</span><span class="sxs-lookup"><span data-stu-id="bd12e-178">Both Kestrel and WebListener `ICommunicationListener` implementations use this mechanism in exactly the same way.</span></span> <span data-ttu-id="bd12e-179">雖然 WebListener 可以使用基礎 http.sys 連接埠共用功能，根據唯一的 URL 路徑內部區分要求，該功能不供 WebListener`ICommunicationListener` 實作使用，因為會導致在稍早所述的案例中的 HTTP 503 和 HTTP 404 錯誤狀態碼。</span><span class="sxs-lookup"><span data-stu-id="bd12e-179">Although WebListener can internally differentiate requests based on unique URL paths using the underlying *http.sys* port sharing feature, that functionality is *not* used by the WebListener `ICommunicationListener` implementation because that will result in HTTP 503 and HTTP 404 error status codes in the scenario described earlier.</span></span> <span data-ttu-id="bd12e-180">這會使用戶端很難判斷錯誤的意圖，因為 HTTP 503 和 HTTP 404 已經常用來表示其他錯誤。</span><span class="sxs-lookup"><span data-stu-id="bd12e-180">That in turn makes it very difficult for clients to determine the intent of the error, as HTTP 503 and HTTP 404 are already commonly used to indicate other errors.</span></span> <span data-ttu-id="bd12e-181">因此，Kestrel 和 WebListener `ICommunicationListener` 實作會在 `UseServiceFabricIntegration` 擴充方法所提供的中介軟體上標準化，讓用戶端只需在 HTTP 410 回應上執行服務端點重新解析動作。</span><span class="sxs-lookup"><span data-stu-id="bd12e-181">Thus, both Kestrel and WebListener `ICommunicationListener` implementations standardize on the middleware provided by the `UseServiceFabricIntegration` extension method so that clients only need to perform a service endpoint re-resolve action on HTTP 410 responses.</span></span>

## <a name="weblistener-in-reliable-services"></a><span data-ttu-id="bd12e-182">Reliable Services 中的 WebListener</span><span class="sxs-lookup"><span data-stu-id="bd12e-182">WebListener in Reliable Services</span></span>
<span data-ttu-id="bd12e-183">WebListener 可在 Reliable Service 中使用，方法為匯入 **Microsoft.ServiceFabric.AspNetCore.WebListener** NuGet 封裝。</span><span class="sxs-lookup"><span data-stu-id="bd12e-183">WebListener can be used in a Reliable Service by importing the **Microsoft.ServiceFabric.AspNetCore.WebListener** NuGet package.</span></span> <span data-ttu-id="bd12e-184">此套件包含 `WebListenerCommunicationListener`，實作`ICommunicationListener`，可讓您使用 WebListener 做為 web 伺服器，在 Reliable Service 內部建立 ASP.NET Core WebHost。</span><span class="sxs-lookup"><span data-stu-id="bd12e-184">This package contains `WebListenerCommunicationListener`, an implementation of `ICommunicationListener`, that allows you to create an ASP.NET Core WebHost inside a Reliable Service using WebListener as the web server.</span></span>

<span data-ttu-id="bd12e-185">WebListener 會建置在 [Windows HTTP Server API](https://msdn.microsoft.com/library/windows/desktop/aa364510(v=vs.85).aspx)上。</span><span class="sxs-lookup"><span data-stu-id="bd12e-185">WebListener is built on the [Windows HTTP Server API](https://msdn.microsoft.com/library/windows/desktop/aa364510(v=vs.85).aspx).</span></span> <span data-ttu-id="bd12e-186">這會使用 IIS 用來處理 HTTP 要求並將它們路由傳送到執行 web 應用程式之處理程序的 http.sys 的核心驅動程式。</span><span class="sxs-lookup"><span data-stu-id="bd12e-186">This uses the *http.sys* kernel driver used by IIS to process HTTP requests and route them to processes running web applications.</span></span> <span data-ttu-id="bd12e-187">這可讓相同實體或虛擬機器上的多個處理序在相同的連接埠上裝載 web 應用程式，由唯一的 URL 路徑或主機名稱區分。</span><span class="sxs-lookup"><span data-stu-id="bd12e-187">This allows multiple processes on the same physical or virtual machine to host web applications on the same port, disambiguated by either a unique URL path or hostname.</span></span> <span data-ttu-id="bd12e-188">這些功能對於在 Service Fabric 中於相同叢集裝載多個網站很有用。</span><span class="sxs-lookup"><span data-stu-id="bd12e-188">These features are useful in Service Fabric for hosting multiple websites in the same cluster.</span></span>

<span data-ttu-id="bd12e-189">下圖說明 WebListener 如何在 Windows 上使用 http.sys 核心驅動程式進行連接埠共用︰</span><span class="sxs-lookup"><span data-stu-id="bd12e-189">The following diagram illustrates how WebListener uses the *http.sys* kernel driver on Windows for port sharing:</span></span>

![http.sys][3]

### <a name="weblistener-in-a-stateless-service"></a><span data-ttu-id="bd12e-191">無狀態服務中的 WebListener</span><span class="sxs-lookup"><span data-stu-id="bd12e-191">WebListener in a stateless service</span></span>
<span data-ttu-id="bd12e-192">若要在無狀態服務中使用 `WebListener`，請覆寫 `CreateServiceInstanceListeners` 方法並傳回 `WebListenerCommunicationListener` 執行個體︰</span><span class="sxs-lookup"><span data-stu-id="bd12e-192">To use `WebListener` in a stateless service, override the `CreateServiceInstanceListeners` method and return a `WebListenerCommunicationListener` instance:</span></span>

```csharp
protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    return new ServiceInstanceListener[]
    {
        new ServiceInstanceListener(serviceContext =>
            new WebListenerCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) =>
                new WebHostBuilder()
                    .UseWebListener()
                    .ConfigureServices(
                        services => services
                            .AddSingleton<StatelessServiceContext>(serviceContext))
                    .UseContentRoot(Directory.GetCurrentDirectory())
                    .UseServiceFabricIntegration(listener, ServiceFabricIntegrationOptions.None)
                    .UseStartup<Startup>()
                    .UseUrls(url)
                    .Build()))
    };
}
```

### <a name="weblistener-in-a-stateful-service"></a><span data-ttu-id="bd12e-193">具狀態服務中的 WebListener</span><span class="sxs-lookup"><span data-stu-id="bd12e-193">WebListener in a stateful service</span></span>

<span data-ttu-id="bd12e-194">由於基礎 http.sys 連接埠共用功能很複雜，`WebListenerCommunicationListener` 目前不是設計用於具狀態服務。</span><span class="sxs-lookup"><span data-stu-id="bd12e-194">`WebListenerCommunicationListener` is currently not designed for use in stateful services due to complications with the underlying *http.sys* port sharing feature.</span></span> <span data-ttu-id="bd12e-195">如需詳細資訊，請參閱下一節的使用 WebListener 動態連接埠配置。</span><span class="sxs-lookup"><span data-stu-id="bd12e-195">For more information, see the following section on dynamic port allocation with WebListener.</span></span> <span data-ttu-id="bd12e-196">針對具狀態服務，Kestrel 是建議的 web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="bd12e-196">For stateful services, Kestrel is the recommended web server.</span></span>

### <a name="endpoint-configuration"></a><span data-ttu-id="bd12e-197">端點組態</span><span class="sxs-lookup"><span data-stu-id="bd12e-197">Endpoint configuration</span></span>

<span data-ttu-id="bd12e-198">使用 Windows HTTP Server API，包括 WebListener 的 web 伺服器需要 `Endpoint` 組態。</span><span class="sxs-lookup"><span data-stu-id="bd12e-198">An `Endpoint` configuration is required for web servers that use the Windows HTTP Server API, including WebListener.</span></span> <span data-ttu-id="bd12e-199">使用 Windows HTTP 伺服器 API 的 web 伺服器都必須先保留其 URL 與http.sys (這通常使用 [netsh](https://msdn.microsoft.com/library/windows/desktop/cc307236(v=vs.85).aspx) 工具來完成)。</span><span class="sxs-lookup"><span data-stu-id="bd12e-199">Web servers that use the Windows HTTP Server API must first reserve their URL with *http.sys* (this is normally accomplished with the [netsh](https://msdn.microsoft.com/library/windows/desktop/cc307236(v=vs.85).aspx) tool).</span></span> <span data-ttu-id="bd12e-200">這個動作需要您服務預設未具有的提高權限。</span><span class="sxs-lookup"><span data-stu-id="bd12e-200">This action requires elevated privileges that your services by default do not have.</span></span> <span data-ttu-id="bd12e-201">*ServiceManifest.xml* 中的 `Endpoint` 設定之 `Protocol` 屬性的 "Http" 或 "https" 選項會特別用來指示 Service Fabric 執行階段，以使用[強式萬用字元](https://msdn.microsoft.com/library/windows/desktop/aa364698(v=vs.85).aspx) URL 前置詞代表您註冊 URL 與 http.sys。</span><span class="sxs-lookup"><span data-stu-id="bd12e-201">The "http" or "https" options for the `Protocol` property of the `Endpoint` configuration in *ServiceManifest.xml* are used specifically to instruct the Service Fabric runtime to register a URL with *http.sys* on your behalf using the [*strong wildcard*](https://msdn.microsoft.com/library/windows/desktop/aa364698(v=vs.85).aspx) URL prefix.</span></span>

<span data-ttu-id="bd12e-202">例如，若要保留服務的 `http://+:80`，應該在 ServiceManifest.xml 中使用下列組態︰</span><span class="sxs-lookup"><span data-stu-id="bd12e-202">For example, to reserve `http://+:80` for a service, the following configuration should be used in ServiceManifest.xml:</span></span>

```xml
<ServiceManifest ... >
    ...
    <Resources>
        <Endpoints>
            <Endpoint Name="ServiceEndpoint" Protocol="http" Port="80" />
        </Endpoints>
    </Resources>

</ServiceManifest>
```

<span data-ttu-id="bd12e-203">端點名稱必須傳遞給 `WebListenerCommunicationListener` 建構函式︰</span><span class="sxs-lookup"><span data-stu-id="bd12e-203">And the endpoint name must be passed to the `WebListenerCommunicationListener` constructor:</span></span>

```csharp
 new WebListenerCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) =>
 {
     return new WebHostBuilder()
         .UseWebListener()
         .UseServiceFabricIntegration(listener, ServiceFabricIntegrationOptions.None)
         .UseUrls(url)
         .Build();
 })
```

#### <a name="use-weblistener-with-a-static-port"></a><span data-ttu-id="bd12e-204">搭配使用 WebListener 與靜態連接埠</span><span class="sxs-lookup"><span data-stu-id="bd12e-204">Use WebListener with a static port</span></span>
<span data-ttu-id="bd12e-205">搭配使用靜態連接埠與 WebListener，在 `Endpoint` 組態中提供通訊埠編號︰</span><span class="sxs-lookup"><span data-stu-id="bd12e-205">To use a static port with WebListener, provide the port number in the `Endpoint` configuration:</span></span>

```xml
  <Resources>
    <Endpoints>
      <Endpoint Protocol="http" Name="ServiceEndpoint" Port="80" />
    </Endpoints>
  </Resources>
```

#### <a name="use-weblistener-with-a-dynamic-port"></a><span data-ttu-id="bd12e-206">搭配使用 WebListener 與動態連接埠</span><span class="sxs-lookup"><span data-stu-id="bd12e-206">Use WebListener with a dynamic port</span></span>
<span data-ttu-id="bd12e-207">若要使用動態指派的連接埠與 WebListener，省略 `Endpoint` 組態中的 `Port` 屬性︰</span><span class="sxs-lookup"><span data-stu-id="bd12e-207">To use a dynamically assigned port with WebListener, omit the `Port` property in the `Endpoint` configuration:</span></span>

```xml
  <Resources>
    <Endpoints>
      <Endpoint Protocol="http" Name="ServiceEndpoint" />
    </Endpoints>
  </Resources>
```

<span data-ttu-id="bd12e-208">請注意，依 `Endpoint` 組態配置的動態連接埠只提供每個主機處理序一個連接埠。</span><span class="sxs-lookup"><span data-stu-id="bd12e-208">Note that a dynamic port allocated by an `Endpoint` configuration only provides one port *per host process*.</span></span> <span data-ttu-id="bd12e-209">目前的 Service Fabric 裝載模型可讓多個服務執行個體及/或複本裝載在相同的程序中，這表示當透過 `Endpoint` 組態配置時，每個都會共用相同的連接埠。</span><span class="sxs-lookup"><span data-stu-id="bd12e-209">The current Service Fabric hosting model allows multiple service instances and/or replicas to be hosted in the same process, meaning that each one will share the same port when allocated through the `Endpoint` configuration.</span></span> <span data-ttu-id="bd12e-210">多個 WebListener 執行個體可以使用基礎 http.sys 連接埠共用功能共用連接埠，但由於其為用戶端要求所帶來的複雜性，`WebListenerCommunicationListener` 並不支援。</span><span class="sxs-lookup"><span data-stu-id="bd12e-210">Multiple WebListener instances can share a port using the underlying *http.sys* port sharing feature, but that is not supported by `WebListenerCommunicationListener` due to the complications it introduces for client requests.</span></span> <span data-ttu-id="bd12e-211">針對動態連接埠使用量，Kestrel 是建議的 web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="bd12e-211">For dynamic port usage, Kestrel is the recommended web server.</span></span>

## <a name="kestrel-in-reliable-services"></a><span data-ttu-id="bd12e-212">Reliable Services 中的 Kestrel</span><span class="sxs-lookup"><span data-stu-id="bd12e-212">Kestrel in Reliable Services</span></span>
<span data-ttu-id="bd12e-213">Kestrel 可在 Reliable Service 中使用，方法為匯入 **Microsoft.ServiceFabric.AspNetCore.Kestrel** NuGet 封裝。</span><span class="sxs-lookup"><span data-stu-id="bd12e-213">Kestrel can be used in a Reliable Service by importing the **Microsoft.ServiceFabric.AspNetCore.Kestrel** NuGet package.</span></span> <span data-ttu-id="bd12e-214">此套件包含 `KestrelCommunicationListener`，實作`ICommunicationListener`，可讓您使用 Kestrel 做為 web 伺服器，在 Reliable Service 內部建立 ASP.NET Core WebHost。</span><span class="sxs-lookup"><span data-stu-id="bd12e-214">This package contains `KestrelCommunicationListener`, an implementation of `ICommunicationListener`, that allows you to create an ASP.NET Core WebHost inside a Reliable Service using Kestrel as the web server.</span></span>

<span data-ttu-id="bd12e-215">Kestrel 根據 libuv 是 ASP.NET Core 的跨平台 web 伺服器，為跨平台非同步 I/O 程式庫。</span><span class="sxs-lookup"><span data-stu-id="bd12e-215">Kestrel is a cross-platform web server for ASP.NET Core based on libuv, a cross-platform asynchronous I/O library.</span></span> <span data-ttu-id="bd12e-216">不同於 WebListener，Kestrel 不會使用集中式端點管理員，例如 http.sys。</span><span class="sxs-lookup"><span data-stu-id="bd12e-216">Unlike WebListener, Kestrel does not use a centralized endpoint manager such as *http.sys*.</span></span> <span data-ttu-id="bd12e-217">且不同於 WebListener，Kestrel 不支援多個處理序之間的連接埠共用。</span><span class="sxs-lookup"><span data-stu-id="bd12e-217">And unlike WebListener, Kestrel does not support port sharing between multiple processes.</span></span> <span data-ttu-id="bd12e-218">Kestrel 的每個執行個體必須使用唯一的連接埠。</span><span class="sxs-lookup"><span data-stu-id="bd12e-218">Each instance of Kestrel must use a unique port.</span></span>

![kestrel][4]

### <a name="kestrel-in-a-stateless-service"></a><span data-ttu-id="bd12e-220">無狀態服務中的 Kestrel</span><span class="sxs-lookup"><span data-stu-id="bd12e-220">Kestrel in a stateless service</span></span>
<span data-ttu-id="bd12e-221">若要在無狀態服務中使用 `Kestrel`，請覆寫 `CreateServiceInstanceListeners` 方法並傳回 `KestrelCommunicationListener` 執行個體︰</span><span class="sxs-lookup"><span data-stu-id="bd12e-221">To use `Kestrel` in a stateless service, override the `CreateServiceInstanceListeners` method and return a `KestrelCommunicationListener` instance:</span></span>

```csharp
protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    return new ServiceInstanceListener[]
    {
        new ServiceInstanceListener(serviceContext =>
            new KestrelCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) =>
                new WebHostBuilder()
                    .UseKestrel()
                    .ConfigureServices(
                        services => services
                            .AddSingleton<StatelessServiceContext>(serviceContext))
                    .UseContentRoot(Directory.GetCurrentDirectory())
                    .UseServiceFabricIntegration(listener, ServiceFabricIntegrationOptions.UseUniqueServiceUrl)
                    .UseStartup<Startup>()
                    .UseUrls(url)
                    .Build();
            ))
    };
}
```

### <a name="kestrel-in-a-stateful-service"></a><span data-ttu-id="bd12e-222">具狀態服務中的 Kestrel</span><span class="sxs-lookup"><span data-stu-id="bd12e-222">Kestrel in a stateful service</span></span>
<span data-ttu-id="bd12e-223">若要在具狀態服務中使用 `Kestrel`，請覆寫 `CreateServiceReplicaListeners` 方法並傳回 `KestrelCommunicationListener` 執行個體︰</span><span class="sxs-lookup"><span data-stu-id="bd12e-223">To use `Kestrel` in a stateful service, override the `CreateServiceReplicaListeners` method and return a `KestrelCommunicationListener` instance:</span></span>

```csharp
protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
{
    return new ServiceReplicaListener[]
    {
        new ServiceReplicaListener(serviceContext =>
            new KestrelCommunicationListener(serviceContext, (url, listener) =>
                new WebHostBuilder()
                    .UseKestrel()
                    .ConfigureServices(
                         services => services
                             .AddSingleton<StatefulServiceContext>(serviceContext)
                             .AddSingleton<IReliableStateManager>(this.StateManager))
                    .UseContentRoot(Directory.GetCurrentDirectory())
                    .UseServiceFabricIntegration(listener, ServiceFabricIntegrationOptions.UseUniqueServiceUrl)
                    .UseStartup<Startup>()
                    .UseUrls(url)
                    .Build();
            ))
    };
}
```

<span data-ttu-id="bd12e-224">在此範例中，`IReliableStateManager` 的單一執行個體會提供給 WebHost 相依性插入容器。</span><span class="sxs-lookup"><span data-stu-id="bd12e-224">In this example, a singleton instance of `IReliableStateManager` is provided to the WebHost dependency injection container.</span></span> <span data-ttu-id="bd12e-225">這並非絕對必要，但它可讓您在 MVC 控制器動作方法中使用 `IReliableStateManager` 和可靠的集合。</span><span class="sxs-lookup"><span data-stu-id="bd12e-225">This is not strictly necessary, but it allows you to use `IReliableStateManager` and Reliable Collections in your MVC controller action methods.</span></span>

<span data-ttu-id="bd12e-226">請注意，`Endpoint` 組態名稱**不**提供給具狀態服務中的 `KestrelCommunicationListener`。</span><span class="sxs-lookup"><span data-stu-id="bd12e-226">Note that an `Endpoint` configuration name is **not** provided to `KestrelCommunicationListener` in a stateful service.</span></span> <span data-ttu-id="bd12e-227">我們會在下列各節中詳細說明這個部分。</span><span class="sxs-lookup"><span data-stu-id="bd12e-227">This is explained in more detail in the following section.</span></span>

### <a name="endpoint-configuration"></a><span data-ttu-id="bd12e-228">端點組態</span><span class="sxs-lookup"><span data-stu-id="bd12e-228">Endpoint configuration</span></span>
<span data-ttu-id="bd12e-229">`Endpoint` 組態不需要使用 Kestrel。</span><span class="sxs-lookup"><span data-stu-id="bd12e-229">An `Endpoint` configuration is not required to use Kestrel.</span></span> 

<span data-ttu-id="bd12e-230">Kestrel 是簡單的獨立 web 伺服器；不同於 WebListener (或 HttpListener)，它不需要 *ServiceManifest.xml* 中的 `Endpoint` 組態，因為它不需要在啟動之前註冊 URL。</span><span class="sxs-lookup"><span data-stu-id="bd12e-230">Kestrel is a simple stand-alone web server; unlike WebListener (or HttpListener), it does not need an `Endpoint` configuration in *ServiceManifest.xml* because it does not require URL registration prior to starting.</span></span> 

#### <a name="use-kestrel-with-a-static-port"></a><span data-ttu-id="bd12e-231">搭配使用 Kestrel 與靜態連接埠</span><span class="sxs-lookup"><span data-stu-id="bd12e-231">Use Kestrel with a static port</span></span>
<span data-ttu-id="bd12e-232">靜態連接埠可以在 ServiceManifest.xml 的 `Endpoint` 組態中設定以供與 Kestrel 搭配使用。</span><span class="sxs-lookup"><span data-stu-id="bd12e-232">A static port can be configured in the `Endpoint` configuration of ServiceManifest.xml for use with Kestrel.</span></span> <span data-ttu-id="bd12e-233">雖然這並非絕對必要，它會提供兩個潛在的好處︰</span><span class="sxs-lookup"><span data-stu-id="bd12e-233">Although this is not strictly necessary, it provides two potential benefits:</span></span>
 1. <span data-ttu-id="bd12e-234">如果連接埠不在應用程式連接埠範圍中，它會由 Service Fabric 透過 OS 防火牆開啟。</span><span class="sxs-lookup"><span data-stu-id="bd12e-234">If the port does not fall in the application port range, it is opened through the OS firewall by Service Fabric.</span></span>
 2. <span data-ttu-id="bd12e-235">透過 `KestrelCommunicationListener` 提供給您的 URL 會使用此連接埠。</span><span class="sxs-lookup"><span data-stu-id="bd12e-235">The URL provided to you through `KestrelCommunicationListener` will use this port.</span></span>

```xml
  <Resources>
    <Endpoints>
      <Endpoint Protocol="http" Name="ServiceEndpoint" Port="80" />
    </Endpoints>
  </Resources>
```

<span data-ttu-id="bd12e-236">如果設定了 `Endpoint`，其名稱必須傳遞至 `KestrelCommunicationListener` 建構函式︰</span><span class="sxs-lookup"><span data-stu-id="bd12e-236">If an `Endpoint` is configured, its name must be passed into the `KestrelCommunicationListener` constructor:</span></span> 

```csharp
new KestrelCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) => ...
```

<span data-ttu-id="bd12e-237">如果未使用 `Endpoint` 組態，請省略 `KestrelCommunicationListener` 建構函式中的名稱。</span><span class="sxs-lookup"><span data-stu-id="bd12e-237">If an `Endpoint` configuration is not used, omit the name in the `KestrelCommunicationListener` constructor.</span></span> <span data-ttu-id="bd12e-238">在此情況下，會使用動態連接埠。</span><span class="sxs-lookup"><span data-stu-id="bd12e-238">In this case, a dynamic port will be used.</span></span> <span data-ttu-id="bd12e-239">如需詳細資訊，請參閱下一節。</span><span class="sxs-lookup"><span data-stu-id="bd12e-239">See the next section for more information.</span></span>

#### <a name="use-kestrel-with-a-dynamic-port"></a><span data-ttu-id="bd12e-240">搭配使用 Kestrel 與動態連接埠</span><span class="sxs-lookup"><span data-stu-id="bd12e-240">Use Kestrel with a dynamic port</span></span>
<span data-ttu-id="bd12e-241">Kestrel 無法在 ServiceManifest.xml 中從 `Endpoint` 組態使用自動連接埠指派，因為來自 `Endpoint` 組態的自動連接埠指派會針對每個主機處理序指派唯一的連接埠，且單一主機處理序可以包含多個 Kestrel 執行個體。</span><span class="sxs-lookup"><span data-stu-id="bd12e-241">Kestrel cannot use the automatic port assignment from the `Endpoint` configuration in ServiceManifest.xml, because automatic port assignment from an `Endpoint` configuration assigns a unique port per *host process*, and a single host process can contain multiple Kestrel instances.</span></span> <span data-ttu-id="bd12e-242">因為 Kestrel 不支援連接埠共用，這並不會如每個 Kestrel 執行個體必須在唯一連接埠上開啟一般運作。</span><span class="sxs-lookup"><span data-stu-id="bd12e-242">Since Kestrel does not support port sharing, this does not work as each Kestrel instance must be opened on a unique port.</span></span>

<span data-ttu-id="bd12e-243">若要使用動態通訊埠指派與 Kestrel，只要完全省略 ServiceManifest.xml 中的 `Endpoint` 組態，且不要將端點名稱傳遞至 `KestrelCommunicationListener` 建構函式︰</span><span class="sxs-lookup"><span data-stu-id="bd12e-243">To use dynamic port assignment with Kestrel, simply omit the `Endpoint` configuration in ServiceManifest.xml entirely, and do not pass an endpoint name to the `KestrelCommunicationListener` constructor:</span></span>

```csharp
new KestrelCommunicationListener(serviceContext, (url, listener) => ...
```

<span data-ttu-id="bd12e-244">在此組態中，`KestrelCommunicationListener` 會自動從應用程式連接埠範圍選取未使用的連接埠。</span><span class="sxs-lookup"><span data-stu-id="bd12e-244">In this configuration, `KestrelCommunicationListener` will automatically select an unused port from the application port range.</span></span>

## <a name="scenarios-and-configurations"></a><span data-ttu-id="bd12e-245">案例和組態</span><span class="sxs-lookup"><span data-stu-id="bd12e-245">Scenarios and configurations</span></span>
<span data-ttu-id="bd12e-246">本章節描述下列案例，並提供建議的 web 伺服器、通訊埠組態、Service Fabric 整合選項，以及其他設定的組合，來達成正常運作的服務︰</span><span class="sxs-lookup"><span data-stu-id="bd12e-246">This section describes the following scenarios and provides the recommended combination of web server, port configuration, Service Fabric integration options, and miscellaneous settings to achieve a properly functioning service:</span></span>
 - <span data-ttu-id="bd12e-247">外部公開 ASP.NET Core 無狀態服務</span><span class="sxs-lookup"><span data-stu-id="bd12e-247">Externally exposed ASP.NET Core stateless service</span></span>
 - <span data-ttu-id="bd12e-248">內部公開 ASP.NET Core 無狀態服務</span><span class="sxs-lookup"><span data-stu-id="bd12e-248">Internal-only ASP.NET Core stateless service</span></span>
 - <span data-ttu-id="bd12e-249">內部公開 ASP.NET Core 具狀態服務</span><span class="sxs-lookup"><span data-stu-id="bd12e-249">Internal-only ASP.NET Core stateful service</span></span>

<span data-ttu-id="bd12e-250">**外部公開**的服務是公開可以從叢集外部連線的端點，通常是透過負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="bd12e-250">An **externally exposed** service is one that exposes an endpoint reachable from outside the cluster, usually through a load balancer.</span></span>

<span data-ttu-id="bd12e-251">**僅供內部使用**的服務是其端點僅可從叢集內連線。</span><span class="sxs-lookup"><span data-stu-id="bd12e-251">An **internal-only** service is one whose endpoint is only reachable from within the cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="bd12e-252">具狀態服務端點通常應該不會公開至網際網路。</span><span class="sxs-lookup"><span data-stu-id="bd12e-252">Stateful service endpoints generally should not be exposed to the Internet.</span></span> <span data-ttu-id="bd12e-253">位於察覺不到 Service Fabric 服務解析度之負載平衡器後的叢集 (例如 Azure Load Balancer)，將無法公開具狀態服務，因為負載平衡器將無法找出並將流量路由到適當的具狀態服務複本。</span><span class="sxs-lookup"><span data-stu-id="bd12e-253">Clusters that are behind load balancers that are unaware of Service Fabric service resolution, such as the Azure Load Balancer, will be unable to expose stateful services because the load balancer will not be able to locate and route traffic to the appropriate stateful service replica.</span></span> 

### <a name="externally-exposed-aspnet-core-stateless-services"></a><span data-ttu-id="bd12e-254">外部公開 ASP.NET Core 無狀態服務</span><span class="sxs-lookup"><span data-stu-id="bd12e-254">Externally exposed ASP.NET Core stateless services</span></span>
<span data-ttu-id="bd12e-255">WebListener 建議用於前端服務的 web 伺服器，這些服務會在 Windows 上公開於外部、網際網路 HTTP 端點。</span><span class="sxs-lookup"><span data-stu-id="bd12e-255">WebListener is the recommended web server for front-end services that expose external, Internet-facing HTTP endpoints on Windows.</span></span> <span data-ttu-id="bd12e-256">它提供更好的保護以免於攻擊，並支援 Kestrel 所沒有的功能，例如 Windows 驗證和連接埠共用。</span><span class="sxs-lookup"><span data-stu-id="bd12e-256">It provides better protection against attacks and supports features that Kestrel does not, such as Windows Authentication and port sharing.</span></span> 

<span data-ttu-id="bd12e-257">Kestrel 這一次不支援作為邊緣 (網際網路) 伺服器。</span><span class="sxs-lookup"><span data-stu-id="bd12e-257">Kestrel is not supported as an edge (Internet-facing) server at this time.</span></span> <span data-ttu-id="bd12e-258">IIS 或 Nginx 之類的反向 Proxy 伺服器必須用來處理來自公用網際網路的流量。</span><span class="sxs-lookup"><span data-stu-id="bd12e-258">A reverse proxy server such as IIS or Nginx must be used to handle traffic from the public Internet.</span></span>
 
<span data-ttu-id="bd12e-259">當公開至網際網路時，無狀態服務應使用可透過負載平衡器連線的已知且穩定端點。</span><span class="sxs-lookup"><span data-stu-id="bd12e-259">When exposed to the Internet, a stateless service should use a well-known and stable endpoint that is reachable through a load balancer.</span></span> <span data-ttu-id="bd12e-260">這是您提供給使用者的應用程式 URL。</span><span class="sxs-lookup"><span data-stu-id="bd12e-260">This is the URL you will provide to users of your application.</span></span> <span data-ttu-id="bd12e-261">建議使用下列組態：</span><span class="sxs-lookup"><span data-stu-id="bd12e-261">The following configuration is recommended:</span></span>

|  |  | <span data-ttu-id="bd12e-262">**注意事項**</span><span class="sxs-lookup"><span data-stu-id="bd12e-262">**Notes**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bd12e-263">Web 伺服器</span><span class="sxs-lookup"><span data-stu-id="bd12e-263">Web server</span></span> | <span data-ttu-id="bd12e-264">WebListener</span><span class="sxs-lookup"><span data-stu-id="bd12e-264">WebListener</span></span> | <span data-ttu-id="bd12e-265">如果服務只公開給信任的網路，例如內部網路，則可能會使用 Kestrel。</span><span class="sxs-lookup"><span data-stu-id="bd12e-265">If the service is only exposed to a trusted network, such an intranet, Kestrel may be used.</span></span> <span data-ttu-id="bd12e-266">否則，WebListener 是慣用的選項。</span><span class="sxs-lookup"><span data-stu-id="bd12e-266">Otherwise, WebListener is the preferred option.</span></span> |
| <span data-ttu-id="bd12e-267">連接埠組態</span><span class="sxs-lookup"><span data-stu-id="bd12e-267">Port configuration</span></span> | <span data-ttu-id="bd12e-268">靜態</span><span class="sxs-lookup"><span data-stu-id="bd12e-268">static</span></span> | <span data-ttu-id="bd12e-269">已知的靜態連接埠應在 ServiceManifest.xml 的 `Endpoints` 組態中設定，例如 HTTP 為 80 或 443 為 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="bd12e-269">A well-known static port should be configured in the `Endpoints` configuration of ServiceManifest.xml, such as 80 for HTTP or 443 for HTTPS.</span></span> |
| <span data-ttu-id="bd12e-270">ServiceFabricIntegrationOptions</span><span class="sxs-lookup"><span data-stu-id="bd12e-270">ServiceFabricIntegrationOptions</span></span> | <span data-ttu-id="bd12e-271">None</span><span class="sxs-lookup"><span data-stu-id="bd12e-271">None</span></span> | <span data-ttu-id="bd12e-272">設定 Service Fabric 整合中介軟體時，應使用 `ServiceFabricIntegrationOptions.None` 選項，以便服務不會嘗試驗證唯一識別項的傳入要求。</span><span class="sxs-lookup"><span data-stu-id="bd12e-272">The `ServiceFabricIntegrationOptions.None` option should be used when configuring Service Fabric integration middleware so that the service does not attempt to validate incoming requests for a unique identifier.</span></span> <span data-ttu-id="bd12e-273">應用程式的外部使用者不會知道中介軟體所使用的唯一識別資訊。</span><span class="sxs-lookup"><span data-stu-id="bd12e-273">External users of your application will not know the unique identifying information used by the middleware.</span></span> |
| <span data-ttu-id="bd12e-274">執行個體計數</span><span class="sxs-lookup"><span data-stu-id="bd12e-274">Instance Count</span></span> | <span data-ttu-id="bd12e-275">-1</span><span class="sxs-lookup"><span data-stu-id="bd12e-275">-1</span></span> | <span data-ttu-id="bd12e-276">在典型的使用案例中，執行個體計數設定應該設為 "-1"，以便在接收來自負載平衡器之流量的所有節點上可以使用執行個體。</span><span class="sxs-lookup"><span data-stu-id="bd12e-276">In typical use cases, the instance count setting should be set to "-1" so that an instance is available on all nodes that receive traffic from a load balancer.</span></span> |

<span data-ttu-id="bd12e-277">如果多個外部公開的服務共用相同的節點集，則應該使用唯一但穩定的 URL 路徑。</span><span class="sxs-lookup"><span data-stu-id="bd12e-277">If multiple externally exposed services share the same set of nodes, a unique but stable URL path should be used.</span></span> <span data-ttu-id="bd12e-278">這可以透過修改設定 IWebHost 時提供的 URL 來完成。</span><span class="sxs-lookup"><span data-stu-id="bd12e-278">This can be accomplished by modifying the URL provided when configuring IWebHost.</span></span> <span data-ttu-id="bd12e-279">請注意，這只適用於 WebListener。</span><span class="sxs-lookup"><span data-stu-id="bd12e-279">Note this applies to WebListener only.</span></span>

 ```csharp
 new WebListenerCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) =>
 {
     url += "/MyUniqueServicePath";
 
     return new WebHostBuilder()
         .UseWebListener()
         ...
         .UseUrls(url)
         .Build();
 })
 ```

### <a name="internal-only-stateless-aspnet-core-service"></a><span data-ttu-id="bd12e-280">僅供內部使用的無狀態 ASP.NET Core 服務</span><span class="sxs-lookup"><span data-stu-id="bd12e-280">Internal-only stateless ASP.NET Core service</span></span>
<span data-ttu-id="bd12e-281">只會從叢集內呼叫的無狀態服務應該使用唯一的 URL 並動態指派連接埠，以確保多個服務之間的合作。</span><span class="sxs-lookup"><span data-stu-id="bd12e-281">Stateless services that are only called from within the cluster should use unique URLs and dynamically assigned ports to ensure cooperation between multiple services.</span></span> <span data-ttu-id="bd12e-282">建議使用下列組態：</span><span class="sxs-lookup"><span data-stu-id="bd12e-282">The following configuration is recommended:</span></span>

|  |  | <span data-ttu-id="bd12e-283">**注意事項**</span><span class="sxs-lookup"><span data-stu-id="bd12e-283">**Notes**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bd12e-284">Web 伺服器</span><span class="sxs-lookup"><span data-stu-id="bd12e-284">Web server</span></span> | <span data-ttu-id="bd12e-285">Kestrel</span><span class="sxs-lookup"><span data-stu-id="bd12e-285">Kestrel</span></span> | <span data-ttu-id="bd12e-286">雖然可能會針對內部的無狀態服務使用 WebListener，但 Kestrel 是建議的伺服器，可允許多個服務執行個體共用主機。</span><span class="sxs-lookup"><span data-stu-id="bd12e-286">Although WebListener may be used for internal stateless services, Kestrel is the recommended server to allow multiple service instances to share a host.</span></span>  |
| <span data-ttu-id="bd12e-287">連接埠組態</span><span class="sxs-lookup"><span data-stu-id="bd12e-287">Port configuration</span></span> | <span data-ttu-id="bd12e-288">動態指派</span><span class="sxs-lookup"><span data-stu-id="bd12e-288">dynamically assigned</span></span> | <span data-ttu-id="bd12e-289">多個具狀態服務的複本可能會共用主機處理序或主機作業系統，因此需要唯一的連接埠。</span><span class="sxs-lookup"><span data-stu-id="bd12e-289">Multiple replicas of a stateful service may share a host process or host operating system and thus will need unique ports.</span></span> |
| <span data-ttu-id="bd12e-290">ServiceFabricIntegrationOptions</span><span class="sxs-lookup"><span data-stu-id="bd12e-290">ServiceFabricIntegrationOptions</span></span> | <span data-ttu-id="bd12e-291">UseUniqueServiceUrl</span><span class="sxs-lookup"><span data-stu-id="bd12e-291">UseUniqueServiceUrl</span></span> | <span data-ttu-id="bd12e-292">使用動態連接埠指派，此設定可防止稍早所述的誤用識別問題。</span><span class="sxs-lookup"><span data-stu-id="bd12e-292">With dynamic port assignment, this setting prevents the mistaken identity issue described earlier.</span></span> |
| <span data-ttu-id="bd12e-293">InstanceCount</span><span class="sxs-lookup"><span data-stu-id="bd12e-293">InstanceCount</span></span> | <span data-ttu-id="bd12e-294">any</span><span class="sxs-lookup"><span data-stu-id="bd12e-294">any</span></span> | <span data-ttu-id="bd12e-295">執行個體計數設定可以設定為操作本服務所需的任何值。</span><span class="sxs-lookup"><span data-stu-id="bd12e-295">The instance count setting can be set to any value necessary to operate the service.</span></span> |

### <a name="internal-only-stateful-aspnet-core-service"></a><span data-ttu-id="bd12e-296">僅供內部使用的具狀態 ASP.NET Core 服務</span><span class="sxs-lookup"><span data-stu-id="bd12e-296">Internal-only stateful ASP.NET Core service</span></span>
<span data-ttu-id="bd12e-297">只會從叢集內呼叫的具狀態服務應該使用動態指派連接埠，以確保多個服務之間的合作。</span><span class="sxs-lookup"><span data-stu-id="bd12e-297">Stateful services that are only called from within the cluster should use dynamically assigned ports to ensure cooperation between multiple services.</span></span> <span data-ttu-id="bd12e-298">建議使用下列組態：</span><span class="sxs-lookup"><span data-stu-id="bd12e-298">The following configuration is recommended:</span></span>

|  |  | <span data-ttu-id="bd12e-299">**注意事項**</span><span class="sxs-lookup"><span data-stu-id="bd12e-299">**Notes**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bd12e-300">Web 伺服器</span><span class="sxs-lookup"><span data-stu-id="bd12e-300">Web server</span></span> | <span data-ttu-id="bd12e-301">Kestrel</span><span class="sxs-lookup"><span data-stu-id="bd12e-301">Kestrel</span></span> | <span data-ttu-id="bd12e-302">`WebListenerCommunicationListener`不是設計由複本共用主機處理序的具狀態服務使用。</span><span class="sxs-lookup"><span data-stu-id="bd12e-302">The `WebListenerCommunicationListener` is not designed for use by stateful services in which replicas share a host process.</span></span> |
| <span data-ttu-id="bd12e-303">連接埠組態</span><span class="sxs-lookup"><span data-stu-id="bd12e-303">Port configuration</span></span> | <span data-ttu-id="bd12e-304">動態指派</span><span class="sxs-lookup"><span data-stu-id="bd12e-304">dynamically assigned</span></span> | <span data-ttu-id="bd12e-305">多個具狀態服務的複本可能會共用主機處理序或主機作業系統，因此需要唯一的連接埠。</span><span class="sxs-lookup"><span data-stu-id="bd12e-305">Multiple replicas of a stateful service may share a host process or host operating system and thus will need unique ports.</span></span> |
| <span data-ttu-id="bd12e-306">ServiceFabricIntegrationOptions</span><span class="sxs-lookup"><span data-stu-id="bd12e-306">ServiceFabricIntegrationOptions</span></span> | <span data-ttu-id="bd12e-307">UseUniqueServiceUrl</span><span class="sxs-lookup"><span data-stu-id="bd12e-307">UseUniqueServiceUrl</span></span> | <span data-ttu-id="bd12e-308">使用動態連接埠指派，此設定可防止稍早所述的誤用識別問題。</span><span class="sxs-lookup"><span data-stu-id="bd12e-308">With dynamic port assignment, this setting prevents the mistaken identity issue described earlier.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="bd12e-309">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bd12e-309">Next steps</span></span>
[<span data-ttu-id="bd12e-310">使用 Visual Studio 偵錯 Service Fabric 應用程式</span><span class="sxs-lookup"><span data-stu-id="bd12e-310">Debug your Service Fabric application by using Visual Studio</span></span>](service-fabric-debugging-your-application.md)

<!--Image references-->
[0]:./media/service-fabric-reliable-services-communication-aspnetcore/webhost-standalone.png
[1]:./media/service-fabric-reliable-services-communication-aspnetcore/webhost-servicefabric.png
[2]:./media/service-fabric-reliable-services-communication-aspnetcore/integration.png
[3]:./media/service-fabric-reliable-services-communication-aspnetcore/httpsys.png
[4]:./media/service-fabric-reliable-services-communication-aspnetcore/kestrel.png
