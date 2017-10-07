---
title: "以 hello ASP.NET Core aaaService 通訊 |Microsoft 文件"
description: "深入了解如何 toouse ASP.NET 核心中無狀態與可設定狀態可靠的服務。"
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
ms.openlocfilehash: 6e6a83ab04390150292f63de5d9b51d290284e50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="aspnet-core-in-service-fabric-reliable-services"></a><span data-ttu-id="ca5f4-103">Service Fabric Reliable Services 中的 ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="ca5f4-103">ASP.NET Core in Service Fabric Reliable Services</span></span>

<span data-ttu-id="ca5f4-104">ASP.NET Core 是新的開放原始碼和跨平台架構，可建置現代化雲端網際網路連線的應用程式，例如 web 應用程式、IoT 應用程式，以及行動後端。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-104">ASP.NET Core is a new open-source and cross-platform framework for building modern cloud-based Internet-connected applications, such as web apps, IoT apps, and mobile backends.</span></span> 

<span data-ttu-id="ca5f4-105">本文是服務網狀架構可靠的服務使用 hello 中服務的 ASP.NET Core 深度指南 toohosting **Microsoft.ServiceFabric.AspNetCore。*** 的 NuGet 套件集。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-105">This article is an in-depth guide toohosting ASP.NET Core services in Service Fabric Reliable Services using hello **Microsoft.ServiceFabric.AspNetCore.*** set of NuGet packages.</span></span>

<span data-ttu-id="ca5f4-106">如需 Service Fabric 中 ASP.NET Core 的簡介教學課程，以及如何安裝開發環境設定的指示，請參閱[使用 ASP.NET Core 為應用程式建置 Web 前端應用程式](service-fabric-add-a-web-frontend.md)。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-106">For an introductory tutorial on ASP.NET Core in Service Fabric and instructions on getting your development environment set up, see [Building a web front-end for your application using ASP.NET Core](service-fabric-add-a-web-frontend.md).</span></span>

<span data-ttu-id="ca5f4-107">hello 本文其餘部分，假設您已熟悉 ASP.NET Core。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-107">hello rest of this article assumes you are already familiar with ASP.NET Core.</span></span> <span data-ttu-id="ca5f4-108">如果不是，我們建議您閱讀 hello [ASP.NET Core 基礎](https://docs.microsoft.com/aspnet/core/fundamentals/index)。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-108">If not, we recommend reading through hello [ASP.NET Core fundamentals](https://docs.microsoft.com/aspnet/core/fundamentals/index).</span></span>

## <a name="aspnet-core-in-hello-service-fabric-environment"></a><span data-ttu-id="ca5f4-109">Hello Service Fabric 環境中的 ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="ca5f4-109">ASP.NET Core in hello Service Fabric environment</span></span>

<span data-ttu-id="ca5f4-110">雖然 ASP.NET Core 應用程式可以執行只能在執行完整的.NET Framework，Service Fabric 服務目前的 hello 或.NET 核心上 hello 完整.NET Framework。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-110">While ASP.NET Core apps can run on .NET Core or on hello full .NET Framework, Service Fabric services currently can only run on hello full .NET Framework.</span></span> <span data-ttu-id="ca5f4-111">這表示當您建置 ASP.NET Core Service Fabric 服務時，您必須仍目標 hello 完整.NET Framework。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-111">This means when you build an ASP.NET  Core Service Fabric service, you must still target hello full .NET Framework.</span></span>

<span data-ttu-id="ca5f4-112">可在 Service Fabric 中以兩種方式使用 ASP.NET Core︰</span><span class="sxs-lookup"><span data-stu-id="ca5f4-112">ASP.NET Core can be used in two different ways in Service Fabric:</span></span>
 - <span data-ttu-id="ca5f4-113">**裝載作為客體可執行檔**。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-113">**Hosted as a guest executable**.</span></span> <span data-ttu-id="ca5f4-114">這是主要使用的 toorun 現有 ASP.NET Core 應用程式服務的網狀架構上沒有變更程式碼。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-114">This is primarily used toorun existing ASP.NET Core applications on Service Fabric with no code changes.</span></span>
 - <span data-ttu-id="ca5f4-115">**在 Reliable Service 內部執行**.</span><span class="sxs-lookup"><span data-stu-id="ca5f4-115">**Run inside a Reliable Service**.</span></span> <span data-ttu-id="ca5f4-116">這允許更貼近 hello Service Fabric 執行階段，並允許可設定狀態的 ASP.NET 核心服務。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-116">This allows better integration with hello Service Fabric runtime and allows stateful ASP.NET Core services.</span></span>

<span data-ttu-id="ca5f4-117">hello 這篇文章的其餘部分將說明如何 toouse ASP.NET Core 內可靠的服務使用 hello 以 hello Service Fabric SDK 的出貨的 ASP.NET Core 整合元件。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-117">hello rest of this article explains how toouse ASP.NET Core inside a Reliable Service using hello ASP.NET Core integration components that ship with hello Service Fabric SDK.</span></span> 

## <a name="service-fabric-service-hosting"></a><span data-ttu-id="ca5f4-118">Service Fabric 服務裝載</span><span class="sxs-lookup"><span data-stu-id="ca5f4-118">Service Fabric service hosting</span></span>

<span data-ttu-id="ca5f4-119">在 Service Fabric 中，您服務的一或多個執行個體及/或複本會在服務主機處理序中執行，這是執行您的服務程式碼的可執行檔。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-119">In Service Fabric, one or more instances and/or replicas of your service run in a *service host process*, an executable file that runs your service code.</span></span> <span data-ttu-id="ca5f4-120">您身為服務作者，擁有 hello 服務主機處理序，Service Fabric 會啟用，並監視您。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-120">You, as a service author, own hello service host process and Service Fabric activates and monitors it for you.</span></span>

<span data-ttu-id="ca5f4-121">（向上 tooMVC 5) 的傳統 ASP.NET 是透過 System.Web.dll 緊密結合的 tooIIS。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-121">Traditional ASP.NET (up tooMVC 5) is tightly coupled tooIIS through System.Web.dll.</span></span> <span data-ttu-id="ca5f4-122">ASP.NET Core 提供 hello web 伺服器和 web 應用程式之間的分隔。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-122">ASP.NET Core provides a separation between hello web server and your web application.</span></span> <span data-ttu-id="ca5f4-123">這可讓 web 應用程式 toobe 可攜式不同的網頁伺服器之間，也可讓 web 伺服器 toobe*自我裝載*，這表示您可以啟動 web 伺服器在自己的程序，但不要的 tooa 程序擁有的專用 web例如，IIS 伺服器軟體。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-123">This allows web applications toobe portable between different web servers and also allows web servers toobe *self-hosted*, which means you can start a web server in your own process, as opposed tooa process that is owned by dedicated web server software such as IIS.</span></span> 

<span data-ttu-id="ca5f4-124">在順序 toocombine Service Fabric 服務和 ASP.NET，為客體可執行檔，或者在可靠的服務中，您必須能夠 toostart ASP.NET 服務的主機處理序內。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-124">In order toocombine a Service Fabric service and ASP.NET, either as a guest executable or in a Reliable Service, you must be able toostart ASP.NET inside your service host process.</span></span> <span data-ttu-id="ca5f4-125">自我裝載的 ASP.NET Core 可讓您 toodo 這。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-125">ASP.NET Core self-hosting allows you toodo this.</span></span>

## <a name="hosting-aspnet-core-in-a-reliable-service"></a><span data-ttu-id="ca5f4-126">在 Reliable Service 中裝載 ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="ca5f4-126">Hosting ASP.NET Core in a Reliable Service</span></span>
<span data-ttu-id="ca5f4-127">自我裝載的 ASP.NET 核心應用程式通常會在應用程式的進入點，例如 hello 建立 WebHost`static void Main()`方法中的`Program.cs`。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-127">Typically, self-hosted ASP.NET Core applications create a WebHost in an application's entry point, such as hello `static void Main()` method in `Program.cs`.</span></span> <span data-ttu-id="ca5f4-128">在此案例中 WebHost 的 hello 生命週期是 hello 的 hello 程序的繫結的 toohello 生命週期。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-128">In this case, hello lifecycle of hello WebHost is bound toohello lifecycle of hello process.</span></span>

![在處理序中裝載 ASP.NET Core][0]

<span data-ttu-id="ca5f4-130">不過，hello 應用程式進入點不是 hello 地方 toocreate WebHost 可靠的服務中，因為只會用 hello 應用程式進入點 tooregister 服務類型，與 hello Service Fabric 執行階段，讓它可能會建立該服務的執行個體型別。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-130">However, hello application entry point is not hello right place toocreate a WebHost in a Reliable Service, because hello application entry point is only used tooregister a service type with hello Service Fabric runtime, so that it may create instances of that service type.</span></span> <span data-ttu-id="ca5f4-131">hello WebHost 中應該建立可靠的服務本身。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-131">hello WebHost should be created in a Reliable Service itself.</span></span> <span data-ttu-id="ca5f4-132">Hello 服務主機處理序內的服務執行個體及/或複本可能經過多個週期。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-132">Within hello service host process, service instances and/or replicas can go through multiple lifecycles.</span></span> 

<span data-ttu-id="ca5f4-133">Reliable Service 執行個體是由您衍生自 `StatelessService` 或 `StatefulService` 的服務類別代表。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-133">A Reliable Service instance is represented by your service class deriving from `StatelessService` or `StatefulService`.</span></span> <span data-ttu-id="ca5f4-134">服務的 hello 通訊堆疊包含在`ICommunicationListener`您的服務類別中實作。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-134">hello communication stack for a service is contained in an `ICommunicationListener` implementation in your service class.</span></span> <span data-ttu-id="ca5f4-135">hello `Microsoft.ServiceFabric.Services.AspNetCore.*` NuGet 封裝包含實作的`ICommunicationListener`，啟動並管理 hello ASP.NET Core WebHost Kestrel 或 WebListener 可靠的服務中。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-135">hello `Microsoft.ServiceFabric.Services.AspNetCore.*` NuGet packages contain implementations of `ICommunicationListener` that start and manage hello ASP.NET Core WebHost for either Kestrel or WebListener in a Reliable Service.</span></span>

![在 Reliable Service 中裝載 ASP.NET Core][1]

## <a name="aspnet-core-icommunicationlisteners"></a><span data-ttu-id="ca5f4-137">ASP.NET Core ICommunicationListeners</span><span class="sxs-lookup"><span data-stu-id="ca5f4-137">ASP.NET Core ICommunicationListeners</span></span>
<span data-ttu-id="ca5f4-138">hello `ICommunicationListener` Kestrel 和實作 WebListener 在 hello `Microsoft.ServiceFabric.Services.AspNetCore.*` NuGet 封裝有相似的使用模式，但執行稍有不同的動作特定 tooeach web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-138">hello `ICommunicationListener` implementations for Kestrel and WebListener in hello  `Microsoft.ServiceFabric.Services.AspNetCore.*` NuGet packages have similar use patterns but perform slightly different actions specific tooeach web server.</span></span> 

<span data-ttu-id="ca5f4-139">這兩個通訊接聽程式提供的建構函式會採用下列引數的 hello:</span><span class="sxs-lookup"><span data-stu-id="ca5f4-139">Both communication listeners provide a constructor that takes hello following arguments:</span></span>
 - <span data-ttu-id="ca5f4-140">**`ServiceContext serviceContext`**: hello`ServiceContext`包含 hello 執行服務的相關資訊的物件。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-140">**`ServiceContext serviceContext`**: hello `ServiceContext` object that contains information about hello running service.</span></span>
 - <span data-ttu-id="ca5f4-141">**`string endpointName`**: hello 名稱`Endpoint`ServiceManifest.xml 中的組態。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-141">**`string endpointName`**: hello name of an `Endpoint` configuration in ServiceManifest.xml.</span></span> <span data-ttu-id="ca5f4-142">這主要是 hello 兩個通訊接聽程式的不同之處： WebListener**需要**`Endpoint`組態，而 Kestrel 沒有。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-142">This is primarily where hello two communication listeners differ: WebListener **requires** an `Endpoint` configuration, while Kestrel does not.</span></span>
 - <span data-ttu-id="ca5f4-143">**`Func<string, AspNetCoreCommunicationListener, IWebHost> build`**：您所實作並在其中建立並傳回 `IWebHost` 的 lambda。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-143">**`Func<string, AspNetCoreCommunicationListener, IWebHost> build`**: a lambda that you implement in which you create and return an `IWebHost`.</span></span> <span data-ttu-id="ca5f4-144">這可讓您 tooconfigure `IWebHost` hello 方式就像平常 ASP.NET Core 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-144">This allows you tooconfigure `IWebHost` hello way you normally would in an ASP.NET Core application.</span></span> <span data-ttu-id="ca5f4-145">hello lambda 提供 URL，這產生的您根據 hello Service Fabric 整合選項您使用和 hello`Endpoint`您提供的組態。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-145">hello lambda provides a URL which is generated for you depending on hello Service Fabric integration options you use and hello `Endpoint` configuration you provide.</span></span> <span data-ttu-id="ca5f4-146">然後可以修改或做為 URL-toostart hello 的網頁伺服器。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-146">That URL can then be modified or used as-is toostart hello web server.</span></span>

## <a name="service-fabric-integration-middleware"></a><span data-ttu-id="ca5f4-147">Service Fabric 整合中介軟體</span><span class="sxs-lookup"><span data-stu-id="ca5f4-147">Service Fabric integration middleware</span></span>
<span data-ttu-id="ca5f4-148">hello `Microsoft.ServiceFabric.Services.AspNetCore` NuGet 套件會包含 hello`UseServiceFabricIntegration`上的擴充方法`IWebHostBuilder`，將服務網狀架構的中介軟體。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-148">hello `Microsoft.ServiceFabric.Services.AspNetCore` NuGet package includes hello `UseServiceFabricIntegration` extension method on `IWebHostBuilder` that adds Service Fabric-aware middleware.</span></span> <span data-ttu-id="ca5f4-149">此中介軟體設定 hello Kestrel 或 WebListener `ICommunicationListener` tooregister 唯一的服務 URL 與 hello Service Fabric 命名服務，然後驗證用戶端要求 tooensure 用戶端連線 toohello 正確的服務。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-149">This middleware configures hello Kestrel or WebListener `ICommunicationListener` tooregister a unique service URL with hello Service Fabric Naming Service and then validates client requests tooensure clients are connecting toohello right service.</span></span> <span data-ttu-id="ca5f4-150">這是必要，在共用主機環境，例如服務網狀架構，其中多個 web 應用程式相同的實體或虛擬機器可以在 hello 中執行，但是不會使用唯一的主機名稱，但是不小心連接 toohello 錯誤的服務 tooprevent 用戶端。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-150">This is necessary in a shared-host environment such as Service Fabric, where multiple web applications can run on hello same physical or virtual machine but do not use unique host names, tooprevent clients from mistakenly connecting toohello wrong service.</span></span> <span data-ttu-id="ca5f4-151">在 hello 下一節中詳細描述此案例。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-151">This scenario is described in more detail in hello next section.</span></span>

### <a name="a-case-of-mistaken-identity"></a><span data-ttu-id="ca5f4-152">誤用身分識別的案例</span><span class="sxs-lookup"><span data-stu-id="ca5f4-152">A case of mistaken identity</span></span>
<span data-ttu-id="ca5f4-153">不論通訊協定，服務複本會接聽唯一 IP:port 組合。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-153">Service replicas, regardless of protocol, listen on a unique IP:port combination.</span></span> <span data-ttu-id="ca5f4-154">服務複本啟動之後 IP:port 端點上接聽，它會報告該端點位址 toohello Service Fabric 命名服務用戶端或其他服務，可以探索到。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-154">Once a service replica has started listening on an IP:port endpoint, it reports that endpoint address toohello Service Fabric Naming Service where it can be discovered by clients or other services.</span></span> <span data-ttu-id="ca5f4-155">如果服務使用，且剛好都可以使用動態指派的應用程式連接埠，服務複本 hello 先前已的另一個服務相同 IP:port 端點 hello 相同的實體或虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-155">If services use dynamically-assigned application ports, a service replica may coincidentally use hello same IP:port endpoint of another service that was previously on hello same physical or virtual machine.</span></span> <span data-ttu-id="ca5f4-156">這可能會造成用戶端 toomistakely 連接 toohello 錯誤的服務。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-156">This can cause a client toomistakely connect toohello wrong service.</span></span> <span data-ttu-id="ca5f4-157">這種情況會發生下列事件順序的 hello:</span><span class="sxs-lookup"><span data-stu-id="ca5f4-157">This can happen if hello following sequence of events occur:</span></span>

 1. <span data-ttu-id="ca5f4-158">服務 A 透過 HTTP 接聽 10.0.0.1:30000。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-158">Service A listens on 10.0.0.1:30000 over HTTP.</span></span> 
 2. <span data-ttu-id="ca5f4-159">用戶端解析服務 A 並取得位址 10.0.0.1:30000</span><span class="sxs-lookup"><span data-stu-id="ca5f4-159">Client resolves Service A and gets address 10.0.0.1:30000</span></span>
 3. <span data-ttu-id="ca5f4-160">服務移 tooa 另一個節點。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-160">Service A moves tooa different node.</span></span>
 4. <span data-ttu-id="ca5f4-161">服務 B 會存放在 10.0.0.1，且剛好都使用 hello 相同的連接埠 30000。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-161">Service B is placed on 10.0.0.1 and coincidentally uses hello same port 30000.</span></span>
 5. <span data-ttu-id="ca5f4-162">用戶端會嘗試使用快取的位址 10.0.0.1:30000 tooconnect tooservice A。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-162">Client attempts tooconnect tooservice A with cached address 10.0.0.1:30000.</span></span>
 6. <span data-ttu-id="ca5f4-163">用戶端是連接已成功連接的 tooservice B 他不知道它現在 toohello 錯誤的服務。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-163">Client is now successfully connected tooservice B not realizing it is connected toohello wrong service.</span></span>

<span data-ttu-id="ca5f4-164">在隨機時間可能是很困難 toodiagnose，這會造成錯誤。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-164">This can cause bugs at random times that can be difficult toodiagnose.</span></span> 

### <a name="using-unique-service-urls"></a><span data-ttu-id="ca5f4-165">使用唯一的服務 URL</span><span class="sxs-lookup"><span data-stu-id="ca5f4-165">Using unique service URLs</span></span>
<span data-ttu-id="ca5f4-166">此服務 tooprevent 張貼端點 toohello 命名服務，且其唯一的識別碼，以及驗證期間用戶端要求的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-166">tooprevent this, services can post an endpoint toohello Naming Service with a unique identifier, and then validate that unique identifier during client requests.</span></span> <span data-ttu-id="ca5f4-167">這在非惡意租用戶受信任環境中的服務之間為合作式動作。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-167">This is a cooperative action between services in a non-hostile-tenant trusted environment.</span></span> <span data-ttu-id="ca5f4-168">這在惡意租用戶環境中不會提供安全服務驗證。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-168">This does not provide secure service authentication in a hostile-tenant environment.</span></span>

<span data-ttu-id="ca5f4-169">在受信任的環境中，hello hello 所加入的中介軟體`UseServiceFabricIntegration`方法會自動將附加的唯一識別碼 toohello 位址張貼 toohello 命名服務及驗證每個要求該識別項。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-169">In a trusted environment, hello middleware that's added by hello `UseServiceFabricIntegration` method automatically appends a unique identifier toohello address that is posted toohello Naming Service and validates that identifier on each request.</span></span> <span data-ttu-id="ca5f4-170">如果 hello 識別碼不符合，hello 中介軟體會立即傳回 HTTP 410 Gone 回應。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-170">If hello identifier does not match, hello middleware immediately returns an HTTP 410 Gone response.</span></span>

<span data-ttu-id="ca5f4-171">使用動態指派連接埠的服務應該要使用此中介軟體。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-171">Services that use a dynamically-assigned port should make use of this middleware.</span></span>

<span data-ttu-id="ca5f4-172">使用固定的唯一連接埠之服務在合作的環境中沒有這個問題。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-172">Services that use a fixed unique port do not have this problem in a cooperative environment.</span></span> <span data-ttu-id="ca5f4-173">固定的唯一通訊埠通常用於外部對向服務至用戶端應用程式 tooconnect 需已知的連接埠。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-173">A fixed unique port is typically used for externally-facing services that need a well-known port for client applications tooconnect to.</span></span> <span data-ttu-id="ca5f4-174">例如，大部分對網際網路開放的 web 應用程式會使用 web 瀏覽器連接的連接埠 80 或 443。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-174">For example, most Internet-facing web applications will use port 80 or 443 for web browser connections.</span></span> <span data-ttu-id="ca5f4-175">在此情況下，不應啟用 hello 唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-175">In this case, hello unique identifier should not be enabled.</span></span>

<span data-ttu-id="ca5f4-176">hello 下圖顯示 hello 要求流程 hello 中介軟體啟用：</span><span class="sxs-lookup"><span data-stu-id="ca5f4-176">hello following diagram shows hello request flow with hello middleware enabled:</span></span>

![Service Fabric ASP.NET Core 整合][2]

<span data-ttu-id="ca5f4-178">Kestrel 和 WebListener`ICommunicationListener`實作會使用這項機制在完全 hello 相同的方式。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-178">Both Kestrel and WebListener `ICommunicationListener` implementations use this mechanism in exactly hello same way.</span></span> <span data-ttu-id="ca5f4-179">雖然 WebListener 就可以在內部區分根據唯一的 URL 路徑使用 hello 基礎要求*http.sys*連接埠共用功能，功能*不*hello WebListener所使用`ICommunicationListener`實作因為會導致在 hello 稍早所述的案例中的 HTTP 503 和 HTTP 404 錯誤狀態碼。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-179">Although WebListener can internally differentiate requests based on unique URL paths using hello underlying *http.sys* port sharing feature, that functionality is *not* used by hello WebListener `ICommunicationListener` implementation because that will result in HTTP 503 and HTTP 404 error status codes in hello scenario described earlier.</span></span> <span data-ttu-id="ca5f4-180">反而能夠讓它很難 hello 錯誤的用戶端 toodetermine hello 意圖以 HTTP 503 HTTP 404 已經常用的 tooindicate 其他錯誤。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-180">That in turn makes it very difficult for clients toodetermine hello intent of hello error, as HTTP 503 and HTTP 404 are already commonly used tooindicate other errors.</span></span> <span data-ttu-id="ca5f4-181">因此，Kestrel 和 WebListener`ICommunicationListener`實作標準化 hello 中介軟體提供的 hello`UseServiceFabricIntegration`擴充方法，讓用戶端只需 tooperform 服務端點重新解決 HTTP 410 回應所引發的動作。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-181">Thus, both Kestrel and WebListener `ICommunicationListener` implementations standardize on hello middleware provided by hello `UseServiceFabricIntegration` extension method so that clients only need tooperform a service endpoint re-resolve action on HTTP 410 responses.</span></span>

## <a name="weblistener-in-reliable-services"></a><span data-ttu-id="ca5f4-182">Reliable Services 中的 WebListener</span><span class="sxs-lookup"><span data-stu-id="ca5f4-182">WebListener in Reliable Services</span></span>
<span data-ttu-id="ca5f4-183">可以藉由匯入 hello 可靠的服務中使用 WebListener **Microsoft.ServiceFabric.AspNetCore.WebListener** NuGet 封裝。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-183">WebListener can be used in a Reliable Service by importing hello **Microsoft.ServiceFabric.AspNetCore.WebListener** NuGet package.</span></span> <span data-ttu-id="ca5f4-184">此套件包含`WebListenerCommunicationListener`，實作`ICommunicationListener`，可讓您 toocreate 可靠的服務內部 ASP.NET Core WebHost WebListener 用作 hello web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-184">This package contains `WebListenerCommunicationListener`, an implementation of `ICommunicationListener`, that allows you toocreate an ASP.NET Core WebHost inside a Reliable Service using WebListener as hello web server.</span></span>

<span data-ttu-id="ca5f4-185">WebListener 建置在 hello [Windows HTTP 伺服器 API](https://msdn.microsoft.com/library/windows/desktop/aa364510(v=vs.85).aspx)。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-185">WebListener is built on hello [Windows HTTP Server API](https://msdn.microsoft.com/library/windows/desktop/aa364510(v=vs.85).aspx).</span></span> <span data-ttu-id="ca5f4-186">這會使用 hello *http.sys*核心驅動程式使用 IIS tooprocess HTTP 要求和傳送它們 tooprocesses 執行 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-186">This uses hello *http.sys* kernel driver used by IIS tooprocess HTTP requests and route them tooprocesses running web applications.</span></span> <span data-ttu-id="ca5f4-187">這可讓多個處理序上 hello 相同實體或虛擬機器 toohost web 應用程式上 hello 明確地區分由唯一的 URL 路徑或主機名稱的相同連接埠。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-187">This allows multiple processes on hello same physical or virtual machine toohost web applications on hello same port, disambiguated by either a unique URL path or hostname.</span></span> <span data-ttu-id="ca5f4-188">這些功能來裝載多個網站中 hello 可用於 Service Fabric 相同叢集中。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-188">These features are useful in Service Fabric for hosting multiple websites in hello same cluster.</span></span>

<span data-ttu-id="ca5f4-189">hello 下列圖表說明了如何 WebListener 使用 hello *http.sys* Windows 上的連接埠共用的核心驅動程式：</span><span class="sxs-lookup"><span data-stu-id="ca5f4-189">hello following diagram illustrates how WebListener uses hello *http.sys* kernel driver on Windows for port sharing:</span></span>

![http.sys][3]

### <a name="weblistener-in-a-stateless-service"></a><span data-ttu-id="ca5f4-191">無狀態服務中的 WebListener</span><span class="sxs-lookup"><span data-stu-id="ca5f4-191">WebListener in a stateless service</span></span>
<span data-ttu-id="ca5f4-192">toouse`WebListener`無狀態服務，在覆寫 hello`CreateServiceInstanceListeners`方法，並傳回`WebListenerCommunicationListener`執行個體：</span><span class="sxs-lookup"><span data-stu-id="ca5f4-192">toouse `WebListener` in a stateless service, override hello `CreateServiceInstanceListeners` method and return a `WebListenerCommunicationListener` instance:</span></span>

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

### <a name="weblistener-in-a-stateful-service"></a><span data-ttu-id="ca5f4-193">具狀態服務中的 WebListener</span><span class="sxs-lookup"><span data-stu-id="ca5f4-193">WebListener in a stateful service</span></span>

<span data-ttu-id="ca5f4-194">`WebListenerCommunicationListener`目前不是以用於可設定狀態服務到期與 hello 基礎 toocomplications *http.sys*連接埠共用功能。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-194">`WebListenerCommunicationListener` is currently not designed for use in stateful services due toocomplications with hello underlying *http.sys* port sharing feature.</span></span> <span data-ttu-id="ca5f4-195">如需詳細資訊，請參閱下列區段上動態連接埠配置以 WebListener hello。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-195">For more information, see hello following section on dynamic port allocation with WebListener.</span></span> <span data-ttu-id="ca5f4-196">對於可設定狀態服務，Kestrel 會是 hello 建議使用 web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-196">For stateful services, Kestrel is hello recommended web server.</span></span>

### <a name="endpoint-configuration"></a><span data-ttu-id="ca5f4-197">端點組態</span><span class="sxs-lookup"><span data-stu-id="ca5f4-197">Endpoint configuration</span></span>

<span data-ttu-id="ca5f4-198">`Endpoint`不需要對使用 hello Windows HTTP 伺服器 API，包括 WebListener 網頁伺服器的組態。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-198">An `Endpoint` configuration is required for web servers that use hello Windows HTTP Server API, including WebListener.</span></span> <span data-ttu-id="ca5f4-199">使用 hello Windows HTTP 伺服器 API 網頁伺服器的第一次必須保留其 URL 與*http.sys* (通常這是以 hello [netsh](https://msdn.microsoft.com/library/windows/desktop/cc307236(v=vs.85).aspx)工具)。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-199">Web servers that use hello Windows HTTP Server API must first reserve their URL with *http.sys* (this is normally accomplished with hello [netsh](https://msdn.microsoft.com/library/windows/desktop/cc307236(v=vs.85).aspx) tool).</span></span> <span data-ttu-id="ca5f4-200">這個動作需要您服務預設未具有的提高權限。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-200">This action requires elevated privileges that your services by default do not have.</span></span> <span data-ttu-id="ca5f4-201">hello"http"或"https"hello 選項`Protocol`hello 屬性`Endpoint`中的組態*ServiceManifest.xml*可用特別 tooinstruct hello Service Fabric 執行階段 tooregister URL*http.sys*代替您使用 hello [*強式萬用字元*](https://msdn.microsoft.com/library/windows/desktop/aa364698(v=vs.85).aspx) URL 前置詞。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-201">hello "http" or "https" options for hello `Protocol` property of hello `Endpoint` configuration in *ServiceManifest.xml* are used specifically tooinstruct hello Service Fabric runtime tooregister a URL with *http.sys* on your behalf using hello [*strong wildcard*](https://msdn.microsoft.com/library/windows/desktop/aa364698(v=vs.85).aspx) URL prefix.</span></span>

<span data-ttu-id="ca5f4-202">例如，tooreserve`http://+:80`服務中，hello 下列組態應該用於 ServiceManifest.xml:</span><span class="sxs-lookup"><span data-stu-id="ca5f4-202">For example, tooreserve `http://+:80` for a service, hello following configuration should be used in ServiceManifest.xml:</span></span>

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

<span data-ttu-id="ca5f4-203">而且必須在 hello 端點名稱傳遞 toohello`WebListenerCommunicationListener`建構函式：</span><span class="sxs-lookup"><span data-stu-id="ca5f4-203">And hello endpoint name must be passed toohello `WebListenerCommunicationListener` constructor:</span></span>

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

#### <a name="use-weblistener-with-a-static-port"></a><span data-ttu-id="ca5f4-204">搭配使用 WebListener 與靜態連接埠</span><span class="sxs-lookup"><span data-stu-id="ca5f4-204">Use WebListener with a static port</span></span>
<span data-ttu-id="ca5f4-205">toouse WebListener，使用靜態連接埠提供 hello hello 連接埠號碼`Endpoint`組態：</span><span class="sxs-lookup"><span data-stu-id="ca5f4-205">toouse a static port with WebListener, provide hello port number in hello `Endpoint` configuration:</span></span>

```xml
  <Resources>
    <Endpoints>
      <Endpoint Protocol="http" Name="ServiceEndpoint" Port="80" />
    </Endpoints>
  </Resources>
```

#### <a name="use-weblistener-with-a-dynamic-port"></a><span data-ttu-id="ca5f4-206">搭配使用 WebListener 與動態連接埠</span><span class="sxs-lookup"><span data-stu-id="ca5f4-206">Use WebListener with a dynamic port</span></span>
<span data-ttu-id="ca5f4-207">toouse WebListener，動態指派連接埠省略 hello`Port`屬性在 hello`Endpoint`組態：</span><span class="sxs-lookup"><span data-stu-id="ca5f4-207">toouse a dynamically assigned port with WebListener, omit hello `Port` property in hello `Endpoint` configuration:</span></span>

```xml
  <Resources>
    <Endpoints>
      <Endpoint Protocol="http" Name="ServiceEndpoint" />
    </Endpoints>
  </Resources>
```

<span data-ttu-id="ca5f4-208">請注意，依 `Endpoint` 組態配置的動態連接埠只提供每個主機處理序一個連接埠。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-208">Note that a dynamic port allocated by an `Endpoint` configuration only provides one port *per host process*.</span></span> <span data-ttu-id="ca5f4-209">hello 目前裝載模型可讓多個服務執行個體及/或複本 toobe hello 中裝載的服務網狀架構相同的處理序，這表示每個會共用相同連接埠時透過 hello 配置的 hello`Endpoint`組態。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-209">hello current Service Fabric hosting model allows multiple service instances and/or replicas toobe hosted in hello same process, meaning that each one will share hello same port when allocated through hello `Endpoint` configuration.</span></span> <span data-ttu-id="ca5f4-210">多個 WebListener 執行個體可以共用連接埠使用 hello 基礎*http.sys*連接埠共用功能，但不是支援`WebListenerCommunicationListener`到期，它會導致用戶端要求 toohello 複雜性。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-210">Multiple WebListener instances can share a port using hello underlying *http.sys* port sharing feature, but that is not supported by `WebListenerCommunicationListener` due toohello complications it introduces for client requests.</span></span> <span data-ttu-id="ca5f4-211">動態連接埠使用量 Kestrel 是 hello 建議使用 web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-211">For dynamic port usage, Kestrel is hello recommended web server.</span></span>

## <a name="kestrel-in-reliable-services"></a><span data-ttu-id="ca5f4-212">Reliable Services 中的 Kestrel</span><span class="sxs-lookup"><span data-stu-id="ca5f4-212">Kestrel in Reliable Services</span></span>
<span data-ttu-id="ca5f4-213">可以藉由匯入 hello 可靠的服務中使用 kestrel **Microsoft.ServiceFabric.AspNetCore.Kestrel** NuGet 封裝。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-213">Kestrel can be used in a Reliable Service by importing hello **Microsoft.ServiceFabric.AspNetCore.Kestrel** NuGet package.</span></span> <span data-ttu-id="ca5f4-214">此套件包含`KestrelCommunicationListener`，實作`ICommunicationListener`，可讓您 toocreate 可靠的服務內部 ASP.NET Core WebHost Kestrel 用作 hello web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-214">This package contains `KestrelCommunicationListener`, an implementation of `ICommunicationListener`, that allows you toocreate an ASP.NET Core WebHost inside a Reliable Service using Kestrel as hello web server.</span></span>

<span data-ttu-id="ca5f4-215">Kestrel 根據 libuv 是 ASP.NET Core 的跨平台 web 伺服器，為跨平台非同步 I/O 程式庫。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-215">Kestrel is a cross-platform web server for ASP.NET Core based on libuv, a cross-platform asynchronous I/O library.</span></span> <span data-ttu-id="ca5f4-216">不同於 WebListener，Kestrel 不會使用集中式端點管理員，例如 http.sys。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-216">Unlike WebListener, Kestrel does not use a centralized endpoint manager such as *http.sys*.</span></span> <span data-ttu-id="ca5f4-217">且不同於 WebListener，Kestrel 不支援多個處理序之間的連接埠共用。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-217">And unlike WebListener, Kestrel does not support port sharing between multiple processes.</span></span> <span data-ttu-id="ca5f4-218">Kestrel 的每個執行個體必須使用唯一的連接埠。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-218">Each instance of Kestrel must use a unique port.</span></span>

![kestrel][4]

### <a name="kestrel-in-a-stateless-service"></a><span data-ttu-id="ca5f4-220">無狀態服務中的 Kestrel</span><span class="sxs-lookup"><span data-stu-id="ca5f4-220">Kestrel in a stateless service</span></span>
<span data-ttu-id="ca5f4-221">toouse`Kestrel`無狀態服務，在覆寫 hello`CreateServiceInstanceListeners`方法，並傳回`KestrelCommunicationListener`執行個體：</span><span class="sxs-lookup"><span data-stu-id="ca5f4-221">toouse `Kestrel` in a stateless service, override hello `CreateServiceInstanceListeners` method and return a `KestrelCommunicationListener` instance:</span></span>

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

### <a name="kestrel-in-a-stateful-service"></a><span data-ttu-id="ca5f4-222">具狀態服務中的 Kestrel</span><span class="sxs-lookup"><span data-stu-id="ca5f4-222">Kestrel in a stateful service</span></span>
<span data-ttu-id="ca5f4-223">toouse`Kestrel`具狀態服務，在覆寫 hello`CreateServiceReplicaListeners`方法，並傳回`KestrelCommunicationListener`執行個體：</span><span class="sxs-lookup"><span data-stu-id="ca5f4-223">toouse `Kestrel` in a stateful service, override hello `CreateServiceReplicaListeners` method and return a `KestrelCommunicationListener` instance:</span></span>

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

<span data-ttu-id="ca5f4-224">在此範例中的單一執行個體`IReliableStateManager`提供 toohello WebHost 相依性插入容器。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-224">In this example, a singleton instance of `IReliableStateManager` is provided toohello WebHost dependency injection container.</span></span> <span data-ttu-id="ca5f4-225">這並非絕對必要，但它可讓您 toouse`IReliableStateManager`和可靠的集合，在您的 MVC 控制器動作方法。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-225">This is not strictly necessary, but it allows you toouse `IReliableStateManager` and Reliable Collections in your MVC controller action methods.</span></span>

<span data-ttu-id="ca5f4-226">請注意，`Endpoint`組態名稱是**不**太提供`KestrelCommunicationListener`中可設定狀態的服務。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-226">Note that an `Endpoint` configuration name is **not** provided too`KestrelCommunicationListener` in a stateful service.</span></span> <span data-ttu-id="ca5f4-227">在 hello 之後 > 一節中詳細的說明。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-227">This is explained in more detail in hello following section.</span></span>

### <a name="endpoint-configuration"></a><span data-ttu-id="ca5f4-228">端點組態</span><span class="sxs-lookup"><span data-stu-id="ca5f4-228">Endpoint configuration</span></span>
<span data-ttu-id="ca5f4-229">`Endpoint`組態並不是必要的 toouse Kestrel。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-229">An `Endpoint` configuration is not required toouse Kestrel.</span></span> 

<span data-ttu-id="ca5f4-230">Kestrel 是簡單的獨立 web 伺服器。不同於 WebListener （或 HttpListener），就不需要`Endpoint`中的組態*ServiceManifest.xml*因為不需要 URL 註冊先前 toostarting。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-230">Kestrel is a simple stand-alone web server; unlike WebListener (or HttpListener), it does not need an `Endpoint` configuration in *ServiceManifest.xml* because it does not require URL registration prior toostarting.</span></span> 

#### <a name="use-kestrel-with-a-static-port"></a><span data-ttu-id="ca5f4-231">搭配使用 Kestrel 與靜態連接埠</span><span class="sxs-lookup"><span data-stu-id="ca5f4-231">Use Kestrel with a static port</span></span>
<span data-ttu-id="ca5f4-232">靜態連接埠可以設定在 hello`Endpoint`搭配 Kestrel ServiceManifest.xml 的組態。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-232">A static port can be configured in hello `Endpoint` configuration of ServiceManifest.xml for use with Kestrel.</span></span> <span data-ttu-id="ca5f4-233">雖然這並非絕對必要，它會提供兩個潛在的好處︰</span><span class="sxs-lookup"><span data-stu-id="ca5f4-233">Although this is not strictly necessary, it provides two potential benefits:</span></span>
 1. <span data-ttu-id="ca5f4-234">Hello 連接埠不是落在 hello 應用程式連接埠範圍中，如果它已透過 hello OS 防火牆開啟由服務網狀架構。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-234">If hello port does not fall in hello application port range, it is opened through hello OS firewall by Service Fabric.</span></span>
 2. <span data-ttu-id="ca5f4-235">hello 透過提供 URL tooyou`KestrelCommunicationListener`會使用此連接埠。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-235">hello URL provided tooyou through `KestrelCommunicationListener` will use this port.</span></span>

```xml
  <Resources>
    <Endpoints>
      <Endpoint Protocol="http" Name="ServiceEndpoint" Port="80" />
    </Endpoints>
  </Resources>
```

<span data-ttu-id="ca5f4-236">如果`Endpoint`是設定，其名稱必須傳入 hello`KestrelCommunicationListener`建構函式：</span><span class="sxs-lookup"><span data-stu-id="ca5f4-236">If an `Endpoint` is configured, its name must be passed into hello `KestrelCommunicationListener` constructor:</span></span> 

```csharp
new KestrelCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) => ...
```

<span data-ttu-id="ca5f4-237">如果`Endpoint`不使用組態，請省略 hello 中的 hello 名稱`KestrelCommunicationListener`建構函式。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-237">If an `Endpoint` configuration is not used, omit hello name in hello `KestrelCommunicationListener` constructor.</span></span> <span data-ttu-id="ca5f4-238">在此情況下，會使用動態連接埠。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-238">In this case, a dynamic port will be used.</span></span> <span data-ttu-id="ca5f4-239">請參閱 hello 下一節，如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-239">See hello next section for more information.</span></span>

#### <a name="use-kestrel-with-a-dynamic-port"></a><span data-ttu-id="ca5f4-240">搭配使用 Kestrel 與動態連接埠</span><span class="sxs-lookup"><span data-stu-id="ca5f4-240">Use Kestrel with a dynamic port</span></span>
<span data-ttu-id="ca5f4-241">Kestrel 無法使用從 hello hello 自動連接埠指派`Endpoint`組態在 ServiceManifest.xml 中，因為從自動連接埠指派`Endpoint`設定會指派唯一的連接埠，每個*主機處理序*與單一主機處理序可以包含多個 Kestrel 執行個體。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-241">Kestrel cannot use hello automatic port assignment from hello `Endpoint` configuration in ServiceManifest.xml, because automatic port assignment from an `Endpoint` configuration assigns a unique port per *host process*, and a single host process can contain multiple Kestrel instances.</span></span> <span data-ttu-id="ca5f4-242">因為 Kestrel 不支援連接埠共用，這並不會如每個 Kestrel 執行個體必須在唯一連接埠上開啟一般運作。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-242">Since Kestrel does not support port sharing, this does not work as each Kestrel instance must be opened on a unique port.</span></span>

<span data-ttu-id="ca5f4-243">toouse 動態連接埠指派與 Kestrel，只要省略 hello `Endpoint` ServiceManifest.xml 中的設定完全，並不會傳遞端點名稱 toohello`KestrelCommunicationListener`建構函式：</span><span class="sxs-lookup"><span data-stu-id="ca5f4-243">toouse dynamic port assignment with Kestrel, simply omit hello `Endpoint` configuration in ServiceManifest.xml entirely, and do not pass an endpoint name toohello `KestrelCommunicationListener` constructor:</span></span>

```csharp
new KestrelCommunicationListener(serviceContext, (url, listener) => ...
```

<span data-ttu-id="ca5f4-244">此設定會`KestrelCommunicationListener`會自動選取未使用的連接埠從 hello 應用程式連接埠範圍。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-244">In this configuration, `KestrelCommunicationListener` will automatically select an unused port from hello application port range.</span></span>

## <a name="scenarios-and-configurations"></a><span data-ttu-id="ca5f4-245">案例和組態</span><span class="sxs-lookup"><span data-stu-id="ca5f4-245">Scenarios and configurations</span></span>
<span data-ttu-id="ca5f4-246">本章節描述下列案例的 hello，並提供 hello 建議的網頁伺服器、 連接埠組態，Service Fabric 整合選項和其他設定 tooachieve 組合正常運作的服務：</span><span class="sxs-lookup"><span data-stu-id="ca5f4-246">This section describes hello following scenarios and provides hello recommended combination of web server, port configuration, Service Fabric integration options, and miscellaneous settings tooachieve a properly functioning service:</span></span>
 - <span data-ttu-id="ca5f4-247">外部公開 ASP.NET Core 無狀態服務</span><span class="sxs-lookup"><span data-stu-id="ca5f4-247">Externally exposed ASP.NET Core stateless service</span></span>
 - <span data-ttu-id="ca5f4-248">內部公開 ASP.NET Core 無狀態服務</span><span class="sxs-lookup"><span data-stu-id="ca5f4-248">Internal-only ASP.NET Core stateless service</span></span>
 - <span data-ttu-id="ca5f4-249">內部公開 ASP.NET Core 具狀態服務</span><span class="sxs-lookup"><span data-stu-id="ca5f4-249">Internal-only ASP.NET Core stateful service</span></span>

<span data-ttu-id="ca5f4-250">**外部公開**是一種可從外部 hello 叢集中，通常是透過負載平衡器連線的端點會公開服務。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-250">An **externally exposed** service is one that exposes an endpoint reachable from outside hello cluster, usually through a load balancer.</span></span>

<span data-ttu-id="ca5f4-251">**僅供內部使用**服務是其中一個端點，才可從 hello 叢集內存取。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-251">An **internal-only** service is one whose endpoint is only reachable from within hello cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="ca5f4-252">可設定狀態的服務端點通常不應該公開 toohello 網際網路。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-252">Stateful service endpoints generally should not be exposed toohello Internet.</span></span> <span data-ttu-id="ca5f4-253">Service Fabric 服務解析，例如 hello Azure 負載平衡器，不需要知道的負載平衡器後方的叢集將會無法 tooexpose 可設定狀態服務，因為 hello 負載平衡器將不能 toolocate 並路由傳送流量 toohello適當的可設定狀態服務複本。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-253">Clusters that are behind load balancers that are unaware of Service Fabric service resolution, such as hello Azure Load Balancer, will be unable tooexpose stateful services because hello load balancer will not be able toolocate and route traffic toohello appropriate stateful service replica.</span></span> 

### <a name="externally-exposed-aspnet-core-stateless-services"></a><span data-ttu-id="ca5f4-254">外部公開 ASP.NET Core 無狀態服務</span><span class="sxs-lookup"><span data-stu-id="ca5f4-254">Externally exposed ASP.NET Core stateless services</span></span>
<span data-ttu-id="ca5f4-255">WebListener 是 hello 建議在 Windows 上的外部的網際網路對向 HTTP 端點所公開的前端服務的網頁伺服器。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-255">WebListener is hello recommended web server for front-end services that expose external, Internet-facing HTTP endpoints on Windows.</span></span> <span data-ttu-id="ca5f4-256">它提供更好的保護以免於攻擊，並支援 Kestrel 所沒有的功能，例如 Windows 驗證和連接埠共用。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-256">It provides better protection against attacks and supports features that Kestrel does not, such as Windows Authentication and port sharing.</span></span> 

<span data-ttu-id="ca5f4-257">Kestrel 這一次不支援作為邊緣 (網際網路) 伺服器。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-257">Kestrel is not supported as an edge (Internet-facing) server at this time.</span></span> <span data-ttu-id="ca5f4-258">必須使用反向 proxy 伺服器，例如 IIS 或 Nginx toohandle 流量 hello 公用網際網路。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-258">A reverse proxy server such as IIS or Nginx must be used toohandle traffic from hello public Internet.</span></span>
 
<span data-ttu-id="ca5f4-259">當公開的 toohello 網際網路，無狀態服務應該使用的已知且穩定的端點是可連線透過負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-259">When exposed toohello Internet, a stateless service should use a well-known and stable endpoint that is reachable through a load balancer.</span></span> <span data-ttu-id="ca5f4-260">這是您將提供您的應用程式的 toousers hello URL。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-260">This is hello URL you will provide toousers of your application.</span></span> <span data-ttu-id="ca5f4-261">建議使用下列組態的 hello:</span><span class="sxs-lookup"><span data-stu-id="ca5f4-261">hello following configuration is recommended:</span></span>

|  |  | <span data-ttu-id="ca5f4-262">**注意事項**</span><span class="sxs-lookup"><span data-stu-id="ca5f4-262">**Notes**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ca5f4-263">Web 伺服器</span><span class="sxs-lookup"><span data-stu-id="ca5f4-263">Web server</span></span> | <span data-ttu-id="ca5f4-264">WebListener</span><span class="sxs-lookup"><span data-stu-id="ca5f4-264">WebListener</span></span> | <span data-ttu-id="ca5f4-265">如果 hello 服務只公開的 tooa 信任的網路，這類內部網路，就可能會使用 Kestrel。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-265">If hello service is only exposed tooa trusted network, such an intranet, Kestrel may be used.</span></span> <span data-ttu-id="ca5f4-266">否則，WebListener 是 hello 慣用選項。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-266">Otherwise, WebListener is hello preferred option.</span></span> |
| <span data-ttu-id="ca5f4-267">連接埠組態</span><span class="sxs-lookup"><span data-stu-id="ca5f4-267">Port configuration</span></span> | <span data-ttu-id="ca5f4-268">靜態</span><span class="sxs-lookup"><span data-stu-id="ca5f4-268">static</span></span> | <span data-ttu-id="ca5f4-269">已知的靜態連接埠應該設定在 hello`Endpoints`組態的 ServiceManifest.xml 中，例如 HTTP 為 80 或 443 的 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-269">A well-known static port should be configured in hello `Endpoints` configuration of ServiceManifest.xml, such as 80 for HTTP or 443 for HTTPS.</span></span> |
| <span data-ttu-id="ca5f4-270">ServiceFabricIntegrationOptions</span><span class="sxs-lookup"><span data-stu-id="ca5f4-270">ServiceFabricIntegrationOptions</span></span> | <span data-ttu-id="ca5f4-271">None</span><span class="sxs-lookup"><span data-stu-id="ca5f4-271">None</span></span> | <span data-ttu-id="ca5f4-272">hello`ServiceFabricIntegrationOptions.None`以便 hello 服務不會嘗試 toovalidate 內送要求的唯一識別碼設定 Service Fabric 整合中介軟體時應使用的選項。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-272">hello `ServiceFabricIntegrationOptions.None` option should be used when configuring Service Fabric integration middleware so that hello service does not attempt toovalidate incoming requests for a unique identifier.</span></span> <span data-ttu-id="ca5f4-273">外部應用程式的使用者將不會知道唯一 hello hello 中介軟體所使用的識別資訊。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-273">External users of your application will not know hello unique identifying information used by hello middleware.</span></span> |
| <span data-ttu-id="ca5f4-274">執行個體計數</span><span class="sxs-lookup"><span data-stu-id="ca5f4-274">Instance Count</span></span> | <span data-ttu-id="ca5f4-275">-1</span><span class="sxs-lookup"><span data-stu-id="ca5f4-275">-1</span></span> | <span data-ttu-id="ca5f4-276">在一般使用案例，hello 執行個體計數設定必須將設定太"-1"，以便可以從負載平衡器接收流量的所有節點上執行個體。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-276">In typical use cases, hello instance count setting should be set too"-1" so that an instance is available on all nodes that receive traffic from a load balancer.</span></span> |

<span data-ttu-id="ca5f4-277">如果多個外部公開的服務共用的 hello 相同設定的節點，則應該使用唯一的但穩定的 URL 路徑。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-277">If multiple externally exposed services share hello same set of nodes, a unique but stable URL path should be used.</span></span> <span data-ttu-id="ca5f4-278">這可以藉由修改 hello URL 提供設定 IWebHost 時完成。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-278">This can be accomplished by modifying hello URL provided when configuring IWebHost.</span></span> <span data-ttu-id="ca5f4-279">請注意這適用於僅 tooWebListener。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-279">Note this applies tooWebListener only.</span></span>

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

### <a name="internal-only-stateless-aspnet-core-service"></a><span data-ttu-id="ca5f4-280">僅供內部使用的無狀態 ASP.NET Core 服務</span><span class="sxs-lookup"><span data-stu-id="ca5f4-280">Internal-only stateless ASP.NET Core service</span></span>
<span data-ttu-id="ca5f4-281">只會從呼叫 hello 叢集內的無狀態服務應使用唯一的 Url，而且多個服務之間的 tooensure 合作時動態指派連接埠。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-281">Stateless services that are only called from within hello cluster should use unique URLs and dynamically assigned ports tooensure cooperation between multiple services.</span></span> <span data-ttu-id="ca5f4-282">建議使用下列組態的 hello:</span><span class="sxs-lookup"><span data-stu-id="ca5f4-282">hello following configuration is recommended:</span></span>

|  |  | <span data-ttu-id="ca5f4-283">**注意事項**</span><span class="sxs-lookup"><span data-stu-id="ca5f4-283">**Notes**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ca5f4-284">Web 伺服器</span><span class="sxs-lookup"><span data-stu-id="ca5f4-284">Web server</span></span> | <span data-ttu-id="ca5f4-285">Kestrel</span><span class="sxs-lookup"><span data-stu-id="ca5f4-285">Kestrel</span></span> | <span data-ttu-id="ca5f4-286">雖然 WebListener 可能用於內部無狀態服務，Kestrel 是 hello 建議伺服器 tooallow 多個服務執行個體 tooshare 主機。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-286">Although WebListener may be used for internal stateless services, Kestrel is hello recommended server tooallow multiple service instances tooshare a host.</span></span>  |
| <span data-ttu-id="ca5f4-287">連接埠組態</span><span class="sxs-lookup"><span data-stu-id="ca5f4-287">Port configuration</span></span> | <span data-ttu-id="ca5f4-288">動態指派</span><span class="sxs-lookup"><span data-stu-id="ca5f4-288">dynamically assigned</span></span> | <span data-ttu-id="ca5f4-289">多個具狀態服務的複本可能會共用主機處理序或主機作業系統，因此需要唯一的連接埠。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-289">Multiple replicas of a stateful service may share a host process or host operating system and thus will need unique ports.</span></span> |
| <span data-ttu-id="ca5f4-290">ServiceFabricIntegrationOptions</span><span class="sxs-lookup"><span data-stu-id="ca5f4-290">ServiceFabricIntegrationOptions</span></span> | <span data-ttu-id="ca5f4-291">UseUniqueServiceUrl</span><span class="sxs-lookup"><span data-stu-id="ca5f4-291">UseUniqueServiceUrl</span></span> | <span data-ttu-id="ca5f4-292">使用動態連接埠指派，這個設定會被誤認為 hello 識別問題稍早所述。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-292">With dynamic port assignment, this setting prevents hello mistaken identity issue described earlier.</span></span> |
| <span data-ttu-id="ca5f4-293">InstanceCount</span><span class="sxs-lookup"><span data-stu-id="ca5f4-293">InstanceCount</span></span> | <span data-ttu-id="ca5f4-294">any</span><span class="sxs-lookup"><span data-stu-id="ca5f4-294">any</span></span> | <span data-ttu-id="ca5f4-295">hello 執行個體計數設定可以設定 tooany 值必要 toooperate hello 服務。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-295">hello instance count setting can be set tooany value necessary toooperate hello service.</span></span> |

### <a name="internal-only-stateful-aspnet-core-service"></a><span data-ttu-id="ca5f4-296">僅供內部使用的具狀態 ASP.NET Core 服務</span><span class="sxs-lookup"><span data-stu-id="ca5f4-296">Internal-only stateful ASP.NET Core service</span></span>
<span data-ttu-id="ca5f4-297">只會從呼叫 hello 叢集內的可設定狀態服務應該使用多個服務之間的動態指派連接埠 tooensure 合作。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-297">Stateful services that are only called from within hello cluster should use dynamically assigned ports tooensure cooperation between multiple services.</span></span> <span data-ttu-id="ca5f4-298">建議使用下列組態的 hello:</span><span class="sxs-lookup"><span data-stu-id="ca5f4-298">hello following configuration is recommended:</span></span>

|  |  | <span data-ttu-id="ca5f4-299">**注意事項**</span><span class="sxs-lookup"><span data-stu-id="ca5f4-299">**Notes**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ca5f4-300">Web 伺服器</span><span class="sxs-lookup"><span data-stu-id="ca5f4-300">Web server</span></span> | <span data-ttu-id="ca5f4-301">Kestrel</span><span class="sxs-lookup"><span data-stu-id="ca5f4-301">Kestrel</span></span> | <span data-ttu-id="ca5f4-302">hello`WebListenerCommunicationListener`不是使用可設定狀態的服務複本共用主控件程序。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-302">hello `WebListenerCommunicationListener` is not designed for use by stateful services in which replicas share a host process.</span></span> |
| <span data-ttu-id="ca5f4-303">連接埠組態</span><span class="sxs-lookup"><span data-stu-id="ca5f4-303">Port configuration</span></span> | <span data-ttu-id="ca5f4-304">動態指派</span><span class="sxs-lookup"><span data-stu-id="ca5f4-304">dynamically assigned</span></span> | <span data-ttu-id="ca5f4-305">多個具狀態服務的複本可能會共用主機處理序或主機作業系統，因此需要唯一的連接埠。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-305">Multiple replicas of a stateful service may share a host process or host operating system and thus will need unique ports.</span></span> |
| <span data-ttu-id="ca5f4-306">ServiceFabricIntegrationOptions</span><span class="sxs-lookup"><span data-stu-id="ca5f4-306">ServiceFabricIntegrationOptions</span></span> | <span data-ttu-id="ca5f4-307">UseUniqueServiceUrl</span><span class="sxs-lookup"><span data-stu-id="ca5f4-307">UseUniqueServiceUrl</span></span> | <span data-ttu-id="ca5f4-308">使用動態連接埠指派，這個設定會被誤認為 hello 識別問題稍早所述。</span><span class="sxs-lookup"><span data-stu-id="ca5f4-308">With dynamic port assignment, this setting prevents hello mistaken identity issue described earlier.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ca5f4-309">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ca5f4-309">Next steps</span></span>
[<span data-ttu-id="ca5f4-310">使用 Visual Studio 偵錯 Service Fabric 應用程式</span><span class="sxs-lookup"><span data-stu-id="ca5f4-310">Debug your Service Fabric application by using Visual Studio</span></span>](service-fabric-debugging-your-application.md)

<!--Image references-->
[0]:./media/service-fabric-reliable-services-communication-aspnetcore/webhost-standalone.png
[1]:./media/service-fabric-reliable-services-communication-aspnetcore/webhost-servicefabric.png
[2]:./media/service-fabric-reliable-services-communication-aspnetcore/integration.png
[3]:./media/service-fabric-reliable-services-communication-aspnetcore/httpsys.png
[4]:./media/service-fabric-reliable-services-communication-aspnetcore/kestrel.png
