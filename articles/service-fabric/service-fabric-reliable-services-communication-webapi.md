---
title: "以 ASP.NET Web API hello aaaService 通訊 |Microsoft 文件"
description: "了解如何逐步使用 tooimplement 服務通訊 hello 與 OWIN 自我主控 hello 可靠的服務應用程式開發介面中的 ASP.NET Web API。"
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
ms.openlocfilehash: 3fb18fcb141ada0d79a0acda3dccbc7fb044346d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-service-fabric-web-api-services-with-owin-self-hosting"></a><span data-ttu-id="5f693-103">開始使用：Service Fabric Web API 服務與 OWIN 自我裝載 | Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="5f693-103">Get started: Service Fabric Web API services with OWIN self-hosting</span></span>
<span data-ttu-id="5f693-104">Azure Service Fabric 置於 hello 電源雙手當您決定要服務 toocommunicate，使用者與彼此。</span><span class="sxs-lookup"><span data-stu-id="5f693-104">Azure Service Fabric puts hello power in your hands when you're deciding how you want your services toocommunicate with users and with each other.</span></span> <span data-ttu-id="5f693-105">本教學課程著重於使用 ASP.NET Web API 與 Open Web Interface for .NET (OWIN) 自我裝載在 Service Fabric 的 Reliable Services API 中實作服務通訊。</span><span class="sxs-lookup"><span data-stu-id="5f693-105">This tutorial focuses on implementing service communication using ASP.NET Web API with Open Web Interface for .NET (OWIN) self-hosting in Service Fabric's Reliable Services API.</span></span> <span data-ttu-id="5f693-106">我們將深入探討深 hello 可靠的服務可插式通訊應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="5f693-106">We'll delve deeply into hello Reliable Services pluggable communication API.</span></span> <span data-ttu-id="5f693-107">我們也會使用 Web 應用程式開發介面中的逐步範例 tooshow 您如何 tooset 註冊自訂通訊接聽程式。</span><span class="sxs-lookup"><span data-stu-id="5f693-107">We'll also use Web API in a step-by-step example tooshow you how tooset up a custom communication listener.</span></span>

## <a name="introduction-tooweb-api-in-service-fabric"></a><span data-ttu-id="5f693-108">服務網狀架構的簡介 tooWeb 應用程式開發介面</span><span class="sxs-lookup"><span data-stu-id="5f693-108">Introduction tooWeb API in Service Fabric</span></span>
<span data-ttu-id="5f693-109">ASP.NET Web API 是建立 HTTP Api 之上 hello.NET Framework 受歡迎且功能強大的架構。</span><span class="sxs-lookup"><span data-stu-id="5f693-109">ASP.NET Web API is a popular and powerful framework for building HTTP APIs on top of hello .NET Framework.</span></span> <span data-ttu-id="5f693-110">如果您不熟悉 hello framework，請參閱[開始使用 ASP.NET Web API 2](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api) toolearn 更多。</span><span class="sxs-lookup"><span data-stu-id="5f693-110">If you're not already familiar with hello framework, see [Getting started with ASP.NET Web API 2](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api) toolearn more.</span></span>

<span data-ttu-id="5f693-111">服務網狀架構中的 web 應用程式開發介面是 hello 相同 ASP.NET Web API，您熟悉且愛用。</span><span class="sxs-lookup"><span data-stu-id="5f693-111">Web API in Service Fabric is hello same ASP.NET Web API you know and love.</span></span> <span data-ttu-id="5f693-112">hello 其間的差異在於如何您*主機*Web API 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5f693-112">hello difference is in how you *host* a Web API application.</span></span> <span data-ttu-id="5f693-113">您不會使用 Microsoft Internet Information Services (IIS)。</span><span class="sxs-lookup"><span data-stu-id="5f693-113">You won't be using Microsoft Internet Information Services (IIS).</span></span> <span data-ttu-id="5f693-114">toobetter 瞭解 hello 差異，我們將其分成兩個部分：</span><span class="sxs-lookup"><span data-stu-id="5f693-114">toobetter understand hello difference, let's break it into two parts:</span></span>

1. <span data-ttu-id="5f693-115">hello Web API 應用程式 （包括控制站和模型）</span><span class="sxs-lookup"><span data-stu-id="5f693-115">hello Web API application (including controllers and models)</span></span>
2. <span data-ttu-id="5f693-116">hello 主機 （hello web 伺服器，通常是 IIS）</span><span class="sxs-lookup"><span data-stu-id="5f693-116">hello host (hello web server, usually IIS)</span></span>

<span data-ttu-id="5f693-117">Web API 應用程式本身不會變更。</span><span class="sxs-lookup"><span data-stu-id="5f693-117">A Web API application itself doesn't change.</span></span> <span data-ttu-id="5f693-118">它並無不同 hello 過去，您可能會寫入 Web API 應用程式和大部分的應用程式程式碼應能 toosimply 移動。</span><span class="sxs-lookup"><span data-stu-id="5f693-118">It's no different from Web API applications you may have written in hello past, and you should be able toosimply move over most of your application code.</span></span> <span data-ttu-id="5f693-119">但如果您已經已裝載於 IIS，您用來裝載 hello 應用程式可能會稍有不同於您所用的。</span><span class="sxs-lookup"><span data-stu-id="5f693-119">But if you've been hosting on IIS, where you host hello application may be a little different from what you're used to.</span></span> <span data-ttu-id="5f693-120">我們取得 toohello 裝載部分之前，讓我們先開始項目比較熟悉： hello Web API 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5f693-120">Before we get toohello hosting part, let's start with something more familiar: hello Web API application.</span></span>

## <a name="create-hello-application"></a><span data-ttu-id="5f693-121">建立 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="5f693-121">Create hello application</span></span>
<span data-ttu-id="5f693-122">若要開始，請在 Visual Studio 2015 中，建立具有單一無狀態服務的新 Service Fabric 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5f693-122">Start by creating a new Service Fabric application with a single stateless service in Visual Studio 2015.</span></span>

<span data-ttu-id="5f693-123">使用 Web 應用程式開發介面的無狀態服務的 Visual Studio 範本是可用 tooyou。</span><span class="sxs-lookup"><span data-stu-id="5f693-123">A Visual Studio template for a stateless service using Web API is available tooyou.</span></span> <span data-ttu-id="5f693-124">在本教學課程中，我們將從頭建置 Web API 專案，這就是您選取此範本時所會得到的結果。</span><span class="sxs-lookup"><span data-stu-id="5f693-124">In this tutorial, we'll build a Web API project from scratch that results in what you'd get if you selected this template.</span></span>

<span data-ttu-id="5f693-125">選取空白無狀態服務專案 toolearn 如何 hello 無狀態服務 Web API 範本的開頭和只沿用 toobuild 從頭開始，或您的 Web API 專案。</span><span class="sxs-lookup"><span data-stu-id="5f693-125">Select a blank Stateless Service project toolearn how toobuild a Web API project from scratch, or you can start with hello stateless service Web API template and simply follow along.</span></span>  

<span data-ttu-id="5f693-126">hello 第一個步驟是 toopull Web API 的某些 NuGet 封裝中。</span><span class="sxs-lookup"><span data-stu-id="5f693-126">hello first step is toopull in some NuGet packages for Web API.</span></span> <span data-ttu-id="5f693-127">我們希望 toouse hello 封裝是 Microsoft.AspNet.WebApi.OwinSelfHost。</span><span class="sxs-lookup"><span data-stu-id="5f693-127">hello package we want toouse is Microsoft.AspNet.WebApi.OwinSelfHost.</span></span> <span data-ttu-id="5f693-128">此套件包含所有 hello 必要的 Web 應用程式開發介面封裝以及 hello*主機*封裝。</span><span class="sxs-lookup"><span data-stu-id="5f693-128">This package includes all hello necessary Web API packages and hello *host* packages.</span></span> <span data-ttu-id="5f693-129">這在稍後會很重要。</span><span class="sxs-lookup"><span data-stu-id="5f693-129">This will be important later.</span></span>

<span data-ttu-id="5f693-130">已安裝 hello 封裝之後，您可以開始建置出 hello 基本 Web API 專案結構。</span><span class="sxs-lookup"><span data-stu-id="5f693-130">After hello packages have been installed, you can begin building out hello basic Web API project structure.</span></span> <span data-ttu-id="5f693-131">如果您已使用 Web 應用程式開發介面，hello 專案結構應該看起來很類似。</span><span class="sxs-lookup"><span data-stu-id="5f693-131">If you've used Web API, hello project structure should look very familiar.</span></span> <span data-ttu-id="5f693-132">首先新增 `Controllers` 目錄和簡單值控制站︰</span><span class="sxs-lookup"><span data-stu-id="5f693-132">Start by adding a `Controllers` directory and a simple values controller:</span></span>

<span data-ttu-id="5f693-133">**ValuesController.cs**</span><span class="sxs-lookup"><span data-stu-id="5f693-133">**ValuesController.cs**</span></span>

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

<span data-ttu-id="5f693-134">接下來，新增啟動類別在 hello 專案根 tooregister hello 路由、 格式器及任何其他組態設定。</span><span class="sxs-lookup"><span data-stu-id="5f693-134">Next, add a Startup class at hello project root tooregister hello routing, formatters, and any other configuration setup.</span></span> <span data-ttu-id="5f693-135">這也是 Web 應用程式開發介面其中插入 toohello*主機*，這將可再次回到稍後。</span><span class="sxs-lookup"><span data-stu-id="5f693-135">This is also where Web API plugs in toohello *host*, which will be revisited again later.</span></span> 

<span data-ttu-id="5f693-136">**Startup.cs**</span><span class="sxs-lookup"><span data-stu-id="5f693-136">**Startup.cs**</span></span>

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

<span data-ttu-id="5f693-137">這是 hello 應用程式組件。</span><span class="sxs-lookup"><span data-stu-id="5f693-137">That's it for hello application part.</span></span> <span data-ttu-id="5f693-138">此時，我們設定只 hello 基本 Web API 專案版面配置。</span><span class="sxs-lookup"><span data-stu-id="5f693-138">At this point, we've set up just hello basic Web API project layout.</span></span> <span data-ttu-id="5f693-139">目前為止，它不應該看起來非常不同，從 Web API 專案，您可能會寫入 hello 過去或 hello 基本 Web API 範本。</span><span class="sxs-lookup"><span data-stu-id="5f693-139">So far, it shouldn't look much different from Web API projects you may have written in hello past or from hello basic Web API template.</span></span> <span data-ttu-id="5f693-140">您的商務邏輯則是放在 hello 控制站和模型像往常一樣。</span><span class="sxs-lookup"><span data-stu-id="5f693-140">Your business logic goes in hello controllers and models as usual.</span></span>

<span data-ttu-id="5f693-141">現在我們怎麼辦才能實際執行裝載？</span><span class="sxs-lookup"><span data-stu-id="5f693-141">Now what do we do about hosting so that we can actually run it?</span></span>

## <a name="service-hosting"></a><span data-ttu-id="5f693-142">服務裝載</span><span class="sxs-lookup"><span data-stu-id="5f693-142">Service hosting</span></span>
<span data-ttu-id="5f693-143">在 Service Fabric 中，您的服務會在服務主機處理序 中執行，這是執行您的服務程式碼的可執行檔。</span><span class="sxs-lookup"><span data-stu-id="5f693-143">In Service Fabric, your service runs in a *service host process*, an executable file that runs your service code.</span></span> <span data-ttu-id="5f693-144">當您使用 hello 可靠的服務應用程式開發介面撰寫的服務時，您的服務專案只會編譯 tooan 可執行檔，註冊您的服務類型，並執行您的程式碼。</span><span class="sxs-lookup"><span data-stu-id="5f693-144">When you write a service by using hello Reliable Services API, your service project just compiles tooan executable file that registers your service type and runs your code.</span></span> <span data-ttu-id="5f693-145">當您在 .NET 中的 Service Fabric 上撰寫服務時，在大部分情況下都是如此。</span><span class="sxs-lookup"><span data-stu-id="5f693-145">This is true in most cases when you write a service on Service Fabric in .NET.</span></span> <span data-ttu-id="5f693-146">當您開啟 Program.cs hello 無狀態服務專案中時，您應該會看到：</span><span class="sxs-lookup"><span data-stu-id="5f693-146">When you open Program.cs in hello stateless service project, you should see:</span></span>

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

<span data-ttu-id="5f693-147">如果這看起來可疑像是 hello 進入點 tooa 主控台應用程式，這是因為它是。</span><span class="sxs-lookup"><span data-stu-id="5f693-147">If that looks suspiciously like hello entry point tooa console application, that's because it is.</span></span>

<span data-ttu-id="5f693-148">進一步詳細 hello 服務主機處理序與服務登錄已超出本文的 hello 範圍。</span><span class="sxs-lookup"><span data-stu-id="5f693-148">Further details about hello service host process and service registration are beyond hello scope of this article.</span></span> <span data-ttu-id="5f693-149">但它是用於重要 tooknow 現在*自己的處理序中執行您的服務程式碼*。</span><span class="sxs-lookup"><span data-stu-id="5f693-149">But it's important tooknow for now that *your service code is running in its own process*.</span></span>

## <a name="self-host-web-api-with-an-owin-host"></a><span data-ttu-id="5f693-150">自我裝載 Web API 與 OWIN 主機</span><span class="sxs-lookup"><span data-stu-id="5f693-150">Self-host Web API with an OWIN host</span></span>
<span data-ttu-id="5f693-151">假設您的 Web API 應用程式程式碼裝載在自己的處理序，如何具 tooa web 伺服器？</span><span class="sxs-lookup"><span data-stu-id="5f693-151">Given that your Web API application code is hosted in its own process, how do you hook it up tooa web server?</span></span> <span data-ttu-id="5f693-152">輸入 [OWIN](http://owin.org/)。</span><span class="sxs-lookup"><span data-stu-id="5f693-152">Enter [OWIN](http://owin.org/).</span></span> <span data-ttu-id="5f693-153">OWIN 只是 .NET Web 應用程式和 Web 伺服器之間的合約。</span><span class="sxs-lookup"><span data-stu-id="5f693-153">OWIN is simply a contract between .NET web applications and web servers.</span></span> <span data-ttu-id="5f693-154">傳統上使用 ASP.NET （向上 tooMVC 5) 時，hello web 應用程式是透過 System.Web 緊密結合的 tooIIS。</span><span class="sxs-lookup"><span data-stu-id="5f693-154">Traditionally when ASP.NET (up tooMVC 5) is used, hello web application is tightly coupled tooIIS through System.Web.</span></span> <span data-ttu-id="5f693-155">不過，Web 應用程式開發介面會實作 OWIN，所以您可以撰寫分離 web 應用程式，從它裝載的 hello web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="5f693-155">However, Web API implements OWIN, so you can write a web application that is decoupled from hello web server that hosts it.</span></span> <span data-ttu-id="5f693-156">因此，您可以使用可在自己的程序中啟動的自我裝載  OWIN web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="5f693-156">Because of this, you can use a *self-hosted* OWIN web server that you can start in your own process.</span></span> <span data-ttu-id="5f693-157">這完全符合我們剛說明 hello Service Fabric 裝載模型。</span><span class="sxs-lookup"><span data-stu-id="5f693-157">This fits perfectly with hello Service Fabric hosting model we just described.</span></span>

<span data-ttu-id="5f693-158">在本文中，我們會使用為 hello OWIN 主機 Katana hello Web API 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5f693-158">In this article, we'll use Katana as hello OWIN host for hello Web API application.</span></span> <span data-ttu-id="5f693-159">Katana 是根據開放原始碼 OWIN 主機實作[System.Net.HttpListener](https://msdn.microsoft.com/library/system.net.httplistener.aspx)和 hello Windows [HTTP 伺服器 API](https://msdn.microsoft.com/library/windows/desktop/aa364510.aspx)。</span><span class="sxs-lookup"><span data-stu-id="5f693-159">Katana is an open-source OWIN host implementation built on [System.Net.HttpListener](https://msdn.microsoft.com/library/system.net.httplistener.aspx) and hello Windows [HTTP Server API](https://msdn.microsoft.com/library/windows/desktop/aa364510.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="5f693-160">深入了解 Katana，移 toohello toolearn [Katana 網站](http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana)。</span><span class="sxs-lookup"><span data-stu-id="5f693-160">toolearn more about Katana, go toohello [Katana site](http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana).</span></span> <span data-ttu-id="5f693-161">如需快速概觀 toouse Katana tooself 主機 Web API，請參閱[使用 OWIN tooSelf 主機 ASP.NET Web API 2](http://www.asp.net/web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api)。</span><span class="sxs-lookup"><span data-stu-id="5f693-161">For a quick overview of how toouse Katana tooself-host Web API, see [Use OWIN tooSelf-Host ASP.NET Web API 2](http://www.asp.net/web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api).</span></span>
> 
> 

## <a name="set-up-hello-web-server"></a><span data-ttu-id="5f693-162">設定 hello 網頁伺服器</span><span class="sxs-lookup"><span data-stu-id="5f693-162">Set up hello web server</span></span>
<span data-ttu-id="5f693-163">hello 可靠的服務應用程式開發介面提供，以便讓使用者和用戶端 tooconnect toohello 服務的通訊堆疊中插入通訊進入點：</span><span class="sxs-lookup"><span data-stu-id="5f693-163">hello Reliable Services API provides a communication entry point where you can plug in communication stacks that allow users and clients tooconnect toohello service:</span></span>

```csharp

protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    ...
}

```

<span data-ttu-id="5f693-164">hello 網頁伺服器 （和任何其他通訊堆疊，您用於未來的例如 WebSockets hello） 應該使用 hello ICommunicationListener 介面 toointegrate 正確 hello 系統。</span><span class="sxs-lookup"><span data-stu-id="5f693-164">hello web server (and any other communication stack you use in hello future, such as WebSockets) should use hello ICommunicationListener interface toointegrate correctly with hello system.</span></span> <span data-ttu-id="5f693-165">這個 hello 原因將會變得更加明顯 hello 步驟中的。</span><span class="sxs-lookup"><span data-stu-id="5f693-165">hello reasons for this will become more apparent in hello following steps.</span></span>

<span data-ttu-id="5f693-166">首先，建立一個稱為 OwinCommunicationListener 的類別，其實作 ICommunicationListener：</span><span class="sxs-lookup"><span data-stu-id="5f693-166">First, create a class called OwinCommunicationListener that implements ICommunicationListener:</span></span>

<span data-ttu-id="5f693-167">**OwinCommunicationListener.cs：**</span><span class="sxs-lookup"><span data-stu-id="5f693-167">**OwinCommunicationListener.cs**</span></span>

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

<span data-ttu-id="5f693-168">hello ICommunicationListener 介面提供三個方法 toomanage 通訊接聽程式為您的服務：</span><span class="sxs-lookup"><span data-stu-id="5f693-168">hello ICommunicationListener interface provides three methods toomanage a communication listener for your service:</span></span>

* <span data-ttu-id="5f693-169">。</span><span class="sxs-lookup"><span data-stu-id="5f693-169">*OpenAsync*.</span></span> <span data-ttu-id="5f693-170">開始接聽要求。</span><span class="sxs-lookup"><span data-stu-id="5f693-170">Start listening for requests.</span></span>
* <span data-ttu-id="5f693-171">。</span><span class="sxs-lookup"><span data-stu-id="5f693-171">*CloseAsync*.</span></span> <span data-ttu-id="5f693-172">停止接聽要求，完成任何進行中的要求，並正常關機。</span><span class="sxs-lookup"><span data-stu-id="5f693-172">Stop listening for requests, finish any in-flight requests, and shut down gracefully.</span></span>
* <span data-ttu-id="5f693-173">中止。</span><span class="sxs-lookup"><span data-stu-id="5f693-173">*Abort*.</span></span> <span data-ttu-id="5f693-174">取消所有項目，並立即停止。</span><span class="sxs-lookup"><span data-stu-id="5f693-174">Cancel everything and stop immediately.</span></span>

<span data-ttu-id="5f693-175">項目 hello 接聽程式將會需要 toofunction tooget 啟動，加入私用類別成員。</span><span class="sxs-lookup"><span data-stu-id="5f693-175">tooget started, add private class members for things hello listener will need toofunction.</span></span> <span data-ttu-id="5f693-176">這些會初始化透過 hello 建構函式，並稍後使用，當您設定 hello 接聽的 URL。</span><span class="sxs-lookup"><span data-stu-id="5f693-176">These will be initialized through hello constructor and used later when you set up hello listening URL.</span></span>

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

## <a name="implement-openasync"></a><span data-ttu-id="5f693-177">實作 OpenAsync</span><span class="sxs-lookup"><span data-stu-id="5f693-177">Implement OpenAsync</span></span>
<span data-ttu-id="5f693-178">tooset hello web 伺服器，您需要兩個資訊片段：</span><span class="sxs-lookup"><span data-stu-id="5f693-178">tooset up hello web server, you need two pieces of information:</span></span>

* <span data-ttu-id="5f693-179">*URL 路徑前置詞*。</span><span class="sxs-lookup"><span data-stu-id="5f693-179">*A URL path prefix*.</span></span> <span data-ttu-id="5f693-180">雖然這是選擇性的它是適合您 tooset 這個向上現在，讓您安全地可以裝載多個 web 服務應用程式中。</span><span class="sxs-lookup"><span data-stu-id="5f693-180">Although this is optional, it's good for you tooset this up now so that you can safely host multiple web services in your application.</span></span>
* <span data-ttu-id="5f693-181">*連接埠*。</span><span class="sxs-lookup"><span data-stu-id="5f693-181">*A port*.</span></span>

<span data-ttu-id="5f693-182">取得 hello web 伺服器的連接埠之前，重要的是您了解 Service Fabric 提供應用程式層級，可做為您的應用程式與 hello 基礎作業系統上執行之間的緩衝區。</span><span class="sxs-lookup"><span data-stu-id="5f693-182">Before you get a port for hello web server, it's important that you understand that Service Fabric provides an application layer that acts as a buffer between your application and hello underlying operating system that it runs on.</span></span> <span data-ttu-id="5f693-183">因此，Service Fabric 提供方式 tooconfigure*端點*為您的服務。</span><span class="sxs-lookup"><span data-stu-id="5f693-183">As such, Service Fabric provides a way tooconfigure *endpoints* for your services.</span></span> <span data-ttu-id="5f693-184">Service Fabric 可確保端點可供服務 toouse。</span><span class="sxs-lookup"><span data-stu-id="5f693-184">Service Fabric ensures that endpoints are available for your service toouse.</span></span> <span data-ttu-id="5f693-185">如此一來，您不需要 tooconfigure 它們自己 hello 基礎作業系統環境中。</span><span class="sxs-lookup"><span data-stu-id="5f693-185">This way, you don't have tooconfigure them yourself in hello underlying OS environment.</span></span> <span data-ttu-id="5f693-186">您輕鬆地可以主控 Service Fabric 應用程式中不同的環境，而不需要 toomake 任何變更 tooyour 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5f693-186">You can easily host your Service Fabric application in different environments without having toomake any changes tooyour application.</span></span> <span data-ttu-id="5f693-187">(例如，您也可以裝載 hello 自己的資料中心或 Azure 中相同的應用程式。)</span><span class="sxs-lookup"><span data-stu-id="5f693-187">(For example, you can host hello same application in Azure or in your own datacenter.)</span></span>

<span data-ttu-id="5f693-188">在 PackageRoot\ServiceManifest.xml 中設定 HTTP 端點：</span><span class="sxs-lookup"><span data-stu-id="5f693-188">Configure an HTTP endpoint in PackageRoot\ServiceManifest.xml:</span></span>

```xml
<Resources>
    <Endpoints>
        <Endpoint Name="ServiceEndpoint" Type="Input" Protocol="http" Port="8281" />
    </Endpoints>
</Resources>

```

<span data-ttu-id="5f693-189">這個步驟很重要，因為受限制的認證 （Windows 上的網路服務） 下執行 hello 服務主機處理序。</span><span class="sxs-lookup"><span data-stu-id="5f693-189">This step is important because hello service host process runs under restricted credentials (Network Service on Windows).</span></span> <span data-ttu-id="5f693-190">這表示您的服務將不會有存取 tooset HTTP 端點，其本身。</span><span class="sxs-lookup"><span data-stu-id="5f693-190">This means that your service won't have access tooset up an HTTP endpoint on its own.</span></span> <span data-ttu-id="5f693-191">藉由使用 hello 端點組態，Service Fabric 會知道 hello 服務的 URL 會接聽 tooset hello 適當的存取控制清單 (ACL)。</span><span class="sxs-lookup"><span data-stu-id="5f693-191">By using hello endpoint configuration, Service Fabric knows tooset up hello proper access control list (ACL) for hello URL that hello service will listen on.</span></span> <span data-ttu-id="5f693-192">服務網狀架構也提供標準位置 tooconfigure 端點。</span><span class="sxs-lookup"><span data-stu-id="5f693-192">Service Fabric also provides a standard place tooconfigure endpoints.</span></span>

<span data-ttu-id="5f693-193">返回 OwinCommunicationListener.cs 中，您可以開始實作 OpenAsync。</span><span class="sxs-lookup"><span data-stu-id="5f693-193">Back in OwinCommunicationListener.cs, you can start implementing OpenAsync.</span></span> <span data-ttu-id="5f693-194">這是您用來啟動 hello web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="5f693-194">This is where you start hello web server.</span></span> <span data-ttu-id="5f693-195">首先，取得 hello 端點資訊，並建立 hello hello 服務將接聽的 URL。</span><span class="sxs-lookup"><span data-stu-id="5f693-195">First, get hello endpoint information and create hello URL that hello service will listen on.</span></span> <span data-ttu-id="5f693-196">hello URL 將是 hello 接聽程式是否使用中的無狀態的服務或可設定狀態的服務而有所不同。</span><span class="sxs-lookup"><span data-stu-id="5f693-196">hello URL will be different depending on whether hello listener is used in a stateless service or a stateful service.</span></span> <span data-ttu-id="5f693-197">可設定狀態的服務，hello 接聽程式需要唯一的每一個可設定狀態的服務複本它會接聽在位址的 toocreate。</span><span class="sxs-lookup"><span data-stu-id="5f693-197">For a stateful service, hello listener needs toocreate a unique address for every stateful service replica it listens on.</span></span> <span data-ttu-id="5f693-198">針對無狀態服務，hello 位址可以是簡單許多。</span><span class="sxs-lookup"><span data-stu-id="5f693-198">For stateless services, hello address can be much simpler.</span></span> 

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

<span data-ttu-id="5f693-199">請注意這裡用 "http://+"。</span><span class="sxs-lookup"><span data-stu-id="5f693-199">Note that "http://+" is used here.</span></span> <span data-ttu-id="5f693-200">這是 toomake 確定該 hello 網頁伺服器正在接聽所有可用的位址，包括 localhost、 FQDN 和 hello 機器的 IP。</span><span class="sxs-lookup"><span data-stu-id="5f693-200">This is toomake sure that hello web server is listening on all available addresses, including localhost, FQDN, and hello machine IP.</span></span>

<span data-ttu-id="5f693-201">hello OpenAsync 實作是 hello 最重要原因之一為什麼 hello 網頁伺服器 （或任何通訊堆疊） 實作直接從 ICommunicationListener，而不是只將它開啟`RunAsync()`hello 服務中。</span><span class="sxs-lookup"><span data-stu-id="5f693-201">hello OpenAsync implementation is one of hello most important reasons why hello web server (or any communication stack) is implemented as an ICommunicationListener, rather than just having it open directly from `RunAsync()` in hello service.</span></span> <span data-ttu-id="5f693-202">hello OpenAsync 傳回值是 hello hello web 伺服器的位址接聽。</span><span class="sxs-lookup"><span data-stu-id="5f693-202">hello return value from OpenAsync is hello address that hello web server is listening on.</span></span> <span data-ttu-id="5f693-203">這個地址傳回 toohello 系統時，它會向 hello 服務註冊 hello 位址。</span><span class="sxs-lookup"><span data-stu-id="5f693-203">When this address is returned toohello system, it registers hello address with hello service.</span></span> <span data-ttu-id="5f693-204">Service Fabric 提供 API，可讓用戶端和其他服務 toothen，已要求此位址的服務名稱。</span><span class="sxs-lookup"><span data-stu-id="5f693-204">Service Fabric provides an API that allows clients and other services toothen ask for this address by service name.</span></span> <span data-ttu-id="5f693-205">這是很重要，因為 hello 服務位址不是靜態。</span><span class="sxs-lookup"><span data-stu-id="5f693-205">This is important because hello service address is not static.</span></span> <span data-ttu-id="5f693-206">服務會移動 hello 叢集中進行資源平衡和可用性。</span><span class="sxs-lookup"><span data-stu-id="5f693-206">Services are moved around in hello cluster for resource balancing and availability purposes.</span></span> <span data-ttu-id="5f693-207">這是 hello 機制，可讓用戶端 tooresolve hello 接聽服務位址。</span><span class="sxs-lookup"><span data-stu-id="5f693-207">This is hello mechanism that allows clients tooresolve hello listening address for a service.</span></span>

<span data-ttu-id="5f693-208">這一點，OpenAsync 啟動 hello web 伺服器，並傳回 hello 位址上接聽。</span><span class="sxs-lookup"><span data-stu-id="5f693-208">With that in mind, OpenAsync starts hello web server and returns hello address that it's listening on.</span></span> <span data-ttu-id="5f693-209">請注意，它會接聽"http://+"，但 OpenAsync 傳回 hello 位址之前，hello"+"會取代 hello IP 或 FQDN，目前在 hello 節點。</span><span class="sxs-lookup"><span data-stu-id="5f693-209">Note that it listens on "http://+", but before OpenAsync returns hello address, hello "+" is replaced with hello IP or FQDN of hello node it is currently on.</span></span> <span data-ttu-id="5f693-210">這個方法所傳回的 hello 位址是向 hello 系統。</span><span class="sxs-lookup"><span data-stu-id="5f693-210">hello address that is returned by this method is what's registered with hello system.</span></span> <span data-ttu-id="5f693-211">它也是用戶端和其他服務要求服務位址時所看到的位址。</span><span class="sxs-lookup"><span data-stu-id="5f693-211">It's also what clients and other services see when they ask for a service's address.</span></span> <span data-ttu-id="5f693-212">如需用戶端 toocorrectly 連接 tooit、 hello 位址中需要實際的 IP 或 FQDN。</span><span class="sxs-lookup"><span data-stu-id="5f693-212">For clients toocorrectly connect tooit, they need an actual IP or FQDN in hello address.</span></span>

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
        this.eventSource.Message("Web server failed tooopen endpoint {0}. {1}", this.endpointName, ex.ToString());

        this.StopWebServer();

        throw;
    }
}

```

<span data-ttu-id="5f693-213">請注意這參考傳入 toohello OwinCommunicationListener hello 建構函式中的 hello 啟動類別。</span><span class="sxs-lookup"><span data-stu-id="5f693-213">Note that this references hello Startup class that was passed in toohello OwinCommunicationListener in hello constructor.</span></span> <span data-ttu-id="5f693-214">Hello web 伺服器 toobootstrap hello Web API 應用程式會使用這個啟動執行個體。</span><span class="sxs-lookup"><span data-stu-id="5f693-214">This startup instance is used by hello web server toobootstrap hello Web API application.</span></span>

<span data-ttu-id="5f693-215">hello`ServiceEventSource.Current.Message()`行稍後會顯示 hello 診斷事件視窗中，當您執行 hello 應用程式 tooconfirm hello 網頁伺服器已順利啟動。</span><span class="sxs-lookup"><span data-stu-id="5f693-215">hello `ServiceEventSource.Current.Message()` line will appear in hello Diagnostic Events window later, when you run hello application tooconfirm that hello web server has started successfully.</span></span>

## <a name="implement-closeasync-and-abort"></a><span data-ttu-id="5f693-216">實作 CloseAsync 和 Abort</span><span class="sxs-lookup"><span data-stu-id="5f693-216">Implement CloseAsync and Abort</span></span>
<span data-ttu-id="5f693-217">最後，實作 CloseAsync 與 Abort toostop hello web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="5f693-217">Finally, implement both CloseAsync and Abort toostop hello web server.</span></span> <span data-ttu-id="5f693-218">hello web 伺服器可以透過處置 OpenAsync 期間所建立的 hello 伺服器控點停止。</span><span class="sxs-lookup"><span data-stu-id="5f693-218">hello web server can be stopped by disposing hello server handle that was created during OpenAsync.</span></span>

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

<span data-ttu-id="5f693-219">實作在本例中，CloseAsync 和中止只會停止 hello web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="5f693-219">In this implementation example, both CloseAsync and Abort simply stop hello web server.</span></span> <span data-ttu-id="5f693-220">您也可以選擇 tooperform CloseAsync hello web 伺服器的更適當地協調關機。</span><span class="sxs-lookup"><span data-stu-id="5f693-220">You may opt tooperform a more gracefully coordinated shutdown of hello web server in CloseAsync.</span></span> <span data-ttu-id="5f693-221">例如，hello 關機無法等候進行中的要求 toobe hello 傳回之前完成。</span><span class="sxs-lookup"><span data-stu-id="5f693-221">For example, hello shutdown could wait for in-flight requests toobe completed before hello return.</span></span>

## <a name="start-hello-web-server"></a><span data-ttu-id="5f693-222">啟動 hello web 伺服器</span><span class="sxs-lookup"><span data-stu-id="5f693-222">Start hello web server</span></span>
<span data-ttu-id="5f693-223">您現在已經準備就緒 toocreate，並傳回 OwinCommunicationListener toostart hello web 伺服器的執行個體。</span><span class="sxs-lookup"><span data-stu-id="5f693-223">You're now ready toocreate and return an instance of OwinCommunicationListener toostart hello web server.</span></span> <span data-ttu-id="5f693-224">在 hello 服務類別 (WebService.cs)，覆寫 hello`CreateServiceInstanceListeners()`方法：</span><span class="sxs-lookup"><span data-stu-id="5f693-224">Back in hello Service class (WebService.cs), override hello `CreateServiceInstanceListeners()` method:</span></span>

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

<span data-ttu-id="5f693-225">這是其中 hello Web API*應用程式*和 hello OWIN*主機*最後符合。</span><span class="sxs-lookup"><span data-stu-id="5f693-225">This is where hello Web API *application* and hello OWIN *host* finally meet.</span></span> <span data-ttu-id="5f693-226">hello 主機 (OwinCommunicationListener) 會指定執行個體的 hello*應用程式*(Web API) 透過 hello 啟動類別。</span><span class="sxs-lookup"><span data-stu-id="5f693-226">hello host (OwinCommunicationListener) is given an instance of hello *application* (Web API) via hello Startup class.</span></span> <span data-ttu-id="5f693-227">然後 Service Fabric 會管理其生命週期。</span><span class="sxs-lookup"><span data-stu-id="5f693-227">Service Fabric then manages its lifecycle.</span></span> <span data-ttu-id="5f693-228">通常可以針對任何通訊堆疊運用相同的模式。</span><span class="sxs-lookup"><span data-stu-id="5f693-228">This same pattern can typically be followed with any communication stack.</span></span>

## <a name="put-it-all-together"></a><span data-ttu-id="5f693-229">組合在一起</span><span class="sxs-lookup"><span data-stu-id="5f693-229">Put it all together</span></span>
<span data-ttu-id="5f693-230">在此範例中，您不需要任何項目在 hello toodo`RunAsync()`方法，因此只會移除覆寫。</span><span class="sxs-lookup"><span data-stu-id="5f693-230">In this example, you don't need toodo anything in hello `RunAsync()` method, so that override can simply be removed.</span></span>

<span data-ttu-id="5f693-231">hello 最終服務實作應該非常簡單。</span><span class="sxs-lookup"><span data-stu-id="5f693-231">hello final service implementation should be very simple.</span></span> <span data-ttu-id="5f693-232">它只需要 toocreate hello 通訊接聽程式：</span><span class="sxs-lookup"><span data-stu-id="5f693-232">It only needs toocreate hello communication listener:</span></span>

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

<span data-ttu-id="5f693-233">完整的 hello`OwinCommunicationListener`類別：</span><span class="sxs-lookup"><span data-stu-id="5f693-233">hello complete `OwinCommunicationListener` class:</span></span>

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
                this.eventSource.Message("Web server failed tooopen endpoint {0}. {1}", this.endpointName, ex.ToString());

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

<span data-ttu-id="5f693-234">既然您已經就地將 hello 的所有項目，您的專案看起來應該像一般 Web API 應用程式使用可靠的服務應用程式開發介面的進入點和 OWIN 主機。</span><span class="sxs-lookup"><span data-stu-id="5f693-234">Now that you have put all hello pieces in place, your project should look like a typical Web API application with Reliable Services API entry points and an OWIN host.</span></span>

## <a name="run-and-connect-through-a-web-browser"></a><span data-ttu-id="5f693-235">透過 Web 瀏覽器執行並連線</span><span class="sxs-lookup"><span data-stu-id="5f693-235">Run and connect through a web browser</span></span>
<span data-ttu-id="5f693-236">如果您尚未這麼做，請 [設定開發環境](service-fabric-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="5f693-236">If you haven't done so, [set up your development environment](service-fabric-get-started.md).</span></span>

<span data-ttu-id="5f693-237">您現在可以建置並部署您的服務。</span><span class="sxs-lookup"><span data-stu-id="5f693-237">You can now build and deploy your service.</span></span> <span data-ttu-id="5f693-238">按**F5**在 Visual Studio toobuild 並部署 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5f693-238">Press **F5** in Visual Studio toobuild and deploy hello application.</span></span> <span data-ttu-id="5f693-239">在 hello 診斷事件視窗中，您應該會看到一個訊息，指出 http://localhost:8281 上開啟該 hello 網頁伺服器 /。</span><span class="sxs-lookup"><span data-stu-id="5f693-239">In hello Diagnostic Events window, you should see a message that indicates that hello web server opened on http://localhost:8281/.</span></span>

> [!NOTE]
> <span data-ttu-id="5f693-240">如果 hello 連接埠已經開啟您的電腦上的另一個處理序，您可能會看到以下錯誤。</span><span class="sxs-lookup"><span data-stu-id="5f693-240">If hello port has already been opened by another process on your machine, you may see an error here.</span></span> <span data-ttu-id="5f693-241">這表示無法開啟該 hello 接聽項。</span><span class="sxs-lookup"><span data-stu-id="5f693-241">This indicates that hello listener couldn't be opened.</span></span> <span data-ttu-id="5f693-242">如果這 hello 案例，請嘗試使用不同的通訊埠 hello ServiceManifest.xml 中的端點組態。</span><span class="sxs-lookup"><span data-stu-id="5f693-242">If that's hello case, try using a different port for hello endpoint configuration in ServiceManifest.xml.</span></span>
> 
> 

<span data-ttu-id="5f693-243">一旦 hello 服務正常執行，請開啟瀏覽器，並瀏覽太[http://localhost:8281/api/值](http://localhost:8281/api/values)tootest 它。</span><span class="sxs-lookup"><span data-stu-id="5f693-243">Once hello service is running, open a browser and navigate too[http://localhost:8281/api/values](http://localhost:8281/api/values) tootest it.</span></span>

## <a name="scale-it-out"></a><span data-ttu-id="5f693-244">相應放大</span><span class="sxs-lookup"><span data-stu-id="5f693-244">Scale it out</span></span>
<span data-ttu-id="5f693-245">向外延展無狀態的 web 應用程式通常表示加入更多電腦，並向上 hello web 應用程式在其上。</span><span class="sxs-lookup"><span data-stu-id="5f693-245">Scaling out stateless web apps typically means adding more machines and spinning up hello web apps on them.</span></span> <span data-ttu-id="5f693-246">Service Fabric 協調流程引擎可以這麼做為您每當 tooa 叢集中加入新的節點。</span><span class="sxs-lookup"><span data-stu-id="5f693-246">Service Fabric's orchestration engine can do this for you whenever new nodes are added tooa cluster.</span></span> <span data-ttu-id="5f693-247">當您建立無狀態服務的執行個體時，您可以指定 hello 數目要 toocreate 的執行個體。</span><span class="sxs-lookup"><span data-stu-id="5f693-247">When you create instances of a stateless service, you can specify hello number of instances you want toocreate.</span></span> <span data-ttu-id="5f693-248">Service Fabric hello 叢集中節點上，將該執行個體數目。</span><span class="sxs-lookup"><span data-stu-id="5f693-248">Service Fabric places that number of instances on nodes in hello cluster.</span></span> <span data-ttu-id="5f693-249">它可確保不 toocreate 多個執行個體的任何一個節點上。</span><span class="sxs-lookup"><span data-stu-id="5f693-249">And it makes sure not toocreate more than one instance on any one node.</span></span> <span data-ttu-id="5f693-250">您也可以指示 Service Fabric tooalways 每個節點上建立執行個體，藉由指定**-1** hello 執行個體計數。</span><span class="sxs-lookup"><span data-stu-id="5f693-250">You can also instruct Service Fabric tooalways create an instance on every node by specifying **-1** for hello instance count.</span></span> <span data-ttu-id="5f693-251">這樣可保證，每當您將節點 tooscale 出您的叢集時，您無狀態服務的執行個體將會建立 hello 新節點上。</span><span class="sxs-lookup"><span data-stu-id="5f693-251">This guarantees that whenever you add nodes tooscale out your cluster, an instance of your stateless service will be created on hello new nodes.</span></span> <span data-ttu-id="5f693-252">這個值是 hello 服務執行個體的屬性，所以它會設定當您建立的服務執行個體。</span><span class="sxs-lookup"><span data-stu-id="5f693-252">This value is a property of hello service instance, so it is set when you create a service instance.</span></span> <span data-ttu-id="5f693-253">您可以透過 PowerShell 設定：</span><span class="sxs-lookup"><span data-stu-id="5f693-253">You can do this through PowerShell:</span></span>

```powershell

New-ServiceFabricService -ApplicationName "fabric:/WebServiceApplication" -ServiceName "fabric:/WebServiceApplication/WebService" -ServiceTypeName "WebServiceType" -Stateless -PartitionSchemeSingleton -InstanceCount -1

```

<span data-ttu-id="5f693-254">您也可以在 Visual Studio 無狀態服務專案中定義預設服務時設定：</span><span class="sxs-lookup"><span data-stu-id="5f693-254">You can also do this when you define a default service in a Visual Studio stateless service project:</span></span>

```xml

<DefaultServices>
  <Service Name="WebService">
    <StatelessService ServiceTypeName="WebServiceType" InstanceCount="-1">
      <SingletonPartition />
    </StatelessService>
  </Service>
</DefaultServices>

```

<span data-ttu-id="5f693-255">如需有關如何 toocreate 應用程式和服務執行個體，請參閱[部署應用程式](service-fabric-deploy-remove-applications.md)。</span><span class="sxs-lookup"><span data-stu-id="5f693-255">For more information on how toocreate application and service instances, see [Deploy an application](service-fabric-deploy-remove-applications.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5f693-256">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5f693-256">Next steps</span></span>
[<span data-ttu-id="5f693-257">使用 Visual Studio 偵錯 Service Fabric 應用程式</span><span class="sxs-lookup"><span data-stu-id="5f693-257">Debug your Service Fabric application by using Visual Studio</span></span>](service-fabric-debugging-your-application.md)

