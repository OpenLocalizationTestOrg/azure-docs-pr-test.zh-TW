---
title: "使用 ASP.NET Web API 的服務通訊 |Microsoft Docs"
description: "了解如何藉由使用 ASP.NET Web API 與 OWIN 自我裝載，在 Reliable Services API 中逐步實作服務通訊。"
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
ms.date: 02/10/2017
ms.author: vturecek
redirect_url: /azure/service-fabric/service-fabric-reliable-services-communication-aspnetcore
ms.openlocfilehash: 73b7e1c0cb93ae7c54780a3aab837b0e5bcdb0a0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-service-fabric-web-api-services-with-owin-self-hosting"></a><span data-ttu-id="75b6f-103">開始使用：Service Fabric Web API 服務與 OWIN 自我裝載 | Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="75b6f-103">Get started: Service Fabric Web API services with OWIN self-hosting</span></span>
<span data-ttu-id="75b6f-104">Azure Service Fabric 讓您能決定您的服務與使用者以及服務彼此之間如何進行通訊。</span><span class="sxs-lookup"><span data-stu-id="75b6f-104">Azure Service Fabric puts the power in your hands when you're deciding how you want your services to communicate with users and with each other.</span></span> <span data-ttu-id="75b6f-105">本教學課程著重於使用 ASP.NET Web API 與 Open Web Interface for .NET (OWIN) 自我裝載在 Service Fabric 的 Reliable Services API 中實作服務通訊。</span><span class="sxs-lookup"><span data-stu-id="75b6f-105">This tutorial focuses on implementing service communication using ASP.NET Web API with Open Web Interface for .NET (OWIN) self-hosting in Service Fabric's Reliable Services API.</span></span> <span data-ttu-id="75b6f-106">我們將深入探討 Reliable Services 隨插即用的通訊 API。</span><span class="sxs-lookup"><span data-stu-id="75b6f-106">We'll delve deeply into the Reliable Services pluggable communication API.</span></span> <span data-ttu-id="75b6f-107">我們也將在逐步範例中使用 Web API，示範如何設定自訂通訊接聽程式。</span><span class="sxs-lookup"><span data-stu-id="75b6f-107">We'll also use Web API in a step-by-step example to show you how to set up a custom communication listener.</span></span>

## <a name="introduction-to-web-api-in-service-fabric"></a><span data-ttu-id="75b6f-108">Service Fabric 中的 Web API 簡介</span><span class="sxs-lookup"><span data-stu-id="75b6f-108">Introduction to Web API in Service Fabric</span></span>
<span data-ttu-id="75b6f-109">ASP.NET Web API 是在 .NET Framework 建置 HTTP API 的常用且功能強大的架構。</span><span class="sxs-lookup"><span data-stu-id="75b6f-109">ASP.NET Web API is a popular and powerful framework for building HTTP APIs on top of the .NET Framework.</span></span> <span data-ttu-id="75b6f-110">如果您不熟悉此架構，請參閱 [開始使用 ASP.NET Web API 2](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api) 以深入了解。</span><span class="sxs-lookup"><span data-stu-id="75b6f-110">If you're not already familiar with the framework, see [Getting started with ASP.NET Web API 2](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api) to learn more.</span></span>

<span data-ttu-id="75b6f-111">Service Fabric 中的 Web API 是您熟知而且喜愛的相同 ASP.NET Web API。</span><span class="sxs-lookup"><span data-stu-id="75b6f-111">Web API in Service Fabric is the same ASP.NET Web API you know and love.</span></span> <span data-ttu-id="75b6f-112">不同之處在於您如何裝載  Web API 應用程式。</span><span class="sxs-lookup"><span data-stu-id="75b6f-112">The difference is in how you *host* a Web API application.</span></span> <span data-ttu-id="75b6f-113">您不會使用 Microsoft Internet Information Services (IIS)。</span><span class="sxs-lookup"><span data-stu-id="75b6f-113">You won't be using Microsoft Internet Information Services (IIS).</span></span> <span data-ttu-id="75b6f-114">若要進一步了解差異，讓我們將它分成兩個部分：</span><span class="sxs-lookup"><span data-stu-id="75b6f-114">To better understand the difference, let's break it into two parts:</span></span>

1. <span data-ttu-id="75b6f-115">Web API 應用程式 (包括控制器和模型)</span><span class="sxs-lookup"><span data-stu-id="75b6f-115">The Web API application (including controllers and models)</span></span>
2. <span data-ttu-id="75b6f-116">主機 (Web 伺服器，通常是 IIS)</span><span class="sxs-lookup"><span data-stu-id="75b6f-116">The host (the web server, usually IIS)</span></span>

<span data-ttu-id="75b6f-117">Web API 應用程式本身不會變更。</span><span class="sxs-lookup"><span data-stu-id="75b6f-117">A Web API application itself doesn't change.</span></span> <span data-ttu-id="75b6f-118">它與您過去撰寫的 Web API 應用程式並無不同，您應該能夠直接搬移大部分的應用程式程式碼。</span><span class="sxs-lookup"><span data-stu-id="75b6f-118">It's no different from Web API applications you may have written in the past, and you should be able to simply move over most of your application code.</span></span> <span data-ttu-id="75b6f-119">但是如果您裝載在 IIS 上，裝載應用程式的位置可能會與您過去習慣的稍有不同。</span><span class="sxs-lookup"><span data-stu-id="75b6f-119">But if you've been hosting on IIS, where you host the application may be a little different from what you're used to.</span></span> <span data-ttu-id="75b6f-120">在我們進入裝載部分之前，讓我們從較熟悉的部分開始：Web API 應用程式。</span><span class="sxs-lookup"><span data-stu-id="75b6f-120">Before we get to the hosting part, let's start with something more familiar: the Web API application.</span></span>

## <a name="create-the-application"></a><span data-ttu-id="75b6f-121">建立應用程式</span><span class="sxs-lookup"><span data-stu-id="75b6f-121">Create the application</span></span>
<span data-ttu-id="75b6f-122">若要開始，請在 Visual Studio 2015 中，建立具有單一無狀態服務的新 Service Fabric 應用程式。</span><span class="sxs-lookup"><span data-stu-id="75b6f-122">Start by creating a new Service Fabric application with a single stateless service in Visual Studio 2015.</span></span>

<span data-ttu-id="75b6f-123">使用 Web API 的無狀態服務有 Visual Studio 範本可供使用。</span><span class="sxs-lookup"><span data-stu-id="75b6f-123">A Visual Studio template for a stateless service using Web API is available to you.</span></span> <span data-ttu-id="75b6f-124">在本教學課程中，我們將從頭建置 Web API 專案，這就是您選取此範本時所會得到的結果。</span><span class="sxs-lookup"><span data-stu-id="75b6f-124">In this tutorial, we'll build a Web API project from scratch that results in what you'd get if you selected this template.</span></span>

<span data-ttu-id="75b6f-125">選取空白的無狀態服務專案，以了解如何從頭建置 Web API 專案，或者您可以從無狀態服務 Web API 範本開始，只需依照指示進行。</span><span class="sxs-lookup"><span data-stu-id="75b6f-125">Select a blank Stateless Service project to learn how to build a Web API project from scratch, or you can start with the stateless service Web API template and simply follow along.</span></span>  

<span data-ttu-id="75b6f-126">第一個步驟是提取一些 Web API 的 NuGet 封裝。</span><span class="sxs-lookup"><span data-stu-id="75b6f-126">The first step is to pull in some NuGet packages for Web API.</span></span> <span data-ttu-id="75b6f-127">我們想要使用的封裝是 Microsoft.AspNet.WebApi.OwinSelfHost。</span><span class="sxs-lookup"><span data-stu-id="75b6f-127">The package we want to use is Microsoft.AspNet.WebApi.OwinSelfHost.</span></span> <span data-ttu-id="75b6f-128">此套件包含所有必要的 Web API 套件和主機  套件。</span><span class="sxs-lookup"><span data-stu-id="75b6f-128">This package includes all the necessary Web API packages and the *host* packages.</span></span> <span data-ttu-id="75b6f-129">這在稍後會很重要。</span><span class="sxs-lookup"><span data-stu-id="75b6f-129">This will be important later.</span></span>

<span data-ttu-id="75b6f-130">安裝封裝後，您就可以馬上開始建置出基本的 Web API 專案結構。</span><span class="sxs-lookup"><span data-stu-id="75b6f-130">After the packages have been installed, you can begin building out the basic Web API project structure.</span></span> <span data-ttu-id="75b6f-131">如果您已使用 Web API，專案結構看起來應該很熟悉。</span><span class="sxs-lookup"><span data-stu-id="75b6f-131">If you've used Web API, the project structure should look very familiar.</span></span> <span data-ttu-id="75b6f-132">首先新增 `Controllers` 目錄和簡單值控制站︰</span><span class="sxs-lookup"><span data-stu-id="75b6f-132">Start by adding a `Controllers` directory and a simple values controller:</span></span>

<span data-ttu-id="75b6f-133">**ValuesController.cs**</span><span class="sxs-lookup"><span data-stu-id="75b6f-133">**ValuesController.cs**</span></span>

```csharp
using System.Collections.Generic;
using System.Web.Http;

namespace WebService.Controllers
{
    public class ValuesController : ApiController
    {
        // GET api/values 
        public IEnumerable<string> Get()
        {
            return new string[] { "value1", "value2" };
        }

        // GET api/values/5 
        public string Get(int id)
        {
            return "value";
        }

        // POST api/values 
        public void Post([FromBody]string value)
        {
        }

        // PUT api/values/5 
        public void Put(int id, [FromBody]string value)
        {
        }

        // DELETE api/values/5 
        public void Delete(int id)
        {
        }
    }
}

```

<span data-ttu-id="75b6f-134">接下來，在專案根目錄加入 Startup 類別以註冊路由、格式器及任何其他組態設定。</span><span class="sxs-lookup"><span data-stu-id="75b6f-134">Next, add a Startup class at the project root to register the routing, formatters, and any other configuration setup.</span></span> <span data-ttu-id="75b6f-135">這也是 Web API 插入至 *主機*的位置，稍後我們將再重返此處。</span><span class="sxs-lookup"><span data-stu-id="75b6f-135">This is also where Web API plugs in to the *host*, which will be revisited again later.</span></span> 

<span data-ttu-id="75b6f-136">**Startup.cs**</span><span class="sxs-lookup"><span data-stu-id="75b6f-136">**Startup.cs**</span></span>

```csharp
using System.Web.Http;
using Owin;

namespace WebService
{
    public static class Startup
    {
        public static void ConfigureApp(IAppBuilder appBuilder)
        {
            // Configure Web API for self-host. 
            HttpConfiguration config = new HttpConfiguration();

            config.Routes.MapHttpRoute(
                name: "DefaultApi",
                routeTemplate: "api/{controller}/{id}",
                defaults: new { id = RouteParameter.Optional }
            );

            appBuilder.UseWebApi(config);
        }
    }
}
```

<span data-ttu-id="75b6f-137">應用程式部分就這樣。</span><span class="sxs-lookup"><span data-stu-id="75b6f-137">That's it for the application part.</span></span> <span data-ttu-id="75b6f-138">現在我們只設定基本的 Web API 專案配置。</span><span class="sxs-lookup"><span data-stu-id="75b6f-138">At this point, we've set up just the basic Web API project layout.</span></span> <span data-ttu-id="75b6f-139">到目前為止，看起來應該與您過去可能已撰寫的 Web API 專案或基本的 Web API 範本有太多不同。</span><span class="sxs-lookup"><span data-stu-id="75b6f-139">So far, it shouldn't look much different from Web API projects you may have written in the past or from the basic Web API template.</span></span> <span data-ttu-id="75b6f-140">您的商務邏輯如往常般在控制器和模型中運作。</span><span class="sxs-lookup"><span data-stu-id="75b6f-140">Your business logic goes in the controllers and models as usual.</span></span>

<span data-ttu-id="75b6f-141">現在我們怎麼辦才能實際執行裝載？</span><span class="sxs-lookup"><span data-stu-id="75b6f-141">Now what do we do about hosting so that we can actually run it?</span></span>

## <a name="service-hosting"></a><span data-ttu-id="75b6f-142">服務裝載</span><span class="sxs-lookup"><span data-stu-id="75b6f-142">Service hosting</span></span>
<span data-ttu-id="75b6f-143">在 Service Fabric 中，您的服務會在服務主機處理序 中執行，這是執行您的服務程式碼的可執行檔。</span><span class="sxs-lookup"><span data-stu-id="75b6f-143">In Service Fabric, your service runs in a *service host process*, an executable file that runs your service code.</span></span> <span data-ttu-id="75b6f-144">當您使用 Reliable Services API 撰寫服務時，您的服務專案只會編譯註冊您的服務類型並執行程式碼的可執行檔。</span><span class="sxs-lookup"><span data-stu-id="75b6f-144">When you write a service by using the Reliable Services API, your service project just compiles to an executable file that registers your service type and runs your code.</span></span> <span data-ttu-id="75b6f-145">當您在 .NET 中的 Service Fabric 上撰寫服務時，在大部分情況下都是如此。</span><span class="sxs-lookup"><span data-stu-id="75b6f-145">This is true in most cases when you write a service on Service Fabric in .NET.</span></span> <span data-ttu-id="75b6f-146">當您在無狀態服務專案中開啟 Program.cs，您應該會看到：</span><span class="sxs-lookup"><span data-stu-id="75b6f-146">When you open Program.cs in the stateless service project, you should see:</span></span>

```csharp
using System;
using System.Diagnostics;
using System.Threading;
using Microsoft.ServiceFabric.Services.Runtime;

internal static class Program
{
    private static void Main()
    {
        try
        {
            ServiceRuntime.RegisterServiceAsync("WebServiceType",
                context => new WebService(context)).GetAwaiter().GetResult();

            ServiceEventSource.Current.ServiceTypeRegistered(Process.GetCurrentProcess().Id, typeof(WebService).Name);

            // Prevents this host process from terminating so services keeps running. 
            Thread.Sleep(Timeout.Infinite);
        }
        catch (Exception e)
        {
            ServiceEventSource.Current.ServiceHostInitializationFailed(e.ToString());
            throw;
        }
    }
}

```

<span data-ttu-id="75b6f-147">如果看起來疑似主控台應用程式的進入點，這是因為它是。</span><span class="sxs-lookup"><span data-stu-id="75b6f-147">If that looks suspiciously like the entry point to a console application, that's because it is.</span></span>

<span data-ttu-id="75b6f-148">關於服務裝載處理序和服務註冊的進一步詳細資料已超出本文的範圍。</span><span class="sxs-lookup"><span data-stu-id="75b6f-148">Further details about the service host process and service registration are beyond the scope of this article.</span></span> <span data-ttu-id="75b6f-149">但是現在請務必了解您的服務程式碼已在自己的處理序中執行 。</span><span class="sxs-lookup"><span data-stu-id="75b6f-149">But it's important to know for now that *your service code is running in its own process*.</span></span>

## <a name="self-host-web-api-with-an-owin-host"></a><span data-ttu-id="75b6f-150">自我裝載 Web API 與 OWIN 主機</span><span class="sxs-lookup"><span data-stu-id="75b6f-150">Self-host Web API with an OWIN host</span></span>
<span data-ttu-id="75b6f-151">假設您的 Web API 應用程式程式碼裝載在自己的處理序中，您如何將它連結到 Web 伺服器？</span><span class="sxs-lookup"><span data-stu-id="75b6f-151">Given that your Web API application code is hosted in its own process, how do you hook it up to a web server?</span></span> <span data-ttu-id="75b6f-152">輸入 [OWIN](http://owin.org/)。</span><span class="sxs-lookup"><span data-stu-id="75b6f-152">Enter [OWIN](http://owin.org/).</span></span> <span data-ttu-id="75b6f-153">OWIN 只是 .NET Web 應用程式和 Web 伺服器之間的合約。</span><span class="sxs-lookup"><span data-stu-id="75b6f-153">OWIN is simply a contract between .NET web applications and web servers.</span></span> <span data-ttu-id="75b6f-154">傳統上使用 ASP.NET (直到 MVC 5) 時，Web 應用程式已透過 System.Web 緊密結合至 IIS。</span><span class="sxs-lookup"><span data-stu-id="75b6f-154">Traditionally when ASP.NET (up to MVC 5) is used, the web application is tightly coupled to IIS through System.Web.</span></span> <span data-ttu-id="75b6f-155">不過，Web API 會實作 OWIN，所以您可以撰寫獨立於裝載它的 Web 伺服器的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="75b6f-155">However, Web API implements OWIN, so you can write a web application that is decoupled from the web server that hosts it.</span></span> <span data-ttu-id="75b6f-156">因此，您可以使用可在自己的程序中啟動的自我裝載  OWIN web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="75b6f-156">Because of this, you can use a *self-hosted* OWIN web server that you can start in your own process.</span></span> <span data-ttu-id="75b6f-157">這樣完全符合我們先前所提到的 Service Fabric 裝載模型。</span><span class="sxs-lookup"><span data-stu-id="75b6f-157">This fits perfectly with the Service Fabric hosting model we just described.</span></span>

<span data-ttu-id="75b6f-158">在本文中，我們將使用 Katana 做為 Web API 應用程式的 OWIN 主機。</span><span class="sxs-lookup"><span data-stu-id="75b6f-158">In this article, we'll use Katana as the OWIN host for the Web API application.</span></span> <span data-ttu-id="75b6f-159">Katana 是開放原始碼 OWIN 主機實作，它是以 [System.Net.HttpListener](https://msdn.microsoft.com/library/system.net.httplistener.aspx) 和 Windows [HTTP 伺服器 API](https://msdn.microsoft.com/library/windows/desktop/aa364510.aspx) 為基礎而建置。</span><span class="sxs-lookup"><span data-stu-id="75b6f-159">Katana is an open-source OWIN host implementation built on [System.Net.HttpListener](https://msdn.microsoft.com/library/system.net.httplistener.aspx) and the Windows [HTTP Server API](https://msdn.microsoft.com/library/windows/desktop/aa364510.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="75b6f-160">若要深入了解 Katana，請移至 [Katana 網站](http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana)。</span><span class="sxs-lookup"><span data-stu-id="75b6f-160">To learn more about Katana, go to the [Katana site](http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana).</span></span> <span data-ttu-id="75b6f-161">如需如何使用 Katana 自我裝載 Web API 的快速概觀，請參閱 [使用 OWIN 自我裝載 ASP.NET Web API 2](http://www.asp.net/web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api)。</span><span class="sxs-lookup"><span data-stu-id="75b6f-161">For a quick overview of how to use Katana to self-host Web API, see [Use OWIN to Self-Host ASP.NET Web API 2](http://www.asp.net/web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api).</span></span>
> 
> 

## <a name="set-up-the-web-server"></a><span data-ttu-id="75b6f-162">設定 Web 伺服器</span><span class="sxs-lookup"><span data-stu-id="75b6f-162">Set up the web server</span></span>
<span data-ttu-id="75b6f-163">Reliable Services API 提供通訊進入點，您可在其中插入通訊堆疊，讓使用者和用戶端連線到服務：</span><span class="sxs-lookup"><span data-stu-id="75b6f-163">The Reliable Services API provides a communication entry point where you can plug in communication stacks that allow users and clients to connect to the service:</span></span>

```csharp

protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    ...
}

```

<span data-ttu-id="75b6f-164">Web 伺服器 (和您未來使用的任何其他通訊堆疊，例如 WebSockets) 應該使用 ICommunicationListener 介面來正確地與系統整合。</span><span class="sxs-lookup"><span data-stu-id="75b6f-164">The web server (and any other communication stack you use in the future, such as WebSockets) should use the ICommunicationListener interface to integrate correctly with the system.</span></span> <span data-ttu-id="75b6f-165">這樣做的原因會在接下來的步驟中變得明顯。</span><span class="sxs-lookup"><span data-stu-id="75b6f-165">The reasons for this will become more apparent in the following steps.</span></span>

<span data-ttu-id="75b6f-166">首先，建立一個稱為 OwinCommunicationListener 的類別，其實作 ICommunicationListener：</span><span class="sxs-lookup"><span data-stu-id="75b6f-166">First, create a class called OwinCommunicationListener that implements ICommunicationListener:</span></span>

<span data-ttu-id="75b6f-167">**OwinCommunicationListener.cs：**</span><span class="sxs-lookup"><span data-stu-id="75b6f-167">**OwinCommunicationListener.cs**</span></span>

```csharp
using Microsoft.Owin.Hosting;
using Microsoft.ServiceFabric.Services.Communication.Runtime;
using Owin;
using System;
using System.Fabric;
using System.Globalization;
using System.Threading;
using System.Threading.Tasks;

namespace WebService
{
    internal class OwinCommunicationListener : ICommunicationListener
    {
        public void Abort()
        {
        }

        public Task CloseAsync(CancellationToken cancellationToken)
        {
        }

        public Task<string> OpenAsync(CancellationToken cancellationToken)
        {
        }
    }
}
```

<span data-ttu-id="75b6f-168">ICommunicationListener 介面提供三個方法來管理服務的通訊接聽程式：</span><span class="sxs-lookup"><span data-stu-id="75b6f-168">The ICommunicationListener interface provides three methods to manage a communication listener for your service:</span></span>

* <span data-ttu-id="75b6f-169">。</span><span class="sxs-lookup"><span data-stu-id="75b6f-169">*OpenAsync*.</span></span> <span data-ttu-id="75b6f-170">開始接聽要求。</span><span class="sxs-lookup"><span data-stu-id="75b6f-170">Start listening for requests.</span></span>
* <span data-ttu-id="75b6f-171">。</span><span class="sxs-lookup"><span data-stu-id="75b6f-171">*CloseAsync*.</span></span> <span data-ttu-id="75b6f-172">停止接聽要求，完成任何進行中的要求，並正常關機。</span><span class="sxs-lookup"><span data-stu-id="75b6f-172">Stop listening for requests, finish any in-flight requests, and shut down gracefully.</span></span>
* <span data-ttu-id="75b6f-173">中止。</span><span class="sxs-lookup"><span data-stu-id="75b6f-173">*Abort*.</span></span> <span data-ttu-id="75b6f-174">取消所有項目，並立即停止。</span><span class="sxs-lookup"><span data-stu-id="75b6f-174">Cancel everything and stop immediately.</span></span>

<span data-ttu-id="75b6f-175">若要開始，請為接聽程式運作所需的項目新增私用類別成員。</span><span class="sxs-lookup"><span data-stu-id="75b6f-175">To get started, add private class members for things the listener will need to function.</span></span> <span data-ttu-id="75b6f-176">這些會透過建構函式初始化，並在您稍後設定接聽 URL 時使用。</span><span class="sxs-lookup"><span data-stu-id="75b6f-176">These will be initialized through the constructor and used later when you set up the listening URL.</span></span>

```csharp
internal class OwinCommunicationListener : ICommunicationListener
{
    private readonly ServiceEventSource eventSource;
    private readonly Action<IAppBuilder> startup;
    private readonly ServiceContext serviceContext;
    private readonly string endpointName;
    private readonly string appRoot;

    private IDisposable webApp;
    private string publishAddress;
    private string listeningAddress;

    public OwinCommunicationListener(Action<IAppBuilder> startup, ServiceContext serviceContext, ServiceEventSource eventSource, string endpointName)
        : this(startup, serviceContext, eventSource, endpointName, null)
    {
    }

    public OwinCommunicationListener(Action<IAppBuilder> startup, ServiceContext serviceContext, ServiceEventSource eventSource, string endpointName, string appRoot)
    {
        if (startup == null)
        {
            throw new ArgumentNullException(nameof(startup));
        }

        if (serviceContext == null)
        {
            throw new ArgumentNullException(nameof(serviceContext));
        }

        if (endpointName == null)
        {
            throw new ArgumentNullException(nameof(endpointName));
        }

        if (eventSource == null)
        {
            throw new ArgumentNullException(nameof(eventSource));
        }

        this.startup = startup;
        this.serviceContext = serviceContext;
        this.endpointName = endpointName;
        this.eventSource = eventSource;
        this.appRoot = appRoot;
    }


    ...

```

## <a name="implement-openasync"></a><span data-ttu-id="75b6f-177">實作 OpenAsync</span><span class="sxs-lookup"><span data-stu-id="75b6f-177">Implement OpenAsync</span></span>
<span data-ttu-id="75b6f-178">若要設定 Web 伺服器，您需要兩項資訊：</span><span class="sxs-lookup"><span data-stu-id="75b6f-178">To set up the web server, you need two pieces of information:</span></span>

* <span data-ttu-id="75b6f-179">*URL 路徑前置詞*。</span><span class="sxs-lookup"><span data-stu-id="75b6f-179">*A URL path prefix*.</span></span> <span data-ttu-id="75b6f-180">雖然這是選擇性的，但您最好現在就設定，以便您能安全地在應用程式中裝載多個 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="75b6f-180">Although this is optional, it's good for you to set this up now so that you can safely host multiple web services in your application.</span></span>
* <span data-ttu-id="75b6f-181">*連接埠*。</span><span class="sxs-lookup"><span data-stu-id="75b6f-181">*A port*.</span></span>

<span data-ttu-id="75b6f-182">在您抓取 Web 伺服器的連接埠之前，必須了解 Service Fabric 提供一個應用程式層，做為您的應用程式與其執行所在之基礎作業系統之間的緩衝區。</span><span class="sxs-lookup"><span data-stu-id="75b6f-182">Before you get a port for the web server, it's important that you understand that Service Fabric provides an application layer that acts as a buffer between your application and the underlying operating system that it runs on.</span></span> <span data-ttu-id="75b6f-183">因此，Service Fabric 讓您能夠設定服務的端點。</span><span class="sxs-lookup"><span data-stu-id="75b6f-183">As such, Service Fabric provides a way to configure *endpoints* for your services.</span></span> <span data-ttu-id="75b6f-184">Service Fabric 可確保端點可供您的服務使用。</span><span class="sxs-lookup"><span data-stu-id="75b6f-184">Service Fabric ensures that endpoints are available for your service to use.</span></span> <span data-ttu-id="75b6f-185">如此一來，您就不用在基礎作業系統環境中自行設定它們。</span><span class="sxs-lookup"><span data-stu-id="75b6f-185">This way, you don't have to configure them yourself in the underlying OS environment.</span></span> <span data-ttu-id="75b6f-186">您可以輕易在不同環境中裝載 Service Fabric 應用程式，而不必對您的應用程式進行任何變更。</span><span class="sxs-lookup"><span data-stu-id="75b6f-186">You can easily host your Service Fabric application in different environments without having to make any changes to your application.</span></span> <span data-ttu-id="75b6f-187">(例如，您可以在 Azure 或您自己的資料中心內裝載相同的應用程式。)</span><span class="sxs-lookup"><span data-stu-id="75b6f-187">(For example, you can host the same application in Azure or in your own datacenter.)</span></span>

<span data-ttu-id="75b6f-188">在 PackageRoot\ServiceManifest.xml 中設定 HTTP 端點：</span><span class="sxs-lookup"><span data-stu-id="75b6f-188">Configure an HTTP endpoint in PackageRoot\ServiceManifest.xml:</span></span>

```xml
<Resources>
    <Endpoints>
        <Endpoint Name="ServiceEndpoint" Type="Input" Protocol="http" Port="8281" />
    </Endpoints>
</Resources>

```

<span data-ttu-id="75b6f-189">這個步驟很重要，因為服務裝載處理序要在受限制的認證 (在 Windows 上的網路服務) 之下執行。</span><span class="sxs-lookup"><span data-stu-id="75b6f-189">This step is important because the service host process runs under restricted credentials (Network Service on Windows).</span></span> <span data-ttu-id="75b6f-190">這表示您的服務並沒有自行設定 HTTP 端點的存取權。</span><span class="sxs-lookup"><span data-stu-id="75b6f-190">This means that your service won't have access to set up an HTTP endpoint on its own.</span></span> <span data-ttu-id="75b6f-191">藉由使用端點組態，Service Fabric 會知道要為服務將接聽的 URL 設定適當的存取控制清單 (ACL)。</span><span class="sxs-lookup"><span data-stu-id="75b6f-191">By using the endpoint configuration, Service Fabric knows to set up the proper access control list (ACL) for the URL that the service will listen on.</span></span> <span data-ttu-id="75b6f-192">Service Fabric 也會提供標準位置來設定端點。</span><span class="sxs-lookup"><span data-stu-id="75b6f-192">Service Fabric also provides a standard place to configure endpoints.</span></span>

<span data-ttu-id="75b6f-193">返回 OwinCommunicationListener.cs 中，您可以開始實作 OpenAsync。</span><span class="sxs-lookup"><span data-stu-id="75b6f-193">Back in OwinCommunicationListener.cs, you can start implementing OpenAsync.</span></span> <span data-ttu-id="75b6f-194">您會從此處啟動 Web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="75b6f-194">This is where you start the web server.</span></span> <span data-ttu-id="75b6f-195">首先，取得端點資訊，並建立服務將接聽的 URL。</span><span class="sxs-lookup"><span data-stu-id="75b6f-195">First, get the endpoint information and create the URL that the service will listen on.</span></span> <span data-ttu-id="75b6f-196">視接聽程式使用於無狀態服務或具狀態服務而定，URL 會有所不同。</span><span class="sxs-lookup"><span data-stu-id="75b6f-196">The URL will be different depending on whether the listener is used in a stateless service or a stateful service.</span></span> <span data-ttu-id="75b6f-197">若為具狀態服務，接聽程式必須針對它所接聽的每個具狀態服務複本建立唯一的位址。</span><span class="sxs-lookup"><span data-stu-id="75b6f-197">For a stateful service, the listener needs to create a unique address for every stateful service replica it listens on.</span></span> <span data-ttu-id="75b6f-198">若為無狀態服務，此位址可以更簡單。</span><span class="sxs-lookup"><span data-stu-id="75b6f-198">For stateless services, the address can be much simpler.</span></span> 

```csharp
public Task<string> OpenAsync(CancellationToken cancellationToken)
{
    var serviceEndpoint = this.serviceContext.CodePackageActivationContext.GetEndpoint(this.endpointName);
    var protocol = serviceEndpoint.Protocol;
    int port = serviceEndpoint.Port;

    if (this.serviceContext is StatefulServiceContext)
    {
        StatefulServiceContext statefulServiceContext = this.serviceContext as StatefulServiceContext;

        this.listeningAddress = string.Format(
            CultureInfo.InvariantCulture,
            "{0}://+:{1}/{2}{3}/{4}/{5}",
            protocol,
            port,
            string.IsNullOrWhiteSpace(this.appRoot)
                ? string.Empty
                : this.appRoot.TrimEnd('/') + '/',
            statefulServiceContext.PartitionId,
            statefulServiceContext.ReplicaId,
            Guid.NewGuid());
    }
    else if (this.serviceContext is StatelessServiceContext)
    {
        this.listeningAddress = string.Format(
            CultureInfo.InvariantCulture,
            "{0}://+:{1}/{2}",
            protocol,
            port,
            string.IsNullOrWhiteSpace(this.appRoot)
                ? string.Empty
                : this.appRoot.TrimEnd('/') + '/');
    }
    else
    {
        throw new InvalidOperationException();
    }

    ...

```

<span data-ttu-id="75b6f-199">請注意這裡用 "http://+"。</span><span class="sxs-lookup"><span data-stu-id="75b6f-199">Note that "http://+" is used here.</span></span> <span data-ttu-id="75b6f-200">這是為了確定 Web 伺服器正在接聽所有可用的位址，包括 localhost、FQDN，以及電腦的 IP。</span><span class="sxs-lookup"><span data-stu-id="75b6f-200">This is to make sure that the web server is listening on all available addresses, including localhost, FQDN, and the machine IP.</span></span>

<span data-ttu-id="75b6f-201">OpenAsync 實作是 Web 伺服器 (或任何通訊堆疊) 之所以實作為 ICommunicationListener，而非直接從服務中的 `RunAsync()` 開啟它，最重要的原因之一。</span><span class="sxs-lookup"><span data-stu-id="75b6f-201">The OpenAsync implementation is one of the most important reasons why the web server (or any communication stack) is implemented as an ICommunicationListener, rather than just having it open directly from `RunAsync()` in the service.</span></span> <span data-ttu-id="75b6f-202">OpenAsync 的傳回值是 Web 伺服器正在接聽的位址。</span><span class="sxs-lookup"><span data-stu-id="75b6f-202">The return value from OpenAsync is the address that the web server is listening on.</span></span> <span data-ttu-id="75b6f-203">當傳回這個位址給系統時，它會向服務註冊位址。</span><span class="sxs-lookup"><span data-stu-id="75b6f-203">When this address is returned to the system, it registers the address with the service.</span></span> <span data-ttu-id="75b6f-204">Service Fabric 會提供一個 API，讓用戶端和其他服務依服務名稱來要求這個位址。</span><span class="sxs-lookup"><span data-stu-id="75b6f-204">Service Fabric provides an API that allows clients and other services to then ask for this address by service name.</span></span> <span data-ttu-id="75b6f-205">這一點很重要，因為服務位址不是靜態的。</span><span class="sxs-lookup"><span data-stu-id="75b6f-205">This is important because the service address is not static.</span></span> <span data-ttu-id="75b6f-206">服務會為了資源平衡和可用性目的在叢集中移動。</span><span class="sxs-lookup"><span data-stu-id="75b6f-206">Services are moved around in the cluster for resource balancing and availability purposes.</span></span> <span data-ttu-id="75b6f-207">這是可讓用戶端解析服務接聽位址的機制。</span><span class="sxs-lookup"><span data-stu-id="75b6f-207">This is the mechanism that allows clients to resolve the listening address for a service.</span></span>

<span data-ttu-id="75b6f-208">記住這一點之後，OpenAsync 會啟動 Web 伺服器，並傳回它接聽的位址。</span><span class="sxs-lookup"><span data-stu-id="75b6f-208">With that in mind, OpenAsync starts the web server and returns the address that it's listening on.</span></span> <span data-ttu-id="75b6f-209">請注意它會接聽 "http://+"，但 OpenAsync 傳回位址之前，"+" 會取代為目前所在節點的 IP 或 FQDN。</span><span class="sxs-lookup"><span data-stu-id="75b6f-209">Note that it listens on "http://+", but before OpenAsync returns the address, the "+" is replaced with the IP or FQDN of the node it is currently on.</span></span> <span data-ttu-id="75b6f-210">這個方法所傳回的位址就是向系統註冊的位址。</span><span class="sxs-lookup"><span data-stu-id="75b6f-210">The address that is returned by this method is what's registered with the system.</span></span> <span data-ttu-id="75b6f-211">它也是用戶端和其他服務要求服務位址時所看到的位址。</span><span class="sxs-lookup"><span data-stu-id="75b6f-211">It's also what clients and other services see when they ask for a service's address.</span></span> <span data-ttu-id="75b6f-212">用戶端若要能正確地連接到它，它們需要位址中有實際的 IP 或 FQDN。</span><span class="sxs-lookup"><span data-stu-id="75b6f-212">For clients to correctly connect to it, they need an actual IP or FQDN in the address.</span></span>

```csharp
    ...

    this.publishAddress = this.listeningAddress.Replace("+", FabricRuntime.GetNodeContext().IPAddressOrFQDN);

    try
    {
        this.eventSource.Message("Starting web server on " + this.listeningAddress);

        this.webApp = WebApp.Start(this.listeningAddress, appBuilder => this.startup.Invoke(appBuilder));

        this.eventSource.Message("Listening on " + this.publishAddress);

        return Task.FromResult(this.publishAddress);
    }
    catch (Exception ex)
    {
        this.eventSource.Message("Web server failed to open endpoint {0}. {1}", this.endpointName, ex.ToString());

        this.StopWebServer();

        throw;
    }
}

```

<span data-ttu-id="75b6f-213">請注意，這會參考傳遞給建構函式中之 OwinCommunicationListener 的 Startup 類別。</span><span class="sxs-lookup"><span data-stu-id="75b6f-213">Note that this references the Startup class that was passed in to the OwinCommunicationListener in the constructor.</span></span> <span data-ttu-id="75b6f-214">這個 startup 執行個體由 Web 伺服器用來啟動 Web API 應用程式。</span><span class="sxs-lookup"><span data-stu-id="75b6f-214">This startup instance is used by the web server to bootstrap the Web API application.</span></span>

<span data-ttu-id="75b6f-215">稍後當您執行應用程式時， `ServiceEventSource.Current.Message()` 列會出現在 [診斷事件] 視窗，確認已成功啟動 Web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="75b6f-215">The `ServiceEventSource.Current.Message()` line will appear in the Diagnostic Events window later, when you run the application to confirm that the web server has started successfully.</span></span>

## <a name="implement-closeasync-and-abort"></a><span data-ttu-id="75b6f-216">實作 CloseAsync 和 Abort</span><span class="sxs-lookup"><span data-stu-id="75b6f-216">Implement CloseAsync and Abort</span></span>
<span data-ttu-id="75b6f-217">最後，實作 CloseAsync 和 Abort 可停止 Web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="75b6f-217">Finally, implement both CloseAsync and Abort to stop the web server.</span></span> <span data-ttu-id="75b6f-218">處置 OpenAsync 時所建立的伺服器控制代碼，可以停止 Web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="75b6f-218">The web server can be stopped by disposing the server handle that was created during OpenAsync.</span></span>

```csharp
public Task CloseAsync(CancellationToken cancellationToken)
{
    this.eventSource.Message("Closing web server on endpoint {0}", this.endpointName);

    this.StopWebServer();

    return Task.FromResult(true);
}

public void Abort()
{
    this.eventSource.Message("Aborting web server on endpoint {0}", this.endpointName);

    this.StopWebServer();
}

private void StopWebServer()
{
    if (this.webApp != null)
    {
        try
        {
            this.webApp.Dispose();
        }
        catch (ObjectDisposedException)
        {
            // no-op
        }
    }
}
```

<span data-ttu-id="75b6f-219">在此實作範例中，CloseAsync 和 Abort 只會停止 Web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="75b6f-219">In this implementation example, both CloseAsync and Abort simply stop the web server.</span></span> <span data-ttu-id="75b6f-220">您也可以選擇在 CloseAsync 中執行更妥善協調的 web 伺服器關閉。</span><span class="sxs-lookup"><span data-stu-id="75b6f-220">You may opt to perform a more gracefully coordinated shutdown of the web server in CloseAsync.</span></span> <span data-ttu-id="75b6f-221">例如，關閉可以等候進行中的要求，在傳回之前完成。</span><span class="sxs-lookup"><span data-stu-id="75b6f-221">For example, the shutdown could wait for in-flight requests to be completed before the return.</span></span>

## <a name="start-the-web-server"></a><span data-ttu-id="75b6f-222">啟動 Web 伺服器</span><span class="sxs-lookup"><span data-stu-id="75b6f-222">Start the web server</span></span>
<span data-ttu-id="75b6f-223">您現在可以開始建立並傳回 OwinCommunicationListener 的執行個體以啟動 Web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="75b6f-223">You're now ready to create and return an instance of OwinCommunicationListener to start the web server.</span></span> <span data-ttu-id="75b6f-224">回到 Service 類別 (WebService.cs)，覆寫 `CreateServiceInstanceListeners()` 方法：</span><span class="sxs-lookup"><span data-stu-id="75b6f-224">Back in the Service class (WebService.cs), override the `CreateServiceInstanceListeners()` method:</span></span>

```csharp
protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    var endpoints = Context.CodePackageActivationContext.GetEndpoints()
                           .Where(endpoint => endpoint.Protocol == EndpointProtocol.Http || endpoint.Protocol == EndpointProtocol.Https)
                           .Select(endpoint => endpoint.Name);

    return endpoints.Select(endpoint => new ServiceInstanceListener(
        serviceContext => new OwinCommunicationListener(Startup.ConfigureApp, serviceContext, ServiceEventSource.Current, endpoint), endpoint));
}
```

<span data-ttu-id="75b6f-225">這正是 Web API 應用程式和 OWIN 主機最後相會之處。</span><span class="sxs-lookup"><span data-stu-id="75b6f-225">This is where the Web API *application* and the OWIN *host* finally meet.</span></span> <span data-ttu-id="75b6f-226">透過 Startup 類別提供應用程式  的執行個體 (Web API) 給主機 (OwinCommunicationListener)。</span><span class="sxs-lookup"><span data-stu-id="75b6f-226">The host (OwinCommunicationListener) is given an instance of the *application* (Web API) via the Startup class.</span></span> <span data-ttu-id="75b6f-227">然後 Service Fabric 會管理其生命週期。</span><span class="sxs-lookup"><span data-stu-id="75b6f-227">Service Fabric then manages its lifecycle.</span></span> <span data-ttu-id="75b6f-228">通常可以針對任何通訊堆疊運用相同的模式。</span><span class="sxs-lookup"><span data-stu-id="75b6f-228">This same pattern can typically be followed with any communication stack.</span></span>

## <a name="put-it-all-together"></a><span data-ttu-id="75b6f-229">組合在一起</span><span class="sxs-lookup"><span data-stu-id="75b6f-229">Put it all together</span></span>
<span data-ttu-id="75b6f-230">在此範例中，您不需要在 `RunAsync()` 方法中執行任何動作，因此可以移除覆寫。</span><span class="sxs-lookup"><span data-stu-id="75b6f-230">In this example, you don't need to do anything in the `RunAsync()` method, so that override can simply be removed.</span></span>

<span data-ttu-id="75b6f-231">最終的服務實作應該非常簡單。</span><span class="sxs-lookup"><span data-stu-id="75b6f-231">The final service implementation should be very simple.</span></span> <span data-ttu-id="75b6f-232">它只需要建立通訊接聽程式：</span><span class="sxs-lookup"><span data-stu-id="75b6f-232">It only needs to create the communication listener:</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Fabric;
using System.Fabric.Description;
using System.Linq;
using Microsoft.ServiceFabric.Services.Communication.Runtime;
using Microsoft.ServiceFabric.Services.Runtime;

namespace WebService
{
    internal sealed class WebService : StatelessService
    {
        public WebService(StatelessServiceContext context)
            : base(context)
        { }

        protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
        {
            var endpoints = Context.CodePackageActivationContext.GetEndpoints()
                                   .Where(endpoint => endpoint.Protocol == EndpointProtocol.Http || endpoint.Protocol == EndpointProtocol.Https)
                                   .Select(endpoint => endpoint.Name);

            return endpoints.Select(endpoint => new ServiceInstanceListener(
                serviceContext => new OwinCommunicationListener(Startup.ConfigureApp, serviceContext, ServiceEventSource.Current, endpoint), endpoint));
        }
    }
}
```

<span data-ttu-id="75b6f-233">完整 `OwinCommunicationListener` 類別：</span><span class="sxs-lookup"><span data-stu-id="75b6f-233">The complete `OwinCommunicationListener` class:</span></span>

```csharp
using System;
using System.Diagnostics;
using System.Fabric;
using System.Globalization;
using System.Threading;
using System.Threading.Tasks;
using Microsoft.Owin.Hosting;
using Microsoft.ServiceFabric.Services.Communication.Runtime;
using Owin;

namespace WebService
{
    internal class OwinCommunicationListener : ICommunicationListener
    {
        private readonly ServiceEventSource eventSource;
        private readonly Action<IAppBuilder> startup;
        private readonly ServiceContext serviceContext;
        private readonly string endpointName;
        private readonly string appRoot;

        private IDisposable webApp;
        private string publishAddress;
        private string listeningAddress;

        public OwinCommunicationListener(Action<IAppBuilder> startup, ServiceContext serviceContext, ServiceEventSource eventSource, string endpointName)
            : this(startup, serviceContext, eventSource, endpointName, null)
        {
        }

        public OwinCommunicationListener(Action<IAppBuilder> startup, ServiceContext serviceContext, ServiceEventSource eventSource, string endpointName, string appRoot)
        {
            if (startup == null)
            {
                throw new ArgumentNullException(nameof(startup));
            }

            if (serviceContext == null)
            {
                throw new ArgumentNullException(nameof(serviceContext));
            }

            if (endpointName == null)
            {
                throw new ArgumentNullException(nameof(endpointName));
            }

            if (eventSource == null)
            {
                throw new ArgumentNullException(nameof(eventSource));
            }

            this.startup = startup;
            this.serviceContext = serviceContext;
            this.endpointName = endpointName;
            this.eventSource = eventSource;
            this.appRoot = appRoot;
        }

        public Task<string> OpenAsync(CancellationToken cancellationToken)
        {
            var serviceEndpoint = this.serviceContext.CodePackageActivationContext.GetEndpoint(this.endpointName);
            var protocol = serviceEndpoint.Protocol;
            int port = serviceEndpoint.Port;

            if (this.serviceContext is StatefulServiceContext)
            {
                StatefulServiceContext statefulServiceContext = this.serviceContext as StatefulServiceContext;

                this.listeningAddress = string.Format(
                    CultureInfo.InvariantCulture,
                    "{0}://+:{1}/{2}{3}/{4}/{5}",
                    protocol,
                    port,
                    string.IsNullOrWhiteSpace(this.appRoot)
                        ? string.Empty
                        : this.appRoot.TrimEnd('/') + '/',
                    statefulServiceContext.PartitionId,
                    statefulServiceContext.ReplicaId,
                    Guid.NewGuid());
            }
            else if (this.serviceContext is StatelessServiceContext)
            {
                this.listeningAddress = string.Format(
                    CultureInfo.InvariantCulture,
                    "{0}://+:{1}/{2}",
                    protocol,
                    port,
                    string.IsNullOrWhiteSpace(this.appRoot)
                        ? string.Empty
                        : this.appRoot.TrimEnd('/') + '/');
            }
            else
            {
                throw new InvalidOperationException();
            }

            this.publishAddress = this.listeningAddress.Replace("+", FabricRuntime.GetNodeContext().IPAddressOrFQDN);

            try
            {
                this.eventSource.Message("Starting web server on " + this.listeningAddress);

                this.webApp = WebApp.Start(this.listeningAddress, appBuilder => this.startup.Invoke(appBuilder));

                this.eventSource.Message("Listening on " + this.publishAddress);

                return Task.FromResult(this.publishAddress);
            }
            catch (Exception ex)
            {
                this.eventSource.Message("Web server failed to open endpoint {0}. {1}", this.endpointName, ex.ToString());

                this.StopWebServer();

                throw;
            }
        }

        public Task CloseAsync(CancellationToken cancellationToken)
        {
            this.eventSource.Message("Closing web server on endpoint {0}", this.endpointName);

            this.StopWebServer();

            return Task.FromResult(true);
        }

        public void Abort()
        {
            this.eventSource.Message("Aborting web server on endpoint {0}", this.endpointName);

            this.StopWebServer();
        }

        private void StopWebServer()
        {
            if (this.webApp != null)
            {
                try
                {
                    this.webApp.Dispose();
                }
                catch (ObjectDisposedException)
                {
                    // no-op
                }
            }
        }
    }
}
```

<span data-ttu-id="75b6f-234">所有細節就緒之後，您的專案看起來應該像一般 Web API 應用程式，並且具有 Reliable Services API 進入點與 OWIN 主機。</span><span class="sxs-lookup"><span data-stu-id="75b6f-234">Now that you have put all the pieces in place, your project should look like a typical Web API application with Reliable Services API entry points and an OWIN host.</span></span>

## <a name="run-and-connect-through-a-web-browser"></a><span data-ttu-id="75b6f-235">透過 Web 瀏覽器執行並連線</span><span class="sxs-lookup"><span data-stu-id="75b6f-235">Run and connect through a web browser</span></span>
<span data-ttu-id="75b6f-236">如果您尚未這麼做，請 [設定開發環境](service-fabric-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="75b6f-236">If you haven't done so, [set up your development environment](service-fabric-get-started.md).</span></span>

<span data-ttu-id="75b6f-237">您現在可以建置並部署您的服務。</span><span class="sxs-lookup"><span data-stu-id="75b6f-237">You can now build and deploy your service.</span></span> <span data-ttu-id="75b6f-238">在 Visual Studio 中按 **F5** 以建置及部署應用程式。</span><span class="sxs-lookup"><span data-stu-id="75b6f-238">Press **F5** in Visual Studio to build and deploy the application.</span></span> <span data-ttu-id="75b6f-239">在 [診斷事件] 視窗中，您應該會看到一則訊息指出 Web 伺服器在 http://localhost:8281/ 中開啟。</span><span class="sxs-lookup"><span data-stu-id="75b6f-239">In the Diagnostic Events window, you should see a message that indicates that the web server opened on http://localhost:8281/.</span></span>

> [!NOTE]
> <span data-ttu-id="75b6f-240">如果電腦上的另一個處理序已經開啟連接埠，您可能會在此看到錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="75b6f-240">If the port has already been opened by another process on your machine, you may see an error here.</span></span> <span data-ttu-id="75b6f-241">這就表示無法開啟接聽程式。</span><span class="sxs-lookup"><span data-stu-id="75b6f-241">This indicates that the listener couldn't be opened.</span></span> <span data-ttu-id="75b6f-242">如果是這種情況，請嘗試在 ServiceManifest.xml 中的端點組態使用不同的通訊埠。</span><span class="sxs-lookup"><span data-stu-id="75b6f-242">If that's the case, try using a different port for the endpoint configuration in ServiceManifest.xml.</span></span>
> 
> 

<span data-ttu-id="75b6f-243">一旦服務正常執行，請開啟瀏覽器並瀏覽至 [http://localhost:8281/api/values](http://localhost:8281/api/values) 進行測試。</span><span class="sxs-lookup"><span data-stu-id="75b6f-243">Once the service is running, open a browser and navigate to [http://localhost:8281/api/values](http://localhost:8281/api/values) to test it.</span></span>

## <a name="scale-it-out"></a><span data-ttu-id="75b6f-244">相應放大</span><span class="sxs-lookup"><span data-stu-id="75b6f-244">Scale it out</span></span>
<span data-ttu-id="75b6f-245">相應放大無狀態的 Web 應用程式通常表示加入更多電腦，並加快其上的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="75b6f-245">Scaling out stateless web apps typically means adding more machines and spinning up the web apps on them.</span></span> <span data-ttu-id="75b6f-246">每當新的節點加入至叢集時，Service Fabric 的協調流程引擎便可以為您完成。</span><span class="sxs-lookup"><span data-stu-id="75b6f-246">Service Fabric's orchestration engine can do this for you whenever new nodes are added to a cluster.</span></span> <span data-ttu-id="75b6f-247">當您建立無狀態服務的執行個體時，您可以指定要建立的執行個體數目。</span><span class="sxs-lookup"><span data-stu-id="75b6f-247">When you create instances of a stateless service, you can specify the number of instances you want to create.</span></span> <span data-ttu-id="75b6f-248">Service Fabric 會在叢集中放置執行個體的數目在節點上。</span><span class="sxs-lookup"><span data-stu-id="75b6f-248">Service Fabric places that number of instances on nodes in the cluster.</span></span> <span data-ttu-id="75b6f-249">它可確保所有節點上都只會建立一個執行個體。</span><span class="sxs-lookup"><span data-stu-id="75b6f-249">And it makes sure not to create more than one instance on any one node.</span></span> <span data-ttu-id="75b6f-250">您也可以指定 **-1** 的執行個體計數，指示 Service Fabric 一律在每個節點上建立執行個體。</span><span class="sxs-lookup"><span data-stu-id="75b6f-250">You can also instruct Service Fabric to always create an instance on every node by specifying **-1** for the instance count.</span></span> <span data-ttu-id="75b6f-251">這樣可保證每當您加入節點相應放大您的叢集，便會在新節點上建立無狀態服務的執行個體。</span><span class="sxs-lookup"><span data-stu-id="75b6f-251">This guarantees that whenever you add nodes to scale out your cluster, an instance of your stateless service will be created on the new nodes.</span></span> <span data-ttu-id="75b6f-252">這個值是服務執行個體的屬性，因此它會在您建立服務執行個體時設定：</span><span class="sxs-lookup"><span data-stu-id="75b6f-252">This value is a property of the service instance, so it is set when you create a service instance.</span></span> <span data-ttu-id="75b6f-253">您可以透過 PowerShell 設定：</span><span class="sxs-lookup"><span data-stu-id="75b6f-253">You can do this through PowerShell:</span></span>

```powershell

New-ServiceFabricService -ApplicationName "fabric:/WebServiceApplication" -ServiceName "fabric:/WebServiceApplication/WebService" -ServiceTypeName "WebServiceType" -Stateless -PartitionSchemeSingleton -InstanceCount -1

```

<span data-ttu-id="75b6f-254">您也可以在 Visual Studio 無狀態服務專案中定義預設服務時設定：</span><span class="sxs-lookup"><span data-stu-id="75b6f-254">You can also do this when you define a default service in a Visual Studio stateless service project:</span></span>

```xml

<DefaultServices>
  <Service Name="WebService">
    <StatelessService ServiceTypeName="WebServiceType" InstanceCount="-1">
      <SingletonPartition />
    </StatelessService>
  </Service>
</DefaultServices>

```

<span data-ttu-id="75b6f-255">如需如何建立應用程式和服務執行個體的詳細資訊，請參閱 [部署應用程式](service-fabric-deploy-remove-applications.md)。</span><span class="sxs-lookup"><span data-stu-id="75b6f-255">For more information on how to create application and service instances, see [Deploy an application](service-fabric-deploy-remove-applications.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="75b6f-256">後續步驟</span><span class="sxs-lookup"><span data-stu-id="75b6f-256">Next steps</span></span>
[<span data-ttu-id="75b6f-257">使用 Visual Studio 偵錯 Service Fabric 應用程式</span><span class="sxs-lookup"><span data-stu-id="75b6f-257">Debug your Service Fabric application by using Visual Studio</span></span>](service-fabric-debugging-your-application.md)

